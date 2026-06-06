# OpenClaw Ecosystem Digest 2026-06-06

> Issues: 467 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-06 02:31 UTC

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

# OpenClaw Project Digest – 2026-06-06

## Today's Overview
The OpenClaw project is in a period of **intense maintenance and active development**. In the last 24 hours, **467 issues were updated** (338 open, 129 closed) and **500 pull requests were updated** (364 open, 136 merged/closed). No new releases were cut today. The activity is dominated by regression fixes, stability improvements, and feature discussions around provider compatibility, session management, and channel integrations. The community is actively reporting and triaging regressions introduced in recent releases (2026.5.x → 2026.6.1), with a notable number of P1 bugs related to message loss and session state.

## Releases
None.

## Project Progress
**136 pull requests were merged or closed** in the last 24 hours. Notable closed/merged PRs that advanced the codebase:

- **[#90748](https://github.com/openclaw/openclaw/pull/90748)** – fix(memory): resolve adapter default model in plain status identity check (memory status now shows correct model after reindex)
- **[#90736](https://github.com/openclaw/openclaw/pull/90736)** – fix(macOS) node mode self-reconnect loop (prevents silent reconnection in healthy direct gateway sessions)
- **[#90773](https://github.com/openclaw/openclaw/pull/90773)** – fix(agents): keep auto-compaction appends owned during prompt lock release (improves session transcript integrity)
- **[#90620](https://github.com/openclaw/openclaw/pull/90620)** – fix(voice-call): preserve live Twilio streams in stale reaper (prevents live calls from being killed)
- **[#90772](https://github.com/openclaw/openclaw/pull/90772)** – fix: guard routing (routing guard fix)
- **[#90809](https://github.com/openclaw/openclaw/pull/90809)** – fix(tui): show immediate feedback while loading models (UX improvement for CLI)

## Community Hot Topics
Issues and PRs with the most engagement:

### Most Commented Issues
- **[#22438](https://github.com/openclaw/openclaw/issues/22438)** – **Tiered bootstrap file loading for progressive context control** (17 comments, 2 months old, still open). Users want to avoid wasting LLM tokens on full workspaces in every session. The feature is high-impact but awaits product decisions and maintainer review.
- **[#62505](https://github.com/openclaw/openclaw/issues/62505)** – **Coding Agent never completes anything** – regression from 2026.4.2 (14 comments, P1). This is a critical regression affecting coding workflow agents. Community is reporting that the agent produces only vague status updates and apologies. No fix PR is yet linked.
- **[#76562](https://github.com/openclaw/openclaw/issues/76562)** – **High CPU and extreme control-plane latency after upgrade to 2026.4.29/5.2** (13 comments, closed). This was a severe performance regression that has now been resolved.
- **[#90083](https://github.com/openclaw/openclaw/issues/90083)** – **OpenAI ChatGPT Responses transport fails with `invalid_provider_content_type` for gpt-5.4/gpt-5.5** (12 comments, opened June 4, P1). A compatibility issue with the latest OpenAI models that blocks users after upgrading to 2026.6.1.
- **[#78308](https://github.com/openclaw/openclaw/issues/78308)** – **Channel-mediated approval for MCP tool calls** (12 comments). Feature request for a consent envelope pattern, analogous to shell-exec approval.

### Active PR Discussions
- **[#90811](https://github.com/openclaw/openclaw/pull/90811)** – "fix(agents): stabilize user-turn serialization across turns to preserve prompt cache" – opened today, waiting on author. Aims to improve token efficiency by keeping the system prompt stable across turns.
- **[#78441](https://github.com/openclaw/openclaw/pull/78441)** – "feat(subagents): forward toolsAllow from sessions_spawn" – a large feature PR (size L) that adds per-subagent tool allowlisting. Awaiting real-behavior proof and maintainer review.

## Bugs & Stability

### Critical / P1 Regressions
- **Coding Agent never completes** ([#62505](https://github.com/openclaw/openclaw/issues/62505)) – regression from 2026.4.2, affects all coding workflows. No fix PR yet.
- **OpenAI gpt-5.4/gpt-5.5 transport failure** ([#90083](https://github.com/openclaw/openclaw/issues/90083)) – blocks use of latest models on 2026.6.1. No fix PR, community reports a migration/config issue.
- **Mattermost slash commands return 503** ([#68113](https://github.com/openclaw/openclaw/issues/68113)) – closed, fixed in recent release.
- **Heartbeat/system events interrupt in-progress Telegram replies** ([#64810](https://github.com/openclaw/openclaw/issues/64810)) – P1, still open. Can cause message loss in forum topics.
- **Codex OAuth refresh failures wedge agents for hours** ([#86215](https://github.com/openclaw/openclaw/issues/86215)) – P1, no clear alerting. Users can lose functionality without noticing.
- **MCP tools not injected into subagent sessions** ([#85030](https://github.com/openclaw/openclaw/issues/85030)) – P1, affects all users relying on `sessions_spawn` with MCP servers.
- **Lobster workflow hangs when launched from agent prompt** ([#87756](https://github.com/openclaw/openclaw/issues/87756)) – regression, P1.
- **Matrix channel dispatch broken in v2026.6.1** ([#90325](https://github.com/openclaw/openclaw/issues/90325)) – new regression (June 5), TypeError on inbound messages. No fix PR.

### Other Notable Bugs
- **Feishu streaming card abnormal typewriter and truncated content** ([#88929](https://github.com/openclaw/openclaw/issues/88929)) – P2, reported June 1.
- **WebChat session transcript overwritten on every turn** ([#77012](https://github.com/openclaw/openclaw/issues/77012)) – regression from 5.2, still open.
- **Cron state silently wiped during SQLite migration to 2026.6.1** ([#90072](https://github.com/openclaw/openclaw/issues/90072)) – closed, but data loss concern.
- **launchd plist hides all gateway stderr** ([#90711](https://github.com/openclaw/openclaw/issues/90711)) – regression in 5.28, hides diagnostics.

### Fix PRs in Flight
- [#90811](https://github.com/openclaw/openclaw/pull/90811) (user-turn cache stability) – may address token waste and session issues.
- [#90773](https://github.com/openclaw/openclaw/pull/90773) (auto-compaction owned writes) – merged today, improves transcript consistency.
- [#90689](https://github.com/openclaw/openclaw/pull/90689) (custom provider auth labels) – awaiting author.
- [#90805](https://github.com/openclaw/openclaw/pull/90805) (Codex native hook relay fail-closed) – P1, still needs proof.

## Feature Requests & Roadmap Signals

### High-Interest Features
- **Tiered bootstrap file loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – 17 comments, likely to be implemented in next release to reduce token waste.
- **Channel-mediated MCP approval envelope** ([#78308](https://github.com/openclaw/openclaw/issues/78308)) – 12 comments, addresses security concerns for external tool calls.
- **Per-agent memory-wiki vault configuration** ([#63829](https://github.com/openclaw/openclaw/issues/63829)) – 9 upvotes, requested for multi-agent setups.
- **Allow hiding/collapsing Workspace rail in WebChat** ([#90246](https://github.com/openclaw/openclaw/issues/90246)) – UX enhancement.
- **Session duration/token caps** ([#64463](https://github.com/openclaw/openclaw/issues/64463)) – cost control for long-running sessions.
- **Discord role-based access lists with per-channel overrides** ([#69748](https://github.com/openclaw/openclaw/issues/69748)) – replaces the current `requireMention` approach.
- **exec() sandbox isolation inspired by Claude Code** ([#58730](https://github.com/openclaw/openclaw/issues/58730)) – security hardening.

### PRs That Signal Future Direction
- **[#78441](https://github.com/openclaw/openclaw/pull/78441)** – `toolsAllow` for `sessions_spawn` – likely to land in next minor release, enabling fine-grained subagent tool control.
- **[#90328](https://github.com/openclaw/openclaw/pull/90328)** – Expose model picker agent runtimes in WebUI – improves visibility for runtime selection.
- **[#88683](https://github.com/openclaw/openclaw/pull/88683)** – Reject unpublished npm targets in update dry-run – CLI reliability.

## User Feedback Summary

**Pain Points (reported in last 24h / recent days):**
- **Regressions after upgrading**: Several users report that the coding agent (workhorse for many) stopped working entirely in 2026.5.x/6.x ([#62505](https://github.com/openclaw/openclaw/issues/62505)). New OpenAI models (gpt-5.4/5.5) fail with cryptic errors ([#90083](https://github.com/openclaw/openclaw/issues/90083)). Multi-account Telegram config broke ([#62985](https://github.com/openclaw/openclaw/issues/62985)). Matrix channel crashed ([#90325](https://github.com/openclaw/openclaw/issues/90325)).
- **Session waste and inefficiency**: Users express frustration that every session loads full tool schemas (~3500 tokens) and all workspace bootstrap files, even when not needed ([#14785](https://github.com/openclaw/openclaw/issues/14785), [#22438](https://github.com/openclaw/openclaw/issues/22438)).
- **Message loss and broken flows**: Heartbeat interruptions in Telegram ([#64810](https://github.com/openclaw/openclaw/issues/64810)), overwritten WebChat transcripts ([#77012](https://github.com/openclaw/openclaw/issues/77012)), and session transcript corruption during backup ([#67417](https://github.com/openclaw/openclaw/issues/67417)).
- **Internal thinking exposed**: A bug causes agent’s chain-of-thought (in English) to leak to the user ([#64267](https://github.com/openclaw/openclaw/issues/64267)).
- **Approval UX broken on restart**: In-flight approvals are lost after gateway restart, leaving users confused by expired buttons ([#64664](https://github.com/openclaw/openclaw/issues/64664)).
- **Android onboarding stuck**: New users on Android cannot complete setup when offline ([#61005](https://github.com/openclaw/openclaw/issues/61005)).

**Satisfaction Signals:**
- The community is actively filing well-structured issues with reproduction steps.
- Many PRs are being proposed quickly in response to bugs (e.g., 6 fix PRs created today alone).
- The ClawSweeper automerge bot is processing smaller fixes efficiently ([#90812](https://github.com/opencl

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Date:** 2026-06-06

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a phase of **intense maturation and fragmentation**, with 13 tracked projects spanning from mature reference implementations to experimental forks. Activity is concentrated on two fronts: **reliability hardening** (regression fixes, session integrity, provider compatibility) and **architectural expansion** (multi-agent orchestration, cross-channel routing, sandboxed execution). The ecosystem is responding to user demand for production-grade stability—coding agents that complete tasks, message delivery that doesn't lose data, and security models that don't require manual config editing. Community health is strong, with several projects seeing 50+ daily issues and PRs, though a notable gap exists between the top 4–5 projects and the long tail of low-activity repositories. The reference implementation (OpenClaw) continues to anchor the ecosystem, but forks and alternatives are carving distinct niches in developer experience, enterprise features, and specialized channels.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases (24h) | Health Score | Notes |
|---------|---------------------|-------------------|----------------|--------------|-------|
| **OpenClaw** | 467 | 500 | None | **High** | Core reference; regression-heavy day |
| **Hermes Agent** | 50 | 50 | v0.16.0 (yesterday) | **High** | Major release shipped; active localization |
| **ZeroClaw** | 50 | 50 | None | **High** | RFC-driven expansion; new providers/channels |
| **NanoBot** | 11 | 28 | None | **Moderate-High** | Fast fix cycle; multi-agent features |
| **IronClaw** | 13 | 50 | None | **Moderate** | "Reborn" architecture rework ongoing |
| **PicoClaw** | 6 | 22 | Nightly build | **Moderate** | Stability focused; OneBot fixes |
| **LobsterAI** | 3 (bumped) | 13 | 2026.6.5 | **Moderate** | Cowork & keyboard shortcuts release |
| **CoPaw** | 21 | 24 | None | **Moderate** | Yuanbao channel bugs; browser fixes |
| **Moltis** | 4 | 5 | None | **Low-Moderate** | Sandbox & Telegram streaming fix |
| **NanoClaw** | 0 | 3 | None | **Low** | Maintenance; onboarding UX only |
| **NullClaw** | 0 | 1 | None | **Low** | Single provider PR; otherwise dormant |
| **TinyClaw** | — | — | — | **Inactive** | No activity |
| **ZeptoClaw** | — | — | — | **Inactive** | No activity |

**Health Score Methodology**: Composite of issue/PR volume, responsiveness to bugs, release cadence, and community engagement signals from each digest.

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Scale**: 467 issues and 500 PRs updated daily—2–10x larger than any peer. This reflects both community size and bug surface area.
- **Ecosystem Anchor**: As the core reference implementation, OpenClaw receives the broadest provider compatibility testing and the most diverse real-world usage patterns.
- **Channel Breadth**: Telegram, Matrix, WeChat, Feishu, Discord, WebChat, Twilio voice—few peers match this coverage.
- **Regression Response**: 6 fix PRs created in a single day for critical P1 bugs (session transcript integrity, Twilio stream preservation, routing guards).

### Technical Approach Differences
- **Session-centric architecture**: Focuses on transcript integrity, prompt cache stability, and tiered bootstrap loading—areas other projects handle more simply.
- **MCP tool injection** for subagents is a distinguishing feature (PR #78441, `toolsAllow` for `sessions_spawn`).
- **Memory-wiki vault** per-agent configuration (issue #63829) is unique; most peers use single-memory models.

### Community Size Comparison
| Metric | OpenClaw | Next Closest (Hermes/ZeroClaw) |
|--------|----------|--------------------------------|
| Daily issues updated | 467 | 50 |
| Daily PRs updated | 500 | 50 |
| P1 bugs with no fix PR | 5+ | 2–3 |
| Community contributors (6mo) | Not reported | 170 (Hermes) |
| Open PRs at any time | 364 | ~30–50 |

**Key insight**: OpenClaw's community is an order of magnitude larger but generates proportionally more regressions, suggesting a trade-off between rapid feature velocity and stability. Projects like PicoClaw and NanoBot, with smaller scopes, ship fixes faster.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across **multiple projects** independently, indicating ecosystem-wide priorities:

| Requirement | Projects Affected | Details |
|-------------|-------------------|---------|
| **Provider-agnostic model switching** | OpenClaw, NanoBot, NullClaw, ZeroClaw | Users want to switch between OpenAI, Anthropic, Azure, and new gateways (Evolink, MiMo) without config rewrites. Extra query parameter support (#4204 NanoBot, #7163 ZeroClaw) is a sub-need. |
| **Session efficiency / token waste reduction** | OpenClaw, LobsterAI, CoPaw | Full tool schemas loaded every session (~3500 tokens), workspace bootstrap files loaded unconditionally. Tiered loading (#22438 OpenClaw), debounce fixes (#1471 LobsterAI), and session caps (#64463 OpenClaw) all address this. |
| **Multi-agent orchestration** | OpenClaw, NanoBot, ZeroClaw | `sessions_spawn` tool forwarding (#78441 OpenClaw), cross-agent message bus (#3992 NanoBot), subagent `fail_on_tool_error` (#4198 NanoBot) indicate demand for hierarchical agent systems. |
| **Channel reliability & message integrity** | OpenClaw, NanoBot, Hermes, PicoClaw, IronClaw, Moltis | Telegram streaming contamination (#64810 OpenClaw, #1097 Moltis), Matrix dispatch crashes (#90325 OpenClaw), OneBot group routing (#3002 PicoClaw), WeCom approval loops (#4502 IronClaw)—each channel is a vector for data loss. |
| **Security granularity** | OpenClaw, ZeroClaw, PicoClaw, IronClaw | Per-execution shell confirmation (#7155 ZeroClaw), channel-mediated MCP approval (#78308 OpenClaw), `exec` tool false positives (#1042 PicoClaw), sandbox isolation (#58730 OpenClaw, #4512 IronClaw). Users want tiered security (allow/ask/block). |
| **Web UI / desktop polish** | Hermes, LobsterAI, CoPaw, ZeroClaw | Sidebar session lists, avatar support, column ordering, keyboard shortcuts, IME input for CJK—UX is a common differentiator. |
| **Cross-platform channel expansion** | ZeroClaw, IronClaw, PicoClaw | SMS (Twilio, Plivo, Sinch, Vonax), polling channels (Mastodon, Rocket.Chat, Zulip), WeCom—the "long tail" of channels is being actively filled. |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | NanoBot | PicoClaw | IronClaw |
|-----------|----------|--------------|----------|---------|----------|----------|
| **Target User** | Power users, integrators | Desktop-first consumers | Enterprise/advanced users | Developers, multi-agent | Stability-focused users | Reborn architecture adopters |
| **Primary Language** | Python (assumed) | Python | Go (implied by toolchain) | Python | Go | Rust |
| **Core Strength** | Reference implementation, channel breadth | UI/UX polish, localization | RFC-driven feature expansion | Rapid fix cycle, multi-agent | Stability, lean footprint | Event hooks, sandboxing |
| **Weakness** | Regression velocity, P1 bug backlog | WeCom channel bugs (new) | Blocked RFCs, config complexity | Smaller community, stale CI | Skill-creator UX, token drain | Nightly E2E failures, release delays |
| **Architecture** | Session-centric, MCP-native | Surface-first (desktop/UI) | Pluggable security provider | Lightweight, fast iteration | Provider-agnostic, JSONL store | Event-driven hooks, Reborn rework |
| **Channel Focus** | Broad (Telegram, Matrix, Discord, Feishu, etc.) | Matrix, WeCom (new) | SMS, polling, chat (new providers) | Weixin, Telegram | OneBot, generic channels | Slack, WeCom (staging) |
| **Release Cadence** | Rapid (multiple/week) | Major (v0.16.0 just shipped) | Milestone-based (v0.9.0 target) | Fast (nightlies) | Nightly + stable | Slower (Reborn integration) |
| **Community Contribution Model** | Large, open PR flood | 170 contributors, structured | Contributor-driven RFCs | Small but responsive | First-time contributor friendly | Maintainer-heavy |

**Key differentiation**: Hermes is winning on desktop UX and localization (v0.16.0 "Surface Release"). ZeroClaw is innovating fastest on architecture (output routing, OIDC, air-gapped mode) but carries blocked RFC risk. OpenClaw is the "safe choice" for compatibility but users pay the tax of regressions. PicoClaw and NanoBot serve the "just works" and "fast iteration" niches respectively.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity, Rapid Iteration**
- **OpenClaw**: Largest community, highest churn. Regression-heavy but responsive (6+ fix PRs/day). Maturity: established but turbulent.
- **Hermes Agent**: Just shipped a massive release (874 commits, 542 PRs). Community of 170 contributors is healthy. Maturity: feature-rich, entering stabilization phase.
- **ZeroClaw**: Explosive growth (50 issues/PRs daily), driven by RFC process and new channel expansion. Maturity: ambitious but still building foundations.

**Tier 2: Steady, Maintainer-Led**
- **NanoBot**: Consistent merge velocity (11 PRs merged in 24h). Small team but responsive. Maturity: solid for its scope.
- **IronClaw**: High PR count (50) but focused on "Reborn" rework—architectural investment rather than user-facing features. Maturity: in transition.
- **LobsterAI**: Released a stable version (2026.6.5). 13 PRs merged, no new bugs. Maturity: stable, incremental.
- **PicoClaw**: Nightly builds, 20 PRs merged, OneBot fixes. Maturity: solid for Go-based users.
- **CoPaw**: 21 issues, 15 PRs merged. Yuanbao channel bugs suggest beta-quality for that integration. Maturity: moderate, growing.

**Tier 3: Low Activity / Maintenance Mode**
- **Moltis**: Low issue/PR volume. Telegram fix merged. Maturity: stable but slow-moving.
- **NanoClaw**: Minimal activity (2 PRs merged). Onboarding fixes only. Maturity: maintenance mode.
- **NullClaw**: Single PR. Essentially dormant. Maturity: stable but unchanging.
- **TinyClaw / ZeptoClaw**: **Inactive.** May be abandoned or awaiting maintainer attention.

**Stabilizing**: Hermes (post-v0.16.0), LobsterAI, PicoClaw
**Rapidly Iterating**: OpenClaw, ZeroClaw, NanoBot
**In Transition**: IronClaw (Reborn), CoPaw (Yuanbao channel maturity)

---

## 7. Trend Signals

### Emerging Industry Trends (from Community Feedback)

1. **Provider Agnosticism is Table Stakes**  
   Users increasingly expect to swap between OpenAI, Anthropic, Azure, and new gateways (GitHub Models, Evolink, MiMo) with zero config changes. Projects that handle `extra_body`, `extra_query`, and schema-v3 providers (ZeroClaw, NanoBot) are ahead. Those hardcoding provider logic will lose users.

2. **Session Cost Efficiency is the New UX Battleground**  
   Token waste—loading full tool schemas, unconditional workspace bootstrap files, redundant memory reads—is a top complaint across OpenClaw (#22438), LobsterAI (#1471), and CoPaw (#4968). Users want tiered loading, session caps, and efficient context management. Projects that solve this (e.g., Hermes' ephemeral system prompt injection) gain loyalty.

3. **Security Must Be Granular, Not Binary**  
   The "allow all / block all" model is dead. Users demand per-execution confirmation (ZeroClaw #7155, OpenClaw #78308), sandbox isolation (IronClaw #4512, OpenClaw #58730), and proper secret redaction (Hermes #40139, ZeroClaw #7261). This is becoming a hard requirement for enterprise adoption.

4. **Channel Integration is an Endless Race**  
   Every new channel (WeCom, SMS, Zulip, Mastodon) creates a new vector for broken flows. The projects investing in channel parity (ZeroClaw with 7 new providers + 5 SMS channels; IronClaw's WeCom staging; CoPaw's Yuanbao debugging) are capturing users who need specific platforms. The "long tail" of channels is a defensible moat.

5. **Localization is a Differentiator**  
   Hermes' v0.16.0 shipped without Japanese i18n (#40219) and received immediate pushback. CJK IME input (Hermes #39647, #40146), Japanese system messages, and Portuguese UI (#40239) are requested across projects. The ecosystem is global—English-only projects are leaving users behind.

6. **From Chatbot to Autonomous Agent**  
   The most vocal users aren't asking for better chat—they want coding agents that complete tasks (#62505 OpenClaw), cron jobs that don't leak context (#39886 Hermes), and subagents that can be orchestrated (#3992 NanoBot). The "agent loop" is the new baseline; projects that break this loop (in

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-06

## 1. Today’s Overview

NanoBot is experiencing a high level of development activity: **11 issues** and **28 pull requests** were updated in the last 24 hours. Of those, 5 issues and 11 PRs were closed or merged—indicating a rapid fix-and-feature cycle. No new releases were created today. The community is actively reporting bugs (particularly around message persistence and provider compatibility) and contributing substantial features (cross-agent messaging, desktop shell polish, and WebUI improvements). The project remains in a healthy, fast-moving state with strong contributor engagement.

## 2. Releases

No new releases today. (Last known version: v0.1.4.post6, referenced in issue #2573.)

## 3. Project Progress

Three pull requests were merged/closed today (among the 11 total closed PRs):

- **PR #4210** – _Fix desktop restart token and replay gaps_ – Resolves token refresh after native engine restart and ensures WebSocket replay does not lose stream output.  
  [Link](https://github.com/HKUDS/nanobot/pull/4210)

- **PR #4197** – _Fix DM pairing for Weixin and Telegram_ – Corrects direct‑message routing for both channels when senders are denied.  
  [Link](https://github.com/HKUDS/nanobot/pull/4197)

- **PR #3968** – _feat(command): add /skill slash command to list enabled skills_ – Addresses issue #3959 by providing a built‑in command to list only enabled skills.  
  [Link](https://github.com/HKUDS/nanobot/pull/3968)

Additionally, several open PRs show significant progress on features (see §6).

## 4. Community Hot Topics

- **Issue #2573** (CLOSED, 4 comments, 9 👍) – *GitHub Copilot login failure* – Users report an “Authorization header is badly formatted” error after switching from litellm to openai. High reaction count indicates broad interest.  
  [Link](https://github.com/HKUDS/nanobot/issues/2573)

- **Issue #3959** (CLOSED, 4 comments) – *[bug] /skill list disabled skills* – User expected disabled skills to be omitted; the fix was delivered in PR #3968.  
  [Link](https://github.com/HKUDS/nanobot/issues/3959)

- **Issue #4204** (OPEN, 1 comment) – *Add extra_query support for OpenAI-compatible providers* – Discussion around Azure gateways that require `?api-version=`. The associated PR #4204 (with patch) is under review.  
  [Link](https://github.com/HKUDS/nanobot/issues/4204)

- **Issue #4203** (OPEN) – *Bug: find_legal_message_start discards all messages after orphan tool results* – Detailed bug report with root‑cause analysis. A fix PR (#4215) is already submitted.  
  [Link](https://github.com/HKUDS/nanobot/issues/4203)

- **Issue #4211** (OPEN) – *SDK leaves stdio MCP open → RuntimeError at shutdown* – Another concrete bug with a fix PR (#4216) ready.  
  [Link](https://github.com/HKUDS/nanobot/issues/4211)

## 5. Bugs & Stability

Ranked by potential impact:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **High** | #4203 | `find_legal_message_start` can drop **all** messages when an orphan tool result follows a user message. | Yes – #4215 |
| **High** | #4211 | SDK usage with stdio MCP causes `RuntimeError: Attempted to exit cancel scope in a different task` at shutdown. | Yes – #4216 |
| **High** | #4200 | User messages lost on browser refresh (regression). | No dedicated PR yet |
| **Medium** | #3959 | `/skill` command listed disabled skills. | Fixed in #3968 |
| **Medium** | #2573 | GitHub Copilot login fails with “bad request” after openai backend switch. | Closed without fix? (likely fixed elsewhere) |
| **Low** | #1946 | Matrix test error on `main` branch – stale (since March) but blocks CI pipeline. | No PR |

All high‑severity bugs have immediate fix PRs, reflecting rapid response from the maintainers.

## 6. Feature Requests & Roadmap Signals

Several user‑requested features are being actively developed or proposed:

- **Extra query support for OpenAI providers** (#4204) – Enables `?api-version=` for Azure‑style gateways. Likely to land in next minor release.
- **Subagent `fail_on_tool_error` configuration** (#4198) – Allows subagents to retry after tool errors instead of failing hard.
- **Fork‑from‑here in WebUI** (#4208) – Strict per‑chat composer isolation for message forking. High UX value.
- **Exa web search provider** (#4213) – Community‑contributed search backend.
- **Cross‑agent message bus** (#3992) – Enables multiple agent instances to communicate; major architectural addition.
- **Gateway start/stop/restart commands** (#3538) – CLI runtime management.
- **IMAP post‑actions for email channel** (#4170) – Automated mailbox processing.
- **Custom image generation providers** (#4132, #4196) – Support for third‑party image APIs (e.g., Agnes AI, Volcengine Seedream).
- **Mailbox‑backed subagent results** (#4205) – In‑memory mailbox protocol for cleaner subagent task handling.

**Prediction for next version (v0.2.0 or v0.1.5):** The `extra_query` provider patch, subagent configuration, and `fork-from-here` WebUI feature are small enough to be included soon. Cross‑agent messaging (#3992) may require more testing before a stable release.

## 7. User Feedback Summary

- **Pain points:**  
  - Several users report authentication/authorization failures with the new OpenAI backend (#2573).  
  - Message loss after browser refresh (#4200) and improper session trimming (#4203) are causing frustration for WebUI users.  
  - Lack of custom image generation provider support (#4132, #4196) limits use cases for Chinese users and alternative APIs.

- **Satisfaction signals:**  
  - Community members are actively contributing PRs (e.g., Exa provider, DingTalk allowlist, desktop surfacing).  
  - The quick turnaround on bugs (PRs for #4203 and #4211 filed same day as report) suggests responsive maintenance.

- **Use cases highlighted:**  
  - Enterprise gateways (Azure‑style) needing query parameters.  
  - Multi‑agent orchestration (cross‑agent bus).  
  - Desktop‑first users wanting self‑contained shell and notifications.

## 8. Backlog Watch

The following issues and PRs have remained open without maintainer comment for an extended period (≥ 2 months) and may need attention:

- **Issue #1946** (OPEN since 2026-03-13) – *Matrix test error on main*. Only 1 comment. Blocks CI for Matrix channel.  
  [Link](https://github.com/HKUDS/nanobot/issues/1946)

- **PR #1408** (OPEN since 2026-03-02) – *feat(CI): add unit-test workflow with coverage gate*. Author has kept it updated, but no maintainer review.  
  [Link](https://github.com/HKUDS/nanobot/pull/1408)

- **PR #1284** (OPEN since 2026-02-27) – *Add CI workflow with quality checks*. Both this and #1408 overlap in purpose; maintainers should decide which direction to take.  
  [Link](https://github.com/HKUDS/nanobot/pull/1284)

- **PR #3538** (OPEN since 2026-04-29) – *feat: add gateway start/stop/restart commands*. No recent maintainer activity despite being labelled.  
  [Link](https://github.com/HKUDS/nanobot/pull/3538)

These items, if stale, risk accumulating technical debt or discouraging first‑time contributors.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-06

## Today’s Overview
Hermes Agent saw high activity on June 6, 2026, with 50 issues and 50 PRs updated in the last 24 hours. A major milestone release **v0.16.0 (The Surface Release)** shipped yesterday, containing 874 commits and 542 merged PRs since v0.15.2. Community engagement is strong, with 22 PRs merged or closed today and 2 issues closed. The project continues to attract contributions from 170 community contributors (including co-authors) over the release cycle. Key themes today include localisation (i18n), IME input handling for CJK users, platform adapter reliability, and security hardening.

---

## Releases
### **v0.16.0 (v2026.6.5) — *The Surface Release***
- **Size:** 874 commits · 542 merged PRs · 1,962 files changed · 205,216 insertions · 46,217 deletions · 399 issues closed (2 P0, 62 P1, 16 security-tagged)
- **Focus:** UI/UX overhaul, desktop app improvements, and surface-level interactions (per release title). Specific breaking changes or migration notes were not included in the release summary; maintainers should review the full changelog for deprecations.
- **No additional releases today.**

---

## Project Progress
22 PRs were merged or closed in the last 24 hours. Notable contributions include:

| PR | Component | Summary |
|----|-----------|---------|
| [#32297](https://github.com/NousResearch/hermes-agent/pull/32297) (merged) | tools/vision | Fixed non-retryable 4xx image downloads wasting retries |
| [#39647](https://github.com/NousResearch/hermes-agent/pull/39647) (merged) | desktop | Improved IME reliability on `compositionend` for Vietnamese/East Asian input |
| [#39427](https://github.com/NousResearch/hermes-agent/pull/39427) (merged) | desktop | Preserve previous unpacked directory on failed pack (Electron builder) |
| [#38828](https://github.com/NousResearch/hermes-agent/pull/38828) (merged) | matrix | Propagate room name to session source via `get_chat_info()` |
| [#38619](https://github.com/NousResearch/hermes-agent/pull/38619) (merged) | cli | Bump version to 0.15.2 to match release tag |
| [#38444](https://github.com/NousResearch/hermes-agent/pull/38444) (merged) | memory (mem0) | Include agent-attributed memories in read filter |
| [#38237](https://github.com/NousResearch/hermes-agent/pull/38237) (merged) | cli | Warn when `claw migrate` source is a remote-mode OpenClaw client |
| [#37765](https://github.com/NousResearch/hermes-agent/pull/37765) (merged) | config | Prevent desktop/gateway config dual-write conflict on model switch |
| [#37380](https://github.com/NousResearch/hermes-agent/pull/37380) (merged) | wecom | Route WeCom MEDIA through live gateway adapter |
| [#37067](https://github.com/NousResearch/hermes-agent/pull/37067) (merged) | gateway/api | Expose reasoning/thinking blocks in `/v1/chat/completions` |

Open PRs advancing new features today:
- [#40254](https://github.com/NousResearch/hermes-agent/pull/40254) – Profile builder web flow
- [#40248](https://github.com/NousResearch/hermes-agent/pull/40248) – Hermex MVP proxy (Anthropic-compatible universal LLM proxy)
- [#40252](https://github.com/NousResearch/hermes-agent/pull/40252) – Inject wall-clock time via ephemeral_system_prompt

---

## Community Hot Topics

### Most Discussed Issues
| Issue | Comments | Summary |
|-------|----------|---------|
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | 5 | macOS DMG is arm64-only, fails on Intel Macs |
| [#40219](https://github.com/NousResearch/hermes-agent/issues/40219) | 4 | Request for Japanese i18n support |
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | 4 | QQ Bot adapter enters silent loop after reconnect failure |
| [#40146](https://github.com/NousResearch/hermes-agent/issues/40146) | 3 | Desktop: Send button doesn't switch from voice during IME composition |

### User Appreciation
[#40251](https://github.com/NousResearch/hermes-agent/issues/40251) — A Chinese user published a heartfelt thank-you letter praising Hermes’ **skill + memory + session_search** system for enabling a true learning loop. This reflects deep satisfaction with the architecture and suggests strong product-market fit for power users doing iterative development.

### Analysis
The community is vocal about **localisation gaps** (Japanese, Portuguese, and improved CJK IME support) and **platform adapter reliability** (QQ Bot, Feishu). The dual themes of surface UI polish and robust backend connectivity dominate today’s discussions.

---

## Bugs & Stability

### Critical (P1)
- **#39886** [cron scheduler](https://github.com/NousResearch/hermes-agent/issues/39886): Profile-job context bleeds into concurrent non-profile job, causing “script not found” errors. No fix PR yet.
- **#40201** [agent](https://github.com/NousResearch/hermes-agent/issues/40201): Post-compression synthesis can fabricate source-backed findings without re-grounding. *High severity for code review use cases.*

### High (P2)
- **#31101** [QQ Bot](https://github.com/NousResearch/hermes-agent/issues/31101): Silent loop after reconnect failure (no retry). No fix PR.
- **#38412** [desktop/gateway](https://github.com/NousResearch/hermes-agent/issues/38412): Remote WebSocket connection always rejected (4403). No fix PR.
- **#38488** [MCP server](https://github.com/NousResearch/hermes-agent/issues/38488): Transient backend outage permanently kills MCP server; requires gateway restart.
- **#40139** [secret redaction](https://github.com/NousResearch/hermes-agent/issues/40139): Redaction modifies actual command execution and output instead of masking display.
- **#40145** [desktop](https://github.com/NousResearch/hermes-agent/issues/40145): Desktop input truncation on Chinese text.
- **#40176** [dependencies](https://github.com/NousResearch/hermes-agent/issues/40176): Pinned Python deps carry known CVEs (urllib3, python-multipart). No fix PR.
- **#40225** [Feishu](https://github.com/NousResearch/hermes-agent/issues/40225): Approval buttons reject all users in DM due to wrong authorization check.
- **#38963** [desktop](https://github.com/NousResearch/hermes-agent/issues/38963): Desktop fails to start with "no git???" error on Windows. No fix PR.

### Medium (P3)
- Multiple IME-related input bugs ([#40146](https://github.com/NousResearch/hermes-agent/issues/40146), [#40226](https://github.com/NousResearch/hermes-agent/issues/40226), [#39614](https://github.com/NousResearch/hermes-agent/issues/39614) closed) – fix PR [#39647](https://github.com/NousResearch/hermes-agent/pull/39647) merged today.
- **#40250** [terminal](https://github.com/NousResearch/hermes-agent/issues/40250): Escape sequences leaking into output, cutting first characters.
- **#40101** [memory plugin](https://github.com/NousResearch/hermes-agent/issues/40101): mnemosyne-hermes plugin not discovered despite correct entry points.
- **#40215** [desktop](https://github.com/NousResearch/hermes-agent/issues/40215): Remote gateway config error `ERR_INVALID_ARGUMENT`.

### Regressions
- [#37918](https://github.com/NousResearch/hermes-agent/issues/37918) (P3, June 3): Sticky human-message clamp obscures long machine-generated first messages (introduced in v0.15.1).
- [#40129](https://github.com/NousResearch/hermes-agent/issues/40129) (P2, closed June 5): CLI resume crash due to Rich markup interpolation – was fixed and closed today.

---

## Feature Requests & Roadmap Signals

### Top community-requested features
| Issue | Feature | Potential Next Version |
|-------|---------|------------------------|
| [#40219](https://github.com/NousResearch/hermes-agent/issues/40219) | Japanese i18n (UI + system messages) | v0.16.x or v0.17 |
| [#40239](https://github.com/NousResearch/hermes-agent/issues/40239) | Portuguese (pt-BR) i18n | v0.16.x |
| [#39425](https://github.com/NousResearch/hermes-agent/issues/39425) | `/approvals` slash command for approval mode toggle | Likely v0.16.1 |
| [#35573](https://github.com/NousResearch/hermes-agent/issues/35573) | ToolCallStormBreaker – suppress repeated tool-call loops | Under RFC, could land in v0.17 |
| [#40199](https://github.com/NousResearch/hermes-agent/issues/40199) | Gateway status expose platform health + recover stale adapters | Post-v0.16 |
| [#40232](https://github.com/NousResearch/hermes-agent/issues/40232) | Schema sanitizer for invalid property keys (strict backends) | v0.16.1 |

### Signal from roadmap
The “Surface Release” label on v0.16.0 suggests a focus on **frontend and integration polish**. Likely next priorities: multi-language support, MCP resilience, and improved platform adapter observability.

---

## User Feedback Summary

### Pain Points
- **Intel Mac incompatibility** (#37505, #38227): Official DMG is arm64-only; Intel Mac users are blocked. Workaround needed.
- **CJK IME input friction** (#40146, #40226, #39614): Poor experience with Chinese/Japanese input – send button not appearing, text truncation, enter not sending. Fixes merged today for desktop IME should help but issues remain.
- **Remote gateway instability** (#38412, #40215): WebSocket connection failures and config errors when using remote gateway mode.
- **Secret redaction breaking commands** (#40139): Feature intended for security is altering actual execution.
- **Cron scheduler unreliability** (#39886): Context leak from profile to non-profile jobs.
- **MCP server fragility** (#38488): Transient outages permanently kill connections.

### Satisfaction Signals
- [#40251](https://github.com/NousResearch/hermes-agent/issues/40251): User calls Hermes “the most ingenious AI agent design” and highlights **skill + memory + session_search** as a true learning loop. This indicates strong adoption by technical users doing iterative work.
- Community response to i18n requests (upvotes on #40239, #39425) shows engaged user base wanting broader language support.

---

## Backlog Watch

### Long-open items needing maintainer attention
| Issue | Opened | Severity | Reason for Attention |
|-------|--------|----------|----------------------|
| [#9553](https://github.com/NousResearch/hermes-agent/issues/9553) | 2026-04-14 | P3 (docs) | Documentation error: missing `reward_functions_library.py` in GRPO training example. Low priority but stale. |
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | 2026-05-23 | P2 (QQ Bot) | Critical for Chinese market: silent loop prevents reconnection. No maintainer response beyond initial triage. |
| [#35573](https://github.com/NousResearch/hermes-agent/issues/35573) | 2026-05-30 | P3 (RFC) | ToolCallStormBreaker RFC – no recent discussion despite clear community interest. |
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | 2026-06-02 | P3 (Intel Mac) | Top comment count today; Intel Mac users actively blocked. |

### Stale PRs
- [#34215](https://github.com/NousResearch/hermes-agent/pull/34215) (opened 2026-05-29, still open): Memory recall context boundaries fix – waiting for review since last week.

---

*Digest generated from GitHub data as of 2026-06-06.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-06

## 1. Today's Overview
PicoClaw saw **very high activity** over the past 24 hours: 22 pull requests were updated (20 merged/closed, 2 open) and 6 issues were updated (4 closed, 2 open). A **nightly build v0.2.9-nightly.20260606** was published, which is an automated release and may be unstable. The merged PRs include critical stability fixes (OneBot group reply routing, type assertion panics, JSONL metadata drift, fallback chain handling), security hardening (CSRF, path traversal), and a new feature adding MiMo vision-capable models. Two new bugs surfaced: a continuous token consumption issue with Evolution mode (high severity) and a remaining unaddressed skill-creator documentation gap. Overall, the project is undergoing rapid, healthy iteration with strong community contribution.

## 2. Releases
- **nightly (v0.2.9-nightly.20260606.89ee8f1b)** — Automated nightly build, potentially unstable. Full changelog from v0.2.9 to main: [https://github.com/sipeed/picoclaw/compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main).  
  No explicit breaking changes or migration notes were provided. Users are advised to test before deploying to production.

## 3. Project Progress
**20 PRs were merged/closed** in the last 24 hours. Notable advances:

- **OneBot group reply fix** ([#3009](https://github.com/sipeed/picoclaw/pull/3009)) — Corrected the `ChatID` prefix to use `group:` when routing group replies, resolving the `send_private_msg` vs `send_group_msg` mix-up.
- **Type assertion safety** ([#3010](https://github.com/sipeed/picoclaw/pull/3010) & [#3011](https://github.com/sipeed/picoclaw/pull/3011)) — Added `ok` checks in `toChannelHashes` and `UnsubscribeEvents` to prevent panics on unexpected config/value types.
- **Context command disambiguation** ([#2985](https://github.com/sipeed/picoclaw/pull/2985)) — `/context` now displays both the soft summarization threshold and the hard compression threshold, fixing confusion reported in issue #2968.
- **JSONL store crash-consistency** ([#2907](https://github.com/sipeed/picoclaw/pull/2907)) — Fixed metadata drift when a crash occurs between appending to the `.jsonl` file and updating the `.meta.json`.
- **Fallback chain improvements** ([#2905](https://github.com/sipeed/picoclaw/pull/2905)) — Expired request contexts now stop the chain immediately instead of pointlessly trying later candidates.
- **Security hardening** ([#2900](https://github.com/sipeed/picoclaw/pull/2900)) — Added CSRF protection, path traversal validation in skill deletion, and security headers to the web backend.
- **MiMo provider models** ([#2915](https://github.com/sipeed/picoclaw/pull/2915)) — Added `mimo-v2.5` (multimodal, vision-capable) and `mimo-v2.5-pro` (text-only) to the provider’s common models.
- **Documentation fix** ([#3013](https://github.com/sipeed/picoclaw/pull/3013)) — Removed references to missing helper scripts in `skill-creator/SKILL.md`.
- **Dependency updates** — Multiple dependabot PRs bumped React TanStack Router, shadcn, react-query, Tabler icons, go.mau.fi/util, and the anthropic-sdk-go library (from 1.26.0 to 1.46.0).

- **Still open PRs**:  
  - [#2551](https://github.com/sipeed/picoclaw/pull/2551) — Refactor to standardize channel identification (open since April, dormant).  
  - [#2964](https://github.com/sipeed/picoclaw/pull/2964) — Adds configurable inbound image compression for the vision pipeline.

## 4. Community Hot Topics

| Item | Type | Title | Comments | Reactions | Status |
|------|------|-------|----------|-----------|--------|
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | Issue | `exec` tool `guardCommand` false positive on non‑path arguments | 15 | 👍 2 | Closed (stale) |
| [#2968](https://github.com/sipeed/picoclaw/issues/2968) | Issue | `/context` always shows “Compress at: 76800 tokens” | 5 | 👍 1 | Closed (fixed by #2985) |
| [#2916](https://github.com/sipeed/picoclaw/issues/2916) | Issue | CPU, Memory and IO optimizations | 4 | – | Closed |
| [#652](https://github.com/sipeed/picoclaw/issues/652) | Issue | skill-creator missing scripts, unable to run | 3 | – | Open (since Feb) |
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) | Issue | Continuous token consumption every minute with Evolution enabled | 1 | – | Open |
| [#3002](https://github.com/sipeed/picoclaw/issues/3002) | Issue | OneBot group reply used `send_private_msg` | 0 | – | Closed (fixed by #3009) |

**Underlying needs**:  
- **#1042** highlights a common pain point where overly aggressive workspace path validation blocks legitimate commands (e.g., `curl` with a URL). The issue was closed as stale, so the underlying guard logic may still be problematic.  
- **#2968** reflects user confusion around context budget thresholds — now addressed by dual-threshold display.  
- **#3012** (new) reveals a critical cost/resource concern for users of Evolution mode — the system appears to consume tokens constantly even when idle.

## 5. Bugs & Stability
Ranked by severity:

1. **High — Continuous token drain with Evolution enabled** ([#3012](https://github.com/sipeed/picoclaw/issues/3012))  
   *Users report tokens are consumed every minute when Evolution is on (Draft mode, Code Path Trigger).*  
   *Status:* Open, no fix PR yet. Impact: increased API costs, possible infinite loops.

2. **Medium — OneBot group reply misrouted** ([#3002](https://github.com/sipeed/picoclaw/issues/3002))  
   *Group replies used `send_private_msg` with the group number as `user_id`, causing “无法获取用户信息” errors.*  
   *Status:* Closed, fixed by [#3009](https://github.com/sipeed/picoclaw/pull/3009).

3. **Low — `/context` display ambiguity** ([#2968](https://github.com/sipeed/picoclaw/issues/2968))  
   *Only the compression threshold was shown, confusing users about summarization triggers.*  
   *Status:* Closed, fixed by [#2985](https://github.com/sipeed/picoclaw/pull/2985).

4. **Unresolved — `exec` tool false positive** ([#1042](https://github.com/sipeed/picoclaw/issues/1042))  
   *Commands like `curl -s "wttr.in/Beijing?T"` are incorrectly blocked by `guardCommand`.*  
   *Status:* Closed as stale, but no PR was found that addresses the regex logic. The bug likely persists.

5. **Potential panic — type assertion panics** (addressed by [#3010](https://github.com/sipeed/picoclaw/pull/3010) & [#3011](https://github.com/sipeed/picoclaw/pull/3011))  
   *Unsafe type assertions in channel config and event subscription could cause panics.*  
   *Status:* Closed, fixed.

## 6. Feature Requests & Roadmap Signals
- **Image compression pipeline** (PR [#2964](https://github.com/sipeed/picoclaw/pull/2964)) — Configurable multi-level compression before model payload construction. Likely to land in the next stable release, reducing bandwidth and processing costs for vision tasks.
- **Channel identification refactor** (PR [#2551](https://github.com/sipeed/picoclaw/pull/2551)) — Decouples channel names from provider types, enabling multiple instances of the same provider. This has been open for two months; it addresses a key architectural limitation.
- **User-requested optimizations** (issue [#2916](https://github.com/sipeed/picoclaw/issues/2916)) — Closed after a comprehensive proposal but the community interest in CPU/memory/IO improvements remains; may be absorbed into smaller PRs.
- **Skill‑creator usability** (issue [#652](https://github.com/sipeed/picoclaw/issues/652)) — The missing `init_skill.py` script and broken `SKILL.md` references are a barrier for new skill developers. PR [#3013](https://github.com/sipeed/picoclaw/pull/3013) partially addresses the documentation, but the core script issue remains.

**Predictions for v0.3.0**: Image compression, channel standardisation, and improved Evolution mode efficiency are strong candidates.

## 7. User Feedback Summary
- **Pain points**:
  - The `exec` tool’s path validation is too strict, blocking harmless commands (weather queries).
  - Evolution mode’s token consumption is unexpectedly high and continuous.
  - OneBot group chat integration was broken (now fixed).
  - New users are unable to run `skill-creator` out of the box due to missing scripts.
- **Satisfaction signals**:
  - Quick turnaround on reported bugs (e.g., OneBot fix within 24 hours of issue creation).
  - Active dependency maintenance (multiple dependabot merges).
  - Community contributions (SiYue-ZO, chengzhichao-xydt, yangwenjie1231) closing important gaps.
- **Dissatisfaction**:
  - Stale issues like #1042 and #652 remain unresolved for months.
  - Nightly builds lack stability guarantees, though users are warned.

## 8. Backlog Watch
Items requiring maintainer attention due to long inactivity or unresolved impact:

- **[#652](https://github.com/sipeed/picoclaw/issues/652)** (open since Feb 22, 2026) — skill-creator setup broken. Despite a docs fix today, the underlying missing scripts have not been provided. Stop-gap: approve PR [#3013](https://github.com/sipeed/picoclaw/pull/3013) and consider adding the missing `init_skill.py`.
- **[#2551](https://github.com/sipeed/picoclaw/pull/2551)** (open since April 16, 2026) — channel refactor PR. Stalled for 7 weeks; may need rebase or maintainer feedback.
- **[#1042](https://github.com/sipeed/picoclaw/issues/1042)** (closed as stale, but bug likely persists) — The `exec` tool false‑positive issue was never resolved by a code change. Consider re‑opening or applying a targeted fix.
- **[#3012](https://github.com/sipeed/picoclaw/issues/3012)** (new, high-severity) — Evolution token drain. Immediate investigation required; currently no fix in progress.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-06

## Today’s Overview
The NanoClaw repository saw **low activity** over the past 24 hours: **zero new issues** were created or updated, and **no releases** were published. Three pull requests were updated, two of which were merged/closed and one remains open. The closed PRs focus on improving developer experience around Hugging Face token setup and OneCLI onboarding, while the open PR addresses resilience against transient API errors from the Claude Agent SDK. Overall, the project is in a maintenance-driven phase with incremental stability improvements.

## Releases
No new releases were published in the last 24 hours. There are no release notes to report.

## Project Progress
Two pull requests were merged (closed) today, both authored by **gavrielc**:

- **#2690** – [fix: simplify HF token setup + correct secret-mode docs](https://github.com/nanocoai/nanoclaw/pull/2690)  
  *Corrected the default secret mode for auto-created agents to `all` (previously incorrectly documented as `selective`). Removed an unnecessary per-agent assignment step in `upload-trace.ts`.*

- **#2691** – [feat: show OneCLI’s own setup URL when HF token is missing](https://github.com/nanocoai/nanoclaw/pull/2691)  
  *Improved the “not signed in” error message by dynamically extracting the correct OneCLI dashboard URL from the gateway’s error response, instead of hardcoding local/hosted URLs.*

A third PR remains open:

- **#2692** (open) – [fix(poll-loop): retry transient 5xx API-error results, notify on exhaustion](https://github.com/nanocoai/nanoclaw/pull/2692)  
  *Handles terminal error results from the Claude Agent SDK (e.g., `529 Overloaded`) by retrying transient failures and notifying on exhaustion.*

## Community Hot Topics
No issues or pull requests attracted comments or reactions in the last 24 hours. The only open PR (#2692) has not yet sparked discussion. Activity remains limited to maintainer-driven changes.

## Bugs & Stability
One bug-fix PR was opened today:

- **#2692** (open) – Addresses a reliability gap: when the Claude Agent SDK exhausts internal retries on a transient 5xx error, the result is reported as a terminal error message rather than an exception. This fix introduces a retry loop with exhaustion notification.  
  *Severity: Medium* — affects long-running poll loops and could lead to silent failures under load.

No crash reports, regressions, or other bugs were filed.

## Feature Requests & Roadmap Signals
The merged PR **#2691** effectively solves a user-facing pain point: confusing setup instructions when a Hugging Face token is missing. This suggests that onboarding friction is an area the maintainers are actively smoothing. No explicit feature requests were submitted today, but the changes in #2691 indicate a roadmap focus on **better error messaging and self-diagnosis** for new users.

## User Feedback Summary
No direct user feedback (comments, issues, or reactions) was recorded in the last 24 hours. The merged PRs (#2690, #2691) address documentation and usability gaps that likely stem from prior user confusion, but no new pain points were voiced today.

## Backlog Watch
No issues or pull requests have been left unattended for an extended period. The open PR #2692 was created on 2026-06-05 and is already pending review. No stale items warrant maintainer attention at this time.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-06

## 1. Today's Overview
Activity on the NullClaw repository remains subdued, with no new issues or releases in the past 24 hours. A single open pull request (#947) proposes adding Evolink as an OpenAI‑compatible provider, reflecting continued interest in expanding model gateway integrations. No issues were updated, indicating a lower community engagement day. The project appears stable with no active bug reports or regression chatter.

## 2. Releases
No new releases were created in the last 24 hours. The latest available release remains unchanged. (No migration notes or breaking changes to report.)

## 3. Project Progress
No pull requests were merged or closed today. The only activity is the newly opened PR #947 (see below), which has not yet been merged.

## 4. Community Hot Topics
The sole active discussion item is:

- **[PR #947 – feat(providers): add Evolink as an OpenAI-compatible provider](https://github.com/nullclaw/nullclaw/pull/947)**  
  *Author: EvoLinkAI | Created/Updated: 2026-06-05 | Comments: 0 | 👍: 0*  

  **Analysis:** This PR adds support for Evolink, a multi-model gateway that exposes models like GPT-5, Gemini, DeepSeek, Doubao, and MiniMax behind a single OpenAI-compatible API. The lack of comments or reactions suggests early-stage review. The underlying need is to give NullClaw users access to a broader set of models through a single authentication pattern (Bearer token), simplifying configuration for multi-provider workflows.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project remains stable with no stability alerts.

## 6. Feature Requests & Roadmap Signals
The only feature signal is the Evolink provider integration (PR #947). Given its clean OpenAI‑compatible interface and the growing demand for multi-model gateways, this PR likely aligns with NullClaw’s roadmap to support flexible provider backends. If reviewed positively, it could be merged in the next release.

No additional user-requested features were observed today.

## 7. User Feedback Summary
No explicit user feedback (comments, issues, or discussions) was recorded today. Indirectly, the submission of PR #947 by an external contributor (EvoLinkAI) indicates a use case where developers want to use NullClaw with a broader set of models without changing their client code. This suggests satisfaction with NullClaw’s provider abstraction layer and a desire for more pre-built adapters.

## 8. Backlog Watch
No long-unanswered issues or pull requests were identified. The repository currently has zero open issues and one open PR, so there is no backlog requiring maintainer attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-06

## 1. Today's Overview

The project is in a high-activity phase with **50 pull requests and 13 issues updated in the last 24 hours**, of which **22 PRs were merged or closed** and **3 issues resolved**. Development remains concentrated on the “Reborn” architecture rework—particularly the hook framework activation, ProductWorkflow refactoring, and Slack/WeCom channel hardening. The number of open PRs (28) indicates sustained forward momentum, while the nightly E2E pipeline continues to fail, requiring immediate attention. No new releases were cut today.

---

## 2. Releases

None.

---

## 3. Project Progress

**Notable Merged/Closed PRs (today):**

- **Hook framework production activation** – Multiple PRs by @zmanian landed to bring the event-driven hook system live (behind a default‑OFF flag). Key PRs:  
  - [#3951](https://github.com/nearai/ironclaw/pull/3951) – Third-party extension hook activation via hook-only projection  
  - [#3938](https://github.com/nearai/ironclaw/pull/3938) – Activate hook framework in production behind `HOOKS_ENABLED`  
  - [#3937](https://github.com/nearai/ironclaw/pull/3937) – Cross-backend adversarial parity suite  
  - [#3936](https://github.com/nearai/ironclaw/pull/3936) – `LibSqlPredicateStateBackend` in own crate  
  - [#3933](https://github.com/nearai/ironclaw/pull/3933) – `PostgresPredicateStateBackend`  
  - [#3931](https://github.com/nearai/ironclaw/pull/3931) – Fix cross-tenant leakage, replay, and provider spoofing in event-triggered hooks  
- **Skill system refactor** – [#2904](https://github.com/nearai/ironclaw/pull/2904) (closed) replaced 11 WASM API-proxy tools with skill‑based HTTP declarations, reducing complexity.  
- **Documentation and testing** – [#2550](https://github.com/nearai/ironclaw/pull/2550) added contributing guide for skills; [#3928](https://github.com/nearai/ironclaw/pull/3928) hardened `arguments_digest` snapshot tests.  
- **Security** – [#3922](https://github.com/nearai/ironclaw/pull/3922) wired `SecurityAuditSink` into obligation handler and hook deny paths.  

**New/Open PRs advancing significant features:**

- [#4506](https://github.com/nearai/ironclaw/pull/4506) – Split `ProductWorkflow` into submit/read/subscribe doors (Reborn)  
- [#4511](https://github.com/nearai/ironclaw/pull/4511) – Outbound preference facade contracts (Reborn)  
- [#4510](https://github.com/nearai/ironclaw/pull/4510) – Add Slack channel route admin wiring  
- [#4479](https://github.com/nearai/ironclaw/pull/4479) – Port IronHub install flow to Reborn  
- [#4463](https://github.com/nearai/ironclaw/pull/4463) – Wire Slack host‑beta durable stores  

---

## 4. Community Hot Topics

- **[Issue #4311](https://github.com/nearai/ironclaw/issues/4311)** – “Reborn model gateway collapses budget governance failures into context-overflow recovery”  
  *2 comments, open since Jun 1*  
  A design concern: non‑context budget governance errors are misclassified as `ContextOverflow`, potentially breaking recovery logic. This is a subtle architectural issue and has attracted maintainer discussion.

- **[Issue #4488](https://github.com/nearai/ironclaw/issues/4488)** – “[Reborn] Split ProductWorkflow into explicit submit/read/subscribe doors”  
  *2 comments, opened Jun 5*  
  A foundational refactoring issue that blocks future OpenAI‑compatible API wiring. The linked PR [#4506](https://github.com/nearai/ironclaw/pull/4506) is already open, indicating strong consensus on the roadmap.

- **[Issue #4502](https://github.com/nearai/ironclaw/issues/4502)** – “WeCom group chat approval reply does not work”  
  *1 comment, opened Jun 5*  
  A functional bug that directly blocks WeCom users from approving tool requests. The community reporter (`sunglow666`) has been filing detailed validation issues, reflecting active real‑world testing.

- **[Issue #4191](https://github.com/nearai/ironclaw/issues/4191)** – “WeCom Channel Validation Findings”  
  *0 comments but high signal* – A comprehensive list of issues from staging validation, many of which have spawned sub‑issues (e.g., #4502, #4505, #4500). This is the central tracking issue for WeCom stability.

---

## 5. Bugs & Stability

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#4502](https://github.com/nearai/ironclaw/issues/4502) | **High** | WeCom group chat approval replies (`y`/`yes`/`always`) are ignored; bot loops asking for approval. | No PR yet |
| [#4512](https://github.com/nearai/ironclaw/issues/4512) | **High** | Concurrent sandbox `job_semaphore` is declared but never `.acquire()`’d, potentially allowing unbounded concurrent jobs. | No PR yet |
| [#4500](https://github.com/nearai/ironclaw/issues/4500) | **Medium** | Channel onboarding system event written to the wrong (existing) conversation instead of the new one. Reproduced on WeCom and Telegram. | No PR yet |
| [#4505](https://github.com/nearai/ironclaw/issues/4505) | **Low** | WeCom group conversation titles are not distinguishable in Web UI sidebar. | Enhancement request |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | **Critical** | Nightly E2E scheduled run has been failing since May 27 (last update Jun 5). No fix commit identified. | Unknown |

Three WeCom‑related bugs (#4502, #4500, #4505) plus the semaphore issue (#4512) are filed by the same reporter (`sunglow666`) and represent real integration pain points. The nightly E2E failure is a red flag for CI health.

---

## 6. Feature Requests & Roadmap Signals

- **Slack enhancements** – [#4491](https://github.com/nearai/ironclaw/issues/4491) requests Slack AI streaming feedback (“Ironclaw is thinking…”), and [#4510](https://github.com/nearai/ironclaw/pull/4510) adds channel route admin. These indicate Slack is a priority channel for near‑term improvements.

- **ProductWorkflow split** – [#4488](https://github.com/nearai/ironclaw/issues/4488) and its PR [#4506](https://github.com/nearai/ironclaw/pull/4506) are critical for the Reborn OpenAI‑compatible API wiring (blocked by #3280). Likely to land in the next release.

- **IronHub integration** – [#4479](https://github.com/nearai/ironclaw/pull/4479) ports IronHub install flow to Reborn, enabling third‑party skill discovery—a clear step toward an extension ecosystem.

- **Outbound preferences** – [#4511](https://github.com/nearai/ironclaw/pull/4511) adds outbound delivery preference contracts, preparing for richer message routing.

- **WeCom UI polish** – [#4505](https://github.com/nearai/ironclaw/issues/4505) asks for better group conversation titles; a small UX improvement that may ship in a patch.

**Prediction for next version (v0.30.x):**  
- Reborn `ProductWorkflow` split  
- Slack streaming feedback  
- IronHub install flow in Reborn  
- Fixes for WeCom approval and onboarding bugs  
- Outbound preference facade contracts (early phase)

---

## 7. User Feedback Summary

The most vocal feedback comes from the WeCom staging validation by `sunglow666`. Overall impression:

- **Core messaging is stable** – Text, pairing, markdown, emoji, and multilingual support work as expected.
- **Tool approval flow is broken** – The bot cannot confirm approvals in group chat, making tool use impractical in that context.
- **Conversation confusion** – Onboarding events land in wrong threads; group vs. DM separation was recently fixed but titles remain ambiguous.
- **Owner visibility** – Unpaired users’ messages are invisible to the owner, which caused uncertainty but was closed as intended behavior (#4198).
- **Slack parity** – No direct user complaints, but the team is actively building missing features (durable stores, channel admin, streaming feedback).

The project appears to be in a “staging validation & polish” phase for WeCom, while the core Reborn architecture advances quickly.

---

## 8. Backlog Watch

| Item | Since | Last Activity | Concern |
|------|-------|---------------|---------|
| [#4108](https://github.com/nearai/ironclaw/issues/4108) – Nightly E2E failure | May 27 | Jun 5 (auto‑update) | No maintainer response; CI red for 10 days. |
| [#3708](https://github.com/nearai/ironclaw/pull/3708) – Release PR (v0.29.1) | May 16 | Jun 6 (updated) | Open for 21 days; breaking changes in two crates. May be blocked on Reborn integration readiness. |
| [#4002](https://github.com/nearai/ironclaw/pull/4002) – Bump actions group (16 deps) | May 24 | Jun 6 (updated) | Large dependency update with potential breaking changes; no review yet. |
| [#4390](https://github.com/nearai/ironclaw/pull/4390) – Wire runtime profiles into approval gates | Jun 3 | Jun 5 | Open but no PR comments; may need reviewer bandwidth. |

The stale release PR (#3708) and the unaddressed nightly E2E failure (#4108) are the highest‑priority items requiring maintainer action.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-06

## 1. Today's Overview
Project activity remains steady, with 13 pull requests merged and 1 new release (2026.6.5) in the last 24 hours. No new issues were opened today, but three existing stale issues (all open since early April) saw updates, suggesting ongoing community engagement. The release focuses on cowork session sync, keyboard shortcuts overhaul, and voice input improvements. Development velocity is high, with maintainers actively closing PRs across multiple areas—cowork, artifacts, security, and platform support.

## 2. Releases
**LobsterAI 2026.6.5** (released 2026-06-05)

**What’s Changed:**
- `feat(cowork): improve channel session sync and cleanup` by @fisherdaddy (PR #2108)
- `feat(shortcuts): overhaul keyboard shortcuts with expanded actions and improved UX` by @fisherdaddy (PR #2109)

**Breaking Changes:** None noted.
**Migration Notes:** No special migration steps required; the release is a standard feature update.

## 3. Project Progress
All 13 PRs updated in the last 24 hours were closed/merged. Key advances:

- **Cowork & UX (#2118, #2116, #2115):** Improved clipboard copy with fallback chain; added empty-state guides and better error classification for free-quota exhaustion; fixed IM reply assembly to only use current-turn messages.
- **Voice Input (#2113):** Added macOS microphone permission request and ASR diagnostics for uploaded audio.
- **Artifacts (#2114):** Enhanced file preview with Office zoom, preview/source toggle menus, Word pagination, PPT centering, PDF/Office scaling, Excel column adjustment, and HTML file browser preview.
- **Security & Configuration (#2117, #1534, #1535):** Preserved user-deleted provider models after migration; prevented API proxy log from leaking credentials; added key whitelist for renderer process kv store IPC.
- **Subscription & Model Selector (#2112):** Locked plan models now show login/subscribe prompt instead of being silently disabled; added OpenClaw repair flow.
- **Settings UI (#1531):** Replaced theme color grid with compact circle selector.
- **Settings Stats (#1533):** Added local session usage statistics panel (SQLite-based).
- **MCP Import (#367):** Added import of `mcp.json` with streamable HTTP configs into SQLite store.

## 4. Community Hot Topics
- **Issue #1487** ([link](https://github.com/netease-youdao/LobsterAI/issues/1487)): "会话中调用python脚本出现问题" – User reports that Python script invocation fails in LobsterAI sessions but works with Claude Code CLI. Two comments, still open. The underlying need is reliable scripting integration, possibly related to environment or skill execution differences. Could benefit from maintainer investigation.
- **Issue #1471** ([link](https://github.com/netease-youdao/LobsterAI/issues/1471)): Input draft loss due to debounce – One comment, open. The debounce (300ms) causes content loss when switching sessions/views too quickly. Community expects immediate persistence on component unmount.
- **Issue #1472** ([link](https://github.com/netease-youdao/LobsterAI/issues/1472)): Re-editing message overwrites unsent input without confirmation – One comment, open. User wants a confirm dialog. Both #1471 and #1472 reflect user frustration over data loss in the cowork editing workflow.

No PRs had reactions or high comment counts; all merged PRs had zero comments/reactions.

## 5. Bugs & Stability
Three open issues updated in the last 24 hours, all classified as bugs:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#1487](https://github.com/netease-youdao/LobsterAI/issues/1487) | Python script invocation broken in sessions (works elsewhere) | None yet |
| **Medium** | [#1471](https://github.com/netease-youdao/LobsterAI/issues/1471) | Input draft lost due to debounce timeout on session/view switch | None yet |
| **Medium** | [#1472](https://github.com/netease-youdao/LobsterAI/issues/1472) | Re-editing history message overwrites unsent input without confirmation | None yet |

Additionally, the recent PRs fixed several stability issues: clipboard fallback chain (#2118), IM reply assembly fix (#2115), and provider model migration preservation (#2117). No regressions or crashes were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
- **Keyboard shortcuts overhaul** (released in 2026.6.5) – Users may request more customizable shortcuts or additional actions.
- **Voice input on macOS** – The PR #2113 adds microphone permission support, signaling upcoming voice features for cowork.
- **Subscription prompts and locked model handling** (#2112) – Suggests ongoing monetization or tiered plan rollout.
- **MCP import** (#367) – Community need for transparent compatibility with existing MCP configurations.
- **Local usage statistics panel** (#1533) – Indicates interest in self-monitoring tools; could expand to cloud sync in future versions.

Likely next version candidates: further voice input integration, enhanced scripting error handling (based on #1487), and draft persistence improvements (based on #1471/#1472).

## 7. User Feedback Summary
- **Dissatisfaction:** Data loss during editing workflow is a recurring pain point—two open issues (#1471, #1472) directly address different forms of content loss. Users expect safe state preservation and confirmation prompts.
- **Pain points:**
  - Python script invocation not working in LobsterAI sessions while working in CLI (#1487) – affects power users.
  - Lack of microphone permission handling on macOS (now fixed in upcoming build via PR #2113).
- **Satisfaction:** No explicit positive feedback captured, but the rapid release cycle and number of merged PRs (13) indicate active development addressing both features and bugs. The artifact preview enhancements (#2114) likely improve the user experience for file-heavy workflows.

## 8. Backlog Watch
- **Issue #1487** ([link](https://github.com/netease-youdao/LobsterAI/issues/1487)) – Open since April 5, stale, no maintainer comment. Important because it blocks Python scripting workflow.
- **Issue #1471** ([link](https://github.com/netease-youdao/LobsterAI/issues/1471)) – Open since April 4, stale. UX regression that causes data loss; should be prioritized.
- **Issue #1472** ([link](https://github.com/netease-youdao/LobsterAI/issues/1472)) – Open since April 4, stale. Similar UX issue; could be combined with #1471 fix.
- **PR #367** ([link](https://github.com/netease-youdao/LobsterAI/pull/367)) – Closed/merged recently, but the underlying MCP import issue (#351) might still need documentation or testing follow-up.

None of these items have received maintainer attention in over two months. Given the current velocity, maintainers should consider scheduling these for the next sprint to reduce backlog.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-06

## 1. Today’s Overview
Project activity remains steady, with four issues and five pull requests updated in the last 24 hours. A significant bug fix for Telegram streaming (mixing intermediates into final replies) was merged, improving the integration’s reliability. The community filed two UI-related bugs and one feature request, while maintainers advanced sandbox improvements for both Podman and Docker deployments. No new releases were cut, but the codebase shows ongoing focus on deployment robustness and user‑facing polish.

## 2. Releases
**None.** No new releases were published in the reported period.

## 3. Project Progress
- **[PR #1099 – Separate Telegram progress stream from final replies](https://github.com/moltis-org/moltis/pull/1099)** was **merged**, fixing the underlying bug [#1097](https://github.com/moltis-org/moltis/issues/1097). Telegram streaming now sends silent progress updates that are deleted after the final reply is delivered, preventing intermediate output from contaminating the final message.
- **[Issue #1097 – Telegram edit-in-place streaming bug](https://github.com/moltis-org/moltis/issues/1097)** was **closed** after the above PR was merged.
- Four other PRs remain open but were updated recently, indicating continued work on sandbox tool fallbacks, Podman support, and model preference management (see sections below).

## 4. Community Hot Topics
No single issue or PR attracted a high number of comments or reactions; all items in the 24‑hour window have zero or one comment. The most discussed item was the now‑closed Telegram bug (1 comment). The following recent issues and PRs are likely to generate community interest as they become more widely noticed:

- **[Issue #1109 – Update banner does not account for Docker installs](https://github.com/moltis-org/moltis/issues/1109)** – A clear pain point for Docker users that could affect upgrade awareness.
- **[PR #1106 – Support Podman escape hatches](https://github.com/moltis-org/moltis/pull/1106)** and **[PR #1105 – Fix Docker sandbox filesystem tool fallback](https://github.com/moltis-org/moltis/pull/1105)** – Both address container deployment reliability, a key theme for self‑hosted users.

## 5. Bugs & Stability
Two new bugs were filed; both are of **moderate to low** severity (no crashes or data loss reported):

| Issue | Title | Severity | Fix In Progress |
|-------|-------|----------|-----------------|
| [#1109](https://github.com/moltis-org/moltis/issues/1109) | Update banner does not account for Docker installs | Medium (user confusion, missed updates) | No PR yet |
| [#1108](https://github.com/moltis-org/moltis/issues/1108) | Session list shows times but not dates for past‑day sessions | Low (inconvenience, especially for users active across midnight) | No PR yet |

The previously reported Telegram streaming bug was resolved with the merge of PR #1099.

## 6. Feature Requests & Roadmap Signals
One explicit feature request was filed:

- **[Issue #1107 – Multiline text input in the mobile web UI](https://github.com/moltis-org/moltis/issues/1107)** – A friction point for mobile users who need to paste or type long messages.

Additionally, two open PRs indicate roadmap priorities:

- **[PR #1104 – Allow replacing preferred models](https://github.com/moltis-org/moltis/pull/1104)** – Enhances provider model management, likely to ship in the next minor release.
- **[PR #1106 – Podman escape hatches](https://github.com/moltis-org/moltis/pull/1106)** and **[PR #1105 – Docker sandbox filesystem fallback](https://github.com/moltis-org/moltis/pull/1105)** – Both improve sandbox reliability across container runtimes, suggesting a near‑term focus on deployment flexibility.

**Prediction:** The next version will likely include the merged PR #1099 and the three open sandbox/PR fixes (#1104, #1105, #1106), along with the UI polish for session dates if a fix is picked up quickly.

## 7. User Feedback Summary
User pain points extracted from the latest issues and PRs:

- **Telegram integration** – The streaming bug (now fixed) caused frustration for users relying on edit‑in‑place replies.
- **Docker deployment** – The update banner omission means Docker users may not be aware of new versions.
- **Web UI date display** – Past‑day sessions show only times, making it hard to distinguish sessions from different days.
- **Mobile web experience** – Lack of multiline input limits usability on smartphones.
- **Model preference management** – The ability to de‑prefer or replace models (addressed by PR #1104) appears to be a workflow need for power users.

Overall satisfaction is not directly measured, but the quick closing of the Telegram bug signals responsive issue triage.

## 8. Backlog Watch
No issues were flagged as long‑unanswered in the 24‑hour window. However, one PR merits attention:

- **[PR #1089 – Cap persisted tool results before rehydration](https://github.com/moltis-org/moltis/pull/1089)** – Open since June 1, last updated June 5. This PR impacts session history size and streaming consistency across multiple conversation modes. With the recent Telegram fix merged, this PR may be a candidate for the next merge window. Maintainers should review it soon to avoid merge conflicts.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest - June 6, 2026

*Generated from GitHub activity data (agentscope-ai/CoPaw)*

## 1. Today's Overview

The CoPaw project shows high community engagement with **21 issues** and **24 pull requests** updated in the last 24 hours. Activity is concentrated on bug fixes, stability improvements, and feature requests. A significant cluster of issues relates to the **Yuanbao channel** (proto file packaging, streaming, authentication) — 5 new bugs filed by a single contributor, many with corresponding fix PRs. The **browser_use** tool also received attention (CDP timeout fix merged). No new releases were cut today. Overall, the project maintains a healthy cadence of triage and pull request review, with multiple first-time contributors submitting PRs.

## 2. Releases

*No new releases in the last 24 hours.*

## 3. Project Progress

**Merged/Closed PRs (15 total)** — several notable fixes and features advanced to `main`:

- **Browser stability**: [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) – Added CDP timeout parameter and browser profile isolation for cross-browser switching.
- **LaTeX rendering**: [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972) – Enabled KaTeX-based LaTeX math formula rendering in Markdown.
- **Security**: [#4026](https://github.com/agentscope-ai/QwenPaw/pull/4026) – `write_file` now blocks overwriting non-empty files (first-time contributor).
- **UI polish**: [#4765](https://github.com/agentscope-ai/QwenPaw/pull/4765), [#4766](https://github.com/agentscope-ai/QwenPaw/pull/4766) – Shield icon centering and scrollbar flicker fix (first-time contributors).
- **Plugin**: [#4934](https://github.com/agentscope-ai/QwenPaw/pull/4934) – Added OpenSandbox plugin for sandboxed shell execution.
- **Gunicorn compatibility**: [#3403](https://github.com/agentscope-ai/QwenPaw/pull/3403) – Deferred provider instantiation to fix gunicorn startup crash.
- **Anthropic tool-result handling**: [#2079](https://github.com/agentscope-ai/QwenPaw/pull/2079) – Strip historical tool-result media on replay.
- **MCP auto-recovery**: [#1347](https://github.com/agentscope-ai/QwenPaw/pull/1347) – Reconnect crashed MCP clients automatically.
- **State storage**: [#1240](https://github.com/agentscope-ai/QwenPaw/pull/1240) – Replaced fragile JSON state with SQLite-backed default.
- **Browser coordinate click**: [#4905](https://github.com/agentscope-ai/QwenPaw/pull/4905) – Added page coordinate click support to `browser_control` (first-time contributor).

**Open PRs** addressing critical channel bugs (see §5) are under active review.

## 4. Community Hot Topics

| Issue / PR | Title | Comments | Highlights |
|---|---|---|---|
| [#4754](https://github.com/agentscope-ai/QwenPaw/issues/4754) (closed) | [Question] 打包方式 – Packaging to EXE | 7 | User asks about differences between PyInstaller and Tauri desktop builds. Resolved? |
| [#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) (closed) | [Bug] browser_use 启动失败 – CDP timeout & Chrome/Edge crash | 6 | Three failure modes documented; resolved via PR #4944. |
| [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) (open) | [Feature] 左侧会话界面列顺序调整 – Session column order | 5 | Community wants "last updated" column moved left; PR #4975 is open. |
| [#4968](https://github.com/agentscope-ai/QwenPaw/issues/4968) (open) | [Bug] Cannot allocate memory – Virtual memory leak | 3 | Severe memory leak on Ubuntu 24.04; root cause under investigation. |
| [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963) (open) | [Feature] Cron: Support direct script/shell execution | 3 | User needs non-AI shell tasks in cron. |
| [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) (open) | [Bug] DeepSeek API 思考过程折叠 – Thinking folding | 3 | Model replies hidden behind collapsed "thinking" block. |
| [#4960](https://github.com/agentscope-ai/QwenPaw/issues/4960) (open) | [Question] 桌面版局域网手机访问 – LAN mobile access | 3 | Unable to reach console via mobile browser despite whitelisting. |
| [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) (open) | [Bug] 执行过程陷入死循环 – Infinite loop in agent execution | 4 | Agent loops indefinitely; user on v1.1.10. |

**Underlying needs**: Users are asking for better documentation on packaging formats, more robust browser automation, flexible cron capabilities, mobile access for local deployments, and visual polish (column ordering, avatar support).

## 5. Bugs & Stability

**High Severity**

- **Virtual memory leak**: [#4968](https://github.com/agentscope-ai/QwenPaw/issues/4968) – `qwenpaw subprocess fork fails with "Cannot allocate memory"` on Ubuntu. Likely a memory leak in subprocess handling. No fix PR yet; status open.
- **Infinite loop**: [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) – Agent execution loops without exit. User on v1.1.10. No reproducer provided.
- **Yuanbao channel missing proto files**: [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976) – `proto/conn.json` and `proto/biz.json` not included in pip wheel. Blocks channel startup entirely. Fix not yet merged.
- **Yuanbao protobuf compatibility**: [#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977) – `including_default_value_fields` not supported in protobuf <4.x. Fix likely needed.
- **Yuanbao AuthBindRsp missing `connectId`**: [#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978) – Causes connection tracking failure. PR [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) open.
- **Yuanbao streaming replies dropped**: [#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979) – `on_streaming_end` empty → replies lost. PR [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) open.

**Medium / Low Severity**

- **DeepSeek thinking folding**: [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) – Replies hidden in collapsed thinking block. Workaround: expand manually.
- **`bot_id` required in SendC2CMessage**: [#4980](https://github.com/agentscope-ai/QwenPaw/issues/4980) – Despite correct proto encoding, error persists. Under investigation.
- **Session config corruption crash**: [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) – Corrupted `loop_config.json` or `prd.json` causes total APE crash. No graceful error handling.
- **Cmd window flash on Windows**: [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) – `subprocess` missing `CREATE_NO_WINDOW` flag. Open.

**Bugs with Fix PRs (open or merged today)**:
- [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972) – LaTeX display (merged)
- [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944) – browser_use stability (merged)
- [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) – Yuanbao streaming reply drop (open)
- [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) – Yuanbao connectId tracking (open)

## 6. Feature Requests & Roadmap Signals

Top user-requested features from today’s activity:

- **Cron script/shell execution**: [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963) – Add direct bash execution task type. Likely to be implemented given existing cron infrastructure.
- **Customizable session column order**: [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) – PR [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) already open; expects merge in upcoming release.
- **Per-Agent avatar**: [#4974](https://github.com/agentscope-ai/QwenPaw/issues/4974) – Upload/set avatar for each agent, displayed in UI. Moderate effort.
- **Session sidebar / easier conversation switching**: [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) – Users want a permanent session list instead of two clicks per switch. High demand for UX improvement.
- **Merge duplicate provider cards**: [#4965](https://github.com/agentscope-ai/QwenPaw/issues/4965) – Collapse multiple entries for same brand (e.g., Zhipu) into one with dropdown. UI cleanup.

**Prediction**: Column order (PR #4975) and potentially cron script execution (#4963) are most likely to land in the next release. Avatar support and session sidebar are longer-term.

## 7. User Feedback Summary

**Pain points**:
- **Packaging confusion**: Users are unsure which desktop client to use (PyInstaller vs Tauri) and how to package their own EXE (#4754).
- **Browser automation fragile**: `browser_use` fails with CDP timeouts and browser crashes; even after #4944, some edge cases remain.
- **Memory issues**: Memory leak on Linux (#4968) is a serious blocker for server deployments.
- **Yuanbao channel: almost unusable out of box**: Missing proto files, protobuf compatibility, and streaming bugs make the channel a high-friction experience.
- **Infinite agent loops**: User reports agent getting stuck in iteration (#4967) — indicates missing loop termination logic.
- **Mobile access blocked**: Cannot reach console from LAN mobile despite whitelisting (#4960).
- **DeepSeek UI glitch**: Model’s “thinking” section obscures final reply (#4962).

**Satisfaction signals**:
- **LaTeX rendering fix** (PR #4972) addressed an outstanding display bug; thanked by reporter.
- **Security improvements** (write file guard #4026, file preview restriction #4981) show proactive hardening.
- **Community welcoming first-time contributors**: 6+ PRs from new contributors were merged or are under review.
- **Reactive maintainers**: Several issues filed today already have open fix PRs (e.g., Yuanbao issues #4976–4980).

## 8. Backlog Watch

| Issue | Created | Last Updated | Comments | Status |
|---|---|---|---|---|
| [#4744](https://github.com/agentscope-ai/QwenPaw/issues/4744) – macOS Tauri Intel support? | 2026-05-28 | 2026-06-05 | 2 | Open, no maintainer reply. |
| [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) – cmd window flash on Windows | 2026-05-31 | 2026-06-05 | 2 | Open, no action since label. |
| [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) – DeepSeek thinking folding | 2026-06-04 | 2026-06-05 | 3 | Open, no maintainer assignment. |
| PR [#4822](https://github.com/agentscope-ai/QwenPaw/pull/4822) – Fix cron empty traces | 2026-05-29 | 2026-06

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-06

**Generated from GitHub activity (github.com/zeroclaw-labs/zeroclaw)**

---

## 1. Today's Overview

ZeroClaw is in a period of intense development, with 50 issues and 50 pull requests updated in the last 24 hours. Activity is concentrated on security hardening, RFC-driven architecture changes (output routing, air-gapped mode, OIDC auth, per-model capabilities), and a massive expansion of the web dashboard (MCP management, SMS channels, plugin lifecycle). The project merged or closed 13 PRs today, with no new stable release yet – the next milestone (0.80‑beta1 or 0.9.0) is being built incrementally through these RFCs and stacked PRs. Community engagement is high, with several feature requests and bug reports receiving multiple maintainer comments, though some important items remain blocked awaiting maintainer review.

---

## 2. Releases

**None** – no releases were tagged in the last 24 hours. The latest known milestone target is **v0.9.0**, with several tracking issues (e.g., #7142 pluggable security provider, #7141 OIDC auth) pointing to that version.

---

## 3. Project Progress

**Merged/Closed PRs (13 total)** – the most notable advances today:

- **Security & Policy**
  - [#7281](https://github.com/zeroclaw-labs/zeroclaw/pull/7281) – Fixed `forbidden_path_argument` false‑positives on heredoc bodies and non‑path tildes (config/policy).
  - [#7123](https://github.com/zeroclaw-labs/zeroclaw/pull/7123) – Fixed UTF‑8 char‑boundary panics in text truncation (Bluesky, dashboard, LinkedIn).
  - [#7261](https://github.com/zeroclaw-labs/zeroclaw/pull/7261) – Redacted nested object‑array secrets in config display.
  - [#7258](https://github.com/zeroclaw-labs/zeroclaw/pull/7258) – Tombstoned killed ACP sessions to prevent silent revival.
  - [#7254](https://github.com/zeroclaw-labs/zeroclaw/pull/7254) – Stripped think blocks before native tool‑call output.

- **Provider & Channel Expansion**
  - [#7163](https://github.com/zeroclaw-labs/zeroclaw/pull/7163) – Added `extra_body` support for OpenAI‑compatible providers (enables provider‑specific fields like `thinking`).
  - [#7244](https://github.com/zeroclaw-labs/zeroclaw/pull/7244) – Reinforced tool formatting prompts & added robust JSON fallback parser for `file_write` (Gemini + Discord).
  - [#7260](https://github.com/zeroclaw-labs/zeroclaw/pull/7260) – Added 7 new OpenAI‑compatible providers under schema v3: Morph, GitHub Models, Upstage, Featherless, Arcee, Lambda AI, Inception.
  - [#7265](https://github.com/zeroclaw-labs/zeroclaw/pull/7265) – Added Twilio, Plivo, Telnyx, Sinch & Vonage SMS channels (schema v3).
  - [#7270](https://github.com/zeroclaw-labs/zeroclaw/pull/7270) – Added Mastodon, Rocket.Chat, Zulip & Lemmy polling channels (schema v3).

- **Dashboard & Developer Experience**
  - [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) – Added four first‑class dashboard tabs (MCP, Skills, Plugins, Providers) to the web UI.
  - [#7235](https://github.com/zeroclaw-labs/zeroclaw/pull/7235) – Added plugin lifecycle endpoints + management UI stubs.
  - [#7240](https://github.com/zeroclaw-labs/zeroclaw/pull/7240) – Made quickstart provider alias editable (fixes #7227).
  - [#7247](https://github.com/zeroclaw-labs/zeroclaw/pull/7247) – Fixed `paired_tokens` drift false‑positive and made ReloadBanner dismissable.

- **Documentation**
  - [#7255](https://github.com/zeroclaw-labs/zeroclaw/pull/7255) – Clarified merge‑ready milestone fallback in PR review docs.
  - [#7262](https://github.com/zeroclaw-labs/zeroclaw/pull/7262) – Added worked examples for the 7 new schema‑v3 providers.
  - [#7277](https://github.com/zeroclaw-labs/zeroclaw/pull/7277) – Added Shazam WASM plugin as a pilot plugin.

- **Infrastructure**
  - [#7176](https://github.com/zeroclaw-labs/zeroclaw/pull/7176) – StageX container pipeline with musl static linking (removed cmake dependency).

---

## 4. Community Hot Topics

The following issues and PRs generated the most discussion (comments) in the last 24h:

1. **#6808** – *RFC: Work Lanes, Board Automation, and Label Cleanup* (9 comments)  
   [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)  
   A governance RFC aiming to reduce manual maintainer overhead through automated P‑R lanes and label cleanup. Indicates the project is maturing its community workflow.

2. **#6969** – *RFC: Unified output routing model (per‑peer modality preference + agent send_via tool)* (7 comments)  
   [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6969)  
   A user who migrated from Letta misses explicit output delivery control. This RFC proposes a formal mechanism for per‑peer modality and an agent `send_via` tool – a highly requested feature for multi‑channel agents.

3. **#5601** – *Add subscription‑native OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax* (6 comments)  
   [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)  
   A long‑standing request (opened April 10) to avoid static API keys. Blocked with `needs-maintainer-review` tag.

4. **#7232** – *RFC: Structured Observability Enhancement* (3 comments, created today)  
   [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)  
   Proposes richer event context (channel/agent/LLM I/O) and OTel trace correlation. Already has a companion PR (#7233) – moving fast.

5. **#7155** – *RFC: Per‑execution confirmation tier for high‑risk shell commands + Claude Code‑style policy* (4 comments)  
   [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)  
   Addresses a missing middle ground between allow/block for shell commands – a security UX gap that many users encounter.

**Underlying needs:** The community is pushing for better **security granularity** (shell confirmation, pluggable providers), **multi‑channel orchestration** (output routing, SMS/chat channels), **developer experience** (MCP dashboard, LSP support), and **observability** for production deployments.

---

## 5. Bugs & Stability

**High‑severity bugs reported or fixed today:**

| Issue | Severity | Description | Status |
|-------|----------|-------------|--------|
| [#7059](https://github.com/zeroclaw-labs/zeroclaw/issues/7059) | S2 – degraded | “default model provider” credential/URL fallback in channel orchestrator; violates V3 schema | In progress |
| [#7247](https://github.com/zeroclaw-labs/zeroclaw/issues/7247) (PR) | High | `is_gateway_managed_field` typo caused `paired_tokens` false‑positive drift detection | Fixed (PR merged) |
| [#7258](https://github.com/zeroclaw-labs/zeroclaw/issues/7258) (PR) | High | ACP session kill left durable row restorable; admin actions could be silently undone | Fixed (PR merged) |
| [#7254](https://github.com/zeroclaw-labs/zeroclaw/issues/7254) (PR) | High | `think` blocks leaked through native tool‑call output | Fixed (PR merged) |
| [#7123](https://github.com/zeroclaw-labs/zeroclaw/issues/7123) (PR) | High | UTF‑8 char‑boundary panics in text truncation (CJK, emoji) | Fixed (PR merged) |
| [#7261](https://github.com/zeroclaw-labs/zeroclaw/issues/7261) (PR) | High | Nested secrets not redacted in config display | Fixed (PR merged) |

Other notable open bugs:
- [#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120) (closed) – Onboarding: OpenAI Codex prompts for OpenAI API key instead (S1, fixed but no release yet).
- [#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) – Tracking issue for pluggable security provider (v0.9.0 target, in progress).

No new crashes or regressions were reported today beyond those already fixed.

---

## 6. Feature Requests & Roadmap Signals

**Active RFCs and feature issues that indicate the project’s direction:**

- **Work Lanes & Label Automation** (#6808) – governance automation, likely for 0.80‑beta1.
- **Unified Output Routing** (#6969) – per‑peer modality preference; a foundational feature for multi‑channel agents.
- **Pluggable Security Provider Interface** (#7142) – targeting v0.9.0, will make security enforcement extensible.
- **OIDC Authentication Provider** (#7141) – also targeting v0.9.0, for RPC/WSS transport.
- **Air‑Gapped Execution Mode** (#6293) – companion daemon over Unix socket; high demand for offline/secure deployments.
- **Per‑Model Capability Configuration** (#7100) – vision, context window; requested by UI/UX users.
- **Per‑Execution Shell Confirmation** (#7155) – addresses a common pain point for power users.
- **LSP Support for Coding Workflows** (#5907) – blocked but accepted; would improve code‑generation quality.
- **Skill‑Scoped Tool Activation** (#6915) – temporary elevation during skill execution; blocked.
- **Process‑Memory Limits on Shell Subprocess** (#6916) – accepted, will prevent container OOM.

**Predictions for next release (0.80‑beta1 or v0.9.0):**  
The merged PRs for MCP dashboard, SMS/chat channels, new providers, and security fixes are likely to land in the next beta. The RFCs for output routing, pluggable security, OIDC, and air‑gapped mode are more ambitious and may target v0.9.0.

---

## 7. User Feedback Summary

**Pain points expressed in issues:**

- **Output routing inflexibility** – “I migrated from Letta and lost the ability to control *how* and *where* a reply is delivered” (#6969).
- **Onboarding friction** – Choosing Codex prompts for OpenAI API key instead of Codex subscription (#6120); quickstart provider alias not editable (#7227, fixed today).
- **Skill audit false positives** – Remote markdown link check blocks valid skills (e.g., Anthropic knowledge‑work plugins) (#6714).
- **No per‑model visual or context‑window indicators** in TUI or web UI (#7100).
- **Windows shell limitation** – `cmd.exe` used by default; users want configurable PowerShell or Git Bash (#7089).
- **High shell‑risk commands** – Only allow/block, no “ask before run” middle tier (#7155).
- **Config complexity** – Hand‑editing required for MCP servers and some provider settings; web dashboard now addressing this.

**Satisfaction signals:**  
High engagement (50 issues, 50 PRs updated daily), multiple community contributors (singlerider, Audacity88, theonlyhennygod, alex-nax, NiuBlibing, tidux), and positive reactions (👍 on #5601, #5882). The project is actively listening and fixing reported bugs quickly.

---

## 8. Backlog Watch

Issues that have been open for a long time, are important, and appear **blocked** or **needing maintainer review**:

| Issue | Date Opened | Labels | Status | Why it matters |
|-------|-------------|--------|--------|----------------|
| [#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601) | 2026-04-10 | `enhancement, security, status:blocked, needs-maintainer-review` | Blocked | OAuth support for 4 providers – requested by many users. |
| [#5907](https://github.com/zeroclaw-labs/zeroclaw/issues/5907) | 2026-04-19 | `enhancement, status:blocked, type:rfc` | Blocked | LSP support for coding – a key differentiator for agent quality. |
| [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) | 2026-05-03 | `enhancement, status:blocked, needs-maintainer-review` | Blocked | Air‑gapped mode – critical for enterprise/security deployments. |
| [#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715) | 2026-05-16 | `enhancement, status:blocked, needs-maintainer-review` | Blocked | Delete unneeded branches – organizational hygiene. |
| [#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) | 2026-05-25 | `enhancement, status:blocked, needs-maintainer-review` | Blocked | Enforce `allowed_tools` in main agent loop – security gap. |
| [#6915](https://github.com/zeroclaw-labs/zeroclaw/issues/6915) | 2026-05-25 | `enhancement, status:blocked, needs-maintainer-review` | Blocked | Skill‑scoped tool activation – required for composio skills. |
| [#5908](https://github.com/zeroclaw-labs/zeroclaw/issues/5908) | 2026-04-19 | `enhancement, status:blocked, needs-maintainer-review` | Blocked | CI/CD container builds – needed for release automation. |

These items should be prioritized to unblock community contributions and maintain momentum. The project has strong ongoing RFC work, but several past proposals are waiting for maintainer decisions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*