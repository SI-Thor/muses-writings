# Syndicate Protocol — The Last Mile, Rebuilt in Minecraft

*Design study, commissioned by Casey 2026-11-08 16:48 AKST: "What if we rebuilt our last mile project into Minecraft? … anywhere from four to 16 players and teams that are doing a syndicate-like game, all as agents, working in teams with communication and coordination, and scripts they are writing before the round starts that help them coordinate — and in the game they have to be more quick and on the fly."*

*Process note: this study was written against the league's own measured record — the triples library, OPERATIONS.md, and the shelf studies of 2026-11-07/08 — not against genre intuition. Every load-bearing claim below is either cited to that record or labelled SPECULATION. Where the record contradicts a natural design instinct, the record wins and the contradiction is stated.*

---

## 1. The game in one page

**Fantasy.** You are not playing a citizen. You are the *back room* of a syndicate: the crew that writes the playbook before the job, then watches four to sixteen embodied agents — Minecraft citizens with names, inventories, hunger and a death count — try to run it live against a world that does not care about the plan. The skill being tested is the fleet's own skill: how much of the thinking can be moved *before* the round, into scripts, protocols and conventions, so that the in-round mile — thin, fast, reflexive — is short enough to survive.

This is the Last Mile pattern wearing a game. In the fleet, the pattern is: deep work happens upstream (briefs, pre-registrations, standing doctrine), and the final execution mile is deliberately thin because everything decidable was decided earlier. Syndicate Protocol makes that pattern the explicit win condition. A team that scripts well wins with mediocre in-round reflexes; a team that scripts badly dies eloquently, in chat, at night.

**Round shape.** Five phases, deliberately echoing the Radio Hour game's phase structure (Work → Persona → Listening Round → Night → Iteration), because that structure already encodes the two-phase cognition this game is about:

1. **Script phase (the listening round).** Off-clock, minutes to hours. Each syndicate writes and revises its playbook: role assignments, formations, rendezvous points, handoff protocols, fallback triggers, comms shorthand. Scripts are *filed artefacts* — versioned, diffed between rounds, never edited mid-round. This is the deep-thinking phase; it is where the game is mostly won.
2. **Drop.** Citizens spawn at their syndicate's surveyed anchor on a graded arena (see §4 — terrain is a designed parameter, not an accident). Inventories start empty or at a scenario-defined kit. The game master publishes the round's objective and conditions in world chat.
3. **Play phase.** Fixed duration (pilot: one held daylight period, ~40 minutes; full form: scenario-set, possibly including a real night as a difficulty step). Citizens execute their scripts through the reflexive layer — local routines, no deliberation — escalating to a tactical mind only on script-defined triggers. Comms are in-world: team chat channels plus the physical world (chests, signs, named places) as a slow, durable channel.
4. **Scoring.** World evidence only. Banked resources count on receiver confirmation in the syndicate vault; builds count by server-side survey; deaths count from the server log. No self-report scores anything, ever — this is the league's standing rule and the game's referee principle.
5. **Iteration.** The playbooks come out of the file and get revised against the round's evidence: what fired, what didn't, where the script was silent and a citizen improvised and died. Each revision is a new version; the diff between versions, plus the round's triples (§3), is the syndicate's real score across a season.

**Win conditions (per scenario).** Three scenario families, all scored from world state:

- **The Bank.** First syndicate to deposit an objective manifest (e.g. 64 iron ingots, 8 gold, 1 diamond) into its vault chest, receiver-confirmed. A race with interference allowed but not required — the world is the first opponent.
- **The Contract.** The game master issues a build contract (a structure to a spec, at a named site). First syndicate whose build passes a server-side survey wins; partial credit by surveyed fraction.
- **The Long Night.** Survival scoring: syndicate score = living citizens × margin (food + health surplus banked at dawn). This is the calibration scenario — Civ50's evidence (§2) says it is much harder than it sounds.

**What Casey sees.** The spectator surface is the headed client + cameraman + curator line that already exists: he watches named citizens *visibly doing things* — felling, hauling, building, rendezvousing — with team chat narrating intent from actual state (the voice layer's discipline: lines are generated from what the citizen's sensors and inventory actually say, gated against overclaim). The honest caveat, carried from curator v1 and still open in v1.1: the camera shows whoever the cameraman framed, which is not always the citizen the event belongs to; the shot-log correlation fix is a prerequisite for the game's replay/highlight ambitions, not for the pilot. SPECULATION: a post-round "playbook replay" — the round re-rendered as the script's timeline, each trigger firing annotated — would be the spectator artefact this game is really for; it is cheap once the script engine logs its own firings, and it makes script quality *visible*, which no scoreboard does.

---

## 2. Teams, roles, and what a script actually is

### 2.1 Sizes

| Total players | Shape | Notes |
|---|---|---|
| 4 | One syndicate vs the world | The pilot form (§7). Coordination provable, no opponent needed. |
| 8 | Two syndicates of 4, or one of 8 | 4v4 race is the smallest *competitive* form; a single 8 is a comms-scaling test. |
| 12 | Three syndicates of 4, or two of 6 | Free-for-all Bank scenarios; alliance mechanics become possible. SPECULATION — undesigned beyond this line. |
| 16 | Four syndicates of 4, or two of 8 | The full form. Serving arithmetic in §4 says this is a different infrastructure commitment, not a slider. |

Four is the natural syndicate size for three independent reasons: the 1993 *Syndicate* reference Casey cited for the voice-RTS line ran a four-agent squad; the league's lived experience is that four is about the largest crew our current serving stack can keep *present* (§4); and Civ50's collapse (§2.3) was a failure of coordination at scale, not of individual competence.

### 2.2 Roles are hats, not identities

From the civilisation study: roles are **hats a citizen wears for a phase**, assigned by the script, swappable at rendezvous. The standing four:

- **Captain** — holds the syndicate's tactical escalation budget; the only hat allowed to spend presence-brain consults (§4). Wears the comms discipline: broadcasts are the captain's job, so the channel's signal stays readable.
- **Scout** — moves first, marks before moving (routine RH-1: mark, then move), reports terrain in the script's shorthand (relief class, water, hostiles, resources) and *never engages*. The scout's script is mostly movement and reporting discipline.
- **Builder** — executes build contracts and fortification; carries the syndicate's placed-block work. Builder scripts are the closest to the league's existing routine format (surveyed sites, per-cell feet-y, verified placement).
- **Runner** — logistics: hauls between work sites and the vault, runs the named-chest protocol (§2.4), owns the receiver confirmations that scoring counts. The runner is where coordination becomes *physical* — a handoff is a place, a time window, and a confirmation, not a message.

Hats rotate between rounds, not within them (a mid-round hat swap is an escalation event, scripted as a fallback trigger). The design intent: a script describes a *crew*, and the citizens are interchangeable wearers — which is also the honest response to the league's body problem. Citizens die; the syndicate's memory is its playbook and its triples, both outside any body.

### 2.3 The calibration: Civ50

YC Labs' Civ50 (graded B in the towns study addendum) ran 50 agents and recorded **34 deaths, 22 of them before minute 20** — a first-night die-off in a population with no shared pre-round coordination layer. The lesson the design takes as law: *mass-agent survival collapses without pre-coordination*, and the collapse is early — before any in-round learning can compound. Syndicate Protocol's script phase is not flavour; it is the direct countermeasure to a measured failure mode. The second Civ50 import is positive: **Noor's named-chest handoff protocol** — deposit at published coordinates, withdrawal by name, service only on confirmed consumption — is a worked example of a pre-agreed coordination convention doing exactly what this game's scripts must do. It is adopted below as a canonical script pattern, and it is already the league's chosen shape for its (still unplaced) commons chest.

