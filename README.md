# EEG Motor Movement Imagery Classification

## Overview

This project processes EEG data from the [EEG Motor Movement/Imagery Dataset](https://physionet.org/content/eegmmidb/1.0.0/) to classify different motor imagery tasks using classical machine learning models (SVM and Random Forest).

---

## Contents

- **Data Loading and Preprocessing:**  
  Loads raw `.edf` EEG files, renames channels to standard names, sets montage, extracts events from annotations, and creates epochs around events for each subject and run.

- **Feature Extraction:**  
  Epoch data is converted into numpy arrays and flattened into feature vectors suitable for classical ML models.

- **Classification:**  
  Implements Support Vector Machine (SVM) and Random Forest classifiers on the EEG epochs to distinguish between motor imagery classes (`rest`, `left fist`, and `right fist`).

---

## Code Breakdown

- `custom_rename(ch_name)`:  
  Renames EEG channels to standard naming conventions for compatibility with MNE montages.

- `process_run(edf_path, task_type)`:  
  Loads and preprocesses EEG data for a single run:
  - Reads EDF file with MNE.
  - Renames channels and applies standard 10-05 montage.
  - Extracts events and epochs.
  - Returns epoch data (`X`) and labels (`y`).

- **Data Iteration Loop:**  
  Loops over multiple subjects (`S001` to `S009`) and runs (`R01` to `R13`), loading and processing each run's EEG data and collecting epoch data.

- **Machine Learning:**  
  - Concatenates all epoch data and labels across subjects and runs.
  - Flattens EEG epochs into 2D feature vectors.
  - Splits dataset into train/test sets with stratification.
  - Trains and evaluates SVM and Random Forest classifiers.
  - Prints classification reports and accuracy scores.

---

## Dependencies

- Python 3.9+
- [MNE](https://mne.tools/stable/index.html)
- numpy
- pandas
- scikit-learn
- matplotlib
- pyEDFlib

---

## How to Run

1. Install dependencies (preferably in a conda environment):
   ```bash
   conda create -n eeg_env python=3.10
   conda activate eeg_env
   conda install -c conda-forge mne numpy pandas matplotlib scikit-learn
   pip install pyEDFlib
