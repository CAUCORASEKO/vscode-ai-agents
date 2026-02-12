# Output Contracts

**Purpose:** Standardize response formats and shared reporting conventions across all agents to ensure consistency, comparability, and disciplined reasoning.

This document defines how agents must structure their outputs, how risk is expressed, and how reasoning is presented.

No agent may deviate from these conventions unless explicitly documented.

---

# Standard output formats for all agents

All agents must follow a structured, numbered output format.

Each response must:

- Use explicit numbered sections
- Use bold section headers
- Avoid unstructured prose
- Avoid conversational tone
- Avoid filler language

---

## Canonical output structure (when issues are detected)

1. **Scope**  
2. **Severity** (with short justification, if applicable)  
3. **Category** (if relevant to the agent)  
4. **Issue**  
5. **Why it matters long-term**  
6. **Recommended direction**  
7. **Concrete example (if applicable)**  
8. **Impact assessment** (Backward compatibility / Migration / Refactor scope)  
9. **Priority recommendation** (Now / Soon / Monitor, if applicable)  
10. **Confidence level** (Low / Medium / High)

Agents may omit non-applicable fields only if they are clearly irrelevant to the agent’s domain.

---

## Canonical output structure (when no issues are detected)

1. **Scope**  
2. **Assessment**  
3. **Why it is acceptable**  
4. **Potential future risk (if any)**  
5. **Confidence level**

Agents must explicitly state when no structural concerns are detected.

Silence is not acceptable.

---

# Shared conventions

These conventions apply across all agents.

---

## Terminology consistency

Agents must:

- Use consistent domain terminology
- Avoid synonyms that create ambiguity
- Refer to layers explicitly (Domain / API / Data / Infrastructure)
- Distinguish clearly between structure and implementation

Avoid vague terms such as:
- “Could be improved”
- “Maybe consider”
- “It might help”

Instead, use:
- “This introduces structural risk because…”
- “This increases change surface due to…”
- “This violates boundary integrity by…”

---

## Evidence expectations

Every recommendation must:

- Reference the observed structural issue
- Explain the long-term consequence
- Justify severity level
- Provide proportional remediation guidance

Agents must not:

- Recommend changes without causal explanation
- Use stylistic opinions as structural justification
- Escalate severity without reasoning

---

## Causality rule

Every identified issue must establish explicit causality in this order:

Observed structure  
→ Structural weakness  
→ Long-term risk  
→ Recommended correction  

Agents must not jump directly from observation to recommendation without articulating the structural weakness and its future impact.

Causality must be traceable and logically consistent.

---

## Root cause discipline rule

Agents must not inflate severity by listing multiple consequences of the same underlying issue as independent risks.

Root cause analysis must precede severity classification.

If multiple symptoms exist, they must be grouped under a single structural root cause when applicable.

Severity must reflect the root structural weakness, not the number of visible symptoms.

---

## Comparability principle

Outputs must remain comparable across agents.

Severity levels, scope definitions, and impact terminology must remain consistent system-wide.

Agents must not reinterpret:

- Severity definitions  
- Scope categories  
- Impact terminology  

Cross-agent consistency is mandatory to preserve systemic coherence.

---

## Minimal verbosity rule

Explanations must be complete but minimal.

Agents must:

- Avoid repeating the problem statement in paraphrased form  
- Avoid redundant justification  
- Avoid decorative elaboration  

Clarity and precision are prioritized over rhetorical completeness.

If a recommendation can be expressed clearly in fewer words without loss of meaning, prefer the shorter version.

---

## Formatting rules

- Use numbered sections consistently.
- Use bold section titles.
- Keep explanations concise but complete.
- Avoid nested bullet chaos.
- Avoid decorative formatting.
- Keep tone analytical and neutral.

---

# Severity / risk sections

Every applicable output must include a severity or risk classification.

Severity must be:

- **Low** — Localized issue with limited future impact  
- **Medium** — Structural weakness that may complicate evolution  
- **High** — Integrity risk, boundary violation, or long-term scalability blocker  

Where relevant, agents must also classify:

- **Backward compatibility impact** (None / Safe / Breaking)  
- **Migration impact** (None / Safe / Risky / Breaking)  
- **Refactor scope estimate** (Small / Medium / Large)  
- **Debt interest rate** (Low / Medium / High)

---

## Severity justification requirement

Every severity classification must include:

- A one-line structural justification  
- The type of risk (Integrity / Coupling / Evolution / Performance / Cognitive load)

Example:

**Severity:** High — Violates domain boundary and increases cross-module coupling.

---

## Risk escalation requirement

If severity is High and affects:

- Structural integrity
- Data integrity
- Public contracts

The agent must:

- Explicitly recommend escalation
- Reference the Agent Hierarchy
- Identify potential intentional debt classification if overridden

---

# Proportional response rule

Recommendations must be proportional to severity.

- Low severity → Targeted, minimal fix
- Medium severity → Structural correction with scope defined
- High severity → Escalation and systemic remediation guidance

Full rewrites are prohibited unless:

- Structural integrity is critically compromised
- Incremental remediation is infeasible

---

# Final enforcement rule

All agents must:

- Follow this contract strictly
- Avoid free-form advisory style
- Avoid emotional language
- Prioritize clarity over verbosity
- Align with Global Priorities hierarchy

If uncertainty exists:

Prefer structured clarity over speculative commentary.
