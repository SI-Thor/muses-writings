# TOWN-0 Build Charter — Execution Plan for the Town's First Milestone

*The execution plan the NPC Town charter named as its next programme step:
"the TOWN-0 build charter — district acceptance, cast, governor write, muster
proof — under the production shape." Design authority:
`npc-town-charter-20261108.md` (the town charter), read in full before this
document was written — its §0.1 order of operations, §1 cast and geography,
§1.3 daylight law, §2.4 governor table, §5 TOWN-0 criteria and §7 failure
table are the requirements this plan executes and does not revise.
Substrate authorities: `syndicate-of-four-spec-20261108.md` (scratch-server
construction, join-in-order, governor launch gate, config-write discipline),
`syndicate-protocol-design-20261108.md` §5 (the Sitka generation pipeline and
its landmark/scale spec), the decode-rate settlement (20 metered probes:
plan on ~120–130 tok/s single-stream on `:8311`, ~79 tok/s per call at
4-way concurrency), and the league's OPERATIONS.md record as cited by both.
Production shape (town charter §0.1, Syndicate Addendum 3): **Muse charters
and verifies → a Claude Code manager seat orchestrates → ZCode/MCode seats
execute in parallel → receipts flow back up, verified against world
evidence.** Where a number here is a proposal rather than an inherited
measurement, it is labelled PROPOSAL.*

---

## 0. What this document is, and its declared decisions

The town charter specified *what TOWN-0 is* — the town exists and the
expensive stack is live — and deliberately left the build decomposition to
this charter. This document decomposes TOWN-0 into seven work packages
(WP-0…WP-F), each with a named owner seat, inputs, outputs, acceptance
evidence drawn only from stores the producer cannot write, and explicit
dependencies. It sequences the packages against the programme's actual
state — **Sitka-gen (Spike 1) is still in flight; the district does not
exist yet** — and it states, per package, whether work can start now or
gates on district acceptance. No package in this plan quietly assumes the
district exists; §4's sequencing table is the control against that failure.

Decisions declared here, in the open, where the town charter left room:

1. **Town workdir (Thor): `~/npc-town/`** — `server/` (the town's own Paper
   instance), `manifest/` (cast manifest, district acceptance record, the
   TOWN-0 claim file), `scripts/` (Reflex Pack v0 and the script book),
   `tom/` (the theory-of-mind store, per town charter §4.2), `days/` (day
   records), `receipts/` (probe receipts, census outputs, hold audits).
   The town's stores live together and apart from the league's: no town
   file is written inside `~/craftmind-league/`, and no league file is
   written by a town lane.
2. **Cast names are proposed here and filed at muster** (the town charter
   fixes the trades, not the names; §3 WP-C). Names are harbour-town names
   in Sitka's own layered spirit — Russian, Norwegian, Tlingit-adjacent
   maritime, plain working names. They are PROPOSAL until the cast manifest
   is filed; renaming before the first join costs nothing, renaming after
   costs an identity.
3. **The manager seat for TOWN-0 is the ProArt Claude Code seat** (the
   proven stand-up: `~/fleet-manager/` on eileen, charter chain byte-
   verified end-to-end on 2026-11-08), re-chartered for this programme per
   §5. The Thor-heavy acceptance runs (mcprobe census, walk proof, hold
   audit) are **Muse's verification work, not the manager's** — the
   manager orchestrates seat-executable builds; verification lives one
   level up, with Muse, against world evidence. That split is the
   production shape working as designed, not a gap in the manager's remit.
4. **TOWN-0 is claimed on the real district or not at all.** Substrate
   packages may *prove themselves* on a scratch flat test world while
   Sitka-gen is in flight (§4), but the milestone's own criteria (town
   charter §5) name the Sitka-gen district, mcprobe-verified. A substitute
   board produces evidence about the substrate; it never produces TOWN-0.

### 0.1 The milestone this plan executes (town charter §5, TOWN-0, restated as the claim)

TOWN-0 is claimed when **all** of the following are verified by Muse
first-hand, each from its named store:

- The Sitka-gen district is in place on the town's own server,
  mcprobe-verified: terracing census in the walked band (5.4–9.5 step
  faces per 100 columns) across the town's rounds.
- Homes row (8), store, dock store, cathedral square with notice board,
  and the first worksite are present and surveyed; the street network's
  routes are filed as surveyed routes.
- All 8 citizens spawned as genuine identities; `.dat` sha256s in the town
  manifest; presence re-verified in LIVE immediately before the first
  operating window.
- All 14 governor identities (town charter §2.4) exist in config,
  grep-verified, with one metered probe receipt each in the governor
  ledger. Any identity on the silent default blocks the milestone.
- The non-lethal regime and the daylight hold are verified against the
  **running server** (gamerules/difficulty read live; two consecutive
  refreshes verified as landed in the server log).
