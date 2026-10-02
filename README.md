# MOV-AAD: Multimodal Auditory Attention Dataset

[![Award](https://img.shields.io/badge/🏆_Award-Best_Student_Paper_@_INTERSPEECH_2026-ffd700.svg?style=for-the-badge)](https://interspeech2026.org)
<br>

[![WEB-Page](https://img.shields.io/badge/Project-Page-blue.svg)](https://mov-aad.github.io)
[![Google Drive](https://img.shields.io/badge/Google_Drive-Access_Upon_Request-e65c00.svg)](https://drive.google.com/open?id=19D0o1WT7R7lDVCC-l7-WhYWsGXVYqpaS&usp=drive_fs)
[![Hugging Face](https://img.shields.io/badge/🤗_HuggingFace-Uploading_/_In_Prep-FF8577.svg)](https://huggingface.co/datasets/naplabdataset/mov-aad)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-green.svg)](https://creativecommons.org/licenses/by/4.0/)

Official repository for **MOV-AAD**, a large-scale multimodal dataset designed for investigating selective auditory attention decoding (AAD), spatial audio localization, and cross-modal peripheral physiological tracking during dynamic, naturalistic conversations with moving sound sources.


---

## 🎬 10-Minute Walkthrough Video

<div align="center">
  <a href="https://www.youtube.com/watch?v=PbIi4rVktc0" target="_blank" title="Watch MOV-AAD Walkthrough on YouTube">
    <img src="https://img.youtube.com/vi/PbIi4rVktc0/maxresdefault.jpg" alt="MOV-AAD Video Walkthrough" style="width: 50%; max-width: 520px; border-radius: 8px; border: 1px solid #e1e4e8; box-shadow: 0 2px 8px rgba(0,0,0,0.06); display: block;">
  </a>
  <p style="margin-top: 8px; font-size: 0.9rem;">
    ▶️ <a href="https://www.youtube.com/watch?v=PbIi4rVktc0" target="_blank"><b>Click to Watch Full 10-Min Walkthrough on YouTube</b></a>
    <br>
    <small style="color: #666;">(Covers experimental paradigm, multimodal sensor alignment, and baseline demonstrations)</small>
  </p>
</div>

---

## 📜 Citation

If you use MOV-AAD in your research, please cite our **Interspeech 2026** paper:

```bibtex
@inproceedings{mov_aad_2026,
  title     = {MOV-AAD: A Large-Scale Multimodal Dataset for Auditory Attention Decoding During Moving Conversations},
  author    = {He, Xiaomin and Choudhari, Vishal and Spratt, Tristan J. and Raghavan, Aarya and Lee, Richard T. and Mesgarani, Nima},
  booktitle = {Interspeech 2026},
  year      = {2026}
}
```


---

## 📊 Dataset At A Glance

| **10** Synchronized Modalities | **1200 Hz** Unified Sampling Rate | **50** Healthy Subjects |
| :--- | :--- | :--- |
| 64-ch EEG, Gaze, Pupil, Respiration Airflow, Respiration Effort, GSR, PPG, SpO₂, Temperature, Motion | Fully aligned across all neural & physiological data streams | Age 24 ± 4.5 years, verified normal hearing status |

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
* **Pupil Dilation:** Binocular measurements captured at 60 Hz via `Tobii Pro Nano` and upsampled with aligned temporal interpolation to 1200 Hz.
* **Gaze Location:** Screen-coordinate gaze tracking (X and Y axes) mapped to screen size (display dimensions: $52 \times 32\text{ cm}$, viewing distance: roughly 60 cm to account for natural posture variation), recorded at 60 Hz and unified to 1200 Hz.
* **Respiration Flow:** Nasal airflow monitoring.
* **Respiration Effort:** Thoracic expansion belt (chest) tracking.
* **GSR:** Galvanic skin response.
* **PPG:** Raw optical photoplethysmography waveform.
* **Heart Rate:** Derived beat-by-beat heart rate extracted from raw PPG streams.
* **SpO₂:** Peripheral oxygen saturation monitoring.
* **Temperature:** Skin temperature monitoring, recorded from the dorsal surface of the non-dominant hand.
* **Accelerometer:** Triaxial motion tracking sampled at 1200 Hz, mounted on the chair back to capture gross body and seat vibrations.

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
│   │   └── ...
│   └── stimulus/                    # Stimuli used in the localization task
│
├── repeated_sentence/               # Repeated Sentence Task
│   ├── recordings/                  # Subject-level recordings for the repeated-sentence task
│   │   ├── sub-001.*
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

## 💻 Download & Access

Because of the massive scale of the multi-channel recordings, the full dataset archive is hosted externally across dedicated data repositories.

### 📦 Access Channels

* **Google Drive (Primary Archive — Controlled Access)**  
  * **Link:** [Google Drive Master Archive](https://drive.google.com/open?id=19D0o1WT7R7lDVCC-l7-WhYWsGXVYqpaS&usp=drive_fs)
  * **Access Note:** Click **Request Access** on Google Drive. Access requests are approved manually in accordance with our institutional governance protocol. You can download the complete archive or select specific task folders (`SC/`, `MC/`, `localization/`, `repeated_sentence/`) as needed.

* **Hugging Face Hub (In Preparation)**  
  * **Link:** [`naplabdataset/mov-aad`](https://huggingface.co/datasets/naplabdataset/mov-aad)
  * **Access Note:** Dataset upload is currently in progress. Direct CLI and programmatic loading via Hugging Face will be supported upon completion.

