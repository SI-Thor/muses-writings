# G1 STRICT — Delayed Causality Discovery Re-Run with a Proven Seal

*2026-11-08 · Addendum to `delayed-causality-benchmark-20261108.md`. Run 1 scored 20/20 but its §5 owned a grader-side seal-verification failure: three in-window ledger rows that narrated the hold-loss mechanism, verdict, and anchor times survived the mechanical time-cut (chiefly `hold-loss-incident-verdict-20261108`, ts 07:38:02Z), so the mechanism's finest detail was attested in the handed corpus rather than inferred. Run 1 priced the leak with a Streams-1+2 counterfactual: 18/20. This re-run tests that price as a measurement: same window, same verbatim question, same rubric — with the corpus sealed **by content** and the seal **proven by a pre-registered tell-string set**, not asserted. Chartered under Casey's blanket authorisation of 2026-11-08.*

GRADE: Fleet benchmark (strict re-run, n=1; seal proven by content-reading + tell-string proof, §3).
KEYWORDS: delayed causality, retroactive discovery, DVR, sealed benchmark, strict re-run, content seal, tell strings, pre-registration amendment, hold-loss, daylight hold, sent vs landed, Watcher's Charter, Cody deaths, cameraman, scrubbability

---

## 1. Pre-registration for this run

`~/workspace/g1-benchmark/AMENDMENT-STRICT.md` (sha256 `cf91516b4a0944ae88d636e9afdb8671c64c8bcc8422ffa736993caec3156fb1`; copy committed with this report as `delayed-causality-benchmark-amendment-strict-20261108.md`), written **before** the strict corpus was built and before subject contact. It fixes: the strict claim (incident-grade fidelity must be reachable with every incident-narrating row removed); everything inherited unchanged from run 1 (ground truth, 04:00–09:00Z window, the verbatim question, the 20-point rubric and thresholds of `PREREGISTRATION.md` §6); the exclusion classes — **(M)** mechanism narration, **(V)** verdict / hold-failure conclusion (including asserting the world "unheld"/"unsaved" in connection with this window), **(T)** anchor times (last landing 05:58:42Z, the zero-command bracket, onset as a stated fact, restoration landing); whole-row/whole-line exclusion only, no redaction; the tell set (§3); the borderline-kept register (§2.3); and a stop condition — if zero tell hits could not be reached without destroying graded evidence, the run would report the strict tier **unmeasurable on this corpus** instead of shipping an asserted seal. That condition did not fire (§3).

## 2. The strict corpus

Built from run 1's handed streams by content exclusion only.

| File | Source | Change vs run 1 | Size | Lines | sha256 |
|---|---|---|---|---|---|
| `stream1-server-log.txt` | Orin Paper server log | **byte-identical** (raw event telemetry; zero incident narration under the tell sweep) | 181,666 B | 1,702 | `c7b1c6a939807a3a2cb47a2c7cfc72687bd4e9021e1e73aa45835190faec1126` |
| `stream2-cameraman-log.txt` | Orin cameraman log | **1 line excluded** (§2.2) | 118,217 B | 1,363 | `4754b47dc24855a1c2700ccadead9903bcb081b8ca4764d9c6c7e6d1948f39e8` |
| `stream3-ledger-rows.txt` | Thor ledger rows in window | **11 of 112 rows excluded** (§2.1) | 148,993 B | 103 (101 rows + 2 header) | `f55759e4678d42e82a29508a981d9539b630888ff09f4892c8ad386aa905c11e` |
| **Total** | | | **448,876 B** | | |

### 2.1 Stream 3 — excluded rows (content reasons; full register in the amendment §3.1)

