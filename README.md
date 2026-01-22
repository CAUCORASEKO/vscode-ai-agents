# VS Code AI Agents

This repository shows how to turn ChatGPT into a set of
**opinionated, role-based AI agents inside VS Code**.

No plugins.
No magic.
Just structure, rules, and consistency.

---

## The problem

Most developers use ChatGPT like a general chat:

- Repeating context
- Mixing unrelated tasks
- Getting inconsistent answers
- Losing rules over time

That doesn't scale.
At least not for serious development work.

---

## The idea: agents, not prompts

Instead of prompts, use **agents**.

An agent is:

- One chat = one role
- Fixed rules
- Fixed output format
- Project-aware context
- Opinionated by design

This mirrors tools like Claude Code,
applied to **ChatGPT + VS Code**.

The goal is not better answers.
The goal is consistent answers.

---

## How this works in practice

- One VS Code chat per agent
- First message = agent definition
- That chat is never reused for other work

Simple, boring, effective.

---

## Repository structure

- `agents/` → React performance, code review, architecture agents
- `docs/` → Design principles, agent contract, and usage
- `examples/` → Examples of real agent output

---

## Who this is for

- Developers using ChatGPT in VS Code
- People who want consistency, not clever prompts
- Anyone curious about agent-based workflows

## Naming conventions

- One agent per file
- File name matches the agent name
- Chat name in VS Code should match the agent name exactly

Example:
File: `react-performance-agent.md`  
Chat: `React Performance Agent`

## Roadmap

- Add testing-focused agent
- Expand real-world usage examples

No automation planned.
This repository focuses on thinking tools, not products.
