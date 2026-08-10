---
version: 2.1.226
established-by: [probe, inference]
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
the binary survives every reset and has to be turned off by settings instead
-- `permissions.deny` for the connectors, `disableBundledSkills` for the
skills that ship inside the executable. See
`../design.kb/040-design.kb/denied-tool-surface.md`.

> [!QUESTION] does disableBundledSkills actually suppress bundled skills?
> Only the connector half of this entry is probed. The bundled-skill half is
> argued from the setting's existence -- hence the `inference` in this
> entry's `established-by`. `../testing.kb/check-what-reaches-the-room.md`
> adapts to settle it: ask a probe session to name the skills available to
> it, with the setting and without.