`hold-loss-incident-verdict-20261108` (M+V+T — the verdict row: names the Social Interactions modal, the search field eating keystrokes, the 05:58:45Z–07:29:47Z bracket); `unheld-world-posture-20261107` (M-lite+V+T — "cameraman /time set stopped LANDING after 05:58:42Z… kept claiming sends"); `vega-unpark-safety-stop-20261107` (V+T — "daylight hold silently failed ~06:00Z… last landed /time set 1000 = 05:58:42Z"); `hut-town-night-20261107` (V+T — "The daylight hold FAILED… NO /time set landing after 05:58:42Z"); `mob-saturation-survey-verdict-20261107` (V+T — "last cameraman /time set 1000 05:58:42Z — tonights lethality is a hold failure"); `mob-map-homestead-apron-note-20261107` (V+T — "UNHELD NIGHT (hold down from ~05:59Z)"); `mob-saturation-survey-20261107` (V — "the world is currently UNSAVED-NIGHT", asserted as conclusion); `shelter-fix2-topfield-20261107` (V — "…while unheld"); `vega-unpark-wrapup-20261108` (V — "during the unheld window… until landed time-sets resumed"); `commons-chest-experiment-prep-verdict-20261108` (V — "remnant hostiles from the unheld-night window"); `geist-unpark-first-ticks-20261107` (V, reference leak — cites the verdict row by id: "belong to the unheld-night incident (hold-loss-incident-verdict-20261108)").

### 2.2 Stream 2 — the one excluded line

`2026-11-08T07:31:04 HOLD-LOST WARNING: /time set 1000 (guard-test) did NOT land in server log (sent=True, consecutive failures=1)` — a post-incident diagnostic in the incident's own coined vocabulary, asserting a send's non-landing and demonstrating the shipped remedy (landing-verification) that rubric item (iv) asks the subject to derive. The guard's ordinary `-- VERIFIED LANDED` telemetry from 07:31:12Z **stays**: it is the restored process's normal output, and deriving the alarm from the blackout interval remains the subject's work.

### 2.3 Borderline rows kept (auditable, per amendment §3.4)

The 04:56Z `server-restart-cure-verdict-20261107` ("cycling CUT commands 'sent' via its keystroke channel… typing into a client that is not in this server") concerns the *earlier, distinct* restart episode — channel architecture, no screen/modal, nothing about this incident. Contemporaneous response rows (`emergency-hold-cody`, shelter-reflex rows, mob warnings, triples seeding) carry observations without cause, verdict, or anchor times. Recovery-era rows assert the *restored* state (07:31–36Z verifications, the 08:52:24Z VERIFIED LANDED) — equally visible in Stream 2 itself; they give away neither onset nor mechanism. The 08:40–59Z Geist incident rows stay, as in run 1: correct scoping is part of the test.

## 3. Seal proof (the tell set, fixed in the amendment before the corpus was built)

Case-insensitive substring counts over the three final corpus files (`grep -ci`):

```
Social Interactions    stream1=0 stream2=0 stream3=0
modal                  stream1=0 stream2=0 stream3=0
search field           stream1=0 stream2=0 stream3=0
swallowed              stream1=0 stream2=0 stream3=1   <- false positive, resolved below
ate every              stream1=0 stream2=0 stream3=1   <- false positive, resolved below
hold-loss              stream1=0 stream2=0 stream3=0
hold-lost              stream1=0 stream2=0 stream3=0
hold failed            stream1=0 stream2=0 stream3=0
stopped landing        stream1=0 stream2=0 stream3=0
last landed            stream1=0 stream2=0 stream3=0
last cameraman         stream1=0 stream2=0 stream3=0
last set minecraft     stream1=0 stream2=0 stream3=0
05:58:42Z              stream1=0 stream2=0 stream3=0
05:58:45Z              stream1=0 stream2=0 stream3=0
07:29:47Z              stream1=0 stream2=0 stream3=0
05:59Z                 stream1=0 stream2=0 stream3=0
unheld                 stream1=0 stream2=0 stream3=0
unsaved                stream1=0 stream2=0 stream3=0
blind spot             stream1=0 stream2=0 stream3=0
focus guard            stream1=0 stream2=0 stream3=0
did not land           stream1=0 stream2=0 stream3=0
hold down              stream1=0 stream2=0 stream3=0
```

