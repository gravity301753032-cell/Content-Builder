# Session Context — AI × Accounting LinkedIn Series

> Recorded 2026-10-28 (HKT) so a future session can resume without re-deriving the thinking.
> Author: Hermes. Subject: Eric Wong.

---

## 1. Why this file exists

Eric's instruction, verbatim: "同時你要先記住今天我們討論了什麼 我跟你的溝通是什麼 為什麼我要做這些東西發GitHub 因為我們這個sessions明天你就可能會忘記了 我想後面再follow up這個事情"

The series is the *output*. The reasoning behind it is the thing that was actually at risk of being lost. Both are now on disk. **When resuming, read this file first, then the part drafts.**

---

## 2. What this series is for

**Audience:** CEOs and CFOs in Hong Kong and APAC. Secondary: HKICPA members, Big4 partners, F500 APAC finance directors.

**Business goal:** build Eric's personal brand as the person who tells finance leaders what AI does to accounting, before the vendor does — and what they should do about it. Not a product pitch. NiteCrew is explicitly *not* the frame here (Eric corrected this hard: "NiteCrew根本是跟accounting完全沒有關係的東西").

**Editorial goal:** one idea per post, short enough that a CEO finishes it. Eric's original complaint: "你寫2000字的東西呢 人家是很累的" — hence the split into Part 1–5, each carrying exactly one concept.

**Voice requirement:** strong, not redundant, not self-deprecating. Zero emoji, zero check marks, no decorative symbols. Reads like a person talking, not a machine. Eric rejected the first machine-sounding draft explicitly.

---

## 3. The source material

**DualBench100** — an accounting AI benchmark run by DualEntry Labs, an AI-native accounting ERP company. Founders: Santiago Nestares (CEO) and Benedict Dohmen.

Facts used in the series, all verified against the DualEntry benchmark writeup:
- 22 models tested, 101 synthetic accounting tasks built on a test company (not live customer data).
- Best: Gemini 4 Argon — 92 of 101 correct (91.1%). Never trained for accounting.
- Open model GLM-5.3 Flash — 89 correct (88.1%) at ~$0.006/task, vs ~$1.18/task for the most expensive. ~200x spread.
- Consistency: every question run three times. 92 right at least twice; only 87 right all three times (86.1%). On ~5 tasks the model was right twice and wrong once, and from the output alone you cannot tell which run you got.
- Each task has exactly one right answer; grading is deterministic, not AI-scored. All models got the same books, the same instructions, the same tools.
- Difficulty mix: 37 easy, 36 medium, 28 hard. Category spread is uneven (AR 41.7%–91.7%; Kimi K3.1 Pro 100% on bank reconciliation; Kimi K3 91.7% on month-end close). No single model is best at everything.
- **Conflict of interest to state when relevant:** DualEntry sells AI-native ERP, so the benchmark doubles as a sales argument.

The two founder quotes used in Part 1:
- Nestares: "finance doesn't run on drafts, it runs on validated records."
- Dohmen: "on accounting work that trade is mostly gone, what is left is consistency."

---

## 4. The series spine

The order is dependency-driven, not arbitrary. Each post assumes the previous one.

| Part | Working title | Dies | Rises | Reader's action | Load-bearing line |
|------|----------------|------|-------|-----------------|-------------------|
| 1 | What this means for your finance team | knowing the rules | writing the rules down | translate what your team reads into something a machine executes and an auditor re-performs | "The gap closes when your accounting is written down, not when the next model ships." |
| 2 | How you make it consistent | hoping the model is right | narrowing the question, coding the checkable parts, giving precedent, testing yourself | run the same judgement three times on your own data | "A vendor leaderboard is a marketing asset." |
| 3 | The precedent you are about to automate may be wrong | assuming history is truth | auditing your own history before it becomes the standard | reconcile policy against the last 100 entries | "You are about to scale your mistakes." |
| 4 | Where the model stops and a person starts | junior handles exceptions | boundary + escalation | write the escalation condition for each decision | "The machine must know when to hand it back." |
| 5 | Who signs when the model drafts | accountant as operator | accountant as author of the control | an audit trail a reviewer can re-perform | "The signature becomes the scarce asset." |

