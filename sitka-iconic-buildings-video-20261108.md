# Sitka's iconic buildings — the "Sea More: Alaska" guide video as a building-roster source

*2026-11-08 · Video source assessment #2 (Casey's submission, 17:44 AKST: "another cheesy but informative and visually good representations of the iconic buildings in Sitka"). Companion to the Castle Hill walked-tour assessment of video `2UX8lPdvKhw` (separate lane: route + orientation). This lane's charge: the BUILDING ROSTER — what this video shows of Sitka's iconic buildings, what it adds to our existing corpora, and the priority list Sitka-gen / the NPC town should build from. All frame claims below were read from the extracted frames themselves; all coverage claims were checked against the street corpus ledger on the Thor (`~/sitka-distill/reference/street/COVERAGE.md`, 1,490 lines, 15 sessions).*

---

## 1. Identification

| Field | Value |
|---|---|
| Title | The "Sea More: Alaska" Guide to Sitka |
| Channel / uploader | Valerie Perry ("Sea More: Alaska") — a cruise director and travel-book author, per the video description |
| Video ID | `bgGy1IngPpA` — https://youtu.be/bgGy1IngPpA |
| Uploaded | 2024-11-10 |
| Duration | 23:52 (1,432 s, ffprobe-verified on the downloaded file) |
| Views / likes at capture | 17,796 / 629 |
| Form | A cruise-passenger port guide: one walked day from the shuttle drop-off, chaptered by attraction |
| Chapters (from the description, cross-checked against yt-dlp metadata) | 00:00 Sitka Sound Cruise Center · 01:50 Harrigan Centennial Hall · 03:40 Russian Bishop's House · 04:45 Sitka Science Center & Sheldon Jackson Museum · 08:48 Sitka National Historical Park & Indian River · 13:21 Alaska Raptor Center · 14:45 Food Truck Park & Swan Lake · 17:04 Lincoln Street · 17:59 St. Michael's Cathedral · 18:50 Russian Block House · 20:38 Baranof Castle State Historic Site (Castle Hill) · 22:58 wrap-up |
| Filming conditions | A clear, sunny late-August day (the narration dates itself: salmon running, "it is August"); single presenter, selfie-style vlog camera plus walking B-roll |
| Bonus artefact | The video repeatedly cuts to the full-frame **Visit Sitka visitor map** (© 2024 Visit Sitka) with its route highlighting — clean captures at frames-best `t300` and `t1250`. The whole town's attraction geography in one graphic; filed with the frames |

**The narration layer was recovered in full — by a side door.** TranscriptAPI's paid endpoints are dead (HTTP 402, no active plan), and no manual subtitle track exists on this upload. But YouTube's own auto-captions (`en-orig`) are fetchable with the media via yt-dlp, and they were: 565 caption lines, converted to a timestamped `transcript.txt` on the Thor alongside the frames. Two honesty flags ride on every story fact in §3:

- The captions are **auto-generated**: names are garbled in characteristic ways (Harrigan → "herrian/haragan", Baranof → "baronoff", Tlingit → "kinget"). Facts below are quoted as *narrated*, lightly de-garbled, and **not independently verified** against NPS or other primary sources. Treat them as the video's claims — good enough to attach to a town building as its story draft, not good enough to carve on a plaque.
- Casey's "cheesy but informative" holds up under inspection: the cheese is real (cruise-director patter, restroom reports, ice-cream recommendations) and so is the information — dates, functions, and one genuine piece of local economic history (the Swan Lake ice story, §3.7).

## 2. Artefacts filed (Thor, reference library — never cloned into the repo)

`~/sitka-distill/reference/video-tours/bgGy1IngPpA/`

| Artefact | Detail |
|---|---|
| `guide.mp4` | 385,379,060 bytes; 1280×720, 30 fps (format 136) + English-original opus audio (251-20), merged |
| `guide.en-orig.vtt` + `transcript.txt` | Auto-captions, raw and converted (565 lines, timestamped) |
| `frames-10s/` | 144 frames, one per 10 s, 640 px wide — the browsing index |
| `frames-best/` | 23 full-resolution chapter grabs (timestamps in §3) |
| `frames-index.tsv` | Timestamp → file map for all 167 frames |
| `meta.json` | Full yt-dlp metadata dump (chapters, formats, description) |
| `download.log`, `download2.log`, `extract.log`, `run-dl.sh`, `run-extract.sh`, `extract_frames.py` | Process record, including the failures in §5 |

