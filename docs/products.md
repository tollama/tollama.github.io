---
sidebar_position: 2
---

# Products & Models

tollama serves multiple time series foundation-model families through one
interface.

Source of truth: [tollama/tollama README](https://github.com/tollama/tollama)

## Supported Model Families

| Family | Example Model | Notes |
| --- | --- | --- |
| Chronos-2 | `chronos2` | torch runner |
| Granite TTM | `granite-ttm-r2` | torch runner |
| TimesFM 2.5 | `timesfm-2.5-200m` | dedicated timesfm runner |
| Uni2TS / Moirai | `moirai-2.0-R-small` | dedicated uni2ts runner |
| Sundial | `sundial-base-128m` | dedicated sundial runner |
| Toto | `toto-open-base-1.0` | dedicated toto runner |

## Covariates Compatibility Snapshot

| Family | Past Numeric | Past Categorical | Known-Future Numeric | Known-Future Categorical |
| --- | --- | --- | --- | --- |
| Chronos-2 | Yes | Yes | Yes | Yes |
| Granite TTM | Yes | No | Yes | No |
| TimesFM 2.5 | Yes | No | Yes | No |
| Uni2TS / Moirai | Yes | No | Yes | No |
| Sundial | No | No | No | No |
| Toto Open Base 1.0 | Yes | No | No | No |

## Product Capabilities

- Ollama-style model lifecycle: `pull`, `list`, `show`, `run`, `ps`, `rm`
- Forecasting through one daemon API (`/api/forecast`)
- Pull integration for Hugging Face snapshot-backed registry models
- Persistent pull defaults in `~/.tollama/config.json`
- Diagnostics for integrations via `GET /api/info`

## Integration Snapshot

The upstream repository reports optional E2E integrations re-run on
**February 17, 2026**, including Chronos, Granite, TimesFM, Uni2TS/Moirai, and
Sundial passing; Toto was marked skipped in that run due to missing package.

