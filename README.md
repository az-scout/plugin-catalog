# az-scout Plugin Catalog

Official plugin catalog for [az-scout](https://github.com/az-scout/az-scout).

Explore the available plugins in the online catalog: [docs.az-scout.com/catalog](https://docs.az-scout.com/catalog)

## Schema

Each plugin entry has the following fields:

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Package name (e.g. `az-scout-plugin-batch-sku`) |
| `description` | Yes | One-line description |
| `source` | Yes | `"pypi"` or `"github"` |
| `url` | If source=github | GitHub URL for direct installation |
| `repository` | Yes | GitHub repository URL |
| `authors` | Yes | Array of GitHub usernames of the authors |
| `tags` | Yes | Array of keyword tags |
| `audit` | No | Enable automated convention audits (`true`/`false`). Defaults to `true` for `az-scout` org repos, `false` for others. |
| `long_description` | No | Longer description shown below the short one in the catalog UI. |

## Adding a plugin

1. Fork this repository
2. Add your plugin entry to `catalog.json` (alphabetical order)
3. Open a pull request

The CI will validate the JSON schema and check that repository URLs are accessible.

## Automated plugin reviews

The catalog includes an automated review workflow that creates review issues
on plugin repos and assigns GitHub Copilot to review them against az-scout
conventions.

It runs monthly (1st of each month) and can be triggered manually via the
**Review Plugins** workflow.

### How it works

1. Reads `catalog.json` and filters plugins with `audit: true`
2. For each plugin, creates an issue on the plugin repo with the full
   [review-plugin checklist](.github/prompts/review-plugin.prompt.md) embedded
3. Assigns Copilot to the issue — Copilot reads the codebase and posts its
   findings as a comment (or opens a PR with fixes)
4. Existing open review issues are skipped to avoid duplicates

### What Copilot reviews

The review checklist covers:

- Naming conventions (package, module, entry point, slug)
- Packaging and build configuration (hatchling, ruff, mypy)
- Plugin protocol compliance (class structure, lazy imports, no global state)
- Type annotations and MCP tool docstrings
- Frontend conventions (JS/CSS patterns, dark theme, event handling)
- Isolation rules (no global mutation, no route conflicts)

### GitHub Actions

The workflow requires an `AUDIT_PAT` secret — a fine-grained PAT scoped to
`az-scout/*` repos with `issues: write` and `contents: read` permissions.

### Manual trigger

Run the workflow from the Actions tab with optional inputs:

- **plugin** — review a single plugin by package name (leave empty for all)
- **dry_run** — print what would happen without creating issues

## Copilot prompts

This repository includes Copilot prompt files in `.github/prompts/`:

- **`add-plugin-to-catalog.prompt.md`** — guides adding a new plugin to the catalog
- **`review-plugin.prompt.md`** — full convention review checklist for a plugin

## Usage

The az-scout Plugin Manager fetches this catalog at startup:

```
GET https://plugin-catalog.az-scout.com/catalog.json
```
