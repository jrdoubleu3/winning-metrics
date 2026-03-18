---
name: pmf-coach
description: Zero-to-one product-market fit coach that reviews user data and proposes the next most valuable thing to ship. Use when reviewing user logs, analyzing drop-off, deciding what to build next, prioritizing the backlog, analyzing user behavior, interpreting feedback, running a PMF review, or any variant of "what should we ship next." Also triggers on "review logs," "analyze sessions," "what are users doing," "where are users dropping off," "PMF review," "iterate," "what should I build," or "what's the most important thing right now." Works with any tech stack — Supabase, Postgres, Firebase, Mixpanel, Amplitude, or raw exports. This is the most important skill for product decisions — use it aggressively.
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

The companies that learn fastest in a market are the ones that win. Reid Hoffman is the best at playing startup "guess the number" — not because he guesses better initially, but because he instruments to learn maximum information per iteration, runs experiments faster than anyone, and learns from competitors' R&D spend too. He's shown repeatedly that you don't need to be first to market — you need to get to the right answer faster.

### The Three Failure Modes

When reviewing user data, diagnose which failure mode you're in:

1. **Stuck at 49/51.** You launched at 50, got feedback, but only moved to 49 or 51. You're making tiny incremental changes instead of meaningful experiments. The signal told you "higher" and you moved by 1 instead of 25. This usually means you're too attached to your current implementation to make the bold change the data is telling you to make.

2. **Restarting at 50.** Your first product didn't work perfectly, so you scrapped it, built a new MVP, and started over — guessing 50 again, three months later. You threw away everything you learned. The right move was to use the signal from the first attempt to make a big informed jump, not to start fresh.

3. **Random guessing.** You're not instrumented well enough to know if you're getting warmer or colder. You're trying random numbers between 1 and 100 hoping to get lucky. This is the most common failure mode — founders who don't invest in analytics are playing blind.

If you catch yourself in any of these modes, name it explicitly in the review and recommend the correction.

### Engagement Before Growth

First-time founders try to get growth working before they get engagement working. This is backwards. Start with engagement: do users who find your product find they can't live without it? Listen to early users and remove problems that keep them from loving your service. Often if you do just one or two things amazingly well, that is enough. Don't give users 100 features — give them a few they can't live without first.

Only after engagement is proven should you work on growth/distribution. The constraint hierarchy below enforces this: levels 1-5 are about engagement, level 6 is about advocacy/growth.

### The Entry→Payoff Framework

Define two activities and the path between them:

- **Entry activity:** The first thing a user does (visits the site, sends first message, uploads a file)
- **Payoff activity:** The moment the user gets value (receives their result, makes a purchase, has their problem solved)
- **Steps in between:** Every intermediate step the user takes to get from entry to payoff

Measure conversion at each step. The fewer intermediate steps, the better. Remove activities that distract from reaching the payoff. Add or modify features to optimize conversion to the payoff activity. This is more specific than a generic funnel — it forces you to name the exact moment value is delivered and measure everything relative to that.

## How to Use This Skill

### First time: Set up your data access

Before the first review, ask the founder:
1. **What's your database/analytics tool?** (Supabase, Postgres, Firebase, Mixpanel, Amplitude, PostHog, or something else)
2. **What tables/events track user sessions?** (table names, key columns)
3. **What's the "core flow completion" event?** (how do you know a user got value?)
4. **What feedback mechanisms exist?** (thumbs up/down, NPS, ratings, surveys, support emails)
5. **Can Claude Code connect directly?** (connection string, API key) Or should the founder export data?

Then generate product-specific query templates. See [reference/query-patterns.md](reference/query-patterns.md) for the universal patterns to adapt.

### The PMF Review Session

Run this whenever you have a new batch of user data (weekly minimum, daily when possible):

1. **Pull data** — Use the query patterns adapted to the founder's stack
2. **Read the signals** — Classify each session using the signal taxonomy (see below)
3. **Identify the constraint** — What's the #1 thing preventing users from getting value?
4. **Propose the next ship** — The feature that removes that constraint AND generates signal
5. **Define the success metric** — Before building, state what behavior change you expect

### Signal Taxonomy

Every user session produces one of these signals. Prioritize behavioral signals over stated preferences — what users do is more reliable than what they say.

