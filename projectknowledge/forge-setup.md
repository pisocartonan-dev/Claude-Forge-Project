# Forge — Knowledge Setup

Forge works out of the box, but it builds *generic* projects. To make it build like *you*, upload these files as project knowledge. All optional — add what you have, skip what you don't.

---

### `stack-preferences.md`
Your default tools. List your preferred languages, frameworks, databases, and CI/CD setup. Also list tools you *don't* want — Forge will avoid them.

Key sections to cover:
- Languages (in order of preference, what each is used for)
- Frameworks per category (backend, frontend, CSS, testing)
- Database preferences and ORM stance
- Infra/hosting defaults
- Blacklisted tools and why

---

### `conventions.md`
Your code style rules. How you name things, organize files, handle errors, write commits.

Key sections to cover:
- Naming conventions (files, variables, classes, constants)
- File/folder organization pattern (feature-based vs layer-based)
- Language-specific rules (e.g. no `any` in TS, type hints in Python)
- Git conventions (commit format, branch naming, rebase vs merge)
- Error handling patterns
- Testing philosophy
- Documentation expectations

---

### `constraints.md`
Real-world limits Forge should respect.

Key sections to cover:
- Dev hardware (desktop, laptop, phone, cloud IDE)
- Budget (free tier only? API cost caps?)
- Hosting preferences
- Platform targets (web, mobile, CLI)
- Performance targets if any

---

### `past-architectures.md`
3-5 past projects that show how you think. For each one, include: what it was, the stack, what worked, what didn't, and one key lesson. Forge uses these to match your design instincts.

---

### `templates/` folder
Config files you always reuse — tsconfig, eslint, prettier, Dockerfile, CI workflows, .gitignore, etc. Upload them and Forge will use yours instead of generating generic ones.

---

Upload whatever you have, start a conversation with your idea, and Forge handles the rest.