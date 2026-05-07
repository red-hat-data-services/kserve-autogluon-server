# kserve-autogluon-server

KServe (Kubernetes inference) fork with an **AutoGluon** model server in `python/autogluonserver/`. This file orients agents quickly; it does not document every module.

## Build & test commands

**AutoGluon server (preferred loop for `python/autogluonserver/` changes)**

| Action | Command |
|--------|---------|
| Install deps | `cd python/autogluonserver && uv sync --active --group test` |
| Test (typecheck + pytest) | `make test` (same directory) |
| Test one file | `pytest tests/test_model.py -W ignore` |
| Typecheck only | `make type_check` |

**Fast single-file checks (Python, AutoGluon tree)** — use after `uv sync --active --group test` in `python/autogluonserver/`; no full build, no scanning the whole repo.

| Action | Command |
|--------|---------|
| Lint one file | `make lint-file FILE=autogluonserver/tabular_model.py` |
| Format one file | `make format-file FILE=autogluonserver/tabular_model.py` |
| Typecheck one file | `make typecheck-file FILE=autogluonserver/tabular_model.py` |

`lint-file` / `format-file` use **`uvx ruff`** (no prior install). **`typecheck-file`** uses **`mypy`** like `make type_check` — use after `uv sync --active --group test` so `mypy` is on your PATH.

Equivalent from **repository root** (same `ruff.toml` rules):  
`uvx ruff check --config ruff.toml python/autogluonserver/autogluonserver/tabular_model.py` — swap `check` for `format` to format.  
Single-file mypy from `python/autogluonserver/` (with venv active):  
`mypy --ignore-missing-imports autogluonserver/tabular_model.py`.

**Repo-wide Go / controller work**

| Action | Command |
|--------|---------|
| Full Go test suite | `make test` from **repository root** (also runs fmt, vet, manifests, envtest — heavy) |
| Format Python (optional before PR) | `make py-fmt` from root (`ruff format`, scopes `./python` …) |
| Lint Python (optional before PR) | `make py-lint` from root (`ruff check`) |
| Lint one Python file from root | `uvx ruff check --config ruff.toml path/to/file.py` (fast; no compile step) |

**Go (package-scoped, faster than full `make precommit`):** e.g. `go vet ./pkg/apis/serving/v1beta1/...` — Go vets packages, not isolated single files.

**Do not use for a tight agent loop:** root `make test` when you only touched Python; **E2E** under `test/e2e/` (needs cluster / infra).

## Key conventions

- **`python/autogluonserver`** depends on local packages via `[tool.uv.sources]` in `pyproject.toml` (`../kserve`, `../storage`). Run installs **from that directory** so path deps resolve.
- **Match layer to validation:** Python server → tests under `python/autogluonserver/`; Go or CRDs → root toolchain and `make test` when appropriate.
- **New Python files** in this tree follow the existing Apache-2.0 header block like other `autogluonserver` modules.
- **Imports:** extend patterns already used in `autogluonserver/` (KServe `InferRequest` / errors, pandas/numpy for tabular/time series).

## Architecture (routing)

| If you are changing… | Start in… |
|---------------------|-----------|
| Tabular / time series serving logic | `python/autogluonserver/autogluonserver/` (`tabular_model.py`, `timeseries_model.py`, …) |
| Tests for that server | `python/autogluonserver/tests/` |
| Shared KServe Python runtime | `python/kserve/` |
| Controllers, APIs, CRDs | `pkg/`, `config/`; see upstream KServe docs for depth |

This repo is **large**. Prefer reading **neighbor files** and package READMEs over exploring top-down.

## PR / CI

**GitHub Actions** (`.github/workflows/autogluonserver.yml`) runs on PRs and pushes that touch `python/autogluonserver/`:

| Job | What it runs |
|-----|----------------|
| **Lint (Ruff)** | `uvx ruff check --config ruff.toml python/autogluonserver` — no install of AutoGluon; failures name file + rule. |
| **Mypy & pytest** | `uv sync --group test`, then `mypy`, then `pytest --tb=short -q` — separate steps so logs stay short and the failing gate is obvious. |

If **`uv sync`** fails resolving packages (e.g. `autogluon.tabular==…+rhaiv`), configure repository secret **`UV_EXTRA_INDEX_URL`** to your team’s PyPI index (see also `python/autogluonserver/autogluon-all-requirements.txt` for index hints).

Contributor norms: [KServe Contributor Guide](https://kserve.github.io/website/docs/developer-guide/contribution).

## For AI agents

- Prefer **`AGENTS.md`** as the single root context file; **`CLAUDE.md`** only imports this repo’s `@AGENTS.md`.
- After edits under `python/autogluonserver/`, run **`make lint-file`**, **`make typecheck-file`**, or **`make test`** as appropriate; prefer single-file checks during iteration.
- Do not add empty scaffolding docs or governance-only files unless asked.
