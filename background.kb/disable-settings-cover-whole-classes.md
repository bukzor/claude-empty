---
version: 2.1.226
established-by: [probe]
---

# The disable settings cover whole classes

`disableBundledSkills` and `disableClaudeAiConnectors` each suppress their
entire class, independently of one another, and remove its content from
context rather than merely blocking access. Neither needs a companion list of
names.

## Evidence

A 2x2 over the two settings, via
`../testing.kb/measure-what-a-setting-suppresses.md`:

| `disableBundledSkills` | `disableClaudeAiConnectors` | skills | connectors | input tokens |
| --- | --- | --- | --- | --- |
| -- | -- | 12 named | Drive tools | 14009 |
| yes | -- | none | Drive tools | 11967 |
| -- | yes | 12 named | none | 9925 |
| yes | yes | none | none | 7910 |

The connector rows are corroborated by the filesystem: `mcp-logs-claude-ai-*`
appeared under `.cache/claude-cli-nodejs/` in exactly the two rows that
reported connectors. The token deltas are consistent across both levels of
the other setting -- about 2.0k for the skills, 4.1k for the connectors --
and they sum to the observed 6.1k, so the two act independently.

## Consequence

Enumerating names alongside these settings buys nothing and costs
correctness: a list of three connectors or sixteen skills goes stale the week
a fourth or a seventeenth ships, and nothing looks wrong when it does. The
room names neither. See `../design.kb/040-design.kb/denied-tool-surface.md`.

The token column is also the cheapest regression test available. Content that
is truly gone from context cannot be measured by asking the model, but it
cannot hide from the input-token count either.
