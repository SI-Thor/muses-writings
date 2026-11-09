# Castle Hill & downtown Sitka — the "Ride UpSide" walked tour as a video source

*2026-11-08 · Video source assessment #1 (Casey's submission, 17:41 AKST: a walked tour of part of downtown that might hold enough to recreate the Castle Hill area — and what he looks at — in Minecraft, including the distant views, as orientation help). Companion to assessment #2, the "Sea More: Alaska" guide video read as a building roster (`sitka-iconic-buildings-video-20261108.md`): that lane catalogued the buildings; this lane's charge is the ROUTE, the Castle Hill approach, and the ORIENTATION layer — what is visible from where, and how the views pin a sense of place. Casey's framing, adopted as this assessment's method: video-to-3D and Gaussian-splat tools are everywhere, but in Minecraft the medium is so forgiving about good-enough feel that the right extraction from a video is not geometry at all — §9 makes that precise.*

*Claims discipline: every frame claim below rests on frames I extracted and read myself (about 29 frames pulled to the VM and eyeballed at full 720p, listed in §3.3), on the machine-generated frame index, or on the auto-caption transcript, and each claim is tiered accordingly. Where narration is the only source, the text says so. The video is a montage, not a continuous walk — §3 is honest about its shape before anything is built on it.*

---

## 1. Identification

