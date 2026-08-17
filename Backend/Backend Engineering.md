# Backend Engineering

## Purpose

Build backends that are easy to reason about, hard to break, safe to change, and ready for real production conditions.

The goal is not:

> write code that merely passes tests, looks clean in isolation, or feels architecturally impressive.

The goal is:

> **Design and implement a backend that remains understandable, correct, operable, and trustworthy as real load, real failures, and real change hit it.**

Prioritize:

1. Correctness
2. Clear ownership
3. Operational reliability
4. Changeability
5. Security
6. Performance
7. Flexibility

Never reverse this order.

This skill is opinionated, but it is not dogmatic.

Do not cargo-cult Clean Architecture, DDD, hexagonal layers, CQRS, or microservices just because they sound mature. Use only the amount of structure the backend actually needs.

## Use This When

Use this skill when:

- designing a new backend or service
- reviewing a backend architecture or implementation
- tightening a backend that grew quickly and now feels fragile
- defining API behavior, integration behavior, or state change rules
- preparing a backend for production readiness work

Do not use this skill for:

- frontend-only work
- database-only tuning without backend design questions
- purely stylistic refactors
- security-only review with no general backend design concerns

## Modes

### 1. New Backend Design

Use when creating a backend, service, or major new subsystem.

Steps:

1. Define the backend's purpose, inputs, outputs, and trust boundaries.
2. Decide module boundaries and ownership of business logic, persistence, and integrations.
3. Define state transitions, failure behavior, and retry behavior.
4. Design the API, validation strategy, and operational model before polishing implementation details.
5. Review readiness, observability, and security before calling the design complete.

### 2. Backend Review

Use when reviewing an existing backend or pull request.

Steps:

1. Identify the backend's actual responsibilities.
2. Check whether boundaries, dependencies, ownership, and validation placement are clear.
3. Check API behavior, error behavior, and duplicate-execution handling.
4. Check production readiness, observability, and security companions.
5. Summarize the highest-value changes rather than listing every possible improvement.

### 3. API and Integration Design

Use when the main risk is API behavior or external system interaction.

Steps:

1. Define the contract, status semantics, and error shape.
2. Define idempotency, retries, pagination, and versioning behavior.
3. Define webhook, queue, and callback semantics explicitly.
4. Confirm failures remain diagnosable and safe under retry or duplication.

### 4. Production Hardening

Use when the backend mostly works but is not yet production-ready.

Steps:

1. Validate configuration, startup, shutdown, and recovery behavior.
2. Check observability, rollback, migration, and background work ownership.
3. Identify capacity-sensitive paths and operational blind spots.
4. Tighten security and deployment readiness before release.

## Core Principles

### 1. Start With Responsibilities

A backend should have a clear job.

Before deciding structure, define:

- what this backend owns
- what it does not own
- what state it changes
- what other systems it depends on
- what failures it must tolerate

If ownership is unclear, the codebase will blur around the same uncertainty.

### 2. Keep Boundaries Visible

Transport, business logic, persistence, and integrations should be easy to locate and reason about.

Do not force a reviewer to reconstruct the architecture by reading twenty files just to learn:

- where requests enter
- where rules are enforced
- where state changes happen
- where external calls leave the system

When the backend is large enough to need stronger internal structure, prefer modules or vertical slices around business capabilities rather than dumping unrelated behavior into generic layers.

### 3. Put Logic in the Right Place

Not all validation or logic belongs in the same layer.

Use transport and request handling to validate shape, format, and presence.

Use application or workflow code to orchestrate steps, permissions, and side effects.

Use domain code to enforce business invariants that must remain true regardless of transport, queue, or entry point.

If controllers become smart, services become god objects, or entities become empty data bags, the backend is drifting.

### 4. Design for Repeated Execution

Backends do not live in a perfect world.

Requests time out.
Queues redeliver.
Webhooks replay.
Clients retry.

State-changing operations must define:

- whether they are idempotent
- how duplicates are detected
- how retries behave
- what happens when work partially succeeds

If repeated execution is left implicit, the backend is not mature.

### 5. Make Failures Legible

A backend should fail in ways operators and developers can understand.

Prefer:

- explicit error contracts
- structured logging
- meaningful health signals
- diagnosable integration boundaries
- visible request, job, and trace identifiers

