# Digestion — La-JEPA: JEPA features as a control substrate, not a description

*2026-11-08. Digestion doc under Casey's standing instruction of the same day (thorough markdown research/digestion documents for everything submitted, including today's earlier items). Source: the La-JEPA paper as surfaced by ScholarBro (published 5 Nov 2026; 0 citations, 45 references at read time); abstract read in full.*

> **Status marker: a replication spike is in flight separately (Thor, `~/la-jepa-spike/`, crew dispatched 2026-11-08). Verdict pending. This doc digests the paper's claims and fixes the fleet framing; it does not duplicate the spike's work and will not be updated with a verdict — the spike's own record carries that.**

## What La-JEPA is

La-JEPA (Latent Action JEPA) is a compact policy transformer trained **from scratch in the feature space of a pretrained V-JEPA 2.1 encoder**. It descends from the Fast-WAM lineage: during training it predicts *future features jointly with actions*; at inference it generates **only actions** — the future-prediction machinery is a training scaffold, discarded at deployment. The thesis is in one sentence: robot foundation models may benefit from architectures *designed for control* rather than inherited from generation.

## Claims (paper-reported)

- State of the art **among policies without embodied pretraining** on clean and randomised RoboTwin 2.0 and on LIBERO-Plus with correct instructions — with far fewer parameters than the comparison class.
- Substantially faster than Fast-WAM at comparable performance; beats LeapBot-WA and JEPA-WAM without their pretrained policy backbones.
- On four real-robot tasks, average success comparable to π0.5 and above the non-embodied-pretrained baselines.
- Design study: **JEPA features outperform video VAE latents**, most clearly out of distribution; and training-time future-prediction choices significantly shape the resulting policy *even when prediction is skipped at inference* — the auxiliary loss is doing representational work, not just multi-task decoration.
- A disclosure worth more than most results: the authors found that **the official LIBERO-Plus evaluator corrupts instructions for most variants**; they corrected the instructions and re-evaluated several strong open baselines themselves. Any prior LIBERO-Plus comparison that used the stock evaluator is suspect — including, potentially, numbers quoted elsewhere in our own studies. Evaluator hygiene of this kind is exactly the "verify the effect in a store you cannot write" instinct applied to benchmarks.

## Why this is not a contradiction of our negative result

Last night's JEV-over-play spike was a clean **negative** for JEPA-as-*description*: embeddings of citizen footage measured the filming apparatus (camera, framing) before they measured the citizen, and a free transcript beat I-JEPA/V-JEPA decisively. La-JEPA is JEPA-as-*control substrate* — a different claim about a different use:

| | JEV-over-play (our spike) | La-JEPA |
|---|---|---|
| Question | "What is happening in this footage?" | "What action follows from this state?" |
| Signal path | Footage → embedding → judgement | Proprioceptive/visual features → policy → action |
| Failure mode found | Embeddings encode the observer | (Paper's OOD arm: JEPA features degrade *less* than VAE latents) |
| Verdict | Negative, measured | Claimed positive, in spike replication |

Both can be true. A representation can be a poor *witness* and a good *steering wheel*; description and control make different demands. Our citizens' measured failures were bodies and margins (locomotion pins, food floors), not representations — so even a fully confirmed La-JEPA would not be a league remedy; it would be a robotics result. The spike exists because the claim is cheap to test on the Thor and the answer is interesting either way.

## Spike design (pointer, not duplication)

The spike (Thor `~/la-jepa-spike/`) is pre-registered in its METHODS.md: variant A action-loss only, variant B action + future-feature loss, variant C a VAE-latent baseline if cheap; a LIBERO/RoboTwin subset; a **mandatory out-of-distribution arm** (the paper's strongest claim lives there); and a written kill criterion. Toshiba offload was sanctioned for weights with move-records and hash verification. This doc will not be edited when the spike lands — the spike record is the verdict's home; the index entry will point at both.

## Grade

**A− as a paper** (method + design study + evaluator correction disclosed; results not yet independently replicated, and this digestion is abstract-level). The grade attaches to the artefact, not to our belief: belief is what the spike is for.

---

*Digested 2026-11-08. Sources: La-JEPA paper via ScholarBro (abstract in full). Fleet framing is this doc's analysis. No league system was touched.*
