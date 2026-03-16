# az-scout Plugin Catalog

Official plugin catalog for [az-scout](https://github.com/az-scout/az-scout).

Served at **https://plugin-catalog.az-scout.com/catalog.json**

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

## Adding a plugin

1. Fork this repository
2. Add your plugin entry to `catalog.json` (alphabetical order)
3. Open a pull request

The CI will validate the JSON schema and check that repository URLs are accessible.

## Usage

The az-scout Plugin Manager fetches this catalog at startup:

```
GET https://plugin-catalog.az-scout.com/catalog.json
```
