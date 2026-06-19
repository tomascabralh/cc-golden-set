---
name: verify-loop
description: Drive any non-trivial coding task to a verifiable green finish line in rounds. Use when implementing, fixing, refactoring, optimizing, or building anything whose result can be checked by a test, build, typecheck, or lint.
---

# Verify loop

Pick a target, work it in rounds, and verify the real thing each round. Don't stop
at "it compiles" or "this should work": stop at mechanical green.

- If the finish line is vague, state your interpretation of "done" before you
  start, so success is measured against a bar you named up front, not one invented
  afterward to declare victory.
- Baseline first: run the project's checks once before changing anything, so you
  know what was already failing and don't credit this change with fixing it, or
  blame it for breaking it.
- After each meaningful change, run the real check end-to-end (the project's own
  tests, build, typecheck, or lint) against real inputs, not a mock.
- Read the output, fix what failed, and run it again. Exit only when the check is
  mechanically green, and show that output as proof (anything reviewing the work
  only sees what actually lands in the transcript, so unshown work doesn't count).
- "Done" also means good against the reference (the spec, design, or acceptance
  criteria), not just passing.
- Never modify, skip, weaken, or delete a test, type, or lint rule to reach green.
  If a check itself is wrong, stop and say so rather than editing it to pass.
- If the same fix fails about 3 times, stop and explain what's actually going wrong
  before trying another approach.
