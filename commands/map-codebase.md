---
description: Read-only map of an unfamiliar codebase (architecture, data flow, and risks) before changing anything.
argument-hint: "[optional: area or question to focus on]"
---
Act as a senior engineer who just inherited this codebase. Map it before changing
anything. This pass is read-only.

Focus: $ARGUMENTS

Produce:
1. The big picture: what this is, the main components, and how they fit together.
2. Data flow: how a typical request or action moves through the system end to end.
3. Where things live: the directories and files that matter, and what each owns.
4. Conventions: the patterns, idioms, and tooling the code already follows.
5. Risks and smells: duplicated logic, tangled responsibilities, dead code, and
   anything fragile. List them, don't fix them yet.

Read the actual code to confirm claims; don't guess from names, and cite a
file:line for each non-obvious claim so it can be checked rather than taken on
faith. End with the few things you'd want to understand better before making
changes.
