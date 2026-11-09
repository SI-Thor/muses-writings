# Room — The shelf itself

## STATE

The meta room: how this shelf is written, indexed, audited and kept. The shelf was stood up on 2026-11-08 under Casey's standing instruction — thorough markdown research and digestion documents for everything submitted, with contacts and searchability that survive days — and sharpened the same day into this rooms layer: documents left in rooms, structured for return, never trusted to any agent's context. The ingestion audit (ACTIONS item 8) is DONE: every durable store's write path checked, findings severity-ordered. MEMORY.md's cap-and-split is DONE the same day (150 lines / 62 KB → 50 lines / 17.8 KB; all 122 entries accounted for exactly, 29 kept in the core, 93 moved verbatim into ten topic files behind one-line pointers). What would reactivate this room: the G2 retention design pass (the policy is composed; the costing is not), or the next audit cycle. Last touched 2026-11-08.

## CONTENTS

- [The ATLAS + this rooms layer](../../ATLAS.md) — the lobby and the nine room files, including this one. The layer copies no content: every entry is a cold contact (path + annotation), so the rooms cannot rot the way a summary does — they can only go stale in their state paragraphs, which carry dates for exactly that reason.
- [The ingestion audit](../../ingestion-audit-20261108.md) — one deterministic pass over every path by which durable memory gets written (triples miners, daily-log → MEMORY.md promotion, this shelf, the league ledger, the consult books), each store classified under the room paper's taxonomy. Headline findings at audit time: a torn ledger line (two records fused by concurrent appends — since repaired, with the append helper now the only sanctioned path), the triples number collisions (007 *and* 008), MEMORY.md outgrowing its load window (108 of 150 lines never reached the auditing session — since split), and the consult books as the cleanest gate in the fleet (6/6, full protocol provenance). Zero one-liner fixes were applied: every candidate touched another lane's claim or Casey's ruling, and the audit said so instead of freelancing.
- [INDEX.md](../../INDEX.md) — the flat search surface: every document with a grade and a keywords line, the Jev/JiRack disambiguation notes, pointers off the shelf, and the searchability test log at its foot (six terms, all landing where they should — re-run whenever a batch lands; a term that stops landing is an index defect, not a searcher defect).
- [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md) — the contacts layer: every organisation, project, repo and recurring source across the shelf, deduplicated and alphabetised, with what we took and our standing verdict for each.
- [Decision-model patterns](../../decision-model-patterns-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — listed here for its closing maintenance rules: the patterns doc is the one shelf document that specifies how *itself* is to be kept (patterns are re-derived from evidence, models are interchangeable), and this room administers that rule.
- [Verification Doctrine v1](../../verification-doctrine-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — the standard this shelf's own claims are graded under: existence checks deterministic, content checks priced, a self-report is an echo, never a landing.
- [Seed #1 digestion, §3b / G2](../../seed-mud-ideas-digestion-20261108.md) *(cross-reference; home room: rooms-and-engine-state)* — the retention policy was composed there (transitions forever / features medium / raw short-ring); this room is where its per-store costing and administration will live when G2 runs.

## OPEN THREADS

- **G2 — the retention design pass.** The policy exists as a composition; what it waits on is a launch word, then arithmetic: measure current growth rates (curator footage/day, league logs/day, ledger/day), assign every named store a tier, a horizon and a cull mechanism, and prove the kept tiers regenerate the working picture before any raw ring is allowed to turn over. Its home thread is in the rooms-and-engine-state room; its deliverable lands here.
- **The claim-landing rule** — today's allocator/provenance race produced the general form: a claim is not landed for other lanes until it is *re-read* as landed (the same law as the cameraman's landing-verification, and as G1's seal lesson in the benchmarks room). Waits on: nothing but habit — it is stated here so the next parallel dispatch inherits it.
- **MEMORY.md's ongoing shape** — the split is deliberate, recorded in the daily log so background memory passes read it as structure, not damage: core-worthy promotions go to MEMORY.md, everything else to the matching topic file. Waits on: the background passes honouring it; a future audit can check.
- **Index hygiene** — INDEX.md's own standing rule: if a study exists in the directory and is not listed, the index — not the doc — is what's wrong. The rooms layer adds the twin rule: if a document is in no room, the atlas is what's wrong.

## ANNOTATIONS

- This layer's founding distinction (from the room paper): links are cold contacts — they hold no content, so they cannot rot; state paragraphs are hot, so they are dated and short. When a state paragraph and the trail disagree, the trail (ACTIONS.md statuses, ledger handbacks) wins and the paragraph is the defect.
- Supersession on this shelf is stated, never silent: a superseded document keeps its file and gains an annotation (the la-jepa PENDING marker's fate — replaced by the spike record, with the digestion pointing at both — is the template).
- The audit's restraint is a precedent, not a gap: when every candidate fix touched another lane's claim or Casey's ruling, the correct output was the finding, severity-ordered — not the fix.

## FURTHER READING

- Palace — via [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md): the ingestion law (memory quality is decided at ingestion; a retrieval stack cannot recover what the miner discarded) that the audit operationalised.
- Anthropic, "The components of agent memory" — via CONTACTS: the taxonomy the shelf's stores were classified against.
