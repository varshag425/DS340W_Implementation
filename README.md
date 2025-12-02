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
├── README.md
├── rg30_set1.csv                        # Week 11 dataset: taken from: https://www.projectmanagement.ugent.be/research/data
├── 340W_testMLmodels.ipynb              # Week 11 ML Models (LogReg / NB / RF) using rg30_set1.csv
├── 340w (2).ipynb                       # Week 11 data generation
│
├── FinalPaperImplementation.zip
│   └── FinalPaperImplementation/
│       ├── final_code.ipynb             # Full pipeline (DAG -> PERT -> CPM -> MC -> ML)
│       ├── rg30_set1.csv                # Dataset
│       └── README.md                    # Instructions for running locally; do NOT run data generation
│
├── Paper3Implementation.zip             # Updated Week 10 Parent Paper implementation for runnning on local machine
│   └── Paper3Implementation/
│       ├── paper3_code.ipynb
│       ├── data/
│       │   ├── RG30_PD.csv
│       │   ├── RG30_NT.csv
│       │   ├── RG30_Baseline.csv
│       │   ├── RG30_Simulations.csv
│       │   ├── RG30_ModelTable.csv
│       │   ├── RG30_BNEdges.csv
│       │   └── rangen2_raw/
│       │       ├── rangen2_SP01/
│       │       ├── rangen2_SP02/
│       │       └── ... up to SP09/
│       └── README.md                    # Instructions for running Week 10 pipeline locally
│
├── data.zip                             # Week 10 data archive (is also inside Paper3Implementation.zip)
└── paper3_code (1).ipynb                # Old Week 10 code

```

---

# Requirements
This project can run on local Jupyter Notebook.

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
Run files only from:
- Paper3Implementation.zip
- FinalPaperImplmentation.zip

1. Download and unzip each folder on your local machine
2. Both zip files contain read me docs with further instructions on how to run code files locally.

If you are using VSCode, Read Me files can be viewed using:
1. Cmd ⌘ + Shift ⇧ + P (Mac) or Ctrl + Shift + P (Windows)
2. Then, type -  Markdown: Open Preview

# Important Note on Data Generation Cells

The notebook contains cells that generate synthetic project networks.

You do NOT need to run these cells.
The project uses the provided datasets (within the zip files)

If you choose to run the simulation cells:
- the output will be identical because the random seed is fixed
- the generated dataset can also be used (same distributions)

# Summary of Methodology

The methodology implemented in this repository includes:

1. Synthetic Project Network Generation
- RanGen2 RG30 structure as baseline (Vanhoucke et al., 2008)
- PERT triplets generated around base durations
- CPM used to compute earliest/critical paths

2. Monte Carlo Simulation (200 runs per project)
  - Extracted distributional uncertainty features, including:
      - mean & variance of activity durations
      - probability of late completion
      - critical-path sensitivity
      - network-level uncertainty indicators

3. Early-Stage EVM Features (20% Progress)
  - Schedule Performance Index (SPI)
  - Cost Performance Index (CPI)
  - These enable semi-dynamic forecasting—unlike snapshot-based methods.

4. Supervised Machine Learning Models
  - Trained and tested:
      - Logistic Regression
      - Naïve Bayes
      - Random Forest

5. Baseline Analytical Comparison
  - Compared ML performance to a simple deterministic CPM/MC classification rule.

# Key Results

- Random Forest achieved the highest predictive accuracy on the held-out test set
- ML models significantly outperformed the deterministic CPM/MC baseline
- Simulation-derived uncertainty features improved delay prediction ability
- Early-stage SPI/CPI contributed meaningful semi-dynamic forecasting power

# Reproducibility Notes

All randomness is controlled with fixed seeds
Final dataset is included in /data
Notebook executes without modification if run via Colab
No external proprietary data used—entire project is synthetic and reproducible

## References

Ünsal-Altuncan, B., & Vanhoucke, M. (2023). *An SEM–BN hybrid model for project forecasting and control using Monte Carlo simulation*. *Computers & Industrial Engineering, 182*, 109367. https://doi.org/10.1016/j.cie.2023.109367
