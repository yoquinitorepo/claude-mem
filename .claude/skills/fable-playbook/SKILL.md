---
name: fable-playbook
description: A working method for non-trivial tasks - how to pin down the task, plan it, break it into verifiable steps, and check the work before reporting. Use when a task has more than one step, touches code or files you have not read yet, or when the user asks for the fable-playbook.
---

# Fable playbook

A method for doing multi-step work without fooling yourself. Follow the
sections in order. When asked which steps you are following, name them by
section number (for example "§1, §2, §4, §6").

Skip the playbook for one-line answers and trivial edits. It is for work
where being wrong costs more than being slow.

## §1 Pin down the task

Before touching anything, write down, in one or two sentences each:

- **The outcome.** What exists or is true when this is done that is not now.
- **The evidence.** What you would show someone to prove it is done: a
  passing test, a rendered page, a command's output, a diff.
- **The boundary.** What is explicitly not part of this. Adjacent problems
  you notice get reported, not fixed.

If you cannot state the evidence, you do not understand the task yet.
Resolve it from the request, the code, or a sensible default. Ask the user
only when the answer changes what you build and you cannot find it yourself.

## §2 Look before planning

A plan made from assumptions is a guess with formatting.

- Read the files you will change, and the callers of anything you will
  change the behaviour of.
- Read the project's instructions (CLAUDE.md, AGENTS.md, CONTRIBUTING,
  the docs they point to). They override your habits.
- Find how the project builds, tests and lints, and run the relevant
  check once **before** changing anything, so you know what was already
  broken.
- Find one existing example of the kind of thing you are adding and copy
  its conventions.

Stop looking when you can predict what the next file will say.

## §3 Plan

- Choose the smallest change that produces the evidence from §1.
- Name the riskiest assumption in the plan and decide how to test it first.
  If it is wrong, you want to know in minute five, not hour two.
- Weigh at most two approaches. Pick one, say why in a sentence, move on.
- Mark which actions are hard to undo or visible to other people (deleting,
  pushing, publishing, sending, migrating). Those need the user's go-ahead;
  everything else does not.

## §4 Break it into steps

Each step must:

1. Leave things in a working state.
2. Have its own check: a command to run or an observation to make.
3. Be small enough that if the check fails, the cause is obvious.

Order the steps so the riskiest assumption is tested first and so each
step builds on something already verified. Run the step's check before
starting the next. Never stack three unverified changes; when the fourth
thing breaks you will not know which one did it.

Do independent lookups in parallel. Do dependent work in sequence.

## §5 When something goes wrong

- Read the whole error. The cause is usually stated in it.
- Reproduce it before fixing it. A fix for a failure you cannot trigger is
  a hope.
- Form one hypothesis, find the cheapest observation that would disprove
  it, and make that observation. Do not change code to "see if it helps".
- Fix the cause, not the symptom. Never make a check pass by weakening,
  skipping or deleting the check.
- If the same approach has failed twice, stop and re-read §1 and §2. The
  plan is wrong, not the execution.
- If the obstacle is deliberate (a permission, a guardrail, a file marked
  off-limits), do not work around it. Say what you found.

## §6 Check your own work

Before saying it is done:

- **Run the real thing.** Tests passing is not the feature working. Execute
  the code path, open the page, call the endpoint, read the output file.
- **Re-read the full diff** as a reviewer who did not write it. Look for
  leftover debug output, unrelated edits, things you meant to come back to.
- **Re-read the original request** word by word. Check every part was
  done, including the small ones at the end of the message.
- **Re-run the baseline check from §2.** Anything red now that was green
  before is yours.
- **Try to break it.** Empty input, missing file, the second run, the
  unusual case the request mentioned.
- **Clean up** what you created along the way: temp files, background
  processes, scratch branches.

## §7 Report honestly

Lead with what the reader most needs: the result, or the decision they
have to make. Then, separately and plainly:

- **Verified:** what you checked and how (the command, the observation).
- **Not verified:** what you could not test, and why.
- **Assumed:** choices you made that the user did not specify.
- **Noticed:** problems outside the boundary that you left alone.

Never report "done" for something you did not run. "Written but untested"
is a useful sentence; a confident claim that turns out false is not. If a
check failed, say so and show the output.

## When to ask for help

If an advisor or stronger model is available, consult it at these points
rather than continuously:

- Before committing to an approach that is expensive to reverse.
- When the same approach has failed twice (§5).
- When two parts of the evidence contradict each other and you cannot see
  why.
- Before reporting, if the work is high-stakes and §6 left anything
  unverified.

Bring it the task statement from §1, what you tried, and the exact output.
A vague question gets a vague answer.