## 3. The building catalogue

Format per entry: **video timestamps → best frames → what it gives us (vs the street corpus) → the blocky extraction (silhouette + palette) → the story**. Corpus verdicts use three words strictly: OVERLAP (the street corpus already holds this building at equal or better depth), NEW (the corpus has no usable coverage), PARTIAL (some coverage, the video adds a distinct angle or layer).

### 3.1 Harrigan Centennial Hall — 01:50–03:40

- **Best frames:** `t150` (the forecourt/plaza, building running behind), `t190` (the tender pier beside it, with the video's own text card: "A 5-minute walk from Harrigan Centennial Hall").
- **Vs the corpus: PARTIAL.** Street sessions 3–4 walked Harbor Dr past the hall: its sign, grounds and lawn are in the corpus at street distance. The video adds the *working* face — the shuttle plaza in use, the hall as the town's arrival machine (museum + restrooms + tour muster inside), and the Sitka Public Library identified right across the parking lot — a building the corpus passes without naming.
- **Blocky extraction:** a long, low, single-storey civic shed: heavy timber posts, sage-green panel infill over a grey stone/block base, shallow pitched roofs with skylight strips. In blocks: spruce-log pillars, pale green concrete/terracotta walls, stone-brick base course, glass skylight band. It reads by *length and lowness*, not height.
- **Story (as narrated):** every cruise arrival in Sitka funnels through this building — bus drop-off and tender pier converge here. For the NPC town this is the front door: the natural muster point and the keeper-of-the-square's neighbour.

### 3.2 Russian Bishop's House — 03:40–04:45

- **Best frames:** `t245` (the long elevation behind the presenter — the single most useful frame in the video for this building), `t270` (street context looking back west along Lincoln).
- **Vs the corpus: OVERLAP — with a confirmation dividend.** The corpus already holds a landmark deep set (Session 5: full 8-shot rotation from pano 57.051189, −135.331474, plus square-on fronts). The video's dividend is *colour truth in moving light*: `t245` shows yellow siding and a red metal roof exactly as the twin study's evidence override already records (`siding=yellow, roof_mat=red_metal`) — the override now has a second, independent source agreeing with it.
- **Blocky extraction:** two-storey rectangular block, steep red gable roof, regular white-trimmed sash windows in a strict rhythm, white corner boards, small red entry stair. In blocks: yellow terracotta/plaster walls, red concrete or nether-brick roof slabs, white quartz trim. The rhythm of the windows *is* the recognition cue.
- **Story (as narrated):** Sitka was the capital of Russian America; the Russian Orthodox bishop lived here. Ground floor a self-guided museum (free), the bishop's upstairs residence by ranger-led tour. A Russian-era map inside identifies which Russian-era buildings still stand — the town's own first roster, drawn by its occupants.

### 3.3 Sitka Sound Science Center — within 04:45–08:48 (chapter shared with §3.4)

- **Best frames:** `f0033` (320 s — the main building square from the sidewalk: a white three-storey block), `t400` (the hatchery yard: grey corrugated building, orange-red metal roof, blue fish totes stacked, the covered working race), `t460` (the gift-shop/chowder building: vertical pale metal siding on the water).
- **Vs the corpus: NEW.** The street survey walked Lincoln St *past the campus turn* but never catalogued the Science Center as a subject. The video gives three of its faces plus its working yard.
- **Blocky extraction:** utilitarian waterfront-industrial: corrugated grey walls (iron-block or light-grey concrete texture), one strong orange-red roof plane, yard clutter as identity (blue tote stacks = blue concrete/ shulker accents; the open hatchery race = a water channel under a flat roof on posts). This is a *working* building — the town's fish economy made visible.
- **Story (as narrated):** aquarium/underwater exhibits, an active salmon hatchery (fish returning July–August, staff working the race), guided tide-pooling on occasion; the building was part of Sheldon Jackson College. For the town: a workplace with a seasonal pulse — the hatchery run is a calendar event citizens can have rounds about.

### 3.4 Sheldon Jackson Museum — within 04:45–08:48

- **Best frames:** `f0036` (350 s — the campus green: lawn, specimen spruce, the campus buildings across it), distant campus elevations in the same stretch. **Honest limit:** the museum's octagon is *described* on camera but never isolated in a clean frame in the sampled set — the segment spends its frames on the Science Center and the campus as a place.
- **Vs the corpus: PARTIAL.** Street sessions 7–8 walked the campus edge on Lincoln St (778–834 Lincoln), so the campus street elevations exist; a museum-grade elevation does not, in either source.
- **Blocky extraction (from narration + campus frames, flagged as the weakest entry in this catalogue):** an **octagonal** building with a domed top — "one of the first concrete structures in Alaska". In blocks: an 8-sided drum (two-block stair-stepped corners), pale concrete walls, a shallow dome, oxidised-copper green or grey. Singular geometry — if built right it is unmistakable; if built as a square box it is nothing.
- **Story (as narrated):** Alaska Native art and artefacts from across the whole state, on the former Sheldon Jackson College campus ("a gorgeous campus… it is no more").

### 3.5 Sitka National Historical Park — visitor centre, Totem Trail, Indian River — 08:48–13:21

- **Best frames:** `t545` (visitor centre front from the car park: totem pole and flagpole on the lawn, cedar-shake roofs), `t620` (trail interior: bear-sign and forest texture), `t680` (a totem pole shot from its base, looking up), `t730` (the Indian River pedestrian bridge, deck level, walking it).
- **Vs the corpus: SPLIT.** The visitor centre is OVERLAP — the corpus holds a "landmark-grade front elevation" (Session 10: square-on across Metlakatla St, totem pole + flagpole). The park *interior* is NEW: the corpus stops at the entrance; the video walks the totem trail and the river. And `t730` matters beyond its segment: the twin study names **the Indian River bridge end** as a corpus gap — the video now holds the bridge at deck level (its deck, rails, and the walk across). That is half the gap closed: deck and far side yes, the street-side approach still missing.
- **Blocky extraction:** visitor centre = low white walls, dark timber trim, weathered cedar-shake roofs (grey-brown slabs in shallow pitches) against a wall of spruce. Totem poles: single carved columns, grey weathered wood with faded pigment — in blocks a 1×1 log column 10–14 high with carved-band texture; spaced along a gravel loop through big spruce. The bridge: a plain concrete deck with metal pipe rails.
- **Story (as narrated):** the Totem Trail is a ~1-mile loop with more than a dozen poles; bears are active (the yellow bear sign is in `t620`); the Indian River in late August is "full of salmon", with eagles in the trees and sometimes bears. The bridge is the hinge of the east side: park on one side, the road to the Raptor Center on the other.

### 3.6 Alaska Raptor Center — 13:21–14:45

- **Best frames:** `t830` / `f0085` (the forested approach drive, the centre's pale building small at its end), `t865` (the Raptor Way street sign at the Sawmill Creek Rd junction — the segment's most identifiable frame is its sign).
- **Vs the corpus: NEW but WEAK.** The street corpus has nothing here (its one "raptor" mention is an Earth-survey relocation note). But the video itself barely shows the building: the segment is approach, signage, and narration. No aviary, no flight-training barn elevation, nothing a builder could draw from beyond massing-at-a-distance.
- **Blocky extraction:** not honestly drawable from this source — a low pale building at the end of a spruce drive. Filed as a roster entry with a source debt, not a build spec.
- **Story (as narrated):** injured birds — bald eagles above all — rehabilitated for release; "Raptors in Residence" for those that can't be; staff presentations and open-air exhibits. ~25 minutes' walk from the shuttle drop, best combined after the park. For the town: a workplace at the edge of the wild, with patients — a distinctive citizen round if the town ever extends east.

### 3.7 Swan Lake & the food-truck park / roundabout — 14:45–17:04

- **Best frames:** `t950` (the Swan Lake Park sign corner), `t905` (the main roundabout: Lake St / Halibut Point Rd junction townscape), `t1045` (the Lake St / Harbor Dr junction, food-truck park behind).
- **Vs the corpus: NEW as ground truth.** Swan Lake exists in our records only as an Earth-overhead survey note. The video gives the park at eye level and — more usefully — the roundabout district: the town's traffic hinge where the shuttle road, Lake St and the food trucks meet.
- **Blocky extraction:** landscape, not building: a small lake in a grass bowl, a wooden park sign, flower beds; around it, food trucks = small bright boxes on wheels in a gravel lot — in the town, market stalls wearing liveries.
- **Story (as narrated — the video's best piece of history):** the $7.2M Alaska Purchase price is said to include $200k for Swan Lake's **ice business** — winter ice cut from the lake and shipped as far as San Francisco. Whether or not the number survives fact-checking, as a town story it is gold: the lake is a former industrial asset, and a citizen can tell you so.

### 3.8 Lincoln Street & Harry Race Pharmacy — 17:04–17:59, pharmacy at ~20:05

- **Best frames:** `t1045` (junction + shuttle bus + storefronts), `t1205` (Harry Race Pharmacy: the covered sidewalk, the hanging sign "Harry Race PHARMACY AND 29 MINUTE PHOTO", the soda-fountain window).
- **Vs the corpus: OVERLAP, texture grade.** Lincoln St is the corpus's home street (both directions, both SV dates). The video adds *use*: buses loading, the pharmacy's ice-cream counter identified as a local institution, food trucks on the main street.
- **Blocky extraction:** the storefront rhythm itself — flat-fronted two-storey boxes, covered sidewalks on posts, hanging perpendicular signs. Harry Race is a named storefront for the override table: blue-trimmed white frontage under a continuous awning.
- **Story (as narrated):** Lincoln is "largely considered to be the main street in town" — local stores over souvenir mills; the pharmacy's old-school ice-cream counter is where the guide herself goes, en route to Castle Hill.

### 3.9 St. Michael's Cathedral — 17:59–18:50

- **Best frames:** `t1095` and `t1120` (the same street-level three-quarter from across Lincoln, ~25 s apart: grey-blue siding, clock tier, belfry with its bell, green spire and the green dome behind).
- **Vs the corpus: OVERLAP — the corpus is deeper and stays primary.** Front elevations in two years (2011 + 2024), the full rotation set, clock/belfry/dome zooms, the complete block circuit (street COVERAGE Sessions 1–2). The video's contribution is a *2024-summer, eye-level, in-traffic* confirmation and one good approach composition (cathedral + Maksoutoff corner + the mountains behind) — a drop-battery frame, not a build source.
- **Blocky extraction:** already settled by the twin study — an icon-variant, hand-authored once: grey-blue horizontal siding, the stacked tower (porch tier, clock tier, belfry, green spire + Orthodox cross), green ribbed dome on its octagonal drum behind. Nothing in the video revises it.
- **Story (as narrated):** the original church (mid-1800s) burned in the 1960s; this is its faithful rebuild in fire-resistant materials, with what was saved from the original on display. Visits by donation ($5 suggested); independent visitors limited to a midday window in cruise season.

### 3.10 The Russian Blockhouse — 18:50–20:38

- **Best frames:** `t1160` (extreme close: the weathered log wall and its corner joinery filling the frame — with, over the presenter's shoulder, the cathedral's green dome in the distance: the town's orientation in one shot), plus the segment's approach walk and interpretive signs.
- **Vs the corpus: NEW — cleanly, completely new.** Grepping the street ledger for castle/blockhouse returns *zero* hits: the corpus never went up Marine Street. This video is our only eye-level source for the building.
- **Blocky extraction:** the simplest icon in Sitka: a two-storey **octagonal log tower**, horizontal weathered-grey logs with squared corner joinery standing proud, a shallow conical/pyramidal cap roof. In blocks: stripped spruce/oak logs laid full-length, grey-weathered palette (dead-bush greys, not fresh browns), a dark slab cap. Small footprint, total silhouette — it will read at a glance from anywhere it is visible.
- **Story (as narrated):** a replica of the blockhouses set into Russian Sitka's fortified wall, cannon houses guarding the settlement; you can't go in; interpretive signs line the walk up; "a lot of people miss it" — one block back from Lincoln St, next to the Pioneers Home, and nearly always empty. A hidden-gem landmark: exactly the kind of place a town's citizens know and visitors don't.

### 3.11 Castle Hill — Baranof Castle State Historic Site — 20:38–22:58

- **Best frames:** `t1250` is a map cutaway; the site itself: `t1300` (the summit: paved top, stone retaining wall, benches, interpretive signs, an empty flagpole, the town and Verstovia behind), `t1355` (the ramped descent through greenery).
- **Vs the corpus: NEW (same zero-hit grep as the blockhouse).** Route and distant-view analysis belong to the sister lane (`2UX8lPdvKhw`); this entry is the roster fact: **Castle Hill is a landmark with no building on it.** The "castle" is the hill — a terraced stone-walled summit with a cannon, five or six interpretive signs, and empty flagpoles.
- **Blocky extraction:** terrain work, not architecture: a flat-topped knoll, stone-brick retaining ring, gravel/paved cap, stairs on the Lincoln side and a ramp on the water side, cannon + flagpole + sign props. Cheap to build, and its fidelity test is inverted — it succeeds if the summit is *empty in the right shape* and the view out is right.
- **Story (as narrated):** the Russian governor's seat and fortification; Tlingit use before that ("the kinget [Tlingit] probably used this place as well"); and the transfer — the US flag raised here for the first time on Alaskan soil. Today "in a little bit of a state of disrepair… they don't even fly the flag anymore." A town could do something about that. (Filed as an observation, not a plan.)

### 3.12 Sitka Sound Cruise Center — 00:00–01:50

Six miles out of town; wood-and-glass terminal buildings, a wooden archway, the shuttle fleet. Not part of the town core and not roster material — noted so its absence from §4 is a decision, not an oversight.

## 4. The iconic building priority list — for Sitka-gen / the NPC town

Ordered by *recognisability-at-a-glance per unit of build effort*, judged against the twin study's vibe gate (a drop passes only if the location can be **named from twin frames alone**). Build classes use the twin study's vocabulary: **icon** = hand-authored singular asset; **override** = a family draw with a named per-building evidence record; **family** = parameter draw.

| # | Building / place | Class | Why this rank | Sources |
|---|---|---|---|---|
| 1 | **St. Michael's Cathedral** | icon | The town's name-tag: the only building a Sitka drop *must* be nameable by. Already the twin loop's calibration landmark and first planned icon | Street corpus (deep, primary) + video confirmation |
| 2 | **Castle Hill** | terrain landmark | The town's orientation anchor — and nearly free: an empty, right-shaped summit. The NPC town charter's citizens navigate by it; the paintball game's board reads from it. Build the hill early, before the streets around it harden | This video (only eye-level source) + Earth overhead + SRTM |
| 3 | **Russian Bishop's House** | override | The evidence override already exists (`yellow / red_metal`) and the video independently confirms the colours — the cheapest *proven* recognition on Lincoln St | Street corpus deep set + video `t245` |
| 4 | **The Russian Blockhouse** | icon | Total silhouette, tiny footprint, one material. The highest recognition-per-block in town — and until this video we had *no* eye-level source for it at all | This video (sole eye-level source) + Earth overhead for siting |
| 5 | **NHP visitor centre + totem poles** | override + props | The east gate of the town: shake-roofed centre (corpus holds a landmark-grade front) plus the poles, which are pure vertical rhythm — a dozen 1×1 carved columns make a place | Street corpus (front) + video (interior, poles, bridge) |
| 6 | **Harrigan Centennial Hall** | family + signage | The town's front door and muster point; reads by length and lowness. Build with its plaza and the library across the lot | Street corpus (street distance) + video (plaza in use) |
| 7 | **Sheldon Jackson Museum** | icon (deferred detail) | Singular geometry (octagon + dome) — but *neither* source holds a clean elevation. Place the octagon massing early; detail pass waits on a better capture | Narration (form) + campus frames both sources — **source debt** |
| 8 | **Sitka Sound Science Center** | family | The working waterfront: hatchery yard, totes, race. Not nameable by tourists, but the town's citizens work there — liveliness before fame | This video (sole catalogue source) |
| 9 | **Lincoln St storefront rhythm + Harry Race Pharmacy** | family + one override | The street as a whole is the landmark; Harry Race is its named exception (awning, hanging sign, soda fountain) | Street corpus (primary) + video texture |
| 10 | **Swan Lake** | landscape feature | A story with a lake attached (the ice money). Cheap: a grass bowl, a sign, still water | This video + Earth overhead |
| 11 | **Alaska Raptor Center** | roster only — **do not build yet** | Real place, real town function, no buildable source. Building it now means inventing it — the one sin the twin loop exists to prevent | Narration only — **source debt** |

**Gaps named plainly.** (i) Katlian St remains a corpus gap in every source we hold — neither video goes there. (ii) The Sheldon Jackson Museum's clean elevation and the Raptor Center's building are the roster's two source debts; both want a short Street View or photo capture session, not invention. (iii) The Indian River bridge is half-closed (deck yes, street approach no). (iv) Interiors: the video enters almost nothing (Bishop's House ground floor and the cathedral are talked about, not filmed inside in the sampled frames) — the town's interiors have no source yet and should be treated as the citizens' own territory to furnish, not as replicas. (v) Winter/night Sitka is absent from every corpus we hold; all sources are summer daylight.

## 5. Process — what actually happened (failures included)

1. **Identification** came from the YouTube page (title, description, chapter list) and was confirmed against yt-dlp metadata on the Thor (uploader Valerie Perry, 23:52, uploaded 2024-11-10, 17,796 views). TranscriptAPI was not attempted beyond noting the standing 402 — its paid plan is inactive (Casey's open item); YouTube's own auto-captions made it unnecessary here.
2. **Download discipline:** the sister (Castle Hill) lane's download was checked first — its `extract.done` was already filed and no yt-dlp/ffmpeg process was running, so the pipe was clear before this lane fetched anything. One download, 720p.
3. **Format traps, both hit and fixed:** the sister lane's format pair (`298+251`) does not exist for this upload (it offers 136 for 720p, and its English audio is `251-20`, not `251`); and yt-dlp **aborted after a 429 on the duplicate `en` subtitle track** before ever fetching media — the `en-orig` captions had already landed, so the re-run fetched media only. The download itself ran at up to ~14 MiB/s and finished in under a minute of transfer (385 MB).
4. **Extraction trap:** the Thor's system ffmpeg fails on this file (hardware-decoded nv12 frames break its mjpeg filter chain — the same class of failure the sister lane's log shows). Extraction was rerouted to Python/OpenCV (`extract_frames.py`, filed with the artefacts): 144 index frames + 23 chapter grabs + the timestamp index, all verified by count.
5. **Reading:** all 23 chapter grabs plus targeted index frames were viewed first-hand for §3; corpus comparisons are from the street ledger's own session entries, grepped and read on the Thor, not from memory.

## 6. What this changes

- The twin study's corpus inventory gains a **video-tour stratum**: two walked videos now sit in `~/sitka-distill/reference/video-tours/` beside the street and Earth corpora — continuous, narrated, eye-level. This one is the roster-shaped half of the pair: it *names* the buildings and attaches their stories, which is precisely the input the vibe gate's named-location test and the town charter's building biographies need.
- Two of the twin study's named gaps shrink: the blockhouse and Castle Hill go from *no eye-level source* to *one good source*, and the Indian River bridge is half-covered.
- The roster (§4) is buildable in order with no invention: ranks 1–6 and 8–10 all have at least one eye-level source plus overhead siting. Ranks 7 and 11 are held *as debts on purpose* — the discipline that keeps the town honest is that a building we cannot source is a capture task, not a drawing task.

---

*Sources: the video itself (identification §1, frames and transcript on the Thor); Thor `~/sitka-distill/reference/street/COVERAGE.md` (corpus sessions 1–15) and `~/sitka-distill/reference/COVERAGE.md` (Earth survey); shelf siblings `sitka-twin-fidelity-loop-20261108.md` (corpus inventory, vibe gate, icon/override vocabulary) and `npc-town-charter-20261108.md` (the town that will live among these buildings). Story facts in §3 are the video's narration as auto-captioned — unverified against primary sources, flagged per entry. PLACEMENT: the-league-and-civilization room.*