| Field | Value |
|---|---|
| Video ID | `2UX8lPdvKhw` — https://youtu.be/2UX8lPdvKhw |
| Title (verbatim, as returned) | **"Sitka Alaska,"** — the trailing comma is in the returned metadata, not a typo introduced here |
| Uploader | **Ride UpSide Video Adventures** |
| Handle / channel ID | `@rideupsidevideoadventures3172` / `UC_6IPOeQagDE246AAAFgD6g` |
| Duration | **1,980 s (33:00)** — media duration 1,980.161 s, 60 fps, 118,808 frames |
| Uploaded | **2022-10-22** |
| Views / likes at identification | 32,987 views · 383 likes (read 2026-11-08) |
| Description (substance) | The creator and Darlene took the grandchildren for a week in Sitka; he lived there from age 11 until leaving at 21 in the mid-1970s — a returning local's tour, not a first-timer's. Links out to sitka.com, alaskaraptor.org, fortressofthebear.org, stmichaelcathedral.org, stpeters-sitka.org |
| Filmed | Summer 2022 (inferred: upload date + the narrator's "this past summer") |
| Subtitles | No manual subtitles. YouTube auto-captions exist and were pulled (see §2) |

**How identified.** Metadata was dumped with yt-dlp on the Thor. (The YouTube page itself renders unusably through the text-fetch route — an oEmbed shell — which is why the fleet route, yt-dlp against the watch page, was used. TranscriptAPI was not attempted: it has no active paid plan — HTTP 402 on every paid call — and no API key exists in the VM environment. It was not needed: the auto-captions came down free with the video job, §2.)

**Narration caveat, filed once here and applied throughout.** The captions are machine ASR and mis-hear the local names recurrently: *Baranof* → "Baron off", *O'Connell* → "John Connolly", *Edgecumbe* → "Edgecombe", *Starrigavan* → "stargavin". One more is flagged rather than silently corrected: the narrator's "Gavin Hill" (31:0x) is written **Gavan Hill** in local usage; the assessment uses Gavan and notes the discrepancy, because a generation constraint table built from ASR spellings would file the wrong name into the town's landmark vocabulary.

## 2. Acquisition & frame extraction — the reference library entry

House pipe doctrine honoured: **one download, smallest adequate format, no parallel fetching.** 720p is plenty for landmark work — §9 shows it already exceeds the blocky channel's tolerance band everywhere it matters.

- **Tooling.** Neither the Thor nor the Oracle had yt-dlp. Standalone yt-dlp **2026.10.26** (aarch64 binary, GitHub releases) was installed at Thor `~/tools/yt-dlp` — it stays there for future video-source lanes.
- **The file.** Format `298+251` merged → Thor `~/sitka-distill/reference/video-tours/2UX8lPdvKhw/tour.mp4` — **774,369,640 bytes**, h264 1280×720 + opus, 1,980.161 s, 60 fps, 118,808 frames.
- **Captions.** English auto-captions pulled in the same job: `tour.en.vtt` (221,123 B), deduplicated into `transcript.txt` — **668 cues, 26,972 B** of narration, the source for every narration-tier claim below.

**Tooling trap, solved and filed (do not re-derive).** The Thor's ffmpeg is `7:8.0.1-nvidia1` with only **33 filters — no `scale`, no `select`** — and it cannot convert the decoder's NV12 output to JPEG ("'scale' filter not present, cannot convert formats"). Three ffmpeg extraction attempts failed on this. The working route is **OpenCV 5.0.0 in `~/ml/.venv`**: `extract_frames.py` (filed in the video's directory) decoded all 118,808 frames and wrote both frame sets. Any future frame work on the Thor goes through OpenCV, not ffmpeg.

**Products** — all under Thor `~/sitka-distill/reference/video-tours/2UX8lPdvKhw/` (the reference library; frames stay on the Thor and are never cloned into this repo):

| Product | Contents |
|---|---|
| `tour.mp4` | The video itself (774 MB) |
| `tour.en.vtt` / `transcript.txt` | Auto-captions raw / deduplicated (668 cues) |
| `frames-10s/` | **199 frames** at 10 s intervals, native 720p JPEG q88, 36 MB — `f%08d.jpg`, filename = milliseconds |
| `frames-scene/` | **908 frames**, scene-change sampling (mean-abs-diff > 14, sampled every 2 s), 170 MB — `s%08d.jpg` |
| `frames-index.json` | Timestamp index for both sets |
| `SOURCE.md` | Provenance + the ffmpeg trap note, filed in the directory |
| `extract_frames.py` | The OpenCV extractor that worked |

The fixed-interval set is the citation spine (anyone can re-derive "the frame at 13:40" from the filename alone); the scene set is the working set for close reading, since the tour's cuts land on subject changes.

## 3. What the video actually is

### 3.1 Honest shape

This is **not one continuous walk**. It is a montage assembled from a week-long family trip: walked segments, drone flights, boat footage, and interiors, shot across multiple days (the bridge segment is visibly another day from the hill segment). Roughly **40% is low-twin-value interior/attraction footage** — the Raptor Center talk, Fortress of the Bear, visitor-centre interiors — which this assessment catalogues but does not mine. The walked, eye-level, in-core material is concentrated, and where it exists it is excellent: the Castle Hill opening (3½ minutes) and the cathedral circuit are the two best eye-level sources this programme holds for their subjects (§7).

### 3.2 Segment map

Timestamps are video time (mm:ss). Value tiers are for the twin/town programme: **core** = walked eye-level material in the town core; **orientation** = distant-view material; **context** = real Sitka, low generation value; **interior** = catalogued, not mined.

| # | Time | Segment | Tier |
|---|---|---|---|
| 1 | 00:00–03:27 | **Castle Hill** (Baranof Castle State Historic Site): interpretive signs, water-side approach, railed switchback ramp, concrete stair shortcut, grass summit, stone parapet, cannon; views out to the bridge and the Sound | **core + orientation** |
| 2 | 03:28–04:03 | ANB Harbor at water level; the bridge from below; Castle Hill seen from the water | orientation (reciprocal) |
| 3 | 04:04–05:05 | Standing **on** the John O'Connell Bridge (another day): channel, seaplanes landing and taxiing, harbours on both shores | orientation |
| 4 | 05:06–06:28 | Harbor Mountain summit + drone panorama over town and Sound; the "14 miles of road" narration | orientation |
| 5 | 06:29–10:40 | Alaska Raptor Center (Sawmill Creek Rd): enclosures, the indoor Spirit-the-eagle talk | interior |
| 6 | 10:44–13:06 | Fortress of the Bear (repurposed pulp-mill clarifier tanks) | context |
| 7 | 13:24–16:27 | **St Michael's Cathedral walked circuit**: the loop road around the church — "sits right in the middle of the road" — front, bells, crossing Lincoln St for the full view | **core** |
| 8 | 16:29–17:30 | Starrigavan cruise dock, from Harbor Mountain by drone | context |
| 9 | 17:31–21:05 | St Peter's by-the-Sea: stone church, grounds, plaque, street | context (exterior usable) |
| 10 | 21:09–21:47 | Blue Lake + dam by drone, first pass | context |
| 11 | 21:47–27:45 | **Totem Park** (Sitka National Historical Park): carver's shed, totem poles along the forest trail (incl. the Raven Memorial Pole), the rocky beach, a pan bringing the town + Edgecumbe into view | **core (park interior) + orientation** |
| 12 | 27:45–29:19 | Blue Lake + dam drone: spillway (~300 ft per narration), campground, Beaver Lake bridge | context |
| 13 | 29:19–31:53 | **The skyline montage**, narrated as a named sequence: Edgecumbe, Harbor Mountain, Gavan Hill, Arrowhead, Cross Mountain | **orientation (the prized layer)** |
| 14 | 31:54–33:00 | Boat outro (Allen Marine vessel, Crescent Bay / off Crescent Harbor) + closing stills, incl. the "Welcome to Sitka" carved sign | orientation |

### 3.3 Frames actually read

About 29 frames were pulled to the VM and read at full 720p during this assessment, spanning every segment; the detailed claims in §5 rest on those, with the index and transcript carrying the segment-level claims. Frame-verified highlights: the Castle Hill interpretive panel (three eras — Tlingit, Russian, American; the "Baranof"/"Baranov" two-spellings note; a district map with legend); the "Baranof Castle State Historic Site — Alaska State Parks" sign with the railed ramp behind it; the switchback ramp; the stair shortcut; the summit grass, parapet and cannon; the summit view with the O'Connell Bridge girder crossing mid-frame, forested channel islets and the snow-patched Baranof ridge behind; Edgecumbe centred over the harbour fuel tanks in an insert shot; the water-level reciprocal (the hill as a tree-covered knoll across the channel, fuel dock foreground, the bridge's twin cable-stayed towers to the right); the bridge-deck view along Sitka Channel toward Crescent Harbor (USCG cutter at the Japonski dock, marina floats, working boats); the cathedral at close range on the circuit (pale blue-grey siding, white trim, green dome); the **Lincoln Street axis shot** — cathedral clock tower dead-centre down the street, Cross Mountain's point at the right edge of frame; a totem pole against spruce canopy (formline palette: black/red/teal on cedar); the Totem Park cobble beach (grey-brown rounded stone, kelp band at the tide line); the Blue Lake spillway; Edgecumbe's cone from the boat; and the closing "Welcome to Sitka" sign (§5.6).

## 4. The route map — the walks, reconstructed

The montage contains four genuine walked routes. Reconstructed from frames + narration, in walking order:

**Route 1 — Castle Hill (00:00–03:27), the centrepiece.** Base at street/water level on the channel side → the interpretive sign cluster (the welcome panel with the district map; the "Story of a Hill" panel) → the galvanised-railed **switchback ramp** climbing the water side of the knoll → a **concrete stair shortcut** cutting the switchbacks → the **grass summit**: stone parapet circuit, cannon, open views. The route is a *loop-shaped ascent*: ramp up one face, parapet circuit at the top, stairs as the direct line. Start and end are both at the sign cluster — the signs are read on the way in, which is how the site teaches itself.

**Route 2 — ANB Harbor → the bridge deck (03:28–05:05).** Water level at ANB Harbor (looking back at the hill — §6, A4) → up onto the John O'Connell Bridge deck → along the deck with the channel below, seaplanes landing and taxiing, harbours on both shores, the Japonski dock and its cutter in view toward Crescent Harbor. (Shot on a different day from Route 1; the route is still walkable as drawn.)

**Route 3 — the cathedral circuit (13:24–16:27).** A full walked loop around St Michael's Cathedral on its loop road — the church "sits right in the middle of the road" — passing the front and the bells at close range, then crossing Lincoln Street to take the full view back, which produces the axis shot: the tower dead-centre down Lincoln, Cross Mountain closing the frame. The circuit matters because the cathedral is an icon you *circulate around*, not one you pass (§7).

**Route 4 — the Totem Park trail (21:47–27:45).** Carver's shed → the forest trail with poles spaced along it (the Raven Memorial Pole among them) → out to the rocky beach → the pan that brings the town skyline and Edgecumbe into one view across Crescent Bay. The trail interior — pole spacing, canopy light — exists in no other source we hold.

The remaining segments are not routes: Harbor Mountain and Blue Lake are drone/summit panoramas, Starrigavan is a drone pass, and the skyline montage (§5.5) is a sequence of composed stills-like shots, not a walk.

## 5. Frame catalogue — near-field and distant, per segment

### 5.1 Castle Hill (segment 1) — near-field

- **The knoll itself**: a small, steep, tree-covered hill — spruce and alder on the slopes, grass only at the summit. From the water it reads as a green knoll, not a rock (the reciprocal frame, segment 2). Height is modest — order 15–20 m above the water (estimate from the ramp/views; the DEM settles it for generation, §10).
- **The sign cluster**: timber-framed interpretive panels at the base. The welcome panel carries a **district map whose "You Are Here" sits on the southern shore by the bridge** — the panel itself is an orientation instrument, and its map's legend (harbours, the O'Connell Bridge Visitors Dock, ANB Harbor, Sitka Channel, Japonski Island with Airport Road and Sealing Cove Harbor) corroborates the geography the frames show. The second panel, "Story of a Hill", gives the site's own reading: a near-island at high tide, defensible, valued by three nations; the Tlingit *Noow Tlein*, with four clan houses thought to have stood on top.
- **The ascent furniture**: galvanised steel railing on the switchback ramp (the railing *is* the route's visual signature — a bright zigzag line up the green face); a separate straight concrete stair as the shortcut; a brown park-rules sign at the base (foot traffic only; park hours 6:00 AM–10:00 PM).
- **The summit**: flat grass pad, low **stone parapet** around the edge, a **cannon**, clear view-cones out (§6). No building — agreeing with assessment #2's roster fact: *Castle Hill is a landmark with no building on it; the "castle" is the hill.*

### 5.2 The harbour band (segments 2–3) — near-field

Working-waterfront texture: fuel dock and white storage tanks with yellow-railed stairs (they anchor the Edgecumbe insert shot, §5.5), marina floats, working boats, a USCG cutter at the Japonski dock, seaplanes landing and taxiing in the channel. This is the town's activity layer — motion and rhythm, not just form (§10, town follow-ups).

### 5.3 The cathedral circuit (segment 7) — near-field

Close passes give the icon's palette at reading distance: **pale blue-grey siding, white trim, green dome**, clock tower; the loop road's geometry (the church islanded in its own roundabout); and from across Lincoln, the full-elevation view with the street running at the viewer. These frames are the icon-variant verification set proposed in §10.

### 5.4 Totem Park (segment 11) — near-field

Poles as **placed verticals in forest**: carved cedar, formline palette black/red/teal, spaced along a gravel trail under spruce canopy; the carver's shed at the trailhead; the beach — grey-brown rounded cobble with a dark kelp band at the tide line — where the trail meets the shore.

### 5.5 The skyline montage (segment 13) — the narration-carried placement table

At 29:19 the narrator stops walking and *names the skyline in sequence* — a salience ranking no dataset holds, delivered as bearings:

- **Mount Edgecumbe** — "about 13 miles off the west coast… right here **between these two little islands**" (~29:29–29:40 — a composed bearing, not just a visible mountain), followed by the Porky Bickar April Fools 1974 story.
- **Harbor Mountain** — the town's northern wall.
- **Gavan Hill** — "more of a hill" (ASR "Gavin"; see §1).
- **Arrowhead** — "right behind St Michael's cathedral in downtown": a backdrop peak whose *definition* is its relation to the icon.
- **Cross Mountain** — two rock faces and the central snow slide that "makes up the cross" (described 31:19–31:35).

### 5.6 The closing artefact (segment 14)

The video ends on the **"Welcome to Sitka" carved sign: an oval relief of the mountain skyline over the cathedral silhouette over water.** The town's own self-portrait states this assessment's thesis in one object — Sitka represents itself as *skyline + icon + water*, in that order. That is exactly the orientation scaffold a citizen needs, and exactly the extraction §9 prescribes.

## 6. The orientation-anchor table — the prized layer

An anchor is a (viewer position → what pins the view) pair: from this spot, these visible things fix where you are and which way you face. Timestamps are video time; "verified" = read from an extracted frame this session, "narrated" = carried by the transcript.

| # | Viewer position | What pins the view | Timestamps | Tier |
|---|---|---|---|---|
| A1 | Castle Hill summit, looking down-channel | The **O'Connell Bridge girder crossing mid-frame** below; forested channel islets beyond; the snow-patched **Baranof ridge** closing the distance | ~02:10–02:40 (frame 02:20 verified) | verified |
| A2 | Castle Hill summit, looking out to the Sound | **Edgecumbe on the horizon**; in the insert shot, the cone centred over the harbour fuel tanks (white tanks, yellow-railed stairs) | ~02:35 pointed out; insert within 00:00–03:27 | narrated + verified frame |
| A3 | Castle Hill summit pad itself | Grass, stone parapet, **cannon** — the summit furniture is the "you have arrived" signal; the parapet circuit is a full 360° anchor ring | 03:10 verified (frame) | verified |
| A4 | ANB Harbor, water level (**the reciprocal**) | **Castle Hill as a tree-covered knoll across the channel** — the landmark others orient *by*; fuel dock in the foreground; the bridge's twin cable-stayed towers to the right | 03:28–04:03 (01:40 street-side frame also verified: the knoll fills the view above the roofline, railing in frame) | verified |
| A5 | John O'Connell Bridge deck | The **channel axis**: harbours on both shores, seaplanes in the channel, the USCG cutter at the Japonski dock toward Crescent Harbor | 04:04–05:05 | verified |
| A6 | Harbor Mountain summit | The **whole-town read**: channel line, bridge, Japonski, and the road's shape — "14 miles of road, seven each way: Halibut Point one way, Sawmill Creek toward Jamestown Bay the other" | 05:06–06:28 | narrated + frames |
| A7 | Lincoln Street, looking along the axis | **Cathedral clock tower dead-centre down the street**, Cross Mountain's point at the right edge of frame — street, icon and backdrop peak in one cone | within 13:24–16:27 (frame 13:40 verified: cathedral + street + mountain behind) | verified |
| A8 | Totem Park beach | **Town skyline across Crescent Bay + Edgecumbe's bearing** from the park shore — the far-shore read of the whole core | ~27:28–27:43, within 21:47–27:45 | frames + narration |
| A9 | The skyline montage positions | The named placement sequence itself: **Edgecumbe framed between two islets**; Harbor Mt → Gavan Hill → **Arrowhead behind the cathedral** → **Cross Mt's snow cross** | 29:19–31:53 (bearings ~29:29–29:40; sequence ~30:15–31:38; the cross 31:19–31:35) | narrated |
| A10 | The "Welcome to Sitka" sign | The town's self-portrait as a single anchor: **skyline over cathedral over water** | 31:54–33:00 (closing stills) | verified |

Two properties make this table load-bearing rather than decorative. First, **it is bidirectional**: A1–A3 are views *from* the hill, A4 is the view *of* the hill — generation needs both directions, because a landmark fails in the twin if it is right from its own summit but wrong from the water. Second, **the anchors are relational, not scenic**: "Edgecumbe *between* two islets", "Arrowhead *behind* the cathedral", the tower *dead-centre down* the street. Relations are what survive a blocky render (§9); scenery does not.

## 7. Assessment (a) — what this gives Sitka-gen that SRTM / charts / OSM / Street View do not

Five things, in descending order of uniqueness:

1. **The Castle Hill approach as a route.** The hill's recreatable content is not its elevation — SRTM's 30 m posting cannot even resolve the knoll's summit furniture — it is the *ascent*: sign cluster → railed switchback ramp → stair shortcut → parapet circuit. That is continuous walked parallax, the one thing none of the held corpora contain: the street corpus (1,492 logged shots) has **zero coverage of Castle Hill or the blockhouse** (assessment #2's grep of the corpus ledger: no hits — the corpus never went up Marine Street), OSM gives at best a path line, and overhead imagery sees a tree canopy, not a route. Until this video, the programme's #2 iconic priority (assessment #2's list) had no eye-level source at all.
2. **Eye-level distant views with bearings.** Datasets give elevations and coastlines; nothing else we hold says "from the summit, Edgecumbe sits between those two islets" (A9) or puts the bridge girder mid-frame under the Baranof ridge (A1). View-cones are *constraints on generation* — the backdrop ring (Verstovia/Edgecumbe-class silhouettes, the skyline peaks) must be placed so the cones come out right — and only a walked source supplies them at eye level.
3. **The landmark's silhouette from outside.** A4 (the reciprocal) is the hill as the town sees it: a tree-covered knoll across the channel, bridge towers to the right. Generation from DEM + overhead alone would produce the hill's shape but not its *read* — canopy-covered, unbuilt, waterside. The silhouette is the citizen-facing fact.
4. **Icons at circulation distance.** The cathedral circuit (Route 3) is a walked loop with close façade passes on all sides plus the across-the-street elevation and the Lincoln axis cone (A7). Street-corpus stills give façades; only the circuit gives the loop road's geometry and the sequence of reveals around an islanded icon.
5. **A salience ranking and an activity layer.** The skyline montage is a local's ordered answer to "what do you look at?" — Harbor Mountain, Gavan Hill, Arrowhead-defined-by-the-cathedral, Cross Mountain's cross. And the harbour segments carry the town's rhythms (seaplanes landing, working boats, a cutter at the dock) that a living town's ambience spec needs and no static corpus records.

