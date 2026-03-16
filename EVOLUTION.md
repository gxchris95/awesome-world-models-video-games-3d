# The Evolution of World Models for Video, Games & 3D

A deep analysis of how methods build upon each other — from foundational ideas to the current frontier.

---

## Table of Contents

- [The Two Founding Philosophies (2018–2022)](#the-two-founding-philosophies-20182022)
- [The Big Bang: February 2024](#the-big-bang-february-2024)
- [The Major Lineages (2024–2026)](#the-major-lineages-20242026)
  - [The Genie Line: From 2D to Real-Time 3D](#the-genie-line-from-2d-to-real-time-3d)
  - [The V-JEPA Line: From Understanding to Action](#the-v-jepa-line-from-understanding-to-action)
  - [The Cosmos Line: Platform Play](#the-cosmos-line-platform-play)
- [The Game Simulation Arc: From RL Training to Multiplayer Worlds](#the-game-simulation-arc-from-rl-training-to-multiplayer-worlds)
  - [Phase 1: Diffusion as Environment (May–Oct 2024)](#phase-1-diffusion-as-environment-mayoct-2024)
  - [Phase 2: Scale and Specialization (Jan–Aug 2025)](#phase-2-scale-and-specialization-janaug-2025)
  - [Phase 3: Self-Forcing and Multi-Agent (Late 2025–2026)](#phase-3-self-forcing-and-multi-agent-late-20252026)
  - [The Domain Progression](#the-domain-progression)
  - [The Speed Progression](#the-speed-progression)
  - [The Action-Conditioning Progression](#the-action-conditioning-progression)
  - [The Memory Strategies](#the-memory-strategies)
- [The 3D World Generation Arc](#the-3d-world-generation-arc-from-implicit-to-native-3d)
- [The Physics Thread](#the-physics-thread-from-they-cant-to-steer-at-inference)
- [Cross-Pollination: The Architectural Imports](#cross-pollination-the-architectural-imports)
- [The Convergence: Hybrid Architectures](#the-convergence-hybrid-architectures)
- [How It All Connects](#how-it-all-connects)

---

## The Two Founding Philosophies (2018–2022)

Everything in this landscape descends from two opposing bets on how machines should model the world:

1. **[Ha & Schmidhuber (2018)](https://arxiv.org/abs/1803.10122)** — *"World Models"*: Learn an environment simulator (VAE + RNN + Controller), then train agents *inside their own dreams*. The key legacy: **most complexity belongs in the world model, not the policy**. [PlaNet (2019)](https://arxiv.org/abs/1811.04551) refined this into the RSSM (Recurrent State-Space Model) for latent dynamics, which fed directly into the Dreamer series ([V1](https://arxiv.org/abs/1912.01603)→[V2](https://arxiv.org/abs/2010.02193)→[V3](https://arxiv.org/abs/2301.04104)), proving agents could learn entirely in imagination, eventually collecting diamonds in Minecraft from scratch.

2. **[LeCun (2022)](https://openreview.net/pdf?id=BZ5a1r-kVsf)** — *"A Path Towards Autonomous Machine Intelligence"*: Proposed JEPA — predict in *abstract representation space*, never in pixel space. The core thesis: generative models waste capacity hallucinating pixel-level detail that is irrelevant for understanding. This became Meta's V-JEPA line.

These two philosophies — **generate pixels vs. predict in latent space** — remain the central tension in the field today.

---

## The Big Bang: February 2024

Three foundation models launched simultaneously, each taking a different architectural bet:

| Model | Architecture | Key Bet |
|-------|-------------|---------|
| **[Sora](https://openai.com/research/video-generation-models-as-world-simulators)** | DiT (Diffusion Transformer) + spacetime patches | Scale diffusion transformers on video → emergent world simulation |
| **[Genie](https://arxiv.org/abs/2402.15391)** | VQ-VAE + MaskGIT + Latent Action Model | Learn action control from *unlabeled* video via discrete tokens |
| **[V-JEPA](https://github.com/facebookresearch/jepa)** | Non-generative JEPA with spatiotemporal masking | Predict masked video in latent space, never generate pixels |

**[Sora](https://openai.com/research/video-generation-models-as-world-simulators)** borrowed DiT's insight (Peebles & Xie, 2022) that replacing U-Nets with Vision Transformers unlocks scaling laws for diffusion. Its innovation was **spacetime patches** — decomposing video into 3D chunks that serve as transformer tokens, enabling variable resolution/duration. OpenAI positioned it not as a video generator but as a "world simulator," and this framing shaped the field's ambition.

**[Genie](https://arxiv.org/abs/2402.15391)** took VQ-VAE's discrete tokenization and made a radical bet: you don't need action labels. Its **Latent Action Model** discovers controllable actions (just 8 discrete codes) from 30K hours of unlabeled platformer gameplay. This was the first proof that interactive world simulation could emerge from passive video.

**[V-JEPA](https://github.com/facebookresearch/jepa)** operationalized LeCun's thesis: mask large spatiotemporal regions of video, predict the missing representation (not pixels). The result was 1.5–6x training efficiency and frozen-encoder transfer that outperformed generative alternatives. No decoder needed.

---

## The Major Lineages (2024–2026)

### The Genie Line: From 2D to Real-Time 3D

```
Genie (Feb 2024) ──→ Genie 2 (Dec 2024) ──→ Genie 3 (Aug 2025)
2D platformers        3D worlds, 1 min         Real-time 24fps 720p
VQ-VAE + MaskGIT      Latent diffusion          Optimized inference
Latent actions         Emergent NPCs             Text-promptable events
```

**Genie → [Genie 2](https://deepmind.google/discover/blog/genie-2-a-large-scale-foundation-world-model/):** Swapped MaskGIT for **autoregressive latent diffusion** with causal masking (borrowing from LLM architecture), jumping from 2D to rich 3D with emergent NPC behavior and object permanence.

**Genie 2 → [Genie 3](https://deepmind.google/discover/blog/genie-3-a-new-frontier-for-world-models/):** Solved the deployment problem — real-time generation at 24fps/720p with multi-minute consistency — by optimizing how the model handles growing trajectory context.

### The V-JEPA Line: From Understanding to Action

```
I-JEPA (2023) ──→ V-JEPA (Feb 2024) ──→ V-JEPA 2 (Jun 2025)
Images               Video                  Video + Robot Actions
Representation        Spatiotemporal mask     1M+ hours, zero-shot planning
                                             16x faster than generative planners
```

[V-JEPA 2](https://arxiv.org/abs/2506.09985) added **action conditioning** (V-JEPA 2-AC) — the non-generative world model could now plan robot actions by predicting outcomes in latent space, achieving zero-shot transfer to new environments. This supported LeCun's thesis: you don't need to generate pixels to act in the world.

### The Cosmos Line: Platform Play

```
Cosmos (Jan 2025) ──→ Cosmos-Predict2.5 (Oct 2025)
Separate models        Unified flow architecture
per modality           Text/Image/Video2World in one model
Open-source            RL post-training on 200M clips
```

NVIDIA's bet was different: not a single model but an **open-source platform** — tokenizers, pre-trained models, and fine-tuning recipes. [Cosmos-Predict2.5](https://arxiv.org/abs/2511.00062) unified three separate models into one flow-based architecture, adding a text-grounding reasoning module (Cosmos-Reason1). The innovation was infrastructure, not architecture. (The diagram below reflects this by placing Cosmos under "Platform" rather than alongside the model lineages.)

---

## The Game Simulation Arc: From RL Training to Multiplayer Worlds

This is the most dramatic evolutionary thread. In 24 months, game world models went from offline RL environments to real-time multiplayer engines.

### Phase 1: Diffusion as Environment (May–Oct 2024)

**[DIAMOND](https://arxiv.org/abs/2405.12399)** (May 2024) asked: what if we replace DreamerV3's discrete latent tokenizer with a diffusion model? The answer: visual details that discrete tokens discard actually matter for RL policy quality. SoTA on Atari 100k. But it was batch-only, not interactive.

**[GameNGen](https://arxiv.org/abs/2408.14837)** (Aug 2024) proved the concept could scale to 3D. Google trained an RL agent to play DOOM, used the gameplay as training data, and ran a Stable-Diffusion-based model at 20 FPS. The key trick: **conditioning augmentation** (adding noise to past frames during training) prevented error accumulation during autoregressive rollout. This was one of the earliest proofs that diffusion models could serve as real-time game engines.

**[Oasis](https://oasis-model.github.io/)** (Oct 2024) took a different architectural approach: transformers instead of U-Nets, **Dynamic Noising** instead of conditioning augmentation, Minecraft instead of DOOM. The domain shift to Minecraft was consequential — procedural infinite worlds, clear action spaces, and an active research community made it the default benchmark.

### Phase 2: Scale and Specialization (Jan–Aug 2025)

The field split into several threads:

**Memory.** [WORLDMEM](https://arxiv.org/abs/2504.12369) (Apr 2025) added an explicit **memory bank with pose-indexed storage**, solving the "revisitation problem" — when you return to a previously seen area, the model retrieves stored frames rather than hallucinating. This influenced [Captain Safari](https://arxiv.org/abs/2511.22815)'s pose-conditioned retrieval.

**Scale.** [Matrix-Game](https://arxiv.org/abs/2506.18701) (Jun 2025) went big — 17B parameters, 3,700 hours of Minecraft data, the GameWorld Score benchmark. Then [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) (Aug 2025) solved deployment: switch from bidirectional to **causal attention**, distill from many denoising steps to few, achieve **25 FPS streaming**.

**Language control.** [AnimeGamer](https://arxiv.org/abs/2504.01014) (Apr 2025) replaced keyboard/mouse with MLLM-generated game states. [Hunyuan-GameCraft-2](https://arxiv.org/abs/2511.23429) (Nov 2025) took this further with a 14B MoE model accepting free-form text instructions ("open the door", "trigger explosion").

**Real-world transfer.** [RealPlay](https://arxiv.org/abs/2506.18901) (Jun 2025) showed that game world model techniques transfer to photorealistic real-world video — train on game controls, apply to real scenes without real-world action annotations.

### Phase 3: Self-Forcing and Multi-Agent (Late 2025–2026)

The **self-forcing** training paradigm was the key unlock. Traditional teacher forcing creates a train-test mismatch: the model trains on ground-truth context but at inference conditions on its own (flawed) outputs. Self-forcing trains the model on its own generated context via autoregressive rollout with KV caching, using video-level loss instead of frame-wise loss.

The evolution of training paradigms:

| Paradigm | Mechanism | Limitation |
|----------|-----------|------------|
| **Teacher Forcing** | Train on ground-truth context | Exposure bias at inference |
| **Scheduled Sampling** (Bengio 2015) | Gradually mix in model predictions | Heuristic schedules, limited |
| **Diffusion Forcing** (NeurIPS 2024) | Independent per-token noise levels | Bridges sequence and diffusion |
| **Self Forcing** (NeurIPS 2025) | Train on self-generated context, video-level loss | Memory cost scales linearly |
| **Checkpointed Self Forcing** (Solaris 2026) | Cache intermediates without gradients | Sublinear memory scaling |

**[Waypoint-1](https://over.world/blog/the-path-to-real-time-worlds-and-why-it-matters)** (Jan 2026) used self-forcing + DMD distillation to achieve real-time interactive world generation from 10K hours of gameplay, trained from scratch.

**[Solaris](https://arxiv.org/abs/2602.22208)** (Feb 2026) introduced **Checkpointed Self Forcing** — a memory-efficient variant — to build the first **multiplayer world model**. Multiple agents in Minecraft seeing consistent, synchronized views of the same world. This is the current frontier.

#### The Domain Progression

| Era | Game | Complexity | Key Models |
|-----|------|-----------|------------|
| 2024 | Atari | 2D, simple sprites | [DIAMOND](https://arxiv.org/abs/2405.12399) |
| 2024 | DOOM | 3D FPS, limited assets | [GameNGen](https://arxiv.org/abs/2408.14837) |
| 2024–2025 | Minecraft | 3D voxel, procedural, infinite | [Oasis](https://oasis-model.github.io/), [MineWorld](https://arxiv.org/abs/2504.08388), [Matrix-Game](https://arxiv.org/abs/2506.18701), [Solaris](https://arxiv.org/abs/2602.22208) |
| 2025+ | GTA5 / Unreal | Photorealistic 3D | [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009), [RealPlay](https://arxiv.org/abs/2506.18901) |

#### The Speed Progression

| Model | Date | Speed | How |
|-------|------|-------|-----|
| [DIAMOND](https://arxiv.org/abs/2405.12399) | May 2024 | Batch (offline) | Diffusion, no optimization |
| [GameNGen](https://arxiv.org/abs/2408.14837) | Aug 2024 | 20 FPS | Conditioning augmentation |
| [Oasis](https://oasis-model.github.io/) | Oct 2024 | 20 FPS | Dynamic Noising + DiT |
| [MineWorld](https://arxiv.org/abs/2504.08388) | Apr 2025 | 4–7 FPS | Parallel token decoding |
| [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) | Aug 2025 | 25 FPS | Causal attention + distillation |
| [Waypoint-1](https://over.world/blog/the-path-to-real-time-worlds-and-why-it-matters) | Jan 2026 | 30 FPS | Self-forcing + DMD |

#### The Action-Conditioning Progression

```
No actions ──→ Latent actions ──→ Keyboard/mouse ──→ Camera/pose ──→ Language ──→ Cross-domain
(Sora)         (Genie)            (GameNGen)         (GEN3C)         (GameCraft-2)  (GWM-1)
```

*GEN3C = NVIDIA's camera-conditioned 3D-consistent video generation. GameCraft-2 = Hunyuan-GameCraft-2 (see Phase 2 above).*

Key stepping stones:

- **[iVideoGPT](https://arxiv.org/abs/2405.15223)** (May 2024): First GPT-style interactive world model with compressive tokenization.
- **[AdaWorld](https://arxiv.org/abs/2503.18938)** (Mar 2025): Self-supervised latent action extraction enabling zero-shot transfer across *unseen* environments — no retraining per domain.
- **[Vid2World](https://arxiv.org/abs/2505.14357)** (May 2025): Showed you can **causalize** an existing pretrained video diffusion model (reshape architecture, retrain with causal objectives) to make it interactive.
- **[RELIC](https://arxiv.org/abs/2512.04040)** (Dec 2025): Camera-aware compressed latent tokens in KV cache → real-time 16 FPS long-horizon interaction.
- **[LIVE](https://arxiv.org/abs/2602.03747)** (Feb 2026): Cycle-consistency (forward-backward generation) eliminates need for teacher distillation — a training-free path to long-horizon coherence.
- **[Generated Reality](https://arxiv.org/abs/2602.18422)** (Feb 2026): Full embodied tracking — 3D head pose + joint-level hand poses → dexterous egocentric world simulation.

#### The Memory Strategies

| Strategy | Representative | Mechanism |
|----------|---------------|-----------|
| Fixed context window | [DIAMOND](https://arxiv.org/abs/2405.12399), [GameNGen](https://arxiv.org/abs/2408.14837) | Limited frame history |
| KV cache compression | [Oasis](https://oasis-model.github.io/), [RELIC](https://arxiv.org/abs/2512.04040), [Yume-1.5](https://arxiv.org/abs/2512.22096) | Sliding window / linear attention |
| Explicit memory bank | [WORLDMEM](https://arxiv.org/abs/2504.12369), [Captain Safari](https://arxiv.org/abs/2511.22815) | Pose-indexed frame storage + retrieval |
| SSM-based memory | [Long-Context SSM WMs](https://arxiv.org/abs/2505.20171) | Linear-cost long-range temporal |
| Cycle-consistent | [LIVE](https://arxiv.org/abs/2602.03747) | Forward-backward reconstruction |
| Reconstituted context | [WorldPlay](https://arxiv.org/abs/2512.14614) | Rebuild past frames with temporal reframing |

---

## The 3D World Generation Arc: From Implicit to Native 3D

This thread shows a rapid representation evolution in ~15 months:

```
Meshes              Implicit fields ──→ Point clouds ──→ Gaussians ──→ Hybrid
(Jul 2025)          (Sep 2025)          (Oct 2025)       (Dec 2025)
HunyuanWorld        FantasyWorld        Terra, EvoWorld   Visionary, WonderZoom
```

**[FantasyWorld](https://arxiv.org/abs/2509.21657)** (Sep 2025) introduced the dual-branch approach: freeze a video model, add a trainable geometric branch, and cross-supervise. The video model provides appearance priors while the geometry branch enforces 3D consistency. This "frozen backbone + geometric adapter" pattern recurred across later work.

**[Terra](https://arxiv.org/abs/2510.14977)** (Oct 2025) made the leap to **native 3D**: a Point-to-Gaussian VAE operating entirely in intrinsic 3D latent space rather than pixel-aligned representations. This was the cleanest separation of 3D structure from 2D rendering.

Two parallel approaches to scene scale emerged:

- **Block-based expansion**: [WorldGrow](https://arxiv.org/abs/2510.21682) (Oct 2025) used hierarchical 3D block inpainting — generate a block, then inpaint adjacent blocks with context — for infinite scene growth.
- **Training-free composition**: [TRELLISWorld](https://arxiv.org/abs/2510.23880) (Oct 2025) repurposed object-level diffusion models as tile generators, composing scenes without any scene-level training. [ChronosObserver](https://arxiv.org/abs/2512.01481) (Dec 2025) similarly achieved training-free 4D by synchronizing multi-view diffusion trajectories in a "hyperspace."

The game world subfield (HunyuanWorld, Matrix-3D) diverged toward **mesh export** for engine compatibility: semantically layered meshes, 360-degree panoramic proxies, decomposable objects. General 3D research prioritized Gaussian splatting and point clouds for novel view synthesis.

By Jan 2026, **[NeoVerse](https://arxiv.org/abs/2601.00393)** eliminated the multi-view capture requirement entirely — pose-free feed-forward 4D reconstruction from monocular in-the-wild video, opening access to internet-scale training data.

### View Progression

```
SINGLE-VIEW INPUT          MULTI-VIEW GENERATION        4D (SPACE+TIME)
       |                           |                          |
FantasyWorld (single)      ChronosObserver (sync)      SeeU (continuous)
WorldGrow (single)         Visionary (4DGS render)     DynamicVerse (dataset)
WonderZoom (single)        EvoWorld (loop-closure)     NeoVerse (monocular 4D)
Matrix-3D (single/text)                                Terra (4D latent)
```

Most papers accept single image/text input but generate multi-view consistent output. The field moved from "generate consistent views" to "model continuous spatiotemporal dynamics."

---

## The Physics Thread: From "They Can't" to "Steer at Inference"

This is the most intellectually interesting arc:

**Step 1 — Diagnosis** (Nov 2024): *["How Far is Video Generation from World Model"](https://arxiv.org/abs/2411.02385)* built a 2D physics testbed and discovered that video models exhibit **case-based** physical reasoning (memorized patterns) rather than **rule-based** (learned laws). Scaling alone doesn't fix this. Models generalize by color > size > velocity > shape — a damning finding.

**Step 2 — Training-time forcing** (Jul–Dec 2025): [Geometry Forcing](https://arxiv.org/abs/2507.07982) (Jul 2025) responded by explicitly aligning diffusion model features with geometric foundation model representations during training. [ProPhy](https://arxiv.org/abs/2512.05564) (Dec 2025) introduced Mixture-of-Physics-Experts with separate semantic and refinement experts for token-level physical dynamics.

**Step 3 — Uncertainty** (Dec 2025): *["World Models That Know When They Don't Know"](https://arxiv.org/abs/2512.05927)* argued that instead of forcing correct physics, models should report *calibrated uncertainty* at subpatch level — know when they are hallucinating.

**Step 4 — Inference-time alignment** (Jan 2026): [Inference-time Physics Alignment](https://arxiv.org/abs/2601.10553) used V-JEPA 2 as a **reward model** (WMReward) to search and steer denoising trajectories at test time. This won the ICCV 2025 PhysicsIQ Challenge. The insight: physics knowledge exists in latent world models — use it to guide generative models at inference, not training.

The progression mirrors RLHF in LLMs: train a base model, then align it with a reward signal. Here, the "reward model" is a physics-aware world model steering a video generator.

| Phase | Date | Paper | Approach |
|-------|------|-------|----------|
| Evaluation | Nov 2024 | [How Far...](https://arxiv.org/abs/2411.02385) | Physics testbed reveals case-based, not rule-based |
| Training-time | Jul 2025 | [Geometry Forcing](https://arxiv.org/abs/2507.07982) | Align features with geometric foundation models |
| Training-time | Dec 2025 | [ProPhy](https://arxiv.org/abs/2512.05564) | MoPE architecture + VLM-assisted alignment |
| Uncertainty | Dec 2025 | [C3](https://arxiv.org/abs/2512.05927) | Calibrated confidence at subpatch level |
| Inference-time | Jan 2026 | [WMReward](https://arxiv.org/abs/2601.10553) | Latent world model steers denoising trajectories |

---

## Cross-Pollination: The Architectural Imports

The field's rapid progress comes from importing innovations from adjacent areas:

| Source | Import | Destination |
|--------|--------|-------------|
| **LLMs** | Autoregressive next-token prediction, scaling laws, causal attention | Genie, Oasis, MineWorld, Matrix-Game |
| **DiT** (Peebles & Xie 2022) | Transformer backbone for diffusion, adaLN conditioning | Sora, Oasis, Matrix-Game, all DiT-based models |
| **VQ-VAE / MAGVIT** | Discrete visual tokenization, masked generative prediction | Genie (LAM), MineWorld, Emu3/3.5 |
| **3DGS / NeRF** | Real-time neural rendering, Gaussian primitives | Terra, Visionary, Marble, HunyuanWorld |
| **Mamba / SSMs** | Linear-complexity sequence modeling | Long-Context SSM World Models (hybrid SSM+attention) |
| **RingAttention** | Million-token context windows | LWM (1M token video-language sequences) |

One consequential import was **LLM-style autoregressive prediction applied to visual tokens**. Emu3.5 pushed this furthest: 10T+ tokens of unified vision-language training, then DiDA (Discrete Diffusion Adaptation) to convert sequential decoding to parallel prediction for ~20x speedup. This is the "language model beats diffusion" thesis applied to world modeling.

---

## The Convergence: Hybrid Architectures

The major lineages exposed a structural tension. Pure generative models (Sora/Genie) produce rich pixels but lack causal action control and accumulate errors over long horizons. JEPA-style objectives (V-JEPA) are efficient and transferable but prone to **representation collapse** — mapping all observations to constant vectors — because no generative decoder enforces meaningful distinctions. The next wave of models attempted to synthesize both sides.

**[PAN](https://arxiv.org/abs/2511.09057)** (MBZUAI, Nov 2025) proposed the cleanest separation: **Generative Latent Prediction (GLP)** uses an LLM dynamics backbone (Qwen2.5-VL-7B) to predict latent world states autoregressively conditioned on natural language actions, while a diffusion decoder (Wan2.1-T2V-14B) renders those states into video via Causal Swin-DPM. The LLM reasons about *what happens next* in abstract space (avoiding pixel hallucination); the decoder ensures latent representations stay meaningful (avoiding JEPA collapse).

**[GWM-1](https://runwayml.com/research/introducing-runway-gwm-1)** (Runway, Dec 2025) took a different path to the same goal: post-train an existing video generator (Gen-4.5) into an autoregressive frame-by-frame model with cross-domain action conditioning (camera, events, poses, speech). Where PAN separates dynamics and rendering architecturally, GWM-1 unifies them in a single model with domain-specific post-training variants (Worlds, Avatars, Robotics).

**[LingBot-World](https://arxiv.org/abs/2601.20540)** (Robbyant, Jan 2026) marked an open-source milestone: a 28B MoE-DiT (extending Wan2.2) with block causal attention for KV-cached streaming at 16 FPS and sub-1s latency. Up to 10 minutes of stable generation with text-based environmental control — the first fully open-source model matching closed-source SOTA.

These three models represent distinct strategies for the same destination — long-horizon, action-conditioned, general-purpose world simulation — via architectural separation (PAN), unified post-training (GWM-1), or open-source scale (LingBot-World).

---

## How It All Connects

```
                    WORLD MODEL EVOLUTION (2018 → 2026)


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  FOUNDATIONS (2018–2022)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Philosophies                         Enabling Techniques
  ────────────                         ────────────────────
  Ha & Schmidhuber (2018)              DiT (2022)
  │  Dream inside learned models       ViT replaces U-Net for diffusion
  │
  ├──→ PlaNet (2019)                   VQ-VAE / MAGVIT
  │    RSSM latent dynamics            Discrete visual tokenization
  │
  └──→ Dreamer V1 → V2 → V3           3DGS / NeRF
       Latent imagination RL           Neural 3D rendering

  LeCun (2022)
  │  Predict in representation space
  └──→ I-JEPA (2023)


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  FEBRUARY 2024: THE BIG BANG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Sora ←── DiT          Genie ←── VQ-VAE       V-JEPA ←── JEPA
  Spacetime patches      Latent actions          Non-generative
  "World simulator"      from unlabeled          Spatiotemporal
   framing               video                   masking


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LINEAGES (2024–2026)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Genie Line             JEPA Line            Game Simulation
  ──────────             ─────────            ───────────────
  Genie (Feb 24)         V-JEPA (Feb 24)      DIAMOND (May 24) ──┐
       ↓                      ↓               GameNGen (Aug 24) ──┤
  Genie 2 (Dec 24)       V-JEPA 2 (Jun 25)                       ↓
  3D, emergent NPCs      Action-conditioned   Oasis (Oct 24)
       ↓                 Zero-shot planning        ↓
  Genie 3 (Aug 25)                            Matrix-Game (Jun 25)
  Real-time 24fps                                  ↓
                                              MG 2.0 (Aug 25)
                                                   ↓
                                              Solaris (Feb 26)
                                              Multiplayer

  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─

  3D Generation          Platform             Training Paradigms
  (← 3DGS / NeRF)       ────────             (orthogonal techniques)
  ─────────────                               ──────────────────
  Terra, Marble          Cosmos (Jan 25)      Diffusion Forcing
  HunyuanWorld                ↓                    ↓
  Visionary              Cosmos-Predict2.5    Self-Forcing
                         (Oct 25)                  ↓
                                              Checkpointed SF
                                              (→ used by Solaris)


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  CONVERGENCE (emerging thesis)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  PAN            — LLM dynamics + diffusion decoder
  GWM-1          — unified post-training
  LingBot-World  — open-source 28B MoE

```

The field converges toward: **real-time, action-conditioned, physically-aware, multi-agent world simulators** — built by combining LLM-scale autoregressive transformers, diffusion rendering, 3D Gaussian representations, self-forcing training, and inference-time physics alignment.

The generative path ([Genie](https://arxiv.org/abs/2402.15391)/[Sora](https://openai.com/research/video-generation-models-as-world-simulators)/[Cosmos](https://arxiv.org/abs/2501.03575)) and the latent-predictive path ([V-JEPA](https://github.com/facebookresearch/jepa)) are no longer separate tracks. The convergence layer — [PAN](https://arxiv.org/abs/2511.09057)'s architectural separation, [GWM-1](https://runwayml.com/research/introducing-runway-gwm-1)'s unified post-training, [LingBot-World](https://arxiv.org/abs/2601.20540)'s open-source scale — shows the field moving toward hybrid designs that combine the strengths of both traditions.

---

*Analysis based on papers catalogued in [Awesome World Models for Video, Games & 3D](README.md).*
