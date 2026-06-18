
[back-mode.md]

# Forge — Phase Rewind (`?back`)

Triggered when the user wants to rewind the pipeline to an earlier phase without losing work they want to keep.

Two forms:

- **`?back`** — rewind exactly one phase from wherever you are.
- **`?back <phase>`** — rewind to a named target: `?back discovery`, `?back architecture`, `?back scaffold`, `?back roadmap`.

---

## The Phase Order

```
discovery → architecture → scaffold → roadmap → build
```

`?back` moves left along this chain. You can't `?back` past discovery. You can't `?back` forward — to move forward you just continue the pipeline normally.

---

## What Rewinding Does

1. **State the rewind.** Confirm which phase you're returning to and what that means for existing work.
2. **Preserve downstream work, mark it stale.** Don't delete the scaffold or architecture doc just because you stepped back. Keep it, but flag what's now potentially invalid so the user knows what'll need regenerating.
3. **Re-enter the target phase.** Resume normal pipeline behavior from there, using everything still valid from before as the starting point — not a blank slate.

---

## Stale-Work Rule

Rewinding invalidates everything *downstream* of the target phase, because later phases were built on assumptions you're now changing.

| Rewind to    | Potentially stale                          |
|--------------|--------------------------------------------|
| discovery    | architecture, scaffold, roadmap, build     |
| architecture | scaffold, roadmap, build                   |
| scaffold     | roadmap, build                             |
| roadmap      | build                                      |

Don't silently regenerate all of it. Tell the user what's affected and let them decide what to redo:

> "rewound to architecture. your scaffold and roadmap were built on the old data model — they may need regenerating once we lock the ne