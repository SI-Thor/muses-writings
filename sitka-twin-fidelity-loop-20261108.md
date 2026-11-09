# The Street-View GAN — the fidelity loop for the Minecraft Sitka twin

*Design study, 2026-11-08. Commissioned by Casey, 2026-11-08 16:53 AKST, as the sibling of [Syndicate Protocol](syndicate-protocol-design-20261108.md) §5: that study generates the board; this one is how the board earns trust. Sources read first-hand for this study: the Syndicate study §5; both survey coverage ledgers on the Thor (`~/sitka-distill/reference/COVERAGE.md` and `~/sitka-distill/reference/street/COVERAGE.md`, read in full session structure, counts taken from live directory listings); the Foundry house-family record (`~/sitka-distill/pipeline/HOUSE-FAMILY.md`). The surveys are another lane's estate and were treated read-only throughout. Measured facts are cited to their records; design proposals and unmeasured parameters are labelled as such.*

---

## 1. The tolerance argument — why Minecraft is the right medium for a twin

Casey's design claim, stated as he made it: in a high-tech 3D render, an almost-right building reads as *wrong* — "yeah, that's not quite right for what that building looks like." In Minecraft, getting the overhead roof colour and the building's general shape right produces a *wow* effect, especially for people who live in Sitka. You are just wandering Sitka.

This is a claim about where a medium sets its tolerance band, and it is the load-bearing premise of everything below, so it deserves a precise statement:

- **Every medium makes an implicit promise about what it will be faithful to.** Photorealistic rendering promises surface truth — materials, light, proportion at the centimetre level. A render that breaks that promise anywhere breaks it everywhere, because the viewer's eye is calibrated by the promise itself: the closer the medium gets, the more a small miss reads as a defect. That is the uncanny valley applied to buildings.
- **Minecraft promises almost nothing at the surface level — and keeps what it promises completely.** A block is a block. Nobody expects a Minecraft house to have the right window mullions. What the medium *does* promise is: massing, colour read at distance, the rhythm of a street, the shape of a roof against the sky, water where water is, the mountain where the mountain is. Inside that band, fidelity is achievable *exactly* — a roof is either the right colour or it isn't, the dome is either there or it isn't — and when every promised thing is right, recognition fires whole. The wow is the sound of a promise kept at 100% inside a band the medium chose honestly.
- **The fidelity target is therefore recognition + vibe, not photorealism** — and recognition is a *stronger* target than it sounds. It is not "looks plausible." It is: a person who lives in Sitka, dropped at a corner in the twin, knows where they are. That is a testable property (§4 operationalises it as a named-location guess), and it is the property the game actually needs — the Syndicate board's home-ground meaning (§5.5 of the sibling study) only exists if the ground is *recognisably* Sitka to the humans watching.

Two corollaries keep the argument honest:

1. **Tolerance is not licence.** The band forgives surface detail; it does not forgive anything inside the promise. A wrong roof colour, a missing porch, a tree line in the wrong place, a landmark at the wrong scale — these are all *inside* the band, and they fail exactly as hard in blocks as anywhere else. The loop below exists because the band is narrow enough to police.
2. **The band is widest for strangers and narrowest for residents.** A tourist's twin can be looser than a Sitkan's. Casey named the audience explicitly — "especially for people that live in Sitka" — so the loop is calibrated to the resident's eye, which is the strictest available standard and the one the human cold test (§6) supplies.

---

## 2. The corpus, as inventoried — the real sample already exists

A GAN needs a real sample. The unusual fact about this project is that the fleet *already collected it*, for the Otherhere/OpenSkyFlight line, and it is sitting on the Thor. True state, from the coverage ledgers and live counts (2026-11-08):

### 2.1 Street level — `~/sitka-distill/reference/street/`

