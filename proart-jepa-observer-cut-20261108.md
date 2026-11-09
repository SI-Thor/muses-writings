# JEPA over citizen footage — the observer-subtracted cut (ProArt specialty job, 2026-11-08)

**Question.** The 2026-11-07 JEPA-over-play spike found that I-JEPA / V-JEPA 2
embeddings over episode footage measured the *filming apparatus* — camera and
curator framing — more than the citizen: on a PROGRESS/STUCK judgement over
seven 120 s Cody windows, the free transcript scored 6/7, I-JEPA 0/7, V-JEPA 2
1/7, and the measured diagnosis was that the embedding velocity floor is set
by the camera itself (a bit-identical frozen window still registered I-JEPA
velocity 0.72 from spectate micro-motion, cuts and scene animation). The
named cheap fix was never run: label each footage segment with the
cameraman's shot log — which citizen was framed, in what shot type, when —
and ask whether any citizen signal survives once the apparatus is accounted
for. This job runs that test.

**Correction to the brief's premise, found on inventory.** The shot-log
correlation was *not* unbuilt: curator v1.1 (2026-11-07/08) already joins
moments to the shot log — manifest moments carry `on_screen` /
`subject_match` fields derived from 3,943 framing points. In the
multi-citizen era, 529 moments include 208 whose labelled subject does not
match who was actually framed (43% mislabelled in v1); in the Cody-only era,
98 moments, 0 mismatches. So the labelling substrate existed. What had never
been run is the JEPA discrimination test *conditioned* on those labels. That
is what this job adds.

**Venue.** ProArt (eileen, WSL) via the Thor hub (`ssh proart-lan` from the
Thor; the direct route can reset at the proxy hop even when healthy — all
access here went through the hub). Embeddings served by the Thor's JEV rack
(`:8077`) over the LAN, per the brief's preference; no internet downloads, no
local model copies. Fleet data read-only throughout; all new files are in
the ProArt workdir `~/jepa-observer-cut/` plus one read-only-fetched shot-log
copy on the Thor (below).

---

## 1. Inventory — what actually exists

**Curator (Thor `~/curator/`).**

- Manifests: `manifest-2026-11-07.jsonl` (529 moments),
  `manifest-2026-11-08.jsonl` (316), `manifest-2026-11-09.jsonl` (2).
- `review/clips/`: 846 cut clips. `kept/`: 435 raw ~120 s segments, 4.0 GB.
- Correlation code: `~/curator/correlate.py` (`parse_shotlog`,
  `subject_at`, MAX_HOLD_S 300) — reused verbatim for this job's dataset
  build so the labels mean exactly what the curator's labels mean.

**Cameraman shot log (Orin `~/cameraman/cameraman.log`).**

- SHOT lines carry the framing command, including
  `/execute at <Name> run tp` and shot types WIDE / FOLLOW / CLOSE / POV /
  FLY / FACE-CAM / FACE-2SHOT / DEATH-WIDE / ORBIT.
- The Thor's retained copy (`~/curator/shotlog/cameraman-20261108T072335Z.log`)
  ends 2026-11-07T06:03Z and covers the Cody-only era only (698 SHOT lines;
  rotation FOLLOW/WIDE/CLOSE) — **it does not cover the multi-citizen
  footage**, so scoping to the Thor copy alone would have made the primary
  test impossible.
- The live log was therefore fetched read-only from the Orin via the Thor
  hub (`orin-lan`; the `jetson` alias fails rc 255 from the Thor):
  1,322,962 B, sha256 `996f637e66bfacdc…`, 14,079 lines, spanning
  2026-11-07T04:21Z → 2026-11-09T00:27Z, saved as a new file,
  Thor `~/curator/shotlog/cameraman-live-copy-20261108.log`. Nothing
  overwritten anywhere.

**Raw capture (Orin `~/capture/segments/`).** 1,097 raw 120 s segments,
4.9 GB, `segments.jsonl` 1,097 lines. Not needed for this test — the
curator's cut clips are the footage the spike's question is about — but
recorded here as the larger untested pool.

