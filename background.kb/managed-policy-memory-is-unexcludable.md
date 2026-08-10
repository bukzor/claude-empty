---
version: 2.1.226
established-by: [documentation]
---

# Managed-policy memory cannot be excluded

A managed-policy `CLAUDE.md` -- `/etc/claude-code/CLAUDE.md` on Linux, or a
`claudeMd` key in managed settings -- loads into every session on the machine
and is exempt from `claudeMdExcludes` by design. No user, project, or local
setting suppresses it.

## Evidence

Documented, not probed: "Managed policy CLAUDE.md files cannot be excluded.
This ensures organization-wide instructions always apply regardless of
individual settings." No probe is possible here -- `/etc/claude-code/` does
not exist on this machine, and creating one to test the claim would need
root.

## Consequence

The room's emptiness is complete on an unmanaged machine and incomplete on a
managed one, with no in-repo remedy. Check `ls /etc/claude-code/` before
trusting the room on unfamiliar hardware; if it exists, a baseline result
produced there must either quote the managed content or be produced
elsewhere.
