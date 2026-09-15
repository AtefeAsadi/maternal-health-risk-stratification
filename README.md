# Maternal Health Risk Stratification

This project examines maternal health risk using six clinical measurements: age, systolic blood pressure, diastolic blood pressure, blood sugar, body temperature, and heart rate.

The aim was to study differences between Low Risk, Mid Risk, and High Risk groups and to evaluate a simple Logistic Regression model. Because this is a health related classification problem, the analysis focuses on Recall and class performance rather than Accuracy alone.

The project is intended for research and educational purposes. It is not a clinical diagnostic tool.

## Data

The dataset contains 1,014 observations.

During the data quality assessment, no missing values were found. Two observations with a HeartRate value of 7 bpm were removed because the values were considered implausible.

A large number of repeated rows were also found. Since patient identifiers were not available, it was not possible to confirm whether identical rows represented the same patient. For the primary analysis, exact repeated rows were removed, leaving 451 observations.

A detailed discussion of these decisions is available in the **Data Quality Assessment** section of the notebook.

## Exploratory Analysis

The clinical variables were compared across the three risk groups.

Blood sugar showed the strongest difference between High Risk observations and the other groups. Systolic and diastolic blood pressure also showed clear differences.

Standardized mean differences were used so that variables measured on different scales could be compared.

Blood sugar had the largest absolute standardized difference, approximately 1.61.

See the **Exploratory Analysis** and **Standardized Mean Difference** sections of the notebook for the full results and figures.

## Model

A multiclass Logistic Regression model was used as the main baseline.

The predictors were standardized inside a Pipeline, and the data were divided into training and test sets using a stratified 80 percent and 20 percent split.

The main test results were:

- Accuracy: 0.670
- Macro F1: 0.511
- High Risk Recall: 0.565
- Mid Risk Recall: 0.048
- Low Risk Recall: 1.000

These results show that overall Accuracy does not fully describe model performance.

See the **Model Evaluation** section of the notebook for the classification report and confusion matrix.

## Error Analysis

The most important errors were High Risk observations predicted as Low Risk.

All 10 missed High Risk observations were classified as Low Risk.

Their mean blood sugar value was approximately 7.35 mmol/L, compared with 12.81 mmol/L among correctly identified High Risk observations.

This suggests that High Risk cases without strongly elevated blood sugar were more difficult for the model to identify.

More details are available in the **Error Analysis** section.

## Sensitivity Analysis

Because repeated observations were an important data quality issue, a second analysis was performed without removing them.

A five fold Stratified Group Cross Validation procedure was used so that identical predictor profiles could not appear in both training and test data.

The average results were:

- Accuracy: 0.607
- Macro F1: 0.593
- High Risk Recall: 0.695
- Mid Risk Recall: 0.330
- Low Risk Recall: 0.777

The results show that model performance depends partly on how repeated observations are handled.

The full comparison is available in the **Sensitivity Analysis** section of the notebook.

## Main Finding

Blood sugar was the strongest descriptive predictor of High Risk and also had the largest positive Logistic Regression coefficient for that class.

The model performed well for Low Risk observations but had difficulty identifying Mid Risk cases and some High Risk cases.

The project also shows that data preparation decisions can affect conclusions about model performance.

## Limitations

The main limitations are the small number of predictors, the lack of patient identifiers, repeated observations, inconsistent labels for some identical clinical profiles, and the absence of an independent validation dataset.

For a complete discussion, see the **Clinical Interpretation and Limitations** section of the notebook and the report.

## Repository

```text
maternal_health_risk_stratification/
│
├── README.md
├── requirements.txt
├── data/
│   └── README.md
├── notebooks/
│   └── maternal_health_risk_analysis.ipynb
├── figures/
└── report/
    ├── maternal_health_risk_report.pdf
    └── maternal_health_risk_short_summary.pdf
Reproducibility

Install the required packages with:

python -m pip install -r requirements.txt

Then open notebooks/maternal_health_risk_analysis.ipynb and run the cells from the beginning.