# Repository guide

This repository contains the FlyRank ML internship notebooks, report-safe aggregate outputs, and a published capstone paper. It is not a full copy of the original starter repository's local pipeline.

## Main paths

| Path | Purpose |
|---|---|
| `README.md` | Project overview, notebook links, assignment requirements, and submission steps |
| `SETUP.md` | GitHub/Colab setup and gated warehouse access |
| `DATA_USE.md` | Data-use and public-safety rules |
| `docs/index.html` | Published capstone paper source |
| `docs/data-dictionary.md` | Confirmed warehouse field guide and schema-verification notes |
| `work/notebooks/w02_ml_task_framing.ipynb` | W02 task framing |
| `work/notebooks/w03_data_contract.ipynb` | W03 data contract, three verification queries, feature frame, and leakage audit |
| `work/notebooks/capstone.ipynb` | Capstone model comparison and report artifacts |
| `work/notebooks/w07_action_playbook.ipynb` | Human-reviewed content action playbook |
| `work/outputs/` | Aggregate, report-safe metrics only |
| `work/figures/` | Report-safe figures |
| `.github/workflows/notebook-validation.yml` | Notebook format and assignment-specific static checks |
| `.github/workflows/capstone-auto-run.yml` | Capstone execution and aggregate-output checks |
| `.github/workflows/w07-action-playbook.yml` | W07 execution, metrics/figure validation, and safe-output checks |

## Important repository limits

The current repository does **not** include `requirements.txt`, `scripts/run_all.py`, the legacy `scripts/` pipeline, or a committed `data/raw/content_refresh_anonymized.csv`. Do not follow old starter-repository instructions that assume those paths exist. The notebook workflows install their own dependencies; local dependency installation is notebook-specific.

The W03 notebook uses the gated `FlyRank/internship-warehouse` dataset. Request access and accept the terms first, then store a Hugging Face READ token in Colab Secrets as `HF_TOKEN`. Never commit tokens, raw warehouse data, or row-level action queues.

## Run and submit

1. Read `DATA_USE.md` and `SETUP.md`.
2. Open the relevant notebook from the Colab link in this repository.
3. Run the notebook top-to-bottom with the required data access.
4. Review the outputs and save the executed notebook back to this repository.
5. Check the repository's GitHub Actions results and ensure only report-safe aggregate outputs are committed.
6. Submit the repository URL on the relevant assignment card.

The W03 GitHub Actions check validates notebook structure and assignment requirements, but cannot prove access to a gated dataset. A successful run against the actual warehouse still requires your approved Hugging Face account and token.
