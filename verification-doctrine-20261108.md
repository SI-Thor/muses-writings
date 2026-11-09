# Verification Doctrine v1 — two classes, one price rule, two gates

*Fleet doctrine, 2026-11-08. Status: v1, in force for all lanes until superseded by a dated revision. This is a rulebook: other lanes execute it as written. It converts ACTIONS item 1 (research-trail repo) into standing rules — the priced two-class model from the MCode seat take on Sage-A1.5 Verification Mode, the provenance/reconciliation provisions from the ZCode seat take on Anthropic's agent-memory paper, and the marks/refusals rows from the Octopus SI OS comparison.*

**Sources.** MCode seat take, `~/craftmind-league/seat-takes/mcode-verification-mode-20261108.md` (Thor) — the class split, the price rule, both gates. ZCode seat take, `~/craftmind-league/seat-takes/zcode-anthropic-memory-20261108.md` (Thor) — provenance, reconciliation, single-writer. Shelf syntheses: `digestion-sage-verification-mode-20261108.md`, `digestion-anthropic-agent-memory-20261108.md`, `decision-model-patterns-20261108.md` (all in this directory). Octopus comparison: `octopus-si-os-comparison-20261108.md` (marks and typed-refusal rows, evidence-checked in that study's appendix). Standing parent doctrine: the Watcher's Charter (`watchers-charter-20261107.md`) — this paper prices and classes what the Charter commands; it does not replace it.

**Scope.** Every check a lane runs on its own work or another lane's: verdicts, takes, digestions, publishes, builds, deploys, guards, memory writes. If a check is not Class A or Class B under §1, it is not verification — it is review, authorisation, or ceremony, and must not be booked as verification.

---

## 0. The doctrine on one screen

1. **Existence is Class A.** Did it land, was it written, is it deployed, is it alive — these are answered by deterministic assertions against the state itself. Unconditional. Never a model pass.
2. **Content is Class B.** Is this take, design, or claim *right* — these are priced by the rule in §3 and rationed by per-class error ledgers. Most content is never verified, by design, and that is the doctrine working.
3. **Gate A.** A verify pass requires a named new evidence source. No new source, no pass.
4. **Gate B.** Verification never substitutes for authorisation. A verified plan is still an unapproved plan.
5. **Marks are not emitted by workers.** Success is recorded by the runtime or verifier into a store the worker cannot write. Refusals are typed ledger rows, never silent drops.
6. **Class B runs after delivery**, except where the operator will act within seconds.
7. **A verification that cannot show the store it read and the assertion it ran did not happen.**

## 1. The two classes

The fleet's verification doctrine was born from existence failure — the agent said it happened; it did not happen — and was then generalised, unpriced, to content. The evidence now separates the two problems, and this doctrine spends the expensive solution only where it belongs.

**Class A — existence checks.** Questions of the form *did X happen / does X exist / is X live*: a command landed, a file was written, a deploy is up, a process is running, a save file is present, a refresh took effect. The answer lives in a state store — a log, a filesystem, a registry, a running process table, the world itself. Class A checks are **unconditional** (every instance, every time) and **deterministic** (a script, a grep, a state read with a boolean exit). A model pass is *prohibited* as the primary Class A mechanism: a grep for the request ID costs milliseconds and is near-perfect; a model re-reading the same log costs a model call and can still answer "let me verify."

**Class B — content checks.** Questions of the form *is this right*: is the take's reading of the paper correct, is the design sound, is the claim in the digestion supported, is the number in the report the number in the run. The answer does not live in any store; reaching it costs a second evidence-gathering pass. Class B checks are **priced** by §3 and **rationed** by the error ledgers in §4. Blanket Class B verification is abolished: on low-error classes it is not merely wasteful, it burns the operator's scarcest resource (attention and waiting time) on every completion forever, and it trains everyone to ignore verification output — a check that fires on 100% of traffic and almost never speaks is a check nobody reads.

**Boundary rule.** If a deterministic oracle exists for the question — a script, a test, a state read — the question is Class A regardless of how it is phrased. "Is this file's content correct?" is Class B; "does this file's hash match the manifest?" is Class A, and the hash check runs first, always. Conversely, dressing a content judgement in a log's clothing does not make it Class A: a log can prove a line was *written*, never that the line was *true*.

## 2. Class A rules

**A1 — Assert against the effect, in a store the actor cannot write.** The check reads the state the action was supposed to change, through a path the acting agent does not control. A worker's own log line, summary, or status report is an **echo, never a landing**.

**A2 — Scripted, boolean, named.** Every recurring Class A check exists as a named assertion (script, test, or documented command sequence) that exits true/false and prints what it read. Ad-hoc eyeballing does not discharge a Class A obligation twice; the second time a check is needed, it is written down as an assertion first.

**A3 — The known wounds are the patterns.** These are standing, named, and not to be re-derived per incident:

- **The daylight hold (league, 2026-11-08).** Refresh commands were sent every five minutes and reported sent; for nearly ninety minutes none landed, because a client modal was eating the keystrokes, and a citizen died repeatedly in a world the operator believed was held at day. Rule: a hold is verified by reading the **server log** for the landed effect, on the cadence of the hold itself. Two consecutive unlanded refreshes = alarm and park (HOLD-LOST). The sender's report is never evidence.
- **The cameraman chain (league, 2026-11-08).** Renewals verify from three independent reads — the process table (pid, start time, computed cap), the cameraman log (VERIFIED LANDED lines flowing at the expected cadence), and the meta-watcher's heartbeat/alarms — before touching anything; the renewal itself is verified the same way after relaunch (startup line, first scheduled refresh landed in the server log). Self-report plays no part at either end.
- **The pool-aside save (league, 2026-11-08).** Move-back timestamps on a directory did not prove the server's save path had seen it; a citizen joined with no save in the live directory and died for it. Rule: verify the artefact's presence **in the live location the consumer will read**, immediately before the dependent launch — not in a staging location, not by timestamp.
- **The release check (publishes).** A push is verified from a **fresh clone**: file list and byte-level spot checks against the pushed tree, visibility read back from the host's own record. The staging tree's state is not evidence about the remote.

**A4 — Cadence matches the claim.** A periodic effect is verified at its own period, not at the operator's convenience. A five-minute hold checked hourly is unheld for fifty-five minutes of every hour. Heartbeats are emitted **from effects** (the landed refresh, the written file), never from process liveness; silence past one period is a failure state, per the Watcher's Charter.

**A5 — Class A failure is a stop, not a note.** An existence check that fails halts the dependent work and raises the alarm path the surface already has. It is never logged-and-continued, and never converted into a Class B judgement call ("it probably landed").

**A6 — Escalation within Class A.** A model pass may be used only when the deterministic check is *inconclusive* — the log shows the command started but not completed, the state is ambiguous between two readings. The model is then answering a reading question about evidence the assertion already gathered, and its verdict cites that evidence.

## 3. Class B: the price rule

**The rule.** Verify a content claim if and only if:

```
P(first-pass wrong) × R × C_error  >  C_verify
```

**The constants (v1, adopted, re-derivable under §12):**

| Term | Value | Derivation |
|---|---|---|
| R (rescue rate) | **≈ 0.38** | The BrowseComp on/off arm in the Sage-A1.5 paper (Lou et al., arXiv:2610.28578): 72.5% → 82.9% over 1,266 questions = 132 of 348 first-pass-wrong answers rescued by the verify pass. |
| C_verify | **≈ 1.0 × C_task** | InferenceKey's measured on-arm: 1,890 vs 934 completion tokens (total 2.02×, so the verify pass itself costs ≈ one task), wall time 25.0 s vs 11.2 s. |
| P(first-pass wrong) | **from the class ledger** | §4. Never estimated by spending a model call on difficulty; the ledger's measured rate for the class is the input. |
| C_error | **task-cost multiple, recorded per class** | What a wrong answer in this class costs if it ships uncaught, in units of the task's own cost. Recorded in the ledger row so audits can correct it. |

**Break-evens.** Solving the rule for P with the v1 constants — verify when the class's measured error rate exceeds:

| C_error | Break-even P(wrong) |
|---|---|
| 3× task | ≈ 88% |
| 5× task | ≈ 53% |
| 10× task | **≈ 26%** |
| 20× task | ≈ 13% |
| 50× task | ≈ 5.3% |
| 100× task | **≈ 2.6%** |
| 1000× task | ≈ 0.26% |

**Worked readings.** A routine lookup class with a measured 4% error rate and a 10× error cost: 0.04 × 0.38 × 10 = 0.15 < 1 — do not verify per-instance; sample-audit (§4). A public-facing claim class with a 4% error rate and a 100× error cost: 0.04 × 0.38 × 100 = 1.52 > 1 — verify every instance, with a named new source (Gate A). A class at 30% error and 10× cost: 1.14 > 1 — verify, and treat the error rate itself as the defect to fix; verification is a bridge, not a home.

**What the easy-question evidence actually says.** On easy questions the verify mode changed nothing measurable (12 answers, all correct both ways — 3 questions × 2 runs per mode, a 100% base rate, so the test had no power to detect a benefit) while roughly doubling cost (2.2× wall, 2.0× tokens), the extra turns spent re-checking facts already confirmed. The doctrine reads this correctly in both directions: it is strong evidence about *cost* and no evidence about *efficacy on easy work* — and it is the reason Gate A exists. The mean is also bimodal in the raw runs (one hafnium on-run: 15.9 s vs 15.5 s off); C_verify ≈ 1× is a budget mean, not a per-run promise.

**The verifier need not be the first passer.** C_verify is priced on the assumption the check costs a task; a cheaper instrument — a small model with new tools, a deterministic falsifier, a targeted source read — lowers C_verify and moves the break-even down. Choosing the cheapest adequate verifier is part of running the rule, not an exception to it.

**Abstention is a valid verdict.** A verify pass must be permitted to terminate in "first pass confirmed, no new evidence sought" at near-zero cost, and to abstain rather than elaborate. A verify pass that always produces a long report is rehearsing, not verifying.

## 4. Error ledgers

**L1 — Every content class carries a ledger.** A class is a recurring kind of content work (seat takes, digestion factual claims, design papers, publish copy, build sign-offs, citizen-behaviour interpretations — the surfaces in §11 each name their class). The ledger is an append-only record, one row per audited or verified instance:

```
class | instance (link/id) | first-pass verdict | checked? (full / audit / none) |
evidence source named (Gate A) | outcome (confirmed / corrected / overturned) |
C_error assumed | cost of the check (tokens, wall, operator-minutes)
```

**L2 — The measured rate is the doctrine's input.** P(first-pass wrong) for the rule in §3 is the ledger's measured overturn+correction rate for the class. Rates are recomputed from the ledger, never asserted from memory or seniority.

**L3 — Sample audits keep unrationed classes honest.** Classes below their break-even are not verified per-instance; they are **sample-audited at 10–20%** (default 15%), drawn without the author's knowledge of which instances will be drawn where the surface allows it. Audit outcomes are ledger rows like any other. An audit that corrects an instance lands as a superseding correction to the delivered artefact where the artefact is still live — appended, never a silent rewrite.

**L4 — Cold start.** A new class has no rate. Until it accumulates **30 graded outcomes**, audit at the top of the band (20%) and treat its P as unknown in the rule — do not run per-instance verification on an unknown rate except where C_error ≥ 100×, where the break-even (≈2.6%) is below any plausible rate.

**L5 — The labels already exist.** The fleet's claimed-but-not-done incident history is labelled training data: every instance where a first pass was wrong and a later check caught it (or didn't) is a ledger seed row. New lanes populate their class ledgers from incident records before inventing estimates.

