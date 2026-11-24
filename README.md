# Sammie-Roto for NukeX (`nuke-sammie-roto`)

A native **Foundry NukeX 17** integration porting the multi-stage video segmentation and temporal matting pipeline of [Sammie-Roto 2](https://github.com) directly into a feature-film compositing environment.

> **Status:** Architecture & Inference Decoupling Phase  
> **Target Environment:** Foundry NukeX 17.x (Python 3.11+ / PySide6 / CUDA)

---

## Why This Tool?
While single-frame segmentation models exist for Nuke, feature-film rotoscoping and extraction require **temporal consistency** and **hair/motion-blur edge fidelity**. Sammie-Roto 2 solves this by chaining interactive point/box segmentation (**SAM 2.1 / EfficientTAM**) into dedicated temporal video matting (**MatAnyone2 / VideoMaMa**).

This project brings that multi-model pipeline natively into NukeX 17, upgrading it for high-resolution, linear-light VFX production plates.

## Key Production Upgrades Over Standalone GUI
1. **32-Bit Linear EXR & ACES 2.0 Pipeline:** Bypasses 8-bit compressed video intermediaries by ingesting Nuke plate buffers directly via OpenImageIO/NumPy with OCIO-aware dynamic range compression for ML inference.
2. **4K+ Feature Plate Support:** Tile-based and region-of-interest (RoI) inference strategies to handle anamorphic and large-format cinema plates within standard workstation VRAM limits.
3. **Interactive Nuke Viewer Prompts:** Place positive/negative tracking points and bounding boxes directly in the Nuke Viewer using a PySide6 overlay, feeding coordinates straight to SAM 2.1.
4. **Native Nuke Outputs:** Outputs clean `alpha` mattes, foreground despilled/unpremultiplied plates, and optional vectorized **RotoPaint** Bézier splines for manual artist refinement.

## Roadmap
- [x] Pipeline architecture & decoupling of Sammie-Roto 2 inference workers from standalone Qt UI
- [ ] Isolated Python/CUDA inference backend (`sam2`, `matanyone2`) communicating over local IPC/ZeroMQ
- [ ] NukeX 17 PySide6 Dockable Panel & Viewer Point-Prompt Overlay
- [ ] Direct `RotoPaint` spline contour extraction (`_curveknob` API)
- [ ] Optional `.cat` (Cattery) TorchScript packaging for lightweight single-model nodes

## Author
Developed by a Senior Feature Film VFX Compositor (30+ years production experience) building practical, artist-driven ML tools for Nuke.

## License
Apache-2.0 / MIT (aligned with upstream model weights and dependencies).
