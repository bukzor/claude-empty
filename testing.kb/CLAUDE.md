# Testing

Procedures that re-establish this repo's claims about Claude Code, so
`../background.kb/` can be re-derived on demand rather than trusted.

## What Belongs Here

- A procedure with a control and a treatment, written so it can be run
  without reading the entry that motivated it
- What a pass and a failure look like, concretely, including the failure that
  looks like a pass

## What Does NOT Belong Here

- The result of any particular run. That updates the `Evidence` section of
  the `../background.kb/` entry the procedure serves.
- Tests of a project running inside the room, as opposed to tests of the room
  itself.

## When to Add / Read

- **Add** when a claim in `../background.kb/` has no procedure behind it, or
  when checking one required reinventing a probe.
- **Read** after upgrading Claude Code, before trusting a result produced in
  the room, and before asserting any new behavioral claim.

Probes cost API calls and write real files. Build them in a throwaway
directory under `trash/`, never in `home/`, so that a failed probe cannot
leave state in the room it was meant to characterize.
