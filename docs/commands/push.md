# twig push

Push the current branch to origin.

## Usage

```sh
twig push [branch] [flags]
twig ps [branch] [flags]
```

## Description

Pushes the current branch to `origin`. Equivalent to `git push origin <current-branch>`.

With a branch name argument, pushes that branch instead.

## Flags

| Flag | Description |
|---|---|
| `--force` | Force push. Equivalent to `git push --force-with-lease origin <branch>`. Uses `--force-with-lease` rather than `--force` for safety — aborts if the remote has changes you haven't fetched. |

## Examples

```sh
# Push current branch
twig push

# Push a specific branch
twig push feat/SHIP-2838

# Force push current branch
twig push --force
```

!!! warning
    `--force` uses `--force-with-lease` under the hood. This is safer than a plain force push but still rewrites remote history. Use with care on shared branches.
