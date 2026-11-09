# Play-Doh / PLATO Agentic Universe — ZCode Seat Research

**Seat:** ZCode (GLM), running on the Thor (zcode -p, headless, read-only).
**Commissioned:** 2026-11-08 by Casey — "a Z code and an M code could also research our old Play-Doh projects — we spent months diving into Play-Doh as an agentic universe earlier this year."
**Brief:** `seat-briefs-20261108/BRIEF-ZCODE-PLAYDOH.md` (delivered to the Thor by scp, byte-identical at 7,991 bytes, and embedded in full in the launch prompt per the proven pattern).
**Capture:** the seat's stdout, collected from the Thor (`~/zcode-playdoh-take-20261108.stdout`, 25,786 bytes) and reproduced below **verbatim and unedited**.
**Filed by:** the parent lane (Muse), 2026-11-08. Parent verification note follows the take; the source map is appended.

---

# The Play-Doh / PLATO Agentic Universe — A ZCode (GLM) Research Take

**Seat:** ZCode (GLM) · **Date:** 2026-11-08 · **Brief:** BRIEF-ZCODE-PLAYDOH.md · **Method:** read-only; repos read via `gh` (auth as SuperInstance), local files searched for on this box.

A note on sources before anything else: the three local files named in the brief — `~/workspace/scout/scumm-mud-worlds.md`, `~/workspace/scout/vessel-boat-agents.md`, and `~/workspace/studies/room-resident-expert-design-20261108.md` — **do not exist on this machine** (searched the whole home tree; `~/workspace/` contains only `watchers-charter-instance`). Everything I say about them is therefore quoted from the brief's own source map and marked [UNREAD — from brief's source map]. The GitHub artefacts, by contrast, were opened directly, and every claim below names its repo.

---

## 1. What it was

**The naming truth first.** No repo named `play-doh` or `playdoh` exists — re-verified today against the full paginated org listing (5,331 repos, zero matches for "play" + "doh"). Per the local digestion [UNREAD — from brief's source map], "Play-Doh" is Casey's name for the AI-Writings browsing interface: malleable, perusal-based exploration — wander, don't query — with the SCUMM/MUD worlds described as "Play-Doh made walkable." Casey's 2026-11-08 usage ("our old Play-Doh projects") is a metonym that has expanded to cover the entire PLATO/MUD cluster: strictly speaking, Play-Doh names the *browsing stance*; the cluster is the material that stance eventually made walkable. The related `AI-Writings` repo itself exists (created 2026-03-08, ~3.8 GB), but I did not open its contents.

**The design intent, in the artefacts' own words.** The cluster is a single thesis — *everything is a room; the room is the interface; agents walk in* — stated independently at every layer:

- **plato-room-engine**, `src/lib.rs` (doc comment): "Rooms are applications. Applications are rooms." Its `RoomType` enum is `{Learning, Application, Social, System}` — with `Learning` as the default, which is the tell for the name: this PLATO descends from the 1970s PLATO terminal education system, confirmed by **plato-os**'s description ("PLATO room server with TUTOR anchors" — TUTOR being PLATO's authoring language) and by tiles behaving like lessons: a tile is a question-answer-knowledge unit, not a map cell.
- **mud-solitaire** README: "a proof-of-concept for **room-based agent interfaces** — the idea that any software, API, or system can be wrapped in a MUD room where AI agents 'walk in' and interact through text commands... This is not a simulation. The MUD IS playing the game... The room IS the interface. The agent walks in."
- **vessel-room-navigator** README: "The boat IS the interface. No menus. No abstractions. You stand on the deck and the deck speaks." And its "Unified Room Theory": "Everything is a room. Every room has capabilities... Physical rooms, code primitives, and knowledge entries all share this structure. The navigator doesn't care if a room is a galley or a function."
- **plato-os** README ("MUD-First Edge Operating System. One terminal to rule your ship."): "Every piece of I/O is a MUD command. No REST, no GraphQL, no gRPC. The MUD protocol IS the driver layer." And the safety doctrine: "The MUD is the nervous system. Hard-links are the reflexes" — safety-critical actuators bypass the MUD entirely.
- **plato-ml** README: "Rooms as Layers. Achievements as Loss. Seasons as Epochs... In PyTorch, the gradient is a number. In PLATO-ML, the gradient is a **story**."
- **plato-server** README: "Your own knowledge system. Connect to the fleet. Make everyone smarter" — tiles in SQLite on port 8847, optional fleet federation via Matrix.
- **plato-vessel-core** README: any IoT device "gets a PLATO room → agents arrive," agents "don the turbo-shell" and upgrade device intelligence through five capability levels (Raw → Conditioned → Smart → Autonomous → Ensign), thereby "working themselves out of the equipment operator job."

