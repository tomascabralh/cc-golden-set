---
description: Inherit an unfamiliar codebase and refactor it incrementally. Map first, then improve without breaking behavior.
argument-hint: [area to refactor or goal]
---
Act as a senior engineer who just inherited a large, unfamiliar codebase.

Goal: $ARGUMENTS

First map the architecture and data flow before changing anything (the
/map-codebase command does exactly this read-only pass if you want the full
version). Then identify: structural problems, duplicated logic, performance
bottlenecks, dead code, and risky patterns. Propose a prioritized refactor plan,
highest impact and lowest risk first, and explain the reasoning.

Then refactor incrementally: keep behavior intact and verify with tests after each
step, showing the output. No big-bang rewrite. If you don't have a test protecting
a change, write one first.
