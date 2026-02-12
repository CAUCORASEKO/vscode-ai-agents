# Severity Guidelines

**Purpose:** Define severity classification, escalation behavior, and reporting discipline for all agents in the system.

Severity is not a measure of aesthetic imperfection.  
It is a measure of long-term structural risk.

All agents must classify severity consistently according to this document.

---

# Severity levels

Severity reflects structural impact, not emotional urgency.

Each level must be justified explicitly.

---

## Low Severity

**Definition:**  
Localized structural weakness with limited systemic impact.

**Characteristics:**

- Does not violate core architectural boundaries  
- Does not threaten data integrity  
- Does not introduce contract instability  
- Does not significantly increase change surface  
- Can be corrected incrementally with minimal ripple effects  

**Typical risk types:**

- Minor inconsistency  
- Limited coupling within same layer  
- Missing non-critical constraint  
- Naming ambiguity without structural consequence  

**Expected behavior:**

- Provide targeted correction  
- No escalation required  
- Priority usually "Monitor" or "Soon"  

Low severity must not be escalated unless compounded by repetition.

---

## Medium Severity

**Definition:**  
Structural weakness that may significantly increase future change cost or introduce evolutionary friction.

**Characteristics:**

- Blurs layer boundaries  
- Introduces moderate coupling  
- Weakens schema evolution safety  
- Creates ambiguous ownership  
- Complicates refactors or incremental change  

**Typical risk types:**

- Cross-layer leakage  
- Weak referential integrity  
- Contract modeling weakness  
- Feature introducing unnecessary abstraction  
- Migration risk without safeguards  

**Expected behavior:**

- Provide structured remediation strategy  
- Identify root cause  
- Define refactor scope estimate  
- Escalation required if it conflicts with higher-level priorities  

Medium severity is a warning sign of growing entropy.

---

## High Severity

**Definition:**  
Structural violation or integrity risk that threatens long-term system stability.

**Characteristics:**

- Violates architectural boundaries  
- Breaks data integrity or referential guarantees  
- Introduces unsafe public contract changes  
- Creates systemic coupling across modules  
- Blocks future evolution  
- Significantly increases change surface  
- Requires cross-module refactor  

**Typical risk types:**

- Shared database access without ownership  
- Breaking API changes without versioning  
- Schema changes that risk destructive migrations  
- Circular dependencies between layers  
- Implicit state transitions without invariants  

**Expected behavior:**

- Explicitly recommend escalation  
- Reference Agent Hierarchy  
- Propose remediation path  
- Classify potential intentional debt if override occurs  
- Provide proportional but systemic correction strategy  

High severity must never be minimized for convenience.

---

## Severity downgrade rule

Severity must be downgraded when:

- The remediation is trivial and fully localized
- No structural ripple effects are introduced
- No cross-module coupling is affected
- No contract or data integrity risk exists

Agents must not preserve Medium or High severity classifications if the issue can be corrected safely and incrementally without systemic impact.

Severity must reflect structural risk, not conceptual disagreement.

---

## Context sensitivity clause

Severity must be evaluated relative to system centrality.

An issue affecting:

- Core domain entities
- Shared infrastructure components
- Public API contracts
- Cross-service boundaries

May justify elevating severity due to systemic impact.

Conversely, the same structural issue in an isolated module may warrant lower severity.

Agents must explicitly justify severity adjustments based on system centrality.

---

## False certainty safeguard

High severity classifications with Low or Medium confidence require explicit uncertainty disclosure.

Agents must state:

- What assumptions were made
- What missing information could change severity
- Whether further validation is required

High severity without confidence transparency is invalid.

Uncertainty must never be hidden behind assertive language.

---

# Severity justification requirement

Every severity classification must include:

- A one-line structural justification  
- The type of risk (Integrity / Coupling / Evolution / Performance / Cognitive load)  

Example:

**Severity:** High — Violates boundary integrity and increases cross-module coupling (Coupling risk).

Severity without explicit justification is invalid.

---

# When to report No Issues

Agents must explicitly report no issues when:

- Structural integrity is preserved  
- Boundaries remain clear  
- No long-term risk is introduced  
- No contract or data integrity is compromised  
- The change aligns with Global Priorities  

Silence is not acceptable.

When reporting no issues, agents must still include:

1. **Scope**
2. **Assessment**
3. **Why it is acceptable**
4. **Potential future risk (if any)**
5. **Confidence level**

False positives are discouraged.  
Over-classification erodes trust in severity discipline.

---

# Escalation thresholds

Escalation is mandatory when severity is High AND affects:

- Structural integrity  
- Data integrity  
- Public contracts  

Agents must:

- Recommend escalation explicitly  
- Reference Agent Hierarchy  
- Identify if the decision may become intentional debt  

---

# Examples of each level

---

## Low Severity Example

**Scenario:**  
A repository method duplicates simple validation logic already present in the same module.

**Classification:**

**Severity:** Low — Localized duplication within same boundary (Maintainability risk).  

**Rationale:**  
No cross-layer coupling. Limited impact. Safe to refactor incrementally.

---

## Medium Severity Example

**Scenario:**  
A feature introduces domain logic directly into the API layer to simplify delivery.

**Classification:**

**Severity:** Medium — Blurs boundary between Domain and API layers (Boundary clarity risk).  

**Rationale:**  
Increases future change surface and complicates refactors.

---

## High Severity Example

**Scenario:**  
Multiple services directly modify shared tables without ownership or foreign key constraints.

**Classification:**

**Severity:** High — Violates structural boundaries and risks data integrity (Integrity and Coupling risk).  

**Rationale:**  
Breaks isolation guarantees, blocks safe evolution, and increases regression risk.

---

# Entropy awareness rule

Repeated Low severity issues in the same area may collectively escalate to Medium.

Repeated Medium severity issues across modules may collectively escalate to High.

Severity must reflect systemic accumulation when patterns emerge.

---

# Final enforcement principle

Severity must remain:

- Consistent  
- Justified  
- Comparable across agents  
- Proportional to structural risk  

Inflated severity reduces credibility.  
Understated severity increases entropy.

Discipline in severity classification preserves system integrity.
