# Contributing

Thank you for considering contributing to this project. This document explains how to report issues, propose changes, and submit pull requests.

## Getting started

Before opening an issue or pull request:

1. Check if a similar issue or PR already exists.
2. Read the [README](./README.md) to understand the project's purpose and scope.
3. Review the [Code of Conduct](./CODE_OF_CONDUCT.md) — all contributors are expected to follow it.

## Reporting issues

Use the issue templates provided when opening a new issue:

- **Bug Report** — for defects or unexpected behaviour
- **Feature Request** — for suggesting new functionality
- **Documentation Issue** — for incorrect, unclear, or missing documentation

Provide as much detail as possible. The more information you include, the faster we can address the issue.

## Proposing changes

### For small changes (typos, formatting, minor fixes)

Open a pull request directly with a clear title and description.

### For larger changes (new features, refactoring, breaking changes)

Open an issue first to discuss the approach before writing code. This ensures your work aligns with the project's direction and avoids wasted effort.

## Submitting a pull request

1. **Fork the repository** and create a new branch from `main`:

   ```bash
   git checkout -b fix/issue-description
   # or
   git checkout -b feature/feature-name
   ```

2. **Make your changes**. Follow the project's code style and conventions (see [STANDARDS.md](./STANDARDS.md)).

3. **Write tests** if your change adds or modifies functionality.

4. **Run the test suite** locally before pushing:

   ```bash
   npm test   # or pytest, cargo test, etc.
   ```

5. **Lint your code** to catch formatting issues:

   ```bash
   npm run lint   # or make lint, cargo clippy, etc.
   ```

6. **Commit your changes** using clear, descriptive commit messages:

   ```
   fix: resolve null pointer dereference in handler

   - Add validation before accessing optional field
   - Add regression test covering the edge case

   Closes #123
   ```

   Follow the commit message format described in [STANDARDS.md](./STANDARDS.md).

7. **Push your branch** and open a pull request against `main`.

8. **Fill out the pull request template** completely. Explain what changed and why.

## Code review process

- A maintainer will review your pull request within **7 days**.
- You may be asked to make changes based on feedback. Push new commits to your branch — the PR will update automatically.
- Once approved, a maintainer will merge your PR. Do not merge it yourself unless you have write access.

## Development environment setup

### Prerequisites

List the tools and dependencies needed for development (same as in README, but more detailed if necessary).

### Building the project locally

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME

# Install dependencies
npm install   # or pip install -r requirements.txt, cargo build, etc.

# Run the project in development mode
npm run dev   # or equivalent
```

### Running tests

```bash
npm test               # run all tests
npm run test:watch     # run tests in watch mode (if supported)
npm run test:coverage  # generate coverage report
```

### Linting and formatting

```bash
npm run lint           # check for style issues
npm run lint:fix       # auto-fix linting issues
npm run format         # format code
```

## Project structure

Refer to the repository structure diagram in the [README](./README.md).

## Style guidelines

- Follow the language-specific style guide (link if you have one).
- Keep functions small and focused.
- Write clear, self-explanatory variable and function names.
- Comment non-obvious logic — explain *why*, not *what*.
- Write tests for new functionality and bug fixes.

For detailed conventions (naming, formatting, commit messages, workflow patterns), see [STANDARDS.md](./STANDARDS.md).

## Documentation

If your change affects user-facing functionality:

- Update the relevant documentation in `docs/`.
- Update the README if usage instructions change.
- Add inline code comments for complex logic.

## Licence

By contributing to this project, you agree that your contributions will be licensed under the same licence as the project (MIT). See [LICENSE](./LICENSE) for details.
