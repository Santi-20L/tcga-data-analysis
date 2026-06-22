# TCGA Clinical Data Analysis — Exploratory Analysis and Survival Insights

Exploratory data analysis (EDA) of clinical data from The Cancer Genome Atlas (TCGA), a landmark cancer genomics program that has molecularly characterized over 20,000 primary cancer samples spanning 33 cancer types.

This project applies Python-based data analysis tools to extract patterns and insights from real-world clinical oncology data, covering patient demographics, diagnosis, treatment, and survival outcomes.

---

## Objectives

- Clean and preprocess raw TCGA clinical data
- Explore patient demographics and diagnosis distributions across cancer types
- Identify patterns in survival outcomes (overall survival, disease-free survival)
- Visualize key clinical variables and their relationships
- Generate actionable insights from the data

---

## Repository Structure

```
tcga-clinical-analysis/
├── notebooks/
│   ├── 01_data_cleaning.ipynb        # Data loading, cleaning, preprocessing
│   ├── 02_exploratory_analysis.ipynb # EDA: distributions, demographics, patterns
│   └── 03_survival_insights.ipynb    # Survival analysis and key findings
├── src/
│   └── utils.py                      # Reusable helper functions
├── data/
│   └── README.md                     # Data source and download instructions
├── results/
│   └── plots/                        # Output visualizations
├── requirements.txt                  # Python dependencies
├── .gitignore
└── README.md
```

---

## Dataset

**Source**: [GDC Data Portal — TCGA](https://portal.gdc.cancer.gov/)

TCGA clinical data includes:
- Patient demographics (age, gender, ethnicity)
- Diagnosis information (cancer type, stage, histology)
- Treatment data (surgery, radiation, chemotherapy)
- Survival outcomes (overall survival, days to death/last follow-up)

---

## Analysis Pipeline

### 1. Data Cleaning (`01_data_cleaning.ipynb`)
- Load raw clinical TSV files from GDC portal
- Handle missing values and inconsistent formatting
- Standardize column names and data types
- Export clean dataset for downstream analysis

### 2. Exploratory Analysis (`02_exploratory_analysis.ipynb`)
- Distribution of cancer types and subtypes
- Patient age and gender distributions
- Stage at diagnosis across cancer types
- Treatment patterns and frequencies
- Correlation analysis between clinical variables

### 3. Survival Insights (`03_survival_insights.ipynb`)
- Overall survival distributions by cancer type
- Kaplan-Meier survival curves
- Factors associated with survival outcomes (age, stage, treatment)
- Key clinical insights and findings summary

---

## Dependencies

```bash
pip install -r requirements.txt
```

| Package | Purpose |
|---------|---------|
| pandas | Data manipulation and cleaning |
| numpy | Numerical computing |
| matplotlib | Static visualizations |
| seaborn | Statistical data visualization |
| plotly | Interactive visualizations |
| lifelines | Survival analysis (Kaplan-Meier) |
| jupyter | Notebook environment |

---

## Usage

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/tcga-clinical-analysis.git
cd tcga-clinical-analysis

# Install dependencies
pip install -r requirements.txt

# Download TCGA clinical data from GDC portal
# Place files in data/ folder

# Run notebooks in order
jupyter notebook notebooks/01_data_cleaning.ipynb
```

---

## Results

**Cohort**: 1,036 TCGA-BRCA patients (1,025 female, 11 male), median age in the late 50s.

### Stage and Diagnosis Distribution

![Stage and Diagnosis](results/plots/stage_diagnosis_distribution.png)

Most patients were diagnosed at Stage II, with Infiltrating duct carcinoma as the predominant histological subtype (~71% of cases) — consistent with established breast cancer epidemiology.

### Mortality by Stage

![Mortality by Stage](results/plots/mortality_by_stage.png)

Mortality increases with stage at diagnosis, from ~4-9% in early stages (IA-IIB) to ~78% in Stage IV. Stage IIIB showed a higher-than-expected mortality rate, likely due to its small sample size (n=23) rather than a genuine biological effect.

### Survival Analysis: Early vs Advanced Stage

![Kaplan-Meier by Stage Group](results/plots/kaplan_meier_by_stage_group.png)

Kaplan-Meier curves show a clear separation in overall survival between early-stage (I-II, n=742) and advanced-stage (III-IV, n=235) patients. A log-rank test confirmed this difference is statistically significant (p = 3.53e-06).

### Cox Proportional Hazards Model

![Cox Forest Plot](results/plots/cox_forest_plot.png)

A Cox model quantified the independent contribution of age and stage to mortality risk:

| Variable | Hazard Ratio | p-value | Interpretation |
|----------|-------------|---------|-----------------|
| Age | 1.04 | < 0.005 | +4% risk per year of age |
| Advanced stage (III-IV) | 2.65 | < 0.005 | 2.65× higher risk vs early stage |

Concordance index: **0.74**. Stage at diagnosis emerged as a substantially stronger predictor of mortality than age, reinforcing the clinical value of early detection.

---

## Author

**Santi Isgrò**
BSc in Computer Science — Università degli Studi di Catania
MSc in Bioinformatics — in progress

---

## License

MIT License
