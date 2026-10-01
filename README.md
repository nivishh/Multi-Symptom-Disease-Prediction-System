# Multi-Symptom-Disease-Prediction-System
ML-powered web app that predicts diseases from symptoms using Random Forest and provides health insights, including medication, diet, exercise, and preventive recommendations.
Explainable Disease Risk Predictor

A symptom-based disease risk estimation system with explainability (SHAP) and honest model validation. Given symptoms entered by a user, it estimates the most likely conditions, shows probabilities, and explains which symptoms drove the result.

⚠️ Medical Disclaimer: This project is for educational purposes only. It is not a medical device and does not provide diagnosis, treatment or medical advice. Always consult a qualified healthcare professional.

Table of Contents
Overview
What's New vs. the Original Repo
Features
Dataset
Project Structure
Installation
Usage
Methodology
Results
Explainability
Limitations
Ethics
Roadmap
Acknowledgements
License
Overview

The original project predicts one of ~41 diseases from ~132 binary symptoms using a Random Forest and reports near-perfect accuracy. That is a warning sign: the underlying dataset is clean, synthetic-style and contains many duplicate rows, so a perfect score often indicates memorisation rather than real generalisation.

This project builds on that foundation and focuses on:

Honest evaluation: de-duplication, stratified splits, cross-validation and robustness tests.
Risk-style output: top-3 predictions with calibrated probabilities instead of a single "diagnosis".
Explainability: SHAP-based global and per-prediction explanations.
What's New vs. the Original Repo
Area	Original	This project
Output	Single diagnosis	Top-3 risk estimates with probabilities
Validation	Single split, ~100% accuracy	De-duplication, stratified train/val/test, 5-fold CV
Metrics	Accuracy	Macro F1, per-class precision/recall, confusion matrix, top-3 accuracy, calibration
Robustness	Not tested	Symptom-dropout and noise tests
Explainability	None	SHAP (global + local) compared with built-in feature importance
Framing	Diagnostic	Educational risk estimation with disclaimer
Features
Multi-class symptom-based prediction (Random Forest baseline plus model comparison)
Top-3 predictions with probabilities
SHAP explanations for each prediction
Symptom spell-correction for user input
Descriptions, precautions, medications, diets and workouts looked up from CSV files
Flask web app
Dataset
Source: Kaggle, Disease Prediction Using Machine Learning (the same CSVs are included in the dataset/ folder of the original repo).
Content: ~132 binary symptom columns, ~41 disease labels, plus supporting CSVs (description.csv, medications.csv, diets.csv, workout_df.csv, precautions_df.csv, Symptom-severity.csv).
Caveat: The data is synthetic-style, with many duplicate rows and no age, sex or lab values.

Place the files in the dataset/ folder (or download them from Kaggle and point the notebook to your path).

Project Structure
.
├── dataset/                  # Training.csv and supporting CSVs
├── model/                    # Saved model, label encoder, symptom list
├── templates/
│   └── index.html            # Web UI
├── main.py                   # Flask app
├── disease_prediction_system.ipynb   # Original baseline notebook
├── notebooks/                # EDA, model comparison, SHAP, calibration (add yours here)
├── requirements.txt
└── README.md

Adjust this tree to match your final layout.

Installation
bash
# 1. Clone your fork
git clone https://github.com/<your-username>/Disease-Prediction-and-Medical-Recommendation-System.git
cd Disease-Prediction-and-Medical-Recommendation-System

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
pip install shap
Running in Google Colab
python
from google.colab import drive
drive.mount('/content/drive')

!git clone https://github.com/<your-username>/Disease-Prediction-and-Medical-Recommendation-System.git
%cd Disease-Prediction-and-Medical-Recommendation-System
!pip install -r requirements.txt shap
Usage
Run the web app
bash
python main.py

Then open http://127.0.0.1:5000 in your browser, enter your symptoms, and view the top-3 risk estimates with SHAP explanations.

Reproduce the analysis

Run the notebooks in order:

EDA (shape, duplicates, class balance, symptom frequency, co-occurrence)
Cleaning and stratified split (70/15/15, fixed random_state)
Baseline and model comparison with 5-fold stratified CV
Tuning, evaluation, robustness tests
SHAP and calibration
Methodology
Data cleaning: remove duplicates, drop empty columns, normalise symptom names.
Splitting: stratified train/validation/test split before any other processing.
Baseline: reproduce the original Random Forest.
Model comparison: Logistic Regression, Decision Tree, Naive Bayes, Gradient Boosting, XGBoost, SVM, Random Forest.
Tuning: GridSearchCV or Optuna on the best two models.
Robustness: randomly drop 1–3 symptoms from test rows and/or add noise, then measure the drop in performance.
Calibration: CalibratedClassifierCV plus calibration curves.
Explainability: SHAP TreeExplainer.
Results

🚧 Fill this section in with your own numbers after running the experiments.

Model	CV Accuracy	Macro F1	Top-3 Accuracy
Random Forest (baseline)	TBD	TBD	TBD
Logistic Regression	TBD	TBD	TBD
Gradient Boosting	TBD	TBD	TBD
XGBoost	TBD	TBD	TBD

Key findings (to complete):

Accuracy before vs. after de-duplication: TBD
Performance when 1, 2, 3 symptoms are dropped: TBD
Calibration quality (Brier score / curve): TBD

Add plots here, for example:

markdown
![Confusion Matrix](images/confusion_matrix.png)
![Calibration Curve](images/calibration_curve.png)
Explainability

SHAP is used in two ways:

Global: which symptoms matter most across all predictions.
Local: why a specific user input led to a specific prediction (bar or waterfall plot shown in the app).

SHAP importance is also compared with the Random Forest's built-in feature importance, with notes on any differences.

Show Image

Limitations
Data is synthetic-style and heavily duplicated, so high scores may not reflect real-world performance.
No age, sex, medical history or lab values.
Symptoms are binary (present/absent) with no severity or duration modelled in the main pipeline.
No real patient records were used, and the model has not been clinically validated.
Outputs are probabilistic estimates, not diagnoses.
Ethics
Predictions must not replace professional medical advice.
Users should be clearly informed that results are educational estimates.
No personal health data is collected or stored by the app. Verify this if you deploy it.
Roadmap
 Use symptom severity as a feature or weight
 Add demographic and clinical features
 Evaluate on external or real-world data
 Deploy to Render or Hugging Face Spaces
 Add a Streamlit version
Acknowledgements

This project builds on the open-source Disease-Prediction-and-Medical-Recommendation-System repository and the Kaggle Disease Prediction Using Machine Learning dataset. Credit goes to the original authors. Replace this line with direct links to the original repo and dataset.

License

Specify your license here (e.g., MIT). Make sure it is compatible with the original repository's license.
