[README.md](https://github.com/user-attachments/files/34281686/README.md)
# Stress detection from wrist-worn wearable data

Code for my MSc dissertation at Queen Mary University of London (2026): can wrist signals identify stress in someone a model has never seen?

## Approach

- **Data:** public [WESAD](https://www.eti.uni-siegen.de/ubicomp/home/datasets/icmi18/) dataset, using wrist EDA, BVP and skin temperature from 15 participants. The dataset isn't included in this repository.
- **Windows:** 60 seconds with a 30-second step, giving 1,015 labelled windows.
- **Features:** 12 statistical features, extended to 18 with skin conductance, heart rate and HRV features.
- **Model:** Random Forest with 100 trees and balanced class weights.
- **Evaluation:** Leave-One-Subject-Out cross-validation.

## Results

| Signal | Baseline F1 | Extended F1 |
| --- | --- | --- |
| EDA | 0.370 | 0.474 |
| BVP | 0.232 | 0.557 |
| Skin temperature | 0.450 | 0.450 |
| Combined | 0.580 | 0.725 |

A random train/test split on one participant gave a perfect F1 of 1.00. This was caused by temporal leakage, as slowly drifting signals revealed the time in the session. The score fell to 0.58 when tested on unseen people.

## Limitations

The pipeline has only been tested on laboratory data, only Random Forest was evaluated, and the model failed completely for one participant (S14).

## Running it

1. Download the WESAD dataset from the link above and add `WESAD.zip` to your Google Drive.
2. Open `stress_detection.ipynb` in Google Colab and run the cells in order. Adjust the file paths if needed.

Libraries: NumPy, pandas, SciPy, scikit-learn, Matplotlib and seaborn.
