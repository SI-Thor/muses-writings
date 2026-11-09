# Decode-Rate Settlement — the :8311 actor, measured

*Settles open question 1 of `syndicate-of-four-spec-20261108.md` (§9): OPERATIONS §5 measures the Thor `:8311` actor at 122–128 tok/s decode; the Syndicate study's §4.2 serving arithmetic used 7.9–8.4 steps/s "from the WSP clause-2 context". Casey's standing rule applies: a striking figure is a claim until independently reproduced. This note reproduces both, identifies what each actually measured, and states the corrected figure. Measured 2026-11-08 (AKST evening) by direct probes against the live serving endpoint; no restarts, no config changes; residents `:8310` / `:8311` / `:8077` health-checked before and after and verified alive.*

---

## 1. What each original figure most plausibly measured

**122–128 tok/s (OPERATIONS §5) — the llama-server serving path, reproduced.** OPERATIONS §5's context is explicit: the actor served by llama.cpp (`llama-server`, BF16 GGUF, `-ngl 99 --ctx-size 8192 --parallel 4 --cont-batching`), "decode 122–128 tok/s on actor-shaped calls". That is per-token decode rate in the production serving stack.

**7.9–8.4 steps/s (study §4.2) — a different stack entirely: the WSP hunt's offline HF generate path.** The chain of custody: the figure enters the record in the WSP Q1 work (item 9) as the rate of "the real generate path" in which clause 2 was unmeasurable, and the batch digestion repeats it in those words. The WSP hunt's own METHODS (Thor `~/wsp-hunt-20261108/METHODS.md`) show what that path was: the HF BF16 checkpoint (`~/models/Qwen3-0.6B-BF16`, 28 layers, hidden 1024) driven through a Python/transformers trace harness (`traces.py`) that runs `generate` **with hidden states returned at every step** — 220-token generations, forced-degenerate continuations, per-step hidden-state materialisation for the loop-direction analysis. One "step" there is one generated token position, so steps/s ≈ tok/s *in that harness* — but the harness is an offline analysis instrument (eager PyTorch, full hidden-state output per step), not a serving stack. The Syndicate study then imported the number as "measured decode on the actor stack" (§4.2), which it never was: it was never measured on `:8311`, on llama-server, or on any serving path. **A unit-and-stack trap, not a measurement error by either side** — each figure is believable for the path it came from; they differ by ~16× because the paths differ by ~16×.

## 2. The probes

20 metered calls against `http://127.0.0.1:8311/v1/chat/completions`, in the actor's real serving configuration: model `qwen3-0.6b-actor`, `chat_template_kwargs: {enable_thinking: false}` (the league's mandatory setting), temperature 0.7, `max_tokens: 120` (the Tier D decision unit in the spec, §2.2). The prompt was actor-shaped in the league's literal sense: the verbatim system prompt from `pulse/actor-client.js`, and a user message built by that file's `contextDigest` structure from Cody's real saved state (position in the dip, hp 1.33, food 9, his actual inventory and milestones), plus a tastes block and a history digest of the size class the voice+tastes layer adds. Cold prompt: 409 tokens (server-reported). Timing taken from llama-server's own `timings` fields and from wall clock. Two conditions:

- **Single-stream:** 12 sequential calls (the league's single-body condition).
- **Concurrent burst:** 8 calls as two bursts of 4 simultaneous (the server's `--parallel 4` slots, cont-batching on) — the pilot's four-body condition.

The governor was not in the path: the `syndicate-captain` identity the spec proposes does not exist yet, and creating it is a config change, out of this job's read-only scope. The governor is an HTTP metering proxy; it does not change decode rate, and its overhead is not what either disputed figure measured.

## 3. Results

**Single-stream decode (llama-server `predicted_per_second`, n=12): median 130.2 tok/s, p10 122.2, p90 131.8, range 114.5–132.2.** Response wall clock: median 0.16 s for the actor's actual short outputs (11–34 tokens generated, median 20, all `finish_reason: stop`).

**OPERATIONS §5's 122–128 tok/s is REPRODUCED** — this run's median sits just above their band and its p10 inside it.

**Four-concurrent decode (n=8): per-call median 79.4 tok/s (p10 64.0, p90 103.4); aggregate across the 4 slots 159.7 and 218.3 tok/s in the two bursts.** Continuous batching buys aggregate throughput (~1.3–1.7× single-stream on these short generations) at a per-stream cost (~60% of single-stream rate) — sublinear, as the study speculated, but around a base ~16× higher than the study assumed.

Prompt processing, for completeness: the one cold 409-token prompt processed at 4,914 tok/s (83 ms); every subsequent identical prompt hit llama-server's prompt cache (server-reported `prompt_n: 1`, ~8 ms). League prompts vary per beat, so the cold figure is the applicable one — and at either figure, prompt cost is negligible next to decode. (OPERATIONS §5's "~1,300 tok/s prompt processing" was not reproduced on this prompt size; prompt-processing rate is prompt-length-dependent and was not part of the dispute — flagged here as an observation, not a settlement.)

## 4. The corrected figure for the Syndicate arithmetic

Use these, replacing §4.2's 7.9–8.4 tok/s and every quantity derived from it:

- **Single-stream actor decode: ~130 tok/s median (plan on 120).**
- **A Tier D decision (~120 output tokens): ~0.9 s of decode single-stream; ~1.5 s per stream at 4-way concurrency** — not the ~15 s §4.2/A2.3 priced in. Tier D's 20 s staggered cycle (spec §2.2) is comfortable by an order of magnitude, and criterion 5's envelope (no citizen waits > 90 s for a Tier D decision more than twice in a round) is not a serving risk on this stack at pilot size.
- **Aggregate at 4 concurrent slots: ~160–220 tok/s measured** (short generations, warm prompt cache on the repeated probe prompt — treat the top of the band cautiously for sustained unlike-prompt load; the per-call concurrent rate, ~79 tok/s median, is the robust planning number).
- **The 7.9–8.4 steps/s figure is retired from serving arithmetic.** It remains the true rate of one thing only: the WSP hunt's offline HF trace harness, which is where clause 2's unmeasurability lives. It says nothing about what the league's minds cost.

What this does **not** change: Addendum 2's tiered conclusion already superseded §4.2's size table on structural grounds (bodies stopped being the multiplier); this settlement removes the surviving caveat in A2.3 ("a Tier-D decision still costs ~15 s of decode single-stream") — it costs ~1 s. The pilot-measurable unknowns A2.3 named (rack concurrency under the reflex rotation; Tier-D aggregate at 4 syndicate streams) stand; the second is now bounded from measurement at one syndicate's scale. The D3D decode question is untouched by this note: D3D was an attack on artefact-generation time in the WSP path, and remains untested for governance reasons, not decode reasons.

*Process note: probe script and raw results were run on the Thor (`/tmp/decode_probe.py`, `/tmp/decode_probe_results.json`, 20/20 calls HTTP 200, all timings server-reported). The one surprise in the run — `prompt_n: 1` on repeated prompts — was traced to llama-server's prompt cache rather than filed as a mystery; it is reported above because it changes which prompt figure applies. Residents verified alive after the bursts: `:8310` ok, `:8311` ok, `:8077` ok (judge + both JEPA arms loaded). `:8310` was never probed — the spec's `syndicate-reflect` identity is a proposal, and nothing in this settlement required touching Casey's presence brain.*
