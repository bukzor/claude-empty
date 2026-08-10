---
version: 2.1.226
established-by: [probe]
---

# Settings load from the working directory only

Claude Code reads project settings from `.claude/settings.json` in the
session's own working directory, and from nowhere above it -- not the parent,
not the enclosing git root. Two lookups share the `.claude/` directory name
and follow opposite rules: memory walks the whole ancestry
(`memory-lookup-walks-past-home.md`), settings do not walk at all.

## Evidence

Via `../testing.kb/find-where-a-settings-file-is-read-from.md`. One settings
file -- `"model": "haiku"` plus twelve tool denials -- moved between five
locations, against a room whose own settings select a different model:

| `.claude/settings.json` at             | loaded |
| -------------------------------------- | ------ |
| nowhere (control)                       | --     |
| the enclosing git root, above `$HOME`   | no     |
| one directory above the cwd, inside `$HOME` | no |
| the cwd                                 | yes    |
| the cwd, which was also `$HOME`         | yes    |

A loaded arm ran haiku on 3.2k tokens of context; an ignored arm ran the
room's own model on 8.0k, against the control's 8.1k.

## Consequence

The repo root is not a settings injection site the way it is a memory-file
one, so the root `.claude/` is free to hold whatever this repo needs.

The room's own root is the injection site, and it is the one place a
contaminant would be invisible: `home/.gitignore` denies by default, so a
`settings.json` appearing there is ignored rather than reported, and it would
shape every later session in the room.

> [!QUESTION] does granting a permission "always" write into the room?
> Claude Code records such a grant in a `.claude/settings.local.json`. If it
> writes it beside the working directory, one keystroke inside the room
> contaminates every session after it. Settled by granting one and looking,
> which needs an interactive session rather than `claude -p`.