What it does **not** give, honestly: measurements (all heights here are estimates pending the DEM), the district grid (the street corpus already owns that, better), and anything at splat fidelity — which §9 argues is not a lack.

## 8. Assessment (b) — the tour stratum: a continuous discriminator path for the twin-fidelity loop

The twin study's battery is **12 discrete drops** (4 strata × 3, paired ≤2 blocks along-street, ≤10° heading): a judge materialises at a point, looks, and files a 9-field punch list. Drops are excellent at *point* defects — wrong palette, missing icon, wrong height class. They are structurally blind to three defect classes that only exist **along a path**:

- **Sequence defects** — a landmark appears or vanishes at the wrong point in a walk (the cathedral tower should stay centred as you walk Lincoln; the hill should grow over the roofline as you approach along the shore).
- **Reveal defects** — a view-cone that should *open* and doesn't: the parapet moment at Castle Hill's summit, where the bridge + islets + ridge arrive together (A1). A drop placed 5 blocks early or late sees a fine view and reports nothing.
- **Bearing defects** — an anchor visible, but in the wrong relative position against earlier frames (Edgecumbe no longer between the islets after the backdrop ring shifted). Point-paired comparisons cannot see drift against the walker's own history.

**Proposal: add a TOUR stratum to the battery.** One continuous walked path per battery, judged *as a path*: the judge walks the twin route corresponding to a source tour (Castle Hill first — the source exists now, Route 1, with the A1–A4 cones as its checkpoint table), and files the same 9-field punch list extended with the three path classes above. Design points:

