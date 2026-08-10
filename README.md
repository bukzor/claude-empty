# claude-empty

A cleanroom for talking to Claude Code: a disposable `$HOME`, free of the
CLAUDE.md, skills, agents, hooks, and MCP servers accumulated in the real one.
Use it to see what Claude does with no priming -- baseline behavior, bug
reports, reproductions worth sharing.

## Use

    cd ~/repo/claude-empty/home
    direnv allow   # first time only
    claude

`home/.envrc` points `HOME` and `CLAUDE_CONFIG_DIR` at `home/`, so Claude reads
`home/.config/claude/settings.json` and finds no user memory, no skills, and no
plugins. `home/CLAUDE.md` is deliberately empty: a marker that says don't write
one, and it keeps `/init` from filling the room back up.

The `.envrc` lives in `home/`, not at the repo root, so the redirect applies
only inside the room. Work on the repo itself -- editing this README, running
CI, committing -- keeps your real `$HOME` and your real `~/.gitconfig`.

## Keep the repo root out of the room

Claude Code finds project instructions by walking up from the working directory,
and it does not stop at `$HOME`. A `CLAUDE.md`, `CLAUDE.local.md`, or `.claude/`
at the repo root would therefore load into every cleanroom session -- the exact
pollution this repo exists to avoid. Don't add any of the three. The
`claudeMdExcludes` in the settings block them as a backstop, but that list
matches on the directory being named `claude-empty`, so it is insurance, not a
guarantee. Anything else at the root is invisible from inside `home/` and safe:
README, LICENSE, `.github/workflows/`, scripts.

## What's tracked

`home/.gitignore` denies everything under `home/`, then allows back the three
files plus the settings. A session leaves transcripts, caches, npm state,
credentials, and its own copy of the `claude` binary behind; all of it stays
untracked, and `git status` stays readable.

## Consequences

Redirecting `HOME` empties out every other tool too: inside the room `git` has
no `~/.gitconfig` (no identity, no aliases) and `gh` has no auth. That is the
intent, not a bug. Drop the dotfiles an experiment needs into `home/` and let
the ignore rules swallow them.
