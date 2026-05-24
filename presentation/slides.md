---
theme: default
title: Optimizing an AI to Identify Particle Collisions
info: Transfer Learning Strategies for Jet Tagging at the LHC
transition: fade-out
fonts:
  sans: Source Sans Pro
  serif: Merriweather
  mono: Roboto Mono
  weights: '300,400,600,700'
  italic: true
drawings:
  enabled: false
layout: cover
---

# Teaching an AI to Identify Particle Collisions

## Without Starting From Scratch

Transfer Learning Strategies for Jet Tagging at the LHC
with Pretrained Foundation Models

---
layout: bgimage
image: /lhc-bg.jpg
---

::title::

# The Big Picture

::default::

**The Large Hadron Collider (LHC)** — CERN, Switzerland — 27 km circular tunnel

- Smashes protons together at near light-speed
- ~40 million collisions per second
- Each collision creates sprays of particles called "jets"
- Jets are how we "see" short-lived heavy particles

---
layout: none
---

<video src="/lhc-animation.mp4" controls style="width:100%; height:100%; object-fit:cover; position:absolute; inset:0;" />

---
layout: image
---

::header::

# The Firework Analogy

## You never see the firework shell — only the burst of sparks it leaves behind. From that pattern alone, you must identify the shell type.

::default::

![Firework analogy diagram](/fireworks.svg)

::footer::

> Different parent particles produce jets with different internal patterns — just like different firework shells!

---
layout: two-cols
leftClass: col-red
rightClass: col-green
---

::header::

# The Problem: AI Training is Expensive

## Current approaches require massive compute and data — but what if we could skip most of that?

::left::

### Training from Scratch

- 2.2 million parameters to optimize
- 100M+ labeled jets needed
- Days to weeks of GPU compute
- Start over for each new task

::right::

### Transfer Learning

- Only 35,000 parameters (1/60th!)
- Works with small datasets
- Minutes to hours of compute
- Reuse existing knowledge

::footer::

> Can we reuse a general-purpose "jet understanding" model to cut costs without sacrificing accuracy?

---
layout: two-cols
leftClass: col-blue
rightClass: col-green
---

::header::

# What is Transfer Learning?

## Taking an AI model that already learned something useful on one task and reusing that knowledge for a different (but related) task. Instead of learning from zero, you start from a foundation of existing knowledge.

::left::

### Learn Spanish First

- Grammar structure
- Latin vocabulary roots
- Conjugation patterns
- *(broad foundation)*

::right::

### Adapt to Italian

- Only learn the differences
- Much faster!
- *(small, cheap adaptation)*

::footer::

> Sophon (188 jet types) → Adapt to 10 classes = Same principle, applied to physics!

---
layout: image
---

::header::

# Meet Sophon: The Foundation Model

## Sophon (Signature-Oriented Pre-training for Heavy-resonant ObservatioN), a pre-trained base model to facilitate all LHC analyses exploring the large-R jet

::default::

![Sophon architecture](/sophon-arch.svg)

::footer::

> Architecture: Particle Transformer, 8 attention blocks, 2.2M params | Pre-training: ~250M jets, 188 classes | Output: 128-number "fingerprint" per jet

<small>Source: Accelerating Resonance Searches via Signature-Oriented Pre-training</small>

---
layout: two-cols
leftClass: col-blue
rightClass: col-green
---

::header::

# What Does “Frozen” Mean?

## Keep the main model unchanged, extracting the data to save on computation costs

::left::

### Frozen = “Use the textbook as-is”

- Like using a published encyclopedia without changing any entries
- You just add sticky-note tabs to find what you need faster
- The model's internal numbers (“weights”) are locked — only the tiny new head gets updated
- **Fast, cheap, nearly as good**

::right::

### Trainable = “Rewrite the textbook”

- Like rewriting chapters to be more relevant to your topic
- All the model's weights are unlocked and can change during training
- Better results, but takes much more time, data, and computing power
- **Slower, expensive, slightly better**

---
layout: image
---

::header::

# Three Adaptation Strategies

## How much of the pretrained model do we allow to change?

::default::

![Three strategies: frozen, partial fine-tune, full fine-tune](/strategies.svg)

::footer::

> **Blue** = FROZEN (locked, not learning) · **Orange/Green** = TRAINABLE (updating during training) · **Orange box** = New classification head

---
layout: image
---

::header::

# Performance vs. Training Data

## Performance improves predictably as data grows, following a "power law" — but with diminishing returns.

::default::

![Performance vs data size](/perf-chart.png)

- Each curve = average test AUC across 3 random seeds, 10K–100M jets
- Solid markers = measured; dashed = power-law fits
- **Frozen Sophon + 35K MLP reaches 0.979, within 0.9% of SOTA's 0.988**
- Crossover at ~100K jets: where fine-tuning begins to outperform frozen features

::footer::

> **AUC(N) = AUC∞ − A · N⁻ᵅ**

---
layout: image
---

::header::

# Visualizing What the Model Learns

## UMAP projections: 128-dimensional embeddings compressed to 2D for visualization

::default::

![UMAP overview](/umap-overview.svg)

::footer::

