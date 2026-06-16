---
mode: agent
description: Add a new HTML page to the Leigh Services website
---

# Add a New Page

You are adding a new page to the **Leigh Services** static website. Follow all rules below exactly.

## Rules

1. **Branch first**: Create a `feature/add-<page-name>` branch from `staging` before making any edits.
2. **Template structure**: Every new page must include:
   - `<header id="header">` with the logo link to `index.html` and the `#menu` nav toggle
   - `<nav id="menu">` with links to `index.html` (Home) and `generic.html` (Meet the Team), **plus** a link to the new page
   - `<footer id="footer">` — identical to the footer in `index.html`
   - All script tags at the bottom: `jquery.min.js`, `browser.min.js`, `breakpoints.min.js`, `util.js`, `main.js`
3. **Nav update required**: Add the new page link to the nav in **both** `index.html` and `generic.html` as well as the new file.
4. **CSS**: Link `assets/css/main.css` in the `<head>`. Add page-specific styles in a `<style>` block in the `<head>` — do not modify SCSS files.
5. **No contact details**: Do not add email addresses or phone numbers.
6. **External links**: Must have `target="_blank" rel="noopener noreferrer"`.
7. **Images**: Place in `images/` named as `descriptor.jpg` (lowercase, no spaces).
8. **Do not commit `main.css`**: If you need a shared style change, flag it as a separate SCSS task.

## After creating the page

1. Open a PR from your feature branch targeting `staging` (not `master`).
2. PR title format: `feat: add <page-name> page`
3. PR description must include: purpose of the page, files created/modified, and nav changes made.
4. The `pr-checks` CI must pass before merging.