**L6 — Difficulty signals are free or they are not used.** Where a lane wants per-instance triage inside a class, it uses signals the first pass already emitted — failed or empty tool calls, hedging, single-source citation, conflicting sources, multi-hop shape, freshness requirements — never a paid difficulty-estimation call. A learned classifier over run history (the take's suggestion: logistic regression on these features, labels from the ledger) is permitted once a class ledger is large enough to train honestly; until then the class rate governs.

**L7 — The headline metric.** Each ledger reports, per period: **verifications that changed the answer per operator-minute spent.** A class whose number sits near zero is performing theatre, and theatre is cut at the next re-derivation (§12) — the check is removed or repriced, publicly, in the ledger. A class whose audits keep changing answers is under-verified and moves up a tier. The metric is computed from ledger rows; it is never estimated.

## 5. Gate A — a verify pass requires a named new evidence source

**Rule.** Before a Class B pass runs, its instruction names the new evidence it will consult: a second source, a second tool, a falsifying check, the primary text behind a summary, the transcript behind a note. If the pass can only consult what the first pass already saw, **the pass does not run.**

**Why.** The mechanism under the one solid rescue number we have is information reach: on BrowseComp the first search often points somewhere plausible-but-wrong, and the correction arrives when the verify pass reaches a *different* source. On the easy questions there was no second source worth having, and the pass degenerated into "let me verify" turns over confirmed facts — cost without rescue. A second look over the same evidence is rehearsal, and rehearsal is prohibited from booking itself as verification.

**Corollary — no-source classes.** Some claims have exactly one evidence source by construction. For those, Gate A returns a definite answer: verification is impossible, not merely unpriced. The claim is marked **UNVERIFIED-BY-CONSTRUCTION** wherever it is carried, its consumers are told, and the lane's options are to change the claim, change the question, or route the decision through authorisation (Gate B) with the unverifiability on the table. Inventing a ceremonial second look is the one prohibited move.

## 6. Gate B — verification never substitutes for authorisation

**Rule.** A passed check — either class — authorises nothing. Publication, adoption of a persistent change, curriculum changes, destructive or financial or public-facing actions, and every standing owner gate in the fleet proceed through their own authorisation path exactly as if the verification had not happened.

**Why.** Verification answers *is this true / did this happen*. Authorisation answers *may this be done*. The Sage take's formulation stands verbatim-grade: a verified plan is still an unapproved plan. Collapsing the two is how a lane talks itself into shipping on the strength of its own homework. The league's form of the same rule: operators repair substrate and floor; the citizens' curriculum stays smith-authored — a verified run does not license an operator to rewrite the exam.

## 7. Timing — Class B is asynchronous by default

**T1 — Deliver first, verify after.** For Class B work whose result the operator will not act on within seconds, the artefact ships and the verify pass (where the rule in §3 calls for one) runs after delivery. Its outcome lands as a correction when it exists. The 2.2× latency belongs on the small minority of completions that earned it, not on the critical path of every completion.

**T2 — Synchronous exceptions.** Verify before delivery only when: the operator will act on the result within seconds; the action the result feeds is irreversible; or the class sits above break-even at C_error ≥ 100× (at that price, the correction-after-the-fact is the expensive path). The exception is claimed in the ledger row, not assumed.

**T3 — Class A has no timing clause.** Existence checks are synchronous with the claim they discharge, at the cadence of §2 A4. There is no "async existence."

## 8. Mechanism, not mood — and proving the trigger fires

**M1 — Instructions specify the mechanism.** A verification instruction names: the store or source to read (Gate A), the assertion or comparison to run, the verdict shape to return (confirmed / corrected / overturned, with citations or the read state attached). "Double-check this," "review carefully," and every mood-level instruction are prohibited: unspecified verification is the measured failure mode — doubled tokens spent restating settled facts.

**M2 — A verify path is proven by behaviour change, never by its acknowledgement.** The cautionary exhibits, both from the Sage evidence:

- The authors' own platform **silently dropped** `{"verification": true}` on its OpenAI-compatible endpoint: the request returned **HTTP 200**, verification was configured, acknowledged — and off. The nonsense value `{"verification": "maybe"}` also returned 200. It was caught only by byte-diffing the rendered template with and without the flag.
- The authors' documented llama.cpp command named a reasoning format, `deepthink`, that **does not exist** (the server dies at launch; `deepseek` is the real value) — and the trigger that does exist is **case-sensitive** ("Verification Protocol" vs the template's lowercase "protocol").
- The daylight hold is the fleet's own exhibit of the same class: the sends were configured, periodic, and reported — and eaten by a modal for ninety minutes.

