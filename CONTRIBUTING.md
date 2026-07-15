# Contributing to bar-localizations

## Overview

This repository is the centralized source of truth for all Beyond All Reason localization strings. English source keys are synced here automatically from their owning repositories (bar-game and bar-lobby). Translations are managed through Transifex.

## How to add or edit English source keys

**Make changes in the repo that owns the namespace**, not here. Changes are synced to this repo automatically.

- **Game strings** (`features.json`, `interface.json`, `tips.json`, `units.json`) - edit in [bar-game](https://github.com/beyond-all-reason/Beyond-All-Reason) under `language/en/`
- **Lobby strings** (`lobby.json`) - edit in [bar-lobby](https://github.com/beyond-all-reason/bar-lobby) under `language/en/`

The daily upstream sync workflows will detect your changes and open a PR here. Additions and edits are auto-approved. Deletions require manual review.

**When to PR directly against this repo:** Only for cross-cutting changes that span multiple namespaces, translation-infrastructure fixes, or edits that don't belong in either source repo. Direct PRs are the exception, not the norm.

## How to contribute translations

Translations are managed through [Transifex](https://www.transifex.com/). Join the BAR project on Transifex to contribute. Do not edit non-English files in this repo - they are overwritten by Transifex on every sync.

## Namespace ownership

Each JSON file represents a namespace with a single **upstream owner** - the repository where English source strings originate.

| File | Owner | Synced via |
|------|-------|------------|
| `features.json` | bar-game | `upstream_sync_game.yml` |
| `interface.json` | bar-game | `upstream_sync_game.yml` |
| `tips.json` | bar-game | `upstream_sync_game.yml` |
| `units.json` | bar-game | `upstream_sync_game.yml` |
| `lobby.json` | bar-lobby | `upstream_sync_lobby.yml` |

Automated upstream sync PRs are validated against this ownership mapping. A sync from bar-game cannot modify `lobby.json`, and vice versa. Violations are flagged for manual review.

## Interpolation syntax

Source strings use `%{variable}` syntax (Lua i18n convention). bar-lobby consumers convert this to `{variable}` (vue-i18n) automatically during their sync process.

## AI Policy

Refer to the [AI Usage Policy](AI_POLICY.md) if you used an AI to generate production code.

## Communication

Join the [Beyond All Reason Discord](https://discord.gg/beyond-all-reason) for discussion.
