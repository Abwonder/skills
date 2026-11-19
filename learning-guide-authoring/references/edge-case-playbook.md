# Edge-Case Playbook

A beginner guide is easy. The value is teaching where the naive model breaks.
Hunt these deliberately, then teach each break as **wrong result → why → fix**.

## How to find edge cases

For any concept, ask these four questions:

1. **What is the empty case?** Zero items, null, undefined, empty string, no input.
2. **What is the boundary case?** First/last, one off, exactly-at-limit, overflow.
3. **What is the identity/aliasing case?** Two things that look equal but are not,
   or one thing referenced twice.
4. **What is the lifecycle case?** What happens before init, after teardown, on
   concurrent/async completion, on retry?

## The trap that breaks most tutorials

**"Capture by value vs capture by reference" is usually taught wrong.**

The precise rule: a closure captures the **variable (binding)**, not a snapshot of
its value. Therefore:

- **Mutate the SAME binding** → the closure sees the new value. NOT stale.
- **Create a NEW binding in a NEW scope** (e.g. React re-render) while the old
  function still points at the old scope → the closure is STALE.

Most tutorials demonstrate the stale closure by mutating a `let` in place, which
actually prints the *updated* value — and the author never runs it to notice. This
is exactly the error to avoid. The correct stale-closure demo uses two scopes:

```js
let cachedFn = null;
function render1() { const name = "Alice"; cachedFn = () => console.log(name); }
function render2() { const name = "Bob"; }   // new scope, new binding
render1(); render2();
cachedFn(); // "Alice"  <-- stale: still points at render1's binding
```

Always model state as "new scope per update", not "mutate in place", when the
concept involves re-render / memo / snapshot semantics.

## Cross-cutting edge cases worth probing

- **Off-by-one** in loops, slices, pagination, timeouts.
- **Floating point** surprises (`0.1 + 0.2`), `NaN`, `Infinity`.
- **Truthiness** (`0`, `""`, `null`, `undefined`, `NaN`, `[]`) in conditions.
- **Reference vs value equality** (`===`, `Object.is`, deep vs shallow).
- **Async ordering** — race, out-of-order completion, unhandled rejection.
- **Resource cleanup** — leaks, double-free, teardown order.
- **Case/encoding** — whitespace, unicode, locale, case sensitivity.
- **Empty/absent** — null vs undefined vs missing key vs empty collection.

## Discipline for each edge case you teach

1. Run the buggy snippet, capture the real (wrong) output.
2. State why it is wrong, in one sentence, naming the mechanism.
3. Show the fix, run it, capture the corrected output.
4. Generalise: "this is an instance of X", so the reader transfers it.

If you cannot reproduce an edge case, do not assert it. Drop it or mark it
"not reproduced".
