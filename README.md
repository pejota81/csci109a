# CSCI 109A — Group 13 Data Science Project

This repository is the home for Group 13's CSCI 109A data science project. The
project question, data sources, methods, and findings will be documented here as
the work develops.

## Environment setup

The shared environment is defined in `pyproject.toml`; `uv.lock` pins the resolved
versions. Python 3.12 and 3.13 are supported. This is a notebook project, not an
installable Python package.

### Recommended: uv

Install [uv](https://docs.astral.sh/uv/getting-started/installation/), then run
these commands from the repository root:

```bash
uv sync --locked
uv run --locked jupyter lab
```

uv creates `.venv` and can download a compatible Python if needed. The environment
includes analysis libraries, Jupyter, `openpyxl` for the Excel data dictionary,
and `python-pptx` and Pillow for slide export. The notebooks download the public
NSCG data on first use, so an internet connection is needed for that step.

In VS Code, select the project's `.venv` interpreter and choose that environment
as the notebook's Python kernel. Restart an already-running kernel after syncing
dependencies. Install dependencies through the project setup, not notebook
`pip install --user` cells.

### Alternative: pip

With Python 3.12 or 3.13, create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyterlab
```

On Windows, activate with `.venv\Scripts\Activate.ps1` in PowerShell instead.
`requirements.txt` is generated from the lockfile; do not edit it separately.

### Changing dependencies

Add a shared dependency and refresh the pip-compatible export:

```bash
uv add package-name
uv export --locked --no-hashes --no-emit-project --output-file requirements.txt
```

Include `pyproject.toml`, `uv.lock`, and the regenerated `requirements.txt` in the
same commit. After pulling changes, run `uv sync --locked` again. Do not commit
`.venv` or other local environment files.

## Suggested organization

- `data/` — project data, with its source and any processing documented
- `notebooks/` — exploratory analysis and experiments
- `src/` — reusable analysis code
- `reports/` — figures, results, and project write-ups

Keep raw data unchanged where possible, and do not commit private or restricted
data.
