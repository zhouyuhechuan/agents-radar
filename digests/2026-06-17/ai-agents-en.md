# OpenClaw Ecosystem Digest 2026-06-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-17 02:56 UTC

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

# OpenClaw Project Digest — 2026-06-17

## Today's Overview
OpenClaw remains in a high-velocity development cycle with **500 issues** and **500 pull requests** updated in the last 24 hours. Activity is balanced: 93 PRs were merged/closed, while 407 remain open, and 37 issues were resolved against 463 still active. A new patch release **v2026.6.8** landed today, focusing on channel delivery robustness. The project continues to address a wide spectrum of concerns—from critical session-state and message-loss bugs (many P1/P0) to long-standing feature requests like Linux/Windows desktop apps. Community engagement is high, with the top issue (#75) accumulating 109 comments and 79 👍 since January.

---

## Releases
### v2026.6.8 (2026.6.8)
- **Highlights**: Richer and less brittle channel delivery for Telegram and WhatsApp.
  - Telegram: structured text rendering (tables, lists, expandable blockquotes, preserved line breaks, CLI-backed replies).
  - WhatsApp: honors configured ACP bindings.
- **Related PRs/Issues**: #92679, #931… (cross-reference missing in snippet)
- **Breaking changes**: None noted in the summary.
- **Migration notes**: No special instructions provided; typical upgrade via `openclaw upgrade` or package manager.

---

## Project Progress
Today saw **93 merged/closed PRs** and **37 closed issues**. Notable closures and merges visible in the top data include:

- **[CLOSED] #32296** – Agent replies to previous message instead of current (session context confusion). A P1 bug with 16 comments.
- **[CLOSED] #91016** – Chinese-community reported DeepSeek Prompt Cache失效 (loss) after upgrade to 2026.6.1, costing ~$6/hour. Fixed in later version.
- **[CLOSED] #73814** – Installer hangs due to stdin consumption in `curl | bash`. Root cause identified and addressed.
- **[MERGED] #68936** – Autofix PR review pipeline + Windows daemon (large script).
- **Numerous small fixes today**: #93877 (secrets env vars), #93876 (skill overlay Docker 25+ compat), #93857 (Dependabot alerts), #93840 (NO_PROXY in web_fetch), #93864 (Ollama thinking levels), #93853 (memory embedding routing), #93848 (absolute-path media for vision blocks), #93821 (mcporter daemon startup logs), #93838 (Telegram richMessages help text), #93874 (Slack MiniMax reasoning tags), #93873 (WhatsApp listener restart on config change), #93632 (macOS HUD wake capture silence), #90579 (trusted host-read HTML after outbound staging), #93871 (cron+subagent completion route registry), #93636 (tolerate deleted cwd), #93580 (cron delivery awareness), #93532 (ClawHub source in skill verify), #91807 (CLI `--file` for image generate), #93579 (Telegram richMessagesAutoDetect), #93007 (gateway web_search_options forwarding), #92154 (QQBot group command gate), #61675 (session reset hooks for daily/idle resets), #60981 (Filesystem Access Control PathGuard – large PR, still open but updated), #65359 (allow historyLimit: 0), #54724 (fix agents primary model selection), #50520 (strip inbound metadata before delivery), #55211 (prevent re-entrant loop in internal hook trigger), #46502 (watchdog core service – large PR, still open).

---

## Community Hot Topics
### Most Active Issues (by comments/reactions)

| Issue | Title | Comments | 👍 | Analysis |
|-------|-------|----------|----|----------|
| [#75](openclaw/openclaw Issue #75) | Linux/Windows Clawdbot Apps | 109 | 79 | Long-standing (Jan 2026) feature request; community strongly wants desktop clients beyond macOS/iOS/Android. Still open with P2 priority. |
| [#88838](openclaw/openclaw Issue #88838) | Track core session/transcript SQLite migration via accessor seam | 30 | 1 | Maintainer-driven P0 migration plan. High internal priority to avoid a monolithic rewrite. |
| [#44925](openclaw/openclaw Issue #44925) | Subagent completion silently lost — no retry, no notification, no auto-restart | 19 | 1 | Critical P1 bug affecting subagent orchestration reliability. Multiple failure patterns documented. |
| [#22676](openclaw/openclaw Issue #22676) | Signal daemon stop() race condition on SIGUSR1 restart | 17 | 0 | P1 race causing orphaned processes; long-running issue (Feb 2026) still open. |
| [#32296](openclaw/openclaw Issue #32296) (CLOSED) | Agent replies to previous message (session context confusion) | 16 | 1 | Fixed today; one of several context-assembly bugs. |
| [#58450](openclaw/openclaw Issue #58450) | Agent can promise follow-up without starting any action | 15 | 3 | P2 user-facing trust issue; agents hallucinate tasks. |
| [#68596](openclaw/openclaw Issue #68596) | Configurable streaming watchdog timeout threshold | 14 | 8 | P2 feature request to avoid false watchdog warnings on long-reasoning models. |
| [#62505](openclaw/openclaw Issue #62505) | Coding Agent never completes anything (regression in 2026.4.x) | 14 | 1 | P1 regression; coding agent became useless after upgrade. |
| [#57901](openclaw/openclaw Issue #57901) | Safeguard compaction ignores compaction.model config | 14 | 1 | P2 bug leads to wrong model used for safeguard checks. |
| [#39604](openclaw/openclaw Issue #39604) | Add tools.web.fetch.allowPrivateNetwork | 13 | 9 | P2 security feature with high demand; web_fetch cannot access local network resources. |
| [#59330](openclaw/openclaw Issue #59330) | Control UI Raw mode permanently disabled since 2026.3.31 | 8 | 14 | P2 regression frustrated users; workaround missing. |
| [#64046](openclaw/openclaw Issue #64046) | 敏感数据脱敏 (Sensitive data masking) | 8 | 0 | Chinese community request for credentials masking in configs/logs/UI. |

### Most Active PRs
- **#50520** (fix outbound strip metadata) – open 3 months, still needs proof.
- **#60981** (PathGuard filesystem access control) – large XL PR, needs real-behavior proof.
- **#46502** (watchdog core service) – open since March, unranked krab rating, needs proof.
- **#54724** (agents primary model selection fix) – waiting on author, screenshot proof provided.
- **#93871** (cron+subagent completion routes) – fresh PR targeting three P1 issues.

---

## Bugs & Stability
### Critical (P0/P1)
- **P0 #88838** – Accessor seam for SQLite migration: maintainer-driven, no fix PR yet.
- **P1 #44925** – Subagent completion silently lost: no fix PR yet, linked to multiple patterns (E31/E42/E45).
- **P1 #22676** – Signal daemon race condition: still open since Feb, linked PR exists.
- **P1 #62505** – Coding Agent regression (worked in 2026.4.2 and earlier): linked PR open, causes severe user impact.
- **P1 #32296** – Session context confusion (CLOSED today).
- **P1 #48003** – Steer mode does not inject messages mid-turn: linked PR open.
- **P1 #63216** – Repeated hard resets despite high reserveTokensFloor: no fix PR.
- **P1 #43367** – Multi-agent orchestration unstable: linked PR open.
- **P1 #67777** – Subagent completion lost on timeout/drain: no fix PR.
- **P1 #64810** – Heartbeat swallows in-progress replies in Telegram topics: no fix PR.
- **P1 #63829** – Feature: per-agent memory-wiki vault: fix PR not yet.
- **P1 #69118** – Claude CLI sessions reset every turn due to groupIntro drift: linked PR open.
- **P1 #57326** – CLI-backed helper paths bypass CLI dispatch: linked PR open.
- **P1 #54531** – Force reply to originating channel: linked PR open.
- **P1 #58957** – Model switch fails silently with large context: no fix PR.
- **P1 #52130** – Restart storm from Telegram retry type mismatch: linked PR open.
- **P1 #66443** – Overflow recovery duplicates user messages: linked PR open.
- **P1 #63930** – Support Anthropic advisor tool: linked PR open.
- **P1 #58514** – Google Chat space messages silently ignored: linked PR open.
- **P1 #48949** – Feishu channel fails with proxy: linked PR open.

### High-severity bugs with fix PRs today
- **#73814** (CLOSED) – Installer hangs (P2, but crash/hang).
- **#91016** (CLOSED) – DeepSeek Prompt Cache失效 (P1, cost spike).
- **#93877** – exec secret provider env vars (P1 fix).
- **#93876** – Docker mount conflict (P2 fix).
- **#93840** – NO_PROXY ignored in web_fetch (P2 fix).
- **#93864** – Ollama thinking levels not shown (P2 fix).
- **#93848** – Telegram images missing (fixes 3 P1/P2 issues).
- **#93853** – Memory embedding routing (P2 fix).
- **#93821** – QMD search JSON parse failure (P1 fix).
- **#93871** – Cron+subagent completion routes (targets P1 #92460, #92076).
- **#90579** – Trusted HTML reports after outbound staging (P1 fix).
- **#93580** – Cron delivery awareness (P2, but related to message loss).

### Notable regressions
- **#62505** (Coding Agent) – major usability regression.
- **#59330** (Raw mode disabled) – UI regression since 2026.3.31.
- **#88657** (DeepSeek V4 Flash incomplete turn) – regression in 2026.5.27/28.

---

## Feature Requests & Roadmap Signals
### High-demand features (backed by reaction count)
1. **#75** – Linux/Windows Clawdbot Apps (79 👍) – Very strong demand for desktop coverage.
2. **#39604** – Private network access for web_fetch (9 👍) – Opt-in security feature.
3. **#63829** – Per-agent memory-wiki vault (9 👍) – Isolation for multi-agent setups.
4. **#68596** – Configurable streaming watchdog timeout (8 👍) – Helps long-reasoning models.
5. **#91016** (CLOSED) – DeepSeek Prompt Cache – Community flagged performance cost.
6. **#64046** – Sensitive data masking – Chinese community need.
7. **#52640** – Persistent task-status surface for long-running channel turns (2 👍).
8. **#81061** – Pre-routing inbound hook for bridging (3 👍).
9. **#78308** – Channel-mediated approval for MCP tool calls (1 👍).

### Likely to appear in next version(s)
- **Per-agent memory-wiki** (PRs may be in development given maintainer review label).
- **Private network access** for web_fetch – simple config change, high demand.
- **Streaming watchdog timeout** – straightforward user-facing config.
- **MCP consent envelope** – security-sensitive, may take longer.
- **Linux/Windows Clawdbot Apps** – huge effort, likely remains on roadmap but not imminent.
- **QQBot group commands gating** (PR #92154) – nearly ready.
- **RichMessagesAutoDetect** (PR #93579) – near ready.
- **Gateway web_search_options forwarding** (PR #93007) – large XL, actively grinding.

---

## User Feedback Summary
- **Positive**: Telegram and WhatsApp delivery improvements in v2026.6.8 directly address user pain points around broken or ugly message rendering. The new release was clearly driven by community feedback.
- **Pain points**:
  - **Session context and message loss** is the #1 category of bugs (dozens of P1 issues). Users on Telegram, Discord, and group channels frequently see duplicate replies, silent loss, or context confusion.
  - **Coding agent regression** (#62505) is a major frustration for power users who rely on it daily. The agent now only gives vague status updates.
  - **Long-reasoning models** trigger false watchdog timeouts (#68596, 8 👍).
  - **Multi-agent orchestration** is unstable (#43367) – concurrent add/config overwrites and session-lock failures.
  - **Chinese users** report specific issues: DeepSeek prompt cache loss costing money (#91016), Feishu plugin failures (#48949, #37626), and nested directory bug (#45765). Also request sensitive data masking (#64046).
  - **Onboarding issues**: installer hang (#73814), type error on Telegram token replace (#67366), nested .openclaw directory (#45765).
  - **Missing features**: Linux/Windows clients (#75), private network fetch (#39604), persistent task status (#52640), per-agent memory-wiki (#63829), MCP approval (#78308).
- **Satisfaction indicators**: High issue engagement (109 comments on #75) shows a passionate community actively shaping the project.

---

## Backlog Watch
### Long-unanswered important issues needing maintainer attention
- **#75** – Linux/Windows Clawdbot Apps (open since Jan 2026, P2). Despite 109 comments and 79 👍, no PR or maintainer assignment visible. Community may be waiting for a roadmap commitment.
- **#22676** – Signal daemon race condition (open since Feb 2026, P1). Linked PR open (likely not merged). Critical for stability under config restarts.
- **#88838** – SQLite migration accessor seam (open June 2026, P0). Maintainer-driven but no fix PR yet; high risk if delayed.
- **#43367** – Multi-agent orchestration unstable (open March 2026, P1). Linked PR may need prioritization.
- **#58450** – Agent promises follow-up without action (P2, open March). Could erode user trust.
- **#57901** – Safeguard compaction ignores config (P2, open March). Linked PR open.
- **#57326** – CLI-backed helper paths bypass CLI dispatch (P1, open March). Linked PR open.
- **#50520** – Strip inbound metadata (P1 PR, open since March). Needs real-behavior proof – important for security/privacy.
- **#60981** – PathGuard filesystem access control (XL PR, open April). Needs proof – security-critical.
- **#46502** – Watchdog core service (XL PR, open March). Needs proof – resilience feature.
- **#63007** – Gateway web_search_options (XL PR, open June). Actively grinding but large scope.

### Recommendations for maintainers
- Address #75 roadmap communication (even a “not now” with explanation would help).
- Push #22676 and #88838 to resolution – they are foundational stability/architecture issues.
- Triage #62505 (Coding Agent regression) as a top blocker – it’s a P1 regression affecting daily users.
- Review PRs with `needs-real-behavior-proof` and `needs-maintainer-review` tags promptly (e.g., #50520, #60981, #46502, #55211).
- Monitor Chinese community issues – #64046, #45765, #48949 – to ensure language parity in support.

---

*This digest was generated from the top 50 issues and top 30 PRs updated in the last 24 hours. Due to the volume, not all 500 items could be individually reviewed.*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

### Cross-Project Comparison Report: Personal AI Agent Ecosystem
**Date:** 2026-06-17

#### 1. Ecosystem Overview

The open-source personal AI agent landscape is characterized by extreme velocity and a clear shift from "can it work?" to "can it work reliably at scale?" The ecosystem is dominated by a core reference architecture (OpenClaw) and a cluster of derivative and competing projects, all racing to solve critical infrastructure challenges around session management, multi-platform delivery, and context optimization. Community contributions are high across the board, with users demanding concrete reliability improvements (e.g., message loss, session context) over flashy new features. A key trend is the fragmentation of focus: while several projects act as general-purpose agents, others are carving niches in multi-agent orchestration, desktop integration, and enterprise platform support (WeCom, QQ Bot, Feishu).

#### 2. Activity Comparison

| Project | Issues (Open/Total Updated) | PRs (Open/Total Updated) | Release Status | Health Score* |
|---|---|---|---|---|
| **OpenClaw** | 463 / 500 | 407 / 500 | **New Release**: v2026.6.8 | **Very High** |
| **NanoBot** | 3 / 9 | 10 / 24 | None today | High |
| **Hermes Agent** | 46 / 50 | 45 / 50 | None today | High |
| **PicoClaw** | 4 / 15 | 3 / 15 | **New Release**: v0.3.0-nightly | Moderate |
| **NanoClaw** | 5 / 6 | 1 / 5 | None today | Moderate |
| **NullClaw** | 2 / 2 | 3 / 3 | None today | Low-Moderate |
| **IronClaw** | 31 / 50 | 35 / 50 | None today | High |
| **LobsterAI** | 1 / 1 | 1 / 4 | None today | Low-Moderate |
| **TinyClaw** | 0 / 0 | 1 / 1 | None today | Low |
| **Moltis** | 3 / 4 | 2 / 2 | None today | Low |
| **CoPaw** | 24 / 44 | 31 / 38 | **New Release**: v1.1.12-beta.1 | Very High |
| **ZeptoClaw** | 0 / 0 | 1 / 1 | None today | Inactive |
| **ZeroClaw** | 37 / 50 | 40 / 50 | None today | Very High |

*Health Score: Qualitative assessment based on contributor activity, issue resolution rate, and community engagement volume.
*Note: All counts reflect items updated in the last 24 hours, not total project backlogs.*

#### 3. OpenClaw's Position

OpenClaw maintains a dominant position as the **core reference implementation**, evidenced by its sheer scale of activity (500 issues and PRs updated in 24h). Its key advantages include:
- **Largest Community & Maturity**: The top issue (#75, Linux/Windows desktop apps) has 109 comments and 79 👍, representing a level of engagement no other project matches. This feedback loop drives its roadmap.
- **Technical Breadth**: It is the only project actively addressing the full stack—from critical backend bugs (session-state, message loss) to platform delivery (Telegram, WhatsApp) and advanced features (clawdbot apps).
- **Release Cadence**: A new patch release (v2026.6.8) landed today, proving rapid, user-driven iteration.
- **Differentiation from Peers**: While NanoBot focuses on tooling/build integration and Hermes on enterprise platforms, OpenClaw is the general-purpose, high-velocity foundation. Projects like PicoClaw and NanoClaw appear to be lighter forks, while IronClaw, CoPaw, and ZeroClaw are heavier, feature-rich competitors with their own strong communities.

**Risk**: Its extreme activity volume (500 open items) creates a risk of maintainer burnout and slower resolution for specific issues, an opportunity for more focused competitors like IronClaw.

#### 4. Shared Technical Focus Areas

The following requirements are emerging simultaneously across multiple projects, signaling a clear community consensus on critical next steps for the ecosystem:

- **Session Context & Message State Management**: A universal pain point. OpenClaw (P1 bug #32296, now closed), NanoBot (duplicate user turn #4079, fixed), and IronClaw (SSO automation state) all struggle with context confusion and message loss.
- **Platform Adapter Reliability**: The "last mile" of agent delivery is a bottleneck. **WeCom** (Hermes, CoPaw), **Telegram** (OpenClaw, PicoClaw, Hermes), **QQ Bot** (Hermes, ZeroClaw), and **Slack** (NanoClaw, Hermes) all have open bugs for message truncation, reconnection loops, and zombie connections.
- **Security & Credential Hardening**: **PicoClaw** (11 security advisories stale), **CoPaw** (keychain isolation), **ZeroClaw** (prebuilt binary regressions), and **NanoClaw** (credential proxy ban risk) show a growing focus on securing the agent pipeline.
- **Context Compression & Token Budgeting**: **NanoBot** (history digest capped), **CoPaw** (sub-agent compaction freeze, Headroom integration), **NullClaw** (incomplete local model answers), and **IronClaw** (Engine V2 quality) all seek to manage infinite context windows efficiently.
- **Multi-Agent Orchestration & Task Management**: **OpenClaw** (subagent completion lost, cron delivery), **Hermes** (multi-agent orchestration model), and **IronClaw** (automation blocking) highlight demand for reliable, persistent task execution.

#### 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | IronClaw | CoPaw | ZeroClaw |
|---|---|---|---|---|---|
| **Target User** | Developers, power users | Enterprise teams (WeCom, QQ, Feishu) | Platform engineers, automation | General users, i18n (Vietnamese) | Developers, CI/CD oriented |
| **Key Feature Focus** | Core agent performance, session state, delivery UI | Enterprise platform reliability, MCP integration | Engine V2 quality, Reborn WebUI, governance | Context compression, channel-specific fixes, security | Prebuilt binaries, shell integration, CI/CD |
| **Architecture** | Unified, high-velocity core | Platform-adapter heavy, multi-tenant | Engine V2 core + WebUI | Desktop-first, beta release | CLI + prebuilt binaries |
| **Risk / Weakness** | Issue overload (463 open), may miss platform-specific bugs | Platform-specific bug proliferation (WeCom 4 bugs) | High number of open PRs (35), review bottleneck | Compaction freeze and long session crashes | Documentation quality ("crap" per user #7758) |

#### 6. Community Momentum & Maturity

**Tier 1 (Very High Momentum, Rapid Iteration):**
- **OpenClaw**, **CoPaw**, **ZeroClaw**: These three projects show the highest raw activity, with hundreds of items in flight. They are shipping new releases (OpenClaw, CoPaw) or have clear, aggressive roadmaps (ZeroClaw). They are likely the primary drivers of core innovation but also carry the highest risk of regressions.

**Tier 2 (High Momentum, Active Maintenance):**
- **NanoBot**, **Hermes Agent**, **IronClaw**: These projects have strong, focused communities but are slightly less chaotic. NanoBot and IronClaw are merging PRs at a high rate (15+ merged/closed), while Hermes is battling a wave of platform-specific bugs. They are stabilizing their core features.

**Tier 3 (Moderate to Low Activity, Stabilizing):**
- **PicoClaw**, **NanoClaw**: Active but at a lower scale. PicoClaw's nightly releases suggest ongoing experimentation, while NanoClaw is addressing specific pain points (budget exhaustion, Slack URLs).
- **NullClaw**, **LobsterAI**, **Moltis**, **TinyClaw**, **ZeptoClaw**: These projects are in maintenance or early-stage mode. They have small (or single) active PRs and low issue volume. TinyClaw and ZeptoClaw are nearly inactive. Their development is likely reactive to community contributions rather than proactive.

#### 7. Trend Signals

The aggregate community feedback from these digests reveals several powerful trends for AI agent developers:

1.  **"Last Mile" is the Biggest Gap**: The hardest problems are not agent intelligence but delivery reliability. Users across **OpenClaw**, **Hermes**, **NanoClaw**, and **CoPaw** are highly frustrated by broken channel adapters (Telegram, QQ Bot, WeCom). A developer who can build a robust, self-healing, and feature-rich platform adapter will have immense value.

2.  **Cost Optimization is Now a Core Feature**: Users are no longer just paying for API tokens; they are paying for wasted inference. **OpenClaw** (DeepSeek cache loss costing $6/hour), **NanoBot** (token-budget overflow), **Hermes** (Claude Max billing), and **NanoClaw** (silent budget exhaustion) all indicate that **token budgeting** and **cost transparency** are required, not optional, features.

3.  **Security is Moving from "Good Idea" to "Hard Requirement"**: The rise of CRITICAL security advisories (PicoClaw), keychain isolation (CoPaw), and credential proxy compliance worries (NanoClaw) signals that enterprises and power users will not tolerate insecure agent deployments. A developer who focuses on supply-chain security (SBOMs, provenance as in ZeroClaw) or zero-trust credential management will have a distinct advantage.

4.  **Persistent Task Execution is the Next Battleground**: The push for **cron subagents** (NullClaw, OpenClaw), **automation management** (NanoBot, IronClaw), and **resuming long sessions** (ZeroClaw) shows the community wants agents to be proactive workers, not just reactive chatbots. Reliability of scheduled tasks is a clear unmet need.

5.  **The Rise of the "Reasoning Model" Meta-Issue**: Multiple projects (**CoPaw**, **OpenClaw**, **NullClaw**) are struggling with how to handle the new generation of "thinking" or "reasoning" models (Gemini thoughts, Kimi thinking, Ollama reasoning levels). The ecosystem is still grappling with how to properly parse, stream, and display these non-standard response formats, creating a short-term integration window.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-06-17

## 1. Today's Overview

NanoBot saw **very high activity** on 2026-06-17, with **24 PRs** updated (14 merged/closed) and **9 issues** touched (6 closed). Momentum centred on stability fixes, build tooling improvements, and the first merge of a major WebUI feature (Automation management). Community contributions drove most of the changes—a healthy sign of project engagement. No new release was cut today, but the dense patch set suggests a release candidate is imminent.

## 2. Releases

**None.** The project has not published a new version since the last release (earlier data not shown). Given the volume of merged fixes and features, a patch/minor release is likely within days.

## 3. Project Progress – Merged/Closed PRs Today

14 PRs were merged or closed today. Key advances:

- **🆕 WebUI Automation Management** – [#4330](https://github.com/HKUDS/nanobot/pull/4330) (merged): adds a first-class Automation section with filtering, searching, editing, pausing/resuming, and deletion. Protected system jobs remain read-only.
- **🔧 Recent-History Digest Capped by Tokens** – [#4352](https://github.com/HKUDS/nanobot/pull/4352) (merged): fixes a long-standing issue where CJK/code-heavy history could overflow the system prompt token budget.
- **🛠️ macOS Installer Fix (PEP 668)** – [#4368](https://github.com/HKUDS/nanobot/pull/4368) (merged): avoids system-wide `pip` on externally managed Python environments, preferring virtualenv/uv/pipx.
- **⏰ Idle Auto-Compact Default 15 min** – [#4370](https://github.com/HKUDS/nanobot/pull/4370) (merged): changes the default from `0` (off) to `15` minutes, enabling automatic memory compaction after idle periods.
- **💬 Dream Empty-Run Explained** – [#4369](https://github.com/HKUDS/nanobot/pull/4369) (merged): replaces the opaque “no history” response with an actionable description pointing users to idle auto-compact.
- **📁 `.gitignore` for Bridge deps** – [#4355](https://github.com/HKUDS/nanobot/pull/4355) (merged): prevents accidental commit of compiled bridge `node_modules`.
- **🔄 Duplicate User Turn on Retry Fixed** – [#4358](https://github.com/HKUDS/nanobot/pull/4358) (merged): closes [#4079](https://github.com/HKUDS/nanobot/issues/4079) by passing `persist_user_message=False` during empty-response retries.
- **🕒 Stream Idle Timeout Validation** – [#4363](https://github.com/HKUDS/nanobot/pull/4363) (merged): centralises timeout parsing and clamps invalid/extreme values (closes [#4065](https://github.com/HKUDS/nanobot/issues/4065)).
- **🌐 WebUI LAN Connection Fix** – [#4364](https://github.com/HKUDS/nanobot/pull/4364) (merged): fixes “Opening new chat…” hang when accessing the dev server from a local network IP.
- **🧠 Kimi K2.7 Thinking Support** – [#4361](https://github.com/HKUDS/nanobot/pull/4361) (merged): adds model IDs to the thinking allowlist and handles the Code variant properly.
- **📖 Curl Installer Docs Improvement** – [#4365](https://github.com/HKUDS/nanobot/pull/4365) (merged): switches from `sh -c "$(curl ...)"` to `curl ... | sh` to avoid shell mangling in Dockerfiles.

## 4. Community Hot Topics

- **📌 Issue #4360 – Installer “end of file unexpected”** (9 comments, closed).  
  A fresh Debian 13 container hit a shell syntax error in the installer. The community quickly diagnosed the problem (embedded script piping) and it was resolved.  
  [Issue #4360](https://github.com/HKUDS/nanobot/issues/4360)

- **📌 Issue #4242 – Dream disabled still injects full history** (1 comment, open).  
  A critical behavioural bug: setting `dream.enabled = false` does not prevent the Dream cursor from injecting all chat history into the system prompt via the “Recent History” section. The root cause is that the cursor is never advanced, so every turn reloads old entries. No maintainer response yet.  
  [Issue #4242](https://github.com/HKUDS/nanobot/issues/4242)

- **📌 PR #4350 – Keenable search provider** (open, 0 comments).  
  A community PR adding a new research-driven web search provider – a clear signal that users desire more search flexibility. No maintainer review yet.  
  [PR #4350](https://github.com/HKUDS/nanobot/pull/4350)

## 5. Bugs & Stability

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#4375](https://github.com/HKUDS/nanobot/issues/4375) | **High** | Git commands (`add`, `commit`, `push`) blocked by workspace security policy even inside allowed paths. Open, no fix PR yet. | ❌ Unresolved |
| [#4374](https://github.com/HKUDS/nanobot/issues/4374) | **Medium** | SOUL.md/USER.md are read from per-turn project path but written to default workspace – asymmetrical behaviour when using WebUI project workspaces. Open, no fix. | ❌ Unresolved |
| [#4366](https://github.com/HKUDS/nanobot/issues/4366) | **Medium** | Local model servers (Ollama, vLLM) break when machine has HTTP_PROXY set – all traffic routed through proxy. Closed, but fix PR [#4367](https://github.com/HKUDS/nanobot/pull/4367) is open. | ✅ Fix PR exists |
| [#4065](https://github.com/HKUDS/nanobot/issues/4065) | **Low** | Invalid `NANOBOT_STREAM_IDLE_TIMEOUT_S` can crash streaming. Closed, fix merged in [#4363](https://github.com/HKUDS/nanobot/pull/4363). | ✅ Fixed |
| [#4079](https://github.com/HKUDS/nanobot/issues/4079) | **Low** | Empty-response retry can duplicate user turns. Closed, fix merged in [#4358](https://github.com/HKUDS/nanobot/pull/4358). | ✅ Fixed |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | **Low** | Agent wrongly reports missing “sustained goal” context. Closed (likely resolved). | ✅ Fixed |

## 6. Feature Requests & Roadmap Signals

- **🆕 Keenable Search Provider** – [PR #4350](https://github.com/HKUDS/nanobot/pull/4350) (open). Likely to be merged in the next release given the positive reception of provider additions.  
- **📋 Automation Management UI** – [PR #4330](https://github.com/HKUDS/nanobot/pull/4330) (merged). Already in main; will be part of the next release.  
- **🧩 Cache Breakpoint for System Prompt** – [PR #4371](https://github.com/HKUDS/nanobot/pull/4371) (open). Improves caching efficiency by isolating the stable prefix from the growing recent-history section. High value for token-heavy users.  
- **🔒 Read-only Roots for Write Tools** – [PR #4053](https://github.com/HKUDS/nanobot/pull/4053) (open since May 29). Prevents write tools from modifying media directories or extra allowed roots. A security-critical improvement still awaiting review.  
- **🌎 Proxy Awareness for Local Endpoints** – [PR #4367](https://github.com/HKUDS/nanobot/pull/4367) (open). Fixes a common pain point for developers behind corporate proxies. Likely to be included soon.

**Prediction for next version:** Automation UI, Keenable search, cache breakpoint, idle auto-compact default, proxy fix, and several stream/timeout hardening patches.

## 7. User Feedback Summary

**Positive signals:**
- The community is actively contributing (24 PRs in 24h) and bugs are being triaged quickly (6 issues closed today).
- The new Automation UI was well received (no negative comments recorded).
- Several long-standing annoyances (duplicate user turns, stream timeout crashes) were fixed.

**Pain points expressed:**
- **Installer fragility:** The Debian 13 shell error (#4360) highlights a need for more robust installation scripts across distributions.
- **Workspace security friction:** Git operations inside allowed paths being blocked (#4375) is a frustrating developer experience.
- **Dream/history confusion:** Users are confused by the interaction between `dream.enabled`, idle auto-compact, and the “Recent History” section (#4242, #4369). The new explanatory message in #4369 should help, but #4242 remains unresolved.
- **Proxy/LAN issues:** Users behind corporate proxies or using LAN access face silent failures (#4366, #4364). Both have fixes in progress or merged.
- **Workspace read/write asymmetry:** The SOUL.md asymmetry (#4374) undermines trust in project workspaces – user expects the agent to persist identity changes back to the project directory, not to the default workspace.

**Satisfaction indicators:** The fast turnaround on bug fixes (e.g., #4065 → #4363 merged same day) shows maintainers are responsive, which correlates with high contributor retention.

## 8. Backlog Watch

- **[Issue #4242](https://github.com/HKUDS/nanobot/issues/4242)** – Dream disabled still injects full history (open since June 8, 1 comment). No maintainer response. A relatively straightforward fix (check `dream.enabled` before injecting cursor) but could have subtle interactions with the new cache breakpoint PR (#4371). High priority for users who disabled Dream.

- **[PR #3662](https://github.com/HKUDS/nanobot/pull/3662)** – Avoid network loads during token estimation (open since May 6). Aims to cache `tiktoken` encoders locally to prevent offline failures. Unreviewed for over 6 weeks.

- **[PR #4053](https://github.com/HKUDS/nanobot/pull/4053)** – Keep read-only roots out of write paths (open since May 29). Security enhancement; no maintainer activity. Could block accidental file deletion in media directories.

- **[Issue #4375](https://github.com/HKUDS/nanobot/issues/4375)** – Git command blocked by security policy (new today). No fix PR yet. Needs immediate attention because it blocks a core developer workflow.

---

*Generated by AI (2026-06-17) from GitHub data of HKUDS/nanobot.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-17

## 1. Today's Overview
The Hermes Agent project is experiencing **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. The majority of issues remain open (46 open issues, 45 open PRs), indicating a vibrant community actively reporting bugs and proposing features. No new releases were cut today. The week’s work reflects a strong focus on **platform adapter reliability** (especially WeCom, QQ Bot, Feishu, and Slack), **multi-tenant and multi-agent architecture**, and **desktop UI stability**. The project's health appears robust, though several long-standing items remain unresolved.

## 2. Releases
No new releases were published today. The latest stable version remains Hermes v0.16.0 (referenced in issue #47360). No breaking changes or migration notes apply.

## 3. Project Progress
Five pull requests were closed or merged in the last 24 hours:

- **[#47562 – fix(feishu): extract table row data from interactive cards for reply-to context](https://github.com/NousResearch/hermes-agent/pull/47562)** (closed)  
  Fixes a gap where table data from Feishu interactive cards was lost in reply-to contexts.

- **[#47575 – chore(deps): temporarily disable Dependabot updates](https://github.com/NousResearch/hermes-agent/pull/47575)** (closed)  
  Workaround for duplicate PR interactions; configuration left intact for easy re-enablement.

- **[#47513 – [Feature]: Slack: render clarify choices as Block Kit buttons](https://github.com/NousResearch/hermes-agent/pull/47513)** (closed as duplicate)  
  Duplicate of #47529; the Slack Button Kit feature request is being consolidated.

- **[#47529 – [Feature]: Slack: render clarify choices as Block Kit buttons](https://github.com/NousResearch/hermes-agent/pull/47529)** (closed)  
  Official feature request; counterpart to Discord’s #19111. Community strongly supports this (+9 reactions on original #8552).

- **[#47360 – [Bug]: Discord gateway connects but never receives MESSAGE_CREATE events](https://github.com/NousResearch/hermes-agent/pull/47360)** (closed)  
  Duplicate bug report; underlying issue may be related to intents or bot permissions.

Additionally, the following open PRs represent active progress:

- **#47027** – Multi-agent orchestration following the IBM CICS model (three-layer architecture: AgentContext, RoutingTable, ContextPool).
- **#47576** – Three new optional skills: graphify (knowledge graphs), ui-ux-pro-max (UI/UX prototyping), and impl-validator (verification gates).
- **#47580** – Refreshes stale skill command caches to prevent “unknown command” errors.
- **#47583** – Denies reading secret-bearing credential files (e.g., cloud service-account JSON keys, private keys) via the file tool.
- **#47586** – Three-layer fix for QQ Bot WebSocket zombie connections: heartbeat ACK tracking, message receipt watchdog.

## 4. Community Hot Topics
The most active discussions (by comment count and reactions) reveal the community’s central concerns:

| Issue | Comments | Reactions | Topic |
|-------|----------|-----------|-------|
| [#34352 – Solving the Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352) | 7 | 0 | Memory hooks bypass isolation; NimbleCoAI proposes production-proven fix. Underlying need: **enterprise-grade tenant isolation** for multi-agent deployments. |
| [#8552 – Slack platform: use Block Kit markdown block type](https://github.com/NousResearch/hermes-agent/issues/8552) | 7 | 9 | Legacy mrkdwn doesn’t support tables or rich formatting. Community strongly backs **modern Slack interactions** (buttons, modals). |
| [#40014 – Claude Code OAuth still hits pay-per-token endpoint](https://github.com/NousResearch/hermes-agent/issues/40014) | 4 | 0 | Max/Pro subscription users are incorrectly billed for “extra usage” instead of using quota. **Cost optimization** and **proper OAuth routing** are critical. |
| [#19821 – QQ Bot WebSocket silently dies](https://github.com/NousResearch/hermes-agent/issues/19821) | 3 | 0 | Zombie connections leave bot unresponsive for 18+ hours. A fix is in flight (#47586). |
| [#39609 – Tasks auto-promote from blocked to ready with no actor](https://github.com/NousResearch/hermes-agent/issues/39609) | 3 | 1 | Kanban workflow bypasses human approval gates. **Audit trail** and **state machine discipline** needed. |
| [#47134 – MCP reload crashes gateway via killpg SIGTERM](https://github.com/NousResearch/hermes-agent/issues/47134) | 3 | 0 | High-severity bug (P1) – `/reload-mcp` terminates the entire session. Patch expected soon. |

**Analysis:** The community is demanding **multi-tenant isolation** (both at memory and orchestration layers), **proper subscription billing integration** (especially for Claude Max), and **more interactive platform UX** (Slack buttons, tables). The surge of WeCom-related issues (4 new today) indicates growing enterprise adoption in Asian markets.

## 5. Bugs & Stability
Newly reported bugs (last 24 hours) are ranked by priority:

| Issue | Priority | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#47134 – /reload-mcp crashes gateway](https://github.com/NousResearch/hermes-agent/issues/47134) | P1 | killpg sends SIGTERM to gateway’s own process group | No (PR expected) |
| [#47571 – WeCom send() hard-truncates at 4000 chars](https://github.com/NousResearch/hermes-agent/issues/47571) | P2 | Breaks plugin-level segmentation (OLG) | No |
| [#47564 – WeCom reconnection dead window 57-79s](https://github.com/NousResearch/hermes-agent/issues/47564) | P2 | Errcode 846609 not triggering reconnection | No |
| [#47539 – Telegram typing indicator stuck forever](https://github.com/NousResearch/hermes-agent/issues/47539) | P2 | Orphaned `_keep_typing` asyncio task | No |
| [#47573 – WeCom duplicate messages on lost ACK](https://github.com/NousResearch/hermes-agent/issues/47573) | P2 | Duplicate delivery due to missing dedup | [#47585](https://github.com/NousResearch/hermes-agent/pull/47585) |
| [#47572 – WeCom reconnection fails silently](https://github.com/NousResearch/hermes-agent/issues/47572) | P2 | No logging of success/failure after reconnect | No |
| [#47500 – Desktop preview triggers custom protocol handlers](https://github.com/NousResearch/hermes-agent/issues/47500) | P2 | Windows pop-ups on hover/click | No |
| [#47498 – Desktop crash “Maximum call stack size exceeded”](https://github.com/NousResearch/hermes-agent/issues/47498) | P3 | Photo attachment causes infinite recursion | No |
| [#41737 – Linux desktop update freezes at 100%](https://github.com/NousResearch/hermes-agent/issues/41737) | P3 | Electron main process never exits after update | No |
| [#47569 – Windows install venv lock](https://github.com/NousResearch/hermes-agent/issues/47569?-> PR) | P2 | `install.ps1` can’t recreate venv due to locked Python processes | [#47569](https://github.com/NousResearch/hermes-agent/pull/47569) (open) |

**Platform-specific troubles dominate:** WeCom (4 new bugs), Telegram (1), Discord (1, already duplicate), QQ Bot (ongoing #19821). The desktop app also shows regressions (photo crash, update freeze, zoom scaling missing). No P0 or security exploits reported today; the P1 MCP crash is the most severe.

## 6. Feature Requests & Roadmap Signals
New feature requests (last 24h) and notable older items:

- **#47517 / #47477 – WhatsApp Group Messaging Skill on Termux** – Community-provided one-file guide for WhatsApp group sending via Hermes Skill. Signals demand for **WhatsApp integration** beyond direct messaging.
- **#47499 – UI zoom/scale controls for desktop** – High-DPI and accessibility need.
- **#38849 – Quick workspace switcher on Desktop status bar** – Multi-profile workflow ease.
- **#39020 – Dedicated Providers settings section** – per-provider API key management in GUI.
- **#44637 – Runtime-enforced verification gates for Skills** – Deterministic enforcement for high-stakes tasks (code, deployments).
- **#47027 (PR) – Multi-agent orchestration (CICS model)** – Single-daemon multi-agent support. Likely to be merged in next version.
- **#47199 – MCP provider for Claude Code subscription** – Local backend without API keys; addresses the #40014 billing pain point.

**Prediction:** The next minor release (v0.17.0) will likely include **multi-agent orchestration** (#47027), **Slack Block Kit buttons** (#47529), **improved WeCom resilience** (multiple fixes in PR pipeline), and the **secret credential blocking** (#47583). Desktop accessibility and provider settings may land in v0.18.0.

## 7. User Feedback Summary
**Pain points (expressed repeatedly):**
- “Multi-tenant memory isolation is impossible without forking core” – NimbleCoAI (#34352)
- “Claude Max subscription billing is broken – we’re paying extra” – harsh-matchmyflight (#40014)
- “QQ Bot goes zombie for 18+ hours” – linxunxr (#19821)
- “Tasks skip human approval; our deployment risk is high” – bill3wits (#39609)
- “MCP reload kills my session” – pioneerAlone (#47134)
- “Desktop app freezes after update on Linux” – Zerodys (#41737)
- “WeCom truncation and reconnection problems make production use unreliable” – tobiglevent001 (#47571, #47564, #47572, #47573)

**Positive signals:**
- Strong community contributions: one-file WhatsApp guides, production multi-tenant patches, optional skills, and thorough platform adapter fixes.
- PRs are being reviewed and merged regularly (5 today), indicating responsive maintainers.

**Overall sentiment:** Users are enthusiastic about Hermes’ extensibility but increasingly frustrated with platform-specific reliability issues. The project’s rapid evolution (50 open issues/day) shows it’s a vital, fast-moving ecosystem.

## 8. Backlog Watch
Long-standing issues with significant community engagement but no recent maintainer response:

| Issue | Opened | Comments | Reason for attention |
|-------|--------|----------|----------------------|
| [#34352 – Solving the Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352) | 2026-05-29 | 7 | Critical for enterprise adoption; includes production-ready fix. No maintainer comment yet. |
| [#8552 – Slack Block Kit support](https://github.com/NousResearch/hermes-agent/issues/8552) | 2026-04-12 | 7 | 9 👍; duplicate PRs #47513/#47529 closed but the original issue remains open. |
| [#19821 – QQ Bot WebSocket zombie](https://github.com/NousResearch/hermes-agent/issues/19821) | 2026-05-04 | 3 | Fix PR #47586 is open but not yet merged. Issue still open. |
| [#36801 – Long sessions grow unbounded context](https://github.com/NousResearch/hermes-agent/issues/36801) | 2026-06-01 | 2 | Proactive compaction missing for Codex path. No assignee. |
| [#40095 – Kanban workers crash with TUI display](https://github.com/NousResearch/hermes-agent/issues/40095) | 2026-06-05 | 1 | Headless worker launches TUI on no TTY, exits without agent loop. |

**Recommendation:** Maintainers should prioritize #34352 (multi-tenancy) and #8552 (Slack UX) as they represent the highest comment and reaction counts. The QQ Bot zombie issue (#19821) has a fix ready and should be merged promptly to resolve a long-standing reliability problem.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-17

## 1. Today's Overview
Project activity remains high with 15 issues and 15 PRs updated in the last 24 hours. A new nightly build (v0.3.0-nightly.20260617) was released, incorporating recent fixes merged from `main`. Security vulnerability reports continue to dominate the open issue tracker, with 11 security-related items opened on June 9 still open and stale. On the positive side, 12 PRs were merged or closed today, including fixes for critical stability issues (panic recovery, Telegram forum topics, context compression) and new feature additions (remote cron commands, out-of-tree channel hooks). Community engagement is moderate, with the most commented feature request (streaming HTTP support) showing sustained interest.

## 2. Releases
- **nightly (v0.3.0-nightly.20260617.a16a1e15)** — Automated unstable build tracking the `main` branch. No breaking changes or migration notes provided.  
  [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

## 3. Project Progress
**12 PRs were merged/closed today**, spanning bug fixes, feature additions, and code quality improvements. Key highlights:

- **Feature: Remote cron commands** ([#3137](https://github.com/sipeed/picoclaw/pull/3137)) — Adds `tools.cron.command_allowed_remotes` config to restrict cron execution to selected remote channels.
- **Feature: Out-of-tree channel registration hook** ([#3120](https://github.com/sipeed/picoclaw/pull/3120)) — Enables third-party channels to register configuration side without forking PicoClaw.
- **Fix: Telegram forum topics** ([#3135](https://github.com/sipeed/picoclaw/pull/3135)) — Resolves issue where replies defaulted to `#General` instead of the specific forum thread.
- **Fix: Panic recovery in core goroutines** ([#3132](https://github.com/sipeed/picoclaw/pull/3132)) — Adds `defer-recover` to critical execution paths to prevent process crashes.
- **Fix: Seahorse tools JSON marshal errors** ([#3130](https://github.com/sipeed/picoclaw/pull/3130)) — Returns descriptive error instead of empty string on marshalling failure.
- **Fix: Explicitly ignore Close() errors on directory file descriptors** ([#3127](https://github.com/sipeed/picoclaw/pull/3127), [#3129](https://github.com/sipeed/picoclaw/pull/3129)) — Code quality improvements.
- **Fix: Web UI session history display** ([#2990](https://github.com/sipeed/picoclaw/pull/2990)) — Now shows full conversation history instead of only the last user message.
- **Fix: Context compression percent config** ([#2988](https://github.com/sipeed/picoclaw/pull/2988)) — `/context` command now respects `summarize_token_percent` setting.
- **Fix: Tool calls dropped during streaming** ([#2987](https://github.com/sipeed/picoclaw/pull/2987)) — Ensures `tool_calls` are not filtered out.
- **Fix: Retry empty LLM responses** ([#2983](https://github.com/sipeed/picoclaw/pull/2983)) — Retries when provider returns semantically empty assistant message.

## 4. Community Hot Topics
- **#2404 – Streaming HTTP request config** ([link](https://github.com/sipeed/picoclaw/issues/2404))  
  *Enhancement, 12 comments, 1 👍*  
  The most active issue. Users request a simple `"streaming": true` config option to enable server-sent events for LLM backends, analogous to the OpenAI Python client. This feature would directly improve user experience for real-time applications.

- **#3134 – `su -c 'echo OK'` not supported** ([link](https://github.com/sipeed/picoclaw/issues/3134))  
  *Bug, 2 comments, closed*  
  User reports that this common shell pattern fails in the agent gateway. The issue was closed quickly, suggesting a fix or workaround was provided.

- **Security advisories batch** (multiple issues, all 1 comment each)  
  A series of 11 vulnerability reports by YLChen-007 (e.g., [#3078](https://github.com/sipeed/picoclaw/issues/3078), [#3075](https://github.com/sipeed/picoclaw/issues/3075), [#3072](https://github.com/sipeed/picoclaw/issues/3072)) detail SSRF bypasses, authorization bypasses, CSRF, and symlink races. These have received only initial maintainer acknowledgement and are now stale.

## 5. Bugs & Stability
**New bugs reported today (updated in last 24h):**

| Issue | Severity | Status | Notes |
|-------|----------|--------|-------|
| [#3134](https://github.com/sipeed/picoclaw/issues/3134) `su -c 'echo OK'` not supported | Medium | Closed | Likely fixed or acknowledged. User reported agent crash. |
| [#3110](https://github.com/sipeed/picoclaw/issues/3110) Telegram forum topic reply defaulting to #General | High | Closed | Fixed by PR [#3135](https://github.com/sipeed/picoclaw/pull/3135) today. |

**Stability improvements merged today:**
- Panic recovery in goroutines ([#3132](https://github.com/sipeed/picoclaw/pull/3132)) prevents process-wide crashes.
- Retry of empty LLM responses ([#2983](https://github.com/sipeed/picoclaw/pull/2983)) improves robustness against misbehaving providers.

## 6. Feature Requests & Roadmap Signals
- **Streaming HTTP requests** ([#2404](https://github.com/sipeed/picoclaw/issues/2404)) — A mature, well-discussed feature request. Likely candidate for v0.3.1 or v0.4.0 given its simplicity and high user demand.
- **Remote cron command restrictions** ([#3137](https://github.com/sipeed/picoclaw/pull/3137)) — Already merged, enabling safer cron execution across channels.
- **Out-of-tree channel registration** ([#3120](https://github.com/sipeed/picoclaw/pull/3120)) — Merged, opens ecosystem for community plugins.
- **Inline data URL handling** (PR [#3115](https://github.com/sipeed/picoclaw/pull/3115) open) — Prevents session history corruption from `data:` URIs in tool output; addresses a subtle bug.

## 7. User Feedback Summary
- **Pain point:** Users encountering `su -c` failures ([#3134](https://github.com/sipeed/picoclaw/issues/3134)) highlights limited shell integration for system administration tasks.
- **Pain point:** Telegram forum topics not working correctly ([#3110](https://github.com/sipeed/picoclaw/issues/3110)) frustrated users expecting proper thread support.
- **Positive sentiment:** The rapid merge of the Telegram fix and the panic recovery PR suggests responsive maintainers.
- **Feature desire:** The streaming request feature request ([#2404](https://github.com/sipeed/picoclaw/issues/2404)) indicates users want lower-latency, real-time interactions with LLMs.

## 8. Backlog Watch
**Stale security issues (all opened June 9, updated June 16 but lacking maintainer response beyond initial ack):**
- [#3078](https://github.com/sipeed/picoclaw/issues/3078) – SSRF bypass via HTTP proxy environment config
- [#3075](https://github.com/sipeed/picoclaw/issues/3075) – Untrusted `skills/` metadata auto-loaded into system prompt
- [#3072](https://github.com/sipeed/picoclaw/issues/3072) – CSRF in launcher password setup
- [#3071](https://github.com/sipeed/picoclaw/issues/3071) – Unauthorized gateway config reload via WebSocket
- [#3068](https://github.com/sipeed/picoclaw/issues/3068) – MQTT `allow_from` spoofing

These represent significant attack surface and have been unaddressed for over a week. Urgent maintainer attention is needed.

**Other stale items:**
- [#2404](https://github.com/sipeed/picoclaw/issues/2404) – Streaming config (open since April 7, 2026; still no implementation)
- PR [#3116](https://github.com/sipeed/picoclaw/pull/3116) – `turn.done` lifecycle signaling (open since June 12, no recent comments)
- PR [#3115](https://github.com/sipeed/picoclaw/pull/3115) – Inline data URL fix (open since June 12)
- PR [#3136](https://github.com/sipeed/picoclaw/pull/3136) – Gemini `thought_signature` fix (open today, awaiting merge)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-17

## Today's Overview

Activity remains moderate with **6 issues updated** (5 open, 1 closed) and **5 pull requests updated** (1 open, 4 merged/closed) in the last 24 hours. No new releases were published. The day’s highlights include a merged fix for silent‑drop of budget‑exhausted LLM turns, a self‑healing fix for the Tailscale‑Docker routing skill, and the closure of a webchat skill PR. Community attention is split between a lingering compliance concern about credential proxying and a newly reported Slack URL‑mangling bug. Overall, the project shows steady maintenance velocity with a blend of bug fixes, documentation improvements, and feature proposals.

## Releases

No new releases today.

## Project Progress

Four pull requests were merged or closed in the last 24 hours:

- **[#2069 – Skill/webchat v1](https://github.com/nanocoai/nanoclaw/pull/2069)** (closed)  
  Adds a WebChat channel skill, providing a new integration for agent interaction via browser chat.

- **[#2782 – fix: make tailscale-docker routing service self-healing](https://github.com/nanocoai/nanoclaw/pull/2782)** (merged)  
  Fixes a bug where the `fix-tailscale-docker-routing` skill only applied the Docker bridge ip rule at boot; Tailscale could flush the rule mid‑session, breaking connectivity. The fix replaces the `oneshot` systemd unit with a continuously running service (using `ip monitor` or periodic re‑apply) to recover automatically.

- **[#2759 – fix(agent-runner): deliver budget/billing error turns instead of dropping them](https://github.com/nanocoai/nanoclaw/pull/2759)** (merged)  
  Closes [Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751). When an LLM turn exhausts its token/spend budget, the agent‑runner now surfaces a user‑facing error instead of silently dropping the turn.

- **[#2775 – docs(changelog): clarify the OneCLI gateway is a separate, operator-driven upgrade](https://github.com/nanocoai/nanoclaw/pull/2775)** (merged)  
  Corrects a misleading `[BREAKING]` note in the changelog by clarifying that updating NanoClaw does _not_ automatically upgrade the OneCLI gateway on existing installations.

One PR remains open: **[#2780 – feat(upgrade-state): env opt-out for the startup tripwire (managed fleets)](https://github.com/nanocoai/nanoclaw/pull/2780)** — introduces `NANOCLAW_DISABLE_UPGRADE_TRIPWIRE=1` to let immutable‑image deployments skip the startup upgrade check.

## Community Hot Topics

- **[Issue #1669 – Does Credential Proxy implementation risk Anthropic account bans?](https://github.com/nanocoai/nanoclaw/issues/1669)**  
  Since April 2026, this question has drawn attention (updated today). The author raises a compliance concern about Anthropic’s prohibition on OAuth reverse‑proxies. With only one comment, the community seems to be waiting for a maintainer assessment. The underlying need is clarity on the legal/ToS risk of the Credential Proxy before deploying it in production.

- **[Issue #2779 – Slack: @handles inside URLs get mangled into broken mentions](https://github.com/nanocoai/nanoclaw/issues/2779)**  
  Reported yesterday, this functional bug causes URLs containing an `@handle` (e.g., HackMD, Mastodon profiles) to be rewritten by Slack into broken mentions. This is a clear user pain point as agents cite or reference such links.

- **[Issue #2751 – Budget-exhausted LLM turns are silently dropped](https://github.com/nanocoai/nanoclaw/issues/2751)** (closed, now fixed by PR #2759)  
  Although closed, this issue had several token/billing‑related concerns that were quickly addressed. The community’s prompt reporting shows high sensitivity to spending limits and silent failures.

## Bugs & Stability

| Issue | Severity | Description | Status |
|-------|----------|--------------|--------|
| [#2779 – Slack URL @handle mangling](https://github.com/nanocoai/nanoclaw/issues/2779) | **Medium** | URLs containing `@` in the path are incorrectly rewritten into Slack @‑mentions, breaking links. No fix PR yet. | Open |
| [#2784 – container-runner session staleness miss](https://github.com/nanocoai/nanoclaw/issues/2784) | **Medium** | The source‑staleness check only watches `index.ts`, ignoring changes to `ipc-mcp-stdio.ts` and other files. This can cause outdated agent code to run in sessions. | Open |
| [#2751 – Budget exhausted drops](https://github.com/nanocoai/nanoclaw/issues/2751) | **High** (now fixed) | Silently dropping billing errors leaves users confused. Merged PR #2759 resolves this. | Closed/fixed |
| [#2783 – docs/SECURITY.md outdated](https://github.com/nanocoai/nanoclaw/issues/2783) | **Low** | The security documentation describes a retired v1 trust model and references a non‑existent skill. Misleading for new users. | Open |

The most critical active bugs are the Slack URL mangling (#2779) and the container‑runner staleness check (#2784); neither has an associated fix PR yet.

## Feature Requests & Roadmap Signals

- **[Issue #2781 – Support NANOCLAW_NATIVE_CREDENTIALS to bypass OneCLI](https://github.com/nanocoai/nanoclaw/issues/2781)**  
  Request to allow downstream packagers to inject provider credentials directly via environment variables, skipping OneCLI. This would enable usage in sandboxed environments where OneCLI is not configured. Likely candidate for a next minor release given its clear use case.

- **[PR #2780 – Env opt-out for upgrade tripwire](https://github.com/nanocoai/nanoclaw/pull/2780)**  
  Already in open PR form, as noted above. If merged, it will appear in the next patch release.

- **[Issue #1669 – Credential Proxy ban risk](https://github.com/nanocoai/nanoclaw/issues/1669)**  
  Though not a feature request, a maintainer response could influence future proxy design or documentation.

## User Feedback Summary

Based on recent issues and PRs, users are expressing:

- **Pain points**:  
  - Silent budget exhaustion (#2751) – now fixed.  
  - Broken Slack URLs when agents reference `@handle` paths (#2779).  
  - Concern about ToS compliance when using Credential Proxy with Anthropic (#1669).  
  - Container sessions running stale code due to incomplete staleness detection (#2784).

- **Use cases**:  
  - Managed fleet deployments that require immutable images and wish to disable upgrade checks (#2780).  
  - Sandboxed/shared environments that need native credential injection without OneCLI (#2781).  
  - Multi‑skill setups needing up‑to‑date agent code in sessions (#2784).

- **Satisfaction**: The quick turnaround on the budget‑drop fix (#2759) demonstrates responsive maintainers. However, the open Slack and container‑runner bugs, plus the lingering credential proxy question, indicate areas needing attention.

## Backlog Watch

- **[Issue #1669 – Credential Proxy ban risk](https://github.com/nanocoai/nanoclaw/issues/1669)**  
  Created **2026-04-06**, last updated 2026-06-16, still open with only one comment. This compliance/ToS question has been unanswered for over two months. A maintainer response or official guidance would help reduce uncertainty for adopters.

- **[Issue #2783 – docs/SECURITY.md outdated](https://github.com/nanocoai/nanoclaw/issues/2783)**  
  Created yesterday, but the documentation drift has likely existed for longer. While low severity, it is the canonical security doc and should be updated to reflect the v2 role‑based model.

No other long‑unanswered PRs were observed; the remaining open issues are recent.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest – 2026-06-17

### 1. Today's Overview

Activity on NullClaw remains moderate, with **2 open issues** and **3 open pull requests** updated in the last 24 hours. No releases were published today. The majority of activity centers on two bug reports—one involving incomplete answers from local Ollama models and another concerning scheduler access—with a dedicated fix PR already opened for the scheduler issue. The long‑running **cron subagent feature** (PR #783) received its most recent update on the same day, indicating continued development momentum. Overall, the project is actively addressing user‑reported problems while advancing substantial new functionality.

### 2. Releases

*No new releases were published today.*

### 3. Project Progress

No pull requests were merged or closed today. However, three open PRs saw activity:

- **#959** – `fix(cron): persist paired token for scheduler tool access (#839)` – A direct fix for the scheduler access bug (see Section 5), this PR introduces encrypted token persistence to enable secure cron/schedule tool authorization.
- **#958** – `fix(teams): accept lowercase serviceurl JWT claim and raise JWKS fetch cap` – Corrects two authentication issues that cause Bot Framework connector‑token validation failures for MS Teams integration.
- **#783** – `feat(cron): cron subagent, run history, JSON output, security hardening` – A large feature adding a DB‑backed cron engine, job types (skill/agent/shell), timezone support, and alerting. Last updated today, signaling ongoing work.

### 4. Community Hot Topics

The most discussed item in the last 24 hours is:

- **Issue #952** – *[bug] Local model using ollama returns incomplete answers*  
  Author: bloodgroup-cplusplus | 2 comments | 0 reactions  
  [GitHub](https://github.com/nullclaw/nullclaw/issues/952)  

  The reporter provides a screenshot showing that the agent, when backed by a locally pulled Gemma model via Ollama, fails to complete sentences and returns truncated responses. This is a common pain point for users running local models, and the lack of an immediate fix suggests the team is still investigating.

Additionally, **Issue #839** – *bug: bit has no access to scheduler !?* (1 comment, open since April) – has gained renewed attention because **PR #959** attempts to resolve it. This pairing of issue and fix often drives community interest.

### 5. Bugs & Stability

Two open bugs were updated today:

| Severity | Bug | ID | Status | Fix PR? |
|----------|-----|----|--------|---------|
| Moderate | Local model (Ollama) returns incomplete answers | [#952](https://github.com/nullclaw/nullclaw/issues/952) | Open, no fix yet | None |
| High | Bit has no access to scheduler | [#839](https://github.com/nullclaw/nullclaw/issues/839) | Open, fix in progress | [#959](https://github.com/nullclaw/nullclaw/pull/959) |

- **#952 (Moderate)**: The agent’s response truncation undermines usability for local‑model users. The issue is recent (June 11) and still awaiting a root‑cause analysis. No associated fix PR exists.
- **#839 (High)**: The inability for a `bit` to access the scheduler is a functional regression reported in v2026.4.17. PR #959 directly addresses this by persisting the bearer token obtained during pairing, which should restore scheduler tool access. Priority should be given to merging this fix.

No crash or regression reports were filed today.

### 6. Feature Requests & Roadmap Signals

While no explicit feature requests were recorded today, the continued activity on **PR #783** (cron subagent) strongly signals that scheduled job execution is a priority for the upcoming release. The PR introduces a full cron engine with historical tracking, multiple job types, and operator alerts. If merged, this would become a major capability.

PR #958 (Teams authentication fix) is a bug fix but also reflects a user‑reported integration gap; successful merge will improve the Teams connector’s reliability.

Predictions for next version:
- **Cron subagent** (likely from PR #783)
- **Scheduler token fix** (from PR #959)
- **Teams auth improvements** (from PR #958)

### 7. User Feedback Summary

Real pain points from the last 24 hours:

- **Inconsistent local model output** – The Ollama/Gemma user reports that the agent does not provide complete sentences, limiting practical use without a cloud model. This user likely expected parity with remote models. No satisfaction comments have been recorded.
- **Scheduler inaccessible after pairing** – The reporter `ats-bcon` encountered a workflow‑blocking bug: after pairing a `bit`, the scheduler tool is denied access. The workaround is unclear, and frustration is implied by the detailed screenshots.

Overall, users are actively testing the latest release and encountering integration hurdles. Positive feedback is absent from today’s data.

### 8. Backlog Watch

Two items warrant maintainer attention:

- **Issue #839** (created April 18) – Despite having a fix PR (#959), the issue itself has been open for two months without a maintainer response. A status update or prioritization note would help the reporter.
- **PR #783** (created April 7) – The cron subagent feature is large and has not been merged after 2+ months of updates. While it is clearly being worked on, the community would benefit from an estimated timeline or request for reviewers.
- **Issue #952** (June 11) – Still unanswered. An initial triage comment (e.g., "we've reproduced this" or "can you provide logs") would improve community trust.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-06-17

## 1. Today's Overview

IronClaw saw **heavy activity** over the past 24 hours: 50 issues and 50 pull requests were updated, with 31 open issues and 35 open PRs still in flight. 19 issues were closed and 15 PRs were merged or closed. No new releases were cut. The majority of work focused on **Engine V2 quality** (milestone 0 completed), **Reborn WebUI bug fixes** (approval dialog, automation UX, auth recovery), and **platform stability** (SSO mismatch, Google Drive auth hardening). The project is in a **fast-paced iteration cycle** with core contributors and regular contributors both shipping fixes.

## 2. Releases

**No new releases** were published on 2026-06-17. The latest tagged release (if any) remains unchanged.

## 3. Project Progress (Merged/Closed Today)

The following high-impact PRs and issues were closed or merged in the last 24 hours, indicating concrete progress:

- **#4902** – Vision support for inline images on `/v1/chat/completions` (closed; feature shipped)  
- **#4858** – Sanitized shell command details now show in approval prompts and activity history (merged; fixes #4852)  
- **#4995** – Benchmarks now forward `NEARAI_API_KEY` for Reborn runs using NEAR cloud (merged; CI improvement)  
- **#4954** – Approval-gate denial now surfaces to the model instead of cancelling the run (merged; fixes a key loop bug)  
- **#4723** – New conversation composer hover state highlighting fixed (closed)  
- **#4857** – Clean state no longer incorrectly marks NEAR AI provider as active (closed)  
- **#2721 / #2725 / #2724 / #2723** – Engine V2 quality Milestone 0: multi-route execution, prompt tightening, orchestrator loop improvements all closed as completed.

**Engine V2 Milestone 0** is now fully resolved, marking a significant architectural step forward for reducing cost and improving finalization behavior.

## 4. Community Hot Topics

The most discussed items (by comment count) in the last 24 hours:

- **#2721** (3 comments, closed) – Engine V2 quality: Milestone 0 + multi-route execution. This epic drove the biggest recent change; its closure signals a go/no-go decision toward the larger architecture track.  
  [nearai/ironclaw Issue #2721](https://github.com/nearai/ironclaw/issues/2721)

- **#4942** (2 comments, open) – Reborn WebUI: tool calls failed won’t appear until re-fetch/reload. Users are experiencing stale SSE delivery for Google Suite operations, causing confusion.  
  [nearai/ironclaw Issue #4942](https://github.com/nearai/ironclaw/issues/4942)

- **#4853** (1 comment, open) – Tool activity disappears after completion on Railway / multi-tenant environments. The approval dialog and activity history incorrectly clear tool entries mid-run.  
  [nearai/ironclaw Issue #4853](https://github.com/nearai/ironclaw/issues/4853)

- **#4986** (1 comment, open) – Recurring automation can become permanently blocked waiting for tool approval. This is a blocking issue for production-grade automations.  
  [nearai/ironclaw Issue #4986](https://github.com/nearai/ironclaw/issues/4986)

- **#4881** (1 comment, open) – Feature request: Preview Deployments for IronClaw PRs. The community is asking for Vercel-like preview links to ease review.  
  [nearai/ironclaw Issue #4881](https://github.com/nearai/ironclaw/issues/4881)

- **#5003** (0 comments, open) – Fix for #4992: recover stranded local-dev SSO automations. This PR addresses a critical Railway automation failure and is actively being reviewed.  
  [nearai/ironclaw PR #5003](https://github.com/nearai/ironclaw/pull/5003)

Underlying needs: stabilization of the Reborn WebUI (especially SSE, approval flow), improved automation management, and better feedback when tools or auth fail.

## 5. Bugs & Stability

Bugs reported today, ranked by severity (most impactful first):

1. **Critical – #4992** (open, fix PR #5003): Railway-hosted SSO automations fail before run/thread creation due to mismatched `creator_user_id`. Runs stuck in `ERROR` with `No thread attached`.  
   [Issue #4992](https://github.com/nearai/ironclaw/issues/4992) | [Fix PR #5003](https://github.com/nearai/ironclaw/pull/5003)

2. **Critical – #4986** (open, no fix yet): Recurring automations can become permanently blocked waiting for tool approval, never progressing.  
   [Issue #4986](https://github.com/nearai/ironclaw/issues/4986)

3. **High – #4991** (open, no fix yet): WASM Google Drive auth failures dead-end with `operation_failed` – no refresh-retry or `AuthRequired` gate.  
   [Issue #4991](https://github.com/nearai/ironclaw/issues/4991)

4. **Medium – #4942** (open): Tool call failures not visible in WebUI until manual refresh. Affects Google Suite and SSE delivery.  
   [Issue #4942](https://github.com/nearai/ironclaw/issues/4942)

5. **Medium – #4853** (open): Tool activity disappears after completion on Railway. Approval history inconsistent.  
   [Issue #4853](https://github.com/nearai/ironclaw/issues/4853)

6. **Medium – #4852** (closed, fixed by #4858): Shell command invisible in approval dialog and activity history.  
   [Issue #4852](https://github.com/nearai/ironclaw/issues/4852)

7. **Low – #5007** (open): Skills validation error does not clear after required fields are filled.  
   [Issue #5007](https://github.com/nearai/ironclaw/issues/5007)

8. **Low – #4977** (open, parent #4879): Approval-deny tool activity not staying visible or ordered after denial.  
   [Issue #4977](https://github.com/nearai/ironclaw/issues/4977)

Additional bug issues opened today: #5004 (failure summary not actionable), #4988 (recent runs visualization confusing), #4972 (font size inconsistency). Most bug reports come from daily dogfooding by core team members.

## 6. Feature Requests & Roadmap Signals

- **#4881** – Preview Deployments for PRs (likely to be implemented soon to improve review workflow).  
- **#4985** – Persist LLM usage for Engine V2 so `/api/admin/usage` returns data (needed for production monitoring).  
- **#4983** – Remove NEAR AI tool-message flattening compatibility path (cleanup toward full OpenAI compliance).  
- **#4999** – Scale Google Drive `download_file` extraction beyond the 1 MB WASM round-trip cap (important for real document processing).  
- **#5006** – Skills page improvements: search/filter, metadata formatting, bulk actions (UX feedback from QA).  
- **#4918** – Automations findings: log page empty, missing retry details, need better failure narratives.  
- **#4692 / #4879** – Dogfooding findings collections continue to produce a steady stream of UX and stability improvements.

Predictions for next minor release: fix for #4992 (SSO automation), #4986 (blocked automations), #4942 (stale tool failures), #4999 (larger Drive extraction), and several Automation/Skills UX enhancements.

## 7. User Feedback Summary

Real pain points captured from issue descriptions and comments:

- **Automation management is confusing:** Empty states don’t guide creation (#4980), status badges are misleading (#4981), row selection is unreliable (#4982), failure summaries are not actionable (#5004), and run threads for approval-gated automations are hard to find (#4987).
- **Tool/approval visibility is broken:** Shell commands missing from approval dialog (#4852, fixed), tool activity disappears after completion (#4853, open), denied approvals remain displayed as running (#4977), and tool call failures require refresh (#4942).
- **Onboarding friction:** Clean state incorrectly shows NEAR AI as active provider (#4857, fixed), New button font inconsistency (#4972), Skills page lacks search/filter (#5006), and validation errors persist incorrectly (#5007).
- **Authentication / reliability:** Google Drive auth failures dead-end without retry (#4991), Railway SSO mismatches break automations (#4992), and approval-gate denial previously cancelled the run instead of informing the model (#4954, fixed).

Overall satisfaction: The community (largely core contributors) is actively dogfooding and reporting issues, indicating engagement. Fixes are being shipped fast (e.g., #4858, #4954, #5003), which builds trust.

## 8. Backlog Watch

Important items that have remained open for an extended period without maintainer comment:

- **#3890** (open since 2026-05-22) – Reborn multi-tenant isolation contract tests. This PR is open and untouched for nearly a month; it’s critical for production readiness but appears blocked or low priority.  
  [PR #3890](https://github.com/nearai/ironclaw/pull/3890)

- **#4518** (open since 2026-06-06) – Add Reborn extension lifecycle e2e coverage. Another PR awaiting review.  
  [PR #4518](https://github.com/nearai/ironclaw/pull/4518)

- **#4712** (open since 2026-06-10) – Move Slack setup into WebUI. Large PR, still open with no merged status.  
  [PR #4712](https://github.com/nearai/ironclaw/pull/4712)

- **#4692** (open since 2026-06-10) – Dogfooding findings from week June 8-14. Contains many small bugs that may be lost if not triaged.  
  [Issue #4692](https://github.com/nearai/ironclaw/issues/4692)

- **#4879** (open since 2026-06-15) – Current week dogfooding findings. Similar to above; needs systematic triage.

No critical security issues appear to be languishing. The project maintainers are responsive, but the sheer volume of open PRs (35) suggests a review bottleneck.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**LobsterAI Project Digest for 2026-06-17**

**1. Today's Overview**
The project is exhibiting a moderate level of activity with four Pull Requests updated in the last 24 hours, three of which were successfully merged or closed. This points to a healthy, ongoing development cycle focused on feature delivery and refactoring. However, only one Issue was updated, and no new releases were published, suggesting the team is consolidating recent merges. A notable concern is the presence of two "stale" items—one issue and one PR—that have been open for over two months, which could indicate growing maintenance debt.

**2. Releases**
No new releases were published in the last 24 hours. This section is omitted.

**3. Project Progress**
The team merged three Pull Requests today, reflecting progress across the Cowork and Artifacts areas:
- **[PR #2170 (MERGED)](https://github.com/netease-youdao/LobsterAI/pull/2170)**: Fixed the Cowork task search to query the backing SQLite database rather than filtering only preloaded sessions. This improves search accuracy and reliability without altering existing UI behavior like the sidebar or pagination.
- **[PR #2169 (MERGED)](https://github.com/netease-youdao/LobsterAI/pull/2169)**: Enhanced the Artifacts preview experience by unifying card styles, adding dark-mode hover effects, and optimizing the HTML open-in-browser menu. This improves visual consistency and user control.
- **[PR #2168 (MERGED)](https://github.com/netease-youdao/LobsterAI/pull/2168)**: Introduced a compact scroll-to-bottom button for Cowork conversations, supporting smooth scrolling, internationalization labels, and click diagnostics.

**4. Community Hot Topics**
Activity is low, making the "stale" items the most significant community signals this week:
- **[Issue #1425](https://github.com/netease-youdao/LobsterAI/issues/1425)** (1 comment): Reports a missing validation check for duplicate keyboard shortcuts. The user notes that pressing "Save" with a duplicate shortcut does not produce an error, despite an expected validation prompt. This reflects a usability need for better input guardrails.
- **[PR #1424](https://github.com/netease-youdao/LobsterAI/pull/1424)** (0 comments): Remains open and serves as a deep analysis of a silent failure in the scheduled tasks system. The underlying need is for meaningful error feedback in the UI, rather than silent successes.

**5. Bugs & Stability**
One significant stability concern has resurfaced:
- **Critical - Silent Error for Scheduled Tasks**: PR #1424 documents a critical bug where the "Stop" IPC handler for timed tasks returns `{ success: true }` without actually performing the operation. All task management failures are written to Redux state but no UI component reads that state, leaving users completely unaware of errors. This undermines user trust in critical automation features. No fix PR has been merged yet.
- **Low - Missing Duplicate Shortcut Validation**: Issue #1425 reports a missing validation for duplicate keyboard shortcuts, which can lead to confusing usability. This is a minor polish issue, not a functional regression.

**6. Feature Requests & Roadmap Signals**
- **Cowork Database-Backed Search**: The merge of PR #2170 signals that the team is prioritizing a more robust, persistent search experience for Cowork tasks, moving beyond transient in-memory filtering.
- **Deduplication & Validation**: Issue #1425 indicates user demand for stronger input validation. Given its lightweight nature, a small fix for shortcut duplicate detection is a likely candidate for the next minor release.
- **Artifacts Preview Optimization**: PR #2169 shows active investment in the Artifacts subsystem, suggesting further UI/UX enhancements may follow, such as richer file previews or deeper browser integration.

**7. User Feedback Summary**
User feedback from the dataset reveals two primary pain points:
- **Lack of Error Feedback**: The core frustration is silent system behavior. Users expect validation and error messages (e.g., duplicate shortcuts, failing scheduled tasks) but receive none, leading to confusion and a feeling of lost control.
- **Scheduled Tasks Reliability**: The scheduled tasks system appears to be a source of user dissatisfaction, as its failure handling is invisible to the user. This could erode confidence if not addressed in the next cycle.

**8. Backlog Watch**
Two items require maintainer attention due to age and lack of resolution:
- **[PR #1424](https://github.com/netease-youdao/LobsterAI/pull/1424)** (stale, 2+ months): This PR is a comprehensive fix for the silent error problem in scheduled tasks. It is a high-value, maintainer-ready improvement that should be reviewed and merged to address a critical stability gap.
- **[Issue #1425](https://github.com/netease-youdao/LobsterAI/issues/1425)** (stale, 2+ months): A simple but impactful UX improvement request for shortcut duplicate validation. Despite being straightforward, it has not received a PR or official response. It should be prioritized for a quick win.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-06-17

## 1. Today's Overview

TinyClaw saw minimal activity over the past 24 hours. No new releases were published, and no issues were created or updated. A single pull request (#281) addressing Windows compatibility remains open. Overall project activity is low, with the community’s attention focused on a targeted cross‑platform fix rather than new features or bug reports. The project appears stable but may benefit from increased engagement to sustain momentum.

## 2. Releases

None. No new versions were published in the last 24 hours.

## 3. Project Progress

**Merged/Closed PRs:**  
No PRs were merged or closed today.

**Open PRs (active):**  
- **[#281] fix: Windows cross-platform support in CLI** – *Open, updated 2026-06-16*  
  Author: [mperkins0155](https://github.com/mperkins0155)  
  This PR targets three Windows‑specific bugs that prevented the `tinyagi` CLI from running natively on Windows (outside WSL). The changes resolve:  
  - A doubled drive letter causing `MODULE_NOT_FOUND` errors due to how `import.meta.url.pathname` is handled on Windows.  
  - Two additional issues (not detailed in the summary but referenced as “three Windows‑only bugs”).  
  No reactions, reviews, or comments have been received yet.  
  [PR #281](https://github.com/TinyAGI/tinyagi/pull/281)

## 4. Community Hot Topics

The only active item is the open PR #281 described above. While it has zero comments or reactions, its presence signals that Windows support is a pain point for at least one contributor. No other issues or PRs have attracted discussion in the last 24 hours.

## 5. Bugs & Stability

**New bugs reported today:** None.  
**Bugs addressed via open PR:**  
- **Bug #1 (Severity: Medium)** – Double drive letter in path resolution causing `MODULE_NOT_FOUND` on Windows.  
- **Bugs #2 & #3 (Severity: Medium)** – Two additional Windows‑only issues (details not specified).  

All three are addressed by PR #281, which is awaiting review and merge. No regressions were reported.

## 6. Feature Requests & Roadmap Signals

No new feature requests were posted today. The single PR is a bugfix, not a feature. If the Windows fixes are merged, future versions may see improved cross‑platform compatibility as a foundation for broader Windows adoption. No roadmap signals (RFCs, milestones, or maintainer comments) were observed.

## 7. User Feedback Summary

No explicit user feedback (comments, satisfaction/dissatisfaction) was recorded in the last 24 hours. The existence of PR #281, however, implies that at least one user (the author) encountered real Windows‑execution issues that prevented CLI usage on native Windows. This points to an unspoken dissatisfaction among Windows users, though the lack of comments suggests the affected user base is small or silent.

## 8. Backlog Watch

There are no long‑unanswered issues or PRs requiring maintainer attention. The only open PR (#281) was created yesterday and is still fresh. No dormant issues are present in the current dataset.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — June 17, 2026

## 1. Today’s Overview
The Moltis project saw light but focused activity over the past 24 hours. Four issues were updated—three remain open (two bug reports, one feature request) and one bug was closed. Two pull requests remain open, both adding configuration and agent‑model flexibility. No new releases were published. Overall, the project is in a steady maintenance and enhancement cycle, with the community actively reporting real‑world deployment pain points.

## 2. Releases
*No new releases available. The latest release remains the one prior to this digest date. No migration notes or breaking changes to report.*

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. Two open PRs continue to advance:
- **#1124** – Adds an optional `chat.context_command` that runs before each turn, injecting dynamic runtime context into the prompt. This improves deployability without manual session preparation.
- **#1125** – Introduces per‑provider model/effort selection for external agents, surfaced in the `/model` command. This increases modularity for users relying on multiple AI backends.

Both PRs are authored by `gptme-thomas` and were last updated on June 16. Neither has received review comments yet.

## 4. Community Hot Topics
The most active issues by comment count:
- **[#1126 – Allow to configure format of TTS output](https://github.com/moltis-org/moltis/issues/1126)**  
  *2 comments* – A feature request asking for user‑configurable TTS output formats. The discussion likely revolves around supporting different audio codecs or streaming modes (raw PCM vs. Opus, etc.). This reflects a need for greater output flexibility in voice‑enabled agents.
- **[#1128 – Transcription errors with self‑hosted whisper.cpp](https://github.com/moltis-org/moltis/issues/1128) (CLOSED)**  
  *1 comment* – This bug was reported and subsequently closed today. The lack of further detail suggests a quick fix, duplicate, or “works‑as‑designed” resolution; maintainers should confirm the rationale for closure.

No PRs have generated discussion yet.

## 5. Bugs & Stability
Two bugs were reported today:
- **[#1129 – Lack of echo cancellation causes agent to retrigger itself in live mode](https://github.com/moltis-org/moltis/issues/1129)**  
  *Severity: High* – In real‑time audio mode, the agent hears its own output and re‑triggers, breaking conversational flow. No fix PR exists yet. This is a critical usability issue for live deployments.
- **[#1128 – Transcription errors with self‑hosted whisper.cpp](https://github.com/moltis-org/moltis/issues/1128)**  
  *Severity: Medium* – Closed without a linked fix PR. If the issue persists in the wild, users may experience degraded STT quality. The closure should be reviewed to ensure a proper resolution was applied.

**Overall stability** is slightly impacted by the echo cancellation problem, which likely requires architectural changes (e.g., AEC integration or silence detection thresholds).

## 6. Feature Requests & Roadmap Signals
Two feature requests were opened today:
- **#1126 – Configure TTS output format** – Elicits support for custom audio formats, indicating a need for flexible voice output.
- **#1127 – Configure RPC timeout** – Users want to adjust RPC timeouts, likely for slow remote models or unreliable networks.

Both are small, self‑contained configuration changes and could land in the next minor release, especially if attached to a PR. The ongoing PRs (#1124, #1125) suggest the team is prioritising configurable runtime behaviour.

## 7. User Feedback Summary
- **Pain points**:  
  - Self‑hosted whisper.cpp produces transcription errors (now closed).  
  - Echo cancellation is missing, making live voice mode unusable.  
  - Lack of TTS format configurability limits integration with custom pipelines.  
  - RPC timeout is hard‑coded, causing failures with high‑latency backends.
- **Use cases**: Deployment of voice‑enabled AI agents in real‑time settings (live chat, voice assistants). Users are tinkering with external model providers and local STT/TTS, indicating a DIY community.
- **Satisfaction/dissatisfaction**: The quick closure of #1128 may be appreciated or could frustrate users if the underlying bug persists. The echo cancellation bug (#1129) currently has zero responses, suggesting either low awareness or high severity requiring maintainer attention.

## 8. Backlog Watch
No issues or PRs appear to be long unanswered. All 4 items were created on June 16–17 and received updates within 24 hours. The two open PRs (#1124, #1125) are waiting for maintainer review or additional testing. Maintainers should prioritise the echo cancellation bug (#1129) and review the closed bug #1128 to ensure it was properly resolved.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-17

## 1. Today's Overview
CoPaw shows high activity with 44 issues and 38 PRs updated in the last 24 hours, split evenly between open/closed items. A new beta release (v1.1.12-beta.1) shipped, focusing on security keychain isolation and Tauri CI hardening. Community engagement is strong, especially around context compression, chat stability, and channel-specific bugs. Several critical stability fixes are in the pipeline, and first-time contributions continue to grow, with multiple language and feature PRs being merged.

## 2. Releases
**v1.1.12-beta.1** – published 2026-06-17  
- **Changes**  
  - Security: Isolate keychain master key per install to prevent cross-install credential leakage.  
  - Desktop: Harden Tauri Windows CI against crates.io fetch failures.  
  - Refactoring (truncated in log): likely internal restructurings.  
- **Breaking Changes**: None identified.  
- **Migration Notes**: No special steps required; beta release for early testing.

[View release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12-beta.1)

## 3. Project Progress
Seven PRs were merged/closed today (in addition to the release):

| PR | Description | Status |
|---|---|---|
| [#5255](https://github.com/agentscope-ai/QwenPaw/pull/5255) | chore: bump version to 1.1.12b2 | Merged |
| [#5248](https://github.com/agentscope-ai/QwenPaw/pull/5248) | feat(console): OSC 8 clickable links in ConsoleChannel | Merged |
| [#5247](https://github.com/agentscope-ai/QwenPaw/pull/5247) | feat(coding): Ponytail philosophy + zero-dep code indexer | Merged |
| [#5240](https://github.com/agentscope-ai/QwenPaw/pull/5240) | perf(config): remove unnecessary deep copy operations in agent config caching | Merged |
| [#5201](https://github.com/agentscope-ai/QwenPaw/pull/5201) | test(integration): Sprint 2.4 cron execution and tool API tests | Merged |
| [#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178) | feat(console): add session filter by title | Merged |
| [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175) | feat(console): add Vietnamese (vi) interface language support | Merged |

These advances improve developer experience (config performance, integration tests), user interface (session filtering, clickable links, i18n), and introduce a formal coding philosophy. Several other PRs remain open (e.g., Headroom compression, cron silent mode, timeout protection for compaction) and are under active review.

## 4. Community Hot Topics
Most active issues by comment count:

- **[#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)** (14 comments) – **Sub-agent context compaction freezes the entire QwenPaw process.** Users report the app becomes completely unresponsive, requiring a manual restart. This is the highest-engagement bug today.

- **[#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)** (6 comments) – **Feature request: Integrate Headroom as optional context compression layer.** Users want 60–95% token reduction via a local-first reversible compressor. A corresponding PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) is open.

- **[#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)** (6 comments) – **MiniMax-M2.5 model returns XML-formatted thinking blocks, breaking command execution.** Long-standing bug (May 22) with no fix yet, causing frequent conversation interruptions.

- **[#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)** (5 comments) – **Feishu CardKit streaming card slow in long replies.** Users report "one character at a time" rendering, making the feature nearly unusable for long outputs.

- **[#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161)** (5 comments) – **Long conversation causes QwenPaw to stop responding entirely.** Similar to #5218 but with a different root cause (context length, not compaction). Multiple users confirming the issue.

The underlying need is clear: context management (compaction, timeout, long conversations) and channel-specific streaming performance are the top community concerns.

## 5. Bugs & Stability
**Critical** (process crash or permanent freeze):

- **[#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209)** – **macOS ARM64 crash loop (SIGSEGV) on desktop app.** Crashes every ~1 minute. Root cause traced to `chromadb_rust_bindings.abi3.so` null pointer dereference. PR [#5246](https://github.com/agentscope-ai/QwenPaw/pull/5246) proposes config overrides; also related to Tauri plugin dependency issue fixed in [#5238](https://github.com/agentscope-ai/QwenPaw/pull/5238).

- **[#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)** – **Sub-agent context compaction freeze.** PR [#5242](https://github.com/agentscope-ai/QwenPaw/pull/5242) adds timeout protection to `agent.reply()` inside compaction, under review.

- **[#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162)** – **Agent thinking logic enters infinite loop.** Reported with reproduction steps missing; still open.

**High** (service disruption but recoverable):

- **[#5250](https://github.com/agentscope-ai/QwenPaw/issues/5250)** – **Cron tasks inject into main chat stream, interrupting user sessions.** PR [#5251](https://github.com/agentscope-ai/QwenPaw/pull/5251) adds `silent` option for agent jobs.

- **[#5235](https://github.com/agentscope-ai/QwenPaw/issues/5235)** – **Cron tasks not executing at scheduled time** (misfire grace period too short). PR [#5241](https://github.com/agentscope-ai/QwenPaw/pull/5241) increases grace from 60s to 3600s.

- **[#5253](https://github.com/agentscope-ai/QwenPaw/issues/5253)** – **Custom channel listener dies after any save operation** (v1.1.10). No fix PR yet.

**Medium** (functional regressions):

- **[#5237](https://github.com/agentscope-ai/QwenPaw/issues/5237)** – **DingTalk channel not working when installed via `uv` on Windows.** Works with installer package. No fix yet.

- **[#5214](https://github.com/agentscope-ai/QwenPaw/issues/5214)** – **DingTalk Stream channel silent after macOS sleep-wake.** TCP half-open connection; SDK reconnection never triggers.

- **[#5208](https://github.com/agentscope-ai/QwenPaw/issues/5208)** – **Assistant message count mismatch with `reasoning` block type.** Incompatibility with OpenAI-compatible providers using non-standard thinking formats.

Several of these have active fix PRs, indicating responsive maintainer effort.

## 6. Feature Requests & Roadmap Signals
Notable user-proposed features that may appear in upcoming releases:

- **Headroom context compression** ([#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)) – PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) implements a HeadroomContextManager. Likely to land in v1.2.x.

- **Agent self-evolution mechanism** ([#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)) – Users want agents to learn from mistakes and auto-correct. No PR yet.

- **WeCom simultaneous image+text push** ([#5217](https://github.com/agentscope-ai/QwenPaw/issues/5217)) – Currently limited to separate messages. Feature request for combined media.

- **Workspace temp file optimization** ([#5225](https://github.com/agentscope-ai/QwenPaw/issues/5225)) – Files stored in workspace root cause management issues. Request to isolate or allow custom paths.

- **Kimi-for-coding support via uv whitelist** ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)) – Users subscribed to Kimi coding tier want direct integration.

- **Vietnamese language & session filter** – Already implemented and merged today (#5175, #5178), showing rapid response to community requests.

- **Governance & sandbox interface** ([#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088)) – A breaking change PR under review, indicating a move toward enterprise-grade security (permission model, sandboxing).

- **User input queue** ([#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158)) – Still open, would allow queuing messages while agent is busy.

- **DataPaw plugin** ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)) – Old PR (May 22) still under review; adds 12 BI skills. Its age suggests possible maintainer backlog.

## 7. User Feedback Summary
**Common pain points:**
- **Stability in long sessions** – Multiple users report the app freezing or becoming unresponsive after extended conversations, regardless of model provider.
- **Channel reliability** – DingTalk Stream silently fails after sleep; custom channel saves break listeners; WeCom lacks combined media.
- **Windows path issues** – Duplicated session IDs in filenames cause MAX_PATH overflow (fixed in #4988 but users still experiencing related problems).
- **Desktop UI footprint** – Top bar takes excessive space; sidebar complexity hides frequently used chat sessions.
- **Cron scheduling flaws** – Tasks either don't run (misfire grace) or interrupt active user chat.

**Positive signals:**
- Users appreciate the Feishu CardKit integration but request streaming optimization.
- Vietnamese language support was quickly acted upon (issue → merged PR within 4 days).
- The community is submitting high-quality first-time contributions (e.g., Headroom, OCS8 links, session filter, config performance).

## 8. Backlog Watch
Issues/PRs that require maintainer attention:

- **[#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625)** – MiniMax XML formatting bug (open since May 22, 6 comments, no fix PR). High impact for MiniMax users.

- **[#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622)** – DataPaw plugin PR (open since May 22, under review). Large feature with 12 skills; may need closer review.

- **[#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088)** – Governance & sandbox PR (open since June 10, breaking change). No recent activity; key for enterprise adoption.

- **[#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)** – Agent self-evolution feature request (no PR). Growing community interest; could be roadmap priority.

- **[#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162)** – Infinite thinking loop bug (open since June 12, no reproduction steps provided). Needs maintainer to request more info.

- **[#5217](https://github.com/agentscope-ai/QwenPaw/issues/5217)** – WeCom combined image+text (open since June 16, 3 comments). Simple request that could improve channel parity.

Overall project health is strong, with responsive maintainers and a growing contributor community. The main risk areas are context management stability and channel-specific edge cases, both being actively addressed.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-17

## Today’s Overview

The ZeptoClaw project experienced minimal activity in the past 24 hours. No new issues were opened or updated, and no pull requests were merged or closed. The only movement was a single open dependency update pull request (#630) submitted by Dependabot, which remains unmerged. No new releases were published. Overall, project health appears stable but quiet, with no indications of urgent community discussions or emerging technical problems.

## Releases

No new releases were created today. The last release remains unknown from the available data; project contributors and users should refer to the [GitHub Releases page](https://github.com/qhkm/zeptoclaw/releases) for historical versions.

## Project Progress

No pull requests were merged or closed in the last 24 hours. The only existing open PR is highlighted in the Community Hot Topics section below.

## Community Hot Topics

Only one pull request was updated in the period:

- **#630** [OPEN] [dependencies, docker] chore(deps): bump debian from `b6e2a15` to `4e401d9`  
  Author: dependabot[bot] | Created: 2026-06-16 | Comments: 0 | 👍: 0  
  [View PR](https://github.com/qhkm/zeptoclaw/pull/630)  
  This routine Dependabot update bumps the `debian` base image in the Dockerfile from a previous digest to a newer one, both still tagged as `trixie-slim`. There are no comments or reactions, indicating low community engagement. The change is purely maintenance and does not fix any reported bug or introduce new features.

No other issues or pull requests attracted discussion today.

## Bugs & Stability

No bugs, crashes, or regressions were reported in the last 24 hours. The project’s bug tracker shows no open or updated bug reports during this period.

## Feature Requests & Roadmap Signals

No feature requests were submitted or discussed today. The project has no publicly visible roadmap signals from this data snapshot.

## User Feedback Summary

No user feedback, pain points, or satisfaction/dissatisfaction comments were recorded in the last 24 hours. The lack of activity may reflect stable usage or low contributor bandwidth.

## Backlog Watch

There are no long-unanswered issues or pull requests requiring maintainer attention based on today’s data. The only open PR (#630) is a low-priority automated dependency bump and does not necessitate immediate review. Maintainers are encouraged to periodically review older open issues for any that may have been overlooked.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-17

## Today’s Overview

The project saw very high activity over the last 24 hours, with **50 issues** and **50 PRs** updated. **13 issues** were closed and **10 PRs** were merged or closed, reflecting continued momentum on the v0.8.x track. No new releases were published today. The bulk of attention is on stability—several S1 (workflow-blocked) bugs surfaced, particularly around provider tool availability, Anthropic message formatting, and prebuilt binary regressions. Community discussion also remains active on the Work Lanes governance RFC ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) and on documentation quality, with one user bluntly stating the docs are “crap” ([#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758)).

## Releases

*No new releases today.* The latest available version remains **v0.8.0**.

## Project Progress

**Closed/merged items from the last 24 hours** (selected from updated issues – PR merge details are not individually listed in the provided data):

| Item | Description |
|------|-------------|
| [#6856](https://github.com/zeroclaw-labs/zeroclaw/issues/6856) (bug, closed) | `show_tool_calls` missing from channel responses in schema v3 – fixed. |
| [#6312](https://github.com/zeroclaw-labs/zeroclaw/issues/6312) (enhancement, closed) | Per-alias webhook path routing for multi-instance channels – landed as `/webhook?agent=` dispatch. |
| [#6150](https://github.com/zeroclaw-labs/zeroclaw/issues/6150) (enhancement, closed) | Added `/clear` command for Telegram/Discord to quickly clear memory. |
| [#6807](https://github.com/zeroclaw-labs/zeroclaw/issues/6807) (enhancement, closed) | Telegram custom web API endpoint support added. |
| [#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143) (bug, closed) | Fixed agent repeatedly running near-duplicate shell discovery commands until `max_tool_iterations` exhausted. |
| [#6859](https://github.com/zeroclaw-labs/zeroclaw/issues/6859) (enhancement, closed) | Added behavioral test coverage for Windows shell code-page decoding. |
| [#6648](https://github.com/zeroclaw-labs/zeroclaw/issues/6648) (bug, closed) | `cron_add` `session_target=main` now correctly reuses the primary session. |
| [#6995](https://github.com/zeroclaw-labs/zeroclaw/issues/6995) (bug, closed) | Backspace in `zeroclaw agent` CLI now deletes character-by-character for CJK UTF-8. |

Additionally, **10 PRs** were merged/closed during this period (details not available in the top-20 PR list).

## Community Hot Topics

| Issue / PR | Comments | Summary |
|------------|----------|---------|
| [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) (open) | 11 | **RFC: Work Lanes, Board Automation, and Label Cleanup** – Governance proposal to simplify issue routing without manual maintainer overhead. Status: accepted, rollout in progress. |
| [#6856](https://github.com/zeroclaw-labs/zeroclaw/issues/6856) (closed) | 5 | **Bug: `show_tool_calls` missing from channel** – Highlighted a configuration regression that broke tool call visibility in schema v3. Now fixed. |
| [#6312](https://github.com/zeroclaw-labs/zeroclaw/issues/6312) (closed) | 4 | **Feat: per-alias webhook path routing** – Enables multiple bots on one gateway via `?agent=` parameter. Community interest in multi-instance deployments. |

The underlying need across these discussions is **operational clarity** – contributors want better tooling to route work, debug configuration mismatches, and manage multi-agent setups without friction.

## Bugs & Stability

**High-severity bugs reported or updated today (06-17):**

| Issue | Severity | Description | Fix PRs? |
|-------|----------|-------------|----------|
| [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) | **S1** – workflow blocked | Native/MCP tools unavailable on OpenAI Responses/reasoning and Anthropic turns. MCP server connects but model does not receive tools. | [PR #7747](https://github.com/zeroclaw-labs/zeroclaw/pull/7747) wires `mcp_bundles` into agent loop (may partially address). |
| [#7787](https://github.com/zeroclaw-labs/zeroclaw/issues/7787) | **S1** – workflow blocked | Prebuilt v0.8.0 binaries ship without Slack/Discord channel features (regression from 0.7.x). | No fix PR yet. |
| [#7804](https://github.com/zeroclaw-labs/zeroclaw/issues/7804) | **S1** – workflow blocked | Code history can send non-alternating Anthropic messages, causing provider 400 errors on long/resumed sessions. | No fix PR yet. |
| [#7809](https://github.com/zeroclaw-labs/zeroclaw/issues/7809) | S2 (priority P1) | Channel turns ignore runtime-profile `strict_tool_parsing` and `parallel_tools` flags. | No fix PR yet. |
| [#7820](https://github.com/zeroclaw-labs/zeroclaw/issues/7820) | S2 | Zeroclaw repeats identical shell approval loops before bounding – local provider loops on `pwd` tool call. | No fix PR yet. |
| [#7799](https://github.com/zeroclaw-labs/zeroclaw/issues/7799) | S2 | Resumed Code sessions reopen with blank transcript even when messages are persisted. | No fix PR yet. |
| [#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) | S2 | ZeroCode help/keybindings misleading or unreachable, especially on macOS. | No fix PR yet. |
| [#7810](https://github.com/zeroclaw-labs/zeroclaw/issues/7810) | S2 | `git_operations` tool gives no recovery hint when run outside a repository. | No fix PR yet. |
| [#7815](https://github.com/zeroclaw-labs/zeroclaw/issues/7815) | S2 | ZeroCode Config pane does not show which config source/state is being edited. | No fix PR yet. |
| [#7795](https://github.com/zeroclaw-labs/zeroclaw/issues/7795) | risk high, no severity | `static_voice_peers` caches config-derived voice peers on the Telegram channel handle (latent SSOT violation). | No fix PR yet. |

**Notable closed bugs:**  
- [#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758) (S1) “Documentation is crap” – user reported inability to write a config file. Closed same day, but no explicit fix mentioned.

## Feature Requests & Roadmap Signals

| Issue | Summary | Likely target |
|-------|---------|---------------|
| [#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759) | Decouple gateway WebSocket lifetime from agent turn – run turns in background, resume on reconnect. | **v0.8.x** (P1, in-progress) |
| [#7794](https://github.com/zeroclaw-labs/zeroclaw/issues/7794) | Per-agent opt-in Dream Mode + parity surfaces (chat command, gateway Dreams view). | **v0.8.x** (P2, in-progress) |
| [#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822) | Should WASM plugins support lifecycle hook subscriptions (`PluginCapability::Hook`)? | Future milestone (no priority yet) |
| [#7675](https://github.com/zeroclaw-labs/zeroclaw/issues/7675) | RFC: Hardened CI pipeline – supply-chain scanning, provenance, SBOM. | Needs maintainer review |
| [#7762](https://github.com/zeroclaw-labs/zeroclaw/issues/7762) | Cron documentation missing; need ability to run cron jobs with a specific (cheap) model. | Likely **v0.8.2/3** |
| [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) | Tracker for v0.8.3: MCP dashboard and web/plugin-management surfaces. | **v0.8.3** |

The roadmap continues to prioritize **gateway resilience** (WebSocket decoupling), **Dream Mode** refinement, and **MCP dashboard** tooling.

## User Feedback Summary

- **Documentation frustration** – User [#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758) wrote: “It doesn't matter how good the code is if the documentation is crap.” The issue was closed but no documentation overhaul is visible yet.
- **Configuration confusion** – Several users report difficulty writing correct configuration files ([#7758](https://github.com/zeroclaw-labs/zeroclaw/issues/7758), [#7815](https://github.com/zeroclaw-labs/zeroclaw/issues/7815)).
- **Tool reliability** – Users report MCP tools not being passed to models ([#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756)), shell tool approval loops ([#7820](https://github.com/zeroclaw-labs/zeroclaw/issues/7820)), and hidden thinking traces from GLM-

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*