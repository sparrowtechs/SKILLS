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

## Output Format

When using this guide, respond with:

1. Production context
2. Blocking readiness gaps
3. Operational weaknesses
4. Specific next actions
5. Production verdict: `Block`, `Revise`, or `Ready`
