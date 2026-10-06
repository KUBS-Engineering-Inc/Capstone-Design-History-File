# Blood Flow Analysis Software: Project Documentation & Source of Truth

## 1. Background

### 1.1 Project Overview

The objective of this capstone project is to develop a graphical software application (GUI) for analyzing duplex Doppler ultrasound recordings to extract quantitative measurements of blood vessels and blood flow. The software will process ultrasound videos in bulk from a local folder, utilizing image-processing techniques for edge detection and signal processing for waveform analysis.

### 1.2 View Specifications

The software processes ultrasound recordings in two primary views, treating each video independently:

- **View 1 - Longitudinal:**
  - **Appearance:** Blood vessel appears as an elongated structure.
  - **Input Data:** B-mode and Doppler recordings.
  - **Measurements:** Perpendicular distance between vascular walls (vessel diameter). Doppler analysis to obtain blood velocity.
  - **Calculations:** Volumetric blood flow.
  - **Target:** Arterial blood vessels.
- **View 2 - Transverse:**
  - **Appearance:** Blood vessel appears as a circular structure/opening.
  - **Input Data:** B-mode recording only (Handle cases with no Doppler).
  - **Measurements:** Vessel-wall edge detection to determine cross-sectional area (CSA).
  - **Target:** Both arterial and venous blood vessels.

### 1.3 Scope & Extensions

- **Core Scope:** Full GUI with automated analysis of ultrasound video and manual human edits/refinements (with revision history keeping the original machine result). Must capture perpendicular diameter, blood velocity, blood flow, and CSA.
- **System Integration:** Integrate with custom vascular AI lab software (PhysioMerge) to replace the existing "Danny Green" software pipeline.
- **Potential Extensions / Bonus Capabilities:**
  - ECG processing using Pan-Tompkins algorithm to find R peaks (Explicitly marked as a bonus).
  - Intima-media thickness (vascular wall thickness) calculations.
  - M-mode support.
  - Middle envelope support for Doppler to classify monophasic, biphasic, and triphasic signals.
  - Calculation of morphological data from Doppler waveforms.

### 1.4 Disciplinary Focus

- **Software Engineering:** UI/UX design, requirements gathering for ultrasound data-processing workflows, handling user interactions, and responsive design.
- **Data Processing:** Research and apply image and signal processing algorithms to extract meaning from videos and Doppler waveforms.
- **Integration & Documentation:** Python integration with existing lab software, and thorough software documentation for requirements, feedback, and development stages.

---

## 2. Established Technical Facts (Agentic Extraction Format)

### 2.1 Hardware & Environment Constraints

- **Network:** Strictly Offline (System will never be hooked up to the internet).
- **Target Hardware:** NVIDIA rtxA5000 GPU and Xeon w-2245 CPU, 32 GB RAM.
- **Fallback Hardware:** Must support fallback for lower-end systems.
- **Language/Framework:** Python-based integration.

### 2.2 Input Data Specifications

- **Format:** Constant frame rate ultrasound video files (approx. 6 GB for 30 mins, 12 GB per person).
- **Visual Markers:**
  - **Scale:** Located on left/right sides. Depth/scale is dynamic and may be changed **mid-video** by the operator. The software must continuously read/track this via OCR. Scale might also be inverted (negative on top).
  - **Color Scale:** Red = blood flow/pulse (artery), Blue = slower/different direction (vein).
  - **ROI Indicator:** Green 'Z' box / bounding box indicates the starting target area. Search (BFS) for vessel walls around this box.
  - **Graphs:** Bottom graph contains Doppler (White line) and ECG (Green line).
- **Noise/Artifacts:** Recordings include patient movement (coughing, laughing, hyperventilating during hypoxia studies), mid-video depth changes, flickering, and the image occasionally going off-screen.

### 2.3 Image & Signal Processing Rules

- **Scale & Time Tracking:** Computer vision (OCR) required to dynamically track depth gradient scale and track the timeline from timestamps.
- **Tracking:** Must analyze dynamically looking forward in time across frames; the analyzed area shifts.
- **Edge Detection Requirements:**
  - Ultrasound image (vessel walls in both longitudinal and transverse views).
  - Bottom graph (waveforms & envelopes).
- **Angle Correction:** Arteries are sloped. Vertical pixel distance is incorrect for diameter; the algorithm must calculate angle-corrected diameter (must be parallel to the Doppler flow line).
- **Waveform Extraction:** Extract the waveform and find the upper, middle, and lower envelope of the Doppler signal.
- **Event Identification:** Identify systole (pulse up/peak) and diastole. Separate the ECG to detect R peaks.
- **UI States:** The interface must handle states for process, edit, pause, cancel, and undo.

### 2.4 Physiological & Anatomical Rules

- **Artery Characteristics:** High pressure, does NOT collapse when pressure is applied, sharper waveform peaks.
- **Vein Characteristics:** Low pressure, collapses under pressure, smoother waveform, giant jumble of noise in Doppler.
- **Anatomical Targets:** Focus on Common Carotid Artery (CCA).
- **Avoidance Zones:** Avoid imaging the bifurcation (split into interior and exterior carotid artery).
- **Hemodynamics (Windkessel Effect):** Large arteries absorb kinetic energy as elastic energy, reintroducing it later. CCA flow pattern differs from brain flow pattern.
- **Biphasic Model:** The system must account for positive and negative signal flipping (e.g., -120 at the top).

### 2.5 System Integration (PhysioMerge / PM)

- **Architecture Goal:** Transition from `Video -> Danny Green -> CSV -> PM` to a setup where PM utilizes our software.
- **Interaction Model:** The software will operate as a standalone service. PhysioMerge will call the software (e.g., via CLI), execute commands, and provide the data as necessary.
- **Existing PM Capabilities to Leverage:** Real-time CSV building, morphology calculations (per cardiac cycle), measurements (mean, systole, diastole), data deletion/filtering for messy signals, error correction via PM's `check` command.

### 2.6 Validation & Testing Baseline

- **Legacy Software Comparison:** Outputs will be tested against the "Danny Green" software.
  - _Note on Danny Green:_ Written in Fortran ("4tran"), capable of perpendicular diameter measurement, but **cannot** do cross-sectional area (CSA).
- **Test Data:** A specific test dataset with a ground truth is being designed. The UI prototype will initially be tested specifically on Flow-Mediated Dilation (FMD) video.
