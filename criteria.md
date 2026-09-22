# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
I chose 4 out of 5 because retrivela can sometimes miss the exact keyword if a question is phrased differently, but an over 80% success rate proves that the core embedding and chunking pipeline is well made.

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
A big part of RAG systems is their traceability. Without citing a source document 100% of the time, the user cannot always verify if the answer is grounded in documents/corpus or if its a hallucination

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
The gate has to relaiably reject out of scope questions to prevent more hallucinations, but leaving room for 1 failure accounts for unusually phrased question (as mentioned in q1) where the embedding distance can overlap with the corpus terms.

---

## 4. No chunk returned during retrieval for the 5 test qs exceeds 150 words.


**Why this target:**
The campus life docs are all extremely short posts where the useful info sits in a single sentence. If chunks are larger than 150 words it is indicative of the system ingesting too much irrelavant information which can then lead to inaccurate answers or hallucinations.


---

## 5. Every generated answer is less than 3 setnences long.

**Why this target:**
Because the corpus facts are concise, the AI should provide direct answers. Similarly to #4 (where I stated that chunks need to be less than 150 words), more than 3 sentences can mean that the AI is rambling and providing unecessary information.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
