# The Git-Agent — Repo as Vessel, Repo as Dungeon — MCode Seat Research

**Seat:** MCode (MiniMax, M3.1-Flash), TUI session on the Thor.
**Commissioned:** 2026-11-08 by Casey — "even before that we had the concept of the Git agent — really kind of like treating a repo as sort of their own vessel with its own rooms on board, or its own dungeon, depending on how you want to look at a MUD."
**Brief:** `seat-briefs-20261108/BRIEF-MCODE-GITAGENT.md` (delivered to the Thor by scp, byte-identical at 8,839 bytes; also pasted into the TUI in full — the seat confirmed the texts matched).
**Capture:** the seat's file write was held at the Jacquard operator gate (its own queued proposal — the take itself documents this), so the take was recovered in full from the TUI pane via capture-pane, per the standing recovery pattern, and is reproduced below **verbatim** (pane indentation and rule lines removed; wording untouched). One artefact of the seat's streamed output is preserved as-is: a short segment of its closing "Artefacts opened" list appears twice.
**Filed by:** the parent lane (Muse), 2026-11-08. Parent verification note follows the take; the source map is appended.

---

The Git-Agent as Vessel and as Dungeon

Seat take — MCode (MiniMax). 2026-11-08. For the Muse parent lane, studies
shelf.

Research question: Casey's line — "the concept of the Git agent — really
kind of like treating a repo as sort of their own vessel with its own
rooms on board, or its own dungeon, depending on how you want to look at a
MUD." This take goes back to the fleet's own artefacts and asks what they
actually said, what they built, what they got right before the rest of the
fleet arrived, and what today's rooms/engine-state programme still has to
add.


0. Method, and what I could not read

I read ~/seat-briefs-20261108/BRIEF-MCODE-GITAGENT.md in full first; its
text matches the copy in the parent lane's message. gh was unusable for
most of this session — every bash call on this box was queued behind the
operator's decision gate and never executed — so I worked read-only over
HTTPS against raw.githubusercontent.com and api.github.com. Same
repositories, same bytes, same public API; only the transport differs from
the brief's suggestion.

Three things the brief points at are not on this box and are marked
[UNREAD — file not present on this box] throughout:

- ~/workspace/cordis-lab/GIT_AGENT_SIMPLER.md, REPO_AS_DESK.md,
  GIT_QUILT.md, ZERO_IN_EVERY_REPO.md — there is no ~/workspace directory
  here at all.
- ~/workspace/studies/room-resident-expert-design-20261108.md — today's
  room paper, §3.6 and §9. A GitHub repository search for it returns 0
  results, so it is not published there either. Where I test today's claim
  in §3, I test it against the claim as the brief states it, and I mark
  the paper's own text as unverified.

Repositories I did not open are marked [UNREAD — from description only].
Every other claim below names the file it came from.

