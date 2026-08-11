---
why:
  - ../020-goals.kb/no-inherited-state.md
---

# The HOME redirect is scoped to the room

`home/.envrc` exports `HOME=$PWD` and
`CLAUDE_CONFIG_DIR=$PWD/.config/claude`. direnv evaluates an `.envrc` with the
working directory set to the file's own directory, so `$PWD` names the room
whether you enter through a subdirectory of it or through a symlink to it --
the redirect resolves to the physical path either way.

The file sits in `home/` rather than at the repo root so that the redirect
covers the room and nothing else. Maintaining this repo -- editing docs,
running git, pushing -- happens outside it, with the real `$HOME` and the
real `~/.gitconfig` intact. A root `.envrc` would put the maintainer inside
the room they are maintaining, where `git` has no identity.

Redirecting `HOME` empties every other tool that reads `~`, not just Claude
Code: `git` loses its config, `gh` its auth. That is intended. An experiment
that needs those configured places the dotfiles in `home/`, where the ignore
rules swallow them, rather than reaching outside for them.

The reach is wider than the tools a person runs. Claude Code shells out to
`gh`, which found no configuration in the redirected home and created its own
state there (`../../background.kb/interactive-startup-populates-the-room.md`)
-- one program pulling another into the room, without either being named
here.
