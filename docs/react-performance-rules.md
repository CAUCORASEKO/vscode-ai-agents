# React Performance Rules

## Authority
These rules are mandatory unless explicitly overridden
by the Architecture Agent with written justification.

## Scope
These rules apply to React and Next.js applications.

They are used by the React Performance Agent
to review, flag, and prioritize performance issues.

## Rule Severity
- CRITICAL: Must be fixed before merge
- HIGH: Should be fixed unless explicitly justified
- MEDIUM: Recommended improvement
- LOW: Optional optimization

## Rules
### RPR-001: No client-side data fetching in layout chains
Severity: HIGH

Rule:
Client-side data fetching in parent components that must render before child content must not be initiated; data must be fetched on the server or in the lowest component that actually needs it.

Rationale:
Parent-level client fetches serialize child rendering and create async waterfalls.

Example:
Move a `useEffect` fetch from `PageLayout` into the specific `UserPanel` that uses it.

### RPR-002: Parallelize independent server requests
Severity: CRITICAL

Rule:
Multiple server requests needed for a render must be initiated in parallel (e.g., `Promise.all`); they must not be awaited sequentially.

Rationale:
Sequential awaits create request waterfalls that directly increase TTFB.

### RPR-003: No per-render fetch in client components
Severity: HIGH

Rule:
Client components must not trigger data fetching on every render; data must be fetched only in effects with stable dependencies or provided by the server.

Rationale:
Per-render fetches cause repeat network work and re-render cascades.

### RPR-004: Prefer server data in React Server Components
Severity: HIGH

Rule:
In Next.js App Router, data must be fetched in React Server Components by default and results must be passed to client components as props.

Rationale:
Server data fetching avoids client waterfalls and reduces bundle size.

### RPR-005: No client components in top-level routes
Severity: HIGH

Rule:
Top-level route components (`page.tsx`, `layout.tsx`) must remain server components unless they require client-only APIs.

Rationale:
Client routes increase bundle size and shift work to the browser.

### RPR-006: Enforce dynamic import for non-critical UI
Severity: MEDIUM

Rule:
UI that is not required for initial paint must be loaded via `dynamic()` or `React.lazy`.

Rationale:
Code splitting reduces initial JS and speeds up first render.

### RPR-007: No large third-party libraries in critical path
Severity: HIGH

Rule:
Third-party libraries exceeding 50 KB min+gzip must not be imported in initial route entry points.

Rationale:
Large dependencies inflate the JS bundle and delay hydration.

### RPR-008: Prohibit barrel imports for large packages
Severity: MEDIUM

Rule:
Package root barrel imports must not be used when the package supports per-module imports; direct paths must be used.

Rationale:
Barrel imports often pull in unused code and increase bundle size.

### RPR-009: Client component boundaries must be minimal
Severity: MEDIUM

Rule:
If a file uses `"use client"`, it must not export non-interactive UI; interactive parts must be split into a small client component.

Rationale:
Keeping client boundaries small reduces client bundle size.

### RPR-010: No re-rendering from unstable props
Severity: MEDIUM

Rule:
New object, array, or function literals must not be passed as props unless memoized (`useMemo`, `useCallback`) or static.

Rationale:
Unstable props defeat memoization and increase re-renders.

### RPR-011: Memoize expensive derived values
Severity: MEDIUM

Rule:
Derived values that are expensive to compute must be memoized with `useMemo` and stable dependencies.

Rationale:
Recomputing on every render wastes CPU and can block the main thread.

### RPR-012: Memoize pure child components
Severity: LOW

Rule:
Pure child components that re-render frequently must be wrapped with `React.memo` or equivalent.

Rationale:
Memoization reduces unnecessary renders when props are unchanged.

### RPR-013: No state updates during render
Severity: HIGH

Rule:
Components must not call state setters during render; updates must occur in effects, handlers, or server actions.

Rationale:
State updates in render trigger render loops and wasted work.

### RPR-014: No synchronous heavy work in render
Severity: HIGH

Rule:
Rendering must not perform heavy synchronous computation; move to a worker, server, or memoized precomputation.

Rationale:
Blocking work in render increases input latency and frame drops.

### RPR-015: Use `useDeferredValue` for non-urgent UI
Severity: LOW

Rule:
Rendering large lists or heavy filters tied to fast input must use `useDeferredValue` or `useTransition`.

Rationale:
Deferring non-urgent renders improves responsiveness.

### RPR-016: No cascading re-renders from context
Severity: MEDIUM

Rule:
Context providers must not store frequently changing values unless consumers are scoped or values are memoized.

Rationale:
Context changes re-render all consumers and can create render storms.

### RPR-017: No `useEffect` for data required to render
Severity: CRITICAL

Rule:
Data required for the initial UI must be fetched on the server or in `async` server components; it must not be fetched in `useEffect`.

Rationale:
Effect-driven data fetching delays first render and creates waterfalls.

### RPR-018: Prevent duplicate requests on re-mount
Severity: MEDIUM

Rule:
Client data fetching must be cached or deduped to avoid duplicate requests on re-mount or route transitions.

Rationale:
Duplicate requests waste bandwidth and delay UI readiness.

### RPR-019: Enforce image optimization usage
Severity: MEDIUM

Rule:
All images in Next.js routes must use `next/image` with explicit `width` and `height` unless inlined as SVG.

Rationale:
Optimized images reduce layout shift and improve load performance.

### RPR-020: No `dangerouslySetInnerHTML` for large content
Severity: LOW

Rule:
Large HTML blobs must be streamed or server-rendered rather than injected via `dangerouslySetInnerHTML` in client components.

Rationale:
Large HTML injections increase client JS work and hydration cost.

### RPR-021: Keep critical CSS out of client JS
Severity: MEDIUM

Rule:
Route-critical CSS must not be imported via client-only modules; critical styles must load with server-rendered content.

Rationale:
Client-loaded CSS delays first render and can cause layout shift.

### RPR-022: Disallow `dynamic()` with `ssr: false` for critical content
Severity: HIGH

Rule:
`dynamic(..., { ssr: false })` must not be used for content visible on initial paint.

Rationale:
Client-only rendering defers content and increases time to meaningful paint.

### RPR-023: Split vendor-heavy routes
Severity: MEDIUM

Rule:
Routes that include vendor libraries over 100 KB min+gzip must be split so the dependency is loaded only where needed.

Rationale:
Route-level code splitting reduces initial bundle size.

### RPR-024: No nested Suspense waterfalls
Severity: HIGH

Rule:
Nested `Suspense` boundaries must not serialize data fetching; child fetches must start before the parent resolves.

Rationale:
Serialized suspense boundaries create async waterfalls and delay rendering.

## Source of Truth
This agent enforces the rules defined in:
docs/rules/react-performance-rules.md
