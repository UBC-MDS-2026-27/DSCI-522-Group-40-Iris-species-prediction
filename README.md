# Iris Species Prediction

DSCI 522 — Group 40

## Project Overview

This project uses machine learning to predict Iris flower species based on sepal and petal measurements.

The dataset contains 150 flowers from three species: Setosa, Versicolor, and Virginica.

## Methods

We compare three classification models:
- Dummy classifier
- K-nearest neighbors (kNN)
- Logistic regression

We use a 70/30 training-test split and five-fold cross-validation.

## Installation

Install the required dependencies using:

uv sync --locked

## Reproducing the Analysis

Run the following command from the project directory on macOS:

QUARTO_PYTHON="$(pwd)/.venv/bin/python3" quarto render analysis/iris-species-prediction.qmd --to html

## Results

The logistic regression model achieved approximately 97.8% test accuracy.

## References

References are stored in analysis/references.bib.