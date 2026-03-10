# MASLD Risk Prediction Calculator

An interactive web-based calculator for predicting the risk of **Metabolic Dysfunction-Associated Steatotic Liver Disease (MASLD)** using simple anthropometric measurements.

🔗 **Live Demo:** [https://ehealth-lab.github.io/MASLD-calculator/](https://ehealth-lab.github.io/MASLD-calculator/)

---

## Overview

This calculator implements a logistic regression model trained on **UK Biobank** imaging data (n = 27,397) and externally validated on **NHANES 2017–2023**. It predicts MASLD risk using five derived anthropometric indices — requiring only age, sex, height, weight, waist circumference, and hip circumference as inputs.

MASLD was defined as hepatic steatosis (MRI-PDFF ≥ 5%) with at least one cardiometabolic risk factor, following the 2023 multi-society Delphi consensus nomenclature.

## Model Details

| Item | Detail |
|------|--------|
| **Algorithm** | Logistic Regression (L2-regularized) |
| **Training cohort** | UK Biobank, n = 27,397 |
| **External validation** | NHANES 2017–2023 |
| **Outcome** | MRI-PDFF–defined MASLD |
| **Internal AUC** | 0.84 |
| **Features** | Age, WHR, WHtR, ABSI, RFM |

### Feature Definitions

| Feature | Formula | Description |
|---------|---------|-------------|
| **WHR** | Waist / Hip | Waist-to-hip ratio |
| **WHtR** | Waist / Height | Waist-to-height ratio |
| **ABSI** | Waist(m) / [BMI^(2/3) × Height(m)^(1/2)] | A Body Shape Index |
| **RFM** | 64 − 20 × Height/Waist (male) <br> 76 − 20 × Height/Waist (female) | Relative Fat Mass |

## Input Requirements

| Parameter | Unit | Typical Range |
|-----------|------|---------------|
| Age | years | 18–100 |
| Height | cm | 100–220 |
| Weight | kg | 30–250 |
| Waist circumference | cm | 50–180 |
| Hip circumference | cm | 50–180 |
| Sex | Male / Female | — |

## Usage

### Online

Visit the [live calculator](https://ehealth-lab.github.io/MASLD-calculator/) — no installation required.

### Local

Download `index.html` and open it directly in any modern browser. The calculator runs entirely client-side with no server dependencies.

## Risk Stratification

| Predicted Probability | Risk Level |
|-----------------------|------------|
| < 20% | Low |
| 20–40% | Moderate |
| 40–60% | High |
| ≥ 60% | Very High |

## Methodology

1. **Cohort construction:** UK Biobank participants with valid MRI-PDFF, excluding excessive alcohol intake (> 20 g/day for women, > 30 g/day for men), viral/autoimmune hepatitis, other chronic liver diseases, and pregnancy.
2. **Feature selection:** Ten candidate anthropometric features were evaluated; Pearson correlation-based collinearity removal (|r| > 0.8) retained five independent predictors.
3. **Training:** SMOTE oversampling for class balance, StandardScaler normalization, hyperparameter tuning via 5-fold cross-validation.
4. **Validation:** External validation on NHANES 2017–2023 with sensitivity analyses across multiple CAP thresholds (≥ 248, ≥ 275, ≥ 300 dB/m).

## Disclaimer

This calculator is intended for **research and educational purposes only**. It should not be used as a substitute for professional medical advice, diagnosis, or treatment. Clinical decisions should always be made in consultation with qualified healthcare providers.

## Citation

If you use this tool in your research, please cite:

> *[Manuscript in preparation]*

## License

This project is open-source under the [MIT License](LICENSE).

## Contact

For questions or collaboration inquiries, please open an [issue](https://github.com/ehealth-lab/MASLD-calculator/issues) on this repository.
