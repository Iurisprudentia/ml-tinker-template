# Data Science Project Template

A minimal, conventional scaffold for local classical ML projects. The goal is a clean desk — enough structure to keep work organised and reproducible, not enough to become an engineering project in its own right.

## Using This Template

**Via GitHub:**

Click the green **Use this template** button at the top of the repo, or via the CLI:

```bash
gh repo create my-new-project --template your-username/ds-project-template --clone
cd my-new-project
```

**Via local script:**

```bash
cp -r ~/Templates/ds-scaffold my-new-project
cd my-new-project
git init && git add . && git commit -m "Initial scaffold"
```

Once cloned, set up the environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -e .
```

That last command installs your own `src/` package in editable mode, meaning any notebook in the project can import from it with no `sys.path` hacks.

---

## Project Structure

```
project-root/
├── .venv/                  # virtual environment — never committed
├── .gitignore
├── README.md
├── pyproject.toml          # dependencies and package config
├── data/
│   ├── raw/                # source data — immutable, never edited in place
│   ├── interim/            # intermediate transforms
│   └── processed/          # final feature sets, ready for modelling
├── notebooks/              # EDA and exploration
├── models/                 # saved model artifacts
└── ml_project/             # reusable package code — starts empty on purpose
    └── __init__.py
```

### The one rule that matters most

**`data/raw/` is sacred.** Whatever you download or receive goes there and is never modified. Every transformation reads from `raw/` and writes elsewhere. This means you can always reproduce your pipeline from scratch and can never corrupt the source by accident.

---

## Dependencies

Edit `pyproject.toml` to add or remove packages, then reinstall:

```bash
pip install -e .
```

To pin a snapshot of the current environment for exact reproducibility:

```bash
pip freeze > requirements-lock.txt
```

---

## Conventions

**`ml_project/` starts empty.** Only move code into it when a notebook cell has earned reuse — when you've written the same logic three times and the pattern is obvious. Abstractions get extracted from working code, never designed up front.

**Notebooks are for exploration.** Code that needs to run reliably or be reused belongs in `ml_project/`, not buried in a notebook cell.

**`data/` and `models/` are gitignored.** Data is too large and sometimes sensitive for version control. The directory structure is tracked via `.gitkeep` files; the contents are not.

**Label your notebook cells by intent.** Distinguish between EDA scaffolding (readable labels, throwaway transforms) and pipeline steps (cleaning rules, feature engineering) that will need to run on future data. They look identical in code and have very different fates.

---

## Starting a New Project

1. Spin up from the template
2. Rename `ml_project/` to match your project name and update `pyproject.toml` accordingly
3. Drop your raw data into `data/raw/`
4. Open `notebooks/` and start with EDA — examine the target first, hunt leakage second, derive cleaning rules third
5. Only touch `ml_project/` when something has genuinely earned its place there

---

## What This Template Deliberately Omits

- No config system or settings module
- No custom CV framework
- No logging framework
- No base classes or factory patterns
- No Makefile
- No type annotations

These are all things that feel productive to build and consistently delay actual modelling. Add them only if a specific, concrete pain point demands them — not in anticipation of a pain point that may never arrive.