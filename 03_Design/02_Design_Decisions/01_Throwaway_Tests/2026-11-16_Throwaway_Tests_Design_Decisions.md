# Throwaway Tests: Design Decisions

**Date:** 2026-11-16
**Source:** module READMEs in [Capstone-Throwaway-Tests](https://github.com/KUBS-Engineering-Inc/Capstone-Throwaway-Tests) (`modules/<module>/README.md`)

> **Full details are in the related repository.** The throwaway test code and each test's complete design decisions live in [Capstone-Throwaway-Tests](https://github.com/KUBS-Engineering-Inc/Capstone-Throwaway-Tests), in each module's `README.md` (Design Decision section). This document is a summary; read the module READMEs for the full reasoning, results and how to run each test.

---

## Why Throwaway Tests

In Milestone 2 the highest-risk algorithms were tested first with throwaway code, so that problems which would force a design change surface in fall rather than winter ([Fall Work Breakdown](../../../00_Admin/Project_Plan/2026-10-02_Fall_Work_Breakdown.md#milestone-mapping)).

- Each test is a small, separate module that checks whether one approach is feasible on our own recordings. The goal is to learn what works, not to write production code.
- Tasks marked "M2 → M3" in the work breakdown are a throwaway spike in M2, then a prototype in M3. Successful spikes are turned into prototypes; the code itself is not meant to be kept.
- All tests use classical image processing (OpenCV, and Tesseract for OCR). Machine learning was ruled out for now because it needs labelled training data that we don't have.
- Every module has a README with How to Run, What it Does and Design Decision sections. This document summarizes the Design Decision sections.

## Overview

| Test | Module | Task | Owner | Main decision |
| --- | --- | --- | --- | --- |
| Segment display windows | `segment_windows` | F7 | Seaya | Identify the layout with OCR, then crop with fixed coordinates plus contour detection |
| Read the scales (OCR) | `scale_ocr` | D1, L1 | Kyle | OCR only inside fixed per-layout regions, not the whole screen |
| Doppler waveform and envelope | `doppler_waveform` | D2 | Ursula | Grayscale threshold; envelope = uppermost pixel per column |
| ECG trace and R-peaks | `ecg` | D3 | Ursula | Green-dominance mask; R-peak candidates with `find_peaks` |
| Perpendicular diameter | `measure_diameter` | L3, L4 | Seaya | Search for the lumen at the Doppler cursor instead of detecting walls |
| Circular vessel detection | `detect_circular_vessels` | T1 | Baoze | Contour threshold sweep scored on shape and wall contrast, not Hough circles |
| Frame extraction | `extract_frames` | — (supports the others) | Baoze | Save original frames named by their index in the video |

Not covered yet: the Doppler timeline test (D4) has no module in the repo.

---

## Segment Display Windows (F7)

- **Layout first, then crop.** OCR reads the footer to identify the display mode (B-only, spectral or M-mode). Stable regions use configured coordinates; the B-mode box, whose width changes with depth, is found with contour detection.
- **Alternatives rejected:** temporal variance between frames (window sizes and positions change between display modes) and a YOLO model (needs manually labelled training data).
- **B-mode scale from the depth ticks.** The crop's top and bottom are aligned with the known depth ticks; with the OCR-read depth this gives centimeters per pixel.
- **Open:** validate the depth-scale calculation against known measurements; consider passing bounding-box coordinates downstream instead of saving crop files.

## Read the Scales with OCR (D1, L1)

- **Fixed regions instead of searching the whole screen.** Detecting digits anywhere would pick up look-alikes from the B-mode image, Doppler spectrum, ECG, settings text and buttons. The scanner places each scale in the same spot for a given layout, so OCR runs only on cropped regions.
- **Separate regions per layout.** The depth scale covers about half the screen height in the spectral view and the full height in the B-mode only view (about 72 vs 146 px per cm for the same 0–4 cm scale). The spectral view also has a velocity axis.
- **Results:** depth and velocity scales read on both sample frames; the depth fit agrees with the "Depth 4 cm" settings readout.

## Doppler Waveform and Envelope (D2)

- **Grayscale thresholding:** the trace is bright on a dark background, so no colour detection is needed. A 2 × 2 opening removes speckle.
- **Envelope = uppermost detected pixel in each column**, since the target is the upper boundary of the spectrum.
- **Only short gaps are interpolated** (up to 5 columns). Longer gaps and edge gaps stay `NaN`, and detected, interpolated and missing columns are tracked separately.
- **Pixel coordinates only;** conversion to time and velocity is left to the scale and timeline work.

## ECG Trace and R-Peaks (D3)

- **Colour-dominance mask:** the trace is green, so pixels must exceed a green threshold and be greener than red and blue. Only the ECG region is analysed.
- **Coverage safeguard:** the ECG is accepted only if at least 70% of columns contain green pixels.
- **R-peak candidates:** median-filtered series, inverted so upward spikes become maxima, then `find_peaks` with prominence, spacing and width limits; each candidate is refined on the unsmoothed series.
- **Limits:** candidates are image-based, not clinically validated. The intended two-peak safeguard is defined but not yet enforced in the code.

## Perpendicular Diameter (L3, L4)

- **Use the Doppler cursor as a search anchor.** Where the cursor crosses the insonation line narrows the lumen search.
- **Lumen instead of walls.** Detecting continuous vessel walls directly was unreliable because of image variation and irregular boundaries; the lumen is a larger, more robust target.
- **Intersection from fitted lines.** Masking the beam and taking the midpoint of the remaining strokes was inaccurate for small cursors; the current method fits the insonation line and intersects it with the beam.
- **Open:** a threshold sweep shows how candidates change with intensity, but choosing a threshold needs more data and a defined error metric. Lumen vs wall detection should be compared further.

## Circular Vessel Detection (T1)

- **Contour over Hough.** Both were tried on the same frames. Hough circles land on the vessel but lock onto the bright wall and don't fit the lumen, so they fail the lumen checks (0 of 4 sample images); the contour method outlines the lumen (score 0.84 on the transverse artery).
- **Threshold sweep.** One darkness cutoff either misses part of the lumen or merges it with nearby tissue, and the right cutoff changes between frames, so every level from 10 to 90 is tried.
- **Scoring on shape and wall contrast.** The highest-scoring outline is kept; a bright wall ring around a dark lumen is what separates a vessel from other round dark regions.
- **Other details:** colour flow counts as lumen and on-screen overlays are removed; ovals are accepted (aspect ≥ 0.4); images are resized to a fixed 300 px working size.
- **Limits:** the outline sits slightly inside the true wall, so sizes read small; small round structures in longitudinal views can pass (score about 0.6); results are in pixels.

## Frame Extraction (supporting)

- **OpenCV only**, already used by every other module.
- **Frames named by their original index** (`frame_000030.jpg`), so any result traces back to its time in the recording (index / frame rate).
- **Frames are skipped, never interpolated**, when sampling at a lower rate; every saved image is a real frame.
- **JPEG by default** (about 3× smaller than PNG); PNG is available when exact pixels matter.

---

## Revision History
| Date | Version | Changes |
| --- | --- | --- |
| 2026-11-16 | 0.1 | Initial summary of throwaway test design decisions from the module READMEs |
| 2026-11-16 | 0.2 | Noted that the full design decisions and test code are in Capstone-Throwaway-Tests |