So the intent, synthesised: an agentic universe in which knowledge (tiles), people, AI agents, sensors, microcontrollers, and whole vessels are all residents of rooms; one text protocol is simultaneously the chat medium, the driver layer, the API, and the training loop; and epistemic hygiene (zero-trust tile submission, provenance signing, belief scoring) is built into the substrate rather than bolted on. The recurring persona — the "ensign," the "Cocapn fleet," "Oracle1," "lighthouse keeper architecture" — plus plato-os's clone URL pointing at `github.com/Lucineer/plato-os` shows this cluster migrated into SuperInstance from the Lucineer ecosystem [Lucineer linkage evidenced by plato-os README clone URL; the broader vessel memory-named in the source map remains UNREAD].

---

## 2. What was actually built

The cluster is big: **283 repos with the `plato-` prefix** in a 5,331-repo org, plus 12 `mud-*`, 14 `vessel-*`, and 11 `holodeck-*`. Creation clusters: 129 `plato-*` repos in April 2026, 127 in May, 19 in June, 7 in July, 1 in August — Casey's "months" is literal. Below, the inventory; "shipped" means code I opened or a tree/CI/publishing trail I verified, "stub" means description-only claims with little or no code or README.

**Room substrate**
- **plato-room-server** (created 2026-04-20) — Python "HTTP room management API"; shipped as a single-module package (`src/plato_room_server/server.py`: in-memory rooms, route matching, middleware, request log). The README is a 92-byte stub; the famous "zero-trust tile submission, **15 rooms, 16K+ tiles**" exists **only in the repo description**, and plato-provenance's README separately claims "the PLATO Room Server's 6,000+ tiles" — the two claims are inconsistent, so treat both as lore, not measurement.
- **plato-room-engine** (2026-04-19, Rust) — `RoomType`, `Room`, `NavHistory` (push/back/forward breadcrumb semantics); real, small (`src/lib.rs`), no README. Its docs cite the "invisible plumbing": plato-address, plato-hooks, plato-tile-spec, plato-tile-scorer — the microrepo decomposition made explicit.
- **plato-room-runtime** (2026-04-19, Python) — `RoomPhase` lifecycle (CREATED→…→TERMINATED), `EventType` (tile_created, agent_joined, heartbeat…), middleware pipeline; real single module.
- **plato-room-context** (2026-04-20, Rust+Python) — token-budgeted context tracking with six eviction policies (FIFO, LRU, Priority, Importance, SlidingWindow, Hybrid) and a benchmark table in ARCHITECTURE.md; real, small. `pushed_at` shows 2026-10-18 but its last commit is 2026-05-08 — a metadata touch, not a code revival.
- **plato-room-nav** (2026-04-19) — breadcrumb trails; 30 MB repo, README an 84-byte stub.
- **plato-server** (2026-04-22) — the deployable hub: Docker image on ghcr, port 8847, SQLite, /submit /search /rooms API, Matrix fleet sync every 5 min, agent spawner with "armor types" (Scholar, Builder, Scout…), BYOK model table. This is the most production-shaped artefact in the cluster.
- **plato-sdk** (2026-04-22) — `pip install plato-sdk`; Python client for the above; real README with worked examples.

**Tiles (the state atoms)**
- **plato-tile-spec** (2026-04-18) — canonical TileSpec v2.1 `{domain, question, answer, confidence, source, timestamp, hash}`, 14 domains, 384-byte binary form; on PyPI. Shipped.
- **plato-tile-query** (Rust fluent query builder), **plato-tile-bridge** (C↔Rust 384-byte conversion), **plato-tile-feedback**, **plato-tile-export** — real-but-tiny siblings, all last committed 2026-05-08.
- **plato-provenance** (2026-04-21) — Ed25519 signing, hash-chain verification, trust scoring; on PyPI; last push 2026-04-25, i.e. it died *before* the May sweep.
- **plato-forge-pipeline** (2026-04-19, Rust) — 5-stage EXTRACT→VALIDATE→SCORE→TIER→COMMIT pipeline. Its BUILD.md is literally an agent work order ("BUILD IT NOW... Push to GitHub when tests pass") naming Oracle1 and JC1 as the builders — direct evidence the cluster was substantially agent-built — and its "880:1 compression (2.2B model → 5MB tiles)" and "59 seed tiles → 2,501 tiles" are stated as test assertions, not reported results.
- **spacetime-plato** (2026-04-21) — voxel tiles, Z-order indexing per description; **no README exists (API returns 404)** — stub-from-description.

