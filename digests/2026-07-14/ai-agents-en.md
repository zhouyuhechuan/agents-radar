# OpenClaw Ecosystem Digest 2026-07-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-14 01:49 UTC

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

Here is the OpenClaw project digest for 2026-07-14.

**1. Today's Overview**

OpenClaw’s activity level is extremely high, with 500 issues and 500 pull requests updated in the last 24 hours, reflecting a very busy development cycle. The project is in a state of intense triage and bug fixing, as a significant number of the most active issues are labelled P0 or P1 and involve critical regressions in session state, message delivery, and data integrity. The release of v2026.7.1 introduced new AI models and providers, but has also immediately generated a regression crash in a CLI command, underscoring the rapid iteration pace. The community is highly engaged, with a long-standing feature request for Linux and Windows desktop apps still dominating discussion, while a cluster of recent critical bugs demands immediate maintainer focus.

**2. Releases**

A new release, **v2026.7.1** (openclaw 2026.7.1), was published on this date. This is a feature release that adds support for new AI model providers: **Featherless**, **Claude Sonnet 5**, **Mythos 5**, **Meta Muse Spark 1.1**, and the new **ClawRouter**. A significant product change is setting **GPT-5.6** as the default model for new setups, with a new `/think ultra` reasoning mode for the "Sol" and "Terra" model configurations and a `max` mode for "Luna". The release also includes system-level improvements to honor Z.AI `max` settings and refresh model availability lists after OAuth authentication. No explicit breaking changes or migration notes were provided in the release highlights.

**3. Project Progress**

