# Leigh Services

Website for **leigh-services.com** — the public presence for Leigh Services, an IT infrastructure and data engineering consultancy.

Live site: [leigh-services.com](https://leigh-services.com)

---

## About

Leigh Services is run by:

- **Luke Leigh** — Infrastructure Engineer. On-prem to M365 migrations, PowerShell automation, system management.
- **Mark Leigh** — Senior Data Engineer & Security Specialist. Data platform integrity, DevSecOps, GCP, SAS. CompTIA Security+, CREST CPSA.

---

## Technology

- **Static site** — plain HTML, CSS, and vanilla JavaScript. No framework, no npm, no build system.
- **Theme** — [Stellar](https://html5up.net/stellar) by HTML5 UP (CCA 3.0 licence).
- **Styling** — SCSS source in `assets/sass/`, compiled to `assets/css/main.css` by CI.
- **Icons** — Font Awesome 4.x.
- **JS** — jQuery-based scripts in `assets/js/`.
- **Hosting** — GitHub Pages, `master` branch → `leigh-services.com` (via `CNAME`).

---

## Repository Structure

```
/
├── index.html            # Homepage
├── team.html             # Meet the Team
├── services.html         # Services
├── case-studies.html     # Case Studies
├── certifications.html   # Certifications
├── testimonials.html     # Testimonials
├── blog.html             # Blog
├── contact.html          # Contact
├── elements.html         # Component showcase (not a public page)
├── assets/
│   ├── sass/             # SCSS source (edit these for style changes)
│   │   ├── main.scss     # Entry point
│   │   ├── base/
│   │   ├── components/
│   │   ├── layout/
│   │   └── libs/
│   ├── css/
│   │   └── main.css      # Compiled output — DO NOT edit directly
│   └── js/               # jQuery scripts
├── images/               # Site images and profile photos
├── CNAME                 # leigh-services.com domain mapping
└── .github/
    └── workflows/        # CI: pr-checks, build-staging, deploy-production
```

---

## Branch Strategy

```
feature/xxx  →  staging  →  master (production)
```

| Branch                | Purpose                                                                           |
| --------------------- | --------------------------------------------------------------------------------- |
| `master`              | Production. Deploys to leigh-services.com. Protected — requires PR + CI + review. |
| `staging`             | Integration. Auto-deploys to the staging preview environment. Protected.          |
| `feature/*` / `fix/*` | All work happens here. PRs target `staging`.                                      |

To promote to production, open a PR from `staging` → `master`. Manual approval in the GitHub `production` environment is required before the deploy runs.

---

## Making Changes

1. Create a branch: `git checkout -b feature/your-change`
2. Make edits to HTML or SCSS files.
3. **Never edit `assets/css/main.css` directly** — CI compiles it from SCSS on every push.
4. Open a PR targeting `staging`.
5. The `pr-checks` workflow must pass (SCSS compile check + HTML validation).
6. After verifying the staging preview, open a PR from `staging` → `master`.

---

## CI Workflows

| Workflow            | Trigger                     | What it does                                          |
| ------------------- | --------------------------- | ----------------------------------------------------- |
| `pr-checks`         | PR to `staging` or `master` | Compiles SCSS, validates HTML                         |
| `build-staging`     | Push to `staging`           | Builds and deploys to staging Pages environment       |
| `deploy-production` | PR merge to `master`        | Deploys to production (requires environment approval) |

---

## Credits

- Theme: [Stellar by HTML5 UP](https://html5up.net/stellar) — [CCA 3.0 licence](https://html5up.net/license)
- Images: [Unsplash](https://unsplash.com) — see [CREDITS.txt](CREDITS.txt)
- Video: [Coverr](http://coverr.co)
