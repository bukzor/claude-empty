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
plugins.

The `.envrc` lives in `home/`, not at the repo root, so the redirect applies only
inside the room. Work on the repo itself -- editing this README, committing,
pushing -- keeps your real `$HOME` and your real `~/.gitconfig`.

## The room starts logged out

A fresh `CLAUDE_CONFIG_DIR` holds no credentials, so the first `claude` exits
with `Not logged in - Please run /login`. Either log in from inside the room, or
lend it the token you already have:

    ln -s ~/.claude/.credentials.json home/.config/claude/.credentials.json

A token refresh can replace that symlink with a real file. Re-link it if you
would rather not keep a second copy of the secret on disk.

## claudeMdExcludes is `**`

Claude Code finds memory files by walking up from the working directory, and it
does not stop at `$HOME`: a `CLAUDE.md` in this repo's root, one level above
`home/`, loads into the room. Verified -- a marker file there came back in a
`claude -p` reply, and went away once the exclude was set.

So the setting excludes everything, everywhere. Nothing is scoped to a path or a
directory name, so nothing breaks when the repo is cloned elsewhere or renamed,
and `.claude/rules/` is covered by the same pattern. That leaves the repo root
free for this README, the knowledge bases below, and a LICENSE. (A
managed-policy CLAUDE.md under `/etc/claude-code/` cannot be excluded by this or
any other setting; there is none on this machine.)

Drop the line if an experiment needs a real project's CLAUDE.md.

## What's tracked, and what git will tell you

`home/` tracks four files: `.envrc`, `.gitignore`, the settings that define
the room, and an empty `.claude/settings.local.json` that exists to be diffed
if anything ever writes settings into the room.

`home/.gitignore` names the state a session is known to leave -- transcripts,
session state, the credential file -- and ignores nothing else. Anything a
session leaves at a path this repo has not seen before therefore shows up in
`git status` as untracked, which is the alarm rather than a defect. That is
where most of the list came from: the room's first interactive session
reported nine paths at once -- its own copy of the binary, the plugin
marketplace, a verbatim prompt history -- none of which any amount of
`claude -p` had produced. Adding them is how the repo records what the tool
actually writes, so expect to add more.

## Reset the room

    git clean -nxd home/   # preview first; read it
    git clean -xd home/

The `-x` is what makes it complete, since the state you want gone is exactly
the state that is ignored. Tracked files survive, which is the definition of
the room. The credential file goes with everything else, so re-link it
afterwards.

After interactive use the room is about 66M, nearly all of it a half-finished
attempt to install a second copy of Claude Code, plus the plugin marketplace
it cloned. Throwing that away costs nothing: the room runs the binary on your
`PATH`, not the one it downloaded.

## Where the reasoning lives

Three knowledge bases at the root, for whoever next has to change `home/`:
`background.kb/` for how Claude Code behaves, `design.kb/` for what this repo
decided about it, `testing.kb/` for how to re-establish either. Every
behavioral claim names the version it held under, because the program changes
weekly and a contaminated room looks exactly like an empty one.

## Consequences

Redirecting `HOME` empties out every other tool too: inside the room `git` has no
`~/.gitconfig` (no identity, no aliases) and `gh` has no auth. That is the intent,
not a bug. Drop the dotfiles an experiment needs into `home/` and let the ignore
rules swallow them.

The one thing the room does not supply is Claude Code itself. `PATH` is
untouched, and `~/.local/bin/claude` is an absolute symlink into your real
`$HOME`, so upgrading Claude Code anywhere on the machine changes what the
room runs, invisibly. Re-check anything you concluded here after an upgrade.