- **First tour = Castle Hill** (Route 1): short, self-contained, checkpoint-dense (sign cluster → ramp → stairs → parapet ring → reciprocal from the water), and it exercises the town's #2 icon. Second candidate: the cathedral circuit (Route 3).
- **Seeded defect mid-path**: plant one known defect *between* checkpoints (e.g. remove the cannon; move the stair shortcut to the wrong face) — the loop's standing governance already requires a seeded-defect discrimination proof in-session before any empty punch list counts; on a path, the seed tests exactly the classes drops can't see.
- **Governance unchanged**: judges remain advisor-never-gate; edits close only on mcprobe re-read + the next battery's re-walk; convergence is still N=3 clean batteries raising a SIGNAL; and the only ship gate is still the **resident cold test** — whose tour form is literal: *walk the hill with Casey*. A resident who climbs the twin's ramp and doesn't feel the parapet reveal has falsified the district in a way no drop battery can argue with.
- **Cost discipline**: one tour per battery, not per drop — paths are the expensive unit, so the stratum stays at one until the punch yield justifies a second. This respects the study's scaling law: never generate what we cannot judge — and, the corollary this source adds, never *walk* what we cannot checkpoint.

## 9. Assessment (c) — Casey's deadband, made precise: why splat fidelity is wasted here, and what the right extraction is

