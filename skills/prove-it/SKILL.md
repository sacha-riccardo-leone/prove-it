---
name: prove-it
description: Debugging discipline that stops guess-and-hope fixes. No fix before the bug is reproduced with a failing test or script; no "fixed" before that same reproduction passes. Use when the user says /prove-it, reports a bug, an error, a crash, a failing test, "it doesn't work", "still broken", or when a previous fix attempt didn't hold.
---

# Prove It

The rule: **a bug is real when you can make it happen on demand, and fixed when the same command that showed it now shows it gone.** Everything else is a guess.

## 1. Reproduce (before touching any code)

- Write the smallest thing that shows the bug: a failing test in the project's test framework (preferred, it stays as a regression test), or a script / command / curl / browser step.
- Run it. Paste the **actual output** showing the failure.
- The failure must match what the user described. If it fails differently, you reproduced something else.

Can't reproduce after a real try? Stop and say so. Don't fix blind. Instead: add logging or assertions where the bug likely lives, tell the user exactly what to run or click, and ask for the output. Ask for the environment details that differ (data, browser, OS, env vars, versions).

## 2. Find the cause

- State a hypothesis in one sentence: "X happens because Y."
- Test it with evidence: a log line, a debugger value, a narrowed input, a `git bisect`. Not by changing code and seeing if the symptom goes away.
- After 3 hypotheses that failed, stop guessing. Step back: re-read the error and stack trace in full, check what changed recently (`git log -p`, dependency updates), and question the assumptions you have been treating as true.

## 3. Fix

- Fix the cause, not the symptom. No `try/catch` that swallows the error, no special case for the failing input, no retry loop around a deterministic bug, no weakening the test.
- Smallest change that fixes the cause.

## 4. Prove

- Run the **same** reproduction from step 1. Paste the passing output.
- Run the surrounding tests (the file, the module, or the whole suite if it is fast). Paste the result.
- Keep the reproduction as a regression test when it is a test.

## 5. Report

```
Bug: <one line>
Repro: <command or test name> — failed with: <key line of output>
Cause: <one or two lines, with the evidence that confirmed it>
Fix: <file:line — what changed>
Proof: same repro now passes; <n> surrounding tests pass
Not verified: <anything you couldn't check, e.g. production data, other browsers>
```

## Banned phrases

Never say "this should fix it", "try it now", "it should work" or "fixed" without the step 4 output above it. If you could not run the proof, say exactly that: "Not verified: I couldn't run X because Y."
