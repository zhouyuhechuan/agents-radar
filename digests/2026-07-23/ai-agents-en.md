# OpenClaw Ecosystem Digest 2026-07-23

> Issues: 441 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-23 02:04 UTC

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

# OpenClaw Project Digest — 2026-07-23

## 1. Today's Overview

OpenClaw remains in a period of intense development activity. Over the last 24 hours, **441 issues** and **500 pull requests** were updated, with 205 PRs merged or closed. No new release was published today. The project shows a healthy but strained state: a large number of regressions and P0/P1 bugs are being actively triaged, while significant feature requests (cross‑platform desktop apps, security hardening, localization) continue to gather community attention. The “ClawSweeper” bot is heavily involved in labeling and routing, indicating a mature triage process.

## 2. Releases

**No new releases** today. The latest available version remains `2026.7.2` (as mentioned in issue #110504).

## 3. Project Progress

Today **205 PRs were merged or closed**. Notable closed PRs from the top updated set include:

- [#112836 [CLOSED] – fix(ui): keep user footer controls in reading order](https://github.com/openclaw/openclaw/pull/112836) — improves accessibility and keyboard navigation.
- [#112821 [OPEN] – feat(scripts): add watch-pr-ci CI watcher](https://github.com/openclaw/openclaw/pull/112821) — a new CI reliability script (still open, but actively refined).
- Several long‑standing issues were also closed today, e.g.:
  - [#85103 (model fallback chain not triggered on quota exhaustion)](https://github.com/openclaw/openclaw/issues/85103) — closed after fix.
  - [#77802 (doctor --fix atomic validation failure)](https://github.com/openclaw/openclaw/issues/77802) — closed.
  - [#98674 (mac app install icon unclickable)](https://github.com/openclaw/openclaw/issues/98674) — closed with fix.

Progress is visible across multiple areas: bound‑reading fixes (to prevent hangs/OOM), localization infrastructure (PRs #112784, #112801), and gateway stability improvements (e.g., model catalog coherence across reloads #112331).

## 4. Community Hot Topics

The most active issues today, ranked by comment count and reactions:

- **[#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** — 115 comments, 80 👍  
  A top wish: native desktop apps for Linux and Windows (already have macOS, iOS, Android). The strong voting signals high demand for cross‑platform parity.

- **[#85333 – `openclaw doctor --fix` 4-5x slower (55s → 229s+)](https://github.com/openclaw/openclaw/issues/85333)** — 17 comments, a performance regression caused by a session snapshot path traversal bottleneck. Users are frustrated because it directly impacts daily maintenance.

- **[#13583 – Pre-response enforcement hooks (hard gates)](https://github.com/openclaw/openclaw/issues/13583)** — 16 comments, 2 👍  
  A security/correctness feature request to mechanically prevent agents from skipping mandatory tool calls. Underlying need: trust in agent behavior for regulated workflows (finance, security ops).

- **[#91009 – Codex PreToolUse hook spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)** — 15 comments, 2 👍  
  A stability issue where the Codex integration causes massive CPU spikes and RPC stalls, affecting production deployments.

- **[#10659 – Masked Secrets (prevent agent from seeing raw API keys)](https://github.com/openclaw/openclaw/issues/10659)** — 15 comments, 4 👍  
  Strong community interest in preventing credential leakage, especially from prompt injection.

The common theme: users are pushing OpenClaw toward **enterprise‑grade reliability**, **security**, and **cross‑platform availability**.

## 5. Bugs & Stability

Today’s bug landscape shows several regressions and critical issues:

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **P0** | [#108435 – Gateway fails to start after update to 2026.7.1](https://github.com/openclaw/openclaw/issues/108435) | Gateway does not start on systemd/Ollama/manual launch. | No linked PR yet. |
| **P0** | [#98674 – Mac app install icon unclickable](https://github.com/openclaw/openclaw/issues/98674) | `.dmg` not scaled, can’t click “install”. | Closed (#98674 was resolved). |
| **P1** | [#108580 – cron tool schema incompatible with llama.cpp grammar‑constrained tool calling](https://github.com/openclaw/openclaw/issues/108580) | Regression in 2026.7.1; every chat request fails. | Linked PR open (#108580). |
| **P1** | [#92043 – 180s compaction timeout fails identically every turn](https://github.com/openclaw/openclaw/issues/92043) | No partial‑progress reuse; legitimate long compactions never complete. | No linked PR. |
| **P1** | [#91009 – Codex hooks CPU‑bound spawns stalls gateway](https://github.com/openclaw/openclaw/issues/91009) | High CPU, RPC hangs. | No linked PR. |
| **P1** | [#90840 – Subagent run completion delivered as raw output to chat user](https://github.com/openclaw/openclaw/issues/90840) | Regression – child agent raw output leaks to user. | No linked PR. |
| **P1** | [#99811 – Gateway memory growth from repeated file read errors](https://github.com/openclaw/openclaw/issues/87314) | 60MB/day memory leak due to unbounded error logging. | No linked PR. |

Many of these P1 issues carry the `clawsweeper:needs-maintainer-review` label, indicating the team is still investigating.

## 6. Feature Requests & Roadmap Signals

The most requested enhancements today point to three themes:

- **Security & Governance**  
  - [#13583 – Pre-response enforcement hooks (hard gates)](https://github.com/openclaw/openclaw/issues/13583)  
  - [#10659 – Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)  
  - [#9912 – `maxTurns`/`maxToolCalls` limit](https://github.com/openclaw/openclaw/issues/9912)

- **Cross‑Platform & UX**  
  - [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) (oldest active issue, 115 comments)  
  - [#38568 – Inject context window % into system prompt runtime](https://github.com/openclaw/openclaw/issues/38568)

- **Workflow Integration**  
  - [#10142 – `session:end` internal hook event](https://github.com/openclaw/openclaw/issues/10142) – for Temporal‑like orchestration.

Given the volume of community interest and the P1/P2 labels, the next release (possibly `2026.7.3`) is likely to include at least one security hardening feature (masked secrets or enforcement hooks) and a fix for the gateway startup regression (#108435).

## 7. User Feedback Summary

Real user pain points expressed today:

- **Performance**: “`doctor --fix` went from 55s to 229s – this is a blocker in production” (#85333).
- **Reliability**: “Gateway does not start after update” (#108435); “subagent output leaks to chat” (#90840); “Mac app can’t be installed” (#98674).
- **Missing Features**: “No Linux/Windows app” (#75); “Can’t see API keys but agent can – leak risk” (#10659).
- **Friction in Workflows**: “Soft tool‑call rules are not enough – we need hard enforcement” (#13583); “Memory system cannot delete stale memories” (#95606).
- **Satisfaction**: Users are generally engaged and constructive, with detailed bug reports and votes for features. The high number of closed issues today (149) indicates that the maintainer team is responsive.

## 8. Backlog Watch

Several important issues and PRs have been open for months and still lack maintainer review or a fix PR:

| Item | Created | Last Updated | Status |
|------|---------|--------------|--------|
| [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | 2026-07-22 | Needs product decision & maintainer review |
| [#85333 – Performance regression in doctor --fix](https://github.com/openclaw/openclaw/issues/85333) | 2026-05-22 | 2026-07-22 | Needs maintainer review & live repro |
| [#10659 – Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | 2026-07-22 | Needs security review & product decision |
| [#13583 – Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) | 2026-02-10 | 2026-07-22 | Needs security review & product decision |
| [#38568 – Context window % injection](https://github.com/openclaw/openclaw/issues/38568) | 2026-03-07 | 2026-07-22 | Needs product decision |
| [#9912 – maxTurns/maxToolCalls config](https://github.com/openclaw/openclaw/issues/9912) | 2026-02-05 | 2026-07-22 | Needs product decision |
| [#112000 – Refactor prompt context labels](https://github.com/openclaw/openclaw/pull/112000) | 2026-07-21 | 2026-07-23 | Waiting on author (merge risk flags) |
| [#107765 – Standard hosting profiles](https://github.com/openclaw/openclaw/pull/107765) | 2026-07-14 | 2026-07-23 | Waiting on author (blocked by #104018) |

Most of these are tagged `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-product-decision`, indicating they are known but not prioritized. The oldest (#75) has been open for over six months, suggesting a strategic decision or resource constraint.

---

## Cross-Ecosystem Comparison

# AI Agent Open-Source Ecosystem: Cross-Project Comparison Report
**Date: 2026-07-23**

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a period of **intense maturation**, with all major projects converging on enterprise-grade requirements—security hardening, observability, cross-platform support, and agent orchestration—while still innovating rapidly on features. The landscape is characterized by a **reference implementation (OpenClaw)** that drives the core protocol and agent model, surrounded by **specialized forks (Hermes, IronClaw, CoPaw, NanoBot)** that optimize for different deployment scenarios (dedicated desktop, enterprise compliance, channel-first, lightweight). Community activity remains high across the board, but **stability and regression management** have emerged as the dominant concern, with several projects shipping fixes faster than they can close bugs. The fork dynamics suggest a healthy but fragmented ecosystem where differentiation is increasingly about **operational maturity** (testing, CI, documentation) rather than raw feature count.

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release | Health Score | Trend |
|---------|-------------|-----------|---------|--------------|-------|
| **OpenClaw** | 441 (updated) | 500 (updated), 205 merged | None (v2026.7.2 latest) | ⚠️ **Strained but active** | High activity, many regressions |
| **NanoBot** | 6 (4 open) | 63 (updated), 40 merged | None | ✅ **Healthy, fast-moving** | Sustained feature completion |
| **Hermes Agent** | 50 (46 open) | 50 (10 merged) | None | ⚠️ **High velocity, growing backlog** | Active but issue debt rising |
| **IronClaw** | 50 (updated) | 50 (updated), 21 merged | None (v1 launch imminent) | ⚠️ **Intense pre-release hardening** | QA bug-bash mode |
| **CoPaw** | 31 (6 closed) | 50 (15 merged) | **v2.0.0.post4** | ⚠️ **Rapid iteration, some stability concerns** | New patch, many v2 bugs |
| **ZeroClaw** | 50 (10 closed) | 50 (0 merged) | None | ✅ **Stable, feature-rich** | RFC-heavy, quality focus |
| **PicoClaw** | 4 (4 open) | 5 (1 merged) | None (v0.2.9) | ⚠️ **Moderate, critical bug unaddressed** | Low activity, Matrix bug |
| **LobsterAI** | 1 (closed) | 5 (merged) | None | ✅ **Stable, maintenance** | Low activity, bug fixes |
| **NanoClaw** | 1 (open) | 3 (0 merged) | None | ⚠️ **Stagnant** | PRs lingering, no merges |
| **Moltis** | 0 | 1 (open) | None | ✅ **Quiet, stable** | Minimal activity |
| **NullClaw** | 1 (closed) | 1 (merged) | None | ✅ **Responsive, low volume** | Two bugs fixed quickly |
| **TinyClaw** | 0 | 0 | None | ✅ **Inactive** | No activity |
| **ZeptoClaw** | 0 | 0 | None | ✅ **Inactive** | No activity |

**Health Score Key:** ✅ Stable/Healthy | ⚠️ Concerns exist | ❌ Critical issues

## 3. OpenClaw's Position

**Advantages over peers:**
- **Largest community and contributor base** — 441 issues and 500 PRs updated in a single day dwarfs every other project. No competitor approaches this velocity.
- **Most mature triage infrastructure** — The `ClawSweeper` bot-driven labeling and routing is unique in the ecosystem; no other project has automated issue management at this scale.
- **Defacto protocol/agent model reference** — Other projects (NanoBot, Hermes) explicitly fork or build on OpenClaw's conceptual architecture; it sets the standard for tool-use semantics, session management, and model fallback chains.

**Technical approach differences:**
- OpenClaw is **modular and protocol-oriented** — its `Gateway`, `Clawdbot`, `Codex` components are designed as swappable microservices, whereas most peers (Hermes, IronClaw) have more monolithic codebases.
- **Cross-platform ambitions** — The community strongly demands Linux/Windows desktop apps (Issue #75, 115 comments), but OpenClaw lags on delivery compared to Hermes, which already ships a desktop app for macOS.
- **Enterprise security features are still aspirational** — Masked Secrets (#10659) and Pre-response Enforcement Hooks (#13583) are in demand but not implemented, while IronClaw already ships admin-managed security policies and ZeroClaw has OIDC auth in progress.

**Community size comparison:**
| Metric | OpenClaw | Next-largest (Hermes / ZeroClaw) |
|--------|----------|-----------------------------------|
| Issues updated/day | 441 | ~50 |
| PRs updated/day | 500 | ~50 |
| Active contributors | Dozens | ~10-15 |
| Reactions on top issues | 80 (Issue #75) | 9 (Hermes #4335) |

OpenClaw is clearly **the dominant project by community volume**, but size introduces complexity: the ratio of open issues to fix PRs is worse than smaller, more focused projects like NanoBot or NullClaw.

## 4. Shared Technical Focus Areas

Several requirements are emerging **independently across multiple projects**, indicating genuine industry needs:

| Focus Area | Projects Affected | Specific Needs |
|------------|------------------|----------------|
| **Security & Governance** | OpenClaw, Hermes, IronClaw, ZeroClaw, CoPaw | - Masked/pre-credential secrets (OpenClaw #10659, Hermes #12651)<br>- Hard enforcement gates for tool calls (OpenClaw #13583, IronClaw #5459)<br>- OIDC/OAuth provider support (ZeroClaw #7141, IronClaw #6531)<br>- Audit logging / admin policies (CoPaw #6368, IronClaw #6527) |
| **Cross-Platform & Desktop UX** | OpenClaw, Hermes, PicoClaw, CoPaw | - Native Linux/Windows desktop apps (OpenClaw #75, Hermes #66875)<br>- PWA/mobile support (NanoBot #4494, Hermes #39248)<br>- Consistent session UI across platforms (Hermes #4335) |
| **Agent Orchestration & Multi-Agent** | NanoBot, IronClaw, ZeroClaw, OpenClaw | - Multi-agent collaboration protocols (NanoBot #5000, ZeroClaw #7218)<br>- Subagent context isolation (OpenClaw #90840, IronClaw #6284)<br>- Cross-session context sharing (Hermes #4335) |
| **Observability & Instrumentation** | ZeroClaw, IronClaw, OpenClaw | - OTel trace correlation (ZeroClaw #6641)<br>- Turn-level lifecycle oracles (IronClaw #6535)<br>- Heartbeat tracking for daemon nodes (ZeroClaw #6391) |
| **Channel Parity & Expansion** | PicoClaw, NanoClaw, Hermes, ZeroClaw | - Matrix reconnection logic (PicoClaw #3203)<br>- Rich message rendering in Telegram (NanoClaw #2877)<br>- DingTalk image support (PicoClaw #3283)<br>- IRC long message handling (PicoClaw #3287)<br>- Multi-bot Telegram config (NanoBot #5033) |
| **Performance & Reliability** | All projects | - OOM crash guards (LobsterAI #2375, OpenClaw #91009)<br>- Compaction timeout fixes (OpenClaw #92043)<br>- Doctor performance regression (OpenClaw #85333)<br>- Idle compaction CPU reduction (NanoBot #5036) |

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes | IronClaw | NanoBot | CoPaw | ZeroClaw |
|-----------|----------|--------|----------|---------|-------|----------|
| **Primary target user** | Developer building custom agents | Desktop power user / enterprise | Enterprise / regulated workflows | Multi-channel operator | API-first / commercial deployment | Hobbyist / homelab / extensibility |
| **Feature emphasis** | Protocol & model flexibility | Desktop app + session UX | Security + orchestration | Channel breadth (Telegram, Slack, Feishu) | API monetization + LangChain compatibility | Community RFCs + plugin ecosystem |
| **Technical architecture** | Microservice (Gateway, Clawdbot, Codex) | Monolithic + Desktop shell | Modular with ProductSurface routing | Lightweight, Python-heavy | API-wrapper, aligned with Aliyun/GLM | Plugin-driven, language-agnostic |
| **Release maturity** | Stable v2026.7.x, but high regression rate | Pre-v1, rapid iteration | Pre-v1, QA hardening | Stable, frequent point releases | v2.x with stability issues | Pre-v0.9, feature-rich but early |
| **Community engagement style** | Large, noisy, mature triage system | Growing, active contributors | QA-focused, bug-bash heavy | Fast maintainer response, low barrier | Chinese-language heavy, first-time contributors | Long RFC discussions, slow merges |
| **Key competitive advantage** | Ecosystem size, protocol leadership | Desktop UX maturity | Enterprise compliance from day one | Channel parity (multi-platform) | Commercial API integration (China) | Extensibility (everything is a plugin) |

## 6. Community Momentum & Maturity

**Tier 1 — High Velocity (rapidly iterating, high churn)**
- **IronClaw** — Pre-release hardening is intense: 50 issues + 50 PRs daily, 21 PRs merged. The QA bug-bash suggests a v1 release is days away. This project has the highest momentum in the ecosystem.
- **CoPaw** — Released v2.0.0.post4 today while simultaneously discovering new v2 regressions. Rapid iteration but **quality concerns** — multiple users reported process crashes and performance regressions.
- **OpenClaw** — Extremely high raw activity (441 issues/day) but **strained by its own scale**. Regression fixes are landing daily, but the backlog of P1 bugs (gateway startup failure, memory leaks) signals that velocity may be outpacing quality.
- **Hermes** — Healthy 10 PRs merged/day, but **46 open issues vs 4 closed** indicates a growing gap between bug discovery and resolution. Desktop session switching breakage (#66875) is a core UX regression.
- **NanoBot** — Best **merge-to-open ratio** in the ecosystem (40 merged out of 63 PRs). Fast, responsive maintainers. The project is in a sustained feature-completion phase.

**Tier 2 — Stable Mature (steady state, lower churn)**
- **ZeroClaw** — RFC-driven development with 10 issues closed today. Features are well-considered but move slowly. Open PRs (50) are often blocked on author action.
- **LobsterAI** — Low activity (5 merged PRs) but all were meaningful bug fixes. Stable maintenance mode.
- **NullClaw** — Minimal activity (2 items) but both were critical bug fixes done within 24 hours. Excellent response time for a small project.

**Tier 3 — Low Activity / Stagnating**
- **PicoClaw** — 1 PR merged (docs revert), but a **critical Matrix bug (#3203)** has been ignored for 21 days. Project may be under-resourced.
- **NanoClaw** — 3 open PRs, **none merged in weeks**. Telegram rich rendering PR (#2877) has been open 25 days with no maintainer feedback. Risk of contributor attrition.
- **Moltis, TinyClaw, ZeptoClaw** — Near-zero activity. Moltis has a single UX polish PR; the others appear **effectively dormant**.

## 7. Trend Signals

From community feedback and technical decisions across all projects, the following industry trends emerge:

1. **Security is moving left** — Multiple projects (OpenClaw, Hermes, IronClaw, ZeroClaw) are adding pre-execution enforcement hooks, credential masking, and OIDC auth. The era of "just trust the agent" is ending; **hard gates and audit trails** are becoming baseline expectations for production deployments.

2. **Cross-platform parity is non-negotiable** — OpenClaw's most-upvoted issue (#75, 80 👍) demands Linux/Windows desktop apps. Hermes' desktop session switching bug is a P2 frustration. The ecosystem is converging on the expectation that AI agents must work identically on any device. **Projects that ignore desktop or mobile risk marginalization.**

3. **Agent-to-agent communication is the next frontier** — NanoBot (#5000), ZeroClaw (#7218, A2A discovery), and IronClaw (#6284, error recoverability) are all exploring multi-agent protocols. **The single-agent assistant model is giving way to agent swarms** with persistent identities, shared state, and negotiation capabilities.

4. **Observability is becoming a feature, not an afterthought** — ZeroClaw's OTel trace correlation, IronClaw's turn lifecycle oracles, and OpenClaw's CI watch scripts all signal that **operators need to observe, debug, and replay agent behavior**. This is driven by enterprise deployment requirements.

5. **"Doctor" tools and self-healing are expected defaults** — OpenClaw's `doctor --fix` performance regression (#85333) generated 17 frustrated comments. Users expect proactive maintenance commands to be fast and reliable. **Self-diagnosis is becoming a core product requirement.**

6. **Channel fragmentation is a burden** — IronClaw's Telegram pairing bugs, PicoClaw's Matrix reconnection failure, and multiple "channel parity" issues across projects indicate that **supporting N messaging platforms is increasingly costly**. Expect consolidation around 3-4 primary channels (Telegram, Discord, Slack, WhatsApp) in the next release cycle.

7. **Performance regressions overshadow new features** — CoPaw's v2.0 overhead (#6307) and OpenClaw's doctor slowdown (#85333) show that **users are more sensitive to regression than to new features**. Post-release quality assurance is the ecosystem

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-23

## 1. Today’s Overview

The past 24 hours saw intensive development activity: **63 pull requests** were updated (40 merged/closed, 23 open) alongside **6 issues** (4 open, 2 closed). No new releases were cut. The high merged‑PR count indicates a sustained push toward stability and feature completion — many bug‑fix PRs from multiple contributors landed, and several long‑pending enhancements (session‑scoped presets, WebUI performance, multi‑bot Telegram) were finalised. Community engagement remains strong, with one issue (#5000) sparking architectural discussion. Overall the project is in a healthy, fast‑moving state; maintainers are actively reviewing contributions and addressing regression claims.

## 2. Releases

*None in the observed window.*

## 3. Project Progress

40 pull requests were merged or closed. Notable advances include:

- **WebUI performance** (#5003) — replaced JSONL transcript reads with an indexed SQLite WAL read model, batching display writes off the event loop.  
- **Session‑scoped model presets** (#4866, closed) — presets are now per‑session; one immutable `LLMRuntime` per turn ensures consistent provider calls, prompt sizing, and compaction.  
- **Telegram multi‑bot support** (#5033, open) — backward‑compatible config for multiple bot instances, each with independent token validation and controls.  
- **xAI Grok OAuth + X Search** (#5035, open) — native OAuth 2.0 / PKCE sign‑in for Grok subscriptions with capability‑gated `x_search` tool.  
- **MCP presets** (#5047, open) — adds Parallel Search as an optional free MCP preset.  
- **Configurable idle compaction** (#5036, open) — allows users to reduce CPU usage on low‑power devices.  
- **Numerous channel‑specific fixes** — fenced markdown tables preserved in Slack (#5045) and Feishu (#5046); improved Feishu group ingest (#5009); DingTalk private‑chat gating (#4446).  
- **Background turn silence** (#4988, open) — keeps cron/local‑trigger turns from emitting an unwanted placeholder when the model returns empty.

## 4. Community Hot Topics

- **Issue #5000** — *Proposal: evolve subagent system toward multi‑agent collaboration*  
  [🔗](https://github.com/HKUDS/nanobot/issues/5000)  
  Most‑commented item (4 comments). The author argues the current subagent model is too “task‑delegation” oriented and lacks persistent identities, shared state, and real negotiation. This signals growing interest in agent‑to‑agent communication within NanoBot — likely a key roadmap discussion.

- **Issue #4934** (closed) — *Qwen models expose thinking content*  
  [🔗](https://github.com/HKUDS/nanobot/issues/4934)  
  Quickly resolved after two comments. Users appreciated the fast turnaround.

- **PR #5035** — *xAI Grok OAuth*  
  [🔗](https://github.com/HKUDS/nanobot/pull/5035)  
  Attracts attention as a new provider integration with OAuth flow — important for users seeking larger model capacity.

## 5. Bugs & Stability

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| #5041 — Dream batch starvation | Medium | Completed no‑op Dream runs don’t advance cursor → later history starved | None yet |
| #5040 — MCP tool schema `$ref` | High | Non‑`#/$defs/` `$ref` breaks strict providers (Kimi/Moonshot) | None yet |
| #5028 — Media path / workspace conflict | Low | Feishu‑uploaded files placed outside workspace scope → inaccessible | None yet |
| #5043 — Cron null `runHistory` | Medium | `null` entries in `jobs.json` raise TypeError, quarantine store | #5043 (open) |
| #5042 — Cron null schedule | Medium | Null `schedule` crashes entire cron store | #5042 (open) |
| #5044 — Pairing null approved channels | Medium | `"telegram": null` crashes `is_approved` | #5044 (open) |
| #4948 — WebUI loses visibility on late subagent | Medium | Subagent completion starts system turn without WebUI lifecycle | Closed, fix merged |

*Severity estimate: High = disables a provider or core feature; Medium = unexpected behaviour with workaround; Low = minor inconvenience.*

Maintainers are actively issuing fix PRs for the cron and channel‑specific crashes; #5040 and #5041 still lack a proposed fix.

## 6. Feature Requests & Roadmap Signals

- **Multi‑agent collaboration** (#5000) — the most substantiated feature request. Likely to influence subagent refactoring in the next 1–2 releases.
- **Configurable idle compaction scan interval** (#5036) — raised by a Raspberry Pi user; straightforward + already has a PR. High chance of merging soon.
- **xAI Grok with OAuth** (#5035) — completed PR; expect it in the next release.
- **Parallel Search MCP preset** (#5047) — low complexity, increases out‑of‑box value.
- **PWA support & mobile gestures** (#4494, from June) — still open, but with conflict labels; may need maintainer rebase.

The pattern suggests a shift toward **agent orchestration** (multi‑agent, session‑scoped state) and **channel/device accessibility** (PWA, Telegram multi‑bot, low‑power tuning).

## 7. User Feedback Summary

- **Pain point**: Media uploads via Feishu can become inaccessible when workspace restrictions are enabled (#5028). Users expected file access to work irrespective of workspace config.
- **Pain point**: Strict provider (Kimi/Moonshot) users are completely blocked by MCP tool schemas containing non‑standard `$ref`s (#5040). This affects anyone who enables MCP tools with those providers.
- **Satisfaction**: The quick closure of #4934 (Qwen thinking leak) and the community‑driven fix PRs for cron resilience (#5042–5044) show that maintainers respond quickly to clear‑cut bugs.
- **Use case**: A Raspberry Pi user described high idle CPU consumption and pushed for configurable compaction — this was explicitly addressed in #5036, indicating the project listens to edge‑case hardware constraints.

## 8. Backlog Watch

Items that have been open for an extended period and may require maintainer attention:

- **PR #2584** — *Feature/xiaozhi support* (created 2026‑03‑28, conflict‑labelled)  
  [🔗](https://github.com/HKUDS/nanobot/pull/2584)  
  Upstream voice gateway + ESP32 MCP tools. Nearly 4 months old; has unresolved conflicts. May need a rebase or decision on inclusion.

- **PR #4439** — *Add read‑only search_history tool* (created 2026‑06‑21, conflict‑labelled)  
  [🔗](https://github.com/HKUDS/nanobot/pull/4439)  
  Simple memory recall tool; conflicts with later memory changes. Unclear if maintainers consider it redundant.

- **PR #4689** — *OAuth status and expiry warnings* (created 2026‑07‑03, conflict‑labelled)  
  [🔗](https://github.com/HKUDS/nanobot/pull/4689)  
  UX improvement with provider‑level OAuth status. Conflicts may stem from the newer xAI OAuth PR (#5035) — possible merge conflict resolution needed.

- **PR #4494** — *PWA support* (created 2026‑06‑24)  
  [🔗](https://github.com/HKUDS/nanobot/pull/4494)  
  Still open despite user demand for mobile WebUI improvements. No recent activity; likely needs maintainer review.

These items do not block releases but could reduce contributor motivation if left stale. Maintainers may want to explicitly mark them as “on hold” or request rebases.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-23

## 1. Today's Overview

Project activity remains **very high**, with 50 issues and 50 pull requests updated in the last 24 hours. The open issue count is substantial (46 open vs. 4 closed), while PRs show a healthier balance (40 open, 10 merged/closed). No new releases were cut today. The community is driving multiple P2/P1 bug reports around session state management, desktop app reliability, and Telegram integration. Several long-standing bugs (e.g., session resurrection, Copilot credential rotation) now have fix PRs under review. The project’s health is strong but **strained by a growing backlog of open issues** — maintainers should prioritise triage and merging the cluster of `sweeper:risk-session-state` PRs.

## 2. Releases

**None** — no releases published today.

## 3. Project Progress (Merged/Closed PRs)

10 PRs were closed or merged today. Notable advances include:

- **[PR #69655](https://github.com/NousResearch/hermes-agent/pull/69655)** (feat billing) – Uniform out-of-credits UX across CLI, TUI, and Desktop.
- **[PR #69691](https://github.com/NousResearch/hermes-agent/pull/69691)** (feat desktop billing) – Polish of the billing page, auto-poll, responsive layout, and shared `Progress` primitive.
- **[PR #69725](https://github.com/NousResearch/hermes-agent/pull/69725)** (fix desktop) – Preserve active correction on warm resume, fixing a race that left stale live prompt state.
- **[PR #69740](https://github.com/NousResearch/hermes-agent/pull/69740)** (fix cron) – Clean up `HERMES_CRON_SESSION` env var after cron jobs finish to prevent leakage into interactive sessions.
- **[PR #17247](https://github.com/NousResearch/hermes-agent/pull/17247)** (feat provider-routing) – Support OpenRouter Zero Data Retention (ZDR) preference via `provider_routing.zdr`.
- **[PR #69694](https://github.com/NousResearch/hermes-agent/pull/69694)** (feat delegation) – Allow per-task model selection in `delegate_task`.

## 4. Community Hot Topics

These issues and PRs generated the most discussion this week.

- **[#4335 – Cross-platform session context sharing](https://github.com/NousResearch/hermes-agent/issues/4335)** (9 comments, 2 👍)  
  *Feature request*: Allow agent to share conversation context across platforms (CLI ↔ Telegram).  
  **Need**: Users want seamless multi-platform conversations without manually copying context.

- **[#66875 – Desktop session switching broken](https://github.com/NousResearch/hermes-agent/issues/66875)** (7 comments)  
  *Bug*: Latest session not activated after navigating to non-chat tabs and back.  
  **Need**: Core UX flow broken – high frustration.

- **[#62936 – Telegram upload timeout](https://github.com/NousResearch/hermes-agent/issues/62936)** (6 comments)  
  *Bug*: Files >15 MB always fail, env var `HERMES_TELEGRAM_HTTP_WRITE_TIMEOUT` has no effect.  
  **Need**: Media delivery parity with other platforms.

- **[#21341 – NixOS module path misconfiguration](https://github.com/NousResearch/hermes-agent/issues/21341)** (5 comments)  
  *Bug*: `documents` option places files in wrong directories.  
  **Need**: Correct installation for Nix users.

- **[#45279 – npm shim shadowing on macOS](https://github.com/NousResearch/hermes-agent/issues/45279)** (4 comments)  
  *Bug*: Node/npm shims still overwrite Homebrew/nvm symlinks despite prior fix.  
  **Need**: Silent regression – developer friction.

- **[#62708 – Silent context overflow](https://github.com/NousResearch/hermes-agent/issues/62708)** (3 comments)  
  *Bug (P1)*: No warning when compression is blocked, context keeps growing until token limit.  
  **Need**: User visibility into agent state – one of the highest-severity open bugs.

## 5. Bugs & Stability

### Severity P1
- **[#62708 – Silent context overflow](https://github.com/NousResearch/hermes-agent/issues/62708)** – Context grows without warning when compression is blocked (cooldown/anti-thrash). No fix PR yet.

### Severity P2
- **[#66875 – Desktop session switching broken](https://github.com/NousResearch/hermes-agent/issues/66875)** – No fix PR; opened July 18, still unassigned.
- **[#62936 – Telegram upload timeout](https://github.com/NousResearch/hermes-agent/issues/62936)** – No fix PR; env var ignored for media.
- **[#21341 – NixOS wrong paths](https://github.com/NousResearch/hermes-agent/issues/21341)** – No fix PR; affects `SOUL.md` and personality files.
- **[#45279 – npm shim shadowing](https://github.com/NousResearch/hermes-agent/issues/45279)** – Regression from PR #38889; fix expected but not merged.
- **[#69551 – Desktop SSH remote mode broken with non-default profile](https://github.com/NousResearch/hermes-agent/issues/69551)** – Token path validation mismatch. Newly opened.
- **[#57775 – Windows `atomic_replace` drops writes on sharing violation](https://github.com/NousResearch/hermes-agent/issues/57775)** – Silent data loss.
- **[#65942 – Snapshot restore can leave newer data when state.db open](https://github.com/NousResearch/hermes-agent/issues/65942)** – Race condition in state persistence.
- **[#63222 – ACP model switch preserves stale `base_url`](https://github.com/NousResearch/hermes-agent/issues/63222)** – Requests routed to old endpoint.

### Fix PRs submitted today for existing bugs
- **[PR #69743](https://github.com/NousResearch/hermes-agent/pull/69743)** – Fix Windows gateway task handling (related #63743).
- **[PR #69733](https://github.com/NousResearch/hermes-agent/pull/69733)** – Forwards `require_parameters` and `data_collection` to cron agents.
- **[PR #69735](https://github.com/NousResearch/hermes-agent/pull/69735)** – Drops stale `api_content` sidecar when merging consecutive assistant turns.
- **[PR #69730](https://github.com/NousResearch/hermes-agent/pull/69730)** – Verify fire tokens against job profile for cron webhooks.

## 6. Feature Requests & Roadmap Signals

Top community-requested features that may appear in the next version:

- **[#4335 – Cross-platform session context sharing](https://github.com/NousResearch/hermes-agent/issues/4335)** – High interest (9 comments, 2 👍). Likely to advance after session state refactors.
- **[#66268 – Advertise delegation toolset isolation in capabilities](https://github.com/NousResearch/hermes-agent/issues/66268)** – Small API change, could ship quickly.
- **[#69726 – WhatsApp `channel_skill_bindings` support](https://github.com/NousResearch/hermes-agent/issues/69726)** – Parity with Discord/Slack, straightforward.
- **[#66393 – Gate browser tool with install hint in non-interactive sessions](https://github.com/NousResearch/hermes-agent/issues/66393)** – Improves user experience for headless deployments.
- **[#44845 – Durable ID-addressable clarify prompts](https://github.com/NousResearch/hermes-agent/issues/44845)** – Architectural change, may be deferred to v0.20.
- **[#68679 – OpenRouter policy-aware catalog and ZDR controls](https://github.com/NousResearch/hermes-agent/pull/68679)** – PR already open, likely to merge soon.

## 7. User Feedback Summary

**Pain points** voiced by the community:

- **Desktop UX regressions** – Sessions not switching, updates broken, animation static on Windows, queued images causing reconnect loops (`#66875`, `#39248`, `#47930`, `#69638`).
- **Telegram reliability** – Large media uploads fail silently, FIFO queue drops media (`#62936`, `#18539`).
- **Silent failures** – Context overflow without warning, snapshot restore races, ACP model switch misroutes (`#62708`, `#65942`, `#63222`).
- **Configuration headaches** – npm shims shadowing Homebrew, nix paths wrong, env sanitizer treats placeholders as real credentials (`#45279`, `#21341`, `#12651`).
- **Context awareness** – Agent fails to correlate session context across platforms or across turn boundaries (`#4335`, `#48027`).

**Satisfaction signals** – The billing UX PRs and OpenRouter ZDR PR received positive reactions. Community members are actively contributing fix PRs, indicating engagement.

## 8. Backlog Watch

Issues and PRs that have gone weeks without a maintainer response despite clear user impact:

| Issue | Created | Last Update | Severity | Gap |
|-------|---------|-------------|----------|-----|
| [#12651](https://github.com/NousResearch/hermes-agent/issues/12651) – `.env` sanitizer does not remove placeholders | 2026-04-19 | 2026-07-22 | P2 | 3 months |
| [#18539](https://github.com/NousResearch/hermes-agent/issues/18539) – FIFO chain drops MEDIA files | 2026-05-01 | 2026-07-22 | P2 | 2.5 months |
| [#21521](https://github.com/NousResearch/hermes-agent/issues/21521) – Unhandled `auth_type oauth_minimax` warning | 2026-05-07 | 2026-07-22 | P3 | 2.5 months |
| [#25837](https://github.com/NousResearch/hermes-agent/issues/25837) – Vision_analyze can brick session with oversized image | 2026-05-14 | 2026-07-22 | P2 | 2 months |
| [#39248](https://github.com/NousResearch/hermes-agent/issues/39248) – Desktop update process broken | 2026-06-04 | 2026-07-22 | P2 | 7 weeks |
| [#44845](https://github.com/NousResearch/hermes-agent/issues/44845) – Clarify prompts should be durable decisions | 2026-06-12 | 2026-07-23 | P3 | 6 weeks |
| [#47930](https://github.com/NousResearch/hermes-agent/issues/47930) – Windows Desktop arc-border animation static | 2026-06-17 | 2026-07-23 | P3 | 5 weeks |
| [#57775](https://github.com/NousResearch/hermes-agent/issues/57775) – Windows atomic_replace drops writes | 2026-07-03 | 2026-07-22 | P2 | 3 weeks |
| [#66183](https://github.com/NousResearch/hermes-agent/issues/66183) – memory_tool creates directories with 000 permissions on Docker | 2026-07-17 | 2026-07-22 | P2 | 5 days (no reply yet) |
| [#66393](https://github.com/NousResearch/hermes-agent/issues/66393) – Gate browser tool install hint | 2026-07-17 | 2026-07-22 | P3 | 5 days |

**PRs needing review**:
- [#62477](https://github.com/NousResearch/hermes-agent/pull/62477) – Fix session reset in self-heal path (P2, 12 days open)
- [#62689](https://github.com/NousResearch/hermes-agent/pull/62689) – Fix Copilot credential rotation (P2, 12 days open)
- [#62521](https://github.com/NousResearch/hermes-agent/pull/62521) – Fix `model.context_length` override leaking (P2, 12 days open)
- [#53743](https://github.com/NousResearch/hermes-agent/pull/53743) – Fix A2A slash command pass-through (P3, 26 days open)
- [#68679](https://github.com/NousResearch/hermes-agent/pull/68679) – OpenRouter policy-aware catalog (P3, 2 days open, needs decision)

**Action recommended**: The cluster of `sweeper:risk-session-state` PRs (#62477, #62689, #62521) should be reviewed and merged together to avoid conflicts. The long backlog on bugs like #12651, #18539, and #21521 suggests a need for a triage pass and possibly a maintenance release.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw Project Digest — 2026-07-23

### 1. Today’s Overview
The project saw moderate activity in the last 24 hours, with 4 issues and 5 pull requests updated. All 4 tracked issues remain open, and one PR (#3285) was merged – a documentation revert. No new releases were published. While several older enhancements and refactors linger in stale state, two new bug fixes (Go dependency update, DingTalk picture support) and one fresh feature request (IRC long message handling) indicate continued community engagement. However, a critical, unaddressed Matrix reconnection bug (#3203) remains the most pressing stability concern.

### 2. Releases
No new releases were published. The latest version remains **v0.2.9** (as referenced in issue #3203).

### 3. Project Progress
Only one pull request was merged today:
- **#3285** – `docs: remove picopaw` (a revert of PR #3096). This is a small documentation cleanup.

Additionally, two new open PRs were submitted:
- **#3286** – `fix: update Go and x/text for govulncheck` (dependency security fix)
- **#3283** – `fix(dingtalk): support picture/image message inbound` (new feature for DingTalk channel)

No further feature or refactoring PRs advanced to merge.

### 4. Community Hot Topics
The most active discussion remains **issue #3203** – *[BUG] Matrix sync loop has no reconnection logic — silent death after network/server disruption*  
- Author: weissfl  
- Comments: 5 | 👍: 2  
- [View Issue](https://github.com/sipeed/picoclaw/issues/3203)  

This bug has gathered significant attention because it causes a complete, silent failure of the Matrix channel with no automatic recovery, and the workaround (systemd restart) is ineffective. The underlying need is clear: **reliable long-polling reconnection in the Matrix bridge** – without this, Matrix users risk losing all agent interaction after any network hiccup.

Other issues with one comment each (e.g., #3258, #3257) generated less discussion, while the fresh request #3287 (IRC long messages) has no comments yet.

### 5. Bugs & Stability
Three bugs were active in the last 24 hours, ranked by severity:

| Issue | Summary | Severity | Fix PR Exists? |
|-------|---------|----------|----------------|
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix sync loop silent death – no reconnection after disruption | **Critical** – permanent channel loss, no auto-restart | ❌ No |
| [#3258](https://github.com/sipeed/picoclaw/issues/3258) | `before_tool` hook failure: decision field discarded, args misparsed | **High** – breaks hook functionality | ❌ No |
| [#3286](https://github.com/sipeed/picoclaw/pull/3286) | Go and `x/text` dependency updates for govulncheck | **Low** – proactive security fix | ✅ PR itself is the fix |

No crash or regression was reported today beyond these. The DingTalk PR #3283 addresses a missing feature rather than a crash.

### 6. Feature Requests & Roadmap Signals
Two feature requests were updated/created today:

- **#3257** – *Add stateless/no-history mode for gateway sessions* (stale)  
  _User pain: gateway mode always derives session key from channel, making stateless CLI-like usage impossible._  
  Likely to be considered if gateway adoption grows.

- **#3287** – *Better support long messages in IRC* (new)  
  _Goal: Treat split IRCv3 messages ( >512 bytes) as a single cohesive message._  
  A straightforward improvement that benefits IRC users; could ship in a minor release.

Two long-standing enhancement PRs remain open but stale:
- **#3163** – *feat(bedrock): leverage Converse prompt caching* (30 days old) – significant cost reduction for AWS Bedrock users.
- **#3222** – *refactor(deltachat): cleanup implementation, documentation -200LOC* (19 days old) – improves code health.

These may be candidates for the next minor version if maintainers resume review.

### 7. User Feedback Summary
Community sentiment reflects both satisfaction with the project’s extensibility (new channel support like DingTalk) and frustration with reliability gaps:

- **Pain points:**
  - Matrix channel silent death after network/server restart (#3203) – leads to unnoticed agent downtime.
  - `before_tool` hook deserialization bug (#3258) – blocks advanced tool customisation.
  - Inability to create stateless gateway sessions (#3257) – limits use of PicoClaw as a stateless API.
  - IRC users experience message splitting (#3287) – disrupts coherent communication.

- **Satisfaction:** 
  - Community actively contributes fixes (DingTalk image support, dependency updates) and documentation fixes.
  - No widespread complaints about core agent functionality.

### 8. Backlog Watch
Several important items risk being overlooked:

| Item | Type | Age (as of today) | Reason for Concern |
|------|------|-------------------|-------------------|
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) – Matrix reconnection | Bug (Critical) | 21 days | No PR or assignee; core channel broken for Matrix users. |
| [#3258](https://github.com/sipeed/picoclaw/issues/3258) – Hook deserialization | Bug (High) | 8 days | No maintainer response or fix. |
| [#3163](https://github.com/sipeed/picoclaw/pull/3163) – Bedrock prompt caching | Enhancement PR | 30 days | No reviewer activity; valuable for cost savings. |
| [#3222](https://github.com/sipeed/picoclaw/pull/3222) – DeltaChat refactor | Refactor PR | 19 days | No reviewer activity; reduces technical debt. |

These items should be prioritised to maintain project health and community trust. The Matrix reconnection bug in particular demands immediate attention, as it affects a major channel and has a clear, reproducible impact.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-23

---

## 1. Today's Overview

NanoClaw shows moderate activity with one new issue and three pull requests updated in the past 24 hours, though no merges or releases occurred. The project remains in a steady state of community contributions, with a mix of documentation clarification requests and feature skill proposals awaiting maintainer review. Activity is primarily driven by open PRs that have been lingering for weeks, indicating a bottleneck in merging or feedback. Despite low closed-item volume, the pipeline demonstrates ongoing community engagement in extending NanoClaw’s channel support and security documentation.

---

## 2. Releases

No new releases were published today. The project has no tagged version in the latest data window.

---

## 3. Project Progress

No pull requests were merged or closed in the last 24 hours. All three open PRs remained in their existing state:

- **#3070** – Fix WhatsApp sender identity divergence between Baileys and Cloud paths (opened 2026-07-16, updated 2026-07-22)  
  Aimed at resolving a user-facing inconsistency where the same phone number gets two different user IDs in the WhatsApp channel. This fix addresses a real deployment pain point for dual-path setups.

- **#3117** – New utility skill: `add-omarchy-statusbar` – a Waybar status indicator for NanoClaw (opened 2026-07-22)  
  A community contribution adding a system tray widget to display NanoClaw status, following the project's skill guidelines.

- **#2877** – Native Telegram rich rendering via Bot API 10.1 `sendRichMessage` (opened 2026-06-28, updated 2026-07-22)  
  A feature skill to leverage Telegram's latest rich message API, enhancing media and layout capabilities. This PR has been open for over three weeks.

No regression fixes or critical patches were closed today.

---

## 4. Community Hot Topics

All issues and PRs currently have zero comments and zero reactions, suggesting low conversational engagement. However, the following items are the most significant by content and time:

- **Issue #3118** – *SECURITY.md overclaims per-group credential isolation*  
  [nanocoai/nanoclaw Issue #3118](https://github.com/nanocoai/nanoclaw/issues/3118)  
  Opened 2026-07-22 by bradfeld. Raises a discrepancy between documented "per-group" credential isolation and actual OAuth behavior on self-hosted OneCLI gateways. The underlying need is for accurate security documentation to prevent misconfigured deployments. This issue may lead to either a documentation fix or a feature enhancement to enforce true per-group isolation.

- **PR #3070** – *Fix WhatsApp sender identity divergence*  
  [nanocoai/nanoclaw PR #3070](https://github.com/nanocoai/nanoclaw/pull/3070)  
  Addresses a bug affecting users who operate both Baileys (native) and Cloud (API) WhatsApp paths. The divergence in user ID assignment can break agent state continuity. No discussion yet, but the problem resonates with multi-path operators.

- **PR #2877** – *feat(telegram): native rich rendering via Bot API 10.1 sendRichMessage*  
  [nanocoai/nanoclaw PR #2877](https://github.com/nanocoai/nanoclaw/pull/2877)  
  A long-open feature request that would bring modern Telegram rich content support. The lack of updates may indicate maintainer capacity issues or unresolved design decisions.

---

## 5. Bugs & Stability

Only one issue with security implications was reported today:

- **#3118** (Severity: **Medium**) – Incorrect documentation stating per-group credential isolation for OAuth connections on self-hosted OneCLI.  
  While not a runtime crash, it poses a security misdirection risk for self-hosters who might assume agent identity boundaries that do not exist. No fix PR exists yet. The report suggests the documentation should be corrected, and potentially the feature itself may need implementation.

No crash, regression, or performance bug reports were filed today.

---

## 6. Feature Requests & Roadmap Signals

Two feature-oriented PRs are in the pipeline:

- **PR #3117** – *Waybar status indicator skill*  
  A utility skill, indicating demand for system-level integration (Linux desktop notifications). Likely to be merged as it follows guidelines and has low complexity.

- **PR #2877** – *Telegram rich rendering*  
  Has been open since June 28. If merged, it would be part of the next minor release. The delay suggests either maintainers are waiting for testing tools or the API support is blocked by Telegram Bot API version requirements.

No new feature requests in the issue tracker itself.

**Prediction**: Next minor release (if any) will likely include PR #3070 (WhatsApp fix) and PR #3117 (Waybar skill). PR #2877 may require additional maintainer feedback to progress.

---

## 7. User Feedback Summary

No explicit user satisfaction or dissatisfaction comments were recorded in the last 24 hours. The only user-generated content is a security documentation concern (issue #3118) from bradfeld, indicating a self-hosted deployment scenario and a need for accurate multi-tenant isolation. This reflects a real use case where administrators rely on documented guarantees to set up agent groups with separate credentials.

The imbalance between open PRs (3) and closed PRs (0) may imply contributor frustration, but without direct feedback it remains speculative.

---

## 8. Backlog Watch

Several pull requests have been open for extended periods without maintainer action:

| Item | Open Since | Days Open | Status | Notes |
|------|------------|-----------|--------|-------|
| **PR #2877** – Telegram rich rendering | 2026-06-28 | 25 | Needs review / tests | High-value feature; risk of contributor abandonment |
| **PR #3070** – WhatsApp identity fix | 2026-07-16 | 7 | Needs review | Bug fix; merge would improve stability |

Issue #3118 is only one day old and does not yet qualify as backlog.

**Action needed**: Maintainers should respond to PR #2877 with either a review request, blockers, or acceptance to keep the community motivated. PR #3070 is a targeted fix that could be merged with minimal risk.

---

*Generated from GitHub activity up to 2026-07-23 23:59 UTC.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-23

## 1. Today’s Overview
The project saw low but focused activity in the last 24 hours, with **one issue closed** and **one pull request merged**. Both items relate to the Discord gateway integration and were reported/fixed by the same contributor (Tetraslam). The closed issue describes a severe bug where the gateway becomes permanently deaf after processing a single `MESSAGE_CREATE` event. The merged PR addresses a separate crash caused by a stack overflow in the typing indicator thread. No new releases were published, and the overnight activity suggests the maintainers are responsive to stability-critical reports.

## 2. Releases
*None in the reporting period.*

## 3. Project Progress
One pull request was merged today:
- **PR #978** ([link](https://github.com/nullclaw/nullclaw/pull/978)) — *“discord: run typing thread on the heavy runtime stack”*  
  The typing‑indicator thread previously used a 512 KB auxiliary stack (`AUXILIARY_LOOP_STACK_SIZE`) but performed full HTTPS requests via `std.http.Client` → `std.crypto.tls`. TLS initialisation does large inline `memcpy` operations that overflow the small stack, aborting the process. This PR moves the thread to the heavy runtime stack, fixing the crash. (Closed/merged 2026-07-22)

No other feature advances or new functionality were introduced.

## 4. Community Hot Topics
Activity was limited to two items, both from the same user. Neither drew comments or reactions beyond the author and maintainer:
- **Issue #977** ([link](https://github.com/nullclaw/nullclaw/issues/977)) — *Discord gateway goes permanently deaf after exactly one MESSAGE_CREATE* (1 comment, 0 👍)  
- **PR #978** ([link](https://github.com/nullclaw/nullclaw/pull/978)) — *discord: run typing thread on the heavy runtime stack* (0 comments, 0 👍)

The low reaction count may reflect a small user base or that the bugs were quickly resolved before garnering wider attention. The underlying need is clear: reliable Discord gateway behaviour without silent failures or process crashes.

## 5. Bugs & Stability
Two stability issues were reported today:

- **HIGH SEVERITY — Issue #977** (Closed)  
  *Discord gateway permanently deaf after first MESSAGE_CREATE*  
  Every gateway connection handles exactly one inbound `MESSAGE_CREATE`, replies successfully, then silently discards all subsequent events. The bot stays online (heartbeats continue) but never dispatches another event until the process restarts. 100% reproducible.  
  → **Status**: Closed, but no associated fix PR was identified in the 24‑hour data. The fix may have been applied in a commit outside the reported PRs or resolved by a different change. Maintainers should confirm the root cause is eliminated and monitor for recurrence.

- **HIGH SEVERITY — PR #978** (Merged)  
  *Typing indicator thread stack overflow*  
  When a turn triggers Discord typing, the thread’s 512 KB stack overflows during TLS `memcpy`, aborting the whole process.  
  → **Status**: Fixed by merging PR #978. A clear improvement in process resilience.

Overall stability improved with the typing thread fix, though the gateway deafness issue (now closed) requires verification that the fix is durable.

## 6. Feature Requests & Roadmap Signals
No feature requests were observed in the reporting period. The project remains in a bug‑fixing phase as far as Discord integration is concerned.

## 7. User Feedback Summary
The only user providing feedback (Tetraslam) reported two concrete pain points:
- A silent, reproducible failure in Discord event dispatch after the first message.
- A crash during typing notification due to insufficient stack space.

Both issues were addressed within 24 hours (one closed, one merged), indicating a responsive maintenance cycle. User satisfaction is likely positive, as no open follow‑up discussions were left unattended.

## 8. Backlog Watch
No outstanding issues or pull requests require maintainer attention. The single open/active item count was zero at the time of the report, and the only updated issue/PR were both closed/merged within hours of creation. The backlog is effectively clear.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

```markdown
# IronClaw Project Digest – 2026-07-23

## 1. Today's Overview
The project remains at extremely high velocity, with **50 issues** and **50 pull requests** updated in the last 24 hours. No new releases were cut, but the bulk of activity targets the **v1 launch checklist** and **QA bug-bash** tracks, indicating the team is hardening Reborn for a forthcoming stable release. A large number of “Completed foundation” issues were closed retrospectively to preserve delivery history, while several critical staging bugs (e.g., Telegram pairing loops, Google OAuth config) surfaced from hosted‑staging QA sessions. Architectural work continues in parallel, with a growing focus on the `ProductSurface` routing abstraction and hermetic testing infrastructure.

## 2. Releases
**No new releases** were published in the last 24 hours. The most recent version remains the unreleased changes tracked by PR #5598 (chore: release), which would bump `ironclaw_common` to 0.5.0 (breaking) and `ironclaw_skills` to 0.4.0 (breaking). Operators should expect breaking changes in the next official release.

## 3. Project Progress
**Merged/closed PRs today (21 total)**, including several that advance critical foundations:

- **ProductSurface routing** – PR #6441 (merged) introduced the `ProductSurface` trait; PR #6444 refreshed the routing design docs. PR #6538 (open) routes OpenAI compat through the new interface.
- **Testing & CI** – PR #6535 (merged) added pure turn/run lifecycle oracles; PR #6537 (open) extends CI to run heavy test gates on release-fix branches. PR #6528, #6525, #6526 (open) add typed provider operations, isolated Emulate worlds, and provider capability inventory.
- **Identity & security** – PR #6527 (open) adds admin‑managed user security policies.
- **Extension lifecycle** – PR #6520 (open) makes extension readiness and channel delivery generic. PR #6531 (open) resolves OAuth config at runtime from WebUI settings, directly addressing the Google OAuth bug (#6534).
- **Container hosting** – PR #6533 (open) adds container‑supervised mode for hosted deployments (partial fix for #6534).

All “Completed foundation” issues (e.g., #6519, #6515, #6514) were closed to record that PRs later merged (e.g., #6411, #6246, #6116) had already delivered those capabilities; they represent roadmap consolidation, not new work.

## 4. Community Hot Topics
The most active discussions center on **error recoverability and lifecycle stability**:

- **#6284 (Error recoverability epic)** – 4 comments, 0 👍. Proposes a strict contract ensuring every mid‑run error is recoverable, with the model seeing both cause and necessary corrective action. This is a fundamental architectural goal for reliability.
- **#6105 (Extension/channel lifecycle state‑machine test + cron)** – 3 comments, 0 👍. Emerged from repeated regressions in Slack integration across four QA waves. The community and core team are demanding automated lifecycle testing (install → connect → … → uninstall) and canary lanes on cron.
- **#5459 (Configurable skills and tools)** – 2 comments, 0 👍. Smaller discussion about admin vs. user installation scoping for WASM tools and skills. Touches governance and tenant separation.
- **#3288 (Production/scoped capability lifecycle admin parity)** – 2 comments, 0 👍. Long‑running refactoring to unify extension, skill, MCP, and WASM lifecycle UX into typed services.

These threads signal that **stability and test automation** are the primary community concerns, especially around channel integrations.

## 5. Bugs & Stability
**Bugs reported today (priority ranking by severity):**

| Bug | Priority | Summary | Fix PR? |
|-----|----------|---------|---------|
| #6523 | **P0 (blocker)** | Agent creation fails when “testing flag” is set during onboarding. Blocks v1 launch. | None yet. |
| #6534 | **P1 (critical)** | Google OAuth config cannot be applied in hosted‑staging; the container‑appropriate restart path is missing. | Partial fix in #6533 (container‑supervised mode); full fix expected in #6531 (runtime OAuth config resolution). |
| #6475 | **P1 (critical)** | Telegram `/pair` command not recognized, trapping users in a pairing loop. | None yet. |
| #6478 | **P2 (high)** | Agent does not recognize connected Telegram, redirects to Slack authorization instead. | None yet. |
| #6474 | **P2 (high)** | Telegram delivery channel not configurable in Delivery Defaults page – only “Web app only” is available. | None yet. |
| #6522 | **P3 (medium)** | No instructions for setting up Telegram locally or on agent.near.ai. | None yet. |
| #6521 | P3 (closed) | `ironclaw` CLI missing from agent staging environment. | Already closed – presumably fixed. |

All bug‑bash items are tagged `v1-launch-checklist`. The Telegram issues (#6475, #6478, #6474) form a cluster that suggests the Telegram integration was shipped without sufficient UX testing for the pairing and routing flows.

## 6. Feature Requests & Roadmap Signals
- **Error‑recoverability endgame (#6284)** – If adopted, this would make IronClaw agents far more robust in production. Likely a v1.x goal.
- **Hermetic testing platform (#6524)** – A new epic proposing deterministic coverage for every capability and user journey. If the team commits, this could surface in the next minor release as part of QA automation.
- **Attested signing + Ledger hardware wallet support (#6532)** – A design/Phase A plan for secure blockchain transactions. This is a significant new feature; given the complexity, it may target a post‑v1 milestone (maybe v2.0).
- **Configurable skills and tools (#5459)** – Admin/private installation scoping. Already partially delivered via PR #6116; the remaining work (per‑user WASM installation) could land in the next release.

## 7. User Feedback Summary
Real pain points captured from this 24‑hour period:

- **Telegram integration is frustrating** – Users are trapped in pairing loops, the agent confuses Telegram with Slack, and the delivery defaults page doesn’t list Telegram. (Issues #6475, #6478, #6474)
- **Agent creation broken with testing flag** – A code path that should be optional for developers actually crashes the onboarding flow. (Issue #6523)
- **Google OAuth deployment gap** – Operators on hosted staging cannot apply OAuth config through the WebUI; configuration appears saved but is never consumed. The only workaround is CLI commands that may not be available. (Issue #6534)
- **Missing documentation** – No in‑product instructions for setting up Telegram; users are left guessing. (Issue #6522)

Satisfaction signals are absent from this data, but the sheer volume of bug reports from a single QA session suggests the product is in a pre‑release hardening phase where many rough edges are being actively filed.

## 8. Backlog Watch
Long‑standing issues that have not seen recent attention from maintainers:

- **#1330 (Tool schema: expose message routing/attachment semantics)** – Opened March 18, last updated July 22. Has 1 comment and is marked `on hold`. No recent activity suggests it’s deprioritised, but the problem (model confusion about message routing) remains live.
- **#2246 (Unify extension model: MCP tools as single‑tool extensions + provider dedup)** – Opened April 10, last updated July 22. 1 comment. Related to the ongoing `ProductSurface` refactoring; may become active again once routing is complete.
- **#1519 (Routine notifications lack context in user's chat thread)** – Opened March 21, last updated July 22. 1 comment. Tagged `scope: agent` and `enhancement`. With the Telegram delivery fixes, this may resurface as a quality‑of‑life request.
- **#3288 (Production/scoped capability lifecycle admin parity)** – Opened May 6, last updated July 22. 2 comments. A large refactoring epic that has been slowly advancing via sub‑issues; maintainers should update the community on its status.

None of these appear to be abandoned, but they lack recent maintainer comments or priority updates.
```

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-07-23

---

## 1. Today's Overview

The project saw moderate activity on July 22–23, with **5 pull requests merged/closed** and **1 issue closed** in the last 24 hours. No new releases were published. The majority of work focused on **stability improvements** (Windows installer hardening, out‑of‑memory crash prevention) and **UI/UX refinements** (cowork export modal layering). Two stale long‑standing PRs (Skills Management, Scheduled Task enhancements) were also closed today, indicating a cleanup of older contribution branches. Overall project health remains stable, with the team addressing both security‑related hardening and bug fixes.

---

## 2. Releases

*No new releases were made today.*  
The last known version remains unchanged. (No release data provided.)

---

## 3. Project Progress

**All 5 pull requests updated in the last 24 hours were closed/merged:**

- **[PR #2377]** `feat: windows update installer hardening` – Strengthens the Windows installer pipeline (areas: renderer, main, platform).  
  *Author: fisherdaddy* · [GitHub](https://github.com/netease-youdao/LobsterAI/pull/2377)

- **[PR #2376]** `fix(cowork): render export modal above sidebar` – Fixes a z‑order issue in the cowork module by mounting the export options modal via a body portal.  
  *Author: liuzhq1986* · [GitHub](https://github.com/netease-youdao/LobsterAI/pull/2376)

- **[PR #2375]** `fix(openclaw): guard against oversized transcript OOM crashes` – Prevents JavaScript heap‑out‑of‑memory crashes when loading very large transcripts; blocks oversized turns before gateway load, classifies OOM crashes, and ignores stale gateway client generations after a heap restart.  
  *Author: fisherdaddy* · [GitHub](https://github.com/netease-youdao/LobsterAI/pull/2375)

- **[PR #1346]** `Feat/skills management` – Stale PR (created Apr 2) referencing a skills management feature (based on PR #846); now closed.  
  *Author: leefinder* · [GitHub](https://github.com/netease-youdao/LobsterAI/pull/1346)

- **[PR #1347]** `feat(scheduledTask): add Cron custom scheduling, Agent selector, UX improvements` – Major enhancement to the scheduled task module: custom Cron expressions (visual builder + raw input), Agent/Model binding, form UX unification. Stale PR now closed.  
  *Author: swuzjb* · [GitHub](https://github.com/netease-youdao/LobsterAI/pull/1347)

---

## 4. Community Hot Topics

The only issue receiving recent attention is **#1348**, which was closed today after being marked as stale:

- **#1348** `定时任务名称重复没有校验` (Duplicate scheduled task name not validated)  
  *2 comments* · 😊 no reactions  
  *Created: 2026-04-02* · *Closed: 2026-07-22*  
  [Issue #1348](https://github.com/netease-youdao/LobsterAI/issues/1348)

The underlying need is a **validation function** to prevent users from creating two scheduled tasks with identical names. This is a typical usability gap that could lead to confusion in task management. The issue was closed without a visible fix PR – it may have been addressed upstream or deprioritized. No other issues or PRs received comments today.

---

## 5. Bugs & Stability

Two merged PRs directly addressed stability and crash issues:

| Bug/Crash | Severity | Fix PR | Status |
|-----------|----------|--------|--------|
| **Overseas transcript OOM crash** – Loading an oversized active transcript could exhaust the JS heap and cause a gateway crash; stale reconnections after OOM restart also caused zombie reconnects. | **High** | [#2375](https://github.com/netease-youdao/LobsterAI/pull/2375) – `fix(openclaw): guard against oversized transcript OOM crashes` | Merged |
| **Export modal layering issue** – Cowork export modal appeared behind sidebar elements due to stacking context. | Medium | [#2376](https://github.com/netease-youdao/LobsterAI/pull/2376) – `fix(cowork): render export modal above sidebar` | Merged |

No regressions or new bugs were reported today.

---

## 6. Feature Requests & Roadmap Signals

- **Skills Management** (PR #1346, now closed) – Although the PR was closed as stale, the feature idea (system for managing AI skills) remains in the repository’s history; it may be revisited or implemented in a future version.
- **Scheduled Task Custom Cron** (PR #1347, now closed) – The detailed enhancement (Cron expressions, Agent/Model binding, visual builder) is a strong signal that **advanced automation** is on the roadmap. The closing of the PR does not imply rejection – the code may have been merged into main (no details provided), or the feature was integrated via other means.
- **Windows installer hardening** (PR #2377) – Shows ongoing focus on **deployment security** on Windows.

Next version likely includes the OOM guard, modal fix, and installer hardening. Skills management and scheduled task features may appear if they were successfully merged earlier.

---

## 7. User Feedback Summary

- **Scheduled task name duplication** (#1348) – A clear pain point for users managing multiple cron jobs: lack of duplicate prevention leads to accidental overwrites or confusion.
- **Large transcript handling** – The OOM fix (#2375) indicates users are encountering crashes when working with very long meeting/gathering transcripts, a real‑world use case for collaboration tools.
- No explicit satisfaction or dissatisfaction data was recorded today; the closed issues and PRs suggest the team is responsive to stability concerns.

---

## 8. Backlog Watch

- **Issue #1348** (`定时任务名称重复没有校验`) – Now closed, but the lack of a visible fix may leave the validation gap unaddressed. Maintainers should confirm whether the duplicate name check was implemented elsewhere (e.g., in the scheduled task PR #1347).
- **Stale PRs #1346 & #1347** – Both were closed today after months of inactivity. If their features are still desired by the community, the maintainers should re‑open or create fresh issues to track progress.
- No other long‑unanswered issues or PRs were identified from the provided data.

---

*Digest generated from GitHub activity on 2026-07-23 (data covers last 24h ending 2026-07-22).*  
*All links reference the [netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI) repository.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-23

## 1. Today's Overview
Project activity was minimal over the past 24 hours. No new issues were reported or closed, and no releases were published. A single open pull request (#1162) was updated, continuing work on improving date labels for session history in the web UI. While no code was merged, the project appears to be in a stable maintenance phase with incremental improvements being refined.

## 2. Releases
No new releases. (No version tags or changelogs detected.)

## 3. Project Progress
**Merged/closed PRs today:** None.  
**Open PRs updated:**  
- [#1162 – fix(web): show dates for older sessions](https://github.com/moltis-org/moltis/pull/1162) (open, last updated 2026-07-22)  
  This PR introduces improved date formatting for the session history list:
  - Keeps localized `HH:MM` labels for sessions updated today.
  - Shows localized “yesterday” and weekday names for recent prior days.
  - Falls back to a calendar date (including year when needed) for older sessions.
  - Adds browser test coverage for all four date buckets.

No other feature or bug-fix PRs were advanced today.

## 4. Community Hot Topics
No issues or PRs received comments or reactions in the last 24 hours. The only active discussion point is PR #1162, which has no comments or upvotes. Community engagement remains low.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported. No fix-related issues were opened. The project currently has zero open/active issues, indicating that known stability problems are either already resolved or not being reported.

## 6. Feature Requests & Roadmap Signals
No feature requests were submitted. The only signal from the codebase is the ongoing work on date label formatting in the web UI (PR #1162), which suggests a focus on polishing user-facing UX for session history. This is likely to land in the next minor release. No major roadmap changes are visible.

## 7. User Feedback Summary
No user feedback (comments, reactions, or new issues) was recorded in the last 24 hours. The project appears to have a quiet user base with no reported pain points or satisfaction/dissatisfaction signals during this period.

## 8. Backlog Watch
- **No long-stale issues** – the issue tracker is empty (0 open issues).  
- **No long-open PRs requiring attention** – the only open PR (#1162) was updated yesterday and is actively being worked on by its author (shixi-li). No maintainer intervention is needed at this time.

**Overall health:** Low activity, stable state, no unresolved problems. The project is in a quiet phase with focused incremental improvement.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-23

## 1. Today's Overview
CoPaw saw elevated activity on 2026-07-23 with **31 issues updated** (6 closed) and **50 PRs updated** (15 merged/closed). A new patch release **v2.0.0.post4** shipped, focusing on agent reasoning optimization. The project remains in rapid iteration; however, several regression and stability reports for v2.0.0 were opened, indicating that the v2.0 line still needs hardening. Community engagement is high, with many first-time contributors submitting fixes and features.

---

## 2. Releases
**v2.0.0.post4** was released. Changes:

- Optimized agent reasoning to mitigate redundant thinking loops and duplicate tool invocations.

No breaking changes or migration notes were published. The release is a direct patch over v2.0.0.post3.

[Full Changelog](https://github.com/agentscope-ai/QwenPaw/compare/v2.0.0.post3...v2.0.0.post4)

---

## 3. Project Progress (Merged/Closed PRs Today)
15 PRs were merged or closed. Notable ones:

- **#6375** (fix): Token usage persistence now retries on transient write failures. *PR closed.*
- **#6359** (fix): Context injection role changed from `system` to `user` to fix API rejection on GLM/OpenAI. *PR merged.*
- **#6293** (feat): Added `qwen3.8-max-preview` to Aliyun Token Plan. *Under review, but likely merged soon.*
- Several first-time-contributor fixes landed for Console test scripts (Windows compatibility), mission parser quoting, approval dialog UX, and memory recovery prompts.

The team merged multiple infrastructure fixes, improving download fallback, queue management, and governance audit logging.

---

## 4. Community Hot Topics
- **#5218** [CLOSED] [Bug] Sub-agent context compaction causes process freeze.  
  URL: [Issue #5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)  
  18 comments, 0 👍. A long-standing critical bug that was closed today, likely fixed in v2.0.0.post4 reasoning optimization.

- **#6322** [CLOSED] [Question] Platform domain redirecting to ad pages.  
  URL: [Issue #6322](https://github.com/agentscope-ai/QwenPaw/issues/6322)  
  8 comments. User reports mobile network ad injection. Likely a third-party interference, not a CoPaw bug.

- **#6314** [OPEN] [Bug] RemoteProtocolError: peer closed connection.  
  URL: [Issue #6314](https://github.com/agentscope-ai/QwenPaw/issues/6314)  
  8 comments. High-severity networking issue with v1.1.2; active discussion.

- **#6318** [OPEN] [Feature] Per-conversation model selection instead of per-agent.  
  URL: [Issue #6318](https://github.com/agentscope-ai/QwenPaw/issues/6318)  
  6 comments. Popular feature request.

- **#6307** [OPEN] [Performance] v2.0 introduces ~2s overhead per reply.  
  URL: [Issue #6307](https://github.com/agentscope-ai/QwenPaw/issues/6307)  
  4 comments. Users are concerned about regression.

---

## 5. Bugs & Stability
**Critical:**
- **#6376** (OPEN) v2.0.0.post3/post4 new `loop` feature causes main process crash.  
  URL: [Issue #6376](https://github.com/agentscope-ai/QwenPaw/issues/6376)  
  User complains about lack of testing. No fix PR yet.

- **#6363** (OPEN) Tool_call arguments polluted with markdown fences/XML tags break all tool execution (GLM-5-Turbo, DeepSeek-V3).  
  URL: [Issue #6363](https://github.com/agentscope-ai/QwenPaw/issues/6363)  
  PR #6364 submitted to strip fences. **Fix exists**.

**High:**
- **#6362** (OPEN) MiniMax-M3 image recognition broken via built-in provider.  
  URL: [Issue #6362](https://github.com/agentscope-ai/QwenPaw/issues/6362)  
  Duplicate of #5135 (still open since June). No fix yet.

- **#6358** (OPEN) Context injection as `role='system'` causes ValueError on GLM/OpenAI.  
  URL: [Issue #6358](https://github.com/agentscope-ai/QwenPaw/issues/6358)  
  Fixed by PR #6359 (merged).

- **#6372** (OPEN) Idle cleanup removes newly recreated queue state.  
  URL: [Issue #6372](https://github.com/agentscope-ai/QwenPaw/issues/6372)  
  PR #6373 submitted to fix.

**Medium:**
- **#6370** (OPEN) File downloader fallback not triggered on timeout.  
  URL: [Issue #6370](https://github.com/agentscope-ai/QwenPaw/issues/6370)  
  PR #6371 submitted.

- **#6368** (OPEN) Audit logging not disabled when `audit_level=none`.  
  URL: [Issue #6368](https://github.com/agentscope-ai/QwenPaw/issues/6368)  
  PR #6369 submitted.

- **#6366** (OPEN) Console coverage test times out with V8 instrumentation.  
  URL: [Issue #6366](https://github.com/agentscope-ai/QwenPaw/issues/6366)  
  PR #6367 submitted.

- **#6361** (OPEN) Console test scripts fail on Windows.  
  URL: [Issue #6361](https://github.com/agentscope-ai/QwenPaw/issues/6361)  
  PR #6365 submitted.

- **#6355** (OPEN) Mission parser splits quoted `--verify` commands.  
  URL: [Issue #6355](https://github.com/agentscope-ai/QwenPaw/issues/6355)  
  PR #6356 submitted.

- **#6354** (OPEN) Approval dialog UI design risks accidental permanent grants.  
  URL: [Issue #6354](https://github.com/agentscope-ai/QwenPaw/issues/6354)  
  PR #6357 submitted to prioritize one-time approval.

- **#6374** (OPEN) Token usage persistence does not retry after transient write failure.  
  URL: [Issue #6374](https://github.com/agentscope-ai/QwenPaw/issues/6374)  
  PR #6375 (closed) fixes this.

---

## 6. Feature Requests & Roadmap Signals
- **Per-conversation model selection** (#6318): Strong community demand. Could be targeted for next minor release.
- **Per-cron-job model override** (#6316, PR #6353): Already implemented in PR #6353 – likely in next post-release.
- **Drag-and-drop file upload** (#6297): Requested for contract review workflows. Not in current milestone but requested.
- **Docker hot-update without container rebuild** (#6344): User suggests AstrBot pattern. Unlikely immediate priority.
- **Plugin market sorting** (#6349, PR merged): Already implemented today – sorting by downloads, update time, favorites.
- **QwenPaw Creator app** (#6284, under review): New app-type plugin for script-to-video workflow. Shows expansion into creative AI.

---

## 7. User Feedback Summary
- **Satisfaction**: v2.0.0.post4 addresses "redundant thinking loops" – a common complaint from v2.0.0.post3.
- **Dissatisfaction**: Several users reported v2.0 introduces **~2s fixed overhead** (#6307), **process crashes** (#6376), and **model response truncation** (#6324). One user questioned quality assurance: “发布前不能测试一些么，最好压力测试一些啊” (“Can't you test before release? Do stress testing at least.”).
- **Pain points**: MiniMax-M3 vision broken, MiniMax-M3 image recognition (#5135, #6362) has been open since June with no fix. Users integrating with enterprise environments also hit networking/timeout issues (#6314, #6370).
- **Positive feedback**: Community contributors are active – many first-time fix PRs landed today, improving UX, testability, and Windows support.

---

## 8. Backlog Watch
- **#5135** [OPEN] *MiniMax-M3 visual capability abnormal*  
  Created 2026-06-11, last updated 2026-07-22. 1 comment, 1 👍. No fix or acknowledgement from maintainers. Duplicate #6362 filed today. Requires urgent attention.

- **#6176** [CLOSED] *cron CLI update resets runtime/metadata fields*  
  Closed today, but the underlying issue of CLI overwriting JSON spec fields may still affect users who rely on Console-set fields.

- **#5218** [CLOSED] *Sub-agent context compaction freeze*  
  Closed after 1 month. If the fix is in v2.0.0.post4, users still on v1.x may need a backport.

- **#6324** [OPEN] *Model response truncated (MiniMax-M3)*  
  Opened 2026-07-22, no maintainer response yet.

- **#6326** [OPEN] *Please explicitly specify Node.js version*  
  Low-comment but important for contributors running Console.

Maintainers should prioritize:
1. Investigating and fixing the v2.0 overhead (#6307) and crash (#6376).
2. Resolving MiniMax-M3 image recognition (#5135 / #6362).
3. Merging all pending first-time-contributor fixes (#6364, #6369, #6371, #6373, #6367, #6365, #6357, #6356, #6352, #6351, #6348) to improve stability and reduce regressions.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-23

## 1. Today's Overview
ZeroClaw saw moderately high activity over the past 24 hours: **50 issues were updated** (10 closed, 40 still open) and **50 pull requests were updated** (all still open, none merged or closed). No new releases were published. The open PR count is inflated by many items tagged `needs-author-action` — a sign that maintainer feedback is pending author response. On the issue side, several long-running RFCs and high-priority bugs (Windows test failures, npm audit failures) remain active. Overall, the project is in a stable “shipping new features while tending to quality” phase, with a strong emphasis on security, observability, and multi-platform support.

## 2. Releases
No new releases were recorded today.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours, but **10 issues were closed**, indicating some completed work or decisions. Notable closed issues include:
- **#6641** — [Turn-level OTel trace correlation](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) (observability milestone, 8 comments)
- **#7184** — [RFC: Move translated .ftl/.po files into a git submodule](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) (i18n repo cleanup)
- **#7218** — [RFC: A2A agent discovery (.well-known/agent-card.json)](https://github.com/zeroclaw-labs/zeroclaw/issues/7218) (multi‑agent interoperability)
- **#6557** — [Reconcile runtime model switching with provider structure](https://github.com/zeroclaw-labs/zeroclaw/issues/6557)
- **#8837** — [[Bug]: history trimming occurs silently with history pruning disabled](https://github.com/zeroclaw-labs/zeroclaw/issues/8837) (critical runtime fix)
- **#6489** — [Feature: "Everything is a plugin" unification path](https://github.com/zeroclaw-labs/zeroclaw/issues/6489)
- **#8925** — [Docs: Explain Bedrock credential profiles and systemd service setup](https://github.com/zeroclaw-labs/zeroclaw/issues/8925) (documentation)

These closures reflect progress in observability, multi‑agent discovery, localization infrastructure, and provider/model consistency.

## 4. Community Hot Topics
The following issues and PRs attracted the most discussion (comments and reactions) in recent days:

- **[Issue #7462: [Bug]: 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)** — **11 comments, S2 severity**. The test suite fails comprehensively on Windows 11 (Chinese locale, code page 936) due to Unix‑only test commands, path semantics, and console encoding. The community is concerned about CI’s Linux‑only coverage and wants Windows parity.
- **[Issue #7141: RFC: OIDC authentication provider support](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)** — **7 comments, high priority, P1**. An umbrella tracking issue for pluggable OIDC auth, with several DoD items still outstanding. Strong interest from enterprise users.
- **[Issue #6641: Turn-level OTel trace correlation](https://github.com/zeroclaw-labs/zeroclaw/issues/6641)** — **8 comments, closed now**. The discussion centered on the `#[tracing::instrument]` approach and follow‑up to earlier feature work.
- **[Issue #6850: RFC: Decouple memory lifecycle policy from storage backends](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)** — **6 comments, high risk**. Proposes a `MemoryStrategy` trait to separate high‑level memory policies from backends.
- **[Issue #6391: Feature: real heartbeat tracking for daemon nodes](https://github.com/zeroclaw-labs/zeroclaw/issues/6391)** — **6 comments, no‑stale**. Users want a move from static “Online” status to true liveness detection via WebSocket message recency.

Underlying needs: cross‑platform compatibility (Windows), enterprise security (OIDC), and better operational observability (heartbeats, memory strategies).

## 5. Bugs & Stability
Several bugs were reported or remain active. Severity ranking (high to low):

| Severity | Issue | Summary | Fix PR exists? |
|----------|-------|---------|----------------|
| **Critical** | [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 74 test failures on Windows — CI blind spot | No |
| **Critical** | [#9235](https://github.com/zeroclaw-labs/zeroclaw/issues/9235) | npm audit failed (high/critical vulns in `@redocly/openapi-core`) | No |
| **High** | [#6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724) | Empty credentials on Signal/Voice Call channel cause supervisor crashloop | No |
| **High** | [#6916](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) | Process‑memory limits on shell/skill_tool subprocesses (OOM risk) | No |
| **High** | [#8837](https://github.com/zeroclaw-labs/zeroclaw/issues/8837) | Silent history trimming despite `history_pruning disabled` | Closed |
| **Medium** | [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) | Channel runtime command replies bypass Fluent localization | No |
| **Medium** | [#8943](https://github.com/zeroclaw-labs/zeroclaw/issues/8943) | Bedrock Nova 2 model fails with `cachePoint` error | PR #8943 open |

New bug fixes in PRs: **#8680** (skill‑review history slice bound against compaction), **#8576** (env‑var fallback for OpenAI STT credentials), **#8838** (idle‑bound SSE streaming on shared transport). These are all open and awaiting review or author action.

## 6. Feature Requests & Roadmap Signals
The backlog is rich with RFCs and feature requests that strongly suggest the next minor release (v0.9.0) focus on:

- **Security & Auth** — OIDC provider support ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) and per‑model capability/context‑window config ([#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100))
- **Multi‑Agent & Discovery** — A2A agent cards ([#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)), LAN peer discovery ([PR #8325](https://github.com/zeroclaw-labs/zeroclaw/pull/8325))
- **Observability** — Structured observability with rich events and OTel trace correlation ([#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232)), Herdr agent reporting ([PR #8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337))
- **Agent Evaluation** — `zeroclaw eval` harness with replay and live modes ([#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065))
- **Channel Expansion** — Native channels for Mastodon ([#6423](https://github.com/zeroclaw-labs/zeroclaw/issues/6423)), Twilio SMS ([#6427](https://github.com/zeroclaw-labs/zeroclaw/issues/6427)), Rocket.Chat ([#6435](https://github.com/zeroclaw-labs/zeroclaw/issues/6435)), Zulip ([#6437](https://github.com/zeroclaw-labs/zeroclaw/issues/6437)), and Inkbox ([PR #8384](https://github.com/zeroclaw-labs/zeroclaw/pull/8384))
- **Zero‑Downtime Operations** — Hot‑reload for security policy and channel config ([#7897](https://github.com/zeroclaw-labs/zeroclaw/issues/7897))
- **OpenAI‑Compatible API** — Gateway OpenAI chat completions endpoint ([PR #8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486))

These features align with user demand for production‑readiness, ecosystem interoperability, and richer observability.

## 7. User Feedback Summary
- **Pain points (Windows)** — Explicit frustration from a Chinese‑locale Windows user (NiuBlibing) about 74 test failures, leading to calls for Windows CI coverage.
- **Silent data loss** — User susyabashti reported that history trimming occurred even when pruning was disabled, requiring manual querying to discover the lost context. The bug was quickly closed, indicating a fix is in.
- **Configuration confusion** — User ngamradt struggled to configure Amazon Bedrock with profiles and systemd, leading to a new documentation issue ([#8925](https://github.com/zeroclaw-labs/zeroclaw/issues/8925)) that was subsequently closed with docs.
- **Desire for operational control** — Several requests for zero‑downtime reload ([#7897](https://github.com/zeroclaw-labs/zeroclaw/issues/7897)), real heartbeat tracking ([#6391](https://github.com/zeroclaw-labs/zeroclaw/issues/6391)), and per‑provider fallback notices ([#7883](https://github.com/zeroclaw-labs/zeroclaw/issues/7883)) show that operators want fine‑grained control over agent behavior without restarts.
- **Satisfaction signals** — The swift closure of #6641 (OTel trace correlation) and #8837 (history trimming) indicates the team values observability and stability. Positive reactions to the Inkbox channel and OpenAI‑compatible endpoint suggest feature requests are well received.

## 8. Backlog Watch
The following items have been open for an extended period (≥45 days) without apparent closure or merge, and still lack maintainer attention or a clear path forward:

| Item | Age | Last Activity | Status |
|------|-----|---------------|--------|
| [#6391](https://github.com/zeroclaw-labs/zeroclaw/issues/6391) — Real heartbeat tracking | 2026-05-05 | Last updated 2026-07-22 | Open, no‑stale |
| [#6390](https://github.com/zeroclaw-labs/zeroclaw/issues/6390) — `zeroclaw node add` CLI | 2026-05-05 | Last updated 2026-07-22 | Open, no‑stale |
| [#6416](https://github.com/zeroclaw-labs/zeroclaw/issues/6416) — Quickstart validation warnings | 2026-05-06 | Last updated 2026-07-22 | Open, no‑stale |
| [#6423](https://github.com/zeroclaw-labs/zeroclaw/issues/6423) — Mastodon channel | 2026-05-06 | Last updated 2026-07-22 | Open, no‑stale |
| [#6427](https://github.com/zeroclaw-labs/zeroclaw/issues/6427) — Twilio SMS channel | 2026-05-06 | Last updated 2026-07-22 | Open, no‑stale |
| [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) — Localization bypass in channel commands | 2026-05-09 | Last updated 2026-07-22 | Open, no‑stale |
| [#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715) — Delete

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*