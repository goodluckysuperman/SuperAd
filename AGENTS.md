# KDDTAAC Development Conventions

This repository uses a fixed Conda environment for Python development.

## Environment Rule

- Run Python commands with `conda run -n kddtaac --no-capture-output`.
- Treat `kddtaac` as the default environment for scripts, notebooks, checks, and tests.
- When verifying the environment, prefer commands that explicitly target `kddtaac` instead of relying on the current shell state.

## Dependency Rule

- Every Python package used by the project must be recorded in `requirements.txt`.
- If a package is added, removed, or upgraded in the `kddtaac` environment, update `requirements.txt` in the same change.
- Keep `requirements.txt` aligned with the environment so the setup remains reproducible.

## Project Organization Rule

- Keep exploratory work, reusable code, and generated outputs in separate top-level areas.
- Use `NOTEBOOKS/` for exploratory notebooks only.
- Use `SRC/` for reusable Python modules once logic needs to be shared across notebooks or scripts.
- Use `OUTPUTS/` for generated figures, tables, submissions, logs, and other run artifacts.
- Do not scatter generated files under `DOC/`, `DATA/`, or next to notebooks unless there is a strong reason.

## Phase Directory Rule

- Organize work by project phase using numeric prefixes so the sequence stays clear as the repository grows.
- Recommended phase folders:
  - `NOTEBOOKS/01_eda`
  - `NOTEBOOKS/02_baseline`
  - `NOTEBOOKS/03_features`
  - `NOTEBOOKS/04_modeling`
  - `OUTPUTS/01_eda`
  - `OUTPUTS/02_baseline`
  - `OUTPUTS/03_features`
  - `OUTPUTS/04_modeling`
- Keep one stage focused on one purpose. Do not mix baseline training, feature engineering, and later modeling experiments in the same notebook folder.

## Notebook and Artifact Rule

- Name notebooks with a numeric prefix and a short purpose, for example `01_data_overview.ipynb`.
- Prefer a small number of clearly scoped notebooks instead of many overlapping drafts.
- If the same code appears in more than one notebook, move it into `SRC/`.
- Save notebook outputs such as charts, csv summaries, and reports under the matching `OUTPUTS/` phase folder.

## Data Directory Rule

- Treat `DATA/` as the place for input datasets and derived datasets only.
- Keep raw or provided samples separate from transformed data.
- Recommended subfolders as the project grows:
  - `DATA/raw`
  - `DATA/interim`
  - `DATA/processed`
- Do not modify provided sample data in place unless the task explicitly requires it.

## Recommended Command Style

- Check Python:
  `conda run -n kddtaac --no-capture-output python --version`
- Install dependencies:
  `conda run -n kddtaac --no-capture-output pip install -r requirements.txt`
- Run a script:
  `conda run -n kddtaac --no-capture-output python path\\to\\script.py`

## Why This Exists

These rules reduce ambiguity about which Python environment is active and make it easier to reproduce the project on the same machine or a new one.
They also keep the repository understandable as exploratory work turns into reusable code and experiment outputs.
