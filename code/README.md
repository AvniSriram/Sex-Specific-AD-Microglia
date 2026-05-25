# Code

This folder contains the main analysis scripts used in the project. Both scripts were developed in Google Colaboratory but can also be run locally.

---

## Scripts

### `microglia_morphology.py`

Performs the full microglial morphometry and machine learning pipeline, including:

- Data loading and preprocessing
- Morphometric feature extraction
- Exploratory data analysis (EDA)
- PCA and clustering
- Supervised classification
- Sex-stratified statistical analysis

Addresses **RQ1** and **RQ2**.

---

### `behavioral_analysis.py`

Performs the 5-choice serial reaction time task (5CSRTT) behavioral analysis, including:

- Data cleaning and preprocessing
- Sex-stratified statistical testing
- Two-way ANOVA
- Summary statistics and visualization

Addresses **RQ3**.

---

# Pipeline Overview

## `microglia_morphology.py`

### 1. Data Loading

- Extracts compressed datasets from `data/`
- Loads `.swc` files from:
  - `AD_SWC/`
  - `Control_SWC/`
- Loads metadata CSV files from:
  - `AD_Metadata/`
  - `Control_Metadata/`

### 2. Feature Extraction

Uses `neurom==4.0.4` to extract 10 morphometric features per microglial cell:

| Feature | Description |
|---|---|
| `soma_volume` | Soma volume (µm³) |
| `soma_surface_area` | Soma surface area (µm²) |
| `soma_radius` | Mean soma radius (µm) |
| `number_of_neurites` | Number of primary processes |
| `number_of_sections` | Number of unbranched sections |
| `number_of_segments` | Number of SWC edges |
| `mean_section_length` | Average section length (µm) |
| `mean_segment_length` | Average segment length (µm) |
| `mean_local_bif_angle` | Mean bifurcation angle (°) |
| `n_bifs` | Number of bifurcation points |

### 3. Metadata Processing

- Merges morphology features with metadata
- Filters to adult-only samples
- Removes ambiguous sex labels

### 4. Exploratory Data Analysis

- Outlier removal (> 3 SD from mean)
- Boxplots and correlation heatmaps
- Welch's t-tests with Bonferroni correction
- Separate balanced and unbalanced datasets used for different analyses

### 5. PCA & Clustering

- Principal Component Analysis (PCA)
- K-means clustering (`k = 2`)
- Silhouette score evaluation

### 6. Supervised Classification

Models used:

- Logistic Regression
- Random Forest
- Gradient Boosting

Includes:

- Stratified 5-fold cross-validation
- Accuracy and ROC/AUC evaluation
- Confusion matrices
- SHAP feature importance analysis

### 7. Sex-Stratified Analysis

- Welch's t-tests by sex
- Two-way ANOVA (disease × sex)
- Effect sizes and corrected p-values

---

## `behavioral_analysis.py`

### 1. Data Loading & Cleaning

- Loads `FB_AD_5Choice.csv`
- Filters valid genotypes
- Standardizes sex labels
- Removes missing values and outliers

### 2. Behavioral Metrics

Analyzes:

- Accuracy
- Omission rate
- Premature responses
- Reward collection latency
- Correct/incorrect response latency
- Perseverative responses
- Threshold performance metrics

### 3. Statistical Analysis

- Sex-stratified Welch's t-tests
- Bonferroni correction
- Two-way ANOVA (disease × sex)
- Effect size calculations

### 4. Outputs

Generates:

- Boxplots and barplots
- Heatmaps
- ANOVA significance plots
- Summary tables

---

# Outputs

Both scripts automatically generate an `outputs/` folder containing:

- Figures (`.png`, 300 dpi)
- Statistical summary tables (`.csv`)

---

# Setup

Install required packages:

```bash
pip install neurom==4.0.4 scikit-learn shap statsmodels scipy pandas numpy matplotlib seaborn
```

Before running locally, update the file paths at the top of each script to match your directory structure.

---

# Reproducibility

> [!NOTE]
> All stochastic procedures use a fixed seed (`random_state = 42`).

The analyses were originally run in Google Colaboratory using standard CPU/GPU resources.
