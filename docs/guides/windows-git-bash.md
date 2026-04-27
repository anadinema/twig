# Windows (Git Bash)

twig works on Windows inside Git Bash using the Linux `amd64` binary. The built-in TUI renders correctly in Git Bash's PTY — no Windows terminal compatibility issues.

## Install

1. Download `twig_linux_amd64` from the [latest release](https://github.com/anadinema/twig/releases/latest)
2. Place it in `~/bin` (Git Bash adds this to `PATH` automatically):

```sh
mkdir -p ~/bin
mv ~/Downloads/twig_linux_amd64 ~/bin/twig
chmod +x ~/bin/twig
```

3. Verify:

```sh
twig --version
```

## Shell aliases

Add to `~/.bashrc`:

```sh
alias gco='twig goto'
alias gdo='twig save'
alias gp='twig push'
alias gprune='twig prune'

# twig root needs a function to change directory
grt() {
  cd "$(twig root)"
}
```

Reload: `source ~/.bashrc`

## VS Code integration

If VS Code is your primary editor with Git Bash as the default terminal, no extra setup is needed. twig works in the integrated terminal identically to a standalone Git Bash window.

Your npm scripts continue to run in Git Bash as normal — twig doesn't affect that setup.

!!! tip
    Keep Git Bash as your VS Code default terminal. The Linux binary works natively there, you get the full TUI experience, and your Node tooling stays unaffected.
