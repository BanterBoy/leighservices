---
mode: agent
description: Update text content, bios, skills or links on the Leigh Services website
---

# Update Site Content

You are editing content on the **Leigh Services** static website. Follow all rules below exactly.

## Scope of this prompt
Use this prompt when asked to:
- Update a person's bio, job title or employer
- Add, remove or change skill tags
- Update social or professional links
- Edit service descriptions on the homepage
- Change footer text or address

## Rules

1. **Branch first**: Create a `feature/update-<brief-description>` branch from `staging` before making any edits.
2. **Files you may edit**: `index.html`, `generic.html`. No other files.
3. **Files you must not touch**: `assets/css/main.css`, `assets/sass/**`, any JS files, `CNAME`, `keybase.txt`.
4. **No contact details on pages**: Do not add email addresses or phone numbers to any page.
5. **External links**: Must have `target="_blank" rel="noopener noreferrer"`.
6. **Nav consistency**: Both `index.html` and `generic.html` must have identical nav links. If nav changes, update both files.
7. **Footer consistency**: Both pages must have identical footers. If footer changes, update both files.
8. **Profile photos**: Referenced as `images/lukeleigh.jpg` and `images/markleigh.jpg`. Do not change filenames.
9. **Do not commit `main.css`**: CI compiles SCSS. If you need a style change, note it as a separate task.

## After editing

1. Open a PR from your feature branch targeting `staging` (not `master`).
2. PR title format: `content: <what changed>` (e.g. `content: update Luke bio and skills`).
3. PR description must include: what changed, which files were edited, and why.
4. The `pr-checks` CI must pass before merging.
