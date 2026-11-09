# Room — World models & drafting

## STATE

Research-complete for this round; one experiment live. The D3D + Cosmos 3 deep dive is delivered (52 KB report, grade A− behind its one-page digestion). The D3D port experiment (ACTIONS item 11) was dispatched under Casey's blanket authorisation — the released system is two-GPU-hardwired, so the port co-locates the Qwen3-8B + D3D pair on the one Thor — and has no verdict in the trail yet; it is the named attack on the WSP Q1 clause-2 decode wall (≈8 steps/s in the real generate path, ~100+ hours per artefact). Cosmos is settled as a map: base-Nano generation is NIM-sanctioned on the Thor, the Sim checkpoints extrapolate to slow-motion only, and Cosmos3-Edge (4B) is the tier designed for this machine. What would reactivate more: the port's verdict, or a sealed evaluation window for Cosmos3-Edge (item 14). Last touched 2026-11-08.

## CONTENTS

- [D3D + Cosmos 3 deep-dive report](../../../research_notes/d3d-cosmos3-deep-dive-20261108-1841/report.md) — the full report. D3D: a standalone diffusion drafter (arXiv:2611.06425, MIT, public checkpoints) with published means of 5.00× (Qwen3-8B) and 5.71× (32B) on 2× H800 — eroding under concurrency (6.1× at 1 request → 2.7× at 16) and costing ~360 GPU-hours per new target; the released system is hard-wired across two devices, so any Thor number must come from a port, and the honest single-stream expectation is an estimated 2–4×, unmeasured. Cosmos 3: four 16B MoT checkpoints under OpenMDW-1.1; NVIDIA's own NIM matrix names the Jetson AGX Thor and says "Default to Nano."
- [Deep-dive working notes — D3D paper](../../../research_notes/d3d-cosmos3-deep-dive-20261108-1841/notes/d3d-paper.md) — the paper-level notes behind the report's D3D half; read these before citing a mechanism detail the report compresses.
- [Deep-dive working notes — Cosmos](../../../research_notes/d3d-cosmos3-deep-dive-20261108-1841/notes/cosmos.md) — the checkpoint/licence notes behind the report's Cosmos half, including the NIM support matrix reading.
- [D3D + Cosmos 3 digestion](../../digestion-d3d-cosmos3-20261108.md) — the one-page index entry for the deep dive; the shelf's doorway into the report, deliberately not a rewrite of it.
- [VFlash digestion](../../digestion-vflash-20261108.md) — speculative decoding for spatial predictions that verifies *structure* instead of exact tokens (acceptance by structural validity — the snap test, in drafting clothes). Thor latency 3,552.7 → 703.3 ms as reported; the source is journalism-grade (C+), so the multipliers are parked until the paper.
- [Frameboy / Atlas digestion](../../digestion-frameboy-atlas-20261108.md) — World Labs' world model streamed to a browser at ≤15 fps; its RTFM lineage (posed frames as spatial memory, "context juggling") is the spatial-memory thread to follow, and its shape rhymes with Confluence (see the rolling-perception room).
- [Batch deep-learn #1](../../batch-deep-learn-20261108.md) — home room for this batch. Its world/drafting spine: §2 D3D and §3 Cosmos 3 (the deep dive's batch-level first pass), §4 VFlash, §5 Frameboy, §15 L3G-World (a latent 3D Gaussian memory that grows with scene extent, not stream length — the bounded-memory representation pattern).
- [Batch deep-learn #2](../../batch-deep-learn-2-20261108.md) *(cross-reference; home room: fleet-and-substrate)* — the Gaussian/capture thread: §5 Echo-3 (capture becoming a commodity; accuracy claims absent), §10 RacerGS (>150× 3DGS compression — the delivery-size leg), §11 FlexiAvatar (evidence weighted by observation frequency — verification relocating into representation, again).
- [Batch deep-learn #3](../../batch-deep-learn-3-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — §1 MeSS and §5 Hi3D (the foundry's 3D intake references); §8 BlenderWorld, whose failure taxonomy is the foundry-verification shortlist #1 — spatial truth lives in state, not renders (ACTIONS item 22).
- [La-JEPA digestion](../../digestion-la-jepa-20261108.md) *(cross-reference; home room: benchmarks-and-experiments)* — JEPA features as a world model you *control from*, not a description you read; this room owns the world-model framing, the benchmarks room owns its spike and verdict.

## OPEN THREADS

- **The D3D port verdict** — IN FLIGHT (ACTIONS item 11). Waits on: the port lane's measurements on our workload shapes. If it lands at the estimated 2–4×, WSP Q1 clause 2 becomes measurable; if it fails its kill criterion, the wall stands and clause 2 stays unmeasurable — either verdict closes a question this room has carried since the deep dive.
- **Cosmos3-Edge evaluation** (ACTIONS item 14) — sealed evidence only, before any adoption for closed-loop work. Waits on: an evaluation window.
- **BlenderWorld taxonomy adoption** (ACTIONS item 22) — programmatic scene inspection for foundry verdicts. Waits on: the next foundry work cycle.
- **VFlash's real multipliers** — waits on: the paper. The digestion's C+ grade is the instruction: do not plan around journalism numbers.
- **WSP Q1 clause 2** — the measurement this room's experiment serves; its home is the fleet-and-substrate room, its unblock (if any) lands here first.

## ANNOTATIONS

- Quote D3D's speedups only with their conditions attached (2× H800, Transformers backend, greedy, non-thinking; concurrency erosion is part of the result, not a footnote).
- The "Default to Nano" line cuts both ways: it sanctions base-Nano generation on the Thor *and* marks the Sim checkpoints as someone else's tier. Slow-motion-only is a measurement-shaped extrapolation, stated as such in the report.
- Do not re-derive the Thor port estimate from the H800 numbers — the deep dive already did the bandwidth arithmetic; the port experiment replaces the estimate with a measurement.

## FURTHER READING

- D3D (arXiv:2611.06425; github.com/fudan-generative-vision/D3D) — via [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md): B+ — the cheapest credible attack on our decode wall.
- Cosmos 3 / NVIDIA NIM matrix — via CONTACTS: the vendor's own support tiers, which our map follows rather than improves on.
- World Labs (Frameboy/Atlas) — via CONTACTS: research preview, grade C; the RTFM lineage is the part worth returning to.
- BlenderWorld (arXiv:2610.23986) — via CONTACTS: A−; the external citation for the state-over-renders doctrine.
