# Syndicate Survey Adoptions — Wiring Amendment

*Follow-through on `minecraft-agent-videos-survey-20261108.md`, Movements C/D/E. The survey adopted four frontier singletons "for the fleet anyway, with concrete wiring noted" (Movement E.1, singletons; Movement C.1, field-ahead list; Movement E.2, closing paragraph). This amendment does the wiring, so the adoptions are programme law for the Syndicate Protocol and Pilot A — not marginalia in a survey. Commissioned under Casey's keep-going charter of the Syndicate build programme, 2026-11-08. Design authority remains `syndicate-protocol-design-20261108.md` + Addenda 2/3; build authority remains `syndicate-of-four-spec-20261108.md` (cited below as "the spec," by section). Where the spec's body and this amendment differ in detail, this amendment governs the four points it covers and the spec governs everything else; the spec carries appended annotations pointing here and is not rewritten.*

*Process note: grounded first-hand for this amendment — the survey's Movements C/D/E in full; the spec in full, including its existing end annotation (the decode-rate settlement), whose pattern the new annotations follow; the game master's live receipt format (Thor `~/game-master/receipt-log.md`, 5,437 B, read 2026-11-08: headed prose sections — What changed / Why / Answering / What it hoped the party would do / How to reverse it / Proof it landed / What happened next); the curator manifest shape (Thor `~/curator/manifests/manifest-*.jsonl`: per-moment lines carrying `citizen`, `event_citizen`, `on_screen`, `type`, `score`, `reason`, `segment`, `in`/`out`, `correlation`); the comms and consult stores the comm-cost counters read from (`commons/comms/chat.jsonl` — `{ts, kind, from, to, text}`; `commons/consults/glm.jsonl` + `minimax.jsonl` — consult/answer lines with `provenance{seat, model, latencyMs}`); and the governor ledger (`ledger/mind-calls.jsonl` — `{ts, agent, model, status, mind_seconds, prompt_tokens, completion_tokens, total_tokens}`), whose fields already carry everything Adoption 4 needs. No store named below has to be invented; every adoption is a field, a ceremony, or a counter over a store that exists.*

---

## Adoption 1 — The fault-owner field (survey Movement D, Q◆3; rubric D.11 Q7)

### What

Movement E's third convergent question — *whose fault is it: agent, harness, prompt, budget, or luck?* — is asked independently in at least five sources and argued everywhere a failure is discussed at length (E.1 ◆Q3). GoldActual's set is the fullest (D.4: money running out filed as a budget fact, the chat toggle as a harness fact, the respawn mechanic as luck). The fleet's judges currently cannot ask it in a field: the league files a *failure class* on verdicts and the spec (§7.7) files a two-value failure *column* (substrate / script), but neither names a causal owner at the grain a reflection tier can act on. This adoption makes the owner a mandatory, enumerated field.

### The field

**Name:** `fault_owner` (JSON stores) / the line `**Fault owner:**` (prose receipts).
**Values — exactly six, no others:**

| Value | Definition | One-line test |
|---|---|---|
| `agent` | The citizen's own decision or actuation, taken with correct input and a working capability, was wrong. | Would a correct decision on the *same* citizen-local input have avoided it? If yes and nothing upstream was broken, it is `agent`. |
| `harness` | The fleet's apparatus — body stack, movement driver, governor routing (not its budgets), perception rotation, plugin, cameraman/hold process — prevented a correct action or misreported state. | Does the log show a tool/driver/process error, or does replaying the same decision through a working harness succeed? |
| `prompt` | The instruction itself caused it: the playbook line, persona/taste line, scaffold ("super prompt"), or brief that the actor faithfully followed. | Can you point to the filed line the actor was obeying when it went wrong? Faithful obedience to a bad line is `prompt`, never `agent`. |
| `budget` | A ration ran out or denied the call: governor calls/mind-seconds, consult caps, API balance. | Is there a metered receipt (denial, 429, exhaustion) timestamped *before* the failure? No receipt, no `budget`. |
| `luck` | A world stochastic event no reasonable plan prices: a remnant hostile at spawn, an unseeded mob, a mechanic nobody was told about. | Is the event in the server log, and was it unpredictable from citizen-local state at decision time? Predictable-but-unpriced is `prompt`, not `luck`. |
| `world` | The world's own state is the cause: terrain relief (the wedge), the spawn-protection square, a moved Door, saved difficulty. | Is it a surveyed world fact, independent of actor and apparatus, reproducible offline from saved state? |

