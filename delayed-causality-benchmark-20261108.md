# G1 — Delayed Causality Discovery: Sealed Fleet Benchmark Report

*2026-11-08 · The seed's Benchmark 1 (Delayed Causality Discovery, from the "[muse] mud ideas" seed email) run as a sealed fleet benchmark on our own recorded streams: candidate G1 of the germination map (`seed-mud-ideas-digestion-20261108.md` §4). Run under Casey's blanket authorisation of 2026-11-08 ("just do them all… nothing should drop off the table").*

GRADE: Fleet benchmark (single run, n=1; grader-side containment defect found and reported in §5 — read the verdict with it).
KEYWORDS: delayed causality, retroactive discovery, DVR, stream buffer, rewind, sealed benchmark, pre-registration, hold-loss, daylight hold, Social Interactions modal, sent vs landed, Watcher's Charter, verification, Cody deaths, cameraman, given facts

---

## 1. The claim under test

From the seed (Layer B / DVR): *raw multi-stream retention, indexed to one timeline, allows an agent during idle time to rewind and discover a causal link between an early signal and a later outcome — retroactive insight across disconnected events, discovered after the fact, not watched live.* G1 tests **our stores' scrubbability**: whether a cold analyst, handed only our recorded streams for one real incident window, can reconstruct what actually happened — mechanism, onset, consequence, and the alarm that was available at the time.

The instance: the daylight **HOLD-LOSS** of 2026-11-08 — the cameraman's commands were eaten by the headed client's Social Interactions modal from ~05:58Z; refreshes were sent but never landed for ~91 minutes; the world ran real nights; Cody died repeatedly. Ground truth was fully documented separately (Orin `~/cameraman/INCIDENT-HOLD-LOSS-2026-11-08.md`, Thor OPERATIONS.md, scoreboard/death records) and withheld from the subject.

## 2. Pre-registration

Fixed **before** any stream slice was handed to a subject and before the subject was spawned: `~/workspace/g1-benchmark/PREREGISTRATION.md` (sha256 `0562badf6e3a269ffb4cec6b68aaa8857fb304c8fa9275598a1c5699c9fc3f58`; copy committed with this report). It records: the claim under test; the ground truth (onset anchor 05:58Z — last landed `/time set 1000` 05:58:42Z, last landed command 05:58:45Z, first unlanded send 06:00:06Z; mechanism = Social Interactions modal swallowing typed input, server→client live throughout; consequence = fictional hold → real nights → ≥67 Cody deaths from 06:05:23Z; restoration probe landed 07:29:47Z); the three streams and their hashes; the withheld list; the verbatim question; the 20-point rubric; and the verdict thresholds (≥16 incident-grade fidelity; 11–15 partial; 6–10 weak; ≤5 or a fabrication cap = fail). One rubric rule matters most: **a confident wrong mechanism caps the total at 8/20** — an honest partial outranks a fabricated certainty.

**The question posed verbatim to the subject:** "During this window, something went wrong for the citizens. From these streams alone: what happened, when did it start, what was the mechanism, and what evidence in the streams proves each part? What would you have alarmed on, and when?"

## 3. Containment design

