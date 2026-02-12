# Project Context

**Purpose:** Define shared project context for all agents and contributors.

This document establishes the stable baseline assumptions for all architectural, API, data, feature, and debt evaluations.

All agents must reference this context before issuing structural recommendations.

If an evaluation contradicts this context, escalation is required.

---

# Project overview

## Product mission

Describe the system in one sentence:

> A scalable, data-driven application designed to deliver predictable, maintainable, and evolvable functionality over time.

## Primary objectives

- Enable safe, incremental evolution
- Maintain strict structural boundaries
- Preserve data integrity and contract stability
- Minimize long-term cognitive load
- Avoid unnecessary architectural complexity

## Scope definition

In scope:

- Core domain functionality
- Public and internal APIs
- Data persistence and schema evolution
- Deployment and operational stability

Out of scope:

- Experimental architectural paradigms
- Premature scaling optimizations
- Unvalidated abstraction layers
- Theoretical purity disconnected from business value

---

# Stack and technologies

## Core languages

- TypeScript (primary application language)
- Node.js (runtime)
- SQL (primary persistence layer)

## Frontend

- Vue.js (UI framework)
- Strong typing and composition-based architecture

## Backend

- Layered application structure
- Explicit domain logic separation
- Service-oriented modules

## Database

- Relational database (e.g., PostgreSQL)
- Strict referential integrity
- Explicit migrations
- No implicit schema drift

## Infrastructure

- Containerized deployment (Docker)
- CI/CD pipeline with controlled migrations
- Environment parity across stages

## Tooling

- ESLint / formatting enforcement
- Structured logging
- Version-controlled migrations
- Explicit dependency management

Agents must not recommend tools or frameworks that violate core stack principles without escalation.

---

## UI constraints

UI implementation must follow disciplined boundaries when translating external designs (Figma, pencil, mockups) into code.

### UI responsibility boundaries

- UI components own presentation, interaction flow, and local view state.
- Domain invariants and business rules must remain in Domain/Application layers.
- Infrastructure concerns (transport, persistence, runtime wiring) must not leak into presentational components.
- Shared UI primitives and layout patterns should be reused before creating new abstractions.

### Cross-agent consultation rules

- Consult Feature Design Agent when design implementation introduces new behavior, flow changes, or ambiguous feature scope.
- Consult API Design Agent when UI requires new endpoints, contract changes, or payload shape decisions.
- Consult Data Modeling Agent when UI interactions imply new entities, constraints, or state transition requirements.
- Escalate to Architecture Agent when UI proposals blur module boundaries or introduce cross-layer coupling.

### Responsive and layout conventions

- Responsive behavior is mandatory, not optional enhancement.
- Layouts must be defined with predictable breakpoint strategy and avoid ad hoc viewport-specific patches.
- Component structure should support progressive adaptation (desktop, tablet, mobile) without duplicating business logic.
- Spacing and alignment must follow system conventions rather than one-off visual fixes.

### Design token and visual consistency rules

- Colors, spacing, typography, radius, and elevation must use approved design tokens.
- Hardcoded visual values are allowed only when explicitly justified and documented.
- Visual consistency takes precedence over local styling convenience.
- Token deviations or missing tokens must be raised explicitly before implementation drift compounds.

---

# Architectural style

## System organization

The system follows a layered architecture:

- Domain layer (business logic and invariants)
- Application layer (orchestration)
- API layer (transport and contracts)
- Data layer (persistence and migrations)
- Infrastructure layer (runtime concerns)

Layer boundaries are explicit and enforced.

## Architectural principles

- Clear ownership per module
- No cross-layer leakage
- No shared mutable global state
- Explicit dependency direction
- Controlled coupling

## Dependency rule

Dependencies must flow inward:

Infrastructure → Application → Domain

Never the reverse.

Violations require explicit justification and escalation.

---

# Naming & patterns

## Naming conventions

- Names reflect domain meaning, not technical implementation
- Avoid generic terms (e.g., “Manager”, “Helper”)
- Explicit verbs for actions
- Explicit nouns for domain entities
- Consistent terminology across API, domain, and database

Ambiguous naming is treated as structural risk.

---

## Recurring implementation patterns

- Explicit state modeling over implicit flags
- Controlled service boundaries
- Explicit transaction handling
- Schema-first migrations
- Resource-oriented API design
- Avoid speculative abstraction

Patterns must serve clarity, not aesthetics.

---

# Conventions and non-goals

## Coding conventions

- Prefer explicit over implicit behavior
- Avoid hidden side effects
- Avoid magic defaults
- Fail explicitly, not silently
- Keep functions small but cohesive

## Process conventions

- Structural changes require agent review
- High-severity findings trigger escalation
- Intentional debt must be documented
- Schema changes require migration review

## Non-goals

The system explicitly avoids:

- Premature microservices
- Event sourcing unless justified by domain complexity
- Over-generalized frameworks
- Complex abstraction hierarchies without proven need
- Optimizing for scale without measured bottlenecks

---

## System invariants

The following invariants must always hold true:

- Domain logic must not depend on infrastructure concerns.
- Data integrity must be enforced at the persistence layer.
- Public contracts must not change silently.
- State transitions must be explicit and controlled.
- Module ownership must remain unambiguous.

Violations of these invariants require explicit escalation and documentation.

---

## Evolution model

The system is designed for incremental evolution.

All changes must:

- Be reversible when feasible.
- Avoid destructive migrations without explicit planning.
- Minimize cross-module ripple effects.
- Preserve backward compatibility where possible.

Large structural shifts must be staged and documented.

---

## Centrality awareness

Not all components have equal weight.

Core domain modules:
- Require stricter modeling discipline.
- Demand higher review thresholds.
- Justify elevated severity classifications.

Peripheral or isolated modules:
- Allow more localized flexibility.
- Do not justify systemic redesign.

Agents must account for module centrality in their evaluations.

---

## Change surface principle

When evaluating a decision, consider:

- How many modules are affected?
- How many boundaries are crossed?
- How many future features depend on this design?
- How difficult is rollback?

Prefer solutions that minimize change surface and systemic ripple effects.

---

## Explicit trade-off declaration rule

If a recommendation intentionally sacrifices:

- Simplicity
- Maintainability
- Boundary clarity
- Operational simplicity

The trade-off must be declared explicitly.

Implicit trade-offs are considered structural risk.

---

## Drift detection principle

Over time, systems drift from their original architecture.

Agents must:

- Detect architectural drift.
- Identify deviations from documented patterns.
- Flag pattern erosion early.
- Recommend correction before entropy compounds.

---

# Context stability rule

This document is considered stable configuration.

If project assumptions change (e.g., architecture shift, database model change, contract exposure change), this file must be updated before agents adjust behavior.

Agents must treat this document as the authoritative baseline for evaluation.

---

# Final principle

All recommendations must align with:

- Structural integrity
- Data integrity
- Contract stability
- Long-term evolvability

This context defines the default mental model for all decisions.
Deviation requires explicit documentation and escalation.