**M3 — The firing-proof ritual.** Any change to verification plumbing (a flag, a prompt suffix, a hook, a watcher) is followed, before the change is booked as live, by a firing proof: a planted error the path must catch, or an observable behaviour signature that differs with the path on vs off (rendered-prompt hash, distinct verdict token, changed tool-call pattern). The ritual repeats **quarterly** for standing paths, alongside the §12 re-derivation. A path that has never been observed to fire is treated as off, whatever its configuration says.

**M4 — HTTP 200 is not a behaviour.** A successful response from a verification endpoint, a green status from a watcher, a heartbeat from a process — none of these discharge anything. Class A asserts on effects; M3 asserts on the verifier itself. The strictest application of "never trust self-report" is that we do not trust our own verification switches until we have watched them visibly change what the system does.

## 9. Marks and refusals

**K1 — Marks are non-emittable by the worker.** A success mark — the record that something happened and was checked — is written **only** by the runtime, the verifier, or the operator-side store, after the applicable check passes. No tool, command, or file path by which the working agent records its own success may exist on a surface this doctrine governs. This is the Octopus row adopted as a general contract: in their kernel, *"neither the model nor an interface can emit a mark"*; a mark is recorded only after a verifier package passes, and a failed check records a failure movement while the work stays open. Our citizens' verdict triples already point this way (the verdict store is one the actor cannot write); K1 generalises the convention into a rule for every surface: scoreboards, publish receipts, build sign-offs, ledger completions.

