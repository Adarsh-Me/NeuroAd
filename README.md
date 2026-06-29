# NeuroAd

**NeuroAd** is a multimodal neurocreative intelligence system that converts advertising media into predicted cortical-response telemetry. It uses **Meta TRIBE v2** as the neural encoding substrate, then wraps the raw high-dimensional brain predictions inside an applied campaign-analysis layer for attention, memory encoding, emotional valence, cognitive load, overload risk, and frame-level creative diagnostics.

Direct Kaggle launch: [https://www.kaggle.com/code/adarshm12/neuroad](https://www.kaggle.com/code/adarshm12/neuroad)

Main notebook: [Notebook/neuroad.ipynb](Notebook/neuroad.ipynb)

NeuroAd is not a classical ad dashboard and it is not just a notebook demo. It is a prototype for a more ambitious category of tooling: **pre-market neural response simulation for creative media**. Instead of waiting for click-through rate, watch-time, conversion lift, or survey recall after a campaign is already live, NeuroAd treats the creative itself as a multimodal stimulus and asks what kind of predicted brain-response structure it may produce before media spend is committed.

## Product Thesis

Most advertising analytics systems operate downstream. They observe user behavior after exposure and summarize what already happened. NeuroAd moves the analysis upstream. It models the creative artifact itself as a temporally structured neural stimulus and produces interpretable telemetry from predicted cortical activity.

The central idea is technically aggressive:

> A campaign asset can be analyzed as a stimulus-response object, not merely as a file, video, or marketing impression.

That means a video, image, or audio asset is not treated as a passive upload. NeuroAd normalizes the media, constructs event sequences, runs brain-encoding inference, compresses cortical prediction tensors into campaign-facing signals, and visualizes the result as a diagnostic decision interface.

## What NeuroAd Does

NeuroAd performs an end-to-end transformation:

1. Ingests campaign media such as video, image, or audio.
2. Converts the media into TRIBE-compatible event structures.
3. Runs gated Hugging Face authentication for Meta TRIBE v2 model access.
4. Executes GPU-backed neural response inference.
5. Produces predicted BOLD-style cortical activity tensors.
6. Derives NeuroAd proxy signals for creative analysis.
7. Visualizes frame-level neural telemetry through plots and dashboard components.
8. Exports prediction arrays and event metadata for downstream analysis.

The project is designed to feel like a miniature campaign brain lab: a place where a creative asset is uploaded, decomposed, interpreted, and converted into a dense neural-response trace.

## Sample Output

The repository includes sample exports and rendered visuals in [Sample Output](Sample%20Output).

### Cortical Activity Summary

![Cortical activity summary](Sample%20Output/newplot.png)

This plot compresses high-dimensional predicted cortical activity into a renderable visualization. The goal is not to show every brain vertex directly, but to provide a tractable view of activation intensity across time and compressed cortical bins. This makes the prediction tensor inspectable without freezing the notebook renderer.

### Dashboard And Runtime Screens

![Sample dashboard output 1](Sample%20Output/Screenshot%202026-06-24%20214018.png)

![Sample dashboard output 2](Sample%20Output/Screenshot%202026-06-24%20214041.png)

![Sample dashboard output 3](Sample%20Output/Screenshot%202026-06-24%20214133.png)

These screenshots show the operational surface of the project: a notebook-driven inference workflow with visual diagnostics, event metadata, and model outputs exported for reuse.

## Repository Structure

| Path | Purpose |
|---|---|
| [Notebook/neuroad.ipynb](Notebook/neuroad.ipynb) | Main executable NeuroAd notebook |
| [Sample Output](Sample%20Output) | Example prediction tensor, event metadata, and rendered visual outputs |
| [README.md](README.md) | Product-facing technical documentation |
| [SUMMARY.md](SUMMARY.md) | Architecture and implementation summary |
| [LICENSE](LICENSE) | Repository license |

## Core Technical Stack

NeuroAd is built around a hybrid stack of neural encoding, multimodal preprocessing, and notebook deployment engineering.

| Layer | Technology |
|---|---|
| Neural encoding | Meta TRIBE v2 |
| Model access | Hugging Face Hub gated authentication |
| Tensor runtime | PyTorch CUDA |
| Video and audio handling | FFmpeg, imageio-ffmpeg |
| Data processing | NumPy, Pandas |
| Visualization | Plotly, lightweight cortical heatmaps |
| Dashboard surface | Gradio |
| Hosted execution | Kaggle GPU, Google Colab GPU |
| Export artifacts | NPY prediction tensors, CSV event traces |

## Architecture

NeuroAd is organized as a staged inference system.

### 1. Runtime Bootstrap

The notebook creates stable working directories for cache, media, and export artifacts. This is necessary because hosted notebook runtimes differ in filesystem layout. Colab tends to use `/content`, while Kaggle exposes `/kaggle/working` for persistent output artifacts.

### 2. Dependency Installation

The installation cell pins sensitive components across Torch, Torchvision, Transformers, Gradio, and Hugging Face Hub. This was necessary because hosted GPU notebooks frequently ship preinstalled packages that are mutually incompatible with newer model stacks.

The notebook includes compatibility handling for:

- Torch and Torchvision CUDA wheel mismatch
- missing Torchvision operator schemas on Kaggle
- missing `torchvision::nms` operator metadata
- Transformers and Hugging Face Hub version conflicts
- Gradio API-schema failures in hosted notebook environments
- Kaggle secret loading for Hugging Face tokens

This engineering layer is a major part of the project. The model is hard to run reliably in transient notebook runtimes, so NeuroAd includes operational hardening rather than assuming a perfect local machine.

### 3. Authentication

TRIBE v2 and related model dependencies are gated. NeuroAd supports:

- Kaggle Secret named `HF_TOKEN`
- Colab Secret named `HF_TOKEN`
- local environment variable named `HF_TOKEN`
- manual secure token prompt fallback

This makes the notebook portable across common ML demo environments.

### 4. Stimulus Processing

Input assets are normalized before inference. The notebook supports:

- video stimulus files
- image files converted into short stimulus videos
- audio files wrapped into video containers
- short Kaggle-safe media paths to avoid VRAM exhaustion

The media asset is turned into a TRIBE event dataframe, which becomes the structured representation that drives inference.

### 5. Neural Inference

TRIBE v2 predicts brain-response activity over time. The resulting array is effectively a temporal matrix:

```text
timesteps x cortical vertices
```

This high-dimensional output is too dense for normal creative review, so NeuroAd adds an interpretation layer that compresses the raw prediction into campaign-facing metrics.

### 6. NeuroAd Proxy Metrics

NeuroAd derives four main proxy signals from the prediction tensor:

| Signal | Interpretation |
|---|---|
| Attention Capture | How strongly a moment activates high-intensity response patterns |
| Memory Encoding | How strongly positive activation patterns suggest durable encoding pressure |
| Emotional Valence | Directional response proxy derived from lateralized activation contrast |
| Cognitive Load | Combined dispersion and temporal-change pressure, used to identify overload risk |

These are not clinical claims. They are pragmatic model-derived signals that make neural prediction outputs usable for creative analysis.

### 7. Dashboard Layer

The Gradio dashboard gives the project a usable product surface. It supports:

- media upload
- sample video execution
- timeline scrubbing
- attention, memory, valence, and cognitive-load scores
- cortical activation plots
- telemetry timeline plots
- event dataframe preview
- exportable prediction artifacts

## Output Artifacts

The [Sample Output](Sample%20Output) folder contains:

| File | Description |
|---|---|
| `prediction_9b678890fb8ca401.npy` | NumPy tensor containing predicted neural activity |
| `events_9b678890fb8ca401.csv` | Event dataframe produced from the stimulus |
| `newplot.png` | Rendered cortical activity summary |
| `Screenshot 2026-06-24 214018.png` | Runtime or dashboard visual sample |
| `Screenshot 2026-06-24 214041.png` | Runtime or dashboard visual sample |
| `Screenshot 2026-06-24 214133.png` | Runtime or dashboard visual sample |

The prediction tensor can be loaded with NumPy:

```python
import numpy as np

preds = np.load("Sample Output/prediction_9b678890fb8ca401.npy")
print(preds.shape)
```

The event metadata can be loaded with Pandas:

```python
import pandas as pd

events = pd.read_csv("Sample Output/events_9b678890fb8ca401.csv")
events.head()
```

## Why This Project Is Technically Difficult

NeuroAd combines several hard problems that usually live in different systems:

- multimodal media preprocessing
- gated model authentication
- hosted GPU runtime stabilization
- high-dimensional neural tensor inference
- temporal event construction
- model output compression
- dashboard rendering under notebook constraints
- exportable artifacts for offline analysis

The project is difficult because it is not only about calling a model. The surrounding system has to make the model usable, reproducible, inspectable, and survivable inside constrained environments like Kaggle and Colab.

## Runtime Notes

TRIBE v2 inference is memory intensive. Audio-enabled clips are especially expensive because the audio extractor can allocate large intermediate tensors. Kaggle GPUs can run short clips, but longer videos with audio may hit CUDA out-of-memory errors.

Recommended operating modes:

- Kaggle: short clips, preferably 2-8 seconds for audio-enabled tests
- Colab L4/A100: longer and more stable inference
- Local GPU workstation: best for repeated experimentation and heavier media

## Suggested Use Cases

NeuroAd can be used as a prototype foundation for:

- pre-market creative scoring
- campaign attention diagnostics
- neural salience mapping
- overload-risk detection
- multimodal creative comparison
- ad-moment ranking
- experimental media intelligence
- ROI-calibrated neurocreative analytics

## Status

NeuroAd is an experimental research and product prototype. It does not claim to replace human-subject neuroscience, clinical measurement, or validated market testing. Its purpose is to explore a powerful idea: using state-of-the-art neural encoding models to create a new kind of pre-market creative intelligence layer.
