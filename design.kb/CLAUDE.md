--- # workaround: anthropics/claude-code#13003
depends:
    - Skill(llm-design-kb)
---

# Design

Why the repo is shaped the way it is: the mission, the properties that serve
it, and the mechanisms that produce those properties. Layer numbering and the
`why:` convention are defined by `Skill(llm-design-kb)`.

## What Belongs Here

- A decision this repo made, stated forward-facing as what the system *is*
- One decision per file, linked upward by `why:` to the property it serves

## What Does NOT Belong Here

- Behavior of Claude Code itself -- `../background.kb/`. An entry here cites
  the constraint; it never restates it.
- How to check that a decision still holds -- `../testing.kb/`.
- The narrative of how a decision was reached. Where a rejected alternative
  is worth remembering, the winning entry says in a line why it lost.

## When to Add / Read

- **Add** when a change to `home/` embodies a choice a future maintainer
  could reasonably make differently.
- **Read** before changing `home/`, and before answering "why not just X?"

Per-layer `CLAUDE.md` files are deliberately absent: the layers' contents are
defined by the skill, and a local guide would only restate it.
