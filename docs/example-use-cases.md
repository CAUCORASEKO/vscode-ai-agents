# Example Use Cases

**Purpose:** Provide reference invocations and expected outputs for common and edge scenarios across all agents in the system.

This document demonstrates how agents should be invoked and how structured outputs must look. These examples serve as calibration references to maintain consistency, rigor, and clarity.

---

# Real examples of invocation

Below are realistic scenarios for each agent.

---

## 1. Feature Design Agent

### Invocation

"We want to introduce a bulk user import feature that allows CSV uploads. The system should validate rows, create users, and return a summary of successes and failures."

---

## 2. Data Modeling Agent

### Invocation

"Proposed schema change:

Table: invoices
- id (uuid, pk)
- customer_id (uuid)
- amount (numeric)
- status (varchar)
- paid_at (timestamp, nullable)

There is no foreign key constraint on customer_id."

---

## 3. API Design Agent

### Invocation

"New endpoint proposal:

POST /orders/create

Request:
{
  userId: string,
  items: OrderItem[],
  discountCode?: string
}

Response:
{
  success: boolean,
  orderId: string
}"

---

## 4. Architecture Agent

### Invocation

"We are moving reporting logic directly into controllers to speed up feature delivery."

---

## 5. Technical Debt Agent

### Invocation

"Several services duplicate validation logic and share database access without clear ownership. Refactors have been postponed multiple times."

---

# Input → Expected Agent Output

Below are calibrated examples showing correct structured output behavior.

---

## Feature Design Agent Example Output

1. **Problem clarity:** Clear  
2. **Scope definition:**  
   - In scope: CSV parsing, validation, batch processing, result summary  
   - Out of scope: Data transformation rules beyond validation  
3. **Affected layers:** Domain, API, Data  
4. **Primary design risks:**  
   - Long-running request blocking  
   - Partial failure handling complexity  
5. **Responsibility allocation:**  
   - Domain: Validation and import orchestration  
   - API: Upload endpoint and summary response  
   - Data: Batch insert strategy  
6. **Recommended structural approach:**  
   Use asynchronous processing with job tracking instead of synchronous request lifecycle.  
7. **Incremental rollout strategy:**  
   - Implement job model  
   - Add background processing  
   - Expose job status endpoint  
8. **Backward compatibility impact:** None  
9. **Complexity assessment:** Medium — touches orchestration and error handling  
10. **Confidence level:** High  

---

## Data Modeling Agent Example Output

1. **Scope:** Single Entity  
2. **Severity:** High — Missing referential integrity constraint  
3. **Issue:** `customer_id` lacks foreign key constraint to customers table.  
4. **Why it matters long-term:** Allows orphan records and inconsistent reporting.  
5. **Recommended direction:** Add foreign key constraint with cascade policy defined explicitly.  
6. **Concrete example:**  
   `customer_id UUID REFERENCES customers(id)`  
7. **Migration impact:** Safe (if no invalid data exists)  
8. **Confidence level:** High  

---

## API Design Agent Example Output

1. **Scope:** Local Endpoint  
2. **Severity:** Medium — Action-based naming  
3. **Issue:** `/create` endpoint naming violates resource-oriented design.  
4. **Why it matters long-term:** Inconsistent semantics complicate API evolution.  
5. **Recommended direction:** Use `POST /orders` and return 201 Created.  
6. **Concrete example:**  
   - `POST /orders`  
   - 201 Created with Location header  
7. **Backward compatibility impact:** Breaking if already published  
8. **Confidence level:** High  

---

## Architecture Agent Example Output

1. **Scope:** Cross-module  
2. **Issue:** Reporting logic placed in controllers violates separation of concerns.  
3. **Why it matters long-term:** Erodes architectural boundaries and increases duplication risk.  
4. **Recommended direction:** Move reporting logic into a dedicated service layer.  
5. **Concrete example:** Introduce ReportingService consumed by controllers.  

---

## Technical Debt Agent Example Output

1. **Scope:** System-wide  
2. **Debt category:** Architectural debt, Coupling debt  
3. **Severity:** High — Boundary erosion and duplicated logic  
4. **Description of debt:** Shared table access without ownership definition.  
5. **Root cause:** Lack of explicit domain ownership early in system design.  
6. **Long-term impact:** Increased regression risk and slower feature velocity.  
7. **Recommended remediation strategy:** Define ownership and centralize validation.  
8. **Refactor scope estimate:** Large  
9. **Priority recommendation:** Soon  
10. **Confidence level:** High  

---

# Edge case examples

---

## Edge Case 1 — Insufficient Context

### Invocation

"Review this feature."

### Expected Behavior

- Agent must request clarification.
- Must list explicit assumptions before proceeding.
- Must not fabricate missing architectural context.

