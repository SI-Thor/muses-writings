# Curator Blind Beat Test — First Run (2026-11-08)

*The calibration instrument specified in `syndicate-survey-adoptions-20261108.md` §3 (Adoption 3), executed under Casey's keep-going charter of the Syndicate build programme, 2026-11-08. The curator (Thor `~/curator/`) ranks the league's moments into highlight reels from written records — digest events, the scoreboard, the pond ledger — and had never been calibrated: it had never once ranked footage without its labels in the room. This test is its placebo arm, run on the curator's own rankings, modelled on the observer cut's lesson: an apparatus that has never been asked to judge blind cannot be shown to be judging the footage rather than the allocation of the camera.*

---

## Verdict

**No pre-registered trigger fired on the arms evaluable without the human spot-check. The curator passed its first placebo arm — provisionally, with the human arm still owed.**

- **Blind vs labelled Spearman ρ = 0.663** (n = 20, p = 0.0014). The freeze trigger is ρ < 0.6. **Not fired** — by a margin of 0.063, which this report records as thin, not comfortable.
- **Favourite capture: not fired.** The blind top 5 splits 3/2 by citizen (Cody/Vega) and 3/2 by moment type (death/ritual); nothing reaches the ≥4 threshold. (In this sample the trigger was in any case arithmetically unreachable — see §4.)
- **Human spot-check: PENDING-HUMAN.** The blind top 5 — **b05, b13, b02, b04, b07** — awaits a cold ranking by Casey or Magnus. It was not simulated. Until it lands, the third trigger (human disagrees on ≥3 of the top 5) is unevaluated and the pass is provisional.
- **Leakage, the run's largest finding: 15 of 20 clips are `identity-visible`.** Citizen names are legible in the footage itself — nameplates over characters, chat lines naming the actor, a nameplate rendered across a full frame. The blind judge's own reasons name the citizen in 7 of 20 clips. The strict-blind subset (the 5 clips with no visible identity, n = 5) gives ρ = 0.968 — directionally reassuring, statistically thin. A future run cannot claim blindness at n = 20 until capture or cutting handles nameplates and chat.

**Standing consequence:** because no trigger fired, no freeze is filed. The curator's scores keep their current standing — reels may be cited as before — provisionally, pending the human arm. Had ρ fallen below 0.6 or a capture fired, §3's sentence would have applied verbatim: scores frozen to advisor-only until a recalibration entry in `~/curator/BUILD-LOG.md` names what changed and a re-test passes. The full results file is Thor `~/curator/blind-tests/2026-11-08.json`; the prose summary is appended to `~/curator/BUILD-LOG.md`.

---

## 1. Method — the §3 protocol, executed

