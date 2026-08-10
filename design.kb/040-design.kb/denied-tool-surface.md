---
why:
  - ../020-goals.kb/no-inherited-state.md
---

# The tool surface is denied, not merely absent

`home/.config/claude/settings.json` denies some thirty tools outright and
sets `disableBundledSkills`, `disableClaudeAiConnectors`, and
`disableWorkflows`, rather than trusting an empty config dir to leave them
unavailable.

The connectors are covered twice over -- by the blanket setting and by three
`mcp__claude_ai_*` denies that predate it. The setting is the one that
survives a fourth connector being added, so the names go once a probe
confirms it works alone.

Deletion has a floor. The claude.ai connectors arrive with the account
(`../../background.kb/connectors-attach-from-the-account.md`) and bundled
skills arrive inside the binary. Neither is local state, so emptying local
state removes neither.

The denials also serve the baseline in their own right. Task management,
artifacts, plan mode, and inter-agent messaging each change how a session
behaves, so leaving them available would fold them into the baseline -- a
different confound than an inherited CLAUDE.md, but a confound. What the room
measures is a session with the smallest defensible tool surface, not a
maximal one that merely lacks memory.