- One full muster walked: all 8 citizens home→square→home on surveyed
  routes, forcedMove count **zero**, read from the server-side record.

Every work package below exists to make one or more of those lines true
and provable. A package is done when its acceptance evidence exists in its
named store — not when its owner seat reports it done.

---

## 1. Work package map

| WP | Package | Owner seat | Gates on |
|---|---|---|---|
| WP-0 | Programme claim, bookings, town workdir | Muse (chartering) | — (starts now) |
| WP-A | District acceptance | Muse (verification) over the Sitka-gen lane's output | Sitka-gen delivery |
| WP-B | Town server | Manager seat → ZCode/MCode execute | WP-0; district install gates on WP-A |
| WP-C | Cast | Manager seat → seats execute; Muse verifies manifest | WP-B + WP-A (joins); design starts now |
| WP-D | Governor write | Manager seat → seats execute; Muse verifies diff + receipts | WP-0 (starts now) |
| WP-E | Reflex Pack v0 | Tier L drafting (manager-orchestrated seats) | District *spec* now; final routes gate on WP-A |
| WP-F | Muster proof (the TOWN-0 acceptance run) | Muse (verification) over manager-run execution | WP-A…WP-E all accepted |

Owner-seat language follows the production shape exactly: "manager seat →
seats execute" means the ProArt manager decomposes the package into seat
briefs, commissions ZCode/MCode, assembles their output into the package's
artefacts, and files the receipt trail in its LOG — and **does not grade
the result** (§5.2). "Muse verifies" means Muse reads the artefact, the
ledger and the tail first-hand before the package is called accepted.

---

## 2. WP-0 — Programme claim, bookings, town workdir

**Owner:** Muse (chartering level; not delegated — this is the claim
every other lane reads before it launches).

**Inputs:** this charter; the town charter; the fleet's parallel-lane
shared-state discipline (claim shared mutable state before parallel lanes
touch it; one named owner per seam; reconcile by reading the live
location).

**Work:**
- File the shared-state claim for the TOWN-0 programme: the seams are
  (a) the Thor governor config (WP-D owns the write window; no other lane
  edits `~/craftmind-league/config/governor.json` while the claim stands),
  (b) the Thor `~/npc-town/` tree (town lanes only), (c) the ProArt
  manager's workdir and seats (WP-B…WP-F commissions), (d) the studies
  shelf + research-trail repo (this charter's lane owns the TOWN-0
  filings until hand-off).
- Book the boxes in SuperInstance/agent-inbox `schedule/`, one file per
  box, per the standing protocol (lane, seat, start UTC, planned duration,
  check-by time): Thor (server + governor windows), ProArt (manager seat —
  exclusive while commissioned), Orin (front-room observation only; the
  town server is Thor-hosted per the spec's construction, and the Orin's
  live league world is **not** a TOWN-0 surface).
- Create `~/npc-town/` and its subdirectories (decision 1, §0) with a
  README naming this charter as the programme's authority.

**Outputs:** the claim record; the schedule bookings; the empty town tree.

**Acceptance evidence:** the claim and bookings readable in agent-inbox
(committed); `ls` of the town tree from a fresh Thor shell. World-evidence
standard applies even here: a booking nobody can read is not a booking.

**Dependencies:** none. **Starts now.**

---

## 3. The build packages

### WP-A — District acceptance

**Owner:** Muse (verification), over the Sitka-gen lane's delivered
district. The generator does not accept its own output — acceptance reads
the world through mcprobe, a code path the generator doesn't write (the
twin study's two-way rule, and study §5.4's verification loop).

**Inputs:** Sitka-gen's delivered district (region files + the generator's
own filing: crop coordinates, terracing parameters — band height, per-
district step-face density targets — the OSM pad/road raster, sea level
y 63, the landmark table from study §5); the league's surface-census
method and its measured bands (walked band 5.4–9.5, veto band 24.8–29.4
step faces per 100 columns; the route-relief survey's companion floor
metric where canopy masks the headline figure).

**Work and acceptance tests, in order:**

