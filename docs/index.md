# twig

**A better git experience** — opinionated commit workflows, a built-in branch picker TUI, and transparent git passthrough. No fzf required.

twig wraps git to make the things you do every day — switching branches, writing conventional commits, cleaning up stale branches — feel like they should have always worked this way. For everything else, twig gets out of the way and passes it straight to git.

---

## What it does

```sh
# Switch branches with an interactive picker
twig goto

# Or jump straight to a branch by name
twig goto feat/SHIP-2838

# Commit with a guided TUI wizard — type, scope, ticket auto-detected
twig save

# Or commit with flags for scripting
twig save --type fix --scope api --message "handle null auth response"

# Push the current branch
twig push

# Clean up stale local branches
twig prune

# Jump to repo root from anywhere
twig root
```

## Why

Git's CLI is powerful but low-level. Wrapping common workflows in shell functions works until the functions break in subtle ways, don't work cross-platform, and can't be tested. twig replaces those functions with a single compiled binary that works identically on macOS, Linux, and Windows (Git Bash).

If twig doesn't know a command, it [passes it through](guides/shell-integration.md) to git transparently — so you can alias `git` to `twig` and nothing breaks.

---

## Quick install

=== "macOS (Homebrew)"

    ```sh
    brew tap anadinema/tap
    brew install twig
    ```

=== "Linux"

    ```sh
    curl --proto '=https' --tlsv1.2 -sSf https://twig.anadinema.dev/install.sh | bash -s -- --to ~/.local/bin
    ```

=== "Windows (Git Bash)"

    Download the `linux_amd64` binary from the [latest release](https://github.com/anadinema/twig/releases/latest) and place it in `~/bin`.

    See the full [Windows guide](guides/windows-git-bash.md).

---

[Get started →](install.md){ .md-button .md-button--primary }
[Configuration reference →](config/reference.md){ .md-button }
