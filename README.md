# forge

a claude-based project incubator. give it an idea, it builds out a fully architected, scaffolded, and implementable project — opinionated by design, built around your stack.

---

## what it does

forge takes you through a strict 5-phase pipeline:

1. **discovery** — asks the right questions, outputs a project brief
2. **architecture** — stack selection, data model, api surface, system design
3. **scaffold** — generates real files, installs deps, verifies the project boots, gives you a download link
4. **roadmap** — breaks implementation into ordered phases with acceptance criteria
5. **build** — implements phase by phase with sanity checks between each

it's not a chatbot. it makes decisions, documents them, and moves forward.

---

## setup

forge runs as a claude project. you'll need a claude.ai pro account.

**1. create a new claude project**

**2. upload the system prompt**

copy the contents of `forge-system-prompt.md` into the project's system prompt field.

**3. upload knowledge files** (all optional — add what you have)

| file | what it does |
|---|---|
| `stack-preferences.md` | your preferred languages, frameworks, databases, and blacklisted tools |
| `conventions.md` | naming, file structure, git conventions, error handling patterns |
| `constraints.md` | hardware, budget, hosting, and platform limits |
| `past-architectures.md` | past projects forge can learn your design instincts from |
| `templates/` folder | your reusable config files (tsconfig, eslint, github actions, etc.) |

forge works without any of these — it'll just build generic projects. upload your own knowledge and it builds like you.

**4. start a conversation with your idea**

---

## commands

| command | what it does |
|---|---|
| `?lean` | compress the pipeline to 2 gates — for small scripts and quick tools |
| `?diff` | modification mode — for changing an existing project instead of starting fresh |
| `?back` / `?back <phase>` | rewind to an earlier phase without losing downstream work |
| `?scope` | audit for scope creep and complexity drift against the original brief |
| `?status` | dump current project state — useful after a break |
| `?learn` | scan the conversation for generalizable signals, output a `forge-learned.txt` to upload |
| `?callmodel` | request a specific claude model for tasks that need heavier reasoning or speed |
| `?setupFORGE` | show the full knowledge setup guide |

---

## knowledge files

detailed guide for each knowledge file is in `forge-explain-prompt.md`, or run `?setupFORGE` in your forge project.

---

## self-learning

run `?learn` at the end of a session. forge scans the conversation for corrections, new preferences, and anything that should become a default — and generates a `forge-learned.txt` file you can upload to your project knowledge. it applies from the next session onward.

---

## notes

- forge is opinionated by design. it picks a stack and goes, rather than presenting a menu of options.
- the value is in the pipeline structure. each phase builds on the last, with explicit confirmation gates before proceeding.
- phase 3 uses claude's sandbox to write real files and verify the project actually boots — not just code blocks.
- forge ships with empty knowledge docs. you populate them, or use a separate claude instance to generate them from your existing projects.

---

## license

mit
