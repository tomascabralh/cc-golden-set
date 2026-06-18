---
description: Chase a bug to its root cause like a senior engineer. Explain it, fix it properly, and prevent the class.
argument-hint: [the bug or symptom]
---
Act as a senior engineer chasing a bug. Read the relevant code carefully and reason
step by step to the root cause; don't patch symptoms. Account for edge cases and
performance.

Bug: $ARGUMENTS

First reproduce the bug reliably. If you can't reproduce it, say so rather than
guessing at a fix, since a fix for an unreproduced bug can't be verified.

Your answer covers three things:
1. The root cause, and why it happens.
2. A solid fix, with the actual code.
3. How to prevent this class of bug from recurring: a test, a guardrail, or a
   structural change.

Capture the reproduction as a failing test first, then make it pass.
