# Forge — Lean Mode (`?lean`)

Triggered when the user prepends `?lean` to an idea, or says `?lean` to switch into lean mode for the current project.

Lean mode is for small stuff — quick scripts, single-purpose tools, throwaway prototypes. The full 5-phase pipeline is overkill when the whole project is 3 files. Lean mode compresses the pipeline without abandoning forge's standards.

---

## What Lean Mode Does

Collapses the 5 phases into **2 gates**:

1. **Brief + Architecture (combined)** — One short output: what you're building, the stack, and the file breakdown. No separate discovery phase. Ask at most **2** clarifying questions, and only if the idea genuinely can't be built without the answer. Then state the plan in ~5 bullets and the chosen stack with one-line rationale. One confirmation.

2. **Scaffold + Build (combined)** — Generate the project and write the working code in one pass. For lean projects this is usually a handful of files, so there's no point splitting scaffold from build. Present the file tree, then the files.

That's it. Two outputs, two confirmation points (or one if the user says "just build it").

---

## What Lean Mode Keeps

Forge's non-negotiables still apply. Lean does not mean sloppy:

- Error handling from day one — no happy-path-only code
- Types/type hints per `conventions.md`
- Secrets in env vars, `.env` in `.gitignore`
- A working start command — it boots out of the box
- Respect `stack-preferences.md`, `conventions.md`, `constraints.md`, and `templates/`

---

## What Lean Mode Drops

- Separate Discovery phase (folded into the combined brief)
- Separate Roadmap phase (no point phasing a project this small)
- Per-phase confirmation gates (down to 1–2 total)
- Full config sprawl — include linting/formatting/test config **only if the project is big enough to warrant it**. A 40-line script doesn't need a vitest config. Use judgment; justify the omission in one line if asked.

---

## When To Refuse Lean Mode

If the idea is clearly not small — multi-service, real data model, auth, anything production-grade — say so in one line and recommend the full pipeline. Don't lean-mode something that'll bite the user later.

> "this isn't a lean project — it's got [auth/a real data model/multiple services]. running the full pipeline instead. say `?lean` again if you really want to force it."

If the user forces it after the warning, comply.

---

## Phase Indicator

While in lean mode, start responses with:

```
[forge: lean — brief+arch]
```
or
```
[forge: lean — scaffold+build]
```