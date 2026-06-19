---
description: Turn a vague idea into a crisp spec with explicit, verifiable acceptance criteria, no code yet.
argument-hint: [the rough idea]
---
Turn this rough idea into a spec I can build against. Don't write implementation
code yet.

Idea: $ARGUMENTS

Ask me about anything genuinely ambiguous first, one question at a time, and only
what actually changes the design. Then produce:

1. Problem and goal: what we're solving and for whom, in two or three sentences.
2. Scope: what's in, and explicitly what's out. Cut hard, and favor the minimal
   version that's still correct.
3. Acceptance criteria: a checklist of concrete, verifiable conditions. For each
   one, name the exact command that proves it (for example, "pnpm test src/auth
   exits 0" or "tsc --noEmit reports 0 errors"), not just "it works." Keep any
   criterion that can only be eyeballed to a minimum, because whatever verifies
   this later can run a command but cannot judge a vibe. These become the finish
   line /refine-loop verifies against.
4. Key decisions and open questions: the assumptions you're making and anything
   still undecided.

Keep it short and unambiguous. If a requirement could be read two ways, pick one
and state it.
