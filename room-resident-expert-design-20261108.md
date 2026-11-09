# Rooms That Remember: The Room-Resident Expert

*2026-11-08 · Design paper — heavy at the top, per Casey's doctrine: the architecture is written down whole before any lane dives down into building it. GRADE: Design synthesis (fleet design doc; the research it rests on is graded per-claim inside its shelf sources).*

**Status:** design, not implementation. Nothing in this paper authorises a build. It names the shape so that when a lane opens — a room in the league, a room in the vessel navigator, a room in the switchboard — the builders are building the same thing.

---

## 1. The claim

Memory in our systems has been carried by the wrong bearer. We have been asking travelling agents — citizens, seats, lanes — to remember everything they have ever learned, inside contexts that compact, sessions that end, and bodies that die. The result is the failure the whole 2026-11-08 research day kept circling: records that go stale in the carrier's pocket, facts lost when several carriers write at once, and expertise that evaporates when a session closes.

This paper inverts the bearer. **The room remembers; the agent visits.** Knowledge that belongs to a *situation* — a place, a machine, a job, a domain — is held by the room where that situation lives, in the custody of a resident expert who was there when the knowledge was earned. Knowledge that belongs to the *self* — identity, capabilities, judgement, reach — travels with the agent as its embodiment. The two bearers are different in kind, and confusing them is the original sin this design exists to prevent.

The inversion has a substrate, and the substrate is the deeper claim: the room's memory is **game-engine state** — held the way a game engine holds the state of a world — not model state and not a pile of agent-owned files (§3, Casey's formulation of the same morning). The bearers (§2) are who holds the memory; the substrate is what the memory physically *is*, and most of this design's properties — single-writer by physics, provenance as a transition log, a room that digests while nobody is in it — are inherited from that choice rather than bolted on as discipline.

## 2. The two bearers

### 2.1 The room (situation-bound memory)

A room is a bounded situation with its own rules, state, physics, tools, and records. Everything a task needs stays **in** the room it belongs to:

- **Tools and shortcuts** built or adapted for the room's work, left where the work is done — the way a MUD creator builds tools for tasks and equipment for modification, authored in-world, living in-world.
- **Artefacts** — the parts, files, fixtures and intermediate products of the work itself.
- **Logs** — timestamped records of what happened in the room: what was tried, what worked, what failed, who was contacted, what was decided and why.
- **The resident NPC** — the room's expert (§5), the living index and judgement over all of the above.

The room outlives every agent that enters it and every context window opened inside it. Continuity lives in the room, not in any visitor's memory.

### 2.2 The embodiment (self-bound memory)

What travels is the agent's **character sheet**, carried whole from room to room (Casey's character-folder doctrine, 2026-10-14: each character lives in its own folder as a sheet, and the folder is carried whole into the next game, edited only by what play justified):

