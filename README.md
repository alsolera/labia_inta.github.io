# AeroML — Data-Driven Fluid Dynamics & Aerodynamics Lab

Jekyll source for **https://aeroml-inta.github.io**.

## Deploying

The repository is named `AeroML-INTA.github.io`, which GitHub serves at the org root,
`https://aeroml-inta.github.io/`, so `_config.yml` sets:

    baseurl: ""

If the repository is ever renamed back to `AeroML-INTA`, it is served from a sub-path
instead and `baseurl` becomes `"/AeroML-INTA"`. Every internal link uses `relative_url`,
so that one line is the only change needed either way.

Deployment runs through `.github/workflows/pages.yml`, which needs the Pages source switched
away from the classic branch build: **Settings → Pages → Build and deployment → Source:
GitHub Actions.** Until that is changed, pushes will not update the live site.

## Running locally

    bundle install
    bundle exec jekyll serve

Then open http://localhost:4000.

## Editing content

Almost nothing lives in the page files. Content is in `_data/`:

| File | What it holds |
| --- | --- |
| `_data/en.yml`, `_data/es.yml` | All interface strings and page copy, per language |
| `_data/research.yml` | Research lines (`title`/`title_es`, `body`/`body_es`) |
| `_data/team.yml` | PI, doctoral researchers, collaborators |
| `_data/publications.yml` | Generated — do not edit by hand |
| `_data/news.yml` | News items, newest first |
| `_data/software.yml` | Repositories and datasets (empty for now) |
| `_data/positions.yml` | Open vacancies (empty for now) |

The pages in `_pages/` are six-line stubs that include a section template; you rarely touch them.

## Publications

Add the BibTeX entry to `files/publications.bib`, then:

    python3 tools/bib2yml.py

This regenerates `_data/publications.yml`. The Publications page groups by year
automatically, and the home page shows the three most recent.

## Images

Drop files into `images/` and reference them from the data files:

* Home hero figure — uncomment `hero:` in `_data/images.yml`.
* Research figures — `image: /images/research/rom.jpg` on any entry in `_data/research.yml`.
* Team photos — `photo: /images/team/name.jpg` on any member in `_data/team.yml`.

Anything without an image renders a neutral striped placeholder, so the layout never breaks.

## Languages

English lives at `/`, Spanish at `/es/`. Each page declares `lang` and `ref` in its front
matter; the header pairs them automatically and renders the EN/ES toggle. To add a page,
create both language stubs with the same `ref` and add the label under `nav:` in both data files.
