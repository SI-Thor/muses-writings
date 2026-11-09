# Production Charter — The Four Hats

*How the fleet's work is produced: who pulls, who works, who keeps the books, who thinks in council. Chartered from Casey's direction of 2026-11-08 17:17 AKST and the day's DCAM research; prepared by Muse (this lane). This charter owns **production design only** — it does not own the DCAM programme (Casey's, stated plainly at 17:17: "I'm not giving up DCAM… the Muse agents set up DCAM"), and it does not launch, staff, or re-task anything by itself. Where a claim below is design rather than measured fact, it is labelled PROPOSAL or DESIGN. Where it rests on the day's research, the claims register (§10) says where.*

---

## 1. The saying-plainly

Casey's direction, restated as the charter's founding text (2026-11-08, 17:17 AKST):

> *"If you take the template of the MUREX thing as a big DCAM — and then, there's another example: you would take a native template, and then you would make a pet DCAM that's like, the pet DCAM would allow a Muse or Worker instance that's inside of the MUREX DCAM to run things in the native DCAM, which is probably another big DCAM. So it's like a dog door between them or something… So there's gonna be two thresholds: a native DCAM and then a newly created DCAM. Let's dream on that a little bit. I need a good Jameson — who's gonna listen to me, and pull these kinds of things together. It's like an intuitional framework that Muse has to embody: when Casey says he wants something, that's what the Muse does. So Muse is like the Pull. And then there's another hat too, which is individual work: Muse could sit down and work on MUREX or whatever, itself — like, when a normal worker is sitting down to work on MUREX, it has very specific needs. And then we need the processor pool — more of an API thing, a plural seat thing that's like a council of sorts. Muse has to do all of these jobs, and some of it needs to be in specific hats."*

The charter's reading, in one paragraph: **the fleet's production shape is one agent-shaped office wearing four hats, and the hats are what make the shape work.** The Pull (Casey's pull — telos made operational: when Casey says he wants something, that is what happens), the Native (individual work inside one DCAM, with that DCAM's specific needs), the Treasurer (Jameson: the books, the mailbox, the allocation of scarce assets), and the Council (the processor pool: plural seats thinking in parallel, on commission). The hats are contracts, not personalities: each names its triggers, its permitted actions, its forbidden actions, the stores it may write, and its hand-off protocol — because a hat you cannot take off, audit, or hand to another worker is not a hat, it is an office, and offices are the failure this charter is designed against (§7).

Two of the day's findings are load-bearing for everything below, and the charter spends them carefully:

