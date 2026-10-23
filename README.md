# FlyRank ML Internship — Applied Search Intelligence

This is my workspace for the FlyRank ML Internship, focused on Google Search ranking, content discoverability, and machine learning.

The project uses anonymized FlyRank search data for educational analysis. Results are for decision support; they do not predict or explain Google's ranking algorithm.


## Capstone report

- **Published paper:** https://sai875.github.io/flyrank-ml-internship/
- **Source HTML:** [docs/index.html](docs/index.html)
- **Aggregate evaluation metrics:** [work/outputs/capstone_metrics.json](work/outputs/capstone_metrics.json)
- **Precision@K chart:** [work/figures/capstone_precision_at_k.png](work/figures/capstone_precision_at_k.png)

The paper is deployed from `docs/` by the GitHub Actions workflow at `.github/workflows/deploy-pages.yml`. If the published URL is not available yet, open **Settings → Pages** and set the build source to **GitHub Actions**, then check the **Actions** tab for the deployment result. Do not commit raw datasets, client-level rows, credentials, or tokens.


## Getting started

1. Read [SETUP.md](SETUP.md) for GitHub, Google Colab, and data-access instructions.
2. Read [GUIDE.md](GUIDE.md) to understand the repository structure and what to edit.
3. Read [skills/README.md](skills/README.md) for the AI-assistant instruction library.
4. Read [DATA_USE.md](DATA_USE.md) before using data.
5. Keep [docs/data-dictionary.md](docs/data-dictionary.md) open while working with dataset columns.

## Open the starter notebooks in Colab

- [Week 1 — First look and discovery](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/01_first_look_and_discovery.ipynb)
- [Week 2 — Your first readable model](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/02_your_first_readable_model.ipynb)
- [Weeks 3+ — Working with the full release](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/03_working_with_the_full_release.ipynb)

The full warehouse is hosted at [FlyRank/internship-warehouse](https://huggingface.co/datasets/FlyRank/internship-warehouse). Access is gated; request access and accept the data-use terms before connecting.

## Repository structure

| Path | Purpose |
|---|---|
| `notebooks/` | Starter notebooks for Weeks 1–2 and full-release exploration |
| `scripts/` | Data preparation, baseline scoring, model training, evaluation, and report generation |
| `data/raw/content_refresh_anonymized.csv` | Anonymized starter dataset, if included in this repository |
| `outputs/` | Example pipeline outputs |
| `work/` | My lane experiments, assignments, and capstone work |
| `work/notebooks/` | My assignment notebooks |
| `docs/` | ML foundations, lane guidance, tooling guidance, and data dictionary |
| `skills/` | Instructions for AI-assisted work |

## Assignment work

### W02 — ML Task Framing

Notebook: [work/notebooks/w02_ml_task_framing.ipynb](work/notebooks/w02_ml_task_framing.ipynb)

This exercise frames a ranking/classification task for prioritizing content pages for review. It defines a proxy label, success metric, unit of analysis, and limitations. The label is a proxy, not ground truth about Google's ranking algorithm.

### W03 — Data Contract

Required notebook: `work/notebooks/w03_data_contract.ipynb`

The W03 notebook should contain:
1. Five plain-English data-contract answers: row grain, source tables, time window, target/proxy, and exclusions.
2. Exactly three verification queries with outputs: grain, row count/date span, and availability filtered using `IS TRUE`.
3. A feature frame with no more than five predictive features, each with an explanation of when it is available.
4. A deliberate label-leakage experiment, with the leaked feature removed from the final inputs and the honest score retained.
5. One named limitation of the data slice.

Use a mid-panel month such as March 2026 for development. Treat June 2026, the final month in the `_sample` table, as a sealed test month and do not use it to develop label logic. Confirm actual table and column names from the schema before running queries.

**Status note:** The W03 notebook must exist and be committed at the required path before the assignment is complete.

## Local workflow (optional)

```bash
git clone <this-repo-url>
cd flyrank-ml-internship
pip install -r requirements.txt
python scripts/run_all.py
```

This runs the reference pipeline on the bundled sample when the required files and dependencies are available.

## Data safety

- Never commit Hugging Face tokens, passwords, or other credentials.
- Store `HF_TOKEN` in Google Colab Secrets when required; do not paste it into notebook cells.
- Follow [DATA_USE.md](DATA_USE.md) and the dataset access terms.
- Never add private client data or unapproved warehouse exports to this public repository.
- Describe results as observed, measured, directional, or decision-support findings—not as predictions of Google's algorithm.

## Submission workflow

1. Complete the assignment in the required notebook under `work/notebooks/`.
2. Run all cells and ensure outputs are visible.
3. Save the notebook to this repository and commit it to the `main` branch.
4. Submit this GitHub repository URL on the corresponding assignment card.

Repository: https://github.com/Sai875/flyrank-ml-internship
