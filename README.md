<div align="center">

# Awesome World Models for Video, Games & 3D

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/gxchris95/awesome-world-models-video-games-3d/pulls)
[![License](https://img.shields.io/badge/License-CC0_1.0-blue.svg)](LICENSE)

**A curated list of world models for video generation, interactive simulation, and 3D world creation.**

From video synthesis to playable game worlds to explorable 3D environments.

</div>

---

## Table of Contents

- [What Are World Models?](#what-are-world-models)
- [Surveys](#surveys)
- [Foundation World Models](#foundation-world-models)
- [World Models for Video Generation](#world-models-for-video-generation)
  - [General Video World Models](#general-video-world-models)
  - [Interactive Video Generation](#interactive-video-generation)
  - [Long-form & Controllable Video](#long-form--controllable-video)
  - [Physics-Aware Video Generation](#physics-aware-video-generation)
- [World Models for Game Simulation](#world-models-for-game-simulation)
  - [Pixel-Space Game Models](#pixel-space-game-models)
  - [3D Game Worlds](#3d-game-worlds)
- [World Models for 3D World Generation](#world-models-for-3d-world-generation)
- [World Models for Creative & Entertainment Applications](#world-models-for-creative--entertainment-applications)
- [Key Approaches & Architectures](#key-approaches--architectures)
  - [Generation Paradigm](#generation-paradigm)
  - [Conditioning & Control](#conditioning--control)
  - [Temporal Consistency & Memory](#temporal-consistency--memory)
  - [3D Representation](#3d-representation)
- [Benchmarks & Evaluation](#benchmarks--evaluation)
- [Theory, Positions & Explainability](#theory-positions--explainability)
  - [Theory](#theory)
  - [Positions](#positions)
  - [Explainability](#explainability)
- [Key Blog Posts & Technical Reports](#key-blog-posts--technical-reports)
- [Contributing](#contributing)
- [Citation](#citation)

---

## What Are World Models?

A **world model** is an AI system that learns to simulate how the world works, capturing physics, dynamics, and cause-and-effect — to predict what happens next given an action or input. Two foundational works define the field:

- **World Models** (Ha & Schmidhuber, 2018) — Train agents inside learned environment simulators (VAE + RNN + controller). [[Paper](https://arxiv.org/abs/1803.10122)] [[Website](https://worldmodels.github.io/)]
- **A Path Towards Autonomous Machine Intelligence** (LeCun, 2022) — Proposed JEPA: world models that predict in latent space, not pixel space. [[Paper](https://openreview.net/pdf?id=BZ5a1r-kVsf)]

For video generation and interactive simulation, world models go beyond passive synthesis — they learn to produce physically plausible environments that respond to user actions in real time.

> **New to the field?** Read [The Evolution of World Models for Media](EVOLUTION.md), a deep analysis of how methods build upon each other — from Ha & Schmidhuber (2018) to real-time multiplayer world simulation (2026).

---

## Surveys

- **Is Sora a World Simulator? A Comprehensive Survey on General World Models and Beyond** (May 2024) — Comprehensive taxonomy of world models across video, driving, and agents toward AGI. [[Paper](https://arxiv.org/abs/2405.03520)] [[Code](https://github.com/GigaAI-research/General-World-Models-Survey)]
- **From Efficient Multimodal Models to World Models: A Survey** (Jul 2024) — Charts evolution from multimodal large models toward world models via 3D generation and embodied intelligence. [[Paper](https://arxiv.org/abs/2407.00118)]
- **Understanding World or Predicting Future? A Comprehensive Survey of World Models** (Nov 2024) — Distinguishes world models by dual functions: understanding mechanisms versus predicting future states. [[Paper](https://arxiv.org/abs/2411.14499)] [[Code](https://github.com/tsinghua-fib-lab/World-Model)]
- **Four Principles for Physically Interpretable World Models** (Mar 2025) — Proposes four principles for world models with verifiable, physically grounded latent representations. [[Paper](https://arxiv.org/abs/2503.02143)]
- **World Models in Artificial Intelligence: Sensing, Learning, and Reasoning Like a Child** (Mar 2025) — Advocates child-like cognitive development integrating six research areas for genuine AI reasoning. [[Paper](https://arxiv.org/abs/2503.15168)]
- **Exploring the Evolution of Physics Cognition in Video Generation: A Survey** (Mar 2025) — Three-tier taxonomy of video generation's evolution from visual mimicry to physical comprehension. [[Paper](https://arxiv.org/abs/2503.21765)] [[Code](https://github.com/minnie-lin/Awesome-Physics-Cognition-based-Video-Generation)]
- **3D and 4D World Modeling: A Survey** (Sep 2025) — First comprehensive review dedicated to 3D/4D world modeling with standardized taxonomy and datasets. [[Paper](https://arxiv.org/abs/2509.07996)] [[Code](https://github.com/worldbench/survey)]
- **From Masks to Worlds: A Hitchhiker's Guide to World Models** (Oct 2025) — Traces the developmental path from masked learning through unified architectures to interactive generation. [[Paper](https://arxiv.org/abs/2510.20668)]
- **Simulating the Visual World with Artificial Intelligence: A Roadmap** (Nov 2025) — Conceptualizes video models as implicit world simulators plus renderers across four technology generations. [[Paper](https://arxiv.org/abs/2511.08585)] [[Website](https://world-model-roadmap.github.io/)]
- **A Mechanistic View on Video Generation as World Models: State and Dynamics** (Jan 2026) — Disentangles state construction from dynamics modeling; advocates functional benchmarks over visual quality. [[Paper](https://arxiv.org/abs/2601.17067)]
- **The Trinity of Consistency as a Defining Principle for General World Models** (Feb 2026) — Unified modal-spatial-temporal consistency framework with CoW-Bench evaluation protocol. [[Paper](https://arxiv.org/abs/2602.23152)]

---

## Foundation World Models

Large-scale, general-purpose world models that serve as platforms for multiple downstream applications.

- **Sora** (OpenAI, Feb 2024) — **Spacetime patches** in a Diffusion Transformer (DiT); emergent 3D consistency and physics from text-to-video at scale. [[Technical Report](https://openai.com/research/video-generation-models-as-world-simulators)]
- **Genie** (DeepMind, Feb 2024) — **Learns action control from unlabeled video**; 11B-param model discovers latent actions without any action annotations. [[Paper](https://arxiv.org/abs/2402.15391)] [[Blog](https://sites.google.com/view/genie-2024/home)]
- **V-JEPA** (Meta, Feb 2024) — **Non-generative** JEPA; predicts masked video in latent space (not pixels), 1.5-6x training efficiency with frozen encoder transfer. [[Blog](https://ai.meta.com/blog/v-jepa-yann-lecun-ai-model-video-joint-embedding-predictive-architecture/)] [[Code](https://github.com/facebookresearch/jepa)]
- **Genie 2** (DeepMind, Dec 2024) — **Autoregressive latent diffusion** for 3D worlds from a single image; minute-long consistency with emergent NPC behavior. [[Blog](https://deepmind.google/discover/blog/genie-2-a-large-scale-foundation-world-model/)]
- **Cosmos** (NVIDIA, Jan 2025) — **Open-source platform** (4B-14B params); full pipeline with tokenizers, pre-trained models, permissive license. [[Paper](https://arxiv.org/abs/2501.03575)] [[Website](https://www.nvidia.com/en-us/ai/cosmos/)] [[Code](https://github.com/NVIDIA/Cosmos)]
- **V-JEPA 2** (Meta, Jun 2025) — **1M+ hours pre-training, <62 hours fine-tuning** for zero-shot robotic planning; 16x faster than video-generation-based planners. [[Paper](https://arxiv.org/abs/2506.09985)] [[Website](https://ai.meta.com/blog/v-jepa-2-world-model-benchmarks/)] [[Code](https://github.com/facebookresearch/vjepa2)]
- **Genie 3** (DeepMind, Aug 2025) — First **real-time interactive** world model (24fps, 720p); promptable world events via text during live play. [[Blog](https://deepmind.google/discover/blog/genie-3-a-new-frontier-for-world-models/)]
- **Emu3.5** (BAAI, Oct 2025) — **Discrete Diffusion Adaptation (DiDA)** converts autoregressive decoding to parallel prediction for ~20x speedup; 10T+ token training. [[Paper](https://arxiv.org/abs/2510.26583)] [[Website](https://emu.world)] [[Code](https://github.com/baaivision/Emu3.5)]
- **RTFM** (World Labs, Oct 2025) — **Learned renderer** with spatial memory and context juggling for unbounded persistence; single H100. [[Blog](https://www.worldlabs.ai/blog/rtfm)]
- **Cosmos-Predict2.5** (NVIDIA, Oct 2025) — **Unified flow architecture** for Text/Image/Video2World in one model; RL-based post-training on 200M clips. [[Paper](https://arxiv.org/abs/2511.00062)] [[Code](https://github.com/nvidia-cosmos/cosmos-predict2.5)]
- **PAN** (MBZUAI, Nov 2025) — **Generative Latent Prediction**: LLM dynamics backbone + diffusion decoder; text-grounded open-domain long-horizon simulation. [[Paper](https://arxiv.org/abs/2511.09057)] [[Website](https://panworld.ai/)]
- **Marble** (World Labs, Nov 2025) — **Chisel** decouples 3D structure from style; multimodal input to exportable Gaussian splats, meshes, or video. [[Blog](https://www.worldlabs.ai/blog/bigger-better-worlds)]
- **GWM-1** (Runway, Dec 2025) — **Cross-domain action conditioning** (camera, events, poses, speech); three variants: worlds, avatars, robotics. [[Blog](https://runwayml.com/research/introducing-runway-gwm-1)]
- **LingBot-World** (Robbyant, Jan 2026) — **Sub-1s latency, 10-min stable generation**; 28B open-source model, internet video + Unreal Engine data. [[Paper](https://arxiv.org/abs/2601.20540)] [[Website](https://technology.robbyant.com/lingbot-world)] [[Code](https://github.com/Robbyant/lingbot-world)]

---

## World Models for Video Generation

### General Video World Models

- **WorldDreamer** (Jan 2024) — **Masked visual token prediction** for multi-domain world modeling; jointly models appearance and dynamics without domain-specific design. [[Paper](https://arxiv.org/abs/2401.09985)] [[Code](https://github.com/JeffWang987/WorldDreamer)]
- **LWM** (Feb 2024) — **RingAttention** scales context from 4K to 1M tokens; enables coherent world modeling over million-length video-language sequences. [[Paper](https://arxiv.org/abs/2402.08268)] [[Code](https://github.com/LargeWorldModel/LWM)]
- **Pandora** (Jun 2024) — **Hybrid LLM (7B) + video model**; fuses pretrained language model with video generator for text-action controlled simulation. [[Paper](https://arxiv.org/abs/2406.09455)] [[Code](https://github.com/maitrix-org/Pandora)]
- **Owl-1** (Dec 2024) — **Latent state variable decoding**; prevents long-term inconsistency accumulation by decoding observations from abstract state representations. [[Paper](https://arxiv.org/abs/2412.09600)]
- **Aether** (Mar 2025) — **Unified task-interleaved learning** combining 4D reconstruction, prediction, and geometry-informed planning in one model. [[Paper](https://arxiv.org/abs/2503.18945)] [[Website](https://aether-world.github.io/)]
- **DeepVerse** (Jun 2025) — **Explicit geometric predictions** from previous timesteps incorporated into action-conditioned 4D video generation. [[Paper](https://arxiv.org/abs/2506.01103)]
- **UnityVideo** (Dec 2025) — **Dynamic noising + modality switcher** unifies heterogeneous modalities for cross-modal world-aware video generation. [[Paper](https://arxiv.org/abs/2512.07831)] [[Website](https://jackailab.github.io/Projects/UnityVideo)] [[Code](https://github.com/dvlab-research/UnityVideo)]
- **NuiWorld** (Jan 2026) — **Generative bootstrapping** synthesizes training data; compresses variable scene chunks to flattened vectors for scalable generation. [[Paper](https://arxiv.org/abs/2601.19048)]
- **Olaf-World** (Feb 2026) — **Seq-delta-REPA** aligns latent actions to temporal semantic effects for cross-context transferability. [[Paper](https://arxiv.org/abs/2602.10104)] [[Website](https://showlab.github.io/Olaf-World/)] [[Code](https://github.com/showlab/Olaf-World)]

### Interactive Video Generation

- **iVideoGPT** (May 2024) — **Compressive tokenization** discretizes high-dimensional observations for scalable GPT-style interactive world modeling. [[Paper](https://arxiv.org/abs/2405.15223)] [[Website](https://thuml.github.io/iVideoGPT/)] [[Code](https://github.com/thuml/iVideoGPT)]
- **AdaWorld** (HKUST/Harvard, Mar 2025) — **Self-supervised latent action extraction** from video enables zero-shot action transfer across unseen environments. [[Paper](https://arxiv.org/abs/2503.18938)] [[Website](https://adaptable-world-model.github.io/)] [[Code](https://github.com/Little-Podi/AdaWorld)]
- **Vid2World** (May 2025) — **Causalizes pretrained video diffusion** models by reshaping architecture and training objectives into interactive simulators. [[Paper](https://arxiv.org/abs/2505.14357)] [[Website](http://knightnemo.github.io/vid2world/)]
- **VRAG** (May 2025) — **Video retrieval augmented generation** with explicit global state conditioning reduces long-term compounding errors. [[Paper](https://openreview.net/forum?id=FzfYoUp8F1)]
- **Astra** (Dec 2025) — **Noise-augmented history memory** balances responsiveness with temporal coherence in streaming autoregressive denoising. [[Paper](https://arxiv.org/abs/2512.08931)] [[Website](https://eternalevan.github.io/Astra-project/)] [[Code](https://github.com/EternalEvan/Astra)]
- **RELIC** (Adobe, Dec 2025) — **Camera-aware compressed latent tokens** in KV cache enable real-time 16 FPS long-horizon interactive generation. [[Paper](https://arxiv.org/abs/2512.04040)] [[Website](https://relic-worldmodel.github.io/)]
- **LIVE** (Feb 2026) — **Cycle-consistency** with forward-backward generation eliminates need for teacher distillation in long-horizon interaction. [[Paper](https://arxiv.org/abs/2602.03747)] [[Website](https://junchao-cs.github.io/LIVE-demo/)]
- **Generated Reality** (Stanford, Feb 2026) — Conditions on **tracked 3D head pose + joint-level hand poses** for dexterous egocentric world simulation. [[Paper](https://arxiv.org/abs/2602.18422)]

### Long-form & Controllable Video

- **GEN3C** (NVIDIA, Mar 2025) — **3D cache** conditions video diffusion on 2D renderings for precise camera control and multi-view consistency. `CVPR 2025` [[Paper](https://openaccess.thecvf.com/content/CVPR2025/papers/Ren_GEN3C_3D-Informed_World-Consistent_Video_Generation_with_Precise_Camera_Control_CVPR_2025_paper.pdf)]
- **FAR** (NUS, Mar 2025) — **Asymmetric patchify kernels** apply large kernels to distant frames for efficient long-context autoregressive video. [[Paper](https://arxiv.org/abs/2503.19325)] [[Code](https://github.com/showlab/FAR)] [[Website](https://farlongctx.github.io/)]
- **Long-Context SSM World Models** (Stanford/Adobe, May 2025) — **Hybrid SSM + local attention**; block-wise scanning trades spatial detail for extended temporal memory at constant cost. [[Paper](https://arxiv.org/abs/2505.20171)] [[Website](https://ryanpo.com/ssm_wm)]
- **Yume** (Shanghai AI Lab, Jul 2025) — **Masked Video Diffusion Transformer** with memory enables infinite autoregressive world generation. [[Paper](https://arxiv.org/abs/2507.17744)] [[Website](https://stdstu12.github.io/YUME-Project/)] [[Code](https://github.com/stdstu12/YUME)]
- **LongVie 2** (Dec 2025) — **Three-stage training** with degradation-aware bridging and history-context guidance for 5-minute controllable video. [[Paper](https://arxiv.org/abs/2512.13604)] [[Website](https://vchitect.github.io/LongVie2-project/)]
- **Yume-1.5** (Shanghai AI Lab, Dec 2025) — **Unified context compression** via linear attention + bidirectional distillation for real-time streaming interaction. [[Paper](https://arxiv.org/abs/2512.22096)] [[Website](https://stdstu12.github.io/YUME-Project)] [[Code](https://github.com/stdstu12/YUME)]
- **VerseCrafter** (Jan 2026) — **4D geometric control** via static point cloud background + per-object 3D Gaussian trajectories. [[Paper](https://arxiv.org/abs/2601.05138)] [[Website](https://sixiaozheng.github.io/VerseCrafter_page/)]

### Physics-Aware Video Generation

- **How Far is Video Generation from World Model** (ByteDance, Nov 2024) — **2D simulation testbed** reveals models exhibit case-based rather than rule-based physical reasoning. `ICML 2025` [[Paper](https://arxiv.org/abs/2411.02385)] [[Website](https://phyworld.github.io/)] [[Code](https://github.com/phyworld/phyworld)]
- **Geometry Forcing** (Microsoft, Jul 2025) — **Angular and scale alignment** guide video diffusion models to internalize latent 3D geometric representations. `ICLR 2026` [[Paper](https://arxiv.org/abs/2507.07982)] [[Website](https://GeometryForcing.github.io)]
- **ProPhy** (Dec 2025) — **Mixture of semantic + refinement physics experts** progressively align token-level physical dynamics during generation. [[Paper](https://arxiv.org/abs/2512.05564)]
- **World Models That Know When They Don't Know** (Princeton, Dec 2025) — **C3 framework** for continuous-scale calibrated uncertainty at subpatch-level localization. [[Paper](https://arxiv.org/abs/2512.05927)]
- **Inference-time Physics Alignment** (Meta FAIR, Jan 2026) — **WMReward** uses V-JEPA 2 as reward model for inference-time denoising trajectory search. [[Paper](https://arxiv.org/abs/2601.10553)]

---

## World Models for Game Simulation

### Pixel-Space Game Models

- **DIAMOND** (May 2024) — **Diffusion replaces discrete latents** for world modeling; preserves visual details that matter for RL, SoTA on Atari. [[Paper](https://arxiv.org/abs/2405.12399)] [[Code](https://github.com/eloialonso/diamond)]
- **GameNGen** (Google, Aug 2024) — First **neural game engine**; autoregressive diffusion with conditioning augmentation runs DOOM at interactive frame rates. [[Paper](https://arxiv.org/abs/2408.14837)]
- **Oasis** (Decart/Etched, Oct 2024) — **Dynamic noising schedule** during inference reduces error accumulation; transformer-based real-time Minecraft-style generation. [[Website](https://oasis-model.github.io/)]
- **GameFactory** (Kuaishou, Jan 2025) — **Domain adapter** decouples game style from action control for scene-generalizable novel game creation. [[Paper](https://arxiv.org/abs/2501.08325)] [[Website](https://yujiwen.github.io/gamefactory/)] [[Code](https://github.com/KwaiVGI/GameFactory)]
- **AnimeGamer** (Tencent, Apr 2025) — **MLLM generates game states** with action-aware multimodal representations for infinite anime life simulation. [[Paper](https://arxiv.org/abs/2504.01014)] [[Website](https://howe125.github.io/AnimeGamer.github.io/)]
- **MineWorld** (Microsoft, Apr 2025) — **Parallel decoding** predicts spatially redundant tokens simultaneously for 4-7 FPS real-time Minecraft simulation. [[Paper](https://arxiv.org/abs/2504.08388)] [[Website](https://aka.ms/mineworld)]
- **WORLDMEM** (Apr 2025) — **Memory bank with attention** maintains long-term 3D spatial consistency across viewpoint changes in game sessions. [[Paper](https://arxiv.org/abs/2504.12369)] [[Website](https://xizaoqu.github.io/worldmem/)] [[Code](https://github.com/xizaoqu/WorldMem)]
- **Matrix-Game** (Skywork, Jun 2025) — **Two-stage pipeline**: unlabeled pretraining for environment understanding, then action-labeled training for control. [[Paper](https://arxiv.org/abs/2506.18701)] [[Code](https://github.com/SkyworkAI/Matrix-Game)]
- **RealPlay** (Jun 2025) — **Iterative chunk-wise prediction** enables transfer from virtual game controls to photorealistic real-world scenarios. [[Paper](https://arxiv.org/abs/2506.18901)] [[Website](https://wenqsun.github.io/RealPlay/)] [[Code](https://github.com/wenqsun/Real-Play)]
- **Matrix-Game 2.0** (Skywork, Aug 2025) — **Few-step causal diffusion + action injection** enables streaming 25 FPS interactive generation. [[Paper](https://arxiv.org/abs/2508.13009)] [[Website](https://matrix-game-v2.github.io/)]
- **Hunyuan-GameCraft-2** (Tencent, Nov 2025) — **Text-driven interaction injection** enables natural language control instead of fixed keyboard/mouse inputs. [[Paper](https://arxiv.org/abs/2511.23429)] [[Website](https://hunyuan-gamecraft-2.github.io/)]
- **Captain Safari** (Nov 2025) — **Pose-conditioned retriever** fetches pose-aligned world tokens from persistent memory for open-ended exploration. [[Paper](https://arxiv.org/abs/2511.22815)] [[Website](https://johnson111788.github.io/open-safari/)]
- **SIMA 2** (DeepMind, Dec 2025) — **Autonomous self-improvement** through task/reward generation from foundation model; conversational generalist game agent. [[Paper](https://arxiv.org/abs/2512.04797)]
- **Waypoint-1** (Overworld, Jan 2026) — **Self-forcing** trained from scratch on 10K hours gameplay for real-time interactive world generation. [[Blog](https://over.world/blog/the-path-to-real-time-worlds-and-why-it-matters)]
- **Solaris** (Feb 2026) — First **multiplayer world model**; synchronized capture with Checkpointed Self Forcing for multi-agent view consistency in Minecraft. [[Paper](https://arxiv.org/abs/2602.22208)] [[Website](https://solaris-wm.github.io/)]

### 3D Game Worlds

- **HunyuanWorld 1.0** (Tencent, Jul 2025) — **Semantically layered 3D mesh** with 360-degree panoramic proxies for immersive, decomposable world generation. [[Paper](https://arxiv.org/abs/2507.21809)] [[Website](https://3d-models.hunyuan.tencent.com/world/)] [[Code](https://github.com/Tencent-Hunyuan/HunyuanWorld-1.0)]
- **Matrix-3D** (Aug 2025) — **Trajectory-guided panoramic video diffusion** conditioned on scene mesh renders for 360-degree geometric consistency. [[Paper](https://arxiv.org/abs/2508.08086)] [[Website](https://matrix-3d.github.io)]
- **WorldGen** (Meta, Nov 2025) — **LLM-driven procedural planning** with navmesh-conditioned reconstruction for traversable compositional 3D scenes. [[Blog](https://www.meta.com/blog/worldgen-3d-world-generation-reality-labs-generative-ai-research)]

---

## World Models for 3D World Generation

- **FantasyWorld** (Alibaba, Sep 2025) — **Frozen video model + trainable geometric branch** with cross-branch supervision for geometry-consistent world modeling. [[Paper](https://arxiv.org/abs/2509.21657)]
- **EvoWorld** (JHU, Oct 2025) — **Evolving explicit 3D memory** guides video generation through geometric reprojections for panoramic consistency. [[Paper](https://arxiv.org/abs/2510.01183)] [[Code](https://github.com/JiahaoPlus/EvoWorld)]
- **Terra** (Tsinghua/Kuaishou, Oct 2025) — **Point-to-Gaussian VAE** operates in intrinsic 3D latent space for native geometric consistency. [[Paper](https://arxiv.org/abs/2510.14977)] [[Website](https://huang-yh.github.io/terra/)]
- **WorldGrow** (Oct 2025) — **Hierarchical 3D block inpainting** with coarse-to-fine strategy for infinite scene expansion. [[Paper](https://arxiv.org/abs/2510.21682)] [[Code](https://github.com/world-grow/WorldGrow)]
- **TRELLISWorld** (CMU/HKUST, Oct 2025) — **Training-free multi-tile denoising** repurposes object diffusion models for scalable scene generation. [[Paper](https://arxiv.org/abs/2510.23880)]
- **MagicWorld** (NUS/Zhejiang, Nov 2025) — **Action-guided 3D geometry module** constructs point clouds for viewpoint-stable video exploration. [[Paper](https://arxiv.org/abs/2511.18886)]
- **ChronosObserver** (Beihang, Dec 2025) — **Training-free hyperspace** synchronizes multi-view diffusion sampling trajectories for 4D consistency. [[Paper](https://arxiv.org/abs/2512.01481)]
- **DynamicVerse** (Xiamen/Meta, Dec 2025) — **Window-based bundle adjustment** with global optimization for metric-scale 4D annotations. [[Paper](https://arxiv.org/abs/2512.03000)]
- **SeeU** (Purdue/Samsung, Dec 2025) — **2D→4D→2D framework** reconstructs continuous spatiotemporal dynamics from single views. [[Paper](https://arxiv.org/abs/2512.03350)] [[Website](https://yuyuanspace.com/SeeU/)]
- **Visionary** (Shanghai AI Lab, Dec 2025) — **WebGPU platform** unifies ONNX inference and 3DGS rendering per-frame for browser-based world interaction. [[Paper](https://arxiv.org/abs/2512.08478)] [[Website](https://visionary-laboratory.github.io/visionary)]
- **WonderZoom** (Stanford, Dec 2025) — **Scale-adaptive Gaussian surfels** enable multi-scale zoom with progressive detail synthesis. [[Paper](https://arxiv.org/abs/2512.09164)] [[Website](https://wonderzoom.github.io/)]
- **WorldPlay** (HKUST/Tencent, Dec 2025) — **Reconstituted context memory** dynamically rebuilds past frames with temporal reframing for geometric consistency. [[Paper](https://arxiv.org/abs/2512.14614)]
- **TeleWorld** (TeleAI, Dec 2025) — **Generation-reconstruction-guidance paradigm** with dynamic 4D representation for real-time multimodal interaction. [[Paper](https://arxiv.org/abs/2601.00051)]
- **NeoVerse** (CAS/CreateAI, Jan 2026) — **Pose-free feed-forward 4D reconstruction** with online monocular degradation simulation from in-the-wild video. [[Paper](https://arxiv.org/abs/2601.00393)] [[Website](https://neoverse-4d.github.io)]

---

## World Models for Creative & Entertainment Applications

- **Martian World Models** (NVIDIA/UT Austin, Jul 2025) — **Metric-accurate 3D reconstruction** from NASA stereo nav images for controllable Mars terrain synthesis. [[Paper](https://arxiv.org/abs/2507.07978)] [[Website](https://marsgenai.github.io)]
- **LatticeWorld** (NetEase/Beihang, Sep 2025) — **LLM-generated symbolic layouts** rendered in Unreal Engine 5 for 90x faster interactive multi-agent world production. [[Paper](https://arxiv.org/abs/2509.05263)]
- **ChronoEdit** (NVIDIA, Oct 2025) — **Temporal reasoning tokens** treat image editing as video generation; tokens dropped after denoising for efficiency. [[Paper](https://arxiv.org/abs/2510.04290)] [[Website](https://research.nvidia.com/labs/toronto-ai/chronoedit)]
- **MorphoSim** (UCSC/UCLA, Oct 2025) — **Feature field distillation** enables object-level 4D editing without full scene regeneration. [[Paper](https://arxiv.org/abs/2510.04390)] [[Code](https://github.com/eric-ai-lab/Morph4D)]
- **Inferix** (Alibaba/HKUST, Nov 2025) — **Semi-autoregressive block diffusion** with LLM-style KV cache for efficient variable-length video generation. [[Paper](https://arxiv.org/abs/2511.20714)] [[Code](https://github.com/alibaba-damo-academy/Inferix)]
- **WorldWander** (NUS, Nov 2025) — **Collaborative position encoding** with in-context perspective alignment for egocentric-exocentric video translation. [[Paper](https://arxiv.org/abs/2511.22098)] [[Code](https://github.com/showlab/WorldWander)]
- **AVWM** (Tsinghua, Dec 2025) — **Modality-expert diffusion transformer** for synchronized audio-visual generation with binaural spatial cues. [[Paper](https://arxiv.org/abs/2512.00883)]
- **WorldPack** (UTokyo/DeepMind, Dec 2025) — **Hierarchical trajectory packing** compresses long-horizon memory for spatial consistency in world modeling. [[Paper](https://arxiv.org/abs/2512.02473)]
- **IC-World** (NTU/Tencent, Dec 2025) — **GRPO-based geometry rewards** enforce multi-view consistency in in-context shared world generation. [[Paper](https://arxiv.org/abs/2512.02793)] [[Code](https://github.com/wufan-cse/IC-World)]
- **Choreographing a World of Dynamic Objects** (Stanford, Jan 2026) — **Rectified flow SDS** with hierarchical Lagrangian deformations for category-agnostic 4D motion synthesis. [[Paper](https://arxiv.org/abs/2601.04194)] [[Website](https://yanzhelyu.github.io/chord)]

---

## Key Approaches & Architectures

### Generation Paradigm

How the model produces world states frame by frame.

| Paradigm | How It Works | Strengths | Limitations | Representative Works |
| --- | --- | --- | --- | --- |
| **Autoregressive (Token)** | Predict next visual token sequentially via transformer | Scalable; leverages LLM-era infrastructure | Compounding error over long horizons | [Genie](https://arxiv.org/abs/2402.15391), [Oasis](https://oasis-model.github.io/), [Matrix-Game](https://arxiv.org/abs/2506.18701) |
| **Autoregressive (Diffusion)** | Denoise each frame conditioned on previous frames causally | High visual fidelity per frame | Slower inference per step | [GameNGen](https://arxiv.org/abs/2408.14837), [DIAMOND](https://arxiv.org/abs/2405.12399), [Astra](https://arxiv.org/abs/2512.08931) |
| **Flow-based** | Unified flow matching for continuous generation | Single model handles multiple input modalities | Training complexity | [Cosmos-Predict2.5](https://arxiv.org/abs/2511.00062) |
| **Latent Prediction (JEPA)** | Predict in abstract representation space, not pixels | Sample-efficient; avoids pixel-level hallucination | Cannot directly render output | [V-JEPA](https://github.com/facebookresearch/jepa), [V-JEPA 2](https://arxiv.org/abs/2506.09985), [AdaWorld](https://arxiv.org/abs/2503.18938) |
| **Hybrid (LLM + Diffusion)** | LLM reasons about dynamics in latent space; diffusion renders | Combines semantic reasoning with visual quality | Two-stage inference overhead | [PAN](https://arxiv.org/abs/2511.09057), [Pandora](https://arxiv.org/abs/2406.09455) |

### Conditioning & Control

How users interact with and steer the generated world.

| Method | Mechanism | Representative Works |
| --- | --- | --- |
| **Latent action discovery** | Learn action spaces from unlabeled video; no annotations needed | [Genie](https://arxiv.org/abs/2402.15391), [AdaWorld](https://arxiv.org/abs/2503.18938), [Olaf-World](https://arxiv.org/abs/2602.10104) |
| **Keyboard/mouse action injection** | Condition on explicit discrete inputs per frame | [GameNGen](https://arxiv.org/abs/2408.14837), [Oasis](https://oasis-model.github.io/), [Matrix-Game 2.0](https://arxiv.org/abs/2508.13009) |
| **Natural language control** | Text instructions drive world dynamics and events | [Genie 3](https://deepmind.google/discover/blog/genie-3-a-new-frontier-for-world-models/), [Hunyuan-GameCraft-2](https://arxiv.org/abs/2511.23429), [Yume-1.5](https://arxiv.org/abs/2512.22096) |
| **Camera/pose conditioning** | 3D camera trajectories or body pose control viewpoint | [GEN3C](https://openaccess.thecvf.com/content/CVPR2025/papers/Ren_GEN3C_3D-Informed_World-Consistent_Video_Generation_with_Precise_Camera_Control_CVPR_2025_paper.pdf), [Generated Reality](https://arxiv.org/abs/2602.18422), [Captain Safari](https://arxiv.org/abs/2511.22815) |
| **Cross-domain action conditioning** | Unified interface across camera, events, poses, speech | [GWM-1](https://runwayml.com/research/introducing-runway-gwm-1) |

### Temporal Consistency & Memory

How models maintain coherence over extended generation.

| Strategy | How It Works | Representative Works |
| --- | --- | --- |
| **Spatial memory bank** | Store and retrieve world tokens indexed by 3D position | [WORLDMEM](https://arxiv.org/abs/2504.12369), [RELIC](https://arxiv.org/abs/2512.04040), [Captain Safari](https://arxiv.org/abs/2511.22815) |
| **KV cache compression** | Compress history into latent tokens in the attention cache | [RELIC](https://arxiv.org/abs/2512.04040), [Yume-1.5](https://arxiv.org/abs/2512.22096) |
| **Context juggling** | Dynamically select relevant past frames from spatial memory | [RTFM](https://www.worldlabs.ai/blog/rtfm) |
| **Reconstituted context** | Rebuild past frames with temporal reframing on the fly | [WorldPlay](https://arxiv.org/abs/2512.14614) |
| **Retrieval augmented generation** | Retrieve relevant past video segments to condition generation | [VRAG](https://openreview.net/forum?id=FzfYoUp8F1) |
| **Hybrid SSM + Attention** | SSM for long-range temporal; local attention for spatial detail | [Long-Context SSM WMs](https://arxiv.org/abs/2505.20171) |
| **Cycle-consistency** | Forward-backward generation enforces temporal coherence | [LIVE](https://arxiv.org/abs/2602.03747) |
| **Checkpointed self-forcing** | Periodic ground-truth resets during autoregressive rollout | [Solaris](https://arxiv.org/abs/2602.22208), [Waypoint-1](https://over.world/blog/the-path-to-real-time-worlds-and-why-it-matters) |

### 3D Representation

How models incorporate spatial understanding.

| Representation | Trade-off | Representative Works |
| --- | --- | --- |
| **Implicit (pixel-space)** | No explicit 3D; fast but limited viewpoint consistency | [GameNGen](https://arxiv.org/abs/2408.14837), [Oasis](https://oasis-model.github.io/), [DIAMOND](https://arxiv.org/abs/2405.12399) |
| **3D cache / depth conditioning** | Lightweight 3D signal guides 2D generation | [GEN3C](https://openaccess.thecvf.com/content/CVPR2025/papers/Ren_GEN3C_3D-Informed_World-Consistent_Video_Generation_with_Precise_Camera_Control_CVPR_2025_paper.pdf), [Geometry Forcing](https://arxiv.org/abs/2507.07982) |
| **Point cloud / point latents** | Native 3D latent space; efficient but sparse | [Terra](https://arxiv.org/abs/2510.14977), [MagicWorld](https://arxiv.org/abs/2511.18886), [EvoWorld](https://arxiv.org/abs/2510.01183) |
| **Gaussian splatting** | Real-time renderable; exportable 3D assets | [Marble](https://www.worldlabs.ai/blog/bigger-better-worlds), [Visionary](https://arxiv.org/abs/2512.08478), [HunyuanWorld](https://arxiv.org/abs/2507.21809) |
| **Mesh-based** | Traditional 3D; compatible with game engines | [HunyuanWorld](https://arxiv.org/abs/2507.21809), [Matrix-3D](https://arxiv.org/abs/2508.08086), [WorldGen](https://www.meta.com/blog/worldgen-3d-world-generation-reality-labs-generative-ai-research) |
| **4D (dynamic 3D)** | Spatiotemporal; captures motion and deformation | [NeoVerse](https://arxiv.org/abs/2601.00393), [DynamicVerse](https://arxiv.org/abs/2512.03000), [SeeU](https://arxiv.org/abs/2512.03350) |

---

## Benchmarks & Evaluation

- **WorldSimBench** (Oct 2024) — **Dual perceptual + manipulative evaluation**; tests whether generated videos translate into valid control signals across embodied scenarios. [[Paper](https://arxiv.org/abs/2410.18072)] [[Website](https://iranqin.github.io/WorldSimBench.github.io/)]
- **WorldModelBench** (Feb 2025) — **Subtle physics violation detection**; 67K human labels measuring whether models catch mass conservation breaches and irregular object changes. [[Paper](https://arxiv.org/abs/2502.20694)] [[Website](https://worldmodelbench-team.github.io/)]
- **VideoVerse** (Oct 2025) — **Event-level temporal causality**; 300 prompts with 815 events evaluating causal reasoning depth beyond per-frame quality. [[Paper](https://arxiv.org/abs/2510.08398)]
- **Gen-ViRe** (Nov 2025) — **Chain-of-Frames reasoning**; decomposes visual reasoning into 6 cognitive dimensions and 24 subtasks measuring multi-step planning. [[Paper](https://arxiv.org/abs/2511.13853)] [[Code](https://github.com/L-CodingSpace/GVR)]
- **4DWorldBench** (Nov 2025) — **Unified 3D/4D evaluation**; maps diverse input modalities into textual representations for perceptual quality, physical realism, and 4D consistency. [[Paper](https://arxiv.org/abs/2511.19836)]
- **SmallWorlds** (Nov 2025) — **Isolated dynamics testbed**; compares RSSM, Transformers, Diffusion, and Neural ODEs under controlled rollout degradation. [[Paper](https://arxiv.org/abs/2511.23465)]
- **WorldBench** (Jan 2026) — **Disentangled physics diagnostics**; isolates individual physical principles (object permanence, friction, viscosity) instead of testing them jointly. [[Paper](https://arxiv.org/abs/2601.21282)] [[Website](https://world-bench.github.io/)]
- **PhysicsMind** (Jan 2026) — **Law-consistent reasoning + generation**; evaluates both VQA physical reasoning and physics-compliant video generation across canonical laws. [[Paper](https://arxiv.org/abs/2601.16007)]
- **MIND** (Feb 2026) — **Closed-loop memory + action control**; first open-domain revisited benchmark testing temporal stability across viewpoint changes. [[Paper](https://arxiv.org/abs/2602.08025)] [[Code](https://github.com/CSU-JPG/MIND)]

---

## Theory, Positions & Explainability

### Theory

- **Scaling Laws for Pre-training Agents and World Models** (Nov 2024) — Establishes predictable scaling laws for agent pre-training; coefficients vary by implementation choices. [[Paper](https://arxiv.org/abs/2411.04434)]
- **When Do Neural Networks Learn World Models?** (Feb 2025) — Proves low-degree-bias models recover latent world variables through multi-task learning under mild assumptions. [[Paper](https://arxiv.org/abs/2502.09297)]
- **General Agents Need World Models** (Jun 2025) — Formally proves multi-step goal-directed agents mathematically require world models for generalization. [[Paper](https://arxiv.org/abs/2506.01622)]
- **What Does it Mean for a Neural Network to Learn a 'World Model'?** (Jul 2025) — Defines precise, testable criteria for verifying neural networks genuinely learn world models. [[Paper](https://arxiv.org/abs/2507.21513)]

### Positions

- **Compositional Generative Modeling: A Single Model is Not All You Need** (Feb 2024) — Composing smaller specialized generative models outperforms monolithic models in efficiency and adaptability. [[Paper](https://arxiv.org/abs/2402.01103)]
- **Video as the New Language for Real-World Decision Making** (Feb 2024) — Proposes video as a unified interface for decision-making, analogous to language for LLMs. [[Paper](https://arxiv.org/abs/2402.17139)]
- **Interactive Generative Video as Next-Generation Game Engine** (Mar 2025) — Argues generative video models will replace traditional game engines for unlimited dynamic content. [[Paper](https://arxiv.org/abs/2503.17359)]
- **Critiques of World Models** (Jul 2025) — World models should simulate actionable possibilities for purposeful reasoning, not just prediction. [[Paper](https://arxiv.org/abs/2507.05169)]
- **Beyond World Models: Rethinking Understanding in AI Models** (Nov 2025) — Challenges the assumption that world model capabilities equate to human-like understanding. [[Paper](https://arxiv.org/abs/2511.12239)]

### Explainability

- **Transformers Use Causal World Models in Maze-Solving Tasks** (Dec 2024) — Shows transformers develop causally interpretable internal world models with asymmetric feature activation. [[Paper](https://arxiv.org/abs/2412.11867)]

---

## Key Blog Posts & Technical Reports

- **Towards Video World Models** — In-depth blog on the trajectory from video generation to world simulation. [[Blog](https://www.xunhuang.me/blogs/world_model.html)]
- **Jim Fan's World Model Thread** — Influential X/Twitter thread defining world models in the context of modern AI. [[Link](https://x.com/DrJimFan/status/1709947595525951787)]

---

## Contributing

Contributions are welcome! Please feel free to submit a [Pull Request](https://github.com/gxchris95/awesome-world-models-video-games-3d/pulls) or open an [Issue](https://github.com/gxchris95/awesome-world-models-video-games-3d/issues).

When adding a new entry, please follow the format below. Affiliation and extra links are optional. Sort chronologically within each section.

**Research papers:**
```
- **Model Name** (Affiliation, Mon Year) — **Key technique**; one-line differentiator. [[Paper](url)] [[Code](url)] [[Blog](url)] [[Website](url)]
```

**Surveys & positions:**
```
- **Paper Title** (Mon Year) — One-line summary. [[Paper](url)]
```

---

## Citation

If you find this repository useful, please consider citing it:

```bibtex
@misc{awesomeworldmodel,
  title={Awesome World Models for Video, Games \& 3D},
  author={Xin (Kris) Gao and Contributors},
  year={2026},
  howpublished={\url{https://github.com/gxchris95/awesome-world-models-video-games-3d}},
}
```


<div align="center">

**If you find this list helpful, please give it a star!**

</div>
