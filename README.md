# fault-diagnosis
CWRU Bearing Faults Classification

## 🔍 Introduction & Dataset Overview

This project focuses on **Mechanical Fault Diagnosis** using vibration signal analysis. The dataset utilized is derived from the benchmark 
**Case Western Reserve University (CWRU) Bearing Data Center Dataset**, which is widely recognized as the industry standard for evaluating machine health monitoring and fault detection algorithms.

### Key Characteristics of the Dataset:
* **Signal Source:** Vibration data collected from accelerometer sensors under various motor loads (e.g., Load 1).
* **Sampling Rate:** 48 kHz sampling frequency (`48k`).
* **Segmentation:** Signals segmented into windows of 2048 samples (`2048`).
* **Extracted Features:** Statistical time-domain features extracted from the vibration signals, including:
  * **Basic/Amplitude Stats:** `max`, `min`, `mean`
  * **Dispersion/Energy Stats:** `sd` (Standard Deviation), `rms` (Root Mean Square)
  * **Distribution Shape Stats:** `skewness`, `kurtosis`
  * **Dimensionless/Waveform Stats:** `crest` factor, `form` factor
* **Target Classes (`fault`):** Various bearing fault conditions (such as ball faults, inner/outer race faults) alongside normal operating states.


# Fault Diagnosis Pipeline

A comprehensive machine learning pipeline for mechanical fault diagnosis using time-domain vibration signal features. 
This repository demonstrates a modular, production-ready approach from exploratory data analysis to model tuning, deployment simulation, and artifact management.

---

## 📁 Project Structure

fault-diagnosis
├── 01_eda.ipynb            # Data exploration, distributions, correlation analysis, and class balance checks
├── 02_baseline_models.ipynb # Initial comparison of untuned models (Logistic Regression, RF, LightGBM, XGBoost, DNN)
├── 03_tuning.ipynb         # Hyperparameter optimization using RandomizedSearchCV and best parameter selection
├── 04_final_pipeline.ipynb # Retraining the best model on full data and serializing artifacts using joblib
├── 05_test_joblib          # Verification and testing of the saved joblib model against dataset samples
├── src/                    # Reusable Python modules (preprocessing pipelines, evaluation metrics, etc.)
├── models/                 # Storage directory for saved .joblib model artifacts
└── README.md               # Project documentation and workflow overview

🚀 Project Workflow & Approach
Exploratory Data Analysis (01_eda.ipynb):

Inspected dataset structure, checked for missing values, and verified duplicate entries.

Analyzed target class distribution to confirm a well-balanced dataset.

Performed correlation and statistical analyses to understand feature relationships (e.g., strong multicollinearity between sd and rms).

Baseline Model Evaluation (02_baseline_models.ipynb):

Benchmarked multiple classification algorithms (Logistic Regression, Random Forest, LightGBM, XGBoost, and a Deep Neural Network) without hyperparameter tuning.

Identified Random Forest and LightGBM as the top-performing architectures.

Hyperparameter Tuning (03_tuning.ipynb):

Applied RandomizedSearchCV on the selected top models to optimize hyperparameters and improve cross-validation accuracy.

Final Model & Deployment Simulation (04_final_pipeline.ipynb & 05_test_joblib):

Retrained the optimized model pipeline on the full dataset.

Serialized the model using joblib inside the models/ directory and successfully tested inference using the saved artifact.

📊 Results & Key Findings
Baseline Performance: Random Forest and LightGBM achieved strong initial accuracies (~96% to 97%).

Tuned Performance: Hyperparameter tuning stabilized cross-validation performance around ~95.9%.

Feature Insights: Vibration features such as standard deviation (sd) and root mean square (rms) showed high correlation, while others like mean and skewness provided unique independent signals.

🛠️ Tech Stack
Python

Pandas & NumPy (Data Manipulation)

Scikit-Learn (Preprocessing & Machine Learning Models)

LightGBM & XGBoost (Gradient Boosting)

Seaborn & Matplotlib (Data Visualization)

Joblib (Model Serialization)

💡 What We Learned
Modularizing reusable functions into the src/ directory drastically reduces code duplication across notebooks.

Balanced multi-class fault datasets allow accuracy and macro-averages to be reliable performance indicators.

Proper pipeline serialization ensures seamless transition from experimentation to inference testing.
