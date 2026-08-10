---
why:
  - ../010-mission.kb/unprimed-baseline-sessions.md
---

# No inherited state

Nothing that shapes a session -- memory files, skills, agents, hooks, MCP
servers, settings -- reaches the room from the real `$HOME`, from any ancestor
directory, or from the account, except by a choice recorded in this repo.

The bar is "nothing arrives", not "nothing is read from `~/.claude/`".
Relocating a lookup does not satisfy this goal if the same content still
arrives by another path.

The single deliberate exception is the credential file, without which the
room cannot start at all
(`../../background.kb/credentials-live-in-the-config-dir.md`).
