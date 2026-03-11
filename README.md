# MASLD Risk Calculator

A web-based screening tool for **Metabolic Dysfunction-Associated Steatotic Liver Disease (MASLD)** using a validated MLP Neural Network model. No laboratory tests or imaging required — only routine anthropometric measurements.

🔗 **Live Calculator**: [your-username.github.io/masld-calculator]( https://ehealth-lab.github.io/MASLD-calculator/)

---

## Overview

This calculator implements a machine learning model developed to support community-based MASLD screening using five simple anthropometric-derived features. The model was trained on the UK Biobank cohort using MRI-derived proton density fat fraction (MRI-PDFF) as the imaging reference standard, and externally validated in an independent NHANES cohort.

| | Internal Validation (UK Biobank) | External Validation (NHANES) |
|---|---|---|
| **Cohort size** | 35,548 | 5,900 |
| **AUC** | 0.828 (95% CI: 0.818–0.839) | 0.833 |
| **Sensitivity** | 0.776 | 0.765 |
| **F1 Score** | 0.547 | 0.730 |
| **Brier Score** | — | 0.170 |

---

## Model Details

| Parameter | Value |
|---|---|
| Algorithm | MLP Neural Network |
| Hidden layer | 1 layer, 50 neurons |
| Activation (hidden) | tanh |
| Activation (output) | logistic (sigmoid) |
| Optimal threshold | 0.367 (Youden's J) |
| Reference standard (training) | MRI-PDFF ≥ 5% |
| Reference standard (validation) | CAP ≥ 238 dB/m |

**Input features** (in order of SHAP importance):

1. **WHtR** — Waist-to-Height Ratio *(dominant predictor)*
2. **ABSI** — A Body Shape Index
3. **Height** (cm)
4. **RFM** — Relative Fat Mass
5. **Age** (years)

All derived indices are calculated automatically from raw measurements entered by the user.

---

## Usage

### Online (recommended)

Visit the live calculator at the link above. Enter the following measurements:

- Age (years)
- Sex
- Height (cm)
- Weight (kg)
- Waist circumference (cm)
- Hip circumference (cm)

The calculator will automatically derive WHtR, ABSI, and RFM, run the model, and display the estimated MASLD probability with a risk classification.

### Local

Clone the repository and open `index.html` in any modern browser:

```bash
git clone https://github.com/your-username/masld-calculator.git
cd masld-calculator
open index.html
```

No installation, server, or internet connection required. All model parameters are embedded directly in the HTML file.

---

## Derived Index Formulas

| Index | Formula |
|---|---|
| WHtR | Waist (cm) / Height (cm) |
| ABSI | [Waist (m)] / [BMI^(2/3) × Height (m)^(1/2)] |
| RFM (Male) | 64 − (20 × Height / Waist) |
| RFM (Female) | 76 − (20 × Height / Waist) |
| BMI | Weight (kg) / Height (m)² |

---

## Data Sources

- **UK Biobank** — Large-scale prospective cohort (n ≈ 500,000), accessed under Application Number 1155908. MRI-PDFF measurements obtained through the dedicated imaging sub-study. Ethics approval: North West Multi-Centre Research Ethics Committee (Ref: 11/NW/0382).

- **NHANES** — National Health and Nutrition Examination Survey, cycles 2017–March 2020 and August 2021–August 2023. Publicly available from the [NCHS website](https://www.cdc.gov/nchs/nhanes). MASLD defined by CAP ≥ 238 dB/m via transient elastography.

---

## Citation

If you use this tool in your research, please cite:

```
[Author names]. Anthropometric indices-based machine learning for interpretable 
MASLD screening: development and external validation in UK Biobank and NHANES. 
[Journal]. [Year]. DOI: [xxx]
```

---

## Disclaimer

This tool is intended for **research and educational purposes only**. It does not constitute medical advice, diagnosis, or treatment. Clinical decisions should be made by qualified healthcare professionals based on comprehensive patient evaluation. The authors accept no responsibility for clinical decisions made on the basis of this tool.

---

## License

MIT License — free to use, modify, and distribute with attribution.

---

## Contact

For questions or feedback, please open an issue or contact the corresponding author at [email].
