# chromaFX - The RAW Editor

<p align="center">
  <img src="chromaFX.png" alt="chromaFX Logo" width="120">
</p>

> **Note:** chromaFX is currently in active development. Pre-release builds and downloads are not yet available.

chromaFX is a non-destructive and GPU-accelerated RAW image editor designed natively for Linux. It operates locally and functions entirely offline without user accounts or tracking.

---

## Overview

This software provides RAW image processing for Linux environments, combining a rendering engine with local image analysis tools and hardware controller compatibility. All processing takes place on the local machine.

### Core Architecture
* Local Operation: Face detection, object segmentation, and image analysis are executed offline using local CPU and GPU hardware.
* Data Processing: Built upon a linear light pipeline with GPU-accelerated operations.
* Data Privacy: No background telemetry, no account creation required, and no remote data transmission.

---

## Technical Features

### Local Analysis Engine
The software includes automated culling, sharpness detection, and object segmentation using MobileSAM ONNX and MediaPipe. The code functions without external cloud APIs.

### Hardware Control
The application supports class-compliant MIDI input. Sliders, exposure controls, and tone curves can be mapped to physical hardware controllers via a manual MIDI-Learn utility.

### Camera Connection and Stacking
The system supports camera connectivity via USB using gphoto2 for image import and bracketing sequences. Images can be aligned and combined locally using Pyramid-Blending algorithms for focus stacking.

---

## Feature Overview

### 1. Image Processing
* Color Pipelines: Linear light pipeline with a Gamma 2.2 approximation, Sigmoid highlight roll-off compression, and 3-way color grading (Shadows, Midtones, Highlights).
* Tone Mapping: Linear, Reinhard, Filmic/Hable, ACES, Drago, and Log-Neutral.
* Color Mixing: 8-channel HSL / Color Mixer, 8-hue weighted Black and White mixer, and Split Toning.
* Adjustments: Lensfun integration for distortion, vignetting, and chromatic aberration corrections. Includes perspective controls, auto-straightening, and a crop tool with 7 compositional overlays.
* Noise Reduction: Multi-scale sharpening alongside LAB-based OpenCV fastNlMeansDenoisingColored algorithms.

### 2. Layers and Masking
* Masking Selection: Brush masks (feather, opacity), linear/radial gradients, and luminance masks.
* Geometric Selections: Depth-based masking using Laplacian sharpness maps, atmospheric gradients, and Apple HEIC depth-data import, alongside a magnetic lasso tool.
* Object Masking: Segmentations for faces, people, edges, and objects.
* Restoration: Content-aware healing brush utilizing Poisson Blending, mask visualization overlays, and mask tracking across batch operations via ORB/ECC.

### 3. Digital Asset Management (DAM)
* Database: SQLite-driven catalog system with support for nested galleries, virtual copies, and rating systems.
* Filtering: Dynamic filters based on boolean logic rules (AND/OR, text matching, date ranges).
* Metadata Search: Full-text search across metadata fields, file names, and tags, with specific filters for ISO, camera body, and face detection status.
* Utilities: Duplicate detection via dHash, XMP sidecar export, and catalog backup tools with merge capabilities.

### 4. Performance and System Optimization
* Hardware Interfaces: OpenCL and CUDA execution via cv2.UMat and PyOpenCL.
* Code Execution: Just-In-Time (JIT) compilation using Numba for processing pipelines, combined with multi-threading via thread and process pools.
* Memory Management: Float16 memory compression for high-resolution files.
* Rendering: Background 1:1 preview generation during idle phases and progressive zoom rendering with Lanczos sharpening.

---

## Development Roadmap

### In Development
* Refine Edge Algorithm: Integration of Guided Filter technology for masking complex structures like hair or fur.
* Tethered Shooting UI: Development of an interface for direct camera triggering and live-view via gphoto2.
* Optimization: Refinement of NumPy and Numba pipelines for hardware configurations lacking AVX2 instructions.

### Planned
* Plugin Interface: Python API documentation to allow the creation of custom filters and export scripts.
* LUT Previews: A grid-based hover preview system for .cube files.
* Synchronization Options: Opt-in preset and smart collection synchronization via user-managed Nextcloud instances.

---

## Meta and Disclaimer

* Developer: Dominik Schrödel
* Target Platform: Linux

Disclaimer: This software is in the development phase. Pre-release builds are used at the user's own risk. The developer assumes no liability for data loss or hardware instability during use.
