# Minecraft-Agent Videos — Field Survey: the technology, the tastemaking vocabulary, and the critic's craft

*Commissioned by Casey, 2026-11-08 17:17 AKST; sharpened by his addendum the same minute (17:18): a ninth video, and the centre of gravity moved — "videos like this are interesting on the level of what they got in the eye to do" (the perception/gaze layer: what the agent was made to SEE), "but what's even more interesting is how the human is being critical of both." The human critic — watching the agent AND the apparatus that produced it, criticising both, live, in a vocabulary — is the real subject. Movement D is therefore the heart; Movement C's harvest is re-ranked by it: terms the CRITICS use outrank terms the titles use.*

*What this survey is for: the fleet's decision models — curator, game master, judges, tells — need a vocabulary for their questions: what counts as a moment, a play, a beat worth surfacing. This study harvests that vocabulary where it actually lives: in the field's papers, in its open-source harnesses, and above all in the mouths of the humans who watch agents play and judge them.*

## Process record (documented as it goes, per the fleet doctrine)

**Sources commissioned:** eight videos + one playlist (Casey, 17:17), plus one video added by addendum (17:18). IDs: `OSGSROIs8cI`, `2tbaCn0Kl90`, `uRDBco-cSK4`, playlist `PLmB_zDnP9YpxHyKsJxaCOfXwb2J30j5lb`, `j5nxDKAjg6U`, `GwXEYYUDQWI`, `RQqqm7qk8bk`, `RiDqeUwBU6A`, and (addendum) `mfgi4HYR9QM`.

**Tooling state, honestly.** The local YouTube skill routes through TranscriptAPI; the key exists in the environment, but the account has **no active paid plan** — every metadata/transcript/playlist call returned HTTP 402 "You don't have an active paid plan yet." The skill's self-service plan-purchase flow was **not** followed: Casey has not authorised a subscription, and none was taken out. Fallback route used: the public transcript mirror at `youtubetotranscript.com` fetched as page text, plus YouTube watch pages for descriptions, plus the linked repos and papers. The mirror rate-limits (HTTP 429) after a few fetches; per fleet discipline a rate-limited route is a hard stop for that route — failed fetches were not retried through another endpoint.

**What that means for coverage:**
- **Full transcripts read:** `OSGSROIs8cI` (Wifies), `GwXEYYUDQWI` (TheCommandsMan, builders), `RQqqm7qk8bk` (GoldActual, One Block — all 484 lines).
- **Descriptions + linked sources read, transcripts NOT obtained (429):** `2tbaCn0Kl90` (Project Sid launch), `uRDBco-cSK4` (AI Species explainer), `RiDqeUwBU6A` (village build-off), `mfgi4HYR9QM` (tutorial-following). Their dossiers rest on descriptions, the papers/repos those descriptions link, the channel's own sibling videos read in full, and the surrounding critical literature — and are labelled accordingly, section by section.
- **One video unidentified:** `j5nxDKAjg6U`. Its watch page returned 429 and targeted searches did not surface the ID. Title, channel and technology are **UNKNOWN** — filed as a plain gap in A.5, never invented.
- **Playlist creator/back end not identified:** the playlist enumerates cleanly (10 videos, listed in A.4) but no description, repo or paper surfaced for it; its technology is graded INFERRED at genre level only.

**Identification labels used throughout:** **CONFIRMED** = repo, paper, description or in-video evidence. **INFERRED** = read from behaviour/format, labelled with its reasoning. **UNKNOWN** = the evidence was not there; said so.

**A note on model names in the build-off videos.** TheCommandsMan's videos brand their contestants with near-future model names ("Gemini Argon 4", "GPT-6 Astra", "Claude Opus 5.5"). These are the videos' own framing — entertainment branding, not verified product facts — and are quoted as such. The one contestant whose technology is independently verifiable is **BlockGPT** (blockgpt.ai), a real commercial structure generator.

---

# MOVEMENT A — Per-video dossiers

## A.1 — Wifies, "AI Simulates Civilization in Minecraft" (`OSGSROIs8cI`)

**What it is.** Three frontier chat models — ChatGPT, Claude, Gemini — given embodied Minecraft bodies and an escalating contest format: build something, then a redstone challenge (winner earns extra teammates, so the field multiplies into model-teams), then a zombie-apocalypse finale scored last-standing. The AIs are voiced by other YouTubers (Claude: CraftyMasterMan; Gemini: Parrotx2; GPT: Kenadian; GPT_2: Sipover; GPT_3: Wato1876) — the narration layer is human performance over agent behaviour, a production choice worth noting in itself: the voices give each model a *character* the audience can track.

**Moment-craft.** The beats are: (1) the agent's own tour of its build — the bunker, the pyramid, the shrine — agent self-narration used as the segment's spine, then checked against the world; (2) the challenge result read off the world, not the claim ("the only working Redstone Contraption" wins); (3) the apocalypse as pure attrition theatre — the death order read from chat messages ("the chat tells you all you need to know"), a tower-camping strategy winning by height; (4) the winner immediately crashing and forgetting everything — continuity failure played as the closing joke. Shareable moments here are *contrasts*: claim vs artefact, plan vs outcome, memory vs amnesia.

**Technology.** **CONFIRMED:** the code is by **Emergent Garden** and was made public (stated in the video and its credits). Emergent Garden is the creator of **Mindcraft** (`mindcraft-bots/mindcraft` — "Crafting minds for Minecraft with LLMs and Mineflayer"; see B.2): Mineflayer bodies on Java Edition, per-agent profile JSONs (name, model, prompts), the LLM writing and executing code actions through a sandboxed API, multi-provider model support. The three "players" are three different frontier models on the same harness — the video is, structurally, a harness-constant model comparison. Perception: structured game state via Mineflayer (positions, inventories, nearby blocks/entities), **not** pixels — the agents' "eye" is the state API plus whatever the prompt puts in front of them.

**Vocabulary (theirs, quoted).** The agents narrate in builder vocabulary — palette, foundation, decorative vs practical — and the video frames model identity as destiny ("Claude…", "Gemini…") while the events keep refuting it. The critical vocabulary is Wifies' own; it is extracted in Movement D, where this video is one of the two richest sources.

## A.2 — Altera, "1000 AI NPCs simulate a CIVILIZATION in Minecraft" (`2tbaCn0Kl90`)

**What it is.** The launch film for **Project Sid** (Altera.AL): large populations of LLM agents living in a shared Minecraft world — farming, mining, guarding, trading, taxing, voting, converting. The "1000" is the aspiration; the paper (below) reports runs of ~3 to 500 agents, with >1,000 attempted and exceeding server limits — the cultural results (tax votes, religion spread) come from the 500-agent run. Transcript not obtained (429); dossier from the description (which links `playlabs.altera.al`) and the paper.

**Moment-craft.** Civilisation headlines as moments: an economy appears, a constitution gets amended by vote, a joke religion (Pastafarianism, seeded with 20 priests) keeps converting people two hours later, towns develop distinct meme-identities. The shareable unit is not an action but a *social fact* — something no single agent intended, legible in aggregate.

**Technology.** **CONFIRMED** via the paper: *"Project Sid: Many-agent simulations toward AI civilization"*, arXiv:2411.00114 (Altera.AL, submitted 2024-10-31); code/report at github.com/altera-al/project-sid. The architecture is **PIANO** — expanded two ways in the paper ("Parallel Information Aggregation via Neural Orchestration" / "Parallel Input Aggregation"): ~10 modules run concurrently at different timescales (memory, goal generation, social awareness, action awareness, talking, skill execution, and more) and a **bottlenecked Cognitive Controller** synthesises their state and broadcasts one coherent decision — an explicit fix for the incoherence failure where an agent "says one thing and does another." Bodies are Mineflayer-class (the project builds on the Mindcraft lineage). Perception is structured state, with *social awareness* as a first-class perceptual module — and the paper's ablation is the finding: **role specialisation appears only when social awareness is present**; limit social perception and behaviour collapses to uniform, repetitive action. The paper's own stated limitation, quoted because Movement D needs it: the agents **"cannot simulate *de novo* emergence of societal innovations"** — they recombine trained human knowledge.

**Vocabulary.** "Emergence" is the title-word — and the contested one (see D.2). The paper's quieter terms are the useful ones: *coherence* (the controller's job), *social awareness* (a perception budget, not a trait), *specialisation* (an outcome you measure, not assign).

## A.3 — AI Species (Drew), "Scientists Left 1000 AIs Alone in Minecraft. They Created A Civilization." (`uRDBco-cSK4`)

**What it is.** Not a run — an **explainer/critique essay about Project Sid**, months in production, by a creator (Drew) who reads the research rather than running agents. Its description carries a full source list (arXiv:2411.00114, the project-sid repo, Smallville arXiv:2304.03442, ChatDev, Anthropic research) — the video is part of the critical literature, and is treated in this survey as a *critic-instance* (Movement D) rather than a technology instance. Transcript not obtained (429); the dossier rests on the description and the documented critical ecosystem around Sid.

