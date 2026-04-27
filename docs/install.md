# Install

## Requirements

- git installed and on your `PATH`
- macOS 12+, Linux (amd64/arm64), or Windows via Git Bash

twig has no other runtime dependencies. The interactive TUI is built in — no fzf or external picker needed.

---

## macOS

```sh
brew tap anadinema/tap
brew install twig
```

To upgrade:

```sh
brew upgrade twig
```

---

## Linux

### Install script

```sh
curl --proto '=https' --tlsv1.2 -sSf https://twig.anadinema.dev/install.sh | bash -s -- --to ~/.local/bin
```

The script detects your architecture and installs the binary to the path specified by `--to`. Make sure that directory is on your `PATH`.

### Manual

Download the binary for your architecture from the [releases page](https://github.com/anadinema/twig/releases/latest), make it executable, and move it to somewhere on your `PATH`.

```sh
# Example for linux/amd64
curl -Lo twig https://github.com/anadinema/twig/releases/latest/download/twig_linux_amd64
chmod +x twig
mv twig ~/.local/bin/twig
```

---

## Windows (Git Bash)

twig works best inside Git Bash using the `linux_amd64` binary. This gives full TUI support without Windows terminal compatibility concerns.

1. Download `twig_linux_amd64` from the [latest release](https://github.com/anadinema/twig/releases/latest)
2. Place it in `~/bin` (Git Bash adds this to `PATH` automatically)
3. Rename and make executable:

```sh
mkdir -p ~/bin
mv ~/Downloads/twig_linux_amd64 ~/bin/twig
chmod +x ~/bin/twig
```

See the [Windows guide](../guides/windows-git-bash.md) for full setup including shell aliases.

---

## Verify

```sh
twig --version
```

---

## Next steps

- [Quickstart](quickstart.md) — up and running in two minutes
- [Configuration reference](../config/reference.md) — all config options
- [Shell integration](../guides/shell-integration.md) — set up aliases and git passthrough
