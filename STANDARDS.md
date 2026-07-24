# Repository Standards

This document is the single source of truth for every convention used across all repositories maintained by [Kuroshitsuji](https://github.com/Kuroshitsuji). All new repositories must follow these standards before their first public commit. All existing repositories must be brought into compliance before accepting external contributions.

---

## Table of contents

1. [Repository structure](#repository-structure)
2. [File naming](#file-naming)
3. [Branding](#branding)
4. [README format](#readme-format)
5. [Badges](#badges)
6. [Commit messages](#commit-messages)
7. [Branch naming](#branch-naming)
8. [Pull requests](#pull-requests)
9. [Issues](#issues)
10. [Markdown style](#markdown-style)
11. [YAML style](#yaml-style)
12. [GitHub Actions workflows](#github-actions-workflows)
13. [Folder conventions](#folder-conventions)
14. [Licensing](#licensing)
15. [Community health files](#community-health-files)
16. [Templates index](#templates-index)

---

## Repository structure

Every repository must contain the following files at the root unless explicitly noted as optional:

```
REPO_NAME/
├── README.md                   # Required — project overview and usage
├── LICENSE                     # Required — MIT licence
├── CONTRIBUTING.md             # Required — contribution guidelines
├── SECURITY.md                 # Required — vulnerability reporting policy
├── CODE_OF_CONDUCT.md          # Required — expected community behaviour
├── CHANGELOG.md                # Recommended — notable changes per version
├── .markdownlint.yaml          # Required if repo contains Markdown files
├── .yamllint.yaml              # Required if repo contains YAML files
├── .github/
│   ├── dependabot.yml          # Required — automated dependency updates
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml
│   │   ├── feature_request.yml
│   │   └── documentation.yml
│   └── workflows/
│       ├── ci.yml              # Build, test, and lint — required for code repos
│       ├── lint-markdown.yml   # Required if repo contains Markdown files
│       ├── lint-yaml.yml       # Required if repo contains YAML files
│       └── check-links.yml     # Required if repo contains Markdown files
├── docs/                       # Optional — detailed documentation
├── src/                        # Source code root (name varies by language)
├── tests/                      # Test files (co-locate or top-level, consistent per repo)
└── assets/                     # Static assets: images, SVGs, diagrams
```

**Rule:** Do not mix documentation, source code, tests, and configuration files at the root level unless the file is a recognised community health file or a tooling config that must live at the root (e.g. `.markdownlint.yaml`, `package.json`, `Makefile`).

---

## File naming

| Type | Convention | Example |
|---|---|---|
| Markdown community files | SCREAMING_SNAKE_CASE | `README.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md` |
| Workflow files | kebab-case | `lint-markdown.yml`, `check-links.yml` |
| Source code | kebab-case (scripts/web) or the language convention | `user-provisioning.sh`, `UserProvisioner.java` |
| Configuration files | dot-prefixed kebab-case | `.markdownlint.yaml`, `.yamllint.yaml` |
| Documentation | kebab-case | `architecture-overview.md`, `api-reference.md` |
| Assets | kebab-case | `banner.svg`, `network-diagram.png` |
| Test files | Same name as the file under test, with `.test.` or `_test` infix/suffix | `handler.test.ts`, `test_handler.py` |

**Rules:**
- No spaces in any filename.
- No uppercase in workflow filenames — GitHub Actions displays the `name:` field as the label; the filename is for filesystem organisation only.
- No generic names like `script.sh`, `utils.py`, `helpers.js`. Every file must be named for its purpose.

---

## Branding

All repositories under this account share a consistent visual identity derived from the profile repository.

| Token | Value | Usage |
|---|---|---|
| Primary accent | `#00d4ff` (cyan) | Badge colour, active elements, links in SVG |
| Secondary accent | `#a78bfa` (purple) | Gradient endpoint, icon colour in stats cards |
| Muted text | `#8b949e` | Secondary labels, captions, view counters |
| Background | `#0d1117` | SVG backgrounds, stats card backgrounds |
| Border | `#30363d` | Dividers, placeholder frames |
| Heading font | Segoe UI / SF Pro Display / Inter (fallback chain) | SVG text elements |
| Code font | JetBrains Mono | Typing animation, code samples in SVGs |

**Rules:**
- Badge style is always `flat-square` — never `for-the-badge`, `plastic`, or `social`.
- Badge label colour follows the primary accent (`#00d4ff`) for status/metadata badges.
- Do not use animated GIFs as hero images. Use SVG for all custom graphics.
- All SVG files must be self-contained — no external font or image references.

---

## README format

Every repository README follows this section order. Omit sections that genuinely do not apply, but do not reorder them.

```
1. Hero / banner image (optional — for prominent public repos)
2. Badges (licence, last commit, CI status — see Badges section)
3. One-line summary
4. Horizontal rule (---)
5. Overview (2–4 sentences)
6. Features (bullet list)
7. Installation
8. Usage (with code examples)
9. Configuration (if applicable)
10. Documentation (links to docs/ if they exist)
11. Development (project structure, build, test, lint commands)
12. Contributing (link to CONTRIBUTING.md)
13. Security (link to SECURITY.md)
14. Licence (one line + link to LICENSE)
15. Footer (maintainer attribution, view counter)
```

### Writing rules

- **Language:** British English. Use *licence* (noun), *color* only in CSS/HTML where the attribute name demands it, *behaviour*, *centralised*, *organised*.
- **Headings:** Sentence case — `## Installation`, not `## INSTALLATION` or `## installation`.
- **Voice:** Active, direct, technical. No filler phrases ("feel free to", "simply run", "easy to use").
- **Code blocks:** Always specify the language identifier (` ```bash`, ` ```yaml`, ` ```python`).
- **Links:** Use relative paths for files in the same repository (`./LICENSE`, `./docs/guide.md`). Use absolute URLs for external links.
- **Emphasis:** Use `**bold**` for UI elements, filenames, and terms being defined. Use `*italic*` sparingly, only for genuine emphasis. Do not use bold as a substitute for headings.
- **Tables:** Include a header row and use pipe-aligned columns. Wrap table cells in `<td>` for complex HTML layouts, otherwise use standard GFM table syntax.

---

## Badges

Badges appear immediately after the hero image (if present), or at the top of the README if no hero image is used.

### Required badges (all repositories)

```markdown
[![License: MIT](https://img.shields.io/badge/License-MIT-00d4ff.svg?style=flat-square)](./LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/Kuroshitsuji/REPO_NAME?style=flat-square&color=00d4ff&label=updated)](https://github.com/Kuroshitsuji/REPO_NAME/commits/main)
```

### Conditional badges

| Condition | Badge |
|---|---|
| Repository has a CI workflow | Build status badge pointing to `ci.yml` |
| Repository has a markdown lint workflow | Markdown lint status badge |
| Repository has a link check workflow | Link check status badge |
| Repository has releases | Version badge from `shields.io/github/v/release` |

### Badges that must never be used

| Badge | Reason |
|---|---|
| Stars count | Vanity metric — not useful for ops/infra repositories |
| Forks count | Same reason |
| Issues count | Does not communicate project health to a recruiter or user |
| Repo size | Not useful information |
| `for-the-badge` style | Inconsistent with `flat-square` standard |
| "Made with" language badges | Generic and uninformative |
| Multiple profile view counters | One counter, placed in the footer only |

### Badge placement rules

- Maximum **5 badges** in the hero area.
- All badges on a single line unless the line exceeds 120 characters, in which case break onto two lines grouped by category.
- Profile view counter goes in the **footer only**, using muted colour `#8b949e`.

---

## Commit messages

All commits follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Format

```
<type>(<scope>): <short summary>

<body — optional>

<footer — optional>
```

### Rules

- **Subject line:** 72 characters maximum. Imperative mood. No trailing period.
- **Body:** Wrap at 72 characters. Explain *why*, not *what*. Use bullet points for multiple changes.
- **Footer:** Reference issues with `Closes #123`, `Fixes #456`, `Refs #789`. Note breaking changes with `BREAKING CHANGE: <description>`.
- **No merge commits** in feature branches — rebase onto `main` before merging.
- **No WIP commits** in pull requests — squash or amend before opening the PR.

### Allowed types

| Type | When to use |
|---|---|
| `feat` | A new feature or capability |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `style` | Formatting, whitespace, punctuation — no logic change |
| `refactor` | Code restructuring without changing behaviour |
| `test` | Adding or correcting tests |
| `chore` | Build process, dependency updates, tooling |
| `ci` | Changes to GitHub Actions workflows or CI configuration |
| `revert` | Reverting a previous commit |
| `perf` | Performance improvement |
| `security` | Security fix (use with `fix` type for CVEs) |

### Examples

```
feat(auth): add token refresh on 401 response

Automatically retries failed requests with a refreshed token.
Previous behaviour required manual re-login on token expiry.

Closes #87
```

```
ci: add yamllint workflow to all branches

Catches YAML syntax errors in workflows and config files
before they reach main and fail the deployment pipeline.
```

```
docs: update installation steps for Docker on Windows

The previous instructions assumed WSL2 was already configured.
Added prerequisite step and link to Microsoft's setup guide.
```

---

## Branch naming

| Purpose | Pattern | Example |
|---|---|---|
| New feature | `feature/<short-description>` | `feature/token-refresh` |
| Bug fix | `fix/<short-description>` | `fix/null-pointer-handler` |
| Documentation | `docs/<short-description>` | `docs/update-install-guide` |
| Refactoring | `refactor/<short-description>` | `refactor/extract-auth-module` |
| CI / tooling | `ci/<short-description>` | `ci/add-yamllint` |
| Release preparation | `release/<version>` | `release/v1.2.0` |
| Hotfix | `hotfix/<short-description>` | `hotfix/db-connection-timeout` |

**Rules:**
- All lowercase, hyphen-separated words.
- No special characters other than `/` (prefix separator) and `-` (word separator).
- Keep descriptions short — three words or fewer.
- Delete branches after merging.

---

## Pull requests

- Every PR must use the [pull request template](./.github/PULL_REQUEST_TEMPLATE.md).
- PR title follows the same format as a commit subject line: `<type>(<scope>): <summary>`.
- PRs must target `main` unless explicitly part of a release process.
- A PR must not contain unrelated changes. If you find an unrelated bug while working on a feature, open a separate issue and fix it in a separate branch.
- All CI checks must pass before a PR is merged.
- At least one approval is required before merging (for multi-contributor repositories).
- Use **squash merge** for feature branches. Use **merge commit** only for release branches where the full commit history is meaningful.

---

## Issues

- Every issue must use one of the three provided templates: Bug Report, Feature Request, or Documentation Issue.
- Issues opened without a template will be asked to resubmit using the appropriate form.
- All new issues are automatically labelled `triage` and must be triaged within 7 days.
- Issue titles follow the template format: `[Bug]: short description`, `[Feature]: short description`, `[Docs]: short description`.
- Duplicate issues are closed with a reference to the original.
- Issues that are not actionable or lack sufficient information are closed after 14 days of no response following a request for clarification.

---

## Markdown style

Governed by `.markdownlint.yaml` in each repository. Core rules:

| Rule | Setting | Reason |
|---|---|---|
| MD013 Line length | Disabled | Badge URLs and inline HTML produce intentionally long lines |
| MD033 Inline HTML | Disabled | Used for centred layouts, tables, and `<picture>` elements |
| MD041 First heading | Disabled for profile repo | SVG banner serves as the visual heading |
| MD036 Emphasis as heading | Disabled for profile repo | Bold used as project card titles in Featured Projects |
| MD024 Duplicate headings | Disabled | Multiple files may share identical section names |
| MD046 Code block style | `fenced` | Consistent use of triple-backtick blocks |
| MD049 Emphasis style | `asterisk` | `*italic*` not `_italic_` |
| MD050 Strong style | `asterisk` | `**bold**` not `__bold__` |

All markdown files must pass `markdownlint-cli2` before merging.

---

## YAML style

Governed by `.yamllint.yaml` in each repository. Core rules:

| Rule | Setting | Reason |
|---|---|---|
| Indentation | 2 spaces | Consistent across all workflow and config files |
| Line length | 120 chars (warning) | Accommodates `uses:` strings in GitHub Actions |
| Truthy values | `true`/`false` only | Prevents `yes`/`no`/`on`/`off` ambiguity |
| Trailing spaces | Error | Clean diffs |
| New line at end of file | Required | POSIX compliance, clean diffs |
| Comments | 1 space after `#` | Readability |

All YAML files must pass `yamllint` before merging.

---

## GitHub Actions workflows

### Naming convention

| File name | Workflow `name:` | Purpose |
|---|---|---|
| `ci.yml` | `CI` | Build, test, lint — primary validation pipeline |
| `lint-markdown.yml` | `Lint Markdown` | Markdown formatting validation |
| `lint-yaml.yml` | `Lint YAML` | YAML formatting validation |
| `validate-svg.yml` | `Validate SVG` | SVG well-formedness and external reference check |
| `check-links.yml` | `Check Links` | Markdown URL validation |
| `snake.yml` | `Generate Contribution Snake` | Profile contribution animation |
| `release.yml` | `Release` | Automated release and changelog generation |
| `deploy.yml` | `Deploy` | Deployment pipeline |

### Required structure for every workflow

```yaml
name: Workflow Name            # Title Case

on:
  push:
    branches: [main]           # or path-filtered for lint/check workflows
  pull_request:
    branches: [main]
  workflow_dispatch:           # Always include — allows manual trigger

concurrency:                   # Always include — prevents redundant runs
  group: <workflow-name>-${{ github.ref }}
  cancel-in-progress: true

jobs:
  job-name:
    name: Human-readable job name
    runs-on: ubuntu-latest
    timeout-minutes: 10        # Always set — prevents runaway jobs

    permissions:               # Always declare — use minimum necessary
      contents: read           # Default for read-only workflows
      # contents: write        # Only when writing back to the repository

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      # Inline comments required for every non-obvious step.
      # Explain why, not what. The step name explains what.
```

### Rules

- **Minimum permissions:** Every workflow declares explicit `permissions:`. Default to `contents: read`. Only grant `contents: write` when the workflow pushes to the repository.
- **Pinned action versions:** Always use `@v4` (or the latest major version) — never `@latest` or `@main`.
- **Concurrency guard:** Every workflow must include a `concurrency:` block to prevent parallel runs on the same branch.
- **Timeout:** Every job must set `timeout-minutes:`. Use 5 for lint jobs, 10 for build/test jobs, 15 for deployment jobs.
- **Comments:** Comment every step whose purpose is not immediately obvious from its name. Comments explain *why*, not *what*.
- **Secrets:** Never hardcode tokens. Use `${{ secrets.GITHUB_TOKEN }}` for repository operations, named secrets for external services.
- **Dependabot:** Every repository must have `.github/dependabot.yml` configured to check GitHub Actions updates on a weekly schedule, grouped into a single PR.

---

## Folder conventions

| Folder | Contents | Notes |
|---|---|---|
| `src/` | Application source code | May be renamed per language convention (`lib/`, `app/`, `cmd/`) |
| `tests/` | Test files | May be co-located with source for unit tests if the framework supports it |
| `docs/` | Documentation markdown files and diagrams | Not to be confused with GitHub Pages output |
| `assets/` | Images, SVGs, fonts, static files | Subdirectories: `assets/screenshots/`, `assets/diagrams/` |
| `scripts/` | One-off or maintenance shell scripts | Must each have a comment block at the top explaining purpose and usage |
| `config/` | Application configuration examples | Checked-in examples only — never real secrets |
| `.github/` | GitHub-specific files: workflows, templates, Dependabot | Do not put application code here |
| `dist/` or `build/` | Compiled output | Always in `.gitignore` |
| `node_modules/`, `venv/`, `.cargo/` | Dependency caches | Always in `.gitignore` |

---

## Licensing

All repositories default to the **MIT Licence**.

- Copy `docs/templates/LICENSE` into the repository root, updating the copyright year and name if necessary.
- The copyright holder is always `Kuroshitsuji`.
- Repositories that incorporate third-party code with incompatible licences must document this in a `NOTICE` file.
- The licence is referenced in:
  - The final section of `README.md` — one line plus a link to `./LICENSE`
  - The `CONTRIBUTING.md` — one sentence at the end of the Licence section
  - The badge block at the top of `README.md`

---

## Community health files

Every repository must include these files before accepting external contributions:

| File | Template source | Notes |
|---|---|---|
| `README.md` | `docs/templates/README.md` | Customise fully — the template is a scaffold, not a final document |
| `CONTRIBUTING.md` | `docs/templates/CONTRIBUTING.md` | Update the development setup section for the specific project |
| `LICENSE` | `docs/templates/LICENSE` | Update year if necessary |
| `SECURITY.md` | `SECURITY.md` (this repository root) | Update the contact address and advisory link |
| `CODE_OF_CONDUCT.md` | `CODE_OF_CONDUCT.md` (this repository root) | Update the contact address |
| `.github/PULL_REQUEST_TEMPLATE.md` | `.github/PULL_REQUEST_TEMPLATE.md` | Use as-is — it is generic enough for all project types |
| `.github/ISSUE_TEMPLATE/*.yml` | `.github/ISSUE_TEMPLATE/` | Use as-is for most projects; add project-specific issue types if needed |

---

## Templates index

All reusable templates live in `docs/templates/` in this repository.

| Template | Path | Use for |
|---|---|---|
| Repository README | `docs/templates/README.md` | Starting point for any new repository README |
| Contributing guide | `docs/templates/CONTRIBUTING.md` | Starting point for any new CONTRIBUTING.md |
| MIT Licence | `docs/templates/LICENSE` | Copy to repository root; update year if needed |
| PR template | `.github/PULL_REQUEST_TEMPLATE.md` | Copy to `.github/` of any new repository |
| Bug report | `.github/ISSUE_TEMPLATE/bug_report.yml` | Copy to `.github/ISSUE_TEMPLATE/` |
| Feature request | `.github/ISSUE_TEMPLATE/feature_request.yml` | Copy to `.github/ISSUE_TEMPLATE/` |
| Documentation issue | `.github/ISSUE_TEMPLATE/documentation.yml` | Copy to `.github/ISSUE_TEMPLATE/` |
| Security policy | `SECURITY.md` | Copy to repository root; update contact and advisory URL |
| Code of Conduct | `CODE_OF_CONDUCT.md` | Copy to repository root; update contact address |

---

## Applying this standard to a new repository

Follow these steps when creating any new repository under this account:

1. Create the repository on GitHub.
2. Copy `docs/templates/README.md` → `README.md` and fill in the project-specific content.
3. Copy `docs/templates/CONTRIBUTING.md` → `CONTRIBUTING.md` and update the development setup section.
4. Copy `docs/templates/LICENSE` → `LICENSE`. Update the year if not 2025.
5. Copy `SECURITY.md`, `CODE_OF_CONDUCT.md` → repository root. Update contact addresses.
6. Copy `.github/PULL_REQUEST_TEMPLATE.md` and `.github/ISSUE_TEMPLATE/*.yml` → `.github/` of the new repository.
7. Copy `.markdownlint.yaml` and `.yamllint.yaml` from this repository if the project contains Markdown or YAML files.
8. Add `.github/dependabot.yml` with weekly GitHub Actions checks grouped into a single PR.
9. Add at minimum `lint-markdown.yml` and `check-links.yml` workflows if the repository contains Markdown files.
10. Add a `ci.yml` workflow with build, test, and lint steps appropriate for the project's language and framework.
11. Apply the 10 recommended topics from the [Topics Guide](https://github.com/Kuroshitsuji/Kuroshitsuji#topics) plus project-specific topics.
12. Verify all CI checks pass on the first push to `main`.

---

<div align="center">
  <sub>
    Maintained by <a href="https://github.com/Kuroshitsuji">Kuroshitsuji</a>
    &nbsp;·&nbsp;
    IT Support &nbsp;·&nbsp; Infrastructure Automation &nbsp;·&nbsp; Network Operations &nbsp;·&nbsp; Full Stack Development
  </sub>
</div>
