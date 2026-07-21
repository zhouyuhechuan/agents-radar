# OpenClaw Ecosystem Digest 2026-07-21

> Issues: 353 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-21 01:57 UTC

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

# OpenClaw Project Digest — 2026-07-21

## Today's Overview

OpenClaw shows very high development activity with **353 issues** and **500 pull requests** updated in the last 24 hours. Of those PRs, **107 were merged or closed**, indicating a steady rate of feature landing and bug fixing. However, no new version releases were published today. The project continues to focus on stability across multi-platform deployments (Telegram, Discord, Slack, QQ Bot, Feishu) and addressing deep session-state and message-delivery regressions that have persisted in recent builds. The high comment counts on top issues reflect ongoing community concern around context management, security boundaries, and cross-backend model compatibility.

## Releases

No new releases were published on 2026-07-21.

## Project Progress

**Merged/Closed PRs (107 total)** — notable completed work includes:

- **Codex WebSocket SSRF guard** – [PR #111233](https://github.com/openclaw/openclaw/pull/111233) replaces a naive `startsWith("127.")` host check with proper `isIP()` to prevent DNS-based SSRF bypasses.
- **Windows `exec`/`read` empty output fix** – [PR #110198](https://github.com/openclaw/openclaw/pull/110198) resolves detached spawn leaks causing empty returns under headless Windows hosts.
- **Microsoft voice discovery resilience** – [PR #110784](https://github.com/openclaw/openclaw/pull/110784) (closed) handles malformed catalog rows gracefully.
- **QQ Bot memory and connection fixes** – [PR #110002](https://github.com/openclaw/openclaw/pull/110002) avoids memory spikes from oversized `clientSecretFile`; [PR #110008](https://github.com/openclaw/openclaw/pull/110008) cancels non-OK response bodies to prevent connection leaks.
- **CI maturity evidence timeout** – [PR #111980](https://github.com/openclaw/openclaw/pull/111980) (closed) prevents premature failure of long-running QA runs.
- **JSON console logging** – [PR #111908](https://github.com/openclaw/openclaw/pull/111908) ensures structured JSON output even in legacy code paths.
- **Mattermost tool warning timing** – [PR #111937](https://github.com/openclaw/openclaw/pull/111937) defers non-terminal tool error warnings until the turn settles, avoiding misleading final deliverable messages.
- **Cron `deliveryBestEffort` respect** – [PR #111453](https://github.com/openclaw/openclaw/pull/111453) stops interim-message suppression when `deliveryBestEffort: true` is set.
- **Cron task history aging** – [PR #111938](https://github.com/openclaw/openclaw/pull/111938) prunes stale cron task entries after 30 days.

**Open PRs of note** – large features still in review:  
- **Session stream mode** ([#93218](https://github.com/openclaw/openclaw/pull/93218)) – adds per-session preview streaming toggle.  
- **Tool result redaction** ([#81185](https://github.com/openclaw/openclaw/pull/81185)) – redacts sensitive payloads from exec tool output.  
- **Subagent announce target** ([#101248](https://github.com/openclaw/openclaw/pull/101248)) – native routing for subagent completion delivery.  
- **WorkBoard–Dashboard integration** ([#111989](https://github.com/openclaw/openclaw/pull/111989)) – stitches cards to session dashboards (new feature).  
- **Signed publisher feeds** ([#109305](https://github.com/openclaw/openclaw/pull/109305)) – search and follow DSSE-signed feeds.

## Community Hot Topics

The most active discussions (by comment count) reveal deep concern around session reliability and security:

- **Tool output rendered as image attachments** ([#99241](https://github.com/openclaw/openclaw/issues/99241), 23 comments, 2 👍) – long-running or ANSI-heavy tool results become unreadable image placeholders. Community wants a proper text fallback.
- **Turn-completion stall regression** ([#88312](https://github.com/openclaw/openclaw/issues/88312), 22 comments, 5 👍, *closed*) – Codex-backed multi-tool turns fail with "Codex stopped before confirming the turn was complete". Fixed by earlier PR #85107 but regressed in 2026.5.27.
- **Memory trust tagging by source** ([#7707](https://github.com/openclaw/openclaw/issues/7707), 19 comments) – request to tag memory entries by origin (user, web, third-party) to prevent poisoning.
- **Telegram turn timeouts** ([#87744](https://github.com/openclaw/openclaw/issues/87744), 17 comments, 3 👍) – Codex-backed Telegram sessions repeatedly time out after update to 2026.5.27.

Underlying needs center on **reliable session lifecycle** (no lost messages, no false context overflows) and **gradual adoption of security hardening** (secrets masking, exec sandboxing, permission manifests).

## Bugs & Stability

**High-severity regressions and crashes** (P1, often with impact:session-state, impact:message-loss):

| Issue | Description | Status |
|-------|-------------|--------|
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | Tool outputs collapse into unreadable image attachments | Open, needs live repro |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex turn-completion stall regression (2026.5.27) | Closed |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Telegram Codex-backed turns repeatedly time out | Open, source repro |
| [#86684](https://github.com/openclaw/openclaw/issues/86684) | Subagent wake compacts parent session at low context usage (65k/1.05M) | Open, needs live repro |
| [#78562](https://github.com/openclaw/openclaw/issues/78562) | Repeated tool-loop compaction cycles after successful compaction | Open, source repro |
| [#64810](https://github.com/openclaw/openclaw/issues/64810) | Heartbeat/system events interrupt and swallow in-progress replies | Open, linked PR open |
| [#58514](https://github.com/openclaw/openclaw/issues/58514) | Google Chat group messages silently ignored (DMs work) | Open, linked PR open |
| [#56733](https://github.com/openclaw/openclaw/issues/56733) | Gateway process alive but event loop frozen – all HTTP timeouts | Open, needs live repro |
| [#108238](https://github.com/openclaw/openclaw/issues/108238) | Session context misreports `cacheRead` as totalTokens, triggering false compaction | Closed (2026.7.1 regression) |
| [#109017](https://github.com/openclaw/openclaw/issues/109017) | Anthropic provider disappears from model picker; static catalog never pulls new models | Open, needs product decision |

**New security-related bugs** – [#88562](https://github.com/openclaw/openclaw/issues/88562) (apiKey written as plain string instead of secret-ref object), [#101349](https://github.com/openclaw/openclaw/issues/101349) (cron `toolsAllow` cannot be cleared, blocking claude-cli backend). Both P1, open.

**Fix PRs in flight** – [#111233](https://github.com/openclaw/openclaw/pull/111233) (Codex SSRF), [#110198](https://github.com/openclaw/openclaw/pull/110198) (Windows exec), [#111841](https://github.com/openclaw/openclaw/pull/111841) (configless gateway rebind fix) are critical.

## Feature Requests & Roadmap Signals

**Prominent user-requested features** (by engagement and project priority tags):

- **Masked secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659), P1, 15 comments, 4 👍) – allow agents to *use* API keys without *seeing* them. Likely to land soon given security focus.
- **Memory trust tagging by source** ([#7707](https://github.com/openclaw/openclaw/issues/7707), P2, 19 comments) – foundational for memory integrity; may see prototype in next release.
- **Exec sandbox isolation** ([#58730](https://github.com/openclaw/openclaw/issues/58730), P1, 6 comments) – inspired by Claude Code source analysis; high priority but complex.
- **Adopt Claude Code multi-layer compaction** ([#58398](https://github.com/openclaw/openclaw/issues/58398), P2, 6 comments) – to avoid repeated compaction loops.
- **Antigravity CLI (agy) backend** ([#84527](https://github.com/openclaw/openclaw/issues/84527), P2, 5 comments, 11 👍) – urgent due to Google Gemini CLI deprecation (deadline June 18, 2026).
- **Per-model generation timeout** ([#8724](https://github.com/openclaw/openclaw/issues/8724), P2, 5 comments) – to break infinite thinking loops in Google models.
- **Session `maxTurns`/`maxToolCalls`** ([#9912](https://github.com/openclaw/openclaw/issues/9912), P2, 5 comments) – limit agent iterations to prevent runaway tool calls.

**Prediction for next version**: The Antigravity CLI backend, masked secrets, and the compaction architecture improvements are most likely to appear in an upcoming release, given their high community demand and security implications.

## User Feedback Summary

**Common pain points** from comments and issues:

- **Session reliability** – Many users report *message loss*, *phantom compactions*, and *silent timeouts* after upgrading to 2026.5.27/2026.7.1. The `cacheRead` counting bug (#108238) was a recent exacerbation.
- **Platform inconsistencies** – Google Chat groups silent, Discord multi-workspace issues, QQ Bot memory spikes, Mattermost false warnings, Slack multi-workspace DM failures. Each platform has its own edge cases.
- **Security hardening** – Users are increasingly demanding credential protection (masked secrets, denylist for exec, permission manifests) especially after the Claude Code source leak discussion.
- **Model provider churn** – Google Gemini CLI deprecation forces migration to Antigravity CLI; Anthropic’s static catalog fails to discover new models; MiniMax API shape changes.

**Satisfaction indicators**: The high number of open PRs (393) and active issue triage suggests a responsive maintainer team, but the volume of regression bugs (especially around Codex-backed turns) indicates recent releases have introduced more instability than users expect.

## Backlog Watch

**Long-open, important items requiring maintainer attention** (labeled `needs-maintainer-review` or `needs-product-decision`, often P1-P2, many since February–March 2026):

- **Memory trust tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707), Feb 3, P2)
- **Masked secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659), Feb 6, P1)
- **Suppress sub-agent announce** ([#8299](https://github.com/openclaw/openclaw/issues/8299), Feb 3, P2)
- **Suppress transient tool error warnings** ([#39406](https://github.com/openclaw/openclaw/issues/39406), Mar 8, P2)
- **Session `maxTurns`** ([#9912](https://github.com/openclaw/openclaw/issues/9912), Feb 5, P2)
- **Session end hook** ([#10142](https://github.com/openclaw/openclaw/issues/10142), Feb 6, P2)
- **Per-model timeout** ([#8724](https://github.com/openclaw/openclaw/issues/8724), Feb 4, P2)
- **Google Chat silent ignore** ([#58514](https://github.com/openclaw/openclaw/issues/58514), Mar 31, P1, linked PR open)
- **Heartbeat swallowing replies** ([#64810](https://github.com/openclaw/openclaw/issues/64810), Apr 11, P1, linked PR open)
- **Repeated compaction loops** ([#78562](https://github.com/openclaw/open

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant Open-Source Ecosystem

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is highly active, with multiple reference implementations and community forks competing for developer mindshare. Projects share a common core challenge—building reliable, secure, multi-platform agents that can orchestrate tools, manage long-running sessions, and integrate with messaging platforms (Telegram, Discord, QQ, Feishu, Slack, etc.). While OpenClaw remains the central reference, several projects (IronClaw, ZeroClaw, CoPaw) are undergoing major architectural rewrites (e.g., replacing monolithic codebases, introducing control planes, adding agent evaluation harnesses), indicating the ecosystem is maturing past proof-of-concept into production-grade infrastructure. Security hardening, session reliability, and deployment ergonomics dominate community feedback across all projects.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | New Release | Health Score |
|---------|----------------------|-------------------|--------------------------|-------------|--------------|
| OpenClaw | 353 | 500 | 107 | No | **High** (very active, but many regressions) |
| IronClaw | 43 | 50 | 28 | No | **High** (large-scale refactoring, stable cadence) |
| ZeroClaw | 39 | 50 | 12 | No | **High** (active triage, major features in flight) |
| CoPaw | 30 | 42 | 10 | No | **High** (healthy community, many edge-case bugs) |
| Hermes Agent | 50 | 50 | 7 | v0.19.0 (yesterday) | **High** (post-release bug reports, rapid response) |
| NanoBot | 7 | 30 | 11 | No | **Medium** (steady improvements, small community) |
| PicoClaw | 11 | 10 | 5 | No | **Medium** (niche, single contributor cluster) |
| NanoClaw | 6 | 20 | 6 | No | **Medium** (security-focused, good engagement) |
| LobsterAI | 0 | 15 | 10 | No | **Medium** (moderate, dependency backlog) |
| NullClaw | 0 | 1 | 0 | No | **Low** (stagnant, 1 open Dependabot PR) |
| TinyClaw | 0 | 0 | 0 | No | **Inactive** |
| Moltis | 0 | 0 | 0 | No | **Inactive** |
| ZeptoClaw | 0 | 0 | 0 | No | **Inactive** |

*Health score based on volume of activity, responsiveness to bugs, and community engagement.*

## 3. OpenClaw’s Position

**Advantages vs. Peers:** OpenClaw maintains the largest community (353 issues, 500 PRs updated in 24h) and serves as the canonical reference implementation for multi-platform agent frameworks. Its integration surface covers Telegram, Discord, Slack, QQ Bot, Feishu, Mattermost, and Google Chat—broader than any other project. The volume of merged PRs (107/day) demonstrates sustained contributor throughput.

**Technical Approach Differences:** OpenClaw uses a monolithic codebase (TypeScript/Node.js?) compared to IronClaw’s Rust‑based Reborn rewrite or ZeroClaw’s modular control plane (SOP). OpenClaw innovates in session stream mode, tool result redaction, and subagent announce routing. However, it suffers from regression density: high-profile bugs like Codex turn-completion stalls (#88312) and heartbeat-induced message loss (#64810) erode trust in recent releases. No other project reports such systemic session reliability issues.

**Community Size Comparison:** OpenClaw’s issue/PR count is ~7× higher than the next busiest project (IronClaw, 50 PRs). No other project has a 500-PR daily volume. While the sheer size implies strong adoption, it also reflects a high bug reporting rate—suggesting OpenClaw’s user base is large but exposed to instability.

**Key Weakness:** Session lifecycle regressions (phantom compactions, false context overflows, Telegram timeouts) are unique to OpenClaw and not reported at similar scale in peers like NanoBot or Hermes Agent.

## 4. Shared Technical Focus Areas

Multiple projects independently prioritise the following needs:

- **Security Hardening**
  - Masked secrets / credential protection: OpenClaw (#10659), NanoBot (#4803), CoPaw (permission governance)
  - Permission manifests / role management: NanoClaw (approval routing #3099), ZeroClaw (skill sandbox #9084)
  - OAuth compliance: PicoClaw (Google OAuth policy violation #3278), IronClaw (Gmail auto‑grant #6348)

- **Session & Context Reliability**
  - Turn-completion stalls: OpenClaw (#88312), IronClaw (#6189)
  - Context compaction / memory overflow: OpenClaw (#78562), CoPaw (#6241 infinite loop)
  - Cross-platform session persistence: Hermes Agent (#4335), OpenClaw (session stream mode #93218)

- **Multi‑Platform Consistency**
  - Telegram, Discord, QQ, Feishu, Slack: all projects support at least 3 platforms; silent group messages, timeouts, and attachment drops are common across OpenClaw, NanoBot, NanoClaw, Hermes Agent.

- **Deployment Ergonomics**
  - One‑click deploy templates: NanoBot (Render #4937, Dokploy #5007)
  - Containerization: OpenClaw (cron task aging #111938), PicoClaw (Docker base bump #3192)
  - Windows compatibility: OpenClaw (#110198), ZeroClaw (#9117, #7462), CoPaw (#6239 PATH issues)

- **Agent Evaluation & Testing**
  - ZeroClaw introduced an agent evaluation harness (#7065) with LLM‑judge calibration.
  - OpenClaw has CI maturity evidence timeout (#111980) but no formal eval harness; other projects lack this entirely.

- **Local Model / Ollama Optimization**
  - NanoBot (#4867) and OpenClaw (Ollama tool prompt cache diagnostics) both report performance degradation with local models; users demand caching efficiency.

## 5. Differentiation Analysis

| Project | Unique Focus | Target Users | Technical Architecture |
|---------|--------------|--------------|------------------------|
| **OpenClaw** | Broadest platform integration (8+ channels); reference implementation | Large community, diverse use cases | Monolithic Node.js/TypeScript; session state machine, cron tasks |
| **IronClaw** | Rust‑based Reborn rewrite; high‑performance, long‑running agents | Developers needing low‑level control and scale | Rust, ACP, tier‑B v1 removal, store consolidation |
| **ZeroClaw** | SOP control plane, agent evaluation harness, A2A protocol | Agent ops teams, enterprise orchestration | Modular daemon with SOP ingress, eval harness, tool policy |
| **CoPaw** | Desktop GUI (Tauri), plugin ecosystem (pawapp), memory (ReMe Light) | Desktop power users, multimodal workflows | Python backend, Tauri desktop, plugin SDK |
| **Hermes Agent** | Desktop (Electron), CLI/TUI, cron jobs, cross‑platform session sharing | Desktop‑first users, CLI enthusiasts | Python, desktop overlay, plugin framework |
| **NanoBot** | Lightweight, channel‑first (Telegram, QQ, Feishu), one‑click deploy | Self‑hosters, non‑technical users | Python, minimal dependencies, channel adapters |
| **PicoClaw** | Golang? small footprint, provider compatibility (Antigravity, DashScope) | Users needing lightweight, multi‑provider agent | Go, goreleaser, WebUI launcher |
| **NanoClaw** | Security‑first: role management, approval routing, privilege auditing | Security‑conscious deployments | Python, CLI‑driven, containerised |
| **LobsterAI** | Cowork collaboration, AI skin creator, Windows silent updates | Enterprise collaboration, customisation | Electron/React, NSIS installer, RPC config |

## 6. Community Momentum & Maturity

**Tier 1 – Rapid Iteration (very high churn, major refactors in flight):**
- **OpenClaw** – largest volume; high risk of regressions but fast patching.
- **IronClaw** – aggressively removing legacy code; stream fixes and consolidation define the day.
- **ZeroClaw** – strong architectural momentum (SOP, eval harness); critical bugs addressed same-day.
- **CoPaw** – active plugin ecosystem development; community submitting detailed bug reports.

**Tier 2 – Steady Improvement (moderate activity, stable releases):**
- **Hermes Agent** – just shipped v0.19.0; post-release bug wave, but team responsive.
- **NanoBot** – consistent PR merge rate (11/day); 1‑click deploys growing adopters.
- **NanoClaw** – security‑focus drives rapid PR submission; all new bugs have fix PRs attached.
- **PicoClaw** – active single‑user contributor; provider compatibility regressions block some users.
- **LobsterAI** – moderate feature development (Cowork, skin creator); dependency PRs stale.

**Tier 3 – Stabilising / Inactive:**
- **NullClaw** – minimal activity; 1 open Dependabot PR untouched for 5 weeks; project may be on hold.
- **TinyClaw, Moltis, ZeptoClaw** – no visible commits, issues, or PRs; effectively dormant.

**Maturity Assessment:** OpenClaw is the most established but also the most unstable. IronClaw, ZeroClaw, and CoPaw are maturing quickly, with cleaner architectures. Hermes Agent has high M but needs to prove stability post‑release. NullClaw and the inactive projects risk being overtaken by alternatives.

## 7. Trend Signals

Several cross‑project patterns indicate where the ecosystem is heading:

1. **Security as a First‑Class Concern**  
   OAuth compliance, masked secrets, permission manifests, and sandboxing are appearing across OpenClaw, NanoClaw, ZeroClaw, and CoPaw. Google’s OAuth crackdown (PicoClaw #3278) and credential leaks (NanoBot #4803) are forcing maintainers to prioritise. Expect integrated secrets management and tool approval workflows in upcoming releases.

2. **Agent Evaluation Harness Emergence**  
   ZeroClaw’s eval harness (#7065) is the first standardised approach to agent quality measurement. With OpenClaw’s CI maturity issues and CoPaw’s loop detection problems, automated evaluation will become a must-have for any project claiming production readiness.

3. **Cross‑Platform Session Persistence**  
   Users want to move between CLI, desktop, Telegram, and WebUI without context loss. Hermes Agent (#4335), OpenClaw (stream mode #93218), and NanoClaw (WhatsApp Cloud issues) all touch this. The next frontier is unified session state with proper sync—not yet solved in any project.

4. **Deployment Friction Reduction**  
   One‑click templates (NanoBot, Render, Dokploy) and container image improvements (PicoClaw, OpenClaw) show demand for “zero‑config” self‑hosting. Enterprise users want systemd integration (PicoClaw #3276); community users want downloadable binaries with auto‑update (LobsterAI #2368).

5. **Plugin / Extension Ecosystems**  
   CoPaw’s pawapp SDK, Hermes Agent’s plugin framework, and LobsterAI’s skin creator all point toward app‑store‑like ecosystems. The challenge is security: supply‑chain verification (ZeroClaw #9084) and permission scoping are unsolved.

6. **Local Model Performance Optimisation**  
   Ollama prompt caching (NanoBot #4867) and tool description token waste (CoPaw #6286) are top complaints. As adoption of local LLMs grows, projects will need to support continuous batching, KV cache reuse, and dynamic tool trimming.

7. **Human‑in‑the‑Loop (HITL) Patterns**  
   Approval routing (NanoClaw), `ask_user_question` tools (CoPaw #6274), and sandbox fallback approvals (CoPaw #6250) show a trend toward giving humans control over agent actions. This is especially critical for enterprise deployments.

**Value for AI Agent Developers:**  
- If you need maximum platform reach, OpenClaw is the most mature but expect to invest in workarounds for session bugs.  
- For performance and clean architecture, IronClaw (Rust) or ZeroClaw (modular) are strong bets.  
- For desktop user experience and plugin expansion, CoPaw and Hermes Agent offer the richest GUI.  
- For security‑sensitive deployments, NanoClaw’s role‑based system is currently the best out‑of‑the‑box.  
- For lightweight self‑hosting, NanoBot leads with one‑click deploys.  

The ecosystem is diverging into specialised niches—generalist reference (OpenClaw), performance‑oriented (IronClaw), security‑focused (NanoClaw), and desktop‑centric (CoPaw, Hermes)—but all are converging on common needs: reliability, security, and cross‑platform persistence.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-07-21

## 1. Today’s Overview

Activity remains high with **30 pull requests** updated and **7 issues** touched in the last 24 hours. The project is undergoing a broad wave of bug fixes and feature additions across channels, agents, and deployment. Notably, **11 PRs were merged/closed**, including critical fixes for QQ WebSocket reconnection, Telegram/Feishu message splitting hangs, and a major refactor of the internal turn lifecycle. No new releases were published today. Security and stability improvements are the dominant themes, alongside community-driven requests for multi-agent collaboration and one-click deployment templates.

## 2. Releases

*No new releases were published today.*

## 3. Project Progress (Merged/Closed PRs)

11 pull requests were merged or closed. Key advancements:

- **Agent core**: [#4993](https://github.com/HKUDS/nanobot/pull/4993) (refactor: unify internal turn lifecycle) – completes a foundational refactor so that system messages (e.g., subagent results) go through the same `TurnContext` state machine, eliminating duplicate code and improving consistency.
- **QQ channel**: [#4768](https://github.com/HKUDS/nanobot/pull/4768) (fix: add exponential backoff to WebSocket reconnect loop) – addresses excessive error logging on DNS/network failures.
- **Provider (multimodal)**: [#5008](https://github.com/HKUDS/nanobot/pull/5008) (fix: keep all images when merging consecutive multimodal user turns) – prevents loss of images in album/multi-image flows.
- **Feishu channel**: [#4982](https://github.com/HKUDS/nanobot/pull/4982) (fix: avoid hang in fallback text chunks when limit <= 0).
- **Telegram channel**: [#4981](https://github.com/HKUDS/nanobot/pull/4981) (fix: avoid hang in markdown split when max_len <= 0).
- **Deployment**: [#4937](https://github.com/HKUDS/nanobot/pull/4937) (feat: add one-click deploy to Render support) – added a Render Blueprint for easy self-hosting.
- **Documentation**: [#4998](https://github.com/HKUDS/nanobot/pull/4998) (docs: Ollama tool prompt cache diagnostics) – new guide for diagnosing prompt-cache reuse across tool calls.
- Also closed: [#4999](https://github.com/HKUDS/nanobot/pull/4999) (duplicate of multi-agent proposal).

## 4. Community Hot Topics

- **Ollama prompt caching** – Issue [#4867](https://github.com/HKUDS/nanobot/issues/4867) (closed, 15 comments) – a user reported that Nanobot adds ~60s to every turn with Ollama due to prompt prefix alteration disabling caching. The issue was closed, but the discussion signals strong demand for provider‑level performance optimizations.
- **Multi-agent collaboration** – Issues [#5000](https://github.com/HKUDS/nanobot/issues/5000) and duplicate [#4999](https://github.com/HKUDS/nanobot/issues/4999) (open, 1 reaction) – a proposal to evolve the subagent system into true multi-agent collaboration with persistent identities and shared state. This is a high-impact feature request that could shape the project’s roadmap.
- **Dokploy template** – Issue [#1503](https://github.com/HKUDS/nanobot/issues/1503) (open since March) now has a corresponding PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) (feat: add Dokploy one‑click deploy template). The original request from a non‑technical user highlights the need for simplified self‑hosting.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | [#4864](https://github.com/HKUDS/nanobot/issues/4864) | Endless loop when `<tool_call><function=complete_goal>` errors due to gateway parameter serialization change. | Open; 4 comments, 1 reaction. Needs investigation. |
| **High** | [#4803](https://github.com/HKUDS/nanobot/issues/4803) | API keys stored as plaintext in `~/.nanobot/config.json`; `repr=False` does not exclude from `model_dump()`. | Open; 1 comment. PR [#5010](https://github.com/HKUDS/nanobot/pull/5010) improves documentation but does not fix the core issue. |
| **Medium** | [#4767](https://github.com/HKUDS/nanobot/issues/4767) | QQ channel WebSocket reconnect loop floods logs on DNS failure. | Fixed in [#4768](https://github.com/HKUDS/nanobot/pull/4768). |
| **Low–Medium** | Several PRs fix hang conditions: [#4982](https://github.com/HKUDS/nanobot/pull/4982) (Feishu), [#4981](https://github.com/HKUDS/nanobot/pull/4981) (Telegram), [#5004](https://github.com/HKUDS/nanobot/pull/5004) (unsupported directory fsync), [#5005](https://github.com/HKUDS/nanobot/pull/5005) (scoped tmp cleanup). | Merged/closed. |

Two open bugs require urgent attention: the complete_goal serialization regression ([#4864](https://github.com/HKUDS/nanobot/issues/4864)) and the plaintext secret storage ([#4803](https://github.com/HKUDS/nanobot/issues/4803)). The latter lacks a fix PR.

## 6. Feature Requests & Roadmap Signals

- **Multi‑agent collaboration** – [#5000](https://github.com/HKUDS/nanobot/issues/5000) (open) proposes evolving subagents into persistent, state‑sharing agents with agent‑to‑agent communication. Likely to appear in a future release given the high level of interest.
- **Dokploy one‑click deploy** – Requested in March ([#1503](https://github.com/HKUDS/nanobot/issues/1503)), now implemented in PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) (open). Expected to be merged soon, making Nanobot accessible to non‑technical users.
- **Guarded tool gateway** – PR [#5006](https://github.com/HKUDS/nanobot/pull/5006) (open) adds an opt‑in `ToolGateway` protocol for channel plugins, enabling tool execution with proper workspace and session context. Signals a move toward safer, extensible channel integrations.
- **Feishu group policy “listen” mode** – PR [#5009](https://github.com/HKUDS/nanobot/pull/5009) (open) allows group chatter to accumulate silently and only reply on `@mention`. Helps reduce noise in busy group chats.

## 7. User Feedback Summary

- **Performance pain**: The Ollama caching issue ([#4867](https://github.com/HKUDS/nanobot/issues/4867)) – “totally unusable with Ollama and 32 GB of VRAM” – reflects critical performance degradation for local model users.
- **Security concern**: The plaintext API key storage ([#4803](https://github.com/HKUDS/nanobot/issues/4803)) is a major trust risk; user frustration is implied by the minimal comment count (1) but the issue remains unaddressed.
- **Deployability**: Users want one‑click solutions (Dokploy [#1503](https://github.com/HKUDS/nanobot/issues/1503), Render [#4937](https://github.com/HKUDS/nanobot/pull/4937)) to reduce friction for non‑technical self‑hosters.
- **Multi‑agent aspiration**: The proposal for true multi‑agent collaboration ([#5000](https://github.com/HKUDS/nanobot/issues/5000)) indicates that advanced users find the current subagent system too limited for complex workflows.
- **Quality‑of‑life fixes**: The hang bugs (Feishu, Telegram, QQ) and the background turn silence fix ([#4988](https://github.com/HKUDS/nanobot/pull/4988)) demonstrate user tolerance for subtle edge cases that degrade reliability.

## 8. Backlog Watch

| Issue | Age | Priority | Action |
|-------|-----|----------|--------|
| [#1503](https://github.com/HKUDS/nanobot/issues/1503) – Dokploy template | 4.5 months (Mar 4) | Medium | PR [#5007](https://github.com/HKUDS/nanobot/pull/5007) is open; merge and close. |
| [#4803](https://github.com/HKUDS/nanobot/issues/4803) – API key plaintext | 15 days (Jul 6) | **High** (security) | No fix PR yet; maintainers should prioritize a solution (e.g., exlusion from `model_dump` or encryption). |
| [#5000](https://github.com/HKUDS/nanobot/issues/5000) – Multi‑agent collaboration | 1 day (Jul 20) | Medium–High | Early stage; needs roadmap discussion and assignment. |
| [#4864](https://github.com/HKUDS/nanobot/issues/4864) – Endless loop with complete_goal | 12 days (Jul 9) | **High** (user blocking) | Likely a regression; has a clear reproduction. Should be paired with a fix PR. |

The project’s rapid merge activity is encouraging, but security and the `complete_goal` regression remain unresolved and require maintainer attention in the near term.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-21

## 1. Today's Overview
Project activity remains very high, with **50 issues** and **50 pull requests** updated in the last 24 hours. The community continues to actively report bugs and propose features against the freshly released **v0.19.0 (“Quicksilver Release”)**, which shipped yesterday with over 2,200 commits and 3,300 closed issues. Despite the release, several **P1/P2 regressions** have emerged today, including a critical packaging flaw that can kill user sessions (Issue #68311) and a broken `brew upgrade` path on macOS (Issue #29866). The maintainer team has responded rapidly – a fix PR for the session-kill canary is already open (#68317) – indicating strong momentum.

## 2. Releases
**v0.19.0 (v2026.7.20) – “The Quicksilver Release”**  
- **Size:** ~2,245 commits · ~1,065 merged PRs · ~3,300 issues closed · 450+ contributors.  
- **Notable changes:** No explicit changelog excerpt is provided in the data, but the release follows a massive development cycle (since v0.18.0). Users should review the [full release notes](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.7.20) for breaking changes and migration steps.  
- **Known post-release issues:** See Bugs & Stability section below.  

*No other releases in the last 24h.*

## 3. Project Progress
While the top 20 PRs shown are all **open**, the 7 merged/closed PRs for the day include critical fixes that have reached `main`:
- **[Issue #46511]** – Cron jobs now properly fall back when credential pool is exhausted (OAuth providers). *(Closed as implemented-on-main)*
- **[Issue #67817]** – Telegram connection failure `'HTTPXRequest' object attribute 'do_request' is read-only` was fixed.  
- **[Issue #66611]** – Desktop “Already up to date” overlay close button issue resolved.  
- **[Issue #67194]** – Windows installer crash (appearance bug) was closed as a duplicate / already fixed.

Additional merged/closed PRs (not listed in top 20) likely include the roll-up of smaller fixes and feature branches.

## 4. Community Hot Topics
Most active discussion threads (by comment count / reactions):

| Issue / PR | Title | Comments | 👍 |
|------------|-------|----------|----|
| [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | Desktop session sidebar empty for `default` profile – named profiles work | **9** | 0 |
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Cross-platform session context sharing (CLI ↔ Telegram) | **8** | 2 |
| [#2788](https://github.com/NousResearch/hermes-agent/issues/2788) | Cron jobs never run / failed without useful logs | **6** | 0 |
| [#3944](https://github.com/NousResearch/hermes-agent/issues/3944) | Slack integration in gateway fails | **5** | 1 |
| [#66868](https://github.com/NousResearch/hermes-agent/issues/66868) | Cron job primary model call fails 401 – provider collapses to "custom" outside runtime session | **5** | 0 |
| [#68311](https://github.com/NousResearch/hermes-agent/issues/68311) **(P1)** | Every sdist ships a canary test that can kill user's entire session | **3** | 0 |
| [#29866](https://github.com/NousResearch/hermes-agent/issues/29866) **(P1)** | `brew upgrade` breaks certifi – all messaging platforms fail | **4** | 0 |
| [#4256](https://github.com/NousResearch/hermes-agent/issues/4256) | Configurable keybindings via config.yaml | **3** | **6** (highest 👍) |

**Underlying needs:**
- **Session isolation & routing** dominates: users expect seamless cross-platform conversations (CLI↔Telegram) but platforms are currently siloed (#4335). Sidebar emptiness (#67600) and credential prompt misrouting (#68261) further erode trust in session management.
- **Cron reliability** is a recurring pain point: silent failures (#2788), missing fallback (#66868), and poor logging.
- **Installation & update fragility** is acute: `brew upgrade` breaks TLS (#29866) and the sdist packaging bug (#68311) is a serious security/UX concern.
- **Plugin ecosystem extensibility** is in demand: `send_message` schema cannot be extended (#64900), MCP server management missing (#690).

## 5. Bugs & Stability
Bugs reported in the last 24 hours, ranked by severity:

- **🔴 P1 – Critical**  
  - **[#68311](https://github.com/NousResearch/hermes-agent/issues/68311)** – Every published sdist (0.13.0–0.19.0) includes `tests/test_live_system_guard_self_test.py` without its required `conftest.py`. Running the packaged tests executes `os.kill(-1, SIGTERM)`, killing the user's session. **Fix PR [#68317](https://github.com/NousResearch/hermes-agent/pull/68317) is already open** to make the canary fail closed.  
  - **[#29866](https://github.com/NousResearch/hermes-agent/issues/29866)** – `brew upgrade hermes-agent` breaks `certifi` (missing `cacert.pem`). Feishu, Telegram, WeChat all fail.  

- **🟠 P2 – High**  
  - **[#67600](https://github.com/NousResearch/hermes-agent/issues/67600)** – Desktop session sidebar empty for `default` profile only. Backend confirms rows are served.  
  - **[#68261](https://github.com/NousResearch/hermes-agent/issues/68261)** – TUI skill credential prompts routed to wrong session (process-global callback).  
  - **[#68244](https://github.com/NousResearch/hermes-agent/issues/68244)** – After update, answering “no” to “Restore local changes” breaks agent → won't start.  
  - **[#68318](https://github.com/NousResearch/hermes-agent/issues/68318)** – Plugin handlers crash with `TypeError: unexpected keyword argument 'task_id'` in v0.19.0.  
  - **[#66868](https://github.com/NousResearch/hermes-agent/issues/66868)** – Cron jobs fail with HTTP 401 on primary model call; provider collapses to "custom".  
  - **[#61573](https://github.com/NousResearch/hermes-agent/issues/61573)** – Desktop: message queued in a busy session delivered to an unrelated idle session.  
  - **[#2228](https://github.com/NousResearch/hermes-agent/issues/2228)** – System error messages injected with dynamic `role=user`, confusing the agent.  

- **🟡 P3 – Medium**  
  Multiple P3 bugs in open issues – e.g., [#2513](https://github.com/NousResearch/hermes-agent/issues/2513) (custom provider context length not auto-detected), [#55369](https://github.com/NousResearch/hermes-agent/issues/55369) (union arg `"007"` coerced to integer 7), [#55551](https://github.com/NousResearch/hermes-agent/issues/55551) (Groq STT ignores language parameter).  

*Fix PRs exist for several of these (e.g., #68317 for #68311, #68319 for #68300, #68323 for desktop sidebar).*

## 6. Feature Requests & Roadmap Signals
Top user-requested features from recent issues:

| Issue | Feature | Likelihood for v0.20.0 |
|-------|---------|------------------------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Cross-platform session context sharing (CLI ↔ Telegram) | **Medium** – high 👍 count, core UX gap |
| [#64900](https://github.com/NousResearch/hermes-agent/issues/64900) | Allow plugins to extend `send_message` with platform-specific schema | **High** – plugin ecosystem needs |
| [#690](https://github.com/NousResearch/hermes-agent/issues/690) | MCP Server Management: CLI, discovery, tool selection | **Medium** – long-standing (March), maintainer awareness |
| [#41075](https://github.com/NousResearch/hermes-agent/issues/41075) | `hermes sessions archive` / `compress` | **Low** – no traction yet |
| [#4256](https://github.com/NousResearch/hermes-agent/issues/4256) | Configurable keybindings via `config.yaml` | **High** – 6 👍, obvious UX improvement |
| [#67316](https://github.com/NousResearch/hermes-agent/issues/67316) | Allow calling skills mid-prompt (not just at start) | **Medium** – desktop interaction pain point |

**Predictions for next release:** Plugin system enhancements (send_message extensibility, plugin framework fixes) and keybinding configurability are strong candidates. The session context bridging (#4335) may land as a follow-up to the routing fixes already in progress.

## 7. User Feedback Summary
Real pain points and use cases observed:

- **Session management frustration:**  
  “Desktop session sidebar empty for default profile” (#67600) – users see a blank UI despite backend data.  
  “Message queued in busy session went to wrong thread” (#61573) – erodes trust in multi-session workflows.

- **Cron unreliability:**  
  Silent failures with no useful logs (#2788, #66868) leave users unaware that tasks are not executing.

- **Installation & update woes:**  
  `brew upgrade` breaks TLS (#29866), PyPI 0.17.0 wheel missing files (#49529), update prompt “Restore local changes?” unclear and destructive (#68244) – users feel updates are risky.

- **Plugin crashes after v0.19.0:**  
  “All my plugin tools are broken” (#68318) – a major regression for the plugin ecosystem.

- **Positive signals:**  
  The community is actively contributing skills (e.g., qodercli skill PR #68314) and plugin improvements (Fluxer plugin skeleton #68260). The high number of closed issues (3,300 since v0.18.0) shows robust maintenance despite rough edges.

## 8. Backlog Watch
Issues and PRs that have been open for extended periods with little recent maintainer activity, yet remain important:

| ID | Type | Title | Created | Last Update | Comments | Status |
|----|------|-------|---------|-------------|----------|--------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Feature | Cross-platform session sharing | 2026-03-31 | 2026-07-21 | 8 | Open, no milestone |
| [#2788](https://github.com/NousResearch/hermes-agent/issues/2788) | Bug | Cron jobs never run / no logs | 2026-03-24 | 2026-07-20 | 6 | Open, no assignee |
| [#690](https://github.com/NousResearch/hermes-agent/issues/690) | Feature | MCP Server Management CLI | 2026-03-08 | 2026-07-21 | 4 | Open, duplicate label |
| [#2228](https://github.com/NousResearch/hermes-agent/issues/2228) | Bug | System error injected as role=user | 2026-03-20 | 2026-07-20 | 3 | Open |
| [#2513](https://github.com/NousResearch/hermes-agent/issues/2513) | Bug | Custom provider context length not auto-detected | 2026-03-22 | 2026-07-20 | 3 | Open |
| [#45317](https://github.com/NousResearch/hermes-agent/pull/45317) | PR (Open) | Fix BlueBubbles duplicate inbound turns (v0.19.0) | 2026-06-13 | 2026-07-21 | – | Open, no recent activity |

These items represent **persistent community needs** (especially cross-platform sharing and cron reliability) that, if left unaddressed, may cause user churn. Maintainer attention on #4335 and #2788 would be particularly impactful for user trust.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-07-21

## 1. Today's Overview

The PicoClaw project saw high activity over the past 24 hours with **11 issues updated** (7 open, 4 closed) and **10 pull requests updated** (5 open, 5 merged/closed). No new releases were published. A significant cluster of issues and one PR came from a single user (`honbou`), covering regressions, Google OAuth policy violations, and feature requests for Japanese localization and external gateway management. The most impactful merged PR (`#3277`) fixed a critical tool-visibility bug that could silently break MCP tool calls across sessions. Overall, development momentum remains strong, especially around provider compatibility and deployment ergonomics, though several long-standing bugs (Android, Matrix sync) remain unresolved.

## 2. Releases

*No new releases were published during the reporting period.*

## 3. Project Progress

The following pull requests were **merged or closed** today, representing tangible progress:

- **#3277** – `fix(tools): deferred-tool visibility heal + sliding TTL + SSE tool-call index fix` — Merged. Fixes a persistent issue where deferred MCP tools become invisible after a process restart or TTL expiry, causing the model to attempt calls to non-existent tools. Introduces persistent tool discovery storage and a sliding TTL mechanism.  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3277)

- **#3192** – `chore(docker): bump goreleaser base images from alpine:3.21 to 3.23` — Merged.  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3192)

- **#3191** – `chore: remove duplicate build/ entry in .gitignore` — Merged.  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3191)

- **#276** – `Docs/improve readme` — Closed (merged earlier, updated today). Polish of README wording and formatting.  
  [GitHub](https://github.com/sipeed/picoclaw/pull/276)

- **#277** – `feat: update the 'make deps' logic to prevent frequent dependency updates` — Closed.  
  [GitHub](https://github.com/sipeed/picoclaw/pull/277)

Additionally, four issues were closed today: **#3231** (basic auth for searxng feature), **#3230** (Gemini `thought_signature` bug), **#3229** (proposal for rolling conversation cache breakpoints), and **#3275** (config rewrite losing `api_keys` bug).

## 4. Community Hot Topics

The most active issues—by comments or reactions—are:

- **#3182** [BUG] “Android version” — **4 comments**. The user reports inability to launch the service on Android despite full permissions; path changes are ignored. The issue has been open since June 26, indicating ongoing frustration with mobile support.  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3182)

- **#3203** [BUG] “Matrix sync loop has no reconnection logic” — **3 comments, 1 👍**. A stale bug highlighting a silent death scenario when network or homeserver fails; the agent process stays alive so systemd does not restart. Users need robust Matrix reliability.  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3203)

- **#3274** [BUG] “Antigravity provider INVALID_ARGUMENT regression” — **1 comment**. Reported as a regression from v0.3.1; the `tool_schema_transform "simple"` is no longer sufficient. The user honbou updated this just hours after creating it, suggesting urgency.  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3274)

The underlying needs from these threads center on **provider stability** (Matrix, Antigravity) and **mobile platform support** (Android). The project appears to be actively used in heterogeneous environments where provider and network failures are common.

## 5. Bugs & Stability

Several bugs were reported or updated today. Ranked by severity:

| Severity | Issue | Description | Status | Fix PR exists? |
|----------|-------|-------------|--------|---------------|
| **Critical** | [#3278](https://github.com/sipeed/picoclaw/issues/3278) | Antigravity OAuth login blocked by Google: “doesn't comply with Google's OAuth 2.0 policy for keeping apps secure” | Open, no comments | No |
| **High** | [#3274](https://github.com/sipeed/picoclaw/issues/3274) | Antigravity provider regression: `INVALID_ARGUMENT` after upgrading from v0.3.1 | Open, 1 comment | No |
| **High** | [#3269](https://github.com/sipeed/picoclaw/issues/3269) | MCP server connection failure causes agent loop to hang; chat interface stops responding | Open, 0 comments | No |
| **Medium** | [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Android app cannot launch service or change settings path | Open since June 26 | No |
| **Medium** | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix sync loop dies permanently after network disruption – no reconnection | Open (stale) | No |
| **Low** | [#3275](https://github.com/sipeed/picoclaw/issues/3275) | Config rewrite via Launcher WebUI loses `api_keys` from `model_list` entries | **Closed** today | Likely fixed by config handling changes |

The critical Google OAuth issue (#3278) suggests an urgent compliance problem that could block all Antigravity provider users. No fix PR has been opened yet. The MCP hang (#3269) is also severe as it renders the chat interface unresponsive.

## 6. Feature Requests & Roadmap Signals

Today's activity reveals several clearly articulated feature requests that may shape the next release:

- **#3272 – Add Japanese localization to WebUI and Launcher** (open, PR #3273 already submitted by the same author). Localization is a strong signal for international adoption.  
  [Issue](https://github.com/sipeed/picoclaw/issues/3272) | [PR](https://github.com/sipeed/picoclaw/pull/3273)

- **#3276 – Launcher: support/detect externally-managed gateway (systemd)** — Headless deployment friction with the WebUI assuming ownership of the gateway lifecycle.  
  [Issue](https://github.com/sipeed/picoclaw/issues/3276)

- **#3270 – Add DashScope TTS provider and WeChat audio file sending** (open PR). Extends TTS support to Alibaba Cloud's DashScope/Bailian platform, plus audio integration for WeChat – likely targeting Chinese market users.  
  [PR](https://github.com/sipeed/picoclaw/pull/3270)

- **#3271 – Update default model names to 2026-07 latest** (open PR). Refreshes model lists for OpenAI, Anthropic, Google, etc.  
  [PR](https://github.com/sipeed/picoclaw/pull/3271)

- **#3229 – (Closed) Proposal: rolling conversation cache breakpoints for anthropic-messages** – Although closed, the request for granular cache control in agentic workloads indicates future demand for cost optimisation with Anthropic.  
  [Issue](https://github.com/sipeed/picoclaw/issues/3229)

**Prediction:** The next minor release will likely include the Japanese localization (PR #3273), updated default models (PR #3271), the DashScope TTS provider (PR #3270), and possibly the fixes for Antigravity regression (#3274) and config rewrite bug (already closed). The Launcher external gateway support (#3276) may follow soon.

## 7. User Feedback Summary

- **Pain points:**
  - *Mobile support*: User `Monessem` on Android cannot even start the service; the issue has seen no resolution in almost a month.
  - *Provider fragility*: Matrix users (`weissfl`) suffer silent agent death; Antigravity users (`honbou`) hit Google OAuth policy blocks and a regression that breaks tool calling; MCP server failures (`ruiyigen`) hang the entire chat.
  - *Configuration instability*: `honbou` reported that `model_list` entries lose API keys after WebUI config rewrites – a data-loss bug that undermines trust.

- **Use cases:**
  - *Agentic workflows with tool use*: Several bugs (Matrix sync, MCP hang, deferred tool visibility) directly impact tool-assisted AI agents, indicating heavy reliance on MCP and provider-agnostic tool calling.
  - *Headless server deployment*: `honbou` is running both gateway and launcher under systemd and wants better lifecycle management – typical of production, self-hosted setups.
  - *Internationalisation*: The Japanese localization request (and accompanying PR) reflects growing non-English user base.

- **Satisfaction/Dissatisfaction:**
  - Dissatisfaction is implied by the number of bugs and the absence of fixes for long-standing issues (Android, Matrix). The prompt closure of #3275 suggests responsive maintainers for recently reported bugs, but the backlog (see below) indicates some areas lag.

## 8. Backlog Watch

The following issues/PRs have been open for an extended period without maintainer resolution and may require attention:

- **#3182** – Android bug (open since June 26, 2026). 4 comments, no assignee. Critical for mobile users.  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3182)

- **#3203** – Matrix sync reconnection (open since July 2, 2026). Stale label, 1 👍, 3 comments.  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3203)

- **#3254** [PR] – `fix(agent): prefer verbatim model matches over provider-alias splits` (open since July 13, 2026, stale label). No recent comments. This fix improves model resolution logic and could be important

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-07-21

### 1. Today’s Overview
The project saw moderate activity with **6 new issues** and **20 pull requests** updated in the last 24 hours. All issues remain open, and six PRs were merged or closed — indicating a steady pace of bug fixing and feature refinement. The latest batch of changes focuses on **security hardening** (role management, approval routing), **WhatsApp Cloud migration stability**, and **inbound attachment handling** across multiple channels. No new releases were published today.

### 2. Releases
*None today.* The last release date is not recorded; no release artifacts were tagged in the past 24 hours.

### 3. Project Progress — Merged/Closed PRs
Six PRs were closed or merged, advancing several fixes and a feature:

- **#3110 — `feat(container): bake caldav-mcp into the agent image`**  
  [PR #3110](https://github.com/nanocoai/nanoclaw/pull/3110) (closed)  
  Pins the `caldav-mcp` MCP server (v0.8.0) into the container image, enabling the `/add-caldav-tool` skill.

- **#3108 — `fix(chat-sdk-bridge): rehydrate inbound attachments when adapters carry no fetchData`**  
  [PR #3108](https://github.com/nanocoai/nanoclaw/pull/3108) (closed)  
  Fixes a gap where inbound attachments without a `fetchData` function were silently dropped.

- **#3107 — `fix(add-whatsapp-cloud): copy the adoption module and document the row re-key`**  
  [PR #3107](https://github.com/nanocoai/nanoclaw/pull/3107) (closed)  
  Companion documentation and module copy for the WhatsApp Cloud instance re‑key fix (see #3106).

- **#3087 — `fix(whatsapp): engage mention-mode wirings on typed @-mentions in groups`**  
  [PR #3087](https://github.com/nanocoai/nanoclaw/pull/3087) (closed)  
  Fixes WhatsApp group @‑mention handling.

- **#1110 — `fix: update container-runtime tests to match implementation`**  
  [PR #1110](https://github.com/nanocoai/nanoclaw/pull/1110) (closed)  
  Updates tests to reflect current container runtime behaviour (uses `--mount` syntax, `system status` command).

- **#2642 — `fix(add-telegram): pin chat-adapter to 4.26.0 to match installed chat`**  
  [PR #2642](https://github.com/nanocoai/nanoclaw/pull/2642) (closed)  
  Resolves peer‑dependency version mismatch for Telegram channel adapter.

### 4. Community Hot Topics
The most active discussion centers on **privilege and approval security** — a cluster of four issues opened by the same author (`k-fls`) on 2026-07-20:

- **#3100 – “Revoking the sole remaining owner is not prevented”**  
  [Issue #3100](https://github.com/nanocoai/nanoclaw/issues/3100)  
  Highlights a critical root‑of‑trust vulnerability in the CLI `ncl roles revoke` handler.

- **#3099 – “Approval routing ignores privilege and can route a role-change to its own target”**  
  [Issue #3099](https://github.com/nanocoai/nanoclaw/issues/3099)  
  Self‑approval possible for role changes; higher‑privilege actions can be gated on lower‑privilege approvers.

- **#3098 – “Approval cards for ncl commands echo the raw command line, not the effect”**  
  [Issue #3098](https://github.com/nanocoai/nanoclaw/issues/3098)  
  Approval UI is opaque—admins see raw CLI strings instead of human‑readable change descriptions.

- **#3097 – “Role grant silently confers GLOBAL admin when --group is omitted”**  
  [Issue #3097](https://github.com/nanocoai/nanoclaw/issues/3097)  
  Accidental privilege escalation via missing `--group` flag.

All four issues have corresponding fix PRs opened by the same author on the same day, showing rapid community response.

### 5. Bugs & Stability
Several bugs were reported today, along with a high‑priority regression fix:

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| **#3105** (WhatsApp Cloud upgrade) | **High** – Silent data loss | Upgrading an existing install strands `messaging_groups` rows, silencing WhatsApp. | [#3106](https://github.com/nanocoai/nanoclaw/pull/3106) (open) |
| **#3100** (sole owner revocation) | **Critical** – Loss of administrative control | System becomes unmanageable if last owner is revoked. | [#3104](https://github.com/nanocoai/nanoclaw/pull/3104) (open) |
| **#3099** (approval routing) | **High** – Security bypass | Self‑approval of own role change possible. | [#3103](https://github.com/nanocoai/nanoclaw/pull/3103) (open) |
| **#3097** (global admin by default) | **Medium** – Privilege escalation | Missing `--group` grants global admin unintentionally. | [#3101](https://github.com/nanocoai/nanoclaw/pull/3101) (open) |
| **#3098** (unclear approval cards) | **Low** – UX / audit | Admins cannot evaluate impact before approving. | [#3102](https://github.com/nanocoai/nanoclaw/pull/3102) (open) |
| **#3044** (inbound attachments) | **Medium** – Feature regression | Telegram voice/audio notes lost bytes. | [#3108](https://github.com/nanocoai/nanoclaw/pull/3108) (merged) |

All bug reports from today already have fix PRs under review, indicating strong maintainer engagement.

### 6. Feature Requests & Roadmap Signals
Two notable feature‑skill PRs continue to gather attention:

- **#2918 – LINE Official Account channel**  
  [PR #2918](https://github.com/nanocoai/nanoclaw/pull/2918) (open since 2026-07-03)  
  Adds native LINE adapter + `/add-line` skill. The companion issue `#3096` (opened today) formalises the RFS process. This is a strong candidate for the next minor release given LINE’s market share in Asia.

- **#3041/#3050 – Dial channel (SMS + AI voice calls)**  
  [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) and [PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) (open since 2026-07-14)  
  Adds a new channel adapter for SMS and voice calls via Dial. Wizard integration is included.

- **#2459 – Voice transcription via whisper.cpp**  
  [PR #2459](https://github.com/nanocoai/nanoclaw/pull/2459) (open since 2026-05-13)  
  Local on‑device transcription for all Chat SDK channels. Still awaiting review.

- **#3060 – Container zombie process reaping**  
  [PR #3060](https://github.com/nanocoai/nanoclaw/pull/3060) (open since 2026-07-16)  
  Production‑grade container fix to add `--init` for PID 1 zombie reaping.

### 7. User Feedback Summary
Community pain points expressed today centre on **security defaults** and **upgrade safety**:

- *“Silent privilege escalation”* – Users report that `ncl roles grant` without explicit scope is too permissive (multiple issues from `k-fls`).
- *“Upgrade breaks WhatsApp”* – The WhatsApp Cloud re‑key (#2913) left existing installs with orphaned rows, causing silent failure (glifocat).
- *“Approval workflow is blind”* – Admins cannot tell what a role‑change command actually does before approving (k-fls).
- *“Inbound attachments lost on Telegram”* – Voice/audio notes fail to deliver bytes to the agent (mashkovtsevlx, now fixed with #3108).

Overall satisfaction is tempered by these regressions, but the rapid PR turnaround (same‑day fixes) is positively noted.

### 8. Backlog Watch
Several older, important PRs have stagnated and need maintainer attention:

- **#2459 – Voice transcription (whisper.cpp)** – open since 2026-05-13, no maintainer comments.  
  [PR #2459](https://github.com/nanocoai/nanoclaw/pull/2459)

- **#2950 – Traditional Chinese README** – open since 2026-07-04, awaiting merge.  
  [PR #2950](https://github.com/nanocoai/nanoclaw/pull/2950)

- **#3060 – Container zombie reaping (`--init`)** – open since 2026-07-16, one review cycle pending.  
  [PR #3060](https://github.com/nanocoai/nanoclaw/pull/3060)

- **#3044 – Inbound attachment fix** (origin #2888) – open since 2026-07-14, now superseded by the merged #3108 but the original PR still shows as open. Should be closed to avoid confusion.  
  [PR #3044](https://github.com/nanocoai/nanoclaw/pull/3044)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-21

## Today’s Overview
NullClaw’s development activity remains minimal over the past 24 hours, with no new issues, no releases, and only a single open pull request. The project appears to be in a maintenance lull, with no user-reported bugs, feature requests, or community discussions recorded. The only change in flight is a routine dependency update from Dependabot, suggesting that core development has paused or shifted focus. Overall project health is stable but stagnant, with little visible forward momentum.

## Releases
No new releases were published in the last 24 hours. The latest release history is empty.

## Project Progress
No pull requests were merged or closed today. The only open PR (#956) remains unmerged and has not been updated since its creation on 2026-06-15.

## Community Hot Topics
No issues or pull requests generated significant discussion or reactions in the last 24 hours. The sole open PR (#956) has zero comments and zero thumbs-up.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. No stability-related issues are currently open.

## Feature Requests & Roadmap Signals
No user-submitted feature requests were recorded. Without recent issues or discussions, it is not possible to predict upcoming features. The next version’s content remains unknown.

## User Feedback Summary
No user feedback—positive or negative—was captured in the last 24 hours. No pain points or use case discussions are visible in the tracked data.

## Backlog Watch
- **PR #956** — [dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group  
  *Author:* dependabot[bot] | Created: 2026-06-15 | Updated: 2026-07-20  
  *Link:* [nullclaw/nullclaw PR #956](https://github.com/nullclaw/nullclaw/pull/956)  
  This routine dependency update has been open for over a month without being merged or reviewed. While not critical, it could indicate that maintainer bandwidth is low or that the PR is blocked. Maintainer attention is recommended to keep the Docker image up‑to‑date.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

## IronClaw Project Digest — 2026-07-21

### 1. Today’s Overview

The IronClaw project remains in a phase of intense architectural refactoring, with **43 issues updated** and **50 PRs updated** in the last 24 hours. The headline event is the deletion of the v1 legacy monolith (`src/`) under Tier‑B, with production deploys now repointed to the Reborn stack. Alongside this, the team merged or closed **28 PRs**—including critical fixes for streaming resilience, feature‑flag cleanup, and a hotfix for a broken `main` after the v1 removal. Bug bash reports dominate the issue tracker, with 20+ P2/P1 bugs filed in the last day alone. The project is healthy but very busy; stability bugs are being triaged quickly, and the core team is delivering large‑scale refactors (XL‑sized PRs) at a high cadence.

### 2. Releases

No new releases were published today. The last tagged release remains pending the `ironclaw-v1.0.0-rc.1` tag, which is being prepared in PR [#6383](https://github.com/nearai/ironclaw/pull/6383).

### 3. Project Progress

The following **28 PRs were merged or closed** today. Key highlights:

- **Tier‑B v1 deletion**: [#6375](https://github.com/nearai/ironclaw/pull/6375) (XL, high risk) completely removed the legacy `src/` monolith and cut deploy configs over to Reborn.
- **Deployment simplification**: [#6374](https://github.com/nearai/ironclaw/pull/6374) eliminated `local_trigger_access` (~1,464 LOC), and [#6387](https://github.com/nearai/ironclaw/pull/6387) shrank the deployment‑mode branching ratchet from 5→3 files.
- **Streaming & retry fixes**: [#6337](https://github.com/nearai/ironclaw/pull/6337) (M) fixed chat streams to stay active without replay; [#6376](https://github.com/nearai/ironclaw/pull/6376) (L) added streaming retry resilience coverage.
- **Feature‑flag cleanup**: [#6378](https://github.com/nearai/ironclaw/pull/6378) removed dead `libsql-secrets` and `filesystem-goal-store` features; [#6377](https://github.com/nearai/ironclaw/pull/6377) removed the `libsql-secrets` module.
- **Security milestone**: [#6386](https://github.com/nearai/ironclaw/pull/6386) consolidated all pre‑flight policy into `authorize()`.
- **Build fixes**: [#6379](https://github.com/nearai/ironclaw/pull/6379) repaired `main` after a `release-plz` failure caused by deleted packages.
- **Release preparation**: [#6370](https://github.com/nearai/ironclaw/pull/6370) prepared changelog for 1.0.0‑rc.1; [#6383](https://github.com/nearai/ironclaw/pull/6383) stripped “Reborn” codename from release notes and fixed an MSI blocker.
- **Dependency bumps**: Several batches updated serde, tokio, agent‑client‑protocol, and 60+ other crates ([#6288](https://github.com/nearai/ironclaw/pull/6288), [#6385](https://github.com/nearai/ironclaw/pull/6385), [#6361](https://github.com/nearai/ironclaw/pull/6361), [#6380](https://github.com/nearai/ironclaw/pull/6380), [#5664](https://github.com/nearai/ironclaw/pull/5664)).

### 4. Community Hot Topics

The issues with the most engagement in the last 24 hours reveal a heavy focus on **store consolidation** and **bug bash regressions**:

- **[#6263](https://github.com/nearai/ironclaw/issues/6263)** – *§4.3 final store consolidation: retire InMemoryTurnStateStore* (9 comments)  
  This is the last DEBT item in the `InMemory*Store` ratchet. Discussion centers on Slice 0 oracle evidence and livelock avoidance. It’s a blocking refactoring for core maintainers.

- **[#6274](https://github.com/nearai/ironclaw/issues/6274)** – *Finish DeploymentConfig as the main composition config* (4 comments)  
  The team is debating how to complete adoption of `DeploymentConfig` as the single sanctioned place for profile‑to‑deployment mapping. Track 1 PR [#6387](https://github.com/nearai/ironclaw/pull/6387) already contributed.

- **[#6190](https://github.com/nearai/ironclaw/issues/6190)** and **[#6189](https://github.com/nearai/ironclaw/issues/6189)** – *Multiple conflicting error messages* and *Retryable stream error leaves completed response in failed state* (4 comments each)  
  Both are P2 bug bash reports highlighting fundamental confusion in the chat error/stream UX. Users are seeing banners for “streaming error” and “model context limit” simultaneously, or a green response paired with a red error banner.

- **[#6369](https://github.com/nearai/ironclaw/issues/6369)** – *Tier B follow-up: gaps left by v1 retirement* (3 comments)  
  A tracking issue for capabilities lost when `src/` was deleted—production configs, CI artifacts, and a missing libSQL restart mechanism.

The underlying need is clear: the community (including bug bash testers) wants a **reliable, predictable chat experience** and a **clean migration path** from the old architecture to Reborn without silent failures.

### 5. Bugs & Stability

A wave of **P1/P2 bugs** was filed yesterday (2026-07-20), mostly by Joe R.L.O. and italic-jinxin. No immediate fix PRs have been linked for most, but several overlap with recent streaming fixes (e.g., PR [#6337](https://github.com/nearai/ironclaw/pull/6337) likely addresses some replay issues).

| Severity | Issue                                                                 | Description                                                                 | Fix PR? |
|----------|-----------------------------------------------------------------------|-----------------------------------------------------------------------------|---------|
| P1       | [#6360](https://github.com/nearai/ironclaw/issues/6360)               | Provider onboarding CLI has no back navigation – users can’t switch provider after selecting one. | None yet |
| P1       | [#6348](https://github.com/nearai/ironclaw/issues/6348)               | Gmail extension re‑installs automatically grant OAuth without user consent (security concern). | None yet |
| P2       | [#6350](https://github.com/nearai/ironclaw/issues/6350)               | Assistant switches response language unexpectedly (e.g., English prompt → Ukrainian response). | None yet |
| P2       | [#6351](https://github.com/nearai/ironclaw/issues/6351)               | Checkpoint unavailable/unreachable errors on multi‑tool requests.                           | None yet |
| P2       | [#6353](https://github.com/nearai/ironclaw/issues/6353)               | Long assistant messages truncated without expansion option.                                 | None yet |
| P2       | [#6352](https://github.com/nearai/ironclaw/issues/6352)               | Streamed response replays in a loop when returning to a chat page.                          | Possibly [#6337](https://github.com/nearai/ironclaw/pull/6337) |
| P2       | [#6349](https://github.com/nearai/ironclaw/issues/6349)               | Telegram chat history rendered inconsistently in WebUI.                                     | None yet |
| P2       | [#6347](https://github.com/nearai/ironclaw/issues/6347)               | Slack instance‑readiness lacks caller‑level test coverage.                                  | None yet |
| P2       | [#6190](https://github.com/nearai/ironclaw/issues/6190)               | Multiple conflicting error messages for a single failed request.                            | None yet |
| P2       | [#6189](https://github.com/nearai/ironclaw/issues/6189)               | Retryable stream error leaves completed response in failed state.                           | None yet |

Additionally, three bugs were closed: [#6335](https://github.com/nearai/ironclaw/issues/6335) (host‑authored capability remediation silently placeholder’d), [#6178](https://github.com/nearai/ironclaw/issues/6178) (automation error banner undismissable), and [#6179](https://github.com/nearai/ironclaw/issues/6179) (settings import reports success when nothing imported).

### 6. Feature Requests & Roadmap Signals

Several enhancement issues were filed by core maintainers (ilblackdragon) that point toward the **next Reborn‑native features**:

- **[#6320](https://github.com/nearai/ironclaw/issues/6320)** – *IronHub extension install flow* (tracking #4479). Enables user discovery, install, and activation of extensions through Reborn surfaces.
- **[#6324](https://github.com/nearai/ironclaw/issues/6324)** – *WebUI workspace redesign and chat‑first onboarding* (tracking #6162/#6163).
- **[#6325](https://github.com/nearai/ironclaw/issues/6325)** – *Thread‑scoped MCP sessions and programmatic MCP config* (tracking #6244).
- **[#6334](https://github.com/nearai/ironclaw/issues/6334)** – *Improve Workspace tree navigation and accessibility* (keyboard, ARIA).

All are tagged as `enhancement` and `scope: webui` / `scope: tool/mcp` / `scope: extensions`. Given the high velocity of Reborn refactoring, these are likely candidates for the **1.0.0‑rc.1 or 1.0.0** release.

### 7. User Feedback Summary

Bug bash reports from Joe R.L.O., italic-jinxin, and others paint a picture of **real user pain points**, especially around chat reliability and configuration flows:

- **Error UX confusion** – Users see multiple error banners for the same failure, or a successful response with a “retryable error” message.
- **Stream unreliability** – Streams replay on page return, responses are truncated, and Telegram conversations render incorrectly in WebUI.
- **Provider onboarding friction** – No back navigation, duplicate “Test connection” / “Fetch models” buttons, and no way to switch providers mid‑flow.
- **Security / consent concerns** – Gmail extension automatically re‑authorizes after reinstall without user consent.
- **Language switching** – The assistant occasionally responds in a different language than the user’s input, with no discernible cause.

No positive feedback is captured in this data, likely due to the nature of the bug bash event. The team should prioritize fixing the P1 security/anxiety issues (#6348) and the P2 stream‑related regressions before the next user‑facing release.

### 8. Backlog Watch

The following important items have been open for an extended period without recent maintainer action:

- **[#2277](https://github.com/nearai/ironclaw/issues/2277)** – *V2: ACP‑backed child thread backends for delegated external agents* (created 2026-04-10, 2 comments, 1 👍). This feature request for delegating work to Codex / Droid / OpenCode has been idle for 3+ months. With the v1 deletion now complete, the team may consider advancing this.

- **[#5598](https://github.com/nearai/ironclaw/pull/5598)** – *chore: release* (open since 2026-07-03, no comments). A release PR that appears to have stalled; it was likely superseded by the separate 1.0.0‑rc.1 workflow.

- **[#5664](https://github.com/nearai/ironclaw/pull/5664)** – *deps: bump actions group* (open since 2026-07-05). A large CI dependency bump that may be held up by breaking changes (e.g., `actions/checkout` v4→v7). It has no comments from maintainers.

- **[#6263](https://github.com/nearai/ironclaw/issues/6263)** – *§4.3 final store consolidation* (open since 2026-07-19, 9 comments). While actively discussed, there is no assignee or linked PR yet. It remains the highest‑priority refactoring debt.

Maintainers should review these items to unblock the release pipeline and ensure no critical feature requests are abandoned.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-21

## Today's Overview
Project activity was moderate, with 15 pull requests updated in the last 24 hours, 10 of which were merged or closed. No new issues were reported, and no releases were published. Development focused on the **Cowork** collaboration module (multi‑annotation support, scroll/jump fixes, IM flicker repair) and the **Windows** build pipeline (silent updates, explicit channel entry points). Three longstanding dependency‑bump PRs from Dependabot remain open, indicating a possible backlog in routine maintenance. Overall, the project appears stable with a steady flow of bug fixes and incremental feature work.

## Releases
*None* — no new releases were tagged on this date.

## Project Progress
All merged/closed PRs from the last 24 hours are listed below. The most significant changes include:

- **Silent Windows updates** (PR #2368 – open, not merged yet) – Launches the NSIS installer via PowerShell with `/S` flag, handles UAC decline gracefully, and restarts the app automatically.
- **Build channel improvements** (PR #2367 – closed) – Added explicit entry points for Windows dist builds to isolate environment variables per build.
- **Browser multi‑annotation in Cowork** (PR #2366 – closed) – Introduced a protocol for browser comments, webview preload, screenshot asset storage, and a badge indicator for annotation count. Includes design docs and test coverage.
- **Config hot‑reload via RPC** (PR #2365 – closed) – Delivers configuration changes through an acknowledgment mechanism instead of file polling.
- **AI skin creation flow** (PR #2361 – closed) – Added a persistent AI skin creation entry in Appearance settings, first‑use onboarding, and a framework prompt for the AI Skin Designer.
- **Bug fixes:**
  - Prevent scroll jumps on session refresh (PR #2364 – closed)
  - Fix periodic IM message flicker (PR #2363 – closed)
  - Preserve local callback across login retries (PR #2360 – closed)
  - Keep preview panel and input area layout stable (PR #2359 – closed)
  - Fix cron UI bug (PR #2362 – closed)
  - Add real API validation for POPO connectivity test (PR #1349 – closed, stale update)

## Community Hot Topics
No issues were updated in the last 24 hours, and none of the PRs received comments or reactions (all `undefined` / `0`). The most visible community‑fueled items are the **Dependabot dependency‑bump PRs** that remain open after several months:

- [#1277] `chore(deps-dev): bump the electron group` – updates `electron` from 40.2.1 to 43.1.1 and `electron-builder`. Open since April 2026.
- [#1282] `chore(deps): bump @headlessui/react` from 1.7.19 to 2.2.9. Open since April.
- [#1283] `chore(deps): bump react` from 18.3.1 to 19.2.4. Open since April.
- [#1284] `chore(deps): bump react-syntax-highlighter` from 15.6.6 to 16.1.1. Open since April.

The lack of community discussion suggests users may be satisfied with the current pace or are more active on other channels. The stale Dependabot PRs hint at a need for maintainer prioritization of dependency upgrades.

## Bugs & Stability
Several bugs were fixed in the latest round of PRs. No new bugs were reported as issues. The fixes are ranked by perceived impact:

| Severity | Bug Description | Fixed In |
|----------|----------------|----------|
| **Medium** | Cowork session refresh caused scroll jumps | PR #2364 |
| **Medium** | Periodic IM message flicker due to reconciliation window mismatches | PR #2363 |
| **Medium** | Auth callback lost across login retries | PR #2360 |
| **Low** | Layout flicker when toggling artifact preview panel | PR #2359 |
| **Low** | Cron UI rendering bug (not described in detail) | PR #2362 |
| **Low** | POPO connectivity test falsely showing success (fixed earlier, updated now) | PR #1349 |

No critical crashes or regressions were reported. The project’s stability appears healthy.

## Feature Requests & Roadmap Signals
Based on the merged/open PRs, the following features are shaping the near‑term roadmap:

- **Enhanced Cowork collaboration** – Multi‑annotation support in the built‑in browser (PR #2366) is a significant UX improvement for collaborative browsing sessions. Likely to be included in the next minor release.
- **AI‑driven skin customization** – The new persistent AI skin creation flow (PR #2361) adds a dedicated user journey, suggesting the team is investing in AI‑assisted personalisation.
- **Windows silent updates** – PR #2368 (still open) will allow automatic, non‑interactive updates on Windows – a quality‑of‑life improvement for enterprise and power users.
- **Build pipeline hardening** – Explicit channel entry points (PR #2367) indicate a focus on reproducible and clean builds for different distribution channels.

User‑requested features (e.g., in issues) are absent from this day’s data, so no external requests can be cited. It is plausible that the multi‑annotation feature was driven by internal or beta‑user feedback.

## User Feedback Summary
No direct user feedback (comments, reactions, or issue descriptions) was captured in the last 24 hours. The absence of new issues suggests that users are either not encountering major problems or are reporting through other channels (e.g., GitHub Discussions, private support). The bug fixes targeting layout jumps, flicker, and auth retries address pain points that users may have experienced in previous builds.

## Backlog Watch
The following PRs and issues require maintainer attention, having been open for over three months:

- [#1277] **chore(deps-dev): bump the electron group** – Open since April 2, 2026. Blocks major Electron upgrade (40 → 43). [Link](https://github.com/netease-youdao/LobsterAI/pull/1277)
- [#1282] **chore(deps): bump @headlessui/react** – Open since April 2, 2026. Major version jump from 1.x to 2.x with potential breaking changes. [Link](https://github.com/netease-youdao/LobsterAI/pull/1282)
- [#1283] **chore(deps): bump react** – Open since April 2, 2026. Upgrading React from 18 to 19 may require compatibility testing. [Link](https://github.com/netease-youdao/LobsterAI/pull/1283)
- [#1284] **chore(deps): bump react-syntax-highlighter** – Open since April 2, 2026. [Link](https://github.com/netease-youdao/LobsterAI/pull/1284)

These Dependabot PRs have accumulated no maintainer activity (no review, no close) and represent a growing technical debt. A review session to merge or adjust them (especially React 19 and Headless UI 2) would reduce future integration risk.

*No other long‑unanswered issues were observed in the 24‑hour window.*

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

# CoPaw Project Digest — 2026-07-21

## 1. Today's Overview

Project activity remains very high, with **30 issues** (22 open, 8 closed) and **42 pull requests** (32 open, 10 merged/closed) updated in the last 24 hours. No new releases were published. The community is actively reporting bugs around multi-tool reasoning, agent loops, and memory stability, while several major feature PRs—including a unified browser engine, per-session model overrides, and an AIOnly model provider—are under review. The volume of concurrent discussions indicates a healthy but slightly overloaded development cycle, with maintenance bandwidth being tested by numerous edge-case crashes.

---

## 2. Releases

None. No new versions were tagged in the reporting period.

---

## 3. Project Progress

**Merged/closed PRs today (10 total):**

| PR | Title | Type |
|----|-------|------|
| [#6150](https://github.com/agentscope-ai/QwenPaw/pull/6150) | feat(pawapp): add pawapp sdk and kanban app | Feature – merged |
| [#6235](https://github.com/agentscope-ai/QwenPaw/pull/6235) | feat(memory): enhance ReMe Light index maintenance stability and chunking | Feature – merged |
| [#6210](https://github.com/agentscope-ai/QwenPaw/pull/6210) | refactor: make the default loop an agent mode | Refactor – merged |
| [#5922](https://github.com/agentscope-ai/QwenPaw/pull/5922) | feat(observability): track user/session/version on langfuse traces | Feature – merged |
| [#6151](https://github.com/agentscope-ai/QwenPaw/issues/6151) | refactor(tool_calls): background tool call offload mechanism with frontend controls | Refactor – open (not closed) |
| [#6203](https://github.com/agentscope-ai/QwenPaw/issues/6203) | fix(utils): bound and hide the Windows tasklist liveness probe | Fix – open |
| [#6187](https://github.com/agentscope-ai/QwenPaw/issues/5187) | feat(computer-use): Windows desktop GUI automation | Feature – open |
| [#5992](https://github.com/agentscope-ai/QwenPaw/issues/5992) | Add per-session model overrides | Feature – open |
| [#6041](https://github.com/agentscope-ai/QwenPaw/issues/6041) | fix(loop): exempt read-only tools from doom loop detection | Fix – open |
| [#6238](https://github.com/agentscope-ai/QwenPaw/issues/6238) | perf(drivers): initialize handlers concurrently | Performance – open |

**Key closed features:**
- **PawApp SDK** (`pawapp` + Kanban app) is now merged, enabling a plugin ecosystem for custom agent applications.
- **ReMe Light memory** received major stability enhancements: index rebuilds are now explicit operations, chunking improved, and concurrent write protection added.
- **Observability** now propagates `user_id`, `session_id`, and version to Langfuse, and fixes trace ID formatting.
- **Default loop** is now a proper agent mode, cleaning up lifecycle ownership.

---

## 4. Community Hot Topics

The most active discussions (by comment count) in the last 24 hours:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#6257](https://github.com/agentscope-ai/QwenPaw/issues/6257) | 13 | Multiple tool calls produce identical thinking output – each call’s reasoning block is a copy. High interest. |
| [#5961](https://github.com/agentscope-ai/QwenPaw/issues/5961) (closed) | 8 | v2.0.0 loop execution bug: agent repeatedly writes/deletes files, never completing tasks. |
| [#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873) | 5 | Two subagents spawn infinite polling loop; cannot interrupt from Feishu. |
| [#5958](https://github.com/agentscope-ai/QwenPaw/issues/5958) (closed) | 4 | Question about integrating AgentScope permission control in QwenPaw. |

**Underlying needs:**
- **Thinking consistency**: Users expect independent reasoning per tool call, not shared boilerplate.
- **Loop detection reliability**: The project’s “doom loop” gate has false positives/negatives; multiple issues report infinite cycles without termination.
- **Subagent concurrency**: Background task orchestration needs better serialization and interrupt handling, especially from messaging channels.
- **Permission governance**: Enterprise users want fine-grained tool-level approval, not a blanket `NONE` setting.

---

## 5. Bugs & Stability

**Critical severity:**
- **[#6241](https://github.com/agentscope-ai/QwenPaw/issues/6241)** – Agent continuously repeats identical output; `memory_search` enters infinite loop. Framework lacks duplicate detection enforcement. **No fix PR filed yet.**
- **[#6257](https://github.com/agentscope-ai/QwenPaw/issues/6257)** – Identical thinking blocks across multiple tool calls corrupts reasoning. **Fix PR [#6280](https://github.com/agentscope-ai/QwenPaw/pull/6280)** submitted by `wananing`.
- **[#6282](https://github.com/agentscope-ai/QwenPaw/issues/6282)** – Reasoning relay repeats the first thinking block across AgentScope 2 tool iterations. **PR [#6280](https://github.com/agentscope-ai/QwenPaw/pull/6280)** addresses this.
- **[#6197](https://github.com/agentscope-ai/QwenPaw/issues/6197)** – QwenPaw Desktop (frozen binary) hangs on startup when `nvidia-smi` hangs indefinitely. No fix PR.

**High severity:**
- **[#6246](https://github.com/agentscope-ai/QwenPaw/issues/6246)** – `recall_history` crashes with “File name too long” due to oversized saved tool references. Closed via fix.
- **[#6255](https://github.com/agentscope-ai/QwenPaw/issues/6255)** – Chat error `BadRequestError: invalid_parameter_error` during conversation. Closed.
- **[#6239](https://github.com/agentscope-ai/QwenPaw/issues/6239)** – Windows PATH concatenation drops semicolons, breaking npm globals for child processes. No fix PR.
- **[#6273](https://github.com/agentscope-ai/QwenPaw/issues/6273)** – Unclear task tracking and same-session concurrency semantics; behavior varies by entry point. No fix PR.

**Medium severity:**
- **[#6242](https://github.com/agentscope-ai/QwenPaw/issues/6242)** – Console embedding dimensions not sent to OpenAI-compatible APIs because `use_dimensions` is not exposed. No fix PR.
- **[#6252](https://github.com/agentscope-ai/QwenPaw/issues/6252)** – Ctrl++/mouse wheel zoom not working on Linux Tauri desktop. No fix PR.
- **[#6261](https://github.com/agentscope-ai/QwenPaw/issues/6261)** – Offline environments cannot preview files because of online resource dependency. No fix PR.
- **[#6250](https://github.com/agentscope-ai/QwenPaw/issues/6250)** – Sandbox fallback hardcoded to ask for approval; no configurable bypass. Closed via workaround (`approval_level: NONE`).
- **[#6258](https://github.com/agentscope-ai/QwenPaw/issues/6258)** – OpenAI max output token setting not applied. No fix PR.

**Notable regressions:**  
- The reasoning/tool-segment duplication bug ([#6282](https://github.com/agentscope-ai/QwenPaw/issues/6282)) appears to be a regression introduced during the AgentScope 2.0 lifecycle-hook migration.

---

## 6. Feature Requests & Roadmap Signals

**Most requested features (by recency and votes):**

| Issue | Request | Predict Next Release |
|-------|---------|---------------------|
| [#6287](https://github.com/agentscope-ai/QwenPaw/issues/6287) | Session grouping/folder support in Desktop sidebar | Medium – low complexity, high UX value |
| [#6286](https://github.com/agentscope-ai/QwenPaw/issues/6286) | Option to disable/customize built-in tool descriptions (save 8–10k tokens) | High – token consumption is a recurring complaint |
| [#6285](https://github.com/agentscope-ai/QwenPaw/issues/6285) | Add `qwen3.8-max-preview` to Aliyun model list | High – trivial update, partner request |
| [#6283](https://github.com/agentscope-ai/QwenPaw/issues/6283) | Auto-attach current timestamp to LLM context to fix date confusion | Medium – important for long-lived sessions |
| [#6274](https://github.com/agentscope-ai/QwenPaw/issues/6274) | New `ask_user_question` tool for Human-in-the-Loop | High – multiple 👍, aligns with permission governance |
| [#6268](https://github.com/agentscope-ai/QwenPaw/issues/6268) / [PR #6271](https://github.com/agentscope-ai/QwenPaw/pull/6271) | Add AIOnly as built-in model provider (190+ models) | Very High – PR already under review |
| [#6281](https://github.com/agentscope-ai/QwenPaw/issues/6281) | Web console mobile adaptation | Medium – growing mobile usage |
| [#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260) | Collapse thinking/tool-call output to focus on results | High – UX pain point |
| [#6264](https://github.com/agentscope-ai/QwenPaw/issues/6264) | Minimize to system tray | Low – nice-to-have |
| [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) | Per-session model overrides | High – large PR, complex, likely next or after |
| [#6157](https://github.com/agentscope-ai/QwenPaw/pull/6157) | Chrome extension plugin for browser control | Medium – depends on unified browser PR |
| [#6276](https://github.com/agentscope-ai/QwenPaw/pull/6276) | Unified browser – one SDK, any backend | High – major architecture change |
| [#6284](https://github.com/agentscope-ai/QwenPaw/pull/6284) | QwenPaw Creator app (script→video workflow) | Medium – new plugin type |

**Roadmap signals:**  
The project is clearly investing in a plugin/app ecosystem (`pawapp`, Kanban, Creator), a unified browser stack, and model provider flexibility (AIOnly). Token optimization and human-in-the-loop patterns are emerging as key community demands.

---

## 7. User Feedback Summary

**Pain points (repeated across multiple issues):**
- **Thinking/output duplication** – Users are frustrated that reasoning blocks are identical across tool calls, making debugging and review confusing.
- **Infinite loops** – Agents stalling in write/delete cycles or polling loops remain a top complaint.
- **Token waste** – Built-in tool descriptions consume 8k–10k tokens per request, even for unused tools.
- **Offline limitations** – File preview and code mode depend on online CDNs, breaking air-gapped deployments.
- **Mobile/UI** – Lack of mobile web console, no zoom on Linux, no session folders, output not collapsible.
- **Memory confusion** – Users are unclear on the roles of `MEMORY.md` vs Dream digest vs ReMe Light.

**Satisfaction signals:**
- Active community submits detailed bug reports and feature suggestions, indicating high engagement.
- Multiple first-time-contributor PRs (e.g., [#6203](https://github.com/agentscope-ai/QwenPaw/issues/6203), [#6041](https://github.com/agentscope-ai/QwenPaw/issues/6041), [#5992](https://github.com/agentscope-ai/QwenPaw/issues/5992)) suggest the project is welcoming to newcomers.
- Users appreciate the rapid iteration: v2.0.0.post3 and v2.0.1b1 are already in use, and many bugs are being addressed quickly.

**Sentiment:** Generally positive but impatient about stability. “Works great until it enters a loop” is a common theme.

---

## 8. Backlog Watch

The following items have been open for a concerning period without clear resolution:

| Item | Age | Issue |
|------|-----|-------|
| [#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873) | 50 days (since June 1) | Subagent infinite polling loop; no maintainer response in last 24h. **High priority** for Feishu/DingTalk users. |
| [#5688](https://github.com/agentscope-ai/QwenPaw/issues/5688) | 20 days (since July 1) | CSS selector prefix mismatch between `ant-` and `qwenpaw-` – likely many styles not applying. **Needs maintainer confirmation.** |
| [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) | 37 days (since June 14) | Windows desktop GUI automation PR – no comments or updates in last 24h. **Stalled feature.** |
|

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-21

## 1. Today's Overview

ZeroClaw is in a period of **high activity**: 39 issues and 50 pull requests were updated in the last 24 hours, with **9 issues closed** and **12 PRs merged or closed**. The team is making strong progress on the **agent evaluation harness** (`zeroclaw eval`, #7065), the **SOP control plane** (#8581, #8288), and **cross‑platform compatibility** (#7462). Several critical bugs were reported and are being addressed immediately (e.g., #9206, #9204). No new releases were published; the project is currently iterating toward the next milestone (0.8.x / 0.9.0).

---

## 2. Releases

*None in the reporting period.*

---

## 3. Project Progress

**Closed Issues (24h):**  
- [#9117] [Bug]: ZeroCode won't start on Windows without `ZEROCLAW_SOCKET`  
- [#8837] [Bug]: History trimming occurs silently with pruning disabled  
- [#9078] [Bug]: Serial transport desynchronized after non‑matching response ID  
- [#9079] [Feature]: Add CI coverage for shared firmware protocol crate  
- [#8675] [Bug]: Malformed native tool‑call arguments sent to OpenRouter/OpenAI → 400 → empty reply  
- [#8664] [Bug]: ZeroCode code‑block Copy includes Markdown fences  
- [#8644] [Bug]: ZeroCode can complete a Code turn with no visible assistant output  
- [#8765] [Bug]: ZeroCode queue/session picker overlays inherit terminal background  
- [#8944] [Bug]: ZeroCode transcript mouse copy blocks word‑level text selection  

**Merged/Closed PRs (12 total, details not all shown):**  
Key areas advanced include **SOP ingress wiring** (#9203), **shared budget atomicity fix** (#9201), **tool‑schema deep‑clone elimination** (#9208), and the beginning of the **eval harness feature series** (#9220–#9224). Several documentation and CI refinements (#8986, #9055, #9211) also landed.

---

## 4. Community Hot Topics

| Issue / PR | Comments | Topic & Underlying Need |
|------------|----------|--------------------------|
| [#6808] RFC: Work Lanes, Board Automation, Label Cleanup | 14 | Governance RFC for reducing maintainer manual overhead. Need for structured workflow routing. |
| [#7462] [Bug]: 74 test failures on Windows | 10 | Cross‑platform CI gap; Windows users blocked. Underlying need for true multi‑OS support. |
| [#3566] [Feature]: A2A (Agent‑to‑Agent) Protocol Support | 9 (👍7) | Interoperability with other agent frameworks (NanoClaw, OpenClaw). High community demand. |
| [#8891] [Tracker]: Persistent memory to parity | 6 | Core infrastructure for cross‑session memory, critical for long‑running agents. |
| [#9117] [Bug]: ZeroCode Windows startup (closed) | 5 | Quick fix for Windows onboarding friction. |
| [#7065] [Feature]: Agent evaluation harness | 4 | Foundational for quality assurance; spawned multiple follow‑ups (#9228, #9227, #9226). |
| [#8581] feat(sop): centralized SOP ingress adapters | 4 | Enables reliable fan‑in from multiple sources (AMQP, HTTP, etc.) — architectural alignment. |

*Links:* [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808), [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462), [#3566](https://github.com/zeroclaw-labs/zeroclaw/issues/3566), [#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891), [#9117](https://github.com/zeroclaw-labs/zeroclaw/issues/9117), [#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065), [#8581](https://github.com/zeroclaw-labs/zeroclaw/issues/8581)

---

## 5. Bugs & Stability

### New Bugs Reported (Last 24h)

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#9206] Cron job `workspace_dir` resolves to `/` on intermittent runs | **S0** (data loss / security risk) | Agent workspace can be the root filesystem. | No |
| [#9204] Landlock sandbox locks zeroclaw itself | **S1** (workflow blocked) | Subprocesses inheriting Landlock policy cause crashes and DB access failures. | No |
| [#9207] `web_fetch` returns garbage for compressed responses | **S1** (workflow blocked) | Sites using gzip/brotli return binary data; agents cannot parse. | No |
| [#9192] `shared_budget` TOCTOU wrap; `finish_run` mutex panic | **S1** (workflow blocked) | Concurrent parent/subagent turns can underflow budget or panic. | ✅ [#9201] |
| [#9216] Comment‑hygiene gate fails on master due to issue refs in comments | **S1** (workflow blocked) | CI gate broken; blocks all PRs. | No (tracked) |
| [#9198] Discord typing indicator stuck after daemon reload | **S3** (minor) | UI issue after web dashboard reload. | No |
| [#9202] `zeroclaw desktop` command uses dead URL, misses installed AppImage | **S3** (minor) | Linux detection broken. | No |

**Trend:** The Windows testing gap (#7462) and the new S0/S1 bugs indicate ongoing stability challenges, but the team is actively shipping fixes (e.g., #9201, #9208, #9203). The tool‑schema deep‑clone removal (#9208) should improve runtime performance for agent loops.

---

## 6. Feature Requests & Roadmap Signals

**Strongest signals for next release (0.8.x / 0.9.0):**

- **Agent Evaluation Harness** (#7065) — Follow‑ups for dashboard (#9228), LLM‑judge calibration (#9227), and memory seeding (#9226) suggest this is a flagship feature near completion.
- **SOP Milestone** (#8288) — PRs #9205 and #9203 advance the daemon‑owned control plane; fan‑in adapters are being centralised.
- **ACP Embedded Resource Blob** (#9178) — Allows agents to return files as ACP embedded resources, enabling richer tool results.
- **OpenAI Chat Completions Endpoint** (#8486) — High interest for IDE and orchestration tool compatibility.
- **Skill Security Hardening** (#9084) — Supply‑chain guard for third‑party skill installation (screen, receipt, verify, sandbox).

**Likely to appear in v0.9.0** (tracker #7432): Auth, security hardening, gateway boundaries, A2A, tool policy, and breaking changes.

---

## 7. User Feedback Summary

**Pain Points & Dissatisfaction:**
- **Cross‑platform gaps:** Windows startup failure (#9117, closed), 74 test failures (#7462 still open), Chinese code page issues.
- **Silent context loss:** History trimming without user awareness (#8837, closed).
- **UI/UX inconsistencies:** ZeroCode copy button includes Markdown fences (#8664, closed); overlays inherit wrong background (#8765, closed); mouse selection conflicts (#8944, closed).
- **Cron/automation unreliability:** Workspace path resolution intermittent (#9206, S0).

**Satisfaction Signals:**
- Active triage and quick fixes for reported bugs (e.g., #9117 fixed same day).
- High community engagement on long‑standing features (A2A, eval harness) with multiple follow‑ups.
- Positive reactions on A2A proposal (👍7) and coordinated RFC (#6808).

---

## 8. Backlog Watch

| Item | Created | Stale? | Why Critical |
|------|---------|--------|--------------|
| [#6685] SOP HTTP fan‑in documented but not wired | 2026-05-15 | **Yes** (9 weeks) | Delays SOP milestone; core feature advertised but missing. |
| [#3566] A2A Protocol Support | 2026-03-15 | **No** (active) | High community demand (👍7); part of v0.9.0 tracker. |
| [#6808] RFC: Work Lanes, Board Automation | 2026-05-20 | **No** (active) | Accepted / rollout in progress; needs attention to avoid drift. |
| [#7462] 74 test failures on Windows | 2026-06-10 | **No** (high priority, opened) | Blocks Windows CI; P1, risk:high. |
| [#8691] ADR baseline restoration | 2026-07-04 | Moderate | Documentation debt; low risk but needs maintainer oversight. |
| [#8879] feat(web): unify risk‑profile tool permissions | 2026-07-09 | Needs‑author‑action | Large PR (XL); if unattended may conflict with other security work. |
| [#8486] OpenAI Chat Completions endpoint | 2026-06-29 | Needs‑author‑action | Major gateway feature; needs maintainer review to unblock. |

*All links use the format `zeroclaw-labs/zeroclaw` (e.g., [#6685](https://github.com/zeroclaw-labs/zeroclaw/issues/6685)).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*