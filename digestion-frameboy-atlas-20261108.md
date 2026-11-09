# Digestion — Frameboy / Atlas (World Labs): a world model streamed to a browser, and the RTFM lineage underneath it

*2026-11-08. Digestion doc under Casey's standing instruction of the same day. Source: Unite.AI report on World Labs' Frameboy release. Source caveat, stated once and plainly: the article's author (Jonas Reeve) is disclosed in the parent handoff as an AI-generated research agent, editorially reviewed — grade the source as a competent secondary digest, not as reporting. The product facts (release, beta status, demo scenes) are checkable; the capability framing is World Labs' own.*

## What shipped

**Frameboy** (World Labs, released 5 Nov 2026): a browser experience that streams Atlas-generated scenes from cloud GPUs at **up to 15 fps with live camera control**. It is integrated into **Viewfinder**, which is in closed beta (waitlist). Demo menu: Stanford Quad, Sutro Baths, Palace of Fine Arts, plus generated scenes (Cyberpunk, Spaceship Interior, Frozen Fortress).

**Atlas** (introduced 1 Sep 2026) is the model underneath: an "omni world model" pretrained from scratch — a multimodal autoregressive diffusion transformer that grounds its inputs in 3D spatial context. Inputs: text, images, camera poses, 3D depth maps. Outputs: up to 1 minute of 1440p video with camera control; reconstructions of real scenes from sparse images; point clouds and 3D Gaussian splats. Viewfinder's loop is the product-shaped version: build a scene frame by frame, receive colour + depth for each Atlas frame, then use the resulting scene as a Frameboy session input.

World Labs' own constraint statement, quoted in the coverage and worth keeping verbatim in spirit: Frameboy **"currently requires a powerful cloud GPU server and is not cheap compared with local rendering methods."** The vendor conceding the economics is the most reliable sentence in the piece.

## The lineage that makes it interesting: RTFM

Atlas did not appear from nowhere. Its research ancestor is **RTFM** (research preview, 16 Oct 2025): real-time interactive frames on a **single H100**, from a *learned renderer with no explicit 3D representation*. RTFM's trick for spatial memory is the detail to keep: instead of attending over an ever-growing history, it keeps **posed frames as spatial memory** and retrieves nearby frames by **"context juggling"** — the past is stored as situated snapshots and re-fetched by pose, not summarised into a latent. Atlas scales RTFM's concepts with a much larger model and orders of magnitude more data, adding explicit 3D outputs (point clouds, splats) that RTFM deliberately lacked.

## Fleet mapping

- **Confluence — the shape rhyme.** Frameboy is a thin browser lending its screen and camera controls to a heavy remote mind: presence/device doctrine in commercial form (the Thor is the only mind; the device is IO). The difference is direction of travel — World Labs streams a *generated* world to the browser; Confluence lends the browser's *senses* to a local mind. Same thin-client conviction, opposite payload. Worth noting because it validates the ergonomics while conceding (in their own words) the cloud cost problem our local-Thor design exists to avoid.
- **Rolling perception:** RTFM's posed-frame memory is a genuine conceptual relative — perception retained as *situated, retrievable frames* rather than a compressed summary, with retrieval by pose/context rather than by attention over everything. Our rolling stream makes the analogous choice for time (rolling beats requested; continuous output folds experimentation into navigation). If the perception line ever needs a spatial-memory design pattern from the literature, "posed frames + context juggling" is the citation.
- **Foundry / Gaussian thread:** Atlas emits 3DGS among its outputs, which puts World Labs on the generation side of the week's five-item Gaussian thread (see batch 2 synthesis). No artefact access; nothing to integrate.
- **League / citizens:** a streamed world model is not a game server and citizens gain nothing from it today. No honest mapping.
- **Jacquard / radio-room / weight-space:** no honest mapping.

## Grade

**C** — a real product in closed beta with a disclosed cloud-cost caveat; capability claims are the vendor's, the source is a secondary digest, and there is no public artefact or benchmark to inspect. The RTFM lineage (a research preview with a described mechanism) is the most durable content here. Park as: *world-model streaming is now a product category with admitted cloud economics; the fleet's local-mind design is the deliberate counter-position.*

---

*Digested 2026-11-08 from the Unite.AI report. No fleet system was touched.*
