---
sidebar_position: 1
---

# tollama Overview

tollama is a **local-first forecasting daemon + CLI** for running and serving
state-of-the-art time series foundation models.

Canonical project source: [github.com/tollama/tollama](https://github.com/tollama/tollama)

## What It Provides

- FastAPI daemon (`tollamad`) exposing `api/*` endpoints
- Typer CLI (`tollama`) for model lifecycle and forecasting commands
- Pluggable runner families over stdio JSON-lines protocol
- Unified covariates contract with `best_effort` and `strict` handling

## Core Runner Families

- `mock`
- `torch` (Chronos-2 and Granite TTM flows)
- `timesfm`
- `uni2ts` (Moirai family)
- `sundial`
- `toto`

## Key Product Value

- One consistent API and CLI experience across model families
- Local-first operation with per-family isolated runtimes by default
- Practical operations support through `tollama info` and `/api/info`

## Learn More

- [Products & Models](/docs/products)
- [Technology & Architecture](/docs/technology)
- [Quickstart](/docs/quickstart)
