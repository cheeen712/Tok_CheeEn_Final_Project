# Tok_CheeEn_Final_Project

## 1. Introduction

### Project Topic/Title
Spectral Dynamics of Cognitive Workload: EEG During Mental Arithmetic Tasks

### Introduction & Cognitive Mechanism
This project aims to explore **working memory** and **sustained attention** within human information processing. Serial subtraction is a typical high-cognitive-load task that requires the brain to temporarily store, retrieve, and repeatedly manipulate numerical information within working memory in a very short period of time while simultaneously filtering out external interference.

The central hypothesis of this project is that transitions from a relaxed resting state to a demanding mental arithmetic task lead to alterations in the power spectral density (PSD) of specific EEG frequency bands.

To investigate these neurophysiological changes, we primarily focus on two EEG indicators: **Frontal Midline Theta (4–8 Hz)** and **Parietal Alpha (8–12 Hz)**.

In cognitive neuroscience, these two spectral indicators have well-established relationships with cognitive processing:

- The enhancement of **Frontal Midline Theta** is considered a reliable biomarker of increased **working memory load**, **executive control**, and **cognitive resource allocation**, reflecting the engagement of frontal brain regions during demanding cognitive tasks.

- **Parietal Alpha** activity is often associated with cortical idling and inhibitory processes. During active information processing and focused attention, Alpha power tends to decrease, a phenomenon commonly referred to as **Event-Related Desynchronization (ERD)**.

Therefore, this project adopts the **Workload Index (Fz Theta / Pz Alpha)** as the primary workload metric to quantify changes in cognitive workload during mental arithmetic tasks.

For demonstration purposes, the present analysis focuses on **Subject 03**, a participant belonging to the **Good-performance group (Group G)** identified in the original dataset. The study compares EEG activity between resting-state and mental arithmetic conditions within this individual to illustrate the implementation and interpretation of EEG-based workload assessment.

---

## 2. Data Source & Technical Parameters

