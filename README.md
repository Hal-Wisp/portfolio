# Portfolio site

A Quarto website for trade compliance and logistics analytics projects.

## Two rules

**Never commit employer data.** No vendor lists, part numbers, BOMs, invoices,
drawings, or entry records. Given ITAR and EAR exposure, anything touching
defense articles is a serious problem on a public site, not just an NDA issue.
Public federal data and synthetic data only.

**Never commit API keys.** Read them from the environment:

```python
import os
API_KEY = os.environ["TRADE_GOV_API_KEY"]
```

Keep them in a `.env` file, which is already gitignored.

## Structure

```
.
├── _quarto.yml                 site config, nav, fonts
├── styles.scss                 theme
├── index.qmd                   homepage and project index
├── about.qmd                   background and experience
├── _template/                  copy this to start a project
├── projects/
│   ├── denied-party-screening/ furthest along
│   ├── tariff-exposure/
│   ├── border-throughput/
│   └── landed-cost-model/
├── data/                       public and synthetic data only
└── .github/workflows/          build and deploy
```
