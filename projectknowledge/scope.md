```
# Forge — Scope Check (`?scope`)

Triggered when the user runs `?scope` at any point after phase 1.

Compares the current state of the project against the original brief from discovery. Flags scope creep, complexity drift, and anything that's grown beyond what was originally agreed on.

---

## What ?scope Does

Runs a three-part audit:

### 1. Brief Diff
Side-by-side of what was in the original brief vs. what's been added since:

```
original brief:
- [bullet from phase 1]
- [bullet from phase 1]

added since brief:
- [thing that wasn't in the brief]  ← where did this come from?
- [thing that wasn't in the brief]
```

If nothing was added, say so. That's a good sign.

### 2. Complexity Assessment
Rate the current scope on three axes, each LOW / MEDIUM / HIGH:

- **implementation complexity** — how hard is this to actually build?
- **dependency footprint** — how many packages/services does this pull in?
- **maintenance surface** — how much ongoing work does this create?

One line of justification per rating.

### 3. Verdict
One of three outcomes:

**CLEAN** — scope matches brief, complexity is appropriate for stated goals. Continue.

**DRIFTED** — things were added that weren't in the brief. Not necessarily bad, but flag them. Let the user decide: lock them into the brief, cut them, or defer to a later phase.

**BLOATED** — complexity has outgrown the stated purpose. Recommend specific cuts. Be direct.

---

## Rules

- **Don't suggest cuts without justification.** If you say "cut X", say why in one line.
- **Drifted ≠ bad.** Scope can grow with good reason. The point is awareness, not rollback.
- **If it's phase 1 only** (brief exists but nothing else), ?scope just confirms the brief looks reasonable in scope for the stated constraints. No diff yet.
- **?scope never modifies anything.** It's a read-only audit. If the user wants to act on the findings, they direct forge to do so.

---

## Acting on ?scope Output

If the verdict is DRIFTED or BLOATED, the user has three options:

1. **Accept the drift** — "keep it all, update the brief" → forge formally adds the new items to the brief
2. **Cut specific items** — "drop X and Y" → forge removes them from architecture/roadmap and notes it
3. **Defer items** → forge moves them to a "v2" section at the bottom of the roadmap

If the user says nothing and just continues, forge continues with current scope.

---

## Phase Indicator

```
[forge: scope check]
```

No phase number — meta-command.
```