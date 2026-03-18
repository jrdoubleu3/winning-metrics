# Winning Metrics — Playbooks

What to do at each level to graduate to the next. Each playbook covers: what to set up, what to measure, what "good" looks like, common mistakes, and when you've graduated.

## Contents

- WM0 Playbook: Make It Work
- WM1 Playbook: Make Them Love It
- WM2 Playbook: Make Them Stay
- WM3 Playbook: Make the Economics Work
- Viral Channel Playbook
- WM4 Playbook: Scale It
- Fundraising Gates

---

## WM0 Playbook: Make It Work

### Your job at this level
Ship the core experience and prove it delivers value to real users. Nothing else matters yet — not growth, not retention, not monetization.

### What to set up

**Instrumentation (do this before anything else):**
1. Log every user session with a unique session ID
2. Track whether the user completed the core flow (a boolean: did they get to the "aha moment"?)
3. Track where users drop off in the flow (which step was the last one?)
4. Have a way to hear from users — even if it's just an email link or a feedback button

**The core flow definition:**
Write down in one sentence: "A user does [X] and gets [Y]." If you can't write this sentence, you don't have a product yet. Examples:
- "A user enters their financial info and gets their Freedom Age"
- "A user uploads a photo and gets a listing with auto-generated description"
- "A user describes a bug and gets a working fix committed to their repo"

### What to measure
- **Core flow completion rate:** sessions that start / sessions that complete. Target: >50%.
- **Time to value:** how long from first interaction to "aha moment." Shorter is better.
- **Drop-off by step:** which step in the flow loses the most users? That's your #1 fix.

### What "good" looks like
- Real users (not friends/family) are completing the core flow
- At least a few users can explain in their own words what value they got
- For B2B: at least one customer's business metrics changed after using your product
- For B2C: at least a few users say their life is better in some specific way

### Common mistakes at WM0
- **Building features before the core flow works.** If users can't complete the basic flow, adding features makes it worse, not better.
- **Optimizing for metrics you don't have.** Don't think about retention, NPS, or CAC yet. Just make the thing work.
- **Asking friends for feedback.** Friends are polite. You need strangers who have no reason to be nice.
- **Not instrumenting.** "I think users like it" is not data. You need numbers.

### When you've graduated
You can say with evidence: "Real users complete our core flow, and at least some of them can articulate the specific value they received." Move to WM1.

---

## WM1 Playbook: Make Them Love It

### Your job at this level
Turn "it works" into "I'd be upset if this went away." This is the qualitative layer on top of the functional foundation.

### What to set up

**NPS survey — do this first:**

1. Pick a tool: Delighted (delighted.com) is the easiest. Alternatives: Wootric, SatisMeter, Refiner.io, or a simple Typeform.
2. Trigger the survey after the user completes the core flow — not before, not during. They need to have experienced the value before you ask.
3. The question: "How likely are you to recommend [product] to a friend or colleague?" (0-10 scale)
4. **Critical follow-up:** If they score 9-10 (promoter), ask "What's the main reason for your score?" — these answers become your marketing copy. If they score 0-6 (detractor), ask "What would we need to change?" — these answers become your fix list.
5. Collect at least 30 responses before drawing conclusions. Fewer than 30 is noise.

**Where to put the NPS survey:**
- **In-app:** Best response rate. Show it after the core flow completes, not on a separate page. Tools like Delighted and Wootric have in-app SDKs that make this a 30-minute integration.
- **Email:** Good for B2B or products with infrequent usage. Send 24-48 hours after core flow completion. Delighted does this automatically.
- **Don't:** Put it on a landing page, in onboarding, or before the user has experienced value.

**Sean Ellis PMF survey — do this second:**

1. Use pmfsurvey.com or add this question to a Typeform/Google Form: "How would you feel if you could no longer use [product]?" Options: Very disappointed / Somewhat disappointed / Not disappointed / I no longer use it.
2. Target: 40%+ "very disappointed" = you have PMF.
3. Send to users who have used the product at least twice. First-time users haven't formed an opinion yet.

**Lightweight alternative if you're pre-revenue with low traffic:**
If you have <50 users, formal surveys won't give you statistical significance. Instead:
1. Talk to every user who completes the core flow. Email them personally. Get on a 15-minute call.
2. Ask: "What did you get out of it?" and "Would you use it again? Why or why not?"
3. Keep a spreadsheet: user, date, what they said, promoter/neutral/detractor.

### What to measure
- **NPS score:** % promoters (9-10) minus % detractors (0-6). Target: >40.
- **PMF score:** % who say "very disappointed" if the product went away. Target: >40%.
- **Promoter reasons:** cluster the "why" answers. The top 3 reasons are your value proposition.
- **Detractor reasons:** cluster the "why" answers. The top 3 reasons are your roadmap.

