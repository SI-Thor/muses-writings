# The MTO Agent, graded — one boss, a crew of workers, and two different brains that never write

*2026-11-08 · Comparison assessment of "Build an MTO Agent: One Boss, a Crew of Workers, and a Brain That Never Writes" (LinkedIn Pulse, TomGor / Hu Zhaoji, published 2026-11-08) against the fleet's own stack — commissioned by Casey the day it appeared: "this seems similar to our idea — are they doing anything exceptional here?"*

**EVIDENCE GRADE: FULL TEXT.** The LinkedIn page was fetched entire (363 lines, all eight parts plus the closing) on 2026-11-09 ~02:55 UTC, within minutes of Casey's submission. Every claim attributed to the article below traces to that text. Two of its three components were independently corroborated: DeepSeek's `dsh-superagent-prototype` via our own Batch 1 deep-learn (§13, which read the repo in October) and fresh third-party coverage; Laya via the model card ecosystem, an independent explainer (laya.studio), a third-party skills repo, and a developer's calibration tutorial (cryptonwz). The third component, MTO, is the author's own framework and has no artefact outside the article — graded as such. Nothing in this study rests on snippets.

**The short verdict.** No — nothing exceptional, with one genuinely interesting artefact inside. The article is a competent *assembly*: three real open-source parts (an organisation layer we had already read and priced in October, a three-word trust checklist, and a judgment model) packaged for advertising agencies by a practitioner. Its slogan collides with ours but names a different invariant — theirs is a brain that never *generates*; ours is a brain that never *gates or writes the record*. The collision is worth a document precisely because the two are easy to confuse, and because convergence on the shape — boss, crew, criteria, fast nods — from an unrelated industry, in the same week, is itself evidence the shape is real. The one piece we had not previously digested is **Laya**: an open-weights, locally runnable decision model in exactly Jev's class, pitched against Jev — which makes it a live candidate behind our provider seam, and its published failure modes are unusually honest. One steal, one checklist, one routing pattern, below.

---

## 1. Their design, in its own terms

The article's own framing: an MTO Agent "that can actually do client work is not a chat box wired to an LLM." It needs three layers at once:

| Layer | Question | Part |
|---|---|---|
| Organization | Who takes the job, who does the work, how they run in parallel | **Super-agent** (DeepSeek `dsh-superagent-prototype`) |
| Criteria | On what grounds do we say this brand is worth trusting | **MTO** — Machine Trust Optimization |
| Judgment | Should we move, this second | **Laya** (Convai Innovations) |

Miss one, the author argues, and it doesn't work: no organisation → a fancy chat box; no criteria → "the faster the Agent works, the less the client believes it"; no judgment layer → "every nod costs an LLM call: slow, expensive, and prone to making things up."

