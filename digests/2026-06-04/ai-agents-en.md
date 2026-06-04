# OpenClaw Ecosystem Digest 2026-06-04

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-04 02:55 UTC

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

# OpenClaw Project Digest – 2026-06-04

## 1. Today’s Overview
The project is in a period of **very high activity**, with 500 issues and 500 pull requests updated in the last 24 hours. Of those issues, 383 remain open/active and 117 have been closed. On the PR side, 406 are open and 94 were merged or closed. Three new releases were cut today, including a beta (v2026.6.2-beta.1) and two stable patches. While development velocity is strong, the project continues to carry a **significant bug backlog** — many P1 regression and session-state issues remain open, some for weeks. Community engagement is high, with several issues drawing double-digit comments and multiple 👍 reactions, indicating acute user pain points around message loss, session stability, and UI regressions.

---

## 2. Releases
Three releases were published today:

- **v2026.6.2-beta.1**  
  *Highlights:* Plugin and skill installs now use an **operator install policy** instead of the old dangerous-code scanner path. The CLI, ClawHub, and troubleshooting surfaces have been updated to reflect the new policy for package, archive, source, upload, and marketplace installs. (#89516)  
  *Potential breaking change:* Operators relying on the previous scanner behavior may need to update their install workflows or policies.

- **v2026.6.1** (stable)  
  *Highlights:* Agents and CLI-backed runtimes recover more cleanly from:
  - Interrupted tool calls
  - Stale session bindings
  - Compaction handoffs
  - Media delivery retries  
  Channels (Telegram, WhatsApp, iMessage, Slack) and mobile delivery are now steadier. (#88129, #88136, #88141, #88162, #88182)

- **v2026.6.1-beta.3** (same changelog as v2026.6.1)

No explicit migration notes were provided beyond the release highlights.

---

## 3. Project Progress
Today **94 PRs were merged or closed**. Among the most commented pull requests, two notable closures stand out:

- [#90131 – fix(subagent-announce): durable-queue fallback when direct handoff is pending](https://github.com/openclaw/openclaw/pull/90131) – Ensures child subagent completion announcements survive transient gateway delays.
- [#90127 – feat(control-plane): add tranche A/B registry and CI gate](https://github.com/openclaw/openclaw/pull/90127) – Adds scaffolding for contracts, schemas, registries, and CI gates for phased rollouts.

Other active PRs that advanced today or are close to merge include:

- [#89183 – fix(tui): keep local slash commands out of model prompts](https://github.com/openclaw/openclaw/pull/89183) (ready for maintainer review)
- [#88504 – feat(memory): add multi-slot memory role architecture](https://github.com/openclaw/openclaw/pull/88504) (ready for maintainer review) – large feature enabling composable memory plugins.
- [#90124 – fix(agents): harden tool-call handling against A2A/model tool-call poisoning](https://github.com/openclaw/openclaw/pull/90124) (needs proof) – addresses unbounded invalid tool-call loops.
- [#90125 – fix(embedded-runner): distinguish model initialization errors from assistant execution errors](https://github.com/openclaw/openclaw/pull/90125) (needs proof)
- [#90066 – fix(telegram): suppress reconnect drain re-entry while delivery is in-flight](https://github.com/openclaw/openclaw/pull/90066) (needs proof)

Multiple PRs are labelled with `merge-risk: 🚨 session-state` or `🚨 message-delivery`, indicating that the team is carefully reviewing stability-critical changes.

---

## 4. Community Hot Topics
The following issues drew the most discussion and reactions in the last 24 hours:

| Issue | Comments | Reactions | Summary |
|---|---|---|---|
| [#88838 – Track core session/transcript SQLite migration via accessor seam](https://github.com/openclaw/openclaw/issues/88838) | 17 | 1 👍 | A planned branch-by-abstraction approach to replace the high-risk full migration. |
| [#65161 – Heartbeat isolated mode: cadence stalls, mislabels exec-events, heavy context, missing writer](https://github.com/openclaw/openclaw/issues/65161) | 14 | 1 👍 | Multi-faceted regression in heartbeat mechanics; open since April 12. |
| [#67035 – Windows chat UI regression: input swallowed, invisible replies, flashing indicator](https://github.com/openclaw/openclaw/issues/67035) | 14 | 0 👍 | Closed bug, but still a top conversation driver. |
| [#88312 – Codex app-server turn-completion stall returns (regression of #84076)](https://github.com/openclaw/openclaw/issues/88312) | 12 | 2 👍 | P1 regression in Codex; priority fix needed. |
| [#68113 – Mattermost slash commands return 503 "not yet initialized"](https://github.com/openclaw/openclaw/issues/68113) | 11 | 3 👍 | P1 regression since v2026.4.15, affecting many Mattermost users. |
| [#63216 – Repeated hard resets on same session key; retry loop re-injects bootstrap context](https://github.com/openclaw/openclaw/issues/63216) | 11 | 3 👍 | Persistent session crash loop with high compaction headroom configured. |
| [#85030 – MCP tools not injected into subagent (sessions_spawn) sessions](https://github.com/openclaw/openclaw/issues/85030) | 6 | 3 👍 | P1 behavior bug blocking MCP-based multi-agent setups. |
| [#77467 – MiniMax Portal OAuth cannot auto-refresh](https://github.com/openclaw/openclaw/issues/77467) | 5 | 3 👍 | Tokens expire after ~2 hours; no auto-refresh implemented. |

The underlying needs are clear: users are **demanding session stability (no crashes, no message loss)**, reliable channel delivery (Telegram, Mattermost, Discord), and proper handling of long-running or complex tool interactions. There is also strong interest in **SQLite migration** and **multi-agent MCP tool injection** for production deployments.

---

## 5. Bugs & Stability
Several high-severity bugs remain open or were actively discussed today:

### P1 Regressions / Critical

- [#88312 – Codex turn-completion stall (regression of #84076)](https://github.com/openclaw/openclaw/issues/88312) – No linked fix PR yet.
- [#86214 – Codex app-server client closes mid-turn during image/tool requests with large logs_2.sqlite](https://github.com/openclaw/openclaw/issues/86214) – P1, impacts session-state and message loss.
- [#87310 – Stale diagnostic tool_call activity can survive recovery and re-block sessions](https://github.com/openclaw/openclaw/issues/87310) – P1, fix PR [#86806](https://github.com/openclaw/openclaw/pull/86806) in review.
- [#81484 – Discord guild reply regression: malformed send payloads and repeated outbound loops](https://github.com/openclaw/openclaw/issues/81484) – P1, linked PR [#82572](https://github.com/openclaw/openclaw/pull/82572) open.
- [#63216 – Repeated hard resets on same session key](https://github.com/openclaw/openclaw/issues/63216) – P1, no fix PR yet.
- [#68113 – Mattermost slash commands 503](https://github.com/openclaw/openclaw/issues/68113) – P1, no fix PR yet.
- [#86215 – Codex OAuth refresh failures wedge agent for hours](https://github.com/openclaw/openclaw/issues/86215) – P1, no fix PR.

### Other Notable Bugs

- [#76038 – Stuck Session Recovery mechanism double failure + excessive preprocessing time](https://github.com/openclaw/openclaw/issues/76038) – P2 but affects session crash loops.
- [#67793 – queue.mode "collect" not batching messages (closed)](https://github.com/openclaw/openclaw/issues/67793) – Closed, but the underlying issue may still affect users.
- [#67419 – Bootstrap files re-injected every turn wasting 20-30% tokens](https://github.com/openclaw/openclaw/issues/67419) – P2, performance impact.
- [#63998 – Session transcript doomloop: crash-restart cycle inflates transcript until OOM](https://github.com/openclaw/openclaw/issues/63998) – P1, crash-loop risk.
- [#68691 – Sandbox zombie processes accumulate until pids.max risk](https://github.com/openclaw/openclaw/issues/68691) – P1, security/availability risk.

**Fix PRs exist for some issues:**  
- [#89183](https://github.com/openclaw/openclaw/pull/89183) addresses TUI slash command forwarding (#71592).  
- [#86806](https://github.com/openclaw/openclaw/pull/86806) addresses crashed main session recovery.  
- [#90124](https://github.com/openclaw/openclaw/pull/90124) hardens tool-call handling against poison loops.  
- [#90130](https://github.com/openclaw/openclaw/pull/90130) fixes auth metadata guard.

Overall, **session-state and message-loss bugs dominate the P1 landscape**, and the community is feeling the impact.

---

## 6. Feature Requests & Roadmap Signals
Notable feature requests with active discussion:

- [#72741 – Standard Interface for External Security and Guardrail Checks](https://github.com/openclaw/openclaw/issues/72741) – 8 comments, 1 👍. Could become a high-impact addition for enterprise deployments.
- [#63990 – Multi-index embedding memory with model-aware failover](https://github.com/openclaw/openclaw/issues/63990) – 6 comments, 1 👍. Important for production vector search reliability.
- [#76159 – Per-job acceptSilentStop flag for cron jobs that produce no output](https://github.com/openclaw/openclaw/issues/76159) – 5 comments, 1 👍. Addresses a common cron workflow pain point.
- [#67000 – Warm-up / session reuse for embedded agents (active-memory)](https://github.com/openclaw/openclaw/issues/67000) – 5 comments, 2 👍. Performance optimization for interactive use.
- [#64438 – Remote Reranker Endpoint Support](https://github.com/openclaw/openclaw/issues/64438) – 5 comments. Improves search quality.
- [#71142 – Configurable upload size limit for Control UI](https://github.com/openclaw/openclaw/issues/71142) – 7 comments. User-facing improvement.

**Likely for next version (2026.6.x):**  
- The **multi-slot memory architecture** (PR #88504) is ready for maintainer review and could land soon.  
- **External security guardrail interface** (#72741) may be targeted if prioritized.  
- **Per-job acceptSilentStop** (#76159) is a small, clear win.  
- **Remote reranker support** (#64438) could follow memory infra improvements.

---

## 7. User Feedback Summary
Based on issue comments and reactions, user sentiment is mixed:

- **Pain points:**  
  - Repeated session crashes and context-bleed (e.g., #63216, #63998, #67419).  
  - Message loss across channels (Telegram, Discord, WebChat) – #67035, #77136, #64810.  
  - Regression on each update – many issue authors report “worked before, fails now”.  
  - Auth token expiration without auto-refresh (#77467, #86215).  
  - MCP tools not working with subagents (#85030) – limits advanced multiagent setups.  
  - WebChat UI rendering issues (#67035, #77136, #86811) – users forced to switch to TUI.

- **Satisfaction signals:**  
  - The v2026.6.1 release notes (cleaner recovery from interrupted tool calls) are likely welcome, but no explicit positive feedback appears in the top issues.  
  - The community is actively contributing PRs (94 merged/closed today), indicating a healthy contributor base.

Overall, users are **f

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant Ecosystem
**Date: 2026-06-04**

---

## 1. Ecosystem Overview

The open-source personal AI agent landscape is undergoing rapid maturation, with several projects converging on a shared set of core challenges—session reliability, memory management, multi-agent orchestration, and enterprise security—while diverging in architectural philosophy and target audience. The ecosystem is bifurcating into two broad categories: **heavyweight, feature-rich reference implementations** (OpenClaw, IronClaw) that prioritize comprehensive functionality at the cost of complexity and bug backlogs, and **lightweight, opinionated alternatives** (NanoBot, PicoClaw, NullClaw) that emphasize minimalism, rapid iteration, and developer ergonomics. A third emerging category—**desktop-first consumer agents** (Hermes Agent, LobsterAI, Moltis, CoPaw)—blurs the line between development framework and end-user product, with strong emphasis on UI polish and channel integration. The ecosystem is healthy and competitive, with cross-pollination of ideas (e.g., MCP standardization, multi-agent patterns) but no single dominant design yet.

---

## 2. Activity Comparison (Last 24 Hours)

| Project | Issues Updated | Open Issues | PRs Updated | PRs Merged/Closed | New Release | Health Score |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 383 (76.6%) | 500 | 94 | ✅ v2026.6.2-beta.1, v2026.6.1, v2026.6.1-beta.3 | ⚠️ **Guarded** — high velocity, massive bug backlog (383 open), P1 regressions dominate |
| **IronClaw** | 27 | 19 (70.4%) | 50 | 29 (58%) | ✅ v0.29.1 | 🟢 **Good** — strong fix-to-bug ratio, Reborn architecture advancing |
| **ZeroClaw** | 30 | 27 (90.0%) | 50 | 3 (6%) | ❌ | 🟡 **Moderate** — release prep, many S1 bugs, strong TUI/Security focus |
| **CoPaw** | 44 | 22 (50.0%) | 49 | 21 (42.9%) | ❌ | 🟢 **Good** — high close rate, responsive maintainers, known memory stability issues |
| **NanoBot** | 33 | — | 34 | 18 (52.9%) | ❌ | 🟢 **Good** — lean backlog, steady merges, memory and MCP stability improving |
| **Hermes Agent** | 50 | 43 (86.0%) | 50 | 7 (14%) | ❌ | 🟡 **Moderate** — active community, but P0 security bug (#38643) and P1 Windows/PID bugs unfixed |
| **LobsterAI** | 0 | — | 16 | 14 (87.5%) | ✅ 2026.6.3 | 🟢 **Good** — efficient release cycle, MCP/cowork focus, one user complaint |
| **Moltis** | 14 | 5 (35.7%) | 3 | 0 | ✅ 2 daily builds | 🟢 **Good** — high closure rate (9 issues closed), Docker/Podman gaps remain |
| **PicoClaw** | 4 | 4 (100%) | 10 | 2 (20%) | ❌ | 🟡 **Moderate** — critical PID bug (#2720) unresolved, two competing fix PRs |
| **NanoClaw** | 1 | 1 (100%) | 9 | 0 | ❌ | 🟡 **Moderate** — scheduler/encryption fixes pending, low merge velocity |
| **NullClaw** | 0 | 0 | 1 | 0 | ❌ | 🔴 **Low** — zero community engagement, single PR awaiting review |
| **ZeptoClaw** | 0 | 0 | 16 | 0 | ❌ | 🔴 **Low** — only Dependabot PRs, no human activity |
| **TinyClaw** | 0 | — | 0 | 0 | ❌ | 🔴 **Inactive** |

**Health Score Definitions:**
- 🟢 **Good** — Active merges, manageable backlog, critical bugs being addressed
- 🟡 **Moderate** — Notable unresolved issues or bottlenecks
- ⚠️ **Guarded** — Activity high but quality/debt concerns
- 🔴 **Low/Inactive** — No meaningful community or maintainer activity

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Community scale**: OpenClaw's 500 issues and 500 PRs updated daily is an order of magnitude larger than any peer; it is the de facto reference implementation and ecosystem gateway (ClawHub, operator install policy).
- **Ecosystem breadth**: Plugin/skill marketplace (ClawHub), multi-channel support (Telegram, WhatsApp, iMessage, Slack, Discord), and rich CLI/TUI tooling.
- **Release cadence**: Three releases in one day (beta + two stable patches) demonstrates strong CI/CD maturity.
- **Cross-project influence**: Features like multi-slot memory architecture (#88504), operator install policy (#89516), and durable queue fallback (#90131) set patterns that smaller projects (NanoBot, PicoClaw) later mirror.

**Technical Approach Differences:**
- OpenClaw adopts a **monolithic, Python-heavy architecture** with deep integration across all components (agent, CLI, channels, memory, MCP). This enables rapid feature development but creates complex dependency chains and regression surfaces.
- By contrast, **NanoBot** (modular plugins), **IronClaw** (Rust-based Reborn rewrite), and **ZeroClaw** (Rust-native) favor decoupled architectures with stronger stability guarantees and fewer moving parts.
- OpenClaw commits to the **MCP (Model Context Protocol)** first-class ecosystem, while others (Moltis, CoPaw) treat MCP as an optional add-on.

**Community Size Comparison:**
- OpenClaw's community is **dominant but frustrated** — 383 open issues, many with 10+ comments and high 👍 counts for recurring P1 bugs (session crashes, message loss, channel regressions). The "worked before, fails now" sentiment is a red flag.
- NanoBot (33 issues) and CoPaw (44 issues) have smaller but more satisfied user bases, with faster issue-to-fix cycles.
- Hermes Agent (50 issues) and IronClaw (27 issues) sit in the middle — active communities that report bugs constructively but face fewer regressions than OpenClaw.

**Key Risk**: OpenClaw's velocity may be destabilizing—383 open issues with many P1 regressions suggests the project may benefit from a stabilization sprint before adding further features.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across **3+ projects** in today's digests, indicating ecosystem-wide priorities:

| Focus Area | Projects Affected | Specific Needs |
|---|---|---|
| **Session Stability & Message Loss** | OpenClaw, Hermes Agent, IronClaw, CoPaw, NanoBot | Crash loops, context bleed, missed delivery, incomplete tool calls — **the #1 cross-project pain point** |
| **MCP Integration & Stability** | OpenClaw, NanoBot, PicoClaw, LobsterAI, Moltis | Session reconnection, parameter validation, URL validation, node awareness, timeout handling |
| **Memory & Context Management** | CoPaw, NanoBot, Moltis, Hermes Agent | Compaction failures, context blowup, deduplication, model-aware failover, user control over memory scope |
| **Multi-Agent Orchestration** | NanoBot, OpenClaw, Hermes Agent, CoPaw | Subagent tool injection, inter-agent communication (mailbox channels), hierarchical permission models |
| **Security Hardening** | ZeroClaw, Hermes Agent, PicoClaw, CoPaw | Path traversal defense, OIDC/OAuth, pluggable security providers, workspace isolation |
| **Channel/Platform Parity** | OpenClaw, Moltis, Hermes Agent, LobsterAI, CoPaw | Telegram streaming, Slack message size limits, Discord delivery loops, QQ reconnection, WeCom support |
| **UI/UX Accessibility** | Hermes Agent, OpenClaw, ZeroClaw, Moltis | VoiceOver support, i18n, keyboard shortcuts, screen-reader compatibility |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | NanoBot | Hermes Agent | CoPaw | LobsterAI | Moltis | PicoClaw |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Language** | Python | Rust | Rust | Python | Python | Python | TypeScript (Electron) | Python | Go |
| **Target User** | Power users, devs, multi-channel | Devs, infra teams, production | CLI-first devs, enterprise | Lightweight agent builders | Desktop consumers, Mac users | QwenPaw ecosystem, power users | Knowledge workers, teams | Privacy-focused individuals | Minimalists, embedded |
| **Architecture** | Monolithic, full-stack | Modular, Reborn rewrite | Binary agent runtime | Plugin-based, micro | Desktop + Gateway | Plugin-based, Tauri | Electron desktop | Self-hosted agent | Single binary |
| **Release Maturity** | Frequent, many regressions | Well-structured, stable | Release prep phase | Frequent, clean | Frequent, Windows weak | Moderate, responsive | Efficient, polished | Daily builds, improving | Rare, bugs persist |
| **Key Strength** | Ecosystem breadth, ClawHub | Rust reliability, Reborn design | TUI parity, performance | Lightweight, fast iteration | Desktop UX, MCP support | Strong memory focus | Collaboration features | Simplicity, privacy | Minimalism, low resource |
| **Key Weakness** | Bug backlog, regression rate | New architecture risk | S1 bugs, TUI stability | Multi-agent docs gap | Windows support, accessibility | Memory crashes, Windows browser | Subscription UX | Docker/Podman gaps | Core bugs (PID) unmerged |

**Strategic Observations:**
- **Rust-based projects** (IronClaw, ZeroClaw, PicoClaw) are converging on performance and security as differentiators, but PicoClaw's unresolved critical bug (#2720) undermines its reliability narrative.
- **Desktop-first projects** (Hermes Agent, LobsterAI, Moltis, CoPaw) compete on UX polish and channel integration; Hermes Agent's accessibility gap (#26689) is a notable blind spot.
- **Minimalist projects** (NanoBot, NullClaw, ZeptoClaw) appeal to developers who find OpenClaw overwhelming; NanoBot is the only one with sustained velocity.
- OpenClaw's **dominance is not absolute** — its bug debt creates opportunity for leaner alternatives to capture dissatisfied users.

---

## 6. Community Momentum & Maturity

**Tier 1: Very High Velocity (Rapid Iteration)**
- **OpenClaw** — 500+ daily updates, multiple releases, but carries significant technical debt.
- **IronClaw** — 50 PRs/day, Reborn architecture advancing, security hardening prioritized.
- **ZeroClaw** — 50 PRs/day, release preparation phase with coordinated trackers.
- **CoPaw** — 49 PRs/day, responsive to bugs, memory stability as primary bottleneck.

**Tier 2: High Velocity (Steady Improvement)**
- **NanoBot** — Stable merge rate (18/day), memory and MCP work maturing, API surface stabilizing.
- **Hermes Agent** — Active but slower merge rate (7/day); focus on Windows/Docker/stability fixes.
- **LobsterAI** — Efficient merging (14/16 PRs merged), focused scope (MCP, cowork, shortcuts).

**Tier 3: Moderate Velocity (Incremental)**
- **Moltis** — High issue closure rate but no PRs merged today; Docker/Podman issues are growing concern.
- **PicoClaw** — Low merge velocity (2/10), critical PID bug unresolved despite two fix PRs.
- **NanoClaw** — 9 PRs open, none merged; scheduler/encryption fixes awaiting review.

**Tier 4: Low/Stalled**
- **NullClaw** — Single PR, zero community engagement.
- **ZeptoClaw** — Dependabot only, no human contributions.
- **TinyClaw** — No activity.

**Key Maturity Insight**: The ecosystem is forming a **"healthy core"** of projects (IronClaw, ZeroClaw, NanoBot, CoPaw, LobsterAI) that balance velocity with stability, while OpenClaw dominates mindshare but may be overextending. Rust-based projects are gaining momentum as reliability-critical workloads seek alternatives to Python.

---

## 7. Trend Signals

**1. Multi-Agent Orchestration is the Next Battleground**
- NanoBot (#222, #4179), OpenClaw (#85030), Hermes Agent (#38552), and CoPaw (#3470) all have active requests for supervisor/subagent architectures, inter-agent communication, and permission inheritance. Projects that deliver ergonomic multi-agent tooling will capture the next wave of users moving beyond single-agent use cases.

**2. MCP Standardization Accelerates Adoption**
- Every project except NullClaw and ZeptoClaw has MCP-related activity. LobsterAI's MCP session timeout fix (#2104), NanoBot's reconnect fix (#4171), and PicoClaw's dynamic headers (#2696) indicate the protocol is being hardened for production. MCP is becoming the universal extensibility layer.

**3. Context/ Memory Management is the #1 Reliability Gap**
- CoPaw (compaction failures, vector index explosion), Moltis (session title generation), NanoBot (Dream deduplication), and OpenClaw (transcript migration) all struggle with memory scaling. Users are losing trust in long-running agents. Projects that solve memory at scale (DAG-based compression, lossless compaction, user-excludable system messages) will gain a decisive advantage.

**4. Enterprise Security is a Growing Requirement**
- ZeroClaw (OIDC, pluggable security providers), Hermes Agent (skill_view file disclosure), and PicoClaw (TLS verification) are all responding to enterprise pressure. OpenClaw's operator install policy (#89516) directly addresses supply-chain security. Expect security to become a table-stakes feature for any project targeting organizational deployment.

**5. Rust-based Agents Are Gaining Production Trust**
- IronClaw and ZeroClaw report "resource-light" performance as a differentiator (ZeroClaw #7143 user feedback). Pico

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-04

## 1. Today's Overview

The project remains **highly active** with **33 issues** and **34 pull requests** updated in the last 24 hours. Of those PRs, **18 were merged or closed**, indicating sustained development velocity. No new releases were published today, but the stream of merged features (auth command, web UI refactoring, MCP reconnection, memory compaction) suggests a stable core is being polished. Community engagement is strong, with several long-standing feature requests (multi-agent setups, task-specific model config) still gathering reactions and discussion.

## 2. Releases

*No new releases today.* The last release (v0.1.4) is still the latest. Upcoming release candidates may include the `nanobot auth` command, multi-agent mailbox channel, and web UI runtime event bus.

## 3. Project Progress

**Merged/closed PRs today (most significant):**

| PR | Title | Area |
|----|-------|------|
| [#4171](https://github.com/HKUDS/nanobot/pull/4171) | fix(mcp): reconnect terminated sessions | MCP stability |
| [#4180](https://github.com/HKUDS/nanobot/pull/4180) | fix(qq): send pairing codes for unauthorized C2C users | QQ channel |
| [#4122](https://github.com/HKUDS/nanobot/pull/4122) | feat(multimodel): support webui recording and transcribe with local ASR | WebUI |
| [#3221](https://github.com/HKUDS/nanobot/pull/3221) | feat: add nanobot auth command | Auth / onboarding |
| [#3990](https://github.com/HKUDS/nanobot/pull/3990) | refactor(dream): replace two-phase Dream class with simple cron + process_direct | Memory |
| [#3461](https://github.com/HKUDS/nanobot/pull/3461) | feat: multi-agent mailbox channel plugin | Agent orchestration |
| [#3858](https://github.com/HKUDS/nanobot/pull/3858) | refactor(agent): extract ContextBuilder.build_user_content() as public method | Code quality |
| [#3920](https://github.com/HKUDS/nanobot/pull/3920) | feat(benchmark): add compaction benchmark + optimize consolidator prompt | Memory |
| [#3932](https://github.com/HKUDS/nanobot/pull/3932) | fix(providers): avoid duplicate tool_call_id in stream mode | LLM compatibility |
| [#3952](https://github.com/HKUDS/nanobot/pull/3952) | feat(memory): enhance Dream + Consolidator prompts for MECE long-term memory | Memory deduplication |
| [#3999](https://github.com/HKUDS/nanobot/pull/3999) | fix(agent): prevent runner from exiting while sustained goal is active | Agent loop |
| [#4135](https://github.com/HKUDS/nanobot/pull/4135) | Refactor WebUI runtime state onto event bus | WebUI architecture |
| [#4157](https://github.com/HKUDS/nanobot/pull/4157) | fix(webui): bound startup fetch waits | WebUI reliability |
| [#4174](https://github.com/HKUDS/nanobot/pull/4174) | fix: restore top-level import order | Code hygiene |

**Key advances:**
- **Memory & Archives:** Consolidator prompt optimised, Dream refactored to a single cron-based flow, and MECE‑style deduplication added to reduce bloat.
- **Multi-agent foundation:** A file‑system mailbox channel plugin landed, enabling inter‑agent communication without core changes.
- **WebUI:** Voice recording + local ASR support, runtime state moved to an event bus, and startup fetch timeout handling.
- **Auth:** OAuth device flow and `--auth-key` support allow headless logins without manual API key configuration.

## 4. Community Hot Topics

| Issue/PR | Comments | 👍 | Subject |
|----------|----------|----|---------|
| [#222](https://github.com/HKUDS/nanobot/issues/222) | 10 | 7 | **Multi‑agent support** – user asks for docs/guide on multi‑agent setup |
| [#979](https://github.com/HKUDS/nanobot/issues/979) | 5 | 0 | Funny observation that `rm` restrictions can be bypassed |
| [#1022](https://github.com/HKUDS/nanobot/issues/1022) | 4 | 3 | **Long‑running tasks fail** – "Starting execution now" but nothing happens |
| [#80](https://github.com/HKUDS/nanobot/issues/80) | 4 | 0 | Lightweight memory retrieval (BM25/TF‑IDF) to reduce token use |
| [#912](https://github.com/HKUDS/nanobot/issues/912) | 3 | 3 | **Task‑specific model configuration** (conversational vs tool use vs browser) |
| [#954](https://github.com/HKUDS/nanobot/issues/954) | 3 | 1 | **Progress streaming leaks internal tool calls** to user chat |
| [#97](https://github.com/HKUDS/nanobot/issues/97) | 1 | 6 | **Core architecture RFC** (memory, security, testing) |

**Analysis:** The community is clearly demanding **multi-agent orchestration** (both setup and docs) and **task‑specific model routing**. The recent mailbox channel plugin (#3461) is a direct step toward the first. The second (#912) remains open with 3 👍 and a detailed proposal. The architecture RFC (#97) has strong upvote support and likely influenced the recent memory and event‑bus refactoring.

## 5. Bugs & Stability

**Reported today or recently updated (last 24h):**

| ID | Severity | Description | Fixed by PR |
|----|----------|-------------|-------------|
| [#4168](https://github.com/HKUDS/nanobot/issues/4168) | High | MCP server unreachable after random time – `McpError: Session terminated` | [#4171](https://github.com/HKUDS/nanobot/pull/4171) (merged today) |
| [#4178](https://github.com/HKUDS/nanobot/issues/4178) | Low | WebUI missing keyboard shortcut for new chat | [#4181](https://github.com/HKUDS/nanobot/pull/4181) (open) |
| [#954](https://github.com/HKUDS/nanobot/issues/954) (stale) | Medium | Progress streaming leaks internal tool calls to user chat | Not yet fixed |
| [#1022](https://github.com/HKUDS/nanobot/issues/1022) (stale) | High | Long‑running tasks stall after "Starting execution now" | Not yet fixed |
| [#937](https://github.com/HKUDS/nanobot/issues/937) (stale) | High | Too many hallucinations in `exec` tool across SOTA LLMs | Not yet fixed |
| [#935](https://github.com/HKUDS/nanobot/issues/935) (stale) | Medium | Remote MCP URL (Streamable HTTP) times out with `asyncio.CancelledError` | Not yet fixed |
| [#896](https://github.com/HKUDS/nanobot/issues/896) (stale) | Medium | Telegram/Discord media files never cleaned up – unbounded disk growth | Not yet fixed |
| [#143](https://github.com/HKUDS/nanobot/issues/143) (stale) | High | Filesystem tools ignore `restrict_to_workspace` – security bypass | Not yet fixed |

**Today’s fix PRs that address existing bugs:** [#4171 (MCP reconnect)](https://github.com/HKUDS/nanobot/pull/4171), [#3999 (sustained goal exit)](https://github.com/HKUDS/nanobot/pull/3999), [#3932 (duplicate tool_call_id)](https://github.com/HKUDS/nanobot/pull/3932), [#4157 (webUI fetch timeout)](https://github.com/HKUDS/nanobot/pull/4157).

## 6. Feature Requests & Roadmap Signals

**Opened/updated today with strong community backing:**

- **[#4179](https://github.com/HKUDS/nanobot/issues/4179): Native Agent-to-Agent (A2A) Orchestration** – proposes a supervisor‑researcher‑writer architecture within a shared memory bus. This builds on the mailbox channel (#3461) and would likely appear in a v0.2 release.
- **[#4178](https://github.com/HKUDS/nanobot/issues/4178): Add Cmd/Ctrl+Shift+O shortcut for new chat** – small UX improvement, already has a pending PR (#4181).
- **[#4182](https://github.com/HKUDS/nanobot/pull/4182): Bocha web search provider** – adds a Chinese search API provider (used by DeepSeek).

**Stale but high-impact requests:**

| Issue | 👍 | Feature |
|-------|----|---------|
| [#97](https://github.com/HKUDS/nanobot/issues/97) | 6 | Core architecture improvements (memory, security, testing) |
| [#143](https://github.com/HKUDS/nanobot/issues/143) | 4 | Filesystem security (restrict_to_workspace enforcement) |
| [#1011](https://github.com/HKUDS/nanobot/issues/1011) | 4 | Mattermost channel support |
| [#912](https://github.com/HKUDS/nanobot/issues/912) | 3 | Task‑specific model configuration |
| [#240](https://github.com/HKUDS/nanobot/issues/240) | 2 | SimpleX Chat channel |
| [#936](https://github.com/HKUDS/nanobot/issues/936) | 0 | Multi‑tenant gateway |

**Prediction for next release:** Memory compaction (Dream/Consolidator improvements) and MCP stability are likely to land. The new auth command and mailbox channel are strong candidates for a minor release. A2A orchestration may be deferred to v0.2.

## 7. User Feedback Summary

- **Satisfaction:** The clean, lightweight architecture continues to be praised (“kept under 4k lines” – #97). The rapid pace of fixes and features (auth, webUI improvements) is well received.
- **Pain points:**
  - **Exec tool hallucinations** (#937) – a major blocker for users evaluating the framework.
  - **Long‑running task stalling** (#1022) – breaks real‑world usage like scraping and data processing.
  - **Security concerns** – filesystem tools bypass workspace restrictions (#143), media files never cleaned (#896).
  - **Multi‑agent absence** – repeated requests for documentation and guided setup (#222, #1006, #1012).
  - **Session model** – single session per channel discourages multi‑user or threaded conversations (#1010, #976).
- **Use cases:** Scraping, automation, personal assistant (Telegram/WhatsApp), skill creation. Users appreciate the flexibility of MCP tools but suffer from connection timeouts (#935) and provider‑level bugs (duplicate tool_call_id).

## 8. Backlog Watch

These open issues have been **unanswered or unresolved for months** despite significant community interest, and would benefit from maintainer attention:

| Issue | Age | Last Update | Activity | Status |
|-------|-----|-------------|----------|--------|
| [#222](https://github.com/HKUDS/nanobot/issues/222) | ~4 months | 2026-06-03 | 10 comments, 7 👍 | No official response on multi‑agent docs |
| [#97](https://github.com/HKUDS/nanobot/issues/97) | ~4 months | 2026-06-03 | 1 comment, 6 👍 | Architecture RFC – no maintainer reply |
| [#143](https://github.com/HKUDS/nanobot/issues/143) | ~4 months | 2026-06-03 | 2 comments, 4 👍 | Security – filesystem bypass not acknowledged |
| [#912](https://github.com/HKUDS/nanobot/issues/912) | ~3.5 months | 2026-06-03 | 3 comments, 3 👍 | Task‑specific model config – no milestone |
| [#1011](https://github.com/HKUDS/nanobot/issues/1011) | ~3.5 months | 2026-06-03 | 0 comments, 4 👍 | Mattermost channel – no response |
| [#935](https://github.com/HKUDS/nanobot/issues/935) | ~3.5 months | 2026-06-03 | 0 comments, 1 👍 | MCP timeout – reported but no progress |
| [#896](https://github.com/HKUDS/nanobot/issues/896) | ~3.5 months | 2026-06-03 | 0 comments | Media cleanup – still open |

The maintainers (dominated by @chengyongru and @Re-bin) are actively merging PRs, but long‑standing feature requests and bugs

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-04

## Today's Overview

The project remains highly active with **50 issues** and **50 pull requests** updated in the last 24 hours, reflecting a vibrant community. Of these, **7 issues were closed** and **7 PRs were merged/closed**, indicating steady progress on bug fixes and features. The open issue count (43) suggests a healthy backlog of community-driven improvements and reports. No new releases were published today, but the frequent updates to PRs and issues point to ongoing development velocity, with particular focus on Windows stability, MCP integration, and security hardening.

## Releases

No new releases were published on 2026-06-04.

## Project Progress

Today saw **7 merged/closed pull requests** addressing several key areas:

- **TUI/CLI stability** – PR [#35992](https://github.com/NousResearch/hermes-agent/pull/35992) (merged) fixes ANSI corruption in long-session transcript resumption in TUI mode, a long-standing intermittent display bug.
- **Docker/Unraid compatibility** – PR [#38098](https://github.com/NousResearch/hermes-agent/pull/38098) and PR [#38655](https://github.com/NousResearch/hermes-agent/pull/38655) improve UID mapping support for low-numbered users (e.g., Unraid’s 99:100), fixing permission issues on Docker containers.
- **Windows gateway workspace** – PR [#35035](https://github.com/NousResearch/hermes-agent/pull/35035) (merged) anchors the detached gateway’s working directory to `HERMES_HOME` on Windows, resolving parity issues between startup and runtime paths.
- **Docker tests** – PR [#38646](https://github.com/NousResearch/hermes-agent/pull/38646) (open, but fixes CI) loosens a TTY width assertion that was failing on headless CI runners, unblocking the `build-amd64` pipeline.

These changes demonstrate ongoing work to harden Hermes Agent across different OS and container environments.

## Community Hot Topics

The most actively discussed issues today reflect real user pain points across platforms:

- **Accessibility** – Issue [#26689](https://github.com/NousResearch/hermes-agent/issues/26689) (“Accessibility improvements for blind VoiceOver users”) leads with **8 comments**. The user describes a totally blind experience with VoiceOver on macOS, highlighting the gap between Hermes’ powerful backend and a screen-reader-friendly UX. This signals a need for inclusive design in the CLI/TUI layers.

- **macOS file descriptor limit** – Issue [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) (“Gateway hits macOS fd limit (256)”) has **3 comments** and describes how gateway processes with multiple MCP servers routinely exceed the default macOS soft limit of 256 file descriptors, causing `OSError: Too many open files`. The user provides detailed diagnostics and a workaround suggestion.

- **Windows update bricking** – Issue [#37881](https://github.com/NousResearch/hermes-agent/issues/37881) (“`hermes update` bricks the install on Windows”) has **3 comments** (and 1 👍). The user reports that the update process leaves the venv without `pyvenv.cfg`, causing `ModuleNotFoundError: hermes_cli` on subsequent runs. This is a P1 bug affecting Windows users.

- **QQBot gateway heartbeat failure** – Issue [#24357](https://github.com/NousResearch/hermes-agent/issues/24357) (“QQBot gateway can stop heartbeating after reconnect”) has **3 comments** and 2 👍. The bot stops responding in QQ after prolonged operation due to a session timeout loop.

Other active items include PRs adding ModelScope provider support ([#38648](https://github.com/NousResearch/hermes-agent/pull/38648)) and a post_tool_call hook for circuit breaker MCP resilience ([#38657](https://github.com/NousResearch/hermes-agent/pull/38657)).

## Bugs & Stability

Several critical bugs were reported today. Ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **P0 (Critical)** | [#38643](https://github.com/NousResearch/hermes-agent/issues/38643) | `skill_view` name traversal allows file disclosure outside trusted skills directory (security advisory). | No fix PR yet. |
| **P1 (High)** | [#38652](https://github.com/NousResearch/hermes-agent/issues/38652) | `parse_available_output_tokens_from_error()` misses OpenRouter/Nous “output cap” format, causing infinite auto-reset loop. | Proposed fix in PR [#38644](https://github.com/NousResearch/hermes-agent/pull/38644). |
| **P1 (High)** | [#38471](https://github.com/NousResearch/hermes-agent/issues/38471) | Hermes Desktop skips onboarding, picks random OAI-API key, and offers no way to configure credentials. | No fix PR yet. |
| **P1 (High)** | [#37881](https://github.com/NousResearch/hermes-agent/issues/37881) | Windows `hermes update` bricks install (venv corruption). | No fix PR yet, but duplicate/reporting thread. |
| **P2 (Medium)** | [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) | macOS fd limit hit by gateway with multiple MCP profiles. | No fix PR yet; workaround discussed. |
| **P2 (Medium)** | [#38580](https://github.com/NousResearch/hermes-agent/issues/38580) | `requests==2.33.0` missing `_types.py` on aarch64, crashes on Jetson ARM. | No fix PR yet. |
| **P2 (Medium)** | [#38638](https://github.com/NousResearch/hermes-agent/issues/38638) | Own-policy adapters (QQBot) fail open without allowlists – CVSS 9.1. Fix PR [#38639](https://github.com/NousResearch/hermes-agent/pull/38639) open. | Yes, PR #38639. |
| **P2 (Medium)** | [#38618](https://github.com/NousResearch/hermes-agent/issues/38618) | Update reports 7 commits behind, remains on v0.15.1 when v0.15.2 exists – version detection mismatch. | No fix PR yet. |
| **P2 (Medium)** | [#38407](https://github.com/NousResearch/hermes-agent/issues/38407) | Windows Desktop app fails after update due to incomplete git checkout and FS cache mismatch. | No fix PR yet. |

Notable regression fixes: PR [#38644](https://github.com/NousResearch/hermes-agent/pull/38644) addresses DeepSeek streaming credential loss and reasoning-only infinite hangs; PR [#38631](https://github.com/NousResearch/hermes-agent/pull/38631) fixes persistent “needs-input” indicator in the desktop UI.

## Feature Requests & Roadmap Signals

Today’s feature requests indicate strong user demand for:

- **Accessibility** – [#26689](https://github.com/NousResearch/hermes-agent/issues/26689) (VoiceOver support) and [#38007](https://github.com/NousResearch/hermes-agent/issues/38007) (system tray background running) are both non-critical (P3) but have community support.
- **Persistent workspace memory** – [#38552](https://github.com/NousResearch/hermes-agent/issues/38552) proposes automated workspace memory so the agent remembers directory purposes across sessions, reducing token waste. This complements existing memory tools.
- **Profile switching in desktop** – [#37713](https://github.com/NousResearch/hermes-agent/issues/37713) wants remote gateway profile switching from the UI, which would enhance multi-profile workflows.
- **Platform-specific features** – WeCom streaming (PR [#38641](https://github.com/NousResearch/hermes-agent/issues/38641)), ModelScope provider (PR [#38648](https://github.com/NousResearch/hermes-agent/pull/38648)), and MiniMax vision fast-path (PR [#38642](https://github.com/NousResearch/hermes-agent/pull/38642)) show expansion of provider and platform support.

Given the high activity around plugin hooks (PR [#38656](https://github.com/NousResearch/hermes-agent/pull/38656) adds `post_tool_call` dispatch), the next minor version may include circuit breaker resilience for MCP servers and richer plugin extensibility. The security fixes for QQBot gateway (#38638/#38639) are likely to be fast-tracked.

## User Feedback Summary

Users are reporting both satisfaction with Hermes’ capabilities and frustration with stability on non-ideal setups:

- **VoiceOver user praises backend power but criticizes UX** – “Hermes has an extremely powerful backend and agent ecosystem, but the current UX is very difficult for screen-reader users.” (Issue #26689)
- **Windows users feel the pain** – Multiple reports of `hermes update` breaking installations (#37881, #38407), phantom directories (#30081), and Docker terminal cwd leaks (#38156) indicate Windows support needs additional attention.
- **MCP integration friction** – While MCP is powerful, users hit authorization issues (#37792), false “failed” status (#38650), and fd limits (#30230). The circuit breaker PR (#38657) aims to improve resilience.
- **Security concerns raised by community** – Two security issues (skill_view traversal #38643, QQBot open gateway #38638) were filed with detailed CVSS scores, suggesting user vigilance around data exposure.
- **Cron silent failures** – A user reports that cron agents lose memory write capability without error (#38647), undermining trust in scheduled workflows.

Overall sentiment is constructive: users are actively helping diagnose, document workarounds, and propose solutions.

## Backlog Watch

The following open items have been dormant or lack maintainer response but are important:

- **Issue #17986** (closed, but background issue remains – HTTP 400 on first turn for Fireworks endpoint – closed 2026-06-03 without clear resolution).
- **Issue #24357** (QQBot heartbeat loop, open since May 12, 3 comments, no fix PR). Still reproducing in Docker.
- **Issue #26689** (Accessibility, open since May 16, 8 comments – maintainer has not responded yet).
- **Issue #29418** (Nous inference streaming timeout on agent-sized payloads, open since May 20, 2 comments, no fix PR). The workaround is non-streaming, which defeats purpose.
- **PR #35277** (i18n Chinese localization, open since May 30, clean branch – awaiting review or merge). With over 16 files changed, this is a significant but uncontroversial feature.
- **Issue #38580** (aarch64 wheel missing `_types.py`, open since June 4, no maintainer response yet – blocks Jetson users).

These items would benefit from maintainer triage or community contributors picking them up.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-04

## 1. Today’s Overview
PicoClaw’s activity over the last 24 hours shows steady maintenance momentum. Four open issues were updated (all still open), and ten pull requests received updates. Two PRs were merged or closed: a security bump for Go (`#2997`) and a fix for configurable TLS verification in the MQTT channel (`#2899`). No new releases were published. The project remains focused on bug fixes — particularly around singleton PID validation, channel configuration merging, and tool-call streaming — while a long-running enhancement for MCP dynamic headers continues to mature. Community engagement is moderate, with the most active threads addressing streaming support and the persistent PID crash loop.

## 2. Releases
**None** — no releases were published today.

## 3. Project Progress
Two pull requests were merged or closed today:
- **#2899** (closed) — `fix: add configurable TLS verification for MQTT channel`  
  Previously, `InsecureSkipVerify` was hardcoded to `true`. This fix introduces a `TLSSkipVerify` config field (default `false`) so users can opt‑in for self‑signed certificates. *(sipeed/picoclaw PR #2899)*
- **#2997** (closed) — `fix(deps): bump go from 1.25.10 to 1.25.11 (GO-2026-5039)`  
  Addresses a security vulnerability in `net/textproto` where header names in error messages were not escaped. *(sipeed/picoclaw PR #2997)*

Additionally, several open PRs saw renewed activity:
- **#2813** and **#2955** — competing fixes for the stale PID identity check (both updated today).
- **#2957** — fix for tool_calls being dropped during streaming (updated).
- **#2992** — fix for session alias promotion causing old messages in new Web UI sessions.
- **#2995** — docs update adding release highlights v0.2.5–v0.2.9 to the README.
- **#2996** — error handling improvements for `json.Marshal` in exec tool responses.

## 4. Community Hot Topics
The most active discussions (by comment count) are:

- **Issue #2404 – [Feature] Add in config to send streaming HTTP request**  
  *11 comments, 1 👍*  
  Request to support a `"streaming": true` config option for LLM requests, mirroring the OpenAI Python client’s `stream=True`. The proposal has broad interest and is a prerequisite for real‑time chat experiences.  
  *(sipeed/picoclaw Issue #2404)*

- **Issue #2720 – [BUG] Singleton PID check doesn't verify process identity — stale PID causes crash loop**  
  *8 comments, priority: high*  
  A long‑standing bug where the gateway crashes if the PID file contains a PID reused by an unrelated process (e.g., `systemd‑resolved`). Two separate fix PRs (#2813 and #2955) exist but remain unmerged.  
  *(sipeed/picoclaw Issue #2720)*

- **PR #2813 – fix(pid): (updated) verify gateway identity before blocking startup on stale PID**  
  *Open since May 7, updated today* — together with #2955, these duplicate‑effort PRs signal that the community considers this a critical fix.  
  *(sipeed/picoclaw PR #2813)*

- **PR #2696 – feat(mcp): support per‑request dynamic headers from channel context**  
  An enhancement to allow channels to forward HTTP headers to MCP servers per‑request. While not heavily commented, it has been active since April 28 and represents a significant architecture expansion.  
  *(sipeed/picoclaw PR #2696)*

**Underlying needs**: Users are demanding both reliability (PID crash loop, tool_calls drop, channel config merging) and expressiveness (native streaming, MCP header forwarding). The PID bug in particular is a frustration that two contributors independently tried to fix.

## 5. Bugs & Stability
Three open bugs were updated in the last 24 hours, each with different severity levels:

| Bug | Severity | Summary | Fix PR Exists? |
|-----|----------|---------|----------------|
| **#2720** – Stale PID causes crash loop | 🔴 **High** | Gateway fails to start when PID file holds a PID reused by another process. Two fix PRs present (#2813, #2955). | ✅ (unmerged) |
| **#2958** – Tool_calls dropped during consecutive requests via pico channel | 🟡 **Medium** | Subsequent `tool_calls` are not delivered to the UI after the first request. | ✅ (#2957, open) |
| **#2954** – 32‑bit Android not supported | 🟢 **Low** | PicoClaw fails on 32‑bit Android systems (e.g., Termux). No fix PR yet. | ❌ |

Additionally, a security vulnerability was patched today in PR #2997 (Go bump). No new regressions were reported today.

## 6. Feature Requests & Roadmap Signals
- **#2404 – Streaming HTTP request config** — This is the most‑requested feature by comment volume. It would bring PicoClaw in line with standard LLM client APIs. Likely to be included in the next release, possibly after the upcoming v0.3.x cycle.
- **#2696 – MCP per‑request dynamic headers** — Already in PR form and addresses a clear use case: injecting authentication or context‑specific headers into MCP tool calls from channel metadata. This is a strong candidate for the next minor release.
- **#2954 – 32‑bit Android support** — While low‑priority due to limited demand, the existence of the bug indicates the community is trying to run PicoClaw on a wider range of devices (Termux on older phones/tablets).

## 7. User Feedback Summary
- **Pain point**: The singleton PID check is fragile; multiple users have reported “gateway fails to start” after crashes or system reboots (#2720). This is the most visible reliability concern.
- **Pain point**: Real‑time streaming is not natively configurable — users must work around the lack of a `streaming` flag (#2404).
- **Pain point**: Tool‑calling workflows break when using the pico WebSocket channel consecutively; `tool_calls` are silently dropped after the first invocation (#2958).
- **Pain point**: Configuration merging between `config.json` and `.security.yml` disables channels; users must redundantly set `enabled: true` in the security file (#2956, PR exists but not merged).
- **Use cases**: LLM backend integration with streaming, multi‑platform deployment (including Android Termux), and tool‑augmented conversational agents.
- **Satisfaction**: Community engagement is positive — contributors are proactively proposing fixes rather than just filing issues. The rapid submission of two independent PID‑check fixes shows strong desire for stability.

## 8. Backlog Watch
The following issues and PRs are stale (no maintainer action for several weeks) yet carry significant importance:

- **Issue #2720** — **High‑priority PID bug** (created Apr 30, last updated Jun 4). Two fix PRs exist (#2813 and #2955) but neither has been reviewed or merged. Without a maintainer decision, the crash‑loop problem persists.
- **PR #2813** — **fix(pid)** (created May 7, stale label). Also updated today. A key blocker for gateway reliability.
- **PR #2696** — **feat(mcp)** (created Apr 28, stale). A significant architectural enhancement that has been awaiting review for over a month.
- **Issue #2954** — **32‑bit Android** (created May 27, stale). No response from maintainers. May need a decision on whether to support or document a limitation.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-04

---

## 1. Today's Overview

NanoClaw saw low-to-moderate activity over the past 24 hours with one open issue and nine open pull requests updated. No new releases were published, and no PRs were merged or closed. The majority of activity centered on bug fixes across scheduling, service startup, container runner, Slack integration, and skill management, along with a new container skill for hybrid markdown search. The project remains in a stable, iterative development phase with contributors actively submitting fixes but awaiting maintainer review and merging.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

No pull requests were merged or closed today. However, the following nine PRs were updated and are currently open, indicating ongoing work toward improving NanoClaw’s reliability and feature set:

- **New Skill**: [#2683 – `feat(skills): add QMD container skill for hybrid markdown search`](https://github.com/nanocoai/nanoclaw/pull/2683) – adds a container skill for local hybrid search (BM25 + vector).  
- **Scheduling fixes (3 PRs)**:
  - [#2679 – `fix(scheduling): surface permanently-failed scheduled tasks to the user`](https://github.com/nanocoai/nanoclaw/pull/2679)  
  - [#2678 – `fix(scheduling): re-arm recurrence when a run fails permanently`](https://github.com/nanocoai/nanoclaw/pull/2678)  
  - [#2677 – `fix(scheduling): retry pre-task script once on failure with diagnostics`](https://github.com/nanocoai/nanoclaw/pull/2677)  
- **Service startup fix**: [#2681 – `fix(service): skip linger on per-home-encrypted systems`](https://github.com/nanocoai/nanoclaw/pull/2681) – addresses issue #2680.  
- **Proxy / networking fix**: [#2676 – `fix(container-runner): add NO_PROXY to bypass OneCLI proxy for local services`](https://github.com/nanocoai/nanoclaw/pull/2676)  
- **Slack integration fix**: [#2675 – `fix(add-slack): patch Slack 3000-char section-block limit`](https://github.com/nanocoai/nanoclaw/pull/2675)  
- **Skill update tooling**: [#2682 – `fix(update-skills): skip v1-only skill branches`](https://github.com/nanocoai/nanoclaw/pull/2682)  
- **Permission inheritance**: [#2605 – `feat: inherit parent agent permissions via OneCLI`](https://github.com/nanocoai/nanoclaw/pull/2605) (opened May 24, still open).

The breadth of fixes suggests the project is actively polishing the scheduling system, container runtime, Slack adapter, and service lifecycle.

---

## 4. Community Hot Topics

The most active issue and PRs in the last 24 hours are:

- **Issue [#2680 – Service doesn't start at boot when linger is enabled on an encrypted home directory](https://github.com/nanocoai/nanoclaw/issues/2680)**  
  - 1 thumbs-up, 0 comments. The issue describes a real-world pain point for users with per-user encrypted home directories (ecryptfs, fscrypt, etc.). The agent’s systemd user service silently fails to start at boot even when `linger` is enabled. The underlying need is robust systemd integration across varied Linux encryption setups. A fix PR (#2681) has already been submitted.

- **PR [#2605 – `feat: inherit parent agent permissions via OneCLI`](https://github.com/nanocoai/nanoclaw/pull/2605)**  
  - Open since May 24, with no comments recorded. This is a feature PR aimed at simplifying agent permission management by inheriting from a parent agent. Its lack of recent discussion may indicate maintainer bottleneck or complexity.

- **PR [#2675 – Slack 3000-char section-block limit fix](https://github.com/nanocoai/nanoclaw/pull/2675)**  
  - Addresses a critical usability issue where long messages are silently dropped by Slack. Community members using Slack integration would be directly affected.

The community’s top concerns are **systemd service reliability on encrypted systems** and **Slack message size limits**, both of which are being addressed via PRs.

---

## 5. Bugs & Stability

One bug report was updated in the last 24 hours, ranked as **medium** priority:

| Issue | Summary | Severity | Fix PR? |
|-------|---------|----------|---------|
| [#2680](https://github.com/nanocoai/nanoclaw/issues/2680) | Service doesn't start at boot when linger is enabled on encrypted home directory | Medium | Yes: [#2681](https://github.com/nanocoai/nanoclaw/pull/2681) |

In addition, multiple open fix PRs address latent stability issues:

- **Scheduling module**:  
  - Tasks failing permanently are not surfaced to the user (PR #2679).  
  - Recurrence is not re-armed after a failure (PR #2678).  
  - Pre-task scripts are not retried on failure (PR #2677).  
- **Container runner**: `NO_PROXY` missing for local services, causing proxy interference (PR #2676).  
- **Slack adapter**: Messages exceeding 3000 characters are rejected entirely (PR #2675).  

No crashes or regressions were reported. The overall stability posture is good, with bugs being quickly patched via PR submissions.

---

## 6. Feature Requests & Roadmap Signals

The following PRs indicate likely upcoming features:

- **Container skill ecosystem**: [#2683 adds a QMD container skill](https://github.com/nanocoai/nanoclaw/pull/2683) for hybrid markdown search. This follows the pattern of the `container skill` model and suggests NanoClaw is expanding its skill marketplace.  
- **Permission inheritance**: [#2605](https://github.com/nanocoai/nanoclaw/pull/2605) would allow agents to inherit permissions from a parent agent via OneCLI, a significant simplification for multi-agent deployments.  
- **Skill versioning**: [#2682](https://github.com/nanocoai/nanoclaw/pull/2682) introduces v2 compatibility checks for skill branches, signaling a commitment to backward compatibility and a structured skill update pipeline.

If merged, these features could appear in the next minor or patch release. The permission inheritance feature (#2605) has been pending for over a week and may be the most impactful addition.

---

## 7. User Feedback Summary

Reported user pain points in the last 24 hours:

1. **Encrypted home directory startup failure** (issue #2680) – Users with non-LUKS per-user encryption cannot rely on the agent starting at boot, even with linger enabled.  
2. **Slack integration message loss** (PR #2675) – Long Slack messages are silently dropped, leading to frustration and data loss.  
3. **Scheduling opacity** (PR #2678, #2679) – Failed scheduled tasks are not re-armed and are invisible to users, reducing trust in the task scheduler.  
4. **Proxy complications** (PR #2676) – Users behind a corporate proxy (OneCLI) cannot reach local services from the container runner.  

No explicit satisfaction signals were recorded, but the prompt submission of fix PRs suggests a responsive contributor community.

---

## 8. Backlog Watch

Notable items that may require maintainer attention:

- **PR [#2605 – `feat: inherit parent agent permissions via OneCLI`](https://github.com/nanocoai/nanoclaw/pull/2605)**  
  - Opened May 24, 2026. Last updated June 3. No reviewer comments or approvals. This is a feature that could significantly improve agent management but appears to be stalled.

- **Issue [#2680](https://github.com/nanocoai/nanoclaw/issues/2680)** has a fix PR (#2681) already submitted; expediting review would resolve a clear user pain point.

No other long-unanswered issues were visible in the last 24h window. The project appears to be in a healthy state with active contributions, though merging velocity could be improved to reduce backlog.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-04

## 1. Today's Overview
The NullClaw repository recorded zero new issues and no merged or closed pull requests in the past 24 hours. A single open pull request (#946) was updated, but received no comments or reactions, indicating minimal community engagement. No new releases were published. Overall project activity remains very low, with no visible maintenance or development acceleration.

## 2. Releases
*No new releases to report.*

## 3. Project Progress
**Merged/Closed PRs:** None today.

**Open (still in review):**  
- **PR #946** ([link](https://github.com/nullclaw/nullclaw/pull/946)) – `fix(agent): filter tools in system prompt text by tool_filter_groups`  
  *Author: vernonstinebaker | Created: 2026-06-03 | Updated: 2026-06-03*  
  This PR introduces `filterToolsForPromptText` to exclude tools from the text-based system prompt unless they belong to the `always` filter group. Dynamic-group MCP tools are omitted from text but their schemas remain available via native API tool-calling when turn keywords match. It also removes stale `Paradigm` references. The change aims to reduce prompt bloat while preserving full tool functionality through API channels.

## 4. Community Hot Topics
No issues or PRs attracted comments or reactions today. The only active PR (#946) has zero reactions and zero comments, suggesting either low community awareness or that the change is uncontroversial. Underlying need: improving system prompt efficiency for agent tool usage without sacrificing API-level tool availability.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The project remains stable with no open issues.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, PR #946 signals ongoing work toward finer-grained control of tool inclusion in prompts, which may indicate a broader roadmap direction: optimizing prompt construction for agents that mix built-in and MCP tools. Future versions may expand filter group configurability or add user-facing settings for tool visibility.

## 7. User Feedback Summary
No user feedback (comments, reactions, or issue descriptions) was recorded today. The absence of new issues or discussions suggests either satisfaction with the current state or low usage/visibility of the project.

## 8. Backlog Watch
No long-unanswered issues or PRs are currently blocking progress. The single open PR (#946) has been awaiting review for only one day, so no maintainer attention lag is apparent.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-06-04

## 1. Today's Overview
IronClaw saw very high activity over the past 24 hours, with **27 issues updated** (19 open, 8 closed) and **50 PRs updated** (21 open, 29 merged/closed). A new minor release **v0.29.1** shipped, adding temperature control to the Responses API and fixing channel conversation history scoping. The bulk of work continues on the **Reborn** architecture – multiple PRs landed for Slack integration, trigger infrastructure hardening, and capability-surface safety. Several critical bugs surfaced around Reborn tool visibility and context management, with corresponding fix PRs in progress.

## 2. Releases
**ironclaw-v0.29.1** (2026-06-04)  
- **Added:** `plumb temperature through Responses API` ([PR #3641](https://github.com/nearai/ironclaw/pull/3641))  
- **Fixed:** `scope v1 history for channel conversations` ([PR #4320](https://github.com/nearai/ironclaw/pull/4320))  
- **CI/Release:** Added WeCo to the release pipeline  

No breaking changes or migration notes were indicated.

## 3. Project Progress
- **Slack integration** advanced significantly:  
  - Slack ProductAdapter MVP with preconfigured credentials (Issue #3857 closed)  
  - Slack personal binding service, WebUI OAuth flow, and pairing flow (PRs #4422, #4423, #4430)  
  - Slack host-beta route wired into Reborn serve (PR #4418 merged)  
- **Reborn workflow layer** matured:  
  - ProductWorkflow and InboundTurnService facade (Issue #3280 closed)  
  - Local dev runtime scope now bound to run actor (PR #4412 merged)  
  - Read-only automations WebUI API added (PR #4380 merged)  
- **Security & safety**:  
  - Zeroize injected HTTP credential material across carriers (Issue #4222 closed)  
  - Capability surface + safety gating — fail-closed injection scan (Issue #4351 closed)  
  - Consolidate duplicated PKCE math into `ironclaw_common` (Issue #4215 closed)  
- **Context handling**:  
  - Context-overflow recovery now applies `ShrinkContext` properly (Issue #4310 closed)  
  - Compaction summary write lifecycle fixed to not block retries (Issue #4309 closed)  
- **Trigger infrastructure**:  
  - PR 18.5a: type-sealed trusted trigger ingress (PR #4406 merged)  
  - PR18.7: trigger poller full-path integration test (PR #4415 merged)  
- **WebUI**:  
  - Fix live projection cursor resume (PR #4417 merged)  
- **Other**:  
  - Subagent completion observer delivery fixed (PR #4413 open)  
  - Loop capability validation hardened (PR #4414 open)  

## 4. Community Hot Topics
- **Issue #3857** ([link](https://github.com/nearai/ironclaw/issues/3857)) – *Slack ProductAdapter MVP* (6 comments) – Core team discussion on preconfigured credentials and Reborn routing; now closed.  
- **Issue #3280** ([link](https://github.com/nearai/ironclaw/issues/3280)) – *ProductWorkflow and InboundTurnService facade* (5 comments) – Finalized after weeks of work; a key Reborn milestone.  
- **Issue #4424** ([link](https://github.com/nearai/ironclaw/issues/4424)) – *Reborn: `builtin.spawn_subagent` advertised but absent from structured tools* (3 comments) – Open bug causing models to loop; high attention.  
- **Issue #4376** ([link](https://github.com/nearai/ironclaw/issues/4376)) – *Harden HTTP credential carriers* (2 comments) – Follow-up design discussion after a security fix.  

## 5. Bugs & Stability
*Ranked by severity (critical → minor)*

- **Critical – `builtin.spawn_subagent` invisible to model** ([#4424](https://github.com/nearai/ironclaw/issues/4424)): Advertised in surface text but missing from structured tools array. No fix PR yet, but #4414 (loop capability validation) may help.  
- **High – `builtin.http` context bomb** ([#4425](https://github.com/nearai/ironclaw/issues/4425)): 1.2 MB output per fetch, no HTML stripping or size cap. No fix PR.  
- **High – Loop exit reason invisible** ([#4427](https://github.com/nearai/ironclaw/issues/4427)): `LoopFailureKind` never logged; operators cannot debug loop termination.  
- **High – Prompt bundle rebuild waste** ([#4429](https://github.com/nearai/ironclaw/issues/4429)): Identity files re-read on every model call.  
- **High – `builtin.skill_list` unbounded** ([#4428](https://github.com/nearai/ironclaw/issues/4428)): Returns 14 KB for 31 skills with no pagination.  
- **High – Parent loop tool surface AllowAll** ([#4426](https://github.com/nearai/ironclaw/issues/4426)): `interactive_tools` profile ignored, lifecycle tools exposed in chat.  
- **Medium – Trigger `CompleteAfterFirstFire` never consulted** ([#4420](https://github.com/nearai/ironclaw/issues/4420)): Triggers re-fire forever.  
- **Medium – Stale PID file prevents startup** ([#4400](https://github.com/nearai/ironclaw/issues/4400)): Production crash loop.  
- **Low – `/model` returns unusable display names** ([#4377](https://github.com/nearai/ironclaw/issues/4377)): Names like “GPT OSS 120B” cannot be used to switch models.  
- **Low – Nightly E2E failure** ([#4108](https://github.com/nearai/ironclaw/issues/4108)): Auto-reported, no human response yet.

## 6. Feature Requests & Roadmap Signals
- **Default OAuth account per provider** ([#4382](https://github.com/nearai/ironclaw/issues/4382)): Once authenticated, OAuth gate should never re-fire. Likely next patch.  
- **Canonical Reborn identity resolver** ([#4381](https://github.com/nearai/ironclaw/issues/4381)): Needed for stable user binding.  
- **Model-visible capability selection for tool-count limits** ([#4407](https://github.com/nearai/ironclaw/issues/4407)): Reborn surface may exceed provider limits; design task.  
- **Python E2E cron trigger scenario** ([#4432](https://github.com/nearai/ironclaw/issues/4432)): Blocked on production profile wiring.  
- **Regression test: every visible capability must be callable** ([#4431](https://github.com/nearai/ironclaw/issues/4431)): Preventive test after #4424.  
- **Migrate read-only CLI commands to Reborn** ([PR #4379](https://github.com/nearai/ironclaw/pull/4379)): In progress.  
- **WebUI v2 quality-of-life: per-thread state store + sidebar pin marker** ([PR #4419](https://github.com/nearai/ironclaw/pull/4419)): Groundwork for live thread state.  

## 7. User Feedback Summary
- **Pain point – Model display names broken** ([#4377](https://github.com/nearai/ironclaw/issues/4377)): User cannot switch models with NEAR AI provider because `/model` returns non-identifier names.  
- **Pain point – Stale PID file** ([#4400](https://github.com/nearai/ironclaw/issues/4400)): Production instances fail to restart; manual cleanup required.  
- **Frustration – Reborn tools invisible** ([#4424](https://github.com/nearai/ironclaw/issues/4424)): User reports model loops narrating about `spawn_subagent` but never calling it.  
- **Frustration – HTTP tool returns raw HTML** ([#4425](https://github.com/nearai/ironclaw/issues/4425)): 1.2 MB context blow-up on a simple fetch; model cannot `.save` properly.  

Overall satisfaction is tempered by these bugs, but the rapid closure of 8 issues and 29 PRs shows strong maintainer responsiveness.

## 8. Backlog Watch
- **Issue #3283** ([link](https://github.com/nearai/ironclaw/issues/3283)) – *Migrate OpenAI-compatible APIs onto Reborn*: Open since May 6, updated June 3, only 1 comment. Important roadmap item awaiting prioritisation.  
- **PR #3951** ([link](https://github.com/nearai/ironclaw/pull/3951)) – *Third-party extension hook activation*: Open since May 23, no recent pushes or reviews. Risk: low, scope: dependencies.  
- **PR #3928** ([link](https://github.com/nearai/ironclaw/pull/3928)) – *Drive arguments_digest snapshot through invoke_capability*: Open since May 23, follow-up to critical review.  
- **PR #3937** ([link](https://github.com/nearai/ironclaw/pull/3937)) – *Cross-backend adversarial parity suite*: Open since May 23, final PR of durable-backend split.  
- **PR #3936** ([link](https://github.com/nearai/ironclaw/pull/3936)) – *LibSqlPredicateStateBackend in own crate*: Open since May 23, awaiting review/merge.  
- **PR #3941** ([link](https://github.com/nearai/ironclaw/pull/3941)) – *Address dropped follow-ups from #3918/#3919*: Open since May 23, small maintainability fixes.  

These PRs from contributor `zmanian` have been pending for nearly two weeks and risk rotting if not reviewed soon.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-04

## 1. Today's Overview
The LobsterAI project saw very high activity over the past 24 hours, with **16 pull requests updated** (14 merged/closed, 2 open) and **1 new release (2026.6.3)** published. The majority of changes focused on the cowork module, MCP reliability, and HTML share improvements. Community engagement remains moderate, with a single open issue (a user complaint about subscription points reset) drawing attention. Overall, the project is in an active development cycle with a clear emphasis on stability and UX refinement.

## 2. Releases
**New Release:** [LobsterAI 2026.6.3](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.3) (published 2026-06-03)

**What’s Changed:**
- `feat(mcp)`: Optimized npx MCP launch resolution and added first response timing logs.
- `feat`: Optimized HTML share (details in PRs #2092 and others).
- `feat(cowork)`: (incomplete note, likely part of larger cowork features).

**Breaking Changes:** None reported.
**Migration Notes:** No special migration steps required; this is a standard patch release.

## 3. Project Progress
**Merged/Closed PRs (14 total)** advanced several key areas:

- **Cowork:**
  - [PR #2097](https://github.com/netease-youdao/LobsterAI/pull/2097): Fixed title bar close button in search modal.
  - [PR #2101](https://github.com/netease-youdao/LobsterAI/pull/2101): Added artifact preview selected text to chat (Markdown/plain text).
  - [PR #2108](https://github.com/netease-youdao/LobsterAI/pull/2108): Improved channel session sync and cleanup.
  - [PR #2085](https://github.com/netease-youdao/LobsterAI/pull/2085): Added local conversation forking (new fork action and IPC handlers).
  - [PR #2098](https://github.com/netease-youdao/LobsterAI/pull/2098): Added selected text snippets to chat context with persistence and badge UI.

- **Shortcuts & UX:**
  - [PR #2109](https://github.com/netease-youdao/LobsterAI/pull/2109): Overhaul of keyboard shortcuts with expanded actions and improved UX.

- **MCP (Model Context Protocol):**
  - [PR #2104](https://github.com/netease-youdao/LobsterAI/pull/2104): Fixed session timeout during gateway config reload.
  - [PR #2103](https://github.com/netease-youdao/LobsterAI/pull/2103): Added validation for remote server URLs.
  - [PR #2100](https://github.com/netease-youdao/LobsterAI/pull/2100): Kept managed MCP installs node-aware (injecting Node toolchain path).

- **HTML Share:**
  - [PR #2105](https://github.com/netease-youdao/LobsterAI/pull/2105): Fixed copy share link and code together.
  - [PR #2099](https://github.com/netease-youdao/LobsterAI/pull/2099): Refined share dialog and access controls (enabled outside test mode, redesigned states).

- **UI & Config:**
  - [PR #2106](https://github.com/netease-youdao/LobsterAI/pull/2106): Fixed kits/skills popover interactions (viewport overflow, delayed close).
  - [PR #2102](https://github.com/netease-youdao/LobsterAI/pull/2102): Preserved user-configured context windows and added Mimo v2.5 models.

- **Release prep:**
  - [PR #2107](https://github.com/netease-youdao/LobsterAI/pull/2107): Release 2026.6.2 (features bundled prior to today’s 2026.6.3).

## 4. Community Hot Topics
The most active item is [Issue #2081 – **“订阅” (Subscription)**](https://github.com/netease-youdao/LobsterAI/issues/2081), with 2 comments. The user angrily reports that 5500 subscription points were cleared before the end of the month, causing frustration. The issue is currently open and has received no official response yet. This is the only issue updated in the last 24h, suggesting concentrated user concern around subscription policy transparency.

## 5. Bugs & Stability
The following bugs were identified and fixed today (ranked by potential severity):

| Severity | Bug Description | Fix PR |
|----------|----------------|--------|
| **High** | MCP session timeout during gateway config reload | [PR #2104](https://github.com/netease-youdao/LobsterAI/pull/2104) |
| **High** | MCP remote servers could be configured with invalid URLs | [PR #2103](https://github.com/netease-youdao/LobsterAI/pull/2103) |
| **Medium** | Managed MCP installs failing because Electron’s Node path not used | [PR #2100](https://github.com/netease-youdao/LobsterAI/pull/2100) |
| **Low** | HTML share copy link and code not working together | [PR #2105](https://github.com/netease-youdao/LobsterAI/pull/2105) |
| **Low** | ModelSelector hover card overflowing viewport; skills popover delayed close | [PR #2106](https://github.com/netease-youdao/LobsterAI/pull/2106) |
| **Low** | User-configured context windows being lost; missing new Mimo models | [PR #2102](https://github.com/netease-youdao/LobsterAI/pull/2102) |

No new critical crashes or regressions were reported. The subscription points issue (#2081) may indicate a backend logic bug but is not confirmed.

## 6. Feature Requests & Roadmap Signals
The only explicit user request visible is **subscription points rollover/transparency** (Issue #2081). While not a formal feature request, the strong language suggests users expect unused subscription credits to persist beyond the billing period.

From merged PRs, newly shipped features that hint at future direction:
- **Conversation forking** (PR #2085) – likely to evolve into more advanced branching.
- **Selected text snippets from artifacts** (PR #2098, #2101) – deepens cowork integration with document preview.
- **Keyboard shortcut overhaul** (PR #2109) – suggests a focus on power-user productivity.

**Prediction for next version:** The team may address the subscription complaint by adding a grace period or clearer UI for point expiration. Further cowork enhancements (e.g., forking with remote sync) are probable.

## 7. User Feedback Summary
- **Pain point:** Subscription point clearing (Issue #2081) – user is upset that 5500 points were reset before month end, implying a lack of warning or unfair policy.
- **Satisfaction:** No positive feedback captured in the last 24h. The high number of merged PRs (14) suggests internal progress but limited user appreciation.
- **Use case:** Cowork collaboration and MCP integration remain core workflows for users, as evidenced by the focus of fixes and features.

## 8. Backlog Watch
Two open PRs have not been merged and may require maintainer attention:

1. **[PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** – `chore(deps-dev): bump the electron group` (updates electron from 40.2.1 to 42.3.1 and electron-builder). Created 2026-04-02, last updated 2026-06-03. This is a major dependency upgrade with potential breaking changes; it has 0 comments and no maintainer review yet. **Risk: High if left unmerged.**

2. **[PR #1463](https://github.com/netease-youdao/LobsterAI/pull/1463)** – `fix long modal titles` (truncation and hover tooltip). Created 2026-04-04, last updated 2026-06-03. Tagged `[stale]` and authored by `leedalei`. This is a bug fix for UI overflow, but has not been merged for over two months. **Risk: Medium, as UX issues may persist.**

No other long-unanswered issues were observed in the 24h window.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-04

## 1. Today's Overview

Moltis saw high activity over the past 24 hours, with 14 issues updated (9 closed, 5 remaining open) and 3 new pull requests opened. No PRs were merged or closed. Two daily incremental releases (20260602.05 and 20260603.01) were published. The project continues to focus on bug squashing, with many older bugs resolved, while new reports highlight Docker integration pain points and Telegram streaming behaviour. The community is actively contributing feature implementations — both open PRs directly address user-reported issues.

---

## 2. Releases

Two new releases are available:

- **20260603.01** — latest daily build
- **20260602.05** — previous daily build

No release notes, breaking changes, or migration instructions were provided for either version. These appear to be incremental CI releases; users should update to the latest for the most recent fixes.

---

## 3. Project Progress

No pull requests were merged or closed today. However, 9 issues were closed, indicating that fixes were landed in earlier merges or resolved via configuration changes. Notable closed issues:

- [#1046 – Vault password detection bug](https://github.com/moltis-org/moltis/issues/1046)
- [#1083 – skills cannot be enabled/disabled individually](https://github.com/moltis-org/moltis/issues/1083)
- [#1053 – automatic session title generation](https://github.com/moltis-org/moltis/issues/1053)
- [#1054 – env vars leaked via `mcp_list`](https://github.com/moltis-org/moltis/issues/1054)
- [#1052 – model picker UI truncation](https://github.com/moltis-org/moltis/issues/1052)
- [#1045 – code block syntax highlighting in light mode](https://github.com/moltis-org/moltis/issues/1045)
- [#1037 – `send_image`/`send_document` failures in Docker](https://github.com/moltis-org/moltis/issues/1037)

The three open PRs are actively addressing ongoing issues (see sections below).

---

## 4. Community Hot Topics

The most-discussed items in the last 24 hours:

- **[#1097 – Telegram edit-in-place streaming mixes intermediate output into final reply](https://github.com/moltis-org/moltis/issues/1097)** (1 comment)  
  User @s-salamatov reported that Telegram’s streaming behaviour conflates progress updates with final answers. This is now being resolved by **PR #1099** ([Separate Telegram progress stream from final replies](https://github.com/moltis-org/moltis/pull/1099)).

- **[#1028 – Agent should have access to Moltis docs OOTB](https://github.com/moltis-org/moltis/issues/1028)** (3 comments, closed)  
  An enhancement that garnered the most comments across all items, suggesting strong community desire for self-documenting agents. It was closed, likely implemented.

- **[#1092 – Add config option to disable channel Activity log tool-status messages](https://github.com/moltis-org/moltis/issues/1092)** (0 comments but paired with a PR)  
  This feature request addresses user annoyance with inline tool logs. **PR #1093** ([Add channel activity log visibility settings](https://github.com/moltis-org/moltis/pull/1093)) implements per-account, per-channel, and per-user toggles.

---

## 5. Bugs & Stability

**New open bugs (ranked by estimated severity):**

| Issue | Title | Severity | Fix PR exists? |
|-------|-------|----------|----------------|
| [#1096](https://github.com/moltis-org/moltis/issues/1096) | `Read`/`Write`/`Edit` tools don't work in Docker | **High** – core file tools broken in Docker deployments | ❌ No |
| [#1095](https://github.com/moltis-org/moltis/issues/1095) | Podman is not working via Moltis | **High** – alternative container runtime unsupported | ❌ No |
| [#1097](https://github.com/moltis-org/moltis/issues/1097) | Telegram edit-in-place streaming mixes intermediate output into final reply | **Medium** – degrades user experience on Telegram | ✅ PR #1099 |
| [#1094](https://github.com/moltis-org/moltis/issues/1094) | De-Preferring Models | **Medium** – model selection logic issue; unclear impact | ❌ No |

Nine older bugs were closed today, indicating the maintainer team is actively triaging and resolving issues. The Docker and Podman reports are particularly concerning for users running Moltis in containerised environments.

---

## 6. Feature Requests & Roadmap Signals

- **[#1092 – Disable channel Activity log tool-status messages](https://github.com/moltis-org/moltis/issues/1092)** – Open feature request with a matching PR (#1093) that adds granular visibility settings. Likely to land in the next release.
- **[#1036 – Support arbitrary inbound file attachments in web UI](https://github.com/moltis-org/moltis/issues/1036)** – Closed (implemented). Users can now attach files via the web interface.
- **[#1028 – Agent access to Moltis docs OOTB](https://github.com/moltis-org/moltis/issues/1028)** – Closed, suggesting the agent now has built-in documentation awareness.

Based on the PR velocity, the next few releases will likely include the Telegram streaming fix and the activity log visibility controls.

---

## 7. User Feedback Summary

Real user pain points surfaced in the last 24 hours:

- **Docker/container support**: Two issues (#1096, #1095) report that core tools and Podman do not work in containerised setups. This is a critical gap for users deploying Moltis via Docker.
- **Telegram interaction quality**: The streaming bug (#1097) causes confusing mixed messages; users expect clean final replies.
- **Model selection confusion**: “De-Preferring Models” (#1094) suggests the model prioritisation logic may behave unexpectedly.
- **Activity log clutter**: Several users want to disable tool-status messages in channels (#1092) — a clear usability request.

Overall, satisfaction appears high regarding the pace of bug fixes (9 closed today), but frustration is building around container runtime compatibility.

---

## 8. Backlog Watch

All currently open issues (5) are from the last 24 hours, so there is no long-unanswered item needing maintainer attention at this time. The three open PRs (#1099, #1098, #1093) are recent and under active development. No stale or abandoned items detected.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-04

## 1. Today's Overview
Project CoPaw (the open-source personal AI agent framework behind QwenPaw) continues to show high community engagement, with 44 issues and 49 pull requests updated in the last 24 hours. Half of the updated issues are resolved or closed (22), indicating responsive maintainers, while the other 22 remain active. The PR pipeline is healthy: 21 PRs have been merged or closed, with 28 still open. No new releases were published today, but the volume of fixes and feature work suggests a release may be imminent. The current focus appears to be on stabilizing core mechanics — context compression, memory management, browser tooling, plugin loading, and channel routing — rather than adding flashy new features.

## 2. Releases
None. No new releases were recorded in the last 24 hours. The latest releases from previous dates remain the active versions (e.g., v1.1.10). Users should stay tuned for an upcoming release that likely bundles the many fixes seen in recent PRs.

## 3. Project Progress
The following pull requests were merged or closed today (2026-06-03 to 2026-06-04 UTC), representing concrete improvements and bug fixes:

- **`fix(skill): increase zip download file size`** (#4941) — Resolves skill download failures when the archive exceeds the previous 5 MB limit (fixes #4928).  
- **`chore(deps): update reme-ai dependency to version 0.3.1.10`** (#4935) — Fixes file watcher reliability (e.g., stop-event not reset on restart).  
- **`fix(context): handle non-dict source objects in media block processing`** (#4933) — Fixes `'str' object has no attribute 'get'` errors during context compaction when media `source` is a plain URL string (fixes #4811).  
- **`docs(roadmap): update the roadmap`** (#4942) — Project direction update.  
- **`test(integration): agent-scoped P0 contract coverage (+55 cases)`** (#4943) — Adds 55 integration tests covering agent-scoped routing, skills CRUD, tools list, heartbeat, and more.  
- **`feat(feishu): add group session sharing mode`** (#4821) — Adds ability to share or isolate sessions for Feishu group chats.  
- **`feat(telegram): add tool_guard interactive approval via inline keyboard`** (#4737) — Brings interactive tool approval cards to Telegram (previously only in QQ and WeCom).  
- **`feat(acp): advertise commands, surface errors, tool params, agent/model meta, file links`** (#4949) — Enriches the ACP server for better terminal UI integration.  
- **`fix(channel): preserve acl_sender_id during native payload merge across all channels`** (#4925) — Fixes whitelist/blacklist checks breaking when rapid messages are merged.  
- **`fix(channel): prevent cross-user message merging in queue routing`** (#4932) — Critical fix for group chats where messages from different users could be incorrectly merged.

These merged PRs address several high-impact bugs and lay groundwork for better channel interoperability and testing coverage.

## 4. Community Hot Topics
The most discussed issues and pull requests (by comment count) reveal strong user demand for stability and memory-related enhancements:

- **#4919** — `[bug] browser_use 启动失败：managed CDP 超时 + Chrome/Edge 浏览器闪退` (6 comments). Users on Windows are unable to launch browsers via `browser_use` due to CDP timeouts and crashes. A fix PR (#4944) is now open.  
- **#3470 & #3516** — Two issues (6 & 4 comments) asking about **self-evolution capabilities** inspired by Hermes Agent. Closed with likely roadmap inclusion.  
- **#3854** — `chromadb Rust binding segfault kills entire process` (5 comments). Dangerous crash on Linux with Python 3.13; no fix PR yet.  
- **#3905** — `Dream agent ISSUE` (5 comments). Memory file handling in Dream agent fails to persist, leaving only blank templates.  
- **#4924** — `上下文压缩失败的问题` (4 comments). Context compaction fails with `'str' object has no attribute 'get'` due to old file block format. Now fixed by #4933 (merged).  
- **#4448** — `Context compaction often fails with "missing ## header"` (4 comments). Another compaction issue, closed.  
- **#3944** — `希望 Auto-Memory 排除心跳与定时任务` (4 comments, 1 👍). Users want system messages excluded from memory consolidation.  
- **#4616** — `Dream awakening task error` (4 comments). Error in WeChat channel detection even when not configured.

On the PR side, **#4794** (plugin uninstall hooks) and **#4900** (decouple plugin loader initialization) are under review and address the widely-reported plugin loader not ready issue (#4889).

Underlying needs: Users are frustrated by recurring memory/compaction failures that break long conversations, and by browser tool instability on Windows. The community also shows strong interest in agent self-improvement (Hermes-style) and better memory hygiene.

## 5. Bugs & Stability
Bugs reported or updated today, ranked by severity:

| Severity | Issue | Description | Status / Fix |
|----------|-------|-------------|--------------|
| **Critical** | #3854 | Chromadb Rust binding segfault kills entire process on Linux (45+ crashes) | Open, no fix |
| **High** | #4795 | Vector index grows to 37 GB, causing memory_search crashes (10+ crashes) | Open, user reports deleting `file_store/` works |
| **High** | #4919 | Browser launch failure on Windows (CDP timeout, Chrome/Edge crash) | Open, fix PR #4944 submitted |
| **High** | #4889 | Plugin Loader not ready in Tauri desktop, cannot install plugins | Open, fix PR #4900 under review |
| **High** | #4781 | `tool_result_pruning` fails to prevent context blowup from oversized shell output | Open |
| **Medium** | #4928 | Skill download fails with 422 error due to size limit | Fixed in #4941 (merged) |
| **Medium** | #4924 | Context compaction fails on old file block format | Fixed in #4933 (merged) |
| **Medium** | #4916 | Backup fails with PermissionError on browser cache files (Windows) | Open |
| **Medium** | #4937 | `/compact` command ignores model's max_input_length, uses 128K default | Open |
| **Low** | #4888 | Dream agent overwrites MEMORY.md of other workspace due to relative path | Closed with fix |
| **Low** | #4710 | Vector store timestamp inconsistency (naive vs UTC) | Open |

Multiple fix PRs are already in the pipeline, especially for context compaction and plugin loading. The chromadb segfault and vector index explosion remain unaddressed but are marked as high priority.

## 6. Feature Requests & Roadmap Signals
Several feature requests received active discussion and may influence the upcoming release:

- **Self-evolution / Hermes-style agent improvement** (#3470, #3516) — Closed, suggesting the team has plans but no concrete timeline.
- **Auto-Memory exclude heartbeat/cron** (#3944) — Simple change, likely to be picked up soon given community desire.
- **Lossless context compression (DAG-based + CJK token fix)** (#4551) — Detailed proposal, addresses a major pain point. High chance of being explored next.
- **Session end auto-summary hook** (#4640) — Pre-hook for memory archiving, aligns with memory enhancement trend.
- **Enhanced memory management and lifecycle** (#3995) — Archive old notes, conflict detection. Good candidate for next minor release.
- **Adaptive context handling** (#3801) — Let model determine max context instead of manual config. May require deeper architectural change.
- **Delete single message in conversation UI** (#4001) — Common request, relatively low complexity, might appear soon.
- **Support mem0** (#4208) — User asks for mem0 integration; currently no documentation.
- **Code mode open other disk directories** (#4876) — Windows-specific, likely addressed in settings enhancement.

The roadmap update PR (#4942) hints at formalized priorities; users should watch for the next blog post or release notes.

## 7. User Feedback Summary
Real user experiences expressed in issues and comments:

- **Pain points**:  
  - Context compaction failures are the #1 frustration, breaking long conversations and forcing restarts.  
  - Chromadb memory leaks and crashes on Linux make the agent unusable for high-usage scenarios.  
  - Plugin system in Tauri desktop is broken, preventing extension of functionality.  
  - Browser automation on Windows is unreliable (CDP timeout, crashes).  
  - Dream agent memory persistence is inconsistent, leading to lost knowledge.  
  - Backup failures on Windows due to locked files.  
  - Lack of manual message deletion forces users to clear entire conversations.

- **Use cases**:  
  - Long-running development tasks (code changes across days).  
  - Daily/weekly report gathering (large search results get compressed).  
  - Multi-turn requirement discussions (early decisions lost after compression).  
  - Users rely on MEMORY.md and daily notes for knowledge retention; any failure is critical.

- **Satisfaction**:  
  - Users appreciate the open approach and active development (many issues closed quickly).  
  - The memory system design is praised as "simple and reliable" in concept, but implementation bugs reduce trust.  
  - Feature requests are well-received, but some (like self-evolution) remain vague on timeline.

## 8. Backlog Watch
Issues and PRs that are important, open, and have not received maintainer attention recently (updated >7 days ago with no comment from project members):

- **#3854** — Chromadb segfault (last update 2026-06-03, but no maintainer reply). Critical, needs immediate investigation.  
- **#4795** — Vector index explosion (last update 2026-06-03, user suggests workaround but no fix acknowledged).  
- **#4208** — Mem0 support request (last update 2026-06-03, no official response). Documentation gap.  
- **#4781** — `tool_result_pruning` fail (last update 2026-06-03, no comment from maintainers).  
- **#4710** — Vector store timestamp inconsistency (last update 2026-06-03, no resolution).  
- **#4640** — Session auto-summary RFC (last update 2026-06-03, no maintainer feedback).  
- **#3995** — Enhanced memory management (last update 2026-06-03, no reply). Large proposal.  
- **#3801** — Adaptive context (last update 2026-06-03, no reply).  
- **#4001** — Delete single message (last update 2026-06-03, no reply).  
- **#3905** — Dream agent issue (last update 2026-06-03, user reported but no fix PR yet).

Maintainer activity is generally high, but these open issues have not yet received a tagged response or assignment. The chromadb and vector index problems are particularly urgent for production users.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-04

## Today's Overview
ZeptoClaw shows no human-driven development activity in the last 24 hours. All 16 open pull requests are automated dependency updates (Dependabot), covering Rust crates, GitHub Actions, JavaScript packages, and Docker images. No new releases were cut, no issues were filed or closed, and no PRs were merged. The project appears to be in a quiet maintenance phase, with the only active changes being routine dependency bumps that require maintainer review. The open issue backlog remains at zero, suggesting either a very stable codebase or low community engagement.

## Releases
None.

## Project Progress
No pull requests were merged or closed today. All 16 open PRs are Dependabot-generated and remain unmerged, awaiting review. There is no evidence of feature work, bug fixes, or documentation improvements being completed in the last 24 hours.

## Community Hot Topics
No issues or pull requests have generated discussion or reactions. All 16 open PRs are dependency bumps with zero comments and no thumbs-up. The project has no active community engagement visible in the tracked data.

## Bugs & Stability
No bug reports, crashes, or regressions were filed today. The lack of open issues indicates no known stability problems.

## Feature Requests & Roadmap Signals
No feature requests were submitted in the last 24 hours. The roadmap direction remains unclear from this data alone.

## User Feedback Summary
No user feedback, pain points, or satisfaction metrics are available from the current dataset. The absence of issues or pull request discussions suggests either very satisfied users or low usage.

## Backlog Watch
No long-standing issues or PRs requiring maintainer attention exist. All open PRs are recent (created 2026-06-03) and are routine dependency updates. The most notable pending changes include:

- Rust upgrade from `1.95-slim-trixie` to `1.96-slim-trixie` ([PR #613](https://github.com/qhkm/zeptoclaw/pull/613))
- Several framework/library version bumps across the `panel` and documentation sites (`astro`, `react`, `tailwindcss`).

Maintainers should review these PRs to keep the project current, but no urgent attention is required.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-04

## Today's Overview
The project saw very high activity over the past 24 hours, with **30 issues updated** (3 closed) and **50 pull requests updated** (3 closed/merged). Development is concentrated on two major tracks: **security/authentication hardening** (pluggable security provider, OIDC support) and **terminal-user interface (TUI)** parity with the web dashboard. The v0.8.0 release queue (#7112) and the v0.8.1 integration tracker (#6970) are both actively coordinated, indicating the team is in a release preparation phase. At the same time, a significant number of S1 (workflow-blocked) bugs were reported—particularly around session lifecycle, quickstart configuration, and the TUI stability—which may delay the release if not addressed promptly.

## Releases
No new releases were published today.

## Project Progress
Three pull requests were merged/closed:
- **PR #7181** fix(update,skills): harden error handling — log `remove_file` failures and strengthen path traversal guard. *This improves non-fatal failure observability.*
- **Issue #6822 closed** — the `zerocode` TUI binary has been added to the release build matrix, CI pipeline, and package manager distributions, meaning it will ship alongside the main `zeroclaw` binary in future releases.
- **Issues #7168 and #7167 closed** — the session branching feature (forking conversations at any message point) has been delivered. This enables users to explore “what-if” scenarios without losing the original conversation thread.

Other notable code improvements merged (via open PRs that advanced):
- **PR #7189** blocks scheduler mutation tools (`cron_add`, `cron_update`, `cron_delete`) inside cron-launched agent jobs by default, preventing accidental self-modification.
- **PR #7188** adds `schedule={"kind":"after","after_seconds":...}` to `cron_add` for relative one-shot reminders (e.g. “in 10 minutes”).
- **PR #7180** fixes the `wire_api = "responses"` setting for custom and OpenAI-compatible model families, so self-hosted vLLM endpoints now correctly use the responses API path.
- **PR #7177** enforces memory-tool exclusion for ACP (Code) sessions server-side, closing a hole where the client could request memory tools in code sessions.

## Community Hot Topics
- **[Issue #7142](zeroclaw-labs/zeroclaw Issue #7142)** (3 comments) — “Expose the security enforcement layer as a pluggable provider interface.” This is a tracking issue for v0.9.0 that covers the entire security surface (enforcement, reporting, incident response) behind a single trait. High community interest in making security modular.
- **[Issue #7141](zeroclaw-labs/zeroclaw Issue #7141)** (3 comments) — “OIDC Authentication Provider support for the RPC/WSS transport.” Paired with #7142, this signals strong demand for enterprise-grade authentication (OpenID Connect) alongside the existing token model.
- **[Issue #7112](zeroclaw-labs/zeroclaw Issue #7112)** (0 comments but central) — v0.8.0 release queue tracker. Lists all breaking-change decisions and stable-tier promotions required before the release. The lack of comments suggests internal coordination, but the issue is the primary milestone hub.
- **[Issue #6970](zeroclaw-labs/zeroclaw Issue #6970)** (0 comments) — v0.8.1 integration/channel/provider/tool PR queue. Complements #6489 and handles additive work. Both trackers are updated daily, reflecting ongoing release engineering.

## Bugs & Stability
### S1 — Workflow Blocked
- **[Issue #7179](zeroclaw-labs/zeroclaw Issue #7179)** — ZeroClaw reaps idle RPC sessions after exactly 10 minutes, preventing long-running conversations. **Fix PR #7182** (persistent RPC sessions) is open and removes the idle-TTL entirely, making sessions persist until explicit close/daemon exit.
- **[Issue #7173](zeroclaw-labs/zeroclaw Issue #7173)** — Quickstart webhook channel setup does not offer a port selection, leading to a missing `field port` TOML error when starting the agent. **No fix PR yet**.
- **[Issue #7125](zeroclaw-labs/zeroclaw Issue #7125)** — TUI (`zerocode`) freezes completely when the daemon disconnects, requiring force-quit. **No fix PR yet**.

### S2 — Degraded Behavior
- **[Issue #7151](zeroclaw-labs/zeroclaw Issue #7151)** — Observability tool_call telemetry leaks onto the chat WebSocket, causing permanent “unknown” tool cards with spinners. Root cause: shared broadcast channel. **No dedicated fix PR yet**.
- **[Issue #7133](zeroclaw-labs/zeroclaw Issue #7133)** — path-policy false-positive on `~` tokens in quoted/heredoc command data (S2). **No fix PR yet**.
- **[Issue #7126](zeroclaw-labs/zeroclaw Issue #7126)** — Web UI “Clear all” only wipes rendered messages, not backend session history. **No fix PR yet**.
- **[Issue #7143](zeroclaw-labs/zeroclaw Issue #7143)** — Agent repeatedly runs near-duplicate shell discovery commands until `max_tool_iterations` exhausted. Reported by user sbenedetto. **No fix PR yet**.

### S3 — Minor Issues
- [#6702](zeroclaw-labs/zeroclaw Issue #6702) — Dashboard assistant bubble accumulates blank lines for each tool-call card (open since May 16).  
- [#7157](zeroclaw-labs/zeroclaw Issue #7157) — Chat timestamps rendered inside message bubble instead of as separate metadata.  
- [#7156](zeroclaw-labs/zeroclaw Issue #7156) — Reload banner shows persistent drift for `gateway.paired_tokens (secret)` that never clears.  
- [#7139](zeroclaw-labs/zeroclaw Issue #7139) — i18n missing translation keys for chat toolbar buttons (compact, clear all, stop, etc.).

Several fix PRs are open for related issues: **PR #7160** improves daemon config load resilience; **PR #6988** invalidates bearer tokens on device rotate/delete; **PR #7123** fixes UTF-8 char-boundary panics in text truncation across channels and tools.

## Feature Requests & Roadmap Signals
- **Security & Auth**: Issues #7142 (pluggable security provider) and #7141 (OIDC authentication) are tracked for v0.9.0, but given their importance, they may be accelerated into v0.8.x.
- **TUI maturation**: Trackers #6826 (ZeroClaw TUI) and #6825 (TUI UX) are at status `in-progress`. The TUI binary (`zerocode`) is now in the release pipeline (closed #6822). Expect the TUI to become stable in v0.8.1.
- **Web UI enhancements**: File upload/path selection UI (#7138) and slash commands (#7137) are feature requests that surfaced today; likely candidates for v0.8.1.
- **High-risk shell confirmation**: #7155 proposes a per-execution confirmation tier for dangerous commands, mimicking Claude Code’s allow/ask/deny pattern. This aligns with the security trend.
- **OpenRPC spec publication**: #7131 asks for machine-readable RPC documentation. This would greatly aid integrators.
- **Sandbox granularity**: RFC #6996 (granular sandbox policy) remains open with `needs-maintainer-review`. Expected to land post-v0.8.0.

## User Feedback Summary
- **Positive**: User sbenedetto (#7143) explicitly thanked the team: *“It is great to see a Rust-based agent runtime that is much lighter on resources than many other agent systems we have tried.”* This reinforces ZeroClaw’s niche as a resource-efficient, Rust-native alternative.
- **Pain points**:
  - The TUI freezes on daemon disconnect (#7125) frustrates power users.
  - The quickstart channel setup (#7173) has a broken webhook creation path that blocks first-time use.
  - Session reaping after 10 minutes (#7179) breaks long-running conversations—a core use case for coding and research agents.
  - The “Clear all” UI bug (#7126) and persistent drift banner (#7156) degrade the dashboard experience.
  - i18n gaps (#7139) affect non-English users.
  - Agent looping on shell commands (#7143) wastes LLM tokens and frustrates Slack-connected coding agents.
- **Missing features**: Several users requested slash commands (#7137), file uploads (#7138), and better confirmation workflows (#7155), indicating a desire for more interactive and safe control.

## Backlog Watch
- **[Issue #6702](zeroclaw-labs/zeroclaw Issue #6702)** — Dashboard blank line accumulation (open since May 16, no fix PR yet). Though S3, it has been open for three weeks and is a persistent visual annoyance.
- **[Issue #6996](zeroclaw-labs/zeroclaw Issue #6996)** — RFC: Granular sandbox policy (needs-maintainer-review). This is a foundational RFC for sandbox capabilities; its long open status (since May 28) may stall future sandbox work.
- **[Issue #7133](zeroclaw-labs/zeroclaw Issue #7133)** — Path-policy false-positive on `~` tokens (S2, no fix PR). Security-sensitive bug that could cause false denials in scripting workflows.
- **[Issue #7128](zeroclaw-labs/zeroclaw Issue #7128)** — Stale `zeroclaw onboard` references after #6848 deletion. User-visible documentation breakage that needs a quick scrub.
- **[Issue #6826](zeroclaw-labs/zeroclaw Issue #6826)** & **[#6825](zeroclaw-labs/zeroclaw Issue #6825)** — TUI trackers in progress since May 21. While active, they are not yet close to completion and represent a significant amount of remaining work.

*All links follow the pattern `zeroclaw-labs/zeroclaw Issue #NNNN` or `zeroclaw-labs/zeroclaw PR #NNNN` as provided.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*