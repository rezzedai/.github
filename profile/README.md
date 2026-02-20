# RezzedAI

Infrastructure for bounded multi-agent systems built on Claude.

RezzedAI contains the production-grade coordination, safety, and validation layers extracted from a persistent multi-agent orchestration system running on Claude Code.

The focus is not "agent autonomy."

The focus is controlled, observable execution.

---

## Context

The underlying system coordinates role-specialized Claude instances (Planner → Worker topology) through CacheBash, a custom MCP relay deployed on GCP Cloud Run.

Current scope:

- 650+ typed tasks within bounded multi-agent orchestration
- 3,500+ total tasks across orchestration + legacy systems
- Explicit WORK vs CONTROL task taxonomy
- Transactional task claiming with TTL-based relay containment
- Tool-boundary audit logging

This is CLI-based orchestration using Claude Code, not hosted public API traffic.

---

## Architectural Priorities

### 1. Governance Before Execution

All tool calls pass through policy gates prior to invocation.

Agents operate within:
- Identity-scoped permissions
- Context consumption limits
- Static token ceilings
- Rate limiting constraints
- Delegation boundaries (Planner cannot execute application code directly)

LLM output is treated as untrusted until validated.

### 2. Typed Task Lifecycle

Tasks are explicitly categorized:

- **WORK** — sprint stories, directives, builds
- **CONTROL** — ACKs, handoffs, system signals

This prevents activity inflation and allows clearer measurement of productive execution.

Lifecycle states are moving toward explicit SUCCESS / FAILED / SKIPPED semantics.

### 3. Bounded Autonomy

Runaway behavior is mitigated through:

- Context health monitoring (self-handoff at threshold)
- Story decomposition constraints (≤30% context per unit of work)
- TTL-based relay expiry with dead-letter handling
- Scoped subagent delegation
- Explicit identity isolation

Autonomy is allowed only within defined envelopes.

### 4. Vendor Neutrality

The relay infrastructure is intentionally decoupled from any specific provider SDK.

The builder tier supports pluggable model routing (Claude, Gemini, etc.) via adapter abstraction.

No orchestration logic depends on proprietary SDK semantics.

### 5. Telemetry Hardening (In Progress)

Active instrumentation work includes:

- Explicit completion semantics (SUCCESS / FAILED / SKIPPED)
- Retry classification
- Dynamic token budgeting
- Prompt/output provenance hashing
- Latency + cost rollups per task class

The goal is to move from "controlled by protocol" to "controlled by measurement."

---

## Public Infrastructure

### [Guardian](https://github.com/rezzedai/guardian)
Pre-tool-use policy gate for Claude Code sessions.

- Intercepts all tool invocations via hook integration
- Evaluates against configurable blocklist policies
- Tamper-proof audit trail with SHA256-chain integrity
- Budget enforcement with configurable breach actions
- Zero dependencies

### [SpecFirst](https://github.com/rezzedai/specfirst)
Confidence-scored planning workflow.

- 4-dimensional confidence scoring (Requirement Clarity, Implementation Certainty, Risk Awareness, Dependency Clarity)
- Threshold-based gating: proceed / flag / block
- Enforces decomposition prior to build
- Auto-scoping for trivial tasks

### [Dreamwatch](https://github.com/rezzedai/dreamwatch)
Overnight autonomous execution with safety guardrails.

- Budget caps with USD cost limits
- Git isolation — dedicated branch, never touches main
- Wall-clock timeout enforcement
- Auto-generated morning reports and PRs
- Graceful shutdown with state preservation

### [Dispatch](https://github.com/rezzedai/dispatch)
Minimal MCP task server for agent delegation.

- Transactional task lifecycle: pending → active → done
- Atomic operations via SQLite
- Works with any MCP client
- Zero configuration, no cloud dependency
- Core logic under 300 lines

---

## What This Org Represents

These repositories are the exposed infrastructure interfaces of a larger orchestration system.

The coordination relay, identity model, and governance framework remain private.

The goal is not maximal autonomy.

The goal is safe, measurable execution within boundaries that matter.

---

*End of line.*
