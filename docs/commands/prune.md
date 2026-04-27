# twig prune

Clean up stale local branches that have no remote and haven't been touched recently.

## Usage

```sh
twig prune [flags]
twig pr [flags]
```

## Description

Identifies and deletes local branches matching **all** of these criteria:

- Not the current branch
- Not in `prune.protected_branches`
- No corresponding branch on `origin` (after a `git fetch -p`)
- Last commit is older than `prune.default_days` days

Before deleting, twig lists all eligible branches with their last commit date and message, and asks for explicit confirmation.

If `require_clean_tree = true` (default), twig aborts immediately if the working tree has uncommitted changes.

## Flags

| Flag | Description |
|---|---|
| `--days <n>` | Override the age threshold for this run. Branches older than `n` days are eligible. |
| `--dry-run` | List eligible branches without deleting anything. No confirmation prompt. |
| `--debug <branch>` | Explain why a specific branch is or is not eligible for pruning. Useful for debugging. |
| `--force` | Skip the confirmation prompt and delete all eligible branches immediately. |

## Examples

```sh
# Interactive prune with confirmation
twig prune

# See what would be deleted without touching anything
twig prune --dry-run

# Use a shorter age threshold
twig prune --days 7

# Debug why a branch isn't being pruned
twig prune --debug my-old-feature

# Non-interactive — useful in scripts
twig prune --force
```

## Example output

```
Branches eligible for deletion:

NAME                    LAST COMMIT     MESSAGE
old-experiment          2026-01-03      WIP: trying something
fix-auth-typo           2025-12-19      fix typo in login handler
stale-deps-update       2025-11-30      bump lodash

Force delete all 3 branches? [y/N]
```
