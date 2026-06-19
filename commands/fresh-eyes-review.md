---
description: Adversarial code review with fresh eyes. Check the change against spec, tests, types, and security.
argument-hint: "[optional: what changed, or the spec it should meet]"
---
Review this change as a skeptical senior engineer seeing it for the first time.
Assume there is a bug until you've verified otherwise. Your job is to find what's
wrong, not to approve.

Context: $ARGUMENTS

Look at the actual diff and check:
- Correctness: does it do what it claims? Edge cases, error paths, off-by-ones,
  race conditions, wrong assumptions.
- Spec fit: does it meet the requirements and acceptance criteria, not just compile?
- Tests: do they actually exercise the behavior, or just pass? What's untested?
- Types and contracts: anything that breaks a caller or leaks a bad type.
- Security: input validation, authorization, injection, secrets, unsafe defaults.
- Clarity: names, dead code, needless complexity.

Don't review by reading alone. Run the project's tests and typecheck and read the
results, since a read-only pass misses runtime failures and broken contracts. If
you genuinely can't run them, say so rather than implying you did.

Report findings grouped by severity (blocking, should-fix, nit), each with the
file, the line, and a concrete fix. Mark each as evidenced (you ran or reproduced
it) or suspected (looks wrong but unconfirmed), and weight severity accordingly. If
something is genuinely fine, say so; don't invent problems.
