# OpenClaw Ecosystem Digest 2026-06-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-11 02:53 UTC

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

# OpenClaw Project Digest – 2026-06-11

## 1. Today's Overview

OpenClaw is experiencing extremely high activity: **500 issues and 500 pull requests were updated in the last 24 hours**, with 470 issues open and 398 PRs open. 30 issues were closed and 102 PRs were merged or closed, indicating a healthy contribution pipeline. A new beta release **v2026.6.6-beta.1** shipped, focused on tightening security boundaries. The project continues to attract significant community engagement on stability, security, and feature requests, while maintainers are actively reviewing PRs.

## 2. Releases

**v2026.6.6-beta.1 (OpenClaw 2026.6.6-beta.1)**  
*2026-06-06 (first appeared in today's data)*

**Highlights** – The release note states that “security boundaries are substantially tighter across transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, elevated sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group ac”. No specific breaking changes or migration notes were provided in the snippet, but operators should review their security configurations, especially for sandbox and tool access policies.

## 3. Project Progress

**Merged/closed PRs today (102 total)** – Notable completed work:

- **Telegram non-streaming tool progress** – PR [#89890](openclaw/openclaw PR #89890) (closed) added a non-streaming tool+commentary progress accumulator for Telegram, complementing the streaming counterpart.
- **Persistent progress mode for streaming** – PR [#89850](openclaw/openclaw PR #89850) (closed) implemented an opt-in `persistProgress` mode that keeps tool/commentary lines visible above the final answer.
- **Durable inter-tool commentary** – PR [#91976](openclaw/openclaw PR #91976) (closed) superseded the two previous PRs, providing a unified solution for verbose standalone progress across Discord and Telegram.
- **Fix Discord multi-bot slash commands** – PR [#77367](openclaw/openclaw PR #77367) (closed) scoped the command-deploy cache by application ID, resolving secondary account registration failures.
- **Background exec completion delivery** – PR [#91921](openclaw/openclaw PR #91921) (open, with proof) fixes the agent receiving `[OpenClaw heartbeat poll]` instead of a proper exec-completion notification.

**Active PRs advancing today:**

- **Tool trust tightening** – PR [#47523](openclaw/openclaw PR #47523) (P1, ready for maintainer look) preflight tool name collisions to prevent local media passthrough abuse.
- **Inbound buffer drain before reload** – PR [#46303](openclaw/openclaw PR #46303) (P1, needs proof) prevents message loss on `SIGUSR1` restart by draining debounce and followup queues.
- **Fail fast on missing probe auth** – PR [#68280](openclaw/openclaw PR #68280) adds clear failure reason for local loopback auth.
- **User-specific memory isolation** – PR [#47277](openclaw/openclaw PR #47277) (P1, needs proof) enables per-user memory files in multi-user environments.
- **New QQBot fix** – PR [#92074](openclaw/openclaw PR #92074) (opened today) flushes tool output before silent non-streaming final replies.

## 4. Community Hot Topics

Most active issues (by comment count):

| Issue | Title | Comments | Reaction |
|-------|-------|----------|----------|
| [#25592](openclaw/openclaw Issue #25592) | [P1, diamond lobster] Text between tool calls leaks to messaging channels | 31 | 👍1 |
| [#44925](openclaw/openclaw Issue #44925) | [P1, diamond lobster] Subagent completion silently lost — no retry, no notification | 19 | 👍1 |
| [#88838](openclaw/openclaw Issue #88838) | [P0, diamond lobster] Track core session/transcript SQLite migration via accessor seam | 19 | 👍1 |
| [#32473](openclaw/openclaw Issue #32473) | [Bug]: control ui requires device identity (use HTTPS or localhost secure context) | 17 | 👍4 |
| [#22438](openclaw/openclaw Issue #22438) | [P2, diamond lobster] Tiered bootstrap file loading for progressive context control | 17 | – |
| [#22676](openclaw/openclaw Issue #22676) | [P1, diamond lobster] Signal daemon stop() race condition on SIGUSR1 restart | 17 | – |
| [#32296](openclaw/openclaw Issue #32296) | [P1, platinum hermit] Agent replies to previous message instead of current | 15 | 👍1 |
| [#58450](openclaw/openclaw Issue #58450) | [P2, platinum hermit] Agent can promise a follow-up without starting any action | 15 | 👍2 |

**Underlying needs:** The community is most concerned about **message leakage and silent failures** – especially tool-call text appearing in chat channels, subagent results being lost, and session context getting mixed up. These point to a strong need for stricter output control and reliability in agent orchestration. Security-related issues (device identity, untrusted prompt injection) also attract many comments and reactions.

**Most upvoted feature requests:**
- [#39604](openclaw/openclaw Issue #39604) (👍9) – Allow private network access in `web_fetch`
- [#18160](openclaw/openclaw Issue #18160) (👍10) – Direct exec mode for cron jobs
- [#42840](openclaw/openclaw Issue #42840) (👍6) – MathJax/LaTeX support in Control UI
- [#79077](openclaw/openclaw Issue #79077) (👍7) – Telegram bot-to-bot and guest-bot modes

## 5. Bugs & Stability

**P0 severity:**
- [#88838](openclaw/openclaw Issue #88838) – Core session/transcript SQLite migration tracking (no fix PR yet)

**P1 severity (critical):**
- [#25592](openclaw/openclaw Issue #25592) – Text leaks to messaging channels (no new fix PR)
- [#44925](openclaw/openclaw Issue #44925) – Subagent completion silently lost (no new fix PR)
- [#22676](openclaw/openclaw Issue #22676) – Signal daemon race condition (no new fix PR)
- [#32296](openclaw/openclaw Issue #32296) – Agent replies to previous message (no new fix PR)
- [#32473](openclaw/openclaw Issue #32473) – Control UI device identity requirement (no new fix PR)
- [#29387](openclaw/openclaw Issue #29387) – Bootstrap files in agentDir ignored (no new fix PR)
- [#31583](openclaw/openclaw Issue #31583) – `exec` tool not inheriting skill env (no new fix PR)
- [#31331](openclaw/openclaw Issue #31331) – Docker+Sandrox workspace access broken (no new fix PR)
- [#38327](openclaw/openclaw Issue #38327) – "Cannot convert undefined or null to object" with Gemini (linked PR open)
- [#40540](openclaw/openclaw Issue #40540) – Windows `openclaw update` EBUSY error (source-repro)
- [#41165](openclaw/openclaw Issue #41165) – Telegram DMs still routing to main session after fix #40519
- [#41744](openclaw/openclaw Issue #41744) – Feishu read image tool result lost before outbound
- [#43015](openclaw/openclaw Issue #43015) – message.send schema overexposes fields causing GPT auto-population
- [#43661](openclaw/openclaw Issue #43661) – Session hangs on compaction timeout
- [#44905](openclaw/openclaw Issue #44905) – Discord leaks internal tool-call traces
- [#83184](openclaw/openclaw Issue #83184) – Heartbeat-driven agent leaves pendingFinalDelivery stuck
- [#39476](openclaw/openclaw Issue #39476) – A2A sessions_send causes duplicate messages
- [#43367](openclaw/openclaw Issue #43367) – Multi-agent orchestration unstable
- [#40001](openclaw/openclaw Issue #40001) – Write tool lacks append mode, data loss in cron
- [#45740](openclaw/openclaw Issue #45740) – gh-issues skill injects untrusted body into sub-agent prompt
- [#37634](openclaw/openclaw Issue #37634) – Sandbox workspaceAccess “none” still writeable

**Fix PRs exist for some but not all:** Many high-severity bugs carry the `clawsweeper:no-new-fix-pr` label, indicating no fix PR has been opened. Notable exceptions with linked PRs: #38327 (linked PR open), #41744 (linked PR), #45740 (linked PR), #39476 (linked PR), #83184 (linked PR). The community is actively waiting for maintainer reviews on many of these.

## 6. Feature Requests & Roadmap Signals

**Likely candidates for the next release (v2026.6.x or beyond):**

- **Security hardening** – Already shipped in v2026.6.6-beta.1, but more is in the pipeline (tool trust PR #47523, user-specific memory isolation #47277).
- **Telegram progress improvements** – The merged PRs for persistProgress and non-streaming progress will likely land in the next stable release.
- **Per-agent cost budgets** – [#42475](openclaw/openclaw Issue #42475) (P2) is being discussed; gateway-level enforcement would please operators.
- **Direct exec for cron jobs** – [#18160](openclaw/openclaw Issue #18160) (👍10) would bypass LLM overhead for simple tasks.
- **Bootstrap file tiered loading** – [#22438](openclaw/openclaw Issue #22438) to save tokens in subagents.
- **MathJax/LaTeX in Control UI** – [#42840](openclaw/openclaw Issue #42840) (👍6) is a small but popular enhancement.
- **Telegram guest-bot and bot-to-bot** – [#79077](openclaw/openclaw Issue #79077) (👍7) following Telegram's May 2026 release.
- **Per-skill model routing** – [#43260](openclaw/openclaw Issue #43260) for agent flexibility.
- **Webhook session reuse** – [#11665](openclaw/openclaw Issue #11665) to fix documented multi-turn support.

**Longer-term roadmap signals:**
- Multi-agent collaboration enhancements (RFC #35203) – capability profiling, shared blackboard, layered memory.
- Pre-response enforcement hooks (hard gates) – #13583 for mission-critical workflows.
- Durable natural-language rule learning – #41366 for multi-agent group chats.

## 7. User Feedback Summary

**Pain points voiced by users:**

- **Message leakage** (most upvoted bug): Internal tool processing text, NO_REPLY markers, and raw JSON appear in Slack/Discord/Telegram channels. Users are frustrated that “internal processing output … gets routed to the active messaging channel.”
- **Subagent reliability**: “Subagent results are silently lost” with no retry or notification – critical for users relying on agent orchestration.
- **Session context confusion**: Agents responding to the wrong message, or not recognizing current conversation state.
- **Memory management chaos**: Different users report completely different behaviors (chunking vs. no chunking, different storage backends) – a regression in v2026.3.x.
- **Setup friction**: Onboarding wizard omits memory/embedding configuration, causing new users to miss important features.
- **Docker and sandbox issues**: Workspace access does not work in Docker+DoD setups, and sandbox isolation is incomplete.
- **Windows update failure**: `openclaw update` fails with EBUSY, blocking self-updates.

**Satisfaction signals:** Users are requesting new features (MathJax, Telegram bot modes, per-skill models) and providing detailed field reports (e.g., browser tool improvements, multi-agent orchestration tests). The high comment and reaction counts indicate an engaged and technically sophisticated community.

## 8. Backlog Watch

**High-impact issues lacking maintainer attention or fix PRs:**

| Issue | Title | Created | Status |
|-------|-------|---------|--------|
| [#10687](openclaw/openclaw Issue #10687) | Models: fully dynamic model discovery (OpenRouter) | 2026-02-06 | stale, needs maintainer review |
| [#135

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent Open-Source Ecosystem
**Date:** 2026-06-11  
**Analyst:** Senior AI Agent Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing an inflection point, characterized by intense activity across multiple reference implementations and specialized agents. The landscape is defined by a dual focus: **security hardening and multi-agent orchestration reliability**, with every major project shipping or planning security-focused releases alongside deeper agent collaboration capabilities. The ecosystem is fragmenting by deployment model — lightweight embedded agents (NanoBot, PicoClaw) versus full-stack enterprise-ready platforms (OpenClaw, IronClaw, ZeroClaw) — yet converging on shared pain points around message leakage, subagent failure modes, and Docker/container experience. Community contributions are outpacing maintainer review bandwidth in several projects, with OpenClaw, ZeroClaw, and IronClaw each processing 50+ PRs in 24 hours, signaling both high engagement and potential bottlenecks. A clear trend toward **WASM plugin architectures** (ZeroClaw) and **programmatic MCP server configuration** (IronClaw, LobsterAI) suggests the ecosystem is preparing for a modular, sandboxed plugin economy.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Issues Open | PRs Open | Release Today | Health Score |
|---------|---------------------|-------------------|-------------|----------|---------------|--------------|
| **OpenClaw** | 500 | 500 | 470 | 398 | ✅ v2026.6.6-beta.1 | ⭐⭐⭐⭐⭐ |
| **ZeroClaw** | 41 | 50 | 23 | 41 | ❌ | ⭐⭐⭐⭐⭐ |
| **IronClaw** | 50 | 50 | 35 open* | 28 open* | ❌ | ⭐⭐⭐⭐ |
| **CoPaw** | 34 | 50 | 18 | 20 | ✅ v1.1.11 | ⭐⭐⭐⭐ |
| **NanoBot** | 10 | 34 | 4 | 15 | ❌ | ⭐⭐⭐⭐ |
| **Hermes Agent** | 50 | 50 | 50 | 43 | ❌ | ⭐⭐⭐ |
| **LobsterAI** | 0 | 25 | 0 | 2 | ✅ 2026.6.10 | ⭐⭐⭐⭐ |
| **PicoClaw** | 5 | 15 | 3 | 9 | ✅ nightly | ⭐⭐⭐ |
| **NanoClaw** | 2 | 11 | 2 | 8 | ❌ | ⭐⭐⭐ |
| **NullClaw** | 0 | 4 | 0 | 4 | ❌ | ⭐⭐ |
| **TinyClaw** | 0 | 0 | — | — | ❌ | Dormant |
| **Moltis** | 0 | 0 | — | — | ❌ | Dormant |
| **ZeptoClaw** | 0 | 0 | — | — | ❌ | Dormant |

*Health Score: Based on activity volume, bug fix velocity, release cadence, and community responsiveness.*  
*IronClaw open counts estimated from "50 issues updated, 15 closed" and "50 PRs updated, 7 merged/closed".*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale:** OpenClaw's 500 issues/PRs updated in 24 hours dwarfs the next largest project (ZeroClaw at 50). It is the clear community center of gravity, serving as the core reference implementation.
- **Release cadence:** Shipped v2026.6.6-beta.1 with explicit security boundary tightening across 10+ attack surfaces — a level of systematic security hardening no other project matched this cycle.
- **Platform breadth:** Telegram non-streaming progress, Discord multi-bot fix, Feishu image tool, QQBot support — OpenClaw covers more messaging channels than any competitor.
- **Community depth:** 31 comments on a single P1 bug (#25592, text leakage) and 470 open issues indicate a highly engaged, technically sophisticated user base actively stress-testing the system.

**Technical Approach Differences:**
- **Accessor seam architecture:** OpenClaw's SQLite migration via accessor pattern (#88838) is a novel architectural approach to session management not seen in other projects.
- **Diamond lobster prioritization:** Unique tiered severity system (P0/P1/P2 + diamond lobster/platinum hermit) allows fine-grained triage that NanoBot (flat label system) and CoPaw (no visible severity labels) lack.
- **Security-first release:** Unlike IronClaw's feature-first (Reborn architecture) or ZeroClaw's architecture-RFC focus, OpenClaw's latest release is explicitly a security release — a strategic differentiator.

**Community Size Comparison (estimated):**
- OpenClaw: ~10x the issue/PR volume of the next largest project
- ZeroClaw: 2nd highest volume, strong architectural RFC culture
- IronClaw / Hermes / CoPaw: Mid-tier, each with 25-50 daily updates
- NanoBot: Smaller but highly responsive (10 issues → 19 fixes merged)

---

## 4. Shared Technical Focus Areas

Emerging requirements that appear across multiple projects:

| Requirement | Projects Affected | Specific Needs |
|-------------|-------------------|----------------|
| **Message leakage prevention** | OpenClaw (#25592), Hermes (#43835, #44905), NanoBot (stream stalling), PicoClaw (#3094), ZeroClaw (#7370 fix) | Tool-call text appearing in chat, raw JSON leaks, NO_REPLY markers, duplicate messages |
| **Subagent reliability** | OpenClaw (#44925), NanoBot (#4290, #4279), ZeroClaw (#7263), CoPaw (#4923) | Silent completion loss, context inheritance, workspace isolation, notification aggregation |
| **Tool-call output control** | OpenClaw (#89850 persistProgress), NanoBot (stream stalled fix), ZeroClaw (#6721 MCP hang), IronClaw (#4704 approval loop) | Non-streaming progress, deferred loading, approval context, streaming rendering |
| **Docker/container friction** | OpenClaw (#31331), Hermes (#23402), ZeroClaw (#3642, #6760), NanoClaw (#2731) | Permissions, full images, host networking, rootless deployment |
| **Memory/context management** | OpenClaw (#22438 tiered bootstrap), NanoBot (#4274, #4270), IronClaw (#4743 context overflow), LobsterAI (#2145 compaction) | Cross-session contamination, compaction loss, overflow errors, tiered loading |
| **Multi-agent orchestration** | OpenClaw (#43367), Hermes (Matrix parity), ZeroClaw (#7415 turn engine), CoPaw (ToolCoordinator PR #5078) | Shared blackboard, capability profiling, unified turn engines |
| **Provider/model flexibility** | OpenClaw (#10687 dynamic discovery), NanoBot (#4291 subagent presets), Hermes (#6626 Gemma4), PicoClaw (#2951 web_search API), ZeroClaw (#7136 Kilo AI Gateway) | Per-skill routing, subagent model presets, provider-agnostic APIs |
| **Security hardening** | OpenClaw (v2026.6.6-beta.1), PicoClaw (#3085 SSRF guard), NanoClaw (#3 IPC namespace), ZeroClaw (remote admin PR #7344) | SSRF prevention, IPC isolation, permission boundaries, authentication hardening |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | NanoBot | Hermes Agent | CoPaw |
|-----------|----------|----------|----------|---------|--------------|-------|
| **Primary focus** | Reference implementation, security | Architecture innovation (WASM, plugins) | Full-stack Reborn rewrite | Lightweight, fast-iterate | Platform parity, i18n | Feature iteration, OAuth free models |
| **Target user** | Advanced operators, integrators | Developers, plugin authors | Enterprise teams | Quick-start individual users | Multi-platform enterprise | Chinese-market consumers |
| **Release philosophy** | Systematic security releases | Tracker-based milestone trains | Feature-driven (Reborn epic) | Rapid bug-fix accumulation | No recent stable release | Balanced feature + bug fix |
| **Architecture** | Monolithic with modular skills | Plugin/WASM future | Reborn microservices | Lightweight Python | Gateway + desktop apps | AgentScope-based |
| **Community culture** | Bug-hunting, stress-testing | RFC-driven, architectural | UX polish, crates.io pressure | High-responsiveness | Platform-specific contributors | Chinese-language majority |
| **Key differentiator** | Largest community, most channels | Future-proof WASM architecture | Reborn WebUI v2 / Config-as-Code | Fastest bug fix turnaround | Internationalization + Matrix | Free models, Xiaomi integration |

**Emerging Niche Players:**
- **LobsterAI:** Desktop-first (Windows/macOS), computer use MVP, notification channels — positioned as the "everyday desktop agent"
- **PicoClaw:** Cross-platform (Go-based), nightly builds, telemetry-focused — lightweight alternative for embedded systems
- **NanoClaw:** Skills-as-plugins model, uninstaller scripts — minimal configuration philosophy
- **NullClaw:** Lowest activity but clean backlog — potential for reinvention

---

## 6. Community Momentum & Maturity

**Tier 1: High-Velocity (Rapidly Iterating, 50+ daily updates)**
- **OpenClaw** — Extremely active, shipping security releases, but risk of reviewer burnout (470 open issues, 398 open PRs)
- **ZeroClaw** — Architecture-heavy iteration, 41 open PRs, strong RFC culture, 3 milestone trains active
- **IronClaw** — Feature-mature (Reborn), but crippled by crates.io publishing bottleneck (#3259, 37 days open)

**Tier 2: Active & Responsive (10-50 daily updates)**
- **NanoBot** — Highest merge-to-issue ratio (19 fixes for 10 issues), fastest bug turnarounds, growing user base
- **Hermes Agent** — High activity but growing backlog (50 open issues, 43 open PRs), platform parity work unblocking Matrix
- **CoPaw** — Balanced iteration with 30 PRs merged, two releases in 24h, strong Chinese-language ecosystem
- **LobsterAI** — Quiet issue tracker but 25 PRs updated, heavy dependency modernization, Windows/desktop focus

**Tier 3: Low Activity / Stabilizing**
- **PicoClaw** — Small team, nightly builds, consolidating cross-platform fixes
- **NanoClaw** — Modest contributions, documentation maturation, skills framework formalizing
- **NullClaw** — Four open PRs, zero issues, maintenance mode — could reawaken with maintainer attention

**Dormant:**
- TinyClaw, Moltis, ZeptoClaw — No activity in 24h; may be abandoned or waiting for next release cycle

**Maturity Assessment:**
- **Stabilizing:** LobsterAI, NullClaw, PicoClaw — fewer bugs, slower change
- **Rapidly maturing:** NanoBot, CoPaw — high fix velocity, active users
- **Still in flux:** ZeroClaw, IronClaw — architectural transitions creating churn
- **Established but scaled:** OpenClaw — mature but struggling with volume

---

## 7. Trend Signals

### Industry Trends Extracted from Community Feedback

**1. Security Boundaries Are the New Feature**
OpenClaw's beta release tightening 10+ attack surfaces, PicoClaw's SSRF guard (#3085), and NanoClaw's IPC namespace isolation (#3) signal a shift from "build features" to "lock down defaults." AI agent developers should prioritize:
- Sandbox inheritance boundaries
- Tool trust preflight checks
- Loopback authentication hardening
- Host environment variable sanitization

**2. Multi-Agent Orchestration Is Moving from Experimental to Production**
Users across OpenClaw, NanoBot, ZeroClaw, and CoPaw are reporting subagent failures as business-critical bugs, not niche edge cases. The demand for:
- Reliable subagent completion notifications (OpenClaw #44925)
- Context and workspace inheritance (ZeroClaw #7263)
- Aggregated vs. raw subagent output (NanoBot #4279)
- Tool coordination patterns (CoPaw PR #5078)

This indicates multi-agent workflows are becoming standard deployment patterns, not just experiments.

**3. "Platform Parity" Is the Competitive Battleground**
Hermes Agent's Matrix parity PRs (#18505-#18507), OpenClaw's Discord/Telegram/Feishu/QQBot coverage, and NanoBot's Slack mention scoping (#4289) show that users expect their agent to work identically across all communication channels. Key parity gaps:
- WhatsApp vs. Telegram vs. Signal vs. WeChat
- macOS vs. Windows vs. Linux desktop behavior
- TUI vs. WebUI vs. CLI consistency

**4. Configuration Complexity Is Driving User Churn**
Multiple projects report Docker configuration pain (OpenClaw #31331, Hermes #23402, ZeroClaw #3642), .env loading failures (NanoClaw #2730), and config schema surprises (ZeroClaw #7471). The ecosystem needs:
- Declarative configuration as code (IronClaw #3036)
- Validation fail-fast (NanoBot #4275)
- Tiered bootstrap files to reduce token waste (OpenClaw #22438)

**5. Developer Experience (DX) Is Becoming the Differentiator**
NanoBot's rapid bug fixes (same-day PRs for stream stalls, context pollution) are earning user trust. ZeroClaw's RFC culture attracts architectural contributors. In contrast, OpenClaw's 470 open issues create a perception of fragility despite its scale. DX trends:
- Error message clarity (CoPaw PR #5079 surfaces API errors)
- Test button for scheduled tasks (LobsterAI PR #1486)
- Rootless Docker examples (ZeroClaw PR #7475)
- Uninstall scripts (NanoClaw PR #2719)

**6. Local Model Support Is a Growing Requirement**
Users across projects report local model integration failures:
- Hermes #6626 (Gemma 4 tool calling)
- NanoClaw #2731 (Ollama blocked by egress lockdown)
- CoPaw #4989 (local Qwen regression)
- OpenClaw #38327 (Gemini "null to object" error)

As local models improve, agent frameworks must provide robust, tested provider integrations — not just token-level API abstractions.

**7. WASM and Plugin Architectures Are the Next Frontier**
ZeroClaw's v0.8.2 milestone (#7314) defining WASM plugin interfaces and IronClaw's programmatic MCP server config (#4735) signal a shift toward sandboxed, hot-swappable agent extensions. This could fundamentally change the plugin economy from skill directories to verifiable, secure WASM modules.

### Value for AI Agent Developers

1. **Prioritize reliability over features:** Users consistently rank silent failures (subagent loss, message leaks, stream stalls) higher than missing features.
2. **Invest in Docker/container experience:** It is the single most

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the project digest for NanoBot, generated from the GitHub data snapshot for 2026-06-11.

---

## NanoBot Project Digest — 2026-06-11

### 1. Today's Overview

The NanoBot project experienced a period of intense, high-velocity activity, processing 34 PRs (19 merged/closed) and 10 issues (6 closed) in the last 24 hours. The maintainers and community contributors focused heavily on stabilizing core features, particularly around context management, WebUI performance, and provider reliability. The rapid closure of several critical bugs indicates a strong operational cadence, though the lack of a new release suggests these fixes and features are being accumulated for a future stable version. The project appears to be in a robust state, actively responding to user-reported regressions from recent updates.

### 2. Releases

No new releases were made today. The latest version remains unreported in this data, indicating the project is currently in a pre-release phase, consolidating recent fixes and features.

### 3. Project Progress (Merged/Closed PRs)

Today saw significant progress across stability, infrastructure, and user experience.

- **Context and Memory Fixes:**
    - **Session Isolation:** A critical fix for `history.jsonl` cross-session contamination was merged ([PR #4274](https://github.com/HKUDS/nanobot/pull/4274)), preventing context pollution from other sessions.
    - **Idle Session Compaction:** A fix ([PR #4270](https://github.com/HKUDS/nanobot/pull/4270)) ensures that user corrections in recent messages are properly included in summaries, preventing information loss during automatic memory compaction.

- **Provider & Stability Fixes:**
    - **Stream Stalled Timeout:** A critical fix ([PR #4272](https://github.com/HKUDS/nanobot/pull/4272)) now allows the system to retry and fallback to alternate models when an LLM stream stalls, preventing truncated, useless replies.
    - **bwrap Sandbox:** A bug fix ([PR #4237](https://github.com/HKUDS/nanobot/pull/4237)) ensures the `$HOME` environment variable is correctly reset inside the sandbox, fixing permission errors for tools.

- **WebUI & Performance:**
    - **Transcript Size & Performance:** Two major PRs address WebUI storage: a fix to auto-compact oversized transcripts ([PR #4247](https://github.com/HKUDS/nanobot/pull/4247)) and a new segmented storage system ([PR #4278](https://github.com/HKUDS/nanobot/pull/4278)) that enables cheaper loading of large chat histories without data loss.
    - **Activity Duration:** A fix ([PR #4283](https://github.com/HKUDS/nanobot/pull/4283)) corrects the WebUI display of activity block durations, properly separating "thought" and "work" labels.

- **Infrastructure & Build:**
    - **Lazy Loading:** The Feishu channel now lazy-loads its heavy SDK, improving startup times ([PR #4277](https://github.com/HKUDS/nanobot/pull/4277)).
    - **Config Validation:** The system now fails fast on invalid config files ([PR #4275](https://github.com/HKUDS/nanobot/pull/4275)), preventing silent misconfigurations.
    - **Version Check:** The version check is now on-demand, removing background PyPI polling ([PR #4255](https://github.com/HKUDS/nanobot/pull/4255)).
    - **Path Prepend:** The `exec` tool now supports a `pathPrepend` config ([PR #4273](https://github.com/HKUDS/nanobot/pull/4273)), resolving a long-standing bug where system Python paths took priority over user-defined ones.

### 4. Community Hot Topics

The community's feedback highlights a tension between powerful features and the brittleness of the execution environment.

- **Context Pollution & Memory Loss:** The most discussed bug was the `history.jsonl` cross-session contamination ([Issue #4259](https://github.com/HKUDS/nanobot/issues/4259)), which caused the model to "remember" events from completely unrelated sessions. The rapid response and fix in [PR #4274](https://github.com/HKUDS/nanobot/pull/4274) was a major win for user trust.
- **Model Stability & Fallback Failures:** Users expressed significant frustration with models failing silently. A bug report about DeepSeek returning empty responses not triggering fallbacks ([Issue #4287](https://github.com/HKUDS/nanobot/issues/4287)) gained immediate attention, with a fix in [PR #4288](https://github.com/HKUDS/nanobot/pull/4288) treating empty responses as fallbackable.
- **Subagent Workflow Reliability:** Two related issues (spawned cronjob ending early [Issue #4290](https://github.com/HKUDS/nanobot/issues/4290) and the risk of LLM hallucinations from real-time subagent results [Issue #4279](https://github.com/HKUDS/nanobot/issues/4279)) show the community is actively pushing the boundaries of multi-agent workflows and finding the pain points. A fix for the cron issue is already proposed in [PR #4293](https://github.com/HKUDS/nanobot/pull/4293).

### 5. Bugs & Stability

Multiple stability issues were reported and addressed, indicating a strong focus on reliability.

| Issue | Title | Severity | Status | Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| [#4290](https://github.com/HKUDS/nanobot/issues/4290) | cronjob ends early when there's a subagent spawned | **High** | **Open** | [PR #4293](https://github.com/HKUDS/nanobot/pull/4293) proposed |
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | Empty model responses not triggering fallback | **High** | **Open** | [PR #4288](https://github.com/HKUDS/nanobot/pull/4288) proposed |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | Unexpected missing "sustained goal" context | **High** | **Open** | None identified |
| [#4261](https://github.com/HKUDS/nanobot/issues/4261) | OpenAICompatProvider: wrong token param for GPT-5.x | **Medium** | **Closed** | Fixed |
| [#4237](https://github.com/HKUDS/nanobot/issues/4237) | bwrap sandbox doesn't reset HOME env var | **Medium** | **Closed** | Fixed |
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | `history.jsonl` cross-session context pollution | **High** | **Closed** | [PR #4274](https://github.com/HKUDS/nanobot/pull/4274) |
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | LLM stream stalled for more than 90 seconds | **High** | **Closed** | [PR #4272](https://github.com/HKUDS/nanobot/pull/4272) |

### 6. Feature Requests & Roadmap Signals

User requests are trending toward more advanced multi-agent control and interface polish.

- **Subagent Model Presets:** A major feature request allows subagents to use a different model than the parent, controlled via configurable presets ([PR #4291](https://github.com/HKUDS/nanobot/pull/4291)). This is a strong candidate for the next release.
- **Aggregated Subagent Notifications:** To combat LLM hallucinations, a user proposed batching subagent results before sending them to the main agent ([Issue #4279](https://github.com/HKUDS/nanobot/issues/4279)). This is a sophisticated architectural request that may appear in a future minor version.
- **Slack Mention Channel Scoping:** A feature ([PR #4289](https://github.com/HKUDS/nanobot/pull/4289)) to require @mentions in allowed Slack channels adds fine-grained control for team environments.
- **WebUI Skill Activation:** The ability to activate skills via a slash command palette in the WebUI ([PR #4284](https://github.com/HKUDS/nanobot/pull/4284)) is a significant UX improvement.
- **File Management in Settings:** A user-driven feature for browsing and modifying agent files directly from the WebUI settings ([PR #4282](https://github.com/HKUDS/nanobot/pull/4282)) addresses a common operational pain point.

### 7. User Feedback Summary

- **Pain Points:** The primary user pain points stem from instability in the LLM execution pipeline. Users reported "useless" replies due to stream stalls, cross-session memory contamination making AI "confused," and workflows failing silently due to subagent scheduling or fallback logic. The `exec` tool's inability to install Python packages was a recurring frustration for developers.
- **Use Cases:** Users are pushing NanoBot into complex, multi-agent workflows (cron jobs with subagents) and professional content creation (article writing).
- **Satisfaction/Dissatisfaction:** While there is clear dissatisfaction with regressions in v0.2.0 (stream stalls), there is high satisfaction with the project's responsiveness. Several feedback issues were closed the same day or the next, demonstrating excellent project health and community support.

### 8. Backlog Watch

No critical items appear to be languishing. The maintainers have been highly responsive. However, two important issues remain open and warrant close attention:

- The subagent cron bug ([Issue #4290](https://github.com/HKUDS/nanobot/issues/4290)) and the empty response fallback bug ([Issue #4287](https://github.com/HKUDS/nanobot/issues/4287)) are both `High` severity and have associated PRs that could be merged.
- The "sustained goal" context issue ([Issue #4286](https://github.com/HKUDS/nanobot/issues/4286)) is new and has no fix PR yet, making it a candidate for immediate investigation to prevent user workflow disruption.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-11

## 1. Today’s Overview

The project is highly active, with **50 issues** and **50 pull requests** updated in the past 24 hours. All 50 issues remain open, reflecting a surge in bug reports and feature requests. On the PR side, 7 were merged or closed, while 43 remain open, indicating steady review but also a growing backlog. No new releases were cut today. The main themes are **Docker configuration pain**, **gateway reliability**, **accessibility gaps**, and **platform-specific regressions** (macOS, Windows, Telegram, WhatsApp). The community is contributing fixes at a fast pace, especially for WhatsApp, Windows, and guardrail improvements.

---

## 2. Releases

**None.** No releases were published in the last 24 hours.

---

## 3. Project Progress

Seven PRs were merged/closed today. The most significant:

- **[#43906 – feat(plugins): add hexis_appraisal plugin](https://github.com/NousResearch/hermes-agent/pull/43906)** — Opt-in metacognitive appraisal plugin (zero deps, fail-open) that gives agents per-turn self-evaluation.
- **[#38749 – fix(docker): optimize image size](https://github.com/NousResearch/hermes-agent/pull/38749)** — Added `.dockerignore` entries, separated build layers, and dropped development dependencies to shrink container images.
- **[#43926 – desktop: un-truncate slash row descriptions](https://github.com/NousResearch/hermes-agent/pull/43926)** — Makes long command descriptions in the desktop slash popover fully readable.
- **[#35127 – feat(i18n): add locale/language pack system](https://github.com/NousResearch/hermes-agent/pull/35127)** — Enterprise-grade internationalization framework for CLI and Gateway, enabling multilingual UI.

Other merged/closed PRs include smaller fixes for WhatsApp LID group support ([#43934](https://github.com/NousResearch/hermes-agent/pull/43934)), Windows `ps.exe` popup suppression ([#43933](https://github.com/NousResearch/hermes-agent/pull/43933)), and Chinese reasoning tag filtering ([#43932](https://github.com/NousResearch/hermes-agent/pull/43932)).

Several long-standing features advanced in open PRs: **Matrix gateway parity** ([#18505–#18507](https://github.com/NousResearch/hermes-agent/pull/18505)), **native OpenTUI TUI** ([#42922](https://github.com/NousResearch/hermes-agent/pull/42922)), **Windows computer_use backend** ([#43927](https://github.com/NousResearch/hermes-agent/pull/43927)), and **repeated-mutation guardrails** ([#43930](https://github.com/NousResearch/hermes-agent/pull/43930)).

---

## 4. Community Hot Topics

### Most Discussed Issues

1. **[Bug: Docker with HERMES_UID; permissions issue with Dashboard chat](https://github.com/NousResearch/hermes-agent/issues/23402)** (15 comments, 3 👍)  
   *User mmartial reports that Unraid Docker templates break due to `HERMES_UID` file ownership, making Dashboard chat unusable. A core usability blocker for container users.*

2. **[Accessibility for blind VoiceOver users](https://github.com/NousResearch/hermes-agent/issues/26689)** (9 comments)  
   *VoiceOver user describes near-total inaccessibility of the TUI and desktop app. High emotional investment – the user wants to use Hermes but cannot.*

3. **[Gemma 4 tool calling support](https://github.com/NousResearch/hermes-agent/issues/6626)** (5 comments, 3 👍)  
   *Parser configuration for Gemma 4 with vLLM is not documented or working. Multiple users have attempted integration; maintainer guidance is still missing.*

4. **[Portuguese (pt-BR) localization](https://github.com/NousResearch/hermes-agent/issues/40239)** (4 comments, 2 👍)  
   *Backend translations already exist; request is to expose them in the desktop UI. Strong community alignment with the newly merged i18n PR (#35127).*

### Most Active PRs

- **[Matrix gateway parity stack](https://github.com/NousResearch/hermes-agent/pull/18505) (P1)** — A 3-PR series for room isolation, native tools, and media/E2EE hardening. Open for 41 days, awaiting final review.
- **[feat(kanban): image paste in comments](https://github.com/NousResearch/hermes-agent/pull/37232)** — Adds clipboard/drag-drop image support to Kanban task comments.
- **[fix: temperature=0.0 for DeepSeek models](https://github.com/NousResearch/hermes-agent/pull/16715)** (P2) — Long-pending fix for DeepSeek reasoning parameters. Needs maintainer sign-off.

**Underlying needs:** Platform parity (Matrix, Windows), accessibility, and internationalization are recurring themes. Users are vocal about Docker usability and gateway stability.

---

## 5. Bugs & Stability

### P1 (Critical)

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#24187](https://github.com/NousResearch/hermes-agent/issues/24187) – SessionDB skips current turn after message repair | Conversation history becomes corrupted; messages lost. | None yet |
| [#43899](https://github.com/NousResearch/hermes-agent/issues/43899) – Cron jobs fail with "Model parameter is required" | Jobs ignore `model.default` from config.yaml. | None yet |
| [#43842](https://github.com/NousResearch/hermes-agent/pull/43842) – macOS: self-update kills launchd service | `refresh_launchd_plist` boots out the process mid‑update. | None yet |

### P2 (Moderate Severity)

- **Docker permissions** ([#23402](https://github.com/NousResearch/hermes-agent/issues/23402)) – Fix PR not yet identified.
- **Weixin token conflict** ([#17198](https://github.com/NousResearch/hermes-agent/issues/17198)) – Race condition during gateway restart.
- **macOS launchd restart** ([#43475](https://github.com/NousResearch/hermes-agent/issues/43475)) – `/restart` exits 0, launchd does not revive.
- **Telegram double messages** ([#43835](https://github.com/NousResearch/hermes-agent/issues/43835)) – Tool output and response body both sent.
- **WhatsApp LID group drop** ([#43830](https://github.com/NousResearch/hermes-agent/issues/43830)) – Fix PR [#43934](https://github.com/NousResearch/hermes-agent/pull/43934) merged today.
- **Bedrock streaming fault unreachable** ([#43915](https://github.com/NousResearch/hermes-agent/issues/43915)) – No retry on `internalServerException` from AWS.
- **Desktop ignores –profile** ([#43571](https://github.com/NousResearch/hermes-agent/issues/43571)) – Overwrites CLI sessions.
- **Webhook signature validation** ([#43575](https://github.com/NousResearch/hermes-agent/issues/43575)) – Fireflies V2 not supported.
- **MacOS self-upgrade kill** ([#43842](https://github.com/NousResearch/hermes-agent/issues/43842)) – Gateway-initiated update breaks service.

### P3 (Minor / Niche)

- Dashboard Hub skill install cancellation ([#43829](https://github.com/NousResearch/hermes-agent/issues/43829))
- Goal command swallowed in desktop ([#43476](https://github.com/NousResearch/hermes-agent/issues/43476))
- Memory bank/category stale on update/delete ([#43621](https://github.com/NousResearch/hermes-agent/issues/43621), [#43622](https://github.com/NousResearch/hermes-agent/issues/43622))
- Chinese reasoning tags missing from filter lists ([#43827](https://github.com/NousResearch/hermes-agent/issues/43827)) – Fix merged ([#43932](https://github.com/NousResearch/hermes-agent/pull/43932)).

**Observations:** Several P1/P2 bugs have no associated fix PR yet, indicating a need for maintainer attention. The merged fix for WhatsApp LID groups (#43934) is a good sign of community responsiveness.

---

## 6. Feature Requests & Roadmap Signals

### User-Requested Features (likely prioritized)

| Feature | Issue | Status |
|---------|-------|--------|
| VoiceOver / screen-reader accessibility | [#26689](https://github.com/NousResearch/hermes-agent/issues/26689) | No PR yet, but high community interest |
| Portuguese (pt-BR) desktop localization | [#40239](https://github.com/NousResearch/hermes-agent/issues/40239) | i18n infra merged (#35127); UI integration pending |
| Simultaneous local + remote backends | [#37876](https://github.com/NousResearch/hermes-agent/issues/37876) | Open, 3 comments |
| Graceful session resume on idle expiry | [#43008](https://github.com/NousResearch/hermes-agent/issues/43008) | Enhancement, no PR |
| Docker .env permissions configurable | [#43473](https://github.com/NousResearch/hermes-agent/issues/43473) | Open |

### Roadmap Signals (from open PRs)

- **Matrix gateway maturity** ([#18505–#18507](https://github.com/NousResearch/hermes-agent/pull/18505)) – Nearing completion; likely to land in next minor release.
- **Windows native support** – Computer use backend ([#43927](https://github.com/NousResearch/hermes-agent/pull/43927)) and `ps.exe` fix (#43933) are small steps toward parity.
- **Advanced tool guardrails** ([#43930](https://github.com/NousResearch/hermes-agent/pull/43930)) – Repeated-mutation halt and destructive-overwrite protection.
- **OpenTUI as default** ([#42922](https://github.com/NousResearch/hermes-agent/pull/42922)) – Experimental; could replace Ink TUI in a future version.

**Prediction for v0.17.0:** Expect merged Matrix parity, Windows computer_use, improved guardrails, and the i18n framework exposed in the desktop UI.

---

## 7. User Feedback Summary

- **Pain Points:**
  - Docker users face permissions and chat non‑functionality out‑of‑the‑box ([#23402](https://github.com/NousResearch/hermes-agent/issues/23402)).
  - Blind users cannot use the agent at all ([#26689](https://github.com/NousResearch/hermes-agent/issues/26689)).
  - Telemetry (WeChat, Telegram, WhatsApp) suffers from race conditions and version‑locked dependencies.
  - macOS service management is fragile: `/restart` and self-update break launchd control.
  - Desktop app ignores `--profile`, causing session contamination ([#43571](https://github.com/NousResearch/hermes-agent/issues/43571)).
  - Credential pools lack exponential backoff, leading to retry loops ([#15296](https://github.com/NousResearch/hermes-agent/issues/15296)).

- **Positive Signals:**
  - Large number of community‑authored PRs (Windows fixes, WhatsApp, Docker, guardrails) shows strong engagement.
  - Matrix and accessibility efforts indicate the community cares about inclusion and platform diversity.
  - i18n framework merges respond to a long‑standing request.

**Net sentiment:** The project is vibrant but stretched – users report real friction in common workflows, especially for Docker and macOS. The maintainer team would benefit from triaging P1 bugs and reviewing aging PRs.

---

## 8. Backlog Watch

Issues and PRs that have been open for weeks or months with minimal maintainer interaction:

| Item | Age | Why it matters |
|------|-----|----------------|
| [#6626](https://github.com/NousResearch/hermes-agent/issues/6626) – Gemma 4 tool calling | 63 days (since Apr 9) | Blocks users from a popular new model; has 5 comments and 3 👍. |
| [#15296](https://github.com/NousResearch/hermes-agent/issues/15296) – Credential pool backoff | 48 days (since Apr 24) | Causes unnecessary API 429 loops; affects reliability. |
| [#17198](https://github.com/NousResearch/hermes-agent/issues/17198) – Weixin token conflict | 43 days (since Apr 29) | Gateway restart broken for WeChat users. |
| [#18505–#18507](https://github.com/NousResearch/hermes-agent/issues/18505) – Matrix parity stack | 41 days (since May 1) | Large PR series awaiting review; blocks Matrix users. |
| [#16715](https://github.com/NousResearch/hermes-agent/issues/16715) – DeepSeek temperature fix | 45 days (since Apr 27) | Simple fix; stale approvals blocks merge. |
| [#9087](https://github.com/NousResearch/hermes-agent/issues/9087) – Nix home-manager module | 59 days (since Apr 13) | NixOS users waiting for per‑user service support. |

**Recommendation:** Prioritize review for #18505–#18507 and #16715 to unblock platform progress. Triaging #6626 (Gemma4) and #15296 (credential pool) would reduce user frustration.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-11

## 1. Today's Overview

The project is experiencing high activity with 15 pull requests updated and 5 issues updated in the last 24 hours, alongside a new nightly release. Six PRs were merged or closed, reflecting steady progress on bug fixes and minor features. The community is actively contributing code to resolve cross‑platform compatibility issues, strengthen security guards, and improve type safety. Overall project health appears robust, though several long‑standing issues and PRs remain open for maintainer review.

## 2. Releases

A new **nightly build** was published: [`v0.2.9-nightly.20260611.d955d5bb`](sipeed/picoclaw compare/v0.2.9...main).  
This is an automated build containing commits merged into the `main` branch since the last stable release. It may be unstable and should be used with caution. No breaking changes or migration notes were provided with this release.

## 3. Project Progress

Six pull requests were merged or closed today:

- **fix os.Root api on Windows issue** ([#3089](sipeed/picoclaw PR #3089)) — Resolves the `list_dir` “invalid argument” error on Windows caused by backslash path separators (fixes issue #2472).
- **fix(tools): block 198.18.0.0/15 in SSRF guard** ([#3085](sipeed/picoclaw PR #3085)) — Closes a security advisory by preventing SSRF bypass via RFC 2544 benchmark addresses.
- **fix: check strconv.Atoi and json.Unmarshal errors** ([#3043](sipeed/picoclaw PR #3043)) — Adds missing error checks in `seahorse` and evolution components.
- **fix: use function-type web_search for better API compatibility** ([#2951](sipeed/picoclaw PR #2951)) — Fixes HTTP 400 errors with OpenAI endpoints that reject `web_search_preview`.
- **fix: skip temperature parameter for claude‑opus‑4‑7 models** ([#2948](sipeed/picoclaw PR #2948)) — Prevents “temperature is deprecated for this model” errors.
- **feat: add debug trace viewer (picoclaw‑tracer)** ([#2945](sipeed/picoclaw PR #2945)) — Adds a standalone web UI for real‑time per‑turn LLM trace inspection.

Additionally, one security issue [#3077](sipeed/picoclaw Issue #3077) was closed without a code change being merged, implying the fix was already addressed.

## 4. Community Hot Topics

- **Windows path separator bug** ([#2472](sipeed/picoclaw Issue #2472)) — The most commented issue (5 comments, 1 👍) remains active. Users are reporting `list_dir` failures on Windows due to Go’s `os.Root` API requiring forward slashes. A fix PR (#3089) was merged today, so this pain point should be resolved in the next nightly build.
- **Asynchronous subagent duplicate messages** ([#3094](sipeed/picoclaw Issue #3094)) — Newly reported, zero comments yet, but describes a clear duplicate‑message issue in chat channels (e.g., Feishu/Telegram). Likely to draw community attention.
- **Agent collaboration bus** ([#2937](sipeed/picoclaw PR #2937)) — A large, stale PR (last updated 2026‑06‑10) proposes a first‑class inter‑agent communication system. It has not been merged, but the feature is a frequent community request.

*Underlying needs*: Strong demand for cross‑platform stability (Windows), elimination of message duplication in multi‑agent workflows, and advanced agent orchestration capabilities.

## 5. Bugs & Stability

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#3094](sipeed/picoclaw Issue #3094) | High | Duplicate messages when async subagent tasks complete, both raw and summarized output sent to user. Impacts Feishu/Telegram channels. | No PR yet. |
| [#3090](sipeed/picoclaw Issue #3090) | Medium | Panel fails on Safari < iOS 16.4; login renders incorrectly. Affects users on older iOS devices. | No PR yet. |
| [#2472](sipeed/picoclaw Issue #2472) | High | `list_dir` broken on Windows with “invalid argument” due to backslash separators. | Fixed in PR [#3089](sipeed/picoclaw PR #3089) (merged). |

A minor panic‑risk bug was also discovered and fixed in today’s PRs: unchecked type assertions in `CreateHTTPClient` ([#3095](sipeed/picoclaw PR #3095)), `native_search` ([#3091](sipeed/picoclaw PR #3091)), and `skills_install` ([#3092](sipeed/picoclaw PR #3092)) – all addressed.

## 6. Feature Requests & Roadmap Signals

- **New messaging gateways** ([#3093](sipeed/picoclaw Issue #3093)) — A user requests support for SimpleX, Wire, or Tox. These are decentralized/encrypted messaging protocols; likely low priority unless community traction grows.
- **Hardened launcher access control** ([#3083](sipeed/picoclaw PR #3083)) — Adds configurable localhost bypass and trusted proxy CIDRs. This is a security enhancement that could land in the next minor release.
- **Agent collaboration bus** ([#2937](sipeed/picoclaw PR #2937)) — Still open, with no recent activity from maintainers. If merged, it would be a major foundational feature for multi‑agent workflows.

**Prediction for next release**: The most likely candidates are the hardened launcher (#3083) and the DmScope persistence fix (#3067), both actively iterating.

## 7. User Feedback Summary

- **Windows users** expressed frustration with the path separator bug (#2472), which has now been fixed. Satisfaction should increase after the next nightly.
- **Subagent users** reported confusing duplicate messages (#3094) — a significant usability regression for those relying on async spawn.
- **Safari on iOS** users cannot access the panel (#3090), limiting mobile administration on older Apple devices.
- **Security‑conscious users** contributed by finding SSRF bypass vectors (#3077), which were promptly addressed.
- **Developers** continue to contribute quality improvements: many PRs today fix silent error handling, demonstrating a community that values code robustness and safety.

## 8. Backlog Watch

The following important items remain open without recent maintainer engagement:

- **Issue #2472** (stale): Now fixed via merged PR #3089, so it should be closed soon.
- **PR #2937** (stale): The agent collaboration feature is a large, unmerged PR with no maintainer review for over two weeks. Risk of bit‑rot.
- **PR #3067**: `DmScope` setting cannot be saved — a simple backend fix that has been open for two days with no merge.
- **PR #3087**: Relative workspace exec paths blocked incorrectly – opened 2026‑06‑09, no maintainer response yet.
- **Issue #3093**: Feature request for SimpleX/Tox – no discussion from maintainers, but may need roadmap prioritisation.

Maintainers should prioritise reviewing the DmScope fix (#3067) and the workspace exec path fix (#3087) to clear small blockers, and provide a status update on the collaboration bus PR (#2937).

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**NanoClaw Project Digest – 2026-06-11**

---

## 1. Today's Overview

The NanoClaw project shows moderate activity over the past 24 hours, with 11 pull requests updated (4 closed/merged) and 2 new issues opened. The community continues to contribute feature skills (guardrails, web search, container log persistence) and targeted bug fixes, particularly around environment variable loading and Telegram pairing. No new releases were published, but the volume of merged documentation and utility skills suggests the project is maturing its skills-based customization framework. One critical bug concerning egress lockdown breaking host-local Docker networking was opened and is already paired with a fix PR for the underlying `.env` loading issue.

---

## 2. Releases

No new releases were recorded in the last 24 hours.

---

## 3. Project Progress

**Merged / Closed PRs (4 total)**

- **[[follows-guidelines] feat: add uninstall.sh — per-copy uninstaller with confirmation, dry-run, and OneCLI agent cleanup (#2719)](https://github.com/nanocoai/nanoclaw/pull/2719)**  
  *Merged.* Adds a user-friendly uninstall script with safety features (confirmation, dry-run) and automatic cleanup of OneCLI agents. Improves operational hygiene for disposable deployments.

- **[docs: customizing intro, skills model, and skill guidelines (#2721)](https://github.com/nanocoai/nanoclaw/pull/2721)**  
  *Merged.* Introduces three new documentation pages (`customizing.md`, skills model overview, and skill guidelines) that formalise the “everything is a skill” customization contract. Aims to reduce merge conflicts on updates and standardise third‑party contributions.

- **[Secure IPC with per-group namespaces to prevent privilege escalation (#3)](https://github.com/nanocoai/nanoclaw/pull/3)**  
  *Closed (updated).* A foundational security fix (originally submitted in February) that isolates each agent group’s IPC directory to prevent privilege escalation. Its closure today signals maintainers are catching up on older, high‑value contributions.

- **[Opened against wrong repo — disregard (#2724)](https://github.com/nanocoai/nanoclaw/pull/2724)**  
  *Closed (mistake).* Immediately closed by the author; no impact.

---

## 4. Community Hot Topics

- **[Issue #1690 – Multi-runtime agent SDK abstraction (Claude + Codex + local models)](https://github.com/nanocoai/nanoclaw/issues/1690)**  
  *6 comments, 3 👍*  
  Proposed by `chipotoe-svg`, this issue describes an abstraction layer that allows different agent SDKs to be installed as modular skills (similar to channel skills like `/add-telegram`). The community shows strong interest in supporting multiple AI providers beyond the current Claude‑centric runtime. **Underlying need:** flexibility and vendor‑neutrality for agent backends.

- **[Issue #2731 – Egress lockdown hijacks host.docker.internal](https://github.com/nanocoai/nanoclaw/issues/2731)**  
  *Opened today, 0 comments*  
  Reports that enabling `NANOCLAW_EGRESS_LOCKDOWN=true` breaks all host‑local services (Ollama, proxies, etc.) reachable via `host.docker.internal`. This is a potential showstopper for users running local model endpoints. A fix PR (#2730) is already open.

- **[PR #2211 – Tool-visibility skill for live tool-call previews](https://github.com/nanocoai/nanoclaw/pull/2211)**  
  *Open since May 3, updated today*  
  Adds PreToolUse/PostToolUse hooks to surface tool calls in the chat. The PR has been reworked as a self‑contained skill per guidelines, indicating the community is actively iterating on observability features.

---

## 5. Bugs & Stability

| Severity | Issue / PR | Description | Fix Status |
|----------|-----------|-------------|------------|
| **Critical** | [#2731 – Egress lockdown hijacks host.docker.internal](https://github.com/nanocoai/nanoclaw/issues/2731) | `EGRESS_LOCKDOWN` (OneCLI gateway) attaches to the Docker bridge, breaking all `host.docker.internal` routes. Agents lose access to host‑local services (Ollama, proxies). | Root cause identified in [#2730](https://github.com/nanocoai/nanoclaw/pull/2730) (env loading) – no complete fix yet. |
| **High** | [#2730 – NANOCLAW_* flags never reach process.env under launchd/systemd](https://github.com/nanocoai/nanoclaw/pull/2730) | Flags read from `process.env` ignore `.env` file when the host is launched by `launchd`/`systemd`. Egress lockdown and other gated features silently fail. | PR #2730 open (directly patches `egress-lockdown.ts`). |
| **Medium** | [#2728 – Telegram pairing does not create `messaging_group_agents` row](https://github.com/nanocoai/nanoclaw/pull/2728) | Pairing with `--intent wire-to:<folder>` succeeds but never wires the agent into the group, rendering the intent ineffective. | PR #2728 open with fix. |
| **Low** | [#2729 – Telegram skill doc mismatch: status blocks refer to non‑existent steps](https://github.com/nanocoai/nanoclaw/pull/2729) | The `add-telegram` SKILL.md references status blocks that the setup step never emits, confusing first‑time users. | PR #2729 open with corrected documentation. |

---

## 6. Feature Requests & Roadmap Signals

Several user‑submitted feature PRs and skills hint at the direction of the next release:

- **Container log persistence** ([#2727](https://github.com/nanocoai/nanoclaw/pull/2727)) – Saves agent container stdout/stderr to disk for debugging. Already merged in a downstream fork; now proposed for upstream.
- **Per‑agent‑group input/output guardrails** ([#2726](https://github.com/nanocoai/nanoclaw/pull/2726)) – Deterministic regex/keyphrase blocking for prompt injection and credential leaks, with a quarantine audit trail.
- **Multi‑provider web search + extraction** ([#2725](https://github.com/nanocoai/nanoclaw/pull/2725)) – A self‑contained utility skill (`web-search-plus`) avoiding MCP dependency.
- **Multi‑runtime support** ([#1690](https://github.com/nanocoai/nanoclaw/issues/1690)) – The most‑upvoted request; likely to influence the 0.x roadmap.

**Prediction:** The next minor version will likely include container log persistence, the guardrails skill, and the documentation foundation for the skills model (already merged). Multi‑runtime abstraction may appear as an experimental feature behind a flag.

---

## 7. User Feedback Summary

The community is actively contributing both code and high‑quality bug reports:

- **Pain points:**  
  - `.env` loading is unreliable under system service managers – `sturdy4days` reported that critical security flags are silently ignored.  
  - Egress lockdown is too aggressive, cutting off legitimate local services – a fundamental trade‑off between security and usability.  
  - Telegram pairing has a wiring gap that makes the “wire‑to” intent non‑functional.

- **Positive signals:**  
  - Skills development is thriving: three new utility skills (uninstall, guardrails, web search) were contributed in the last week.  
  - Documentation improvements are welcomed – the “customizing” docs (#2721) standardise the contribution model.  
  - Older security‑related PRs (#3) are finally being closed, showing maintainer bandwidth is increasing.

- **Key use case:** Deploying agents with local LLMs (Ollama) or host‑side proxies is a recurring theme, yet current networking isolation clashes with that setup – a tension the project must resolve.

---

## 8. Backlog Watch

- **[Issue #1690 – Multi-runtime abstraction](https://github.com/nanocoai/nanoclaw/issues/1690)**  
  *Created 2026-04-07, 6 comments, 3 👍*  
  No maintainer response yet. This is the most‑desired feature based on reactions, but it has been open for over two months without triage. The community may be waiting for a decision on whether to incubate as a core feature or leave it as a third‑party skill.

- **[PR #2211 – Tool-visibility skill](https://github.com/nanocoai/nanoclaw/pull/2211)**  
  *Created 2026-05-03, updated today*  
  An older, feature‑rich PR that has been revised per guidelines but still awaits review. Continued updates suggest the author is eager to merge.

- **[Issue #2731 – Egress lockdown bug](https://github.com/nanocoai/nanoclaw/issues/2731)**  
  *Just opened, but urgent – no maintainer comment yet.* The associated fix PR (#2730) only addresses the `.env` loading; the actual Docker networking fix may require a separate discussion.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-11

## 1. Today's Overview

No new issues or releases were recorded in the last 24 hours. The project saw activity from four open pull requests, all created on 2026-06-10, which address bug fixes and minor feature enhancements. With zero open issues and no merged changes today, the project appears to be in a low-activity, maintenance-focused phase. The open PRs target several stability and configuration gaps that could improve the agent runner, gateway, and cron delivery subsystems.

## 2. Releases

No new releases were published today. The latest release history remains unchanged.

## 3. Project Progress

No pull requests were merged or closed today. All four open PRs remain under review:

| PR | Title | Author | Status |
|----|-------|--------|--------|
| [#951](https://github.com/nullclaw/nullclaw/pull/951) | fix(agent_runner): suppress stderr initialization logs on agent failure | vernonstinebaker | Open |
| [#949](https://github.com/nullclaw/nullclaw/pull/949) | fix: make queue\_mode configurable from config.json, default to latest | vernonstinebaker | Open |
| [#948](https://github.com/nullclaw/nullclaw/pull/948) | fix cron agent delivery attribution | DonPrus | Open |
| [#950](https://github.com/nullclaw/nullclaw/pull/950) | fix(gateway): move port probe before allocations to prevent test leak | addadi | Open |

No features or fixes have advanced to the main branch today.

## 4. Community Hot Topics

No issues or pull requests received comments or reactions in the last 24 hours. The four open PRs, all with zero comments and zero 👍 reactions, represent the entirety of recent community contribution. The most notable technical discussions are embedded in the PR summaries themselves:

- **PR #951** – Suppresses spurious stderr logs (memory plan, MCP server registration, channel startup) from being posted as agent responses when the child process exits non-zero.
- **PR #949** – Introduces a `agent.default_queue_mode` configuration field, making the queue mode user-configurable via `config.json` with a fallback to `latest`.
- **PR #948** – Ensures cron delivery origin metadata is passed into spawned agent processes, fixing attribution of `agent_start` events.
- **PR #950** – Fixes a test leak where `gateway.run()` allocations were left uncleaned when an `AddressInUse` error occurred early.

Given the lack of community response, the project team may benefit from explicitly requesting review or feedback on these changes.

## 5. Bugs & Stability

All four open PRs address bugs or stability concerns. They are ranked by potential user impact:

| Severity | Bug Description | Fix PR | Notes |
|----------|----------------|--------|-------|
| **Medium** | Agent failure causes stderr initialization logs to be posted to channels as if they were agent responses. | [#951](https://github.com/nullclaw/nullclaw/pull/951) | Could confuse users and clutter message history. Fix restricts stderr fallback to success-only cases. |
| **Medium** | Cron agent delivery lacks origin metadata, breaking `agent_start` attribution to the correct delivery channel/account. | [#948](https://github.com/nullclaw/nullclaw/pull/948) | Affects audit trails and routing for scheduled agent runs. |
| **Low** | `queue_mode` cannot be set via `config.json`, forcing users to rely on defaults or runtime overrides. | [#949](https://github.com/nullclaw/nullclaw/pull/949) | Enhancement-fix; no crash or data loss. |
| **Low** | Gateway test leaks memory/state when `AddressInUse` occurs because allocations happen before port probe. | [#950](https://github.com/nullclaw/nullclaw/pull/950) | Only affects test environments with real config files; not a production bug. |

No new bugs were reported via issues today.

## 6. Feature Requests & Roadmap Signals

The only user-facing feature request visible in today’s data is the **configurable default queue mode** proposed in PR #949. By adding `agent.default_queue_mode` to `config.json`, users gain the ability to control initial queue behavior for new sessions without code changes. This is a low-risk, high-usability change that is likely to be merged in the next release.

No other feature requests were voiced in issues or PR discussions today. The project roadmap appears focused on stability and incremental configuration improvements.

## 7. User Feedback Summary

No direct user feedback (comments, bug reports, or feature requests) appeared in the last 24 hours. However, the PR summaries imply several pain points that users may have encountered:

- **Misleading agent responses** (PR #951) – Users reported seeing initialization logs posted as agent replies when the agent process failed.
- **Missing cron attribution** (PR #948) – Scheduled agent runs were not properly associated with the calling channel/account, hindering tracking.
- **Inflexible queue mode** (PR #949) – Users had no way to set the default queue mode in persistent configuration.
- **Test environment fragility** (PR #950) – Developers running tests with real configs faced resource leaks on address conflicts.

These are addressed by the open PRs, indicating the maintainers are responsive to community-observed defects even without formal issue reports.

## 8. Backlog Watch

There are no open issues in the repository (`0 items`). This suggests either a very clean backlog or low community engagement in reporting problems. No long-unanswered issues or PRs requiring maintainer attention were identified. The four open PRs are recent (24–48 hours) and are still awaiting review or merge. The absence of any stale items is a positive health indicator, though it also means there is no pending work visible beyond these PRs.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-11

## 1. Today’s Overview

IronClaw saw **very high activity** over the past 24 hours: 50 issues and 50 PRs were updated, with 15 issues closed and 22 PRs merged or closed. The team is heavily focused on **shipping the Reborn architecture** — WebUI v2, provider configuration, agent-loop auth-gate resume, and Slack delivery — while simultaneously fixing a wave of UX bugs discovered during local testing. No new releases were published today, but a long‑standing release PR (#3708) has been open since May 16 and is a blocker for pushing `0.25.0`–`0.27.0` to crates.io. Overall project health is strong but the community is growing impatient for crates.io updates to address downstream CVEs.

## 2. Releases

**No new releases today.**  
The latest tags are `ironclaw-v0.27.0` (April 29) but only `0.24.0` is on crates.io, a situation flagged in Issue #3259.

## 3. Project Progress

Merged/closed PRs today (7 total) advanced several critical areas:

| PR | Title | Impact |
|----|-------|--------|
| [#4745](https://github.com/nearai/ironclaw/issues/4745) | Refactor(reborn): back automations panel facade with TriggerRepository | Removes synthetic capability‑dispatch from panel reads, simplifies architecture |
| [#4743](https://github.com/nearai/ironclaw/issues/4743) | Fix NEAR context overflow classification | Properly classifies `prompt too long` errors as `ContextLengthExceeded` |
| [#4742](https://github.com/nearai/ironclaw/issues/4742) | Fix manual token runtime credential selection | Threads `ManualToken` vs `OAuth` mode through authorization obligations |
| [#4652](https://github.com/nearai/ironclaw/issues/4652) | Document Reborn serve/WebUI flow + launcher script | Adds `run-reborn-webui.sh` and corrects stale docs |
| [#4730](https://github.com/nearai/ironclaw/issues/4730) | Personal triggered‑event delivery: Slack DM end to end | User can pair Slack, get DM delivery target, and receive triggered runs |
| [#4739](https://github.com/nearai/ironclaw/issues/4739) | Enable Slack for QA Railway Reborn | Enables Slack in Docker configs for QA deployment |
| [#4717](https://github.com/nearai/ironclaw/issues/4717) | Restore WebUI v2 always‑approval affordance | Adds persistent approval policies for product‑workflow gates |

Additionally, a batch of issues were closed (e.g., #3283, #4594, #3615, #4604, #4585, #4603, #4642, #4673, #4734) indicating progress on Reborn API migration, config diagnostics, auth/security audit, E2E coverage, and provider configuration.

## 4. Community Hot Topics

The most active discussions revolve around **crates.io publishing** and **Reborn migration**:

- **[Issue #3259](https://github.com/nearai/ironclaw/issues/3259)** (14 comments) — Publish 0.25.0–0.27.0 to crates.io; downstream pinned to 0.24.0 due to wasmtime 28.x CVEs. **Underlying need:** urgent security mitigation and unblocking consumers stuck on old versions.
- **[Issue #3036](https://github.com/nearai/ironclaw/issues/3036)** (6 comments) — Configuration‑as‑Code epic for tenant blueprints. **Need:** declarative, auditable configuration instead of hand‑editing `.env` and JSON.
- **[Issue #3283](https://github.com/nearai/ironclaw/issues/3283)** (3 comments, now closed) — Migrate OpenAI‑compatible APIs onto Reborn. **Need:** preserve external API compatibility while adopting Reborn workflow model.
- **[Issue #4703](https://github.com/nearai/ironclaw/issues/4703)** (2 comments) — NEAR AI provider cannot be used after successful setup. **Need:** reliability in provider onboarding.

No PRs have high comment counts (most show 0), but the release PR [#3708](https://github.com/nearai/ironclaw/issues/3708) and the Trace Commons onboarding PR [#4559](https://github.com/nearai/ironclaw/issues/4559) are gathering attention.

## 5. Bugs & Stability

Today’s bug reports are concentrated on **Reborn WebUI v2 usability** and **provider configuration**. Severity ranking:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Critical** | [#4741](https://github.com/nearai/ironclaw/issues/4741) | Corrupt/low‑entropy local‑dev master key causes opaque “Invalid master key” error, preventing server startup | No fix yet |
| **Critical** | [#4729](https://github.com/nearai/ironclaw/issues/4729) | NEAR AI login broken for local/desktop builds: `private.near.ai` rejects non‑origin callback | No fix yet |
| **High** | [#4704](https://github.com/nearai/ironclaw/issues/4704) | `builtin.http` approval loop repeats after `invalid_input` failure without actionable error details | No fix yet |
| **High** | [#4701](https://github.com/nearai/ironclaw/issues/4701) | Approval modal lacks context for `builtin.http` tool requests (shows only Approve/Deny) | No fix yet |
| **High** | [#4683](https://github.com/nearai/ironclaw/issues/4683) | Generic “driver unavailable” error shown for invalid model configuration | No fix yet |
| **High** | [#4706](https://github.com/nearai/ironclaw/issues/4706) | Authorization flows (NEAR AI SSO, ChatGPT) do not recover after failed/cancelled sign‑in | No fix yet |
| **Medium** | [#4673](https://github.com/nearai/ironclaw/issues/4673) | NEAR AI provider save fails silently after Test connection (CLOSED, fixed by [#4731](https://github.com/nearai/ironclaw/issues/4731)) | ✅ Fixed |
| **Medium** | [#4724](https://github.com/nearai/ironclaw/issues/4724) | Unsent draft lost when leaving New Conversation | No fix yet |
| **Medium** | [#4725](https://github.com/nearai/ironclaw/issues/4725) | Composer remains interactive while in Working state (disabled but hover styles still appear) | No fix yet |
| **Medium** | [#4722](https://github.com/nearai/ironclaw/issues/4722) | Conversation messages don’t show user or assistant identity (IC placeholder disappears) | No fix yet |
| **Low** | [#4734](https://github.com/nearai/ironclaw/issues/4734) | Agent avatar shows “IC” instead of IronClaw icon (CLOSED) | ✅ Fixed |
| **Low** | [#4708](https://github.com/nearai/ironclaw/issues/4708) | Generated code blocks lack syntax highlighting | No fix yet |
| **Low** | [#4707](https://github.com/nearai/ironclaw/issues/4707) | Conversation page font size too small | No fix yet |
| **Low** | [#4723](https://github.com/nearai/ironclaw/issues/4723) | New conversation composer hover highlights only top border | No fix yet |

Also reported: the `slack` tool’s `parameters_schema()` omits typed fields ([#4740](https://github.com/nearai/ironclaw/issues/4740)), strict‑mode providers’ null‑for‑unset optionals rejected by capability‑port validation ([#4642](https://github.com/nearai/ironclaw/issues/4642), CLOSED), and builtin.http approval loop UX.

## 6. Feature Requests & Roadmap Signals

Several feature‑oriented issues and PRs point to the near‑term roadmap:

- **[#3036](https://github.com/nearai/ironclaw/issues/3036)** — Configuration‑as‑Code epic (tenant blueprints, use‑case harnesses). Likely to be a major 0.30.0 theme.
- **[#4632](https://github.com/nearai/ironclaw/issues/4632)** — Build out Reborn WebUI v2 end‑to‑end smoke coverage. Critical for QA.
- **[#4700](https://github.com/nearai/ironclaw/issues/4700)** — Enable NEAR AI MCP automatically when NEAR AI credentials are configured. Low‑hanging usability improvement.
- **[#4747](https://github.com/nearai/ironclaw/issues/4747)** — Unify pending gate‑resume records and move replay payload out of checkpointed state. Architecture refinement.
- **[#4559](https://github.com/nearai/ironclaw/issues/4559)** (PR) — Agent‑driven Trace Commons onboarding via invite link. A new integration.
- **[#4735](https://github.com/nearai/ironclaw/issues/4735)** (PR) — Programmatic MCP server config + PATCH update. Extends Extensions API.
- **[#4738](https://github.com/nearai/ironclaw/issues/4738)** (PR) — Attachment web UX on WebChat v2 SPA. Enables file uploads in chat.
- **[#4670](https://github.com/nearai/ironclaw/issues/4670)** (PR) — Bridge inbound bytes into transcript AttachmentRefs. Backend for attachments.
- **[#4588](https://github.com/nearai/ironclaw/issues/4588)** (PR) — Observability seams: trajectory observer + LLM provider injection. Supports external benchmarking.

Prediction for next minor release (0.28.0 or 0.30.0): Reborn WebUI v2 with attachment support, MCP extension configuration, improved auth‑gate resume, and the Configuration‑as‑Code blueprint framework.

## 7. User Feedback Summary

Users (especially local testers) report several pain points:

- **crates.io freeze** – Downstream consumers cannot upgrade past 0.24.0, missing security fixes for wasmtime CVEs.
- **Reborn WebUI setup friction** – Provider configuration fails silently (#4673), corrupt master keys crash the server (#4741), OAuth login is broken (#4729), and model misconfigurations yield misleading errors (#4683).
- **Poor UX for tool approvals** – `builtin.http` approval lacks context (#4701) and can loop after failure (#4704). Users want more transparency.
- **UI polish gaps** – No syntax highlighting, tiny font, lost drafts, missing identity avatars, and inconsistent hover states degrade the chat experience.
- **Auth flows are fragile** – Cancelled sign‑ins leave users unable to retry (#4706).

Satisfaction signals: contributors are actively fixing issues (e.g., 7 PRs merged today), and the community is engaged in shaping Configuration‑as‑Code and MCP extensions.

## 8. Backlog Watch

The following high‑importance items need maintainer attention:

| Item | Age | Why it matters |
|------|-----|----------------|
| **[#3259](https://github.com/nearai/ironclaw/issues/3259)** – Publish 0.25.0–0.27.0 to crates.io | Opened 2026-05-05 (37 days) | Downstream blocked by `0.24.0`; wasmtime CVEs unfixed. Release PR [#

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-11

## 1. Today’s Overview
The LobsterAI project saw high activity with 25 PRs updated in the last 24 hours, of which 23 were merged or closed. A new patch release (2026.6.10) was published, adding data migration, local callback login, and initial OpenClaw surface settings. No new issues were created, indicating the current focus is on stabilizing merged features and closing long‑standing PRs. Two PRs remain open, one fixing a Windows installer issue and the other a dependency update, both awaiting further review.

## 2. Releases
**New release: [LobsterAI 2026.6.10](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.10)**  
*Released June 10, 2026*  
- **feat(data-migration):** Adds user data backup and restore functionality.  
- **feat(auth):** Introduces local callback login flow.  
- **feat(settings):** Begins surfacing OpenClaw‑related settings (partially listed).  

No breaking changes or migration notes were included in the changelog. Users should upgrade to obtain these features.

## 3. Project Progress
Today’s merged/closed PRs advanced several core areas:

- **Computer Use MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) – merged: Adds a built‑in Computer Use kit for Windows x64, including marketplace metadata, skill bundle integrity, install/uninstall logic, and a runtime lifecycle with MCP server bridge (app/window listing, app launching, screenshot capture).  
- **Context continuity after compaction** ([PR #2145](https://github.com/netease-youdao/LobsterAI/pull/2145)) – merged: Enhances Cowork session context compaction so agents maintain task state after OpenClaw compresses chat history; adds diagnostic tools, session‑scoped task state, and lightweight workspace tracking.  
- **Portal fallback fix** ([PR #2144](https://github.com/netease-youdao/LobsterAI/pull/2144)) – merged: Updates authentication portal fallback URLs to point to the new LobsterAI portal domains, covering both test and production endpoints.  
- **Windows update fix** ([PR #2141](https://github.com/netease-youdao/LobsterAI/pull/2141)) – merged: Resolves AppImage update flow on Windows.  
- **Task completion notifications** ([PR #2134](https://github.com/netease-youdao/LobsterAI/pull/2134)) – merged: Restores LobsterAI from task completion notifications when the main window is closed/destroyed, waits for renderer notification handler readiness, and preserves macOS Notification Center actionability.  
- **Styling polish** ([PR #2139](https://github.com/netease-youdao/LobsterAI/pull/2139)) – merged: Refines markdown and code block themes (One Dark/Light syntax highlighting, word wrap for prose languages, expanded virtualized rendering limits) and adds a model selector `enableLargePreview` toggle.  
- **Scheduled task improvements** (multiple stale PRs closed):  
  - [PR #1486](https://github.com/netease-youdao/LobsterAI/pull/1486) – “Test Task” button in task creation form.  
  - [PR #1489](https://github.com/netease-youdao/LobsterAI/pull/1489) – Local macOS notification channel for scheduled tasks.  
  - [PR #1490](https://github.com/netease-youdao/LobsterAI/pull/1490) – Fix for delivery channel not updating after edit.  
- **Skill disabling enforcement** ([PR #1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [PR #1501](https://github.com/netease-youdao/LobsterAI/pull/1501)) – closed: Disabled skills are now excluded from system prompts and active skill lists, preventing unintentional invocation.  
- **Session pruning** ([PR #1499](https://github.com/netease-youdao/LobsterAI/pull/1499)) – closed: Adds automatic session trimming to avoid model context‑window overflow.  
- **Exit behavior on Windows** ([PR #1497](https://github.com/netease-youdao/LobsterAI/pull/1497)) – closed: Allows users to choose “minimize to tray” or “quit app” on window close (Windows only).  
- **Markdown editor for Agent guides** ([PR #1503](https://github.com/netease-youdao/LobsterAI/pull/1503)) – closed: Replaces plain‑text `<textarea>` with a rich Markdown editor for `IDENTITY.md`, `SOUL.md`, and `USER.md` in Settings.

A batch of dependency updates (Electron, CI actions) were also merged, bringing the project to modern tooling.

## 4. Community Hot Topics
No issues were reported or updated in the last 24 hours. Among PRs, the most notable are:

- **Computer Use MVP** ([PR #2143](https://github.com/netease-youdao/LobsterAI/pull/2143)) – while merged today, this large PR generated substantial discussion (undefined comment count, but high activity). The feature enables agents to control desktop apps, indicating strong community interest in real‑world automation.  
- **Context continuity** ([PR #2145](https://github.com/netease-youdao/LobsterAI/pull/2145)) – addresses a core pain point: losing agent state after context compaction. The underlying need is for reliable long‑running Cowork sessions without manual restoration.  
- **Scheduled task notification channels** ([PR #1489](https://github.com/netease-youdao/LobsterAI/pull/1489)) – users wanted local macOS notifications that actually work, showing demand for platform‑specific integration.

All PRs received zero reactions (👍 count zero), which may reflect a small reviewer base rather than lack of interest.

## 5. Bugs & Stability
No new bugs were reported as issues today. The following fixes were merged or are open:

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | Windows update in‑app fails | Fixed | [#2141](https://github.com/netease-youdao/LobsterAI/pull/2141) |
| **High** | NSIS installer destructive init on Windows / engine loading page glitch | **Open** | [#2142](https://github.com/netease-youdao/LobsterAI/pull/2142) |
| **Medium** | Portal fallback URLs pointing to old domains | Fixed | [#2144](https://github.com/netease-youdao/LobsterAI/pull/2144) |
| **Medium** | Disabled skills still active in cowork chat | Fixed | [#1485](https://github.com/netease-youdao/LobsterAI/pull/1485), [#1501](https://github.com/netease-youdao/LobsterAI/pull/1501) |
| **Medium** | Scheduled task notification channel not persisting after edit | Fixed | [#1490](https://github.com/netease-youdao/LobsterAI/pull/1490) |

The open PR #2142 (NSIS destructive init) remains critical for Windows users; it also proposes a redesigned engine loading page.

## 6. Feature Requests & Roadmap Signals
Several merged PRs indicate near‑term roadmap priorities:

- **Computer Use (MVP)** – now merged, likely to be refined in coming releases.  
- **Data backup & migration** (released in 2026.6.10) – user‑requested capability to safeguard and transfer settings.  
- **Local callback login** – reduces dependency on external authentication.  
- **Task completion notifications** – improves user experience for background agent tasks.  
- **Rich Markdown editor for Agent guides** – a quality‑of‑life improvement for power users.

Based on the PR backlog, future versions may include:
- Full Electron version bump (PR #1277 open) for security and performance.
- Further Windows‑specific fixes (installer, update, tray behavior).
- Integration of scheduled task features with more notification channels (e.g., webhook).

No specific user‑requested feature requests were filed as issues today, but the merged PRs address frequently requested areas (session pruning, skill disabling, notification reliability).

## 7. User Feedback Summary
Indirect feedback from PR descriptions reveals several pain points:

- **Agent state lost after compaction** – users reported that agents forget context after long conversations; PR #2145 directly addresses this.  
- **Disabled skills still invoked** – a “silent” bug that caused unexpected behavior; now fixed.  
- **Scheduled tasks notifications not working** – macOS users saw no notification or incorrect behavior; fixed by PR #1489.  
- **Task form lacks “test run”** – users had to save & run manually; now has a dedicated button (PR #1486).  
- **Session overflow errors** – model context window exceeded; pruned automatically (PR #1499).

Satisfaction is implied by the high merge velocity – most reported issues receive a fix within days to a few weeks.

## 8. Backlog Watch
- **[PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** – **Open** (dependabot). Bumps Electron from 40.2.1 to 42.3.3 and electron‑builder. Originally created April 2, 2026. Last updated June 10 (CI re‑run). Requires maintainer review/merge to keep dependencies current.  
- **[PR #2142](https://github.com/netease-youdao/LobsterAI/pull/2142)** – **Open** (fisherdaddy). Fixes NSIS destructive init and redesigns engine loading page. Created June 10, 2026. This is a recent critical fix for Windows users; should be prioritized.

No other issues or PRs have been unanswered for more than a month. The project maintains a healthy triage cadence.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-11

## 1. Today's Overview
CoPaw saw high activity over the past 24 hours, with **34 issues** updated (18 open, 16 closed) and **50 pull requests** updated (20 open, 30 merged/closed). Two releases were published: a stable **v1.1.11** and a beta **v1.1.11-beta.3**. The project is in a rapid iteration phase, balancing new features (OAuth free models, self-evolving skills) with critical bug fixes, especially around Windows desktop startup failures and tool‑call reliability. The community is actively reporting regressions and requesting enhancements like visual model fallback and better sub‑agent visibility.

## 2. Releases

### **v1.1.11** (stable)
[Release link](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11)
- **Free Model OAuth**: Zero‑configuration free models with one‑click OAuth authentication ([#5049](https://github.com/agentscope-ai/QwenPaw/pull/5049))
- **Xiaomi MiMo Provider**: Added Xiaomi MiMo Token Plan as a built‑in provider ([#4722](https://github.com/agentscope-ai/QwenPaw/pull/4722))
- No explicit breaking changes or migration notes.

### **v1.1.11-beta.3** (pre‑release)
[Release link](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11-beta.3)
- Removed redundant channel‑tests CI workflow ([#5056](https://github.com/agentscope-ai/QwenPaw/pull/5056))
- **Enhanced make‑skill flow** to support self‑evolving skill creation ([#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857))
- Other skill‑related improvements.

No release mentions breaking changes; updates appear backward‑compatible.

## 3. Project Progress (Merged/Closed PRs)
**30 PRs** were merged or closed yesterday. Highlights include:

| PR | Description | Status |
|----|-------------|--------|
| [PR #5080](https://github.com/agentscope-ai/QwenPaw/pull/5080) | Release v1.1.11 | Merged |
| [PR #5083](https://github.com/agentscope-ai/QwenPaw/pull/5083) | Use certifi CA bundle for Windows build verification | Merged |
| [PR #5082](https://github.com/agentscope-ai/QwenPaw/pull/5082) | Pin aiohttp<=3.14.0 to fix Windows SSL error | Merged |
| [PR #5084](https://github.com/agentscope-ai/QwenPaw/pull/5084) | Compile‑check discord after conda‑unpack (reverted later) | Merged |
| [PR #5079](https://github.com/agentscope-ai/QwenPaw/pull/5079) | Surface original API error reason in user‑facing message | Merged |
| [PR #5081](https://github.com/agentscope-ai/QwenPaw/pull/5081) | Allow previewing files outside workspace in file guard | Merged |

Key fixes: SSL build failures on Windows, error message clarity, and file guard usability.

## 4. Community Hot Topics
Issues with the most engagement (comments/reactions):

- **[#4342](https://github.com/agentscope-ai/QwenPaw/issues/4342)** – `[CLOSED]` Unit test coverage for local_models, providers, tunnel, utils. 11 comments. Community showed strong interest in test completeness.
- **[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)** – `[OPEN]` Migrate backend from AgentScope 1.x to 2.0. 8 comments, 2 👍. This is the top roadmap discussion; users are awaiting the upgrade.
- **[#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)** – `[CLOSED]` WeChat push failure for scheduled tasks. 7 comments. Root cause identified in channel.py – a bug that was fixed.
- **[#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989)** – `[CLOSED]` Local Qwen 3.6‑27B model no response in 1.1.9/1.1.10. 5 comments. Regression from earlier version; likely fixed in 1.1.11.
- **[#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)** – `[OPEN]` Agent‑generated scheduled tasks cannot trigger or be edited. 5 comments. High concern for automation reliability.

Underlying needs: Users demand **test reliability**, **backward compatibility**, **channel delivery robustness**, and **agent‑generated task lifecycle** control.

## 5. Bugs & Stability
Ranked by severity:

1. **Critical: OpenSSL 3.5 regression** – [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086)  
   *Desktop fails to start, stuck at “Waiting for HTTP ready…”*  
   Fix PRs: [#5083](https://github.com/agentscope-ai/QwenPaw/pull/5083) and [#5082](https://github.com/agentscope-ai/QwenPaw/pull/5082) (merged). Also reverted a conflicting change in [#5092](https://github.com/agentscope-ai/QwenPaw/pull/5092). Hotfix release v1.1.11.post1 likely incoming.

2. **High: Agent‑generated scheduled tasks not triggering** – [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)  
   *No fix PR yet, still open.*

3. **High: MCP server process accumulation across restarts** – [#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834)  
   *Open; no dedicated fix identified.*

4. **Medium: Tool‑call `arguments` keyword error after several rounds** – [#5052](https://github.com/agentscope-ai/QwenPaw/issues/5052)  
   *Open; likely a runtime coordination issue.*

5. **Medium: DingTalk AI Card sends empty card on empty output** – [#5057](https://github.com/agentscope-ai/QwenPaw/issues/5057), fix in [PR #5061](https://github.com/agentscope-ai/QwenPaw/pull/5061) (open).

6. **Low: UI jitter on image preview drag, session switch lag, etc.** – multiple closed issues, many already addressed.

## 6. Feature Requests & Roadmap Signals
Top user‑requested features from the last 24h:

- **Independent visual model fallback** – [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) (4 comments, 1 👍)  
  Highly likely to be included in v1.2.0 given strong community need.
- **Headroom context compression integration** – [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) (2 comments)  
  Early stage, but could reduce token costs significantly.
- **Sub‑agent task visibility** – [#4923](https://github.com/agentscope-ai/QwenPaw/issues/4923) (3 comments)  
  Would improve multi‑agent debugging.
- **System tray for Windows desktop** – [#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751) (3 comments)  
  Longstanding request; may land in v1.2.0.
- **Fine‑grained file guard control (read‑only / whitelist)** – [#4356](https://github.com/agentscope-ai/QwenPaw/issues/4356) (2 comments)  
  Important for enterprise security.

**Roadmap signals**: The open PR [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) (Runtime 2.0 modular architecture with ToolCoordinator) and [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) (Agent OS Driver for MCP/A2A/ACP) indicate a significant architecture overhaul. These are likely planned for v2.0.

## 7. User Feedback Summary
- **Pain points**:
  - Windows desktop startup failure due to OpenSSL regression (multiple users).
  - Local model compatibility broken between 1.1.5 and 1.1.9/1.1.10.
  - Scheduled tasks created by agents cannot be edited or triggered.
  - UI lag when switching between many conversation tabs.
  - Tool‑call errors after several rounds confuse users.
- **Positive feedback**: Community appreciates the rapid bug‑fix release cycle (v1.1.11 post1 being prepared). Free model OAuth and Xiaomi MiMo integration are welcomed.
- **Dissatisfaction**: Some regressions (local model, WeChat push) indicate gaps in pre‑release testing.

## 8. Backlog Watch
Issues/PRs requiring maintainer attention due to age or importance:

- **[#3751](https://github.com/agentscope-ai/QwenPaw/issues/3751)** – System tray for Windows (opened Apr 23, 3 comments, no assignee). Low activity but repeatedly requested.
- **[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)** – Migrate to AgentScope 2.0 (opened May 27, 8 comments, 2 👍). Major dependency upgrade – no PR yet.
- **[#4356](https://github.com/agentscope-ai/QwenPaw/issues/4356)** – File guard whitelist/read‑only (opened May 14, 2 comments). Important for security, no movement.
- **[#4865](https://github.com/agentscope-ai/QwenPaw/issues/4865)** – Streaming rendering of tool call content (opened Jun 1, 2 comments). Affects UX severely.
- **[#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887)** – Custom endpoint for DingTalk private deployment (opened Jun 2, 2 comments). Enterprise blocker.
- **[#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)** – Agent‑generated timer tasks (opened Jun 10). Critical automation bug, no fix yet.
- **[#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086)** – OpenSSL regression (opened Jun 10). Being addressed but needs final verification.

*Note: All links use the repository `agentscope-ai/QwenPaw` as provided. No assignees or milestone data were visible.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-06-11

## 1. Today's Overview
ZeroClaw remains under **intense development**, with **41 issues** and **50 pull requests** updated in the last 24 hours. Community engagement is high: **23 issues are open/active** and **41 PRs are open** (9 merged/closed today). No new releases were published today, but the repository shows clear momentum toward the **v0.8.0**, **v0.8.1**, and **v0.8.2** milestone trains (trackers #7112, #6970, #7314). Maintainer attention is spread across **bug fixes** (e.g., Discord channel, telemetry attribution, truncated tool‑call envelopes) and **architecture RFCs** (unified turn engines, native plugin system). The project is actively addressing both user‑reported regressions and long‑standing feature requests, although several high‑risk issues remain unmerged.

## 2. Releases
**No new releases** in the last 24 hours. The latest published version remains v0.7.x (no tag change observed).

## 3. Project Progress
Nine PRs were **merged or closed** today. Key merged/closed contributions include:

- **#7370** – `fix(channels): drop truncated tool‑call envelopes at delivery, keep the reply` (merged). Prevents mid‑tool‑call cut‑offs from corrupting channel output.
- **#7136** – `feat(providers): add Kilo AI Gateway as first‑class model provider with pricing capture` (merged). Expands official provider support and supplies cost tracking infrastructure.
- **#7382** – `fix(gateway): attribute WS turn telemetry and cost to the agent's model` (merged). Squashes a bug where WebSocket turn telemetry was misattributed to the first provider in the list.
- **#7347** – `fix(channels/discord): ignore system messages so the bot stops replying to thread creation` (merged). Eliminates unwanted bot responses to Discord thread‑creation system messages.
- **#7344** – `feat(gateway): opt‑in remote /admin/reload via gateway.allow_remote_admin` (merged). Enables remote admin reload (default localhost‑only) for multi‑host deployments.
- **#7475** – `docs(container): add rootless Debian compose example` (open). Addresses #6760 by documenting how to run ZeroClaw in a Docker Compose setup.
- **#7480**, **#7481**, **#7473**, **#7479**, **#7474**, **#7482**, **#7477**, **#7478**, **#7476** – a wave of documentation and localization fixes (plurality authored by `Alix-007`), improving Fluent string routing, editor fallback, macOS key mapping, and config docs.

Several closed issues from earlier days also saw updates today (e.g., #6309, #4627, #6722, #7409), indicating ongoing resolution of backlog items.

## 4. Community Hot Topics
The most active discussions over the past 24 hours (by comment count) are:

- **[Issue #3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) – [Feature]: Provide a "full" docker image** (12 comments, 3 👍). Users request a pre‑built image with all feature flags (e.g., WhatsApp) to lower the entry barrier, particularly for non‑technical users. The discussion reveals frustration with the current fragmented Docker experience. Status: `blocked`, awaiting packaging decisions.

- **[Issue #6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) – [Bug]: 单轮对话以及多轮对话会出现丢失 user message的现象** (6 comments). A P1 bug affecting runtime/daemon where user messages are silently dropped in both single and multi‑turn conversations. The error originates from a custom API endpoint. The issue has been accepted but remains open without a fix PR.

- **[Issue #6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) – tool_search not in default_auto_approve → deferred_loading+webhook silently hangs 120s then auto‑denies** (5 comments). A high‑risk bug where MCP tools can never be loaded in non‑interactive modes, effectively blocking headless deployments. No fix PR yet.

- **[Issue #6309](https://github.com/zeroclaw-labs/zeroclaw/issues/6309) – [Bug]: Agent running model_routing_config "action": "upsert_agent" stomps on schema_version = 2 settings** (5 comments). A provider configuration corruption bug (S2 severity) caused by incorrect handling of schema upgrades. **Closed** today, presumably resolved.

- **[RFC #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) – Prefer a lighter ZeroClaw core through external integrations** (4 comments). Proposes removing built‑in integrations (gws‑cli, jira, github) in favour of skill‑based or plugin‑based approaches. Remains under discussion as a long‑term architecture shift.

## 5. Bugs & Stability
Several high‑severity bugs are currently open, with no immediate fix PRs attached:

| Issue | Severity | Component | Status | Notes |
|-------|----------|-----------|--------|-------|
| [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) – User message loss | S1 – workflow blocked | runtime/daemon | Open, accepted | No published fix; Chinese locale reporter. |
| [#6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) – MCP tool_search silent hang | S1 – workflow blocked | agent, gateway, MCP | Open, accepted | Blocks headless/webhook usage. |
| [#7263](https://github.com/zeroclaw-labs/zeroclaw/issues/7263) – Subagents do not inherit "cwd" in ACP sessions | S1 – workflow blocked | ACP channel | Open, accepted | Blocks multi‑agent reviewer workflows. |
| [#7436](https://github.com/zeroclaw-labs/zeroclaw/issues/7436) – image_info tool output does not reach multimodal models | S2 – degraded | runtime, provider | Open | Relative paths silently drop image data. |
| [#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470) – Delegate agentic mode rejects empty tool lists and same‑profile gating | S1 – workflow blocked | runtime/daemon | **Opened today** | New S1 bug with no fix yet. |
| [#7469](https://github.com/zeroclaw-labs/zeroclaw/issues/7469) – Default using "vi" but container does not include it | S3 – minor | unknown | Opened 2026‑06‑10 | A **fix PR #7476** (avoid hardcoded vi fallback) already open. |

**New bugs reported today:** #7470 (S1, delegate mode), #7469 (S3, editor fallback). The container `vi` issue has a quick PR (#7476).

## 6. Feature Requests & Roadmap Signals
The following enhancement requests and RFCs are shaping upcoming milestones:

- **v0.8.0** ([tracker #7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) – Stable‑tier promotions for config and tool‑call parsers; breaking‑change cleanup; release‑default decisions.
- **v0.8.1** ([tracker #6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) – Additive channels, providers, tools, and integration work.
- **v0.8.2** ([tracker #7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314)) – WASM plugin program (FND‑001), WIT interfaces, host‑function support.
- **RFC #7415** – “Unify the three agent turn engines” – proposes merging `run_tool_call_loop`, `turn_streamed`, and `Agent::turn` into a single code path to reduce bugs and maintenance.
- **RFC #7420** – “Native Dynamic‑Library Plugin System” – argues for a dlopen‑based plugin architecture to replace the monolithic kernel; initial design under review.
- **RFC #6165** – “Prefer a lighter ZeroClaw core through external integrations” – still blocked pending architectural consensus.

**Predictions for next release:** The wave of localization/container/docs PRs (#7475–#7482) suggests the team is preparing for a **v0.7.6 or v0.8.0 release candidate**. The Kilo AI Gateway provider (#7136) and remote admin reload (#7344) are likely to land in the next tag.

## 7. User Feedback Summary
Real user pain points surfaced in the last 24 hours:

- **Docker complexity** (#3642, #5908, #6760): Users repeatedly ask for a “full” Docker image that bundles all feature flags. The existing minimal image forces users to compile extensions themselves, which is a barrier.
- **Headless/webhook friction** (#6721): MCP `deferred_loading` + webhook mode silently hangs for 120 seconds and then auto‑denies, making ZeroClaw unusable in automated pipelines.
- **Configuration surprise** (#7471): The `config-list` command matches on string prefix boundaries, not segment boundaries, causing sibling aliases to leak into results (e.g., `agents.aaa` also returns `agents.aaab`).
- **Editor missing in containers** (#7469): The TUI assumes `vi` is always present, but the Debian container image does not include it.
- **Subagent workspace isolation** (#7263): Subagents cannot access repositories outside `~/.zeroclaw/agents/<agent>/workspace`, breaking multi‑agent collaborator setups.
- **Image tool limitation** (#7436): The `image_info` tool only works with absolute POSIX paths; relative or workspace‑relative paths silently drop images for vision models.

**Satisfaction signals:** The number of open PRs (50 updated in 24h) and fast bug‑fix turnaround (e.g., #7370, #7347 merged same day) indicates a responsive maintainer team. The “full Docker image” request (#3642) has 12 comments and 3 👍, suggesting moderate demand but unresolved logistics.

## 8. Backlog Watch
Issues that have been open for an extended period without a fix or maintainer response:

- **[Issue #3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)** – Full Docker image request. Created 2026‑03‑15, **98 days open**. Status `blocked` and `accepted`. No associated PR. High community interest (12 comments).
- **[Issue #6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034)** – User message loss (S1). Created 2026‑04‑23, **49 days open**. Status `accepted` but no fix PR. Core runtime bug affecting Chinese‑locale users.
- **[RFC #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)** – Lighter core via external integrations. Created 2026‑04‑27, **45 days open**. Status `blocked`. Awaiting architectural sign‑off.
- **[Issue #6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721)** – MCP `tool_search` silent hang. Created 2026‑05‑16, **26 days open**. P1 bug blocking headless usage. No PR.
- **[Issue #7263](https://github.com/zeroclaw-labs/zeroclaw/issues/7263)** – Subagent `cwd` inheritance. Created 2026‑06‑05, **6 days open**. S1 bug with only 1 comment; no maintainer response yet.

These issues represent **call‑to‑action gaps** that, if left unresolved, risk user churn in headless/multi‑agent and containerized deployments.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*