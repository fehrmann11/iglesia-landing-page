## Project

Public landing page for a church, built with Astro (static-first, near-zero shipped JS). Content is in Spanish. Deploys to GitHub Pages (`fehrmann11/iglesia-landing-page`) via GitHub Actions on push to `main`. No backend, no auth, no database in this phase.

**Specs live in `docs/specs/`** (Spec-Driven Development):

- `docs/specs/changes/add-church-landing-page/` — current change: proposal, delta spec, design, tasks (Iteration 1 / MVP scope only)
- `docs/roadmap.md` — future iterations (carousel + image storage provider TBD, events, prédicas, editable calendar, donations) and open decisions not yet resolved

Read `docs/specs/changes/add-church-landing-page/tasks.md` before picking up work — it's the source of truth for what's done and what's next in this iteration.

## Current status (updated per phase)

- **Phase 1 — Project scaffolding: done.** Astro project initialized (TypeScript strict), `astro.config.mjs` set for GitHub Pages (`site`/`base`), base `Layout.astro` with responsive meta + global styles, favicon and page title/description wired. Repo created at github.com/fehrmann11/iglesia-landing-page (private), `develop` is the default branch.
- **Phase 2 — Hero section: done.** `src/components/Hero.astro` built with the church's real logo and Facebook cover photo (`public/images/logo.png`, `public/images/hero-cover.jpg`, resized/compressed with `sips`). Church name: "Casa de Restauración". Tagline: "Bienvenido a Casa" (matches their Facebook cover).
- **Phase 3 — Ministries section: done.** `src/components/Ministries.astro`: responsive card grid (1 col mobile → 2 → 4 on desktop) for the 4 ministries (Reunión General, Mesa Kids, Jóvenes, Mujeres). Schedules are placeholder ("Consulta horarios") per the maintainer's choice — no real day/time data yet.
- **Phase 4 — Static images/gallery: done, pending review.** Added 3 real photos (`culto-casa-nueva.jpg`, `equipo-arreglando-casa.jpg`, `ceremonia-mesa-kids.jpg`, resized/compressed with `sips`, ~200-300KB each) and a new `src/components/Gallery.astro` (static 3-photo grid, no carousel — matches MVP scope) wired into `index.astro`. **Not committed yet** — the maintainer wants to review the working tree before this lands in git.
- Phase 5 (final assembly / responsive QA) and beyond: not started yet — see tasks.md.

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