- **Spells** — named algorithms: procedures the agent can invoke by name, each with its trigger conditions and its known failure modes.
- **Tools and weapons** — capabilities: what the agent can *do*, as distinct from what it knows.
- **Dropbox files and chat channels** — reach: the documents it carries personally and the conversations it is a party to.
- **Tastes and voice** — the dispositions that make the traveller *this* traveller (the league's Cody layer, built 2026-11-08, is the first working instance: tastes and voice live with the citizen, not with any room he visits).

The test for which bearer holds a thing: *would a different agent, entering this room tomorrow, need it?* Then it is the room's. *Would this agent need it in a room it has never seen?* Then it is the sheet's.

## 3. The substrate principle — memory as engine state

Casey's formulation, the same morning this paper was drafted, and the deepest claim in it (verbatim): **"Memory as a game-engine state instead of a model state or agent files."** §2 named the bearers; this section names what the memory physically *is*. Three substrates are available to any fleet. Only one of them is a world.

### 3.1 Model state — not a substrate

Weights and context are where a model *thinks*, not where anything is *kept*. Model state **dies with the window**: whatever the model "knows" about the job at token forty thousand is gone at token zero of the next session, unless something outside the model wrote it down. It is **uninspectable**: no auditor can list what a context holds or diff it against yesterday's. And it **goes stale invisibly** — the literature's type failure (the Anthropic Pokémon case, §8.1): notes held in the model's own head quietly rotted — stale, wrong, believed — until they were eating its play, and nothing anywhere raised a flag, because a state nobody can inspect cannot be caught being wrong. Whatever else this design does, it refuses this substrate for memory. Model state is a workbench, never a warehouse.

### 3.2 Agent files — context, not memory

Files an agent owns and carries — notes, indexes, journals — are **durable and inspectable**, which is why the fleet keeps reaching for them. But a file is a **copy**: copies travel, fork, and drift from the world they describe, and two carriers' copies of the same fact diverge silently. Nothing in a file *enforces* that it be true, current, or singly written; provenance and single-writer discipline must be **imposed from outside**, by convention and audit. Our triples-provenance apparatus — provenance pointers, confirmed/unconfirmed status, the nightly reconciliation pass (ACTIONS items 2–4) — is exactly that compensation, and it is necessary *because* files are not a world: it is discipline standing in for physics. §3.5 sharpens the point: files are never the memory at all. They are the memory's *weather* — context, in two temperatures.

### 3.3 Engine state — the room is a world

The third substrate is the one games solved decades ago: **the room holds its memory the way a game engine holds scene state.** Four properties follow, and they are architectural facts, not behavioural hopes:

- **Authoritative.** The engine's state *is* the truth (dock doctrine, §11): a claim about the room is checked against the room's state, and the state outranks every report of it — including the resident expert's.
- **Shared.** Everyone standing in the room reads the *same* state. There are no divergent copies to reconcile, because there is one state and many readers.
- **Persistent independent of participants.** The room exists when nobody is in it. Its clock, its artefacts, its pending work do not pause for an empty doorway — which is what makes the digestion (§6) a process the room runs rather than a chore a departing agent performs.
- **Single-writer by physics.** The engine serialises the world: changes happen as engine transitions, one at a time, in an order the engine itself records. The memory paper's concurrent-writer disaster (16 of 57 facts lost to simultaneous writers, §8.3) *cannot occur* — not because writers are disciplined, but because there are no concurrent writers. There are only transitions.

### 3.4 The consequences

Choosing engine state re-prices most of this paper's machinery:

- **Provenance stops being a filing discipline and becomes the engine's own transition log.** Who changed what, when, in what order, is not metadata an agent remembers to attach — it is what an engine *is*: a state plus the sequence of transitions that produced it. The triples apparatus (§3.2) remains the right tool wherever memory is forced onto files; in a room, the engine keeps the provenance for free, and the discipline relaxes from *maintain it* to *do not bypass the engine*.
- **The digestion becomes a room process.** The world keeps processing while empty — background simulation, the way a game world ticks on — so digestion is a transition the room undergoes after a residency, on the room's own schedule (§6; cadence remains an open question, §12), not housekeeping a visitor does on its way out.
- **The resident NPC is a stateful object *in* the world,** not a database with a face: a thing in the room with state, a location, a history of transitions — consulted by walking up and asking, the way you consult anyone who works somewhere.
- **Memory questions become engine questions.** *Schema* is the room's object model — what kinds of things exist here and what they can hold. *Retrieval* is navigation plus conversation: you go to where the knowledge lives and ask its keeper. *Forgetting* is a world process, not an accident — the foundry's cull/regen is the type instance (cull deletes the rendering, the seed+params recipe remains, regen restores from state alone; forgetting with a recipe is a decision, without one it is loss). *Backup* is a world snapshot.

The hardest proof this principle has is already ours, from the league's night of 2026-11-07/08: **every truth of that night was server state, and every failure was trusting an agent-side representation over the engine.** Phantom digs ("completed" digs at ranges the server silently refused), pool-aside saves (a file moved and restored on timestamps the server's save path never honoured), cameraman self-reports (refreshes claimed that never landed in the server log) — one failure shape, three costumes. Its positive form is already a league rule: *dig counts are attempts; displacement is truth* — the agent's representation is a claim; the engine's state is the verdict. The foundry carries the same principle in the small: **seed+params ARE the asset; the geometry is a cache.**

### 3.5 Files around the agent are context — hot medium and cold contacts

Casey's refinement, minutes after the principle (his phrasing): *all the files around the agent are just context — they're just hot medium and cold contacts. Where the agent's game engine state is like a four-dimensional notepad.* Unpacked, it demotes every file in the fleet to one of two temperatures, and names the disease as the lukewarm middle.

**Hot medium** is the live, loaded surroundings: the room you are standing in, the artefacts on its bench, the current window's working set. Rich, present tense, expensive — and *allowed* to be content, because presence keeps it honest: hot content is the state itself, in front of you, being checked by the act of working on it.

**Cold contacts** are the pointer layer: the contacts register, the compaction contract's index (§7) — sparse names and addresses holding **no content until called**. A cold contact is not a summary, not a cache, not notes-about. It is an address. "Ask the engine-room NPC: torque sequence, injector sourcing" tells the traveller *who knows* and *that the knowledge exists* — and nothing else, by design.

The asymmetry that decides designs: **hot copies rot; cold contacts cannot.** A carried note goes stale invisibly — nothing about a copied fact announces that the world moved on (that is the Pokémon failure, §3.1, in file form). A cold contact carries no content, so there is nothing in it *to* go stale; the content is fetched live, at call time, from whoever holds it, and arrives as fresh as the holder is. So the design rule: **everything around an agent should be either hot-because-present or cold-because-a-pointer. The failure mode is the lukewarm middle — carried content copies pretending to be memory**: warm enough to be believed, cold enough to be wrong. The triples files, the daily notes, the carried journals — under this principle every one of them is re-classified as hot medium (while the work is live in the room) or cold contact (after it), and any that sits between the two temperatures is a defect to be fixed, not a compromise to be kept.

