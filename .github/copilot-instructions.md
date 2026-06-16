# Copilot Instructions — leighservices

This is the repository for **leigh-services.com** — a static GitHub Pages site for Leigh Services, an IT infrastructure and data engineering consultancy.

---

## Repository Overview

- **Type**: Static site (plain HTML + CSS + vanilla JS). No framework, no npm, no build system locally.
- **Domain**: leigh-services.com (CNAME → BanterBoy/leighservices master branch)
- **Pages**: `index.html` (home), `generic.html` (Meet the Team)
- **Styling**: SASS source lives in `assets/sass/`. Compiled output is `assets/css/main.css`.
- **Icons**: Font Awesome 4.x (loaded from `assets/css/font-awesome.min.css`)
- **JS**: jQuery-based, no bundler. Scripts live in `assets/js/`.
- **Images**: `images/` directory. Profile photos: `lukeleigh.jpg`, `markleigh.jpg`.

---

## Critical Rules

### Never edit `assets/css/main.css` directly
SCSS is compiled to `main.css` by CI (GitHub Actions). Editing `main.css` directly will be overwritten on the next deployment. All style changes must go in `assets/sass/`.

### No npm / no build commands needed locally
There is no `package.json`. Do not add one unless explicitly asked. Do not suggest running `npm install`, `npm build`, or any bundler commands.

### HTML pages are self-contained
Each HTML page includes its own `<style>` block for page-specific CSS and links to `assets/css/main.css` for the shared theme. Do not extract page-specific styles to SASS unless there is a clear shared pattern.

---

## Branch Strategy

```
feature/xxx  →  staging  →  master (production)
```

- **`master`**: production branch. Deploys to leigh-services.com. Protected — requires PR + CI pass + 1 review approval. Never push directly.
- **`staging`**: integration branch. Auto-deploys to the staging GitHub Pages environment for preview. Protected — requires CI pass.
- **Feature branches**: all work happens here. Name as `feature/description` or `fix/description`. PRs target `staging`, not `master`.
- **Promoting to production**: open a PR from `staging` → `master`. Requires manual approval in GitHub Environments before the production deploy runs.

---

## Content Conventions

### Pages
- Every page must include the shared `<header id="header">`, `<nav id="menu">`, and `<footer id="footer">`.
- Nav links: `index.html` (Home) and `generic.html` (Meet the Team) only. Update both files if nav changes.
- Footer must include: Leigh Services name, address (63 Archer Avenue, Southend on Sea, Essex SS2 4QU), social/professional links. No email addresses or phone numbers on the public site.
- All external links must have `target="_blank" rel="noopener noreferrer"`.

### Images
- Profile photos go in `images/` named as `firstnamelastname.jpg` (lowercase, no spaces).
- Use `object-fit: cover; object-position: center top` for all profile photo crops.
- Prefer aspect-ratio wrapper divs (`padding-top: X%`) over fixed pixel heights for responsive images.

### Owners
- **Luke Leigh**: Infrastructure Engineer at Rail Delivery Group. Focus: on-prem to M365 migrations, PowerShell automation, system management. Links: LinkedIn (`/in/lukeleigh`), GitHub (`BanterBoy`), Blog (`blog.lukeleigh.com`), PowerShell Gallery.
- **Mark Leigh**: Senior Data Engineer & Security Specialist. CompTIA Security+, CREST CPSA. Focus: data platform integrity, DevSecOps, GCP, SAS. Links: LinkedIn (`/in/markleigh`).
- Do not include email addresses or phone numbers for either owner on the site.

### Copyright year
The footer copyright currently reads 2024. Update if explicitly asked.

---

## GitHub Workflow

- All content changes should be made on a `feature/` branch, then PR'd to `staging`.
- When creating a PR, use a descriptive title and include a brief summary of what changed and why.
- The `pr-checks` workflow must pass before merging.
- After verifying the staging preview, open a PR from `staging` → `master` to go live.
- Tag releases from `master` after each production deployment. Format: `v1.YYYY.MM.DD`.

---

## What Not to Do

- Do not add JavaScript frameworks (React, Vue, etc.)
- Do not add a CSS framework (Bootstrap, Tailwind, etc.)
- Do not commit `assets/css/main.css` as part of style changes — CI owns this file
- Do not add email addresses or phone numbers to any page
- Do not push directly to `staging` or `master`
- Do not remove the CNAME file or keybase.txt