1. **Terracing census.** mcprobe re-read of the whole town area: step-face
   density computed per district and per named round (the town charter
   §1.2 geography: homes row streets, store↔dock store, square approaches,
   the carter's circuit streets, worksite approach). **ACCEPT line: every
   town round's corridor reads in the walked band (≤9.5/100 columns)**,
   with the floor-based companion metric reported wherever canopy or
   structure masks the headline. Deliberately ungraded obstacle terrain,
   if the generator designates any (study §5.3 rule 4), must be outside
   every town round and have its density published in the acceptance
   record — an ungraded pocket *on* a round is a census failure, not a
   designation.
2. **Landmark placement check.** Against the gen spec (study §5 + the OSM/
   charts layers): (a) **the cathedral block** — St Michael's Cathedral's
   plot on Lincoln Street present as pad + icon placement, correctly
   seated relative to the Lincoln Street frontage and the square (the
   twin corpus's most-surveyed block; its position is checkable against
   1,492 logged street frames); (b) **Castle Hill** — the rise present at
   its OSM/charts position relative to the harbour and the downtown grid,
   at the core's 1:1 vertical (it is inside the playable crop, not
   backdrop), its approaches terraced to the walked band like every other
   town surface; (c) harbour frontage and waterline at y 63 continuous
   with the charts coast; (d) the town-functional plots exist as graded
   pads: homes row frontage, the store plot, the dock store plot, the
   worksite plot. Placement tolerance: PROPOSAL — pad centres within
   ±3 blocks of the OSM-derived position, orientation matching the street
   grid; a landmark outside tolerance is misplaced even if beautifully
   built, because the town's rounds and the twin loop's batteries are
   written against the real map.
3. **Bot walk proof.** A fleet mineflayer body (a throwaway acceptance
   identity on the *acceptance copy* of the district, never a cast name)
   walks the muster skeleton — homes row → square → dock store → square →
   homes row — on the filed routes. **ACCEPT line: the walk completes with
   forcedMove count zero** (the Q1a pattern: displacement is truth, read
   server-side). Any pin, grind or forcedMove loop is a census-class
   failure with coordinates attached, whatever the density numbers said —
   the walk is the census's own placebo arm.
4. **The acceptance record.** Filed at `~/npc-town/manifest/district-
   acceptance.md`: census tables, landmark check results with the
   evidence pairs, walk-proof log extracts, and the verdict.

**Outputs:** the accepted district (installed into WP-B's server by WP-B's
procedure, from the accepted files — hash the region set at acceptance so
what was accepted is provably what was installed); or a send-back.

**ACCEPT / SEND-BACK rule.** ACCEPT requires all three tests green.
SEND-BACK is a filing, not a mood: the failing census (per-corridor
densities), the failing landmark coordinates, or the walk-proof pin
coordinates are attached, `fault_owner` assigned from the amendment's six
values (a terracing miss is `world`; a generator defect is `harness`; a
spec ambiguity is `prompt`), and the district returns to the Sitka-gen
lane with the evidence. One send-back cycle is normal programme weather;
a second failure on the *same* corridor escalates to Muse + the gen
lane's charter, not a third quiet retry.

**Dependencies:** Sitka-gen delivery. **Nothing in WP-A can start before
the district lands** — but its instruments (census scripts, the walk-proof
harness) are league-proven and need no preparation window; they are
re-pointed, not rebuilt.

### WP-B — Town server

**Owner:** manager seat → ZCode/MCode execute (server build, config,
harness scripts); Muse verifies (§5.3).

**Inputs:** the Pilot A spec's scratch-server construction (fleet Paper
26.1.2 build 74 bundle, Java 25+, own directory, own ports — booked, not
assumed free; the paint spike's port discipline and its RCON-collision
lesson apply); the town charter §1.3 regime; the guarded cameraman chain
as the hold's reference implementation.

**Work:**
- Build the server at `~/npc-town/server/`: own ports (game + RCON)
  recorded in the booking; `world/players/data/` **empty by
  construction** and verified by direct directory listing (never a
  `-path "*players/data*"` pattern — OPERATIONS §1's search trap, carried
  in the spec).
- Regime, set and then **read back from the running server** (never from
  files alone — the NORMAL-difficulty divergence is the standing lesson):
  non-lethal night by construction (difficulty and spawn rules per the
  town charter §1.3: the night is a pause, not a threat), the town's spawn
  point on the square, daylight-hold parameters for the day parts.
- The **daylight-hold harness**: the guarded pattern (refresh on a fixed
  cadence, each refresh **landing-verified in the server log** within its
  window; **two consecutive misses = HOLD-LOST** — alarm + park: citizen
  drivers stop issuing work, citizens hold or shelter per standing
  orders). Built and proven *before* any cast join: the hold proof is two
  consecutive refreshes read as landed in the server log, on this server,
  in its own log.
- District install procedure (executes when WP-A accepts): copy the
  accepted region set, verify hashes against the acceptance record,
  boot, re-read spawn and regime from the running server.
- Booking in agent-inbox `schedule/thor.md` for the server's standing
  windows; the server is stopped outside chartered windows until TOWN-1
  (a town server left running unattended is a hold waiting to be lost).

**Outputs:** a bootable, regime-verified town server; the hold harness
with its proof receipts in `~/npc-town/receipts/`; the install record.

**Acceptance evidence:** directory listing showing `players/data` empty
at construction; the running server's own readback of difficulty/
gamerules (console query output filed); two landed-refresh log lines with
timestamps; port/booking record. **A server whose regime was only read
from its files is not accepted** — that sentence is the divergence
finding applied.

