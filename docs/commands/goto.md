# twig goto

Switch branches with an interactive TUI picker, or jump straight to a branch by name.

## Usage

```sh
twig goto [branch] [flags]
twig g [branch] [flags]
```

## Description

With no arguments, opens an interactive branch picker showing local branches first, then remote branches (filtered by `goto.skip_patterns`). Use arrow keys to navigate, type to filter, Enter to select.

With a branch name argument, twig resolves the branch without the picker:

- If the branch exists locally — switch to it
- If the branch exists on the remote — create a tracking branch and switch
- If the branch exists nowhere — ask for confirmation (when `confirm_new = true`), then create it locally

Ticket detection from branch names also runs here — if the branch name contains a Jira ticket matching `save.ticket_prefixes`, it is stored for use in the next `twig save` invocation.

## Flags

| Flag | Description |
|---|---|
| `--local-only` | Show only local branches in the picker. Overrides `goto.local_only` config. |
| `--new` | Skip confirmation when creating a new branch. Useful in scripts. |

## Examples

```sh
# Open interactive picker
twig goto

# Jump to a known branch
twig goto main
twig goto feat/SHIP-2838

# Only show local branches
twig goto --local-only

# Create a new branch without confirmation prompt
twig goto my-new-feature --new
```

## Picker behaviour

The picker displays branches in this order:

1. Local branches (current branch marked)
2. Remote branches not already checked out locally

Branches matching any pattern in `goto.skip_patterns` are hidden. Typing narrows the list in real time. Pressing Escape cancels without switching.
