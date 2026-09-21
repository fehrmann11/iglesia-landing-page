# Roadmap — Church Landing Page

Centralized backlog of future iterations, beyond the Iteration 1 MVP (see `docs/specs/changes/add-church-landing-page/`). Each iteration below becomes its own SDD change (`proposal.md` + delta `spec.md` + `design.md` + `tasks.md`) when it's time to build it.

## Iteration 1 — MVP (in progress)

Hero, static ministries section, a handful of static images, GitHub Actions deploy to GitHub Pages. See `docs/specs/changes/add-church-landing-page/`. Goal: something to show church leadership and validate interest.

## Iteration 2 — Content-driven site

- **Interactive image carousel** (replaces the static image block), backed by an external image storage provider instead of the repo
- **Events** as content-driven entries (Astro Content Collections)
- **Prédicas** (sermons) as content-driven entries
- **Calendar of activities**, editable by a third party without touching git — decision pending (see Open Decisions below)

## Iteration 3 — Polish & donations

- Donations section (informational: bank details / external link, no payment processing)
- Visual design polish, SEO pass
- Documentation for non-technical content editing (whichever mechanism Iteration 2 lands on)

## Later / not yet scoped

- Authenticated backoffice/CMS (separate project)
- Payment gateway integration for donations
- Multi-language support
- Custom purchased domain

---

## Open Decisions

### Image storage provider (for Iteration 2's carousel)

Evaluated at a target scale of up to ~5GB of photos:

| Option | Free tier | Notes |
| --- | --- | --- |
| **Cloudinary** (current front-runner) | ~25 credits/month (≈25GB storage+bandwidth+transformations, shared) | Automatic image optimization/responsive delivery — good fit for a carousel. Quota is per-account, shared across all projects using that account. |
| **Firebase Storage** | 5GB storage free, ~1GB/day download, **per Firebase project** | Exactly at the 5GB target. Per-project quota isolation is useful if we build multiple independent landing pages later and want to avoid one site eating another's shared quota. |
| Supabase Storage | 1GB free | Ruled out — too small for the 5GB target. |
| ImageKit.io | ~20GB storage+bandwidth combined | Viable alternative to Cloudinary, not yet compared in depth. |

**Multi-landing-page cost note:** none of these become paid just from adding more landing pages, as long as total usage (across all sites, if sharing one account) stays under the free tier. Cloudinary's free tier is shared across everything on one account; Firebase isolates quota per project. Revisit this once there's a concrete second landing page.

**Status:** not decided yet — defer until Iteration 2 actually needs the carousel, and re-evaluate with real photo volume/traffic in hand.

### Calendar edited by a third party

The person maintaining the calendar may not be the developer and won't use git. Options to evaluate in Iteration 2:

- Google Sheets (public, read at build time, generate content from it) — no-code for the editor, needs a small build-time fetch script
- Airtable free tier — similar to Sheets, nicer UI
- Plain JSON/Markdown in the repo, edited via GitHub's web UI — no new tooling, but requires teaching the editor basic GitHub web editing

**Status:** not decided yet — depends on who ends up maintaining the calendar and their comfort with each tool.
