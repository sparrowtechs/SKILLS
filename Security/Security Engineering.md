# Security Engineering

## Purpose

Build products and systems that remain hard to misuse, hard to expose by accident, and hard to escalate when something goes wrong.

The goal is not:

> bolt on a final security pass, satisfy a checklist mechanically, or rely on vendors and frameworks to save a weak design.

The goal is:

> **Design, implement, and ship systems where trust boundaries are explicit, privileges stay narrow, dangerous defaults are removed, and security failures are caught before they become incidents.**

Prioritize:

1. Broken access prevention
2. Trust boundary clarity
3. Least privilege
4. Safe handling of secrets and sensitive data
5. Secure defaults
6. Detection and recovery
7. Convenience

Never reverse this order.

This skill is opinionated, but it is not compliance theater.

Do not treat security headers, scanners, frameworks, or cloud defaults as proof that the system is secure. They help, but they do not replace security decisions made in the product, backend, data model, and deployment path.

## Use This When

Use this skill when:

- designing a new product, API, backend, or internal tool
- reviewing whether a system is safe enough to ship
- tightening a project that was built quickly and now needs real security discipline
- deciding how auth, authorization, secrets, data handling, and deployment controls should work
- reviewing a change that crosses a trust boundary

Do not use this skill for:

- legal or compliance advice
- incident response runbooks
- forensic investigation after compromise
- purely stylistic code review with no security relevance

## Modes

### 1. New System Design

Use when designing a new application or major subsystem.

Steps:

1. Identify trust boundaries, privileged actions, and sensitive data.
2. Decide where authentication, authorization, validation, and secrets handling live.
3. Reduce privileges, public exposure, and unnecessary data collection before implementation grows around them.
4. Define failure behavior, logging, and operational visibility before release.

### 2. Security Review

Use when reviewing an existing system, milestone, or pull request.

Steps:

1. Identify the real attack surfaces.
2. Check access control, validation, secrets handling, and exposed operations first.
3. Check whether security is enforced at the correct boundary instead of implied by the UI or deployment story.
4. Summarize the highest-risk issues and the shortest path to reducing them.

### 3. Pre-Launch Hardening

Use when a system mostly works and needs to be made safer before release.

Steps:

1. Check deployment, configuration, and secret handling.
2. Check browser-facing, API-facing, data-facing, and storage-facing controls.
3. Remove unsafe defaults, debug paths, and over-broad privileges.
4. Verify the deployed environment directly, not only the code.

### 4. Surface-Specific Review

Use when the review needs to go deep on one area.

Surfaces:

- deployment
- backend
- frontend
- database
- storage

Use the supporting guides below for those cases.

## Core Principles

### 1. Security Starts at Trust Boundaries

Security problems usually appear where one trust level meets another:

- browser to server
- public request to internal logic
- application to database
- worker to storage
- service to third-party integration
- admin action to user-owned data

Make those boundaries visible before you try to harden them.

### 2. Enforce on the Side That Can Actually Stop the Action

A control only counts if it exists where the action can be blocked.

That means:

- authorization on the server, not only in the UI
- storage policy at the storage layer, not only in app intent
- database privilege limits at the database or identity layer, not only in code comments
- secret protection in runtime systems, not only in local discipline

If a client, hidden button, or convention is the main thing preventing abuse, the control is weak.

### 3. Prefer Narrow Privilege and Narrow Exposure

Security gets worse as scope gets broader.

Prefer:

- short-lived credentials
- per-service identities
- minimal database roles
- private-by-default storage
- restricted admin surfaces
- tightly scoped signed URLs and tokens

Broad access usually survives longer than intended.

### 4. Treat Input as Hostile and Output as Dangerous

Validate untrusted input at the boundary before it reaches deeper logic.

Encode, sanitize, or isolate dangerous output before it reaches a browser, shell, template engine, or downstream system.

Do not trust:

- file types reported by the client
- hidden form fields
- IDs from URLs
- callback URLs
- webhook payloads
- content rendered as rich text

### 5. Minimize Secrets and Sensitive Data

The safest secret is the one you never issued.
The safest sensitive field is the one you never collected.

Reduce:

- number of secrets
- lifespan of secrets
- places secrets can appear
- number of systems holding sensitive data
- copies of production data outside production

### 6. Assume Replays, Retries, and Partial Failure

Attackers are not the only source of repetition.

Browsers retry.
Clients reconnect.
Workers redeliver.
Webhooks replay.
Deployments partially fail.

Security-sensitive behavior must define what happens when the same action is attempted again, interrupted, or only partly completed.

### 7. Make Detection Useful Without Leaking More

Logs and alerts should help operators see abuse and failure without creating a second security problem.

Prefer:

- auth and access-denial audit trails
- alerting on unusual failure patterns
- request, job, and trace correlation
- no passwords, tokens, raw secrets, or oversized personal payloads in logs

### 8. Write Down Exceptions

If a risky decision remains in place, document:

- what the exception is
- why it exists
- who owns it
- how long it will remain
- what follow-up is required

Undocumented exceptions turn into permanent exposure.

## Supporting Guides

Use these when you need deeper direction in one area:

- `Deployment/Deployment Security.md`
- `Backend/Backend Security.md`
- `Frontend/Frontend Security.md`
- `Database/Database Security.md`
- `Storage/Storage Security.md`

## Output Format

When using this skill, structure the response around:

1. Context
   - system or surface reviewed
   - trust boundaries
   - sensitive data or privileged actions involved
2. Key Risks
   - access control risks
   - exposure risks
   - data handling risks
   - deployment or operational risks
3. Recommended Changes
   - what to restrict
   - what to validate
   - what to remove
   - what to harden before launch
4. Final Direction
   - a short summary of how the system should become safer

For security reviews, prefer:

- what the system is trying to protect
- the highest-priority risks
- why they matter
- the clearest next fixes
- final security verdict: `Block`, `Revise`, or `Ready`

## Durability Checks

Use these checks to keep the work durable over time instead of treating security as a one-time review artifact.

### 1. Reduce Exposure Before You Add Controls

The cheapest security control is often removing the exposure entirely.

Prefer:

- fewer public entry points
- fewer privileged roles
- fewer long-lived secrets
- fewer stored copies of sensitive data
- fewer third-party dependencies with broad access

If the system can become safer by removing a surface, do that before layering more policy on top of it.

### 2. Treat the Build Path as Part of the Security Model

Production risk does not start at runtime.

Dependencies, CI pipelines, package registries, build agents, artifact storage, and deployment credentials all affect whether the shipped system can be trusted.

If the release path is easy to poison, bypass, or over-privilege, the product is not secure even if the application code looks disciplined.

### 3. Verify Controls by Trying the Wrong Thing

A control is stronger when it has survived misuse, not when it merely exists in configuration.

Check whether the system still holds when someone:

- changes IDs or tenant identifiers
- retries the same operation
- replays a webhook
- uploads the wrong type of file
- calls an internal-looking endpoint from the outside
- uses an expired, missing, or downgraded credential

Security confidence should come from failed abuse paths, not from documentation alone.

### 4. Keep Security Decisions Close to Ownership

Security weakens when critical decisions are spread across unclear owners.

Every meaningful exception or exposure should have:

- a named owner
- a reason it exists
- a review point
- a path to removal or replacement

If nobody clearly owns a risk, the risk is already growing.

## References Used To Shape This Guide

This guide is intentionally shorter than the source material behind it, but it is shaped primarily by durable security references, especially:

- OWASP ASVS
- OWASP Cheat Sheet Series
- OWASP Secure by Design Framework
