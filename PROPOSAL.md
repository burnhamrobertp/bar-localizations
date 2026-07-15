# Adoption Proposal

> For BAR maintainers evaluating this repo. Delete after adoption.

## The Problem

BAR's translation strings are scattered across bar-game and bar-lobby with no automated sync between them. Lobby developers manually copy translation files from bar-game ([bar-lobby#419](https://github.com/beyond-all-reason/bar-lobby/issues/419)). Strings drift out of sync. Translator effort is duplicated or lost.

## What This Repo Does

Centralizes all English source strings and Transifex integration into one repo. Developers keep editing files in their own repos - automation handles the rest:

1. **Pulls** English sources from bar-game and bar-lobby daily
2. **Manages Transifex** - one project, one sync pipeline
3. **Pushes** translations back to consumer repos automatically

## Advantages

- **Zero friction** - developers change nothing about their workflow; keep editing `language/en/` in your own repo
- **Single Transifex integration** - translators work in one place, translations reach all consumers
- **No manual copying** - solves [bar-lobby#419](https://github.com/beyond-all-reason/bar-lobby/issues/419); changes sync automatically in both directions
- **Consolidated infrastructure** - replaces the duplicated, ad-hoc sync setups across bar-game and bar-lobby with one managed pipeline (one repo, two secrets)
- **Safe by default** - key deletions flagged for review (they're destructive on Transifex), namespace ownership enforced, additions/edits auto-merged

## Trade-offs

- **Indirection** - changes take up to 24 hours to sync (daily cron), or can be triggered manually.
  - Already the case: bar-game uses the same deferred-sync pattern via `transifex-synchronization-source`.
- **Merge conflicts** - possible if the same key is edited both in a source repo and directly here.
  - Minor in practice, and CI can rule it out: block any non-system PR from a consumer repo that targets a namespace other than `common`, so direct edits and the automated sync never touch the same keys.
  - Same risk already exists with bar-game's Transifex sync branch.

## Migration Steps

1. **Transifex config** - point the Transifex GitHub App at this repo's `transifex-synchronization-source` branch (BAR org admin, one-time)
2. **Secrets** - configure `ACTION_RUNNER_PRIVATE` (deploy key) and `DOWNSTREAM_TOKEN` (PAT with repo access)
3. **bar-lobby layout** - migrate `lang/` -> `language/` to match bar-game's convention
4. **Transfer** - [transfer the repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository) to the `beyond-all-reason` org, then update org references in workflow files
