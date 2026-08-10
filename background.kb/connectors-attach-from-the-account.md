---
version: 2.1.226
established-by: [probe]
---

# Connectors attach from the account, not the config dir

The claude.ai MCP connectors -- Gmail, Google Calendar, Google Drive --
attach to a session on the strength of the logged-in account. They are not
configured locally, so an empty config dir does not exclude them and deleting
local state does not detach them.

## Evidence

A probe home whose config dir held nothing but `settings.json` and a linked
credential file accumulated
`.cache/claude-cli-nodejs/*/mcp-logs-claude-ai-Google-Drive/` on every run.

## Consequence

Emptiness by deletion has a floor. Whatever arrives with the account or with
the binary survives every reset and has to be turned off by settings instead,
which `./disable-settings-cover-whole-classes.md` establishes that they can
be.
