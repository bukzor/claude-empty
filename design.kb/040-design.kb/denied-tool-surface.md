---
why:
  - ../020-goals.kb/no-inherited-state.md
---

# The tool surface is denied, not merely absent

`home/.config/claude/settings.json` denies some thirty tools and connectors
outright and sets `disableBundledSkills` and `disableWorkflows`, rather than
trusting an empty config dir to leave them unavailable.

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
