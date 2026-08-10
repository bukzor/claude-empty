---
why:
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
---

# Find where a settings file is read from

Determines which paths a session loads settings from, by holding one settings
file's content fixed and moving it.

## Procedure

1. Build a throwaway home under `trash/` as `check-what-reaches-the-room.md`
   describes, reproducing the geometry in question -- including a `git init`
   at whatever layer stands in for the repo root, since a lookup could
   plausibly key on the git root rather than on the parent.
2. Write one settings file carrying two effects at once: a `model` the room's
   own settings do not select, and a `permissions.deny` list long enough to
   strip several thousand tokens of tool schemas.
3. Run one arm per candidate location, moving that same file between them,
   plus a control arm with the file absent:

       ( cd $room && HOME=$PWD CLAUDE_CONFIG_DIR=$PWD/.config/claude \
         claude -p --output-format json 'Reply with exactly: OK' ) > arm.json

4. Read `.modelUsage | keys` from each arm, and the sum of `.usage`'s
   `input_tokens`, `cache_creation_input_tokens`, and
   `cache_read_input_tokens`.
5. Unlink the probe's `.credentials.json`, the one part of it that is not
   disposable. The rest stays where it was built: it is already in `trash/`,
   and the arms are the evidence behind the entry they established.

## Reading the result

A loaded arm swaps the model *and* drops the token total; an ignored arm
moves neither. Two readouts for one API call, and they fail independently: a
model swap alone means the deny list is malformed, a token drop alone means
the model name is.

Sum the three token fields rather than reading `input_tokens`. Arms share a
prompt prefix, so a later one reports nearly all of its context as
`cache_read_input_tokens` and looks empty if only the first field is read.

Include an arm where the candidate location *is* the working directory. It is
the positive control: without it, an all-negative result cannot be told from
a probe whose settings file was never valid. Where the working directory is
also `$HOME` -- as it is in the room -- that arm proves less than it appears
to, since `$HOME/.claude/` is a candidate location on its own account. Run a
second positive arm with the two separated.
