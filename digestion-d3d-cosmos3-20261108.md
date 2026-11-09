# Index entry — D3D + Cosmos 3 deep-dive (report lives elsewhere; this page makes the studies shelf complete)

*2026-11-08. This is a one-page summary + pointer, written under Casey's standing digestion instruction. The deep-dive itself already exists and is not rewritten here:*

- **Full report:** `~/workspace/research_notes/d3d-cosmos3-deep-dive-20261108-1841/report.md` (52,331 B; with working notes `notes/d3d-paper.md` and `notes/cosmos.md` alongside)
- **Built page:** slug `d3d-and-cosmos-3-deep-dive` (audit passed)

## D3D — asynchronous speculative decoding (arXiv 2611.06425)

Speculative decoding where the drafter runs *asynchronously* rather than in lockstep with the target. Headline means of **5.00× / 5.71×** need their conditions attached: measured on 2×H800, Transformers backend, greedy non-thinking decoding, **single-stream** — the 32B pair's advantage erodes from 6.1× to 2.7× at 16 concurrent requests. Code is MIT with 6 draft checkpoints public; the Qwen3-8B/32B pairs need no training, and a new target costs ≈360 GPU-hours. Drafter initialised from Qwen3 weights; B=16 blocks; auxiliary AR loss λ=1 (worth +0.24–0.40 τ); asynchronous packed pass N_async=384 tokens with a 71.3% cache hit at the optimum; pruning 36→31 layers retains >99% of τ. **Fleet relevance:** serving economics for our own Thor endpoints — speculative decoding is a serving-side win that costs no model quality, but the concurrency erosion says it serves *our* low-concurrency pattern (a household's worth of agents) far better than a public API's.

## Cosmos 3 — NVIDIA's interactive world-simulation family

The deep-dive's most useful correction: **GB200 was a test configuration, not a floor.** NIM memory floors for base Nano: 58 GiB BF16 / 44 GiB FP8 / 31 GiB FP8+offload (Transfer: 64 GiB BF16). NVIDIA's own NIM matrix names **Jetson AGX Thor (~86 GiB effective)** and says "default to Nano." Sim checkpoints' documented route is GB200-tested, so Thor rates are extrapolations: single-digit fps for Sim-Bimanual (54.1 fps on GB200); multi-view Sim-Auto ≪1 fps (GB200: 16.8 fps at 1 view → 3.0 at 7 → 1.8 at 11). **Cosmos3-Edge (4B) is the tier actually designed for Thor**: 1.53 s per 32-action chunk at a 15 Hz action rate, NVIDIA-measured on a Thor T5000. Licence: OpenMDW-1.1 (permissive, commercial use OK). Honesty notes from the report: all Cosmos quality numbers are NVIDIA-reported; LiDAR detection F1 is 0.188; policy-learning fidelity is unmeasured by NVIDIA's own admission. **Fleet relevance:** Cosmos is the world-model pole of the week's world-model thread (cf. Frameboy/Atlas digestion) — simulation as a service to policies; the Edge tier is the only piece sized for our hardware.

## Grade

Report-internal grading applies (primary sources verified live 2026-11-08; extrapolations labelled as such in the report). This entry adds no new claims.

---

*Pointer page compiled 2026-11-08. Read the report for evidence; read this page only to find it.*
