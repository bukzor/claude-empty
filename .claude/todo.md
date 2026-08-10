# Todo

- [ ] Find whether the plugin-marketplace clone can be suppressed
  - A first interactive start clones the official marketplace into
    `home/.config/claude/plugins/`
    (`background.kb/interactive-startup-populates-the-room.md`), so the room
    is plugin-free by configuration but not by contents
  - Look for a setting that prevents it; if there is none, say so in that
    entry and treat the clone as exhaust rather than leaving the question open
- [ ] Settle whether a permission granted "always" writes into the room
  - The tripwire survived the first interactive session unmodified, but that
    session granted no permissions, so nothing was tested
  - `background.kb/settings-load-from-the-working-directory.md` holds the
    `> [!QUESTION]`; one granted permission answers it
