# claude-empty

A cleanroom for talking to Claude Code: a disposable `$HOME`, free of the
CLAUDE.md, skills, agents, hooks, and MCP servers accumulated in the real one.
Use it to see what Claude does with no priming -- baseline behavior, bug
reports, reproductions worth sharing.

## Use

    cd ~/repo/claude-empty
    direnv allow   # first time only
    claude

`.envrc` points `HOME` and `CLAUDE_CONFIG_DIR` at this directory, so Claude
reads `.config/claude/settings.json` and finds no user memory, no skills, and
no plugins. `CLAUDE.md` is deliberately empty: a marker that says don't write
one, and it keeps `/init` from filling the room back up.

`claudeMdExcludes` in the settings names the real `$HOME` paths by hand. That is
redundant while `.envrc` is loaded, and the whole point of the repo when it
isn't -- keep it.

## What's tracked

`.gitignore` denies everything, then allows back the four files above. A
session leaves transcripts, caches, npm state, credentials, and its own copy of
the `claude` binary behind; all of it stays untracked, and `git status` stays
readable.

## Consequences

Redirecting `HOME` empties out every other tool too: inside the cleanroom `git`
has no `~/.gitconfig` (no identity, no aliases) and `gh` has no auth. That is
the intent, not a bug. Drop the dotfiles an experiment needs into the repo and
ignore them.
