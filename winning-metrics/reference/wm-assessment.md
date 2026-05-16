# Winning Metrics — Assessment Criteria

Detailed criteria for evaluating each WM level, including what data to gather, what good answers look like, and red flags that need pushing back on.

## Contents

- WM0: Does It Work?
- WM1: Net Promoter Score
- WM2: Retention Asymptote
- WM3: Unit Economics (CACD)
- WM4: Scale
- Product/Market/Channel Fit

---

## WM0: Does It Work?

The product is live and customers use core functionality successfully.

**B2B test:** Does their income statement change materially after you vs before you?

**B2C test:** Does their family thrive far more after they use your product vs before?

This is you proving value. Everything else is premature until this is answered with evidence.

### What data to gather

1. **Is the product live and accessible to real users?** (not just friends/family, not just a demo)
2. **What is the core flow?** (the single thing a user does that delivers value)
3. **What % of users who start the core flow complete it?** (if they don't know, ask for total sessions and total completions in the last 7-30 days)
4. **Where do users drop off?** (which step in the flow loses the most people?)
5. **Can users articulate the value they received?** (qualitative evidence — support emails, tweets, verbal feedback, session recordings)

### Where this data lives

- Core flow completion: app database, product analytics (Mixpanel, Amplitude, PostHog), or server logs
- Qualitative evidence: support inbox, social media mentions, user interviews, session recordings (FullStory, Hotjar)

### Push until you hear

- A specific completion rate with a time range: "47% over the last 30 days"
- A specific drop-off point: "40% drop off at step 3"
- At least one real user quote that articulates value (not "it's cool" — what specifically changed?)
- For B2B: evidence that a customer's business metrics moved
- For B2C: evidence that users' lives improved in a specific way

### Red flags

- "I think most people complete it." — Thinking is not measuring. What's the number?
- "People say it's interesting." — Interesting is not valuable. What did it change for them?
- "We haven't instrumented the funnel yet." — Then WM0 is NOT YET MEASURED. Instrumentation is task #1.
- "Our friends/family love it." — Friends are polite. You need strangers who have no reason to be nice.
- "We're focused on adding features first." — Features on top of a broken core flow make things worse, not better.

### Scoring

- **PASSING:** Product is live, real users complete the core flow at >50% rate, at least some users can articulate value. For B2B: at least one customer's income statement changed. For B2C: at least some users report their life improved.
- **PARTIALLY PASSING:** Product is live and some users complete the flow, but completion rate is low (<50%) or no qualitative evidence of value delivery.
- **NOT YET MEASURED:** Product is live but no instrumentation to measure completion rate.
- **FAILING:** Product is not live, or live but nobody completes the core flow, or users complete it but nobody can articulate any value.

---

## WM1: Net Promoter Score (NPS)

**The question:** "How likely are you to refer [product] to your friends and colleagues?" (0-10 scale)

**Scoring:** NPS = % Promoters (9-10) minus % Detractors (0-6). Passives (7-8) don't count.

**What to do with results:**
- Promoters (9-10): Ask "why?" — These are your marketing messages
- Detractors (0-6): Ask "why?" — These are what you need to fix

**Complement:** Sean Ellis PMF Score — "How would you feel if you could no longer use [product]?" Target: 40%+ say "very disappointed."

**Tools:** Delighted (delighted.com) for NPS capture. PMF Survey (pmfsurvey.com) for Ellis score.

### What data to gather

1. **NPS score** — the number, not a feeling
2. **Sample size** — how many responses?
3. **PMF survey results** — % "very disappointed"
4. **Promoter reasons** — why did they score high?
5. **Detractor reasons** — why did they score low?

### Push until you hear

- A specific NPS number with sample size: "NPS is 45 with 38 responses"
- A specific PMF percentage: "42% said very disappointed"
- Specific promoter reasons you could put on a landing page
- Specific detractor reasons that map to fixable product gaps

### Red flags

- "We haven't measured NPS yet." — That's your first task at WM1. Takes 30 minutes to set up Delighted.
- "We asked 5 people." — Five is noise, not signal. You need 30+ before drawing conclusions.
- "NPS is high but I can't tell you why." — The why matters more than the number. Promoter reasons are your value proposition. Detractor reasons are your roadmap.
- "We surveyed people before they used the product." — NPS before value delivery is meaningless. Survey after core flow completion.
- "People love it!" — Show me the number. Love without measurement is a guess.

### Scoring

- **PASSING:** NPS > 40 with 30+ responses, OR PMF "very disappointed" > 40% with 30+ responses. Can articulate promoter and detractor reasons.
- **PARTIALLY PASSING:** NPS or PMF measured but below threshold, OR strong qualitative evidence of love but no formal survey data.
- **NOT YET MEASURED:** No NPS or PMF survey in place.
- **FAILING:** NPS is negative or PMF "very disappointed" < 20% with adequate sample size.

---

## WM2: Retention Asymptote Chart

**Structure:**
- X-axis: months since acquisition
- Y-axis: % of cohort still active
- Each cohort plotted as a separate line
- Newest cohort = darkest shade, older = lighter

**What to read:**
- **Asymptote height** = what % of acquired users become long-term loyal users. Higher is better.
- **Slope to asymptote** = how quickly non-retainers drop off. Tells you if you're targeting the right audience.
- **Cohort-over-cohort trend** = are you getting better? Newest cohorts with higher asymptotes = improvement.

### What data to gather

1. **User identification method** — auth/login, device fingerprint, payment identity?
2. **Retention event definition** — what counts as "active"? (Must be meaningful, not just "visited")
3. **Retention cohort data** — by week or month, at least 3 cohorts
4. **Asymptote value** — where does the curve flatten?
5. **Cohort-over-cohort trend** — are newer cohorts better or worse?
6. **Churn reasons** — why do users leave?

### Push until you hear

- A specific retention asymptote: "25% of users are still active at 90 days"
- A cohort-over-cohort comparison: "March cohort retained at 28% vs January's 20%"
- A meaningful retention event (not "opened the app" — "completed the core flow again")
- Specific churn reasons from actual churned users

### Red flags

- "We can't identify returning users." — You can't measure retention without user identification. That's task #1 at WM2.
- "Our retention is good." — What's the number? Good compared to what?
- "We look at DAU." — DAU without cohort breakdown hides whether you're getting better or worse.
- "Retention is 90%." — Over what time period? Day 1 retention of 90% is meaningless if day 30 is 5%.
- "We don't know why users leave." — Every churned user is a data point. Have you asked them?

### Scoring

- **PASSING:** Retention asymptote > 20%, improving cohort-over-cohort, and the founder understands why users stay and why they leave.
- **PARTIALLY PASSING:** Some retention data but asymptote < 20%, or no cohort-over-cohort comparison, or no churn analysis.
- **NOT YET MEASURED:** No user identification or no retention tracking in place.
- **FAILING:** Retention asymptote < 10% with no improvement trend, or all cohorts show declining retention.

---

## WM3: Unit Economics (CACD)

**CACD (CAC Doubling Time):** months until cumulative gross margin from a user equals 2× their acquisition cost.

**Key formula:**
```
CACD = months until cumulative_gross_margin(user) ≥ 2 × CAC(user)
```

### What data to gather

1. **Revenue** — MRR/ARR, or revenue model if pre-revenue
2. **CAC by channel** — NOT blended. Per channel.
3. **CACD by channel** — months to recover 2× CAC
4. **LTV/CAC by channel** — target ≥ 5x
5. **Channel testing duration** — how long have you been testing? Weekly A/B tests?
6. **Channel capacity** — can you 2x spend and maintain CACD?

### For B2B companies

Channel is typically a human sales team.

**Key benchmark:** One rep team (~$350K/year fully loaded) should close ~$1M new ARR/year (3× their cost).

**Founder test:** Before hiring reps, founder should act as first rep and hit $7K new MRR for 3 consecutive months.

### Push until you hear

- Per-channel CAC numbers (not blended): "Google Ads CAC is $12, organic is $0, referral is $3"
- A CACD number per channel: "CACD is 6 months on Google Ads"
- An LTV/CAC ratio: "LTV/CAC is 7x on our primary channel"
- Evidence of sustained testing: "We've been running Google Ads for 8 months with weekly A/B tests"

### Red flags

- "Our blended CAC is $8." — Blended CAC hides what's working and what's losing money. Break it out by channel.
- "I'm not tracking channel attribution." — UTM parameters take an hour to set up. That's your first task.
- "We've been running ads for 3 weeks and CAC looks great." — Three weeks is not a channel. It takes ~6 months of systematic testing to know.
- "We're pre-revenue." — You need revenue to calculate unit economics. Even $1/month gives you real data. What's stopping you from charging?
- "Our CAC is zero because it's all word of mouth." — Great, but can you control the volume? If not, you need a scalable channel too.

### Scoring

- **PASSING:** CACD ≤ 8 months AND LTV/CAC ≥ 5x on at least one scalable channel, sustained over 3+ months. You have product/market/channel fit.
- **PARTIALLY PASSING:** Revenue exists and you can calculate CAC, but CACD > 8 months or LTV/CAC < 5x. Or metrics look good but on a non-scalable channel (founder's personal network).
- **NOT YET MEASURED:** Pre-revenue, or revenue exists but no channel-level attribution.
- **FAILING:** CACD > 18 months or LTV/CAC < 2x. You're losing money on every user acquired.

---

## WM4: Scale

### What data to gather

1. **Current ARR/MRR** and monthly growth rate
2. **Unit economics at current spend level** — do CACD and LTV/CAC hold?
3. **Diminishing returns signals** — is CPC rising? Conversion rate falling?
4. **Channel diversification** — how many channels, what happens if primary channel dies?
5. **Next ARR milestone** — $1M → $5M → $30M → $100M

### Push until you hear

- Unit economics at current scale AND at prior (smaller) scale — the comparison matters
- Evidence that increasing spend doesn't degrade CACD
- A diversification plan (not "we'll figure it out when we need to")

### Red flags

- "We're scaling spend and CAC keeps rising." — Diminishing returns. You may have saturated the channel.
- "We only have one channel." — One channel failure away from zero growth. Diversify.
- "Unit economics were great at $10K/month spend but we haven't checked since we went to $50K." — Check. Now.

### Scoring

- **PASSING:** Unit economics hold at current scale, growth rate supports reaching next ARR milestone, channel diversification in place.
- **PARTIALLY PASSING:** Growing but unit economics are degrading at higher spend levels.
- **NOT YET MEASURED:** Haven't scaled spend enough to know if economics hold.
- **FAILING:** Unit economics broke when you scaled. CACD lengthened materially or LTV/CAC dropped below 3x.

---

## Product/Market/Channel Fit

There is product-market fit. Then there is product-market-**channel** fit.

WM0-2 prove product-market fit.
WM3 proves channel fit.
WM0-3 together prove product/market/channel fit.

It isn't enough to have a product that solves a need in a big market — you also need a channel to reach those customers profitably. Only then do you scale (WM4).
