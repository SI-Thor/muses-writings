# Room — Decision models & verification

## STATE

Doctrine landed today. Verification Doctrine v1 is DONE (ACTIONS item 1): Class A existence checks are unconditional and deterministic; Class B content checks are priced by the verify-iff rule. The decision-model patterns library is written — eight patterns in triples shape plus the modality-gap register — under the working phrasing *the fleet collects tells, not models*. The triples substrate hardened the same day: provenance + reconciliation (item 2) and the single allocation path (item 3) both landed, per the trail record. Parked or running: the d3-ultra vs Jev sealed held-out A/B (item 13) is a named candidate, not yet run; the WSP loop-direction hunt (item 9) was dispatched under Casey's blanket authorisation and has no verdict in the trail yet. Last touched 2026-11-08.

## CONTENTS

- [Decision-model usage patterns](../../decision-model-patterns-20261108.md) — the pattern library: state-once economics; frame/triage/reflexes; absence-as-≈0-confidence with hard fail; cadence classes; published-limit routing (Jev's four limits: arithmetic, counting, dates, **indirect reasoning**); advisor-never-gate; sealed-evidence swaps; judge-inside-the-loop (**flagged extrapolated** — the demonstrated judges in AgenSH/Harness² are workers and frontier models, not small decision models). Closes with the modality-gap register and the model-zoo anti-pattern: patterns transfer behind the provider interface; models are interchangeable witnesses.
- [Verification Doctrine v1](../../verification-doctrine-20261108.md) — the rulebook. Class A: verify effects in a store the actor cannot write, scripted, unconditional. Class B: verify iff P(wrong) × R × C_error > C_verify, with R ≈ 0.38 (BrowseComp rescue 132/348 — a placeholder from one benchmark family, explicitly awaiting replacement by our own ledgers) and break-evens ≈26% at 10× error cost, ≈2.6% at 100×. Gate A: a verify pass needs a *named new evidence source*. Gate B: verification never substitutes for authorisation. Marks K1–K4 non-emittable with typed refusals — K1 compliance is procedural until a mark-recording runtime exists (named gap). Decision-model readings are barred from serving as verification.
- [Sage Verification Mode digestion](../../digestion-sage-verification-mode-20261108.md) — index entry for the MCode seat take: the verify-iff rule priced against the InferenceKey primary read (12/12 in both modes on easy questions at 2.2× time and 2× tokens; BrowseComp 72.5% → 82.9% on hard questions). The easy-question arm proves cost, not inefficacy — recorded as such.
- Seat take (pointer, Thor-side): `~/craftmind-league/seat-takes/mcode-verification-mode-20261108.md` — the full MCode take behind the digestion entry, including the silently-dropped `{"verification": true}` flag exhibit.
- [Anthropic agent-memory digestion](../../digestion-anthropic-agent-memory-20261108.md) — index entry for the ZCode seat take: our architecture matches Anthropic's endorsed design, and all three gaps sit in the verification layer (provenance + reconciliation for triples; state-vs-derived split with single-writer ownership; tiered steering). The source of ACTIONS items 2 and 4.
- Seat take (pointer, Thor-side): `~/craftmind-league/seat-takes/zcode-anthropic-memory-20261108.md` — the full ZCode take behind the digestion entry.
- [MTO Agent comparison](../../mto-agent-comparison-20261108.md) — the LinkedIn "one boss, crew of workers, brain that never writes" assembly (dsh-superagent + MTO criteria + Laya) graded against our stack: same slogan, different invariant (their judge never *generates*; no model of ours ever *gates/writes the record*); nothing exceptional, convergence noted as evidence, and one real find — **Laya**, an open-weights local Jev-class decision model, filed as a provider-seam candidate with a pre-registered sealed trial and its five published traps as the intake checklist.
- [Octopus SI OS comparison](../../octopus-si-os-comparison-20261108.md) — the ProArt ZCode deep comparison. Steal: typed refusals as ledger rows, formed-never-stored policy, non-emittable marks (ACTIONS items 17–19, filed for the next Jacquard design pass). Don't steal: per-call synchronous approvals. Open question carried in its own thread below.
- [Batch deep-learn #3](../../batch-deep-learn-3-20261108.md) — home room for this batch. Its decision-model spine: §10 disambiguates TechCrunch's Jev as TypeSafe's Jev (the same product as Jacquard's advisor and Aura's triage component); §11 clears JiRack as a namesake, unrelated to our JEV rack; §§2/9 (AgenSH, Harness²) ground the judge-inside-the-loop pattern and its correction.
- [Batch deep-learn #2](../../batch-deep-learn-2-20261108.md) *(cross-reference; home room: fleet-and-substrate)* — §2 is the d3-ultra file: the vendor's private-set lead (SR-Text 87.2 vs Jev 73.1) and the ≈7.3 ms marginal cost per extra question that make it the named challenger for a sealed A/B; §1 (LFM3/d1) is the category confirmation at 2B on-device.
- [Watcher's Charter](../../watchers-charter-20261107.md) *(cross-reference; home room: the-league-and-civilization)* — the doctrine's ancestry: verify the effect in a store you cannot write (Rule 1) is Class A before Class A had a name.

## OPEN THREADS

- **d3-ultra vs Jev, sealed held-out A/B** (ACTIONS item 13). Waits on: construction of the sealed set. Whoever wins, Jev stays advisor-only, never the gate (item 26, standing).
- **WSP loop-direction hunt** (ACTIONS item 9) — IN FLIGHT under the blanket authorisation; no verdict in the trail yet. Its rule: edits unblock, they don't add (the Gemma-control null); adoption of any patch is Casey's gate, whatever the hunt finds.
- **The mark-recording runtime (K1)** — the doctrine's named gap: until it exists, non-emittable marks are a procedure, not a mechanism. Waits on: a Jacquard/runtime design pass.
- **R ≈ 0.38 replacement** — the constant is one benchmark family's placeholder; our own error ledgers are supposed to replace it (quarterly re-derivation is in the doctrine). Waits on: graded outcomes accumulating.
- **ACTIONS items 17–19** (typed refusals, formed-never-stored policy, non-emittable marks as a runtime contract). Waits on: the next Jacquard design pass.
- **The Octopus open question** — can a Jacquard charter admit a delegate *more capable* than its delegator (their creator-is-not-an-input) when our claims inherit the claimer's scope? Unanswered; filed with the steal list.

## ANNOTATIONS

- Disambiguation is load-bearing in this room: **Jev is TypeSafe's Jev everywhere** (TechCrunch, Jacquard's advisor, Aura's SDK, d3-ultra's baseline); the Thor's local `jev-semantic` ONNX judge is a deliberate namesake in the same seat — never merge the product's benchmarks with the local service's measurements. **JiRack is a namesake only** (CMS Manhattan ternary LLMs) — not the JEV rack, not Jira.
- The JEV-over-play spike was a clean negative (embeddings measured the filming apparatus: baseline 6/7, I-JEPA 0/7, V-JEPA 1/7). It disciplines every "just embed it" proposal in this room; it does not touch La-JEPA's control-substrate claim (benchmarks room).
- Never quote R ≈ 0.38 without its provenance. A constant with a named replacement plan is honest; the same number quoted bare is how placeholders harden into doctrine.
- Superseded: the pre-doctrine habit of treating a second read of the same evidence as verification. Gate A killed it — same-evidence re-reads are rehearsal.

## FURTHER READING

- TypeSafe AI — Jev (typesafe.ai) and vLLM Semantic Router — d3-ultra — via [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md): the incumbent and the named challenger, with the standing verdicts.
- Microsoft AgenSH and Google Harness² — via CONTACTS: the published-scale claim/verify and harness references behind the patterns doc.
- Octopus SI OS (github.com/miuuyy/Octopus-SI-OS) — via CONTACTS: headline claims verified accurate against the repo; scenarios are intended use, not tested features.
- Sage-A1.5 / InferenceKey — via CONTACTS: the measured cost side of verification that priced the doctrine's rule.