* **Data Source:** PhysioNet - *EEG During Mental Arithmetic Tasks (v1.0.0)*
* **URL:** [https://physionet.org/content/eegmat/1.0.0/](https://physionet.org/content/eegmat/1.0.0/)
* **Primary Citation:** Zyma I., Tukaev S., Seleznov I., Popov A., Chernykh M., Shpenkov O. (2019). *EEG During Mental Arithmetic Tasks*. PhysioNet. DOI: 10.13026/C2JQ1P
* **Platform Citation:** Goldberger A. L., Amaral L. A. N., Glass L., et al. (2000). *PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals*. Circulation 101(23):e215–e220.

### Recording Device & Technical Specs
* **Hardware / System:** Neurocom EEG 23-channel system (XAI-MEDICA, Ukraine).
* **Electrode Setup:** Ag/AgCl sintered electrodes, placement according to the International 10/20 system. Monopolar recording with interconnected ear reference electrodes.
* **Sampling Rate:** 500 Hz.
* **Hardware Filtering:** Built-in hardware filters including a low-pass (high-cut) filter at 30 Hz and a notch filter at 50 Hz.
* **Data Format:** EDF (European Data Format).

### Sample Size & Metadata
* **Participants:** 36 healthy subjects (mean age ≈ 21 years; 25 Female / 11 Male).
* **Performance Grouping:** Subjects were grouped by arithmetic performance (based on the number of correct subtractions per 4 minutes): Group B (Bad count quality, n = 12) vs. Group G (Good count quality, n = 24).

### Original Purpose
The dataset was originally collected to provide artifact-free EEG segments (60 seconds each) for investigating brain activity during mental arithmetic (serial subtraction). It was primarily designed to support comparative analyses of neural dynamics between low-performing and high-performing individuals under high cognitive load scenarios.

---

## 3. Data Preprocessing & Quality Control

The objective of this stage was to preprocess raw EEG signals to improve data quality and ensure reliable feature extraction for cognitive state analysis, particularly mental workload estimation. The preprocessing pipeline was implemented using **NeuroPype**.

### Visual Inspection of Raw EEG

Prior to preprocessing, raw EEG signals were visually inspected to identify potential artifacts and noise sources. The following issues were observed:

- **Baseline Drift:** Slow fluctuations likely caused by electrode movement or impedance changes.
- **High-Frequency Noise:** Rapid fluctuations possibly due to environmental electrical interference or muscle activity.
- **High-Amplitude Transients:** Sudden spikes that exceed typical EEG amplitude ranges and may distort spectral estimates.

These artifacts may negatively affect power spectral density (PSD) estimation and subsequent EEG feature extraction.

### Preprocessing Pipeline (NeuroPype)

The EEG preprocessing pipeline consisted of the following steps:

1. **Import EDF**  
   EEG data were imported from EDF files in the PhysioNet dataset.

2. **Separate Streams (EEG modality)**  
   EEG signals were isolated from other data streams.

3. **Stream Data**  
   EEG data were loaded into the processing pipeline.

4. **Dejitter Timestamps**  
   Timestamp irregularities were corrected to ensure temporal consistency.

5. **Assign Channel Locations**  
   Standard EEG montage was applied for spatial channel localization.

6. **Remove Unlocalized Channels**  
   Channels without valid spatial information were excluded.

7. **IIR Bandpass Filtering**  
   A Butterworth bandpass filter was applied to retain EEG signals within the relevant frequency range while attenuating low-frequency drift and high-frequency noise.

8. **Detrending**  
   Linear detrending was applied along the time axis to remove slow signal drifts.

9. **Decimation (2× Downsampling)**  
   The signal was downsampled by a factor of 2 to reduce computational load while preserving relevant EEG frequency information.

10. **Re-referencing**  
   Spatial re-referencing was applied to reduce reference-dependent variability across channels.

11. **Artifact Removal (AR)**  
   An artifact removal step with threshold = 15.0 was used to suppress high-amplitude non-physiological activity.

### Feature Extraction Preparation

After preprocessing, EEG signals were segmented using a **3-second moving window**. Power spectral density (PSD) was computed using the **multitaper method (TBWP = 2.5)**.

Average spectral power was calculated for the following frequency bands:

| Band | Frequency Range (Hz) |
|------|----------------------|
| Delta | 1–4 |
| Theta | 4–8 |
| Alpha | 8–12 |
| Beta  | 12–30 |
| Gamma | 30–50 |

These band powers were used for subsequent cognitive state analysis, including mental workload estimation and frontal EEG activity analysis.

### Quality Control Results

Visual inspection of preprocessed EEG data showed clear improvements in signal quality:

- Reduced baseline drift
- Suppressed high-frequency noise
- Reduced high-amplitude artifacts
- Enhanced visibility of rhythmic neural activity

These improvements indicate that the preprocessing pipeline effectively enhanced EEG signal quality for further analysis.

### NeuroPype Pipeline Overview

```text
Import EDF
↓
Separate Streams (EEG)
↓
Stream Data
↓
Dejitter Timestamps
↓
Assign Channel Locations
↓
Remove Unlocalized Channels
↓
IIR Bandpass Filter
↓
Detrending
↓
Decimation (2×)
↓
Re-referencing
↓
Artifact Removal (Threshold = 15.0)
↓
Moving Window (3 s)
↓
Power Spectrum (Multitaper, TBWP = 2.5)
↓
Frequency Band Averaging
```

Subject03_rest
<img width="1440" height="802" alt="截圖 2026-06-12 晚上9 31 40" src="https://github.com/user-attachments/assets/e2adeb5f-e8c4-4b83-add6-a1048309208f" />
Subject03_work
<img width="1440" height="798" alt="截圖 2026-06-12 晚上9 33 29" src="https://github.com/user-attachments/assets/6e6e6c94-9831-4835-bff4-b0a27dccfb47" />

---

## 4. Neurophysiological Feature Extraction

Following preprocessing, EEG spectral features were extracted to quantify neurophysiological changes associated with mental arithmetic. The same analysis procedures were independently applied to both the **resting-state** and **mental arithmetic** recordings.

### Mental Workload

Mental workload was estimated using the ratio proposed by Holm et al. (2009):

**Mental Workload = Theta(Fz) / Alpha(Pz)**
where:

- **Theta(Fz)** represents Theta-band power recorded at the frontal midline electrode **Fz**;
- **Alpha(Pz)** represents Alpha-band power recorded at the parietal electrode **Pz**.

Higher values of this ratio are generally interpreted as reflecting greater cognitive workload.

Feature extraction was implemented using the following NeuroPype operations:

#### Theta (Fz)

```
Select Range
[16 along space (indices)]

Select Range
[1 along frequency (indices)]
```

#### Alpha (Pz)

```
Select Range
[18 along space (indices)]

Select Range
[2 along frequency (indices)]
```

#### Workload Computation

```
Divide
[Theta(Fz) / Alpha(Pz)]
```

Higher values indicate increased cognitive workload.

---

### Frontal Theta Analysis

Frontal Theta activity was extracted to investigate task-related changes in executive processing and mental effort.

The frontal electrode cluster consisted of:

- Fp1 (index 0)
- Fp2 (index 1)
- F3 (index 2)
- F4 (index 3)
- F7 (index 4)
- F8 (index 5)
- Fz (index 16)

The following operations were performed:

```
Select Range
[[0, 1, 2, 3, 4, 5, 16] along space (indices)]

Select Range
[1 along frequency (indices)]

Sum
[over space, emitted as feature axis]
```

The resulting values were visualized using:

```
Bar Plot
['Frontal_theta']
```

Higher frontal Theta power is generally associated with increased cognitive control and mental workload.

### Frontal Alpha Analysis

Frontal Alpha activity was extracted using the same frontal electrode cluster:

- Fp1 (index 0)
- Fp2 (index 1)
- F3 (index 2)
- F4 (index 3)
- F7 (index 4)
- F8 (index 5)
- Fz (index 16)

The following operations were performed:

```
Select Range
[[0, 1, 2, 3, 4, 5, 16] along space (indices)]

Select Range
[2 along frequency (indices)]

Sum
[over space, emitted as feature axis]
```

The resulting values were visualized using:

```
Bar Plot
['Frontal_alpha']
```

Task-related decreases in Alpha power may reflect enhanced attentional allocation and cortical activation.

###  Feature Extraction Workflow

```text
Frequency Band Averaging
↓
├─ Mental Workload Branch
│    ├─ Fz (Index 16) → Theta
│    ├─ Pz (Index 18) → Alpha
│    └─ Divide (Theta / Alpha)
│
├─ Frontal Theta Branch
│    ├─ Frontal Cluster
│    ├─ Theta Selection
│    └─ Sum Across Channels
│
└─ Frontal Alpha Branch
     ├─ Frontal Cluster
     ├─ Alpha Selection
     └─ Sum Across Channels
```

The extracted features were subsequently used to compare resting-state and arithmetic-task conditions.