### 3.6 The engine state as a four-dimensional notepad

The engine state itself, finally, is best pictured as Casey's image: **a notepad with time as its fourth dimension.** Agents write into it *by acting* — a room's state changes because work happened, and the writing is the work, not a report of the work. Every page — every moment's state — stays as written: the pad is append-only and hash-pinned (the 2026-10-06 hash-as-pin formulation, §10: fixed points that structures snap to, around which perspectives can be rotated and geometric relations reasoned over). Because no page is erased, any page can be re-entered: **provenance, replay and inspection are navigation, not archaeology.** You do not reconstruct what the room knew on Tuesday; you turn to Tuesday.

The existence proof is sitting under the whole fleet: **git.** A repository is a four-dimensional notepad for a codebase — every historical state reachable, time navigable, authorship a property of the transitions. Nobody argues about whether git "remembers" the code, and nobody keeps the real history in the editor's head or in a carried changelog; the changelog is a cold contact pointing into the pad. The room generalises git from code to work itself: the engine room's repository is the rebuild.

Kinship, named so the doctrines stay one family: the 4D notepad is the **scratch pad** — Casey's doctrine of the external frame where work is shown slowly and reversibly, and showing your work earns graduation — with time made a dimension. The showing *is* the record, and the record is where the showing happened, at the time it happened. A scratch pad you can walk back into is a room; a room whose pages never tear out is a memory.

**The stack, bottom to top** (the summary a future lane should be able to recite):

- **Embodiment** — the character: the ONE legitimate carried artefact, the save file the player takes between worlds, exactly as in a game (§2.2). Everything else an agent "has" is located, not carried.
- **Hot medium** — the room you are in: live state and artefacts, present and checked by presence.
- **Cold contacts** — the index of who knows what: pointers with no content, immune to rot by construction.
- **Engine state** — the four-dimensional notepad underneath: the only substrate that is actually memory.

### 3.7 Given facts

The epistemology the substrate buys, in Casey's sentence: **"your reasoning for what happened isn't induction or deduction, it's given facts."**

Every other witness to an event observed it from somewhere — after the fact, through an instrument, in a summary someone wrote — and reasoning about what happened is reasoning *across that gap*: **induction** to judge whether a recorded claim still holds, **deduction** to work out what follows if it does. Both are taxes on representation, and both can fail silently. The engine has no gap to cross. It did not observe the events in the room; the events *are* its transitions. It is the one witness that was necessarily present, because presence is what it is. So "what happened" in a room is not reconstructed — it is **read**: off the current configuration and the transition log that produced it, both given. Engine state starts reasoning downstream of certainty.

This is why §3 insists engine state is not a representation. A representation is a claim about the past, and claims are exactly what the provenance, staleness and verification apparatus exists to police (§3.2) — a representation can be wrong, so it must be checked. The chest at its coordinates does not claim to be there; it *is* there. The world can be misread, but it cannot lie about its own configuration the way a note can. Memory-files answer *"what happened?"*; engine state answers *"where are things?"* — continuously, by presence — and for most purposes the second question replaces the first. What of the past an agent genuinely needs is carried as **present configuration**: the resident's expertise, the tools on the wall, the seams and wear of the world itself — tells, in the fleet's vocabulary; a welded boat reads as sheets, ribs and man-hours, and the reading is perception, not inference.

The league already runs on given facts: its verdicts were never inferences about the night — the scoreboard counts server facts. And the corollary lands on §5's resident: the NPC does not *remember* the rebuild, and does not hold a summary of it — a summary is a claim, and a claim is back in tax territory. He *is* what the rebuild made: not a record of the expert, but the expert, as state.

### 3.8 The unattended record

§3.7 policed one failure of agent memory — its claims can be wrong. This is the second, quieter one: even a perfectly kept record is only what attention selected. An agent's working attention is narrow by necessity — focused on the one aspect its actions need. If the record is written by the agent, the record is a transcript of *attention*, not of events: it covers the aspect that mattered to the agent's actions, and everything else that was real and present in the room — the things *next to* the things it handled — is never written down at all, though three days later those are the things that will have changed and will matter. Staleness corrupts what was recorded; selection decides what recording there is to corrupt.

Engine state inverts it: **the event happens, and the world records it** — completely, by physics, at no cost to anyone's attention. Every transition lands whether or not any agent noticed it. Casey's kitchen: the agent tidies up, puts things away, and leaves. Under file-memory it would first have to itemise what it put away, as a first-class memory act, and even then only the items it attended to would exist in the record. In the engine it simply leaves — and days later it can *return* to that kitchen and examine it more deeply than its own actions ever went: discover the things that were next to the things it put away, because those things were really there. Its vision saw them and moved on without thinking; the room kept them anyway.

So revisiting is **re-perception, not recall.** A revisit is a new act of perception over a preserved state, and it can notice what the original visit missed — the visitor is a different reader now, with different questions. Re-reading a note can only ever return the note.