---

## Edge Case 2 — Business Pressure Override

### Invocation

"We know this breaks boundaries, but we need to ship this week."

### Expected Behavior

- Architecture Agent flags structural violation.
- Escalation path is triggered.
- If override is chosen, classify as intentional debt.
- Technical Debt Agent must track remediation window.

---

## Edge Case 3 — No Issues Detected

### Invocation

"Review this small endpoint that follows all conventions."

### Expected Behavior

Agent must explicitly state:

"No structural concerns detected."

And still provide:
- Scope
- Assessment
- Confidence level

---

## Edge Case 4 — Overengineering Risk

### Invocation

"We want to introduce event sourcing for this small CRUD module."

### Expected Behavior

- Feature Design Agent flags overengineering risk.
- Architecture Agent evaluates long-term necessity.
- Recommendation favors simplicity unless justified by constraints.

---

## Edge Case 5 — Cross-Agent Conflict

### Scenario

- API Design Agent suggests contract change.
- Data Modeling Agent warns about migration risk.

### Expected Handling

- Escalation to Architecture Agent.
- Explicit documentation of trade-offs.
- Decision recorded and, if applicable, classified as intentional debt.

---

This document serves as calibration to ensure consistent, disciplined agent behavior across routine, complex, and high-pressure scenarios.

---

# Multi-Agent Interaction Example

## 1. Scenario description

A new feature, "Team Billing Profiles," introduces a new `billing_profiles` entity linked to `teams`.  
The initial proposal stores `default_payment_method_id` as a nullable string without a foreign key.  
The API proposal introduces `POST /teams/{teamId}/billing-profile/create` with action-based semantics.  
A boundary conflict appears because billing profile validation logic is proposed inside API controllers.  
Delivery pressure requires shipping before a full domain-service extraction is completed.

---

## 2. Sequential agent outputs

### Feature Design Agent Output

1. **Problem clarity:** Clear  
2. **Scope definition:**  
   - In scope: Introduce billing profile entity, create/update billing profile flow, payment method association  
   - Out of scope: Full billing ledger redesign, invoice generation workflow  
3. **Affected layers:** Domain, API, Data  
4. **4. Primary design risks (structural, coupling, state, migration):**  
   - Controller-level validation bypassing domain ownership  
   - Nullable payment method reference creating ambiguous state  
   - Future coupling between team lifecycle and billing profile lifecycle  
5. **Responsibility allocation:**  
   - Domain: Billing profile invariants and validation rules  
   - API: Contract exposure and request normalization  
   - Data: Referential integrity and lifecycle constraints  
6. **Recommended structural approach:**  
   Introduce a dedicated billing domain service and enforce explicit entity constraints before endpoint expansion.  
7. **Incremental rollout strategy:**  
   - Add `billing_profiles` schema with constraints  
   - Implement domain service with minimal commands  
   - Expose create endpoint and follow-up update endpoint  
8. **Backward compatibility impact:** None  
9. **Complexity assessment:** Medium — introduces new entity and cross-layer invariants  
10. **Confidence level:** High  

---

### Data Modeling Agent Output

1. **Scope:** Cross-entity  
2. **Severity:** High — Missing referential integrity on payment method relationship  
3. **Issue:** `billing_profiles.default_payment_method_id` is defined as free-form nullable text without a foreign key to payment methods.  
4. **Why it matters long-term:** Invalid references will accumulate and break billing workflows, reporting, and migration safety.  
5. **Recommended direction:** Use UUID foreign key with explicit nullability policy and enforce relationship constraints.  
6. **Concrete example (if applicable):**  
   - `default_payment_method_id UUID NULL REFERENCES payment_methods(id)`  
7. **Migration impact:** Risky  
8. **Confidence level:** High  

---

### API Design Agent Output

1. **Scope:** Service-level  
2. **Severity:** Medium — Action-based endpoint naming and ambiguous create semantics  
3. **Issue:** `POST /teams/{teamId}/billing-profile/create` mixes action naming with resource creation semantics and complicates future contract consistency.  
4. **Why it matters long-term:** Inconsistent endpoint conventions increase API surface entropy and make versioning strategy harder to maintain.  
5. **Recommended direction:** Use resource-oriented endpoint shape and explicit response semantics.  
6. **Concrete example (if applicable):**  
   - `POST /teams/{teamId}/billing-profile`  
   - Return `201 Created` with profile resource representation  
7. **Backward compatibility impact:** Safe  
8. **Confidence level:** High  

---

### Architecture Agent Output

