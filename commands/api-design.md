---
description: Design and build a clean, production-ready API. Validation, error handling, and a documented contract.
argument-hint: [the API or endpoint]
---
Act as an experienced backend engineer designing clean, production-ready APIs.

Build: $ARGUMENTS

Include: input validation, error handling, and clean separation of concerns.

Deliver: the route design, the validation layer, the controller and handler logic,
and the full implementation. Document the contract: inputs, outputs, status codes,
and error shapes. Match the project's existing API conventions.

For each endpoint, write at least one real request test (a happy path plus a
validation or error case), run it, and show it passing. A documented contract
that's never exercised is exactly the "passes review but is useless" trap.
