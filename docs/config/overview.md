# Configuration Overview

twig works without any config file — all defaults are built in. The config file exists only for customisation.

## File location

```
~/.config/twig/config.toml    (TOML — default)
~/.config/twig/config.yaml    (YAML — also supported)
```

If both exist, TOML takes precedence. The directory is not created automatically — create it when you need it.

---

## What needs config and what doesn't

**Works without config:**

- `twig goto` — branch picker, branch creation with confirmation
- `twig save` — TUI wizard with default commit types (feat, fix, chore, test, docs)
- `twig push` — push current branch
- `twig root` — jump to repo root
- `twig prune` — prune branches older than 30 days, skipping main/develop/master

**Requires config to enable:**

- Passthrough to git for unknown commands
- Jira ticket auto-detection from branch names (`ticket_prefixes`)
- Pinned scopes in the save TUI
- Custom or extra commit types
- Overriding default prune thresholds or protected branches

---

## Runtime files

twig maintains one runtime file separate from config — never hand-edited:

| File | Purpose |
|---|---|
| `~/.local/share/twig/scope_history` | Auto-saved scope history for the save TUI picker |

---

## Sections

| Section | Purpose |
|---|---|
| `[passthrough]` | Forward unknown subcommands to git |
| `[save]` | Commit behaviour, ticket detection, type customisation |
| `[save.scopes]` | Pinned scopes and history settings |
| `[goto]` | Branch picker behaviour |
| `[prune]` | Stale branch cleanup settings |
| `[aliases]` | Short aliases for twig subcommands |

See the [full reference](reference.md) for every field.
