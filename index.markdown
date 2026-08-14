---
layout: default
title: Oleg Rubtsov
page_title: "Oleg Rubtsov — Senior ML / Research Engineer"
---

Eight years taking vision problems from paper to production: diffusion models and GANs, real-time models running on phones, and the infrastructure that serves them. I take open-ended problems, research the options, and ship the result.


## Experience

### Senior Data Scientist — [Prequel Inc.](https://prequel.app)
*Apr 2020 – Present · Remote, Kuala Lumpur, Malaysia*

Joined as a middle engineer building on-device computer vision, promoted to Senior after the first year, and moved progressively into generative modelling, production inference at scale, and open-ended R&D.

- **Video transitions** (2026, current): cutting cost per generation **2.5×** against the incumbent third-party API by fine-tuning an open video generation model in-house with **LoRA**, and adapting a stronger, costlier model alongside it to map the quality-versus-unit-cost trade-off. Also took a modern video restoration model into production.
- **Generative inference in production** (2023–2025): built and shipped a large number of **Stable Diffusion**, **SDXL** and fine-tuned diffusion services — inference code, serving plumbing, checkpoint conversion, and production deployment. Compiled **SDXL** and **Flux** for **AWS Inferentia** with the **AWS Neuron** SDK.
- **Generative models in production** (2022–2024): trained per-user **DreamBooth** models that shipped as a production feature, and built an identity-preserving **ControlNet** from scratch — own dataset, own training pipeline. Ran the virtual try-on feasibility study that settled the company's position on the technology.
- **Open-ended R&D on automatic photo enhancement** (2025–2026): took an ill-defined product problem through three research directions — predicting parameters for differentiable filters, a goal-conditioned **RL** agent that drives the app's non-differentiable graphics engine as its environment, and **vision-language models** choosing adjustments end to end. The VLM approach works and is the line currently in development.
- **Real-time computer vision on mobile** (2020–2022): shipped human segmentation and pose estimation to **iOS** and **Android** end to end — model, algorithmic optimization, and native integration. Made pose estimation real-time on user video with an **optical-flow** keypoint-tracking scheme that re-runs inference only on drift, and wrote the **Objective-C** and **JNI** bindings myself. Shipped click-driven interactive segmentation at **150 ms** per interaction on device via **MNN**, training it against a user-behaviour simulator I wrote from scratch.
- Owned research-to-production projects delivered with teams of around three engineers; mentored engineers and ran technical interviews.

### Computer Vision Research Engineer — [Frisbuy](https://frisbuy.ru)
*Jun 2018 – Feb 2020 · Kaliningrad, Russia*

Sole engineer on the company's core product, from research through to production.

- Built an end-to-end **street-to-shop** system: identify garments from everyday photos and retrieve visually similar products from catalogs holding tens of thousands of items.
- Trained a **RetinaNet** detector from scratch and learned garment embeddings with **triplet loss** on an **Inception**-family backbone.
- Designed and implemented the entire production infrastructure — **Kubernetes**, **RabbitMQ**, **MongoDB**, **MinIO** — including a custom message consumer, then onboarded and mentored a junior engineer onto the project.
- Shipped to production and validated in A/B tests with pilot clients, where it lifted overall sales by around **12%**.

[Detailed write-ups of individual projects →](/projects/)


## Selected Research

### Video Diffusion from Scratch on a Single GPU
*Independent research · 2025, resumed Mar 2026 – present*

Adapted ["Diffusion Training from Scratch on a Micro-Budget"](https://arxiv.org/abs/2407.15811) from images to video, training on a single **RTX 6000 Pro** with **OpenVid** under a **flow-matching** objective. Set the research direction, designed the experiments and ablations, and drove the model through successive improvements: 3D **RoPE**, richer captions, CFG with caption dropout, **REPA**, and a move from pixel space to latents.

**FVD-I3D 146.76** and **CLIPScore 32.28**, versus 30.63 on held-out real video–caption pairs under the same evaluation pipeline.


## Skills

- **ML & Generative Vision**: PyTorch; diffusion and flow-matching models, GANs, vision-language models, reinforcement learning, metric learning; detection, segmentation, pose estimation, image enhancement
- **ML Systems & Optimization**: C++, TensorRT, AWS Inferentia / Neuron, MNN; GPU inference optimization, real-time mobile inference, Objective-C / JNI integration
- **Training & Production Infrastructure**: Python, Triton, Ray, Modal, Docker, Kubernetes, MLflow