Avoid:

- silent fallback behavior
- ad hoc retries
- generic logs with no operational value
- errors that require guesswork to debug

### 6. Record Important Decisions

If a backend makes a non-obvious structural choice, record it while the context is still fresh.

Examples:

- why the service is modular monolith instead of microservices
- why a workflow is asynchronous instead of synchronous
- why a persistence model differs from the domain model
- why a queue, cache, or event bus exists

Use short architecture decision records or equivalent notes when the choice will matter again.

### 7. Make Change Local

A healthy backend lets you add or change behavior without touching unrelated parts of the system.

If every new feature forces changes across routing, validation, service logic, persistence, and background workers with no clear pattern, the backend is already accumulating drag.

### 8. Production Is Part of the Design

Do not treat production behavior as a later concern.

The backend design must account for:

- startup failure
- shutdown behavior
- rollback
- schema changes
- integration failure
- degraded dependencies
- operational ownership

If a system only works under happy-path development conditions, it is incomplete.

## Supporting Guides

Use these when you need deeper direction in one area:

- `Architecture/Backend Architecture.md`
- `API Design/Backend API Design.md`
- `Production/Backend Production Readiness.md`
- `../Security/Backend/Backend Security.md`

## Output Format

When using this skill, structure the response around:

1. Context
   - backend purpose
   - main responsibilities
   - important boundaries
2. Key Risks or Weaknesses
   - ownership problems
   - API or integration problems
   - operational problems
   - security or readiness problems
3. Recommended Changes
   - what to simplify
   - what to separate
   - what to define explicitly
   - what to harden before production
4. Final Direction
   - a short summary of how the backend should evolve

For backend reviews, prefer:

- what the backend is trying to do
- the highest-priority issues
- why they matter
- the clearest next fixes
- final backend verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep backend decisions mature as the system grows instead of only looking clean at first release.

### 1. Prefer Simpler Deployment Shapes Until Pressure Is Real

Do not split a system into more services, queues, or abstractions just because the pattern sounds advanced.

Earn extra complexity through real pressure such as:

- conflicting release cadence
- clearly different scaling needs
- stable ownership boundaries
- isolation requirements you can name concretely

### 2. Make Repeated Execution a First-Class Design Case

If the backend changes money, inventory, permissions, or workflow state, retries and duplicate delivery are core behavior, not edge behavior.

Design and review for repetition explicitly.

### 3. Separate Runtime Authority From Change Authority

The credentials and privileges needed to serve normal traffic should not be the same ones used for migrations, emergency repair, or platform administration.

Backends stay healthier when normal runtime power is narrow.

### 4. Force Important Tradeoffs Into the Open

When a backend depends on a non-obvious choice, such as sync versus async flow, modular monolith versus service split, or eventual consistency versus strong consistency, record the choice while it is still fresh.

Undocumented tradeoffs get rediscovered as accidental defects later.

### 5. Make Control Loops Explicit

If the backend depends on retries, queues, feature flags, rate limits, autoscaling, or circuit breakers, define who controls them and what they are allowed to do.

Operational controls should have:

- a clear owner
- explicit trigger conditions
- known rollback or abort behavior
- cleanup rules when they are temporary

If control loops exist only as scattered config, the backend will drift during incidents.

### 6. Measure Before You Optimize

Do not redesign architecture, add caching, split services, or tune concurrency because the system feels slow in theory.

Measure:

- the slow path
- the expensive query
- the queue that is backing up
- the payload that is too large
- the dependency that is stretching the response path

Real bottlenecks deserve design changes.
Imagined bottlenecks usually create unnecessary complexity.

### 7. Test the Seams That Carry Real Risk

The most important backend tests usually sit at the boundaries where state, retries, validation, permissions, and integrations meet.

Prefer tests that prove:

- business invariants stay true
- repeated execution stays safe
- APIs fail predictably
- workflows recover or compensate correctly
- dependencies can be swapped or simulated without rewriting business logic

## References Used To Shape This Guide

- Microsoft REST API Guidelines
- Martin Fowler guidance on architecture and evolutionary design
- Google SRE guidance on operability and production readiness
- Google SRE Workbook and OpenTelemetry guidance on reliability signals
- mature progressive-delivery guidance from systems such as LaunchDarkly and Unleash