**JEV rack (Thor `:8077`).** Health OK from the Thor and from the ProArt
over the LAN (192.168.0.78:8077): I-JEPA, V-JEPA 2 and the semantic judge all
loaded. I-JEPA card: 99.6 ms mean over 391,239 calls. V-JEPA 2 card: 64
frames, 256×256, 1024-dim output. Measured from the ProArt: V-JEPA 62.8 s
per 16 s clip sequential; a 3-way concurrency probe finished 3 calls in
66.3 s total (≈22 s/clip effective), so the video pass ran 3-way concurrent
— a documented deviation in the workdir RUNLOG; embeddings are per-window
independent, so concurrency cannot change values.

**ProArt tooling.** 15 GB RAM (10 GB available), 830 GB free, Python 3.14.4,
venv with numpy 2.5.4 + requests, full ffmpeg (incl. libx264). No usable
torch environment found (the radio-room venv is not at its expected paths),
so local-GPU inference was not used; the rack route was kept per the brief.
Thor ffmpeg is a minimal build — no libx264, no mpeg4 encoder, mjpeg encoder
broken (Invalid argument −22 on stills) — so window cuts on the Thor used
`h264_nvenc -preset fast -cq 23` (a test cut verified at exactly 16.000 s),
and mid-frame stills were extracted on the ProArt instead. Two failed
encoder attempts preceded the working route; no data was touched by either.

## 2. Overlap and the observer-labelled dataset

Re-segmenting the footage at framing changes (shot-log framing points,
correlate.py semantics) gives:

- **8,270 framing points**: Cody 7,014 / Vega 609 / Geist 369 / two-citizen
  pairs 218 / transitions 60. Shot types across 8,210 points: FOLLOW 2,760 /
  CLOSE 2,055 / WIDE 1,299 / POV 1,292 / FLY 323 / FACE-2SHOT 218 /
  FACE-CAM 204 / DEATH-WIDE 55 / ORBIT 4.
- **844 manifest moments** have usable footage, and all 844 clips are
  present on disk.
- Re-segmentation yields **760 constant-subject sub-clips ≥ 16 s**; their
  shot-log labels agree with the manifest's own `on_screen` field on
  731/760 (96.2%). The 3.8% disagreement is the v1 mislabelling residue —
  the shot log, not the manifest label, is treated as ground truth here.
- 750 single-subject sub-clips tile into **1,770 windows** (16 s, stride
  8 s), 383.8 minutes of labelled footage.

**Labels are the cameraman's commands, not frame-verified per window.** One
documented blind spot: the 04:54–05:02Z rejoin window, where the log cannot
say who was framed.

## 3. The confound map — read this before the results

Shot type is not randomly assigned. It is allocated **by citizen and by
era**, and that structure bounds what any probe on this footage can mean:

- Early era (epoch < 1794100000, ≈ before 2026-11-08T05:46Z): CLOSE windows
  are Geist 327 / Vega 315 / Cody 12. FOLLOW windows pooled are Cody 594,
  but early-era FOLLOW is only Cody 59 / Vega 32 / Geist 22. FACE-CAM's 282
  windows are **all Cody**. The late era's 931 windows are **all Cody**.
- Therefore cross-citizen discrimination is honestly testable in exactly two
  cells: **EARLY × CLOSE (Geist vs Vega)** — the primary test — with
  EARLY × FOLLOW (3-way, small n) as replication.
- Citizen identity is also confounded with **location**: each citizen was
  filmed mostly at their own anchor / home ground, so "separates Geist from
  Vega" can be place/scene recognition rather than behaviour. This is
  stated in the preregistration and is **not removable with existing
  footage**. Any positive result below inherits this caveat in full.
- Citizen is further confounded with moment-type mix (what the curator
  chose to keep differs per citizen).

## 4. Pre-registered probe (written before any probe embedding was computed)

