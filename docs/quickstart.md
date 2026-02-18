---
sidebar_position: 4
---

# Quickstart

This quickstart mirrors the upstream `tollama/tollama` workflow for local setup
and first forecast.

## Prerequisites

- Python 3.11
- A Unix-like shell (examples use bash/zsh)

## Install

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
```

## Start Daemon

```bash
tollama serve
```

Default base URL is `http://localhost:11435` and API base is
`http://localhost:11435/api`.

## Model Lifecycle (Ollama-style)

```bash
tollama list
tollama pull mock
tollama show mock
tollama run mock --input examples/request.json --no-stream
tollama ps
tollama rm mock
```

## Forecast API Call

```bash
curl -s http://localhost:11435/api/forecast \
  -H 'content-type: application/json' \
  -d @examples/chronos2_request.json
```

## Example: Chronos-2

```bash
python -m pip install -e ".[dev,runner_torch]"
tollama serve
tollama pull chronos2
tollama run chronos2 --input examples/chronos2_request.json --no-stream
```

## Useful Commands

```bash
curl http://localhost:11435/api/version
tollama info
tollama info --json
ruff check .
pytest -q
```

## Reference

Product and architecture details:
[https://github.com/tollama/tollama](https://github.com/tollama/tollama)
