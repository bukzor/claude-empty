---
version: 2.1.226
established-by: [probe]
---

# Credentials live in the config dir

Claude Code reads and writes OAuth credentials at
`$CLAUDE_CONFIG_DIR/.credentials.json` on Linux. Redirecting the config dir
therefore redirects authentication: a freshly created one is logged out, and
`claude` exits immediately with `Not logged in - Please run /login`.

## Evidence

A probe home with a new config dir refused to start until
`.credentials.json` was symlinked in from the real config dir; the same probe
then ran normally.

The file is invisible to `ls -R`, which is how it was missed the first time.
A room is almost entirely dotfiles, so any inventory of one that omits `-a`
reports emptiness it has not checked.

## Consequence

An empty room is an unusable room until it is seeded, so the credential file
is a deliberate exception to
`../design.kb/020-goals.kb/no-inherited-state.md` -- and the only one.

It is also the only reason the room's ignore rules can name the one file that
must never be committed. A session creates it unprompted, at a dotfile path
an inventory taken with `ls -R` does not report.
