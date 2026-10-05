# The Unofficial Guide

<!-- Duc Nguyen - Corpus: campus_life -->

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->

This guide searches 88 student posts in the campus_life corpus about courses, dining, housing, and campus rules. It retrieves relevant posts and uses them to answer questions with source filenames. When the closest post is beyond the 0.6 cutoff, it refuses the question before calling the model

## Chunking Strategy

**Chunk size:** One complete post per chunk (178–549 characters in this corpus)
**Overlap:** 0 characters

The 88 documents produced 88 chunks. In the five posts I inspected, the title and details formed readable, complete thoughts. Keeping each post together preserves that context; `chunker.py::split_documents` skips empty posts

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->


**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```

**Chunk 2** — source: `course_biol_160.txt#0` — produced by: `chunker.py::split_documents`

```
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```

**Chunk 3** — source: `course_hist_118_workload.txt#0` — produced by: `chunker.py::split_documents`

```
Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.
```

**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::split_documents`

```
Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.
```

**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::split_documents`

```
Innisfree Hall — what it's actually like

Transferred in last year, so take this with a grain of salt. Built 1991, renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between two rooms.

The good: the shared-bathroom-between-two-rooms arrangement is the best compromise on campus.

The bad: no air conditioning, which matters for the first three weeks of September.

Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building is L-shaped and the short wing is much quieter.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:** How long is the peak wait at Pellew Dining Hall?

**Answer:**

```
The peak wait time at Pellew Dining Hall is 12 to 18 minutes.

Source: `dining_pellew_dining_hall.txt` (and also mentioned in `dining_pellew_dining_hall_followup.txt`).
```

**My relevance cutoff:** 0.6. Covered questions had best distances from 0.1782 to 0.3855; uncovered questions ranged from 0.8246 to 0.9340. The cutoff falls in the gap between those groups. The Mongolia question was refused without a model call

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---:|
| Course drop W | Yes | 0.3145 |
| BIOL 160 curve | Yes | 0.3083 |
| HIST 118 reading | Yes | 0.3164 |
| Pellew peak wait | Yes | 0.1782 |
| Innisfree air conditioning | Yes | 0.3855 |
| Capital of Mongolia | No | 0.8246 |
| Diesel oil change | No | 0.9340 |
| 1994 World Cup | No | 0.8859 |
| Ibuprofen dosage | No | 0.8442 |
| Rust for loop | No | 0.8960 |

## How I Used AI 

1. Used Chatgpt to troubleshoot a Windows installation error. Its first suggestion, Python 3.12, also failed. We checked the package files, switched to Python 3.11, and I confirmed the fix when `test.py` passed all 10 checks.

2. Used Chatgpt to draft questions and sharpen two criteria using five chunks I printed from `campus_life`. I entered the questions and cleaned up `criteria.md`. The chunks support the facts in the questions; I still need to test the generated answers.

3. Chatgpt suggested keeping each short post as one chunk. I updated split_documents, corrected its old description, and verified that reindexing produced 88 chunks. I compared five covered and five unrelated questions and kept the 0.6 cutoff because it falls between their distance ranges.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

## How I Used AI in Unit 2
Used Chatgpt to help interpret the run logs and draft the tables and explanations below. It pointed out that the Innisfree answer was factually correct but failed my exact-phrase criterion. I then compared the draft with the saved output before adding it to this README

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Five sample chunks have complete sentences and intact endings | 5/5 |5/5 | 5/5| 5/5| MET |
| 5. Answers contain their expects phrase | 4/5| 4/5| 4/5| 4/5 | MET |

- Criterion 1: the five answer-bearing sample chunks appear among the retrieved sources for their questions in every run.
- Criterion 2: all 15 generated answers name at least one source filename.
- Criterion 3: the gate refused all five unrelated questions; the deterministic result applies to all three columns.
- Criterion 4: all five sampled chunks have complete sentences and intact endings; this check is deterministic.
- Criterion 5: four answers per run contain their expected phrase. Innisfree says “does not have air conditioning,” which fails the literal “no air conditioning” check.

### Baseline evidence

Evaluation report: `results/run_2026-10-05_0104_before.md`.
Sample chunks: `results/chunks_before.txt`.

**Generated answer — Innisfree question, run 1**

Produced by `generate.py::answer_from_chunks`, recorded by `run_eval.py::main`.

Question: Does Innisfree Hall have air conditioning?

```text
No, Innisfree Hall does not have air conditioning, which matters for the first three weeks of September.

Source: housing_innisfree_hall.txt
```

This answer names a source and conveys the correct fact, but does not contain the exact expected phrase `no air conditioning`. The same wording mismatch occurred in all three runs.

**Sample chunk — criterion 4**

Source: `course_biol_160.txt#0`.
Produced by `chunker.py::split_documents`.