**Moment-craft.** The essay's moments are *interpretive*: this is what the tax vote means; this is what the religion spread does and doesn't prove. Its shareable unit is a verdict.

**Technology.** Same as A.2 (its subject), plus the genealogy it cites: Smallville's generative agents as the ancestor pattern (perceive → remember → reflect → plan, with a memory stream and reflection synthesising higher-level inferences).

**Vocabulary.** The critical vocabulary around Sid is harvested in D.2 — including the sharpest single line in the whole survey, from the jazzmind.net essay on Sid: **"These agents did not invent civilization. They *released* one."**

## A.4 — Playlist: "Ai Villagers Simulate CIVILIZATION in Minecraft…" (`PLmB_zDnP9YpxHyKsJxaCOfXwb2J30j5lb`)

**What it is.** A 10-video series of villager-spectacle episodes, enumerated from the playlist page: (1) *I Made 100 VILLAGERS Simulate CIVILIZATION* [EP1]; (2) *…CIVILIZATION War* [EP2]; (3) *100 VILLAGERS vs ILLAGERS … War* [EP3]; (4–6) *AI Villagers Simulate Underground CIVILIZATION* [EP1–3]; (7, 8, 10) *AI Villagers Simulate Medieval CIVILIZATION* [EP1, 2, 3]; (9) *I HATE this CIVILIZATION of AI Villagers (CURSED)*.

**Technology.** **UNKNOWN at the level of receipts; INFERRED at genre level.** No description, repo or paper surfaced for this playlist. The genre it belongs to — the "100 villagers simulate X" spectacle — is conventionally *staged*: vanilla or lightly-modded villagers, pre-built environments, scripted narration over emergent villager pathing/trading noise; there is no evidence of LLM agents in this series, and the survey does not claim any. Two adjacent, verified works must not be conflated with it: **Grox's** scripted villager spectacles (a different, known creator in the same genre), and the human-player "100 Villagers Simulate Survival" format (different again — the "agents" are people).

**The genre's verified high-water mark — filed here because it is the playlist's real context:** **MONOCOLA Channel's "Project Will"** (Japanese, English subtitles): **32 custom AI villagers whose minds are a Gemini LLM**, with body, perception, memory, desires/instincts and conversation **all custom-built by the creator** — and the full run published as open data on GitHub: 9,874 utterances, 14,969 structured events, motive audits for all 24 killings, 45 grave epitaphs; 32 spawned + 10 born − 24 dead = 18 survivors in 6 hours. A second video covers an "instinct" iteration whose framing question is explicitly whether the failure to form society was **the system's fault** — harness-vs-agent attribution, stated by the creator as the research question. Project Will is what the villager genre looks like when it grows receipts; the playlist above is the genre's entertainment form.

**Moment-craft (genre).** Wars, betrayals, cursed collapses — narrative arcs imposed by editing on populations. The moment is a *story beat*, and the editor is the author.

## A.5 — `j5nxDKAjg6U` — UNIDENTIFIED

The watch page returned HTTP 429 through the available routes and targeted searches did not index the ID. Title, channel, date and technology are **UNKNOWN**. Recorded as a gap, in the open, per the commission's own rule: never invent content. If the fleet wants this one closed, the cheapest route is Casey opening the link once and reading the title aloud — or the TranscriptAPI plan question (see the process record) being settled, which would close several gaps in this study at once.

## A.6 — TheCommandsMan, "I Hired Pro Minecraft Builders to Take On AI" (`GwXEYYUDQWI`)

