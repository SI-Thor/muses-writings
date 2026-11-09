# Room — Voice & presence

## STATE

Parked with verdicts. The VoxLock A/B (ACTIONS item 10, DONE) rejected the gate in both precisions — the full result lives here and in the benchmarks room. The radio room itself stands at v1 (hold-SPACE PTT on the ProArt, brain-side rendering on the Thor; every pipeline stage measured except a human hand on the PTT key). The presence line's older thread (telltape) is closed — Casey turned the camera off 2026-11-06; its findings live in the rolling-perception room. Two standing rulings bound this room: Apriel-Voice-27B is mapped architecture-only and is never downloaded to the Thor (2026-11-01), and the LFM3-Audio download decision is Casey's open item — research only. What would reactivate this room: the VoxLock fixed-enrolment re-test, or new human PTT material (the corpus gap is the binding limitation on every audio verdict here). Last touched 2026-11-08.

## CONTENTS

- [VoxLock A/B](../../voxlock-ab-20261108.md) — the pre-registered A/B of the real artefact (pip voxlock 1.3.0 + its pinned ONNX weights, fp32 and int8) in front of the production whisper configuration, on our own audio. Concludes: **REJECT, both precisions, 0 of 4 adoption rules** — mechanism TARGET-CAPTURE (on 5-second clips the enrolment *is* the loudest 3 seconds of the mixture, so at adverse SNR the gate locks the interferer); clean PTT is saturated (WER 0.000 in every arm); fp32 on pure room noise invented a 34-word phantom transmission where whisper alone hallucinated 2 words. The corpus finding is half the result: exactly one genuine human PTT recording exists in the estate (tx_kestrel.wav). Kit retained on the Thor at `~/voxlock-ab/`; the integration sketch is filed there, not adopted.
- [Batch deep-learn #1](../../batch-deep-learn-20261108.md) *(cross-reference; home room: world-models-and-drafting)* — the voice thread's origins: §8 is the VoxLock claim as submitted (and the pattern it proposed — isolate before you recognise — with its deployment shape: gate on detected background speech, never unconditionally); §3 (Soniox) gives the played-text-is-truth contract and the behaviour-diff rule for provider upgrades; §9 (Audio8) is the Piper successor candidate, audition-first; §16 is the Apriel architecture map, research-only by ruling.
- [Batch deep-learn #2](../../batch-deep-learn-2-20261108.md) *(cross-reference; home room: fleet-and-substrate)* — §4 (ESP32-P4 offline ASR): a phrase-bounded recogniser with zero false activations across 88 near-miss clips — "a doorbell, not an ear," and consonant with the presence doctrine; §6 (VoicePipe) is announcement-grade only, filed as such.
- [Batch deep-learn #3](../../batch-deep-learn-3-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — §3 (Block's Dessa) is the voice thread's far pole: a conversation model trained only on speech, demos only; §4 (Bolt E4B) is the named presence evaluation candidate (ACTIONS item 15), with its Tau2 loss printed in our doc so a future evaluation benchmarks the right weakness.
- Radio-room records (pointer, Thor-side): `~/radio-room-thor/` (brain-side service :8079, render receipts) and the ProArt `~/radio-room/` (PTT client) — the live system's records live with the system; TOOLS.md carries the measured pipeline summary.

## OPEN THREADS

- **VoxLock fixed-enrolment re-test** — the first of three filed re-test candidates: enrol explicitly from tx_kestrel instead of auto-enrolling on the mixture. It attacks the exact failure mechanism and matches the real deployment (one known operator). Waits on: a chartered spike.
- **A presence/energy gate for the background class** — filed candidate 2 from the A/B: an extractor is not a rejector, and no arm had a presence floor. Waits on: the same spike window as the re-test.
- **More human PTT material** — filed candidate 3, and the binding one: every audio verdict in this room currently rests on one human clip plus constructed mixtures. Waits on: real transmissions being recorded and retained (which is itself a retention-policy question — the shelf-itself room's G2 thread).
- **Audio8 listening audition** — the batch-1 spike-lite: audition the Piper successor candidate on our own lines, per language, before any table is believed. Waits on: a voice work cycle.
- **Bolt E4B presence evaluation** (ACTIONS item 15) — sealed evidence only. Waits on: an evaluation window.
- **LFM3-Audio** — Casey's open item. Not re-asked.

## ANNOTATIONS

- Load-bearing: on clean PTT audio there was never a value case for the gate — WER 0.000 for whisper alone. VoxLock's published headline (23% → 5%) is benchmark-dependent, and an independent eval already beat it on AMI live; our rejection is a workload verdict (one speaker, one synthetic interferer, 18 constructed items), not a law about the artefact.
- The presence doctrine bounds everything here: recording *of people* is presence-shaped — opened deliberately, visibly live, consented — however it is dressed as telemetry (the seed digestion's tension (a), rooms-and-engine-state room). Ambient always-on listening stays refused; the ESP32 doorbell pattern is the acceptable shape.
- Superseded: the pre-A/B assumption that the radio room's problem was interference. The measured problems are enrolment capture and a missing presence floor — and, underneath both, a corpus that barely exists.

## FURTHER READING

- Soniox — via [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md): the agent-text-echo contract; the integration rule (feed the recogniser the text that actually played) is the steal.
- ESP32-P4 / Kroko — via CONTACTS: the rule-book-instead-of-LM recogniser; open artefact with eval scripts.
- Block — Dessa — via CONTACTS: the speech-native horizon marker (C+; demos only, no paper, no weights).
- NVIDIA Bolt E4B — via CONTACTS: open weights, vendor numbers, losses disclosed by the vendor itself.