```text
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```

This chunk contains complete sentences and ends with a complete sentence. I checked all five chunks in `results/chunks_before.txt`.

**Out-of-scope gate results — criterion 3**

Produced by `run_eval.py::check_out_of_scope`.

```text
Out-of-scope questions (the gate should refuse these):
  refused  (best distance 0.825)  What is the capital of Mongolia?
  refused  (best distance 0.934)  How do I change the oil in a diesel engine?
  refused  (best distance 0.886)  Who won the 1994 World Cup?
  refused  (best distance 0.844)  What is the recommended dosage of ibuprofen for a headache?
  refused  (best distance 0.896)  How do I write a for loop in Rust?
  -> gate refused 5 of 5
```

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunks contain the answer | MET | Each question retrieved a source whose displayed chunk contains the answer, giving 5/5 in each run against the 4/5 target. |
| 2 | Every answer names a source | MET | All five answers in each of the three runs name at least one source filename. |
| 3 | Gate stops out-of-corpus questions | MET | The gate refused 5/5 unrelated questions, exceeding the 4/5 target. This deterministic measurement is repeated across the three columns. |
| 4 | Sample chunks contain complete sentences and intact endings | MET | All five displayed chunks contain at least one complete sentence and have no sentence cut off at the end. This deterministic inspection is repeated across the three columns. |
| 5 | Answers contain their expected phrase | MET | Four of five answers contain their expected phrase in every run, meeting the 4/5 target. The Innisfree answer fails the literal phrase check in all three runs. |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

All five criteria met their targets in the baseline test.

One result stood out: the Innisfree answer failed the exact-phrase check in all three runs. The source says “no air conditioning,” while the answer says “does not have air conditioning.” Both express the same fact, so this is a limitation of my phrase check rather than a factual error.

Criterion 5 still passed because its 4/5 target allows one question to fail. My five questions also ask for straightforward facts from short posts, so these results do not show how well the system handles harder questions.

In a future test, I would tighten criterion 5 to require correct facts for all five questions in every run, with a checklist that accepts equivalent wording. For this evaluation, I am keeping the original criterion and target unchanged.

## The Improvement

**What I changed:** Reduce `TOP_K` from 5 to 3 in `config.py`.

**Why I picked it:** The baseline retrieved some posts about other courses for the BIOL 160 question. I want to test whether using fewer chunks reduces unnecessary context while preserving the answers. All baseline criteria passed, so this is an efficiency experiment rather than a fix for an incorrect answer

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

Evaluation report: `results/run_2026-10-05_0128_after.md`.

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4/5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5/5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4/5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Five sample chunks have complete sentences and intact endings | 5/5 | 5/5 | 5/5 | 5/5 | MET |
| 5. Answers contain their expected phrase | 4/5 | 4/5 | 3/5 | 4/5 | MISSED |

All five answer-bearing sources remained in the retrieved results, and all 15 answers named a source. The gate refused all five unrelated questions. Gate results were measured once; chunk quality uses the unchanged baseline sample inspection. These deterministic checks are repeated across the three columns.

Criterion 5 missed its target in run 2. The course-drop answer used “after the second week” instead of “week two.” The Innisfree answers also failed the literal “no air conditioning” check in all three runs, although they conveyed the correct fact.

**Generated answer — course-drop question, run 2**

Produced by `generate.py::answer_from_chunks`, recorded by `run_eval.py::main` in `results/run_2026-10-05_0128_after.md`.

```text
**A course drop shows as a W on your transcript if it occurs after the second week (up through the end of week six).**

Source: admin_add_drop_deadline.txt
```

The answer conveys the correct timing but does not contain the expected phrase `week two`.

**Did it help?**

Reducing TOP_K from 5 to 3 lowered input tokens from 9,162 to 6,273, about 31.5%, across 15 model calls. The retrieved evidence still supported all five answers, and source citations and gate results met their targets. However, criterion 5 changed from 4/5 in every baseline run to 4/5, 3/5, and 4/5 afterward. The change reduced context usage, but did not improve the exact-phrase score. These runs do not establish whether the wording difference came from the smaller context or normal model variation.

## What's Still Broken

Criterion 5 missed its target in the second after run. The relevant facts were retrieved, but generation used equivalent wording that my literal phrase check rejected. This exposes a weakness in how I measured answer correctness. I kept the original criterion unchanged and stopped after this one measured change.

## What I'd Do Differently

Before a future evaluation, I would define a fact checklist that accepts equivalent wording and requires all five answers to be correct in every run. I would also include harder questions that require evidence from multiple posts. The current results only cover five straightforward factual questions.