<!--
Paste this into your project's CLAUDE.md (or ~/.claude/CLAUDE.md) so the
verify-the-real-thing discipline is always on, with no command needed.
-->

## Default working loop

For any non-trivial task, work in a loop toward a verifiable finish line. Don't
stop at "it compiles" or "this should work":

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
