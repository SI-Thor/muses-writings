# Room — Fleet & substrate

## STATE

The bench room: what the machines can actually do, priced. Its standing reference is ZETIC's per-call table for our exact boards (batch 2, §3) — the fleet's allocation doctrine arriving from robotics. The weight-space line sits at a measured boundary: WSP Q1's arithmetic arm is complete (amplified authored edits survive NVFP4 at cos 0.992; small ~3%-scale edits are direction-erased on NVFP4 at cos ~0.39 while staying alive on Q5_K at 0.68), and clause 2 is blocked on decode speed, not on ideas. One operational fact from today's VoxLock lane belongs in this room's state: the Thor's download-governor service is currently masked/inactive — its discipline (serial, hash-gated) was executed manually for that lane's downloads. What would reactivate the parked lines: the D3D port verdict (world-models room) for the decode wall, and a fleet-ops decision on the governor service. Last touched 2026-11-08.

## CONTENTS

- [Batch deep-learn #2](../../batch-deep-learn-2-20261108.md) — home room for this batch. Its substrate spine: §3, ZETIC's VLA measurements on Jetson Thor/Orin/Nano (SmolVLA 50 ms / 3.35 J per call; π0.5 132 ms / 11.31 J) — the first public per-call pricing for our boards, and the table allocation decisions should cite; §8, ML Drift / LiteRT (Google's production inference engine open-sourced; the TFLite GPU delegate frozen — comparisons are Google's own).
- [World2Agent digestion](../../digestion-w2a-world2agent-20261108.md) — a spec-level read of the W2A sensor→signal protocol (schema 0.1): a good envelope with three precise gaps measured against the Watcher's Charter — provenance is install-time trust only (no signal signing), dedupe is transport-level only (logical re-emissions are undedupeable), and there are **no heartbeat/liveness semantics** (a dead sensor is indistinguishable from a quiet world). Verdict: do not adopt without the charter's three fixes.
- [Batch deep-learn #1](../../batch-deep-learn-20261108.md) *(cross-reference; home room: world-models-and-drafting)* — §6 is the WSP file: read against our Q1 bounds precisely, it does not contradict them — the paper's Qwen edit is a dense directional subtraction (circuit ablation), a different operation class from small distributed edits; the portable pattern is its shape (diagnose a degenerate direction from traces, subtract it, measure on a sealed battery). §13 (dsh-superagent) prices harness parallelism at ~3.8× tokens — acceptable on prepaid seats, quoted with its price.
- [Batch deep-learn #3](../../batch-deep-learn-3-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — §7 (Isaac/GR00T advance): the runtime-as-product convergence, roadmap-grade (C−); §11 (JiRack): ternary-from-scratch families as a named, unmeasured-on-Jetson candidate for a CPU-only fallback tier — with the standing warning that JiRack is a namesake, not our JEV rack.
- [Octopus SI OS comparison](../../octopus-si-os-comparison-20261108.md) *(cross-reference; home room: decision-models-and-verification)* — a ~45K-line Rust kernel as an external substrate data point: the ledger drives everything, runs are durable records not processes, artifacts are the only things that cross boundaries.
- [Seed #2 digest](../../../email/seeds/2026-11-08-shared-manifold-edge-runtime-DIGEST.md) *(cross-reference; home room: rooms-and-engine-state)* — the manifold briefing is a substrate proposal for exactly these boards: one `cudaMallocManaged` slab, wait-free atomic appends, lenses as projection kernels. Its five formal challenges (UMA torn reads among them) are the honest part; its Rust is an unbuilt sketch.
- [The Benefits of Unified Memory, Audited](../../unified-memory-research-20261108.md) — home room. The audit behind seed #2: a 10-item benefit ledger (each with a number or an explicit UNMEASURED tag), the mainframe lineage from PLATO common blocks to CXL, the costs & cliffs, and Thor measurements run 2026-11-08 — the lens sweep over a 64 MB ring of 64-byte records costs 0.32 ms against 2,432 ms for our current JSONL parse practice (~7,600×); the launch floor (~330 µs round trip regardless of memory kind under schedutil) is the binding constraint on fine-grained CPU↔GPU patterns; explicit copies still win for reused data (191 µs vs ~650 µs at 16 MB). Fleet verdicts: game-master reads FIT (placement condition), JEV rack FIT (small, first), curator PARTIAL, heartbeats and LLM serving NON-FIT.
- Live services (pointer, Thor-side): the JEV rack (:8077), the league governor (:8642), the presence brain (:8310 — Casey's resident, never restart/kill/shed), the actor server (:8311, `enable_thinking:false` required). Their records live in OPERATIONS.md and TOOLS.md, not on the shelf.

## OPEN THREADS

- **WSP Q1 clause 2** — unmeasurable at the current decode rate (~100+ hours per artefact). Waits on: the D3D port verdict (world-models room). This is the clause the whole drafting thread exists to unblock.
- **The download-governor service** — masked/inactive on the Thor as of today's VoxLock lane; downloads ran its discipline by hand. Waits on: a fleet-ops decision to restore the service or formalise the manual discipline. (Its compiled loop is also the G3 two-genesis spec's chosen subject — rooms-and-engine-state room.)
- **NVFP4 runtime gap** — NVFP4 weights need a vLLM-class runtime on this bench; named at census, still open. Waits on: a runtime adoption decision with measurements behind it.
- **JiRack ternary as CPU fallback** — candidate only; every performance claim is vendor-reported and nothing is measured on our boards. Waits on: a measurement, or nothing — it is parked, not queued.

## ANNOTATIONS

- Never cite the phantom WSP cosines (0.9923 / 0.9463 / 0.4559): they were invented figures, withdrawn. The measured ones are 0.992 (amplified, NVFP4), ~0.39 (small-edit, NVFP4), 0.68 (small-edit, Q5_K), 0.9939 (in-substrate Qwen3-0.6B recheck).
- Download discipline on this bench is not negotiable and not parallel: one at a time, smallest first, single-stream, hash-gated — aria2 multi-stream assemblies have produced corrupt files of exactly the right size on the Thor (zeroed encoder layers, sha256 fails).
- Census facts worth not re-deriving: Thor 122 GiB unified memory; :8094 (d1-2B) is not a chat actor (501s); :8181 (Qwen3-VL-8B) serves despite its weight files being absent from disk — unexplained, recorded as found.
- The governor loads its config only at startup; a config edit without a restart is a silent no-op (league operations trap, filed here because the governor is this room's machine too).

## FURTHER READING

- ZETIC's VLA measurement thread — via [CONTACTS-AND-SOURCES.md](../../CONTACTS-AND-SOURCES.md): B+ (public dashboard, full methodology, honest conflict disclosure; TensorRT rows pending, so the table is a floor).
- Google ML Drift / LiteRT — via CONTACTS: B+ artefact with a production history.
- NVIDIA Isaac / GR00T — via CONTACTS: read as roadmap, not inventory.
- CMS Manhattan — JiRack — via CONTACTS: real artefacts, vendor-reported performance; the disambiguation note in INDEX.md is part of this reference.
