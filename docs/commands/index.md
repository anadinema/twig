# Commands

twig provides five focused subcommands. For anything else, enable [passthrough](../guides/shell-integration.md) to forward to git transparently.

| Command | Alias | Description |
|---|---|---|
| [`twig goto`](goto.md) | `g` | Switch branches with a TUI picker, or jump to a branch by name |
| [`twig save`](save.md) | `s` | Commit with a guided TUI wizard or flags |
| [`twig push`](push.md) | `ps` | Push the current branch to origin |
| [`twig root`](root.md) | `rt` | Print the repo root path |
| [`twig prune`](prune.md) | `pr` | Clean up stale local branches |

## Global flags

| Flag | Description |
|---|---|
| `--config <path>` | Use a config file at a custom path |
| `--help` | Show help |
| `--version` | Print twig version |
