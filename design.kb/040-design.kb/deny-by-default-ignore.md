---
why:
  - ../020-goals.kb/resettable-to-empty.md
  - ../020-goals.kb/no-inherited-state.md
---

# The room's ignore rules deny by default

`home/.gitignore` ignores `/*` and then re-admits only the files that define
the room, re-including each parent directory in turn so that the re-admission
can reach down into `.config/claude/`.

An allowlist is the only shape that holds, because the room's exhaust is
unbounded and partly secret. A session writes credentials, transcripts, shell
history, and its own copy of the `claude` binary, at paths that follow the
tool's version rather than this repo's expectations. A denylist protects
against the files someone thought of, which is the wrong set.

The same rule is what makes the reset cheap: anything not named is disposable
by definition, so the distinction between "defines the room" and "was left in
the room" is mechanical rather than remembered, and `git status` inside the
room stays readable enough to trust.
