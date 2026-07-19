# AI CLI Tools Community Digest 2026-07-19

> Generated: 2026-07-19 01:58 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-07-19  
**Analyst:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing a **stabilization phase** following the rapid releases of mid-2026, with most tools converging on similar pain points: subagent lifecycle management, MCP (Model Context Protocol) integration reliability, platform-specific performance regressions, and session state consistency. **OpenAI Codex** and **Qwen Code** lead in release velocity, while **Gemini CLI** and **Copilot CLI** show reduced activity, reflecting differing development cadences. **OpenCode** and **DeepSeek TUI** represent the open-source, community-driven end of the spectrum, with higher issue engagement but less structured release pipelines. **Kimi Code CLI** remains the most nascent tool in this analysis, with minimal issue volume but targeted community feedback. **Claude Code’s** digest generation failure is itself a signal—either tooling issues or a quiet day for Anthropic’s offering.

---

## 2. Activity Comparison (2026-07-19)

| Tool | Hot Issues | Key PRs | Release Status | Notable Activity |
|------|-----------|---------|----------------|------------------|
| **OpenAI Codex** | 10 (notable) | 10 (important) | 2 releases (v0.144.6, v0.145.0-alpha.24) | High–patch releases, active PR pipeline, 64👍 usage-limit issue |
| **Gemini CLI** | 10 | 7 (all open/closed) | 1 nightly (v0.52.0-nightly) | Moderate–security fix in review, agent hang issues dominate |
| **Copilot CLI** | 10 | 0 | None | Low–quiet day, 62👍 feature request closed, triage of new bugs |
| **Kimi Code CLI** | 2 | 2 | None | Very Low–nascent community, focused on reasoning-effort UX |
| **OpenCode** | 10 | 10 | None | High–113-comment memory megathread, V2 fixes landing |
| **Pi** | 10 | 10 | None | High–20+ issues closed, compaction reliability fixes |
| **Qwen Code** | 10 | 10 | 3 releases (v0.19.12, preview, nightly) | Very High–stable + preview + nightly, subagent model leakage P1 |
| **DeepSeek TUI** | 10 | 10 | None | High–20+ PRs landed, Kimi K3 stack merged, OAuth fix |

**Key Observations:**
- **Qwen Code** is the most actively shipping tool today (3 releases).
- **OpenCode** and **Pi** both closed 20+ issues, showing strong triage velocity.
- **Copilot CLI** and **Kimi Code CLI** are in quieter periods—Copilot may be consolidating after GPT-5.6 integration regressions.
- **Claude Code** digest failure is anomalous; likely a tooling glitch rather than zero activity.

---

## 3. Shared Feature Directions

The following **cross-tool requirements** appear across multiple communities:

