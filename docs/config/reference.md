# Configuration Reference

Complete reference for every field in `~/.config/twig/config.toml` (or `config.yaml`).

All fields are optional. twig ships with sensible defaults for everything.

---

## [passthrough]

Controls whether unknown subcommands are forwarded to git.

| Field | Type | Default | Description |
|---|---|---|---|
| `enabled` | bool | `false` | When `true`, subcommands twig does not recognise are passed to git verbatim with all original arguments, flags, exit codes, stdout, and stderr unchanged. |
| `prefer_twig` | bool | `true` | When `true` and passthrough is enabled, twig's own subcommands take priority over git commands of the same name. When `false`, git wins on conflict. |

```toml
[passthrough]
enabled     = false
prefer_twig = true
```

!!! tip "Using twig as a git drop-in"
    With `enabled = true` and `alias git=twig` in your shell, all existing git commands continue to work. twig handles `goto`, `save`, `push`, `root`, and `prune`; everything else goes to git.

---

## [save]

Controls the `twig save` command — commit message construction, push behaviour, and the TUI wizard.

| Field | Type | Default | Description |
|---|---|---|---|
| `default_message` | string | `"quick fixes on code"` | Commit message used when `--message` is not provided and the TUI is skipped via `--no-tui`. |
| `auto_push` | bool | `true` | Push to remote after committing. `--no-push` overrides per invocation. |
| `auto_add` | bool | `true` | Stage all changes before committing (`git add .`). `--no-add` overrides per invocation. |
| `ticket_prefixes` | string[] | `[]` | Jira project key prefixes. twig scans the current branch name for `<PREFIX>-<NUMBER>` patterns (e.g. `SHIP-2416`). If found, the ticket is auto-suggested in the TUI and appended to the commit message. |
| `disabled_types` | string[] | `[]` | Remove specific default commit types from the TUI picker. Valid values: `feat`, `fix`, `chore`, `test`, `docs`. |

```toml
[save]
default_message = "quick fixes on code"
auto_push       = true
auto_add        = true
ticket_prefixes = ["SHIP", "DEX"]
disabled_types  = []
```

### Default commit types

These are shipped in the twig binary and require no config:

| Type | Emoji | When to use |
|---|---|---|
| `feat` | 🎉 | New behaviour or capability |
| `fix` | 🐛 | Something broken is now fixed |
| `chore` | 🧹 | Maintenance, deps, config, refactor, CI — anything that isn't feat or fix |
| `test` | 🧪 | Adding or updating tests |
| `docs` | 📚 | Documentation only — signals no code changed |

### Adding extra types

To add project-specific types on top of the defaults:

```toml
[[save.extra_types]]
emoji       = "🔥"
label       = "hotfix"
description = "Emergency production fix"
```

Repeat the block for each additional type. Extra types appear after the default types in the picker.

### Removing default types

```toml
[save]
disabled_types = ["test", "docs"]
```

---

## [save.scopes]

Controls the scope picker in the `twig save` TUI.

| Field | Type | Default | Description |
|---|---|---|---|
| `pinned` | string[] | `[]` | Scopes always shown at the top of the picker regardless of history. Never expire. |
| `history_limit` | integer | `20` | Maximum number of scopes kept in the history file. When the limit is reached, the oldest entry is dropped. Set to `0` for unlimited. |
| `history_dedup` | bool | `true` | Skip saving a scope to history if it already exists in `pinned` or recent history. |

```toml
[save.scopes]
# pinned        = ["api", "infra", "ci", "docs"]
history_limit   = 20
history_dedup   = true
```

**Scope history file:** `~/.local/share/twig/scope_history` — managed automatically, never hand-edited.

**Picker order:** pinned scopes first (visually separated), then recent history newest-first, then older history.

---

## [goto]

Controls the `twig goto` command — the interactive branch picker and branch creation behaviour.

| Field | Type | Default | Description |
|---|---|---|---|
| `local_only` | bool | `false` | Show only local branches in the picker. Skips fetching and listing remote branches. `--local-only` overrides per invocation. |
| `confirm_new` | bool | `true` | When a typed branch name doesn't exist locally or on the remote, ask for confirmation before creating it. When `false`, creates immediately. |
| `skip_patterns` | string[] | `["dependabot/*", "dependabot-*"]` | Glob patterns for branches to hide from the picker. Matched against the branch name. |

```toml
[goto]
local_only    = false
confirm_new   = true
skip_patterns = ["dependabot/*", "dependabot-*"]
```

---

## [prune]

Controls the `twig prune` command — cleanup of stale local branches.

A branch is eligible for pruning when **all** of these are true:

- It is not the current branch
- It is not in `protected_branches`
- It has no corresponding remote branch on origin
- Its last commit is older than `default_days` days

| Field | Type | Default | Description |
|---|---|---|---|
| `default_days` | integer | `30` | Branches with a last commit older than this many days are eligible for pruning. Override per invocation with `--days N`. |
| `protected_branches` | string[] | `["main", "develop", "master"]` | Branches never eligible for pruning regardless of age or remote status. |
| `require_clean_tree` | bool | `true` | Abort pruning if the working tree has uncommitted changes. |

```toml
[prune]
default_days       = 30
protected_branches = ["main", "develop", "master"]
require_clean_tree = true
```

---

## [aliases]

Short aliases for twig subcommands. Single-character or abbreviated forms.

| Field | Type | Default | Description |
|---|---|---|---|
| `<alias>` | string | — | Maps the alias to a subcommand name. Value must exactly match a twig subcommand. |

```toml
[aliases]
g  = "goto"
s  = "save"
ps = "push"
rt = "root"
pr = "prune"
```

Usage: `twig g` is equivalent to `twig goto`. Aliases work with all flags: `twig g --local-only`.
