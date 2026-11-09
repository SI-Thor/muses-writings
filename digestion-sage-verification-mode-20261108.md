# Index entry — Sage-A1.5 Verification Mode: when is a second look worth its cost? (MCode seat take, summarised)

*2026-11-08. Studies-shelf index entry under Casey's standing digestion instruction. The full research take already exists and is the evidence; this page summarises it in one page and points at it.*

- **Full seat take (primary):** on the Thor — `~/craftmind-league/seat-takes/mcode-verification-mode-20261108.md` (19,982 B, ~2,880 words, delivered untrimmed by the MiniMax Code seat, 2026-11-08)
- **Primary source under study:** InferenceKey's run of Sage-A1.5 (Medium, 8 Nov 2026), read directly for this entry.

## The facts (source-verified)

Sage-A1.5 (Shanghai AI Laboratory; Wenjie Lou + 98 co-authors; Apache-2.0) is an open research agent built on Qwen's 35B MoE base with ~3B parameters active per token. InferenceKey ran the authors' own ~22 GB compressed file on **one RTX 4090 (24 GB)** under llama.cpp at ~136 tok/s single-request. Its **Verification Mode** is a switch made of one sentence added to the standing instructions: the agent reviews its own answer before handing it over.

- On easy questions: **12/12 correct with the mode off and on** — but on-mode averaged **25.0 s vs 11.2 s** and **1,890 vs 934 tokens**. The hafnium worked example: off 13.6 s / 5 tool calls / 1,159 tokens; on 24.7 s / 9 calls / 2,320 tokens — the extra turns almost entirely *re-checking facts already confirmed*. ("Let me verify" as a loop, not a gate.)
- In the authors' own paper the same mode lifted **BrowseComp from 72.5% → 82.9%** across all 1,266 questions — a benchmark built from facts that are hard to dig up, where the first search often points the wrong way. The mode buys accuracy exactly where first-pass answers are unreliable, and buys nothing where they aren't.
- Gotcha for anyone reproducing: the authors' llama.cpp command names a reasoning option `deepthink` that llama.cpp doesn't recognise (the server dies at launch); `deepseek` works. Also: the model thinks before it speaks (a two-sentence definition took 14.4 s / 1,905 reasoning tokens), and sub-24 GB operation (16/12 GB imitated on the same card) stayed correct but much slower; real cards of those sizes are untested.

## The seat take's contribution — a decision rule, not a vibe

MCode's take converts the anecdote into arithmetic. **Verify iff P(first-pass wrong) × R × C_error > C_verify**, where R ≈ **0.38** (the BrowseComp rescue rate implied by the paper: 132 of 348 would-be-wrong answers rescued), and C_verify ≈ 1× task cost (the measured doubling). Break-even: at error-cost 10× the task, verify when error probability exceeds ~26%; at 100×, ~2.6%. Around that rule, four gates and adjustments, of which the sharpest are:

1. **A verify pass needs a NAMED NEW EVIDENCE SOURCE.** Re-reading your own confirmed facts (Sage's failure mode above) is not verification; it is rehearsal. If the second look consults nothing new, it cannot rescue anything.
2. **Split the doctrine by check class.** Class A *existence* checks (did it land / was it written / is it deployed) stay **unconditional but deterministic** — scripted assertions and log greps, not model passes. Class B *content* checks are the rationed ones: priced by the rule, run from per-class error ledgers, sample-audited at 10–20% at low stakes, and run **async after delivery** except where seconds are critical.
3. **Prove verify triggers fire by behaviour change, not HTTP 200** — the take cites an InferenceKey finding of a silently dropped `{"verification": true}` returning success: a verify path that reports OK while doing nothing is worse than none.
4. Sceptical notes the take files against its own sources: the easy-question test proves *cost*, not inefficacy (100% base rate, n=6/arm — nothing to rescue); and the headline 2.2× is a mean over a bimodal distribution (one hafnium on-run was 15.9 s vs 15.5 s off).

**Standing boundary (the take is explicit): verification never substitutes for authorisation.** A verified plan is still an unapproved plan.

## Why this is on the studies shelf

It is the priced version of the fleet's verification doctrine. Our Watcher's Charter says *verify the effect*; Sage + the seat take say *what a content-verification costs, when it pays, and how to tell a real second look from a ceremonial one*. Filed beside the Anthropic memory entry: both are about spending offline/second-pass compute where it demonstrably changes outcomes — and refusing to spend it where it only changes latency.

---

*Index entry compiled 2026-11-08 from the seat take (Thor path above) and the InferenceKey primary. The seat take is the full argument; this page is its map.*
