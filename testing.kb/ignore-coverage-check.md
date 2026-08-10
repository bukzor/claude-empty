---
why:
  - ../design.kb/020-goals.kb/resettable-to-empty.md
---

# Ignore-coverage check

Confirms `home/.gitignore` still admits exactly the files that define the
room, after any change to it or to the room's layout.

## Procedure

Name the paths a session is known to create -- transcripts, caches, shell
history, credentials, the downloaded binary -- and ask git about each:

    git -C <repo> check-ignore -v \
      home/.config/claude/.credentials.json \
      home/.config/claude/projects \
      home/.cache/x home/.npm/y home/.bash_history

Every path must report the rule that ignores it. Then check the opposite
error, a defining file silently dropped:

    git -C <repo> add --dry-run -A .

## Reading the result

`check-ignore` answers about paths, not files, so it works on exhaust a run
has not produced yet -- which is the point, since the coverage that matters
is for files that do not exist during the check.

It cannot catch a rule that ignores a file git already tracks: tracked files
are never consulted against `.gitignore`. That failure shows up only in
`add --dry-run`, which is why both halves are run.
