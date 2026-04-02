# poc-automated-releases

This repository uses [release-please](https://github.com/googleapis/release-please) to automate versioning and changelog generation based on [Conventional Commits](https://www.conventionalcommits.org/).

## How It Works

Whenever commits are pushed to the `main` branch, the **Release Please** GitHub Action inspects the commit messages. If it finds releasable commits, it opens (or updates) a release pull request that bumps the version in `package.json` and updates `CHANGELOG.md`. Merging that PR creates a GitHub Release and git tag automatically.

## Conventional Commits

Commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification so that release-please can determine the correct version bump:

| Commit prefix | Example | Version bump |
|---|---|---|
| `fix:` | `fix: handle null pointer in parser` | Patch (`1.0.x`) |
| `feat:` | `feat: add dark mode support` | Minor (`1.x.0`) |
| `feat!:` or `BREAKING CHANGE:` | `feat!: rename config file` | Major (`x.0.0`) |
| `chore:`, `docs:`, `style:`, `refactor:`, `test:` | `docs: update README` | No release |

### Examples

```
# Patch release (bug fix)
fix: correct off-by-one error in pagination

# Minor release (new feature)
feat: add export to CSV functionality

# Major release (breaking change)
feat!: remove deprecated v1 API endpoints

BREAKING CHANGE: The /v1/* endpoints have been removed. Use /v2/* instead.

# No release triggered
chore: update dependencies
docs: add contributing guide
```

## Files

| File | Purpose |
|---|---|
| `.github/workflows/release-please.yml` | GitHub Actions workflow that runs release-please on every push to `main` |
| `release-please-config.json` | release-please configuration (release type: Node.js) |
| `.release-please-manifest.json` | Tracks the current released version for each package |

## Getting Started

1. Ensure your repository's default branch is `main`.
2. Make commits using the Conventional Commits format above.
3. Push to `main` — release-please will open a release PR automatically.
4. Merge the release PR to publish a new GitHub Release.
