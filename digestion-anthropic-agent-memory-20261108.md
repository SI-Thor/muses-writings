# Index entry — Anthropic, "The components of agent memory": dreaming, salience, and the verification layer our memory is missing (ZCode seat take, summarised)

*2026-11-08. Studies-shelf index entry under Casey's standing digestion instruction. The full research take already exists and is the evidence; this page summarises it in one page and points at it.*

- **Full seat take (primary):** on the Thor — `~/craftmind-league/seat-takes/zcode-anthropic-memory-20261108.md` (~2,540-word body, delivered by the GLM/ZCode seat, 2026-11-08)
- **Primary source under study:** Anthropic, "The components of agent memory" (published 6 Nov 2026), read directly and in full for this entry.

## The paper in brief (source-verified)

Anthropic's framing: **memory is a prediction** — a written note is a bet that a future session will want to rely on it without re-checking. Agents capture work in logs/transcripts; **dreaming** (sleep-time compute, after Letta/UC Berkeley) is the offline pass that reorganises those logs into notes, corrects them against the transcripts, and maintains higher-level representations.

- **CL-Bench 1.0 learning loop:** Opus 5 was the first model to *close* it — memory entries carrying a **rule plus how the rule was known to be true**, answers to earlier questions, and explicit **trap warnings**. Sonnet 4.6, by contrast, scattered untested guesses across files. Opus 5.5/Sonnet 5.5 also closed the loop.
- **Pokémon Red salience:** Sonnet 3.7 wrote **413 files in 225 folders** (an archive of every battle, item, NPC), earned **1 badge**, and its memory went stale until maintenance ate play time. Fable 5 wrote **9 files + a `global.md`** and earned **4 badges**; Opus 5.5's small, live-rewritten folder beat the game. Lesson: memory should hold what the world *doesn't* re-tell you every turn — plans, tested rules, strategy — not state you can read off the screen.
- **Dreaming corrects:** the Mt. Moon case — a wrong note ("PokéCenter is on the east side") caused repeated one-way-ledge failures; a dreaming pass checked the note against the session transcript, caught and rewrote it, and the corrected run went through. Without correction, the agent looped three times and gave up.
- **Wikis as representation:** over ~350k Stainless files, wiki quality grew **13% → 48%** across 128 dreaming sessions; **wiki + search scored 61% vs 53% search-only**, saving ~20k tokens/question. But on the Harvey LAB legal-brief tasks the wiki sometimes didn't help (single-document lookup tasks), and once grew larger than its source corpus — a map as big as the empire abstracts nothing.
- **Steering:** telling strong models what memory is *for* helps; prescribing capture rules hurt — a "record only failures" rule **reduced** the memory benefit for Opus 5/4.7. Steering helped weaker models most (prompting Sonnet 4.6 to read memory before answering and test its theories nearly doubled its score).
- **Single-writer ownership (the LAB datum):** when several agents wrote a shared contract-terms table concurrently, the brief met only **41/57 facts (72%)** — agents overwrote each other. Rebuilt with **one page per contract, written by a single agent, quoting terms verbatim**: **57/57 (100%)**.
- **Promotion is dangerous:** notes promoted into every session's context (context injection) must keep the top layer small — Claude Code loads only the first 200 lines / 25 KB of MEMORY.md as an *index* — because an incorrect injected note is carried into *every* session.

## The seat take's thesis — our architecture matches; our verification layer doesn't

ZCode's take: the fleet's memory architecture already *is* the paper's endorsed design — `MEMORY.md` as index, daily notes as the log, nightly distillation as dreaming, the citizens' triples library as body-independent memory, consult books as the promotion path. **All three gaps it finds are in verification, not structure:**

1. **Triples need provenance + status + reconciliation.** Give each triple a provenance pointer and a confirmed/unconfirmed status, and add a nightly **Mt. Moon-style reconciliation pass** that samples the oldest / least-verified triples and checks them against source transcripts — dreaming aimed at the entries most likely to have drifted.
2. **State-vs-derived split with single-writer ownership.** Durable memory should hold plans, tested rules, traps and strategy only (state is re-read from the world); and any shared table needs one writer — the paper's 16-of-57-facts loss under concurrent writers is the measured cost of doing otherwise.
3. **Tier the steering, route the consults.** Purpose-only doctrine for strong models (prescribed capture rules measurably weakened them); explicit checklists for citizens (weaker reasoners benefit most from steering). Route consults by task shape: books/wikis for synthesis questions, direct triples queries for single-fact lookup — the LAB result says a wiki earns its keep on multi-document synthesis and not on single-fact retrieval.

Evidence grading (the take files it against its own source): the Pokémon arms are single runs, Mt. Moon is a constructed demonstration, there are no error bars anywhere, and the best wiki numbers are 48–61% — directionally strong, numerically soft. One verification episode from the seat's own work is recorded in the parent record: its "no-memory control arm" claim for Mt. Moon is absent from the post's body text but corroborated by four secondary sources (the third arm lives in Figure 8's alt text) — the seat was substantively right; the fault was provenance labelling, and the correction was ledgered. Which is, neatly, the paper's own point about memory: the claim was fine; its receipt was missing.

## Why this is on the studies shelf

It is the external audit of our memory design by the lab that productised the pattern — and its verdict (structure right, verification thin) matches the fleet's 2026-11-08 experience from the other direction: our failures this week were not missing memory but unlanded effects and unlabelled provenance. The three gaps above are the actionable residue; they belong to the league/memory lanes, not to this digestion.

---

*Index entry compiled 2026-11-08 from the seat take (Thor path above) and the Anthropic primary, read in full. The seat take is the full argument; this page is its map.*
