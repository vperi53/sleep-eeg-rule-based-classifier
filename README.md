
# Sleep EEG Rule-Based Classifier

This repository contains the full pipeline for EEG signal processing and rule-based sleep stage classification using the Sleep-EDF Expanded Dataset (2013). The framework includes preprocessing, amplitude and power feature extraction (Hilbert, Welch, STFT), and stage classification with validation via expert-annotated hypnograms.

SleepStageClassifier
Overview

SleepStageClassifier is a signal processing framework that automates sleep stage classification using full-night EEG recordings from the Sleep-EDF Database. Using frequency domain analysis, amplitude envelopes, and domain-specific thresholds, this rule-based system classifies EEG signals into standard AASM-defined stages: Wake, N1, N2, N3, and REM.

This project uses open-source libraries such as MNE, YASA, SciPy, and NumPy to process EEG recordings and generate hypnograms validated against expert annotations.

Features
EEG Preprocessing: Butterworth bandpass filtering and artifact mitigation.
Sleep Stage Classification: Rule-based system using Delta/Theta/Alpha dominance, ratios, and temporal smoothing.
Spectral and Temporal Analysis: Extracts Welch’s PSD, STFT-based spectrograms, and Hilbert amplitude envelopes.
Event Detection: Identifies spindles, K-complexes, and bursts using YASA’s detection API.
Full-Night Hypnogram Generation: Creates and validates sleep architecture using expert-labeled hypnograms.
Visualization: Stage-wise PSDs, amplitude tables, and frequency transitions plotted with Matplotlib.

Methodology
1. Data Source

Dataset: Sleep-EDF Expanded (2013)
Format: Polysomnographic (PSG) .edf recordings and expert-labeled hypnograms.
Channels Used: Fpz-Cz, Pz-Oz.
2. Preprocessing

Sampling Rate: 100 Hz
Filter: 0.5–30 Hz Butterworth
Segmentation: 30-second epochs
3. Feature Extraction

Welch’s PSD: Computes absolute/relative band power in Delta (0.5–4 Hz), Theta (4–8 Hz), Alpha (8–12 Hz) bands.
STFT: Short-Time Fourier Transform to detect time-varying spectral events.
Hilbert Transform: Instantaneous amplitude envelopes for sleep-related transient detection.
Spindle/K-Complex Detection: YASA’s rule-based detectors.
4. Classification

Rule-Based Classifier:
Delta power → N3
Spindles/K-complexes → N2
Theta dominance → N1
Mixed alpha → Wake
Smoothing: Majority voting across neighbors for robustness
Output: Hypnogram
5. Evaluation

Metrics: Accuracy, Cohen’s Kappa, Stage-wise F1 Scores
Compared against: Expert hypnograms from PhysioNet
📊 Results
Sleep Stage	Dominant Band	Classifier Accuracy
N3	Delta (0.5–4 Hz)	High (Delta Power Threshold)
N2	Spindles + Theta	Moderate
N1	Theta/Alpha	Moderate
REM	Mixed Theta + Bursts	Variable
Wake	Alpha	High


pip install -r requirements.txt
Run

jupyter notebook notebooks/analysis.ipynb
Requirements
requirements.txt:

numpy
scipy
mne
yasa
matplotlib
pandas
seaborn
scikit-learn
Usage
Place .edf files in data/edf/
Open analysis.ipynb and run all cells
View output:
Stage-wise power tables
Hypnogram plots
Rule-based classification logs
Future Work
Integration of event-based classifiers (e.g., spindle-based transition detection)
Use of additional EEG, EOG, EMG channels
Real-time implementation on wearable headbands
Comparison with deep learning models (e.g., SleepEEGNet)
Clinical testing on disordered populations (sleep apnea, insomnia)
- yasa
- numpy, scipy, pandas
- matplotlib, seaborn
- scikit-learn
- statsmodels

Install with:

```bash
pip install -r requirements.txt
# or
conda env create -f environment.yml