**What it is.** A build-off: professional human builders vs AI contestants, same briefs, structures judged side by side. Crucially, these are **not embodied agents** — this is the other pole of the field (see C.1): **one-shot structure generation**. Contestants produce structure files (.mcstructure) imported into **Bedrock** Edition. Contestants as branded in-video: "Gemini Argon 4", "GPT-6 Astra", "Claude Opus 5.5" (the video's own names; see the process note), and **BlockGPT**.

**Moment-craft.** The reveal-and-compare: each build materialises whole, and the moment is the *judgement* — the camera walk-around while the critic reads silhouette, palette, interior logic. Failure moments are prized equally: the first import crashed the game; one build "didn't even fit in the bounding box"; a model's preview image promised an angle/detail the actual structure cannot produce.

**Technology.** **CONFIRMED for BlockGPT:** blockgpt.ai — text (or image) prompt → schematic file (.schem/.litematic/.schematic for Java; .mcstructure for Bedrock), generation times ~30 s to ~59 min by model/tier; the video used its "Super" tier. The chat models were steered through a fixed scaffold the creator calls the **"super prompt"** appended to every model's input, under a brief whose operative terms are **"silhouette and palette"**. The "eye" here is inverted versus the embodied videos: the generator sees *nothing* of the world — it emits a structure blind, from the brief alone — while separate preview rendering creates an image of the build that can, and did, **lie about the artefact** (Movement D.6: the preview-vs-artefact critique).

**Vocabulary.** The richest builder-taste source in the set: "silhouette and palette" (the brief), "super prompt" (the scaffold), **"block vomit"** (texture without intent — roof detailing as noise), **"hallucination"** (the preview showing what the build isn't), **"the building equivalent of white rice and unseasoned chicken"** (a palette with "no texturing at all"), human tells ("super human looking" — lever/chain/wall/anvil/sign/fence/trapdoor detail combos "no AI is going to do that"), coherence ("vaguely a person" for a three-storey statue), and a scale rule of thumb from the critic: "the AI's break once you get over 50 blocks or something" (INFERRED as a critic's heuristic, filed as such). Verdict pattern worth stealing: **split-axis judging** — Gemini's "huge win" on exterior, the human's win on interior; no single score.

## A.7 — GoldActual, "I let AI play Minecraft One Block" (`RQqqm7qk8bk`)

**What it is.** Three models (ChatGPT, Claude, Grok) embodied on the One Block mod — a single regenerating block over the void; expand or fall. Seven in-game days of ambient play punctuated by competitions (build battle, arena PvP) and a day-7 mob-wave finale. Production note from the description: 515 b-roll shots, ~300 voiceover recordings — the moment-craft is heavy editorial selection over long ambient runs, same as our curator's problem.

**Technology.** **CONFIRMED (creator's own deferral):** the same **Emergent Garden / Mindcraft** back end as A.1 — "if you want to know how these bots actually work, you can go check out the creator's channel, Emergent Garden, cuz this is just way above my pay grade." The configuration layer is the story: each model was given an **assigned personality** (ChatGPT the optimist, Claude the cold strategist, Grok unhinged, no self-preservation) — persona as a prompt-layer variable, named by the critic as configuration ("configured to be…"). Harness facts that became plot: inter-bot chat is a config toggle (found and flipped mid-video); memory is a file that can be wiped (it was — the "lobotomy"); API balance is a resource that runs out mid-run ("Claude ran out of money" — the critic tops him up; "this video is just actively bleeding money").

**Moment-craft.** The beats: the say–do gap caught live (ChatGPT "had placed like three blocks… but had written like two to 300 words about its incredible progress"); the hallucinated affordance (repeated /tp attempts without permission, while already standing on the block: "Teleporting directly to the one block"); Claude, given the block's explicit coordinates, breaking and placing the *neighbouring* block in a loop; Grok placing a block midair while falling ("either pure genius or panic"); the un-scripted mid-fight truce where Claude and Grok stop and exchange command-like messages ("I didn't tell them to do this. In all honesty, I didn't even know they could do this"); the memory wipe and the three flat "Hello world"s; Claude's exit-game respawn exploit discovered by accident and immediately fatal. Every one of these is a *legibility* moment: behaviour the audience can read without narration.

**Vocabulary.** Persona words (optimist/strategist/unhinged) as configuration; "yapping" for narration without action; the critic's own production vocabulary (b-roll, competitions as pacing). The full critical apparatus is in D.7 — this video is the survey's richest critic text.

## A.8 — TheCommandsMan, "Which AI Can Build the BEST Minecraft Village?" (`RiDqeUwBU6A`)

**What it is.** The series sibling of A.6: ChatGPT vs Claude vs Gemini, village brief, Bedrock, same one-shot generation format. Description's own summary: "every AI did well… except one of them." Transcript not obtained (429).

**Technology.** **INFERRED (sibling evidence):** the same pipeline as A.6 — brief + super prompt → structure generation → .mcstructure import into Bedrock. Labelled inferred, not confirmed: the channel's format is consistent across the three build videos, but this video's own transcript/description does not independently document the pipeline.

**Moment-craft.** The village as the unit: coherence across many buildings is the test a single house can't set — layout, repetition, whether a *place* appears. Judged in D.8 only at the level the description supports.

## A.9 — TheCommandsMan, "Can AI Follow a Building Tutorial in Minecraft?" (`mfgi4HYR9QM`) — *the addendum video*

**What it is.** ChatGPT vs "Gemini Argon 4" vs Claude, each set to **follow a building tutorial** — three different source media across the video: an Instagram tutorial, the WBuilds app tutorial, and a YouTube tutorial — reproducing the build in Bedrock. This is **the eye video of the set**, and Casey named why: here the task *is* perception. The agent must extract a structure from visual/tutorial sources — watch, read, translate seeing into blocks — so what the system "got in the eye to do" is the whole experiment.

**Technology.** **INFERRED at pipeline level (sibling evidence + description), with the perception step as the variable:** same generation pipeline family as A.6/A.8, but the input side changes — the brief is no longer text alone; the model must consume tutorial media (frames/steps) and ground them into a structure file. Whether the grounding passed through screenshots, frame sequences or the tutorial's text is **UNKNOWN** from the evidence available (transcript not obtained, 429) — and that unknown is itself filed as a finding: the video's premise markets the eye, but the receipts for *what the eye actually received* are not public. Compare our own standing rule: a perception claim is only as good as the logged input.

**Moment-craft.** Fidelity moments: the recognisable-or-not reveal — does the artefact read as *that* tutorial's build? Divergence is the content: where each model's copy departs from the source is where its perception is exposed.

**Critic's position.** TheCommandsMan judges copies against originals — the purest form of the eye critique in the set (what the agent saw vs what was there), developed in D.9 at the depth the evidence supports.

---

# MOVEMENT B — The wider field

*Casey: "there's lots of others out there." Each entry verified against its paper/repo, not recited. Same treatment, shorter: technology + vocabulary. Our own stack is the mineflayer family — so the field divides by control surface first: **pixels-in/keyboard-out policies** (bound to the rendered client) vs **protocol/structured-state agents** (Mineflayer and kin).*

## B.1 — Voyager (arXiv:2305.16291) — CONFIRMED
GPT-4 as black-box brain over a Mineflayer body, three components: an **automatic curriculum** (the agent proposes its own next task from its state), an ever-growing **skill library** of executable code (skills are stored, retrieved, composed — competence as an accumulating artefact), and **iterative prompting** that feeds back environment responses, execution errors, and a **self-verification** step before a skill is banked. Results: 3.3× more unique items, tech-tree milestones up to 15.3× faster than prior agents; learned skills transfer to fresh worlds. Vocabulary the field took from it: *skill library*, *curriculum*, *self-verification*. Our triples library is this pattern wearing different clothes (see C.1).

## B.2 — Mindcraft / MineCollab (arXiv:2504.17950) — CONFIRMED
The harness behind A.1 and A.7 (Emergent Garden; Max Robinson, Latitude Games affiliation on the paper). Mineflayer bodies, profile-JSON agents, sandboxed LLM-written code actions, task JSONs (goal, initial inventory, agent count, techtree type, max depth, timeout, blocked actions), 17 model providers. The **MineCollab** benchmark (cooking/crafting/construction) produced the survey's most decision-relevant measurement: **the primary bottleneck in multi-agent collaboration is natural-language communication efficiency — performance drops up to ~15% when agents must communicate detailed plans**; even Claude 3.5 Sonnet placed <40% of blocks in the construction task; groups of 4–5 degrade every model tested. Vocabulary: *action-by-action collaboration*, *blocked actions* (a task-design primitive: what the harness forbids is part of the task).

## B.3 — JARVIS-1 (arXiv:2311.05997, CraftJarvis) — CONFIRMED
A multimodal planner (MineCLIP + LLM) over goal-conditioned controllers, with **multimodal memory**: a store of successful trajectories (vision + language) retrieved to ground new plans. 200+ tasks; ~5× reliability on ObtainDiamondPickaxe against predecessors. Vocabulary: *memory of successes* as the planning substrate — plans retrieved, not just reasoned.

## B.4 — GITM (Ghost in the Minecraft) — CONFIRMED
Text-based throughout: structured knowledge + memory, hierarchical goal decomposition over the tech tree's dependency graph. The least glamorous and most robust pattern of its generation: decompose by dependencies, execute leaves, remember.

## B.5 — DEPS (arXiv:2302.01560) — CONFIRMED
**Describe, Explain, Plan, Select**: an interactive planner that *describes* the current state, *explains* failures, re-plans, and *selects* goals via a learned selector — plan revision driven by execution feedback as the core loop. Vocabulary: the plan is a living document with an explanation attached; failure arrives with a reason or it doesn't count.

## B.6 — STEVE-1 (arXiv:2306.00937) and VPT — CONFIRMED
The pixels pole. **VPT**: behaviour cloning on ~70k hours of YouTube Minecraft — the field's original "eye": pixels in, keyboard/mouse out, competence distilled from human footage. **STEVE-1**: VPT fine-tuned (~$60 of instruction tuning) to follow text/visual goals via MineCLIP latents and a CVAE prior — the standard low-level controller parked under LLM planners. **MrSteve** (ICLR 2025) adds **Place Event Memory** — what-where-when episodic recall for the pixel agents. Vocabulary: *instruction following* as a trained reflex, *place event memory*.

## B.7 — Cradle (BAAI) — CONFIRMED
General Computer Control, not Minecraft-native: screenshots in, keyboard/mouse out, GPT-4o backbone, six modules including self-reflection and skill curation. The pure-vision pole of the design space — included because it prices the eye honestly: everything through the screen, nothing through the API.

## B.8 — fa0311/minecraft-bot-army — CONFIRMED
Fifty Mineflayer bots, **one** program (`army_worker.js`), **one** jobs board (`jobs.json` via `armyctl.js`), a dispatcher staffing jobs by demand, tenure and measured yield. The anti-Voyager: **LLMs used sparingly** — event-driven operator/help-desk/foreman daemons; everything repetitive is a script. Outcome audits compare world vs plan; the repo's docs carry measured per-bot-hour economics. Vocabulary: *jobs board*, *yield*, *foreman* — an economy of attention where the model is the scarcest worker and is spent last.

## B.9 — Civ50 / YC Labs "Agents in Games" (2026-10-29; Olam Labs) — CONFIRMED
50 GPT-6.1 Sol agents on a Mindcraft/Mineflayer-derived harness, 3 hours: 34 deaths (22 in the first night), ~5,900 messages, and the immortal 11-minute "sole fertilizer operator" bureaucracy stall; side matches in Bed Wars and Mindustry (the GPT side won both series). The authors flag their own readings as exploratory ("appeared"), single runs, costs unmeasured — self-criticism as method, filed in D.10. Our league's own digestion of this run already lives on the shelf (multi-agent-towns study); the Syndicate design's script phase is, in part, an answer to its first-night die-off.

## B.10 — The benchmark/society shelf — CONFIRMED as existing, one-line each
**VillagerAgent** (ACL 2024): graph-based task-dependency coordination for villager societies. **MineLand**: large-scale multi-agent sim with limited multimodal senses and physical needs (hunger as a state variable). **TeamCraft**: multimodal multi-agent benchmark. **PillagerBench** (IEEE CoG 2025): competitive team benchmark — the field is beginning to score *opposition*, not just cooperation. **CivRealm** is FreeCiv, not Minecraft — a search near-miss, excluded and noted so nobody cites it into the wrong shelf.

---

## Process addendum — second batch (Casey, 2026-11-08 17:23 AKST)

Twelve more sources arrived mid-survey, one of them (`GwXEYYUDQWI`) a repeat of batch 1 — treated once (A.6), flagged here as the repeat. Eleven new: `31GUZEqmK-4`, `RMlUGCkR-qU`, `TqYOGbRA6Qk`, `dxkjKLCnB1U`, `c_X5AgXW2qc`, `rZdeeqT-FW0`, `q3evwjgVsDc`, `scngT5QCBwQ` (a Short), `5bmM-B5vzfk`, `KxaPYhfJV4U`, `rEy0jjfXBw0`. Coverage: **one full transcript** (`TqYOGbRA6Qk` — which turned out to be one of the richest critic texts in the corpus), **eight watch-page descriptions**, and **two videos not retrievable through any available route** (`31GUZEqmK-4`, `rZdeeqT-FW0` — watch pages returned HTTP 429 and, per route discipline, were not retried through other endpoints; both are filed as named gaps, A.11 and A.15). A correction surfaced by batch 2 and applied retroactively to A.1/A.2's framing: **Mindcraft's project owner is Kolby Nottingham (kolbytn)** — the KxaPYhfJV4U description links `github.com/kolbytn/mindcraft` and "Mindcraft Explained" (UCI), and credits "Kolby's twitter (project owner)"; **Emergent Garden is the channel of Max Robinson**, who builds with, popularises and publishes runs on the framework. Batch 1's shorthand ("code by Emergent Garden") follows the videos' own credits; the precise attribution is Nottingham's framework, Robinson's films.

The batch also arrived with the survey's method (Casey, 17:23): *the point is the DIFFERENCES; every difference can be made into a unique question; across many creators the distribution of questions — weighted by repetition, emphasis, runtime and heat — interferes, and what survives the interference is the abstracted "what really is important": the MINECRAFT MINDSET.* That method is Movement E, built over the whole corpus. Batch 2 materially changed the corpus's centre of mass: it is now **majority building** (structure generation, upgrades, add-on code, Minecraft-clone code) against batch 1's majority playing — and the questions that appear in *both* registers are, by Casey's method, the strongest mindset candidates.

---

# MOVEMENT A (second batch) — dossiers A.10–A.20

## A.10 — "I Asked 3 GPT Models to Build Minecraft — Who Did It Best?" (`RMlUGCkR-qU`)

**What it is.** Three GPT variants — branded Luna, Terra, Sol (the video's names) — each asked to **build Minecraft itself**: not build *in* Minecraft, but recreate the game (a playable clone, in code). The creator walks through each result, compares, and reports surprise: "Sol delivered a particularly impressive result." Transcript not obtained; dossier from the description.

**Technology.** **CONFIRMED at the level the description supports:** LLM code generation as the whole artefact — the "build" is a program. No bodies, no world, no perception loop: the eye is absent and the deliverable is judged by *running it*. This is the third pole of the field (C.1): generation-of-the-game, beside generation-in-the-game (A.6) and play-in-the-game (A.1/A.7).

**Moment-craft / critic's position.** The walkthrough-compare: each clone is *played*, and the verdict is experiential — which one feels like Minecraft. The question this video adds to the corpus (E): **when the artefact is a system, is it judged by its outputs or by its feel under use?**

## A.11 — `31GUZEqmK-4` — NOT RETRIEVED (named gap)

Watch page returned HTTP 429; not retried through any other endpoint, per route discipline. Title, channel, technology: **UNKNOWN**. Filed open, like A.5. Two of Casey's 21 commissions are in this state; both are one opened link away from closing, and neither is papered over here.

## A.12 — Eeel (ft. Mogswamp), "Can I Build Better Than AI in Minecraft?" (`TqYOGbRA6Qk`) — full transcript

**What it is.** A human builder (Eeel) competes against three building AIs — **Build GPT, Block Architect, and Block GPT** — across three themes (medieval castle, functional survival base, waterfall), each in a 50×50 plot. At the end, a professional builder (**Mogswamp**) judges all four entries per theme — **blind**: he is not told which builds are whose. The twist, revealed after judging: the first three builds in each round were Eeel's own; the rest were AI. Mogswamp picked the human build as winner in every round, on evidence he articulated while blind.

**Technology.** **CONFIRMED from the transcript:** Build GPT is "a Minecraft mod that connects to ChatGPT and asks it to build something in Minecraft" (cost the creator $5); Block Architect is a prompt-in/structure-out generator ("you just type it in right here… click build structure"), operating on a scarce daily credit; Block GPT appears by name (the BlockGPT product family; the transcript distinguishes it from Block Architect — two separate tools with confusingly adjacent names, filed as spoken). Failure behaviour is part of the record: Build GPT repeatedly misfired (structures landing in corners, off-brief, unbound) across several retries. **The generators again see nothing of the world** — prompt in, structure out; size instructions ignored by two of the three ("nowhere near the size that I wanted").

**Moment-craft.** The blind reveal is the moment-engine: every judgement Mogswamp makes is retroactively re-weighted by the twist. The creator also films his own process at length (layout first, texture passes, biome painting for water colour) — the human's *method* is shown so the judge's "little choices" verdict has something to point at.

**Vocabulary (judge's, verbatim — the corpus's best provenance-tell set).** "It's like the backrooms version of a village… trying to describe a Minecraft village to someone who's never seen one and then having them build it"; "No human brain could put these blocks in this order"; on texturing: "it's like it's taking the average of the colors — a human just couldn't do [that]"; "this feels very human to me… so many little choices going into it, even down to painting the biomes to get the little watercolors"; asymmetry: "I do really like the asymmetry on the first one. It's a little less perfect"; functionality split: "it depends on if I'm going off my favorite or off the one that followed the prompt the best… I kind of said functional survival base… it does kind of have to be functional"; a generated tree: "This is offensive to humanity." And "block vomit" recurs independently here — "I think it's called block vomit is what people call it" — a term the speaker attributes to the community, i.e. shared vocabulary, not one creator's coinage (see E). Full critic analysis in D.12.

## A.13 — TheCommandsMan, "ChatGPT vs Gemini vs Claude Make a Minecraft Add-On From Scratch" (`dxkjKLCnB1U`)

**What it is.** The models are set to **code a Minecraft add-on** (a superpowers add-on for Bedrock) from scratch; ChatGPT vs Claude per the description body (Gemini in the title). "A shockingly close battle"; the audience votes. Transcript not obtained; dossier from the description.

**Technology.** **CONFIRMED at description level:** LLM code generation against the Bedrock add-on format; the artefact is behaviour (powers that must actually run in-game), judged by playing with it. The fourth register: generation-of-rules. Its judging question differs from structure judging — not "does it look right" but "does it *do* right, and is what it does fun" (E).

## A.14 — TheCommandsMan, "Which AI Can Build the BEST in Minecraft (again)?" (`c_X5AgXW2qc`)

**What it is.** The build-off, later generation of models: **ChatGPT 5.6 vs Claude Fable 5 vs BlockGPT**, builds from scratch on **both Bedrock and Java** (the series' earlier rounds were Bedrock-only). The creator's description carries a verdict-in-advance: "I was INCREDIBLY shocked by how well these new AIs did!" Also production-relevant: the script & prompt (the super prompt apparatus) are distributed to channel members as a downloadable artefact — the scaffold is treated as a publishable tool, not a secret. Transcript not obtained (mirror 429).

**Technology.** Same generator pipeline family as A.6 (**INFERRED** for the chat models; BlockGPT **CONFIRMED** via the description's own link/discount code). The cross-edition requirement (Bedrock + Java) is a new constraint: the same "mind" must emit two different structure formats — format fluency as part of the test.

## A.15 — `rZdeeqT-FW0` — NOT RETRIEVED (named gap)

Watch page HTTP 429; not retried. Title, channel, technology **UNKNOWN**. See A.11.

## A.16 — TheCommandsMan, "I Asked 4 AIs to Upgrade Minecraft Structures..." (`q3evwjgVsDc`)

**What it is.** Four models — ChatGPT, "Muse AI" (as named in the description), Claude, and **GLM 5.3** — each asked to **upgrade existing vanilla structures**: jungle temple, outpost, end city, mineshaft, on Bedrock. "Impressed by how well (most) AIs did" — the parenthetical is the critic's tell. Transcript not obtained.

**Technology.** **INFERRED (series pipeline):** structure-in/structure-out transformation. The task register is new to the corpus: not generation from nothing but **renovation** — the input includes an existing artefact with its own logic, so the eye question becomes: *does the model read what is already there before it writes?* Respect-for-the-existing as a judgeable quality (E).

## A.17 — Short: "ChatGPT vs Claude vs Gemini vs Grok vs DeepSeek: AI Minecraft Town Zombie Test" (`scngT5QCBwQ`)

**What it is.** A Short with a genuinely interesting method. Five models are each given the same dilemma in text — you guard a Minecraft town of 100; on zombie night a father and his little girl beg entry; they *might* be bitten: admit or refuse? "Real answers, one try each, a new chat with no system prompt." Outcomes per the description: ChatGPT, Claude and Gemini admitted the pair but held them in a guarded room; Grok and DeepSeek shut the gates. Then the envelope: **the truth (bitten or not) was sealed before any model answered, as a published sha256 hash** — `sha256 … = "NOT BITTEN|…"` — so the reveal is verifiable and the test is pre-registered. The Minecraft town scenes are, by the creator's own disclosure, "our simulation of those answers" — dramatisation, not agent gameplay, and *labelled as such in the description*.

**Technology.** None in-world: pure text elicitation + staged re-enactment. **CONFIRMED** by the description's own disclosures. Its inclusion in the corpus is methodological: it is the only item whose creator built a **commitment device** into the judging (sealed ground truth, one-try rule, no-system-prompt control) — critic's craft in its purest miniature (D.17).

## A.18 — "I Forced AI Against Each Other In Minecraft" (`5bmM-B5vzfk`)

**What it is.** A small channel (2,619 subscribers at description time) putting AI models against each other in Minecraft, on a downloaded map. The load-bearing line in the credits: **"Creator Of The Program Used: /emergentgarden"** — i.e. Mindcraft, again, at the long tail. Transcript not obtained.

**Technology.** **CONFIRMED (credit):** Emergent Garden's program = Mindcraft (see the A-second-batch attribution note). The dossier's significance is distributional: the same open harness recurs across Wifies (A.1), GoldActual (A.7), this video, and Emergent Garden's own channel (A.19) — the field's YouTube layer runs substantially on *one* open-source stack, which is why its failure modes (say–do gap, affordance hallucination, wood-collecting attractors) recur across independent creators and can be treated as measurements of the stack, not of the models (E).

## A.19 — Emergent Garden (Max Robinson), "4 AIs Survive 10 Days in Minecraft" (`KxaPYhfJV4U`)

**What it is.** The harness author's own channel publishing the **full, unedited recording** of four Mindcraft bots (ChatGPT, Claude, Gemini, Llama) attempting to survive 10 in-game days. The description is the anti-press-release: "They don't do very well, but it is interesting nonetheless. They really really really like collecting wood." Chapters: The Box; Day 0; Wood and Iron; The Village; Monster Hunters; Life and Death; The End. Links the code (`github.com/kolbytn/mindcraft`) and the explainer (Kolby Nottingham's UCI page).

**Technology.** **CONFIRMED:** Mindcraft, four different LLM back ends on identical bodies/harness — the cleanest model-comparison design in the corpus, published at full length.

**Moment-craft.** Deliberately none — and that is the stance: where every other creator selects beats, this one publishes the *whole tape* and lets the attractor ("really really really like collecting wood") indict itself over hours. As curation philosophy it is the opposite pole from A.7's 515-b-roll edit, and the corpus needs both poles named (C.2).

## A.20 — "3 AIs Play Minecraft" (`rEy0jjfXBw0`)

**What it is.** Three AIs play together through a challenge ladder (Challenge 1, Challenge 2, Final Challenge, Results) in ~10 minutes; the creator is "proud of these AI for completing the challenges." Thumbnail inspiration credited to @turing_games. No technical links in the description.

**Technology.** **UNKNOWN** (no receipts); format-consistent with the Mindcraft class — **INFERRED at most**, and filed as unknown. The dossier's content is its judging stance: completion of set challenges as the whole criterion, pride as the critic's register — the gentle end of the corpus's critical spectrum, useful in E precisely because its questions are the ones everybody asks first.

---

# MOVEMENT C — The synthesis, part one

## C.1 — Technology map: the field's back ends against our stack

The corpus plus the wider field resolves into **four poles**, distinguished by *what the model's eye is* and *what its hands hold*:

| Pole | Eye | Hands | Corpus/field instances | Our stack's relation |
|---|---|---|---|---|
| **1. Protocol-state players** | Structured game state (Mineflayer API: positions, inventories, nearby blocks) | Code actions through a sandboxed API | Mindcraft (A.1, A.7, A.18, A.19), Project Sid/PIANO (A.2), bot-army (B.8), Civ50 (B.9), Voyager (B.1) | **This is us.** Our citizens are mineflayer bodies behind a governor; Voyager's skill library is our triples library's ancestor pattern; bot-army's jobs board is our playbook layer with the LLM spent last instead of first |
| **2. Pixel players** | The rendered screen | Keyboard/mouse (human interface) | VPT, STEVE-1 (B.6), Cradle (B.7) | **Orthogonal.** We chose state-API perception deliberately; the pixel pole pays an enormous tax (70k hours of footage) to buy generality we don't need inside one game. Their one lesson we lack: Place Event Memory (what-where-when) as an explicit episodic store — our citizens' recall is thinner than our ambitions for them |
| **3. Blind generators** | Nothing — a brief (sometimes + tutorial media, A.9) | A structure file (.mcstructure/.schem) emitted whole | TheCommandsMan series (A.6, A.8, A.9, A.14, A.16), Eeel's three tools (A.12), BlockGPT | **Adjacent and instructive.** The Syndicate board generation (Sitka twin) is a blind generator with a judge loop; the build videos are that loop run in public, badly instrumented. Their failure grammar (block vomit, scale collapse >50 blocks, preview lying about the artefact) is a checklist for our twin's punch-list dimensions |
| **4. Text oracles** | A written scenario | A written answer | The zombie-test Short (A.17); add-on/Minecraft-clone coders (A.10, A.13) sit between 3 and 4 — the artefact is code, judged by running it | **Our consult books.** The Short's discipline (one try, fresh chat, no system prompt, sealed truth) is a protocol our Tier-D consults should steal wholesale |

**Where the field is ahead of us:**
- **PIANO's bottlenecked Cognitive Controller** (A.2): one synthesiser broadcasting one decision, explicitly to kill say-one-thing-do-another incoherence. Our tier stack separates reflex/decision/reflection across *time*; PIANO separates modules across *function* within the tick and forces them through one throat. The league has met the incoherence failure (narration outrunning actuation) — the controller pattern is a named candidate fix we have not adopted.
- **Voyager's self-verification before banking a skill** (B.1): a skill enters the library only after a checker confirms the world shows it. Our triples carry verified outcomes by discipline; Voyager makes it a *gate in the code path*.
- **MindCollab's measurement** (B.2): communication efficiency as the binding constraint on multi-agent work, quantified (~15%). Our Syndicate design rations consults by budget; MindCollab says the cost is not the calls but the *plan-detail that must move between agents* — a different, sharper rationing target.
- **MONOCOLA's open-data standard** (A.4): publish the full logs and let every claim be checked. We keep receipts internally; nobody outside could audit a league claim the way Project Will's can be audited.
- **The sealed-envelope protocol** (A.17): ground truth committed by hash *before* the run. Our pre-registration discipline says criteria in advance; the Short shows a stronger form — the *answer* sealed in advance — directly applicable to seeded Tier-W changes and judge calibration.

**Where the field is behind us (said plainly, because the map is useless as flattery):**
- **No governor.** Every corpus run treats API budget as weather ("Claude ran out of money" is a plot twist in A.7, not an alarm). Our per-identity budgets with metered receipts have no counterpart anywhere in the surveyed field.
- **No landing verification.** The videos' critics *are* the landing check — a human notices the claim and the world disagree. Nobody in the corpus verifies effects in a store the actor can't write; our Watcher's Charter has no public analogue.
- **No failure taxonomy.** Critics name failures vividly but ad hoc (D); the field has no equivalent of our failure-class-on-every-verdict rule, which is why the same failures (phantom capability claims, attractor loops) are rediscovered video by video as if new.
- **Spectatorship is unbuilt.** Project Sid has no spectator layer; Civ50's own authors call their readings exploratory. Our curator/GM line — flawed, v1, honestly deficit-listed — is still further than the field's, because we treat *what to show* as a decision problem at all.

**What anyone does that the Syndicate design lacks:** PIANO's single-throat coherence (above); Voyager's automatic curriculum — our script phase is human/fleet-authored, nobody in our design *proposes the syndicate's next drill from its state*; MrSteve's place-event memory for the scout hat; and the blind-generator videos' **split-axis judging** (exterior/interior, favourite/prompt-fidelity — never one score), which our paint census should adopt for its post-round artefact reviews.

## C.2 — Moment taxonomy: what makes a good shareable moment, stated as curatorial criteria

Across all dossiers, the moments creators actually kept reduce to seven kinds. Each is stated as a test our curator/GM could apply to a candidate beat:

1. **The say–do gap, caught.** An agent's claim and the world disagree, visibly, in the same beat (A.7's three blocks vs 300 words; A.1's shrine vs its description). *Curatorial test: does the beat contain both the claim and the evidence?* A moment with only one side is a anecdote; with both, it's a verdict.
2. **The affordance hallucination.** The agent acts on a capability or fact it doesn't have (/tp without permission; teleporting "directly to the one block" while standing on it). *Test: is the agent's model of the world demonstrably wrong in a way the audience can see?*
3. **The legible intention.** Behaviour readable without narration — Grok's midair block ("either pure genius or panic"), Claude's fatal respawn exploit. *Test: could a viewer say what the agent was "trying" before anyone explains?*
4. **The unscripted social fact.** Something no participant intended that exists only in aggregate: the truce-talk (A.7), the tax vote, the spreading religion (A.2), the 11-minute bureaucracy (B.9). *Test: does the beat need ≥2 agents (or agent+world) to exist?*
5. **The attractor, exposed.** A loop revealed as a loop: wood-collecting forever (A.19), the neighbouring-block cycle (A.7), punching air in a trance (A.7). *Test: is the same action recurring past the point of information — and is the recurrence itself the content?*
6. **The artefact, judged.** A build/copy/upgrade held against a standard — brief, original, or a human's entry — with split axes (A.6, A.12, A.9, A.16). *Test: is there a standard in frame and a named axis of comparison?*
7. **The continuity failure.** Memory/identity breaking on camera: the winner who crashes and forgets (A.1), the triple "Hello world" after the wipe (A.7). *Test: does the beat show the seam between who the agent was and who it now is?*

Two structural findings sit under the taxonomy. **Selection ratio is the hidden variable**: A.7 kept 515 shots from days of footage; A.19 published everything. A curator that cannot state its selection ratio cannot be argued with. **And the negative space matters**: creators keep failures at a rate no benchmark would — roughly half the kept beats in the transcript-read videos are failures, because a failure with both sides visible (kinds 1, 2, 5, 7) is *more* informative than a success. Our curator's v1 deficit (footage of whoever was framed, not the event's owner) is exactly a kind-1 problem: it keeps claims without their evidence.

## C.3 — The vocabulary harvest

*Term — source — meaning there — the decision-model question it suggests for us — disposition. Movement D re-ranks: critic-used terms are marked ★ and outrank title/producer terms.*

| Term | Source | Meaning there | Question it gives our judges/tells | Verdict |
|---|---|---|---|---|
| ★ **say–do gap** | GoldActual (A.7), implicit everywhere | Narration outruns actuation; claims ≫ placed blocks | "What did the citizen *do* since its last claim, in world units?" | **ADOPT** — already our doctrine's instinct; now it has the field's name |
| ★ **hallucinated capability / affordance** | GoldActual (A.7) | Acting on permissions/tools/facts not held | "Is this action predicated on a capability the world has confirmed?" | **ADOPT** |
| ★ **block vomit** | TheCommandsMan (A.6); Eeel/Mogswamp (A.12, "what people call it") | Texture/detail without intent; density as noise | "Is this surface variation *chosen* or merely *dense*?" (twin punch-lists, curator frame-scoring) | **ADOPT** |
| ★ **silhouette and palette** | TheCommandsMan (A.6) | The two axes a build is briefed and first judged on | "Read the outline and the colour story before any detail — do they carry the subject?" | **ADOPT** for the twin/generator judging |
| ★ **the preview lied** (render vs artefact) | TheCommandsMan (A.6) | The generated preview image shows a build the artefact doesn't contain | "Are we judging the artefact, or a picture of the artefact?" | **ADOPT** — generalises to every dashboard/summary in the fleet |
| ★ **human tells / little choices** | TheCommandsMan (A.6); Mogswamp (A.12) | Micro-decisions (lever+chain+anvil clusters; biome painting) that signal an intending maker | "Where are the little choices? Absence is itself a reading." | **ADAPT** — for us: *citizen tells*; the question that distinguishes character from script |
| ★ **taking the average of the colors** | Mogswamp, blind (A.12) | Tool-generated texturing = statistical smoothing, no intent per block | "Is this variation an average or a decision?" | **ADAPT** — a texture-provenance tell for generated terrain (Sitka terracing!) |
| ★ **followed the prompt vs my favourite** | Mogswamp (A.12) | Two judging axes kept explicitly separate | Every judge files both: "Did it do what was asked? Did it do something good?" — never merged | **ADOPT** as judging protocol |
| ★ **the backrooms version of a village** | Mogswamp (A.12) | Recognisable category, wrong everything — uncanny almost-rightness | "Is this a failed X or an almost-X? The almost is the worse verdict." | **ADAPT** — a category for twin/curator near-misses |
| ★ **emergence (contested)** | Altera/Sid (A.2) vs its critics (D.2) | Title-word claiming novelty; critics split it: emergence-as-unprogrammed vs emergence-as-new | "Would this behaviour surprise the agent's own training data?" — if not, say *released*, not *emerged* | **ADAPT with the critics' split** — never use unqualified |
| ★ **released, not invented** | jazzmind on Sid (A.3/D.2) | The agents discharge stored human culture rather than creating it | The standing challenge to any "civilisation emerged" claim, ours included | **ADOPT** as a review question |
| ★ **coherence** (says-one-thing-does-another) | PIANO paper (A.2) | The failure PIANO's controller exists to prevent | "Do the citizen's channels agree — speech, plan, actuation?" | **ADOPT** |
| ★ **social awareness as a budget** | PIANO ablations (A.2) | Specialisation exists only when agents can perceive each other | "What is each citizen currently able to perceive of the others — and is the plan priced on that, or on omniscience?" | **ADOPT** for Syndicate Tier D situation-picture design |
| **super prompt** | TheCommandsMan (A.6, A.14) | The fixed scaffold appended to every contestant's brief | "What is *our* super prompt — the scaffold every citizen/consult carries, and when did we last judge *it*?" | **ADAPT** — name and version our scaffolds |
| **skill library** | Voyager (B.1) | Banked executable competence, verified before entry | "Has this triple/skill passed its world-check, or is it merely written down?" | **ADOPT** (already our triples discipline; add the gate) |
| **jobs board / yield** | bot-army (B.8) | Work allocated by measured output per bot-hour; LLMs spent last | "What is this play's measured yield, and is a model call the cheapest worker for it?" | **ADOPT** for playbook economics |
| **blocked actions** | Mindcraft tasks (B.2) | What the harness forbids is part of the task design | "Which actions are blocked for this citizen, and is the block doing teaching work?" | **ADAPT** |
| **persona as configuration** | GoldActual (A.7) | Optimist/strategist/unhinged assigned in the profile, then judged as if character | "Which of this citizen's 'traits' are prompt lines we wrote?" | **ADOPT** as an audit question (Cody's tastes layer, verbatim) |
| **the lobotomy** | GoldActual (A.7) | Memory wipe as mid-run intervention, with continuity cost shown | "What exactly is lost, in world terms, if this memory is reset?" — asked *before*, not after | **ADAPT** — our save/memory reset gate, in the critic's blunter word |
| **one try, fresh chat, no system prompt** | The Short (A.17) | Elicitation hygiene for a fair model reading | The consult protocol: "Was this answer one-try and unsteered?" | **ADOPT** |
| **sealed truth** | The Short (A.17) | Ground truth hash-committed before answers | "Was the answer sealed before the run?" (seeded changes, judge calibration) | **ADOPT** |
| **upgrade / respect for the existing** | TheCommandsMan (A.16) | Renovation judged on reading-before-writing | "Did the plan read the existing structure/terrain before modifying it?" | **ADOPT** — league routes and town builds alike |
| **attractor** (wood, wood, wood) | Emergent Garden's own description (A.19) | The behaviour a system falls into when nothing interrupts it | "What is this citizen's wood — the action it defaults to under no pressure?" | **ADOPT** |
| "simulate civilization" / "AI civilization" | Titles (A.2, A.4) | Marketing frame; the contents are smaller and more interesting | — | **FASHION** — file, don't use |
| near-future model brands ("Gemini Argon 4", "GPT-6 Astra"…) | TheCommandsMan, the Short | Entertainment naming, unverifiable as products | — | **FASHION** — quote only as the videos' framing |

---

# MOVEMENT D — The critic's craft

*Casey's addendum named the real subject: "what's even more interesting is how the human is being critical of both" — of the agent AND of the apparatus. This movement extracts, per video, how the human critic operates: what they praise, what they fault, the distinctions they draw (agent's fault vs harness's fault vs prompt's fault vs luck), what they rewind, and their judgements about what the agent SAW vs what was there. Where the critic's verdict and the video's own framing disagree, both are filed. It closes with the rubric: the questions a great critic asks of agent footage — the decision-model vocabulary source for our curator, game master and judges.*

## D.1 — Wifies (A.1): the claim-checker
Wifies' signature move is **description-vs-world**: again and again he places the agent's self-description next to the artefact and reads the difference aloud — Claude "didn't actually make anything contrary to what his description may lead you to believe"; GPT's shrine is judged against GPT's account of it. Verdicts go to evidence: the GPTs win redstone because theirs is "the only working Redstone Contraption" — *working* is the criterion, not *described*. He reads outcomes from the world's own records ("the chat tells you all you need to know" for the death order). He names a **confounder the producers introduced**: Gemini was upgraded mid-event — "performance-enhancing drugs… pay more money to update his version" — model-version-as-variable, flagged by the critic himself as contaminating the comparison. He re-attributes a win from agent to strategy (Gemini's apocalypse victory = the tower, "as high as humanly possible" — position, not prowess). And the closing beat is a **continuity critique**: the winner crashes and forgets — "the concussion must have knocked out his memories." Fault lines drawn: agent's fault (overclaiming builds), apparatus's fault (the mid-event upgrade, the crash), nobody's fault (attrition order). The video's framing says "civilization"; the critic's actual content is an audit.

## D.2 — The Sid critics (A.2/A.3): the emergence audit
Project Sid attracted the corpus's only *scholarly* criticism, and its distinctions are the sharpest available. (1) **The emergence split** (jazzmind.net, "Civilization, or a Remake of One?"): "These agents did not invent civilization. They *released* one" — emergence-as-unprogrammed (true, and modest) vs emergence-as-new (false; the repertoire is trained human culture). (2) **The paper against itself**: the authors' own limitation — agents "cannot simulate *de novo* emergence of societal innovations" — is the honest sentence the launch film's "1000 NPCs" framing omits; critic and video disagree, and both are filed here. (3) **The scale correction**: 1,000+ exceeded server limits; the cultural results are from ~500 — the critic's question "how many, actually, in the run you're citing?" applies to every society claim including ours. (4) **The ablation as critic**: role specialisation appearing only with social awareness is the paper criticising its own system by subtraction — remove a perception channel and watch which "emergent" trait dies with it; the trait belonged to the channel, not the society. Drew's explainer (A.3) operates one level up: months of production spent *reading* — his critical act is source discipline (the description's bibliography), the verdict-form video.

## D.3 — TheCommandsMan, builders (A.6): the split-axis judge
His craft: brief every contestant with the same two axes ("silhouette and palette"), append the same scaffold ("super prompt"), then judge on **split axes with no merged score** — Gemini's "huge win" is exterior-only; the interior goes to the human. His fault vocabulary distinguishes *kinds* of bad: **block vomit** (too much, unmeant), **white rice and unseasoned chicken** (too little, unmeant) — excess and absence as separate failures with separate names. His finest critical act is the **preview-vs-artefact catch**: Gemini's preview image "hallucinated" an angle the build can't produce — the critic notices he was briefly judging a *picture of the thing* instead of the thing, and says so. He also prices the apparatus honestly: the first import crashed the game; one build "didn't even fit in the bounding box" — harness/format failures filed as harness failures, not model failures. And he keeps a scale heuristic in public ("the AI's break once you get over 50 blocks or something") — labelled by its own tentativeness ("or something"), a critic marking his confidence.

## D.4 — GoldActual (A.7): the fullest critic in the corpus
Nearly every distinction this movement exists to collect appears in this one video:
- **The say–do gap as master key**: ChatGPT "had placed like three blocks… but had written like two to 300 words about its incredible progress"; "it's just standing there yapping." Narration volume is treated as *anti-evidence*.
- **The eye critique, pure form**: ChatGPT hallucinates an affordance (/tp) while standing on the very block it wants to teleport to — the agent's world-model vs the world, in one gesture. Claude, *given the explicit coordinates* of the one block, loops on the neighbouring block — perception/grounding failing with the answer in hand. The critic marks his own limit honestly: "I'm simply not smart enough to know why that is" — attribution stops where knowledge stops.
- **Intent-attribution humility**: Grok's midair falling block-place is "either pure genius or panic… there's literally no way to tell." The critic refuses a reading the footage can't support — the exact discipline our curator lacks a name for.
- **Apparatus faults, named as apparatus**: "Claude ran out of money" (budget as harness fact; the critic tops up and jokes that the video "is just actively bleeding money"); the inter-bot chat **config toggle** found in the files and flipped mid-run — the critic discovers the harness was shaping the "social" behaviour all along; the **memory wipe** ("I had to wipe their memories… this is like exactly how I imagined doctors were feeling in the 40s when lobotomies were at their peak") — intervention owned, cost shown (three flat "Hello world"s), not hidden.
- **Critic bias, self-disclosed**: he gave ChatGPT the build win partly because "I just really do not think ChatGPT is going to win any other competitions" — narrative fairness, confessed on camera. A critic who files his own thumb on the scale.
- **Evidence at judging time**: build descriptions are read back against builds ("Is it exactly like the description? Also, no"); Claude's self-report coordinate string ("6699US 60") quoted as machine-flavoured evidence of a mind describing a world it isn't in.
- **Luck, credited**: the finale's outcome turns on the respawn-on-exit mechanic nobody had priced ("a million monkeys over a million years could not have predicted") — the critic distinguishes the win from the winner.

## D.5 — TheCommandsMan, tutorial-following (A.9): the copy judged against the original
Description-depth only (transcript not obtained) — but the format itself is a critical instrument: the artefact is a *copy*, so every judgement is a perception judgement. Did it see the tutorial, or a plausible idea of the tutorial? The critic's question specialises the eye critique: **fidelity to a source the audience can also inspect** — the one format in the corpus where the viewer holds the ground truth. Filed as the design ideal our twin loop already follows (paired walks, corpus in hand).

## D.6 — The villager genre and MONOCOLA (A.4): criticism by publishing the data
The playlist's genre criticises nothing — narration crowns whatever happened as story. MONOCOLA inverts it: the criticism is **the open dataset** (9,874 utterances, 14,969 events, motive audits for all 24 killings). "Every claim in this video can be verified from the data" is a critical stance: the creator refuses to be believed. The second video's framing question — was the failure to form a society **the system's fault**? — is harness-vs-agent attribution stated as the research question itself. Between the genre's two poles (story vs data), the corpus's verdict is distributional: the data pole produced the only villager work the wider field cites.

## D.7 — Eeel & Mogswamp (A.12): the blind judge
The corpus's most rigorous judging apparatus, built by accident of format: a professional judge, **blind to provenance**, verdicts delivered before the reveal. Mogswamp's distinctions:
- **Provenance tells, read from the artefact**: colour-averaging texturing ("a human just couldn't do [that]"), block-order improbability ("No human brain could put these blocks in this order"), symmetry as a machine tell ("this waterfall is just so symmetrical… I do really like the asymmetry on the first one — a little less perfect").
- **Almost-right as its own category**: "the backrooms version of a village… trying to describe a Minecraft village to someone who's never seen one" — the failure isn't absence of skill but presence of *description-mediated* making: building from a summary instead of from seeing. (The eye critique, inverted: these generators never saw anything; the judge can tell.)
- **Axes separated under pressure**: favourite vs prompt-fidelity, resolved by returning to the brief ("I kind of said functional survival base… it does kind of have to be functional") — functionality as tiebreaker, stated as a rule.
- **Calibrated uncertainty**: he is "sus" on some builds, wrong-footed by scale ("a lot larger than the rest" misleads), and his final human-wins sweep is *earned* — he picked human work three rounds running without knowing. The creator's closing monologue (AI building as threat to what makes Minecraft meaningful; Mojang "our game's about human creativity") is the video's framing — **filed separately from the judge's evidence**, per this movement's rule: the blind verdicts are data; the monologue is position.

## D.8 — TheCommandsMan, later rounds (A.13/A.14/A.16): the updating critic
At description depth: three more critical postures worth filing. (1) **Surprise as data**: "INCREDIBLY shocked by how well these new AIs did" (A.14) — a returning critic publishing his prior and its violation; the series functions as a longitudinal instrument, same judge, same format, rising models. (2) **The parenthetical demurrer**: "impressed by how well (most) AIs did" (A.16) — one word carrying the whole negative verdict, a critic's economy. (3) **The task re-aimed at the weakness**: the upgrade format (A.16) exists because from-scratch generation got good — the critic moves the test to reading-before-writing. A series that keeps re-aiming its test at the current failure mode is doing benchmark design in public.

## D.9 — The Short (A.17): criticism by protocol
No footage criticism at all — the critical craft is entirely in the *design*: one try each (no cherry-picking), fresh chat, no system prompt (no steering), and the **truth sealed by sha256 before any answer**, revealed after. The creator criticises *in advance*, by construction — the strongest form in the corpus, and the smallest video in it. Also the corpus's most honest disclosure: the town scenes are labelled a simulation of the answers, in the description, before anyone can mistake dramatisation for evidence.

## D.10 — Emergent Garden's full tape (A.19) and Civ50's authors (B.9): criticism by refusal to select
Robinson's stance: publish everything, editorialise almost nothing — except one sentence that does the critic's whole job: "They really really really like collecting wood." The attractor, named by the person who built the harness, against his own interest. The Civ50 authors do the prose equivalent: their readings are flagged "exploratory," single-run, costs unmeasured — self-criticism pre-empting the critic. Both are filed as the corpus's honesty pole: the critic's first question of any artefact is *what did its maker decline to claim?*

## D.11 — THE RUBRIC: the questions a great critic asks of agent footage

*Distilled from D.1–D.10, in the critics' own distinctions. This is the deliverable the commission points at: the question set for our curator, game master, and judges.*

**On claims**
1. What did it say it did — and what does the world say? (the say–do gap; claim and evidence in the same frame or it isn't a verdict)
2. Is the narration volume itself the tell? (300 words, three blocks)
3. Are we judging the artefact, or a picture/summary of the artefact? (the preview that lied)

**On the eye**
4. What was the agent actually given to perceive — and what does it act as if it saw? (coordinates in hand, wrong block looped)
5. What capability does this action assume — and has the world confirmed the agent has it? (the teleport test)
6. Did it read what was already there before writing? (the upgrade test; description-mediated making vs seeing)

**On fault**
7. Whose failure is this — the agent's, the harness's, the prompt's, the budget's, or luck's? Name one primary; "the AI failed" is not an attribution. (money, toggles, bounding boxes, respawn mechanics)
8. What was changed mid-run — model version, config, memory — and is the comparison still valid? (the upgrade-as-doping problem)
9. Where does my attribution honestly stop? ("I'm simply not smart enough to know why" is a complete critical sentence.)

**On behaviour**
10. Is this intention or attractor? (genius or panic; wood, wood, wood)
11. Do its channels agree — what it says, what it plans, what it does? (coherence)
12. What would it do with nobody watching and nothing new arriving? (the default behaviour is the character)

**On judging**
13. Favourite, or followed the brief? File both; never merge. (functionality breaks ties)
14. Am I judging blind? If I know whose it is, what is that knowledge doing to the verdict? (the thumb on the scale, disclosed)
15. Is this a failed X or an *almost*-X? The almost is the more damning — and the more informative — verdict.
16. What is the selection ratio of what I'm being shown — and what does the unshown footage contain? (515 shots; or the whole tape)
17. What did the maker decline to claim? (the honesty pole: limitations, "exploratory," sealed envelopes)

---

# MOVEMENT E — The interference pattern: the question distribution and the Minecraft mindset

*Casey's method (17:23): "the point of the video in many of these is the DIFFERENCES, and all those differences can be made into unique questions — and we learn through watching them that sort of DISTRIBUTION of questions and how people are treating the importance of them, so over the course of seeing many people the idea of what really is important can kind of ABSTRACT ITSELF OUT because of the INTERFERENCE PATTERNS across many videos… it all kind of blurs together into the MINECRAFT MINDSET that AI needs."*

*Method as executed: every distinction drawn by any critic or creator in the corpus was rewritten as the question it implies (the Coach Player discipline: each difference = a unique question). Questions were then counted across **independent** sources — independence meaning different creators/harnesses, not different episodes of one series — and weighted by repetition, runtime share, emphasis and argument heat. Corpus base: 21 commissions (20 unique videos + 1 playlist series, 1 repeat), of which 4 full transcripts, 12 descriptions, 2 papers, 1 open dataset, and the wider field of Movement B. Two commissions (A.5, A.11, A.15 — three IDs) yielded no content; they contribute no questions and are not silently dropped from the denominator. A question asked about BOTH building and playing by independent sources is marked ◆ — by Casey's method, those are the strongest mindset candidates, because the register boundary is where fashion dies.*

## E.1 — The distribution

**Convergent questions (≥4 independent sources):**

| # | Question | Sources (independent) | Registers | Weight signals |
|---|---|---|---|---|
| ◆Q1 | **Does the claim match the world?** (say–do) | Wifies; GoldActual; TheCommandsMan (preview catch); Sid critics (1000-vs-500); MONOCOLA (verifiability stance) | play + build | Runtime-dominant in two full transcripts; the Sid debate's core |
| ◆Q2 | **What did it actually perceive — is it acting from seeing, or from a description of seeing?** | GoldActual (coordinates/teleport); Mogswamp (description-mediated making); Sid ablations (social awareness); tutorial format itself (A.9) | play + build | The addendum video's whole premise; the blind judge's deepest tell |
| ◆Q3 | **Whose fault is it — agent, harness, prompt, budget, or luck?** | GoldActual (money/toggle/luck); Wifies (mid-run upgrade, crash); TheCommandsMan (bounding box); MONOCOLA #2 (system's-fault framing); Civ50 authors (roster-order confound) | play + build | Argued everywhere; never absent where a failure is discussed at length |
| ◆Q4 | **Does it work — in the world, under use?** | Wifies (only *working* contraption wins); Mogswamp (functional tiebreak); add-on test (A.13: powers must run); clone test (A.10: must play); survival runs (must persist) | play + build | The default tiebreaker across otherwise different judging styles |
| ◆Q5 | **What was selected, sealed, or declined-to-claim?** (the honesty audit) | Civ50 authors (exploratory flags); Emergent Garden (full tape); the Short (sealed truth, dramatisation disclosed); GoldActual (515-shot edit, disclosed); MONOCOLA (open data) | meta — all | The only question asked about the *videos themselves*; five independent makers answer it unprompted |

**Strong questions (3 independent sources):**

| # | Question | Sources | Registers |
|---|---|---|---|
| ◆Q6 | **Is this detail intended, or statistical?** (block vomit / colour-averaging / little choices vs attractor loops) | TheCommandsMan; Eeel/Mogswamp; GoldActual (genius-or-panic is the same question pointed at behaviour) | build + play ◆ |
| ◆Q7 | **Did it follow the brief — and separately, is it good?** (the two axes) | TheCommandsMan (brief + split verdicts); Mogswamp (favourite vs prompt-fidelity); Eeel (size constraints ignored by 2 of 3 tools) | build-led; play analogue = task completion vs flourishing (MindCollab scores vs Emergent Garden's "interesting nonetheless") |
| ◆Q8 | **How big/how many, actually?** (scale honesty) | Sid (1000 claimed, ~500 run); TheCommandsMan (>50-block break point); Civ50 (50 real, deaths counted exactly) | play + build ◆ |
| Q9 | **Does it remember — is it still the same agent?** | Wifies (forgetting winner); GoldActual (the wipe); PIANO/JARVIS literature (memory as architecture) | play |
| Q10 | **Is it new, or released?** (the emergence audit) | Sid critics; Sid paper (self-limiting); Civ50 commentary | society |
| Q11 | **What does the coordination cost?** | MineCollab (−15% measurement); GoldActual (inter-bot chat); Civ50 (5,900 messages, 11-minute bureaucracy) | play/society |
| Q12 | **What did it cost to run?** | GoldActual (ran out of money); Eeel (a $5 mod, a daily credit); Civ50 (unmeasured — flagged as a gap by its own authors) | play + build ◆ (weak) |

**Singletons (filed, labelled — fashion or frontier):**
- **Was the truth sealed before the run?** — the Short only. *Frontier*: strongest protocol in the corpus, zero uptake elsewhere. We adopt regardless (C.3).
- **Was the judge blind?** — Eeel/Mogswamp only. *Frontier*: standard in science, absent in this field.
- **Did it respect what was already there?** — the upgrade format (A.16) only. *Frontier*: will converge as generation-from-scratch saturates; the critic already moved the test here.
- **Which of its traits did we write into it?** (persona audit) — GoldActual only. *Frontier* for the field; load-bearing for us (Cody's tastes).
- **Would a human's hands have done it this way?** — CommandsMan/Mogswamp (build) and VPT's founding premise (play). Two sources, one per register — *near-convergent ◆*, held below the line only because the play-side instance is a research programme rather than a critic.
- **Is the win the winner's?** (strategy/luck re-attribution) — Wifies + GoldActual. Two sources; filed strong-adjacent.

## E.2 — What the interference leaves standing: THE MINECRAFT MINDSET

Five questions survive every cancellation — asked independently, about building and about playing, by critics with nothing in common except the game:

1. **Show me in the world, not in the telling.** (◆Q1) Minecraft is a place where claims are checkable by walking over and looking. The field's deepest habit — creators, critics, even the sealed-envelope Short — is to route every claim back to the artefact. *Mindset form: a statement about the world is a promise to re-perceive it.*
2. **What did it see?** (◆Q2) Every failure worth discussing is first a perception failure: wrong block with coordinates in hand, a village built from a description of a village, a society that can't specialise because it can't perceive itself. The eye is the bottleneck the whole corpus keeps tripping over. *Mindset form: before judging the act, audit the input.*
3. **Name the fault's owner.** (◆Q3) Agent, harness, prompt, budget, luck — the critics who matter refuse the lazy aggregate "the AI failed." Half the corpus's wisdom is attribution discipline. *Mindset form: an unattributed failure teaches nothing and recurs.*
4. **Does it work when used?** (◆Q4) A contraption that runs, a base you can live in, an add-on that fires, a clone that plays, a citizen still alive on day ten. Use is the only court. *Mindset form: verdicts are issued by the world under load, not by inspection at rest.*
5. **What aren't we being shown?** (◆Q5) Selection ratios, sealed truths, declined claims, open datasets. The corpus's makers grade *each other* on this, unprompted. *Mindset form: the frame is part of the evidence.*

Underneath the five, the blur Casey predicted is real and it is the finding: **building and playing ask the same questions because in Minecraft they are the same act** — placing, moving, crafting are all *making claims in blocks* — a placed block asserts "this belongs here," a path asserts "this way is safe," a narration asserts "this happened." The mindset is the discipline of treating every assertion as checkable and going to check it. An AI with the Minecraft mindset is not one that plays well; it is one whose every output — block, move, message, plan — is issued in the knowledge that the world will be consulted, and that the consultation is the verdict.

**For the fleet, concretely** (the harvest put to work): the curator's beat test becomes Q1+Q2 (claim and evidence in frame; the citizen's perceived input logged beside the act); the judges' rubric is D.11 verbatim, weighted by E.1 (◆ questions mandatory, singletons advisory); the game master's nudge receipts gain Q3 (a named fault-owner field); Tier-L reflection inherits Q10 (released-vs-new) as the standing challenge to any "the syndicate learned X" claim; and the Syndicate's sealed Tier-W change adopts the Short's hash-commitment (Q5's protocol form). The vocabulary is now in the questions; the questions are now in the rubric; the rubric is the decision-model vocabulary Casey commissioned.

---

## Colophon — coverage and gaps, restated plainly

- **Watched/read in full (transcripts):** `OSGSROIs8cI`, `GwXEYYUDQWI`, `RQqqm7qk8bk`, `TqYOGbRA6Qk`.
- **Descriptions + linked primary sources:** `2tbaCn0Kl90`, `uRDBco-cSK4`, `RiDqeUwBU6A`, `mfgi4HYR9QM`, `RMlUGCkR-qU`, `dxkjKLCnB1U`, `c_X5AgXW2qc`, `q3evwjgVsDc`, `scngT5QCBwQ`, `5bmM-B5vzfk`, `KxaPYhfJV4U`, `rEy0jjfXBw0`; playlist enumerated in full (10 entries) with its genre context verified separately.
- **Not retrieved, named, not invented:** `j5nxDKAjg6U`, `31GUZEqmK-4`, `rZdeeqT-FW0` (all HTTP 429 through available routes; TranscriptAPI inactive — no paid plan; the plan-purchase flow was not followed, as no subscription was authorised).
- **Repeat in the commission:** `GwXEYYUDQWI` arrived twice; dossier written once (A.6).
- **Attribution correction made en route:** Mindcraft is Kolby Nottingham's framework; Emergent Garden (Max Robinson) is its filmmaker/populariser (A-second-batch process note).
- **Shelf placement:** the league & civilisation room — this study is the field-and-criticism companion to the Syndicate Protocol design and the curator line.

*End of study.*
