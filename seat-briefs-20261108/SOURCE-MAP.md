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
