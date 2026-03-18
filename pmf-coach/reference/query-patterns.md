# PMF Coach — Query Patterns & Signal Reference

## Part 1: Example Database Queries

Adapt these queries to your own database schema. They assume a conversation-based product with session tracking.

### Session Overview

Start every PMF review with this. Gives you the shape of the data.

```sql
-- Session summary: total sessions, completion rate, avg depth
SELECT
  COUNT(DISTINCT session_id) AS total_sessions,
  COUNT(DISTINCT session_id) FILTER (
    WHERE session_id IN (
      SELECT DISTINCT session_id FROM calculation_history
      WHERE tool_name = 'your_core_action'
    )
  ) AS completed_sessions,
  ROUND(AVG(turn_count), 1) AS avg_turns,
  COUNT(DISTINCT session_id) FILTER (
    WHERE turn_count >= 3
  ) AS engaged_sessions
FROM (
  SELECT session_id, COUNT(*) AS turn_count
  FROM conversation_logs
  WHERE created_at >= NOW() - INTERVAL '7 days'
  GROUP BY session_id
) session_stats;
```

### Drop-off Analysis

The most valuable query. Shows exactly where users stop.

```sql
-- Last turn per abandoned session (no core action completed)
SELECT
  cl.session_id,
  cl.turn_number,
  cl.assistant_message,
  cl.user_message,
  cl.created_at
FROM conversation_logs cl
WHERE cl.session_id NOT IN (
  SELECT DISTINCT session_id FROM calculation_history
  WHERE tool_name = 'your_core_action'
)
AND cl.turn_number = (
  SELECT MAX(turn_number) FROM conversation_logs cl2
  WHERE cl2.session_id = cl.session_id
)
AND cl.created_at >= NOW() - INTERVAL '7 days'
ORDER BY cl.created_at DESC;
```

**How to read this:** The `assistant_message` on the last turn tells you what the product was asking when the user left. Cluster these by what the product was requesting to find the friction point.

### Engagement Depth Distribution

```sql
-- How deep do sessions go? Histogram of turn counts.
SELECT
  CASE
    WHEN turn_count = 1 THEN '1 (bounce)'
    WHEN turn_count = 2 THEN '2 (shallow)'
    WHEN turn_count BETWEEN 3 AND 5 THEN '3-5 (engaged)'
    WHEN turn_count BETWEEN 6 AND 10 THEN '6-10 (deep)'
    ELSE '11+ (power user)'
  END AS depth_bucket,
  COUNT(*) AS session_count,
  ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER (), 1) AS pct
FROM (
  SELECT session_id, COUNT(*) AS turn_count
  FROM conversation_logs
  WHERE created_at >= NOW() - INTERVAL '7 days'
  GROUP BY session_id
) s
GROUP BY 1
ORDER BY MIN(turn_count);
```

### Feedback Signals

```sql
-- Thumbs up/down with the turn they're attached to
SELECT
  f.session_id,
  f.feedback_type,
  f.created_at,
  cl.turn_number,
  cl.assistant_message,
  cl.user_message
FROM feedback f
LEFT JOIN conversation_logs cl
  ON cl.session_id = f.session_id
  AND cl.id = f.message_id
WHERE f.created_at >= NOW() - INTERVAL '7 days'
ORDER BY f.created_at DESC;
```

### Completion Funnel

```sql
-- Funnel: sessions → engaged → core action completed → explored further
WITH session_turns AS (
  SELECT session_id, COUNT(*) AS turns
  FROM conversation_logs
  WHERE created_at >= NOW() - INTERVAL '7 days'
  GROUP BY session_id
),
core_completions AS (
  SELECT DISTINCT session_id
  FROM calculation_history
  WHERE tool_name = 'your_core_action'
    AND created_at >= NOW() - INTERVAL '7 days'
),
explorations AS (
  SELECT DISTINCT session_id
  FROM calculation_history
  WHERE tool_name IN ('your_secondary_action_1', 'your_secondary_action_2')
    AND created_at >= NOW() - INTERVAL '7 days'
)
SELECT
  COUNT(*) AS total_sessions,
  COUNT(*) FILTER (WHERE turns >= 3) AS engaged,
  COUNT(*) FILTER (WHERE st.session_id IN (SELECT session_id FROM core_completions)) AS completed_core,
  COUNT(*) FILTER (WHERE st.session_id IN (SELECT session_id FROM explorations)) AS explored_further
FROM session_turns st;
```

### User Questions the Product Can't Answer

