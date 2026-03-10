# Tollama AI Website

Static marketing site and product microsite bundle for Tollama AI.

This repository is the GitHub Pages site for [www.tollama.com](https://www.tollama.com). It contains the landing page plus product pages for the current Tollama AI stack:

- `tollama`: TSFM runtime and unified forecasting API
- `spline-lstm`: spline + LSTM/GRU forecasting pipeline
- `Market Calibration Agent`: prediction-market calibration and trust scoring
- `tollama-eval`: forecasting evaluator and benchmarking layer

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

The site currently presents Tollama AI as an AI platform for predictive industries with:

- a landing page covering platform, agents, solutions, roadmap, and open source positioning
- a `tollama` product page for the forecasting runtime
- a `spline-lstm` product page for the neural forecasting pipeline
- a `Market Calibration Agent` page for prediction-market trust scoring
- a newly added `Forecasting Evaluator Agent` page for `tollama-eval`

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
