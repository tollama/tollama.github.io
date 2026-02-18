---
sidebar_position: 3
---

# Technology & Architecture

tollama is designed as a local-first serving system with a stable API/CLI
surface and pluggable model-family runners.

## Stack

- Python package with PEP 621 metadata (`pyproject.toml`)
- FastAPI daemon (`tollamad`)
- Typer CLI (`tollama`)
- Runner subprocesses speaking newline-delimited JSON over stdio
- Ruff + Pytest + CI checks

## Runtime Model

- Default mode is family-level isolated runtimes
- Runtimes are created under `~/.tollama/runtimes/<family>/venv/`
- `daemon.auto_bootstrap=true` enables first-use bootstrap per family
- Shared single-venv mode is available by disabling `auto_bootstrap`

## API Surface

Primary lifecycle and forecasting endpoints:

- `GET /api/version`
- `GET /api/info`
- `GET /api/tags`
- `GET /api/ps`
- `POST /api/show`
- `POST /api/pull`
- `DELETE /api/delete`
- `POST /api/forecast`

Backward-compatible endpoints:

- `GET /v1/health`
- `POST /v1/forecast`

## Covariates Contract

tollama uses a unified covariates contract across families:

- `past_covariates[name]` must match target length
- `future_covariates[name]` must match horizon length
- every future key must also exist in past covariates
- arrays must be type-consistent (numeric-only or string-only)
- `covariates_mode=best_effort` ignores unsupported inputs with warnings
- `covariates_mode=strict` returns HTTP `400` on unsupported inputs

## Internal Layout

```text
src/tollama/
  cli/
  core/
  daemon/
  runners/
```

- `core`: schemas and protocol helpers
- `daemon`: API layer and runner supervision
- `runners`: model-family runtime implementations
- `cli`: command entry points for operators and developers

