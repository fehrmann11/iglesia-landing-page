# Proposal: add-church-landing-page

## Intent

The church currently has no public web presence. We need a low-cost (ideally $0) public landing page that presents the church, its schedule of activities, and its ministries (kids, youth, women), so it can be shown to church leadership as a trial to validate interest before investing further. The site must be trivially easy to update (content changes via git commits, auto-deployed) since the maintainer is a solo volunteer developer, not a designer.

## Scope — Iteration 1 (MVP)

This change covers **only Iteration 1**, whose sole goal is to have something deployable to show church leadership and validate interest, before investing in richer content features. Everything beyond this is tracked in `docs/roadmap.md` and will become separate changes.

- A single, mostly-static public landing page (no login) built with a content-focused framework
- Hero/about section
- Static ministries/activities section (mesa kids, youth meeting, women's meeting, general meeting) — plain content, no per-event data model yet
- Logo + a handful of static images (no interactive carousel yet — see Out of Scope)
- GitHub Actions pipeline that builds and deploys automatically on push to the main branch
- Deployment to a free hosting tier
- A `docs/roadmap.md` file centralizing future iterations (carousel, events, prédicas, editable calendar, donations, backoffice, payment gateway, image-storage decision at scale) for iterative delivery

## Out of Scope (deferred to later iterations, see roadmap)

- Interactive image carousel with external image storage (Iteration 2)
- Events list and prédicas as content-driven entries (Iteration 2)
- Calendar of activities editable by a third party without git access (Iteration 2/3 — needs a decision: Google Sheets/Airtable vs. GitHub-edited JSON)
- Donations section with informational details (Iteration 3)
- Authenticated backoffice / CMS for non-technical content editors (tracked as a separate future change)
- Payment gateway integration for donations
- Interactive/embedded third-party calendar (e.g. Google Calendar)
- Multi-language support
- Custom purchased domain (uses the free subdomain provided by the hosting platform)

## Approach

Build the landing page as a static-first site using **Astro** (chosen for near-zero shipped JavaScript, and the ability to add interactive islands later — e.g. the carousel — without adopting a full SPA framework). For Iteration 1, content is plain static markup/frontmatter committed to the repository; no external CMS or paid storage service is introduced yet. A GitHub Actions workflow builds the site on every push to `main` and deploys it to a free static hosting target (GitHub Pages). This keeps recurring cost at $0 while still enabling a full CI/CD loop the user explicitly asked for, and gives a shippable demo fast.

## Impact

- **Affected users:** Church leadership and visitors (public read-only access); the volunteer developer (content updates via git)
- **Affected modules:** New project (greenfield) — no existing codebase affected
- **Risk:** Low — no user data is collected, no authentication, no payments; the only risk is scope creep into backoffice/payments before validating interest, mitigated by keeping those explicitly out of scope

## Source

- **Jira:** N/A — personal/church project, not tracked in Jira
