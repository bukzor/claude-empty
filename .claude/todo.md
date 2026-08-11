# Todo

- [ ] Find whether the plugin-marketplace clone can be suppressed
  - A first interactive start clones the official marketplace into
    `home/.config/claude/plugins/`
    (`background.kb/interactive-startup-populates-the-room.md`), so the room
    is plugin-free by configuration but not by contents
  - Look for a setting that prevents it; if there is none, say so in that
    entry and treat the clone as exhaust rather than leaving the question open
- [ ] Re-run `testing.kb/after-a-claude-code-upgrade.md`: the outer `claude`
      is 2.1.227 and every `background.kb/` entry says 2.1.226
  - The upgrade landed the same day the claims did, so nothing here has been
    rechecked under it -- least of all the memory-file claim, which every
    result the room produces depends on
- [ ] Settle whether the room's self-update finished
  - `.cache/claude/staging/2.1.226.../claude` is 61 MB and not executable;
    `.local/share/claude/versions/2.1.226` is zero bytes
  - The `> [!QUESTION]` in
    `background.kb/interactive-startup-populates-the-room.md` holds the two
    readings; a second interactive start should distinguish them
- [ ] Settle whether a permission granted "always" writes into the room
  - The tripwire survived the first interactive session unmodified, but that
    session granted no permissions, so nothing was tested
  - `background.kb/settings-load-from-the-working-directory.md` holds the
    `> [!QUESTION]`; one granted permission answers it
