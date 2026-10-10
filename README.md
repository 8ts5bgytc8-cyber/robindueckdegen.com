# Site maintenance

## Branch and authorship rules

- Make site changes only on `DevelopmentBranch`; never modify `main`.
- Do not generate prose that visitors could assume was written by the site owner.

## Blog and unlisted notes

- Blog entries belong in `_posts/YYYY-MM-DD-slug.md`, with `layout: post` and the owner's title and content. Jekyll's post date controls ordering and future-post exclusion. They appear automatically at `/blog/`. The blog index and posts have no navigation bars. The main site does not link to the blog or automatically list blog entries; open `/blog/` directly.
- Unlisted notes belong in `_notes/slug.md`. They inherit `layout: post` and `noindex: true`, and normally use `/notes/slug/`. They are not included in the blog, homepage post listings, related-post listings, or previous/next blog navigation.
- Link a note manually from a project when wanted. A Markdown link can use `[your link text]({{ '/notes/slug/' | relative_url }})`.
- An explicit `permalink` overrides the default note URL. The existing finance note retains `/blog/2026/09/25/GatheringDataForFinancialExperiments/` to preserve old links despite now being an unlisted note.
- Unlisted notes are publicly accessible by URL. `noindex` is not access control.
- `/projects/` lists published pages using either `project` or `research-project`. Existing research URLs remain valid.

## Build

Use Ruby and Bundler versions specified by `.ruby-version` and `Gemfile.lock`:

```sh
bundle install
bundle exec jekyll build
```

The tracked `_site/` directory is generated output. Rebuild it from the current source before previewing or deploying it. Wrangler serves `_site/`.
