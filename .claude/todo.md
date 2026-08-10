# Todo

- [ ] Probe whether granting a permission "always" writes into the room
  - Settings load from the working directory, which in the room is also
    `$HOME` and is ignored by default, so a `.claude/settings.local.json`
    written there would shape every later session with `git status` clean
  - Needs an interactive session -- `claude -p` never offers the choice:
    grant one permission, then look for `home/.claude/`
  - On a pass, `background.kb/settings-load-from-the-working-directory.md`
    loses its `> [!QUESTION]`, and the room needs a defense the ignore rules
    cannot provide
