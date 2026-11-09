# Ingestion audit — where the fleet's durable memory is written, and what would catch a bad entry

*2026-11-08. ACTIONS item 8 (research-trail repo): a one-pass, deterministic audit of the fleet's memory/triple ingestion points, run on the Palace lesson (batch-deep-learn-20261108.md §11): **the durable record's quality is decided at ingestion; a retrieval stack cannot recover what the miner discarded.** Palace's three silent corruption classes — structural truncation, dropped openers, quote-forked boundaries — are the template; each store below is checked for its own version of them. Classifications use the room paper's taxonomy (room-resident-expert-design-20261108.md §3.5/§3.8): engine state / hot medium / cold contacts / the lukewarm middle (carried content copies pretending to be memory — the defect class).*

*Method note: this audit ran read-only against the league stores under a ledger claim (`ingestion-audit-20261108`, filed in `pulse/ledger.jsonl` before any read of the triples seam, which the allocator + provenance lanes own today). Every check below is a mechanical read — JSON parses, pointer resolution, field census, index-vs-file diff — not an impression. Citizens untouched; nothing rewritten anywhere.*

---

## 1. The triples library — Thor `~/craftmind-league/commons/triples/`

**What enters.** Situation → plan → verified-outcome triples, appended by citizen lanes to `triples.jsonl` (13 entries, 45 KB, append-only). Admission doctrine is the strongest on paper in the fleet (the library README): outcomes judged **only from world evidence** (inventory deltas, block scans, server log lines — never self-report); every triple carries `provenance` (citizen, lane, date, evidence pointers as `ledger:<id>` / `file:<path>`) and `epoch`; an evidence pointer that does not resolve "is a defect in the triple, not a detail."

**Measured today.** Provenance is present on 13/13 entries; **all 81 evidence pointers resolve** (checked mechanically against the ledger's id set and the filesystem). Outcome statuses are honestly mixed — 6 pass / 5 fail / 2 unverified — and `retrieve.py` excludes `unverified` by default and marks it when included. The runtime consumer (`pulse/actor-client.js`, Cody's callback digest) parses defensively, per line.

**What a bad entry looks like.** Two live shapes, both already in the file's history:

