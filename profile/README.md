# RezzedAI

Infrastructure for bounded multi-agent systems.

We build the coordination, safety, and observability layers that make AI agents work together reliably. Not "agent autonomy" — controlled, observable execution.

---

## CacheBash

**The coordination layer between your AI coding agents and your phone.**

[CacheBash](https://github.com/rezzedai/cachebash) is an MCP server that gives AI agents task queues, messaging, session tracking, and human-in-the-loop approvals. 50+ tools, 12 modules, one endpoint.

- **Task dispatch** — Create, claim, complete. Transactional claiming prevents double-work.
- **Relay messaging** — Agent-to-agent communication with multicast groups and dead-letter handling.
- **Session management** — Track what every agent is doing, heartbeats, progress monitoring.
- **Sprint orchestration** — Break work into stories, execute in waves, track completion.
- **Mobile companion** — Monitor and control your agents from your phone.
- **Human-in-the-loop** — Questions routed to mobile for approval. Agents pause, you decide.

```bash
npx cachebash init
```

One command. Browser auth. MCP config injected. Done.

[Documentation](https://docs.rezzed.ai) · [Get Started](https://docs.rezzed.ai/getting-started/quick-start)

---

## Safety & Governance

### [Guardian](https://github.com/rezzedai/guardian)
Pre-tool-use policy gate for Claude Code. Intercepts all tool invocations, evaluates against configurable policies, maintains tamper-proof audit trail. Zero dependencies.

### [SpecFirst](https://github.com/rezzedai/specfirst)
Confidence-scored planning. 4-dimensional scoring (Requirement Clarity, Implementation Certainty, Risk Awareness, Dependency Clarity) with threshold-based gating. Plan before you build.

### [Dreamwatch](https://github.com/rezzedai/dreamwatch)
Overnight autonomous execution with budget caps, git isolation, wall-clock timeouts, and auto-generated morning reports.

---

## Infrastructure Libraries

### [poll-hooks](https://github.com/rezzedai/poll-hooks)
Async work-polling with claim semantics and lifecycle hooks. The backbone of agent task consumption.

### [dual-auth](https://github.com/rezzedai/dual-auth)
Firebase Auth + API key dual authentication with AES-256 encryption utilities.

### [rate-gate](https://github.com/rezzedai/rate-gate)
Sliding window rate limiter with pluggable backends.

### [dispatch](https://github.com/rezzedai/dispatch)
Lightweight MCP task server. SQLite-backed, zero config, under 300 lines.

---

## Content & Analysis

### [Unstructured MCP Server](https://github.com/rezzedai/unstructured-mcp-server)
MCP server for document processing with Unstructured.io. Extract structured content from PDFs, PowerPoints, HTML, images — including tables that other parsers break on. Dual mode: local SDK or hosted API.

### [Voicekeeper](https://github.com/rezzedai/voicekeeper)
AI writing detection + voice matching. Know when content sounds like ChatGPT. Maintain your authentic voice.

### [xfetch](https://github.com/rezzedai/xfetch)
Social media content extraction via Playwright. No API keys, no rate limits.

### [Reach](https://github.com/rezzedai/reach)
AI-powered personalized outreach. Your message. Their name. Your voice.

---

## Architectural Priorities

1. **Governance before execution** — All tool calls pass through policy gates. LLM output is untrusted until validated.
2. **Typed task lifecycle** — Explicit SUCCESS / FAILED / SKIPPED semantics. No ambiguous completion states.
3. **Bounded autonomy** — Context limits, story decomposition constraints, TTL-based expiry, scoped delegation.
4. **Vendor neutrality** — No orchestration logic depends on proprietary SDK semantics.
5. **Observable execution** — Trace propagation, cost tracking, fleet health monitoring. Controlled by measurement, not hope.

---

*End of line.*
