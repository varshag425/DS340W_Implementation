# Simulation-Driven Machine Learning Framework for Semi-Dynamic Project-Delay Prediction
DS 340W – Fall 2025
Authors: Siyona Behera, Sahana Ramachandran, Varsha Giridharan


# Project Overview / Motivation
Schedule delays are a recurring problem in engineering, construction, and software projects. Traditional forecasting tools such as CPM, PERT, fuzzy EVM, and classical Monte Carlo simulations either assume static inputs or treat risks as independent—meaning they fail to capture cascading, interacting risks within project networks.

This project introduces a simulation-driven machine-learning framework that learns delay-risk patterns directly from data. Instead of relying on predefined fuzzy rules, grey intervals, or causal diagrams, we use Monte Carlo simulation to generate empirical uncertainty features, and then train ML models to predict project-delay outcomes.

Our final dataset contains 1050 synthetic project networks, each simulated with:

- PERT-based uncertainty

- CPM-based structure

- 200-run Monte Carlo outcomes

- Early performance indicators (SPI, CPI at 20% progress)

Three ML models were evaluated: Logistic Regression, Naïve Bayes, and Random Forest, and compared to a simple analytical CPM/MC baseline.


---

## Repository Structure

```
DS340W_Implementation/
│
├── 340W_testMLmodels.ipynb            # ML model testing notebook (Week 11)
├── 340w (2).ipynb                     # Updated implementation notebook (Week 11)
├── paper3_code (1).ipynb              # Parent Paper 3 implementation code
│
├── Paper3Implementation.zip           # Compressed files from earlier implementation
├── data.zip                           # Dataset files used in earlier submissions
├── rg30_set1.csv                      # Project network dataset (Week 11)
│
├── README.md                          # Project documentation (this file)
└── ...

```

---

# Requirements
This project can run on Google Colab (recommended) or local Jupyter Notebook.

Python Version: 3.x
Required Libraries:

- pandas

- numpy

- matplotlib

- seaborn

- scikit-learn

- networkx

- tqdm

any additional libraries used in the notebook

---

# How to Run the Notebook
Option 1 — Google Colab (Recommended)

✔ Easiest way
✔ Avoids local installation issues
✔ Supports Drive mounting

Steps:

Upload final_dataset.csv to your Google Drive

Open final_notebook.ipynb in Google Colab

Run the cell that mounts Google Drive

Update the file path in Cell 1 under “Data Preprocessing”

df = pd.read_csv('/content/drive/MyDrive/your_path/final_dataset.csv')


Run all cells top-to-bottom

Option 2 — Local Execution (Jupyter Notebook)

Steps:

Download final_dataset.csv

Open the notebook in Jupyter

Update the file path in Cell 1:

df = pd.read_csv('path/to/final_dataset.csv')


Skip the cell that mounts Google Drive

Run all cells in order

# Important Note on Data Generation Cells

The notebook contains cells that generate synthetic project networks.

You do NOT need to run these cells.
The project uses the final dataset provided in /data/final_dataset.csv.

If you choose to run the simulation cells:

the output will be identical because the random seed is fixed

the generated dataset can also be used (same distributions)

# Summary of Methodology

The methodology implemented in this repository includes:

1. Synthetic Project Network Generation

- RanGen2 RG30 structure as baseline (Vanhoucke et al., 2008)
- PERT triplets generated around base durations
- CPM used to compute earliest/critical paths

2. Monte Carlo Simulation (200 runs per project)

  Extracted distributional uncertainty features, including:

  mean & variance of activity durations

  probability of late completion

  critical-path sensitivity

  network-level uncertainty indicators

3. Early-Stage EVM Features (20% Progress)

  Schedule Performance Index (SPI)

  Cost Performance Index (CPI)

  These enable semi-dynamic forecasting—unlike snapshot-based methods.

4. Supervised Machine Learning Models

  Trained and tested:

  Logistic Regression

  Naïve Bayes

  Random Forest

5. Baseline Analytical Comparison

  Compared ML performance to a simple deterministic CPM/MC classification rule.

# Key Results

Random Forest achieved the highest predictive accuracy on the held-out test set

ML models significantly outperformed the deterministic CPM/MC baseline

Simulation-derived uncertainty features improved delay prediction ability

Early-stage SPI/CPI contributed meaningful semi-dynamic forecasting power

# Reproducibility Notes

All randomness is controlled with fixed seeds

Final dataset is included in /data

Notebook executes without modification if run via Colab

No external proprietary data used—entire project is synthetic and reproducible

## References

Ünsal-Altuncan, B., & Vanhoucke, M. (2023). *An SEM–BN hybrid model for project forecasting and control using Monte Carlo simulation*. *Computers & Industrial Engineering, 182*, 109367. https://doi.org/10.1016/j.cie.2023.109367
