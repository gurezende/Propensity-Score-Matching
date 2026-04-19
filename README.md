# Propensity Score Matching (PSM) for Causal Inference

This project provides a step-by-step implementation of **Propensity Score Matching (PSM)** in Python. PSM is a statistical technique used to estimate the effect of a treatment or intervention by accounting for the covariates that predict receiving the treatment. 

In observational studies, treatment assignment is rarely random. This notebook demonstrates how to create a "balanced" dataset (finding statistical twins) to move from simple correlation to **Causal Inference**.

## 🚀 Overview

Simple averages in data often "lie" because of **Selection Bias**. For example, if we want to measure the impact of an advertisement on spending, we might find that people who saw the ad spent more. However, if those people were already frequent shoppers (high propensity to see the ad), the ad might not be the cause of the increase.

**This project solves that by:**
1.  Predicting the probability of treatment (Propensity Score) using Logistic Regression.
2.  Matching treated units with control units that have similar scores.
3.  Evaluating the balance of the new dataset using Standardized Mean Differences (SMD).
4.  Calculating the true causal effect (Difference in Means).

## 🛠️ Tech Stack

* **Python 3.x**
* **Scikit-Learn:** `LogisticRegression` for scoring and `NearestNeighbors` for matching.
* **Pandas/NumPy:** Data manipulation and synthetic dataset generation.
* **Matplotlib/Seaborn:** Visualization of distribution overlaps.
* **SciPy:** Statistical testing (T-tests).

## 📊 Key Implementation Steps

### 1. Propensity Score Calculation
We use a Logistic Regression model where the dependent variable is the treatment indicator (`saw_ad`) and the independent variables are the pre-treatment covariates (`age`, `past_spend`, `is_mobile`).

### 2. Matching with Caliper
To ensure high-quality matches, we implement a **Caliper**. This prevents "bad" matches by requiring that twins have a propensity score distance within a specific threshold (e.g., 0.05).

### 3. Evaluation (Balance Check)
We check the success of the matching by calculating the **Standardized Mean Difference (SMD)**. A successful match should result in an SMD < 0.1 for all covariates, indicating the groups are now comparable.

## 📈 Results Highlights

In the provided synthetic dataset:
* **Pre-Matching:** Significant bias existed in spending habits between groups.
* **Post-Matching:** The groups achieved an **Excellent Balance** (SMD close to 0).
* **Causal Effect:** We isolated the specific lift in spend attributable only to the treatment.

## 💻 Usage

If you are using the `uv` package manager:

```bash
uv pip install pandas numpy scikit-learn matplotlib seaborn scipy
```

To run the analysis:

Open Propensity_Score_Match.ipynb.

Run the "Dataset Generation" cell to create the biased sample.

Follow the documented steps to perform the matching and view the causal results.

## 📄 License

This project is open-source and available under the MIT License.
