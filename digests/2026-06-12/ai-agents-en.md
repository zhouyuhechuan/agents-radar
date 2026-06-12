# OpenClaw Ecosystem Digest 2026-06-12

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-12 02:50 UTC

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

# OpenClaw Project Digest — 2026-06-12

## 1. Today's Overview
The OpenClaw project remains in a highly active phase, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, **25 issues** were closed and **116 PRs** were merged or closed, indicating sustained development velocity. However, **475 open issues** and **384 open PRs** signal a growing backlog, with many items awaiting maintainer review or product decisions. No new releases were published today. The community continues to drive substantial feature discussion and bug reporting, particularly around multi-agent orchestration, security boundaries, and cross-platform support.

## 2. Releases
No new releases were published in the last 24 hours. The latest available version remains **2026.6.5** (implied from PR #92113 reference). Users are encouraged to check the [GitHub Releases](https://github.com/openclaw/openclaw/releases) page for future updates.

## 3. Project Progress
In the past day, **116 pull requests were merged or closed**. Notable examples include:

- **PR #68936** ([Autofix pipeline + Windows daemon](https://github.com/openclaw/openclaw/pull/68936)) – closed after adding a PR review autofix pipeline using Claude Agent SDK and a Windows background daemon.
- **PR #83729** ([Fix exec blocked denied path operands](https://github.com/openclaw/openclaw/pull/83729)) – closed after implementing `tools.exec.deniedPaths` as a security preflight guard.
- **PR #92316** ([Docs: Remove "React Like a Human!" from default AGENTS.md](https://github.com/openclaw/openclaw/pull/92316)) – merged, cleaning up the default agent template to remove overly aggressive emoji-reaction guidance.

Additionally, **25 issues** were closed, including:
- **Issue #91330** ([Message-tool replies replaced by bookkeeping finals](https://github.com/openclaw/openclaw/issues/91330)) – closed, fixing a bug in automatic channel delivery.
- **Issue #39992** ([`openclaw doctor` warn about synthetic models](https://github.com/openclaw/openclaw/issues/39992)) – closed after feature implementation.

These merges reflect steady progress on security hardening, automation tooling, and UX cleanup.

## 4. Community Hot Topics
The most active discussions this week revolve around long-standing gaps and recurring stability issues:

- **Issue #75** ([Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)) – 109 comments, 79 👍. A top community request for desktop apps beyond macOS/iOS/Android. Users express strong demand for parity, especially on Windows.
- **Issue #9443** ([Prebuilt Android APK releases](https://github.com/openclaw/openclaw/issues/9443)) – 25 comments. Submitted by an AI assistant on behalf of a user; asks for APK downloads in releases.
- **Issue #32473** ([Control UI requires HTTPS/localhost](https://github.com/openclaw/openclaw/issues/32473)) – 17 comments. A regression affecting VPS/Docker setups; users report difficulty with Brave key configuration.
- **Issue #22438** ([Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438)) – 17 comments. A proposal to reduce token waste in large workspaces.
- **Issue #22676** ([Signal daemon race condition on restart](https://github.com/openclaw/openclaw/issues/22676)) – 17 comments. A P1 bug causing orphaned processes and send failures.
- **Issue #32296** ([Agent replies to previous message](https://github.com/openclaw/openclaw/issues/32296)) – 15 comments. A session context confusion bug affecting conversation alignment.

Several of these issues have linked open PRs (e.g., #22438 → PR #22439; #22676 → PR likely in progress), suggesting active development.

## 5. Bugs & Stability
Multiple high-severity bugs were updated in the last 24 hours, many with **P1** priority:

- **P1 – Regression**: Issue #32473 ([Control UI requires HTTPS/localhost](https://github.com/openclaw/openclaw/issues/32473)) – affects VPS/Docker users; may be related to secure context enforcement. No fix PR linked yet.
- **P1 – Crash loop**: Issue #22676 ([Signal daemon race condition](https://github.com/openclaw/openclaw/issues/22676)) – orphaned processes and send failures on SIGUSR1 restart. Has `linked-pr-open` label.
- **P1 – Session context**: Issue #32296 ([Agent replies to previous message](https://github.com/openclaw/openclaw/issues/32296)) – misalignment in conversation flow. No fix PR yet.
- **P1 – Silent ignore**: Issue #29387 ([Bootstrap files in agentDir ignored](https://github.com/openclaw/openclaw/issues/29387)) – per-agent bootstrap files not loaded. Has `linked-pr-open`.
- **P1 – Exec env not inherited**: Issue #31583 ([`exec` tool ignores `skills.entries.*.env`](https://github.com/openclaw/openclaw/issues/31583)) – regression, fix PR (#83729) was closed today.
- **P1 – Crash on update**: Issue #40540 ([`openclaw update` EBUSY on Windows](https://github.com/openclaw/openclaw/issues/40540)) – prevents self-updating on Windows.
- **P1 – Heartbeat blocking**: Issue #40611 ([Heartbeat drift fix blocks Telegram](https://github.com/openclaw/openclaw/issues/40611)) – regression after PR #39182; linked PR open.
- **P1 – LLM request fails**: Issue #91363 ([Isolated cron fails with "LLM request failed"](https://github.com/openclaw/openclaw/issues/91363)) – model requests never reach provider; no fix PR yet.

Notable regressions include #38327 ([Google Vertex/gemini-3.1-pro-preview crash](https://github.com/openclaw/openclaw/issues/38327)) and #32473. Overall, stability concerns are concentrated around session state, security, and authentication provider interactions. Multiple issues carry `impact:session-state`, `impact:security`, and `impact:auth-provider` labels.

## 6. Feature Requests & Roadmap Signals
The community continues to push for enhancements in several areas:

- **Cross-platform clients** – #75 (Linux/Windows apps) and #9443 (Android APK) remain the most requested features.
- **Security & secrets management** – #10659 (masked secrets), #6615 (denylist for exec-approvals), #13610 (native secrets manager integration), #7722 (filesystem sandboxing config), #39979 (path-scoped RWX). These indicate strong demand for auditability and leak prevention.
- **Multi-agent orchestration** – #35203 (capability profiling + shared blackboard), #27445 (announceTarget for sub-agents), #22358 (post-subagent hook), #43367 (multi-agent orchestration instability). The project is likely to invest in stable sub-agent workflows.
- **Session memory & context** – #40418 (automated session memory preservation), #7707 (memory trust tagging), #13616 (backup/restore utility). Users want persistent learning across sessions.
- **Channel expansion** – #20786 (Telegram Business Bot support) and #33413 (Slack tool-level progress).
- **Tooling improvements** – #14785 (reduce tool schema overhead), #22438 (tiered bootstrap loading) – both have open PRs (#22439) and may land in the next minor release.

Given the high engagement, the **next version (2026.7.x)** will likely include:
- Merged PRs for tiered bootstrap (PR #22439)
- Path-scoped exec permissions (PR #83729 style)
- Improved cron reliability (multiple open PRs)
- Avatar fix for webchat (PR likely)

## 7. User Feedback Summary
- **Strong dissatisfaction** with the lack of Linux/Windows desktop apps (#75, 79 👍) and absence of prebuilt Android APK (#9443). Users want to run Clawdbot independently of the web UI.
- **Frustration with regressions**: Several users report that clean setups break after updates (#32473, #38327, #40611), eroding trust in incremental releases.
- **Pain points in multi-agent usage**: Issue #43367 details concurrent config overwrites and session lock failures; users find parallel orchestration "unreliable in practice."
- **Desire for better auditing**: The exec-approvals allowlist-only model is seen as insufficient; denylist support (#6615) and masked secrets (#10659) are highly valued.
- **Onboarding friction**: New users struggle with bootstrap file placement (#29387) and environment variable inheritance (#31583), causing silent misbehavior.
- **Positive reception** for recent security improvements (PR #83729, closed today) and the bilingual Feishu fallback (PR #92172).

## 8. Backlog Watch
Several important issues and PRs have been open for months and are still awaiting maintainer action:

- **Issue #75** ([Linux/Windows Apps](https://github.com/openclaw/openclaw/issues/75)) – created **2026-01-01**, **109 comments**, labeled `clawsweeper:needs-product-decision`. Despite high demand, no maintainer decision or assignee.
- **Issue #9443** ([Prebuilt Android APK](https://github.com/openclaw/openclaw/issues/9443)) – created **2026-02-05**, needs maintainer review.
- **Issue #6731** ([Safe/unsafe ClawdBot in Rust](https://github.com/openclaw/openclaw/issues/6731)) – created **2026-02-02**, labeled `clawsweeper:needs-product-decision`. Ambitious rewrite proposal that has not seen progress.
- **PR #62063** ([Swedish control UI locale](https://github.com/openclaw/openclaw/pull/62063)) – opened **2026-04-06**, marked `stale`. No progress despite being a straightforward localization addition.
- **PR #22439** ([Tiered bootstrap loading](https://github.com/openclaw/openclaw/pull/22439)) – opened **2026-02-21**, waiting on author for tests/signoff. If accepted, would address a top token-waste complaint.
- **Issue #10659** ([Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)) – created **2026-02-06**, needs product decision. Security-critical but unanswered.

The maintainer team appears bandwidth-constrained given the large volume of open items. Community contributors are strongly encouraged to pick up `help wanted` and `queueable-fix` issues to accelerate progress.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report, generated from the digest data provided.

---

## Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-12  
**Prepared For:** Technical decision-makers and AI agent developers

### 1. Ecosystem Overview

The open-source personal AI agent landscape in mid-2026 is characterized by hyper-competitive, high-velocity development across a dozen-plus projects, with a clear maturation of architecture toward multi-agent orchestration, security hardening, and production-grade reliability. While OpenClaw remains the dominant reference implementation, specialized forks and alternative architectures (Hermes, ZeroClaw, CoPaw) are racing to differentiate on desktop UX, provider flexibility, and enterprise features. The ecosystem is moving from prototype curiosity to serious deployment, evidenced by the surge in bug reports around session state, credential persistence, and billing safety—hallmarks of real-world usage. However, stability is the common bottleneck: every major project carries a backlog of P1/P0 bugs, indicating that feature velocity may be outpacing the community’s capacity for thorough testing.

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Today | Health Score (1-10) |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | None | **6** |
| **ZeroClaw** | 50 | 50 | v0.8.0 (major) | **8** |
| **Hermes Agent** | 50 | 50 | None | **7** |
| **CoPaw** | 34 | 42 | v1.1.11.post2 (patch) | **7** |
| **IronClaw** | 30 | 48 | None | **8** |
| **PicoClaw** | 6 | 31 | v0.2.9-nightly | **7** |
| **NanoBot** | 4 | 19 | None | **8** |
| **LobsterAI** | 2 | 16 | None | **8** |
| **NanoClaw** | 2 | 15 | None | **8** |
| **Moltis** | 1 | 1 | None | **4** |
| **NullClaw** | 1 | 0 | None | **3** |
| **TinyClaw** | 0 | 0 | None | **2** |
| **ZeptoClaw** | 0 | 0 | None | **2** |

*Health Score is a composite of velocity, bug severity/backlog, maintainer responsiveness, and community engagement. Score 8+ = healthy production-capable projects; 6–7 = active but with notable risk; <5 = stagnant or experimental.*

**Key observations:**
- OpenClaw’s raw volume (500 issues/PRs) dwarfs all others, but its backlog of 475 open issues and 384 open PRs signals a potential scaling problem.
- ZeroClaw, IronClaw, and NanoBot show the best balance of high velocity with contained backlogs.
- NullClaw, Moltis, TinyClaw, and ZeptoClaw are effectively dormant or in maintenance mode.

### 3. OpenClaw's Position

**Advantages vs. Peers**
- **Largest community & ecosystem:** 500 daily contributions signal massive mindshare; the reference implementation for all forks.
- **Most complete channel integrations:** Telegram, Slack, Discord, email, Signal, WeChat—others lack similar breadth.
- **Deepest security hardening:** `deniedPaths`, `tools.exec.deniedPaths` preflight guard (PR #83729), and path-scoped RWX proposals are ahead of most peers.
- **Rapid bug fix turnaround:** 116 PRs merged/closed in 24h; P1 bugs acknowledged quickly.

**Technical Approach Differences**
- OpenClaw follows a monolithic “swiss-army-knife” design: one agent handles all channels, tools, and memory. In contrast, ZeroClaw and NanoClaw are pursuing multi-agent daemon architectures with per-agent isolation.
- OpenClaw’s configuration is YAML-heavy, whereas CoPaw and IronClaw are moving toward wizard-driven UI setup.
- OpenClaw prioritizes backward compatibility; this slows adoption of breaking architectural improvements (e.g., the multi-agent daemon shift).

**Community Size Comparison**
- OpenClaw: ~500 active contributors/month (implied by PR/issue volume). ZeroClaw: ~50. Hermes: ~50. CoPaw: ~42. All others trail.
- OpenClaw is the de-facto benchmark: all forks measure their feature parity against it.

**Vulnerability (from data)**
- Lack of Linux/Windows desktop apps (Issue #75, 109 comments, 79 👍) is its biggest community pain. Hermes has a mature desktop client; CoPaw is investing heavily in desktop reliability.
- The backlog (475 open issues) may erode trust in maintainer responsiveness over time.

### 4. Shared Technical Focus Areas

The following requirements emerged across **three or more** projects, indicating ecosystem-wide needs:

| Requirement | Projects Demonstrating Need | Specific Evidence |
|---|---|---|
| **Multi-agent orchestration** | OpenClaw, ZeroClaw, NanoClaw, CoPaw, LobsterAI, Hermes | OpenClaw #35203 (capability profiling), ZeroClaw #5849 (Dream Mode), NanoClaw #2742 (PR Factory recipe), CoPaw #5139 (swarm), LobsterAI #1462 (room/manager) |
| **MCP integration reliability** | Hermes, ZeroClaw, PicoClaw, Moltis, NanoBot | Hermes #38945 (tools not exposed in desktop), ZeroClaw #6699 (tool_filter no-op), PicoClaw #2696 (dynamic headers), Moltis #1115 (Fastmail auth) |
| **Cross-platform desktop parity (Linux/Windows)** | OpenClaw, Hermes, PicoClaw, CoPaw, ZeroClaw | OpenClaw #75 (Linux/Windows apps), Hermes #44532 (Linux setup friction), CoPaw #5106/#5086 (Windows crashes), ZeroClaw #5542 (WSL2 OOM) |
| **Secrets / credential management** | OpenClaw, IronClaw, CoPaw, ZeroClaw | OpenClaw #10659 (masked secrets), IronClaw #4766 (NEAR AI credential persistence), CoPaw #5028 (keychain isolation), ZeroClaw #6914 (tool filtering enforcement) |
| **Cron/automation reliability** | Hermes, PicoClaw, ZeroClaw, CoPaw | Hermes #44585 (billing leakage from cron), ZeroClaw #6037 (cron burst), CoPaw #5064 (scheduled tasks not triggering), PicoClaw #2957 (tool_calls dropped during streaming) |
| **Memory/context management improvements** | OpenClaw, NanoClaw, CoPaw, ZeroClaw | OpenClaw #40418 (session memory preservation), NanoClaw #1356 (memory system redesign), CoPaw #3817/#5137 (memory config loss), ZeroClaw #5849 (Dream Mode consolidation) |
| **Token & cost visibility** | OpenClaw, CoPaw, Hermes, PicoClaw | OpenClaw #22438 (tiered bootstrap loading), CoPaw #5103 (token stats), Hermes #44585 (billing safety), PicoClaw #2121 (repeated output wasting tokens) |

### 5. Differentiation Analysis

| Differentiation Axis | Project(s) Leading | Key Difference |
|---|---|---|
| **Desktop-first UX** | **Hermes Agent**, **CoPaw** | Hermes has a polished Electron/Tauri desktop client; CoPaw is investing heavily in Windows reliability. OpenClaw, ZeroClaw, NanoClaw lack desktop apps. |
| **Multi-agent daemon architecture** | **ZeroClaw**, **NanoClaw** | ZeroClaw v0.8.0 introduced a single daemon managing many named agents with isolated workspaces, memory, and security policies. NanoClaw uses per-group idle-timeout containers. OpenClaw is single-agent-many-channels. |
| **Enterprise / production focus** | **IronClaw**, **LobsterAI** | IronClaw has automated QA, production cutover pipelines, and operator log filtering. LobsterAI integrates Gmail triggers and real-time ASR. Both focus on reliability and credential hygiene. |
| **SDK & developer tooling** | **NanoBot** | NanoBot emphasizes a Python SDK for custom agents, skill caching, and provider configurability. Most others are end-user focused. |
| **Rust-native performance** | **PicoClaw** | Written in Go (not Rust), but its nightly builds and fast iteration show a focus on high-performance runtime. (ZeroClaw is also Go-based.) |
| **Experimental / research** | **NullClaw**, **TinyClaw**, **ZeptoClaw** | Minimal activity; likely used for internal R&D or niche experiments. Not production-relevant. |
| **User interface & onboarding** | **CoPaw**, **IronClaw** | CoPaw has a modern “AionUi” design language and wizard-driven setup. IronClaw has a polished WebUI v2. Others rely more on config files. |
| **Channel & platform breadth** | **OpenClaw**, **Moltis** | OpenClaw supports the most channels. Moltis is unique in its WhatsApp/privacy-chat focus. |

### 6. Community Momentum & Maturity

**Tier 1 – Rapid Iteration / Feature Velocity (8+ on Health Score)**
- **ZeroClaw** – Major architectural release (v0.8.0) drew intense activity; high risk/reward profile.
- **IronClaw** – Production push (Reborn binary, automated QA), high PR merge rate, very responsive to bug reports.
- **NanoBot** – Small but efficient team; merges features and fixes quickly with minimal backlog.
- **LobsterAI** – Surged today with 15 merged PRs; focus on reliability and automation triggers.
- **NanoClaw** – Consistent moderate activity; strong on infrastructure (containers, bridge, approvals).

**Tier 2 – High Activity, Stabilizing (7–8)**
- **Hermes Agent** – Very high engagement (50 issues/PRs) but 43 open issues and multiple P1/P2 bugs. Community is large but testing friction is high.
- **CoPaw** – Intense activity (34 issues, 42 PRs) but two patches shipped today reveal desktop reliability crisis. Feature velocity is high but quality is uneven.
- **PicoClaw** – Rapid nightly releases (31 PRs in 24h) but has a critical image hallucination bug and a months-old Windows path issue.

**Tier 3 – Stagnant / Maintenance (2–4)**
- **NullClaw**, **Moltis**, **TinyClaw**, **ZeptoClaw** – Near-zero activity. Moltis has one bug fix PR; the others have no PRs. Not recommended for active development or production use.

**Project Lifecycle Summary:**
- **Peak hype & growth:** OpenClaw, Hermes, ZeroClaw
- **Stabilization phase:** IronClaw, LobsterAI, NanoBot
- **Declining / unmaintained:** NullClaw, TinyClaw, ZeptoClaw

### 7. Trend Signals

The following industry trends are evident from cross-project community feedback and issue patterns. These represent high-value opportunities for AI agent developers and infrastructure builders:

1. **Multi-agent orchestration is the #1 unmet need.** Six projects (OpenClaw, ZeroClaw, NanoClaw, Hermes, CoPaw, LobsterAI) have explicit feature requests or architectural work for agent-to-agent delegation, swarm modes, or memory consolidation across agents. The demand is not just for multiple agents running in parallel, but for **hierarchical orchestration** (manager/worker patterns) and

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-06-12

## 1. Today’s Overview
The NanoBot project is experiencing **high development velocity** with 19 pull requests updated in the last 24 hours, of which 6 were merged or closed. Issue activity is moderate (4 updated, 2 closed). No new releases were published today. The repository shows a strong focus on **stability fixes** (sandbox compatibility, MCP crash prevention, orphaned tool results), **feature expansions** (new transcription provider, skill caching, Slack improvements), and **SDK/API enhancements**. The maintainer team is actively reviewing and merging contributions, particularly from external contributors.

## 2. Releases
No new releases were recorded for this period.

## 3. Project Progress – Merged/Closed PRs
The following pull requests were merged or closed today, representing concrete advancements:

- **feat(providers): make stream-idle timeout configurable per-provider** ([#4020](https://github.com/HKUDS/nanobot/pull/4020)) – Closes #4013. Adds a provider-level `stream_idle_timeout` setting, replacing the global environment var. **Impact**: Better support for local LLMs (LM Studio, Ollama) with longer timeout needs.
- **feat(slack): add groupRequireMention to scope allowlist channels to @mentions** ([#4289](https://github.com/HKUDS/nanobot/pull/4289)) – When `groupPolicy` is `"allowlist"`, the bot can now be configured to reply only when @mentioned, even in allowed channels.
- **feat(transcription): add SiliconFlow as transcription provider** ([#4281](https://github.com/HKUDS/nanobot/pull/4281)) – Registers SiliconFlow with default model `FunAudioLLM/SenseVoiceSmall`, reusing the OpenAI-compatible adapter.
- **fix(utils): make split_message fenced-code-block-aware** ([#4257](https://github.com/HKUDS/nanobot/pull/4257)) – Prevents broken code blocks when long messages are split at arbitrary boundaries.
- **Worktree feature + Hermes research doc** ([#4298](https://github.com/HKUDS/nanobot/pull/4298), [#4297](https://github.com/HKUDS/nanobot/pull/4297)) – Documentation/analysis PRs, likely internal.
- **feat(skills): cache skills loader entries and metadata** ([#4301](https://github.com/HKUDS/nanobot/pull/4301)) – Avoids repeated directory scans and YAML parsing on every agent context build. (Opened, not merged yet, but noted as active progress.)

## 4. Community Hot Topics
The most active issues and PRs (by comments and reactions) reflect key user concerns:

- **Issue #4233 – Show nanobot version in WebUI** ([#4233](https://github.com/HKUDS/nanobot/issues/4233)) – Closed with 2 comments. Users want version visibility for easier debugging and update awareness.
- **Issue #4236 – bwrap sandbox fails on Ubuntu 24.04** ([#4236](https://github.com/HKUDS/nanobot/issues/4236)) – Closed after fix. Highlights friction with modern Linux security restrictions.
- **Issue #4305 – Multiple custom providers** ([#4305](https://github.com/HKUDS/nanobot/issues/4305)) – Open, 0 comments yet, but a long-standing need (see backlog).
- **Issue #4302 – Gateway crash after MCP reconnect** ([#4302](https://github.com/HKUDS/nanobot/issues/4302)) – Open, 0 comments; linked to similar issue #4211. A stability hot topic.

**Underlying needs**: Users are pushing for better **usability** (version display), **compatibility** (Linux sandboxing), **flexibility** (multiple custom provider endpoints), and **reliability** (MCP reconnection).

## 5. Bugs & Stability
Identified bugs with severity ranking:

| Bug | Severity | Status | Fix PR exists? |
|-----|----------|--------|----------------|
| Gateway crash on MCP reconnect ([#4302](https://github.com/HKUDS/nanobot/issues/4302)) | **Critical** – Crashes the service. | Open | [#4303](https://github.com/HKUDS/nanobot/pull/4303) (fix MCP generator cleanup) |
| Orphaned tool results persisted to history ([#4006](https://github.com/HKUDS/nanobot/issues/4006)) | **High** – Causes API rejection for OpenAI/Anthropic. | Open (fix PR open) | [#4306](https://github.com/HKUDS/nanobot/pull/4306) |
| Cron subagents marked complete before finishing ([#4290](https://github.com/HKUDS/nanobot/issues/4290)) | **Medium** – Race condition in cron jobs. | Open (fix PR open) | [#4304](https://github.com/HKUDS/nanobot/pull/4304) (wait for subagents) |
| bwrap sandbox failure on Ubuntu 24.04 ([#4236](https://github.com/HKUDS/nanobot/issues/4236)) | **Medium** – Affects users on restricted user namespaces. | Closed (fixed) | Not applicable (already merged) |
| Codex duplicate reasoning item error ([#3633](https://github.com/HKUDS/nanobot/issues/3633)) | **Medium** – Multi-turn conversation breakage. | Open (fix PR open) | [#4021](https://github.com/HKUDS/nanobot/pull/4021) |

**Observation**: The project is responding quickly to crash-level bugs with targeted fix PRs. The most urgent is the MCP reconnect crash, addressed in [#4303](https://github.com/HKUDS/nanobot/pull/4303).

## 6. Feature Requests & Roadmap Signals
Several user-requested features are either being implemented or are gaining traction:

- **Multiple custom OpenAI-compatible providers** – Issue [#4305](https://github.com/HKUDS/nanobot/issues/4305) and long-standing PR [#3239](https://github.com/HKUDS/nanobot/pull/3239) (since April). Likely to land in next minor release.
- **Skill caching** – PR [#4301](https://github.com/HKUDS/nanobot/pull/4301) improves performance for skill-heavy agents. Likely to be merged soon.
- **Cron automations bound to sessions** – PR [#4299](https://github.com/HKUDS/nanobot/pull/4299) enables scheduled tasks to run within specific sessions. High demand for automation.
- **Python SDK runtime controls** – PR [#4296](https://github.com/HKUDS/nanobot/pull/4296) expands the SDK from a basic `bot.run()` to richer metadata and state control. Expected to be developer-community beneficial.
- **SiliconFlow transcription** – Already merged (PR [#4281](https://github.com/HKUDS/nanobot/pull/4281)), meeting user demand for more ASR providers.
- **Gateway start/stop/restart commands** – PR [#3538](https://github.com/HKUDS/nanobot/pull/3538) (open since April) may be revisited.

**Prediction for next version**: The combination of multiple custom providers, skill caching, and session-bound cron will likely define the next feature release.

## 7. User Feedback Summary
**Real pain points**:
- **Linux sandbox compatibility**: Users on Ubuntu 24.04 cannot use `bwrap` sandbox without workarounds (fixed in #4236).
- **Version visibility**: Users want the version shown in the WebUI (#4233) – closed, but feature may be in progress.
- **MCP reconnection crashes**: One user reported a gateway crash after session termination, highlighting reliability concerns.
- **Multiple provider limitation**: Users needing several custom endpoints find the single `custom` provider restrictive.
- **Slack @mention behavior**: Channel allowlist users wanted an option to require @mentions (#4289) – now available.

**Satisfaction indicators**: The quick closure of #4236 (bwrap) and #4289 (Slack) and the proactive fixes for crash bugs suggest responsive maintainers. No negative sentiment was expressed in the data.

## 8. Backlog Watch
The following important items remain open or unattended for an extended period and may need maintainer attention:

- **PR #3239 – Multiple custom OpenAI-compatible providers** (opened 2026-04-17) – Stalled despite high user demand. Could conflict with new issue #4305.
- **PR #3538 – Gateway start/stop/restart commands** (opened 2026-04-29) – Awaiting review; would improve operational UX.
- **PR #4021 – Codex dedup reasoning items** (opened 2026-05-27, AI-assisted) – Addresses a known duplicate-item error; still open.
- **Issue #4290 – Cron subagent timing** – Already has a fix PR (#4304), but the issue itself remains open.

**Maintainers should prioritize reviewing #3239 / #4305 to resolve the long-standing provider limit, and merge #4021 and #4304 to close stable, well-understood bugs.**

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-12

## 1. Today’s Overview

Hermes Agent remains in a state of high activity, with **50 issues** and **50 pull requests** updated in the last 24 hours. Of the issues, 43 remain open and 7 were closed; on the PR side, 35 are open and 15 were merged or closed. No new releases were published today. The project shows intense community engagement, particularly around desktop/Ui bugs, OAuth/MCP integration, and cron reliability. A critical P1 bug (#44585) concerning billing leakage during cron pause containment was reported, while multiple fix PRs are already in flight for high-impact issues like Discord reconnection handling and malformed tool call retries.

## 2. Releases

No releases today.

## 3. Project Progress — Merged & Closed PRs

Today **15 PRs were merged or closed**, including:

- **#44596** (closed/merged) — Auto-detect RTL/bidi text direction in desktop chat.
- **#44605** (open, fix MCP OAuth Accept header) — likely still under review but closed items confirm progress.
- **#40032, #40050, #40082, #40131, #44340** — closed by author after being opened before the current contribution gate; they address desktop session refresh, Intel macOS build support, voice transcription timeout, and session notification badges.
- **#44575** — test issue closed.

While the majority of open PRs target bug fixes, several feature PRs (memory/delegation enhancements, prompt overrides, Feishu streaming) remain open for review. The project’s pace suggests steady improvement in stability and platform parity.

## 4. Community Hot Topics

The most active discussions (by comments & reactions) reveal five key areas of user interest:

- **Skills index freshness** ([#38240](https://github.com/NousResearch/hermes-agent/issues/38240), 11 comments) — An automated watchdog detected a stale skills index. Users are discussing the impact on search/retrieval and how to improve the CI rebuild cadence.
- **Exposing model_switch as an agent tool** ([#16525](https://github.com/NousResearch/hermes-agent/issues/16525), 7 comments, 3 👍) — A feature request for autonomous model routing based on task complexity. The high reaction count indicates strong demand for self-routing capabilities beyond current slash commands and config-based options.
- **Desktop approvals not rendering** ([#37812](https://github.com/NousResearch/hermes-agent/issues/37812), closed, 7 comments, 4 👍) — A major UX gap that made manual approval mode unusable on macOS. The community applauded the fix and highlighted the need for better approval workflow testing.
- **MCP tools not reliably exposed in Desktop/TUI** ([#38945](https://github.com/NousResearch/hermes-agent/issues/38945), 6 comments) — Users report that configured MCP servers (especially Todoist) work in CLI but not in Desktop or TUI session, degrading workflow parity with tools like Claude Code.
- **npm ci lock file mismatch** ([#44121](https://github.com/NousResearch/hermes-agent/issues/44121), 6 comments) — A clean checkout build failure on npm 11, causing friction for contributors and developer onboarding.

**Underlying needs:** Users are pushing for more autonomous agent capabilities, cross-platform consistency, and smoother developer experience. The MCP ecosystem integration remains a pain point, especially for productivity tools.

## 5. Bugs & Stability

**Critical (P1)**
- [#44585](https://github.com/NousResearch/hermes-agent/issues/44585) — Cron jobs can inherit temporary paid provider state during pause/stop, continuing billing. This creates real cost leakage. *No fix PR yet*, but flagged as top priority.

**High (P2)**
- [#44560](https://github.com/NousResearch/hermes-agent/issues/44560) — `model.options` handler blocks on synchronous HTTP calls, causing WebSocket timeout. Affects responsiveness especially with slow providers.
- [#44541](https://github.com/NousResearch/hermes-agent/issues/44541) — Cron delivery to Discord fails with `Session is closed` after adapter reconnects. **Fix PR #44599** is already open.
- [#44499](https://github.com/NousResearch/hermes-agent/issues/44499) — Desktop agent ignores configured BrowserOS MCP and uses built-in browser tools instead.
- [#40344](https://github.com/NousResearch/hermes-agent/issues/40344) — WebUI profile state.db not created for new profiles; sessions leak to main database.
- [#44121](https://github.com/NousResearch/hermes-agent/issues/44121) — `npm ci` fails on clean checkout; lock file mismatch. Blocks contributor onboarding.
- [#44580](https://github.com/NousResearch/hermes-agent/issues/44580) — `hermes update` reports success when desktop rebuild silently fails. **Fix PR #44608** is open.
- [#44581](https://github.com/NousResearch/hermes-agent/issues/44581) — Desktop folder drag-and-drop fails with `file not found`. **Fix PR #44606** is open.
- [#44592](https://github.com/NousResearch/hermes-agent/issues/44592) — OAuth token exchange fails on `application/x-www-form-urlencoded` responses (e.g., GitHub). **Fix PR #44605** is open.
- [#43657](https://github.com/NousResearch/hermes-agent/issues/43657) — `aiohttp` ClientSession leak after auxiliary tasks, causing unclosed connector warnings.
- [#16425](https://github.com/NousResearch/hermes-agent/issues/16425) — Windows local terminal commands complete without returning output, appearing to hang.

**Medium (P3)**
- [#44562](https://github.com/NousResearch/hermes-agent/issues/44562) — Desktop frontend crash: `tapClientLookup: Index out of bounds` when tool returns unexpected data.
- [#41693](https://github.com/NousResearch/hermes-agent/issues/41693) — Similar crash in renderer error boundary triggers "Reload window".
- [#40544](https://github.com/NousResearch/hermes-agent/issues/40544) — Desktop inline edit submits on Enter during IME composition.
- [#44543](https://github.com/NousResearch/hermes-agent/issues/44543) — `/undo` slash command does not work in Hermes Desktop GUI on Windows.
- [#44557](https://github.com/NousResearch/hermes-agent/issues/44557) — Hermes Studio update deadlock on Windows: updater killed when parent process exits.
- [#44582](https://github.com/NousResearch/hermes-agent/issues/44582) — `pre_tool_call` plugin hook not invoked during agent tool execution.
- [#43883](https://github.com/NousResearch/hermes-agent/issues/43883) — `web.backend=anysearch` silently ignored; falls back to DuckDuckGo (unreachable for some regions).

**Summary:** The project is facing a wave of desktop-specific bugs (drag-drop, IME, crash on non-standard tool responses), along with platform gaps (Windows, Linux setup, Discord cron). Many of these have incoming fix PRs, indicating fast turnaround from the community and maintainers.

## 6. Feature Requests & Roadmap Signals

Several feature requests with meaningful community traction point toward future directions:

- **Autonomous model routing** ([#16525](https://github.com/NousResearch/hermes-agent/issues/16525), 3 👍) — Likely candidate for next minor release. The PR ecosystem lacks an implementation yet.
- **Xiaomi token plan support** ([#14285](https://github.com/NousResearch/hermes-agent/issues/14285), 2 👍, closed) — Already resolved; included for completeness.
- **Native RTL support for Arabic** ([#44150](https://github.com/NousResearch/hermes-agent/issues/44150), closed) — Addressed in PR #44596 which was merged today.
- **Declarative per-fragment system-prompt overrides** — PR #44610 open, adds config surface for prompt fragment modifications without edits to source code. This is an advanced customization feature likely to be included in next release.
- **Memory + Delegation Layer Enhancements (M1-M6)** — PR #44586 open, opt-in modules for layered memory, proposal gate, retrieval pack, integration plugins. Large architectural enhancement likely targeted at v0.16 or later.
- **Feishu CardKit v1 streaming** — PR #44594 open, adds real-time streaming card UI for Feishu platform. Shows continued enterprise platform expansion.
- **Rust-backed install manager** — PR #44067 open, moving bootstrap logic to Rust for install/repair/uninstall. This suggests a focus on cross-platform installation reliability.

The roadmap is bifurcating into **stability fixes** (OAuth, cron, desktop) and **large feature injections** (memory layer, prompt overrides, new platform integrations).

## 7. User Feedback Summary

Real user pain points observed in today’s issues include:

- **Friction in Linux/WSL setup** (#44532) — The setup workflow is incomplete compared to macOS, missing tool API configuration steps.
- **Credential duplication** (#44548) — `.hermes/.env` variables not propagated to MCP subprocesses, forcing users to repeat credentials in multiple places.
- **Inconsistent MCP tool exposure** (#38945) — Desktop/TUI sessions not showing the same tools as CLI, forcing workflow interruptions.
- **Billing risk from cron** (#44585) — Real money spent due to state inheritance after temporary provider changes.
- **Desktop update UX** (#44515, #44580) — Updates stuck if background processes running; silent failures mislead users.
- **WeChat duplicate responses** (#44497) — Single message triggers two independent AI replies, causing confusion and spam.
- **Dashboard CLI confusion** (#44567) — `hermes dashboard --status` and `--stop` not working while dashboard runs in PowerShell.

**Sentiment:** Users are pushing Hermes into serious production and enterprise use (Discord, WeChat, billing concerns, multi-account OAuth). There’s appreciation for rapid bug fixes (e.g., the approvals fix got 4 👍) but frustration with platform parity and configuration complexity.

## 8. Backlog Watch

The following open issues/PRs require maintainer attention due to age, severity, or lack of response:

- **#16425** — Windows terminal command output missing (2026-04-27, P2, 1 comment). No fix PR or maintainer note. Critical for Windows users.
- **#14285** (closed) — Already resolved, but shows that user-desired features can take weeks to close.
- **#43657** — aiohttp session leak (2026-06-10, P2). Relatively recent, but no fix assigned yet.
- **#38945** — MCP tools not exposed in Desktop/TUI (2026-06-04, P2). Community has asked for a solution but no PR yet.
- **#16525** — model_switch tool (2026-04-27, P3). High community interest but no implementation progress.
- **#43883** — `anysearch` backend ignored (2026-06-11, P3). Simple fix needed but not prioritized.

Several old PRs from author `manualzuru` (e.g., #40032, #40050, etc.) were closed today without merging, likely needing re-audit. No outstanding long-unanswered PRs, but the volume of open issues (43 open) indicates the maintainer team is working through a backlog. The project would benefit from triage attention to these items, especially the Windows and MCP gaps.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-06-12

## 1. Today's Overview
PicoClaw saw intense development activity over the past 24 hours, with **31 pull requests updated** (18 merged/closed, 13 open) and **6 issues updated** (3 open, 3 closed). A new nightly build **v0.2.9-nightly.20260612** was released, continuing the project’s rapid iteration cycle. The high PR merge rate indicates strong momentum in fixing bugs, improving channel integrations, and advancing the agent collaboration system. Three open bugs – including a critical image hallucination issue and a Windows path bug – remain under investigation.

---

## 2. Releases
**New Release: `v0.2.9-nightly.20260612.413d3749`**  
[Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
This is an automated nightly build and may be unstable. It includes all merged changes up to `413d3749`. No breaking changes or migration notes are documented; users upgrading from stable versions should test carefully.

---

## 3. Project Progress
**18 pull requests were merged/closed today**, reflecting progress across multiple areas:

- **Channel & Streaming Fixes**  
  - [#2957](https://github.com/sipeed/picoclaw/pull/2957) – Fixed `tool_calls` messages being dropped during streaming (closed related issue #2958).  
  - [#2934](https://github.com/sipeed/picoclaw/pull/2934) – Enabled WhatsApp native mode via `use_native: true`.  
  - [#2956](https://github.com/sipeed/picoclaw/pull/2956) – Preserved channel `enabled` state when merging `security.yml` (still open, but update active).

- **MCP & Tooling**  
  - [#2696](https://github.com/sipeed/picoclaw/pull/2696) – Added per-request dynamic HTTP headers from channel context to MCP servers.  
  - [#3048](https://github.com/sipeed/picoclaw/pull/3048) – Rejected unknown pre-positional flags in `mcp add`.

- **Configuration & Identity**  
  - [#2955](https://github.com/sipeed/picoclaw/pull/2955) – Fixed singleton PID check to verify process identity (prevents startup failure due to PID reuse).  
  - [#3067](https://github.com/sipeed/picoclaw/pull/3067) – Added `DmScope` field to persist session configuration.  
  - [#3060](https://github.com/sipeed/picoclaw/pull/3060) – Corrected error wrapping (`%w`) and handled `json.MarshalIndent` errors.

- **Model Configuration**  
  - [#2947](https://github.com/sipeed/picoclaw/pull/2947) – Fixed `claude-sonnet-4.6` model ID (hyphens vs dots).

- **Dependency Updates**  
  Multiple automated bumps (AWS SDK, `modelcontextprotocol/go-sdk`, Vite, ESLint, shadcn, etc.) ensure compatibility with latest libraries.

---

## 4. Community Hot Topics
The most active discussions centred on cross‑platform compatibility and async messaging:

| Issue / PR | Comments | Topic | Link |
|------------|----------|-------|------|
| **#2472** – `list_dir` returns “invalid argument” on Windows due to path separator mismatch | 5 comments | Windows compatibility; Go `os.Root` expects forward slashes. A long‑standing bug (opened Apr 10) still unresolved. | [Issue](https://github.com/sipeed/picoclaw/issues/2472) |
| **#2954** – 32‑bit Android unsupported | 3 comments | Platform support gap; closed as stale without fix. | [Issue](https://github.com/sipeed/picoclaw/issues/2954) |
| **#2958** – `tool_calls` dropped during consecutive requests via pico channel | 2 comments | Message delivery reliability; fixed by PR #2957. | [Issue](https://github.com/sipeed/picoclaw/issues/2958) |
| **#3094** – Duplicate messages when async subagent (spawn) completes | 1 comment | Messaging architecture – `ForUser` field used twice. | [Issue](https://github.com/sipeed/picoclaw/issues/3094) |
| **#2937** – First‑class Agent Collaboration Bus (open PR) | No comments yet but a major feature PR | Expected to enable durable inter‑agent communication with mailboxes and permission‑aware delivery. | [PR](https://github.com/sipeed/picoclaw/pull/2937) |

The underlying needs are clear: **Windows users expect full file‑system tool support**, while **channels (Telegram, Feishu) need reliable async message deduplication**. The Agent Collaboration PR signals a strategic push toward multi‑agent workflows.

---

## 5. Bugs & Stability
Three open bugs were reported or updated in the last 24 hours, ranked by severity:

1. **Critical – Image hallucination when active model lacks vision support**  
   [#3108](https://github.com/sipeed/picoclaw/issues/3108) – When using a text‑only model (e.g., `deepseek/deepseek-v4-flash` via OpenRouter), the `load_image` tool is called but the model invents descriptions. **No fix PR yet.**  
   *Impact: Users may receive fabricated content.*

2. **High – Windows `list_dir` fails due to path separator**  
   [#2472](https://github.com/sipeed/picoclaw/issues/2472) – `\` vs `/` mismatch with `os.Root`. Affects all directory‑listing tools on Windows. **No fix PR yet.**

3. **Medium – Duplicate messages from async subagent (spawn)**  
   [#3094](https://github.com/sipeed/picoclaw/issues/3094) – Subagent output pushed directly and also summarized by the main agent, causing duplicates on Feishu/Telegram. **No fix PR yet.**

Additionally, a **security vulnerability** (#3080) – bypass of `allowed_cidrs` via loopback proxying – was **closed as resolved**, indicating a fix was applied (likely through configuration hardening).  

Two previously reported bugs were closed as stale: #2954 (32‑bit Android) and #2958 (tool_calls dropped, now fixed via #2957).

---

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed as issues in the last 24 hours, but the open PRs and merged work point toward:

- **Agent Collaboration Bus** ([#2937](https://github.com/sipeed/picoclaw/pull/2937)) – a first‑class, durable inter‑agent communication system. This is the most significant upcoming feature, likely targeted for the next minor release (v0.3.0).  
- **MCP improvements** – dynamic headers (#2696) and better argument parsing (#3048) are already merged, suggesting continued investment in MCP tool ecosystem.  
- **Session configuration persistence** (#3067) – user‑requested ability to save `dm_scope` setting, now merged.

Predictions: The **Agent Collaboration Bus** will land in the next stable release (v0.3.0). **Windows file‑path fix** should be prioritised in an upcoming patch. Given the high volume of dependabot PRs, dependency hygiene remains a priority.

---

## 7. User Feedback Summary
- **Pain Points**  
  - Windows users cannot use `list_dir` (issue #2472, open since April).  
  - Async subagent spawn sends duplicate messages on Feishu/Telegram (#3094).  
  - Non‑vision models produce hallucinated image descriptions (#3108).  
  - 32‑bit Android support was requested but closed as stale (#2954) – potential dissatisfaction among mobile/embedded users.

- **Satisfaction Signals**  
  - Security vulnerability #3080 was acknowledged and closed quickly.  
  - The project maintains a healthy flow of dependency updates and bug fixes.  
  - Contributors are actively submitting PRs (31 updated in 24h), indicating a responsive maintainer team.

- **Use Cases**  
  - Multi‑channel deployment (WhatsApp, Telegram, Feishu) with tool‑calling agents is the primary pattern.  
  - MCP integration for external tool servers is gaining traction.

---

## 8. Backlog Watch
Long‑standing or high‑importance items that need maintainer attention:

| Item | Status | Priority | Notes |
|------|--------|----------|-------|
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) – Windows `list_dir` path bug | Open since Apr 10, last updated Jun 11 | High | No fix PR; Windows adoption blocker. |
| [#2954](https://github.com/sipeed/picoclaw/issues/2954) – 32-bit Android support | Closed as stale | Medium | Should be reopened or documented as unsupported. |
| [#3094](https://github.com/sipeed/picoclaw/issues/3094) – Duplicate async subagent messages | Open since Jun 10 | Medium | Affects multiple channels; needs design fix. |
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) – Agent Collaboration Bus PR | Open since May 24 | High | Large feature PR; requires thorough review and testing. |
| [#2956](https://github.com/sipeed/picoclaw/pull/2956) – Preserve channel enabled state | Still open (update Jun 11) | Medium | Merged? Actually status says [OPEN] – needs merge after review. |
| [#3108](https://github.com/sipeed/picoclaw/issues/3108) – Image hallucination | Opened Jun 11, no comments | Critical | Urgent priority; missing model validation. |

Maintainers should prioritise the Windows path fix and the image hallucination bug, as they directly impact user trust and platform reach. The Agent Collaboration PR represents a major architectural change that will benefit from community feedback before merging.

---

*Generated on 2026-06-12 from GitHub data provided by the project.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-12

## 1. Today's Overview
The project saw high activity over the past 24 hours with **15 pull requests** processed (9 merged/closed, 6 still open) and **2 issues updated** (1 open, 1 closed). No new releases were published. The majority of PRs were concentrated in infrastructure improvements (container lifecycle, session management, channel bridging) and skill recipes, indicating a strong push toward both stability hardening and extensibility. The community issue around **memory system scalability** (#1356) continues to attract interest (6 👍), while a critical bug in `writeOutboundDirect` (read-only DB) was promptly fixed and merged.

## 2. Releases
*No new releases since the last digest.*

## 3. Project Progress (Merged/Closed PRs Today)
Nine pull requests were merged or closed today, reflecting a mix of bug fixes and feature additions:

| PR | Title | Type | Summary |
|----|-------|------|---------|
| [#2740](https://github.com/nanocoai/nanoclaw/pull/2740) | feat(container): per-group idle timeout — clean exit for ephemeral sessions | Feature | Adds configurable idle timeout per messaging group, enabling clean container teardown for ephemeral sessions. |
| [#2739](https://github.com/nanocoai/nanoclaw/pull/2739) | feat(webhook-server): raw-route registry — non-Chat-SDK webhooks become an append | Feature | Registers raw routes for external webhooks that don’t use the Chat SDK, allowing custom integrations. |
| [#2738](https://github.com/nanocoai/nanoclaw/pull/2738) | fix(session-manager): writeOutboundDirect opens outbound.db read-only — command-gate denials never deliver | Bug Fix | Resolves issue #2495 where outbound writes silently failed because the DB was opened in read-only mode. |
| [#2737](https://github.com/nanocoai/nanoclaw/pull/2737) | feat(approvals): approval-resolved callback registry — modules observe resolution additively | Feature | Implements a callback registry that fires when an approval is resolved, allowing multiple modules to react without interference. |
| [#2736](https://github.com/nanocoai/nanoclaw/pull/2736) | fix(host-sweep): grace period for freshly-woken containers with stale processing claims | Bug Fix | Prevents premature termination of containers that have just woken up but still hold stale claims from a prior run. |
| [#2735](https://github.com/nanocoai/nanoclaw/pull/2735) | fix(chat-sdk-bridge): record the acting user on resolved approval cards | Bug Fix | Ensures approval cards in Chat SDK show which user resolved them, improving audit trail. |
| [#2734](https://github.com/nanocoai/nanoclaw/pull/2734) | feat(delivery): getDeliveryAction read side for the action registry | Feature | Exposes a read-only query for delivery actions, enabling monitoring and debugging. |
| [#2733](https://github.com/nanocoai/nanoclaw/pull/2733) | feat(channels): native channel-instance dimension — multi-bot substrate | Feature | Adds a native “channel instance” abstraction, laying groundwork for running multiple bot instances per channel. |
| [#2741](https://github.com/nanocoai/nanoclaw/pull/2741) | fix(setup): auto-submit handoff context as Claude's first prompt | Bug Fix | Corrects interactive setup handoff to Claude so that context is automatically submitted as a user prompt, making the handoff actionable. |

These merges represent a significant step forward in platform reliability (grace periods, DB access fixes) and extensibility (callback registries, raw routes).

## 4. Community Hot Topics

### Most Active Issue
- **[#1356 – Agent memory system redesign](https://github.com/nanocoai/nanoclaw/issues/1356)** (6 👍, 2 comments)  
  This long-running issue (opened March 2026) continues to gather support. It tracks research into scaling the existing markdown-file-based memory system beyond ~54 files / 83 KB. The community is clearly concerned about future scalability as agent deployments grow. No PR or formal proposal is linked yet, but the sustained attention suggests a high-demand feature.

### Most Notable Open PRs
- **[#2744 – fix(signal): deliver agent reactions and forward inbound reactions](https://github.com/nanocoai/nanoclaw/pull/2744)**  
  Addresses a silent drop of agent reactions on Signal. Although currently 0 comments/reactions, the underlying bug (reactions never delivered) is likely a blocker for Signal users.
- **[#2742 – feat(recipes): the PR Factory — a published recipe for PR review, triage & testing](https://github.com/nanocoai/nanoclaw/pull/2742)**  
  A skill/recipe that spins up a dedicated worker agent per PR, automating review and testing. This is a community-contributed “recipe” that could become a template for automated CI workflows.
- **[#2743 – fix(cli): wirings create silently skips the agent_destinations side effect](https://github.com/nanocoai/nanoclaw/pull/2743)**  
  Reports a missing side-effect when creating a wiring, causing messages sent to new chats to be dropped.

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | `writeOutboundDirect` opens outbound DB read-only, causing command-gate denial responses to be silently dropped (issue #2495) | ✅ Fixed | [#2738](https://github.com/nanocoai/nanoclaw/pull/2738) merged |
| **High** | Signal adapter silently drops agent reactions and ignores inbound reaction envelopes (PR #2744) | 🔴 Open | [#2744](https://github.com/nanocoai/nanoclaw/pull/2744) |
| **Medium** | `ncl wirings create` skips `agent_destinations` side effect, causing messages to new chats to never arrive (PR #2743) | 🔴 Open | [#2743](https://github.com/nanocoai/nanoclaw/pull/2743) |
| **Low** | Freshly-woken containers with stale processing claims could be prematurely killed (PR #2736) | ✅ Fixed | [#2736](https://github.com/nanocoai/nanoclaw/pull/2736) merged |
| **Low** | Chat SDK approval cards did not record which user resolved them (PR #2735) | ✅ Fixed | [#2735](https://github.com/nanocoai/nanoclaw/pull/2735) merged |

The **read-only DB** bug (#2495) was the most critical today—it silently lost administrative denials—and has been resolved. The Signal reaction drop (PR #2744) remains a pressing issue for any Signal-integrated agent.

## 6. Feature Requests & Roadmap Signals

Several merged features today point toward a more modular and extensible NanoClaw:

- **Per-group idle timeout** (#2740) suggests a push toward fine-grained resource management for ephemeral sessions.
- **Raw-route registry** (#2739) opens NanoClaw to non-Chat-SDK webhooks, hinting at broader integration support.
- **Native channel-instance dimension** (#2733) implies a multi-tenant bot architecture, possibly for hosting multiple agents on one channel.
- **Approval callback registry** (#2737) and delivery action read side (#2734) add observability and extensibility hooks.

The still-open **PR Factory recipe** (#2742) could become a flagship skill if merged, demonstrating agentic CI workflows. The **memory redesign** (#1356) remains the most requested infrastructure change, and given the 6 👍, it may be prioritized in the next minor release.

## 7. User Feedback Summary

While no direct user comments were captured, patterns from issues and PRs indicate:

- **Pain point**: Silent failures (read-only DB, missing side effects) erode trust in commands. The quick fix on #2495 is likely appreciated.
- **Use case demand**: Automated PR review (PR #2742) and multi-bot channels (PR #2733) show users want NanoClaw to handle higher-level workflows.
- **Satisfaction indicator**: The volume of merged PRs (9 in one day) and the rapid turnaround on critical bugs suggests an active, responsive maintainer team.

## 8. Backlog Watch

| Item | Type | Since | Last Update | Reason for Attention |
|------|------|-------|-------------|----------------------|
| [#1356 – Agent memory system redesign](https://github.com/nanocoai/nanoclaw/issues/1356) | Issue | 2026-03-23 | 2026-06-11 | High community interest (6 👍), no formal proposal or PR yet; may require architectural discussion. |
| [#2611 – fix(cli): preserve caller context after approval](https://github.com/nanocoai/nanoclaw/pull/2611) | PR | 2026-05-25 | 2026-06-11 | Security fix (replaying admin context) still open with no merges; critical for multi-user approval workflows. |
| [#2685 – docs(signal): group typing, outbound reactions, quote-reply fix](https://github.com/nanocoai/nanoclaw/pull/2685) | PR | 2026-06-04 | 2026-06-11 | Documentation updates for Signal features; stale for a week with no reviewer activity. |
| [#2744 – fix(signal): deliver agent reactions and forward inbound reactions](https://github.com/nanocoai/nanoclaw/pull/2744) | PR | 2026-06-11 | 2026-06-11 | Recently opened but addresses a high-severity bug; needs prompt review. |

Notably, PR #2611 has been open for over two weeks and deals with security context preservation—an issue that could have real consequences if exploited. The maintainer team may want to prioritize it alongside the Signal fixes.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-06-12

## Today's Overview
Project activity remains very low in the past 24 hours. Only one new issue was opened, describing a functional bug when using local models via Ollama; no pull requests were created, merged, or closed, and no new releases were published. The project appears to be in a quiet maintenance phase with no visible ongoing development or community engagement beyond the single bug report. Overall health is stable but stagnant, with no immediate signs of progress on existing or new features.

## Releases
No new releases in the last 24 hours.

## Project Progress
No pull requests were updated (open, merged, or closed) today. No features, fixes, or improvements were advanced.

## Community Hot Topics
Only one issue was active today, but it has received no comments or reactions yet:
- **#952 [bug] Local model using ollama returns incomplete answers**  
  *Author: bloodgroup-cplusplus* | Created: 2026-06-11 | Updated: 2026-06-11  
  [Link to Issue](https://github.com/nullclaw/nullclaw/issues/952)  
  The user reports that after pulling a Gemma model via Ollama, the agent does not respond in complete sentences. No discussion has begun, so underlying needs (e.g., model compatibility, truncation handling, or configuration issues) are not yet clarified.

## Bugs & Stability
One bug was reported today:
- **#952 – Incomplete answers from Ollama-backed local models**  
  **Severity: Medium** – The issue impacts core functionality (agent output quality) but does not crash the system or cause data loss. No fix PR has been created. The cause is currently unknown; possible factors include prompt truncation, context window limits, or Ollama integration settings.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the reported bug may hint at an underlying need for better documentation or configuration handling for local model deployments (e.g., adjusting temperature, max tokens, or prompt format). If the community engages with the issue, it could steer the roadmap toward improved Ollama/Ollama-compatible model support in the next minor release.

## User Feedback Summary
The only user feedback captured today is a clear pain point: the agent fails to generate complete sentences when using a locally pulled Gemma model via Ollama. The user provided a screenshot (visible in the issue) but no workaround or further context. This suggests dissatisfaction with the out-of-the-box experience for local model users, especially those expecting full conversational coherence.

## Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention were identified in the current data. The sole open issue (#952) was created less than 24 hours ago and has not yet received a maintainer response.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-12

## Today’s Overview

The project is experiencing **very high activity** today: 30 issues and 48 pull requests were updated in the last 24 hours, with 25 PRs merged or closed and 17 issues remaining open. Development continues to concentrate on the **Reborn** binary and WebUI v2, with a strong push toward production readiness, credential/configuration hygiene, and UX refinement. Roughly half of the closed issues today address bugs reported during local testing (e.g., credential persistence, SSO setup, model picker, approval modals), while several new feature / enhancement epics (automated QA, operator log filtering, global tool-approval settings) signal the team is already planning beyond the current stability sprint. No new releases were cut.

## Releases

*None* — no new versions were published in the last 24 hours.

## Project Progress (Merged/Closed PRs Today)

25 PRs reached a merged or closed state. Notable advances:

- **Production cutover & QA**  
  - [PR #4786](https://github.com/nearai/ironclaw/pull/4786) – Promoted `main` to `qa` branch.  
  - [PR #4763](https://github.com/nearai/ironclaw/pull/4763) – Closed production cutover readiness checks for the Reborn binary.  
  - [PR #4769](https://github.com/nearai/ironclaw/pull/4769) – Added 22 deterministic, fully‑mocked end‑to‑end test suites for the Reborn binary.

- **Slack & outbound delivery**  
  - [PR #4757](https://github.com/nearai/ironclaw/pull/4757) – Fixed blank screen when opening triggered runs from the Automations page.  
  - [PR #4782](https://github.com/nearai/ironclaw/pull/4782) – Unifies the outbound state store so WebUI delivery defaults actually reach Slack delivery.

- **Extension & capability handling**  
  - [PR #4744](https://github.com/nearai/ironclaw/pull/4744) – Gated extension activation and hardened GSuite OAuth runtime.  
  - [PR #4784](https://github.com/nearai/ironclaw/pull/4784) – Returns capability runtime unavailability as a tool failure instead of aborting the agent loop.

- **Documentation & tooling**  
  - [PR #4781](https://github.com/nearai/ironclaw/pull/4781) – Ported autonomous loop commands (`build` / `deslop` / `review`) from Orchard to the IronClaw Reborn context.

## Community Hot Topics

The most engaged issue by far remains:

- **[#3036 – [EPIC] Configuration-as-Code for IronClaw Reborn](https://github.com/nearai/ironclaw/issues/3036)**  
  *7 comments, 1 👍 | Created Apr 28, updated Jun 11*  
  This long‑running epic proposes declarative tenant blueprints and use‑case harnesses. While it has been quiet for several weeks, the fact that it still receives updates (and 17 open issues today depend on it) shows it is a foundational roadmap item. Community members are likely waiting for a concrete design proposal or a first implementation slice.

Other issues with 2 comments each (moderate engagement):

- **[#4766 – Chat runtime does not use UI‑saved NEAR AI credentials after restart](https://github.com/nearai/ironclaw/issues/4766)** (closed) – A highly relatable pain point that was fixed same‑day.  
- **[#4703 – NEAR AI model picker saves display name instead of model ID](https://github.com/nearai/ironclaw/issues/4703)** (open) – Blocked on a backend fix now included in [PR #4772](https://github.com/nearai/ironclaw/pull/4772).

No pull request received more than a handful of comments; the most active open PRs are large UI fixes and operator‑log wiring.

## Bugs & Stability

The following bugs were **reported today** (ranked by severity):

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| 🔴 High | [#4761](https://github.com/nearai/ironclaw/issues/4761) | Agent stops after repeated tool failures instead of recovering | Open, no fix PR yet |
| 🔴 High | [#4751](https://github.com/nearai/ironclaw/issues/4751) | Large response request fails with “provider tool arguments exceed 16384 bytes” | Open |
| 🔴 High | [#4783](https://github.com/nearai/ironclaw/issues/4783) | WASM extension capabilities with no credentials fail dispatch with “network” error before execution | Open |
| 🟡 Medium | [#4764](https://github.com/nearai/ironclaw/issues/4764) | Denying shell approval leaves tool invocation pending with no user feedback | Open |
| 🟡 Medium | [#4762](https://github.com/nearai/ironclaw/issues/4762) | Failed tool workflow causes follow‑up messages and activity ordering to become inconsistent | Open |
| 🟡 Medium | [#4759](https://github.com/nearai/ironclaw/issues/4759) | Workspace path is duplicated when using workspace‑relative paths | Open |
| 🟡 Medium | [#4770](https://github.com/nearai/ironclaw/issues/4770) | Tool activity may stop updating after refresh (possible SSE reconnect issue) | Open |
| 🟢 Low | [#4748](https://github.com/nearai/ironclaw/issues/4748) | “Wrap / No Wrap” toggle has no visible effect in code blocks | Open |

Several high‑severity bugs are still unaddressed. A batch UI fix ([PR #4772](https://github.com/nearai/ironclaw/pull/4772)) resolves the model‑picker bug (#4703) plus other WebChat v2 glitches, and [PR #4760](https://github.com/nearai/ironclaw/pull/4760) wires the operator‑log page, but core agent‑loop recovery and large‑response handling remain gaps.

## Feature Requests & Roadmap Signals

- **[#4776 – Add global Always Allow setting for eligible tools](https://github.com/nearai/ironclaw/issues/4776)** (open, parent #4692) – Users want a “trust this agent/extension” toggle instead of approving every tool call. Likely to land in the next UI milestone.
- **[#4775 – Epic: Automated QA for the Reborn binary](https://github.com/nearai/ironclaw/issues/4775)** (open) – Formalizing the testing strategy; already partially implemented by today’s merged test suites.
- **[#4771 – Follow‑up: add run/thread‑scoped operator log filtering](https://github.com/nearai/ironclaw/issues/4771)** (open) – After wiring logs in #4760, the next step is per‑run filtering. A clear near‑term enhancement.
- **[#4750 – Workspace files are not discoverable from WebUI](https://github.com/nearai/ironclaw/issues/4750)** (open) – Users cannot view files created by the agent in the WebUI. This is a UX gap that could block advanced workflows.
- **Closed feature issues today**:  
  [#4595](https://github.com/nearai/ironclaw/issues/4595) (runtime readiness APIs) and [#4593](https://github.com/nearai/ironclaw/issues/4593) (effective config API) were both closed, indicating the operator‑facing APIs are now delivered.

The next version will likely include the config‑APIs, improved log visibility, and the global tool‑approval setting. The Configuration‑as‑Code epic (#3036) may start landing as an RFC or experimental feature.

## User Feedback Summary (Real Pain Points)

Based on today’s issues and comments, users are:

- **Relieved** that credential persistence after restart ([#4766](https://github.com/nearai/ironclaw/issues/4766)) and SSO setup ([#4705](https://github.com/nearai/ironclaw/issues/4705)) are now fixed – these were blocking first‑run experience.
- **Frustrated** by the agent’s inability to recover from tool failures ([#4761](https://github.com/nearai/ironclaw/issues/4761)) and by large‑response failures ([#4751](https://github.com/nearai/ironclaw/issues/4751)). These represent core reliability concerns.
- **Confused** by approval modals that lack context ([#4701](https://github.com/nearai/ironclaw/issues/4701) closed today) and by the model picker showing friendly names instead of IDs ([#4703](https://github.com/nearai/ironclaw/issues/4703) still open).
- **Wanting** workspace file visibility ([#4750](https://github.com/nearai/ironclaw/issues/4750)) and a global “always allow” setting for trusted tools ([#4776](https://github.com/nearai/ironclaw/issues/4776)).

Overall, the community is actively testing the Reborn WebUI v2 and providing actionable bug reports, which the team is addressing quickly – the gap between report and fix is often less than 24 hours.

## Backlog Watch

Issues or PRs that appear stale or need maintainer attention:

- **[#3036 – EPIC Configuration-as-Code](https://github.com/nearai/ironclaw/issues/3036)** – Last updated Jun 11 but created in April. Despite high activity elsewhere, this foundational epic has no associated implementation PR. If it remains a priority, maintainers should share a design timeline.
- **[#4108 – Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)** – Opened May 27, last updated Jun 11 but with **zero comments** from maintainers. A persistent CI failure without triage is a red flag for release confidence.
- **[#3708 – chore: release](https://github.com/nearai/ironclaw/pull/3708)** – Open since May 16, this release PR contains breaking API changes for two crates (`ironclaw_common`, `ironclaw_skills`). It could be blocking downstream consumers but appears to have no recent maintainer activity.
- **[#4588 – observability seams (trajectory observer + LLM provider injection)](https://github.com/nearai/ironclaw/pull/4588)** – Open since Jun 9 with no comments from core team. This PR enables external benchmarking and is a genuine contributor effort that risks bit‑rot.

These items should be reviewed for prioritisation or closure to avoid accumulating technical debt.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-12

## Today’s Overview

The project saw a surge of activity, with 16 pull requests updated (15 merged/closed) and 2 open issues. No new releases were published. The high close‑rate indicates the team is aggressively merging fixes and incremental features after a period of development. Notable work includes real‑time ASR voice input for Cowork, model failover, Gmail email triggers, and several stability patches (timeout extension, heap limit, race‑condition fixes). Two user‑reported issues remain open, one of which highlights a possible token‑wasting bug and the other a long‑standing feature request for multi‑agent collaboration.

## Releases

None.

## Project Progress

The following features and fixes advanced or were completed today (all merged/closed PRs, unless noted):

**New Features**
- **Real‑time ASR voice input (#2148)** – Adds a streaming WebSocket‑based ASR mode to Cowork voice input, with configurable “voice input mode” and i18n support.  
- **HTML share access mode selection (#2146)** – Allows choosing between share‑code or public access when creating/updating HTML shares.  
- **Automatic model failover (#1483)** – On transient errors (rate limits, timeouts), the system retries with a user‑configured fallback model.  
- **Gmail email trigger (#1484)** – Polls Gmail API to automatically start agent sessions on new emails (desktop‑native, no Pub/Sub infra).  
- **Skill hover tooltip (#1459)** – *Open (stale)* – Adds a rich tooltip showing full skill name, official badge, and description on hover.

**Bug Fixes & Stability**
- **Extend pre‑send model sync timeout to 90s (#2152)** – Prevents dropped messages on slow gateways (observed 35–107s).  
- **Raise OpenClaw gateway heap limit (#2149)** – Reduces OOM crashes under long‑running multi‑channel workloads.  
- **Prevent stopped startup turns from sending chat (#2147)** – Cancels turn startup if user stop arrives early.  
- **Keep expert suite controls sticky (#2150)** – Fixes scrolling issues in the expert suite page.  
- **Fix NSIS destructive init & redesign engine loading page (#2142)** – Windows installer fix.  
- **CopyButton timer memory leak (#1478)** – Cleans up timers on unmount.  
- **Reject duplicate skill folders on install (#1479)** – Prevents `name-1`, `name-2` duplicates.  
- **Toast & refresh after skill install (#1480)** – Shows success notification and updates skill list.  
- **Scroll‑friendly active skill chips (#1481)** – Horizontal scroll for skill badges in prompt bar.  
- **Fix scheduled tasks description & enabled state overwrite (#1482)** – Preserves user’s description and enabled flag when editing task time.

All links: [PR #2152](https://github.com/netease-youdao/LobsterAI/pull/2152), [#2148](https://github.com/netease-youdao/LobsterAI/pull/2148), [#2146](https://github.com/netease-youdao/LobsterAI/pull/2146), etc.

## Community Hot Topics

**Issue #1462** – *“Feature request: per‑agent model binding & multi‑agent collaboration”*  
Created 2026-04-04, updated 2026-06-11, 2 comments.  
The user praises LobsterAI’s multi‑instance IM channels and asks for (1) each agent to bind its own model, and (2) a “room/manager” pattern where a main agent can orchestrate others. They note that a competing product (Hiclaw) has inferior UX. This is a long‑standing request with no official response yet.  
[Issue #1462](https://github.com/netease-youdao/LobsterAI/issues/1462)

**Issue #2121** – *“Suspected bug: repeated output wasting tokens”*  
Created 2026-06-07, updated 2026-06-11, 1 comment.  
The user reports that the agent appears to repeat text, leading to excessive token consumption. They ask if it’s a Claw problem and how to resolve. No maintainer reply yet.  
[Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121)

## Bugs & Stability

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| Medium | #2121 | Repeated output may waste tokens | None yet |
| Low | #2152 (fix) | Pre‑send model sync timeout too short | Merged |
| Low | #2149 (fix) | OpenClaw gateway OOM under heavy load | Merged |
| Low | #2147 (fix) | Startup turn race on user stop | Merged |
| Low | #1478 (fix) | CopyButton memory leak on unmount | Merged |

The only unaddressed bug is #2121. All other issues detected in the field have been resolved by today’s merged PRs.

## Feature Requests & Roadmap Signals

- **Per‑agent model binding & multi‑agent orchestration (#1462)** – Most requested feature. Given the concurrent work on Cowork voice, model failover, and share modes, a “room/manager” system may appear in the next major release (e.g., 4.4).  
- **Gmail email trigger (#1484)** – Already merged, showing the team is expanding automation.  
- **Real‑time ASR (#2148)** – Adds parity with voice interfaces; likely to be standard in future releases.  
- **Skill tooltip (#1459)** – Stale PR, but if merged would improve UX for skill selection.

Predictions: Next minor release will likely include the failover, Gmail trigger, ASR, and share‑access mode. Multi‑agent features may follow in a future major update.

## User Feedback Summary

Pain points expressed in open issues:
- **Token waste** (#2121): A user suspects repeated output is burning tokens, affecting cost and utility.
- **Feature gaps** (#1462): User desires per‑agent model control and multi‑agent collaboration, explicitly stating LobsterAI’s UX is superior to competitors’.
- **Satisfaction**: The same user (#1462) appreciates the current multi‑instance IM feature, indicating general satisfaction with the product direction.

## Backlog Watch

| Item | Type | Status | Last Update | Notes |
|------|------|--------|-------------|-------|
| #1462 | Issue | Open, stale | 2026-06-11 | No maintainer response in 2+ months. High‑impact feature request. |
| #1459 | PR | Open, stale | 2026-06-11 | Skill tooltip feature, last activity March. Needs review/merge. |
| #2121 | Issue | Open, new | 2026-06-11 | Bug report with no maintainer reply. Low severity but user waiting. |

These items require maintainer attention to avoid community frustration. In particular, #1462 is a popular feature request that could shape the product roadmap.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-12

## Today’s Overview
Activity over the past 24 hours remained low but focused. One new bug report was opened regarding Fastmail MCP authorization, and one pull request was submitted to fix a WhatsApp message delivery issue. No releases were published, and no PRs were merged or closed. The project appears stable with incremental maintenance, though community engagement is light. Overall health is neutral — no regressions introduced, but no new features landed either.

## Releases
None.

## Project Progress
- **No PRs were merged or closed** today.  
- **Open PR #1116** (`fix(whatsapp): deliver replies to @lid chats via PN JID rewrite`) by juanlotito targets a critical WhatsApp delivery bug where replies to privacy‑enabled `@lid` chats were silently dropped. The proposed fix rewrites the JID used for push notifications. This is the only active PR and, if merged, would resolve a significant user‑facing issue.  
  [View PR #1116](https://github.com/moltis-org/moltis/pull/1116)

## Community Hot Topics
- **Issue #1115** – **[Bug]: Fastmail MCP Authorisation**  
  Reported by kmath313 with a detailed preflight checklist (confirmed using latest version). The issue likely concerns authentication handshake or token handling with Fastmail’s MCP service. It has received 1 comment so far, suggesting at least one other user or maintainer has engaged. Given the specificity of the title, this may affect users integrating Moltis with Fastmail.  
  [View Issue #1115](https://github.com/moltis-org/moltis/issues/1115)

No other issues or PRs accumulated significant discussion or reactions today.

## Bugs & Stability
| Bug | Severity | Status | Fix PR? |
|-----|----------|--------|---------|
| **#1115 – Fastmail MCP Authorisation** | Medium (affects a specific integration, no reports of crashes) | Open, no reproduction steps yet | No |
| **#1116 (underlying bug) – WhatsApp @lid chats replies dropped** | High (messages lost without error) | Open but fix PR exists (#1116) | Yes – #1116 |

The WhatsApp delivery bug is more severe from a user perspective, but a targeted fix is already proposed. The Fastmail authorization issue is isolated and requires further investigation.

## Feature Requests & Roadmap Signals
No explicit feature requests were submitted in the last 24 hours. The only actionable item is the WhatsApp delivery fix, which is a bug fix rather than a new feature. No roadmap signals (e.g., discussion of upcoming releases, milestones) were present in the data.

*Prediction:* The next release will likely include PR #1116 (WhatsApp fix) and potentially a resolution for issue #1115 if a simple patch is identified. No major feature additions are indicated.

## User Feedback Summary
- **Pain point (WhatsApp):** Replies to privacy‑mode contacts (`@lid` chats) are never delivered. The agent generates responses visible in the web UI, but the outbound message is silently lost — no `Delivered` receipt and no error. This is a clear user‑experience issue affecting reliability.
- **Pain point (Fastmail MCP):** Authorization failure when using Moltis with Fastmail’s MCP (likely a custom tool or integration). The reporter has not provided full session context, but the issue is acknowledged.
- **Satisfaction indicators:** No positive feedback or thanks were recorded today.

## Backlog Watch
No long‑unanswered issues or PRs were identified in today’s data. The two active items (#1115 and #1116) are both recent and have received maintainer or author attention. No items appear to be neglected.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-12

> **Data Source:** GitHub repository `agentscope-ai/CoPaw` (referenced as `QwenPaw` in issues/PRs)  
> **Analysis Period:** 2026-06-11 00:00 UTC – 2026-06-12 12:00 UTC

---

## 1. Today's Overview

CoPaw saw **intense activity** over the past 24 hours: **34 issues** updated (21 open, 13 closed) and **42 PRs** updated (24 open, 18 merged/closed), alongside **two patch releases** (v1.1.11.post1 and v1.1.11.post2). The project is actively addressing a surge of **desktop client stability bugs**—including SSL certificate failures, infinite process spawning, and memory exhaustion—while also progressing on major architectural shifts like the **AgentScope 2.0 backend migration** (Issue #4727) and a **Runtime 2.0 modular redesign** (PR #5078). Two new patches were shipped to fix tool-card UI rendering and revert a broken conda-unpack fix. Overall, the project is in a **high-velocity, high-bug-report** phase, with maintainers responding quickly but desktop reliability remains a pressing concern.

---

## 2. Releases

### v1.1.11.post2
- **Date:** 2026-06-11  
- **Changelog:**  
  - `style`: Truncate tool card titles to single line with ellipsis (@zhaozhuang521, PR #5119)  
  - `chore`: Bump version to 1.1.11post2 (@rayrayraykk, PR #5124)  
- **Breaking changes:** None  
- **Migration notes:** No migration steps required; this is a hotfix for UI styling.

### v1.1.11.post1
- **Date:** 2026-06-11  
- **Changelog:**  
  - `chore`: Bump version to 1.1.11.post1 (@rayrayraykk, PR #5093)  
  - `Revert "fix(pack): compile-check discord after conda-unpack"` – a previous fix that caused regressions was rolled back (@rayrayraykk, PR #5092)  
  - `Chore`: Release duty checklist updates  
- **Breaking changes:** None  
- **Migration notes:** Users who manually applied the conda-unpack fix may need to revert; otherwise, no action needed.

**Full release notes:**  
- [v1.1.11.post2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11.post2)  
- [v1.1.11.post1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.11.post1)

---

## 3. Project Progress

### Merged / Closed PRs (18 total, most notable):

| PR | Title | Status | Type |
|----|-------|--------|------|
| [#5124](https://github.com/agentscope-ai/QwenPaw/pull/5124) | chore: bump version to 1.1.11post2 | Merged | Maintenance |
| [#5126](https://github.com/agentscope-ai/QwenPaw/pull/5126) | Release Duty v1.1.11.post2 — Installation Verification | Closed (verified) | Release process |
| [#5028](https://github.com/agentscope-ai/QwenPaw/pull/5028) | fix(security): isolate keychain master key per install | Merged | Security fix |
| [#5133](https://github.com/agentscope-ai/QwenPaw/pull/5133) | feat(ui): apply AionUi design language to Console layout | Merged | UI enhancement |
| [#5134](https://github.com/agentscope-ai/QwenPaw/pull/5134) | feat(.claude): qwenpaw-changelog historian agent for dev pipeline | Merged | Developer tooling |
| [#5136](https://github.com/agentscope-ai/QwenPaw/pull/5136) | feat(i18n): completa tradução pt-BR do workspace | Merged | Localization |

### Key advances in the pipeline (still open but active):

- **Runtime 2.0** (PR #5078) – modular runtime replacing monolithic `Runner` + `stream_query`; introduces `ToolCoordinator`. Under review.
- **Agent OS Driver** (PR #5067) – unified abstraction for MCP/A2A/ACP protocols. Under review.
- **Plugin loader decoupling** (PR #4900) – fixes plugin boot in frozen environments. Still open after 10 days.
- **Langfuse trace grouping** (PR #5128) – groups agent loops into a single trace. New today, open.
- **Session filename deduplication & Desktop inter-agent call fix** (PR #5036) – targets Issue #4988. Open.

---

## 4. Community Hot Topics

### Most Active Issues (by comment count):

| Issue | Title | Comments | Status |
|-------|-------|----------|--------|
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | [Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0 | 9 | Open |  
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | [Bug]: Scheduled tasks created by agent cannot trigger | 8 | Open |  
| [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) | [Bug]: Tauri SSL certificate error + infinite processes + PyInstaller fail | 7 | Closed |  
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | [Bug]: Local Qwen 3.6-27B model no response after upgrade to 1.1.9/1.1.10 | 6 | Closed |  
| [#3817](https://github.com/agentscope-ai/QwenPaw/issues/3817) | [Question]: Long-term memory vector model config resets on restart | 5 | Closed |  
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | [Bug]: OpenSSL 3.5 regression prevents Desktop startup | 5 | Closed |  
| [#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095) | [Bug]: Windows v1.1.11 desktop client cannot start | 5 | Closed |  

**Analysis:**  
- **#4727** is the most “liked” (👍2) and discussed – the planned **AgentScope 2.0 migration** is a fundamental architectural change that will affect all users; community interest is high.  
- **#5064** (scheduled tasks not triggering) reflects a core agent capability gap that impacts automation workflows – users are frustrated by the lack of manual overrides.  
- The **three desktop bugs (#5106, #5086, #5095) were all closed quickly**, indicating maintainer responsiveness, but their recurrence across versions signals deeper packaging/infrastructure issues.

### Most Active PRs (by comments, though not listed in data – we infer from activity):

- [#5028](https://github.com/agentscope-ai/QwenPaw/pull/5028) (keychain isolation) was merged – security fix with broad impact.  
- [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) (per-turn token popover) is new and addresses a requested feature.  
- [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) (Agent OS Driver) has a `first-time-contributor` label and is under review – could attract external contributors.

---

## 5. Bugs & Stability

### Reported today (2026-06-12) – ranked by severity:

| # | Issue | Severity | Description | Fix PR exists? |
|---|-------|----------|-------------|----------------|
| [🔴 #5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) | **Critical** | Windows client processes increase continuously, memory >90% | No fix PR yet |
| [🔴 #5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | **High** | v1.1.11.post2 attachment download broken for non-text files (404 error) | No fix PR yet |
| [🟡 #5142](https://github.com/agentscope-ai/QwenPaw/issues/5142) | **Medium** | Coding Mode session lost on page refresh | No fix PR yet |
| [🟡 #5143](https://github.com/agentscope-ai/QwenPaw/issues/5143) | **Medium** | Math formula (root symbol) rendering broken in web UI | No fix PR yet |
| [🟡 #5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) | **Medium** | Memory config lost when collapsed card not expanded before save | ✅ PR #5144 (Fix/collapse forcerender memory config loss) |
| [🟢 #5127](https://github.com/agentscope-ai/QwenPaw/issues/5127) | **Low** | Langfuse traces fragmented across single agent loop | ✅ PR #5128 (group langfuse observations) |
| [🟢 #5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) | **Low** | Context compression stats mismatched with actual API input | No fix PR yet |

### Regression highlights:

- **Windows process leak (#5138)** – reported only today, but likely related to the earlier `#5106` issue (infinite processes) that was closed – may not be fully resolved.  
- **Attachment download (#5140)** – a regression in 1.1.11 that was partially fixed (plain text works) but still broken for docx/pdf.  
- **Memory config loss (#5137)** – a UI logic bug where collapsed panels cause form values to be lost on save; a fix PR (#5144) was opened the same day.  
- **OpenSSL regression (#5086)** – closed, but its root cause (OpenSSL 3.5.7) may resurface in other packaged environments.

---

## 6. Feature Requests & Roadmap Signals

### Requests opened/updated today:

| # | Feature Request | Comments | Likelihood for next version |
|---|----------------|----------|-----------------------------|
| [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | Agent Team / Swarm Collaboration (multi-agent orchestration) | 1 | Medium – aligns with PR #5067 (Agent OS Driver) |
| [#5131](https://github.com/agentscope-ai/QwenPaw/issues/5131) | Code completion in Coding Mode | 1 | Low – requires IDE integration |
| [#5116](https://github.com/agentscope-ai/QwenPaw/issues/5116) | Configurable chat interaction modes (interrupt, steering, queue) | 1 | Medium – similar to #5103 |
| [#5110](https://github.com/agentscope-ai/QwenPaw/issues/5110) | Quote/reference text from responses (like Perplexity) | 1 | Low – UI-only enhancement |
| [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103) | Conversation queue, token stats, accurate timestamps | 2 (👍1) | High – PR #5130 already adds token popover |
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | Integrate Headroom context compression (60–95% token reduction) | 3 | Medium – would benefit plugin ecosystem |
| [#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887) | Custom endpoint for DingTalk private deployment | 3 | Low – enterprise niche |

### Roadmap signals:

- **AgentScope 2.0 migration (#4727)** is confirmed as a planned breaking change – will likely ship as v1.2.0 or higher.  
- **Runtime 2.0 (PR #5078)** and **Agent OS Driver (PR #5067)** are under active review; these could land in the next minor release.  
- The **skill market update (PR #5123)** is new and adds QwenPaw platform support – could be released as part of v1.1.12.

---

## 7. User Feedback Summary

**Pain points (high dissatisfaction):**

- **Desktop client reliability** – multiple users report crashes, startup failures, memory leaks, and process flooding on Windows. “新版本 … 电脑黑屏死机，完全无法使用” (new version causes black screen, completely unusable).  
- **Attachment handling regression** – broken download for docx/pdf in v1.1.11.post2 forces users to downgrade to v1.1.10.  
- **Memory configuration loss** – users must manually expand collapsed cards to avoid losing vector model settings; reported as a “sneaky” bug.  
- **Scheduled tasks unusable** – agent-created cron tasks do not trigger and cannot be edited, breaking automation workflows.  

**Positive signals:**

- The new UI (v1.1.11) is described as “简洁” (clean/simple), but users want it to be functional.  
- **Token and context usage display** (PR #5130) directly addresses a long-standing request from #5103 – users will welcome this.  
- **Community localization** (pt-BR PR #5136) shows growing international adoption.  

**Missing features users frequently ask for:**

- Conversation queue (chaining multiple inputs without waiting)  
- Real-time token statistics and timestamps  
- Multi-agent team collaboration (swarm)  
- Code completion in coding mode  

---

## 8. Backlog Watch

### Issues needing maintainer attention (inactive for >7 days):

| # | Issue | Last Updated | Days Idle | Reason |
|---|-------|--------------|-----------|--------|
| [#3817](https://github.com/agentscope-ai/QwenPaw/issues/3817) | Memory vector model config reset on restart | 2026-06-11 | 48 days since creation, closed yesterday but root cause may persist | Similar to #5137;

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-12

## Today’s Overview

ZeroClaw remains in a period of intense development following the release of **v0.8.0**, which introduces multi-agent daemon support, per-agent workspaces and memory, and a rewritten configuration schema with automatic migration. Activity is extremely high: 50 issues and 50 pull requests were updated in the last 24 hours, with 48 open issues remaining active, 47 open PRs awaiting review or author action, and three PRs merged/closed. The project is stabilizing after a major architectural shift, but numerous high-severity bugs and feature requests signal that v0.8.x will require several patch releases to reach full reliability. Community engagement is strong, with long-running discussions around memory consolidation, MCP tool filtering, and multi-agent delegation.

## Releases

**v0.8.0** — the “big one” released today.  
Key changes:
- A single daemon now manages many **named agents**, each with its own workspace, memory, model provider, security policy, channels, and personality.
- The configuration schema has been **rewritten**; existing setups are **migrated automatically** on first run.
- New coordination layer for multi-agent scenarios.

*No breaking changes listed in the release notes beyond the schema migration, which is automatic. Users should verify their custom agent configs after upgrade.*

## Project Progress

Three pull requests were merged/closed today, all landing on `master`:

- **[PR #7517](zeroclaw-labs/zeroclaw/pull/7517)** (merged) – Fix runtime/subagent: inherit ACP session `cwd` into `spawn_subagent` and `delegate`. Resolves a workflow-blocking bug where subagents ignored the client-supplied working directory.  
- **[PR #7519](zeroclaw-labs/zeroclaw/pull/7519)** (merged) – Fix config persistence: the per-field `[[mcp.servers]]` editor now correctly writes incremental changes to disk via a natural-key dirty-path walker.  
- **[PR #7520](zeroclaw-labs/zeroclaw/pull/7520)** (merged) – CI: install cross g++ for ARM glibc release builds, fixing v0.8.0 release pipeline failures on aarch64/armv7/arm targets.

Two issues were closed:
- **[Issue #7112](zeroclaw-labs/zeroclaw/issues/7112)** – v0.8.0 release queue tracker (stable-tier blockers resolved).  
- **[Issue #7263](zeroclaw-labs/zeroclaw/issues/7263)** – Subagent `cwd` inheritance bug, fixed by PR #7517.

## Community Hot Topics

The following issues and PRs attracted the most discussion and reactions:

- **[#5849 Dream Mode — Periodic Memory Consolidation](zeroclaw-labs/zeroclaw/issues/5849)** *(17 comments)*  
  A long-running feature request for a background process that consolidates daily memories and updates long-term knowledge. Accepted as `status:accepted` and tagged `priority:p2`. No PR yet, but high community interest.

- **[#6699 tool_filter_groups is a no-op for real MCP tools](zeroclaw-labs/zeroclaw/issues/6699)** *(7 comments)*  
  Two distinct bugs cause the documented `[agent] tool_filter_groups` to have zero effect on MCP tool surfaces. Tagged `priority:p1, status:in-progress`. A fix is being actively worked on.

- **[#7470 Delegate agentic mode rejects empty risk_profile.allowed_tools](zeroclaw-labs/zeroclaw/issues/7470)** *(7 comments)*  
  Newly filed S1 (workflow blocked) bug affecting multi-agent delegation when target agents have empty `allowed_tools`. Coupled with same-profile gating issues. Opened just today; no fix PR yet.

- **[#5542 Consecutive OOM in WSL2](zeroclaw-labs/zeroclaw/issues/5542)** *(4 comments)*  
  S0 (data loss / security risk) memory exhaustion bug. Still awaiting reproduction (`r:needs-repro`).

- **[#6302 Gemini 400 — history serializer violation](zeroclaw-labs/zeroclaw/issues/6302)** *(4 comments)*  
  Provider-specific bug where conversation history places tool calls before first user turn. PR #6303 exists but is stalled (needs-author-action).

- **[#6312 Per-alias webhook path routing](zeroclaw-labs/zeroclaw/issues/6312)** *(4 comments)*  
  Enhancement request for multi-instance channels. Alternative mechanism (`?agent=`) landed in #7297, but path routing remains desired.

- **[#6391 Real heartbeat tracking for daemon nodes](zeroclaw-labs/zeroclaw/issues/6391)** *(4 comments)*  
  Feature request for liveness detection beyond registry presence. Blocked pending node infrastructure.

## Bugs & Stability

**New high-severity bug reported today:**

- **[#7470](zeroclaw-labs/zeroclaw/issues/7470)** (S1) – Delegate agentic mode rejects empty `risk_profile.allowed_tools` and gating blocks stricter targets. *No fix PR yet.*

**Previously reported but still active high-severity bugs (updated today):**

- **[#5542](zeroclaw-labs/zeroclaw/issues/5542)** (S0, `r:needs-repro`) – Consecutive OOM in WSL2. Memory leak suspected.  
- **[#5808](zeroclaw-labs/zeroclaw/issues/5808)** (S1) – Default 32k context budget exceeded by system prompt + tools from iteration 1, causing perpetual preemptive trim.  
- **[#5903](zeroclaw-labs/zeroclaw/issues/5903)** (S1) – MCP stdio child processes leak one orphan per heartbeat tick when `heartbeat.enabled=true`.  
- **[#6037](zeroclaw-labs/zeroclaw/issues/6037)** (S1) – Cron jobs launched repeatedly while running (burst execution). PR #6038 exists to add claim lock.  
- **[#6302](zeroclaw-labs/zeroclaw/issues/6302)** (S1) – Gemini 400 due to conversation history ordering. PR #6303 exists but stale.  
- **[#6350](zeroclaw-labs/zeroclaw/issues/6350)** (S2) – WhatsApp Web allowed-numbers bypassed for LID-based contacts; silent message drops.  
- **[#6361](zeroclaw-labs/zeroclaw/issues/6361)** (S1) – Context compression drops `assistant(tool_calls)` and `tool(result)` for OpenAI-compatible providers (e.g. MiniMax), causing tool loops.  
- **[#6434](zeroclaw-labs/zeroclaw/issues/6434)** (S1) – Shell tool calls refused at autonomy level `"full"` – `tool_dispatch` never reaches runtime.  
- **[#6678](zeroclaw-labs/zeroclaw/issues/6678)** (S1) – Skill tools rejected by Anthropic API due to generated tool names violating `^[a-zA-Z0-9_-]{1,128}$`.  
- **[#6699](zeroclaw-labs/zeroclaw/issues/6699)** (S1) – `tool_filter_groups` no-op for MCP tools (two distinct bugs).  
- **[#6914](zeroclaw-labs/zeroclaw/issues/6914)** (S1) – `allowed_tools / denied_tools` not enforced at execution time (blocked).

Fix PRs exist for some: #6038 (cron lock), #6303 (Gemini history), #7517 (subagent cwd, closed today). Many others lack active PRs.

## Feature Requests & Roadmap Signals

**Active accepted features (likely for v0.8.x or v0.9.0):**

- **[#5849](zeroclaw-labs/zeroclaw/issues/5849)** – Dream Mode: periodic memory consolidation & reflective learning. Accepted but no PR yet.  
- **[#6312](zeroclaw-labs/zeroclaw/issues/6312)** – Per-alias webhook path routing for multi-instance channels. Alternative mechanism shipped; path routing still desired.  
- **[#6391](zeroclaw-labs/zeroclaw/issues/6391)** – Real heartbeat tracking for daemon nodes (Online/Stale/Offline). Blocked on #6346.  
- **[#6390](zeroclaw-labs/zeroclaw/issues/6390)** – `zeroclaw node add <url>` CLI for remote daemon registration. Blocked on #6346.  
- **[#6346](zeroclaw-labs/zeroclaw/issues/6346)** – `zeroclaw node` CLI + dashboard health management. Blocked (previous attempts closed).  
- **[#6365](zeroclaw-labs/zeroclaw/issues/6365)** – Dashboard “Update ZeroClaw” button exposing `zeroclaw update` via gateway. In progress.  
- **[#6642](zeroclaw-labs/zeroclaw/issues/6642)** – OTel GenAI spans capturing full prompt/completion. In progress; contributed downstream.  
- **[#6823](zeroclaw-labs/zeroclaw/issues/6823)** – TUI ACP Bridge (client-side connection layer for TUI daemon interaction). Tracker for client-side work.

**Prediction for next version (v0.8.1 / v0.9.0):**  
Heartbeat tracking, node CLI, and Dream Mode are all `status:accepted` and have high community traction. However, the sheer volume of P1 bugs may delay new features until stability improves. We expect the next minor release to focus on bug fixes and MCP reliability.

## User Feedback Summary

**Common pain points expressed in recent issues:**

- **Multi-agent delegation and tool filtering** (#7470, #6699, #6914) – Users deploying multiple agents face blocked workflows when delegating across security profiles.
- **MCP tool unreliability** (#5903 – orphan processes, #6699 – filter no-op) – MCP integrations are a key use case; current bugs undermine trust.
- **Provider-specific issues** – Gemini, Anthropic, MiniMax all have distinct serialization/invocation bugs (#6302, #6361, #6678).
- **Context budget mismanagement** (#5808) – Default budget forces trim on turn 1, frustrating users with complex tool sets.
- **Cron and channel delivery** (#6037, #6350, #6224) – Cron bursts, WhatsApp filtering bypass, and missing delivery channel support cause production outages.
- **Windows and subprocess environment** (#7214 – Claude Code on Windows; #7263 – subagent cwd) – Cross-platform users encounter path and environment variable gaps.

**Positive signals:** The v0.8.0 release is a major milestone that addresses long-standing multi-agent demands. Users who successfully migrate report improved configurability and per-agent isolation. The community is engaged in reporting and debugging, indicating a healthy user base willing to invest in stability.

## Backlog Watch

Issues and PRs that have been open for extended periods without maintainer action, mostly tagged `needs-author-action` or `stale-candidate`:

- **[#5516](zeroclaw-labs/zeroclaw/pull/5516)** (2026-04-08) – Fuzz stubs not wired to real code paths. Stale for 2+ months.  
- **[#5661](zeroclaw-labs/zeroclaw/pull/5661)** (2026-04-12) – Cron CLI delivery flags (large XL PR). Stale candidate.  
- **[#5892](zeroclaw-labs/zeroclaw/pull/5892)** (2026-04-19) – Three production blockers: tool_choice, orphaned tool_use, vision capability. Stale.  
- **[#6038](zeroclaw-labs/zeroclaw/pull/6038)** (2026-04-23) – Cron claim/release lock (fix for #6037). Needs author action.  
- **[#6085](zeroclaw-labs/zeroclaw/pull/6085)** (2026-04-24) – Default session TTL 168h and trim on seed. Needs author action.  
- **[#6143](zeroclaw-labs/zeroclaw/pull/6143)** (2026-04-26) – Universal skill registry (large XL). Needs author action.  
- **[#6230](zeroclaw-labs/zeroclaw/pull/6230)** (2026-04-30) – WhatsApp cron delivery. Needs author action, stale candidate.  
- **[#6288](zeroclaw-labs/zeroclaw/pull/6288)** (2026-05-02) – Derive systemd unit name from config-dir. Needs author action.  
- **[#6303](zeroclaw-labs/zeroclaw/pull/6303)** (2026-05-03) – Gemini history fix (closes #6302). Stale candidate.  
- **[#6318](zeroclaw-labs/zeroclaw/pull/6318)** (2026-05-03) – `on_before_compaction` hook. Needs author action, stale candidate.

Additionally, several issues have been `status:blocked` for weeks:
- **[#6391](zeroclaw-labs/zeroclaw/issues/6391)** (heartbeat tracking) – Blocked on #6346.  
- **[#6914](zeroclaw-labs/zeroclaw/issues/6914)** (tool filtering enforcement) – Blocked on MCP dispatch refactoring.

**Maintainer attention recommended:**  
- Prioritize review of the three stale P1 fix PRs (#5892, #6038, #6303) that directly address S1 bugs.  
- Unblock #6391/#6346 node infrastructure to enable fleet management features.  
- Triage the 10+ `needs-author-action` PRs to either merge, close, or request updates.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*