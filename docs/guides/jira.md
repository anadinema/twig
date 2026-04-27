# Jira Integration

twig can automatically detect Jira ticket references from your branch name and include them in commit messages.

## How it works

When you run `twig save`, twig scans the current branch name for patterns matching `<PREFIX>-<NUMBER>` using the prefixes you configure. If a match is found, the ticket ID is auto-populated in the TUI and appended to the commit message.

```
branch: feat/SHIP-2838-add-auth
         ↓ detected
commit: 🎉 feat(api:SHIP-2838): add user authentication
```

## Configuration

```toml
[save]
ticket_prefixes = ["SHIP", "DEX", "NEDI"]
```

Add every Jira project key your team uses. The detection is case-sensitive and matches the prefix exactly.

## Supported branch name formats

twig detects tickets in any position in the branch name:

```
SHIP-2416                     → ticket: SHIP-2416
feat/SHIP-2838                → ticket: SHIP-2838
fix-SHIP-2474-auth-null       → ticket: SHIP-2474
my-branch-SHIP-9001-something → ticket: SHIP-9001
```

If multiple ticket patterns are found (e.g. a branch named `SHIP-1-DEX-2`), twig uses the first match.

## Overriding in the TUI

The detected ticket is pre-filled in the TUI but editable. You can clear it, change it, or skip it entirely. Use `--no-ticket` to suppress detection for a single commit:

```sh
twig save --no-ticket
```

Or provide a different ticket explicitly:

```sh
twig save --ticket DEX-9001
```

## No Jira

If you don't use Jira or don't want ticket references, simply don't set `ticket_prefixes`. The ticket field won't appear in the TUI at all.
