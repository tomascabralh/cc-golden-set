# cc-golden-set

A golden set of Claude Code commands for driving coding work to a verified, green
finish line: pick a target, work it in rounds, verify the real thing each round,
and stop only at mechanical green.

> **The idea.** Most work with an agent ends at "this should work." This set ends
> at proof: the test exits 0, the typecheck is clean, the real flow runs. You pick a
> finish line a command can settle, then loop until it is green.

It ships as slash commands for the whole arc of real work (orient, spec, build,
loop-to-green, review, ship), plus a `verify-loop` skill that keeps the
verify-every-round habit on. `/refine-loop` is the headline: it drives one task to
a verified finish line.

## Why a plugin

Everything is mapped to how Claude Code actually runs:

| Primitive | What it does | In this set |
|---|---|---|
| `/goal <condition>` | Runs turns back-to-back; a fast evaluator reads the transcript after each turn and stops when your condition holds. Needs Claude Code v2.1.139+. | `/refine-loop` is written to be driven this way. |
| `/loop <interval\|cron> <prompt>` | Re-runs a prompt on a clock, or self-paced if you omit the interval. | `/watch` is built for it. |
| A skill | Auto-loads instructions when the task matches its description. | `verify-loop` carries the verify-loop habit. |

> **Tip:** the `/goal` evaluator only reads the transcript. It can't run commands or
> open files, so a check only counts if its output (exit code, error count) lands in
> the transcript. Keep the condition short and mechanical, and put the cap in the
> condition itself ("...or stop after 20 turns"); a cap in the prompt body is only
> advisory.

## Install

```text
/plugin marketplace add tomascabralh/cc-golden-set
/plugin install cc-golden-set@cc-golden-set
```

Then type `/` and the commands show up. Pass the task inline, like
`/refine-loop migrate the auth module to the new API` or
`/senior-debug uploads hang above 5MB`.

Manual fallback (no marketplace): copy the commands, and optionally the skill, into
where Claude Code looks for them.

```bash
cp commands/*.md ~/.claude/commands/                          # commands, global
cp -r skills/verify-loop ~/.claude/skills/verify-loop         # skill, global
```

## Always-on discipline (optional)

The `verify-loop` skill loads when its description matches the task, which is most
coding work but not literally every turn. A plugin can't ship an always-on
`CLAUDE.md` (Claude Code ignores a plugin's `CLAUDE.md`), so if you want the
verify-loop habit on unconditionally, paste this into your own `CLAUDE.md` (project
or `~/.claude/CLAUDE.md`):

```text
## Default working loop

For any non-trivial task, work in a loop toward a verifiable finish line. Don't
stop at "it compiles" or "this should work":

- If the finish line is vague, state your interpretation of "done" before you start.
- Baseline first: run the project's checks once before changing anything, so
  pre-existing failures aren't misattributed or "fixed."
- After each meaningful change, run the real check end-to-end (the project's own
  tests, build, typecheck, or lint) against real inputs, not a mock. Show the output.
- Exit only when the check is mechanically green and good against the reference
  (spec, design, acceptance criteria), not just passing.
- Never modify, skip, weaken, or delete a check to reach green. If a check is itself
  wrong, stop and say so.
- If the same fix fails about 3 times, stop and explain what's wrong before trying
  another approach.
```

## The commands

### Loops & goals
| Command | What it does |
|---|---|
| `/refine-loop` | Drive a task to a verified finish line: implement, run the real check, fix, repeat until green. |
| `/parallel-goal` | Plan end-to-end, then execute: parallelize independent units and verify each before integrating. |
| `/maker-checker` | One pass writes, a separate fresh-eyes pass reviews, and only what passes gets integrated. |
| `/watch` | Recurring watch: re-check a real status each cycle and act only on what changed. Pair with `/loop`. |

### Orient & spec
| Command | What it does |
|---|---|
| `/spec-from-idea` | Turn a vague idea into a crisp spec with verifiable acceptance criteria. |
| `/map-codebase` | Read-only map of an unfamiliar codebase (architecture, data flow, risks) before changing anything. |

### Build (test-first)
| Command | What it does |
|---|---|
| `/tdd` | Write the failing test first, then implement just enough to make it pass. |
| `/production-build` | Ship production-ready work: analyze, design, then build the minimal scalable version. |
| `/ui-components` | Reusable, accessible UI components, with every state covered and nothing hardcoded. |
| `/api-design` | Clean, production-ready APIs: validation, error handling, and a documented contract. |

### Fix & improve
| Command | What it does |
|---|---|
| `/senior-debug` | Chase a bug to its root cause: explain it, fix it properly, and prevent the class. |
| `/inherit-refactor` | Map an unfamiliar codebase, then refactor incrementally without breaking behavior. |
| `/perf-optimize` | Optimize for speed, memory, and scalability. Measure where the cost is before changing anything. |

### Review & ship
| Command | What it does |
|---|---|
| `/fresh-eyes-review` | Adversarial review against spec, tests, types, and security. |
| `/ship-pr` | Finalize into a clean PR: tidy the diff, run checks, write the commit message and PR body. |

## Interactive vs autonomous

Some commands ask questions or surface decisions mid-run. That's what you want when
you're driving, but it pauses an unattended `/goal` loop:

- **Interactive** (expect to answer questions): `/spec-from-idea`, `/map-codebase`,
  `/fresh-eyes-review`, `/ship-pr`.
- **Autonomous** (safe to leave running): `/refine-loop`, `/parallel-goal`,
  `/maker-checker`, `/watch`.

`/refine-loop` straddles both: its "stop and ask before a different approach" line
is right for interactive use but pauses an overnight run, so drop that line when you
need it fully hands-off.

## A typical flow

```
/spec-from-idea  ->  /map-codebase  ->  /refine-loop  ->  /fresh-eyes-review  ->  /ship-pr
```

Use `/tdd` for individual units, and keep `/watch` running on a `/loop` to hold CI
green while you work.

## License

MIT licensed. See [LICENSE](LICENSE).
