---
version: 2.1.226
established-by: [probe]
---

# An interactive start populates the room; `claude -p` does not

A first interactive session writes nine paths that no amount of
non-interactive use produces. It downloads a 61 MB copy of the binary into
`.cache/claude/staging/<version>.<n>.<n>/claude` and leaves a zero-byte file
named for that version at `.local/share/claude/versions/`. It clones
the official plugin marketplace -- some forty plugins' metadata -- into
`.config/claude/plugins/`. It records every prompt verbatim in
`.config/claude/history.jsonl`, caches the changelog and a lookup of the
account's closed issues under `.config/claude/cache/`, and registers a
`claude-code-url-handler.desktop` for the login flow. And it shells out to
`gh`, which finds no configuration of its own in the redirected home and
creates `.cache/gh/` and `.local/state/gh/`.

## Evidence

The room ran only `claude -p` for a day and accumulated six paths. One
interactive session -- log in, type "oh, hi!", read the reply -- added the
nine above. All nine were reported as untracked rather than swallowed,
because the ignore rules name only exhaust already observed
(`../design.kb/040-design.kb/ignores-name-only-known-exhaust.md`); the
inventory above is that report, not an audit anyone had to think to run.

## Consequence

A room verified with `claude -p` is not a room verified for interactive use,
and the gap is not small. Any claim about the room's contents established
non-interactively describes a strictly emptier room than the one a person
sits down in.

The marketplace clone is the sharpest instance: "no plugins" describes the
room's configuration, not its contents, from the first interactive start
onward. Nothing here establishes whether that clone can be suppressed.

The self-update is the largest of these and the only one that failed. It
accounts for 59 of the room's 66 MB and installs nothing: the room runs the
machine's binary regardless (`the-binary-comes-from-outside-the-room.md`).

Two of these matter beyond the ignore file. `history.jsonl` is a verbatim
record of what was typed into a room whose purpose is unguarded experiments.
And the `gh` state is direct evidence that the HOME redirect catches tools
this repo never enumerated, which is the intent of
`../design.kb/040-design.kb/home-redirect-scoped-to-the-room.md` rather than
a surprise -- confirmed here by one program invoking another.
