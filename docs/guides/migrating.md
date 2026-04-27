# Migrating from Shell Functions

If you're coming from a set of shell functions like `gco`, `gdo`, `gp`, `grt`, and `gprune`, this guide maps each to its twig equivalent.

## Command mapping

| Shell function | twig equivalent | Notes |
|---|---|---|
| `grt` | `twig root` (via shell function) | Needs a `cd "$(twig root)"` wrapper — see [shell integration](shell-integration.md) |
| `gp` | `twig push` | `gp +branch` force push → `twig push --force` |
| `gdo` | `twig save --no-tui` | For quick commits with default message |
| `gdp` | `twig save` | Full TUI wizard replaces the fzf-based gdp flow |
| `gco` | `twig goto` | TUI picker replaces fzf, branch creation fixed |
| `gprune` | `twig prune` | `--debug branch` replaces `gprune_debug` |
| `gprune_debug` | `twig prune --debug <branch>` | Absorbed as a flag |

## What's better

**`twig goto` fixes branch creation.** The old `gco` had a known bug where creating a new local branch sometimes failed silently. twig handles the local/remote/new branch cases explicitly with proper error handling and confirmation.

**`twig save` replaces both `gdo` and `gdp`.** The old split between "quick commit" (`gdo`) and "guided commit" (`gdp`) is unified — `twig save` with no flags launches the wizard, with flags it's a one-liner. The scope history works the same way but is stored cleanly in `~/.local/share/twig/scope_history` instead of a dotfiles temp file.

**No fzf dependency.** The interactive pickers in `twig goto` and `twig save` are built into the binary. No external tooling needed — works identically on macOS, Linux, and Windows Git Bash.

**Testable and debuggable.** Shell functions fail silently and are hard to reproduce. twig is a compiled binary with consistent behaviour across environments.

## Migration steps

1. Install twig — see [install](../install.md)
2. Add shell aliases to your `.zshrc` or `.bashrc` — see [shell integration](shell-integration.md)
3. Create a minimal config if you use Jira tickets or pinned scopes — see [minimal example](../config/examples/minimal.md)
4. Test `twig goto`, `twig save`, `twig prune --dry-run`
5. Remove the old shell functions once you're comfortable

## Keeping old functions temporarily

Rename them while you test twig in parallel:

```sh
_legacy_gco() { ... }
_legacy_gdo() { ... }
_legacy_gdp() { ... }
```

Fall back if needed, remove when you're confident.
