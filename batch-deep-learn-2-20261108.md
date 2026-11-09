# Batch deep-learn #2 — eleven links, read in full, graded, and mapped to the fleet

*2026-11-08. Written under Casey's standing instruction of the same day: "make sure you're using markdowns and making thorough research documents and digestion documents about everything I'm submitting to you including these and the ones earlier today and even our own research." Companion to batch 1 (`batch-deep-learn-20261108.md`). Part B of the same instruction — the retroactive digestion sweep over the morning's earlier submissions — lives in the `digestion-*.md` files listed in `INDEX.md`.*

## Grading scheme (house standard)

- **A** — paper + artefact: peer-reviewed or arXiv-grade write-up with a public artefact (code, weights, benchmark) others can run.
- **B** — public runs: artefact or data public and inspectable; numbers come from the authors/vendor and are not independently replicated.
- **C** — demos: a real product or demo you can touch, but capability claims rest on vendor material.
- **D** — marketing: announcement-grade only; nothing to inspect.

Grades judge the *evidence*, not the idea. A D can still be worth parking on the shelf; it just can't carry weight in an argument yet.

## Contents

1. Liquid AI LFM3 (text / VL / audio / omni / decision models) — **B**
2. vLLM Semantic Router d3-ultra (27B decision model) — **B−**
3. VLA models measured on Jetson AGX Thor / AGX Orin / Orin Nano (ZETIC) — **B+**
4. ESP32-P4 offline speech recognition (Kroko on a microcontroller) — **B**
5. SpAItial Echo-3 (iPhone video → metric 3D twin) — **C**
6. VoicePipe (script in, performed dialogue out) — **C−**
7. Skill∞ (arXiv 2610.35434 — recursive self-improvement of agent skills) — **A−**
8. Google ML Drift (LiteRT GPU engine open-sourced; TFLite GPU delegate frozen) — **B+**
9. Microsoft MAI-Image-2.6 / Flash in Foundry — **C**
10. RacerGS (3D Gaussian splatting compression) — **B−**
11. FlexiAvatar (UNIST — 3D avatars from partial camera framings) — **A−**

---

## 1. Liquid AI LFM3 — a 2B-class family that now includes decision models

**Source:** liquid.ai blog, "LFM3" (published 27 Oct 2026, updated 5 Nov 2026), read in full (541 lines). **Grade B** — open weights and model cards, extensive vendor-run benchmarks, no independent replication yet. Everything below is Liquid-reported unless noted.

### What it is

LFM3 is Liquid's third-generation foundation family, built around a tri-hybrid backbone: of 24 layers, 13 are gated short convolutions (kernel 7), 5 are sliding-window attention (256-token window), and only 6 are global attention. Head-wise gated attention, partial RoPE, sandwich normalisation, a 128K vocabulary. Pretrained on 22T tokens with a final 3.5T-token mid-training phase; context extends to 256K. The architecture itself was found by search over 14 device/backend combinations — the design brief was "fast on real hardware," not "biggest on a leaderboard."

Six ~2B models are derived from the LFM3-1.7B-Base:

- **LFM3-1.7B** (text), **LFM3-VL-2B** (vision-language), **LFM3-Audio-2B**, **LFM3-Omni-2B** (2.2B, all modalities),
- **d1-2B** and **d1-Omni-2B** — *decision* models (see below).

### The numbers that matter

Text model: average 49.37 across Liquid's suite vs Qwen3.5-9B at 47.24 and the previous LFM2.5-2.6B at 31.55 — i.e., a 1.7B claiming parity-or-better with a 9B on agentic/tool benchmarks (WebArena-Verified 38.42, AutomationBench 41.29, BFCL V4 71.39, IFEval 96.66). Honest weak spots, disclosed in the same post: long-context retrieval (RULER 128K: 65.56 vs Qwen3.5-4B's 84.63 and 9B's 87.11) and factual accuracy (AA-Omniscience accuracy 7.07 — though its non-hallucination score is 92.93, i.e. it abstains rather than inventing).

Post-training recipe: SFT on 1.75T tokens → mixed RL with a length penalty → **MOPD** (six specialist RL teachers distilled into one generalist) → agentic RL inside real harnesses (Hermes, Pi, OpenClaw are named). That last step matters to us: the model was RL-tuned *in the harness*, not just on transcripts of it.

On-device (llama.cpp, Q4_0, 32K context): fastest decode in its comparison set, 1.8–2.8× the next model; 128K-context KV cache is 1.6 GB vs Qwen3.5-4B's 4.3 GB and MiniCPM5-2B's 5.6 GB. On a B300 under SGLang BF16: 3.6B tokens/day at 1,024 concurrent requests; a 300,000-agent Enron-corpus demo is included as a serving proof. One external testimonial with real numbers: MacPaw reports 64% vs 48% task success against Qwen3.5-2B on 65 macOS agent tasks, 58% fewer tokens, and a stuck rate under 1% vs 15%.

VL-2B: 71.4 average over 62 benchmarks — statistically level with Gemma 4 12B (71.7) at 1.9B parameters — and the first LFM with video input. Its new vision encoder (164M params, 2.2× fewer FLOPs) matches the encoder of Qwen3.5-2B (55.9% average across 13 VLM benchmarks). Throughput claim: >12,000 tok/s on a B300.

Audio-2B: English WER 6.2, multilingual average 6.0; TTS UTMOSv2 3.8 with output WER 1.4; VoiceBench 73.1; tool-calling 58.5 (internal eval); MMAR 50.6. The architecturally interesting part: the audio encoder is **fully causal** — it prefills while you are still speaking, giving time-to-first-token as low as 50 ms. Their LiquidCodec represents 80 ms of speech in 12 tokens and runs ~87× real time on a single M4 Max CPU thread. 18 languages.

Omni-2B: Daily-Omni 70.1, WorldSense 47.1, EmbSpatial 67.6, RealWorldQA 64.7.

### The decision models — the part that maps hardest to us

d1-2B and d1-Omni-2B do not chat. They answer *typed* questions with calibrated probabilities, all questions in **one forward pass**:

- Yes/No, Choice, Score (the d1-1.x line we already know),
- **Point** (new: bounding box / count answers),
- **Read** (new: span extraction with an explicit "not found"),
- **Estimate** (new: a number plus a range),
- **Pick** (new: multi-select with a per-option probability).

