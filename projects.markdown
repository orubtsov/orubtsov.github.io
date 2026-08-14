---
layout: default
title: Projects
page_title: "Projects — Oleg Rubtsov"
permalink: /projects/
---

Longer write-ups of the work summarised on the [main page](/), most recent first.

## Prequel Inc. · Apr 2020 – Present

### Video Transitions · 2026 – present

Generating animated transitions from a still photograph. The incumbent implementation relied on a third-party API; fine-tuning an open video generation model in-house with **LoRA** brought the cost per generation down by **2.5×**.

A larger video model was adapted in parallel, also with **LoRA**: it produced visibly better transitions and worked acceptably even without fine-tuning, but at a higher cost per inference. Running both lines gave the product a measured quality-versus-unit-cost curve to choose from rather than a single option.

### Video Restoration in Production · 2026

Took a modern video restoration model from evaluation through to a working production deployment.

### NSFW Content Classification · 2026

Trained an in-house classifier for automatic labelling of NSFW content. Currently under evaluation ahead of integration.

### Automated Image Adjustment · 2025–2026

Three successive approaches to automatic photo enhancement.

**Differentiable filters.** Trained a network to predict parameters for a suite of image filters — brightness, contrast, saturation and similar — implemented directly in **PyTorch** so the whole chain stayed differentiable. Iterated extensively on the formulation.

**Reinforcement learning over a non-differentiable engine.** The production graphics engine exposes primitives that cannot be differentiated through, so the problem was reframed: a goal-conditioned RL agent takes an image plus summary statistics and learns to drive the engine's controls toward a reference auto-adjustment target, with the engine itself serving as the environment. Built as a research prototype.

**Vision-language models.** The current line of work drives a VLM against the engine's **JSON** API and lets the model choose the adjustments end-to-end. This works in practice and produces good results; a further iteration is underway.

### Generative Inference in Production · 2023–2025

Built and shipped a large number of production services around **Stable Diffusion**, **SDXL** and fine-tuned diffusion checkpoints: writing the inference code and serving plumbing, converting checkpoints into the formats each runtime required, and taking the services through to deployment.

In 2025 this extended to specialised hardware — compiling **SDXL** and **Flux** for **AWS Inferentia** using the **AWS Neuron** SDK.

### Virtual Try-On — Feasibility Study · Summer 2024

Assessed **IDM-VTON** for virtual garment try-on: established the boundaries of applicability, benchmarked inference latency, and presented the findings to the product team, which used them to decide against productization.

### SDXL Inpainting · 2023

Fine-tuned **SDXL** for inpainting and worked on accelerating inference for production use.

### Identity-Preserving ControlNet · 2022–2023

Trained a **ControlNet** for identity preservation from scratch, building both the dataset and the training pipeline in-house, and got identity transfer working end to end.

### Personalized Generation · 2022

Trained per-user **DreamBooth** models powering a personalized generation feature shipped to production.

### Stylization at Scale · 2021–2022

An in-house pipeline turned only 20–30 reference photos of a target style into a large volume of synthetic paired training data, making new styles cheap and fast to produce. That synthetic data trained a compact **img2img** model — a **SPADE**-based **U-Net** — which shipped to production and was served through **Triton** and custom cloud pipelines. The team delivered an extensive catalog of styles this way, including a broad range of anime looks.

### Interactive Image Segmentation · 2021

Click-driven segmentation of arbitrary objects on an **HRNet** backbone: the user taps a point, the model segments the object, and each further tap refines the mask — growing or trimming the previous prediction rather than starting over. The model takes the click history as input, so corrections accumulate.

**Training without users.** Training such a model needs click sequences that no dataset provides, so I wrote a user-behaviour simulator from scratch. Instead of sampling clicks at random it places them the way a person would — mostly near the centre of mass of an object mask, occasionally along its edges — and generates the corrective clicks that follow from the model's own current error.

**On device.** Ported to mobile with the **MNN** inference framework, running at **150 ms** per interaction.

### On-Device Computer Vision · 2020–2021

**Human segmentation.** Trained a **U-Net**-style human segmentation model and ported it to mobile single-handedly, running in real time on device.

**Pose estimation on video.** Adapted an open-source pose estimation model for video: rather than running full inference on every frame, predicted keypoints are tracked between frames with **optical flow** and inference is re-run only once a keypoint drifts beyond a set threshold. This reached real-time performance on typical user-recorded video. Ported to **iOS** and **Android**, including the **Objective-C** and **JNI** bindings.

**Denoising.** Two complementary solutions: a dual-context convolutional denoising network, and a **Non-Local Means** implementation hand-written in **C++** and ported to mobile.


## Frisbuy · Jun 2018 – Feb 2020

### Fashion Recognition and Recommendation Systems

An end-to-end **street-to-shop** pipeline allowing users to identify garments from everyday photos and retrieve visually similar products from partner catalogs holding tens of thousands of items.

**Models.** A **RetinaNet** clothing detector trained from scratch, and garment embeddings learned with **triplet loss** on an **Inception**-family backbone to power visual similarity search.

**Infrastructure.** Designed and implemented single-handedly — provisioning services, writing a custom **RabbitMQ** consumer, and owning model deployment, optimization, and iterative improvements across **Kubernetes**, **MongoDB**, and **MinIO**.

**Outcome.** Shipped to production and validated in A/B tests with several pilot clients, where it lifted overall sales by around **12%**.

**Team.** Started as the sole engineer on the project and later onboarded and mentored a junior engineer.


## Independent Research

### Video Diffusion from Scratch on a Single GPU
*Free-time research · 2025, resumed Mar 2026 – present*

Adapted the ["Diffusion Training from Scratch on a Micro-Budget"](https://arxiv.org/abs/2407.15811) approach from images to video generation, training on a single **RTX 6000 Pro** with the **OpenVid** dataset under a **flow-matching** objective.

The model improved across successive iterations: 3D **RoPE**, richer generated captions, classifier-free guidance with caption dropout, **REPA** representation alignment, and a move from pixel space to latents using an off-the-shelf **VAE**.

**Results.** **FVD-I3D 146.76** and **CLIPScore 32.28**, versus 30.63 measured on held-out real video–caption pairs under the same evaluation pipeline. Current samples show coherent temporal structure across frames and recognisable object features.

**Ownership.** A solo project: I set the research direction, designed the experiments, chose the objective and the architectural changes, decided which ablations to run, and interpreted the results to pick the next step.

### Satellite Image Segmentation
*Volunteer collaboration with an independent group of ML enthusiasts*

Semantic segmentation of satellite imagery to identify regions of ice, water, and clouds.
