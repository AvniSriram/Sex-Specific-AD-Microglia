# Sex-Specific Microglial Morphometry and Phenotyping in Alzheimer's Disease

A computational neuroinformatics pipeline integrating large-scale microglial morphometry, statistical analysis, and machine learning to characterize sex-dependent and Alzheimer's disease–associated differences in hippocampal microglial structure and cognitive outcomes.

---

## Overview

This repository contains all code and data supporting the analysis presented in:
> **"An Integrative Framework for Sex-Specific Microglial Morphometry and Phenotyping in Alzheimer's Disease"**

The study analyzes over **6,000 digitally reconstructed hippocampal microglia** from 5xFAD (Alzheimer's model) and wild-type control mice, alongside behavioral performance data from the 5-choice serial reaction time task (5CSRTT), to characterize how AD-related and sex-dependent factors shape microglial morphology and cognitive outcomes.

---

## Key Findings

* **Morphological Alterations:** AD microglia show reduced branching complexity and altered soma size relative to controls.
* **High-Accuracy Classification:** Ensemble ML models (*Random Forest, Gradient Boosting*) classified AD vs. control microglia with **~96% accuracy** and **AUC = 0.99**.
* **Sex-Dependent Differences:** * Female microglia exhibited greater morphological simplification than males across nearly all metrics.
  * Male 5xFAD mice showed broader cognitive impairments on 5CSRTT; females showed a narrower but significant impairment profile.

---

## Data Sources

* **Microglial reconstructions:** [NeuroMorpho.org](https://neuromorpho.org/) (SWC files, hippocampal microglia)
* **Behavioral data:** [MouseBytes](https://mousebytes.ca/) (5CSRTT performance records)

---

## Dependencies

The pipeline requires **Python 3.x** (developed in Google Colaboratory) and the following libraries:

```text
neurom==4.0.4
scikit-learn
shap
statsmodels
scipy
pandas
numpy
matplotlib
seaborn