d1-2B beats its own bigger sibling: Decision Bench 85.2 vs d1-3B's 83.6; Decision Index 51.1 vs 49.0; ImajevBench 75.5 vs 64.0; meta index 63.2 vs 58.8. d1-Omni-2B shows a spoken-vs-written gap worth noting (DecisionBench 78.2 spoken vs 83.4 written; Typed Decisions 48.0 vs 50.5) but *reverses* it on JevBench (89.0 spoken vs 87.6 written); ESC-50 84.5%, FLEURS language ID 92.5% across 43 languages.

Two applied demos: (a) a wind-turbine defect classifier fine-tuned from ~3,000 photos with SFT+GRPO in a few hours on one A100 — classification went from <10% to 67%, detection F1 0.003→0.11 (vs GPT-6 Luna's 0.01) on ~1,400 held-out images; (b) robotics — an orchestration LoRA (rank 32, ~40k samples, ~6 GPU-hours on one MI325X) where a fine-tuned d1-2B acting as *skill monitor* doubles recovery success under disturbances; a navigation variant emitting 5 tokens per decision (2 spatial/control + 3 RQ codes → a 10-waypoint path; 2,068 vocabulary tokens repurposed; 2.8M samples / 72 GPU-hours) scoring R2R 53% / RxR 43% unseen and running at **>2.5 Hz on a Jetson AGX Orin under TensorRT FP16**; and a VLA variant using parallel action prediction (the OpenVLA-OFT/StarVLA-α pattern: 8 action-query tokens produce an 8-step action chunk in one pass), one generalist checkpoint across 15 embodiments (170 GPU-hours), LIBERO 96.2% average, RoboCasa-GR1 45.7%, action chunks in **<50 ms on a Jetson AGX Orin** under TensorRT FP16.

### Fleet mapping

- **Decision models / governor / Jacquard:** This is the second independent confirmation (after item 2) that "a model that answers many typed questions in one pass, with probabilities, and never generates prose" is now a *product category*, not our private pattern. d1-2B at 2B is the on-device end of that category: it would run on the Orin, let alone the Thor. Under Jacquard's standing rule — decision models sit behind a provider interface, advisor readings only, never the gate — d1-2B is a candidate provider for exactly the slots Jev currently fills, at zero marginal cost and with no network dependency. **Not** a reason to change anything today: Jev is wired, d1's numbers are vendor-run, and the swap test belongs to the same sealed held-out discipline as everything else in the FIX class.
- **Radio-room / presence voice:** Audio-2B's fully causal encoder (prefill-while-speaking, 50 ms TTFT) plus a codec that runs 87× real time on one CPU thread is precisely the shape our voice pipeline wants — the radio room's measured bottleneck was never the brain, it was turn latency. **Constraint, stated plainly: LFM3-Audio is research-only for us. Casey ruled on 2026-11-01 against downloading Apriel-Voice-27B to the Thor on space/priority grounds, and the LFM3-Audio download is a standing open item that is Casey's decision. Nothing was downloaded; this section is a map, not a fetch.**
- **Edge serving (Thor/Orin):** the KV-cache arithmetic (1.6 GB at 128K) and the Orin robotics numbers (>2.5 Hz navigation decisions, <50 ms VLA chunks, both TensorRT FP16) are the useful kind of vendor number — they tell us the 2B class is comfortably inside our hardware envelope, which de-risks any future "small model on the Orin as front-room brain" design.
- **Craftmind league:** the skill-monitor result (a small decision model watching a policy and doubling disturbance recovery) rhymes with our cameraman/guard pattern — a cheap watcher whose only job is typed judgements about an ongoing run. Our guards are currently scripted assertions; a learned monitor is a later option, not a current need.
- **Rolling perception / telltape:** no honest mapping beyond the general one — a 2B omni model is another possible *consumer* of a perception stream, not a contribution to the stream itself.

### Verdict

**B.** The family is real, open, and unusually honestly benchmarked for a launch post (weak spots disclosed in-line). The strategic fact is the d1 line: Liquid is productising the exact "state once, answer everything, with probabilities" pattern our governor and Jev rack already embody — at 2B, on-device, with typed Point/Read/Estimate/Pick answers we don't currently have. Park as: *candidate decision-provider, revisit when a sealed comparison against Jev is worth the lane time; audio model research-only pending Casey's word.*

---

## 2. d3-ultra — vLLM Semantic Router's 27B decision model, benchmarked against Jev in public

**Source:** MarkTechPost, "vLLM Semantic Router Releases D3-Ultra" (26 Oct 2026), read in full, cross-checked against the vLLM recipe details quoted in it. **Grade B−** — weights are open (Apache-2.0) and a free API exists, so the artefact is inspectable; but **every benchmark number is self-reported on the vendor's own private test sets**, a caveat the article itself flags. Treat the scores as claims awaiting a neutral run — including ours.

### What it is

A 26.09B-parameter dense multimodal model (including a 0.46B vision encoder), Qwen3.5-architecture backbone — 64 layers, 48 linear-attention and 16 full-attention — with a 131,072-token context *per question*. Like Jev and d1, it never generates text: you "state once" (present the input a single time) and it returns a probability for every answer to every question you posed. Question types: Choice, Yes/No, Score, Box, Track.

Two hard edges worth knowing: a Box question always returns exactly one box plus a confidence (≈0 means "target absent" — absence is expressed as low confidence, not as a null), and inputs over 131,072 tokens **hard-fail** rather than silently truncating. The second is a doctrine we recognise: fail loud, never degrade silently.

### The numbers

On **SR-Text** (in-house: 10,411 requests, 73,495 questions, chance-corrected so 0 = chance and 100 = perfect):

| Model | SR-Text |
|---|---|
| **d3-ultra** | **87.2** |
| GLiDE V1.2 | 85.1 |
| d1-ultra | 83.4 |
| d3-turbo | 83.1 |
| d3 | 81.4 |
| **Jev 1.14** | **73.1** |

Tools/automation is d3-ultra's best area (97.8). On arts/human taste, d1-ultra (90.8) edges d3-ultra (89.6) — a reminder that "decision quality" is not one number.

On **SR-Box** (5,678 questions, 4,984 images, 10 domains, IoU ≥ 0.5): d3-ultra 58.2% across 10 domains, 54.6% across the 9-domain subset (the figure the launch material leads with as its "worst case"); d3-turbo is actually stronger on boxes overall (60.0 / 59.6 — turbo leads on natural images, ultra on charts); **Jev scores 45.7 / 46.9**.

Latency (1× AMD MI325X, BF16): one question on a photo = 304 ms; 255 questions on the same input = 2.16 s total, i.e. **≈7.3 ms marginal cost per additional question**. That marginal-cost curve is the whole economic argument for the category: perception is paid once, judgement is nearly free per question.

Deployment: Transformers (transformers==5.17.0, `trust_remote_code=True`, optional flash-linear-attention), `vllm-sr serve` (PR #5449, merged 25 Oct 2026), a free hosted API at decision.vllm-sr.ai, and an HF Space. The wider "Decision 3.0" family spans 0.6B–27B. Comparison points from the article's table: Jev — 262,144 context, hosted/proprietary, $0.042/M input tokens; GLiDE — Fastino Community License, $0.04/M; d1-ultra — hosted only, $0.042/M. Public index scores (different index versions, not directly commensurable): GLiDE 71.5 (Decision Index 0.4.1), d3-turbo 70.2 (Jev DI, vendor estimate), d1-ultra 65 (AA), Jev 57 (AA).

Caveats: tested on MI325X only; no official quantised variant yet (at BF16, 26B ≈ 52 GB+ before KV cache).

### Fleet mapping

- **Governor + Jev-advisor pattern — the direct hit.** This is the first time our house pattern (Jev rack on the Thor at :8077, advisor readings behind a provider interface, never the gate) has a public, open-weight, Apache-2.0 counterpart benchmarked head-to-head against Jev itself — and on the vendor's own sets Jev 1.14 trails by 14 points on text and ~12 points on boxes. That does **not** dethrone Jev in our stack: the sets are private, the runs are the vendor's, and our doctrine is that swaps require evidence-dominant results on *sealed held-out* data we control. What it does do is give us, for the first time, a concrete candidate for that sealed comparison — one that fits the Thor (122 GB unified memory swallows 52 GB of BF16 weights; the Orin at 8–64 GB does not, absent a quantised variant).
- **Rolling perception / telltape:** the "state once, ask everything" economics (≈7.3 ms per extra question after a 304 ms state) is the same shape as telltape's premise — pay for perception once, let many cheap judgements ride on it. d3-ultra's Box-with-confidence (absence = ≈0, never null) is a clean convention worth stealing for our own typed-answer surfaces regardless of which model sits behind them.
- **Jacquard:** a second provider candidate for the decision interface, strengthening the interface itself: with Jev, d1, GLiDE and now d3 all behind the same typed-question shape, the provider interface is validated by the market, and our "advisor, never gate" rule is the differentiator, not the plumbing.
- **Craftmind league:** no direct mapping today. A 27B box/score judge is conceivable as an offline film-study tool (the curator line), but our measured result stands: JEPA-style embeddings over footage measured the camera, not the citizen — any vision-judge trial inherits that warning and the "subtract the observer first" requirement.
- **Foundry / radio-room / weight-space line:** no honest mapping.

### Verdict

**B−.** Open weights + free API + an honest self-caveat about private benchmarks. Park as: *the named candidate for a future sealed A/B against Jev 1.14 on our own question sets; until that run exists, the 87.2-vs-73.1 gap is a vendor claim, not a finding.*

---

## 3. VLA models measured on Jetson — the first public per-call table for our exact boards

**Source:** NVIDIA Developer Forums post by ZETIC (28 Oct 2026) with a public dashboard (ixian.zetic.ai) and full methodology disclosed in-thread. **Grade B+** — public dashboard, complete methodology, honest conflict disclosure (ZETIC sells inference optimisation; their optimised builds are separately labelled and excluded from fastest-path comparisons). Not A: vendor-adjacent, single source, and **TensorRT rows are not yet measured** (promised; ZETIC replied 6 Nov 2026 that they are coming).

### Method (why the numbers are usable)

Boards: AGX Thor devkit (128 GB), AGX Orin (64 GB), Orin Nano Super (8 GB). JetPack 7.2.1 / L4T R39.2.1, CUDA 13.2.2, PyTorch 2.14.1+cu130 aarch64. Power modes MAXN (Thor / AGX Orin) and MAXN_SUPER (Nano); `jetson_clocks` pinned (Thor GPU 1575 MHz, AGX Orin 1300 MHz). BF16, batch 1. Backends: PyTorch eager and torch.compile (Inductor, reduce-overhead). Metrics are **per policy call**, end-to-end (preprocessing → postprocessing): p50/p90 latency; energy per inference (average board power × duration ÷ count, tegrastats over a ~60 s steady window); peak memory above idle *including model load*; average power; and task success on each model's own suite. The authors state explicitly this is "not a ranking" — success setups differ per model — and rows are not physical-robot validation unless a row says so.

Models in the starting set: π0.5 (lerobot/pi05_libero_base), GR00T N1.7, GR00T N1.6 G1 PnP, SmolVLA (lerobot/smolvla_libero), RLDX-1, Cosmos3 Edge Policy DROID.

### AGX Thor, BF16, batch 1 — the table

| Model | Backend | p50 latency | Avg power | Energy / call | Peak memory |
|---|---|---|---|---|---|
| π0.5 | eager | 254 ms | 68.2 W | 16.74 J | 12.4 GB |
| π0.5 | torch.compile | 132 ms | 86.5 W | 11.31 J | 11.9 GB |
| SmolVLA | eager | 197 ms | 43.4 W | 8.58 J | 4.22 GB |
| SmolVLA | torch.compile | 50 ms | 66.9 W | 3.35 J | 6.76 GB |
| GR00T N1.7 | eager | 109 ms | 65.5 W | 7.11 J | 15.6 GB |

Cross-board anchor: π0.5 on AGX Orin runs 949 ms eager / 394 ms compiled (28.6 W / 43.5 W) — roughly 3–4× slower than the Thor, at roughly half the power.

### Findings that generalise

1. **torch.compile trades power for energy.** Compilation *raises* sustained board power (SmolVLA 43.4 → 66.9 W; π0.5 68.2 → 86.5 W) while *lowering* energy per call (8.58 → 3.35 J; 16.74 → 11.31 J). Thermal design and battery budget therefore pull in opposite directions: a passively cooled or thermally capped deployment may prefer eager even though each call costs more joules.
2. **Compilation can cost memory.** SmolVLA's peak rose 4.22 → 6.76 GB under compile. On an 8 GB Orin Nano that delta is the difference between fitting and not fitting — backend choice is a memory decision, not just a speed decision.
3. **The TensorRT gap is large and quantified.** An NVIDIA moderator (AastaLLL) in-thread: π0.5 under TensorRT FP8+NVFP4 = **49 ms** (vs 132 ms compiled, 254 ms eager on Thor); GR00T TensorRT deployment ≈ 28 Hz. So the table above is a *floor* for these models on our hardware, not a ceiling — any capacity plan drawn from it should carry a "TensorRT not yet applied" margin of roughly 2.5–5× on latency for the models that have a TRT path.
4. Small models are startlingly cheap: SmolVLA compiled is a 50 ms, 3.35 J policy call. A policy-call budget for a hypothetical Thor-resident actor is not the constraint; perception and judgement cadence are (which is the rolling-perception thesis arriving from the robotics side).

### Fleet mapping

- **Thor/Orin edge serving — direct.** This is our exact hardware, our exact JetPack (7.2.1 / R39.2.1), measured per-call with energy and memory — the first public table we can plan against without running the bench ourselves. Filed as the reference for any future VLA/policy work and for Thor power budgeting generally (a 65–87 W sustained draw under compiled inference is a number our thermal/power thinking should use).
- **Craftmind league / agent community:** indirect but real. If citizens ever get learned policy components (today they are scripted drivers over Mineflayer-class control), this table prices them: a SmolVLA-class call at 50 ms / 3.35 J is affordable at citizen cadence; a π0.5-class call at 132–254 ms is a "main character" cadence only — which is precisely Casey's rolling-perception allocation (main characters tap the stream many cycles per minute, peon-class workers far less). The table gives that doctrine numbers.
- **Cosmos line:** Cosmos3 Edge Policy DROID is in ZETIC's starting set — when its rows land, they will be the first independent-ish Thor numbers to set beside NVIDIA's own Cosmos 3 Edge claims (1.53 s per 32-action chunk at 15 Hz, from the D3D+Cosmos deep-dive). Watch item, not a task.
- **Rolling perception / telltape, Jacquard, foundry, radio-room, weight-space:** no honest mapping.

### Verdict

**B+.** Bookmark the dashboard; re-check when the TensorRT rows land. Until then, cite these numbers as "PyTorch eager/compile, BF16, batch 1, MAXN" — never as the boards' limits.

---

## 4. ESP32-P4 offline ASR — a real speech recogniser on a microcontroller, with a rule-book instead of an LM

**Source:** Open Source For You (28 Oct 2026), read in full. Project: **esp32-pie-asr** by Boumedine Billal, Apache-2.0; the repo ships the engine, firmware, eval scripts, benchmarks and flashing instructions. **Grade B** — open-source artefact with eval scripts anyone can rerun; all performance figures are developer-reported.

### What it is

The recogniser is **Kroko** (by Banafo), a 65.7M-parameter streaming ASR model. Original weights ~71 MB were compressed to **26.65 MB** by mixed 2-bit/4-bit quantisation. The weights live on a microSD card and load into the board's 32 MB PSRAM at startup. Inference runs on the ESP32-P4's dual RISC-V cores plus its PIE SIMD unit — no cloud, no separate accelerator, no NPU. Tested on Espressif's ESP32-P4X-Function-EV-Board (microphone, display, microSD, 32 MB PSRAM).

Performance: 1.28 s of audio processed in ~0.90 s (faster than real time); a spoken word is typically finalised ~2 s after it is spoken. **LibriSpeech test-clean WER 4.34%** with beam search over 4 hypotheses — a genuinely respectable number for a 65.7M model on a microcontroller.

The command layer is the design decision that matters: there is **no language model**. Commands are configurable word/phrase rules in editable text files on the microSD, including alternate spellings for recognition variants. Six demos (smart home, robot vacuum, car cabin, etc.); command success 94–99% with curated phrase lists; **zero false activations across 88 near-miss clips per demo**. English only for now; Arabic and the ESP32-S31 are stated future work.

### Fleet mapping

- **Confluence / presence — the honest mapping is a posture, not a component.** Our presence doctrine is fixed: a deliberately opened, visibly live session; the refusal of always-on ambient microphone perception does not move. A bounded phrase grammar with *zero measured near-miss false activations* is a different posture from ambient listening — it is a doorbell, not an ear. If a thin device ever needs a local "open a session" trigger, this is the shape it should take: on-device, phrase-bounded, no audio leaves the board, and the Thor remains the only mind. That is consonant with the Confluence product definition (device as IO; Thor as the only mind) rather than a violation of it.
- **Radio-room voice:** no direct mapping — the radio room is a *conversation* (open-vocabulary STT via faster-whisper), and Kroko's phrase lists are the opposite tool. The transferable lesson is the quantisation result: mixed 2/4-bit took a usable ASR model to 26.65 MB at 4.34% WER — evidence that our edge STT components have more headroom than their default precisions suggest.
- **Citizens / league, Jacquard, foundry, weight-space, telltape:** no honest mapping.

### Verdict

**B.** A small, complete, inspectable artefact. Park as: *the reference design if a presence device ever needs a local wake/trigger layer — phrase-bounded, offline, zero-false-activation measured — under the standing rule that ambient listening stays refused.*

---

## 5. SpAItial Echo-3 — capture is becoming a commodity; accuracy claims are absent

**Source:** Startup Fortune (28 Oct 2026), secondary coverage citing Radiance Fields and Runtime Wire. Product released 27 Oct 2026. **Grade C** — a real, downloadable product (demo class), with **no accuracy metrics anywhere in the coverage**: no PSNR, no geometric error, no comparison against a measured ground truth. Everything about quality is currently the company's framing.

### What it is

Echo-3 is an iPhone app (iOS 18+, any modern iPhone) that turns a short phone video into a photorealistic, **metric-scale** 3D Gaussian splat / point cloud / mesh. On LiDAR-equipped Pro models it adds live coverage guidance and a denser scan preview. Free to download; scan processing draws credits; subscription plans include a free first month; Android "coming." An API accepts photos/video and returns a 3D world.

The company: SpAItial, CEO Matthias Niessner (TUM professor on leave; Synthesia co-founder), $13M seed (May 2025), working on "Spatial Foundation Models" spanning geometry, physics and materials. Lineage: Echo (3D generation from text/image) → Echo-2 (spring 2026, real-time 3DGS generation in the browser) → Echo-3, a pivot from *generating* worlds to *capturing* them. Their framing, which is a genuinely useful distinction: reconstruction as "conditional generation" — the opposite bet from Genie 3. Genie invents a world; Echo-3 digitises the one that exists.

### Fleet mapping

- **Foundry / 3D line:** the mapping is competitive context, not technology. Our foundry doctrine is *seed + params are the asset; geometry is a cache* — assets are born parametric and regenerable. Echo-3 is the opposite pole: geometry captured from the world, no recipe. The two meet in exactly one place — **reference**. A metric-scale scan of a real harbour building or boat interior is a better ground truth for a parametric archetype than a photograph. If capture is this cheap, "mint a foundry archetype from a scanned reference" becomes a plausible workflow; the scan is the evidence, the seed stays the asset.
- **SculptForge (batch 1):** same note as batch 1's Gaussian thread — generation-side tools (SculptForge, L3G-World) and capture-side tools (Echo-3) are converging on the same representations (3DGS) from opposite directions. See the synthesis: the Gaussian line is now five items in a week.
- **League / citizens:** a scanned real place as a world seed is a nice thought and nothing more today — no artefact, no metrics, no API evaluation. Park it.
- **Everything else:** no honest mapping.

### Verdict

**C.** Real product, serious founder, zero published accuracy. Park as: *capture-side context for the foundry; revisit only if they publish geometric accuracy numbers or we have a specific real-place archetype to build.*

---

## 6. VoicePipe — performed temp dialogue for games; an announcement, not a technology disclosure

**Source:** itch.io devlog by CanicaAzul (27 Oct 2026), read in full (it is short). **Grade C−** — the tool is downloadable (demo class), but the devlog names **no engine, no model, no pricing, and includes no audio samples**. What is being sold is a workflow claim, and the workflow claim is the only thing that can be evaluated.

### What it is

VoicePipe takes a script in and returns performed dialogue audio: it casts characters (assigns a voice per character, swappable), directs every line (emotion, pace, emphasis and pauses follow the scene), and renders files ready to drop into a build, a review or a playtest. It integrates with Wwise (audio middleware) and Arcweave (narrative design). The audience is game teams who need *temp* dialogue — for playtests, pitches, vertical slices — and narrative designers who want to hear a scene before booking a recording session. Its own positioning is explicit and creditable: "VoicePipe doesn't replace actors. It makes a scene playable and reviewable before the real record."

### Fleet mapping

- **Radio-room / voice dressing:** the overlap is the *direction* layer, not synthesis. Our radio room already separates brain → TTS → dressing (bandpass, squelch, static) and the citizens' voice layer separates intent-declared narration from the actor. VoicePipe's cast/direct/render split is the commercial version of the same separation, aimed at a different problem (temp tracks for human games). Nothing to adopt; one thing to note: "directs every line from the scene" is a claim about *prosody from context*, which is exactly the layer our citizen narration currently gets from templates and triples callbacks. If a tool like this ever publishes how it directs, that page is worth reading. This devlog doesn't.
- **Craftmind league:** citizens' chat narration is text-first by design (it is read in world chat and in the curator's manifest); performed audio for citizens is not a current requirement. No honest mapping beyond the voice-layer note above.
- **Everything else:** no honest mapping.

### Verdict

**C−.** Park as: *workflow-shaped, technically opaque; the honest temp-dialogue positioning is noted, and there is nothing here to build on until an engine/model or samples are public.*

---

## 7. Skill∞ — the optimiser is itself a skill, and it rewrites itself (arXiv 2610.35434)

**Identification:** the bare arXiv link resolves to *"Skill∞: Recursive Self-Improvement for Agent Skill Optimization"* — Tao, Yan, Wu, Wong; submitted 26 Oct 2026; CC BY 4.0. **Grade A−** — arXiv paper with a public benchmark evaluation; **read at abstract level this pass** (code not inspected), which is why it is A− and not A.

### What it claims

Prior skill-optimisation methods split into two camps: hand-designed optimisation procedures (a human writes the loop that improves skills), or a meta-skill confined to a fixed pipeline and relearned per task. Skill∞ removes both limits: a **meta agent follows a meta-skill** — a skill whose content is the optimisation procedure itself (diagnose execution traces, propose candidate revisions, request independent reviews, allocate the search budget) — **and optimises the meta-skill with the same procedure it uses on task skills**. The optimiser is itself a skill, so self-improvement can rewrite the improvement process, not just its outputs.

Design points: the meta-skill is *decoupled* from task skills, refined *across* multiple skill-optimisation tasks, and *reused* across domains; skills at both levels are standard packages loaded through native skill discovery (i.e., the same skill-file mechanism agent harnesses already have — no new infrastructure).

Results on 83 SkillsBench tasks: **60.7% pass with Skill∞ vs 56.4% for human-curated skills vs 54.5% for SkillEvolver**. The headline comparison is the first gap: a self-improving optimiser beat the human-curated baseline by 4.3 points.

### Fleet mapping

- **Our own skill files — the direct hit.** This workspace runs on exactly the substrate Skill∞ assumes: skill packages (system skills, custom skills, lane playbooks) loaded by native discovery, revised by hand when a lesson is learned (AGENTS.md's lessons section is a manual version of this loop). Skill∞ is evidence that the loop can be mechanised — trace diagnosis, candidate proposal, *independent review*, budget allocation — and that the mechanised version can edge out careful human curation on a broad bench. The fleet-relevant detail is the independent-review step inside the loop: it is our "verify by an agent that didn't write it" discipline, internalised by the optimiser.
- **Craftmind league / citizens:** citizens' skill graduation (behaviours that prove out in the world graduate from scratch-pad to standing procedure — Casey's frame-to-weights doctrine in league clothes) is the same shape at a smaller scale: triples record situation → plan → verified outcome, and routines are designed to fade as competence is proven. Skill∞ suggests the graduation *procedure itself* is a learnable artefact, not a fixed harness. Not actionable this week — our citizens' bottleneck is bodies and food margins, not skill-file quality — but it names the direction the triples library grows in.
- **Jacquard:** the resonance is structural — Jacquard already treats approval history as something that compiles into standing rules (charter-scoped auto-allow, 2026-11-05 ruling). A meta-skill that allocates its own search budget under review is a cousin of the batched decision queue: bounded autonomy with an audit trail. No change implied.
- **Weight-space line:** a skill file is a behaviour-deployment instrument in text; Skill∞'s result (optimising the text artefact beats curating it) sits comfortably beside the weight-space line's finding that authored patches deploy behaviour without adding capability. Both say: the artefact you edit is a legitimate control surface.
- **Everything else:** no honest mapping.

### Verdict

**A−** (abstract-level read; full-text + code inspection would be needed to move it). Park as: *the reference point for any future "who improves the playbooks" design — for the fleet's skills and for citizen graduation alike. The +4.3 over human curation is a benchmark claim from one paper; treat as promising, not proven here.*

---

## 8. ML Drift — Google open-sources its production GPU inference engine; the TFLite GPU delegate is frozen

**Source:** TechTimes (26 Oct 2026), read with the scepticism the brief demanded — the headline is indeed garbled. Cross-referenced against the InfoQ report (25 Oct 2026) the article draws on. **Grade B+** — the artefact is real and verifiable (open-source release with a production history inside Google's own apps); the performance comparisons are Google's own, via InfoQ, with no independent validation, and one acknowledged gap (no Core ML head-to-head exists).

### What the artefact actually is

Strip the headline down to the verifiable claim: **Google has open-sourced ML Drift — the GPU inference engine it runs in production inside YouTube Shorts, Google Photos, Chrome and Meet — as the GPU accelerator for LiteRT** (the renamed TFLite runtime), under **Apache-2.0 with a patent grant**. Simultaneously, **the legacy TFLite GPU delegate receives no new features**: frozen, kept backward-compatible, not removed. So "TFLite GPU delegate ends" (headline) really means "the delegate is end-of-life for new work; ML Drift is the successor path."

The core technology is **tensor virtualization**: a logical tensor is decoupled from its physical allocation, and shader templates resolve the coordinate mappings at compiler initialisation. That yields one unified shader per operation for every backend, authored in **UCL** (Unified Compute Language) sitting above GLSL/MSL/WGSL. It also removes the legacy delegate's hardcoded 4D-tensor limit — 5D spatiotemporal models (YOLO 11n, MobileViT v2, Swin V2 are named) become expressible. For LLM inference there are phase-aware kernels (prefill is compute-bound, decode is bandwidth-bound; they get different kernel configurations), a convolution-aligned KV cache in OHWI layout, and in-kernel activation quantisation. Memory: greedy-by-size buffer reuse takes Stable Diffusion 1.4's peak GPU memory from **4.31 GB to 387 MB (−93%)** — Google-reported.

Production numbers (all Google-reported): Shorts segmentation effects up to 40% lower average frame latency across Android+iOS; Photos Unblur up to 2 s faster than the legacy delegate; Chrome's Gemini Nano Built-In AI APIs (Prompt / Summarize / Writer) already run on ML Drift; Adobe Lightroom/Photoshop features up to 30% faster; Snap via LiteRT reports 30% lower latency and larger diffusion models enabled. Hardware co-optimisation with Arm (Mali/Immortalis), Intel (WebGPU path + Xe XMX) and Qualcomm (Adreno OpenCL). Desktop runs via Dawn/WebGPU (Windows D3D12, Linux Vulkan) as a "desktop preview"; macOS is native Metal. The release ships an "agentic coding guide" so AI coding agents can author, register and verify custom shaders — a small but telling sign of who Google expects to write inference code now. Versus llama.cpp/MLX LM: up to 12% lower memory overhead on Gemma workstation tests (Google's own benchmarks).

*Read note: this pass covered the article's substance (lines 0–160 of 222); the remainder is migration planning. A re-fetch of the tail failed and was not retried; nothing in the first 160 lines suggests the tail changes the artefact's identity or terms.*

### Fleet mapping

- **Edge serving / Confluence thin devices:** the actionable fact is a platform direction, not a benchmark: **for Android GPU inference, LiteRT + ML Drift is now the path, and the old TFLite GPU delegate is frozen.** Any future fleet Android work (a phone as Confluence IO running anything locally — wake layer, camera preprocessing) should target ML Drift from the start rather than inheriting delegate-era code.
- **Rolling perception:** the phase-aware kernel split (different configs for prefill vs decode because the bottleneck differs) rhymes with our own measured result that rolling perception and batched perception are different workloads with different winners. Same lesson, silicon level: *name the phase before you tune.*
- **Thor/Orin serving:** no direct mapping — our Jetson stack is CUDA/TensorRT, not LiteRT. The tensor-virtualization idea (one logical tensor, physical layout resolved at compile time) is noted as a design pattern, nothing more.
- **Everything else:** no honest mapping.

### Verdict

**B+.** A real artefact with a real production history; performance deltas are vendor-reported. Park as: *platform-direction fact for any Android edge work (ML Drift, not the frozen delegate), plus a memory figure (−93% peak on SD 1.4) that is worth remembering as a claim to test if we ever run diffusion on a phone-class GPU.*

---

## 9. MAI-Image-2.6 — Microsoft's image models go GA in Foundry, with honest two-tier pricing

**Source:** Superpower Daily post on the Foundry GA (27 Oct 2026); both models had been on Vercel AI Gateway since 13 Oct 2026. **Grade C** — pricing and availability are factual and checkable; capability claims are vendor positioning with a single testimonial that describes "potential rather than a completed rollout" (Minute, the Sports Illustrated publisher, early tests). Adobe Firefly availability is announced with no date.

### What shipped

MAI-Image-2.6 and MAI-Image-2.6-Flash moved out of preview in Microsoft Foundry. Features: editing with up to **5 reference images** (product/character/brand preservation), Bing web grounding (Microsoft itself notes this is not a substitute for reviewing output), dynamic aspect ratios, output up to 1.5K.

**Pricing, per million tokens, starting prices:**

| | Text input | Image input | Image output |
|---|---|---|---|
| MAI-Image-2.6 | $5 | $8 | **$38** |
| MAI-Image-2.6-Flash | $1.75 | $2.50 | **$19** |

Flash's output price is exactly half the flagship's. Microsoft's suggested workflow is the interesting line: **Flash explores and revises; the flagship produces finals.**

### Fleet mapping

- **Image-studio economics — the only mapping, and it is a reference price, not a candidate.** Our incumbent is local SDXL on the Thor (hash-verified, ~11.8 s warm at 1024×1024, marginal cost ≈ electricity). MAI's $38/M output tokens gives us a cloud reference price for the flagship tier and, more usefully, validates the two-tier shape we already practise: cheap/fast exploration, expensive finals — except ours is local/local (SDXL drafts and finals at different step counts) rather than cloud/cloud. The 5-reference-image editing is the one capability with no local equivalent in the studio today; if a future job needs reference-locked product/character edits beyond what our ControlNet stack does, this is the priced fallback. **Standing rule applies: don't spend his money — the paid route is the fallback after the paid-for/local route is exhausted, not the default.**
- **Foundry (3D):** name collision only — Microsoft Foundry is not our foundry. No mapping.
- **Everything else:** no honest mapping.

### Verdict

**C.** Filed as a price reference card for image work: *flagship $38 / Flash $19 per million output tokens; two-tier explore-then-final workflow; 5-reference editing is the differentiator; local SDXL remains the default on cost and on principle.*

---

## 10. RacerGS — autoregressive context modelling compresses 3DGS by >150×

**Source:** GameDev.net news item (27 Oct 2026) summarising an arXiv cs.GR paper; **no artefact was linked from the news item and none was inspected this pass**. **Grade B−** — a paper exists behind the summary (A-class in principle), but this digestion rests on the news summary, and compression ratios are the paper's own experimental claims across five datasets.

### What it claims

3D Gaussian splatting scenes are large. RacerGS attacks the size with the standard codec playbook, modernised: compact **hash-projected context features**, and a **FiLM-modulated autoregressive GRU** that models causal dependencies between anchor feature groups, so that quantised anchor-attribute residuals can be entropy-coded against context-predicted means — predict well, and the residual stream is cheap to store. Reported results across five datasets: **>150× compression vs vanilla 3DGS and 28× vs Scaffold-GS, at comparable rendering quality.**

### Fleet mapping

- **Foundry / Gaussian line:** this is the *delivery* end of the Gaussian problem. The week's other Gaussian items attack capture (Echo-3), memory-bounded world representation (L3G-World, batch 1) and generation (SculptForge, batch 1). RacerGS attacks the file: a 150× smaller splat is the difference between "download a scene" and "stream a scene" — which is the Confluence shape (thin device, heavy world elsewhere) applied to 3D. If the foundry ever ships splat-based assets to a phone or browser, a codec in this family is the enabling layer; our parametric assets don't need it (the seed *is* the compression), which is itself the comparison worth keeping: **seed+params compresses by regeneration; RacerGS compresses by prediction. Both are bets that structure beats storage.**
- **Everything else:** no honest mapping.

### Verdict

**B−.** Park as: *the delivery-size reference for the Gaussian thread; artefact unverified — if splat delivery ever becomes a real requirement, read the paper and find the code before citing the 150×.*

---

## 11. FlexiAvatar — one avatar model for every camera framing, by pruning what the camera never saw

**Source:** Seoul Economic Daily (27 Oct 2026) reporting UNIST + University of Aberdeen work presented at **ECCV 2026** (Malmö, September); team led by Prof. Baek Seung-ryeol (UNIST Graduate School of AI); funded by NRF Korea / IITP / InnoCORE. **Grade A−** — a peer-reviewed conference paper with standard public benchmarks and stated caveats; this pass read the press coverage rather than the paper, hence the minus.

### The problem and the method

Avatar systems assume the full body is in frame. Real cameras disagree: video calls and broadcasts show upper bodies and faces, and models trained for full-body hallucinate unseen limbs and distort the visible face and torso; the previous fix was a separate model per framing. FlexiAvatar builds on SMPL-X + 3D Gaussian splatting with **visibility-based optimization**: compute each Gaussian's *observation frequency*; exclude under-observed Gaussians from training and rendering; filter position errors from occluded joints (posture correction); refine face and both hands separately; and fill never-seen regions (back, back of head) with generative-AI auxiliary full-rotation footage that is **weighted below real footage** — synthetic evidence is admitted, but at a discount. That weighting rule is the most quotable design decision in the paper's coverage: exactly our provenance discipline (confirmed vs unconfirmed, receiver-confirmed vs pickup-reported) expressed in a training loss.

### Numbers

PSNR, best at every framing: NeuMan full-body **35.77 dB vs ExAvatar 34.80**; WildAvatar real full-body **30.98 vs ToMiE 28.65**; TalkShow upper-body 36.73; INSTA face-focused 33.04. Efficiency on the face-focused case: Gaussians 167,390 → 84,095; data 8.94 MB → 4.49 MB (**−49.8%**); rendering 29.18 → 39.15 fps (+~34%). **Stated caveat, to their credit: total production time and GPU memory did *not* fall by the same proportion.** Loose clothing is named future work.

### Fleet mapping

- **Foundry / 3D line:** the visibility-pruning result (−49.8% data, +34% fps, quality *up*) is a general 3DGS hygiene technique, not avatar-specific: any splat asset we generate or capture carries Gaussians the working camera never meaningfully observes, and observation-frequency pruning is a cheap post-pass with measured upside. Noted for the foundry shelf.
- **Curator / perception:** the deeper rhyme is epistemic. FlexiAvatar's core move — *track how often each element was actually observed, and discount or exclude the rest* — is the Watcher's Charter instinct inside a renderer, and the same correction our JEPA-over-play spike forced (the embedding stream measured the filming apparatus first). "Weight by observation, discount the synthetic" is a fleet-wide principle; this paper is a clean external instance of it.
- **League / citizens, radio-room, Jacquard, weight-space, telltape:** no honest mapping.

### Verdict

**A−.** Park as: *visibility-based pruning is a candidate post-pass for any future splat work; the synthetic-at-a-discount weighting is filed as an external witness for our provenance rules.*

---

## Synthesis — what batch 2 changes, taken together

**1. The decision-model category is now a market, and we were early to its shape.** Two of the eleven items (LFM3's d1 line, d3-ultra) are the same architectural idea our governor and Jev rack already run: state the input once, answer many typed questions in one pass, return probabilities, never generate prose. d3-ultra's marginal economics (≈7.3 ms per additional question after a 304 ms state) are the category's whole argument in one number, and Liquid's d1-2B proves the idea now runs at 2B on-device — navigation decisions at >2.5 Hz and VLA chunks at <50 ms on a Jetson AGX Orin. Three consequences for us: (a) the provider interface behind Jacquard is validated — Jev, d1, GLiDE and d3 all fit it; (b) Jev now has named, open-weight challengers (d3-ultra Apache-2.0 at 27B; d1-2B at 2B), so a future sealed A/B on our own question sets is *possible* in a way it wasn't last month; (c) nothing changes today — our rule (advisor readings only, never the gate; swaps on sealed held-out evidence, not vendor tables) is precisely the discipline that keeps a vendor's private-benchmark 14-point lead from becoming our architecture decision.

**2. The Gaussian thread is now five items in a week, and its open problems have moved.** Batch 1 brought L3G-World (latent Gaussian *memory* for world models) and SculptForge (generation). Batch 2 adds Echo-3 (capture, commoditised by a phone app), RacerGS (delivery, 150× compression) and FlexiAvatar (hygiene, visibility pruning at −49.8% size). Capture is effectively solved commercially; generation is crowded; the unsolved, valuable ground is what it was in batch 1 — *memory-bounded representation* (how a world model keeps a Gaussian scene in bounded memory) and now *delivery* (how a scene reaches a thin device). Both are Confluence-shaped problems. Our foundry's seed+params doctrine remains the contrarian and, for generated assets, still the strongest position: regeneration is the ultimate compression. The Gaussian line matters to us where the world is *captured or remembered*, not where it is *authored*.

**3. The edge numbers are getting real, and they keep confirming the fleet's allocation doctrine.** ZETIC's table prices policy calls on our exact boards (SmolVLA 50 ms / 3.35 J compiled; π0.5 132 ms / 11.31 J; TensorRT still to come at ~49 ms for π0.5). Liquid prices decision calls on the same silicon class. ESP32-P4 prices a bounded voice trigger at 26.65 MB and zero measured false activations. In every case the cheap, frequent, typed judgement is affordable and the expensive, general call is the rationed one — main characters tap often, workers tap rarely — which is the rolling-perception allocation Casey set, arriving independently from robotics, decision models and microcontrollers in a single week.

**4. Verification keeps relocating — this batch's quiet theme.** FlexiAvatar weights evidence by how often it was actually observed and discounts synthetic footage. d3-ultra expresses absence as ≈0 confidence instead of a null and hard-fails on over-length input instead of truncating. Skill∞ puts independent review *inside* the optimisation loop. ESP32-P4's command layer gets zero false activations by refusing open vocabulary. Different fields, same move: **make the unreliable thing structurally hard to express, and make the reliable thing carry its provenance.** That is the Watcher's Charter and the receiver-confirmation rule stated in other people's engineering — useful confirmation that the fleet's verification instincts are converging with the field's, not drifting from it.

**5. Platform directions worth one line each.** LiteRT's GPU future is ML Drift; the TFLite GPU delegate is frozen (any Android edge work starts on Drift). Image generation's cloud reference price is now $38/M output tokens flagship / $19 Flash, with a vendor-endorsed explore-on-Flash/final-on-flagship split that mirrors our local-first economics. Neither requires action; both belong on the shelf so a future design doesn't rediscover them.

## Shortlist

**Act on (cheap, high value):**
- File ZETIC's Jetson table as the fleet's VLA/policy-call reference (done — item 3 above); re-check the dashboard when TensorRT rows land.
- Steal d3-ultra's two conventions for our own typed-answer surfaces, independent of any model swap: absence as low confidence (never null), and hard-fail over silent truncation.

**Candidate, gated on our own evidence:**
- d3-ultra (or d1-2B at the small end) as a *named candidate* for a sealed held-out A/B against Jev 1.14 — to be run only when a lane has the time to do it properly; vendor numbers (87.2 vs 73.1) are the hypothesis, not the result.
- Visibility-based Gaussian pruning as a post-pass, if splat assets enter the foundry pipeline.

**Research-only / parked by standing decision:**
- LFM3-Audio-2B — mapped to radio-room/presence (causal encoder, 50 ms TTFT, 87×-real-time codec), **not downloaded; the download decision is Casey's and remains open**.
- ESP32-P4 Kroko — parked as the reference shape for any future presence wake/trigger layer (phrase-bounded, offline, zero false activations); ambient listening remains refused.
- Echo-3, VoicePipe, MAI-Image-2.6, RacerGS, Skill∞ — context and reference cards; no build implications this week.

**No honest mapping (stated, not forced):** VoicePipe beyond the voice-layer note; MAI-Image beyond pricing; ESP32-P4 beyond the presence-trigger posture; Skill∞ beyond skills/graduation design. Each item's section says so in place.

## Gaps in this batch (honest)

- Skill∞ was read at abstract level; its code was not inspected.
- RacerGS was read via the GameDev.net news summary of the paper; no artefact was linked or inspected.
- The ML Drift article was read for its substance (lines 0–160 of 222); the tail (migration planning) was not re-fetched after a failed fetch, and was not retried.
- All LFM3 and d3-ultra performance figures are vendor/self-reported, as flagged in their sections; the ZETIC table is a single (methodologically open) source; FlexiAvatar was read via press coverage of the ECCV paper, not the paper itself.

---

*Compiled 2026-11-08 from the sources cited in each section. Fleet mappings are this study's analysis; grades follow the house A/B/C/D scheme defined at the top. No downloads were made for this batch; no league or fleet system was touched.*
