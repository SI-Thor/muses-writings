# The Benefits of Unified Memory, Audited

**Date:** 2026-11-08 · **Lane:** studies shelf, fleet-and-substrate · **Status:** complete; measurements run on the fleet Thor the same day.

**Commission:** Casey's direction, 2026-11-08 12:37 AKST — *"there should be a lot more research into the benefits of the unified memory. My ideas of borrowing from old mainframe concepts like Plato is just the beginning."* This document is the audit behind seed #2, the Shared-Manifold Edge Runtime: what unified memory (UMA) actually buys on Jetson-class silicon, what the mainframe era already knew about it, what it costs, what we measured on our own hardware, and which of our live systems it would — and would not — help.

**Provenance.** The research and measurements here were executed from the seed itself (`~/workspace/email/gmail/` copy of Casey's 2026-11-08 12:30 AKST email) and the digest filed beside it (`~/workspace/email/seeds/2026-11-08-shared-manifold-edge-runtime-DIGEST.md`); the seed's shelf digestion (`seed-manifold-digestion-20261108.md`) landed while the measurements ran, and its claim audit — eleven load-bearing hardware claims graded SOUND 4 / OVERSOLD 5 / WRONG 2, with zero bus contention on a shared 273 GB/s bus as the headline WRONG — corroborates Part 3 of this document from an independent pass; its germination candidate M1 (a managed-memory slab micro-benchmark on the Thor, "the required MEASUREMENT") is Part 4 here, executed. Claims are graded: **[M]** measured on our kit in Part 4 · **[V]** vendor-documented · **[P]** paper / third-party measurement · **[U]** UNMEASURED — named as an absence, not papered over. Every quantitative claim carries one of these marks or a citation in the source register.

---

## Part 1 — The Benefit Ledger

Unified memory on a Jetson is not a faster bus. The CPU and GPU sit on the same SoC and read and write the *same physical DRAM*; there is no PCIe link and no second memory to copy across. What UMA removes is therefore not transfer time in the abstract — it removes the *copies, serialisations, and duplicate residencies* that discrete-memory programming forces on you, and it replaces them with coherence, which has its own price (Part 3). The ledger below states each benefit as a mechanism plus its number, or its named absence of one.

### B1. The copy that never happens — one stage fewer, every handoff
**Mechanism.** With `cudaMallocManaged` or pinned (`cudaMallocHost`) memory on Jetson, a kernel dereferences the same pages the CPU just wrote. The `cudaMemcpy` stage of the classic write→copy→compute pipeline does not exist. On discrete GPUs that stage is a bus transfer; on Jetson it was always a DRAM-to-DRAM copy over the same bus the kernel then reads over — pure waste motion.
**Number [M].** On the Thor, the explicit-copy reference arm (pageable source → device copy → kernel, 16 MB) costs 191.2 µs end-to-end, of which the kernel alone is ~116–120 µs — the copy stage is ~71–75 µs, i.e. ~37% of the pipeline, spent moving bytes between two addresses in the same DRAM. Zero-copy arms delete that stage by construction.

### B2. Single residency — one copy of the world
**Mechanism.** A slab held once in DRAM is the only copy. Every consumer — CPU clerk, GPU lens, logger — reads the same bytes. The alternative, our current practice, keeps the world in a producer's memory, serialises it to a JSON file or an HTTP body, and re-materialises it in every consumer: N consumers, N copies, and a synchronisation tax paid in staleness rather than microseconds. The seed names this the duplication/sync tax; it is the manifold's founding complaint.
**Number.** The arithmetic is exact but the fleet gain is **[U] UNMEASURED** for our systems: nobody has yet counted the bytes our current pipelines duplicate per tick. The probe's own example is illustrative — the 1M-record test ring is 64 MB as binary records and 117.7 MB as JSONL text [M], and every JSON consumer pays the parse again (B10).

### B3. Pointer identity — the same address means the same bytes on both sides
**Mechanism.** With unified addressing, a pointer value is valid on CPU and GPU alike (Thor device properties measured in Part 4: `unifiedAddressing=1`, `canMapHostMemory=1` [M]). Linked structures — trees, graphs, ring buffers with embedded offsets-that-are-pointers — can be built by the CPU and traversed by the GPU without a translation layer. Message passing *cannot fake this*: serialisation flattens pointers into data, and the receiver rebuilds a different graph that merely resembles the original.
**Number.** This is a capability, not a speed; its measure is the class of algorithms it admits (in-place graph traversal, shared lock-free rings — B9). No honest scalar exists; tagged as capability-grade, not UNMEASURED-by-omission.

### B4. Fine-grained handoff latency — record-scale, not file-scale
**Mechanism.** A producer can publish a single 64-byte record and a consumer can see it after one coherence action — a fence and a flag — instead of after a file write, a flush, an HTTP round trip, and a parse. The granularity of sharing drops from "snapshots" to "records".
**Number [M].** On the Thor, the launch→CPU-visible flag latency is ~330 µs median for both pinned and managed memory — but the honest reading is that this figure is *launch-path-dominated* under the box's power-managed (schedutil) driver stack; the coherence action itself is below that floor and not separately measurable with this method. The comparison that matters is against the incumbent: a file-or-HTTP handoff is milliseconds on a good day. The incumbent's precise latency in our stack is **[U] UNMEASURED**; the ordering (µs-class vs ms-class) is not in doubt.

### B5. Demand paging — allocate the trajectory, touch what you use
**Mechanism.** Managed allocations are populated on first touch: pages materialise when CPU or GPU faults on them (CUDA for Tegra documents this for Thor-class parts [V]). A design can allocate a slab sized for the whole trajectory history and pay residency only for the windows actually touched — the append-only stream the seed wants, without pre-committing 128 GB.
**Number [M].** The price of the fault path is measurable: the first CPU fill of a fresh 16 MB managed region took 3,364 µs, against ~1,396 µs to re-read the same region warm — first touch costs roughly 2–3× and belongs in any capacity plan.

### B6. Bandwidth honesty — the bus is shared, but it is only crossed once
**Mechanism.** UMA does not add bandwidth. The Thor's LPDDR5X is rated at 273 GB/s [V] and that single pool serves CPU, GPU, and everything else on the SoC. What zero-copy changes is how many times a logical transfer crosses the bus: an explicit copy crosses it twice (read + write) before the kernel crosses it a third time; direct access crosses it once.
**Number [M].** A focused lens sweep over a 64 MB pinned ring sustained ≈210 GB/s effective — 77% of the rated peak, in-situ, alongside the box's standing services. The Orin's envelope is smaller: 204 GB/s rated for the 64 GB AGX Orin, 102 GB/s for Orin NX Super [V].

### B7. The clerk can read the oracle's notebook — in-place post-processing
**Mechanism.** Because GPU results land in ordinary DRAM pages, the CPU can inspect, filter, log, or partially reduce GPU output with normal code — no download stage, no second representation. This is the seed's "CPU as clerk" made literal: bookkeeping over the same bytes the oracle wrote.
**Number [M].** A single CPU core scanning GPU-written managed memory read 16 MB in 1,396 µs (~12 GB/s, scalar loop) — slow in absolute terms, but the point is that the *option exists at zero setup cost*; a discrete pipeline pays a copy before the first byte can be examined at all.

### B8. Zero-copy at the sensor edge
**Mechanism.** Jetson's multimedia and camera stacks are built on pinned/dmabuf surfaces precisely so ISP, encoder, and GPU consume frames where they were captured. A UMA slab extends the same treatment to derived state — detections, tracks, embeddings — appended beside the frame metadata rather than shipped to it.
**Number.** Fleet-specific gain **[U] UNMEASURED** — our curator pipeline's per-frame copy budget has never been instrumented. Named here because the mechanism is the Jetson platform's own idiom [V], not an invention of this document.

### B9. System-scope atomics — the wait-free ring is legal
**Mechanism.** The seed's append-only ring stands or falls on one question: can a CPU writer and a GPU reader share a head pointer with acquire–release semantics and never tear a 64-byte record? Thor-class silicon answers yes: `concurrentManagedAccess=1` [M], and CUDA for Tegra documents full system coherency on Thor — CPU and GPU may both cache, and the CPU can read the GPU's latest cached updates [V]. System-wide atomics are unavailable below CC 7.2 [V]; the Orin (CC 8.7) and Thor (CC 11.0) are both clear of that floor, though only Thor carries the full-coherency guarantee (Part 3).
**Number.** Capability-grade (see B3). The contention probe in Part 4 ran exactly this pattern — CPU appending while GPU swept — with no torn reads observed in 5-second arms [M].

### B10. Projection without extraction — the lens is cheaper than the parse
**Mechanism.** This is the manifold seed's core economic claim: if state already lives in a binary slab, a "lens" is a kernel sweep over records in place. If state lives in a JSON file, every question begins with reading and parsing the whole file. The lens cost scales with the records; the parse cost scales with the *text*.
**Number [M].** Over the identical 1,048,576 records: the GPU lens sweep takes 0.32 ms; a generous native floor — a hand-rolled C++ scan-parser, parse-time only, file already in memory — takes 129.8 ms; our actual fleet practice, python3 `json.loads` per line, takes 2,432 ms. The slab is ~400× cheaper than the native parse and ~7,600× cheaper than current practice, per question asked. Every correctness check agreed to the digit (3,145,720.0).

**Ledger count: 10 benefits. 7 carry measured or vendor numbers (B1, B4, B5, B6, B7, B10 measured; B6/B9 vendor-backed); 2 are capability-grade (B3, B9); 2 carry explicit UNMEASURED tags on their fleet-specific gain (B2, B8).**

---

## Part 2 — The Mainframe Lineage

Casey's instinct — that PLATO solved this shape of problem before — is correct, and the lineage is wider than PLATO. The industry has re-derived "many consumers, one shared memory, no copies" at least six times, and each derivation left a lesson a Jetson UMA design should not have to re-learn.

### L1. PLATO common blocks (CDC Cyber, 1970s)
**Mechanism.** On PLATO, each user process owned a private segment of 150 variables that persisted across sessions. A lesson could additionally attach *one shared common block* of up to 1,500 words, visible to every terminal running that lesson; named commons were bound to a lesson file, unnamed ones lived while the lesson was active. Spasim (1974) put ship positions in common storage and every terminal projected its own wireframe view from the same words — the seed's slab-and-lenses arrangement, on a CDC 6600, fifty years early. By early 1976 PLATO IV served ~950 terminals at 150+ locations from one Cyber 73.
**Lesson for UMA.** The common block was *small and fixed-schema* (1,500 words ≈ 11 KB in 60-bit words) while private state was per-user. The split is the design: share the world's state in the slab; keep each agent's scratch private. PLATO also shows the governance model — a common block belonged to a lesson, i.e. shared state had an *owner*, not a free-for-all.

### L2. CICS and the shared-storage transaction monitors (1970s– )
**Mechanism.** CICS ran thousands of terminals' transactions inside one address space, with shared storage areas (the Common Work Area and successors) that any transaction could read, precisely so that no task paid for a private copy of reference data. The monitor owned scheduling and integrity; transactions were short, stateless-ish, and touched shared state briefly.
**Lesson for UMA.** The transaction monitor is the ancestor of the seed's "CPU as clerk": a single trusted bookkeeper mediates writes to shared state while many readers proceed freely. Short touches, one writer discipline, readers unblocked — that is a ring-append protocol wearing a suit.

### L3. The Coupling Facility — Parallel Sysplex (IBM, 1994)
**Mechanism.** Dedicated hardware running CFCC microcode holds three structure types — *lock*, *list*, and *cache* — shared by up to 32 systems. Changed data is invalidated in local caches by hardware cross-interrogation, and a common time source (Sysplex Timer, later STP) gives every system the same clock, so ordering claims are checkable. CICS data sharing, named counters, and data tables all run on it.
**Lesson for UMA.** Two of them. First: the winning primitives were not "shared memory" in the abstract but three named shapes — locks, lists, caches — which map embarrassingly well onto slab practice (a head-pointer lock word, append-only list rings, read-mostly reference regions). Second: *shared time is a feature of the substrate*, not the application — the manifold's time-first records (every VectorState leads with a timestamp) are Sysplex thinking; on one SoC the monotonic clock is free, across boxes it is the first thing you lose (Part 5).

### L4. Single-level store — System/38 → AS/400 (1979– )
**Mechanism.** The System/38 made RAM and disk one contiguous virtual address space: 48-bit addresses, every object — program, file, queue — in the same store, addressed the same way, with the machine (not the programmer) deciding residency. Its Technology Independent Machine Interface meant that when the line moved from 48-bit CISC to 64-bit PowerPC in 1995, the installed base recompiled *nothing*: the abstraction, not the hardware, was the contract. AS/400 (1988) carried the design to market scale.
**Lesson for UMA.** This is the closest historical relative of UMA thinking: *one address space, residency is the platform's problem*. Its warning is equally transferable — single-level store worked because the platform owned paging policy completely; a UMA design that lets every agent improvise its own access pattern gets the costs of Part 3 without the benefits. Policy (prefetch, advise, residency) must be platform-owned, as it was in Rochester.

### L5. Multics segments (1965– )
**Mechanism.** Multics made the segment the unit of both memory and filing: a file *was* a segment, mapped into the address space and shared between processes by name, with per-segment access control. The "single-level memory" phrasing in the seed's lineage traces here.
**Lesson for UMA.** Sharing by *named, permissioned object* rather than by raw range. A manifold slab wants the same: named regions (world ring, frame ring, embeddings) with stated read/write rights per lens — Multics had the access-control list in 1965; a design without one is behind the state of the art by six decades.

### L6. Oracle's SGA (1980s– )
**Mechanism.** An Oracle instance is built around the System Global Area — buffer cache, redo log buffer, shared pool — held in shared memory and touched by every server and background process, while each process keeps a small private PGA for its own session state. The database's hot state exists once; processes attach to it.
**Lesson for UMA.** The SGA/PGA split is PLATO's common/private split industrialised, and it has survived forty years of hardware change intact — evidence that the *shape* is load-bearing, not nostalgic. Note also what Oracle put in the shared area: buffers and *redo* — the log is shared too, because recovery is a consumer like any other. A slab design should expect its ledger to live in the slab.

### L7. Modern echo: RDMA and far memory
**Mechanism.** RDMA let one machine read another's memory without involving its CPU; "far memory" systems then swapped cold pages to a neighbour's spare DRAM. The mechanism works and the industry measured its tax precisely: network round trips in the tens of microseconds, against ~100 ns for local DRAM.
**Lesson for UMA.** Far memory's entire literature is a study in what UMA does *not* have to pay: on one SoC, the "remote" side is the same DRAM. But the converse also holds — the moment a design spans boxes (Orin world ↔ Thor brain), it *becomes* far memory and inherits its costs. Part 5's non-fits live exactly there.

### L8. Modern echo: CXL pooled memory (2020s)
**Mechanism.** CXL.mem attaches memory pools to hosts over a cache-coherent load/store fabric: ~170–250 ns round-trip [P], Type-3 devices measured at 150–400 ns and ~32 GB/s per Gen5 x8 link [P]. The motivation is measured waste — Microsoft's Azure traces found ~6% of fleet memory stranded on average, up to 25% at peak [P] — and the performance is real where the fabric is (H100 LLM inference over CXL ran 3.8×/6.5× faster than 200G/100G RDMA baselines [P]).
**Lesson for UMA.** CXL is the industry re-deriving the slab at rack scale, and its numbers are the calibration for any "slab across the LAN" idea: CXL achieves its latencies on a purpose-built fabric; gigabit Ethernet is three orders of magnitude away from 200 ns. A LAN-spanning manifold is a *consistency* research problem (Part 5), not a memory problem.

### L9. Modern echo: Apache Arrow and zero-copy columnar interchange
**Mechanism.** Arrow fixed a columnar memory format so that processes and languages share tables *in place* — the format is the memory layout, so "loading" is pointer arithmetic. Plasma/shared-memory object stores built the same idea for ML pipelines.
**Lesson for UMA.** The seed's 64-byte VectorState is an Arrow-style move at record scale: the discipline that makes zero-copy real is a *frozen layout with versioned evolution*, agreed before the first consumer. Arrow's other lesson is adoption economics: the format won because the layout contract was published and boring.

### L10. Modern echo: shared-memory IPC done right — iceoryx / ROS 2
**Mechanism.** iceoryx has publishers write into loaned shared-memory chunks managed by a daemon (RouDi); subscribers read the chunk in place and return it. No copy, no serialisation, loan discipline instead of ownership transfer. Independent benchmarking (CMLabs Psyclone, July 2026) measured iceoryx at ≈6 µs p50 against ≈27 µs for a tuned Fast-DDS shared-memory transport and ≈9–10 µs for intra-process delivery [P].
**Lesson for UMA.** Even *within* shared memory, discipline is the difference between 6 µs and 27 µs: chunk loaning, fixed pools, no allocation on the hot path. The slab's ring protocol should be designed with iceoryx's austerity, and its numbers are the bar for any future fleet IPC we build on the slab.

**Lineage count: 10 entries (6 historical, 1 bridge — far memory — and 3 modern echoes). The pattern across all ten: the mechanism that survives is never "share everything"; it is a small, owned, fixed-schema shared region, a named set of primitives, platform-owned residency policy, and private scratch for everyone.**

---

## Part 3 — The Costs & Cliffs

Equal weight, per the commission: this is an audit, not a brochure. Every benefit in Part 1 has a shadow price, and two of them were measured on our own kit during this study.

### C1. Page-fault storms — first touch is a cliff, not a slope
Managed memory materialises on fault. A kernel that sweeps a freshly-allocated region pays the fault cost for every page it touches, on the critical path. Measured [M]: the first CPU fill of a fresh 16 MB managed region cost 3,364 µs versus ~1,396 µs to read it warm; the first kernel pass over fresh pages ran at the slow end of every distribution in this study. The failure mode compounds: a design that allocates per-tick (a fresh managed buffer per frame, per tick, per lens) pays the storm *every tick*. Mitigations are known and boring — allocate once, warm deliberately, prefetch (`cudaMemPrefetchAsync`) or advise (`cudaMemAdvise`) ahead of the sweep — and measured prefetch removed the tail at 16 MB (p90 816 µs → 653 µs) even where the median barely moved [M]. But they are policy, and policy must be owned (L4's lesson).

### C2. Coherence granularity and the false-sharing analogue
What migrates or invalidates is never the 64-byte record you were thinking about; it is the page or cache line the hardware thinks in. Two agents writing *different* records that share a line still pay each other's coherence traffic — the classic false-sharing tax, transplanted to CPU↔GPU. On Thor the current UVM driver maps managed memory as GPU-uncached / I/O-coherent [V], which trades one failure mode for another: no stale-cache surprises, but GPU reads of managed pages do not enjoy the caching the same silicon gives device memory. The design consequence is layout discipline: hot per-writer state gets its own lines; read-mostly regions are separated from append regions; the ring head lives alone. None of this is optional, and none of it is visible in the API — it is exactly the class of cost a brochure omits.

### C3. The shared-bus contention tax — real, bounded, and easy to overstate
One DRAM pool means the CPU writer and the GPU reader drink from the same 273 GB/s [V]. Our contention probe [M] ran a CPU append writer against continuous GPU sweeps of a 64 MB managed ring for 5-second arms: the writer's throughput fell 9.5% under concurrent sweeps (156.4M → 141.5M records/s, in a deliberately cache-resident writer loop — the direction is trustworthy, the magnitude is an upper-bound sketch), and no sweep degradation beyond run-to-run clock-ramp noise was observed. Two honest qualifiers: the writer loop was cache-resident, so true DRAM-level contention at slab scale is **[U] UNMEASURED** in the strict sense; and the box's power management (schedutil governor) moved clocks during the arms, which is why this study reports the contention tax as *present but not catastrophic under probe conditions* and refuses a false-precision number. A streaming writer that actually misses cache is the follow-up probe (Part 5).

### C4. The launch floor — fine-grained ping-pong is launch-bound on this stack
The seductive UMA pattern is a tight loop: CPU writes a record, GPU answers, CPU reads the answer. Measured [M] on the Thor, a single launch→read→sync round trip costs ~338–385 µs *regardless of memory kind* — device-resident control included — and a launch→CPU-visible-flag round trip costs ~330 µs for pinned and managed alike. The coherence mechanism's contribution is below this floor; the floor itself is the driver/launch/wake path under the box's current power management. Consequence: designs must *batch* — sweep windows, not records; ask the GPU questions at 10–100 Hz, not per event — or the launch floor, not memory, becomes the system's clock. This is the single most consequential measurement in the study for manifold design.

### C5. Explicit copies sometimes win — the crossover the seed never mentions
Measured [M] at 16 MB with an alternating full-buffer rewrite pattern: explicit copy + device-resident kernel, **191 µs**; zero-copy pageable direct access, 297 µs; managed/pinned end-to-end (CPU fill included), ~646–651 µs. When data is *reused* by the GPU across many kernels, or rewritten wholesale each round, device residency amortises and zero-copy's bookkeeping is pure overhead. Zero-copy wins when data is touched once, streamed, or produced and consumed at different rates by the two sides — the ring pattern. The honest rule: **stream → share; reuse → copy.** A manifold that puts its hot model weights or its repeatedly-swept static geometry in managed memory has chosen wrong; a manifold that copies its append-only event stream has also chosen wrong.

### C6. The Orin's tighter envelope
Everything above is Thor-measured. The Orin differs in ways that matter: 204 GB/s (64 GB model) or 102 GB/s (NX) rated bandwidth [V]; no Sysmem Full Coherency — its `concurrentManagedAccess` posture is weaker than Thor's [V], so patterns that are free on Thor (both sides caching the same managed pages) are not guaranteed there; and `cudaMemPrefetchAsync` is unsupported where concurrent managed access is absent [V]. Any slab design must be specified against the Orin's floor, not the Thor's ceiling, if it is to run in the world where the game actually lives. Orin-side numbers in this study are by pointer: the platform figures above, plus the fleet's existing Orin operational record — no new load was placed on the Orin's game stack, per the commission.

### C7. Quirks and unsupported paths (documented)
From CUDA for Tegra (Release 13.5, Nov 2026) [V]: GPUDirect RDMA is not supported on Tegra; peer-to-peer is not supported; NVML exists only on Thor and later; physical pages of a managed allocation may not be mapped at all until touched; pinned memory is uncached below CC 7.2 and cached at or above it; on the current driver, managed mappings are GPU-uncached/I/O-coherent by policy (C2). CUDA 13 adds memory-sharing IPC on Thor with the open-source driver — promising for multi-process slab designs, and untested by us. Each of these is a place a naive port from desktop CUDA assumptions will silently misbehave.

### C8. The complexity bill
The deepest cost is not in any table: UMA replaces a *visible* cost (copies you can profile) with an *invisible* one (coherence and fault behaviour you must infer). Debugging a torn read or a fault storm across a CPU/GPU boundary is harder than debugging a slow memcpy, and the tooling on Tegra is thinner than on desktop. The seed's own challenge list — sheaf gluing, tolerance vs stability, torn reads, kernel divergence, causal drift — is the honest price list; UMA pays the transfer bill and presents this one instead. Budget for it.

---

## Part 4 — Measurements on Our Kit

**Pre-registration** (written before the first probe ran; the full text ships with the probe source): **(a) Handoff** — MANAGED vs PINNED vs PAGEABLE at 1 KB / 64 KB / 16 MB; 100 repetitions (30 at 16 MB), 5 warm-ups excluded; median + p10/p90; a managed first-touch block; a prefetch arm at 16 MB. **(b) Lens-sweep proxy** — 64-byte records, MANAGED and PINNED rings at 16,384 records (1 MB) and 1,048,576 records (64 MB); 100 sweeps per scale; baselines python3 `json.loads` per line (fleet practice) and a C++ read+scan parse (generous native floor), 5 runs, median. **(c) Contention** — three 5-second arms: CPU writer alone, GPU sweeps alone, both together. Probe source: `uma_probe.cu` (≈13.8 KB), compiled `nvcc -O2 -arch=sm_110`; follow-up spot probes (focused sweep, latency) run from /tmp and deleted after.

**Environment truth.** Jetson AGX Thor; device "NVIDIA Thor", CC 11.0; driver/CUDA runtime 13.2; `concurrentManagedAccess=1`, `pageableMemoryAccess=1`, `canMapHostMemory=1`, `unifiedAddressing=1`; nvpmodel MAXN; CPU governor **schedutil** (dynamic clocks; 972 MHz observed at idle) — latency figures below are therefore *as the fleet actually runs*, not as a locked-clock benchmark rig would flatter them; kernel 6.8.12-1021-tegra. The box's standing services (presence :8310, actor :8311, JEV rack :8077) ran untouched throughout; all probe processes have exited and all allocations were freed.

### 4a. Handoff — CPU writes, GPU reads (end-to-end, median)

| Size | MANAGED | PINNED | Notes |
|---|---|---|---|
| 1 KB | 39.3 µs | 39.3 µs | kernel-only 21.0 µs both |
| 64 KB | 39.3 µs | 39.2 µs | kernel-only 20.9 µs both |
| 16 MB | 650.6 µs | 646.1 µs | kernel-only 120.0 / 116.3 µs; managed+prefetch 645.9 µs (p90 816→653) |

GPU writes → CPU reads: 1 KB 21.1 µs both kinds; 64 KB 27.2 µs; 16 MB sync+read 1,945 µs managed / 2,063 µs pinned, of which the CPU's own scalar read is 1,396 / 1,523 µs (~12.0 / ~11.0 GB/s single-core). PAGEABLE direct GPU dereference **succeeded** on Thor (`pageableMemoryAccess=1`): 16 MB end-to-end 297.3 µs; the explicit memcpy+kernel reference arm: 191.2 µs (see C5). First touch on a fresh 16 MB managed region: first CPU fill 3,363.9 µs; first kernel pass 680.1 µs.

Reading: below ~64 KB, every handoff is the same ~39 µs of launch-and-sync overhead wearing different hats — memory kind is irrelevant at record/window scale. At 16 MB the kinds still tie (managed ≈ pinned), prefetch buys tail-latency rather than median, and the fastest full-buffer pattern is the explicit copy the zero-copy story was supposed to retire (C5).

### 4b. Lens sweep — the number the manifold seed needs

Ring of 64-byte records (`ts u64, ent u32, flags u32, pose[4], dyn[4], tel[4]`); lens = sum of `tel[0]` over records with `flags&1`; all arms agree exactly (1 MB: 49,142.0; 64 MB: 3,145,720.0).

| Arm | 1 MB ring (16K records) | 64 MB ring (1M records) |
|---|---|---|
| MANAGED sweep, per-launch end-to-end | 219.3 µs | 429.9 µs (p10 318.5, max 1,224.9 — spiky) |
| PINNED sweep, per-launch end-to-end | 221.2 µs | 341.1 µs |
| PINNED sweep, focused kernel time (CUDA events, grid right-sized) | 62.4 µs | 319.8 µs (≈210 GB/s) |
| C++ read+scan parse of the same 1M records (JSONL, parse only) | — | 129.8 ms |
| python3 `json.loads` per line (read + parse, fleet practice) | — | 2,432.1 ms |

The lens over a 64 MB binary ring costs **0.32 ms**; asking the same question of the same data in our current file-and-parse practice costs **2.43 s**; even a hand-tuned native parser floor is **129.8 ms**. Ratios: ~7,600× vs practice, ~400× vs the native floor. At world-digest scale (1 MB) the fixed launch overhead dominates and the honest figure is ~62 µs of kernel per question. Managed and pinned are statistically indistinguishable for reads; managed shows a spikier tail at 64 MB.

### 4c. Contention — writer appending while lenses sweep (MANAGED 64 MB ring, 5 s arms)

- Writer alone: 156.4M records/s (cache-resident append loop — an upper-bound instrument, see C3).
- Sweeps alone: median 0.998 ms per sweep (batch-of-10 amortised).
- Both together: writer 141.5M records/s (**−9.5%**); median sweep 0.812 ms — *lower* than sweeps-alone, an artifact of clock ramping across arm order under schedutil; reported only as evidence that no contention catastrophe occurs, not as a speedup.

### 4d. Latency spot checks

Launch+read+sync of a single word: 384.6 µs pinned / 372.7 µs managed / 337.7 µs device-resident (medians, 200 reps). Launch→CPU-visible flag with a spin-wait and no sync call: 331.2 µs pinned / 330.5 µs managed (300 reps). The memory kind contributes nothing measurable at this granularity on this stack; the launch path is the latency (C4).

**Cleanup verification:** `pgrep` shows no probe processes; presence (:8310) and actor (:8311) server processes confirmed present and unsignalled before and after; JEV rack untouched; probe allocations freed at process exit; scratch probes deleted; the Thor working directory holds only the probe source and its 117 MB JSONL test file alongside this study's inputs.

---

## Part 5 — So-What for the Fleet

UMA is a *within-box* technology. Every fit below is judged on that line first: if the producer and the consumer of the state live on the same SoC, a slab can serve them; if they live on different boxes, the slab cannot span the gap and the honest technology is messaging — or research (open questions).

### Fits

**Game master's world-state reads — FIT, with a placement condition.** The mechanism of gain is B10 verbatim: the game master's questions (who is stalled, who is hungry, what changed) are lens sweeps over world state. Today that state crosses Orin→Thor as files/HTTP and is parsed per question. The condition: the slab must live where the digest is *written* — the Orin, which has its own UMA (weaker than Thor's, C6) — with lens *results* (small) crossing the LAN, or the digest producer moves to the Thor. Either way the migration cost is real: a binary digest writer beside the world digest, a frozen 64-byte-ish record layout (L9's contract), and lens kernels where JSON queries are today. Expected gain: per-question cost from seconds-class (at 1M-record scale) to sub-millisecond-class, per §4b — which converts the game master from a batch reader into something that can afford to ask continuously.

**Curator frame handling — PARTIAL FIT.** Within the Thor, frames already ingested can be slab-resident for the curator's GPU passes (embeddings, scoring) with zero re-staging — B8's mechanism. But capture happens on the Orin; the Orin→Thor leg remains a network transfer no slab can remove. Migration cost: moderate (frame-ring writer in the ingest path). Gain: the Thor-side stages only; do not let the proposal quietly claim the cross-box leg.

**JEV rack embeddings — FIT, modest gain.** The rack already computes on the Thor's GPU; its inputs and outputs stage through ordinary host memory today. A managed slab for judge inputs/outputs removes the staging copies (B1) and lets CPU-side bookkeeping read results in place (B7). Expected gain is honest-small — the rack's costs are model-bound, not copy-bound — but the migration cost is the smallest of any fit here, which makes it the right *first* slab: a low-risk place to learn the discipline (C2 layout rules, C1 warming policy) before the game master depends on it.

**League heartbeats — NON-FIT (named, with reason).** Heartbeats exist to prove, across boxes, that an effect landed in a store the actor cannot write. A shared-memory slab is definitionally a store the actor *can* write, on a box the watcher may not share; and the failure the heartbeat guards against — refreshes sent but never landed, the daylight-hold lesson — is a cross-box delivery failure that no intra-box mechanism can even observe. UMA would make heartbeats faster and *less true*. The correct technology here remains what the Watcher's Charter already specifies: effect-verification in an independent store.

**Presence / actor LLM serving — NON-FIT (named, with reason).** The :8310/:8311 llama.cpp servers are bound by weight bandwidth inside their own allocator's residency choices; their weights are the canonical C5 case — reused every token, wholesale — where device residency wins and managed memory adds a fault path while removing no copy that actually happens. Wrapping them in a slab buys nothing and risks the standing services. Excluded.

### Open research questions (the reflection layer)

1. **Sheaf gluing across boards.** The seed's hardest challenge sharpens off-box: two slabs on two SoCs, each with local lenses, whose overlapping projections must not contradict. What is the cheapest consistency that keeps a game master's Thor-side view honest about Orin-side state — and is the answer just "ship lens results, never state"?
2. **CXL-over-LAN analogues.** CXL buys 200 ns coherence on a purpose-built fabric [P]; our LAN offers ~100 µs-class latency on a good hop. Three orders of magnitude is not a gap engineering closes; what consistency model (the seed's tolerance ε is the candidate) makes a *slow-coherent* manifold useful rather than merely correct?
3. **Lens versioning and causal drift, measured.** Re-projecting history with a newer lens must reproduce or honestly diverge; nobody has yet built the harness that measures drift on our own trajectory data.
4. **Contention under a streaming (cache-missing) writer.** Part 4's writer was cache-resident by design; the DRAM-level tax of a real ingest stream against concurrent sweeps is the follow-up probe this study owes (C3).
5. **DVFS-honest benchmarking.** Every latency in Part 4 carries the schedutil caveat. A locked-clock re-run would separate mechanism from power management — at the cost of measuring a machine the fleet does not actually run.
6. **Managed weights, honestly.** C5 says reuse → copy; but a demand-paged weight store (B5) would let an oversubscribed box hold more models than its residency budget — the JEV rack's cold models are the test case. Unmeasured, and worth one spike before it is believed either way.

---

## Source register (CONTACTS-style)

- **Seed & digest (primary):** Casey, "Architectural Briefing: The Shared-Manifold Edge Runtime", emailed 2026-11-08 12:30 AKST (subject line lost in his send pipeline); digest at `~/workspace/email/seeds/2026-11-08-shared-manifold-edge-runtime-DIGEST.md`. The seed's Rust corpus is an unbuilt sketch; its performance rhetoric ("single clock cycle", "bandwidth drops to zero") is treated as rhetoric throughout, per the digest's own caveat.
- **NVIDIA, Jetson AGX Thor product page** — 128 GB 256-bit LPDDR5X, 273 GB/s; AGX Orin 204 GB/s; Orin NX Super 102 GB/s. (One independent review measured 276 GB/s on Thor.)
- **NVIDIA, CUDA for Tegra, Release 13.5 (Nov 2026), docs.nvidia.com** — same-DRAM residency on Tegra; Sysmem Full Coherency Thor-only; `concurrentManagedAccess` / `pageableMemoryAccess` gating; GPU-uncached I/O-coherent UVM mapping policy; prefetch/attach semantics; atomics floor CC 7.2; no GPUDirect RDMA / no P2P on Tegra; NVML Thor+; CUDA 13 IPC on Thor.
- **PLATO / TUTOR documentation (CERL lineage, via platohistory & bitsavers mirrors)** — 150 private variables per user; common blocks to 1,500 words; named vs temporary commons; CDC 60-bit words. Spasim: Jim Bowery, 1974. PLATO IV scale ~950 terminals, early 1976.
- **IBM, System/38 & AS/400 records** — single-level store, 48-bit addressing, TIMI; S/38 Aug 1979; AS/400 Jun 1988; 64-bit PowerPC migration 1995 without application recompilation.
- **IBM, Parallel Sysplex / Coupling Facility records** — Apr 1994; CFCC; lock/list/cache structures; hardware cache invalidation; up to 32 systems; Sysplex Timer/STP common time.
- **Oracle, SGA documentation** — buffer cache, redo log buffer, shared pool as shared memory per instance; PGA per-process private.
- **CXL / far-memory measurements** — CXL.mem ~170–250 ns round-trip; Type-3 devices 150–400 ns, ~32 GB/s per Gen5 x8; Azure stranded-memory traces (~6% average, ~25% peak; Microsoft, 100 clusters / 75 days); Microsoft Research NSDI 2026 CXL pod results; H100 LLM-over-CXL inference comparisons vs RDMA.
- **iceoryx / ROS 2 benchmarking** — CMLabs, Psyclone AIOS v2.2 (July 2026): iceoryx ≈6 µs p50; tuned Fast-DDS shared-memory ≈27 µs; intra-process ≈9–10 µs.
- **Own measurements** — Part 4 and `RESULTS.md`, probe source `uma_probe.cu`; pre-registration `PREREG.md`; all on the fleet Thor, 2026-11-08.

*Rooms placement: filed in the fleet-and-substrate room (primary), cross-referenced from rooms-and-engine-state; its Part 4 numbers are also pointed to from the benchmarks room, and Part 2's PLATO lineage supports the rooms room's PLATO/South-Africa thread (the room paper's L1 experiment: Casey as an always-available player in his own PLATO-flavoured room system).*
