# Causes and Conditions — site source

Jekyll source for causesandconditions.com, served by GitHub Pages from the
`aiHTE/aiHTE.github.io` repository. Uses only the default GitHub Pages build
pipeline — push to `main` and it deploys.

## Site map

| Section     | Where content lives          | How it renders                                    |
|-------------|------------------------------|---------------------------------------------------|
| Home        | `index.md` (+ `home` layout) | Hero title + 6 most recent post cards             |
| Posts       | `_posts/`                    | All posts as cards, newest first (`/posts/`)      |
| Datasets    | `_datasets/`                 | One page per dataset (`/datasets/<name>/`)        |
| Methodology | `_methodology/`              | One page per method (`/methodology/<name>/`)      |

## Adding a blog post

Create `_posts/YYYY-MM-DD-slug.md`:

```yaml
---
title: "Post Title"
image: /assets/images/my-figure.png   # optional; card shows a fallback otherwise
abstract: >                            # optional, ~200 words; card falls back to excerpt
  One-paragraph abstract shown on the Home and Posts cards.
datasets: [nhanes]                     # optional; links to _datasets pages by slug
methodology: [ipw]                     # optional; links to _methodology pages by slug
---
Body in Markdown (rendered from your .Rmd/.qmd — see _source/ workflow below).
```

## Adding a dataset page

Create `_datasets/<slug>.md`. The `slug` field must match the filename —
methodology pages reference datasets by this slug:

```yaml
---
title: "Dataset Name"
slug: my-dataset
blurb: "One-line description shown on the Datasets index."
source_name: "Agency"
source_url: "https://..."
years: "2000–present"
license: "Public domain"
---
```

Dataset pages automatically list every methodology page that declares them.

## Adding a methodology page

Create `_methodology/<slug>.md`:

```yaml
---
title: "Method Name"
slug: my-method
summary: "One-line description shown on the Methodology index."
datasets: [my-dataset, other-dataset]   # slugs from _datasets/
---
```

The layout renders a "Datasets used with this method" block automatically.

## R notebook workflow

Keep sources in `_source/` (excluded from the build). Render to
GitHub-flavored Markdown and move the output into `_posts/`:

- **Quarto**: set `format: gfm` in the `.qmd`, run `quarto render`, copy the
  `.md` (renamed to `YYYY-MM-DD-slug.md`) into `_posts/` and its figure
  folder into `assets/images/`.
- **R Markdown**: use `output: md_document: {variant: gfm, preserve_yaml: true}`.

## Local preview

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```
