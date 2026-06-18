# cc-loops-goals-prompts

A small, opinionated set of **golden prompts and slash commands for Claude Code**,
built around one idea:

> **Give the agent an explicit, verifiable finish line, and make it verify the
> real thing every round.**

Most "prompt packs" are 100-entry grab-bags. This is the opposite: a tight toolkit
for the full arc of real work (orient, spec, build, loop-to-green, review, ship),
with each prompt mapped to how Claude Code actually runs (`/goal`, `/loop`, and
your `CLAUDE.md`).

## Why these are different

- **Verifiable, not hopeful.** Every "done" is a mechanical, visible check (tests
  exit 0, typecheck clean) and good against a reference, not "this should work."
- **Verify the real thing.** Real inputs, real data, the actual flow, never a mock
  standing in for the truth.
- **Mapped to the primitives.** The loop prompts are written to drive `/goal` and
  `/loop`, not just to be read.

## The two primitives (and one more)

Claude Code gives you two built-in ways to keep an agent working, plus your
`CLAUDE.md` for always-on behavior:

| Use | What it does | Reach for |
|---|---|---|
| `/goal <condition>` | Runs turns back-to-back; a fast evaluator reads the transcript after each turn and stops when your condition is met. Needs Claude Code v2.1.139+. | Driving one task to a finish line. |
| `/loop <interval\|cron> <prompt>` | Re-runs a prompt on a clock (`5m`, `--cron ...`), or self-paced if you omit the interval. Session-scoped. | Recurring checks: CI, deploys, audits, watching a long job. |
| `CLAUDE.md` | Standing instructions applied to every turn, no command needed. | Making the verify-loop discipline always-on. |

> **Tip:** the `/goal` evaluator only reads the transcript. It does not run commands
> or open files itself, so a check only counts if its output (exit code, error
> count) actually lands in the transcript. Keep the condition short, mechanical, and
> provable from Claude's own output (for example, "`npm test` exits 0, `tsc
> --noEmit` is clean, and the UI matches the design"), and keep the long spec in
> `CLAUDE.md` as background. To cap a run, put the limit in the condition itself
> ("...or stop after 15 turns"); a cap written in the prompt body is only advisory,
> because the model has to count its own turns.

> **One goal per session.** Only one `/goal` runs at a time. `/parallel-goal` below
> is a single agent self-parallelizing with worktrees and subagents, not several
> goals stacked together.

## Install

These are standard Claude Code slash commands. Copy them wherever Claude Code looks
for commands:

```bash
# global, available in every project
cp commands/*.md ~/.claude/commands/

# or per-project, checked in with the repo
mkdir -p .claude/commands && cp commands/*.md .claude/commands/
```

Then in Claude Code, type `/` and they show up. Pass the task inline, like
`/goal-loop migrate the auth module to the new API` or
`/senior-debug uploads hang above 5MB`.

For the always-on discipline, paste `claude-md/default-goal-loop.md` into your
project's `CLAUDE.md` (or `~/.claude/CLAUDE.md`). It carries the universal
guardrails (baseline before changing anything, never weaken a check to pass, name
your bar when the goal is vague) so every command inherits them.

## The commands

### Loops & goals
| Command | What it does |
|---|---|
| `/goal-loop` | Drive a task to a verified finish line: implement, run the real check, fix, repeat until green. |
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
- **Autonomous** (safe to leave running): `/goal-loop`, `/parallel-goal`,
  `/maker-checker`, `/watch`.

`/goal-loop` straddles both: its "stop and ask before a different approach" line is
right for interactive use but pauses an overnight run, so drop that line when you
need it fully hands-off.

## A typical flow

```
/spec-from-idea  ->  /map-codebase  ->  /goal-loop  ->  /fresh-eyes-review  ->  /ship-pr
```

Use `/tdd` for individual units, and keep `/watch` running on a `/loop` to hold CI
green while you work.

## License

MIT licensed. See [LICENSE](LICENSE).