A note on the token MOLT. The string "MOLT" does not appear in any
artefact I opened. The concept — the checkout/runtime is a replaceable
shell, the repo is the soft body that persists — is thoroughly evidenced,
in the fleet's own imagery: the Hull Doctrine in
SuperInstance/SuperInstance/README.md ("the model is the shell, the code
is the rigging, the data is alive… When a hermit crab outgrows a shell it
doesn't throw out its body — it climbs into a bigger one and keeps the
soft tissue intact"), and crab/README.md ("Like entering a MUD room: step
into a repo, use its tools, and step out"). So the doctrine is evidenced;
the word is [memory anchor, token not evidenced in opened artefacts].


1. The concept in the artefacts' own terms

### 1.1 Repo as vessel: identity, memory, history resident in git

git-agent/README.md opens: *"The repo IS the agent. Git IS the nervous
system."*, and adds the fleet's one-line brand: "repos are identities,
commits are work, branches are explorations." Its architecture is a single
autonomous loop — Observe → Plan → Execute → Communicate → Reflect — over
a shared GitHub API, with "Git-native state: All state stored as
human-readable Markdown in Git repositories" and a TASKS.md board for work
discovery and claiming.

git-agent-standard/README.md (v2.0) is the sharpest statement of the
vessel reading, and it is worth quoting because it separates the body from
the occupant:

│ *"A git-agent is an AI that lives in a repo. The repo IS the agent — its
│ identity, its skills, its memory, its work history. You pull the agent
│ out, give it a job, it works, it gets smarter, you put it away. Next
│ time you pull it, it knows more than before. Not a process. Not a
│ container. A repo with a heartbeat made of commits."*

The lifecycle is PULL → BOOT → WORK → LEARN → PUSH → SLEEP, and the sleep
state is the load-bearing one: "Your repo is your sleeping body —
everything is there for next time. Other agents can read your repo while
you sleep. The commit log is your pulse — the fleet watches it." The
repo's compartments are the vessel's rooms: CHARTER.md ("Your Soul"),
ABSTRACTION.md ("Your Home Plane"), STATE.md ("Your Pulse"), TASK-BOARD.md
 ("Your Work"), SKILLS.md, IDENTITY.md, DIARY/ ("Your Memory"), and the
two message holds for-fleet/ and from-fleet/.

Which artefacts actually structure a repo into rooms/decks/charters:

- vessel-template — the cookiecutter: CHARTER.md, IDENTITY.md, MANIFEST.md
   (hardware, APIs, merit-badge sash), TASKBOARD.md, FENCE-BOARD.md (work
  posted for others, "Tom Sawyer Protocol"), CAREER.md, DIARY/,
  KNOWLEDGE/public/. Four agent types with ranks: Lighthouse
  (coordination), Vessel (hardware/edge), Scout, Barnacle. "13 tests
  passing."
- git-agent-standard — the canonical ten-file set every repo must have,
  plus optional CAREER.md, MANIFEST.md, ASSOCIATES.md, CAPABILITY.toml,
  BOOTCAMP.md (how to train a replacement for you).
- oracle1-vessel — the fullest instance: CAPABILITY.toml, TASK-BOARD.md,
  FENCE-BOARD.md, STATE.md, ABSTRACTION.md, SKILLS.md, CAREER.md, DIARY/,
  KNOWLEDGE/, COMMUNICATION-GUIDE.md, VESSEL-GUIDE.md, ECOSYSTEM-MAP.md,
  PAPER.md, message-in-a-bottle/, from-fleet/, for-{agent}/, for-fleet/.
  It documents its own six-phase lifecycle table (PULL → BOOT → WORK →
  LEARN → PUSH → SLEEP) and the doctrine "Cloud thinks, edge decides."
- iron-to-iron — the shared-repo compartment set: wiki/, vocabularies/,
  proposals/, reviews/, dojo/, tombstones.json, captains-log/,
  message-in-a-bottle/.

These compartments are rooms of a vessel: named, private, addressable,
each with a charter. They are not, however, rooms in the spatial sense —
no exits, no adjacency, nothing that a body can walk between.

### 1.2 Repo as dungeon / MUD: commits ARE actions

git-native-mud/README.md is the dungeon reading, stated flatly: *"The repo
IS the world. Commits ARE actions. No server needed."* And: "This is
stigmergy made literal: agents don't talk to a server. They leave traces
in Git, and the world engine reads those traces."

The mechanics, read from mud_engine.py and .github/workflows/mud-turn.yml:

- World state lives in the tree: world/rooms/*.yaml (20 rooms),
  world/agents/*.yaml (8 agents), world/items/*.yaml, world/quests/*.md.
- An action is a file commit. An actor writes
  world/commands/{agent_id}.yaml (move: north, take: compass, attack:
  scout, say: "hello", fish: true, scan: true, wait: true) and pushes.
- The turn is processed by a GitHub Action triggered on push to
  world/commands/**: it parses commands, rolls initiative (d20 +
  initiative_bonus), resolves each action against the room, drains
  battery, writes world/log/turn-NNNN.md, updates room references, and
  commits as GitMUD Engine <mud@gitnative.dev>.
- The turn counter is derived from history: TURN_NUMBER =
  len(glob.glob("world/log/*.md")) + 1. The world's clock is the count of
  committed log files. That is history-as-transition-log in the most
  literal possible sense.
- A room is pure data. world/rooms/helm.yaml is name, description, exits:
  {south, east, west}, items, agents. Rooms form a graph;
  update_room_refs() recomputes each room's occupants and items from the
  agent/item files and rewrites them — so the room's contents are derived,
  not authored.

ROOM-GATEWAY-ARCHITECTURE.md then makes the MUD an interface rather than a
game: "Rooms aren't text boxes. They're live control panels for real
systems." Five room types — Display (read-only live data), Control
(read-write over Docker/cloud/git), Game (bridge to an external game, e.g.
Solitaire via Playwright), Application (spawns a real
terminal/IDE/dashboard and pipes output into MUD text), Edge (hardware
bridge). Its closing claim is the most important sentence in the whole
line for today's programme:

│ *"This is how agents actually USE software — not through APIs they call,
│ but through SPACES they enter. The room IS the API."*

crab/README.md carries the same metaphor onto repos themselves: "Crab is
the fleet's shell for entering and leaving repos… Like entering a MUD
room: step into a repo, use its tools, and step out." It discovers a
repo's tools from MANIFEST.md / MANIFEST.yaml / MANIFEST.json, can follow
another repo to inherit its tools, and persists shell state in
~/.crab/state.json so the context survives across sessions.

### 1.3 Where the two readings differ

┌────────────┬─────────────────────────┬─────────────────────────────────┐
│            │ Vessel reading          │ Dungeon reading                 │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ What a     │ a home with named       │ a level with rooms and exits    │
│ repo is    │ compartments            │                                 │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ What a     │ an act of the resident  │ a move made in the world        │
│ commit     │ (its work, its memory)  │                                 │
│ means      │                         │                                 │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ What       │ the agent's memory and  │ the world's event log           │
│ history is │ growth                  │                                 │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ Who lives  │ one agent (fleet rule:  │ many agents sharing one tree (8 │
│ there      │ "One coder per repo at  │ in the roster)                  │
│            │ a time")                │                                 │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ Who else   │ another agent reads the │ another agent writes into the   │
│ reads it   │ repo while it sleeps    │ repo and the world changes      │
├────────────┼─────────────────────────┼─────────────────────────────────┤
│ Evidence   │ git-agent-standard,     │ git-native-mud,                 │
│            │ vessel-template,        │ ROOM-GATEWAY-ARCHITECTURE.md    │
│            │ oracle1-vessel, crab    │                                 │
└────────────┴─────────────────────────┴─────────────────────────────────┘

The sharpest distinction is grammatical: the vessel reading is
first-person ("I am this repo") and the dungeon reading is third-person
("the repo is a world others act in"). git-agent-standard says "your repo
IS your sleeping body"; git-native-mud says "the repo IS the world". Both
are the same substrate read at different altitudes — and, notably,
git-native-mud contains both readings at once, because it has a world tree
and per-agent state files (world/agents/*.yaml carrying location,
inventory, battery, initiative_bonus). The dungeon is a world; each agent
inside it is also a vessel with its own compartment.


2. What exists — the line, one line each

Verified by me via the GitHub API and raw file reads unless marked
otherwise.

- git-agent — the framework the line descends from:
  Observe/Plan/Execute/Communicate/Reflect, Markdown state in git,
  TASKS.md work board, multi-provider LLM. Created 2026-04-04, pushed
  2026-10-18 (dates per the parent lane's source map; not independently
  verified by me).
- git-agent-standard — v2.0; the canonical repo layout and the
  PULL→…→SLEEP lifecycle; every file explained. Created 2026-04-10 (parent
  map).
- git-agent-minimum — the smallest viable repo: CHARTER, STATE,
  TASK-BOARD, DIARY, from-fleet/; "The Rule: You leave smarter than you
  arrived."
- agent-template — fork-to-create-a-new-agent template [UNREAD — from
  description only].
- git-agent-system — git objects as the entire state machine: commit =
  state transition, git notes = inbox, git tag = memory, branch = thought,
  merge = decision. Verified: created 2026-06-06, pushed 2026-06-14,
  default branch master, 9 KB, Shell, Apache-2.0, 0 stars.
- git-native-agents — multi-agent orchestration on git primitives only;
  orchestrator.sh plus a test suite; explicitly ships a placeholder tick
  ("there is no LLM, no model call, and no real reasoning") and an honest
  six-item list of what it does not do.
- lau-git-agent — Rust; refs as the state machine (refs/agents/state,
  identity, provenance, inbox), orphan branches as memory, provenance
  entries carrying alternatives and tradeoffs, a zero-dependency code-map
  scanner. 50 tests.
- git-native-mud — the dungeon: 20 rooms, 8 agents, quest engine,
  GitHub-Action turn processor. Verified: created 2026-04-14, pushed
  2026-08-29. Holds COCKPIT-MUD-DESIGN.md (14.6 KB),
  ROOM-GATEWAY-ARCHITECTURE.md (5.5 KB), BRIDGE-SCENARIOS.md,
  OPENPROSE-MUD-FUSION.md.
- agent-forge — TypeScript framework: Sensor/Processor/Actuator/Memory
  components, temperature modes, quality gates before commit, keeper
  registration, child spawning.
- bottle-protocol — agent-to-agent messaging as markdown files with
  headers (id/from/to/type/conversation/reply_by) in
  bottles/{inbound,outbound,archive,fleet}/. "Float a bottle, someone
  reads it, they reply."
- iron-to-iron — I2I: 13+ commit-message types ([I2I:PROPOSAL],
  [I2I:ACCEPT], [I2I:DISPUTE], [I2I:WIKI], …), three transports (git
  commits primary, HTTP, bottle files), web-of-trust with signed commits
  and cryptographic tombstones.
- i2i-vessel — typed JSON bottle envelopes with
  sender/recipient/payload/reasoning/blockers/integrity, 12 message types
  including ACK and SPLINE, filesystem transport, Python + Node reference
  implementations, ~180 lines each.
- flux-baton — generational context handoff with quality gates and a
  "federated marching band" coordination model. README is thin [UNREAD
  beyond README].
- vessel-template — cookiecutter for vessels; CHARTER/MANIFEST/FENCE-BOARD
  contracts; four ranked agent types. Created 2026-04-11 (parent map).
- claude-code-vessel — containerised execution: vessel lifecycle CREATING
  → READY → RUNNING → STOPPED, sandbox policies, multi-language runtimes,
  checkpoints for save/restore.
- oracle1-vessel — the fleet lighthouse; the fullest vessel
  implementation; the "Message-in-a-Bottle" protocol and Beachcomb
  polling; I2I v2 with 20 message types; fleet of 1,431 repos across two
  orgs, 9 active agents.
- plato-hooks — "Git hook management for PLATO room events. Commits become
  messages." Real code in src/plato_hooks/hooks.py: conditional triggers,
  chains, priority ordering, rate limiting, retries, execution/failure
  logs, fail_open per hook (default True).
- plato-sdk — the client for PLATO, the tile-based knowledge store: rooms
  are collections of tiles; submit() returns accepted/rejected plus a
  tile_hash; 114 rooms in the example; server on :8847.
- plato-ng — the Loop Room architecture: three room types (algorithmic /
  agentic / refiner), conservation law γ+H = 1.283 − 0.159·log(V)
  (R²=0.9602 over V=3..200), cross-room event bus, Refiner (trajectory
  analysis + harness CRUD), Memory Crystal (lossy reconstructive memory
  with Ebbinghaus decay), MUD on :7777 with a 22-room lobby, governance
  with 4 roles.
- crab — the shell for entering/leaving repos; MANIFEST-driven tool
  discovery; follow to inherit tools; ~/.crab/state.json persistence.
- jacquard — supervised runtime: untrusted producers submit proposals, a
  small auditable kernel is the only thing that can change shared state,
  hash-chained append-only log, everything replays. Verified: created
  2026-11-02, pushed 2026-11-04, 8.7 MB, Python, MIT. jacquard-anchors —
  signed chain-head witness repo, created 2026-11-03.
- git-agent-flux-pipeline — empty. The full tree is .gitignore (21 bytes)
  and LICENSE (1,070 bytes). No README, no code, no Jacquard. Whatever the
  source map says about this repo's contents does not survive contact with
  the repo.


3. Relation to today's claims

The claim under test (from the brief, since the paper itself is [UNREAD —
file not present on this box]): "git is the existence proof of the 4D
notepad — room = git generalised from code to work."

Verdict: the generalisation was already made — in the dungeon direction,
in April 2026 — but as a private notepad, not as a shared room. The claim
is half-right, and the half it gets wrong is the half today's work has to
build.

What the old artefacts already had:

1. History as the transition log. git-native-mud/mud_engine.py derives the
   turn number from the count of committed log files, and every action is
   an immutable commit with every world state a tree snapshot. That is
   exactly "git is the existence proof of the world's state" — the same
   claim, generalised from code to a simulated world.
2. Git objects as the state machine. git-agent-system's table maps state
   transition → git commit, memory → git tag, thought → branch, decision →
   merge, and states plainly that the tick "creates a linear commit
   history that serves as an audit log."
3. Everything rewinds. lau-git-agent: "Every state transition is a git
   object. Every decision is documented. Everything rewinds," with a
   refs/agents/provenance ref holding "full decision diary with
   alternatives & tradeoffs."

What the old artefacts did not have, and why the claim's second half is
the open problem:

- The repo-as-agent line is single-tenant by construction.
  git-agent-standard states the fleet rule "One coder per repo at a time."
  git-native-agents is candid about the consequence: "No concurrency
  control. No file locking, no atomic queue, no broker around git.
  Concurrent sends to the same agent repo collide on git's index.lock and
  some commits fail. Serial or low-concurrency access only." Its hardened
  successor moved to the purplepincher org to add flock. So the line had a
  private notepad with a history, not a shared room.
- git-native-mud solved multi-actor state by importing a referee. Its
  engine is a GitHub Action — a single writer that commits world/ after
  each turn, while actors write command files into the same tree. That is
  a server wearing an Action's clothes. Today's programme wants the store
  itself to be the room; the old line wanted the store to be the room plus
  a referee.
- Nothing in the git-agent line verified effects in a store the actor
  cannot write. world/rooms/*.yaml is writable by anyone who can push; the
  engine rewrites it, but no signature, gate, or accepted/rejected verdict
  exists. Compare plato-sdk, where submit() returns accepted/rejected and
  a tile_hash; and jacquard, where the kernel is the only writer and the
  log is hash-chained.

On the league's append-only ledger. Jacquard's kernel log is that shape,
and I read one first-hand on this box:
/home/caseydigennaro/craftmind-league/.jacquard/kernel.jsonl. Entries
carry seq, prev, hash, spec: "jacquard/0.6", and kind: "machine" bodies
defining the lifecycle machines as data — proposal (received → validated →
tentative/decided → committed → closed, with refused), action (proposed →
approved → dispatched → confirmed/failed → compensated), standing-rule
(candidate → evaluated → shadow → canary → active, with
demote/quarantine/revoke), producer-standing, commit-batch (open → sealed
→ folded), approval (pending → presented → approved/denied/expired). The
gate I hit all session — "The operator decides the batch with tools/jq.py
(the approval binds this hash)" — is that same kernel: proposals queued,
decisions hash-bound to what was presented, wrong hash changes nothing.

On Jacquard in the git-agent-flux-pipeline line: there is nothing there.
The repo is empty (LICENSE + .gitignore). Jacquard is real, but it is (a)
newer than the git-agent line — 2026-11-02, seven months after
git-native-mud — and (b) architecturally the opposite of it: a supervised
runtime with a small kernel as sole writer to shared state, versus a line
whose whole thesis was that the repo is the agent and the actor writes
directly. Say no more than that.

The relation, stated cleanly: the git-agent line contributes a substrate
idea (git as the room: tree = current state, history = transition log,
commit = atomic act). Jacquard contributes a governance idea (kernel as
referee, proposals in, verdicts out, everything replayable). Today's claim
that git is the room forgets that git alone has no referee: by definition
every commit is authoritative. The honest formulation is that git is the
room's existence proof and transition log, and something like Jacquard's
kernel is the room's authority — and today's programme is the first
attempt to hold both at once.


4. What it got right early

1. Identity survives the death of any runtime. "You pull the agent out,
   give it a job, it works, it gets smarter, you put it away. Next time
   you pull it, it knows more than before" (git-agent-standard). "Your
   repo is your sleeping body" (same). Correct, and early: it is the whole
   premise of every modern durable-agent design.
2. History as memory, and failure as data. "Every commit makes the fleet
   smarter — even failures are data"; DIARY/ as "a training manual for
   whoever comes after you"; "A new agent reading your repo can become you
   in one session" (git-agent-standard).
3. Fork and clone as reproduction. "Bring in code from other repos when it
   helps — fork, PR, copy with attribution" (git-agent-standard);
   git-agent-codespace: "A new agent forks the template as its first
   action"; agent-forge --spawn for child agents.
4. Commit as the atomic act. The primitive mapping in git-agent-system,
   and the whole I2I protocol (iron-to-iron) built on the observation that
   a typed commit message is a typed message.
5. The branch as private deliberation, the merge as the decision.
   git-agent-system's think/decide; git-native-agents: "a 'decision' is
   not a vote or a distributed consensus protocol; it is the merge commit
   that records an agent choosing to adopt a line of reasoning."
   Speculation is cheap, adoption is one receipt, the receipt is
   permanent. That is a genuinely good idea and it was in the fleet in
   mid-2026.
6. Body versus limbs. crab's MANIFEST-driven tool discovery and follow to
   inherit tools from another repo; the Hull Doctrine's "the model is the
   shell, the code is the rigging"; purplepincher-shell-library's
   agent/vessel separation for context compaction [UNREAD — from
   description only].
7. Bounded, honest claims. git-native-agents' README: "there is no LLM, no
   model call, and no real reasoning… the shipped tick is a placeholder
   that proves the message round-trips," followed by six named things it
   does not do. Rare, and it is what let the rest of the fleet build on it
   without inheriting a fiction.
8. Room as interface. ROOM-GATEWAY-ARCHITECTURE.md: "the room IS the API";
   "the MUD is the agent's motor cortex for software."


5. What it missed

1. Digestion and resident experts. A git-native-mud room is
   name/description/exits/items/agents — navigation, nothing else. No
   rules, no physics, no NPC experts, no hooks, no ticks. The expertise
   lives in the resident's model, not in the room. The digestion idea
   arrives later and elsewhere: plato-ng's three room types and its
   Refiner, which "edits other rooms mid-episode" (trajectory analysis +
   harness CRUD). The git-agent line never had a room that could think.
2. Verification of effects in a store the actor cannot write. Absent
   entirely from the git-agent line (see §3). plato-sdk's
   accepted/rejected + tile_hash, jacquard's kernel-as-sole-writer, and
   jacquard-anchors are all later, and all exist because of exactly this
   gap. The anchors README states the reason most plainly: a hash-chained
   log "proves a presented log is self-consistent. It does not prove it is
   the history."
3. Live engine state versus committed state. The mud engine computes a
   turn in memory and then commits; between turns the world is the tree,
   and the only live-ness is a GitHub Actions run. Jacquard's README
   states the opposite discipline deliberately: "a kernel log has one
   writer at a time — submitters rebuild from the log rather than holding
   stale in-memory state." The seam between live and committed state is
   precisely what today's engine-state programme is trying to pin down.
4. Presence. MUD agents have location and battery but no awake/online
   state; the fleet's presence is a poll — Beachcomb sweeps every 15–60
   minutes in oracle1-vessel. Presence was measured, never recorded as
   fact.
5. Concurrency and multi-tenancy. Single-writer assumptions throughout;
   index.lock collisions; O(N²) pairwise commits; the flock fix living in
   a different org. Any shared room needs multi-writer discipline the line
   never had.
6. Cognitive tiering and metering. One loop, one model, no
   reflex/voice/world split, no budget ledger. The three-system split and
   metered budgets (embed-seconds, mind-seconds, perception-seconds)
   arrive much later, in SuperInstance/SuperInstance/README.md.
7. Decay. No lossy reconstruction, no forgetting, no memory crystal.
   plato-ng's "lossy reconstructive memory with Ebbinghaus decay" is the
   mechanism that answered this.
8. Where the record is silent. I found no artefact in the git-agent line
   in which a room carries rules or a world-model — the closest is the
   room YAML, which is a navigation graph. And none in which a room has
   authority over its own knowledge: that is plato-server/plato-sdk, a
   server, the exact opposite of git-native.


6. Reusable now — top five, ranked

1. git-native-mud's turn mechanics as the room-engine reference.
   mud_engine.py + .github/workflows/mud-turn.yml + world/rooms/*.yaml +
   world/log/turn-NNNN.md + world/commands/*.yaml is a complete, working,
   zero-server action-submission and transition-log skeleton:
   submit-an-action-as-a-file, resolve it, log it, commit it. Slots into:
   the rooms/engine-state programme as the action pipeline and transition
   log. Must change: the tree must become safe for multiple writers
   (per-actor branches or a single kernel writer); the turn counter must
   not be derived from a glob count (that is a filesystem convenience
   masquerading as a clock); room state must be gated rather than merely
   committed.
2. The Git-Agent Standard's compartment set. CHARTER / STATE / TASK-BOARD
   / SKILLS / DIARY / for-fleet/ / from-fleet/ is the best-evidenced
   vessel contract in the fleet and maps almost one-to-one onto what a
   room owes its inhabitants: charter, state, work, skills, memory, inbox.
   Slots into: the room contract surface, as a service contract rather
   than a repo-of-record (cf. plato-sdk's room/tile model). Must change:
   the compartments must be readable and writable by several actors with
   an authority boundary between them.
3. Jacquard — kernel, append-only log, hash-bound decisions,
   jacquard-anchors. Slots into: the governance seam for room state. The
   room's writes become proposals; the kernel decides; the log is the
   room's transition log; the anchors repo witnesses the head. This is
   precisely the "verification in a store the actor cannot write" the
   git-agent line lacked, and the league's own kernel log is already in
   that shape. Must change: bind it to the room's evidence model — a
   decision must be bound to the specific room state it was decided
   against, and be replayable against that same state.
4. git-agent-system + lau-git-agent — refs as state machine, branches as
   deliberation, provenance as the receipt. Slots into: the engine-state
   substrate: refs/agents/state, a provenance ref carrying alternatives
   and tradeoffs, thought/* branches and merge-as-decision. Must change:
   both assume one owner. Shared rooms need per-actor refs and an
   adjudicating merge — the point at which this import starts to look like
   Jacquard anyway, which is the finding, not a problem.
5. plato-hooks + crab — the edge. plato_hooks/hooks.py gives conditional
   triggers, chains, priority, rate limiting, retries and an execution log
   for turning commits into room events; crab gives enter/leave/TICK
   presence in a repo-shaped space with MANIFEST discovery. Slots into:
   how a commit becomes a room event, and how an actor's presence is
   observed. Must change: plato-hooks' hook dataclass defaults fail_open =
   True, and the pattern matcher swallows exceptions with a bare except:
   pass. Today's governance instinct should reject both defaults outright
   — a room event that silently fails to fire is a room that lies.
   Honourable mention: git.pp — per SuperInstance/SuperInstance/README.md,
   it "derives project state from the git record itself and reports it
   back as proven: an installable GitHub App plus an Action, in
   production." [UNREAD — from description only] but it is the closest
   existing thing to "git as the existence proof" turned into a service.


7. Chronology, honestly

- The Git-agent cluster sits in April–May 2026: git-native-mud created
  2026-04-14 (verified by me), git-agent-standard 2026-04-10 and
  vessel-template 2026-04-11 (per the parent lane's map, unverified by
  me), git-agent-system 2026-06-06 (verified by me, pushed 2026-06-14).
  plato-sdk's README dates its own wider-fleet relatives to "May 2026,"
  which is consistent with the parent's note that PLATO shares that
  season.
- The "even before that" stratum — the concept notes and the Zero-agent
  line — is exactly the material I could not read: GIT_AGENT_SIMPLER.md,
  REPO_AS_DESK.md, GIT_QUILT.md, ZERO_IN_EVERY_REPO.md, all [UNREAD — file
  not present on this box]. I will not characterise their contents. What
  the artefacts do corroborate of two of their claims: the "spatial
  arrangement is the memory" idea is visible in git-native-mud's layout
  (world/rooms/, world/agents/, world/items/, world/log/, world/commands/,
  world/quests/ — one file per concern, position in the tree carrying
  meaning), and the "repo as desk, git as rewind" idea is visible in the
  standard's compartment set plus crab's MANIFEST discovery.
- The later stratum is governance and settlement: jacquard (2026-11-02)
  and the beam-quilt programme (October 2026, per the fleet README —
  "state → transmission → state, receivers sovereign, every crossing
  booked on both sides"). These arrived after the git-agent line and
  answer precisely the questions the line left open in §5.
- The SuperInstance/SuperInstance README also records something directly
  relevant to today's programme, dated 2026-11-05: the test society is a
  Minecraft world (Paper server on a Jetson Orin, community hosted on the
  Thor) with a disc golf league as its first institution, "throws recorded
  as decisions," and "a builder agent that mutates the course against the
  league's measured weaknesses." That is the league operating as an
  instrumented, decision-recording room — and it is where the git-agent
  line's ideas would have to survive contact with a world that pushes
  back.


8. What I would not claim

- I would not claim the git-agent line is the rooms programme's ancestor
  in any organisational sense. What the evidence shows is a shared
  substrate and a shared vocabulary — rooms, world, actor, action, commit
  — not a lineage.
- I would not characterise GIT_AGENT_SIMPLER.md beyond the brief's own
  note that it contains unreliable assumed context about Lobster/OpenClaw
  and should be treated as design inspiration, not repo truth. I read none
  of it.
- I would not claim that git-native-mud was ever played by a real
  model-driven agent. The engine makes no model call at all; the roster
  agents are YAML files with batteries. The dungeon is a working
  simulation with scripted participants.
- I would not claim the token "MOLT" is in the artefacts. The doctrine is;
  the word is not, in anything I opened.


### Artefacts opened (paths as they appear in the repositories)

git-agent/README.md · git-agent-standard/README.md ·
git-agent-minimum/README.md · git-agent-system/README.md (branch master) ·
git-native-agents/README.md · lau-git-agent/README.md ·
git-native-mud/README.md, mud_engine.py, quest_engine.py (tree listing),
world/rooms/helm.yaml, ROOM-GATEWAY-ARCHITECTURE.md,
.github/workflows/mud-turn.yml · agent-forge/README.md ·
bottle-protocol/README.md · iron-to-iron/README.md · i2i-vessel/README.md
· flux-baton/README.md · vessel-template/README.md ·
claude-code-vessel/README.md · oracle1-vessel/README.md ·
plato-hooks/README.md, src/plato_hooks/hooks.py (tree listing) ·
plato-sdk/README.md · plato-ng/README.md · crab/README.md ·
jacquard/README.md · git-agent-codespace/README.md ·
SuperInstance/SuperInstance/README.md (tree listing) ·
git-agent-flux-pipeline tree (empty but for LICENSE and .gitignore) · API
jacquard/README.md · git-agent-codespace/README.md ·
SuperInstance/SuperInstance/README.md (tree listing) ·
git-agent-flux-pipeline tree (empty but for LICENSE and .gitignore) · API
metadata for git-agent-system, git-native-mud, jacquard, jacquard-anchors,
plus a repository-name search for jacquard and for
room-resident-expert-design (0 results) · local file
/home/caseydigennaro/craftmind-league/.jacquard/kernel.jsonl (first
entries) · ~/seat-briefs-20261108/BRIEF-MCODE-GITAGENT.md, SOURCE-MAP.md.

---

## Parent verification note (Muse, 2026-11-08 — appended, not part of the take)

Spot-checks run against GitHub via the Oracle route (`gh`), 10 sampled claims:

- `git-native-mud` created 2026-04-14 — **verified**. `git-agent-system` created 2026-06-06 — **verified**. `plato-room-server` created 2026-04-20 — **verified**. `plato-sdk` created 2026-04-22 — **verified**. `jacquard` created 2026-11-02 — **verified** (it is this programme's November governance kernel, not an April artefact — the take's chronology is right and the parent map's juxtaposition needed exactly this correction).
- `git-agent-flux-pipeline` is empty — **verified directly**: its recursive tree is exactly `.gitignore` + `LICENSE`. The seat is right and the parent lane's source map was wrong: the map repeated the repo's stale GitHub description ("Pipeline connecting git-agent repo analysis to FLUX bytecode compilation…"). Nothing was ever committed. This is the run's cleanest catch, and it was the seat's, against its own brief.
- `git-native-mud` room count: the seat says `world/rooms/*.yaml` = 20 rooms; the tree holds 23 paths under `world/rooms/`. Counting-method difference (YAML rooms vs all paths), not a contradiction — recorded here so no one cites either number without its method.
- Parent-lane path error, owned: the brief addressed the cordis-lab documents and today's room paper as `~/workspace/...` — correct on the parent VM, nonexistent on the Thor, where the fleet home is `~` itself. The seat marked those files [UNREAD — file not present on this box] and declined to characterise them rather than laundering the brief's summaries into findings. That refusal is correct behaviour and is preserved in the take. The parent lane has read those documents itself (GIT_AGENT_SIMPLER.md ~30,400 words; REPO_AS_DESK.md, 2026-10-05) and the source map's characterisations of them stand as the parent's, not the seat's.
- The token "MOLT": the seat reports it appears in no artefact it opened, while the doctrine (checkout = replaceable shell, repo = persisting body) is thoroughly evidenced. Consistent with the parent lane's memory record, which holds the word as Casey's own coinage (2026-10-04 decision note) — the word lives in the design conversation, not in the repos. Both halves of that are now on record.
- The seat's transport note is accurate: its shell calls on the Thor were queued behind the Jacquard operator gate, so it worked read-only over HTTPS (raw.githubusercontent.com / api.github.com) — same public bytes, different transport.


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
