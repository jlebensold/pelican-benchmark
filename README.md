# pelican-benchmark

> Eighteen trajectories of a pelican-on-bicycle SVG. Inspired by Simon Willison's [pelican-riding-a-bicycle](https://simonwillison.net/tags/pelican-riding-a-bicycle/) benchmark, run as agentic workflows on [Jetty](https://jetty.io).

Live at **[pelicans.jetty.bot](https://pelicans.jetty.bot)**.

## What's here

Four self-contained HTML visualizations of the same benchmark, exploring two axes:

- **Iterating the runbook** (v1 → v11, same agent + model) — what happens when you edit the prompt
- **Iterating the agent/model** (one runbook, seven combinations) — what happens when you swap the model

| Page | What it shows |
|------|---------------|
| [`/climb`](https://pelicans.jetty.bot/climb) | Self-score over time, per-axis bars, full timeline of every iteration |
| [`/filmstrip`](https://pelicans.jetty.bot/filmstrip) | Focal viewer + thumbnail strip — click any frame to see the SVG, ask, and diff |
| [`/head-to-head`](https://pelicans.jetty.bot/head-to-head) | Speed × score scatter + side-by-side outputs across seven agents |
| [`/runbooks`](https://pelicans.jetty.bot/runbooks) | Diff any two runbook versions side-by-side or unified |

## The task

Generate a pure-XML SVG of a pelican riding a bicycle. No `<image>` tags. Under 50 KB. Both subjects must be unmistakable and the pelican must be visibly **interacting** with the bicycle.

## The rubric

Four axes, 0–10 each: **Pelican** · **Bicycle** · **Composition** · **Polish**. Each trajectory runs three self-critique rounds and reports the best round's score.

## Key findings

1. **Iterating the runbook is worth ~6 points.** v1 (31/40) → v5 (37/40 PEAK) over four targeted runbook edits. Embedding a baseline SVG into the runbook is the single highest-leverage change (+5 points in one revision).
2. **Iterating the model is worth ~5 points.** Hermes on the same v1 runbook climbs from 34/40 (Sonnet) to 39/40 (Flash). Model choice matters as much as prompt engineering.
3. **Self-scoring isn't cross-comparable.** Flash hands out 10/10s freely; Sonnet caps near 37/40 even on great work. A real leaderboard needs an external vision judge.

## Stack

- Static HTML — every page is self-contained (SVGs and Pelly logo base64-inlined)
- Chart.js for the climb/scatter charts
- jsdiff for the runbook diff page
- PostHog for analytics
- Deployed on Vercel; DNS via the `jetty.bot` zone

## Local preview

```bash
# any static server works
python3 -m http.server 8000
# then open http://localhost:8000
```

## License

The visualizations are MIT. The pelican mascot ("Pelly") belongs to Jetty.
