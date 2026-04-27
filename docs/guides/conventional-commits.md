# Conventional Commits

twig's `save` command follows the [Conventional Commits](https://www.conventionalcommits.org/) specification. This page explains the format and how twig assembles commit messages.

## Format

```
<emoji> <type>(<scope>:<ticket>): <message>
```

All parts except `<type>` and `<message>` are optional:

```
🎉 feat(api:SHIP-2416): add user authentication endpoint
🐛 fix(api): handle null response from auth service
🧹 chore: bump dependencies
```

## Types

| Type | Emoji | Meaning |
|---|---|---|
| `feat` | 🎉 | New behaviour or capability |
| `fix` | 🐛 | Something broken is now fixed |
| `chore` | 🧹 | Maintenance, config, deps, refactor, CI |
| `test` | 🧪 | Adding or updating tests |
| `docs` | 📚 | Documentation only |

## Scopes

The scope identifies **what part of the codebase** the commit touches. It's project-specific — twig doesn't enforce any particular scopes. Examples: `api`, `infra`, `ci`, `auth`, `db`.

Configure frequently-used scopes as pinned so they always appear at the top of the picker:

```toml
[save.scopes]
pinned = ["api", "infra", "ci", "docs"]
```

## Why conventional commits

- Machine-readable — tools like goreleaser use commit types to generate changelogs and determine version bumps automatically
- Scannable — `git log` becomes useful at a glance
- Self-documenting — the type and scope explain intent without reading the diff