Filed at ProArt `~/jepa-observer-cut/PREREGISTRATION.md`, sha256
`10f96fa28fa211b490e5f5f26be08392ca4d9d1438eaf9df36ae891f95b3f469`.

**Sample** (deterministic, seed 20261108; ≤1 window per sub-clip preferred,
≤2 allowed): **346 windows from 279 source clips** — Geist-early-CLOSE 80,
Vega-early-CLOSE 80, Cody-early-CLOSE 12 (all that exist),
Cody-early-FOLLOW 40, Vega-early-FOLLOW 32 (all), Geist-early-FOLLOW 22
(all), Cody-late-FOLLOW 40, Cody-late-CLOSE 40.

**Classifiers.** Nearest-centroid cosine and 1-NN cosine, leave-one-out,
balanced accuracy. Significance: 1,000 label shuffles **at sub-clip level**
(windows from one sub-clip share a shuffled label, so overlapping windows
cannot leak), seed 7. Majority baseline = 1/n_classes.

**Probes.**

- **P1 — apparatus audit (raw, pooled):** predict SHOT TYPE from the
  embedding, all sample windows pooled. This is the (a) raw arm's measure
  of how much of the embedding is apparatus.
- **P2 — citizen, raw:** predict citizen, early era pooled across shot
  types. The naive pooled number, expected to be inflated by the
  shot-type × citizen allocation above.
- **P3 — PRIMARY, observer-conditioned:** within EARLY × CLOSE only,
  Geist vs Vega, 80/80 balanced. Same camera state, same era; the only
  cell where the apparatus is held constant across citizens.
- **P3 secondary:** EARLY × FOLLOW, 3-way (Cody/Vega/Geist), small n.
- **P4 — transfer:** train the centroid on FOLLOW, test on CLOSE, and
  reverse (Geist vs Vega). If the citizen signal is behaviour rather than
  shot-specific appearance, it should survive a change of camera state.
- **P5 — placebo:** Cody only, predict ERA (early vs late), pooled and
  within FOLLOW. Cody is one citizen; an "era" signal here is
  scene/apparatus drift, and it calibrates how much non-behaviour signal
  the embeddings carry even with citizen held constant.

**Decision rule (pre-registered).** The observer-subtracted route earns a
second spike **iff** P3 balanced accuracy ≥ 0.65 for at least one
classifier with permutation p < 0.01 — with the report stating plainly how
much of that signal could be place/scene rather than behaviour. Otherwise
the verdict is negative and the route closes.

**Embedding pass (as run).** 346 windows cut on the Thor (800.8 MB, 0
failures on the working route), transferred Thor→ProArt over the LAN hub
(765 MB), stills extracted on the ProArt. V-JEPA 2: 346/346. I-JEPA:
346/346. Zero failures. Video pass wall time ≈2 h 20 m at 3-way
concurrency under shared-Thor contention.

## 5. Results

All cells: leave-one-out, balanced accuracy; permutation p from 1,000
sub-clip-level label shuffles (p = 0.000999 is the floor — no shuffle matched
the real accuracy). Full machine-readable results: ProArt
`~/jepa-observer-cut/results/probes.json`.

### (a) Raw / pooled — the spike's view, reproduced and quantified

**P1, apparatus audit** (predict shot type, CLOSE vs FOLLOW — the only two
shot types the citizen design could sample; n = 346, chance 0.50):

| Model | Centroid | 1-NN |
|---|---|---|
| V-JEPA 2 | 0.865, p < 0.001 | 0.915, p < 0.001 |
| I-JEPA | 0.776, p < 0.001 | 0.876, p < 0.001 |

The apparatus is unambiguously in the embeddings: shot type is decodable
far above chance from both models. This is the quantitative form of the
original spike's verdict.

**P2, citizen raw, early era pooled across shot types** (n = 266 —
Cody 52 / Geist 102 / Vega 112; chance 0.333):

| Model | Centroid | 1-NN |
|---|---|---|
| V-JEPA 2 | 0.623, p < 0.001 | 0.861, p < 0.001 |
| I-JEPA | 0.576, p < 0.001 | 0.833, p < 0.001 |

