--- # workaround: anthropics/claude-code#13003
git-caution: personal
requires:
    - Skill(llm-kb)
depends:
    - Skill(llm-design-kb)
    - Skill(llm-subtask)
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
- `testing.kb/` -- procedures that check the room and re-establish the claims
  in `background.kb/`, instead of trusting either.

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

Settings are a separate question from memory, with the opposite answer: they
load from the working directory and nowhere above it
(`background.kb/settings-load-from-the-working-directory.md`), so the root
`.claude/` is free. The site to watch is inside the room, which is why a
settings file appearing there is reported rather than ignored, and why an
empty one is committed to be diffed against.

Scaffolding and room are separate jobs, but not separate trees: a tool run
at the root walks into `home/`, which after one interactive session holds
thousands of vendored files it did not put there
(`background.kb/interactive-startup-populates-the-room.md`). Scope validators
and searches to the three `.kb/` directories, or read a result that is mostly
someone else's plugins.

## Current Work

There is no task list, deliberately. What is open here is open questions,
and they live as `> [!QUESTION]` blocks in the entry each one belongs to:

    grep -rn '\[!QUESTION\]' background.kb design.kb testing.kb

Every one of them settles as a side effect of using the room -- the tripwire
reports a settings write the first time it happens, `du` shows a repeated
download -- so none of them is worth scheduling ahead of the use that
answers it. A question that does not resolve that way is a probe, and a
probe belongs in `testing.kb/` as a procedure, not on a list as an
intention.

The standing obligation is the other direction: the room runs the machine's
Claude Code (`background.kb/the-binary-comes-from-outside-the-room.md`), so
every claim here is provisional until re-checked under the version in front
of you. That is `testing.kb/after-a-claude-code-upgrade.md`, and it is a
precondition of trusting a result, not an item to work off.
