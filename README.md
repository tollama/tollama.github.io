# tollama — Ollama for Time Series

`v0.1` · **Open Source** · **MIT License**

**Ollama for Time Series.**  
Run state-of-the-art foundation models locally.

`tollama` is a local-first forecasting daemon with a unified REST API. Pull, serve, and query **Chronos**, **TimesFM**, **Moirai**, **Sundial**, **Granite TTM**, and **Toto** — all through one CLI and HTTP interface.

<p align="center">
  <a href="#quickstart"><strong>Quickstart</strong></a> ·
  <a href="#want-a-deeper-dive"><strong>Deeper dive</strong></a> ·
  <a href="#model-registry"><strong>Models</strong></a> ·
  <a href="#features"><strong>Features</strong></a> ·
  <a href="#rest-api"><strong>API</strong></a> ·
  <a href="#compatibility-matrix"><strong>Matrix</strong></a>
</p>

---

## What is tollama?

`tollama` runs a **FastAPI daemon** on `http://127.0.0.1:11435` by default and exposes an **Ollama-style API under `/api`**.

Typical workflow:

1. **Serve** the daemon
2. **Pull** a model from the registry
3. **Forecast** via HTTP or the CLI

---

## Quickstart

### 1) Install

**Option A — pip**

```bash
pip install tollama
```

**Option B — from source (dev)**

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
```

### 2) Start the daemon

```bash
tollama serve
# check:
curl http://localhost:11435/api/version
```

### 3) Pull + forecast

**HTTP**

```bash
# pull
curl -s http://localhost:11435/api/pull   -H 'content-type: application/json'   -d '{ "name": "chronos2" }'

# forecast (example payload)
curl -s http://localhost:11435/api/forecast   -H 'content-type: application/json'   -d @examples/chronos2_request.json
```

**CLI**

```bash
tollama pull chronos2
tollama run chronos2 --input request.json
```

---

## Want a deeper dive?

Documentation lives in the repo — it’s versioned, reviewable, and stays close to the code.

- **Run guide:** [`docs/how-to-run.md`](docs/how-to-run.md)  
  Install runner families, pull all TSFM registry models, and troubleshoot common issues.
- **Covariates contract:** [`docs/covariates.md`](docs/covariates.md)  
  Exact rules, family mappings, compatibility matrix, and strict vs best-effort behavior.
- **Roadmap:** [`roadmap.md`](roadmap.md)  
  Implementation-aware progress tracker and planned v1 hardening items.

---

## Model registry

Six foundation models are highlighted in the landing page.

| Registry name | Vendor / family |
|---|---|
| `chronos2` | Amazon · Chronos-2 |
| `granite-ttm-r2` | IBM · Granite TTM |
| `timesfm-2.5-200m` | Google · TimesFM 2.5 |
| `moirai-2.0-R-small` | Salesforce · Uni2TS / Moirai |
| `sundial-base-128m` | THUML · Sundial |
| `toto-open-base-1.0` | Datadog · Toto |

Pull any model with:

```bash
tollama pull chronos2
```

---

## Features

- **⚡ Ollama-style UX**  
  Familiar `pull`, `run`, `serve`, `list`, `rm` commands for managing time series models locally — no cloud required.
- **🔒 Isolated runtimes**  
  Each model family gets its own venv under `~/.tollama/runtimes/`. No dependency conflicts.
- **📡 Unified HTTP API**  
  FastAPI daemon with consistent `/api/*` endpoints — drop-in across all supported model families.
- **📊 Rich covariates**  
  Unified past + future covariates contract across runners. Best-effort or strict validation modes.
- **🤗 Hugging Face integration**  
  Snapshot pull with progress streaming, proxy support, offline mode, and HF token auth.
- **🔭 Diagnostics built-in**  
  `tollama info` output with daemon health, loaded models, runner statuses, and pull defaults.

---

## REST API

### Forecast with a single POST

Send time series data with covariates, receive probabilistic forecasts. Consistent request/response schema across model families.

Example request body for `POST /api/forecast`:

```json
{
  "model": "timesfm-2.5-200m",
  "horizon": 7,
  "series": [{
    "id": "store_001",
    "freq": "D",
    "target": [120, 135, 142],
    "past_covariates": {
      "promo": [0, 1, 0]
    },
    "future_covariates": {
      "promo": [1, 1, 0, 0, 1, 0, 1]
    }
  }],
  "parameters": {
    "covariates_mode": "best_effort"
  }
}
```

---

## Compatibility matrix

| Model family | Past numeric | Past categorical | Known-future numeric | Known-future categorical |
|---|:---:|:---:|:---:|:---:|
| Chronos-2 | ✓ | ✓ | ✓ | ✓ |
| Granite TTM | ✓ | — | ✓ | — |
| TimesFM 2.5 | ✓ | — | ✓ | — |
| Uni2TS / Moirai | ✓ | — | ✓ | — |
| Sundial | — | — | — | — |
| Toto Open Base | ✓ | — | — | — |

---

## Landing page

This repo can ship a nice GitHub Pages landing page from `docs/index.html`.

GitHub → **Settings → Pages** → **Deploy from a branch** → Branch: `main` (or default) / Folder: **`/docs`**

---

## License

MIT — see [`LICENSE`](LICENSE).
