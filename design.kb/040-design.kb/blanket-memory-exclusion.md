---
why:
  - ../020-goals.kb/no-inherited-state.md
---

# Memory exclusion is blanket, not scoped

`claudeMdExcludes` is `["**"]`: every memory file, at every path, excluded.
Placement cannot achieve this, because lookup walks past `$HOME`
(`../../background.kb/memory-lookup-walks-past-home.md`).

Blanket beats scoped on three counts. It survives renaming or cloning the
repo, where a pattern naming a directory would silently stop matching. It
covers file classes nobody enumerated -- `.claude/rules/` escapes a list
written to catch `CLAUDE.md`. And it has no partial state: one pattern either
works or visibly does not, where a list of six can leave a single ancestor
leaking with everything appearing fine.

The cost is that a project's own `CLAUDE.md` is invisible inside the room
too. An experiment that needs one deletes the line; its absence then shows up
in `/context`, which is the right place to notice it.

This is also why `home/` holds no `CLAUDE.md` of its own. One lived there as
a marker meaning "deliberately empty", until a probe confirmed the room's own
root is excluded like every other path -- a file that cannot load is a note
to a reader, and the readers who need it are reading this instead.

This exclusion, not the layout, is what keeps the repo root out of the room.
The root is free to hold a README, a LICENSE, CI workflows, and these
knowledge bases because of this line.
