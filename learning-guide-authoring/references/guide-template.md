# Guide Template

The canonical structure for a from-zero guide. Adapt the section count to the
concept, but keep the shape: build up, show the breaks, elevate to production.

## Title + "what you'll learn"

One line on the outcome, not the topic. "You will be able to explain a stale
closure and read the exhaustive-deps rule" beats "React Hooks tutorial".

## Part 0 — The one mental model you need

A single, self-contained, runnable example that plants the core idea. Plain
language first, then code, then "what just happened".

## Parts 1..N — Progressive layers

Each part is one idea. The pattern, repeated:

1. **Idea** — one plain sentence, an analogy only if it survives contact.
2. **Code** — runnable, minimal, no framework needed unless it is the concept.
3. **What just happened** — restate the mechanism in one sentence.

Order matters. The classic progression for a state/function concept:

```
what a closure is
→ function identity (=== is object identity, not behaviour)
→ why the framework re-creates things (re-render = new scope)
→ the memo/cache primitive (useCallback / memo)
→ the stale case (new scope + old reference)
→ the rule that catches it (lint / compiler)
→ the real fix in a real codebase
```

## Edge cases section

Explicit, not buried. For each: **wrong result → why it's wrong → fix**.
The reader must see the bug before the fix. See `edge-case-playbook.md`.

## Enterprise section

The concept placed in production. System design, architecture, failure modes,
scaling, observability, security, and the tradeoffs as decisions. See
`enterprise-elevation.md`.

## Experiments to run yourself

Numbered, ordered, each with expected output. Build on the earlier layers.

## Cheat sheet + 10-second summary

A table of one-liners, then a single paragraph that compresses the whole guide.

---

## Style rules

- Second person, imperative where it fits.
- One idea per paragraph. Blank line between ideas.
- Code blocks are copy-paste runnable. No ellipses (`...`) hiding required parts.
- Plain JS/Python for the idea; framework syntax only when the framework IS the idea.
- Show the actual output as a comment or after the block, and only the output you ran.
- A `>` blockquote for the one idea the reader must retain from a section.
