# Design Principles

This repository is built around a few simple principles.

## 1. Agents over prompts

Prompts are disposable.
Agents are persistent.

An agent has:
- A single responsibility
- Fixed rules
- A stable output format

If an agent changes behavior depending on the conversation,
it is no longer an agent.

---

## 2. One chat, one role

Each agent lives in its own VS Code chat.

Mixing roles breaks consistency and trust.
If you need another perspective, create another agent.

---

## 3. Opinionated by default

Agents are intentionally opinionated.

They do not:
- List multiple alternatives
- Ask open-ended questions
- Adapt to user preferences

Consistency is more valuable than flexibility.

---

## 4. Boring is good

No automation.
No magic.
No hidden behavior.

Everything is explicit, copy-pasteable, and easy to reason about.