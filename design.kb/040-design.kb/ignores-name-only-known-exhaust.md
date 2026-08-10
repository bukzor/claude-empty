---
why:
  - ../020-goals.kb/emptiness-is-verifiable.md
  - ../020-goals.kb/resettable-to-empty.md
---

# The ignore rules name only known exhaust

`home/.gitignore` lists the paths a session is known to write -- Claude
Code's config-dir state, and the credential file -- and ignores nothing else.
Anything a session leaves that is not on that list appears in `git status` as
an untracked file.

The rule this replaced was the opposite shape: ignore `/*`, re-admit the few
files that define the room. That shape is defensible in the abstract, since
the exhaust is the tool's to name and not this repo's. It is wrong here
anyway, because it makes a contaminated room and a clean one produce
identical output. The one thing it optimizes -- a quiet `git status` -- is
the instrument this repo reads.

The abstract argument also lost on the facts. After several sessions the
room's exhaust is six paths, all inside `.config/claude/`, not the unbounded
scatter the earlier reasoning assumed. Where that stops being true -- an
interactive session, a self-update -- the list grows by a line, and the line
records a discovery instead of performing a chore.

The file opens with `!/**`, re-including everything, because the user's
global ignore file hides `**/.claude/settings.local.json`, `**/CLAUDE.local.md`,
`tmp/`, and `*.log` in every repo on the machine. Each of those is something
the room needs to see, and the first was already hiding this repo's own
tripwire when the rule was written. What the room reports must not depend on
a file outside the repo -- the same boundary
`home-redirect-scoped-to-the-room.md` draws for what the room *reads*.

Two costs, both accepted. A new secret arriving under a new name is untracked
rather than ignored, so `git add -A` would take it; that is the price of
seeing it at all, and the mitigation is that `git status` now says something
worth reading. And the room gets noisy the first time a session writes
something new -- which is the alarm working, not a defect.
