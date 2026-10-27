# FlyRank ML Internship — Applied Search Intelligence

This is my workspace for the FlyRank ML Internship, focused on Google Search ranking, content discoverability, and machine learning.

The project uses anonymized FlyRank search data for educational analysis. Results are for decision support; they do not predict or explain Google's ranking algorithm.


## Capstone report

- **Published paper:** https://sai875.github.io/flyrank-ml-internship/
- **Source HTML:** [docs/index.html](docs/index.html)
- **Aggregate evaluation metrics:** [work/outputs/capstone_metrics.json](work/outputs/capstone_metrics.json)
- **Precision@K chart:** [work/figures/capstone_precision_at_k.png](work/figures/capstone_precision_at_k.png)

The paper is published from `main` → `/docs` using GitHub Pages. Check **Settings → Pages** to confirm the publishing source is `main` and `/docs`, then use the **Actions** tab to inspect the latest Pages build. Do not commit raw datasets, client-level rows, credentials, or tokens.


## Getting started

1. Read [SETUP.md](SETUP.md) for GitHub, Google Colab, and data-access instructions.
2. Read [GUIDE.md](GUIDE.md) to understand the repository structure and what to edit.
3. Read [skills/README.md](skills/README.md) for the AI-assistant instruction library.
4. Read [DATA_USE.md](DATA_USE.md) before using data.
5. Confirm actual warehouse table and column names from the schema before running SQL.

## Run the capstone notebook in Colab

- [Open ML-11 capstone experiment in Google Colab](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/capstone.ipynb)
- The notebook installs its Python dependencies, downloads the public anonymized starter CSV at runtime if it is not present, and generates aggregate metrics plus a report-safe Precision@K chart. The raw CSV is runtime-only and must never be committed.
- The capstone GitHub Actions workflow executes the notebook and commits only the executed notebook, aggregate metrics, and report-safe chart. In Colab, use **File → Save a copy in GitHub** to save your notebook work. Never paste tokens into notebook cells or outputs.

## Open the starter notebooks in Colab

- [Week 1 — First look and discovery](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/01_first_look_and_discovery.ipynb)
- [Week 2 — Your first readable model](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/02_your_first_readable_model.ipynb)
- [Weeks 3+ — Working with the full release](https://colab.research.google.com/github/flyrank-bih/flyrank-ml-internship-starter/blob/main/notebooks/03_working_with_the_full_release.ipynb)

The full warehouse is hosted at [FlyRank/internship-warehouse](https://huggingface.co/datasets/FlyRank/internship-warehouse). Access is gated; request access and accept the data-use terms before connecting.

## Repository structure

| Path | Purpose |
|---|---|
| `notebooks/` | Starter notebooks for Weeks 1–2 and full-release exploration |
| `work/` | My lane experiments, assignments, and capstone work |
| `work/notebooks/` | My assignment notebooks |
| `docs/` | ML foundations, lane guidance, tooling guidance, and data dictionary |
| `skills/` | Instructions for AI-assisted work |

## ML-10 — Content action playbook

- [Executed action-playbook notebook](work/notebooks/w07_action_playbook.ipynb) · [Open in Colab](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w07_action_playbook.ipynb)
- [Aggregate playbook metrics receipt](work/outputs/w07_playbook_metrics.json)
- [Priority-tier figure (PNG)](work/figures/w07_priority_tiers.png) · [SVG version](work/figures/w07_priority_tiers.svg)
- [Automatic execution workflow](.github/workflows/w07-action-playbook.yml) runs the notebook top-to-bottom and commits only the executed notebook, aggregate metrics, and report-safe figure; it removes the row-level queue and downloaded CSV before committing.
- The ranked queue is generated as `work/outputs/w07_ranked_action_queue.csv` when the notebook runs. It is intentionally excluded from Git by the repository's data-safety rule; do not commit it.

The playbook is for human-reviewed triage only. Reason codes are review cues, not explanations of model internals; scores are not calibrated probabilities of recovery. Content changes, publishing, URL changes, and budget decisions must not be automated from this ranking.

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

**Status note:** The W03 notebook is present at the required path. The assignment is complete only after its cells run successfully, outputs are reviewed, and required checks and limitations are documented. The [W03 execution workflow](.github/workflows/w03-data-contract.yml) runs the notebook automatically when a repository Actions secret named `HF_TOKEN` is configured with an approved Hugging Face READ token. It now fails clearly and gives setup instructions if the secret is absent, and verifies dataset access before starting the longer warehouse query.

## Local workflow

A general-purpose local pipeline is not currently included in this repository: `requirements.txt` and `scripts/run_all.py` are not present. Use the linked Google Colab notebooks for the documented workflow, or install each notebook's dependencies in your own environment. Do not assume a local `python scripts/run_all.py` command is available.

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
