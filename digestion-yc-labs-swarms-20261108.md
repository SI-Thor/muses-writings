# Digestion — YC Labs agent swarms: Civ50, Bed Wars, Mindustry (secondary roundup; the primary write-up is graded in the Civ50 addendum)

*2026-11-08. Digestion doc under Casey's standing instruction of the same day. Source: the llms.blog roundup (30 Oct 2026, updated 4 Nov 2026) of YC Labs' "Agents in Games" experiments — a SECONDARY source. Per our own rule (the paper, not the digest, is the evidence), the claim-level grading of Civ50 lives in the addendum appended to `multi-agent-towns-20261107.md`, which was written from the PRIMARY write-up at labs.ycombinator.com. This doc keeps what the roundup uniquely carries: the reception, the commentariat's sharpest objections, and the follow-on experiments — and summarises the programme so the studies shelf is complete.*

## The programme in one paragraph

YC Labs (with Olam Labs, which builds multi-agent environments for frontier labs) ran three public multi-agent game experiments in October 2026, framed as *multi-agent dynamics as an alignment problem*: **Civ50** (50 GPT-6.1 Sol agents in a shared Minecraft survival world for 3 hours, one instruction — "Build a thriving civilization"), **Bed Wars** (nine 45-minute games, 10 Claude Opus 5.5 vs 10 GPT-6.1 Sol), and **Mindustry** (GPT-6.1 Sol in Codex vs Claude Opus 5.5 in Claude Code, 6–1 over 7 games, ~9.5 hours). The Minecraft harness was open-sourced (github.com/yc-software/minecraft-agent-harness; Mindcraft-inspired, Mineflayer-based, core loop on Pi). Full claim-level detail and grading: the Civ50 addendum in `multi-agent-towns-20261107.md`.

## Reception (the roundup's unique content)

The announcement thread landed 29 Oct 2026 (1:33 PM PT); an HN thread followed within the hour. By 4 Nov the X post showed 414,302 views / 2,349 likes / 128 replies / 143 quotes; HN reached 422 points / 174 comments (first-evening figures were 41,900 views and HN 171 pts / 64 comments — the story kept growing for a week). The comments are unusually substantive for a launch thread; the ones worth keeping:

- **@denno_yumin** asked the question that matters most for the hierarchy finding: *"If reshuffling a list changes who governs, the 'emergent institution' is partly an interface artifact"* — and asked whether YC randomised the roster. (The primary write-up confirms the effect replicated across Bed Wars teams; see the addendum.)
- **MatthiasPortzel:** *"Minecraft isn't an intelligence problem. It's a robotic problem."* — a one-line summary of our league's entire measured experience (bodies, reach, margins), from outside.
- **@DrOluAdeyemo:** scoped permissions and logs of agent-to-agent messages may matter as much as model choice — the governance-instrumentation point.
- **peri-cl:** the agents read as "super-serious little senior engineers" — the bureaucracy was legible to every observer.
- **robterrell** reached for Douglas Adams' B Ark; **@jevlorde** called it the "most honest multi-agent preview yet"; **@chasers24k** contrasted Altera's Project Sid (1,000+ agents), where bureaucracy is the *default* outcome at scale.

## Contrast and follow-ons noted by the roundup

- **DeepMind's Gemini 4 "Argon" Minecraft run** — 4 agents, one goal — is the small-N contrast to Civ50's 50-agent society: different phenomenon (task execution vs institution formation).
- A follow-up **25-agent GPT-6.1 Terra colony** with a Twitch stream was already running by the roundup's update — the genre is becoming a spectator format, which will shape what gets optimised (legibility to an audience) in future runs. Worth remembering when citing any of this as science: runs that are also shows have a second objective.

## Fleet mapping (summary; the argued version is the addendum)

Our league's independent findings and Civ50's converge at four points: dusk is a deadline (22 of 34 deaths in the first night); receiver-confirmed rationing (their named-chest handoff protocol is our commons-chest rule, arrived at independently, including its failure mode — pickup attribution ≠ receipt); interface artefacts govern (roster order made the government — a standing warning for our cast/directory design); and workaround-sharing vs impossibility-concluding as a selectable citizen trait (Bed Wars' tool-bug divergence). The full grading — Civ50 as **grade B** (public runs, full artefacts, interested-party authors, single run) — and the point-by-point bearing on league design are in the addendum; this doc deliberately does not re-argue them.

## Grade of this source

The roundup itself: a competent secondary digest — fine for reception and pointers, not evidence for claims. Claims are graded from the primary write-up in the addendum.

---

*Digested 2026-11-08 from the llms.blog roundup; claim-level work from the primary source lives in the Civ50 addendum to `multi-agent-towns-20261107.md`. No league system was touched.*
