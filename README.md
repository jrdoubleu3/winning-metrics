# Winning Metrics

Two Claude Code skills for 0→1 founders finding product/market/channel fit.

Based on Tim Connors's Winning Metrics framework (PivotNorth Capital) and his Founding playbook.

## Skills

### winning-metrics

Assesses where your startup sits on the WM0→WM4 progression and gives a specific playbook for what to do next at each level. Covers NPS, retention asymptotes, CAC Doubling Time (CACD), viral loop design, and scaling milestones. The core rule: don't spend on growth before love is proven.

### pmf-coach

Reads your user logs and proposes the next most valuable thing to ship. Treats PMF as a search problem — each ship is a guess, user behavior is the signal. Includes a constraint hierarchy, signal taxonomy, and example database queries you can adapt to your own stack.

## Install

```bash
git clone https://github.com/jrdoubleu3/winning-metrics.git /tmp/wm-install && cp -r /tmp/wm-install/winning-metrics ~/.claude/skills/winning-metrics && cp -r /tmp/wm-install/pmf-coach ~/.claude/skills/pmf-coach && rm -rf /tmp/wm-install
```

## Quick Start

**Winning Metrics assessment:**

```
Read ~/.claude/skills/winning-metrics/SKILL.md and the reference files. Assess where my startup sits on WM0-WM4. Ask me for the data you need at each level.
```

**PMF review session:**

```
Read ~/.claude/skills/pmf-coach/SKILL.md and the reference files. Connect to my database and run a PMF review on the last 7 days of user data.
```

## Contributing

Open an issue or PR. If you're a founder using these skills, share what worked and what's missing — this is designed to be extended.

## License

MIT
