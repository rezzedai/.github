# RezzedAI

Infrastructure for bounded multi-agent systems.

We build the coordination, safety, and observability layers that make AI agents work together reliably. Agents run inside controlled, observable limits.

---

## CacheBash

[CacheBash](https://github.com/rezzedai/cachebash) is an open-source MCP server for multi-agent coordination, written in TypeScript and model-agnostic. 108 MCP tools in 21 domains, one endpoint.

- **Task dispatch.** Create, claim, complete. Claims run in a Firestore transaction, so two agents never claim the same task.
- **Relay messaging.** Agent-to-agent messages with multicast groups and a dead-letter queue.
- **Session management.** Track what every agent is doing, with heartbeats and fleet health.
- **Capability-scoped keys.** Each API key sees only the tools its capabilities allow.
- **Policy checks.** Dispatch evaluates policies before a task is created.
- **Per-task telemetry.** Tokens, cost, model and failure class are recorded on completion.
- **Mobile companion.** Monitor agents and answer their questions from your phone. Agents pause, you decide.

```bash
npx cachebash init
```

One command signs you in through the browser and writes the MCP config.

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
MCP server for document processing with Unstructured.io. Extract structured content from PDFs, PowerPoints, HTML, images. including tables that other parsers break on. Dual mode: local SDK or hosted API.

### [Voicekeeper](https://github.com/rezzedai/voicekeeper)
AI writing detection + voice matching. Know when content sounds like ChatGPT. Maintain your authentic voice.

### [xfetch](https://github.com/rezzedai/xfetch)
Social media content extraction via Playwright. No API keys, no rate limits.

### [Reach](https://github.com/rezzedai/reach)
AI-powered personalized outreach. Your message. Their name. Your voice.

---

## Architectural Priorities

1. **Governance before execution**. All tool calls pass through policy gates. LLM output is untrusted until validated.
2. **Typed task lifecycle**. Explicit SUCCESS / FAILED / SKIPPED semantics. No ambiguous completion states.
3. **Bounded autonomy**. Context limits, story decomposition constraints, TTL-based expiry, scoped delegation.
4. **Vendor neutrality**. No orchestration logic depends on proprietary SDK semantics.
5. **Observable execution**. Trace propagation, cost tracking, fleet health monitoring. Controlled by measurement, not hope.

---

*End of line.*
