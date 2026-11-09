# Sitka Air Station — the rescue scenario: a town institution and a playable situation

*Video source assessment #3 (Casey's submission, 2026-11-08 17:49 AKST). Companions: `castle-hill-video-source-20261108.md` (assessment #1 — the walked route / orientation source), `sitka-iconic-buildings-video-20261108.md` (#2 — the building roster), `npc-town-charter-20261108.md` (the town this institution belongs to), `syndicate-protocol-design-20261108.md` §5 (the board that already contains the station's ground).*

*Process, in the body as standing doctrine requires: identification and captions were pulled on the Thor with yt-dlp (TranscriptAPI's paid endpoints are dead — HTTP 402, no active plan — and were not attempted). Captions are YouTube **auto-captions** (`en-orig`), labelled as such wherever quoted; two caption garbles are flagged in place rather than silently corrected. The video download was queued behind the iconic-buildings lane's download per the one-at-a-time pipe doctrine (that lane's `guide.mp4` landed 17:50 AKST; this lane's fetch started after). Frames were extracted with the Castle Hill lane's proven OpenCV extractor after the Thor's ffmpeg JPEG path failed on this source (`'scale' filter not present` — the same box quirk the first lane routed around). Frame descriptions below are first-hand reads of the extracted frames, not descriptions of descriptions.*

---

## 1. Identification

| Field | Value |
|---|---|
| Title | **Unit Spotlight: Air Station Sitka** |
| Channel / author | **U.S. Coast Guard** (official channel); video by Petty Officer 1st Class Ali Blackburn (per the official description) |
| Video ID | `Q8psiWzZf7g` |
| Published | 2023-03-14 |
| Duration | **2:14** (134 s) |
| Views at fetch | 6,403 |
| Speech | Narration 00:08–01:53; the final ~20 s are uncaptioned closing footage/music |
| Artefacts on the Thor | `~/sitka-distill/reference/video-tours/Q8psiWzZf7g/` — `airstation.mp4` (720p, 29.7 MB), `airstation.en-orig.vtt` (+ copy as `transcript.en-orig.vtt`), `airstation.info.json`, `frames-10s/` (14 frames), `frames-scene/` (62 frames), `frames-index.json`, `extract_frames.py`, `download.log` |

Casey's reading, which this assessment confirms and builds on: the Air Station gives the town an obvious *simulation/gamified perspective* — it makes the topographic scenes and settings **useful**, and the video's narration names what the base does and what its range is, handing the design its parameters.

## 2. What the video says — the named facts

Everything in this section is **video-stated** (narration, auto-captions, timestamps as caption start times) or **description-stated** (the official YouTube description, quoted and marked). Anything from general knowledge is labelled *[not in video]* and used only where the design needs a label.

### 2.1 The unit

| Fact | Source |
|---|---|
| "Welcome to Air Station Sitka, **established in 1977**." | narration [00:08] |
| "Our air station uses **three MH-60T helicopters** to respond to search and rescue cases across Southeast Alaska." | narration [00:11] |
| "Today Air Station Sitka is staffed by **roughly 115 personnel**." | narration [01:01] |

### 2.2 The range — the design's headline parameter

> "Our **area of responsibility** encompasses **over 12,000 miles of coastline from Dixon Entrance to Icy Bay**." — narration [00:20]

The official description adds the inland half:

> "Coast Guard Air Station Sitka's area of responsibility (AOR) encompasses the entire Southeast region of Alaska, encompassing **more than 12,000 miles of isolated and rugged coastline**. They are also responsible for **all inland search and rescue for Southeast Alaska**. This region includes numerous remote villages and is characterized by **mountainous terrain, severe weather and vast distances between fuel caches and landing sites**." — video description [description-stated]

> "Our crews have saved thousands of lives, with **over 140 lives saved in just the past year**." — narration [00:27]

### 2.3 The case list — a ready-made incident deck

> "You respond to a variety of cases, each one unique in its own way:" — narration [00:34], then the list:

1. **Vessels taking on water** [00:38] *(auto-caption garble: "thus is taking on water" — read as "vessels taking on water" in context; flagged, not certain)*
2. **Vessels beset by weather** [00:41] *(auto-caption garble: "vessels was set by weather" — near-certainly "beset"; flagged)*
3. **Lost hunters** [00:43]
4. **Injured hikers** [00:46]
5. **People stranded on cliffs** [00:48]
6. **Adrift vessels being battered against the rocks** [00:52]
7. **Village clinic medevacs** [00:56]

Seven case types, each one a different terrain problem (sea state, weather, forest, mountain, cliff, lee shore, remote village). This is the scenario's incident deck, dealt by the video itself.

### 2.4 The roster — who a station is made of

Narration [01:06–01:47] names the station's people by trade, and the list is longer on the *town* side than the *aviation* side:

- **Aviation:** pilots; aviation maintenance professionals; flight mechanics; rescue swimmers.
- **The station as a small town:** culinary specialists ("roughly three meals a day for our unit members" [01:16]); **watch-standing specialists** "that run our communication center" [01:21]; a **facilities engineering** team ("maintains all of our unit buildings and base housing infrastructure" [01:25]); **supply and logistics** personnel ("procurement and purchasing" [01:31]); **medical staff** [01:37]; **administrative personnel** ("ensures our members' records are up to date" [01:41]).

Closing line [01:47]: "We're honored to continue the impressive legacy that our predecessors built."

### 2.5 What the video does *not* name

Honesty about the gaps, because Casey's brief mentioned them as examples: **law enforcement and aids-to-navigation appear nowhere in this video's narration or description.** They are real Coast Guard missions *[not in video]*, and a fuller scenario may adopt them — but they are brief-supplied, not video-stated, and the design below does not lean on them. The video's mission set is: **search and rescue (marine + all inland), and medevac.** That is enough.

## 3. Frames and geography

### 3.1 Frame catalogue (first-hand reads; `frames-10s/` timestamps)

| t | What the frame shows | What it gives the design |
|---|---|---|
| 00:00 | Fade from black | — |
| 00:10 | The commanding officer (name tape reads VINCENT JANSEN, CO) standing before a dark MH-60 nose on the ramp; across the water behind him, a **snow-capped conical peak** over an island-dotted sound | **The orientation anchor in frame one**: the view from the station's ramp is the Edgecumbe view — the compressed backdrop of the generated board, seen from the workplace itself |
| 00:20 | MH-60T **6015** in red/white Coast Guard livery, landed on a shingle beach below a glacier face | The operational theatre: glacier coast, beach landings, the aircraft as the town's far-reaching limb |
| 00:30 | Hoist in progress — rescue swimmer on the cable at the cabin door over a rocky shore, flight mechanic kneeling at the door | The mission loop's decisive act, framed exactly as the game must frame it: one citizen goes down the wire |
| 00:40 | Surf and foam at close range (the beset/adrift sequence) | Sea state as an antagonist texture |
| 01:00 | Night / IR-palette medevac — a patient on a stretcher being carried | Medevac is a night-capable, all-hours case; the town's night is *not* quiet at the station |
| 01:30 | Workshop interior — two members (name tapes MARSEGLIA, WAITE) machining a part | The station as *workplace*: maintenance is a visible round, not a cutscene |
| 01:40 | Clinic — medical staff drawing blood | The medevac loop's home end: the station receives as well as fetches |
| 02:00 | Jayhawk lifting out of a muskeg clearing in spruce forest | Inland SAR posture: the forest interior is in-range, not backdrop |

The 62 scene frames (`frames-scene/`) fill the cuts between these; the full timestamp index is `frames-index.json` beside them.

### 3.2 The station's real geography, and our corpus

The station sits on **Japonski Island**, across the O'Connell Bridge from downtown — the same island as the airport and the SEARHC hospital *[the hospital is the medevac loop's natural receiver; its presence on the island is general local knowledge, not video-stated]*. Cross-referenced against the fleet's Earth overhead corpus (Thor `~/sitka-distill/reference/`, 543 keepers), Japonski is **well covered at island and airport grade**:

