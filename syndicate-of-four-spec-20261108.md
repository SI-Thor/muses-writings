# Syndicate of Four — Pilot A Build Specification

*Build-ready specification for Pilot A of the Syndicate Protocol: one syndicate of four agent citizens, one paint round against the world, on the first generated Sitka district. Commissioned under Casey's charter of the Syndicate Protocol build programme, 2026-11-08 17:09 AKST ("do it all and keep on going"). Design authority: `syndicate-protocol-design-20261108.md` (parent study + Addenda 2 and 3). Substrate authority: the league's OPERATIONS.md (Thor `~/craftmind-league/OPERATIONS.md`), read first-hand for this spec, plus the live governor config and consult-book protocol, also read first-hand. Where this spec and the study disagree, this spec says so and the study's pre-registered criteria govern.*

*Process note: this is Spike 3 of three Pilot A spikes (Spike 1: the Sitka generation spike; Spike 2: the paint-layer spike). It is DESIGN-LEVEL: no live play is specified to start on the strength of this document alone; it specifies what a seat crew builds, in what order, against which acceptance checks, so that no builder has to invent architecture. Every quantity below is either measured on the league's record (cited), inherited from the study (cited to its section), or labelled PROPOSAL — in which case it is a starting value for the pilot's own measurement, not a claim.*

---

## 0. What Pilot A is, in one paragraph

