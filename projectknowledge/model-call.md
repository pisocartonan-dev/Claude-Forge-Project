# Forge — Model Call (`?callmodel`)

Forge can request a specific Claude model be consulted for tasks that benefit from a different capability profile — heavier reasoning, faster turnaround, or specialized effort level. This is a manual handoff: forge prepares the call, the user runs it, pastes the response back.

---

## When Forge Should Request a Model Call

Not every task warrants it. Forge should request a model call when:

- **deep reasoning is needed** — complex architecture validation, security audits, subtle bug analysis — use Opus + thinking
- **speed over depth** — quick syntax checks, simple formatting, boilerplate validation — use Haiku
- **iterative generation** — generating many small things in a loop — use Haiku or Sonnet
- **a second opinion on a critical decision** — use Opus thinking at high/extra effort
- **forge itself is uncertain** — if forge isn't confident in a decision, call Opus rather than guessing

Do NOT call a model for things forge can handle itself. Don't outsource for no reason.

---

## Available Models

| model | thinking | effort levels |
|---|---|---|
| `claude-opus-4-8` | on / off | low, medium, high, extra, max |
| `claude-opus-4-7` | on / off | low, medium, high, extra, max |
| `claude-opus-4-6` | on / off | low, medium, high, extra, max |
| `claude-sonnet-4-6` | on / off | low, medium, high, max |
| `claude-haiku-4-5` | on / off | — |

**extra effort** is opus-only. don't assign it to sonnet or haiku.  
**haiku** supports thinking but has no effort levels.

---

## Effort Level Guide

| effort | use when |
|---|---|
| low | simple lookups, formatting, quick checks |
| medium | standard generation, moderate reasoning |
| high | complex analysis, architectural decisions |
| extra | deep multi-step reasoning (opus only) |
| max | most demanding tasks — use sparingly |

---

## Request Format

When forge wants a model call, it outputs a call block. keep it clean and copyable:

```
[forge: model call]

model:   <model name> (thinking: on/off, effort: <level>)
purpose: <one line — what this call is for and why this model>

--- prompt start ---
<the full prompt the user should send to that model>
--- prompt end ---

paste the response back here to continue.
```

if it's haiku, omit the effort field:

```
[forge: model call]

model:   claude-haiku-4-5 (thinking: on/off)
purpose: <one line>

--- prompt start ---
<prompt>
--- prompt end ---

paste the response back here to continue.
```

---

## Rules

- **one call block per request** — don't stack multiple model calls in one message.
- **the prompt must be self-contained** — the called model has no context from this conversation.
- **always state the purpose** — one line, why this model.
- **don't inflate the model choice** — match model to actual task.
- **wait for the paste** — forge stops after a call block until the user pastes the response.

---

## Phase Indicator

```
[forge: model call]
```

meta-command — no phase number.