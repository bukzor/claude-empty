# Background

Facts about Claude Code, its configuration resolution, and this machine that
the design has to accommodate. Constraints discovered, not decisions made.

## What Belongs Here

- One observed behavior of the tool or the environment per file
- The evidence that established it: the procedure used, in prose; the version
  it held under and the strength of the evidence, in frontmatter
- The consequence for a cleanroom -- what leaks, or what stays broken, if
  the design ignores it

## What Does NOT Belong Here

- The choices this repo made in response. Those are `../design.kb/` entries,
  and they cite these files for their justification.
- Reusable verification procedures. Those are `../testing.kb/` entries; an
  entry here cites one rather than restating it.
- Anything true only of a project run inside the room, rather than of the
  room itself.

## When to Add / Read

- **Add** when a probe, an upgrade, or a surprise establishes a behavior the
  design depends on -- especially a behavior that defeats it.
- **Read** before changing anything under `home/`, and before concluding
  that the room is empty of something.

Entries carry no `why:`, since background motivates every layer and is
motivated by none. They carry `version:` and `established-by:` instead, which
make two maintenance questions greppable: what an upgrade invalidates, and
which claims were argued rather than observed. Record the version there and
nowhere else, so it cannot go stale in one place and not the other.
