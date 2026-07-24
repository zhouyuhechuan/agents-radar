# OpenClaw Ecosystem Digest 2026-07-24

> Issues: 317 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-24 01:59 UTC

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

# OpenClaw Project Digest – 2026-07-24

## Today's Overview

OpenClaw saw **extremely high activity** over the past 24 hours: 317 issues updated (220 open, 97 resolved), 500 pull requests updated (312 open, 188 merged/closed), and zero new releases. The project remains in a continuous delivery cadence with significant community engagement on regressions introduced in recent versions (2026.7.1 and 2026.6.11). Several **P0/P1 bugs** are being actively patched, while a large number of feature requests and design discussions (e.g., unified cron, memory MVP) continue to accumulate without maintainer decisions. The backlog of `clawsweeper:needs-maintainer-review` issues remains a concern.

## Releases

No new versions were published today. The latest release remains the 2026.7.1 series (beta and stable).

## Project Progress

**Merged/closed pull requests today (2026-07-24):** 5 notable merges, mostly bug fixes for channel-specific issues and infrastructure improvements.

- **WhatsApp reactions restored** – PR [#113178](https://github.com/openclaw/openclaw/pull/113178) fixes agent‑selected reactions being rejected in active DMs/groups.
- **iOS release screenshot stalls fixed** – PR [#113187](https://github.com/openclaw/openclaw/pull/113187) removes 60‑140 s XCTest quiescence stalls in Settings.
- **Feishu outbound lifecycle settled** – PR [#113152](https://github.com/openclaw/openclaw/pull/113152) ensures auto‑replies complete full outbound hook lifecycle before settlement.
- **Configuration path fix for OPENCLAW_HOME** – PR [#87255](https://github.com/openclaw/openclaw/pull/87255) prevents nested `.openclaw` when the env var already points to a state directory.
- **Approval prompt formatting declared per channel** – PR [#112686](https://github.com/openclaw/openclaw/pull/112686) gives each channel a capability descriptor for rendering approval markdown, enabling richer formatting on iMessage and future channels.

Additionally, several PRs advanced toward review: a fix for large `commands.ownerAllowFrom` lists ([#103797](https://github.com/openclaw/openclaw/pull/103797)), a prevention of plugin‑skipping during upgrades ([#95384](https://github.com/openclaw/openclaw/pull/95384)), and a new feature to accept WebSocket trace context for OpenTelemetry correlation ([#113189](https://github.com/openclaw/openclaw/pull/113189)).

## Community Hot Topics

Most active issues by comment/reaction volume:

- **#44925 – Subagent completion silently lost** ([link](https://github.com/openclaw/openclaw/issues/44925)) – 22 comments, 2 👍. A long‑standing P1 bug (since March) where subagent results are lost on timeout without retry or notification. Still open, with an open fix PR linked.
- **#102020 – Second message fails with “reply session initialization conflicted”** ([link](https://github.com/openclaw/openclaw/issues/102020)) – 15 comments, 1 👍. Regression affecting cross‑channel sessions (Signal, Telegram).
- **#94228 – Native Anthropic `thinking` block bricks long tool‑use threads** ([link](https://github.com/openclaw/openclaw/issues/94228)) – 14 comments, 2 👍. Permanent 400 error after signature check fails on multi‑turn sessions. No fix PR yet.
- **#92043 – Compaction timeout resets entire pipeline with no partial progress reuse** ([link](https://github.com/openclaw/openclaw/issues/92043)) – 13 comments, 3 👍. 180 s wall‑clock timeout makes legitimate long compactions fail identically every turn.
- **#108435 – Gateway fails to start after upgrade to 2026.7.1** ([link](https://github.com/openclaw/openclaw/issues/108435)) – 10 comments, 2 👍. P0 regression affecting systemd and manual launches.

The underlying needs are clear: **reliability of agent orchestration**, **session state integrity across channels**, and **graceful handling of provider‑specific limitations** (Anthropic signatures, compaction timeouts).

## Bugs & Stability

Critical regressions and stability issues reported today (ranked by severity):

- **P0 – Gateway fails to start (2026.7.1)** – [#108435](https://github.com/openclaw/openclaw/issues/108435). Blocks all operation. No fix PR yet, but maintainers have logs.
- **P0 – Cron store migration silently drops config (5.28→6.1)** – [#90378](https://github.com/openclaw/openclaw/issues/90378). SQLite migration broke job delivery mode and didn’t preserve previous config. Linked fix PR open.
- **P1 – All channels enter broken state after 2026.6.11** – [#101814](https://github.com/openclaw/openclaw/issues/101814). One message per session then permanent silence. Awaiting live repro.
- **P1 – Telegram DM replies fall back after stale DM‑scope cleanup** – [#111519](https://github.com/openclaw/openclaw/issues/111519). Regression in 2026.7.2‑beta.3.
- **P1 – Subagent completion silently lost** – [#44925](https://github.com/openclaw/openclaw/issues/44925). Open fix PR exists but not yet merged.
- **P1 – Compaction timeout prevents completion** – [#92043](https://github.com/openclaw/openclaw/issues/92043). No fix PR yet.
- **P1 – Tool result channel becomes empty after several calls** – [#99481](https://github.com/openclaw/openclaw/issues/99481). Affects 2026.7.1‑beta.1 on macOS.
- **P1 – Cron tool schema incompatible with llama.cpp grammar‑constrained calling** – [#108580](https://github.com/openclaw/openclaw/issues/108580). Regression in 2026.7.1.

Numerous older P1/P2 bugs remain in `stale` status without maintainer review, including issues around session context bloat, MCP loopback reconnection, backup stalls, and security concerns.

## Feature Requests & Roadmap Signals

New and recurring feature requests from today’s top issues:

- **“Everything is a cron”** – [#110950](https://github.com/openclaw/openclaw/issues/110950) proposes unifying heartbeat, watchers, and scheduled automation under a single cron primitive. Closed as “maintainer” but still a strong signal.
- **Context window percentage in system prompt** – [#38568](https://github.com/openclaw/openclaw/issues/38568) would inject usage into the Runtime section. Repeatedly requested.
- **Suppress sub‑agent announce** – [#8299](https://github.com/openclaw/openclaw/issues/8299) wants a config option instead of relying on model output.
- **Session TTL / max lifetime** – [#45390](https://github.com/openclaw/openclaw/issues/45390) to prevent runaway context growth.
- **Memory MVP CLI/skill surface** – [#42651](https://github.com/openclaw/openclaw/issues/42651) and [#42648](https://github.com/openclaw/openclaw/issues/42648) propose `remember`/`recall`/`forget` commands and a write pipeline with dedup.
- **Pre‑compaction notification & deferral** – [#38520](https://github.com/openclaw/openclaw/issues/38520) would let agents finish stateful work before forced compaction.
- **Azure Foundry GPT Realtime Talk** – [#87325](https://github.com/openclaw/openclaw/issues/87325) requests gateway relay support.
- **Group scope consolidation** – [#7524](https://github.com/openclaw/openclaw/issues/7524) would allow `groupScope: "main"` similar to `dmScope`.

These features point toward **better session lifecycle management**, **permissions and safety** (skill manifests, dry‑run mode), and **multi‑channel parity**.

## User Feedback Summary

Real pain points from the community:

- **Silent failures are the #1 frustration** – agents dropping results, sessions freezing, timeouts without notification. Multiple users report wasted hours troubleshooting non‑obvious failures.
- **Upgrade breaks existing setups** – several regressions from 2026.6.11 and 2026.7.1 have made users wary of upgrading. One reporter had to roll back after gateway startup failure (#108435).
- **Context management is unpredictable** – compactions firing even with `mode: "off"` (#48579), bootstrap files eating 20‑30% of context every turn (#67419), no way to enforce session lifetimes.
- **Channel inconsistencies** – approvals not formatted on iMessage, Discord missing MCP tools, WhatsApp images failing on second read, Feishu streaming latency.
- **Operational friction** – `openclaw backup create` stalls on large installations (#42273), logs show UTC with no local time option (#46748), `openclaw doctor` gives conflicting status (#87637).

Satisfaction signals are harder to find, but the number of reopened issues and detailed field reports (e.g., [#41372](https://github.com/openclaw/openclaw/issues/41372) with 25 findings) suggests users invest heavily in self‑hosted deployments and expect higher reliability.

## Backlog Watch

Long‑unanswered tickets that need maintainer attention (sorted by age and impact):

- **#44925** (Mar 13) – Subagent silent loss, P1, linked fix PR open but no merge.
- **#94228** (Jun 17) – Anthropic signature bricking, P1, fix PR absent.
- **#92043** (Jun 10) – Compaction timeout, P1, needs product decision.
- **#90378** (Jun 4) – Cron migration broke config, P0, fix PR linked but open.
- **#8299** (Feb 3) – Sub‑agent announce suppression, P2.
- **#87325** (May 27) – Azure Foundry Talk support, P2, needs security review.
- **#42820** (Mar 11) – Feishu message tool polluted by poll schema, P1, linked PR open.
- **#43374** (Mar 11) – All LLM calls time out simultaneously, P1, needs live repro.
- **#42273** (Mar 10) – Backup stalls on large installs, P2.
- **#49259** (Mar 17) – Prune orphaned sessions, P2.

Many of these are tagged `clawsweeper:needs-maintainer-review` and `needs-product-decision`. The project would benefit from a dedicated triage session to clear these long‑standing issues, especially those with clear user impact and existing fix attempts.

---

## Cross-Ecosystem Comparison

# AI Agent Open-Source Ecosystem Cross-Project Comparison Report
**Date:** 2026-07-24  
**Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is experiencing intense concurrent development across multiple projects, with an estimated 500+ issues and 800+ pull requests updated in a single 24-hour period. The ecosystem shows clear convergence around core challenges—session reliability, cross-channel parity, and security hardening—while projects pursue divergent architectural philosophies ranging from monolithic reference implementations to modular, embeddable frameworks. A significant tension exists between rapid feature iteration (CoPaw, ZeroClaw) and stabilization phases (OpenClaw, IronClaw), with the latter groups absorbing community pain from regressions introduced in recent releases. Community investment remains high, evidenced by detailed bug reports and contributed fix PRs, but several projects maintain backlogs of unanswered issues exceeding 60 days, creating fragmentation risk as users may migrate to more responsive alternatives.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | New Releases | Health Score |
|---------|---------------------|--------------------|--------------------|--------------|--------------|
| **OpenClaw** | 317 | 500 | 188 | 0 | B (active but regressions weigh) |
| **ZeroClaw** | 50 | 50 | ~1 | 0 | C (high activity, low merge ratio, S0 bugs) |
| **IronClaw** | 31 | 50 | 18 | 0 | B (intense stabilization, no release blocker) |
| **Hermes Agent** | 50 | 50 | 2 | 0 | B- (P1 OAuth loop, session bugs) |
| **CoPaw** | 38 | 50 | 23 | 1 (v2.0.1-beta.2) | A- (high velocity, critical regressions open) |
| **NanoBot** | 8 | 37 | 31 | 0 | A (best merge ratio, low bug count) |
| **Picoclaw** | 1 | 15 | 7 | 0 | B (steady, low community engagement) |
| **NanoClaw** | 1 | 10 | 4 | 0 | B (targeted hardening, container lifecycle) |
| **Moltis** | 2 | 5 | 5 | 2 | A (focused, all PRs merged) |
| **LobsterAI** | 3 | 3 | 2 | 0 | D (critical bugs stale >90 days, low activity) |
| **ZeptoClaw** | 2 | 1 | 0 | 0 | C- (critical security bug, no merge) |
| **NullClaw** | 0 | 0 | 0 | 0 | Inactive |
| **TinyClaw** | 0 | 0 | 0 | 0 | Inactive |

**Health Score Key:** A = Fast, responsive, low regressions; B = Active with manageable issues; C = High activity but low resolution rate or critical bugs; D = Stalled or unmaintained.

---

## 3. OpenClaw's Position

OpenClaw remains the **largest and most comprehensive reference implementation** in the ecosystem, with 317 issues and 500 PRs updated in 24 hours—3–6× the activity of the next-busiest projects (ZeroClaw, Hermes, CoPaw). Its advantages include:

- **Broadest channel support:** WhatsApp, Feishu, iMessage, Telegram, Signal, Discord—with per-channel formatting capability (#112686) that peers lack.
- **Most mature feature surface:** Memory MVP, cron unification, subagent orchestration, OpenTelemetry correlation, multiple provider integrations.
- **Largest community investment:** 220 open issues and 312 open PRs indicate deep engagement, though maintainer bandwidth is strained (tagged `needs-maintainer-review` backlog).

**Key weaknesses vs peers:**
- **Regressions per release:** 5 P0/P1 bugs introduced in 2026.7.1 alone; NanoBot merged 31 PRs with zero critical regressions in the same period.
- **Maintainer bottleneck:** Issues like [#44925](https://github.com/openclaw/openclaw/issues/44925) (subagent silent loss, P1) have open fix PRs but no merge decision after 4+ months. NanoBot resolves similar bugs within days.
- **Complexity tax:** 180-second compaction timeouts, session context bloat, and P0 gateway failures (#108435) create operational overhead that simpler projects (Moltis, PicoClaw) avoid.

**Technical approach:** OpenClaw follows a "universal gateway" architecture—a single runtime handling all channels, providers, and agent types. This contrasts with ZeroClaw's multi-agent routing approach and IronClaw's composition-based Reborn architecture, giving OpenClaw breadth but at the cost of edge-case fragility.

---

## 4. Shared Technical Focus Areas

The following requirements emerge consistently across **5+ projects**, signaling ecosystem-wide priorities:

### Session & Context Management
- **Session TTL/Max Lifetime:** OpenClaw (#45390), CoPaw, Hermes (#14694), ZeroClaw (#9191)
- **Compaction Timeout Handling:** OpenClaw (#92043), Hermes (#29390), CoPaw (#6323), ZeroClaw
- **Context Window Visibility:** OpenClaw (#38568), ZeroClaw (#8966)

### Cross-Channel Parity & Reliability
- **Channel-Specific Formatting:** OpenClaw (#112686, iMessage approval rendering), CoPaw (governance policy blocks), ZeroClaw (#8999, small model compatibility)
- **Telegram/Slack Webhook Stability:** OpenClaw (#102020), IronClaw (#6548), ZeroClaw (#9188)
- **Message Deduplication & Crash Recovery:** ZeroClaw (#9187, WeChat sync cursor), OpenClaw (Feishu lifecycle)

### Security Hardening
- **Subprocess Environment Scrubbing:** ZeptoClaw (#644, P1-critical), NanoBot (#4594, shell guard), ZeroClaw (#9204, Landlock)
- **Admin-Sender Allowlists:** NanoBot (#4889), ZeroClaw (#6378), OpenClaw (#103797)
- **Credential Encryption Architecture:** ZeroClaw (#9127, KeySource trait), IronClaw (#3997, signing)

### Scheduling & Automation
- **Unified Cron/Scheduling:** OpenClaw (#110950, "Everything is a cron"), CoPaw (#6316, per-cron model selection), ZeroClaw (#9191, cron timeout)
- **Agent-Type Cron Jobs:** CoPaw, ZeroClaw, OpenClaw

### Provider Interoperability
- **A2A Protocol:** ZeroClaw (#3566, outbound client + tools), OpenClaw (subagent model)
- **Model Fallback Chains:** NanoBot (#5017, fallback badge), PicoClaw (#3200, configurable fallback)
- **SSE Streaming Consolidation:** ZeroClaw (#8838, unified transport)

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | CoPaw | ZeroClaw | IronClaw | Hermes Agent |
|-----------|----------|---------|-------|----------|----------|--------------|
| **Target User** | Self-hosters, power users | Channel-oriented teams | Multi-agent developers | Enterprise/cloud | Devops, staging QA | Desktop users |
| **Architecture** | Universal gateway | Modular agent loop | ReAct+Qwen-centric | Multi-gateway routing | Composition-based | Desktop-first |
| **Channel Focus** | Max breadth (10+) | Core 5 channels | Docker/Web, Chinese ecosystem | Telegram/WeChat/Discord | Slack/Telegram/WebChat | Desktop + Telegram |
| **Feature Cadence** | Continuous delivery | Stable patches | Rapid iteration | Milestone-driven (v0.9.0) | Reborn refactoring | Maintenance-heavy |
| **Community Model** | Large, contributor-driven | Maintainer-led, responsive | Active in Chinese ecosystem | Growing, PR-heavy | Internal+QA focused | Contributor-invested |
| **Key Differentiator** | Most comprehensive | Highest merge velocity | Deep model integration (Qwen) | A2A protocol pioneer | Production-hardened | Session-state innovation |

**Notable Absences:**
- **Desktop-first UX** is uniquely Hermes Agent's domain (collapsible sidebar, Kanban plugins).
- **Container-native design** (Podman, Docker) is most advanced in Moltis and CoPaw.
- **End-to-end encryption** only in NanoClaw (Matrix E2EE via PR #2844).

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity, Responsive Maintenance
- **NanoBot** (A-tier) – 31 PRs merged in 24h, zero new critical bugs. Model for healthy project governance.
- **CoPaw** (A-tier) – 23 PRs merged, 1 pre-release shipped daily. Highest release cadence in ecosystem.
- **Moltis** (A-tier) – 5/5 PRs merged, 2 releases. Focussed, low noise.

### Tier 2: High Activity, Some Struggles
- **OpenClaw** – Ecosystem leader but maintainer bottleneck and regression load are creating risk.
- **ZeroClaw** – Extremely active but 49 open PRs with low merge ratio; S0 data-loss bugs without fix PRs.
- **IronClaw** – Intense stabilization phase; no release for 21+ days despite active PR volume.
- **Hermes Agent** – Strong community fixes but P1 OAuth loop and session bugs remain unresolved.

### Tier 3: Stable, Lower Engagement
- **PicoClaw** – Steady dependency management and feature work; low community volume.
- **NanoClaw** – Targeted hardening with healthy merge cadence; minimal user feedback.
- **ZeptoClaw** – Focused on critical security fix; otherwise low activity.

### Tier 4: Inactive or Stalled
- **LobsterAI** – Critical bugs (database corruption) unaddressed for >90 days. Community trust eroding.
- **NullClaw, TinyClaw** – No activity. Likely abandoned or in hibernation.

---

## 7. Trend Signals

### From Community Feedback Across Projects

**1. Silent Failures Are the #1 User Frustration**
Across OpenClaw (#44925, subagent loss), CoPaw (#6363, tool call corruption), ZeroClaw (#9188, message drop), and Hermes (#67762, cost reset), the dominant complaint is **agents failing without notification**. Users report hours wasted debugging non-obvious failures. This is an ecosystem-wide signal that observability and error propagation must become first-class features, not afterthoughts.

**2. Performance Regressions Erode Trust**
OpenClaw's 2026.7.1 introduced 5 P0/P1 regressions. CoPaw's v2.0 added ~2s fixed overhead (#6307). ZeroClaw's Telegram parser drops messages. Users are becoming "upgrade-shy"—multiple reports of rolling back versions. **Stability and regression testing** are now the highest-value investments for maintainer teams.

**3. Security Is Becoming a Hard Requirement**
Subprocess credential exposure (ZeptoClaw #644), shell injection bypasses (NanoBot #4594), Landlock sandbox locking daemons (ZeroClaw #9204), and OAuth retry loops (Hermes #70401) indicate that **security is no longer optional** for self-hosted agents exposed to real-world data. Expect TOTP approval flows and credential encryption to become baseline features.

**4. Multi-Agent Orchestration Is the Next Battleground**
ZeroClaw's A2A protocol PR (#9324), OpenClaw's subagent model, CoPaw's agent-type cron, and Hermes' Mixture-of-Agents all point to **multi-agent architectures** as the defining feature race of 2026–2027. The winner will be the project that makes reliable inter-agent routing and state sharing transparent to users.

**5. Users Want Flexible Model Routing**
The pattern of "fast cloud model for simple queries, private local model for sensitive data" is emerging across NanoBot (#4253), CoPaw (#6316, per-cron models), and PicoClaw (#3200, fallback chains). **Per-conversation model overrides** and **configurable fallback chains** are table-stakes features.

**6. Docker/NAS/HDD Users Face Systemic Pain**
CoPaw users report 1.5-hour updates on HDD (#6380). Docker users lose tool environments on each upgrade (#6344). OpenClaw backup stalls on large installations (#42273). The ecosystem is optimizing for developers on fast hardware, leaving **operational efficiency for lower-end deployments** as an underserved need.

**7. Windows Remains the Weakest Platform**
ZeroClaw desktop installer crashes (#9290), IronClaw `serve` fails on Windows (#6590), CoPaw PATH issues (#6239), NanoBot test runner lacking `python` (#5062). The ecosystem is heavily Linux/Mac-oriented, and Windows users face friction that limits adoption in enterprise environments.

---

## Key Recommendations for AI Agent Developers

1. **Prioritize error observability:** Implement structured failure notifications (not silent drops) and expose retry/diagnostics UI.
2. **Invest in session-state stability:** Compaction, TTL, and recovery should be the top architectural concern—users will tolerate fewer features before they tolerate data loss.
3. **Watch A2A protocol adoption:** ZeroClaw's PR #9324 is the most concrete implementation; its interface design may become the ecosystem norm.
4. **Benchmark against NanoBot:** For teams seeking a highly responsive maintenance model, NanoBot's 31:1 merge-to-bug ratio and 5-day average issue resolution provide a clear target.
5. **Avoid over-featuring without stabilization:** OpenClaw and CoPaw's regression pain demonstrates that rapid feature release cycles without regression test suites erode the trust advantage that early-adopter communities provide.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-24

## 1. Today's Overview
The project saw high activity with 8 issues (3 open) and 37 PRs (6 open) updated in the last 24 hours. A total of 31 PRs were merged or closed, indicating strong maintenance momentum. No new releases were published. The focus was on security hardening, workspace-boundary fixes, WebUI polish, and cross-channel reliability. Community engagement remains healthy, with feature requests like per-conversation model switching now resolved.

## 2. Releases
None — no new version tags were created on this date.

## 3. Project Progress
Below are key merged/closed PRs today that advanced functionality or fixed issues:

- **Security & Workspace Guard**
  - [PR #4889](https://github.com/HKUDS/nanobot/pull/4889) – Added `channels.admin_senders` allowlist to protect destructive commands (`/restart`, `/stop`) from non-admin users.
  - [PR #4594](https://github.com/HKUDS/nanobot/pull/4594) – Shell guard now treats `=` as a path delimiter, closing a bypass like `curl --output=/etc/passwd`.
  - [PR #4987](https://github.com/HKUDS/nanobot/pull/4987) – Workspace validation bound to opened file handles with `O_NOFOLLOW` (still open with conflict label).
- **WebUI Enhancements**
  - [PR #5061](https://github.com/HKUDS/nanobot/pull/5061) – Simplified model preset settings with reusable presets and explicit call order; legacy configs get one-click conversion.
  - [PR #5017](https://github.com/HKUDS/nanobot/pull/5017) – WebUI now shows which fallback model is actually handling a turn via a hover badge.
  - [PR #5065](https://github.com/HKUDS/nanobot/pull/5065) – Media directory access works again when `restrictToWorkspace` is enabled.
  - [PR #5067](https://github.com/HKUDS/nanobot/pull/5067) – Composer model badge stays in sync after settings changes.
  - [PR #5060](https://github.com/HKUDS/nanobot/pull/5060) – Responsive layout improvements and settings search polish.
  - [PR #5058](https://github.com/HKUDS/nanobot/pull/5058) – Unified flat surfaces for settings and dark mode.
- **Agent Loop & Tools**
  - [PR #5056](https://github.com/HKUDS/nanobot/pull/5056) – Length recovery now preserves all output segments across `finish_reason="length"`.
  - [PR #5055](https://github.com/HKUDS/nanobot/pull/5055) – Telegram markdown splitter no longer hangs on long single-line code fences.
  - [PR #5039](https://github.com/HKUDS/nanobot/pull/5039) – DOCX table content (including nested and merged cells) is now preserved during extraction.
- **Channels & Infrastructure**
  - [PR #5069](https://github.com/HKUDS/nanobot/pull/5069) – QR connection cancellation now ignores late confirmations for WeChat/Feishu.
  - [PR #5066](https://github.com/HKUDS/nanobot/pull/5066) – Stale exec sessions are retained after cleanup failure, allowing later retries.
  - [PR #5068](https://github.com/HKUDS/nanobot/pull/5068) – Session listing tolerates files removed concurrently.
  - [PR #5042](https://github.com/HKUDS/nanobot/pull/5042) – Cron store no longer drops all jobs when one has `"schedule": null`.
  - [PR #5057](https://github.com/HKUDS/nanobot/pull/5057) – MCP tool schemas with arbitrary `$ref` pointers are normalized for strict providers (e.g., Kimi).

## 4. Community Hot Topics
The most discussed item today is **Issue #4253** (6 comments), a feature request for overriding the model per conversation. It was closed, suggesting the maintainers have either implemented it or decided not to. The second most active is **Issue #5059** (4 comments), asking which browser versions are supported – a sign of growing community interest in browser-based usage.

- [Issue #4253](https://github.com/HKUDS/nanobot/issue/4253) – Override model per conversation (closed)
- [Issue #5059](https://github.com/HKUDS/nanobot/issue/5059) – Browser version support inquiry (closed)

**Underlying needs:** Users want flexible model routing (fast vs. private) and clearer compatibility documentation.

## 5. Bugs & Stability
Three bugs were reported today:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#5051](https://github.com/HKUDS/nanobot/issue/5051) (open) | `AgentRunner` length recovery drops earlier output segments; only the last continuation is kept. | [PR #5056](https://github.com/HKUDS/nanobot/pull/5056) (open) addresses this |
| **High** | [#5028](https://github.com/HKUDS/nanobot/issue/5028) (open) | Media directory and `restrictToWorkspace` conflict – uploaded files via Feishu land in `media/` but workspace guard prevents access. | [PR #5065](https://github.com/HKUDS/nanobot/pull/5065) (merged) fixes the WebUI preview, but the underlying tool access may still be broken. |
| **Low** | [#5062](https://github.com/HKUDS/nanobot/issue/5062) (closed) | Test `test_workspace_scope` uses `python` command unavailable on Debian/Ubuntu. | [PR #5063](https://github.com/HKUDS/nanobot/pull/5063) / [#5064](https://github.com/HKUDS/nanobot/pull/5064) (merged) |

Older bugs updated today: [#4592](https://github.com/HKUDS/nanobot/issue/4592) (ExecTool path extraction, closed by PR #4594) and [#4940](https://github.com/HKUDS/nanobot/issue/4940) (session metadata lost after restart, closed).

**Assessment:** Two high-severity bugs remain open. The length recovery issue (#5051) has an open fix PR, while the media/workspace conflict (#5028) is partially addressed but may need a more comprehensive solution.

## 6. Feature Requests & Roadmap Signals
- **Model handling** – PR #5061 and issue #4253 indicate a push toward more flexible model presets and per-conversation overrides. Expect this to land in an upcoming release.
- **Per-turn fallback visibility** – PR #5017 was merged, adding visual feedback when a fallback model is used. This is a direct community need.
- **Browser support** – Issue #5059 closed without code changes; likely answered via documentation. No strong roadmap signal.
- **MCP lifecycle decoupling** – Issue #4858 (open, refactor) proposes moving MCP state out of `AgentLoop`. This is a design improvement that may appear in a future refactoring release.

## 7. User Feedback Summary
- **Pain points**:
  - Workspace-restriction conflicts with media files (Feishu uploads) – reported by KuruZaphkiel (#5028).
  - Length recovery losing earlier parts of long responses – reported by martin1847 (#5051).
  - Linux test environment lacking `python` command – reported by flyzstu (#5062, fixed).
- **Use cases**:
  - Alternating between fast cloud models and private local models per conversation (rombert, #4253).
  - Managing official accounts across multiple browser versions (qteamo, #5059).
- **Satisfaction indicators**:
  - High PR merge velocity (31 merged today) signals responsive maintenance.
  - Feature requests like model override are being actively addressed.

## 8. Backlog Watch
- **Issue #4858 (refactor, p2)** – MCP provider lifecycle in `AgentLoop`. Open since July 9, one comment. No assignee. This is a significant architectural change and may need a design discussion.
- **PR #4987 (conflict)** – Filesystem workspace check v2. Open since July 19 with a conflict label. It touches security-sensitive code and could block other fixes.
- **PR #5042 (conflict)** – Cron null schedule fix. Open since July 22 with a conflict label. Small but could cause data loss for cron users.
- **Issue #5051 (bug, open)** – Length recovery missing segments. Has an open PR (#5056) but not yet merged; should be prioritized for the next patch release.

All items have links to the respective GitHub pages. Maintainers should consider reviewing the conflicted PRs and assigning issue #4858 to a core contributor.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-24

## 1. Today's Overview
Activity remains high: 50 issues and 50 pull requests were updated in the last 24 hours, with 33 open/active issues and 28 open PRs. No new release was published today. The community is actively reporting bugs (many in the desktop and session‑state areas) and contributing fixes – several critical and high‑severity problems were identified, including an OAuth retry loop and a session‑UI connectivity degradation. The project is in a maintenance‑heavy phase with substantial PR activity addressing both regressions and long‑standing feature requests.

## 2. Releases
**None** – no new versions were cut today.

## 3. Project Progress
Two PRs were merged or closed today:

- **[#67768 – fix(cli): clean up oneshot resources before exit](https://github.com/NousResearch/hermes-agent/pull/67768)** (CLOSED)  
  A P2 bug fix that ensures `hermes -z` properly releases MCP, aiohttp, memory, terminal, browser, and SQLite resources before interpreter teardown. This resolves resource leaks after one‑shot responses.

- **[#70455 – fmt(js): `npm run fix` auto-fix](https://github.com/NousResearch/hermes-agent/pull/70455)** (CLOSED)  
  Automated formatting fix from the CI auto‑fix workflow. Squash‑merged on passing CI.

Several significant open PRs were updated today and represent work in progress:

- **#70458** – New additive verbs on the `ContextEngine` ABC (salvage of PR #51226).  
- **#70462** – Collapsible message navigation sidebar for WebUI (implements #69532).  
- **#70454** – Reject redacted credential placeholders in config (fixes #42727).  
- **#70461** – Add `serve` to agent command allowlist so shell hooks actually fire in desktop mode (fixes #69825).  
- **#70464** – Desktop port conflict detection (fixes #69925).  
- **#70443** – Documentation clarifying xurl skill search behaviour.

## 4. Community Hot Topics
The most active issues (by comment count) highlight recurring pain points:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#66875](https://github.com/NousResearch/hermes-agent/issues/66875) | 8 | Latest session does not switch after navigating to non‑chat tabs (Plugins/Artifacts). |
| [#69314](https://github.com/NousResearch/hermes-agent/issues/69314) | 7 | Telegram gateway behind HTTP proxy gets stuck in retry loop with CLOSE_WAIT sockets. |
| [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | 6 | Session cost resets to $0 on gateway restart (blocker for billing features). |
| [#69551](https://github.com/NousResearch/hermes-agent/issues/69551) | 5 | Desktop SSH remote mode broken with non‑default profiles (hardcoded path). |
| [#513](https://github.com/NousResearch/hermes-agent/issues/513) | 5 | Feature: Two‑phase context compression (prune then compact) inspired by Kilocode. |
| [#14694](https://github.com/NousResearch/hermes-agent/issues/14694) | 4 | Anti‑thrashing protection permanently disables auto‑compression with no recovery. |

The underlying need is clear: users are **begging for session‑state stability, reliable proxy handling, and proper cost tracking**. The two‑phase compression (#513) and idle pre‑compression (#29390) ideas have strong community support and are being actively discussed as roadmap candidates.

## 5. Bugs & Stability
Multiple new bugs were filed today or saw updates. Ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **P1** | [#70401](https://github.com/NousResearch/hermes-agent/issues/70401) | OAuth credential pool enters unbounded 401 retry loop (ignores stop signals) | No |
| **P2** | [#70445](https://github.com/NousResearch/hermes-agent/issues/70445) | Desktop remote session loading is slow, cancels on navigate, can spin forever | No |
| **P2** | [#70424](https://github.com/NousResearch/hermes-agent/issues/70424) | Desktop: clicking chat session from Kanban/Artifacts does not return to chat | No |
| **P2** | [#69930](https://github.com/NousResearch/hermes-agent/issues/69930) | Desktop GUI websocket reconnects on a ~30‑45s grid, causing UI freeze | No |
| **P2** | [#69825](https://github.com/NousResearch/hermes-agent/issues/69825) | `serve` command never registers shell hooks | Yes – [#70461](https://github.com/NousResearch/hermes-agent/pull/70461) |
| **P3** | [#70400](https://github.com/NousResearch/hermes-agent/issues/70400) | Desktop app missing window controls on WSLg | No |
| **P3** | [#70444](https://github.com/NousResearch/hermes-agent/issues/70444) | Project list order jumps when entering/exiting chats | No |
| **P3** | [#61003](https://github.com/NousResearch/hermes-agent/issues/61003) | False‑positive 'Stale systemd unit' warning on startup | No |

The **P1 OAuth loop** (#70401) is a security‑boundary risk – it self‑sustains until process kill. **Desktop session‑switching** bugs (#70424, #69930) indicate broader renderer/WebSocket stability issues that may be linked to the same root cause (stale session list, connection handling).

## 6. Feature Requests & Roadmap Signals
New feature requests and PRs today point toward several likely next‑version inclusions:

- **Message navigation sidebar** (PR #70462, implementing #69532) – collapsible list of user messages for quick jumping, similar to DeepSeek.  
- **Context engine ABC verbs** (PR #70458, RFC #36765) – salvage of a two‑phase compression interface. Likely to be merged soon.  
- **Opt‑in compression progress notices** (PR #70457, #52995) – lets Telegram/Discord users see compression status.  
- **Org‑skill namespace** (PR #70459) – token‑gated discovery and provenance for organisation skills.  
- **Redacted credential rejection** (PR #70454) – prevents mis‑configuration from persisting placeholders.  
- **Cursor Models billing via standalone plugin** (#70140) – request to reuse Cursor Pro subscription for Hermes’ Grok provider.  
- **Idle time‑gap pre‑compression** (#29390 – closed but implemented) – compressing stale sessions before user returns.

**Prediction for v0.20.0**: The context engine verbs (#70458), compression progress notices (#70457), and credential safety (#70454) are likely candidates. The message sidebar (#70462) is also a strong contender given the PR is ready.

## 7. User Feedback Summary
Real pain points expressed in today’s issues:

- **Session‑switching frustration**: Users are stuck on non‑chat tabs and cannot return to conversation via sidebar (#66875, #70424).  
- **Proxy degradation**: HTTP proxies for Telegram cause permanent connection leaks – a production blocker for corporate deployments (#69314).  
- **Cost tracking blind spot**: `agent.session_estimated_cost_usd` resets to zero on restart, making billing unreliable (#67762).  
- **Profile handling inconsistencies**: SSH remote mode breaks with non‑default profiles; `HERMES_HOME` is sometimes ignored (#52669, #69551).  
- **MoA quality concerns**: Reference models fabricate tool execution text (#61452) – a major trust issue for Mixture‑of‑Agents mode.  
- **UI freeze**: Desktop websocket reconnects cause renderer stalls that only clear on user input (#69930).  
- **False‑positive warnings**: Systemd unit check emits misleading errors (#61003).  

Satisfaction signals: The community is actively contributing fixes (22 PRs updated, 2 merged) and new features (collapsible sidebar, credential safety). The rapid adoption of the `MoA` feature is driving both bug reports and enhancement requests (progress indicators, privacy filters).

## 8. Backlog Watch
The following issues and PRs have been open for an extended period and likely require maintainer attention:

| Issue/PR | Opened | Severity | Last Update | Why it matters |
|----------|--------|----------|-------------|----------------|
| [#14694](https://github.com/NousResearch/hermes-agent/issues/14694) | 2026-04-23 | P1 | 2026-07-24 | Anti‑thrashing protection permanently disables compression – a severe UX blocker for long sessions. No fix PR yet. |
| [#513](https://github.com/NousResearch/hermes-agent/issues/513) | 2026-03-06 | P3 | 2026-07-24 | Long‑requested two‑phase context compression (now partially addressed by PR #70458). Still waiting for merge. |
| [#47359](https://github.com/NousResearch/hermes-agent/issues/47359) | 2026-06-16 | P3 | 2026-07-24 | Backend update reports failure even when successful – confusing users in remote mode. |
| [#52669](https://github.com/NousResearch/hermes-agent/issues/52669) | 2026-06-25 | P3 | 2026-07-24 | System prompt hardcodes `~/.hermes` – affects installs with custom `HERMES_HOME`. |
| [#67768 PR](https://github.com/NousResearch/hermes-agent/pull/67768) | 2026-07-19 | P2 | 2026-07-24 | Fix for oneshot resource cleanup – **already merged today** but was aging for 5 days. |
| [#63298 PR](https://github.com/NousResearch/hermes-agent/pull/63298) | 2026-07-12 | P2 | 2026-07-24 | Preserve queued prompt boundaries – important for desktop session hydration. Still open. |

**Key takeaway**: The community is steadily working through a backlog of session‑state bugs and feature requests. Several P1/P2 issues (OAuth loop, session switching) are still without fix PRs and should be prioritised.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-24

## 1. Today's Overview
Project activity on 2026-07-24 was moderate, driven primarily by automated dependency management and a small batch of merged feature/fix pull requests. 15 pull requests were updated in the last 24 hours (7 merged/closed, 8 open), while only one issue saw activity – a stale bug report that was closed. No new releases were published. The project continues to show steady maintenance momentum, with important feature work (remote WebSocket mode, configurable fallback chains) moving forward alongside routine dependency bumps and security fixes.

## 2. Releases
No new releases were cut today.

## 3. Project Progress
**Merged/Closed PRs (non‑dependency):**
- **#3118** — Add remote Pico WebSocket mode to `picoclaw agent` ([PR](https://github.com/sipeed/picoclaw/pull/3118)). This enables connecting to a remote agent via WebSocket while preserving local behavior. Merged.
- **#3115** — Fix inline data URL media extraction for generic tool output ([PR](https://github.com/sipeed/picoclaw/pull/3115)). Fixes session‑history corruption when `data:image/…` strings appear in plain tool text. Merged.
- **#3286** — Update Go and `x/text` for `govulncheck` ([PR](https://github.com/sipeed/picoclaw/pull/3286)). Addresses security vulnerabilities reported by Govulncheck. Merged.
- **#3237, #3236, #3238, #3235** — Dependency bumps for `golang.org/x/sync`, `github.com/github/copilot-sdk/go` (to 1.0.6), `github.com/aws/aws-sdk-go-v2/config` (to 1.32.29), and `github.com/pion/rtp` (to 1.10.3). All closed as stale or superseded by newer bumps.

**Notable Open PRs (in progress):**
- **#3200** — Add configurable default fallback chain for models in the web UI ([PR](https://github.com/sipeed/picoclaw/pull/3200)). Backend API and UI changes are ready for review.
- **#3222** — Refactor deltachat implementation, dropping legacy features and reducing code by ~200 LOC ([PR](https://github.com/sipeed/picoclaw/pull/3222)). Adds `show_invite_link` and renames `invite_link` → `join_invite_link`.

## 4. Community Hot Topics
The only issue updated in the last 24 hours was **#3195**, a closed bug report about OpenAI GPT not working on NanoKVM with the default configuration ([Issue](https://github.com/sipeed/picoclaw/issues/3195)). It drew 4 comments from the reporter and maintainers, reflecting user interest in the new NanoKVM 2.4.0 integration. The issue was closed as stale, but the interaction suggests the configuration documentation may need clarification for NanoKVM users.

No other issues or PRs attracted significant comments or reactions. The community is currently quiet, with most activity centred on automated dependency updates.

## 5. Bugs & Stability
**Resolved bugs this cycle:**
- **#3195** (moderate severity) — OpenAI GPT models failed on NanoKVM with default config. Closed as stale; no evidence of a root‑cause fix, but the issue status implies either user error or a stale configuration that has since been corrected.
- **#3115** (moderate severity) — Session‑history corruption caused by misinterpretation of base64 data URLs in tool output. Fixed and merged.
- **#3286** (high severity, security) — Govulncheck detected vulnerabilities in Go and `x/text`. Fixed by updating dependencies.

No new bugs were reported today. The project remains stable, with the most impactful stability issues addressed in the past 24–48 hours.

## 6. Feature Requests & Roadmap Signals
**Recently merged features:**
- Remote WebSocket mode (`--remote ws://…`) for the agent CLI (#3118) — points toward headless/remote agent deployments.
- Configurable default fallback chain (#3200, still open) — expected in the next minor release. This will allow users to define a ordered list of fallback models in the web UI.

**Signals from open PRs:**
- Deltachat refactoring (#3222) suggests improved messaging integration is being polished.
- Dependency bumps to `github.com/github/copilot-sdk/go` v1.0.8 (currently open as #3291) indicate preparation for the latest Copilot SDK.

No explicit feature requests were filed in the last 24 hours, but the direction is clear: the project is investing in remote agent modes, model fallback chains, and third‑party SDK updates.

## 7. User Feedback Summary
Direct user feedback is sparse. The closed issue #3195 reflects a pain point for users deploying PicoClaw on NanoKVM – the default configuration did not work with OpenAI GPT. The frustration is mitigated by maintainer engagement, but the lack of a documented workaround in the issue thread leaves a gap. The fix in #3115 addresses a less visible but annoying corruption bug that likely affected users employing generic tools like `read_file` or `exec`. Overall, users can expect a smoother experience with remote agent connections and fallback model selection in the near future.

## 8. Backlog Watch
Several open pull requests are accumulating age or have been marked as stale. The following items need maintainer attention:

- **#3263** (actions/setup-node bump from v6 to v7) — Open since July 16, marked as stale. Without review, CI may lag behind.
- **#3262** (actions/setup-go bump from v6 to v7) — Same status and age as above.
- **#3222** (deltachat refactor) — Open since July 3, last updated July 23. Likely awaiting final review and merge.
- **#3200** (configurable fallback chain) — Open since July 1, no recent comments. A feature that has significant user impact; should be prioritised.

No long‑unanswered issues were identified; the only issue was closed.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-24

## 1. Today's Overview
Project activity was moderate, with **10 pull requests** updated in the last 24 hours (4 merged/closed, 6 open) and **1 open bug issue** receiving attention. The team focused on **stability fixes** (duplicate container spawns, typing indicator behavior, orphan container reconciliation) and merged two significant feature PRs—native **Matrix E2EE** support and **Telegram thread tracking**. No new releases were published. Overall health is stable with a healthy cadence of fixes and incremental improvements.

## 2. Releases
No new releases today. (Latest release is unchanged.)

## 3. Project Progress (Merged/Closed PRs)
Four pull requests were merged or closed in the last 24 hours, advancing both features and hardening:

- **[#2844 – feat(matrix): native persistent E2EE adapter via matrix-bot-sdk](https://github.com/nanocoai/nanoclaw/pull/2844)**  
  Replaces the Beeper Chat SDK bridge with a native Matrix adapter using `matrix-bot-sdk` + Rust‑based crypto. This enables **true end‑to‑end encryption** for Matrix rooms without relying on a third‑party bridge.

- **[#2892 – fix(telegram): enable thread support](https://github.com/nanocoai/nanoclaw/pull/2892)**  
  Sets `supportsThreads: true` for the Telegram adapter so forum/topic threads are correctly tracked and messages routed appropriately.

- **[#3120 – Keep typing indicator alive through a single long tool call](https://github.com/nanocoai/nanoclaw/pull/3120)**  
  Prevents the typing indicator from disappearing prematurely when an agent runs a long‑running tool, improving user experience.

- **[#3115 – fix(onecli): block legacy Gmail API routes](https://github.com/nanocoai/nanoclaw/pull/3115)**  
  Adds idempotent network rules to block traffic to legacy `www.googleapis.com` Gmail endpoints, ensuring all Gmail interactions go through the modern `gmail.googleapis.com` API.

## 4. Community Hot Topics
The only active issue remains the most‑discussed:

- **[#2466 – [Bug, Low Priority, Hardening] Duplicate container spawn race on wakeContainer](https://github.com/nanocoai/nanoclaw/issues/2466)**  
  Reported two months ago, this issue describes a race condition where concurrent script execution and host sweep can spawn two identical containers that process the same message. With 2 comments and no reactions, it has not drawn broad attention, but it indicates a **reliability gap in container lifecycle management**. The emergence of a related fix (PR #3119) suggests the maintainers are actively addressing the underlying cause.

No other issue or PR received comments or reactions today.

## 5. Bugs & Stability
| Severity | Bug / Issue | Status | Fix PR |
|----------|-------------|--------|--------|
| **Medium** | **Duplicate container spawn race** – two containers processing same message when `wakeContainer` runs concurrently with host sweep ([#2466](https://github.com/nanocoai/nanoclaw/issues/2466)) | Open, low priority | [#3119](https://github.com/nanocoai/nanoclaw/pull/3119) – reconciles untracked orphan containers to prevent duplicate per‑group spawns |
| **Low** | **Reaction delivery non‑best‑effort** – failed reaction sends may block or raise errors | Fixed by [#3121](https://github.com/nanocoai/nanoclaw/pull/3121) (open) | Open PR changes delivery to best‑effort |
| **Low** | **Orphan container accumulation** – after 5d uptime an agent group reached 3 concurrent containers due to `*/15` sweep | Addressed by [#3119](https://github.com/nanocoai/nanoclaw/pull/3119) (open) | Same as above |
| **Low** | **Legacy Gmail API route leakage** – legacy endpoints bypassed modern control | Fixed in [#3115](https://github.com/nanocoai/nanoclaw/pull/3115) (merged) | Merged |
| **Low** | **Unknown slash commands misclassified** – treated as `passthrough`, causing silent drops | Fix in [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) (open since May) | Not yet merged |

## 6. Feature Requests & Roadmap Signals
No explicit user‑requested features were filed today. However, the following newly opened and merged PRs give strong signals about upcoming capabilities:

- **OpenCode compatibility** ([#3122](https://github.com/nanocoai/nanoclaw/pull/3122)) – adds `main` compatibility, custom‑endpoint transport, and memory parity with OpenCode. Likely to land in next release.
- **NCC utility skill** ([#2971](https://github.com/nanocoai/nanoclaw/pull/2971)) – a CLI tool for host operational and health checks, requested via skill contribution. Still open, but actively updated.
- **Template context prepend** ([#3090](https://github.com/nanocoai/nanoclaw/pull/3090)) – ensures all top‑level context Markdown is prepended correctly; a core‑team fix that improves agent reliability.

Based on activity, the **next minor release** will likely include: native Matrix E2EE, Telegram thread support, OpenCode integration, the NCC utility skill, and a batch of container‑lifecycle fixes.

## 7. User Feedback Summary
Direct user feedback is minimal, but the issues and PR descriptions reveal several real pain points:

- **“Duplicate container spawning wastes resources and duplicates processing”** – reported in #2466, and independently observed in the root‑cause analysis of PR #3119 (one agent group reaching 3 concurrent containers).
- **“Typing indicator disappears mid‑tool‑call”** – fixed by #3120, indicating frustration with silent responses during long operations.
- **“Reaction delivery errors are too noisy”** – addressed by #3121, changing to best‑effort delivery.

Overall, users seem to value **reliability and resource efficiency**, and the team is responding with targeted hardening.

## 8. Backlog Watch
The following items have remained open for an extended period without maintainer response or progress:

- **[#2346 – fix(formatter): treat unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/pull/2346)**  
  Open since **2026-05-08** (77 days). This small PR prevents silent message drops when a user types an unrecognized slash command. Despite being a one‑line fix, it has not been reviewed or merged. Maintainer attention is recommended to close this long‑standing usability bug.

No other issues or PRs are notably stalled. The project’s overall maintenance responsiveness appears healthy.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-24

## 1. Today’s Overview

IronClaw remains in an intense stabilization and rebranding phase, with **50 PRs** and **31 issues** updated in the last 24 hours. The team merged **18 PRs** (including critical fixes for WebChat disconnect bugs, extension lifecycle improvements, and the retirement of legacy source trees) while **32 open PRs** continue to refine the Reborn runtime, configuration contracts, and testing infrastructure. Community and internal QA activity is high, driven by the **v1-launch-checklist** series of issues — nine open items surfaced by staging deployments that block a production release. No new releases were published today, indicating the project is still heating toward a stable milestone.

## 2. Releases

**None.** The most recent release candidate remains `ironclaw 1.0.0-rc.1` (referenced in Issue #6575). The automated release PR (#5598) is still open and waiting for breaking changes in `ironclaw_common` and `ironclaw_skills` to be finalized.

## 3. Project Progress

The following major work was merged or closed in the last 24 hours:

- **Extension lifecycle overhaul** — PR #6520 (closed) collapsed extension readiness into three manifest-derived states (`uninstalled`, `setup_needed`, `active`), separated tenant admin configuration from user membership, and made channel delivery generic. This was a high-risk, XL-sized change that triggered several follow‑up fixes.
- **Playwright suite reconciliation** — PR #6603 (closed) reconciled three shards to the new #6520 wire contracts and fixed two product‑side defects.
- **Live‑QA fixes** — PR #6602 (closed) fixed a `422 invalid_value` error in operator extension‑configuration by expecting a sequence instead of a map. PR #6606 (closed) mapped setup‑source names (`team_id:channel` → `C...`) to declared admin‑group handles.
- **WebChat rate‑limit and reconnection fix** — PR #6592 (closed) resolved the stuck “Disconnected” badge by fixing both a backend rate‑limit budget error and a navigation‑race SSE thrash in the frontend.
- **Legacy source tree removal** — PR #6594 (closed) deleted `tools-src/` and `channels-src/` and updated CI, README, and registry references.
- **Filesystem store renaming** — PR #6598 (open, large) renames concrete `Filesystem*Store` types to plain names and renames colliding traits to `*StorePort`.
- **Rebranding effort** — PR #6556 (open, XL) makes IronClaw the default product identity in CLI and WebUI. PR #6559 (open, XL) makes `IRONCLAW_*` env vars canonical with fallback to `IRONCLAW_REBORN_*`.
- **Operator reset script** — PR #6601 (closed) added `scripts/reset-extension-state.sh` to preserve admin config while removing user‑level extension state.
- **Canary verification** — PR #6582 (closed) caused `/benchmark` to start working again after fixing cross‑repo access policy.

## 4. Community Hot Topics

The most commented issue today is:

- **#6389** (11 comments) — *Phase 4: collapse build_local_runtime + build_production_shaped into one build_runtime(cfg)*. This architecture simplification was closed after wide discussion; it reduces duplication in the composition factory.
- **#6274** (5 comments) — *Finish DeploymentConfig as the main composition config*. Closed after resolving remaining gaps in §4.4/§5.6/§5.11.
- **#6524** (3 comments) — *Epic: Hermetic capability and journey testing platform*. This open epic reflects the team’s desire for deterministic coverage across all capabilities — a recurring theme in QA gaps.

No PRs had comment counts listed, but the most active PRs in terms of updates include #6607 (automations fix), #3997 (signing registration stack, 1184 commits behind main), and #6556 (rebranding).

**Underlying needs:** The community (largely project maintainers and QA) is pushing for **deterministic test coverage**, **configuration ergonomics** (DeploymentConfig and env vars), and **stable webhook delivery** (Telegram/Slack). The high comment count on composition refactoring hints at ongoing tension between legacy patterns and the new Reborn architecture.

## 5. Bugs & Stability

Several bugs were reported and many already have fix PRs in flight:

| Severity | Issue | Summary | Fix PR |
|----------|-------|---------|--------|
| **Critical** | #6548 (closed) | Preview auth wall blocks Telegram/Slack webhook delivery on staging | Not yet |
| **High** | #6581 (open) | 429 Too Many Requests on SSE channel causes stuck “Disconnected” | #6592 (merged) |
| **High** | #6605 (open) | Telegram inbound silent dead after extension reinstall (missing `telegram_webhook_secret`) | Not yet |
| **High** | #6544 (closed) | No UI/CLI to persist `IRONCLAW_REBORN_SLACK_PERSONAL_OAUTH_REDIRECT_URI` — Slack auth 503 | Closed as unsolved? |
| **Medium** | #6590 (open) | `serve` fails on Windows due to workspace root overlap with default skill root | No fix PR |
| **Medium** | #6575 (open) | `systemd` service error right after `ironclaw onboard` on Ubuntu | No fix PR |
| **Medium** | #6534 (open) | Google OAuth config can’t be applied in hosted deployments | No fix PR |
| **Low** | #6541 (open) | WebUI constantly shows “Reconnecting” banner (cosmetic) | Not yet |

The **most impactful bug** fixed today was the WebChat disconnect lockout (#6581 via #6592). The **Telegram reinstall bug** (#6605) and **auth‑wall blocking webhooks** (#6548) remain open and blocker for production.

## 6. Feature Requests & Roadmap Signals

The following open issues indicate strong product direction signals:

- **Epic: Admin‑Managed Agents as UserId Subjects** (#6578) — Tenants need non‑human subjects for automations and integrations without weakening user isolation. Likely to land in next release (P1).
- **Epic: Reliable Skill Discovery, Routing, and Activation** (#6565) — Fixes model‑directed skill selection; suggests a structured activation pipeline. High risk, P1.
- **Heartbeat MVP** (#6569, #6570, #6571) — Three‑part stack for durable heartbeat scheduling, delivery, and suppression. Already has defined contracts and owner (italic‑jinxin).
- **Rebranding: Remove “Reborn” from user‑facing surfaces** (#6550, #6551, #6552) — Rename crates, env vars, CLI, WebUI. PRs #6556 and #6559 are open and large; likely to land soon after v1‑launch.
- **E2E test migration** (#6560, #6561, #6562) — Retire legacy Python E2E and move to IronClaw‑native harness. Indicates investment in long‑term test reliability.

**Prediction for next version:** At least two of the “v1-launch-checklist” issues (#6521, #6522, #6544, #6550, etc.) plus the heartbeat MVP and the skill discovery epic will make it into the next release, alongside the rebranding PRs.

## 7. User Feedback Summary

Real user pain points visible in today’s data:

- **Slack and Telegram integration setup is confusing and error‑prone.** Issues #6544 (redirect URI), #6522 (no Telegram setup instructions), #6534 (Google OAuth not persistable), #6605 (Telegram silent after reinstall) — all from staging QA by `sergeiest` and `matiasbenary`.
- **WebChat disconnection anxiety.** Users see “Reconnecting” constantly (#6541) and sometimes get stuck disconnected (#6581). The fix merged today should alleviate this.
- **CLI not available on hosted staging.** #6521 and #6591 report that `ironclaw` command is missing on `agent-stg.near.ai`, forcing operators to use the UI.
- **Windows users blocked.** #6590 reports a basic `serve` failure on Windows — a cross‑platform regression.
- **SSE rate‑limiting under normal usage.** Users with multiple tabs saw 429 errors (fixed by #6592).

Overall, satisfaction seems low for staging deployments, but the team is reacting quickly with targeted fixes. The lack of a release means users cannot benefit from fixes without running from `main`.

## 8. Backlog Watch

Several important items have been open for an extended period without maintainer action:

- **Issue #4548** (opened 2026-06-08) — *Chat completion request serializes duplicate top‑level model field when tools are included (DeepSeek 400)*. **2 comments, 0 reactions.** This is 46 days old and affects DeepSeek provider — a key third‑party model. No PR linked. Needs attention.
- **PR #3997** (opened 2026-05-24) — *feat(signing): register NEAR/WC providers + flip production to durable composition*. This XL PR is a stack of 13 PRs for attested signing. It was force‑pushed yesterday but still open after 2 months. It blocks production‑ready signing.
- **PR #5598** (opened 2026-07-03) — *chore: release*. This automated release PR has been open for 21 days, blocked by breaking changes in `ironclaw_common` and `ironclaw_skills`. Until merged, no official release is published.
- **Issue #6524** (opened 2026-07-22) — *Epic: Hermetic capability testing*. While only 2 days old, it has no assigned owner yet and already has 3 comments. If not prioritized, it may stall.

**Recommendation:** Maintainers should assign or comment on #4548 and #3997 to unblock the DeepSeek integration and the signing feature. The release PR (#5598) should be merged as soon as the breaking changes are stable to give users a new version.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-07-24

## Today's Overview
The project shows low activity over the past 24 hours, with 3 open issues (all stale, last updated on July 23) and 3 pull requests updated. No new releases were published today. Two PRs were merged, including a release candidate for version 2026.7.20 and a UI polish for AI skins. The open issue tracker continues to host unresolved high-severity bugs and feature requests that have not seen maintainer response for over three months. Community engagement is minimal, with no comments or reactions on today’s items beyond single comments on each stale issue.

## Releases
*No new releases as of 2026-07-24.* The most recent tagged release appears to be the one referenced in merged PR #2379 (Release/2026.7.20), which may have been published on July 20 but is not listed as a new release in today’s data.

## Project Progress
Two PRs were closed/merged today:
- **[#2379 – Release/2026.7.20](https://github.com/netease-youdao/LobsterAI/pull/2379)** (merged) – Covers multiple areas (renderer, build, docs, main, openclaw, cowork, artifacts, Windows platform). This likely bundles features and fixes for a scheduled release.
- **[#2378 – feat(skin): polish AI skin appearance behavior](https://github.com/netease-youdao/LobsterAI/pull/2378)** (merged) – Enhances the AI skin system: aligns artifact tab and task-search surfaces, improves saved-skin ordering (newest first), makes standard themes and AI skins mutually exclusive with exact theme binding per skin, and simplifies the skin settings UI.

No open PRs were merged. The only remaining open PR is the stale dependency bump (#1277).

## Community Hot Topics
All tracked issues and PRs have at most **1 comment and 0 reactions**, indicating low community discussion. The most notable items by potential impact:

- **[#1263 – Duplicate scheduled tasks with “API rate limit reached”](https://github.com/netease-youdao/LobsterAI/issues/1263)** – User reports that scheduled tasks appear twice in the UI, both showing the same rate-limit error. Suggests a possible race condition or UI sync bug.
- **[#1265 – Multi-agent IM bot and model binding](https://github.com/netease-youdao/LobsterAI/issues/1265)** – A feature request to allow different agents to be tied to different IM bots and models, enabling role-specialised multi-agent teams.
- **[#1273 – sql.js (WASM) memory access out of bounds crash](https://github.com/netease-youdao/LobsterAI/issues/1273)** – Reports that high-frequency writes cause WASM memory corruption, leading to unrecoverable crashes and risks of permanent database file damage. This is the most critical open issue.

## Bugs & Stability

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#1273 – sql.js WASM crash & database corruption](https://github.com/netease-youdao/LobsterAI/issues/1273) | **Critical** – Unrecoverable crash, potential data loss under high load (cowork sessions, dense message flows). Non-atomic `save()` with `fs.writeFileSync` can corrupt database on write interruption. | No open fix PR |
| [#1263 – Duplicate scheduled tasks with rate-limit error](https://github.com/netease-youdao/LobsterAI/issues/1263) | **Medium** – UI shows duplicate identical tasks; API rate limit reached indicates possible excessive requests or caching issue. User confirms only one session exists. | No fix PR |

Both bugs remain open and have not received maintainer responses in months. The WASM crash (#1273) poses a serious risk for production workflows.

## Feature Requests & Roadmap Signals
- **[#1265 – Per-agent IM bot and model assignment](https://github.com/netease-youdao/LobsterAI/issues/1265)** – This request aligns with a growing need for multi-agent orchestration. The rationale is strong: different agents (e.g., a dispatcher, a PPT generator) require different underlying models for optimal performance. Given that the merged PR #2378 improved the AI skin system, the next minor release might include foundational work for agent-level configuration, though no explicit roadmap commitment exists.
- **No other new feature requests surfaced today.** The stale issues dominate.

## User Feedback Summary
- **Pain point: API rate limiting** – Issue #1263 shows a user frustrated by API limits appearing repeatedly in scheduled tasks, hindering automation.
- **Pain point: Stability under load** – Issue #1273 describes a crash that forces application exit or freeze, with risk of database file corruption. The user provided detailed reproduction steps and code analysis, indicating a genuine production blocker.
- **Desired capability: Multi-agent flexibility** – Issue #1265 articulates a clear use case: teams of agents with distinct roles and underlying models. This suggests advanced users are pushing LobsterAI toward complex multi-agent workflows.
- **No positive feedback** was captured; overall satisfaction cannot be assessed from this data set.

## Backlog Watch
The following long-unanswered items need maintainer attention:
- **[#1263](https://github.com/netease-youdao/LobsterAI/issues/1263)** – Open since April 2, 2026 (stale); related to scheduled tasks and rate limiting.
- **[#1265](https://github.com/netease-youdao/LobsterAI/issues/1265)** – Open since April 2, 2026 (stale); feature request for per-agent model binding.
- **[#1273](https://github.com/netease-youdao/LobsterAI/issues/1273)** – Open since April 2, 2026 (stale); critical database crash bug. No maintainer response or linked fix.
- **[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** – Open since April 2, 2026 (stale); dependency bump PR (electron 40→43) by Dependabot, awaiting review.

These four items represent a backlog of unresolved technical debt and user-facing issues that may affect adoption and trust if left unaddressed.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-24

## Today's Overview
The project saw a burst of integration and stability work, with **five Pull Requests merged** and **two new releases** published in the last 24 hours. Issue activity was light (2 items updated), but both items concern bugs — one still open and one closed today. The merged PRs address Slack security, web UI date formatting, context injection, and dependency updates, indicating a focused push toward hardening production deployments. Overall project health is strong, with maintainers actively resolving issues and shipping fixes.

## Releases
Two new versions were cut on 2026-07-23: **20260723.02** and **20260723.03**. The provided data does not include changelogs or migration notes. Operators are advised to review the [releases page](https://github.com/moltis-org/moltis/releases) for details before upgrading.

## Project Progress
All five PRs updated in the last 24 hours were closed (merged):

- **[PR #1124](https://github.com/moltis-org/moltis/pull/1124)** — Adds an optional `chat.context_command` that runs before each chat turn and injects stdout into the prompt context. This allows deployments to automatically provide dynamic runtime context without manual pasting.
- **[PR #1161](https://github.com/moltis-org/moltis/pull/1161)** — Dependency bump: Astro from 7.0.9 to 7.1.3 in the `/docs` directory (via dependabot).
- **[PR #1162](https://github.com/moltis-org/moltis/pull/1162)** — Fixes the web UI session list to display dates for older sessions (showing “yesterday”, weekday, or calendar dates with year) instead of empty times, addressing [Issue #1108](https://github.com/moltis-org/moltis/issues/1108).
- **[PR #1164](https://github.com/moltis-org/moltis/pull/1164)** — Moves Slack API base URL validation into the shared `channels` crate and introduces an operator‑controlled `MOLTIS_SLACK_API_BASE_URL_ALLOWLIST` environment variable to allow internal Slack proxy hosts.
- **[PR #1163](https://github.com/moltis-org/moltis/pull/1163)** — Fixes empty‑allowlist bypasses in Slack DMs/channels, Microsoft Teams, Signal, and Matrix DMs when the allowlist is empty (deny‑by‑default); adds OTP self‑approval for non‑allowlisted Slack DM users.

## Community Hot Topics
No issues or PRs attracted significant discussion (comments or reactions) in the last 24 hours. The most notable open item remains:

- **[Issue #1095](https://github.com/moltis-org/moltis/issues/1095)** — “Podman is not working via Moltis” (open since June 3). It has one comment from the author but no maintainer response yet.

## Bugs & Stability
Two bugs were reported in the last 24 hours (one still open, one fixed):

| Severity | Issue | Status | Fix PR |
|----------|-------|--------|--------|
| **High** | **[#1095](https://github.com/moltis-org/moltis/issues/1095)** – Podman runtime broken. | **Open** | None yet. |
| **Low** | **[#1108](https://github.com/moltis-org/moltis/issues/1108)** – Past‑day sessions show times but not dates in web UI. | **Closed** | **[#1162](https://github.com/moltis-org/moltis/pull/1162)** (merged today) |

No new crashes or regressions were reported.

## Feature Requests & Roadmap Signals
The merged PRs point toward two clear upcoming features:

- **Dynamic runtime context** ([#1124](https://github.com/moltis-org/moltis/pull/1124)): The ability to run a command before each chat turn and append its output to the prompt. This is likely to ship in the next release (already merged) and will be valuable for deployments needing real‑time environment awareness (e.g., file system state, metrics).
- **Slack security hardening** ([#1163](https://github.com/moltis-org/moltis/pull/1163), [#1164](https://github.com/moltis-org/moltis/pull/1164)): Both PRs were merged today, so the next release will include strict allowlist handling and OTP‑based self‑approval for Slack DMs. These changes close potential bypass vulnerabilities.

No explicit feature requests were raised in the last 24 hours.

## User Feedback Summary
- **Pain point**: Podman support is currently broken ([#1095](https://github.com/moltis-org/moltis/issues/1095)). The author reported it over six weeks ago, and the issue remains open without a fix or maintainer reply. This may affect users relying on Podman as a container runtime.
- **Satisfaction**: The quick resolution of the web UI date display bug ([#1108](https://github.com/moltis-org/moltis/issues/1108)) via [#1162](https://github.com/moltis-org/moltis/pull/1162) indicates the team is responsive to UI/UX concerns.

## Backlog Watch
**Important open issue requiring maintainer attention**:

- **[Issue #1095](https://github.com/moltis-org/moltis/issues/1095) – Podman not working via Moltis**  
  Opened 2026-06-03, last updated 2026-07-23 (by author). One comment from the reporter, no maintainer response. This is a functional block for Podman users and has been unanswered for nearly two months. Acknowledgment or a workaround would reduce community frustration.

No other issues or PRs have been left unanswered for an extended period.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-24

## 1. Today's Overview
Project activity remains very high with **38 issues** and **50 pull requests** updated in the last 24 hours, along with one new pre-release (v2.0.1-beta.2). The community continues to report performance regressions and stability bugs in the v2.0.x line, but the maintainers are responding with targeted fixes—23 PRs were merged or closed today. The release pipeline and desktop build orchestration have been unified, and several major feature branches (scroll compaction, third-party agent backends, unified browser SDK) are under active review. Overall, the project is in a rapid iteration phase with strong community engagement, though several core regressions still demand attention.

## 2. Releases
**v2.0.1-beta.2** was released today. Key changes:
- **feat(ci):** Unified release orchestrator gating web builds on desktop build completion.
- **fix(runtime):** Rotate text message on new reasoning block to improve display continuity.

No explicit breaking changes or migration notes were included in the release notes. However, users migrating from v1.x should be aware of the known ~2s fixed overhead issue (see Bugs section) that may affect upgrade decisions.

## 3. Project Progress (Merged/Closed PRs Today)
21 PRs were merged or closed. Notable ones:

- **#6351** – `fix(memory): guide failed memory edits` — Adds recovery prompts for MEMORY.md writing failures.
- **#6225** – `fix(desktop): gracefully shut down backend sidecar before exit` — Prevents force-kill on Desktop quit.
- **#6390** – `fix(governance): bridge tool_guard detection rules into governance policy Phase 1` — Tightens security policy enforcement.
- **#6393** – `perf(console): stabilize chat options memo and reduce SSE re-parsing` — Improves console rendering performance.
- **#6368** – `fix(governance): honor audit_level=none before persisting events` — Prevents unnecessary SQLite writes when auditing is off.
- **#6268** – `feat(providers): add AIOnly as a built-in model provider` — New provider with 190+ models.
- **#6219** – `fix(desktop): force-kill shutdown` — Resolved in #6225.
- **#6294** – `fix(skill market): installed skill not visible until page refresh` — Likely resolved in this batch.
- **#6379** – `[bug] official plugins blocked by security policy` — Addressed via governance bridge PR.
- **#6366** – `fix(console): coverage timeout in AgentLoopCard Gate test` — Testing infrastructure fix.

These fixes address memory edit reliability, desktop shutdown, governance policy gaps, and console performance.

## 4. Community Hot Topics
Most active issues (by comment count):

- **#6307** – *[Performance] v2.0 introduces ~2s fixed overhead per simple conversational reply vs v1.x* (6 comments).  
  Users are experiencing a consistent latency increase unrelated to model performance. It is the most upvoted issue and is a key regression.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/6307)

- **#6344** – *Feature：为Docker部署增加Web端热更新* (3 comments).  
  Docker users request a one-click hot-update button to avoid container rebuilds and tool environment loss.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/6344)

- **#6342** – *[Question]: ReMe 配置 embedding 模型之后，怎么确保已经生效？* (3 comments).  
  Users need verification that their embedding configuration is actually working, as no vector data files are observed.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/6342)

- **#6363** – *[Bug] tool_call arguments polluted with markdown fences / XML tags break all tool execution* (3 comments).  
  Models wrapping tool calls in markdown or XML cause JSONDecodeError, breaking tool execution entirely.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/6363)

- **#6316** – *[Feature]: Allow agent-type cron jobs to optionally specify a model* (3 comments).  
  Users want per-cron model selection independent of the agent's default.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/6316)

Underlying needs: Stability at scale (Docker, cron), clearer feedback for new features (ReMe), and model interoperability (tool call format handling).

## 5. Bugs & Stability
| Bug | Severity | Fix PR Exists? |
|-----|----------|----------------|
| **#6307** – ~2s overhead per reply in v2.0 | Critical | Not yet |
| **#6363** – Tool call arguments polluted by markdown/XML (all tool execution fails) | Critical | Not yet |
| **#6407** – ReAct Agent context mixes tool_result with role:assistant causing API 400 errors | High | Not yet |
| **#6405** – MCP tool "not found" after upgrade to 2.0 | High | Not yet |
| **#6401** – Cron jobs overwrite user session history when `share_session: true` | High | Not yet |
| **#6376** – `loop` feature crashes the main process (v2.0.0.post3/4) | High | Not yet |
| **#6379** – Official plugins blocked by governance policy (e.g., GPT Image 2 Tool) | Medium | Fixed via #6390 |
| **#6386** – Tool calling repeatedly (model returns same tool call) | Medium | Not yet |
| **#6406** – Windows `execute_shell_command` collapses multiline PowerShell | Medium | Fixed via #6412 |
| **#6362** – MiniMax-M3 model cannot recognize images | Medium | Not yet |
| **#6239** – Windows PATH concatenation drops semicolon | Low | Not yet |

Several bugs have associated PRs submitted today: #6412 (Windows multiline), #6410 (Gemini null schema), #6409 (local model tool call JSON), #6395 (spawn_subagent args), #6402 (usage persistence). The governance policy block (#6379) was addressed in #6390.

## 6. Feature Requests & Roadmap Signals
Notable user-requested features today:

- **#6392** – Agent-level token statistics per conversation and overall.
- **#6414** – Ability to rename custom provider names after creation.
- **#6413** – UI simplification: replace “Full Mode” with standard settings button.
- **#6408** – `/undo` command to roll back and re-edit previous conversation turn.
- **#6403** – RobotFramework syntax highlighting in Coding Mode web IDE.
- **#6380** – Optimize update process for HDD/NAS users (currently ~1.5h).
- **#6377** – Expose agent capabilities as HTTP APIs with custom request/response formats.

Active feature PRs under review suggest the next minor release may include:
- **#6398/#6399** – Reranker support for ReMe memory search (back-end + UI).
- **#6397** – Extensible third-party agent backends (Codex, Qoder).
- **#6276** – Unified browser SDK supporting multiple backends.
- **#6323** – Staged compaction and durable scroll context management.
- **#5187** – Windows desktop GUI automation via UIA + Tauri Control Mode.
- **#6284** – QwenPaw Creator app (script + assets → storyboard → video).
- **#6387** – On-demand installation of built-in channel dependencies (reduces core footprint).

## 7. User Feedback Summary
Real pain points expressed today:

- **Performance:** Users are disappointed that v2.0 added ~2s of overhead per reply, making the upgrade feel like a regression. “Upgrading from v1.1.12.post2 to v2.0.0.post3 introduces approximately 2 seconds of fixed overhead” (#6307).
- **Docker maintenance:** “QwenPaw iteration is very fast – more than ten minor versions in July alone… every update destroys the container runtime layer, requiring reinstallation of tools” (#6344). Users on HDD report 1.5-hour updates (#6380).
- **Tool reliability:** Several reports of tools not working after upgrade – MCP tools “not found” (#6405), tools blocked by governance (#6379), tool calls repeated (#6386), and tool result format errors (#6407). This directly impacts user trust.
- **Feature parity:** Users want token tracking (#6392), undo support (#6408), and model-per-cron (#6316), indicating they expect more granular control similar to Cherry Studio or advanced chat clients.
- **UI confusion:** The “Full Mode” vs “Simple Mode” concept is counterintuitive: “just use the settings button… don't make it so complicated” (#6413).

Satisfaction signals: The new Creator app (#6284) and browser unification (#6276) are welcomed, and the rapid iteration shows the team is responsive.

## 8. Backlog Watch
Important items needing maintainer attention:

- **#2999** – *Repeated MCP client registration with list_tools() leads to task cancellation* (opened April 6). Still open with no resolution. Every chat request reconnects MCP servers.  
  [Link](https://github.com/agentscope-ai/QwenPaw/issues/2999)

- **#3015** – *MEMORY.md write failure causing repeated retries* (closed but underlying pattern may persist).  
  Similar issue in #6351 attempt to fix, but monitor for recurrence.

- **#5187** – *Windows desktop GUI automation* (large PR, open since June 14). This is a major feature but has seen no updates in the last 24h. Needs review or chunking.

- **#6239** – *Windows PATH concatenation drops semicolon* (low priority but affects npm global tools). No fix PR yet.

- **#6323** – *Scroll compaction* PR open and under review, but no maintainer comments yet. Given the performance issues in v2.0, this could help.

- **#6397** – *Third-party agent backends* PR is under review; important for extensibility. No comments from maintainers in last 24h.

- **#6276** – *Unified browser SDK* PR, also under review. Large surface area – needs careful security and cross-platform testing.

The project maintains a healthy pipeline, but the backlog shows that several critical issues (#2999, #6307, #6363) have not yet seen a concrete fix PR. Prioritizing these would improve user confidence in v2.0.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-07-24

## 1. Today's Overview
Project activity was low overall, with no new releases and no merged or closed pull requests. Two open issues and one open pull request were updated in the last 24 hours, all created yesterday by the same author. The most notable development is a critical bug report concerning subprocess security and a corresponding fix PR, indicating active but focused maintenance work. Community engagement remains minimal, as none of the items have comments or reactions. The repository appears to be in a steady state, with no visible feature velocity.

## 2. Releases
*No new releases today.*

## 3. Project Progress
No pull requests were merged or closed today. The single open PR (#645) is a proposed fix for the critical subprocess vulnerability described in issue #644, but it has not yet been reviewed or merged.

## 4. Community Hot Topics
With zero reactions and no comments on any issues or PRs, there are no community-discussed topics today. The only notable activity is the critical bug report (#644) and its accompanying fix PR (#645), which together represent the core focus of recent development.

- **Issue #644** – Bug report: subprocess environments not scrubbed, process trees not terminated on timeout.  
  [GitHub](https://github.com/qhkm/zeptoclaw/issues/644)
- **PR #645** – Fix: scrub subprocess secrets and reap timed-out process trees.  
  [GitHub](https://github.com/qhkm/zeptoclaw/pull/645)

## 5. Bugs & Stability
One critical bug was reported today, with a fix already available in an open PR.

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#644](https://github.com/qhkm/zeptoclaw/issues/644) | P1‑critical | Subprocesses inherit full ZeptoClaw environment, exposing credentials; timeouts do not terminate spawned process trees. | [#645](https://github.com/qhkm/zeptoclaw/pull/645) |

Additionally, issue [#646](https://github.com/qhkm/zeptoclaw/issues/646) (chore, P1‑critical) tracks CI failures caused by new Clippy warnings and vulnerable dependencies (*quick-xml 0.39.2*, *lopdf 0.40.0*). While not a runtime bug, these block CI and could delay future releases if unaddressed.

## 6. Feature Requests & Roadmap Signals
No user-requested features were observed today. The only signals come from the maintainer’s own issues, which focus on CI hygiene and safety improvements. These suggest the near-term roadmap will prioritize:
- **Safety & hardening** (subprocess environment scrubbing, timeout handling)
- **Dependency vulnerability remediation**
- **Toolchain compatibility**

## 7. User Feedback Summary
No user feedback (comments, reactions, or external mentions) was recorded today. The project appears to have low community engagement at this time.

## 8. Backlog Watch
No issues or PRs are currently languishing unanswered. All open items were created yesterday and are actively being worked on. The only potential concern is the lack of a merged CI fix for issue #646, but it is still very fresh.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-07-24

## Today's Overview
The ZeroClaw project continues at a high level of activity (50 issues and 50 PRs updated in the last 24 hours), but with a low merge cadence (only 1 PR merged/closed). Most of the open work is concentrated on security hardening, multi-agent interoperability, and channel stability fixes. The 43 open issues and 49 open PRs indicate a significant backlog of work-in-progress, with several high-severity bugs being actively addressed by contributors. No new releases were published today.

## Releases
No new releases today. The project is likely between milestone versions (v0.8.3 is the latest stable).

## Project Progress
**Merged/closed PRs:** Only 1 PR was merged or closed today (not among the top 20 by comment count). No detailed changelog is available for that single merge.

**Notable PR advances (still open):**
- [#9324 – A2A outbound client config, shared wire-model, tools](https://github.com/zeroclaw-labs/zeroclaw/pull/9324) – Phase 1 of A2A protocol support, adding four `a2a_*` tools and a default-closed `[a2a.client]` config block. This is a major step toward external agent interoperability.
- [#8966 – Emit model_context_window separately from max_context_tokens trim budget](https://github.com/zeroclaw-labs/zeroclaw/pull/8966) – Solves a provider compatibility issue where smaller models’ context windows were misrepresented.
- [#9201 – Harden shared budget iteration reservation](https://github.com/zeroclaw-labs/zeroclaw/pull/9201) – Fixes a potential `usize::MAX` wrap in the agent turn loop.
- [#9295 – Repair package publishing workflows](https://github.com/zeroclaw-labs/zeroclaw/pull/9295) – Fixes Scoop and Homebrew release automation.
- [#9251 – PostgreSQL as the first supported session backend](https://github.com/zeroclaw-labs/zeroclaw/pull/9251) – Adds a full Postgres-backed session store, replacing the earlier multi-backend approach.
- [#8838 – Idle-bound SSE streaming on one shared transport](https://github.com/zeroclaw-labs/zeroclaw/pull/8838) – Consolidates SSE parsers for OpenAI, Anthropic, and compatible providers.

Several other PRs addressing config, channel, and security fixes remain in review or awaiting author action.

## Community Hot Topics
The most active discussions this week cluster around security, multi-agent routing, and channel reliability:

1. **[#3566 – A2A protocol interoperability tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)**  
   Comments: 9, Reactions: 7  
   This long-running tracker (since March) is the coordination hub for native Agent2Agent protocol support. The PR #9324 now provides a concrete implementation – a strong sign the community’s top interoperability request is finally landing.

2. **[#9127 – RFC: Abstract a `KeySource` trait for master-key material](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)**  
   Comments: 7, Reactions: 0  
   A design RFC proposing to classify master-key sources (file, env, TPM, etc.) to unify ZeroClaw’s credential encryption. This reflects growing demand for flexible secret management across deployment forms.

3. **[#2767 – Multi-Agent Routing (closed, 7 comments, 9 reactions)](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)**  
   Closed today, having collected strong community support. The feature allows multiple isolated agents and channel accounts in one gateway – a foundational piece for enterprise deployments.

4. **[#6378 – Discord bot respond only in specific channels (closed, 8 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)**  
   A requested config option for channel-scoped Discord responses, now implemented.

5. **[#4721 – Log to stderr instead of stdout (closed, 5 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/4721)**  
   A long-standing UX fix – CLI tools like `config schema` now produce clean output.

## Bugs & Stability
Today’s bug reports include several **critical (S0/S1) issues**, all with active fix PRs:

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#9188 – Telegram long-poll advances offset before delivery](https://github.com/zeroclaw-labs/zeroclaw/issues/9188) | S0 (data loss) | Update offset is committed before voice/attachment parsing; failures lose messages. | – |
| [#9187 – WeChat sync cursor persisted before enqueue](https://github.com/zeroclaw-labs/zeroclaw/issues/9187) | S0 (data loss) | Crash after sync cursor save but before message processing drops inbound messages. | – |
| [#9192 – shared_budget TOCTOU can wrap AtomicUsize; SopEngine unwrap panics](https://github.com/zeroclaw-labs/zeroclaw/issues/9192) | S1 (blocked) | Concurrent parent/subagent iterations can overdraw the budget; mutex unwrap panic. | [#9201](https://github.com/zeroclaw-labs/zeroclaw/pull/9201) |
| [#9191 – Cron agent jobs have no wall-clock timeout](https://github.com/zeroclaw-labs/zeroclaw/issues/9191) | S1 (blocked) | Hung agent runs hold job lock indefinitely until daemon restart. | [#9320](https://github.com/zeroclaw-labs/zeroclaw/pull/9320) |
| [#9204 – Landlock sandbox restricts the daemon itself](https://github.com/zeroclaw-labs/zeroclaw/issues/9204) | S1 (blocked) | Landlock policy prevents SQLite and other daemon-internal operations. | – |
| [#9284 – config flush can overwrite concurrent writes](https://github.com/zeroclaw-labs/zeroclaw/issues/9284) | S2 (degraded) | Race in `flush_config` – clone under read lock, then save without write guard. | – |
| [#9290 – Windows desktop installer fails with missing TaskDialogIndirect](https://github.com/zeroclaw-labs/zeroclaw/issues/9290) | S1 (blocked) | v0.8.3 installer crashes on launch. | – |
| [#9207 – web_fetch returns garbage for compressed responses](https://github.com/zeroclaw-labs/zeroclaw/issues/9207) | S1 (blocked) | gzip/brotli/deflate responses rendered as binary garbage. | – |

Other notable bugs:  
- [#9236 – Fresh Telegram aliases dropped after config reload](https://github.com/zeroclaw-labs/zeroclaw/issues/9236) (S1)  
- [#9285 – Nested set_prop masks invalid values as unknown properties](https://github.com/zeroclaw-labs/zeroclaw/issues/9285) (S3) – fix PR [#9310](https://github.com/zeroclaw-labs/zeroclaw/pull/9310)  
- [#9297 – save_dirty fails on map keys containing dots](https://github.com/zeroclaw-labs/zeroclaw/issues/9297) – fix PR [#9297](https://github.com/zeroclaw-labs/zeroclaw/pull/9297)  
- [#9202 – `zeroclaw desktop` command uses dead download URL, doesn't detect AppImage](https://github.com/zeroclaw-labs/zeroclaw/issues/9202) (S3) – fix PR [#9291](https://github.com/zeroclaw-labs/zeroclaw/pull/9291)  
- [#8999 – ZeroCode streamed user turns look like log/API payloads to small local models](https://github.com/zeroclaw-labs/zeroclaw/issues/8999) (S2)

## Feature Requests & Roadmap Signals
The following feature requests are active and likely candidates for upcoming milestones:

- **[#3566 – A2A protocol interoperability](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** – With PR #9324 now open, this is the clearest signal that v0.9.0 will include outbound A2A support.
- **[#9127 – KeySource trait for master-key material](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)** – This RFC, if accepted, would unify credential encryption backends and likely land in a security-focused release.
- **[#3767 – Require TOTP for cross-channel approval of critical tools](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)** – A highly requested security enhancement for multi-channel deployments.
- **[#4760 – Schema-validated tool calls for memory consolidation](https://github.com/zeroclaw-labs/zeroclaw/issues/4760)** – Would replace fragile JSON parsing with typed tool calls; important for reliable memory.
- **[#3672 – Workspace file and memory change history](https://github.com/zeroclaw-labs/zeroclaw/issues/3672)** – Tracking file/memory changes for audit and rollback, requested by advanced agent authors.
- **[#9228 – Eval results dashboard and trend tracking](https://github.com/zeroclaw-labs/zeroclaw/issues/9228)** – Deferred from #7065; a monitoring surface for regression tests.
- **[#8997 – Warn when peer_groups channel ref points at non-existent alias](https://github.com/zeroclaw-labs/zeroclaw/issues/8997)** – Config validation improvement to prevent silent authorization failures.
- **[#3696 – Configure external commands for message lifecycle hooks](https://github.com/zeroclaw-labs/zeroclaw/issues/3696)** – Shell hooks for memory integration and automation.

## User Feedback Summary
User feedback this week highlights several pain points:

- **Stability on Windows**: The desktop installer crash (#9290) and the missing PowerShell support (PR #9182) indicate that Windows users face significant friction. The PR adding PowerShell as native shell is a welcome fix, but the installer crash blocks new users.
- **Data loss risks**: The Telegram and WeChat issues (#9188, #9187) show that message delivery is not resilient to transient failures. Users depend on these channels for critical workflows.
- **Configuration confusion**: Nested `set_prop` masking errors (#9285), dot-separated map keys (#9297), and Telegram alias drops (#9236) create a frustrating on-boarding and administration experience.
- **Secure sandbox friction**: The Landlock sandbox locking the daemon (#9204) undermines the security model and blocks users who rely on sandboxing.
- **Positive signals**: The community is actively contributing – many PRs have author names like IftekharUddin, JordanTheJet, Nillth, indicating a healthy contributor base. The A2A PR (#9324) and Postgres backend (#9251) are ambitious, well-received additions.

## Backlog Watch
Several issues and PRs have remained open for extended periods without visible maintainer action:

- **[#3566 – A2A protocol tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** – Created March 15, now 4+ months old. While PR #9324 has appeared today, the tracker itself has been pending for many releases.
- **[#2767 – Multi-Agent Routing (closed today)](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)** – Was open since March 4, finally closed but only after a long wait. The gap between feature request and closure can be a concern.
- **[#7432 – v0.9.0 auth, security, gateway tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)** – Open since June 9, with only 2 comments. This milestone tracker seems under-discussed given the volume of related work.
- **PRs with `needs-author-action` label** (at least four in the top 20): #9201, #8966, #9182, #8838, #8746, #9251, #8741. These PRs have been open for weeks and lack author responses to reviews. If maintainers cannot get timely updates, these improvements risk stalling.
- **PR #8838 (Idle-bound SSE streaming)** – Open since July 8, marked `needs-author-action`. This fix affects three major providers and is critical for reliability; its long idle period is worrying.

Maintainer attention is especially needed on the backlog of PRs awaiting author updates and on the data-loss channel bugs (#9188, #9187) which have no fix PRs yet.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*