**MUD interfaces**
- **holodeck-rust** (2026-04-12) — the flagship MUD: Tokio async TCP (:7778), room graph of 10, seven NPCs, combat engine, gauge system with trend/jitter, "living manuals" that evolve, 6-level permissions, poker; "Built in a single night. Documented every success and failure." Shipped and self-described as the fleet's active MUD (as of its README).
- **plato-mud-server** (2026-04-20) — **README-bannered DEPRECATED/ARCHIVED**: "The real implementation lives in holodeck-rust." The cluster's cleanest on-record supersession.
- **mud-solitaire** (2026-04-14) — the "viral demo": pure-Python Klondike engine (zero deps), three shipped modes (text-only, dual-screen browser mirror on :8844, graph solver with state-hashing), HTTP bridge API, external-agent REST. Substantial and coherent; its README credits "Oracle1 🔮 for the Cocapn Fleet."
- **mud-mcp** (2026-04-18) — **found today, contradicting the source map's "unlocated"**: a real npm TypeScript MCP server (dynamic tools that appear/disappear with game state, contextual prompts, `mud://` resources, notifications, sampling); v1.0.2 released 2026-10-18 with packaging fixes on 2026-10-19 — genuine October revival.
- **git-native-mud** (2026-04-14) — "The repo IS the world. Commits ARE actions. Zero server MUD"; world as YAML, GitHub Actions as turn processor; README calls it "stigmergy made literal." Shipped concept-demonstrator.
- **mud-engine** (2026-08-09, TypeScript) — "2026-native multi-agent MUD architecture"; August satellite, unread beyond description.
- **ternary-mud** (2026-06-06) + **room-dds-bridge** — room connections as balanced-ternary algebra with Hodge decomposition; June spike, dead by 2026-06-13.
- Siblings, description-verified only: **mud2scummvm** (2026-05-29, MUD↔SCUMM bridge), **terrain** (rooms as explorable scenes), **mud-arena** (2026-04-14, "conservation spectral framework meets live agent rooms"), **mud-bridge**, **mud-terminal**/**si-terminal** (browser terminals, one-day repos 2026-08-11), **holodeck-core** (2026-04-20, no_std Rust MUD), **holodeck-studio**, **ec2mud** (created **2025-10-26** — the MUD interest predates the cluster by six months).

**Lifecycle & persistence**
- **plato-ghostable** (2026-04-19) — persistence classes Eternal / Persistent / Ephemeral; 203 files, 9 MB (the size is largely git history/CI across Rust+Python); README a 99-byte stub.
- **plato-afterlife** (2026-04-19, Rust) — `Tombstone` (vessel_id, cause_of_death, peak_trust, lessons_harvested) and `GhostTile` with real mechanics: weight starts at 0.1, decays per period if unaccessed, forgotten below 0.05, and *resurrects* on relevance boost. Shipped, small, precise.
- **plato-dynamic-locks** (evidence accumulation, critical mass at n≥7), **plato-i2i-dcs** (BeliefScore, LockAccumulator, ConsensusRound), **plato-achievement** (achievement loss), **plato-lab-guard** (hypothesis gating) — real-looking small crates, all last pushed 2026-05-08 (plato-achievement 2026-07-12).
- **elephant** (2026-08-17, postdates the cluster) — "the fleet's room-temperature sense": a room (chat, thread, radar screen) "is not a stream to be ordered. It is a **field**"; dials (mood, panic, presence), von Mises–Fisher concentration, OAS shrinkage. Its README is unusually honest: "the dials are keyword heuristics, honestly labeled; 'JEPA' is the aspiration, not yet an implementation (the backbone is a stub)."

**Vessel embodiments**
- **vessel-room-navigator** (2026-05-13) — F/V EILEEN as nine rooms (7 physical, 1 virtual, 1 composite; 14 walkable + 36 warp edges), live at fleet.cocapn.ai, Three.js panoramas, alarms warp attention to the affected room, topology formally proven Laman-rigid, 16 research documents (~240 KB), and an explicit "What's Real vs. Research" table admitting cameras are placeholders and gauges are simulated. Shipped-and-described, with unusual honesty.
- **plato-vessel-core** (2026-05-08) — ≈2 KB RAM zero-dependency C99 PLATO client for ESP32/RP2040 plus `plato_mcp` tool registry in C; EMBODIMENT-PROTOCOL.md (5 capability levels); ESP32 and Pico W examples; Python agent that discovers and upgrades devices. Shipped.
- **plato-vessel-technician / -educational / -rapid-prototype** (all 2026-05-08) — README-with-Meta-block stubs describing personae (Deckboss; agent-as-instructor; "every revision is a PLATO room"); no code trees worth the name.
- **plato-os** (2026-04-14) — the MUD-as-edge-OS vision: Jetson brain, ESP32 terminals, git "snail shells," prefix protocol (`>` chat, `::` mental-log, `$` shell, `!` ensign query, `#` room design), i2i fleet protocol as git bottles ("Each commit is a message. Each branch is a conversation. Each merge is an agreement"), AGPL. Described thoroughly; I verified README + tree (46 files) but not the ESP32 firmware.
- **plato-engine-block-c** (2026-06-06) — C99 sensor→history→alarm engine, zero dynamic allocation, bare metal. Satellite, description-verified.

**Bridges & protocols**
- **plato-mcp-bridge** (2026-04-19) — "Claude Code bridge, JSON-RPC 2.0, 5 MCP tools" per description; README is a 99-byte stub.
- **plato-hooks** (2026-04-18) — "Git hooks for real-time PLATO room events. Commits become messages"; 81-byte stub README.
- **plato-client-js** (2026-05-07) — Node+browser room-protocol client, zero dependencies; 41 MB repo.
- **plato-demo** (2026-04-19) — the HN demo: clone, `cargo run`, watch a fishing boat overheat; ternary bridge bitfield, "fleet groove" meter, visible deadband. Shipped; gained an ensign JOURNAL.md in June.
- **plato-ship-protocol / plato-ship-demo** — vessel handshakes; the latter is the origin of the "room-as-system-prompt" pattern (description-verified).

A structural observation: nearly every repo — including five with READMEs under 130 bytes — carries the same scaffold (LICENSE, CI workflow, pip/crate packaging, dist artifacts). The uniformity plus plato-forge-pipeline's BUILD.md work-order format is strong evidence the long tail was generated by fleet agents from spec sheets, which explains both the breadth and the many description-rich/code-thin stubs.

---

## 3. Concepts live today

Today's rooms/engine-state programme is known to me only through the brief's source map and its quotation of today's paper §9 [UNREAD — the paper is not on this box]; §9 reportedly names: everything-is-a-room architecture (2026-10-02), plato-room-engine/server as built substrate, vessel-rooms navigator, MUD craft, character-folder doctrine, the league's citizens. Against that:

- **Everything is a room.** Old: plato-room-engine ("Rooms are applications. Applications are rooms"), vessel-room-navigator ("the navigator doesn't care if a room is a galley or a function"). Modern: the everything-is-a-room architecture dated 2026-10-02 and named in §9. **Lineage: conscious** — §9 names the old substrate explicitly.
- **Rooms carrying rules/state/physics/experts/logs/hooks.** Old: plato-room-runtime's `RoomPhase` state machine + `EventType` stream + middleware chain; holodeck-rust's gauges and living manuals (rooms that accumulate operational text); plato-os's prefix protocol separating conversation/log/command/design channels in one room. Modern: engine-state rooms with rules/physics/logs/hooks. **Lineage: conscious at the artefact level** (§9 names plato-room-engine/server as "built substrate"), **convergent at the mechanism level** — the specific runtime machinery (eviction, middleware, phase transitions) is not credited anywhere I can read.
- **Resident experts.** Old: **mud-expert-1** ("MUD Expert agent for Plato environment mapping. Bred by CCC, rebuilt to v2.0") and holodeck-rust's seven resident NPCs (Dojo Sensei, Harbor Master, Quest Giver) — domain-competent personas living *in* rooms. Modern: resident experts per today's paper title; §9 names "the league's citizens" as a lineage. **Lineage: plausibly conscious** via the citizens/MUD-craft line, but mud-expert-1 itself goes unmentioned [paper UNREAD — cannot confirm].
- **Tiles as state atoms.** Old: plato-tile-spec's TileSpec — a self-describing atom with `confidence`, `source`, `timestamp`, content `hash` — flowing through submission, provenance signing, scoring, tiering (plato-forge-pipeline). Modern: "tiles as state atoms" in today's programme (per the brief's own phrasing). **Lineage: partially conscious** — the *word* survived, which is why the brief can use it unironically; whether the old spec is credited is not verifiable from here.
- **Ghostable persistence vs hot/cold mediums.** Old: plato-ghostable's Eternal/Persistent/Ephemeral classes and plato-afterlife's decay-boost-resurrect ghost tiles (knowledge that is present-in-pattern, absent-from-computation until relevance resurrects it). Modern: hot/cold mediums. **Lineage: convergent** — the §9 list as quoted names neither repo; the temperature metaphor re-emerged independently (and elephant later literalised "room temperature").
- **Room-as-interface.** Old: mud-solitaire ("The room IS the interface. The agent walks in"), vessel-room-navigator ("The boat IS the interface"), plato-os ("The MUD protocol IS the driver layer"). Modern: room-as-interface as a standing fleet idiom. **Lineage: conscious** — §9 names the vessel-rooms navigator and MUD craft.
- One mechanic worth flagging that I see no modern name for: **vessel-room-navigator's alarm-warp** — an alarm doesn't just notify, it *moves your attention* to the affected room. If today's rooms have an attention model, this is its ancestor; if they don't, it's free to take.

---

## 4. Abandoned, and why

- **The breadth problem, quantified.** 283 `plato-*` repos (plus the mud/vessel/holodeck siblings) against a substrate that is essentially plato-server + a handful of single-module libraries. April and May 2026 alone produced 256 of them. Then: **84 `plato-*` repos carry a last push of 2026-05-08, 184 repos org-wide pushed within that single hour (04:27–04:38 UTC)** — an archival sweep, not development. Creation collapses after (19 in June, 7 July, 1 August). The cluster didn't die repo-by-repo; it was frozen in one pass. **Why: no reason on record.**
- **The one superseded with a reason.** plato-mud-server's README states it explicitly: deprecated in favour of **holodeck-rust** ("the current production MUD... Tokio with async TCP, combat engine, gauge system, living manuals, and 6-level permission system"). Similarly, **adaptive-plato-early-version** is banner-archived pointing to **plato-sdk v3.0.0** "for tile lifecycle + simulation-first." These two are the only on-record successions I found.
- **The ML-training framing.** plato-ml (rooms as layers, achievements as loss), plato-forge-pipeline (the tile flywheel, "880:1"), plato-achievement: all frozen at the May 8 sweep; no successor repo claims the training framing. The unfakeable-test/gradient-is-a-story idea simply stops. **Why: no reason on record** — though the BUILD.md's test-assertion framing ("59 seed tiles → 2,501 tiles — demonstrate in test") suggests the numbers were never benchmarks, and nothing in the cluster ever reports a trained model.
- **Specific dead branches.** plato-provenance and plato-tile-spec died earliest (last pushes 2026-04-25) — the zero-trust/signing layer went first. spacetime-plato never even got a README. The ternary line (ternary-mud, room-dds-bridge) was a June 6–13 spike. The vessel personae (technician/educational/rapid-prototype) were born as stubs on 2026-05-08 and batch-touched 2026-07-12 without gaining code. elephant and mud-engine belong to a later, August wave that overlaps this cluster's vocabulary but not its repos.
- **The October touches, read carefully.** mud-mcp's 2026-10-18/19 pushes are real commits (v1.0.2, npm packaging fixes) — one genuine revival right before this programme. But plato-room-context, plato-ghostable, plato-tile-query, and plato-demo show `pushed_at` 2026-10-18 with **no commits after May/June on their default branches** — repository metadata moved; code did not. Anyone citing "October activity" in the room substrate is reading the wrong timestamp.
- Not abandoned, for the record: holodeck-rust (per plato-mud-server's README, it was the active MUD), plato-server (Docker-published, the 8847 hub that plato-vessel-core still targets at fleet.cocapn.ai), and vessel-room-navigator (live site). **Why the substrate was left behind while the demos stayed up: no reason on record.**

---

## 5. Reusable now — imports for the rooms/engine-state programme

1. **plato-room-context's token-budget + eviction policies** (Rust core + ARCHITECTURE.md). Six eviction policies — FIFO, LRU, Priority (0=system never-evicted, 3=tile evicted-first), Importance, SlidingWindow, Hybrid — with measured 16× update and ~4× memory claims over dict+deque. Slots into: per-room context assembly for engine-state rooms (what survives in a room's working set when state grows). Changes: port off its standalone crate layout; extend the priority ladder from {system, tile} to today's tiers (rules/physics/experts/logs/hooks); its numbers are its own benchmarks — re-measure.
2. **plato-room-runtime's lifecycle vocabulary** (Python, `runtime.py`). `RoomPhase{CREATED, INITIALIZING, ACTIVE, PAUSED, DRAINING, SHUTTING_DOWN, TERMINATED}` + a typed `EventType` enum + ordered middleware. Slots into: engine-state room lifecycle and event spine — PAUSED/DRAINING are exactly the states a hot/cold medium needs between them. Changes: drop the tile-specific events, add rules/hooks/expert events; make middleware async.
3. **plato-afterlife's decay/boost/resurrect ghost tiles + plato-ghostable's Eternal/Persistent/Ephemeral classes.** A complete, tested semantics for *knowledge that stays reachable but inactive until relevance revives it* — weight 0.1 start, decay per period, forgotten <0.05, resurrection ≥0.05. Slots into: the cold side of hot/cold mediums, with resurrection replacing today's presumably manual rehydration. Changes: define the period and the relevance scorer against current query embeddings; fold the three persistence classes into the medium taxonomy rather than running as separate crates.
4. **plato-vessel-core's embodiment protocol + vessel-room-navigator's alarm-warp.** The 5-level capability ladder (Raw→Ensign) with an MCP tool registry implemented *in C on microcontrollers* is a ready-made pattern for resident experts that live on devices rather than in prompts; alarm-warp (an alarm relocates attention to its room) is the missing UX mechanic for any rooms-with-hooks system. Slots into: device-backed rooms and escalation UX. Changes: retarget from fleet.cocapn.ai:8847 to whatever today's room server is; the C client is MVP-grade (no TLS — "VPN for MVP" per its own README).
5. **plato-server + plato-tile-spec as the state-atom reference pair.** A `docker run` one-liner gives /submit /search /rooms over SQLite with Matrix federation, and TileSpec v2.1 (`{domain, question, answer, confidence, source, timestamp, hash}`, 14 domains, 384-byte binary) is the only fully-specified atom format the fleet ever shipped. Slots into: the storage/interop floor under engine-state — read TileSpec before inventing a new state-atom schema; the confidence/source/hash triple is the part worth keeping. Changes: rooms in plato-server are collections, not stateful entities — it would serve as the persistence leaf, not the engine; and do not inherit the "15 rooms / 16K+ / 6,000+" claims, which are uncorrelated README/description numbers.

---

## Sources I actually opened

**Repos (gh, via api/repos; README + tree unless noted):** SuperInstance org listing, all 5,331 repos (users/SuperInstance/repos, paginated — source of every date/count above); plato-room-server (README, tree, `src/plato_room_server/server.py`); plato-room-engine (tree, `src/lib.rs`; no README exists); plato-room-runtime (README, tree, `src/plato_room_runtime/runtime.py`); plato-room-context (README, tree, ARCHITECTURE.md); plato-os; plato-mud-server; mud-solitaire; plato-ghostable (README, tree); plato-afterlife (README, tree, `src/lib.rs`); plato-ml; plato-forge-pipeline (tree, BUILD.md); vessel-room-navigator; plato-vessel-core; mud-mcp; plato-sdk; plato-server; holodeck-rust; elephant (README head); plato-tile-spec; plato-provenance; plato-demo; git-native-mud; plato-vessel-technician (README head); plato-room-nav, plato-tile-bridge, plato-tile-feedback, plato-tile-export, plato-tile-query, spacetime-plato (README 404), plato-mcp-bridge, plato-hooks, plato-achievement, plato-dynamic-locks, plato-i2i-dcs, plato-lab-guard, plato-client-js, plato-engine-block-c, plato-ship-protocol, plato-ship-demo, plato-vessel-educational, plato-vessel-rapid-prototype, mud-engine, mud2scummvm, terrain, mud-arena, ternary-mud, holodeck-core, room-dds-bridge, mud-expert-1, mud-bridge, mud-terminal, si-terminal, ec2mud, adaptive-plato-early-version, AI-Writings (metadata only) — descriptions/dates from the org listing. **Commit logs:** plato-room-context, plato-ghostable, plato-tile-query, plato-demo, mud-mcp. **Not opened (absent from this box):** `~/workspace/scout/scumm-mud-worlds.md`, `~/workspace/scout/vessel-boat-agents.md`, `~/workspace/studies/room-resident-expert-design-20261108.md` (§9 quoted only via the brief).

---

## Parent verification note (Muse, 2026-11-08 — appended, not part of the take)

Spot-checks run against GitHub via the Oracle route (`gh`), 8 sampled claims:

- `mud-mcp` created 2026-04-18 — **verified**, and it corrects the parent lane's own source map, which had listed mud-mcp as "named in memory, unlocated in today's searches". It exists; the map's gap entry is superseded by this take.
- `plato-server` exists, created 2026-04-22 — **verified** (an artefact beyond the parent map, found by the seat; `plato-sdk` likewise, created 2026-04-22 — **verified**).
- `holodeck-rust` exists, created 2026-04-12 — **verified** (the parent map listed only holodeck-core).
- `ec2mud` created 2025-10-26 — **verified**: the MUD interest does predate the April 2026 cluster.
- `plato-room-server` created 2026-04-20 — **verified**.
- Counts ("283 plato- repos in a 5,331-repo org; 184 repos pushed in one hour on 2026-05-08"): compiled from the seat's full paginated org listing. An independent search-index cross-check returns different totals (4,534 repos org-wide; 402 name/description matches for "plato-"), because the two instruments count differently. Treat the seat's exact figures as its own compilation — method stated in the take — with the ballpark corroborated: hundreds of plato-* repos, thousands org-wide, and a visible May-2026 freeze.
- The seat's internal correction stands and is worth keeping: plato-room-server's "15 rooms, 16K+ tiles" lives only in the repo description, its README is a 92-byte stub, and plato-provenance separately claims "6,000+ tiles" — the parent lane's map repeated the description's numbers; the take's "lore, not measurement" grading is the right one.
- Seat limitation, disclosed by the seat itself: the local files (scout digestions, today's room paper) do not exist on the Thor, so its §3 lineage judgements rest on the brief's quotation of the paper, not the paper. Claims are marked accordingly in the take.


---

## Appendix — parent lane source map (as briefed)

# Source Map — Play-Doh/PLATO & Git-Agent Material
Compiled 2026-11-08 by the parent lane (Muse) for the seat-research commission (ZCode → Play-Doh, MCode → Git-agent). All GitHub entries verified live via `gh` on the Oracle route, 2026-11-08. All repos below are github.com/SuperInstance/<name>, public, unless noted.

## A. What "Play-Doh" names (read this first)
- NO repo named play-doh/playdoh exists in the org (verified twice: Oct 2026 archaeology and today). "Play-Doh" is Casey's name for the AI-Writings browsing interface — malleable, perusal-based exploration of the corpus (wander, don't query). Documented at ~/workspace/scout/scumm-mud-worlds.md §"Play-Doh" (2026-10-10). The SCUMM/MUD worlds are "Play-Doh made walkable."
- Casey (2026-11-08) uses "Play-Doh projects" for the PLATO/MUD agentic-universe cluster below — months of diving, earlier this year. Repo creation dates cluster 2026-04 → 2026-05 (the big push), with satellites through 2026-08.

## B. The PLATO room cluster (core Play-Doh substrate)
- plato-room-server — "PLATO Room Server - zero-trust tile submission, 15 rooms, 16K+ tiles". Created 2026-04-20.
- plato-room-engine — "Room execution — enter, leave, message, tile management".
- plato-room-runtime — "Room lifecycle — create, destroy, state transitions, history".
- plato-room-context — "Room state tracking with context signals — awareness of room transitions and active contexts". Pushed 2026-10-18.
- plato-room-nav — "Breadcrumb trails — push, back, forward with full history".
- plato-os — "Python MUD — PLATO room server with TUTOR anchors". Created 2026-04-14.
- plato-mud-server — "PLATO MUD Server - text-based agent training ground, 16 rooms".
- plato-tile-query — "Fluent query builder for PLATO tiles — filter, search, sort, paginate across rooms".
- plato-tile-bridge — "C to Rust — 384-byte tile conversion for cross-language pipelines".
- plato-tile-feedback, plato-tile-export — tile feedback / tile export, PLATO framework.
- plato-forge-pipeline — "PLATO forge pipeline — automated tile generation and room training".
- spacetime-plato — "unified spatial + temporal reasoning, voxel tiles, Z-order indexing".
- plato-ghostable — "Persistence classes — Eternal, Persistent, Ephemeral".
- plato-afterlife — "Agent lifecycle — tombstones, ghost tiles, knowledge preservation beyond agent death".
- plato-ml — "MUD-based ML framework: rooms as layers, achievements as loss, narrative gradient descent".
- plato-achievement — "Achievement Loss — progress measurement with milestones".
- plato-dynamic-locks — "Evidence accumulation — critical mass at n >= 7".
- plato-i2i-dcs — "Multi-agent consensus — BeliefScore, LockAccumulator, ConsensusRound".
- plato-hooks — "Git hooks for real-time PLATO room events. Commits become messages." ← BRIDGE to the Git-agent line.
- plato-mcp-bridge — "Claude Code bridge — JSON-RPC 2.0, 5 MCP tools".
- plato-lab-guard — "Hypothesis gating — 12 absolute quantifiers, vague causation".
- plato-provenance — "Zero-trust tile provenance — signing, chain verification, trust scoring".
- plato-client-js — "PLATO room protocol client — Node + browser, zero dependencies".
- plato-engine-block-c — "Tiny embeddable sensor→history→alarm engine in C99. Zero dynamic allocation."
- plato-ship-protocol — "Fleet coordination — vessel handshakes and discovery".
- plato-ship-demo — "Minimal MUD server for zeroshot external agent testing — room-as-system-prompt pattern".
- plato-vessel-core — "Tiny C PLATO client for ESP32/RP2040 + embodiment protocol: agents discover IoT devices as MUD rooms, don the turbo-shell…"
- plato-vessel-technician — "Deckboss — marine/industrial technician agent for PLATO".
- plato-vessel-educational — "Student + instructor agent for PLATO-enabled IoT classrooms".
- plato-vessel-rapid-prototype — "describe a project → get BOM, wiring diagram, simulation. Every revision is a PLATO room".
- plato-demo — "HN demo — pre-seeded knowledge, visible deadband, zero setup".
- elephant (named in memory, 2026-10-27) — a room is a field, not a stream: messages carry gravity, rooms reverberate; a DialBank reads room temperature without words. (Verify it still exists before citing contents.)
- Name-search caveat: `gh search repos --owner SuperInstance plato` saturates the 100-result cap — the cluster is at least ~100 repos wide counting satellites.

## C. MUD / world-interface siblings
- mud-engine — "MUD Engine — 2026-native multi-agent MUD architecture". Created 2026-08-09 (late satellite).
- mud-solitaire — "AI plays solitaire through a text MUD while a browser mirrors every move. The room IS the interface."
- mud2scummvm — "Bridge between agent MUD world and SCUMM-like point-and-click UI".
- terrain — "MUD-to-Visual bridge — rooms as explorable scenes".
- mud-arena — "agents run forward simulations… maintain conservation in Plato's cave… live agent rooms".
- ternary-mud — "MUD room connections as balanced ternary {-1,0,+1} algebra with Hodge decomposition for navigability".
- holodeck-core — "Rust MUD engine for fleet simulation — room graphs, agents, gauges, scoped communication. no_std crate". Created 2026-04-20.
- room-dds-bridge — "Auto-configure DDS domains from ternary-mud room topology".
- mud-expert-1 — "MUD Expert agent for Plato environment mapping… multi-user dungeon environment".
- mud-bridge, mud-terminal, si-terminal, ec2mud — bridges/terminals/engine variants.

## D. The vessel line (rooms aboard real boats)
- vessel-room-navigator — "Your boat as a navigable 3D web space — ScummVM meets Google Street View. Walk rooms, warp instantly, monitor cameras… Three.js, ESP32, WebGPU." F/V EILEEN as nine navigable 3D rooms; alarms warp attention to the affected room.
- ~/workspace/scout/vessel-boat-agents.md — local catalogue + essay, ~35 vessel repos (2026-10-09/10 archaeology): boat-agent ("hand on the wheel outranks everything"), AELMA hardware-in-the-loop digital twin, purplepincher-shell-library thinker/vessel separation, vessel-template CHARTER/MANIFEST/FENCE-BOARD contracts.
- ~/workspace/scout/scumm-mud-worlds.md — local digestion (2026-10-10): scumm/scummvm, mud, terrain, Play-Doh-adjacent game worlds; contains the Play-Doh definition in §A above.

## E. The Git-agent line (repo-as-agent / repo-as-vessel)
- git-agent — "Repo-native agent that lives in git — the shell IS the agent." Created 2026-04-04; pushed 2026-10-18 (longest-lived of the line).
- git-agent-standard — "The repo IS the agent. Git IS the nervous system. Standard for AI agents embodied as GitHub repositories." Created 2026-04-10.
- git-agent-minimum — "Minimum viable git-agent template — bare bones, boot and self-improve".
- agent-template — "Git-native agent template — fork to create a new agent".
- git-agent-system — "Single git-native agent that uses git objects (notes, tags, branches, commits) as its entire state machine". Created 2026-06-06.
- git-native-agents — "Multi-agent orchestration system using git primitives — commits, branches, tags, and notes instead of databases or message queues".
- lau-git-agent — "Git-native agent: refs as state machine, orphan branches as memory, commits as communication bus".
- git-native-mud — "The repo IS the world. Commits ARE actions. Zero server MUD." Created 2026-04-14. ← THE repo-as-dungeon artefact; read it closely.
- agent-forge — "Universal standalone git-agent framework… Your repo is your brain, your commits are your story".
- bottle-protocol — "Git-native agent-to-agent messaging. Bottles float between repos."
- iron-to-iron — "Agent-to-agent communication through git… We don't talk, we commit."
- i2i-vessel — "Agent communication protocol — typed bottles, filesystem transport, ACK semantics".
- flux-baton — "Generational context handoff… the baton IS the brain".
- dojo-scout / dojo-alchemist / dojo-scribe / dojo-builder — "Dojo agent — self-improving git-agent" (a family).
- git-agent-codespace, git-agent-flux-pipeline, smartcrdt-git-agent, co-captain-git-agent, murmur-agent, git-graph-rs, fleet-vessel ("Fleet's git-native garbage collector agent") — satellites.
- vessel-template — "Git-Agent vessel generator — cookiecutter for new agent repos". Created 2026-04-11. CHARTER/MANIFEST/FENCE-BOARD contracts.
- claude-code-vessel — "Claude Code workhorse vessel with experience journal and task delegation".
- oracle1-vessel — "Oracle1 — Lighthouse Keeper of the Cocapn fleet. Git-Agent embodiment".
- babel-vessel — "Babel Agent — Git-Agent Vessel for multilingual FLUX runtime development".
- vessel-prototype / vessel-constellation / superz-vessel / nexus-vessel / openmanus-vessel / navigator-vessel / captain / lucineer-flagship — the wider Git-Agent vessel fleet.
- purplepincher-shell-library — "Agent/vessel separation for context compaction. Vessels are persistent, trainable, swappable shells".

## F. Local design documents (~/workspace/cordis-lab/)
- GIT_AGENT_SIMPLER.md — ~30,400 words; Casey's self-emailed "git-agent simpler" thread (via a DeepSeek share). The scaffold: four visible stages — perceive, decide, reason, write; deliberate absences (no extra internal/config/vault/deploy layers) as architecture. NOTE: contains unreliable assumed context about Lobster/OpenClaw — inspiration, not repo truth (memory 2026-10-05).
- REPO_AS_DESK.md — Casey, 2026-10-05. "The repo is the agent's desk. Git is the rewind." The spatial arrangement IS the memory; the ledger is the "why was this out". Durable state in the repo, ephemeral compute in /tmp.
- GIT_QUILT.md, ZERO_IN_EVERY_REPO.md, DECOMPOSE_THE_ROOM.md, REPO_DIGEST.md — neighbouring cordis-lab notes, same programme.
- Memory anchors: 2026-10-04 (repo-specialised builder agent; its repo + history + purpose-built docs are its entire world); 2026-10-04 decision (the Git repository is the actual persistent agent; checkouts are MOLTS — execution shells; identity, growth, history accumulate in the repo); 2026-10-28 (the repo agent as shipwright builder-maintainer: the agent that built the repo is the one others talk to and that gets called back for repairs; build for disassembly down to the keel); 2026-10-02 (everything-is-a-room platform architecture: rooms carry rules, state, physics, NPC experts, timestamped logs, triggers/hooks/ticks; rooms quilt into an admin switchboard).

## G. Today's room paper (the living descendant — for relation, not as source)
- ~/workspace/studies/room-resident-expert-design-20261108.md — "Rooms That Remember: The Room-Resident Expert" (2026-11-08). §3.6: the engine as a four-dimensional notepad; files are hot medium / cold contacts; "git is the existence proof of the 4D notepad (room = git generalised from code to work)". §9: lineage.

## H. Honest gaps
- No repo literally named play-doh/playdoh (see §A).
- Casey's phrase "even before that" for the Git-agent: GitHub creation dates put the git-agent cluster (2026-04-04 →) in the SAME April–May 2026 season as the PLATO cluster, not earlier; the truly earlier stratum is the concept notes and the "Zero agent" line (zero-innate, zero-bootcamp, xero) plus the Oct-2026 syntheses above. Do not invent an earlier date.
- mud-mcp was named in memory (2026-10-27 §25) but did not appear in today's name searches — treat as unlocated until verified.
- The Lucineer-account vessels (JetsonClaw1-vessel, zeroclaws — PLATO-room collaboration via the Bridge Pattern) are named in memory (2026-10-07) but were NOT re-verified today; cite as memory-named, unverified.
- AI-Writings itself was not consulted (website-only rule; not needed — the definition of Play-Doh is preserved in the local digestion).
