---
why:
  - ../010-mission.kb/unprimed-baseline-sessions.md
---

# Resettable to empty

Returning the room to its defining state is a cheap, routine operation, not
an audit of what a session left behind. A session writes transcripts, caches,
history, npm state, downloaded binaries, and credentials into the room under
names that follow the tool's version rather than this repo's expectations;
the reset must not depend on predicting them.

This is what makes the room disposable enough to contaminate on purpose. An
experiment can install anything it likes, because getting back to empty does
not require knowing what it installed.
