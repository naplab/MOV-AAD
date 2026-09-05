# MOV-AAD: Multimodal Auditory Attention Dataset

[![WEB-Page](https://img.shields.io/badge/Project-Page-blue.svg)](https://mov-aad.github.io)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-green.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Data-Sampling](https://img.shields.io/badge/Sampling--Rate-1200_Hz-orange.svg)]()

Official repository for **MOV-AAD**, a large-scale multimodal dataset designed for investigating selective auditory attention decoding (AAD), spatial audio localization, and cross-modal peripheral physiological tracking during dynamic, naturalistic conversations with moving sound sources.

---

## 📊 Dataset At A Glance

| **9** Synchronized Modalities | **1200 Hz** Unified Sampling Rate | **50** Healthy Subjects |
| :--- | :--- | :--- |
| 64-ch EEG, Gaze, Pupil, Respiration, GSR, PPG, SpO₂, Temp, Motion | Fully aligned across all neural & physiological data streams | Age 24 ± 4.5 years, verified normal hearing status |

| **~75 Min** Total Duration | **4** Distinct Tasks | **Rich** Behavioral Tracking |
| :--- | :--- | :--- |
| Massive continuous recording per participant for AAD modeling | From structured validation to naturalistic conversations | Active repeated-word detection & precise localization reports |

---

## 🛠️ Experimental Paradigms & Data Composition

The dataset encompasses four sequential experimental tasks per participant, transition from structured sensory validation to ecologically valid, naturalistic listening scenarios:

1. **Repeated Sentence Task (120 trials):** A baseline neural reliability check featuring shuffled short sentences repeated without background noise to evaluate within-subject response consistency.
2. **Localization Task (54 trials):** A spatial perception task conducted prior to the main experiment to familiarize participants with spatial cues and assess their localization accuracy.
3. **Single-Conversation Task (40 trials):** An active listening task where participants track naturalistic, continuous conversational narratives from a single dynamically moving sound source.
4. **Multi-Conversation Task (56 trials):** A selective attention task requiring participants to attend to one target conversational stream while ignoring a competing co-spatial distractor.

### Parameters Summary Matrix

| Task / Condition | Experimental Purpose | Stimuli & Speakers | Spatial Configuration | Background Noise | Total Stimuli / Duration | Available Modalities |
| :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **Repeated Sentence Task** | Split-half & odd-even reliability check | 6 short sentences (shuffled); 3M/3F talkers | Diotic presentation (None) | None | 120 trials<br>`(~12 min)` | ✓ EEG & Physio<br>✓ Behavioral |
| **Localization Task** | Familiarize spatial cues & assess perception accuracy | Independent short sentences; Single talker/trial | Static; 9 coordinates (-90° to +90° in 22.5° steps) | None | 54 sentences<br>`(Short segments)` | - No Neural<br>✓ Behavior Metrics |
| **Single-Conversation Task** | Track neural tracking of speech with spatial change | Continuous dialogue context; Multi-turn talkers | HRTF-based dynamic moving (-90° to +90°); RMS-matched | Diotic pedestrian/babble noise (-9, -12 dB) | 40 trials<br>`(~30 min)` | ✓ EEG & Physio<br>✓ Behavior & Audio |
| **Multi-Conversation Task** | Evaluate selective Auditory Attention Decoding (AAD) | Two parallel stories; Continuous context & turn-taking | Two independent HRTF sources moving dynamically within ±90° | Diotic pedestrian/babble noise (-9, -12 dB) | 56 trials<br>`(~45 min)` | ✓ EEG & Physio<br>✓ Behavior & Audio |

---

## 🔬 Recording Modalities Specification

All signals were synchronously recorded and streamed through **g.tec HIamp** and a **Simulink GUI** at **1200 Hz**, with a hardware 60 Hz notch filter applied during acquisition.

* **EEG:** 64 channels, 1200 Hz high-density neural recordings via `g.tec g.HIamp`.
* **Pupil Dilation:** Binocular measurements captured at 60 Hz via `Tobii Pro Nano` and upsampled with aligned temporal interpolation to **1200 Hz**.
* **Gaze Location:** Screen-coordinate gaze tracking (X and Y axes) mapped to screen size, recorded at 60 Hz and unified to **1200 Hz**.
* **Respiration Flow:** Nasal airflow monitoring sampled at 1200 Hz.
* **Respiration Effort:** Thoracic expansion belt tracking sampled at 1200 Hz.
* **GSR:** Galvanic skin response sampled at 1200 Hz.
* **PPG:** Raw optical photoplethysmography waveform sampled at 1200 Hz.
* **Heart Rate:** Derived beat-by-beat heart rate extracted from raw PPG streams (1200 Hz).
* **SpO₂:** Peripheral oxygen saturation monitoring sampled at 1200 Hz.
* **Temperature:** Skin temperature monitoring sampled at 1200 Hz.
* **Accelerometer:** Triaxial head motion tracking sampled at 1200 Hz.

---

## 📂 Dataset Directory Structure

The released dataset is organized **by experimental task**. The four task folders are arranged in parallel, with task-specific recordings and stimuli stored together. For the conversation tasks, each subject recording file contains all trials from that task for the participant, including the synchronized neural, physiological, and behavioral modalities.

```directory
MOV-AAD/
├── SC/                              # Single-Conversation Task
│   ├── recordings/                  # One subject file per participant; all SC trials and synchronized modalities
│   │   ├── sub-001.*
│   │   ├── sub-002.*
│   │   └── ...
│   └── stimulus/
│       ├── audio/                   # Trial-level audio presented during SC
│       └── trajectory/              # Trial-level source-motion trajectories
│
├── MC/                              # Multi-Conversation Task
│   ├── recordings/                  # One subject file per participant; all MC trials and synchronized modalities
│   │   ├── sub-001.*
│   │   ├── sub-002.*
│   │   └── ...
│   └── stimulus/
│       ├── audio/                   # Trial-level target/distractor audio used during MC
│       └── trajectory/              # Trial-level source-motion trajectories
│
├── localization/                    # Localization Task
│   ├── recordings/                  # Subject-level behavioral response recordings
│   │   ├── sub-001.*                # Localization choice responses
│   │   ├── sub-002.*
│   │   └── ...
│   └── stimulus/                    # Stimuli used in the localization task
│
├── repeated_sentence/               # Repeated Sentence Task
│   ├── recordings/                  # Subject-level recordings for the repeated-sentence task
│   │   ├── sub-001.*
│   │   ├── sub-002.*
│   │   └── ...
│   └── stimulus/                    # Repeated-sentence stimuli
│
├── preprocessing_scripts/           # Preprocessing and alignment scripts
├── README.md
└── dataset_info.json
```

### Organization Notes

* **Task-first organization:** Data are grouped by experimental task rather than by participant.
* **SC and MC recordings:** Each subject file contains that participant's complete set of trials for the corresponding conversation task, with all available synchronized modalities stored together.
* **Conversation stimuli:** Audio and source trajectories are stored under each conversation task's `stimulus/` directory so that each trial can be paired with the exact presented stimulus and motion path.
* **Localization task:** The released subject recordings contain the behavioral localization responses, corresponding to the participant's multiple-choice spatial reports, together with the task stimuli.
* **Repeated Sentence task:** Subject recordings and the corresponding repeated-sentence stimuli are stored within the same task-level structure.

---

## 🛠️ Preprocessing & Data Alignment Notes

To ensure high data reproducibility, the released dataset provides clean, aligned pipelines processed as follows:

* **EEG Artifact Handling & Channel Interpolation**
    * EEG channels exhibiting abnormal cross-trial variance or high-frequency impedance spikes were automatically flagged.
    * Bad channels were reconstructed using **Spherical Spline Interpolation** (following standard `EEGLAB` procedures [Delorme & Makeig, 2004]).
    * *Note:* Peripheral modalities are released in a minimally processed form (hardware notch filtering only) to retain raw autonomic dynamics.

* **Trial Epoching & Windowing**
    * **Conversation Tasks (SC & MC):** Each continuous trial includes a **3-second pre-onset baseline** segment prior to speech onset.
    * **Baseline Period:** Vital for calculating trial-level neural entrainment, baseline normalization, or calculating time-frequency relative power.

* **Cross-Modal Temporal Realignment**
    * Primary sync was established via hardware trigger pulses routed simultaneously into the `g.tec` digital input channel.
    * Fine-grained temporal jitter was eliminated post-hoc via **cross-correlation analysis** between the recorded acoustic playback loop and the original master stimulus waveforms, ensuring sub-millisecond precision.

---

## 💻 Download & Usage (Get Dataset)

The dataset is distributed through a **Google Drive download link provided in this GitHub repository**. The GitHub repository contains the documentation, dataset metadata, and preprocessing code, while the full data archive is hosted externally on Google Drive because of its size.

### 📦 Download the Dataset

1. Open the [Google Drive Dataset Link](https://creativecommons.org/licenses/by/4.0/](https://drive.google.com/open?id=19D0o1WT7R7lDVCC-l7-WhYWsGXVYqpaS&usp=drive_fs) .
2. Download the complete dataset, or select only the task folders needed for your analysis.
3. Keep the task-level directory structure unchanged so that recordings can be matched directly to their corresponding stimuli and trajectories.

### 💾 Repository Usage

Clone this repository to obtain the README, dataset metadata, and preprocessing scripts:

```bash
git clone https://github.com/mov-aad/mov-aad.github.io.git
cd mov-aad.github.io
```

After downloading the dataset from the linked Google Drive, place or mount the dataset at a location accessible to your analysis environment. The preprocessing scripts can then be applied to the task-specific recordings using the released directory structure described above.

---

## 📜 Citation

If you use the **MOV-AAD** dataset, synchronized multimodal recordings, behavioral measurements, stimuli, trajectories, or released preprocessing code in your academic work, please cite the associated **Interspeech 2026** paper.

```bibtex
@inproceedings{mov_aad_2026,
  title     = {MOV-AAD: A Large-Scale Multimodal Dataset for Auditory Attention During Moving Conversations},
  author    = {Author list to be updated},
  booktitle = {Proceedings of Interspeech 2026},
  year      = {2026}
}
```

The final author list, page numbers, DOI, and official proceedings metadata can be updated here once the Interspeech 2026 bibliographic record is available.
