---
version: 2.1.226
established-by: [probe]
---

# Claude Code rewrites settings.json in place

An interactive session re-serializes `$CLAUDE_CONFIG_DIR/settings.json` into
its own canonical key order. Nothing is added, removed, or changed in value,
but the bytes are, so a version-controlled settings file comes back modified.

## Evidence

The room's `settings.json` was committed in hand-written order. After a
session that only logged in and exchanged one message, `theme` and
`claudeMdExcludes` had moved to the end and two `disable*` keys had
transposed. `jq -S` output was byte-identical before and after, which is what
rules out a settings change hiding inside a reformat.

## Consequence

The room's defining file is the tool's to format. Committing the order the
tool emits makes the rewrite a no-op; committing a hand-tidied order makes
every interactive session dirty the tree, and trains a reader to wave off
modifications to the one file whose modification would matter most.
