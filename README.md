# prove-it

**A Claude Code skill that stops "this should fix it".**

AI coding assistants love to guess at a bug, change something, and announce it's fixed. `prove-it` enforces the loop a senior engineer uses:

1. **Reproduce**: a failing test or script, with its real output, before any code is touched.
2. **Find the cause**: a one-sentence hypothesis, confirmed with evidence (logs, debugger, bisect), not by changing code until the symptom goes away. After 3 failed hypotheses, it steps back and re-reads everything.
3. **Fix the cause**: the smallest change. It never swallows the error, special-cases the failing input, or weakens the test.
4. **Prove it**: the *same* reproduction now passes, and the surrounding tests still pass. The output is shown.
5. **Report**: the bug, the reproduction, the cause, the fix, the proof, and what wasn't verified.

"Should work now", "try it now" and "fixed" are banned unless the proof is shown above them.

## Install

```
/plugin marketplace add sacha-riccardo-leone/prove-it
/plugin install prove-it@prove-it
```

Or copy `skills/prove-it/` into `~/.claude/skills/`.

## Use

```
/prove-it the export button downloads an empty CSV
```

It also triggers when you report a bug, an error, a crash, a failing test, or say *"it's still broken"*.

If it can't reproduce the bug, it says so. It adds logging and tells you exactly what to run, instead of fixing blind.

## License

MIT