**Dependencies:** WP-0. **Starts now** — the server skeleton, regime and
hold proof are all provable on a scratch flat test world while Sitka-gen
is in flight (§4); only the district install gates on WP-A.

### WP-C — Cast

**Owner:** manager seat → seats execute (identity files, driver configs,
home/work assignment filing); Muse verifies the manifest against the
LIVE directory.

**Inputs:** town charter §1.1 (eight citizens, four trades, senior/junior
pairs) and §1.2 (functional geography); the spec §1.1 join protocol,
adopted whole.

**The cast (names PROPOSAL, §0 decision 2; trades and pairing per the
charter):**

| # | Name | Trade | Seniority | Home | Workplace |
|---|---|---|---|---|---|
| 1 | Maren | Harbour hand | Senior | Homes row H1 | Dock store + harbour workface |
| 2 | Ilya | Harbour hand | Junior | Homes row H2 | Dock store + harbour workface |
| 3 | Anka | Shopkeeper | Senior | Homes row H3 | Commons store, Lincoln St |
| 4 | Theo | Shopkeeper | Junior | Homes row H4 | Commons store, Lincoln St |
| 5 | Stian | Builder | Senior | Homes row H5 | The worksite |
| 6 | Runa | Builder | Junior | Homes row H6 | The worksite |
| 7 | Vera | Keeper of the square | — (sole) | Homes row H7 | Cathedral square + notice board |
| 8 | Tomas | Carter | — (sole) | Homes row H8 | The street network (all workplaces) |

Home/work assignments are stated functionally here and bind to surveyed
coordinates only at filing time, on the **accepted** district's geography
(WP-A): H1–H8 are the homes-row plots in filed order; workplaces are the
accepted pads. An assignment written against the gen *spec's* coordinates
before acceptance is a draft, labelled as such — the Door-moves lesson
generalised: never file a citizen's geography against a map nobody has
walked.

**Join protocol (per citizen, in cast order, no batching):**
1. Immediately before the join window: verify `world/players/data/` in
   the LIVE town server directory directly; confirm the pool holds
   exactly the `.dat`s of citizens already joined in this procedure and
   no others.
2. Join the one citizen; clean disconnect; verify **that citizen's own**
   `.dat` now exists in the LIVE directory; record its **sha256 in the
   town manifest** (`~/npc-town/manifest/cast-manifest.md`) beside the
   name, trade, home and workplace.
3. A `.dat` that appears under the wrong name, a hash that changes between
   disconnect and filing, or any unexpected file in the pool **stops the
   procedure** (§6 stop conditions) — the sample-clone's signature is a
   substrate emergency, never a retry.

**Outputs:** eight genuine identities; the cast manifest (names, trades,
pairing, homes, workplaces, `.dat` sha256s, join receipts).

**Acceptance evidence:** the manifest's hashes re-computed by Muse from
the LIVE directory and matching; the join-order log extracts. Presence is
re-verified in LIVE immediately before the WP-F window (the league's
Rule v2, inherited): a citizen whose save is absent at a launch has no
stable existence, and the town does not launch on a stale manifest.

**Dependencies:** design (names, assignments-as-drafts) **starts now**;
joins gate on WP-B accepted **and** WP-A accepted (the cast joins onto
the real district, into their real homes — joining onto a test world and
moving saves later would re-open the exact save-pool questions this
construction exists to close).

### WP-D — Governor write

**Owner:** manager seat → seats execute (the config edit, assembled by
the manager); Muse verifies the diff and the probe receipts. The
governor is shared league infrastructure on the Thor (`127.0.0.1:8642`,
config `~/craftmind-league/config/governor.json`) — WP-0's claim covers
the write window, and OPERATIONS §5's discipline governs the write.

**Inputs:** town charter §2.4's identity table (fourteen identities);
the spec §1.4 gate pattern; the decode settlement.

**The fourteen identities (town charter §2.4, verbatim budgets):**

| Identity | Consumer | Upstream | Budget (calls / mind-s per rolling 3600 s) |
|---|---|---|---|
| `town-maren`, `town-ilya`, `town-anka`, `town-theo`, `town-stian`, `town-runa`, `town-vera`, `town-tomas` | Citizen bodies (Tier R voice/routine) | `:8311` via `agentUpstreams` | 120 / 300 each |
| `town-roster` | Roster engine | `:8311` | 120 / 300 |
| `town-stock` | Stock engine | `:8311` | 120 / 300 |
| `town-works` | Works engine | `:8311` | 120 / 300 |
| `town-social` | Social engine | `:8311` | 60 / 300 |
| `town-reflect` | Tier L crafting shift | default `:8310` | 60 / 1800 |
| `town-smith` | Script-crafting seats (consult-book pattern) | books / `:8310` | 60 / 900 |