- **A double-allocated number.** Prefixes `007` and `008` each name **two different triples** (`007-dig-face-travel` + `007-dip-escape-route`; `008-geist-collect-verified-chain-outcome` + `008-stance-probe`). Full ids are unique, so nothing breaks mechanically — but every human reference to "triple-007" or "triple-008" is now ambiguous, and the known collision was worse than the record said (007 was the filed one; 008 was found by this audit). This is Palace's boundary class in allocator form: the corruption is silent, and it compounds with every citation.
- **A well-formed lie.** A triple whose provenance pointers all resolve and whose format is perfect, but whose *situation* was mis-surveyed — the Mt. Moon shape (digestion-anthropic-agent-memory-20261108.md). Format gates cannot catch it; only reconciliation against source transcripts can (ACTIONS item 2, in flight under another lane's claim).

**What would catch a bad entry today.** Nothing mechanical. There is **no writer tool and no validator**: any lane can append any line with a text editor, and the README's rules are enforced by discipline alone. A malformed or provenance-free triple would be caught only when a reader trips over it. The confirmed/unconfirmed marking from ACTIONS items 2/4 is not yet present as a field (status lives inside `outcome.status`, which conflates *the run's verdict* with *the entry's verification state* — related, not identical). One read-side softness: the actor's defensive parse **silently drops** an unparseable line from Cody's callback digest — Palace's silent loss, at read time.

**Classification: hot medium with engine-state discipline.** *Evidence sentence: outcomes are judged from world state, but the store is an append-only file any lane can append to with no mechanical gate — the discipline is real, the physics is not.*

## 2. Daily logs → MEMORY.md — the promotion path

**What enters.** Lanes append raw records to `~/memory/YYYY-MM-DD.md` (November files alone: 5,059 lines, 1.8 MB) with plain shell appends — no schema, no validation, by design: the log is the raw record. A background pass (the runtime's memory system + nightly alignment synthesis) distils the logs into `~/MEMORY.md`, the curated file injected into every session.

**What decides promotion.** Criteria live inside the background pass; **no checker a lane can read or invoke exists in the workspace.** The read-side provenance tool (`memory_explain`) can show where a promoted claim came from — after promotion. Nothing validates a claim *before* it is promoted, and nothing a writing lane can run tells it whether its log line will survive distillation or in what form.

**What a bad entry looks like.** The fleet's documented disease: a lane logs a completion that never landed (claimed-but-not-done), the distillation promotes it, and the error is thereafter **injected into every session** — the blast radius of a promoted error is the whole fleet's context. Corrections survive as prose supersessions (the file carries both the original claim and its correction in several standing cases — the repo-identity and Orin-timeline corrections are the type examples); which one wins is decided by the reader's judgement and position, not by any structure. Nothing marks a superseded claim machine-readably.

**The truncation finding — measured in this audit's own session.** `MEMORY.md` is 150 lines / 61,975 bytes. The copy injected into *this* session omitted **108 of its 150 lines (~41.7 KB)** — the auditor is Exhibit A. Whatever the precise load window is, the curated file has outgrown it: a majority of the fleet's curated memory, including wherever its corrections sit, does not reach the reader, and nothing announces the omission at write time. This is Palace class (a) — structural truncation — except the truncation is at the *loader*, so re-mining cannot fix it; only the file's shape can.

**What would catch a bad entry today.** The background synthesis itself (a model pass, unpriced and unaudited from the lanes' side) and read-side `memory_explain`. No deterministic check exists anywhere on this path.

**Classification: daily logs = hot medium (the live record, honestly raw); MEMORY.md = the lukewarm middle at its tail.** *Evidence sentence: it is a carried copy that presents as the complete curated record while roughly two-thirds of it never reaches the session it is injected into.*

## 3. The studies shelf — `~/workspace/studies/` + `INDEX.md`

**What enters.** Research/digestion/design documents written by lanes, landed with an INDEX entry in a fixed format (title, date, one-line description, GRADE, KEYWORDS) — the discipline Casey set on 2026-11-08 ("searchability even days later"). Source pointers are prose-level inside the docs (vendor/paper/arXiv named in the head matter); URL-level sources are centralised in `CONTACTS-AND-SOURCES.md`.

**Measured today.** A 10-doc sample spanning batches, digestions, night studies and design papers: **10/10 index blocks carry GRADE + KEYWORDS + date**, and the sampled docs carry their source narration as claimed. The index-vs-shelf diff found one defect: **`verification-doctrine-20261108.md` sits on the shelf with no index entry** (observed at audit time; its owning lane may still be mid-landing). An unindexed doc is a room with no door: present, complete, and undiscoverable by the search discipline the shelf exists to serve.

**What a bad entry looks like.** Exactly that: a good document that never got its pointer — or an index GRADE that overstates the doc beneath it. Nothing re-reads docs against their entries after landing; the check run for this audit is the first mechanical one.

**What would catch a bad entry today.** Nothing automatic. The format is uniform because today's lanes were careful, not because anything enforces it.

**Classification: cold contacts over hot rooms — the healthiest shape in this audit.** *Evidence sentence: the index is a pointer layer that does not pretend to be the content (one-line description + grade + keywords, content fetched live from the doc), which is why its one failure was a missing pointer, not a rotten copy.*

## 4. The league ledger — Thor `~/craftmind-league/pulse/ledger.jsonl`

**What enters.** Every lane's declarations, verdicts, claims and handbacks — the coordination record the whole claim protocol reads. Free-form JSONL: 205 rows at audit time, **48 distinct key-sets**, no schema enforcement.

**Measured today.** One hard corruption, in the worst possible place: **line 202 is torn** — two entries (a cameraman renewal verdict and a triples-allocator coordination entry) fused onto one physical line by interleaved concurrent appends ("Extra data" at char 1700). Strict JSONL readers silently drop **both** records; tolerant readers recover them by luck. The coordination store is being corrupted *by coordination itself* — the LAB concurrent-writer failure (41/57) in append form. Also: 21 rows carry no `id` (unreferenceable — a triple cannot point at them, a correction cannot supersede them), 7 rows have no `kind`, and claim completeness is prose-only: of the 5 `kind:"claim"` entries, 4 carry `lane: null` — owner, scope and release condition live inside the free-text `what`, where a dispatcher cannot check them mechanically before launching against a claimed seam (the shared-state skill asks for named owner, covered state, start, and release condition; the ledger's claims mostly *say* these things, in sentences, unauditably).

**What a bad entry looks like.** It already happened: a claim and a verdict, fused and invisible to strict readers, in the one file every dispatcher trusts. A quieter version: a claim whose prose omits its release condition — nothing downstream can tell a live claim from a dead one except by reading the lane's mind.

**What would catch a bad entry today.** Nothing. The torn line sat unnoticed until this audit's parse pass; whether a given reader loses the records depends on that reader's parser, which is to say the loss is random per consumer.

**Classification: hot medium — the live coordination surface — with a torn page.** *Evidence sentence: it is the room everyone is standing in, and two of its floorboards are already fused together.*

## 5. The consult books — Thor `~/craftmind-league/commons/consults/`

**What enters.** Citizens file consults (`glm.jsonl`, `minimax.jsonl`); community drivers (ZCode/MCode seats) answer in the same book. `PROTOCOL.md` requires provenance on every answer — seat, model, latency — and doctrinally bounds the blast radius: **answers are suggestions, never evidence**; only world evidence confirms anything.

**Measured today.** **6/6 answers carry full protocol provenance** (seat, model, latencyMs all present, values plausible: `thor-zcode` / GLM-5.3 via zcode -p, 19.7–35.3 s; `thor-mcode` / MiniMax M3.1-Flash, 40.3 s). No unparseable rows in either book. The 2-per-citizen-per-hour cap is structural (filing side + driver).

**What a bad entry looks like.** Provenance here is **self-asserted by the driver that writes the answer**: a broken or misrouted driver could file an answer claiming `seat: thor-zcode` for text the seat never produced, and nothing cross-checks the book against seat-side logs. The entry would be perfectly formed and quietly false — a provenance-shaped claim, not a verified one. The doctrine contains the damage (a suggestion can mislead a citizen's afternoon; it cannot enter the triples library as evidence without a world-verified run), which is why this is the audit's mildest finding.

**What would catch a bad entry today.** The driver's own code writes the provenance block (not a freehand lane), which is a real gate of the structural kind; content-level verification of the seat round-trip: none.

**Classification: cold contacts, protocol-complete.** *Evidence sentence: the books are a contacts register with a question log — pointers to communities that hold no authority — and their pointers, uniquely in this audit, are machine-checked by the writer's own structure every time.*

---

## Fix list — severity-ordered

### [needs a lane]
1. **Ledger append integrity (worst finding).** Concurrent appends tear lines — present tense, line 202, two coordination records fused and silently dropped by strict readers. Fix shape: a locked/single-writer append helper for `ledger.jsonl` (append is a physics problem, not a care problem), plus a tolerant-reader sweep that *reports* torn lines instead of dropping them. Owner: league commons lane. The already-torn line needs an append-only correction entry, never an in-place edit.
2. **Triples number allocation — scope confirmed.** The double allocation covers **two** prefixes (007 *and* 008), not the one on record; 13 entries, full ids unique, all 81 evidence pointers resolving — so the allocator lane's renumbering risk is contained and verifiable. This audit's contribution is the scope correction; the fix is theirs (claim already live: `triples-allocator-claim-20261108`).
3. **No mechanical gate on triples writes.** The README spec is unenforced: a validator (deterministic, Class A — parse, required fields, pointer resolution, id uniqueness, ~one small script) run at append time and inside `retrieve.py` would make the fleet's best paper gate a real one. Owner: triples lane, pairs with fix 2. Same pass should split `outcome.status` (the run's verdict) from an entry-level confirmed/unconfirmed field (ACTIONS 2/4).
4. **Shelf landing has no closing check.** A doc landed unindexed today. Fix shape: a shelf lint as the landing lane's final step — every shelf doc has an index block with GRADE + KEYWORDS; every index block names an existing doc — run before handback. Small script, research-lane ownership.

### [needs Casey's ruling]
5. **MEMORY.md has outgrown its load window.** 62 KB / 150 lines against a window that demonstrably delivered only ~42 of those lines to a live session: the curated record's tail — corrections included — does not reach its readers, silently. The ruling: cap-and-split (a small index MEMORY.md + topic files, the shape the Anthropic paper prescribes) or knowingly demote the tail. Either is defensible; the current state — pretending completeness — is the lukewarm middle at fleet scale.
6. **Claims are prose-complete but not machine-checkable.** Structured owner/scope/release fields on ledger claims would let dispatchers verify a seam before launching against it. Low urgency, real payoff; it is a small schema ruling in the Jacquard direction (policy formed from structured inputs, not parsed out of sentences).

### [one-liner: done]
**None applied.** Every candidate one-liner touched a store under another lane's live claim (triples, ledger) or a policy that is Casey's to rule (MEMORY.md shape, claim schema). The audit's own writes were confined to this document and its index entries — which is itself the discipline being audited.

---

*Filed 2026-11-08 under ledger claim `ingestion-audit-20261108`. Sources: the five stores as read this pass; batch-deep-learn-20261108.md §11 (Palace); digestion-anthropic-agent-memory-20261108.md (Mt. Moon, the LAB datum, the load-window note); room-resident-expert-design-20261108.md §3.5/§3.8 (the taxonomy); the shared-state claim skill (claim completeness criteria).*
