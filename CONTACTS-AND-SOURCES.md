# Contacts and sources — who made what we read, where it lives, what we took, our standing verdict

*The "contacts" layer for the studies shelf, built 2026-11-08 under Casey's sharpened instruction (papers about everything, with good knowledge, contacts and searchability days later). One row per organisation, project, repo, author or recurring source across the 2026-11-07 night studies, the three 2026-11-08 batch deep-learns and the digestion docs. Deduplicated and alphabetised. "Standing verdict" is the fleet's current position — it changes only on new evidence, and the change gets appended, never silently rewritten. Study files are cited by short name; all live in `~/workspace/studies/` unless a fuller path is given.*

---

## A

**AGIBOT (GO-3)** — embodied-AI company; GO-3 preview announced via PRNewswire claiming top spots on three embodied benchmarks. *Where:* PRNewswire release (batch 1, §5). *What we took:* the model-lifecycle pattern (preview → benchmark → open) as the batch's example of announcement-shaped evidence. *Verdict:* **D+/C−.** Press release; claims unverified; parked.

**AgenSH — see Microsoft.**

**Allen Institute for AI (AllenAI) — OlmoEarth** — earth-observation foundation model programme. *Where:* huggingface.co/blog/allenai/olmoearth-v1-3; weights/data/code open; precomputed planetary embeddings on Source Cooperative; Explorer at olmoearth.allenai.org. *What we took:* the provenance-carrying embedding pattern (every value traces to its source scenes) and change-detection-by-embedding-delta, validated against MAAP monitoring; the SI-Marine shelf's first named external data layer. *Verdict:* **A-grade source.** The strongest-evidence item in batch 3; the standard other perception releases should be held to.

**AlphaEarth Foundations / Tessera** — Google DeepMind's and Cambridge's satellite embedding models, present in our reading only as OlmoEarth's named competitors (batch 3, §6). *Verdict:* reference points; not independently read.

**Altera — Project Sid** — 1,000+-agent Minecraft society (2024), the prior art YC's Civ50 is compared against. *Where:* cited in multi-agent-towns-20261107.md and the Civ50 addendum. *What we took:* the baseline claim that large-agent societies produce institutions; our addendum's verdict — Sid's institutions were substantially prompt-provided, Civ50's ration protocol was incident-born; the difference is the finding. *Verdict:* background canon for the towns thread; claims read with the provided-vs-emerged correction applied.

**Amazon Conservation — MAAP** — monitoring programme whose ground record validates OlmoEarth's mining-change maps (batch 3, §6). *Verdict:* an example of the independent store a verdict can be signed from.

**Anthropic** — the lab; in this shelf for "The components of agent memory" (anthropic.com/research), digested via the ZCode seat take. *Where:* digestion-anthropic-agent-memory-20261108.md; full take at Thor `~/craftmind-league/seat-takes/zcode-anthropic-memory-20261108.md`. *What we took:* the memory taxonomy (notes vs weights vs in-context vs compaction), dreaming/sleep-time consolidation, the salience results (413 files/1 badge vs 9 files/4 badges), the concurrent-writer fact-loss datum (16/57 lost vs 57/57 single-writer verbatim), and the finding that prescribed capture rules *reduced* the memory benefit for strong models. *Verdict:* **B+ source** — the take's thesis stands: our architecture matches its endorsed design; our gaps are in the verification layer.

**Apriel-Voice-27B (ServiceNow AI)** — open voice model (Whisper encoder + projector into a Gemma 4 backbone; synthesis external). *Where:* Hugging Face model card; batch 1, §16. *What we took:* proof the two-stage graft preserves the backbone's reasoning while the voice/dressing layer stays ours. *Verdict:* **B; architecture-only.** Casey's standing ruling (2026-11-01): **do not download to the Thor** — mapped, never queued.

**Aura Autopilot (Ramen)** — open-source autonomous game-testing harness (Unreal/Unity/Godot, BYO model). *Where:* BusinessWire launch release + whitepaper/repo; batch 1, §14. *What we took:* two findings — its decision model is **Jev via the TypeSafe SDK**, structured as frame (LLM-written harness) / triage (Jev macro-action picks) / reflexes, a shipping commercial instance of our advisor-behind-interface pattern; and the open tension with our cold-falsifier playtesting doctrine, resolved as two instruments (regression vs falsification). *Verdict:* **C+ release / B− whitepaper+repo.** The Jev sighting is the batch-1 item with the longest shadow.