### What "good" looks like
- NPS > 40 (world-class is >70)
- PMF "very disappointed" > 40%
- You can complete these sentences with evidence:
  - "Users love us because ___"
  - "Users leave because ___"
  - "If we fixed ___, detractors would become promoters"

### Common mistakes at WM1
- **Measuring NPS before the product works (WM0).** Broken products get bad NPS. Fix the product first.
- **Only listening to promoters.** Detractors are more valuable — they tell you what to fix.
- **Surveying too early in the user journey.** A user who just signed up hasn't experienced enough to give useful feedback.
- **Small sample bias.** 5 responses means nothing. Wait for 30+.
- **Not closing the loop.** Collecting NPS and not acting on it is worse than not collecting it, because it signals you asked but don't care.

### When you've graduated
NPS > 40 with 30+ responses, or PMF "very disappointed" > 40% with 30+ responses. You know what users love and what they want fixed. Move to WM2.

---

## WM2 Playbook: Make Them Stay

### Your job at this level
Prove that users who love your product come back repeatedly. NPS says they love it in the moment — retention proves that love persists.

### What to set up

**User identification (prerequisite):**
You must be able to identify returning users. This requires one of:
- Auth/login (email, OAuth, SSO)
- Device fingerprinting (less reliable but works for anonymous products)
- Payment identity (Stripe customer ID)

If you don't have user identification, setting it up is your first task at WM2. You can't measure retention without it.

**Retention cohort tracking:**

1. **Define your retention event:** What counts as "active"? Be specific. Examples:
   - "Logged in and completed the core flow"
   - "Made a purchase"
   - "Sent a message"
   - Not: "visited the landing page" (too weak) or "opened the email" (too passive)

2. **Build the cohort chart.** Options from easiest to hardest:
   - **Amplitude/Mixpanel/PostHog:** Built-in retention charts. Set up the event tracking, define your retention event, and the chart generates automatically. This is the easiest path — 1-2 hours if you have event tracking in place.
   - **Looker/Metabase/Mode:** SQL-based. Write a cohort query against your database. More flexible but requires SQL knowledge.
   - **Spreadsheet:** For very early stage (<100 users). Export user activity by week, build the cohort table manually in Google Sheets. Template: rows = acquisition week, columns = weeks since acquisition, cells = % still active.
   - **Custom SQL:** If you have a Postgres/MySQL database with user events, the query pattern is:

```sql
-- Retention cohort query template
-- Replace [events_table], [user_id_col], [event_date_col] with your schema
WITH user_cohorts AS (
  SELECT
    [user_id_col],
    DATE_TRUNC('week', MIN([event_date_col])) AS cohort_week
  FROM [events_table]
  GROUP BY [user_id_col]
),
activity AS (
  SELECT
    e.[user_id_col],
    uc.cohort_week,
    DATE_TRUNC('week', e.[event_date_col]) AS activity_week,
    EXTRACT(DAYS FROM DATE_TRUNC('week', e.[event_date_col]) - uc.cohort_week) / 7 AS weeks_since
  FROM [events_table] e
  JOIN user_cohorts uc ON e.[user_id_col] = uc.[user_id_col]
)
SELECT
  cohort_week,
  weeks_since,
  COUNT(DISTINCT [user_id_col]) AS active_users,
  ROUND(
    100.0 * COUNT(DISTINCT [user_id_col]) /
    MAX(COUNT(DISTINCT [user_id_col])) OVER (PARTITION BY cohort_week),
    1
  ) AS retention_pct
FROM activity
GROUP BY cohort_week, weeks_since
ORDER BY cohort_week, weeks_since;
```

3. **Plot it.** X-axis = weeks/months since acquisition. Y-axis = % retained. One line per cohort. Darkest line = newest cohort.

### What to measure
- **Retention asymptote:** Where does the curve flatten? This is the % of users who become long-term loyal.
- **Cohort-over-cohort trend:** Are newer cohorts retaining better than older ones? If yes, your product is improving.
- **Time to asymptote:** How many weeks until the curve flattens? Faster = better targeting of the right users.
- **DAU/MAU ratio:** Quick proxy if you don't have cohort charts yet. >20% is decent for most products. >50% is exceptional.