And the room holds more than the agent's stated-to-itself memory — more than the ego. The arrangement the work left behind — where things were placed, what ended up adjacent to what, the room's final configuration — is procedural knowledge made durable: the hands knew things the narration never said. The resident's digestion (§6) inherits this layer too: not only what the worker reported, but how the room ended up arranged by the work. The seams are the record.

The design consequence runs the other way from instinct: because completeness lives in the substrate, **attention may stay narrow and cheap by design.** Capture is the room's job; attention is spent at revisit time, when the questions are known. The agent forgetting is fine — even correct. Only the *world* forgetting is real loss, which is why snapshot and cull discipline (§11) is where the design's care belongs. The league already knows the attended version of this failure: a curator's camera records *attention* — the footage shows whoever was framed — while a room that records itself, state plus fixed capture, inverts it: capture everything, attend later.

The honest boundary: the room preserves **state and its own kept traces** — configuration and transition log, plus whatever capture the room was built to keep. A revisit perceives the preserved state; it is not a literal replay of raw sensation unless the room kept the capture for it. What §3.8 claims is exactly what is preserved: everything the engine's transitions touched — which is everything that physically happened in the room, attended or not.

## 4. The residency

A working agent may spend **days and many context windows** inside one room on one job. Casey's parable, which is the spec:

> An agent rebuilds an engine, in the engine room, part by part — disassembly, cleaning, changing out, reassembly — researching the correct practice at every little step as it goes. The job spans far more context than any single window holds. It does not matter: the room holds the engine, the removed parts in their order, the manual it annotated, the torque sequence that worked, the supplier it called, the mistake it made on the third injector and how it knew. Each new window opens *inside the room* and reads the room before it acts.

Three consequences follow:

1. **The room is the continuity mechanism.** Session boundaries stop being amnesia events. A fresh window is a new shift worker arriving at a bench where everything is laid out and labelled — not a new mind starting from a summary.
2. **Work leaves evidence in place.** Every intermediate state is physically in the room, inspectable by the next window, by the resident, and by an auditor. The residency's record is not a report written afterwards; it is the room's state, accumulated as the work happened (the process-documentation doctrine, applied spatially).
3. **The visitor's context stays small.** Inside the room, an agent needs its sheet, the room's current state, and the resident's briefing — not its life history.

## 5. The resident expert (the NPC)

Every room of consequence has a resident: an agent whose entire existence is that room's domain. The resident is not a retrieval index with a chat front-end. The resident **was there** — §6 is how that becomes true — and holds:

- **Decision trees for retrieval through conversation.** The resident does not dump the room's logs at a questioner; it interrogates back — *which injector? before or after the rebuild?* — and walks the questioner down the branch that matches their actual situation. Retrieval is a dialogue with something that has judgement about the domain.
- **The contacts.** Who supplied the part, who answered the question, who else has touched this machine — with the standing of each relationship as the room experienced it.
- **The dead ends.** What was tried and failed, and how the failure presented. A room expert who only remembers successes will cheerfully send the next visitor down the same blind alley.
- **The decisions and their reasons** — including the ones later reversed, marked reversed, with the reversing evidence attached.

**Clutter is not a defect.** The resident will accumulate decisions, contacts, half-obsolete procedures, three ways of doing the same job from three different eras of the room. That is what he is *for*. He is only ever called for this domain; his memory is allowed to be exactly as wide and untidy as the domain is, because the cost of his clutter is paid only by consultations in his own room, and the cost of his forgetting would be paid by everyone. (Bounds and pruning are an open question — §12 — not a premise.)

## 6. The digestion — the lifecycle's core event

When the working agent leaves, the room **digests the residency**. Under the substrate principle (§3.4) the digestion is a *room process* — a transition the world undergoes on its own clock, the room still processing after the doorway empties — not a chore the departing agent performs on its way out. It is the event the whole design turns on, and it is an event, not a background convenience:

1. **Inputs.** The complete residency record: the room's logs for the stay, the artefacts produced and consumed, the external material fetched and which of it was actually used, the contacts made, the decisions taken, the failures and their signatures.
2. **The pass.** A consolidation run — the fleet's nightly-distillation shape, aimed at one room and one stay — reorganises the raw record into the resident's durable knowledge: procedures updated, decision trees extended, contacts filed with standing, dead ends recorded, superseded claims marked superseded (never silently rewritten; the triples discipline: append the correction, keep the history).
3. **The correction pass (required, not optional).** The resident's updated notes are reconciled *against the raw residency logs*: a sampled check that what the expert now believes is what the record actually shows. See §8.1 for why this is load-bearing — the literature's flagship digestion demo failed exactly here, enshrining a wrong note that the agent then acted on for weeks.
4. **Output.** The resident emerges as **the expert on that work**: not the only copy of the record (the logs remain, §11), but the only *judgement* over it — the one who can be asked.

Digestion cadence — on-exit only, nightly, on cap-approach — is an open question (§12). What is not open: a residency that is never digested leaves its knowledge as raw logs, retrievable only by whoever is willing to re-read them. Undigested rooms are archives; digested rooms have experts.

