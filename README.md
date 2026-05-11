# eelkeslassy.github.io

Personal academic site for **Eliott Elkeslassy**, built with **[al-folio](https://github.com/alshedivat/al-folio)** and deployed to **https://eelkeslassy.github.io** via GitHub Actions (`Deploy site` workflow → `gh-pages` branch).

## Edit

- Global settings: `_config.yml`
- Home page: `_pages/about.md`
- Research, proposal, projects, CV: `_pages/research.md`, `_pages/research-proposal.md`, `_pages/projects.md`, `_pages/cv.md`
- Social links: `_data/socials.yml`
- GitHub repo cards: `_data/repositories.yml`

## Local preview

Use Docker per [al-folio INSTALL.md](https://github.com/alshedivat/al-folio/blob/main/INSTALL.md) (`docker compose up`), or Ruby + `bundle install && bundle exec jekyll serve`.

## GitHub settings

**Actions → General → Workflow permissions:** allow **read and write** so the deploy workflow can push to `gh-pages`.

**Settings → Pages:** source = **Deploy from a branch** → **`gh-pages`** → **`/ (root)`** (after the first successful workflow run).
