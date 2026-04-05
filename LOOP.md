# LOOP

You are improving `{{TARGET}}` by running it, finding failures, fixing them, and making sure you don't break what already works.

---

## Setup

Before starting, read:

- `loop.yaml` — defines your target, commands, and failure modes
- `learnings.md` — what previous iterations discovered
- `suite.json` — things that must keep working (optional, created after first pass)

---

## The Loop

### 1. Run

```bash
{{RUN_COMMAND}}
```

Read the output. Note what failed.

### 2. Classify

Match each failure to a mode in `loop.yaml → failure_modes`. The mode tells you what to fix and how.

If a failure doesn't match any mode, add a new one to `learnings.md` — you just discovered something.

### 3. Fix

Apply the fix for that failure mode. One fix per iteration. Only touch `{{TARGET}}` unless the mode says otherwise.

### 4. Gate

```bash
{{GATE_COMMAND}}
```

**Pass:** go to step 5.
**Fail:** revert, try a different approach. Three strikes on the same idea = abandon it.

### 5. Record

Commit the change. Add any newly-passing cases to `suite.json`.

### 6. Learn

Check `learnings.md`. If you discovered a new pattern or failure mode, add it. If this iteration just confirmed something already there, don't — move on.

### 7. Repeat

Go to step 1. Stop after 5 iterations with no improvement.

---

## Rules

1. Only edit what `target` and `failure_modes` allow — nothing else
2. Never skip the gate
3. One fix per iteration
4. Always check `learnings.md` before fixing — don't re-solve solved problems
5. Never modify the gate, the run command, or `suite.json` by hand