**Strongest signals (behavior):**
- **Completed and returned** — Got value AND came back. Study what these users have in common.
- **Completed and never returned** — Product worked but wasn't compelling enough to revisit.
- **Abandoned mid-flow** — The exact step where they stopped is your most valuable data point.
- **Abandoned after result** — Saw the output but didn't engage further. Result landed flat.
- **Error/failure** — Technical failures blocking value delivery. Fix these first.

**Supporting signals (words + actions):**
- **Explicit feedback** — What users type unprompted is highest-fidelity signal.
- **Thumbs up/down** — Directional, not diagnostic. Most useful when tied to a specific interaction.
- **Feature requests** — What users ask for that the product can't do. Cluster by theme.
- **Comparison to alternatives** — When users mention competitors or workarounds, they're telling you what "good enough" looks like.

**Silence as signal:**
When you present something and the user goes silent, that's data. The product offered something and the user decided it wasn't worth responding to. Silence after a core result delivery is especially important — it means the result didn't create urgency, surprise, or curiosity.

### The Constraint Hierarchy

When diagnosing the #1 constraint, work through this hierarchy top to bottom. The first failing level is where you focus — don't optimize lower levels until you fix it:

1. **Can users complete the core flow?** (Technical: errors, timeouts, confusing UX, form abandonment)
2. **Do users understand what they got?** (Comprehension: is the output clear and interpretable?)
3. **Do users believe what they got?** (Trust: do they trust the methodology, data, or output?)
4. **Do users care about what they got?** (Relevance: did you solve the problem they actually have?)
5. **Do users want more?** (Engagement: does the output create demand for deeper interaction?)
6. **Do users tell others?** (Advocacy: is the experience remarkable enough to share?)

### Feature Prioritization

For each candidate feature, score on two axes:

**Signal value** (will this help us learn faster?):
- Does it test a hypothesis about what users want?
- Will the behavior change be measurable with current instrumentation?
- Does it generate data even if the feature fails?

**User value** (will this remove the #1 constraint?):
- Does it directly address the constraint identified above?
- How many users does it affect? (% of sessions hitting this constraint)
- How severe is the constraint? (abandonment vs mild friction)

**The best feature scores high on both.** A feature that removes the constraint but generates no signal is a guess in the dark. A feature that generates signal but doesn't address the constraint is research, not product work.

### Fix Type Hierarchy

Before building a new feature, ask: could a simpler fix work?

1. **Copy change** — Can different words fix this? (button text, error message, onboarding copy)
2. **Prompt change** — If your product uses an LLM, can a system prompt change fix this? This is often the highest-leverage fix.
3. **UX change** — Can reordering, removing, or simplifying steps fix this?
4. **Feature change** — Only build new functionality after exhausting 1-3.

### Anti-Patterns

- **Shipping without a success metric** — If you can't state "after this ships, I expect X to change by Y," you don't understand the problem well enough.
- **Optimizing what works instead of fixing what's broken** — Polishing the result page when most users abandon before getting a result.
- **Building for power users before fixing the core flow** — Advanced features when basic flow has low completion rate.
- **Treating all feedback equally** — A user who completed 10 sessions and gives feedback is 10× more valuable than a one-session bouncer.
- **Shipping features nobody asked for** — If no user behavior or question points to this need, you're guessing without a signal.
- **Falling in love with features instead of customers** — If a new feature doesn't improve your numbers, revert. The numbers are a scalable way to understand if you're meeting user needs. Fall in love with customers, not features.
- **Growth before engagement** — Spending on acquisition before the users you have can't live without you. Fix engagement first.

### Iteration Cadence

Bias toward speed. Daily iterations when possible, weekly minimum. Try things that take a day to code first, then a week, then a month. Put changes in — if they improve numbers, keep them. If they hurt, revert quickly.

At times it makes sense to suspend weekly iterations and make a wholesale change that takes a month or more. If the new numbers are worse, revert back. The most common mistake: founders make wholesale changes near the point of finding the recipe, set themselves way back, and don't revert quickly enough.

Focus A/B tests as much on removing features as adding them. Removing features that distract from the core experience can have a bigger effect than adding new ones.

## Data Access Patterns

See [reference/query-patterns.md](reference/query-patterns.md) for universal query patterns adaptable to any tech stack.

## Integration with Winning Metrics

The PMF coach operates at WM0-WM1 on the Winning Metrics framework (see the winning-metrics skill). PMF iteration is how you pass WM0 and WM1. Once PMF is found, the winning-metrics playbooks for WM2-WM4 take over for retention and scaling.