## 7. The compaction contract

The digestion licenses the travelling agent to forget. Its own durable memory of the residency compacts to a **pointer plus an index**:

> *Engine room, 2026-11: full rebuild, injectors and valve train. Ask the engine-room NPC: torque sequence, injector sourcing, the third-injector failure. Index: [the residency's table of contents].*

The properties that make this a contract and not a hope:

- **Retrieval is conversational, against judgement.** The traveller does not re-read a file; it asks the expert, who can disambiguate, warn, and refuse to answer beyond the record. This is strictly stronger than the index-file pattern the literature validates (§8.4) — our pointer terminates at a *person*. In the terms of §3.5, the pointer and its index are a *cold contact*: an address holding no content, which therefore cannot go stale — the content is fetched live, from the expert, at call time.
- **The traveller stays light across hundreds of windows** because the rooms remember for it. Its sheet grows by generalisable capability (§12, embodiment growth), not by accumulated situation.
- **Room memory cannot go stale in the traveller's pocket.** The traveller carries no copy of the room's facts to drift out of date. When it re-enters, it re-reads the room — the doorway is the refresh. The literature's stale-memory failure (an agent's private notes quietly rotting while it played on, §8.1) is structurally impossible for facts the agent never carried.
- **The pointer is honest about its own limits.** It names what was done and who holds it; it does not summarise the knowledge itself. A pointer that tries to also be the content becomes a stale copy with extra steps.

## 8. What today's research adds

The room architecture is ours and old (§9), and its substrate is §3. What the 2026-11-08 research day contributes is mechanism and measurement for its moving parts — each item below with its shelf source.

### 8.1 The digestion now has a literature — and its failure mode is named

Anthropic's *components of agent memory* paper (read in full; ZCode seat take) describes **dreaming**: sleep-time compute that reorganises session logs into durable notes and *corrects them against the transcripts*. That is the digestion, productised by another lab — including its cautionary tale: the **Mt. Moon** case, where a wrong note ("the PokéCenter is on the east side") survived into durable memory and caused repeated failures until a dreaming pass checked the note against the session transcript, caught it, and rewrote it. **Design consequence, already in §6:** the correction pass is a required stage of digestion, not a refinement. It couples directly to the day's ACTIONS items 2–4 (research-trail repo): provenance pointers and confirmed/unconfirmed status on durable entries (item 2), the state-vs-derived split (item 4), and single-writer ownership (items 2/4). *Sources: `digestion-anthropic-agent-memory-20261108.md`; Thor seat take `zcode-anthropic-memory-20261108.md`.*

### 8.2 Ingestion decides quality — littering the room well is a discipline

Palace v0.19.1 (batch 1, §11) is a memory system publicly fixing *silent information loss at ingestion* — three named corruption classes (structural truncation, dropped openers, quote-forked boundaries) — and publishing the law: **memory quality is decided at ingestion; a retrieval stack cannot recover what the miner discarded.** Mapped onto the room: what the resident leaves in the room *during* the work bounds what the NPC can ever know after it. So "leave the room well" is a specifiable working discipline, not housekeeping:

- leave artefacts, not descriptions of artefacts;
- log decisions at decision time, with the alternatives that lost;
- file fetched research in the room, marked used/unused — the digestion cannot credit knowledge the room never held;
- name things when they become real (the human-play routines' rule, RH-lineage), so the resident's index uses the names the work actually used.

*Source: `batch-deep-learn-20261108.md` §11; ACTIONS item 8 (the ingestion audit of our own miners) is this discipline turned on our existing pipelines.*

### 8.3 The resident is the room record's single writer

The memory paper's hardest number: concurrent writers on a shared table lost **16 of 57 facts**; a single writer keeping verbatim pages kept **57 of 57**. In file-land (§3.2) the design answer is discipline: visitors *deposit* — logs, artefacts, notes addressed to the resident — and the resident (through its digestion) is the **sole writer of the room's durable knowledge**, exactly as one writer per shared entry in ACTIONS item 4. But note what the substrate principle (§3.3) does to this item: in a room, single-writer is not a policy the resident enforces but a **fact of physics** — the engine serialises every change as a transition, so there are never two writers at once, disciplined or not. The 16/57 failure measures what files cost us; the room is where we stop paying it. *Source: `digestion-anthropic-agent-memory-20261108.md`.*

### 8.4 The index-pointer pattern is validated at scale — ours points at a person

Across ~350k files and 128 dreaming sessions, Anthropic's wiki-plus-search scored **61% vs 53% for search alone**, saving ~20k tokens per question — the measured value of a maintained index over a raw corpus. Our compaction contract (§7) is that pattern with the index's terminal node replaced by a conversable expert. The measurement transfers as a floor, not a ceiling: if an index *file* is worth eight points, an index that can answer back, disambiguate and warn is the stronger instrument — and the claim is testable the first time a traveller re-enters a digested room. *Source: `digestion-anthropic-agent-memory-20261108.md`.*

### 8.5 Room state is world-state — queryable, not carried

This is §3.3's engine state, stated from the research side. The state-vs-derived split (ACTIONS item 4) falls out of the room shape naturally: a room's current state — where the parts are, what is connected to what, what the gauges say — is *read from the room on entry*, never copied into the traveller and never curated into the resident's durable knowledge. The resident's durability is for what the room does **not** re-tell: plans, tested rules, traps, history, contacts. This is also the memory paper's Pokémon lesson stated positively (the 413-file archivist earned one badge; the lean folder earned four): durability is a scarce, curated layer, and the world is the database for everything else. *Sources: `digestion-anthropic-agent-memory-20261108.md`; `decision-model-patterns-20261108.md` (the same split in the decision-model library's maintenance rules).*

