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
    git -C <repo> status --short home/

## Reading the result

`OK` means three things at once: direnv is allowed, `HOME` and
`CLAUDE_CONFIG_DIR` resolve, and the credential file is readable.

`Not logged in - Please run /login` means only the last one failed. Seed
`.config/claude/.credentials.json` as `README.md` describes; nothing else is
wrong.

The `status` half is the point of running them together. A single
non-interactive run creates `projects/`, `sessions/`, `backups/`, and
`.claude.json` in the config dir, and every one of them must come back
ignored.

Anything else git reports is a session writing somewhere this repo has not
seen it write before, which is a finding rather than a failure: read it,
then add the path to `home/.gitignore` with a note saying what produced it
(`../design.kb/040-design.kb/ignores-name-only-known-exhaust.md`). A
modification to `.claude/settings.local.json` is the loudest such finding
(`../design.kb/040-design.kb/tracked-tripwire-for-local-settings.md`) --
something wrote settings into the room.

The check is total, not partial: the ignore rules name only exhaust already
observed, so a clean `status` is a claim about the room rather than an
artifact of a blanket rule.

Total over what this procedure runs, which is one non-interactive session. An
interactive start writes nine paths that `claude -p` never produces
(`../background.kb/interactive-startup-populates-the-room.md`), so the first
interactive session in a fresh or freshly-cleaned room wants the same
`status` afterward. That is how those nine were found.