**An honesty note on the title.** "MTO" names only the middle layer — a *marketing* discipline (making a brand's evidence chain machine-verifiable so AI recommenders can trust it). The headline "Build an MTO Agent" is packaging: the agent architecture is Super-agent's, the judgment is Laya's, and MTO supplies the criteria the workers' external statements must satisfy. A reader who expects MTO to be a software component will not find one; there is no MTO code, repo, or artefact in the article.

### 1.1 Super-agent — the organisation layer

Open-sourced 2026-10-31 by DeepSeek's Harness team, MIT, explicitly "a research prototype, not a shipping product" (the article says this plainly — credit where due). Its stated problem: "Models increasingly complete single tasks without human intervention. The bottleneck has become how many sessions a person can watch at once. One person can typically follow 3–5 active sessions."

Two roles:

- **Router** — always on; takes every human message, holds the global context, assigns work. "It does no execution itself; it doesn't even need tools attached." A counter-intuitive finding the article relays: a lightweight model suffices for the Router; only Workers need the strongest model, "because the Router dispatches, it doesn't create."
- **Worker** — one per ticket; fully isolated context, tools loaded, one job; delivers a report when done; "never speaks to the outside world directly."

Three designs the article pulls out:

1. **Two-stage filtering.** A deterministic program layer filters most noise (source, group, whitelist); surviving candidates go to a model applying policy. (This is the slot Laya later fills.)
2. **Subscription pass-through.** Once a Worker owns a PR, it subscribes to that thread directly; follow-up comments route to it *by code*, bypassing the Router. Result claimed: ~30% fewer Router decisions; without pass-through, cached-token reads burn 37% more.
3. **Context as a cache.** High-frequency info inlined; long content truncated with a "continue reading" handle; every object inlines the ID of its next hop. Their line: "Wasting context window is wasting model intelligence."

Results as reported: ~300 messages, 20 work requests, 5 runs per group; two-layer p50 12.4 min / p95 15.7 min vs single-session p95 29.5 min (single-session p50 not reported — the table shows "—"). The article's gloss: across 5 runs the single-session setup "never once called a Subagent on its own. Not incapable. It just doesn't know how to split the work by itself."

Operating notes: plugin for DeepSeek Harness; needs Node 22+, pnpm, git, GitHub CLI, and a *dedicated* GitHub account for the agent. Permission warning carried honestly: it runs at full privileges by default under your system account; official guidance is a separate system account, whitelist-only at first, observation mode before autonomy, and "don't rush to enable auto-merge — the official recommended answer is no."

*Fleet corroboration:* Batch 1's §13 read the repo itself in October and priced what the article doesn't: the p95 win costs **~3.8× cache-read tokens**; the benchmark traffic is synthetic with simulated tools and real coding quality unmeasured (DeepSeek's own disclaimer); the repo and its design essay diverge (some essay ideas are unimplemented future directions). The article repeats the headline numbers without the token price or the synthetic-traffic caveat.

### 1.2 MTO — the criteria layer

"Machine Trust Optimization. In one line: make your evidence chain verifiable and trustworthy to a machine." Not "make the AI like you" — make it able to *find something checkable* when comparing prices, shortlisting vendors, or recommending media. Three hard metrics:

1. **Verifiable** — does your data have a source, or is it "our research shows"?
2. **Reproducible** — can someone else, using the same method, arrive at the same conclusion?
3. **Attributable** — when the money is spent, can the effect be traced to a specific person and a specific moment?

That is the entire layer. There is no mechanism, schema, or measurement protocol attached — the criteria are applied inside the worked example as authoring discipline for the worker's output ("a concession is fine — but it buys something… every term has to be written into a clause someone can verify"). What the article claims as novel is the *framing itself*: trust as a machine-checkable property of an evidence chain, optimised deliberately, in the SEO-for-AI-recommenders sense. As agency doctrine that is a genuinely useful coinage. As agent architecture it is a checklist, not a component.

### 1.3 Laya — the judgment layer ("the brain that never writes")

Open-sourced 2026-09-18 by Convai Innovations; Apache 2.0, open weights, runs entirely on your own machine. The title's "brain that never writes" refers to *this* part: "it generates no text at all." You give it content plus questions defined in advance; one forward pass returns a probability per option. Three typed question shapes — **Choice** (pick one), **Score** (rate on a scale), **Noul** (probability of "yes") — the same three shapes as TypeSafe's Jev, whose question files, per a third-party skills repo, "work UNCHANGED" against Laya. Under the hood (from the model-card ecosystem, not the article): a 421M-parameter bidirectional encoder (ModernBERT-large) with a small decision head; trained with RLCD — reinforcement learning against strictly proper scoring rules, so reported probability is rewarded for matching reality rather than for being confidently right.

Speed as reported: M4 Pro multilingual build 11.2 ms/question GPU, 29.7 ms CPU; official T4 numbers 39.5 ms English, 32.8 ms multilingual — against a generative answer "starting in the hundreds of milliseconds — and then you still have to parse it." Language routing: non-Latin scripts auto-route to the multilingual build. The worked example: one client email, two questions in one pass — `Department: Billing p = 1.0`, `Cancel? p = 0.875`. "No sentence was generated. No format errors, no hallucinations, and the answer is guaranteed to be inside the options you supplied." The contrast drawn is with "ask an LLM for JSON and parse it — with the latter, you're forever handling parse failures."

**The traps section is the article's best writing, and it is honest.** Five, sourced to "Laya's own docs and third-party tests":

1. **>20 options and accuracy falls off** — all options share one fixed token budget; at 77 options each gets 3–4 tokens. Compress under 20, or use it as a coarse first pass.
2. **Score is the weakest type** — official five-level sentiment scoring 0.372; in Chinese tests scored items collapsed toward the midpoint. Fix: rewrite levels as Choice options, or split into several yes/no questions and combine.
3. **Without fine-tuning, basically unusable** — untuned English build 0.362 on the official dataset, *below* the 0.461 of always guessing the most common answer. "Do nothing, guess blindly, and you beat it." Step one is calibrating against your own historical tickets.
4. **Factory confidence runs hot** — fit temperature per question type; calibration error drops 0.466 → 0.081 after fitting. And thresholds don't catch everything: in Chinese tests the 5 wrong answers on "does this need human confirmation" averaged **0.89 confidence**.
5. **It cannot write** — by design; receipts, summaries and decks still go to a generative model. "It's a judgment layer, not an expression layer. Put it in the wrong slot and you've wasted it."

Plus the unwritten rule: "It reads literally. A cancellation email containing the words 'no rush' still got a 0.80 cancellation probability. Any action that spends money, sends something out, or deletes something — keep a human confirmation on it. Always."

Third-party texture the article doesn't carry: the English checkpoint collapses outside Latin scripts (0.000 accuracy on Khmer at 0.952 reported confidence in a 51-language sweep — the multilingual build exists because of this); the shipped `choice:11+` temperature (0.10) is outside its own valid range and gets clamped by the loader; independent testers put post-fit ECE around 0.08–0.10. None of this contradicts the article; all of it sharpens Trap 4.

### 1.4 The assembled run and the rollout order

The end-to-end example (a client asking "can we squeeze another 20% off this site?"): rules gate in microseconds → Laya classifies (scope change / price inquiry / grumble) in 33 ms → Router opens a ticket if confidence suffices, else logs and waits → Worker pulls quote history, cost structure, last concession → MTO criteria shape the answer (concession conditional on verifiable terms) → Worker reports "we can go X% lower, conditional on these three items, based on these numbers" → Router speaks one line back. "A human appears exactly once in the whole run — between Step 6 and Step 7. Nod, or edit."

The rollout order is the article's closing argument, and it is good: **(1) Tickets first** — turn verbal work into trackable tickets (what's wanted, what counts as done, who raised it, who has veto); **(2) then the gate** — which classes finish alone, which need one human click, "written as rules, not as a model judgment — because a model judgment gets flattened by the four words 'the client said so'"; **(3) then calibrate judgment** on six months of labelled tickets; **(4) only now wire Router and Worker**. "Reverse the order and the outcome is guaranteed: the Agent runs at full speed, and a human follows behind cleaning up."

**What the article does not specify** (absence noted, not fault imputed): persistence/memory beyond the Router's in-session global context (DeepSeek lists long-term memory among the prototype's open areas); any verification of a Worker's report against a store the Worker cannot write — the human nod between Steps 6–7 is the only check, and it is a *judgement* check on a summary, not an *effect* check on the work; failure attribution when a run goes wrong; and what the criteria layer does when its three metrics conflict.

