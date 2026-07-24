# Contributing

This is a personal GitHub profile repository. Its contents are the `README.md`
profile page, the `assets/banner.svg` hero graphic, and the GitHub Actions
workflow that generates the contribution snake animation.

## Repository structure

```
Kuroshitsuji/
├── README.md                        # Profile page rendered on github.com/Kuroshitsuji
├── CONTRIBUTING.md                  # This file
├── LICENSE                          # MIT licence
├── .markdownlint.yaml               # markdownlint config (used by lint-markdown workflow)
├── .yamllint.yaml                   # yamllint config (used by lint-yaml workflow)
├── assets/
│   └── banner.svg                   # Custom SVG hero banner (self-contained, no external deps)
└── .github/
    ├── dependabot.yml               # Automated GitHub Actions version updates
    └── workflows/
        ├── snake.yml                # Daily cron + push-triggered contribution snake generator
        ├── lint-markdown.yml        # Markdown formatting validation
        ├── lint-yaml.yml            # YAML formatting validation
        ├── validate-svg.yml         # SVG well-formedness + external reference check
        └── check-links.yml          # Markdown link validation (runs weekly + on change)
```

## Editing the profile

**README.md** — Standard GitHub Flavoured Markdown with inline HTML for layout.
The file uses `<div align="center">` blocks for centred content and a `<table>`
for the disciplines section. Both render correctly on GitHub desktop and mobile.

**assets/banner.svg** — Fully self-contained SVG. All gradients, filters, and
animations are defined in the `<defs>` block at the top of the file. No external
fonts or images are referenced. Edit dimensions via the `viewBox` attribute on
the root `<svg>` element.

**snake.yml** — See inline comments in the file for a description of each step.
The workflow requires `contents: write` permission to push generated SVGs to the
`output` branch. No secrets beyond the default `GITHUB_TOKEN` are needed.

## Workflows

All workflows run on push, pull request, and manual dispatch unless noted otherwise.
Every workflow uses `contents: read` (read-only) except `snake.yml`, which requires
`contents: write` to push to the `output` branch.

| Workflow | Trigger | Tool | What it checks |
|---|---|---|---|
| `lint-markdown.yml` | Push/PR on `**.md` | markdownlint-cli2 | Markdown style against `.markdownlint.yaml` |
| `lint-yaml.yml` | Push/PR on `**.yml`, `**.yaml` | yamllint (pre-installed) | YAML syntax and style against `.yamllint.yaml` |
| `validate-svg.yml` | Push/PR on `assets/**.svg` | xmllint + shell | SVG well-formedness and absence of external references |
| `check-links.yml` | Push/PR on `**.md`, weekly Monday | lychee | All URLs in Markdown files |
| `snake.yml` | Push to `main`, daily 00:00 UTC | Platane/snk, peaceiris/actions-gh-pages | Generates contribution snake SVGs |

### Linter configurations

**`.markdownlint.yaml`** — Disables rules that conflict with this repository's
intentional use of inline HTML (`MD033`), long badge URLs (`MD013`), and the
SVG-based opening section instead of an H1 (`MD041`). Every disabled rule has
a comment explaining why.

**`.yamllint.yaml`** — Extends the yamllint `default` profile with a relaxed
line-length warning (120 chars, to accommodate GitHub Actions `uses:` strings)
and an explicit `truthy` rule that flags `yes`/`no`/`on`/`off` in favour of
`true`/`false`. The `on:` workflow trigger key is excluded from this check via
`check-keys: false`.

### Dependabot

`.github/dependabot.yml` configures Dependabot to check for GitHub Actions
version updates every Monday at 06:00 UTC. All updates are grouped into a
single pull request per week to reduce noise. PRs are labelled `dependencies`
and `github-actions`.

## Making changes

1. Fork the repository.
2. Create a branch: `git checkout -b your-change`.
3. Make your edits.
4. Open a pull request with a clear description of what changed and why.

Corrections to factual content and improvements to the workflow or SVG are
welcome. Unsolicited redesigns of the profile layout are unlikely to be merged.
