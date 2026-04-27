# Full Config

Complete `~/.config/twig/config.toml` with every option explicitly set. Use this as a reference — in practice most of these can be omitted to use the defaults.

```toml title="~/.config/twig/config.toml"
# ─── Passthrough ──────────────────────────────────────────────────────────────
[passthrough]
enabled     = false    # opt-in — forwards unknown subcommands to git
prefer_twig = true     # twig subcommands win over git on name conflict

# ─── Save (commit + push) ─────────────────────────────────────────────────────
[save]
default_message = "quick fixes on code"
auto_push       = true
auto_add        = true

# Jira ticket auto-detection from branch name
ticket_prefixes = ["SHIP", "DEX", "NEDI"]

# Remove any default types you don't want (feat, fix, chore, test, docs)
disabled_types = []

# Add project-specific commit types on top of the defaults
[[save.extra_types]]
emoji       = "🔥"
label       = "hotfix"
description = "Emergency production fix"

[save.scopes]
pinned        = ["api", "infra", "ci", "docs"]
history_limit = 20
history_dedup = true

# ─── Goto (branch switch / create) ───────────────────────────────────────────
[goto]
local_only    = false
confirm_new   = true
skip_patterns = ["dependabot/*", "dependabot-*"]

# ─── Prune ────────────────────────────────────────────────────────────────────
[prune]
default_days       = 30
protected_branches = ["main", "develop", "master"]
require_clean_tree = true

# ─── Aliases ──────────────────────────────────────────────────────────────────
[aliases]
g  = "goto"
s  = "save"
ps = "push"
rt = "root"
pr = "prune"
```