## B

**BASALT (MineRL BASALT competition)** — the only verified build-a-house/pen evidence in the Minecraft-agents literature, episode-scoped with gifted inventory. *Where:* successful-agents-minecraft-20261107.md. *Verdict:* B-grade canon; the solvability-class decomposition is the steal.

**BitNet (Microsoft Research)** — the ternary (1.58-bit) pretraining line JiRack explicitly follows (batch 3, §11). *Verdict:* the legitimate ancestor; JiRack's claims inherit BitNet's plausibility, not its evidence.

**BlenderWorld** — benchmark for visual agents doing 3D creation in Blender (Zhejiang University, Alibaba Token Hub, CUHK; Fang, Wang, Yu et al.). *Where:* arXiv:2610.23986; github.com/QwenLM/BlenderWorld; blenderworld.github.io; batch 3, §8. *What we took:* the failure taxonomy (viewpoint inconsistency, ground contact, contact constraints, view-dependent shortcuts) and the VLM-as-Judge / Agent-as-Judge split — programmatic scene inspection as the verdict that renders can't game. Shortlist #1 of batch 3: adopt the shape for foundry verification. *Verdict:* **A−.** The external citation for the league's state-over-screenshots doctrine.

**Block — Dessa lab** — small AI research lab inside Block (Square), founded by former members of Dessa (the Toronto DL startup Block acquired); reports to Jack Dorsey. Lead: Ragavan Thurairatnam. *Where:* block.xyz/dessa; batch 3, §3. *What we took:* the speech-native existence proof — a full-duplex conversation model trained only on sound — as the voice thread's far pole. *Verdict:* **C+.** Curated demos only; no paper, no weights; horizon marker.

## C

**CMS Manhattan — JiRack** — Konstantin Grabko's company; three ternary LLM families (Precision, JiRack Ultra, JiRack DeltaNet). *Where:* HF org CMSManhattan (e.g. JiRackTernaryPrecision-16B-chat), Ollama (cmsmanhattan), github.com/cmsmanhattan/ROBOS, LinkedIn Pulse articles by Konstantin Grabko; batch 3, §11. *What we took:* the ternary-from-scratch answer to the substrate question our Q1 measurements posed; a named (unmeasured-on-Jetson) candidate for a CPU-only fallback tier. *Verdict:* **C+.** Real artefacts; all performance claims vendor-reported. **NOT our JEV rack, NOT Atlassian Jira** — namesake only; see the disambiguation note in INDEX.md.

**Cosmos 3 (NVIDIA)** — world-model family; the interactive-simulation checkpoints (Transfer/Sim lines) deep-dived with D3D. *Where:* full report at `~/workspace/research_notes/d3d-cosmos3-deep-dive-20261108-1841/report.md`; digestion-d3d-cosmos3-20261108.md; batch context in batch 1. *What we took:* the GB200-is-a-test-config correction (base-Nano generation is NIM-sanctioned on the Thor; the Sim checkpoints extrapolate to slow-motion only) and Cosmos3-Edge as the Thor-designed tier. *Verdict:* **B** as a product line; quality figures NVIDIA-reported only.

## D

**D3D** — decoupled diffusion drafting for speculative decoding (Chen et al.; Fudan Univ., Shanghai Academy of AI for Science, Shanghai Innovation Institute, Nanjing Univ., Huawei). *Where:* arXiv:2611.06425; github.com/fudan-generative-vision/D3D (MIT, checkpoints public); deep-dive report as under Cosmos. *What we took:* the single-stream caveat (5.00×/5.71× on 2×H800, eroding to 2.7× at 16 concurrent) and the per-target drafter cost (~360 GPU-hours) — a porting experiment for the Thor, not a drop-in. *Verdict:* **B+.** The cheapest credible attack on our decode wall; starts with the Qwen3-8B pair.

**DataChaz (Charly Wargnier)** — X/Typefully promoter whose W2A launch thread Casey submitted. *Where:* digestion-w2a-world2agent-20261108.md. *Verdict:* **D as a source** — marketing-shaped; everything usable came from the repo read behind it.

