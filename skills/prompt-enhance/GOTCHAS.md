# Gotchas

## Over-enhancing

Inventing context, constraints or output formats beyond the original intent makes results worse, not better.
Do not add what the original did not have. When unsure, the default is not to enhance.

The most common form is **made-up facts that look specific**. Turning "hmm, why is this doing that?" into
"analyze the error log at line 42 of the open file" looks convincing, but if you never checked the line number
or the tech stack, it sends the agent to analyze the wrong place. Facts in the enhanced prompt must come from the
request or from something you checked this turn. Turn the rest into an exploration step or an `(assumption)`
(SKILL.md, Principle 2).

## Distorting intent

When enhancing "do this", guessing the wrong target for "this" runs an entirely different task.
If the target is unclear, ask instead of enhancing.

## Skipping confirmation, and over-confirming

Running without showing the enhanced prompt breaks the core of this skill.
Even when the user says "just do it", show at least a one-line summary.

The non-blocking path is where this slips most. The agent decides not to wait, then goes straight to its
first tool call and never prints the enhanced prompt, so the user cannot tell what ran. Print it before the
first tool call, every time.

On the other hand, waiting for confirmation on every read-only question doubles the round trips.
Showing is not the same as waiting. Wait only for write actions, `(assumption)` items, or more than one reading.

## Enhancing an approval reply

Approval or continuation replies such as "go ahead", "yes" or "next" are not prompts to enhance.
Enhancing one breaks the flow in progress and adds another checkpoint. Just carry on.