**Write discipline (OPERATIONS §5, in effect verbatim):** back up
`governor.json` first (hash the backup); write **all fourteen identities
in one edit**; verify in the same diff that every existing league identity
(cody, cody-actor, vega, geist-mind, pulse-smith, the syndicate set) is
**byte-unchanged**; time the governor restart **before operations
begin**, never mid-day and never inside a join or muster window (a restart
clears in-memory budget windows — that is priced, scheduled, and filed,
not discovered).

**The launch gate (BLOCKING, the spec's rule carried over unchanged):**
an identity counts as existing only when **both** halves exist —
(a) the config grep: the identity's name, budget and upstream read from
the live config by a reader who didn't write it; (b) **one metered probe
receipt per identity** in the governor ledger (`ledger/mind-calls.jsonl`):
a real probe call through the governor under that identity, its receipt
found in the ledger by identity name, upstream and budget window. Probe
shape note (decode settlement): plan on **~120–130 tok/s single-stream**
on `:8311` (median 130.2 measured); probes are short actor-shaped calls,
so the whole fourteen-probe gate is minutes of serving, and no budget in
the table was sized against the retired 7.9–8.4 steps/s figure. An
identity missing either half is on the **silent permissive default
(120/120)** by definition, and a town body on the default presents as a
dumb citizen — the gate blocks WP-F, full stop, with `fault_owner:
harness` on the filing.

**Outputs:** the written config (+ backup), the fourteen probe receipts,
the gate record at `~/npc-town/receipts/governor-gate.md`.

**Acceptance evidence:** Muse's independent config read + diff against
the pre-write backup (existing identities byte-identical); fourteen
ledger receipts located by grep, one per identity, post-dating the write.

**Dependencies:** WP-0's claim on the governor seam. **Starts now** —
the governor and both upstreams are live league infrastructure; nothing
in this package waits for the district, the server, or the cast. It is
deliberately the programme's first completable package: the cheapest
launch-blocking defect class in the fleet's record is retired before
anything with a body depends on it.

### WP-E — Reflex Pack v0

**Owner:** Tier L drafting, manager-orchestrated: the manager commissions
the drafting seats (ZCode/MCode for script text and route tables; Claude
Code for the trigger audit — the spec's Phase-0 pattern of parallel
audit seats applies), assembles the pack, files it as the script book's
v0. **Tier L authors the pack; no citizen improvises it in-world, and no
citizen is ever launched unscripted to "see what happens"** — TOWN-0's
citizens are scripted before first dawn by charter, not by preference.

**Inputs:** town charter §2.1 (Tier R: filed scripts, trigger-surface
legality — a reflex fires only on citizen-local state), §1.2/§1.3
(geography and day rhythm); the league's proven body stack and its
standing orders (surveyed ground only, mark-then-move, eat/shelter floor,
quoted-calls-only); the spec's playbook format.

**Contents of v0 (the minimum that makes TOWN-0's muster and first day
honest):**
- **Muster routes** — home→square and square→home for all eight citizens,
  as route tables over the surveyed street network, each route a filed
  sequence with its survey receipt reference.
- **Greeting set** — the muster discipline: who greets whom at the
  square, the confirmation formulae, the notice-board read (the keeper's
  script carries the board; everyone else's carries listening).
- **Work-round stubs** — one stub per trade (harbour circuit, store open/
  close + shelf count, worksite stage-attend, carter's circuit), each
  stub deliberately *shallow*: v0 stubs exist so the first day-parts have
  filed behaviour with declared trigger surfaces and declared failure
  behaviour (mark, hold, file), not so the town is finished. Depth is the
  crafting shift's ongoing work (§2.3 of the town charter), and the stubs
  say so in their headers.
- **Standing orders** — the shelter/hold behaviour under HOLD-LOST, the
  wedge response (stop, file, never grind — §6), the eat/shelter floor
  inherited from the league's orders as form (the town's non-lethal
  regime makes the floor a rhythm rule, not a survival rule).
- **The seeded ToM beliefs** (town charter §4.1) filed alongside the pack
  as beliefs with status `seeded` — *the shopkeeper is at the store in
  work parts; the carter passes the square every circuit* — filed in
  `~/npc-town/tom/`, **not** baked into scripts as silent assumptions.

**Trigger audit (parallel, before the pack is called v0):** one seat
audits every trigger in the pack against the legality rule (citizen-local
state only — position on a surveyed route, own inventory, the chest in
front of me, the day-part bell); violations are listed in the pack's
process note, not fixed silently (the spec's Phase-0 audit pattern).

**Acceptance evidence:** the pack on disk at `~/npc-town/scripts/` with
the audit appended; every muster route referencing a surveyed-route
filing from WP-A (a route without a survey reference is a draft line and
blocks WP-F for that citizen); per-script trigger surfaces stated in the
file headers, greppable.

**Dependencies:** drafting **starts now** against the district *spec*
(route tables as templates parameterised by surveyed coordinates,
greetings and standing orders in full — none of that waits for terrain).
Finalisation — binding route tables to the accepted district's surveyed
routes — gates on WP-A.

### WP-F — Muster proof (the TOWN-0 acceptance run)

**Owner:** execution run by the manager seat's assembled drivers under
Muse's observation; **the verdict is Muse's**, from the stores below.

**Inputs:** WP-A accepted district installed (WP-B), WP-C cast manifest
verified, WP-D gate record green, WP-E pack finalised; the town charter
§5 TOWN-0 lines as the checklist — this run *is* the milestone claim's
last unproven line, and it re-verifies the others in passing.

**The run:**
1. **Pre-window re-verification (same hour):** all eight `.dat`s present
   in the LIVE town directory, hashes matching the manifest; governor
   gate still green (config re-grep, spot probe on two identities);
   running server's regime re-read live; hold harness armed.
2. **Dawn muster:** all eight citizens walk home→square on WP-E's filed
   routes, assemble at the square, the keeper performs the notice-board
   read (scripted), greetings fire per the pack.
3. **Return:** all eight walk square→home.
4. **Hold audit during the run:** every refresh in the window
   landing-verified; any HOLD-LOST suspends the run (§6) — a muster
   completed across a lost hold is not a muster proof, it is an incident
   with good luck.

**Acceptance evidence (world evidence only):** the server-side movement
record for all sixteen legs — **forcedMove count zero across the run**,
positions closing at the square and at homes (displacement is truth; a
citizen's or a driver's self-report of arrival counts for nothing); the
hold audit lines; the run filing at `~/npc-town/manifest/town-0-claim.md`
assembling every §0.1 line with its store pointer. **Muse verifies the
claim file line by line against the stores before TOWN-0 is called** —
artefact, ledger, tail.

**Dependencies:** WP-A…WP-E accepted. This is the only package that
cannot start early in any form — and by design it should be short: every
hard question it asks was already answered by the package that owned it.

---

## 4. Sequencing against reality — what starts now, what gates

Sitka-gen is **still in flight**. The programme does not wait for it, and
does not pretend it has landed. The split:

| Package | Starts now | Gates on district acceptance (WP-A) |
|---|---|---|
| WP-0 Claim/bookings/tree | ✅ in full | — |
| WP-D Governor write | ✅ in full (gate record completable now) | — |
| WP-B Town server | ✅ skeleton, regime, hold proof on a scratch flat test world | District install only |
| WP-C Cast | ✅ names, pairing, assignment drafts, join-procedure filing | The joins themselves |
| WP-E Reflex Pack v0 | ✅ greetings, standing orders, stubs, route-table templates, ToM seeds | Binding routes to surveyed coordinates |
| WP-A District acceptance | ❌ (instruments proven, re-pointed on delivery) | **Is** the gate |
| WP-F Muster proof | ❌ | Everything |

Two sequencing rules, stated plainly:

1. **No package may quietly assume the district exists.** Any artefact
   produced before WP-A that mentions district geography carries the
   label DRAFT-AGAINST-SPEC until WP-A's acceptance record replaces its
   coordinates with surveyed ones. A draft found unlabelled in a filing
   is a defect in that filing, fixed by annotation, never by silence.
2. **The critical path runs through WP-A, and the programme's slack is
   honest about it.** WP-D, WP-B's proof and WP-E's drafting consume the
   wait productively, so that when the district lands, acceptance is the
   only long pole: census + landmark check + walk proof, then install,
   joins, finalised routes, muster. If Sitka-gen slips badly, the
   fallback is §0 decision 4's: the substrate evidence stands, TOWN-0
   waits, and the slip is reported as a slip — not papered over with a
   substitute board or a quieter milestone.

---

## 5. The manager-seat execution shape

### 5.1 The hand-off chain (the proven stand-up, repeated exactly)

1. Muse files this charter on the shelf (done — you are reading it) and
   writes the manager's TOWN-0 charter — the seat-facing brief, on the
   pattern of `manager-charter-proart-20261108.md` — naming the packages
   the manager owns (WP-B, WP-C, WP-D, WP-E), their acceptance evidence,
   and §5.2's prohibitions.
2. The manager charter reaches the ProArt by the proven route: **scp via
   Thor staging** to `~/fleet-manager/` on eileen, **byte count verified
   on the far side**, and the brief's **full text embedded in the launch
   prompt** — the fleet's standing lesson (a lane launched on a 0-byte or
   unread brief parks politely and builds nothing) is not re-learned on
   this programme.
3. The manager runs headless in its tmux session, decomposes each package
   into seat briefs (each brief likewise filed + byte-counted + embedded
   for its executor), commissions **ZCode and MCode in parallel** where
   packages allow (WP-D's edit and WP-E's drafting have no shared seam;
   WP-B's config work and WP-C's filings share the server directory and
   run in sequence — the parallel-lane discipline: shared state gets one
   owner at a time, claimed in the manager's LOG before the lanes run).
4. Receipts flow back up: the manager assembles package artefacts and
   keeps `~/fleet-manager/LOG.md` current (every commission, byte counts,
   failures named plainly); Muse verifies at §5.3's points.

### 5.2 What the manager may NOT do

- **Grade its own lanes.** The manager assembles and reports claims as
  claims; acceptance is Muse's, against world evidence. (The stand-up's
  one self-reported failure was exactly a grading-adjacent gap, and its
  honesty about it is the pattern expected.)
- **Touch the live league world.** Not the Orin server, not Cody/Vega/
  Geist's saves or directory, not the league's citizens in any form (town
  charter §0 decision 3). The town's server, the town's cast, the town's
  stores — nothing else with a body in it.
- **Write the governor config outside WP-D's claimed window**, restart
  the governor outside WP-D's scheduled timing, or treat a probe receipt
  it generated as verified — verification re-reads the ledger from a
  reader who didn't write it.
- **Accept the district** (WP-A is Muse's), **claim the milestone**
  (WP-F's verdict is Muse's), or soften a send-back into a pass.
- **Exceed the ProArt hold discipline:** the box is Casey's (and
  Magnus's); the manager's load stays modest and stoppable, and it yields
  instantly when the box is wanted. Nothing persistent is installed on
  the ProArt for this programme.

### 5.3 Muse's verification points

Fixed, in programme order — each is a first-hand read, not a report:

1. WP-D: config diff vs backup (fourteen in, league byte-unchanged);
   fourteen probe receipts located in the ledger.
2. WP-B: `players/data` listing at construction; running-server regime
   readback; two landed-refresh log lines.
3. WP-A: the census, landmark and walk-proof record (Muse runs or
   re-derives these directly — WP-A *is* a verification point).
4. WP-C: manifest hashes recomputed from the LIVE directory.
5. WP-E: the trigger audit's violations list present in the pack; every
   muster route carrying a survey reference.
6. WP-F: the claim file checked line by line against its stores, tail
   included, before the milestone is spoken.

---

## 6. TOWN-0 failure table and stop conditions

The town charter's §7 table maps the programme's standing risks; this
table is TOWN-0's own — the failures this build can actually meet, each
with its stop. **The governing stop principle, adapted from the league's
three-death circuit-breaker:** town citizens are non-lethal by design, so
the town's breaker trips on *grinding*, not dying — **a citizen who
wedges, pins, or loops stops and files; it never retries its way out.**
PROPOSAL thresholds, filed here so the run doesn't negotiate them
mid-incident: a route leg that fails twice consecutively, a forcedMove
count above zero on a muster leg, or 60 seconds without displacement
while under way — any one stops that citizen's driver, holds the citizen
in place (or at the last surveyed point it reached), and files the
incident with `fault_owner` before any human or shift decides what
happens next. One citizen stopped does not stop the town; the muster
proof (WP-F) requires all eight, so a stopped citizen suspends WP-F
until its incident is resolved and its leg re-walked clean.

| # | Failure | Detection (store) | Stop / response |
|---|---|---|---|
| 1 | District census in the veto band on a town round | WP-A census (mcprobe store) | SEND-BACK with census attached; WP-B install, WP-C joins and WP-F all blocked; `fault_owner: world` (or `harness` if the generator, not the terrain, missed the terracing spec) |
| 2 | Landmark misplaced (cathedral block / Castle Hill outside tolerance) | WP-A landmark check vs OSM/charts + twin corpus | SEND-BACK (same channel as #1); a town built around a wrong map fails the twin loop before it starts |
| 3 | Walk-proof pin on a census-green route | WP-A walk proof (server-side record) | SEND-BACK with pin coordinates; the census's band claim is re-examined for that corridor (canopy-masked headline → floor metric governs) |
| 4 | Any cast identity on the silent governor default | WP-D gate (config grep + ledger receipts) | **All launches blocked** — WP-C joins may proceed (identity ≠ budget), WP-F may not; `fault_owner: harness`; no debugging citizens for a config absence |
| 5 | `.dat` anomaly at a join (wrong name, hash drift, unexpected pool file) | WP-C procedure (LIVE directory) | **Join procedure stops immediately**; no further joins, no deletion of the anomaly; Muse diagnoses from the directory before anything resumes — the sample-clone's signature is handled as a substrate emergency |
| 6 | HOLD-LOST during any operating window | Hold harness (server log: two consecutive unlanded refreshes) | Citizens park per standing orders; the window is void for milestone purposes; TOWN-0 lines depending on it re-run, never annotated (town charter §5's TOWN-1 rule, applied at TOWN-0) |
| 7 | Regime differs from files (difficulty/spawn rules not as configured) | WP-B live readback from the running server | Server not accepted; the regime is fixed and re-read live; no cast joins onto an unverified regime |
| 8 | Citizen wedge/grind in any run | Driver displacement record (server-side) | The breaker above: stop, hold, file with `fault_owner`; never a relaunch loop, never a nudge-and-hope |
| 9 | Reflex pack incomplete at first dawn (a citizen without filed scripts) | WP-E acceptance grep (pack coverage per citizen) | That citizen does not launch; WP-F suspends (muster is all eight); Tier L finishes the pack on the ground, not in the world |
| 10 | Manager or seat grades its own work into a filing | Muse's verification points (§5.3) | The filing is returned unaccepted; the claim is re-derived from the store; the LOG records the return — the production shape's trust depends on this being routine, not dramatic |
| 11 | ProArt box wanted mid-commission | The box's owner, at the desk | Manager yields instantly; commissions resume from the LOG's receipt trail when the box is free; no TOWN-0 deadline argues with the hold discipline |
| 12 | Sitka-gen slips past the programme's patience | WP-A's empty input tray | §4 rule 2: substrate evidence stands, the milestone waits, the slip is reported as a slip. TOWN-0 is never redefined downward to fit a calendar |

**Global stop conditions (any one halts all TOWN-0 execution until Muse
clears it):** a `.dat` anomaly (#5); discovery that any operating window
ran across a lost hold (#6, retroactively); any town lane found writing
outside the town's stores or touching the live league world (§5.2); a
governor config diff showing a *league* identity changed (WP-D's write
was supposed to be additive — a changed league line means the write went
wrong in a way that outranks the town).

---

## 7. What TOWN-0 hands forward

On acceptance, `~/npc-town/manifest/town-0-claim.md` is the programme's
single page of truth: the district acceptance record, the cast manifest,
the governor gate record, the hold proof, the muster record — each line
pointing at its store. TOWN-1 (one full town day, receipted; the
expensive-phase baseline *measured*) then needs no new substrate: its
charter is the town charter's §5 lines executed against stores this plan
built. The paintball game remains behind its arrival gate (verified
TOWN-1) exactly as the town charter §6 left it — written up, ready, and
not this plan's business beyond keeping its inheritance intact: a board
with a status quo, surveyed and lived-in, waiting to be disrupted.

## 8. Claims register (load-bearing only)

| # | Claim | Source |
|---|---|---|
| 1 | TOWN-0's six criteria, world-evidence only | Town charter §5 |
| 2 | Fourteen governor identities with the table's budgets/upstreams; the silent 120/120 default blocks | Town charter §2.4; spec §1.4 |
| 3 | Governor write discipline: backup, one edit, league identities byte-unchanged, restart before operations | OPERATIONS §5 via spec §1.4 |
| 4 | Scratch construction: empty `players/data`, join one at a time, sha256 in the manifest, presence re-verified in LIVE | Spec §1.1; league Rule v2 |
| 5 | Walked band 5.4–9.5 / veto band 24.8–29.4 step faces per 100 columns; the floor-metric companion where canopy masks | League surface census; route-relief survey; triple-020 |
| 6 | The board: town core 2.4 × 2.0 km at 1:1, sea level y 63; cathedral block + Castle Hill inside the playable crop; landmarks checkable against OSM/charts + the 1,492-frame street corpus | Study §5.1–5.2; twin study corpus inventory |
| 7 | Decode planning figure ~120–130 tok/s single-stream on `:8311`; the 7.9–8.4 figure retired from serving arithmetic | Decode-rate settlement (20 metered probes) |
| 8 | Hold law: landing-verified refreshes, two misses = HOLD-LOST park, unheld until proven, gamerules read from the running server | Town charter §1.3; Watcher's Charter; the NORMAL-difficulty divergence |
| 9 | The manager-seat chain: scp + byte count + brief embedded in the launch prompt; the manager assembles and never grades | Manager charter (ProArt stand-up, 2026-11-08, byte-verified end-to-end) |
| 10 | Cast names, breaker thresholds, landmark tolerance (±3 blocks), town workdir paths | **PROPOSALS in this charter (§0), labelled in-line; the trades, counts and criteria they dress are the town charter's** |

*End of build charter. Filed on the studies shelf; home room:
the-league-and-civilization. Parent: `npc-town-charter-20261108.md`.
Siblings: `syndicate-of-four-spec-20261108.md` (the construction pattern),
`syndicate-protocol-design-20261108.md` §5 (the district spec),
`manager-charter-proart-20261108.md` (the seat chain). Next step on
acceptance of this plan: Muse writes the manager's TOWN-0 charter and
the WP-0 claim is filed — WP-D and WP-B start the same day.*
