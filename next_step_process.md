# Development Process

This file defines the repeating cycle for advancing the quantxiv project.
Follow these steps in order, every development session.

> **All code written during this process must comply with `coding_guidelines.md`. Read it before executing any step.**
> **Also read `hints.md` for project-specific context and decisions before planning the next step.**

---

## Step 1 — Read the Goal
Read `GOAL.md` in full. This is the north star. Every action taken must move toward it.

## Step 2 — Review the Log
Read `log.md`. Understand what has already been done, what decisions were made, and what was last in progress. If `log.md` does not exist, treat the project as freshly started.

## Step 3 — Draft the Next Step
Determine the single most valuable, granular next action to advance the goal. Criteria:
- It must be concrete and executable (not vague like "improve UX")
- It must be small enough to complete in one session
- It must build directly on what was previously done
- Prefer foundational work early (infra, data model, core flows) over polish

## Step 4 — Write `next_step.md`
Overwrite `next_step.md` with the chosen next step. Format:

```
# Next Step

## What
[One sentence describing the task]

## Why
[One sentence on how this advances the goal]

## Steps
1. ...
2. ...
3. ...
```

## Step 5 — Execute
Carry out the task described in `next_step.md`. Write code, create files, configure services — whatever is needed. Do not move on until the step is complete and working.

## Step 6 — Update `log.md`
Append a new entry to `log.md` (create it if it doesn't exist). Format:

```
## [Short title] — YYYY-MM-DD, HH-MM
- What was done
- Any decisions made and why
- Anything left incomplete or deferred
```

## Step 7 — Update `current_project_status.md`
Overwrite `current_project_status.md` with the current state of the project. Rules:
- Must not exceed 3 pages (~150 lines)
- Cover: what exists, what works, what is missing, what comes next
- Write it so a new developer (or Claude in a new session) can get fully oriented in under 2 minutes

## Step 8 — Commit and Push
Stage all changed and new files. Write a clear, descriptive commit message summarizing what was done. Push to the `main` branch on GitHub.

```
git add <files>
git commit -m "<short description of what was built/changed>"
git push origin main
```

---

> Repeat from Step 1 each new session.
