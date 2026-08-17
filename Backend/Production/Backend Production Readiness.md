# Backend Production Readiness

## Purpose

Use this guide to decide whether a backend is actually ready for production behavior: deployment, rollback, recovery, observability, capacity, and operational ownership.

## Use This When

Use this guide when:

- preparing a backend for launch
- reviewing a service that works locally but feels operationally thin
- tightening rollout, migration, or recovery behavior
- checking whether production safety is real or merely assumed

## Core Rules

### 1. Production Readiness Starts Before Deployment

If release, rollback, configuration, and recovery are undefined, the backend is not production-ready even if the code works.

### 2. Startup and Shutdown Must Be Predictable

The service should start, fail, stop, and restart in understandable ways.

Define:

- required runtime configuration
- startup validation behavior
- graceful shutdown behavior
- what happens to in-flight work on restart or crash

### 3. Stateful Change Requires a Rollout Plan

Schema changes, data migrations, queue contract changes, and cache-shape changes are production events, not implementation details.

If a release changes stored state, define:

- rollout order
- backward compatibility assumptions
- rollback limits
- recovery behavior when migration only partly succeeds

### 4. Observability Must Support Diagnosis

Production evidence should let operators answer:

- what failed
- where it failed
- which request, job, or trace is affected
- whether the issue is local or downstream

If logs and dashboards cannot answer those questions, the backend is still under-instrumented.

Useful production evidence usually includes:

- structured logs
- request, trace, or job identifiers
- dashboards for critical paths
- alerts tied to user-impacting failures
- runbooks for recurring incidents

### 5. Capacity Is Part of Correctness

A backend that only works at low load is not fully correct for its intended environment.

Identify:

- hot paths
- expensive queries
- fan-out operations
- queue pressure points
- timeout and pool limits

### 6. Ownership Must Be Explicit

Someone must own:

- on-call response
- release execution
- rollback decisions
- migrations
- background job behavior
- disaster recovery expectations

If ownership depends on tribal knowledge, production readiness is weaker than it looks.

### 7. Make Operational Decisions Visible

When the backend depends on a non-obvious production choice, write it down.

Examples:

- rollback limits after a schema migration
- reasons for queue concurrency values
- why a background job is synchronous or asynchronous
- why a dependency timeout is set the way it is

This keeps production behavior reviewable instead of institutional memory only.

### 8. Reliability Targets Must Shape Release Decisions

For user-critical paths, define what healthy behavior means in measurable terms.

That usually means:

- the signal you trust
- the target you are trying to hold
- the burn or failure condition that should stop a rollout
- who decides whether to continue, rollback, or repair forward

If the team cannot say what "too broken to keep shipping" means, release discipline is weak.

### 9. Progressive Delivery Needs a Kill Path and a Cleanup Path

Feature flags, canaries, staged rollouts, and dark launches can reduce release risk, but only when they are controlled deliberately.

Before relying on them, define:

- abort criteria
- kill-switch behavior
- monitoring during rollout
- when the temporary control will be removed

Flags and rollout controls that never get cleaned up become operational debt.

## Output Format

When using this guide, respond with:

1. Production context
2. Blocking readiness gaps
3. Operational weaknesses
4. Specific next actions
5. Production verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep production readiness tied to operational truth rather than to launch-day confidence.

### 1. Measure the Signals That Predict User Pain

A backend is not production-ready if nobody can answer quickly:

- how slow requests are
- how much traffic is arriving
- what is failing
- what resource is close to saturation

Track the operational signals that let the team see trouble before users explain it for you.

### 2. Make Rollback and Roll-Forward Explicit

Deployment safety depends on knowing which changes can be reverted, which require compensation, and which require forward repair.

If the release changes data or contracts, document the recovery path before deployment.

### 3. Test Degraded Conditions on Purpose

Production readiness is stronger when the team has seen the system under:

- slow downstream dependencies
- queue backlog
- partial startup failure
- missing configuration
- exhausted connection pools

If every check assumes normal conditions, readiness is overstated.

### 4. Tie Ownership to the Operational Surface

Alerts, dashboards, jobs, migrations, and recovery procedures should have clear owners.

A service is not ready if it can wake people up at night but nobody clearly owns the fix path.

### 5. Use Reliability Targets and Burn Alerts for Real Decisions

Reliability targets should not live only in a slide deck or dashboard.

If a path is important enough to protect, define the indicator, the target, and the burn condition that should change release behavior.

Otherwise the system has telemetry, but not operational discipline.

### 6. Treat Feature Flags as Temporary Operational Controls

Release flags, kill switches, and staged rollout controls should have:

- a purpose
- an owner
- a removal point
- a documented fallback behavior

Permanent flag debt makes production behavior harder to reason about.

### 7. Profile Before You Tune

When a backend is slow or expensive, prove the bottleneck before changing architecture, concurrency, caching, or infrastructure shape.

Use profiling, query evidence, and load testing to show where time or resource is actually being spent.

## References Used To Shape This Guide

- Google SRE guidance on golden signals and service operability
- Google SRE Workbook guidance on SLIs, SLOs, and error budgets
- OpenTelemetry guidance on traces and production telemetry
- practical rollback and progressive delivery guidance
- production reliability practices from mature backend platform teams
