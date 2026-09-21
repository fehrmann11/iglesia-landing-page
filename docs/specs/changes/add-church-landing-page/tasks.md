# Tasks: add-church-landing-page (Iteration 1 — MVP)

> Scope: only what's needed for a shippable demo to validate interest with church leadership. Carousel, events, prédicas, calendar and donations are **not** in this list — see `docs/roadmap.md` for Iteration 2/3.
>
> Difficulty: **S** (< 1h), **M** (1–3h), **L** (half day+)

## 1. Project scaffolding

- [ ] 1.1 Initialize Astro project with TypeScript (`npm create astro@latest`) — **S**
- [ ] 1.2 Configure `astro.config.mjs` for GitHub Pages (`site`, `base`) — **S**
- [ ] 1.3 Set up base layout (`src/layouts/Layout.astro`) with responsive meta tags and global styles — **M**
- [ ] 1.4 Add basic favicon and page `<title>`/meta description — **S**

## 2. Hero / about section

- [ ] 2.1 Add logo and a short church description/tagline as static copy — **S**
- [ ] 2.2 Build `src/components/Hero.astro` (logo, name, tagline, responsive) — **M**

## 3. Ministries section

- [ ] 3.1 Write static copy for the 4 ministries (general meeting, mesa kids, jóvenes, mujeres) — **S**
- [ ] 3.2 Build `src/components/Ministries.astro` (card/grid layout, responsive) — **M**

## 4. Static images

- [ ] 4.1 Collect and optimize (compress) logo + 2–3 sample photos — **S**
- [ ] 4.2 Add images under `public/images/` and reference them from Hero/Ministries — **S**

## 5. Assembly

- [ ] 5.1 Assemble Hero + Ministries into `src/pages/index.astro` — **S**
- [ ] 5.2 Basic responsive QA pass (mobile ~375px and desktop) — **M**

## 6. CI/CD

- [ ] 6.1 Create `.github/workflows/deploy.yml` (build + deploy to GitHub Pages on push to `main`) — **M**
- [ ] 6.2 Enable GitHub Pages (Actions source) in repository settings — **S**
- [ ] 6.3 Verify a push to `main` triggers a successful automated deploy — **S**

## 7. Documentation

- [ ] 7.1 Create `docs/roadmap.md` with Iteration 2/3 items and open decisions (image storage, editable calendar) — **S**
- [ ] 7.2 Add a `README.md` with local dev and deploy instructions — **S**

## 8. Verification

- [ ] 8.1 Verify the site loads with no auth and renders on mobile + desktop — **S**
- [ ] 8.2 Verify images load correctly on the deployed (published) URL, not just locally — **S**
- [ ] 8.3 Verify against specs (completeness, correctness, coherence) — **S**
- [ ] 8.4 Share the deployed link with church leadership for feedback — **S**
