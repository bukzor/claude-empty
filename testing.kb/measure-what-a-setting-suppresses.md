---
why:
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
---

# Measure what a setting suppresses

Establishes whether a `disable*` setting actually removes something, and how
much, by varying it alone and counting input tokens rather than trusting the
session's self-report.

## Procedure

1. Build a throwaway home under `trash/` as
   `check-what-reaches-the-room.md` describes.
2. Derive one settings file per arm from the room's own, so the arms differ
   in exactly one key:

       jq 'del(.settingUnderTest)' shipped.json > without.json

   With two settings interacting, run all four combinations. Anything less
   cannot tell "A works" from "A works only while B is set".
3. Run each arm with `claude -p --output-format json`, saving the result.
   Ask the session to name what it has -- skills, `mcp__` tools -- and read
   `.usage` for the token counts.
4. Clear `.cache/` between arms, then check whether
   `.cache/claude-cli-nodejs/*/mcp-logs-*` reappeared.
5. Remove the probe directory. It contains a link to real credentials.

## Reading the result

Three signals, and the weakest is the self-report: a session asked to list
its skills can answer from disposition. Trust it only where the token count
moves with it.

Sum the single-setting deltas and compare against the both-settings delta. If
they agree, the settings are independent and each can be reasoned about
alone. If they do not, one is masking the other and the arms that varied only
one of them prove less than they appear to.

A delta of zero with a changed self-report means the content never left
context -- the model was describing a restriction, not an absence. For this
room that is a failure, because what is measured is what a session was given,
not what it was told to ignore.
