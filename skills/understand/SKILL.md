---
name: understand
description: "Map how the relevant code works as a flow trace, saved to docs/flows/, before changing it. Use when starting a task in unfamiliar code, or before design on a non-trivial change."
argument-hint: "<task, area, or question>"
---

# Understand

Map the path a request takes through the code before changing it. Save the map so the next task in this area starts from it.

## Process

1. Read the request and anything linked: files, errors, docs, `PROJECT.md`, project `AGENTS.md`, existing designs.
2. Look in `docs/flows/` for a flow that covers this area. If one exists, read it and run `git diff --stat <its commit> -- <its files>`. Re-trace only the steps whose files changed. Also check files added since that commit for anything new on this path, like middleware or a new route.
3. If no flow exists, trace from the trigger (user action, request, or job) to the end (database, external API, or response). Every step gets a file, line, and function.
4. Mark where the change goes and what else calls that code.
5. Write or update `docs/flows/<flow-slug>.md`.

## Flow file

```markdown
# Flow: <name>
Commit: <short hash> · Updated: <YYYY-MM-DD>

Trigger: <user action or request>
1. path/file.ts:42  functionName()  -> what it calls next
2. ...

Also used by:
- step N: <other callers>

Patterns:
- <conventions this flow follows>
```

## Boundaries

- Exact one-line change: skip this, go to **build**.
- Write only inside `docs/flows/`. One flow per file.
- Task details (where the change goes, open questions) stay in chat. The file describes the flow, not one task.

## Return

In chat: the trace, "Where the change goes: step N", "What else uses step N", open questions, and the flow file path. Ask the human to check the steps in their editor before moving on.

Blocking questions: ask first. Otherwise, open choices go to **design**, a clear fix goes to **build**, and an unknown failure goes to **debug**.