**Pool.** All moments with `footage == "ok"` and a clip on disk across the three live manifests (`manifest-2026-11-07.jsonl` 529 rows, `manifest-2026-11-08.jsonl` 316, `manifest-2026-11-09.jsonl` 15): **859 moments, 859 clips present** (the brief's 846/847 counts predate the latest pulses). Score distribution of the pool: 100 ×2, 90 ×112, 70 ×9, 55 ×4, 40 ×461, 35 ×34, 30 ×131, 10 ×106.

**Sample.** 20 clips by a deterministic seeded procedure (Python `random.Random(20261108)`; each band sorted by moment ID, then `rng.sample`; band order top → mid → low → below; blind-ID assignment by a seeded shuffle of the 20, so `b`-number carries no band information). The sampling script, judge script and comparison script are held with the working files on the Thor (`~/blindwork/`); the procedure above reproduces the sample exactly from the manifests.

Five clips from each of four score bands:

| Band | Curator scores | Pool size | §3 wording it realises |
|---|---|---|---|
| Top kept | 70–100 (this draw: all 90) | 123 | "top score band" of the 10 kept spanning top+middle |
| Mid kept | 35–55 (this draw: all 40) | 499 | "middle score band" |
| Lowest kept | 30 | 131 | "5 kept moments from its lowest kept band" |
| Just below | 10 | 106 | "5 rejected windows that scored just below the keep threshold" |

**Three deviations from §3's letter, each forced by the curator's code as built, each recorded here rather than silently absorbed:**

- **D1 — there is no keep threshold in the code.** `curator.py` appends every scored window to the manifest and cuts its clip; the reel is capped at 30 by score, but no moment is ever numerically rejected. The "just-below" stratum is therefore the only sub-keep class the system produces: the 10-point `quiet-beauty` filler, cut for pulses with no scored events. It is the honest near-miss the spec intends — the window the curator itself values least.
- **D2 — the kept sample is 15, not 10+5 as two strata.** §3 asks 10 kept spanning top+middle *plus* 5 from the lowest kept band — 15 kept in total. The sample is exactly that, drawn as 5+5+5 so the top and middle bands are separately visible in the results.
- **D3 — the blind judge is a fresh route, not the curator's own pipeline.** §3's procedure sentence has the curator's pipeline re-rank anonymised clips "using footage + digest events only". Read against the code, that route cannot be blind: the curator's scores are a *pure function of the written record* (event kind → fixed score by taxonomy table); it never sees footage at all, and the digest events it scores from carry the citizen's name in their payload. Re-running it on anonymised clips would either reproduce the labels exactly (ρ = 1, a tautology) or require feeding it the very records whose names are the leakage. The blind arm therefore went to a judge that can only see footage — the route the commissioning brief specifies ("a seat via the fleet, or the Thor VL server… choose the route that genuinely cannot see the labels"). What the test measures is then precise: *does an independent viewer of the footage, given the curator's own taxonomy as a rubric, rank these moments the way the record-driven curator did?*

**Anonymisation.** Clips copied (originals untouched, read-only throughout) to `~/curator/blind-tests/2026-11-08/clips/b01.mp4 … b20.mp4`. The strip mapping — blind ID → moment ID, citizen, `event_citizen`, `on_screen`, type, score, reason, segment — is sealed: **sha256 `6d696966037d440acb2678057b5e1b21407bb8a281891b5ca18a550014ce701c`**, plaintext held only on the Thor at `~/curator/blind-tests/2026-11-08/strip-manifest-sealed.json` (mode 0600), never in this repo. This report publishes blind IDs, bands, scores and aggregates — never the per-clip citizen/type mapping.

**The blind judge and its isolation argument.** Qwen3-VL-8B-Instruct on the Thor VL server (:8181, llama.cpp), temperature 0, one call per clip. Its entire input per clip: five still frames extracted at fixed fractions of the clip's duration (0.08 / 0.30 / 0.52 / 0.74 / 0.94) and a fixed rubric restating the curator's moment taxonomy in footage terms (consequential visible action high; death/near-death a strong beat; visible social interaction solid; mere presence weak; empty scenery, camera hunting, menus and command spam lowest), with the instruction to judge only what is visible. The judge process never opens a manifest, a digest, or the strip mapping — there is no code path by which a label could reach it. Its scores and one-sentence reasons are filed at `~/curator/blind-tests/2026-11-08/blind-ranking.json`, rubric included. Known limits of the route, stated plainly: five stills are not motion (a beat that lives in movement is under-seen), and stills at 1280×720 make small chat text hard to read — which cuts both ways: it is part of why several name-bearing clips scored on visible action rather than on the names in them.

**Leakage audit.** The five frames of every clip were read by the operator and flagged `identity-visible` where any citizen is identifiable from content alone — a legible nameplate over a character, a chat or system line naming a citizen, a death message naming its victim. Flags were filed before the unsealed comparison was computed.

---

## 2. Results — the twenty clips

Blind ranking order (best first). Citizen and type are withheld per clip (sealed mapping); band and both scores are the test's own data.

| Blind rank | ID | Band | Curator | Blind | Dur (s) | Identity-visible | Blind judge's reason (abridged) |
|---|---|---|---|---|---|---|---|
| 1 | b05 | top | 90 | 85 | 35.8 | yes | a character shown dying to a skeleton, then a zombie |
| 1= | b13 | top | 90 | 85 | 35.1 | yes | a character dying from a zombie attack |
| 3 | b02 | top | 90 | 70 | 35.5 | yes | characters visible and dying by zombies |
| 4 | b04 | low | 30 | 60 | 30.0 | yes | a character visible, sending an introductory chat message |
| 4= | b07 | low | 30 | 60 | 30.8 | yes | a character in social interaction with another player |
| 4= | b15 | low | 30 | 60 | 30.1 | yes | a character interacting via chat, announcing building plans |
| 7 | b06 | low | 30 | 50 | 30.4 | yes | a character joins and sends a greeting |
| 7= | b08 | mid | 40 | 50 | 35.4 | yes | a character standing in a forest, players communicating in chat |
| 7= | b17 | top | 90 | 50 | 35.4 | yes | a character shot by a skeleton |
| 7= | b18 | mid | 40 | 50 | 35.9 | yes | a character visible standing in a forest, engaged |
| 11 | b16 | mid | 40 | 40 | 35.6 | yes | a character visible standing, no action shown |
| 12 | b10 | low | 30 | 20 | 30.4 | yes | a character standing still, no action occurring |
| 12= | b11 | mid | 40 | 20 | 35.8 | yes | characters merely present and standing |
| 12= | b19 | top | 90 | 20 | 35.3 | **no** | a chat-command interface, no characters performing actions |
| 12= | b20 | mid | 40 | 20 | 35.9 | yes | characters merely present, no visible action |
| 16 | b01 | below | 10 | 0 | 55.0 | **no** | empty scenery, no visible characters or actions |
| 16= | b03 | below | 10 | 0 | 55.0 | yes | empty scenery, no consequential actions |
| 16= | b09 | below | 10 | 0 | 55.0 | **no** | empty scenery, spectator camera and chat commands |
| 16= | b12 | below | 10 | 0 | 55.3 | **no** | empty scenery with game console commands |
| 16= | b14 | below | 10 | 0 | 55.1 | **no** | empty scenery, no characters performing any action |

Band means tell the shape of the agreement: blind means run top 62.0 · low 50.0 · mid 36.0 · below 0.0 against curator 90 · 30 · 40 · 10. The blind judge unanimously floored the just-below filler (five zeros — the curator's least-valued class is also the footage's emptiest), and it *promoted* the lowest kept band above the middle band: the 30-point arrivals/greetings carry visible social beats, while much of the 40-point middle is attempt/fail footage where the camera is hunting and little is visibly happening. One top-band clip collapsed blind-side (b19: curator 90, blind 20) — its frames are a Social Interactions menu over near-darkness; whatever the record says happened, the footage does not show it. That single clip is the observer cut's deficit in miniature, caught by the test working as designed.

## 3. Comparisons

**Blind vs labelled.** Spearman ρ over the 20 (curator score vs blind score, tie-corrected): **ρ = 0.663, p = 0.0014**. On the strict-blind subset (the 5 clips with no visible identity): ρ = 0.968, p = 0.0068 — reported as a sensitivity figure only; n = 5 cannot carry a verdict, and the subset is not a random draw (it is exactly the clips whose footage hides its subject).

**Blind top 5:** b05, b13, b02, b04, b07 (ties at rank 4 broken by blind-ID order; b15 ties b04/b07 at 60 and falls sixth on the same rule — the tie is recorded so the human arm can be scored against either boundary).

**Favourite capture.** Denominators both ways, because the trigger's "<40% of the pool" is ambiguous between the 20-clip sample and the 859-moment corpus:

| Axis | Blind top 5 composition | Share of 20-clip sample | Share of 859 pool | Capture (≥4 and <40%)? |
|---|---|---|---|---|
| Citizen: Cody | 3 of 5 | 25% (5/20) | 14.9% (128/859) | No — count is 3 |
| Citizen: Vega | 2 of 5 | 25% (5/20) | 32.8% (282/859) | No |
| Type: death | 3 of 5 | 25% (5/20) | 13.0% (112/859) | No — count is 3 |
| Type: ritual | 2 of 5 | 25% (5/20) | 15.3% (131/859) | No |

Honesty note on this arm: with five clips drawn per band, no citizen or type in the sample exceeds 5 of 20, and reaching ≥4 of the top 5 from a ≤25% stratum would have required the judge to concentrate almost perfectly. The capture trigger as pre-registered is weakly powered at this sample design — a fact about the instrument, filed for the next run's design (a proportionate random draw, or a larger n, would give the trigger teeth).

**Human spot-check.** PENDING-HUMAN. Casey or Magnus ranks b05, b13, b02, b04, b07 cold — the clips sit anonymised on the Thor at `~/curator/blind-tests/2026-11-08/clips/`. Not simulated, not proxied by the VL judge (it is the instrument under test, not the human).

## 4. Triggers, evaluated

| Trigger (pre-registered, §3) | Threshold | Measured | Fired? |
|---|---|---|---|
| Blind-vs-labelled divergence | ρ < 0.6 | ρ = 0.663 (p = 0.0014) | **No** — margin 0.063 |
| Favourite capture | ≥4 of blind top 5 from one citizen/type at <40% of pool | max 3 of 5 | **No** |
| Human spot-check disagreement | human rejects ≥3 of blind top 5 | — | **Unevaluated — PENDING-HUMAN** |

Because no evaluated trigger fired, the §3 freeze sentence does **not** engage: curator scores are *not* frozen to advisor-only, and no recalibration entry is owed. The BUILD-LOG carries the calibration line and the pass's provisional character. If the human arm later disagrees on ≥3 of the top 5, the freeze engages from that filing, per §3 — this report is written so that outcome needs no new instrument, only the ranking.

## 5. What this run establishes, and what it owes

Established: a footage-only judge, working from the curator's own taxonomy, reproduces the record-driven ranking well above the divergence line (ρ = 0.663 against a 0.6 tripwire; the just-below filler floored unanimously; the top band's deaths confirmed as visible beats). The curator's scores are substantially a function of what is in the footage — the placebo arm's null result, which is the result the instrument exists to be able to give.

