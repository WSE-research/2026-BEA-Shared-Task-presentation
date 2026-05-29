# Speaker script — BEA 2026 pre-recording (≤ 10 min)

Same text as the in-deck speaker notes (press **S** in the browser for the speaker view). Timings are targets;
total ≈ 9:00, leaving buffer under the 10-minute Underline cap. Read at a calm pace; the deck is a backup/supplement
to the live Poster #147, not a full conference talk.

| # | Slide | Target | Cumulative |
|---|-------|-------:|-----------:|
| 1 | Title | 0:45 | 0:45 |
| 2 | The task | 1:10 | 1:55 |
| 3 | Why it's hard | 1:00 | 2:55 |
| 4 | Multi-strategy pipeline | 1:10 | 4:05 |
| 5 | Results | 1:00 | 5:05 |
| 6 | Prompting: commercial vs OSS | 1:05 | 6:10 |
| 7 | Fine-tuning closes the gap | 1:05 | 7:15 |
| 8 | Lessons learned | 0:55 | 8:10 |
| 9 | Conclusion & future work | 0:50 | 9:00 |

---

## 1 · Title (0:45)
Hi, I'm Jonas Gwozdz from WSE Research at HTWK Leipzig. This is joint work with Andreas Both. I'll walk you through
our submission to BEA 2026 Shared Task 2 — rubric-based short answer scoring for German. In short: we built a
multi-strategy system combining prompting, fine-tuning, and aggregation, and it placed second on three of the four
official tracks. Let me show you how it works and what we learned.

## 2 · The task (1:10)
The task is automated short-answer grading in German, with a twist: each item comes with a textual rubric that
defines what counts as correct. We predict one of three labels — Correct, Partially correct, Incorrect — and we're
scored with quadratic weighted kappa, which rewards getting close on ordinal labels. There are four tracks along two
axes: three-way vs. two-way scoring, and seen vs. unseen questions. The unseen-question tracks give you 39 brand-new
questions with new rubrics, so the system must generalize from understanding rubrics, not from memorizing questions.
That's the hard part.

## 3 · Why it's hard (1:00)
Four things. First, the rubric carries the meaning — almost a quarter of the questions are so generic that without
the rubric you can't grade them. Second, generalization: the unseen-question tracks force you to apply rubrics the
model never trained on. Third, "partially correct" is genuinely fuzzy, and models tend to be too lenient. Fourth,
answer length correlates with correctness — a trap, since German STEM answers can be short and still correct.

## 4 · Multi-strategy pipeline (1:10)
Our system has three blocks. One — prompting: condition on the rubric, add a few carefully chosen examples (TF-IDF
similarity plus deliberate boundary cases), adapt the count to question difficulty. Two — fine-tuning: LoRA adapters
on the Qwen family, scaled from 7 to 72 billion parameters. Three — aggregation: a QWK-weighted vote. The key insight:
we don't ship one system. For seen questions an ensemble of comparable models wins; for unseen questions a single
large fine-tuned model generalizes better — so we choose the strategy per track.

## 5 · Results (1:00)
The official results: second on three of four tracks, third on the hardest, track 4. The winner across the board was
IWM-DKM, the Meurers lab in Tübingen — an established German ASAG group. Notice the last column: we trail the top
system by between six and seventeen thousandths of a QWK point. A very tight field of nine teams — and the gap was
largest exactly where generalization matters most, the unseen-question two-way track.

## 6 · Prompting: commercial vs. open-source (1:05)
On prompting, the biggest lever by far is few-shot example selection — rubric-only to smart example selection buys
about six QWK points. One subtlety: prompts and models are tightly coupled. Our German prompt works for Gemini and
Qwen3.5, but an XML/English prompt that helps Claude and GPT actually hurts Gemini. The best single commercial API
model was Gemini 3 Flash at 0.748 — and cheap, about two hundredths of a cent per answer. But open source closes
the gap.

## 7 · Fine-tuning closes the gap (1:05)
We LoRA-tuned the Qwen family and evaluated out-of-sample — the honest estimate. Two open-source models, 14B and 32B,
beat the commercial Gemini baseline. Model generation matters more than size — Qwen3.5 at 9B edges Qwen2.5 at 14B.
Scaling saturates: 72B matches 32B for this data size. One practical note: the fine-tuned models are over 99%
confident, so confidence-based re-ranking gave us nothing. The headline: you don't need a proprietary model for
competitive German ASAG.

## 8 · Lessons learned (0:55)
Four methodological takeaways. One: which examples you show matters more than clever wording — and forcing
step-by-step reasoning hurt us by over-predicting "partially correct". Two: ensembles only help with comparable
members; one weak model poisons the vote. Three: scaling saturated around 32 billion parameters. Four — a
measurement lesson — evaluate out-of-sample: training on all data and scoring the trial set gave about 0.85, but
that's memorization; the honest out-of-sample number was about 0.77, much closer to real test performance. Trust
the unbiased estimate.

## 9 · Conclusion & future work (0:50)
To wrap up: competitive, open-source, rubric-based grading for German is feasible — within two hundredths of a QWK
point of the best system on three tracks, with fine-tuned Qwen models that beat a commercial baseline out-of-sample.
The frontier is generalization to unseen questions — track 4 at 0.53 is where the headroom is. Next: rubric
decomposition, better handling of the partially-correct boundary, and we're planning BEA 2027, this time with
students. The code is open. Thank you — please come by Poster #147.
