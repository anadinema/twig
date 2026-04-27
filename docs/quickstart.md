# Quickstart

Get twig working in about two minutes. No config required to start.

---

## 1. Install

=== "macOS"

    ```sh
    brew tap anadinema/tap && brew install twig
    ```

=== "Linux / Git Bash"

    ```sh
    curl --proto '=https' --tlsv1.2 -sSf https://twig.anadinema.dev/install.sh | bash -s -- --to ~/.local/bin
    ```

---

## 2. Try it — no config needed

twig works out of the box with sensible defaults. Inside any git repo:

```sh
# Open the interactive branch picker
twig goto

# Commit with the guided TUI wizard
twig save

# Push current branch
twig push

# See stale local branches eligible for cleanup
twig prune --dry-run
```

---

## 3. Add shell aliases (optional but recommended)

Add these to your `.zshrc` or `.bashrc` to keep your short-form muscle memory:

```sh
alias gco='twig goto'
alias gdo='twig save'
alias gp='twig push'
alias grt='twig root'
alias gprune='twig prune'
```

Or use twig's built-in aliases directly:

```sh
twig g    # goto
twig s    # save
twig ps   # push
twig rt   # root
twig pr   # prune
```

---

## 4. Create a config file (optional)

twig's defaults cover most cases. Create a config only when you want to customise behaviour.

```sh
mkdir -p ~/.config/twig
```

```toml title="~/.config/twig/config.toml"
[save]
ticket_prefixes = ["SHIP", "DEX"]    # auto-detect Jira tickets from branch names

[save.scopes]
pinned = ["api", "infra", "ci"]      # always shown at top of scope picker
```

That's a typical minimal config. See the [full reference](config/reference.md) for everything available.

---

## 5. Enable passthrough (optional)

To use twig as a full git replacement — passing unknown commands through to git transparently:

```toml title="~/.config/twig/config.toml"
[passthrough]
enabled = true
```

Then alias `git` to `twig` in your shell:

```sh
alias git=twig
```

Now `git rebase -i`, `git stash`, `git log` all continue to work exactly as before.
