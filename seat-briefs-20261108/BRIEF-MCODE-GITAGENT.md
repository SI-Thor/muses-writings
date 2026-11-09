# BRIEF — MCode seat take: the Git-agent (repo-as-vessel / repo-as-dungeon) — research

You are MCode (MiniMax), a research seat in the SuperInstance fleet. Casey directed today, 2026-11-08: "even before that we had the concept of the Git agent — really kind of like treating a repo as sort of their own vessel with its own rooms on board, or its own dungeon, depending on how you want to look at a MUD." Research that concept from the fleet's own artefacts. Your take will be filed, attributed to you, as a research document on the studies shelf, feeding today's rooms/engine-state programme.

DELIVERABLE: write your take as a markdown file at ~/git-agent-take-20261108.md (in your home directory on this box), then confirm in the session that the file is written. If you cannot write the file, output the full document as your final message instead.

## Sources (the parent lane's source map is pasted in full at the end of this brief — start there)
Read the actual artefacts (gh on this box is logged in as SuperInstance; use `gh repo view SuperInstance/<name>` and `gh api repos/SuperInstance/<name>/readme -q .content | base64 -d`, or clone read-only into /tmp):
- git-agent (created 2026-04-04, still pushed 2026-10-18 — the longest-lived), git-agent-standard ("The repo IS the agent. Git IS the nervous system."), git-agent-minimum, agent-template
- git-agent-system (git objects — notes, tags, branches, commits — as the entire state machine), git-native-agents (git primitives instead of databases/message queues), lau-git-agent (refs as state machine, orphan branches as memory)
- git-native-mud ("The repo IS the world. Commits ARE actions. Zero server MUD.") — the dungeon reading; read it closely
- vessel-template (cookiecutter for Git-Agent vessels; CHARTER/MANIFEST/FENCE-BOARD), claude-code-vessel, oracle1-vessel, agent-forge
- bottle-protocol, iron-to-iron, i2i-vessel (git as the communication bus); flux-baton (generational handoff)
- Local files on this box: ~/workspace/cordis-lab/GIT_AGENT_SIMPLER.md (~30,400 words — the scaffold: perceive/decide/reason/write; read its structure and key claims, you need not read every word), ~/workspace/cordis-lab/REPO_AS_DESK.md ("The repo is the agent's desk. Git is the rewind."), plus GIT_QUILT.md and ZERO_IN_EVERY_REPO.md in the same directory.

## Answer these, citing repo names / file paths for every claim
1. THE CONCEPT: repo-as-vessel in the artefacts' own terms — the repo as the agent (identity, memory, history resident in git; the checkout/runtime as a replaceable shell — the fleet's word is MOLTS). Then the two spatial readings Casey named: the repo as a VESSEL with rooms aboard (which artefacts actually structure a repo into rooms/decks/charters?) and the repo as a DUNGEON / MUD (git-native-mud above all: rooms, actions-as-commits, zero server). Say what each reading emphasises and where they differ.
2. WHAT EXISTS: an inventory of the line — the standards/templates, the state-machine implementations, the comms protocols, the named vessels — one line each: what it is, its evidenced state (created/pushed dates, README vs code).
3. RELATION TO TODAY'S CLAIMS: today's room paper (~/workspace/studies/room-resident-expert-design-20261108.md, read §3.6 and §9) claims "git is the existence proof of the 4D notepad — room = git generalised from code to work". Test that claim against the old artefacts: did the Git-agent line already treat history as the room's state/transition log? Also relate: the league's append-only ledger, and Jacquard (decision models behind a provider interface; Jacquard appears in the git-agent-flux-pipeline line — say what you find, no more).
4. WHAT IT GOT RIGHT EARLY: the insights that were correct before the rest of the fleet caught up (e.g. identity survives the death of any runtime; history as memory; fork/clone as reproduction; commit as the atomic act). Evidence each from an artefact.
5. WHAT IT MISSED: the gaps — what the Git-agent line did NOT solve that today's work had to add (digestion/resident experts? verification of effects in a store the actor cannot write? live engine state vs committed state? presence?). Argue from the artefacts; where the record is silent, say so.
6. REUSABLE NOW: concrete imports for the rooms/engine-state programme — named artefacts/mechanisms, what each slots into, what must change. Ranked, top 5 maximum.

