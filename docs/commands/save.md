# twig save

Commit with a guided TUI wizard, or pass flags directly for scripting.

## Usage

```sh
twig save [flags]
twig s [flags]
```

## Description

With no flags, launches the interactive TUI wizard:

1. **Type picker** — choose a commit type (feat, fix, chore, test, docs, plus any extras you've configured)
2. **Scope picker** — choose or type a scope (pinned scopes at top, then history)
3. **Ticket** — auto-populated from branch name if a Jira ticket is detected, otherwise optional input
4. **Message** — type the commit message body

The assembled commit message follows conventional commits format:

```
🎉 feat(api:SHIP-2416): add user authentication endpoint
```

After the wizard completes, twig runs `git add .` (if `auto_add = true`) and `git commit`, then `git push` (if `auto_push = true`).

With flags, the wizard is skipped entirely:

```sh
twig save --type fix --scope api --message "handle null auth response"
```

## Flags

| Flag | Description |
|---|---|
| `--type <label>` | Commit type. Must match a default or configured type label. |
| `--scope <scope>` | Commit scope. Any string. Saved to history if new. |
| `--message <msg>` | Commit message. Skips the message input step. |
| `--ticket <id>` | Jira ticket ID (e.g. `SHIP-2416`). Overrides auto-detected ticket. |
| `--no-ticket` | Omit ticket from commit message even if one is detected. |
| `--no-push` | Commit without pushing. Overrides `save.auto_push`. |
| `--no-add` | Skip `git add .`. Overrides `save.auto_add`. |
| `--no-tui` | Skip the wizard entirely and use `save.default_message`. |

## Examples

```sh
# Full interactive wizard
twig save

# Flags only — no wizard
twig save --type feat --scope api --message "add rate limiting"

# Commit without pushing
twig save --no-push

# Commit only staged changes, no auto-add
twig save --no-add --type fix --message "fix edge case in parser"

# Quick commit with default message, skip everything
twig save --no-tui
```

## Commit message format

```
<emoji> <type>(<scope>:<ticket>): <message>
```

All parts except `<message>` are optional depending on what's provided:

```
🎉 feat(api:SHIP-2416): add user auth
🐛 fix(api): handle null response       # no ticket
🧹 chore: bump dependencies             # no scope or ticket
```
