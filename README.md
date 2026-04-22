# himalaya-girard.com

Personal website of Himalaya Girard, Research Assistant at the Donders Institute. Deployed at <https://himalaya-girard.com>.

The repository serves two things:

1. **Main site** — a bilingual (EN / FR) research site documenting a project on trust and risk decoupling, built around Prospect Theory.
2. **That One Paper** subsite, at `/that-one-paper/` — a self-contained brand island for a short-form video series from the Donders Institute.

---

## Stack

- [Astro 5](https://astro.build/) (static site generator)
- [Tailwind CSS 4](https://tailwindcss.com/) (via `@tailwindcss/vite`)
- Typography: Figtree (main site), Bebas Neue + DM Serif Display + Archivo + JetBrains Mono (That One Paper)
- Hosted on GitHub Pages with a custom domain (`CNAME` in `public/`)
- Continuous deployment via GitHub Actions (`.github/workflows/deploy.yml`)

---

## Getting started

```bash
npm install
npm run dev       # local dev server on http://localhost:4321
npm run build     # production build to ./dist
npm run preview   # serve the production build locally
```

Node 20 or newer recommended. No environment variables are required.

---

## Project structure

```
.
├── public/                        Static assets served as-is
│   ├── CNAME                      Custom domain for GitHub Pages
│   ├── favicon.png
│   ├── images/                    Profile photos
│   ├── references.json            Bibliography (EN)
│   ├── references-fr.json         Bibliography (FR)
│   └── that-one-paper/wordmark/   That One Paper brand assets (PNG)
│
├── src/
│   ├── components/                Reusable Astro components
│   ├── i18n/translations.ts       Key-based EN / FR dictionary + t() helper
│   ├── layouts/
│   │   ├── Layout.astro           Main site layout (Figtree, custom cursor)
│   │   └── TOPLayout.astro        That One Paper layout (separate font stack)
│   ├── pages/                     Main site pages, English
│   │   ├── index.astro
│   │   ├── about.astro
│   │   ├── explore.astro          Interactive Prospect Theory demo
│   │   ├── journey.astro          Research timeline (+ 5 sub-pages)
│   │   ├── references.astro      Searchable bibliography
│   │   ├── fr/                    Mirror of the main site in French
│   │   └── that-one-paper/        Brand-island landing page
│   └── styles/                    global.css + that-one-paper.css
│
├── STYLE_GUIDE.md                 Design rules for the main site
└── astro.config.mjs               i18n locales, site URL, Tailwind plugin
```

---

## Design system

All design decisions for the main site are codified in [`STYLE_GUIDE.md`](./STYLE_GUIDE.md). The four-colour palette, typography, component patterns, and hard rules (no `bg-white`, no `rounded-full` on rectangles, no em-dashes in copy) are enforced there.

The `/that-one-paper/` subsite uses a separate brand system and its own layout (`TOPLayout.astro`). Do not mix tokens or components between the two.

---

## Internationalisation

The site is bilingual:

- Default locale: English. Served at the root (no `/en/` prefix).
- French locale at `/fr/...`. Mirrors every page of the main site.
- Configured in `astro.config.mjs` under `i18n`.

Adding a translated string:

1. Open `src/i18n/translations.ts`.
2. Add the key to both the `en` and `fr` objects.
3. Reference it with `t('key.name', lang)` from any page or component.

Writing copy:
- Keep the key namespaces short and grouped (`home.*`, `about.*`, `references.*`).
- HTML in translated strings is allowed (used with `set:html`) for inline emphasis.
- Follow the style guide when adding French copy too: no em-dashes, no bright-contrast violations, no off-palette colour markup.

---

## Deployment

Deployment is automatic on push to `main`:

1. GitHub Actions builds the site (`astro build`).
2. The output is published to GitHub Pages.
3. The `public/CNAME` file keeps the custom domain `himalaya-girard.com` attached.

Do not disable the CNAME file or change the Pages source; doing so detaches the custom domain from the repo.

---

## Contributing

- All source code, comments, variable names, and commit messages: **English**.
- User-facing copy: English at the root, French under `/fr/`.
- Follow `STYLE_GUIDE.md`. When in doubt, match the nearest existing component.
- Run `npm run build` locally before pushing — the site fails to deploy if the build errors.

---

## Contact

Himalaya Girard — <himalaya.girard@donders.ru.nl>