Casey's framing — video-to-3D/Gaussian-splat tools are everywhere, but in Minecraft it becomes extremely easy because the game is so forgiving about good-enough feel — is a statement about **channel capacity**, and it can be made exact.

**What the blocky channel can express.** A Minecraft render of a landmark can carry only: presence/absence; position to ±0.5 block; a height *class*, not a height; a block-resolution silhouette; one dominant colour per face (the nearest block-family palette entry, not a ΔE); and rhythm/spacing of repeated elements. Everything a source contains beyond that band is **below the channel's noise floor at the moment of rendering** — it cannot reach the viewer's eye, so it cannot affect recognition, vibe, or any judgement the twin loop makes.

**Measured against the programme's own tolerances**, the band is wide: the twin study pairs real and twin views at ≤2 blocks along-street and ≤10° of heading; palette judgement is nearest-block-family. A splat pipeline measures geometry to centimetres and colour to ΔE — two to three orders of magnitude finer than the tolerances any consumer in this programme applies. That precision is not merely wasted; it is *unfalsifiable* here — no punch list can name a defect finer than the band, so no edit can close on one. Splat-grade extraction spends the scarce resource (lane time, pipe bytes, judge attention) measuring what the medium throws away.

**The right extraction from any video source is therefore a four-tuple per landmark:**

