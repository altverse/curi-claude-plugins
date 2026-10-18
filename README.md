# Curi plugins for Claude

Claude plugins from [Curi](https://askcuri.com) (Blackhoods Inc.).

| Plugin | What it does |
|---|---|
| [`channel`](./channel) | Plan topics and email campaigns in [channel](https://channel.askcuri.com) from Claude. Creates **drafts only** — sending and scheduling stay in channel web. |
| [`signal`](./signal) | Draft surveys with AI, publish after you confirm the title, and read masked results and report PDFs in [signal](https://signal.askcuri.com) from Claude. |

## Install

```
/plugin marketplace add altverse/curi-claude-plugins
/plugin install channel@curi-claude-plugins
/plugin install signal@curi-claude-plugins
```

The `channel` plugin connects to `https://api-channel.askcuri.com/mcp`. Sign in with any Google account; a first-time account gets a sample workspace so every tool returns something to look at.

The `signal` plugin connects to `https://api-signal.askcuri.com/mcp`. Reading needs the Claude connector (read) feature, on every plan; drafting and publishing need Claude connector (write), from Starter up. An account with no team gets an example team with a sample survey and synthetic responses (drafts capped at 3 a day, no publishing).

Docs: https://askcuri.com/docs/claude · Privacy: https://askcuri.com/en/terms/privacy · Contact: calix@askcuri.com