**Why Part 3 sits after Part 2:** Part 2 tells the reader to feed precedent to the model. Part 3 immediately asks whether that precedent is even right. The tension is the point — a reader who does Part 2 without Part 3 will automate their own errors at scale. This sequence was Eric's own structure, not an assistant invention.

---

## 5. Eric's original ideas, and what was changed (and why)

Eric's framework is his own. These are the five ideas he brought, plus the three corrections he accepted after challenge.

### Idea 1 — "The profession needs to understand how LLMs work and translate accounting policy into machine-readable rules"
**Verdict: direction right, framing changed.**
- *Changed to:* the capability is **specification, not AI expertise**. "Understand LLM principles" reads to a CFO as "become an engineer," and they disengage. "Machine-readable" also over-promises: the real test is **unambiguous and testable** — a sentence a human reviewer can re-perform, and which therefore does not need to be code.
- *Sharpened to:* **AI does not create a new skill, it makes an old one scarce again — writing down what you actually do.** Most finance teams discover at that point their policy exists nowhere except in people's heads. This framing is stronger and less "please learn a new thing" than the original.

### Idea 2 — "LLM solved 91%; the rest is company-specific rules"
**Verdict: half right; needs a stated limit.**
- Part of the residual gap is not company-specific rules at all. With 37 easy / 36 medium / 28 hard, some of it is genuine ambiguity — two good accountants can disagree on a modified contract. No rule closes that, and it is permanent human work.
- *Added to Part 1:* "Some of that gap no rule will ever close, because it is not ignorance, it is judgement." This also makes the claim survivable: an accountant reader who pushes back on "rules solve it" gets a straight answer, and the professional case gets stronger, not weaker.

### Idea 3 — "LLM + local RAG, and as training cost falls every company will train its own model"
**Verdict: direction right; the inference was too fast.**
- The 2026 enterprise sequence is prompt → RAG → fine-tune → distill. The order cannot be reversed. A LoRA fine-tune of a 13B model on 50K examples is roughly $400–1,200 per run, but building a clean 50K-example set is a multi-month effort costing roughly $40K–150K in labour. The bottleneck moves to data preparation — and data preparation is accounting work.
- **Fine-tuning is for form, not facts.** An accounting policy changes (IAS 8 amendments, business change), so policy belongs in retrieval, permanently, not baked into weights.
- *Safe formulation used in Part 1:* "a general model with your own data attached, and as the cost of running a model on your own data falls, more of it moves in-house."

### Idea 4 — the metaphor: "LLM is a bare shell, every company has to do the fit-out"
**Verdict: keep it, change what is being decorated.**
- The flaw in the shell version is that it makes the LLM look empty, and it is not empty — 92 of 101. The right reading: the shell is generic and identical for every tenant; what each company does is decide its own layout, fittings and rules.
- *Correction:* decorate **the rules**, not the space. A well-built, off-the-shelf unit that is identical for every tenant, and the fit-out is your policy.
- *English register:* the metaphor actually used in Part 1 is **"the best accountant in the world who has never worked in your industry."** It is the only candidate that explains *why* a 92/101 model still fails, and it makes the professional action (onboard it properly) the obvious next step. The shell metaphor is retained for the Chinese-language version.

### Idea 5 — "Before you feed historical entries to the LLM, check they actually match your accounting policy — otherwise you scale your past mistakes"
**Verdict: the strongest idea in the series, and it is Eric's original. Not changed, only widened.**
Three layers:
1. *Why* history and policy diverge: old policy later changed / genuine error / a deliberate case-by-case exception (audit adjustment, one-off treatment). The third is the dangerous one, because it looks like a mistake and it was right.
2. *Why RAG cannot save you:* retrieval is faithful, so a wrong precedent is handed back with the same confidence every time, and now it looks like policy because the policy says so.
3. *The sharpest layer:* skip the check and you are not automating your judgement, you are automating your past — mistakes included, at volume — and every future user of your system inherits it. You are not only hurting yourself; you are hurting your clients and your auditor.
- *New addition in Part 3:* the RAG caveat (layer 2) was not in Eric's original framing and is worth making explicit to any technical reader.

