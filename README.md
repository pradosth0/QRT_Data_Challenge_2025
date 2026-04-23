# Submission for the QRT date challenge 2025
## Overview

This project implements a model evaluation framework for a financial data challenge.  
The primary objective is to **estimate model performance as reliably as possible** under noisy and unstable conditions typical of financial datasets.

Rather than relying on a single train/test split, this notebook uses **repeated sampling over time-series blocks** to approximate the distribution of model performance metrics.

---

## Objectives

- Evaluate classification models on financial time-series data
- Estimate:
  - Mean performance
  - Variance of performance
- Compare models using **robust statistical summaries**
- Reduce evaluation noise through repeated experiments

---

## Methodology

### 1. Data Structure

- The dataset is composed of **time-series segments (TS)**
- Each TS is treated as a **grouped unit** to avoid leakage across samples

---

### 2. Sampling Strategy

A custom sampling function (`echantillon_numpy`) is used to:

- Randomly split time-series blocks into:
  - Training set
  - Test set
- Repeat the process **NB_TESTS times (default: 100)**

This produces multiple performance estimates across different data configurations.

---

### 3. Model Training

For each split:

- A model is trained on the training subset
- Predictions are generated on the test subset

---

### 4. Evaluation Metrics

The following metrics are computed for each run:

- Accuracy
- Precision
- Recall
- F1-score
- ROC AUC

---

### 5. Aggregation of Results

Across all runs:

- Compute:
  - Mean performance
  - Standard deviation
- Analyze variability and stability of models

---

## Key Idea

Instead of relying on a single evaluation:

> Model performance is treated as a **distribution**, not a point estimate.

This is particularly important in finance, where:
- Data is noisy
- Regimes change
- Results are highly sensitive to sampling

---

## Limitations

This approach has several important limitations:

- Overlapping samples reduce independence between runs

---

## Usage

1. Load the dataset
2. Run the notebook
3. Adjust parameters:
   - `NB_TESTS` (number of repetitions)
   - Train/test split ratio
4. Compare models based on:
   - Mean metrics
   - Variability

---

## Conclusion

This project provides a **Monte Carlo-style evaluation framework** for financial models.  
While it improves over single-split validation, it should be extended with **time-aware validation techniques** for more reliable real-world performance estimation.
```