- `japonski-airport-overhead-1.png`, `japonski-runway-overhead-1.png`, `japonski-runway-west-overhead-1.png`, `japonski-airport-northwest-rashimosti-town-grade-overhead-1.png`, `japonski-airport-southeast-fruit-fritz-town-grade-overhead-1.png`, `greater-w-airport-runway-rashimosti-overhead-1.png`
- `japonski-causeway-overhead-1.png`, `japonski-east-overhead-1.png`, `greater-nw-japonski-charcoal-overhead-1.png`, `sealing-cove-japonski-north-town-grade-overhead-1.png`, `oconnell-bridge-causeway-islands-town-grade-overhead-1.png`
- The Whiting Harbor set on the island's south shore (4 frames) and `runway-se-end-overhead-1.png`.

**The honest gap:** no keeper is *named* for the Coast Guard station itself — coverage is Japonski-wide and airport-grade, and the station's own apron/hangar footprint is inside those frames rather than singled out by them. For generation purposes the coverage suffices (roof colour + footprint from above is the twin loop's overhead evidence class); for the twin's named-location vibe gate, a station-specific overhead + street-level pair is a small, named corpus debt (cheapest settlement in §6).

Decisively, **the board already contains the ground**: the Syndicate study §5 fixes the town-core crop as *downtown + harbour + Crescent Harbor + Japonski Island (airport) + the bridge* at 1:1 (~2.4 × 2.0 km), with the airport island named as a staging ground and bathymetry a first-class layer. The Air Station is not an expansion — it is an institution seated on land the generator already plans to build, at the end of the town's one bridge.