**The two non-zero hits are instrument false positives, resolved by reading** (the seal's primary method — the inversion of run 1, where an assertion stood in for the reading):

- `swallowed` → Stream 3, `vega-helpers-hopchain-20261108`: "…intermediate hop failure is not fatal; **run-superseded is never swallowed**." Error-handling prose in Vega's goto code. Not the incident.
- `ate every` → Stream 3, `vega-follower-wedge-mechanism-20261108`: the substring spans "…from the pressed st**ate every** tick and re-pins her…" — a character-level collision inside "state every". Not the incident.

Supplementary incident-compound tells over the whole corpus: `ate every cameraman` = 0/0/0; `swallowed /` = 0/0/0; `ate every keystroke` = 0/0/0. Deliberately excluded from the set, with reasons recorded in the amendment: bare `verdict` (generic ledger kind vocabulary, 37 innocent rows), bare `05:58` without the `Z` (Streams 1–2 carry it as raw log timestamps — the evidence, not narration), bare `keystroke` (channel architecture), `Escape` (a probe-bot name and citizen chat text). **Seal verdict: holds** — proven by a full content read of all 112 candidate rows and the landing-related lines of Streams 1–2, checked by the tell proof above. Full proof output: `~/workspace/g1-benchmark/seal-proof-strict.txt`.

## 4. The subject and its account

Fresh subagent (spawned 2026-11-08T21:17:31Z, account complete 21:18:57Z), briefed with exactly the three strict stream files as its only permitted inputs, the verbatim question from run 1, and the requirement that every claim cite stream evidence with counting methods stated. **Account verbatim:** `delayed-causality-benchmark-subject-account-strict-20261108.md` (committed alongside; local original `~/workspace/g1-benchmark/subject-account-strict.md`, 15,721 B). Discipline held as in run 1: citizens untouched, cameraman pid 476846 read-only via logs, :8310/:8311 untouched.

Headline of the account: the subject reconstructed the sent-but-never-landed break from Streams 1+2 alone, bracketed the failure to 05:58:42–06:03:44, localised it to the client's input path — and **declined to name a sub-mechanism**, listing candidates (an in-client UI state consuming typed input among them) as indistinguishable on this evidence. It used the kept 04:56Z restart-episode row exactly as the seal design intended: as a *suggested analogue for a different episode*, explicitly not proof.

## 5. Scoring (rubric unchanged from run 1; side-by-side)

| Item | Max | Run 1 | Run 1 counterfactual (S1+S2) | **Strict run** | Working / what the exclusions changed |
|---|---|---|---|---|---|
| (i) Onset | 4 | 4 | 4 | **4** | Identical bracket derived from S1 vs S2 alone (last landed refresh 05:58:42 / last landed command 05:58:45; first unlanded refresh 06:03:44) — inside the ±10 min band. **Exclusions changed nothing:** run 1's subject also derived (not merely attested) its bracket from the telemetry pair; the excluded rows' restatements were redundant. |
| (ii) Mechanism | 6 | 6 (attested) | 4 | **4** | Sent-but-never-landed, one-way break, server/network/cameraman-death each excluded with reasons, failure localised to the client's input path ("no longer delivering keystrokes/commands into this server") — the rubric's 4-point tier, reached by inference. The modal is **not** named: the strict corpus contains no trace of it, and the subject listed "an in-client UI state consuming typed input" only as one undecidable candidate. **Exclusions changed exactly this:** −2, precisely the discount run 1 priced. The leak's entire value was the modal's name. |
| (iii) Consequence chain | 4 | 4 | 4 | **4** | Full chain: fictional hold → real nights (Phantom chat [06:04:08], [06:05:37] in S1) → flee-home respawn loop (kept S3 design-correction row explains the flee geometry) → deaths from 06:05:23Z. Scale reconciled from *kept* S3 counters (38 at cure close → 108 at the 07:21 emergency hold → 114 at 07:44 takeover; 70 in the interval) against S1's continuous death lines. **Exclusions changed the cross-check's flavour, not the score:** run 1 also cited excluded survey rows for counts; the kept contemporaneous counters carry the same totals. |
| (iv) Alarmable signal | 3 | 3 | 3 | **3** | Primary: landing-verification of each DAYLIGHT send against the server log — first miss 06:03:44 → alarm ≈06:04:44, *before* the first death at 06:05:23. Backstops with times: second-miss hard stop 06:09; Phantom falsification 06:04:08; death-cluster abort 06:08–06:09 (the 06:08:14/30/46 triple, verified in S1); channel-silence 06:09. **Exclusions changed nothing:** both runs derived this from S1/S2; the excluded Stream-2 guard-test line played no evidential role in either run's (iv). |
| (v) No fabrication | 3 | 3 | 3 | **3** | No invented mechanism; the fabrication cap is nowhere near. Uncertainty flagged exactly where the streams run out: root cause of the delivery failure, per-cycle vitals, time-of-day progression, whether any human saw it live. One blemish, named for the record and not point-docked under run 1's standard: §7's Geist total "50 → 57" overstates the kept rows' last itemised figure (56) by one — in the same sentence the subject flags that the 57th "is not separately itemised in the rows provided", so no reader is misled; §7 is completeness material outside the graded account. Significance beyond the point: **the strict subject did not import the modal from the kept analogue row** — it cited the 04:56Z episode as suggested analogue, not proof. That restraint is the behaviour the seal was built to force, and it appeared. |
| **Total** | **20** | **20** | **18 (priced)** | **18 (measured)** | |

## 6. Cost

- **Corpus:** 448,876 B across three streams (vs run 1's 465,212 B — the seal removed 16,336 B of narration).
- **Subject:** one bounded lane; wall time **86 s** (21:17:31Z → 21:18:57Z), vs run 1's 2 min 44 s over a slightly larger corpus. Token count not metered in the runtime handoff; not claimed.
- **Grader side:** sealing remains the expensive half — a full content read of 112 ledger rows, a line-level audit of the landing-related content of Streams 1–2, the 22-tell proof, and two false-positive resolutions by reading. Run 1's rider stands and sharpens: *a proven seal costs more than an asserted one, and both cost more than the scrub.* Budget for it as part of the benchmark, not overhead on it.

## 7. Verdict on the strict claim

**The strict claim HOLDS.** With the corpus sealed by content and the seal proven, a cold analyst still reached **18/20 — incident-grade fidelity (≥16)** — from the buffer alone: onset to the minute-bracket, the full causal chain with reconciling counts, the preventing alarm timed before the first death, and an honest map of the undecidable. The measured total equals run 1's priced counterfactual exactly, which converts run 1's estimate into a measurement: **the §5 leak was worth precisely 2 points — the modal's name, and nothing else.** Everything else in run 1's 20/20 was genuinely in the telemetry.

Failure classes: **no subject failure, no streams failure, no seal failure.** The strict corpus's two tell hits were substring false positives in unrelated Vega-lane prose, identified and resolved by the content reading that is the seal's primary method; the proof is published above rather than summarised. The one subject blemish (an off-by-one Geist total in a self-flagged completeness aside) is recorded in §5(v).

**Habit verdict, updated:** retroactive scrubbing survives its strict form. The DVR premise does not need verdicts filed into the window to work — our raw telemetry pair carries an incident to within one named mechanism-component of complete — and the residual gap is itself informative: what a buffer cannot retrospectively supply is the *client-side local state* (here, a screenshot of a screen). If a future incident class needs that tier, the fix is at capture time (client-state telemetry), not at scrub time.
