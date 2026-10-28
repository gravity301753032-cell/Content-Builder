# Eric Wong — LinkedIn Series: AI × Accounting (Part 2 of 5)

**Working title:** Part 2 — How you make it consistent

**Status:** Draft for Eric's review (pushed to GitHub 2026-10-28 for later review)
**Length:** 1367 chars / 242 words

---

Part 2 of 5: How you make it consistent.

The people who built that benchmark did not trust a single run. Every model was run three times, and they report two numbers: got it right at least twice, and got it right every time. That second number is the one to build your life around.

Neither should you. Take one judgement your team makes every week, run it three times on your own data, and see what happens.

Four things move the number.

Narrow the question until it has one answer. Those 101 questions are narrow, one decision each. Your judgement calls are usually wider than you think. Split a question like "is this revenue" until each version can be answered yes or no.

Put the checkable parts in code, not in the model. Dates, arithmetic, account validity, tax rates are 100% checks and they are cheap. Let the model handle the fuzzy part and let code check the rest.

Give it precedent, not a policy document. The last fifty entries of that type and how you decided them. That is what removes the variance, because it removes the guessing.

Then measure it yourself. Your number on your books, on your data, is your baseline. A vendor leaderboard is a marketing asset.

One warning before you feed it your history.

Next in this series: whether the history you are about to hand over is actually right.

#Accounting #AI #CPA #CFO #AIinFinance #FutureOfWork
