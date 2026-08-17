# Backend API Design

## Purpose

Use this guide to design and review backend APIs so they remain predictable under real consumers, retries, failures, and long-lived integrations.

## Use This When

Use this guide when:

- defining a new HTTP or RPC API
- reviewing an inconsistent or fragile existing API
- improving retries, webhook handling, or error semantics
- deciding versioning, pagination, or compatibility behavior

## Core Rules

### 1. Make the Contract Obvious

A good API should let consumers predict behavior without guesswork.

Define clearly:

- what each endpoint does
- what each method means
- what success looks like
- what failure looks like
- what changes are safe to make later

The contract should help consumers build reliable clients without private knowledge of your implementation.

### 2. Let Status Codes and Methods Mean What They Normally Mean

Do not make clients learn a private dialect of HTTP.

Prefer:

- methods that match the behavior they trigger
- status codes that reflect actual outcomes
- explicit validation failures

Avoid:

- `200` responses that actually represent failure
- action semantics hidden behind inconsistent routes
- retry behavior that depends on undocumented side effects

For long-running work, do not pretend the operation finished when it has only been accepted. Model asynchronous behavior honestly.

### 3. Design for Retry From the Start

Clients retry.
Networks fail.
Webhooks replay.

State-changing API behavior must define:

- whether it is idempotent
- how duplicate requests are recognized
- how ambiguous failure is resolved
- what retry-safe behavior means for clients

If retries are not designed intentionally, the API is incomplete.

If POST is used for creation or commands, define repeatability explicitly instead of assuming clients will never retry.

### 4. Make Errors Useful

Error handling is part of the API contract.

Prefer:

- a consistent error envelope
- machine-readable error codes
- clear validation errors
- no leaked internal implementation detail

If the client cannot tell what went wrong, whether the request is safe to retry, or how to correct the input, the error contract is still weak.

### 5. Keep Evolution Visible

APIs live longer than teams expect.

Define:

- versioning strategy
- backward-compatible change rules
- deprecation behavior
- how consumers learn about breaking changes

An API version should be adoptable without hidden behavior shifts.

### 6. Treat Webhooks and Async Flows as First-Class Contracts

Async behavior is not secondary behavior.

For webhooks, callbacks, or queue-driven APIs, define:

- duplicate delivery behavior
- verification rules
- ordering assumptions
- eventual-consistency expectations

### 7. Validate at the Boundary

Request validation belongs at the API boundary, before bad input can leak deeper into the system.

Validate:

- required fields
- supported content types
- parameter formats
- header requirements
- request size and complexity limits

Fail clearly and early when the request contract is broken.

## Output Format

When using this guide, respond with:

1. API context
2. Contract problems
3. Retry and async behavior problems
4. Specific fixes
5. API design verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep API design stable under long-lived client use instead of only under fresh internal knowledge.

### 1. Make the Contract Honest About State

Do not return "success" when work was only accepted, partially completed, or failed downstream.

The API should tell the truth about what has happened so clients can behave safely.

### 2. Design Errors for Machines and Humans

Clients need machine-readable codes and predictable structure.

Operators and integrators need messages that explain what failed without exposing internals.

If either side has to guess, the contract is still weak.

### 3. Assume Clients Will Retry Imperfectly

Some clients retry too soon, some retry forever, and some retry after losing the original response.

Define idempotency, conflict behavior, pagination stability, and async completion rules so the API stays usable under messy real traffic.

### 4. Make Compatibility a Deliberate Policy

Versioning is not enough by itself.

Also define:

- what changes are backward compatible
- how deprecations are announced
- how long old clients are supported
- what consumers can rely on staying stable

## References Used To Shape This Guide

- Microsoft REST API Guidelines
- RFC-style API error and HTTP semantics guidance
- production API practices shaped by long-lived public APIs such as Stripe
