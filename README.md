# loop

The smallest unit of a self-improving system.

```
run it → see what failed → fix one thing → make sure you didn't break what worked → remember what you learned → repeat
```

---

## The idea

Every self-improving system — no matter how complex — is doing the same four things:

1. **Generate** — try something
2. **Evaluate** — check it against something you can't fool
3. **Select** — keep what survived
4. **Accumulate** — remember what you learned

`loop` is that pattern, stripped to its minimum. Two files: `LOOP.md` tells an agent what to do. `loop.yaml` tells it what *your* project needs.

The critical constraint: the agent can only touch what `target` and `failure_modes` allow. It cannot modify the gate, the run command, or the eval suite. That's what makes improvement real instead of theater.

---

## How to use it

**1. Drop `LOOP.md` into your project** (or point your agent at this repo's copy).

**2. Create a `loop.yaml`:**

```yaml
target: agent.py
run: python benchmark.py
gate: python gate.py

failure_modes:
  - name: prompt_gap
    signal: "agent failed a task it should handle"
    fix: "add an explicit rule to the system prompt"
    edit: target
```

**3. Point a coding agent at it:**

```
Read LOOP.md and loop.yaml. Start the loop.
```

That's it. The agent runs your benchmark, classifies failures against your `failure_modes`, applies the right fix, gates the change, and logs what it learned — until scores stop improving.

---

## Why failure_modes matter

Without a classification table, the agent guesses. With one, it matches. The difference between "try random fixes" and "I know exactly what kind of problem this is and what to do about it."

The failure modes are also how domain knowledge enters the loop. The loop itself is generic. What makes it work for *your* project is the taxonomy of things that go wrong.

---

## Examples

- [`examples/cortex/`](examples/cortex/) — improving a semantic knowledge ledger's retrieval quality
- [`examples/auto-harness/`](examples/auto-harness/) — improving an agentic task harness (system prompt + tools)

---

## Philosophy

This pattern shows up everywhere under different names:

- Karpathy's autonomous research loop
- NeoSigma's [auto-harness](https://github.com/neosigmaai/auto-harness)
- RGDP's object layer
- Evolutionary algorithms
- The scientific method

They're all the same loop. The only thing that varies is what "evaluate" means — and that's the only part that matters. Make it something you can't argue with: a test suite, a slicer, a judge panel, physics. The moment evaluation becomes self-assessment, the loop breaks.

---

## What loop is not

A framework. There's no package to install, no API to learn. It's a markdown file and a yaml config. The "runtime" is whatever coding agent you already use.
