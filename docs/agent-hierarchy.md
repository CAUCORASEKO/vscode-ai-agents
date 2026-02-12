# Agent Hierarchy

**Purpose:** Define how agents coordinate, prioritize, and escalate decisions to maintain systemic coherence, prevent contradictory guidance, and protect long-term structural integrity.

This hierarchy ensures that all agents operate within clear authority boundaries and that recommendations remain consistent across architecture, data, API, feature design, and technical debt evaluations.

---

## System philosophy

The agent ecosystem operates under three principles:

1. Prevention is superior to correction.
2. Structural integrity overrides local optimization.
3. Long-term maintainability overrides short-term convenience.

Agents are not equal. They operate within defined authority layers.

---

# Authority Layers

Agents are organized into three levels of authority:

## Level 1 — Structural Authority (Highest)

- Architecture Agent
- Data Modeling Agent

These agents define structural boundaries, domain shape, and integrity constraints.

They override all lower-level recommendations if structural integrity is at risk.

---

## Level 2 — Contract & Design Authority

- API Design Agent
- Feature Design Agent

These agents define interface shape and feature structure within architectural constraints.

They cannot violate structural decisions made by Level 1.

---

## Level 3 — Corrective & Observational Authority

- Technical Debt Agent

This agent identifies erosion and recommends remediation but does not redefine architecture unless escalated.

---

# Define how agents interact

## Interaction model

Agents operate sequentially based on development phase:

1. Feature Design Agent (problem shaping)
2. Data Modeling Agent (entity and schema validation)
3. API Design Agent (contract validation)
4. Architecture Agent (system alignment)
5. Technical Debt Agent (ongoing audit)

Not all steps are mandatory for small changes, but structural changes should follow this flow.

---

## Small change shortcut

For localized, low-risk changes:
- Feature Design Agent and Architecture Agent reviews may be optional.
- Technical Debt Agent review remains recommended.

---

## Ownership boundaries

Each agent owns a specific dimension:

- Feature Design → Scope and responsibility allocation
- Data Modeling → Data integrity and schema evolution
- API Design → Contract stability and interface clarity
- Architecture → System boundaries and long-term structure
- Technical Debt → Risk accumulation and remediation

Agents must not expand beyond their defined domain.

## Scope containment rule

No agent may expand the original problem scope unless explicitly requested.

---

# Priority rules

When conflicting recommendations arise, precedence follows authority layer:

1. Architecture Agent overrides all.
2. Data Modeling Agent overrides API and Feature decisions when integrity is at risk.
3. API Design Agent overrides Feature Design when contract stability is at risk.
4. Feature Design cannot override structural or contract constraints.
5. Technical Debt Agent may recommend changes but cannot override without escalation.

---

## Conflict resolution principle

When two agents disagree:

- The agent with higher authority prevails.
- The lower-level agent must adapt within structural constraints.
- Trade-offs must be explicitly documented.

---

# Escalation rules

Escalation is required when:

- Structural integrity conflicts with business requirements.
- Data integrity conflicts with API backward compatibility.
- Technical debt remediation requires architectural redesign.
- Feature scope pressures violate architectural boundaries.

## Temporary override rule

Temporary overrides are allowed only if:

- The risk is explicitly documented
- A review checkpoint is scheduled
- The Technical Debt Agent tracks the decision

---

## Escalation path

1. Conflict must be clearly articulated in structured format.
2. Each conflicting agent must state:
   - Risk if recommendation is ignored
   - Long-term impact
3. The Architecture Agent performs final arbitration.
4. If business constraints override structural recommendations, the decision must be documented as intentional debt.

---

## Intentional debt protocol

If a lower-quality structural decision is chosen due to business constraints:

- The Technical Debt Agent must classify it.
- A remediation window must be defined.
- Debt must be tagged as intentional and monitored.

---

# Stability safeguard rule

No agent may:

- Introduce architectural changes implicitly.
- Suggest cross-layer shortcuts without explicit structural review.
- Override long-term integrity for local convenience.

---

# Final arbitration principle

When uncertainty remains:

Long-term system clarity wins over short-term delivery speed.

If still unresolved, prefer the solution that:

- Minimizes future migration risk
- Reduces cross-module coupling
- Preserves explicit boundaries

---

This hierarchy ensures:

- Consistency across decisions
- Reduced cognitive dissonance between agents
- Clear escalation logic
- Long-term structural discipline
