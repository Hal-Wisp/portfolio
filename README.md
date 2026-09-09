# Portfolio site

A Quarto website for trade compliance and logistics analytics projects.
Source for the site published at [your-domain].

## Getting it running

**1. Install Quarto and Python packages**

Download Quarto from [quarto.org/docs/get-started](https://quarto.org/docs/get-started/),
then:

```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

**2. Preview locally**

```bash
quarto preview
```

This opens the site in your browser and reloads as you edit. Run it now — if
anything in the scaffold is broken, this is where you find out, and the error
message names the file and line.

**3. Fill in your details**

Search the repo for these and replace every occurrence:

| Placeholder | Where |
|---|---|
| `YOUR-GITHUB-USERNAME` | `_quarto.yml`, `about.qmd`, every project page |
| `YOUR-LINKEDIN` | `_quarto.yml`, `about.qmd` |
| `site-url` | `_quarto.yml` |

```bash
grep -rn "YOUR-GITHUB-USERNAME\|YOUR-LINKEDIN" --include="*.qmd" --include="*.yml" .
```

## Publishing to GitHub Pages

1. Create a public repo and push this folder to `main`.
2. In the repo: **Settings → Pages → Build and deployment → Source →
   GitHub Actions**.
3. Push. The workflow in `.github/workflows/publish.yml` builds and deploys.

Your site is then at `https://YOUR-GITHUB-USERNAME.github.io/REPO-NAME/`.

### Custom domain

Buy a domain (~$10–15/year; Cloudflare Registrar sells at cost). Then:

- Add a `CNAME` file in the repo root containing just your domain, e.g.
  `jacobgray.dev`
- At your registrar, add an `ALIAS`/`ANAME` record for the apex pointing to
  `YOUR-GITHUB-USERNAME.github.io`, and a `CNAME` record for `www` pointing to
  the same
- In **Settings → Pages**, enter the domain and tick **Enforce HTTPS**
- Update `site-url` in `_quarto.yml`

A resume link reading `jacobgray.dev` is worth the $12.

## Adding a project

```bash
cp -r _template projects/my-new-project
```

Then edit `projects/my-new-project/index.qmd` and add an `.entry` block to
`index.qmd` so it shows on the homepage. Drop the `.pending` class and the
`<span class="status">` once it is finished.

The homepage index is written by hand rather than generated. With a handful of
projects that is simpler and gives full control over the wording; if you get
past about ten, switch to a
[Quarto listing](https://quarto.org/docs/websites/website-listings.html).

## How execution works

`execute: freeze: auto` in `_quarto.yml` means code runs when you render
locally, and the results are cached in `_freeze/`. **Commit that folder.**
GitHub Actions then reuses your cached output instead of re-running analysis
that might need an API key or a large local file.

Code chunks in the scaffold are marked `#| eval: false` so the site builds
before you have written any real analysis. Remove that line from a chunk once
it actually runs.

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