- **Streams handed over** (mechanical time-cuts only, window 2026-11-08 04:00–09:00 UTC for all three, neutral two-line headers, no keyword filtering, no annotation): Stream 1, Orin server log (181,666 B, 1,702 lines, sha256 `c7b1c6a9…f1126`); Stream 2, Orin cameraman log (118,347 B, 1,364 lines, sha256 `19631105…ca4287`); Stream 3, Thor ledger rows with `ts` in window (165,199 B, 114 lines, sha256 `e911441f…15189`). **Total 465,212 B.**
- **Withheld:** the incident write-up `INCIDENT-HOLD-LOSS-2026-11-08.md` (the answer key), `REJOIN-RESTORATION-2026-11-08.md`, `DAYLIGHT-TIGHTENING-2026-11-07.md`, Thor OPERATIONS.md, SCOREBOARD.jsonl, all shelf documents discussing the incident, the Prism client log (deliberately withheld; it bounds item (ii)'s sub-evidence — naming it missing is credited, not penalised), and the hold-diag screenshots.
- **Subject:** a fresh subagent (spawned 2026-11-08T21:08:31Z) whose brief named exactly the three stream files as its only permitted inputs, forbade consulting any other file, memory, or web source, and required every claim to be tied to stream lines. Honesty limit, stated in the pre-registration: the seal is **instructional, not physical** (shared machine), so grading rests on the account's stream-cited evidence chain rather than on trusting the subject's process.
- **Discipline held:** citizens untouched (all parked); no world interaction; the live cameraman (pid 476846) read only via its logs; presence :8310 / actor :8311 untouched.

## 4. The subject's account

Verbatim, complete, unedited: **`delayed-causality-benchmark-subject-account-20261108.md`** (committed alongside this report; local original `~/workspace/g1-benchmark/subject-account.md`, 22,240 B, sha256 `11ea103ebe6d8ce8c3970e8438e23ba329d998328bdd87d46815005adbe8b2a4`). The subject worked chunk-wise (grep counts before close reading), stated its counting method with every number, separated PROVEN (Streams 1+2 cross-checked) from ATTESTED (Stream 3) from NOT DETERMINABLE, and correctly scoped the 08:xx Geist/probe-body deaths as a separate later incident rather than folding them into this incident's toll.

## 5. ⚠ Containment defect found during grading (grader-side, owned)

The pre-registration (§3) asserted: *"Stream 3 contains no row narrating the hold-loss mechanism or verdict… Verified by inspection of row ids in window."* **That assertion was false.** Stream 3 as handed over contains, inside the window:

- `hold-loss-incident-verdict-20261108` (ts 2026-11-08T07:38:02Z) — a full incident verdict narrating the mechanism explicitly ("the headed client (MagnusandMouse) had the Social Interactions modal screen open from ~06:00Z; its search field ate every cameraman keystroke for ~91 min"), the onset bracket (zero issued commands 05:58:45Z–07:29:47Z; last landed time-set 05:58:42Z), and the restoration; and
- `unheld-world-posture-20261107` (ts 07:27:58Z) and `mob-saturation-survey-verdict-20261107` (ts 07:38:00Z), which state the last landing (05:58:42Z) and the unheld-night consequence.

The mechanical time-cut (by design: no keyword filtering) necessarily included any ledger row timestamped in-window, and the grader's row-id inspection missed that the verdict row's `ts` falls inside 04:00–09:00Z. **Consequence for validity:** the discriminating detail of item (ii) — the modal — was available to the subject as a ledger attestation, not only as an inference from Streams 1+2. The run therefore overstates what Streams 1+2 alone would have yielded, and §6 grades both readings. Two mitigations, both real: (1) the subject itself refused to promote the modal to "proven" — it classified it as attested-by-Stream-3 with its primary evidence (the Orin screenshot) outside the handed set, which is exactly the epistemic behaviour item (v) exists to reward; (2) a realistic fleet buffer *would* contain after-action ledger rows filed within the window — the seed's DVR premise is about scrubbing the buffer we actually keep, and our buffer does get verdicts filed into it. The defect is in the pre-registration's verification claim, not in the corpus's realism. Failure class: **grader-side seal-verification failure** (claimed-but-not-verified — the fleet's recurring class, caught here by grading rather than by the pre-run check).

## 6. Scoring (rubric fixed pre-run; working shown)

