# Data

This folder contains the raw and processed datasets used in the microglial morphometry and behavioral analyses.

All data were obtained from open-access scientific repositories.

---

# Data Sources

## Microglial Reconstructions — NeuroMorpho.org

- **URL:** https://neuromorpho.org
- **Format:** SWC (Standardized Wireframe Cell) files
- **Contents:** 3D reconstructions of hippocampal microglia from 5xFAD and wild-type control mice
- **Reference:** Ascoli et al. (2007), *Journal of Neuroscience*

---

## Behavioral Data — MouseBytes

- **URL:** https://mousebytes.ca
- **Format:** CSV
- **Contents:** 5-choice serial reaction time task (5CSRTT) behavioral performance records from 5xFAD and control mice
- **Reference:** Beraldo et al. (2019), *eLife*

---

# Dataset Summary

| Dataset Subset | Number of Cells / Records | Notes |
|---|---|---|
| Full adult cohort | 3,818 | 2,642 control + 1,176 AD |
| Filtered dataset | 3,585 | Outliers removed |
| Balanced ML dataset | 2,352 | 1,176 cells per class |
| Balanced + filtered | 2,197 | Used for PCA and clustering |
| Female subset | 2,002 | 1,349 control + 653 AD |
| Male subset | 1,583 | 1,067 control + 516 AD |
| Behavioral (control) | 2,317 | C57BL/6J + B6129SF2/J |
| Behavioral (5xFAD) | 992 | After outlier removal |

---

# SWC File Format

Each SWC file represents one reconstructed microglial cell as a collection of connected 3D nodes.

| Column | Field | Description |
|---|---|---|
| 1 | Index | Sequential node identifier |
| 2 | Type | `1 = soma`, `7 = glial process` |
| 3 | X | X-coordinate (µm) |
| 4 | Y | Y-coordinate (µm) |
| 5 | Z | Z-coordinate (µm) |
| 6 | R | Node radius (µm) |
| 7 | Parent | Parent node index (`-1 = root`) |

---

# Morphometric Features Extracted

| Feature | Description |
|---|---|
| Soma volume | Total 3D volume of the soma (µm³) |
| Soma surface area | Total soma surface area (µm²) |
| Soma radius | Mean soma radius (µm) |
| Number of neurites | Number of primary processes |
| Number of sections | Number of unbranched cable sections |
| Number of segments | Number of SWC edges |
| Mean section length | Average section length (µm) |
| Mean segment length | Average node-to-node edge length (µm) |
| Number of bifurcations | Number of branch points |
| Mean local bifurcation angle | Average angle between daughter branches (°) |

---

# Notes

- Metadata (age, sex, disease status) were retrieved programmatically from the NeuroMorpho.org API alongside SWC files.
- 25 control cells with soma extraction errors were excluded before analysis.
- 317 cells with ambiguous `"Male/Female"` annotations were excluded from sex-stratified analyses.
- Outliers were defined as values exceeding 3 standard deviations from the mean for any morphometric feature.
