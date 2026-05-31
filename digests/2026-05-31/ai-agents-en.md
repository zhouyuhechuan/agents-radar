# OpenClaw Ecosystem Digest 2026-05-31

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-31 06:56 UTC

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

# OpenClaw Project Digest — 2026-05-31

## 1. Today's Overview

OpenClaw saw extremely high activity on May 31, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, 371 issues remain open/active and 129 were closed; on the PR side, 428 are open while 72 were merged or closed. Two new releases landed today: `v2026.5.30-beta.1` and `v2026.5.28`. The project continues to prioritize stability and recovery across agent runtimes, mobile delivery channels, and convergence on SQLite-based state persistence. The volume of regression and crash reports (many ranked P1 or higher) indicates a period of rapid iteration, but the maintainers are responding with targeted fix PRs and hotfix releases.

## 2. Releases

Two releases were published:

### v2026.5.30-beta.1
**Highlights:**  
- Agents and CLI‑backed runtimes now recover more cleanly from interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries (fixes #88129, #88136, #88141, #88162, #88182).  
- Channels and mobile delivery are steadier across Telegram, WhatsApp, iMessage, and Slack.

### v2026.5.28
**Highlights:**  
- Agent and Codex runtime recovery improvements: subagents keep cwd/workspace separation, hook context stays prompt‑local, session locks release on timeout abort, live OpenClaw locks survive cleanup, stale restart continuations are avoided, and Codex app‑server/helper failures no longer cascade.

**Breaking changes / migration notes:** None explicitly called out in the release text. Users of Codex and CLI backends should verify session recovery behavior.

## 3. Project Progress

**Merged/closed PRs today: 72** (out of 500 updated). Among those visible in the top‑30 list:
- [#80983 [CLOSED]](https://github.com/openclaw/openclaw/pull/80983) – Fix Telegram `/model status` showing `auth: missing` for Codex provider rows when OAuth is active.
- [#86176](https://github.com/openclaw/openclaw/pull/86176) – Fix Telegram media message edits (caption‑only handling and inline button updates). *(Open at last check but listed as “fix”, likely merged soon.)*

Key features advancing in open PRs (many waiting on review or author action):
- **SQLite runtime‑state refactor** (#81402, [#88469](https://github.com/openclaw/openclaw/pull/88469)) – Moving plugin state (Telegram) and core runtime state off JSON sidecars into typed SQLite tables.
- **Twilio SMS channel** (#88476) – Adds bundled SMS support with Twilio webhooks, signed validation, pairing/allowlist, and chunked outbound delivery.
- **MCP operator controls** (#88536) – New CLI commands (`doctor`, `status`, `logout`) and a dedicated Control UI settings page for MCP servers.
- **Extract media and ACP core packages** (#88534) – Refactoring media primitives into `@openclaw/media-core` and ACP types into `@openclaw/acp-core` for better modularity.

## 4. Community Hot Topics

The most active discussions (by comment count):

| Issue | Comments | 👍 | Summary |
|-------|----------|----|---------|
| [#87395 [CLOSED]](https://github.com/openclaw/openclaw/issues/87395) | 14 | 8 | Native hook relay becomes unavailable after 2026.5.26 upgrade on macOS, blocking memory/filesystem tools. |
| [#87646 [CLOSED]](https://github.com/openclaw/openclaw/issues/87646) | 12 | 1 | Feishu channel crashes after v2026.5.27 with `TypeError: read property 'run' of undefined`. |
| [#78308 [OPEN]](https://github.com/openclaw/openclaw/issues/78308) | 11 | 1 | Feature request for channel‑mediated approval for MCP tool calls (consent envelope). |
| [#87307 [OPEN]](https://github.com/openclaw/openclaw/issues/87307) | 9 | 1 | Matrix thread replies regressed in 2026.5.22; `/status` and `/model` silent. |
| [#87436 [CLOSED]](https://github.com/openclaw/openclaw/issues/87436) | 8 | 2 | Codex harness recreates legacy session‑route state after `doctor --fix`. |
| [#85888 [OPEN]](https://github.com/openclaw/openclaw/issues/85888) | 7 | 1 | Cron jobs fail with MiniMax 503 during early morning hours; manual triggers succeed. |
| [#86047 [OPEN]](https://github.com/openclaw/openclaw/issues/86047) | 7 | 3 | Codex app‑server approval stalls cause turn interruptions in Nextcloud Talk sessions. |

**Underlying needs:**  
- **Stable session/channel recovery** is the dominant theme – users upgrading between minor versions frequently hit regressions in hook relay, session routing, and channel dispatch.  
- **Feature completeness for MCP** – the consent envelope (#78308) has 11 comments and remains open, suggesting strong desire for better security controls around MCP tool calls.  
- **Channel‑specific regressions** (Feishu, Matrix, Telegram) show that edge‑case handling in multi‑account or group scenarios remains brittle.

## 5. Bugs & Stability

High‑severity bugs reported or updated today:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#88020 [OPEN]](https://github.com/openclaw/openclaw/issues/88020) | P1 | Anthropic "Invalid signature in thinking block" causes hard session failure instead of retry. | Not yet linked. |
| [#88443 [OPEN]](https://github.com/openclaw/openclaw/issues/88443) | P1 | `auth.cooldowns` config change forces full gateway restart, dropping in‑flight CLI runs. | Not yet. |
| [#87307 [OPEN]](https://github.com/openclaw/openclaw/issues/87307) | P1 | Matrix thread replies sent as normal replies; `/status` silent – regression. | Not yet. |
| [#86047 [OPEN]](https://github.com/openclaw/openclaw/issues/86047) | P1 | Codex approval stalls cause interrupted turns and timeouts in Nextcloud Talk. | Not yet. |
| [#78435 [OPEN]](https://github.com/openclaw/openclaw/issues/78435) | stale/P2 | Slack `start‑account` blocks event loop for minutes on Windows. | Not yet. |
| [#79375 [OPEN]](https://github.com/openclaw/openclaw/issues/79375) | P1 | Upgrade leaves stale user‑level systemd unit; dueling services kill each other on Linux. | Not yet. |
| [#87646 [CLOSED]](https://github.com/openclaw/openclaw/issues/87646) | P1 | Feishu dispatch crash after v2026.5.27 – **closed** (fix likely released in today’s beta). | Yes (implied). |
| [#87395 [CLOSED]](https://github.com/openclaw/openclaw/issues/87395) | (unlabeled) | Native hook relay unavailable on macOS – **closed**, fix included in v2026.5.30‑beta.1. | Yes. |

**Recurring pattern:** Session‑state corruption, channel‑specific dispatch failures, and config‑change trigger crashes are the most impactful regression classes.

## 6. Feature Requests & Roadmap Signals

Notable open feature requests:

- **[#78308](https://github.com/openclaw/openclaw/issues/78308)** – Channel‑mediated approval for MCP tool calls (consent envelope). High community engagement (11 comments). Likely candidate for next minor release given security focus.
- **[#79458](https://github.com/openclaw/openclaw/issues/79458)** – i18n fields for slash command descriptions (stale but user‑requested).
- **[#79047](https://github.com/openclaw/openclaw/issues/79047)** – Preserve conversation context across cross‑backend model switches (e.g., switching from Claude CLI to OpenRouter).
- **[#76952](https://github.com/openclaw/openclaw/issues/76952) [CLOSED]** – Docs for Realtime Talk voices and phone bridge options (closed as stale but still a common request).

**Predictions for next version:**  
- MCP consent envelope (#78308) may land soon given it has “needs‑product‑decision” tag and repeated activity.  
- The ongoing SQLite refactor (#81402) is large but once merged will improve state consistency and reduce JSON sidecar issues.  
- Twilio SMS channel (#88476) is likely to be included in the next stable release.

## 7. User Feedback Summary

**Real pain points expressed by users:**

- **Frequent regressions after minor upgrades** – Several users report that upgrading from one .x release to another breaks previously working channels (Feishu, Matrix, Discord, Telegram). The speed of iteration seems to outpace thorough regression testing.
- **Message loss and silent delivery failures** – Issues like #87326 (Telegram intermediate text blocks lost) and #77666 (Feishu group replies=0) indicate that message delivery reliability is a top concern.
- **Intermittent crashes under load** – Multi‑tenant setups on Windows (#78435) and Linux (#79375) experience gateway hangs or systemd conflicts.
- **Cold‑start performance** – Auth resolution taking 4 seconds on cold dispatch (#78041) frustrates users expecting near‑instant responses.

**Satisfaction signals:**  
- The rapid release cadence (two betas in two days) shows responsiveness, and many bugs are closed quickly (e.g., #87395 fixed within 4 days).  
- Users appreciate new features like Twilio SMS and better MCP controls, even if they are in PR stage.

## 8. Backlog Watch

Long‑unanswered or maintainer‑attention‑needed items:

| Item | Age | Issue | Status |
|------|-----|-------|--------|
| [#78308](https://github.com/openclaw/openclaw/issues/78308) | 25 days | Feature: MCP consent envelope | Stale, needs product decision, linked PR open. |
| [#78435](https://github.com/openclaw/openclaw/issues/78435) | 25 days | Slack start‑account blocks event loop (Windows) | Stale, P2. |
| [#77802](https://github.com/openclaw/openclaw/issues/77802) | 26 days | `doctor --fix` fails atomically on multiple validation errors | Stale, no PR. |
| [#76104](https://github.com/openclaw/openclaw/issues/76104) | 29 days | Feishu sessions_send routes to webchat instead of origin channel | Closed with fix, but root cause may still affect others. |
| [#85538](https://github.com/openclaw/openclaw/issues/65538) (accessibility) | 49 days | Screen readers announce every token during streaming | Open, P1, needs live repro. |

**Notable:** The **SQLite runtime‑state refactor** (#81402) has been open since May 13 and remains a huge PR (XL size, 173 changed files). It is critical for future stability but risky – maintainers have been reviewing it carefully.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent Open-Source Ecosystem
**Date: 2026-05-31**

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is experiencing intense, concurrent development across multiple independent projects, with a collective focus on production reliability, multi-channel delivery, and security hardening. The landscape is bifurcating between reference implementations (OpenClaw) and opinionated forks/hybrids (NanoBot, Hermes Agent, ZeroClaw) that target specific niches—from lightweight mobile agents to enterprise-grade multi-tenant deployments. A recurring pattern across virtually all projects is the tension between rapid feature iteration and regression management, with several projects shipping fixes within hours of bug reports. The ecosystem is converging on SQLite for state persistence, MCP (Model Context Protocol) as the dominant tool integration standard, and modular architecture patterns that separate runtime, channels, and provider layers.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Health Score | Notes |
|---------|----------------------|-------------------|--------------|--------------|-------|
| **OpenClaw** | 500 (129 closed) | 500 (72 merged) | ✅ v2026.5.30-beta.1, v2026.5.28 | 9/10 | Extremely high velocity; regression surge managed with hotfix releases |
| **NanoBot** | 7 (4 closed) | 20 (6 merged) | ❌ | 8/10 | Steady, healthy pace; security hardening focus |
| **Hermes Agent** | 50 (11 closed) | 50 (4 merged) | ❌ | 7/10 | High bug volume but responsive maintainer team |
| **PicoClaw** | 8 (4 closed) | 12 (3 merged) | ✅ Nightly build | 6/10 | Moderate; regressions after v0.2.9 upgrade |
| **NanoClaw** | 5 (0 closed) | 15 (3 merged) | ❌ | 8/10 | Strong velocity; critical fd-exhaustion bug open |
| **IronClaw** | 4 (0 closed) | 16 (9 merged) | ❌ (blocked) | 7/10 | High merge rate; crates.io blockage is key risk |
| **ZeroClaw** | 50 (19 closed) | 50 (15 merged) | ❌ | 7/10 | High volume; review pipeline bottlenecks |
| **CoPaw** | 7 (0 closed) | 2 (1 merged) | ❌ | 5/10 | Bug-dominated; Windows UX issues unaddressed |
| **Moltis** | 0 | 1 (0 merged) | ❌ | 4/10 | Low activity; lone PR for Codex provider fix |
| **LobsterAI** | 0 | 1 (0 merged) | ❌ | 3/10 | Near-dormant; 58-day-old stale PR |
| **ZeptoClaw** | 1 (1 closed) | 0 | ❌ | 3/10 | Minimal activity; security chore only |
| **TinyClaw** | 0 | 0 | ❌ | 2/10 | No activity |
| **NullClaw** | 0 | 0 | ❌ | 2/10 | No activity |

**Health Score Methodology:** Based on velocity, responsiveness to bugs, merge rate, stability signals, and community engagement. 10 = excellent.

---

## 3. OpenClaw's Position

OpenClaw serves as the **canonical reference implementation** in this ecosystem, with advantages that stem from its scale and maintainer responsiveness:

**Advantages vs. Peers:**
- **Velocity & Scale:** 500 issues and 500 PRs updated in 24 hours—an order of magnitude larger than any peer. This reflects both a larger user base and a more active contribution pipeline.
- **Release Cadence:** Two releases in two days (beta and stable patch) demonstrate a CI/CD maturity that peers (e.g., ZeroClaw, Hermes Agent) have not yet achieved. No other project matched this cadence.
- **Regression Response:** Hotfixes for P1 bugs (Feishu crash, macOS hook relay) are ship within 4 days. This contrasts with CoPaw (Windows shell flash open for 23 days) and ZeroClaw (Gemini OAuth broken for 63 days).
- **Modularity Investment:** The SQLite runtime-state refactor (#81402, 173 files) and package extraction (`@openclaw/media-core`, `@openclaw/acp-core`) signal architectural scaling for multi-module consumption. Only IronClaw's Rust crate decomposition mirrors this depth.

**Technical Approach Differences:**
- OpenClaw's **dual runtime** (CLI-backed + Codex) is distinct from NanoClaw's OneCLI or Hermes Agent's TUI-centric model.
- Its **channel-first** architecture (Telegram, WhatsApp, iMessage, Slack, Feishu, Matrix) is broader than any peer. CoPaw covers only Console and Discord; NanoBot emphasizes WebUI and mobile.

**Community Size:**
- OpenClaw's raw issue/PR count (500 each) suggests a contributor base significantly larger than ZeroClaw (50 each) or NanoClaw (15 PRs). Only Hermes Agent approaches with 50 issues/PRs, though with fewer merges.

**Risk:** The high regression rate (7 P1 bugs open at once) signals that velocity is outpacing thorough testing. The SQLite refactor, while critical, introduces further risk if deployed prematurely.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging *independently* across multiple projects, indicating ecosystem-wide priorities:

| Focus Area | Projects Involved | Specific Needs |
|------------|-------------------|----------------|
| **MCP Security & Approval** | OpenClaw (#78308), Hermes Agent (#16462, #21849, #33905), NanoClaw (#2641) | Human-in-the-loop consent envelopes for tool calls, per-tool approval policies, MCP server vetting against supply-chain attacks |
| **Session/Channel Stability** | OpenClaw (#87395, #87646), NanoBot (#4080), Hermes Agent (#35576), PicoClaw (#2972), CoPaw (#4454) | Recovery from interrupted tool calls, stale session bindings, channel-specific dispatch failures, message ordering after upgrades |
| **Multi-Platform Delivery** | OpenClaw (Telegram, WhatsApp, Feishu, Matrix), ZeroClaw (Telegram, WhatsApp, Email), NanoClaw (Discord, Telegram), NanoBot (Feishu, Matrix, WebUI) | Consistent media handling, reply-to-mention in groups, platform-specific syntax (Discord `<URL>`, Matrix SAS verification, WhatsApp LID bots) |
| **Apple Silicon & Container Mounts** | NanoClaw (#2649, #2650), OpenClaw (macOS native hook relay regression), PicoClaw (FreeBSD reports) | Apple container mount races causing phantom inodes; platform-specific binary deployment |
| **Memory & Context Management** | OpenClaw (SQLite refactor), NanoBot (#3885 Dream toggle, #4109 RAG), ZeroClaw (#6850 MemoryStrategy trait), CoPaw (#4833 compaction failure) | Moving from JSON sidecars to typed DB tables, decoupling memory policy from storage, global toggles for automated memory jobs |
| **Provider Compatibility** | ZeroClaw (#5962 Ollama, #7022 Kimi), Hermes Agent (#29327 LiteRT), IronClaw (#4230 reasoning preservation), Moltis (#1088 Codex arguments) | Handling non-OpenAI API shapes (custom kwargs, temperature ranges, tool-call streaming), preserving reasoning chains |
| **Cron & Scheduled Tasks** | OpenClaw (#85888), ZeroClaw (#6954, #6647), PicoClaw (#2977), LobsterAI (#1465) | Cron output routing to channels, inspection/editing without remove-add cycles, ghost session cleanup after deletion |

**Key Insight:** **MCP security** and **channel stability** are the two most urgent cross-project pain points, with every major project reporting at least one related P1 bug or feature request this week.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | NanoClaw | IronClaw | ZeroClaw | CoPaw |
|-----------|----------|---------|--------------|----------|----------|----------|-------|
| **Target User** | Power users, multi-platform | Mobile/WebUI users | CLI power users, TUI | Home lab, multi-tenant | Rust/CLI developers | Hybrid users | Windows console users |
| **Primary Architecture** | Reference runtime + channels | Modular plugin-based | Agent runtime + TUI | OneCLI container-runner | Rust crate ecosystem | Monorepo with orchestrator | Console-focused AgentScope |
| **Channel Breadth** | 7+ (broadest) | 4 (WebUI, Feishu, Matrix, Heartbeat) | 3 (CLI, Telegram, Discord) | 3 (Discord, Telegram, voice) | Slack (Reborn in progress) | 4 (Telegram, WhatsApp, Email) | 2 (Console, Discord) |
| **Language** | TypeScript | TypeScript | TypeScript | TypeScript | Rust | TypeScript/Python | Python |
| **State Persistence** | SQLite migration (in progress) | JSON sidecars (legacy) | SQLite (partial) | SQLite | Filesystem + in-memory | SQLite | JSON files |
| **Security Model** | MCP consent envelope (RFC) | Matrix SAS, SSRF fix, media bounds | Per-tool approval (RFC) | Interactive origin validation | Deny-by-default delegation (RFC) | Risk profiles, RBAC (RFC) | Basic tool allowlists |
| **Key Differentiator** | Reference completeness | WebUI timeline & composer | TUI resume & Kanban | Multi-instance container orchestration | "Reborn" triggers & outbound system | Model-wise reasoning config | Windows shell integration |

**Architectural Divide:** The ecosystem splits between **monolithic runtimes** (OpenClaw, Hermes Agent) and **containerized/microservice approaches** (NanoClaw, IronClaw's crate decomposition). NanoClaw's OneCLI pattern—wrapping the gateway in a Docker container with per-instance proxy—is unique and drives its Apple mount issues.

**User Targeting:** OpenClaw and ZeroClaw compete on breadth (multi-channel, multi-provider), while NanoBot and Hermes Agent optimize for specific interaction models (WebUI vs. TUI). CoPaw is uniquely Windows-focused but underperforms on that platform.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity, Rapid Iteration**
- **OpenClaw** — 500 issues/PRs, 2 releases in 24h. Highest raw activity but also highest regression rate. The project is in a "feature velocity with reactive stability" phase.
- **Hermes Agent** — 50 issues/PRs, responsive maintainers (security bugs closed same day). High bug volume but low regression persistence.
- **NanoClaw** — 15 PRs, 3 merged. Very high per-capita contribution quality. Critical fd-exhaustion bug signals infrastructure scaling pressure.
- **ZeroClaw** — 50 issues/PRs, 15 merged. Strong community RFC culture. Review pipeline bottlenecks (10 PRs awaiting author action) indicate process friction.

**Tier 2: Steady, Stabilizing**
- **NanoBot** — Moderate activity (7 issues, 20 PRs), high merge rate (6/20). Security-first trajectory (SSRF, Matrix SAS, media bounds). Lowest regression count of active projects.
- **IronClaw** — 16 PRs, 9 merged (highest merge rate). Deep architectural work (Reborn triggers, outbound system). Blocked by crates.io publication issue (#3259).

**Tier 3: Low Activity / Maintenance**
- **PicoClaw** — Moderate activity but v0.2.9 regressions suggest incomplete QA. Nightly build is only release channel.
- **CoPaw** — Bug-dominated; no merged fixes for oldest issues (23+ days). Risk of contributor attrition if Windows bugs remain unaddressed.
- **Moltis** — Very low activity; lone PR for Codex provider. May be in maintenance-only mode.
- **LobsterAI** — Near-dormant; 58-day-old PR untouched. Community engagement absent.
- **ZeptoClaw, TinyClaw, NullClaw** — Effectively inactive. Not driving ecosystem conversation or code.

**Maturity Signals:**
- **OpenClaw** and **IronClaw** are the only projects with **formal release engineering** (versioned releases, changelogs, migration notes).
- **NanoBot** and **NanoClaw** show the strongest **community contribution culture**—multiple external PRs with tests and root-cause analysis.
- **ZeroClaw** has the most mature **RFC process** for design decisions (model-wise reasoning, memory strategies, output routing).

---

## 7. Trend Signals

**1. The Regression Tax is Real**
Across OpenClaw, PicoClaw, NanoClaw, and CoPaw, users consistently report that minor version upgrades break previously working channels. This signals a need for **automated regression test suites** covering multi-channel delivery paths. Projects that invest here (NanoBot's security-focused testing is a model) will gain trust.

**2. MCP Security Will Define the Next Release Wave**
Virtually every project has at least one open feature request or RFC for per-tool approval, consent envelopes, or deny-by-default policies. With supply-chain attacks already documented (NanoClaw #2641), expect **MCP security** to be the defining feature of Q3 2026 releases. OpenClaw's consent envelope (#78308) and Hermes Agent's tool approval RFC (#16462) are bellwethers.

**3. SQLite Convergence Accelerates**
OpenClaw's massive SQLite refactor (#81402), combined with NanoClaw and ZeroClaw already on SQLite, signals the death of JSON sidecar files. The ecosystem is converging on a standard persistence layer, which will enable **cross-project data interchange** and **unified migration tools**.

**4. Multi-Platform Is the Default, Not a Differentiator**
Seven+ channel support (OpenClaw) is becoming table stakes. Users expect agents to work across Telegram, Discord, Email, and WebUI simultaneously. The differentiation is shifting to **channel-specific quality** (reply handling, media delivery, group chat awareness) rather than raw channel count.

**5. Platform-Specific Pain Points Drive Forking**
Windows (CoPaw), Apple Silicon (NanoClaw), and FreeBSD (PicoClaw) each have dedicated projects because the reference implementation (OpenClaw) does not prioritize them. This suggests an opportunity for a **cross-platform compatibility layer** or a community-maintain compatibility wiki.

**6. Self-Healing Infrastructure Becomes a Requirement**
NanoClaw's fd-exhaustion crash (#2655) and IronClaw's E2E nightly failure (#4108) highlight that **operational resilience** (auto-restart, health checks, process limits) is moving from "nice-to-have" to "must-have" as agents are deployed in production environments.

**Value for AI Agent

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-31

## 1. Today's Overview
The NanoBot project is in a **high-activity phase** with 20 pull requests updated in the last 24 hours (6 merged/closed, 14 open) and 7 issues updated (3 open, 4 closed). The maintainers have been actively reviewing and merging fixes for several critical bugs, including session dispatch locks, WebUI crashes, and security patches for Matrix channels and SSRF checks. Several long-standing feature requests (e.g., Dream job toggle, Anthropic content block coercion) have been resolved. The project shows a healthy mix of bug fixes, security hardening, and ongoing feature development, with community contributors driving more than half of the PRs.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Six pull requests were merged/closed in the last 24 hours (summary of key changes):

- **[#4054] fix: coerce typeless Anthropic content blocks + add Dream enable toggle**  
  *Closes #3993 and #3885.* Adds `DreamConfig.enabled` (default `true`); when `false`, Dream cron registration is skipped. Also coerces bare dict content blocks to text for Anthropic compatibility.  
  [HKUDS/nanobot PR #4054](https://github.com/HKUDS/nanobot/pull/4054)

- **[#4110] fix(matrix): handle SAS device verification**  
  *Fixes #4042.* Adds opt-in Matrix SAS device verification for Element X clients, resolving "unverified device" warnings on all E2EE messages.  
  [HKUDS/nanobot PR #4110](https://github.com/HKUDS/nanobot/pull/4110)

- **[#4104] fix(agent): acquire per-session lock in process_direct (#4080)**  
  *Fixes #4080.* Prevents concurrent session corruption by reusing the dispatch lock in the `process_direct` path.  
  [HKUDS/nanobot PR #4104](https://github.com/HKUDS/nanobot/pull/4104)

- **[#4108] feat(webui): refine output timeline and model controls**  
  Major WebUI update: reworked activity timeline, stable turn ordering, media/preview improvements, and new composer guidance flow for staging/editing messages.  
  [HKUDS/nanobot PR #4108](https://github.com/HKUDS/nanobot/pull/4108)

- **[#4086] fix(security): normalize IPv6-mapped IPv4 addresses in SSRF checks**  
  *Fixes a security vulnerability.* Prevents SSRF bypass by normalizing IPv6-mapped IPv4 addresses.  
  [HKUDS/nanobot PR #4086](https://github.com/HKUDS/nanobot/pull/4086)

- **[#4106] fix(matrix): bound inbound media downloads**  
  Security hardening: enforces configured media download limits, rejecting events without trusted `content.info.size`.  
  [HKUDS/nanobot PR #4106](https://github.com/HKUDS/nanobot/pull/4106)

## 4. Community Hot Topics
The most active discussions (by comments/reactions) in the last 24 hours:

- **Issue #3885 [Closed] — Dream system job global toggle** (4 comments)  
  Users wanted a configurable switch to disable the Dream cron job entirely. Resolved in PR #4054.  
  [HKUDS/nanobot Issue #3885](https://github.com/HKUDS/nanobot/issues/3885)

- **Issue #4042 [Closed] — Matrix SAS verification for Element X** (1 comment, but high impact)  
  The “unverified device” warning for all messages was a major user-experience blocker for Matrix users. Fixed in PR #4110.  
  [HKUDS/nanobot Issue #4042](https://github.com/HKUDS/nanobot/issues/4042)

- **PR #4115 [Open] — Refactor HTTP handler from WebSocket**  
  Community PR by chengyongru that extracts HTTP routing from WebSocketChannel, paving the way for hot-reload. No comments yet but signals architectural interest.  
  [HKUDS/nanobot PR #4115](https://github.com/HKUDS/nanobot/pull/4115)

- **PR #4111 [Open] — Heartbeat sends false “All clear.”**  
  A bug report with a fix PR (#4114) already in progress; discussion around edge cases of empty HEARTBEAT.md.  
  [HKUDS/nanobot Issue #4111](https://github.com/HKUDS/nanobot/issues/4111)

*Underlying needs:* Users are demanding finer-grained control over automated agent behaviors (cron jobs, memory operations) and better integration stability with third-party platforms (Matrix, Anthropic). The community is actively contributing both bug fixes and architectural improvements.

## 5. Bugs & Stability
New bugs reported today (2026-05-31), ranked by severity:

| Severity | Bug | Status | Fix PR? |
|----------|-----|--------|---------|
| **High** | **WebUI: Code blocks without language specifier cause white screen crash** (#4116) | Open | Yes, PR #4117 (proposed) |
| **Medium** | **Heartbeat cron sends false “All clear.” to Feishu** (#4111) | Open | PR #4114 and #4112 (both open) |
| **Medium** | **process_direct bypasses per-session dispatch locks** (#4080) | Closed | Fixed in PR #4104 |
| **Medium** | **Matrix inbound media not bounded** (security) | Closed | Fixed in PR #4106 |
| **Low** | **SSRF check bypass via IPv6-mapped IPv4** (#4086) | Closed | Fixed in PR #4086 |

*No regressions or crashes beyond #4116 have been reported today.* The white screen crash is currently the most critical open bug; a fix is already proposed. The Heartbeat false-positive issue has two competing fix PRs, indicating community interest.

## 6. Feature Requests & Roadmap Signals
Requests from the last 24h (both new and existing):

- **Additional bind mounts for bwrap sandbox** (#4107, open) — User requests configurable extra paths (e.g., `/nix/store`).  
  *Likelihood for next version:* High, given the active sandbox development and multiple related PRs already merged.
- **Dream system job global toggle** — Already closed in #3885/#4054, but sets precedent for more agent behavior knobs.
- **Heartbeat delivery fail-closed behavior** — Both PR #4114 and #4112 propose fail-closed logic; likely to be merged soon.
- **Lightweight RAG for memory retrieval** (#4109, open) — New PR adds local embeddings for RAG. Signals a move toward on-device semantic memory.

*Predictions for next release:* A toggle for Dream, refined Heartbeat logic, configurable sandbox mounts, and possibly the manual memory mode (#4050) and RAG integration (#4109) if testing completes.

## 7. User Feedback Summary
- **Pain Points:**
  - Heartbeat cron sending irrelevant “All clear.” messages (Feishu users) → confusion and notification fatigue. (Issue #4111)
  - WebUI crashing on code blocks without language → loss of session context. (Issue #4116)
  - Difficulty disabling Dream memory jobs despite disabling memory skill. (Issue #3885)
  - Element X users unable to clear “unverified device” warnings → E2EE trust friction. (Issue #4042)
- **Satisfaction Signals:**
  - Multiple users contributed PRs with detailed root-cause analysis and tests (e.g., #4110, #4114, #4112).
  - Positive reaction to PR #4108 (WebUI timeline rework) – no explicit negative feedback yet.

## 8. Backlog Watch
The following open items have no recent maintainer response or are long-pending:

- **PR #4034 — Add GitAgent Protocol support** (open since 2026-05-28, no maintainer comment)  
  Proposes standard `agent.yaml` + `SOUL.md` files for portability. Given the project’s extensibility focus, this warrants a maintainer review.  
  [HKUDS/nanobot PR #4034](https://github.com/HKUDS/nanobot/pull/4034)

- **Issue #4107 — Configurable bwrap bind mounts** (open since yesterday, no maintainer response yet)  
  Reasonable request that aligns with the sandbox feature.  
  [HKUDS/nanobot Issue #4107](https://github.com/HKUDS/nanobot/issues/4107)

- **Issue #4111 — Heartbeat false “All clear.”** (open, but two PRs already proposed)  
  Maintainer should consolidate the two overlapping fixes quickly to avoid divergence.  
  [HKUDS/nanobot Issue #4111](https://github.com/HKUDS/nanobot/issues/4111)

| Item | Age (days) | Last Activity | Risk |
|------|------------|---------------|------|
| PR #4034 (GitAgent) | 3 | None from maintainer | Low (non-critical) |
| Issue #4107 (bwrap mounts) | 1 | None | Low-Medium (blocked?) |
| Issue #4111 (Heartbeat) | <1 | Two PRs exist | Medium (if not unified) |

*Overall project health: robust.* The maintainer team is responsive, and community contributions are high-quality and well-tested. The backlog is small and well-covered.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-31

## 1. Today’s Overview

The Hermes Agent project experienced very high activity on May 31, with **50 issues updated** (39 still open, 11 closed) and **50 pull requests updated** (46 open, 4 merged/closed). No new releases were published. The community reported a wide range of bugs, security concerns, and feature requests, with several high‑severity issues (P0/P1) being addressed rapidly. The maintainer team appears to be actively reviewing and merging fixes, notably a batch of fixes from contributor `sweetcornna` that were updated today. Overall project health is robust, though the volume of open issues (hundreds) suggests ongoing refinement is needed.

## 2. Releases

No new releases were made today.

## 3. Project Progress (Merged/Closed PRs & Key Fixes)

Four pull requests were merged or closed today:

- **#35588** — `fix(kanban): honor all toolset aliases` (merged) – Ensures profiles configured with `toolsets: ["all"]` or `["*"]` correctly expose Kanban tools, closing #35581.
- **#35597** — `feat: Operationalize holographic memory governance evidence` (closed) – Adds regression coverage and telemetry for holographic memory retrieval.
- **#35611** — `fix: redact_sensitive_text() unconditional Discord mention masking` (closed) – Fixes a bug that broke multi‑bot @-pings on Discord.
- **#35636** — `fix: cronjob create fails/loops when passing model override` (closed) – Resolves a validation error in the cron tool.

Additionally, a large set of fixes authored by `sweetcornna` were updated today (PRs #33820–#33846), addressing skills persistence, compression deadlocks, Telegram/Discord routing, cron double‑fire, missing locales, and fallback provider activation. While not newly merged, these PRs signal substantial progress on stability.

Several high‑priority issues were also closed (e.g., #35584 P0 security config exposure, #30719 P1 cron respawn loop), indicating the team is actively triaging and resolving critical bugs.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal community focus on security, cross‑platform continuity, and developer experience:

- **Security Policies Thread** – [#9179](https://github.com/NousResearch/hermes-agent/issues/9179) (25 comments, closed) – Request to enable GitHub private vulnerability reporting. Generated significant discussion and was closed today, suggesting the maintainers took action.
- **Cross‑Platform Session Handoff** – [#8366](https://github.com/NousResearch/hermes-agent/issues/8366) (5 comments, 6 👍) – A feature request to allow session continuity across CLI, Telegram, and iMessage. High user interest (6 reactions) indicates strong demand.
- **MCP Server Tool First‑Invoke Approval** – [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) (4 comments, 2 👍) – Proposes a security gate before LLM can call any MCP tool. Aligns with other permission‑gating requests.
- **Web UI Build Failure with NODE_ENV=production** – [#27430](https://github.com/NousResearch/hermes-agent/issues/27430) (4 comments) – A deployment‑related bug affecting VPS/CI users.
- **Discord Markdown Table Rendering** – [#21168](https://github.com/NousResearch/hermes-agent/issues/21168) (3 comments) – A usability bug that makes data summaries unreadable on Discord.

The underlying themes are **security**, **multi‑platform parity**, and **deployment robustness**.

## 5. Bugs & Stability

Today’s bug reports span several severity levels, with many already having associated fix PRs.

### Critical (P0)
- **#35584** – `Gateway attaches protected config.yaml via extract_local_files` (closed) – Security hole where a denied write to `~/.hermes/config.yaml` still leaked the file path. Closed with a fix.

### High (P1)
- **#35595** – `/model` command returns structured field list instead of human‑readable message in v0.15. No fix PR yet; regression from v0.14.
- **#30719** – `Agent can schedule gateway-restart cron job causing respawn loop` (closed) – Addressed by a fix that prevents cron‑induced loops.

### Medium (P2) – Representative selection
- **#27430** – `hermes update` fails when `NODE_ENV=production` due to skipped devDependencies. Fix needed.
- **#21168** – Discord markdown tables render as garbage; proposal to auto‑wrap in code fences.
- **#29617** – Empty `web.search_backend` silently disables web tools even when provider API key is set. UX trap.
- **#35654** – Browser tool fails on Windows when arguments contain shell characters (`&`, `|`, `<`, `>`). Root cause: `.cmd` wrapper evaluation.
- **#35576** – Auto‑resume sends stale thread_id to Feishu causing validation error.
- **#35739** – Telegram media messages not routed correctly in DM Topics.
- **#35192** – TUI input box disappears after assistant response, requiring session restart.
- **#35542** – TUI resume listing hides message‑bearing child sessions.
- **#35695** – `extract_media()` false positives on example paths in code blocks.
- **#28802** – Kanban helpers leak SQLite connections in long‑lived processes.
- **#35743** – `skill_view` falsely reports collision when another skill has an asset file with the same name.
- **#35736** – `skill_manage` tool fails when agent mistakenly passes `content` instead of `file_content`.
- **#35738** – TUI layout broken in Warp terminal after `clampStdoutDimensions` fix.

Many of these have corresponding fix PRs (e.g., #35741 fixes #35736), indicating active maintenance.

## 6. Feature Requests & Roadmap Signals

Several feature requests align with a clear community desire for **granular security controls** and **multi‑platform continuity**:

- **Cross‑Platform Session Handoff** – [#8366](https://github.com/NousResearch/hermes-agent/issues/8366) – Would unify conversations across CLI, Telegram, iMessage. Likely a candidate for the next minor release given strong interest.
- **MCP Server Tool First‑Invoke Approval** – [#16462](https://github.com/NousResearch/hermes-agent/issues/16462) – Adds a human‑approval step before LLM can invoke MCP tools for the first time.
- **Per‑Tool / Per‑Toolset Approval Policies** – [#21849](https://github.com/NousResearch/hermes-agent/issues/21849) & [#33905](https://github.com/NousResearch/hermes-agent/issues/33905) – Both request configurable approval rules per tool, beyond the current “dangerous shell command” gate.
- **Per‑User Toolset Restrictions** – [#35479](https://github.com/NousResearch/hermes-agent/issues/35479) – Allow approved pairings to restrict tool access per user.
- **Background Multi‑Agent Harness** – [#35688](https://github.com/NousResearch/hermes-agent/issues/35688) – Lightweight Doer/Reviewer pattern with shared memory, filling a gap between synchronous delegation and full Kanban boards.
- **Chat History Normalization for Strict Backends** – [#29327](https://github.com/NousResearch/hermes-agent/issues/29327) – Adapter for LiteRT and custom OpenAI shims to avoid API validation errors.

**Prediction**: The next version is likely to ship **MCP tool approval** (already has a dedicated issue and PR community) and **improved TUI responsiveness** (multiple TUI bugs reported and fixed). Cross‑platform session handoff may be deferred to a later milestone due to complexity.

## 7. User Feedback Summary

Real‑world pain points expressed in today’s issues:

- **TUI Usability**: Several users report input box disappearance (#35192), broken auto‑scroll (#35671), and layout corruption in specific terminals (#35738). These degrade the core chat experience.
- **Windows Support**: Shell character handling in browser tool (#35654) and broader platform compatibility issues continue to frustrate Windows users.
- **Deployment & CI**: The `NODE_ENV=production` build failure (#27430) affects headless/server deployments, a key use case.
- **Discord & Feishu Integration**: Markdown table rendering (#21168) and auto‑resume failures (#35576) reduce reliability on these platforms.
- **Security Awareness**: Users are actively requesting more granular permission controls (#16462, #21849, #33905, #35479) and were alarmed by the config exposure bug (#35584).
- **Positive Signals**: The swift closure of security issues (#35584, #9179) and the volume of fix PRs from both maintainers and community contributors (e.g., `sweetcornna`, `season179`) indicates a responsive and committed project team.

## 8. Backlog Watch

Several important issues have not received recent maintainer attention and may need escalation:

- **Security Policies & Practices** – [#9179](https://github.com/NousResearch/hermes-agent/issues/9179) was closed today, so this is resolved.
- **Cross‑Platform Session Handoff** – [#8366](https://github.com/NousResearch/hermes-agent/issues/8366) – Created April 12, no assignee, but high community interest (6 👍). May need a design discussion.
- **Tool Permission Gating System** – [#21849](https://github.com/NousResearch/hermes-agent/issues/21849) – Created May 8, no maintainer response. Overlaps with #33905; should be consolidated.
- **Per‑Tool / Per‑Toolset Approval Policies** – [#33905](https://github.com/NousResearch/hermes-agent/issues/33905) – Created May 28, still open. No comment from maintainers.
- **Chat History Normalization** – [#29327](https://github.com/NousResearch/hermes-agent/issues/29327) – Created May 20, no maintainer follow‑up. Could block users of niche backends.
- **Web Search Backend Empty String Trap** – [#29617](https://github.com/NousResearch/hermes-agent/issues/29617) – Created May 21, no fix yet. A simple UX fix would prevent user confusion.

These items represent gaps that, if addressed, would significantly improve developer experience and platform maturity.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-31

## 1. Today's Overview

The project saw **high activity** over the past 24 hours: 8 issues were updated (4 closed), 12 pull requests were touched (3 merged/closed), and a new nightly build was released. Community engagement remains strong, with a mix of bug reports, feature requests, and infrastructure improvements. The nightly build (`v0.2.9-nightly.20260531`) is an automated snapshot from `main` and may be unstable. Overall project health is **moderate** — development is active, but several regressions and usability bugs surfaced after the `v0.2.9` line.

## 2. Releases

**Nightly build**  
`v0.2.9-nightly.20260531.1ce353ba` — [Full changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

- This is an automated build; no stable release today.
- No breaking changes or migration notes are provided.
- **Note**: Users on `v0.2.9` have reported regressions (see §5), so this nightly may contain fixes, but use with caution.

## 3. Project Progress (Merged/Closed Today)

Three pull requests were merged/closed, along with several issues:

- **PR #2969** – `feat(web): add chat image paste and drag-and-drop upload`  
  Merged. Enables image pasting and drag‑and‑drop in the Web UI. Handles extension‑only files and mixed clipboard payloads.  
  [Link](https://github.com/sipeed/picoclaw/pull/2969)

- **PR #2971** – `feat(provider): Add optional Azure Identity support for Azure OpenAI provider`  
  Merged. Adds build‑tag (`azidentity`) optional Azure Identity authentication, useful when local auth is disabled by policy.  
  [Link](https://github.com/sipeed/picoclaw/pull/2971)

- **PR #2974** – `feat(i18n): Add Bangla support bn-in`  
  Merged. Adds Bengali language localisation for the web frontend.  
  [Link](https://github.com/sipeed/picoclaw/pull/2974)

Additionally, four issues were closed:  
- #2742 (bug: gateway starts with no channels, closed as stale)  
- #2880 (bug: permission denied on Android, closed as stale)  
- #2973 (feature request: i18n Bangla, closed after PR #2974)  
- #2970 (feature request: Azure Identity, closed after PR #2971)

## 4. Community Hot Topics

Most active discussions in the last 24 hours:

- **Issue #2952** (3 comments) – Feature request in Chinese:  
  User reports problems with `exec` command actions, QQ channel restart loops, and requests a model/provider picker dropdown with key reuse and API test connection.  
  [Link](https://github.com/sipeed/picoclaw/issues/2952)

- **Issue #2742** (6 comments, now closed) – Bug report about gateway starting with no channels in v0.2.8.  
  This was the most commented issue overall, indicating a significant user pain point that has been resolved.  
  [Link](https://github.com/sipeed/picoclaw/issues/2742)

- **Issue #2972** (2 comments) – Bug: Web UI message chaos after upgrade to v0.2.9; old messages appear in new sessions.  
  Users on FreeBSD with MiniMax provider are affected.  
  [Link](https://github.com/sipeed/picoclaw/issues/2972)

- **Issue #2968** (1 comment, 1 👍) – Bug: `/context` always shows “Compress at: 76800 tokens”.  
  Likely a display/calculation issue with context compression.  
  [Link](https://github.com/sipeed/picoclaw/issues/2968)

**Underlying needs**: Users want a more robust upgrade path, better handling of context compression, and more intuitive model provider configuration.

## 5. Bugs & Stability

**Severity: High**  
- **#2972** – Web UI message chaos after upgrade to v0.2.9. New sessions include old messages.  
  No fix PR yet.  
  [Link](https://github.com/sipeed/picoclaw/issues/2972)

- **#2968** – `/context` always reports “Compress at: 76800 tokens”.  
  Suggests a token counting or compression state bug.  
  [Link](https://github.com/sipeed/picoclaw/issues/2968)

**Severity: Medium**  
- **#2952** – `exec` command `actions:run` issue where models often omit the command on first call, causing extra runs.  
  Also a QQ channel restart loop after successful restart (clear history works around it).  
  [Link](https://github.com/sipeed/picoclaw/issues/2952)

**Severity: Low**  
- **#2976** – Makefile compilation fails due to spaces in `go env GOVERSION` (e.g., “go1.25.10 X:nodwarf5”).  
  Fix PR #2976 is open.  
  [Link](https://github.com/sipeed/picoclaw/pull/2976)

**Regression note**: Two bugs (#2972, #2968) emerged directly after upgrading to v0.2.9, suggesting the release introduced unintended changes in session handling and context compression.

## 6. Feature Requests & Roadmap Signals

- **#2978** – Add OmniRoute as a provider. User asks for guidance or direct integration.  
  [Link](https://github.com/sipeed/picoclaw/issues/2978)

- **#2952** – (already mentioned) Requests dropdown for model providers, key reuse, and API test connection – likely to be addressed in a future UI overhaul.

- **Open PRs** that signal upcoming features:  
  - #2977 – `feat(cron): add get and update actions to cron tool` (allows agents to inspect/edit cron jobs without remove‑add cycles)  
  - #2975 – `feat(telegram): treat reply to bot message as mention in group chats` (improves UX for mention‑only mode)  
  - #2967 – `fix(codex): preserve streamed output text deltas` (fixes empty responses for Codex OAuth)  
  - #2856 – `feat(message): support media attachments and Telegram rich delivery` (stale, but foundational for richer messaging)  
  - #2838 – `feat(agent): support frontmatter tool policy filters` (stale, but adds granular allow/deny for tools)

**Prediction**: The next minor release (v0.3.0 or v0.2.10) will likely include the cron tool enhancement, Telegram reply-as-mention, and Codex streaming fix, as these PRs are actively maintained and address reported bugs.

## 7. User Feedback Summary

- **Pain points**: Multiple users on FreeBSD and Linux report regressions after v0.2.9 (message chaos, context display).  
- **Usability**: The `exec` command workflow is fragile (model often skips the action), and the QQ channel restart behaviour is frustrating (requires clearing context).  
- **Configuration**: Lack of a model provider dropdown with key reuse and API testing is seen as a missing productivity feature.  
- **Satisfaction**: Users appreciate the new features (image paste, Azure Identity, Bangla i18n) but are vocal about stability. The high number of closed issues (4 today) indicates maintainers are responsive, though some stale items remain.

## 8. Backlog Watch

Items that have been open for a while and may need maintainer attention:

- **PR #2856** – `feat(message): support media attachments and Telegram rich delivery`  
  Opened May 11, staleness flagged. No recent activity. Could be a large feature needing review.  
  [Link](https://github.com/sipeed/picoclaw/pull/2856)

- **PR #2838** – `feat(agent): support frontmatter tool policy filters`  
  Opened May 9, stale. Adds important security granularity for tool access.  
  [Link](https://github.com/sipeed/picoclaw/pull/2838)

- **PR #2965** – `fix(tools): stop workspace guard misreading scheme-less URLs`  
  Open since May 29, no maintainer comments yet. Fixes a realistic security/usability issue with `restrict_to_workspace`.  
  [Link](https://github.com/sipeed/picoclaw/pull/2965)

- **Issue #2952** – User feature/bug report in Chinese (May 27). No maintainer response yet.  
  [Link](https://github.com/sipeed/picoclaw/issues/2952)

Maintainers are encouraged to triage these items to avoid further stagnation, especially the two stale feature PRs that could unblock richer agent capabilities.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-05-31

## 1. Today's Overview
NanoClaw shows very high development velocity with **15 pull requests updated** in the last 24 hours (12 open, 3 merged) and **5 open issues** – all active but none yet closed. The project is tackling both quality-of-life improvements (context windows, backup, multi-user) and critical infrastructure fixes (file descriptor exhaustion, self-healing, container mount races on Apple). No new releases were published today, but the pace suggests a significant patch release is likely within days. Overall project health is strong, with a vibrant community contributing multiple features and stability patches simultaneously.

## 2. Releases
*None.* No new releases were published on this date.

## 3. Project Progress – Merged/Closed PRs Today
Three pull requests were merged or closed:

- **#2652 – `fix(container-runner): rewrite OneCLI proxy port for multi-instance installs`** (by matty271828)  
  Corrects the hardcoded `host.docker.internal:10255` in `HTTPS_PROXY` so that multi-instance setups (using `instances.conf`) receive the correct gateway port.  
  [PR #2652](https://github.com/nanocoai/nanoclaw/pull/2652)

- **#2645 – `feat(router): per-agent-group context_messages window for group chats`** (by yairixStudio)  
  Adds an optional per-agent-group context window. When an agent is @-mentioned in a group chat, it now receives the last N unseen messages as a `[Context — last N messages]` block, improving conversational awareness.  
  [PR #2645](https://github.com/nanocoai/nanoclaw/pull/2645)

- **#2521 – `feat(formatter): add from-channel and from-type to XML message attributes`** (by crookies)  
  Emits the originating channel type (`fromDest.channelType`) in XML‑formatted message transcripts, enabling multi‑channel dashboards to display channel‑specific icons.  
  [PR #2521](https://github.com/nanocoai/nanoclaw/pull/2521)

## 4. Community Hot Topics
The most active discussions revolve around security and reliability:

- **Issue #2044 – “v2 Using @chat-adapter/discord changes <URL> handling, makes it worse”** (2 👍, 1 comment)  
  A regression where Discord’s `<URL>` anti‑preview syntax is converted to `[URL](URL)`, enabling unwanted link expansions. Users are clearly frustrated by a feature that worked before v2.  
  [Issue #2044](https://github.com/nanocoai/nanoclaw/issues/2044)

- **Issue #2641 – “Supply chain risk – @gongrzhe/server-gmail-autoauth-mcp”** (1 comment)  
  Warns about a third‑party MCP server that asks for Gmail passwords. The linked Medium article describes a real‑world supply‑chain attack. This has attracted attention from the security‑conscious part of the community.  
  [Issue #2641](https://github.com/nanocoai/nanoclaw/issues/2641)

- **PR #212 – “feat: add WebUI control panel”** (still open since February)  
  Despite being long‑standing, it remains a top‑voted feature. Community members frequently comment on its blocking status.  
  [PR #212](https://github.com/nanocoai/nanoclaw/pull/212)

## 5. Bugs & Stability
Several stability‑critical issues were reported today, ranked by severity:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| 🔴 Critical | [#2655](https://github.com/nanocoai/nanoclaw/issues/2655) | OneCLI gateway **hard‑exits** under burst load due to default 1024 file‑descriptor soft limit (`os error 24`), causing a silent total agent outage. | No |
| 🟠 High | [#2657](https://github.com/nanocoai/nanoclaw/issues/2657) | Lack of **self‑healing**: Docker marks gateway container `unhealthy` but does nothing because `restart:` only fires on container exit. | No |
| 🟠 High | [#2044](https://github.com/nanocoai/nanoclaw/issues/2044) | Discord URL **handling regression** ( <URL> → [URL](URL) ) – a v2 bug that breaks expected behaviour. | No |
| 🟡 Medium | [#2649](https://github.com/nanocoai/nanoclaw/pull/2649) + [#2650](https://github.com/nanocoai/nanoclaw/pull/2650) | **Apple Container mount race** – nested file mounts produce phantom inodes that silently disable all MCP servers. Two companion fix PRs are open. | Yes – #2649 & #2650 (open) |
| 🟡 Medium | [#2656](https://github.com/nanocoai/nanoclaw/pull/2656) (fix PR) | `/add-mnemon` skill entries never run because `mnemon setup` is placed in `entrypoint.sh` but the host overrides the ENTRYPOINT. The fix moves setup to `index.ts`. | Yes (open PR) |
| 🟢 Low | [#2641](https://github.com/nanocoai/nanoclaw/issues/2641) | Supply chain risk from a third‑party MCP server – not a code bug, but a warning for operators. | N/A (awareness) |

**Notable:** PR #2651 ([security] fix interactive origin validation) was opened yesterday to harden the `ask_user_question` response boundary – a proactive security fix.

## 6. Feature Requests & Roadmap Signals
The following user‑requested features signal where NanoClaw is heading:

- **Multi‑user support on a single install** – [#2653](https://github.com/nanocoai/nanoclaw/issues/2653)  
  The data model already supports it, but `src/` initialisation is a blocker. Likely to land in the next minor release, given the community need for shared family Macs.

- **Per‑agent‑group context window** – already merged in PR #2645 (see section 3). This directly addresses the common pain point of agents losing conversation flow in group chats.

- **Backup & disaster recovery** – [#2084](https://github.com/nanocoai/nanoclaw/pull/2084) (open since April)  
  A full backup/restore CLI is in review – essential for production users.

- **GitHub integration with polling mode** – [#2301](https://github.com/nanocoai/nanoclaw/pull/2301) (open since May 6)  
  Adds a no‑port‑required REST polling option for users behind NAT/firewall. High demand for webhook‑free setups.

- **Voice transcription (free Whisper)** – [#2317](https://github.com/nanocoai/nanoclaw/pull/2317)  
  Local, CPU‑friendly voice support – a clear roadmap item for multi‑modal agents.

- **WebUI control panel** – [#212](https://github.com/nanocoai/nanoclaw/pull/212) (blocked since February)  
  Still the most‑wanted feature; maintainers should prioritise unblocking it.

**Prediction for v2.1 / next release:** Multi‑user support, context window (already in), and the fd‑exhaustion fix will likely ship together. Backup and GitHub polling may follow in v2.2.

## 7. User Feedback Summary
Real pain points expressed in the last 24 hours:

- **Security anxiety**: A user (NoamGit) publicly warned about a third‑party MCP that requests Gmail passwords, referencing a real‑world supply‑chain attack. The community is asking for better MCP vetting or guardrails.
- **Silent failures**: The fd‑exhaustion crash (mshirel) and the unhealthy gateway (mshirel) are causing **total agent outages without any alert** – a major production concern.
- **Platform friction**: Apple Container users (jurre‑mbt‑it) are hitting mount‑race conditions that silently disable MCP servers. The fact that two PRs were filed within hours shows frustration.
- **Regression frustration**: Long‑time Discord users (pwinnski) are upset that `<URL>` suppression broke in v2, calling it “worse” than the original behaviour.
- **Multi‑user demand**: A shared‑family‑Mac user (elancode) explicitly requests separate Telegram bots per user on the same host – a clear use case for home labs.

Overall, users appreciate the rapid pace of fixes and features but are vocal about reliability and security gaps.

## 8. Backlog Watch
Several important issues and PRs have been languishing for weeks or months:

| Item | Type | Age | Notes |
|------|------|-----|-------|
| [#212](https://github.com/nanocoai/nanoclaw/pull/212) – WebUI control panel | PR (blocked) | Since Feb 13 (3.5 months) | Most‑requested feature; marked “Blocked” and “Pending Closure”. Needs maintainer decision. |
| [#2044](https://github.com/nanocoai/nanoclaw/issues/2044) – Discord URL regression | Issue | Since Apr 27 (34 days) | No fix yet; 2 thumbs up show community agreement. |
| [#2084](https://github.com/nanocoai/nanoclaw/pull/2084) – Backup system | PR | Since Apr 28 (33 days) | No maintainer review comments visible. |
| [#2301](https://github.com/nanocoai/nanoclaw/pull/2301) – GitHub polling mode | PR | Since May 6 (25 days) | Stale; still open with no merge activity. |
| [#2537](https://github.com/nanocoai/nanoclaw/pull/2537) – Pre‑commit hooks (CI) | PR | Since May 18 (13 days) | Simple CI improvement; no objections but no merge. |

**Call to action:** The project maintainers should review the long‑standing WebUI PR and the backup PR, as these are top‑voted community needs. The Discord regression (#2044) also deserves a fix – it is a v2 regression that breaks existing user workflows.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-05-31

## 1. Today’s Overview
The IronClaw project remains highly active with **16 PRs** and **4 issues** updated in the last 24 hours. Of those PRs, **9 were merged or closed**, indicating strong forward momentum on the “Reborn” trigger and outbound communication system, as well as critical bug fixes in the agent runtime and authentication surfaces. No new releases were published today, though a blocked publication to crates.io (Issue #3259) continues to draw community attention. The project’s health is good, with multiple core contributors driving large feature slices (XL-size PRs) and a low-risk profile across most changes.

## 2. Releases
*No new releases today.* The latest published version on crates.io remains `0.24.0` (March 31, 2026), while tags exist up to `0.27.0`. See Issue #3259 under “Community Hot Topics” for details on the publication blockage.

## 3. Project Progress (Merged/Closed PRs)
Nine PRs were merged or closed today, advancing major Reborn features and fixing two runtime bugs:

- **Reborn Triggers Crate & Trusted Inbound**  
  - [#4261](https://github.com/nearai/ironclaw/pull/4261) – Added `ironclaw_triggers` crate skeleton including domain types, cron validation, and in-memory repository.  
  - [#4254](https://github.com/nearai/ironclaw/pull/4254) – Implemented trusted inbound facade for trigger ingress with replay‑first idempotency.

- **Outbound Communication System**  
  - [#4260](https://github.com/nearai/ironclaw/pull/4260) – Added `CommunicationPreferenceRepository` for tenant/user delivery preferences (in‑memory & filesystem).  
  - [#4255](https://github.com/nearai/ironclaw/pull/4255) – Introduced delivery‑resolution domain types in `ironclaw_outbound`.

- **Auth Surfaces & Credential Migration**  
  - [#4245](https://github.com/nearai/ironclaw/pull/4245) – Completed product‑facing auth HTTP routes (manual token, recovery, refresh, cleanup).  
  - [#4246](https://github.com/nearai/ironclaw/pull/4246) – Migrated NEAR AI MCP credentials to the new `ProductAuthAccount` runtime credential source.  
  - [#4247](https://github.com/nearai/ironclaw/pull/4247) – Design documentation for WebUI v2 auth E2E tests.

- **Bug Fixes**  
  - [#4259](https://github.com/nearai/ironclaw/pull/4259) – Fixed `capability_info` rejecting synthetic capabilities (model could not inspect the tool itself).  
  - [#4258](https://github.com/nearai/ironclaw/pull/4258) – Fixed host runtime dispatch failures being incorrectly routed to terminal `Failed` instead of surfacing tool errors; also coerces `oneOf`/`anyOf` stringified containers.

## 4. Community Hot Topics
- **Issue #3259** – [Publish 0.25.0–0.27.0 to crates.io](https://github.com/nearai/ironclaw/issues/3259)  
  *12 comments* – Downstream consumers are unable to pull versions beyond `0.24.0` due to a dependency on `wasmtime` 28.x CVEs. The community is awaiting a resolution that allows new releases to flow to crates.io. This is the most active issue and represents a real blocker for users.

- **Issue #228** – [Feat: add deny-by-default delegation policy for sub-job creation](https://github.com/nearai/ironclaw/issues/228)  
  *1 comment* – Though only one comment, the issue has been open since February and touches on a fundamental security/control mechanism. The community may be under‑voiced but the need is clear: prevent runaway sub‑jobs from LLM hallucinations or prompt injections.

- **Issue #4108** – [Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)  
  *0 comments, automated report* – A scheduled nightly E2E run failed, specifically the “Full E2E / E2E (extensions)” job. No discussion yet, but it signals a potential stability regression.

## 5. Bugs & Stability
| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | Nightly E2E failure (`extensions` job) | Open #4108 (automated) | Not yet identified |
| **Medium** | `capability_info` incorrectly rejects synthetic capabilities | Fixed | [#4259](https://github.com/nearai/ironclaw/pull/4259) (merged) |
| **Medium** | Route dispatch failures cause terminal `Failed` instead of tool error; stringified `oneOf`/`anyOf` containers break agent loop | Fixed | [#4258](https://github.com/nearai/ironclaw/pull/4258) (merged) |

Additionally, the crates.io publication blockage (#3259) is a **high‑severity infrastructure bug** that prevents all downstream consumers from accessing bug fixes and new features.

## 6. Feature Requests & Roadmap Signals
Several open PRs point to the next major features likely to land in the coming weeks:

- **Reborn Triggers Persistence** – [#4263](https://github.com/nearai/ironclaw/pull/4263) (open, XL) adds a libSQL backend for trigger repository, the first durable storage for triggers.
- **Outbound Resolution Engine** – [#4262](https://github.com/nearai/ironclaw/pull/4262) (open, XL) introduces candidate selection for communication delivery.
- **Slack Reborn ProductAdapter** – [#4035](https://github.com/nearai/ironclaw/pull/4035) (open, XL) is the first reviewable slice of Slack integration under the Reborn architecture.
- **Auth Enhancement** – [#4257](https://github.com/nearai/ironclaw/pull/4257) (open, XL) wires OAuth challenge enrichment for GSuite, Notion MCP, and GitHub PAT.
- **Provider Reasoning Preservation** – [#4230](https://github.com/nearai/ironclaw/pull/4230) (open, XL) will preserve OpenAI/Codex reasoning summaries and enable Anthropic thinking for compatible models.
- **GitHub SSO** – [#4229](https://github.com/nearai/ironclaw/pull/4229) (open, XL) adds native GitHub OAuth to WebUI v2.

These features strongly suggest the next minor or major release will focus on Reborn trigger and outbound system completion, along with richer authentication options.

## 7. User Feedback Summary
- **Pain Point – Version Blockage** (#3259): Downstream users are stuck on `0.24.0` from crates.io, missing up to three minor releases. This is the single most reported friction point.
- **Pain Point – Agent Runtime Failures** (#4258, #4259 fixes): Users experienced unexpected run failures when LLMs passed malformed tool arguments (stringified JSON) or when `capability_info` was called. Both have been resolved today.
- **Satisfaction**: The steady stream of large feature PRs and rapid bug fixing indicates a healthy development pace that should address many user concerns in the near term.

## 8. Backlog Watch
- **Issue #228** – [Feat: denial policy for sub‑job creation](https://github.com/nearai/ironclaw/issues/228)  
  *Opened 2026‑02‑19, last updated 2026‑05‑31 – Comments: 1* – This long‑standing feature request for a deny‑by‑default delegation policy has received minimal maintainer engagement. As the Reborn trigger system evolves, the need for a policy layer to control sub‑job creation becomes more pressing. Maintainers should consider triaging this for inclusion in the next planning cycle.

- **Issue #3259** – [Publish 0.25.0–0.27.0 to crates.io](https://github.com/nearai/ironclaw/issues/3259)  
  *Opened 2026‑05‑05, last updated 2026‑05‑30 – Comments: 12* – Although not “long‑unanswered” in age, the blockage has persisted for nearly a month. The maintainer team should prioritize resolving the wasmtime CVE dependency to unblock downstream consumption.

*No other stale issues or PRs were identified in today’s snapshot.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-05-31

## 1. Today's Overview
Project activity remains very low, with no new issues or merged pull requests in the last 24 hours. The only update is a stale pull request (#1465) that was touched today, indicating ongoing attention to a persistent bug around scheduled task cleanup. No new releases were published, and the issue tracker is completely empty, which may suggest either a quiet period or that the team is focused on internal work. Overall, the project appears to be in a maintenance phase with minimal community interaction.

## 2. Releases
No new releases were recorded for this date. The latest release information is unavailable.

## 3. Project Progress
No pull requests were merged or closed today. The single PR updated is #1465, which remains open.

## 4. Community Hot Topics
The only active discussion point is pull request **#1465** ([link](https://github.com/netease-youdao/LobsterAI/pull/1465)), titled *"fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现"*. This PR addresses a ghost session bug where deleted scheduled tasks reappear after restart. It has zero comments and reactions, indicating very low community engagement. The underlying need is clearly a data consistency issue between the gateway cron removal and local SQLite session cleanup.

## 5. Bugs & Stability
No new bugs were reported in the last 24 hours. However, the open PR #1465 directly targets a stability problem: deleted scheduled tasks persisting as empty ghost sessions after application restart. The root cause is identified (missing local session deletion), and a fix exists in draft form. This bug is of **moderate severity** as it affects user trust in task management, but the lack of recent reports suggests it may not affect a large number of users.

## 6. Feature Requests & Roadmap Signals
No feature requests were filed or discussed today. The project roadmap remains unclear from recent activity. The only signal is the continued work on the scheduled-tasks fix, indicating that improving task lifecycle management is a current priority.

## 7. User Feedback Summary
No user feedback or pain points were captured in the last 24 hours. The absence of new issues or comments suggests either satisfaction with the current state or lack of active community usage.

## 8. Backlog Watch
- **PR #1465** ([link](https://github.com/netease-youdao/LobsterAI/pull/1465)) – Open since 2026-04-04 (58 days), last updated today. This is the only item requiring maintainer attention. It is a fix for a reported bug (linked issue #1359) but has not been merged or reviewed. The staleness and lack of comments raise concern about whether maintainers are actively processing contributions. No other long-unanswered items exist.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-05-31

## 1. Today's Overview
Activity on the Moltis repository was minimal today, with no new issues or releases and only a single open pull request updated. The project appears to be in a low-activity phase, likely reflecting a weekend or a period of focused internal development. The lone PR (#1088) addresses a specific improvement in the OpenAI Codex provider, indicating ongoing maintenance work. Overall project health remains stable, but community engagement via issues was absent.

## 2. Releases
No new releases were published today. The latest release history remains unchanged.

## 3. Project Progress
No pull requests were merged or closed today. The only open PR updated in the last 24 hours is:

- **#1088 (OPEN): [codex] Handle OpenAI Codex final tool-call arguments**  
  Author: s-salamatov  
  This PR improves the Codex provider by recording final `response.function_call_arguments.done` payloads and synthesizing a streaming argument delta when none were emitted. It also ensures empty accumulated argument strings flow through decode diagnostics to prevent missing-argument errors.  
  [View PR](https://github.com/moltis-org/moltis/pull/1088)

No feature advancements or fixes were completed today.

## 4. Community Hot Topics
No issues or pull requests received comments or reactions in the last 24 hours. The single open PR (#1088) has zero reactions. There are no active community discussions to highlight.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported today. The project currently shows no open issues. Stability is presumed unchanged from previous reports.

## 6. Feature Requests & Roadmap Signals
No feature requests were submitted today. The only actionable signal is the open PR #1088, which improves the OpenAI Codex provider’s handling of streaming tool-call arguments. This may indicate upcoming refinements to tool-use functionality in the next release.

## 7. User Feedback Summary
No user feedback (comments, reactions, or issues) was recorded today. There is no data to assess satisfaction or pain points from the community.

## 8. Backlog Watch
There are no open issues requiring maintainer attention. The only open PR (#1088) is recent and appears to be under active development. No long-unanswered items exist in the backlog.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-31

## 1. Today’s Overview
Project activity remains high with **7 issues updated** and **2 pull requests** touched in the last 24 hours, though no new releases were published. Bug reports dominate the day: three new issues were filed (a workspace-killing job validation error, an MCP process leak, and a memory compaction failure) alongside a Windows shell window flash duplicate. One PR was closed (improving slash command suggestions) and another remains open (routing non‑standard provider kwargs). The overall picture suggests the team is actively addressing stability and UX regressions, but the volume of critical bugs indicates the current release (v1.1.9) may need a hotfix.

## 2. Releases
**No new releases** were created today. The latest published version remains **v1.1.9** (as referenced in issue #4833).

## 3. Project Progress
**Merged/Closed PR:**  
- **#4810** – [feat(console): improve chat slash skill suggestions](https://github.com/agentscope-ai/QwenPaw/pull/4810) (closed, under review). This PR enhances the slash command popup by showing only skill names, limiting to 5 visible items with scrolling, and adding debug logs. It addresses a user experience request for more compact skill suggestions.

**Closed Issue:**  
- **#4828** – [Bug: Windows cmd window flash](https://github.com/agentscope-ai/QwenPaw/issues/4828) was closed, but the identical root cause was re‑opened later in #4832 (see Bugs section). The fix or resolution for #4828 is not yet visible.

## 4. Community Hot Topics
The most active discussions in the last 24 hours revolve around **Windows usability and workspace stability**:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#4123 – Windows: execute_shell_command flashes a console window](https://github.com/agentscope-ai/QwenPaw/issues/4123) | 8 | Persistent bug from May 8; still open. Users report the cmd window appears on every shell execution. |
| [#4454 – /mission command freezes Console](https://github.com/agentscope-ai/QwenPaw/issues/4454) | 4 | Console becomes unresponsive after `/mission`; process remains alive but UI freezes. No fix yet. |
| [#4835 – Invalid job in jobs.json fails entire workspace](https://github.com/agentscope-ai/QwenPaw/issues/4835) | 1 | High‑severity: a single malformed job prevents the whole workspace from starting. |
| [#4834 – MCP server processes accumulate across restarts](https://github.com/agentscope-ai/QwenPaw/issues/4834) | 1 | Process leak leads to slow console loading after repeated restarts. |

**Underlying need:** Users are demanding better error isolation (single invalid job should not block everything) and proper resource cleanup (MCP processes, Windows shell windows). The `/mission` freeze (#4454) indicates a concurrency or UI‑state bug that needs maintainer investigation.

## 5. Bugs & Stability
**New bugs filed today (2026-05-31):**

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#4835](https://github.com/agentscope-ai/QwenPaw/issues/4835) | **High** – workspace fails to start if any job in `jobs.json` has a missing field (e.g., `session_id`). No graceful degradation. | No |
| [#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834) | **Medium** – MCP server processes are not killed on restart, leading to process accumulation and slow loading. | No |
| [#4833](https://github.com/agentscope-ai/QwenPaw/issues/4833) | **Medium** – `Failed to compact memory in pre_reasoning hook` error in v1.1.9. Likely a memory management regression. | No |
| [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) | **Low** – Windows cmd window flash on every shell command (duplicate of #4123, #4828). Root cause: missing `CREATE_NO_WINDOW` flag. | #4828 was closed but the bug reappeared; no fix PR linked. |

**Ongoing high‑severity bugs (not filed today):**  
- [#4454 – Console freeze on `/mission`](https://github.com/agentscope-ai/QwenPaw/issues/4454) – remains open with no fix PR.
- [#4123 – Windows shell flash](https://github.com/agentscope-ai/QwenPaw/issues/4123) – open since May 8; many user reports.

## 6. Feature Requests & Roadmap Signals
While no explicit feature requests were filed today, the **one open PR** points to a desired capability:

- **#4689** – [feat(providers): route non-standard generate_kwargs into extra_body](https://github.com/agentscope-ai/QwenPaw/pull/4810) (open) – enables compatibility with non‑OpenAI providers (e.g., DashScope’s `enable_search`) by forwarding unknown kwargs into the request body. This signals a push to broaden provider support beyond the OpenAI API shape.

The closed PR **#4810** (slash skill suggestions) indicates the team is investing in **console UX improvements**, likely for the next minor release. Given the bug load, the next release (v1.2.0) will probably prioritize stability fixes over new features, but the provider routing PR (#4689) may land soon.

## 7. User Feedback Summary
Real pain points expressed in the last 24 hours:

- **Windows users are frustrated**: multiple reports of cmd window flashing (#4832, #4828, #4123). The issue has been open for weeks with no permanent fix.
- **Workspace fragility**: one invalid job kills the entire workspace (#4835). Users expect partial failures to be tolerated.
- **Resource leaks degrade experience**: MCP process accumulation (#4834) forces users to manually kill processes or restart the machine.
- **Console freezing** after `/mission` (#4454) makes the tool unusable for mission‑related workflows.

Satisfaction signals are absent; all activity is bug‑related. The community is engaged (comments on issues), but the lack of merged fixes for the oldest bugs may erode trust.

## 8. Backlog Watch
Two important issues have been **open for weeks with no maintainer response or fix**:

- **#4123** – [Windows shell command flashes console window](https://github.com/agentscope-ai/QwenPaw/issues/4123) (created May 8, 8 comments) – the most‑voted bug. A fix should be trivial (add `CREATE_NO_WINDOW` flag), yet it remains open despite multiple duplicates.
- **#4454** – [`/mission` command freezes Console](https://github.com/agentscope-ai/QwenPaw/issues/4454) (created May 17, 4 comments) – a usability blocker for mission features. No PR or milestone assigned.

These require **maintainer attention** to either triage with a fix timeline or request more debugging info. The project’s health would benefit from closing or commenting on these long‑standing issues.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-31

## Today's Overview
Project activity was minimal over the past 24 hours. Only one issue was closed—a repository-wide security scan chore—with no new pull requests or releases. No open issues or active PRs were updated, indicating a period of low development velocity or a stable state. The project appears to be in a maintenance mode today with no feature work or bug fixes reported.

## Releases
No new releases were created today.

## Project Progress
No pull requests were merged or closed today. The only closed item is **Issue #609** (chore: repository-wide Codex Security scan for webhook identity routing), which was an automated security audit rather than a feature or fix. No functional changes to the codebase occurred.

## Community Hot Topics
There were no highly active discussions. The sole issue updated today, **Issue #609**, received one comment from the author. Given it is a chore (security scan), it does not reflect ongoing user engagement or debate.

- [Issue #609 – chore(security): repository-wide Codex Security scan for webhook identity routing](https://github.com/qhkm/zeptoclaw/issues/609)

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. No stability-related issues are currently open.

## Feature Requests & Roadmap Signals
No feature requests were submitted or discussed today. The roadmap remains unchanged; no signals indicate upcoming functionality.

## User Feedback Summary
No user-reported feedback, pain points, or satisfaction comments were captured today. The community is either satisfied or inactive.

## Backlog Watch
There are no long-unanswered issues or pull requests needing maintainer attention. The project’s backlog shows zero open issues and zero open PRs as of this update. The single item from today was promptly closed. Maintainer response time appears good for submitted items, though overall activity is very low.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-31

## 1. Today's Overview

ZeroClaw is in a period of intense development, with **50 issues and 50 pull requests updated within the last 24 hours**. 31 issues remain open/active, 19 were closed, and of the PRs, 35 are open while 15 have been merged or closed. No new releases were published today. The project shows healthy community engagement, with several high‑risk RFCs under review and a steady stream of bug fixes and feature additions. The core team is actively processing PRs, though a number of contributions are tagged `needs-author-action` or `needs-maintainer-review`, indicating some bottlenecks in the review pipeline.

## 2. Releases

No new releases were created on 2026-05-31. The latest public release remains **v0.8.0-beta-1** (as referenced in issue #6876). No migration notes or breaking changes to report.

## 3. Project Progress

Today’s closed issues and merged PRs reflect progress across multiple areas:

- **Bug fixes:**  
  - [#4842](https://github.com/zeroclaw-labs/zeroclaw/issues/4842) – `zeroclaw update` now correctly downloads the aarch64 binary on Raspberry Pi.  
  - [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) – Cron job output is now routed to configured channels (not just the web dashboard).  
  - [#5289](https://github.com/zeroclaw-labs/zeroclaw/issues/5289) – Bedrock provider no longer sends the `x-api-key` header, fixing 403 errors.  
  - [#5256](https://github.com/zeroclaw-labs/zeroclaw/issues/5256) – 500 Internal Server Error with llama.cpp resolved.  

- **Enhancements accepted (closed as implemented or RFC accepted):**  
  - [#5731](https://github.com/zeroclaw-labs/zeroclaw/issues/5731) – Manifest provider support added.  
  - [#6883](https://github.com/zeroclaw-labs/zeroclaw/issues/6883) – Shared reply‑message constructor `SendMessage` RFC accepted.  
  - [#6327](https://github.com/zeroclaw-labs/zeroclaw/issues/6327) – Desktop menu‑bar chat channels overview.  
  - [#6329](https://github.com/zeroclaw-labs/zeroclaw/issues/6329) – Desktop tray menu items (quit, restart, copy token, logs).  
  - [#5843](https://github.com/zeroclaw-labs/zeroclaw/issues/5843) – Model‑wise reasoning configuration RFC accepted (though still blocked).  

No PRs from the top‑20 list were merged today; the 15 merged/closed PRs are not listed in the sample.

## 4. Community Hot Topics

The most active discussions this week:

- **#5937** – [Refactor: unify providers architecture and reqwest client management](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) (9 comments). Users and maintainers are debating a deep refactor of the provider module to eliminate code duplication and inconsistent `reqwest` usage. This is a high‑risk, p2 enhancement that likely influences the upcoming release.  
- **#5982** – [Per‑sender RBAC for multi‑tenant deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) (8 comments). Strong demand for role‑based access control to allow one instance to serve different user classes with isolated workspaces and tool sets.  
- **#6909** – [Computer‑use support (screen interaction like Codex / Peekaboo)](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) (4 comments + 4 👍 on related #4467). Users are requesting desktop GUI control capability, noting that competitors already offer it.  
- **#6954** – [Route scheduled tasks through the orchestrator message pipeline](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) (3 comments). An RFC that ties together multiple cron‑related bugs (#6037, #6105, etc.), showing the community’s desire for a unified scheduling pipeline.  
- **#6969** – [Unified output routing model](https://github.com/zeroclaw-labs/zeroclaw/issues/6969) (3 comments). A user migrating from Letta requests per‑peer modality preference and an agent‑driven send_via tool, reflecting a gap in reply delivery control.

**Highly upvoted items:**  
- #4467 – [MCP resource and prompt support](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) (4 👍) – long‑standing request.  
- #4879 – [Gemini CLI OAuth not working](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) (2 👍) – a critical workflow blocker.

## 5. Bugs & Stability

Open bugs reported or updated today, ranked by severity:

| Issue | Severity | Description | Status |
|-------|----------|-------------|--------|
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | S1 – workflow blocked | Gemini CLI OAuth fails after successful authentication | No fix PR; 2 comments |
| [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | S1 – workflow blocked | Ollama provider fails when tools are needed, blocks session | In progress; no fix PR |
| [#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022) | S1 – workflow blocked | Kimi K2.6 fails with 400 invalid temperature due to hardcoded 0.7 | New today; no fix |
| [#5866](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) | S1 – workflow blocked | Telegram group bot ignores replies on its own messages when `mention_only=true` | No fix PR |
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | S2 – degraded behavior | `allowed_private_hosts` does not work for domains that resolve to private IPs | In progress; no fix PR |
| [#6720](https://github.com/zeroclaw-labs/zeroclaw/issues/6720) | S2 – degraded behavior | `context_aware_tools` config field declared but never read | Accepted, no fix |
| [#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) | S1 – workflow blocked | `allowed_tools` in risk profiles does not restrict MCP tools | Accepted, no fix PR |
| [#6916](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) | S1 – workflow blocked | Shell subprocess can OOM container; missing memory limits | Blocked, needs maintainer review |

**Regression note:** No regressions specifically flagged in today’s activity, but the close of #4842 (aarch64 update failure) and #6647 (cron routing) removes two long‑standing S1 bugs.

**Fix PRs in flight:**  
- #6122 (Gemini 429 retry‑after parsing) is open to address #4879 partially.  
- #7035 (media pipeline vision path) resolves an image attachment bug.  
- #7034 (WhatsApp LID bot mention) fixes a group gating issue.

## 6. Feature Requests & Roadmap Signals

High‑impact features under active discussion or with open PRs indicate the likely direction of the next major release:

- **Provider architecture overhaul** (#5937) – unifying provider traits and `reqwest` management.  
- **Multi‑tenant RBAC** (#5982) – per‑sender access control.  
- **Computer‑use (screen interaction)** (#6909) – desktop GUI control.  
- **Memory lifecycle decoupling** (#6850) – `MemoryStrategy` trait to separate policy from storage.  
- **Scheduled task pipeline** (#6954) – route cron jobs through the orchestrator.  
- **Unified output routing** (#6969) – per‑peer modality and agent `send_via` tool.  
- **Skill‑scoped tool activation** (#6915) – temporary tool elevation during skill execution.  
- **Process memory limits for shell tools** (#6916) – container safety.  
- **Email channel improvements** (#7021) – XOAUTH2, observer mode, read‑only IMAP tools.  
- **Conversation loop overhaul** (#7030) – a massive 28‑item PR encompassing context pipeline, streaming tool execution, retry with backoff, and agent‑directed provider selection.

**Prediction:** The next minor release (v0.9 or v0.8.1) will likely include provider refactoring, cron pipeline routing, skill tool elevation, and email XOAUTH2. RBAC and computer‑use are high‑risk and may require a separate major version.

## 7. User Feedback Summary

Real‑world pain points expressed in today’s issues:

- **Deployment frustrations:** Users on Raspberry Pi and aarch64 hit platform‑specific binary bugs (#4842); Docker users lack clear documentation (#6760).  
- **Provider compatibility:** Ollama tool calls break sessions (#5962), Gemini OAuth is broken (#4879), Kimi/K2.6 fails due to hardcoded temperature (#7022), custom endpoints have TLS issues (#5797).  
- **Cron and scheduled tasks:** Cron output not reaching channels is a recurring complaint (#6647, #6954). Users want more granular control over delivery (CLI flags, channel selection).  
- **Security and tool restrictions:** MCP tools bypass risk profile allowlists (#6876); `allowed_tools` not enforced at execution (#6914).  
- **Channel‑specific issues:** Telegram group bot ignores replies (#5866), WhatsApp bot mention detection broken (#7034).  
- **Desired capabilities:** Per‑sender RBAC for multi‑tenant deployments (#5982), computer‑use for desktop automation (#6909), Mattermost on‑call mode (#3100), and unified output routing (#6969).  

Overall sentiment is positive (active contributions, many RFCs), but frustration exists around slow‑moving bug fixes (especially Gemini OAuth) and the complexity of configuring security policies.

## 8. Backlog Watch

Issues and PRs that have been open for an extended period without maintainer response or resolution:

| Item | Created | Last Activity | Status | Notes |
|------|---------|---------------|--------|-------|
| [#3100](https://github.com/zeroclaw-labs/zeroclaw/issues/3100) – Mattermost on‑call mode | 2026-03-10 | 2026-05-31 (update) | Open, in‑progress | Only 1 comment; no assignee |
| [#4467](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) – MCP resource/prompt support | 2026-03-24 | 2026-05-31 (update) | Open, in‑progress | 4 👍; no maintainer response in 2 months |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) – Gemini OAuth broken | 2026-03-28 | 2026-05-31 (update) | Open | S1 severity; no fix merged; PR #6122 open but untouched for 35 days |
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) – `allowed_private_hosts` ineffective | 2026-03-29 | 2026-05-31 (update) | Open, in‑progress | S2 bug with no fix PR |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) – Audit of 153 commits lost in bulk revert | 2026-04-24 | 2026-05-31 (update) | Open, in‑progress | Needs maintainer action |

**PRs needing maintainer review (tagged `needs-maintainer-review`):**  
- #5361 (fix `codex exec` subcommand)  
- #6876, #6914, #6915, #6916, #6917 (all security/tool‑related enhancements)  
- #6850 (MemoryStrategy trait RFC)

**PRs needing author action (`needs-author-action`):** 10 PRs listed in the top‑20, including #5797 (TLS CA cert), #5461 (Slack broadcasts), #5418 (concurrency), #5242 (native tool calls for custom endpoints), #5458 (UTF‑8 truncation), #5539 (Gemini loadCodeAssist), #5175 (auth module public), etc. These contributions risk becoming stale unless the authors respond to reviewer comments.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*