Pooled citizen separation looks strong — and per §3 it cannot be read at
face value, because shot type is allocated by citizen in this era (Cody is
mostly FOLLOW; Geist and Vega are mostly CLOSE). P2 is what you get when
the apparatus is pooled rather than controlled: a number inflated by an
unknown amount of camera allocation.

### (b) Observer-conditioned — apparatus held constant

**P3 PRIMARY — within EARLY × CLOSE, Geist vs Vega** (80/80 balanced,
chance 0.50). Same era, same camera state; the only cell where a citizen
contrast is honestly testable in this footage:

| Model | Centroid | 1-NN |
|---|---|---|
| V-JEPA 2 | **0.806, p < 0.001** | **0.869, p < 0.001** |
| I-JEPA | **0.744, p < 0.001** | **0.863, p < 0.001** |

The pre-registered bar (≥ 0.65 at p < 0.01 for at least one classifier) is
met by **all four** model × classifier combinations. Conditioning on the
shot log changes the answer: inside one camera state there is robust
citizen separation where the pooled analysis is dominated by apparatus.

**P3 secondary — EARLY × FOLLOW, 3-way** (Cody 40 / Geist 22 / Vega 32,
chance 0.333): V-JEPA centroid 0.541 (p = 0.007), 1-NN 0.880 (p < 0.001);
I-JEPA centroid 0.440 (**p = 0.111, not significant**), 1-NN 0.822
(p < 0.001). The 1-NN arm replicates; the centroid arm is weak and absent
for I-JEPA. Small n, especially Geist (22).

**P4 — transfer across camera states** (centroid; train on one shot type,
test on the other, Geist vs Vega; chance 0.50):

| Direction | V-JEPA 2 | I-JEPA |
|---|---|---|
| FOLLOW → CLOSE | 0.488 | 0.475 |
| CLOSE → FOLLOW | 0.484 | 0.443 |

**Zero transfer, in all four cells, at or below chance.** The direction in
embedding space that separates Geist from Vega inside CLOSE is not the
direction that separates them inside FOLLOW. A citizen/behaviour
representation should be at least partially invariant to camera state;
this signal is entirely shot-specific.

**P5 — placebo: Cody only, predict ERA** (citizen held constant; chance
0.50). Pooled (early 52 / late 80): V-JEPA centroid 0.774, 1-NN 0.959;
I-JEPA centroid 0.719, 1-NN 0.861 — all p < 0.001. **Within FOLLOW only**
(citizen *and* shot type held constant, 40/40): V-JEPA centroid 0.863,
1-NN 0.963; I-JEPA centroid 0.838, 1-NN 0.900 — all p < 0.001.

The placebo reaches accuracy **equal to or higher than the primary citizen
effect** (0.84–0.96 vs 0.74–0.87) with no citizen contrast in it at all.
What differs between Cody-early and Cody-late is when and where he was
filmed — the world state around him, his built-up homestead, the footage's
era. The embeddings are excellent *place/time fingerprints*.

**A structural tell across all probes:** 1-NN beats centroid everywhere,
often by a wide margin (P2: +0.24/+0.26; P3 secondary: +0.34/+0.38).
1-NN exploits local neighbourhood structure — windows near other windows
from the same place — while centroid measures a global class direction.
The permutations were at sub-clip level, so this is not leakage between
overlapping windows: the neighbours that vote are genuinely different
sub-clips of the same ground. A signal that lives in local clusters and
has no global, shot-invariant direction is the signature of **scene
identity**, not of behaviour.

## 6. Verdict

**By the pre-registered decision rule, the observer-subtracted route earns
its second spike**: P3 balanced accuracy 0.74–0.87 against the ≥ 0.65 bar,
p < 0.001 in all four cells. Conditioning on the cameraman's shot log is
not cosmetic — it converts the spike's pooled "mostly apparatus" picture
into a controlled contrast with a real, significant effect. That part is a
clean positive, and the labelling substrate (shot log + correlate.py) is
proven reusable: 8,270 framing points, 96.2% label agreement with the
manifest, 1,770 tiled windows.

