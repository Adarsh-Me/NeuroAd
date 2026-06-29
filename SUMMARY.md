# NeuroAd Technical Summary

NeuroAd is a multimodal neural-response inference prototype for advertising media. It uses Meta TRIBE v2 as the core brain-encoding model and surrounds it with a practical product layer for media ingestion, hosted runtime compatibility, neural tensor export, visualization, and campaign-facing interpretation.

The system is best understood as a **media-to-cortical-telemetry pipeline**. A creative asset enters the notebook as a video, image, or audio file. NeuroAd converts that asset into model-compatible event sequences, runs TRIBE v2 inference, receives predicted cortical activity over time, and translates the output into interpretable signals for creative analysis.

## High-Level Objective

The goal is to transform ad evaluation from a purely behavioral, downstream workflow into a model-assisted, upstream diagnostic workflow. Rather than waiting for post-launch metrics, NeuroAd attempts to estimate how a media asset may distribute attention, memory pressure, emotional directionality, and cognitive load across time.

The product concept is a campaign brain lab: upload a creative stimulus, simulate a neural-response trace, inspect frame-level activation behavior, and export the result for deeper analysis.

## System Decomposition

NeuroAd contains six major subsystems.

### 1. Runtime And Environment Layer

This layer prepares the notebook execution environment. It defines cache directories, media directories, export directories, and detects hosted notebook behavior. The project was built to survive both Colab and Kaggle, which have different filesystem conventions, GPU availability patterns, and preinstalled dependency stacks.

Key responsibilities:

- create stable working paths
- configure cache, media, and export folders
- support Colab and Kaggle execution
- reduce repeated setup friction

### 2. Dependency And Compatibility Layer

This is one of the most important engineering parts of the project. TRIBE v2 depends on a sensitive stack involving PyTorch, Torchvision, Transformers, Hugging Face Hub, and other scientific packages. Kaggle and Colab frequently ship package versions that are not mutually compatible.

NeuroAd includes explicit handling for:

- CUDA-enabled Torch installation
- Torchvision schema registration problems
- missing `torchvision::nms` operator metadata
- Hugging Face Hub API drift
- Transformers version compatibility
- Gradio schema-route failures
- notebook kernel memory constraints

This turns the notebook from a fragile research artifact into a more reproducible runtime product.

### 3. Authentication Layer

TRIBE v2 access requires Hugging Face authentication and accepted gated-model terms. NeuroAd supports multiple credential paths:

- Kaggle Secrets
- Colab Secrets
- environment variables
- secure manual prompt fallback

This allows the same notebook to function across public hosted environments without hardcoding secrets.

### 4. Stimulus Construction Layer

The system normalizes campaign assets into model-ingestible stimuli. This layer handles:

- video inputs
- image-to-video conversion
- audio-to-video wrapping
- short media generation for Kaggle-safe tests
- event dataframe creation

The key artifact here is the event dataframe. It becomes the structured bridge between raw media and TRIBE v2 inference.

### 5. Neural Encoding Layer

The neural encoding layer loads TRIBE v2 and runs prediction over the event sequence. Its output is a high-dimensional tensor representing predicted cortical activity across timesteps and brain vertices.

Conceptually:

```text
stimulus media -> event dataframe -> TRIBE v2 -> predicted cortical response tensor
```

This tensor is the core technical output of the system.

### 6. Interpretability And Product Layer

Raw cortical tensors are not directly useful to a creative strategist or product evaluator. NeuroAd derives proxy metrics and visual summaries from the prediction tensor.

The project exposes:

- attention capture score
- memory encoding score
- emotional valence score
- cognitive load score
- overload-risk classification
- timeline visualization
- cortical activity summary
- event dataframe preview
- exportable NPY and CSV files

## Data Flow

The complete execution flow is:

1. User provides media or selects a sample asset.
2. Notebook normalizes the asset into an ingestible stimulus.
3. TRIBE event dataframe is created.
4. TRIBE v2 predicts cortical response over time.
5. Prediction tensor is cached and transformed.
6. NeuroAd derives proxy metrics from the tensor.
7. Visualizations are generated for inspection.
8. Artifacts are exported for downstream analysis.

## Sample Artifacts

The repository includes sample output artifacts in [Sample Output](Sample%20Output).

Included files:

- `prediction_9b678890fb8ca401.npy`: predicted neural activity tensor
- `events_9b678890fb8ca401.csv`: event metadata dataframe
- `newplot.png`: cortical activity visualization
- screenshot images showing runtime/dashboard output states

The sample output demonstrates that the notebook is not merely conceptual. It produces concrete artifacts that can be loaded, inspected, visualized, and used for subsequent experimentation.

## Technical Complexity

The project has meaningful complexity across several axes.

### Multimodal Complexity

The system has to reason over video, audio, and image inputs. These media types have different preprocessing needs, temporal structures, and memory costs.

### Model Complexity

TRIBE v2 is not a small classical ML model. It is a neural encoding system with gated model access, substantial dependency requirements, and heavy inference demands.

### Runtime Complexity

Hosted notebooks are volatile. They have preinstalled packages, limited GPU memory, notebook-specific process behavior, and inconsistent package resolver outcomes. NeuroAd includes compatibility patches because the target runtime is part of the engineering problem.

### Interpretation Complexity

Predicted cortical tensors are not naturally product-friendly. NeuroAd adds a conversion layer that turns dense model output into attention, memory, valence, and load proxies.

### Product Complexity

The project exposes an interactive workflow, exportable artifacts, and sample results. This makes it closer to a product prototype than a one-off model experiment.

## Why It Matters

NeuroAd points toward a new kind of advertising technology: neural-response-informed creative intelligence. The system does not simply classify an ad as good or bad. It tries to expose when a stimulus becomes salient, when it may overload viewers, when memory pressure increases, and where the creative timeline may contain stronger or weaker response moments.

That makes the project valuable as a technical demonstration of:

- applied neural encoding
- multimodal inference engineering
- hosted GPU deployment
- model-output interpretability
- creative analytics product thinking

## Repository Artifacts

Primary notebook:

- [Notebook/neuroad.ipynb](Notebook/neuroad.ipynb)

Sample outputs:

- [Sample Output](Sample%20Output)

Live Kaggle notebook:

- https://www.kaggle.com/code/adarshm12/neuroad

## Current Status

NeuroAd is a research-grade prototype. It is not a clinical neuroscience system and should not be interpreted as validated human-subject measurement. It is a technically ambitious proof of concept for applying neural encoding models to creative media analysis and pre-market campaign intelligence.