In the 24-hour window, 238 pull requests were merged or closed, indicating a high rate of change. Notable fixes and features that advanced include:
- A fix to drain root work continuations before gateway process exit, preventing data loss in plugin hooks during shutdown (PR #105848).
- A fix for the `models fallbacks` command that was silently editing global defaults instead of the specified agent (PR #106414).
- A fix for Telegram message parsing to correctly handle malformed multi-colon delivery targets, preventing silent misrouting (PR #97823).
- A fix to prevent progress drafts from appearing for short tasks, improving the user experience during model calls (PR #106026).
- A significant PR to redact exec tool result payloads, a critical security and privacy improvement (PR #81185).
- A new `sleep` tool that allows agents to pause and resume sessions after a delay, enabling more complex wait-for-external-condition workflows (PR #103052).

**4. Community Hot Topics**

The most active community discussion by a wide margin remains **Issue #75**, a long-standing request for **Linux and Windows desktop apps**, which has 112 comments and 81 reactions. This highlights a persistent and strong user demand for platform parity beyond macOS, iOS, and Android.

Other highly active threads reveal deep technical pain points. **Issue #7707** (18 comments) requests a "Memory Trust Tagging by Source" feature to prevent memory poisoning attacks from untrusted content. This signals a growing user concern about security as agents become more autonomous. Several critical bugs are also generating significant discussion, including **Issue #104721** (16 comments), where all tool results are returning the literal string "(see attached image)" instead of actual output—a P0 regression that renders file reads and many tools useless. Similarly, **Issue #102020** (13 comments) describes a "reply session initialization conflicted" error on the second message in a session, breaking basic conversation flow.

**5. Bugs & Stability**

The project is facing a significant stability challenge, with multiple P0 (critical) and P1 (high-severity) bugs reported.
- **P0 - Critical:**
    - **Issue #104721**: Tool results returning "(see attached image)" literal string instead of output. No linked fix PR yet.
    - **Issue #101290**: CLI startup preflight can corrupt the live state database (`openclaw.sqlite`), leading to a "database disk image is malformed" error. No linked fix PR yet.
    - **Issue #103076**: Additional legacy-state migration sources still block gateway startup after a previous fix, causing a crash loop. No linked fix PR yet.
- **P1 - High Severity:**
    - **Issue #38327**: "Cannot convert undefined or null to object" regression with google-vertex/gemini-3.1-pro-preview. No linked fix PR yet.
    - **Issue #90944**: Session yield resume replies are recorded but not delivered to the user, causing message loss. No linked fix PR yet.
    - **Issue #77012**: WebChat session transcript is overwritten on every turn, causing complete data loss on page refresh. No linked fix PR yet.
    - **Issue #77443**: WhatsApp event loop blocks on first inbound message, causing the gateway to hang. No linked fix PR yet.
    - **Issue #106914**: A regression in the new v2026.7.1 release causes `openclaw models list` to crash if a configured model has no cost data. A fix PR (#106914) is noted in the issue data.
- **Regressions:** A large number of these bugs are marked as regressions, suggesting recent changes have introduced significant instability. The "Cannot convert undefined or null to object" (#38327) and the "database corruption" (#101290) bugs are particularly concerning as they cause hard failures.

**6. Feature Requests & Roadmap Signals**

The most ambitious feature requests focus on security, reliability, and extensibility.
- **Security & Trust:** The **Memory Trust Tagging by Source** (#7707) and **Filesystem Sandboxing Config** (#7722) requests are both highly rated and touch on critical security boundaries. Given the project's current stability issues, more foundational security features may be prioritized for the next release.
- **Reliability & Observability:** The requests for **dynamic model discovery** (#10687) and **triggering model fallback on context length exceeded** (#9986) signal a desire for the system to be more resilient and self-configuring. The high volume of crashes and errors suggests these will be roadmap priorities.
- **User Experience:** Smaller enhancements like **TUI accessibility options** (#9637), **Shift+Enter for multi-line input** (#10118), and a **`/models test-fallback` command** (#6599) are community requests that improve daily usability. These are likely candidates for upcoming minor releases.

**7. User Feedback Summary**

User sentiment is sharply divided. On one hand, there is strong satisfaction with the rapid addition of new models and providers (Featherless, Mythos 5, GPT-5.6 default), showing a commitment to cutting-edge AI. On the other hand, there is deep dissatisfaction and frustration stemming from a wave of critical regressions. Users are reporting that basic functionality is broken—tools returning placeholder text, sessions losing all context, and the gateway crashing on the second message. The core pain points are **data loss** (message history overwritten, session context lost, tool results missing), **reliability** (crashes, database corruption, event loop blocking), and **security** (fear of memory poisoning, lack of exec-approval forward to backends). The community is clearly using OpenClaw in production-like environments and is feeling the impact of these instabilities.

**8. Backlog Watch**

Several important issues and PRs are languishing for extended periods, requiring maintainer attention.
- **Issue #75** (Linux/Windows desktop apps) is the most visible, open since January 2026 with no fix PR. User demand remains extremely high.
- **Issue #7707** (Memory Trust Tagging) and **Issue #7722** (Filesystem Sandboxing) are both critical security features that have been open for over five months and are tagged with `clawsweeper:needs-product-decision`, indicating a stalled roadmap decision.
- **Issue #10687** (Dynamic Model Discovery) is a core infrastructure improvement open since February that would resolve numerous configuration friction points.
- **PR #81185** (Redact exec tool results) is a large and critical security PR that has been open since May 12 and is marked "ready for maintainer look." Its size and potential impact likely require careful review.
- **PR #95604** (Discord subagent progress) and **PR #103052** (Sleep tool) are significant feature PRs also "ready for maintainer look," indicating a potential bottleneck in the review pipeline for larger contributions.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent Open-Source Ecosystem
**Date:** 2026-07-14

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing a surge in development velocity, driven by the release of new foundation models (GPT-5.6, Claude Sonnet 5, Meta Muse Spark 1.1) and growing production adoption. The landscape is bifurcating: large reference implementations (OpenClaw, ZeroClaw) are shipping features rapidly but struggling with regression-induced instability, while mid-tier projects (NanoBot, Hermes Agent) are demonstrating stronger bug-fix turnaround times. A critical theme across all active projects is the tension between feature velocity and reliability—users explicitly report downgrading from v2.0 releases or abandoning new versions due to broken core workflows. Security hardening (approval flow smuggling, memory poisoning prevention, exec-tool redaction) has emerged as a cross-cutting priority, reflecting the ecosystem's maturation beyond prototyping into production-sensitive deployments.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | New Release Today | Health Signal |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 238 | ✅ v2026.7.1 | 🔴 Regression-heavy; P0 bugs in session state & data integrity |
| **ZeroClaw** | 50 | 50 | 3 | ❌ | 🟡 Active development; v0.8.3 finalization; S1 Docker bug |
| **CoPaw** | 50 | 50 | 28 | ✅ v2.0.0.post1 | 🟡 Post-release stabilization; critical context-compression bugs |
| **IronClaw** | 34 | 50 | 5 | ❌ | 🟡 Bug-bash cycle; 10+ P2/P3 UI/integration issues |
| **NanoBot** | 13 | 44 | 17 | ❌ | 🟢 Strong fix velocity; one critical open loop bug (#4864) |
| **Hermes Agent** | 50 | 50 | 13 | ❌ | 🟢 Rapid triage; CJK/Windows/Docker fixes merged same-day |
| **LobsterAI** | 0 | 21 | 19 | ❌ | 🟢 Focused polish; all critical installer bugs fixed |
| **PicoClaw** | 4 | 5 | 1 | ❌ | 🟡 Moderate activity; stale backlog needs maintainer review |
| **NanoClaw** | 3 | 33 | 27 | ❌ | 🟢 High throughput; security smuggling fixes shipped |
| **NullClaw** | 0 | 12 | 0 | ❌ | 🟡 Consolidation phase; 12 PRs nearing merge |
| **Moltis** | 0 | 1 | 0 | ❌ | 🟢 Low activity but stable; single CalDAV fix in progress |
| **TinyClaw** | 0 | 0 | 0 | ❌ | ⚪ Dormant |
| **ZeptoClaw** | 0 | 0 | 0 | ❌ | ⚪ Dormant |

*Health: 🟢 Stable/Improving | 🟡 Moderate risk | 🔴 Critical issues | ⚪ Inactive*

---

## 3. OpenClaw's Position

OpenClaw remains the **largest and most feature-rich reference implementation** in the ecosystem, but its position is under pressure from reliability failures. Key comparison points:

**Advantages vs. Peers:**
- **Model provider breadth**: First to ship Featherless, Claude Sonnet 5, Mythos 5, and ClawRouter—outpacing Hermes Agent and ZeroClaw on provider support velocity.
- **Raw feature quantity**: `/think ultra` reasoning mode, `sleep` tool for wait-for-condition workflows, and ClawRouter demonstrate architectural ambition beyond incremental fixes.
- **Community demand signal**: Issue #75 (Linux/Windows desktop apps) has 112 comments + 81 reactions—an order of magnitude more engagement than any single request in other projects.

**Technical Approach Differences:**
- **Monolithic core vs. modular**: OpenClaw ships a single reference binary; NanoBot and NullClaw favor composable channel/tool plugins. This gives OpenClaw tighter integration but slower regressions surface.
- **Top-down model defaults**: Setting GPT-5.6 as default for new setups contrasts with ZeroClaw's RFC-driven approach to configuration validation and local-first modes.
- **Audit trail gap**: NanoBot merged an audit system today (#4320); OpenClaw's equivalent (PR #81185, exec redaction) has been open since May 12—a potential security differential.

**Community Size:**
- OpenClaw's 500 issues/PRs updated in 24 hours dwarfs every other project (next: ZeroClaw at 50). This reflects both a larger user base and a higher bug-discovery rate.
- However, the **bug-to-fix ratio** is concerning: 238 PRs merged vs. 500 updated suggests a triage bottleneck. Hermes Agent, by contrast, closes most bugs within 1-2 days.

---

## 4. Shared Technical Focus Areas

Several requirements are emerging independently across multiple projects, indicating industry consensus:

| Requirement | Affected Projects | Specific Needs |
|---|---|---|
| **Cross-platform desktop apps** | OpenClaw (#75), ZeroClaw (Docker bug), Hermes (Windows fix) | Linux/Windows parity beyond macOS/iOS |
| **Memory/context management** | NanoBot (Dream fixes), ZeroClaw (#8891 persistent memory tracker), OpenClaw (#7707 trust tagging) | Preventing poisoning, durable cross-session recall |
| **Security hardening (MCP/tool)** | NanoClaw (approval smuggling fix #2827), CoPaw (tool allow/deny rules), OpenClaw (#7707), NullClaw (#969 structured approval) | Full parameter rendering on approval cards, allowlisting |
| **Reliability (cron/message delivery)** | OpenClaw (session overwrite), NullClaw (#954 use-after-free), ZeroClaw (#9035 Docker), LobsterAI (#2320 cron skip) | Surviving restarts, preventing silent drops |
| **Streaming & progress UX** | Hermes (async delegation results), NanoClaw (streaming thinking blocks), ZeroClaw (#8443 Matrix drafts) | Per-turn thinking display, tool-call deltas |
| **Localization/i18n** | NanoBot (Brazilian Portuguese), ZeroClaw (#6548 Fluent bypass), Hermes (CJK text truncation) | Non-English locale support, CJK IME compatibility |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | CoPaw |
|---|---|---|---|---|---|
| **Target user** | Advanced developers, production deployments | Mid-tier developers, channel-heavy workflows | Desktop-first, Windows/CJK users | Systems engineers, Docker/offline | Chinese-language users, WeChat/Feishu |
| **Architecture** | Monolithic reference binary | Plugin-based, composable | Desktop-first (Electron) | Modular with WASM channels | AgentScope framework integrated |
| **Key differentiator** | Fastest model provider support | Audit system + tool gateway for channels | CJK/Windows reliability focus | RFC-driven governance, local-first mode | v2.0.0.post1 rapid stabilization |
| **Security posture** | P0 exec-tool redaction stalled (PR #81185) | Audit system shipped today (#4320) | OIDC support, dashboard token fixes | Approval-gated tool execution (#7686) | MCP allow/deny still broken |
| **Release cadence** | Feature releases weekly | No formal release train | v0.15.1 (stable, May 29) | v0.8.3 finalizing; monthly milestones | Hotfix same-day as report |
| **Channel support** | Telegram, WebChat, WhatsApp | Discord, Telegram, Feishu | Desktop, Telegrams, Slack | Matrix, Telegram, Slack + WASM | WeChat, Feishu, Telegram |

**Key Insight:** No single project dominates across all dimensions. OpenClaw leads in provider breadth and community size; NanoBot and NullClaw lead in security feature velocity; Hermes and CoPaw dominate platform-specific reliability (CJK, Chinese ecosystem).

---

## 6. Community Momentum & Maturity

**Tier 1: Rapidly iterating but unstable**
- **OpenClaw**: Highest raw activity, but P0 database corruption and tool-result bugs signal growing pains. Users report data loss—a critical trust-eroding pattern.
- **CoPaw**: v2.0.0 post-release stabilization shows responsiveness, but users explicitly compare unfavorably to v1.x. Community frustration is high.
- **ZeroClaw**: v0.8.3 finalization is orderly, but S1 bugs (Docker unreachable, Windows force-quit) threaten production rollout.

**Tier 2: Strong bug-fix velocity, stabilizing**
- **NanoBot**: Merged 17 PRs today, including security audit system. Only one critical open bug (#4864). Healthiest fix:issue ratio of high-activity projects.
- **Hermes Agent**: 13 PRs merged, CJK/Windows bugs closed same-day. Responsive maintainer team; post-v0.15.1 fixes are accumulating but not yet released.
- **NullClaw**: Consolidation phase with 12 PRs approaching merge. No new bugs reported today—suggests a window of stability before the next release.

**Tier 3: Quiet maintenance, low volatility**
- **LobsterAI**: Internal team-driven; all critical installer bugs fixed today. No community engagement—good for reliability, weak for external contributions.
- **Moltis**: Single CalDAV fix. Possibly unmaintained public-facing but stable for current users.
- **PicoClaw**: Moderate activity but stale backlog (9+ days for maintainer-unreviewed PRs). Security migration (vodozemac) is urgent but unaddressed.

**Tier 4: Dormant**
- **TinyClaw, ZeptoClaw**: No activity at all.

---

## 7. Trend Signals

**1. From "works on my machine" to production-grade reliability**
The ecosystem's most vocal pain points are now about **data loss and session corruption**—not feature gaps. OpenClaw's session transcript overwrite (#77012) and NullClaw's cron use-after-free (#954) indicate that users are deploying agents in workflows where state persistence is non-negotiable. Developers should prioritize **idempotent message delivery, crash recovery, and database integrity checks** over new model support.

**2. Security is becoming the primary differentiator**
NanoClaw's approval smuggling fix, OpenClaw's stalled exec redaction, and ZeroClaw's approval-gated tool execution tracker all point to a market where **trust boundaries between agent and user** are the next battleground. Projects that ship robust approval workflows (structured approval flows with full parameter rendering) will win enterprise adoption. The contrast between NanoBot's shipped audit system and OpenClaw's 2-month-old PR #81185 is a competitive gap.

**3. Localization is not optional**
Hermes Agent's rapid CJK fixes and NanoBot's Portuguese locale show that **non-English UX is a first-class requirement**, not a nice-to-have. ZeroClaw's Fluent localization bypass (#6548) was flagged by users within hours of a release. Agent developers targeting global audiences must invest in locale-aware string handling from day one.

**4. The "core + plugin" architecture is winning over monolithic builds**
NanoBot, NullClaw, and ZeroClaw all embrace channel/tool plugin models. OpenClaw's monolithic approach is generating more regression surface. The industry is converging on **WASM-based channel execution** (ZeroClaw #6062, IronClaw skeleton) and **MCP-based extensibility** as the standard pattern.

**5. Community governance matters for long-term health**
ZeroClaw's RFC #6808 on work lanes and board automation, combined with its milestone trackers (#8891, #8288), represents the most mature governance model in the ecosystem. OpenClaw's lack of structured triage is visible in its stalled PRs (PR #81185, 2 months). Projects with clear RFC processes and maintainer response SLAs will retain contributors better.

**6. Offline/local-first is an underserved requirement**
ZeroClaw's #5287 (local-first mode) and CoPaw's Docker regressions highlight that **small-model offline agents** are a growing use case. Most projects optimize for cloud API usage; the project that ships reliable local execution (via ollama, llama.cpp) with minimal prompt bloat will capture the privacy-conscious segment.

**Bottom line for decision-makers:** If you need **maximum provider support and community size**, OpenClaw remains the default—but budget for maintenance overhead due to regressions. For **production reliability with strong security posture**, NanoBot and NullClaw offer better risk profiles. For **Chinese-language workflows**, CoPaw is the clear leader. The ecosystem is converging on plugin-based architectures, structured approval flows, and first-class localization—these should be non-negotiable requirements for new agent deployments.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot Project Digest — 2026-07-14

### 1. Today’s Overview

NanoBot is experiencing **high community activity**, with 13 issues and 44 pull requests updated in the last 24 hours. 11 issues were closed (2 remain open), while 17 PRs were merged/closed and 27 PRs are still open. No new releases were cut today. The project is in a **vigorous maintenance and feature-development phase**, with contributors actively fixing regressions (Dream, Discord, Windows Shell, Heartbeat), polishing documentation, and adding new capabilities such as session-scoped model presets, a Brazilian Portuguese locale, and a guarded tool gateway for channels.

### 2. Releases

**None.** No new releases were published today.

### 3. Project Progress

**17 PRs merged/closed** in the last 24 hours. Notable advances:

- **Audit system** — [#4320](https://github.com/HKUDS/nanobot/pull/4320) (merged) adds `tools.audit` config and `AuditTool` for agent action observability.
- **Dream fixes** — [#4909](https://github.com/HKUDS/nanobot/pull/4909) (closed) ignores line-ending-only memory diffs; [#4893](https://github.com/HKUDS/nanobot/pull/4893) (closed via issue) and [#4894](https://github.com/HKUDS/nanobot/pull/4894) (closed) fix Dream log and pruning bugs.
- **WebUI & i18n** — [#4914](https://github.com/HKUDS/nanobot/pull/4914) (closed) adds Brazilian Portuguese locale; [#4913](https://github.com/HKUDS/nanobot/pull/4913) (closed) updates README with recent changes.
- **Documentation** — [#4912](https://github.com/HKUDS/nanobot/pull/4912) (closed) removes broken Star History embed; [#4916](https://github.com/HKUDS/nanobot/pull/4916) (open) reorganizes docs around user workflows.
- **Heartbeat** — [#4915](https://github.com/HKUDS/nanobot/pull/4915) (open) makes heartbeat evaluation more configurable (addresses #4896).

Additionally, several bug-fix PRs (see *Bugs & Stability*) have been merged or are in review.

### 4. Community Hot Topics

- **Endless loop on `complete_goal`** — [#4864](https://github.com/HKUDS/nanobot/issues/4864) (open, 3 comments) reports a critical bug where the gateway parses a JSON parameter as a bare string, causing an infinite tool-call loop. This is the most active open issue.
- **Discord bot integration failure** — [#4897](https://github.com/HKUDS/nanobot/issues/4897) (closed, 3 comments) describes a bot that goes online but receives no messages. The community helped diagnose a configuration issue.
- **Forced output verbosity** — [#1500](https://github.com/HKUDS/nanobot/issues/1500) (closed, 2 comments, 1 👍) requests a message-level filtering system, reflecting user desire for cleaner feedback.
- **Tool gateway for channels** — [#4911](https://github.com/HKUDS/nanobot/issues/4911) (open, 0 comments, new) proposes a guarded seam so voice/real-time channels can invoke agent tools, signaling a forward-looking architectural need.

**Underlying needs:** Users are hitting integration rough edges (Discord, Feishu, Windows), want more granular control over output verbosity, and are pushing for richer channel capabilities (streaming, tool access).

### 5. Bugs & Stability

| Severity | Bug | Fix PR / Status |
|----------|-----|-----------------|
| **Critical** | [#4864](https://github.com/HKUDS/nanobot/issues/4864) – Endless loop on `complete_goal` due to gateway JSON parsing regression | Open (no fix PR yet) |
| **High** | [#4897](https://github.com/HKUDS/nanobot/issues/4897) – Discord bot integration: bot online but no messages received | Closed (resolved via config guidance) |
| **Medium** | [#4882](https://github.com/HKUDS/nanobot/issues/4882) – `dream_content_diff` reports empty files as changed after init | [#4909](https://github.com/HKUDS/nanobot/pull/4909) (merged) |
| **Medium** | [#4893](https://github.com/HKUDS/nanobot/issues/4893) – `/dream-log` shows non-Dream commits | [#4893](https://github.com/HKUDS/nanobot/issues/4893) (closed, fix included) |
| **Medium** | [#4894](https://github.com/HKUDS/nanobot/issues/4894) – `prune_dream_sessions` fails with base64-encoded filenames | [#4894](https://github.com/HKUDS/nanobot/issues/4894) (closed) |
| **Medium** | [#4881](https://github.com/HKUDS/nanobot/issues/4881) – Windows PowerShell output has embedded NUL bytes (UTF-16) | [#4917](https://github.com/HKUDS/nanobot/pull/4917) (open) |
| **Low** | [#4887](https://github.com/HKUDS/nanobot/issues/4887) – Test setup: `lark-oapi` missing from dev extras | Closed (dev dependency guide updated) |

Many bugs are **being actively fixed** with dedicated PRs. The critical #4864 still lacks a fix, making it the top stability risk.

### 6. Feature Requests & Roadmap Signals

**Likely for next version:**

- **Session-scoped model presets** [#4866](https://github.com/HKUDS/nanobot/pull/4866) — Persisting model selection per session, with immutable LLM runtime capture. This is a significant UX improvement for multi-model workflows.
- **Heartbeat trigger command** [#4620](https://github.com/HKUDS/nanobot/pull/4620) — Adds CLI `nanobot heartbeat trigger` with dry-run and JSON output, addressing #3437.
- **Telegram streaming** [#1599](https://github.com/HKUDS/nanobot/pull/1599) — Real-time token streaming via `sendMessageDraft`. Open for months; may be rebased soon.
- **WebUI Markdown export** [#4587](https://github.com/HKUDS/nanobot/pull/4587) — Export session messages as `.md`, part of #4579.
- **WebUI / config.json parity** [#4313](https://github.com/HKUDS/nanobot/pull/4313) — Adds UI controls for temperature, tool limits, memory, etc.
- **`nano_timer` core tool** [#4853](https://github.com/HKUDS/nanobot/pull/4853) — Timezone-aware UTC/local time with calendar fields.

**Longer-term signals:**

- **Guarded tool gateway for channels** [#4911](https://github.com/HKUDS/nanobot/issues/4911) — Enables channels (e.g., voice) to run agent tools, a foundational change for real-time interaction.
- **Auto-discovery for agent hooks** [#4878](https://github.com/HKUDS/nanobot/pull/4878) — Simplifies hook registration (like channels/tools already do).
- **Output mode control** (from #1500) — Message severity levels are still wanted.

### 7. User Feedback Summary

**Pain points reported this week:**

- Discord integration: bot shows online but doesn’t respond to messages (#4897).
- Tool call loops: `complete_goal` repeatedly errors due to gateway parameter parsing (#4864).
- Dream pruning: old-style glob patterns don’t cover new base64 filenames (#4894).
- Windows shell execution: PowerShell output corrupted by UTF-16 encoding (#4881).
- Feishu file uploads: bot cannot download files despite correct permissions (#2352, closed).
- Output verbosity: users want to suppress intermediate thinking steps (#1500).

**Positive signals:**

- Community is actively submitting bug reports and fixes (high PR volume).
- i18n contributions are growing (Portuguese locale #4914).
- Documentation restructuring (#4916) shows maintainers are investing in onboarding.

### 8. Backlog Watch

**Old PRs needing maintainer attention** (open >30 days, with conflicts or low review activity):

- [#1599](https://github.com/HKUDS/nanobot/pull/1599) (Mar 6) — Telegram streaming; has conflicts and no recent updates.
- [#4313](https://github.com/HKUDS/nanobot/pull/4313) (Jun 12) — WebUI/config.json parity; large, with conflicts.
- [#4587](https://github.com/HKUDS/nanobot/pull/4587) (Jun 29) — WebUI Markdown export; has conflicts.
- [#4620](https://github.com/HKUDS/nanobot/pull/4620) (Jul 1) — Heartbeat trigger command; open but no conflicts listed.

**Old issues** such as #192 (WeChat, Feb), #1011 (Mattermost, Feb) and #1304 (codex, Feb) have been closed as stale. They no longer require attention.

**Currently open issues with no assigned fix:** #4864 (critical, no PR yet) and #4911 (enhancement, 0 comments) are fresh and could use maintainer triage.

---

*Generated from GitHub data for the 24-hour period ending 2026-07-13.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-14

## 1. Today's Overview

The project saw very high activity in the last 24 hours, with **50 issues** and **50 pull requests** updated. Of these, **28 issues were closed** (most with confirmed fixes) and **13 PRs were merged/closed**, indicating a strong focus on bug fixing and stability. The majority of resolved bugs targeted the Desktop app, CLI update process, CJK/IME text handling, and Docker integration. Meanwhile, **22 new or reactivated issues** remain open, several classified as P2 (high priority) and requiring reproduction. The average issue age is low, suggesting the maintainers are actively triaging incoming reports. No new releases were published today.

## 2. Releases

**No new releases** were published today. The latest available version remains **v0.15.1** (2026-05-29), although a significant number of post‑v0.15.1 fixes have been merged onto `main` (marked `sweeper:implemented-on-main`).

## 3. Project Progress

**13 PRs were merged or closed today**, the majority of which are bug fixes now integrated into `main`. Key resolved pull requests include:

| PR | Title (abbreviated) | Component |
|----|---------------------|-----------|
| [#39565](https://github.com/NousResearch/hermes-agent/pull/39565) | fix(desktop): clip sidebar overflow while sessions run | Desktop |
| [#39557](https://github.com/NousResearch/hermes-agent/pull/39557) | fix(cli): catch _build_web_ui exceptions to prevent half‑updated state | CLI |
| [#39566](https://github.com/NousResearch/hermes-agent/pull/39566) | fix(desktop): inline local files for remote gateway prompts | Desktop |
| [#39562](https://github.com/NousResearch/hermes-agent/pull/39562) | fix(model‑metadata): gate Ollama /api/show probes to non‑Ollama providers (e.g. OpenRouter) | Agent / Providers |
| [#39554](https://github.com/NousResearch/hermes-agent/pull/39554) | fix(desktop): omit invalid dashboard web dist env | Desktop |
| [#39546](https://github.com/NousResearch/hermes-agent/pull/39546) | fix(agent): preserve explicit CLI session source over gateway defaults | Agent |
| [#39543](https://github.com/NousResearch/hermes-agent/pull/39543) | fix(dashboard): preserve injected session token | Dashboard |

Additional merged fixes addressed the `execute_code` “Always” approval persistence ([#39187](https://github.com/NousResearch/hermes-agent/issues/39187)), Windows Docker backend working‑directory errors ([#39143](https://github.com/NousResearch/hermes-agent/issues/39143)), auto‑update failures on Windows due to file‑lock ([#39431](https://github.com/NousResearch/hermes-agent/issues/39431)), and uv‑based update failures ([#39444](https://github.com/NousResearch/hermes-agent/issues/39444)).

No major feature PRs were merged today; however, two new‑feature PRs remain open: the **autoplay image carousel** ([#62706](https://github.com/NousResearch/hermes-agent/pull/62706)) and **surface async delegation results in chat** ([#64094](https://github.com/NousResearch/hermes-agent/pull/64094)).

## 4. Community Hot Topics

The most active issues and PRs (by comment count) reflect real‑world friction, especially among users of CJK languages, Windows, and Docker. All of the following closed issues received fixes today:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#3956](https://github.com/NousResearch/hermes-agent/issues/3956) | 9 | Empty Codex response treated as incomplete → retried 3× |
| [#39534](https://github.com/NousResearch/hermes-agent/issues/39534) | 8 | Chinese prompt cut off in Desktop window (Windows) |
| [#39538](https://github.com/NousResearch/hermes-agent/issues/39538) | 6 | CJK IME text drops on Enter in Desktop composer |
| [#39349](https://github.com/NousResearch/hermes-agent/issues/39349) | 4 | `~/.hermes/.env` overrides dashboard session token → WebSocket failure |
| [#39549](https://github.com/NousResearch/hermes-agent/issues/39549) | 3 | `hermes update` aborts with `ValueError` → half‑updated state (5 👍) |
| [#39503](https://github.com/NousResearch/hermes-agent/issues/39503) | 3 | Desktop 0.15.1 fails to start: unrecognized argument `--tui` |
| [#39444](https://github.com/NousResearch/hermes-agent/issues/39444) | 3 | `hermes update` fails with uv when `VIRTUAL_ENV` not set |

**Underlying needs**: Users demand robust update mechanisms, correct handling of non‑ASCII text input, and seamless cross‑platform operation (Windows, macOS, Linux, Docker). The relatively low reaction counts suggest these are functional rather than widely‑voted issues.

## 5. Bugs & Stability

**New bugs reported today** (created 2026-07-13/14) — all open and awaiting triage or fix:

| ID | Severity | Component | Summary |
|----|----------|-----------|---------|
| [#64073](https://github.com/NousResearch/hermes-agent/issues/64073) | P2 – needs‑repro | Agent / MCP | Streamable HTTP MCP server stuck in keepalive/reconnect loop; `send_ping` times out ~600s |
| [#63911](https://github.com/NousResearch/hermes-agent/issues/63911) | P3 | Gateway / Telegram | Telegram DM topic mode: root lobby silently swallows kanban wake events with no `thread_id` |
| [#64020](https://github.com/NousResearch/hermes-agent/issues/64020) | P2 – needs‑repro | Portal / Billing | Payment method setup fails even on free plan; user cannot connect |
| [#63895](https://github.com/NousResearch/hermes-agent/issues/63895) | P2 – needs‑repro | CLI / Terminal | Terminal autoscrolls to bottom even when agent output is finished, blocking history review |
| [#63695](https://github.com/NousResearch/hermes-agent/issues/63695) | P2 – needs‑repro | Cron / Slack | `dan-blockers` cron delivery failures due to API & network errors |
| [#63069](https://github.com/NousResearch/hermes-agent/issues/63069) | P2 | Tools / File | `read_file` falsely reports “File not found” when interrupted by SSE disconnect |
| [#63849](https://github.com/NousResearch/hermes-agent/issues/63849) | P2 | Agent / OpenAI | Tool‑result images never evicted on OpenAI‑compatible path → OOM |
| [#64055](https://github.com/NousResearch/hermes-agent/issues/64055) | P2 – closed | Dashboard / Auth | Dashboard no longer respects self‑hosted OIDC (closed, may be fixed) |
| [#54801](https://github.com/NousResearch/hermes-agent/issues/54801) | P3 | Dashboard / CLI | Backup button passes path as positional argument instead of `--output` flag (open since June 29) |

**Stability assessment**: The high volume of closed bugs today indicates a responsive development cycle. However, several P2 issues remain unaddressed, particularly around MCP server stability, file reading edge cases, and convergence of multiple concurrent, non‑critical but disruptive bugs (e.g., persistent autoscroll, image memory leak). Two recent bugs ([#64073](https://github.com/NousResearch/hermes-agent/issues/64073), [#63849](https://github.com/NousResearch/hermes-agent/issues/63849)) may escalate to P1 if they block production use.

## 6. Feature Requests & Roadmap Signals

Only one explicit feature request appears in today’s issue set — [#39509](https://github.com/NousResearch/hermes-agent/issues/39509) (open but marked `incoherent`) — asking for examples of tasks that the `openclaw` skill‑creation mechanism cannot handle. This is not actionable in its current form.

More concrete signals come from open PRs:

- **autoplay image carousel** ([#62706](https://github.com/NousResearch/hermes-agent/pull/62706)) – brings a `MEDIA‑GALLERY` block with thumbnails and autoplay. Likely candidate for next minor release as it extends existing media support.
- **surface async delegation results in chat** ([#64094](https://github.com/NousResearch/hermes-agent/pull/64094)) – provides visible transcript rows for background process completions (e.g., Hephaestus). Indicates an ongoing effort to improve user visibility of asynchronous workflows.

No roadmap documents or milestones were mentioned. The focus remains on **desktop UX, MCP integration, and platform‑specific reliability**.

## 7. User Feedback Summary

**Pain points** expressed in today’s updates:

- **Update process fragility**: Several users reported `hermes update` leaving their installation in an incomplete state (ValuedError, half-built UI, uv virtual env not found). These were fixed within hours of reporting.
- **CJK IME / text truncation**: Multiple users with Chinese/Japanese/Korean input methods experienced dropped characters, missing send buttons, or text that “disappears” while typing. All such reports were quickly resolved (merged today).
- **Windows‑specific friction**: File‑lock errors during auto‑update (`speedups.pyd`), Docker backend failing with “invalid working directory”, and taskkill locale decode errors continue to be a recurring theme.
- **Dashboard connectivity**: Users running remote or self‑hosted setups encountered token mismatches and frontend 404 errors, both addressed today.

**Satisfaction** is evident from the quick closure of reported bugs (often within 1–2 days). The community is actively contributing reproducers and even fix PRs (e.g., `sweetcornna`, `kyssta‑exe`, `liuhao1024`, `LeonSGP43`). The “invalid” flag on [#39368](https://github.com/NousResearch/hermes-agent/issues/39368) (“FAKE” accusation) was closed quickly, indicating effective moderation.

## 8. Backlog Watch

Several important issues and PRs have remained open for **more than a month** without maintainer updates:

| ID | Age | Pending Action |
|----|-----|----------------|
| [#39563 (PR)](https://github.com/NousResearch/hermes-agent/pull/39563) | Since 2026-06-05 | Feishu media replies fix waiting for merge (open, unassigned) |
| [#39564 (PR)](https://github.com/NousResearch/hermes-agent/pull/39564) | Since 2026-06-05 | Desktop scroll/composer jumps fix waiting for merge |
| [#39555 (PR)](https://github.com/NousResearch/hermes-agent/pull/39555) | Since 2026-06-05 | Fix API‑forked sessions listability waiting for merge |
| #39545 (PR) | Since 2026-06-05 | Catch `PermissionError` in `_gh_authenticated` waiting for merge |
| #39542 (PR) | Since 2026-06-05 | Profiles root nesting fix waiting for merge |
| [#37667 (PR)](https://github.com/NousResearch/hermes-agent/pull/37667) | Since 2026-06-02 | Windows in‑app update rebuild fix waiting for merge |
| #39530 (PR) | Since 2026-06-05 | Dashboard uvicorn self‑heal waiting for merge |
| #39539 (PR) | Since 2026-06-05 | Windows taskkill decode error fix waiting for merge |
| [#54801 (issue)](https://github.com/NousResearch/hermes-agent/issues/54801) | Since 2026

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-07-14

## Today's Overview
Project activity remains moderate, with 4 open issues and 5 pull requests updated in the last 24 hours, mostly reflecting community feature requests and internal maintenance. A single PR (#3253) was merged, adding a gateway webhook feature. Several items carry the `stale` label, suggesting a need for maintainer attention, while the most commented issue (#3088) highlights a high-priority security-driven migration from `libolm` to `vodozemac`. Overall, the project shows steady community engagement but has a growing backlog of stagnating contributions.

## Releases
*None today – no new releases detected.*

## Project Progress
- **Merged PR:** **#3253 – Feat/gateway webhook** (by `tisoga`)  
  *Closed on 2026-07-13* – Adds a webhook integration for the AI gateway, enabling external event handling. No breaking changes reported.  
  [GitHub Link](https://github.com/sipeed/picoclaw/pull/3253)

- **Other notable open PRs** (not merged, but part of ongoing work):
  - **#3228** – Aims to enable Anthropic prompt caching on the `anthropic-messages` provider by sending `SystemParts` as blocks with `cache_control`.  
  - **#3254** – Fixes model resolution priority to prefer verbatim matches over provider-alias splits.  
  - **#3192 & #3191** – Chore updates bumping Alpine base images and cleaning up `.gitignore`.

## Community Hot Topics
1. **#3088 – [Feature] Use vodozemac instead of libolm**  
   *8 comments, 2 👍, high priority*  
   Users demand replacing the unmaintained `libolm` with its official successor `vodozemac` for better security. The proposal suggests making `libolm` optional at compile time. This is the most active and highest-urgency issue currently open.  
   [Issue Link](https://github.com/sipeed/picoclaw/issues/3088)

2. **#3229 – Proposal: rolling conversation cache breakpoints for Anthropic**  
   *1 comment*  
   Requests per-block `cache_control` for conversation history in agentic workloads, building on top of the fix in #3228. Highlights a real performance need for long-running tool-use sessions.  
   [Issue Link](https://github.com/sipeed/picoclaw/issues/3229)

3. **#3231 – [Feature] Add BasicAuth request header for SearXNG search**  
   *1 comment*  
   Chinese-language request to support header-based authentication for SearXNG, as the current URL-embedded method is non-functional.  
   [Issue Link](https://github.com/sipeed/picoclaw/issues/3231)

## Bugs & Stability
- **#3230 – [BUG] Function call missing thought_signature with Gemini via OpenAI compat format**  
  *Severity: Medium*  
  Reported across PicoClaw versions 0.2.9 to 0.3.1. When using Google Gemini via Cloudflare AI Gateway in OpenAI-compatible mode, tool calls return a `missing thought_signature` error. No fix PR exists yet, though the issue is only a day old.  
  [Issue Link](https://github.com/sipeed/picoclaw/issues/3230)

- No crashes or regression reports in the past 24 hours.

## Feature Requests & Roadmap Signals
The following user-requested features are likely candidates for the next minor release (v0.3.2 or later):

| Request | Priority | Likelihood |
|---------|----------|------------|
| **vodozemac migration** (#3088) | High (security) | High – already has detailed implementation plan |
| **Anthropic conversation cache breakpoints** (#3229) | Medium | Medium – depends on #3228 being merged first |
| **SearXNG BasicAuth header** (#3231) | Low (niche) | Low – language barrier and low engagement |
| **Gemini thought_signature fix** (#3230) | High (compatibility) | High – blocking basic Gemini tool use |

The PR #3228 (cache_control for Anthropic) is closely tied to #3229 and has strong potential to land soon. The `vodozemac` issue (#3088) has been open since June 9 and may be bundled in a future release if maintainer bandwidth allows.

## User Feedback Summary
- **Positive:** Users appreciate the community effort on Anthropic caching (#3229/#3228) and the new gateway webhook (#3253).
- **Pain points:**
  - **Security concern:** Several users are uneasy about the continued inclusion of `libolm`, which is unmaintained and insecure.
  - **Gemini compatibility:** The `thought_signature` bug affects anyone using Gemini through OpenAI-compatible gateways – a realistic multi-provider use case.
  - **SearXNG authentication:** The current method of appending credentials to the URL is broken, indicating a regression or design flaw.

## Backlog Watch
| Item | Age | Status | Maintainer Action Needed |
|------|-----|--------|--------------------------|
| **#3088** – vodozemac (high priority) | 35 days | Stale (last update yesterday) | Review and assign or triage implementation |
| **#3228** – Anthropic cache_control PR | 8 days | Stale, no maintainer comment | Review and possibly merge – foundational for #3229 |
| **#3192** – Alpine base image bump | 17 days | Stale, awaiting review | Simple chore – should be merged |
| **#3191** – Duplicate gitignore entry | 17 days | Stale | Trivial cleanup – merge |
| **#3229** – Cache breakpoints proposal | 8 days | Stale, no maintainer feedback | Needs maintainer input to gauge feasibility |

All these items have seen no maintainer interaction despite being open for over a week. Clearing the stale PRs (#3191, #3192) would improve project hygiene, while a decision on #3088 would address a key security concern and reduce community frustration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-07-14

## Today’s Overview
NanoClaw saw a burst of activity with **33 pull requests updated** in the last 24 hours — **27 were merged or closed** and **6 remain open**. Three issues were closed, all security-related or bug fixes. No new releases were published. The high PR throughput indicates an accelerated maintenance and feature cycle, with a clear focus on hardening security (approval-flow fixes), improving reliability (missing-adapter handling), and adding new integrations (Dial channel, scheduled tasks, persistent memory).

## Releases
No new releases were cut in the last 24 hours. The latest available version remains unchanged.

## Project Progress
The 27 merged/closed PRs advanced several areas:

- **Security hardening**: Multiple patches addressed the `add_mcp_server` approval smuggling vulnerability, requiring full server payload rendering on approval cards ([#2998](https://github.com/nanocoai/nanoclaw/issues/2998)) and routing messages through retry when adapter is missing ([#2996](https://github.com/nanocoai/nanoclaw/issues/2996)).
- **Infrastructure & CLI fixes**: The `ncl wirings create` command now correctly creates the required `agent_destinations` ACL row ([#2938](https://github.com/nanocoai/nanoclaw/issues/2938)), and a silent data loss bug in the session cleanup script was fixed ([#1889](https://github.com/nanocoai/nanoclaw/issues/1889)).
- **Channel & provider improvements**: A new **Dial** channel adapter (SMS + AI voice calls) was merged ([#3032](https://github.com/nanocoai/nanoclaw/issues/3032)) along with its setup wizard ([#3033](https://github.com/nanocoai/nanoclaw/issues/3033)). Provider output substitution rules ([#2120](https://github.com/nanocoai/nanoclaw/issues/2120)) and a default agent provider for new groups ([#2906](https://github.com/nanocoai/nanoclaw/issues/2906)) also landed.
- **Scheduled tasks**: A highly anticipated feature – recurring cron-driven task templates – was integrated ([#3022](https://github.com/nanocoai/nanoclaw/issues/3022)).

## Community Hot Topics
No issues or PRs accumulated significant comments or reactions in the last 24 hours. The most active threads were all administrative follow-ups to previously reported vulnerabilities. The community’s silence suggests that the rapid closure of high-severity issues is meeting expectations, though the lack of public discussion may also reflect a small contributor base or GitHub-only engagement.

## Bugs & Stability
Three issues were closed today, all after resolution:

| Issue | Severity | Summary | Fix PR |
|-------|----------|---------|--------|
| [#2827](https://github.com/nanocoai/nanoclaw/issues/2827) – Security | Critical | `add_mcp_server` approval card hid runtime `args` and `env`, enabling approval smuggling. | [#2998](https://github.com/nanocoai/nanoclaw/issues/2998) |
| [#2762](https://github.com/nanocoai/nanoclaw/issues/2762) – Security | Critical | Similar hidden `args`/`env` approval bypass (duplicate of #2827). | [#2998](https://github.com/nanocoai/nanoclaw/issues/2998) |
| [#2995](https://github.com/nanocoai/nanoclaw/issues/2995) – Bug | High | Outbound messages to offline/unregistered channel adapters were marked delivered without being sent. | [#2996](https://github.com/nanocoai/nanoclaw/issues/2996), [#2226](https://github.com/nanocoai/nanoclaw/issues/2226) |

All three issues were closed with corresponding fix PRs included in today’s merge batch. No new regressions were reported.

## Feature Requests & Roadmap Signals
Several open PRs point to near-term features likely to land in the next version:

- **Provider-agnostic persistent memory** ([#3012](https://github.com/nanocoai/nanoclaw/issues/3012) – open) – shared memory tree for agent groups, paired with a Codex integration ([#3013](https://github.com/nanocoai/nanoclaw/issues/3013)).
- **MCP tool allowlisting** ([#3037](https://github.com/nanocoai/nanoclaw/issues/3037) – open) – an environment variable to restrict which MCP tools are visible/invocable.
- **Current-time injection into agent context** ([#3036](https://github.com/nanocoai/nanoclaw/issues/3036) – open) – improves day-of-week and hour awareness, especially helpful for scheduled tasks.
- **Socket transport hardening** ([#2802](https://github.com/nanocoai/nanoclaw/issues/2802) – open) – adds timeouts and buffer bounds to host-side `ncl` sockets to prevent resource exhaustion.

These features collectively address operator control, reliability, and agent accuracy. Expect the next release to include at least the memory system and the allowlist if testing completes quickly.

## User Feedback Summary
No explicit user feedback or satisfaction indicators appear in today’s data. However, the following implicit pain points were addressed:

- **Approval-flow opacity**: The repeated security issues around `add_mcp_server` suggest users (or security researchers) are closely auditing self-modification flows. The fix now renders full parameters on approval cards.
- **Silent message drops**: The bug where offline adapters silently accepted deliveries (#2995) likely frustrated operators; the retry-path fix will reduce confusion.
- **Setup reliability**: The diagnostics `DO_NOT_TRACK` fix ([#1887](https://github.com/nanocoai/nanoclaw/issues/1887)) and sqlite3 error handling ([#1889](https://github.com/nanocoai/nanoclaw/issues/1889)) address edge cases that cause silent failures during setup.

## Backlog Watch
The following open PRs have been in review for an extended period relative to their complexity:

| PR | Age (days) | Last Update | Notes |
|----|------------|-------------|-------|
| [#2802](https://github.com/nanocoai/nanoclaw/issues/2802) – Socket hardening | 27 | 2026-07-13 | Still open, no core-team label. May need maintainer review or rebase. |
| [#3012](https://github.com/nanocoai/nanoclaw/issues/3012) – Persistent memory | 4 | 2026-07-13 | High interest, but waiting for Codex counterpart (#3013) to also be finalized. |
| [#3036](https://github.com/nanocoai/nanoclaw/issues/3036) – Time injection | 1 | 2026-07-13 | Very recent; should be reviewed soon. |

No issues in the bug tracker have remained unanswered for more than a week. The two security issues were closed promptly.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-14

## 1. Today's Overview
Activity on the NullClaw repository is **moderate but focused on PR refinement**. No new issues or releases were opened in the last 24 hours, and **zero pull requests were merged or closed**. However, **12 open pull requests** received updates, indicating that contributors are actively polishing features and fixes. The project is in a **consolidation phase**, with several important bug-fix and feature PRs approaching a mergeable state. No regression or crash reports were filed today.

## 2. Releases
**None.**  
No new releases were published on 2026-07-14. The most recent release remains the previously tagged version (not specified in the data).

## 3. Project Progress
No PRs were merged or closed today. The following **open PRs** received updates and represent ongoing work:

- **#970** – `fix(cli): handle arrow keys in agent REPL`  
  Adds a lightweight, allocation-free line editor with POSIX raw-mode input for the interactive REPL.  
- **#969** – `feat(agent): structured approval_request / approval_response flow`  
  Implements a two-turn tool approval mechanism for shell and other tools, emitting events via SSE.  
- **#968** – `fix(matrix): persist next_batch across restart + test env isolation`  
  Fixes a data-loss bug where the Matrix sync cursor was lost on restart, causing full resyncs.  
- **#966** – `fix(http): secure buffered curl fallback on Android`  
  Hardens the HTTP fallback to curl on Android Termux, where Zig’s stdlib DNS resolution can fail.  
- **#964** – `Enable native API-level tool calls during streaming`  
  Preserves structured tool-call deltas in streaming responses so the agent can execute tools mid-stream.  
- **#963** – `fix(channels): document and harden Weixin iLink QR auth`  
  Adds documentation and security hardening for the Weixin transport.  
- **#962** – `docs(providers): document native Anthropic provider with API key and OAuth support`  
  Full documentation for the Native Anthropic provider (direct API + OAuth).  
- **#961** – `feat(memory): add configurable auto-recall, recall_limit, max_context_bytes`  
  Adds three new JSON configuration keys to control memory recall behavior.  
- **#959** – `fix(cron): persist paired token for scheduler tool access (#839)`  
  Persists the paired bearer token to an encrypted file so cron jobs can authenticate after restart.  
- **#958** – `fix(teams): accept lowercase serviceurl JWT claim and raise JWKS fetch cap`  
  Fixes a 403 error in Microsoft Teams connector-token validation (case sensitivity and JWKS fetch limits).  
- **#954** – `Fix: one-shot cron jobs silently fail to deliver messages (use-after-free in OutboundMessage.channel)`  
  Fixes a critical use-after-free bug causing silent delivery failures for scheduled messages.

> **Note:** All PRs above remain open and were updated between 2026-07-13 and 2026-07-14.

## 4. Community Hot Topics
No issues or PRs today garnered explicit comments or reactions (all show `Comments: undefined`). Based on the scope and recency of updates, the following PRs are drawing the most attention from contributors:

- **#954** – *Cron use-after-free*: a blocker for scheduled message delivery; root cause identified and fix proposed.  
- **#968** – *Matrix sync cursor persistence*: a data-loss bug affecting Matrix channel users.  
- **#969** – *Structured approval flow*: introduces a new two-turn tool approval pattern, likely to impact many tools.

**Underlying needs:**  
- **Reliability**: Users expect cron jobs and Matrix syncs to survive restarts.  
- **Security**: Token persistence (PR #959) and auth hardening (PR #958, #963) show demand for safe credential handling.  
- **Usability**: REPL improvements (#970) and documentation (#962, #963) improve the developer/end-user experience.

## 5. Bugs & Stability
No new bugs were reported today, but several **open fix PRs** target known issues. Ranked by severity:

1. **Critical** – **#954** (use-after-free in `OutboundMessage.channel`)  
   Silent message delivery failure for scheduled (“one-shot”) cron jobs. Likely to affect all channels. **Fix exists in open PR.**

2. **High** – **#968** (Matrix `next_batch` not persisted across restart)  
   Forces initial sync on every restart, causing data loss and excessive load. **Fix exists in open PR.**

3. **Medium** – **#958** (Teams 403 due to lowercase `serviceurl` claim)  
   Blocks incoming Teams messages. **Fix exists in open PR.**

4. **Medium** – **#959** (cron token not persisted)  
   Cron jobs fail to authenticate after restart. **Fix exists in open PR.**

5. **Low** – **#966** (Android HTTP fallback)  
   DNS resolution fails on Termux; curl fallback is incomplete. **Fix exists in open PR.**

6. **Low** – **#970** (REPL arrow keys)  
   Input handling improvement, not a functional regression.

## 6. Feature Requests & Roadmap Signals
The following open PRs indicate features likely to appear in the next release:

- **#969** – Structured tool approval with SSE events  
- **#964** – Native API-level tool calls during streaming  
- **#961** – Configurable memory recall (`auto_recall`, `recall_limit`, `max_context_bytes`)  
- **#962** – Native Anthropic provider documentation (already implemented, pending docs merge)

**Predictions for next minor version:**  
- Configurable memory settings  
- Streaming tool execution  
- First-class Anthropic provider support  
- Structured approval UI/eventing for shell tool

## 7. User Feedback Summary
No direct user feedback was captured in the last 24 hours. However, the nature of the open PRs reflects real pain points:

- **“My cron jobs don’t deliver messages”** – addressed by #954 (use-after-free) and #959 (token persistence).  
- **“Matrix channel re-syncs every time I restart”** – addressed by #968.  
- **“Teams messages get 403 errors”** – addressed by #958.  
- **“Termux users have HTTP issues”** – addressed by #966.  

Overall satisfaction is not measurable today, but the volume of bug-fix PRs suggests the project is responsive to user reports.

## 8. Backlog Watch
No issues or PRs with long-standing inactivity were identified from the provided data. All open items have been updated within the last 30 days. The oldest updated PR (#954) was created 2026-06-13 and last updated 2026-07-13, indicating active work.

---

*Generated from [NullClaw GitHub repository](https://github.com/nullclaw/nullclaw) data snapshot for 2026-07-14.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-14

## 1. Today's Overview

Project activity remains very high: **34 issues** and **50 pull requests** were updated in the last 24 hours, with 28 open issues and 34 open PRs. The majority of recent issues originate from an ongoing bug-bash cycle, with 10+ **P2** and **P3** bugs filed by tester `joe-rlo`. On the development side, 5 PRs were merged or closed, advancing the unified extension model (NEA-25), a Matrix channel skeleton, offline migration workflow, and dependency updates. No new releases were made today. The volume suggests a team actively closing defects while pushing forward major architectural changes.

## 2. Releases

No new releases were published today. The previous release train (PR #5598) remains open and unmerged as of July 3.

## 3. Project Progress

**Merged/closed PRs in the last 24 hours (5 total):**

- **#6062** – [Matrix Reborn channel skeleton](https://github.com/nearai/ironclaw/issues/6062) (new WASM channel component, host-managed capability manifest, CI build/test gate).  
- **#6021** – Dependency bump (22 updates across agent-client-protocol, webpki-roots, uuid, etc.).  
- **#6058** – [Ship extension-ownership migration binary](https://github.com/nearai/ironclaw/issues/6058) in the Reborn Railway runtime image, with cargo-chef caching for libSQL/Postgres builds.  
- **#5971** – [Fix: carry storage error cause](https://github.com/nearai/ironclaw/issues/5971) when `persist_summary` fails — now logs the underlying `SessionThreadError` instead of discarding it.  
- **#5957** – [Harden OAuth and per-user extension lifecycles](https://github.com/nearai/ironclaw/issues/5957) (unified Slack OAuth, generic extension-removal cleanup, explicit ownership migration).

Additionally, two bug-bash issues were closed:  
- **#5891** (“Last completed” timestamp bug) – closed after fix.  
- **#5860** (Tool activity details missing during run) – closed.

## 4. Community Hot Topics

**Most active issues (by comment count):**

- **#5948** (5 comments) – ["Assistant incorrectly reports GitHub extension as activated"](https://github.com/nearai/ironclaw/issues/5948). The assistant claims the extension is configured even when only installed. Community discussion indicates confusion about status propagation between UI and model state.  
- **#6050** (2 comments) – ["Conversation history error banner displayed despite successful chat response"](https://github.com/nearai/ironclaw/issues/6050). Users report a persistent failure banner that misleads conversation flow. A fix PR (#6064) is already open.  
- **#6000** (1 comment) – [Security reporting channel missing](https://github.com/nearai/ironclaw/issues/6000). The reporter found a potential vulnerability but cannot file privately — no `SECURITY.md` and GitHub private reporting is disabled. This has not yet received a maintainer response.  
- **#6029** (1 comment) – [GitHub extension cannot be deactivated or uninstalled](https://github.com/nearai/ironclaw/issues/6029) after activation. A lifecycle management gap that may affect usability for many users.

**Top PR by scope:** **#6061** ([Unified extension model – NEA-25 Train A roll-up](https://github.com/nearai/ironclaw/issues/6061)) – 8‑PR stack rolled into a single atomic pull request. This is a major architectural change touching the entire extension taxonomy, wire format, and WebUI.

## 5. Bugs & Stability

**New bugs reported today (severity P1–P3):**

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| P1 | [#5943](https://github.com/nearai/ironclaw/issues/5943) | Slack DM action posts to current channel instead of user’s DMs | No |
| P2 | [#5836](https://github.com/nearai/ironclaw/issues/5836) | Routine fails on every scheduled run with “No thread attached” – 0% success rate | No |
| P2 | [#5885](https://github.com/nearai/ironclaw/issues/5885) | Approval notification opens action without showing approval message | No |
| P2 | [#5879](https://github.com/nearai/ironclaw/issues/5879) | Stale error banner remains after successful follow-up | [#6064](https://github.com/nearai/ironclaw/issues/6064) |
| P2 | [#6048](https://github.com/nearai/ironclaw/issues/6048) | Agent run fails because model calls unavailable tool | No |
| P2 | [#6047](https://github.com/nearai/ironclaw/issues/6047) | Task messages displayed out of chronological order | No |
| P2 | [#6046](https://github.com/nearai/ironclaw/issues/6046) | Email-to-sheet workflow invokes 124 tools (excessive) | No |
| P2 | [#6045](https://github.com/nearai/ironclaw/issues/6045) | Agent diagnoses root cause instead of retrying action | No |
| P2 | [#6044](https://github.com/nearai/ironclaw/issues/6044) | Enter key sometimes does not submit message (WebUI) | No |
| P2 | [#6043](https://github.com/nearai/ironclaw/issues/6043) | GitHub connection flow fails with generic capability error | No |
| P2 | [#6060](https://github.com/nearai/ironclaw/issues/6060) | Routine delivery target leaks across all routines (global default) | No |
| P2 | [#5882](https://github.com/nearai/ironclaw/issues/5882) | Repeated Slack reconnect leaves auth flow broken | No |
| P3 | [#6050](https://github.com/nearai/ironclaw/issues/6050) | Conversation history error banner displayed despite success | [#6064](https://github.com/nearai/ironclaw/issues/6064) |
| P3 | [#6052](https://github.com/nearai/ironclaw/issues/6052) | Extensions Registry takes up to 10 seconds to load | No |
| P3 | [#6051](https://github.com/nearai/ironclaw/issues/6051) | Large documents show warning icon instead of informational | No |
| P3 | [#6049](https://github.com/nearai/ironclaw/issues/6049) | Gmail disconnect fails with generic “Validation” error | No |
| P3 | [#6037](https://github.com/nearai/ironclaw/issues/6037) | Chat connection status hidden during disconnects | No |
| P3 | [#6039](https://github.com/nearai/ironclaw/issues/6039) | Light theme unreadable button/status colors | No |
| P3 | [#6028](https://github.com/nearai/ironclaw/issues/6028) | Stray `$` rendered before MCP heading | No |

**Security:** [#6000](https://github.com/nearai/ironclaw/issues/6000) (no private reporting channel) remains unaddressed and is a process risk.

**Stability trends:** Several P2 bugs indicate systemic issues in routine scheduling, Slack integration, and agent tool routing. The high number of UI/UX bugs (banners, connection status, themes) suggests the WebUI frontend is undergoing active churn.

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signals from open PRs and issues:**

- **Unified extension model (NEA-25):** PRs #6061 (Train A roll-up), #5845 (one Slack extension), #5847 (wire refactor) are in review – a complete taxonomy overhaul.
- **Per-user MCP registration store:** PR #5970 (T1) is open and rebuilt on top of new `InstallationOwner` machinery – likely to land next.
- **Matrix channel support:** PR #6062 (skeleton) was merged today, indicating planned Matrix integration.
- **Offline v1-to-Reborn migration:** PR #5936 (with Docker, libSQL, PostgreSQL support) is open – important for production adopters.
- **System prompt improvements:** PR #6027 adds verification, table-precision, and output-format guidelines to the default system prompt.
- **Tools-capable completion nudges:** PR #6013 enables interactive coding nudges with tool support.
- **Extension ownership migration binary:** PR #6058 shipped today – needed for the new extension model.

**User-requested features:**  
- Ability to deactivate/reconfigure/uninstall extensions (#6029).  
- Security reporting channel (#6000).  
- Better handling of large file loads (#6051, #5741).  
- Cron-based routine reliability (#5836).  

Likely next version will include the unified extension model (NEA-25), MCP registration, and many of the bug-bash fixes currently in progress.

## 7. User Feedback Summary

**Real pain points reported (from issue text):**

- “The assistant says the GitHub extension is activated even though it's only installed” – status inconsistency confuses users.  
- “I see a 'Failed to load conversation history' banner even though my message was sent successfully” – misleading error states.  
- “When I ask to send a Slack DM, the bot posts to the shared channel” – routing logic broken (P1).  
- “After disconnecting and reconnecting Slack multiple times, the auth flow becomes stuck” – no recovery except reinstall.  
- “I cannot deactivate the GitHub extension after activation” – missing lifecycle management.  
- “The light theme makes buttons unreadable” – accessibility issue.  
- “Agent spends 124 tool calls on a simple email-to-sheet task” – inefficiency frustrates users.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-14

## Today's Overview
The project saw intense maintenance activity with **21 pull requests updated in the last 24 hours**, all but two of which were closed or merged. No new releases or issues were created, indicating a focus on polishing and bug fixing rather than new feature introduction. The vast majority of changes originate from core contributor `fisherdaddy`, followed by `liuzhq1986`, suggesting a coordinated push to resolve Windows deployment problems, cowork stability, and UI/UX refinements. Project health appears robust, though community involvement remains low (zero comments on PRs).

## Releases
*None*

---

## Project Progress
The following key changes were merged today, grouped by area:

### Platform & Build (Windows / macOS)
- **#2327** – Fix Windows app binary signing: `electron-builder` had only signed the installer shell, leaving `LobsterAI.exe` unsigned; security software would freeze on first execution. The fix signs every Windows binary via the internal Youdao signing service.  
  [PR #2327](https://github.com/netease-youdao/LobsterAI/pull/2327)
- **#2326** – Self-heal interrupted `win-resources.tar` extraction: the NSIS installer now tries `tar.exe` first and falls back to a bundled extractor with a 10-minute watchdog, preventing unrecoverable install hangs.  
  [PR #2326](https://github.com/netease-youdao/LobsterAI/pull/2326)
- **#2323** – Add opt-in Windows web installer target: gated by `LOBSTERAI_WEB_INSTALLER`, downloads the app package from a CDN at install time.  
  [PR #2323](https://github.com/netease-youdao/LobsterAI/pull/2323)
- **#2321** – Fix `hdiutil` failure on macOS updates.  
  [PR #2321](https://github.com/netease-youdao/LobsterAI/pull/2321)

### Cowork & Notifications
- **#2318** – Upgrade desktop notifications: renamed `TaskCompletionNotifier` to `DesktopNotificationManager`, added waiting notifications for permission requests and questions, foreground mode, and stale alert tracking.  
  [PR #2318](https://github.com/netease-youdao/LobsterAI/pull/2318)
- **#2324** – Stream ordered thinking blocks: display OpenClaw thinking as per-turn blocks before tools/final response, preventing duplicate thinking during history reconciliation.  
  [PR #2324](https://github.com/netease-youdao/LobsterAI/pull/2324)
- **#2319** – Revamp homepage quick-action scenarios: replaced "教育学习" with "文档写作" mapped to docx skill; refreshed copy for PPTX and website prompts; kept chip bar visible after category selection.  
  [PR #2319](https://github.com/netease-youdao/LobsterAI/pull/2319)
- **#2315** – Connect queued follow-up coordinator: process follow-ups across sessions and while minimized.  
  [PR #2315](https://github.com/netease-youdao/LobsterAI/pull/2315)
- **#2292** – Stabilise steer follow-up routing: added Codex-style queued steer follow-ups, replaced temporary new-chat sessions with real ones, scoped streaming state to active session.  
  [PR #2292](https://github.com/netease-youdao/LobsterAI/pull/2292)
- **#2300** – Support attachments in steer queue: allow files, dragged/pasted items, selected text, and images in queued follow-ups.  
  [PR #2300](https://github.com/netease-youdao/LobsterAI/pull/2300)
- **#2325** – Fix badge/title descender clipping and stabilise template in cowork UI.  
  [PR #2325](https://github.com/netease-youdao/LobsterAI/pull/2325)
- **#2320** – Fast-forward missed cron jobs instead of skipping catch-up alone: prevents replay of every missed job on first timer tick.  
  [PR #2320](https://github.com/netease-youdao/LobsterAI/pull/2320)
- **#2289** – Clear stalled compaction retry maintenance: reuse recoverable wait path for auto-compaction retries, added regression coverage.  
  [PR #2289](https://github.com/netease-youdao/LobsterAI/pull/2289)

### Other Fixes
- **#2328** – Fix serialise concurrent browser launch/search to stop Chrome leaks.  
  [PR #2328](https://github.com/netease-youdao/LobsterAI/pull/2328)
- **#2322** – Optimise file card rendering.  
  [PR #2322](https://github.com/netease-youdao/LobsterAI/pull/2322)
- **#2316** – Prevent Windows title bar logo compression when sidebar is collapsed with an update badge.  
  [PR #2316](https://github.com/netease-youdao/LobsterAI/pull/2316)

### Stale PRs Closed Today
- **#1488** – Scheduled task UI upgrade (cards, search, history grouping) – merged after months.  
  [PR #1488](https://github.com/netease-youdao/LobsterAI/pull/1488)
- **#1494** – Cowork skill selection state per session – merged.  
  [PR #1494](https://github.com/netease-youdao/LobsterAI/pull/1494)

---

## Community Hot Topics
No issues were created or updated in the last 24 hours, and all PRs have **0 comments** and **0 reactions**. The lack of community discussion suggests either a low external contributor base or that the project’s maintainers are driving changes internally. Two long-standing **open PRs** remain:

- **#1277** (dependabot, Electron bump from 40.2.1 to 43.1.0) – Open since April, last updated July 13.  
  [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)
- **#1323** (stale, cowork input-too-long error classification) – Open since April, needs maintainer review.  
  [PR #1323](https://github.com/netease-youdao/LobsterAI/pull/1323)

These may represent untapped stability or dependency updates that could affect future releases.

---

## Bugs & Stability
Several high-severity bugs were fixed today:

| Severity | Bug | Fix PR |
|----------|-----|--------|
| **Critical** | Windows installer hangs due to unsigned `LobsterAI.exe` | #2327 |
| **Critical** | Interrupted `win-resources.tar` extraction makes installation unrecoverable | #2326 |
| **High** | Chrome leaks caused by concurrent browser launches | #2328 |
| **High** | Missed cron jobs replayed on first timer tick despite skip logic | #2320 |
| **High** | Stalled compaction retries not cleared, causing infinite maintenance loops | #2289 |
| **Medium** | macOS update fails with `hdiutil` error | #2321 |
| **Medium** | Title bar logo compressed on Windows when sidebar collapsed with badge | #2316 |
| **Low** | Badge/title descender clipping in cowork template | #2325 |

All critical and high-severity items have been addressed with merged PRs today.

---

## Feature Requests & Roadmap Signals
No user-submitted feature requests are visible in the data. However, the merged PRs point to the following internal roadmap priorities:

- **Desktop notification system** – upgraded to cover waiting states and foreground mode (likely aimed at proactive user engagement).  
- **Ordered thinking blocks** in OpenClaw – improves transparency of AI reasoning.  
- **Quick-action scenarios** on homepage – better onboarding for document creation tasks.  
- **Web installer option** – simplifies distribution and updates.  
- **Attachment support in steer queue** – enables richer multi-modal interaction during follow-ups.

These features are already merged, so they will appear in the next release. No breaking changes are evident.

---

## User Feedback Summary
While no explicit user comments are recorded, the fixes implicitly address real-world pain points reported through bug reports or internal testing:

- **Windows installer failures** – security software interference and broken extraction were causing field installs to hang, a critical UX failure.  
- **Unsigned executables** – led to security software false positives, degrading trust.  
- **Missing notifications** – users were not alerted to pending permission requests or questions, reducing responsiveness.  
- **Stale notifications** – fixed by tracking resolved requests, preventing confusion.  
- **UI clipping** – badge/title alignment was broken on certain templates.  
- **Inconsistent skill selection** across sessions (fixed in #1494) – a long-standing usability annoyance.

The rapid closure of these issues suggests good internal feedback loops, but the absence of public community commentary limits external satisfaction assessment.

---

## Backlog Watch
The following open PRs require maintainer attention:

- **#1277** – Dependabot PR to bump Electron and electron-builder. Open since **2026-04-02**; updated July 13 but still not merged. This is a security and compatibility dependency update that should be prioritised.  
  [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)

- **#1323** – Fix cowork input-too-long error classification (marked stale). Open since **2026-04-02**; last updated July 13 (likely stale bot). The change fixes misleading UI errors for short user inputs.  
  [PR #1323](https://github.com/netease-youdao/LobsterAI/pull/1323)

No issues are currently open, so the backlog is only these two PRs. They have been open for over three months and should be reviewed for merge or close to reduce technical debt.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-14

## Today's Overview
Moltis shows minimal activity over the past 24 hours: no issues were updated (open or closed) and no new releases were published. One pull request (#1147) was updated recently, though it remains open and has not been merged. The project appears to be in a quiet maintenance phase, with the only noteworthy motion being a bug fix for the CalDAV integration. Overall health is stable but contributions are low.

## Releases
*No new releases have been published (latest release data is empty).*

## Project Progress
No pull requests were merged or closed today. The only PR with recent activity is **#1147 – fix(caldav): honor time range in list_events via server-side calendar-query** (author: thoscut, created 2026-07-11, last updated 2026-07-13). This PR addresses a critical functional gap in the CalDAV client where the `start` and `end` parameters of `list_events` were ignored, causing the tool to always fetch all calendar resources regardless of the requested time range.

## Community Hot Topics
The sole active PR **#1147** is the only item drawing attention. With zero comments or reactions reported, there is no significant community discussion at this time. The underlying need—correct handling of time-range filters in calendar queries—is a functional correctness issue that directly impacts user trust in the CalDAV tool.

## Bugs & Stability
**Medium severity** – Bug: The `list_events` tool in the CalDAV client ignored the provided time range and always returned all events. This contradicted documentation and could lead to performance degradation or incorrect results on servers that rely on client-side filtering. A fix is proposed in PR #1147, which rewrites the query to issue a proper CalDAV calendar-query with time-range parameters. No other bugs or regressions were reported.

## Feature Requests & Roadmap Signals
No new feature requests were raised or updated in the past 24 hours. The single PR is a bug fix, not a feature. Given the low activity, no clear roadmap signals can be inferred from this data.

## User Feedback Summary
No direct user feedback (comments, reactions, or issue descriptions) was provided in the last day. The existence of PR #1147 suggests that at least one user or contributor encountered a discrepancy between documented behavior and actual implementation, indicating a pain point in using `list_events` with time constraints.

## Backlog Watch
No long-unanswered issues or PRs currently require maintainer attention. The only open PR (#1147) is recent and has been updated within the last two days, so it is still actively progressing. No items are flagged as stale.

---
*All links:*  
- [PR #1147](https://github.com/moltis-org/moltis/pull/1147)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-14

**Data Source:** GitHub (agentscope-ai/CoPaw, issues/PRs updated in last 24h as of 2026-07-14)

---

## 1. Today's Overview

The project is experiencing **very high activity** with 50 issues and 50 pull requests updated in the last 24 hours, plus a new patch release (v2.0.0.post1). The vast majority of discussion and development effort is focused on **stabilising the v2.0.0 release**, which has introduced multiple regressions compared to the v1.x line. Users report frequent `400 BadRequestError` due to orphaned `tool_result` messages, context compression breaking message pairing, and missing features like the message queue. A total of 23 issues were closed and 28 PRs were merged/closed in the past day, indicating a rapid response by maintainers to the most critical bugs.

---

## 2. Releases

**v2.0.0.post1** was released [today](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0.post1).  
**What's Changed:**
- Fixed browser autofill on provider search input (#5981)
- Fixed legacy session handling
- Version bump from 2.0.0 to 2.0.0.post1

This is a hotfix release; no breaking changes or migration notes beyond upgrading. Users on v2.0.0 are encouraged to update immediately.

---

## 3. Project Progress

**28 PRs were merged or closed today.** Notable merges include:

- **[#6058](https://github.com/agentscope-ai/QwenPaw/pull/6058)** – Flatten offload hint message and temporarily disable broken offload mechanism (critical bug fix for tool-call offloading)
- **[#6052](https://github.com/agentscope-ai/QwenPaw/pull/6052)** – Fix orphan `ToolResultBlock` in background tool hints (fix for #5996)
- **[#6045](https://github.com/agentscope-ai/QwenPaw/pull/6045)** – Clear message queue when a session is deleted (fix for #6006)
- **[#6044](https://github.com/agentscope-ai/QwenPaw/pull/6044)** – Bridge plugin `register_tool` to runtime `ToolRegistry` pipeline (fix for missing tools)
- **[#6061](https://github.com/agentscope-ai/QwenPaw/pull/6061)** – Add unit tests for Ponytail Quality plugin backend
- **[#5935](https://github.com/agentscope-ai/QwenPaw/pull/5935)** – Unify tool result pruning with block-scoped metadata (refactor, fixes multiple pruning issues)
- **[#5791](https://github.com/agentscope-ai/QwenPaw/pull/5791)** – Fix `formatCompact` rounding rollover in console

Open PRs advancing features include [#6067](https://github.com/agentscope-ai/QwenPaw/pull/6067) (more sensitive file handling), [#6063](https://github.com/agentscope-ai/QwenPaw/pull/6063) (bridge frontend tool-guard rules into policy deep scan), and [#6041](https://github.com/agentscope-ai/QwenPaw/pull/6041) (fix doom loop detection for read-only tools).

---

## 4. Community Hot Topics

The most discussed issues (by comment count) reveal three key user pain points:

1. **[#5996](https://github.com/agentscope-ai/QwenPaw/issues/5996)** (10 comments) – *"2.0.0对话时会产生MODEL_EXECUTION_ERROR"*  
   Root cause identified: orphaned `ToolResultBlock` in hint messages. **Already fixed** by PR #6052.

2. **[#5961](https://github.com/agentscope-ai/QwenPaw/issues/5961)** (7 comments, still open) – *"v2.0.0版本循环执行的问题"*  
   Agent repeatedly writes/deletes files when using Qwen3.7-Plus, stuck in infinite loops. No fix PR linked yet.

3. **[#5947](https://github.com/agentscope-ai/QwenPaw/issues/5947)** (6 comments, closed) – *"MCP中禁用了某些子工具的访问,但是agent还是可以调用"*  
   MCP tool allow/deny rules not respected. Likely related to governance pipeline gaps; PR #6063 aims to address this.

Users are clearly **dissatisfied with v2.0.0 stability** (see #6006, #6013, #6034) and many compare unfavourably to v1.x or competing products.

---

## 5. Bugs & Stability

**High severity** (blocking core functionality):

- **Context compression breaks tool_call/tool_result pairing** → `400 BadRequestError`  
  Affected issues: #5986, #5960, #5962, #6049  
  Fix PRs: #5935 (merged), #6058 (merged) – partially addressed; root cause in `_split_context_for_compression()` may still need further work.

- **MCP tool allow/deny rules ignored** (#5947, #5984)  
  No dedicated fix merged yet; PR #6063 in progress.

- **Message queue feature missing in v2.0.0** (#6006) – **Fixed** by PR #6045.

- **Desktop / Docker regressions:**
  - SSH Offline and Profiles returning 404 (#5980) – feature gap.
  - Docker `browser_use` fails due to dbus errors (#5872) – open.
  - Electron CLI crashes on Linux when sandbox maps user to root (#5979) – open.
  - `qwenpaw-backend.exe` missing submodule `agentscope.tool._builtin._scripts` (#5965) – **fixed** in v2.0.0.post1? Not explicitly.

**Medium severity:**

- `execute_shell_command` hard-capped at 60s, ignoring user timeout config (#5963) – open.
- Background offload kills subprocess immediately (#6056) – open.
- `Dream` auto-memory fails with `ModuleNotFoundError` (#6024, #6012) – fix not yet confirmed.

**Low severity / niche:**

- TUI crash on mouse click on streaming output (#6008) – fix PR #6069 open.
- Plugin HTTP routes lost after workspace hot-reload (#5977) – open.

---

## 6. Feature Requests & Roadmap Signals

User requests that are likely to influence the next minor version:

- **CIDR whitelist for authentication bypass** ([#6048](https://github.com/agentscope-ai/QwenPaw/issues/6048)) – simple network config.
- **Ability to use AgentScope permission control features in QwenPaw** ([#5958](https://github.com/agentscope-ai/QwenPaw/issues/5958)) – governance consolidation.
- **Configurable shell command timeout** ([#5963](https://github.com/agentscope-ai/QwenPaw/issues/5963)) – already has PR #5935 groundwork.
- **Environment variables not passed to agents** ([#6055](https://github.com/agentscope-ai/QwenPaw/issues/6055)) – Docker env ignored.
- **Improved tool white-list mode** ([#5955](https://github.com/agentscope-ai/QwenPaw/issues/5955)) – similar to #5984.

The roadmap appears focused on **stabilising v2.0** first, with governance improvements (PR #6063, PR #6054) and better timeout/hint handling likely landing in the next patch.

---

## 7. User Feedback Summary

- **Frustration with v2.0.0 instability:** Multiple users explicitly state that v2.0.0 is “worse than v1” (#6013, #5980, #6034) and that they had to downgrade.
- **Workflow disruptions:** Internal errors on WeChat/Feishu channels, infinite loops, and missing message queue break daily operations.
- **Positive notes:** The development team is responsive – many critical issues are closed within 24 hours of being reported (e.g., #5996, #6006). Users appreciate the rapid patches.
- **Feature parity demand:** Users migrating from v1.x expect SSH offline, full skill list display (>20 items), and working tool governance.

---

## 8. Backlog Watch

Issues and PRs that have been open for a significant time without resolution:

- **[#2439](https://github.com/agentscope-ai/QwenPaw/issues/2439)** – Voice message transcription broken (opened 2026-03-28, 4 comments) – no recent activity.
- **[#5872](https://github.com/agentscope-ai/QwenPaw/issues/5872)** – Docker `browser_use` dbus failure (opened 2026-07-09, 5 comments) – no maintainer response.
- **[#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980)** – Missing features after upgrade (opened 2026-07-12, 5 comments) – no official fix yet.
- **[#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069)** – Visual model fallback (opened 2026-06-10) – still open, needs review.
- **[#5927](https://github.com/agentscope-ai/QwenPaw/pull/5927)** – GBK compatibility fix (opened 2026-07-10) – marked ready for human review but not merged.

These items indicate missing maintainer bandwidth for non-critical features and platform-specific bugs. Users on Windows (GBK) and ARM devices (Docker sandbox) are particularly underserved.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-14

## Today's Overview

ZeroClaw is in an active development and planning phase, with 50 issues and 50 pull requests updated in the last 24 hours. The project is preparing to close the v0.8.3 milestone — all six child trackers are closed, leaving only the release index (#7320) while final validation and publication are finished. The v0.8.4 maintenance train (#8357) is already open with a target of July 31. Activity is heavy across runtime execution, memory subsystem parity, configuration validation, and a governance RFC on work lanes and board automation. Maintainers are reviewing multiple high-risk contributions, and a notable number of PRs are blocked waiting for author action.

## Releases

No new releases in the last 24 hours. The v0.8.3 release is being finalized; v0.8.4 planning is underway.

## Project Progress

**Merged/closed PRs today (3 total, 2 visible in top-20 list):**

- [#8777 – fix(zerocode): strip markdown fences from code block copy text](https://github.com/zeroclaw-labs/zeroclaw/pull/8777) — Closed. ZeroCode’s `[Copy]` button now returns plain code body instead of fenced markdown.
- [#8562 – fix(cron): filter `recv_log_event` by `job_id` to prevent cross-test broadcast pollution](https://github.com/zeroclaw-labs/zeroclaw/pull/8562) — Closed. Fixes a flaky test caused by broadcast subscriber pollution during parallel test runs.

*(The third merged/closed PR was not visible in the sample; total confirmed: 3.)*

**Feature & enhancement advances visible in open PRs:**

- [#8438 – feat(cron): add `shell_output_format` config for raw stdout output](https://github.com/zeroclaw-labs/zeroclaw/pull/8438) — Adds per-job option to emit plain stdout instead of the wrapped envelope.
- [#8440 – feat(telegram): add per-channel inbound debounce](https://github.com/zeroclaw-labs/zeroclaw/pull/8440) — Operators can now override global debounce per Telegram alias.
- [#8443 – feat(matrix): add single-message progress drafts](https://github.com/zeroclaw-labs/zeroclaw/pull/8443) — Large addition (size:XL) for Matrix streaming with progress drafts and typed tool events.
- [#8779 – fix(zerocode): use daemon final text when no streaming text was accumulated](https://github.com/zeroclaw-labs/zeroclaw/pull/8779) — Improves turn commit reliability for non-streaming scenarios.
- [#9018 – fix(cli): apply config-dir before locale detection](https://github.com/zeroclaw-labs/zeroclaw/pull/9018) — Bootstrap `--config-dir` before i18n so explicit config controls locale.
- [#9049 – fix(i18n): localize agent-scope rejection](https://github.com/zeroclaw-labs/zeroclaw/pull/9049) — Completes five-locale coverage for a recent authorization message.
- [#9051 – fix(release): restore lean prebuilt feature set](https://github.com/zeroclaw-labs/zeroclaw/pull/9051) — Reverts an accidental broadening of the standard distribution.

**Tracker updates:** The v0.8.3 milestone index (#7320) reports all implementation work merged or moved out. The persistent memory tracker (#8891) and the SOP milestone tracker (#8288) are both active.

## Community Hot Topics

**Most commented issues (top three):**

1. [#6808 – RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) — *14 comments*  
   Governance RFC, revision 16, accepted and in rollout. Proposes automated routing without manual board maintenance. High engagement indicates strong community interest in contributor workflow improvements.

2. [#6165 – RFC: Prefer a lighter ZeroClaw core through external integrations](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) — *9 comments*  
   Defines boundary for moving long-tail integrations to skills/MCP/plugin-hosted tools. Underlying need: reduce core bloat while preserving extensibility.

3. [#5287 – Feature: Local-First Mode for Small Models](https://github.com/zeroclaw-labs/zeroclaw/issues/5287) — *5 comments, 2 👍*  
   Requests compact prompting, strict parsing, and no prompt leakage for local small models. Represents a vocal user segment wanting better offline capability.

**Most active PRs** (by comment count are undefined in the data, but the following have received maintainer attention and author-action labels):
- [#8927 – fix(providers): remove unconditional `strip_think_tags`](https://github.com/zeroclaw-labs/zeroclaw/pull/8927) — Community contributor wangmiao0668000666 addresses reasoning model compatibility with MiniMax.
- [#8898 – fix(memory): let durable global memories reach semantic recall across sessions](https://github.com/zeroclaw-labs/zeroclaw/pull/8898) — Critical memory fix awaiting author action.

## Bugs & Stability

**Bugs reported/updated in the last 24 hours, ranked by severity:**

- **S1 – Workflow blocked:**
  - [#9035 – Docker Compose gateway can remain loopback-bound behind a published port](https://github.com/zeroclaw-labs/zeroclaw/issues/9035) (updated 2026-07-13, 3 comments). Port unreachable after `docker compose up -d`. No fix PR visible yet.

- **S2 – Degraded behavior:**
  - [#9046 – models_cache.json is read but never written](https://github.com/zeroclaw-labs/zeroclaw/issues/9046) (created 2026-07-13, 1 comment). `/model` command always fails because cache file is never created.
  - [#9028 – Ctrl+C on Windows causes force quit with exit code 1073741510](https://github.com/zeroclaw-labs/zeroclaw/issues/9028) (created 2026-07-13, 1 comment). Graceful shutdown broken on Windows.

- **S3 – Minor issues:**
  - [#8847 – cargo test --doc fails with duplicated rustdoc theme flag](https://github.com/zeroclaw-labs/zeroclaw/issues/8847) (updated 2026-07-14, 0 comments). CI tooling issue under Rust 1.96.
  - [#6548 – Channel runtime command replies bypass Fluent localization](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) (updated 2026-07-13, 3 comments). Hard-coded English strings persist even under `zh-CN` locale.

**Fix PRs in progress for these bugs:**
- [#9049](https://github.com/zeroclaw-labs/zeroclaw/pull/9049) addresses the localization gap (#6548) for agent-scope rejection.
- [#9037](https://github.com/zeroclaw-labs/zeroclaw/pull/9037) fixes trailing provider terminal markers leaking into transcript (related to #9006).
- [#9029](https://github.com/zeroclaw-labs/zeroclaw/pull/9029) fixes OpenAi vision capability configuration (#9019).
- [#8781](https://github.com/zeroclaw-labs/zeroclaw/pull/8781) removes stale security advisory ignores causing CI gate failure.

Other bugs mentioned in the sample: [#9044](https://github.com/zeroclaw-labs/zeroclaw/issues/9044) (Google Workspace camelCase methods rejected) — closed as a quick fix, but not yet merged.

## Feature Requests & Roadmap Signals

**Notable feature requests with recent activity:**

- [#5287 – Local-First Mode for Small Models](https://github.com/zeroclaw-labs/zeroclaw/issues/5287) — Accepted with risk:high. Likely to be included in v0.8.4 or later as it addresses a core use case for offline users.
- [#8997 – Warn when peer_groups.*.channel ref points at a non-existent channel alias](https://github.com/zeroclaw-labs/zeroclaw/issues/8997) — Accepted, risk:medium. A config validation quality-of-life improvement.
- [#8998 – Dedicated GUI surface for a channel's pending one-time bind code](https://github.com/zeroclaw-labs/zeroclaw/issues/8998) — Accepted, risk:high. Would improve onboarding for Telegram/WeChat/Line pairing.
- [#9022 – Optional Slack Events API (HTTP) mode for scale-to-zero deploys](https://github.com/zeroclaw-labs/zeroclaw/issues/9022) — Accepted, risk:high. Responds to a common deployment pattern.
- [#9048 – RFC: Separate conversation history from agent-curated long-term memory](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) — Created today, 1 comment. Proposes architectural separation to fix mixing of session history and long-term memory in the same backend.

**Roadmap signals:** The v0.8.4 maintenance train (#8357) is open. The persistent memory tracker (#8891) and SOP control plane tracker (#8288) are actively being worked and will likely define major v0.8.4 features. The governance RFC #6808 (work lanes automation) is in rollout and will affect future maintenance processes.

## User Feedback Summary

**Pain points voiced in recent issues and PRs:**

- Local-first users want a compact mode without prompt bloat and with strict parsing (#5287).
- Windows users are experiencing a force-quit on Ctrl+C (#9028), degrading the interactive experience.
- Non-English users encounter untranslated channel replies (#6548), despite locale configuration.
- Docker Compose deployers hit a “connection refused” bug (#9035) that blocks evaluation.
- Model cache never being written (#9046) makes the `/model` command unusable until a fix lands.
- Google Workspace tool users cannot call camelCase methods like `batchUpdate` (#9044), limiting integration.
- Some users desire Slack Events API over HTTP for serverless deployments (#9022).

**Positive signals:** The community is actively submitting fixes (e.g., @wangmiao0668000666, @Project516, @JordanTheJet). The high number of “good first issue” labeled issues (e.g., #7694, #7688) and comprehensive trackers suggest a healthy contributor onboarding path.

**Satisfaction indicators:** The rapid closure of v0.8.3 trackers and the start of v0.8.4 planning indicate maintainers are keeping pace with scope. However, the S1 Docker Compose bug and the Windows crash are urgent regressions that may erode user confidence if not addressed quickly.

## Backlog Watch

**Important issues and PRs needing maintainer attention** (based on `needs-maintainer-review`, `needs-author-action`, or long-standing without activity):

| Item | Type | Age | Status |
|------|------|-----|--------|
| [#8891 – Persistent memory parity tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8891) | Issue (tracker) | Since Jul 9 | `needs-maintainer-review`, `no-stale` |
| [#8288 – SOP milestone: daemon-owned control plane](https://github.com/zeroclaw-labs/zeroclaw/issues/8288) | Issue (tracker) | Since Jun 24 | `no-stale`, open |
| [#8691 – Restore ADR baseline and audit accepted RFCs](https://github.com/zeroclaw-labs/zeroclaw/issues/8691) | Issue (tracker) | Since Jul 4 | `needs-maintainer-review`, `no-stale` |
| [#7685 – Test coverage tracker across 13 shards](https://github.com/zeroclaw-labs/zeroclaw/issues/7685) | Issue (tracker) | Since Jun 15 | Open, risk:high |
| [#7686 – feat(runtime): cover approval-gated tool execution ordering](https://github.com/zeroclaw-labs/zeroclaw/issues/7686) | Issue (enhancement) | Since Jun 15 | Open, **priority p1**, risk:high |
| [#8357 – v0.8.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*