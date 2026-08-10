--- # workaround: anthropics/claude-code#13003
git-caution: personal
requires:
    - Skill(llm-kb)
depends:
    - Skill(llm-design-kb)
---

# claude-empty

A disposable `$HOME` for Claude Code, at `home/` -- "the room" throughout
this repo. `README.md` orients a human arriving at it; this file orients an
agent maintaining it.

## Collections

- `background.kb/` -- how Claude Code and this machine behave. Constraints
  the design works around, not choices this repo made.
- `design.kb/` -- what this repo decided, and why, in the layered form
  `Skill(llm-design-kb)` defines.
- `testing.kb/` -- procedures that re-establish the claims in
  `background.kb/` instead of trusting them.

## Every behavioral claim is version-scoped

This repo's value rests entirely on claims about how a weekly-changing
program resolves memory files, credentials, and connectors. An entry
asserting such behavior belongs in `background.kb/`, whose schema forces it
to name the version it was established under and how strong the evidence is.
Where you can cite neither a probe nor a doc, mark the claim
`> [!QUESTION]` rather than asserting it: an unverified claim is worse than
an absent one here, because a contaminated room looks exactly like an empty
one.

## Two directories, two jobs

`home/` is the cleanroom; everything else is scaffolding for it. Nothing
outside `home/` may be needed at runtime by a session inside it, and nothing
inside `home/` should be committed beyond the files that define the room.

The scaffolding is invisible from inside the room only because
`claudeMdExcludes` is `**`. An agent that narrows that setting must re-check
what the root then leaks -- this file included.