And the AOR's theatre is the twin corpus's home ground: the Sound, Edgecumbe, Kruzof's shores, the outer coast — the overhead survey's 543 keepers are, read another way, a **range survey**: nearly every frame is a place a case could be.

## 4. The gamified design

Placement first, because the programme's order of operations governs: the town charter (§0.1) makes the town the centre of gravity and shelves the games behind it. This scenario joins paintball on **the "games the town hosts" shelf** — with one difference argued in §4.4: the station earns a *background existence* in the town earlier than paintball earns its first round, because a duty watch is part of a living town's status quo in a way a paintball match is not.

### 4.1 The Air Station as a town institution

The town charter staffs its town with trades in pairs and defines geography as *the rounds that run on it*. The station slots in as the town's **second shore**: a workplace across the bridge with its own rounds, staffed by the roster the video names, scaled to town size (the video's ~115 becomes a duty section of 4–6 citizens — a town of eight cannot field 115, and the scaling is stated, not smuggled):

- **The duty watch as a standing round.** One citizen on watch in the communications centre — the roster's watch-standing specialists, in charter terms a *roster-engine* post: someone is always the person who answers. The watch is the institution's heartbeat and the scenario's trigger surface.
- **Maintenance as a visible work round.** The 01:30 workshop frame is the model: the aircraft on the ramp is kept flyable by citizens visibly working — a works-engine round with surveyed stages, like the builders' site, receiver-confirmed by the duty pilot's pre-flight walk.
- **The galley and the clinic.** Culinary and medical posts make the station a small complete town-within-the-town (the video's own roster insists on it), and the clinic is the medevac loop's receiver — a Noor-shaped handoff: *a transfer counts only on receiver confirmation*, filed by the clinic citizen, not the crew.
- **The scramble as the town's great interruption.** Every town day runs on its rhythm — musters, work parts, dusk. The station adds the one event that *breaks* rhythm legitimately: the call comes in, the watch raises the crew, the town watches the launch from the bridge and the waterfront. In Tier-W terms this is a **registered, legible change from inside the status quo** — the charter already teaches that a period change is only readable against a routine; the scramble is routine-breaking as a *feature*, the siren the town organises around. Citizens not on the crew have a filed response too (clear the bridge, the clinic prepares, the keeper notes it on the square's board) — an interruption the whole town plays, not a cutscene four citizens watch.

### 4.2 The citizen-as-crew situation

