# FlyRank ML Internship — ML-03 Task Framing

This repository contains my work for the FlyRank Machine Learning Internship, with a focus on **ML-03: ML Task Framing**.

## Assignment notebook

**Notebook:** [W02 — ML Task Framing](work/notebooks/w02_ml_task_framing.ipynb)

[![Open in Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w02_ml_task_framing.ipynb)

The notebook frames a machine-learning task using the provided anonymized content-refresh dataset.

## What the notebook covers

- **Task type:** Defines the task as a ranking/classification problem for prioritizing pages for review.
- **Target and proxy label:** Explains the measurable proxy used in the notebook and its limitations.
- **Success metric:** Uses Precision@K to assess whether high-ranked pages contain more of the proxy-positive cases.
- **Data and unit of analysis:** Inspects the real dataset and identifies what each row represents.
- **Why machine learning:** Explains why a learned score may be more useful than a single fixed rule, while keeping a simple baseline for comparison.
- **Self-check and limitations:** Records assumptions, risks, and checks before moving to model building.

## Dataset

The notebook uses the repository's anonymized dataset:

`data/raw/content_refresh_anonymized.csv`

The dataset is used for learning and analysis. The notebook treats the label as a **proxy**, not ground truth about Google's ranking algorithm or the true potential of a page.

**Leakage caution:** Variables that directly encode the label or related outcome information (such as `trend_direction` and `trend_pct`, where applicable) should not be used as predictive features without a careful leakage review.

## How to open the notebook

1. Open the notebook link above, or browse to `work/notebooks/w02_ml_task_framing.ipynb`.
2. To run it in Colab, choose **Open in Colab** and run the cells from top to bottom.
3. If you make changes in Colab, save a copy back to this GitHub repository.

## Scope and limitations

This is an educational task-framing exercise based on anonymized observational data. Results are descriptive and intended to support prioritization; they do not establish causation or reveal Google's ranking algorithm.

## Repository

- **Repository:** https://github.com/Sai875/flyrank-ml-internship
- **Assignment notebook:** [work/notebooks/w02_ml_task_framing.ipynb](work/notebooks/w02_ml_task_framing.ipynb)

