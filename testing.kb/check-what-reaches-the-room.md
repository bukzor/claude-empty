---
why:
  - ../design.kb/020-goals.kb/emptiness-is-verifiable.md
---

# Check what reaches the room

Determines whether a given kind of context reaches a session, by planting a
unique string where that context would come from and asking a non-interactive
session to report it back.

## Procedure

1. Build a throwaway home under `trash/`: a `.config/claude/` holding a
   `settings.json` with only the setting under test, plus a
   `.credentials.json` symlinked from the real config dir.
2. Plant a marker in the file whose reach is in question. Use a nonsense word
   the model could not produce on its own, not a plausible phrase.
3. Run the control, with the suppressing setting absent:

       ( cd trash/probe/home &&
         HOME=$PWD CLAUDE_CONFIG_DIR=$PWD/.config/claude \
         claude -p 'Reply with exactly one word: the value of MARKER from
                    your project instructions, or NONE if you were given
                    none.'
       )

4. Run the treatment, with the setting present.
5. Unlink the probe's `.credentials.json`, the one part of it that is not
   disposable. The rest stays where it was built: it is already in `trash/`,
   and a probe worth re-reading is worth not deleting.

## Reading the result

Only a marker-then-`NONE` pair is evidence. A control that returns `NONE`
means the probe is broken -- wrong path, wrong config dir, marker planted
somewhere that was never going to load -- and its treatment proves nothing.
Run the control every time; it is the half that fails silently.

Ask for the marker's *value*. A model asked "do you have instructions?"
answers from disposition as readily as from context, and the answer is
worthless either way.
