---
description: Optimize code for speed, memory, and scalability. Measure where the cost is before changing anything.
argument-hint: [what to optimize]
---
Act as a performance engineer optimizing this code. Targets: speed, memory,
scalability.

Target: $ARGUMENTS

Find the bottlenecks, inefficient logic, and unnecessary recomputation or
re-renders. Reason about where the cost actually is before changing anything; don't
optimize on a hunch.

Measure first and measure after: capture a real before number, make the change,
then capture the after number and show both plus the delta. That before/after is
the proof the optimization worked, and a perf change with no numbers isn't
verifiable.

Pair the benchmark with a correctness check (the existing tests, shown passing) so
speed isn't bought by quietly changing behavior.

Return: an explanation of what was slow and why, the optimized code, the before and
after numbers, and the trade-offs you made.