1. **Silhouette** — the outline as seen from the anchor viewpoints (the knoll's tree-covered profile from the water; the cathedral's dome-and-tower profile down Lincoln).
2. **Palette** — dominant block-family colours per face (pale blue-grey siding / white trim / green dome; black-red-teal formline on cedar; grey-brown cobble, kelp-dark tide band).
3. **Placement** — position and relations within the tolerance band (the hill between the channel and the bridge approach; Arrowhead *behind* the cathedral; the blockhouse one block back from Lincoln).
4. **View-cones** — the anchor table (§6): from where, what is visible, in what relation. Cones are the extraction with no splat analogue at all — a splat captures a place; a tour captures *what the place lets you see*, which is what orientation is made of.

**The source-quality corollary.** This video is 720p, shot on a consumer device in fair weather — and it already exceeds the band everywhere it matters: every silhouette, palette entry, placement and cone in §§5–6 is decidable from its frames. A lidar scan or a 4K splat pass would add nothing the twin could express. Tourist-phone video is not a degraded source for this programme; it is a *sufficient* one, and the sufficiency is provable from the tolerance table rather than asserted.

**The one exception class: icons.** Resident recognition is icon-anchored — the cathedral is recognised before the street grid is — so icons (cathedral first; the blockhouse by silhouette) earn hand-authored detail *above* the band: authored to silhouette + palette at viewing distance, verified against close-pass frames like §5.3's. The exception is about authorship effort, not capture fidelity: even for icons, the *source* requirement stays at the four-tuple.

