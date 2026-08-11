---
version: 2.1.227
established-by: [probe]
---

# The room runs the machine's binary, not its own

`claude` on `PATH` is `~/.local/bin/claude`, an absolute symlink into the
real `$HOME`'s `versions/` directory. `home/.envrc` redirects `HOME` and
`CLAUDE_CONFIG_DIR` and nothing else, so a session started in the room execs
the outer machine's binary by absolute path. Nothing about which binary runs
is inside the room.

The updater disagrees with the launcher about where `$HOME` is. Its install
target does follow the redirect: an interactive start downloads into
`home/.cache/claude/staging/<version>.<n>.<n>/claude` and writes a zero-byte
`home/.local/share/claude/versions/<version>`. That install is unusable even
if it completed, because the symlink that would select it --
`home/.local/bin/claude` -- is never created.

## Evidence

The outer `~/.local/share/claude/versions/` holds four binaries of 295-304 MB
each, mode 755, and `~/.local/bin/claude` points at the newest of them by
absolute path. The room's `versions/2.1.226` is 0 bytes, mode 644; its
`.local/bin/` exists and is empty; its staged copy is 61 MB and not
executable. The room's staged version equals the version the outer install
was running when the session started.

## Consequence

The room is not hermetic in the one dimension it cannot inspect. Upgrading
the machine's Claude Code changes what every session in the room runs, with
no file inside the room changing and nothing for `git status` to report --
the failure mode `../testing.kb/after-a-claude-code-upgrade.md` exists for,
now with a second cause.

So a version read "inside the room" is a fact about the machine, and
`git clean -xd home/` resets everything except the program. Pinning the room
to a version would mean putting a launcher in the room, not a setting.

> [!QUESTION] does every interactive start re-download the binary?
> The install cannot complete, so the room may pay 61 MB per start rather
> than once. Two starts and a `find home/.cache/claude/staging -maxdepth 1`
> settle it.
