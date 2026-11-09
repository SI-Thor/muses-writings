# Digestion — VFlash: verify the *shape* of a prediction, not its tokens

*2026-11-08. Digestion doc under Casey's standing instruction of the same day. Source: Interesting Engineering (6 Nov 2026) reporting "VFlash: Fast, Accurate Visual Planning via Flash Primitive Decoding" (NVIDIA + collaborators, Nov 2026). Journalism-grade source; all performance figures carry "up to" qualifiers and are dataset/configuration-dependent as reported. Grade accordingly: the idea is gradeable today, the numbers are claims.*

## The problem it attacks

Vision-language models emit spatial predictions — waypoints, trajectories, points — **one coordinate at a time**, autoregressively. Spatial output is slow for the same reason prose is slow, but with a worse property: a trajectory is not improved by being generated token-by-token, and standard speculative decoding's exact-match verification is a poor fit for numbers, where a near-miss coordinate is usually still a *valid* plan.

## The move — and why it is the interesting part

VFlash pairs the VLM with a **lightweight diffusion drafter that predicts the coordinates jointly in one forward pass**, and then — the key design decision — **accepts predictions that are structurally valid without requiring token-by-token agreement with the target model**. Verification is by *structure*, not by *exact match*.

Set this beside D3D (see the D3D+Cosmos index entry): speculative decoding's classic bargain is "draft cheap, verify exactly." VFlash changes the verification predicate for spatial outputs: if the drafted trajectory is well-formed and plausible as a plan, accept it. That is a transfer of trust from token identity to *shape validity* — the same relocation of verification this week's batch keeps exhibiting (verification moves from re-checking outputs to constraining/validating their form).

## Numbers as reported

- Trajectory decoding **up to 12× faster**.
- 3D trajectory average displacement error **down up to 61%** (dataset/config-dependent — the "up to" is doing real work here).
- **Jetson Thor end-to-end latency 3,552.7 ms → 703.3 ms (~80% reduction)**; DGX Spark 3,356.5 → 649.9 ms. (Vendor-platform numbers; the Thor figure is the one we can eventually check against our own bench.)
- 3D point-motion forecasting: ~25× faster generation — flagged as preliminary, single-rollout.
- Plugged into a world action model on MolmoSpaces: **70.2% average task success vs 62.6% baseline**; pick-and-place +11.6 points; object-closing +12.8 points.
- Driving (NAVSIM / Waymo trajectories): competitive, improved further with RL.

## Fleet mapping

- **Thor edge serving / robotics direction:** a ~5× latency cut on spatial prediction *on our exact board* is directly relevant to any future Thor-resident planning component (citizen navigation planning is scripted today; a VLM planner is not on the roadmap, but if one arrives, its decoding strategy is this paper's question). The honest status: a technique to remember, with vendor numbers.
- **Rolling perception / telltape:** the transferable idea is the verification predicate. Our own stack already prefers structural checks (schema-valid signals, typed answers) over re-derivation; "accept if structurally valid" is that preference inside a decoder. Noted as a design-pattern witness, not a component.
- **League / citizens:** citizens' failures are locomotion and margins in a real body, not plan-decoding latency. No honest mapping today.
- **Jacquard / foundry / radio-room / weight-space:** no honest mapping.

## Grade

**C+ as reported** (journalism-grade source, "up to" numbers, no artefact inspected this pass) for an idea that is plausibly **B-class** once the paper itself is read. Park as: *structural-verification-for-spatial-decoding — remember the predicate, distrust the multipliers until the paper is in hand.*

---

*Digested 2026-11-08 from the Interesting Engineering report. No fleet system was touched.*
