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

This project uses Docker to provide a reproducible environment for running the Iris Species Prediction analysis. Docker includes the required Python dependencies and Quarto, so users do not need to install them separately.

### Prerequisites

Install the following software:

- [Git](https://git-scm.com/downloads)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

Make sure Docker Desktop is running before continuing.

The Docker Compose configuration also requires an SSH public key at `~/.ssh/id_ed25519.pub` and a Git configuration file at `~/.gitconfig`. Both files must exist before starting the container.

SSH key setup

The Docker environment requires an SSH public key at ~/.ssh/id_ed25519.pub.

If you do not already have an SSH key, generate one using:

ssh-keygen -t ed25519

Press Enter to accept the default file location (~/.ssh/id_ed25519) and follow the prompts to configure an optional passphrase.

If an SSH key already exists at that location, do not overwrite it.

You can verify that your public key exists by running:

ls ~/.ssh/id_ed25519.pub

The Docker Compose configuration also requires a Git configuration file at ~/.gitconfig. If it does not exist, configure your Git name and email using git config --global user.name and git config --global user.email with your own values.

### Clone the repository

Open Terminal and run:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-40-Iris-species-prediction.git
cd DSCI-522-Group-40-Iris-species-prediction
```

### Start the Docker environment

From the repository's root directory, run:

```bash
docker compose pull
docker compose up -d
```

These commands download the project's Docker image from Docker Hub and start the container in the background.

The repository is mounted at `/workspace` inside the container, so changes to project files are accessible both locally and inside Docker.

### Verify the environment

Check that Python and Quarto are available inside the container:

```bash
docker compose exec analysis-env uv run python --version
docker compose exec analysis-env quarto --version
```

You can also verify the main Python dependencies:

```bash
docker compose exec analysis-env uv run python -c "import pandas, sklearn, altair; print('All packages installed successfully!')"
```
## Reproducing the Analysis

After starting the Docker environment, render the Quarto report from the repository's root directory:

```bash
docker compose exec analysis-env uv run quarto render analysis/iris-species-prediction.qmd --to html
```

This executes the analysis inside the Docker container and generates the HTML report at `analysis/iris-species-prediction.html`.

To view the report on macOS, run:

```bash
open analysis/iris-species-prediction.html
```

On Windows, open the report using PowerShell:

```powershell
Start-Process analysis/iris-species-prediction.html
```

The report includes exploratory visualizations, cross-validation results, and final model evaluation.

Running the report in a temporary container

Alternatively, you can render the report using a temporary Docker container:

docker compose run --rm analysis-env uv run quarto render analysis/iris-species-prediction.qmd --to html

The --rm flag automatically removes the temporary container after the command finishes, so you do not need to manually remove it.

This differs from docker compose up -d, which starts a persistent container that you can stop and remove later using docker compose down.

For additional development instructions, see CONTRIBUTING.md.

## Stopping the Docker Environment

When you have finished working, stop and remove the project's containers and network:

```bash
docker compose down
```

This does not delete the project files or generated reports stored in your local repository.

To restart the environment later, run:

```bash
docker compose up -d
```
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