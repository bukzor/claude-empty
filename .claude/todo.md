# Todo

- [ ] Settle whether `disableBundledSkills` actually suppresses bundled skills
  - The `> [!QUESTION]` block in
    `background.kb/connectors-attach-from-the-account.md` is the only claim
    in the repo that is argued rather than observed
  - `testing.kb/check-what-reaches-the-room.md` adapts to it: ask a probe
    session to name its available skills, with the setting and without
  - On a pass, drop the callout and set `established-by: [probe]`
- [ ] Decide on a pre-commit hook running `testing.kb/ignore-coverage-check.md`
  - Guards the one expensive failure: committing the room's credential
    symlink or its exhaust
  - CI was considered and declined -- a check that fires after the push
    reports a leak already published

## Later

- [ ] Decide whether `home/CLAUDE.md` still earns its place
  - With `claudeMdExcludes: **` it would not load even if filled, so its
    only remaining job is telling a human or an `/init` run not to write one
  - Recommendation on file: keep it; zero bytes, and nothing else in the
    room states the intent
