# VS Code AI Agents

A structured, role-based engineering governance system built on top of ChatGPT inside VS Code.

No plugins.  
No automation layer.  
No black-box magic.

Just explicit rules, contracts, priorities, and disciplined thinking.

---

# Why this exists

Most developers use ChatGPT like a general-purpose chat:

- Repeating context
- Mixing unrelated problems
- Receiving inconsistent answers
- Losing structural rules over time
- Getting clever suggestions without discipline

That works for small tasks.

It does not scale for serious development.

This repository exists to solve that.

---

# The core idea: governance, not prompts

Instead of ad-hoc prompting, this system defines:

- Role-based agents
- Fixed output contracts
- Severity discipline
- Escalation hierarchy
- Global priorities
- Shared project context

Each agent operates within defined authority boundaries.

The goal is not “better answers”.

The goal is:

- Consistent decisions
- Reduced cognitive load
- Controlled structural evolution
- Long-term maintainability

---

# What this system provides

## 1. Specialized agents

- Architecture Agent
- API Design Agent
- Data Modeling Agent
- Feature Design Agent
- Technical Debt Agent
- UI Implementation Agent

Each agent:

- Owns a specific decision domain
- Follows strict output contracts
- Classifies severity consistently
- Escalates when structural integrity is threatened

---

## 2. Governance documents

The `docs/` directory defines:

- Global priorities
- Severity guidelines
- Output contracts
- Agent hierarchy and escalation rules
- Example calibrated use cases

This ensures:

- Agents remain consistent
- Recommendations are comparable
- Structural discipline is enforced
- Drift is detected early

---

## 3. Project context

`project-context.md` defines:

- Stack and technologies
- Architectural style
- Naming conventions
- System invariants
- Explicit non-goals

Agents evaluate decisions against this baseline.

If recommendations contradict the documented context, escalation is required.

---

# How this works in practice

- One VS Code chat per agent.
- The first message defines the agent.
- That chat is never reused for other purposes.
- Structural changes trigger cross-agent review.

This mirrors structured engineering review, not casual conversation.

---

# Who this is for

- Engineers working on evolving systems
- Developers building long-lived products
- Teams who care about structural integrity
- People who prefer boring consistency over clever chaos

This is not:

- A no-code automation system
- A productivity gimmick
- A replacement for architectural thinking

It is a structured augmentation tool.

---

# Philosophy

This system is built around one principle:

> Reduce long-term change cost while preserving structural integrity.

Every document and agent enforces that principle.

---

# Repository structure

```
agents/              → Domain-specific decision agents
docs/                → Governance framework and contracts
project-context.md   → Stable baseline assumptions
examples/            → Calibrated usage examples
```

---

# Design constraints

- No hidden automation
- No runtime dependencies
- No external orchestration layer
- No magic state persistence

All discipline is explicit.

---

# Roadmap

Future expansions may include:

- Testing Agent
- Security Review Agent
- Performance Profiling Agent
- Multi-agent simulation scenarios

The focus remains structural thinking, not tooling complexity.

---

# Final note

This repository is not about AI.

It is about disciplined engineering decision-making.

AI is only the execution medium.