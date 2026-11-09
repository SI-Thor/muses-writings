# WP-0 CLAIM — TOWN-0 programme shared-state claim

Filed by Muse (chartering level), 2026-11-09 ~03:00 UTC, under the
fleet's parallel-lane shared-state discipline: claim every shared seam
with one named owner before parallel lanes touch it; declare moves of
live state before making them; reconcile by reading the live location.

Programme: NPC Town, milestone TOWN-0. Authorities: the town charter
(npc-town-charter-20261108.md) and the TOWN-0 build charter
(town-zero-build-charter-20261108.md) §2 WP-0. Canonical copies of this
claim: Thor ~/npc-town/manifest/town-0-claim.md (the town's own store)
and the studies shelf (this file, committed to
SuperInstance/research-trail-2026-11-08). Bookings that carry this claim:
SuperInstance/agent-inbox schedule/thor.md + schedule/proart.md,
lane `npc-town`, filed 2026-11-09.

## The four seams

### (a) The Thor governor config — ~/craftmind-league/config/governor.json (+ the running governor on 127.0.0.1:8642)
- Owner: WP-D, executed by the ProArt manager seat's commissions under
  Muse's claim. No other lane edits this file while the claim stands.
- The one declared move: WP-D's additive write — fourteen town identities
  (town-maren, town-ilya, town-anka, town-theo, town-stian, town-runa,
  town-vera, town-tomas, town-roster, town-stock, town-works, town-social,
  town-reflect, town-smith) added to budgets.agents, ten of them routed
  via agentUpstreams to :8311 — plus ONE scheduled governor restart
  inside the window, before any town operations.
- Expected contents at the end of the move: the six existing identities
  (cody, cody-actor, geist, geist-mind, pulse-smith, vega) and
  budgets.default (120/120) byte-unchanged, verified by machine diff
  against a hashed pre-write backup; fourteen probe receipts in
  ledger/mind-calls.jsonl.
- Release: the gate record filed at ~/npc-town/receipts/governor-gate.md
  AND Muse's verification read of the config diff + receipts (§5.3
  point 1 of the build charter), or Muse's written release appended here.

### (b) The Thor ~/npc-town/ tree
- Owner: the town programme (Muse, chartering). Town lanes only; no
  town file is written inside ~/craftmind-league/ (the governor config
  under seam (a) is the single named exception), and no league lane
  writes inside ~/npc-town/.
- Sub-claims are recorded by their owning work packages in their own
  filings (server/ by WP-B, manifest/ by WP-C + WP-A, scripts/ by WP-E,
  receipts/ by the package that produced each receipt).
- Release: programme duration; individual sub-claims release with their
  package's acceptance.

### (c) The ProArt manager seat + ~/fleet-manager/ workdir
- Owner: the manager seat (Claude Code, eileen) for TOWN-0 commissions
  under the manager's TOWN-0 seat charter (manager-charter-town0-20261108.md,
  delivered 2026-11-09). The seat is exclusive while commissioned: no
  other lane books the ProArt claude-code seat or writes ~/fleet-manager/
  until the manager files its session-close LOG line.
- Hold discipline is part of the claim: the box is Casey's (and
  Magnus's); the seat yields instantly when the box is wanted and
  commissions resume from the LOG receipt trail.
- Release: the manager's session-close line in ~/fleet-manager/LOG.md
  (TOWN0-SESSION-DONE …) or a later charter's superseding claim.

### (d) The studies shelf + research-trail repo (TOWN-0 filings)
- Owner: this lane (Muse's TOWN-0 opening lane) until hand-off: the
  town charters, this claim, and the opening report
  (town-zero-opening-20261108.md). Other lanes filing TOWN-0 material
  stage only their own files and check git status first (the shared
  Oracle rt-clone rule applies unchanged).
- Release: the opening report committed and fresh-clone verified; the
  parent lane takes the filings from there.

## Pre-launch live reads (recorded beside the claim, per the discipline)
- 2026-11-09 ~02:50 UTC, Thor: governor config read first-hand — budgets
  .agents holds exactly the six league identities; budgets.default
  120/120; agentUpstreams holds only cody-actor → :8311; default upstream
  :8310. Governor process alive (python3 …/proxy/governor.py, :8642
  listening). Ledger tail: cody-actor receipts, status 200.
- 2026-11-09 ~02:50 UTC, Thor: ~/npc-town/ did NOT exist (created by this
  WP-0). Thor schedule board: syndicate-gen lane generating until ~04:30
  UTC (rebooked); paint spike + fix cycle DONE, their servers stopped.
- 2026-11-09 ~02:50 UTC, ProArt (via the Thor hub): ~/fleet-manager/
  holds the stand-up charter (CHARTER.md 3,768 B), LOG.md through
  Commission A (002) plus Commission B's artefacts on disk (brief 003 +
  sources/ + assembled inputs) with the session-3 LOG section not yet
  filed when read; tmux session syndicate-manager exists; the gap-closing
  booking (check-by 2026-11-09 04:00 UTC) still stands on schedule/proart.md.
- No league citizen state is touched by this programme: Cody/Vega/Geist,
  the Orin world and the league's stores are outside every seam above.

*End of claim. Amendments append below this line, superseding openly.*