**DeepSeek — dsh-superagent** — open multi-agent project covered in batch 1, §13 via a secondary news source. *What we took:* real repo, ablations priced; its parallelism costs ~3.8× tokens (acceptable on prepaid seats, quoted with price); its benchmark measures scheduling, not code. *Verdict:* **B+.** Verify against the repo before any reuse; the news wrapper is not the evidence.

**Dessa — see Block.**

## E

**ESP32-P4 offline ASR (Kroko)** — microcontroller speech recognition without internet (batch 2, §4). *What we took:* the phrase-bounded trigger pattern — zero false activations across 88 near-miss clips — a doorbell, not an ear; consonant with presence doctrine (ambient listening still refused). *Verdict:* **B** (open artefact + eval scripts; developer-reported figures).

**Extrapolator AI** — independent technical-explainer publication; our route into the MeSS paper (batch 3, §1). *Verdict:* competent secondary source that includes critical observations; the paper remains primary.

## F

**FlexiAvatar (UNIST)** — 3D avatars from any camera (ECCV 2026; batch 2, §11). *What we took:* evidence weighted by observation frequency, synthetic footage discounted — verification relocating into representation, again. *Verdict:* **A−** (peer-reviewed; read via press coverage).

**Frameboy / Atlas — see World Labs.**

## G

**GITM (Ghost in the Minecraft)** — Minecraft agent framework whose "first to unlock the entire technology tree" is the literature's most over-claimed result (per-item rates across staged episodes; never replicated). *Where:* successful-agents-minecraft-20261107.md. *Verdict:* the cautionary tale our evidence grading exists for. Its versioned text knowledge graph for recipes, though, is a genuine steal.

**Google — Harness²** (Google Cloud AI Research + Northwestern) — recursive agent harnessing: 8 file-mounted harness components, contrastive Propose/Probe/Compose editing, EXPERIENCE.md lessons library; weights frozen. *Where:* arXiv paper; Apache-2.0 repo v0.1.0; harness2.github.io; batch 3, §9. *What we took:* the invariant/domain candidate split; the refusal — verifier-free per-task adoption is an unguarded self-modification loop by our doctrine. *Verdict:* **A−.** The harness-thread's reference implementation for file-mounted, contrast-edited harnesses.

**Google — ML Drift / LiteRT** — on-device inference engine open-sourced (batch 2, §8); the submitted article's headline was garbled, the artefact is real with a production history. *Verdict:* **B+**; comparisons are Google's own. One article tail (migration planning) went unread after a failed re-fetch — recorded in the batch doc, not smoothed over.

**GR00T / Isaac — see NVIDIA.**

## H

**Harness² — see Google.**

**HermitCraft / 2b2t** — human Minecraft communities whose practice literature grounds the human-play-routines study (batch context: RH-1…RH-8 starter routines). *Where:* human-play-routines-20261107.md. *What we took:* chest-a-dead-player's-drops etiquette, named-chest ration culture (independently matched by Civ50), the Boatem Pole principle (a named joke object preceded the town), 2b2t's do-less expertise. *Verdict:* practice literature, no controlled studies — stated plainly in the study.

**Hi3D** — AI 3D creation company; Hi3D v1.0 (formerly Sparc3D) open-sourced. Contact named in the release: Yasmin Zhang. *Where:* github.com/hi3d-official/Hi3Dv1.0; huggingface.co/hi3d-official/Hi3Dv1.0; PRNewswire release; batch 3, §5. *What we took:* the open image-to-3D reference point for the foundry's un-authored long tail; the 90% slicing claim as a claim. *Verdict:* **B− artefact / D superlative.** "First production-validated" is marketing; no production user is named anywhere.

## I

**InferenceKey** — independent benchmarking blog (Medium + inferencekey.com) that ran Sage-A1.5 on one RTX 4090. *Where:* digestion-sage-verification-mode-20261108.md and the MCode seat take (Thor). *What we took:* the measured cost side of verification (2.2× time, 2× tokens, identical answers on easy questions) that the MCode take priced into the fleet's verify rule. *Verdict:* **B** — small-n, honestly bounded, artefact-level detail (including the launch-flag gotcha).

