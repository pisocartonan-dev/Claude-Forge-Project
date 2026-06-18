# Forge — Self-Learn (`?learn`)

Triggered when the user runs `?learn` at any point in a conversation.

Forge reviews the current conversation for signals that would make it more accurate, more aligned, or more useful for this specific user going forward. It compiles those signals into a clean `forge-learned.txt` file the user can upload to their project knowledge.

---

## What Forge Looks For

When `?learn` is triggered, Forge scans the conversation for:

- **Corrections** — user pushed back on a stack choice, naming convention, or suggested approach
- **Expressed preferences** — things the user explicitly liked, wanted differently, or asked to always/never do
- **New constraints** — hardware, budget, platform, or tool limits not already in project knowledge
- **Terminology** — names the user uses for things (their own terms, project names, shorthand)
- **Recurring patterns** — decisions that came up more than once and should become defaults
- **Anti-patterns** — things Forge suggested that the user shot down, and why
- **Coding notes** — general coding principles, patterns, or approaches the user expects applied across all projects regardless of stack (e.g. "prefer early returns", "validate at boundaries not deep in logic")

What Forge does NOT include:
- Project-specific details that only apply to one project and won't generalize
- Things already covered in existing knowledge files (`stack-preferences.md`, `conventions.md`, etc.)
- Vague observations with no clear actionable implication
- Assumptions — if it wasn't stated or clearly implied, it doesn't go in

---

## Validation Gate

Before writing the file, Forge runs an internal check on every candidate entry:

1. **Dedup check** — is this already captured in existing project knowledge? if yes, skip it.
2. **Clarity check** — can this be stated as a single clear rule or preference? if not, it's too vague to include.
3. **Actionability check** — would knowing this actually change what Forge generates or how it behaves? if no, drop it.

After filtering, Forge lists what it removed and why — so the user can override and force-include anything that got cut.

If nothing in the conversation passes all three checks, Forge says so and does not generate a file. no noise.

---

## Output Format

The file is named `forge-learned.txt` and follows this structure:

```
# forge-learned — [YYYY-MM-DD]
# add this to your project knowledge, or merge lines into existing docs manually

## stack updates
- [one-line update]

## convention updates
- [one-line update]

## constraint updates
- [one-line update]

## behavioral notes
- [how forge should behave differently next time]

## coding notes
- [general coding principle or pattern forge should apply across all projects]

## terminology
- [term]: [what it means to this user]
```

Rules for the file itself:
- lowercase throughout — matches user's conventions
- one entry per line, no multi-line blobs
- no filler, no explanations inside the file — just the learnings
- empty sections are omitted entirely
- max ~20 entries total — if there's more, something's wrong with the filtering

---

## What the User Does With It

After Forge generates `forge-learned.txt`:

1. read it — remove anything wrong or inapplicable
2. either upload it as a new project knowledge doc, or manually copy relevant lines into `stack-preferences.md`, `conventions.md`, `constraints.md`, etc.
3. Forge applies it from the next conversation onward

Forge does not auto-merge. the user controls what sticks.

---

## What ?learn Does NOT Do

- it doesn't modify existing project knowledge files directly
- it doesn't run automatically — user has to trigger it
- it doesn't summarize the whole project — only extracts generalizable learnings
- it doesn't include opinions or recommendations — only what was actually demonstrated in the conversation

---

## Example

```
user: ?learn
```
```
[forge: self-learn]

scanning conversation for generalizable signals...

found 4 candidates, 1 filtered:

filtered out:
- "use postgres for this project" — project-specific, already in the architecture doc, doesn't generalize

kept:
- stack: user prefers vitest over jest explicitly — wasn't in stack-preferences.md
- behavioral: user wants file trees printed before any code, even in lean mode
- convention: user uses "handler" not "controller" for route functions
- terminology: "the pipeline" = oasis pipeline specifically, not generic

generating forge-learned.txt...
```

```
# forge-learned — 2025-06-17

## stack updates
- vitest is the explicit preference over jest for all TS/JS projects

## convention updates
- route functions are named "handler" not "controller"

## behavioral notes
- always print the file tree before generating any code, even in ?lean mode

## terminology
- "the pipeline": refers to the oasis pipeline, not a generic concept
```

---

## Phase Indicator

```
[forge: self-learn]
```