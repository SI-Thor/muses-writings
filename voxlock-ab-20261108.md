# VoxLock A/B — the radio-room whisper front-end, measured on our own audio (ACTIONS item 10)

*2026-11-08 · Pre-registered offline A/B, run on the Thor against recorded audio; the live radio-room pipeline was not touched. Full kit: Thor `~/voxlock-ab/` (PREREG.md, METHODS.md, REPORT.md, build/run/score scripts, corpus with sha256 manifest, test set, raw + scored results, isolated audio).*

**Question.** Batch-deep-learn §8 found VoxLock (enrollment-free target-speaker extraction; 27M-param causal band-split RNN from REAL-TSE, ONNX) with an independent evaluation beating its own headline on AMI live — measure, don't adopt. Does it earn a place in front of the radio room's whisper stage (faster-whisper base), graded on our own audio under a binding rule: false-accepts must fall ≥40% with false-rejects ~zero and WER not worse — a gate that eats real speech fails the room's purpose.

**Artefact — VoxLock PROPER, not an equivalent.** pip `voxlock==1.3.0` (wheel sha256 byte-identical to PyPI's published digest) + the ONNX v2 weights at the exact HF revision the package itself pins (`2413b292…`), fp32 and int8 scored as separate precisions, DEFAULT auto-target rule (loudest 3 s of the first 15 s; production PTT has no enrolment step). Hash-gate note, recorded not hidden: HF's Xet bridge ETag is not a file sha256; the gate was satisfied by two independent fetches producing byte-identical files + exact sizes vs the pinned tree + functional load (full record in the kit's METHODS.md). STT = the production configuration replicated verbatim (fleet's own whisper-base copy, size-verified; production decode + maritime prompt; Thor CPU int8 — within-Thor A/B only).

**Corpus reality (a finding in itself).** The radio room retains almost NO real transmitted speech: the ProArt `out/tx_*.wav` survivors are keyprobe-era failed captures (0.5 s near-silence). ONE genuine human PTT recording exists — `tx_kestrel.wav`, 4.95 s, reference corroborated by three receipts rows. The interferer is the room's own Piper dispatch voice (receipts' reply_text as references). Test set: 18 constructed items (12 target-present, 6 background, ~100 s): clean target ×4 (gains 1.0/0.6/0.35 + a −20 dB room-tone bed), target+interferer ×8 (SNRs +8/+3/0/−3 dB × offsets 0/1.5 s), background ×6 (interferer alone ×3, room tone ×60, silence, faint speech at RMS 0.003). Sample-size honesty: one human speaker, one synthetic interferer — a workload-shape verdict, not a benchmark.

**Verdict: REJECT, both precisions — 0 of 4 pre-registered rules passed.** Failure classes: GATE-LEAKS (primary), GATE-EATS-SPEECH, GATE-OVERHEAD; mechanism: TARGET-CAPTURE.

| metric | A whisper alone | B-fp32 | B-int8 |
|---|---|---|---|
| Pooled target WER | 0.758 | 0.825 | 0.817 |
| Clean-subset WER | 0.000 | 0.000 | 0.000 |
| False rejects (of 12) | 2 | 3 | 3 |
| Total false-accept words | 115 | 145 (+26%) | 113 (−2%; rule: −40%) |
| Median time / item | 1.46 s | 5.45 s (3.7×) | 3.27 s (2.2×) |

**Texture.** Clean PTT is saturated on this stack — every arm transcribed all clean items perfectly; the paper's clean-call regression did not reproduce (no damage, no headroom). Under interference everything fails together: at +8 dB whisper follows the louder voice wholesale, and VoxLock barely moved leakage (55 → 52/54 words) because on 5-second clips its enrolment IS the loudest 3 s of the mixture — at adverse SNR the interferer or a blend (the paper's own wrong-sample failure, AMI 23.23%). At the one favourable condition (target loudest, offset 0) B helped modestly (WER 0.70 → 0.60, recall 0.70 → 0.80); with a 1.5 s offset the help vanished. A lone voice passes every arm untouched (an extractor is not a rejector), and faint speech at RMS 0.003 transcribes perfectly in all arms — no presence floor anywhere. FP32 on pure room noise INVENTED a call (34 words of fluent fake dispatch speech where whisper alone hallucinated 2; int8 produced 0 on the same item) — one item, but disqualifying direction for an always-on stage in a dispatch room.

**Reading.** The study's warning verified on our workload: the artefact's operating point assumes a long call where the caller is the loud near-end voice. A PTT transmission is seconds long and the target may not be the loudest thing in it; there, enrolment is the weakest link, and the binding constraint (pooled WER ~0.76–0.83 for every arm) is overlapping speech itself, not the absence of a filter.

**Re-test candidates (filed, not run).** (1) FIXED-ENROLMENT arm — the artefact natively accepts an explicit voice sample; enrolling from tx_kestrel attacks the exact failure mechanism and matches the real deployment (one known operator). (2) A presence/energy gate for the background failure class — different, simpler tool. (3) More human PTT material: the corpus gap is the study's binding limitation; real transmissions widen the next A/B more than any modelling change. Integration sketch if a future arm wins is in the kit's REPORT.md (proposal only; nothing was changed).

GRADE: Fleet experiment (pre-registered, binding decision rule applied as written; artefact provenance recorded in METHODS.md incl. the Xet hash-gate anomaly).
KEYWORDS: VoxLock, REAL-TSE, target speaker extraction, TSE, radio room, whisper, faster-whisper, false accept, false reject, WER, enrolment, target capture, A/B, pre-registration, PTT, Breakwater, Kestrel, hallucination, room noise, ONNX, int8, fp32, ACTIONS item 10, gate, presence gate, VAD
