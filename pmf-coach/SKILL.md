---
name: pmf-coach
description: Zero-to-one product-market fit coach that reads user logs from your database and proposes the next most valuable feature to ship. Use when reviewing conversation logs, analyzing user drop-off, deciding what to build next, prioritizing the backlog, analyzing user behavior patterns, interpreting feedback signals, running a PMF review session, or any variant of "what should we ship next." Also triggers on "review logs," "analyze sessions," "what are users doing," "where are users dropping off," "PMF review," or "iterate." This is the most important skill for product decisions — use it aggressively.
---

# PMF Coach

A 0→1 product-market fit iteration coach. Treats PMF as a search problem: each feature shipped is a guess, each batch of user sessions is a signal. The goal is to narrow the search space as fast as possible.

## Core Mental Model

PMF iteration is "guess the number":

1. **The number** = the product configuration where users say "I'd be very disappointed if this went away"
2. **Each ship** = a guess
3. **User behavior** = the "higher/lower" signal
4. **This skill** = helps you read the signal and pick the next guess that maximally narrows the search space

The worst thing you can do is ship features that don't generate signal. Every change should be designed to learn something.

## How to Use This Skill

### The PMF Review Session

Run this whenever you have a new batch of user data (weekly minimum, daily when possible). The workflow:

1. **Pull data** — Export recent sessions from your database (see [reference/query-patterns.md](reference/query-patterns.md) for example queries)
2. **Read the signals** — Classify each session using the signal taxonomy (see below)
3. **Identify the constraint** — What's the #1 thing preventing users from getting value?
4. **Propose the next ship** — The feature that would remove that constraint AND generate the most signal for the next iteration
5. **Define the success metric** — Before building, state what behavior change you expect to see

### Signal Taxonomy

Every user session produces one of these signals. Read them in this priority order:

**Strongest signals (behavior > words):**
- **Completed and returned** — They got value AND came back. These users are your PMF signal. Study what they have in common.
- **Completed and never returned** — They got the result but it wasn't compelling enough to revisit. The product worked but didn't create a habit or need.
- **Abandoned mid-flow** — The exact turn where they stopped is the most valuable data point you have. What was the last thing the product said? What was it asking for?
- **Abandoned after result** — They saw the result but didn't explore further. The result didn't create enough curiosity or urgency.
- **Error/failure** — Technical failures that prevented value delivery. Fix these first — they're blocking signal.

**Supporting signals (words + actions):**
- **Thumbs up/down** — Directional, not diagnostic. A thumbs-down on a specific turn tells you more than a thumbs-down at the end.
- **Explicit feedback** — Rare but gold. What users type unprompted is highest-fidelity signal.
- **Feature engagement** — Which features do users interact with? Which do they ignore? Engagement = relevance.
- **Question patterns** — What do users ask that the product can't answer? These are feature candidates.
- **Scenario exploration** — Users who explore "what if" scenarios are deeply engaged. What scenarios do they try?

### The Constraint Hierarchy

When diagnosing the #1 constraint, work through this hierarchy top to bottom. The first failing level is your constraint — don't optimize lower levels until you fix it:

1. **Can users complete the core flow?** (Technical: errors, timeouts, confusing UX)
2. **Do users understand what they got?** (Comprehension: is the result clear?)
3. **Do users believe what they got?** (Trust: do they trust the math, the assumptions, the output?)
4. **Do users care about what they got?** (Relevance: is this the thing they actually wanted to know?)
5. **Do users want more?** (Engagement: does the result create demand for deeper interaction?)
6. **Do users tell others?** (Advocacy: is the experience remarkable enough to share?)

### Feature Prioritization Framework

For each candidate feature, score on two axes:

**Signal value** (will this help us learn faster?):
- Does it test a hypothesis about what users want?
- Will the behavior change be measurable with current instrumentation?
- Does it generate data even if the feature fails?

**User value** (will this remove the #1 constraint?):
- Does it directly address the constraint identified above?
- How many users does it affect? (% of sessions hitting this constraint)
- How severe is the constraint? (abandonment vs mild friction)

**The best feature to ship scores high on both.** A feature that removes the constraint but generates no signal is a guess in the dark. A feature that generates signal but doesn't address the constraint is research, not product work.

### Anti-Patterns

- **Shipping features nobody asked for** — If no user behavior or question points to this need, you're guessing without a signal. Save it for later.
- **Optimizing what works instead of fixing what's broken** — Polishing the result page when 40% of users abandon before getting a result.
- **Building for power users before fixing the core flow** — Advanced scenarios when basic flow has 30% completion rate.
- **Treating all feedback equally** — A user who completed 10 sessions and gives feedback is 10x more valuable than a one-turn bouncer.
- **Shipping without a success metric** — If you can't state "after this ships, I expect X metric to change by Y," you don't understand the problem well enough.

## Data Sources

See [reference/query-patterns.md](reference/query-patterns.md) for example database queries and behavioral signal patterns.

## Integration with Other Skills

- **winning-metrics** — PMF coach operates at WM0-WM1 (does it work? do they love it?). Once PMF is found, winning-metrics WM2-WM4 takes over for retention and scaling.
