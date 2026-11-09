# BRIEF — ZCode seat take: the Play-Doh / PLATO agentic universe (research, read-only)

You are ZCode (GLM), a research seat. Casey (the user) directed today, 2026-11-08: "a Z code and an M code could also research our old Play-Doh projects — we spent months diving into Play-Doh as an agentic universe earlier this year." Your take will be filed, attributed to you, as a research document on the fleet's studies shelf, feeding today's rooms / engine-state programme. Work READ-ONLY. Do not modify anything. Your entire answer is the deliverable: output it as one complete markdown document in your reply (no preamble, no "here is…", the document itself).

## Sources (start from the parent lane's source map — it is pasted in full at the end of this brief)
Key anchors you must actually read (use `gh repo view SuperInstance/<name>` and fetch READMEs via `gh api repos/SuperInstance/<name>/readme -q .content | base64 -d`, or clone read-only into /tmp if you need trees; gh on this box is logged in as SuperInstance):
- plato-room-server, plato-room-engine, plato-room-runtime, plato-room-context (the room substrate)
- plato-os, plato-mud-server, mud-solitaire (the MUD face)
- plato-ghostable, plato-afterlife (persistence + agent lifecycle)
- plato-ml, plato-forge-pipeline (rooms as training machinery)
- vessel-room-navigator + plato-vessel-core (rooms aboard a real vessel; devices as rooms)
- ~/workspace/scout/scumm-mud-worlds.md and ~/workspace/scout/vessel-boat-agents.md (local digestions, on this box)
- ~/workspace/studies/room-resident-expert-design-20261108.md §9 ONLY (today's lineage claim — to test against the artefacts, not to copy)

## Answer these, in the artefacts' own terms, citing repo names / file paths for every claim
1. WHAT IT WAS: the design intent of the Play-Doh/PLATO agentic universe as the artefacts themselves state it. Include the naming truth: no repo is named play-doh — what "Play-Doh" actually names (per the local digestion), and how Casey's broader use of the word (the whole PLATO/MUD universe) relates to that original definition.
2. WHAT WAS ACTUALLY BUILT: an inventory, grouped (room substrate / tiles / MUD interfaces / lifecycle & persistence / vessel embodiments / bridges & protocols), each entry one line: what it does, and its state as far as you can evidence it (dates, README claims vs code presence). Distinguish shipped-and-described from stub-from-description.
3. CONCEPTS LIVE TODAY: which ideas from this universe are visibly alive in the fleet's current rooms/engine-state work (rooms carrying rules/state/physics/experts/logs/hooks; resident experts; tiles as state atoms; ghostable persistence classes vs today's hot/cold mediums; room-as-interface). For each: the old artefact, the concept, the modern descendant — and whether the lineage looks conscious (named in today's paper) or convergent.
4. ABANDONED, AND WHY: what was left behind (the breadth problem — the cluster's repo count; the ML-training framing; specific dead branches), with evidence (dates, archive state, superseding artefacts) rather than vibes. Where you cannot evidence a "why", say "no reason on record".
5. REUSABLE NOW: concrete imports for the rooms/engine-state programme — named artefacts or mechanisms, what each would slot into, and what would have to change. Ranked, top 5 maximum. Be specific enough that a builder could start from your list.

## Rules
- Every factual claim about a repo must name the repo. If you could not open a source, mark the claim [UNREAD — from description only].
- Do not invent dates, counts, or contents. The room server's "15 rooms, 16K+ tiles" is its own README/description claim — attribute it as such.
- Length: substance over ceremony; roughly 2,500–4,500 words.
- End with a section "## Sources I actually opened" listing each repo/file you read.

---

## SOURCE MAP (parent lane, 2026-11-08 — verified via gh + local files)

### A. What "Play-Doh" names
- NO repo named play-doh/playdoh exists in the SuperInstance org (verified Oct 2026 and 2026-11-08). "Play-Doh" is Casey's name for the AI-Writings browsing interface — malleable, perusal-based exploration (wander, don't query). Documented at ~/workspace/scout/scumm-mud-worlds.md §"Play-Doh" (2026-10-10). The SCUMM/MUD worlds are "Play-Doh made walkable."
- Casey (2026-11-08) uses "Play-Doh projects" for the PLATO/MUD agentic-universe cluster below. Repo creation dates cluster 2026-04 → 2026-05, satellites through 2026-08.

### B. PLATO room cluster (all github.com/SuperInstance, public)
plato-room-server — "PLATO Room Server - zero-trust tile submission, 15 rooms, 16K+ tiles", created 2026-04-20. plato-room-engine — "Room execution — enter, leave, message, tile management". plato-room-runtime — "Room lifecycle — create, destroy, state transitions, history". plato-room-context — "Room state tracking with context signals", pushed 2026-10-18. plato-room-nav — breadcrumb trails with full history. plato-os — "Python MUD — PLATO room server with TUTOR anchors", created 2026-04-14. plato-mud-server — "text-based agent training ground, 16 rooms". plato-tile-query — fluent query builder for PLATO tiles across rooms. plato-tile-bridge — C to Rust, 384-byte tile conversion. plato-tile-feedback, plato-tile-export. plato-forge-pipeline — automated tile generation and room training. spacetime-plato — spatial + temporal reasoning, voxel tiles, Z-order indexing. plato-ghostable — persistence classes Eternal / Persistent / Ephemeral. plato-afterlife — tombstones, ghost tiles, knowledge preservation beyond agent death. plato-ml — rooms as layers, achievements as loss, narrative gradient descent. plato-achievement — achievement loss, milestones. plato-dynamic-locks — evidence accumulation, critical mass at n>=7. plato-i2i-dcs — multi-agent consensus (BeliefScore, LockAccumulator, ConsensusRound). plato-hooks — git hooks for real-time PLATO room events; commits become messages. plato-mcp-bridge — Claude Code bridge, JSON-RPC 2.0, 5 MCP tools. plato-lab-guard — hypothesis gating. plato-provenance — zero-trust tile provenance, signing, chain verification. plato-client-js — room protocol client, zero dependencies. plato-engine-block-c — embeddable sensor→history→alarm engine in C99. plato-ship-protocol — vessel handshakes and discovery. plato-ship-demo — room-as-system-prompt pattern. plato-vessel-core — ESP32/RP2040 PLATO client + embodiment protocol: agents discover IoT devices as MUD rooms, don the turbo-shell. plato-vessel-technician, plato-vessel-educational, plato-vessel-rapid-prototype (every revision is a PLATO room). plato-demo — HN demo, visible deadband. elephant (memory-named) — a room is a field, not a stream; DialBank reads room temperature. Name-search for "plato" saturates the 100-result cap.

### C. MUD / world-interface siblings
mud-engine (created 2026-08-09, "2026-native multi-agent MUD architecture"), mud-solitaire (the room IS the interface), mud2scummvm, terrain (rooms as explorable scenes), mud-arena, ternary-mud (room connections as ternary algebra), holodeck-core (Rust MUD engine, room graphs, created 2026-04-20), room-dds-bridge, mud-expert-1, mud-bridge, mud-terminal, si-terminal, ec2mud.

### D. Vessel line
vessel-room-navigator — F/V EILEEN as nine navigable 3D rooms; alarms warp attention to the affected room. Local catalogue: ~/workspace/scout/vessel-boat-agents.md (~35 vessel repos). Local digestion: ~/workspace/scout/scumm-mud-worlds.md.

### E. Today's paper
~/workspace/studies/room-resident-expert-design-20261108.md — §9 lineage names: everything-is-a-room architecture (2026-10-02), plato-room-engine/server as built substrate, vessel-rooms navigator, MUD craft, character-folder doctrine, the league's citizens.

### F. Honest gaps
No play-doh repo. mud-mcp named in memory but unlocated in today's searches. Lucineer-account vessels memory-named, unverified today.
