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
-- `disableClaudeAiConnectors` for the connectors, `disableBundledSkills` for
the skills that ship inside the executable. See
`../design.kb/040-design.kb/denied-tool-surface.md`.

> [!QUESTION] do the suppression settings actually suppress anything?
> What is probed is that the connectors arrive. That they can be turned off
> -- by `disableClaudeAiConnectors`, or bundled skills by
> `disableBundledSkills` -- is argued from the settings' existence and from
> their use in the real `~/.claude/settings.json`, hence the `inference` in
> this entry's `established-by`. `../testing.kb/check-what-reaches-the-room.md`
> adapts to settle both in one run: ask a probe session to name the skills
> and connectors available to it, with the settings and without.