> Silhouette score measures cluster separation (higher = better). Going from 0.077 to 0.206 = 2.7× tighter clusters after fine-tuning.

---
layout: image
title: UMAP Detail Comparison
---

::header::

# UMAP Detail Comparison

::default::

![UMAP detail comparison](/umap-detail.svg)

::footer::

- 2D projections of Sophon's 128-d jet embeddings for 30K test jets (axes locked for comparison)
- Even the pretrained backbone (left) already groups jet types into visible clusters; full fine-tuning (right) makes them much tighter
- **Silhouette score improves 0.077 → 0.206, ~2.7× improvement in cluster sharpness**

---
layout: two-cols
leftClass: col-blue
rightClass: col-gray
---

::header::

# Understanding AUC (Area Under the Curve)

::left::

### The ROC Curve

Plots a tradeoff:

**Y-axis: True Positive Rate**
How many real jets you correctly catch

**X-axis: False Positive Rate**
How many fakes you accidentally accept

AUC = area under this curve:
- 1.0 = perfect classifier
- 0.5 = random guessing
- 0.97+ = excellent

::right::

### Intuition Scale

<div style="display:flex; flex-direction:column; gap:0.5rem; margin-top:0.5rem;">
<div style="background:#D32F2F; color:white; padding:0.5rem 1rem; border-radius:6px; font-size:0.82rem; font-weight:500;">0.5 — Random (coin flip)</div>
<div style="background:#F57C00; color:white; padding:0.5rem 1rem; border-radius:6px; font-size:0.82rem; font-weight:500;">0.7 — Fair</div>
<div style="background:#FBC02D; color:#333; padding:0.5rem 1rem; border-radius:6px; font-size:0.82rem; font-weight:500;">0.85 — Good</div>
<div style="background:#66BB6A; color:white; padding:0.5rem 1rem; border-radius:6px; font-size:0.82rem; font-weight:500;">0.95 — Excellent</div>
<div style="background:#2E7D32; color:white; padding:0.5rem 1rem; border-radius:6px; font-size:0.82rem; font-weight:500;">0.979 — This paper!<br>0.988 — State-of-the-art</div>
</div>

---
layout: image
title: ROC Curves
---

::header::

# Training results

::default::

![ROC curves for all strategies](/roc-curves.svg)

::footer::

- 10 class-vs-rest ROC curves per panel (log-scale false-positive axis)
- Macro AUC: Frozen 0.979, Partial FT 0.979, Full FT 0.984
- **Heavy-flavor jets (H→bb, t→bqq) are easiest; gluon-tagging is hardest — consistent with known physics**

---
layout: quad
---

::header::

# Why This Matters

::tl::

<svg width="54" height="54" viewBox="0 0 40 40"><circle cx="20" cy="20" r="18" fill="none" stroke="#2E7D32" stroke-width="2.5"/><path d="M12 20l5 5 11-11" stroke="#2E7D32" stroke-width="2.5" fill="none" stroke-linecap="round" stroke-linejoin="round"/></svg>

### Massive Cost Savings

99.1% of SOTA performance using 1/60th the trainable parameters

::tr::

<svg width="54" height="54" viewBox="0 0 40 40"><rect x="4" y="8" width="32" height="24" rx="3" fill="none" stroke="#2E7D32" stroke-width="2.5"/><path d="M4 16h32M14 16v16" stroke="#2E7D32" stroke-width="2.5"/><circle cx="9" cy="12" r="1.5" fill="#2E7D32"/></svg>

### Practical Guidance

If labeled data < 100K jets, don't fine-tune — frozen features are better

::bl::

<svg width="54" height="54" viewBox="0 0 40 40"><circle cx="20" cy="14" r="6" fill="none" stroke="#2E7D32" stroke-width="2.5"/><path d="M8 34c0-6.6 5.4-12 12-12s12 5.4 12 12" fill="none" stroke="#2E7D32" stroke-width="2.5"/><path d="M26 10l4-4M26 6l4 4" stroke="#2E7D32" stroke-width="2" stroke-linecap="round"/></svg>

### Foundation Models for Physics

Like GPT for language, Sophon learns general "jet physics" that transfers to specific tasks

::br::

<svg width="54" height="54" viewBox="0 0 40 40"><path d="M20 4v32M4 20h32" stroke="#2E7D32" stroke-width="2.5" stroke-linecap="round"/><path d="M10 10l20 20M30 10l-20 20" stroke="#2E7D32" stroke-width="1.5" stroke-linecap="round" opacity="0.5"/><circle cx="20" cy="20" r="3" fill="#2E7D32"/></svg>

### Scalable Science

Makes cutting-edge analyses accessible to smaller labs without massive GPU budgets

---
layout: cover
---

# Summary

## A frozen pretrained backbone with a tiny classification head achieves 99% of state-of-the-art accuracy at 1/60th the cost.

- Transfer learning lets us reuse existing AI knowledge
- Frozen features beat fine-tuning when data is scarce
- Foundation models work for physics just like they work for language
- This makes advanced particle physics accessible to more researchers

> UC San Diego | San Diego Supercomputer Center | References: arXiv:2202.03772, arXiv:2405.12972