**Isaac — see NVIDIA.**

## J

**JARVIS-1** — Minecraft agent with a multimodal memory of (situation, plan, verified outcome) triples. *Where:* successful-agents-minecraft-20261107.md. *What we took:* the triples pattern itself — our commons/triples library is JARVIS-1's shape, living outside any body. Near-perfect short-horizon, 12.5% flagship long-horizon: the honest shape of the approach. *Verdict:* A/B canon for the league's memory design.

**Jev — see TypeSafe AI.** *(And see the disambiguation note in INDEX.md: TechCrunch's Jev, Jacquard's advisor, Aura's SDK component and d3-ultra's baseline are all the one TypeSafe product; the Thor's local `jev-semantic` ONNX judge is a separate namesake implementation in the same seat.)*

**JiRack — see CMS Manhattan.** *(Not the JEV rack. Not Jira.)*

## L

**La-JEPA** — latent-world-model robot policy paper (V-JEPA 2.1 feature space; ScholarBro as the submission route). *Where:* digestion-la-jepa-20261108.md. *What we took:* the control-vs-description distinction that reconciles its claims with our JEV-over-play negative. *Verdict:* **spike in flight** (Thor `~/la-jepa-spike/`, pre-registered kill criterion); verdict deliberately not pre-written.

**Lead Lab (leadlabhq.com)** — aggregator/news desk ("Milluki — News desk") whose Bolt E4B piece printed NVIDIA's full table including the lost rows. *Where:* batch 3, §4. *Verdict:* usable aggregator — reports vendor figures as vendor figures.

**L3G-World** — real-time world generation with a latent 3D Gaussian memory (memory grows with scene extent, not stream length). *Where:* HF papers page; batch 1, §15. *What we took:* the bounded-memory representation pattern for the perception thread. *Verdict:* **B−** (paper; no artefact linked).

**Liquid AI — LFM3 family (incl. d1/d1-Omni decision models)** — open model family; the d1 decision models prove the decision-model pattern at 2B on-device. *Where:* liquid.ai/blog/lfm3; batch 2, §1. *What we took:* category confirmation for Jacquard's provider interface. *Verdict:* **B** (open weights; vendor-run numbers). **LFM3-Audio download remains Casey's open item — research only, nothing downloaded.**

**llms.blog** — secondary roundup of reaction to the YC Labs swarms. *Where:* digestion-yc-labs-swarms-20261108.md. *Verdict:* **C as a source** — its value is the reception record; claim-level grading lives in the Civ50 addendum, from the primary write-up.

## M

**MachinePulse — World2Agent (W2A)** — open sensor→signal protocol for agent awareness. *Where:* github.com/machinepulse-ai/world2agent (schema 0.1 read at spec level); digestion-w2a-world2agent-20261108.md. *What we took:* a good envelope, three precise gaps measured against the Watcher's Charter — provenance is install-time trust only (no signal signing); dedupe is transport-level only and logical re-emissions are undedupeable via the protocol; **no heartbeat/liveness semantics** (a dead sensor is indistinguishable from a quiet world). *Verdict:* **B as a spec read.** Do not adopt without the charter's three fixes.

**MarkTechPost** — AI media outlet; source for the Auto Ontology (batch 1), d3-ultra (batch 2) and Harness² (batch 3) items. *Verdict:* technically competent secondary coverage; every load-bearing number traced to its paper/repo before use in our docs.

**MeSS** — 3D urban scene synthesis from 2D mesh via image diffusion (arXiv:2508.15169; author blog: albertchen98.github.io). *Where:* batch 3, §1. *What we took:* consistency-as-an-explicit-correctable-pass (GCAlign) and the image-over-video argument for geometry-conditioned synthesis. *Verdict:* **A−** (paper; read via explainer).

**Microsoft — AgenSH** — self-organised coding-agent harness, open-sourced MIT 24 Oct 2026 with paper, launch scripts and reproduction guide. *Where:* Microsoft's GitHub repo + arXiv paper (via NeoTeo's careful coverage); batch 3, §2. *What we took:* the claim/verify/merge cycle at published scale (Gitea workspace, Mattermost messaging, DeLM-derived shared context) as the comparison point for our shared-state claim skill. *Verdict:* **A−.** Shortlist: read its protocol against our claim skill before the next large parallel dispatch.

