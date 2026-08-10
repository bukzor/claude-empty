---
why:
  - ../020-goals.kb/emptiness-is-verifiable.md
  - ../020-goals.kb/no-inherited-state.md
---

# An empty local-settings file is committed as a tripwire

`home/.claude/settings.local.json` is tracked, and holds `{}`.

It exists so that a write to it is loud. Settings load from the working
directory (`../../background.kb/settings-load-from-the-working-directory.md`),
which in the room is the room itself, and Claude Code records a permission
granted "always" in a file of exactly this name. Committing an empty one
turns that write from a file appearing where nobody looks into a one-line
diff.

Tracking is what does the work, not the file's contents. Git consults
`.gitignore` only for untracked paths, so a tracked file reports its own
modification however the ignore rules change around it -- including a change
made by someone who never read `ignores-name-only-known-exhaust.md`. The
tripwire and the ignore rules answer the same threat independently, which is
the point of having both.

`{}` rather than an absent file: a merged empty object changes nothing about
a session, since the room's real settings live in the user scope at
`.config/claude/settings.json`, while an absent file leaves nothing to diff
against.

The tripwire is also this repo's answer to its own open question. Whether
Claude Code writes that grant beside the working directory is unprobed, and
probing it needs an interactive session; the committed file will report the
answer the first time anyone grants a permission in the room, without anyone
having to remember to look.
