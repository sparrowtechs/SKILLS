# Backend Architecture

## Purpose

Use this guide to shape and review backend architecture: service boundaries, module ownership, dependency direction, workflow design, and the choices that determine whether a system stays understandable over time.

## Use This When

Use this guide when:

- defining a new service or backend boundary
- reviewing whether a backend is too coupled or too scattered
- splitting or merging service responsibilities
- deciding where logic, persistence, and integrations should live

Do not treat every backend as if it needs the heaviest possible architecture. Small CRUD-heavy systems often need clearer boundaries more than they need more abstractions.

## Core Rules

### 1. Give Every Service a Clear Job

If a service has blurry ownership, every downstream decision gets weaker.

Define:

- what this service owns
- what data it owns
- what it is allowed to change
- what it reads from others
- what it should never become responsible for

If the boundary is still fuzzy, the service boundary is probably premature.

### 2. Prefer Clear Boundaries Over Clever Abstractions

A backend is easier to change when a reviewer can answer quickly:

- where requests enter
- where rules are enforced
- where state changes happen
- where external dependencies are called

Do not hide the architecture behind generic utility layers or framework ceremony.

When the backend is large enough, group behavior by module, domain capability, or vertical slice so that code that changes together stays near each other.

### 3. Avoid Chatty Backends

If a normal request requires multiple synchronous downstream calls just to assemble an answer, the system becomes slower, harder to debug, and easier to break.

Prefer:

- clear service ownership
- local authority over owned data
- deliberate aggregation points when needed

Be suspicious of architectures that look elegant in diagrams but require excessive request hopping in practice.

### 4. Keep Dependency Direction Understandable

Dependency direction should be obvious enough that engineers can predict the impact of change.

Avoid:

- circular dependencies
- business rules spread across unrelated layers
- shared modules that quietly become a second application

If you use ports, adapters, facades, or mediators, use them to clarify direction and ownership, not to create ceremony.

### 5. Design State Changes Explicitly

Important state transitions should not emerge accidentally from side effects.

Define:

- the event or request that triggers the change
- the owner of the change
- what happens on partial failure
- what happens on repeated execution

If a workflow spans multiple modules or services, define the handoff points and failure semantics explicitly.

### 6. Keep Change Local

Good architecture reduces the blast radius of normal changes.

If every feature requires touching transport, orchestration, persistence, jobs, and integrations with no obvious pattern, the structure is already working against the team.

### 7. Write Down the Decisions That Will Be Re-Litigated

The more important the architecture choice, the more likely the team will revisit it later.

Record the reasoning for:

- service boundaries
- shared database choices
- sync versus async workflows
- event-driven versus request-driven coordination
- persistence model tradeoffs

A short ADR is usually enough.

## Output Format

When using this guide, respond with:

1. Architecture context
2. Boundary and ownership problems
3. Coupling and dependency problems
4. Refactoring directions
5. Architecture verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep architecture grounded in real system pressures instead of diagram quality.

### 1. Choose Service Boundaries for Ownership, Not Fashion

Do not split by technical layer, team preference alone, or the desire to look distributed.

Prefer boundaries that match business capability, data ownership, and change cadence.

### 2. Be Suspicious of Shared Write Authority

If multiple modules or services can write the same important state without a clear owner, the boundary is weak no matter how clean the code layout looks.

### 3. Count the Cost of Every Network Hop

Every extra service boundary adds failure handling, latency, deployment coordination, observability work, and on-call load.

If the system pays that tax without gaining meaningful independence, the structure is too fragmented.

### 4. Make the Recovery Story Match the Architecture Story

Ask how the system behaves when one dependency is slow, unavailable, or partially updated.

Architecture is not mature if it only reads well under happy-path diagrams.

### 5. Make Long-Running Workflows Explicit and Recoverable

If work spans multiple modules, queues, or services, define:

- who owns the workflow
- what state is checkpointed
- which steps may retry
- which steps need compensation
- how stuck work is detected

Async architecture becomes fragile when the recovery path is only implied.

## References Used To Shape This Guide

- Martin Fowler guidance on monolith-first and architectural evolution
- Sam Newman guidance on service boundaries and independent deployability
- practical ADR guidance for recording important architecture choices
- domain-driven design guidance on bounded contexts and ownership
