# twig root

Print the root directory of the current git repository.

## Usage

```sh
twig root
twig rt
```

## Description

Prints the absolute path to the root of the current git repository — the directory containing `.git`. Useful for scripting or jumping to the repo root in your shell.

## Shell integration

To make `twig root` change your current directory (not just print it), add this function to your `.zshrc` or `.bashrc`:

```sh
grt() {
  cd "$(twig root)"
}
```

This is necessary because a subprocess cannot change the parent shell's working directory — the function wrapper handles that.

## Examples

```sh
# Print repo root
twig root
# → /Users/you/dev/myproject

# Use in a script
cp build/output.zip "$(twig root)/dist/"
```

!!! note
    Running `twig root` outside a git repository exits with a non-zero status and prints an error. This makes it safe to use in scripts that need to guard against non-repo directories.
