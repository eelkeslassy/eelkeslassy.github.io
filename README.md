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

## GitHub settings (required — or the website will not change)

The **`main`** branch only holds **source** for al-folio. The **built site** is pushed to the **`gh-pages`** branch by the **Deploy site** workflow. GitHub Pages must publish **`gh-pages`**, not `main`.

1. **Settings → Actions → General → Workflow permissions:** **Read and write** (so the workflow can update `gh-pages`).
2. **Settings → Pages → Build and deployment:** **Source** = **Deploy from a branch**.
3. **Branch** = **`gh-pages`** / **`/ (root)`** — **not** `main`.  
   - If you leave **main**, GitHub’s legacy Jekyll builds the wrong (old) site — that is why you still see the previous theme.
4. Wait 1–5 minutes, then hard-refresh the site (**Cmd+Shift+R** / **Ctrl+Shift+R**).

Check the latest build: [Actions → Deploy site](https://github.com/eelkeslassy/eelkeslassy.github.io/actions/workflows/deploy.yml).
