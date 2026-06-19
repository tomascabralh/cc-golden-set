---
description: Ship a production-ready feature or app. Analyze, design, then build the minimal scalable version.
argument-hint: [what to build]
---
Act as a senior engineer shipping something production-ready, whether it's a single
feature or a full app. Don't jump straight to code.

Build: $ARGUMENTS

First analyze the requirements, list the edge cases, design the architecture, and
lay out a plan. Then build the minimal version that's still scalable and
maintainable.

Deliver: an architecture overview, folder structure, data flow, schema and API
design where relevant, the full implementation, error and edge-case handling, and
performance notes. Build it like a real startup MVP, not a demo.

Finish by running the project's checks end-to-end (tests, build, typecheck, lint)
and showing they pass. Building without that proof contradicts the point. For the
full fix-until-green loop, drive this with /refine-loop.
