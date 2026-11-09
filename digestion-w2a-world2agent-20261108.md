# Digestion — World2Agent (W2A): a signal protocol for giving agents eyes, read at spec level against our Watcher's Charter

*2026-11-08. Digestion doc under Casey's standing instruction of the same day. Sources: the launch thread (Typefully, Charly Wargnier/@DataChaz, 8 Nov 2026) and — per the brief — a spec-level read of the GitHub repo (github.com/machinepulse-ai/world2agent): README, `docs/signal-format.md`, `docs/architecture.md`, `docs/multi-sensor.md`, the `schema/0.1/` layout, and the official HackerNews sensor's SETUP.md in the sibling sensors repo. Where a claim comes from a third-party due-diligence summary rather than the repo itself, it is flagged.*

> **Name-collision caution:** an unrelated "w2a" on PyPI is the Web2Agent Protocol (agents.json). Not this project. Anyone searching later should not conflate them.

## The pitch and the shape

"If MCP gave AI agents hands to work, World2Agent gives them eyes to see." The motivating failure: agents have advanced logic but are "completely disconnected from live context" — when a system crashes, the agent "just sits there idly until you tell it what to do." The protocol shape is **World event → Sensor → Signal → Agent → Action**.

Sensors are npm packages speaking one unified schema; the protocol is open and framework-agnostic (Claude, Codex, OpenClaw, Hermes named). Four launch use cases: a **Deal Sensor** (a limited-time free game appears → signal → agent auto-claims it), an **X Sensor** (a senior engineer posts an optimisation → agent audits your codebase), a **Bug Sensor** (production crash → packaged error signal → Claude Code drafts the PR fix), and a **GitHub Trending Sensor** (a repo gains traction → summary into the team's Notion).

## Repo facts (as crawled 2026-11-08)

`machinepulse-ai/world2agent`, public, **Apache-2.0**, created 2026-04-23, 20 commits, 1,123 stars, 41 forks, 14 watchers, **0 releases, 0 tags**. Root: `docs/`, `schema/0.1/` (a *versioned* schema directory — consumers are told to pin to the directory, never to `main`), `scripts/`, `skills/build-w2a-sensor/`. SensorHub (world2agent.ai) is the catalog; sensors are discoverable via `npm search w2a-sensor`. Runtime plugins exist for Claude Code (`/plugin marketplace add …`, sensor-add commands, restart with the plugin channel loaded), Hermes (`@world2agent/hermes-sensor-bridge` — each signal triggers a fresh `AIAgent.run_conversation()` against a generated handler skill), and OpenClaw (`@world2agent/openclaw-sensor-bridge` — writes a managed hooks block into `~/.openclaw/openclaw.json`, auto-generates a hooks token, keeps a timestamped config backup; each signal triggers a fresh `/hooks/agent` call). A build-a-sensor skill scaffolds a new sensor in ~50 lines; publish to npm and it is installable. A graph layer to compose/enrich signals from multiple sensors is **roadmap (RFC only)**. Deployment partner: Zeabur. MachinePulse is a Singapore Pte. Ltd.; sibling repos include world2agent-sensors, a TypeScript SDK, and a notify hub with post-publish auto-registration on SensorHub; other products: Karpo, Shotwright.

The README's own security note deserves quoting in substance: *a sensor's signals drive what your agent perceives and does, so an untrusted sensor is effectively an untrusted instruction source — stick to open-source sensors from authors you trust, and review the code first.* Correct, and (see below) it is also the protocol's entire provenance story.

## The signal, precisely (from `docs/signal-format.md`)

Every sensor emits the same envelope; the canonical schema is `schema/0.1/schema.ts` with a generated `schema.json`. Fields:

- `signal_id` — UUID v4, **fresh per emission, even for logically identical events**; the doc says "consumers dedupe on this."
- `schema_version` — `"w2a/0.1"`; consumers **MUST reject** versions they don't understand.
- `emitted_at` (UTC ms) — distinct from `event.occurred_at`.
- `source` — `sensor_id` (the npm coordinate), `sensor_version`, `source_type` (a coarse platform grouping — `github`, `cron`, `feishu` — an open set with no central registry), `user_identity` (self-asserted, e.g. "octocat"), `package`.
- `event` — `type` in `domain.entity.action` form with a **past-tense verb** (`repo.pull_request.opened`, `messaging.message.mentioned`, `market.quote.threshold_crossed`); `occurred_at`; and `summary` — "the soul of the signal," written to the pattern **Actor → Action → Object → Context → Impact**, on the stated principle that *if the summary alone is not enough to decide whether and how to act, the signal has failed*.
- `source_event` — the source-native payload as a self-describing `{schema, data}` pair (JSON Schema draft-07; every property SHOULD carry a `description`, because the description is what lets an agent reason without sensor-specific knowledge).
- `attachments` — a tagged union (inline or reference, `description` required on both; prefer reference beyond a few KiB).

Design notes stated in the doc: **no routing in protocol** (routing and priority are consumer-side; a sensor just emits); extensibility via `_meta` (consumers MUST ignore unknown keys). Architecture doc adds the neutrality constraints: **sensors don't make value judgments**, don't assume where they run, don't define actions; transports are stdout piping, HTTP POST, WebSocket/SSE, or consumer-defined custom transports. Multi-sensor composition is fan-out via an SDK (`runAll` + `fanout` over transports) or plain shell pipes (`w2a-sensor-github | your-consumer-app`).

Signal anatomy in practice (official HN sensor's SETUP.md): a signal carries `event.summary` pre-tagged (e.g. [HOT] / [POPULAR] / [ACTIVE DISCUSSION]) plus `source_event.data` with the native payload ({id, title, url, hn_url, score, comments, author, rank}). Sensor config lives in `~/.world2agent/config.json` (HN defaults: top_n 10, min_score 20 pre-filter, **interval_seconds 300 polling**). *"Semantic filtering is the handler skill's job"* — sensors pre-filter cheaply and stay dumb; a generated handler skill (natural-language instructions with thresholds) does triage and presentation.

## The charter comparison — the reason this doc exists

Our Watcher's Charter (2026-11-07 study + first-pass implementation) was written against a specific, lived failure: a daylight hold that *sent* refreshes every five minutes while none *landed* for ~90 minutes, and citizens died in a world everyone believed was held. The charter's core rules: **(1) verify the effect in a store the watcher cannot write; (2) silence is a failure state; (8) who watches the guard** — with effects-based heartbeats (7 watchers reporting into a commons the watcher doesn't own; meta-watcher on timers on two boxes; the one open gap being an external expecter). Read against that standard, W2A as specified (schema 0.1, docs as crawled) has three precise gaps:

**Provenance — install-time trust only.** The envelope's `source` block is entirely *self-asserted*: a sensor claims its npm coordinate, its version, and a `user_identity`, and nothing in the signal format as read provides a signature or attestation binding a signal to the package that supposedly emitted it. The README's mitigation is social, not cryptographic: only install sensors from authors you trust, review the code. That answers "should this sensor be on my machine?" It does not answer "did *this signal* come from that sensor, unmodified?" — and for the Bug Sensor use case (a crash signal that triggers a PR-drafting agent run), the difference is the whole game. By charter lights: a signal is a claim; W2A gives claims no receipts.

**Dedupe — transport-level only, and the spec's own sentence overpromises.** The signal-format doc says consumers "dedupe on" `signal_id`. But `signal_id` is *fresh per emission even for logically identical events* — so the only duplicates a consumer can actually suppress are re-deliveries of the *same emission* (same UUID arriving twice over a transport). Sensors poll (the HN sensor every 300 s): if the same world event is still over threshold at the next poll and the sensor re-emits, it arrives under a **new** `signal_id` and is indistinguishable from a new event. There is no event-identity field (no source-native ID promoted into the envelope's dedupe surface — the HN `id` sits inside `source_event.data`, unindexed by the protocol), no windowing or suppression semantics, and no acknowledgement: signals are fire-and-forget triggers that spawn fresh agent runs. Dedupe of *meaning* is left, silently, to every handler author. (An earlier chat summary said W2A has "no deduplication semantics"; the spec read corrects that to the sharper statement above — dedupe exists, but only where it matters least.)

**Heartbeat — absent, and absence is the dangerous part.** Nothing in the signal format, architecture, or multi-sensor docs as read defines liveness: no heartbeat signal type, no expected-cadence declaration, no dead-sensor detection. A sensor that crashes, loses its credentials, or wedges is **indistinguishable from a quiet world** — the agent simply hears nothing, forever, and "nothing happened" is the one conclusion it cannot distinguish from "the sensor died." This is, almost word for word, the failure mode the charter was written against: our hold *process* was alive and sending; the *effect* had stopped; silence was read as safety. W2A's design centre is the eventful world (deals, crashes, trends) where silence usually does mean quiet — but its own Bug Sensor use case inverts that: the sensor you most need is the one whose silence you most cannot afford to trust. A `sensor.heartbeat` convention (or an expected-cadence field in sensor metadata, with consumer-side staleness alarms) would close most of this gap cheaply; its absence in 0.1 is the finding.

**What W2A gets right by charter lights:** neutral sensors ≈ a clean separation of sensing from judgement (the charter's watchers likewise report effects, not verdicts); one schema with a MUST-reject versioning rule (fail loud, never degrade silently); self-describing payloads whose descriptions do the semantic work; and the handler-as-skill pattern (declarative, inspectable handling logic rather than code paths). The protocol is a good *envelope*. It is not yet a *watching* system: it can tell an agent that something happened, but it cannot yet assure the agent that it would know if something stopped happening — and it cannot prove who told it.

## Fleet mapping

- **Rolling perception / telltape:** W2A is the event-driven cousin of our stream: discrete signals vs continuous rolling perception. The summary discipline (Actor → Action → Object → Context → Impact; "if the summary alone can't support a decision, the signal has failed") is a genuinely good standard for any event surface we expose — worth adopting as a style rule for watcher alerts into the commons.
- **Watcher's Charter line:** this doc is the mapping. W2A is now the named external example of "perception without liveness semantics" — useful when explaining why the charter exists.
- **Jacquard / governor:** a sensor ecosystem behind a provider-shaped interface is conceivable, but nothing in 0.1 meets our provenance bar for anything that can trigger action; observation-only use (a trending sensor feeding a human-read digest) is the ceiling today.
- **League / foundry / radio-room / weight-space:** no honest mapping.

## Grade

**B− as an artefact** (real repo, Apache-2.0, working plugins, honest README security note; but 0 releases, 20 commits, and the semantics above are 0.1-thin) — and **instructive** beyond its grade: it is the cleanest available specimen of the gap between *giving agents eyes* and *knowing the eyes are open*.

---

*Digested 2026-11-08 from the launch thread and the repo's own docs/schema as crawled that day. Charter comparison is this doc's analysis. No fleet system was touched; nothing was installed.*
