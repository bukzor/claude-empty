---
why:
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
  - ../design.kb/020-goals.kb/resettable-to-empty.md
---

# Smoke-test the room

Confirms the room starts, is authenticated, and leaves nothing git can see.
Run it after any change to `home/`, and before any probe -- a broken room
produces the same silence as a suppressed one.

## Procedure

    ( cd home && direnv exec . claude -p 'Reply with exactly one word: OK' )
    git -C <repo> status --short
    test ! -e home/.claude

## Reading the result

`OK` means three things at once: direnv is allowed, `HOME` and
`CLAUDE_CONFIG_DIR` resolve, and the credential file is readable.

`Not logged in - Please run /login` means only the last one failed. Seed
`.config/claude/.credentials.json` as `README.md` describes; nothing else is
wrong.

The `status` half is the point of running them together. A single
non-interactive run creates `projects/`, `sessions/`, `backups/`, and
`.claude.json` in the config dir, and every one of them must come back
ignored. Anything git reports is a hole in `home/.gitignore`, found at the
cheapest possible moment -- with one file of exhaust rather than a month of
it.

The third line covers what `status` structurally cannot. Settings load from
the working directory
(`../background.kb/settings-load-from-the-working-directory.md`), which in
the room is the room itself, and the ignore rules deny by default -- so a
`.claude/` there would shape every session while `status` stays clean. It is
the one contaminant a passing check actively conceals.
