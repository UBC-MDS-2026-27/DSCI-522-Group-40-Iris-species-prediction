# Iris Species Prediction

**DSCI 522 — Group 40**

## Project Overview

This project uses machine learning to predict Iris flower species based on sepal and petal measurements.

The dataset contains 150 flowers from three species: Setosa, Versicolor, and Virginica. Each flower has four measurements: sepal length, sepal width, petal length, and petal width.

The goal is to investigate how accurately machine learning models can classify Iris species using these measurements.


## Authors

- [Cesar Figueroa](https://github.com/cfigue09)
- [Nick Petersen](https://github.com/Nick-Petersen)
- [Parva Fazeli Farsani](https://github.com/ParvaFarsani)
- [Qibing He](https://github.com/AlexHe03)


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

**Note:** The repository setup and complete Quarto report rendering have been successfully tested on both macOS and Windows.

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
├── docs/
│   └── index.html
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

The `docs/` directory contains the HTML report published through GitHub Pages.


## Published Report

The complete Quarto report is available online through GitHub Pages:

[View the published Iris Species Prediction report](https://ubc-mds-2026-27.github.io/DSCI-522-Group-40-Iris-species-prediction/)

The report includes the Summary, Introduction, Methods, Results, Discussion, visualizations, and references.

The rendered HTML report is also available in the repository at `analysis/iris-species-prediction.html`.

The `docs/index.html` file contains the published version of the report used by GitHub Pages.


## References

References for the dataset, statistical methods, machine learning tools, and data organization are maintained in `analysis/references.bib`.

These include the UCI Iris dataset, Fisher (1936), Pedregosa et al. (2011), and Wickham (2014).

## License

The project code is licensed under the MIT License.

The original report text, figures, and tables are licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0) license.

See [LICENSE.md](LICENSE.md) for details.


## Generative AI Use

Generative AI tools, including ChatGPT and Claude, were used to assist with documentation drafting, Git workflow guidance, troubleshooting, and reviewing reproducibility instructions.

ChatGPT was used to support documentation, Git and GitHub workflows, and troubleshooting. Claude was used to suggest a solution to the SSL certificate verification issue encountered when downloading the Iris dataset on Windows.

AI-assisted content and technical suggestions were reviewed and tested by project contributors before inclusion.

Examples of AI prompts and troubleshooting questions used during the project include:

- "Help write reproducibility instructions for a Python project using uv and Quarto."
- "How can I troubleshoot a Quarto report that times out while starting a Jupyter kernel?"
- "Suggest relevant academic references for an Iris species classification report."
- Windows SSL certificate verification troubleshooting (Claude; exact prompt not recorded).