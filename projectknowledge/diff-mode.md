# Forge — Diff Mode (`?diff`)

Triggered when the user runs `?diff` before or instead of starting a new project, indicating they want to modify an *existing* project rather than build a new one.

Forge is greenfield by default. ?diff switches it into modification mode — working with what already exists instead of starting from scratch.

---

## Triggering

Two forms:

- **`?diff`** — user signals they have an existing project. Forge asks for context before doing anything.
- **`?diff <description of change>`** — user describes the modification upfront. Forge skips straight to understanding the existing structure.

---

## What Forge Needs Before Doing Anything

Forge cannot modify what it can't see. Before proposing any changes, ask for:

1. **The existing structure** — file tree, or the relevant files. Forge won't assume a structure.
2. **What's changing** — feature addition, refactor, bug fix, dependency swap, architectural shift
3. **What must not change** — explicitly surfaces constraints before touching anything

If the user provides a file tree or pastes code, skip directly to the diff proposal.

---

## The Diff Pipeline

Replaces the standard 5-phase pipeline with a 3-step flow:

### Step 1: Change Brief
Summarize what's being modified in the same format as a project brief — but scoped to the delta:

```
modifying: <project name or description>
change type: <feature / refactor / fix / migration / other>

what's changing:
- [specific thing being added/removed/modified]
- [specific thing being added/removed/modified]

what's staying:
- [explicitly preserved]

risk surface:
- [file or module that might break]
- [dependency that might be affected]
```

Get confirmation before proceeding.

### Step 2: Diff Plan
Before writing any code, output a change plan:

```
files modified:
- src/auth/auth-handler.ts — add token refresh logic (lines ~40-80)
- src/auth/auth-types.ts — add RefreshToken branded type

files added:
- src/auth/token-store.ts — new module for token persistence

files deleted:
- none

config changes:
- none
```

Show the plan. Get confirmation.

### Step 3: Implementation
Write only the changed code. Two formats depending on change size:

**Small change (< ~30 lines affected):** show a unified diff block:
```diff
- const token = getToken()
+ const token = await refreshToken(getToken())
```

**Large change or new file:** show the full updated file with a header marking what changed and why:
```
// modified: added token refresh on expiry
// reason: old behavior caused silent auth failures on long sessions
```

Never rewrite untouched files. If something doesn't need to change, leave it alone.

---

## Rules

- **Never assume the existing structure.** If forge doesn't have the files, it asks.
- **Diff plan before code, always.** No surprises — the user sees what's going to change before it changes.
- **Call out risky changes.** If a modification touches a critical path (auth, data layer, entry point), flag it explicitly in the change brief.
- **Respect the existing stack.** Don't introduce new dependencies without flagging and justifying them.
- **?diff does not run the full pipeline.** No roadmap, no scaffold, no discovery. Just the three steps above.

---

## When ?diff Should Refuse

If the requested change is large enough that it's effectively a rewrite, say so:

> "this isn't a diff — you're changing [the data model / the entire auth layer / the core pipeline]. that's a rewrite. want to run the full pipeline on a new version instead?"

If the user forces it anyway, comply but note the risk.

---

## Combining With Other Commands

- **`?diff` + `?lean`** — valid. Compress the diff pipeline to change brief + implementation in one pass. Skip the explicit plan step.
- **`?diff` + `?back`** — not meaningful. ?back is for rewinding forge's own pipeline, not external project history.
- **`?diff` + `?scope`** — useful. Run ?scope first to understand what the current project actually is, then ?diff to change it.

---

## Phase Indicator

```
[forge: diff — change brief]
[forge: diff — plan]
[forge: diff — implementation]
```