**Microsoft — MAI-Image-2.6 / Flash** — image models in Foundry at $38/$19 per M output tokens (batch 2, §9). *Verdict:* **C** — filed as a price reference only; local SDXL remains the default.

**MineRL / VPT (OpenAI)** — Minecraft imitation-learning lineage: VPT's diamond pickaxe at 2.5% of 10-minute episodes after a 70K-hour prior; MineRL 2019's ~660 entries with zero diamonds. *Where:* successful-agents-minecraft-20261107.md. *Verdict:* A/B canon — the field's honest base rates.

## N

**NeoTeo** — tech publication whose AgenSH piece corrected its own garbled headline in-body (the 1,024-agent figure is one task, not the mean). *Where:* batch 3, §2. *Verdict:* a secondary source that modelled the scepticism we ask of ours.

**NVIDIA — Auto Ontology** — open-source semantic layer for agents (batch 1, §§4+7, where the dev.to audit and the product were graded separately: audit A−, product C+; plaintext-creds-by-default noted). *Verdict:* the audit harness is the steal; the product needs its scores published.

**NVIDIA — Bolt E4B (Nemotron 3.5)** — 4 GB conversational-agent model on a Gemma 4 E4B base. *Where:* research.nvidia.com Nemotron lab page (primary); HF/Ollama/LM Studio; batch 3, §4. *What we took:* a named presence/front-room evaluation candidate, with its Tau2 loss printed in our doc so future-us benchmarks the right weakness. *Verdict:* **B** (open weights; vendor numbers, losses disclosed).

**NVIDIA — Cosmos — see Cosmos 3.**

**NVIDIA — Isaac / GR00T** — robotics platform: Isaac Lab 3.0 GA, Isaac OS runtime (on Holoscan), SimReady asset library, Human 1M dataset (full set gated to Cosmos Coalition partners), GR00T foundation models, Halos safety; partner reference humanoid Agile ONE SN (Agile Robots, Jetson Thor onboard, early 2027). *Where:* nvidianews.nvidia.com GTC Berlin release; batch 3, §7. *What we took:* the runtime-as-product convergence, noted in the harness census; the SimReady/data-as-shared-artefact pattern. *Verdict:* **C−** (roadmap-grade; the software artefacts are real, the headline humanoid is a future partner product).

## O

**Octopus SI OS** (repo: github.com/miuuyy/Octopus-SI-OS, MIT, created 2026-10-09, 0 releases) — open-source Rust-kernel agent runtime: an append-only ledger drives the kernel; artifacts (hash-pinned manifests) are the only things that cross boundaries; runs are durable records that park on checkpoints and wake on artifact arrival; policy is never stored — a deterministic formation recomputes each grant as worker-ceiling ∩ EE-chain ∩ run-bindings, with "the creator is not an input" as a stated rule; success is a **mark**, recorded only after a verifier package passes, and no mark-emission tool exists for agents to claim success with. *Where:* repo README + `docs/architecture.md` + contracts set (primary); AlphaSignal preview for framing only; full comparison in octopus-si-os-comparison-20261108.md (ProArt ZCode seat + parent evidence check, 2026-11-08). *What we took:* the mark/verifier pattern as the strongest external form of our claimed-but-not-done doctrine; policy-as-formation (recomputed, never stored) as a design contrast for Jacquard's compiled rules. *Verdict:* **fleet study graded** — headline claims (≈45K lines, ledger-driven, five concepts) verified accurate against the repo; scenarios are the author's intended use, not tested features; author candour about limits is unusually high.

**Olam Labs — see YC Labs.**

**OlmoEarth — see Allen Institute for AI.**

## P

**Palace** — conversation-mining/memory tool whose v0.19.1 release corrected its own embedding performance claims (batch 1, §11). *What we took:* the ingestion-corruption taxonomy and the obligation it creates — re-measure or withdraw our own 10.39× if the execution path changes. Shortlist (batch 1): a Palace-style ingestion audit of our memory/triple miners. *Verdict:* **B+**, lifted by the self-correction.

