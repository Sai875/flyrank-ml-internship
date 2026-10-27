# Setup — this repository

This guide is for working in [Sai875/flyrank-ml-internship](https://github.com/Sai875/flyrank-ml-internship). The repository does not include the legacy starter pipeline, `requirements.txt`, `scripts/run_all.py`, or a committed raw CSV. Use the notebook workflows linked below rather than instructions that assume those paths exist.

## 1. Open and save notebooks

Open the notebook from its link in the repository README, or use these direct Colab links:

- [W03 — Data Contract](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w03_data_contract.ipynb)
- [Capstone](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/capstone.ipynb)
- [W07 — Content Action Playbook](https://colab.research.google.com/github/Sai875/flyrank-ml-internship/blob/main/work/notebooks/w07_action_playbook.ipynb)

Run a notebook from top to bottom, review the outputs, then use **File → Save a copy in GitHub** to save your notebook changes to this repository. The GitHub Actions workflows also execute the capstone and W07 notebooks and commit only their executed notebooks, aggregate metrics, and report-safe figures.

## 2. Public starter data — capstone and W07

The capstone and W07 notebooks download the public anonymized starter CSV from [FlyRank/internship-starter](https://huggingface.co/datasets/FlyRank/internship-starter) when a local copy is not available. The file is placed in `data/raw/content_refresh_anonymized.csv` for runtime use only.

**Do not commit the CSV.** It is excluded from Git intentionally. The workflows remove the temporary file before committing generated outputs.

## 3. Gated warehouse data — W03

The W03 data-contract notebook uses the larger [FlyRank/internship-warehouse](https://huggingface.co/datasets/FlyRank/internship-warehouse) dataset. Access is gated.

1. Sign in to Hugging Face and open the dataset page above.
2. Complete the access form, use **`FlyRank ML Internship 2026`** as the affiliation, accept the data-use terms, and wait for access approval.
3. After access is approved, create a Hugging Face **READ** token under Settings → Access Tokens.
4. In Colab's **Secrets** panel (key icon), add the token under the name `HF_TOKEN` and allow the notebook to read it.
5. Restart the runtime and run W03 from the first cell.

Never paste the token into notebook code, markdown, outputs, or a public issue.

### Optional automatic W03 execution in GitHub Actions

To let [.github/workflows/w03-data-contract.yml](.github/workflows/w03-data-contract.yml) execute the gated notebook automatically, add a repository Actions secret named `HF_TOKEN` with the approved READ token:

**Repository → Settings → Secrets and variables → Actions → New repository secret**

If that secret is absent, the workflow fails early with the exact setup instructions in the GitHub Actions job summary rather than silently skipping execution. It checks that the token can download a small warehouse dimension before starting the notebook. Do not send the token in chat or commit it to the repository.

## 4. Checks and outputs

- `notebook-validation.yml` checks notebook format and assignment-specific requirements.
- `capstone-auto-run.yml` runs the public-starter capstone, validates grouped-split metrics and leakage controls, validates the figure, and commits report-safe outputs.
- `w07-action-playbook.yml` runs W07 and validates aggregate metrics, tier counts, and the figure.
- `w03-data-contract.yml` runs W03 only when the approved `HF_TOKEN` secret is configured.

Only aggregate metrics, public-safe figures, and notebooks without secrets or raw records should be committed. Follow [DATA_USE.md](DATA_USE.md) before working with data.