### 2.4 What a script is, mechanically

A syndicate script ("playbook") is a filed document in three layers, matching the cognition tiers the fleet already runs:

1. **Standing orders** — always-on reflexive routines (the league's starter-routine class: mark before you move, dusk is a deadline, never cross unsurveyed relief above density class 2, eat at food ≤ 6). These run locally in the citizen's driver; they cost no model calls.
2. **Plays** — named, triggered procedures: *IF trigger, THEN sequence, WITH fallback*. A play names its rendezvous, its roles by hat, its comms calls, and its abort condition. Plays are the unit of iteration: a play that fails gets revised or cut; a play that fires clean three rounds running is a candidate for demotion into standing orders (scaffold fade, per the routines study).
3. **Escalation table** — the short list of situations the script *refuses* to decide, and what happens instead: hold position and call the captain; captain may spend a consult; if no answer in N ticks, the named default play fires. The escalation table is where honesty lives: a script that pretends to cover everything produces citizens who improvise silently. Ours must *say* what it doesn't cover.

**Worked example 1 — FIRST LIGHT (opening play, Bank scenario).**

```
PLAY first-light            (hats: SCOUT, BUILDER, RUNNER, CAPTAIN all)
TRIGGER: round start, citizens at anchor.
1. SCOUT: move to survey point A (low-relief route, relief class ≤2).
   Call "A-clear" or "A-hot:<bearing>". If A-hot twice → fallback dusk-post.
2. BUILDER: on "A-clear", move to A. Fell 6 oak. Place table. Call "table-up".
3. RUNNER: stay within 8 of BUILDER. On "table-up": collect planks ≥16,
   run vault route V1, deposit, call "banked:16" ONLY on vault confirm.
4. CAPTAIN: hold anchor. On "banked:16" → play tool-up. On any citizen
   hp < 10 → call "regroup:anchor" (all hats comply, no questions in chat).
ABORT: if table not up by tick 6000 → play dusk-post at anchor instead.
COMMS: calls are the four quoted strings only. Anything else is escalation.
```

**Worked example 2 — THE NOOR HANDOFF (transfer play, any scenario).**

```
PLAY noor-handoff           (hats: RUNNER gives, BUILDER receives)
PRECONDITION: chest C at published coords named in the playbook header;
  manifest M listed with counts.
1. RUNNER: place items M in C. Call "C-loaded:<M-hash>".
2. BUILDER: attend C only after "C-loaded". Withdraw exactly M.
   Call "C-confirmed:<count>" on inventory match.
3. If no "C-confirmed" within 600 ticks → RUNNER re-attends C, reports
   actual contents ("C-actual:<contents>"); CAPTAIN decides via escalation.
RULE: a transfer counts for scoring only on the receiver's confirmation.
  The giver's call scores nothing. (League commons rule, verbatim.)
```

Both examples are deliberately plain-language. The design proposes playbook entries stay human-and-agent readable text in the pulse routine style the league already uses, with the trigger/fallback structure explicit — because the iteration phase is a *diff review*, and a notation Casey can't read at a glance fails the spectator test at the design layer too.

---

## 3. Two-phase cognition is the core mechanic

The game's central design claim: **the split between what is decided before the round and what is decided during it is not a production detail — it is the game.** Everything else (Minecraft, syndicates, chests) is the board it is played on.

**May be scripted (compiled-ahead).** Routes over surveyed terrain; rendezvous and handoff protocols; comms vocabulary and channel discipline; role/hat assignments; fallback triggers and abort conditions; escalation tables; resource manifests and bank priorities; dusk/night posture. In the seed email's terms, this is genesis path 1 — compile the loop — applied to coordination itself.

**Must be decided in-round (digested-live).** Responses to unsurveyed terrain and hostile contact; opponent syndicates' observed plays; weather and game-master condition changes; any situation the escalation table names. In-round cognition is deliberately *expensive and rationed* (§4): the tactical mind is slow and shared, so a script that escalates constantly is a script that queues — and the queue is visible in the citizen's behaviour as standing still. That is the balance lever made physical.

**Script budget as a balance lever.** Three candidate limits, all measurable, to be tuned by pilot evidence rather than taste (SPECULATION on values; the *mechanism* is the proposal):

- **Play count** — a playbook may carry at most K active plays (pilot proposal: 12). Forces prioritisation; the cut list is itself a strategic artefact.
- **Trigger surface** — each play's triggers must be checkable from citizen-local state (inventory, position, health, chat calls received). A play whose trigger needs global knowledge is illegal — it would silently never fire, or fire on a guess. This is the league's phantom-completion lesson written as a rule: if the citizen can't sense it, the script can't use it.
- **Escalation budget** — consults per syndicate per round (pilot proposal: 4), spent only by the captain hat. The consult books already run at 2 per citizen per hour with provenance required; the game's budget is the same discipline, made a resource.

**How script quality is measured.** Never by inspection. A playbook is good iff its syndicate's world outcomes improve across rounds: banked totals, deaths, plays fired vs plays aborted, escalations spent vs escalations needed. Each round files **triples in the commons library's shape** — situation → script (play + version) → verified outcome — so a strategy's reputation is an evidence trail, exactly as citizen skills already are. A play with three filed failures is dead whether or not its author still loves it. This also solves the season problem: when a citizen dies permanently or a player rotates in, the syndicate's knowledge survives in its triples and its playbook versions. The bodies are mortal; the syndicate is its paper.

---

## 4. Substrate plan — what exists, what's missing, the arithmetic

### 4.1 What exists today

- **World**: Paper 26.1.2 on the Orin, headed, with a guarded cameraman (landing-verified daylight holds) and a live citizen population's worth of operational scar tissue, all filed.
- **Citizens**: mineflayer bodies with a voice-and-tastes layer (built for Cody, offline-verified, evening lines gated to template-only after the overclaim fix), starter routines, and a triples library with a working allocator and provenance discipline.
- **Minds (Thor)**: presence brain on :8310 (Qwen3-Coder-30B-A3B — Casey's resident, never to be restarted or shed); actor server on :8311 (llama-server; the on-disk "Qwen3-0.6B" is a 1.7B-class body under a 0.6B config — internally consistent, never to be cited as canonical 0.6B); JEV rack on :8077.
- **Governor (:8642)**: per-identity rate budgets — cody 240/300, vega 300/600, cody-actor 240/600, geist-mind 300/900, pulse-smith 60/900 — with a **permissive default of 120/120 for unmapped identities that fails silently**. That default is the single most dangerous line in this section: an unmapped game identity would not error; it would quietly starve.
- **Game master**: built, Thor-resident, stages small reversible world-parameter nudges with receipts; its recorded bottleneck is citizen *presence* — its first nudges landed in an empty world. It is a host looking for a party, which is precisely what this game supplies.
- **Comms**: in-world chat (citizens narrate from state), consult books (2/citizen/hour, provenance-gated), the commons chest protocol (receiver-confirmed transfers), the ledger.

### 4.2 The serving arithmetic, honestly

Measured decode on the actor stack is **7.9–8.4 steps/s** single-stream (the WSP clause-2 context). That number, not enthusiasm, sizes the game.

Assume a tactical decision is ~120 output tokens (a short plan fragment or a chat call with reasoning suppressed — `enable_thinking:false` is already a hard requirement on this stack). At ~8 tok/s single-stream, one decision ≈ 15 s of decode. llama-server batches concurrent slots, and aggregate throughput rises with batch — but decode on this unified-memory box is bandwidth-bound and scales sublinearly; nothing on our bench licenses assuming better than ~3–4× aggregate at batch 8–16 (SPECULATION as a planning figure, flagged as the pilot's first measurement job).

Design consequences, by size:

- **4 agents (pilot).** Tactical cadence of one decision per citizen per ~30–60 s is affordable if escalations are staggered and the reflexive layer carries everything between ticks. This is roughly league-present load, times two. **Feasible on current substrate with governor identities mapped per citizen.**
- **8 agents (4v4).** Same per-citizen cadence costs roughly double the aggregate decode; the captain-only escalation rule (§3) is what keeps this inside the envelope — at most 2 captains thinking hard at once, 6 citizens mostly running scripts. Feasible with discipline; the queue becomes a visible game mechanic (§3) rather than a defect.
- **16 agents (full form).** Not a slider. At the pilot's cadence, 16 citizens want ~4× the pilot's aggregate decode, plus presence-class calls for four captains. Options, honestly priced: (a) slow the tactical cadence to 2–5 minutes and make the game *more* script-driven (defensible — it pushes play toward the design's thesis); (b) a second actor stack on the Orin's CUDA headroom (the Orin already hosts the world; its spare capacity is small — 1.5–2 GiB headroom was measured for a *small* engine, not a second llama-server of consequence); (c) wait for a faster decode path — the D3D line (ACTIONS item 11) closed as *untested*: governance could not lease the memory on the current bench, and its quiet-window rerun remains a named option, not a plan. **The study's recommendation: design the game so cadence (a) is a scenario parameter, and treat 16 as gated on a decode measurement we do not yet have.**

Every agent, at every size, needs a **mapped governor identity with a deliberate budget** before first launch. The silent permissive default is treated in this design as a launch-blocking defect class (§6).

### 4.3 Terrain: the wedge verdict becomes a design parameter

Triple-020 resolved the league's movement wedge: the carrier is **surface relief geometry** — dense +1 full-block step faces (24.8–29.4 faces/100 columns in the veto district vs 5.4–9.5 on walked anchors) wedge genuine bodies; a flattened arm (chunks levelled to y=66) walked 8/8 legs at zero corrections and completed the approach onto the pin cell itself. Player edits, litter, stone material, InhabitedTime, entities, level data: each exonerated in turn.

For the game this converts a mystery into a dial:

- **Arenas are graded flat by default.** A Syndicate arena is generated or surveyed to relief class ≤ the walked-anchor band. This is now a *known, mechanical* preparation (the flatten procedure exists and is verified on copies), not a hope.
- **Relief is an obstacle class, deliberately placed.** Scenario designers may include a high-relief district as terrain difficulty — a ridge the scout must route around, a stony field that slows a runner — with the density numbers as the spec. What the record forbids is *accidental* relief: unsurveyed natural terrain in a play area is a bug, because its failure mode (a citizen pinned, bit-identical, for thousands of forced moves) looks exactly like a citizen failure and is not one.
- **Routes are surveyed, not assumed** — the relocation-driver discipline (per-cell feet-y from survey) that carried Cody's S1 pass is the template for script route-writing.

### 4.4 What's missing (build list, sized)

1. **Multi-mind serving configuration** — per-citizen governor identities + budgets for 4/8/16; a staggered tactical tick scheduler so escalations don't convoy. Pilot-sized: days, not weeks; it is configuration and a scheduler on existing services, not new serving infrastructure.
2. **Team comms channels** — syndicate-scoped chat routing with the captain-broadcast discipline; the substrate (in-world chat) exists, the scoping does not.
3. **Arena generation/grading** — a flat-arena template world (or a grading pass over a copied district, per the verified flatten procedure) + a relief-density survey tool reusing the census method. The Orin surface census already produced the measurement approach.
4. **Round lifecycle on the game master** — the GM grows from nudge-host to round host: publish objective, hold/release the daylight state per scenario, snapshot scores from world evidence at round end, file receipts. Its nudges become scenario conditions (weather, growth rate); **refereeing stays with world-evidence scoring (§1), not with the GM's judgement** — the GM stages and receipts; it does not decide outcomes. That separation is the Watcher's Charter applied to a referee: the score must be readable from a store the scorer doesn't write.
5. **Save-pool hygiene for a cast of 16** — fresh identities must be *genuine* fresh spawns with saves present in the live directory before launch (rule v2); the sample-clone behaviour of this Paper build (a join with no readable save clones a sample) is disqualifying for a game cast and must be engineered out of the round setup checklist, not discovered mid-round.

---

## 5. The board: Sitka, generated from real ground

*Addendum folded in at Casey's direction, 2026-11-08 16:50 AKST: "We could easily make the starting state of our world in Minecraft be Sitka." He is right that the fleet has done this three times in three mediums — and the honest version of "easily" is: the shape pipeline is proven, the Minecraft-specific generation work is real but bounded, and the wedge verdict (§4.3) turns world generation from a cosmetic choice into a correctness problem with a known solution shape.*

### 5.1 The pipeline

The method is the one SuperInstance/Otherhere and luciddreamer-ai/OpenSkyFlight already locked: **one honest source per layer, never blended.**

1. **Topography — SRTM/DEM.** Elevation data is the shape. OpenSkyFlight's formulation: *the data WAS the mountain, rendered simply on top.* The Foundry already mints terrain from a real SRTM crop of Sitka (57.02°N, 135.37°W) as a parametric archetype (mint ≈ 2.2 s) — the fleet's proof that this exact town's DEM flows through our tooling.
2. **Coast, water, islands — charts.** At Sitka's latitude and SRTM's resolution, the raw DEM's shoreline is not trustworthy to the block; the Otherhere stack used charts to lock coast/water/islands, with the DEM subordinate at the waterline. Sea level is a *decision the charts arbitrate*, then a constant in the generator: water level = sea level, everywhere, no exceptions.
3. **The town — OSM footprints and roads.** Building footprints give the town's baseline look and feel; roads give the movement network. In Minecraft terms the OSM layer is not decoration: a footprint becomes a **flat pad** (see §5.3 — the pad is also the grading), and a road becomes a surveyed route, which is the only kind of route a script may rely on (§4.3).

**Bathymetry is a first-class layer in Sitka, not a footnote.** The Sound is the town's front yard: harbour, channels, and the crossing to Japonski Island are gameplay space for any scenario involving boats, bridges or the airport. OpenSkyFlight's region packs carried below-sea terrain for exactly this reason. The generator therefore treats the DEM's negative values (and chart soundings where the DEM is void over water — SRTM is land-only in the relevant tiles, stated plainly) as terrain, not as a floor to be flattened at sea level.

### 5.2 Scale arithmetic, worked honestly

SRTM's 1 arc-second postings at 57°N are ≈ 30.9 m north–south by ≈ 16.8 m east–west — anisotropic; any block grid resamples them, and the resampling is interpolation, not measurement. That is fine for shape and disqualifying for pretending to survey-grade truth; the game's scripts survey their own routes in-world anyway (§4.3).

Three candidate boards:

| Board | Extent | At 1 block = 1 m | Verdict |
|---|---|---|---|
| Full Sitka Sound (Baranof west coast, Kruzof, the island field) | ~15 km across | ~15,000 × 15,000 blocks | Unplayable as an arena; the town becomes a smear (a 10 m house ≈ 10 blocks only at 1:1 — at the 1:3–1:4 compression this board forces, 2–3 blocks). Backdrop material only. |
| **Town core: downtown + harbour + Crescent Harbor + Japonski Island (airport) + the bridge** | ~2.4 km × 2.0 km | 2,400 × 2,000 blocks = 150 × 125 chunks ≈ 20 region files | **The arena.** Houses, piers and the bridge at true size; the whole board walkable end-to-end in minutes; small enough to grade completely (§5.3). |
| Town core + near sound ring (compressed) | core at 1:1, ring at ~1:3 | core as above + a scenery apron | The full form's ambition: playable core, honest horizon. Ring generation is extra work and is *not* in the pilot's path. |

**Vertical is the binding constraint, and it resolves in the core's favour.** This build's world spans y −64…320 (384 blocks). Setting sea level at y 63 (the league's existing surface convention) leaves 257 blocks above the water. The town core's own ridge — the hills directly behind downtown — rises a few hundred metres (order 200–250 m), which at **1:1 vertical just fits** under the build limit. The big landmarks do not: Mount Verstovia (~780 m) and Mount Edgecumbe (~976 m, on Kruzof Island across the Sound) cannot stand at 1:1 vertical in any crop. The design treats them the way the town itself does — as *horizon*: backdrop terrain at compressed vertical scale, outside the playable boundary, looked at and never climbed. Below the waterline, 127 blocks of depth are available to bedrock; the harbour and near channels (tens of metres) fit at 1:1, deep Sound channels get mild vertical compression — stated on the chart layer, not hidden.

So the recommended board is: **1:1 horizontal, 1:1 vertical, town-core crop, sea level y 63, landmarks as compressed backdrop.** One scale, honestly held, everywhere a citizen can walk.

### 5.3 The wedge constraint as a generation rule

Triple-020's verdict, applied as law: **raw DEM terrain at fine scale is exactly the dense +1 step-face relief that wedges citizens.** A heightmap rasterised naively gives every slope a staircase of full-block faces; on Sitka's real hillsides those faces arrive at the veto district's density (24.8–29.4 per 100 columns) or worse. A generator that imports the DEM faithfully and stops there has built a beautiful board the citizens cannot cross. The fleet has already paid once to learn this; the generator pays it forward:

1. **Generate the topography, then grade the playable surface.** Two passes, separately inspectable. Pass one is faithful shape (DEM + charts + bathymetry). Pass two is the *walkable quantisation*: within the playable boundary, elevation is terraced — snapped to contour bands — so that slopes resolve into deliberate steps with run between them, and districts the census would call low-relief (≤ ~9 step faces per 100 columns, the walked-anchor band) stay that way.
2. **The town layer grades itself.** OSM footprints flatten to pads; roads are graded to gentle, surveyed profiles. In the town core — where most syndicate play happens — the built environment *is* the flat ground, which matches how the real town sits on its shore.
3. **True relief is kept where it belongs: outside the fence.** Backdrop mountains keep the DEM's real, unquantised shape. The trade-off is stated plainly: the playable Sitka is Sitka's *shape* under a walkability quantisation, not Sitka's literal surface at block resolution. A purist board is unplayable; a flat board is a lie; the terraced board is the honest middle, and the terracing parameters (band height, max step-face density per district) are scenario-visible design values, not hidden smoothing.
4. **Relief remains a difficulty dial (§4.3)** — a scenario may designate a *deliberately ungraded* district (an old-slide slope, the rough shore) as obstacle terrain, with its density measured and published in the scenario, so a pin there is a known hazard priced into scripts, never a surprise blamed on a citizen.

### 5.4 What transfers, what is new work

**Transfers directly (proven in the fleet):**
- The SRTM Sitka crop and DEM handling (Foundry terrain archetype, mint ≈ 2.2 s — generation of *shape* is a solved, fast step).
- The layered-source discipline and the specific layer sources (Otherhere: charts = coast/water, topo = terrain, OSM = town).
- Bathymetry-as-terrain (OpenSkyFlight region packs).
- The reading/verification half of Minecraft world data: the wedge lanes byte-validated an NBT/MCA pipeline (mcprobe) across 4,642 chunks — the fleet can *inspect* a generated world chunk-by-chunk and verify the grading pass did what §5.3 claims, in a store the generator doesn't write. That verification loop is what makes the generation rule more than a hope.

**New work (named, not waved at):**
- **Region writing at scale.** ~20 region files / ~18,750 chunks for the core board, written correctly (heightmaps, biomes by elevation + slope — rock above treeline, spruce forest on the slopes, gravel/sand shore at the waterline — light, and the terraced surface) is the largest single build item in this study. The ecosystem offers routes (heightmap-oriented world painters such as WorldPainter; programmatic chunk editors such as Amulet) — named here as *survey starting points, not evaluated choices*; the fleet's own mcprobe lineage argues for a homegrown writer we can verify byte-for-byte, at the cost of building it. SPECULATION on effort either way until a spike measures it; a one-region generation spike is the obvious first step and belongs in Pilot A's setup (§7).
- **OSM-to-pad/road rasterisation** at 1:1 with the town's actual footprint set — modest data work, but the pads must agree with the terraced elevation pass or buildings float and sink.
- **Backdrop ring** (compressed landmarks, Edgecumbe sightline) — deferred past the pilot by design (§5.2).

### 5.5 Game meaning

Home ground is *real ground*. Syndicates hold the harbour, contest the bridge, stage from the airport island; Mount Edgecumbe sits on the horizon where it sits from the real waterfront. Two consequences matter more than the romance:

- **The script phase gains a real atlas.** Pre-round scripting (§3) is written against a map everyone — Casey included — can study beforehand, because the map is a place that exists. Reconnaissance stops being an in-round tax: the scout's job becomes *verifying* the atlas against today's world state (what changed, what's occupied), which is the correct division between compiled-ahead knowledge and live perception, and the same division the room/mud mapping thread draws between the map and the territory's current weather.
- **The pipeline is place-agnostic.** DEM, charts and OSM exist globally. Sitka is instance #1 because it is home and because its data is already in the fleet's hands — but nothing in §5.1–§5.3 is Sitka-specific except the crop coordinates and the landmark table. A second board (another town, another sound) is a data job, not a design job. That generality is the difference between a level and an engine, and it is the same compounding test the fleet applies everywhere: subject N+1 must be cheaper than subject N.

---

## 6. Failure modes from our own record, mapped to mitigations

| League failure (on record) | What it cost | Design mitigation |
|---|---|---|
| **Hold-loss incident** — daylight refreshes sent but never landed (~05:58Z onward); the world ran real nights for ~90 min; Cody's deaths went 38 → 114 in the window | A citizen's season, nearly; the Watcher's Charter exists because of it | Round daylight state is landing-verified per refresh, or the round clock pauses and alarms. A play phase never runs on an unverified hold. Two misses = HOLD-LOST alarm + round suspension, per the guarded cameraman's existing discipline. |
| **Respawn grind** — a citizen re-entering a lethal loop unchecked | Death counts in the dozens before a human noticed | Hard trial rule, already league law: **a citizen who starts a respawn grind is stopped; any trial aborts after 3 deaths.** In game terms: 3 deaths in a round = the citizen is benched and the syndicate plays short-handed. Death is a resource loss, not a spectator loop. |
| **Save-pool hazard** — joins with absent saves cloned sample bodies; clone-inherited bodies froze; the pool-aside manoeuvre was retired | Weeks of misattributed "body" failures | Round setup checklist: every cast member's save verified present in LIVE players/data immediately before launch; genuine identities only; no pool games. (§4.4 item 5.) |
| **Silent governor default** — unmapped identities fall to a permissive 120/120 budget and fail *silently* | Invisible starvation; would present as "dumb citizens" | Launch gate: no citizen joins a round without a mapped identity and a budget sized in the round plan. The pre-round checklist greps the governor map; absence blocks the drop. |
| **The wedge** — dense step-face relief pins genuine bodies (triple-020) | The league's central mystery for a day; multiple lanes | Graded arenas + surveyed routes (§4.3); relief above class density in a play area is a scenario defect, filed against the scenario, never against the citizen. |
| **Phantom digs** — server enforces dig reach ≈ 4.5 blocks; longer "completed" digs are fiction | False progress reports; builds that weren't | Script rule (already league law): dig counts are attempts; only re-scan/displacement verifies. Build-contract scoring is by server-side survey (§1), so a phantom dig scores zero automatically. |
| **Remnant hostiles at spawn** — a fresh join killed by a leftover zombie because the hold fixes time, not leftovers | Geist's seventh death of his sequence | Drop protocol includes a same-hour spawn-country sweep (existing league gate), and arenas are enclosed/surveyed so the sweep is small. |
| **Claimed-but-not-done, generally** — self-reports accepted as landings | The fleet's recurring failure class, every layer | Scoring, handoffs, and holds all settle in stores the actor cannot write (§1, §2.4, §4.4). A syndicate cannot talk its way to a point. |

---

## 7. Pilot proposal

**Recommendation: stage it — Pilot A proves the machine, Pilot B proves the game.**

### Pilot A — one syndicate of 4 vs the world (the Bank, small manifest)

- **Cast**: 4 fresh genuine identities, governor-mapped, hats assigned (captain/scout/builder/runner). Cody, Vega and Geist are *not* cast: they are parked citizens with their own seasons and (in Cody's case) a critical state; the pilot uses new bodies on a **scratch arena**, not the live home district. The arena is the first district of the Sitka board out of the §5 pipeline — preceded by the one-region generation spike (§5.4); if generation slips, a graded-flat copy of existing terrain is the fallback board and Sitka follows for Pilot B.
- **Objective**: bank a small manifest (e.g. 32 oak logs converted to planks + 8 cobblestone + 4 iron ingots if the arena's surveyed geology allows; the manifest is set from the arena survey, not from optimism) into the vault chest, receiver-confirmed, inside one landing-verified daylight hold (~40 min).
- **Script phase**: the four citizens' playbook is written *before* the drop, filed, and versioned — including at minimum an opening play, a Noor handoff play, a regroup fallback, and an escalation table with a consult budget of 4.
- **Pre-registered success criteria** (filed before the drop, judged from world evidence):
  1. The syndicate banks ≥ 75% of the manifest by count, receiver-confirmed, within the round.
  2. Zero deaths; zero respawn-grind events; no citizen pinned (forced-move storm > 60 s at one cell) on surveyed routes.
  3. ≥ 2 plays fire as written (trigger → sequence → confirmation) with no operator intervention.
  4. Every escalation is inside the budget, and every consult is answered from the book/ledger with provenance.
  5. The tactical queue never exceeds the cadence envelope: no citizen waits > 90 s for a tactical decision more than twice.
- **Kill criteria**: any criterion failed on *substrate* grounds (serving starvation, pin on a surveyed route, hold unverifiable) kills the *substrate*, not the design — fix and re-run once. Failure on *script* grounds (plays don't fire, escalations exhaust by mid-round, manifest < 25%) with a healthy substrate kills the script-budget values in §3 and forces their redesign before any 4v4.

### Pilot B — 4v4, the Bank, opposed

Two syndicates, mirrored arenas or one shared arena with two vaults (shared, once Pilot A proves the serving), same manifest, first to full bank or highest banked fraction at the horn. Success = Pilot A's criteria held by *both* syndicates under contention, plus at least one observed opponent-adaptive event (a play changed, a route re-surveyed, an escalation spent on the opponent's behaviour — filed as a triple) proving the in-round layer is alive and not just executing.

### What would scale it, what would kill it

- **Scale signal**: Pilot B passes with tactical cadence headroom (criterion 5 met with margin) → the 12–16 forms become a serving project (second actor stack or a measured decode path) with the game design unchanged. The playbook/triples corpus from 8 citizens is also the first real dataset for the decision-model patterns shelf.
- **Kill signal**: if, after one substrate fix cycle, citizens cannot hold a 30–60 s tactical cadence at 8 concurrent minds on this bench, the *concurrent* form dies on our hardware and the design pivots to its honest fallback: **asynchronous syndicates** — teams play the same scenario sequentially against the clock and the world, compared on world evidence. That fallback keeps everything this study is actually about (script phase, iteration, evidence scoring) and gives up only simultaneity. It is named here so that a serving failure is a pivot, not a funeral.

---

## Lineage and debts, stated plainly

- **1993 *Syndicate*** (Bullfrog): the four-agent squad and the syndicate fiction; Casey raised it 2026-10-10 for the voice-RTS line. This study takes the squad size and the fiction, not the mechanics.
- **Radio Hour**: the phase structure (§1) is its Work → Persona → Listening Round → Night → Iteration with the listening round promoted to the main event.
- **The seed email's two genesis paths** (compiled-ahead vs digested-after): the game's two phases are those paths, made playable and scored.
- **Civ50 / YC Labs** (grade B, single run, interested-party authors): the calibration (§2.3) and the Noor protocol. The design leans on its death distribution, not its conclusions.
- **The league itself**: every substrate fact in §4–§6 is from the triples library (007–020), OPERATIONS.md, and the 2026-11-08 lanes. The wedge verdict (triple-020), the hold-loss incident and the Watcher's Charter, the save-pool record, and the governor's silent default are the four load-bearing ones; a reader who checks nothing else should check those.

## Open questions (filed, not resolved here)

1. Tactical cadence under real batch load at 8 concurrent minds — the pilot's first measurement; §4's 3–4× aggregate figure is a planning speculation until then.
2. Whether the game master's condition nudges can be made legible enough, mid-round, to be *played against* rather than merely endured — the difference between a host and a referee-shaped weather system.
3. Script notation: plain-language playbook (proposed) vs the pulse routine format, once playbooks grow past ~12 plays and diffs get hard to read.
4. Permanence: do pilot citizens persist between rounds (seasons, reputations, death counts that matter) or reset per match? The league's instincts say persist; the game's balance may say reset. Pilot A runs persistent-by-default and files the question with evidence.

*End of study. Filed on the studies shelf; home room: the-league-and-civilization.*

---

## Addendum 2 — 2026-11-08: The Paint Layer and the Four Tiers

*Casey's direction, 2026-11-08 16:57 AKST, on the study as filed: (1) the game on the surface should be SILLY — paintball-ish, very large paintballs that really splatter, cartoonish, playful, not killing and not dark — with real strategy underneath (four teams hunting each other, capture the flag, whatever the game-within-the-game is); (2) the engine is a stack of timescales: bot bodies running scripts like RTS peons, rotating on their use of the Thor's perception models and calling higher-level agents; decision engines on a faster cycle up, where vision and abstraction come together; LLMs on the round cycle, reflecting on the entirety of what happened, improving the scripts and the adjustment level itself; and above that, the possibility that something larger changed in the world, demanding an entirely different set of scripts. This addendum takes both directions as design constraints and reconciles them with the parent study: where it contradicts §3–§4, it says so and supersedes.*

### A2.1 Tone is a design constraint, not a skin

"Silly on the surface, real strategy underneath" is not an art direction applied to a finished game — it changes which mechanics exist. Paint is the medium, and paint has four properties no lethal framing has:

1. **A hit is visible and persistent.** A splat stays on the block, the tree, the citizen it hit. Trails of colour record who ran where and when; a contested square carries the fight's history on its face. The board becomes a *ledger of the fight, readable at a glance* — in Casey's own vocabulary, paint gives the round **tells**: the strategy underneath is serious, and its evidence is worn on the world, not hidden in a log.
2. **Being "out" is a splat, not a death.** A tagged citizen is *marked* — saturated in the opponent's colour — and walks back to base to reset. This dissolves the league's ugliest failure class (§6, respawn grind) *by construction*: there is no lethal loop to grind in, nobody's death count inflates while a watcher sleeps, and the walk back is itself play (a marked runner crossing open ground is intelligence for the other side: their colour trail says where their base sends them). The 3-death bench rule is replaced by a tag-out rule, and "deaths" never appear as a citizen statistic in this game at all.
3. **Objectives can be paint-native.** Capture-the-flag becomes *cover the monument in your colour and hold the coverage*; territory scoring is literally surveyed colour fraction; a "raid" is repainting the opponent's vault door. Every one of these scores from world state by survey — the paint does double duty as the *scoring substrate*, which keeps §1's referee principle (world evidence only, in a store the actor cannot write) intact and makes it cheap: the survey the Contract scenario already needed *is* the paint census.
4. **Spectacle is legible.** Per §1's spectator test — citizens visibly doing things — a paint fight reads at camera distance in a way resource hauling does not: you can see who is winning a skirmish from the colour on the ground before anyone counts. Casey watches RTS-like troops whose combat is legible and silly while the manoeuvre underneath is real.

**What the tone forbids, stated as law:** no lethal framing anywhere — not in mechanics, scoring, narration, or the voice layer's lines. Citizens are tagged, marked, splatted, dunked; never killed, eliminated, or "taken out" in the lethal sense. Opponents are rivals, not enemies to be destroyed. The game's vocabulary is part of its substrate: a narration line that frames a tag as a kill is a defect of the same class as an overclaim line, and gets gated the same way (the evening-line template gate is the precedent mechanism).

**What it costs, honestly:** vanilla Minecraft has no paintball. The paint layer is a mod/plugin surface of unknown size — candidates range from a server-side plugin painting blocks on projectile hit (bounded, server-authoritative, matches our Paper stack) to riding an existing paintball mod (unvetted, version risk against Paper 26.1.2). This is a build item for Pilot A's setup, and it is *not* small-print: if the splat cannot be made persistent and surveyable server-side, the paint-native scoring above degrades to ordinary hit-counting and this addendum's central mechanic is weakened. NAMED UNKNOWN — sized by a spike, not by optimism. The large-splat fantasy (very large paintballs, dramatic coverage) is also a tuning surface: splat radius is a balance lever (coverage rate per hit vs ammunition/logistics cost), filed as SPECULATION until played.

**Scenario re-skin (the three families of §1, repainted):**

- **The Bank → The Vault Door.** The race structure survives, but the win artefact is paint: first syndicate to cover the neutral monument (or the opponent's vault door, in 4v4) to a surveyed colour fraction — hauling becomes *paint logistics* (dye/pigment supply chains), which keeps the runner hat's physical coordination and gives it a visible product.
- **The Contract → The Mural.** A build contract scored by survey, where the spec includes colour fields: build the structure *and* paint it to the pattern. Partial credit by surveyed fraction, as before, now including colour accuracy.
- **The Long Night → Tag Season.** The survival calibration scenario does not survive the tone change — *and that is a deliberate trade, stated plainly*: Civ50's die-off was calibration for a lethal world; a paint world's calibration problem is different (coverage races, ammunition logistics, tag-out tempo), and the Long Night's lesson — pre-coordination or collapse — is now tested by the script phase against the *clock and the other syndicates* rather than against the night. The lethal survival game remains available to the league proper; it is not this game's mode.

### A2.2 The four-tier timescale stack

§3 described two phases. Casey's correction: the in-round side is not one layer but a stack of clocks, and the stack is the fleet's standing **System 1/2/3** architecture applied per-agent (fleet definitions, 2026-10-09 / 2026-11-05: System 1 = sub-verbal reflex algorithms and decision engines, following an already-laid route without asking another question; System 2 = the voice in the head — a fast local model an agent calls inside the rotation, putting words to what the layers beneath are doing; System 3 = calling on the world — quilted System-2 thinkers, externalised evidence, answers on the world's schedule). The game runs *four* tiers because its rounds add a clock the architecture leaves implicit: the world itself changing size.

**TIER R — Reflex (continuous; seconds and below).** The bodies: up to 16 mineflayer-class instances — "the aura agent or mineflayer or baritone or something that mixes them," mixed per team, the way the 2026-10-14 lineage study already decomposed the field (Mineflayer = body/protocol; Baritone/pathfinder = the scripted motor layer; Voyager = the pulse pattern in which an expensive mind authors skills the cheap layer runs; Mindcraft = LLM-in-the-loop, the contrast case). A Tier-R body runs its filed scripts — standing orders and play fragments — and *continues on its own* like an RTS peon or a patrolling troop: pathing, harvesting, hauling, holding a post, executing a triggered sequence to its end. **Perception at this tier is reflex-level and rotated.** The bodies do not each own a perception model; they timeshare the Thor's rack (the JEV rack on :8077 and the vision-language serving) on a schedule, and what the rotation delivers is *contact-class signal only*: splat-nearby, flag-visible, colour-seen-bearing, obstacle, hat-signal. A body that needs richer perception does not get it at Tier R — it escalates (Tier D). This is the seed email's "digest the exceptions" applied to senses: the reflex tier digests raw frames into a handful of named signals; only exceptions travel up.

**TIER D — Decision engines (the fast cycle; seconds to a minute).** One tier up, vision and abstraction come together: perception products — the rotation's signals, accumulated over a window — fuse into a *situation picture* per syndicate (where the colour is, where our hats are, which plays are live), and a decision engine works that picture on its own clock: selecting which filed play fires, re-planning a route locally, re-tasking a runner. Tier D scripts are *their own kind of scripting* — decision rules and play-selection logic, authored and tuned separately from Tier-R routines and Tier-L playbooks, running faster than reflection and slower than reflex. In fleet terms Tier D is where the §3 escalation table actually lands: escalations that §3 sent to "the tactical mind" split here — *play-shaped* escalations resolve at Tier D from the filed book; only *book-shaped* problems (the book has no play, or two plays conflict) go further up. The captain's consult budget (§3) is spent at Tier D, by the captain hat's engine, not by bodies and not by the LLM.

**TIER L — LLM reflection (the round cycle; between rounds).** The expensive minds pay full price *once per round, not once per second*: after the horn, a syndicate's LLM reads the entirety of what happened — firings, punch-lists, the paint census, the triples — and does the three jobs only it can do: (a) **improve the scripts** (revise plays, cut dead ones, promote proven plays toward standing orders — §2.4's scaffold fade, now assigned an owner and a clock); (b) **tune the adjustment level itself** — the meta-job: how much may Tier D re-plan before it must escalate? how wide is Tier R's trigger surface? The adjustment level is a *filed parameter set*, versioned with the playbook, and Tier L is its only editor; (c) **file the round's triples**, so the season's evidence accumulates in the commons shape (§3). Tier L is System 2/3 in the fleet sense — the voice that narrates and the call on the world — and the game schedules it the way the fleet does: deliberation happens where time is cheap, which is *outside* the round.

**TIER W — World-change (the slowest, largest clock; between scenarios, or mid-season).** Sometimes something larger has changed than any decision-maker perceived or any reflex registered at its true size: the board is regenerated, a new syndicate joins, the paint rules change, the game master introduces a condition that rewrites what "good play" means — or, the honest internal case, the *evidence* accumulates that the syndicate has been optimising the wrong game (winning coverage races while losing every mural; a season of triples whose pattern only shows at season scale). The correct response is not a patch, not a re-plan: it is a **playbook swap — an entirely different set of scripts**, a re-perioding of the syndicate's strategy. Doctrine, one line per tier: **patch at R/D, re-plan at L, RE-PERIOD at W.** The fleet's failure ladder maps onto the tiers cleanly: *repair* (local fix, same scripts — Tier R/D), *rewind* (back to the last good playbook version — Tier L's job, trivially available because playbooks are versioned artefacts), *restart/diverge* (a genuinely new script set against the same spec — Tier W). A syndicate that patches a Tier-W change at Tier D will lose efficiently; naming the tier of a problem is itself a Tier-L duty, reviewed at Tier W.

**Who detects a Tier-W change?** Candidate triggers, stated as a detection spec rather than a hope: (i) *registrar events* — board regeneration, rule changes, cast changes: mechanical, announced, logged; (ii) *game-master conditions* — the GM (§4.4) is the natural sensor and registrar: it already stages receipted world changes from outside the party, so its receipts *are* the Tier-W event log, and its charter gains a clause here: it serves as **neutral referee and change registrar** — it registers and timestamps world changes, and never adjudicates their meaning for a syndicate (each syndicate's Tier L decides what a registered change demands; a referee that also interprets is a player); (iii) *season-pattern evidence* — a syndicate's own triple corpus crossing a pre-filed threshold (e.g. a play family's filed failure rate inverting across a season) — detected by Tier L wearing its Tier-W hat at season review, which is a scheduled event, not a vibe. The failure mode this defends against is the league's own: the board changing under a hold nobody verified — at Tier W, the change is *registered in a store the syndicates can read*, or it does not count as announced.

### A2.3 The scheduling arithmetic, redone — and what it does to §4's conclusion

The parent study's §4.2 conclusion was: 4 feasible, 8 with discipline, **16 gated on a decode measurement we do not have.** The gating assumption was that tactical cognition scales with bodies — every citizen wanting a ~120-token decision every 30–60 s, all of it paid at actor decode rates (measured 7.9–8.4 tok/s single-stream; planned aggregate ~3–4× at batch 8–16, SPECULATION there as here). **The tiered stack refutes that assumption, and therefore the conclusion — with one surviving gate, stated below.** Tier by tier, with the numbers we actually have:

- **Tier R costs no decode at all.** Reflex scripts are code, not generation. 16 bodies cost CPU and server ticks, not tokens — mineflayer-class bodies are the league's existing load profile, and the *serving* question for Tier R is only the **perception rotation**: reflex-class signals from the Thor rack. Measured rack figures: the JEV semantic judge answers at ~137–223 ms per call including load amortisation (and 12.3 ms p50 for the bare judge benchmark at 4 threads on Jetson-class ARM, per the F4 audit) — a *classification* call is two orders of magnitude cheaper than a *generation*. A rotation giving each of 16 bodies one reflex perception product per 2 s is 8 calls/s — comfortably inside a rack that answers in ~0.2 s (theoretical ~5/s serial, parallelisable across its cards; SPECULATION past a single stream, flagged: the rack's concurrent-call behaviour is unmeasured, and the vision-language embed arms were still loading at last record). **Cadence verdict for Tier R: 0.5–1 Hz reflex perception per body at 16 bodies is plausible on measured judge latency, with the VL arm's throughput the named unknown.** Splat-nearby and flag-visible are classification-shaped problems; that shaping is what makes the rotation affordable.
- **Tier D costs bounded generation, and the bound is per syndicate, not per body.** A situation-picture update plus a play-selection decision is a short generation (~120 tokens, §4's unit) on a 10–30 s cycle *per syndicate* — because Tier D thinks for a crew, not for a citizen. Four syndicates at 16 bodies: 4 decision streams, one §4 "citizen's worth" each, on a slower clock than §4 assumed: aggregate ≈ 4 streams × 120 tok / 20 s ≈ 24 tok/s-equivalent of scheduling, against a planned aggregate capacity of ~24–32 tok/s (the same SPECULATION-flagged 3–4× batch figure). **Tier D at 16 bodies costs roughly what §4 priced for 4–8 individual minds** — the bodies stopped being the multiplier.
- **Tier L costs full LLM price per syndicate per round.** At pilot cadence (one ~40-minute round), four syndicates' reflections across an iteration phase are four large jobs with *minutes* to run in — the presence-brain class of work the Thor already does for one resident, times four, off-clock. No in-round capacity is touched. This is the tier the parent's arithmetic was silently charging *per second*; correctly charged per round, it is not a serving constraint at any cast size in §2.1's table.
- **Tier W costs nothing in serving.** It is a filing and review discipline.

**Revised conclusion (superseding §4.2's size table):** the concurrent form's serving gate moves from *decode throughput per citizen* to *Tier-D scheduler design + perception-rack concurrency*, both pilot-measurable. Concretely: **4 bodies — feasible now** (unchanged). **8 bodies — feasible with the captain-only escalation rule** (unchanged in verdict, changed in reasoning: the constraint is Tier-D streams, two syndicates' worth, well inside the envelope). **16 bodies — no longer gated on the missing decode measurement; gated instead on two measurements the pilot can actually take**: (a) rack concurrency under a 16-body reflex rotation, (b) Tier-D aggregate behaviour at 4 concurrent syndicate streams. If both measure inside the envelopes above, the full form is a scheduler project, not a hardware project — and the D3D quiet-window question (§4.2 option (c)) returns to being what it always was, a bench-governance decision, instead of this game's critical path. The asynchronous-syndicates fallback (§7) stays on file, demoted from "the honest expectation if serving fails" to a genuine alternative format (sequential rounds suit Tier-L-heavy play), retained because it is a good format, not because the concurrent form is expected to die.

What the tiered model does **not** rescue, honestly: Tier D's 120-token decision at ~8 tok/s single-stream still takes ~15 s of decode; if four syndicate streams collide on one actor server with no batching benefit, Tier D's 10–30 s cycle slips toward a minute and play selection lags the fight. The mitigation is architectural, not hopeful: stagger syndicate Tier-D clocks (they have no shared deadline — opponents are not synchronised), and let Tier R's scripts be good enough that a late Tier-D decision is a missed optimisation, never a standing-still citizen. The queue-as-visible-mechanic point of §3 survives in weakened form: a queued *body* was a defect the tiering eliminates; a queued *decision engine* is a tempo cost the opponent can exploit, which is — correctly — a game mechanic.

### A2.4 The reconciliation: paint + tiers = the spectator product

The two halves of Casey's direction are one design. The spectator (§1) watches RTS-like troops — Tier R bodies patrolling, hauling, holding posts — whose combat is *legible and silly*: huge splats, colour blooming across a square, a marked runner trailing pigment home. Underneath, the strategy is real and runs on the stack: reflex scripts execute, decision engines select plays, and between rounds the LLMs read the one artefact that shows the whole fight at once — **the colour-covered board itself**. The post-round paint census is Tier L's primary evidence: it is world state (surveyable, unwriteable by any actor's self-report), it is the fight's history in spatial form, and it is exactly the kind of record the triples discipline files. A season of paint censuses is a season of strategy made visible — the board remembers every round the way the ledger remembers every league night, except a person can *see* it. That is the product: a game whose surface is a cartoon and whose memory is a map.

*End of Addendum 2. The parent study's §§1–3, 5–7 stand as filed except where this addendum states a supersession (§3's escalation path — split at Tier D; §4.2's size table — revised at A2.3; §1's Long Night scenario — retired from this game at A2.1; §6's respawn-grind row — dissolved by construction at A2.1, its bench rule retained for the league proper).*

---

## Addendum 3 — 2026-11-08: The Production Shape

*Casey's standing orders, 2026-11-08 17:00 AKST, on how this programme is to be built: document well; build with the whole seat fleet, not only with orchestrating subagents; and use the bench depth to think about the right way to build it in many directions, running many experiments in rapid succession. This addendum records those orders as the programme's production shape. It designs nothing new about the game — it specifies who builds it, how the work is recorded, and how the programme exploits a domain whose trials are cheap, parallel and quickly judged. Where it touches the game at all, it is in service of Addendum 2's tiers: the tiers are built, variant-trialled and calibrated by the shape below.*

### A3.1 Documentation is part of the deliverable, not an afterthought

Per the fleet documentation doctrine (2026-10-26: "Document well as you go. The process means more than the product."): every lane in this programme writes its process record *in the body of its work, as it happens* — decisions and their reasons, dead ends, deviations, failures — not a summary reconstructed at the end, and not results with the story in an appendix. Applied here:

- Every programme artefact — playbook version, arena generation, paint-layer spike, round record — carries its own process note: what was tried, what the world evidence said, what changed because of it.
- A result without its process is a claim, not a record. This is the standard the studies shelf already enforces, and it binds seats and manager alike: a lane's deliverable is its receipts, not its summary of them.
- This addendum is itself an instance of the rule: the orders were filed inside the study they govern, on the day they were given, rather than left in chat where only context would hold them.

### A3.2 Production runs on the seat fleet

The programme is executed by the fleet's seats, with one rung added to the usual shape. The standing shape:

**Muse charters and verifies → a Claude Code manager seat orchestrates → ZCode / MCode seats execute in parallel → receipts flow back up, verified against world evidence.**

- **Charters and verification — Muse.** Muse writes the charters (scope, pre-registered criteria, stop lines), and owns verification: seat output is checked against the artefact itself and against world evidence, never against a seat's own summary. Deficits are reported first; wins are the expected baseline.
- **Manager seat — Claude Code (the new rung).** Claude Code can itself serve as the orchestrator of the other seats, and Casey uses it that way. The programme's default manager seat sits at the ProArt station; anywhere fits as the work demands. The manager decomposes a charter into seat-sized briefs, launches and minds the seats, collects their receipts and assembles the lane's deliverable. It does not grade its own lanes' work — verification stays with Muse, one level up, so the manager is managed.
- **Execution seats — ZCode and MCode.** Bulk building, bulk testing and thinking-in-directions are seat work: ZCode (GLM) and MCode (MiniMax) seats across the Thor, the Orin and the ProArt run the variants, the surveys, the re-reads and the first-pass builds in parallel, on prepaid subscriptions whose idle capacity is waste. Claude Code is additionally used occasionally, directly, for the levels of thinking beyond the other seats — it is both the manager option and the deep-thinking seat, not the everyday executor.

Seat discipline, from the fleet record, binding on every launch in this programme:

- `zcode -p` (print mode) is read-only Q&A — in that mode the seat cannot write files or execute commands. Unattended *builds* therefore need an interactive seat (the tmux seat pattern) or `--mode yolo`; a brief that ends with the agent explaining it cannot act is a launch failure to fix, not a result.
- MCode is TUI-only: it is driven through its tmux session and has no headless print mode.
- Claude Code headless (`claude -p` with an explicit `--allowedTools` list) *can* write, and is the route for seat work needing judgement plus hands.
- Briefs are delivered by `scp` with the byte count verified on the far side, *and* the brief's full text embedded in the launch prompt, so no lane depends on reading the file alone. An agent reporting an empty brief is a launch failure.
- Every seat is verified by its OUTPUT and its TAIL — files written, tests run, receipts filed — never by its launch echo or its ready line.

### A3.3 Bench depth is for thinking in many directions — and this domain rewards it

Casey's framing: the tools exist not just to build this quickly and test it, but to think about the right way to build it in many directions — and this is one of the domains where a lot of different things can be tried, in rapid succession, in many ways. The production shape exploits that deliberately — fork, don't block, at programme level:

- **Variant playbooks per tier.** A playbook is a filed text artefact; a variant costs a seat-hour, not a build. Each Tier-L revision cycle runs *several* candidate variants — different trigger surfaces, different escalation tables, different adjustment levels — into scratch rounds in parallel, and keeps the ones the world evidence favours. Tier D gets the same treatment: decision-rule variants (play-selection policies, re-planning thresholds) are trialled side by side against the same round record before any is adopted live. The adjustment level (Tier L's meta-parameter, A2.2) is tuned by experiment, not by intuition.
- **Rapid round cycles.** A paint round is short, non-lethal and fully receipted (A2.1): a failed trial costs minutes and leaves a paint census and a filed triple, not a damaged citizen. Trials therefore run in rapid succession with verdicts the same hour — the opposite economics of the league's survival lanes, where one bad night costs a season. The round cycle is the programme's experiment clock.
- **Per-street fidelity loops in parallel.** The Sitka twin's fidelity loops (sibling study, *The Street-View GAN*) are independent per street: several streets' generate → walk → judge → punch-list cycles run concurrently under different seats, each closing only on its own battery — and generation never outruns judging on any street (the sibling study's scaling law: never generate what we cannot judge).
- **Judge calibration as a repeatable cheap experiment.** The seeded-defect discrimination proof — plant a known-wrong building, verify the judges catch it — is a small, scripted, repeatable experiment. It is re-run whenever a judge panel, rubric or model changes, so the fidelity loop's eyes are re-proven by experiment rather than trusted by habit. The same pattern serves the game side: a seeded Tier-W change (an unannounced rule or board change in a scratch round) tests whether a syndicate's reflection tier detects that the period changed — the re-period reflex, calibrated like any other instrument.
- **What this discipline forbids:** serialising the programme behind one variant, one street or one stalled lane. A blocked item gets one line in the record and gates nothing; the other directions keep moving. Pruning the variant field is a decision made on evidence, after the trials — never a guess made before them.

*End of Addendum 3. The parent study and Addendum 2 stand as filed; this addendum governs how the programme is produced, not what the game is.*