### The closing line
Eric asked for: "以後AI的發展一定會更加好."
Used as the *easy* half of a two-part close, then the hard half lands: **AI will keep getting better — cheaper, faster, more accurate — and that is the easy part. The gap between a general model and your business closes when your accounting is written down, not when the next model ships.**

---

## 6. The communication protocol for this series

Recorded because Eric corrected it repeatedly in one session:

- **No check marks, no emoji, no decorative symbols.** Eric's words: "你發給我的所有東西 不要加個tick 很難看整個article."
- **Plain declarative opening.** No "In today's rapidly evolving landscape…" No throat-clearing.
- **Short sentences, one idea per sentence.** Average 10–15 words. Nothing over ~30 words except the deliberate "best accountant in the world" line.
- **Second person, addressed to the reader's actual job.** "Your finance team", "your close", "your books."
- **End every post with a question the reader can answer from their own experience.** This is the engagement mechanic.
- **Hashtags:** exactly 6 — `#Accounting #AI #CPA #CFO #AIinFinance #FutureOfWork`
- **Length:** target ~1,000–1,800 chars, ceiling 2,400. Part 1 is the longest at 2,686 because it carries the whole setup; Parts 2–5 are 1,367–2,027.
- **No jargon without unpacking.** Eric's worry: "有時候我不知道我是不是寫的太多jargon 然後他們會聽不懂." Every term (accrual basis, capitalisation threshold, consistency) is either explained inline or replaced with a concrete scenario.
- **Do not front-run a later post.** If an idea belongs to Part 3, Part 1 ends with the hook that makes Part 3 necessary, not with Part 3's answer. Part 2 ends with "One warning before you feed it your history" and stops there.

---

## 7. Open questions for the next session

1. **Part 1 is longer than Eric's typical post.** He has not yet seen v6 (2,686 chars) after the three corrections. His real published posts run ~1,000–1,800 chars. Decide: trim Part 1 by cutting the benchmark detail, or accept it as the series opener.
2. **The 毛坯房 / new-hire metaphor choice** was made by the assistant, not by Eric. Eric has not explicitly endorsed "the best accountant in the world who has never worked in your industry." He only said the shell metaphor was his. Confirm before publishing.
3. **Publication order.** The series is designed to be read in order (Part 2 sets up Part 3). But Part 3 is the sharpest and most original — there is a case for publishing it first as a standalone hook, then sequencing. Undecided.
4. **Hashtags are identical across all five parts.** Fine for a series, but each post may need a distinct angle for reach. Undecided.
5. **Chinese-language versions.** The shell metaphor and some of the strongest lines land better in Cantonese. The `personal-content-creation` skill records a source-first book pipeline; this series breaks that model (source = a benchmark, not a book) and the Content-Builder README may need a new root for it.
6. **No post has been published.** `LinkedIn/README.md` still says "Published on LinkedIn: 0" across the whole account. Personal-brand momentum depends on actually shipping these, not on having five drafts.
7. **Part 5's claim that junior work is disappearing** is asserted from the benchmark, not sourced. If Eric wants to publish it, it needs a citation for the CPA-retirement / junior-work claim, or it should be framed as an inference.

---

## 8. Where everything lives

- **Local wiki (SSOT):** `/root/wiki/content/ai-accounting-series/` — part1–part5 drafts + this file. Tracked in `/root/wiki/content/00-content-tracker.md`.
- **GitHub `gravity301753032-cell/Content-Builder` (public):** `LinkedIn/ai-accounting-series/` — the five drafts plus this context file. Plus `research/dualbench100-accounting-benchmark.md` — the source notes for the benchmark facts.
- **GitHub `gravity301753032-cell/second-brain` (private):** the wiki mirror.
- **Hindsight (cross-session recall):** the evaluation of Eric's five ideas and the three accepted corrections, stored 2026-10-28.
- **Skill:** `personal-content-creation` → `references/linkedin-strong-voice-architecture.md` — holds the metaphor analysis, the three accepted corrections, and the series spine so a future session does not re-derive them.
