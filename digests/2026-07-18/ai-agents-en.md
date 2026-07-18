# OpenClaw Ecosystem Digest 2026-07-18

> Issues: 413 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-18 01:49 UTC

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

# OpenClaw Project Digest – 2026-07-18

## 1. Today’s Overview

The project saw heavy activity on 2026-07-18: **413 issues** updated (245 open, 168 closed) and **500 PRs** updated (297 open, 203 merged/closed). A new beta release, **v2026.7.2-beta.2**, landed with highlights around remote coding sessions and native automation. The community is actively reporting regressions and reliability concerns, especially around Codex-powered sessions, Telegram delivery, and model fallback behavior. Maintainers merged several high-severity fixes and kept CI pipelines running, but many critical issues remain under review.

## 2. Releases

**v2026.7.2-beta.2** (one release in the period)

- **Highlights** (from truncated notes):  
  - Remote coding sessions: run Control UI sessions on cloud workers; open Codex and Claude catalog sessions in terminals; resume OpenCode and Pi sessions directly in a terminal.  
  - Native automation and nodes (details cut short).  
- **Notable:** No breaking changes or migration notes were published alongside this release.  
- **Status:** Beta; users running production workloads should test before upgrading.

---

## 3. Project Progress

**Merged/closed PRs today: 203** (out of 500 total PRs updated). Key examples from the top PR list:

