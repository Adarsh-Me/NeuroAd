# NeuroAd

**NeuroAd** is an experimental neurocomputational advertising intelligence notebook that converts campaign media into predicted cortical-response telemetry using Meta's TRIBE v2 brain-encoding stack. Instead of treating creative review as a shallow click-through exercise, NeuroAd frames an advertisement as a multimodal neural stimulus and produces time-resolved proxies for attention capture, memory encoding, emotional valence, and cognitive load.

The project is intentionally notebook-native: it can be executed in Colab or Kaggle with GPU acceleration, authenticates against gated Hugging Face models, runs TRIBE v2 inference over video/audio/image stimuli, and exposes an interactive Gradio dashboard for frame-level inspection.

Direct Kaggle launch: [https://www.kaggle.com/code/adarshm12/neuroad](https://www.kaggle.com/code/adarshm12/neuroad)

## Core Idea

Modern ad analytics usually measures behavior after exposure. NeuroAd explores the harder question: **what does the creative stimulus look like inside a predicted brain-response manifold before the campaign is shipped?**

The notebook combines:

- Meta TRIBE v2 neural encoding inference
- Hugging Face gated-model authentication
- multimodal stimulus normalization for video, image, and audio assets
- cortical activation summarization
- NeuroAd proxy metrics for attention, memory, valence, and load
- an interactive campaign diagnostics dashboard
- exportable prediction arrays and event tables for downstream analysis

## Why This Is Different

NeuroAd is not a conventional marketing dashboard. It is a research-grade creative telemetry layer that treats media as a stimulus sequence and translates that stimulus into structured neural-response signals. The result is a prototype workflow for evaluating creative intensity, overload risk, salience, and memory pressure before launching expensive media.

## Notebook

The main artifact is:

- [`Notebook/neuroad.ipynb`](Notebook/neuroad.ipynb)

It includes installation, environment verification, Hugging Face authentication, TRIBE v2 model loading, Kaggle/Colab compatibility fixes, short smoke tests, lightweight visualization, Gradio dashboard execution, and export utilities.

## Runtime Requirements

Recommended:

- Python notebook runtime
- CUDA GPU
- Hugging Face account with accepted gated-model terms
- Hugging Face token saved as `HF_TOKEN`
- Colab L4/A100 or Kaggle GPU for short stimuli

Kaggle GPUs can run the workflow, but long audio/video clips can exhaust VRAM. For Kaggle, keep audio-enabled stimuli short unless a larger GPU is available.

## Authentication

Create a Hugging Face token and accept model access terms for:

- `facebook/tribev2`
- the LLaMA model resolved by TRIBE v2

Then save the token as:

- Kaggle Secret: `HF_TOKEN`
- Colab Secret: `HF_TOKEN`
- or environment variable: `HF_TOKEN`

## Execution Flow

Run the notebook cells in order:

1. Runtime path setup
2. Dependency installation
3. Runtime restart
4. Environment verification
5. Hugging Face login
6. TRIBE v2 model load
7. Smoke test or dashboard inference
8. Dashboard launch
9. Export predictions

## Outputs

NeuroAd can export:

- `.npy` prediction tensors
- `.csv` event dataframes
- frame-level dashboard diagnostics
- cortical activation summaries

These files can be used for offline modeling, creative comparison, ROI calibration, or future campaign-intelligence pipelines.

## Status

This is an experimental research prototype, not a clinical neuroscience system and not a validated substitute for human-subject measurement. Its value is in rapid neurocreative prototyping: using state-of-the-art brain-encoding models to create a new layer of pre-market creative intelligence.