**But the same pre-registered battery answers the behaviour question
negatively, and the report must say so plainly.** The P3 effect is fully
explainable without any citizen behaviour: (i) P4 shows the separation
does not survive a change of camera state — it is a within-shot appearance
effect; (ii) P5 shows embeddings separate *eras of the same citizen, in
the same shot type*, as strongly as they separate citizens — they encode
where/when footage was taken at least as well as who is in it; and (iii)
each citizen was filmed predominantly at their own home ground (§3), so
"Geist vs Vega within CLOSE" is, on this footage, also "Geist's ground vs
Vega's ground." **How much of the P3 signal could be place/scene rather
than behaviour? On the P4 + P5 evidence: plausibly all of it.** No
measurement in this battery isolates a behaviour component above zero.

**Recommendation.** A second spike is worth it only if it is designed to
break the citizen ↔ place confound, which this footage cannot do:

1. Film citizens at shared and swapped locations (both citizens on the
   same ground, ideally in the same session), then re-run P3 within shot
   type *and* within location. Citizen separation that survives a location
   swap is the first evidence behaviour could claim.
2. Keep P4 (cross-shot transfer) and a same-citizen placebo (P5-style) as
   mandatory arms — they were the two probes that did the real work here.
3. Do not scale up window counts on the existing footage: more windows of
   the same confounded allocation only measure scene identity more
   precisely.

If the goal is a citizen-behaviour readout rather than a
citizen-recognition one, the cheaper instrument remains the one the
original spike crowned: the free transcript / state feed, which beat both
JEPA models decisively in 2026-11-07 and is untouched by any of these
apparatus problems.

**Failure class of the original spike, restated with this job's evidence:**
not "embeddings contain no citizen information" — they contain plenty —
but *pooled judgement over unlabelled footage attributes scene, era and
camera allocation to the citizen*. The observer's contribution is real,
measurable (P1), and removable by conditioning (P3 design) — what remains
after conditioning is, on present evidence, the place the observer was
pointed at.

---

### Process notes / deviations (as-run)

- Shot log: Thor's retained copy ended 2026-11-07T06:03Z (Cody era only);
  the live Orin log was fetched read-only via the Thor hub and saved as a
  new file — the primary test is impossible without it, and the gap is a
  standing curator-hygiene item (retain the full log with the manifests).
- Thor ffmpeg lacks libx264/mpeg4 encoders and its mjpeg encoder is
  broken; cuts used `h264_nvenc`, stills were extracted on the ProArt.
  Two failed encoder attempts, no data touched.
- V-JEPA rack latency (62.8 s/clip sequential) motivated 3-way concurrent
  embedding calls (≈22 s/clip effective); per-window independence means
  values are unaffected. Documented in the workdir RUNLOG at the time.
- No torch env usable on the ProArt; embeddings via the JEV rack over LAN
  throughout, per the brief's preference. Loads stayed modest and
  stoppable; the box was never exclusively held.

### Artefacts

- ProArt workdir `~/jepa-observer-cut/`: `PREREGISTRATION.md` (sha256
  `10f96fa28fa211b490e5f5f26be08392ca4d9d1438eaf9df36ae891f95b3f469`),
  `RUNLOG.md`, `sample.json`, `dataset/` (sub-clips, windows),
  `windows/` (346 mp4 + 346 mid-frame jpgs), `embeddings/` (692 .npy),
  `results/probes.json`, `src/` (embed + probe code).
- Thor scratch: `/tmp/observer_dataset/` (framing points, sub-clips,
  windows, sample), `/tmp/observer_windows/`; shot-log copy at
  `~/curator/shotlog/cameraman-live-copy-20261108.log` (sha256
  `996f637e66bfacdc…`).
- This digestion: `~/workspace/studies/proart-jepa-observer-cut-20261108.md`.
