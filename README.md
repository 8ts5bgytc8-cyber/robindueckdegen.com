# robindueckdegen.com — site prototype v2

This is the second Jekyll prototype for Robin Dueck Degen's personal academic/professional website.

## Page types

The site intentionally uses three visual templates:

1. **Landing template** — the homepage. Professional, summary-oriented, and sidebar-driven.
2. **Index template** — Projects and Blog. Designed for navigation and overview.
3. **Content template** — individual project pages and blog posts. Quieter and optimized for reading substantial work.

## Local preview

With Ruby 3.4.11 active:

```bash
bundle install
bundle exec jekyll serve --livereload
```

Then open `http://localhost:4000`.

Useful pages:

- `/`
- `/projects/`
- `/projects/twisting-theory-of-lie-algebras/`
- `/blog/`
- `/blog/2026/09/25/example-project-note/`

The example blog post is temporary and should be removed once the first real post is ready.


## Mathematics in project pages and blog posts

MathJax is enabled site-wide. In Markdown files, use `$...$` for inline mathematics and `$$...$$` for display mathematics. These delimiters survive Jekyll/kramdown parsing reliably. AMS-style equation tags are enabled.

## Third-party images and sourcing

Third-party images should be accompanied by a visible caption that names the creator/source and links to the source page and license where applicable. Keep an image unchanged unless its license permits derivatives and the required derivative-license terms are understood.


## Removing CV or GitHub before publishing

### Remove the CV
1. Delete `cv/index.md`.
2. Remove the `CV` anchor from `_includes/navigation.html`.
3. The CV-specific CSS in `assets/css/main.css` may be left in place harmlessly, or remove the block beginning `/* CV template */`.

### Remove GitHub
1. In `_config.yml`, change:
   `github_url: "https://github.com/8ts5bgytc8-cyber"`
   to:
   `github_url: ""`
2. Because the templates check whether `site.github_url` is non-empty, the GitHub links disappear automatically from the top navigation, homepage sidebar, footer, and CV page.
3. Restart Jekyll after editing `_config.yml`.
