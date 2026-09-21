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
- **Phase 4 — Static images/gallery: done.** Added 3 real photos (`culto-casa-nueva.jpg`, `equipo-arreglando-casa.jpg`, `ceremonia-mesa-kids.jpg`, resized/compressed with `sips`, ~200-300KB each) and `src/components/Gallery.astro` (static 3-photo grid, no carousel — matches MVP scope). Committed and pushed to `develop` by the maintainer directly.
- **Phase 5 — Assembly & responsive QA: done.** Hero + Ministries + Gallery assembled in `index.astro`. Mobile responsiveness verified by the maintainer on a real phone (LAN IP) since browser-automation viewport resizing was unreliable in this environment — see git history for details if that ever needs revisiting.
- **Phase 6 — CI/CD: done. Site is live.** `.github/workflows/deploy.yml` builds with `withastro/action` (pinned to Node 22 — Astro 7 requires >=22.12, GH runners default to Node 20) and deploys via `actions/deploy-pages` on push to `main`. Repo visibility switched to **public** (GitHub Pages is not available on private repos on the Free plan). `main`'s `github-pages` environment deployment-branch-policy was updated to allow `main` (GitHub defaulted it to `develop`, the repo's default branch, when Pages was first enabled). Live at **https://fehrmann11.github.io/iglesia-landing-page/**.
- **Branching model going forward:** feature branches → `develop` (day-to-day work) → fast-forward `develop` into `main` when ready to publish (pushing `main` is what triggers the deploy).
- **Phase 3.5 — Calendar section: done, added after initial MVP review.** `src/components/Calendar.astro`: static list (date badge + weekday/time) **plus a month-grid view with a toggle button** (list ⇄ grid, both built from the same event data), wired into `index.astro` between Ministries and Gallery. **Dates are illustrative/sample data (late Sept), not real** — replace before sharing the link widely. Third-party (non-git) editing of the calendar is still an Iteration 2 open decision — see `docs/roadmap.md`.
  - Grid days with an activity also show a CSS-only hover/focus popover (title + time), no JS — `position:relative` on the day cell, `position:absolute` popover shown via `:hover`/`:focus-visible`.
  - **Learning:** Ministries' "Consulta horarios" was styled like a link (bold, brand color) but was plain text — looked actionable, did nothing. The maintainer caught this before sharing with church leadership. Fixed by linking it to `#calendario`. General rule going forward: never style static text to *look* interactive (colored/bold like a CTA) unless it actually does something — visually-actionable-but-inert elements read as broken to users.
  - Gotcha found: toggling `.hidden` on an element whose CSS also sets `display: flex`/`grid` directly does nothing, because the author rule beats the UA `[hidden]{display:none}` rule at equal specificity. Fix: scope the display rule to `:not([hidden])`.
  - Also corrected a factual error: assumed Sept 21 2026 was a Sunday without checking — it's actually a Monday. Verify weekdays with `date -j -f "%Y-%m-%d" ...` before hardcoding sample dates again.
- Iteration 1 (MVP) tasks.md is now fully complete — see `docs/roadmap.md` for Iteration 2+ (carousel, events, prédicas, calendar third-party editing, donations).

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