## 10. Concrete follow-ups

**For Sitka-gen (Spike 1 and after):**

1. **Castle Hill as a named sub-district**, spec from §§5–6: summit pad (grass) at DEM height — the frames suggest order 15–20 m above the waterline (y ≈ 78–83 against the district's y 63 waterline; the DEM settles it, the estimate does not ship) — stone parapet ring, cannon, flagpole(s), tree cover on the slopes (the silhouette is canopy, A4), the railed switchback ramp on the water side as a bright zigzag line, the concrete stair shortcut on the direct face, the interpretive sign cluster at the base. Assessment #2's priority stands: build the hill early, before the streets around it harden.
2. **File the §6 anchor table as generation CONSTRAINTS**, not references: backdrop-ring and skyline placement (Edgecumbe-class cone, Harbor Mt, Gavan Hill, Arrowhead behind the cathedral block, Cross Mt) gets *checked against the cones* — a placement that breaks A7 or A9 is a defect by table, not by taste.
3. **Totem Park**: poles as a placed-vertical icon family (formline palette, trail spacing), cobble-beach palette at the shore; the beach cone (A8) joins the constraint set.
4. **Cathedral circuit frames** (§5.3) into the icon-variant verification set for the `sitka_house`-class machines' icon sibling — close-pass palette + the loop-road geometry.
5. **Coverage bookkeeping**: add a `video-tours/` line to the sitka-distill COVERAGE record — first entry `2UX8lPdvKhw` (Castle Hill, harbour band, cathedral circuit, Totem Park; summer 2022 vintage). In the corpus's newer-wins ordering this source sits between the Aug 2011 official Street View and the Aug 2024 spheres — and for Castle Hill it has no competitor at any vintage.

**For the twin-fidelity loop:**

6. Adopt the **tour stratum** (§8) at the loop's next revision: Castle Hill path first, cannon-removal as its seeded defect, the three path punch classes added to the 9-field list for tour judgements only.

**For the NPC town charter lane:**

7. **Landmark vocabulary**: the §6 anchors are the citizens' orientation tells — Tier R reflexes and Tier D situation pictures should name places the way the anchors do (relationally: "Edgecumbe between the islets", "the tower down Lincoln"), because that is the form in which position knowledge survives in a blocky world. The corrected name **Gavan Hill** (not ASR "Gavin") goes into the vocabulary as filed here.
8. **The summit as a candidate social node**: a parapet-ringed, view-commanding, building-free pad a short climb from the street is the town's natural lookout/muster-adjacent gathering point — a charter decision, proposed here, not taken.
9. **Ambience spec from the harbour band** (§5.2): seaplane movements in the channel, working-boat traffic, the cutter at the Japonski dock — rhythms for the town's background life, filed from observed footage rather than invented.

**District-acceptance tie-in (TOWN-0 WP-A):** the build charter's acceptance requires the cathedral block + Castle Hill within ±3 blocks of their OSM/charts positions, checked by census and bot-walk, never by the generator's say-so. This tour is the eye-level corroboration those checks compare against: it fixes the hill's position relative to the bridge approach and the cathedral axis (A1, A4, A7) from the ground, which is the direction the census cannot see.

## 11. Caveats

- **Single creator, fair-weather bias**: one family's summer trip, drone days chosen for weather. Winter light, rain and darkness are absent from this source; palettes are summer palettes.
- **Vintage summer 2022**: between the corpus's Aug 2011 and Aug 2024 reference points (§10.5). Waterfront furniture and signage may have moved since; nothing load-bearing here depends on post-2022 state.
- **Montage, not survey**: segment boundaries are editorial; two segments are a different day from their neighbours (§4). Route reconstructions are walkable-as-drawn, not claims that the creator walked them in one pass.
- **Narration is ASR** with recurrent name errors (§1); distances quoted from narration ("13 miles", "14 miles of road", "~300 ft") are the narrator's figures, carried as attributed claims.
- **Reading depth**: ~29 frames eyeballed at full resolution (§3.3); segment-level claims rest on the index + transcript. The frame sets on the Thor support a deeper pass if a follow-up needs one (e.g. ramp geometry counts) — that pass is not claimed here.

## Appendix — thumbnail proofs

Three frames, embedded small (480 px wide, recompressed) as provenance proofs; the full-resolution frames live on the Thor at the paths given. Filenames encode milliseconds of video time.