**PIANO / AgentSociety / VillagerBench / Smallville** — multi-agent society architectures surveyed in multi-agent-towns-20261107.md. *What we took:* the Sid verdicts (specialisation collapses without social information flow; provided institutions vs emerged ones) and the Seeded Word + Commons Chest experiment designs. *Verdict:* mixed B/C canon, graded claim-by-claim inside the study.

## R

**RacerGS** — residual autoregressive context for 3DGS compression (>150×) (batch 2, §10). *Verdict:* **B−** (paper exists; read via news summary, no artefact inspected). Third leg of the Gaussian thread's delivery-size question.

**Ramen — see Aura Autopilot.**

## S

**Sage-A1.5 (Shanghai AI Laboratory)** — open research agent (Qwen 35B MoE base) whose Verification Mode the fleet priced. *Where:* digestion-sage-verification-mode-20261108.md; MCode seat take (Thor). *What we took:* the decision rule — verify iff P(wrong) × R≈0.38 × C_error > C_verify; a verify pass needs a *named new evidence source*; verification never substitutes for authorisation. *Verdict:* **B.** The easy-question arm proves cost, not inefficacy — recorded as such.

**ScholarBro** — paper-digest mailing; the route by which La-JEPA arrived. *Verdict:* a finding aid, never a source.

**SculptForge** — Gaussian splats trained from phone video (batch 1, §10). *Verdict:* **B** (open source; numbers changelog-grade). The foundry thread's phone-capture reference.

**SenseTime — Loop-9B** — open 9B model reusing layers for deeper processing (batch 1, §12). *Verdict:* **C+** (vendor chart, one internal benchmark in the set, no tech report).

**Soniox** — speech API; v6 "agent text echo" migration (batch 1, §3). *What we took:* a precise integration contract and a new fleet rule candidate — Soniox silently reroutes pinned v5 names to v6, so **behaviour-diff checks on provider upgrades**. *Verdict:* **B−** (contract A-grade, accuracy data absent).

**SpAItial — Echo-3** — iPhone scans to 3D digital twins (batch 2, §5). *Verdict:* **C.** Real product, zero accuracy metrics in coverage.

## T

**TechCrunch (Russell Brandom)** — "Jev is Vercel's fastest-adopted AI model ever" (16 Oct 2026). *Where:* batch 3, §10. *Verdict:* **B** — named-source journalism over published platform data, caveat carried in the piece. Its subject is TypeSafe's Jev; see the disambiguation note.

**Triband** — game studio whose developer interview (Press Play) contributed the LPM metric and the ladder that resolved the Aura tension (insider-learning for regression, cold agents for falsification). *Where:* batch 1, §2. *Verdict:* **C+** practitioner testimony; the metric is the steal.

**TypeSafe AI — Jev** — the System One **decision model**: state + typed questions (Choice/Score/Noul) in, calibrated probability distributions out; no generated text; 70–500 ms; $0.042/M input tokens, output free; launched 15 Sep 2026 (limited release), on Vercel AI Gateway as `typesafe-ai/jev` from 16 Sep 2026; trained with RLCD; published limitations include arithmetic, counting, date comparison, indirect reasoning. *Where:* typesafe.ai docs; Vercel changelog 2026-09-02; Leonis Capital, "Jev and the Rise of Decision Models" (2026-09-24); TechCrunch 2026-10-16; batch 3, §10 (full disambiguation), batch 1 §14 (Aura's use), batch 2 §2 (d3-ultra's baseline). *What we took:* independent market validation of the decision-model category our Jacquard architecture bet on — and of its placement: **advisor behind a provider interface, NEVER the gate**, a ruling the product's own limitation notes support. *Verdict:* **the same Jev as ours.** The category is proven; the vendor choice stays subject to our sealed held-out A/B (d3-ultra is the named challenger).

## V

**Vercel — AI Gateway** — the platform whose published adoption data underlies the TechCrunch Jev story (35% of paid teams in two weeks; open-source models >70% of gateway tokens). *Where:* vercel.com changelog + gateway data; batch 3, §10. *Verdict:* primary platform data with a stated limited-view caveat — it undercounts labs with their own APIs, and Vercel says so.

**VFlash (NVIDIA)** — speculative decoding for spatial predictions: a structured draft accepted on structural validity rather than token agreement; Thor latency 3,552.7 → 703.3 ms as reported. *Where:* digestion-vflash-20261108.md. *Verdict:* **C+** (journalism-grade source; multipliers parked pending the paper).

