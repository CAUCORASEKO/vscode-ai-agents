# Global Priorities

**Purpose:** Define system-wide decision priorities and shared quality criteria that govern all agents, override local optimizations, and ensure long-term structural discipline.

This document is the highest-level decision framework in the system.  
All agents must align with these principles.  
When conflicts arise, these priorities prevail.

---

# The global decision hierarchy

When trade-offs exist, decisions must follow this ordered hierarchy:

1. **Structural integrity**
2. **Data integrity**
3. **Contract stability**
4. **Boundary clarity**
5. **Long-term maintainability**
6. **Cognitive load minimization**
7. **Operational simplicity**
8. **Performance (only when measurable and material)**
9. **Local convenience**

No lower-level priority may override a higher-level one without explicit escalation and documentation.

---

## Non-negotiable invariants

The following principles must never be compromised:

- Data integrity (no silent corruption, no orphan records)
- Explicit ownership of responsibilities
- Referential integrity at the persistence layer
- Contract clarity for public and cross-service interfaces
- Clear architectural boundaries between layers

Any violation of these invariants requires:

- Explicit escalation
- Documented risk acceptance
- Classification as intentional debt
- A defined remediation window

These invariants override performance, convenience, and delivery pressure.

---

## 1. Structural integrity

The system must preserve:

- Clear architectural boundaries  
- Explicit ownership of responsibilities  
- Layer separation (Domain / API / Data / Infrastructure)  
- Controlled dependencies  

Structural shortcuts compound over time.  
When in doubt, protect boundaries.

---

## 2. Data integrity

The system must guarantee:

- Referential integrity  
- Explicit constraints  
- Predictable state transitions  
- Safe schema evolution  

Data corruption is more expensive than feature delay.

---

## 3. Contract stability

Public and internal interfaces must be:

- Explicit  
- Predictable  
- Backward-compatible (unless intentionally versioned)  
- Evolution-safe  

Breaking contracts requires structured escalation.

---

## 4. Boundary clarity

Responsibilities must be:

- Explicitly owned  
- Non-overlapping  
- Discoverable  
- Predictable  

Hidden coupling increases future change cost.

---

## 5. Long-term maintainability

The system must:

- Support incremental change  
- Avoid compounding complexity  
- Favor explicitness over cleverness  
- Allow safe refactors  

Maintainability is measured by ease of change, not code aesthetics.

---

## 6. Cognitive load minimization

Changes must:

- Reduce implicit knowledge  
- Avoid hidden side effects  
- Keep mental models stable  
- Prefer boring, obvious solutions  

If a solution increases required context to understand the system, it must be justified.

---

## 7. Operational simplicity

The system must:

- Support safe deployments  
- Enable clear migrations  
- Avoid fragile runtime dependencies  
- Minimize hidden infrastructure complexity  

Operational risk is architectural risk.

---

## 8. Performance

Performance optimizations are justified only when:

- A measurable bottleneck exists  
- Impact is material  
- Structural integrity is preserved  

Never trade clarity for hypothetical speed.

---

## 9. Local convenience

Short-term speed, reduced typing, or minor code brevity must never override structural or integrity principles.

---

## Change cost heuristic

When evaluating any structural or design decision, estimate:

- How many modules must change if this decision evolves?
- How many mental models are affected?
- How difficult is rollback?
- Does this introduce hidden coupling?
- Does this expand the change surface area?

Prefer the option that:

- Minimizes long-term change surface
- Localizes impact
- Preserves boundary clarity
- Reduces cascading modifications

A solution that is slightly more verbose but reduces systemic ripple effects is preferred.

---

## Entropy principle

System entropy increases naturally over time.

Every change must:

- Reduce entropy
- Contain entropy
- Or explicitly track entropy if it cannot be avoided

Untracked entropy becomes technical debt.

Agents must explicitly flag decisions that:

- Increase structural ambiguity
- Blur boundaries
- Introduce implicit behavior
- Increase cognitive load

If entropy is increased intentionally, it must be:

- Classified
- Time-bounded
- Monitored by the Technical Debt Agent

---

# Definitions of simplicity, maintainability, clarity

These definitions standardize interpretation across agents.

---

## Simplicity

Simplicity means:

- Fewer moving parts  
- Explicit behavior  
- Predictable control flow  
- No unnecessary abstractions  
- No speculative flexibility  

Simplicity does NOT mean:

- Fewer lines of code  
- Over-condensed logic  
- Clever shortcuts  

True simplicity reduces future decision friction.

---

## Maintainability

Maintainability means:

- Safe, incremental change is possible  
- Responsibilities are discoverable  
- Modifications do not require global context  
- Changes are localized  
- Refactors do not cascade unpredictably  

Maintainability is validated by change cost, not static elegance.

---

## Clarity

Clarity means:

- Intent is obvious from structure  
- Naming reflects domain meaning  
- Boundaries are visible  
- Invariants are explicit  
- Failure modes are understandable  

Clarity eliminates guesswork.

---

# Decision enforcement rule

All agents must:

- Reference this hierarchy when justifying recommendations  
- Explicitly state when trade-offs violate a higher-level priority  
- Escalate when structural integrity is threatened  

If uncertainty remains:

Prefer the option that:

- Minimizes future migration risk  
- Reduces coupling  
- Preserves explicit boundaries  
- Decreases cognitive load  

---

# Final principle

The system exists to enable sustainable evolution.

Any decision that increases future change cost without strong justification is misaligned with global priorities.