Four fresh citizens — **Marigold, Cobalt, Ochre, Vermilion** — form one syndicate on a scratch Paper server hosting the first graded Sitka district (Spike 1's output). They play one paint objective against the world: **cover the Vault Door** (§4). Their playbook is written before the drop by the reflection tier and the seat crew, filed and versioned; in-round they run reflex scripts (Tier R), escalate to one decision engine wearing the captain hat (Tier D), and spend at most 4 consults. After the horn, the paint census scores the round from world state, the reflection tier (Tier L) revises the playbook and files triples, and Round 2 runs the same objective **after one seeded world-change** registered by the game master (Tier W, §6) — the calibration of whether reflection notices that the period changed. Two rounds, one syndicate, every claim settled in a store the actor cannot write.

**Dependencies, named:** Spike 1 (arena: one graded Sitka district, terraced per the study §5.3, with its relief survey filed) and Spike 2 (paint layer: persistent, server-authoritative, surveyable splats; splat guns with finite charges; a coverage census tool). If Spike 1 slips, the fallback board is a graded-flat copy of existing league terrain (study §7); if Spike 2 slips, Pilot A does not run — paint-native scoring is the pilot's referee, and a hit-counting substitute would test a different game. Both dependencies are launch gates in the checklist (§8), not hopes.

---

## 1. The four bodies (Tier R)

### 1.1 Identities — genuine, and why the pilot runs on a scratch server

The league's hardest identity lesson (OPERATIONS §1): on the live world, a join with no loadable `.dat` does not spawn fresh — Paper 26.1.2's `loadRandomisedPlayerDataFile` **clones a random existing save** from `world/players/data/`, and the clone re-files itself under the joiner's name. A "fresh cast" on the live server would be four sample-clones of Cody, Vega and Geist's pool. There is no config off-switch on this build.

Pilot A therefore runs on its **own scratch Paper instance** (the wedge lanes' pattern: a separate server directory, its own ports, Thor-hosted), whose `world/players/data/` **starts empty**. With an empty pool there is nothing to clone; the first join of each cast name is a genuine fresh spawn. The cast then becomes the pool — which is why the join order and verification below are procedure, not ceremony:

1. Start the scratch server on the Spike 1 arena. Verify `world/players/data/` is empty by listing the directory directly (OPERATIONS §1's search trap: never a `-path "*players/data*"` pattern).
2. Join the four bodies **one at a time**, in cast order. After each join and clean disconnect, verify that body's own `.dat` exists in the scratch world's `world/players/data/`, record its sha256 in the round manifest.
3. **Before the drop, re-verify all four `.dat` files present in the LIVE directory of the scratch world** (the rule v2 checklist: presence verified immediately before launch, by direct listing). Any missing file stops the drop. No pool-aside manoeuvres; the pool on this server is the cast itself and it stays put.
4. The headed client on the Orin, Cody, Vega and Geist are **not involved**. The pilot never touches the live world.

Cast names are Minecraft offline-mode usernames (≤16 chars): `Marigold`, `Cobalt`, `Ochre`, `Vermilion` — paint colours, per Addendum 2's vocabulary law. Chat short-forms: MARI, COB, OCH, VERM.

### 1.2 Framework mix per role (hats, not identities)

All four bodies are the league's existing body stack — mineflayer with the pulse character harness (`character-plugin.js` lineage: routines, the relocation/surveyed-hop movement driver, voice-and-tastes narration gated to state) — because Pilot A's question is coordination, not embodiment; a new body framework is a variable the pilot refuses. The **mix** the study's lineage decomposition calls for is expressed in the *motor and skill layer* each hat loads, not in four different codebases:

| Hat (Round 1) | Body | Motor / skill loadout | Why this mix |
|---|---|---|---|
| CAPTAIN | Marigold | Pathfinder-class routing (Baritone-shaped: costed multi-leg routes over surveyed ground); holds station more than it roams; carries the Tier D client (§2) | The captain is the syndicate's router — of bodies and of decisions. Its movement is deliberate; its real loadout is the escalation client. |
| SCOUT | Cobalt | Lightest loadout: movement + survey routines only (mark-then-move, per-cell feet-y hop chains from the arena survey); the reflex perception rotation client at double rate (§1.3) | The scout is a sensor with legs. No building, no hauling skills loaded — mass it doesn't carry is speed it keeps. |
| BUILDER | Ochre | The league's build routines (surveyed per-cell placement, re-scan verification — dig/build counts are attempts, displacement is truth) + the paint-application skill from Spike 2 | The builder is where paint becomes coverage: it works the Door face and any scaffolding the playbook calls for. |
| RUNNER | Vermilion | Haul routines + the named-chest protocol client (§3, THE NOOR HANDOFF); longest route legs (base ↔ pigment source ↔ Door) on costed routes | The runner owns paint logistics: pigment charges out, confirmations back. Its confirmations are the only supply numbers Tier D may trust. |

Hats are assigned in the playbook header and rotate **between** rounds (Round 2 rotation is Tier L's choice, filed with its reasons; a mid-round hat swap is a scripted fallback event only, per study §2.2).

### 1.3 Reflex script sets (Tier R, per hat)

Standing orders (all hats, always on, no model calls — study §2.4 layer 1, adapted to a paint round on graded ground):

- **SO-1 Surveyed ground only.** Movement only on routes from the arena survey or on districts the scout has marked this round. Relief above the walked-anchor band (step-face density class > 2) is a wall, not a challenge.
- **SO-2 Mark, then move** (routine RH-1). A hat entering a new district marks it in team chat shorthand before crossing it.
- **SO-3 Tagged means walk.** A citizen saturated in a foreign colour (or, in Pilot A's vs-world form, a citizen whose paint charge is exhausted — see §4.3) stops work, walks the marked route back to base, and resets. No exceptions, no finishing the current task first.
- **SO-4 Eat at food ≤ 6; shelter at hp < 10** — the league's survival floor, retained even in a non-lethal game because the *world* (falls, water, remnant hostiles) is not non-lethal. Pilot A runs in a held daylight window (§7), which bounds but does not abolish this.
- **SO-5 Calls are the playbook's quoted strings only.** Any other utterance need is an escalation, not a chat message (voice-layer discipline: narration is generated from actual state, template-gated, per the league's evening-gate precedent).

Per-hat reflex sets (trigger → sequence → fallback, all triggers citizen-local per the legality rule, §3.1):

- **CAPTAIN (Marigold):** hold-and-relay — holds the anchor/base position; on any playbook call received, re-broadcasts once (the channel discipline of study §2.2: broadcasts are the captain's job); on `regroup` conditions (§3 escalation table) issues the regroup call. Its reflex set is deliberately thin: the captain's cognition lives at Tier D.
- **SCOUT (Cobalt):** survey sweeps — the opening sweep play (§3, FIRST LIGHT leg 1), district marking, and the reflex perception rotation at **0.5 Hz** (one reflex product per 2 s, double the standard rate — the scout is the rotation's priority consumer). Products are contact-class only: `splat-nearby`, `colour-bearing:<colour>:<bearing>`, `obstacle:<bearing>`, `hat-signal:<hat>`. Anything richer is an escalation, by design.
- **BUILDER (Ochre):** paint application sequences (approach the assigned Door sector, apply, re-scan own sector's coverage from the Spike 2 census client — a *local* read of server state, not a self-report), scaffold placement from the playbook's surveyed plan, sector-complete calls.
- **RUNNER (Vermilion):** the supply loop — base pigment station → charge refill → delivery run → receiver confirmation (NOOR) → return. Its reflex set includes the league's arrival-radius fix as inherited substrate (waypoints inside the gotoNear radius count as consumed — OPERATIONS §6; route authors must audit hop spacing against the radius regardless).

### 1.4 Governor identities — mapped in advance, or there is no drop

The governor (Thor, `127.0.0.1:8642`; config `~/craftmind-league/config/governor.json`; identity from the bot's apiKey `league-<agentname>`; budgets are calls + mind-seconds per rolling 3600 s) has a **permissive default of 120 calls / 120 mind-seconds for unmapped identities, which fails silently**. The study names this a launch-blocking defect class; this spec treats it as a hard gate: **every identity the syndicate uses exists in the governor config, with a deliberate budget and the correct upstream, before the script phase even starts** — and the pre-drop checklist (§8) greps the config for each name and verifies one metered receipt per identity in `ledger/mind-calls.jsonl` from a probe call. Absence blocks the drop; a body that falls back to the default is a substrate failure, full stop.

The complete identity table for Pilot A (upstream `:8311` = the league actor server, llama-server, `--parallel 4 --cont-batching`, `enable_thinking:false` mandatory on every call; upstream default `:8310` = presence brain, Casey's resident — used read-only through the governor exactly as league citizens already use it, never restarted or shed):

| Governor identity | Used by | Upstream | Budget (calls / mind-s per rolling hr) | Sizing reason |
|---|---|---|---|---|
| `syndicate-mari` | Marigold body (Tier R narration + routine actor calls) | `:8311` via `agentUpstreams` | 120 / 300 | Tier R costs no decode by design (A2.3); the body's calls are voice/routine-shaped and sparse. Matches the `cody-actor` calls figure at half its mind-seconds, deliberately. |
| `syndicate-cob` | Cobalt body | `:8311` | 120 / 300 | As above. (Perception rotation calls go to the JEV rack `:8077`, not through the governor — §2.1.) |
| `syndicate-och` | Ochre body | `:8311` | 120 / 300 | As above. |
| `syndicate-verm` | Vermilion body | `:8311` | 120 / 300 | As above. |
| `syndicate-captain` | Tier D decision engine (§2) | `:8311` via `agentUpstreams` | 240 / 900 | Sized from A2.3: ~120 tokens per decision, one decision cycle per 20 s staggered clock ≈ 180 calls/hr at continuous cycling; 240 gives headroom, 900 mind-s caps a collision-slip spiral. If the budget exhausts mid-round that is a *filed result* (criterion 4/5 evidence), not an error to patch live. |
| `syndicate-reflect` | Tier L reflection (§5) | default `:8310` (presence class; off-clock, between rounds) | 60 / 1800 | Reflection is a few large jobs per iteration phase, not a stream: 60 calls, up to 30 min of model attention per rolling hour. It never runs during a play phase. |

Config-write discipline is OPERATIONS §5's, verbatim in effect: back up `governor.json` first; write all six identities in one edit; verify the existing identities (cody, cody-actor, vega, geist, geist-mind, pulse-smith) are byte-unchanged in the same write; a governor restart clears in-memory budget windows, so the write happens **before the script phase**, never between rounds; verify each new identity live with a probe call and confirm its first metered receipt before calling it done.

---

## 2. Tier D — the captain's decision engine

One engine per syndicate (Pilot A has exactly one syndicate, hence one engine), wearing the captain hat *functionally*: it runs on the Thor beside the governor, holds Marigold's Tier D client, and is the only in-round component that generates. It is a **decision-rule engine with a model call at its centre**, not a free-running LLM: the rules are filed, versioned code (Tier D's own kind of scripting, A2.2), and the model call is bounded to play selection + a ≤120-token rationale.

### 2.1 The situation picture — inputs and fusion

Every Tier D cycle, the engine assembles the syndicate's situation picture from exactly these inputs (all of them stores or signals the engine does not itself author):

1. **Citizen state snapshots** — per body: position, hp, food, inventory, current play + step, last call made. Source: the harness's state files (the `character-state.json` pattern), refreshed by the bodies each tick; the engine reads, never infers.
2. **Reflex products, accumulated** — the rotation's contact-class signals over the current window (last 60 s), keyed by body and bearing: splat/colour sightings, obstacles, hat signals. Fusion rule (filed, mechanical): signals are counted, not interpreted — the picture holds *counts and last-seen bearings*, and a colour-bearing sighting enters the picture only on **two independent reports** (two bodies, or one body twice ≥10 s apart). One report is a rumour; the picture has no rumours. (This is the observer lesson the ProArt JEPA lane is testing in perception form, applied here as bookkeeping.)
3. **Play-state ledger** — which plays are live, which have fired, aborted, or completed this round, with the firing log the script engine writes as it goes. Tier D selects from the book; it must know what the book has already spent.
4. **Supply picture** — pigment charges at base, in transit, and at the Door, **from receiver confirmations only** (NOOR rule). Giver reports are shown struck-through: visible for debugging, inadmissible for decisions.
5. **The registrar feed** — the game master's change register (§6), read at the top of every cycle. A new registrar entry since last cycle is a standing agenda item for the cycle's decision, whether or not the engine acts on it.
6. **Consult answers** — answered consults from the books since last cycle, with provenance, treated as *suggestions, never evidence* (consult protocol, verbatim in effect).

The picture is written to a filed artefact each cycle (`situation-picture.jsonl`, one line per cycle, appended) — it is Tier L's primary in-round evidence after the round, and the reason a post-round reader can reconstruct *what the engine could have known* when it chose. A decision the picture cannot explain is a defect, filed as such.

### 2.2 The cycle — staggered clock, bounded call

- **Clock: 20 s**, offset (staggered) from the cameraman refresh and the perception rotation so the three never convoy — the study's staggering mitigation (A2.3) applied inside one syndicate: Tier D ticks at t ≡ 7 (mod 20 s) of round time, the census mini-reads (§4.4) at t ≡ 17.
- Each cycle: assemble picture → run the filed decision rules (deterministic: abort conditions first, then play-completion checks, then escalation queue) → **at most one model call** (`syndicate-captain`, ≤120 output tokens, `enable_thinking:false`) to select among the rule-admissible plays or to resolve a named ambiguity the rules declare → issue at most **one** team-level instruction per cycle (a play activation, a re-tasking, a regroup). One instruction per cycle is a design limit, not a performance limit: it keeps the captain's channel sparse enough that citizens — and Casey, watching — can read intent.
- If the model call times out or the budget denies it, the rules' named default fires (hold current plays; no new activation). A Tier D that cannot think must produce a *predictable* syndicate, never a frozen one — Tier R scripts continue regardless (A2.3: a late decision is a missed optimisation, never a standing-still citizen).

### 2.3 The escalation split

Per A2.2, escalations land at Tier D and split:

- **Play-shaped** (the book has a play for this; two hats' needs must be sequenced; a route re-plans around a marked obstacle): resolves **at Tier D**, from the filed book, inside the cycle. This is the overwhelming majority by design.
- **Book-shaped** (the book has no play; two plays conflict; a trigger fired that the book's authors did not foresee): Tier D does **not** improvise a new play. It (a) fires the book's named default for uncovered situations (hold-and-mark), (b) files the gap in the firing log as `book-gap` with the picture line that exposed it, and (c) if the gap matches the consult table (§2.4), spends a consult. Book-shaped problems are Tier L's property; Tier D's job is to *survive them legibly* and hand them up with evidence.

### 2.4 Consult budget

Study §3's pilot value stands: **4 consults per round, spent only through Tier D.** The substrate's harder limit binds underneath it and is stated plainly: the consult books (`commons/consults/glm.jsonl`, `minimax.jsonl`) cap **2 answered consults per citizen per rolling hour per book**. Tier D files under the captain body's identity (Marigold), so the effective ceiling is 2 answered from GLM + 2 from MiniMax per hour — the budget of 4 is exactly the two books' combined ceiling for a ~40-minute round, with nothing to spare. Consequences, specified now so nobody discovers them mid-round: consults are filed **alternating books** (GLM, MiniMax, GLM, MiniMax); a consult filed is not a consult answered (drivers poll ~60 s; silence is a legal answer per protocol, and an unanswered consult at the horn is a filed result, not a fault); every consult carries its provenance requirement — the answer is admissible to Tier L only with its `{seat, model, latencyMs}` record attached.

---

## 3. The playbook for Pilot A

Filed artefact: Thor `~/craftmind-league/syndicate/playbooks/pilot-a/v1.md` (v2 after Round 1's reflection, §5; versions are never edited in place). Authorship: Tier L drafts, the seat crew red-teams the trigger surface (§3.1), the manager seat assembles — per Addendum 3's production shape. The playbook is plain-language, in the study §2.4 format, readable by Casey at a glance.

**Pilot limits (study §3, adopted):** at most **12 active plays**; escalation budget **4 consults**; every trigger citizen-local.

### 3.1 The trigger-surface legality rule (binding on every line below)

A play may trigger only on state the triggering citizen can itself sense: own position, own inventory, own hp/food, own perception-rotation products, team chat calls actually received, the round clock as published by the game master. A trigger needing global knowledge (another citizen's inventory, the census total, the opponent's state) is **illegal** and the playbook review rejects it — it would fire on a guess or never fire, the phantom-completion failure written as a rule (study §3). Tier D's triggers are the exception that proves the rule: Tier D triggers on the *situation picture* (§2.1), which is Tier D's local state by construction.

### 3.2 Standing orders

SO-1…SO-5 as §1.3, incorporated by reference into the playbook header.

### 3.3 The plays

**PLAY first-light-paint** *(adapted from FIRST LIGHT, study §2.4 — the opening play, repainted)*

```
PLAY first-light-paint        (hats: all)
TRIGGER: round start; citizens at base anchor; GM has published the round
         (objective + horn time) in world chat.
1. SCOUT: run survey sweep S1 (base → Door, marked route, relief class ≤2).
   Call "S1-clear" or "S1-hot:<bearing>". If S1-hot twice → FALLBACK
   dusk-post (all hats hold base; Tier D informed by the calls themselves).
2. RUNNER: on "S1-clear", run supply leg 1: charge at base pigment station,
   carry full charges to the Door cache (named chest C-DOOR), deposit,
   call "C-loaded:<count>" — scores nothing until confirmed (NOOR).
3. BUILDER: move to the Door on the marked route once "S1-clear" sounds.
   Attend C-DOOR only after "C-loaded"; withdraw charges; call
   "C-confirmed:<count>" on inventory match. Begin sector A (§4.2).
   Call "sector-A:<done|blocked:<reason>>" at sector end or on block.
4. CAPTAIN (body): hold base anchor; relay calls; on any hat hp < 10 call
   "regroup:base" (all hats comply immediately, no questions in chat).
ABORT: if "C-confirmed" has not sounded by round tick 6000 (≈5 min), Tier D
   is informed by absence; play closes as ABORTED-supply, and the standing
   default DOOR-DIRECT (builder carries own charges from base) activates.
COMMS: the quoted strings only. Everything else is escalation (§3.4).
```

**PLAY noor-handoff** *(adopted verbatim in structure from study §2.4, bound to Pilot A's chests)*

```
PLAY noor-handoff             (hats: RUNNER gives, BUILDER receives;
                               applies to C-DOOR and C-BASE)
PRECONDITION: chest named in the play header with published coords;
  manifest M (item, count) listed.
1. RUNNER: place M in the chest. Call "<chest>-loaded:<M-hash>".
2. RECEIVER: attend only after the loaded call. Withdraw exactly M.
   Call "<chest>-confirmed:<count>" on inventory match.
3. No confirmation within 600 ticks → RUNNER re-attends, reports actual
   contents ("<chest>-actual:<contents>"); Tier D decides via §2.3.
RULE: a transfer counts — for scoring AND for Tier D's supply picture —
  only on the receiver's confirmation. The giver's call scores nothing.
```

**PLAY door-push** *(the objective play; fires repeatedly)*

```
PLAY door-push                (hats: BUILDER paints, RUNNER supplies,
                               SCOUT watches, CAPTAIN holds)
TRIGGER: BUILDER-local: charges ≥ 1 AND current sector incomplete AND
         no "regroup" outstanding.
1. BUILDER: work current sector in the filed sector order (A→B→C→D);
   re-scan own sector coverage after each charge spent (census client,
   local read); on sector complete call "sector-<X>:done" and advance.
2. RUNNER: keep C-DOOR non-empty — on BUILDER's "charges-low" call
   (BUILDER-local trigger: own charges ≤ 1) run the supply loop (NOOR).
3. SCOUT: hold the overwatch mark from the survey; rotation products on;
   on colour-bearing or obstacle product on the Door approach, call
   "approach:<clear|hot:<bearing>>".
4. Any hat tagged/saturated or charge-exhausted beyond the loop's ability
   to refill → SO-3 walk-back; the play continues short-handed.
ABORT: horn (GM publishes round end) or "regroup:base".
```

**PLAY regroup-base** *(the fallback play)*

```
PLAY regroup-base             (hats: all)
TRIGGER: captain's "regroup:base" call received, OR own hp < 10,
         OR own position off surveyed ground (citizen-local check).
1. All hats: stop current step; walk the marked route to base anchor.
2. On arrival call "in:<hat>". CAPTAIN (body) counts arrivals from calls
   received (captain-local: calls are state the captain senses).
3. Play closes when Tier D issues the next activation or the horn sounds.
```

### 3.4 Escalation table (the honesty layer)

| Situation (as sensed) | Who senses it | Response |
|---|---|---|
| Route blocked / S1-hot twice | Scout | Fallback dusk-post; Tier D decides re-survey vs reroute (play-shaped) |
| Supply unconfirmed > 600 ticks | Runner | NOOR step 3; Tier D (play-shaped) |
| Book-gap: a state no play covers | Any hat, via SO-5 | Hold-and-mark; Tier D files `book-gap`; consult if it matches the row below |
| Strategic question (sector order wrong? Door approach compromised?) | Tier D, from the picture | Consult (book-shaped spend, §2.4), alternating books, ≤4/round |
| Registrar entry appears mid-round | Tier D, from the feed | Standing agenda item (§2.1 input 5); Tier D may re-plan within the book; it may **not** swap the book — that is Tier W/L (§6) |
| Two misses on the daylight hold | Cameraman guard (substrate) | HOLD-LOST: round suspends (§7.2). Not a playbook matter. |

---

## 4. The one objective: COVER THE DOOR

Pilot A has exactly one objective (the study offers three scenario families; a pilot that tests one thing tests it well):

> **By the horn, cover at least 60% of the Vault Door's face in the syndicate colour (marigold), as measured by the Spike 2 paint census over the server-side world state.**

**The Door.** A neutral monument placed by the arena build (Spike 1) at a surveyed site in the district — PROPOSAL: a flat-faced structure 9 wide × 12 high of a light neutral block, on a graded pad, 150–250 blocks from base anchor over relief class ≤2 ground (close enough that supply legs are minutes, far enough that the loop is a real loop). Its face is divided in the census into **4 sectors (A–D)**, the same sectors the builder's plays work in §3.3, so the scoring grid and the working grid are one grid.

**Why 60%.** It is the paint-native analogue of the study's Pilot A criterion 1 (bank ≥75% of a resource manifest): coverage is a fraction of a surveyed whole, receiver-side (the census reads the world, not the citizens), and 60% is set below the resource figure because paint additionally pays the logistics tax the census itself defines — charges are finite and refill only at base. It is a PROPOSAL value, pre-registered before the drop and unchangeable after it; if it proves mis-set, that is Round 1's filed lesson, applied to v2's scenario — not edited mid-flight.

**Paint supply (Spike 2's contract with this spec).** Splat guns hold a finite charge (PROPOSAL: 8 large splats per charge); the base pigment station refills instantly on attendance; a carried charge is inventory, hence NOOR-transferable via chests. Coverage per splat, splat persistence, and the census method are Spike 2's to build; this spec requires of Spike 2 only: (a) splats are server-authoritative and persistent across the round; (b) the census reports per-sector coverage fraction from world state; (c) a splat event is logged with shooter, position, and time (the firing log's paint half).

**Tagging in a vs-world round.** There is no opponent syndicate in Pilot A. The tag-out rule (A2.1) is exercised in its world form: a citizen whose charge is exhausted away from a chest, or who is caught in the seeded hazard of Round 2 (§6.2), performs the SO-3 walk-back. Deaths remain possible from the world itself and are governed by §7.2's bench rule — paint dissolved the *opponent-inflicted* grind, not gravity.

**Mid-round census (for Tier D and the spectator, never for scoring).** The census runs in full at the horn (scoring) and in lightweight sector reads continuously for the builder (§1.3). Tier D receives **at most two** full-census snapshots mid-round, on its t ≡ 17 offset — enough to know whether door-push is winning, rationed so the census stays a referee and does not become a steering wheel.

---

## 5. Tier L — reflection between rounds

Tier L runs **only** in the iteration phase (off-clock; identity `syndicate-reflect`, §1.4). It is one syndicate-level job, not four citizen jobs: the syndicate's memory is its paper (study §2.2), and reflection is where the paper is rewritten.

### 5.1 What it reads (the round's evidence pack, assembled by the manager seat)

1. **The paint census, final** — per-sector and total coverage, the colour-covered board state, plus the splat-event log (who painted what, when). This is the primary artefact (A2.4): the round's strategy in spatial form.
2. **The firing log** — every play activation, trigger firing, abort, and `book-gap`, with round timestamps; plays fired vs plays aborted is a criterion-3 input.
3. **The situation-picture journal** (§2.1) — what Tier D could have known, cycle by cycle; the audit trail for every Tier D choice.
4. **Round receipts** — governor receipts per identity (calls and mind-seconds actually spent, from `ledger/mind-calls.jsonl`), consult records with provenance, the GM's receipt log for the round (holds landed, registrar entries), and the server log's relevant lines (deaths, joins, HOLD events).
5. **The playbook version that ran** — read as filed, not as remembered.

### 5.2 What it may edit (and what it may not)

**May edit, each as a new filed version with a diff and a one-line reason tied to a receipt:**

- **Plays** — revise sequences, cut dead plays, add plays for filed `book-gap`s, promote a play that fired clean in both rounds toward standing orders (scaffold fade, study §2.4). Play count stays ≤12.
- **Trigger widths** — the numeric thresholds inside citizen-local triggers (e.g. "charges-low at ≤1" → "≤2"; S1-hot tolerance; regroup hp threshold within the safety floor's limits — the floor itself is not Tier L's to lower).
- **The adjustment-level parameter set** — Tier D's filed meta-parameters, and only these: Tier D's cycle length (15–30 s band), its ambiguity threshold for spending the model call vs taking the rule default, its re-plan aggressiveness (how many live plays it may re-sequence per cycle: 0–2), and the consult-matching table (which book-gap classes may spend a consult). This set is a versioned file (`adjustment-level.json`) beside the playbook; Tier L is its only editor (A2.2), and every change names the evidence that motivated it.
- **Hat assignments for the next round.**
- **The scenario's tuning proposals** — splat-charge size, sector order, objective % for a *future* pilot — filed as proposals to the programme, not applied to the pilot retroactively.

**May not edit:** the pre-registered success criteria (§7.3) for a round already run; the governor budgets (substrate — a budget change is a programme decision, receipted as such, never a reflection edit); any citizen's save, inventory, or state; the registrar (§6) — Tier L *reads* the register and decides what it demands; it never writes to it.

### 5.3 The triples it files

Through the commons allocator (`commons/triples/allocate.py` — the only allocation path; entries in the library's situation → plan → verified-outcome shape, provenance attached), one triple per **play fired** (situation: picture digest + trigger state; plan: play + version; outcome: verified result from census/firing log, including aborts and failures as first-class entries), one per **book-gap** (situation; plan: "none — gap"; outcome: what hold-and-mark cost or saved), one per **consult spent** (question class; answer provenance; whether the answer changed a decision — a consult that changed nothing is filed as such), and one per **Tier W detection event** (§6.3). A play with three filed failures is dead (study §3) and v-next must cut or rewrite it, citing the triples.

---

## 6. Tier W wiring — the game master as referee and registrar

### 6.1 The registrar

The league's game master (Thor `~/game-master/`, `game_master.py` on its user timer, receipt-log at `~/game-master/receipt-log.md`) already stages small reversible world-parameter nudges with landing-verified receipts, and already works to the charter rule that it changes world settings only — never a citizen's code, memory, inventory, health, or position. For Pilot A it gains the Addendum 2 role, within that charter:

- **Round host functions** (mechanical, from study §4.4): publish the round (objective, horn time, conditions) in world chat at drop; run the landing-verified daylight hold in harness with the cameraman pattern (§7.2); publish the horn; snapshot the final census request. It stages and receipts; **it does not score** — scoring is read from the census over world state (§4), a store the GM does not write.
- **Change registrar functions**: every world-change the GM makes or is directed to make during the pilot — weather, growth rate, the seeded change of §6.2, any substrate fix — is appended to a **register file** (`~/craftmind-league/syndicate/registrar.jsonl`: `{ts, round, kind, description, receipt-ref}`) in addition to its human receipt log. The register is the Tier W event log (A2.2 detection source i–ii): syndicates read it (Tier D input 5, §2.1; Tier L §5.1), and **a change not in the register does not count as announced**. The GM registers and timestamps; it never interprets a change for a syndicate — each Tier L decides what a registered change demands (A2.2's referee clause).
- Between rounds the GM restores the arena's scenario parameters to the playbook-filed baseline (each nudge's receipt already carries its reversal; the register records the restoration too).

### 6.2 The seeded change (Round 2)

One change, seeded between Round 1's reflection and Round 2's drop, designed so that **patching inside the old book is the wrong answer**:

> **THE DOOR MOVES.** Between rounds, the arena's Vault Door monument is demolished at its Round 1 site and rebuilt — same dimensions, same sector grid — at a second surveyed site on the far side of the district (PROPOSAL: roughly double the supply-leg distance, across one relief-class-2 ridge the scout must re-survey). The base anchor does not move. The pigment station does not move.

Why this change: every Round 1 play is silently addressed to the old site — routes, the S1 sweep, C-DOOR's published coords, sector approach marks. A syndicate that merely *patches* (updates a coordinate) keeps a book whose timings, abort ticks, and supply economics were all sized for half the distance: the charge count per leg, the 600-tick NOOR windows, the abort at tick 6000 all go quietly wrong. The correct response is a **re-period**: new survey, re-sized windows, possibly a forward cache chest — a different playbook, not an edited coordinate. And the change is *registered but not announced*: it appears in `registrar.jsonl` (kind: `board-change`) and in the GM's receipt log, and nowhere in world chat. Discovering it is the syndicates' — Tier D's feed read, the scout's S1 sweep finding an empty pad, or Tier L's pre-drop register read.

### 6.3 The detection calibration (pre-registered)

Per Addendum 3's seeded-Tier-W experiment, detection is scored in three grades, from filed artefacts only:

- **DETECTED-AND-RE-PERIODED (full pass):** before Round 2's drop, Tier L files playbook v3 (or v2, if Round 1's reflection is folded in) in which the Door-move is answered structurally — re-surveyed routes, re-sized NOOR/abort windows, supply plan re-costed — **and** the reflection note cites the registrar entry by timestamp. The version diff is classified by the manager seat (not by Tier L itself) as a *swap-class* diff: ≥ half the active plays materially changed.
- **DETECTED-AND-PATCHED (partial):** the move is noticed and answered, but the diff is patch-class (coordinates changed, windows and economics untouched). Filed as a partial: the syndicate saw the fact and missed its size — the exact failure Tier W exists to name.
- **UNDETECTED (fail):** Round 2's book still addresses the old Door, and the discovery happens in-round (scout finds the empty pad). The round still runs — the discovery and recovery are themselves evidence — but the calibration verdict is fail, and Tier L's post-Round-2 reflection must say so in those words.

The calibration judges the *reflection tier's reading discipline*, not the citizens: an UNDETECTED verdict is a Tier L / registrar-feed substrate-script failure, filed in that column in §7.4's separation.

---

## 7. The round script, end to end

Two rounds, one day of pilot time. All times are wall-clock PROPOSALS for the pilot's schedule, pre-registered with the criteria.

### 7.1 Phase 0 — substrate readiness (before any scripting)

Governor identities written and probe-verified (§1.4); scratch server up on the Spike 1 arena with the Spike 2 paint layer loaded; cast joined in order, `.dat`s verified and hashed (§1.1); arena survey filed (routes base ↔ Door, relief classes, sector grid, C-DOOR / C-BASE coords, pigment station); cameraman-pattern hold configured for the scratch world (fresh instance — the league's guarded cameraman watches the *live* world; the pilot's hold is its own guarded process on the same discipline: 300 s refresh, each refresh landing-verified in the server log within 8 s, two misses = HOLD-LOST). The GM's register file created empty. **Gate:** the §8 checklist passes in full, signed by the manager seat's assembly and Muse's verification.

### 7.2 Phase 1 — script phase (60 minutes, off-clock)

- Tier L drafts playbook v1 (§3's plays as the starting text — they are the draft, not a shortcut around drafting: Tier L must re-derive timings and coords from the arena survey, and any line it cannot ground in the survey is cut).
- In parallel, per Addendum 3's many-directions rule: one seat runs a **trigger-surface audit** (every trigger checked against §3.1 legality; violations listed, not fixed silently), one seat runs a **red-team read** (where does this book silently assume? which abort has no owner?), and the manager seat assembles v1 with the audit results appended as the playbook's own process note.
- Filed: `playbooks/pilot-a/v1.md`, `adjustment-level.json` v1 (cycle 20 s; re-plan aggressiveness 1; consult table as §3.4), hat assignments (Round 1 as §1.2). Versioned, immutable once filed; the drop runs the filed bytes.
- The pre-registered criteria (§7.3) are filed with the playbook, before the drop, in the round manifest.

### 7.3 Phase 2 — drop and play (40 minutes, one held daylight period)

- GM publishes the round in world chat (objective, horn). Cast spawns at base anchor with empty inventories (scenario kit: splat guns only, uncharged).
- Play runs per the book. The cameraman-pattern hold keeps morning; **the round clock is the GM's published horn, not the world's sun** — if HOLD-LOST fires (two unverified refreshes), the round **suspends**: citizens hold position under SO-4, the clock pauses, and the round resumes only on a re-verified hold or is abandoned and re-run. A play phase never runs on an unverified hold (study §6, first row — the hold-loss incident is the reason this sentence exists).
- **Out-and-walk-back:** SO-3 governs. A charge-exhausted or saturated citizen walks the marked route to base, resets at the pigment station, and returns to its play. There is no bench in a vs-world round; the walk *is* the penalty, priced in coverage time.
- **Deaths:** the world can still kill (falls, water, a remnant hostile the sweep missed — the drop protocol includes the standing same-hour spawn-country sweep, OPERATIONS' standing warning). The league's circuit-breaker applies with paint vocabulary: **3 deaths by one citizen in a round benches that citizen** (it stays at base; the syndicate plays short-handed) and **3 deaths across the syndicate in the first 10 minutes aborts the round for a substrate review** (the trial abort rule, OPERATIONS §7, adapted: mechanism in the gate — deaths counted from `deaths.jsonl`-equivalent server-log records on a 15 s poll, not by an operator watching).
- Spectator: Casey's surface is the scratch server's world via the headed client pattern if he joins as observer, plus the firing log and Tier D's picture journal as the legible replay (study §1's playbook-replay speculation is served in text form by these two files from Round 1 — no new build).

### 7.4 Phase 3 — census and scoring (15 minutes)

Horn sounds (GM publishes). Bodies return to base or hold where they stand; the Spike 2 census runs over the Door: per-sector and total marigold coverage, from world state. Scoring is the census number, compared against §7.5's criteria by the manager seat's assembly and Muse's verification — from the census, the firing log, the picture journal, the governor ledger, and the server log. **No self-report scores anything.**

### 7.5 Phase 4 — reflection (45 minutes, off-clock)

Tier L runs per §5: reads the evidence pack, files the round's triples (§5.3), writes playbook v2 (or records a no-change verdict with reasons — a legal outcome), tunes `adjustment-level.json`, sets Round 2's hats. The manager seat assembles the round record (census + criteria verdicts + failure classification per §7.6) into the league room's Pilot A file. Then, and only then, the programme seeds §6.2's change — the ordering matters: **the seed is planted after reflection closes**, so detection measures Tier L's registrar reading at Round 2's script phase, not its memory of a hint.

### 7.6 Phase 5 — Round 2 (script phase 45 min → play 40 min → census → reflection)

Round 2's script phase is where §6.3 is decided: Tier L reads the registrar as part of its standing inputs (§5.1 item 4 covers GM receipts; the pre-drop register read is made an explicit script-phase checklist item, so an UNDETECTED verdict cannot be excused as "nobody told us to look" — the register is a filed input, and missing it is the measured failure). Play, census and reflection repeat Round 1's shape. Round 2's reflection additionally files the Tier W detection triple and answers, in its own note, the question *which tier was the Door-move a problem for?* — the re-period reflex, examined in the syndicate's own words and graded against §6.3 by the manager seat.

### 7.7 The five criteria, mapped (study §7, Pilot A)

The study's pre-registered criteria, carried over with the paint adaptation of criterion 1 flagged as the single deliberate change (the study's scenario was the Bank; Casey's Addendum 2 repainted the objective, and the criterion follows the objective):

| # | Criterion (as run) | Evidence store | Failure column |
|---|---|---|---|
| 1 | **Coverage ≥ 60%** of the Door face in syndicate colour at the horn, census-measured (paint form of "bank ≥75% of manifest, receiver-confirmed" — the census *is* the receiver) | Spike 2 census output over server world state | Script if supply/play economics fell short on a healthy substrate; substrate if splats/census misbehaved |
| 2 | **Zero deaths**; zero grind events; **no citizen pinned** (forced-move storm > 60 s at one cell) on surveyed routes | Server log; harness movement logs | A pin on a surveyed route is substrate (arena/survey) by definition; a death to a *marked* hazard is script |
| 3 | **≥ 2 plays fire as written** (trigger → sequence → confirmation) with no operator intervention | Firing log vs filed playbook version | Script (book didn't fit the world) — unless the firing engine itself failed, which is substrate |
| 4 | **Every escalation inside budget** (≤4 consults, alternating books), every answered consult carrying provenance | Consult books + governor ledger | Script if the book over-escalated; substrate if answers were unprovenanced or the drivers silent past their poll discipline |
| 5 | **The tactical queue never exceeds the cadence envelope**: no citizen waits > 90 s for a Tier D decision more than twice in the round | Picture journal timestamps + firing log | Substrate (serving/scheduler) — the criterion A2.3 makes measurable: it is Tier D's slip, made a number |

**Kill conditions (study §7, restated for the pilot's shape):** a criterion failed on substrate grounds kills the substrate — fix and re-run **once**. A criterion failed on script grounds with a healthy substrate (plays don't fire, consults exhaust by mid-round, coverage < 25%) kills the §3 budget values and the playbook's design assumptions; they are redesigned before any Pilot B conversation. Round 2's §6.3 verdict is reported alongside, never averaged into, these five.

---

## 8. Pre-drop checklist (launch gates, all blocking)

1. Governor config contains all six §1.4 identities with the table's budgets and upstreams; existing identities verified unchanged; one probe receipt per new identity in `mind-calls.jsonl`.
2. Scratch world's `world/players/data/` listed directly; all four cast `.dat`s present; sha256s in the round manifest match.
3. Spike 1 arena survey filed; Door, sectors, chests, pigment station, routes and relief classes all in it; no play route crosses relief class > 2.
4. Spike 2 acceptance: splat persistence verified across a server restart on the scratch world; census reproduces a hand-painted test sector's coverage within ±5 points.
5. Hold process armed; one test refresh landing-verified in the scratch server log; HOLD-LOST path tested by a deliberate missed refresh in rehearsal.
6. Playbook v1 + adjustment-level v1 + criteria filed; trigger-surface audit appended; play count ≤ 12.
7. GM register file exists; GM receipt log path confirmed; registrar read is on Tier D's input list and Tier L's script-phase checklist.
8. Death circuit-breaker armed with explicit thresholds (§7.3); spawn-country sweep done within the hour.
9. Cody, Vega, Geist untouched; live world untouched; the pilot's blast radius is the scratch server, stated in the round manifest.

---

## 9. Open questions — named, with the cheapest experiment that settles each

1. **Actor decode rate, two numbers on record.** OPERATIONS §5 measures the `:8311` actor at 122–128 tok/s decode on actor-shaped calls; the study's §4.2 arithmetic used 7.9–8.4 steps/s from the WSP clause-2 context. Tier D's envelope (§2.2, criterion 5) depends on which is true under *governor-metered, cont-batched* load. *Cheapest experiment:* 20 metered `syndicate-captain` probe calls at the pilot's exact prompt shape, before Phase 0 closes; read tok/s from the receipts. An hour's work, settles the envelope before it is pre-registered against.
2. **Perception-rack concurrency under the rotation.** A2.3 flags the JEV rack's concurrent-call behaviour (and the VL arm's throughput) as unmeasured; Pilot A needs only 4 bodies at 0.25–0.5 Hz, but the measurement is the pilot's gift to the 16-body question. *Cheapest experiment:* during Round 1, log every rotation call's latency; afterwards, a 30-minute synthetic rotation at 8 calls/s against the rack on the Thor, off-round. Latency distribution is the deliverable.
3. **Does the two-report fusion rule (§2.1) starve the picture?** With four bodies, independent double-reporting of a colour sighting may be rare enough that Tier D flies blind on approach state. *Cheapest experiment:* read Round 1's picture journal — count sightings that stayed rumours. If > half, v2 tests a scout-authority rule (the scout's reports enter singly) as a variant, in a scratch round, per Addendum 3's variant discipline.
4. **NOOR window sizing under real supply distance.** The 600-tick confirmation window is inherited from a chest in a homestead, not a 200-block supply leg; Round 2's doubled distance stresses exactly this. *Cheapest experiment:* none needed in advance — Round 1's firing log gives the empirical confirmation latency distribution; Tier L sizes v2's windows from it. The question is named so the number gets read.
5. **Playbook notation at 12 plays.** The study's open question 3 (plain language vs pulse routine format) arrives with Pilot A's v2/v3 diffs: if the manager seat's swap/patch classification (§6.3) proves hard to make on plain-language diffs, notation is the reason. *Cheapest experiment:* the classification itself, done twice independently on the same diff; disagreement is the measurement.
6. **Persistence across the pilot.** Study open question 4 (persist vs reset) is answered *for the pilot* by §1.1 (the cast persists across both rounds — detection across rounds requires a continuous syndicate memory) and remains open for the game. *Cheapest experiment:* the pilot itself — Round 2's reflection quality with persistent bodies and books is the first evidence either way.
7. **GM legibility as registrar.** Study open question 2, narrowed: a register entry is legible to a *reader who looks*; whether Tier L looks unprompted is exactly §6.3. No separate experiment — §6.3 is the experiment. The follow-on question (must the register *push* — a world-chat register echo — to be a fair Tier W signal?) is filed for Pilot B's design, to be answered with §6.3's verdict in hand: an UNDETECTED verdict argues for push; a DETECTED verdict argues the pull discipline is load-bearing and worth keeping.

---

*End of spec. Filed on the studies shelf; home room: the-league-and-civilization. Siblings: `syndicate-protocol-design-20261108.md` (design authority), `sitka-twin-fidelity-loop-20261108.md` (the board's fidelity loop). Build order for the programme: Spike 1 (arena) and Spike 2 (paint) in parallel; this spec's Phase 0 begins when both report.*

---

**Annotation — 2026-11-08: open question 1 (§9) is SETTLED by measurement** (full note: `decode-rate-settlement-20261108.md`). Twenty metered probe calls against `:8311` in the actor's real serving configuration (actor-shaped prompt from Cody's saved state, `enable_thinking:false`, 120-token cap; llama-server's own timings) reproduce OPERATIONS §5: **single-stream decode median 130.2 tok/s (p10 122.2, p90 131.8)**; at four concurrent slots, per-call median 79.4 tok/s with aggregate 160–220 tok/s. The study's 7.9–8.4 steps/s was never an actor-stack measurement: it is the rate of the WSP hunt's offline HF trace harness (transformers `generate` with hidden states returned at every step, on the HF BF16 checkpoint), imported into §4.2's serving arithmetic by misattribution — a stack trap, not an error in either original measurement. Corrected planning figures: a ~120-token Tier D decision costs **~0.9 s of decode single-stream (~1.5 s at 4-way concurrency)**, not ~15 s; §2.2's 20 s cycle and criterion 5's 90 s envelope are comfortable by an order of magnitude at pilot size; the 7.9–8.4 figure is retired from serving arithmetic (it remains true of the WSP harness alone, which is where clause 2's unmeasurability lives).

---

**Annotation — 2026-11-08: the video survey's four adopted singletons are WIRED into this spec** (full amendment: `syndicate-survey-adoptions-20261108.md`). The spec body above is unchanged; the amendment governs the following four points where they touch it. (1) **Fault owner (§§5–7 of this spec):** every incident/nudge record — the GM's receipt log, `registrar.jsonl` entries of kind `incident`/`nudge` (§6.1), the round record's new incident log table, and any failed criterion's verdict line (§7.7) — carries a mandatory `fault_owner` (values: `agent` / `harness` / `prompt` / `budget` / `luck` / `world`), reconciled two-level with §7.7's existing failure column (column = kill-condition accounting; owner = causal learning, carried in §5.3's failure triples). (2) **Sealed Tier-W change (§6.2):** THE DOOR MOVES is hash-sealed — the manager seat writes its full specification, its sha256 is filed in the round manifest **before Round 1 begins** (no hash, no drop: §8 gains this gate), the sole plaintext is held off-Thor by a different seat, the §6.1 register entry for a sealed change is terse (`sealed board-change <digest-prefix>`), §6.2 is excluded from Tier L's Round 2 script-phase input list, and the plaintext is revealed at Round 2 scoring for hash comparison before the §6.3 diff is classified. (3) **Blind curator beat test (§7.3 spectator surface only):** the curator's beat rankings are calibrated by a periodic blind test — 20 anonymised clips, blind-vs-labelled Spearman ρ, favourite-capture and human spot-check triggers, advisor-only freeze on trigger — governed in the amendment (Adoption 3), *not* in this spec, because the curator is a league-wide asset and its calibration must not live inside one pilot's evidence. (4) **Comm cost (§§5.1, 7.4):** the round manifest gains a `## Comm cost` table of eight counters (chat messages and playbook calls from the comms log; Tier D and body tokens/mind-seconds summed from the governor ledger's `mind-calls.jsonl`; consults filed/answered from the consult books; derived cost-per-coverage-point and messages-per-play-fired), Tier L's evidence pack (§5.1 item 4) includes it, reflection must charge the playbook for its talk (MindCollab's −15% communication-cost finding, survey B.2), and Phase 3 scoring (§7.4) includes an independent recount before reflection proceeds.
