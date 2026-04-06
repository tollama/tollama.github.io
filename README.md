# Tollama AI Website

Static marketing site and product microsite bundle for Tollama Core + Trust.

This repository is the GitHub Pages site for [www.tollama.com](https://www.tollama.com). It contains the landing page plus product pages for the current Tollama Core + Trust story:

- `tollama`: the Core OSS front door for preprocess, forecast, benchmark, and route
- `spline-lstm`: preprocessing lineage and spline differentiation
- `Market Calibration Agent`: hero wedge for trust-aware market workflows
- `tollama-eval`: the richer benchmarking and evaluation layer behind Core artifacts

The previous `README.md` described the `tollama` Python package. That is no longer what this repository contains. This repo is now the website source only.

## Site Structure

```text
docs/
  index.html
  CNAME
  product/
    tollama.html
    spline-lstm.html
    market-calibration-agent.html
    forecasting-evaluator-agent.html
DEPLOY.md
```

All pages are hand-authored static HTML with inline CSS. There is no build step, package manifest, or framework runtime in this repository.

## Current Content

The site is being aligned to present Tollama as `Core + Trust` for
forecast-driven time-series workflows, with:

- a landing page and product pages centered on the Core-first workflow
- a `tollama` product page for the OSS Core front door
- a `spline-lstm` page for preprocessing differentiation and lineage
- a `Market Calibration Agent` page for the hero trust wedge
- a `Forecasting Evaluator Agent` page that explains `tollama-eval` as the deeper benchmark layer

## Local Preview

Because the site is static, any simple file server works:

```bash
cd docs
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Deployment

Deploy with GitHub Pages from the `docs/` directory.

1. Push this repository to GitHub.
2. In GitHub, open `Settings -> Pages`.
3. Set `Source` to `Deploy from a branch`.
4. Select the default branch and the `/docs` folder.
5. Save and wait for Pages to publish.

Custom domain is configured via [`docs/CNAME`](docs/CNAME) for `www.tollama.com`.

Additional deployment notes live in [`DEPLOY.md`](DEPLOY.md).

## Notes

- This repository does not contain the application code for the linked products.
- Product pages link out to their respective GitHub repositories under the Tollama organization.
- If you are looking for the `tollama` runtime itself, use the product link on [`docs/product/tollama.html`](docs/product/tollama.html).
