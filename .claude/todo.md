# Todo

- [ ] Run one interactive session in the room and record what it writes
  - The ignore rules now name only exhaust that has actually been observed,
    and every session so far has been `claude -p`; an interactive one will
    write names nobody has seen yet
  - Each new name goes into `home/.gitignore` with a note saying what
    produced it -- that is the discovery being recorded
  - It also settles the open `> [!QUESTION]` in
    `background.kb/settings-load-from-the-working-directory.md` for free:
    grant one permission "always" and see whether
    `home/.claude/settings.local.json` comes back modified