### What "good" looks like
- Retention asymptote >20% (meaning 20%+ of acquired users become long-term)
- Newer cohorts have higher asymptotes than older cohorts (you're improving)
- You know why retained users stay (interview them) and why churned users left (exit survey)

### How to improve retention
- **Find your "aha moment":** What do retained users do that churned users don't? (Facebook's was "7 friends in 10 days." What's yours?)
- **Shorten time to aha moment:** The faster users experience value, the more likely they retain.
- **Build re-engagement hooks:** Email/push triggers when something changes that matters to the user. (For a financial planning tool: "Your Freedom Age changed because markets moved — check your updated plan.")
- **Attack markets where incumbents have negative NPS.** Your customer obsession on retention is the moat.

### Common mistakes at WM2
- **Measuring retention before proving love (WM1).** If NPS is negative, users aren't coming back regardless of what you build.
- **Using vanity retention metrics.** "Opened the app" is not retention. "Completed the core flow again" is retention.
- **Only looking at aggregate retention.** Break it down by cohort. Aggregate hides whether you're getting better or worse.
- **Not investigating churn.** Every churned user is a data point. Ask them why they left.

### When you've graduated
Retention asymptote >20%, improving cohort-over-cohort, and you understand why users stay and why they leave. Move to WM3.

---

## WM3 Playbook: Make the Economics Work

### Your job at this level
Prove that you can acquire users for less than they're worth. This is where 99% of startups fail — the product works, users love it, but there's no cost-effective way to reach them at scale.

### What to set up

**Revenue (if you don't have it yet):**
You need revenue to calculate unit economics. If you're pre-revenue:
1. Pick a pricing model. For most software: subscription.
2. Start charging. Even $1/month gives you real data. Free-to-paid conversion rate is the most important number you don't have.
3. If you can't charge yet, model it: what would users pay? Multiply by your expected conversion rate. Use this as a rough LTV estimate.

**Channel tracking:**
1. **Separate CAC by channel.** Google Ads CAC is different from referral CAC is different from content CAC. Never blend them — blended CAC hides what's working and what's not.
2. **Set up UTM parameters** on all acquisition links. UTMs flow through to your analytics tool and let you trace each user back to their source.
3. **Connect acquisition to revenue.** You need to be able to say: "This user came from Google Ads, and they've paid us $X over their lifetime." This usually means connecting your ad platform → your app → your billing system (Stripe). Tools like Segment or a simple database join can do this.

**CACD calculation:**

For each channel:
```
1. CAC = total spend on channel / paying users acquired through channel
2. Monthly gross margin per user = ARPU × gross margin %
3. CACD = months until cumulative GM ≥ 2 × CAC
4. LTV = monthly gross margin × average customer lifetime in months
5. LTV/CAC = LTV / CAC
```

### For B2C companies: channel-specific playbook

**Google Ads:**
- Start at $20-50/day. Enough to get statistically significant data, not enough to waste.
- Track: cost per click (CPC), click-to-signup rate, signup-to-paid rate, CAC
- Good Google Ads CAC varies wildly by industry. The question isn't "is my CAC good" — it's "is my CACD ≤ 8 months?"
- If CPC is rising quarter over quarter, the channel may be saturating.

**Meta/Facebook Ads:**
- Same structure as Google. Start small, track per-channel.
- Warning: CPCs have roughly doubled in the last 1-2 years. Budget accordingly.
- If Meta works, go for it. But have a backup channel.

**Content/SEO:**
- Slowest to produce results (3-6 months), but lowest marginal CAC once it works.
- CAC calculation is tricky: count your time/contractor costs as the investment.

**Referral/word-of-mouth:**
- Lowest CAC (often $0). But you can't control the volume.
- If NPS is high (WM1), this should be generating some organic growth. If it's not, your share mechanics are broken.

**Scale path:** When you reach $1M/month in ad spend, test digital TV. The combination of TV + digital is working for companies at that scale.

### For B2B companies: channel-specific playbook

**The founder-as-first-rep test:**
Before hiring a single salesperson, the founder acts as the first rep. Target: close $7K new MRR for 3 consecutive months. If the founder can't sell it, a hired rep won't either.

**First reps:**
- Hire 2 reps (not 1 — you need to see if the process works independent of one person).
- Fully loaded cost per rep team: ~$350K/year (AE + SDR + lead gen + fraction of SE).
- Target per team: ~$1M new ARR/year (3× their cost).
- Monitor for 6 months before concluding the channel works.

**Scale path:** 2 reps → 4 → 8 → 16. Re-verify the 3× ratio at each doubling.

### What to measure
- **CACD per channel** — the #1 metric. Target: ≤ 8 months.
- **LTV/CAC per channel** — Target: ≥ 5x.
- **Payback period** — months to recover 1× CAC (this is your cash flow reality).
- **Channel capacity** — can you 2x spend and maintain CACD? If not, the channel is saturated.

### What "good" looks like
- CACD ≤ 8 months on at least one scalable channel
- LTV/CAC ≥ 5x
- You've tested the channel for at least 6 months with systematic weekly A/B testing
- You understand what creative/targeting/messaging works and why

### Common mistakes at WM3
- **Spending on growth before WM1 (love) is proven.** You'll acquire users who churn.
- **Blending CAC across channels.** Hides what's working.
- **Giving up too early on a channel.** It takes ~6 months of systematic testing to know if a channel works. Weekly A/B tests, not monthly guesses.
- **Only testing one channel.** Test 2-3 in parallel.
- **Ignoring organic/referral.** If NPS is high and organic growth is zero, your share mechanics are broken.

### When you've graduated
CACD ≤ 8 months and LTV/CAC ≥ 5x on at least one scalable channel, sustained over 3+ months. You have product/market/channel fit. Move to WM4.

---

## Viral Channel Playbook

Viral adoption is the best possible channel: zero CAC means instant CACD.

### Two prerequisites
1. **Is the product more useful if your friends also use it?** (network effects)
2. **Have you made it easy to share?** (mechanics)

Both must be true. If #1 is weak, no amount of share buttons will make it viral.

### K-factor calculation
```
k = (% users who invite) × (invites per inviter) × (% invited who click) × (% clickers who convert)
```
Target: k ≥ 1.1 = exponential growth.

**Worked example:** Say 50% of site visitors register, 20% become inviters, they send 5 invites, and 20% of those invites become site visitors. Your k-factor is: 50% × 20% × 5 × 20% = 0.1 — one-tenth of what you need to grow exponentially.

To fix it, look at each multiplier: Can you get inviters to send 25 invites instead of 5 via address book integration or easy writes to social media? Can you make inviting part of the standard flow so 40% become inviters instead of 20%? Each bottleneck in the loop is a leverage point.

**Growth formula:**
```
end_of_month_users = beginning_users × (1 + k)^(loops_per_month)
```
If k = 1 and each loop takes 15 days (2 loops/month), you 4× your users monthly — for free. This is why viral is the most powerful channel: zero CAC, instant CACD.

If your service isn't inherently more useful when friends are on it, it will be hard to force virality. But if it is inherently viral, focus R&D resources here to get k over 1.0 before investing in paid channels.

### How to find and fix bottlenecks
1. Print/screenshot every screen in your product
2. Tape them to a wall or whiteboard
3. Draw the viral loop: where does a user invite others? Where does the invitee land? What's their path to becoming a user?
4. Make sure the loop is closed end-to-end
5. Measure each step's conversion rate
6. The step with the lowest conversion is your bottleneck — A/B test to improve it

### Design for virality from day 1
With AI, it's never been easier to have short CACDs. Don't bolt on virality later — design network effects and sharing into the core product experience from the start.

---

## WM4 Playbook: Scale It

### Your job at this level
Pour fuel on the fire. You've proven the product works, users love it, they stick around, and you can acquire them cost-effectively. Now the question is how fast you can grow.

### What to set up
- **Real-time CACD monitoring** per channel, per cohort, per time period
- **Diminishing returns alerting:** flag when CPC or CAC rises >20% month-over-month
- **Channel diversification:** test 1-2 new channels for every one you're scaling

### Milestones
$1M ARR → $5M → $30M → $100M. At each doubling of spend, re-verify unit economics hold.

### Scale path by CACD

**If CACD is short (≤4 months):**
- Get to breakeven fast
- Grow at breakeven — minimal dilution
- Potentially reach $100M ARR without raising past seed
- You'll own most of your company at IPO

**If CACD is long (8-18 months, common in SaaS):**
- Pre-seed: Get WM0-3 working, reach ~$40K MRR
- Seed: Scale to $3M ARR
- Series A: Scale to $15M ARR
- Series B, C: Continue scaling
- IPO at $100M ARR run-rate

---

## Fundraising Gates

Walk into an investor meeting with these metrics proven and you are fundable at each stage:

| Stage | What to prove | Typical milestone |
|-------|--------------|-------------------|
| Pre-seed | WM0 + early WM1 signals | Product works, some users love it |
| Seed | WM0-WM2 + early WM3 signals | Product works, users love it, some stick, channel experiments running |
| Series A | WM0-WM3 proven | Product/market/channel fit, $3M+ ARR |
| Series B+ | WM4 in progress | Unit economics hold at scale, $15M+ ARR |

Each successive round of investment is just funding more of what's already working on the CAC spend. If your CACD is short, you need fewer rounds and less dilution.
