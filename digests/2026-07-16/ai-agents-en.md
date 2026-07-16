# OpenClaw Ecosystem Digest 2026-07-16

> Issues: 468 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-16 01:55 UTC

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

# OpenClaw Project Digest — 2026-07-16

## 1. Today's Overview

OpenClaw remains highly active with **468 issues and 500 pull requests updated in the last 24 hours**. The project released a new beta (`v2026.7.2-beta.1`) featuring remote coding sessions. However, the community is experiencing significant friction from **P0/P1 crash-loop regressions in the 2026.7.1 upgrade path**, particularly around legacy state migration gates. Over **177 PRs were merged or closed today**, including several critical fixes for startup failures and session takeover errors. Overall health is **strained but responsive** — the maintainers are actively merging fixes for the most severe regressions.

## 2. Releases

**v2026.7.2-beta.1** ([openclaw/openclaw release](https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.1))

### Highlights
- **Remote coding sessions**: Run Control UI sessions on cloud workers, open Codex and Claude catalog sessions in terminals on their owning hosts, and resume OpenCode/Pi sessions directly in a terminal. (PRs #107670, #107086, #107200)
- **Native automation and nodes**: (details truncated in provided data; inferred expansion of agent automation capabilities)

**Migration Notes**: Users upgrading from 2026.7.1 are advised to run `openclaw doctor --fix` **before** upgrading to address legacy-state conflicts that caused gateway crash-loops. Several fixes for these crashes landed today (see §5).

## 3. Project Progress (Merged/Closed PRs Today)

Of the **177 merged/closed PRs** in the last 24h, notable resolved items include:

- **#108163** – *fix(ui): keep mount recovery retrying after stalled probes* – closed.
- **#107683** – *exec: allow-always script grants survive content changes* – closed (security fix).
- **#107605** – *fix(agents,cron): remove pattern field from model-facing cron tool schema* – closed (fixes #107449, llama.cpp compatibility).
- **#107727** – *[Bug]: Gateway refuses readiness after 2026.7.1 update due to plugin install metadata conflict* – closed.
- **#103076** – *[Bug]: additional legacy-state migration sources still block gateway startup after #102780* – closed.
- **#107330** – *[Bug]: OpenClaw Update 2026.7.1 Crash* – closed (Windows update crash resolved).
- **#103734** – *Codex usage-limit surfaced as promptError, not thrown — model fallback never fires* – closed.
- **#107227** – *2026.7.1 startup-migration gate is fatal, but `openclaw doctor` doesn't resolve the conflict* – closed (now a known documented step).

**Key areas advanced**: Gateway startup reliability, Codex integration, cron tool schema, Feishu media delivery (#98320 merged), and Telegram model picker (#98694 merged).

## 4. Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | 👍 | Summary |
|-------|----------|---|---------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – **Linux/Windows Clawdbot Apps** | 113 | 81 | Long-standing feature request for desktop platform parity (macOS already supported). Demand is high. |
| [#104721](https://github.com/openclaw/openclaw/issues/104721) – **All tool results return "(see attached image)" literal string** | 17 | 1 | **P0 regression**: actual file content replaced with placeholder. Users report this breaks all file-reading tools. |
| [#102020](https://github.com/openclaw/openclaw/issues/102020) – **Second message fails "reply session initialization conflicted"** | 14 | 1 | Cross-channel, position-dependent bug affecting Signal and other channels. |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) – **Codex PreToolUse native hook relay spawns CPU-bound processes** | 12 | 2 | High CPU usage stalls gateway RPC. |
| [#84583](https://github.com/openclaw/openclaw/issues/84583) – **Cron announce delivery triggers EmbeddedAttemptSessionTakeoverError** | 12 | 3 | Active chatting interrupted by cron jobs; session takeover error. |

**Underlying needs**: Users are frustrated with **regression stability** (multiple P0 bugs from recent builds) and **missing cross-platform support** (Linux/Windows). The top-voted issue (#75) also signals a desire for decentralized node support across all major OSes.

### Most Active PRs (by generated activity – top 30 shown; many with `undefined` comment counts but high review activity)

- **#102369** – *fix(agents): memoize exec auto-reviewer verdicts* – needs proof, security-boundary.
- **#108258** – *fix(state): gateway starts when WSL chmod returns EROFS* – low-risk fix for WSL2 users.
- **#98694** – *fix(telegram): use index-based callback_data to avoid silent model drops* – merged.
- **#107821** – *fix(agents): avoid premature compaction in tool-heavy sessions* – addresses #107655.

## 5. Bugs & Stability

### Severity P0 (Critical – Gateway crash-loop / Data loss)

| Issue | Created | Summary | Fix Status |
|-------|---------|---------|------------|
| [#107694](https://github.com/openclaw/openclaw/issues/107694) | 2026-07-14 | Gateway fails to start due to strict `startupMigrationWarnings` guard on benign legacy migration skips | Open, P0 |
| [#107220](https://github.com/openclaw/openclaw/issues/107220) | 2026-07-14 | 2026.7.1 gateway crash-loop: legacy memory sidecar `meta`/`chunks` conflicts fatal; `files` auto-resolves | Open, P0 |
| [#107727](https://github.com/openclaw/openclaw/issues/107727) | 2026-07-14 | Gateway refuses readiness after 2026.7.1 update due to plugin install metadata conflict for codex/discord | **Closed** |
| [#107330](https://github.com/openclaw/openclaw/issues/107330) | 2026-07-14 | OpenClaw Update 2026.7.1 Crash on Windows | **Closed** |
| [#104721](https://github.com/openclaw/openclaw/issues/104721) | 2026-07-11 | All tool results return "(see attached image)" literal string (regression, stable) | Open, P0 |
| [#101763](https://github.com/openclaw/openclaw/issues/101763) | 2026-07-07 | Hosted Molty: model selector doesn't persist – API receives dotted id `claude-opus-4.8` | Open, P0, maturity:stable |
| [#103076](https://github.com/openclaw/openclaw/issues/103076) | 2026-07-09 | Additional legacy-state migration sources still block gateway startup after #102780 | **Closed** |

### P1 (High Severity)

- [#107449](https://github.com/openclaw/openclaw/issues/107449) – cron tool JSON Schema incompatible with llama.cpp tool parser (regression) – **Fixed in #107605 (closed)**.
- [#106779](https://github.com/openclaw/openclaw/issues/106779) – Issue with 2026.7.1: local llama.cpp provider returns 400 parser error – Open.
- [#96834](https://github.com/openclaw/openclaw/issues/96834) – WhatsApp 1:1 image wedges main lane ~3min – Open.
- [#94518](https://github.com/openclaw/openclaw/issues/94518) – DeepSeek cache hit rate <10% after 6.x upgrade – Open.
- [#80040](https://github.com/openclaw/openclaw/issues/80040) – Cascading failure: invalidated OAuth, duplicate tool execution, cold-cache bootstrap – Open since May.

### Assessment
The **2026.7.1 release introduced several critical startup regressions**. While most have been identified and several fixed today (#107727, #107330, #107227, #103076), users still report issues with legacy state migration guards (#107694) and memory sidecar conflicts (#107220). The **placeholder tool output bug (#104721)** remains unresolved and is a release-blocker. Overall stability is **below average** for a beta cycle.

## 6. Feature Requests & Roadmap Signals

### High-Interest Requests (by 👍 + comments)

- **#75** ([Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)) – 81 👍, 113 comments. Most-voted feature request. Likely to be considered for next major after beta stabilization.
- **#94518** ([DeepSeek cache optimization](https://github.com/openclaw/openclaw/issues/94518)) – 10 👍. Users demand better caching for cost-efficiency.
- **#11665** ([Webhook multi-turn session support](https://github.com/openclaw/openclaw/issues/11665)) – Long-standing (Feb 2026), need for consistent session reuse.
- **#107686** ([Intelligent Multi-LLM Router](https://github.com/openclaw/openclaw/issues/107686)) – New request for automatic model routing to reduce token costs.
- **#82548** ([AI safety/quality observability](https://github.com/openclaw/openclaw/issues/82548)) – Operators want monitoring for prompt injection and citation quality.

### Predictions for Next Version
- **Cross-platform Clawdbot app** (Linux/Windows) – demand is clear.
- **Improved legacy-state migration automation** – current pain point.
- **Multi-LLM router** – several issues (#107686, #85103) highlight need for intelligent fallback.
- **Memory lifecycle curation** (#87660) – likely to see progress given community interest.

## 7. User Feedback Summary

### Pain Points (most vocal)
- **Upgrade regressions**: Multiple users reported gateway crash-loops after 2026.7.1, especially on long-lived installs. "Completely broken" (#104721) and "no documented remedy" (#107227).
- **Session takeover errors**: Cron jobs and cross-channel interactions causing `EmbeddedAttemptSessionTakeoverError` (#84583, #80040, #85103). Users feel the system cannot handle concurrent access gracefully.
- **Missing platform parity**: Linux/Windows users feel left behind (Issue #75).
- **Tool output corruption**: The placeholder string bug (#104721) is described as "this is completely broken."

### Positive Signals
- **Active maintainer response**: Many critical bugs fixed within 1–2 days of reporting (e.g., #107227, #107727, #107330).
- **Community engagement**: High comment counts on feature requests show an invested user base.
- **Remote coding sessions** in the new beta are appreciated by cloud-heavy users.

## 8. Backlog Watch

### Important Issues Needing Maintainer Attention

| Issue | Last Updated | Age | Signs of Neglect |
|-------|-------------|-----|------------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows Clawdbot Apps | 2026-07-15 | 6+ months | Only labels: `enhancement`, `help wanted`, `P2`. No recent maintainer comment. |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) – Webhook multi-turn session support | 2026-07-15 | 5 months | `needs-product-decision` label. Linked PR open but no maintainer review. |
| [#9607](https://github.com/openclaw/openclaw/issues/9607) – Himalaya skill: missing email formatting philosophy | 2026-07-16 | 5 months | `P3`, low priority but user reported inaccuracies. |
| [#80040](https://github.com/openclaw/openclaw/issues/80040) – Cascading failure: OAuth, tool duplication, context loss | 2026-07-15 | 2 months | Multiple `needs-*` labels (maintainer-review, product-decision, security-review). |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) – Codex PreToolUse CPU-bound processes | 2026-07-15 | 1 month | `needs-product-decision`, linked PR open. |
| [#84242](https://github.com/openclaw/openclaw/issues/84242) – `memory-lancedb` not exposed as agent tool | 2026-07-15 | 2 months | `stale` label, but 3 👍. |

### Long-Standing PRs Awaiting Review

- **#101973** – *Create Claw-managed workspace files* – `waiting on author`, P2.
- **#89039** – *fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError* – `waiting on author` since June 1.
- **#97175** – *fix(context-engine): bound deferred turn maintenance with a per-task timeout* – `ready for maintainer look`, P1.
- **#98694** – *fix(telegram): use index-based callback_data* – `ready for maintainer look` (merged later today).

**Conclusion**: While the project has high velocity, several important feature requests and long-lived bugs remain unattended. The current focus is clearly on stabilizing the 2026.7.x release cycle.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digests.

---

## Cross-Project Comparison Report: AI Personal Assistant Open-Source Ecosystem

**Date:** 2026-07-16
**Analyst:** Senior Analyst, AI Agent & Personal AI Assistant Ecosystem

### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is in a phase of **rapid maturation**, marked by high-velocity development, significant stability regressions, and a clear shift toward multi-provider and production-grade architectures. Projects are converging on a core set of features—remote coding, persistent memory, and platform parity—while diverging in implementation philosophy (e.g., monolithic vs. modular, Python vs. Rust). The ecosystem is experiencing **growing pains from the 2026.7.x upgrade cycle**, with several projects (notably OpenClaw and IronClaw) facing critical crash-loop regressions that have strained community trust. Despite this, maintainer responsiveness remains high, with many P0/P1 bugs being resolved within 24 hours. The most successful projects are those balancing feature velocity with a disciplined focus on migration tooling and test harnesses.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Score | Key Signal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 468 | 500 | Beta v2026.7.2-beta.1 | **Strained but Responsive** | P0 regressions from 2026.7.1 upgrade path; high fix velocity. |
| **ZeroClaw** | 38 | 50 | v0.8.3 | **Healthy, High-Velocity** | Major feature cycle (SOP engine, WASM); security hardening wave. |
| **CoPaw** | 50 | 43 | None | **Active, but Regressing** | High bug count from v2.0 upgrade; memory leak and context loss. |
| **NanoBot** | 24 | 27 | None | **Healthy, Maintenance Heavy** | Comprehensive security audit; 20+ bugs closed in 24h. |
| **Hermes Agent** | 50 | 50 | None | **Balanced, Growing Backlog** | Steady fixes on `main`; 44 open PRs indicate review bottleneck. |
| **IronClaw** | 23 | 38 | None | **Active, Slack Regression Churn** | High activity on v1 runtime removal; Slacks bugs remain unresolved. |
| **LobsterAI** | Low (1 new) | 17 (11 merged) | v2026.7.15 | **Healthy, Polishing** | Quick iteration on UI/UX, new model support (GPT-5.6). |
| **Moltis** | Low (1 open) | 6 (all merged) | None | **Healthy, Focused** | Provider fixes, ACP agent auto-detection; very low issue count. |
| **NanoClaw** | 2 | 11 (4 merged) | None | **Moderate, Feature-Focused** | Multi-provider push; critical delivery retry bug (P0) open. |
| **PicoClaw** | 6 (3 stale) | 2 (0 merged) | None | **Low, At Risk** | Stale bugs closed without fixes; new ARM64 launcher blocker. |
| **TinyClaw** | 0 | 1 (0 merged) | None | **Quiescent** | Minor CLI bug fix pending. |
| **NullClaw / ZeptoClaw** | 0 | 0 | None | **Inactive** | No activity observed. |

### 3. OpenClaw's Position

**Advantages:**
- **Scale & Community:** OpenClaw is the undisputed core reference, with a community order of magnitude larger than peers (468 issues/500 PRs in 24h). This creates a strong network effect for plugins and integrations.
- **Velocity of Fixes:** Maintainers show exceptional responsiveness, merging 177 PRs in 24h and closing P0/P1 regressions within 1–2 days of reporting. This sets a high bar for ecosystem support.
- **Feature Set:** The `v2026.7.2-beta.1` release introduces *remote coding sessions*, a feature that directly addresses developer workflows, putting it ahead of peers in cloud-native agent capabilities.

**Technical Approach Differences:**
- OpenClaw follows a **monolithic, full-stack approach** (gateway, agents, UI, plugins) with a heavy reliance on Python. This contrasts with **ZeroClaw's Rust-based, modular architecture** (SOP engine, WASM plugins), which offers better performance and security isolation but a smaller contributor base.
- Its approach to **state management (legacy migrations)** is the primary source of its current instability, whereas **NanoBot** and **IronClaw** are spending more effort on security audits and formal testing harnesses to prevent such regressions.

**Community Size Comparison:**
- OpenClaw's activity dwarfs all others. The next most active project (ZeroClaw) has ~10% of OpenClaw's PR volume, indicating OpenClaw has a dominant mindshare but also a higher risk of fragmentation and noisy issues.

### 4. Shared Technical Focus Areas

The following requirements are emerging as industry-level standards across multiple projects:

1.  **Provider Agnosticism & Quota Fallback:** A clear trend is the need to seamlessly switch between LLM providers upon hitting quota or errors.
    - **Projects:** NanoClaw (Claude→Codex fallback, PR #3057), OpenClaw (Codex integration), ZeroClaw (multi-user auth prf), Moltis (MiniMax M3, dynamic providers).
    - **Need:** Automatic failover to avoid service interruption.

2.  **Persistent & Isolated Memory:** Users demand that agents maintain context across sessions and that memory is logically separated from conversation history.
    - **Projects:** CoPaw (memory loss in v2.0, PR #6123), ZeroClaw (memory separation RFC #9048), NanoClaw (provider-agnostic memory, PR #3012).
    - **Need:** Data integrity and long-term agent coherence.

3.  **Security Hardening & Audit:** A wave of security reviews is sweeping the ecosystem, particularly for authorization bypass and command injection.
    - **Projects:** NanoBot (42-finding audit, 20+ fixes), ZeroClaw (multi-user auth, pluggable security), OpenClaw (exec script grants).
    - **Need:** Production-grade security for enterprise use.

4.  **Platform Parity (Linux/Windows/ARM):** Significant user demand for first-class support on all major platforms, not just macOS.
    - **Projects:** OpenClaw (Issue #75, 81👍), PicoClaw (ARM64 launcher missing, Issue #3260), CoPaw (Kylin OS support), Hermes Agent (Windows console fixes).
    - **Need:** Broadening user base from developers to enterprise and personal use.

5.  **Session Takeover & Reliability:** Handling concurrent interactions (cron, multi-channel, multiple user queries) without dropping messages or losing state.
    - **Projects:** OpenClaw (#84583, #80040), NanoBot (#4924, heartbeat in unified sessions), CoPaw (#5995, silent message drops).
    - **Need:** Robust, non-blocking concurrency in agent systems.

### 5. Differentiation Analysis

| Feature Focus | Primary Projects | Target User | Architectural Philosophy |
| :--- | :--- | :--- | :--- |
| **Remote Coding & Cloud Dev** | **OpenClaw**, **ZeroClaw** | Developers, DevOps | Monolithic (Python) vs. Modular (Rust) |
| **Multi-Channel Messaging** | **NanoBot**, **Hermes Agent**, **IronClaw** | Power Users, Chat Integrators | High channel coverage; IronClaw specific to Slack ecosystem. |
| **UI Polish & Model Support** | **LobsterAI**, **CoPaw** | Consumers, Enterprise (China) | Strong focus on desktop client quality and local model support. |
| **Lightweight / CLI-First** | **TinyClaw**, **NanoClaw**, **Moltis** | Developers, Minimalists | Simpler setups, containerized runtimes, lower feature surface. |
| **Embargo / Security-First** | **ZeroClaw** | Enterprise | Air-gapped mode, WASM sandboxing, OIDC, formal capability checks. |

**Key Takeaway:** **OpenClaw** and **ZeroClaw** are competing for the top spot in the "developer agent" space, with different technical bets (Python vs. Rust). **NanoBot** is the strongest contender for the "personal assistant" use case due to its multi-channel routing and community polish. **IronClaw** and **CoPaw** are tied to specific platform ecosystems (Slack, Feishu) and are struggling with the complexity of those integrations.

### 6. Community Momentum & Maturity

- **Tier 1 (High Velocity, High Friction):** **OpenClaw**, **NanoBot**, **ZeroClaw**, **CoPaw**. These projects are pushing the most features but are also dealing with the most regressions. They are in a "build fast and fix" cycle.
- **Tier 2 (Steady Iteration):** **Hermes Agent**, **IronClaw**, **Moltis**, **LobsterAI**. These are more stable, focusing on specific feature areas (automation, Slack integration, provider compatibility). They are less likely to break core functionality but may create review backlogs.
- **Tier 3 (Low Activity / Niche):** **NanoClaw**, **PicoClaw**. These are at risk of falling behind on features and security. PicoClaw's ARM64 blocker is a critical threat to its user base.
- **Tier 4 (Dormant):** **TinyClaw**, **ZeptoClaw**, **NullClaw**. These projects appear stalled or are in a long-term hibernation phase.

### 7. Trend Signals

1.  **"Stability Over Features" is the New Mandate.** The harsh community backlash against the 2026.7.1 upgrade regressions (OpenClaw) and v2.0 context loss (CoPaw) signals a plateau in tolerance for breaking changes. For AI agent developers, this means **investment in migration tooling, legacy state management, and robust test harnesses (like IronClaw's tier-2 fault injection) is now a competitive differentiator.**

2.  **Observability is Becoming a First-Class Citizen.** Requests for OTel trace correlation (ZeroClaw), token-level accounting (OpenClaw), and agent run logs are becoming standard. Developers building on these ecosystems will need to provide hooks for turn-level debugging and cost attribution.

3.  **The "Local-First" Renaissance.** The volume of issues around Ollama compatibility (#107449, #63680), ARM64 support, and air-gapped execution shows a strong undercurrent of users wanting to run agents on their own hardware, away from API dependencies. This is a direct response to rising API costs and privacy concerns.

4.  **Security is No Longer Optional.** The NanoBot audit reveals that many projects have systemic authorization problems. For the ecosystem to mature, agents must enforce **capability-based access control** (e.g., "allow-always script grants" in OpenClaw, "principal isolation" in ZeroClaw) as a default, not an afterthought. Developers should expect to integrate with OIDC or similar standards (see ZeroClaw RFC #7141).

**Value for AI Agent Developers:** The choice between OpenClaw (massive community, fast fixes, risk of complexity) and ZeroClaw (modern architecture, security-focused, smaller community) is becoming the central decision for teams building production agent systems. A third option is building on the **NanoBot kernel** (Python, well-audited, multi-channel) for a more stable, consumer-facing personal assistant.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-16

## 1. Today's Overview

The project experienced a surge in activity over the past 24 hours, with **24 issues updated** (21 closed, 3 open) and **27 pull requests updated** (16 open, 11 merged/closed). The majority of activity came from a comprehensive security and correctness audit (see Issue #4815) that produced 42 findings; 20+ of those issues were closed through corresponding fix PRs. Additionally, several feature PRs advanced toward merging, including session-local triggers, heartbeat commands, and Render deployment support. Overall the project is in a **highly active maintenance phase**, with equal emphasis on patching vulnerabilities and adding planned features. No new releases were published today.

> **Links:** [NanoBot Repository](https://github.com/HKUDS/nanobot) | [Issues](https://github.com/HKUDS/nanobot/issues) | [Pull Requests](https://github.com/HKUDS/nanobot/pulls)

---

## 2. Releases

**No new releases** were published in the last 24 hours. The latest published release remains unreported in this data; a future release is likely once the current batch of security fixes and refactors stabilishes.

---

## 3. Project Progress

### Merged/Closed Pull Requests (11 total)

| PR # | Title | Summary |
|------|-------|---------|
| #4944 | fix(gateway): stop channels before draining tasks | Fixes shutdown ordering where DingTalk Stream could swallow cancel signals; adds regression test. |
| #4943 | fix(providers): honor Codex proxy config consistently | Ensures OAuth login and image-generation clients respect the selected proxy configuration. |
| #4649 | fix(webui): correct activity timer duration | Fixes live “Working for …” timer to start from user turn, not first trace. |
| #4870 | Share channel markdown helpers | Extracts duplicated markdown-to-platform converters into shared utilities (Telegram, Signal, Feishu). |
| #4813 | fix(loop): guard .strip() on msg.content against list-form multimodal data | Prevents `AttributeError` when multimodal messages (list-form content) arrive. |
| #4926 | fix: include Feishu SDK in dev dependencies | Ensures `lark-oapi` is installed when running tests with `uv sync --extra dev`. |
| **5 other PRs** (not fully shown) | — | Likely includes fixes for the remaining security issues closed today. |

**Key advancements:**
- **Security hardening** — 7+ authorization bypass and command injection vulnerabilities closed via PRs (e.g., ProcessDirect bypass, /stop cross-user cancellation, Dream overwrite).
- **Refactoring** — Channel init duplication extracted to `BaseChannel`; shared markdown helpers reduce code duplication across 3 channels.
- **Multi‑modal support** — Guard added for `.strip()` on list‑form content (PR #4813).
- **Proxy consistency** — Codex provider now properly forwards proxy settings for OAuth and image generation.

> **Links:** [PR #4944](https://github.com/HKUDS/nanobot/pull/4944) | [PR #4943](https://github.com/HKUDS/nanobot/pull/4943) | [PR #4649](https://github.com/HKUDS/nanobot/pull/4649) | [PR #4870](https://github.com/HKUDS/nanobot/pull/4870) | [PR #4813](https://github.com/HKUDS/nanobot/pull/4813) | [PR #4926](https://github.com/HKUDS/nanobot/pull/4926)

---

## 4. Community Hot Topics

The most active issue by comment count is:

- **#4924** — *`cli/commands.py:_pick_heartbeat_target_from_sessions` fails when `unifiedSession: true`*  
  **4 comments** | Open | Reported by wzrayyy  
  This bug is particularly impactful for users relying on unified session mode, as heartbeats cannot be delivered. A fix PR (#4928) is already open.

Other notable topics:

- **Security Audit (#4815)** — 42 findings from a deep code audit by contributor hamb1y. While only 1 comment on the issue itself, the finding spawned 20+ individual issues (now closed) and corresponding fix PRs, indicating high community/team engagement.
- **#4779, #4778, #4777, #4776** (all closed) — Security issues around authorization bypass. Each had 2 comments and were resolved quickly.
- **#4940** (open, 0 comments) — *read_session_metadata() lacks legacy filename fallback, causing WebUI workspace_scope to be lost after restart.* New bug affecting sessions with custom project paths.

**Underlying needs:**  
Users and auditors are focused on **security and correctness** — authorization gaps, privilege escalation, and silent data loss. The rapid closing of these issues suggests a strong maintainer response.

> **Links:** [Issue #4924](https://github.com/HKUDS/nanobot/issues/4924) | [Issue #4815](https://github.com/HKUDS/nanobot/issues/4815) | [Issue #4779](https://github.com/HKUDS/nanobot/issues/4779) | [Issue #4940](https://github.com/HKUDS/nanobot/issues/4940)

---

## 5. Bugs & Stability

### Open Bugs (needs resolution)

| Severity | Issue | Description |
|----------|-------|-------------|
| **High** | #4924 | Heartbeat target selection fails in unified singleton session mode. Fix PR #4928 open. |
| **High** | #4940 | Session metadata (workspace_scope) lost after restart for legacy filenames. No fix PR yet. |
| **Medium** | #4934 | Qwen models (e.g., qwen3.6-flash) expose thinking/reasoning content in chat responses. Fix PR #4946 open. |

### Closed Bugs (fixed today)

- **Security: ProcessDirect bypass (#4779)** — Fixed via merged PR.
- **Security: System channel bypass (#4778)** — Fixed.
- **Security: /stop cross-user cancel (#4777)** — Fixed.
- **Security: /restart DoS (#4776)** — Fixed.
- **Security: Message tool outbound bypass (#4076)** — Fixed.
- **Security: Dream skill overwrite (#4075)** — Fixed.
- **Bug: Cron job context reuse (#4082)** — Fixed.
- **Bug: Multimodal .strip() crash (#4800)** — Fixed via PR #4813.
- **Bug: Token budget 128 spillover (#4802)** — Fixed.
- **Bug: None URL cache signature (#4799)** — Fixed.
- **Bug: Global ExecSessionManager cross‑session visibility (#4793)** — Fixed via PR #4862 (merged? still open? but likely merged given closed issues).
- **Bug: WeakValueDictionary lock GC deletion (#4789)** — Fixed.
- **Bug: Socket proactive message drop (#4062)** — Fixed.
- **Bug: Context trimming drops assistant question (#4056)** — Fixed.
- **Bug: Invalid config silent fallback (#4067)** — Fixed.

### Stability Assessment

Today’s activity resolved nearly **20 bugs**, most of which were security-critical. The project’s testing infrastructure appears robust (many fix PRs include new tests). Two open bugs (#4924, #4940) are high-severity and should be prioritized.

> **Links:** [Issue #4924](https://github.com/HKUDS/nanobot/issues/4924) | [Issue #4940](https://github.com/HKUDS/nanobot/issues/4940) | [Issue #4934](https://github.com/HKUDS/nanobot/issues/4934) | [PR #4928](https://github.com/HKUDS/nanobot/pull/4928) | [PR #4946](https://github.com/HKUDS/nanobot/pull/4946)

---

## 6. Feature Requests & Roadmap Signals

### Open Feature PRs

- **#4942** — *feat(triggers): let agents manage session-local triggers*  
  Adds a `local_trigger` tool so agents can create/list/enable/disable/remove session-scoped triggers. Likely to be merged next.
- **#4620** — *add heartbeat trigger command*  
  CLI-based heartbeat trigger runner with LLM decision and workspace lock. Addresses #3437.
- **#4621** — *feat(memory): gate archive facts with provenance context*  
  Improves Consolidator archive prompts to skip duplicates and recognize corrections.
- **#4919** — *feat(telegram): support custom Bot API base URL and extra headers*  
  Enables self-hosted Bot API servers. Requested via #4702.
- **#4937** — *feat: add one-click Deploy to Render support*  
  Render Blueprint with bundled WebUI and persistent sessions.
- **#4947** — *fix(web): keep sensitive URLs out of Jina Reader*  
  Security improvement (closes #4884), but includes configuration change.

### User-Requested Features (from Issues)

- **Session-local triggers** — Users want agents to manage recurring actions per conversation.
- **Custom Telegram Bot API** — Enterprise users need self-hosted endpoints.
- **Preserve automation source in WebUI** — PR #4822 attempts to fix streamed reply metadata loss.
- **Session metadata persistence for legacy filenames** — Issue #4940 indicates pain with data loss after restart.

### Roadmap Prediction

The next version (likely v0.6.x or similar) will include:
- Consolidated security fixes (authorization, input validation)
- Session-local triggers (PR #4942)
- Heartbeat trigger command (PR #4620)
- Memory provenance gating (PR #4621)
- One-click Render deployment (PR #4937)
- Telegram custom API support (PR #4919)

> **Links:** [PR #4942](https://github.com/HKUDS/nanobot/pull/4942) | [PR #4620](https://github.com/HKUDS/nanobot/pull/4620) | [PR #4919](https://github.com/HKUDS/nanobot/pull/4919) | [PR #4937](https://github.com/HKUDS/nanobot/pull/4937) | [PR #4947](https://github.com/HKUDS/nanobot/pull/4947) | [Issue #4884](https://github.com/HKUDS/nanobot/issues/4884)

---

## 7. User Feedback Summary

### Pain Points (from Issues & PRs)

- **Authorization gaps** — Users reported that ProcessDirect, system channel, /stop, and /restart commands could bypass permissions. This was the most prominent concern.
- **Data loss** — Session metadata (workspace_scope) silently lost after restart (Issue #4940). Also, cron jobs reusing the same session context caused cross-run contamination (#4082).
- **Qwen reasoning leakage** — Thinking content exposed in normal chat responses (#4934).
- **Heartbeat failure in unified sessions** — Sessions without explicit channel config lose heartbeat delivery (#4924).
- **Inconsistent proxy handling** — Codex provider ignored proxy settings for OAuth and image generation (#4943, fixed).
- **Markdown converter duplication** — Three channels had nearly identical converters, causing maintenance overhead (#4810, #4870 fixed).

### Satisfaction Signals

- **Rapid issue closure** — 21 out of 24 issues updated were closed, most within hours or days of reporting.
- **Audit acknowledged** — The comprehensive 42‑finding audit (#4815) was a positive sign of community investment in quality.
- **Feature progression** — 16 open PRs indicate active development beyond just bug fixes.

> **Links:** [Issue #4940](https://github.com/HKUDS/nanobot/issues/4940) | [Issue #4082](https://github.com/HKUDS/nanobot/issues/4082) | [Issue #4934](https://github.com/HKUDS/nanobot/issues/4934)

---

## 8. Backlog Watch

No issues or PRs in the backlog appear long‑standing or unanswered. The oldest issues updated today were from **2026-05-29** (e.g., #4082, #4076, #4075, #4067, #4062, #4056) and were all closed today. The maintainer team has been exceptionally responsive, likely due to the security audit push.

**Potential items to watch:**

- **#4924** (unified heartbeat) and **#4940** (legacy metadata) are the only open bugs without a merged fix yet. Both are under active development (#4928 open for heartbeat; no PR yet for #4940).
- **#4918** (config centralization refactor) is a large PR with conflicts — it may need review or rebase.
- **#4621** (memory provenance) has been open since July 1 and may be awaiting design sign-off.

> **Links:** [Issue #4924](https://github.com/HKUDS/nanobot/issues/4924) | [Issue #4940](https://github.com/HKUDS/nanobot/issues/4940) | [PR #4918](https://github.com/HKUDS/nanobot/pull/4918) | [PR #4621](https://github.com/HKUDS/nanobot/pull/4621)

---

*Generated from NanoBot GitHub data snapshot: 2026-07-16*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent Project Digest — 2026-07-16

### Today's Overview

Project activity remains high, with 50 issues and 50 pull requests updated in the last 24 hours—a balanced split between open and closed items. The 6 merged/closed PRs indicate steady incremental progress, though 44 open PRs suggest a growing review backlog. No new releases were published today. The community is actively discussing plugin interface expansion and desktop session-stability bugs, while maintainers continue to close high-severity issues with sweeper-driven fixes on `main`.

### Releases

No new releases today.

### Project Progress (Merged/Closed PRs Today)

Three PRs were merged or closed in the top-20 sample, all labelled `sweeper:implemented-on-main`:

- **#64097** (fix(agent): recognize vLLM/Qwen context-length error as output-cap error) – Resolves a provider compatibility issue where overflow errors from vLLM and Qwen were misclassified, preventing graceful fallback.  
- **#64084** (feat(agent): add PreToolUse enforcement hook for prompt-level rules) – Implements #63770, making behavioral rules resilient to LLM recency bias via a programmatic lifecycle hook.  
- **#64077** (fix(telegram): wrap callback_query handler with resilient_handler to swallow TimedOut) – Prevents polling loops caused by unhandled Telegram `TimedOut` exceptions.

These represent targeted stability and provider-compliance improvements, with no major feature releases today.

### Community Hot Topics

1. **#64182** (Plugin Interface Expansion — tracking issue, 12 comments) – The most active thread, collecting community ideas from Discord for expanding the core plugin interface. Contributors are coordinating on long-queued PRs to ship stable public APIs.  
2. **#63911** (Telegram DM topic mode root-lobby gate swallows wake events, 5 comments, closed) – A subtle gateway bug where lobby-mode DMs never process kanban wake events; fixed on `main`.  
3. **#23359** (Model/Provider inventory lacks scriptable surface, 4 comments, open since May) – Repeated friction: five PRs reinvent CLI/API surfaces because no single endorsed command-line output format exists.  
4. **#3326** (`--output-format json` flag, 5 👍, open since March) – Strong community support for structured query output, but implementation still pending.  
5. **#44771** (Curator LLM review loop on symlinked skills, 2 comments, open) – A critical resource-waste bug consuming millions of tokens; maintainer attention needed.

### Bugs & Stability

**Highest severity (P0):**  
- **#63712** (AsyncSessionDB methods silently dropped without `await`, *closed, fix on main*) – Lost writes and runtime warnings when gateway model-switch code omitted `await`. Patch preventing future occurrences.

**Notable P2 bugs (many with fixes on main):**  
- **#63698** ([Windows] Console windows flash despite `windows_hide_console`, *closed*) – Resolved via sweeper.  
- **#63680** (Tool definitions not transmitted to custom endpoints, *closed, fix on main*) – Models never trigger real tool calls; impact on Ollama/local setups.  
- **#64789** (Desktop prompt.submit targets stale runtime, *open*) – Session state drift leads to submissions against wrong agent instance.  
- **#65297** (Desktop image paste broken – session ID drift between `image.attach` and `prompt.submit`, *open, P2*) – New bug reported today, blocking media-rich workflows on macOS.  
- **#52514** (Checkpoint restore fails with target message not in history, *open, P2*) – Recurring session corruption in Desktop v0.17.  
- **#64079** (Hermes Studio auto-update misses pip dependencies, *closed, fix on main*) – Second occurrence of silent failures after desktop update.

**Platform-specific:** Several Windows/WSL bugs (#63698, #64079) and Telegram polling conflicts (#63387, #63724) have been fixed this week. Open P2 bugs on Desktop (#64789, #65297) lack companion fix PRs yet.

### Feature Requests & Roadmap Signals

The tracking issue **#64182** signals a concerted effort to stabilise the plugin interface—likely targeting the next minor release. Other popular or recurring requests:

- **#64666** – Configurable default view (rendered vs. diff) for right-rail file preview in Desktop.  
- **#63923** – Preserve user customisations across updates (branding, widgets).  
- **#63668** – Make `--tui` the default interface (no flag needed).  
- **#11367** – Add MiniMax highspeed model variants (long-standing, 3 months).  
- **#64094** (PR) – Surface async delegation results natively in chat; could improve observability.  
- **#64075** (PR) – Rule-injector plugin for contextual hard-rules at point of need.

Given the volume of `sweeper:implemented-on-main` tags, the next release (v0.19?) will likely include the PreToolUse hook (#63770), the vLLM error fix, and several Telegram/DM stability patches.

### User Feedback Summary

**Pain points (direct user reports):**  
- Telegram bot goes deaf silently (#63911, #63724) – a recurring theme across multiple issues.  
- Desktop sessions disappear after restart (#63516) or fail to persist (#63474) – data loss erodes trust.  
- Windows users face console flashes (#63698) and missing native binaries (#63805).  
- Custom Ollama/local endpoints do not receive tool definitions (#63680) – community reliance on local models.  
- Massively wasteful token loops (#44771) cause unexpected costs.  

**Satisfaction signals:**  
- Several bugs closed with `sweeper:implemented-on-main` in <3 days, indicating effective sweep automation.  
- The plugin tracking issue (#64182) shows active community collaboration and maintainer engagement.  
- 5 👍 on the JSON output request (#3326) indicate lasting demand for scriptable interfaces.

### Backlog Watch

These issues and PRs have been open for extended periods without resolution or maintainer comment, risking community frustration:

| Item | Created | Type | Notes |
|------|---------|------|-------|
| **#23359** (Scriptable provider/model inventory) | 2026-05-10 (2+ months) | Feature/P2 | Four issues blocked, five PRs reinvent the wheel. |
| **#3326** (JSON output flag) | 2026-03-27 (3.5 months) | Feature/P3 | 5 👍, no maintainer activity since May. |
| **#44771** (Curator loop on symlinks) | 2026-06-12 (1 month) | Bug/P2 | 91M token waste reported; no fix PR. |
| **#46778** (Desktop pool backends orphaned) | 2026-06-15 (1 month) | Bug/P3 | Leaks `hermes dashboard` processes; no progress. |
| **#52514** (Checkpoint restore fails) | 2026-06-25 (3 weeks) | Bug/P2 | Reported on Windows, stil open. |
| **#11367** (MiniMax highspeed models) | 2026-04-17 (3 months) | Feature/P3 | Trivial change; likely waiting for maintainer. |
| **PR #9031** (Structured tool errors in hooks) | 2026-04-13 (3 months) | Feature/P3 | No merge despite being marked `sweeper:risk-compatibility`. |

Maintainers should prioritise these items to prevent stagnation, especially the high-impact bugs (#44771, #52514) and the foundational feature gap (#23359).

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-16

## 1. Today's Overview

The project saw moderate activity over the past 24 hours: 6 issues were updated (3 closed as stale, 3 newly opened) and 2 pull requests received updates (both remain open). No new releases were published. The stale bugs that were closed involve tool‑call leaking with Volcengine Doubao and OAuth login failures, suggesting recurring integration pains. Two fresh bugs were reported — one blocking ARM64 users from launching the app, and another breaking the `before_tool` hook system. A feature request for stateless gateway sessions also appeared. Overall, the project is addressing older reports through cleanup but still faces several unresolved functional issues.

---

## 2. Releases

None. No new versions were published in the last 24 hours.

---

## 3. Project Progress

No pull requests were merged or closed today. Two PRs remain open:

- **PR #3259** (opened 2026-07-15) – *Update PicoClaw description for parallelization*  
  A documentation‑level change that adds a note about better parallelization. No code impact.

- **PR #3222** (opened 2026-07-03, updated 2026-07-15) – *refactor(deltachat): cleanup implementation, documentation -200LOC*  
  A larger refactoring of the Delta Chat integration that removes legacy features, drops password‑based email config, and renames endpoints. Still awaiting review/merge.

No functional advances were merged today.

---

## 4. Community Hot Topics

The most commented items are closed stale bugs, indicating past community engagement that did not result in fixes:

- **[Issue #3153](https://github.com/sipeed/picoclaw/issues/3153)** (4 comments) – *[CLOSED] Volcengine Doubao Seed tool calls leak as raw `<seed:tool_call>` text*  
  Users encountered tool calls being returned as plaintext instead of executed. Closed as stale, but the underlying issue with Volcengine integration remains unresolved.

- **[Issue #3197](https://github.com/sipeed/picoclaw/issues/3197) & [#3196](https://github.com/sipeed/picoclaw/issues/3196)** (2 comments each) – *[CLOSED] Codex and antygravity OAuth login not working*  
  Duplicate reports of OAuth login failures. Also closed as stale.

All open issues have zero comments or reactions, so no current hot topics are generating discussion. The community’s main pain points appear to be integration reliability and authentication.

---

## 5. Bugs & Stability

Two new bugs were reported today; no fix PRs exist yet.

| Severity | Issue | Summary |
|----------|-------|---------|
| **High** | [#3258](https://github.com/sipeed/picoclaw/issues/3258) | `Process Hook before_tool modify` not working: `decision` field discarded and arguments misparsed due to a deserialization defect. This breaks a core hook mechanism for tool modification. |
| **Medium** | [#3260](https://github.com/sipeed/picoclaw/issues/3260) | The ARM64 (arm64) release from picoclaw.io is missing the launcher executable entirely, making the app unusable on Raspberry Pi 3B / Raspbian. |

Three stale bugs (#3153, #3197, #3196) were closed without evidence of fixes. This pattern may indicate insufficient maintainer capacity to address older reports. The two new bugs demand attention to avoid regressing on ARM support and hook reliability.

---

## 6. Feature Requests & Roadmap Signals

One feature request appeared today:

- **[Issue #3257](https://github.com/sipeed/picoclaw/issues/3257)** – *Add stateless/no‑history mode for gateway sessions*  
  The user wants the gateway to support ephemeral sessions (similar to `--session` in CLI mode) so that each chat interaction starts fresh without accumulating history. This is a logical extension for use cases like stateless chatbots or testing.

Additionally, PR #3259 (descriptive update about parallelization) hints that the team may be considering or improving concurrency, though no code changes are attached.

Given the absence of current release activity, these features are unlikely to land in the immediate next version unless the project’s release cadence accelerates.

---

## 7. User Feedback Summary

Reported pain points from recent issues:

- **Integration trouble**: Tool calls with Volcengine Doubao leak as raw text instead of executing (Issue #3153). This erodes trust in third‑party provider support.
- **Authentication failures**: OAuth login for Codex and antygravity not working (Issues #3197, #3196). Hinders adoption on those platforms.
- **Platform incompleteness**: ARM64 users cannot even launch the app (Issue #3260). A critical blocker for Raspberry Pi users.
- **Customization broken**: The `before_tool` hook system is unusable due to deserialization errors (Issue #3258). Frustrates advanced users relying on hooks for tool rewriting.
- **Desire for stateless operation**: Gateway users want session control similar to the CLI (Issue #3257).

No positive feedback or satisfaction indicators were recorded in the observed data.

---

## 8. Backlog Watch

Items that have been open for a while without maintainer response or resolution:

- **[PR #3222](https://github.com/sipeed/picoclaw/pull/3222)** – *refactor(deltachat)* – Open since **2026-07-03**, updated yesterday. No maintainer review or merge. This is a substantial code cleanup that touches a core integration; its stagnation may block other Delta Chat improvements.
- **[Issue #3153](https://github.com/sipeed/picoclaw/issues/3153)** – Closed as stale, but the Volcengine tool‑call leak was never fixed. If still reproducible, it should be re‑opened or tracked elsewhere.
- **[Issue #3197](https://github.com/sipeed/picoclaw/issues/3197) & [#3196](https://github.com/sipeed/picoclaw/issues/3196)** – Same status: closed stale, OAuth login failures unresolved.

The lack of response on recently opened issues (#3260, #3258, #3257) could also become a backlog concern if maintainers do not acknowledge them soon.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-07-16

### 1. Today’s Overview
NanoClaw saw moderate activity over the past 24 hours, with **11 pull requests** updated (4 merged/closed, 7 still open) and **2 issues** updated (1 open, 1 closed). The project advanced significantly on its multi‑provider strategy: a new *OpenCode* provider was merged, and the provider‑agnostic persistent memory system (shared between Claude and Codex) was completed. A critical bug in the delivery retry logic—where transient network failures were permanently dropping agent replies—drew immediate attention and an open fix PR. Operational stability also improved through container idle‑timeout logic and host gateway fixes for macOS VM runtimes. No new releases were published.

### 2. Releases
*None in the last 24 hours.*

### 3. Project Progress
Four pull requests were merged/closed today:

- **#3013** (core-team) – [Load shared memory on session start for Codex](https://github.com/nanocoai/nanoclaw/pull/3013)  
  Adds the Codex counterpart of the provider‑agnostic memory system, registering a `SessionStart` hook for startup/clear/compact (excluding resume).
- **#3012** (core-team) – [Provider‑agnostic persistent memory](https://github.com/nanocoai/nanoclaw/pull/3012)  
  Scaffolds a shared memory tree (`memory/index.md`, `memory/system/definition.md`) for every agent group, loaded on new contexts after startup, clear, and compaction.
- **#3056** – [Add OpenCode as an agent provider](https://github.com/nanocoai/nanoclaw/pull/3056)  
  Introduces the `opencode` provider to the container agent‑runner, spawning an `opencode serve` subprocess and translating NanoClaw MCP server configs.
- **#3055** – [Add deploy.sh for one‑command redeploys](https://github.com/nanocoai/nanoclaw/pull/3055)  
  Provides a `deploy.sh` script that SSH’s into the remote server, pulls latest, installs dependencies, builds, and restarts the service.

Issue **#3054** (stale `agent_message_policies` rows surviving group deletion) was also closed, presumably fixed via the approval‑lifecycle unification in #3040 or a related change.

### 4. Community Hot Topics
The most active discussion remains **Issue #3058** ([Transient outbound failures permanently dropped after 3 fast retries](https://github.com/nanocoai/nanoclaw/issues/3058)), presenting a clear consensus problem: `markDeliveryFailed()` in `src/delivery.ts` treats all failures as permanent after three retries, with no distinction between a network blip and an unrecoverable error. The issue has one comment and a dedicated fix PR (#3059) already open. The underlying need is **resilience against temporary infrastructure hiccups**—a common operational requirement.

No other issues or PRs attracted more than 0 comments or reactions, indicating that the community is highly focused on active development rather than prolonged debate.

### 5. Bugs & Stability

| Severity | Bug | Status |
|----------|-----|--------|
| **High** | **#3058** – Transient send failures permanently dropped after 3 fast retries (no network/permanent distinction). Data loss can occur on brief blips. | Open issue; fix PR #3059 open. |
| **Medium** | **#3054** – `agent_message_policies` rows cause FK failures when their parent group/connection is deleted. CLI destination removal leaves stale gates. | Closed (likely fixed by PR #3040). |
| **Medium** | **#3053** – Container agent‑runner never exits on its own, forcing a 30‑min SIGTERM kill. → **fix PR open**. | Open PR #3053. |
| **Low** | **#3052** – Host gateway not resolved under Colima/Lima/Rancher Desktop (macOS VMs). → **fix PR open**. | Open PR #3052. |
| **Low** | **#3051** – Provider config preflight validation missing before save. → **fix PR open**. | Open PR #3051. |

Operationally, the container idle‑timeout fix (#3053) and host‑gateway resolution (#3052) address recurring pain points for developers using macOS VM runtime alternatives.

### 6. Feature Requests & Roadmap Signals
Several newly merged/opened features hint at the next version’s direction:

- **Automatic Claude → Codex quota fallback** (PR #3057, still open) – per‑agent‑group failover when Claude hits its quota mid‑turn, plus new Telegram/WhatsApp channel adapters and pilot‑activation module. This is the largest pending feature and likely to be included in the upcoming release.
- **Provider‑agnostic persistent memory** (merged #3012 / #3013) – foundational for any multi‑provider deployment. Already available for use.
- **OpenCode provider** (merged #3056) – expands the list of supported agent runtimes beyond Claude and Codex.

The cluster of open PRs around *groups*, *approval lifecycle*, and *provider config validation* (#3040, #3051) suggests that the team is locking down administrative reliability before the next feature push.

### 7. User Feedback Summary
Real user pain points captured today:

- **Delivery resilience**: A user (“mashkovtsevlx”) identified that a transient network timeout leads to permanent message loss, and contributed a fix (PR #3059). This reflects a real operational frustration with the rigid retry logic.
- **Policy cleanup**: User “jguillen1984” reported FK violations when deleting groups/connections because `agent_message_policies` rows were not cleaned up—a data‑integrity issue that affects administrators.
- **Container lifecycle**: User “adamhowell” noted that every session container lingers until the host‑ceiling kill (exit 143), wasting resources—and proposed an idle‑timeout mechanism (PR #3053).
- **macOS Docker alternative compatibility**: User “adamhowell” also surfaced the host‑gateway issue with Colima/Lima, which blocks container networking on many developer machines.

Satisfaction signals include the prompt response from the core team on these issues, and the overall volume of contributions (11 PRs in 24h) indicates a healthy, collaborative development process.

### 8. Backlog Watch
- **PR #2591** (open since 2026-05-22) – [Fix namespace user IDs by channel‑type prefix, not bare colon](https://github.com/nanocoai/nanoclaw/pull/2591) by “mmahmed”. Last updated today, but no maintainer comments or changes requested. This is a long‑standing PR addressing ID collisions across channels; its prolonged open status may indicate a lack of reviewer bandwidth or unresolved design questions. Worth a review cycle soon.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-16

## 1. Today's Overview

The IronClaw project is experiencing **very high activity**, with 23 issues and 38 pull requests updated in the last 24 hours. **8 issues were resolved, and 13 PRs were merged or closed**, indicating steady progress. The team is heavily focused on **stabilizing the Slack channel lifecycle** (the top bug family), **removing the retired v1 runtime**, and extending the **Reborn tier-2 fault-injection test harness**. No new releases were published today. The project remains in a “reborn” transition phase, with significant infrastructure churn and a high volume of regression fixes landing.

## 2. Releases

No new releases in this window.

## 3. Project Progress (Merged/Closed PRs Today)

The following PRs were merged or closed, delivering important fixes and feature work:

- **[#6135** – fix(reborn): recover Slack host after OAuth activation](https://github.com/nearai/ironclaw/issues/6135)  
  *Size XL, risk low.* Re-establishes Slack connectivity after OAuth re-authentication, fixing multiple Slack-related regressions.

- **[#6128** – fix(auth): audit + review blockers — scope ceiling, Notion refresh, fan-out retryability, removal/callback race](https://github.com/nearai/ironclaw/issues/6128)  
  *Size XL, risk low.* Addresses a batch of authentication lifecycle bugs uncovered during code review of the unified extension runtime.

- **[#6055** – test(reborn): StaleSurface same-run refresh pin + extension-remove channel-cleanup integration coverage](https://github.com/nearai/ironclaw/issues/6055)  
  *Size M, risk low.* Adds integration tests for two previously-uncovered production paths (stale surface refresh and extension removal cleanup).

- **[#6084** – feat(webui): replace native confirmations with a shared modal](https://github.com/nearai/ironclaw/issues/6084)  
  *Size M, risk low.* Replaces all native browser `confirm()` dialogs with a reusable Reborn `ConfirmDialog` component for chat deletion, automation deletion, and extension removal.

- **[#6082** – fix(webui-v2): render extension registry without enrichment delay](https://github.com/nearai/ironclaw/issues/6082)  
  *Size S, risk low.* Eliminates the 10-second loading delay by rendering registry cards immediately and then progressively enriching them.

**Notable open PRs still in progress** include the massive **v1 runtime removal** ([#6123](https://github.com/nearai/ironclaw/issues/6123), size XL, DB migration), the **unified generic extension runtime** ([#6116](https://github.com/nearai/ironclaw/issues/6116), size XL), and the **OAuth flow-lifecycle hygiene** fix ([#6130](https://github.com/nearai/ironclaw/issues/6130), size XL).

## 4. Community Hot Topics

The most active discussions (by comment count) revolve around **Slack reliability** and **channel lifecycle testing**:

- **[Issue #6105** – Extension/channel lifecycle state-machine test](https://github.com/nearai/ironclaw/issues/6105)  
  *3 comments, opened 2026-07-14.* This issue is the **#1 user-facing bug family** (Slack lifecycle regressions across four QA waves). It calls for a comprehensive test covering install→connect→disconnect→reconnect→uninstall. The associated PR [#6113](https://github.com/nearai/ironclaw/issues/6113) (M-sized, open) already delivers tests for five priority transitions.

- **[Issue #5834** – Slack disconnect request is incorrectly rejected by agent](https://github.com/nearai/ironclaw/issues/5834)  
  *3 comments, opened 2026-07-08.* P2 bug where the agent refuses to disconnect Slack, leaving users unable to remove the integration. This is part of the larger Slack lifecycle regression cluster.

- **[Issue #3533** – [CLOSED] Telegram in v0.28.1 does not automatically setup from UI](https://github.com/nearai/ironclaw/issues/3533)  
  *3 comments, closed today.* A historical bug that was finally resolved, indicating ongoing cleanup of older, unfixed issues.

**Underlying need**: Users are demanding **reliable, tested channel lifecycle management** – especially for Slack – after repeated regressions in QA. The team is responding with dedicated testing infrastructure (tier-2 harness, state machine tests) and targeted fixes.

## 5. Bugs & Stability

**Severity P1** (critical user-facing bugs reported today or still active):

| Issue | Summary | Fix PR status |
|-------|---------|---------------|
| [#5943](https://github.com/nearai/ironclaw/issues/5943) – P1 | Slack DM action posts to current channel instead of user’s DM | Open, no fix PR yet |
| [#5877](https://github.com/nearai/ironclaw/issues/5877) – P1 | Slack notification delivered to wrong user | Open, no fix PR yet |
| [#5944](https://github.com/nearai/ironclaw/issues/5944) – P2 | Slack DM silently fails but run reports success | Open, no fix PR yet |
| [#6125](https://github.com/nearai/ironclaw/issues/6125) – P2 | User message rejected with “busy” error while routine runs in background | Open – new today |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) – P2 | Repeated Slack reconnects leave auth flow broken | Open, no fix PR yet |

**New bugs reported today (2026-07-15/16):**

- **[#6138](https://github.com/nearai/ironclaw/issues/6138)** – Tier-2 harness can’t express compound denied-gate + HTTP-egress-error scenario. Found while building fault-injection coverage.
- **[#6137](https://github.com/nearai/ironclaw/issues/6137)** – Mixed-batch gate resume never redispatches the non-first gated call. Prevents approval workflows from completing correctly.
- **[#6136](https://github.com/nearai/ironclaw/issues/6136)** – WebChatV2Event `accepted`/`cancelled`/`failed` variants are dead code (no production constructor). Indicates incomplete SSE event coverage.
- **[#6127](https://github.com/nearai/ironclaw/issues/6127)** – P3: Running routine incorrectly displays “Previous run still in progress” on first execution.
- **[#6126](https://github.com/nearai/ironclaw/issues/6126)** – P3: First message in a new chat has no loading or streaming state (blank screen).
- **[#6117](https://github.com/nearai/ironclaw/issues/6117)** – Workspace UI displays untranslated region names and raw file sizes (localization gap).
- **[#6118](https://github.com/nearai/ironclaw/issues/6118)** – Admin UI lacks per-user secrets management (feature request, but also a missing capability).

**Closed bugs**: [#5741](https://github.com/nearai/ironclaw/issues/5741) (builtin.http.save fails with OutputTooLarge), [#6052](https://github.com/nearai/ironclaw/issues/6052) (Extensions Registry slow load), [#6044](https://github.com/nearai/ironclaw/issues/6044) (Enter key not submitting), [#6085](https://github.com/nearai/ironclaw/issues/6085) (broken Create token action), [#5886](https://github.com/nearai/ironclaw/issues/5886) (pending approval blocks subsequent runs), [#6083](https://github.com/nearai/ironclaw/issues/6083) (native confirmations replaced), [#6087](https://github.com/nearai/ironclaw/issues/6087) (extension catalog empty state on failure).

## 6. Feature Requests & Roadmap Signals

The following user-facing gaps and roadmap items emerged from today’s data:

- **[#6105](https://github.com/nearai/ironclaw/issues/6105)** – **Channel lifecycle state-machine test infrastructure** is actively being built (PR [#6113](https://github.com/nearai/ironclaw/issues/6113) delivers tests). Likely to be a high-priority stable feature in the next release.
- **[#6118](https://github.com/nearai/ironclaw/issues/6118)** – **Per-user secrets management in Admin UI**. The backend API already supports it; the frontend is missing. Expected in a near-term WebUI update.
- **[#6117](https://github.com/nearai/ironclaw/issues/6117)** – **Workspace UI localization and human-readable file sizes**. Low impact but improves UX; might ship as part of a broader UI polish release.
- **[#6123](https://github.com/nearai/ironclaw/issues/6123)** – **Remove retired v1 runtime** (XL PR, DB migration). This is a major internal refactor that signals the project’s full commitment to the Reborn architecture. Likely to land in the next major version (0.30+).
- **[#6130](https://github.com/nearai/ironclaw/issues/6130)** – **OAuth flow-lifecycle hygiene** (supersede-on-start, durable PKCE, expiry-honest projections). This is a fix for live, user-facing OAuth bugs; could be cherry-picked into a patch release.

## 7. User Feedback Summary

**Pain points** (derived from bug reports and comments):

- **Slack integration is unreliable.** Users experience: DMs not delivered (even with green checkmarks), messages posted to wrong channels/recipients, inability to disconnect, and authentication that breaks after repeated reconnects.
- **UI feels unresponsive.** First messages show no loading indicator (blank screen), Extensions Registry loads slowly, and the Enter key intermittently fails to submit.
- **Automation routines lock out users.** When a routine runs, user messages are rejected with a “busy” error, and the UI shows misleading “Previous run still in progress” status on the first execution.
- **Admin tools are incomplete.** No way to manage per-user secrets from the UI; Create token button leads to a dead action.

**Use cases** driving these issues:
- Users relying on Slack DMs for workflow notifications.
- Operations teams running recurring routines (e.g., hourly monitoring) who need to interrupt with follow-up queries.
- Administrators provisioning API tokens for new users.

**Satisfaction indicators**: The team is actively fixing these issues (5 tickets closed today, 13 PRs merged), which may improve sentiment. However, the repeated regression across QA waves (noted in [#6105](https://github.com/nearai/ironclaw/issues/6105)) suggests frustration is building – the same Slack bugs keep resurfacing despite multiple fixes.

## 8. Backlog Watch

Issues and PRs that have remained open for an extended period without resolution:

- **[#5834](https://github.com/nearai/ironclaw/issues/5834)** – Slack disconnect rejected (P2, opened 2026-07-08, 8 days). Still no fix PR; part of the critical Slack lifecycle cluster.
- **[#5882](https://github.com/nearai/ironclaw/issues/5882)** – Repeated Slack reconnects break auth (P2, opened 2026-07-09, 7 days). No fix PR.
- **[#5877](https://github.com/nearai/ironclaw/issues/5877)** – Slack notification wrong user (P1, opened 2026-07-09, 7 days). No fix PR.
- **[#5943](https://github.com/nearai/ironclaw/issues/5943)** – Slack DM posts to wrong channel (P1, opened 2026-07-10, 6 days). No fix PR.
- **[#5944](https://github.com/nearai/ironclaw/issues/5944)** – Slack DM silent failure (P2, opened 2026-07-10, 6 days). No fix PR.
- **[#5910](https://github.com/nearai/ironclaw/issues/5910)** – PR: fix approval gates on notification open (L-sized, opened 2026-07-10, 6 days). Still open with no recent activity. This could unblock several approval-related bugs.
- **[#5598](https://github.com/nearai/ironclaw/issues/5598)** – Release PR (ironclaw common 0.5.0 breaking). Opened 2026-07-03, 13 days. A new release has been pending for nearly two weeks, likely blocked by the Slack regression churn. Breaking changes in `ironclaw_common` and `ironclaw_skills` may be delaying the release.

**Maintainer attention needed**: The **Slack lifecycle bugs** have gone unfixed for over a week despite being P1/P2 and affecting multiple users. The [release PR #5598](https://github.com/nearai/ironclaw/issues/5598) should be triaged – either merge or decide to hold for a more stable point. The project would benefit from a dedicated release branch or a hotfix release to address the Slack regressions before shipping the next major version.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-16

## Today's Overview

The project saw a high-activity day with 17 PRs updated (11 merged/closed) and a new patch release (v2026.7.15). Five stale, older issues were closed as inactive, while one fresh user issue (#2342) was opened about a newly introduced bottom-left advertisement. The release cycle appears to be moving quickly, with multiple fixes and feature additions landing in the past 24 hours. Overall project health is strong, with a clear focus on polish (UI, update flow, settings) and model support (GPT-5.6, Grok 4.5).

## Releases

**v2026.7.15** — [Release Notes](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.15)

- **New features**:
  - Optimized file card display.
  - Added opt-in Windows web installer target (build).
  - Revamped homepage quick-action scenario (cowork).
- **Notable changes**: No breaking changes or migration notes mentioned. The release appears to be a minor patch.

## Project Progress

**Merged/closed PRs today (11 total):**

| PR # | Title | Area | Summary |
|------|-------|------|---------|
| [#2341](https://github.com/netease-youdao/LobsterAI/pull/2341) | Release/2026.7.13 | multiple | Patch release merge. |
| [#2340](https://github.com/netease-youdao/LobsterAI/pull/2340) | Revert "fix: fixed model not allowed" | renderer, docs, main, openclaw, cowork | Reverted a previous model fix. |
| [#2339](https://github.com/netease-youdao/LobsterAI/pull/2339) | fix(update): align update card header content | renderer | Improved title truncation and responsive alignment in narrow sidebars. |
| [#2338](https://github.com/netease-youdao/LobsterAI/pull/2338) | feat(update): refine the blocking update overlay | renderer | Centered update progress, scrollable release notes, error recovery, keyboard focus lock. |
| [#2337](https://github.com/netease-youdao/LobsterAI/pull/2337) | fix: fixed model not allowed | renderer, docs, main, openclaw, cowork | Fixed model permission bug. (Later reverted by #2340) |
| [#2336](https://github.com/netease-youdao/LobsterAI/pull/2336) | feat(settings): group General settings into labeled cards | renderer, main | Reorganized General settings into sections (basics, notifications, data & privacy). Merged permission and question notification toggles. |
| [#2335](https://github.com/netease-youdao/LobsterAI/pull/2335) | fix: fixed content copy bug | renderer, artifacts | Fixed copying content failure. |
| [#2334](https://github.com/netease-youdao/LobsterAI/pull/2334) | fix(cowork): restore IM session loading state | renderer, main | Subscribed to gateway session lifecycle events, kept polling as fallback. Prevented cron/desktop events from affecting IM loading. |
| [#2333](https://github.com/netease-youdao/LobsterAI/pull/2333) | feat(update): block app interactions during user-initiated updates | renderer | Added lightweight overlay during downloads/installs, restores on cancel/failure. |
| [#2332](https://github.com/netease-youdao/LobsterAI/pull/2332) | feat(providers): add GPT-5.6 and Grok 4.5 default models | renderer, main, openclaw | Introduced versioned model migration path to avoid duplicate user customizations. |
| [#1372](https://github.com/netease-youdao/LobsterAI/pull/1372) | 修复会话中多文件选择只保留最后一个文件的问题 | renderer | Fixed multi-file attachment bug in cowork input; added 8 Vitest unit tests. |

**Key advancements:** UI/UX polishing (update overlay, settings cards, copy fix), model provider expansion (GPT-5.6, Grok 4.5), cowork IM loading stability, and a long-standing file attachment bug fix.

## Community Hot Topics

- **Issue #2342** ([link](https://github.com/netease-youdao/LobsterAI/issues/2342)) — *“左下角广告可以彻底关闭吗”* (Can the bottom-left ad be permanently disabled?)  
  Opened today (1 comment, 0 reactions). User reports a new advertisement in v2026.7.15 and requests a permanent disable option. High user impact, likely to be addressed in next patch.

- **Issue #1381** ([link](https://github.com/netease-youdao/LobsterAI/issues/1381)) — *Cron tasks create new sessions each run* (closed as stale).  
  Underlying need: Users want scheduled tasks to reuse existing conversation windows to reduce clutter. Not yet resolved.

- **Issue #1385** ([link](https://github.com/netease-youdao/LobsterAI/issues/1385)) — *WeChat bot: deleting session doesn't clean history on re-query* (closed stale).  
  Persistent UX issue for WeChat bot users; no fix PR identified yet.

## Bugs & Stability

| Issue | Severity | Status | Notes |
|-------|----------|--------|-------|
| [#2342](https://github.com/netease-youdao/LobsterAI/issues/2342) – Unwanted persistent ad | Medium | Open, today | Affects all users of v2026.7.15. No fix PR yet, but likely to be addressed quickly. |
| [#1384](https://github.com/netease-youdao/LobsterAI/issues/1384) – Multi-file upload only shows last file (closed stale) | Medium | Closed (fix PR #1372 merged today) | **Resolved.** |
| [#1383](https://github.com/netease-youdao/LobsterAI/issues/1383) – WeChat bot duplicate text sync issue (closed stale) | Low | Closed | Still not fully fixed; was closed due to inactivity. |
| [#2337](https://github.com/netease-youdao/LobsterAI/pull/2337) – Model not allowed (merged then reverted) | Medium-High | Reverted | Regression potential; revert indicates the fix introduced other issues. Monitoring needed. |
| [#1322](https://github.com/netease-youdao/LobsterAI/pull/1322) – LRU eviction not working in cowork memory judge (stale open) | Medium | Open (stale) | PR exists since April, not merged. Cache eviction bug still present. |

## Feature Requests & Roadmap Signals

- **Persistent ad disable toggle** — requested today (#2342). Likely to appear in next hotfix as a settings option.
- **WeChat bot session history cleanup** — multiple user reports (#1385) imply a need for consistent lifecycle management across platforms.
- **Cron task consolidation** (#1381) — users want scheduled task output in same session. Could be considered for cowork roadmap.
- **Model migration path** (already implemented in #2332) — indicates proactive support for upcoming models (GPT-5.6, Grok 4.5).

## User Feedback Summary

- **Positive**: Quick iteration on UI polish (update overlay, settings organization, copy fix). Users likely appreciate the improved visual consistency.
- **Pain points**:
  - The new advertisement is seen as intrusive and lacks a permanent off switch.
  - WeChat bot history management remains confusing (deleted sessions not cleaned).
  - Multi-file upload bug, though fixed, frustrated users who encountered it.
- **Overall sentiment**: Users are active (many bug reports in April), but recent release shows responsiveness to community issues. The advert backlash may temporarily affect satisfaction.

## Backlog Watch

- **PR #1322** ([link](https://github.com/netease-youdao/LobsterAI/pull/1322)) — *fix(cowork): true LRU eviction for LLM memory judge cache*  
  Open since April 2, no updates. Addresses a real performance bug in cowork memory cache. Needs maintainer review/merge.

- **PR #1277** ([link](https://github.com/netease-youdao/LobsterAI/pull/1277)) — *chore(deps-dev): bump electron group*  
  Open since April, still not merged. Keeps Electron and electron-builder dependencies updated. Security/stability risk if left too long.

- **Issue #1385** (closed stale) — WeChat bot session cleanup still unresolved. Might need a new issue or PR to reopen the discussion.

- **Dependabot PRs #2164–2167** — Open since June 15. They involve CI tool updates (trufflehog, actions/stale, actions/checkout, paths-filter). No activity; low priority but should be reviewed eventually.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw Project Digest — 2026-07-16

## 1. Today’s Overview
Project TinyClaw experienced very low activity in the past 24 hours. No new issues were created or updated, and no releases were published. One open pull request (#295) was updated, targeting a logic bug in the CLI’s team removal command. No changes were merged, and community engagement remains minimal. Overall, the project appears to be in a quiet maintenance phase.

## 2. Releases
*None at this time.*

## 3. Project Progress
No pull requests were merged or closed today. The only open PR (#295) is still under review.

## 4. Community Hot Topics
- **[PR #295 – fix(cli): print the "New leader" note after removing a team leader](https://github.com/TinyAGI/tinyagi/pull/295)**  
  *Author: Osamaali313*  
  *Created: 2026-07-15 | Updated: 2026-07-15 | Comments: 0 | 👍: 0*  
  This is the only active item. It addresses a conditional bug in `teamRemoveAgent` where the success message always prints a "New leader" note incorrectly because the condition compares the leader before it is reassigned. The underlying need is to correct misleading CLI output and improve user confidence when managing team leaders.

## 5. Bugs & Stability
- **Moderate – CLI team leader removal message logic**  
  The bug reported in PR #295 causes the CLI to always display "New leader: …" even when a new leader was just assigned, because the condition checks the old leader reference against the new one *before* the assignment is persisted. This does not break functionality but misleads users. A fix PR exists but has not been merged yet.

## 6. Feature Requests & Roadmap Signals
No feature requests or roadmap signals were observed in the last 24 hours.

## 7. User Feedback Summary
No user feedback, pain points, or satisfaction signals were recorded on GitHub during this period.

## 8. Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention were identified in the available data.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-16

## 1. Today’s Overview
Project activity remains solid with **6 pull requests merged** in the last 24 hours, covering provider fixes, new model support, ACP agent auto-detection, and CLI improvements. The only open issue (a feature request for per‑topic model routing) received its first comment after three months, indicating renewed user interest. No new releases were published. Overall, the project shows healthy maintenance velocity with a clear focus on provider robustness and external agent integration.

## 2. Releases
*None.* No new releases were cut today.

## 3. Project Progress
All six PRs updated in the last 24 hours were merged. Notable advances:

- **New model support** – [PR #1151](https://github.com/moltis-org/moltis/pull/1151) added MiniMax M3 to the model registry while retaining M2.7, with documentation for global and China endpoints.
- **Authentication fix** – [PR #1152](https://github.com/moltis-org/moltis/pull/1152) resolved a critical token‑expiry dead end in the `openai-codex` provider that caused session drops after ~10 days.
- **Context window improvements** – [PR #1150](https://github.com/moltis-org/moltis/pull/1150) centralised context‑window mappings and enabled dynamic providers (Copilot/Codex) to parse live model metadata.
- **ACP agent auto‑detection** – [PR #1149](https://github.com/moltis-org/moltis/pull/1149) added named external‑agent kinds for 13 ACP adapters (Claude, Gemini, Augment, OpenHands, etc.) with automatic capability detection.
- **CLI service fallback** – [PR #1153](https://github.com/moltis-org/moltis/pull/1153) introduced a systemd‑less fallback for containers (Coder/devbox), managed by a supervisor script.
- **Dependency updates** – [PR #1148](https://github.com/moltis-org/moltis/pull/1148) bumped `esbuild` and `vite` across `/crates/web/ui` and `/docs`.

## 4. Community Hot Topics
The only open issue updated today is the highest‑activity item:

- **[Issue #574 – Model Routing Per Topic](https://github.com/moltis-org/moltis/issues/574)**  
  *Author: azharkov78* | *Created: 2026-04-06* | *Updated: 2026-07-15* | *Comments: 1* | *👍: 1*  
  The user requests the ability to route different conversation topics to different models (e.g., use a fast model for casual chat and a heavy model for coding). The single comment (by the same author) likely provides additional context. The underlying need is flexibility in multi‑purpose assistants – users want to optimise cost/latency without manually switching providers.

No PRs generated notable discussion (all had 0 comments and 0 reactions).

## 5. Bugs & Stability
Two bugs were fixed today, both with matching merged PRs:

- **Critical: Token‑expiry dead end in `openai-codex`** (fixed in [#1152](https://github.com/moltis-org/moltis/pull/1152)) – sessions failed after ~10 days with no recovery other than re‑login. The fix derives expiration from the JWT `exp` claim.
- **Medium: Missing context window values for dynamic providers** (fixed in [#1150](https://github.com/moltis-org/moltis/pull/1150)) – incorrect or null context windows caused silent truncation errors. The PR adds fallback mappings and capability‑based derivation.
- **Low: No service management in containers without systemd** (fixed in [#1153](https://github.com/moltis-org/moltis/pull/1153)) – users inside dev containers couldn’t start/stop Moltis services. Now a supervisor script handles `install`, `status`, `stop`, `restart`, and `uninstall`.

No new bugs or regressions were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
One feature request is active:

- **[Issue #574 – Model Routing Per Topic](https://github.com/moltis-org/moltis/issues/574)**  
  Suggests a rule‑based or heuristic router to assign different LLMs per conversation context. Given the recent work on provider flexibility (MiniMax M3, dynamic context windows, ACP agents), this feature aligns with the project’s trajectory. It could appear in the next minor release if the team decides to implement a simple routing DSL.

Additionally, the merged PR [#1149](https://github.com/moltis-org/moltis/pull/1149) for ACP agent auto‑detection signals a roadmap priority: making Moltis interoperable with a growing ecosystem of external agents.

## 7. User Feedback Summary
- **Pain point** – The `openai-codex` token expiry issue (fixed in #1152) was a significant frustration for users relying on that provider; the fix eliminates a recurring failure.
- **Use case** – The request for topic‑based routing (issue #574) reflects a desire to combine multiple models in a single session, a common pattern in advanced AI assistants.
- **Satisfaction** – No specific positive or negative feedback was recorded today, but the high merge rate suggests maintainer responsiveness, which generally correlates with user satisfaction.

## 8. Backlog Watch
Only one open issue exists in the provided data, and it is the feature request [#574](https://github.com/moltis-org/moltis/issues/574). It has been open for over three months with no maintainer comment. While it received an update (user comment) on July 15, it still lacks an official triage label or assignee. Given the single `👍` reaction, it may not be a top priority, but the project should consider acknowledging it to signal openness to community input.

No other stuck or unanswered items are visible in this snapshot.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-16

## Today’s Overview

CoPaw (also referred to as QwenPaw) saw very high activity in the last 24 hours, with **50 issues** and **43 PRs** updated. Of those, 32 issues were closed and 22 PRs were merged or closed, indicating an active maintenance cycle. No new releases were published. The community is engaged, reporting several bugs related to the recent v2.0 upgrade (e.g., memory leaks, context loss, and silent message drops) while also requesting important features like enterprise OS support and pre-built agent templates. Overall, the project is moving fast but grappling with stability regressions introduced in the latest major version.

## Releases

No new releases today.

## Project Progress

**Merged/Closed PRs (selected):**

- **#6147** – [feat(website): add blog view/like counts and switch GA to QwenPaw property](https://github.com/agentscope-ai/QwenPaw/pull/6147)  
  *Ready for human review, closed.* Adds Supabase-backed view counts and Google Analytics integration for the project website.

- **#6140** – [fix(utils): add `errors='replace'` to `_run_command` for GBK compatibility](https://github.com/agentscope-ai/QwenPaw/pull/6140)  
  Fixes command output decoding errors on Windows GBK environments.

- **#6143** – [ci: pass Supabase config to website build](https://github.com/agentscope-ai/QwenPaw/pull/6143)  
  CI fix to enable Supabase in deployment builds.

- **#6142** – [fix(console): require `auto_memory_interval` as int >= 0, disallow empty](https://github.com/agentscope-ai/QwenPaw/pull/6142)  
  Validation fix; allows setting zero to disable automatic memory, solving a usability loophole described in issue #6132.

- **#6039** – [fix(mcp): resolve `${VAR}` env references in legacy driver migration](https://github.com/agentscope-ai/QwenPaw/pull/6039)  
  *First-time contributor.* Fixes a regression where environment variable references were not expanded during MCP credential migration, breaking tools like Wind MCP.

- **#6137** – [fix(loop): fine-tune doom loop limits and preserve spaces in thinking blocks](https://github.com/agentscope-ai/QwenPaw/pull/6137)  
  Dual fix: adjusts model repetition loop thresholds and fixes whitespace trimming in thinking/reasoning blocks.

Additionally, **open PRs** that advanced today include fixes for desktop caching, multimodal image stripping, scroll context limits, and a new Chrome extension plugin (PR #6157).

## Community Hot Topics

**Most discussed issues (by comment count):**

- **#2911** (6 comments, closed) – *Windows client closes itself after a few hours*  
  https://github.com/agentscope-ai/QwenPaw/issues/2911  
  A persistent crash bug affecting all versions up to 1.0.1b1. Closed, but no fix publicised.

- **#6129** (5 comments, open) – *Missing spaces and line feeds in thinking blocks*  
  https://github.com/agentscope-ai/QwenPaw/issues/6129  
  Reported in v2.0.0.post2; frontend rendering bug that breaks reasoning display. A fix PR (#6139) is already open.

- **#6125** (5 comments, open) – *Plans to support Kylin OS (Galaxy Kylin)*  
  https://github.com/agentscope-ai/QwenPaw/issues/6125  
  Feature request from government/enterprise users for a domestic Chinese Linux distribution.

- **#2969** (5 comments, closed, 👍3) – *Add personal knowledge base functionality*  
  https://github.com/agentscope-ai/QwenPaw/issues/2969  
  Highly upvoted request to integrate RAG/knowledge base directly into the console.

- **#5995** (3 comments, open) – *Messages silently dropped when session is busy*  
  https://github.com/agentscope-ai/QwenPaw/issues/5995  
  Critical reliability issue in Feishu channel—new messages are lost when agent is processing a previous request.

- **#6148** (2 comments, open) – *Severe memory loss after upgrading to 2.0*  
  https://github.com/agentscope-ai/QwenPaw/issues/6148  
  User reports that `/compact` does not actually compress context, leading to truncated conversations.

**Most upvoted:** #2969 (3 👍) signals strong desire for a built-in knowledge base feature.

## Bugs & Stability

**High-severity bugs reported today (2026-07-15):**

1. **Memory leak during startup (editable install)** – #6124  
   https://github.com/agentscope-ai/QwenPaw/issues/6124  
   36 ReMe background loops consume 48GB+ RAM and never complete. Affects 2.0.0.post2 on Windows. No fix PR yet.

2. **Silent message dropping** – #5995  
   https://github.com/agentscope-ai/QwenPaw/issues/5995  
   Feishu channel drops incoming messages when session is busy; no queue, no error logged.

3. **Context/“memory loss” after upgrade to 2.0** – #6148  
   https://github.com/agentscope-ai/QwenPaw/issues/6148  
   `/compact` acts as simple truncation instead of intelligent compression, causing amnesia.

4. **MODEL_EXECUTION_ERROR after mission abort** – #6141  
   https://github.com/agentscope-ai/QwenPaw/issues/6141  
   Conversation becomes unusable after aborting a multi-worker analysis; tool messages mismatch.

5. **Embedding mapping and auto-memo issues** – #6155  
   https://github.com/agentscope-ai/QwenPaw/issues/6155  
   `use_dimensions` not passed to embedding config, failure with local models.

6. **Loading animation stuck** – #5790  
   https://github.com/agentscope-ai/QwenPaw/issues/5790  
   Console frontend shows spinner after agent finishes.

**Fix PRs known to address these:**
- #6139 fixes #6129 (spaces in thinking blocks)
- #6123 fixes #6148 (scroll context limits and compaction)
- #6153 fixes #6155 (ReMe config and indexing safeguards)
- #6154 fixes #6155 and other multimodal image stripping issues
- #6138 and #6137 address doom loop thresholds (related to #6148 / #6116)

## Feature Requests & Roadmap Signals

**Top requested features (with underlying user needs):**

- **Enterprise OS support** (#6125) – Demand for Kylin OS (domestic Chinese Linux). Suggests growing government/enterprise adoption.
- **Personal knowledge base** (#2969, 👍3) – Users want to attach files/docs for agent to reference directly in the console.
- **Pre-built agent templates** (#4259) – Lower barrier for non-technical users; would reduce manual prompt/skill configuration.
- **Multiple channel session sharing** (#2899) – Ability to continue a conversation across different messaging apps.
- **LSP support & fallback models** (#2912) – Developer-focused features for better code editing and model resilience.
- **Whisper voice input** (#2910) – Browser voice input broken; want API or local Whisper integration.
- **Claude Code agent team functionality** (#2922) – Multi-agent collaboration is currently stiff and lacks shared context.
- **Zulip channel integration** (#2921) – Open-source Slack alternative.
- **Desktop workspace shortcut** (#6083) – One-click access to agent output files from Tauri app.
- **Non-Tauri variant for Win7** (#6076) – Legacy OS support.

**Likely roadmap items:**  
Give the community intensity, agent templates (#4259) and knowledge base (#2969) could ship in the next minor version. The ongoing work on memory/context management (PRs #6123, #6153) suggests improved ReMe integration is a priority. The Chrome extension PR (#6157) and PawApp SDK (#6150) hint at a broader platform strategy.

## User Feedback Summary

**Real pain points voiced:**

- **v2.0 regression (memory loss, fatal errors, bugs)** – Multiple users (e.g., #6148, #6141, #6155) express frustration with the upgrade. The `/compact` feature is perceived as broken.
- **Agent collaboration is weak** (#6136) – Users want a “leader” agent to autonomously delegate to other agents without explicit prompts.
- **Desktop user experience gaps** (#6083) – Accessing workspace files is cumbersome; users want in-app file browser.
- **Enterprise deployment barriers** (#6125, #6076) – Lack of support for Chinese domestic OS and Windows 7 hinders adoption in certain sectors.
- **Missing advanced features** (LSP, Zulip, knowledge base) – Repeated requests indicate the current feature set does not fully satisfy power users.

**Satisfaction signals:**  
Despite issues, users are enthusiastic (“特别棒的项目” in #6125, #6076) and actively suggest improvements. The high number of feature requests (50+ open issues) shows strong engagement.

## Backlog Watch

**Issues/PRs needing maintainer attention:**

- **#5995** (open, 3 comments) – Silent message dropping in Feishu channel. No assignee or fix PR. High severity, especially for production use.
- **#6124** (open, 2 comments) – Memory leak during startup (48GB+). No fix yet. Could block users with limited RAM.
- **#6148** (open, 2 comments) – Memory loss in v2.0. Despite related PR #6123, the issue itself remains open and needs a clear resolution.
- **#2911** (closed) – Windows client crash was closed without a fix explanation. Should be reopened or documented.
- **#2907** (closed question) – PR #2448 needing review. The original PR might have been merged, but the question indicates a pending dependency.
- **#6136** (open, 2 comments) – Difficulty triggering agent collaboration. Feature request with no reply from maintainers yet.
- **#6076** (open, 2 comments) – Non-Tauri variant for Win7. Important for legacy enterprise users.

The project maintainers should prioritize the memory leak (#6124) and message dropping (#5995) as they directly impact usability and reliability.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-16

## 1. Today’s Overview

ZeroClaw remains in a high-velocity cycle with **38 issues** and **50 pull requests** updated in the last 24 hours, alongside the release of **v0.8.3** (379 commits, 56 contributors). Activity is concentrated on the new Standard Operating Procedure (SOP) engine, WebAssembly plugin host, and a broad security hardening wave. The project also saw closure of 12 PRs and 20 issues, indicating steady resolution of both bugs and feature work. The community continues to engage deeply around provider reliability, authentication architecture, and memory isolation.

## 2. Releases

### v0.8.3 — Consolidation Cycle
- **Commits:** 379 | **Contributors:** 56  
- **Key highlights:**  
  - Standard Operating Procedure (SOP) engine (daemon-owned control plane)  
  - WebAssembly plugin host (`runtime:wasm`)  
  - Git forge channel  
  - Broad runtime, provider, and security hardening  
- **Breaking changes / migration notes:** None formally documented; this is a consolidation release. Users should review the official changelog for any minor API shifts.  
- **Release link:** [ZeroClaw v0.8.3](zeroclaw-labs/zeroclaw/releases/tag/v0.8.3)

## 3. Project Progress

**Merged/closed PRs in the last 24h (12 total):**

| PR | Summary | Type |
|---|---|---|
| [#9098](zeroclaw-labs/zeroclaw/pull/9098) | ci: raise build matrix timeout to 90 min (fix v0.8.3 timeout) | CI fix |
| [#9062](zeroclaw-labs/zeroclaw/pull/9062) | gate `execute_pipeline` sub-tools by per-agent access policy | Fix / security |
| [#9060](zeroclaw-labs/zeroclaw/pull/9060) | normalize malformed native tool‑call arguments before outbound requests | Fix (provider) |
| [#8672](zeroclaw-labs/zeroclaw/pull/8672) | multi-user auth providers, permission profiles, principal isolation | Feature (security) |
| [#8754](zeroclaw-labs/zeroclaw/pull/8754) | schema V4 cut of skills, inert tunable, summary_model cruft | Breaking config change |
| [#8838](zeroclaw-labs/zeroclaw/pull/8838) | idle-bound SSE streaming on shared transport | Fix (provider reliability) |
| [#8845](zeroclaw-labs/zeroclaw/pull/8845) | rebuild live sessions on `agents.<alias>.model_provider` edits | Fix (daemon) |
| [#8901](zeroclaw-labs/zeroclaw/pull/8901) | strip comment bureaucracy across tree; gate in CI | Refactor / CI |
| [#9070](zeroclaw-labs/zeroclaw/pull/9070) | flush open `tool_use` block at `message_stop` (Anthropic) | Fix (provider) |
| [#9071](zeroclaw-labs/zeroclaw/pull/9071) | log agent init failure on `session/new` (ACP) | Fix (logging) |
| [#9083](zeroclaw-labs/zeroclaw/pull/9083) | trim context overflow to model window, attribute compactions | Fix (runtime) |
| [#9090](zeroclaw-labs/zeroclaw/pull/9090) | enforce tool-call pairing at one canonical chokepoint | Fix (agent loop) |

**Key feature advances:**
- The **multi‑user auth stack** ([#8672](zeroclaw-labs/zeroclaw/pull/8672)) lands the RFC #7141 OIDC provider and permission profiles.
- **Schema V4** ([#8754](zeroclaw-labs/zeroclaw/pull/8754)) retires legacy channels and tools, reducing config surface.
- **SSE streaming reliability** ([#8838](zeroclaw-labs/zeroclaw/pull/8838)) adds per-read idle timeouts to prevent hangs.
- **SOP approval broker** ([#8880](zeroclaw-labs/zeroclaw/pull/8880) – open) adds group membership and quorum for SOP gates.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal three key areas of concern:

### 🔴 Provider reliability & compatibility
- **[#5600](zeroclaw-labs/zeroclaw/issues/5600)** – `kimi-code` streaming call with tools fails (`400 Bad Request: "thinking is enabled but reasoning_content missing"`). **12 comments**, open, P1.  
  *Need:* Accurate provider parity for streaming + tool calls, especially for non‑OpenAI providers.
- **[#7141](zeroclaw-labs/zeroclaw/issues/7141)** – RFC: OIDC authentication provider (7 comments). Closed but foundational.

### 🧠 Memory & context architecture
- **[#9048](zeroclaw-labs/zeroclaw/issues/9048)** – Separate conversation history from agent-curated long-term memory. **4 comments**, open, P2.  
  *Need:* Clearer lifecycle separation to avoid unintended cross‑contamination.
- **[#6641](zeroclaw-labs/zeroclaw/issues/6641)** – Turn-level OTel trace correlation (6 comments, in‑progress).  
  *Need:* Observability around multi‑step agent turns.

### 🛡️ Security & audit
- **[#7142](zeroclaw-labs/zeroclaw/issues/7142)** – Pluggable security enforcement provider (5 comments, closed).
- **[#6293](zeroclaw-labs/zeroclaw/issues/6293)** – Air-gapped execution mode with companion daemon (5 comments, closed).  
  *Need:* Production‑grade security isolation.

**Underlying needs:** Users are demanding **reliable multi‑provider support**, **observability into agent reasoning**, and **robust security defaults** that don’t break workflows.

## 5. Bugs & Stability

### High-severity (P1 / S1) bugs reported today

| Issue | Severity | Behaviour | Fix PR exists? |
|---|---|---|---|
| [#9089](zeroclaw-labs/zeroclaw/issues/9089) | S2 – degraded | `[AUDIO:]` markers not parsed; sent as literal text. Tool output audio not rendered. | No open PR yet |
| [#9092](zeroclaw-labs/zeroclaw/issues/9092) | S2 – degraded | ZeroCode TUI keystroke lag in long sessions (full history rendering). | No |
| [#8559](zeroclaw-labs/zeroclaw/issues/8559) | S1 – workflow blocked | Agents stop when user exits web dashboard chat window. | No (open) |
| [#8794](zeroclaw-labs/zeroclaw/issues/8794) | S1 – workflow blocked | Stopping agent mid‑work erases tool calls/thinking from context. | No (open) |

### Closed bugs with fixes

| Issue | PR fixing it |
|---|---|
| [#8560](zeroclaw-labs/zeroclaw/issues/8560) – `browser_open` hangs on headless host | Widespread fix in #8838 (idle timeout) |
| [#8519](zeroclaw-labs/zeroclaw/issues/8519) – `cargo audit` / CVE drift | Part of #8901 sweeping changes |
| Provider tool-call argument malformation | [#9060](zeroclaw-labs/zeroclaw/pull/9060) |
| Anthropic tool_use flush at message_stop | [#9070](zeroclaw-labs/zeroclaw/pull/9070) |
| Agent initialization failure not logged (ACP) | [#9071](zeroclaw-labs/zeroclaw/pull/9071) |
| Context overflow recovery too aggressive | [#9083](zeroclaw-labs/zeroclaw/pull/9083) |

**Takeaway:** While provider and runtime fixes are landing, two blocking UI bugs remain unassigned (#8559, #8794), and a new audio‑rendering gap (#9089) could affect media‑focused users.

## 6. Feature Requests & Roadmap Signals

### User‑requested features (not yet implemented)

| Issue | Feature | Priority | Likelihood for next release |
|---|---|---|---|
| [#8046](zeroclaw-labs/zeroclaw/issues/8046) | Optional Telegram webhook mode | P2 | Medium – long polling is functional but webhook is a natural evolution. |
| [#7875](zeroclaw-labs/zeroclaw/issues/7875) | RunPod/ComfyUI image generation provider with provider‑scoped config | P3 | Lower – #6555 already added basic Comfy, but this refines config. |
| [#9047](zeroclaw-labs/zeroclaw/issues/9047) | Clarify ZeroCode code session vs persistent memory isolation | P2 | High – part of ongoing memory separation (#9048). |
| [#9093](zeroclaw-labs/zeroclaw/issues/9093) | Show ZeroCode version in TUI top bar | P3 | Likely – trivial change. |
| [#9086](zeroclaw-labs/zeroclaw/issues/9086) | Structured Security Audit Pipeline (Merkle chain, anomaly detection) | P2 | Medium – RFC just opened; long‑term security investment. |

### Predicted roadmap for v0.9.0

Based on closed RFCs targeting v0.9.0:
- **OIDC authentication** ([#7141](zeroclaw-labs/zeroclaw/issues/7141)) ✅ closed, PR #8672 merged.
- **Pluggable security enforcement** ([#7142](zeroclaw-labs/zeroclaw/issues/7142)) ✅ closed, partially landed.
- **Air‑gapped execution mode** ([#6293](zeroclaw-labs/zeroclaw/issues/6293)) ✅ closed, likely in progress.
- **A2A agent discovery** ([#7218](zeroclaw-labs/zeroclaw/issues/7218)) ✅ closed, groundwork laid.
- **Schema V4** ([#8754](zeroclaw-labs/zeroclaw/pull/8754)) merged – will break existing configs for those using retired channels.

## 7. User Feedback Summary

### Pain points expressed in recent issues

- **Workflow interruptions:** Exiting web dashboard stops agent mid‑task ([#8559](zeroclaw-labs/zeroclaw/issues/8559)) and stopping agent erases context ([#8794](zeroclaw-labs/zeroclaw/issues/8794)) are the most frustrating blockers, both with “S1 – workflow blocked” severity.
- **Provider incompatibility:** `kimi-code` streaming with tools fails ([#5600](zeroclaw-labs/zeroclaw/issues/5600)) – a specific provider but highlights broader reliability concerns.
- **Missing media support:** Audio markers not rendered ([#9089](zeroclaw-labs/zeroclaw/issues/9089)) limits use cases for voice‑enabled agents.
- **Performance degradation in ZeroCode:** Keystroke lag in long sessions ([#9092](zeroclaw-labs/zeroclaw/issues/9092)) affects developer experience.

### Satisfaction signals

- **Active community:** 38 issues and 50 PRs updated in one day, with 56 contributors in the latest release.
- **Rapid iterative improvements:** Provider streaming timeout fix (#8838), tool‑call argument normalization (#9060), and context overflow handling (#9083) address previously reported pain points.
- **Positive engagement on RFCs:** Users actively participate in design discussions (e.g., #9048, #9086) which indicates a healthy, invested user base.

## 8. Backlog Watch

Issues and PRs that are significant but appear to be stalled or awaiting maintainer action:

| Item | Opened | Last Update | Status | Risk | Notes |
|---|---|---|---|---|---|
| [#9048](zeroclaw-labs/zeroclaw/issues/9048) – Memory separation RFC | 2026-07-14 | 2026-07-15 | Open, needs author action | High | No maintainer comment yet; critical for memory architecture. |
| [#7875](zeroclaw-labs/zeroclaw/issues/7875) – RunPod/ComfyUI provider | 2026-06-17 | 2026-07-15 | Open, accepted | Medium | Waiting for provider‑scoped config pattern to stabilise. |
| [#8046](zeroclaw-labs/zeroclaw/issues/8046) – Telegram webhook mode | 2026-06-20 | 2026-07-15 | Open, accepted | High | No PR linked; maintainer interest unclear. |
| [#9079](zeroclaw-labs/zeroclaw/issues/9079) – CI for firmware protocol crate | 2026-07-15 | 2026-07-15 | Open | Medium | Needs maintainer to add CI job. |
| [#8486](zeroclaw-labs/zeroclaw/pull/8486) – OpenAI chat completions endpoint | 2026-06-29 | 2026-07-16 | Open, needs author action | High | Large PR (size:XL) – pending author response. |
| [#7821](zeroclaw-labs/zeroclaw/pull/7821) – SandboxPolicyConfig schema | 2026-06-17 | 2026-07-16 | Open, needs author action | High | Security‑critical, but awaiting backend wiring. |
| [#8536](zeroclaw-labs/zeroclaw/pull/8536) – preserve inner Elapsed error (hardware) | 2026-06-30 | 2026-07-16 | Open | Medium | Small fix, no recent maintainer review. |

All links follow `zeroclaw-labs/zeroclaw` on GitHub. 

**Disclaimer:** This digest is generated from a snapshot of issues

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*