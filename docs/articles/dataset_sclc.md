# Codebook for small-cell lung cancer dataset

## Codebook: Small-Cell Lung Cancer Dataset

### Where to find it

- **Used in:** [Lab 4b: logistic
  regression](https://cuny-epibios.github.io/PUBH614/articles/04b_logistic.html)
- **File name:** `Stats4- more.csv`
- **Location:** Available online at
  <https://media.githubusercontent.com/media/CUNY-epibios/PUBH614/tree/main/datasets>
- [Download the dataset
  now](https://media.githubusercontent.com/media/CUNY-epibios/PUBH614/refs/heads/main/datasets/Stats4-%20more.csv)

Code to load this dataset into R, and ensure all columns are read in as
factor type:

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Dataset Overview

This dataset contains information about small-cell lung cancer cases,
including smoking status, cancer status, and patient sex. The dataset
includes 209 observations with 3 variables.

### Variables

#### smoke

- **Description**: Smoking status of the patient
- **Type**: Binary (0/1)
- **Values**:
  - 0 = Non-smoker
  - 1 = Smoker
- **Missing values**: None

#### lungca

- **Description**: Lung cancer status
- **Type**: Binary (0/1)
- **Values**:
  - 0 = No lung cancer
  - 1 = Has lung cancer
- **Missing values**: None

#### sex

- **Description**: Biological sex of the patient
- **Type**: Binary (M/F)
- **Values**:
  - M = Male
  - F = Female
- **Missing values**: None

### Summary Statistics

Please enable JavaScript to experience the dynamic code cell content on
this page.

### Data Quality Notes

- The dataset is complete with no missing values
- All variables are coded consistently
- `smoke` and `lungca` use 0/1 coding
- `sex` is coded using single-letter values (M/F)

### Acknowledgements

This codebook was drafted by Microsoft Copilot and edited by Levi
Waldron.
