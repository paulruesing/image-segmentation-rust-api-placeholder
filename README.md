# Film Impurity Removal — Native Desktop Application (Rust)

> **Privacy notice:** This repository is a public placeholder. The full source code remains
> private as this is an ongoing freelancing engagement. I am happy to walk through the
> architecture and code in a private session upon request — feel free to reach out at
> pr@paulruesing.de.

---

## What this project is

A native desktop application for **automated detection and inpainting of image artefacts
**. Built end-to-end as a freelance project for an imaging technology client.

The system combines neural-network-based confidence heatmaps with adaptable, area-wise filtering
and deterministic non-AI inpainting, wrapped in a real-time GUI with an interactive layer-compositing canvas.

---

## Key ingredients

### Inference
- **Ensemble model architecture** — multiple specialised models targeting distinct
  artefact types, merged at inference time for robust joint detection
- **Runtime-optimised inference** via ONNX Runtime (cross-platform) and CoreML
  `.mlpackage` (Apple Silicon / Intel Mac)
- **Resolution-adaptive preprocessing** — input scaling is adjusted to balance sensitivity and inference cost

### Detection filtering
- **Adaptive filtering** — detections are filtered through a multi-threshold
  confidence pipeline, suppressing noise while retaining genuine artefacts
- **Area-wise sensitivity control** — the operator configures per-region detection
  aggressiveness directly on the canvas without requiring re-inference

### Inpainting
- **Deterministic non-AI inpainting** using classical computer vision methods,
  bounded strictly to detected regions — no generative model, no hallucination risk

### Application architecture
- **Native Rust** — no Python runtime required at inference time
- **Real-time rendering** via egui GUI with a layer-compositing canvas
- **Background threading** — inference and processing run off the main thread;
  the GUI remains responsive throughout

---

## Stack

| Layer | Technology |
|---|---|
| Language | Rust (stable ≥ 1.85) |
| GUI | egui / eframe |
| ML inference | ONNX Runtime (`ort`), CoreML (macOS) |
| Image processing | OpenCV 4.x |
| Build system | Cargo |

---


## Companion repository

This application consumes models trained and exported by a companion Python ML pipeline
(also private), which covers synthetic data augmentation, training, checkpoint
validation, and model export. A public placeholder for that repository is
available separately.

---

## Authors

Paul Rüsing — [pr@paulruesing.de](mailto:pr@paulruesing.de) — sole contributor  
Developed for an imaging technology client (ongoing engagement).

## License

All rights reserved by the client. Source code not included in this repository.