Two discipline rules, from the critics themselves:

- **One primary owner.** Secondary contributors go in the evidence sentence, not in a second value. "The AI failed" is not an attribution (D.11 Q7); neither is a list of all six.
- **Provisional is a flag, not a value.** Where attribution honestly stops (D.11 Q9 — "I'm simply not smart enough to know why" is a complete critical sentence), the writer still files a best-evidence value and appends `fault_owner_provisional: true` (JSON) or "(provisional — attribution stops at: *what is known*)" (prose). A record may not be left ownerless because the evidence is thin; it may be left *flagged*.

### Where it lands

**(a) Game-master receipts — Thor `~/game-master/receipt-log.md`.** The live format is headed prose sections (quoted in the process note above). Every **nudge** section gains the line immediately after its **Why** / **Answering** block, and every **incident** section (standing-down notices, HOLD-LOST records, and any future incident heading) gains it as its second block:

```
**Fault owner:** world — the condition this nudge answers is a surveyed
world fact (rain settled open-ended across three checks); no citizen,
harness, or budget failure is in evidence.
```

For a nudge, the owner names the owner of the *condition the nudge answers* — that is what makes the log's existing history legible (Nudge 2's growth-rate nudge answers a `world` condition; the standing-down notice's bottleneck — citizen absence — would file `agent`-side absence honestly as no-fault and therefore, under the one-owner rule, as `world` with the evidence sentence saying the world sat empty, *not* as an agent failure). The GM's code change is one line in its receipt template; nudges 1–3 are **not** backfilled — the field applies from the next receipt forward, and this amendment is the receipt that says so.

**(b) The Syndicate referee register — spec §6.1, `registrar.jsonl`.** The register's entry shape `{ts, round, kind, description, receipt-ref}` gains two keys on every entry of kind `incident` or `nudge`: `"fault_owner": "<value>"` and `"fault_owner_evidence": "<one sentence, naming the store consulted>"`. Entries of kind `board-change` are exempt — a registered change is a fact, not a fault (sealed changes are Adoption 2's business). A change *discovered to have been caused by a failure* gets a separate `incident` entry carrying the owner; the `board-change` entry itself stays clean.

**(c) The spec's round manifest (§7).** Phase 3's round record (spec §7.4/§7.5) gains an **incident log table**: one row per incident in the round — timestamp, what happened, evidence store, `fault_owner`, provisional flag. Additionally, each of the five criterion verdict lines (§7.7) gains a trailing `fault_owner` naming the primary owner *when the criterion fails*; a passed criterion files no owner (there is no fault to own).

**(d) The league's own verdict lines — reconciliation, not duplication.** The league already files a failure class on verdicts (its standing rule; e.g. CELL-BOUND WEDGE in the triples/ledger record) and the spec's §7.7 maps each criterion to a failure column (substrate / script) for kill-condition accounting. **Neither is replaced.** The reconciliation is two-level, stated once and binding in both programmes:

- **Level 1 (unchanged):** the existing class / column. It answers *which kill condition applies* — an accounting question.
- **Level 2 (new):** `fault_owner`. It answers *what caused it* — a learning question, and the one Tier L's triples (§5.3 of the spec) must carry: every triple filed for a failure gains the owner, so a play with three filed failures shows not just that it failed but *whose* failures they were — three `prompt` failures kill the play; three `luck` failures kill nothing but the scenario's assumptions.