1. **Scope:** Cross-module  
2. **Issue:** Billing validation inside controllers violates boundary ownership and introduces cross-layer coupling between API orchestration and domain invariants.  
3. **Why it matters long-term:** Boundary leakage increases duplication risk and weakens change isolation as billing rules evolve.  
4. **Recommended direction:** Keep controllers thin, route validation and invariants through a billing domain service, and isolate persistence access behind service boundaries.  
5. **Concrete example (if applicable):** `BillingProfileService` handles create/update invariants; controllers only map request/response contracts.  

---

### Technical Debt Agent Output

1. **Scope:** Cross-module  
2. **Debt category:** Architectural debt, Coupling debt, Migration debt  
3. **Severity:** Medium — Temporary boundary compromise accepted under delivery constraint  
4. **Description of debt:** Controller retains interim validation path for one release while domain service extraction is deferred.  
5. **Root cause:** Delivery deadline before completion of domain-service refactor sequence.  
6. **Long-term impact:** If not remediated quickly, duplicated validation paths will diverge and increase regression risk.  
7. **Recommended remediation strategy:**  
   - Complete domain service extraction  
   - Remove controller-level validation branch  
   - Add guardrail tests at service boundary  
8. **Refactor scope estimate:** Medium  
9. **Priority recommendation:** Soon  
10. **Confidence level:** High  
11. **Debt interest rate:** Medium  

---

## 3. Final arbitration decision

Architecture Agent arbitration is accepted as final:

- Resource-oriented API contract is adopted (`POST /teams/{teamId}/billing-profile`).
- Data Modeling constraint changes are mandatory before production rollout.
- A temporary controller validation fallback is allowed for one release only.
- Domain service extraction is scheduled as a required follow-up checkpoint.

---

## 4. Intentional debt classification (if applicable)

- **Type:** Intentional debt  
- **Reason:** Delivery deadline required staged migration to preserve release timing  
- **Owner:** Technical Debt Agent tracking with Architecture Agent checkpoint  
- **Remediation checkpoint:** Next release hardening milestone  

---

# Intentional Debt Example

## 1. Invocation

"Enterprise onboarding must ship this sprint.  
To move faster, we will allow direct API-layer writes into the subscription table from the onboarding controller, even though billing ownership belongs to the billing module."

---

## 2. Architecture Agent structured output

1. **Scope:** System-wide  
2. **Issue:** Direct onboarding-controller writes into billing persistence violate module ownership boundaries.  
3. **Why it matters long-term:** This creates hidden coupling between onboarding and billing, increasing migration and change-risk across both modules.  
4. **Recommended direction:** Preserve billing module ownership by routing all subscription mutations through billing services, even if onboarding orchestrates the flow.  
5. **Concrete example (if applicable):** Onboarding calls `BillingSubscriptionService.createSubscription(...)`; controller never writes billing tables directly.  

---

## 3. Final decision summary

Escalation is triggered due to business-critical deadline.  
A temporary override is approved with explicit risk acceptance and scheduled review.  
Decision is recorded as intentional debt with mandatory remediation in the next planning cycle.

---

## 4. Technical Debt Agent structured output

1. **Scope:** Cross-module  
2. **Debt category:** Architectural debt, Coupling debt  
3. **Severity:** High — Boundary violation on critical domain ownership  
4. **Description of debt:** Onboarding module writes directly to billing subscription tables, bypassing billing service boundary.  
5. **Root cause:** Time-constrained delivery decision prioritizing short-term throughput over boundary integrity.  
6. **Long-term impact:** Higher regression probability, brittle integration points, and delayed billing module evolution.  
7. **Recommended remediation strategy:**  
   - Replace direct writes with billing service command path  
   - Add ownership guard checks and integration tests  
   - **Remediation window:** Complete within 2 sprints  
8. **Refactor scope estimate:** Medium  
9. **Priority recommendation:** Now  
10. **Confidence level:** High  
11. **Debt interest rate:** High  

---

# False Positive Handling Example

## 1. Invocation

"Review this reporting endpoint refactor.  
The controller now calls `ReportingFacade.generateTeamSummary(teamId)` and no SQL logic is present in controller code."

---

## 2. Initial concern

Architecture Agent initially flags a potential boundary concern because reporting behavior appears newly introduced at controller level and could indicate misplaced business logic.

---

## 3. Clarification context

Further clarification confirms:

- Controller only performs request mapping and response serialization.
- `ReportingFacade` belongs to the reporting application layer.
- Domain and data access remain encapsulated in reporting services.
- No cross-module ownership violations are introduced.

---

## 4. Final structured output

1. **Scope:** Cross-module  
2. **Assessment:** No structural concerns detected.  
3. **Why it is acceptable:** Responsibility boundaries are preserved; controller remains orchestration-only and reporting logic is contained in designated service layers.  
4. **Potential future risk (if any):** Monitor facade growth to avoid aggregation of unrelated responsibilities.  
5. **Confidence level:** High  
