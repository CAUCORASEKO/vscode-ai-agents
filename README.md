# VS Code AI Agents

This repository shows how to turn ChatGPT into a set of
**opinionated AI agents inside VS Code**.

No plugins.
No magic.
Just structure, rules, and consistency.

---

## The problem

Most developers use ChatGPT like a chat:

- Repeating the same context
- Mixing unrelated tasks
- Getting inconsistent answers
- Losing rules over time

That does not scale.

---

## The idea: agents, not prompts

Instead of prompts, use **agents**.

An agent is:

- One chat = one role
- Fixed rules
- Fixed output format
- Project-aware context
- Opinionated by design

This is the same idea behind tools like Claude Code,
applied to **ChatGPT + VS Code**.

---

## How this works in practice

- One VS Code chat per agent
- First message = agent definition
- That chat is never reused for other tasks

Simple, boring, effective.

---

## Repository structure

- - `agents/` → React performance, code review, architecture agents
- `docs/` → How to use and how to design agents
- `examples/` → Real examples of agent output

---

## Who this is for

- Developers using ChatGPT inside VS Code
- People who want consistency, not clever prompts
- Anyone curious about agent-based workflows