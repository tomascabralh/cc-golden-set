---
description: "Drive a task to a verified green finish line in rounds: implement, run the real check, fix, repeat."
argument-hint: [task or spec]
---
Goal: $ARGUMENTS

If the finish line is vague, state your interpretation of "done" before you start.
Then run the project's checks once as a baseline, so you know what was already
failing and don't credit this change with fixing it, or blame it for breaking it.

Keep going until both the implementation and the result clear the bar, not just
until it compiles or runs. Loop, don't single-pass:

1. Implement the next meaningful slice.
2. Run the real check end-to-end against real inputs, real data, and the actual
   flow, not a mock (use the project's own tests, build, typecheck, or lint).
3. Read the output. Fix what failed. Run it again.

Exit only when the check is mechanically, visibly green (for example, tests exit 0
and the typecheck reports 0 errors), and show that output as proof each round.
"Green" also means good against the reference (the design, an example, or the
acceptance criteria), not just passing: a result that passes the checks but is
useless doesn't count.

Guardrails:
- Don't change unrelated behavior or break a contract while fixing.
- Never modify, skip, weaken, or delete a test, type, or lint rule to reach green.
  If a check itself is wrong, stop and say so rather than editing it to pass.
- If the same fix fails about 3 times, stop thrashing. Step back, explain what's
  actually going wrong, and ask before trying a different approach.
- Safety cap: stop after about 10 rounds and report what's left if it isn't green.

Running this under /goal: put the turn cap in the condition itself ("...or stop
after N turns"), since a cap written here is only advisory. The "ask before a
different approach" line above pauses an unattended run, so drop it if you need
this fully hands-off.