```sql
-- User messages where no tool was called in the assistant response
SELECT
  cl.user_message,
  cl.assistant_message,
  cl.session_id,
  cl.turn_number
FROM conversation_logs cl
WHERE cl.tools_called IS NULL
  AND cl.user_message IS NOT NULL
  AND LENGTH(cl.user_message) > 20
  AND cl.created_at >= NOW() - INTERVAL '7 days'
ORDER BY cl.created_at DESC
LIMIT 50;
```

**How to read this:** Cluster these user messages by theme. Common themes = feature candidates.

### Cohort Comparison

Compare behavior between two time periods to see if a change helped.

```sql
-- Before/after comparison (adjust dates for your ship)
WITH before_period AS (
  SELECT session_id, COUNT(*) AS turns
  FROM conversation_logs
  WHERE created_at BETWEEN 'YYYY-MM-DD' AND 'YYYY-MM-DD'
  GROUP BY session_id
),
after_period AS (
  SELECT session_id, COUNT(*) AS turns
  FROM conversation_logs
  WHERE created_at BETWEEN 'YYYY-MM-DD' AND 'YYYY-MM-DD'
  GROUP BY session_id
)
SELECT
  'before' AS period,
  COUNT(*) AS sessions,
  ROUND(AVG(turns), 1) AS avg_turns,
  COUNT(*) FILTER (WHERE turns >= 3) AS engaged
FROM before_period
UNION ALL
SELECT
  'after',
  COUNT(*),
  ROUND(AVG(turns), 1),
  COUNT(*) FILTER (WHERE turns >= 3)
FROM after_period;
```

---

## Part 2: Signal Patterns

A catalog of behavioral patterns to watch for when analyzing user sessions.

### Positive Signals

**Scenario exploration after result** — User gets a result, then asks "what if" questions. Deep engagement. They're using the product as a thinking tool, not just a calculator. Measure: number of scenarios explored per session.

**Return visit with updated inputs** — User comes back and changes their inputs. They're treating it as their planning tool. This is retention behavior. Measure: time between visits, what input changed.

**Partner sharing** — User mentions a partner, uses "we" language, or asks about household planning. The product has expanded to a conversation between partners. This is viral potential.

**Trust verification** — User asks "how does this work?" or "what assumptions are you using?" Positive skepticism — they care enough to challenge. Skeptical users who get satisfying answers become the strongest advocates.

### Negative Signals

**Input abandonment** — User stops responding when asked for a specific input. That input is either too sensitive, too hard to recall, or feels irrelevant. Measure: abandonment rate per input field.

**Single-turn bounce** — User sends one message and never sends a second. The opening experience didn't match their expectation or the first response was off-putting. Measure: cluster first-message intents.

**Result without reaction** — User gets a result and the session ends immediately. The result didn't create urgency, surprise, or curiosity. It landed flat. Measure: % of sessions that end within 1 turn of result delivery.

**Repeated action with same inputs** — User tries to re-trigger the core action without changing anything. They didn't understand the result, don't trust it, or think they'll get a different answer.

### Ambiguous Signals

**Short polite engagement** — User goes through 4-5 turns, gives basic inputs, gets a result, says "thanks" and leaves. Could be satisfied or politely disappointed. Need NPS or follow-up to disambiguate. Measure: do these users return?

**Very long sessions (15+ turns)** — Could be power-user exploration (positive) or confused/stuck in a loop (negative). Check if turns are progressive (new ground) or repetitive (circling).

### Silence as Signal

When you present something and the user goes silent, that silence tells you something specific:

- **Silence after asking for sensitive input** — Too personal to share
- **Silence after result delivery** — Result didn't land (confusion, disbelief, or irrelevance)
- **Silence after feature reveal** — That feature wasn't relevant to them
- **Silence after suggestion** — They don't want to explore, they wanted a single answer

Treat silence with the same analytical rigor as explicit feedback.

### Common Drop-off Patterns

| Drop-off point | Likely cause | Likely fix type |
|---|---|---|
| Turn 1 (bounce) | Expectation mismatch from ad/landing page | Ad copy or landing page change |
| Turn 2-3 (early abandon) | Opening conversation not compelling | System prompt change |
| Sensitive input question | Privacy concern or recall difficulty | Offer ranges instead of exact numbers |
| After result delivery | Result not compelling or unclear | Result presentation change |
| During exploration | Overwhelmed by options | Narrow to 1-2 most impactful options |

**The fix type matters.** Most drop-off fixes are prompt changes, not code changes. Before building a new feature, ask: could a prompt change fix this drop-off?