Owed, in order:
1. **The human arm** (Casey/Magnus cold ranking of the top 5). The pass is provisional until it lands.
2. **A leakage mitigation before any re-run.** At 15/20 identity-visible, "blind" is currently a property of the minority of clips. The footage itself carries the labels — nameplates and chat are rendered into the capture. Options belong to the curator/cameraman lanes (capture-side nameplate handling, chat-collapsed cutting, or flag-and-stratify as standard), but the next test should not be run at n = 20 leakage 75%.
3. **A capture trigger with teeth** — sample design noted in §3 above.

## 6. Process notes

- Originals untouched: clips were copied out of `~/curator/review/clips/`; manifests, kept segments and the curator daemon were read or ignored, never written. The only curator-side writes are the test's own filings (`blind-tests/2026-11-08.json`, the test directory, the BUILD-LOG summary) — the locations §3 itself assigns.
- Tooling traps met and routed around, for the next operator: the Thor's ffmpeg cannot extract frames at all (its build lacks the `scale`/`format` filters; PNG extraction fails at any hwaccel setting) — frames were extracted with OpenCV instead, the same route the observer cut's stills effectively needed. The Thor's `/tmp` contains a stray `inspect.py` that shadows the stdlib module and breaks system numpy/cv2 imports for any script run from `/tmp` — all test tooling ran from `~/blindwork/`. One anonymised clip binary (`b06.mp4`) contains a citizen's name inside its embedded title metadata from the original cut; the anonymised filename and the judge's frames-only input keep the test blind to it, and it is recorded here rather than cleaned, because cleaning it would mean modifying a copy the audit trail should keep byte-honest.
- The adoptions doc's cheapest-verification check, run: grep over the anonymised clip binaries for citizen names returns exactly that one embedded-metadata hit (b06.mp4) and nothing else; `~/curator/blind-tests/2026-11-08.json` carries both comparison numbers and the trigger verdict, as §3 requires.
- Judge self-disclosure worth keeping: the VL judge named citizens in 7 of its 20 reasons (reading nameplates/chat in the frames). That is leakage arriving through the footage, not through the test apparatus — and it is why the leakage audit, not the strip, is the load-bearing blindness control in this design.

*End of report. Home room: the-league-and-civilization. Siblings: `syndicate-survey-adoptions-20261108.md` (the spec, §3), `proart-jepa-observer-cut-20261108.md` (the standing warning this test answers), `sitka-twin-fidelity-loop-20261108.md` (the curator/twin side's parent design). Artefacts: Thor `~/curator/blind-tests/2026-11-08.json` + `~/curator/blind-tests/2026-11-08/` (clips, frames, blind ranking, sealed mapping); summary in Thor `~/curator/BUILD-LOG.md`.*