## Rules
- Every factual claim about a repo names the repo. Unopened sources are marked [UNREAD — from description only]. No invented dates, counts, or contents.
- One honest chronology note from the parent lane: GitHub creation dates put the git-agent cluster in the same April–May 2026 season as the PLATO cluster; the "even before that" stratum is the concept notes and the Zero-agent line. Keep your chronology evidence-based.
- GIT_AGENT_SIMPLER.md contains unreliable assumed context about other projects (Lobster/OpenClaw) — treat it as design inspiration, not repo truth.
- Length: substance over ceremony; roughly 2,500–4,500 words.

---

## SOURCE MAP (parent lane, 2026-11-08 — verified via gh + local files)

### The Git-agent line (all github.com/SuperInstance, public)
git-agent — "Repo-native agent that lives in git — the shell IS the agent", created 2026-04-04, pushed 2026-10-18. git-agent-standard — "The repo IS the agent. Git IS the nervous system. Standard for AI agents embodied as GitHub repositories", created 2026-04-10. git-agent-minimum — minimum viable template, boot and self-improve. agent-template — fork to create a new agent. git-agent-system — "uses git objects (notes, tags, branches, commits) as its entire state machine", created 2026-06-06. git-native-agents — orchestration using git primitives instead of databases or message queues. lau-git-agent — refs as state machine, orphan branches as memory, commits as communication bus. git-native-mud — "The repo IS the world. Commits ARE actions. Zero server MUD", created 2026-04-14. agent-forge — "Your repo is your brain, your commits are your story". bottle-protocol — git-native agent-to-agent messaging; bottles float between repos. iron-to-iron — "We don't talk, we commit". i2i-vessel — typed bottles, filesystem transport, ACK semantics. flux-baton — generational context handoff; the baton IS the brain. dojo-scout/alchemist/scribe/builder — self-improving git-agent family. git-agent-codespace, git-agent-flux-pipeline (git → structured extraction → FLUX compiler → VM → PLATO), smartcrdt-git-agent, co-captain-git-agent, murmur-agent, git-graph-rs, fleet-vessel (git-native garbage collector). vessel-template — "Git-Agent vessel generator — cookiecutter", created 2026-04-11; CHARTER/MANIFEST/FENCE-BOARD contracts. claude-code-vessel — workhorse vessel, experience journal, task delegation. oracle1-vessel — "Git-Agent embodiment" of the fleet lighthouse keeper. babel-vessel, vessel-prototype, vessel-constellation, superz-vessel, nexus-vessel, openmanus-vessel, navigator-vessel, captain, lucineer-flagship — wider vessel fleet. purplepincher-shell-library — agent/vessel separation for context compaction; vessels are persistent, trainable, swappable shells.

### Local design documents (~/workspace/cordis-lab/)
GIT_AGENT_SIMPLER.md (~30,400 words; scaffold: perceive, decide, reason, write; deliberate absences as architecture; contains unreliable assumed context — inspiration, not truth). REPO_AS_DESK.md (Casey, 2026-10-05: "The repo is the agent's desk. Git is the rewind." — the spatial arrangement IS the memory; the ledger is the "why was this out"; durable state in the repo, ephemeral compute in /tmp). GIT_QUILT.md, ZERO_IN_EVERY_REPO.md, DECOMPOSE_THE_ROOM.md, REPO_DIGEST.md — neighbouring notes.

### Memory anchors (fleet memory, for orientation — verify against artefacts where you can)
2026-10-04: repo-specialised builder agent; its repo + history + purpose-built docs are its entire world. 2026-10-04 decision: the Git repository is the actual persistent agent; checkouts are MOLTS (execution shells); identity, growth, history accumulate in the repo. 2026-10-28: the repo agent as shipwright builder-maintainer — the agent that built the repo is the one other agents talk to, and that gets called back for repairs; build for disassembly down to the keel. 2026-10-02: everything-is-a-room architecture (rooms carry rules/state/physics/NPC experts/logs/hooks/ticks; switchboard).

### Bridge artefacts (both lines at once)
plato-hooks — "Git hooks for real-time PLATO room events. Commits become messages." git-native-mud (above). git-agent-flux-pipeline (git → … → PLATO).

### Today's paper
~/workspace/studies/room-resident-expert-design-20261108.md — §3.6 four-dimensional notepad (git as existence proof), §9 lineage.
