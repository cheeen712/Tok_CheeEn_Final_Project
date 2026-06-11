# Tok_CheeEn_Final_Project
---

## 1. Introduction

### Project Topic/Title
Spectral Dynamics of Cognitive Workload:EEG During Mental Arithmetic Tasks

### Introduction & Cognitive Mechanism
This project aims to explore Working Memory and Sustained Attention within human information processing mechanisms. Serial subtraction is a typical high-cognitive-load task that requires the brain to temporarily store, retrieve, and repeatedly manipulate numerical information within working memory in a very short period of time, while simultaneously filtering out external interference. The core hypothesis of this project is: when subjects transition from a relaxed resting-state to a high-intensity mental arithmetic task, the synchronous firing patterns of their cortical neurons will change, subsequently leading to a significant spatial distribution shift in the power spectral density (PSD) of specific EEG frequency bands.

To verify this neurophysiological phenomenon, we will primarily extract and quantify two specific EEG indicators: the **frontal Theta band (4–8 Hz)** and the **parieto-occipital Alpha band (8–13 Hz)**.

In cognitive neuroscience, these two spectral indicators have a highly clear association with the brain's information processing:
* The power enhancement of **Frontal Midline Theta** is a reliable biomarker for increased "cognitive resource allocation" and "working memory load," reflecting the high activation of the prefrontal cortex during executive functions.
* **Parieto-Occipital Alpha** waves typically represent the brain in a relaxed or inhibited state. When the brain enters a state of active information processing and focus, the Alpha wave power in this region significantly decreases, a phenomenon known as "Event-Related Desynchronization (ERD)."

By jointly observing the "enhancement of Theta waves" and the "desynchronization of Alpha waves," we can accurately quantify the brain's resource allocation and cognitive workload state. Furthermore, we adopted the **Workload Index (Fz theta / Pz alpha)** as our core metric. By quantifying the ratio of these two spectral indicators, we can accurately observe the dynamic fluctuations of the subjects' cognitive workload during the execution of mental arithmetic tasks.

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

