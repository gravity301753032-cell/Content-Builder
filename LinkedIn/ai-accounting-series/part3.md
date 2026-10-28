# Eric Wong — LinkedIn Series: AI × Accounting (Part 3 of 5)

**Working title:** Part 3 — The precedent you are about to automate may be wrong

**Status:** Draft for Eric's review (pushed to GitHub 2026-10-28 for later review)
**Length:** 1778 chars / 321 words

---

Part 3 of 5: The precedent you are about to automate may be wrong.

Here is the obvious move. Give the system your accounting policy and your historical journal entries, so it learns the way your company actually works. It works. That is exactly why it is dangerous.

Retrieval is faithful. If a precedent in your history is wrong, the system will hand it back with the same confidence every time, and now it looks like policy, because the policy says so.

Three reasons your history and your policy disagree, and they need different answers.

The first is old policy. Your treatment changed two years ago and the old entries are still in the books. The second is a real error, someone booked it wrong and it was never corrected. The third is a deliberate exception, approved case by case, an audit adjustment or a one-off treatment. That third one is the dangerous one, because it looks like a mistake and it was right.

So audit the precedent before you automate it. Take your policy, take the last hundred entries of each type, and find the ones that do not match. For each one ask which of the three it is. A real error, correct it. An old policy, date it. A deliberate exception, write down the condition that makes it an exception, otherwise the model will treat it as a rule and apply it to every similar transaction from now on.

The point is not that your history is bad. The point is that your history is not the same thing as your rules, and only you can tell them apart. Which is the whole job.

If you skip this step, you are not automating your judgement. You are automating your past, mistakes included, and doing it at volume.

Which past decision of yours would you not want a system to copy without asking?

#Accounting #AI #CPA #CFO #AIinFinance #FutureOfWork