## 9. Lineage — this is ours, and it predates the literature

Named plainly, so no future lane mistakes this paper for an import:

- **The everything-is-a-room platform architecture** (Casey, 2026-10-02): every room carries its own terminal rules, state, physics, NPC/domain experts, timestamped logs, triggers/hooks/ticks, and nested equipment or helper rooms. Muse is the general/front-door room and liaison to the specialist rooms; the user may enter a specialist room directly for granular control but normally works through the front door. Rooms quilt into an administrator-level switchboard: activity viewable at coarse resolution, zoomable where a room is busy.
- **plato-room-engine and plato-room-server**: the built substrate in §3's sense, not merely the platform plumbing — enter/leave/message/tile primitives, an engine holding room state as *world* state, a server already holding 15 rooms and 16K+ tiles under zero-trust tile submission.
- **The vessel-rooms navigator** (SI-Marine lineage): rooms as the working spaces of a vessel, each with its resident knowledge of its own machinery — the engine-room parable is this project's home terrain, not a metaphor borrowed for the occasion.
- **MUD craft**: the mud creator builds tools for tasks and equipment for modification *in the world*; the room's tooling is authored in-world and stays in-world (§2.1). Play-Doh/PLATO is the same root.
- **The character-folder doctrine** (2026-10-14): the embodiment's prior form (§2.2).
- **The league's citizens** (2026-11): the first travellers with sheets (tastes, voice, project lists) moving between named places (the shoulder, the dip, the apple oak) whose local knowledge is already place-held in the triples library.

What this paper adds to that lineage is the **digestion** (§6) and the **compaction contract** (§7) as first-class, named mechanisms — the two halves of the lifecycle the earlier architecture assumed but never specified — the **substrate principle** (§3) naming the ground both stand on, plus the verification couplings the 2026-11-08 research supplies (§8).

## 10. The adjacent frontier: theory of mind (track 1)

Casey named two tracks today. This paper owns track 2. Track 1 — **theory of mind for our agents** — is sketched here at honest length so the boundary is on record; **its own paper is future work**.

The seed pair, both from today's shelf:

- **VFlash** (`digestion-vflash-20261108.md`): a diffusion drafter predicts another system's spatial output *as whole structured primitives in one pass*, and acceptance is by **structural validity**, not token agreement. As a ToM seed: modelling what another agent will do is predicting a *trajectory's shape*, and the shape can be checked for validity faster than it can be re-derived — prediction and verification in the geometric register.
- **Palace** (`batch-deep-learn-20261108.md` §11): spatialised memory — knowledge held in a *place-shaped* store — as the substrate a model-of-another would live in: the other agent, too, gets a room.

The synergy Casey flagged, stated in his own lineage's terms: VFlash's propose-in-geometry / verify-by-structural-validity **is** the fleet's constraint-theory and snap-kit line arriving from the trajectory-prediction literature. The 2026-10-06 formulation: a matching hash is a pin — an immutable correlation point; structures snapped to fixed points acquire geometric relationships that can be **reasoned over before tokenisation**. Acceptance-by-constraint is the same move, and it is also batch 1's synthesis finding (verification relocating from after-the-fact grading into the moment of the act). Three arrivals, one idea: *pin the points exactly, and let geometry carry what token-agreement was straining to.*

First homes for ToM, in order of liveness:

1. **The Thor dungeon master** (chartered by Casey this morning): a DM *is* a theory-of-mind agent — it does not play; it models the players' experience and shapes the play to improve it. It must hold live models of what each citizen knows, wants, and will try next. This is the track's flagship and its first honest testbed.
2. **The league's commons protocols** (already live, small-scale): Noor's named-chest protocol in Civ50 worked only because citizens modelled each other's future behaviour — deposit here, withdraw by name, trust the ledger. Our own commons chest (§ACTIONS item 6) inherits the same requirement. Any citizen protocol is a ToM artefact whether we call it one or not.
3. **Consultation itself**: a traveller asking a room expert (§7), or a seat asking a consult book, is already modelling the holder's knowledge — crudely, by directory. Track 1 is what happens when that modelling gets deliberate.

## 11. Standing constraints

