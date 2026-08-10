# Todo

- [ ] Probe whether a root `.claude/settings.json` reaches a session in `home/`
  - `claudeMdExcludes` governs memory files and says nothing about settings,
    so the repo root may be a settings injection site the way it was a memory
    one; `CLAUDE.md` currently limits the root `.claude/` to `todo.md` on
    that suspicion alone
  - `testing.kb/measure-what-a-setting-suppresses.md` adapts: put a setting
    with an observable effect in a parent `.claude/settings.json` and see
    whether the room's session shows it
  - On a pass, it becomes a `background.kb/` entry and the room needs a
    defense; on a fail, `CLAUDE.md` loses a caveat
