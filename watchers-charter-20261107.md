# Night Study 4 — Successful Always-On Systems: What Keeps Long-Running Agents Honest

_Written 2026-11-07 (AKST), after the night the league's watchers lied quietly. Companion to OPERATIONS.md and the hold-loss incident record._

## Why this study exists

Tonight the league had no dramatic failures. It had two quiet ones:

1. **The cameraman** kept typing daylight commands into a client that wasn't receiving them, and kept writing "sent" in its log. Every surface said the hold was fine; the server log — read hours later — showed nothing had landed since 05:58Z, and the world ran real nights while a citizen died in a loop.
2. **The curator** crashed on a sort over a null value and stalled curation for hours. Nothing alerted, because nothing was watching for its *output*; its process state was the only health signal anyone had, and a crashed watcher produces no error rate at all — zero runs produce zero errors.

Neither failure is exotic. Both are the standard way always-on systems fail in production everywhere: **not by breaking loudly, but by continuing to report health from inside the failure.** This study looks at systems and standards that run unattended *successfully*, at the documented incidents where the dashboard was green and the system was down, and distils the result into a charter the league's background processes can be held to — as checkable properties, not aspirations.

The one-sentence version of everything below: **a watcher earns trust only by proving, in a store it does not control, that the effect it exists to cause is still happening — and by treating its own silence as a failure.**

---

## Part 1 — Incidents: when the surface said fine

### 1.1 GitLab, 31 January 2017 — five safety nets, none of them real ⭐

An exhausted engineer, fighting a stalled database replica late at night, ran a cleanup command on the wrong host and deleted ~300 GB of the production database. Accidents happen; that's what backups are for. When the team went to restore, they found — in their own livestreamed incident notes — that **"out of five backup/replication techniques deployed none are working reliably or set up in the first place."**

The primary one is the instructive one. The nightly `pg_dump` job had been failing for months: a PostgreSQL upgrade left it invoking a `pg_dump` 9.2 binary against a 9.6 server, which refuses and exits — so the S3 bucket held empty/zero-byte output. The job *did* have failure notifications — sent by email, and the emails were being rejected because of a DMARC configuration elsewhere, so the alarm fired every night into a path that dropped it on the floor. Nothing anywhere checked that a backup artefact of plausible size had actually *arrived*, or that the alarm channel itself still delivered. Azure disk snapshots turned out never to have been enabled for the database servers at all. The only usable copy was a manual LVM snapshot an engineer had happened to take ~6 hours earlier to refresh staging. Six hours of production data — ~5,000 projects, 5,000 comments, 700 accounts — was permanently lost; the site was down ~18 hours.

What changed after: GitLab's postmortem made backup health itself a monitored, visible thing (they stood up public backup monitoring), committed to testing that backups could actually be restored rather than trusting backup *logs*, and published the whole episode — chats, livestream, postmortem — which is why it's still the industry's teaching case. The lesson isn't "test your backups" as a slogan; it's the mechanism: **the backup job's own report of success was the only evidence anyone consulted, and the job and its alarm channel shared fate with each other.** Existence, size and restorability of the artefact — in the bucket, readable by someone else — was never verified by an independent reader.

_Sources: GitLab's postmortem as retold with postmortem quotations at https://angri-tech.org/en/blog/gitlab-com-database-outage-2017-five-backup-layers-none-working-reliably and https://uptimepage.dev/blog/cron-jobs-fail-silently (the latter quotes the postmortem on the DMARC-rejected failure notifications and the empty bucket); narrative reconstruction at https://www.vivianvoss.net/blog/the-backup-that-wasnt_

### 1.2 AWS S3, 28 February 2017 — the dashboard that couldn't turn red

A typo in a playbook command removed far more S3 index/placement capacity than intended in US-EAST-1; S3 needed a full subsystem restart and was down for ~4 hours, taking a visible slice of the internet with it. The famous detail: **for the first two hours, Amazon could not update its own Service Health Dashboard.** The dashboard's administration depended on S3 in the affected region, and the status icons on the public page were image files stored on S3 — so the page kept displaying green "operating normally" icons for services that could not serve a single request. AWS communicated via Twitter until it regained the ability to update the dashboard at 11:37 PST.

