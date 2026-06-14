# OpenClaw Ecosystem Digest 2026-06-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-14 02:54 UTC

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

# OpenClaw Project Digest — 2026-06-14

## 1. Today's Overview

OpenClaw remains in an intensely active development phase. In the last 24 hours, **500 issues** and **500 pull requests** were updated — a clear signal of sustained community and maintainer engagement. Among these, 199 PRs were merged or closed, and two new beta releases (v2026.6.7 and v2026.6.8) shipped with channel delivery improvements. However, the project is wrestling with a cluster of high-severity stability issues: subagent completion loss, memory leaks, session-state contamination, and security vulnerabilities from unsanitised skill inputs. The backlog contains several long-standing feature requests and critical bugs that still lack fix PRs, indicating that maintainer bandwidth is stretched despite high overall activity.

## 2. Releases

Two new beta versions were published today:

**[v2026.6.8-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.1)**
- **Telegram**: structured rich text with tables, lists, expandable blockquotes; prompt-preserving CLI backend delivery; retired native draft migration; safer rich-media boundaries.
- **WhatsApp**: richer, more brittle channel delivery.

**[v2026.6.7-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.7-beta.1)**
- **Slack**: same-channel finals persist in transcripts.
- **Telegram**: top-level `image` message‑tool sends attached media; expandable blockquotes and spool improvements.
- **Outbound media & silent replies**: tighter delivery across channels.
- Progress drafts and paged action results refined.

No breaking changes or migration notes were included in the provided release notes; both are labelled beta and focus on delivery reliability.

## 3. Project Progress

Of the 199 merged/closed PRs today, the following notable fixes and features stand out from the sample:

- **Merged/closed PRs:**
  - [#91824](https://github.com/openclaw/openclaw/pull/91824) – Added usage guidance to `sessions_spawn` tool description to encourage sub‑agent delegation (fixes #91814).
  - [#91403](https://github.com/openclaw/openclaw/pull/91403) – Fixed OpenAI‑compatible adapter emitting empty responses when stream finishes with `stop` but no content.
  - [#39857](https://github.com/openclaw/openclaw/pull/39857) – Closed: session context window over‑reporting issue.
  - [#45698](https://github.com/openclaw/openclaw/issues/45698) – Closed: Control UI progressive stuckness (likely resolved).
  - [#43260](https://github.com/openclaw/openclaw/issues/43260) – Closed: support for `model` field in SKILL.md frontmatter (per‑skill model routing).
  - [#44922](https://github.com/openclaw/openclaw/issues/44922) – Closed: cron job with `sessionTarget:"main"` causing duplicate triggers.

- **Open but advancing PRs:**
  - [#92840](https://github.com/openclaw/openclaw/pull/92840) – Fixes Feishu monitor memory leak (#48183) by awaiting HTTP server shutdown during cleanup.
  - [#92842](https://github.com/openclaw/openclaw/pull/92842) – Fixes Telegram progress bubble lingering above subsequent messages.
  - [#92770](https://github.com/openclaw/openclaw/pull/92770) – Places Qwen/DashScope image prompts in user content instead of system message.
  - [#92660](https://github.com/openclaw/openclaw/pull/92660) – Fixes plugin dry‑run update check with exact version pin.
  - [#90057](https://github.com/openclaw/openclaw/pull/90057) – Polish of Workboard operations UI (large feature).

The release cadence (two betas in two days) shows that maintainers are pushing delivery and channel improvements to production quickly.

## 4. Community Hot Topics

The following issues generated the most discussion and reactions, revealing deep user concerns about reliability and missing features:

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 19 | 1 👍 | **P1**: Subagent completion silently lost – no retry, no notification, no auto‑restart on timeout. Users report silent data loss in long‑running agents. |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) | 18 | 0 | **P2**: Request for a centralized filename encoding utility to handle multi‑encoding Content‑Disposition (Shift‑JIS, GB18030, etc.) across all channel adapters. |
| [#48183](https://github.com/openclaw/openclaw/issues/48183) | 18 | 0 | **P2**: Feishu monitor state cleanup incomplete – potential memory leak in `httpServers` Map. Fix PR [#92840](https://github.com/openclaw/openclaw/pull/92840) is now open. |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | 10 | 4 👍 | **P2**: Request for pre‑reset agentic memory flush – `/new` and daily reset should trigger the same memory flush as compaction to avoid losing context. |
| [#43015](https://github.com/openclaw/openclaw/issues/43015) | 8 | 3 👍 | **P1**: `message.send` schema overexposes poll/components/modal causing GPT auto‑population breakages. |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 8 | 3 👍 | **P1**: Regression – "Cannot convert undefined or null to object" with google‑vertex/gemini‑3.1‑pro‑preview. |

**Underlying needs**: Users are demanding **reliability** (subagent orchestration, session state management), **security** (sanitisation of injected content), and **cross‑platform encoding support** for non‑Western language users. The high engagement on memory management issues reflects frustration with context loss and data corruption.

## 5. Bugs & Stability

Several severe bugs remain open, while some have active fix PRs. Severity ranking (P0 > P1 > P2):

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | **P0** | Gateway memory leak – RSS grows from 350 MB to 15.5 GB over days, causing OOM crashes. | No |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | **P1** | Subagent completion silently lost – no retry or notification. | No |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | **P1** | Multi‑agent orchestration unstable – concurrent config overwrites, session‑lock failures. | No |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) | **P1** | `gh-issues` skill injects raw issue body into sub‑agent prompt – security vulnerability. | No |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | **P1** | Steer mode does not inject messages mid‑turn for main sessions. | No |
| [#46786](https://github.com/openclaw/openclaw/issues/46786) | **P1** | `tools.elevated.enabled: true` breaks exec routing – all calls go to gateway host instead of sandbox. | No |
| [#48183](https://github.com/openclaw/openclaw/issues/48183) | **P2** | Feishu monitor memory leak. | Yes – [#92840](https://github.com/openclaw/openclaw/pull/92840) |
| [#44905](https://github.com/openclaw/openclaw/issues/44905) | **P1** | Discord leaks internal tool‑call traces (NO_REPLY, commentary, `to=functions`) to channel. | No |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | **P1** | Regression: google‑vertex/gemini‑3.1‑pro‑preview fails with "Cannot convert undefined or null to object". | No |
| [#40540](https://github.com/openclaw/openclaw/issues/40540) | **P1** | `openclaw update` fails with EBUSY on Windows. | No |
| [#43661](https://github.com/openclaw/openclaw/issues/43661) | **P1** | Session hangs indefinitely when compaction times out, causing repeated duplicate message sends. | No |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) | **P2** | Multi‑encoding filename handling – no fix PR yet. | No |

**Regression bugs** are particularly concerning: #38327, #46786, #40540, #43661, and #45494 (cron jobs silently timeout during sustained API outages) all indicate recent changes introduced regressions. The lack of fix PRs for P0/#91588 and many P1s is a risk signal for production deployments.

## 6. Feature Requests & Roadmap Signals

The most requested features that are likely candidates for the next minor release:

- **Centralized filename encoding** (#48788) – high demand (18 comments) and directly affects international users. A fix for Feishu Chinese filenames was attempted but shelved in favour of a broader solution.
- **Per‑agent cost budgets** (#42475) – 12 comments, 1 👍. Operators need spend control without external monitoring; would be a natural gateway‑level enhancement.
- **YAML config support** (#45758) – 7 comments, 2 👍. Popular among DevOps users but low urgency (P3). Could be a community contribution.
- **MathJax/LaTeX in Control UI** (#42840) – 7 comments, 6 👍 (highest upvotes). High interest for academic/scientific use cases.
- **Memory trust tagging by source** (#7707) – 11 comments, 0 👍. Security‑focused feature to prevent memory poisoning from untrusted sources.
- **Tool search directory mode** – active PR [#91632](https://github.com/openclaw/openclaw/pull/91632) adds `tools.toolSearch.mode: "directory"` for large tool catalogs.
- **Path‑scoped RWX permissions** (#39979) – replaces binary allowlist with Unix‑style DAC. High security impact.

**Roadmap prediction**: The next version (likely 2026.6.x stable) will include the filename encoding utility (PR expected from community), the Feishu memory leak fix, and possibly the cost budget enforcement. Memory trust tagging and per‑skill model routing (merged as #43260) may also land soon.

## 7. User Feedback Summary

**Pain points expressed by users:**
- **Silent data loss**: Subagent results disappear without retry (#44925), write tool has no append mode (#40001), session resets lose memory (#45608).
- **Configuration instability**: Multi‑agent orchestration fails under concurrent access (#43367), cron jobs contaminate global state (#90991).
- **Security leaks**: Discord leaks internal tool‑call JSON (#44905), gh‑issues skill injects untrusted bodies into prompts (#45740), elevated exec routing exposes sandbox bypass (#46786).
- **Platform‑specific breakage**: Windows EBUSY on update (#40540), Chinese filename garbling (#48788), Feishu mention placeholders not resolved (#48786).
- **UI/UX frustration**: Control UI becomes stuck (#45698), Workboard view needs polish (PR #90057), cost dashboard omits archived session files (#46252).

**Use cases** driving feedback: multi‑agent coding batches, cron‑based scheduled tasks, Telegram/Feishu/Discord integration for team workflows, and browser automation (email sign‑ups, form filling). Users expect OpenClaw to handle concurrent sessions reliably without manual intervention.

**Satisfaction signals**: High community engagement (500 issues/PRs updated daily) and rapid release cadence suggest users are invested. The two new betas show that maintainers are actively addressing channel delivery issues. However, the volume of unaddressed P1 bugs and regressions indicates a gap between user expectations and current stability.

## 8. Backlog Watch

The following items have remained open for extended periods without maintainer action or a fix PR, despite significant community attention:

| Issue | Age | Comments | Status |
|-------|-----|----------|--------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) – Memory Trust Tagging by Source | Since Feb 3 (≈5 months) | 11 | Needs product decision + security review; no PR. |
| [#39979](https://github.com/openclaw/openclaw/issues/39979) – Path‑scoped RWX permissions | Since Mar 8 (≈3 months) | 7 | Needs maintainer + security review; no PR. |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) – MathJax/LaTeX rendering in Control UI | Since Mar 11 (≈3 months) | 7 | Needs product decision; no PR. |
| [#42475](https://github.com/openclaw/openclaw/issues/42475) – Per‑agent cost budgets | Since Mar 10 (≈3 months) | 12 | Needs product decision; no PR. |
| [#45758](https://github.com/openclaw/openclaw/issues/45758) – YAML config support | Since Mar 14 (≈3 months) | 7 | Low priority (P

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI agent open-source landscape on 2026-06-14 reveals a rapidly maturing but fragmented ecosystem. Most projects derive from OpenClaw's architecture, creating a family tree of specialized forks targeting different hardware tiers, deployment models, and user personas. The ecosystem is characterized by intense feature iteration (1,100+ combined issues/PRs updated daily), a shared struggle with production stability (memory leaks, subagent failures, configuration regressions), and growing demand for cross-platform integration (Telegram, Slack, WeChat, WhatsApp). A clear tension exists between rapid feature development and the reliability required for production deployments, with each project prioritizing different trade-offs.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release (24h) | Health Score | Key Stability Risk |
|---------|---------------------|-------------------|---------------|--------------|---------------------|
| **OpenClaw** | 500 | 500 | 2 betas | ⚠️ Moderate | P0 memory leak (#91588), no fix PR |
| **ZeroClaw** | 42 | 50 | None | ⚠️ Concern | 5x S1 regressions in 24h; quick fixes |
| **Hermes Agent** | 50 | 50 | None | ✅ Good | 48 open PRs, review bottleneck |
| **IronClaw** | 2 | 22 | None | ⚠️ Moderate | Nightly E2E failing 18 days (#4108) |
| **NanoBot** | 5 | 19 | None | ✅ Good | Anthropic temperature regression (#4333), fix PR open |
| **CoPaw** | 8 | 8 | None | ⚠️ Moderate | Chat freezes after idle; Windows startup 10+ min |
| **PicoClaw** | 2 | 7 | Nightly | ✅ Good | Token consumption bug (#3012), no fix PR |
| **NanoClaw** | 1 | 6 | None | ✅ Good | Container data loss (#2516, #2640), fix PR open |
| **LobsterAI** | 4 | 5 | None | 🔴 Critical | 4 bugs open since April, no maintainer response |
| **Moltis** | 1 | 3 | None | ✅ Good | OAuth blocker (#1119), fix PR open |
| **NullClaw** | 2 | 1 | None | ⚠️ Moderate | Scheduled jobs silently fail (#941), fix PR open |
| **TinyClaw** | 0 | 0 | None | 🟢 Dormant | No activity |
| **ZeptoClaw** | 0 | 0 | None | 🟢 Dormant | No activity |

**Health Score criteria**: Combines bug severity/volume, fix PR velocity, community responsiveness, and regression prevalence. "Good" indicates manageable issues with active fixes; "Moderate" indicates a significant unresolved bug; "Concern" indicates multiple S1 regressions or pipeline failure; "Critical" indicates abandoned project risk.

## 3. OpenClaw's Position

OpenClaw remains the undisputed **core reference implementation** by community size and feature surface area. Its 500 daily issue/PR updates dwarf all peers, and its two-beta-per-day release cadence demonstrates aggressive iteration. Key advantages:

- **Channel breadth**: Telegram, Slack, WhatsApp, Feishu, Discord — no peer matches this coverage for rich media delivery
- **Skill/tool ecosystem**: Largest library of third-party skills and subagent orchestration patterns
- **Community investment**: 199 PRs merged/closed in 24h, sustained engagement from maintainers

However, OpenClaw's sheer complexity introduces **proportional instability**. The P0 memory leak (#91588) with no fix PR, multiple unresolved P1 subagent completion bugs, and regressions from "recent changes" create a reliability gap that smaller, focused projects exploit. ZeroClaw has effectively forked OpenClaw's architecture with a tighter scope (security-first, WASM plugins). Hermes Agent offers better provider flexibility (Bedrock, GitHub Copilot). The core advantage OpenClaw retains is **ecosystem gravity** — new features land here first, and the community base provides faster bug discovery.

**Community size comparison** (by daily activity):
- OpenClaw: 1,000 total updates → 10× larger than next tier
- Tier 2 (50-100 updates): Hermes Agent, ZeroClaw, IronClaw
- Tier 3 (5-20 updates): NanoBot, CoPaw, PicoClaw, NanoClaw
- Tier 4 (<5 updates): LobsterAI, Moltis, NullClaw, TinyClaw, ZeptoClaw

## 4. Shared Technical Focus Areas

Across projects, five common requirements emerge:

| Focus Area | Affected Projects | Specific Need |
|------------|------------------|---------------|
| **Memory/Context Reliability** | OpenClaw (#45608, #43661), NanoBot (#4264), Hermes Agent (#23975, #33907), CoPaw (#5171), ZeroClaw (#5849) | Non-destructive context compression, predictable memory flush/consolidation, orphan session recovery |
| **Subagent Orchestration Stability** | OpenClaw (#44925, #43367), Hermes Agent (#31155), NullClaw (#941), CoPaw (#5174) | Reliable subagent completion with retry/notification, cross-session delegation, cron job execution guarantees |
| **Channel-Specific Delivery** | OpenClaw (Feishu #48788, Discord #44905), Hermes Agent (Telegram #44428), ZeroClaw (QQ/WeChat #7531), CoPaw (Zalo #5168) | Encoding consistency (Shift-JIS, GB18030), streaming cards for Chinese IM, rich media parity, leak prevention |
| **MCP/Plugin Extensibility** | ZeroClaw (#7497, #7420), Moltis (#1119), NanoBot (#4303), Hermes Agent (#45674) | Native plugin loading, OAuth for MCP servers, streaming MCP stability, tool restriction semantics |
| **Configuration/Provider Friction** | Hermes Agent (#44666, #43586), OpenClaw (#43015), ZeroClaw (#6876), CoPaw (#5156) | Silent API key failures, per-skill model routing, env var transparency, provider timeout configurability |

**Cross-cutting pattern**: Every project with active development is investing in **non-destructive state management** — the ability to handle long-running sessions without corrupting history, losing subagent results, or leaking memory. This is the single greatest reliability concern across the ecosystem.

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | NanoBot | PicoClaw | IronClaw | Others |
|-----------|----------|----------|--------------|---------|----------|----------|--------|
| **Primary User** | Power users, integrators | Security-conscious operators | Multi-provider developers | WebUI-centric teams | Embedded/edge deployers | Rust-native enterprise | Niche (CN, RAG, minimal) |
| **Architecture** | Monolithic reference | Modular with RFC-driven design | Provider-agnostic adapter layer | Config-focused, WebUI-first | Lightweight, embedded-optimized | Rust rewrite, typed capability | Single-purpose |
| **Language** | Python/TypeScript | Rust/WASM | Python | Python | Go | Rust | Python/Go |
| **Deployment Target** | Cloud/server | Desktop/mobile | Cloud + desktop | Desktop + local | Low-resource devices | High-throughput server | Variable |
| **Innovation Driver** | Channel breadth | Plugin system + security | Provider flexibility | Settings parity + TUI | Model routing + i18n | Attachment framework | Localization |
| **Stability vs Features** | Features > Stability | Balancing both | Features with quick fixes | Slow, steady | Nightly, experimental | Stable core, new features PR | Mostly stalled |

**Key insight**: The ecosystem is differentiating along a **complexity gradient**. ZeroClaw and IronClaw are building for **principled extensibility** (type-safe, auditable, containerized). Hermes Agent and OpenClaw prioritize **feature surface area** and provider coverage. PicoClaw and NanoBot target **accessibility** (embedding, WebUI-first). This creates a healthy market where different deployment contexts are served — but the diversity also means no single project offers "end-to-end reliability" yet.

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating (ship-fast/stabilize-later):**
- **OpenClaw**: 500 daily updates, 2 releases/day. Highest feature velocity but accumulating technical debt (P0 memory leak, regression cluster). Maintainers stretched.
- **ZeroClaw**: 92 daily updates. Most aggressive stabilization (5 S1 bugs met with 6+ fix PRs same day). Strong architectural RFC process. Approaching v0.8.1 maturity.
- **Hermes Agent**: 100 daily updates. Heavy community contribution (48 open PRs). Strong provider support but reviewer bottleneck.
- **IronClaw**: 24 daily updates. Attachment framework shipping. Nightly pipeline failure (#4108) undermines quality signal.

**Tier 2 — Steady Improvement (measured pace):**
- **NanoBot**: 24 daily updates. Merged 5 PRs including critical memory and WebUI fixes. Cleanest health profile among active projects.
- **PicoClaw**: 9 daily updates. Nightly releases, ongoing feature work (image compression, remote mode). Single open bug, one fix merged.
- **NanoClaw**: 7 daily updates. Infrastructure-focused (providers, memory scaffold, SDK). No user-facing complaints.

**Tier 3 — Low Activity / Stabilization Phase:**
- **NullClaw**: 3 daily updates. Single critical bug fix under review. Minimal engagement.
- **Moltis**: 4 daily updates. Focused OAuth fix. Healthy but low-volume.
- **CoPaw**: 16 daily updates but 7 open bugs with first-time-contributor PRs under review. Tauri migration regressions.

**Tier 4 — Stalled / Maintenance Mode:**
- **LobsterAI**: 9 daily updates but 4 issues open since April 3 without maintainer response. At risk of abandonment.
- **TinyClaw, ZeptoClaw**: No activity.

**Overall momentum heat map**: 🔥 OpenClaw, ZeroClaw, Hermes Agent | 🔥🔥 NanoBot, PicoClaw, IronClaw | ❄️ CoPaw, NullClaw, Moltis | 🧊 LobsterAI, TinyClaw, ZeptoClaw

## 7. Trend Signals

**1. Subagent reliability is the universal blocking issue.**  
Across OpenClaw, Hermes Agent, and NullClaw, silent subagent failure is the top complaint. Users can't trust multi-step workflows. Expect every project to ship retry/notification/health-check mechanisms in Q3 2026.

**2. MCP is winning as integration protocol, OAuth is the gap.**  
ZeroClaw, Moltis, and NanoBot all touch MCP extensibility. The blocking issue is OAuth flow — MCP servers increasingly require it, and current implementations fail silently. This is the next "must-have" platform feature.

**3. Chinese IM channels (WeChat, QQ, Feishu, Zalo) represent an underserved market.**  
ZeroClaw, CoPaw, and OpenClaw all field requests for streaming cards and native support. Western-focused projects (IronClaw, NullClaw) are missing a growing user base.

**4. Non-destructive memory management is the next frontier.**  
Projects with tight budgets (NanoBot's `idleCompact`, OpenClaw's compaction timeout bug, ZeroClaw's Dream Mode) are all converging on the same insight: agents need offline, safe memory consolidation that doesn't lose recent corrections. The ecosystem is moving from "append-only history" to "structured, queryable memory."

**5. Security and trust are moving up the priority stack.**  
OpenClaw's memory poisoning issue (#7707), ZeroClaw's risk profile redesign (#6876), and Hermes Agent's delegation model (#31155) all point to a shift: the AI agent market is moving beyond "can it do X?" to "can I trust it to do X without leaking data or following a poisoned prompt?" Expect trust-tagged memory and granular permission frameworks to become table stakes.

**Value for AI agent developers**: The ecosystem is currently in a **standardization-innovation cycle**. OpenClaw provides the baseline; ZeroClaw and IronClaw are building the standard library of secure, modular components. If you need breadth today, choose OpenClaw. If you need reliability and auditability for production, watch ZeroClaw's v0.9 and IronClaw's attachment framework. The trend toward **provable memory** and **MCP-first architecture** suggests that investing in MCP server development and trust-tagged data pipelines will be higher-ROI than building on fragile subagent orchestration patterns.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-14

## 1. Today's Overview

The project shows high activity over the past 24 hours, with **19 pull requests updated** (14 open, 5 merged/closed) and **5 issues touched** (3 closed, 2 open). No new releases were published. The development pulse is focused on **provider compatibility fixes**, **WebUI performance & parity improvements**, **MCP/streaming reliability**, and **new feature additions** such as a TUI mode, TTS configuration, and subagent model presets. The maintainers are actively merging bug fixes and refactoring efforts, indicating a healthy pace toward a next minor release.

## 2. Releases

*No new releases today.*

## 3. Project Progress — Merged/Closed PRs

Five pull requests were merged or closed in the last 24 hours, advancing both stability and feature sets:

- **#4098 — Fix exec workspace symlink guard and path precedence**  
  *Merged* — Addresses #4072 and #4083 by blocking restricted exec commands from following relative symlinks outside the workspace, and prepends `pathAppend` on Unix so configured tool paths take executable lookup precedence.

- **#4326 — fix(memory): summarize full session tail during idle compaction**  
  *Merged* — Fixes #4264: `idleCompact` now summarizes over the entire unconsolidated session tail, including the retained recent suffix, preventing loss of corrective user feedback in history.

- **#4327 — Fix WebUI startup blocking on slow gateway routes**  
  *Merged* — Moves slow HTTP handlers off the gateway event loop, avoids full session JSONL reads for workspace scope resolution, and makes chat surface fetch only installed CLI apps instead of the full remote catalog at startup.

- **#4314 — Break tool config schema import cycle**  
  *Merged* — Moves shared Pydantic config `Base` into a new `nanobot.config_base` module, resolving circular imports while keeping built-in tool configs alongside their implementations.

- **#4313 — Feat(webui): config.json/webui parity**  
  *Merged* — Closes the gap between WebUI settings panels and `config.json` by adding write endpoints for temperature, tool limits, dream, channels, and memory fields, plus expanded UI controls.

## 4. Community Hot Topics

- **#193 — Ollama API support? (CLOSED, 15 comments)**  
  [Issue](https://github.com/HKUDS/nanobot/issues/193) — The most commented issue, asking for Ollama API support. Although closed, the high engagement signals strong user desire for non‑vLLM local inference options. No direct PR was created, but the discussion may influence future provider abstractions.

- **#4333 — Anthropic provider sends deprecated temperature to opus-4-8 / Fable (OPEN, 0 comments, new)**  
  [Issue](https://github.com/HKUDS/nanobot/issues/4333) — Despite being very recent, this issue is critical for all users of newer Anthropic models and already has a fix PR (#4334) proposed.

- **#4322 — NameError: 'session_key' is not defined in context.py after merge (OPEN, 1 comment)**  
  [Issue](https://github.com/HKUDS/nanobot/issues/4322) — A regression affecting users who merged `origin/main` into `fix/prompt-caching`. The root cause was identified and a fix is expected soon.

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | #4333 – Anthropic provider sends deprecated `temperature` to opus-4-8 / Fable → 400 on every request | Open | #4334 (proposed) |
| **High** | #4322 – `NameError: 'session_key' is not defined` crashes agent on startup after merging | Open | No PR yet |
| **Medium** | #4303 – MCP streamableHttp server crash on `_close_server` reconnect due to cancel scope task mismatch | Open | #4303 (proposed) |
| **Low** | #4083 – `pathAppend` did not give configured tools precedence – **Closed** | Fixed | #4098 (merged) |
| **Low** | #4264 – `idleCompact` summarized incomplete history – **Closed** | Fixed | #4326 (merged) |

Additional fix PRs addressing environment-variable resolution in transcription (#4323) and WebUI settings (#4324, #4325) are still open.

## 6. Feature Requests & Roadmap Signals

- **Ollama API support** (#193) – While closed, the high comment count suggests it remains a desired feature. May appear as a new provider in a future release.
- **Subagent model presets** (#4291, open) – Allows LLM to specify a named preset when calling `spawn`, enabling subagents to run with a different model than the parent.
- **Text-to-Speech configuration** (#4316, open) – Adds a configurable TTS system with OpenAI, Groq (Orpheus), and ElevenLabs providers, exposed through WebUI settings.
- **TUI mode for `nanobot agent`** (#4329, open) – A non‑full‑screen interactive TUI with markdown rendering, slash commands, multimodal input, and session management.
- **WebUI automation management** (#4330, open) – A dedicated UI for listing, filtering, running, pausing/resuming, and deleting user automations.
- **Toggle for built-in filesystem tools** (#4138, open) – Would allow deployments to restrict the model to only MCP‑provided filesystem capabilities, useful for remote sandboxes.

The features in open PRs (#4291, #4316, #4329, #4330) are strong candidates for the next minor release.

## 7. User Feedback Summary

Real pain points voiced through issues and PRs include:

- **Anthropic model breakage** (#4333) – Users relying on `claude-opus-4-8` or Fable cannot make any request until the `temperature` parameter is omitted. High frustration.
- **Memory summarization losing corrections** (#4264) – Users who correct the model during a conversation found that `idleCompact` dropped the final correct response from history, leaving erroneous records. The fix in #4326 directly addresses this.
- **MCP streaming crashes** (#4303) – Users with streamableHttp MCP servers encounter crashes on session reconnect. Fix proposed.
- **Slow WebUI startup** (#4327, now fixed) – Previous slow gateway routes made the WebUI unresponsive at launch.
- **Settings parity gaps** (#4313, now merged) – Users had to manually edit `config.json` because WebUI panels were missing fields like temperature or tool limits.

Overall, the community is actively reporting bugs and seeing quick responses from maintainers, indicating a responsive development process.

## 8. Backlog Watch

No extremely long‑standing open issues were found. The following open PRs have been awaiting review or further action for more than 12 days:

- **#4138** – `add tools.file.enable to toggle built-in filesystem tools` (opened 2026-06-01, last updated 2026-06-13) – This enhancement touches on deployment security and may need maintainer feedback.
- **#4291** – `feat(spawn): allow subagents to use configurable model presets` (opened 2026-06-11) – A substantial feature that may require review of the preset configuration schema.
- **#4303** – `fix(mcp): close tracked generators in _close_server to prevent GC crash` (opened 2026-06-11) – A stability fix that should be prioritized.

Maintainers are encouraged to review these items to prevent them from lingering.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-14

## 1. Today’s Overview

The Hermes Agent project continues its rapid pace with **50 issues** and **50 PRs** updated in the last 24 hours. Community activity is intense: 44 issues remain open, 6 were closed, while only 2 PRs were merged/closed against 48 still open. No new releases were issued today. The volume of open pull requests (48) indicates a large backlog awaiting review, but the steady stream of bug fixes and features—especially around provider support, TUI/Desktop UI, and gateway integrations—shows a project actively addressing user pain points. Key themes this week include **Telegram Bot API 10.1 rich messages**, **context compression stability**, **Delegation model routing**, and **memory consolidation**.

## 2. Releases

No new releases were published on this date.

## 3. Project Progress

**Merged/Closed PRs (2):**
- [#45728](https://github.com/NousResearch/hermes-agent/pull/45728) — **[fix]** (salvage of #27829) `target_model` now correctly drives Bedrock `api_mode` routing between AnthropicBedrock SDK and Converse API. A regression test was added. (Author: Bartok9)
- [#45464](https://github.com/NousResearch/hermes-agent/pull/45464) — **[feat]** Fully wires `kimi-k2.7-code` across provider lists, setup flows, and coding plan model selection. (Author: SonusCap)

**Closed Issues (6):**
- [#501](https://github.com/NousResearch/hermes-agent/issues/501) — **[Feature]** Web UI Gateway — Local Browser-Based Interface. *(Closed, likely implemented or superseded)*
- [#44927](https://github.com/NousResearch/hermes-agent/issues/44927) — **[Feature]** Add streaming auto-follow as an opt-in setting. *(Closed as duplicate)*
- [#42454](https://github.com/NousResearch/hermes-agent/issues/42454) — **[Bug]** Photon (iMessage) plugin unusable due to broken Spectrum Cloud host. *(Closed)*
- [#29205](https://github.com/NousResearch/hermes-agent/issues/29205) — **[Bug]** Anthropic fallback fails after Codex empty turns (trailing assistant prefill). *(Closed, likely fixed)*
- [#44942](https://github.com/NousResearch/hermes-agent/issues/44942) — **[Bug]** Skill-update backup handling can corrupt or lose skills. *(Closed)*
- [#45826](https://github.com/NousResearch/hermes-agent/issues/45826) — **[Bug]** macOS file tool tests fail on resolved `/private` paths and config guard precedence. *(Closed)*

## 4. Community Hot Topics

| Issue/PR | Title | Comments | Reactions |
|---|---|---|---|
| [#501](https://github.com/NousResearch/hermes-agent/issues/501) | Web UI Gateway | 14 | 👍1 |
| [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) | Auto Dream – automatic memory consolidation | 8 | 👍5 |
| [#44428](https://github.com/NousResearch/hermes-agent/issues/44428) | Support Telegram Bot API 10.1 Rich Messages | 5 | 👍3 |
| [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) | Context compression interrupted by gateway messages | 5 | 0 |
| [#19344](https://github.com/NousResearch/hermes-agent/issues/19344) | Planning Consultant – model-initiated frontier-model review via /consult | 4 | 0 |
| [#44666](https://github.com/NousResearch/hermes-agent/issues/44666) | `api_key_env` silently ignored in named custom providers | 4 | 0 |

**Analysis:** The community’s strongest demand is for a **local web-based UI** (#501, now closed) and **smarter memory management** (#10771, with 5 👍). Telegram rich messages (#44428) and the ability to consult a more capable model mid-task (#19344) also see active discussion. Configuration friction (API key handling, provider routing) is repeatedly highlighted.

## 5. Bugs & Stability

**Critical / P1:** No open P1 bugs reported today. (A previous P1 - Anthropic fallback #29205 - was closed.)

**High Priority (P2) issues reported in the last 24h:**
- [#44666](https://github.com/NousResearch/hermes-agent/issues/44666) — `api_key_env` silently ignored in custom providers → sends `no-key-required`.
- [#43586](https://github.com/NousResearch/hermes-agent/issues/43586) — `key_env` ignored in `model:` block with bare `provider: custom` → returns 401.
- [#31155](https://github.com/NousResearch/hermes-agent/issues/31155) — `delegation.model` override ignored — subagents always inherit parent model.
- [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) — Context compression fails when gateway message arrives during compression.
- [#42405](https://github.com/NousResearch/hermes-agent/issues/42405) — Memory at capacity → `replace` zero-match retry loop → silent hang.
- [#33907](https://github.com/NousResearch/hermes-agent/issues/33907) — Context compression creates orphan sessions missing from `state.db`.
- [#45783](https://github.com/NousResearch/hermes-agent/issues/45783) — Tool call burst on session resume causes massive credit spikes.
- [#45813](https://github.com/NousResearch/hermes-agent/issues/45813) — GitHub Copilot provider always returns 400 Bad Request.
- [#45674](https://github.com/NousResearch/hermes-agent/issues/45674) — `hermes mcp list` crashes with AttributeError when server entry is a string.
- [#45792](https://github.com/NousResearch/hermes-agent/issues/45792) — Docker container does not understand its environment (mount path mismatch).
- [#45860](https://github.com/NousResearch/hermes-agent/issues/45860) — Three Windows installation bugs (missing `hermes.exe`, update interrupt, etc.)

**Fix PRs available for some bugs:**
- [#45888](https://github.com/NousResearch/hermes-agent/pull/45888) — Wires approval callbacks into Responses API path (fixes gateway blocking).
- [#45919](https://github.com/NousResearch/hermes-agent/pull/45919) — Returns Anthropic-shaped partial stubs on stream death.
- [#45922](https://github.com/NousResearch/hermes-agent/pull/45922) — Shapes partial-stream recovery stub for `anthropic_messages` mode.
- [#45866](https://github.com/NousResearch/hermes-agent/pull/45866) — Native OS notifications (fixes missing notification toggles).
- [#45926](https://github.com/NousResearch/hermes-agent/pull/45926) — Stops thread settle from fighting user scroll (Desktop).
- [#44999](https://github.com/NousResearch/hermes-agent/pull/44999) — Prevents 403 error when switching sessions across profiles.
- [#45900](https://github.com/NousResearch/hermes-agent/pull/45900) — Runs TUI shell exec in session cwd (fixes workspace context).

**Lower Priority (P3) notable bugs:** Desktop auto-scroll (#42366), Matrix thread message loss (#45493), TUI compressed sessions moving to No workspace (#42228), Cron background review blocking read-only tools (#45877), duplicate patch application (#45834), SSH sessions unaware of host-local paths (#45909 fix PR exists).

## 6. Feature Requests & Roadmap Signals

**Most requested features (by volume/reactions):**
- **Web UI Gateway** (#501, closed) – likely already in progress after community demand.
- **Automatic Memory Consolidation (“Auto Dream”)** (#10771, 5 👍) – high interest; likely to be prioritized.
- **Telegram Bot API 10.1 Rich Messages** (#44428, #45864, #45854) – three separate issues/PRs, strong demand. Likely candidate for next minor release.
- **Planning Consultant** (#19344) – model-driven escalation to frontier models – fits project’s flexible provider architecture.
- **Native OS notifications** – PR #45866 already open; likely to be merged soon.
- **hashline mode for file patching** – PR #45627 adds content-hash-anchored line editing to reduce stale-view failures.
- **Provider account removal** – PR #45910 adds remove action for connected provider accounts.

**Incremental improvements:**
- Streaming auto-follow toggle (duplicate of #501/UI work).
- MCP server listing robustness (#45674 fix).
- Cron job read-only tool allowlist (#45877).

**Predictions for next release (v0.x.x):**
- Telegram rich message support (merging one or more PRs).
- Memory consolidation auto-dream feature (if #10771 is implemented).
- Bedrock provider routing fixes already landed (#45728).
- Desktop native notifications and auto-scroll fixes.
- Configuration key_env and api_key_env alignment.

## 7. User Feedback Summary

**Pain Points (frequently mentioned):**
- **Config friction:** API key handling (`api_key_env` vs `key_env`) is confusing and silent failures (401 errors) waste time.
- **Context compression unreliability:** Interruptions from gateway messages, orphan sessions, retry loops on memory replace.
- **Delegation model override ignored:** Users wanting to run subagents on cheaper models cannot configure that separately.
- **Desktop/TUI usability:** No auto-scroll during streaming, missing scrollbar in workspace selector, input prompt disappears.
- **Windows installation:** Multiple bugs after interrupted updates (missing exe, broken venv).
- **Docker environment:** Config mounted to container not recognized as valid.
- **Credit spikes:** Resuming sessions replays tool call bursts, causing unexpected costs.

**Satisfaction signals:**
- Active community contributions (43+ open PRs from user AIalliAI, many feature PRs).
- Quick closing of high-profile bugs (Anthropic fallback, Photon plugin).
- High engagement on Telegram and memory features indicates users value rich platform integration.

**Use cases highlighted:**
- Legal text analysis with custom reasoning evaluation engines (ThinkCheck integration, #22417).
- Running cost-effective models with fallback to frontier models for complex tasks (#19344).
- Using Hermes as a multi-platform assistant (Telegram, WhatsApp, Matrix, Desktop).

## 8. Backlog Watch

| Issue/PR | Created | Updated | Comments | Priority | Concern |
|---|---|---|---|---|---|
| [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) | 2026-04-16 | 2026-06-13 | 8 | P3 | Highly requested feature (5 👍) with no maintainer response for nearly 2 months. |
| [#19245](https://github.com/NousResearch/hermes-agent/issues/19245) | 2026-05-03 | 2026-06-13 | 2 | P2 | Orphaned session JSON not recovered after crash – P2 unaddressed for 6 weeks. |
| [#31155](https://github.com/NousResearch/hermes-agent/issues/31155) | 2026-05-23 | 2026-06-14 | 3 | P2 | Delegation model override ignored – reported 3 weeks ago, no maintainer comment. |
| [#33907](https://github.com/NousResearch/hermes-agent/issues/33907) | 2026-05-28 | 2026-06-13 | 2 | P2 | Context compression creates orphan sessions missing from state.db – 17 days old. |
| [#42228](https://github.com/NousResearch/hermes-agent/issues/42228) | 2026-06-08 | 2026-06-13 | 2 | P3 | TUI sessions move to No workspace after compression – reported 6 days ago, no response. |
| [#40739](https://github.com/NousResearch/hermes-agent/pull/40739) | 2026-06-06 | 2026-06-14 | 0 | P3 | Linear gateway integration PR open 8 days without review. |

**Maintainer attention needed:** The backlog of P2 issues exceeding two weeks without a maintainer reply (especially #10771, #19245, #31155) risks user frustration. The 48 open PRs also suggest a review bottleneck – automated or community-review processes may be required to sustain momentum.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-14

## 1. Today's Overview
PicoClaw shows moderate-to-high activity with **2 issues** and **7 pull requests** updated in the last 24 hours, plus a nightly release. The project continues to address both bug reports and feature development at a steady pace. Five PRs were merged or closed, covering documentation (Traditional Chinese i18n), linter fixes for error handling, TTS fallback support, and a critical fix for image hallucination in non-vision models. Two open PRs (image compression and remote WebSocket mode) signal ongoing feature work. The single open bug (continuous token consumption) remains under investigation.

## 2. Releases
A new **nightly build** was published:  
[`v0.2.9-nightly.20260614.cf67dd38`](https://github.com/sipeed/picoclaw/releases/tag/nightly)  
- **Type**: Automated nightly (unstable)  
- **Changelog**: [Full diff](https://github.com/sipeed/picoclaw/compare/v0.2.9...main) (includes all changes merged to `main` up to today)  
- **Breaking changes**: None noted.  
- **Migration notes**: Not required for nightly builds; caution advised for production use.

## 3. Project Progress
Five PRs were merged or closed today, advancing stability and features:

| PR | Status | Description |
|----|--------|-------------|
| [#2935](https://github.com/sipeed/picoclaw/pull/2935) | **Merged** | **i18n:** Added Traditional Chinese (zh-TW) locale and READMEs for docs and frontend. |
| [#3065](https://github.com/sipeed/picoclaw/pull/3065) | **Merged** | **fix(seahorse):** Explicitly ignore `Close()` errors on PRAGMA/migration failure paths to resolve linter warnings. |
| [#3066](https://github.com/sipeed/picoclaw/pull/3066) | **Merged** | **fix:** Explicitly ignore `tmpFile.Close()` errors on temp file write/sync failures (three locations). |
| [#3119](https://github.com/sipeed/picoclaw/pull/3119) | **Merged** | **fix(tts):** Support OpenRouter voice overrides (`extra_body`) and automatic fallback when `response_format` is rejected. |
| [#3117](https://github.com/sipeed/picoclaw/pull/3117) | **Merged** | **fix(agent):** Route media turns and `load_image` follow-ups to the configured image model, fixing hallucination bug (#3108). Also embeds onboarding workspace from `workspace/` directory. |

**Open PRs still in progress** (updated today):
- [#2964](https://github.com/sipeed/picoclaw/pull/2964) — **Feat/image input compression**: Adds configurable multi-level compression for inbound images (vision pipeline).
- [#3118](https://github.com/sipeed/picoclaw/pull/3118) — **Feat: remote Pico WebSocket mode**: Extends `picoclaw agent` with `--remote` flag for connecting to a remote WebSocket endpoint.

## 4. Community Hot Topics
The most active discussion this week centers on **continuous token consumption**:

- **[#3012 – [BUG] Continuous consumption of tokens every minutes when evolution is enabled](https://github.com/sipeed/picoclaw/issues/3012)** (3 comments, open) – User `xpader` reports that enabling Evolution (Draft mode, Code Path Trigger) causes steady token usage every minute on FreeBSD with MiniMax. The issue has been open for 9 days and is the only active bug with community discussion. No resolution yet.

- **Related fix**: [#3117](https://github.com/sipeed/picoclaw/pull/3117) fixes the image hallucination bug reported in [#3108](https://github.com/sipeed/picoclaw/issues/3108) (closed, 0 comments). This fix was well received as it directly addresses a user-reported problem when using text-only models via OpenRouter.

## 5. Bugs & Stability
Two bugs were handled today:

| Issue | Severity | Status | Notes |
|-------|----------|--------|-------|
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) — Token consumption every minute with Evolution | **High** – could rapidly exhaust API budgets | **Open** | No fix PR yet; maintainers may need to investigate the Evolution Draft mode's polling logic. |
| [#3108](https://github.com/sipeed/picoclaw/issues/3108) — Image description hallucination when model lacks vision | **Medium** – incorrect answers, but non‑crashing | **Closed** | Fixed by [#3117](https://github.com/sipeed/picoclaw/pull/3117) (merged today). The fix routes image turns to the configured vision model. |

Additionally, three linter‑level warnings (ignored `Close()` errors) were resolved in PRs [#3065](https://github.com/sipeed/picoclaw/pull/3065) and [#3066](https://github.com/sipeed/picoclaw/pull/3066). No new crashes or regressions reported.

## 6. Feature Requests & Roadmap Signals
Two significant features are in active development:

- **Image input compression** ([#2964](https://github.com/sipeed/picoclaw/pull/2964)) – Configurable multi‑level compression before building model payloads. Expected to reduce bandwidth/API costs and improve processing speed for vision tasks. Likely to land in the next minor release (v0.3.0).

- **Remote WebSocket agent mode** ([#3118](https://github.com/sipeed/picoclaw/pull/3118)) – Allows `picoclaw agent` to connect to a remote PicoClaw instance via WebSocket, enabling remote control and headless deployment. Growing community interest in distributed agent architectures.

- **i18n expansion** ([#2935](https://github.com/sipeed/picoclaw/pull/2935)) – Traditional Chinese support was merged today, indicating continued investment in internationalization for broader adoption.

**Prediction for next version**: Both #2964 and #3118 are strong candidates for inclusion in v0.3.0 along with the TTS flexibility improvements from #3119.

## 7. User Feedback Summary
Key pain points expressed in today’s issues and PR comments:

- **Token waste (Evolution mode)**: User `xpader` describes a scenario where tokens are consumed every minute without generating any visible output. Frustration is implicit; the bug impacts cost predictability.
- **Model capability mismatch**: User `afjcjsbx` reported that PicoClaw incorrectly attempted to describe an image using a text‑only model (`deepseek/deepseek-v4-flash`), producing hallucinated results. The fix (#3117) has been positively received.
- **Growing demand for remote operation**: The new remote WebSocket mode (#3118) addresses a common request from developers wanting to run PicoClaw agents on separate servers or edge devices.

Overall community satisfaction appears stable, with quick turnaround on reported bugs (hallucination fixed in 2 days). The token consumption issue remains the primary dissatisfaction point.

## 8. Backlog Watch
No long‑unanswered issues or PRs were identified in today’s data. However, two items may require continued maintainer attention:

- **[#3012 – Token consumption bug](https://github.com/sipeed/picoclaw/issues/3012)** – Open for 9 days with no fix PR. Should be prioritized to prevent user churn.
- **[#2964 – Image compression feature PR](https://github.com/sipeed/picoclaw/pull/2964)** – Open since 2026-05-28 (17 days). No recent comments from maintainers; may need review to keep momentum.

All other open items (e.g., #3118) are recent and actively being discussed.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-14

## 1. Today's Overview

Activity is moderate, with six pull requests updated in the last 24 hours—four merged/closed and two open. The only updated issue was a self-deleted post (posted in error), so no user-reported bugs or feature requests entered the tracker today. The merged PRs indicate steady feature progress in provider capabilities, credential management, and memory scaffolding. Both open PRs focus on reliability: one hardens container lifecycle handling following a multi-agent health audit, the other fixes two long-standing data loss bugs from container kills. No new releases were published.

## 2. Releases

No new releases today.

## 3. Project Progress

Four pull requests were merged or closed today, advancing core infrastructure:

- **#2754 – `feat(runner): onExchangeComplete provider hook + slash-command interruption`** (merged)  
  Adds an optional `onExchangeComplete` hook and a slash-command interruption mechanism for agent-runner providers.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2754)

- **#2747 – `feat(onecli): SDK 2.2.1 — credential-stub mounts + machine-checkable pins`** (merged)  
  Bumps `@onecli-sh/sdk` from 0.5.0 to 2.2.1, introduces credential-stub mounts for provider containers and machine-checkable pin verification.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2747)

- **#2746 – `feat(providers): agent-surfaces capability seam`** (merged)  
  Adds a host-side registry where providers declare capabilities, enabling the host to query provider affordances before dispatching tasks.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2746)

- **#2745 – `feat(memory): opt-in persistent memory scaffold for providers`** (merged)  
  Introduces a `usesMemoryScaffold` capability and a container-mount contract for providers that wish to persist structured memory across restarts.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2745)

## 4. Community Hot Topics

No issues or PRs attracted comments or reactions today. The only activity of note is the two open PRs, which are fresh enough that community discussion may still be developing:

- **#2750** (open) – Fix for stale `outbound.db` journals after container kills; cracks two related failure modes (#2516, #2640). Likely to draw interest from users experiencing data loss.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2750)

- **#2732** (open) – Harden host and agent-runner from a multi-agent health audit; touches bind-mounts, crash loops, and circuit breakers. Could be a high-impact stability improvement.  
  [Link](https://github.com/nanocoai/nanoclaw/pull/2732)

## 5. Bugs & Stability

Two bugs are directly addressed but not closed yet:

- **Stale `outbound.db` journals after container SIGKILL** (Severity: High) – Reported in #2516 and #2640. The fix in #2750 is open and ready for review.  
  [Issue #2516](https://github.com/nanocoai/nanoclaw/issues/2516), [Issue #2640](https://github.com/nanocoai/nanoclaw/issues/2640)

- **Container lifecycle failures from health audit** (Severity: Medium) – Includes Docker Desktop drvfs staging crash-loop (exit 127) and missing `MAX_CONCURRENT_CONTAINERS` enforcement. Addressed by open PR #2732.  
  [PR #2732](https://github.com/nanocoai/nanoclaw/pull/2732)

No new bugs or crashes were filed today. The self-deleted issue #2755 was a user error.

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. However, the set of merged PRs provides strong signals for the next release:

- **Persistent memory scaffold** (#2745) – Providers can now opt into structured, container-mountable memory. Likely to be included in the next minor version.
- **Agent-surfaces capability seam** (#2746) – Allows the host to dynamically learn provider capabilities. This foundational feature will enable smarter dispatch and integration.
- **SDK 2.2.1 with credential-stub mounts** (#2747) – Paves the way for secure credential handling inside provider containers.
- **`onExchangeComplete` hook** (#2754) – Enables providers to act after an exchange finishes, useful for telemetry, logging, or side effects.

These features together suggest the next version may focus on **provider extensibility, security, and resilience**.

## 7. User Feedback Summary

No direct user feedback (comments, reactions, or new issues) was recorded today. The only user interaction was a self-deleted issue (#2755) posted in error.

## 8. Backlog Watch

No unaddressed important issues or stale PRs were identified in the data provided. The two open PRs (#2750, #2732) are from core contributors and have been updated within the last 24 hours, so they are actively maintained. No long-unanswered items require attention.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-06-14

## Today’s Overview
No new releases were published in the last 24 hours. Two open issues were updated, and one open pull request received activity. The project remains stable with no merged or closed PRs today. Community attention is focused on a critical bug where agent‑type scheduled jobs silently fail to deliver messages (Issue #941) and a proposed fix (PR #954). A feature request for JIRA integration (Issue #914) also received an update. Overall activity is moderate, with the core team addressing a use‑after‑free defect that affects message delivery reliability.

## Releases
*None – no new versions were released in this period.*

## Project Progress
- **Merged/Closed PRs today:** 0  
  No pull requests were merged or closed in the last 24 hours.

## Community Hot Topics
- **Issue #941 – Agent‑type cron jobs don’t spawn a subprocess (7 comments)**  
  [Link](nullclaw/nullclaw Issue #941)  
  The user reports that scheduled tasks with `job_type: "agent"` and `delivery_channel: "telegram"` are marked completed but never actually start the agent process. The thread has attracted the most comments and reactions this week, highlighting a clear pain point in message delivery reliability.

- **PR #954 – Fix for use‑after‑free in OutboundMessage.channel (related to #941)**  
  [Link](nullclaw/nullclaw PR #954)  
  Submitted 2026‑06‑13, this PR directly addresses the root cause of Issue #941: a use‑after‑free bug on `OutboundMessage.channel` that prevents any channel delivery for one‑shot cron jobs. The fix is awaiting review.

## Bugs & Stability
- **Critical Bug: Scheduled agent jobs silently fail to deliver messages**  
  *Issue #941* – Affects all delivery channels (Telegram, Mattermost, etc.) when using `job_type: "agent"` with `delivery_mode: "always"`. The job runs but the agent subprocess is never spawned, and no message is sent. Severity: **High** – users lose confidence in scheduled task execution.  
  A fix PR (#954) is open and under review.

- No other bugs, crashes, or regressions were reported in the last 24 hours.

## Feature Requests & Roadmap Signals
- **JIRA Access Tool (Issue #914)** – Created 2026‑05‑13, last updated 2026‑06‑13.  
  Requests a new tool to authenticate with JIRA and perform operations like reading issues, creating tickets, updating statuses, and adding comments. This is a medium‑complexity integration that could expand NullClaw’s project management capabilities. Given the lack of maintainer response (only 1 comment), it may not be prioritized in the next release unless community interest grows.

## User Feedback Summary
- **Pain Points:**  
  - Silent failures in scheduled agent jobs (#941) – users cannot trust cron‑style deliveries without explicit log or message confirmation.  
  - Need for JIRA integration to streamline workflow automation (#914).  
- **Satisfaction:** No explicitly positive feedback was captured in the data. The focus remains on fixing a blocking bug.  
- **Use Cases:** Teams using NullClaw for automatic alerting (Telegram) and project management (JIRA) are currently impacted.

## Backlog Watch
- **Issue #941** – High priority bug with an open fix PR. No further maintainer action needed beyond reviewing #954.  
- **Issue #914** – Open since 2026‑05‑13 with only one comment and no official response. This feature request may be at risk of becoming stale. Maintainer attention is recommended to confirm whether the JIRA tool aligns with the roadmap or to request additional details.  
- **PR #954** – Awaiting maintainer review; delaying a resolution for the critical bug in #941.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-14

## Today’s Overview
Activity remains high with **22 pull requests updated in the last 24 hours** (17 open, 5 merged/closed) and **2 open issues refreshed**. The project is deep in two major threads: the **attachment framework (#4644)** – five core PRs merged today – and a concentrated **Slack reliability push** targeting the re-approval loop, credential order, and gate delivery bugs. No new releases were published. The nightly E2E pipeline remains broken (#4108) and is the most significant open stability concern.

## Releases
**None.** No new versions were cut in the last 24 hours.

## Project Progress
Five pull requests were merged/closed today, all part of the **attachment infrastructure (#4644)**:

- **#4654** (closed) – `feat(common): extensible attachment format registry` — unified format definition replacing scattered hardcoded lists.  
  URL: nearai/ironclaw PR #4654

- **#4655** (closed) – `feat(threads): carry attachment refs through the Reborn transcript contract` — transcripts now persist attachment references (never bytes) so uploads survive `accept → persist`.  
  URL: nearai/ironclaw PR #4655

- **#4668** (closed) – `feat(attachments): MountView-based attachment landing crate` — byte-storage foundation for inbound attachments.  
  URL: nearai/ironclaw PR #4668

- **#4670** (closed) – `feat(attachments): bridge inbound bytes into transcript AttachmentRefs` — reusable unit for turning raw bytes into durable `AttachmentRef`s.  
  URL: nearai/ironclaw PR #4670

- **#4672** (closed) – `feat(reborn): accept inline attachment uploads on the WebChat v2 send path` — end-to-end ingress wiring for browser-based file uploads.  
  URL: nearai/ironclaw PR #4672

These five PRs close the core backend tracks of the attachment feature, enabling persistent document uploads through transcript lifecycle.

## Community Hot Topics
The following issues and pull requests attracted the most attention (by size, scope, and number of related sub-PRs):

- **#4845 (new issue)** – *Extract shared resume-authority head across resume_json / auth_resume_json*. Opened today with zero comments, but targets foundational deduplication of capability-resume logic.  
  URL: nearai/ironclaw Issue #4845

- **#4839 (open PR)** – *fix: preserve invocation identity across auth-gate re-dispatch (Slack re-approval loop)*. Large (XL) change to stop consecutive approval requests on reborn capabilities requiring both approval and OAuth.  
  URL: nearai/ironclaw PR #4839

- **#4838 (open PR)** – *Explicit gate-open feedback for busy threads (no parking)*. Replaces a deferred re-submission approach with direct rejection notices, making the user the retry actor.  
  URL: nearai/ironclaw PR #4838

- **#4836 (open PR)** – *feat(runtime-context): surface connected channels, delivery state, and run origin*. Gives the model visibility into channel connectivity and outbound delivery state every loop start.  
  URL: nearai/ironclaw PR #4836

- **#4841 (open PR)** – *reborn: no run-borking failures — failure explanation + retryable failed runs*. Eliminates opaque terminal errors in the reborn binary, adding recovery paths and human-readable explanations.  
  URL: nearai/ironclaw PR #4841

The underlying need is clear: **Slack UX is fragile** – approval loops, missing credential order, and opaque failures frustrate users. The core team is investing heavily in both detection and recovery.

## Bugs & Stability
| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| 🔴 High | #4108 | Nightly E2E scheduled run has been failing since 2026-05-27, last updated 2026-06-13. No associated fix PR. | Open, unattended |
| 🟡 Medium | #4839 | Slack re-approval loop – repeated approval gates for one logical call. | Open, fix PR active |
| 🟡 Medium | #4840 | Missing-credential auth gate appears *after* the approval gate, causing wasted user approvals. | Open, fix PR |
| 🟡 Medium | #4843 | Single-flight gate delivery per run_id – resolution ack can be fanned out multiple times leading to duplication. | Open, fix PR |
| 🟡 Medium | #4844 | Gate route filtering used incorrect `fn(&GateRef)` instead of `fn(&str)` causing allocation overhead and potentially wrong match. | Open, fix PR |
| 🟢 Low | #4838 | Busy-thread parking replaced with explicit rejection – design choice, not a defect. | Open (replaces #4812) |

The most critical open bug is **#4108** (nightly E2E failure) – no resolution yet.

## Feature Requests & Roadmap Signals
- **Attachment support (#4644)** – The five merged PRs today complete the backend pipeline; remaining frontend work (#4738, #4777) and extraction (#4675, #4676) are in progress. Likely to ship in next version.
- **Routine creation endpoint** (#4264) – Adds `POST /api/routines` to the web gateway; open since 2026-05-31.
- **Slack connected state persistence** (#4777) – Fixes WebUI treating Slack as always disconnected; open.
- **Outbound delivery targeting** (#4780) – Adds model-visible guidance for channel selection before routine/trigger creation.
- **QA-trace recorder fix** (#4842) – Makes QA-trace work with auth gates instead of hanging.

Predictions for next version: attachment upload in WebChat, Slack stability fixes (loop + credential order), runtime-context model visibility, and the routine API endpoint.

## User Feedback Summary
While direct user comments are not captured, the PR descriptions reveal clear pain points from this period:

- **Slack reconnect loop** – Users saw four consecutive approval gates for a single action; UX described as “frustrating.”
- **Missing-credential order** – “A human approved an action that could not yet run; the approval was then burned by the auth bounce.”
- **Opaque failures** – “run-borking” terminal errors with no recovery path or explanation.
- **Busy-thread handling** – Previous defer-and-drain approach was confusing; users now get explicit rejection + retry prompt.

Satisfaction signals: the attachment feature is moving fast, and the Slack fix PRs (#4839, #4840, #4843, #4844) directly address user-facing bugs.

## Backlog Watch
| Item | Age | Status | Reason for Attention |
|------|-----|--------|----------------------|
| **#4108** – Nightly E2E failed | Created 2026-05-27, last updated 2026-06-13 | Open, no fix PR | Continuous pipeline failure affecting all merges; no maintainer response. |
| **#4264** – Routine create endpoint | Created 2026-05-31, updated 2026-06-13 | Open, awaiting review | Feature request with no movement; scoped as `new` contributor. |
| **#3708** – chore: release | Created 2026-05-16, updated 2026-06-14 | Open, 9 packages awaiting release | Blocking API breaking changes (`ironclaw_common` 0.4.2→0.5.0, `ironclaw_skills` 0.3.0→0.4.0); stale despite frequent updates. |

**Maintainer attention needed** on the nightly E2E failure (#4108) – it is the highest-priority unaddressed item – and the release PR (#3708) to prevent further drift between merged features and published versions.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-14

## 1. Today's Overview
Activity over the past 24 hours remained low, with 4 open issues and 5 pull requests updated — all created in early April and only now seeing notes or comments. No new releases were published, and no maintainer feedback was observed on stale items. The project appears to be in a maintenance phase, with the community waiting for resolutions on several open bugs and feature requests.

## 2. Releases
**None** — no new versions were tagged or released in the last 24 hours.

## 3. Project Progress
Two pull requests were closed (merged) today, both addressing frontend usability issues:

- **[PR #1466] fix(mcp): modal close button unreachable when content grows tall**  
  Closed/merged. Fixes a layout bug where the MCP server form modal’s Cancel button scrolled out of view when many environment variables were added.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1466)

- **[PR #1467] fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS**  
  Closed/merged. Corrects keyboard shortcut labels in Settings > Shortcuts to show platform‑appropriate modifier keys on macOS.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1467)

Three other PRs remain open and stale (#1440, #1441, #1445), awaiting review.

## 4. Community Hot Topics
The only issue with more than one comment is:

- **[Issue #1443] – 有计划支持新版本的openclaw吗？**  
  → 2 comments, created 2026‑04‑03, last updated 2026‑06‑13  
  User asks whether the project will support the new version of OpenCLaw, which introduced breaking changes. No official response yet.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1443)

All other open issues have only one comment each, indicating low community engagement or unresolved blockers.

## 5. Bugs & Stability
**High severity** (functional blocker or misbehavior):

- **[Issue #1437] – 创建定时任务时，计划选择不重复，清空日历，点击【创建任务】按钮没反应**  
  UI button does not respond when creating a non‑repeating task after clearing the calendar. No error feedback.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1437)

- **[Issue #1439] – 上传技能已停用，对话中仍然可以调用**  
  Disabled skills are still invocable during conversation — a logic/authorization bug.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1439)

- **[Issue #1443] – OpenCLaw v2026.3.24 compatibility**  
  Breaking change prevents the project from starting after upgrade. Blocks users who need the new version.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1443)

**Medium severity** (UX confusion):

- **[Issue #1442] – Agent添加技能，对话后引用的技能不展示**  
  Selected skills disappear from the UI after the first conversation turn; reappear only after switching agents. User questions the intended behavior.  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1442)

**Fix PRs in progress**:  
- **PR #1445** addresses skill duplication and zip import directory name issues, which relate to #1439 and #1442.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1445)

## 6. Feature Requests & Roadmap Signals
Two notable features are visible in the open PRs and issues:

- **OpenCLaw compatibility** (#1443) – user request for support of the latest OpenCLaw release. Given the breaking change, this is a high‑priority integration task that may appear in the next version.

- **Extensible preview pipeline** (PR #1441) – adds support for HTML, React, and Mermaid previews in Cowork sessions. This is a significant UX enhancement. If merged, it will likely be part of the next minor release.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1441)

- **Skill UI improvements** (PR #1440) – moves skill badges from the bottom toolbar to the top of the input area to reduce clutter. Already submitted but not yet merged.  
  [Link](https://github.com/netease-youdao/LobsterAI/pull/1440)

## 7. User Feedback Summary
Real user pain points reported in the last 24 hours (all from stale issues):

- **UI responsiveness failures** – the “Create Task” button does not work in certain configurations, with no error message.
- **Skill lifecycle bugs** – disabled skills remain callable; selected skills disappear after conversation.
- **Upgrade blocking** – the latest OpenCLaw breaking change prevents the project from running.
- **Import confusion** – skills imported via zip or GitHub can duplicate silently, causing system prompt pollution (addressed in PR #1445).
- **Agent skill selection unclear** – users don’t understand whether skills are supposed to be enforced or only suggested.

Overall sentiment is one of frustration due to unresolved issues and lack of maintainer responses.

## 8. Backlog Watch
The following items have been open since April 3, 2026, and have not received any maintainer reply or assignment:

- **Issue #1443** – OpenCLaw compatibility  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1443)

- **Issue #1437** – Task creation button broken  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1437)

- **Issue #1439** – Disabled skills usable  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1439)

- **Issue #1442** – Skill display after agent conversation  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1442)

Additionally, three pull requests (#1440, #1441, #1445) remain open without review comments since early April. These represent substantial feature work and critical bug fixes that should be evaluated promptly to avoid further community disengagement.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-14

---

## Today's Overview

Activity is moderate, with **3 pull requests** and **1 issue** updated in the last 24 hours. All PRs remain open, and no releases or merges occurred today. The project is actively addressing a significant OAuth integration bug (Issue #1119) that affects popular MCP servers like Notion and Linear, with a corresponding fix PR (#1120) already submitted. A Dockerfile improvement (PR #1122) and a routine dependency bump (PR #1121) round out today’s contributions. Overall, the project appears healthy but in a focused bug-fix phase.

---

## Releases

- **No new releases** in the last 24 hours. The latest available version remains unchanged.

---

## Project Progress

No PRs were merged or closed today. However, three open PRs represent active work:

- **PR #1120** (`fix(mcp): use direct fetch for resource_metadata URL from WWW-Authenticate`) – Directly addresses the OAuth bug reported in Issue #1119, providing a fix for servers that include `resource_metadata` in their `WWW-Authenticate` header. [View PR](https://github.com/moltis-org/moltis/pull/1120)

- **PR #1122** (`fix: drop VOLUME declarations that shadow the home bind mount`) – Fixes a Dockerfile issue where declared `VOLUME` paths could interfere with home directory bind mounts, a pathological case for deployments that mount the whole home directory. [View PR](https://github.com/moltis-org/moltis/pull/1122)

- **PR #1121** (`chore(deps-dev): bump esbuild from 0.25.12 to 0.28.1`) – Routine dependency update for the web UI crate. [View PR](https://github.com/moltis-org/moltis/pull/1121)

---

## Community Hot Topics

The only active issue, **#1119** – *[Bug]: MCP OAuth fails with `invalid_target` for servers using `resource_metadata`* – is the main community focus. Authored by `xzavrel`, it details a failure when adding remote MCP servers (Notion, Linear) that require OAuth with a `resource_metadata` parameter. The browser displays a JSON error, blocking the authorization flow. The issue has **1 comment** but no reactions yet. The fix PR (#1120) was also submitted by the same author, indicating active collaboration.

- **Issue #1119**: [Link](https://github.com/moltis-org/moltis/issues/1119)
- **PR #1120**: [Link](https://github.com/moltis-org/moltis/pull/1120)

**Underlying need**: Users of popular external MCP services are unable to complete OAuth authentication, which is a critical integration point. The community is pushing for a prompt resolution, and the maintainers have responded quickly with a fix proposal.

---

## Bugs & Stability

| Issue | Severity | Status | Notes |
|-------|----------|--------|-------|
| **#1119** – MCP OAuth `invalid_target` with `resource_metadata` | **High** – Blocks OAuth login for Notion, Linear, etc. | Open – fix PR #1120 exists | Affects a core integration feature; impact is broad for users of those servers. |

No other bugs or regressions were reported in the last 24 hours. The existing bug has a targeted fix in review, lowering risk of prolonged instability.

---

## Feature Requests & Roadmap Signals

- **OAuth compatibility for `resource_metadata`**: The bug fix (PR #1120) signals that the project is moving toward more robust MCP OAuth support. This may become a standard part of the authentication flow in the next release.
- **Docker deployment robustness**: PR #1122 improves Docker volume handling, suggesting ongoing care for containerized deployments – a likely feature for users running Moltis via Docker.

No explicit feature requests were filed today, but the community’s need for broader MCP server compatibility is clear. The next version will probably include the OAuth fix and the Docker improvement.

---

## User Feedback Summary

- **Pain point**: The OAuth flow fails silently for well-known MCP servers, requiring manual workarounds. The issue author provided detailed context, demonstrating a strong desire for seamless integration.
- **Satisfaction**: The quick submission of a fix PR by the same user (and its prompt review) suggests a responsive maintainer community, which tends to improve user satisfaction.
- **Use case**: Users are integrating Moltis with external productivity tools (Notion, Linear) – a key use case for an AI personal assistant. Resolving OAuth will likely unblock many real-world workflows.

---

## Backlog Watch

No long-unanswered issues or PRs require immediate maintainer attention today. The most time-sensitive items (#1119 and #1120) are already being handled. PR #1122 has been open for less than 24 hours and has no comments yet; maintainers should review it soon to avoid Docker deployment regressions.

- **Needs review**: PR #1122 (Docker VOLUME fix) – no comments yet, but it addresses a potentially breaking deployment scenario.
- **All other items** are either recent or have active engagement.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-14

## Today’s Overview
CoPaw shows moderate activity with **8 issues** and **8 pull requests** updated in the last 24 hours. One issue was closed and two PRs were merged, while the remaining open items reflect a mix of bug reports and feature requests. No new releases were published. The project is actively addressing edge‑case bugs (mostly via first‑time contributor PRs) and gathering community input for new integrations and localisation. Overall health is stable, though the open issue count (7 active) suggests ongoing user friction points that maintainers are likely to prioritise.

## Releases
*None.* No new versions were shipped this week.

## Project Progress
Two PRs were merged/closed in the last day, moving both fixes and features forward:

- **#2498** *fix(agents): use console language when creating agent and fallback unsupported langs*  
  Merged on 2026‑06‑13. Previously, new agents always defaulted to English and copied Chinese persona files regardless of the user’s UI language. Now the creation process reads the console’s language and provides server‑side fallback for unsupported languages.

- **#4969** *feat(skill): Add skill tag batch download*  
  Merged on 2026‑06‑13. The skill batch download feature now supports tag‑based filtering, addressing the long‑standing request #2961.

These merges indicate that the team is focusing on both usability polish (language consistency) and feature completeness (skill management).

## Community Hot Topics
The most engaging discussions revolve around integration gaps and performance issues:

- **#5156** *[Feature]: 建议支持 kimi-for-coding / 加入 uv 白名单* (4 comments)  
  Users who subscribe to Kimi coding want to use its API inside CoPaw. The current Kimi integration only supports the official API, leaving paying subscribers unable to leverage their existing plan. This request also asks for adding `uv` (a Python package manager) to the tool whitelist.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5156)

- **#5047** *[Question]: Windows Tauri 桌面端启动特别慢* (3 comments)  
  After switching from Python packaging to Tauri, startup times have increased from 1–2 minutes to over 10 minutes, often resulting in unresponsive states. Users report the issue persists across versions 1.1.10 and 1.1.11b1 on Windows 11.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5047)

These issues reflect a clear user desire for better platform integration (Kimi, local tools) and smoother desktop experience.

## Bugs & Stability
Three new bugs were opened today, each with moderate to high severity:

- **#5172** *[Bug]: 聊天总出现问完问题没反应一直等待* (Closed)  
  After idle periods, the chat stops responding to new queries. Only clicking “Stop” (which raises `Task has been cancelled!`) and re‑asking fixes it. The bug is especially critical for channel‑connected bots (QQ, WeChat) where manual intervention is impossible. Severity: **High** – impacts core conversational capability.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5172)

- **#5171** *[Bug]: 上下文压缩保留缺少按条数保留或排除人设文件* (Open)  
  When a character‑profile (`PROFILE.md`) exceeds the token‑retention threshold, context compression can reduce the conversation to zero tokens, completely losing the agent’s memory and breaking ongoing tasks. Severity: **High** – causes total session failure.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5171)

- **#5174** *[Bug]: 定时任务和心跳机制的缺陷是吗？* (Open)  
  Cron agents can run Python scripts but cannot produce knowledge files (no `write_file`, no `spawn_subagent`). The heartbeat agent, despite being a separate instance, also fails to execute knowledge‑intensive tasks. Severity: **Medium** – restricts automation workflows.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5174)

Additionally, a long‑standing startup‑speed issue (#5047) remains open.

**Fix PRs in progress:** Several first‑time‑contributor PRs (all still under review) address related edge cases:
- #5035 – llama.cpp version parsing with fixed‑width slice (will break at build #10000).
- #5037 – empty `Exec=` line in Linux browser detection.
- #5038 – empty message list in context manager.
- #5040 – malformed `jobs.json` crashing cron.
- #5041 – unreadable files aborting backup.

These PRs show the community is actively helping harden the codebase.

## Feature Requests & Roadmap Signals
New feature ideas continue to surface, many focused on regional expansion and tool flexibility:

- **#5169** *Add Vietnamese (vi) interface language* – follows the pattern of Indonesian (#4219) and Brazilian Portuguese language additions. Likely to be accepted in a future release.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5169)

- **#5168** *Add official Zalo Bot channel support* – Zalo is dominant in Vietnam; this request would open CoPaw to a large user base.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/5168)

- **#5156** *Support kimi-for-coding / uv whitelist* – integrational need already discussed above.

- **#5170** *perf(agents): cache PROFILE.md reads on agent‑list endpoint* (PR, not merged yet) – a performance improvement that could reduce latency for users with many agents.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/5170)

Predictably, **Vietnamese localisation** (#5169) has the highest chance of landing soon, given the precedent of similar past additions. The **Zalo channel** (#5168) may take longer as it requires a new channel provider.

## User Feedback Summary
Real user pain points captured today:

- **Desktop startup time** remains a top frustration – multiple users confirm the Tauri switch made things worse, with waiting times of several minutes.
- **Chat freezes after idle** – a critical reliability bug that breaks trust, especially for unattended bots.
- **Context compression failures** – power‑users who rely on long‑running agent conversations lose all context when the profile token limit is hit.
- **Integration gaps** – paying users of Kimi coding feel locked out; Vietnamese and Vietnamese‑platform users ask for native support.
- **Automation limitations** – cron and heartbeat agents cannot produce files, limiting their utility for scheduled knowledge‑work.

Overall, users are enthusiastic about CoPaw’s potential but frustrated by stability and performance regressions.

## Backlog Watch
The following items remain open without maintainer response or clear timeline:

- **#5047** *Windows Tauri slow startup* (open since June 9) – no official acknowledgment in the issue thread.
- **#5156** *kimi-for-coding / uv whitelist* (open since June 12) – no maintainer comment yet.
- **PRs #5035, #5037, #5038, #5040, #5041** – all first‑time‑contributor fixes, labelled “Under Review” since June 9. None have been merged or received additional review comments.

These items warrant maintainer attention to avoid contributor frustration and to address critical user feedback.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw Project Digest — 2026-06-14

### 1. Today's Overview
ZeroClaw saw heavy activity over the past 24 hours: **42 issues** were updated (25 open, 17 closed) and **50 pull requests** were updated (41 open, 9 merged/closed). No new releases were published. The community is actively shaping the v0.8.1 milestone, with major RFCs around architecture unification, a native plugin system, and memory consolidation approaching decision points. Several S1 regressions were reported, but quick fix PRs are already in flight, indicating a responsive maintainer team.

### 2. Releases
*None.* No new releases were tagged in the last 24 hours.

### 3. Project Progress
**9 PRs were merged/closed** in the last day. Notable accomplishments:
- **RFC executed: Unify agent turn engines** ([#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) → closed) – the phased migration was replaced by a single consolidation PR ([#7540](https://github.com/zeroclaw-labs/zeroclaw/pull/7540), not listed but referenced).
- **Cron pause/resume** ([#7398](https://github.com/zeroclaw-labs/zeroclaw/pull/7398) → closed) – scheduled tasks can now be toggled without deletion.
- **MCP tool restriction docs gap resolved** ([#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) → closed) – clarified that `risk_profiles.allowed_tools` does not restrict MCP tools (by design).
- **OpenAI provider timeout config fixed** ([#6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723) → closed) – `timeout_secs` now respected by native OpenAI provider.
- **Zerocode UI bugs closed**: Cmd-C quit chord ([#7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378)) and dark theme readability ([#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377)).
- **Quickstart infinite redraw** ([#7507](https://github.com/zeroclaw-labs/zeroclaw/issues/7507) → closed) – fixed non-TTY stdin flooding.
- **Windows test fix** ([#7509](https://github.com/zeroclaw-labs/zeroclaw/issues/7509) → closed) – self-test no longer fails on Windows hosts.

Other merged/closed PRs include minor bugfixes and documentation improvements. No new major features were merged today, but six significant enhancement PRs remain open and under review.

### 4. Community Hot Topics
Issues and PRs attracting the most discussion:

- **[Feature]: Dream Mode – Periodic Memory Consolidation** ([#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)) – 18 comments. The community is deeply interested in offline memory consolidation. A corresponding PR ([#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693)) is open but flagged `needs-author-action`.
- **RFC: Native Dynamic-Library Plugin System** ([#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)) – 3 comments, high engagement. Proposes moving from WASM-only to a `.so`/`.dylib` plugin architecture.
- **RFC: OCI-Compliant Container Registries for WASM Plugins** ([#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497)) – 2 comments. An alternative to the JSON index approach, using `wasm-pkg-client` and cosign.
- **Prompt-triggered install suggestions** ([#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)) – 3 comments. Users want automatic skill/plugin discovery when capabilities are missing.
- **MCP tools auto-include in risk profiles** ([#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547)) – new PR addressing a regression after flipping MCP defaults.
- **Per-agent delegate roster with cross-profile reach** ([#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590)) – proposed to fix delegation limitations between risk profiles.

**Underlying needs:** The community is pushing for a more modular, dynamically extensible architecture (plugins, MCP, delegation) and for memory/learning features that work offline.

### 5. Bugs & Stability
Multiple S1 (workflow-blocked) bugs were reported today:

| Issue | Severity | Description | Fix PR Status |
|-------|----------|-------------|---------------|
| [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563) | S1 | `canvas-store` regression after #6986 – Web UI `/canvas` empty after WS chat | No fix PR yet |
| [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | S1 | `ask_user` fails with "Channel closed before receiving a response" in gateway WS sessions | Multiple fix PRs: [#7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588), [#7584](https://github.com/zeroclaw-labs/zeroclaw/pull/7584), [#7586](https://github.com/zeroclaw-labs/zeroclaw/pull/7586) |
| [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | S1 | Web dashboard not available after macOS brew install (`cargo web build` needed) | Workaround documented, no formal fix PR yet |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | S1 | macOS app not working (permissions, empty page, window disappears) | No fix yet |
| [#7551](https://github.com/zeroclaw-labs/zeroclaw/issues/7551) | S1 (implied) | Free-form `ask_user` broken in WS approval channel | Fix PRs: [#7587](https://github.com/zeroclaw-labs/zeroclaw/pull/7587), [#7585](https://github.com/zeroclaw-labs/zeroclaw/pull/7585), [#7589](https://github.com/zeroclaw-labs/zeroclaw/pull/7589) |

**S2/S3 bugs:** Drag of dark theme text readability ([#7377], closed), Cmd-C quit chord ([#7378], closed), and a minor Windows test failure ([#7509], closed) were all resolved. A regression in `delegate` tool empty allowed_tools handling ([#7574](https://github.com/zeroclaw-labs/zeroclaw/pull/7574)) has a fix PR under review.

**Stability note:** The number of S1 bugs reported in a single day is elevated, but the team is shipping fixes quickly for most of them. The canvas-store regression and macOS app issues remain open and require maintainer attention.

### 6. Feature Requests & Roadmap Signals
New feature requests filed in the last 24 hours:

- **llama.cpp model router** ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)) – quick switching between local models.
- **Streaming card messages for QQ/DingTalk/WeChat/Feishu** ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)) – reduce wait time in Chinese IM channels.
- **Multi-session support in web chat UI** ([#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543)) – session sidebar with create/switch/rename/delete.
- **`file_read` charset detection** ([#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521)) – decode non-UTF-8 files (e.g., Windows-1251).
- **WhatsApp message reactions** ([#7518](https://github.com/zeroclaw-labs/zeroclaw/issues/7518)) – parity with Telegram/Discord/Matrix.
- **Delegate subagents with different risk profiles** ([#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514)) – follow-up to #7470.

**Predictions for next release (v0.8.1 or v0.9.0):**  
The v0.8.1 tracker ([#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) is active. Likely inclusions: Dream Mode (PR #6693), delegate roster cross-profile (PR #7590), MCP tools auto-include (PR #7547), and the native plugin RFC ([#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420)) if it gains maintainer approval. The multi-database session backends PR ([#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)) is still open but may target a later release due to its XL size.

### 7. User Feedback Summary
Real user pain points observed in today’s activity:

- **MCP tool visibility confusing** – Users setting `allowed_tools` expect MCP tools to be restricted too; documentation gap now closed but UX still unclear ([#6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876)).
- **macOS experience rough** – Brew installation yields a non-functional dashboard; the desktop app has permission and display issues ([#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523), [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)).
- **WebSocket ask_user unusable** – Multiple users hit “Channel closed before receiving a response” ([#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542), [#7551](https://github.com/zeroclaw-labs/zeroclaw/issues/7551)).
- **Quickstart non-TTY loop** – Scripted/CI environments crashed with 4.3 GB output ([#7507], now fixed).
- **Dark theme readability** – Light terminal profiles break dark zerocode themes ([#7377], fixed).
- **Chinese IM channels missing streaming** – Users of QQ/DingTalk/WeChat/Feishu experience long waits for rich card messages ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)).
- **Local model switching** – Need quick model router for llama.cpp to avoid editing config ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)).

**Positive signals:** Community is actively contributing fixes (4 PRs from xuwei-xy for WS ask_user bugs) and proposing well-researched RFCs. The dream mode feature is highly anticipated.

### 8. Backlog Watch
Long-standing items that may need maintainer attention:

- **Dream Mode implementation PR** ([#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693)) – Open since May 16, flagged `needs-author-action`, despite high community interest (18 comments on issue #5849). Awaiting author updates.
- **Skill improvement background review fork** ([#6667](https://github.com/zeroclaw-labs/zeroclaw/pull/6667)) – Open since May 14, also `needs-author-action`. Closes a gap from #4619.
- **Prompt-triggered install suggestions** ([#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)) – Accepted since May 2, no implementation PR yet.
- **Stabilize Node.js to latest LTS** ([#6211](https://github.com/zeroclaw-labs/zeroclaw/issues/6211)) – Open since April 29, `in-progress` but no merge.
- **Zerocode ACP Bridge tracker** ([#6823](https://github.com/zeroclaw-labs/zeroclaw/issues/6823)) – Open since May 21, accepted, but no PR linked.
- **v0.8.1 PR queue tracker** ([#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) – Updated today but still has zero comments; could benefit from a summary of blockers.
- **RFCs needing maintainer review:** [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) (native plugins), [#7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497) (OCI registries), [#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514) (delegate risk profiles). These have `needs-maintainer-review` labels and no formal decision yet.

**Overall project health:** High activity with strong

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*