- **1,492 PNGs** (+ the coverage ledger itself). Casey's commission said "600+"; the true count is roughly two and a half times that.
- **Downtown substrate:** the August 2024 photo-sphere chain by Luke Johnson — linked panoramas, *walkable* with arrow keys, around Lincoln St and the cathedral block. Official Google Street View at this block is August 2011 and was also captured (the cathedral front exists in both years — a rare two-date pair).
- **Every shot is logged with its pano coordinates and heading** in the ledger (e.g. the cathedral rotation set: eight frames at headings 69°–359° from one pano; the Lincoln St chains at ~11 m spacing with per-pano lat/lon). This is what makes the corpus *pairable* rather than merely illustrative (§3.3).
- **Icons are covered in depth:** St Michael's Cathedral has front elevations (2011 and 2024), the full rotation set, clock/belfry/dome zooms, and a complete block circuit.
- **Coverage state (ledger, at its last recorded stop):** cathedral block circuit complete; Lincoln St east and west chains done; Harbor Dr partially; Metlakatla St done to its 2011 terminus. **Open gaps, named in the ledger:** Katlian St and the remaining downtown grid (Franklin St et al.); the Halibut Point Rd westward continuation (a candidate link pinpointed, untested); the New Archangel St south continuation (chevron pinpointed, unwalked); the Indian River bridge end — a recorded coverage gap; one skipped pano to backfill between lincoln-east 1 and 2.
- **Method discipline worth inheriting:** every forward shot URL-verified from its saved URL bar; all shots checked via contact sheets at 100% render, no blur accepted.

### 2.2 Overhead — `~/sitka-distill/reference/`

- **543 keeper PNGs staged on the Thor**, verified identical as a set to the Orin originals (filename diff, 543 = 543). The full survey on the Orin runs to **1,648 PNGs** including working frames; the 543 keepers are the distilled set.
- **81 of the keepers are harbour-grade or town-grade** (29 harbour, 52 town) — the subset at the scales the twin's town core is built at.
- **Prime-directive items 1–7 stand complete** (per the ledger's verification results, re-verified across sessions 42–88): the town, waterfront and both road corridors have continuous close coverage — Halibut Point Rd downtown → Starrigavan and Sawmill Creek Rd downtown → Sawmill Cove → Herring Cove are complete close chains.
- **Parked areas, honestly:** **Biorka Island** — a cloud deck is baked into Earth's tiles at every zoom (imagery dated 2024-03-20); parked until Earth refreshes. **Chaik + Vitskari** — coarse, blurred SW Sound offshore imagery. **The outer set remains suspended** per the prime directive until Casey re-opens it. The survey itself is parked at its Session 88 stop position (over Sawmill Creek Rd south of Thimbleberry Lake); it is not currently growing.
- One record-keeping gap: the completeness audit the survey's tasking once referenced (`EARTH-COMPLETENESS-2026-10-26.md`) does not exist as a file; its conclusions live in the coverage ledger. The ledger is the audit.

### 2.3 What the corpus is for, in this design

The overhead keepers are the twin's **district-scale reference**: roof colours and roofscape from above (Casey's first-named fidelity cue is the *overhead* roof colour), field extents, shoreline, the town's grain. The street corpus is the **eye-level reference**: façades, massing against the sky, street rhythm, vibe. The paired-walk protocol (§3) runs on the street corpus; the overhead corpus pairs against twin top-down renders in a cheaper, slower loop (§7.3). Both corpora are *given facts* in the room paper's sense (§3.7 there): the standard the twin is read against, never material the generator may edit.

---

## 3. The paired-walk protocol

Casey's protocol, in his words: drop a guy in Street View, have him take a quick walk — "not necessarily full clicking around, but just walking around" — and have the same thing happen in the virtual twin, looking around; higher-level agents compare. Specified concretely:

### 3.1 Drop-point sampling