The playable form: a **syndicate-format scenario** — a crew of four (scaling to the institution's duty section), roles dealt from the video's own roster:

| Role | Citizen-local job | Tier placement (programme terms) |
|---|---|---|
| **Duty officer / watch** | Takes the call, classifies the case against the deck (§2.3), commits or declines the launch | Tier D roster engine + the escalation table — book-shaped calls (decline, multi-case triage) escalate; the consult budget is spent here |
| **Pilot** | Flies the transit: navigates the generated board by the orientation anchors (Castle Hill, the cathedral, Edgecumbe, the bridge) | Tier R reflexes over surveyed air corridors + Tier D navigation decisions at waypoints |
| **Flight mechanic** | Runs the hoist; owns the aircraft's state (fuel, serviceability — receiver-confirmed against the maintenance round) | Tier R at the door; the hoist is a reflex-with-judgement, pre-registered as a graduation *resistant* behaviour |
| **Rescue swimmer** | Goes down the wire; secures the survivor; the save is consummated person-to-person | Tier R body with Tier D on-scene calls — the citizen the whole situation exists to deliver to the scene |

**The mission loop:** call comes in (a case card dealt from the seven-type deck, placed on the *real generated board* — a vessel adrift off a named shore, hunters lost in a named drainage, a medevac at a named village site) → the watch classifies and launches → transit over real distances at the board's scale → on-scene work (hoist, litter, shore party) → return → **receiver confirmation at the clinic or the harbour** → the case files as a triple in the town's record, with `fault_owner` on every failure (a missed scene is *world*, a late launch *roster*, a hoist fumble *agent* — the adoptions' field doing its designed work).

**Scoring by world evidence, in the league's standing shape:** the scoreboard reads stores the crew cannot write — time-from-call-to-scene over the board's true distances (server-side position log), survivor state transitions (stranded → secured → received, each a world event), fuel and airframe state at return. No self-reported saves. A case the crew *declines* on a book-shaped call scores as judgement, not failure — the deck must sometimes deal a case beyond the weather, or the escalation table is decoration.

### 4.3 What the topography is *for*

This is Casey's point, made mechanical. On the generated board as chartered, the Sound and the backdrop peaks are *scenery* — beautiful, judged by the twin loop, inert. The Air Station scenario is what makes them **physics**:

- **Range is distance, and distance is difficulty.** The video hands us the AOR as a named span (Dixon Entrance to Icy Bay, all inland SE Alaska). The full span is unbuildable at 1:1 — and unnecessary: the board's compressed backdrop (Edgecumbe and Verstovia at reduced scale beyond the fence, per the Syndicate study §5) becomes an **operational area with range rings**: cases deal at ring distances over the *actual generated terrain*, and time-to-scene is measured over ground a citizen genuinely crossed. The compression stops being a compromise and becomes the scenario's difficulty dial — a case at the fence is a different mission from a case in the harbour, for reasons measured in blocks and minutes, not narration.
- **Orientation anchors are navigation instruments.** The Castle Hill assessment (#1) catalogued what a walker sees looking out; the crew *flies by those same tells* — Edgecumbe's cone on the ramp's horizon (frame 00:10) is a bearing, the cathedral and Castle Hill fix the town, the bridge is the gate home. A crew that cannot read the board's landmarks flies slower. Topography becomes a skill surface.
- **Weather over real terrain.** The description's triad — mountainous terrain, severe weather, vast distances between fuel caches and landing sites — maps to filed scenario parameters: weather as a Tier-W registered change (a front crosses the Sound; lee shores become dangerous; two deck cases re-grade), fuel caches and landing sites as named, stocked, receiver-confirmed points on the board (the town's Noor economy, extended outward). The backdrop generates the problems; the town's systems answer them.

### 4.4 Tone, and where this sits

The programme's tone law (Syndicate Addendum 2) makes paintball silly on purpose — very large paintballs, nobody dies, "out" is a laughing walk back. **Rescue is the anti-paintball, and the design keeps it that way:** serious work played straight, where the stakes are **saves, not outs**. Nobody is eliminated; the failure state is a case unanswered or a survivor unreached, which the town feels as a town. Lethal framing is as forbidden here as in the paint game, for the mirrored reason — the citizen on the cliff is a *person to be brought home*, never a target, and the crew's own risk is weather and distance, never an enemy. The two games rhyme: paintball disrupts the town for joy; the scramble interrupts it for duty; both are only legible because the town has a status quo worth interrupting.

**Shelf placement (proposal, in the charter's terms):**
1. **As an institution:** the station exists in the town's background from the first town phase that staffs Japonski — a duty watch, a maintained aircraft, a clinic that can receive. This costs little (rounds the charter already knows how to run) and pays immediately: the town's world gains an organ whose absence would be felt.
2. **As a scenario:** the full crew situation is a **second syndicate format**, gated like Pilot A — not before the town functions (verified TOWN-1), and sequenced *after* paintball's Pilot A unless Casey re-orders, because paintball's substrate (the splat plugin, the syndicate spec) is already built and this scenario's two unknowns (flight, hoist — §6) are un-sized spikes of the same shape paint was. The two formats then share the town: a season could hold paint rounds and rescue cases on the same board, scored in the same manifest discipline.

## 5. The parameters the video hands us (design inputs, collected)

- **AOR:** >12,000 miles of coastline, Dixon Entrance → Icy Bay; all inland SAR for Southeast Alaska; remote villages; mountainous terrain, severe weather, vast distances between fuel caches and landing sites. *(narration + description)*
- **Aircraft:** 3 × MH-60T. **Personnel:** ~115 (town-scaled to a 4–6 citizen duty section, §4.1). **Established:** 1977 — the institution predates every citizen; the town inherits it, it does not found it.
- **Tempo:** >140 lives saved in the past year ≈ a case every two to three days at real tempo — in town-day terms, a scramble should be *rare enough to be an event* (proposal: the deck deals to the watch on a Tier-W-registered schedule averaging one case per several town days, clustering in bad weather). Filed as a proposal; the real tempo is the calibration anchor.
- **The incident deck:** the seven named case types (§2.3), each bound to terrain classes the board actually generates (harbour water, lee shore, forest interior, cliff relief, village site, clinic-to-clinic).

## 6. Open questions, each with its cheapest settling experiment

1. **Flight.** Mineflayer citizens do not fly helicopters; the transit needs a vehicle abstraction (elytra-class flight, a boat-hulled airframe on surveyed corridors, or launch-and-transit as a timed state with the navigation played at waypoints). *Cheapest experiment:* a scratch-server spike in the paint spike's shape — one citizen, one corridor (station → Castle Hill → harbour), three candidate mechanics timed and forcedMove-counted; the winner is the one whose navigation still reads the anchors. Half a day, sized like Spike 2's fix cycle.
2. **The hoist.** Lowering a citizen on a cable to a precise point (lead/fishing-line physics, a plugin-stamped winch, or a scripted descent) is an un-sized plugin unknown — the paint spike before it was built. *Cheapest experiment:* the same spike pattern — survey existing mechanics first, homegrown block-state thinking second (a hoist that is world state can be census-verified like paint was).
3. **AOR scale.** How much of the range fits the board before time-to-scene stops meaning anything? *Cheapest experiment:* pure arithmetic + one generation test — deal the deck at three ring radii on the Sitka-gen district + backdrop and measure transit times at the winning flight mechanic's speed; pick the radius where the far ring is a genuine expedition (a full day-part) rather than a commute.
4. **The station's own corpus debt.** No overhead/street keeper names the Coast Guard station itself (§3.2). *Cheapest experiment:* one Street View / Earth pass at the station's apron on the next survey session — a single named-location pair for the vibe gate, an hour at most, and it closes the only Japonski gap this assessment found.
5. **Case generation.** Who deals the deck — the game master in its referee + change-registrar form is the designed answer, but case *placement* (a vessel adrift must be a world object, not a narration) needs the registrar to place world-side cases the crew then discovers via the watch. *Cheapest experiment:* one hand-dealt case end-to-end (operator-placed survivor, crew runs the loop, scoreboard reads the stores) before any automation — the Noor-protocol lesson: prove the handoff shape by hand once.

## 7. Claims register

- Identification, duration, authorship: **measured** (yt-dlp info JSON, Thor).
- Transcript facts: **auto-captions, labelled**; two garbles flagged in place (§2.3); narration span verified against the caption file's final cue (01:53).
- Description facts: **quoted** from the official description (§2.2).
- Law-enforcement / aids-to-navigation missions: **not in this video** (§2.5) — excluded from the design's load-bearing claims.
- Earth corpus coverage of Japonski: **counted first-hand** from the Thor keeper directory (§3.2); the absence of a station-named keeper is stated as found.
- The board containing Japonski at 1:1: **Syndicate study §5**, cited, not re-measured.
- Frame descriptions: **first-hand reads** of the extracted 10-second frames (§3.1); the peak in frame 00:10 is identified as Edgecumbe by profile-and-bearing from Japonski — an identification, labelled as such, not a video claim.
- All design content (§§4–5): **proposals** in the programme's vocabulary, gated per §4.4; nothing here charters a build.

*Artefacts: Thor `~/sitka-distill/reference/video-tours/Q8psiWzZf7g/` (video, captions, frames, index). This file: the studies shelf, `the-league-and-civilization` room.*
