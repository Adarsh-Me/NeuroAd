# NeuroAd Technical Summary

NeuroAd is a multimodal neural-response analytics prototype for advertising and campaign media. It operationalizes Meta's TRIBE v2 brain-encoding model as a creative-intelligence engine, transforming videos, images, and audio stimuli into predicted cortical activity and NeuroAd-specific diagnostic telemetry.

## Conceptual Thesis

Advertising analytics is usually downstream, behavioral, and delayed. NeuroAd pushes the analysis upstream. It asks whether a creative asset can be interrogated as a neural stimulus before market deployment, producing a structured approximation of how the asset may distribute salience, memory pressure, affective valence, and cognitive load over time.

In practical terms, NeuroAd turns campaign media into a temporally indexed neuro-response object.

## System Architecture

The notebook pipeline is organized into five layers:

1. **Runtime substrate**  
   GPU-enabled notebook execution with explicit dependency control for Colab and Kaggle.

2. **Model substrate**  
   TRIBE v2 loading through gated Hugging Face authentication and compatibility handling for hosted notebook environments.

3. **Stimulus substrate**  
   Media normalization for video, image, and audio inputs, including conversion utilities that make non-video assets ingestible by the TRIBE event pipeline.

4. **Inference substrate**  
   TRIBE event construction, multimodal feature extraction, brain-response prediction, caching, and export.

5. **Interpretability substrate**  
   NeuroAd proxy metrics, cortical heat summaries, timeline plots, frame-level creative labeling, and Gradio-based inspection.

## NeuroAd Proxy Signals

The dashboard derives campaign-facing signals from predicted BOLD response tensors:

- **Attention Capture**: high-percentile absolute activation intensity across time
- **Memory Encoding**: positive-response intensity used as a coarse memory-pressure proxy
- **Emotional Valence**: lateralized activation contrast transformed into a directional score
- **Cognitive Load**: dispersion and temporal-change pressure used to flag overload conditions

These are not clinical measurements. They are operational heuristics designed to make high-dimensional neural predictions usable for creative diagnostics.

## Novelty

The central novelty is the compression of neural encoding outputs into an advertising-native decision interface. Instead of displaying raw model outputs, NeuroAd maps predicted cortical activity into the vocabulary of campaign review: salience, overload, emotional approach, memory trace strength, and frame-level creative risk.

This creates a bridge between computational neuroscience and creative strategy.

## Kaggle And Colab Compatibility

The notebook includes explicit handling for hosted-notebook instability:

- Kaggle secrets support for `HF_TOKEN`
- Colab secrets support for `HF_TOKEN`
- pinned Torch/Torchvision CUDA wheel strategy
- Transformers and Hugging Face Hub compatibility pins
- Torchvision import guards for Kaggle operator-registration failures
- Gradio API schema workaround for Kaggle runtime combinations
- lightweight visualization fallback to avoid kernel crashes
- short audio/video smoke tests to avoid VRAM exhaustion

## Practical Constraints

TRIBE v2 inference is memory intensive. Audio-enabled clips are especially expensive because the audio extractor can allocate large intermediate tensors. On Kaggle-class GPUs, short clips are recommended. Full-length campaign analysis should run on larger GPU hardware such as L4, A100, or equivalent infrastructure.

## Research And Product Potential

NeuroAd can become the foundation for:

- pre-market creative scoring
- campaign moment detection
- overload-risk analysis
- neural telemetry benchmarking
- multimodal ad comparison
- automated creative editing recommendations
- ROI-calibrated neurocreative intelligence

The long-term product direction is a campaign brain lab: a system where creative teams upload stimulus assets and receive time-resolved neural-response diagnostics before media spend is committed.

## Artifact

Primary artifact:

- [`Notebook/neuroad.ipynb`](Notebook/neuroad.ipynb)

Supporting documentation:

- `README.md`
- `SUMMARY.md`
- Kaggle launch: https://www.kaggle.com/code/adarshm12/neuroad