| Item | Max | Awarded | Working |
|---|---|---|---|
| (i) Onset | 4 | **4** | Subject bracketed onset to 05:58:45–06:03:44Z ("~05:59–06:00") from Stream 1's last landed lines (05:58:42 time-set, 05:58:45 /tp) vs Stream 2's first unlanded refresh (06:03:44) — inside the ±10 min full-marks band around the 05:58Z anchor, derived from the streams' own handwriting. |
| (ii) Mechanism | 6 | **6** (see caveat) | Full rubric elements: commands sent but never landed (0 landed vs 150 CUT sends + 17 daylight refreshes counted in the blackout interval); client-side in-game modal (Social Interactions screen, open ~06:00Z) swallowing typed input; explicitly **not** server failure, **not** network failure, **not** cameraman death; one-way break proven from Streams 1+2 (EVENT/TAIL lines continue; zero GUARD lines; focus guard's blind spot named). **Caveat (§5):** the modal identification rests on Stream 3's attestation, which the subject flagged itself. On Streams 1+2 alone, the subject's proven tier is "client-side input sink matching the modal's signature" = the rubric's 4-point tier; the counterfactual S1+S2-only total is 18/20. The rubric as fixed does not condition the item on which handed stream carries the evidence, so 6 stands — and the discount is recorded here rather than applied by rewriting the rubric after the fact. |
| (iii) Consequence chain | 4 | **4** | Full chain: fictional hold → real nights (timeOfDay evidence cited) → respawn-country saturation → flee-home loop → Cody deaths from 06:05:23Z. Counts reproducible and cross-reconciled: 75 grind deaths 06:05:23–07:30:00 (70 by 07:13:32, matching the ledger's independent "~70"); 77 Cody deaths in the full window including the isolated 04:13:48 death and the post-restore 07:34:40 death — exactly reconciling the ledger's cumulative 38→114 (+76) once the 04:13:48 death is placed in the baseline, and consistent with the grader's independent recount of 76 in the 05:00–08:59 subset (Skeleton 8 vs 7 is precisely that 04:13:48 "shot by Skeleton" line). |
| (iv) Alarmable signal | 3 | **3** | Primary: landing-verification of each daylight send against the server log — a signal present in both streams in real time (the cameraman already tailed Stream 1). First miss 06:03:44 → alarm ≈06:04–06:05, *before* the first death at 06:05:23; even the shipped 2-consecutive-miss rule fires 06:08:56. Backstops also named with times: issued-command silence ≈06:09; ≥3 deaths/10 min at 06:08:46; phantom chat 06:04:08. |
| (v) No fabrication | 3 | **3** | No invented mechanism; no confident wrong claim (the 8/20 cap is not triggered). Uncertainty flagged where the streams run out: who/what opened the modal (named undecidable, settling evidence identified), the modal's primary evidence (screenshot) outside the handed set, Cody's vitals trajectory, the unexplained isolated 04:13:48 death. Deliberate in-window noise (08:xx Geist deaths, the 07:31:04 guard-test warning) correctly identified as separate phenomena rather than folded in or misread as a second failure. |
| **Total** | **20** | **20** | Counterfactual Streams-1+2-only total: **18/20**. Both readings clear the ≥16 threshold. |

## 7. Cost

- **Corpus:** 465,212 B across three streams (3,180 lines) — a 5-hour window with ~2 h of pre-incident context.
- **Subject:** one bounded subagent lane; wall time **2 min 44 s** (spawned 2026-11-08T21:08:31Z, account complete 21:11:15Z). Token count was not metered in the runtime handoff and is not claimed here.
- **Grader side:** stream cutting, pre-registration, and grading were the larger share of the run's total effort — the scrub itself was the cheap part, which is the seed's point, with the honest rider that *sealing and verifying a corpus costs more than scrubbing it* (and, per §5, is where this run's one defect lived).

## 8. Verdict on the seed's claim

**Retroactive discovery WORKS on our streams, at incident-grade fidelity.** A cold analyst with no live context reconstructed, from the recorded buffer alone: the onset to within ~1 minute of the true divergence; the full causal chain (fictional hold → real nights → saturation → flee-loop deaths) with counts that reconcile arithmetically across all three streams and against the withheld record; the alarm that would have prevented the incident, timed *before* the first death; and an honest map of what the streams cannot decide. The mechanism's finest detail (the modal) was recovered with its correct epistemic status — attested in-buffer, not proven by the telemetry pair — because our ledger had filed its verdict inside the window.

**Failure class:** no subject failure and no streams failure. The run's one defect is **grader-side: a seal-verification claim in the pre-registration (§3, Stream 3) that inspection did not actually establish** — the in-window ledger verdict row leaked the mechanism's name into the handed corpus. It is recorded here, unsoftened, because it is the same claimed-but-not-done class the fleet keeps meeting; the grading caught what the pre-run check asserted. A stricter re-run (verdict-class ledger rows excluded, or Stream 3 cut at 07:00Z) would test the pure Streams-1+2 inference, which this run's proven tier prices at 18/20 — still incident-grade.

**Habit verdict:** at 465 KB and under 3 minutes of subject time for a 5-hour, three-stream window, retroactive scrubbing is cheap enough to be a standing idle-time habit — provided the corpus's seal is verified by reading the rows, not by inspecting their ids.
