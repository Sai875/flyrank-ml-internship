# FlyRank ML Internship — Search Intelligence

**Applied Search Intelligence: Google Search Ranking & Discoverability**

This repository is your assignment workspace and portfolio. The notebooks below are hosted in **your repository** and their Colab links open those exact files. Start by opening a notebook, run its cells from top to bottom, review the outputs, then use **File → Save a copy in GitHub** to save your work.

> **Important:** Colab displays outputs only after cells have run. The capstone and W07 notebooks have GitHub Actions workflows that execute them and save the executed notebooks. W03 uses a gated Hugging Face warehouse and needs approved access plus an `HF_TOKEN` secret for automatic execution. See [SETUP.md](SETUP.md).

## Assignment notebooks — open in Google Colab

All links below point to `Sai875/flyrank-ml-internship`, not the shared starter repository.

| Week | Card | Notebook | Open in Colab | View on GitHub |
|---|---|---|---|---|
| 1 | ML-02 | Research question | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w01_research_question.ipynb?flush_cache=true) | [Notebook](work/notebooks/w01_research_question.ipynb) |
| 2 | ML-03 | ML task framing | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w02_ml_task_framing.ipynb?flush_cache=true) | [Notebook](work/notebooks/w02_ml_task_framing.ipynb) |
| 3 | ML-04 | Data contract | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w03_data_contract.ipynb?flush_cache=true) | [Notebook](work/notebooks/w03_data_contract.ipynb) |
| 3 | ML-05 | Feature leakage check | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w03_feature_leakage_check.ipynb?flush_cache=true) | [Notebook](work/notebooks/w03_feature_leakage_check.ipynb) |
| 4 | ML-06 | Signal audit | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w04_signal_audit.ipynb?flush_cache=true) | [Notebook](work/notebooks/w04_signal_audit.ipynb) |
| 4 | ML-07 | Baseline score | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w04_baseline_score.ipynb?flush_cache=true) | [Notebook](work/notebooks/w04_baseline_score.ipynb) |
| 5 | ML-08 | Model | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w05_model.ipynb?flush_cache=true) | [Notebook](work/notebooks/w05_model.ipynb) |
| 6 | ML-09 | Validation audit | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w06_validation_audit.ipynb?flush_cache=true) | [Notebook](work/notebooks/w06_validation_audit.ipynb) |
| 7 | ML-10 | Action playbook | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w07_action_playbook.ipynb?flush_cache=true) | [Notebook](work/notebooks/w07_action_playbook.ipynb) |
| 8 | ML-11 | Capstone | [Open](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/capstone.ipynb?flush_cache=true) | [Notebook](work/notebooks/capstone.ipynb) |

### How to use the links

1. Click **Open** for the assignment you are working on.
2. In Colab, choose **Runtime → Run all** and read the outputs. If an error appears, fix it before submitting.
3. Choose **File → Save a copy in GitHub** and select `Sai875/flyrank-ml-internship` and the same notebook path.
4. Open the saved notebook on GitHub and check that the code and execution outputs are present.

If Colab cannot open a notebook, use **File → Open notebook → GitHub**, then enter `Sai875/flyrank-ml-internship` and select the file under `work/notebooks/`.

## Data access and execution

- **W03 Data Contract:** requires access to the gated [FlyRank/internship-warehouse dataset](https://huggingface.co/datasets/FlyRank/internship-warehouse). Follow [SETUP.md](SETUP.md) and never paste a Hugging Face token into code or chat.
- **Public sample notebooks:** use the anonymized starter CSV from [FlyRank/internship-starter](https://huggingface.co/datasets/FlyRank/internship-starter).
- **Automated execution:** [Public assignment workflow](.github/workflows/assignment-auto-run.yml) executes W01, W03 leakage check, W04 signal audit/baseline, and W06 validation audit and saves outputs. [Capstone workflow](.github/workflows/capstone-auto-run.yml) and [W07 workflow](.github/workflows/w07-action-playbook.yml) separately execute and validate those notebooks. W03 Data Contract remains gated on Hugging Face access.
- **Notebook checks:** [Notebook validation workflow](.github/workflows/notebook-validation.yml) validates notebook structure and assignment requirements.

## Project and data safety

This project uses anonymized search-performance data to prioritize content pages for human review. A decline proxy is a decision-support signal, not proof of causality or a guarantee of future Google ranking performance.

- Never commit private client data, raw warehouse records, credentials, or access tokens.
- Exclude target-derived fields and identifiers from model inputs.
- Use client-grouped holdout validation where applicable and report the metrics honestly.
- Follow [DATA_USE.md](DATA_USE.md) and the setup instructions in [SETUP.md](SETUP.md).

## Research paper

- **Paper / project site:** https://sai875.github.io/flyrank-ml-internship/
- **Capstone notebook:** [Google Search Ranking and Discoverability Capstone](work/notebooks/Google_Search_Ranking_and_Discoverability_Capstone.ipynb)

## Repository documentation

- [SETUP.md](SETUP.md) — Colab, GitHub, and gated data setup.
- [GUIDE.md](GUIDE.md) — repository guide and file map.
- [docs/data-dictionary.md](docs/data-dictionary.md) — data field definitions.
- [skills/README.md](skills/README.md) — instructions for using the project skills.

