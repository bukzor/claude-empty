---
why:
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
---

# After a Claude Code upgrade

The room auto-updates its own copy of the binary, and every claim in
`../background.kb/` names the version it held under. An upgrade can therefore
invalidate this repo's central claim without changing a single tracked file,
which is the one failure mode git will not surface.

## Procedure

1. Run `smoke-test-the-room.md`, then `claude --version` inside the room, and
   compare against `grep -r version: ../background.kb/`.
2. Re-run `check-what-reaches-the-room.md` against the memory-file claim.
   That one is load-bearing: if it regresses, every result the room produced
   since the upgrade is suspect.
3. Advance the `version:` of each entry that still holds, rather than leaving
   it citing an older one. An entry whose version is stale is
   indistinguishable from one that was never rechecked.
4. Recheck the entries whose `established-by:` includes `inference` hardest.
   Nothing observed them holding under the old version either.
5. Re-run `measure-what-a-setting-suppresses.md` if the room's token count
   moved. A setting that quietly stopped working restores several thousand
   tokens of context, which is visible before any behavior is.

## Reading the result

A regression is a finding, not an obstacle to route around. It belongs in
`../background.kb/` as a described behavior, and upstream as a report.

Resist the repair that suggests itself -- adding scoped patterns until the
probe passes again. That rebuilds the fragile arrangement blanket exclusion
replaced, and it hides the regression instead of reporting it.
