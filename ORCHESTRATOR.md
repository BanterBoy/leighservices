# ORCHESTRATOR.md

> Living memory for the Leigh Services A.I. orchestrator agent.
> Maintained per [.github/agents/LeighServicesAIagent.md](.github/agents/LeighServicesAIagent.md).
> Update this file after every subagent completion or user decision **before** responding.

---

## Repo Identity

| Property | Value |
|---|---|
| Site | leigh-services.com |
| Repo | BanterBoy/leighservices |
| Type | Static GitHub Pages — HTML5 + SCSS + jQuery |
| Theme | Stellar (HTML5 UP) |
| Local build system | None |
| SCSS compilation | CI only (GitHub Actions) |

---

## Branch Strategy

```
feature/xxx  →  staging  →  master (production)
```

- **`master`**: production. Deploys to leigh-services.com on push. Protected — requires PR + CI pass + 1 review.
- **`staging`**: integration. Auto-deploys to staging GitHub Pages on push.
- **Feature branches**: all work happens here. Named `feature/description` or `fix/description`. PRs target `staging`, never `master`.
- **Production promotion**: PR from `staging` → `master`. Requires manual approval in the `production` GitHub Environment before the deploy runs.
- **Release tags**: CI auto-creates `v1.YYYY.MM.DD[-N]` on every production deploy.

---

## Pages

| File | Purpose |
|---|---|
| `index.html` | Homepage — hero video banner, highlights, CTA, testimonials |
| `team.html` | Meet the Team |
| `services.html` | Services overview |
| `certifications.html` | Certifications |
| `case-studies.html` | Case studies |
| `testimonials.html` | Testimonials |
| `blog.html` | Blog |
| `contact.html` | Contact |
| `generic.html` | Reusable template skeleton |
| `elements.html` | Component showcase (not a public page) |

---

## CI/CD Workflows

### `pr-checks.yml` — runs on PRs to `staging` or `master`
1. SCSS compile check (`sass assets/sass/main.scss /tmp/main-check.css`)
2. HTML lint (`html-validate index.html generic.html`)
- **This must pass before any PR can be merged.**

### `build-staging.yml` — runs on push to `staging`
1. Compile SCSS → `assets/css/main.css` (CI owns this file — never commit it manually)
2. Deploy to staging GitHub Pages
3. Post preview URL comment on open PRs targeting `staging`

### `deploy-production.yml` — runs on push to `master`
1. Compile SCSS → `assets/css/main.css`
2. Deploy to production GitHub Pages (leigh-services.com)
3. Auto-create release tag `v1.YYYY.MM.DD[-N]`
- Requires manual approval in the `production` GitHub Environment gate.

---

## SCSS Architecture

Import order in `assets/sass/main.scss`:

```
libs/ → base/ → components/ → layout/
```

| Layer | Key files |
|---|---|
| `libs/` | `_vars.scss` (colours, sizes), `_mixins.scss`, `_breakpoints.scss`, `_functions.scss` |
| `base/` | `_reset.scss`, `_page.scss`, `_typography.scss` |
| `components/` | `_button.scss`, `_form.scss`, `_box.scss`, `_highlights.scss`, `_testimonials.scss`, … |
| `layout/` | `_header.scss`, `_banner.scss`, `_menu.scss`, `_footer.scss`, `_main.scss`, … |

Key tokens:
- `accent1 = #ce1b28`, `accent2 = #111111`
- 7 breakpoint levels — use `@include breakpoint('<=medium')`
- `@include color(accent1)` cascades to ALL components — handle with care
- Vendor prefixes via `@include vendor()`

---

## Module Conventions

- **CSS classes**: BEM-like — `.button`, `.button.primary`, `.button.fit`
- **Utility classes**: `.wrapper`, `.inner`, `.fit`, `.small`, `.alt`
- **SASS helpers**: `_size()`, `_palette()` functions; `@include vendor()` for prefixes
- **JS**: jQuery-based. Plugins in `assets/js/util.js` (navList, panel). Initialized in `assets/js/main.js`.
- **Analytics**: centralized in `assets/js/metrics.js` (GTM-5NBQFP8F)
- **Fonts**: Font Awesome 4.x loaded from `assets/css/font-awesome.min.css`
- **External links**: must have `target="_blank" rel="noopener noreferrer"`
- **Images**: profile photos named `firstnamelastname.jpg` in `images/`. Use `object-fit: cover; object-position: center top`
- **No frameworks**: do not add React, Vue, Bootstrap, Tailwind, or any bundler

---

## Content Owners

| Person | Role | Links |
|---|---|---|
| Luke Leigh | Infrastructure Engineer, Rail Delivery Group | LinkedIn `/in/lukeleigh`, GitHub `BanterBoy`, Blog `blog.lukeleigh.com`, PowerShell Gallery |
| Mark Leigh | Senior Data Engineer & Security Specialist (CompTIA Security+, CREST CPSA) | LinkedIn `/in/markleigh` |

- **Never include email addresses or phone numbers on any page.**
- Footer must include: Leigh Services name, address (63 Archer Avenue, Southend on Sea, Essex SS2 4QU), social links.

---

## Known Fragile Areas

1. **`assets/css/main.css` is CI-owned.** Never commit it. SCSS changes without a CI run have zero effect on the live site.
2. **`body` padding-top must equal `header-height` (3.25rem).** Mismatch causes layout shift.
3. **Menu is JS-only.** No `<noscript>` fallback.
4. **`.is-preload` class** depends on `main.js` executing successfully. If JS fails, animations freeze.
5. **`banner.mp4`** — performance risk on mobile; do not add additional video assets without testing.
6. **`pr-checks.yml` targets `generic.html` for HTML lint**, but the site's actual shared-page template is `generic.html`. If it is renamed or replaced, update the workflow.
7. **`CNAME` and `keybase.txt`** must not be removed — they control domain routing and identity verification.

---

## Agents & Prompts

| Path | Purpose |
|---|---|
| `.github/agents/LeighServicesAIagent.md` | Orchestrator agent definition — role, workflow, and branch rules |
| `.github/copilot-instructions.md` | Repo-wide Copilot instructions (auto-attached to every chat) |
| `.github/prompts/` | Any stored prompt files |

---

## Decision Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-06-17 | Created ORCHESTRATOR.md | User requested initialization so agent contract matches reality |
| 2026-06-17 | Analytics centralized into `assets/js/metrics.js` (GTM-5NBQFP8F) | Feature branch `feature/centralize-analytics`, merged via PR #8 |

---

## Current Task State

| Status | Task | Branch | Notes |
|---|---|---|---|
| ✅ Complete | Initialize ORCHESTRATOR.md | `feature/init-orchestrator` | PR to `staging` pending |

---

*Last updated: 2026-06-17 — ORCHESTRATOR.md initialized.*