---

## 2. Our stack, in the same terms

Four load-bearing pieces, each citable to the shelf:

**(a) Jacquard's constitutional line** (`~/workspace/cybernetic-architecture/`, v1.3.0 tagged @a178d22, 2026-11-03). Decision models sit behind a provider interface; Jev readings are recorded *uncollapsed* as advisor testimony; "the judge does not gate; **the record gates**" (doc 03). Senses are read-only: "senses cannot write, route, or gate" (doc 07). Classes gate by stakes, scores rank — a match score never appears in a gate decision. This is a *write-authority* invariant enforced by a kernel over a hash-chained log: models propose, the record disposes.

**(b) The frame-to-weights / scratch-pad doctrine** (DESIGN-FRAME-TO-WEIGHTS, published 2026-11-07 on SI-Thor/rolling-perception). The external frame is the slow, deliberative, receipted writer; behaviours *graduate* into compiled reflexes only through a pipeline (accumulation → candidacy with state ablation + prober ceiling → corpus with failures at natural rate → sealed graduation exam with a shifted slice → adoption at Casey's gate), and behaviours that read live world state at decision time **never graduate** — they stay on the scratch paper permanently, correctly. "Compile the triage; keep the verdicts expensive, slow, and outside."

**(c) Today's production shape** (Syndicate study Addendum 3, 2026-11-08, and running since): Muse charters and verifies → a Claude Code manager seat orchestrates → ZCode/MCode seats execute in parallel → receipts flow back up and are **verified against world evidence** — stores the workers cannot write (the server log, the census, the ledger). Seats are verified by output + tail, never by launch echo; briefs travel by scp with byte counts checked and the full brief text embedded in the launch prompt; the manager never grades its own lanes.

**(d) The verification doctrines** (Verification Doctrine v1; the Watcher's Charter; the survey adoptions). Class A existence checks are unconditional and deterministic — verify the effect in a store the actor cannot write; a self-report is an echo, never a landing. Class B content checks are priced (verify iff P(wrong) × R × C_error > C_verify). A verify pass requires a *named new evidence source*; verification never substitutes for authorisation. Every failure carries a `fault_owner` (agent / harness / prompt / budget / luck / world). Claimed-but-not-done is the fleet's standing failure class — it fired again tonight (a completed fix whose report was lost was caught by artefact re-derivation, not by trusting either story).

---

## 3. The comparison

| Dimension | MTO Agent (article) | Our stack | Call |
|---|---|---|---|
| The "never writes" invariant | The *judge* generates no text — output is a probability over supplied options; no parse failures, nothing outside the option set | No *model* writes or gates the authoritative record — the kernel/record writes; models are senses/advisors behind a provider seam | **Same slogan, different invariant.** Theirs is about output modality; ours is about write authority. Theirs prevents malformed answers; ours prevents unverified state |
| Who orchestrates | Router (lightweight model, no tools, holds global context) | Muse charters → Claude Code manager seat (no grading of its own lanes) | Convergent shape; ours adds a verification rung above the orchestrator and a prohibition the Router lacks |
| Who executes | Worker per ticket, isolated context, strongest model, reports up, never speaks out | Seat per commission, isolated brief, reports up as receipts | Convergent — independently arrived, theirs published Oct 31, ours running from the seat-fleet discipline of October |
| Who checks the work | A human nod on the Worker's *summary* (Step 6→7), once | World-evidence verification in stores the worker cannot write; placebo arms; landing verification; fault-owner on every failure | **Ours is a layer they don't have.** Their check is a judgement on a story; ours is a read of an effect |
| The gate | Rules by class, written by humans before wiring ("the gate as rules, not model judgment"); human confirmation on spend/send/delete | Effect classes gate by stakes in policy (Jacquard R5); adoption of compiled behaviour is Casey's gate; verification never substitutes for authorisation | Convergent, strikingly — their Step-2 rationale is our Gate B in an account director's words |
| Fast judgment | Laya: typed Choice/Score/Noul, one forward pass, ~33 ms, local, open weights; calibration is the operator's job | Jev (closed, API) as advisor behind the seam; local `jev-semantic` ONNX judge on the Thor rack; d3-ultra as named challenger; patterns library prices all three | **Their artefact is new to us** — see §4. Our *doctrine* for the slot (advisor-never-gate, published limits as routing rules) predates our knowledge of Laya |
| Criteria for trust | Verifiable / Reproducible / Attributable — three metrics for outward claims | Evidence grades A–D on every study; provenance on every triple; receiver-confirmation as admissibility; sealed held-out sets | Convergent instinct; ours is mechanised, theirs is a mnemonic. Their three words are the better *portable* form |
| Memory / persistence | Router's session context; workers' traces; long-term memory an admitted open area of the prototype | Engine state / ledger / triples library with provenance + reconciliation; the record is the memory | Ours is built; theirs is a named gap (theirs honestly) |
| Numbers | Super-agent: synthetic traffic, simulated tools, no quality measure, token price unstated. Laya: vendor + third-party, failure modes published | Fleet numbers carry method + store; striking figures are treated as claims until independently reproduced (three dissolved this week alone) | Their Laya honesty is the exception in their own article — the Super-agent numbers are repeated at headline strength |
| Rollout order | Tickets → gate → calibrate → wire | Charter → claim → seats → receipts (WP-0 first completable package retires the silent-default class before any body depends on it) | Convergent; the same "definitions before machinery" instinct |
| Failure thinking | Five traps, all about the *judge's* calibration | Failure classes about the *system's* claims: hold-loss, placebo-matched primaries, silent defaults, confounded apparatus | Complementary blind spots — theirs would not catch a hold-loss; ours had not priced option-count collapse |

## 4. The verdict

**What they do that we don't — precisely one artefact and two habits.**

1. **Laya itself.** An open-weights (Apache 2.0), locally runnable, Jev-shaped decision model: 421M parameters, ~33 ms on a T4, zero per-call cost, question files interchangeable with Jev's. Our slot for this class is filled by a closed API (Jev, advisor-only) and a small local namesake ONNX judge. An open local entrant changes the economics of the reflex tier — Tier R/D nods in the town charter are currently budgeted as governor-metered calls; a Laya-class model on the Thor rack would make the nod effectively free at exactly the cadence classes our patterns doc prices. This is a candidate, not a conclusion: Laya arrives with Trap 3 attached (untuned ≈ below the majority baseline), and our standing rule is that a decision model is adopted behind the seam only on sealed evidence, never on a vendor chart — including this article's.
2. **Subscription pass-through as a named, priced pattern.** Route follow-ups on a claimed thread directly to the owning worker *by code*, bypassing the router — ~30% fewer router decisions claimed. Our manager seat re-briefs per commission; a persistent manager (the TOWN-0 seat is one) pays that tax repeatedly. We had priced dsh's decoupling win in tokens (Batch 1: the 37% cache-read figure, inverted) but had not named the routing rule as a seat-fleet pattern.
3. **Calibration traps published as operating instructions.** The five traps are written for the *operator*, with numbers (0.362 vs 0.461; ECE 0.466 → 0.081; wrong answers at 0.89 confidence). Our patterns doc carries published-limit routing for Jev; it has no equivalent operator-facing trap list for decision models generally. Their Trap 2 corollary — *rewrite Score questions as Choice/Noul decompositions* — is a concrete design rule we had not filed.

**What's convergent — and what convergence is worth.** Router/Worker ≈ charterer/manager/seats; rules-before-model filtering ≈ our deterministic Class A gates in front of any model reading; the gate-as-rules Step 2 ≈ Gate B; tickets-first ≈ charter-first; "the bottleneck is how many sessions a person can watch" ≈ the table rule (attention is the scarce resource; bits-through-Casey minimised). None of this is copying in either direction: the components are all public and dated (Laya 2026-09-18, dsh 2026-10-31), our corresponding record is public and dated (Jacquard rulings 2026-11-02, v1.3.0 tagged 2026-11-03, frame-to-weights published 2026-11-07, the production shape running and documented 2026-11-08 — the same day this article appeared, in an unrelated industry, on another continent's platform). Independent arrival at the boss/crew/criteria/nod shape by an advertising practitioner assembling other people's parts is *evidence the shape is load-bearing*, not evidence either side borrowed. Timestamping cuts our way on the assembly and the doctrine; it cuts theirs on the two named components. Both directions are stated because both are true.

**Where they're behind our practice** (evidence-bounded): the assembled system has no verification layer in our sense — a human nods at a summary, and nothing reads the effect in a store the worker cannot write; the Super-agent numbers are carried without their synthetic-traffic caveat or their ~3.8× token price; MTO, the title component, is a checklist with no mechanism, where our criteria are mechanised (grades, provenance, receiver confirmation, sealed sets). And the article's own unwritten rule — human confirmation on anything that spends, sends, or deletes — is doing the work their architecture doesn't: it is a *policy* taped over the exact hole (unverified worker effects) that a record-gate fills by construction.

**Answer to Casey's question, in one line:** they are not doing anything exceptional — they are doing *our* shape, competently, for agencies, with one component (Laya) we should trial behind the seam and two habits (subscription routing, the trap list) we should file.

## 5. Steals, with the smallest experiments

1. **STEAL: Laya as a provider-seam candidate.** *Experiment:* on the Thor, `pip install laya` beside the JEV rack; run the fleet's existing triage question sets (game-master fault-owner classification is the natural first set — six options, world-evidence ground truth already filed) three ways: untuned, temperature-fitted, fine-tuned-on-our-labels if the first two justify it. Measure accuracy + ECE against `jev-semantic` on the same set, sealed split. Kill criterion pre-registered: if fitted Laya does not beat the local judge on accuracy at ≤ its latency, it stays a citation, not a component. Cost: one seat-session plus rack time; no doctrine changes on a pass — a pass earns a *sealed A/B against Jev/d3-ultra* (ACTIONS item 13's set), nothing more.
2. **STEAL: the trap list as a decision-model intake checklist.** *Experiment:* none needed — a filing action. Add Traps 1–5 (option-count collapse, Score weakness + the Choice/Noul decomposition rule, untuned-below-baseline, hot factory confidence, literal reading) to the patterns doc as the standard intake questions for any decision model, beside the four asterisks we already apply to "open" releases. Any future model that cannot answer Trap 3 with its own untuned number is graded D until it can.
3. **STEAL: subscription pass-through for the persistent manager seat.** *Experiment:* in the TOWN-0 manager's next commission cycle, let follow-up traffic on a claimed work package route to the owning seat by the package ID in the brief header (code-level routing in the manager's dispatch script, not a model decision); count manager re-briefs before/after over one cycle. Adopt if re-briefs fall without a single misroute; the misroute count is the kill metric, not the saving.
4. **TAKE THE WORDS, NOT THE LAYER: MTO's three metrics as the outward-claims mnemonic.** Verifiable / Reproducible / Attributable is a better pocket form of our evidence grading for anything the fleet publishes outward (the outward pieces already run a cold test; this gives the test a three-word checklist a non-fleet reader can apply). *Experiment:* apply it as the pre-publish checklist on the next outward piece and see whether it catches anything the cold test didn't. No adoption into doctrine on one pass.

## 6. Process

Sources, in order of weight: the article's full text (browser fetch, 2026-11-09 ~02:55 UTC, lines 0–363 — title, all eight parts, closing); the fleet's Batch 1 deep-learn §13 (repo-first read of dsh-superagent, October) refreshed against November third-party coverage (dev.to, codesprintconsulting, Elets CIO — all consistent with the repo read, including the synthetic-benchmark caveat the article omits); Laya's surrounding record (eesel explainer, laya.studio, the DrOlu use-laya skill noting Jev question-file compatibility, the cryptonwz calibration tutorial, aichina news) for mechanism and third-party numbers the article doesn't carry. Our side read first-hand from the shelf: the Jacquard programme docs (03/07 especially), the decision-models room and patterns doc, Verification Doctrine v1's INDEX record, the Syndicate study's Addendum 3, and MEMORY.md's standing rulings. No claim about the article rests on anything but its fetched text; no claim about the components rests on the article alone. Placement: the decision-models-and-verification room — this is a decision-model and verification-doctrine comparison; its organisation-layer half cross-references Batch 1 in the fleet-and-substrate room.
