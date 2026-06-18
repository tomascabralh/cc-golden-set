---
description: Test-first. Write a failing test that pins the behavior, then implement just enough to make it pass.
argument-hint: [feature or bug to implement]
---
Build this test-first. Do not write implementation code before the test.

Target: $ARGUMENTS

1. Write a test that pins the desired behavior. For a bug, make it reproduce the
   bug. Match the project's existing test style and location.
2. Run it and watch it fail for the right reason. Confirm the failure is the one
   you expect, not a setup error, and show the failing output. If the test passes
   immediately, it isn't pinning the behavior yet, so fix the test before you write
   any implementation.
3. Implement the minimum needed to make it pass. No extra scope.
4. Run the test again and show it green. Then run the wider suite to confirm you
   broke nothing.
5. Refactor if it helps, with the test still green as your safety net.

Keep each cycle small: one behavior at a time. Never weaken or delete the test just
to make it pass.
