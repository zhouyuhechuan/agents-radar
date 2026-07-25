# OpenClaw Ecosystem Digest 2026-07-25

> Issues: 463 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-25 01:59 UTC

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

# OpenClaw Project Digest — 2026-07-25

## Today’s Overview

OpenClaw sees extremely high activity in the last 24 hours: 463 issues updated (355 still open, 108 closed) and 500 pull requests updated (203 open, 297 merged/closed). No new releases arrived today, but the sheer volume of updates signals intense community and development engagement. The project is stable in terms of releases but grappling with a long tail of regressions, provider-specific bugs, and longstanding feature requests. Many high-impact issues remain unresolved, though nearly 300 PRs were merged or closed, indicating active maintainer throughput.

## Releases

No new releases were published today. The latest available version remains the previously released 2026.7.x series (2026.7.2-beta.3 being the newest per issues). No migration notes or breaking changes to report.

## Project Progress

**297 pull requests were merged or closed in the last 24 hours**, reflecting a healthy rate of fix and feature integration. Notable among the top-commented PRs (which are mostly still open or waiting for review):

- **#113459** (`fix(sqlite): prevent stale verifier quarantine after database replacement`) — a direct fix for issue #113306.
- **#113176** (`fix(googlechat): honor lowercase no_proxy when NO_PROXY is blank`) — solves proxy bypass misconfiguration.
- **#112416** (`fix(compaction): thread agent streamFn into safeguard summarizer`) — addresses a compaction bug for OpenRouter models.

Several closed PRs in the top-30 list include **#113450** (`feat(ui): render chat notice rows as markdown` — a small UI enhancement) and **#113226** (`fix: workflow sanity audit passes on main`). The high merge count suggests maintainers are actively pushing fixes through, though the backlog of open issues remains large.

## Community Hot Topics

The most active threads (by comment count and reactions) highlight persistent pain points:

1. **#102020** (16 comments, 1 👍) — “Second message in a session fails with 'reply session initialization conflicted'” – cross-channel, position-dependent. Represents a fundamental session handling bug that undermines multi-turn conversations.

2. **#86996** (14 comments, 2 👍) – “Active Memory + Codex app-server path causes long response latency, hook timeouts, startup aborts, and gateway event-loop stalls” – a P1 with diamond lobster rating, stuck in `needs-maintainer-review` and `needs-product-decision`. Huge impact on users relying on Active Memory.

3. **#94228** (14 comments, 2 👍) – “Native Anthropic path: replaying historical thinking blocks bricks long tool-use threads” – 400 errors on thinking block signatures. Blocks Anthropic users on long sessions.

4. **#92043** (13 comments, 3 👍) – “180s compaction timeout is a single wall clock over the whole chunk pipeline with no partial-progress reuse”. Causes repeated compaction failures for legitimate long workloads.

5. **#107220** (10 comments, 1 👍, CLOSED) – “Fatal gateway crash-loop on 2026.7.1: legacy memory sidecar meta/chunks conflicts”. A critical P0 that was apparently resolved, but its high comment count reflects the urgency.

The community’s core concerns revolve around **session reliability, provider-specific compatibility (Anthropic, OpenAI, Google), and compaction/performance regressions** introduced in recent releases.

## Bugs & Stability

Several high-severity bugs were reported or updated in the last 24 hours:

- **#113306** (P1, 7 comments, new) – “SQLite snapshot restore lacks end-to-end crash and identity guarantees”. A fresh bug with a fix PR already submitted (#113459). Impacts data safety.
- **#106786** (P1, 5 comments) – “gpt-5.6-* is advertised on ChatGPT-OAuth, then silently falls back when rejected”. Silent fallback misleads users.
- **#111498** (P1, regression) – “Main agent blocked by persistent workspace-state migration after Anthropic auth recovery”. Blocks entire agent operation after credential recovery.
- **#111519** (P1, regression) – “Telegram DM replies fall back after stale DM-scope cleanup”. Communication reliability issue.
- **#112906** (new) – “`\`\`` renders broken in v2026.7.1 / v2026.7.1-2 (rich messages regression)”. Markdown parsing regression in recent release.

