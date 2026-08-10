---
version: 2.1.226
established-by: [probe]
---

# Memory-file lookup walks past $HOME

Claude Code discovers `CLAUDE.md`, `CLAUDE.local.md`, and `.claude/rules/` by
walking up the directory tree from the working directory. `$HOME` is not a
boundary: a memory file in any ancestor loads, including ancestors outside
the redirected home.

Redirecting `HOME` therefore does not by itself produce an empty session. It
relocates the user-scope lookup; it does not stop the walk.

## Evidence

Via `../testing.kb/check-what-reaches-the-room.md`. A `CLAUDE.md` placed
one directory *above* a redirected `HOME` returned its marker verbatim
from `claude -p`, as did a `.claude/rules/*.md` inside the redirected home.
Both returned `NONE` once `claudeMdExcludes` was set to `["**"]`.

## Consequence

Every directory above the room -- this repo's root, `~/repo/`, `~/`, `/` --
is a memory-file injection site, and the set of them is not under this
repo's control. The design cannot rely on placement; it relies on exclusion.
See `../design.kb/040-design.kb/blanket-memory-exclusion.md`.
