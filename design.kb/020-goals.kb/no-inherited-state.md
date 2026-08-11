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

The one deliberate exception is the credential file, without which the room
cannot start at all
(`../../background.kb/credentials-live-in-the-config-dir.md`).

There is a second exception, undeliberate and unfixed: the program. `PATH`
survives the redirect, so the room runs the machine's Claude Code
(`../../background.kb/the-binary-comes-from-outside-the-room.md`). It does
not violate the sentence above -- a binary is not something that shapes a
session the way a hook does, and every reader of a reproduction supplies
their own anyway -- but it does mean the room cannot state its own version.
A result carried out of here has to quote the version it was produced under,
because no file in the room records it.
