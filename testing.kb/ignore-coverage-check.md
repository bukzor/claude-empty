---
why:
  - ../design.kb/020-goals.kb/resettable-to-empty.md
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
---

# Ignore-coverage check

Confirms `home/.gitignore` still ignores the room's known exhaust and nothing
else, after any change to it, to the room's layout, or to the machine's
global ignore file.

## Procedure

Ask git which rule covers each path a session is known to write:

    git -C <repo> check-ignore -v \
      home/.config/claude/.credentials.json \
      home/.config/claude/projects \
      home/.config/claude/backups

Each must report a rule, and the rule must live in `home/.gitignore`. Then
the opposite error -- a rule broader than the evidence for it, swallowing
something the room was supposed to report:

    git -C <repo> check-ignore -v \
      home/.claude/settings.local.json home/CLAUDE.local.md \
      home/tmp/x home/x.log home/.cache/y home/.bash_history

Each of these must report the `!/**` negation. Anything else means a pattern
is hiding a path the room has never been shown to produce. Finally, the
defining files must still be addable:

    git -C <repo> add --dry-run -A home/

## Reading the result

`check-ignore` answers about paths, not files, so both halves work on files
that do not exist yet -- which is the point, since the coverage that matters
is for paths nothing has created.

Read the source file in the `-v` output, not just the exit status. The second
half exists because the machine's `~/.config/git/ignore` matches
`**/.claude/settings.local.json` and `**/CLAUDE.local.md` in every repo, and
it was hiding this room's own tripwire until `!/**` was added. That failure
is silent from inside the repo: the rule is real, applies, and is written
somewhere this repo does not version.

Read *which* rule matched, not merely that one did. Half of these patterns
were once written with a trailing `#` comment, which gitignore does not
have: the comment text joined the pattern and the pattern then matched
nothing. Every path fell through to `!/**` and stayed visible, which reads
exactly like a correctly visible path unless you check the rule.

Neither half can catch a rule that ignores a file git already tracks, since
tracked paths are never consulted against `.gitignore`. That one shows up
only in `add --dry-run`, which is why all three run.
