# MomentumIQ Website

Marketing site for [MomentumIQ](https://momentumiq.ai) — built with Jekyll, deployed on GitHub Pages.

## Local development

Requires Ruby 3.x with Bundler.

```bash
# Install dependencies
bundle install

# Start dev server with live reload at http://localhost:4000
bundle exec jekyll serve --livereload

# Production build (outputs to _site/, which is gitignored)
bundle exec jekyll build
```

## How it works

Jekyll static site. Every page is a Markdown file at the root with frontmatter specifying a layout. The layouts in `_layouts/` wrap content in `_layouts/default.html`, which includes the shared nav and footer.

**Key directories:**

| Path | What |
|------|------|
| `_layouts/` | Page templates (home, about, products, splash, blog, post, teammember) |
| `_includes/` | Shared partials (navigation, footer) |
| `_products/` | One `.md` file per product — generates a page + appears in nav/home/about automatically |
| `_teammembers/` | One `.md` file per team member |
| `_data/` | YAML data for nav links (`navigation.yml`) and footer company links (`footer.yml`) |
| `_sass/main.scss` | All custom styles (Bootstrap 4.1.3 loaded from CDN) |

## Deployment

Pushing (or merging a PR) to `main` triggers an automatic GitHub Pages rebuild and deploy. No manual deploy step. Verify the live site at the CNAME domain a minute or two after merge.

## Adding a product

Create `_products/YourProduct.md` — the product will automatically appear in the footer, home page product cards, and about page. See `CLAUDE.md` for the full frontmatter schema.

## Full project docs

See [`CLAUDE.md`](./CLAUDE.md) for architecture details, git workflow, and contributor guidelines.
