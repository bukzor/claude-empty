# Todo

- [ ] Settle whether `disableBundledSkills` actually suppresses bundled skills
  - The `> [!QUESTION]` block in
    `background.kb/connectors-attach-from-the-account.md` is the only claim
    in the repo that is argued rather than observed
  - `testing.kb/check-what-reaches-the-room.md` adapts to it: ask a probe
    session to name its available skills, with the setting and without
  - On a pass, drop the callout and set `established-by: [probe]`
- [ ] Drop the three `mcp__claude_ai_*` denies once
      `disableClaudeAiConnectors` is probed
  - The setting was added because it is blanket where the denylist is
    enumerated -- a fourth connector would defeat the names, not the setting
  - Both are in force today, which is redundant but harmless; the denies go
    only after a probe shows the setting alone suppresses the connectors
  - Same probe as the `disableBundledSkills` item: one run can settle both
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
