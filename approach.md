# Approach: Autoresearch for Business Optimization

## What This Project Is

We are building an **autonomous business experimentation system** inspired by Karpathy's [autoresearch](https://github.com/karpathy/autoresearch). We don't use any of his code — no ML training, no GPUs, no `train.py` or `prepare.py`. We borrowed the **concept** and are building everything from scratch for our own use cases.

## Relationship to Karpathy's Repo

We forked the original repo as a starting point, but in practice:

- **What we took:** The idea of an autonomous loop (try → measure → keep/discard → repeat), the `program.md` agent instruction format, and the `results.tsv` logging convention.
- **What we don't use:** All of the Python code (`train.py`, `prepare.py`), the ML training pipeline, the NVIDIA GPU requirement. None of it is relevant to us.
- **Going forward:** All code we write is new, built specifically for our business use cases. The fork serves as a reference, not a foundation.

## The Core Pattern

An AI agent runs an autonomous loop:

1. **Create a variation** — the agent changes a variable (e.g., email copy, ad text, pricing)
2. **Run the experiment** — execute via platform API (send emails, launch ads, etc.)
3. **Wait for results** — allow time for data to come in (replies, clicks, conversions)
4. **Measure the outcome** — pull metrics from the platform's API
5. **Keep or discard** — if the metric improved, keep. If not, revert to previous best.
6. **Log and repeat** — record results, generate the next variation, loop forever.

## How It Runs

- **Development and testing** — locally on MacBook (no GPU needed, ever)
- **Production execution** — GitHub Actions on a schedule (e.g., hourly)
- **Results tracking** — `results.tsv` style logging with keep/discard decisions
- **No human intervention required** — the agent runs autonomously until manually stopped

## What Each Use Case Needs

For each use case we build, we need three things:

| Component | What it is | Example |
|-----------|-----------|---------|
| **A clear metric** | The number we're optimizing | Reply rate, CTR, conversion rate |
| **A variable to change** | What the agent modifies between experiments | Email copy, ad headline, pricing |
| **An API integration** | How we run experiments and read results | Instantly API, Meta Ads API, etc. |

## Inspiration

This approach was inspired by [Nick Saraev's example](nick_saraev_example.md) of applying autoresearch to cold email optimization. We generalize this to any business process with a measurable metric.

## Use Cases

> To be defined. Each use case will get its own section here with:
> - The metric to optimize
> - The variable being changed
> - The platform/API involved
> - The experiment cadence (how often the loop runs)
