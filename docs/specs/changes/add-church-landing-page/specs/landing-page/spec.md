# Delta for landing-page

> Scope: Iteration 1 (MVP) only. Requirements for the carousel, events, prédicas, editable calendar and donations are intentionally **not** included here — they are tracked as future iterations in `docs/roadmap.md` and will land as their own delta specs when implemented.

## ADDED Requirements

### Requirement: Public landing page access

The system SHALL serve a public landing page reachable without authentication, presenting the church's identity and ministries to any visitor.

#### Scenario: Visitor opens the site

- GIVEN a visitor with a link to the published site
- WHEN they open the URL in a browser
- THEN the landing page loads without requiring login or credentials
- AND the page renders correctly on both mobile (~375px width) and desktop viewports

### Requirement: Hero and about section

The system SHALL present a hero section identifying the church (name, logo, short tagline/description).

#### Scenario: Visitor views the hero section

- GIVEN the landing page is loaded
- WHEN the visitor views the top of the page
- THEN the church's name, logo, and a short description are visible

### Requirement: Static ministries and activities information

The system SHALL present the church's recurring ministries as static content: general meeting, kids ministry ("mesa kids"), youth meeting, and women's meeting.

#### Scenario: Visitor views ministries section

- GIVEN the landing page is loaded
- WHEN the visitor scrolls to the ministries section
- THEN each ministry (general meeting, kids, youth, women) is listed with a short description
- AND this content is static (defined directly in the page, not sourced from a dynamic content collection)

### Requirement: Static images (logo and sample photos)

The system SHALL display a small, fixed set of images (church logo and a handful of representative photos) sourced from images committed to the repository, without interactive carousel navigation.

#### Scenario: Visitor views site images

- GIVEN a logo and a small set of sample images have been added to the repository
- WHEN the landing page is loaded
- THEN those images are visibly rendered on the page

### Requirement: Automated deployment on change

The system SHALL automatically build and publish the site to its public hosting target whenever a change is pushed to the main branch.

#### Scenario: Content or code change is pushed to main

- GIVEN a commit is pushed to the `main` branch
- WHEN the CI/CD pipeline runs
- THEN the site is built and deployed to the public hosting URL without manual steps
- AND the previously published version remains available if the build fails (no broken deploy replaces a working site)

### Requirement: Zero-cost hosting and image delivery

The system SHALL be hosted and SHALL serve its images using only free-tier services, with no recurring monetary cost for this trial phase.

#### Scenario: Site is reachable at no cost

- GIVEN the site has been deployed via the CI/CD pipeline
- WHEN a visitor accesses the published URL
- THEN the page and all its images load successfully
- AND no paid service tier is required to keep the site and its images publicly available