Mapping, so the two levels can never be filed inconsistently (the column is derivable from the owner, not chosen separately): `harness`, `budget`, `world` → substrate column; `agent`, `prompt` → script column; `luck` → files under whichever column the criterion already sits in, with the owner recorded as `luck` so a lucky failure is never laundered into a substrate kill or a script kill. Worked mappings from the league's existing record: CELL-BOUND WEDGE → class unchanged, owner `world`; governor mind-budget exhaustion mid-attempt (the 600/600 pattern in the curator's build survey) → owner `budget`; a phantom dig past the ~4.5-block server reach → owner `harness` (the driver's completion claim is the apparatus misreporting state); an evening voice line overclaiming a finished hut → owner `prompt` if the template invited it, `agent` if the line was generated against the template — decided by pointing at the line, per the `prompt` test above.

### Cheapest verification it is live

At Pilot A Phase 0, one grep pair over the Thor: count `^## ` headings in `~/game-master/receipt-log.md` written after this amendment's date and count `**Fault owner:**` lines in the same range — the counts must match; and `jq -r 'select(.kind=="incident" or .kind=="nudge") | .fault_owner' registrar.jsonl` must return no `null`. Either check is one command; both are added to the spec's pre-drop checklist by the annotation appended to it.

---

## Adoption 2 — The hash-sealed Tier-W change (survey A.17/D.9; C.3 "sealed truth"; E.1 singleton, adopted regardless)

### What

The Short's creator sealed the ground truth — `sha256 … = "NOT BITTEN|…"` — *before* any model answered, so the reveal was verifiable and no reading could be retrofitted (A.17). The survey's C.1 names this "directly applicable to seeded Tier-W changes," and E.2 repeats it. The spec's seeded Round 2 change (§6.2, THE DOOR MOVES) is currently specified in the open, inside the spec itself: anyone operating Round 2's reflection — or writing its verdict — could, in principle, retrofit what the change "was" (its distance, its timing, whether it was registered before or after reflection closed) to fit the outcome. The seal removes that degree of freedom.

### The ceremony

Five steps, with named roles. **Writer** and **holder** are different seats; **Tier L and its operators are neither.**

1. **Write (before Round 1's script phase ends).** The writer — the manager seat (ProArt Claude Code, per the production shape) — writes the change's full specification to a plaintext file, `sealed-tierw-round2.txt`, containing exactly: the change kind; the old site's coordinates; the new site's coordinates; the monument's dimensions and sector grid; the supply-distance consequence in blocks; the exact text that will appear in `registrar.jsonl` at seeding time (see step 3); the restoration note (how the arena returns to baseline). Nothing about detection grades or expected playbook responses goes in the file — it specifies the *world*, not the hoped-for verdict.
2. **Hash and file the hash (before Round 1 begins).** The writer computes `sha256sum sealed-tierw-round2.txt` and files, in the **round manifest** (spec §7.1 gate artefacts): the hex digest, the filename, the writer's seat identity, and the UTC timestamp. This filing is a Phase 0/Phase 1 gate: **no hash in the manifest, no Round 1 drop** — added to the pre-drop checklist by annotation. The plaintext does **not** enter the manifest, the repo, the playbook directory, or the Thor.
3. **Hold.** The holder — Muse (the parent lane), not the manager seat — keeps the sole plaintext copy off the Thor (Oracle-side, mode `0600`, outside any git working tree). Tier L runs on Thor-side evidence packs; the plaintext is not in any evidence pack, and the spec's §6.2 is **excluded from Tier L's script-phase input list** for Round 2 (the input list is filed in the manifest; this exclusion is named there, so an UNDETECTED verdict cannot be excused by — or credited against — a document Tier L was never given).
4. **Seed (after Round 1's reflection closes — spec §7.5 ordering, unchanged).** The GM executes the change by retrieving the plaintext from the holder at seeding time. The `registrar.jsonl` entry it writes is deliberately terse — `{ts, round: 2, kind: "board-change", description: "sealed board-change <first 8 hex of the filed digest>", receipt-ref: <GM receipt id>}` — so the register announces *that* a change exists (the spec's "a change not in the register does not count as announced" rule still binds) without leaking *what* it is beyond what a scout's sweep would find anyway.
5. **Reveal (at Round 2 scoring — spec §7.4 applied to Round 2).** After Round 2's census and before the manager seat classifies the playbook diff (§6.3's swap/patch grading), the holder publishes the plaintext into the round record. Anyone can then run `sha256sum` on the revealed text and compare it against the manifest digest filed before Round 1. A mismatch voids the §6.3 calibration (filed as a substrate failure, `fault_owner: harness` — the registrar process, not the citizens, failed) and the change is re-sealed and re-seeded for a re-run round.

**Honest limit, stated in the open:** for Pilot A the change's *identity* (the Door moves) is known to the programme's designers — it is printed in the spec's §6.2. The seal does not pretend otherwise. What it protects is everything a verdict could be retrofitted on: the exact new site, the exact distance, the seeding timestamp relative to reflection closing, and the register text. And by excluding §6.2 from Tier L's inputs, it keeps the calibration measuring *register-reading discipline* (§6.3's stated target), not prior knowledge. From Pilot B onward, the sealed file is also the *only* place the change is specified, and this ceremony is already the right shape for that.

### Cheapest verification it is live

Before the Round 1 drop: the manifest contains a 64-hex digest + writer + timestamp, and the holder returns a one-line receipt — its own `sha256sum` of the held file — matching the manifest digest digit-for-digit. That comparison is the pre-drop checklist item; it costs one command on each side and no plaintext crosses.

---

## Adoption 3 — The blind curator beat test (survey A.12/D.7; E.1 singleton "Was the judge blind?")

### Where this belongs — and why it is not in the game spec

Filed here, on the **curator/twin side**, deliberately *not* as a section of the syndicate-of-four spec. Three reasons. (1) The curator is a league-wide asset, older than the Syndicate programme: it films and ranks beats for Cody/Vega/Geist today and for syndicates tomorrow; a bias in it is a property of the curator, not of Pilot A, and a calibration buried in one pilot's spec would be run once and orphaned. (2) Pilot A's round record is evidence; contaminating it with a curator experiment would blur the spec's substrate-vs-script separation — the curator is part of the *spectator* surface (§7.3 of the spec), never a scoring store. (3) The twin-fidelity loop's governance (seeded-defect proofs, judges advisory never the gate) is the curator's natural home doctrine; this test is that doctrine applied to beat selection. The spec therefore receives only a pointer annotation (its §7.3 spectator paragraph is where a reader needs it), and the governing text is this section.

### The test

Modelled on Mogswamp's blind judging (A.12/D.7): a professional judge, blind to provenance, whose verdicts — delivered *before* the reveal — picked the human build in every round on evidence articulated while blind. The curator gets the same discipline as a standing calibration.

**Cadence.** Run (a) before any Pilot A reel is used as evidence or shown as the round's record, (b) after any change to the curator's scoring weights or moment taxonomy (Thor `~/curator/BUILD-LOG.md` versions it), and (c) otherwise once per **500 kept moments** or once a month, whichever comes first. It is cheap by design (below) so the cadence survives contact with a busy programme.

**Sample.** **20 clips** per test, drawn by the manager seat (not the curator) from the most recent manifest: 10 kept moments spanning the curator's top and middle score bands, 5 kept moments from its lowest kept band, and 5 *rejected* windows that scored just below the keep threshold — the near-misses are where bias hides. Each clip is copied to an anonymised test directory under a random ID (`b01`–`b20`): the manifest line's `citizen`, `event_citizen`, `on_screen`, `type`, `score`, and `reason` are stripped; filenames carry no citizen, date, or segment number. **Leakage check (mandatory, filed with the test):** if a clip's *content* visibly names its citizen (an on-screen nameplate, a chat line naming the actor), the clip is flagged `identity-visible` and reported separately — a blind test that isn't blind is the preview-that-lied failure (C.3) wearing a lab coat.

**Procedure.** The curator's scoring pipeline ranks the 20 anonymised clips using footage + digest events only (its normal inputs minus the stripped labels). Two comparisons are then computed and filed:
1. **Blind vs labelled:** Spearman rank correlation between the blind ranking and the curator's own original (labelled) ranking of the same 20.
2. **Blind vs human spot-check:** a human (Casey, or Magnus — the twin loop's cold-test residents) ranks the **top 5 blind picks** cold, without being told which citizens or moments they are; agreement is counted on those five.

Both rankings, the strip manifest (kept sealed until scoring, Adoption 2's pattern in miniature), and the two comparisons are filed to `~/curator/blind-tests/<date>.json` on the Thor, with a prose summary appended to `~/curator/BUILD-LOG.md`.

**Divergence triggers — pre-registered, any one fires:**
- blind-vs-labelled Spearman **ρ < 0.6** (the curator's ranking is substantially a function of its labels, not the footage); **or**
- **favourite capture:** ≥4 of the blind top 5 belong to a single citizen or a single moment *type* that constitutes <40% of the 20-clip pool (the curator only loves its favourites); **or**
- the human spot-check **disagrees on ≥3 of the top 5** (would not have kept them).

On any trigger: the curator's scores are **frozen to advisor-only** (reels may still be assembled, but no reel or ranking is cited as evidence in any round record or study) until a recalibration entry in the BUILD-LOG names what changed and a re-test passes. No trigger fired = the test files a clean calibration line and the curator's rankings keep their current standing. Either outcome is a filed result, per the doctrine that a calibration you only hear about when it fails is not a calibration.

**Why this test, in the fleet's own evidence:** the ProArt observer cut (`proart-jepa-observer-cut-20261108.md`) is the standing warning. There, embeddings separated Geist from Vega decisively *within* a camera state (0.74–0.87) — and the same battery's placebo (separating eras of one citizen) scored as high, with cross-shot transfer at chance: the apparatus was measuring **place and camera allocation**, not the citizen. The curator has the identical structural exposure: the cameraman frames whom it frames (curator v1's named deficit), the curator then "prefers" the citizens and beat-types it has the most footage of, and the preference reads as taste. A curator that only loves its favourites *is* the apparatus measuring itself. The blind test is the placebo arm for the curator, run on the curator's own rankings — the only form in which the confound can be caught before it is published as judgement.

### Cheapest verification it is live

The test directory exists and self-certifies: `grep -ril "marigold\|cody\|vega\|geist\|cobalt\|ochre\|vermilion" ~/curator/blind-tests/<date>/clips/` returns nothing for the anonymised copies (labels stripped in fact, not in intention), and `<date>.json` carries both comparison numbers and the trigger verdict. One grep + one file read; both are the pre-Pilot A spectator check.

---

## Adoption 4 — The comm-cost measure (survey B.2/E.1 Q11; MindCollab's −15%)

### What

MineCollab's measurement (B.2) is the survey's most decision-relevant number for a coordination game: **the primary bottleneck in multi-agent collaboration is natural-language communication efficiency — performance drops up to ~15% when agents must communicate detailed plans.** The spec rations communication by *budget* (the governor identities, §1.4; the consult cap, §2.4) but measures nothing about communication *volume*: Tier L cannot currently see what coordination cost, so it cannot charge a playbook for it — a verbose play and a terse play look identical in the evidence pack if both fire. This adoption makes comm cost a measured, filed quantity in every Pilot A round.

### The counters (per syndicate, per round — Pilot A has one syndicate; the shape is per-syndicate so Pilot B's 4v4 inherits it)

All counters are computed over the round window (GM's published drop timestamp → horn timestamp) by the manager seat at Phase 3, from stores that already exist:

| # | Counter | Definition | Read from |
|---|---|---|---|
| 1 | `chat_msgs` | Count of in-round chat messages, total and per hat | The round's comms log — scratch-server equivalent of `commons/comms/chat.jsonl`, filtered `kind=="chat"`, cast senders only, window-bounded |
| 2 | `chat_calls` | Subset of (1) that are playbook quoted call strings (spec §3's COMMS rule) — the coordination *signal*, separated from narration noise | Same log, matched against the filed playbook version's quoted strings |
| 3 | `tierd_calls` / `tierd_tokens` / `tierd_mind_seconds` | Tier D's model spend: calls, total tokens, mind-seconds for identity `syndicate-captain` | Governor ledger `ledger/mind-calls.jsonl`, filtered `agent=="syndicate-captain"`, window-bounded — the ledger's `total_tokens` and `mind_seconds` fields, summed, nothing estimated |
| 4 | `body_tokens` / `body_mind_seconds` | The four bodies' combined model spend (identities `syndicate-mari/cob/och/verm`) | Same ledger, same filter pattern |
| 5 | `consult_filed` / `consult_answered` | Consults filed and answered in-round, by book | `commons/consults/glm.jsonl` + `minimax.jsonl`, window-bounded, citizen = the captain body; answered lines carry the `provenance` the spec §2.4 already requires |
| 6 | `comm_tokens_total` | (3) tokens + (4) tokens + consult question+answer tokens (counted from the consult lines' text, labelled as the one *estimated* counter in the table) | Derived; the derivation is filed with the number |
| 7 | `comm_per_coverage_point` | `comm_tokens_total` ÷ final census coverage % (§4 of the spec) — what a point of Door cost in talk | Derived from (6) + the Spike 2 census output |
| 8 | `msgs_per_play_fired` | `chat_msgs` ÷ plays fired (firing log) — the verbosity of the book as run | Derived from (1) + the firing log |

### Where it lands

- **The round manifest** gains a `## Comm cost` table with the eight counters, per round, beside the governor-receipts section — so Round 1 vs Round 2 (and any re-run) are comparable at a glance.
- **Tier L's evidence pack** (spec §5.1) gains the comm-cost table as part of item 4 (round receipts). Tier L's reflection note must then **charge the playbook explicitly**: it names the round's most expensive play by comm share (counters 1–3 apportioned by the firing log's play windows — apportionment method filed with the numbers, since exact per-play attribution of shared Tier D cycles is approximate and must say so), and applies this rule, labelled PROPOSAL as the spec labels its starting values: *a play that consumed >25% of `comm_tokens_total` and failed is a first candidate for simplification or cutting in the next version — before any play that failed cheaply.* A play may still be kept, but the reflection must say why in receipt of its cost. That is MindCollab's finding turned into a budget line: the playbook is charged for the talk it causes.
- **The triples** (§5.3): each play's triple gains the play's comm share in its situation block, so the library accumulates cost beside outcome and a future retrieval can prefer the cheaper of two plays that both worked.

### Cheapest verification it is live

One independent recount at Phase 3: a second seat (or Muse) re-sums `mind-calls.jsonl` for the five syndicate identities over the round window and re-counts the comms log; the manifest's counters 1, 3, 4, 5 must match the recount exactly (they are sums and counts of filed lines, not measurements with error bars). A mismatch is a manifest defect, filed as such (`fault_owner: harness`), and the reflection may not proceed on unrecounted numbers.

---

## What changes where — summary for the builders

| Adoption | Artefact changed | Change | Gate it joins |
|---|---|---|---|
| 1. Fault owner | Thor `~/game-master/receipt-log.md` (template in `game_master.py`) | `**Fault owner:**` line on every nudge/incident receipt from adoption forward | GM receipt grep-pair check |
| 1. Fault owner | Spec §6.1 `registrar.jsonl` | `fault_owner` + `fault_owner_evidence` on `incident`/`nudge` entries | Pre-drop checklist (annotation) |
| 1. Fault owner | Spec §7 round record + §7.7 verdicts; league triples | Incident log table; owner on failed criteria; owner in failure triples; two-level reconciliation with the existing failure class/column | Phase 3 assembly check |
| 2. Sealed Tier-W | Round manifest (new sealed-change block); holder file on the Oracle; register entry format for sealed changes | sha256 filed before Round 1; plaintext held off-Thor by a different seat; revealed at Round 2 scoring; §6.2 excluded from Tier L Round 2 inputs | Pre-drop checklist (annotation): no hash, no drop |
| 3. Blind beat test | Thor `~/curator/` (`blind-tests/`, BUILD-LOG) — *not* the game spec | 20-clip anonymised ranking test; ρ + favourite-capture + human spot-check triggers; advisor-only freeze on trigger | Pre-Pilot A spectator check |
| 4. Comm cost | Round manifest (`## Comm cost`); Tier L evidence pack; play triples | Eight counters from governor ledger + comms + consult stores; reflection must charge the playbook | Phase 3 independent recount |

Nothing in this amendment reopens the spec's settled questions, changes a budget, a criterion, or a play, or authorises live play. It wires four questions the field's critics taught us to ask — *whose fault, was it sealed, was the judge blind, what did the talk cost* — into the fields, ceremonies, and counters that make the answers unavoidable.

*End of amendment. Filed on the studies shelf; home room: the-league-and-civilization. Siblings: `minecraft-agent-videos-survey-20261108.md` (source), `syndicate-of-four-spec-20261108.md` (build authority, annotated to point here), `sitka-twin-fidelity-loop-20261108.md` (the curator/twin side's parent design).*