- [#110284](https://github.com/openclaw/openclaw/pull/110284) – Fix: reject malformed MCP App sandbox policies.  
- [#110080](https://github.com/openclaw/openclaw/pull/110080) – Fix: signed thinking replays across providers permanently bricks Claude 5 sessions (fixes #110079).  
- [#105860](https://github.com/openclaw/openclaw/pull/105860) – Fix: filter non-string env entries instead of silently deleting entire env block.  
- [#110282](https://github.com/openclaw/openclaw/pull/110282) – Fix(ci): bound git fetch operations with timeout to prevent stuck workflows.  

Many other CI, UI localization, and gateway stability PRs were merged. The team is actively working on session-state safety, plugin compatibility, and test infrastructure.

---

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 114 | 👍 81 | Long-standing request for desktop apps on missing platforms. |
| [#88312 – Codex app-server turn-completion stall regression](https://github.com/openclaw/openclaw/issues/88312) | 21 | 👍 5 | Regression in multi-tool agent turns starting in 2026.5.27. |
| [#7707 – Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) | 18 | 👍 0 | Security feature to prevent memory poisoning. |
| [#87744 – Codex-backed Telegram timeouts](https://github.com/openclaw/openclaw/issues/87744) | 16 | 👍 3 | Turns never reach completion, breaking Telegram sessions. |
| [#10659 – Masked Secrets for API keys](https://github.com/openclaw/openclaw/issues/10659) | 14 | 👍 4 | Security request to hide credentials from agents. |

**Underlying needs**: Users want more operating system coverage (Linux/Windows), better security controls for agent memory and secrets, and reliable Codex integration across all channels.

---

## 5. Bugs & Stability

Several high-severity bugs were reported in the last 24 hours. Below is a ranking by impact:

- **P0** (release-blocker):  
  - [#109867](https://github.com/openclaw/openclaw/issues/109867) – Migration creates index before adding column, blocking gateway startup after beta.2 upgrade.  
  - [#108435](https://github.com/openclaw/openclaw/issues/108435) – Gateway fails to start after update to 2026.7.1 (systemd, Ollama, manual launch).  
  - [#101763](https://github.com/openclaw/openclaw/issues/101763) – Hosted Molty model selector doesn’t persist; API receives malformed model ID.

- **P1** (critical regressions):  
  - [#88312](https://github.com/openclaw/openclaw/issues/88312) – Codex turn-completion stall (regression from 2026.5.27).  
  - [#87744](https://github.com/openclaw/openclaw/issues/87744) – Telegram timeouts with Codex.  
  - [#107873](https://github.com/openclaw/openclaw/issues/107873) – WebChat turns abort after tool failure instead of retrying.  
  - [#106779](https://github.com/openclaw/openclaw/issues/106779) – Local llama.cpp provider fails with parser generation error.

- **Fix PRs exist for some bugs**:  
  - [#110080](https://github.com/openclaw/openclaw/pull/110080) addresses the Claude 5 session bricking (closes #110079).  
  - [#110284](https://github.com/openclaw/openclaw/pull/110284) fixes MCP sandbox policy handling.  
  - [#109959](https://github.com/openclaw/openclaw/pull/109959) fixes connection retention on guarded redirect failures.

The overall stability picture is mixed: many fixes are being pushed, but the volume of P0/P1 regressions suggests the recent beta releases introduced significant breakage.

---

## 6. Feature Requests & Roadmap Signals

Notable requests from the top issues:

- **Cross-platform desktop apps** ([#75](https://github.com/openclaw/openclaw/issues/75)) – Very high demand for Linux/Windows native clients.  
- **Memory Trust Tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) – Tag memory entries by source trust level.  
- **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – Prevent agents from reading raw API keys.  
- **Filesystem Sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) – Configurable allowed/denied paths.  
- **Topic-session families** ([#90916](https://github.com/openclaw/openclaw/issues/90916)) – Isolated context lanes for one assistant.  
- **Streaming TTS pipeline** ([#8355](https://github.com/openclaw/openclaw/issues/8355)) – Sentence-level LLM→TTS→audio for voice calls.

**Likely to appear in next version:** Masked Secrets and Memory Trust Tagging are security-driven and already have “needs-product-decision” labels; they may be prioritized given the community upvotes. The Linux/Windows apps request (#75) is a long-term effort.

---

## 7. User Feedback Summary

**Common pain points** reported by users:

- Codex session reliability (stalls, timeouts, OAuth migration issues) – multiple issues with high engagement.  
- Local model compatibility (llama.cpp, OpenRouter) – static model discovery frustrates fast-moving providers.  
- Telegram duplicate messages and turn completion failures.  
- Loop detection not terminating stuck agents (resource waste).  
- Plugin/core version drift causing silent channel failures.  

**Satisfaction signals**: The release of remote coding session features and continuous fixes show active development. However, the stream of P0/P1 regressions (especially around Codex and migrations) indicates users are frustrated with stability in the latest betas.

**Positive mentions**: Some users appreciate the level of configurability (e.g., fallback chains, subagent isolation) and the responsiveness of the maintainers on fix PRs.

---

## 8. Backlog Watch

Issues and PRs that have been open for a long time or are critical but still awaiting maintainer review:

- [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows Clawdbot Apps (open since Jan 1, 2026; 114 comments; needs product decision).  
- [#7707](https://github.com/openclaw/openclaw/issues/7707) – Memory Trust Tagging (open since Feb 3, 2026; labelled “needs-maintainer-review”).  
- [#10659](https://github.com/openclaw/openclaw/issues/10659) – Masked Secrets (open since Feb 6, 2026; “needs-product-decision”).  
- [#11665](https://github.com/openclaw/openclaw/issues/11665) – Webhook multi-turn support (open since Feb 8, 2026; “needs-maintainer-review”).  
- [#87763](https://github.com/openclaw/openclaw/issues/87763) – SSRF guard DNS dispatcher conflicts (open since May 28; “needs-maintainer-review”).  

These items have been languishing for weeks to months; users are eager for movement, especially on security-related features.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report

**Date:** 2026-07-18  
**Scope:** 11 open-source AI agent/personal assistant projects

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is undergoing a rapid maturation phase, characterized by aggressive feature iteration, security hardening, and platform expansion across a fragmented ecosystem. A clear pattern emerges: the community is converging on multi-agent orchestration, robust channel integrations (Telegram, Discord, WhatsApp, Matrix), and enhanced security controls (memory tagging, secrets masking, sandboxing) as baseline expectations rather than differentiators. However, stability remains a significant pain point, with multiple projects shipping beta releases that introduce critical regressions—particularly in Codex integration, provider fallback logic, and migration tooling. The ecosystem is bifurcating between reference implementations (OpenClaw) that prioritize extensibility and specialized forks (ZeroClaw, IronClaw) that target specific deployment models like enterprise multi-tenancy or hardware-accelerated edge inference. The high volume of community-contributed features across projects signals strong developer engagement, but the accumulation of unresolved P0/P1 bugs in several codebases suggests the pace of innovation may be outpacing quality assurance.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score |
|---------|---------------------|--------------------|----------------|--------------|
| **OpenClaw** | 413 (245 open, 168 closed) | 500 (297 open, 203 merged) | v2026.7.2-beta.2 | **Moderate** – high volume but P0/P1 regressions |
| **NanoBot** | Not reported | 11 (4 merged) | No release | **Good** – fast merge cadence, responsive to API breaks |
| **Hermes Agent** | 50 (43 open, 7 closed) | 50 (49 open, 1 merged) | No release | **At Risk** – high open-to-closed ratio, P1 bugs unfixed |
| **PicoClaw** | 4 (3 open, 1 closed) | 12 (10 open, 2 merged) | No release | **Good** – steady, security-focused |
| **NanoClaw** | 4 (all updated) | 15 (3 merged) | No release | **Good** – healthy triage, active contributors |
| **NullClaw** | 1 (open) | 0 | No release | **Critical** – single crash bug, no maintainer response |
| **IronClaw** | 50 (26 open, 24 closed) | 50 (25 open, 25 merged) | No release (pre-v1) | **Good** – intense refactoring, rapid bug closure |
| **LobsterAI** | 7 (2 open, 5 closed) | 15 (13 merged) | v2026.7.16 | **Excellent** – 87% merge rate, all known bugs closed |
| **TinyClaw** | 0 | 0 | No release | **Dormant** |
| **Moltis** | 1 (open) | 2 (open, 0 merged) | 2 releases (no notes) | **Low** – minimal activity, backlogged feature request |
| **CoPaw** | 25 (15 open, 10 closed) | 40 (17 open, 23 merged) | v2.0.0.post3 | **Good** – high activity, but Windows stability issues |
| **ZeptoClaw** | 8 (all closed) | 0 | No release | **Minimal** – data curation workflow only |
| **ZeroClaw** | 50 (42 open, 8 closed) | 50 (40 open, 10 merged) | No release | **Moderate** – intense but many blocked/long-standing issues |

**Key observation:** LobsterAI leads in delivery efficiency (87% PR merge rate, all known bugs fixed). OpenClaw and ZeroClaw have the highest raw activity but struggle with regression velocity and backlog accumulation.

---

## 3. OpenClaw's Position

OpenClaw serves as the **de facto reference implementation** for the ecosystem, with the largest community (413 issues, 500 PRs in 24h) and the most comprehensive feature surface. Its advantages include:

- **Extensibility-first architecture:** Remote coding sessions, subagent isolation, fallback chains, and MCP sandbox policies provide the deepest configuration surface among peers.
- **Cross-provider support:** Codex, Claude, Ollama, OpenRouter, and local model support create the widest model compatibility in the ecosystem.
- **Community gravity:** The 114-comment Linux/Windows desktop app request (#75) demonstrates unmatched user engagement, though it also highlights a critical platform gap.

**Technical approach differences compared to peers:**
- Unlike **ZeroClaw** (Wasm-first plugin runtime, A2A protocol), OpenClaw relies on a monolithic gateway with plugin-style MCP integration.
- Unlike **IronClaw** (Rust-based, Reborn architecture simplification), OpenClaw uses a Python/JavaScript stack optimized for rapid prototyping over performance.
- Unlike **CoPaw** (Tauri-based desktop, Windows-first), OpenClaw's desktop story is community-driven and incomplete.

**Community size comparison:** OpenClaw's activity volumes (413 issues, 500 PRs) dwarf all peers; the next highest (IronClaw, ZeroClaw) operate at roughly 12% of that volume. However, this scale introduces coordination overhead and regression risk that smaller projects manage better.

**Vulnerability:** OpenClaw's beta.2 release introduced multiple P0 blockers (migration index failure, gateway startup crash, Codex stall regression) that erode trust. Peers like LobsterAI and NanoBot demonstrate that smaller scopes enable higher stability.

---

## 4. Shared Technical Focus Areas

The following requirements emerge across **multiple projects**, indicating ecosystem-wide priorities:

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Memory & Secrets Security** | OpenClaw, PicoClaw, ZeroClaw, CoPaw | Memory trust tagging (#7707), masked secrets (#10659), OAuth refresh concurrency (#3239), per-sender RBAC (#5982) |
| **Multi-Channel Platform Support** | OpenClaw, PicoClaw, NanoClaw, CoPaw, NullClaw | Linux/Windows desktop apps, QQ streaming, WhatsApp typing presence, Discord channel filtering, Matrix stability |
| **LLM Provider Reliability** | OpenClaw, NanoBot, Hermes Agent, NanoClaw, CoPaw | Codex stall/timeout issues, Moonshot API incompatibility, Claude+OpenRouter silent drops, MCP sequential startup |
| **Performance & Memory Efficiency** | IronClaw, CoPaw, ZeroClaw, Moltis | Budget gate store consolidation, MCP parallel startup, Wasm plugin runtime, context window auto-detection |
| **Configuration & Usability** | OpenClaw, Hermes Agent, ZeroClaw, CoPaw | TUI editing (arrow keys), cron documentation, skill harness consistency, capability-aware docs, model-specific cron jobs |
| **Migration & Upgrade Safety** | OpenClaw, IronClaw, CoPaw | v2→v3 config migration, 1.x→2.0 upgrade regressions, v1 naming cleanup, breaking change management |

**Most urgent cross-project trend:** Security-driven features (memory tagging, secrets masking, OIDC, RBAC, supply-chain signing) are the most upvoted and most frequently requested across all projects, indicating that the ecosystem is shifting from "can it work?" to "can we trust it?"

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | CoPaw | NanoBot | Hermes Agent |
|-----------|----------|----------|----------|-------|---------|--------------|
| **Primary language** | Python/JavaScript | Rust | Rust | Python/Tauri | TypeScript | Python |
| **Target user** | Power users, integrators | Enterprise multi-tenant | Performance-sensitive | Windows desktop | Self-hosters, rapid deploy | CLI/automation users |
| **Deployment model** | Gateway + plugins | Wasm runtime | Binary + Reborn engine | Desktop app | Docker / Render | CLI + desktop |
| **Security posture** | Reactive (fix-driven) | Proactive (OIDC, SLSA) | Moderate | Moderate | Minimal | Minimal |
| **Channel breadth** | Broad (Telegram, Codex, web) | Very broad (Discord, Matrix, Inkbox) | Telegram + engine v2 | Broad (QQ, Feishu, webhook) | Moderate (web, CLI) | Moderate (Telegram, web) |
| **Innovation edge** | Remote coding sessions | A2A protocol, pluggable auth | Architecture simplification | AI-generated skins | One-click deploy, new models | Deep CLI automation |
| **Stability vs. Features** | Features > stability (beta regressions) | Balanced but backlogged | Balanced (rapid bug closure) | Features > stability (Windows issues) | Stability-focused | Stability struggling (open PR pile) |

**Key insight:** The ecosystem is **not converging on a single architecture**—it's diverging by deployment context. OpenClaw owns the "anything, anywhere" integrator role; ZeroClaw targets security-conscious organizations; CoPaw aims for desktop consumers; IronClaw optimizes for embedded/edge performance. This diversity is healthy but creates fragmentation for users seeking a single solution.

---

## 6. Community Momentum & Maturity

**Tier 1 – High Momentum, Rapid Iteration (shipping weekly):**
- **OpenClaw** – Massive community, but regression velocity threatens trust. Needs a stability sprint.
- **IronClaw** – Intense refactoring toward v1.0 with clear roadmap (store consolidation, Telegram channel, onboarding).
- **CoPaw** – v2.0 ecosystem, high PR merge rate, but Windows desktop experience is a persistent weak point.
- **ZeroClaw** – Broadest security feature set in development; long-standing blocked issues are the main drag.

**Tier 2 – Steady, Quality-Focused (shipping biweekly):**
- **LobsterAI** – Best stability record in the ecosystem; AI-generated skins signal UI innovation.
- **NanoBot** – Small scope but excellent API responsiveness (Moonshot fix in hours). Growing feature surface.
- **NanoClaw** – Healthy contributor diversity; iMessage unification and skill packs show maturing architecture.
- **PicoClaw** – Security hardening and multi-channel focus. Low volume but deliberate.

**Tier 3 – Slower, Niche or Stalled:**
- **Hermes Agent** – High open PR count and unfixed P1 bugs indicate a review bottleneck.
- **Moltis** – Minimal activity; single feature request (#574) unanswered for 3+ months.
- **NullClaw** – Critical ARM64 crash with no maintainer response; project may be abandoned.
- **ZeptoClaw** – Not a product; data curation workflow only.
- **TinyClaw** – Dormant.

**Maturity verdict:** The ecosystem has one mature flagship (OpenClaw with caveats), several rapidly maturing peers (IronClaw, ZeroClaw, CoPaw), and a long tail of hobby/specialist projects. The gap between Tier 1 and Tier 3 is widening.

---

## 7. Trend Signals

**1. Security Governance is the New Baseline**  
Across OpenClaw (#7707, #10659), ZeroClaw (#5982, #7141, #8177), PicoClaw (#3246), and CoPaw, users consistently rank memory poisoning prevention, credential masking, and multi-tenant RBAC as top priorities. **Implication:** AI agent developers must treat security as a first-class feature, not an afterthought. Projects that fail to implement trust tagging and secrets masking will lose enterprise adopters.

**2. LLM Provider Integration is a Fragile Dependency**  
Codex stalls (OpenClaw #88312, Hermes Agent #66045), Moonshot API breaks (NanoBot #4961), Claude+OpenRouter drops (NanoClaw #3074), and local model parser errors are recurring across projects. **Implication:** The ecosystem is over-reliant on proprietary APIs. Developers should invest in provider-agnostic retry logic, graceful degradation, and local model fallback chains as core platform stability mechanisms.

**3. Multi-Agent Orchestration is the Next Frontier**  
ZeroClaw's A2A protocol (#3566) and multi-agent routing (#2767), CoPaw's bounded multi-agent startup (#6198), and OpenClaw's subagent isolation signals that standalone single-agent assistants are no longer sufficient. **Implication:** Expect rapid standardization around agent-to-agent communication protocols (A2A, MCP) within 6-12 months, similar to the HTTP/API standardization wave of the 2010s.

**4. Cross-Platform Desktop Remains Unsolved**  
Linux/Windows desktop apps (#75, 114 comments), macOS crashing (NullClaw #976, ZeroClaw #7527), and Windows admin privilege issues (CoPaw #6161) are blocking adoption for non-developer users. **Implication:** Tauri-based desktop shells (CoPaw, LobsterAI) are gaining traction; pure-web or CLI-only projects will struggle to reach mainstream users.

**5. Configuration Complexity is a Friction Point**  
Skill docs supporting only one syntax (NanoClaw #3072), cron documentation gaps (ZeroClaw #7762), TUI editing limitations, and migration failures are repeatedly cited across projects. **Implication:** AI agent developers who prioritize "configuration by example" and interactive setup wizards will capture users frustrated by competing projects' YAML/TOML complexity.

**6. Performance at Scale is Emerging as a Priority**  
MCP sequential startup (CoPaw #6193), context window exhaustion (IronClaw #4278), voice call pipeline latency, and bounded startup memory for 36+ agents show that production deployments are stressing current architectures. **Implication:** Wasm-based plugin runtimes (ZeroClaw), store consolidation (IronClaw), and memory strategy decoupling will become differentiators as agent deployments grow beyond single-user hobby projects.

**7. The Value of "Just Works" Cannot Be Overstated**  
LobsterAI's 87% merge rate, zero open bugs, and rapid update cycle contrast sharply with OpenClaw's beta regression parade. **Implication:** In a fragmented ecosystem, the project that delivers the simplest upgrade experience and fastest bug fixes will win the largest share of non-expert users. Stability is becoming a competitive advantage over feature count.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Based on the provided GitHub data for NanoBot (github.com/HKUDS/nanobot), here is the project digest for 2026-07-18.

---

## NanoBot Project Digest: 2026-07-18

### 1. Today's Overview

The project is in a very active development phase, with a high volume of activity split between rapid-fire bug fixes and significant feature work. A total of 11 pull requests were updated, with 4 being merged or closed, indicating a fast merge cadence for critical issues. The community is responsive, with contributors quickly addressing a reported API incompatibility and a maintainer resolving a longstanding architectural coupling. No new releases were cut today, but the codebase is undergoing substantial changes across the provider layer, WebUI, and deployment options.

### 2. Releases

*None.* No new releases were published in the last 24 hours.

### 3. Project Progress

Today, 4 pull requests were merged or closed. The team resolved a critical provider bug and integrated contributions from the community.

- **Critical Provider Fix:** **PR #4962** (closed) and **PR #4967** (closed) were merged to fix a breaking change in the Moonshot API. #4962 corrected the hardcoded temperature for `kimi-k2.6` from `1.0` to `0.6`. This was followed by #4967, which improved the fix by omitting the `temperature` parameter entirely for `kimi-k2.5` and `kimi-k2.6`, allowing the provider to select the correct value based on the mode.
- **WebUI Polish:** **PR #4953** (closed) was merged, adding support for native folder picker bridges in the WebUI, which enhances the user experience for file selection in desktop or hosted environments.
- **Community Localization:** **PR #4958** (closed) was merged, significantly improving the quality of the Traditional Chinese (zh-TW) locale.

### 4. Community Hot Topics

The most active topics today revolve around improving the developer experience and fixing integration blockers.

- **Issue #4968: Unbound cron jobs proposal** ( [View Issue](https://github.com/HKUDS/nanobot/issues/4968) )
    - *Comments: 4* | This issue questions a restriction in the CLI code that prevents the creation of "unbound" cron jobs. The discussion (which reached a conclusion and was closed) indicates a desire for more flexible agent scheduling. The underlying need is for users to run cron jobs attached to a specific agent definition rather than a specific conversation, which is a more modular and powerful use case.
- **PR #4937: One-click Deploy to Render** ( [View PR](https://github.com/HKUDS/nanobot/pull/4937) )
    - *Status: Open* | This feature request, now up for 4 days, is a significant priority for making NanoBot more accessible. It aims to reduce the barrier to entry for non-developers. It has not yet received official approval, suggesting it may be pending a final review from the tagged maintainer.
- **PR #4908: Refactoring built-in channels** ( [View PR](https://github.com/HKUDS/nanobot/pull/4908) )
    - *Status: Open* | This is a large-scale architectural refactor (removing central coupling from channels) that has been open for several days. It is a complex, high-priority (p1) change that has generated discussion and required conflict resolution, indicating it's a core team effort to modernize the plugin system.

### 5. Bugs & Stability

A single critical bug (both discovered and fixed today) is the main stability event.

- **Severity: High**
    - **Bug Report:** **Issue #4961** ([View Issue](https://github.com/HKUDS/nanobot/issues/4961)) reported that the Moonshot API is rejecting all requests for its `kimi-k2.6` model because NanoBot was forcing an incompatible `temperature=1.0` parameter.
    - **Resolution:** This was a breaking change from the upstream provider. The bug was categorized as high severity as it rendered a popular model completely unusable.
    - **Fix PRs:** Two fix PRs were rapidly authored, reviewed, and merged today: **PR #4962** ([View PR](https://github.com/HKUDS/nanobot/pull/4962)) and **PR #4967** ([View PR](https://github.com/HKUDS/nanobot/pull/4967)). The final solution elegantly defers the temperature selection entirely to the Moonshot API for the affected models.

### 6. Feature Requests & Roadmap Signals

Based on open PRs and issues, the next minor version is likely to include the following:

- **New Model and Provider Support:**
    - **PR #4966** ([View PR](https://github.com/HKUDS/nanobot/pull/4966)) - Support for Moonshot's new `Kimi K3` model, including its unique `reasoning_effort` parameter.
    - **PR #4965** ([View PR](https://github.com/HKUDS/nanobot/pull/4965)) - Adding ModelScope as a new provider, which would grant all users access to a wide range of open-source Chinese models.
- **Infrastructure Improvements:**
    - **PR #4937** ([View PR](https://github.com/HKUDS/nanobot/pull/4937)) - The "one-click deploy to Render" feature is a strong signal the project is prioritizing easier self-hosting.
- **User Experience Enhancements:**
    - **PR #4963** ([View PR](https://github.com/HKUDS/nanobot/pull/4963)) and **PR #4964** ([View PR](https://github.com/HKUDS/nanobot/pull/4964)) are both active UI/UX improvements from maintainer `Re-bin`, focusing on a calmer output display, live image generation settings, and better organization of agent outputs.

### 7. User Feedback Summary

- **Pain Points Addressed:**
    - **API Incompatibilities:** User `SkyLeo-ozim` (Issue #4961) experienced a total service failure due to a model API change. The rapid fix within 24 hours highlights a responsive support model for provider-side breaking changes.
    - **Cron Job Flexibility:** The closure of Issue #4968 suggests the team is open to relaxing rigid constraints. This addresses a user need for more advanced automation patterns.
- **Satisfaction Signals:**
    - **Community Contribution:** `PeterDaveHello` contributed a high-quality translation (PR #4958), which is a strong indicator of an engaged and satisfied user base willing to give back to the project.
    - **Feature Requests:** The high number of open feature PRs (e.g., ModelScope, Render deploy, Kimi K3) suggests users are actively building for and investing in the platform's direction.

### 8. Backlog Watch

While the project is very active, two high-priority, long-standing architectural PRs require continued focus:

- **PR #4908: `refactor(channels): make built-in channels self-contained`** ( [View PR](https://github.com/HKUDS/nanobot/pull/4908) )
    - *Priority: p1, Open since 2026-07-13* | This is a major refactor. While it has recent activity and a `conflict` label, its complexity means it needs careful shepherding to avoid breaking the extensive plugin system. It is a critical foundation for future external channel development.
- **PR #4925: `fix(agent): report hard context overflow clearly`** ( [View PR](https://github.com/HKUDS/nanobot/pull/4925) )
    - *Priority: p1, Open since 2026-07-14* | This bug fix for context length handling has been open for several days. Improving the user experience for context overflow errors is important for reliability, especially for users running long, complex agent conversations. It needs to be merged to improve stability signposting.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-18

## Today’s Overview

The project remains highly active with **50 issues and 50 pull requests updated in the last 24 hours**, reflecting a vibrant contributor and user community. The open-to-closed ratio is tilted heavily toward open items (43 open issues, 49 open PRs), with only **1 PR merged or closed** during the period and **7 issues closed**. No new releases were tagged, suggesting the team is currently focusing on bug triage and feature PR preparation rather than cutting a new version. Several **P1 and P2 severity bugs** were filed today, many of which already have associated fix PRs submitted by the same reporter (enzo-adami), signaling a rapid response from maintainers.

## Releases

*None. No new versions were released in the last 24 hours.*

## Project Progress

Only **one pull request was merged or closed** in the last 24 hours, though the exact PR is not identified in the top‑20 comment‑count list. The large volume of open PRs (49) indicates a healthy but potentially backlogged review pipeline. Notable open PRs that advanced today include a cluster of fixes from contributor **enzo-adami** covering auxiliary compression timeouts (#66635), file glob preservation (#66636), compression intent (#66637), Ink workspace dependencies (#66638), one‑shot skills loading (#66639), and reasoning replay contracts (#66640). Other PRs with recent commits address MCP tools for gateway platforms (#65826), desktop macOS permissions (#65220), and cron session reaping (#62663). The sole merge likely addressed one of the closed issues (e.g., #66045 or #66559).

## Community Hot Topics

The most active discussions (measured by comment count) revolve around core regressions and provider bugs:

- **#3523** (6 comments, P2) – `hermes update` regressions after #3492: silent git output and unnecessary stashes. A long‑standing issue (created March 28) still awaiting a decision path.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/3523)

- **#62810** (5 comments, P2) – CLI dispatcher drops integer exit statuses, breaking `set -e` and CI chains.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/62810)

- **#66267** (5 comments, P1) – Multimodal content list crashes and exhausts API budget after vision turns. A **critical bug** already targeted by fix PR #66637.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/66267)

- **#66045** (5 comments, closed) – Codex transport emits over‑length `prompt_cache_key`, causing silent fallback. Marked as closed, likely fixed.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/66045)

- **#9978** (4 comments, P3) – Request for Feishu/Lark interactive card format with metadata footer. A long‑standing feature request (April 15) with steady interest.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/9978)

- **#60841** (4 comments, P3) – Vulnerable package pins in `uv.lock` survive pip‑audit fixes across reboots. Security‑sensitive.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/60841)

- **#60197** (4 comments, P2) – `Event loop is closed` exception during `/exit` with MCP servers.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/60197)

The underlying needs across these threads are **reliability in CLI workflows**, **provider compatibility (especially OpenAI‑compatible and Codex)**, and **better user feedback** (session state, error messages, UI metadata).

## Bugs & Stability

Several new bugs were filed or updated today, ranked by severity:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| **#66267** | P1 | Multimodal content list crashes API budget on retry. | Yes (#66637 – fix(compression)) |
| **#66637** (PR) | P1 | Compression loses human intent and durable handoffs. | Associated PR itself is the fix |
| **#62810** | P2 | CLI exits with code `0` even on error; breaks automation. | No |
| **#66587** | P2 | Gemini HTTP 400: missing `thought_signature` in function calls. | No |
| **#66589** | P2 | Telegram startup notification races with `send_path_degraded`. | No |
| **#66544** | P2 | Custom‑provider metadata probes ignore per‑provider CA settings. | No |
| **#66641** | P2 | `key_env` ignored in auxiliary task config → vision/compression 401. | No |
| **#66642** | P2 | Terminal tool loses venv PATH on login‑shell snapshot. | No |
| **#66392** | P2 | Linux/X11 CUA pointer can crash entire KDE Plasma session. | No |
| **#66518** | P2 | stdio MCP watchdog kills healthy children on WSL2 due to btime drift. | No |
| **#66572** | P3 | LM Studio init hardcodes 64K context length. | No |
| **#66574** | P2 | Windows Desktop/TUI: reasoning exhaustion not surfaced + stale state. | No |

The **P1 multimodal crash** (#66267) is the most urgent, with a dedicated PR (#66637) already submitted today. The **CLI exit status bug** (#62810) is also high‑impact for CI/CD pipelines. Several WSL2‑specific bugs (#66518, #51448) indicate ongoing Windows/platform gaps.

## Feature Requests & Roadmap Signals

Notable feature requests and RFCs discussed recently:

- **#9978** – Feishu interactive cards (P3, 4 comments). Likely to be considered for a future gateway plugins release.  
- **#66536** – Per‑call model/provider override for `delegate_task` (P3, filed today). Would increase flexibility for sub‑agent routing.  
- **#14859** – Show session title in status bar (P3, April 24). Adds user‑visible session identification.  
- **#11442** – GitHub Copilot on GHE (P3, April 17). Expands enterprise support.  
- **#66621** – Custom icons for desktop profiles (P3, filed today). UX polish.  
- **#50748** – Display token generation speed in desktop app (P3, June 22). Helps users compare models.  
- **#33981** – Centralized Model/Provider Registry (RFC, closed). The discussion signals desire for a unified configuration model.

From the PR side, **#11870** (`/openmd` command) and **#36218** (tool search guidance) indicate ongoing improvement of CLI and agent prompting.

Given the current bug‑fixing churn and the fact that three P1/P2 fix PRs were opened today by a core contributor, the next minor release will likely prioritise **compression reliability, CLI exit handling, and MCP tool visibility** over new features.

## User Feedback Summary

Users express satisfaction with Hermes’ extensibility but frustration with **regression stability** and **platform incompatibilities**:

- **Pain**: After #3492, `hermes update` became silent and stashes unnecessarily (#3523).  
- **Pain**: Native Windows Desktop + LM Studio fails, while WSL works (#51448).  
- **Pain**: Exit code `0` on CLI errors breaks automated scripts (#62810).  
- **Pain**: Multimodal sessions can cost excessive API budget due to infinite retry loops (#66267).  
- **Pain**: MCP tools are invisible to gateway platforms (#65826, PR open).  
- **Delight**: The community actively contributes both bugs and fixes; many issues are responded to within hours.

Overall satisfaction appears solid, but the accumulation of P2 regressions suggests a **stabilisation sprint** would be well received.

## Backlog Watch

Several open issues and PRs have been awaiting maintainer attention for an extended period:

- **#3523** (P2, needs‑decision) – `hermes update` regressions. Last updated July 17 after months of inactivity. 6 comments.  
- **#9978** (P3) – Feishu interactive cards. Unanswered since April 15.  
- **#14859** (P3) – Session title in status bar. Unanswered since April 24.  
- **#11442** (P3) – GitHub Copilot on GHE. Unanswered since April 17.  
- **#60841** (P3, security) – Vulnerable `uv.lock` pins. Unresolved since July 8 with 4 comments.  
- **#60197** (P2) – Event loop crash on `/exit` (MCP). No assignee. Last updated July 17 from a comment.  
- **#46732** (P2) – Desktop message leaks across windows after `/new`. Last updated July 17 without resolution.  
- **#51448** (P2, needs‑repro) – Windows Desktop + LM Studio fail. Unresolved since June 23.  

The **#60841** security issue is particularly concerning because it describes a persistent vulnerability in the dependency lock file. While the team may be waiting for upstream fixes, a temporary workaround or advisory would help affected users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-18

## 1. Today's Overview
PicoClaw shows moderate activity with **4 issues updated** (3 open, 1 closed) and **12 pull requests updated** (10 open, 2 closed) in the last 24 hours. No new releases were published. The project is in a steady state, with a clear focus on **security hardening, performance improvements, and provider-specific fixes** (OAuth, WhatsApp, MQTT). Two PRs were merged/closed, addressing dependency stability and CLI robustness. The community continues to push for streaming support and better user feedback in channels like QQ and WhatsApp.

## 2. Releases
None.

## 3. Project Progress
Two pull requests were merged/closed today:
- **PR #3204** (closed) – *fix(deps): restore Azure dependency freeze baseline* – Downgraded Azure SDK modules to frozen versions to align with downstream supply‑chain checks.  
- **PR #3180** (closed) – *fix(cli): skip tool calls with invalid arguments* – Prevents malformed CLI tool calls from crashing the agent; adds regression tests.

Additionally, **Issue #3206** was closed with a fix for the v2→v3 config migration failure (false “unknown field” errors).

## 4. Community Hot Topics
- **Issue #3201** – *[Feature] Support streaming output for QQ channel* (3 comments). Users want token‑by‑token streaming for QQ, similar to Telegram and WebSocket. Continuation of the existing `StreamingCapable` pattern.  
  [sipeed/picoclaw Issue #3201](https://github.com/sipeed/picoclaw/issues/3201)
- **Issue #3206** – *v2→v3 config migration fails* (2 comments). Now closed, but generated significant discussion about migration reliability.  
  [sipeed/picoclaw Issue #3206](https://github.com/sipeed/picoclaw/issues/3206)
- **PR #3242** – *feat(whatsapp): add native typing presence* – Addresses user demand for real‑time feedback on WhatsApp. No comments yet, but linked to Issue #3240.  
  [sipeed/picoclaw PR #3242](https://github.com/sipeed/picoclaw/pull/3242)
- **PR #3241** – *fix(auth): make OAuth refresh provider‑correct and concurrency‑safe* – Fixes runtime failures caused by rigid OAuth refresh logic (Issue #3239).  
  [sipeed/picoclaw PR #3241](https://github.com/sipeed/picoclaw/pull/3241)

## 5. Bugs & Stability
| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | **#3239** | OAuth refresh requests use incompatible provider semantics and can race; OpenAI expects JSON, others form – causes failures under concurrent checks. | PR #3241 (open) |
| **Medium** | **#3240** | WhatsApp native channel does not publish typing presence; users see no feedback for several seconds. | PR #3242 (open) |
| **Low** | #3206 (closed) | v2→v3 config migration falsely rejected valid fields `build_info`, `session.dm_scope`. | Fixed |

A **security hardening PR** (#3246) is also open, addressing MQTT TLS verification (was `InsecureSkipVerify: true`), OAuth timeouts, and bounded search reads.

## 6. Feature Requests & Roadmap Signals
- **Streaming for QQ** (#3201) – Still open, no associated PR yet. Likely to be picked up in a future release as it aligns with existing streaming infrastructure.
- **WhatsApp typing presence** (#3240 – PR #3242) – Near‑ready; expected in v0.3.x.
- **Simplex channel type** (PR #3193) – New channel abstraction, open since June 27. Could broaden platform support.
- **Czech translations** (PR #3247) – Minor locale addition.
- **Performance optimizations** – Three PRs from `corporatepiyush` (#3244, #3245, #3243) reduce allocations in XML escaping and summary compaction; already open, likely to merge soon.

Predicting next release (v0.3.2 or v0.4.0) will include: WhatsApp typing presence, OAuth refresh fixes, security hardening, and several small performance improvements.

## 7. User Feedback Summary
- **Pain points**: Lack of streaming on QQ channel; no typing indicator on WhatsApp; OAuth refresh failures when using multiple providers; config migration breaking on fresh installs.
- **Satisfaction**: The quick closure of Issue #3206 (config migration) and the security/performance PRs show maintainers are responsive. Users appreciate the detailed issue reports and linked PRs.
- **Use cases**: Multi‑channel chatbot deployment (QQ, WhatsApp, Telegram), provider‑agnostic OAuth, and CLI‑based agent interaction.

## 8. Backlog Watch
- **PR #1951** – *chore: move installation scripts from docs repo to here* (opened 2026‑03‑24, last updated 2026‑07‑17). Very old, no comments from maintainers. May need triage or closure.  
  [sipeed/picoclaw PR #1951](https://github.com/sipeed/picoclaw/pull/1951)
- **PR #3193** – *Added simplex channel type* (opened 2026‑06‑27). No comments or review. Could be a candidate for next version if maintainers approve the design.  
  [sipeed/picoclaw PR #3193](https://github.com/sipeed/picoclaw/pull/3193)
- **Issue #3201** – Streaming for QQ (opened 2026‑07‑01). No assignee or milestone. Could benefit from a design discussion.  
  [sipeed/picoclaw Issue #3201](https://github.com/sipeed/picoclaw/issues/3201)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-18

## 1. Today's Overview

The project saw high activity with **4 issues** and **15 pull requests** updated in the last 24 hours, though no new release was cut. Three PRs were merged/closed, and three open issues remain active. The development focus is split between urgent bug fixes (rate-limit handling, session routing, test infrastructure) and feature unification (iMessage channel consolidation, Adoption Companion skill pack). Community contributions are robust, with multiple first-time and repeat contributors submitting patches. Overall, the project is in a healthy state with active triage and steady progress toward the next release.

## 2. Releases

No new releases have been published. The latest release version remains unchanged.

## 3. Project Progress

Three pull requests were merged or closed in the last 24 hours:

- [#2952 – Skill/add opencode stack](https://github.com/nanocoai/nanoclaw/pull/2952) (merged) — Adds operational/container skill for the OpenCode stack.
- [#2951 – fix(opencode): dedicated OPENCODE_BASE_URL, read from .env, NO_PROXY …](https://github.com/nanocoai/nanoclaw/pull/2951) (merged) — Fixes environment configuration for the OpenCode skill.
- [#3063 – docs(changelog): drop duplicated Unreleased bullets](https://github.com/nanocoai/nanoclaw/pull/3063) (merged) — Cleans up duplicated changelog entries.

Additionally, issue [#3071](https://github.com/nanocoai/nanoclaw/issues/3071) (Discord bare URLs not clickable) was closed after a fix.

**Features advanced:**  
- iMessage channel unification (PRs [#2999](https://github.com/nanocoai/nanoclaw/pull/2999), [#3076](https://github.com/nanocoai/nanoclaw/pull/3076)) continue to mature with a second, more refined implementation targeting spectrum-ts v11.  
- Scheduled task visibility improvements (PR [#3068](https://github.com/nanocoai/nanoclaw/pull/3068)) address cross-session feedback for broadcast vs. operational sessions.

**Security:**  
- PR [#3065](https://github.com/nanocoai/nanoclaw/pull/3065) fixed a CWE-306 vulnerability on the loopback webhook server, now authenticated to prevent action forgery (GHSA-h9g4-589h-68xv).

## 4. Community Hot Topics

**Most discussed issue:** [#3071](https://github.com/nanocoai/nanoclaw/issues/3071) — *Discord: bare URLs posted by the agent arrive as literal `[url](url)` and aren't clickable* (1 comment, now closed). This highlights a common user pain point with chat SDK formatting incompatibilities.

**Open issues with zero comments but high impact potential:**  
- [#3075](https://github.com/nanocoai/nanoclaw/issues/3075) — *Silent log loss + inbound message duplicate-insert errors after long uptime* (Matrix channel). No discussion yet, but the combination of data loss and duplication signals a stability-critical bug.  
- [#3074](https://github.com/nanocoai/nanoclaw/issues/3074) — *Claude provider with custom ANTHROPIC_BASE_URL (OpenRouter): turns silently dropped*. Users relying on alternative inference providers face silent failures.  
- [#3072](https://github.com/nanocoai/nanoclaw/issues/3072) — *Skill docs only document /name, which works in one of three coding harnesses*. A documentation mismatch that affects developer onboarding.

**Active PRs drawing attention:**  
- [#3077](https://github.com/nanocoai/nanoclaw/pull/3077) — *fix(claude): only abort on a rejected rate_limit_event; split rate_limit vs quota*. Directly addresses the OpenRouter issue from #3016 and is likely to be merged quickly.  
- [#3081](https://github.com/nanocoai/nanoclaw/pull/3081) – *fix(agent-runner): route per-turn results by turn generation, not entry-frozen routing*. Fixes multi-channel cross-talk in long-lived queries.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **High** | [#3075](https://github.com/nanocoai/nanoclaw/issues/3075) | Silent log loss + message duplicate-insert errors after long uptime (Matrix). Potential data corruption. | No open fix PR yet. |
| **Medium** | [#3074](https://github.com/nanocoai/nanoclaw/issues/3074) | Claude+OpenRouter: turns silently dropped when SDK result event is empty. Model replies lost. | PR [#3077](https://github.com/nanocoai/nanoclaw/pull/3077) targets related rate-limit handling, but not this exact issue. |
| **Medium** | [#3071](https://github.com/nanocoai/nanoclaw/issues/3071) (closed) | Discord URLs not clickable due to markdown double-encoding. | Fixed. |
| **Low** | [#3072](https://github.com/nanocoai/nanoclaw/issues/3072) | Skill docs only document `/name` syntax, ignoring Codex `$name` and other harnesses. | No fix PR. |

**Other stability fixes in flight:**  
- [#3080](https://github.com/nanocoai/nanoclaw/pull/3080) – Ship the `matrix-js-sdk` ESM fix as a pnpm patch instead of a fragile node_modules edit.  
- [#3078](https://github.com/nanocoai/nanoclaw/pull/3078) – Pin agent-shared session resolution to an anchor session to prevent session forking.  
- [#3079](https://github.com/nanocoai/nanoclaw/pull/3079) – Gate mid-turn follow-up pushes on trigger=1 to prevent self-sustaining background responses.  
- [#3082](https://github.com/nanocoai/nanoclaw/pull/3082) – Skip a chmod-based backup-failure test when running as root (Docker/LXC environments).

## 6. Feature Requests & Roadmap Signals

**Prominent feature PRs under review:**  
- **iMessage unification** – Two PRs ([#2999](https://github.com/nanocoai/nanoclaw/pull/2999), [#3076](https://github.com/nanocoai/nanoclaw/pull/3076)) propose unifying local and hosted iMessage backends into a single `imessage` channel. The newer PR targets `spectrum-ts v11` and is likely the version that will be merged.  
- **Adoption Companion pack** ([#3073](https://github.com/nanocoai/nanoclaw/pull/3073)) – Adds two utility skills (Memory Receipts + Knowledge Inventory), reflecting demand for onboarding and knowledge management tooling.

**Prediction for next release:**  
- The iMessage unification (one of #2999 or #3076) will likely land.  
- The session resolution fix (#3078) and the rate-limit/OpenRouter fix (#3077) are strong candidates for inclusion.  
- The security fix (#3065) is important and will be included.  
- The Adoption Companion skills may be deferred to a later minor release if more testing is needed.

## 7. User Feedback Summary

**Pain points:**  
- Discord users experience broken URL formatting (#3071).  
- Matrix users on long-running instances report silent message duplication and log loss (#3075), which undermines trust in the channel integration.  
- Users of alternative Claude providers (OpenRouter) encounter silent turn drops (#3074) that are hard to debug.  
- New skill developers are confused by documentation that only covers Claude Code’s slash-command syntax, omitting Codex and other harnesses (#3072).

**Use cases driving contributions:**  
- **Self-hosted homeservers** (Matrix on localhost) are a key deployment scenario, as shown by #3075.  
- **Third-party AI model providers** (OpenRouter) are being actively used, evidenced by #3074 and #3077.  
- **iMessage integration** continues to be a high-demand channel, with two competing feature PRs from different contributors.

**Satisfaction signals:**  
- High PR velocity and multiple new contributors indicate a healthy and welcoming community.  
- The prompt closure of #3071 shows responsive triage for simple bugs.

## 8. Backlog Watch

**Long-open feature PR needing maintainer attention:**  
- [#2999](https://github.com/nanocoai/nanoclaw/pull/2999) – *unify iMessage into a single `imessage` channel* (opened July 10, last updated July 17). This PR is now 8 days old without maintainer comment. A competing PR (#3076) arrived later; maintainers should clarify direction to avoid duplication of effort.

**Open issues with no response:**  
- All three open issues from yesterday (#3072, #3074, #3075) currently have zero comments from maintainers. While recent, they represent bugs with high impact and should be triaged promptly.

**No other long-stale issues or PRs** were found in the 24-hour window data. The project appears to have a responsive core team.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest — 2026-07-18

### 1. Today's Overview
Project activity is minimal, with no new releases or pull requests. A single issue (#976) was updated in the last 24 hours, remaining open and exposing a critical crash bug on aarch64 Linux. The absence of merged PRs or closed issues suggests a quiet phase, but the severity of the reported crash may require prompt maintainer response. Overall project health appears stable in terms of code churn, though user impact from the Telegram crash could erode trust if unresolved.

### 2. Releases
No new releases today.

### 3. Project Progress
No pull requests were merged or closed in the last 24 hours. No feature branches advanced.

### 4. Community Hot Topics
The only active thread is the crash bug [#976](https://github.com/nullclaw/nullclaw/issues/976) (SIGSEGV on every inbound Telegram message), filed by @wonhotoss. It has 2 comments and 0 reactions, indicating focused discussion rather than widespread clamor. The issue reveals a deep stability problem: the inbound worker thread is allocated with a ~512 KB stack, which overflows on aarch64 Linux, causing a segfault on every message. The user is forced to operate in a crash-loop as a systemd service. Underlying need: immediate fix to increase stack size or refactor worker thread handling for aarch64 compatibility.

### 5. Bugs & Stability
**Critical** — [#976](https://github.com/nullclaw/nullclaw/issues/976): SIGSEGV on every inbound Telegram message on `nullclaw v2026.5.29` (aarch64 Linux). The crash is reproducible with 100% frequency; all messages are lost. No fix pull request exists yet. The severity is **high** because it renders the Telegram gateway completely unusable on ARM64 platforms. Mitigation: temporarily adjusting thread stack size (e.g., via environment variable or config) may be possible, but no official workaround documented.

No other bugs, regressions, or crashes were reported.

### 6. Feature Requests & Roadmap Signals
No feature requests were filed or discussed in the last 24 hours. The community focus is entirely on stability.

### 7. User Feedback Summary
The sole user (@wonhotoss) is experiencing significant pain: complete loss of Telegram message handling, forced process restarts, and inability to receive replies. The underlying use case—running NullClaw as a systemd service for continuous message processing—is broken on aarch64. Satisfaction is likely low, though no additional users have chimed in. No positive feedback was recorded.

### 8. Backlog Watch
The only open issue (#976) is recent (filed 2026-07-16) and has received one comment from the author and one from a potential developer. It requires maintainer attention to triage, confirm, and either patch or provide a workaround. No other long-unanswered items exist in the current data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-18

## 1. Today's Overview

The project remains in an intense refactoring and stabilization cycle ahead of the v1 release. Over the past 24 hours, 50 issues were updated (26 open, 24 closed) and 50 pull requests were updated (25 open, 25 merged/closed). The majority of activity is concentrated on the **Reborn architecture simplification** (code-named §4.3–§4.4), with a series of mechanical store consolidations replacing hand-written in-memory stores with filesystem-backed implementations. Additionally, the **Telegram channel extension** for Reborn was merged, and a critical security fix for multi-tenant file-system access was closed. A new regression in the Reborn boot sequence (#6215) was opened, reflecting the risk of rapid refactoring. No new releases were published today.

## 2. Releases

No new releases were published in the last 24 hours. The previous release cycle is tracked in PR #5598 (still open), which would bump `ironclaw_common` from 0.4.2 to 0.5.0 (breaking), `ironclaw_skills` from 0.3.0 to 0.4.0 (breaking), and the root `ironclaw` binary from 0.24.0 to 0.29.1.

## 3. Project Progress

**Closed/Merged PRs today (6 total):**

- [#6159](https://github.com/nearai/ironclaw/pull/6159) — **feat(reborn): telegram channel extension** — added admin bot setup, WebGeneratedCode pairing, DM entrypoint, and triggered delivery for Telegram as a first-class Reborn channel.
- [#6208](https://github.com/nearai/ironclaw/pull/6208) — **docs(reborn): architecture-simplification r2–r7** — revised the architecture proposal to refine product-surface capability conduits and dynamic-capability gate contract.
- [#6209](https://github.com/nearai/ironclaw/pull/6209) — **refactor(reborn): rename LocalFilesystem → DiskFilesystem** — part of §4.4 deployment-mode naming cleanup.
- [#6210](https://github.com/nearai/ironclaw/pull/6210) — **refactor(reborn): budget-gate store over RootFilesystem** — deleted `InMemoryBudgetGateStore`, replaced with filesystem-backed implementation.
- [#6217](https://github.com/nearai/ironclaw/pull/6217) — **fix(reborn): compile Telegram host in production image** — ensured Telegram v2 host feature is included in Docker build.
- [#6219](https://github.com/nearai/ironclaw/pull/6219) — **fix(telegram): finish LocalFilesystem→DiskFilesystem rename in test code** — caught five missed references in Telegram extension tests.

**Also closed today (from earlier PRs):** Several store-consolidation PRs merged yesterday (#6209, #6210) were closed today after validation.

**Key feature advance:** The Telegram channel extension for Reborn is now fully merged, completing a major milestone for multi-channel support on the new engine.

## 4. Community Hot Topics

Issues and PRs attracting the most discussion (by comment count) during the past 24 hours:

- [#2767 (closed)](https://github.com/nearai/ironclaw/issues/2767) — “Epic: Separate engine v2 capability background from callable tool schemas” (7 comments). This month-old epic was closed today, marking completion of one of the largest structural changes in engine v2.
- [#2813 (closed)](https://github.com/nearai/ironclaw/issues/2813) — “engine-v2: add typed assistant content model for final vs internal tool-use text” (6 comments). Also closed, addressing a long-standing clarity issue in tool-output rendering.
- [#2835 (closed)](https://github.com/nearai/ironclaw/issues/2835) — “Tool discovery: add curated summaries for core built-ins used by engine v2 prompting” (3 comments). Closed as part of the v2 tool guidance work.
- [#6170 (closed)](https://github.com/nearai/ironclaw/issues/6170) — “Remove user access to file system via shell” (2 comments). Raised by a user or tester; urgent security fix that was quickly closed with a fix.
- [#4644 (open)](https://github.com/nearai/ironclaw/issues/4644) — “Universal attachments across all channels” (2 comments). Long-running feature request for attachment support in Reborn.
- [#6215 (open)](https://github.com/nearai/ironclaw/issues/6215) — “Reborn: model cost table / budget accountant not rebuilt by LLM reload chokepoint” (0 comments, opened today). New regression; expected to attract attention.

**Underlying needs:** The community (mostly internal core contributors) is pushing toward completing the Reborn architecture simplification while ensuring no regressions in security, cost accounting, and UI stability. The closure of several engine v2 epics signals a shift from feature development to hardening.

## 5. Bugs & Stability

**Severity: High**

- **[#6170 (closed)](https://github.com/nearai/ironclaw/issues/6170)** — Security vulnerability: users on multi-tenant instances could execute arbitrary shell commands via the WebUI, gaining access to the server file system (`ls -all` unbounded to workspace). Fixed and closed. **Fix already merged** (likely in companion PRs).

**Severity: Medium**

- **[#6215 (open, created today)](https://github.com/nearai/ironclaw/issues/6215)** — Regression: after PR #6174 (boot convergence), the model cost table and budget accountant are not rebuilt when LLM settings are reloaded, potentially allowing unbounded usage or incorrect cost tracking. **No fix PR yet.** Affects the Reborn onboarding journey.

**Severity: Low/Closed**

- [#5331](https://github.com/nearai/ironclaw/issues/5331) — Tool-approval ‘always’ may not auto-approve the next same-tool call under engine v2. Closed today.
- [#3618](https://github.com/nearai/ironclaw/issues/3618) — Debug panel stats stuck at 0 on engine v2. Closed.
- [#3465](https://github.com/nearai/ironclaw/issues/3465) — Engine v2 repeatedly calls `tool_info` during tool-use flows. Closed.
- [#3464](https://github.com/nearai/ironclaw/issues/3464) — Failed tool calls render inconsistently in Gateway UI. Closed.
- [#3463](https://github.com/nearai/ironclaw/issues/3463) — Engine v2 generated images do not render correctly in Gateway UI. Closed.
- [#4278](https://github.com/nearai/ironclaw/issues/4278) — Potential performance issue with unbounded conversation growth in engine v2 (context window exhaustion). Closed.

Also, a CI issue ([#6221](https://github.com/nearai/ironclaw/pull/6221) open) extends the benchmark job time cap from 240 to 350 minutes to prevent premature cancellation of heavy suites.

## 6. Feature Requests & Roadmap Signals

- **[#4644 (open)](https://github.com/nearai/ironclaw/issues/4644)** — “Universal attachments across all channels” is a long-standing request to wire a legacy attachment pipeline into Reborn with an extensible format registry. Still open, likely for a post-v1 release.
- **[#6198 (open)](https://github.com/nearai/ironclaw/issues/6198)** — Epic for pre-v1 refactoring & legacy cleanup. This is the current main roadmap focus for the team.
- **[#6201 (open)](https://github.com/nearai/ironclaw/issues/6201)** — Rename `ironclaw_reborn_*` crates to `ironclaw_*` after 1.0 cut. Signals that the v1 release is imminent.
- **[#5124 (closed via #6159)](https://github.com/nearai/ironclaw/issues/5124)** — Support Telegram channel for Reborn. Now delivered.
- **[#6174 (open)](https://github.com/nearai/ironclaw/pull/6174)** — Onboarding journey (keychain master key, two-prompt setup, login link) is a new PR targeting standalone usage. Likely to be included in the next release.

**Predictions:** The next release will include the onboarding CLI, Telegram channel, and the completed store-consolidation work. Universal attachments and full channel porting (e.g., Discord, Slack) will likely follow after v1.

## 7. User Feedback Summary

Limited direct user feedback in the last 24 hours. Notable signals:

- **Security concern (positive response):** Issue #6170 (file system access via shell) was reported and fixed within hours, demonstrating responsive security handling.
- **Performance worry:** Issue #4278 (closed) raised by liaoqianchuan about unbounded conversation growth in engine v2 — acknowledged and addressed, but the underlying solution may still be verified by users.
- **QA-testing bugs:** Several engine v2 UI rendering bugs (#3463, #3464, #3618) were reported by QA testers and are now closed, indicating active testing cycles and rapid bug squashing.
- **Satisfaction:** No explicit satisfaction feedback, but the closure of long-standing engine v2 epics (e.g., #2767, #2813) suggests progress is tangible.

## 8. Backlog Watch

Issues and PRs that remain open for an extended period or appear to need maintainer attention:

- **[#4644 (open since June 9)](https://github.com/nearai/ironclaw/issues/4644)** — Universal attachments. No update in over a month; may need re-scoping for v2.
- **[#3577 (open since May 13)](https://github.com/nearai/ironclaw/issues/3577)** — Track v1 channel ports for Reborn. Still active (updated yesterday), but progress is ongoing via individual channel PRs.
- **[#5219 (open since June 25)](https://github.com/nearai/ironclaw/issues/5219)** — Follow-up to harden activity identity invariants. Updated July 17 but no associated PR yet.
- **[#5598 (open since July 3)](https://github.com/nearai/ironclaw/pull/5598)** — Release PR still open with breaking changes. Merge seems blocked or waiting for more commits. Should be resolved before v1.
- **[#6185 (open since July 17)](https://github.com/nearai/ironclaw/pull/6185)** — Large PR renaming binaries (`ironclaw-reborn` → `ironclaw`). Still open; may be merged soon as it’s a prerequisite for v1.
- **[#6174 (open since July 17)](https://github.com/nearai/ironclaw/pull/6174)** — Onboarding CLI PR. Needs review and merge before release.
- **[#6211 (open since July 17)](https://github.com/nearai/ironclaw/pull/6211)** — Fix for CLI stubs (channels/hooks/logs). Low risk, could be merged quickly.

No issues have gone completely unanswered for more than a few weeks — the team is actively tending the backlog.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-07-18

## 1. Today's Overview

Over the past 24 hours, LobsterAI saw intense development activity with **15 pull requests updated** (13 merged/closed) and **7 issues updated** (5 closed, 2 still open). A new minor release **2026.7.16** was shipped, and the team focused heavily on UI refinements, stability patches, and a major new AI‑generated skin experience. The high merge rate (87% of PRs) indicates a productive sprint, with most changes targeting the renderer, cowork, and OpenClaw subsystems. Two long‑standing feature‑request PRs remain open from April, signalling potential backlog pressure.

## 2. Releases

**New Version: [LobsterAI 2026.7.16](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.16)**  
Released 2026-07-16 (source: release notes).  
Changes:
- **Refactor**: Extracted clipboard attachment file extraction into a testable helper (`#2343`).
- **Feature**: Added campaign final reward claim functionality (`6eafb`).

No breaking changes or migration notes were documented. Users can upgrade via the built‑in updater (now checking every 2 hours per PR `#2347`).

## 3. Project Progress

The 13 merged/closed PRs today advanced several areas:

**New Features**
- **AI‑Generated Skins** ([PR #2352](https://github.com/netease-youdao/LobsterAI/pull/2352)) – Adds an AI‑generated skin‑pack workflow, appearance customization, and immersive skin presentation across sidebar, title bars, and conversations.
- **Structured Failure Details** ([PR #2348](https://github.com/netease-youdao/LobsterAI/pull/2348)) – Surfaces provider/model/HTTP error details from OpenClaw in the assistant turn UI when a cowork run fails.
- **Service Deployment Data Persistence** ([PR #2349](https://github.com/netease-youdao/LobsterAI/pull/2349)) – Persists service deployment data for cowork and artifacts.

**Bug Fixes**
- **OpenClaw**: Fixed stale chat error after successful deferred final ([PR #2354](https://github.com/netease-youdao/LobsterAI/pull/2354)).
- **Email Diagnostics**: Prevented stale chat history from overriding new diagnostics chat ([PR #2346](https://github.com/netease-youdao/LobsterAI/pull/2346)).
- **Build**: Localised NSIS web installer download prompts and fixed progress bar overlap ([PR #2345](https://github.com/netease-youdao/LobsterAI/pull/2345)).
- **Window Caption**: Aligned hover colours with sidebar controls ([PR #2355](https://github.com/netease-youdao/LobsterAI/pull/2355)) and refined icon sizing/styling ([PR #2351](https://github.com/netease-youdao/LobsterAI/pull/2351)).
- **Artifacts**: Stabilised preview panel and input area layout to reduce flashing ([PR #2357](https://github.com/netease-youdao/LobsterAI/pull/2357)).

**Chores & Maintenance**
- Updated update check interval from 12h to 2h ([PR #2347](https://github.com/netease-youdao/LobsterAI/pull/2347)).
- Optimised sidebar ad banner ([PR #2350](https://github.com/netease-youdao/LobsterAI/pull/2350)).
- General UI update ([PR #2353](https://github.com/netease-youdao/LobsterAI/pull/2353)) and release preparation ([PR #2356](https://github.com/netease-youdao/LobsterAI/pull/2356)).

## 4. Community Hot Topics

Activity on issues and PRs was moderate, with no single item gathering many comments or reactions. The two **open issues** that continue to attract attention are:

- **[#1311](https://github.com/netease-youdao/LobsterAI/issues/1311)** (open, created Apr 2) – Table content displays raw HTML tags on line breaks; request for hover tooltip on truncated text. 1 comment.
- **[#1314](https://github.com/netease-youdao/LobsterAI/issues/1314)** (open, created Apr 2) – Request for draggable sidebar width (180–480px). 1 comment.

Both are labelled `stale` and have corresponding open PRs (`#1308` for input‑draft isolation, `#1315` for sidebar drag). The underlying need is clear: users want a more customisable and visually polished UI, especially for dense data rendering (tables) and flexible layout (sidebar). Despite being months old, these items remain the most active community suggestions.

## 5. Bugs & Stability

Five bugs were **closed** today (all from April, likely fixed in earlier releases):

| Issue | Severity | Summary | Status |
|-------|----------|---------|--------|
| [#1354](https://github.com/netease-youdao/LobsterAI/issues/1354) | **Critical** – BSOD after starting Pageant | Closed |
| [#1357](https://github.com/netease-youdao/LobsterAI/issues/1357) | **High** – “Start Pageant” response says started but not actually running | Closed |
| [#1358](https://github.com/netease-youdao/LobsterAI/issues/1358) | **Medium** – Scheduled task button gives no feedback | Closed |
| [#1359](https://github.com/netease-youdao/LobsterAI/issues/1359) | **High** – Deleted tasks reappear after restart | Closed |
| [#1360](https://github.com/netease-youdao/LobsterAI/issues/1360) | **Low** – Agent duplicate names allowed on creation | Closed |

Additionally, today’s PRs fixed **newly discovered** stability issues:
- OpenClaw stale chat error after a successful deferred final ([PR #2354](https://github.com/netease-youdao/LobsterAI/pull/2354)).
- Email diagnostics overriding new chat when stale history exists ([PR #2346](https://github.com/netease-youdao/LobsterAI/pull/2346)).
- Build installer progress bar overlap ([PR #2345](https://github.com/netease-youdao/LobsterAI/pull/2345)).

No open bug reports remain in the last 24 hours. The project’s stability appears solid, with quick turnaround on reported issues.

## 6. Feature Requests & Roadmap Signals

The most prominent feature request gaining steam is **draggable sidebar width** ([Issue #1314](https://github.com/netease-youdao/LobsterAI/issues/1314), [PR #1315](https://github.com/netease-youdao/LobsterAI/pull/1315)). The proposed implementation (180–480px range, col‑resize cursor) is already coded in the PR but has been open since April. Given the high visibility of UI customisation requests, this is a strong candidate for inclusion in the next release.

Another signal is the **AI‑generated skin feature** shipped today ([PR #2352](https://github.com/netease-youdao/LobsterAI/pull/2352)). This suggests the team is actively investing in visual personalisation. The sidebar drag feature would complement this nicely.

The **table HTML tag display** issue ([#1311](https://github.com/netease-youdao/LobsterAI/issues/1311)) is a UX polish request that could be addressed with a small renderer fix. It may also be prioritised soon given that table usage is common in cowork responses.

## 7. User Feedback Summary

**Pain points** (all from closed issues):
- Crashes (BSOD) when using Pageant automation – resolved.
- False positive responses for system commands – resolved.
- No visual feedback for scheduled tasks – resolved.
- Task persistence failure after deletion – resolved.
- Agent name duplication – resolved.

**Satisfaction indicators**: The five closed issues were all marked `stale` but received fixes (likely in earlier releases). The fact that users reported them suggests active use of automation and task scheduling features. The existence of UI enhancement requests (sidebar drag, table formatting) indicates users are comfortable with the product and want finer control.

No new negative feedback appeared in the last 24 hours. The release of AI‑generated skins may generate positive sentiment among users seeking a more personalised experience.

## 8. Backlog Watch

Two feature‑request issues and their corresponding PRs remain **unanswered for over 3.5 months**:

| Item | Type | Created | Last Update | Status |
|------|------|---------|-------------|--------|
| [Issue #1311](https://github.com/netease-youdao/LobsterAI/issues/1311) – Table content formatting | Bug/Enhancement | Apr 2 | Jul 17 (stale automark) | Open, no maintainer comment |
| [Issue #1314](https://github.com/netease-youdao/LobsterAI/issues/1314) – Drag sidebar width | Feature Request | Apr 2 | Jul 17 (stale automark) | Open, 1 comment |
| [PR #1308](https://github.com/netease-youdao/LobsterAI/pull/1308) – Isolate input draft per agent | Feature | Apr 2 | Jul 17 | Open, no reviewer activity |
| [PR #1315](https://github.com/netease-youdao/LobsterAI/pull/1315) – Drag sidebar width (implementation) | Feature | Apr 2 | Jul 17 | Open, no reviewer activity |

These items are at risk of being forgotten. The sidebar drag PR (#1315) is particularly concerning because it directly addresses a community request that is still open. Maintainer attention is needed to either merge, reject, or provide feedback. Similarly, the table display issue (#1311) is a clear user pain point that could be resolved with a small renderer change.

---

*Analysis based on GitHub activity for netease-youdao/LobsterAI as of 2026-07-18.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-18

## 1. Today’s Overview
Project activity remains low but steady. One issue was updated in the last 24 hours, and two pull requests were opened (none merged or closed). Two new releases were published (version tags `20260717.03` and `20260717.02`), though no changelogs or breaking changes are documented. The open PRs introduce useful quality-of-life improvements (ACP-only chat support) and an experimental vector-database memory backend, indicating continued community-driven development. Overall project health appears stable with moderate contributions.

## 2. Releases
Two releases were published today:
- **`20260717.03`** – no accompanying details.
- **`20260717.02`** – no accompanying details.

No breaking changes, migration notes, or feature lists were provided. Users should consult the project’s release notes or commit history for further context.

## 3. Project Progress
No pull requests were merged or closed today. However, two new PRs were opened, representing ongoing feature work:
- **PR #1158** (open) — *feat(memory): add zvec vector database memory backend* — an experimental alternative memory backend using Zvec and Redb, feature-gated behind a `zvec` cargo flag.  
  [GitHub](https://github.com/moltis-org/moltis/pull/1158)
- **PR #1157** (open) — *fix(web): support ACP-only chat setup* — allows users to configure a chat environment using only ACP agents (no LLM models required), updates the session header picker and model selector accordingly.  
  [GitHub](https://github.com/moltis-org/moltis/pull/1157)

Neither PR has received comments or reviews yet.

## 4. Community Hot Topics
The only issue updated in the last 24 hours is the most discussed item:
- **Issue #574** (open) — *[Feature]: Model Routing Per topic*  
  Author: azharkov78 | Created: 2026-04-06 | Updated: 2026-07-18  
  Comments: 3 | 👍: 1  
  [GitHub](https://github.com/moltis-org/moltis/issues/574)  
  **Analysis:** The user requests the ability to route chat messages to different models based on topic (e.g., technical vs. creative). The issue has remained open for over three months with only three comments and one reaction, suggesting moderate interest but no active design discussion. The underlying need is for smarter, context-aware model orchestration—a common pain point in multi-model agent systems.

No other issues or PRs have significant comment counts or reactions.

## 5. Bugs & Stability
No bug reports, crashes, or regressions were recorded in the last 24 hours. Both open PRs are feature/fix contributions rather than bug fixes. System stability appears solid.

## 6. Feature Requests & Roadmap Signals
- **Model Routing Per Topic** (#574) – likely to remain under consideration; no immediate implementation signals.
- **Zvec vector database backend** (PR #1158) – if merged, would provide a new memory storage option for users running local embedding servers. Could be included in the next release (e.g., `20260718.x`) if reviewed quickly.
- **ACP-only chat setup** (PR #1157) – a straightforward UX improvement that is likely to be merged soon, as it fixes a configuration edge case.

Predicting the next minor release: will likely incorporate PR #1157 (web fix) and possibly PR #1158 if the community tests it positively. The older feature request (#574) is not moving toward implementation yet.

## 7. User Feedback Summary
Direct user feedback is limited. The sole issue (#574) highlights a user’s desire for topic-based model routing, indicating that some users feel constrained by the current monolithic model assignment. No complaints about crashes, performance, or missing documentation were visible. The new PRs suggest contributors are experimenting with alternative backends (Zvec memory) and smoothing onboarding (ACP-only setup), which aligns with a general push for flexibility and easier configuration.

## 8. Backlog Watch
- **Issue #574** (open since 2026-04-06) – has received no maintainer response beyond initial triage. With only one reaction and three comments, it is not high-traffic, but it represents a feature request that has been waiting for over three months. Maintainers should consider adding a label or comment to acknowledge the request and set expectations.

No other stale or unanswered issues or PRs were identified in the 24-hour window.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-18

*Data snapshot: Issues updated in 24h: 25 (15 open, 10 closed) · PRs updated in 24h: 40 (17 open, 23 merged/closed) · New release: v2.0.0.post3*

---

## 1. Today’s Overview

CoPaw saw **very high activity** with 40 pull requests touched and 25 issues updated in the past day, coinciding with the **v2.0.0.post3** patch release. The community is heavily focused on **Windows desktop stability** (admin privileges, graceful shutdown, progressive rendering), **MCP performance** (sequential‑vs‑parallel driver startup, llama.cpp errors), and **memory management improvements** (manual reindex, Dream digest architecture). A strong batch of 23 PRs were merged or closed, indicating fast iteration by maintainers. Several new feature requests around per‑chat MCP control, reasoning depth, and internet search toggles signal growing demand for **conversation‑level configurability**.

---

## 2. Releases

**v2.0.0.post3** – *Published 2026‑07‑17*

**What’s Changed:**
- **fix(mcp):** MCP driver migration now correctly converts `${VAR}` headers to environment credential references during driver migration.
- **refactor(ci):** Hardened desktop workflows and removed legacy verify dead code.

**Breaking changes:** None reported. **Migration notes:** Existing MCP configs using `${VAR}` headers will be automatically migrated on upgrade; no manual action required.

---

## 3. Project Progress

**23 PRs were merged/closed today.** Key advances:

| PR | Description | Status |
|----|-------------|--------|
| [#6234](https://github.com/agentscope-ai/QwenPaw/pull/6234) | Use absolute import in Tauri entry point (fixes PyInstaller sandbox startup) | Merged |
| [#6220](https://github.com/agentscope-ai/QwenPaw/pull/6220) | Fix token_usage cache: don’t persist unseeded cache on shutdown | Merged |
| [#6204](https://github.com/agentscope-ai/QwenPaw/pull/6204) | Drop redundant `nvidia-smi` probe in `get_vram_size_gb` (first‑time contributor) | Merged |
| [#6218](https://github.com/agentscope-ai/QwenPaw/pull/6218) | Pass `model_slot_override` from HTTP request to model factory | Merged |
| [#6217](https://github.com/agentscope-ai/QwenPaw/pull/6217) | Treat unprobed multimodal as fail‑open to prevent image stripping | Merged |
| [#6170](https://github.com/agentscope-ai/QwenPaw/pull/6170) | Add `MAX_WAITTIME` cap to browser automation tool | Merged |
| [#6198](https://github.com/agentscope-ai/QwenPaw/pull/6198) | Bound multi-agent startup concurrency and improve readiness UX | Merged |
| [#6159](https://github.com/agentscope-ai/QwenPaw/pull/6159) | Refactor per‑turn token/context usage from ConsoleChannel into BaseChannel | Merged |

**Still open but notable:** [#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225) (graceful Desktop shutdown) and [#6235](https://github.com/agentscope-ai/QwenPaw/pull/6235) (manual memory reindex endpoint) are under review.

---

## 4. Community Hot Topics

Most active discussions in the past 24h (by comment count and reactions):

| Issue / PR | Comments | Topic |
|------------|----------|-------|
| [#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161) | 7 | Windows update breaks normal‑user startup – closed as invalid after investigation |
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) | 6 | Messages silently dropped when session busy (Feishu webhook) – **no fix PR yet** |
| [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) | 5 | Multiple regressions after 1.x → 2.0 upgrade (embedding bug, auto‑memo, system prompt) |
| [#6221](https://github.com/agentscope-ai/QwenPaw/issues/6221) | 5 | Test notification bot (internal testing) |
| [#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976) | 4 | Request: separate tool‑call parameters from tool‑call results in channel display |
| [#6193](https://github.com/agentscope-ai/QwenPaw/issues/6193) | 3 | MCP drivers start sequentially (8× slower than parallel) – high community interest |
| [#6227](https://github.com/agentscope-ai/QwenPaw/issues/6227) | 👍1 | Per‑chat MCP server & tool selection – **most upvoted feature request** |

**Underlying needs:** Users want **granular per‑chat control** (MCP servers, internet access, reasoning depth) and **better channel UX** (tool result truncation). The MCP performance issue reflects a pain point for multi‑client deployments.

---

## 5. Bugs & Stability

**New bugs reported today (24h window)** ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#6219](https://github.com/agentscope-ai/QwenPaw/issues/6219) | Desktop force‑kills backend instead of graceful shutdown (data loss risk) | ✅ [#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225) |
| **High** | [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) | Messages silently dropped when session busy (no queue) – open 6 days | ❌ |
| **High** | [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) | 1.x → 2.0 upgrade regressions: embedding mapping, auto‑memo, system prompt left‑truncation | ❌ |
| **Medium** | [#6201](https://github.com/agentscope-ai/QwenPaw/issues/6201) | PubMed MCP causes llama.cpp error – temporary workaround by disabling MCP | ❌ |
| **Medium** | [#6193](https://github.com/agentscope-ai/QwenPaw/issues/6193) | MCP drivers start sequentially (performance bug) | ❌ (community PR suggested) |
| **Low** | [#6202](https://github.com/agentscope-ai/QwenPaw/issues/6202) | Desktop progressive skill rendering broken – closed as duplicate | ✅ (likely fixed in earlier patch) |

Additionally, the Windows admin‑privilege issue ([#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161)) was closed as invalid after investigation, and [#6169](https://github.com/agentscope-ai/QwenPaw/issues/6169) (forced UAC) was closed, likely resolved in v2.0.0.post3.

---

## 6. Feature Requests & Roadmap Signals

Top user‑requested features observed in the last 24h:

| Issue | Feature | Likely in next version? |
|-------|---------|-------------------------|
| [#6227](https://github.com/agentscope-ai/QwenPaw/issues/6227) | Per‑chat MCP server & tool selection | **High** – aligns with existing console refactoring |
| [#6228](https://github.com/agentscope-ai/QwenPaw/issues/6228) | Per‑chat internet search toggle | Medium – could be combined with above |
| [#6229](https://github.com/agentscope-ai/QwenPaw/issues/6229) | User‑selectable reasoning depth (Light/Medium/Deep/Auto) | Medium – new UI component needed |
| [#6230](https://github.com/agentscope-ai/QwenPaw/issues/6230) | Support Hermes model family as secondary reasoning engine | Low (niche) |
| [#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976) | Separate channel tool‑call from tool‑result display | **Already in PR** [#6233](https://github.com/agentscope-ai/QwenPaw/pull/6233) |
| [#6231](https://github.com/agentscope-ai/QwenPaw/issues/6231) | Multiple configs for same model ID (e.g., thinking on/off) | Medium |
| [#6162](https://github.com/agentscope-ai/QwenPaw/issues/6162) | Auto‑read max context window from model API | **High** – prevents manual config errors |
| [#6205](https://github.com/agentscope-ai/QwenPaw/issues/6205) | Compress & cache static assets in Console | **Already in PR** [#6232](https://github.com/agentscope-ai/QwenPaw/pull/6232) |
| [#5919](https://github.com/agentscope-ai/QwenPaw/issues/5919) | Global runtime configuration (avoid per‑agent setup repetition) | Low (architectural change) |

**Prediction:** Next minor release (v2.0.1) will likely include **per‑chat MCP controls**, **static asset compression**, **channel tool display splitting**, and **automatic context‑window detection** – all of which already have open PRs or strong community backing.

---

## 7. User Feedback Summary

**Positive signals:**
- Community is actively contributing (first‑time contributor [#6204](https://github.com/agentscope-ai/QwenPaw/pull/6204)), and maintainers are responsive.
- The move to 2.0 is bringing many wanted features despite some migration pains.

**Pain points & dissatisfaction:**
- **Windows desktop experience** remains the biggest friction point – admin‑privilege issues, force‑kill shutdown, and broken progressive rendering are repeatedly reported.
- **MCP startup performance** (sequential) and **message dropping** (no queue) are top blockers for power users.
- **Upgrade from 1.x to 2.0** has caused multiple regressions (embedding, auto‑memo, system prompt handling) that are not yet fully resolved.
- **Channel tool results** are considered too verbose; users want truncation and toggling.

**Use cases:**
- Multi‑agent deployments (36+ agents) needing bounded startup memory ([#6144](https://github.com/agentscope-ai/QwenPaw/issues/6144)).
- Cross‑platform setups (Windows + Linux) with media file path inconsistencies ([#5934](https://github.com/agentscope-ai/QwenPaw/issues/5934)).
- Daily use of MEMORY.md and Dream digest – users seek clearer documentation on their distinct roles ([#6222](https://github.com/agentscope-ai/QwenPaw/issues/6222)).

---

## 8. Backlog Watch

Important items that have been open for **7+ days without maintainer response or fix PR**:

| Issue / PR | Opened | Days open | Why it matters |
|------------|--------|-----------|----------------|
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) | 2026‑07‑12 | 6 | Messages dropped when busy – no workaround; affects all channel integrations |
| [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155) | 2026‑07‑15 | 3 | Upgrade regressions blocking users from adopting 2.0 |
| [#5698](https://github.com/agentscope-ai/QwenPaw/pull/5698) | 2026‑07‑01 | 17 | 💤 `run_tool_batch` adaptation to AgentScope 2.0 – no review activity |
| [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) | 2026‑06‑14 | 34

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-07-18

## Today’s Overview
The ZeptoClaw repository saw a quiet, maintenance-focused day. Eight issues were closed in the last 24 hours, all authored by YLChen-007 and representing routine “chore” updates to D5 gate-point metadata (gate_points, cross_component) for specific CVE JSON records tied to a CSV-based curation workflow. No pull requests were opened or merged, and no new releases were published. The absence of new feature work, bug reports, or community discussion suggests the project is currently in a data-refinement phase rather than active development.

## Releases
None.

## Project Progress
No PRs were merged or closed today. However, the eight closed issues (see below) reflect steady progress on the project’s internal data quality pipeline—specifically, the systematic re-analysis and updating of D5 gate metadata for rows 34–38 of the `all-exist-vuls-d5-gate-point-type-missing-data-collect.csv` file. Each issue corresponds to updating a single row’s JSON record (tied to issues #263, #264, #268, #329, #466) and writing a workflow completion receipt.

### Closed Issues (all chore/analysis)
- [#636 — chore(analysis): update D5 gate data for Issue-zeptoclaw-263 row 34](https://github.com/qhkm/zeptoclaw/issues/636)
- [#637 — chore(analysis): update D5 gate data for Issue-zeptoclaw-264 row 35](https://github.com/qhkm/zeptoclaw/issues/637)
- [#638 — chore(analysis): update D5 gate data for Issue-zeptoclaw-268 row 36](https://github.com/qhkm/zeptoclaw/issues/638)
- [#639 — chore(analysis): update D5 gate data for Issue-zeptoclaw-329 row 37](https://github.com/qhkm/zeptoclaw/issues/639)
- [#640 — chore(analysis): update D5 gate data for Issue-zeptoclaw-466 row 38](https://github.com/qhkm/zeptoclaw/issues/640)
- [#641 — chore(llm-enhance): refresh D5 gate metadata for issue 268 row 36](https://github.com/qhkm/zeptoclaw/issues/641)
- [#642 — chore(llm-enhance): refresh D5 gate metadata for issue 329 row 37](https://github.com/qhkm/zeptoclaw/issues/642)
- [#643 — chore(llm-enhance): refresh D5 gate metadata for issue 466 row 38](https://github.com/qhkm/zeptoclaw/issues/643)

These are essentially the same physical update tasks but tracked under two different issue labels (`analysis` vs `llm-enhance`) for the same rows, indicating a slightly redundant or parallel workflow.

## Community Hot Topics
There were no active discussions today. Each of the eight closed issues received exactly one comment (likely an automated confirmation or receipt) and zero reactions. The lack of engagement points to a workflow that is either fully tool-driven or involves only a single maintainer. No trending topics or user debates emerged.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The repository appears stable from a defect standpoint, with all activity focused on data curation rather than code changes.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. The recurring pattern of D5 gate-point metadata updates suggests that the project’s roadmap is currently centered on completing the coverage of a vulnerability dataset (the “all-exist-vuls” CSV) rather than adding new capabilities.

## User Feedback Summary
No explicit user feedback was captured in today’s issues or PRs. The only feedback signal is the steady closure of data-update tasks, implying that upstream consumers (likely an LLM-enhancement pipeline) are receiving the expected metadata refreshes. No expressions of satisfaction or dissatisfaction were recorded.

## Backlog Watch
No long-unanswered or high-priority issues were identified. All open issues (if any exist) were not updated today, and the only activity was the closure of the eight listed above. Maintainers may wish to review the status of any older data-collection or feature issues that have not seen updates in weeks, but none surfaced in the last 24 hours.

---

*Digest generated from ZeptoClaw public GitHub data for 2026-07-18.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-18

## 1. Today's Overview

ZeroClaw saw intense activity over the past 24 hours, with 50 issues and 50 pull requests updated. Of these, 42 issues remain open/active and 8 were closed; 40 PRs are open, and 10 were merged or closed. No new releases were published. The project continues to focus on security hardening (supply-chain signing, OIDC authentication, sandbox policies), multi-agent routing and A2A protocol support, and infrastructure improvements (Wasm plugin runtime, memory strategy decoupling). Several high-severity bugs were reported, particularly around macOS compatibility and agent workflow hangs, with a few fix PRs in progress. Community engagement remains strong, with multiple RFCs and feature requests attracting significant discussion.

## 2. Releases

None.

## 3. Project Progress (Closed/Merged PRs Today)

The following pull requests were closed (most likely merged) in the last 24 hours:

- **#8173 – feat(gateway): in-app upgrade with auto-restart from the web dashboard**  
  Implements RFC #8170, turning the sidebar version tag into a full “detect → show release notes → apply → restart” flow. (zeroclaw-labs/zeroclaw PR #8173)

- **#9045 – docs(architecture): document generated docs and localization lifecycles**  
  Clarifies which sources, generators, and checks own generated documentation and Fluent runtime catalog lifecycles. (zeroclaw-labs/zeroclaw PR #9045)

- **#8974 – docs(firmware): fix ESP32 hardware design link**  
  Corrects a broken link in the firmware README. (zeroclaw-labs/zeroclaw PR #8974)

- **#8896 – ci(actions): narrow benchmark compile experiment**  
  Reduces CI compilation scope to only the `agent_benchmarks` target under the lean `agent-runtime` feature graph. (zeroclaw-labs/zeroclaw PR #8896)

- **#8882 – test(api): cover escaped schema refs in properties**  
  Adds regression tests for escaped local `$ref` names in schema cleaner. (zeroclaw-labs/zeroclaw PR #8882)

- **#8768 – fix(zerocode): expose channel root settings**  
  Adds a root `[channels]` row to ZeroCode’s Config -> Channels type list. (zeroclaw-labs/zeroclaw PR #8768)

- **#8743 – test(config): cover LinkedIn Schema V4 removal scope**  
  Adds a focused config regression test for the LinkedIn schema removal. (zeroclaw-labs/zeroclaw PR #8743)

- **#8742 – docs(sop): add no-toml syntax examples**  
  Replaces empty SOP.toml section with authoring guidance and copyable examples. (zeroclaw-labs/zeroclaw PR #8742)

Several other PRs remain open and under active review (see Community Hot Topics).

## 4. Community Hot Topics

The most active discussions (by comment count or reactions) highlight critical security and architectural needs:

- **#8177 – RFC: Supply chain signing – hardware PGP, hermetic builds, SLSA provenance** (11 comments, 54 days old)  
  Proposes StageX-style supply-chain security for container images and release binaries. This RFC expands Phase 3 of the hardened CI pipeline.  
  (zeroclaw-labs/zeroclaw Issue #8177)

- **#5982 – Feature: Per-sender RBAC for multi-tenant agent deployments** (10 comments, 87 days old)  
  Requests optional per-sender role-based access control for multi-user ZeroClaw instances. High priority (P2) with strong backing.  
  (zeroclaw-labs/zeroclaw Issue #5982)

- **#3566 – Feature/interop: A2A (Agent-to-Agent) Protocol Support** (8 comments, 125 days old, 7 👍)  
  Native A2A protocol (v0.3.0+) support to enable inter-agent communication. This is a highly upvoted request.  
  (zeroclaw-labs/zeroclaw Issue #3566)

- **#6378 – Feature: Discord Bot respond only in specific channels** (7 comments, 74 days old)  
  Consistent with `allowed_rooms` pattern in Matrix/Nextcloud Talk.  
  (zeroclaw-labs/zeroclaw Issue #6378)

- **#7141 – RFC: OIDC authentication provider support** (7 comments, 45 days old)  
  Tracking issue for pluggable authentication-provider work, targeting v0.9.0.  
  (zeroclaw-labs/zeroclaw Issue #7141)

- **#6641 – Feature: Turn-level OTel trace correlation** (7 comments, 66 days old)  
  Follow-up to #6009 and #6190, aiming to nest spans under a single turn trace.  
  (zeroclaw-labs/zeroclaw Issue #6641)

- **#2767 – Feature: Multi-Agent Routing** (6 comments, 136 days old, 9 👍)  
  Isolated agents with separate workspaces and multiple channel accounts in one gateway. Second highest reaction count.  
  (zeroclaw-labs/zeroclaw Issue #2767)

The recurring themes are **security** (supply-chain, OIDC, RBAC) and **interoperability** (A2A, multi-agent routing). These issues are likely to shape the next major release (v0.9.0).

## 5. Bugs & Stability

Several bugs were reported or updated in the last 24 hours. Listed by severity:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| #8563 – SOPs not available via web dashboard chat | S1 (workflow blocked) | Standard Operating Procedures configured under `shared/sops` are not detected by agent runtime. | No fix PR yet. |
| #8560 – `browser_open` hangs agent turn | S1 (workflow blocked) | When browser can’t open a window, the agent hangs indefinitely. Also affects TTS and ffmpeg channels. | In progress (status:in-progress) |
| #7527 – macOS app not working | S1 (workflow blocked) | Post-install, app can’t detect permissions; window disappears after restart. | No fix PR; blocked. |
| #5628 – Daemon port conflict on auto-start | S2 (degraded) | systemd service binds to port 42617, preventing manual `zeroclaw daemon` runs. | No fix PR. |
| #5869 – RUSTSEC advisory cluster via rumqttc | S1 (security) | 4 advisories blocked by transitive dependency `rumqttc v0.25.1`. | Blocked by upstream. |
| #5269 – Installation documentation gaps | S2 (degraded) | `cargo binstall zeroclaw` not documented; general UX issues. | No fix PR. |

Additionally, PRs addressing bugs:
- **#8845** (open, size:S) – Fixes live session rebuild on model_provider edits.
- **#8913** (open, size:XS) – Adds visible reason when agent stops due to max tool iterations.
- **#8996** (open, size:XL) – Preserves running goals across daemon reload.

## 6. Feature Requests & Roadmap Signals

Major feature requests and RFCs that are likely candidates for the next version (v0.9.0) include:

- **Pluggable Authentication & Security**  
  - #7141 – OIDC authentication provider support (RFC, target v0.9.0)  
  - #7142 – Pluggable security enforcement provider interface (RFC, target v0.9.0)  
  - #6250 – Route-layer auth middleware on `/api/config` and `/api/onboard`

- **Interoperability & Multi-Agent**  
  - #3566 – A2A protocol support (v0.3.0+)  
  - #2767 – Multi-agent routing (9 👍)  
  - #7218 – A2A agent discovery via `.well-known/agent-card.json`

- **Security Hardening**  
  - #8177 – Supply-chain signing, SLSA provenance (RFC, Phase 3)  
  - #8135 – Wasm-first plugin runtime with signed distribution  
  - #6293 – Air-gapped execution mode with companion daemon (blocked)  
  - #6996 – Granular sandbox policy (filesystem/network)

- **Memory & Observability**  
  - #6850 – Decouple memory lifecycle policy from storage backends (RFC)  
  - #8891 – Persistent memory parity tracker  
  - #6641 – Turn-level OTel trace correlation (in progress)

- **Usability & Docs**  
  - #7762 – Cron documentation and model-specific cron jobs  
  - #8367 – Capability-aware documentation for agent-visible features  
  - #6378 – Discord channel-specific responses

These features indicate a strong push toward enterprise-grade security, multi-tenant support, and ecosystem interoperability.

## 7. User Feedback Summary

User-reported pain points (captured in issues) reveal several recurring frustrations:

- **Installation & configuration friction** (#5269, #5628): Users struggle with documentation gaps and port conflicts when running daemon alongside systemd service. The lack of clear installation docs for `cargo binstall` is noted.
- **macOS crashing** (#7527): The app fails to detect permissions and becomes unusable on macOS 15.7.7, leading to complete workflow blockage.
- **Web dashboard SOPs not working** (#8563): Critical feature (Standard Operating Procedures) not accessible via web UI – a blocking issue for users relying on the dashboard.
- **Browser open hangs** (#8560): The agent turn hangs indefinitely when no display is available. This affects headless deployments.
- **TUI editing limitations** (#7467, #7468): Users want arrow-key navigation in edit strings and the ability to rename aliases, indicating demand for a more polished TUI experience.
- **Cron documentation missing** (#7762): Users cannot find documentation for cron jobs or set them to use specific (cheaper) models – a common use case.

Overall, while the project is advancing rapidly on core architecture, end-user experience (docs, macOS stability, TUI polish) needs attention.

## 8. Backlog Watch

Issues and PRs that have been open for a long time or require maintainer action:

- **#6293 – RFC: Air-gapped execution mode** (created 2026-05-03, 75 days open, status:blocked, needs-author-action)  
  Blocked; no recent maintainer response. (zeroclaw-labs/zeroclaw Issue #6293)

- **#5869 – security: rumqttc RUSTSEC advisory cluster** (created 2026-04-18, 91 days open, status:blocked)  
  Blocked by upstream dependency; maintainers may need to consider switching MQTT client. (zeroclaw-labs/zeroclaw Issue #5869)

- **#8367 – RFC: capability-aware documentation** (created 2026-06-26, 22 days open, needs-maintainer-review)  
  Has only 2 comments; no maintainer review yet. (zeroclaw-labs/zeroclaw Issue #8367)

- **#8891 – Tracker: Persistent memory parity** (created 2026-07-09, 9 days open, needs-maintainer-review)  
  A milestone tracking issue; needs maintainer sign-off. (zeroclaw-labs/zeroclaw Issue #8891)

- **PRs with `needs-author-action`** (requiring author revision):  
  - #8996 – fix(goal): preserve running goals across daemon reload (risk:high, size:XL)  
  - #8384 – feat(inkbox): add native Inkbox channel (risk:high, size:XL)  
  - #8443 – feat(matrix): add single-message progress drafts (risk:high, size:XL)  
  - #8866 – fix(daemon): share MCP registry across heartbeat ticks (risk:high, size:XL)  
  - #8638 – feat(skills)!: replace ClawHub with git-catalog (risk:high, size:L)  

These may be stalled due to missing author responses; maintainers should follow up.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*