**vLLM Semantic Router — d3-ultra** — 27B multimodal decision model (batch 2, §2), benchmarked by its vendor against Jev 1.14 on private sets (SR-Text 87.2 vs 73.1; SR-Box 58.2% vs 45.7%). *What we took:* the named challenger for a sealed held-out A/B behind Jacquard's provider interface; "state once" economics (≈7.3 ms marginal per extra question). *Verdict:* **B−.** Nothing changes on vendor tables — that rule is the point of the interface.

**VoicePipe** — script-in, performed-dialogue-out tool (batch 2, §6). *Verdict:* **C−** (downloadable; no engine/model/pricing/samples disclosed).

**VoxLock** — speech-to-text error reduction for calls (batch 1, §8). *What we took:* an artefact with author-declared limits and an independent eval that partly disagrees, in print — and a shortlist item (A/B in front of radio-room whisper, graded on our own PTT audio). *Verdict:* **A−/B+** — the batch-1 model of how to publish a claim.

**Voyager** — the Minecraft agent whose verified skill library is the field's load-bearing result (skill ablation −73% without verification). *Where:* successful-agents-minecraft-20261107.md. *Verdict:* B canon; world-evidence-as-verifier is the steal our league is built on.

## W

**World Labs — Frameboy / Atlas** — world model streamed to a browser at interactive rates; RTFM lineage (posed frames as spatial memory, "context juggling"). *Where:* digestion-frameboy-atlas-20261108.md. *What we took:* the Confluence shape-rhyme (a thin client lending its IO to a remote mind) with the opposite payload. *Verdict:* **C** (research preview; the source article's author is AI-generated and editorially reviewed — stated in the doc).

**World2Agent — see MachinePulse.**

## Y

**YC Labs + Olam Labs — the Minecraft/Mindustry swarms** — Civ50 (50 GPT-6.1 Sol agents, one survival world, "build a thriving civilization"), Bed Wars, Mindustry; logs, replays and code published. *Where:* labs.ycombinator.com (primary); digestion-yc-labs-swarms-20261108.md (reception, via llms.blog); **Civ50 addendum in multi-agent-towns-20261107.md, graded B**. *What we took:* 22 of 34 deaths before minute 20 (RH-4 vindicated); the roster-order hierarchy artefact (46/49 first DMs to the first-listed agent — a standing warning for our cast/directory design); Noor's named-chest ration protocol (transfer counts only on confirmed consumption — our RH-5 rule, independently arrived at, failure mode included); the workaround divergence (diagnose-and-share vs conclude-impossible). *Verdict:* **B** — full public artefacts; interested-party authors; single run/world/model; near-zero death cost by design, which bounds what its survival findings can teach a league where death is expensive.

## Z

**ZETIC** — the NVIDIA-forum VLA measurement thread (π0.5, GR00T, SmolVLA) on Jetson Thor/Orin/Nano (batch 2, §3). *What we took:* the first public per-policy-call pricing for our exact boards (SmolVLA compiled 50 ms / 3.35 J; π0.5 132 ms / 11.31 J) — the fleet's allocation doctrine, arriving from robotics. *Verdict:* **B+** (public dashboard, full methodology, honest conflict disclosure; TensorRT rows pending, so the table is a floor).

---

## Fleet-internal sources (not external contacts, listed so future searches land)

- **Seat takes** (Thor `~/craftmind-league/seat-takes/`): MCode on Sage verification mode; ZCode on Anthropic agent memory — both 2026-11-08, both indexed from digestion docs on this shelf.
- **Octopus comparison study** — ProArt ZCode seat, landed 2026-11-08 as `octopus-si-os-comparison-20261108.md` on this shelf (indexed above); its contacts row carries the graded verdict.
- **La-JEPA spike** — Thor `~/la-jepa-spike/`; the digestion doc marks it in flight by design.
- **League operations** — Thor `~/craftmind-league/OPERATIONS.md` and `commons/triples/` are the primary records the studies cite; the studies are commentary on them, never a substitute.

*Built 2026-11-08. If a source appears in a study on this shelf and not here, the contacts file — not the study — is what's wrong; add the row.*
