# Winning Metrics — Playbooks

## Contents

- WM3: CAC Doubling Time (CACD) & Unit Economics
- Viral Channel Design
- WM4: Scaling Working Unit Economics
- Timelines & Fundraising Gates
- B2B-Specific Benchmarks

---

## WM3: CAC Doubling Time (CACD) & Unit Economics

This is where 99% of startups fail. The product works, but they can't get it to market cost-effectively.

### The Value Chain

1. **Value delivered** to customer (measured at WM0)
2. **Price** ≈ 10% of value delivered
3. **Gross margin** = price minus cost of goods sold
4. **CAC** = cost to acquire one customer through a given channel
5. **CACD** = months for cumulative gross margin from one customer to reach 2× their CAC

### The Formula

```
CACD = months until: cumulative_gross_margin(customer) ≥ 2 × CAC(customer)
```

### Benchmarks

- CACD ≤ 8 months + LTV/CAC ≥ 5x = great business
- Every month you shave off CACD = meaningfully better business
- Shorter CACD = less VC needed, faster to $100M revenue, more ownership at IPO

### For B2C Companies

**Channels:** Google ads, Facebook ads, affiliate/influencers, TikTok shop, etc.

**Measure per channel:**
1. CAC through that channel (cost per acquired user)
2. Monthly gross margin per user
3. Months to recover 2× CAC
4. Cumulative gross margin over customer lifetime (LTV)
5. LTV/CAC ratio

**Channel warning (as of ~2024-2026):** Facebook CPCs have doubled in the last year. If they double again, most B2C VC-backed startups can't use Facebook as a channel. Google Ads may have similar dynamics. Monitor CPCs weekly.

**Scale path:** When you hit $1M/month ad spend, start testing digital TV. TV is targetable now and the combo of TV + digital is working for companies at $1M+ monthly spend.

### For B2B Companies

**Channel:** Human sales rep teams.

**Unit of investment:** ~$350K/year per rep team (AE + SDR + lead gen + fraction of SE).

**Target:** Rep team hitting quota sells ~$1M new ARR/year (3× their cost).

**Math breakdown:**
- $1M new ARR/year = ~$80K new ARR/month = ~$7K new MRR/month
- Not all reps hit quota, plus 3-month ramp, plus S&M leadership overhead
- Net result: $1 of S&M spend → $1 of new ARR (the Salesforce math)
- 2× that efficiency = outstanding

**Founder test:** Before hiring reps, founder acts as first rep. Hit $7K new MRR for 3 consecutive months. Then you're ready to add reps. Scale 2 → 4 → 8 → 16, monitoring 3× ratio at each doubling.

### CACD as the Buffett Test

CACD is essentially the Buffett "good business" test translated to startups. A business where $1 invested in S&M returns $2 quickly is a business with a durable competitive advantage in its distribution channel.

---

## Viral Channel Design

Viral adoption is the best channel: zero CAC means zero-day CACD.

### Two Key Questions

1. **Is the service more useful to a user if their friends also use it?** (network effects)
2. **Do you make it easy to share?** (mechanics)

Both must be yes for viral growth potential.

### K-Factor Calculation

```
k_factor = % users who invite × invites per inviter × % of invited who click × % of clickers who convert
```

**Target:** k-factor ≥ 1.1 = exponential growth.

### How to Optimize

1. Print screenshots of every page/screen
2. Tape to whiteboard
3. Circle the CTA that drives conversion to next step
4. Draw lines showing the flow
5. Ensure the viral loop is end-to-end closed
6. Track each step, find bottlenecks
7. A/B test to remove bottlenecks

### Design for Virality from Day 1

With AI, it's never been easier to have short CACDs. Design network effects and virality into the product from day 1 — don't bolt it on later.

---

## WM4: Scaling Working Unit Economics

Once WM0-3 all work, move to WM4: scaling.

**Milestones:** $1M ARR → $5M → $30M → $100M ARR

**At each milestone:**
- Re-verify unit economics still hold
- Monitor CACD at increased spend levels
- Watch for channel saturation (diminishing returns at higher spend)
- Expand to adjacent channels when primary channel shows fatigue

---

## Timelines & Fundraising Gates

**WM1/WM2 to WM3 timeline:** Plan ~6 months of systematic weekly A/B testing to prove or disprove cost-effective, scalable channels.

**If CACD is short:**
- Get to breakeven fast
- Grow at breakeven
- Minimal dilution from VC rounds
- Get to $100M revenue fast, own most of your company at IPO

**If CACD is long (common in SaaS):**
- Pre-seed: Get WM0-3 working, reach ~$40K MRR
- Seed: Scale to $3M ARR
- Series A: Scale to $15M ARR
- Series B, C: Continue scaling
- IPO at $100M ARR run-rate

**Fundraising pitch:** If you walk into an investor meeting with strong NPS, strong retention, and short CAC doubling times — you are fundable. Each successive round just funds more of what's already working.
