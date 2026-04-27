# Shell Integration

## Shell aliases

The simplest way to keep your existing muscle memory. Add to your `.zshrc` or `.bashrc`:

```sh
alias gco='twig goto'
alias gdo='twig save'
alias gp='twig push'
alias grt='twig root'
alias gprune='twig prune'
```

twig also has built-in short aliases (`twig g`, `twig s` etc.) if you prefer not to define shell aliases.

---

## twig root — changing directory

`twig root` prints the repo root path but cannot change your shell's working directory — that requires a shell function:

```sh
grt() {
  cd "$(twig root)"
}
```

---

## Passthrough — using twig as a git replacement

With `passthrough.enabled = true`, any subcommand twig doesn't recognise is forwarded to git verbatim:

```toml title="~/.config/twig/config.toml"
[passthrough]
enabled     = true
prefer_twig = true    # twig subcommands win on name conflict
```

Then alias `git` to `twig` in your shell:

```sh
alias git=twig
```

Now everything works transparently:

```sh
git rebase -i HEAD~3    # → forwarded to git
git stash               # → forwarded to git
git log --oneline       # → forwarded to git
twig save               # → handled by twig
git save                # → also handled by twig (alias resolves to twig)
```

!!! note
    Passthrough is disabled by default. Enable it intentionally — forwarding unexpected subcommands to git is a one-way door if your config has a typo.

---

## Windows (Git Bash)

The same aliases and shell functions work in Git Bash — paste them into `~/.bashrc`. See the [Windows guide](windows-git-bash.md) for full setup.
