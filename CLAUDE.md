# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Install dependencies (first time or after Gemfile changes)
bundle install

# Local dev server with live reload at http://localhost:4000
bundle exec jekyll serve

# Production build (outputs to _site/)
bundle exec jekyll build
```

## Architecture

This is a **Jekyll static site** deployed on GitHub Pages. Pushing to `main` triggers an automatic rebuild and deploy — there is no staging environment.

### How pages are built

Every page is a Markdown file at the root with frontmatter specifying a layout. Jekyll combines that content with the matching layout in `_layouts/`, wrapping it in `_layouts/default.html` (the master template). All pages inherit the nav and footer via `{% include navigation.html %}` and `{% include footer.html %}` in `default.html`.

### Navigation and footer links

Nav links and footer links are **not hardcoded in HTML** — they are driven by YAML data files:
- `_data/navigation.yml` → top navbar (rendered in `_includes/navigation.html`)
- `_data/footer.yml` → "Company" column in footer (rendered in `_includes/footer.html`)

The footer's "Products" column is auto-populated from the `_products/` collection via `site.products`.

### Collections

Two Jekyll collections are configured in `_config.yml`:
- `_products/` — each file becomes a product page using `_layouts/products.html`
- `_teammembers/` — each file becomes a team profile using `_layouts/teammember.html`

Both have `output: true`, meaning they generate their own URLs.

### CDN dependencies with SRI hashes

`_layouts/default.html` loads Bootstrap 4.1.3, jQuery 3.3.1, and Popper.js from CDNs with `integrity` SRI hashes. If you change a CDN URL or version, you must update the corresponding hash or browsers will block the resource.

### Styling

Custom styles live in `_sass/main.scss`. Bootstrap is loaded from CDN (not bundled), so only overrides and custom classes go in the SCSS file.

## Keeping This File Updated
When making architectural changes — new shared files, new patterns, changes to the component model, or new pages — update the relevant section of this file before closing the task.

## Git Workflow

### Branching Rules
- NEVER commit directly to `main`. Always create a feature branch first.
- Before making any edits, verify the current branch with `git status`. If on `main`, create a new branch immediately.
- Branch naming convention: `feature/short-description` or `fix/short-description`
- One branch per task or feature set.

### Commits
- Write clear, descriptive commit messages following the format:
  `type(scope): short description`
  Examples: `feat(nav): add responsive hamburger menu`, `fix(footer): correct broken link`
- Commit logical chunks of work — don't batch unrelated changes.
- Always stage and review changes before committing (`git diff --staged`).

### Pull Requests & Merging
- When a feature or fix is complete and ready to deploy, create a PR from the feature branch into `main`.
- PR title should clearly describe what changed.
- PR description should include: what changed and why. For visual changes, note which pages were affected and confirm they were checked in a browser.
- Only merge via PR — no direct pushes to `main`.
- Self-review is acceptable given the team size — just read the diff before merging.
- Delete the feature branch after a successful merge.

### Deployment Checklist (before merging PR)
1. All changes committed and pushed to the feature branch
2. PR created, diff reviewed, no conflicts with `main`
3. Merge commit created (not squash, to preserve history)
4. Post-merge: `git checkout main && git pull`
5. **GitHub Pages auto-deploys on merge to `main`** — no manual deploy step needed. Verify the live site at the CNAME domain after a minute or two.