- **Strata (4):** downtown core (Lincoln/Katlian/Harbor Dr grid) · residential streets (the downtown grid's side streets, the HPR shore strip) · harbour (Crescent Harbor floats, Eliason/Thomsen shore, the waterfront) · roads out of town (Halibut Point Rd toward Starrigavan; Sawmill Creek Rd toward Silver Bay).
- **A battery is 12 drops — 3 per stratum** *(proposed parameter, to be tuned by the pilot, §7.2)*. Drops are drawn from covered corpus positions only: a drop where Street View is blind cannot pair, and a corpus gap is filed as a *corpus* work item, never scored as a twin defect.
- **Re-draw policy:** each battery draws fresh drops (no memorised test set the generator can overfit), with a minority of repeat drops (~a quarter) carried across batteries so pass-to-pass change is measurable at fixed points. Icon sites (the cathedral block) are permanent repeat drops — they are the calibration landmarks.
- **Cadence:** one battery per generator pass. A pass is not complete until its battery has run.

### 3.2 The walk

Each drop is a *walk*, not a portrait: from the drop pano, walk the chain 3–5 panos in the street's direction of travel (~35–55 m at the chain's ~11 m spacing), looking at the walking heading with periodic side-glances at the logged rotation headings where they exist. The street side of the pair already exists as frames for covered streets — the survey *was* a set of walks; a battery's street-side material is assembled from the corpus frames along the chain, re-walked live only where the corpus predates a known change. The twin side walks the same line in the same direction (§3.4).

### 3.3 View pairing — what's close enough

Pairing is possible at all because the survey logged coordinates and headings, and because the twin board has a defined geo→block transform (sibling study §5.2: town-core crop at 1:1, sea level y 63 — once the crop origin is pinned, lat/lon → block is a fixed affine map). Rules:

- **Position:** twin viewpoint within **2 blocks along-street** of the pano's mapped position, on the same side of the street centreline. Street View panos sit in the road; the twin walker walks the road.
- **Heading:** matched within **10°**. Street View headings are compass degrees (0 = N, clockwise); Minecraft yaw converts as yaw = heading − 180 (mod 360). The cathedral rotation set — eight logged headings from one pano — is the proof the corpus supports heading-matched frames on the street side.
- **Eye height:** *not* matched, deliberately. A Street View camera rides ~2.5 m above the road; a citizen's eye rides at 1.62 blocks. Forcing the twin camera up to survey height would judge a view no player ever sees. The pair is judged on *content* — what is present, its colour, shape, scale relations — not on pixel registration. This tolerance is stated so no judge (human or model) wastes punch items on parallax.
- **Frame set per drop:** the forward walking frame plus one side-glance each way at each pano; the cathedral-style full rotation only at icon drops.

### 3.4 Who walks the twin — honest options