What changed after: the Service Health Dashboard was rebuilt to run across multiple AWS regions, so that no single region's outage can take down the page that reports outages; the capacity-removal tooling was also changed to remove capacity more slowly and to refuse to drop a subsystem below a safe floor. The generalisable lesson is about **shared fate between the watched system and the reporting surface**: the dashboard wasn't lying maliciously — it was *frozen*, because the mechanism for changing it lived inside the failure it was meant to report. Any status that can only be updated through the system it describes will, on the worst day, display whatever it last believed.

_Sources: The Register's contemporaneous report, https://www.theregister.com/off-prem/2017/03/01/awss-s3-outage-was-so-bad-amazon-couldnt-get-into-its-own-dashboard-to-warn-the-world/337924 ; long-form reconstruction citing AWS's official summary, https://dev.to/vivian-voss/the-command-that-removed-too-much-115f ; status-page analysis at https://completestatus.com/blog/s3-outage-status-page-lessons_

### 1.3 Facebook, 4 October 2021 — the safeguard had a bug, and the lifeboats were on the ship

During routine maintenance, a command intended to *assess* global backbone capacity instead took down all backbone connections, disconnecting Facebook's data centres globally. Facebook's systems were designed to audit commands like this before execution — **but a bug in the audit tool prevented it from properly stopping the command** (Santosh Janardhan's postmortem says this in so many words). The DNS servers then did exactly what they were designed to do — withdrew their BGP advertisements when they couldn't reach the data centres — making themselves unreachable even though they were still operational. Recovery was slowed by the second-order effect: the internal tools engineers normally use to diagnose and fix outages depended on the same network and DNS that were down, and the data centres are hardened to be difficult to enter and modify even with physical access. Engineers had to go on-site. Total: ~6–7 hours for Facebook, Instagram, WhatsApp and Oculus.

Two lessons for watchers specifically. First, **a guard is itself a component**: the audit tool was the check standing between a bad command and the world, it had an untested bug, and nothing verified the guard. (Tonight's league version: a focus guard that truthfully verified the *window* had focus while a modal inside the window ate the keys — a guard checking a true fact that was not the load-bearing fact.) Second, **recovery tooling must not share fate with the failure**: Facebook's diagnostic and access tooling rode the network it existed to repair, which converted a configuration error into a physical expedition.

_Sources: Facebook engineering postmortem (Janardhan, 2021-10-05) as reported at https://www.networkworld.com/article/970304/facebook-outage-was-a-series-of-unfortunate-events.html and https://datacentercatalog.com/news/2021/facebook-we-disconnected-our-data-centers-from-the-internet_

### The common anatomy

All three incidents, and both of tonight's league failures, share one skeleton:

| Step | GitLab | AWS | Facebook | League cameraman | League curator |
|---|---|---|---|---|---|
| Component fails | backup job errors nightly | S3 index/placement down | backbone command executes | keystrokes land in a modal | sort crashes the pulse |
| Its own report says | nothing (emails rejected) | icons: green | DNS "healthy" logic fires as designed | log: "sent" | nothing — process gone |
| The check that would have caught it | read the bucket; test a restore | update the dashboard from outside the region | test the audit tool; reach tools out-of-band | read the server log for the landing line | alarm on missing output, not on errors |
| Why it wasn't there | success was self-reported | reporting lived inside the failure | guard untested; tools shared fate | send treated as effect | silence isn't an event |

**Monitoring that reads the component's own outputs can only ever confirm the component's opinion of itself.**

---

## Part 2 — Patterns that keep always-on systems truthful

### 2.1 Invert the signal: the dead man's switch

Ordinary monitoring asks "did anything report an error?" A dead job reports nothing, so the answer is vacuously "no" forever. The dead man's switch inverts the burden of proof: the job must actively check in — a heartbeat ping on success, at a declared period with a declared grace window — and **the absence of the ping is the alarm**. This is the operating model of Healthchecks.io and Cronitor-style cron monitoring: register the expected interval; if `last ping + period + grace` passes with nothing, the check goes down and notifies. Its decisive property, as the practitioners put it, is that it catches failures no in-process error handler can catch — the job that crashed before its error handling loaded, the cron entry that was deleted, the host that vanished. It also has a stated limit worth keeping: a heartbeat proves the job *ran and reached the ping*, not that its work was good — a job can ping while writing an empty file. Heartbeats are therefore the floor of liveness, always paired with §2.3's effect checks, never a substitute.

League translation: every periodic process (curator pulse, digest, capture rotation, consult drivers, cameraman refresh) already has a natural period. Each needs a heartbeat *with content* (see Rule 2) landing in a store outside itself, and an independent reader that alarms on staleness.

_Sources: https://www.pagerly.io/blog/cron-job-monitoring-silent-failures-2026-09-15 (the "absence of a signal is not a signal" framing; the exit-zero lie); https://dev.to/serverkueche/healthchecks-monitor-cron-jobs-backups-dead-mans-switch-2oo1 (period + grace mechanics); https://pulse.pulsecima.com:443/cron-monitoring.html_

### 2.2 Watchdogs with a separate time base (IEC 61508)

Embedded safety engineering solved "the processor says it's fine" decades ago: don't ask the processor. IEC 61508-2 recommends, as a diagnostic measure for processing units, a **watchdog with a separate time base** — an independent hardware timer the MCU must service with the correct pattern inside a window; too late *or too early* both count as failure, and on expiry the watchdog forces the system into a **safe state** (reset/safe shutdown) without the failed component's cooperation. The standard's reasoning is exactly the league's problem: an internal watchdog is part of the thing that may be defective, so common-cause failure takes both down together; the external watchdog survives because it shares no clock, no code and no fate with the supervised unit. Windowed and challenge-response variants go further — the supervised unit must not merely twitch, but answer correctly, proving it executed the right sequence, not just *a* sequence.

League translation: the supervisor of a league process must not be a thread inside that process, a timer on the same host's goodwill, or a check written in the same code path. "Separate time base" for us means: independent process, independent host where it matters (Orin vs Thor is a real boundary tonight), and a safe state it can impose (self-park, STOP file) rather than merely report.

_Sources: EDN/Analog Devices treatment of program-sequence monitoring under IEC 61508-2 (watchdog with separate time base; internal WDT common-cause caveat), https://www.edn.com/wp-json/wp/v2/posts/5973846 ; arc42 quality model, "Watchdog Supervision" (independence as the key property; missed heartbeat → restart, failover, or safe state), https://quality.arc42.org/approaches/watchdog-supervision_

### 2.3 Verify the effect, not the send — the end-to-end argument for actuators

Saltzer, Reed & Clark's end-to-end argument (1981/84) is usually quoted for networks, but its file-transfer example is an actuator parable: no amount of care inside the channel can substitute for the endpoint checking that the file *arrived intact*, because only the endpoint knows what "correct" means and only the final state is the truth. Applied to anything that acts on the world: **a command is a hypothesis; the world's subsequent state is the result.** Three mature disciplines implement this as non-negotiable protocol:

- **Spacecraft operations (ECSS PUS, Service 1 — telecommand verification).** ESA's Packet Utilisation Standard (ECSS-E-ST-70-41) defines a dedicated verification service: for each telecommand, the spacecraft returns staged telemetry reports — acceptance success/failure (TM[1,1]/[1,2]), execution started (1,3), progress (1,5), execution completed (1,7) or failed (1,8). Ground never treats "we transmitted it" as "it happened": acceptance is distinguished from execution, execution from completion, and each stage is confirmed by the spacecraft's own telemetry — a *different channel* from the command uplink. Flight recordings (e.g., Hera, JUICE) show the 1,1 → 1,7 pairing on real traffic.
- **Substation automation (IEC 61850, select-before-operate).** A breaker operation is two messages: select the device (it reserves and reports back), then execute — and after execution, **confirmation that the switch reached its new position is returned to the operator**; the HMI symbol flashes *until the new position is confirmed*, and a failed operation returns an indication with the reason. "Command sent" is not a state the operator is ever shown as success.
- **Reconciliation loops (Kubernetes controllers).** The controller pattern never trusts that its action worked: it runs observe → compare desired vs actual → act → repeat, level-triggered rather than edge-triggered, with idempotent actions. If it crashes and misses a hundred events, the next pass re-reads reality and closes the gap; "events are hints, not commands." A one-shot actuator that fires and forgets is the anti-pattern this replaced.

The discriminating question in all three: **is your confirmation an echo or a measurement?** An echo is the channel repeating your command back (an API's 200, a client's "sent", a bot's self-report). A measurement is independent evidence that the world changed — the server log's landing line, the artefact in the bucket, the switch's position contact, the spacecraft's telemetry. Tonight's cameraman had echoes. The guard built tonight — drain the server log to a byte offset, send, then require the landing line in that independent log within seconds — is a textbook PUS-style staged confirmation, arrived at the hard way.

_Sources: Saltzer, Reed & Clark, "End-to-End Arguments in System Design" (1981/84), summarised at https://devopedia.org/end-to-end-principle ; ECSS PUS Service 1 report types as catalogued in the SPIRE Data ICD, http://archives.esac.esa.int/hsa/legacy/ADP/SPIRE/SPIRE_docs/SPIRE_Internal_Documents/001078_DOC_DataICD_KJK/PRJ001078_SPIRE_Data_ICD__Issue2.pdf , and observed on Hera telemetry at https://destevez.net/2024/11/hera-telemetry/ ; IEC 61850 select-before-operate with execution confirmation, https://patents.google.com/patent/EP2293159A1/en ; Kubernetes reconciliation (level-triggered, idempotent), https://notes.kodekloud.com/docs/Prep-Course-Certified-Cloud-Native-Platform-Engineering-CNPE/Platform-APIs-and-Self-Service-Capabilities/Operators-Controllers-Reconcile-Like-a-Pro/page_

### 2.4 Black-box probes beat component health (Google SRE)

Google's SRE book (Ch. 6, "Monitoring Distributed Systems") draws the line the league crossed tonight: **white-box monitoring** reads a system's internals — its logs, its self-reported metrics; **black-box monitoring** tests externally visible behaviour "as a user would see it" and is symptom-oriented: it represents problems that are active *right now*, not predicted. Google's practice is heavy white-box *plus* "modest but critical" black-box — because a component's internals can be immaculate while the service it exists to provide is dead (the cameraman's log was a perfect white-box record of a dead service: daylight). The corollary for health endpoints: a `/health` that returns 200 because the process is up is a white-box vanity metric; the check that pages must be the one that performs the service's actual transaction from outside — a synthetic probe. For the league: the cameraman's health is not "process alive + log lines flowing" but "a probe reads the server-side world time and finds it inside the held band"; the curator's health is not "no exceptions lately" but "a reel/manifest younger than X exists and a probe can name its newest moment."

_Source: Google, Site Reliability Engineering, Ch. 6 — https://sre.google/sre-book/monitoring-distributed-systems/_

### 2.5 Test the alarm path itself — the always-firing watchdog alert

The Prometheus ecosystem's answer to "who watches the watchers" is disarmingly literal: configure an alert that **always fires** (`vector(1)`), route it through the entire alerting pipeline to an external service that *expects* to receive it every few minutes — and have the external service raise the alarm when the ever-firing alert *stops arriving*. If anything in the chain breaks (rule evaluation, Alertmanager, the notification integration, the network), the heartbeat's absence is detected by a party outside the chain. This is the dead man's switch applied one level up, to the alerting system itself, and it's the standard kube-prometheus pattern (the "Watchdog" alert → DeadMansSnitch/PagerDuty). Two supporting practices travel with it: meta-monitoring must live in a **different failure domain** from what it monitors (the storage-engineering version of the same rule: never host the monitoring on the SAN it watches — when the SAN failed, the monitor went with it and nobody was paged), and **absence must be a first-class alert condition**, not an inference someone draws from an empty graph.

_Source: PromLabs, "End-to-End Watchdog Alerts" (always-firing alert + external expectation; kube-prometheus Watchdog rule), https://training.promlabs.com/training/monitoring-and-debugging-prometheus/metrics-based-meta-monitoring/end-to-end-watchdog-alerts/ ; separate-failure-domain monitoring, https://awjunaid.com/storage/implementing-monitoring-alerting-and-reporting-strategy-for-storage-protection/_

---

## Part 3 — THE WATCHER'S CHARTER

_The payload. Applies to every league background process: cameraman, curator, digest, governor, consult drivers, capture, actor server, and any successor. Each rule is stated as a checkable property — a sceptical checker with log access should be able to return pass/fail without interviewing the process. "Independent store" means a record the acting process cannot write: the Minecraft server log for world effects, another host's filesystem, or an append-only ledger the process can append to but not edit._

### Rule 1 — Verify the effect in an independent store, or it didn't happen
Every actuation must be confirmed by its effect in an independent store within a declared window (default ≤ 10 s for commands, ≤ 1 period for artefacts). "Sent", "exit 0", and the process's own log are echoes and count for nothing. Two consecutive unverified actuations = **alarm + self-park** into the rule-6 safe state.
_Grounding:_ ECSS PUS Service 1 staged verification (acceptance ≠ execution ≠ completion, each confirmed by telemetry); IEC 61850 SBO position confirmation. _League instance:_ tonight's cameraman guard (server-log landing line within 8 s; two misses → HOLD-LOST alarm + one recovery + STOP). _Compliance check:_ for any sampled actuation in the process's log, the checker finds the matching effect record in the independent store inside the window; the process's log shows the verification result, not just the send.

### Rule 2 — Silence is a failure state: heartbeat with content, or be presumed dead
Every watcher emits a heartbeat into a store it does not own, at a declared period with a declared grace (grace ≈ 2× period). The heartbeat carries *content* — last verified effect, last output artefact id, counters — not a bare "alive". A separate reader alarms on staleness; **no process may be its own only witness.** A watcher whose heartbeat is stale is treated as down in every league status summary, however green its own dashboard looks.
_Grounding:_ dead man's switch / Healthchecks model (period + grace; absence is the alarm); GitLab — the backup that reported into a rejected-email void for months. _Compliance check:_ pick any hour; heartbeat timestamps in the external store are never older than period+grace without a corresponding alarm record.

### Rule 3 — No shared fate with the watched, the alarmed, or the evidence
A watcher, its alarm path, and its evidence store must not depend on the system watched, on each other, or on a single host/channel. If the thing you watch can take your reporting down with it, your reporting is decoration.
_Grounding:_ AWS 2017 — the dashboard's icons and admin lived on the S3 that was down; Facebook 2021 — recovery tooling rode the network it existed to repair. _Compliance check:_ a written dependency list per watcher; a drill (Rule 7) that kills the watched system and shows the alarm still arriving through a surviving path.

### Rule 4 — Page on the black-box symptom, not the white-box story
Each watcher defines one user-visible truth it exists to maintain (daylight held; reels being born; consults being answered; budgets being enforced) and an external probe of that truth. The probe's failure is what alarms; internal metrics are for diagnosis only. A process may never mark itself healthy by a metric the probe contradicts.
_Grounding:_ Google SRE Ch. 6 — black-box monitoring is symptom-oriented and represents active problems; white-box alone masks them. _Compliance check:_ the probe exists, runs from outside the process (ideally outside the host), and its result — not the process's self-report — is what league status summaries quote.

### Rule 5 — Reconcile levels, don't trust edges
Watchers that maintain a state of the world must periodically diff desired vs actual from a fresh read (level-triggered), and their corrective actions must be idempotent — safe to run twice, safe to resume after a crash mid-act. A missed event, a restart, or a duplicated command must converge, not compound.
_Grounding:_ Kubernetes controller pattern (observe → compare → act → repeat; events are hints; idempotent reconciles). _League instances:_ daylight hold as a reconciled level (world time read fresh each cycle) rather than a schedule of remembered sends; curator offsets rebuilt from the manifest store rather than trusted from memory. _Compliance check:_ restart the watcher mid-cycle in a drill; it converges to the correct state with no duplicated or lost effects, and its log shows the diff it acted on.

### Rule 6 — Fail loud, park safe, and write it down before you stop
On unverified state (Rule 1 exhausted, probe contradiction, heartbeat gap in a dependency), a watcher gets a bounded recovery budget — declared in advance, small (one documented recovery attempt is tonight's precedent). Exhausted, it must: stop acting, enter its declared safe state, raise the loudest alarm it has, and leave a durable incident record (mechanism, timeline, last verified effect) in the independent store. Continuing to act on unverified premises is the one unforgivable behaviour — it converts a fault into a false history.
_Grounding:_ IEC 61508 — watchdog expiry forces a safe state without the failed unit's cooperation; Facebook 2021 — the inverse lesson: the audit guard failed to *stop* a dangerous command, so the power to halt must itself be simple and tested. _League instances:_ cameraman self-park via its STOP file; a citizen lane stopping a grinding bot rather than feeding the loop. _Compliance check:_ every park event in the record has an incident note with a last-verified-effect timestamp; no actuation records exist after a park until a verified resume.

### Rule 7 — The alarm path is a product: test it end-to-end on a schedule
Every alarm chain carries an always-on test signal through its full length to an external expecter (the Prometheus Watchdog pattern), and every watcher undergoes a scheduled kill-drill: the watched thing is broken on purpose, in a declared window, and the drill passes only if the alarm arrives and the safe state engages. **A watcher that has never fired a test alarm is assumed broken.** Drill results are ledger entries, not memories.
_Grounding:_ kube-prometheus Watchdog → DeadMansSnitch (the ever-firing alert whose absence pages); GitLab's post-incident standing-up of backup monitoring and restore testing. _Compliance check:_ drill log shows, per watcher per month, one forced failure with alarm-arrival time and safe-state confirmation; the test signal's external expectation has no gaps unexplained by a drill or an incident.

### Rule 8 — Who watches the guard: a boring meta-watcher, and the chain ends outside the fleet
The guard (Rule 1's verifier, Rule 2's staleness reader, Rule 7's expecter) is itself watched by a **meta-watcher** with three properties: (a) it is *boring* — the simplest code in the league, no shared libraries with the watchers, doing only: read heartbeats and verification records, compare ages, alarm; (b) it runs in a different failure domain from the watchers (different host — Thor watches Orin's processes and vice versa — and a different runtime path); (c) its *own* heartbeat is expected by a service **outside the fleet entirely** (a third-party dead-man's-switch endpoint), so the meta-watcher's death also produces an absence alarm that no fleet failure can suppress. The recursion terminates there deliberately: the last link is a human-glanceable surface Casey already looks at (the external service's status), plus the monthly Rule-7 drill in which a human confirms an alarm actually reached a human. There is no rule 9: beyond the meta-watcher, the design goal is not infinite regress but *independence* — each level shares no fate with the level below, so a single failure cannot silence two levels at once.
_Grounding:_ Prometheus end-to-end watchdog (external expecter as the terminus); IEC 61508's external watchdog with a separate time base (the watcher of the watcher is hardware-simple and independent); AWS's post-2017 multi-region dashboard (the reporting surface moved out of the failure it reports). _Compliance check:_ the meta-watcher's heartbeat-expectation is registered with the external service and shows green; killing the meta-watcher in a drill produces the external absence alarm; the meta-watcher's dependency list contains nothing the watchers also depend on except power and Casey's glance.

### Compliance summary — the one-page audit

| Process | Rule 1 effect store | Rule 2 heartbeat → | Rule 4 black-box truth | Rule 6 safe state |
|---|---|---|---|---|
| Cameraman | server log landing lines | Thor ledger, 5 min + grace | world time inside held band, read server-side | STOP self-park |
| Curator | manifest/reel artefacts on disk | Thor ledger (own store doesn't count) | newest reel age < 2 periods, probe names its moments | stop pulsing; offsets frozen + incident note |
| Digest | digest file growth + content hash | external store | a probe can answer "last event digested" matching the log tail | halt + note; never fabricate a summary |
| Governor | budget ledger entries vs call receipts | external store | sampled call's receipt exists in the model's server log | deny-all default on unverified state |
| Consult drivers | answer present in the book + consumed flag set by the citizen loop | external store | round-trip time of a seeded test consult, weekly | stop filing; answers marked stale by epoch |
| Capture | segment files growing on the Orin, verified from the Thor | cross-host heartbeat | newest segment age < 2× segment length | unit stop + note; never overwrite old segments |

_Any row that cannot be filled in for a new process is the design review failing, before the process is allowed to run unattended._

---

## Closing note

The successful always-on systems in this study are not the ones that never fail. GitLab still runs backups; ESA still uplinks commands; Kubernetes controllers crash constantly. What distinguishes them is where the truth lives: in an artefact, a telemetry stream, a position contact, a store the actor can't edit — and in the standing assumption that **silence, self-report and yesterday's green are all the same colour of nothing.** The league already believes this about its citizens — verdicts only from world evidence, never a bot's self-report. The charter simply extends the dock doctrine to the fleet's own machinery: the watchers stand on the same dock as everyone else.

### Sources
- GitLab 2017 postmortem accounts: https://angri-tech.org/en/blog/gitlab-com-database-outage-2017-five-backup-layers-none-working-reliably · https://uptimepage.dev/blog/cron-jobs-fail-silently · https://www.vivianvoss.net/blog/the-backup-that-wasnt
- AWS S3 2017: https://www.theregister.com/off-prem/2017/03/01/awss-s3-outage-was-so-bad-amazon-couldnt-get-into-its-own-dashboard-to-warn-the-world/337924 · https://dev.to/vivian-voss/the-command-that-removed-too-much-115f · https://completestatus.com/blog/s3-outage-status-page-lessons
- Facebook 2021: https://www.networkworld.com/article/970304/facebook-outage-was-a-series-of-unfortunate-events.html · https://datacentercatalog.com/news/2021/facebook-we-disconnected-our-data-centers-from-the-internet
- Google SRE, Ch. 6 Monitoring Distributed Systems: https://sre.google/sre-book/monitoring-distributed-systems/
- Dead man's switch / heartbeat practice: https://www.pagerly.io/blog/cron-job-monitoring-silent-failures-2026-09-15 · https://dev.to/serverkueche/healthchecks-monitor-cron-jobs-backups-dead-mans-switch-2oo1 · https://pulse.pulsecima.com:443/cron-monitoring.html
- Watchdog supervision / IEC 61508: https://www.edn.com/wp-json/wp/v2/posts/5973846 · https://quality.arc42.org/approaches/watchdog-supervision
- End-to-end argument: https://devopedia.org/end-to-end-principle
- ECSS PUS telecommand verification: http://archives.esac.esa.int/hsa/legacy/ADP/SPIRE/SPIRE_docs/SPIRE_Internal_Documents/001078_DOC_DataICD_KJK/PRJ001078_SPIRE_Data_ICD__Issue2.pdf · https://destevez.net/2024/11/hera-telemetry/
- IEC 61850 select-before-operate: https://patents.google.com/patent/EP2293159A1/en
- Kubernetes reconciliation: https://notes.kodekloud.com/docs/Prep-Course-Certified-Cloud-Native-Platform-Engineering-CNPE/Platform-APIs-and-Self-Service-Capabilities/Operators-Controllers-Reconcile-Like-a-Pro/page
- Prometheus end-to-end watchdog alerts: https://training.promlabs.com/training/monitoring-and-debugging-prometheus/metrics-based-meta-monitoring/end-to-end-watchdog-alerts/
- Monitoring in a separate failure domain: https://awjunaid.com/storage/implementing-monitoring-alerting-and-reporting-strategy-for-storage-protection/