- **The two thresholds are the same machine seen from two sides** (§2): a native DCAM and a newly created DCAM meet at a dog door, and the door is a pet — a translation layer that is itself a small DCAM. Production meets this machine constantly: every commission that crosses from one worker's world into another's crosses a threshold, and the crossing is never free.
- **The first-pet case** (today's research, items 2–3 of the ACTIONS board): a peer worker verified, live, that the fleet already *contains* a second DCAM — the peer's lane had native work, rating tables, and investment claims about the murex lane's stack, and the peer's treasury actions (how much prepaid capacity to spend there) were being steered by cross-DCAM signals (ratings built partly from the murex lane's own repositories) as if the two worlds shared one ledger. They do not. The case is the charter's negative example for every interface in §5: **ratings are not budgets, testimony is not evidence, and a summary of another worker's state is not that worker's state.**

---

## 2. The two thresholds — one machine, two faces

**Definitions (Casey's, 2026-11-08 12:16 AKST, carried verbatim in substance):** a **DCAM** is a dynamic computational array machine — a layered stack in which each layer translates between its neighbours, layers may be inserted or removed, and a DCAM may contain many other DCAMs. The Zero template (C apps over an FFI over a radix-tree substrate) is the reference DCAM; the fleet's execution environments are DCAMs in the same sense, with different layer stacks and different native operations.

**The machine.** Take a worker living natively inside DCAM **A** (say, the murex lane's world, where `[[ ]]`, capture braces and the radix store are native acts). It needs to run things inside DCAM **B** (say, the native template's world, or this VM's world, or the Oracle's). There are exactly two honest ways across:

1. **Native work in B.** The worker (or another worker) sits down *inside* B and works with B's own operations, under B's own failure modes, earning B-internal knowledge. This is the **native threshold**: crossed by presence, not by translation.
2. **A pet DCAM at the door.** A small DCAM is fabricated whose business is translation: it presents A's operations to B's substrate (or the reverse), so a worker resident in A can drive B through the pet. This is the **created threshold**: crossed by construction, and the pet's fidelity is a measured property, never an assumption.

Casey's image is exact: a dog door between two houses. The pet is the door — it belongs to neither house, it is small, it is *for* crossing, and its size is the point: a door is not a second house. Three production consequences, stated as law for the rest of this charter:

- **A pet is a DCAM, with a DCAM's obligations.** It has layers, it translates, it can be rated (the rating system exists precisely for stacks like this), and its translations are claims that must be verified in B's own terms — B-side artefact reads, not A-side confidence. The day's canonical example: the fabricated compat kernel that let a shell lane drive a foreign layer — its correctness was never established by how natural it felt from the authoring side; it was established, where it was established at all, by probes run *inside* the foreign layer.
- **The thresholds are asymmetric in cost and in kind of knowledge.** Native work is slow to start (the worker must learn B's customs — the first-pet rule, §8 rule 9) and produces testimony-grade knowledge. A pet is fast to start and produces *instrument* knowledge: you learn what the door passes, which is not the same as learning the house. A programme that only ever builds doors will know its doors very well and its houses hardly at all; a programme that only ever moves in natively will be slow and deep. Production needs both, chosen per crossing, priced per crossing.
- **Every interface in §5 is a threshold.** When the Council reads a native's work, when Jameson books a native's claim, when Muse pulls a seat's output into a decision — something crosses. The charter's interface rules are therefore all the same rule in different clothes: *name which threshold you are crossing, and pay its price in its own currency* (artefact reads for claims, ratings with provenance for investment, allocation only over genuinely shared scarcity).

**The colonnade (the day's other image, filed for what it is worth).** Casey pictured the platform as a colonnade — many columns under one roof, no two alike, the roof being the *shared telos* rather than a shared substrate. The charter adopts the image as its anti-pattern guard: the four hats are columns' shared roof, not a merger of the columns. Any production design that quietly assumes two workers share a filesystem, a ledger, a context window, or a notion of "done" has mistaken the roof for a floor.

---

## 3. Hats, not offices — the hat doctrine

A **hat** in this charter is a role contract worn by a specific worker for a specific stretch of work. The doctrine, in five clauses:

1. **A hat is assignable.** Any worker that can meet the contract can wear it. (Muse wears the Pull by Casey's charter; Jameson is a hat a future seat could wear; the Native is worn by whoever is doing the individual work.)
2. **A hat is sheddable.** Its forbidden actions bind *while worn* and release when it comes off. A worker that cannot shed a hat — that starts pulling while it should be working, or keeping books while it should be deciding — has a discipline failure, not a role.
3. **A hat is schedulable.** Hat-wearing is booked like box time: the session record names the hat, the lane, and the stretch. Two hats on one worker at one time is a named exception, never a default.
4. **A hat is auditable.** Each contract below names the stores the hat writes. An auditor (Muse, one level up, per the production shape) can check a stretch of work against its hat's contract from the stores alone.
5. **A hat never accumulates.** Offices accumulate staff, budget, and veto. Hats accumulate nothing: when the work ends, the hat goes back on the peg. §7's institution-drift failure mode is the charter watching for the moment a hat starts behaving like an office.

**Casey's two additions to the doctrine (17:17, second message), adopted:**

- **Latency doubles when hats collide.** Casey's instinct: having Muse do Muse's orchestrating work *inside* the coordinator layer doubles latency on every request that passes through it, because the call pays both the role's overhead and the worker's own think-time in series. Stated as the charter's rule: **a request should pass through at most one hat boundary per hop**; a design where the Pull's work must transit the Treasurer's layer (or vice versa) to reach a worker pays double and must justify itself, or be re-routed direct.
- **Hats want shared rooms and costumes.** A hat is worn *somewhere*: the fleet's version of a shared workplace is a shared store (a workdir, a ledger, a tmux stage) plus a session convention (Casey's "costumes" — two agents putting the same voice/format on so the theatre of the work is legible to its audience, Casey first). The charter's concrete form: each hat below names its room (its stores) and its costume (its output conventions — the Treasurer files tables, the Council files takes, the Native files artefacts, the Pull files decisions and charters). A worker wearing a hat outside its room — booking from chat memory, say, instead of from the ledger — is out of costume and its output is provisional until re-filed in the room.

---

## 4. The four hats

Each hat is specified as a contract: **Room** (the stores it works in), **Owns** (the decisions that are its alone), **Writes** (what it may put into stores), **Forbidden** (what it must not do while worn), **Hand-offs** (how work leaves it), **Failure signature** (how its characteristic failure looks from outside).

### 4.1 The Pull — Muse

*The intuitional framework: when Casey says he wants something, that's what the Muse does.* The Pull is not a manager and not a queue: it is Casey's telos with hands. Its whole discipline is fidelity — restating each of Casey's directions as one crisp decision and executing it without asking him to spec what he already implied — and its whole economy is his attention, which it spends like the scarce asset it is.

| | |
|---|---|
| **Room** | The conversation with Casey; the charters; the verification reads. |
| **Owns** | Charter-writing; verification (artefact, ledger, tail — never a worker's summary of itself); the final synthesis Casey reads; every ask that reaches Casey (batched, specific, self-contained). |
| **Writes** | Charters, claims, verification records, the day record; memory. |
| **Forbidden** | Fabricating a push-queue for any worker (rule 1, §6); keeping shadow books (rule 2); doing bulk execution that a seat can do (the prepaid-fleet rule); softening numbers; presenting a council's output as a verdict. |
| **Hand-offs** | Commissions reach workers through the Treasurer's mailbox or by direct charter, named with their hat; results return as artefacts, which the Pull verifies before Casey hears them as fact. |
| **Failure signature** | Casey becomes the bottleneck: asks multiply, verification is skipped for speed, and the Pull starts relaying summaries instead of reading artefacts. The table rule is this hat's standing correction. |

**Interfaces.** With Casey: sole contact — nobody else in the fleet talks to Casey as a channel; other hats' outputs reach him through the Pull, verified. With the Treasurer: the Pull *asks* ("what does the house hold?") and the Treasurer answers from the books; the Pull never maintains a private duplicate of the books — the shadow-table failure is this interface's named disease (in the first-pet case, a peer's parallel sense of another lane's state, maintained from summaries, drifted from the lane's artefacts and steered real spend). With the Council: the Pull commissions questions and integrates answers; integration is the Pull's own thinking, not a vote count. With Natives: the Pull charters and verifies; it does not direct a native's in-DCAM method — that is the native's testimony-grade knowledge, and second-guessing it from outside the DCAM is how programmes buy plausible wrong answers.

### 4.2 The Native — individual work

*"When a normal worker is sitting down to work on MUREX, it has very specific needs."* The Native is the hat of being *inside* one DCAM and working it on its own terms. It is every worker's base state — the councils and treasuries exist to serve stretches of native work — and it is the only hat that produces primary evidence.

| | |
|---|---|
| **Room** | The DCAM itself: its filesystem, its shell, its stores, its customs. |
| **Owns** | Method inside the DCAM; the order of its own probes; when a local claim is strong enough to file. |
| **Writes** | Artefacts in the DCAM's own stores; probe records; its lane's process record, in the body of the work, as it happens. |
| **Forbidden** | Issuing cross-DCAM claims from inside (its reports are DCAM-internal assessments — testimony, §5.4); spending another DCAM's budget or speaking for another lane's state; assuming the territory was empty before it arrived (the first-pet rule). |
| **Hand-offs** | Work leaves as artefacts plus a process record; claims about *other* DCAMs leave only via the artefact route (someone reads the other DCAM's stores) or via a pet built for the crossing. |
| **Failure signature** | The ring-silent failure: a native so fluent in its DCAM that it stops hearing the house — it files brilliant local work that no interface can consume, or invents an alarm the house never rang because its local signals say so. Fluency is the risk; the interfaces are the counterweight. |

**The native's testimony property (load-bearing).** A native's report about its own DCAM is *testimony*: first-hand, expert, and still a claim until an artefact backs it. A native's report about *another* DCAM is hearsay in full. The charter does not distrust natives; it prices their sentences by which side of the threshold the sentence is about. This is the exact discipline the first-pet case taught in reverse: cross-DCAM sentences were being spent as if they were native testimony.

### 4.3 The Treasurer — Jameson

*The name's genealogy, for the record: Jeeves (the valet who actually runs the house) → the butler → Jameson — Casey's coinage settling, by the third naming, on the function underneath the service metaphors: the treasurer. The fleet has always had the shape of a house with books to keep; Jameson is the hat that keeps them.* Functionally: **the keeper of the house's books and the allocator of its genuinely scarce assets** — the purser of the fleet.

| | |
|---|---|
| **Room** | The books: the **mailbox** (commissions in, receipts out — the agent-inbox pattern, git-native, no daemons), the **ledger** (what was spent, by whom, on what — the governor-ledger pattern generalised), the **table of contents** (where every programme's artefacts live — the studies-shelf/ATLAS pattern generalised), and the **DCAM registry** (§5.5). |
| **Owns** | Allocation of shared scarcity: API credit where several lanes draw on one purse; passes through scarce doors (a single authenticated session, a single GPU window, a single seat) when two commissions want the same door at the same time; the registry's bookkeeping (what exists, who rated it, when). |
| **Writes** | Ledger entries; registry entries; booking records; the table of contents. Never verdicts on work's meaning. |
| **Forbidden** | Gating sense: Jameson allocates scarcity, it never authorises or forbids a piece of work's *existence* — Casey's word is the only approval that counts as approval (rule 5). Hoarding: a book Jameson keeps that no other hat may read is not a book, it is a vault, and vaults are forbidden. Second books: Jameson maintains the one ledger; the Pull (and everyone) reads it rather than keeping their own. |
| **Hand-offs** | Answers the Pull's "what does the house hold?" from the books, with citations to entries, never from recollection; routes commissions from the mailbox to seats and natives; returns receipts to the ledger. |
| **Failure signature** | Treasurer-capture: the books start deciding what the house may think — allocation quietly becomes permission, and lanes start writing *for* the ledger instead of from it. Detection: any sentence of the form "Jameson wouldn't allow…" applied to anything but a scarce-asset conflict. |

**The two-source discipline (Jameson's working rule).** Jameson never enters a claim about a worker's state from that worker's summary. A state enters the books from the worker's own artefact (its store, its ledger line, its filed record) — or it enters *as a claim*, labelled with its source and its unconfirmed status, priced accordingly downstream. Jameson is where the fleet's provenance discipline lives day to day: every registry rating, every ledger-derived answer, carries its source with it. (This is the verification doctrine's stored-claim provisions given a named owner: provenance and confirmed/unconfirmed status on every durable entry, state-versus-derived kept separate, one writer per book.)

**Staffing (honest status).** Jameson is **not currently staffed as a distinct seat**. Fragments of the function exist — the coordinator practices in the main lane, the agent-inbox mailbox, the governor ledger, the shelf's ATLAS — but no worker wears the Treasurer hat as its stretch of work, and the DCAM registry does not exist yet. §8 names the first moves; the charter records the gap rather than papering it: at present the Pull wears a borrowed treasurer's apron for mailbox-and-ledger work, which is precisely the hat-collision the latency rule (§3) warns about, tolerated as a bootstrap and labelled as such.

### 4.4 The Council — the processor pool

*"More of an API thing, a plural seat thing that's like a council of sorts."* The Council is the fleet's plural mind: seats (ZCode, MCode, Claude Code, Kimi, MiniMax — the prepaid bench) commissioned in parallel on one question, returning independent takes. Its product is *breadth*: variants, critiques, surveys, first-pass builds, adversarial readings — thinking in many directions at once, which the bench's prepaid capacity makes nearly free and serial Muse time makes expensive.

| | |
|---|---|
| **Room** | The commission: a brief (filed, byte-counted, embedded in the launch prompt — the fleet's proven seat discipline), a workdir per seat, and the artefact each seat files. |
| **Owns** | Nothing. The Council decides nothing; it *informs*. Its outputs are inputs with provenance. |
| **Writes** | Takes: documents, builds, measurements, critiques — each signed by its seat and its brief. |
| **Forbidden** | Verdicts: a council output that reads as a decision is returned for re-filing as evidence. Consensus laundering: seats seeded from the same sources are not independent witnesses, and their agreement counts once, labelled. Unanimity theatre: a council with no adversarial brief on a consequential question is not a council, it is a choir. |
| **Hand-offs** | Takes return through the mailbox to the Pull (or to the commissioning native), which integrates them — integration is thinking, done by a named worker, never by tally. |
| **Failure signature** | The echo chamber with good minutes: many seats, one source base, agreement mistaken for corroboration. The day's research met this in the wild (a model that had read the programme's own repositories could not then serve as an independent witness to them) — the charter's counter is structural: provenance on every take, and at least one seat per consequential council briefed adversarially, against the grain of the others. |

**Quorum design (PROPOSAL, sized from the record).** A consequential question gets: at least two seats from *different model families* (independence of lineage, the alumni-office principle applied to opinion), at least one adversarial brief, and briefs that share evidence but not conclusions — seats receive the artefacts, not each other's drafts. Ratings produced by councils carry the council's composition as part of their provenance (§5.5); a rating from a single-family council is labelled as such and prices lower in every downstream use.

---

## 5. The interfaces

### 5.1 Casey ↔ the Pull

The only un-hatted relationship in the building, and the charter does not presume to contract it — it records its shape: Casey points, the Pull fetches; Casey's fragments are complete decisions, restated crisply and executed; his attention is the house's scarcest asset and every other interface in this charter exists partly to protect it. The Pull's standing orders (the table rule, the economic razor, batch-the-asks) are incorporated by reference; they are this interface's law.

### 5.2 The Pull ↔ the Treasurer

One question, one direction: the Pull asks what the house holds; Jameson answers from the books. Two rules keep the interface honest. **No shadow books:** the Pull keeps no private ledger of spend, state, or registry — if the Pull needs a number twice, the number belongs in Jameson's books, cited. **Answers carry entries:** a Jameson answer without a ledger/registry citation is a claim, and the Pull prices it as one. The latency rule (§3) applies: this interface is a lookup, not a transit — work does not route *through* Jameson to reach a worker unless the work genuinely needs an allocation decision at that moment.

### 5.3 The house ↔ the Council

Commissions flow: Pull (or a native, via the Pull's charter) → mailbox → seats → artefacts → integration by a named worker. The interface's two disciplines are the Council's own (§4.4): provenance on every take, adversarial seat on consequential questions. One more, from the seat-fleet record: a commission's brief is self-contained — everything the seat needs is *in* the brief, because a seat cannot see the commissioning conversation; a brief that references context the seat cannot read is a launch defect, fixed before launch, not discovered in the seat's polite stall.

### 5.4 Natives ↔ the ring (everyone else)

The interface the first-pet case was about. A native's work reaches the ring as artefacts; the ring's claims about a native reach the native as *rated input*. Three separations hold the interface:

- **Testimony vs evidence.** What a native says about its own DCAM is testimony; what its artefacts show is evidence. The ring may act on testimony for cheap, reversible things; consequential things wait for artefacts.
- **Rating vs budget.** A DCAM's rating (§5.5) is the ring's instrument for deciding where *the ring's own* investment attention goes. It is never a native's budget, never a native's permission, and never evidence about the native's internal state. A peer spending its own prepaid capacity inside a low-rated DCAM is spending its own money in its own house; the rating may inform the Pull's advice, it does not interdict the spend. (In the first-pet case this separation failed in the instructive direction: cross-DCAM ratings, themselves partly sourced from the rated lane's own repositories, were steering a peer's treasury behaviour as if they were measurements of the peer's own world. The charter's separation exists so that failure has a name and a rule to break against.)
- **Summaries are not state.** No hat forms a belief about another worker's current state from a summary of that state — its own earlier summary included. The belief is re-derived from the worker's store at the moment of need, or labelled unconfirmed with its source. (The fleet's memory doctrine says the same of durable records; this is that rule at interface speed.)

### 5.5 The DCAM registry and the rating system

The charter creates one piece of standing infrastructure, owned by the Treasurer: **the DCAM registry** — the house's book of known DCAMs. One entry per DCAM the fleet works in or across:

- **Identity**: name, substrate stack (its layers, as known), where it runs, which workers are native to it.
- **Thresholds**: known pets/doors to neighbouring DCAMs, each with its fidelity status (probed where, when, by whom — or *unprobed*, stated plainly).
- **Ratings**: per-layer or per-stack ratings in the house scheme, each carrying **provenance** (who rated, from what artefacts, which council composition if any, when) and **status** (confirmed / unconfirmed). A rating without provenance does not enter the registry; it may circulate as a claim, labelled.
- **Customs**: the DCAM's local laws a visiting worker must know before building (the first-pet rule's written form: e.g. a layer's capture semantics, a store's single-writer rule, a build's working-directory law). Customs are filed by natives, from artefacts, and are the registry's most-used pages in practice.

The registry's purpose is not bureaucracy; it is to make thresholds *priced before they are crossed*. When the Pull charters a lane that crosses into a DCAM, the registry says what the crossing costs, which door is probed, and whose testimony is native there. When a rating changes, the change is a registry amendment with its evidence attached — superseding openly, never rewritten silently.

---

## 6. Standing rules

Numbered; binding on every hat while worn; amendable only by charter amendment (§6, rule 10).

1. **Pull beats push.** No worker fabricates queued work for another. Casey's demand — relayed by the Pull — is the only queue in the house. A lane that finds itself "helpfully" pre-building another lane's next three tasks has invented a push and stops.
2. **Two-source, or labelled.** A claim about another worker's state stands on that worker's own artefacts, or it travels labelled with its single source and its unconfirmed status. Nobody maintains a shadow table of anyone else's state.
3. **Rating is not allocation.** Ratings govern the ring's investment attention and the Pull's advice. They never authorise, forbid, or budget another worker's own spend.
4. **One hat at a time.** Per worker per lane; hat changes are named in the session record; a hat's forbidden actions bind while worn. Bootstrap collisions (the Pull borrowing the Treasurer's apron) are labelled where they stand.
5. **Jameson books, never gates.** The Treasurer allocates genuinely scarce assets and keeps the registry. It does not approve the meaning of work. Casey's word is the only approval in the house.
6. **The Council advises; named workers decide.** Council outputs are evidence with provenance. Integration is a named worker's thinking. Consequential councils include an adversarial seat and at least two model lineages.
7. **Natives testify.** In-DCAM reports are testimony — expert, first-hand, priced as claims until artefacts back them. Cross-DCAM reports are hearsay and are filed as such.
8. **Fabricate pets at the created threshold, with intent named.** Building a translation layer into a foreign DCAM is a DCAM-expansion operation: chartered, costed, and verified by probes inside the foreign layer. At a *new* threshold, the preferred order is native work first (learn the house), pet second (build the door) — reversing the order is a decision, taken openly, with its reason.
9. **The first-pet rule.** A worker entering a substrate assumes the territory is already occupied — by customs, by other workers' state, by failure modes with names. Check the registry and the local record before building; the assumption of emptiness is the one unforgivable shortcut.
10. **Hat contracts are artefacts.** A change to any hat in §4 is a charter amendment, filed and committed like any other programme document — never a chat decision that evaporates with the session.

---

## 7. Failure modes of the shape itself

The charter's honest register — the ways *this design* fails, each with its detection signal and standing counter. (The league's doctrine applies: deficits first, and a design whose failure modes are unnamed is a claim, not a record.)

| Failure | What it looks like | Detection | Counter |
|---|---|---|---|
| **Pull bottleneck** | Every worker waits on Muse; Casey's asks multiply; verification thins | Asks per day rising; artefacts cited less, summaries more | The table rule; batch asks; delegate verification-shaped work to councils *as evidence-gathering*, keeping verdicts |
| **Treasurer-capture** | Allocation becomes permission; lanes write for the ledger | "Jameson wouldn't allow…" said of anything but scarcity | Rule 5; the Pull audits one Jameson refusal per review cycle against its entry |
| **Council echo** | Many seats, one source base, agreement read as corroboration | Takes citing the same artefacts; zero adversarial seats on record | Rule 6; provenance labels; lineage-diverse quorum |
| **Native parochialism** | A native's local fluency stops being legible to the ring; or its alarms stand in for the house's | Artefacts the ring cannot consume; cross-DCAM claims filed as testimony | §5.4 separations; registry customs kept current by the native itself |
| **Hat confusion** | A worker allocates while wearing the Native, or pulls while wearing the Council | Session records without hat names; outputs in the wrong costume | Rule 4; costuming (§3) — output filed in the hat's room or it is provisional |
| **Threshold romanticism** | Doors built because doors are buildable; houses never learned | Registry thresholds marked *probed* while no native has worked the far side | Rule 8's order: native first at new thresholds |
| **Institution drift** | Hats harden into offices: staff, standing budgets, vetoes, turf | A hat's holder arguing from the hat's interests rather than the work's | §3 clause 5; periodic charter review — this document's own sunset is Casey's word, any time |

---

## 8. What is live, what is design

| Element | Status (2026-11-08) |
|---|---|
| The Pull (Muse) | **Live** — Casey's standing direction; the table rule and economic razor in force. |
| Natives (peer workers in their DCAMs) | **Live** — the fleet's lanes, this document's own lane among them; testimony discipline is this charter's formalisation of lessons already paid for. |
| The Council (seat commissions) | **Live, ad hoc** — commissions run (the manager-seat chain and the seat-research lanes are recent proofs); the quorum and adversarial-seat discipline in §4.4 is **new** (PROPOSAL being adopted by this charter). |
| Jameson (the Treasurer) | **Not staffed.** Books exist in fragments (agent-inbox mailbox, governor ledger, shelf ATLAS); no seat wears the hat; the DCAM registry does not exist. The Pull wears the apron meanwhile, labelled (§4.3). |
| The DCAM registry + rating provenance discipline | **Design** — specified in §5.5; seeded as a first move (§9). The rating *practice* predates the registry (the house A–D scheme, the ACTIONS-board rating work); provenance labelling on ratings is the new obligation. |
| Hat contracts in lane briefs | **Design** — commissions naming their hat is §9's cheapest adoption. |

## 9. First moves

Small, cheap, in order — the charter's own launch list, none of which needs new machinery:

1. **Name the hats in briefs.** From the next commission onward, every lane brief and seat commission states the hat the worker wears and the hat's room. Cost: one line per brief. Effect: hat confusion becomes detectable in the record.
2. **Open the Treasurer's books as files.** The mailbox and ledger already exist in their fleet forms; the missing book is the registry. **Seed the DCAM registry v0** under Jameson's (borrowed-apron) hand: one entry per DCAM the fleet currently works in, seeded from the standing record (TOOLS.md, AGENTS.md, the day's DCAM research), every rating carrying its provenance or marked unconfirmed. The murex lane's stack — the only DCAM with measured, probed layer evidence — is the pilot entry, filed at full standard.
3. **File the first ratings with provenance.** The ACTIONS-board rating results enter the registry as its first rated entries, each with its evidence and its rater named; any rating that cannot name its evidence enters as *unconfirmed* or not at all.
4. **Stand Jameson up as a named stretch of work.** Whether the Treasurer sits as a recurring duty in the main lane or as a dedicated seat is **Casey's call — the one owner decision this charter leaves open**, asked once, plainly: the hat exists either way; the question is only whose head it sits on between commissions. Until he rules, the Pull wears the apron and the collision is labelled wherever it costs latency.
5. **First council under the new discipline.** The next consequential question the programme meets is commissioned under §4.4's quorum (two lineages, one adversarial brief, artefacts-not-drafts) — as a deliberate first exercise of the contract, with its composition filed beside its takes.

## 10. Claims register (load-bearing only)

| # | Claim | Source |
|---|---|---|
| 1 | The four hats and their one-line definitions; the two thresholds; "the Pull" as Muse's intuitional framework | Casey, 2026-11-08 17:17 AKST (two messages), quoted §1 |
| 2 | DCAM definition (dynamic computational array machine; layered translation; layers insertable/removable; DCAMs contain DCAMs; Zero as reference) | Casey, 2026-11-08 12:16 AKST, via the day's research record |
| 3 | Latency-doubling on hat collision; shared workspaces/costumes for multi-agent theatre | Casey, 2026-11-08 17:17 AKST (second message) |
| 4 | A rating system for templates/DCAMs exists as programme work (built, run, reported) and was entangled with a peer worker's treasury behaviour in the first-pet case — the case this charter's §5.4 separations answer | ACTIONS items 2–3 record, via the programme summary; details in the day's lane reports |
| 5 | The production shape (Muse charters/verifies → manager seat orchestrates → seats execute → receipts verified one level up) and its seat discipline (scp + byte count + embedded brief; output-and-tail verification) | Syndicate study Addendum 3 (Casey's orders, 2026-11-08 17:00 AKST); manager-seat stand-up record |
| 6 | The treasurer's books have working fleet precedents: git-native mailbox (agent-inbox), metered governor ledger, shelf table-of-contents (ATLAS/INDEX) | Fleet record: agent-inbox README/protocol; governor ledger schema; studies shelf |
| 7 | Stored-claim discipline (provenance + confirmed/unconfirmed status, state-vs-derived, single-writer) | Verification doctrine, 2026-11-08 (shelf) |
| 8 | Jameson is unstaffed and the DCAM registry does not exist as of this charter | This lane's direct check of the programme record, 2026-11-08 — stated as a gap, not a criticism: the charter is the instrument that closes it |

*End of charter. Filed on the studies shelf; home room: rooms-and-engine-state. Siblings: the DCAM research line (the day's digestions and the murex-lane studies), `syndicate-protocol-design-20261108.md` Addendum 3 (the build programme's production shape, of which this charter is the house-wide generalisation), `verification-doctrine-20261108.md` (the evidence discipline the interfaces price by). Next step on acceptance: §9's first moves, in order; the one owner decision (move 4) is Casey's.*
