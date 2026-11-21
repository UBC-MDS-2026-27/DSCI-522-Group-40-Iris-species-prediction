# Iris Species Prediction

**DSCI 522 — Group 40**

## Project Overview

This project uses machine learning to predict Iris flower species based on sepal and petal measurements.

The dataset contains 150 flowers from three species: Setosa, Versicolor, and Virginica. Each flower has four measurements: sepal length, sepal width, petal length, and petal width.

The goal is to investigate how accurately machine learning models can classify Iris species using these measurements.

## Authors

- Cesar Figueroa
- Nick Petersen
- Parva Fazeli Farsani
- Qibing He

## Methods

We compare three classification models:

- Dummy classifier
- K-nearest neighbors (kNN)
- Logistic regression

The data is divided into 70% training and 30% testing sets using stratified sampling. We use five-fold cross-validation to compare model performance on the training data.

The final logistic regression model is evaluated on the held-out test set using classification accuracy and a confusion matrix.

## Installation

To reproduce this analysis, you will need:

- [Git](https://git-scm.com/downloads)
- Python 3.13 or newer
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [Quarto](https://quarto.org/docs/get-started/)

### Clone the repository

Open Terminal (macOS/Linux) or PowerShell (Windows) and run:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-40-Iris-species-prediction.git
cd DSCI-522-Group-40-Iris-species-prediction
```

### Install dependencies

From the repository's root directory, run:

```bash
uv sync --locked
```

This creates the project's virtual environment and installs the Python dependencies specified in `pyproject.toml` and `uv.lock`.

The main Python dependencies include pandas, scikit-learn, Altair, and Jupyter.

## Reproducing the Analysis

After installing the dependencies, run the Quarto report from the repository's root directory.

### macOS / Linux

Run:

```bash
QUARTO_PYTHON="$(pwd)/.venv/bin/python3" quarto render analysis/iris-species-prediction.qmd --to html
```

### Windows (PowerShell)

Run:

```powershell
$env:QUARTO_PYTHON = (Resolve-Path ".venv\Scripts\python.exe").Path
quarto render analysis/iris-species-prediction.qmd --to html
```

### Output

The rendered report will be saved to:

`analysis/iris-species-prediction.html`

Open the HTML file in a web browser to view the analysis, visualizations, and results.

**Note:** The macOS instructions have been tested successfully. The Windows instructions still need to be tested on a Windows computer.

## Results

The logistic regression model achieved approximately **97.8% accuracy** on the held-out test set, correctly classifying 44 out of 45 observations.

The results suggest that sepal and petal measurements can be used to distinguish the three Iris species with high accuracy on this dataset. However, the dataset is small, so these results may not generalize to more diverse flower populations or measurement conditions.

## Project Structure

```text
.
├── analysis/
│   ├── iris-species-prediction.qmd
│   ├── iris-species-prediction.html
│   └── references.bib
├── data/
│   ├── raw/
│   │   └── iris.data
│   └── processed/
│       ├── iris_clean.csv
│       ├── iris_train.csv
│       └── iris_test.csv
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

Other repository documentation, including contribution guidelines, the code of conduct, and licensing information, is maintained in the repository as it becomes available.

## Published Report

The Quarto report is available locally at `analysis/iris-species-prediction.html`.

A GitHub Pages link will be added once the report has been published.

## References

References for the dataset, statistical methods, machine learning tools, and data organization are maintained in `analysis/references.bib`.

These include the UCI Iris dataset, Fisher (1936), Pedregosa et al. (2011), and Wickham (2014).

## License

The planned licenses are MIT for the project code and Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0) for the report, subject to confirmation in `LICENSE.md`.

Please refer to `LICENSE.md` for the final license terms once that file is merged into the repository.

## Generative AI Use

Generative AI tools, including ChatGPT, were used to assist with documentation drafting, Git workflow guidance, troubleshooting, and reviewing reproducibility instructions.

All AI-assisted content and technical suggestions should be reviewed and verified by the project contributors before inclusion.

Examples of prompts used during the project include:

- "Help write reproducibility instructions for a Python project using uv and Quarto."
- "How can I troubleshoot a Quarto report that times out while starting a Jupyter kernel?"
- "Suggest relevant academic references for an Iris species classification report."