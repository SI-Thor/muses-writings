# Decision-Model Usage Patterns: tells, not models

*2026-11-08 · Fleet synthesis doc, compiled from the day's batch deep-learns (sources cited per pattern). GRADE: Synthesis — per-pattern evidence grades inside, in the house scheme (A = paper + artefact, B = public runs, C = demos, D = marketing).*

**Premise (Casey's doctrine, stated 2026-11-08).** We do not need to download endless new decision models. The articles' value is the *use patterns* people have discovered — the modalities of how decision models earn their keep — and as long as the modality contract holds, our systems can adapt and learn those patterns without adopting every model mentioned. The provider interface is what makes this true: Jacquard never wired Jev in as Jev; it wired in a contract — a typed judgement over a stated situation, returned with probabilities, advisor readings only, never the gate. Models behind that interface are interchangeable witnesses. What compounds is the pattern library, not the model zoo.

Each pattern is filed in the triples shape: **Situation → Idiom → Evidence/Outcome → Modality requirement → Our status**, with its source doc on this shelf named. A pattern without a shelf source does not exist (see Maintenance).

---

## P1. State once, ask everything (state-once economics)

- **Situation:** One expensive input — an image, a world state, a long document — and many small judgements to make over it.
- **Idiom:** Present the input a single time ("state once"); pose every typed question (Choice / Yes-No / Score / Box / Track) against that one stating; the model returns a probability for every answer and never generates prose. Perception is paid once; judgement is nearly free per question.
- **Evidence/Outcome:** d3-ultra (vLLM Semantic Router, 26.09B, Apache-2.0): stating a photo costs 304 ms (1× AMD MI325X, BF16); 255 questions on the same input total 2.16 s — **≈7.3 ms marginal cost per additional question**. On the vendor's private SR-Text set it scores 87.2 against Jev 1.14's 73.1. The shape itself is corroborated as a category: Jev and Liquid's d1 line do the same thing. **Grade B−** — weights open and a free API exists, but every benchmark number is self-reported on the vendor's own private test sets.
- **Modality requirement:** The advisor accepts one stated input plus a batch of typed questions, and returns calibrated probabilities per answer. No text generation.
- **Our status:** **Adopted in architecture.** The governor and the JEV rack already run this shape (batch 2's summary: Liquid is productising "the exact 'state once, answer everything, with probabilities' pattern our governor and Jev rack already embody"). The ≈7.3 ms figure is filed as the marginal-cost expectation any seated provider is held to.
- **Source:** `batch-deep-learn-2-20261108.md` §2.

## P2. Frame / triage / reflexes

- **Situation:** A real-time loop (game play, live control) where decisions arrive several times a second, most are routine, a few need judgement, and the action space itself must stay trustworthy.
- **Idiom:** Three layers. A general LLM writes the harness — the *frame* — defining the macro-action space. The decision model *triages*: it picks among the framed macro-actions at speed. Generated *reflexes* handle what neither can reach in time. The decision model never redefines the action space. Compile the triage, never the verdicts.
- **Evidence/Outcome:** Aura Autopilot (Ramen, Apache-2.0, open source) ships this structure commercially: an engine plugin reads game state and injects real input events; the coding agent writes per-game harnesses; **Jev, via the TypeSafe SDK, decides roughly every 0.25 s during play**, choosing among framed macro-actions; reflexes are generated and stored as code. Runs found cheating are disqualified even when the goal was achieved — the verdict attaches to the path, not the outcome. **Grade B−** (whitepaper + repo; the press release's commercial claims are C+).
- **Modality requirement:** The advisor returns a choice among a caller-supplied enumerated action set, with probabilities, at ~4 Hz cadence.
- **Our status:** **Adopted in doctrine.** Jacquard's advisor placement is the same boundary in structure: nothing lets the decision model redefine the action space. Our league drivers mirror frame/triage/reflex with hand-built reflexes; the *generated* reflex layer is the unbuilt part (batch 1's shortlist carries a harness-authorship spike candidate).
- **Source:** `batch-deep-learn-20261108.md` §14.

## P3. Absence is a confidence, never a null — and hard-fail beats silent truncation

- **Situation:** A typed-answer surface where "not there" and "cannot say" must be distinguishable, and where inputs can exceed the model's context.
- **Idiom:** Two contract rules. (1) A localisation answer always returns exactly one box plus a confidence; **≈0 confidence means the target is absent** — absence is expressed as low confidence, never as a null or a missing value. (2) An over-length input **hard-fails** rather than silently truncating: fail loud, never degrade silently.
- **Evidence/Outcome:** d3-ultra's documented behaviour: a Box question always returns exactly one box plus a confidence; inputs over 131,072 tokens hard-fail. Batch 2's synthesis names both conventions as steals "independent of any model swap" for our own typed-answer surfaces. **Grade B−** (vendor-documented product behaviour; inspectable via the free API and open weights).
- **Modality requirement:** Every answer in the schema carries a confidence, including localisation answers; errors are loud, never silent degradations.
- **Our status:** **Candidate.** Named steal for our typed-answer surfaces regardless of which provider sits behind them; not yet written into interface policy.
- **Source:** `batch-deep-learn-2-20261108.md` §2 and shortlist.

## P4. Cadence classes — cheap typed judgements at control-loop rates, expensive reasoning rationed

- **Situation:** An embodied or live system that needs decisions at several hertz (navigation, action chunks) alongside rarer, harder judgements.
- **Idiom:** Seat a small on-device decision model for the high-cadence typed judgements; reserve large-model reasoning for the slow loop; price each class by latency and energy per call, and allocate cadence by role.
- **Evidence/Outcome:** Liquid's d1-2B navigation variant emits 5 tokens per decision (2 spatial/control + 3 RQ codes → a 10-waypoint path) and runs at **>2.5 Hz on a Jetson AGX Orin** under TensorRT FP16; its VLA variant produces 8-step action chunks in **<50 ms** on the same board. ZETIC's independent measurement table corroborates the economics on our exact boards: SmolVLA compiled is a 50 ms / 3.35 J policy call; a π0.5-class call at 132 ms / 11.31 J is a main-character cadence only. **Grade B** (vendor benchmarks on open weights; the ZETIC table is a single, methodologically open source).
- **Modality requirement:** An advisor small enough for on-device TensorRT-class serving, returning typed answers at control-loop latency.
- **Our status:** **Adopted in doctrine, numbers filed.** This is Casey's rolling-perception allocation — main characters tap the stream many cycles per minute, peon-class workers far less — arriving independently from robotics, decision models and microcontrollers in a single week. No on-device decision model is seated yet; the doctrine and the price table are.
- **Sources:** `batch-deep-learn-2-20261108.md` §1 (LFM3/d1) and §3 (ZETIC).

## P5. Published-limit routing — a model's disclosed weaknesses are class-level routing rules

- **Situation:** Deciding which question shapes may be sent to a small decision advisor at all.
- **Idiom:** Read the vendor's own limitation notes and promote them into routing rules for the whole model class: shapes the class is weak at are never routed to any small decision advisor — they go to a full model, a deterministic tool, or a human.
- **Evidence/Outcome:** TypeSafe's published limitation notes for Jev (1.13, reviewed Sep 2026) concede weakness at **arithmetic, counting, date comparison and indirect reasoning**. Batch 3's conclusion: the product "cannot count or compare dates reliably; it must never hold a veto." The negative inheritance may be the most durable kind: the rule outlives every model named today. **Grade B** (the limitation notes are a primary artefact; the disambiguation resting on them is graded solid).
- **Modality requirement:** None on the advisor — the requirement is on the router: question shapes are classified before dispatch.
- **Our status:** **Candidate — this doc is its filing.** Proposed standing routing rule: no arithmetic, counting, date-comparison or indirect-reasoning shape is routed to the advisor seat, whoever sits in it. Jev's limits are already respected informally through the never-gate rule (P6).
- **Source:** `batch-deep-learn-3-20261108.md` §10.

## P6. Advisor, never gate — behind a provider interface

- **Situation:** Any architecture tempted to let a fast, cheap, usually-right model hold a veto, sign a verdict, or take an irreversible action.
- **Idiom:** Decision models sit behind a provider interface and return *readings*. Gates, vetoes and adoption decisions live elsewhere: deterministic checks, world evidence in a store the actor cannot write, the owner. Providers are interchangeable behind the interface; the interface is the asset.
- **Evidence/Outcome:** Jacquard's standing ruling (decision models behind a provider interface; Typesafe.ai/Jev is advisor readings only, **never the gate**). External validation arrived twice in one week: Aura ships the same boundary in a commercial product (P2), and the category itself matured in public — TechCrunch reports Jev was used by **35% of paid Vercel AI Gateway teams within two weeks of launch**, nearly double the second most popular model and the fastest first-two-weeks adoption Vercel has recorded. The industry validated the category with usage; the product's own published limits (P5) validate our placement of it. **Grade B** for the external corroboration (named-source journalism reporting published platform data, its limited-view caveat stated in the piece; Aura at B−).
- **Modality requirement:** The interface itself: typed questions in, probability-bearing readings out; a provider must be swappable without caller changes.
- **Our status:** **Adopted in doctrine** (standing Jacquard ruling; the JEV rack on the Thor at :8077 is the seated instance).
- **Sources:** `batch-deep-learn-3-20261108.md` §10; `batch-deep-learn-20261108.md` §14.

## P7. Sealed-evidence swaps — a vendor lead earns a test, never a swap

- **Situation:** A challenger publishes benchmark leads over the seated advisor — on its own private test sets.
- **Idiom:** The lead becomes a hypothesis, not a result. The swap decision waits for a sealed held-out comparison on question sets we control, graded evidence-dominant; until then, nothing changes.
- **Evidence/Outcome:** The live instance: d3-ultra over Jev 1.14 on the challenger's private sets — SR-Text 87.2 vs 73.1, SR-Box 58.2% vs Jev's 45.7. Batch 2's verdict stands: "the sets are private, the runs are the vendor's… swaps require evidence-dominant results on *sealed held-out* data we control." d3-ultra is the first concrete candidate the rule has had — Apache-2.0, 27B, and it fits the Thor (BF16 ≈52 GB+ inside 122 GB unified memory; the Orin does not, absent a quantised variant). **Grade B−** for the challenger's numbers; the rule itself is fleet doctrine (Jacquard's FIX-class adoption classification: evidence-dominant on sealed held-out, rollback-proven, blast-radius-bounded).
- **Modality requirement:** The challenger must sit behind the same provider interface (P6), or the A/B measures the plumbing, not the judgement.
- **Our status:** **Adopted as rule; instance queued.** ACTIONS item 13 in the research-trail repo: d3-ultra vs Jev sealed held-out A/B — to be run when a lane has the time to do it properly.
- **Source:** `batch-deep-learn-2-20261108.md` §2, synthesis and shortlist.

## P8. The judge sits inside the loop (verification as a harness component)

- **Situation:** Multi-step agent work where grading afterwards discovers failure too late — or where the harness around the work is itself the thing being improved.
- **Idiom:** Put the verify step *inside* the work loop. Workers verify results as part of the claim cycle, before merging progress; when a harness edits itself, a composer compares the candidate trajectories against the reference and keeps only edits backed by observed behaviour.
- **Evidence/Outcome — stated precisely, because this pattern's edges matter:** AgenSH (Microsoft, MIT, paper + reproduction guide, **grade A−**): workers gather context, claim subtasks, act, **verify results, and merge progress asynchronously** — verification inside the loop, not a separate grading lane; batch 3 notes our lanes still lean on the parent for verdicts, and names AgenSH's claim/verify/merge protocol as the comparison to read before the next large parallel dispatch. Harness² (Google Cloud AI Research + Northwestern, paper + Apache-2.0 repo, **grade A−**): an editor proposes two candidate harness edits (an *invariant* candidate for general failures, a *domain* candidate for knowledge/procedures); both run on the same task; a composer compares trajectories against the reference and keeps only behaviour-backed edits. **The correction this filing carries:** in both demonstrated systems the judge is *not* a small typed decision model — AgenSH's verifiers are the workers themselves, and Harness²'s editor/composer is a frontier LLM (Claude Opus 4.8). A small decision model in the *verdict* seat is evidenced only in the selection role (Aura's triage, P2). The decision-model-as-judge form is therefore filed as the **extrapolated** form of a demonstrated harness idiom, not as a demonstrated pattern.
- **Modality requirement:** For the demonstrated form: a judge able to verify a claimed result against a reference or compare trajectories. For the extrapolated form: P1's modality pointed at verdicts — typed Score/Choice answers over a stated claim plus its evidence bundle.
- **Our status:** **Candidate.** The demonstrated form is a named read (AgenSH protocol vs our shared-state claim skill); the extrapolated form waits on a sealed trial like everything else in the FIX class.
- **Sources:** `batch-deep-learn-3-20261108.md` §2 (AgenSH) and §9 (Harness²).

---

## (a) Modality-gap register — observed, not transferable to the seated advisor

Our seated advisor (the Thor's `jev-semantic`, :8077) takes *text state* and returns typed readings. These patterns from the day's reading require modalities it does not have. Each entry names the evaluation that would close the gap; none closes by download.

- **Image grounding (Box over pixels).** d3-ultra's SR-Box: 58.2% at IoU ≥ 0.5 across 10 domains. Our advisor has no image input. *Evaluation needed:* a multimodal advisor behind the interface, graded on a sealed held-out box/score set over league-relevant imagery — and any vision-judge trial inherits the JEV-over-play warning (the embedding stream measured the filming apparatus first; the observer must be subtracted before the citizen can be seen).
- **Tracking (identity over time).** d3-ultra's Track question type has no counterpart in our interface's question vocabulary. *Evaluation needed:* a tracking question set over curator footage, under the same observer-subtraction caveat.
- **Richer typed answers (Point / Read / Estimate / Pick).** Batch 2 notes Liquid's d1 line carries typed answer forms "we don't currently have." Transfer here is an interface-vocabulary extension first and a model question second. *Evaluation needed:* re-run our existing question sets under the extended vocabulary and prove nothing regresses.
- **Spoken-modality decisions.** d1-Omni answers spoken questions with a measurable spoken-vs-written gap (DecisionBench 78.2 spoken vs 83.4 written; JevBench reversed, 89.0 vs 87.6). Our advisor is text-only; this is where the radio room would land, and the adjacent audio-model downloads are Casey's standing open items — research only. *Evaluation needed:* none until Casey opens the audio lane.
- **On-device cadence.** P4's >2.5 Hz class assumes a 2B-class model seated on the edge board; our advisor is a rack service on the Thor, a network round trip away. Transfer is a deployment change, not a model swap. *Evaluation needed:* a latency/energy measurement on the board itself (a ZETIC-style table), not benchmark scores.

## (b) The anti-pattern: model-zoo collecting

Downloads as a substitute for inheritance. One day's reading produced four providers — Jev, GLiDE, d1, d3 — behind a single typed-question shape. Everything we gained from the three we do not run arrived as *idioms*: state-once economics, absence-as-confidence, cadence pricing, published-limit routing — at zero bytes downloaded. The zoo charges three currencies: disk (the Thor's is finite and shared), evaluation debt (every seated model owes a sealed battery before it may influence anything), and attention (the scarcest resource in the system). The pattern library charges a page per idiom. Named exceptions exist and are gated (P7's candidate is the only live one); ambient collecting is not a research strategy.

## (c) Maintenance — how this library grows

- **Entry rule.** A new pattern enters only from a digestion or batch doc on this shelf, cited by filename in its Evidence line. A pattern without a shelf source does not exist.
- **Status discipline.** Statuses move (candidate → adopted-in-doctrine → adopted-in-architecture) only on a fleet artefact: a doctrine file, an interface change, a sealed run. The move is appended as a dated status note, never a rewrite — the triples discipline: append superseding corrections, do not rewrite history.
- **Gap discipline.** Modality-gap entries close the same way: by a cited evaluation record, appended, with the gap entry marked closed and dated.
- **Corrections.** When a shelf doc contradicts a filed pattern (as §2/§9 of batch 3 constrain P8 above), the pattern is corrected in place with the contradiction named — the correction is part of the record, as it is in this filing.
