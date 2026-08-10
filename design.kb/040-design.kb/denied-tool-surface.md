---
why:
  - ../020-goals.kb/no-inherited-state.md
---

# The tool surface is denied, not merely absent

`home/.config/claude/settings.json` sets `disableBundledSkills`,
`disableClaudeAiConnectors`, and `disableWorkflows`, and denies some
twenty-six tools by name, rather than trusting an empty config dir to leave
them unavailable.

The split is deliberate. Where a setting covers a whole class it is the only
mechanism used, because a list of member names goes stale the week a new
member ships and nothing looks wrong when it does
(`../../background.kb/disable-settings-cover-whole-classes.md`). The deny
list is what remains: individual tools with no class-level switch.

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