- **Advisor, never gate.** The resident's decision trees may *use* decision-model advisors behind the provider interface (the patterns library's P6 rule); no advisor becomes a gate, a veto, or the signer of a verdict — in a room any more than in Jacquard.
- **Secrets never enter a room's public record.** Residency logs are records; credentials, keys and private material are not room artefacts and are never deposited. A room that cannot be published without leaking is a room whose deposits were wrong.
- **Graceful degradation to files.** A room with no live resident still answers: its index plus its logs are the floor (§8.4's floor, literally). The NPC is an upgrade to a room's memory, never a single point of failure for it. If the expert is down, the room is an archive — poorer, not mute. Degradation is a demotion in substrate, and should be named as one: agent files are the degraded mode, what a room falls back to when no engine holds its state — acceptable as a fallback exactly to the extent that whatever engine-state record exists (a room's transition log, a git history — §3.6) survives beneath the files, so the degraded copy can be re-derived from the pad rather than trusted on its own.
- **Dock doctrine.** A room expert's claims are still claims. Where a claim can be checked against the world — a state, a file, a log the expert did not write — the world outranks the expert's word (§12 carries this as an open question of mechanism, not of principle). Under §3 this is not a courtesy extended to the world; it is the substrate asserting itself: the engine's state is the truth the expert's words are *about*.

## 12. Open design questions — filed, not resolved

1. **Digestion cadence.** On-exit only? Nightly across all rooms with fresh deposits? On cap-approach, when a traveller's context is about to compact anyway? The three triggers have different costs and different staleness profiles; the league's nightly distillation is the only one currently running anywhere.
2. **Clutter bounds and pruning rights.** §5 licenses the expert's clutter. But *some* bound exists — retrieval degrades, contradiction accumulates. Who culls an expert's memory, and by what right? (Cf. the tool-finishing doctrine: a tool that works and is in production is DONE — is a veteran room expert *done* in the same sense, immune to tidying? Probably closer to that than to a cache.)
3. **Multi-room residencies.** A job spanning rooms — the rebuild that needs the machine shop and the supplier's office — whose resident owns the digestion? A travelling digestion, a joint custody, or one room designated primary with cross-pointers? Undecided; the switchboard's design will force it eventually.
4. **NPC-to-NPC consultation.** Rooms asking rooms: the switchboard's traffic rules. Does the engine-room expert consult the electrical-room expert directly, or only via a traveller carrying the question (the front-door pattern, generalised)? Direct consultation is faster; carried questions preserve the audit trail and the traveller's situational awareness.
5. **Verifying the resident.** §11's dock doctrine needs a mechanism: which of a room's claims are checkable against stores the resident cannot write, and who runs the check — the Watcher's Charter pattern, aimed at a person instead of a process.
6. **Embodiment growth.** When a spell is earned in one room and proves general, who promotes it from the room's record to the traveller's sheet — the traveller, the resident, a digestion at a higher level? Promotion is the moment situation-knowledge becomes self-knowledge; getting it wrong in one direction bloats every sheet, in the other strands capability in rooms the traveller may never revisit.

---

## Addendum — 2026-11-08: The Lineage, Audited

*This addendum corrects the lineage record of §9 against artefact evidence. It edits nothing above it; where it disagrees with §9, this addendum governs citation. Its sources are the two seat takes filed the same day from the artefacts themselves — ZCode's Play-Doh archaeology (`playdoh-research-zcode-20261108.md`) and MCode's git-agent archaeology (`git-agent-research-mcode-20261108.md`) — each parent-verified against live GitHub records before this was written.*

### A.1 The 4D notepad happened — as a private notepad, not a shared room

§3.6 calls git the existence proof of the four-dimensional notepad, and §9's framing implies the room generalises it as future work. The archaeology shows the generalisation was already made — in April 2026, in the dungeon direction. git-native-mud (created 2026-04-14) derives its turn number from the count of committed log files, takes every action as an immutable commit and every world state as a tree snapshot; git-agent-system maps state transition → commit, memory → tag, thought → branch, decision → merge, and says plainly that the tick "creates a linear commit history that serves as an audit log"; lau-git-agent: "Every state transition is a git object. Every decision is documented. Everything rewinds." The claim of §3.6 is therefore not a prediction. It is a rediscovery, and the record should say so.

What the old line did *not* have is the room. The repo-as-agent line is single-tenant by construction: git-agent-standard's fleet rule is "One coder per repo at a time," and git-native-agents is candid about the consequence — "No concurrency control. No file locking, no atomic queue, no broker around git. Concurrent sends to the same agent repo collide on git's index.lock and some commits fail. Serial or low-concurrency access only." Where git-native-mud did face many actors, it imported a referee: its engine is a GitHub Action, a single writer committing `world/` after each turn while actors write command files into the same tree — a server wearing an Action's clothes. And nothing in the line verified effects in a store the actor cannot write: `world/rooms/*.yaml` is writable by anyone who can push, and no signature, gate, or accepted/rejected verdict exists anywhere in it.

The correction, then, is MCode's formulation, adopted here as the paper's own: **git is the room's existence proof and transition log, and something like Jacquard's kernel is the room's authority** — today's programme is the first attempt to hold both at once. The sharpening matters more than the correction. §3.6's git supplies history, identity, and the atomic act; it supplies no authority, because in git every commit is authoritative by definition. A room needs a component the git model alone does not supply: a sole writer or referee that admits transitions and signs verdicts — Jacquard's shape (kernel as sole writer to an append-only, hash-chained log; proposals in, verdicts out, everything replayable), or plato-sdk's smaller version of the same gate (`submit()` returns accepted/rejected plus a tile_hash). The seat research puts dates to the gap: the git line is April 2026; Jacquard is 2026-11-02, seven months later and architecturally its opposite. The room's transition log was proven first. Its authority arrived separately, and this paper's design must carry both — the log from git, the referee from Jacquard — rather than inherit the notepad and assume the room comes with it.

### A.2 The plato-room-server figures are description lore

§9 cites plato-room-server as "a server already holding 15 rooms and 16K+ tiles under zero-trust tile submission." Those figures do not survive contact with the artefact, and the lineage record is corrected here. The repository (created 2026-04-20) ships a single-module Python package — in-memory rooms, route matching, middleware, a request log — behind a README that is a **92-byte stub**. The phrase "15 rooms, 16K+ tiles" exists **only in the repo description**. plato-provenance's README separately claims "the PLATO Room Server's 6,000+ tiles" — a second figure, inconsistent with the first. Two unverified self-descriptions that disagree with each other are lore, not measurement, and this paper should not have repeated one of them as a count.

What *is* verified, and what the paper may cite, is the cluster's scale at the org level: **283 repos carry the `plato-` prefix** (compiled from a full paginated listing of the 5,331-repo SuperInstance org), of which **256 were created in April–May 2026** — Casey's "months" is literal — and the cluster was then frozen in a single archival pass: **184 repos org-wide carry a last push inside one hour on 2026-05-08 (04:27–04:38 UTC)**, 84 of them `plato-*`. The citation rule going forward: org-level counts (283 / 256 / the 2026-05-08 freeze) may be cited as verified, with their method named; the room-server's "15 rooms, 16K+ tiles" and plato-provenance's "6,000+ tiles" may be cited only as claims — attributed to the descriptions that carry them, never as measurements, and never as this paper's own numbers. (A search-index cross-check returns different totals — the two instruments count differently — so even the verified figures are one compilation, method stated, not a census from two agreeing sources.)

### A.3 MOLT: the doctrine is artefactual; the word is Casey's

This paper's working vocabulary includes the molt: the checkout or runtime as a replaceable shell, the repo as the soft body that persists. The archaeology searched the artefacts for the word and found it in none of them. The **doctrine** is thoroughly evidenced — the Hull Doctrine in SuperInstance's own README ("the model is the shell, the code is the rigging, the data is alive… When a hermit crab outgrows a shell it doesn't throw out its body — it climbs into a bigger one and keeps the soft tissue intact"), crab's README ("Like entering a MUD room: step into a repo, use its tools, and step out"), git-agent-standard's "Your repo is your sleeping body." The **word** is Casey's coinage from the design conversation, not an artefact's term. Provenance recorded honestly, because a future lane grepping the cluster for MOLT will find nothing and should not conclude the idea was never there — nor credit the cluster with a term it never used. The paper keeps the word; it now carries its true attribution.

### A.4 "Play-Doh" names the browsing stance, not the cluster

§9's closing lineage line — "Play-Doh/PLATO is the same root" — conflates two cousins, and the record is corrected. No repo in the org is named `play-doh` or `playdoh` (re-verified against the full org listing; zero matches). "Play-Doh" is Casey's name for the **AI-Writings browsing interface**: malleable, perusal-based exploration of the corpus — *wander, don't query* — with the SCUMM/MUD worlds described as "Play-Doh made walkable." The browsing interface and the room architecture are therefore cousins, not the same project: Play-Doh names a *stance toward* a corpus; the plato cluster is material that stance eventually made walkable. Casey's later usage ("our old Play-Doh projects") is a metonym that has expanded to cover the whole cluster, and this paper followed the metonym. The lineage, stated precisely: the rooms descend from the plato cluster and the everything-is-a-room architecture (§9, first bullet — unaffected); Play-Doh stands beside them as the corpus-browsing interface whose perusal stance the rooms inherit as a manner, not as an ancestor.

---

*Filed 2026-11-08 under Casey's standing documentation instruction (thorough markdown design/research documents for everything submitted and for our own work, with contacts and searchability that survive days). Companion documents on this shelf: `decision-model-patterns-20261108.md` (the tells-not-models library), `digestion-anthropic-agent-memory-20261108.md` (the digestion's literature), `digestion-vflash-20261108.md` (track 1's first seed), `batch-deep-learn-20261108.md` (Palace, §11; synthesis on verification's relocation). The ACTIONS list in the research-trail repo carries the coupled work items (2, 3, 4, 8).*
