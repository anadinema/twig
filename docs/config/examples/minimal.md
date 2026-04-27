# Minimal Config

The smallest useful config — just Jira ticket detection and a couple of pinned scopes. Everything else uses twig's built-in defaults.

```toml title="~/.config/twig/config.toml"
[save]
ticket_prefixes = ["SHIP"]

[save.scopes]
pinned = ["api", "infra", "ci"]
```

That's it. No other config is needed for most day-to-day use.
