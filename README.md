# bar-localizations

Centralized localization (i18n) source of truth for [Beyond All Reason](https://www.beyondallreason.info/). English source strings and translations for bar-game and bar-lobby are managed here, with automated bidirectional sync and a single Transifex integration.

> **Evaluating this repo for adoption?** See [PROPOSAL.md](PROPOSAL.md).

## Usage

### For developers (bar-game and bar-lobby)

Each namespace has a single owning repo (see [Namespace Ownership](#namespace-ownership)).

1. Edit the appropriate `language/en/*.json` file **in your repo**
2. Commit and merge to `master`
3. The upstream sync opens a PR here within 24 hours (additions/edits auto-merge; deletions require review)
4. Translations flow back to your repo automatically via downstream sync

> **Why are deletions flagged?** Removing a key from Transifex is destructive - existing translations are permanently demoted to suggestions and must be manually re-accepted per language.

### For translators

1. Join the BAR project on [Transifex](https://www.transifex.com/)
2. All namespaces are available in one place
3. Completed translations are distributed to consumer repos automatically

### For direct contributors

Fork this repo, edit `language/en/*.json`, and open a PR. Useful for cross-cutting changes spanning multiple namespaces.

## How It Works

Three automated pipelines keep everything in sync. Each links to a diagram with more detail.

| Pipeline | What it does | Diagram |
|----------|-------------|---------|
| **Upstream sync** | Daily pull of English sources from bar-game and bar-lobby | [docs/upstream-sync.md](docs/upstream-sync.md) |
| **Transifex sync** | Weekly rebase feeds Transifex; bot PRs bring translations back | [docs/transifex-sync.md](docs/transifex-sync.md) |
| **Downstream sync** | Translations pushed to consumer repos on every `master` update | [docs/downstream-sync.md](docs/downstream-sync.md) |

## Namespace Ownership

| File | Owner |
|------|-------|
| `features.json` | bar-game |
| `interface.json` | bar-game |
| `tips.json` | bar-game |
| `units.json` | bar-game |
| `lobby.json` | bar-lobby |
| `common.json` | bar-localizations (direct edits) |

## Workflows

All seven workflows also support manual `workflow_dispatch`.

| Workflow | Trigger | Auto? |
|----------|---------|-------|
| `upstream_sync_game.yml` | Daily 04:30 UTC | Yes |
| `upstream_sync_lobby.yml` | Daily 04:45 UTC | Yes |
| `localization_pr_review.yml` | PRs touching `language/en/**` | Adds auto, deletes flagged |
| `transifex_rebase.yml` | Weekly Monday 05:15 UTC | Yes |
| `transifex_merge.yml` | Transifex bot PR merged | Yes |
| `downstream_sync_game.yml` | Push to `master` | Yes |
| `downstream_sync_lobby.yml` | Push to `master` | Yes |

## Supported Languages

`en` (source), `cs`, `de`, `es`, `fr`, `hr`, `it`, `lt`, `ru`, `zh`

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## AI Policy

See [AI_POLICY.md](AI_POLICY.md).

## License

[MIT](LICENSE.md)