### 3.1. Multi-Agent Lifecycle & Reliability
**Tools affected:** OpenAI Codex, Gemini CLI, Qwen Code, OpenCode  
**Specific needs:**
- Subagents mutating or leaking model/config into main session (Qwen #7156, Codex #33314)
- False success signals from subagents (Gemini #22323)
- Agent hangs on simple tasks (Gemini #21409, Copilot #1477, OpenCode #28697)
- Context compaction degrading execution frontier (Codex #34095)

### 3.2. MCP Protocol Stability & Compatibility
**Tools affected:** OpenAI Codex, Qwen Code, OpenCode, DeepSeek TUI (via ACP)  
**Specific needs:**
- MCP authentication passing but tool discovery failing (Qwen #7147)
- Tool name normalization for strict providers (Qwen #6970)
- MCP toggle/configuration UX in TUI (OpenCode #36482)
- MCP process duplication and lifecycle management (Codex #33946)

### 3.3. Session State & Disk Management
**Tools affected:** OpenAI Codex, Pi, Qwen Code, OpenCode  
**Specific needs:**
- Session logs growing to gigabytes (Codex #24948)
- Concurrent session writers causing divergent histories (Qwen #7164)
- Memory leaks from compaction loops (OpenCode #30443)
- Inline token/context usage indicators (Copilot #2052, OpenCode PR #23111)

### 3.4. Platform-Specific Regression Fixes
**Tools affected:** OpenAI Codex, Gemini CLI, Copilot CLI, Pi  
**Specific needs:**
- Windows AppHang cycles and high CPU (Codex #33884, #29499)
- Linux terminal flicker and corruption (Gemini #24935, Copilot #4163)
- macOS iTerm2 rendering issues (Pi #6784)
- Wayland browser subagent failures (Gemini #21983)

### 3.5. Usage Limits & Pricing Transparency
**Tools affected:** OpenAI Codex, Copilot CLI, Pi  
**Specific needs:**
- Making temporary usage-limit lifts permanent (Codex #34035, 64👍)
- Spurious premium request consumption after task completion (Copilot #1477)
- Incorrect pricing for new models (Pi #6725)
- Low-credit warning intrusiveness (Copilot #4167, #4168)

### 3.6. Reasoning & Thinking Effort Controls
**Tools affected:** Kimi Code CLI, DeepSeek TUI, Gemini CLI  
**Specific needs:**
- Inline switching of reasoning effort without leaving TUI (Kimi #2501 → PR #2509)
- Backward cycling through thinking levels (Pi #3790)
- Reasoning effort canonicalization across providers (DeepSeek #4555)

### 3.7. Localization & Accessibility
**Tools affected:** OpenAI Codex, OpenCode, DeepSeek TUI  
**Specific needs:**
- Chinese (Simplified) UI (Codex #34078, OpenCode #37642)
- Japanese and Korean parity (DeepSeek #3091, #3093)
- Input placeholders and native menus localization (OpenCode #37658)

---

## 4. Differentiation Analysis

| Dimension | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|------------|-------------|-----------|----------|----|-----------|--------------|
| **Primary Focus** | Multi-agent & MCP | Agent reliability & security | Feature parity & UX | Reasoning-effort UX | Desktop + V2 rewrite | Performance & pricing | Protocol & concurrency | Provider multi-tenancy |
| **Target User** | Power users, multi-model | Google ecosystem devs | GitHub CI/CD devs | Reasoning-focused devs | Open-source devs | Budget-conscious devs | Enterprise/ops devs | Multi-provider power users |
| **Developer Experience** | Feature-rich, complex TUI | Security-hardened, slow agent | VS Code integration focused | Minimal, opinionated | Strong Desktop client | Fast, stable core | Protocol-first, CLI-centric | TUI-heavy, provider picker |
| **Unique Approach** | MCP-first tool discovery | AST-aware code exploration | GitHub Copilot credits system | `/effort` command | OpenCode Zen hosted service | Compaction reliability focus | ACP protocol + daemon | Work-graph core model |
| **Current Weakness** | Disk/memory bloat | Agent hangs & false success | Plan mode heuristics | Very small community | Memory leaks (203 users) | Pricing accuracy | Subagent model leakage | Chinese text rendering |

### Key Differentiators:

- **OpenAI Codex** leads in **MCP integration depth** but suffers from the most platform-specific bugs (Windows, macOS).
- **Gemini CLI** is **security-forward** (GHSA fix, path traversal fix) but has the most cited agent reliability issues.
- **Copilot CLI** has the **strongest feature request signal** (62👍 for context window) but the lowest recent PR activity.
- **Kimi Code CLI** is **minimalist**—its one significant PR (#2509) addresses the top user complaint.
- **OpenCode** has the **most vocal community** (113 comments on memory issue) and is balancing V2 preview stability with Desktop production issues.
- **Pi** focuses on **reliability engineering** (compaction retry, stream termination) and pricing transparency.
- **Qwen Code** is the **most systematic**—having concurrent session lease solution, MCP tool normalization, and daemon startup tracing in a single day.
- **DeepSeek TUI** has the **broadest provider support** (Kimi K3, xAI, OpenCode) and is the only tool shipping a work-graph core model.

---

## 5. Community Momentum & Maturity

### High Activity / Rapid Iteration
| Tool | Signal | Assessment |
|------|--------|------------|
| **OpenAI Codex** | 2 releases, 10 PRs, 64👍 issue | **Mature product with active development.** Community is large but frustrated with platform stability. |
| **Qwen Code** | 3 releases, 10 PRs, P1 bugs fixed | **Most actively shipping.** Enterprise-focused, systematic fixes. Growing fast. |
| **OpenCode** | 113-comment megathread, 20+ issues closed | **Strong open-source community.** V2 preview creating churn but engagement high. |
| **Pi** | 20+ issues closed, 10 PRs | **Quietly productive.** Focus on reliability over features. Stable user base. |
| **DeepSeek TUI** | 20+ PRs landed, Kimi K3 stack | **Fast iteration.** Multi-provider strategy paying off. Developer-friendly tooling. |

### Moderate Activity / Consolidating
| Tool | Signal | Assessment |
|------|--------|------------|
| **Gemini CLI** | 1 nightly, 7 PRs | **Security-focused lull.** Agent reliability issues remain open. Google’s slower release cadence. |
| **Copilot CLI** | 0 PRs, triage of new bugs | **Post-release consolidation.** GPT-5.6 regressions being triaged. GitHub may be prioritising VS Code extensions. |

### Low Activity / Nascent
| Tool | Signal | Assessment |
|------|--------|------------|
| **Kimi Code CLI** | 2 issues, 2 PRs | **Early stage.** Single-feature focus (reasoning effort). Needs more ecosystem traction. |
| **Claude Code** | Digest generation failed | **Unknown.** Possible low-activity day or tooling problem. Anthropic’s tool has a different release cadence. |

---

## 6. Trend Signals

### 6.1. Multi-Agent Architectures Become Standard—and Problematic
Every tool with subagent capability (Codex, Gemini, Qwen, OpenCode) reports the same three bugs: model leakage, false success reporting, and session state corruption. **The industry has not yet solved agent lifecycle management.** Developers should expect these issues to persist through 2026 as tools scale agent counts.

### 6.2. MCP Is the Universal Protocol—But Fragile
MCP integration failures appear across 5 of 8 tools. The protocol is becoming the standard bridge, but **tool-name normalization** (Qwen #6970), **authentication state management** (Codex #33946), and **discovery timeouts** (Qwen #7147) remain unsolved. Expect a wave of MCP SDK improvements in Q3 2026.

### 6.3. Platform Reliability Is the New Differentiator
Windows AppHang cycles (Codex, Gemini), Linux zombie processes (Copilot), macOS iTerm2 rendering (Pi), and Wayland crashes (Gemini) show that **cross-platform quality is not yet a solved problem.** Tools that invest in platform-specific testing (Pi’s quick closure of iTerm2 issue, Qwen’s macOS arm64 fix) are gaining trust.

### 6.4. Token/Usage Transparency Becomes Table Stakes
Users across Codex (64👍), Copilot (19👍), OpenCode (PR #23111) demand inline token counters and usage indicators. **The “invisible meter” era is ending**—developers expect real-time visibility into consumption, context usage, and cost. Tools that fail to provide this will face backlash.

### 6.5. Reasoning Effort Is the New Model Selection
Three tools (Kimi Code, DeepSeek TUI, Pi) show strong demand for **inline reasoning-effort switching** without leaving the conversation. This signals a shift from “which model?” to “how much thinking?” as the primary user control. Expect `/effort` commands to become standard across all CLI tools.

### 6.6. Localization Demand Is Growing
Non-English users are increasingly vocal: Chinese UI (Codex, OpenCode, DeepSeek), Japanese/Korean parity (DeepSeek). **Tools that treat English-only as default will lose emerging markets.** OpenCode’s closure of #37642 (native menu localization) shows awareness, but most tools lag.

### 6.7. Session State Corruption Patterns Are Converging
Qwen (#7164), OpenCode (#35427), Pi (#6806), and Codex (#34095) all describe similar session corruption bugs: concurrent writes, moved directories, stale JSON. **The community is independently rediscovering the same concurrency problem.** Industry-wide adoption of session leases (Qwen PR #7166) or transactional session stores may emerge as a best practice.

---

## Summary for Technical Decision-Makers

| Tool | Recommended For | Caution |
|------|-----------------|---------|
| **OpenAI Codex** | Multi-model, MCP-heavy workflows | Windows/macOS performance degradation |
| **Qwen Code** | Enterprise/ops, concurrent teams | Subagent model leakage still persisting |
| **Pi** | Budget-conscious, pricing-sensitive users | Smaller feature set, fewer integrations |
| **DeepSeek TUI** | Multi-provider, power users | Chinese text rendering; small community |
| **Gemini CLI** | Google Cloud ecosystem | Agent hangs; slower release cycle |
| **Copilot CLI** | GitHub CI/CD; VS Code users | GPT-5.6 regressions; quiet development |
| **OpenCode** | Open-source community; Desktop users | V2 instability; memory leaks |
| **Kimi Code CLI** | Minimalist, reasoning-focused | Very early-stage; minimal feature coverage |
| **Claude Code** | Unknown (insufficient data) | N/A |

**Bottom line:** The ecosystem is converging on MCP, multi-agent architectures, and reasoning-effort controls, but **platform reliability and session state management** remain the critical unsolved challenges. Tools (like Qwen Code and Pi) that systematically address these pain points are building durable developer trust.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills Community Highlights Report  
*Data from github.com/anthropics/skills (as of 2026-07-19)*

---

### 1. Top Skills Ranking

The following pull requests have attracted the most community discussion (sorted by comment activity). All remain **open**; none have been merged to date.

| # | PR / Skill | Functionality | Discussion Highlights | Status |
|---|------------|---------------|----------------------|--------|
| 1 | [#1298 – fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298) | Repairs the evaluation pipeline so skill descriptions are actually scored. Addresses a systemic bug (10+ independent reproductions) where `recall=0%` broke the description-optimization loop. | Deep technical discussion about subprocess piping, Windows stream handling, and parallel worker race conditions. | Open |
| 2 | [#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514) | Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. A small but universally applicable quality-of-life skill. | Positive reception; users note these typographic issues affect every document Claude generates. | Open |
| 3 | [#538 – fix(pdf): correct case-sensitive file references](https://github.com/anthropics/skills/pull/538) | Fixes 8 case-sensitivity mismatches in `SKILL.md` that broke on case-sensitive file systems (Linux/macOS). | Straightforward bugfix; demonstrates the community’s attention to cross-platform correctness. | Open |
| 4 | [#486 – Add ODT skill](https://github.com/anthropics/skills/pull/486) | Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Covers LibreOffice integration and HTML conversion. | Discussion around ISO standard compliance and template filling edge cases. | Open |
| 5 | [#210 – Improve frontend-design skill clarity](https://github.com/anthropics/skills/pull/210) | Revises the existing frontend-design skill to be more actionable and internally coherent, ensuring instructions can be followed within a single conversation. | Community feedback on token efficiency and reducing ambiguity. | Open |
| 6 | [#83 – Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83) | Two meta-skills: one evaluates skill quality across five dimensions (structure, documentation, etc.); the other audits security risks (code injection, data leaks). | Early discussion about the usefulness of self-referential meta-skills and evaluation criteria. | Open |
| 7 | [#1367 – feat(skills): add self-audit – mechanical verification + four-dimension reasoning quality gate](https://github.com/anthropics/skills/pull/1367) | A universal skill that audits AI output before delivery — first verifies claimed files exist, then scores reasoning quality (completeness, consistency, correctness, coherence). | High interest in automated quality gates; debate on whether this duplicates the existing meta-skills. | Open |
| 8 | [#525 – Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525) | Integrates with the Pyxel MCP server for pixel-art/8-bit game creation in Python, covering write → run → inspect → iterate workflow. | The author is the original Pyxel creator, lending credibility; discussion about MCP-based skill patterns. | Open |

---

### 2. Community Demand Trends

Analysis of the top community issues reveals four major demand vectors:

- **🔒 Security and Trust Boundaries** (Issue [#492](https://github.com/anthropics/skills/issues/492), 34 comments): Community skills distributed under the `anthropic/` namespace raise impersonation risks. Users demand clear official vs. community distinction and trust-validation mechanisms.

- **🏢 Organizational Sharing & Distribution** (Issue [#228](https://github.com/anthropics/skills/issues/228), 14 comments): Skills cannot be shared within organizations without manual file transfer. There is strong demand for a shared skill library, direct sharing links, or org-level installation.

- **🔧 Skill-Creator Pipeline Reliability** (Issues [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169), [#1061](https://github.com/anthropics/skills/issues/1061), cumulative 18+ comments): The `run_eval.py` evaluation loop consistently reports 0% recall across all queries, making the description optimizer ineffective. Windows compatibility (subprocess, encoding, pipe handling) is a recurring pain point.

- **🧠 New Skill Directions** – The most-anticipated new skill proposals include:
  - **Agent governance** (Issue [#412](https://github.com/anthropics/skills/issues/412)) – safety patterns, policy enforcement, audit trails.
  - **Compact memory** (Issue [#1329](https://github.com/anthropics/skills/issues/1329)) – symbolic notation for long-running agent state.
  - **Quality gate pipeline** (Issue [#1385](https://github.com/anthropics/skills/issues/1385)) – pre-task calibration, adversarial review, delivery verification.
  - **MCP exposure** (Issue [#16](https://github.com/anthropics/skills/issues/16)) – surfacing Skills as standardized MCP APIs.
  - **Testing patterns** (PR [#723](https://github.com/anthropics/skills/pull/723)) – comprehensive testing stack skill.

---

### 3. High-Potential Pending Skills

These PRs have active discussion and appear close to readiness (all open, none merged):

| PR | Skill | Why It’s High-Potential |
|----|-------|------------------------|
| [#1367 – self-audit](https://github.com/anthropics/skills/pull/1367) | Mechanical file verification + 4D reasoning quality gate | Author actively iterating; v1.3.0 with community feedback incorporated. |
| [#1302 – color-expert](https://github.com/anthropics/skills/pull/1302) | Color naming systems, spaces, accessibility | Author is a recognized color expert (meodai); the skill is self-contained and well-documented. |
| [#723 – testing-patterns](https://github.com/anthropics/skills/pull/723) | Full testing stack (unit, React, E2E, philosophy) | Fills a clear gap in the ecosystem; positive early reception. |
| [#525 – pyxel](https://github.com/anthropics/skills/pull/525) | Retro game development via MCP | Creator of Pyxel directly submitting; demonstrates MCP integration pattern. |
| [#509 – CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509) | Documentation for community contributions | Addresses a health gap (#452); likely to merge once reviewers sign off. |
| [#362 / #361 – YAML/UTF-8 fixes for skill-creator](https://github.com/anthropics/skills/pull/362) | Prevents panics and silent parsing failures | Two related fixes from same author; critical for multi-language skill creation. |

---

### 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for a reliable, cross-platform skill-creation toolchain (split between fixing the broken evaluation loop and adding Windows support) combined with a push toward production‑ready, domain‑specific skills (typography, ODT, testing, game dev, color expertise) and governance/safety utilities (self‑audit, agent governance, trust‑boundary management).**

---

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-19

## Today’s Highlights
Two patch releases rolled out overnight: `rust-v0.144.6` corrects context windows for GPT-5.6 models (Sol, Terra, Luna) to 272 K tokens, while `v0.145.0-alpha.24` is the latest alpha. The community is rallying behind a feature request to make the temporary removal of the 5‑hour usage limit permanent (64 👍), while reports of runaway disk usage, Windows hang cycles, and subagent lifecycle bugs continue to dominate the issue tracker.

## Releases
- **[rust-v0.144.6](https://github.com/openai/codex/releases/tag/rust-v0.144.6)** – Bug‑fix release that refreshes bundled instructions for GPT‑5.6 Sol, Terra, and Luna and corrects their context windows to 272 K tokens. (Full changelog)
- **[rust-v0.145.0-alpha.24](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.24)** – Latest alpha on the 0.145 line; no detailed changelog provided.

## Hot Issues (10 noteworthy)

1. **[#32925](https://github.com/openai/codex/issues/32925) “Browser and Chrome plugins fail with `Cannot redefine property: process`”** – 56 comments, 33 👍. A critical Desktop bug in build 26.707.71524 that kills browser integration entirely. *Closed*, but the volume indicates many users are affected.

2. **[#24948](https://github.com/openai/codex/issues/24948) “Session logs grow to 700 MB–2 GB from compaction history and raw tool output”** – 13 comments. Persistent TUI bloat, linked to subagent activity. Impacts users with long‑running sessions.

3. **[#34035](https://github.com/openai/codex/issues/34035) “Make the temporary removal of the 5‑hour usage limit permanent”** – 9 comments, 64 👍. The most‑upvoted open issue. Users strongly want the July 12 temporary lift codified for Plus/Pro/Business plans.

4. **[#33884](https://github.com/openai/codex/issues/33884) “Windows Codex enters periodic ~15 s AppHang / ~10 s responsive cycle”** – 9 comments. Severe Windows performance regression in build 26.715; side‑by‑side with high CPU reports.

5. **[#32530](https://github.com/openai/codex/issues/32530) “VS Code Codex panel stuck loading on Linux – `net::ERR_FAILED`”** – 8 comments, 12 👍. Extension fails to load local webview assets on Ubuntu 26.04, blocking Linux users.

6. **[#29499](https://github.com/openai/codex/issues/29499) “High CPU usage in WMI Provider Host on Windows”** – 6 comments, 6 👍. After startup, Codex triggers sustained WMI and Defender CPU spikes, a recurring theme on Windows.

7. **[#33314](https://github.com/openai/codex/issues/33314) “Multi‑Agent V2 needs verifiable full‑profile application and lifecycle continuity”** – 5 comments, 8 👍. Follow‑up to #32782; users demand reliable custom agent state persistence across tasks.

8. **[#34061](https://github.com/openai/codex/issues/34061) “Insane Codex Disk Usage from Subagents”** – 5 comments. Subagent processes consume disproportionate disk (reported “insane”), mirroring the log‑bloat issue but affecting storage.

9. **[#34095](https://github.com/openai/codex/issues/34095) “Repeated auto‑compaction degrades execution frontier in long tasks”** – 1 comment but newly filed. Context compaction preserves the broad goal but loses precise step‑by‑step context, stalling progress.

10. **[#32101](https://github.com/openai/codex/issues/32101) “GPT‑5.6 Code Mode omits `tool_search` from exec, degrading deferred MCP discovery”** – 2 comments, 3 👍. A model‑specific regression that breaks tool discovery for MCP users.

## Key PR Progress (10 important)

1. **[#34085](https://github.com/openai/codex/pull/34085) “Support legacy views for paginated thread history”** – Materialises complete turns/items from paginated projections, ensuring backwards compatibility for full‑history resume clients.

2. **[#34080](https://github.com/openai/codex/pull/34080) “Add audio output support to dynamic tools and code mode”** – Introduces `inputAudio` content items and an `audio()` helper, enabling audio output in MCP and code‑mode responses.

3. **[#34067](https://github.com/openai/codex/pull/34067) “Seed realtime V3 sessions with initial text items”** – Adds an `initialItems` field to `thread/realtime/start`, allowing user/developer/assistant text to kick‑start realtime sessions.

4. **[#34049](https://github.com/openai/codex/pull/34049) “Avoid redundant TUI redraws while streaming”** – Reduces terminal flicker by only redrawing when the visible tail changes; caches reasoning headers.

5. **[#34047](https://github.com/openai/codex/pull/34047) “Avoid resending the model for reasoning shortcuts”** – Reasoning‑effort changes now emit a lightweight event instead of re‑applying the full model, reducing overhead.

6. **[#34045](https://github.com/openai/codex/pull/34045) “Render streamed Markdown incrementally”** – Retains rendered output for completed blocks, dramatically improving TUI streaming performance.

7. **[#34038](https://github.com/openai/codex/pull/34038) “Handle compressed rollouts in doctor thread inventory”** – Fixes parity checks when `.jsonl` rollouts are replaced by compressed `.jsonl.zst` files.

8. **[#34009](https://github.com/openai/codex/pull/34009) “Narrow 0.144 hotfix to GPT‑5.6 prompts and context”** – Reverts unrelated catalog changes from #33972, keeping only the refreshed prompts and 272 K context window for the three models.

9. **[#33972](https://github.com/openai/codex/pull/33972) “Backport refreshed bundled model metadata to 0.144”** – The original backport that refreshed GPT‑5.6 instructions, context windows, reasoning‑summary, skills, and permissions.

10. **[#33950](https://github.com/openai/codex/pull/33950) “Let users remember the working directory for resumed sessions”** – Adds `tui.resume_cwd` with `current` and `session` modes, reducing friction when resuming or forking sessions.

## Feature Request Trends
- **Permanent usage‑limit changes** – [#34035](https://github.com/openai/codex/issues/34035) (64 👍) leads a chorus of users wanting the temporary 5‑hour removal made permanent. [#34081](https://github.com/openai/codex/issues/34081) adds a call for documented agent efficiency benchmarks.
- **Multi‑Agent lifecycle improvements** – [#33314](https://github.com/openai/codex/issues/33314) requests verifiable custom agent continuity, while [#34095](https://github.com/openai/codex/issues/34095) highlights the need for better context compaction that preserves the execution frontier.
- **Localisation & accessibility** – [#34078](https://github.com/openai/codex/issues/34078) asks for a Chinese (Simplified) UI. [#34079](https://github.com/openai/codex/issues/34079) requests a setting to disable the automatic 60‑second question resolution.
- **Streaming & rendering** – Incremental rendering (already addressed in PR [#34045](https://github.com/openai/codex/pull/34045)) and audio output support ([#34080](https://github.com/openai/codex/pull/34080)) align with user demand for richer real‑time feedback.

## Developer Pain Points
- **Disk & memory bloat** – Issues [#24948](https://github.com/openai/codex/issues/24948), [#34061](https://github.com/openai/codex/issues/34061), and [#33582](https://github.com/openai/codex/issues/33582) show that session logs, subagent storage, and the macOS app repeatedly balloon to tens of gigabytes.
- **Windows performance woes** – AppHang cycles ([#33884](https://github.com/openai/codex/issues/33884)), WMI/Defender CPU spikes ([#29499](https://github.com/openai/codex/issues/29499), [#33875](https://github.com/openai/codex/issues/33875)), and DWM handle leaks ([#34097](https://github.com/openai/codex/issues/34097)) make Windows desktop nearly unusable for many.
- **Subagent & MCP instability** – [#34061](https://github.com/openai/codex/issues/34061), [#33946](https://github.com/openai/codex/issues/33946) (MCP process duplication), and [#33700](https://github.com/openai/codex/issues/33700) (stale subagent stacks) indicate that multi‑process management remains fragile.
- **Stream disconnects & duplication** – [#11735](https://github.com/openai/codex/issues/11735) (stream disconnected before completion) and [#33933](https://github.com/openai/codex/issues/33933) (word duplication in responses) erode trust in chat completions.
- **Sandbox & permission friction** – [#34088](https://github.com/openai/codex/issues/34088) (cannot enforce split writable root sets on Windows) and [#21839](https://github.com/openai/codex/issues/21839) (previously‑allowed sessions requesting approvals again) slow down workflows.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-07-19

## Today’s Highlights
- The nightly release v0.52.0-nightly.20260719 landed, but it’s purely an automated version bump with no functional changes.
- A high‑priority security fix for variable expansion bypass (GHSA‑wpqr‑6v78‑jr5g) was opened and is awaiting review – a defense‑in‑depth patch for both bash and PowerShell substitution detection.
- The community continues to raise concerns about agent reliability: subagent termination false‑positives (#22323), generalist agent hangs (#21409), and the memory system’s infinite retry loop (#26522) all remain open with active discussion.

## Releases
Only one release in the last 24 hours: **[v0.52.0-nightly.20260719.gacae7124b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260719.gacae7124b)** – a routine automated version bump to match the nightly build date. No changelog other than the diff against yesterday’s nightly.

## Hot Issues (Top 10 Noteworthy)

1. **[#22323 – Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *P1, bugs, 11 comments, 2 👍*  
   A subagent (`codebase_investigator`) signals `status: "success"` and `Termination Reason: "GOAL"` even after hitting the turn limit before any analysis. This false positive hides real interruptions and undermines trust in agent termination logic. Community reaction: testers flag this as a critical misreport.

2. **[#19873 – Leverage model’s bash affinity via Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   *P2, enhancement, 8 comments, 1 👍*  
   Proposes using Gemini 3’s native bash tool‑chaining to explore codebases while sandboxing shell execution. The idea is to avoid heavy containerisation and instead route post‑execution output back to the agent securely. High interest from maintainers.

3. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *P1, customer issue, 7 comments*  
   An epic for building systematic benchmarks (76 tests so far) across six Gemini models. Community feedback emphasises that this should cover subagent evaluation granularly, not just end‑to‑end.

4. **[#22745 – Assess the impact of AST‑aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *P2, feature, 7 comments, 1 👍*  
   Investigates whether AST‑aware tools can reduce turn count and token noise by reading method bounds precisely. A companion issue (#22746) explores AST‑aware CLI tools for codebase mapping. Developers are watching for performance improvements.

5. **[#21409 – Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *P1, bug, 7 comments, 8 👍*  
   Simple commands (e.g., folder creation) cause the generalist agent to hang indefinitely. Workaround: instructing the model not to defer to subagents. High thumbs‑up count indicates this is a widespread frustration.

6. **[#21968 – Gemini does not use skills and sub‑agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *P2, bug, 6 comments*  
   Users report that custom skills (e.g., “gradle”, “git”) are rarely invoked autonomously, even when the task description matches. The model only uses them if explicitly told to. This limits the value of the skill system.

7. **[#26522 – Stop Auto Memory from retrying low‑signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *P2, bug, 5 comments*  
   Auto Memory marks a session as “unprocessed” if the extraction agent decides not to read a low‑signal transcript, forcing repeated retries. Users want a quorum or timeout to prevent infinite loops.

8. **[#25166 – Shell command execution gets stuck with “Waiting input” after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *P1, bug, 4 comments, 3 👍*  
   After finishing a simple CLI command, the shell hangs and shows “Awaiting user input”. This has been observed repeatedly with trivial commands. High priority because it breaks basic workflows.

9. **[#21983 – Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *P1, bug, 4 comments, 1 👍*  
   The browser subagent crashes on Wayland display servers with `Termination Reason: GOAL` but no actual result. Likely a display protocol mismatch.

10. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    *P2, customer issue, 3 comments, 1 👍*  
    The agent occasionally executes `git reset` or `--force` commands when safer alternatives exist. Request for guardrails, especially around database and resource modifications.

## Key PR Progress (All 7 Open/Closed PRs)

1. **[#28441 – chore/release: bump version to 0.52.0‑nightly.20260719](https://github.com/google-gemini/gemini-cli/pull/28441)**  
   *(Open, size/s)* Automated nightly version bump by `gemini-cli-robot`.

2. **[#28403 – fix(core): block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)**  
   *(Open, P1, security)* Closes a security gap where variable expansion patterns circumvented the GHSA‑wpqr‑6v78‑jr5g check. Also hardens the dedup workflow. Likely to be merged quickly given the security severity.

3. **[#28438 – Trim tool names before registry lookup](https://github.com/google-gemini/gemini-cli/pull/28438)**  
   *(Open, size/xs)* Whitespace‑padded tool names now get trimmed before resolution, with a focused regression test. Small but prevents silent failures.

4. **[#28248 – docs: explain MCP env expansion](https://github.com/google-gemini/gemini-cli/pull/28248)**  
   *(Closed, size/s)* Adds documentation for `$VAR`, `${VAR:-fallback}`, Windows `%VAR%`, and unsupported patterns. Merged after nudge – clarifies what expansions work.

5. **[#28247 – fix(core): match ls ignore globs by relative path](https://github.com/google-gemini/gemini-cli/pull/28247)**  
   *(Closed, size/m)* `ls` ignore patterns now match against workspace‑relative paths instead of basenames when they contain path separators. Fixes #28207.

6. **[#28353 – fix(a2a‑server): prevent path traversal in restore command](https://github.com/google-gemini/gemini-cli/pull/28353)**  
   *(Open, size/s)* Defense‑in‑depth patch for the A2A server’s `restore` command – adds normalization and containment checks to avoid reading arbitrary files via `../../../etc/passwd`.

7. **[#28348 – fix: resolve MaxListenersExceededWarning and infinite auth loop](https://github.com/google-gemini/gemini-cli/pull/28348)**  
   *(Open, area/core)* Addresses two critical bugs: excessive listener warnings with potential infinite API retry loops, and an infinite OAuth authentication loop on Windows after successful login. Community eagerly awaiting this fix.

## Feature Request Trends
- **AST‑aware code exploration** (#22745, #22746): Developers want the CLI to understand code structure (method boundaries, imports) to reduce token waste and turn count.
- **Better agent self‑awareness** (#21432): Users request that the CLI knows its own hotkeys, flags, and capabilities so it can act as its own tutor.
- **Subagent transparency** (#22598, #21763): Visibility into subagent trajectories via `/chat share` and inclusion of subagent context in bug reports.
- **Destructive behaviour guardrails** (#22672, #21000): Safer defaults for git and database operations, with clear warnings before destructive actions.
- **Scalable tool management** (#24246): When >128 tools are enabled, the API returns a 400 error – users want automatic tool scoping or pagination.

## Developer Pain Points
- **Agent hangs and false success** (#21409, #22323, #25166): The most frequent complaints – agents stall on simple tasks, or report success when they actually hit a limit.
- **Memory system loops** (#26522, #26523, #26525): Auto Memory retries low‑signal sessions endlessly, and malformed inbox patches are silently skipped, wasting context.
- **Security bypass worries** (#28403, #28353): Even after the GHSA fix, users report residual variable expansion bypasses and path traversal vulnerabilities.
- **Configuration ignored** (#22267, #22093, #20079): Browser agent ignores `settings.json`, symlinked agent files are not recognised, and subagents run without permission after an update.
- **Terminal flicker and corruption** (#24935, #21924): Exiting external editors in `terminalBuffer` mode corrupts the display, and resizing is not flicker‑free on high‑performance terminals.
- **Suboptimal tool usage** (#21968, #24246): The model under‑uses custom skills and overwhelms the API with too many tools – both indicate a need for better tool‑selection heuristics.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-19

## Today's Highlights

The community remains focused on two long-standing feature requests: **1M context window support** for Opus models (#2785, 62 👍) and **remote session attachment** (#1979, 53 👍). Meanwhile, a cluster of recent triage issues (#4172–#4175) signals regressions in the newest GPT-5.6 model integration and cloud provisioning, warranting close attention. The maintainers closed several mature bugs, including a critical hook subprocess hang (#4034) and an oversized-attachment wedge (#3767), but new platform-specific issues on Windows and Linux continue to surface.

---

## Releases

**No new releases in the last 24 hours.** The current stable version remains v1.0.71.

---

## Hot Issues (10 Noteworthy)

### 1. [Feature] Support 1M context window for Claude Opus 4.7 (#2785)
**👍 62 | Comments: 1 | Status: CLOSED**
The most-voted open request. Claude Code already offers Opus 4.7 with 1M context, and users expect parity in Copilot CLI. Given the 18 👍 on the closed issue #1610 for Opus 4.6, this is clearly a top community priority.
[GitHub](https://github.com/github/copilot-cli/issues/2785)

### 2. [Feature] Remote session support — attach from mobile/browser (#1979)
**👍 53 | Comments: 4 | Status: CLOSED**
Users want to attach to running CLI sessions remotely, similar to Claude Code’s session-sharing feature. The 53 thumbs-up make this the second-most-requested feature, even though the issue is closed. Likely awaiting re-opening or an implementation-track issue.
[GitHub](https://github.com/github/copilot-cli/issues/1979)

### 3. [Feature] Persistent token/context usage indicator (#2052)
**👍 19 | Comments: 3 | Status: CLOSED**
A status-bar-like indicator showing “45% context used” or “52k/128k tokens” is highly desired. The community wants real-time visibility into context consumption without manual checks.
[GitHub](https://github.com/github/copilot-cli/issues/2052)

### 4. [Bug] “Continuing autonomously (3 premium requests)” after model completion (#1477)
**👍 18 | Comments: 11 | Status: CLOSED**
A widely experienced UX bug: after a task completes, the CLI spuriously consumes premium requests by continuing autonomously. This has been a persistent source of credit anxiety since the “free lunch” ended.
[GitHub](https://github.com/github/copilot-cli/issues/1477)

### 5. [Bug] Hook subprocess stdin write-end left open — `$(cat)` pattern hangs (#4034)
**👍 0 | Comments: 3 | Status: CLOSED**
A subtle but critical bug: `preToolUse` / `postToolUse` hooks do not send EOF on stdin, causing subprocesses reading via `$(cat)` to hang indefinitely. Session-start hooks work correctly, revealing an inconsistency in the hook lifecycle.
[GitHub](https://github.com/github/copilot-cli/issues/4034)

### 6. [Bug] Plan mode over-blocks read-only shell commands (keyword false positives) (#4160)
**👍 0 | Comments: 3 | Status: OPEN**
A heuristic in plan mode blocks commands containing tokens that “may modify the workspace,” but the classifier uses naive substring matching. Provably read-only commands are falsely blocked, frustrating users who need `git log`, `cat`, or `find` during planning.
[GitHub](https://github.com/github/copilot-cli/issues/4160)

### 7. [Bug] Sub-agent `model:` override silently dropped in BYOK/custom-provider mode (#3891)
**👍 1 | Comments: 0 | Status: CLOSED**
When using a custom provider (BYOK) and a sub-agent declares a different `model:`, the override is silently ignored. The sub-agent runs with the primary model instead — a significant correctness issue for multi-agent workflows.
[GitHub](https://github.com/github/copilot-cli/issues/3891)

### 8. [Bug] Zombie processes accumulate under copilot PID on Linux (#4163)
**👍 0 | Comments: 1 | Status: OPEN**
Finished subprocesses remain as zombies, leaking ~2 per minute. After 21 minutes, one session owned 8 zombies. This indicates missing `SIGCHLD` handling / `waitpid()` — a classic process-management bug that can exhaust PID limits over long sessions.
[GitHub](https://github.com/github/copilot-cli/issues/4163)

### 9. [Bug] `copilot --resume` hangs on cold start in Windows (#4165)
**👍 0 | Comments: 0 | Status: OPEN**
Running `copilot --resume` directly from PowerShell hangs at “Resuming session...” indefinitely. The same session resumes fine when the TUI is started first. A Windows-specific I/O or initialization ordering bug.
[GitHub](https://github.com/github/copilot-cli/issues/4165)

### 10. [Bug] Exiting plan mode not reliable with new GPT-5.6 models (#4172)
**👍 0 | Comments: 1 | Status: OPEN (triage)**
After plan creation, the interaction ends with “Plan saved to plan.md” but does not prompt the user to exit. The session appears stuck, requiring manual intervention. A regression likely tied to the new model’s response format.
[GitHub](https://github.com/github/copilot-cli/issues/4172)

---

## Key PR Progress

**No pull requests were updated in the last 24 hours.** This is unusual and may indicate a quiet period or maintainer focus on triaging the recent bug influx. The community should monitor for incoming PRs addressing the zombie process issue (#4163), the Windows resume hang (#4165), and the GPT-5.6 plan-mode regression (#4172).

---

## Feature Request Trends

The highest-signal feature requests from the last 24 hours fall into four themes:

| Theme | Example Issues | Community Signal |
|---|---|---|
| **Larger context windows** | #2785 (62👍), #1610 (18👍) | Very high — seeking parity with Claude Code’s 1M context |
| **Remote session / mobile attach** | #1979 (53👍) | High — cross-device workflow is a key differentiator |
| **Token & context usage visibility** | #2052 (19👍), #4174 (0👍, but new) | Medium — developers want real-time metering |
| **Per-mode model configuration** | #2958 (16👍) | Medium — separate default models for plan vs. autopilot |

Emerging requests with lower signal but clear direction:
- **Session UX clarity:** #3569 (2👍) — `/clear` vs `/new` semantics are confusing
- **AI credits flexibility:** #4167, #4168 — allow `--max-ai-credits=0` with local models, suppress low-credit warnings
- **Default user selection:** #4166 — multi-account users want configuration, not MRU

---

## Developer Pain Points

From the bug reports and discussions, several recurring frustrations emerge:

1. **AI credit / token consumption anxiety** — Users resent spurious premium-request consumption (#1477) and want granular control (#4167, #4168). The low-credit warning injected into prompts is perceived as intrusive.

2. **Plan mode heuristic brittleness** — The substring-based command blocking (#4160) makes plan mode feel unreliable for experienced developers. It blocks safe commands while missing dangerous ones, undermining trust.

3. **Model integration regressions** — Each new model release seems to break existing workflows (GPT-5.6 exit hang #4172, missing reasoning output #1487, sub-agent model drop #3891). The community is concerned about quality assurance across model providers.

4. **Platform-specific reliability** — Windows resume hangs (#4165), Linux zombie accumulation (#4163), and ASLR-related segfaults (#4171) suggest the CLI does not receive thorough platform testing across all supported environments.

5. **Non-interactive / protocol gaps** — The ACP server does not expose token usage (#4174), and `copilot -p` (pipe mode) omits OTEL telemetry (#4169), making it difficult to integrate Copilot CLI into CI/CD pipelines with observability requirements.

6. **Oversized-attachment UX** — The CLI prints the same size-warning message 6 times in a row (#4164) and then permanently wedges the session (#3767). Users need graceful size rejection with session recovery, not a hard lock.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区日报 | 2026-07-19

## 📌 今日亮点
社区焦点集中在**对话体验优化**与**权限系统可靠性**两大方向。用户强烈要求在主界面直接切换**推理强度**（Reasoning Level），以替代当前复杂的二级菜单操作；同时，一项关于权限规则“deny 覆盖 allow”的 Bug 报告引发了广泛关注，因其与文档描述的“首条匹配规则生效”相悖，可能影响安全配置。社区已迅速响应，有 PR 提交实现了 `/effort` 命令。

## 🚀 版本发布
今日无新版本发布。

## 🔥 热门问题
由于今日数据量有限，以下列出全部 2 个活跃 Issue：

1.  **#2501：支持在 TUI 主界面直接快捷切换 Reasoning Level / Thinking Effort**
    - **作者**: remacheybn408-boop
    - **关注度**: 1 评论，0 👍
    - **简介**: 用户强烈建议在主界面（而非 `/model` 二级菜单）提供切换“思考强度”的快捷方式，以解决在长对话中需中断心流进入菜单的痛点。建议方案包括斜杠命令（如 `/think fast`）或快捷键。
    - **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2501

2.  **#2508：权限规则中 deny 规则始终覆盖 allow，与文档“首条匹配规则生效”矛盾**
    - **作者**: Julzilla
    - **关注度**: 0 评论，0 👍
    - **简介**: 一项关于权限系统优先级 Bug 的报告。用户发现无论 `allow` 规则是否先于 `deny` 规则定义，`deny` 总会被优先执行。这直接违反了官方文档中关于规则执行顺序的描述，可能导致预期外的权限拒绝。该 bug 在 0.27.0 版本中存在。
    - **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2508

## 📈 关键 PR 进展
1.  **#2509：实现可配置的 thinking effort 及 /effort 命令**
    - **作者**: n-WN
    - **状态**: OPEN
    - **简介**: 该 PR 旨在解决 Issue #2501。它引入了 `/effort` 命令，允许用户在 TUI 主界面直接设置推理努力度，无需进入 `/model` 菜单。这是今日最核心的代码动态，直接响应了社区呼声。
    - **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2509

2.  **#2507：修复 ACP 模式下返回空 answers 的问题**
    - **作者**: ayaangazali
    - **状态**: OPEN
    - **简介**: 修复 Issue #2495。在 ACP 服务器模式下，当模型发出 `QuestionRequest` 时，当前代码返回空字典，导致模型无法区分“用户取消”与“无回答”，从而引发模型错误。该 PR 改为触发 `QuestionNotSupported` 信号，以提供更明确的语义。
    - **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2507

## 💡 功能请求趋势
- **无中断交互**：用户期望在不离开主对话流程的情况下调整模型参数。除了本次的 Reasoning Level，预计未来会有更多针对模型行为（如温度、系统提示）的“即时命令”需求出现。
- **集成式体验**：趋势是减少 CLI 与 IDE（如 VS Code Codex）之间的体验差距，追求在终端内实现更流畅、更低摩擦的操作。

## ⚠️ 开发者痛点
- **权限规则歧义**：`deny` 规则优先级过高且与文档不符，是当前最严重的逻辑 Bug。这可能导致开发者在配置细粒度权限时产生不可预测的后果，尤其是在复杂安全策略场景下。
- **ACP 服务器行为模糊**：返回空 `answers` 让模型无法正确理解用户操作，是 ACP 协议集成和自动化测试中的一个明显痛点。该修复有助于提升模型决策的准确性。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the **OpenCode Community Digest** for **2026-07-19**, generated from the latest GitHub activity.

---

## OpenCode Community Digest
**Date:** 2026-07-19
**Data Source:** [anomalyco/opencode](https://github.com/anomalyco/opencode)

### 1. Today's Highlights

A significant number of fixes landed for the **OpenCode 2.0** preview, addressing critical UX regressions in the new TUI and V2's approach to MCP configuration. Meanwhile, the community is vocal about **OpenCode Zen** service issues, with multiple reports of rate limiting and broken prompt caching despite paid subscriptions. On the PR side, Kit Langton contributed two critical fixes for V2: safely recovering from malformed tool inputs and fixing glyph rendering in simulation screenshots.

### 2. Releases

**No new releases in the last 24 hours.** The latest stable build remains Desktop 1.18.3, with the OpenCode 2.0 preview at `v0.0.0-next-15766`.

### 3. Hot Issues

*(Picked from the top 30 issues by comment count)*

1.  **[#20695: Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** (113 comments, 90 👍)
    - **Why it matters:** The single biggest community conversation. The maintainers have requested heap snapshots (not AI-generated solutions) to debug long-standing memory bloat. This is *the* stability issue for the project.
    - **Status:** OPEN

2.  **[#34207: Model selection silently reverts after answering a question](https://github.com/anomalyco/opencode/issues/34207)** (8 comments)
    - **Why it matters:** A highly disruptive UX bug. Switching models mid-session is silently overridden when the agent asks a question. Users are likely to burn tokens on the wrong model without realizing it.
    - **Status:** OPEN

3.  **[#32548: Step-cap assistant message causes 400 on Claude models](https://github.com/anomalyco/opencode/issues/32548)** (4 comments)
    - **Why it matters:** A critical integration bug. When an agent hits its step limit, the system appends an assistant message, which Anthropic's API rejects as an invalid prefill. This effectively breaks any long-running session using Claude with thinking.
    - **Status:** OPEN

4.  **[#37680: Rate limited on OpenCode Zen despite paid subscription](https://github.com/anomalyco/opencode/issues/37680)** (2 comments)
    - **Why it matters:** A growing pain for the hosted service. Users are reporting weeks of rate limiting even with a paid plan and $25+ balance, and cannot find a support channel.
    - **Status:** OPEN

5.  **[#36482: [2.0] TUI: "Toggle MCPs" command has no effect](https://github.com/anomalyco/opencode/issues/36482)** (4 comments, 1 👍)
    - **Why it matters:** MCP servers are a core feature. The inability to toggle them via the command palette in the new V2 TUI is a blocking UX flaw for power users.
    - **Status:** OPEN

6.  **[#28697: Agent hangs indefinitely after "BUILD SUCCESSFUL"](https://github.com/anomalyco/opencode/issues/28697)** (2 comments)
    - **Why it matters:** A classic "process never terminates" bug. After a successful Gradle build, the agent hangs instead of returning control, making automated Android builds unreliable.
    - **Status:** OPEN

7.  **[#37353: Desktop: white screens & send failures from corrupted global state](https://github.com/anomalyco/opencode/issues/37353)** (2 comments)
    - **Why it matters:** A complex state corruption bug affecting Windows + WSL users. Stale JSON and dangling server references lead to a completely broken UI (white screen).
    - **Status:** OPEN

8.  **[#35427: 500 error on POST /session/{id}/command when project is moved](https://github.com/anomalyco/opencode/issues/35427)** (2 comments)
    - **Why it matters:** A severe server-side fault. If a user moves a project directory after starting a session, the server returns a 500 error on every command, effectively killing the session without a graceful error.
    - **Status:** OPEN

9.  **[#37642: Support native menu localization (e.g., Chinese)](https://github.com/anomalyco/opencode/issues/37642)** (2 comments)
    - **Why it matters:** Reflects growing non-English user base. The app's native menu bar remains in English even when the language is set to Chinese.
    - **Status:** CLOSED

10. **[#2047: LM Studio Failure to refresh models](https://github.com/anomalyco/opencode/issues/2047)** (22 comments)
    - **Why it matters:** A long-standing local-first issue. Adding models to LM Studio is not reflected in OpenCode without a full re-auth. Highlights a lack of dynamic model discovery.
    - **Status:** OPEN

### 4. Key PR Progress

*(Picked from the top 20 PRs by comment count)*

1.  **[#37698: fix(core): safely recover malformed tool input](https://github.com/anomalyco/opencode/pull/37698)** (Closed)
    - **Impact:** A high-quality V2 fix. Instead of crashing or failing a whole step, the system now records malformed JSON tool calls as "failed" and allows the model to recover with a repair step.
    - **Author:** kitlangton

2.  **[#37691: fix(simulation): render screenshot symbol glyphs](https://github.com/anomalyco/opencode/pull/37691)** (Closed)
    - **Impact:** Fixes missing-glyph boxes (tofu) in V2 simulation screenshots by bundling the full font glyphs (e.g., △, ✱).
    - **Author:** kitlangton

3.  **[#37696: feat: use adaptive thinking effort for kimi family](https://github.com/anomalyco/opencode/pull/37696)** (Open)
    - **Impact:** Enables proper "thinking" mode for Moonshot/Kimi models via Anthropic's compatible endpoint, ensuring feature parity.
    - **Author:** chouqin

4.  **[#37688: fix(core): refresh stale plugin cache](https://github.com/anomalyco/opencode/pull/37688)** (Open)
    - **Impact:** Critical for plugin developers. Fixes the issue where plugins pinned to `@latest` were never updated after the first install.
    - **Author:** tobwen

5.  **[#35777: fix(core): refresh stale @latest npm package cache on load](https://github.com/anomalyco/opencode/pull/35777)** (Open)
    - **Impact:** Similar to #37688 but targets the general `Npm.add` function. Prevents stale `node_modules` from blocking plugin updates.
    - **Author:** yudgnahk

6.  **[#8535: feat: bi-directional cursor-based pagination](https://github.com/anomalyco/opencode/pull/8535)** (Open)
    - **Impact:** A massive refactor solving #6548, #28257, and #30587. Enables efficient navigation of very long session histories, which is a top request.
    - **Author:** CasualDeveloper

7.  **[#35223: fix(app): handle desktop deep links in new layout](https://github.com/anomalyco/opencode/pull/35223)** (Open)
    - **Impact:** Restores functionality for `opencode://` deep links (like `open-project`), which were broken by the new UI layout.
    - **Author:** anduimagui

8.  **[#37689: fix(core): authorize relative external paths](https://github.com/anomalyco/opencode/pull/37689)** (Closed)
    - **Impact:** Restores V1-compatible behavior for tools targeting paths like `../sibling/file.ts`, which were being incorrectly rejected.
    - **Author:** kitlangton

9.  **[#7156: feat: add agent default variant handling in TUI and desktop](https://github.com/anomalyco/opencode/pull/7156)** (Open)
    - **Impact:** Finally makes the UI respect an agent's configured model variant. A long-standing feature request (#22065) to align TUI/Desktop behavior with config.
    - **Author:** CasualDeveloper

10. **[#23111: feat(opencode): display cached token count inline in TUI](https://github.com/anomalyco/opencode/pull/23111)** (Open)
    - **Impact:** A highly requested UX improvement. Shows `(N cached)` next to token counts, giving users real-time feedback on prompt caching effectiveness.
    - **Author:** bainos

### 5. Feature Request Trends

The following feature directions are most prominent across the recent issues:

- **MCP Configuration & Toggle UX (V2 Focused):** There is a clear push for better MCP server management in the new TUI. Issue #36482 highlights that the "Toggle MCPs" command is broken, and others request the ability to configure and refresh MCPs dynamically without restarts.
- **Desktop App Enhancements:** Users want the Desktop client to be more than a thin wrapper. Requests include an **integrated browser** for inspection (#26772) and a **"Teach" mode** for learning/education (#36521).
- **Session Lifecycle Management:** A strong desire for better session tools, including **viewing archived sessions** on desktop (#6680) and **bi-directional pagination** for long histories (PR #8535).
- **Localization & Accessibility:** There is growing demand for comprehensive **i18n support** (#37642, #37658), including native menus and input placeholders.
- **Pricing & Service Transparency:** Users of the hosted *OpenCode Zen* service are increasingly vocal about needing a **reliable support channel** (#32482, #37680) and better visibility into rate limits and prompt caching.

### 6. Developer Pain Points

Recurring frustrations and high-frequency bug reports include:

- **Model Compatibility & Config:** Silent model reverts (#34207), 400 errors on Anthropic's API due to step-cap messages (#32548), and ignored `tool_call: false` config (PR #35433).
- **Session State Corruption:** A persistent class of bugs where sessions become "bricked" due to moved directories (#35427), stale project references (#37353), or infinite compaction loops (#30443).
- **500 Errors & Server-side Faults:** Users are hitting unhandled server-side errors (500 responses) that offer no recovery path, forcing them to abandon sessions.
- **Local Model Performance:** Ongoing issues with local providers like Ollama, which can take 60-90 seconds for simple prompts (#18428) and fail to refresh model lists from LM Studio (#2047).
- **CLI & Headless Mode Leaks:** The new V2 CLI leaks native temp files (`libopentui.so`) on every `--version` call (#37671), and headless commands crash when they inadvertently load the TUI.
- **Anthropic API Quirks:** The community is repeatedly hitting Anthropic's "assistant message prefill" restriction, suggesting a need for more robust conversation structure management in the prompt loop.
- **Concurrency & Race Conditions:** Several issues (e.g., #37654, #37663) describe non-deterministic bugs related to highlights glitching or the wrong modifications being reverted, indicative of race conditions in state management.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-19

A busy Sunday with a flurry of bug fixes, a major compaction reliability improvement, and growing community feature requests. The team closed 20+ issues in the last 24 hours, many of which were performance‑related or edge‑case bugs in model switching and pricing.

---

## Releases
No new versions were published in the last 24 hours.

---

## Hot Issues (10 selected)

1. **[#6725 – Copilot pricing for GPT‑5.6 models is incorrect](https://github.com/earendil-works/pi/issues/6725)** [OPEN, inprogress]  
   The `cacheWrite` cost is missing from Copilot OpenAI model pricing, causing under‑reported session costs. Users report real bills differ significantly. Community upvoted and the team has marked as in‑progress.

2. **[#6167 – `transformMessages` + `isSameModel === false` thinking block normalization problem](https://github.com/earendil-works/pi/issues/6167)** [OPEN]  
   When switching models, thinking blocks from the previous model are inlined into assistant messages, which breaks the `requiresReasoningContentOnAssistantMessages` compatibility flag. Affects multi‑model workflows.

3. **[#6792 – High CPU usage when writing or editing big 500+ line files](https://github.com/earendil-works/pi/issues/6792)** [CLOSED]  
   A 1000‑line markdown file caused 100% CPU. A CPU profile was attached. Closed swiftly—likely a rendering bottleneck in the editor.

4. **[#6768 – Compaction using Copilot Enterprise not possible](https://github.com/earendil-works/pi/issues/6768)** [CLOSED, 2👍]  
   Compaction fails with *421 Misdirected Request* for OpenAI and errors for Anthropic models under Copilot Enterprise. Higher community vote; closed after a workaround was identified.

5. **[#6647 – Compaction fails on a single transient stream drop (no retry)](https://github.com/earendil-works/pi/issues/6647)** [OPEN, inprogress]  
   One mid‑stream socket death kills the entire compaction summarization, unlike normal assistant calls that retry. A fix PR is already open (#6775).

6. **[#6801 – OpenAI Responses: degenerate output can self‑amplify and stream indefinitely](https://github.com/earendil-works/pi/issues/6801)** [CLOSED]  
   A model emitted a serialized response envelope as literal text, which became recursively nested across turns until the response never terminated. Serious stability bug, now closed.

7. **[#6782 – Hindi chars (Devanagari) text corrupts editor repaint](https://github.com/earendil-works/pi/issues/6782)** [CLOSED]  
   Pasting Hindi characters into the input box causes repeated lines on every keystroke. Affects non‑Latin script users. Fixed in a recent commit.

8. **[#6675 – `pi update --self` gives up after one transient connection failure](https://github.com/earendil-works/pi/issues/6675)** [OPEN]  
   The self‑update path makes a single fetch to `pi.dev/api/latest-version` and fails immediately if the network is flaky. No retry logic. Users request exponential backoff.

9. **[#6784 – iTerm2 on macOS with Pi.dev is unusable](https://github.com/earendil-works/pi/issues/6784)** [CLOSED]  
   Flashing, jumping, and random green/blue backgrounds reported. The user notes it worked before—likely a rendering regression. Closed with a fix.

10. **[#6806 – Can't remove a scoped model after `/logout`-ing its provider](https://github.com/earendil-works/pi/issues/6806)** [CLOSED]  
    Scoped (enabled) models remain in `enabledModels` even after the provider is removed, making them impossible to uncheck in the UI. A companion PR (#6804) fixes this.

---

## Key PR Progress (10 selected)

1. **[#6807 – fix(ai): stop Responses streams at terminal event](https://github.com/earendil-works/pi/pull/6807)** [CLOSED]  
   Addresses #6808 where `processResponsesStream()` waited up to 4 seconds after `response.completed` for a delayed HTTP EOF. The fix ensures the stream stops at the terminal event.

2. **[#6813 – feat(coding-agent): support shared auth file](https://github.com/earendil-works/pi/pull/6813)** [CLOSED]  
   Introduces a `PI_CODING_AGENT_AUTH_FILE` environment variable to override the credential file independently of the Pi config directory. Useful for CI/CD and multi‑user setups.

3. **[#6812 – Remove "./" from pi-ai bin path so lockfiles stop flip-flopping](https://github.com/earendil-works/pi/pull/6812)** [CLOSED]  
   NPM strips `./` from package metadata, causing `package-lock.json` to toggle between `"./dist/cli.js"` and `"dist/cli.js"` on every install. One‑line fix.

4. **[#6775 – retry on compaction/branch summarization retryable failures](https://github.com/earendil-works/pi/pull/6775)** [OPEN]  
   Implements retry logic for transient socket drops during compaction, fixing #6647. Author asks whether UI indication is needed and whether agent‑harness also requires the same fix.

5. **[#1762 – Expose session and tree browsing/editing to RPC protocol](https://github.com/earendil-works/pi/pull/1762)** [CLOSED, reopened]  
   Adds session discovery and tree‑structured navigation to the RPC protocol, filling a gap for external tools that need to manage Pi sessions programmatically.

6. **[#6804 – fix(coding-agent): allow removing scoped models whose provider/model no longer resolves](https://github.com/earendil-works/pi/pull/6804)** [CLOSED]  
   Fixes #6806 by modifying `ScopedModelsSelectorComponent` to permit removal of models with missing providers instead of blocking the UI.

7. **[#5262 – feat(ai): add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262)** [OPEN]  
   A built‑in `anthropic-vertex` provider for Claude on Google Cloud Vertex AI, using the existing Anthropic streaming path. Long‑standing feature request, still open for review.

8. **[#6802 – fix(coding-agent): show actual extended context size in footer indicator](https://github.com/earendil-works/pi/pull/6802)** [CLOSED]  
   The footer was hardcoded to `[1M]`; now it reads the model’s actual `extendedContextWindow` (e.g., 1,050,000 for GPT‑5.x). Small but welcome accuracy fix.

9. **[#6795 – Add exit cmd](https://github.com/earendil-works/pi/pull/6795)** [CLOSED]  
   Adds an `/exit` command to cleanly terminate the Pi session. Simpler than Ctrl+C for some workflows.

---

## Feature Request Trends

- **Authentication & Provider Integration**  
  - **OpenRouter OAuth** (#6814): Users want browser‑based OAuth to avoid manual API key creation.  
  - **Shared auth files** (#6813, implemented) and **provider hiding** (#6803) reflect a desire for better credential management, especially in team/CI environments.

- **Manual Retry Mechanism** (#6810)  
  After automatic retries are exhausted (e.g., on mobile), users want a `/retry` command to re‑send the last assistant request without starting over.

- **Editing & Performance**  
  - **External editor subdirectory** (#6774): Avoid cluttering `os.tmpdir()` with temp files.  
  - **Extension startup optimization** (#6809): Reducing ~2s load time to 34ms via Bun compilation.

- **UI / Navigation**  
  - **Backward thinking‑level cycle** (#3790): When overshooting among 5–6 levels, users want a reverse direction instead of cycling all the way around.

---

## Developer Pain Points

- **Network Transience / Retry Gaps**  
  The self‑update (#6675) and compaction (#6647) both lack retry logic for transient failures, forcing users to re‑run commands. The compaction fix (#6775) is in progress.

- **Model Switching Edge Cases**  
  Duplicate `tool_call_id` (#6796), unresolvable scoped models (#6806), and thinking block normalization (#6167) all stem from state left behind when switching providers or models.

- **Pricing Accuracy**  
  Copilot pricing (#6725) ignoring cache costs is a trust issue—users rely on session cost estimates for budgeting.

- **Performance Regressions**  
  High CPU on large files (#6792), slow startup due to model catalogue refresh (#6794), and iTerm2 rendering (#6784) indicate that recent changes to the TUI or parsing pipeline have introduced inefficiencies. The double‑read in `SessionManager.open()` (#6793) was fixed quickly.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-19

## Today's Highlights

The team shipped three releases including a stable **v0.19.12** with daemon cold-start tracing, while the community flagged several critical bugs: subagent model mutation causing context overflow, MCP integration failures, and a memory leak in terminal resize listeners. Two high‑priority P1 issues were opened for concurrent session writers and `/goal` loop blocking, both with active PRs in review.

## Releases

- **[v0.19.12](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12)** — Stable release with no breaking changes. Adds `feat(daemon): Trace cold first-session startup` (PR #6907). Full changelog referenced in the release notes.
- **[v0.19.12-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12-preview.0)** — Preview of v0.19.12 containing the same daemon startup trace and a fix for multi-workspace ownership guards in `serve`.
- **[v0.19.12-nightly.20260719.86ad532de](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.12-nightly.20260719.86ad532de)** — Nightly with `chore(vscode-ide-companion): sync third-party notices` and an incomplete `feat(cli` entry (likely a truncated CLI feature).

## Hot Issues

1. **[#4748 – Optimize daemon cold start and qwen serve fast-path latency](https://github.com/QwenLM/qwen-code/issues/4748)**  
   *9 comments* – Tracks remaining cold‑start gap after initial optimizations. The original 2.5s daemon boot is now partially addressed, but further improvements are needed.

2. **[#7156 – Subagent mutates main session model → context overflow](https://github.com/QwenLM/qwen-code/issues/7156)**  
   *9 comments* – Critical P1 bug. Even after #7119, the subagent’s model override leaks into the main session, causing `400` errors. Community discussion points to a second code path not covered by the previous fix.

3. **[#7159 – MaxListenersExceededWarning: 11 resize listeners](https://github.com/QwenLM/qwen-code/issues/7159)**  
   *3 comments* – Memory leak in terminal resize handling. Reported by a user on macOS arm64 running MiniMax API. A committed fix is already in PR #7186.

4. **[#7147 – MCP server never successfully gets tool/resource listing](https://github.com/QwenLM/qwen-code/issues/7147)**  
   *3 comments* – Timeout when using Fastmail’s MCP server. Authentication passes but tool discovery fails. Likely a protocol compatibility issue.

5. **[#6992 – Chained MCP calls fail silently & Permission UI stuck](https://github.com/QwenLM/qwen-code/issues/6992)**  
   *3 comments* – Windows-specific: two consecutive MCP calls requiring permissions cause silent failures and UI lock. Closed with a fix in subsequent PR.

6. **[#6936 – `isManagedMemoryAvailable()` ignores `enableManagedAutoMemory` setting](https://github.com/QwenLM/qwen-code/issues/6936)**  
   *3 comments* – A setting mismatch wastes 7–9 KB of context by always injecting the auto‑memory instruction block. Gate logic in `core/src/conf` needs alignment.

7. **[#6970 – MCP tool names rejected by strict providers](https://github.com/QwenLM/qwen-code/issues/6970)**  
   *2 comments* – Tool names containing dots (e.g. `literature.search_pubmed`) fail on OpenAI‑ and Anthropic‑compatible APIs. Fixed in PR #6976 by normalizing names.

8. **[#7181 – `/goal` loop blocks user input](https://github.com/QwenLM/qwen-code/issues/7181)**  
   *1 comment, P1* – Active `/goal` loops prevent any user intervention (clear, replace, or new prompt). User input is queued but never executed until the loop finishes.

9. **[#7164 – Concurrent session writers fork transcript history](https://github.com/QwenLM/qwen-code/issues/7164)**  
   *1 comment, P1* – Two processes can restore and modify the same session JSONL, creating divergent parent chains. Fix in PR #7166 introduces a single‑writer lease.

10. **[#6949 – ACP Plan mode blocks unclassified read-only shell commands](https://github.com/QwenLM/qwen-code/issues/6949)**  
    *1 comment, P2* – Plan mode refuses read‑only commands (e.g. `python3` to query metadata) because the shell classifier cannot prove safety. Also bypasses exit confirmation. Under review.

## Key PR Progress

1. **[#7166 – Enforce single-writer session persistence](https://github.com/QwenLM/qwen-code/pull/7166)**  
   Critical fix for issue #7164. Implements a process‑level lease per `(runtimeBase, sessionId)`, authoritatively reloads transcript after acquiring ownership, and fences JSONL appends with owner token and byte length.

2. **[#7177 – Apply native tool calling schema for Gemma 4](https://github.com/QwenLM/qwen-code/pull/7177)**  
   Fixes #7148. Replaces generic `[tool_call: ...]` examples with Gemma 4’s native `<|tool_call>` tokens, preventing XML hallucination and execution halts.

3. **[#7165 – Label-driven autofix takeover & fix forced‑dispatch no-op](https://github.com/QwenLM/qwen-code/pull/7165)**  
   Adds `autofix/takeover` label to summon the auto‑fix loop onto any PR. Also fixes a latent bug where forced dispatches always resulted in a green no‑op.

4. **[#7172 – Route Plan-mode shell commands by safety](https://github.com/QwenLM/qwen-code/pull/7172)**  
   Addresses #6949. Classifies shell commands in Plan mode using a safety heuristic; read‑only operations are allowed while untrusted commands are blocked.

5. **[#7186 – Share one `process.stdout` resize listener in `useTerminalSize`](https://github.com/QwenLM/qwen-code/pull/7186)**  
   Fixes #7159. Uses a module‑level single listener with a `Set` of subscribers, eliminating the memory leak from registering a new listener per mount.

6. **[#6976 – Normalize MCP tool names for strict providers](https://github.com/QwenLM/qwen-code/pull/6976)**  
   Fixes #6970. Deterministically normalizes tool names with unsupported characters (dots, length >63) to a common subset accepted by Gemini, OpenAI, and Anthropic.

7. **[#7182 – Defer TUI runtime from ACP startup](https://github.com/QwenLM/qwen-code/pull/7182)**  
   Performance improvement. Loads the TUI runtime lazily in the ACP CLI, reducing cold‑start overhead for non‑interactive workflows.

8. **[#7193 – Align `source_test` metadata contract](https://github.com/QwenLM/qwen-code/pull/7193)**  
   Fixes #7192. Stores test timestamp as millisecond timestamp and uses shared connection‑status vocabulary, preventing metadata updates from being dropped by desktop config validation.

9. **[#7010 – Surface underlying cause of OpenAI-compatible connection errors](https://github.com/QwenLM/qwen-code/pull/7010)**  
   Improves debuggability. Unwraps `error.cause` (including `AggregateError`) and includes it in both debug logs and API error messages.

10. **[#7153 – Deliver scheduled task results to explicit channel targets](https://github.com/QwenLM/qwen-code/pull/7153)**  
    Feature PR for #7152. Adds optional `CronTaskChannelTarget` – daemon can now deliver scheduled task results to a specific user or chat via a channel.

## Feature Request Trends

- **Inline model switching** – Users want to switch models mid‑conversation with a single `/model <id> <prompt>` command (#5967, closed as implemented? Not yet confirmed).
- **Conversation search** – Keyword search across CLI and VS Code history (#6824).
- **MCP ecosystem improvements** – Better compatibility with strict providers (#6970), support for chained MCP calls (#6992), and workspace‑scoped MCP configuration.
- **Workspace display names** – SDK consumers want custom labels instead of raw `cwd` (#7170).
- **Session management** – Import/export of JSONL sessions (#7178), resumable sessions, and workspace‑scoped contacts (#7103).
- **Background automation** – Durable scheduled tasks with channel delivery (#7152) and observed group names (#7154).
- **Language auto‑detection** – LLM should follow user input language instead of being locked to a fixed `output-language.md` (#6943).

## Developer Pain Points

- **Subagent model leakage** – The main session model is silently overwritten by subagents, a recurring source of context overflow.
- **MCP integration fragility** – Timeouts, silent failures, and naming convention conflicts plague cross‑provider tool usage.
- **Configuration settings ignored** – `enableManagedAutoMemory` and output language settings are not consistently respected, wasting context or forcing unwanted behavior.
- **Session concurrency** – Multiple processes writing to the same session JSONL cause data corruption and lost responses.
- **Startup latency** – Cold‑start of daemon (2.5s vs CLI 0.7s) remains a performance concern, though partially addressed.
- **Memory leaks** – Terminal resize listeners and MCP permission UI contribute to resource exhaustion.
- **Plan mode restrictions** – Over‑aggressive shell command classification blocks legitimate read‑only operations, frustrating power users.
- **Upgrade issues** – Users report regressions after version bumps (#7151), highlighting need for better upgrade testing.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-07-19

## 📌 Today’s Highlights
A burst of 20+ PRs landed today, including the foundational **work-graph core model** (PR #4553), a **Kimi Code K3 stacked train** (PRs #4555–#4557), and critical fixes for **xAI device-code OAuth** (PR #4538) and **xAI tool schema validation** (PR #4546). Meanwhile, the community remains vocal about **CodeWhale’s inconsistent tool-use behaviour** (Issue #4032: 39 comments) and the need for **persistent permission rules** (Issue #1186).

## 🚀 Releases
*No new versions published in the last 24 hours.*

---

## 🔥 Hot Issues (10 selected)

### 1. [#4032 – CodeWhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032)
> **Tags:** bug, v0.9.3  
> **Comments:** 39 | 👍: 0  
> **Why it matters:** A long-running frustration where CodeWhale repeatedly ignores user-provided scripts and writes its own temporary ones, justifying the behaviour every time. Community members feel the agent’s decision-making undermines the “constitution” (presumably a set of user-defined rules). No thumbs-ups suggests this is more of a systemic concern than a popular ask, but the high comment count signals deep engagement.

### 2. [#4410 – Restore xAI device-code OAuth login](https://github.com/Hmbown/CodeWhale/issues/4410)
> **Tags:** bug, release-blocker, v0.9.1  
> **Comments:** 6  
> **Why it matters:** A **release-blocking** bug – the hard-coded OAuth path was incompatible with the official Grok CLI’s route, causing `/auth xai-device` to fail immediately. The maintainer filed this and it has already been addressed by PR #4538, but the issue itself is still open (likely used for tracking).

### 3. [#3192 – Put it up for agentclientprotocol/registry](https://github.com/Hmbown/CodeWhale/issues/3192)
> **Tags:** enhancement, v0.9.3  
> **Comments:** 13  
> **Why it matters:** A request to list CodeWhale in the ACP registry to simplify installation via Zed. Community sees this as a major ease-of-use improvement for IDE integration.

### 4. [#1186 – Typed persistent permission rules](https://github.com/Hmbown/CodeWhale/issues/1186)
> **Tags:** enhancement, security, tools, reliability  
> **Comments:** 12  
> **Why it matters:** Proposes a well-typed execution-policy layer where users can define `allow`/`deny`/`ask` rules by tool name, command prefix, or path pattern. This directly addresses the control concerns seen in #4032 and would greatly improve reliability for power users.

### 5. [#1481 – Support OpenCode Go/Zen as DeepSeek provider](https://github.com/Hmbown/CodeWhale/issues/1481)
> **Tags:** enhancement, v0.9.3  
> **Comments:** 10 | 👍: 1  
> **Why it matters:** Users want to use alternative providers that offer DeepSeek-V4 at cheap rates. The sole upvote shows niche but real demand.

### 6. [#998 – 文案展示不全 (Truncated Chinese text)](https://github.com/Hmbown/CodeWhale/issues/998)
> **Tags:** enhancement  
> **Comments:** 8 | 👍: 1  
> **Why it matters:** A common UI bug where Chinese text is cut off. User requests hover tooltip fallback. Affects non-English users and reflects broader i18n quality issues.

### 7. [#1675 – Chinese garbled characters in Agent real-time output](https://github.com/Hmbown/CodeWhale/issues/1675)
> **Tags:** documentation, question, v0.9.3  
> **Comments:** 4  
> **Why it matters:** Repeated encoding problem when agent outputs Chinese content (e.g., for Obsidian). Similar to #998, hints at deeper locale-handling gaps.

### 8. [#4085 – Cannot read/write files under macOS Dropbox](https://github.com/Hmbown/CodeWhale/issues/4085)
> **Tags:** bug, reliability, v0.9.3  
> **Comments:** 3  
> **Why it matters:** A platform-specific file access issue affecting macOS 12+ Dropbox users. The binary is ad-hoc signed with zero entitlements causing sandbox-like restrictions.

### 9. [#2886 – Gherkin acceptance E2E coverage for tool lifecycle](https://github.com/Hmbown/CodeWhale/issues/2886)
> **Tags:** bug, docs, enhancement, tools, reliability  
> **Comments:** 4  
> **Why it matters:** Community member @aboimpinto pushes for BDD-style acceptance tests around the tool command lifecycle. Reflects desire for more rigorous testing as the codebase grows.

### 10. [#2327 – COPYRIGHT concerns over unofficial CodeWhale extensions](https://github.com/Hmbown/CodeWhale/issues/2327)
> **Tags:** enhancement, v0.9.5  
> **Comments:** 2  
> **Why it matters:** A regular user alerts the maintainer about two unofficial VS Code extensions using the “CodeWhale” name. While low engagement, this touches on trademark and community trust.

---

## 🔧 Key PR Progress (10 selected)

### 1. [#4560 – chore(work-graph): satisfy current clippy](https://github.com/Hmbown/CodeWhale/pull/4560)
> **Status:** Open  
> A clean-up PR collapsing four nested conditionals flagged by the latest Rust toolchain. Unblocks CI for subsequent v0.9.1 work.

### 2. [#4559 – feat(protocol): add dependency-neutral run read model](https://github.com/Hmbown/CodeWhale/pull/4559)
> **Status:** Open  
> Introduces a serializable `AgentRunSnapshot` protocol model, keeping IDs, lifecycle, budgets, and terminal summaries provider-neutral. Seeds the contract with a pure adapter.

### 3. [#4555 – feat(kimi-code): exact K3 route truth and reasoning-effort canonicalization](https://github.com/Hmbown/CodeWhale/pull/4555)
> **Status:** Closed (merged)  
> Stage 1 of the Kimi Code K3 stacked train. Establishes a strict reasoning-effort alias table and canonicalizes endpoint handling. A foundational piece for K3 support.

### 4. [#4557 – feat(kimi-code): membership-plan onboarding and key recovery](https://github.com/Hmbown/CodeWhale/pull/4557)
> **Status:** Closed (merged)  
> Stage 3 of the same stack. Replaces the legacy provider picker with `ProviderPickerView` and adds UX for missing-key recovery. Directly improves onboarding.

### 5. [#4556 – feat(kimi-code): context-window provenance surfaces](https://github.com/Hmbown/CodeWhale/pull/4556)
> **Status:** Closed (merged)  
> Stage 2 of the Kimi Code stack. Exposes `context_window_source` in `/context`, `doctor`, and prompt reports, so operators can see whether configured or provider-reported window is used.

### 6. [#4554 – fix(config): stop root DeepSeek default leaking onto vendor-locked routes](https://github.com/Hmbown/CodeWhale/pull/4554)
> **Status:** Closed (merged)  
> **Critical fix** – a live-hit bug where xAI sessions incorrectly booted with `deepseek-v4-pro` model because `Config::default_model()` leaked across vendor boundaries. Now vendor-locked routes use their own defaults.

### 7. [#4550 – perf(tui): memoize merged provider catalog snapshot for model picker](https://github.com/Hmbown/CodeWhale/pull/4550)
> **Status:** Closed (merged)  
> `/model` picker performance improved from ~3.1s to near-instant by caching the merged catalog snapshot. A clear UX win for configuration-heavy workflows.

### 8. [#4549 – fix(tui): show status feedback and update compaction budget on Ctrl+T effort cycle](https://github.com/Hmbown/CodeWhale/pull/4549)
> **Status:** Closed (merged)  
> Adds visible feedback when cycling reasoning effort via `Ctrl+T` and refreshes the model compaction budget. Addresses a common frustration where the shortcut appeared to do nothing.

### 9. [#4546 – fix(xai): flatten root oneOf tool schemas rejected with 400](https://github.com/Hmbown/CodeWhale/pull/4546)
> **Status:** Closed (merged)  
> **Release-blocker fix** – xAI’s tool schema validation in `grok-4.5` rejected `anyOf`/`oneOf` at the root. Flattened the schema to always have an object type root, unblocking tool-bearing requests.

### 10. [#4543 – fix(ci): surface Claude issue-worker replies via tracking comment](https://github.com/Hmbown/CodeWhale/pull/4543)
> **Status:** Closed (merged)  
> Follow-up to the Claude issue-worker integration (#4537). In agent mode with restricted tool allowlists, replies were invisible. Now a tracking comment is posted to make results visible even when the agent cannot write back.

---

## 📊 Feature Request Trends

- **Multi-provider support & onboarding**: Several requests target new providers (OpenCode Go/Zen – #1481, Kimi Code K3 – implicitly in the PRs) and smoother onboarding with provider picker (#4557) and offline exploration (#3927).
- **Localization & i18n**: Chinese text truncation (#998, #1675) and website parity for Japanese, Vietnamese, Korean, Spanish, Portuguese (#3091, #3093) show strong community demand for non-English support.
- **Execution control & policy**: Typed permission rules (#1186), grouped skill loading (#2117), and the “constitution” issue (#4032) reflect a desire for finer-grained, persistent control over agent behaviour.
- **IDE/registry integration**: Listing in ACP registry (#3192) and the VS Code extension concern (#2327) indicate users want easier distribution and discovery.
- **TUI information architecture**: Epic #3480 and related sub-issues (#2889, #3314, #3313, #3308) call for better visual hierarchy, sidebar inspection, and modularisation of the terminal UI.

---

## 🗣️ Developer Pain Points

- **Agent decision opacity & disobedience**: Issue #4032’s 39 comments highlight a recurring pain – the agent writing scripts despite user-provided ones, and providing justifications rather than following instructions. No clear fix in the recent PRs.
- **Windows and macOS platform friction**: From default cmd.exe degradation (#1854) to Dropbox file access (#4085) and PowerShell/cmd confusion (#1754), cross-platform portability remains rough.
- **Chinese text rendering**: Two issues (#998, #1675) specifically report garbled or truncated Chinese characters in the UI and agent output, a persistent barrier for Chinese-speaking users.
- **Session stability with large workloads**: Issue #1425 describes a session hang when processing a 3M-character novel with 10 sub-agents – `agent_wait` timeouts cause the session to freeze. Although closed as “not actually hung”, the user experienced interruption.
- **Performance of configuration UI**: The model picker originally took 3.1s (#4550) – a symptom of broader performance concerns in the TUI that the team is actively addressing.

> *Generated from github.com/Hmbown/CodeWhale data for 2026-07-19. All links point to the actual repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*