Many of these have no linked fix PRs (marked `clawsweeper:no-new-fix-pr`). The long-standing P1/P0 bugs from prior weeks (e.g., #86996, #92043, #94228) remain open, indicating a need for more maintainer resources to break through the backlog.

## Feature Requests & Roadmap Signals

Several feature requests received active discussion:

- **#110950** (10 comments, 2 👍, CLOSED) – “Everything is a cron — unify heartbeat, watchers, and scheduled automation”. This ambitious proposal to merge all automation into a single cron primitive was closed, perhaps deferred or merged into an internal design.
- **#7722** (10 comments, 4 👍) – “Filesystem Sandboxing Config (tools.fileAccess)”. High community demand (most 👍 today) for security controls. Stuck in `needs-security-review`.
- **#10687** (10 comments, 3 👍) – “Models: fully dynamic model discovery (OpenRouter + beyond)”. A long-requested feature to keep model lists up to date.
- **#45758** (8 comments, 2 👍) – “Support YAML as config file format”. Still waiting for maintainer review and product decision.
- **#38520** (6 comments, 1 👍) – “Pre-compaction agent notification, structured handoff window, and deferral mechanism”. A safety feature for long-running workflows.

Next release likely includes fixes for the top crash/regression bugs (e.g., #107220 already closed, #113306 fix submitted). The feature roadmap seems less defined; many requests are in `needs-maintainer-review` or `needs-product-decision` for weeks.

## User Feedback Summary

User pain points center on:

- **Unreliable multi-turn sessions**: Cross-channel and position-dependent failures (#102020, #47975) cause frustration.
- **Provider-specific issues**: Anthropic thinking block errors (#94228), Ollama streaming not consumed (#94251), Google Antigravity bans (#44134) – users feel forced into certain providers.
- **Configuration migration surprises**: Cron store migration without user visibility (#90378) and silent fallback on model errors (#106786) erode trust.
- **Performance regressions**: Compaction timeout becomes failure (#92043), bloat from re-injected bootstrap files (#67419), and prompt-cache not working (#95610) increase costs.
- **Security concerns**: Filesystem sandboxing (#7722), skill permission manifest (#12219), and 1Password exec integration (#102293 PR) show demand for better security governance.

Satisfaction is evident in high merge activity (297 PRs) and the willingness of contributors to file detailed reports, but the sheer number of open critical issues indicates the project is struggling with technical debt from rapid feature growth.

## Backlog Watch

Several important issues and PRs have been outstanding for weeks or months without maintainer action:

- **#86996** (P1, diamond lobster) – Active Memory + Codex latency. Last updated 2026-07-25 but still marked `needs-maintainer-review` and `needs-product-decision` since May 26.
- **#92043** (P1, diamond lobster) – Compaction timeout failure. Same staleness, no fix PR.
- **#94228** (P1, platinum hermit) – Anthropic thinking block bug. `needs-live-repro` since June 17.
- **#7722** (P2, diamond lobster) – Filesystem sandboxing. `needs-security-review` since February.
- **#10687** (P2, platinum hermit) – Dynamic model discovery. `needs-maintainer-review` since February.
- **#102293 PR** (XL, waiting on author) – 1Password exec SecretRef plugin. Important for enterprise deployments but stalled.
- **#95333 PR** (XL, P1, `needs proof`) – Trusted inbound-decoration contract – a heavy PR that addresses a core security design issue, waiting since June 20.

These items represent the most impactful gaps in the project’s current state. Without maintainer decisions, the community’s confidence in the roadmap may suffer.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

**Date:** 2026-07-25  
**Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing a **development surge**, with the core reference implementation (OpenClaw) processing nearly 1,000 issues and PRs in 24 hours, while specialized forks and derivatives advance at varying velocities. The ecosystem is bifurcating between **generalist platforms** (OpenClaw, ZeroClaw, IronClaw) aiming for all-purpose agent orchestration, and **niche-optimized agents** targeting specific channels, providers, or deployment models (NanoBot for local-first, CoPaw for team collaboration, LobsterAI for IM-heavy Chinese workflows). A clear pattern emerges: **session reliability, provider compatibility, and performance under load** are the universal pain points, while security governance and configuration UX remain persistent gaps across nearly every project. The ecosystem is maturing rapidly but carrying significant technical debt from rapid feature growth, with downstream projects benefiting from upstream fixes while also surfacing divergent priorities.

---

## 2. Activity Comparison

| Project | Issues Updated (Open/Closed) | PRs Updated (Open/Merged-Closed) | Release This Period | Activity Health Score |
|---------|------------------------------|----------------------------------|---------------------|----------------------|
| **OpenClaw** | 463 (355 open, 108 closed) | 500 (203 open, 297 merged/closed) | ❌ | **High** – Massive throughput, but large open backlog |
| **ZeroClaw** | 47 (39 open, 8 closed) | 50 (40 open, 10 merged/closed) | ❌ | **High** – Sustained sprint, heavy RFC activity |
| **IronClaw** | 32 (26 open, 6 closed) | 50 (31 open, 19 merged/closed) | ❌ | **High** – Bug bash and v1 launch prep driving activity |
| **Hermes Agent** | 50 (32 open, 18 closed) | 50 (42 open, 8 merged/closed) | ❌ | **High** – Responsive, but PR backlog growing |
| **CoPaw** | 50 (28 open, 22 closed) | 37 (23 open, 14 merged/closed) | ✅ **v2.0.1** | **High** – Healthy ratio, new release with PawApp platform |
| **LobsterAI** | 19 (19 open, 0 new) | 50+ (7+ open, 43 merged/closed) | ✅ **2026.7.23** | **Medium-High** – Heavy merge activity, but security PRs stalled |
| **NanoBot** | 4 (2 open, 2 closed) | 24 (4 open, 20 merged/closed) | ❌ | **High** – Rapid iteration toward v0.3.0, focused scope |
| **PicoClaw** | 3 (1 open, 2 closed) | 8 (1 open, 7 merged/closed) | ❌ | **Moderate** – Steady clean-up, small team |
| **NanoClaw** | 0 | 7 (6 open, 1 closed–erroneous) | ❌ | **Low-Moderate** – Consolidation phase, no community engagement |
| **Moltis** | 0 | 2 (2 open, 0 merged) | ❌ | **Low** – Focused Slack-only development, low activity |
| **ZeptoClaw** | 2 (2 open, 0 closed) | 2 (1 open, 1 merged) | ❌ | **Low** – Small scope, critical CI issue pending |
| **NullClaw** | 0 | 0 | ❌ | **Inactive** – No activity |
| **TinyClaw** | 0 | 0 | ❌ | **Inactive** – No activity |

**Health Score Criteria:** Merge/closure rate relative to open items, presence of releases, community engagement (comments/reactions), response time to critical bugs.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Largest community & contributor base** – 463 issues and 500 PRs in 24 hours dwarfs every other project. This creates a virtuous cycle of faster bug discovery, broader provider coverage, and richer integrations.
- **Breadth of integration** – No other project matches OpenClaw's provider support (OpenAI, Anthropic, Google, Ollama, OpenRouter, etc.) or channel span (Telegram, Slack, Discord, Web), making it the default choice for multi-environment deployments.
- **Reference implementation status** – As `openclaw/openclaw`, it sets architectural patterns that forks like PicoClaw, NanoClaw, and ZeptoClaw inherit. Design decisions here ripple downstream.

**Technical Approach Differences:**
- **Monolithic reference architecture** – Unlike IronClaw's Rust-native focus or NanoBot's modular TypeScript approach, OpenClaw maintains a comprehensive stack that prioritizes completeness over optimization. This leads to richer features but also to the "long tail of regressions" visible in its backlog.
- **Compaction-driven session management** – OpenClaw's aggressive session compaction strategy (visible in issues like #92043) is unique; other projects either lack compaction (NanoBot) or use simpler truncation (PicoClaw). This gives OpenClaw better long-session memory but at the cost of timeout and reliability issues.

**Community Size Comparison:**
- OpenClaw's 297 merged PRs/day vs. CoPaw's 14 and LobsterAI's 43 demonstrates ~7-20x more contribution throughput.
- However, **issue resolution ratio**: OpenClaw closes 23% of its issues (108/463), while CoPaw closes 44% (22/50) and Hermes closes 36% (18/50). This suggests OpenClaw's scaling is outpacing its maintenance capacity.

**Risk:** OpenClaw's massive issue backlog (355 open) includes critical P0/P1 bugs persisting for weeks (Active Memory + Codex latency #86996 since May, Anthropic thinking block #94228 since June). If unresolved, this could fragment the community toward more stable forks.

---

## 4. Shared Technical Focus Areas

**Cross-project requirements emerging in the last 24 hours:**

| Requirement | Affected Projects | Specific Pain Points |
|-------------|-------------------|---------------------|
| **Session reliability & multi-turn state** | OpenClaw, Hermes, CoPaw, NanoBot, ZeroClaw | #102020 (OpenClaw): cross-channel session init conflicts. #4064 (NanoBot): pending messages losing context. #6401 (CoPaw): cron tasks overwriting history. #9340 (ZeroClaw): cron output silently discarded. |
| **Provider-specific compatibility fixes** | OpenClaw, NanoBot, LobsterAI, CoPaw | #94228 (OpenClaw): Anthropic thinking block. #1813 (LobsterAI): DeepSeek V4 schema rejection. #6407 (CoPaw): ReAct tool_result mixing with assistant messages. #4867 (NanoBot): Ollama KV-cache prefix drift. |
| **Performance & compaction optimization** | OpenClaw, Hermes, CoPaw, PicoClaw | #92043 (OpenClaw): 180s compaction timeout. #6307 (CoPaw): 2s fixed overhead per reply. #71097 (Hermes): in-place compression failure. #3244-3245 (PicoClaw): string allocation reduction. |
| **Security & sandboxing** | OpenClaw, ZeroClaw, LobsterAI, ZeptoClaw | #7722 (OpenClaw): filesystem sandboxing config. #9247 (ZeroClaw): symlink workspace bypass. #1885 (LobsterAI): email path traversal. PR #645 (ZeptoClaw): runtime secrets leakage. |
| **Streaming across channels** | NanoBot, ZeptoClaw, Moltis, ZeroClaw | PR #648 (ZeptoClaw): Telegram streaming added. PR #4567 (NanoBot): WeChat streaming fix. PR #1165-1166 (Moltis): Slack acknowledgments & streaming. #8228 (ZeroClaw): DingTalk streaming request. |
| **Configuration UX & migration** | OpenClaw, Hermes, ZeroClaw, CoPaw | #8834 (ZeroClaw): config alias creation. #5980 (CoPaw): v2 migration missing features. #71125-71127 (Hermes): config CLI overhaul. #106786 (OpenClaw): silent model fallback. |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | Hermes | NanoBot | CoPaw | LobsterAI |
|-----------|----------|----------|----------|--------|---------|-------|-----------|
| **Primary language** | Multi-stack | Rust | Rust | Python | TypeScript | Python | TypeScript |
| **Target deployment** | Self-hosted | Self-hosted + Cloud | Self-hosted + Managed | Desktop + Server | Desktop + Local-first | Team-collab | IM-centric (Chinese) |
| **Key architectural focus** | Session compaction, provider abstraction | Goal-stack, plugin SDK, governance | Error recoverability, Hermetic testing | MCP, Windows parity, billing | Modular, caching, WebUI polish | PawApp mini-apps, multi-agent | Cowork, scheduled tasks, security |
| **Community engagement model** | Broad contributor base, slow triage | RFC-driven, contributor-heavy | QA/bug-bash driven | Responsive but backlog | Rapid iteration, issue-driven | Active maintainers, feature-gated | Youdao-internal + external |
| **Unique strength** | Largest integration surface | Most advanced RFC/planning process | Formal v1 launch rigor | Best Windows/desktop parity | Fastest iteration cycle | Strongest team-collab & Kanban | Best Chinese IM integration |
| **Unique weakness** | Technical debt, slow fix turnaround | Many PRs awaiting author action | Slack/Telegram stability fragile | Windows encoding hell | Ollama performance cliff | v2 migration pain | Security PRs stalled 3 months |

**Key Differentiating Factors:**

- **IronClaw** is the only project with a formal v1 launch checklist and structured bug bash process, indicating a release engineering maturity absent in other projects.
- **ZeroClaw** leads in governance innovation (work lanes, plugin catalog, wire protocol RFCs) but carries high architectural risk from ambitious RFCs.
- **Hermes** is uniquely focused on **Windows desktop parity**, a pain point largely ignored by other projects. Its MCP support depth is second only to OpenClaw.
- **NanoBot** and **PicoClaw** are optimized for **lightweight, local-first** use cases – NanoBot's rapid WebUI polish and PicoClaw's i18n efforts contrast with the heavy infrastructure focus of ZeroClaw/IronClaw.
- **CoPaw** uniquely targets **team collaboration** with its PawApp mini-app platform and Kanban board, positioning it as an enterprise workflow tool rather than a personal assistant.

---

## 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration & High Momentum**
- **NanoBot** – Highest velocity relative to scope. 20 PRs merged/closed in 24 hours with clear v0.3.0 trajectory. Responsive to community feedback (Ollama caching acknowledged, WeChat streaming fixed same-day). Exceptionally healthy for its size.
- **CoPaw** – Released v2.0.1 with PawApp platform while closing 44% of issues. Active maintainers shipping features and fixes simultaneously. High community feature demand (11 requests from single power user) shows engagement.

**Tier 2: High Activity, Mixed Stability**
- **OpenClaw** – High merge throughput but accumulating critical debt. 355 open issues with 60+ P1 bugs. Community engagement is massive but maintainer bandwidth is strained. **Risk of contributor fatigue** if long-standing bugs (#86996, #94228) remain unfixed.
- **ZeroClaw** – Deeply engaged RFC process (5 active RFCs) with 10 PRs merged/closed. Heavy architectural work in progress (goal-stack, plugin SDK). However, many PRs stalled on `needs-author-action` – momentum could stall if contributors don't respond.
- **IronClaw** – Active bug bash with 19 PRs merged, but the Slack/Telegram P1 bugs are serious regression risks for the v1.0.0 release. v1 launch is clearly driving activity, but quality gates may slip.

**Tier 3: Steady, Focused Development**
- **Hermes** – Busy triage (50 issues, 8 merged PRs) but low issue closure ratio (36%). Windows bugs keep surfacing without systemic fix. Responsive but reactive – no major feature releases imminent.
- **LobsterAI** – High PR merge count (43) with new release (2026.7.23), but 3-month unmerged security PRs are a red flag. Activity is inward-focused (cowork, build) rather than community-driven.

**Tier 4: Low Activity / Consolidation**
- **PicoClaw** – Modest but clean activity. 7 PRs merged, CI fixed quickly. Appears healthy for its scope but unlikely to see major expansion.
- **NanoClaw** – No community engagement, 6 open PRs with zero comments. Consolidation phase with unclear future momentum.
- **Moltis**, **ZeptoClaw** – Very small scope, single-contributor or near-single-contributor activity. Not viable for ecosystem-wide impact.
- **NullClaw**, **TinyClaw** – Inactive. Unclear if projects are abandoned or dormant.

---

## 7. Trend Signals

**Emerging Industry Trends from Community Feedback:**

1. **Session State is the #1 Quality Gate**
   - Across all active projects, session initialization conflicts, context loss, and history corruption are the most complained-about issues. Users expect **persistent, reliable multi-turn conversations** as table stakes. Projects that solve this (IronClaw's error-recoverability epic, OpenClaw's compaction fixes) will have a competitive advantage.

2. **Caching Efficiency is Critical for Local Models**
   - NanoBot (#4867: 60s overhead per Ollama turn) and OpenClaw (#95610: prompt-cache not working) both surface the same finding: **KV-cache reuse is broken** in many agent stacks. As local models (Llama, Qwen, DeepSeek) gain adoption, prompt prefix preservation and cache-aware architecture become make-or-break features.

3. **MCP is Becoming an Integration Standard**
   - Hermes (MCP Smart Loading #66473), CoPaw (Repeated MCP registration #2999), ZeroClaw (plugin SDK reflecting MCP patterns), and several others are investing in MCP compatibility. **Agent-to-tool protocol standardization** is emerging as a key interoperability requirement.

4. **Security Governance is Moving from Nice-to-Have to Requirement**
   - Multiple projects face real security bugs: OpenClaw filesystem sandboxing (#7722), ZeroClaw symlink bypass (#9247), LobsterAI path traversal (#1885), ZeptoClaw secrets leakage (PR #645). **The ecosystem is being forced to harden** as agents gain access to files, credentials, and production systems.

5. **Multi-Channel Streaming is Non-Negotiable**
   - Telegram streaming (ZeptoClaw), WeChat streaming (NanoBot), Slack ack/Block Kit (Moltis), and DingTalk streaming (ZeroClaw) all received attention this 24-hour period. **Users expect real-time, progressive responses across all messaging platforms**, not just the WebUI.

6. **Configuration Drift is a Universal UX Pain Point**
   - Silent model fallback (OpenClaw), dual config sources (Hermes), alias bugs (ZeroClaw), migration-surprise features (CoPaw) – configuration is the most consistent source of user confusion. **Declarative, validated, migration-safe config** is an unmet need across the ecosystem.

7.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-25

## Today’s Overview
The project saw an intense burst of activity with **24 PRs updated** in the last 24 hours—20 of which were merged or closed. This signals a high-velocity development cycle, likely in preparation for a **v0.3.0 release** (chore PR #5081 is already open). Meanwhile, **four issues were updated** (two closed, two open), indicating focused triage. No new releases were published today, but the codebase is clearly moving toward a major milestone.

## Releases
*(No new releases today)*

## Project Progress
Today’s **20 merged/closed PRs** span frontend, agent, provider, and branding improvements:

- **Branding & UX**  
  – [#5080](https://github.com/HKUDS/nanobot/pull/5080) replaced README and WebUI assets with scalable SVGs.  
  – [#5079](https://github.com/HKUDS/nanobot/pull/5079) added an official SVG logo.  
  – [#5078](https://github.com/HKUDS/nanobot/pull/5078) launched a first-time setup flow directly in the WebUI (retaining terminal wizard).  

- **WebUI enhancements**  
  – [#5077](https://github.com/HKUDS/nanobot/pull/5077) added model preset switching from the composer via long-press.  
  – [#5071](https://github.com/HKUDS/nanobot/pull/5071) fixed quoted context display after follow-up sends.  
  – [#5060](https://github.com/HKUDS/nanobot/pull/5060) polished responsive layouts and settings search.  
  – [#5031](https://github.com/HKUDS/nanobot/pull/5031) resolved mobile welcome composer overlap.  
  – [#5076](https://github.com/HKUDS/nanobot/pull/5076) fixed custom gateway port handling with Vite.  

- **Agent & tooling**  
  – [#5074](https://github.com/HKUDS/nanobot/pull/5074) introduced inline subagent consultation with `wait=true`.  
  – [#5075](https://github.com/HKUDS/nanobot/pull/5075) made authorized tasks proceed through verification without unnecessary confirmations.  
  – [#5073](https://github.com/HKUDS/nanobot/pull/5073) fixed preservation of multimodal tool outputs (text, image, file blocks) across provider conversions.  
  – [#5049](https://github.com/HKUDS/nanobot/pull/5049) corrected delivery of non-streamed finalization responses.  

- **Streaming & channel fixes**  
  – [#4567](https://github.com/HKUDS/nanobot/pull/4567) fixed WeChat streaming by adding `streaming` field to `WeixinConfig`.  
  – [#5050](https://github.com/HKUDS/nanobot/pull/5050) surfaced xAI hosted X Search as structured agent activity.  
  – [#4696](https://github.com/HKUDS/nanobot/pull/4696) (still open) improves streaming Markdown reveal with a buffered rAF scheduler.  

- **Other**  
  – [#4963](https://github.com/HKUDS/nanobot/pull/4963) replaced raw tool logs with one-line activity language and improved streamed answer rendering.  
  – [#5053](https://github.com/HKUDS/nanobot/pull/5053) pinned migration TODOs to v0.2.4 for pending deprecations.  

## Community Hot Topics
| Issue/PR | Description | Comments | Status |
|----------|-------------|----------|--------|
| [#4867](https://github.com/HKUDS/nanobot/issues/4867) | Preserve exact prompt prefix to enable caching (Ollama) – 23 comments | **Closed** – The user reports a 60-second overhead per turn with Ollama/32GB VRAM, making the system unusable. The feature request aims to keep prompt prefixes identical to leverage KV-cache. High-priority. | Closed via earlier PRs? |
| [#4637](https://github.com/HKUDS/nanobot/issues/4637) | Telegram long message split – trunks fail to render after the first (4 comments) | **Closed** – Markdown truncation issue; partly addressed. | Closed |
| [#4858](https://github.com/HKUDS/nanobot/issues/4858) | Refactor dynamic tool provider lifecycle out of AgentLoop (2 comments) | **Open** – MCP lifecycle is currently hardwired into AgentLoop; proposes a generalized provider abstraction. | Under discussion |
| [#4064](https://github.com/HKUDS/nanobot/issues/4064) | Pending mid-turn messages lose sender/channel/chat runtime context (1 comment, 1 👍) | **Open** – Queued messages are injected as plain `{"role": "user"}` without runtime identity. Dating from May 2026. | Still unaddressed |

The **most active thread** is #4867 (23 comments), reflecting strong community demand for Ollama cache efficiency—a make-or-break for local LLM users.

## Bugs & Stability
- **Critical** – [#4064](https://github.com/HKUDS/nanobot/issues/4064): Pending mid-turn messages lose channel/sender context. Open since May 2026 with only 1 comment. **No fix PR in flight**; a revert PR [#5072](https://github.com/HKUDS/nanobot/pull/5072) was merged today that *removes* an earlier attempt (#4665) to fix this because it became stale after the `RuntimeContextProvider` refactor. The bug remains active.
- **High** – [#4867](https://github.com/HKUDS/nanobot/issues/4867) (closed) performance regression with Ollama. While closed, the root cause (prompt prefix drift) may still affect users if not preserved in config.  
- **Medium** – [#4637](https://github.com/HKUDS/nanobot/issues/4637): Telegram message truncation was closed but the fix may be partial; no follow-up reported.  
- **Fixed today** – [#5049](https://github.com/HKUDS/nanobot/pull/5049) fixed a regression where non-streamed finalization responses were dropped. [#5071](https://github.com/HKUDS/nanobot/pull/5071) fixed quoted context display. [#4567](https://github.com/HKUDS/nanobot/pull/4567) fixed WeChat streaming not being enabled.

## Feature Requests & Roadmap Signals
- **Caching** – [#4867](https://github.com/HKUDS/nanobot/issues/4867) demands a mechanism to preserve exact prompt prefixes for KV-cache reuse in Ollama and similar providers. Likely to land in v0.3.0 given community outcry.
- **Tool lifecycle refactor** – [#4858](https://github.com/HKUDS/nanobot/issues/4858) aims to extract MCP and future tool providers out of `AgentLoop`. This architectural change signals preparation for a plugin ecosystem.
- **Inline subagent** – Merged [#5074](https://github.com/HKUDS/nanobot/pull/5074) adds `wait` argument to spawn tool for direct results. This is a new feature already in main.
- **WebUI polish** – First-time setup ([#5078](https://github.com/HKUDS/nanobot/pull/5078)), preset switching ([#5077](https://github.com/HKUDS/nanobot/pull/5077)), and branded SVGs ([#5079](https://github.com/HKUDS/nanobot/pull/5079), [#5080](https://github.com/HKUDS/nanobot/pull/5080)) are clearly aimed at improving onboarding and aesthetics for v0.3.0.
- **Streaming Markdown** – [#4696](https://github.com/HKUDS/nanobot/pull/4696) (open) proposes a smoother reveal animation; if merged, it will enhance perceived speed.

**Prediction**: v0.3.0 (preparation in [#5081](https://github.com/HKUDS/nanobot/pull/5081)) will likely include caching improvements, the tool lifecycle refactor, inline subagent, and many WebUI UX upgrades.

## User Feedback Summary
- **Pain point: Ollama performance** – User *The-Markitecht* (issue #4867) reports **60 seconds added per turn** with 32 GB VRAM, calling the system “totally unusable” with Ollama. The community contributed 23 comments, indicating widespread validation.
- **Pain point: Telegram message handling** – User *MARJORIESHA-pBAD* (#4637) found that long markdown messages are truncated and only the first trunk renders; the fix was merged but multiple users may still encounter this.
- **Pain point: Context metadata loss** – User *hamb1y* (#4064) reports pending messages injected without channel/sender identity, breaking workflows that rely on runtime context.
- **Satisfaction** – Quick turnaround on WeChat streaming fix ([#4567](https://github.com/HKUDS/nanobot/pull/4567)) and WebUI layout bugs ([#5031](https://github.com/HKUDS/nanobot/pull/5031)) show responsive maintainers.

## Backlog Watch
| Item | Type | Age | Priority | Notes |
|------|------|-----|----------|-------|
| [#4064](https://github.com/HKUDS/nanobot/issues/4064) | Bug (open) | 57 days | High | Pending messages lose context; no current fix after revert. Needs design with new `RuntimeContextProvider`. |
| [#4858](https://github.com/HKUDS/nanobot/issues/4858) | Refactor (open) | 16 days | Medium | Low comments but architectural importance; needed to prevent further MCP coupling. |
| [#4383](https://github.com/HKUDS/nanobot/pull/4383) | Enhancement PR (open, conflict) | 38 days | Medium | Globalping MCP preset – merge blocked by conflicts; useful for network diagnostics. |
| [#4696](https://github.com/HKUDS/nanobot/pull/4696) | Feature PR (open) | 21 days | Low-Medium | Streaming Markdown reveal; waiting for review. Many related polish PRs have already merged. |

---

*Project health: High activity with clear momentum toward v0.3.0, but the lingering #4064 bug and unresolved Ollama caching issue (despite closed issue) remain concerns for local-model users.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-25

## 1. Today's Overview

The Hermes Agent project saw very high activity in the past 24 hours: **50 issues updated** (32 open, 18 closed) and **50 pull requests** (42 open, 8 merged/closed). No new releases were cut today. The community continues to surface **Windows‑specific encoding bugs** (UTF‑8 BOM, GBK, cp1252) as a primary pain point, while core contributors are pushing fixes for session‑state corruption, gateway reliability, and billing accuracy. A cluster of PRs around config tooling and session export safety indicates an ongoing effort to improve developer experience and data‑integrity guarantees. Overall, the project is **busy and responsive**, with many day‑of patches already in the review queue.

## 2. Releases

No new releases today. The latest stable release remains v0.19.0 (noted in related issues).

---

## 3. Project Progress

8 PRs were merged or closed in the last 24 hours. While the top‑20 PR list shows only open items, several notable fixes landed or are near landing:

- **Session export cascading deletion** – PR [#71123](https://github.com/NousResearch/hermes-agent/pull/71123) (open) would fix `hermes sessions export --delete-after-verified` so that delegate/subagent transcripts are exported and verified before cascade deletion.
- **Compression fallback** – PR [#71115](https://github.com/NousResearch/hermes-agent/pull/71115) (open) adds a `replace_messages` fallback when in‑place compaction fails, addressing issue [#71097](https://github.com/NousResearch/hermes-agent/issues/71097).
- **Gateway security** – PR [#71120](https://github.com/NousResearch/hermes-agent/pull/71120) (open) rejects path‑unsafe `session_id` values on `/v1/runs` to prevent Docker sandbox path injection.
- **Billing improvements** – PRs [#71128](https://github.com/NousResearch/hermes-agent/pull/71128) and [#71129](https://github.com/NousResearch/hermes-agent/pull/71129) (both open) persist `NULL` costs for unpriced models and expose `cost_status`/`cost_source` in the API.
- **Config CLI overhaul** – Three PRs by *Watergard* ([#71125](https://github.com/NousResearch/hermes-agent/pull/71125), [#71126](https://github.com/NousResearch/hermes-agent/pull/71126), [#71127](https://github.com/NousResearch/hermes-agent/pull/71127)) fix dotted‑key addressing, missing `model_routes`/`mcp_servers`/`plugins` in `config show`, and provide actionable hints when no editor is found.
- **Desktop image persistence** – PR [#71121](https://github.com/NousResearch/hermes-agent/pull/71121) (open) ensures attached images remain renderable across session switches and restarts.

These contributions show focused work on **data safety, configuration introspection, and Windows compatibility**.

---

## 4. Community Hot Topics

The most active discussions (by comment count) highlight three recurring themes:

### 🐛 Windows Encoding & Session Corruption
| Issue | Comments | Summary |
|-------|----------|---------|
| [#60144](https://github.com/NousResearch/hermes-agent/issues/60144) | 6 | Desktop boot fails when platform adapter import or MCP registration exceeds 15s timeout (CLOSED) |
| [#50210](https://github.com/NousResearch/hermes-agent/issues/50210) | 5 | Windows Smart App Control blocks unsigned `Hermes.exe` after signed bootstrap installer (CLOSED) |
| [#68474](https://github.com/NousResearch/hermes-agent/issues/68474) | 5 | `state.db` zeroed (95 MB of null bytes) during desktop update to v0.19.0 on Windows (CLOSED) |
| [#66473](https://github.com/NousResearch/hermes-agent/issues/66473) | 4 | Feature: MCP Smart Loading — lazy connection, tool budget, per‑session scoping (CLOSED) |
| [#71097](https://github.com/NousResearch/hermes-agent/issues/71097) | 1 (new) | Hygiene agent in‑place compression fails because `_last_compaction_in_place` not set (OPEN) |

The **state.db zeroed** issue (#68474) was particularly alarming for users, as it destroyed all session history. It was closed today with a fix (likely the compression fix in PR #71115). The **MCP Smart Loading** proposal (#66473) attracted broad interest as it addresses a fundamental performance bottleneck.

### 🔌 Gateway & Platform Reliability
- [#69230](https://github.com/NousResearch/hermes-agent/issues/69230) (3 comments) – Desktop app’s remote gateway reachability check fails despite the server being healthy (OPEN, needs‑repro).
- [#60313](https://github.com/NousResearch/hermes-agent/issues/60313) (1 comment) – Dual `config.yaml` sources (AppData vs. `~/.hermes`) cause confusing MCP OAuth behavior (OPEN).

### 📊 Insights & Billing
- [#71026](https://github.com/NousResearch/hermes-agent/issues/71026) (3 comments) – `/insights` crashes with `TypeError: unsupported operand type(s) for -: 'str' and 'int'` (OPEN). Likely caused by a field being a string instead of integer.
- [#71128](https://github.com/NousResearch/hermes-agent/pull/71128) – Fix for unpriced models storing `0` instead of `NULL` (open).

---

## 5. Bugs & Stability

### Critical & High Severity (P1–P2)
| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#68474](https://github.com/NousResearch/hermes-agent/issues/68474) | P1 | `state.db` zeroed on Windows update (CLOSED) | Yes (PR #71115) |
| [#50210](https://github.com/NousResearch/hermes-agent/issues/50210) | P1 | Windows unsigned exe blocked by Smart App Control (CLOSED) | Likely fixed in v0.19.0 |
| [#69559](https://github.com/NousResearch/hermes-agent/issues/69559) | P2 | Agent hangs after tool call completes, across 3 providers (CLOSED, needs‑repro) | Unknown |
| [#71097](https://github.com/NousResearch/hermes-agent/issues/71097) | P2 | Hygiene agent in‑place compression fails (OPEN) | PR #71115 open |
| [#71026](https://github.com/NousResearch/hermes-agent/issues/71026) | P3 | Insights crash on string vs. int subtraction (OPEN) | No |
| [#70586](https://github.com/NousResearch/hermes-agent/issues/70586) | P2 | Desktop session with `async_delegation_complete` messages fails to reopen (CLOSED) | Probably merged |

### Recurring Windows Encoding Bugs
Many issues (some CLOSED as duplicates) report `UnicodeDecodeError` when reading files on Windows with non‑UTF‑8 locales:
- [#10878](https://github.com/NousResearch/hermes-agent/issues/10878) – BOM not stripped from MEMORY.md (OPEN since April)
- [#68369](https://github.com/NousResearch/hermes-agent/issues/68369) – `hermes skills check` crashes on Chinese Windows (CLOSED)
- [#65123](https://github.com/NousResearch/hermes-agent/issues/65123) – UTF‑8 BOM in `.env` silently drops first key (CLOSED)
- [#51691](https://github.com/NousResearch/hermes-agent/issues/51691) – `skill_view` UTF‑8 decode error on Windows Desktop (CLOSED)

These indicate the project is actively cleaning up encoding pitfalls, but the root cause — use of `path.read_text()` without explicit `encoding` or `errors` parameter — persists in several older code paths.

### Gateway & Cron
- [#69230](https://github.com/NousResearch/hermes-agent/issues/69230) – Gateway reachability check false negative (OPEN, needs‑repro).
- [#42384](https://github.com/NousResearch/hermes-agent/issues/42384) – Cron stdout silently dropped on Windows when it contains emoji (OPEN).
- [#63586](https://github.com/NousResearch/hermes-agent/pull/63586) – PR fixing cron manual runs on gateway loop (open).

---

## 6. Feature Requests & Roadmap Signals

### High Community Interest
- **MCP Smart Loading** – [#66473](https://github.com/NousResearch/hermes-agent/issues/66473) (CLOSED) proposes lazy connections, tool budgets, and per‑session scoping. This is a significant performance and flexibility improvement that would reduce startup time and memory for users with many MCP servers.
- **Per‑session skill auto‑injection** – [#26709](https://github.com/NousResearch/hermes-agent/issues/26709) (OPEN) requests a config option to automatically inject a skill on every session start. Despite being filed in May, it has only 1 comment and no maintainer response.
- **Microsoft Agent Governance Toolkit** – [#69128](https://github.com/NousResearch/hermes-agent/issues/69128) (OPEN, needs‑decision) proposes an optional governance plugin to consolidate 53+ open governance issues. It received a 👍 from the community but no formal decision.

### Likely Next‑Version Predictions
- **Billing & session cost reporting** – PRs [#71128](https://github.com/NousResearch/hermes-agent/pull/71128) and [#71129](https://github.com/NousResearch/hermes-agent/pull/71129) are small, well‑scoped changes that will likely land in v0.20.
- **Config CLI improvements** – The three PRs by *Watergard* ([#71125–71127](https://github.com/NousResearch/hermes-agent/pulls?q=author:Watergard)) are user‑experience enhancements that are likely to be merged soon.
- **Hindsight relevance floor** – PR [#71122](https://github.com/NousResearch/hermes-agent/pull/71122) adds `recall_min_scores` to avoid injecting stale/irrelevant facts. This addresses a long‑standing Hindsight annoyance.

---

## 7. User Feedback Summary

| Pain Point | Evidence | Satisfaction Level |
|------------|----------|-------------------|
| **Windows encoding hell** – BOM, GBK, cp1252 break core features (memory, skills, env files) | Issues #10878, #68369, #65123, #51691, #42384 | Low — many duplicates, fixes slowly trickle in |
| **State database corruption** – `state.db` zeroed on update | #68474 (closed, but alarming) | Low, but quick fix |
| **MCP startup overhead** – all servers connected at startup | #66473 (proposal with 4 comments) | Medium demand for lazy loading |
| **Config confusion** – dual `config.yaml` sources | #60313 | Low, but confusing |
| **Desktop boot timeout** – 15s not enough with many MCP/adapters | #60144 (closed) | Medium — fixed with increased timeout? |
| **Agent hangs** – after tool calls, specific providers | #69559 (needs‑repro) | High severity, but isolated |
| **Insights crash** – string vs. int subtraction | #71026 | Medium — breaks billing reporting |
| **Billing lacks transparency** – cost_status not exposed | PR #71129 | Medium, being addressed |

Users are **generally satisfied** with the breadth of integrations and rapid bug fixes, but **Windows users continue to face disproportionate friction** due to encoding assumptions. The project’s active response to `state.db` zeroing (fix landed same day) demonstrates strong stability focus.

---

## 8. Backlog Watch

Several important issues have remained unanswered or have minimal maintainer attention for weeks or months:

| Issue | Created | Last Update | Age | Priority | Status |
|-------|---------|-------------|-----|----------|--------|
| [#10878](https://github.com/NousResearch/hermes-agent/issues/10878) – BOM in MEMORY.md | 2026-04-16 | 2026-07-25 | 3 months | P2 | OPEN (3 comments, no maintainer reply) |
| [#10879](https://github.com/NousResearch/hermes-agent/issues/10879) – Non‑UTF‑8 MEMORY.md raises uncaught error | 2026-04-16 | 2026-07-25 | 3 months | P2 | CLOSED (duplicate, but root fix unclear) |
| [#26709](https://github.com/NousResearch/hermes-agent/issues/26709) – Per‑session skill auto‑injection | 2026-05-16 | 2026-07-25 | 2 months | P3 | OPEN (1 comment, no assignee) |
| [#35266](https://github.com/NousResearch/hermes-agent/issues/35266) – `hermes status` missing ZAI_API_KEY detection | 2026-05-30 | 2026-07-25 | 2 months | P3 | OPEN (3 comments) |
| [#38414](https://github.com/NousResearch/hermes-agent/issues/38414) – install.sh doesn’t verify Node.js architecture after migration | 2026-06-03 | 2026-07-25 | 1.5 months | P2 | OPEN (2 comments) |
| [#47107](https://github.com/NousResearch/hermes-agent/issues/47107) – write_file blocks writing to `~/.hermes/.env` | 2026-06-16 | 2026-07-25 | 1 month | P2 | OPEN (2 comments) |
| [#69128](https://github.com/NousResearch/hermes-agent/issues/69128) – Governance toolkit integration | 2026-07-22 | 2026-07-25 | 3 days | P3 (needs‑decision) | OPEN (1 comment, no maintainer response) |

**Notable:** The BOM/encoding issues (#10878, #10879, #57754) have been reported multiple times and closed as duplicates without a systemic fix. The core memory tool (`memory_tool.py`) still uses `read_text()` without `errors=` parameter — a fact acknowledged in issue #57754 but not yet patched in the latest commits. This remains a **landmine for Windows users**.

Additionally, the **Dockerfile Podman incompatibility** (#62849) has been open since July 11 without maintainer comment, despite the fix being simple (use `--chmod` flag compatible with both Docker and Podman).

---

*Digest generated from GitHub data retrieved 2026-07-25. All links point to NousResearch/hermes-agent repository.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date:** 2026-07-25  
**Source:** GitHub (sipeed/picoclaw)

---

## Today’s Overview

PicoClaw saw moderate activity in the last 24 hours with three issues touched and eight pull requests processed. The project closed seven PRs – a mix of bug fixes, internationalisation contributions, and performance refactoring – while one new PR (#3293) was merged to resolve a reported CPU-spike bug. No new releases were published. Community engagement remained steady, with Chinese and English-language issues receiving attention, and the maintainers appear to be actively cleaning stale items (two issues closed as stale). Overall project health is solid, with responsiveness to both user-reported bugs and code quality improvements.

---

## Releases

None. No new releases were published today.

---

## Project Progress

**Merged/Closed PRs today (7 closed, 1 open):**

- [#3293](https://github.com/sipeed/picoclaw/pull/3293) **fix bug of input box on chat page** – Merged. Directly fixes the CPU‑high issue reported in #3292.  
- [#3261](https://github.com/sipeed/picoclaw/pull/3261) **Add zh-TW locale and Traditional Chinese translations** – Still open, last updated July 24. Adds Taiwanese terminology to WebUI and documentation.  
- [#3247](https://github.com/sipeed/picoclaw/pull/3247) **feat(i18n): add Czech translations for code wrap options** – Merged/closed. Fills missing translations for v0.3.1 keys.  
- [#3246](https://github.com/sipeed/picoclaw/pull/3246) **fix: security and robustness hardening (MQTT TLS, OAuth timeouts, bounded search reads)** – Merged. Important hardening: enables TLS certificate verification by default in MQTT, adds timeouts for OAuth, and bounds search reads.  
- [#3245](https://github.com/sipeed/picoclaw/pull/3245) **refactor(skills): single-pass escapeXML, drop no-op Sprintf** – Merged. Performance micro‑optimisation in `pkg/skills`.  
- [#3244](https://github.com/sipeed/picoclaw/pull/3244) **refactor(seahorse): cut allocations in summary XML assembly** – Merged. Allocation reduction via `strings.NewReplacer`.  
- [#3243](https://github.com/sipeed/picoclaw/pull/3243) **refactor(seahorse): use strings.Builder in compaction string helpers** – Merged. Replaces O(n²) string concatenation with O(n) `strings.Builder`.  
- [#323](https://github.com/sipeed/picoclaw/pull/323) **fix(discord): handle character limits and maintain typing status** – Merged/closed. Earlier PR (Feb) that appears to have been re‑evaluated and finally closed.

These PRs indicate a focused effort on performance, security, and internationalisation, with the maintainers actively reviewing and merging community contributions.

---

## Community Hot Topics

**Most active issues (by comment count, last 24h):**

- [#2796](https://github.com/sipeed/picoclaw/issues/2796) **[[stale] [BUG] 历史记录中，一次对话有多次用户消息，只能查看到最后一条用户消息，先前的都看不到]** – 7 comments. *Status:* Closed as stale. The user reported that conversation history shows only the last user message when multiple user messages exist in a single dialog. The expected behaviour is to display all user messages, as compression should only apply to the LLM context, not the history UI. This issue was opened in May but only closed today without a fix – a potential lingering UX problem.  

- [#3292](https://github.com/sipeed/picoclaw/issues/3292) **[[OPEN] [BUG] CPU usage too high when focus on input box in chat interface / 聊天界面输入框在选中时cpu占用高]** – 0 comments yet, but a fix PR (#3293) was created and merged within hours. This suggests the issue was quickly replicated and resolved.  

**Underlying needs:**  
The user base clearly values full visibility of conversation history (issue #2796) and low client‑side resource usage (#3292). The quick fix for CPU suggests the team prioritises performance regressions.

---

## Bugs & Stability

### Ranked by severity

1. **CPU spike on input focus** (#3292) – Severity: **High** (affects usability on any device). *Fix exists:* PR #3293 merged.  
2. **Conversation history truncation** (#2796, closed stale) – Severity: **Medium** (information loss in UI). No fix merged. Although closed, the underlying problem may resurface if users encounter it again.  
3. *(No other bugs reported today.)*

The rapid turnaround on the CPU bug demonstrates good maintenance hygiene. The history truncation issue, however, remains unresolved despite being filed two months ago – likely because it is a design‑level concern (message compression vs. UI rendering).

---

## Feature Requests & Roadmap Signals

- **Streaming output for QQ channel** ([#3201](https://github.com/sipeed/picoclaw/issues/3201), closed stale) – The user requested real‑time token‑by‑token output for QQ, similar to Telegram and Pico WebSocket. While closed, it signals demand for consistent streaming support across all channels. This could reappear in a future release if the maintainers prioritise channel parity.  
- **Traditional Chinese (zh‑TW) locale** ([#3261](https://github.com/sipeed/picoclaw/pull/3261), open) – A PR adding Taiwanese terminology is still pending. Given that several i18n PRs were merged today, this is likely to be reviewed and merged soon.  
- **Czech translations** ([#3247](https://github.com/sipeed/picoclaw/pull/3247)) – Already merged, indicating the project welcomes incremental locale improvements.

**Prediction for next version (v0.3.2 or v0.4.0):** Expect the zh‑TW locale to land, possibly alongside continued performance refinements (e.g., string‑handling optimisations). Streaming for QQ may be revisited if community interest persists.

---

## User Feedback Summary

- **Satisfaction signal:** The quick fix for the CPU bug shows that user reports are taken seriously and acted upon promptly.  
- **Dissatisfaction signal:** The unresolved history truncation issue (#2796) may frustrate users who rely on reviewing multi‑turn conversations. The failure to close it with a fix (only a stale closure) could indicate that the maintainers consider it a low priority or a difficult architectural change.  
- **Use case highlight:** A Debian/Linux user running the Web channel in Firefox explicitly reported the CPU issue, confirming that PicoClaw’s WebUI is actively used on desktop platforms.

---

## Backlog Watch

- **[#3261 – Add zh‑TW locale](https://github.com/sipeed/picoclaw/pull/3261)** – Open since July 16 (9 days). No reviewer activity since July 24. While not extremely old, it is the only open PR that appears ready for merge. The maintainers may be awaiting final review or testing.  
- **[#2796 – History truncation bug](https://github.com/sipeed/picoclaw/issues/2796)** – Closed as stale without a fix. If the project database is still searchable, this issue could be reopened if similar reports emerge. Maintainers should consider labelling it as “needs design decision” to track it for future planning.  
- No other long‑unanswered items are apparent in the last 24‑hour data window. The project appears to have cleared its backlog effectively during this period.

---

*Generated from GitHub activity for sipeed/picoclaw on 2026-07-25.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-25

## Today's Overview
The project saw no new issues filed or resolved in the last 24 hours, indicating a quiet day in terms of bug reporting and user feedback. Pull request activity remains steady with 7 PRs updated, though only one was closed (and that was an erroneous submission). The six open PRs all carry the `core-team` or `follows-guidelines` labels, signalling focused internal work on stability and configurability. No releases were published, so the latest stable version remains unchanged. Overall, the project appears to be in a consolidation phase with several important fixes in review.

## Releases
*None this period.* No new versions were published. The latest release (if any) remains as previously documented.

## Project Progress
- **Merged/closed PRs**: Only **PR #3123** was closed, with the note *“Pacific changes. Wrong PR.”* — this was a mistaken submission and contains no meaningful changes.
- **Active fixes in review**: Five fix-oriented PRs are open and being updated:
  - `fix(agent-runner): never deliver silence when a nudged chat turn stays bare` ([#3126](https://github.com/nanocoai/nanoclaw/pull/3126))
  - `fix(opencode): main compatibility, custom-endpoint transport, memory parity` ([#3122](https://github.com/nanocoai/nanoclaw/pull/3122))
  - `fix(chat): keep typing active for processing turns` ([#3093](https://github.com/nanocoai/nanoclaw/pull/3093))
  - `fix: report unavailable MCP servers` ([#3124](https://github.com/nanocoai/nanoclaw/pull/3124))
  - `fix(templates): prepend all top-level context Markdown` ([#3090](https://github.com/nanocoai/nanoclaw/pull/3090))
- **New feature**: `feat: per-agent-group timezone override` ([#3125](https://github.com/nanocoai/nanoclaw/pull/3125)) adds IANA timezone support per agent group, including database migration and CLI commands.

## Community Hot Topics
No issues or PRs received reactions or comments beyond author updates. The most discussed items (by virtue of being updated most recently) are:

- **PR #3126** (`fix(agent-runner)`) — addresses a potentially frustrating UX issue where a nudged chat turn could produce silence. This is the newest PR and likely to draw attention from users relying on agent-runner.
- **PR #3125** (`feat: per-agent-group timezone`) — a new configuration capability that several multi-group deployments may have been lacking.
- **PR #3122** (`fix(opencode)`) — a compatibility fix for custom endpoints and memory parity, important for users integrating external AI providers.

All PRs have zero comments or reactions, indicating that the contributor base is small and discussions may happen off-GitHub (e.g., chat or internal meetings). Maintainers should consider encouraging more public discussion to increase community involvement.

## Bugs & Stability
No new bugs were reported as issues. However, the five open fix PRs target stability improvements:

| PR | Area | Severity Estimate | Fix Available? |
|----|------|-------------------|----------------|
| [#3126](https://github.com/nanocoai/nanoclaw/pull/3126) | agent-runner: silence on nudged turns | Medium (user-facing, could lose responses) | Yes, in review |
| [#3122](https://github.com/nanocoai/nanoclaw/pull/3122) | opencode: compatibility & memory | Medium (integration breakage) | Yes, in review |
| [#3093](https://github.com/nanocoai/nanoclaw/pull/3093) | chat: typing indicator during processing | Low (cosmetic/UX) | Yes, in review |
| [#3124](https://github.com/nanocoai/nanoclaw/pull/3124) | MCP server availability reporting | Low (affects diagnostics) | Yes, in review |
| [#3090](https://github.com/nanocoai/nanoclaw/pull/3090) | templates: context Markdown ordering | Medium (could affect prompt quality) | Yes, in review |

No regressions or crashes were reported. The project’s bug landscape is dominated by these incremental fixes.

## Feature Requests & Roadmap Signals
- **Per-agent-group timezone override** ([#3125](https://github.com/nanocoai/nanoclaw/pull/3125)) is the most concrete new feature in flight. It suggests product direction towards better multi-tenant/group configuration.
- The `fix(opencode)` PR ([#3122](https://github.com/nanocoai/nanoclaw/pull/3122)) implies continued investment in `opencode` compatibility, likely to support custom endpoints — a signal that the project values integration flexibility.
- No feature requests were filed as issues, so community demand is inferred from the PRs themselves. Likely to appear in the next minor release: timezone overrides, opencode memory parity, and the agent-runner silence fix.

## User Feedback Summary
No direct user feedback (issues, comments, reactions) was recorded in the last 24 hours. From the PR descriptions, we can infer pain points:
- Users of nudged chat turns occasionally experience dropped responses (silence) — addressed by [#3126](https://github.com/nanocoai/nanoclaw/pull/3126).
- `opencode` integration users may have faced compatibility issues with custom endpoints and missing memory — addressed by [#3122](https://github.com/nanocoai/nanoclaw/pull/3122).
- Chat users may have noticed a lag where typing indicator stops while processing — addressed by [#3093](https://github.com/nanocoai/nanoclaw/pull/3093).

Satisfaction appears neutral; no complaints or praises were publicly voiced.

## Backlog Watch
- **No stale issues** — the issue tracker is empty of open items. This is unusual for a project of NanoClaw’s size and suggests either a very responsive maintenance team or that issues are managed externally.
- **Open PRs to watch**: All six open PRs have been updated within the last 24 hours, so none are lingering. However, PR [#3090](https://github.com/nanocoai/nanoclaw/pull/3090) and [#3093](https://github.com/nanocoai/nanoclaw/pull/3093) have been open since July 19 — they are approaching a week old. Maintainers should ensure they receive review priority to avoid growing stale.

**Maintainer action item**: Consider tagging PRs that need discussion or are blocked. The lack of issue/PR comments may indicate a need to lower the bar for community participation.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-07-25

## 1. Today's Overview

IronClaw enters a high-activity phase as the team pushes toward a v1.0 release candidate. In the past 24 hours, 32 issues were updated (26 open, 6 closed) and 50 pull requests were touched (31 open, 19 merged/closed). No new releases were published. The majority of activity centres on **v1-launch-checklist** tasks, a structured **bug bash** (severity P1/P2), and long-running architectural epics (error recoverability, skill discovery, Hermetic testing, extension host refactoring). The project shows strong contributor momentum but also reveals critical user-facing defects in Slack and Telegram integrations that will need immediate attention before a final v1 release.

## 2. Releases

**None** – no new tags or published versions in the last 24 hours. The latest releases remain those from previous weeks (e.g., pre-reborn and RC versions). The team is actively resolving blockers to ship v1.0.0.

## 3. Project Progress

**Merged/Closed PRs (19 total in last 24h):**  
The following key PRs were merged or closed:

- [#6664 – test(e2e): count capability coverage per outcome, not per capability](https://github.com/nearai/ironclaw/pull/6664)  
  Fixes a false-positive in coverage reporting: a capability was considered “tested” if any harvested trace emitted a `tool_calls` entry with that name, even if the model never actually invoked it. Now tracks outcomes to ensure genuine exercised coverage.

- [#6663 – Default cargo run to WebUI serve](https://github.com/nearai/ironclaw/pull/6663)  
  Makes `cargo run` in the workspace launch the shipping Reborn CLI and defaults to `ironclaw serve` while preserving existing auth checks. Also adds a fallback for WebUI build script to pinned `pnpm@11.7.0`.

- [#6637 – Document Reborn storage landscape and target relational model](https://github.com/nearai/ironclaw/pull/6637)  
  Provides an inventory of current persistence authorities (filesystem-backed, relational, local-file, append-log, legacy) and proposes a hybrid target model with normalized control-plane tables and ER diagrams.

- [#6656 – Disable upgrade for version before v1.0.0](https://github.com/nearai/ironclaw/issues/6656) (closed)  
- [#6521 – ironclaw CLI not available on agent staging](https://github.com/nearai/ironclaw/issues/6521) (closed)  
- [#6614 – Slack personal OAuth binding stays unresolved](https://github.com/nearai/ironclaw/issues/6614) (closed)  
- [#6482 – Epic: Pluggable Memory Providers](https://github.com/nearai/ironclaw/issues/6482) (closed)  
- [#6490 – Define Manifest V3 contract, compatibility, and migration](https://github.com/nearai/ironclaw/issues/6490) (closed)  

These closures reflect progress on the v1 launch checklist, memory architecture, and manifest schemas. No major feature PRs were merged today; the focus was on bug fixes, documentation, and testing infrastructure.

## 4. Community Hot Topics

Most active issues by comment count:

- **#6284 – [EPIC] error-recoverability endgame** (5 comments)  
  [Issue link](https://github.com/nearai/ironclaw/issues/6284)  
  Defines the rigorous contract that every mid-run error must be recoverable: the run survives, the model sees the cause and a corrective action, and the system never reports a non-success to the user. This epic touches the core agent loop and is central to reliability guarantees.

- **#6544 – No UI or CLI to configure IRONCLAW_REBORN_SLACK_PERSONAL_OAUTH_REDIRECT_URI** (4 comments)  
  [Issue link](https://github.com/nearai/ironclaw/issues/6544) (CLOSED)  
  Revealed that the Slack OAuth redirect URI cannot be persisted via the UI or CLI, causing 503 errors. This was a critical blocker for hosted environments, now resolved.

- **#6524 – Epic: Hermetic capability and journey testing platform** (3 comments)  
  [Issue link](https://github.com/nearai/ironclaw/issues/6524)  
  Addresses the mechanical gap of deterministic, meaningful coverage for every capability and critical user journey. The platform aims to combine recorded fixtures, Emulate work, and new hermetic test runners.

- **#6565 – Epic: Reliable Skill Discovery, Routing, and Activation** (0 comments, but high visibility)  
  [Issue link](https://github.com/nearai/ironclaw/issues/6565)  
  Updated today with a corrected diagnosis: the `TurnCoordinator` path does not run the keyword/regex auto-activation pipeline, and the absence of skill discovery leads to silent failures. This epic is now the top priority for skill reliability.

**Underlying needs:** The community (primarily the core team) is demanding ironclad reliability for error handling, Slack integration, skill routing, and testing coverage before declaring v1 stable. The bug bash results are surfacing real integration pain points.

## 5. Bugs & Stability

Today’s bug bash (tagged `bug_bash_P1` and `bug_bash_P2`) has revealed several critical defects:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **P1** | [#6645 – Slack send_message reports success but DM never delivered](https://github.com/nearai/ironclaw/issues/6645) | Tool reports success but outbound delivery never reaches the user. | No specific fix PR yet. |
| **P1** | [#6644 – Telegram replies delivered to wrong user message](https://github.com/nearai/ironclaw/issues/6644) | Telegram bot responses are associated with incorrect user prompts. | No fix PR yet. |
| **P1** | [#6643 – Telegram messages accepted but never processed after pairing](https://github.com/nearai/ironclaw/issues/6643) | Post-pairing messages go into a void. | No fix PR yet. |
| **P2** | [#6650 – Agent fabricates AQI data from mixed/cached web sources](https://github.com/nearai/ironclaw/issues/6650) | Reports AQI 199 for Connecticut from no live source. | None. |
| **P2** | [#6649 – Tool activity panel appears after assistant response instead of during execution](https://github.com/nearai/ironclaw/issues/6649) | UI timing defect. | None. |
| **P2** | [#6648 – Tool failure messages are duplicated and inconsistent](https://github.com/nearai/ironclaw/issues/6648) | Two nearly identical error messages. | None. |
| **P2** | [#6646 – Agent ignores Google Sheets action, reports only email results](https://github.com/nearai/ironclaw/issues/6646) | After 26 tool calls, never writes to sheet. | None. |
| – | [#6651 – Agent repeats question text after responding](https://github.com/nearai/ironclaw/issues/6651) | UI duplication. | None. |
| – | [#6642 – ironclaw models list shows stale provider/model after TUI switch](https://github.com/nearai/ironclaw/issues/6642) | Config.toml updated, but CLI reads old defaults. | None. |
| – | [#6623 – Chat failure messages ignore selected application language](https://github.com/nearai/ironclaw/issues/6623) | Hard-coded English. | None. |
| – | [#6622 – Completed automation filtering flashes a full loading skeleton](https://github.com/nearai/ironclaw/issues/6622) | UX flash. | None. |
| – | [#6621 – Extension configuration modal does not trap or restore keyboard focus](https://github.com/nearai/ironclaw/issues/6621) | Accessibility violation. | None. |

**Stability assessment:** The Slack and Telegram channels are the most fragile, with P1 bugs indicating broken deliverability and message routing. Data fabrication (AQI) is a serious trust issue. The large number of P2 UI/UX bugs suggests the WebUI needs polishing. No fix PRs have yet been opened for today’s bugs, though related infrastructure (OAuth config fix, extension host refactoring) is in progress.

## 6. Feature Requests & Roadmap Signals

**Explicit feature requests captured today:**

- **Skill Self-Creation** – [#6641](https://github.com/nearai/ironclaw/issues/6641) proposes a design doc for an agent that distills learned knowledge into reusable skills without human intervention, with runtime discovery and hot-swapping.
- **WebUI Performance Enhancements** – [#6628](https://github.com/nearai/ironclaw/issues/6628) (epic) plus three sub-issues: route-level code splitting [#6629](https://github.com/nearai/ironclaw/issues/6629), static asset compression/caching [#6630](https://github.com/nearai/ironclaw/issues/6630), and chat markdown/streaming render optimization [#6631](https://github.com/nearai/ironclaw/issues/6631).
- **Docker image CI restoration** – [#6635](https://github.com/nearai/ironclaw/issues/6635).
- **Hermetic testing platform** (epic #6524) and **Reliable Skill Discovery** (epic #6565) continue as long-running roadmaps.

**Predictions:** Based on the v1-launch-checklist urgency and the number of bug bash issues, the next RC (v1.0.0-rc.9 or final) will likely include:
- Fixes for Slack/Telegram delivery (merged PRs #6531 and possibly new ones).
- Completion of the extension host refactoring (PR #6616) and filesystem-backed extension state normalization (PR #6655).
- Improved error diagnostics (PR #6665) and termination warnings (PR #6530).
- Improved WebUI bundle size (epic #6628) – may be deferred to post-v1.

## 7. User Feedback Summary

**Real pain points from today’s bug reports:**

- **Slack integration broken:** Users cannot receive DMs despite successful tool calls – a showstopper for any team relying on Slack notifications.
- **Telegram unreliability:** Messages are not associated with the correct user, and messages after pairing are silently dropped – makes the chatbot practically unusable on Telegram.
- **Data fabrication:** The agent invented AQI values from mixed/cached sources, undermining trust in agent output.
- **UI confusion:** Duplicated question text, delayed tool activity panel, and inconsistent error messages degrade the user experience.
- **Configuration state mismatch:** Swapping LLM providers via TUI does not reflect in CLI queries – forces manual database editing.
- **Localization gaps:** Chat failure messages are hard-coded in English, breaking non-English workflows.
- **Accessibility violation:** Modal focus management missing, excluding keyboard-only users.

**Satisfaction signals:** None noted – the bug bash is explicitly surfacing dissatisfaction. The team is responsive (many issues filed today by QA members), but no fix PRs have landed yet.

## 8. Backlog Watch

**Long-unanswered important items needing maintainer attention:**

| Item | Created | Last Updated | Comments | Notes |
|------|---------|--------------|----------|-------|
| [#4058 – KMS curve-capability fail-closed on custodial-mainnet ship-gate](https://github.com/nearai/ironclaw/pull/4058) | 2026-05-25 | 2026-07-24 | 0 | Huge XL PR for signing hardening; open for two months with no merge activity. |
| [#4060 – fix(signing): continuation asserts caller scope/run/gate_ref](https://github.com/nearai/ironclaw/pull/4060) | 2026-05-25 | 2026-07-24 | 0 | Companion PR to #4058; also stalled. |
| [#4104 – grant expiry + binding tenant-key + retryable consistency](https://github.com/nearai/ironclaw/pull/4104) | 2026-05-27 | 2026-07-24 | 0 | Deferred trait-level durable-store follow-up. |
| [#4055 – TrustEnrollment ceremony + connected-wallet trust registration](https://github.com/nearai/ironclaw/pull/4055) | 2026-05-25 | 2026-07-24 | 0 | Another stalwart signing PR. |
| [#4054 – test(signing): multi-tenant operating model + isolation tests](https://github.com/nearai/ironclaw/pull/4054) | 2026-05-25 | 2026-07-24 | 0 | Test coverage for signing isolation. |
| [#5598 – chore: release](https://github.com/nearai/ironcl

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-07-25

## 1. Today's Overview
The project shows **high development velocity** with **43 pull requests merged or closed** in the last 24 hours, offsetting a backlog of **19 open issues** (all stale, none newly filed). The latest release (2026.7.23) introduced AI skin creation flow, multi‑annotation attachments, and new build entry points. While no new issues were opened, the community continues to react to long‑standing problems — especially DeepSeek V4 incompatibility, IM integration gaps, and UI quality concerns. The maintainer team is actively closing PRs (security, cowork, build) but a cluster of critical security fixes remain unmerged.

## 2. Releases
**New version: LobsterAI 2026.7.23**  
- `feat(skin): improve AI skin creation flow` — PR [#2361](https://github.com/netease-youdao/LobsterAI/pull/2361)  
- `feat(cowork): 支持浏览器多注释附件` — PR [#2366](https://github.com/netease-youdao/LobsterAI/pull/2366)  
- `feat(build): add explicit channel entry points for Wind`  
No breaking changes or migration notes provided. The release focuses on UI improvements and Windows build compatibility.

## 3. Project Progress
**Merged/closed PR highlights** (43 total, top items):  
- **Cowork reliability**  
  - [#2382](https://github.com/netease-youdao/LobsterAI/pull/2382) – Better model timeout handling (330s server timeout, local long‑wait hint after 30s)  
  - [#2299](https://github.com/netease-youdao/LobsterAI/pull/2299) – Sync subagent child tool history  
  - [#2264](https://github.com/netease-youdao/LobsterAI/pull/2264) – Large session rendering optimisations + diagnostics ZIP export  
- **Scheduled tasks**  
  - [#2306](https://github.com/netease-youdao/LobsterAI/pull/2306), [#2231](https://github.com/netease-youdao/LobsterAI/pull/2231), [#2314](https://github.com/netease-youdao/LobsterAI/pull/2314) – Fixed IM group routing, gateway‑backed run history, and ID casing preservation  
- **Build & platform**  
  - [#2327](https://github.com/netease-youdao/LobsterAI/pull/2327) – Windows binary signing via internal Youdao service  
  - [#2326](https://github.com/netease-youdao/LobsterAI/pull/2326) – Self‑healing installer for interrupted `win-resources.tar` extraction  
  - [#2328](https://github.com/netease-youdao/LobsterAI/pull/2328) – Serialised browser launch/search to prevent Chrome leaks  
- **Open PRs of note**  
  - [#2381](https://github.com/netease-youdao/LobsterAI/pull/2381) – Support Kimi K3 model  
  - [#2193](https://github.com/netease-youdao/LobsterAI/pull/2193) – Add LiteLLM as AI gateway provider  

## 4. Community Hot Topics  
*(Links to top‑comment issues)*

| Issue | Comments | Summary | Need |
|-------|----------|---------|------|
| [#1813](https://github.com/netease-youdao/LobsterAI/issues/1813) – DeepSeek V4 | 7 | `LLM request failed: provider rejected the request schema` | Model provider compatibility |
| [#1849](https://github.com/netease-youdao/LobsterAI/issues/1849) – Infinite NO_REPLY | 3 | Task completes prematurely while model still outputting | Response streaming reliability |
| [#1878](https://github.com/netease-youdao/LobsterAI/issues/1878) – WeChat IM verification | 3 | No UI input for 2FA code during WeChat scan | IM integration completeness |
| [#1796](https://github.com/netease-youdao/LobsterAI/issues/1796) – Write tool fails | 2 | Write/Edit tools always fail after recent updates | Core tool reliability |

**Underlying need**: Users are heavily dependent on external LLM providers (DeepSeek, Alibaba Qwen) and IM channels (WeChat, DingTalk); any compatibility break or missing UI flow immediately blocks core workflows.

## 5. Bugs & Stability  
Ranked by severity (High → Low):

| Severity | Bug | Issue / Fix PR | Status |
|----------|-----|----------------|--------|
| 🔴 High | DeepSeek V4 schema rejection | [#1813](https://github.com/netease-youdao/LobsterAI/issues/1813) | No fix PR yet |
| 🔴 High | AI engine connection lost (desktop app) | [#1993](https://github.com/netease-youdao/LobsterAI/issues/1993) | No fix PR |
| 🔴 High | Email path traversal (CWE‑22) | [#1885](https://github.com/netease-youdao/LobsterAI/issues/1885) | No fix merged; see [#1831](https://github.com/netease-youdao/LobsterAI/pull/1831) for related security |
| 🟡 Medium | IM infinite NO_REPLY | [#1849](https://github.com/netease-youdao/LobsterAI/issues/1849) | Partial fix in [#2382](https://github.com/netease-youdao/LobsterAI/pull/2382) (timeout handling) |
| 🟡 Medium | Model forcing to NetEase backend | [#1988](https://github.com/netease-youdao/LobsterAI/issues/1988) | No fix PR |
| 🟢 Low | Cowork blank loading state | [#1920](https://github.com/netease-youdao/LobsterAI/issues/1920) | No fix PR |
| 🟢 Low | Session scroll anomaly with long Mermaid | [#1971](https://github.com/netease-youdao/LobsterAI/issues/1971) | No fix PR |

Multiple security‑fix PRs ([#1831](https://github.com/netease-youdao/LobsterAI/pull/1831), [#1832](https://github.com/netease-youdao/LobsterAI/pull/1832), [#1833](https://github.com/netease-youdao/LobsterAI/pull/1833)) remain open since April – a notable gap in addressing reported vulnerabilities.

## 6. Feature Requests & Roadmap Signals  
**User‑requested features** (from issues):  
- Hermes Agent integration (like Open WebUI) – [#1880](https://github.com/netease-youdao/LobsterAI/issues/1880)  
- OpenHuman engine support – [#2016](https://github.com/netease-youdao/LobsterAI/issues/2016)  
- Batch conversation deletion – [#1797](https://github.com/netease-youdao/LobsterAI/issues/1797)  
- UI/UX redesign – [#1836](https://github.com/netease-youdao/LobsterAI/issues/1836)  

**Roadmap signals from PRs** (likely candidates for next release):  
- **LiteLLM provider** ([#2193](https://github.com/netease-youdao/LobsterAI/pull/2193)) – would enable one‑click proxy to 100+ models, directly addressing the “model forcing” complaints.  
- **Kimi K3 support** ([#2381](https://github.com/netease-youdao/LobsterAI/pull/2381)) – expanding model choice.  
- **Advanced memory system** – hinted by discussions in [#2039](https://github.com/netease-youdao/LobsterAI/issues/2039) and [#2040](https://github.com/netease-youdao/LobsterAI/issues/2040) (Dreaming bug, memory schema improvements).  

## 7. User Feedback Summary  
**Pain Points**  
- **Model provider lock‑in** – Several users report that after updates, external models (Qwen3.6‑plus, DeepSeek V4) fail, and the app forces NetEase backends without clear configuration control ([#1988](https://github.com/netease-youdao/LobsterAI/issues/1988), [#1813](https://github.com/netease-youdao/LobsterAI/issues/1813)).  
- **Desktop reliability** – “AI engine connection lost” error on the desktop app but stable on IM bots ([#1993](https://github.com/netease-youdao/LobsterAI/issues/1993)).  
- **Local deployment friction** – Build prerequisites not automatically satisfied, causing login failures ([#2017](https://github.com/netease-youdao/LobsterAI/issues/2017)).  
- **UI polish** – “Ugly compared to competitors” ([#1836](https://github.com/netease-youdao/LobsterAI/issues/1836)), blank loading states ([#1920](https://github.com/netease-youdao/LobsterAI/issues/1920)).  

**Satisfaction signals**  
- Active PR merging shows maintainers are addressing cowork reliability and build stability.  
- Users are contributing detailed security analyses and feature PRs (e.g., LiteLLM, security patches).  

## 8. Backlog Watch  
Issues and PRs that have been open for an extended period (≥3 months) and lack recent maintainer engagement:

| Item | Opened | Last activity | Maintainer response? | Risk |
|------|--------|---------------|----------------------|------|
| [#1796](https://github.com/netease-youdao/LobsterAI/issues/1796) – Write tool fails | 2026‑04‑22 | 2026‑07‑24 (comment) | No official reply | High – blocks writing skill |
| [#1797](https://github.com/netease-youdao/LobsterAI/issues/1797) – Batch delete conversations | 2026‑04‑23 | 2026‑07‑24 | None | Low – feature request |
| [#1836](https://github.com/netease-youdao/LobsterAI/issues/1836) – UI redesign | 2026‑04‑27 | 2026‑07‑24 | None | Medium – user retention |
| [#1885](https://github.com/netease-youdao/LobsterAI/issues/1885) – Email path traversal | 2026‑05‑06 | 2026‑07‑24 | No fix merged; security PRs still open | **Critical** – vulnerability |
| [#1920](https://github.com/netease-youdao/LobsterAI/issues/1920) – Blank loading state | 2026‑05‑08 | 2026‑07‑24 | None | Low – UX |
| Security PRs [#1831](https://github.com/netease-youdao/LobsterAI/pull/1831)‑[#1835](https://github.com/netease-youdao/LobsterAI/pull/1835) | 2026‑04‑27 | 2026‑07‑24 | Maintainer pinged? | **Critical** – unmerged despite clear vulnerability |

**Maintainer attention needed**: The three security PRs (log sanitisation, IPC access control, scheme whitelist) were submitted three months ago. They address active CWE classes (path traversal, token leakage, open redirect). Their continued open state, together with the reported path traversal bug ([#1885](https://github.com/netease-youdao/LobsterAI/issues/1885)), creates a significant security risk for users.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest – 2026-07-25**

---

### 1. Today’s Overview
The project is in a low‑activity window. No new issues or releases were created in the last 24 hours, and no pull requests were merged or closed. Activity is concentrated on two open PRs focused exclusively on Slack integration enhancements, both authored by **penso** and updated today. The lack of issue churn or user feedback may indicate that contributors are concentrated on feature development rather than triaging community reports. Overall project health appears stable, with incremental feature work underway.

---

### 2. Releases
*No new releases today. Latest release remains unchanged.*

---

### 3. Project Progress
**No pull requests were merged or closed today.**  
Two open PRs are actively being refined:

- **PR #1165** – [feat(slack): acknowledge messages with reactions and add reaction triggers](https://github.com/moltis-org/moltis/pull/1165)  
  Adds Slack acknowledgment reactions (giving users a visual signal that a message was received) and inbound reaction triggers. Fixes a confirmed bug where threaded replies were sent to the wrong message.

- **PR #1166** – [feat(slack): phase reactions, reconnect supervision, Block Kit, and a premature-ack bugfix](https://github.com/moltis-org/moltis/pull/1166)  
  A stacked follow‑up to #1165 implementing eight additional Slack improvements. Includes a fix for a premature‑acknowledgment race condition (agent run returns immediately, but acknowledgment is sent too early) and introduces reconnect supervision logic and Block Kit support.

Together these PRs represent a concerted effort to close the feature gap with other Slack‑based agent frameworks (e.g., Hermes).

---

### 4. Community Hot Topics
**No issues or PRs received comments or reactions today.**  
The two open PRs have no recorded discussion or sponsor engagement. This likely reflects the PRs being very recent (created yesterday) and still under author review. No community‑driven threads were active.

---

### 5. Bugs & Stability
One confirmed bug is fixed in the current open PRs:

- **Wrong‑message bug in threaded replies** (fixed in #1165) – Affected users when Slack threads were used; the bot could respond to the wrong parent message.  
  *Severity: Medium* – Could cause confusing or incorrect responses in threaded conversations.  

- **Premature‑acknowledgment race condition** (fixed in #1166) – The `chat.send` function returned immediately, causing the “ack” reaction to appear before the agent actually processed the request.  
  *Severity: Low/Medium* – Misleading user feedback; breaks the trust that the bot has started working.

Both fixes are contained within the open PRs and have not yet been merged. No other stability issues reported.

---

### 6. Feature Requests & Roadmap Signals
The two Slack PRs are the clearest roadmap signal. Features requested (and implemented) today include:

- Acknowledgment reactions (emoji on user messages)
- Inbound reaction triggers (user reacts to bot messages)
- Reconnect supervision (automatic reconnection to Slack)
- Block Kit support (rich interactive UI components)
- Several internal improvements from the Hermes comparison

No new external feature requests were filed in the last 24 hours. Given the concentrated work on Slack, the next minor release will almost certainly include these integration improvements. No indication of deeper architectural changes.

---

### 7. User Feedback Summary
*No direct user feedback or support tickets were recorded today.*  
The PR descriptions implicitly capture pain points:

- Slack bot users had no typing indicator and no signal that their message was received → frustration  
- Threaded replies occasionally went to the wrong message → confusion  
- Acknowledgment arrived before processing started → false sense of completion  

These represent real user‑experience issues that the project is actively addressing.

---

### 8. Backlog Watch
**No long‑unanswered issues or PRs identified.**  
All open items are recent (created yesterday). No stale issues or pull requests appear in the data. The project maintains a clean backlog at this time.

---

*Generated from GitHub data for moltis-org/moltis on 2026-07-25 24h window.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-25

## Today's Overview

CoPaw (QwenPaw) is in an active development phase, with **50 issues** and **37 pull requests** updated in the last 24 hours, and **2 new releases** published. The project shows a healthy ratio of merged/closed PRs (14 out of 37) and a slightly higher share of open issues (28 open vs. 22 closed), indicating sustained community engagement. Today’s release of **v2.0.1** introduces the PawApp mini-app platform with a Kanban board, while a companion beta patch focuses on performance and stability. Several critical bugs around MCP tool registration, agent context handling, and performance regressions are under active discussion, and a wave of feature requests from a dedicated user suggests strong demand for UX and capability enhancements.

## Releases

### v2.0.1 (2026-07-25)
[View release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.1)

**What’s New**
- **PawApp Platform**: A new mini-app SDK that enables plugins to build rich interactive UIs inside QwenPaw. Ships with a built-in **Kanban task board** for project management.
- No breaking changes or migration notes were documented in the release notes.

### v2.0.1-beta.3 (2026-07-25)
[View release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.1-beta.3)

**Changes**
- Performance fix: stabilized chat options memo and reduced SSE re-parsing.
- Version bump and date update.

---

## Project Progress

Today **14 PRs** were merged or closed. Notable advances include:

- **History/Context durability** – PR [#6323](https://github.com/agentscope-ai/QwenPaw/pull/6323) (merged) redesigned Scroll context management around staged compaction and durable task continuity, making `history.db` the source of truth.
- **Zalo Bot Channel** – PR [#6118](https://github.com/agentscope-ai/QwenPaw/pull/6118) (merged) added a long-polling Zalo Bot channel, expanding messaging integration.
- **Tool batch control flow** – PR [#5698](https://github.com/agentscope-ai/QwenPaw/pull/5698) (merged) adapted the `run_tool_batch` tool for AgentScope 2.0 with control-flow primitives.
- **Plugin install authentication fix** – PR [#6428](https://github.com/agentscope-ai/QwenPaw/pull/6428) closed a security gap by requiring auth for plugin operations even on localhost.
- **Local model tool call parsing** – PR [#6409](https://github.com/agentscope-ai/QwenPaw/pull/6409) fixed `AttributeError` when tool call JSON is a non-object (e.g. array).
- **Gemini schema sanitization** – PR [#6410](https://github.com/agentscope-ai/QwenPaw/pull/6410) patched nullable schema handling for Gemini.
- **Windows PowerShell multiline** – PR [#6412](https://github.com/agentscope-ai/QwenPaw/pull/6412) preserved newlines in PowerShell commands.
- **Many feature requests closed for review** – A series of issues by user **Hazemaan** (e.g. #6441–#6451) were closed with a “Close-and-review-later” label, signaling maintainer triage.

Several large PRs remain open and under review, including the **QwenPaw Creator app** (#6284), **unified browser SDK** (#6276), **reranker support** (#5692), and **third-party agent integrations** (#6397).

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) – v2.0.0 Missing features: SSH Offline, Profiles returning 404** (7 comments)
   - Long-standing migration complaint. User reports critical features from v1.1.12 are completely inaccessible in v2.0.0.

2. **[#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) – v2.0 introduces ~2s fixed overhead per reply** (7 comments)
   - Performance regression after upgrade; overhead is independent of model latency.

3. **[#6258](https://github.com/agentscope-ai/QwenPaw/issues/6258) – openai model max output token not working** (3 comments)
   - Chinese user reports that `max_tokens` setting is ignored.

4. **[#2999](https://github.com/agentscope-ai/QwenPaw/issues/2999) – Repeated MCP client registration leads to task cancellation** (3 comments)
   - Open since April; each request reconnects to MCP servers, causing `CancelledError`.

5. **[#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) – MCP tool always shows "Tool not found"** (3 comments)
   - Docker user encountering tool name mismatch after v2.0 upgrade.

6. **[#6401](https://github.com/agentscope-ai/QwenPaw/issues/6401) – Cron task reusing session overwrites history** (3 comments, closed)
   - Bug confirmed: scheduled tasks with `share_session: true` wipe existing conversation history.

### Most Active PRs (by comment count)
- PRs are mostly developer-reviewed with few comments; several open PRs (e.g. #6459, #6323, #6284) are under active review but not heavily discussed in comments.

**Underlying needs**: Users are feeling pain from v2.0 migration (missing features, performance regression), MCP reliability issues, and lack of data integrity in scheduled tasks. The community is also requesting richer interaction patterns (undo, isolation, token stats).

---

## Bugs & Stability

### High Severity
- **[#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) – Performance regression (~2s overhead per reply)**
  - Critical for user experience. No fix PR identified yet.
- **[#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) – Missing features in v2.0.0 (SSH Offline, Profiles)**
  - Major migration blocker. No fix PR.
- **[#6401](https://github.com/agentscope-ai/QwenPaw/issues/6401) – Cron task overwrites session history (CLOSED)**
  - Confirmed bug; closure status suggests fix may be in progress or accepted.

### Medium Severity
- **[#6407](https://github.com/agentscope-ai/QwenPaw/issues/6407) – ReAct Agent tool_result mixed into assistant message causes 400 error**
  - Clear reproduction; OpenAI-compatible APIs fail. No fix PR yet.
- **[#6258](https://github.com/agentscope-ai/QwenPaw/issues/6258) – OpenAI max_tokens not honored**
  - Configuration setting silently ignored.
- **[#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) – MCP tool not found after upgrade**
  - Naming issue with `[mcp-key]__[tool_name]`.

### Low Severity / New
- **[#6460](https://github.com/agentscope-ai/QwenPaw/issues/6460) – High CPU in Edge+Wayland on session page**
  - Possibly rendering/WebSocket issue.
- **[#6458](https://github.com/agentscope-ai/QwenPaw/issues/6458) – Cron task safety check defaults to OFF**
  - Behavior question; not a crash.

### Fix PRs Available Today
- **[#6409](https://github.com/agentscope-ai/QwenPaw/pull/6409) – fix local model tool call JSON**
- **[#6410](https://github.com/agentscope-ai/QwenPaw/pull/6410) – fix Gemini nullable schema**
- **[#6412](https://github.com/agentscope-ai/QwenPaw/pull/6412) – fix PowerShell multiline**
- **[#6428](https://github.com/agentscope-ai/QwenPaw/pull/6428) – fix auth for plugin operations**

---

## Feature Requests & Roadmap Signals

### New Requests (2026-07-24/25)

- **[#6461](https://github.com/agentscope-ai/QwenPaw/issues/6461) – Full agent isolation** (1 comment, privacy concern)
- **[#6432](https://github.com/agentscope-ai/QwenPaw/issues/6432) – Built-in RAG knowledge base** (1 comment)
- **[#6455](https://github.com/agentscope-ai/QwenPaw/issues/6455) – Multi-model parallel execution** (1 comment)
- **[#6408](https://github.com/agentscope-ai/QwenPaw/issues/6408) – Undo/redo conversation turns** (2 comments)
- **[#6392](https://github.com/agentscope-ai/QwenPaw/issues/6392) – Agent-level token statistics** (2 comments)
- **[#6454](https://github.com/agentscope-ai/QwenPaw/issues/6454) – Copy context menu on selection**
- **[#6453](https://github.com/agentscope-ai/QwenPaw/issues/6453) – Preserve Chinese filenames in prompts**
- **[#6452](https://github.com/agentscope-ai/QwenPaw/issues/6452) – Hide "no multimodal" prompt elegantly**

### Closed Feature Requests (triage)
A massive batch of 11 feature issues by Hazemaan (e.g. #6441–#6451) were closed with “Close-and-review-later” – covering MCP bundling, parallel sub-agents, image generation, OCR, translation, notes, mini-apps, per-chat parameters, web search toggle, and assistant picker. This suggests the maintainers are aware of these directions but are not committing to them immediately.

### Likely Next-Release Candidates
- **PawApp mini-app platform** (already shipped in v2.0.1) – future plugins will leverage it.
- **Memory reranker** – PR [#5692](https://github.com/agentscope-ai/QwenPaw/pull/5692) and [#6399](https://github.com/agentscope-ai/QwenPaw/pull/6399) are under review.
- **AskUserQuestion tool** – PR [#6384](https://github.com/agentscope-ai/QwenPaw/pull/6384) adds structured user interaction.
- **Unified browser SDK** – PR [#6276](https://github.com/agentscope-ai/QwenPaw/pull/6276) could land soon.

---

## User Feedback Summary

**Pain points (real users):**
- **Migration friction**: Two users reported critical v1 features missing in v2.0.0 (SSH offline, profiles). One user called it “completely inaccessible”.
- **Performance regression**: A user measured ~2s fixed overhead per reply, calling it “absent in v1.x”.
- **MCP reliability**: Repeated registration (issue since April) and tool-not-found errors after v2.0 upgrade cause workflow failures.
- **Data integrity**: Cron tasks overwriting existing session history is a serious trust issue for automation users.
- **Agent isolation**: A user discovered one agent could read and modify another agent’s memories and settings, calling it a privacy leak.

**Satisfaction signals:**
- The new v2.0.1 with PawApp platform and Kanban app was released today, likely well-received.
- Several PRs addressing community-reported issues (auth fix, tool parsing, Windows PowerShell) show responsiveness.

**Use cases:**
- Enterprise-like: project management (Kanban), scheduled tasks, multi-channel bots (QQ, Zalo).
- Power users: model parameter tuning, multi-model comparisons, document-based RAG.
- Local first: ComfyUI integration, offline models.

---

## Backlog Watch

### Issues Needing Maintainer Attention

- **[#2999](https://github.com/agentscope-ai/QwenPaw/issues/2999) – Repeated MCP client registration leading to CancelledError** (open since April 6, 2026)
  - 3 comments, 0 reactions. Core architecture issue. No PR assigned. High impact.

- **[#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) – v2.0.0 missing features** (open since July 12, 2026)
  - 7 comments, high visibility. Affects migration from v1.1.12. No maintainer response visible.

- **[#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) – ~2s fixed overhead** (open since July 21, 2026)
  - 7 comments. Performance regression clearly described. No fix PR yet.

### PRs Needing Review

- **[#5692](https://github.com/agentscope-ai/QwenPaw/pull/5692) – Reranker support** (open since July 1)
  - Large feature; may need more eyes.
- **[#6284](https://github.com/agentscope-ai/QwenPaw/pull/6284) – QwenPaw Creator app** (open since July 20)
  - Considerable scope; under review but not yet merged.
- **[#6276](https://github.com/agentscope-ai/QwenPaw/pull/6276)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-07-25

## 1. Today's Overview
ZeptoClaw saw moderate activity over the past 24 hours, with two issues updated and two pull requests (one merged, one still open). The project’s most significant milestone is the closure of **PR #648**, which brings Telegram streaming support to the gateway. At the same time, a **critical CI regression** (Issue #646) was identified and remains open, and a **security-focused runtime fix** (PR #645) is under review. Overall, project health is strong with active develop/merge cycles, though the CI instability and the security fix require prompt resolution.

## 2. Releases
*No new releases were published today.*

## 3. Project Progress
| Merged/Closed PR | Description |
|------------------|-------------|
| **PR #648** (closed) | **feat(telegram): stream gateway responses** – Adds real-time Telegram response streaming via cumulative outbound stream phases. Progressive message edits preserve reply/fourm-topic routing, UTF-16 limits, HTML final rendering, and long-response continuations. |

The only PR merged today (#648) represents a major feature addition. The underlying issue **#647** (Telegram streaming) has also been closed.

## 4. Community Hot Topics
The most active item is **Issue #646** (2 comments), which is also the only discussion thread outside of PR reviews.

- **Issue #646** (open, P1-critical) – *[chore, area:safety, dependencies] chore(ci): restore Clippy and cargo-deny checks on current toolchain*  
  https://github.com/qhkm/zeptoclaw/issues/646  
  **Analysis:** The issue describes two CI failures exposed by PR #645: new Clippy warnings from Rust 1.97.1 and vulnerable dependencies (quick-xml 0.39.2, lopdf 0.40.0). The community’s underlying need is **maintaining CI reliability and supply-chain security** – any CI breakage stalls future development and undermines confidence in builds. Expect immediate maintainer attention.

No other issues or PRs attracted comments or reactions in the last 24 hours.

## 5. Bugs & Stability
Two stability/security items are active today:

| Item | Severity | Status | Details |
|------|----------|--------|---------|
| **PR #645** – Fixed runtime secrets leakage & process-reaping | **Critical** | Open (fix PR under review) | The PR corrects two runtime bugs: (1) subprocess environment inheriting provider keys and credentials, and (2) timeouts failing to terminate and reap descendant processes (including Docker containers). A working fix exists. |
| **Issue #646** – CI failures (clippy warnings + vulnerable deps) | **High** (P1-critical) | Open, no fix PR yet | Five new Clippy warnings and two known-vulnerable crate versions block CI. The root cause is toolchain and dependency churn; a chore PR is expected soon. |

*Note:* Issue #646 is not a runtime bug, but it directly blocks CI passes and thus constitutes a stability risk for the repository.

## 6. Feature Requests & Roadmap Signals
The only feature merged today is **Telegram streaming** (PR #648 / Issue #647). This aligns with the project’s gateway improvements and is likely to ship in the next release (already merged). No new feature requests were filed today.

Predictions for the next version (based on current pipeline):
- **Telegram streaming** (confirmed – merged)
- **Subprocess security fix** (PR #645 likely to be merged after review)
- **CI restoration** (Issue #646 – a chore fix will be necessary before any release)

## 7. User Feedback Summary
User feedback is not directly recorded in the provided data, but we can infer pain points from the issues and PRs:
- **Security & reliability:** The need for secure subprocess handling (PR #645) indicates user concerns about credential leakage and uncontrolled process trees, especially in multi-tenant or production settings.
- **Message delivery quality:** The Telegram streaming feature (PR #648) addresses a common user desire for lower-latency, progressive responses in chat channels – a clear satisfaction driver once released.

No explicit satisfaction/dissatisfaction comments are visible in the 24-hour window.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified in the current data. All items (issues #646, #647 and PRs #645, #648) were created or updated within the past two days and are receiving active maintainer attention.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-07-25

## 1. Today’s Overview
ZeroClaw continued at a high level of contributor activity: **47 issues** were updated (39 open/active, 8 closed) and **50 pull requests** were updated (40 open, 10 merged or closed). No new releases were published today. The project is deep in a sustained development sprint, with major RFCs on governance, plugin architecture, and security advancing alongside a steady stream of bug fixes and feature PRs. The eight closed issues and ten closed/merged PRs indicate healthy forward progress, while the number of open items (especially security S1/S0 bugs) shows that hardening and stabilisation remain top priorities.

## 2. Releases
No new releases today. The last known release is **v0.8.3** (mentioned in issue #9290). Upcoming v0.9.0 is being coordinated via [tracker #7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) and will bundle auth, security, gateway, and breaking changes.

## 3. Project Progress
Merged or closed items today include:

- **PR #9305** (closed) – `chore(deps): bump anchore/sbom-action` – Dependencies update for SBOM generation.
- **PR #8679** (closed) – `docs(sop): clarify boolean condition comparisons` – Documentation improvement for SOP condition evaluator.
- **Issues closed (8 total)** – Among them:
  - **#6074** – Tracker for recovering 153 lost commits after a bulk revert (closed, work complete).
  - **#8834** – Config alias creation bug for non-provider sections (closed with fix).
  - **#6434** – Shell tool calls refused at `autonomy level = "full"` (closed).
  - **#9204** – Landlock sandbox restricting the daemon itself (closed, fix merged?).
  - **#9236** – Fresh Telegram aliases dropped after config reload (closed).
  - **#9240** – `save_dirty` silently dropping writes with dots in map keys (closed).
  - **#7623** – Delegate sub-agent still leaking API keys (closed).
  - **#9116** – ACP console splitting thinking entries (closed).

Features that advanced include goal command admission (PR #8689), trusted goal tools (PR #8688), goal controller/verifier (PR #8687), and the first-class Crusoe provider (PR #9338). Several PRs remain open in the goal-stack series, indicating this feature is nearing completion.

## 4. Community Hot Topics
The following issues attracted the most discussion (by comment count):

- **#6808 (14 comments)** – [RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808). This governance RFC proposes a system to automate issue routing and reduce manual label maintenance. It has been in progress since May and is now in rollout; the community is engaged on implementation details.
- **#6489 (4 comments)** – [[Feature]: "Everything is a plugin"](https://github.com/zeroclaw-labs/zeroclaw/issues/6489) – A long-term architectural RFC to unify integrations and plugins. Accepted but still being scoped.
- **#8396 (3 comments)** – [RFC: Make wire protocol first-class in provider construction](https://github.com/zeroclaw-labs/zeroclaw/issues/8396) – Proposes formalizing the wire protocol (e.g., REST vs gRPC) as a first-class concept in provider onboarding.
- **#9285 (3 comments)** – [Bug: nested `set_prop` masks invalid values](https://github.com/zeroclaw-labs/zeroclaw/issues/9285) – A config validation edge case discovered by a contributor.

The PRs with the most activity (though comment counts are not reported as high) are the goal-stack PRs (#8746, #8689, #8688, #8687, #8996) – these represent a major cross-cutting feature that touches many components.

**Underlying needs:** The community is driving toward better governance automation, a unified plugin model, and formal protocol descriptions. The goal-stack PRs indicate a desire for persistent, interruptible agent tasks.

## 5. Bugs & Stability
Several high-severity bugs were reported or updated today:

| Issue | Severity | Status | Summary | Fix PR Exists? |
|-------|----------|--------|---------|----------------|
| [#9247](https://github.com/zeroclaw-labs/zeroclaw/issues/9247) | **S0** – data loss / security risk | Open | Shell tool workspace boundary bypass via symlinks. | No |
| [#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) | **S1** – workflow blocked | Open | CLI-created cron jobs have hardcoded `delivery.mode = "none"`, discarding output. | Yes, [#9350](https://github.com/zeroclaw-labs/zeroclaw/pull/9350) |
| [#9290](https://github.com/zeroclaw-labs/zeroclaw/issues/9290) | **S1** – workflow blocked | Open | Windows desktop installer crashes on launch due to missing `TaskDialogIndirect`. | No |
| [#9204](https://github.com/zeroclaw-labs/zeroclaw/issues/9204) | **S1** – workflow blocked | Closed | Landlock sandbox restricted the daemon itself (fix merged). | Yes, [#9114](https://github.com/zeroclaw-labs/zeroclaw/pull/9114) (open, depends on #9233) |
| [#9328](https://github.com/zeroclaw-labs/zeroclaw/issues/9328) | p2, **high risk** | Open | `verifiable-intent` evaluates constraints without verifying the credential chain. | [Fix PR #9327](https://github.com/zeroclaw-labs/zeroclaw/pull/9327) (open, needs author action) |
| [#8519](https://github.com/zeroclaw-labs/zeroclaw/issues/8519) | p1, **high risk** | Open | Cargo-audit/deny.toml drift for Wasmtime CVEs remains unresolved. | Partial work in #8781 |
| [#9285](https://github.com/zeroclaw-labs/zeroclaw/issues/9285) | p2, minor | Open | Nested config set_prop returns confusing path errors instead of value errors. | No |

**Key observations:** Two S0/S1 bugs were reported today (#9247 shell bypass, #9340 cron delivery). The shell bypass is a security gap requiring immediate attention. The cron delivery issue has an associated fix PR. The Windows installer bug blocks desktop users entirely.

## 6. Feature Requests & Roadmap Signals
Notable feature requests and RFCs updated today:

- **#6808** – Work lanes / board automation (accepted, rollout in progress) – Likely to land as v0.8.x or v0.9.0 governance improvement.
- **#6489** – Unified plugin catalog (accepted, phased) – Will reshape how integrations are added; likely v0.9.0+.
- **#8396** – Wire protocol as first-class construct (accepted) – Affects provider onboarding, could land in v0.9.0.
- **#8228** – DingTalk streaming message support (accepted) – Low blocking, but wanted by Chinese users.
- **#9246** – Preserve Todo tracker config during ZeroCode ownership migration (RFC open) – Aims to avoid breaking user configuration.
- **#9323** – Execution-tree iteration budget ownership (RFC open) – Proposes bounding parent/child agent loops; could prevent resource exhaustion.
- **#9335** – Support data-wrapped OpenAI-compatible responses (accepted) – Enables compatibility with non-standard providers.
- **#9315** – Classify Telegram file-download failures (accepted) – Reduces retry waste.

**Prediction:** The next release (likely v0.9.0) will include:
- Goal-stack features (persistent goals, goal commands)
- Plugins with scoped secrets and encrypted state (PR #8857)
- Improved channel streaming (DingTalk, Telegram improvements)
- Security hardening: Landlock fixes, SSRF gates (PR #8713), symlink boundary protection

## 7. User Feedback Summary
Real pain points and use cases reflected in today’s issues:

- **Configuration friction:** Multiple reports about config alias leaks, dots in map keys, and silent drops (#8834, #9236, #9240, #9285). Users find the config system unpredictable.
- **Security restrictions blocking legitimate usage:** Shell tool refusal at `full` autonomy (#6434 – now fixed) and landlock sandbox breaking the daemon (#9204 – fixed) indicate that the security model can be too aggressive.
- **Missing output delivery:** CLI cron jobs silently discard results (#9340) – a usability regression for automation users.
- **Desktop on Windows broken:** Installer fails on missing `TaskDialogIndirect` (#9290) – a platform blocker for new users.
- **Channel integration quirks:** Discord typing indicator stuck (#9198), QQ passive reply missing msg_id (#7872), Telegram alias loss (#9236). Users expect reliable channel operation.
- **Verifiable-intent trust gap:** VI constraints evaluated without cryptographically verified credentials (#9328) – undermines security promises.

Overall, the community is heavily invested in both fixing existing bugs and pushing ambitious RFCs, indicating a healthy but stretched maintainer capacity.

## 8. Backlog Watch
Issues and PRs that have been open for extended periods or appear stalled:

- **#8519** (p1, high risk) – `Reconcile cargo-audit ignores and remediate wasmtime-wasi CVEs` – Open since June 30, no fix PR merged. Security-relevant.
- **#8288** (p2, high risk) – `SOP milestone: daemon-owned SOP control plane to 5/5` – Open since June 24, multiple PRs in progress but not yet complete.
- **#7904** (p2) – `always-inject SKILL.md frontmatter no longer works in compact prompt mode` – Open since June 17, no fix PR.
- **#7872** (p1) – `QQ group replies need msg_id` – Open since June 17, although a PR (#9180) merged, the tracker remains open.
- **#9047** (p2) – `Clarify Code session history and persistent-memory isolation` – Open since July 14, only one comment, needs maintainer decision.
- **#9323** (RFC, p2, high risk) – `Define execution-tree iteration budget ownership` – Filed yesterday, needs maintainer review.
- **PRs with `needs-author-action` label:** Many large PRs (e.g., #8713, #8746, #8689, #8688, #8687, #8996, #8857, #9195, #9327, #8781) have this label, indicating they are waiting for author updates. Maintainers should ping these contributors or offer assistance to unblock.

**Call to action:** The `needs-author-action` stack represents a significant amount of work that, if unpaused, could move several features forward. The CVE reconciliation (#8519) and the Windows installer bug (#9290) are particularly pressing.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*