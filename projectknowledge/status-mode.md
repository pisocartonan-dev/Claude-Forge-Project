# Forge — Status (`?status`)

Triggered when the user runs `?status` at any point in a conversation.

Dumps the current project state in a compact, readable summary. Built for returning to a session after a break, or just checking where things stand mid-build.

---

## What ?status Outputs

A single block with four sections — only include sections that have content:

```
[forge: status]

project: <project name or "unnamed">
phase:   <current phase name + number, or "not started">
stack:   <one-line summary of confirmed stack>

completed:
- phase 1 (discovery) — brief confirmed
- phase 2 (architecture) — stack and data model locked

in progress:
- phase 3 (scaffold) — file tree generated, configs pending

pending:
- phase 4 (roadmap)
- phase 5 (build)

last decision: <the most recent architectural or structural decision made>
next action:   <exactly what forge will do next if the user says "continue">
```

---

## Rules

- **No re-asking questions.** ?status is read-only. It doesn't prompt for confirmation or restart anything.
- **"last decision" is one line.** The most recent thing that got locked in — a stack choice, data model decision, a file that got written. Not a summary of everything.
- **"next action" must be concrete.** Not "continue the pipeline" — say exactly what comes next: "generate the package.json and tsconfig" or "write the database connection module".
- **If nothing has happened yet**, say so and remind the user what discovery needs:

  > `phase: not started — send your idea to begin`

- **If a phase was rewound** (via ?back), reflect that state accurately. Don't show rewound phases as completed.

---

## What ?status Does NOT Do

- It doesn't resume the pipeline — the user does that by continuing normally
- It doesn't re-validate decisions or check for conflicts
- It doesn't regenerate anything
- It doesn't ask questions

---

## Phase Indicator

```
[forge: status]
```

No phase number — status is a meta-command, not a pipeline phase.