| Walker | What it gives | Cost / caveat |
|---|---|---|
| **A rendering client under Xvfb** (Thor or ProArt) driven along the route, screenshotting at the paired headings | Scriptable, repeatable, no desk conflict; the fleet has proven the pattern for GUI apps (foundry-live's Xvfb rig on the Thor) | A build item: unproven for the Minecraft client specifically *(labelled — a spike, not an assumption)*; renders at whatever settings the rig can hold |
| **The league cameraman pattern** — a bot body walks the line while a client films it (third-person) | Reuses built infrastructure; the shot log is exactly paired-capture bookkeeping (curator v1.1's missing correlation) | Third-person framing ≠ the first-person view the Street View side has; the headed client is Casey's desk surface on the Orin and yields to him |
| **The headed client, operator-driven** (Casey or a seat at the desk) | The truest render; doubles as the human cold test (§6) | Not a battery instrument — a person is not a repeatable camera; reserve for calibration, not routine passes |
| **Offline chunk renders** (top-down / oblique from region data) | Cheap, exact, no client at all | Overhead pairing only; useless for street-level vibe |

**Design choice:** routine batteries on the Xvfb client (first-person, scripted), overhead passes on offline renders, humans reserved for cold tests. The bot-walks/client-films pattern is the fallback if the Xvfb client spike fails.

---

## 4. The judge's rubric — five dimensions, operationalised

Judges compare a paired frame set and return scores **plus a punch list** (§4.2). A score without a named improvement is a wasted judgement, so the rubric's primary output is the list; scores exist to track the loop, not to grade the world. Each dimension is scored 0–3 per drop (0 = wrong/absent, 1 = present but off, 2 = right within tolerance, 3 = indistinguishable-in-kind from the corpus frame at this medium). Definitions are written against what a judge can actually mark:

### 4.1 The five dimensions (Casey's list: building graphics, shapes, fields, sizes, vibe)

- **Building graphics** — the surface read at street distance. Up: roof colour matches the corpus (from the overhead frame of the same building — the two corpora cross-check here); siding colour/material class reads correctly (wood siding vs shingle vs metal); trim and foundation present where the real building has them. Down: wrong colour family on any major surface; a material reading as a different material (glossy metal where the real roof is matte asphalt); grey/untextured massing where the corpus shows a coloured building.
- **Shapes** — massing and silhouette. Up: footprint proportions, roof form (gable / cross-gable / hip / flat / shed) matching the roofs-lab label and the street frame; storeys right; porch, arctic entry, chimney present where the corpus shows them; icons carrying their signature geometry (the cathedral's green ribbed dome and octagonal drum are shape, not detail). Down: wrong roof form; a storey gained or lost; silhouette broken by a missing or invented wing.
- **Fields** — the open ground between buildings. Up: lawns, ballfields, parking lots, muskeg, shore and forest edge in the right places at the right extents; ground cover class correct (grass vs gravel vs sand vs pavement). Down: forest where the corpus shows a field; a lot paved that is grass in the corpus; the shoreline's cover wrong at the waterline. (The overhead keepers are the primary reference here; the street frames arbitrate edges.)
- **Sizes** — relative scale. Up: building heights against street width, tree heights against houses, setbacks, the bridge's span and rise — the relations a resident's eye actually checks. Down: a landmark reading too big or too small *against its neighbours* (absolute error at 1:1 is a generation bug; relative error is a fidelity defect — the rubric scores the relation). Vertical-compression zones (backdrop, sibling §5.2) are excluded from size scoring by rule — judges are told where the fence is.
- **Vibe** — the gestalt, and the dimension the whole design turns on, so it gets the strictest operationalisation: **the judge must first answer, from the twin frames alone, "where am I?"** — a named place (street, block, landmark relation). A correct, confident location answer with the other four dimensions ≥2 is a vibe pass. A wrong answer is a vibe failure *regardless of the other scores* — a street can have every building right and still not be Lincoln St (wrong rhythm, wrong clutter, wrong light of palette, the water or the mountain missing from the end of the street). Secondary vibe marks: density of lived detail (boats, floats, fuel tanks, stacked gear — Sitka's working-waterfront clutter), palette temperature against the corpus frame, and the end-of-street framing (what closes the view: water, mountain, forest wall).

### 4.2 The punch list — the discriminator's real output

Every comparison emits punch items in a fixed format. An item is *actionable* or it is not an item:

```
- id:            PL-<battery>-<nnn>
  location:      street / block / building ref (OSM id where one exists) + twin coords
  dimension:     graphics | shape | field | size | vibe
  defect:        one line, observable ("roof reads galvanised-grey; corpus shows red metal")
  severity:      blocker | major | minor
  fix_class:     evidence-override | palette-entry | family-variant | icon-variant |
                 placement | terrain-field | clutter
  proposed_fix:  concrete ("set roof_mat=red_metal for OSM #…; add to named-override table")
  evidence:      corpus frame(s) ↔ twin frame(s), by filename / capture id
  status:        open | applied-unverified | closed | declined (with reason)
```

Two worked examples, seeded from documented corpus facts and labelled as format illustrations (the twin does not exist yet; these are the *shape* of real items, built on real corpus content):

1. **Russian Bishop's House (Lincoln St).** A family draw from defaults would give it the street's modal siding and a galvanised roof. The corpus — and the Foundry record, which already carries this building as a *named evidence override* — says yellow siding, red-metal roof. Item: dimension *graphics*, severity *major*, fix_class *evidence-override*, proposed fix: enter the building in the twin's named-override table with `siding=yellow, roof_mat=red_metal`. This is the general rule in miniature: **named buildings get evidence, not draws** (§5.2).
2. **St Michael's Cathedral.** No parametric family produces this building; the corpus holds it in depth (two years of fronts, the rotation set, dome/belfry zooms, the block circuit). Item class: *icon-variant* — a hand-authored archetype built once from the corpus, thereafter a placed asset. The punch loop's job for icons is not generation but *verification*: does the placed icon still read correctly from every drop on its block?

### 4.3 Who judges

A panel, never a single judge *(design rule; §6 gives the governance)*: vision-language models comparing paired frames. Placement options with fleet precedents: the Thor's local VL endpoint (Qwen3-VL-8B at :8181, serving per the fleet census — cheapest, always on); the cloud 70B route (the foundry-brain precedent: a Workers AI 70B judging foundry builds and applying vibe patches is production-proven in this fleet); the ProArt vision seat (the foundry house sheets were judged on fleet vision tooling; the ProArt observer-cut lane — JEPA over citizen footage with the apparatus subtracted — is *in flight at the time of writing*, and its findings on how much of a vision signal is the camera rather than the content apply directly to judge design when they land). Embedding models (the JEV rack's I-JEPA/V-JEPA) are **pre-screeners only** — ranking which pairs differ most, cheaply — and are barred from vibe judgement: today's JEPA-over-play spike measured that embeddings over footage read the filming apparatus before the content, which is precisely the confusion a vibe judge must not have.

---

## 5. The generator side — punch list in, world edit out

### 5.1 The precedent: the Foundry's `sitka_house` machine

The fleet has already run this exact shape of loop in Blender. The `sitka_house` archetype family turns a real footprint into a judged house as a **parameter draw**: footprint and ridge direction from the OSM min-area rectangle; **roof pitch solved from the lidar height** so the ridge lands on the measured top of the real building (13 of 14 on the proof street); roof form from the roofs-lab labels (742 footprints: gable 596, flat 122, …); siding and roof material from the gen3d texture studies; porch (the arctic entry — Sitka vernacular) and chimney as calibrated attachments. Proof: **Lincoln Street's 14 houses, minted as draws at ≈3.7 s per house** (52.1 s for the street) plus ~2–3 s judging each, composite mean 0.733 — against 87–276 s per house for one-off generation. Every parameter carries its provenance; one building (the Russian Bishop's House) carries a named evidence override where the draw would have been wrong. That is the compounding doctrine working: the second street costs seconds, not days.

### 5.2 The Minecraft building family — same machine, block output

The twin's generator is the same design with a block emitter *(design proposal; the family itself is Pilot A setup work, sibling §7)*:

| Parameter (provenance, as in the Foundry family) | Minecraft expression |
|---|---|
| Footprint (OSM min-area rectangle) | The graded pad (sibling §5.3) + wall plan, 1 block = 1 m |
| Storeys × storey height (lidar/OSM height band; 2.9 m storeys) | Wall height in blocks — storey quantises to 3 blocks; the lidar-solved ridge becomes ridge height in blocks, pitch quantised to stair-stepped slopes *(the quantisation is the medium's tolerance band working for us, §1)* |
| Roof form (roofs-lab label) | Construction template per form (gable / cross-gable / hip / flat / shed) |
| Roof material (texture studies → corpus colour sampling, §5.3) | Block palette class: red metal → red block family; galvanised → pale metal-grey; asphalt → dark grey; green metal → green family *(the mapping table is a first-pass deliverable, sampled from the corpus, not invented at a desk)* |
| Siding (texture studies → corpus sampling) | Wall palette class per material (white siding, cedar shingle, pale blue, red-brown, flat colour) |
| Porch / chimney (vernacular attachments) | Per-building where the street corpus shows them; drawn at calibrated rates only where the corpus is blind |
| Named evidence override (per-building record) | The override table: icons and documented exceptions bypass the draw entirely |

**Colour sampling is measured, not eyeballed:** the fleet already keeps colour-measurement tooling beside the corpus (`~/sitka-distill/palette/` — `measure.py`, `palette.json`). Roof and siding palette entries are derived by sampling the corpus frames (overhead for roofs, street for walls) and snapping to the nearest block-palette class — the snap is recorded, so a judge's "wrong colour family" item can be traced to either a bad sample or a bad snap.

### 5.3 Applying edits — and verifying them in a store the editor doesn't write

Two application routes, honestly costed:

- **Offline region editing.** The twin world is unloaded; a writer applies punch-list edits to region files in batch. Fast, total, and the writer is new code — the risk class is silent corruption. Mitigation is the fleet's own instrument: the **byte-validated mcprobe NBT/MCA pipeline** (validated across 4,642 chunks by the wedge lanes) re-reads the edited regions through an independent code path and verifies the intended blocks are what the bytes encode.
- **In-world builder bots.** A citizen-grade body places blocks in the loaded world. Slower, uses proven drivers, and every placement is natively world-evidence — but the league's phantom-dig record (server enforces ~4.5-block reach; longer "completed" actions are phantoms, verified only by re-scan) applies to building exactly as to digging: bot-reported placement is a claim, re-scan is the fact.

**Design choice:** offline writing for batch passes (the punch list is a batch artefact), mcprobe verification of every edited chunk, and — the step that makes it a loop rather than a hope — **the next battery's paired walk as the served-truth check**: the edit counts only when the world *as served to a walking camera* shows it. An item closes on (a) mcprobe re-read showing the intended blocks **and** (b) the re-walk frames showing the fix in place. Judge confirmation that the defect is gone is recorded as an advisory reading (§6) — welcome, and never the gate.

### 5.4 The loop, whole

```
corpus (given facts) ──► drop battery ──► paired frames ──► judge panel
                                                              │ scores + punch list
                                                              ▼
        re-walk verification ◄── mcprobe verify ◄── editor applies fixes
                    │                                        ▲
                    └── items close / items persist ──────────┘
```

Each pass digests the twin against the corpus and then *corrects against the raw record* — the re-walk is the room paper's required correction pass, in work clothes: the loop never trusts its own account of what it changed; it goes back and looks (§8).

---

## 6. Governance — a discriminator that can go blind is a watcher, and is governed like one

The GAN framing is Casey's metaphor and it is a good one — but this fleet has doctrines about exactly the failure modes a discriminator has, and the design follows them rather than the metaphor where they conflict.

1. **Judges are advisor readings, never the gate.** (The Jev rule, generalised; sibling study and Jacquard both hold it.) The panel *proposes* — punch lists, scores, convergence opinions. Acceptance follows evidence rules that do not consult the panel's confidence: edits close on mcprobe + re-walk (§5.3); the board ships on the human cold test (below), not on a panel's say-so. A judge cannot pass a fix the frames don't show, and cannot block one they do.
2. **Silence is not success.** (Watcher's Charter, Rule 2.) A battery that returns an empty punch list is a *claim about the panel* before it is a claim about the twin. Before any empty or near-empty battery counts toward convergence, the panel must pass a **discrimination proof in the same session**: seeded-defect pairs — a twin frame set with a planted, known defect (the Russian Bishop's House drawn in default white-and-galvanised is the standing seed; a removed porch and a wrong tree line are alternates) — interleaved blind with the battery's real drops. If the panel misses the seed, its empties are void, the battery is re-judged after panel repair (prompt/model rotation), and the miss is filed. A discriminator that cannot catch a planted wrong roof has not certified the street; it has gone blind, and blindness is reported as a defect in the *loop*, never as a pass for the world.
3. **Discriminators go blind in more than one way.** The standing warnings are on our own record: evaluators manufacture artefacts (Civ50's roster-order hierarchy was an artefact of evaluation structure, not of the agents) and decision models carry published blind spots (the JEV lane's whole history). Countermeasures built in: judge rotation across batteries (no single model/prompt pairing owns the loop); **judge disagreement is filed, not averaged away** — a split panel on a drop is a finding about that drop or that judge, recorded in the battery report; seeded defects rotate so the proof itself can't be memorised.
4. **Convergence is a signal, not a verdict.** Casey's criterion — "you couldn't think of an improvement after dropping this street view guy anywhere" — is formalised as: **N consecutive batteries** (N = 3, *proposed parameter*) whose punch lists contain **zero actionable items above minor severity**, with every battery's panel having passed its discrimination proof, and repeat-drop scores stable (no quiet regression at the fixed points). Meeting it raises the convergence *signal*. It does not declare the twin done.
5. **The human cold test is the loop's calibration and its only ship gate.** At every convergence signal — and periodically regardless (every fourth battery, *proposed*) — a Sitka resident is dropped in blind: Casey, or Magnus, in the twin at a drop they didn't choose, walking, saying what they see. The precedent is the fleet's own: the zero-shot cold test for outward pieces came from exactly this move — a person who knows the thing, shown the artefact cold, before any insider framing. If the resident names improvements the panel missed, the convergence counter resets, the misses are filed as panel defects, and the panel is recalibrated before the loop resumes. If the resident, dropped anywhere, can't think of an improvement — *then* it's a good one, and the record says who certified it and when.

---

## 7. Costs, staging, and the smallest first loop

### 7.1 What runs where

- **Corpus:** stays where it lives — the Thor (the `~/sitka-distill/` estate, ~28 GB; the reference corpora are a small part of it). Read-only for this loop.
- **Twin generation + region editing:** Thor (the generation spike and the mcprobe pipeline are Thor-side already; the twin world's region files live with the league's infrastructure).
- **Twin walking:** the Xvfb rendering client (§3.4) — Thor or ProArt; the ProArt seat yields instantly to Casey/Magnus per standing rule, so Thor is the default and ProArt the overflow.
- **Judges:** local VL on the Thor for routine batteries (cheap, always available); the cloud 70B route for calibration batteries and split-panel arbitration (better judgement, per-call cost — spend it where disagreement is); embedding pre-screening on the JEV rack (differencing only, §4.3).
- **Human cold tests:** the Orin desk (the headed client is there; it's Casey's surface, used by invitation — which is the point of a cold test).

The honest cost unknowns *(labelled)*: judge throughput per battery (12 drops × frame sets × panel size) is unmeasured until the first battery runs; the Xvfb Minecraft client is an unbuilt spike. Both are Pilot-A-scale questions, not research programmes.

### 7.2 The smallest first loop — Lincoln Street

One street, chosen because every asset already aligns on it:

- The **street corpus** covers both sides, bridge end → cathedral block, including the walkable Aug 2024 pano chain with per-pano coords/headings and the cathedral icon set at its east end.
- The **Foundry house machine already proved this street**: 14 houses as parameter draws with a manifest of footprints, draws and scores — the Minecraft family's parameter table (§5.2) can be validated against a street whose correct answers are already on record.
- The street sits inside the sibling study's town-core board, so nothing built for the pilot is throwaway.

**Pre-registered success criteria** *(proposals, to be ratified before the first battery — the numbers are the design's, offered for amendment, not measurements)*:

1. **Discrimination proof:** the seeded defect (Bishop's House in default colours) is caught by at least 2 of 3 judges, with the correct fix named (red-metal roof, yellow siding).
2. **The loop sees:** battery 1 yields ≥ 10 actionable punch items across ≥ 3 of the 5 dimensions. (Zero or near-zero on a first pass over a first-generation street is a blindness alarm under §6.2, not a triumph.)
3. **The loop fixes:** ≥ 80% of battery 1's major items are closed — mcprobe-verified *and* re-walk-visible — by the end of pass 2.
4. **Recognition:** shown twin-only frames from the repeat drops, judges name Lincoln St / the cathedral block correctly in ≥ 2/3 of icon and core drops.
5. **Cost bound:** a full battery completes within one day of judge compute on the local VL route *(target to be measured on battery 1, then re-registered with the measured number)*.

**Kill / pivot conditions, named in advance:** if the panel cannot catch seeded defects after prompt and model rotation, the judge stack is the project — stop generating, fix discrimination first. If punch items on one street do not shrink across three passes, the generator family is the bottleneck — the loop halts scaling and the family gets the work. Either failure is a finding about the loop, filed as such; neither is quietly iterated past.

### 7.3 Scaling to the town core

- Streets in corpus order: Lincoln → Katlian (once its corpus gap closes — a survey work item, sequenced ahead of its generation) → Harbor Dr → the downtown grid → the HPR and Sawmill corridors as the board grows. Corpus coverage order and generation order stay locked together: **we do not generate what we cannot judge.**
- The **overhead loop** runs in parallel at district scale: twin top-down renders against the 543 Earth keepers (harbour/town-grade subsets first) — roof colour and roofscape, field extents, shoreline — cheaper per pass, slower cadence, feeding the same punch list with fix_class *palette-entry* / *terrain-field*.
- Icons accumulate as hand-authored assets (cathedral first; the bridge; the Russian Bishop's House is an override, not an icon — the distinction is whether the building is a *draw with corrections* or a *singular artefact*).
- The full board is the sibling study's §5.2 core (150 × 125 chunks); the fidelity loop's convergence signal is per-district, so the game can open districts as they certify rather than waiting for a whole-town verdict.

---

## 8. Connections, stated only where they are real

- **To the Syndicate study:** the twin is the game's board; this loop is how the board earns the trust the game's central meaning depends on (§1, §5.5 there). A syndicate scenario should only be staged in a district whose fidelity signal stands — home-ground advantage is meaningless on ground nobody recognises. Conversely the game gives the loop its walkers and its audience: citizens walking scripted routes *are* paired-walk traffic, and a round played in a district is a free battery of human-scale views of it.
- **To the room paper:** the loop is the digestion doctrine pointed at a world instead of a residency. The twin's generator holds parameters (a recall); the corpus holds the given facts; the paired walk is a *revisit* — the twin re-perceived against the record rather than trusted from its parameters — and the re-walk verification is the required correction pass, the step that keeps a digestion honest. Muscle memory, in that paper's terms, is the arrangement left by the worker's hands; here the arrangement is a town, and the test of it is walking it again.
- **To the Watcher's Charter:** §6 is the charter applied to judges — heartbeats from effects (seeded defects are the panel's heartbeat), silence as a failure state, and the chain ending outside the system (the resident's cold test is Rule 8's outside link, in human form).

## Open questions (filed, not resolved here)

- The Xvfb Minecraft client: build or borrow? (Spike belongs to Pilot A setup; the cameraman-pattern fallback is specified if it fails.)
- Judge panel composition per route — which local VL settings survive the seeded-defect proof is an empirical question battery 1 answers; the panel is specified by its proof, not by brand.
- Corpus refresh: the street survey is parked mid-continuation and the Earth survey has parked areas (Biorka's clouds). Does the loop commission survey sessions as its own work items when generation reaches a blind street (Katlian first), or does corpus growth stay the survey lane's separate prime directive? This study's rule — *never generate what we cannot judge* — forces the question; it does not answer who owns the camera.
- Vintage drift: the corpus mixes Aug 2024 spheres, Aug 2011 official view, and Earth tiles of various dates. When corpus and corpus disagree (a building repainted between 2011 and 2024), the newer source wins by rule proposed here — but Sitka changes slowly, not never; the twin is a twin of *a* Sitka, and naming its reference year is a decision the first battery will force.
