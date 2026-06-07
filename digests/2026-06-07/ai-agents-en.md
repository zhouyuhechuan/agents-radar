# OpenClaw Ecosystem Digest 2026-06-07

> Issues: 294 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-07 02:50 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-07

## 1. Today's Overview

OpenClaw remains in an intense development cycle, with **294 issues** and **500 pull requests** updated in the past 24 hours, plus **99 PRs merged or closed**. Two new beta releases (v2026.6.5-beta.1 and v2026.6.5-beta.2) landed, containing critical fixes for QQBot thinking-content leakage and MCP tool result coercion. Despite strong forward momentum, the project is grappling with several regressions introduced in recent stable versions—particularly around the OpenAI/ChatGPT Responses transport and the Codex app-server turn-completion path. Community engagement is high, with multiple "platinum hermit"–severity bugs attracting lengthy comment threads and reactions.

## 2. Releases

Two new versions were published today:

- **v2026.6.5-beta.2** — Includes the QQBot thinking-strip fix (issues #89913, #90132) and improved MCP tool result coercion for `resource_link`, `resource`, `audio`, and malformed image payloads.
- **v2026.6.5-beta.1** — Same core changes as beta.2 (truncated release notes), marking the beginning of this beta cycle.

**Migration notes**: These are beta releases; users on the `latest` npm dist-tag should not receive them automatically. No breaking changes or required migrations are noted beyond standard beta precautions.

## 3. Project Progress

Today saw **99 pull requests merged or closed**, reflecting steady churn across the codebase. Among open PRs close to landing (status `ready for maintainer look`):

- **PR #91057** — `fix(sessions): prune stale gateway model-run sessions` — adds a configurable retention period for model-run probe sessions, preventing unbounded accumulation.
- **PR #90903** — `fix(agents): inherit default agent model catalog for secondary agents` — resolves a `FailoverError` when secondary non-default agents use Google/Gemini models without explicit catalog population.
- **PR #90741** — `perf(models-config): unify auth-profile fingerprint cache + targetProvider short-circuit` — supersedes two older PRs to reduce overhead in provider resolution.
- **PR #89045** — `fix: recover terminal session status on visible inbound turns` — prevents group chat sessions stuck in `failed` from silently dropping messages.

Other notable open PRs address broader areas: browser MCP capability expansion (#85993), policy coverage for exec approvals (#90003), and runtime self-context configuration (#90101).

## 4. Community Hot Topics

The most active issues by comment count:

- **Issue #90083** (14 comments, 3 👍) — `[Bug]: 2026.6.1 OpenAI ChatGPT Responses transport fails with invalid_provider_content_type for gpt-5.4/gpt-5.5`. Users report a `causeCode=invalid_provider_content_type` error after upgrading, breaking inference for OpenAI’s latest models.
- **Issue #67035** (14 comments) — `[Bug]: 2026.4.14 Windows chat UI regression` — input text swallowed, streamed replies often invisible. Closed but still generating discussion.
- **Issue #88312** (13 comments, 3 👍) — `[Regression] Codex app-server turn-completion stall returns` — a known fix (#85107) apparently reverted or incomplete; multi-tool agent turns reliably fail.
- **Issue #88929** (11 comments, 2 👍) — `Feishu streaming card: abnormal typewriter effect and final content truncated to last character` — a channel-specific bug causing severe display issues for Feishu users.
- **Issue #73424** (10 comments) — `image tool: 'Failed to optimize image' error` — closed as stale but still gathering reports.

**Underlying needs**: Users are demanding reliable multi-provider support (especially for the newest OpenAI and DeepSeek models), stable chat UI across platforms, and channel-specific polish (Feishu, Telegram). The recurring theme of regressions suggests the project’s rapid iteration is outpacing thorough regression testing.

## 5. Bugs & Stability

Several critical and high-severity bugs were reported or updated today:

| Issue | Title | Severity | Fix PR? |
|-------|-------|----------|---------|
| #91018 | ⚠️ Upgrade 2026.6.1 broke DeepSeek prompt cache - $6 burned in one hour | **P1** (financial impact) | None identified |
| #90991 | Cron scheduled trigger contaminates global runtime state causing transient system-wide overload failures | **P1** | None identified |
| #90925 | Subagent announce compaction for Codex/OAuth falls into openai-responses API-key route | **P1** (routing regression) | None identified |
| #90886 | gateway hangs at `[gateway] starting...` when a declared provider lacks credentials (regression v2026.4.8 → v2026.4.26) | **P1** (startup failure) | None identified |
| #90595 | Cron run "failed" notifications fire during hot reload and during retries, causing alert fatigue | **P2** | None identified |
| #90428 | exec tool triggers gateway SIGTERM restart on WSL2 with Node 24 | **P2** | None identified |

**Analysis**: The DeepSeek prompt cache break (#91018) has direct cost consequences, making it a likely priority. The cron runtime contamination (#90991) and gateway hang (#90886) affect server stability. None of these currently have linked fix PRs, though the project’s high PR velocity suggests fixes may be in flight.

## 6. Feature Requests & Roadmap Signals

Several feature requests garnered community traction this week:

- **Issue #90916** (6 comments, 1 👍) — `Topic-session families for one assistant across multiple named context lanes` — proposes isolated context lanes per topic while sharing durable memory. Likely influenced by user demand for multi-role or multi-context assistants.
- **Issue #89265** (5 comments, 1 👍) — `More local providers` — argues for first-class local model support as open-weight models improve. Signals a shift toward self-hosted deployments.
- **Issue #90354** (4 comments) — `Add bounded/validated append semantics for pre-compaction memory flush` — aims to prevent model-generated noise from corrupting memory files.
- **Issue #11955** (4 comments) — `Memory/Context Improvements` — a long-standing meta-issue covering agent self-evaluation, global semantic search, and conversation chaining.
- **Issue #45508** (4 comments) — `Self-hosted STT/TTS provider support in webchat` — requests routing voice I/O through the gateway instead of browser Speech API.
- **Issue #58818** (6 comments, 2 👍) — `Guarantee last N raw messages in agent context (survive compaction and session reset)` — addresses agent memory persistence, a common pain point.

**Prediction for next version**: Topic-session families (#90916) and local provider improvements (#89265) have active discussion and clear use cases. Given the project’s focus on agent flexibility, these may appear in an upcoming minor release.

## 7. User Feedback Summary

Real pain points from the community include:

- **Financial impact**: DeepSeek prompt cache broken after upgrade (#91018) costing $6/hour.
- **Channel-specific UI regressions**: Feishu card truncation (#88929) and Windows webchat input loss (#67035) degrade daily workflows.
- **Server stability**: Cron cronjobs causing global overload (#90991) and gateway hang on misconfiguration (#90886) disrupt production setups.
- **Codex/OAuth routing**: High-context codex sessions fail mid-turn (#90925) and subagent compaction routes to wrong API key path.
- **Approval and alert fatigue**: In-flight approvals lost on gateway restart (#64664) and cron failure notifications spamming during hot reload (#90595).

**Satisfaction signals**: The new beta releases address QQBot thinking leakage and MCP results, suggesting responsive maintainers. Users also appreciate the quick release cadence.

## 8. Backlog Watch

Several important issues and PRs have been waiting for maintainer attention for weeks or months:

- **Issue #49603** (opened March 18) — `Orphaned lock files not cleared on gateway restart when PID matches current process` — **P1**, no fix PR.
- **Issue #43015** (opened March 11) — `message.send schema overexposes poll/components/modal` — **P1**, linked PR open but stalled.
- **Issue #57256** (opened March 29) — `openclaw status falsely reports openclaw-mem0 memory as unavailable` — **P2**, linked PR open but needs review.
- **Issue #58818** (opened April 1) — `Guarantee last N raw messages in agent context` — **P2**, no decision.
- **Issue #62615** (opened April 7) — `Add gateway-side circuit breaker for unhealthy sessions` — **P2**, no decision.
- **Issue #64267** (opened April 10) — `OpenClaw 2026.4.9 exposes agent internal thinking (English) to user` — **P1**, no fix.
- **Issue #64664** (opened April 11) — `Approvals lost on gateway restart` — **P2**, product decision pending.
- **Issue #69327** (opened April 20) — `Subagent sandbox does not propagate sandbox.docker.env and may reuse stale state` — **P2**, needs product decision and security review.
- **Issue #71491** (opened April 25) — `Kimi K2.6 reasoning_content 400 regression in long conversations after LCM compaction` — **P1**, linked PR open but not merged.

**PRs needing maintainer look**:  
- **PR #85155** (May 22) — `fix(agents): avoid inviting provider swaps in model alias guidance` — ready for review but waiting.
- **PR #78441** (May 6) — `feat(subagents): forward toolsAllow from sessions_spawn` — ready and important for agent policy control.

These items represent a backlog that could benefit from dedicated triage sessions to close or advance them, especially given their severity or long inactivity.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-06-07

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing a phase of intense differentiation and rapid iteration. Projects are converging on a core set of requirements—multi-provider support, channel integration, plugin/MCP extensibility, and robust memory management—while diverging sharply in architectural philosophy (monolithic vs. modular, runtime environments, target deployment sizes). The ecosystem shows clear stratification into three tiers: hyper-active core platforms (OpenClaw, ZeroClaw) with hundreds of daily contributions; mid-tier focused projects (NanoBot, Hermes Agent, PicoClaw) with steady feature velocity; and lower-activity projects (Moltis, CoPaw, ZeptoClaw) that are either stabilizing or building toward specific milestones. A notable trend is the emergence of specialized sub-projects for trading (PicoClaw's ClawTrade) and embedded/constrained deployments (ZeptoClaw's binary-size governance), indicating maturation beyond general-purpose chat agents.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | Release Today | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 294 | 500 | 99 | ✅ v2026.6.5-beta.1 & beta.2 | High velocity, 2 beta releases, critical regressions under active triage |
| **ZeroClaw** | 39 | 50 | ~7 (7 S0/S1 bugs closed) | ❌ | Very high activity, 3 concurrent milestone trackers, strong stability focus |
| **Hermes Agent** | 50 | 50 | 8 merged, 10 issues closed | ❌ | Healthy churn, broad community engagement, macOS challenges |
| **NanoBot** | 7 | 24 | 10 | ❌ | Moderate but focused; long-standing features finally merging |
| **PicoClaw** | 12 | 18 | 15 | ✅ v0.2.9-nightly | High merge rate; defensive fixes + new trading module signal growth |
| **NanoClaw** | 2 | 14 | 3 | ❌ | Low activity; Signal adapter and Slack fixes pending for weeks |
| **LobsterAI** | 6 | 2 | 2 | ❌ | Steady but slow; 5 stale bugs from April still unresolved |
| **CoPaw** | 11 | 0 | 0 (2 issues closed) | ❌ | Bug-report-heavy day; v1.1.10 introduced critical regressions |
| **IronClaw** | 2 | 31 | 10 | ❌ | Core team focused on Reborn architecture; CI issue lingering 11 days |
| **ZeptoClaw** | 2 | 1 | 0 (1 issue closed) | ❌ | Low activity, focused CI/tooling; no runtime bugs |
| **Moltis** | 3 | 0 | 0 | ❌ | Minimal activity; 3 new issues, no maintainer responses |
| **NullClaw** | 0 | 0 | 0 | ❌ | **No activity in 24h** |
| **TinyClaw** | 0 | 0 | 0 | ❌ | **No activity in 24h** |

**Health Score (subjective):**
- **Hyper-active:** OpenClaw, ZeroClaw
- **Active & Stable:** Hermes Agent, NanoBot, PicoClaw
- **Moderate / Bug-Fix Phase:** IronClaw, LobsterAI, CoPaw, NanoClaw
- **Stable / Low:** ZeptoClaw, Moltis
- **Inactive:** NullClaw, TinyClaw

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Scale:** 294 issues + 500 PRs in 24h is ~6x ZeroClaw (next largest) and an order of magnitude above most peers
- **Release cadence:** Two beta releases today, indicating mature CI/release infrastructure
- **Community engagement:** "Platinum hermit"–severity bugs attract deep comment threads; users financially impacted (DeepSeek cache bug costing $6/h) receive rapid attention
- **Provider support:** Explicit fixes for OpenAI gpt-5.x, DeepSeek, QQBot, Feishu—breadth unmatched

**Technical approach differences:**
- OpenClaw is the **core reference implementation** of the Claw protocol family, meaning most other projects (PicoClaw, NanoClaw, ZeptoClaw, ZeroClaw, NullClaw) derive from or interoperate with it
- Uses a **gateway + session + agent model** with heavy emphasis on MCP tool integration and provider federation
- Employs a **centralized runtime** compared to NanoBot's SDK-based model or PicoClaw's Go/goroutine architecture

**Community size comparison:**
- OpenClaw's community is self-sustaining with hundreds of active contributors; the beta release discussion alone dwarfs most projects' total activity
- Only ZeroClaw approaches OpenClaw in volume, but from a smaller user base (39 issues vs 294)

**Weakness:** Regressions from rapid iteration outpace regression testing, creating trust issues for production users (3 P1 regressions open today).

---

## 4. Shared Technical Focus Areas

**1. Multi-Provider Reliability & Cost Management** (All active projects)
- OpenClaw: DeepSeek prompt cache broken (#91018, $6/h)
- Hermes Agent: Gemma4 + Ollama max token issue (#39281), openai-codex proxy routing (#40913)
- NanoBot: OpenAI image params incompatibility (#4167), GitHub Copilot OAuth login failure (#2573)
- ZeroClaw: Subscription-native OAuth for Ollama Cloud, Kimi, MiniMax (#5601)

**2. Context & Memory Management** (OpenClaw, NanoBot, ZeroClaw, CoPaw, LobsterAI)
- OpenClaw: Topic-session families (#90916), last N raw messages guarantee (#58818)
- NanoBot: Max messages truncation defeats prompt caching (#4222)
- CoPaw: /compact command ignores model's max_input_length (#4937)
- LobsterAI: Memory compression not working after upgrade (#4661)
- *Need:* Configurable, reliable context management that respects model limits and user intent

**3. Channel-Specific Polish & Regressions** (OpenClaw, Hermes Agent, CoPaw, NanoBot, NanoClaw)
- OpenClaw: Feishu streaming card truncation (#88929), Telegram edit flood
- Hermes Agent: Slack formatting, QQ bot CPU spin, Discord identity
- CoPaw: WeChat Work tool integration broken (#4990)
- NanoBot: WhatsApp bridge fixes, Signal adapter issues
- *Need:* Reliable, production-grade IM channel support across platforms

**4. Plugin & MCP Ecosystem Expansion** (OpenClaw, ZeroClaw, NanoClaw, NanoBot)
- OpenClaw: MCP tool result coercion fix, browser MCP capability expansion (#85993)
- ZeroClaw: WASM plugin infrastructure (sandbox, namespace, registry), 7 new plugin PRs today
- NanoClaw: HTTP/SSE MCP transport (#2208), Google Contacts MCP skill (#2693)
- NanoBot: Per-MCP-server allowFrom access control (merged #2533)
- *Need:* Secure, portable plugin architectures with sandboxing and access controls

**5. Authentication & Identity Federation** (OpenClaw, ZeroClaw, NanoBot, Hermes Agent)
- ZeroClaw: OIDC authentication (#7141), OAuth for additional providers
- NanoBot: GitHub Copilot Enterprise support (#4220)
- OpenClaw: OAuth routing regression (#90925)
- *Need:* Enterprise-grade auth (SSO, OIDC) and native OAuth flows for self-hosted deployments

**6. Cron & Background Automation** (OpenClaw, NanoBot, ZeroClaw, Moltis, Hermes Agent)
- OpenClaw: Cron runtime state contamination (#90991), alert fatigue (#90595)
- NanoBot: Silent cron mode, WebUI cron management (#4218)
- ZeroClaw: Pre-hook skip gates for cron/SOP (#5607)
- Moltis: Cron notification suppression keyword (#1110)
- *Need:* Reliable, configurable, user-visible cron job management with proper isolation

**7. Security & Policy Hardening** (ZeroClaw, NanoBot, IronClaw, PicoClaw, ZeptoClaw)
- ZeroClaw: Path-guard false positives (#7133), secret redaction (#6978), session rehydration (#7252)
- NanoBot: ExecTool workspace isolation (#4221)
- PicoClaw: Type assertion safety, goroutine leak fixes
- ZeptoClaw: Binary-size governance for embedded security
- *Need:* Sandboxing, input validation, and policy enforcement at every layer

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | NanoBot | Hermes Agent | PicoClaw | CoPaw |
|---|---|---|---|---|---|---|
| **Target User** | Enterprise / power users | Plugin developers / embedders | Chat-first personal assistant | Knowledge workers / desktop | Quant traders / embedded | General consumer / chat |
| **Architecture** | Monolithic gateway + sessions | Modular plugin-host | SDK-based, multi-platform | Desktop + CLI + gateway | Go microservices | Python, channel-first |
| **Runtime** | Node.js (npm) | Python + WASM plugin runtime | Python | Python | Go | Python |
| **Plugin Model** | MCP tools | WASM plugins + MCP | Stdio MCP + built-ins | Plugin hooks + built-in tools | MCP + ClawHub messages | Channel adapters + skills |
| **Primary Channel** | QQ, Feishu, Discord, Telegram | Web dashboard + MCP servers | Discord, WhatsApp, Telegram | Desktop UI + CLI | Slack, Google Chat | WeChat, QQ, Telegram |
| **Memory Model** | Server-side session + durable memory | Durable session history | Per-user memory (merged today) | Goal + episode lifecycle | Unknown | Session-based compression |
| **Deployment** | Self-hosted (npm) | Self-hosted (Python) | Self-hosted (Python) | Desktop (DMG/Installer) + CLI | Embedded / ARM | Desktop (Windows/Mac) |
| **Key Differentiator** | Reference implementation, largest ecosystem | WASM plugin sandbox + rapid release cycle | Multi-user isolation, GitHub Copilot focus | Desktop-first, goal-orientated workflows | Low-latency trading + embedded | Channel coverage for Chinese users |

---

## 6. Community Momentum & Maturity

**Tier 1: Hyper-iteration (Rapidly evolving, high risk of regressions)**
- **OpenClaw** — 500+ PRs/day, 2 beta releases, 3 P1 regressions open. Self-sustaining community but stability concerns for production deployments.
- **ZeroClaw** — 50 PRs/day, 3 concurrent milestone trackers, 7 critical bugs closed today. Strong stability emphasis despite high velocity.

**Tier 2: Active Development (Steady feature delivery, manageable bug counts)**
- **Hermes Agent** — 50 issues + 50 PRs, 8 PRs merged, 10 issues closed. Broadest channel support among desktop-first projects. macOS compatibility is a recurring pain point.
- **NanoBot** — 24 PRs, 10 merged. SDG-focused, SDK-based. Merging long-standing features (per-user memory, MCP access control) signals maturity.
- **PicoClaw** — 18 PRs, 15 merged. Rapidly closing fixes; trading module is speculative but could attract a niche.

**Tier 3: Stabilization / Milestone Building (Lower activity, targeting specific goals)**
- **IronClaw** — Focused on Reborn architecture overhaul; 31 PRs but few from community. CI issue (#4108) may be blocking progress.
- **CoPaw** — Bug-report-heavy day (11 issues, 0 PRs). v1.1.10 introduced critical regressions that must be hotfixed.
- **NanoClaw** — 14 PRs, only 3 merged. Signal adapter fixes have been open for weeks; maintainer bandwidth appears constrained.

**Tier 4: Low Activity / Maintenance Phase**
- **LobsterAI** — 2 PRs merged, but 5 stale bugs from April. Need triage attention.
- **ZeptoClaw** — Stable, focused on CI improvements. Low risk, low community interaction.
- **Moltis** — 3 issues, no maintainer response. Project may be under-resourced.
- **NullClaw, TinyClaw** — No activity in 24h. Inactive or deprecated.

---

## 7. Trend Signals

**1. Cost-Aware Agent Architecture**
- Multiple projects (OpenClaw #91018, NanoBot #4222) report financial impacts from broken prompt caching or inefficient context management. AI agent developers should prioritize **predictable token consumption**, **transparent caching invalidation**, and **cost break-even alerts**. The era of "just call the API" is over—cost governance is becoming a first-class feature.

**2. Isolation & Sandboxing as Default**
- ZeroClaw's WASM sandbox, NanoBot's ExecTool workspace isolation, and PicoClaw's goroutine leek fixes signal a shift toward **defensive-by-default* architecture. Expect requirements for:
  - SSRF egress guards in MCP/plugin execution
  - Resource limits (CPU, memory) on tool runs
  - Session/process isolation (WASM, container, or OS-level)
  - Secret redaction from all user-facing surfaces

**3. Multi-User & Enterprise Multi-Tenancy**
- NanoBot merged per-user memory today; ZeroClaw has OIDC on roadmap; Hermes Agent sees demand for goal lifecycle hooks. The ecosystem is moving from single-user chat to **multi-tenant agent platforms** with:
  - Per-user memory isolation
  - Role-based access control for skills/tools
  - Enterprise SSO/OIDC integration
  - Shared vs. isolated context lanes (OpenClaw #90916)

**4. Local-First & Self-Hosted Models Ascending**
- OpenClaw (#89265) and CoPaw (#4989 local Qwen regression) both see demand for local model support. Developers want **offline-capable agents** that can fall back to local LLMs when cloud APIs are unavailable or too expensive. This implies investment in:
  - Ollama/vLLM integration standards
  - Cross-model context window negotiation
  - Local embedding and RAG pipelines

**5. Agent Identity & Emotional/State Exposure**
- Hermes Agent (#13529) requests "Agent Activity API & Emotional State Exposure." This is an early signal of demand for **observable, introspectable agents**—developers want to see agent confidence, reasoning traces, and internal state for debugging and orchestration. Expect growth in:
  - Structured logging of agent decision steps
  - Public APIs for agent-confidence scores
  - "Think-aloud" modes with controllable visibility

**6. Channel Convergence on Real-Time Protocols**
- Multiple projects are moving from webhook-based channel integration (HTTP) to real-time socket protocols: ZeroClaw's Telegram fixes, NanoClaw's Slack Socket Mode switch, OpenClaw's Feishu streaming card. Developers should **prefer real-time (WebSocket, SSE, Socket Mode) over polling/webhook models** for lower latency and simpler state management.

**7. Plugin Ecosystems Becoming Competitive Moats**
- ZeroClaw's 7 new WASM plugins in one day, NanoClaw's Google Contacts MCP skill, and OpenClaw's MCP tool expansion all indicate that **plugin richness is a key differentiator**. Expect a race to build plugin registries, sandboxed runtimes, and marketplaces. Developers should:
  - Build for MCP as the emerging standard (OpenClaw, ZeroClaw, NanoClaw, NanoBot all support it)
  - Design plugins as sandboxed, versioned, and independently deployable
  - Provide plugin search/install/discovery from the UI (ZeroClaw v0.8.3)

---

*Report generated from community digest data spanning 13 projects, reflecting activity as of 2026-06-07.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**Project Digest: NanoBot (github.com/HKUDS/nanobot)**  
**Date: 2026-06-07**

---

## 1. Today’s Overview
NanoBot shows high development velocity with **24 PRs updated** and **7 issues updated** in the last 24 hours. Ten PRs were merged or closed, signaling active bug fixing and feature integration, while the remaining four open issues and 14 open PRs indicate ongoing work. The project has **no new release** today, but the volume of closed PRs (including several long-standing items) suggests a major release may be building. Community engagement is moderate, with one issue receiving notable reactions.

---

## 2. Releases
*No new releases today.*

---

## 3. Project Progress (Merged/Closed PRs)
9 PRs were closed today (out of 10 merged/closed total). These represent significant forward progress across multiple areas:

- **Bug Fixes**  
  - [#4228](https://github.com/HKUDS/nanobot/pull/4228) – Preserve empty `reasoning_content` in streaming responses (fixes #4105).  
  - [#4209](https://github.com/HKUDS/nanobot/pull/4209) – Allow dropping default OpenAI image params via `null` `extraBody` (fixes #4167).  
  - [#4211](https://github.com/HKUDS/nanobot/issues/4211) – SDK stdio MCP shutdown error – no dedicated PR listed but issue closed.  
  - WhatsApp bridge fixes:  
    - [#2555](https://github.com/HKUDS/nanobot/pull/2555) – Close old clients on new connection to prevent duplicate messages.  
    - [#2529](https://github.com/HKUDS/nanobot/pull/2529) – Download audio messages for transcription.  
    - [#2528](https://github.com/HKUDS/nanobot/pull/2528) – Drop messages older than startup to avoid replaying history.  

- **Features**  
  - [#2968](https://github.com/HKUDS/nanobot/pull/2968) – Per-user memory isolation via `agents.defaults.per_user_memory` (multi-user deployment).  
  - [#2533](https://github.com/HKUDS/nanobot/pull/2533) – Per-MCP-server `allowFrom` access control.  
  - [#2532](https://github.com/HKUDS/nanobot/pull/2532) – Add Serper.dev as Google Search provider.  
  - [#4195](https://github.com/HKUDS/nanobot/pull/4195) – Desktop shell polish and shared WebUI surfaces.

These merges advance multi-user support, MCP security, search integration, and desktop readiness.

---

## 4. Community Hot Topics
- **Most Discussed Issue** – [#2573](https://github.com/HKUDS/nanobot/issues/2573) *“Github Copilot登录失败”* (3 comments, 9 👍). The user reported an OAuth login failure with a malformed authorization header after switching to OpenAI from LiteLLM. This closed issue drew significant attention.  
- **Active Feature PRs** – Several PRs from contributor `franciscomaestre` (e.g., [#4226](https://github.com/HKUDS/nanobot/pull/4226), [#4225](https://github.com/HKUDS/nanobot/pull/4225)) generate discussion around WhatsApp bridge improvements and cron enhancements.  
- **Observation**: The per-user memory PR [#2968](https://github.com/HKUDS/nanobot/pull/2968) (from April) was merged today after a long review cycle, indicating strong maintainer interest in multi-tenant features.

**Underlying needs**: Users want reliable authentication (GitHub Copilot), better multi-user isolation, and richer background automation.

---

## 5. Bugs & Stability (Reported in Last 24h)
*Bug issues sorted by estimated severity:*

| Severity | Issue | Description | Fix Available? |
|----------|-------|-------------|----------------|
| **High** | [#4222](https://github.com/HKUDS/nanobot/issues/4222) | `max_messages` truncation and micro-compact continuously invalidate prefix/prompt caching, causing degraded LLM performance. | No PR yet. |
| **Medium** | [#4211](https://github.com/HKUDS/nanobot/issues/4211) | SDK leaves stdio MCP open → `RuntimeError: exit cancel scope in a different task` at shutdown. | Closed (likely fixed by other changes). |
| **Medium** | [#4105](https://github.com/HKUDS/nanobot/issues/4105) | Custom provider drops empty `reasoning_content` string in tool call messages. | Fixed via [#4228](https://github.com/HKUDS/nanobot/pull/4228) and [#4227](https://github.com/HKUDS/nanobot/pull/4227). |
| **Low** | [#4167](https://github.com/HKUDS/nanobot/issues/4167) | Image generation fails with OpenAI-compatible APIs that reject `response_format`. | Fixed via [#4209](https://github.com/HKUDS/nanobot/pull/4209). |
| **Low** | [#2573](https://github.com/HKUDS/nanobot/issues/2573) | GitHub Copilot OAuth login header malformed. | Closed, fix presumed part of provider refactor. |

**Security-related**: [#4221](https://github.com/HKUDS/nanobot/pull/4221) (open) blocks relative symlink workspace escapes in `ExecTool` – a workspace isolation fix.

---

## 6. Feature Requests & Roadmap Signals
- **Enterprise & Multi-User**  
  - [#4220](https://github.com/HKUDS/nanobot/issues/4220) – Support GitHub Copilot for Business / Enterprise (different API endpoints).  
  - [#2968](https://github.com/HKUDS/nanobot/pull/2968) (merged today) – Per-user memory isolation.  
  - [#2533](https://github.com/HKUDS/nanobot/pull/2533) (merged) – Per-MCP-server access control.  

- **Cron & Automation**  
  - [#4218](https://github.com/HKUDS/nanobot/issues/4218) – WebUI cron job management (user requests UI for schedule editing).  
  - [#4225](https://github.com/HKUDS/nanobot/pull/4225) (open) – Add silent mode and `lock_recipient` for cron jobs (background monitoring use case).  

- **Transcription Providers**  
  - [#4224](https://github.com/HKUDS/nanobot/pull/4224) (open) – Add AssemblyAI as a third transcription provider (alongside OpenAI and Groq).  

- **Context/Sender Identity**  
  - [#4033](https://github.com/HKUDS/nanobot/pull/4033) (open) – Chat sender identity context for multi-user Discord channels and threads.  

**Prediction for next release**: GitHub Enterprise support (`agent providers`), AssemblyAI transcription, cron UI improvements, and further identity/context features are likely candidates for inclusion.

---

## 7. User Feedback Summary
- **Pain Points**  
  - *GitHub Copilot login* – user `cheanus` reported a broken OAuth flow after provider change (closed, but underscores sensitivity to authentication changes).  
  - *Image generation incompatibility* – user `gkd2323c` hit `UnsupportedParamsError` with APIs not supporting `response_format`. Fixed quickly.  
  - *Custom provider reasoning* – user `tjc0726` noticed empty `reasoning_content` being dropped, breaking APIs like DeepSeek. Fixes now merged.  
  - *Caching inefficiency* – user `imkuang` detailed how truncation and micro-compact defeat prompt caching, impacting performance. No fix yet.  

- **Use Cases**  
  - Multi-user deployments (per-user memory, MCP access control).  
  - Enterprise self‑hosted GitHub (GHE).  
  - Background monitoring via silent cron jobs.  
  - Voice message transcription from WhatsApp.  

- **Satisfaction Signals**  
  - Quick turnarounds on bugs (e.g., #4167, #4105).  
  - Long-standing features like per-user memory and Serper search finally merged, meeting community demands.

---

## 8. Backlog Watch
- **Long‑standing Issue Now Closed**: [#2573](https://github.com/HKUDS/nanobot/issues/2573) – created in March 2026, closed today.  
- **Long‑standing PR Merged**: [#2968](https://github.com/HKUDS/nanobot/pull/2968) (per-user memory) – opened April 9, merged after 2 months.  
- **No visible stale items** in the last 24h snapshot, but the open caching issue [#4222](https://github.com/HKUDS/nanobot/issues/4222) (created today) needs prioritization as it affects prompt caching performance.  
- **Maintainer attention** to open PRs like [#4094](https://github.com/HKUDS/nanobot/pull/4094) (channel dispatch, open since May 29) and [#4123](https://github.com/HKUDS/nanobot/pull/4123) (MCP SSRF guard, open since May 31) would be advisable to keep momentum.

---

*Data source: GitHub Issues & PRs for HKUDS/nanobot updated in the last 24 hours as of 2026-06-07.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-07

## Today's Overview
Hermes Agent saw **very high activity** on 2026-06-07, with 50 issues and 50 pull requests updated in the last 24 hours. Of these, **10 issues were closed** and **8 pull requests were merged/closed**, indicating steady progress on bug fixes and enhancements. No new official releases were published today. The community is actively reporting and discussing a wide range of bugs, feature requests, and platform-specific problems, with particular attention to macOS compatibility, provider integrations, and plugin lifecycle. The project remains healthy with strong contributor engagement across multiple components (CLI, desktop, gateway, plugins, tools).

## Releases
*No new releases today.*

## Project Progress
**8 pull requests were merged or closed today**, though specific titles are not listed in the provided data. However, several **issues were closed**, reflecting fixes that likely went into the codebase:

- [#40296 – Model displayed in UI/footer differs from config.yaml when using Nous provider](https://github.com/NousResearch/hermes-agent/issues/40296) (closed)
- [#22961 – Dashboard displays vision_analyze tool result as user message](https://github.com/NousResearch/hermes-agent/issues/22961) (closed)
- [#31193 – QQ Bot Reconnect Busy Loop Causes 100% CPU Spin](https://github.com/NousResearch/hermes-agent/issues/31193) (closed)
- [#40490 – CLI input locks up unrecoverably on lazy-dep install prompt](https://github.com/NousResearch/hermes-agent/issues/40490) (closed, P1)
- [#38358 – `_build_web_ui()` npm install missing --workspace web flag](https://github.com/NousResearch/hermes-agent/issues/38358) (closed)
- [#39436 – Desktop chat composer send button hidden until space is typed](https://github.com/NousResearch/hermes-agent/issues/39436) (closed)

These closures indicate that the team is actively resolving both stability issues and user-facing bugs across the desktop, CLI, and gateway platforms.

## Community Hot Topics
The following issues attracted the most discussion (by comment count or reactions):

- [#37505 – Hermes Desktop macOS DMG is arm64-only and fails on Intel Macs](https://github.com/NousResearch/hermes-agent/issues/37505) (6 comments)  
  The community is concerned about missing x86_64 support in the official DMG. This is a fundamental compatibility issue for Intel Mac users.

- [#27683 – web_tools.py: missing `_ensure_plugins_discovered()` causes web tools to silently fail](https://github.com/NousResearch/hermes-agent/issues/27683) (4 comments)  
  A fresh-install blocker: web search, extract, and crawl do not work due to uninitialized plugin system.

- [#40820 – Desktop installer fails on macOS when home directory path contains spaces](https://github.com/NousResearch/hermes-agent/issues/40820) (3 comments)  
  Affects users with external drives or non-standard home paths. A **fix PR exists** ([#40923](https://github.com/NousResearch/hermes-agent/pull/40923)).

- [#6718 – Background Process Auto-Notifications Not Delivering to Agent](https://github.com/NousResearch/hermes-agent/issues/6718) (3 comments, 👍1)  
  A long-standing notification delivery issue, same root cause as cron delivery problem.

- [#39281 – Hermes fails to work using gemma4 with ollama backend](https://github.com/NousResearch/hermes-agent/issues/39281) (3 comments)  
  Model hits max output tokens and stops; affects users of locally-run Gemma4.

Underlying needs: **multi-platform support** (Intel Mac, home paths with spaces), **robust plugin initialization**, **notification reliability**, and **provider compatibility** (Ollama, custom model configs).

## Bugs & Stability
Bugs reported or updated today, ranked by severity:

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#24433 – 'No inference provider configured' in interactive chat despite working CLI](https://github.com/NousResearch/hermes-agent/issues/24433) | **P1** | Interactive chat mode fails with provider misdetection; affects openai-codex users. | No PR yet |
| [#40831 – macOS 26: launchd domain hardcoded, breaks Aqua sessions](https://github.com/NousResearch/hermes-agent/issues/40831) | **P1** | Regression from PR #40581, gateway fails to start under gui domain. | No explicit PR |
| [#40820 – Desktop installer fails when home path contains spaces](https://github.com/NousResearch/hermes-agent/issues/40820) | **P2** | Critical for users with spaces in home directory. | PR [#40923](https://github.com/NousResearch/hermes-agent/pull/40923) |
| [#40801 – Cron script-path guard rejects profile-scoped jobs with default profile scripts](https://github.com/NousResearch/hermes-agent/issues/40801) | **P2** | Breaks cron jobs referencing shared scripts. | PR [#40918](https://github.com/NousResearch/hermes-agent/pull/40918) |
| [#40250 – Terminal escape sequences leaking into response output](https://github.com/NousResearch/hermes-agent/issues/40250) | **P2** | First 1-3 characters cut from responses. | No PR yet |
| [#39281 – gemma4 with ollama backend hits max output tokens](https://github.com/NousResearch/hermes-agent/issues/39281) | **P2** | Model stops responding. | No PR yet |
| [#40913 – openai-codex provider ignores `model.base_url` and env var](https://github.com/NousResearch/hermes-agent/issues/40913) | **P2** | Makes proxy routing impossible. | PR [#40924](https://github.com/NousResearch/hermes-agent/pull/40924) |
| [#40843 – Camofox HTTP client ignores browser.command_timeout](https://github.com/NousResearch/hermes-agent/issues/40843) | **P3** | Hardcoded 30s timeout overrides config. | No PR yet |

Several P2 fixes were PRed today, suggesting the maintainers are actively addressing these.

## Feature Requests & Roadmap Signals
Notable feature requests from the community (updated today):

- [#40917 – Board-level / auto-subscribe kanban event notifications](https://github.com/NousResearch/hermes-agent/issues/40917) → Would simplify multi-agent orchestration workflows.
- [#27777 – Goal lifecycle plugin hooks](https://github.com/NousResearch/hermes-agent/issues/27777) → Enables plugins to react to goal state changes.
- [#30577 – Structured metadata for gateway /goal status notices](https://github.com/NousResearch/hermes-agent/issues/30577) → Improves third-party gateway integration.
- [#35279 – Discord server management agent](https://github.com/NousResearch/hermes-agent/issues/35279) → Community owners want a bot to handle tickets, navigation, etc.
- [#13529 – Agent Activity API & Emotional State Exposure](https://github.com/NousResearch/hermes-agent/issues/13529) → Structured access to Hermes’s internal state for external systems.
- [#40940 – ScoutGate v2: bind /goal authority to lifecycle leases](https://github.com/NousResearch/hermes-agent/issues/40940) → Adds security-oriented lifecycle management.
- [#40484 – Desktop file tree should support deleting files via Delete key / right-click](https://github.com/NousResearch/hermes-agent/issues/40484) → Quality-of-life for UI users.
- [#40873 – OpenAI-compatible API audio passthrough for voice chat](https://github.com/NousResearch/hermes-agent/issues/40873) → Model-native audio input (e.g., Gemma4).

**Likely next-version features**: The `Keep Tool Calls Expanded` toggle ([PR #40942](https://github.com/NousResearch/hermes-agent/pull/40942)) is a small UI improvement that could be shipped soon. The new `AGIone provider` ([PR #40910](https://github.com/NousResearch/hermes-agent/pull/40910)) and `source-backed knowledge recall tool` ([PR #37884](https://github.com/NousResearch/hermes-agent/pull/37884)) are also in active review. Goal lifecycle hooks (#27777) and kanban board subscriptions (#40917) may appear in a subsequent minor release given community interest.

## User Feedback Summary
Real pain points expressed by the community:

- **macOS Intel users** are blocked from using the desktop app because the DMG is arm64-only ([#37505](https://github.com/NousResearch/hermes-agent/issues/37505)).
- **Plugin discovery and installation** remains fragile: web tools fail silently ([#27683](https://github.com/NousResearch/hermes-agent/issues/27683)) and the `mnemosyne-hermes` plugin is not detected ([#40101](https://github.com/NousResearch/hermes-agent/issues/40101)).
- **Desktop installer** fails for users with spaces in home paths ([#40820](https://github.com/NousResearch/hermes-agent/issues/40820)) or on Windows when PowerShell is not in PATH ([PR #40927](https://github.com/NousResearch/hermes-agent/pull/40927)).
- **Terminal UI** has escape sequence leaks and input lock-ups on lazy dep prompts ([#40250](https://github.com/NousResearch/hermes-agent/issues/40250), [#40490](https://github.com/NousResearch/hermes-agent/issues/40490)).
- **Slash commands** break with smart/curly quotes (e.g., `/kanban create “my prompt”` fails, [#40915](https://github.com/NousResearch/hermes-agent/issues/40915)).
- **Desktop users** experience missing send button and truncated messages ([#39436](https://github.com/NousResearch/hermes-agent/issues/39436)).
- **Background notifications** (cron, task completion) often do not reach the agent ([#6718](https://github.com/NousResearch/hermes-agent/issues/6718)).

Satisfaction: The sheer volume of feature requests suggests a highly engaged user base that sees Hermes as extensible. Frustration is concentrated on installation and initial configuration hurdles.

## Backlog Watch
Issues and PRs that have been open for an extended period without resolution, requiring maintainer attention:

- [#6718 – Background Process Auto-Notifications Not Delivering to Agent](https://github.com/NousResearch/hermes-agent/issues/6718) (open since **2026-04-09**, 3 comments, P3) – fundamental notification pipeline bug.
- [#13529 – Agent Activity API & Emotional State Exposure](https://github.com/NousResearch/hermes-agent/issues/13529) (open since **2026-04-21**, 1 comment) – a major feature request with no maintainer response.
- [#24433 – 'No inference provider configured' in interactive chat despite working configuration](https://github.com/NousResearch/hermes-agent/issues/24433) (open since **2026-05-12**, P1) – a high-severity bug affecting chat mode, still unaddressed.
- [#27683 – web_tools.py: missing plugin discovery](https://github.com/NousResearch/hermes-agent/issues/27683) (open since **2026-05-18**) – a fresh-install blocker with no linked PR.
- [#34197 – /goal auto-continuation amplified by preflight compression](https://github.com/NousResearch/hermes-agent/issues/34197) (open since **2026-05-29**) – non-trivial state management issue.

The project maintainers may want to triage these older items, especially the P1 bug #24433, which could degrade the core interactive experience.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-07

## 1. Today’s Overview

PicoClaw saw **high development velocity** with 18 pull requests updated in the last 24 hours (15 merged/closed) and 12 issues updated (10 open/active). A new **nightly build** (v0.2.9‑nightly) was released, though marked as unstable. The bulk of activity came from **stability fixes** (goroutine leaks, nil pointer guards, type assertion safety) and the start of a **trading/CLI module** (exchange connectors, risk manager, ClawHub message types) introduced as a batch of new issues by contributor `jcafeitosa`. Two older enhancement PRs (WhatsApp support, multi‑agent collaboration) were finally closed after months of inactivity, signalling a push to clear backlog.

## 2. Releases

**Nightly Build** — `v0.2.9‑nightly.20260607.7d2b0c2a`  
- Automated build, may be unstable.  
- Changes are incremental vs. the v0.2.9 tag; full changelog: [compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main).  
- No breaking changes or migration notes documented.

## 3. Project Progress (Merged/Closed PRs Today – 15 items)

**Multiple defensive fixes** by `chengzhichao xydt` (PRs #3014, #3021, #3022, #3023, #3017, #3019) addressed:  
- Goroutine leak in `Manager.Reload()` (cancel old dispatch context).  
- Safe type assertions on `sync.Map` operations (Slack, Windows, Feishu).  
- Unchecked `Close()` errors in updater extraction functions.  
- Missing `encoder.Close()` on `io.Copy` failure path.

**Feature/bug PRs closed:**  
- **#1112** – Added `deepseek‑ai` protocol support for ModelScope.cn (fixes provider recognition).  
- **#2711** – Fixed frontend copy button error in non‑secure HTTP contexts.  
- **#830** – Google Chat channel support (enhancement).  
- **#423** – Base multi‑agent collaboration framework & shared context (WIP, now merged).  
- **#2838** – Frontmatter tool policy filters (allow/deny glob patterns for tools/MCP).  
- **#2662** – Unified vendors table in providers documentation.  
- **#3020** – Improved Slack formatting and channel routing (allow/ignore filters).  
- **#2965** – Fixed workspace guard misreading scheme‑less URLs (e.g., `curl wttr.in`).  
- **#3013** – Removed references to missing helper scripts in skill‑creator docs.

## 4. Community Hot Topics

- **#2625** (closed, 8 comments, 1 👍) — *“Provide compiled builds with WhatsApp support”*  
  User requests WhatsApp inclusion in default ARM64 builds. The PR #830 (Google Chat) and #2625’s closing suggest maintainers may be rethinking build flags.  
  [Issue #2625](https://github.com/sipeed/picoclaw/issues/2625)

- **#2929** (closed, 3 comments, 2 👍) — *“First‑class agent‑to‑agent communication”*  
  Tracks a proposal for peer‑to‑peer agent messaging beyond `spawn`/`delegate`. While closed, it laid groundwork for future multi‑agent protocols.  
  [Issue #2929](https://github.com/sipeed/picoclaw/issues/2929)

- **#3032** (open, 1 comment) — *“EXM‑003: cmd/clawtrade CLI structure”*  
  Part of a larger exchange‑trading module. High interest from the developer community.  
  [Issue #3032](https://github.com/sipeed/picoclaw/issues/3032)

- **#3015** (open, 0 comments) — *“QQ channel connection failure on Windows”*  
  A fresh bug report; may become more active once Windows users test.  
  [Issue #3015](https://github.com/sipeed/picoclaw/issues/3015)

## 5. Bugs & Stability

**Reported today:**  
- **#3015** (QQ channel, Windows) — Token retrieval timeout. No workaround yet. Severity: medium (blocks QQ on Windows).  
- **#3028/#3027/#3026/#3025/#3024** — New exchange connector tasks are pre‑planned; not yet bugs.

**Fixed today (all via merged PRs):**  
- **Goroutine leak** on reload (critical, fixed in #3014).  
- **Nil agent panic** in startup info (#3021).  
- **Unchecked type assertions** causing panics in Slack/Windows/Feishu (#3022).  
- **Silent write failures** in updater extraction (#3023).  
- **Buffer corruption** in base64 encoder (#3017).  
- **Redundant type assertions** and missing error checks (#3019).  
- **Slack formatting/routing** improvements (#3020).  
- **Workspace guard bypass** with scheme‑less URLs (#2965).

Overall stability is improving rapidly, with **7+ defensive fixes merged in a single day**.

## 6. Feature Requests & Roadmap Signals

**Active feature requests:**  
- WhatsApp support in bundled builds (#2625) — likely to be addressed in next stable release via compile‑time flags.  
- Agent‑to‑agent communication (#2929) — a community request that may drive a dedicated messaging layer.  
- Traditional Chinese locale (#2935, PR still open) — low priority but uncontroversial.

**Roadmap signals from new issues (EXM‑xxx series):**  
- **ClawHub message types** (#3030) — core hub for agent/exchange messaging.  
- **Risk manager interface** (#3029).  
- **Binance WebSocket/REST connectors** with TDD and latency benchmarks (#3025, #3026, #3028).  
- **Lock‑free order book ring buffer** (#3027) – 1M updates/s, zero alloc.  
- **CLI for trade, backtest, agent, status** (#3032).

These new issues point to an **upcoming “ClawTrade” sub‑project** targeting quantitative trading and exchange integration. Expect a feature release focused on exchange connectors, risk management, and low‑latency data processing.

## 7. User Feedback Summary

- **Pain points:**  
  - WhatsApp users on ARM cannot use the default build (#2625).  
  - Windows users encountering QQ channel token timeout (#3015).  
  - Workspace guard false positives on scheme‑less URLs (#2965, now fixed).  
  - Missing Traditional Chinese documentation (#2935).

- **Satisfaction/dissatisfaction:**  
  - Positive: Slack formatting improvements (#3020) show responsiveness to messaging channel feedback.  
  - Mixed: Contributor `jcafeitosa` appears to be building the trading module solo; community adoption will depend on how quickly maintainers review and merge the upcoming PRs.

## 8. Backlog Watch

| Item | Status | Age | Notes |
|------|--------|-----|-------|
| [#2935 – Traditional Chinese locale (PR)](https://github.com/sipeed/picoclaw/pull/2935) | Open | 14 days | Awaiting maintainer review; low risk. |
| [#3016 – Fix goroutine leak & nil guard (PR)](https://github.com/sipeed/picoclaw/pull/3016) | Open | 1 day | Duplicates already‑merged #3014? Needs clarification. |
| [#3018 – Add type assertion `ok` checks (PR)](https://github.com/sipeed/picoclaw/pull/3018) | Open | 1 day | Similar to fixed #3022; may need conflict resolution. |
| [#3028 – Binance latency benchmarks](https://github.com/sipeed/picoclaw/issues/3028) | Open | 1 day | Part of trading roadmap; not yet blocking. |

**Priority attention** should go to PR #3016 and #3018 to avoid duplicated work. The zh‑TW locale PR remains unmerged for two weeks—low effort, high inclusivity value.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-07

---

## 1. Today’s Overview

The project saw high activity today, with **14 pull requests** updated (3 merged/closed) and **2 new open issues**. No new release was published. The merged PRs focused on solidifying the skill library’s upgradeability (conformance model) and preventing duplicate messages from multiple host processes. Several long-standing fix PRs (particularly around the Signal adapter, Slack integration, and container runner) remain open, while new issues highlight onboarding friction and edge cases in CLI commands. Overall, the project is in an active bug‑fix and refinement phase, with community contributors driving the majority of changes.

---

## 2. Releases

*None.*

---

## 3. Project Progress — Merged/Closed PRs

Three pull requests were merged or closed today:

- **[#2698 — Skills conformance: exemplars + fleet retrofit](https://github.com/nanocoai/nanoclaw/pull/2698) (merged)**  
  Establishes a skill upgradeability model: every skill must have minimal reach‑ins, a test per integration point, an idempotent `REMOVE.md`, and no `VERIFY.md`. This PR retrofits the entire skill library and retires/rewrites non‑conformant skills, making future maintenance significantly easier.

- **[#2696 — feat(add-dashboard): make the skill conformant (drift fix + shipped test)](https://github.com/nanocoai/nanoclaw/pull/2696) (merged)**  
  First exemplar of the new conformance model. Fixed silent import drift that would break the skill for new adopters and added an in‑process integration test.

- **[#2697 — feat(host): single-instance lock to prevent duplicate messages](https://github.com/nanocoai/nanoclaw/pull/2697) (merged)**  
  Introduces a file‑based lock so that only one host instance can run at a time, eliminating duplicate message deliveries that occurred when both `pnpm run dev` and the installed service were active.

---

## 4. Community Hot Topics

While no issues or PRs have accumulated comments yet, the following topics show the highest concentration of related work and updates:

- **Slack integration re‑architecture** — Two PRs were opened today to switch the Slack adapter and the `/add-slack` skill from HTTP webhook mode (which required a public URL) to **Socket Mode**, aligning with the rest of the codebase that uses real‑time connections.  
  [#2702 – fix(slack): switch adapter to Socket Mode](https://github.com/nanocoai/nanoclaw/pull/2702)  
  [#2700 – fix(skill/add-slack): switch to Socket Mode setup](https://github.com/nanocoai/nanoclaw/pull/2700)

- **Signal adapter fixes** — Two bug‑fix PRs from contributor `cfis` address fundamental issues with inbound image attachments and DM routing, both of which were causing silent message drops. These PRs have been pending for over a month and were updated again today.  
  [#2695 – fix(signal): stage inbound image attachments as base64](https://github.com/nanocoai/nanoclaw/pull/2695)  
  [#2694 – fix(signal): set isMention/isGroup on inbound DMs](https://github.com/nanocoai/nanoclaw/pull/2694)

- **User onboarding friction** — Issue [#2703](https://github.com/nanocoai/nanoclaw/issues/2703) describes a fresh‑install hang when following the recommended setup path, which is likely to draw attention from new contributors.

---

## 5. Bugs & Stability

| Severity | Issue / Related PR | Description | Fix Available? |
|----------|--------------------|-------------|----------------|
| **High** | [#2703 – Setup hang after recommended install](https://github.com/nanocoai/nanoclaw/issues/2703) | `cli/local` remains unwired after recommended setup; `pnpm run chat hi` hangs for 120s then times out with no diagnostic. | No fix yet. |
| **Medium** | [#2701 – `ncl groups restart --rebuild` fails on empty packages](https://github.com/nanocoai/nanoclaw/issues/2701) | Command crashes with “No packages to install” when both `packages_apt` and `packages_npm` are empty, even though a normal restart succeeds. | No fix yet. |
| **Low/Medium** | [#2699 – CLI generates UUIDs that break OneCLI agent IDs](https://github.com/nanocoai/nanoclaw/pull/2699) | `ncl groups create` produces UUIDs that can start with a digit; OneCLI requires a leading letter. Fix included in the PR. | PR open (follows guidelines). |
| **Low** | [#2531 – Poll loop sends duplicate text during mid‑turn send_message](https://github.com/nanocoai/nanoclaw/pull/2531) | Users see repeated text when `send_message` fires while the poll loop is active. | Fix PR open (since May 18). |
| **Low** | [#2184 – Poll loop delivers stale session error to user](https://github.com/nanocoai/nanoclaw/pull/2184) | Expired session IDs cause a raw error message to appear in chat before a fresh retry. | Fix PR open (since May 2). |

**Stability win**: The merging of [#2697](https://github.com/nanocoai/nanoclaw/pull/2697) (single‑instance lock) prevents the most common cause of duplicate messages, a significant quality‑of‑life improvement.

---

## 6. Feature Requests & Roadmap Signals

The following PRs and issues indicate likely near‑term feature additions:

- **[#2693 – feat(skill): add /add-google-contacts-tool](https://github.com/nanocoai/nanoclaw/pull/2693) (open)**  
  Adds a standalone MCP server skill for Google Contacts, completing the trio with existing Gmail and Google Calendar tools. Expected to be merged soon given its self‑contained nature.

- **[#2208 – feat(mcp): support HTTP and SSE MCP server transports](https://github.com/nanocoai/nanoclaw/pull/2208) (open)**  
  Extends MCP support beyond stdio to HTTP and Server‑Sent Events, enabling remote tool servers. This has been open since May 3 and appears to be a major feature awaiting final review.

- **Slack Socket Mode** (PRs #2702, #2700) — Once merged, it will eliminate the need for a public webhook URL, making Slack setup simpler and more secure. Likely to land in the next patch release.

- **Skill conformance model** (#2698) is now merged, so the next version will likely enforce these standards across all new skill submissions, improving long‑term maintainability.

---

## 7. User Feedback Summary

Based on the two new issues and the themes of open PRs:

- **Onboarding pain**: The most impactful user feedback comes from issue [#2703](https://github.com/nanocoai/nanoclaw/issues/2703). A fresh install that follows the recommended setup leads to a confusing 120‑second hang with zero diagnostic hints. This is a **high‑severity friction point** that can turn away new users immediately.

- **CLI edge cases**: Issue [#2701](https://github.com/nanocoai/nanoclaw/issues/2701) shows that advanced users attempting `ncl groups restart --rebuild` with empty package lists get a cryptic error rather than a graceful no‑op. The user explicitly notes “a normal restart succeeds,” highlighting an inconsistency.

- **Signal channel reliability**: The volume of Signal‑related PRs (two new fixes today, plus older ongoing work) suggests that Signal users are experiencing silent message drops and unusable image attachments. The community is actively contributing fixes.

- **No explicit satisfaction data** is present in the 24‑hour window, but the number of merged PRs and the conformance overhaul signal that maintainers are investing in quality.

---

## 8. Backlog Watch

Several important pull requests remain open for extended periods, requiring maintainer review:

| PR | Date Created | Days Open | Reason for Watch |
|----|--------------|-----------|------------------|
| [#2184 – fix(poll-loop): retry immediately on stale session](https://github.com/nanocoai/nanoclaw/pull/2184) | 2026-05-02 | 36 | Fixes a user‑visible error message; contributor is active but waiting for maintainer sign‑off. |
| [#2208 – feat(mcp): support HTTP/SSE transports](https://github.com/nanocoai/nanoclaw/pull/2208) | 2026-05-03 | 35 | Major feature that would unlock remote MCP tools; lacks recent maintainer activity. |
| [#2230 – fix(container-runner): map host user via keep-id on rootless podman](https://github.com/nanocoai/nanoclaw/pull/2230) | 2026-05-03 | 35 | Addresses container permissions for rootless Podman; important for Linux users. |
| [#2349 – fix(mount-security): tolerate allowlist entries missing path field](https://github.com/nanocoai/nanoclaw/pull/2349) | 2026-05-08 | 30 | Security hardening; prevents crashes on malformed mount allowlists. |
| [#2531 – fix(poll-loop): suppress duplicate text when send_message fires mid‑turn](https://github.com/nanocoai/nanoclaw/pull/2531) | 2026-05-18 | 20 | Duplicate messages degrade user experience; fix is awaiting review. |

All backlogged PRs are authored by active contributors (`cfis`) and are marked as following guidelines. Their prolonged open status may indicate maintainer bandwidth constraints.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-07

## 1. Today’s Overview
The IronClaw project experienced a high-activity day, with **31 PRs updated** and **2 issues updated** in the last 24 hours. Of those PRs, **10 were merged or closed**, and **21 remain open**. Most activity came from core contributors, with a heavy focus on the **Reborn architecture** (extension lifecycle, WebChat v2, Slack channel routing, OpenAI-compatible endpoints, and context compaction design). One new community PR was opened, and a critical **nightly E2E test failure** remains open. No new releases were published today. Overall, the project shows strong forward momentum on the Reborn track, though CI stability requires attention.

## 2. Releases
**None.**  
No new releases were published in the last 24 hours. The previous open release PR (#3708, updating `ironclaw_common` and `ironclaw_skills` to 0.5.0/0.4.0 with API breaking changes) is still open and has not been merged.

## 3. Project Progress
Today’s merged/closed PRs (10 total) advanced several key areas:

- **Documentation & Design**  
  - `#4486` & `#4485` (both merged) – Added unified design doc for background subagents, proactive context compaction, and WebUI run nesting.  
  - `#4520` (merged) – CI classification to keep Reborn-only PRs out of legacy test suites.

- **Reborn Capabilities**  
  - `#4508` (merged) – Converted repeated capability-call stops into a two-stage warning gate.  
  - `#4509` (merged) – Added Slack channel subject routing for product workflow.  
  - `#4508` (merged) – Gate repeated-call stops behind warning.

- **Fixes & Infrastructure**  
  - `#4523` (open but updated) – Fixes `TenantId`/`UserId` deserialization rejection of the system sentinel.  
  - `#4520` (merged) – CI: dynamic test discovery for Reborn.  
  - Several documentation-only PRs closing.

Other notable open PRs (still in review) include `#4522` (shared tool_args parsing primitives), `#4511` (outbound preference facade), `#4519` (WebUI session capabilities endpoint), `#4518` (extension lifecycle e2e), `#4516` (WebChat thread deletion), `#4489` (OpenAI-compatible refs), and `#4495` (routing chat completions through ProductWorkflow).

## 4. Community Hot Topics
While direct comment counts are unavailable, the following PRs attracted the most activity (by size and contributor diversity):

- **`#4521`** ([PR](https://github.com/nearai/ironclaw/pull/4521)) – *Add JSON cleaner for formatting and sanitization*  
  - **Author:** Dannye013 (new contributor)  
  - **Size:** S, **Risk:** Medium  
  - **Summary:** Implements a JSON cleaner that removes null keys and empty strings.  
  - **Significance:** First contribution from this author; addresses a practical developer UX issue.

- **`#3981`** ([PR](https://github.com/nearai/ironclaw/pull/3981)) – *Test: cover runtime HTTP redaction markers*  
  - **Author:** failuresmith (new contributor)  
  - **Size:** M, **Risk:** Low  
  - **Scope:** Security, Tests  
  - **Open since:** 2026-05-24 – awaiting maintainer review.  
  - **Significance:** Adds host API tests for sensitive header classification.

- **`#4002`** ([PR](https://github.com/nearai/ironclaw/pull/4002)) – *chore(deps): bump the actions group*  
  - **Author:** dependabot  
  - **Open since:** 2026-05-24, 16 updates pending.  
  - **Risk:** Medium (CI dependency upgrades).

**Underlying needs:**  
The community is beginning to contribute small utilities (JSON cleaner) and test coverage (redaction markers). The high volume of Reborn-focused PRs from core team indicates internal development is prioritized, but the presence of external contributors shows the project is open to community improvements.

## 5. Bugs & Stability
- **`#4108`** ([Issue](https://github.com/nearai/ironclaw/issues/4108)) – *Nightly E2E failed*  
  - **Severity:** High  
  - **Status:** Open (since 2026-05-27, last updated 2026-06-06)  
  - **Details:** The "Full E2E / E2E (extensions)" workflow failed on commit `26e41dc`. No comments or fix PR yet.  
  - **Impact:** Blocking confidence in the extension runtime path. This should be escalated.

- **`#4523`** ([PR](https://github.com/nearai/ironclaw/pull/4523)) – *fix(host_api): round-trip system sentinel through string_id Deserialize*  
  - **Severity:** Medium  
  - **Status:** Open (created 2026-06-06)  
  - **Details:** Fixes a bug where `TenantId`/`UserId` deserialization rejected the `\x1fSYSTEM\x1f` sentinel, causing LLM settings endpoints to return `service_unavailable`.  
  - **Affected area:** Host API, LLM settings.

- **`#4521`** (PR mentioned above) – while not a bug fix, the JSON cleaner addresses potential formatting issues.

**Overall stability:** Two active bug-related items exist: a persistent nightly failure (no fix yet) and a newly opened sentinel fix. The nightly E2E failure is the most critical.

## 6. Feature Requests & Roadmap Signals
No explicit user feature requests appear in the provided data. However, the following PRs and issues indicate forthcoming capabilities:

- **Notion MCP capability** – Issue #3805 (closed) outlines a planned MCP tool package for Notion.
- **Reborn extension lifecycle** – PRs #4518, #4517, #4516 signal that extension management (search, install, activate, remove) and configuration seeding are nearing completion.
- **OpenAI-compatible API** – PRs #4489 and #4495 are building out `POST /v1/chat/completions` with ProductWorkflow routing and ref management.
- **Slack channel administration** – PRs #4509, #4510 add persistent Slack channel routes and admin wiring.
- **Context compaction & subagents** – Design doc #4486 outlines future run nesting and proactive compaction.

These are likely part of the **Reborn** track targeting improved extensibility, multi-channel support, and API compatibility.

## 7. User Feedback Summary
No direct user feedback (comments, reactions) is present in the dataset. The only signal is the nightly E2E failure, which may impact developers relying on CI. The project’s focus on Reborn suggests internal priorities rather than external user requests.

## 8. Backlog Watch
- **`#4108`** ([Issue](https://github.com/nearai/ironclaw/issues/4108)) – *Nightly E2E failed*  
  - **Open since:** 2026-05-27 (11 days)  
  - **Importance:** Critical – no fix PR exists; needs maintainer investigation.

- **`#3981`** ([PR](https://github.com/nearai/ironclaw/pull/3981)) – *test: cover runtime HTTP redaction markers*  
  - **Open since:** 2026-05-24 (14 days)  
  - **Importance:** Moderate – community contribution awaiting review; merges could encourage more external contributions.

- **`#4002`** ([PR](https://github.com/nearai/ironclaw/pull/4002)) – *deps: bump actions group*  
  - **Open since:** 2026-05-24 (14 days)  
  - **Importance:** Low-medium – dependency updates; stale PR may cause CI drift.

- **`#3708`** ([PR](https://github.com/nearai/ironclaw/pull/3708)) – *chore: release*  
  - **Open since:** 2026-05-16 (22 days)  
  - **Importance:** High – contains breaking changes for `ironclaw_common` and `ironclaw_skills`. Blocking downstream consumers from getting new features.

**Maintainer attention needed:** Prioritize the nightly failure (#4108) and the stalled release PR (#3708). Responding to community PRs (#3981, #4521) would also foster contributor engagement.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-07

## Today's Overview
The project shows moderate activity over the past 24 hours, with **6 issues updated** (all remaining open) and **2 pull requests merged**. No new releases or tags were published. The community continues to report several long-standing bugs, particularly around silent data loss in modal dialogs and unexpected process terminations, while two feature PRs advanced the cowork and scheduled task modules. Overall, development velocity appears steady but may benefit from increased focus on resolving stale issues that have been open since early April.

## Releases
*No new releases in the last 24 hours.*

---

## Project Progress
Two pull requests were merged/closed today, both adding tangible functionality:

- **[PR #1529 – feat(cowork): batch export sessions as JSON](https://github.com/netease-youdao/LobsterAI/pull/1529)**  
  *Author: MaoQianTu*  
  Closes issue #1528. Adds a batch export button in cowork mode, allowing users to select multiple sessions and export them into a single structured JSON file. The backend IPC handler `cowork:session:exportBatch` prompts a save dialog with default filename `lobster-cowork-sessions-{timestamp}.json`.

- **[PR #1530 – feat(scheduledTask): multi-agent task assignment](https://github.com/netease-youdao/LobsterAI/pull/1530)**  
  *Author: gongzhi-netease*  
  When more than one agent is enabled, this PR introduces an **Agent selector** next to the model picker in the new scheduled task dialog. Users can now explicitly assign a task to any enabled agent (default remains `main`). This addresses confusion where tasks created via conversation implicitly belonged to the current conversation’s agent.

---

## Community Hot Topics
The most interactive discussions (by comments or reactions) include:

- **[Issue #2120 – Suggestion (new, 1 comment)](https://github.com/netease-youdao/LobsterAI/issues/2120)**  
  User *nbjoe* requests three improvements: (1) ability to pre-queue tasks while Claw is running (inspired by WorkBuddy), (2) extend single‑task timeout to avoid premature termination during long-running scripts, and (3) adjust the skill interface UI from 2‑column to 3‑column on wide screens (2560×1600). This is the only issue created today.

- **[Issue #1495 – Unexpected process interruption (1 👍, 1 comment)](https://github.com/netease-youdao/LobsterAI/issues/1495)**  
  User *xuzhiwu123* reports frequent “terminated” prompts during script monitoring. The comment asks whether the issue lies with the client or the LLM backend. This bug has been open since April and is receiving community attention (one thumbs‑up).

- **[Issue #1496 – Task marked complete but no return (2 comments)](https://github.com/netease-youdao/LobsterAI/issues/1496)**  
  User *netease-george* reports that submitted tasks show as “complete” but return no data. Two comments discuss the lack of output, but no resolution has been posted.

*Underlying needs*: Users are asking for better reliability in task execution (no silent failures), longer run limits, and UI improvements to accommodate higher‑resolution displays.

---

## Bugs & Stability
**High severity:**

- **[Issue #1495 – Unexpected process interruption](https://github.com/netease-youdao/LobsterAI/issues/1495)**  
  *Stale since Apr 7.* The client or backend terminates running scripts with no clear cause. This directly impacts user workflow and is the most critical active bug. No fix PR exists.

- **[Issue #1496 – Task completed but no output](https://github.com/netease-youdao/LobsterAI/issues/1496)**  
  *Stale since Apr 7.* Tasks show as finished but the result is empty. The user provided a screenshot but no root cause identified.

**Medium severity (usability / data loss):**

- **[Issue #1468 – Unsaved changes lost in Agent creation modal](https://github.com/netease-youdao/LobsterAI/issues/1468)**  
- **[Issue #1469 – Unsaved changes lost in Agent settings panel](https://github.com/netease-youdao/LobsterAI/issues/1469)**  
- **[Issue #1470 – Unsaved changes lost in MCP server config modal](https://github.com/netease-youdao/LobsterAI/issues/1470)**  

  All three (opened by *MaoQianTu* on Apr 4) describe identical UX flaws: closing any of these modals/dialogs via X, Cancel, Escape, or clicking the overlay immediately discards all unsaved input without a confirmation prompt. While not runtime crashes, these bugs cause real user frustration and data loss. No fix PR has been submitted.

---

## Feature Requests & Roadmap Signals
The single new feature request (issue #2120) points toward three clear user desires:

1. **Task queue / pre‑input**: Allow users to queue the next task while Claw is still running, improving pipeline continuity.
2. **Extended task runtime**: Increase the timeout (or make it configurable) to prevent “terminated” signals during long‑running scripts.
3. **UI layout flexibility**: Make the skill grid responsive (e.g., 3 columns) for large displays.

Given the merged PRs today, the roadmap appears to be investing in **cowork batch exports** and **scheduled task agent assignment**. The next minor release may include these features along with potential fixes for the stale bugs. The task‑queue concept aligns with the cowork workflow and could appear in a later version.

---

## User Feedback Summary
Real pain points expressed by users:

- **Reliability**: Tasks complete silently without returning data (#1496) or get terminated mid‑execution (#1495). Users are unsure whether to blame the client or the LLM backend.
- **Data loss**: Filling in agent settings, MCP environment variables, or creation forms only to lose them on accidental close (#1468, #1469, #1470) is a recurring complaint.
- **Usability friction**: The skill interface looks poor on ultra‑wide monitors; users want a denser layout. Also, the lack of a task queue forces manual serialization.
- **Satisfaction indicators**: No explicit positive feedback in today’s issues, but the number of stale issues suggests that unresolved bugs may be dampening user enthusiasm.

---

## Backlog Watch
Several important issues remain open without resolution for over two months:

| Issue | Created | Severity | Last Updated | Maintainer Action Needed |
|-------|---------|----------|--------------|--------------------------|
| [#1495 – Process interruption](https://github.com/netease-youdao/LobsterAI/issues/1495) | 2026-04-07 | 🔴 Critical | 2026-06-06 | Investigate root cause; consider adding logging or timeout configuration |
| [#1496 – Task done, no return](https://github.com/netease-youdao/LobsterAI/issues/1496) | 2026-04-07 | 🔴 High | 2026-06-06 | Reproduce; check task execution pipeline |
| [#1468 – Unsaved confirm missing (AgentCreateModal)](https://github.com/netease-youdao/LobsterAI/issues/1468) | 2026-04-04 | 🟡 Medium | 2026-06-06 | Add `beforeunload` or dirty‑state guard |
| [#1469 – Unsaved confirm missing (AgentSettingsPanel)](https://github.com/netease-youdao/LobsterAI/issues/1469) | 2026-04-04 | 🟡 Medium | 2026-06-06 | Same pattern as #1468 |
| [#1470 – Unsaved confirm missing (McpServerFormModal)](https://github.com/netease-youdao/LobsterAI/issues/1470) | 2026-04-04 | 🟡 Medium | 2026-06-06 | Same pattern as #1468 |

All five are **stale** (tagged with `[stale]`). Despite being updated in the last 24h, none have received a maintainer response or a linked fix PR. They should be prioritized to improve user trust and reduce frustration.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-07

## 1. Today's Overview
Project activity is moderate but focused on bug reports and one feature request. Three issues were updated in the last 24 hours, all opened yesterday (2026-06-06) and remaining open. No pull requests were updated, no new releases were published, and no code changes were merged. The development pace appears low today, with maintainer attention likely needed on the reported bugs, particularly the authentication bypass in Docker.

## 2. Releases
No new releases are available. The latest release remains unchanged.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. No feature advancements or fixes have been recorded.

## 4. Community Hot Topics
The most active issue today (by comment count) is:
- **[#1112 [Bug]: Disabling auth doesn't seem to disable auth (Docker)](https://github.com/moltis-org/moltis/issues/1112)** – 1 comment, authored by methompson. The reporter indicates that even after disabling authentication (likely via configuration), the Docker container still enforces auth. This is a potential security or usability blocker for local deployments.

Issues #1111 and #1110 have no comments yet. The underlying need across all three items points to cron job management and authentication configuration – users are seeking reliable toggles and suppression controls.

## 5. Bugs & Stability
Two bugs were reported today. Ranked by severity:

1. **High – [Issue #1112](https://github.com/moltis-org/moltis/issues/1112): Disabling auth doesn't work in Docker**  
   Impact: Users running Moltis in Docker cannot bypass authentication even when explicitly disabled, potentially blocking access or causing confusion. No associated fix PR exists.

2. **Medium – [Issue #1111](https://github.com/moltis-org/moltis/issues/1111): Archiving a cron session has no visible effect**  
   Impact: The archive UI action for cron sessions appears non-functional, leading to user confusion about session lifecycle management. No fix PR in progress.

Both bugs were reported by different users and lack maintainer responses.

## 6. Feature Requests & Roadmap Signals
One feature request was opened:
- **[#1110 [Feature]: Keyword to suppress cron job notifications (like NO_REPLY)](https://github.com/moltis-org/moltis/issues/1110)** – User IlyaBizyaev proposes a magic keyword (e.g., `NO_REPLY`) that, when included in a cron job message, suppresses notification output. This is a lightweight, user-driven feature that aligns with power-user workflows. It is unlikely to land in the next patch release but could be considered for a minor milestone if development resources permit.

## 7. User Feedback Summary
Two distinct pain points are emerging from today’s community input:

- **Authentication usability**: The Docker auth toggle does not work as documented, hindering local development or simple deployments. This suggests either a documentation gap or a code logic error.
- **Cron session visibility**: Archiving has no visible feedback, implying either missing UI state updates or backend inaction. Users want clearer lifecycle controls.
- **Cron notification fatigue**: The desire for a suppression keyword indicates that cron job output can become noisy, especially in automated or high-frequency scenarios. Users are looking for simple, inline mechanisms to manage noise without complex configuration.

Satisfaction is neutral; no positive feedback was recorded. Dissatisfaction stems from broken expected behaviors.

## 8. Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention were identified today. All three recent items are fresh (less than 24 hours old). Maintainers should prioritize responding to #1112 and #1111 to clarify next steps and signal active triage.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-07

**Note:** This digest is based on data from the [QwenPaw repository](https://github.com/agentscope-ai/QwenPaw), the primary product of the CoPaw ecosystem.

---

## 1. Today's Overview

Project activity over the past 24 hours was **moderate**, driven exclusively by issue reports. No pull requests were opened or merged, and no releases were published. Of the 11 issues updated, 9 remain open and 2 were closed (one long-standing context compression bug and a user-reported “false alarm” about approval commands). The majority of new issues are **bugs introduced in version 1.1.10**, including a critical regression where locally-hosted models fail to respond, a Windows path overflow crash, and a broken session-switching feature in Coding Mode. Community engagement is healthy, with maintainers actively commenting on several reports.

---

## 2. Releases

**No new releases** in the last 24 hours. The latest published version remains **v1.1.10** (referenced in many new bug reports). Users are advised to check for hotfix announcements in the coming days.

---

## 3. Project Progress

No pull requests were merged or closed today. The two closed issues are:

- **#4661** (closed) – [Bug]: v1.1.8post1 model context length configuration and memory compression not working.  
  *Author: wxfvf |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4661)  
  This issue, originally opened on May 25, was resolved after several comments and a configuration fix. It does not represent a code change from today.

- **#4984** (closed) – `<管家小新> Resolved: approval command already exists.`  
  *Author: Sclifftop |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4984)  
  User confirmed that the `/approval approve` magic command works as documented; no code change needed.

No feature advances or fixes were committed today via PRs.

---

## 4. Community Hot Topics

The following issues generated the most discussion and highlight recurring pain points:

- **#4937** – [Bug]: `/compact` command ignores model’s `max_input_length`, still uses 128K default.  
  *5 comments |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4937)  
  Users are frustrated that after configuring a model with 512K context (e.g., MiniMax M3), the `/compact` command falls back to 128K. This indicates a **core logic bug in context compression** that affects all large-context models.

- **#4661** (now closed) – [Bug]: Memory compression not working after upgrade.  
  *6 comments |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4661)  
  Detailed configuration issues and eventual fix. Many users likely experienced the same problem.

- **#4971** – [Feature]: Current session management is too cumbersome.  
  *2 comments |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4971)  
  Requests a sidebar for one-click session switching instead of current two-click workflow. Reflects desire for **better UX in session navigation**.

- **#4886** – [Feature]: Add MAX Messenger as a channel.  
  *2 comments |* [Link](https://github.com/agentscope-ai/QwenPaw/issues/4886)  
  Russian-speaking users request support for MAX (a popular messenger in Russia), aligning with QwenPaw’s “every channel” philosophy.

**Underlying needs:**  
- Reliable context compression that respects user-defined model limits.  
- Frictionless session switching.  
- Broader international channel support.

---

## 5. Bugs & Stability

Seven new bugs were reported today. Ranked by severity:

| Priority | Issue | Summary | Impact |
|----------|-------|---------|--------|
| **Critical** | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | Local Qwen 3.6-27B model (via vLLM) produces no response in v1.1.9/1.1.10; worked in v1.1.5.post2. | Users with self-hosted models are blocked entirely from using the latest versions. No error logs shown. |
| **Critical** | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | Session JSON filenames have duplicated session ID, causing MAX_PATH overflow on Windows. | Windows users cannot start the application or create new sessions. |
| **High** | [#4987](https://github.com/agentscope-ai/QwenPaw/issues/4987) | Session switching always fails in Coding Mode (works in normal mode); regression from v1.1.9. | Breaks a core workflow for users relying on Coding Mode. |
| **High** | [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) | WeChat Work channel returns error “Sorry, I cannot answer your question” when tool call info is closed. | IM channel tool integration broken for WeChat Work users. |
| **Medium** | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | `/compact` ignores model’s configured `max_input_length`. | Context compression fails for non-default models; workaround is manual config. |
| **Low** | [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) | Delete file command output does not wrap; requires horizontal scroll. | Minor UI annoyance. |
| **Low** | [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) | No real-time feedback while shell executes or file writes; user thinks system is stuck. | UX improvement request; not a crash. |

**No fix PRs exist yet** for any of these bugs.

---

## 6. Feature Requests & Roadmap Signals

Three feature requests were opened today:

- **#4986** – Real-time feedback during shell execution or file writing (like Cursor, WorkBuddy).  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/4986)  
  Users want live output streaming to avoid perceived freezes.

- **#4971** – Session management UI improvement: add session sidebar for quick switching.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/4971)  
  High upvote potential; likely to be prioritized in next UI iteration.

- **#4886** – MAX Messenger channel support (Russian market).  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/4886)  
  If the team aims for broader channel coverage, this may appear in v1.2.0.

**Prediction for next version:**  
- Session sidebar (from #4971)  
- Fix for context compression config (#4937)  
- At least one critical regression fix (#4989, #4988, #4987) will block any release otherwise.

---

## 7. User Feedback Summary

**Satisfaction drivers:**  
- Quick acknowledgment of issues by maintainers (e.g., comments on #4937, #4971).  
- Approval command works as documented (#4984 closed with thanks).

**Pain points (multiple users):**  
- **Regressions** in v1.1.10 are the strongest signal of dissatisfaction. Users upgrading from v1.1.5.post2 or v1.1.9 lose functionality.  
- **Configuration inconsistencies** – model-specific `max_input_length` is not honored by compression (#4937, #4661).  
- **Windows compatibility** – session file naming is broken (#4988), a problem that likely existed earlier but only surfaced with specific usage.  
- **Lack of real-time feedback** for long-running operations (#4986) makes the system feel unresponsive.

**Overall sentiment:** The community is active and constructive, but the v1.1.10 release appears to have introduced several serious regressions that need immediate hotfixes.

---

## 8. Backlog Watch

| Issue | Age | Last Updated | Status | Maintainer Action Needed |
|-------|-----|--------------|--------|--------------------------|
| [**#4661**](https://github.com/agentscope-ai/QwenPaw/issues/4661) – context compression config not working | 12 days | Jun 6 (closed) | **Closed** – resolved after configuration guidance. | – |
| [**#4937**](https://github.com/agentscope-ai/QwenPaw/issues/4937) – `/compact` ignores `max_input_length` | 4 days | Jun 6 | Open, 5 comments | Maintainers have asked for logs; follow-up needed to confirm root cause. |
| [**#4886**](https://github.com/agentscope-ai/QwenPaw/issues/4886) – MAX Messenger channel | 5 days | Jun 6 | Open, 2 comments | No maintainer reply yet. Low urgency but important for Russian community. |

**No unresolved issues older than two weeks** remain open now that #4661 is closed. The current backlog is fresh and actively being triaged. The team should prioritize the critical bugs (#4989, #4988, #4987) before addressing feature requests.

---

*Digest generated on 2026-06-07 from [GitHub data](https://github.com/agentscope-ai/QwenPaw).*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-07

## 1. Today’s Overview
Project activity has been moderate over the last 24 hours, with all movement concentrated on the binary-size tracking and gating infrastructure. One issue was closed (a completed audit of size drift) and a new issue was opened to tighten the gate for the aarch64 target. The corresponding PR that promotes the binary-size check to a PR gate remains open and was updated yesterday. No new releases were cut, but the ongoing work signals that the maintainer team is actively hardening deployment constraints for constrained environments (robots, embedded, Apple Silicon). The project is in a stable, focused CI/tooling improvement phase.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
- **Closed Issue** [#612 – `chore(perf): audit ~800KB binary-size drift since 6.2MB low water mark, tighten gate to 7MB`](qhkm/zeptoclaw/issue/612) (P2-high). This closed issue documented a size regression and the decision to tighten the gate. The audit is complete, laying groundwork for the current gating changes.
- **Open PR** [#611 – `chore(ci): promote binary-size to PR gate at 7.5MB`](qhkm/zeptoclaw/pull/611) was updated but not merged yet. It lowers the ceiling from the previous post‑mortem check to a live PR gate at 7.5 MB (darwin‑arm64 currently sits at 6.98 MB). The community can expect this PR to land soon after the follow-up issue #629 is resolved.

## 4. Community Hot Topics
The only two issues and one PR in the last 24 hours are thematically linked, making them the centre of discussion:

- **[Issue #629 (OPEN) – `chore(ci): add aarch64 binary-size gate at 7MB (the actual robot moat)`](qhkm/zeptoclaw/issue/629)** — This newly created issue proposes a separate, stricter gate for aarch64 (Pi/Jetson/Apple Silicon) at 7 MB, reflecting the real-world deployment constraint (“robot moat”). It currently has 0 comments but was opened by the same maintainer behind the related PR.
- **[PR #611 (OPEN) – `chore(ci): promote binary-size to PR gate at 7.5MB`](qhkm/zeptoclaw/pull/611)** — Although the PR itself has `undefined` comments in the data feed, it is the central mechanism for enforcing size discipline. The underlying need is clear: prevent unplanned binary bloat from entering the main branch and guarantee that the product can fit on resource‑limited hardware.

**Analysis**: The community (driven by the maintainer team) is prioritising deterministic binary size control. The debate between a unified 7.5 MB gate (PR #611) versus a per-architecture 7 MB aarch64 gate (issue #629) indicates a thoughtful design process. No external user feedback has surfaced yet, suggesting this is an internal engineering initiative.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. All tracked items are classified as “chore” and relate to CI process improvements rather than runtime defects. The project appears stable.

## 6. Feature Requests & Roadmap Signals
The only roadmap signals come from the binary-size governance work:
- **7.5 MB universal gate** (PR #611) — likely to land in the next minor commit.
- **7 MB aarch64-specific gate** (Issue #629) — a follow‑up that will tighten the constraint for edge devices. This may become part of the next release cycle (e.g., v0.10.x).
- No external feature requests appeared. The maintainer is driving the roadmap based on deployment needs (robots, embedded).

## 7. User Feedback Summary
No direct user feedback was captured in the last 24 hours. The issues and PRs are authored by the project maintainer (`qhkm`) and reflect internal quality goals. Implicit user needs derived from the work: smaller binary footprints for embedded/robotic deployments, and confidence that PRs won’t silently increase binary size.

## 8. Backlog Watch
There are no long-unanswered important issues or PRs requiring maintainer attention. The two open items (Issue #629, PR #611) are both recent (created/updated on 2026-06-06) and are being actively worked. The closed issue #612 was resolved in one week. The backlog is clean.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-06-07

## Today’s Overview
ZeroClaw experienced another day of very high activity: **39 issues** and **50 pull requests** were updated in the last 24 hours. The project is deep into a rapid-release cycle, with three concurrent milestone trackers (v0.8.0, v0.8.1, v0.8.2) driving work on **security hardening, plugin infrastructure, and web dashboard features**. Seven high-severity bugs were closed, and a large wave of new WASM plugin PRs (n8n, ACE-Step, SD‑WebUI, Nominatim, LanguageTool, Ollama Embed) signals that the plugin ecosystem is growing fast. No new releases were cut today, but the pipeline is building toward v0.8.0.

## Releases
**None.** No version was published today.

## Project Progress (Merged/Closed PRs)
The following PRs were merged or closed today, advancing several critical areas:

- **Security & Policy Fixes**
  - [#7281 (merged)](https://github.com/zeroclaw-labs/zeroclaw/pull/7281) — fix path‑guard false‑positives on heredoc bodies and non‑path tildes (closed #7133)
  - [#7334 (merged)](https://github.com/zeroclaw-labs/zeroclaw/pull/7334) — clamp zero draft‑update interval in Telegram partial streaming (closed #7332)

- **Gateway/Webhooks**
  - [#7297 (merged)](https://github.com/zeroclaw-labs/zeroclaw/pull/7297) — per‑request agent dispatch for `POST /webhook` via `?agent=` parameter

- **Plugin Infrastructure (Opened, high‑impact PRs)**
  Three major stacked PRs were opened that will likely merge in the coming days:
  - [#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335) — sandbox isolation for WASM plugins (resource limits, SSRF egress guard, env scoping)
  - [#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337) — namespace plugin tools (`plugin__`) + rate‑limited tool wrapping
  - [#7336](https://github.com/zeroclaw-labs/zeroclaw/pull/7336) — default `signature_mode` to permissive + surface signature status

Additionally, **seven new WASM tool plugins** were contributed (all opened, not yet merged): n8n workflow trigger, ACE‑Step music generation, SD‑WebUI image generation, Nominatim geocoding, LanguageTool grammar/style, Ollama Embed local embeddings, and a remote plugin registry CLI (`zeroclaw plugin search/install`).

## Community Hot Topics
The most actively discussed issues (by comment count) reflect three recurring themes:

- **Authentication & Provider Expansion**
  - [#5601 (7 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/5601) — “Add subscription‑native OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax.” Users want to ditch static API keys for these emerging providers. This is a **high‑risk**, blocked feature that remains a top community request.
  - [#7141 (4 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) — “OIDC Authentication Provider support.” A tracking issue for pluggable auth (target v0.9.0), signaling interest in enterprise‑grade identity federation.

- **Repository & Localization Hygiene**
  - [#7184 (4 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) — RFC to move translation files (`.ftl`, `.po`) into a git submodule, reducing clutter in the main repo.
  - [#6715 (4 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/6715) — Delete unneeded merged branches (over 200). Community member `Project516` drives a cleanup effort.

- **Tool Execution & Security**
  - [#6915 (3 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/6915) — Skill‑scoped tool activation (already closed/merged). The underlying need: skills must be able to temporarily use tools not in the agent’s allowlist without compromising security.
  - [#6914 (3 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) — Enforce `allowed_tools` / `denied_tools` in the main agent loop (still open, blocked). Community wants consistent tool policy enforcement.

## Bugs & Stability
Today saw **seven high‑severity bugs closed**, including two S0 (data loss / security risk) issues. No new S0/S1 bugs were opened today.

| Issue | Severity | Summary | Fix PR |
|-------|----------|---------|--------|
| [#7252 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7252) | **S0** | Killed ACP sessions can be rehydrated from durable history → data loss / security | No separate PR (fixed in #7182 follow‑up) |
| [#6978 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/6978) | **S0** | Nested secrets in `ObjectArray` config fields not redacted | No separate PR |
| [#7068 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7068) | **S1** | Telegram channel may send internal Codex scratchpad as final response | Not linked |
| [#7126 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) | **S2** | Web UI “Clear all” only wipes frontend, not backend session history | Not linked |
| [#7133 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7133) | **S2** | Path‑policy false‑positive on `~` in quoted/heredoc commands | [#7281](https://github.com/zeroclaw-labs/zeroclaw/pull/7281) |
| [#7197 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7197) | **S2** | Web toolbar slow on Windows + visible `cmd` windows | Not linked |
| [#7332 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7332) | **S2** | Telegram partial streaming accepts zero draft update interval → flood edits | [#7334](https://github.com/zeroclaw-labs/zeroclaw/pull/7334) |

All seven bugs were closed today, indicating a strong focus on stability. The two S0 fixes (config secret redaction, session rehydration) are critical for production deployments.

## Feature Requests & Roadmap Signals
Several open enhancements point directly to the near‑term roadmap:

- **v0.8.0** (tracker [#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) – Blockers include: `allowed_tools` enforcement ([#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914)), tool‑call parser fix for plural `<tool_calls>` (closed [#6875](https://github.com/zeroclaw-labs/zeroclaw/issues/6875)), and provider fallback wiring (closed [#6295](https://github.com/zeroclaw-labs/zeroclaw/issues/6295)). Expected imminently.
- **v0.8.1** (tracker [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) – Focus on integration/channel/provider/tool additions (e.g., Feishu hardening PR [#7256](https://github.com/zeroclaw-labs/zeroclaw/pull/7256), new plugin PRs).
- **v0.8.2** (tracker [#7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314)) – WASM plugin program: FND‑001 component model, WIT interfaces, host‑function support. The sandbox PRs [#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335) and [#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337) are the first building blocks.
- **v0.8.3** (tracker [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320)) – MCP dashboard + web/plugin‑management surfaces (PR [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) nearly ready).

Prominent user‑requested items include: OAuth for more providers ([#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)), per‑skill security permissions ([#5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775)), and pre‑hook skip gates for cron/SOP ([#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607)). These are all still open and likely to land in v0.9.0 or later.

## User Feedback Summary
From issue comments and reports, the following real‑user pain points emerged:

- **Authentication friction**: Users want OAuth for Ollama Cloud, Zhipu, Kimi, MiniMax – static keys are a barrier ([#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)).
- **Tool security granularity**: Skill authors need per‑skill `allow_scripts` and `allowed_commands` ([#5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775)).
- **Nix flake usability**: `wariuccio` reported that the flake outputs a toolchain, not the zeroclaw package ([#6906](https://github.com/zeroclaw-labs/zeroclaw/issues/6906)).
- **Web UI parity**: Users expect the daemon Config tab to match zerocode’s split‑pane layout (PR [#7298](https://github.com/zeroclaw-labs/zeroclaw/pull/7298)).
- **Windows experience**: The web toolbar spawns visible `cmd` windows and loads slowly ([#7197](https://github.com/zeroclaw-labs/zeroclaw/issues/7197), closed today).

Satisfaction signals: rapid fix turnaround on the Telegram draft‑edit flood, the path‑policy false‑positive, and the session rehydration bug show that the team is responsive to production‑level stability.

## Backlog Watch
Several important issues remain open for weeks with no recent maintainer update:

- [#5601 (April 10)](https://github.com/zeroclaw-labs/zeroclaw/issues/5601) – OAuth for additional providers. High risk, blocked. Last updated June 6 but no assignee activity. *Most‑commented issue overall.*
- [#5607 (April 10)](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) – Pre‑hook skip gates for cron/SOP triggers. High risk, blocked, accepted. No recent movement.
- [#5775 (April 15)](https://github.com/zeroclaw-labs/zeroclaw/issues/5775) – Per‑skill security permissions. High risk, blocked. No assignee.
- [#5908 (April 19)](https://github.com/zeroclaw-labs/zeroclaw/issues/5908) – GitHub Actions CI/CD for Debian container images. Blocked, accepted. Outdated by almost two months.
- [#6906 (May 25)](https://github.com/zeroclaw-labs/zeroclaw/issues/6906) – Nix flake improvement. Still open with no assignee; maintainer attention would be appreciated by Nix users.

These are all officially `status:blocked` or `status:accepted`, but they lack updated timelines or milestone assignments. The community would likely benefit from a comment explaining the blocking dependencies.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*