**K2 — Where no runtime exists yet, the separation is procedural and named.** Most fleet surfaces today have conventions, not a mark-emitting runtime. Until a surface has one, the mark is written by a *different role* than the worker (the verifying lane, the parent, the script that ran the Class A assertion), and the surface's documentation says so. A surface where the worker still writes its own success record is listed as a known gap under §12, not silently tolerated.

**K3 — Refusals are typed ledger rows, never silent drops.** When a claim, request, delivery, or check is refused — by a gate, a verifier, a claim protocol, a policy — the refusal is recorded as a row carrying a machine-readable reason type, the refusing rule, and the artefact refused. Octopus again: a refusal is a typed `DeliveryRefused` row in the movement ledger, "not a silent drop"; their failed verification is likewise a recorded `VerificationFailed`, with the checkpoint left open. The fleet learned this once already in the shared-state claim protocol: collisions were invisible until they were recorded. A refusal that leaves no row will be re-attempted, misdiagnosed, or routed around; a typed row is debuggable. Silent drops are prohibited on governed surfaces.

**K4 — A mark is only as strong as its verifier.** (Octopus's own candour, adopted.) K1 does not manufacture trust; it records which verifier passed. Marks carry the verifier's identity and the check's name, so a weak verifier's marks can be re-priced when §12 re-derives the constants.

## 10. Stored claims — the memory provisions

A stored note, triple, or memory entry is a first-pass content claim with a long fuse: it will be relied on later, without re-checking, by sessions that never saw its origin. The ZCode take's three gaps are therefore Class B provisions for stored claims, and they bind here.

**S1 — Provenance and status on every durable claim.** Each entry carries: a pointer to the transcript, session, or run that produced it, and an epistemic status — **unconfirmed / confirmed / contradicted**. The CL-Bench ladder is the evidence: the first model to fully close the learning loop wrote *rules plus how each rule was known to be true plus trap warnings*; the model a generation earlier that marked checked-vs-unconfirmed was already most of the way there; the failure mode was untested guesses scattered as files — predictions posing as knowledge. A bare (subject, predicate, object) store with no provenance is a wrong-note generator: a fact written wrong or drifted stale is trusted forever.

**S2 — Reconciliation: the Mt. Moon pass.** Raw session logs stay immutable. On the standing distillation cadence, a reconciliation pass samples the **oldest and least-verified** stored claims and checks them against the transcripts that produced them, rewriting contradicted entries and marking the correction in place (append a superseding entry; never rewrite history silently). The type case: a wrong note ("the PokéCenter is east") survived because nothing ever compared it to the transcript; one dreaming pass with the transcript as ground truth caught it, and the corrected run went straight through. Reconciliation is the Class B pass that stored claims periodically owe; Gate A is satisfied by construction — the transcript is a source the note-writer's summary never consulted as evidence.

**S3 — State is re-read, not stored; derived knowledge is what memory holds.** Durable memory holds plans, tested rules, traps, and strategy — what the world does *not* re-tell you every turn. Volatile state (positions, inventories, balances, who-is-where) lives in the queryable layer the world itself backs, and is read at need. Storing re-told state is the measured disease: the 413-file archive that went continuously stale until curation ate the play. A stored claim that duplicates a Class A read is deleted in favour of the read.

**S4 — Single writer per shared entry.** Concurrent writers on a shared table measurably destroy content: 41 of 57 graded facts survived multi-writer edits; the single-writer, per-page, verbatim-quoting rebuild kept 57 of 57 (the intervention bundled three changes, so attribution is confounded — the direction is not in doubt, the exact share due to single-writership is). Governed stores assign each shared entry one owning writer; other lanes propose, the owner writes. Growth is capped by structure: pages stay indexes with links, not copies of the territory — a memory that grows larger than its sources has abstracted nothing.

**S5 — Steering is tiered; consults are routed by task shape.** For strong models, doctrine states what memory is *for* and stops: prescribed capture rules measurably *reduced* the benefit for frontier models ("record only failures" stripped most of it). For weak, citizen-class reasoners, prescribe the checklist — read your notes before acting; test a theory before it becomes a rule — the prompting that nearly doubled the weaker model's score. Consults route by shape: curated books/wikis for cross-source synthesis and judgement questions; direct store queries for single-fact lookup, where the curated layer adds nothing over search.

## 11. Applicability — the doctrine on live surfaces

| Surface | Class A (always, deterministic) | Class B (priced, ledgered) | Default timing / notes |
|---|---|---|---|
| **League verdicts** (exam passes, collect/craft checks, triples) | World/server state only: displacement, inventory sync, save presence in the live directory, landed daylight. Self-report is an echo (§2 A3). | Interpretations — is this behaviour graduation-worthy, is a route a *learned* fix vs scaffold luck. Class: `league-interpretations`. | Verdict marks written by the verifying lane, never the citizen's stack (K1). Gate B: a verified run never licenses curriculum changes; the smith authors, operators repair substrate. |
| **Seat takes** (ZCode / MCode / Claude Code research) | File exists on the named box, byte count, tail intact, seat process exited as reported. | The take's claims: are its readings of the primary right, are its numbers the source's numbers. Class: `seat-takes`. | Async by default (§7). Gate A exemplar: the ZCode provenance episode — seat substantively right, its receipt missing; caught because the parent cross-checked four secondary sources, a named new source, and ledgered the correction. |
| **Digestions & batch studies** | Cited file exists; quoted figures byte-match the source where quoted; link targets resolve. | Interpretive syntheses, grades, fleet mappings. Class: `digestions`. | Async; sample-audit the factual-claim rate at the band; syntheses verified only above break-even. |
| **Publishes** (repos, pages, releases) | Fresh-clone byte checks, ls-remote state, visibility read-back, tag/commit identity (§2 A3). | Content correctness of what ships. Class: `publish-content`; C_error is typically high (public, persistent). | Class A synchronous, always. Gate B is absolute here: verification never publishes; the owner's word publishes. |
| **Builds & deploys** | The released artefact — cloned from its tag, not the working tree — builds, runs, answers on the exact surface the user will use; health = a behaviour assertion, not HTTP 200 (§8 M4). | Design soundness, the build's own claims about itself. Class: `build-signoff`. | Class A before any "done" is spoken. A user-facing door is done only when it has answered back through that surface. |
| **Guards, watchers, holds** | Effect-heartbeats at the claim's cadence; silence past one period is a failure state (Charter; §2 A4). | The guard's *policy* (thresholds, deadbands) is a design claim, reviewed as content on change. | Class A continuous. Firing-proof ritual (§8 M3) applies to the guard itself. |
| **Memory writes** (triples, curated memory, consult books) | The write landed in the store at the named path; single-writer ownership held (S4). | The claim itself: provenance + status at write time (S1), reconciliation on cadence (S2), state-vs-derived split (S3). | Status starts *unconfirmed* unless the writer names its confirming source. Promotion to always-loaded layers is a Class B decision with the smallest blast radius kept in mind — an injected wrong note rides every session. |
| **Decision-model readings** (advisor surfaces) | The reading arrived, in schema, from the named provider. | Never applicable as verification: an advisor reading is a *reading*, never a gate, a verdict, or a check on anything (provider-interface doctrine). | A decision model may be the cheap verifier inside a Class B pass only where the pass's Gate A source is evidence, not the model's own say-so. |

## 12. Honest limits — what the constants rest on, and what would change them

This doctrine's authority is operational, not statistical. Its limits, stated so a future lane can re-derive rather than re-litigate:

**E1 — R comes from one benchmark family.** R ≈ 0.38 is derived from BrowseComp alone: hard-to-find facts, where the rescue mechanism is a second *search*. Fleet classes whose new evidence is a world-state read, a transcript, or a second model may rescue at a different rate — plausibly higher (a transcript reconciliation is a stronger instrument than a second web search) or lower. R is adopted as a placeholder constant, and §4's ledgers exist precisely to replace it with measured per-class rescue rates. The first re-derivation that contradicts 0.38 for a class wins for that class.

**E2 — The easy-question arm proves cost, not inefficacy.** n = 6 answers per mode, 100% base rate, no discriminating power; the 2.2× headline is a mean over a bimodal distribution. The doctrine uses it only as a cost measurement and as the Gate A motivation. Anyone citing it as "verification doesn't work on easy tasks" has overstated the evidence; the correct claim is "no benefit was detectable, at double cost."

**E3 — The headline ambiguity is unreconciled.** The Sage paper's headline BrowseComp figure (81.7, 82.8 with orchestration) vs the on/off arm (72.5 → 82.9) cannot be fully reconciled from the relayed sources — whether the headline already includes the verification gain is explicitly undetermined in the InferenceKey write-up. The doctrine's R uses only the on/off arm, the one comparison with a stated design.

**E4 — Nothing here is independently reproduced.** The BrowseComp arm is the authors', run BF16 on their harness; the independent run used a 5-bit quant on llama.cpp with different tools, did not reproduce the benchmark, and never observed the authors' demo-grade structured review ("what is established, what failed") — so whether the *trained structured* behaviour rescues at a different rate than plain re-checking is unknown. Gate A is the doctrine's operational substitute for that missing behaviour. Seed variance on such harnesses is typically ±1–2 points; the +10.4-point effect is far outside that band, the fine structure is not.

**E5 — P and C_error are the soft terms.** P is only as good as the ledger behind the class (§4 L4 handles the cold start crudely, by band-top audits). C_error is a judgement recorded in task-cost multiples; two honest lanes can differ by an order of magnitude on what a shipped error costs, and the rule's output flips across that range at mid error rates. The ledger records the assumed C_error per row so audits argue about a written number, not a vibe.

**E6 — The marks contract is ahead of our runtime.** §9 adopts Octopus's non-emittable marks as doctrine; Octopus implements them as a kernel property with verifier packages, while most fleet surfaces still rely on role separation (K2). Until a surface has a runtime that records marks, its K1 compliance is procedural — a determined worker on such a surface could still write its own success record. That gap is listed, per surface, wherever the surface's own documentation lives; closing it is engineering, not doctrine.

**E7 — Provenance evidence is strong in design, soft in number.** The memory provisions (§10) rest on Anthropic's paper: controlled steering A/Bs and LAB arms on one side; single-run Pokémon anecdotes, a constructed Mt. Moon demonstration (its no-memory control arm corroborated by secondary coverage, not the post's body text), and no error bars anywhere on the other. The doctrine adopts the *structure* (provenance, status, reconciliation, single-writer) because each element also matches a fleet incident we measured ourselves — not because the paper's numbers are hard.

**Revision protocol.** Constants and tier boundaries are re-derived **quarterly** from the ledgers (§4 L7's metric is the agenda), or immediately when a ledger's measured rate crosses its class's break-even in either direction for two consecutive periods. Revisions are appended as dated amendments to this file with the ledger evidence cited; the superseded constants stay readable. A doctrine whose constants cannot be changed by its own ledgers is a mood, and §8 prohibits moods.

---

*Filed 2026-11-08 under ACTIONS item 1 of the research trail (SuperInstance/research-trail-2026-11-08), which asked for the two seat takes to be split into doctrine: Class A existence checks deterministic and unconditional; Class B content checks priced and rationed. Companions: `watchers-charter-20261107.md` (the parent doctrine this paper prices), `decision-model-patterns-20261108.md` §P8 (the judge inside the loop), `digestion-sage-verification-mode-20261108.md` and `digestion-anthropic-agent-memory-20261108.md` (the one-page maps of the two seat takes).*
