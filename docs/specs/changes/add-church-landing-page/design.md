# Design: add-church-landing-page

## Technical Approach

The project is greenfield, so this design establishes the initial architecture. **This design covers Iteration 1 (MVP) only.** The site is built with **Astro** as a static-first multi-page site. For Iteration 1, all content (hero copy, ministries descriptions) is written directly in the page/component markup — no content collections yet, since there is no repeating per-item data (events, prédicas) in this iteration. Content Collections are deferred to Iteration 2, when events/prédicas/calendar entries are introduced (see `docs/roadmap.md`).

Images (logo, a handful of sample photos) are committed directly into the repository under `public/images/` for this iteration. This avoids signing up for any third-party storage account and is genuinely free — Astro copies `public/` assets as-is and the hosting platform serves them from its CDN. **This is explicitly a placeholder for Iteration 1 only.** The carousel and its external image-storage provider (Cloudinary is the current front-runner — see `docs/roadmap.md` § Open Decisions) are deferred to Iteration 2, once there's a real, larger set of photos to manage and the repo-storage approach stops being convenient.

Deployment targets **GitHub Pages**, built and published by a **GitHub Actions** workflow that runs on every push to `main`. This satisfies the explicit requirement for a GitHub-based CI/CD loop, needs no third-party account beyond GitHub itself, and is free for public repositories indefinitely.

## Architecture Decisions

### Decision 1: Framework — Astro over Next.js/React

- **Context:** The site is almost entirely informational/static content with no authenticated user flows in this phase. The user is a programmer, not a designer, and wants the simplest path to a fast, easily-updatable site.
- **Chosen option:** Astro — ships zero JS by default, first-class Markdown/content collections fit the events/activities/prédicas content model directly, and it can still embed a React/Vue/Svelte/vanilla island for the carousel without adopting a full SPA framework.
- **Discarded alternatives:**
  - **Next.js** — More powerful (SSR, API routes, server actions) but that power targets exactly the backoffice/dynamic-app phase this change explicitly excludes; heavier mental model and build for a purely static v1.
  - **Plain React (CRA/Vite SPA)** — Ships a JS bundle for a page that is mostly static content; worse SEO and initial load for a public marketing-style page with no client state to justify a full SPA.

### Decision 2: Image storage — repository (`public/images/`) for Iteration 1 only, provider TBD for Iteration 2

- **Context:** The user wants to minimize cost. For Iteration 1 there are only a handful of images (logo + a few sample photos), updated infrequently and only by the developer, so no external service is worth the setup cost yet. For Iteration 2 (interactive carousel, potentially scaling to ~5GB of photos), a dedicated provider becomes worthwhile.
- **Chosen option (Iteration 1):** Store the small image set in `public/images/` in the repo, referenced directly from the page markup. Zero external dependencies, zero cost, images are versioned with the code and served by the same free hosting CDN.
- **Deferred decision (Iteration 2 — see `docs/roadmap.md` § Open Decisions):** front-runner is **Cloudinary free tier** (~25GB/month combined storage+bandwidth+transformations, automatic image optimization/responsive delivery — valuable for a carousel). Runner-up is **Firebase Storage** (5GB storage free, per-project quota isolation — relevant if multiple independent landing pages are built later and quota isolation per project matters more than Cloudinary's larger shared pool). **Supabase Storage** (1GB free) was ruled out at this target scale — too small.
- **Discarded for Iteration 1:**
  - **Cloudinary / Firebase / Supabase now** — Adds an external account/API key to manage for no real benefit while there are only a handful of static images and no dynamic upload flow yet.
  - **GitHub raw URLs / jsDelivr CDN pointing at the repo** — Works but is more fragile (rate limits, no cache invalidation control, awkward URLs) than simply letting the static host serve `public/`.

### Decision 3: Hosting & CI/CD — GitHub Pages via GitHub Actions

- **Context:** The user explicitly asked for a GitHub Actions-driven CI/CD pipeline, and wants $0 recurring cost during the trial phase.
- **Chosen option:** GitHub Pages, deployed via the official `withastro/action` (or `actions/deploy-pages`) GitHub Actions workflow triggered on push to `main`. Free indefinitely for a public repo, no third-party account needed, and matches the CI/CD requirement literally.
- **Discarded alternatives:**
  - **Vercel/Netlify with their native Git integration** — Also free-tier and arguably smoother DX (preview deploys per PR), but their default flow deploys via their own platform hook rather than a GitHub Actions workflow the user owns and can inspect/extend; can be reconsidered later if preview deployments per PR become valuable.

## Files Involved (Iteration 1 / MVP)

| Action | File | Description |
| --- | --- | --- |
| Create | `package.json`, `astro.config.mjs`, `tsconfig.json` | Project scaffolding (Astro + TypeScript) |
| Create | `src/pages/index.astro` | Landing page assembling MVP sections |
| Create | `src/components/Hero.astro` | Hero/about section |
| Create | `src/components/Ministries.astro` | Static ministries/activities section |
| Create | `public/images/` | Logo and a handful of sample images (static, no carousel yet) |
| Create | `.github/workflows/deploy.yml` | Build + deploy to GitHub Pages on push to `main` |
| Create | `docs/roadmap.md` | Centralized backlog of future iterations (carousel, events, prédicas, editable calendar, donations, backoffice, payment gateway, image-storage decision) |

> Content Collections (`src/content/`), the Carousel island, Events/Prédicas/Calendar/Donations components are **out of scope for this change** — see `docs/roadmap.md`.

## Risks

| Risk | Probability | Impact | Mitigation |
| --- | --- | --- | --- |
| Repo grows large from binary images over time | Medium | Low | Keep images optimized/compressed; migrate to Cloudinary when volume grows or backoffice is built |
| GitHub Pages free tier limits (bandwidth/build minutes) reached if traffic spikes | Low | Low | Acceptable for a trial; migrate to Vercel/Netlify free tier if needed, no architecture lock-in since Astro output is portable |
| Scope creep into backoffice/payments before validating interest | Medium | Medium | Explicitly out of scope in proposal.md; tracked in `docs/roadmap.md` instead of implemented now |
