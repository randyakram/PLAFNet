# PLAF-Net

## 1. Overview
 
PLAF-Net (Phase-Location Attention Fusion Network) is a hierarchical attention model for binary classification of myocardial infarction (MI) vs. normal from multi-site phonocardiogram (PCG) recordings. It is intended as a **complementary screening / decision-support signal**, not a replacement for standard MI diagnosis (clinical, ECG, biomarker, imaging evidence). The model applies attention first across the four cardiac phases (S1, systole, S2, diastole) within each auscultation clip, then across the four auscultation locations (Apex, RUSB, LUSB, LLSB), to produce a single patient-level MI prediction score, while enforcing strict patient-level separation during evaluation to avoid data leakage.

## 2. Data provenance and governance
 
- **Source:** PCG recordings were collected in collaboration with Dr. Hasan Sadikin General Hospital, Bandung, and Universitas Padjadjaran, together with Telkom University.
- **Cohort size:** 140 subjects (70 MI, 70 normal). Each subject contributed one 30-second recording from each of four auscultation locations (Apex, RUSB, LUSB, LLSB) at a 4 kHz sampling rate, divided into six non-overlapping 5-second clips per recording — 560 recordings and 3,360 clips total.
-  **Ethics approval:** Approved by the Health Research Ethics Committee of Universitas Padjadjaran, approval number **LB.02.01/X6.5/75/2022**.
-  **Data availability:** The code and datasets used and/or analyzed during the current study are available from the corresponding author on reasonable request. Contact: Satria Mandala, mandalasatria@gmail.com or Randy Akram, randy.pdr@gmail.com
-  **Funding:** Directorate of Research, Technology, and Community Service, Ministry of Education, Culture, Research, and Technology of the Republic of Indonesia (Grant No. 283/C3/DT.05.00/PLBARU/2026 and No. 1609/LL4/PG/2026)

## 3. Data splits
 
- **Overall split:** 140 patients were divided *before model development* into a 112-patient development cohort (80%) and a 28-patient independent holdout (20%), at the patient level. The holdout was excluded from all preprocessing decisions, model selection, hyperparameter selection, threshold selection, and checkpoint selection.
- **Development cross-validation:** 5-fold `StratifiedGroupKFold` within the development cohort, grouped by patient ID so all recordings from one patient stay in the same fold. Within each outer-training fold, ~15% of patients formed a subject-disjoint internal validation set for early stopping (this is a nested split inside the development cohort, distinct from the main 80:20 split).

## 4. Reproducibility plan
 
- **Code:** Full training and evaluation pipeline provided in `PLAFNet.ipynb` and `PLAFNet_Inference.ipynb`.
- **Random seeds:** 21, 42, 84, used consistently for both development CV and final retraining (`REAL_SEEDS = (21, 42, 84)`).
- **Data access:** The full 140-patient dataset is **not** publicly distributed due to patient privacy. Per the paper's data availability statement, it is available from the corresponding author (mandalasatria@gmail.com or randy.pdr@gmail.com).
- **Data path:** Notebooks currently reference local absolute paths (e.g. `DATA_DIR = "E:/Research"`, `CSV_PATH = "E:\notebook\hyperparameter_search_log.csv"`).

## 4. Citation
 
Mandala S, Akram RR, Pramudyo M, Utomo WH. PLAF-Net: Hierarchical Explainability at the Cardiac-Phase and Auscultation-Location Levels for Leakage-Resilient Myocardial Infarction Detection from Multi-Site Phonocardiograms
