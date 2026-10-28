# DualBench100 — Accounting AI Benchmark (source notes)

> Source: DualEntry Labs benchmark writeup + founder posts (Santiago Nestares, Benedict Dohmen).
> Retrieved 2026-10-28. Used as the factual spine of the LinkedIn series `ai-accounting-series`.
> **Conflict of interest to keep in mind:** DualEntry sells AI-native accounting ERP, so this benchmark also functions as a sales argument for its own category. Every number below is a vendor-run result.

## Structure

- 101 synthetic accounting tasks, built on a test company — **not live customer data**.
- Difficulty mix: 37 easy, 36 medium, 28 hard.
- Category spread is uneven — no single model is best at everything:
  - AR: 41.7% to 91.7% across models
  - Bank reconciliation: Kimi K3.1 Pro 100%
  - Month-end close: Kimi K3 91.7%
- Categories covered: transaction classification, journal entries, financial reporting, bank reconciliation, AP, AR, month-end close, accounting knowledge.
- Grading is deterministic against fixed reference answers — **no AI scoring** (avoids favouring one model family).
- All models ran on the same books, the same instructions, the same accounting tools.

## Scoring

- Each model ran **three times** per task.
- **Accuracy** = correct at least 2 of 3 runs.
- **Consistency** = correct in all 3 runs.
- Also reported: cost per task, output tokens, duration.

## Results

| Model | Accuracy | Notes |
|---|---|---|
| Gemini 4 Argon | 92/101 = 91.1% | Best. Consistency 86.1% (87/101 all three runs). Never trained for accounting. |
| GLM-5.3 Flash | 89/101 = 88.1% | Open model, ~$0.006/task |
| Most expensive model | — | ~$1.18/task |
| Claude Opus 5.5 | 82.2% | |
| GPT-6 Astra | 81.2% | |

- 22 models tested. Cost spread across the leaderboard: **~$0.006 to ~$1.18 per task (~200x)**.
- Gap between accuracy and consistency on the winner: 92 right at least twice, only 87 right all three times. **~5 tasks the model was right twice and wrong once — and from the output alone you cannot tell which run you got.**

## Quotes

- **Santiago Nestares (co-founder & CEO):** "finance doesn't run on drafts, it runs on validated records."
- **Benedict Dohmen (co-founder):** "on accounting work that trade is mostly gone, what is left is consistency."
- **Official framing:** "AI Still Fails a Third of Real Accounting Tasks" (across the model set, not the best model).
- Dohmen's argument: for open models, the accuracy / cost / control trade-off no longer holds.

## The number the series leads with, and how to use it honestly

91.1% is **101 discrete task answers**, not the correctness rate of a whole close workflow. A close is hundreds of decisions in sequence. At ~91% per question, the chance that every question across a 200-question close is right is on the order of **one in a hundred million**. Consistency (86.1%) is the more audit-relevant number, because a signing decision is "right every time", not "right usually".

## Inference vs. official statement (keep these separate)

- **Official:** the test's purpose, the scoring rules, that benchmark pass does not guarantee complete financial validity, that the portfolio does not cover every company, industry or accounting policy.
- **Inference (mine, 2026-10-28):** the benchmark conclusion is also being turned into a sales argument — even at 91% the model fails about a third of the tasks, and consistency is not enough, so system-level controls, validation and audit trail are needed. That supports DualEntry's ERP value and creates an "AI-native ERP" category, with a free leaderboard as PR and SEO.
- **Inference:** specialised LAM (e.g. Campfire's claimed 95%+) is a vendor claim on its own tasks and was never benchmarked here, so it cannot be compared to 91.1%. General models have already matched or beaten the specialised claim on standard accounting tasks. The defensible moat is not model accuracy — it is company-specific chart of accounts, policy, historical judgement, data context, rules, audit trail, migration cost and auditor familiarity.

## Series usage

- Part 1 — the 92/101 and 87/101 numbers, the one-in-a-hundred-million arithmetic, the founder quotes.
- Part 2 — why the benchmark itself runs every model three times, and why you should do the same on your own data.
- Parts 3–5 — company-specific rules, judgement boundaries, audit trail.
