---
description: Plan the whole task end-to-end, then execute it. Parallelize independent units and verify each.
argument-hint: [task or spec]
---
Write yourself an end-to-end plan for this, then execute the whole thing, not just
the next step, until architecture, implementation, tests, and a self-review all
meet the bar.

Task: $ARGUMENTS

This is one agent self-parallelizing with worktrees and subagents, not several
goals running at once (a session has one goal at a time).

- Break the work into independent units. Parallelize the ones that don't depend on
  each other, and isolate them so two never edit the same files at once.
- After each unit, run the real flow end-to-end to verify it before integrating,
  with real inputs and real data, not a mock.
- After integrating, run the full end-to-end flow once more and show it passing.
  Units that each passed in isolation can still break once merged, and that
  combined run is the one that matters.
- Keep a short running log of what's done, what passed, and what's still open.
- Surface blocking decisions to me; otherwise keep going to completion. (That pause
  for decisions makes this interactive rather than fully unattended.)

In Claude Code, give true-parallel units their own git worktrees so they don't
collide. Stop and report if a unit can't reach green after a few attempts.
