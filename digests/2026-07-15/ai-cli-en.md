# AI CLI Tools Community Digest 2026-07-15

> Generated: 2026-07-15 01:45 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-07-15

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with seven major projects shipping 12 releases across 24 hours. Windows stability remains the ecosystem's most glaring weak point—Claude Code, Codex, and OpenCode all report critical platform-specific crashes that block adoption for a significant user segment. Agent orchestration reliability (subagent lifecycle, turn limits, background session management) is the single most active cross-tool concern, with Gemini CLI, Qwen Code, and Copilot CLI all logging P1 bugs. Meanwhile, the ecosystem is converging on several emerging standards: TUI customization (inspired by Claude Code's status line), MCP security hardening, and multi-workspace daemon architectures. The tools are rapidly differentiating on provider support breadth vs. depth of native integration, with Pi and Kimi pushing hardest on multi-provider compatibility while Claude Code and Copilot CLI double down on proprietary ecosystem lock-in.

---

## 2. Activity Comparison

| Tool | Open Issues (Notable) | Key PRs Today | Releases Today | Overall Health |
|------|----------------------|---------------|----------------|----------------|
| **Claude Code** | 10 hot issues (75-comment thread on Windows cowork) | 9 active PRs | 2 patches (v2.1.209, v2.1.210) | 🌕 Stable with Windows pain points |
| **OpenAI Codex** | 10 hot issues (52-comment browser crash) | 10 PRs | 6 alpha releases (v0.145.0-alpha.8–12) | 🌗 High churn, critical browser regressions |
| **Gemini CLI** | 10 hot issues (P1 hanging bugs) | 5 PRs | 1 nightly (v0.52.0) | 🌗 Agent orchestration gaps |
| **GitHub Copilot CLI** | 10 hot issues (400 error on code review) | 0 PRs | 2 patches (v1.0.71-1, v1.0.71-2) | 🌕 Stable but feature regression risk |
| **Kimi Code CLI** | 2 issues updated | 3 PRs (all merged) | None | 🌑 Low activity, narrow scope |
| **OpenCode** | 10 hot issues (Desktop v2 regressions) | 10 PRs | 2 releases (v1.18.0, v1.18.1) | 🌔 Active iteration, UI transition pain |
| **Pi** | 10 hot issues (provider integration) | 10 PRs | 1 breaking release (v0.80.7) | 🌕 High velocity, broad provider push |
| **Qwen Code** | 10 hot issues (daemon/memory bugs) | 10 PRs | 3 releases (nightly, preview, stable) | 🌔 Steady maturation, multi-workspace focus |
| **DeepSeek TUI** | 10 issues (I18N, agent trust) | 10 PRs | None (v0.8.68 RC in prep) | 🌗 Niche but dedicated community |

*Note: Health scores reflect stability relative to each tool's maturity level, not absolute quality.*

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating ecosystem-wide priorities:

### 3.1 Customizable TUI Status Line
- **Tools:** Claude Code (inspiration), Codex (#17827, 103 👍), Gemini CLI (terminal UX polish requests)
- **Need:** Users want persistent display of token usage, model name, rate limits, git branch, and session metadata.

### 3.2 Multi-Workspace & Daemon Session Management
- **Tools:** Qwen Code (#6378 RFC), Claude Code (background sessions), Gemini CLI (multi-session issues)
- **Need:** Single daemon serving multiple projects with workspace-aware session isolation, reduced resource overhead, and reliable reconnect semantics.

### 3.3 Subagent Lifecycle & Communication
- **Tools:** Gemini CLI (#22323 false success), Qwen Code (#5239 weak communication), Copilot CLI (#4127 background cancellations), Codex (#15723 no wake-on-completion)
- **Need:** Bidirectional notification between subagents and main session, accurate termination reason reporting, and survivor semantics for background tasks.

### 3.4 MCP Security Hardening
- **Tools:** Qwen Code (#6924 trust for read-only auto-approval), Copilot CLI (#4096 OAuth bridging), Claude Code (permission rule deprecation)
- **Need:** Trust-aware permission flows, deterministic secret redaction before model dispatch, and read-only vs. write tool auto-approval boundaries.

### 3.5 Session Management Enhancements
- **Tools:** OpenCode (#36965–#36968 fork/rename/delete/compact), Claude Code (#77651 interleaved thinking data loss), Kimi Code (#2496 fork corruption)
- **Need:** Inline session rename, delete with confirmation, fork from any response, one-click context compaction, and faithful state serialization across reasoning modes.

### 3.6 Provider Extensibility & Model Catalog Freshness
- **Tools:** Pi (#5363 Bedrock Mantle, #6461 xAI OAuth), Kimi Code (#2499 reasoning effort), Qwen Code (#6846 PDF vision bridge), DeepSeek TUI (#4354 MiniMax)
- **Need:** Easy self-serve provider configuration, up-to-date model catalogs, and provider-specific parameter passthrough without silent overrides.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|-------------|------------|-------------|----------|-----|-----------|--------------|
| **Primary Strength** | Hook/plugin ecosystem maturity | GPT-5.6 model exclusivity | Agent orchestration depth | GitHub ecosystem integration | Desktop UI innovation | Provider breadth (20+ providers) | Daemon architecture | TUI visual refinement |
| **Target User** | Power developers, security-conscious teams | OpenAI subscribers, GPT power users | GCP/A2A enterprise shops | GitHub-centric enterprises | VS Code power users | Multi-provider devs, tinkerers | Daemon-first multi-project teams | Chinese-speaking developers |
| **Core Technical Approach** | Plugin/hook system with permission rules | Rust CLI with sandbox via Codex Desktop | Agent delegation with A2A server | GitHub MCP toolset + voice mode | Desktop v2 TUI + web hybrid | Provider-agnostic proxy | Single daemon, multi-workspace | Ambient TUI, stateful terminal |
| **Windows Support Quality** | ⚠️ Poor (cowork VM fails, Bun crashes) | ⚠️ Poor (browser crashes, access violations) | ❌ No Windows-specific issues (likely Unix-heavy) | ⚠️ Moderate (orphaned processes, cards stuck) | ⚠️ Moderate (regressions in v1.18.1) | N/A (proxy tool) | N/A (CLI-focused) | N/A (cross-platform) |
| **Community Size Signal** | High (54 👍 on connection issue) | High (103 👍 on status line FR) | Medium (8 👍 on hanging bug) | Medium (33 👍 on PDF reading) | Medium (37 👍 on hooks compat) | Medium-Low (8 👍 on Bedrock FR) | Medium (23 comments on RFC) | Low (35 comments on trust issue) |
| **Release Cadence** | Patch releases daily | Alpha churn (6 releases/wave) | Nightly builds | Patch releases 2-3x/week | Releases every 2-3 days | Breaking release + patches | Stable + nightly + preview | RC cycles |

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
- **OpenCode** (anomalyco) — Shipping 2 releases/day with 10+ PRs from contributor `ohsalmeron`; Desktop v2 transition signals active UI innovation despite regressions.
- **Pi** (earendil-works) — Breaking release (v0.80.7) plus 10 PRs; strong provider integration velocity (xAI OAuth, Bedrock Mantle).
- **Qwen Code** — 3 release variants + hot-reload milestone (#3696 closed); multi-workspace architecture signals long-term investment.

### Established Stability / Moderate Iteration
- **Claude Code & Copilot CLI** — Both ship patches reliably but face ecosystem-specific friction (Windows for Claude, code review 400 errors for Copilot). Feature velocity is slower than challengers.
- **OpenAI Codex** — Alpha churn with 6 releases suggests active development, but critical browser crashes (#32925) and context degradation (#32806) erode user trust.

### Niche / Lower Activity
- **Kimi Code CLI** — Only 3 merged PRs today, 1 open issue of note; limited community engagement suggests narrower adoption.
- **DeepSeek TUI** — Active RC preparation but smaller community; I18N issues hint at localization challenges.

### Community Sentiment Indicators
| Tool | Highest-Reacted Issue | Signal |
|------|----------------------|--------|
| Claude Code | #69415 (54 👍) — Connection drops | Broad impact, usability threat |
| Codex | #17827 (103 👍) — Status line FR | Strong demand for parity with Claude |
| Gemini CLI | #21409 (8 👍) — Agent hangs | Moderate but concentrated pain |
| Copilot CLI | #443 (33 👍) — PDF reading | Long-standing feature gap |
| OpenCode | #12472 (37 👍) — Hooks compatibility | Community wants Claude Code parity |
| Pi | #5363 (8 👍) — Bedrock Mantle | Niche but enthusiastic provider demand |
| Qwen Code | #6378 (23 comments) — Multi-workspace RFC | Active design conversation |
| DeepSeek TUI | #4032 (35 comments) — Trust issue | Deep engagement but small group |

---

## 6. Trend Signals

### Industry-Level Observations for Decision-Makers

**1. Windows Stability Is the Ecosystem's Largest Unaddressed Risk**
Three of the five CLI tools with Windows support report critical platform-specific bugs: Claude Code (cowork VM service missing, Bun segfaults), Codex (browser crashes, access violations), and OpenCode (v2 UI regressions). For enterprises standardizing on Windows, this creates a material vendor lock-in risk. The root cause appears to split between infrastructure (Hyper-V container services, WebView2) and runtime (Bun vs. Node.js stability on Intel hardware). Tools using native Rust (Codex, Pi) fare somewhat better than Bun-based stacks.

**2. Agent Orchestration Is the Next Frontier—and Pain Point**
Every tool with subagent capabilities logs bugs around lifecycle management: false success reporting (Gemini), silent cancellation (Copilot), weak communication (Qwen), and missed wake signals (Codex). The model "delegate and forget" pattern is fundamentally unreliable without robust feedback loops. Expect the tools that solve bidirectional subagent communication and accurate termination reason propagation to gain significant enterprise traction.

**3. The TUI Renaissance Has a UX Ceiling**
Overlapping text in tmux (Claude Code), garbled diff previews (Qwen Code), non-scrollable overflow (Qwen Code), and Unicode decoration pollution (DeepSeek TUI) show that terminal UI rendering remains fragile. While TUI tools offer unmatched performance and scripting potential, they hit a quality-of-experience ceiling that desktop-native UIs (OpenCode Desktop v2) are starting to exploit. The hybrid web+TUI approach (Copilot CLI, OpenCode) may become the dominant pattern for non-power-users.

**4. Provider Agnosticism Is Winning but Fragile**
Pi's 20+ provider support and Kimi's Moonshot focus represent opposite strategies, but the community trend is clear: users want model choice without vendor lock-in. However, the fragmentation of thinking/reasoning formats (Claude Fable 5, GPT-5.6 Sol, Gemini thinking), session ID semantics, and rate-limit implementations creates significant integration complexity. Pi's breaking change on session affinity format (#v0.80.7) and Codex's model catalog migration (PR #33173) exemplify this tension.

**5. Security and Trust Are Shifting Left**
Multiple tools show movement toward pre-execution security: Claude Code deprecates legacy permission rules; Qwen Code mandates explicit trust for MCP read-only hints (PR #6924); Gemini CLI limits recursive reasoning turns (PR #28164). The pattern is moving from reactive permission prompts to declarative, deterministic trust policies. This aligns with enterprise compliance requirements and is likely to accelerate.

**6. Documentation Gaps Signal Market Maturation**
Claude Code saw 10+ doc issues filed by a single user (#coygeek) covering sandboxing, memory limits, agent tool security, and MCP SDK connections. DeepSeek TUI faces I18N translation quality issues. As these tools move from early adopter to mainstream adoption, documentation quality and localization become competitive differentiators. The tools investing in structured docs now (Claude Code's doc sweep, DeepSeek's documentation-led redesign) are positioning for the next growth phase.

**7. Pricing Transparency Is an Emerging Pain Point**
Codex users report subscription tier confusion (Pro limits applied to Plus subscribers, #29968); DeepSeek TUI fixes zero-cost cache writes (#4318); OpenCode adds cache write token reporting (PR #36752). As AI CLI usage scales from individual developers to team budgets, accurate cost attribution and transparent billing become table stakes. Tools with built-in cost dashboards (Pi's offline scorecard, Copilot CLI's `/chronicle cost-tips`) gain operational trust.

---

**Bottom Line for Technical Decision-Makers:**
- **If you need reliability today:** Claude Code (stable patches) or Copilot CLI (GitHub integration) unless your team is Windows-heavy.
- **If you value provider flexibility:** Pi offers the broadest coverage but expects configuration friction.
- **If you prioritize agent orchestration:** Gemini CLI has depth but unresolved P1 hanging bugs; Qwen Code's multi-workspace daemon is architecturally promising.
- **If you want the latest models fastest:** Codex (GPT-5.6 exclusive) and Pi (rapid provider addition) lead on freshness.
- **If community velocity signals future direction:** OpenCode and Qwen Code show the strongest feature iteration momentum.

The ecosystem remains fragmented but is converging on shared patterns—customizable TUI, multi-agent lifecycle management, MCP security hardening, and provider-agnostic architectures will define the winners in the next 6–12 months.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (Data as of 2026-07-15)

## 1. Top Skills Ranking

The following 8 Skills (or Skill improvements) have drawn the most community discussion and attention via pull requests. All remain **open** as of the data snapshot.

| Skill (PR) | Description | Discussion Highlights | Status |
|---|---|---|---|
| **[Document Typography](https://github.com/anthropics/skills/pull/514)** | Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. | Strong consensus that typographic defects are pervasive; users want automated post-processing. | Open |
| **[ODT Skill](https://github.com/anthropics/skills/pull/486)** | Enables creation, template filling, and ODT-to-HTML conversion for OpenDocument files (.odt, .ods). | Interest in cross-format compatibility; some debate on scope (include .ods?). | Open |
| **[Frontend Design Improvement](https://github.com/anthropics/skills/pull/210)** | Revises existing skill to be more actionable and specific for single-conversation use. | Community agreed the original was too vague; this addresses “what can Claude actually do?” | Open |
| **[Skill Quality & Security Analyzer](https://github.com/anthropics/skills/pull/83)** | Two meta-skills: evaluate skills across structure/documentation (20%) and security patterns. | High demand for quality gates; concerns about false positives in security checks. | Open |
| **[Self-Audit Skill v1.3.0](https://github.com/anthropics/skills/pull/1367)** | Four-dimension reasoning audit plus mechanical file verification before output delivery. | Universality praised; some worry about token overhead for large outputs. | Open |
| **[Testing Patterns Skill](https://github.com/anthropics/skills/pull/723)** | Covers testing trophy model, unit/React/E2E patterns, and edge case guides. | Broad support; requests for additional coverage of mocking strategies. | Open |
| **[SAP-RPT-1-OSS Predictor](https://github.com/anthropics/skills/pull/181)** | Wraps SAP’s open-source tabular foundation model for predictive analytics on business data. | Niche but enthusiastic; discussion about model download size and API keys. | Open |
| **[Color Expert Skill](https://github.com/anthropics/skills/pull/1302)** | Comprehensive color knowledge skill: naming systems (ISCC-NBS, Munsell, XKCD), color spaces table, accessibility. | Well-received for design workflows; minor debate on including Pantone values. | Open |

---

## 2. Community Demand Trends

From the most-discussed Issues, several clear patterns emerge for new Skill directions:

- **Agent Governance & Safety** — Issue #412 (6 comments) proposes a dedicated *agent-governance* skill for policy enforcement, threat detection, and audit trails. Combined with #492 (34 comments, security namespace abuse), the community is actively pushing for trust and safety guardrails.
- **Compact Memory & Notations** — Issue #1329 (9 comments) requests a *compact-memory* skill that uses symbolic notation to store agent state more efficiently, reducing context waste from verbose prose.
- **Reasoning Quality Gates** — Issue #1385 (3 comments, very recent) outlines a three-stage pipeline (pre-task calibration → adversarial review → delivery verification) to catch reasoning errors across the full session lifecycle.
- **Org-Wide Skill Sharing** — Issue #228 (14 comments, 7 👍) asks for built-in sharing mechanisms instead of manual `.skill` file distribution—an infrastructure demand rather than a skill content request.
- **MCP Exposure** — Issue #16 (4 comments) suggests exposing Skills as MCP tools, enabling programmatic API contracts for AI-generated software.
- **Broken Tooling (skill-creator)** — Issues #556 (12 comments), #1169 (3 comments), and #1061 (3 comments) all report that `run_eval.py` returns 0% recall on Windows, blocking skill authors from optimizing descriptions. This is the most urgent *infrastructure* pain point.

*Top-anticipated new Skill areas:* **agent safety/governance**, **memory compaction**, **reasoning quality auditing**, and **MCP integration**.

---

## 3. High-Potential Pending Skills

These open PRs show active discussion and are likely to be merged soon:

- **[Document Typography](https://github.com/anthropics/skills/pull/514)** — Single-skill scope, clear value, no major blockers. Last updated 2026-03-13.
- **[ODT Skill](https://github.com/anthropics/skills/pull/486)** — Long-running (since March), but active discussion on scope. May land as a narrower first cut.
- **[Testing Patterns Skill](https://github.com/anthropics/skills/pull/723)** — Well-structured, community alignment. Last updated 2026-04-21.
- **[Color Expert Skill](https://github.com/anthropics/skills/pull/1302)** — Low controversy, high utility for designers. Last updated 2026-06-12.
- **[Self-Audit Skill](https://github.com/anthropics/skills/pull/1367)** — Very recent (June 28) but already cited in issue #1385 as a building block. Momentum is high.
- **[Skill Quality & Security Analyzer](https://github.com/anthropics/skills/pull/83)** — Meta-skills that could be merged quickly given the ongoing security discussion (#492).

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for quality-related skills**—both applied (typography, document formatting, testing patterns) and meta (self-audit, reasoning gates, skill quality analyzers)—while simultaneously demanding that the skill-creation tooling itself be made cross-platform reliable (Windows fixes, YAML validation, accurate recall evaluation).

---

# Claude Code Community Digest — 2026-07-15

## Today's Highlights
Two patch releases landed today: **v2.1.210** adds a live elapsed‑time counter for long‑running tool calls and deprecation warnings for legacy permission rules, while **v2.1.209** fixes a regression where `/model` dialogs were blocked in agent background sessions. On the issue tracker, Windows cowork instability remains the dominant pain point (75‑comment thread on missing VM services), and a flurry of documentation‑gap issues signals that the docs team may be preparing a sweep.

---

## Releases

### [v2.1.210](https://github.com/anthropics/claude-code/releases/tag/v2.1.210)
- **Live elapsed‑time counter** on the collapsed tool summary line – long‑running tool calls now visibly tick instead of appearing stuck.
- **Deprecation warnings** for `Write(path)`, `NotebookEdit(path)`, and `Glob(path)` permission rules – users are advised to switch to `Edit(path)` or `Read(path)`.

### [v2.1.209](https://github.com/anthropics/claude-code/releases/tag/v2.1.209)
- **Fixed** `/model` and other dialogs being blocked in `claude agents` background sessions – an overly broad guard was reverted.

---

## Hot Issues (10 noteworthy)

### 1. [#74649 – Missing HCS services: vfpext – Cowork not working on Windows 11 Pro](https://github.com/anthropics/claude-code/issues/74649)
75 comments, 4 👍. The highest‑activity issue right now. Cowork fails because the Hyper‑V container service (vfpext) isn’t present. Multiple users confirm repro across Windows 11 Pro builds. No fix yet.

### 2. [#69415 – API Error: Connection closed mid‐response, frequent enough to make Claude Code unusable](https://github.com/anthropics/claude-code/issues/69415)
26 comments, 54 👍 (highest reaction count). Users on WSL and VSCode see dropped connections mid‑response. The heavy reaction tally signals broad impact across environments.

### 3. [#64592 – Cowork VM service not running on Windows 11 (fresh repro + workaround)](https://github.com/anthropics/claude-code/issues/64592)
11 comments. Extends a cluster of closed issues (#54891, #61559). Workaround: manually enable Virtual Machine Platform. Still waiting for an official fix.

### 4. [#73587 – Desktop app ignores `permissions.allow` rules — prompts for everything](https://github.com/anthropics/claude-code/issues/73587)
5 comments. A regression in the desktop app: even allow‑listed paths (including Claude’s own config directory) trigger permission prompts. This breaks workflows that rely on trust presets.

### 5. [#77548 – Advisor treats genuine transcript content as prompt injection](https://github.com/anthropics/claude-code/issues/77548)
Filed yesterday, 1 comment. The advisor model (`advisorModel: fable`) can mis‑classify real tool results as injection and deny them. Distinct from the availability bug in #76199. Could erode trust in the advisor feature if widespread.

### 6. [#77625 – Claude Code crashes with 0xC0000005 on Windows 11 with Bun‐based versions](https://github.com/anthropics/claude-code/issues/77625)
Filed today. Windows users on Bun‑based versions (v2.1.112+) encounter access violation crashes at startup. Related to earlier #66683 (Meteor Lake segfault) — both point to Bun runtime instability on certain Windows hardware.

### 7. [#77615 – UI rendering broken with overlapping text in tmux on macOS](https://github.com/anthropics/claude-code/issues/77615)
Overlapping/garbled TUI inside tmux. Bare iTerm works fine. This regression (v2.1.202) makes the tool unusable for tmux users – a common development setup.

### 8. [#77651 – Assistant text between tool calls silently lost (interleaved thinking)](https://github.com/anthropics/claude-code/issues/77651)
Filed today. When using `claude-fable-5` with interleaved thinking, the text the model emits between tool calls is not rendered, not available via Ctrl+O, and not persisted to the session `.jsonl`. Critical for users who rely on those transcripts.

### 9. [#77649 – Background‐session daemon: duplicate idle sessions on reconnect](https://github.com/anthropics/claude-code/issues/77649)
A bundle of four lifecycle defects in the background daemon: uns‑ettled workers pin the daemon, reconnect re‑forks duplicate sessions, and `--continue` drops permission mode. Complex, but indicates the background‑session machinery needs hardening.

### 10. [#66683 – Bun startup segfault on Windows 11 + Intel Meteor Lake](https://github.com/anthropics/claude-code/issues/66683)
2 comments but a recurrence after an earlier issue (#55219) was auto‑closed as stale. Core Ultra 5 (Meteor Lake) users crash on startup with any Bun‑based version. No fix yet.

---

## Key PR Progress (10 important)

### 1. [#77613 – `claude-compare`](https://github.com/anthropics/claude-code/pull/77613)
A new open PR from a community contributor. Likely a comparison/benchmarking tool for Claude sessions. Worth watching.

### 2. [#77556 – Fix hook schema validator for plugin hooks.json format](https://github.com/anthropics/claude-code/pull/77556)
Fixes two bugs in the plugin-dev hook schema validation script that caused false failures on valid configs. Affects the Hook Development skill shipped with the plugin.

### 3. [#77492 – Fix hookify: match Write and prompt rules](https://github.com/anthropics/claude-code/pull/77492)
A reopened and reworked fix for hookify. Makes file rules inspect content passed to `Write`, maps simple prompt rules to the correct payload, and adds regression tests. Important for users relying on hooks for security or compliance.

### 4. [#77443 – Fix ralph‑wiggum stop hook jq error handling under `set -e`](https://github.com/anthropics/claude-code/pull/77443)
The stop hook used `$?` after `jq` but `set -e` caused an early exit before the error check. This PR makes the error path reachable.

### 5. [#77442 – Fix issue‑automation telemetry and dead `days_back` input](https://github.com/anthropics/claude-code/pull/77442)
Three correctness fixes: Statsig events timestamped in 1970 (fixed with correct `now | floor`), workflow‑to‑script argument mismatch, and an always‑overridden `days_back` input.

### 6. [#77439 – Sync security‑guidance listing with v2.0.0 plugin manifest](https://github.com/anthropics/claude-code/pull/77439)
The security‑guidance plugin was rewritten to v2.0.0 but marketplace listings still described v1.0.0. This PR updates `.claude-plugin/marketplace.json` and the plugin index.

### 7. [#77427 – Make code‑reviewer a leaf agent in pr‑review‑toolkit](https://github.com/anthropics/claude-code/pull/77427)
Restricts the `code-reviewer` to repository‑inspection tools only, preventing it from spawning further agents. This closes a recursion risk and makes the agent’s scope explicit.

### 8. [#76298 – Document Remote Control background‑task panel](https://github.com/anthropics/claude-code/pull/76298)
Merged (closed). Updates Remote Control docs to describe the web/mobile background‑task panel and task status synchronization added in v2.1.205.

### 9. [#77260 – Previous iteration of hookify fix (closed)](https://github.com/anthropics/claude-code/pull/77260)
Replaced by #77492, but noteworthy as an intermediate attempt that was reopened before being superseded.

### 10. [#77427 – (already listed)](https://github.com/anthropics/claude-code/pull/77427)
— (Only 9 distinct open PRs in the data; selecting 10 from total 9 items repeats. Use 9 key PRs.)

---

## Feature Request Trends

- **Cowork VM customization** – The most upvoted feature request ([#56089](https://github.com/anthropics/claude-code/issues/56089), 26 👍) asks for the ability to configure where the cowork VM bundle (vhdx) is stored. Users need control over disk space and drive location.
- **Session title language** – [#72004](https://github.com/anthropics/claude-code/issues/72004) (4 👍) requests that session titles respect the user’s conversation language instead of always being English.
- **Fable 5 in plan mode** – [#77650](https://github.com/anthropics/claude-code/issues/77650) (filed today) asks for Fable 5 model support in plan mode, specifically for security audits.
- **Documentation gaps** – A burst of 10+ doc issues today from a single user (coygeek) covering undocumented behavior in sandboxing, memory limits, agent tool security, skills, accessibility, and MCP SDK connection. This signals a community demand for more precise documentation.

---

## Developer Pain Points

1. **Windows cowork unreliability** – Three separate issues (#74649, #64592, #56089) with a combined 92 comments and 30 👍. The VM service fails to start, HCS components are missing, and there’s no storage customization. Cowork on Windows remains a blocker for many.

2. **Permission prompt regressions** – Desktop app (#73587) ignores `permissions.allow` rules; MCP allowlisted tools still trigger prompts on fresh sessions (#76238). Users who have carefully configured trust are getting friction.

3. **Bun‑based crashes on Windows** – Two issues (#66683, #77625) report segfaults and access violations on specific hardware (Meteor Lake, general). The crash code 0xC0000005 suggests a runtime memory issue.

4. **Connection stability** – #69415 (54 👍, highest reaction) shows that connection drops during long responses are making the tool unusable for many, especially on WSL/VSCode.

5. **TUI rendering regressions** – #77615 (tmux overlapping text) and #77655 (subagent view showing wrong identity) show that terminal UI changes are introducing visual bugs that break common workflows.

6. **Data loss in interleaved thinking** – #77651 reports that assistant text between tool calls is silently dropped when using Fable 5. This undermines the value of extended reasoning traces.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-15

## Today's Highlights

Today’s data shows a cluster of **alpha releases** (v0.145.0-alpha.8–12) for the Rust CLI, though no changelogs accompany them. The most urgent community concern is a **critical browser plugin crash** (`Cannot redefine property: process`) affecting both the bundled in-app browser and Chrome extension, with 52 comments and 31 upvotes. Meanwhile, a **SEVERE regression** in context window size (353K → 258K) for GPT-5.6 Sol sparked 22 comments, and a long-running **feature request** for a customizable status line (103 👍) continues to gather steam.

---

## Releases

| Version | Notes |
|---------|-------|
| `rust-v0.144.4` | Patch release with no user-facing changes. |
| `rust-v0.145.0-alpha.8` | Alpha release; no changelog provided. |
| `rust-v0.145.0-alpha.9` | Alpha release; no changelog provided. |
| `rust-v0.145.0-alpha.10` | Alpha release; no changelog provided. |
| `rust-v0.145.0-alpha.11` | Alpha release; no changelog provided. |
| `rust-v0.145.0-alpha.12` | Alpha release; no changelog provided. |

*No meaningful user-visible changes were documented in today’s releases.*

---

## Hot Issues

1. **[#32925] Browser plugin fails – `Cannot redefine property: process`**  
   Both bundled browser and Chrome extension crash on initialization (52 comments, 31 👍). Affects Codex Desktop 26.707.71524 on Darwin. High-severity blocking issue for Browser Use workflows.  
   [GitHub](https://github.com/openai/codex/issues/32925)

2. **[#17827] Customizable status line (Feature Request)**  
   Long‑standing request for a TUI status line similar to Claude Code’s (28 comments, 103 👍). Users want token usage, model, rate limits, git branch, etc.  
   [GitHub](https://github.com/openai/codex/issues/17827)

3. **[#32806] SEVERE REGRESSION: GPT-5.6 Sol context cut**  
   Advertised 1.05M context drops to 258K (22 comments, 23 👍). Reported as a regression for Pro users, blocking large‑project analysis.  
   [GitHub](https://github.com/openai/codex/issues/32806)

4. **[#25463] Desktop project threads disappear from UI**  
   Conversations become invisible in project view but remain on disk (16 comments). Users must manually search for JSONL files.  
   [GitHub](https://github.com/openai/codex/issues/25463)

5. **[#29968] Subscription usage anomalies (Pro → Plus limits)**  
   Pro20x subscribers see Plus‑tier rate limits (16 comments, 14 👍). No official response yet; impacts heavy users.  
   [GitHub](https://github.com/openai/codex/issues/29968)

6. **[#20880] Silent `~/Documents/Codex` folder creation**  
   App creates empty folder on every launch (16 comments, 36 👍). Nuisance bug with no opt‑out.  
   [GitHub](https://github.com/openai/codex/issues/20880)

7. **[#30178] Windows Desktop in‑app browser crashes main app**  
   WebView navigation causes full crash (15 comments). Critical for Windows users relying on Browser Use.  
   [GitHub](https://github.com/openai/codex/issues/30178)

8. **[#32683] Windows crash in CrBrowserMain (access violation)**  
   Crashes when Browser Use opens a page (13 comments, 2 👍). Stack trace points to `chrome.dll`.  
   [GitHub](https://github.com/openai/codex/issues/32683)

9. **[#28919] Windows missing “Control other devices” tab**  
   Remote control feature missing in Settings on Windows (12 comments, 21 👍). Feature parity gap.  
   [GitHub](https://github.com/openai/codex/issues/28919)

10. **[#15723] Subagents do not wake calling agent on completion**  
    Background tasks complete silently (10 comments, 5 👍). Causes missed outputs and confusion.  
    [GitHub](https://github.com/openai/codex/issues/15723)

---

## Key PR Progress

1. **[#33201] Branch conversations when editing earlier TUI prompts**  
   Fork conversation instead of rolling back, preserving original history.  
   [GitHub](https://github.com/openai/codex/pull/33201)

2. **[#33200] Separate exec permission paths from core models**  
   Refactors permission types to handle native vs. portable URIs for sandbox contexts.  
   [GitHub](https://github.com/openai/codex/pull/33200)

3. **[#33198] Keep interrupted prompts in conversation history**  
   Interrupted prompts (Esc/Ctrl‑C) now stay visible with a blank composer for the next input.  
   [GitHub](https://github.com/openai/codex/pull/33198)

4. **[#33187] Honor workspace spend controls in rate‑limit handling**  
   Prevents stale rate‑limit metadata from overriding newer workspace hard stops.  
   [GitHub](https://github.com/openai/codex/pull/33187)

5. **[#33185] Keep approval test targets in temporary home**  
   Approval tests now resolve relative paths consistently in test environments.  
   [GitHub](https://github.com/openai/codex/pull/33185)

6. **[#33184] Reuse MCP tool catalogs across sessions**  
   Caches unchanged stdio MCP server configurations to avoid re‑initialization delays.  
   [GitHub](https://github.com/openai/codex/pull/33184)

7. **[#33182] Preserve plugin install failure subtypes during imports**  
   Carries detailed error subtypes through progress/completion notifications.  
   [GitHub](https://github.com/openai/codex/pull/33182)

8. **[#33180] Serialize concurrent MCP stdin writes**  
   Uses a semaphore to prevent race conditions when sending multiple JSON‑RPC messages.  
   [GitHub](https://github.com/openai/codex/pull/33180)

9. **[#33177] Support model catalog templates for Guardian policy prompts**  
   Adds `policy_template` field for customizing auto‑review instructions.  
   [GitHub](https://github.com/openai/codex/pull/33177)

10. **[#33173] Migrate GPT-5.4 uses to GPT-5.6 variants**  
    Hides GPT-5.4 models and redirects users to Terra/Luna, with memory consolidation updates.  
    [GitHub](https://github.com/openai/codex/pull/33173)

---

## Feature Request Trends

- **Customizable TUI status line** (issue #17827, 103 👍) – the most popular request, mirroring Claude Code’s approach.
- **Restore `Option+Space` quick chat** on macOS (#31925, 11 👍) – lost after ChatGPT/Codex app unification.
- **Add “Read Aloud” for responses** (#20957, 7 👍) – accessibility feature already present in ChatGPT.
- **Better remote device control** on Windows (#28919, 21 👍) – missing settings tab.
- **Banked usage resets** for promotions (#33017) – users want official communication on resets.

---

## Developer Pain Points

1. **Browser/plugin crashes on Windows** (#30178, #32683, #32925, #32935, #33004) – Multiple reports of `Cannot redefine property: process` and access violations. Severely impacts Browser Use functionality.
2. **Context window degradation** (#32806) – Advertised capacity not delivered; users feel misled.
3. **Subscription/rate‑limit confusion** (#29968, #33017) – Pro users getting Plus limits, promotional resets missing.
4. **Silent data issues** (#25463, #20880) – Conversations vanish from UI, unwanted folders created.
5. **Windows feature gaps** (#28919, #31220) – Missing remote control, sandbox restrictions.
6. **Session stability** (#20213, #18723, #24045) – SQLite lock contention, websocket disconnects, reconnect loops.
7. **Subagent coordination** (#15723) – Background processes fail to signal completion.

*Overall, Windows‑specific bugs and browser integration failures dominate the trouble reports, while the community continues to push for UI customization and parity with Claude Code.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-15

**Data source:** [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## Today’s Highlights

A new nightly build (v0.52.0-nightly.20260715) was released with automated version bumps. The community continues to report critical agent orchestration bugs — notably, subagents incorrectly reporting `GOAL` success when actually hitting turn limits (Issue #22323), and the generalist agent hanging indefinitely on simple tasks (Issue #21409). Meanwhile, a high-priority security issue around Auto Memory’s logging of secrets before redaction has drawn renewed attention (Issue #26525).

---

## Releases

- **[v0.52.0-nightly.20260715.gfa975395b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260715.gfa975395b)** — Routine nightly release with automated version bump. No feature changes visible in the changelog.
  - [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260714.gfa975395b...v0.52.0-nightly.20260715.gfa975395b)

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *Priority: P1 | Comments: 10 | 👍: 2*  
   A critical bug where `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` despite actually hitting its maximum turn limit before performing any analysis. This masks real failures and misleads users into thinking work was completed. Community members have flagged this as a systemic AI eval reporting issue.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *Priority: P1 | Comments: 7 | 👍: 8*  
   Longstanding P1 bug: the generalist agent hangs indefinitely (up to an hour) on simple operations like folder creation. Workaround exists (instructing the model not to defer to subagents), but the root cause remains unresolved. Heavy community upvotes indicate this is a widespread frustration.

3. **[#25166 — Shell command execution gets stuck with “Waiting input” after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *Priority: P1 | Comments: 4 | 👍: 3*  
   The CLI hangs after executing trivial shell commands, showing the command as still active and “awaiting user input.” Affects even commands that cannot prompt for input. Likely related to PTY handling or output stream buffering.

4. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *Priority: P1 | Comments: 4 | 👍: 1*  
   `browser_agent` fails on Wayland display servers with a vague `Termination Reason: GOAL`. No usable error output. Affects a growing segment of Linux users.

5. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *Priority: P2 | Comments: 5 | 👍: 0*  
   Auto Memory only marks sessions as processed when the extraction agent successfully reads the transcript. If a session is skipped as low-signal, it remains unprocessed and resurfaces repeatedly, causing infinite retry cycles. Tied to broader memory quality concerns.

6. **[#20079 — ~/.gemini/agents/filename.md is not recognized as an agent if filename.md is a symlink](https://github.com/google-gemini/gemini-cli/issues/20079)**  
   *Priority: P2 | Comments: 4 | 👍: 0*  
   Symlinked agent definitions under `~/.gemini/agents/` are silently ignored. Blocks users who manage agent configs via dotfile repos or symlinks.

7. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *Priority: P2 | Comments: 3 | 👍: 0*  
   Auto Memory reads local transcripts and sends selected content to the extraction model *before* redaction occurs. Secret content is thus exposed in model context and could be logged by the service. Request for deterministic redaction *before* model dispatch.

8. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   *Priority: P2 | Comments: 3 | 👍: 0*  
   With more than ~128 tools enabled, the CLI hits a 400 error from the Gemini API. No smart tool-scoping exists. Blocks users with large custom skill libraries or many MCP tools.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
   *Priority: P2 | Comments: 3 | 👍: 1*  
   Models sometimes issue `git reset`, `--force` flags, or destructive database commands when safer alternatives exist. Proposal to add safety prompts or refusal patterns for destructive actions.

10. **[#22466 — Fix instances of incorrect \n escape behavior](https://github.com/google-gemini/gemini-cli/issues/22466)**  
    *Priority: P2 | Comments: 2 | 👍: 0*  
    Naive logic to work around Gemini’s handling of `\n` breaks in certain contexts. Reported in the CLI users chat. Simple fix but affects output formatting.

---

## Key PR Progress

1. **[#28402 — chore/release: bump version to 0.52.0-nightly.20260715.gfa975395b](https://github.com/google-gemini/gemini-cli/pull/28402)**  
   Automated nightly version bump. (Merged)

2. **[#28319 — refactor(a2a-server): enforce path trust check prior to environment loading and isolate task environment](https://github.com/google-gemini/gemini-cli/pull/28319)**  
   *(Size: M/L/XL | Open)*  
   Refactors `CoderAgentExecutor` to perform workspace path trust checks *before* loading environment variables. Introduces `AsyncLocalStorage` for env isolation across tasks. Security hardening for A2A server scenarios.

3. **[#24303 — feat(diagnostics): Native V8 Memory & Profiling Suite](https://github.com/google-gemini/gemini-cli/pull/24303)**  
   *(Size: L | 🔒 Maintainer Only | Open)*  
   GSoC 2026 proposal adding a terminal-integrated performance and memory investigation companion. Implements native V8 heap snapshots, allocation profiling, and flamegraph generation directly from the CLI.

4. **[#28164 — fix(core): limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)**  
   *(Size: M/L/XL | Help Wanted | Open)*  
   Enforces a strict limit of 15 recursive reasoning turns per request (configurable via `maxSessionTurns`). Addresses infinite loop scenarios that consume local CPU and API quota. Community contribution by `amelidev`.

5. **[#28401 — fix(shell): bound command output sent to the model](https://github.com/google-gemini/gemini-cli/pull/28401)**  
   *(Size: M | Priority: P1 | Open)*  
   Prevents shell tool from forwarding unbounded output (e.g., `find /`, verbose builds) to the model context. Adds an output size cap to avoid token waste and degraded responses. Directly addresses a common user pain point.

---

## Feature Request Trends

The community is consistently requesting improvements in three areas:

1. **Agent orchestration and reliability** — Better subagent lifecycle handling (recovery after interrupts, turn limits), smarter delegation to custom skills, and visible subagent trajectories for debugging. Multiple P1 bugs suggest this is the single greatest user friction point.

2. **Security and safety guards** — Destructive command prevention, deterministic secret redaction before model processing, and stricter permission controls for subagents. Users want the agent to “think twice” before running risky operations.

3. **AST-aware tooling** — A cluster of issues (Issues #22745, #22746) proposes using AST-aware file reads and codebase mapping to reduce turn overhead and improve code navigation precision, especially for large repositories.

4. **Terminal UX polish** — Requests for flicker-free resizing, corruption-free exit from external editors, and proper handling of interactive prompts (e.g., `vite create`).

---

## Developer Pain Points

- **Pervasive hanging bugs** — Both the generalist agent (#21409) and shell execution (#25166) hang indefinitely on simple tasks. Users report waiting hours and needing to force-kill sessions.
- **Subagent permission changes without notice** — Since v0.33.0, subagents have been executing even when explicitly disabled in config (#22093). Users feel their security preferences are being ignored.
- **Terminal corruption after editor use** — Exiting external editors (vim, nano) in `terminalBuffer` mode corrupts the display and requires a full screen refresh (#24935).
- **Tool count limit hard crashes** — Hitting the 128-tool ceiling (#24246) results in a 400 error with no graceful fallback, making the CLI unusable for power users with extensive tool registrations.
- **Missing subagent context in bug reports** — The `/bug` command only captures the main session, omitting subagent trajectories (#21763), making root-cause analysis nearly impossible for agent-chain failures.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-07-15

## Today’s Highlights

Two patch releases (v1.0.71-1 and v1.0.71-2) shipped yesterday, delivering voice device persistence, a new plugin marketplace system, and canvas support for extensions. Meanwhile, the community flagged several blockers: a persistent 400 error on code reviews, silent voice transcription failures, and a critical session‑size blow‑up caused by deleted binaries being stored in conversation history.

## Releases

- **v1.0.71-2** – *Added:* `/voice` devices selection and persistence; ability to limit which built‑in agents are available to tasks/subagents; canvas support for extension‑driven interactions. *Improved:* richer cost profile recommendations in `/chronicle cost-tips`.

- **v1.0.71-1** – *Added:* Persistence of GitHub MCP toolset/tool config via `settings.json`; `plugins marketplace` subcommands (list, add, remove); sidebar session persistence across restarts; `plugins marketplace browse` and `update` commands. *Other:* Split infrastructure changes.

## Hot Issues (10 noteworthy)

1. **[#1274 – CLI constantly getting 400 errors for invalid request body](https://github.com/github/copilot-cli/issues/1274)**  
   *area:tools* – 95% of recent code‑review attempts fail with 400. 25 comments, 11 👍. Likely server‑side validation or malformed request. High impact for users relying on diff review.

2. **[#4024 – Voice mode: all bundled ASR models fail silently](https://github.com/github/copilot-cli/issues/4024)**  
   *area:models* – `/voice` captures audio but every transcription is empty across all three Nemotron models. A routing bug in `MultiModalProcessor` is suspected. 8 comments.

3. **[#443 – Feature Request: Built‑in PDF Reading Support](https://github.com/github/copilot-cli/issues/443)**  
   *area:tools* – Still heavily upvoted (33 👍). Users want native PDF parsing instead of relying on external `pdftotext`. No progress yet.

4. **[#2165 – Ubuntu keychain support is broken](https://github.com/github/copilot-cli/issues/2165)**  
   *area:platform-linux, area:authentication* – Two bugs: wrong documentation and broken `secret-tool` integration. 21 👍, 3 comments.

5. **[#4096 – Third‑party MCP server shows “Connected” but tools missing from CLI sessions](https://github.com/github/copilot-cli/issues/4096)**  
   *area:authentication, area:mcp* – OAuth token never bridged to spawned CLI sessions despite green “Connected” badge. Affects Atlassian Remote MCP and similar integrations. 3 comments.

6. **[#4097 – `apply_patch` stores deleted binary in session history, permanently exceeding CAPI 5 MB limit](https://github.com/github/copilot-cli/issues/4097)**  
   *area:sessions, area:context-memory, area:tools* – Deleting a large binary inflates conversation history, causing subsequent requests to exceed the 5 MB limit and forcing `/compact` loops. 1 👍.

7. **[#4103 – Plugin marketplace clone disables Git credential helpers](https://github.com/github/copilot-cli/issues/4103)**  
   *area:authentication, area:plugins* – Regression from v1.0.70: cloning private HTTPS repos (e.g., Azure DevOps) fails because Git Credential Manager is bypassed. 2 👍.

8. **[#4127 – Background agents cancelled when a new user turn emits `user.abort`](https://github.com/github/copilot-cli/issues/4127)**  
   *triage* – Submitting a new turn cancels background subagents, leaving them as `cancelled` with unreadable IDs. Fresh triage, no comments yet.

9. **[#4128 – SQL tool blocks reserved keywords inside quoted string literals](https://github.com/github/copilot-cli/issues/4128)**  
   *triage* – The built‑in `sql` tool rejects valid SQL when a keyword (e.g., `SELECT`) appears only inside a string literal. Blocks storing ordinary text like “Select a todo”.

10. **[#4118 – `/app` command does not select current working directory by default](https://github.com/github/copilot-cli/issues/4118)**  
    *triage* – 33 👍 in a few hours. Users want the GUI app to auto‑select the CWD instead of requiring manual navigation. Strong community interest.

## Key PR Progress

No pull requests were updated or merged in the last 24 hours.

## Feature Request Trends

- **Native PDF reading** (#443) remains the most‑requested tool extension, with 33 👍.
- **Better in‑session navigation**: Show conversation title in main view (#4124, 0 👍 but clear need), allow double‑tap Enter to skip queue (#4125).
- **Customization**: Color/theme customization (#4117), granular OTel auth for enterprises (#3477).
- **JSON output completeness**: Include token/cost usage in `--output-format json` (#4107).
- **Plugin & MCP polish**: Fix OAuth bridging (#4096), persist tool usage metadata.
- **Voice reliability**: Resolve silent transcription failures (#4024) – a top priority for voice mode users.

## Developer Pain Points

- **400 errors on code review** (#1274) – many users unable to use a core feature.
- **Voice ASR broken** (#4024) – blocks the `/voice` workflow entirely.
- **Ubuntu keychain & snap issues** (#2165, #4109) – Linux users face clipboard and auth friction.
- **Session bloat from binary deletions** (#4097) – forces manual `compact` and breaks long sessions.
- **Plugin marketplace Git credential regression** (#4103) – stops private repo usage.
- **Background agent cancellation** (#4127) – disrupts multi‑agent workflows.
- **Windows orphaned processes and stuck confirmation cards** (#4111, #4114) – degrade interactive sessions.
- **Subagent relative link resolution** (#4122) and **ignored `AGENTS.MD`** (#4123) – hinders custom agent development.
- **Copy/paste contamination** (#4126, #4116) – minor but annoying UX regressions.
- **Session data loss after unexpected restart** (#4115) – threatens reliability for heavy users.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-15

## Today's Highlights
No new releases landed in the last 24 hours, but three important bug‑fix pull requests were merged, targeting reasoning‑effort serialization, empty‑string reasoning content, and dynamic completion budget tuning. Meanwhile, a long‑standing rate‑limit bug (issue #2318) remains open and has seen renewed community attention.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues
*(Only two issues were updated in the last 24h; both are listed below.)*

### #2318 — [bug] request reached organization TPD rate limit, current: 1505241  
- **Author:** globalvideos272-lab  
- **Status:** Open since 2026-05-18, last updated 2026-07-14  
- **Comments:** 1 | 👍 1  
- **Link:** [Issue #2318](https://github.com/MoonshotAI/kimi-cli/issues/2318)  
- **Why it matters:** Reports a critical bug where the CLI incorrectly calculates or respects the “transactions per day” (TPD) limit for the Moonshot API, causing unexpected rate‑limit errors even when the user may be within quota. The issue has been open for nearly two months, and the single comment suggests the community is waiting for a fix. This affects any team relying on Kimi Code CLI for batch or automated coding tasks on the moonshot.ai platform.  
- **Community reaction:** The issue has only one reaction (👍), indicating moderate interest but limited discussion.

### #2496 — [bug] resuming forked session results in corrupted output  
- **Author:** TheKevinWang  
- **Status:** Closed, last updated 2026-07-14 (created 2026-07-13)  
- **Comments:** 0 | 👍 0  
- **Link:** [Issue #2496](https://github.com/MoonshotAI/kimi-cli/issues/2496)  
- **Why it matters:** Describes a specific corruption when using `kimi -r` to resume a forked session. While closed without public comments, the bug likely has been addressed by one of the recent PRs (e.g., handling of reasoning content). Forked sessions are a core workflow for parallel exploration, so this fix is important for power users.  
- **Community reaction:** No comments or reactions—likely a narrow edge case that the developer reported and the team fixed quickly.

---

## Key PR Progress
*(All three PRs updated in the last 24h are listed; all were closed/merged.)*

### #2499 — fix(kosong): stop sending Kimi reasoning effort implicitly  
- **Author:** RealKai42  
- **Status:** Closed (merged) on 2026-07-14  
- **Comments:** 0 | 👍 0  
- **Link:** [PR #2499](https://github.com/MoonshotAI/kimi-cli/pull/2499)  
- **Description:** Configures Kimi thinking requests through `thinking.type` instead of automatically serializing the legacy `reasoning_effort` parameter. The change preserves the caller‑provided thinking effort exactly as independent provider state, without implicit clamping or reverse mapping.  
- **Why it matters:** Eliminates unintended behavior where the CLI would silently override or transform the reasoning effort, which could lead to unpredictable model responses. Developers using custom thinking configurations will see more predictable output.

### #2498 — fix(kosong): preserve empty-string reasoning_content as ThinkPart  
- **Author:** bigeagle  
- **Status:** Closed (merged) on 2026-07-14  
- **Comments:** 0 | 👍 0  
- **Link:** [PR #2498](https://github.com/MoonshotAI/kimi-cli/pull/2498)  
- **Description:** Fixes a 400 error from the model `coding-model-okapi-0711-vibe` that occurred when `thinking.keep=all` required `reasoning_content` on every assistant message but the sixth message had an empty string. The PR preserves empty‑string `reasoning_content` as a `ThinkPart` instead of stripping it.  
- **Why it matters:** Directly resolves a live session crash and closes the class of errors around reasoning content presence. Important for users experimenting with the “keep all thinking” feature.

### #2494 — fix(kimi): use remaining context for completion budget  
- **Author:** RealKai42  
- **Status:** Closed (merged) on 2026-07-14  
- **Comments:** 0 | 👍 0  
- **Link:** [PR #2494](https://github.com/MoonshotAI/kimi-cli/pull/2494)  
- **Description:** Changes the default Kimi completion budget from a fixed 32k provider cap to the remaining model context window. The dynamic limit applies only to Kimi requests (including Kimi wrapped by ChaosChatProvider), while generic ChatProvider, kosong.generate/step, and all non‑Kimi providers remain unaffected.  
- **Why it matters:** Prevents premature truncation of completions when the context window has spare capacity, and avoids wasting budget on short conversations. This should improve output quality for long‑running coding sessions without hitting arbitrary caps.

---

## Feature Request Trends
Based on the limited issue activity, no explicit feature requests appeared in the last 24h. However, the nature of the closed PRs and the open bug #2318 points to two recurring community desires:

1. **Better rate‑limit handling & transparency** – The long‑standing TPD bug (#2318) implies users want reliable, user‑friendly rate‑limit feedback (e.g., remaining quota display, backoff control, or automatic retries).  
2. **Robust session management for forks** – Despite #2496 being closed, the corruption bug highlights an underlying need for stable fork/restore semantics, especially when reasoning content or thinking modes are involved.

---

## Developer Pain Points
- **Rate‑limit unpredictability** – The TPD calculation bug (#2318) has been open for two months with minimal progress, causing frustration for teams that hit unexpected blocks during heavy usage.  
- **Session corruption on resume** – The fork‑resume issue (#2496) – though fixed – reflects a broader pain point: the CLI’s session serialisation must faithfully preserve all state, including complex reasoning content, to avoid silent data loss.  
- **Implicit parameter override** – The reasoning‑effort serialisation fix (#2499) addresses a pattern where the CLI silently modifies user‑supplied parameters, which erodes trust and can lead to hard‑to‑debug output differences.

---

*Generated from github.com/MoonshotAI/kimi-cli activity on 2026-07-15.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-15

## Today's Highlights
OpenCode v1.18.0 and v1.18.1 shipped, completing the Desktop v2 UI migration with a transitional layout toggle. The rollout has sparked heated community discussion: the new tab layout, missing Plan/Build mode selector, and agent picker are the top pain points, while a flurry of feature requests and PRs from contributor `ohsalmeron` address session management (archived browsing, inline rename, delete, fork, one-click compaction).

---

## Releases

- **v1.18.1** — Bugfix: Fixed spacing between model provider sections in Settings ([Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.18.1)).
- **v1.18.0** — Completed Desktop v2 migration, including upgrade handling for the new layout and first-launch onboarding. Added a setting to switch between new and old Desktop layouts during the transition period. Fixed file views using the wrong background ([Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.18.0)).

---

## Hot Issues (Top 10 by Community Activity)

1. **#28957 — [BUG] "Upstream idle timeout exceeded"**  
   Users hit session timeouts when using the `writing-plans` skill on macOS Tahoe / Apple M4. 20 comments, 2 👍. The root cause appears to be infrastructure-level idle disconnection.  
   [Issue #28957](https://github.com/anomalyco/opencode/issues/28957)

2. **#12472 — Native Claude Code hooks compatibility (PreToolUse, PostToolUse, Stop)**  
   Highly requested (37 👍) — OpenCode already supports Claude Code rules and skills, but lacks the hooks system. Community wants full parity for cross-editor workflows.  
   [Issue #12472](https://github.com/anomalyco/opencode/issues/12472)

3. **#25239 — Expose GitHub Copilot "Auto" option in model selector**  
   Users want the "Auto" model selection (as seen in VS Code Copilot) to automatically choose the best model per task. 14 👍, 16 comments.  
   [Issue #25239](https://github.com/anomalyco/opencode/issues/25239)

4. **#22129 — [CLOSED] Skills don't show up in TUI autocomplete but they do in the web app**  
   Root cause identified in `autocomplete.tsx:363`. Closed after fix, but highlights an ongoing gap between TUI and web feature parity.  
   [Issue #22129](https://github.com/anomalyco/opencode/issues/22129)

5. **#36936 — Desktop: wtf is the new tab layout, tab titles don't fit anymore**  
   Strong reaction to the new layout — horizontal tabs cut off session titles. Users reverted to v1.17 to work around this. 10 comments, 5 👍.  
   [Issue #36936](https://github.com/anomalyco/opencode/issues/36936)

6. **#32747 — @ file mentions do not include files created after startup**  
   TUI autocomplete for `@` doesn't pick up newly created files until restart. Stale search state bug, affecting developer workflow. 10 comments, 8 👍.  
   [Issue #32747](https://github.com/anomalyco/opencode/issues/32747)

7. **#31972 — New Layout prevents switching Plan/Build mode**  
   After enabling the new layout, both the UI toggle and Ctrl+. shortcut stop working. Affects Windows 10, reported by multiple users. 8 comments, 8 👍.  
   [Issue #31972](https://github.com/anomalyco/opencode/issues/31972)

8. **#36986 — [FEATURE] Why remove the task sidebar? Bring back sidebar**  
   A user (translated from Chinese) asks for the sidebar task view instead of a dedicated page, calling the new design "unnecessary".  
   [Issue #36986](https://github.com/anomalyco/opencode/issues/36986)

9. **#36979 — Agents not visible when switching with Ctrl+. + folders not expanding (Desktop v1.18.1, Windows)**  
   Two separate regressions in the v2 UI: agent picker missing and central file explorer folders not expanding.  
   [Issue #36979](https://github.com/anomalyco/opencode/issues/36979)

10. **#36971 — Session history not loading on home page using a VPS as server (new layout)**  
    After the July 15 update, home page fails to render past session list. Remote server setups are broken.  
    [Issue #36971](https://github.com/anomalyco/opencode/issues/36971)

---

## Key PR Progress (Top 10 by Activity)

1. **#36894 — fix(core): expand reasoning option variants**  
   Adds conditional toggle variants (`none`/`thinking`, `none`/`high`/`max`) for model reasoning efforts, with budget clamping across providers.  
   [PR #36894](https://github.com/anomalyco/opencode/pull/36894)

2. **#36978 — perf(codemode): batch OpenAPI query parameters**  
   Serializes query parameters into ordered tuples and appends in one batch, avoiding quadratic rebuilds for exploded arrays/objects.  
   [PR #36978](https://github.com/anomalyco/opencode/pull/36978) *(closed)*

3. **#36691 — refactor(llm): replace LLMError reasons with flat tagged union**  
   `LLMError` becomes a flat tagged union (e.g., `RateLimit | QuotaExceeded | ServerError`), simplifying error handling across the codebase.  
   [PR #36691](https://github.com/anomalyco/opencode/pull/36691)

4. **#36542 — fix(core): tolerate AlreadyExists in FSUtil.ensureDir**  
   Fixes a crash introduced in v1.17.15 when `ensureDir` races with parallel config resolution. Closes #35828.  
   [PR #36542](https://github.com/anomalyco/opencode/pull/36542)

5. **#36968 — feat(app): add archived sessions browser dialog**  
   Introduces `/archived` slash command with a dialog showing all archived sessions sorted by date, addressing a common discoverability gap.  
   [PR #36968](https://github.com/anomalyco/opencode/pull/36968)

6. **#36967 — feat(app): delete session with confirmation dialog**  
   Adds right-click "Delete Session" in sidebar with confirmation, leveraging existing `session.delete` API endpoint.  
   [PR #36967](https://github.com/anomalyco/opencode/pull/36967)

7. **#36966 — feat(app): inline session rename in sidebar**  
   Double-click session title in sidebar to edit inline, reusing the `InlineEditor` component from workspace rename UX.  
   [PR #36966](https://github.com/anomalyco/opencode/pull/36966)

8. **#36965 — feat(app): add fork button to assistant response texts**  
   One-click fork from any assistant message, creating a new session branched from that point.  
   [PR #36965](https://github.com/anomalyco/opencode/pull/36965)

9. **#36964 — feat(app): add one-click context compaction button**  
   A compact icon next to the context usage indicator triggers `/compact` without needing the command palette.  
   [PR #36964](https://github.com/anomalyco/opencode/pull/36964)

10. **#36752 — fix(opencode): read cache write tokens from raw usage**  
    Fixes `cache.write: 0` reporting for Anthropic models via OpenAI-compatible gateways, ensuring correct billing.  
    [PR #36752](https://github.com/anomalyco/opencode/pull/36752)

---

## Feature Request Trends

The community is overwhelmingly focused on **Desktop v2 UI refinements**. The most requested directions are:

- **Restore missing UI elements**: Plan/Build mode toggle, agent picker, sidebar sessions list, and the ability to switch between vertical/horizontal tab layouts.
- **Session management improvements**: Inline rename, delete with confirmation, archived session browser, fork from any response, and a one-click context compaction button.
- **TUI parity**: Skills autocomplete in the TUI, `@` file mentions for new files, and `--no-color` flag for `opencode run`.
- **Model and provider enhancements**: Expose GitHub Copilot's "Auto" model selector, add Claude Code hooks compatibility, support for xAI Grok OAuth in v2, and expanded reasoning effort options.
- **Plugin UX**: Show friendly names for local plugins instead of raw `file://` paths in the status popover.

---

## Developer Pain Points

1. **Desktop v2 migration regressions** — The new layout (shipped in v1.18.0) broke core workflows: Plan/Build switching, agent selection, session history loading, and tab title visibility. Multiple issues with high 👍 and comments signal broad frustration.

2. **TUI autocomplete gaps** — Skills and newly created files are missing from `@` autocomplete until restart. This breaks the "start a file, then reference it" flow in terminal-based work.

3. **Context window management is hidden** — Users must remember the `/compact` command instead of having a visual button; the new one-click compaction PR (#36964) directly addresses this.

4. **Session history discoverability** — No persistent sidebar and Ctrl+S conflict with editor save shortcuts make it hard to find past conversations, especially for new users.

5. **Infrastructure resilience** — The "upstream idle timeout" (#28957) and "notification server not found" errors (#36977) after plugin installation highlight stability concerns under non-standard setups (VPS, WSL).

6. **Provider-specific issues** — xAI Grok OAuth missing in v2, Gemini tool call argument parsing bugs, and cache write token misreporting for OpenAI-compatible gateways show the complexity of multi-provider support.

---

*Generated from GitHub data for anomalyco/opencode (2026-07-15). For the full list of issues and PRs, visit the [repository](https://github.com/anomalyco/opencode).*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-07-15

## Today's Highlights
The day’s action centers on **v0.80.7** with a breaking change to session-affinity configuration, plus a flurry of activity around **OpenAI Codex compatibility** (clamped headers, originator spoofing for gpt-5.6-luna) and **OAuth integration** for xAI’s Grok subscription. A new **Amazon Bedrock Mantle** provider proposal continues to gain traction, while regression fixes for timeouts and npm script execution are being merged quickly.

## Releases
- **[v0.80.7](https://github.com/earendil-works/pi/releases/tag/v0.80.7)** – Breaking change: `openai-responses` `compat.sendSessionIdHeader` flag removed; replaced by `compat.sessionAffinityFormat` (`"openai"`, `"openai-nosession"`, `"openrouter"`). Migrate existing configurations accordingly.

## Hot Issues (10)

1. **[#5363 – Add amazon-bedrock-mantle provider](https://github.com/earendil-works/pi/issues/5363)** – 16 comments, 👍8. Requests a new provider for Bedrock Mantle models using OpenAI-compatible API (not Converse). High community interest; a PR is already open (#6216).

2. **[#6476 – Regression: httpIdleTimeoutMs ignored for self-hosted OpenAI providers](https://github.com/earendil-works/pi/issues/6476)** – 10 comments. Timeouts breaking vLLM/local setups after v0.80.6; downgraded to v0.80.3 works. Critical for local inference users.

3. **[#6522 – openai-completions: no floor on max_completion_tokens → 400](https://github.com/earendil-works/pi/issues/6522)** – 7 comments. Missing minimum validation causes proxy rejects; users forced to disable auto-compact, risking context overflow.

4. **[#6509 – Extension-reported usage in footer cost display](https://github.com/earendil-works/pi/issues/6509)** – 5 comments. Proposes `ctx.ui.setUsage` so extensions (e.g., subagents) can report external LLM costs. In progress.

5. **[#6624 – Add GPT-5.6 models (luna/terra/sol) to GitHub Copilot provider](https://github.com/earendil-works/pi/issues/6624)** – 5 comments. These models exist in Copilot CLI but are missing from Pi’s catalog; closed as no-action because a catalog refresh PR (#6636) landed.

6. **[#3200 – Support video/audio in `prompt` command](https://github.com/earendil-works/pi/issues/3200)** – 5 comments, 👍3. Wanted for multimodal models (Gemma 4, GPT-4o). Still open; long-standing request.

7. **[#6461 – Add xAI Grok SuperGrok OAuth login](https://github.com/earendil-works/pi/issues/6461)** – 4 comments. Desires a `xai-oauth` provider for device-code login, similar to Claude/Codex/Copilot. Two PRs already submitted (#6651, #6656).

8. **[#6374 – Model catalog reasoning-level metadata conflicts](https://github.com/earendil-works/pi/issues/6374)** – 3 comments, 👍1. Incorrect reasoning levels across providers break deduplication. In progress.

9. **[#6167 – `transformMessages` + `isSameModel` thinking block normalization bug](https://github.com/earendil-works/pi/issues/6167)** – 3 comments. Redacted thinking blocks inlined incorrectly when switching models, causing compatibility flag issues.

10. **[#6600 – `pi update --extensions` blocked by npm 11.16.0 default script restrictions](https://github.com/earendil-works/pi/issues/6600)** – 3 comments. New npm policy breaks extension updates; needs documentation or workaround.

## Key PR Progress (10)

1. **[#6659 – fix(openai-codex): clamp session-id header to 64 chars](https://github.com/earendil-works/pi/pull/6659)** – Closed. Fixes #6630; merged quickly. Ensures headers match clamped `prompt_cache_key` to avoid backend rejections.

2. **[#6656 – feat(ai): add xAI subscription OAuth](https://github.com/earendil-works/pi/pull/6656)** – Closed. Adds OAuth support (no tools yet) for Grok subscription; addresses #6626.

3. **[#6654 – feat(ai): add promptCacheKey stream option](https://github.com/earendil-works/pi/pull/6654)** – Open. Opt-in override of `prompt_cache_key` for OpenAI providers; reduces cache invalidation.

4. **[#6651 – feat(ai): add xAI device OAuth and route grok-4.5 through Responses](https://github.com/earendil-works/pi/pull/6651)** – Closed. Closes #6461; adds low/medium/high reasoning for grok-4.5 via Responses API.

5. **[#6645 – fix: don't send session-id header to opencode openai-responses models](https://github.com/earendil-works/pi/pull/6645)** – Closed. Fixes #6625; removes problematic header for models that don’t need it.

6. **[#6594 – feat: sqlite session storage (open)](https://github.com/earendil-works/pi/pull/6594)** – Open. Adds `retainedTail` to compaction; changes `getPathToRoot` to stop at last compaction. Significant performance improvement for large sessions.

7. **[#6216 – feat: Add Amazon Bedrock Mantle OpenAI Responses provider (open)](https://github.com/earendil-works/pi/pull/6216)** – Open. Uses OpenAI’s Bedrock provider; supersedes earlier attempt. High community demand.

8. **[#6584 – fix: forward provider options to summary requests](https://github.com/earendil-works/pi/pull/6584)** – Closed. Closes #6555; ensures compaction/summary calls inherit transport settings from parent session.

9. **[#6635 – fix(ai): recover openai-completions tool calls emitted in content](https://github.com/earendil-works/pi/pull/6635)** – Closed. Parses tool-call JSON from assistant `content` when structured `tool_calls` is missing; fixes local inference servers (Ollama, LM Studio).

10. **[#6636 – feat(ai): refresh generated model catalogs](https://github.com/earendil-works/pi/pull/6636)** – Closed. Adds GPT-5.6 models to GitHub Copilot; refreshes all provider catalogs from latest upstream data.

## Feature Request Trends
The strongest themes are:
- **New provider integrations** – Amazon Bedrock Mantle (#5363) and xAI OAuth (#6461) are the most‑requested; both have active PRs.
- **Model catalog completeness** – Users consistently want the latest model IDs (GPT‑5.6 series, Grok 4.5) added immediately.
- **Multimodal support** – Video/audio in the `prompt` command (#3200) remains open with steady demand.
- **Extension API expansion** – `ctx.ui.setUsage` (#6509) and `message_end` hooks (PR #6633) indicate a push for richer extension capabilities.
- **Cache/compaction control** – Options to override prompt cache keys (#6654) and avoid cache writes for compaction (#6618) show growing attention to provider costs.

## Developer Pain Points
- **Regression bugs** – The `httpIdleTimeoutMs` regression (#6476) and npm script blocking (#6600) cause immediate frustration for local/self‑hosted users.
- **API compatibility edge cases** – Missing floor on `max_completion_tokens` (#6522), thinking block normalization (#6167), and MiniMax M3 thinking format (#6658) highlight fragile interoperability with non‑OpenAI providers.
- **Hardcoded paths and headers** – Crash log hardcoding `~/.pi/` (#6652) and originator spoofing needed for gpt‑5.6‑luna (#6601) waste debugging time.
- **Compaction inefficiency** – Fixed image size estimates (#6603) and proactive compaction blocking user input (#6606) degrade UX for heavy sessions.
- **Subagent/timeout management** – Subagent silence killing long dispatches (#6655) and session‑id length limits (#6630) reveal gaps in the agent harness.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-15

## Today’s Highlights
v0.19.10 landed with multi-workspace support now spanning ACP transport, daemon workers, split-view sessions, and workspace-aware actions, cementing the architecture for shared daemon use across projects. The long-running comprehensive hot-reload system (#3696) was officially closed after delivering runtime reload for skills, extensions, MCP, LSP, and configuration. Meanwhile, a dense wave of MCP security hardening, UI rendering fixes, and CI reliability improvements kept the PR queue busy, with most changes shipping as patch-level or nightly releases.

## Releases
- **v0.19.10-nightly.20260715.c538bd70d** — Nightly release containing docs improvements (PR scope capping) and workspace path lock for web-shell.  
  [View Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.10-nightly.20260715.c538bd70d)

- **v0.19.9-preview.0** — Preview release with the same doc and web-shell changes as the nightly above.  
  [View Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.9-preview.0)

- **v0.19.10** — Stable release. **Highlights:** Multi-workspace support now works across ACP transport, daemon workers, split-view sessions, and workspace-aware actions (PRs #6621, #6635, #6746).  
  [View Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.10)

- **sdk-typescript-v0.1.8** — TypeScript SDK bundled with CLI v0.19.10 (stable).  
  [View Release](https://github.com/QwenLM/qwen-code/releases/tag/sdk-typescript-v0.1.8)

## Hot Issues (Top 10)

1. [#6378 – RFC: Support multiple workspaces in one qwen serve daemon](https://github.com/QwenLM/qwen-code/issues/6378)  
   *Priority: P2 | 23 comments*  
   A key RFC proposing that a single `qwen serve` daemon manage multiple workspaces, preserving backward compatibility for existing clients. This would unify daemon resource usage across projects without breaking current workflows. Community interest is growing, though design consensus is still being sought.

2. [#3696 – feat: comprehensive hot-reload system for skills, extensions, MCP, and configuration](https://github.com/QwenLM/qwen-code/issues/3696)  
   *Priority: P1 | 7 comments*  
   **Closed.** The complete runtime hot-reload system for skills, extensions, MCP servers, LSP servers, and configuration is now merged. This eliminates the need for session restarts and is a major quality-of-life gain for developers.

3. [#4748 – Optimize daemon cold start and qwen serve fast-path latency](https://github.com/QwenLM/qwen-code/issues/4748)  
   *Priority: P2 | 5 comments*  
   Original benchmarks showed a large cold-start gap (2.5s vs 0.7s) between daemon boot and CLI initialization. Significant optimizations have been applied; this issue now tracks remaining latency work.

4. [#5979 – Bug: /auth model config changes do not apply to new sessions (401 error)](https://github.com/QwenLM/qwen-code/issues/5979)  
   *Priority: P2 | 5 comments*  
   **Closed.** After modifying a model provider API key via `/auth`, new sessions still reported 401 errors. The fix ensures that configuration changes made via `/auth` are correctly propagated to newly created sessions.

5. [#5219 – CI: integration tests don't run on PR/merge, regressions surface only at release time](https://github.com/QwenLM/qwen-code/issues/5219)  
   *Priority: P2 | 5 comments*  
   **Closed.** E2E integration tests only ran on nightly cron jobs, not on PRs or merges to main. The team added PR-run integration tests to catch regressions earlier in the development cycle.

6. [#6809 – Bug: Ctrl+S diff preview garbled for multi-line edits in permission dialog](https://github.com/QwenLM/qwen-code/issues/6809)  
   *Priority: P2 | 4 comments*  
   Lines in the diff preview are incorrectly concatenated (e.g., `};timeout: 30000`). The rendering logic fails to handle multi-line span boundaries, breaking the permission review UX.

7. [#6149 – VP mode breaks link interaction; non-VP mode cannot scroll when content overflows](https://github.com/QwenLM/qwen-code/issues/6149)  
   *Priority: P2 | 4 comments*  
   Two related TUI rendering bugs: in VP mode, OSC 8 hyperlinks cannot be selected; in non-VP mode, overflow content is unscrollable. Both degrade interactive terminal experience.

8. [#5239 – Weak subagent/main-session communication; need two-way notification](https://github.com/QwenLM/qwen-code/issues/5239)  
   *Priority: P2 | 4 comments*  
   Subagents that fail silently leave the main session unaware. The reporter resorted to file-based monitoring. The community is calling for a proper notification/bidirectional communication mechanism between subagents and the main session.

9. [#6914 – Fractional session and per-turn tool-call limits terminate runs prematurely](https://github.com/QwenLM/qwen-code/issues/6914)  
   *Priority: P2 | 3 comments*  
   Fractional values like `0.5` pass validation but cause premature termination on the first turn. The core config boundary does not enforce integer-only values, leading to confusing behavior.

10. [#6487 – Memory index stale after /remember; memory content lost on compaction](https://github.com/QwenLM/qwen-code/issues/6487)  
    *Priority: P2 | 3 comments*  
    Over long sessions, `MEMORY.md` is correctly written to disk after `/remember`, but the in-session system instruction does not update. Compaction can also silently drop memory content. This undermines the reliability of long-running agent memory.

## Key PR Progress (Top 10)

1. [#6891 – feat(channels): support DingTalk webhook delivery to direct messages](https://github.com/QwenLM/qwen-code/pull/6891)  
   Extends daemon-triggered DingTalk webhooks to deliver Markdown responses to both direct messages (one-to-one robot API) and group chats, reusing existing token caching and error handling.

2. [#6846 – feat(core): add PDF vision bridge fallback](https://github.com/QwenLM/qwen-code/pull/6846)  
   Adds a text-first visual fallback for PDFs when the primary model is text-only. Falls back to rendering only on extraction failure or oversized single-page results, with transcript limits.

3. [#6900 – fix(cli): don't mutate cached trusted-folders config on preview trust check](https://github.com/QwenLM/qwen-code/pull/6900)  
   Fixes #6831 where a read-only trust-status preview mutation persisted stale config to disk. The fix uses a deep clone before applying the override.

4. [#6854 – fix(core): sanitize standalone closing thinking tags](https://github.com/QwenLM/qwen-code/pull/6854)  
   Handles model protocol errors where a standalone `</think>` or `</thinking>` tag appears after structured reasoning. Qwen Code now suppresses the orphaned tag instead of discarding the entire turn.

5. [#6920 – fix(config): reject fractional session and tool-call limits](https://github.com/QwenLM/qwen-code/pull/6920)  
   Enforces integer-only values for `model.maxSessionTurns` and `model.maxToolCallsPerTurn` in config validation, preventing premature termination. Resumed agents also revalidate persisted values.

6. [#6887 – fix(cli): apply FETCH_TIMEOUT_MS to /update version check and log fetchInfo results](https://github.com/QwenLM/qwen-code/pull/6887)  
   Wires the existing 2000ms timeout constant into the `/update` version check, ensuring blocked network callers don't hang indefinitely.

7. [#6926 – fix(mcp): terminate descendants after discovery timeout](https://github.com/QwenLM/qwen-code/pull/6926)  
   When non-pooled MCP discovery times out for a stdio server, now terminates child processes below the transport wrapper before disconnecting, preventing zombie processes.

8. [#6924 – fix(mcp): require trust for read-only auto-approval](https://github.com/QwenLM/qwen-code/pull/6924)  
   Closes a security gap: `readOnlyHint` from an untrusted MCP server no longer grants default `allow` permission. Explicit trust is required for read-only auto-approval.

9. [#6847 – fix(cli): wrap long compact tool summaries](https://github.com/QwenLM/qwen-code/pull/6847)  
   **Closed.** Long tool summary text now wraps within available terminal width instead of being truncated with `…`, improving readability of file paths and command outputs.

10. [#6902 – fix(vscode-companion): don't let a non-boundary @ suppress / completion](https://github.com/QwenLM/qwen-code/pull/6902)  
    **Closed.** A stray `@` (e.g., in an email address) no longer suppresses slash-command completions in the VS Code chat input. Extracted trigger logic into a pure function with unit tests.

## Feature Request Trends

- **Multi-Workspace & Daemon Sessions** – Growing demand for multiple workspaces in a single `qwen serve` daemon (#6378, #6621, #6635, #6746). Users want to manage multiple projects without spawning separate daemon processes, reducing resource overhead and simplifying collaboration.

- **Unified Hot-Reload & Live Configuration** – The closure of #3696 marks a milestone, but follow-up requests for more granular runtime reload (e.g., per-extension, selective MCP server restart) continue to surface.

- **Subagent & Multi-Agent Communication** – Feature requests (#5239, #4753) ask for bidirectional notification between subagents and the main session, plus better subagent lifecycle monitoring. This is becoming a blocker for complex agent workflows.

- **Desktop & UI Modernization** – A new community proposal (#6896) outlines directions for Qwen Code Desktop: unified right-sidebar for Review, Terminal, Browser, File Explorer, and an in-app browser for live preview. This signals a shift toward a richer IDE-like experience.

- **MCP & Tool Integration Improvements** – Requests for exposed tool-call preparation events (#6775), liveness heartbeats for silent shell commands (#6901), and trust-aware permission flows (#6917) indicate a maturing focus on secure, observable, and extensible tool integrations.

- **Long-Session Reliability** – Memory management (#2128, #6487) and per-turn limit validation (#6914) are recurrent themes. Users want predictable, leak-free behavior over sessions lasting hours or days.

## Developer Pain Points

1. **Trust Config Mutation on Preview Check** – A read-only trust-status preview silently mutates and persists config (#6831). Developers must be careful to deep-clone before overriding, or risk leaking unconfirmed trust states to subsequent saves.

2. **Daemon Channel Worker Debugging** – When a daemon-managed channel fails during startup, the actual adapter error is written to stderr but lost at the worker/supervisor boundary, leaving only a generic exit code (#6909). This makes debugging channel failures unnecessarily difficult.

3. **`/update` Version Check Blindness** – The `/update` command on v0.19.9 reports "up to date" even when v0.19.10 is available, because the fetch timeout was never wired to the underlying `update-notifier` call (#6857). Users face phantom "up to date" messages for one full version cycle.

4. **Long-Session Memory Degradation** – Memory index becomes stale after `/remember` and content can be lost during compaction (#6487). For developers running extended agent sessions, this undermines the core short-term memory feature.

5. **Ctrl+C & Input Interference** – In PyCharm terminals, a single `Ctrl+C` can accidentally exit the CLI agent instead of interrupting output, while `Escape` may switch focus to the editor instead of stopping the current conversation (#4586). Users familiar with other CLIs find this behavior surprising and disruptive.

6. **Fractional Limits Passing Validation** – Settings like `model.maxSessionTurns: 0.5` are accepted but cause premature termination on the first turn (#6914). This validation gap can silently break long-running workflows.

7. **Missing Liveness Signals for Silent Commands** – Foreground shell commands that produce no output for extended periods leave the user uncertain whether the agent is still working or has hung (#6901). A liveness heartbeat feature has been requested but not yet shipped.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-15

*Based on data from github.com/Hmbown/CodeWhale (DeepSeek TUI project)*

## Today's Highlights

The project is wrapping up v0.8.68 with a major underwater TUI visual overhaul, finalised receipt settling and mouse interactions, and cross-platform fixes (BSD, Android). A high‑activity bug (#4032, 35 comments) about “Codewhale not following the constitution” remains open, while a new I18N issue (#4369) highlights unnatural Chinese translations that may affect non‑English users. Several Dependabot bumps and a new MiniMax provider PR landed.

## Releases

No new releases in the last 24 hours. The v0.8.68 release candidate (PR #4361) is being prepared.

## Hot Issues (10 noteworthy)

1. **[#4032 – Codewhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032) [OPEN]**
   The AI agent writes temporary scripts instead of using user‑provided ones, despite explicit rules. 35 comments – clearly a core UX trust issue.

2. **[#4369 – [I18N] Unnatural Chinese translation for "Constitution" / "Code"](https://github.com/Hmbown/CodeWhale/issues/4369) [OPEN]**
   The setup wizard uses “宪法” (constitution) for user‑defined rules – culturally awkward. Community feedback suggests clearer terms like “规则” or “准则”.

3. **[#4365 – `@` file watcher scans entire directory tree eagerly, causing terminal lag](https://github.com/Hmbown/CodeWhale/issues/4365) [OPEN]**
   When mentioning a non‑workspace path, the TUI freezes on large directories. PR #4367 already implements a wall‑clock budget fix.

4. **[#4368 – Override kimi baseUrl leads to context limit warming](https://github.com/Hmbown/CodeWhale/issues/4368) [OPEN]**
   Configuring a custom base URL for Kimi (moonshot) provider triggers “exseed context limit”. Needs investigation of routing logic.

5. **[#4270 – Streaming text display too slow (流式文本显示太慢了)](https://github.com/Hmbown/CodeWhale/issues/4270) [CLOSED]**
   TUI typing speed lags behind model output (especially DeepSeek V‑flash), then bursts text. Reported previously but now more pronounced. Closed – likely addressed upstream.

6. **[#4208 – TUI copy‑paste polluted with box‑drawing Unicode](https://github.com/Hmbown/CodeWhale/issues/4208) [CLOSED]**
   Selecting text copies Unicode decorations (╎▎●│). Breaks pasting into terminals. Fix merged.

7. **[#3765 – Expose SeamManager.enabled and CompactionConfig.enabled to config.toml](https://github.com/Hmbown/CodeWhale/issues/3765) [CLOSED]**
   Hardcoded true values prevent disabling context compaction. Now configurable via `[compaction].enabled` and `[seam_manager].enabled`.

8. **[#4318 – Pricing: cache‑write rates dropped by CurrencyPricing/TokenUsage](https://github.com/Hmbown/CodeWhale/issues/4318) [CLOSED]**
   Anthropic cache‑write costs (1.25×–2× input) were hardcoded to zero. Critical for cost‑sensitive users.

9. **[#4335 – Make offline scorecard pricing provider‑aware](https://github.com/Hmbown/CodeWhale/issues/4335) [CLOSED]**
   Scorecard used model‑only pricing, ignoring provider (e.g., OAuth routes). Now fails closed on unknown routes.

10. **[#4345 – Key bindings not user‑friendly (key 太不友好了)](https://github.com/Hmbown/CodeWhale/issues/4345) [CLOSED]**
    User complained about unintuitive keyboard shortcuts. Closed with no resolution – may be reopened.

## Key PR Progress (10 important)

1. **[#4361 – Prepare CodeWhale v0.8.68 release candidate](https://github.com/Hmbown/CodeWhale/pull/4361) [CLOSED]**
   One‑branch RC finishing underwater TUI, mouse/keyboard parity, reduced‑motion semantics.

2. **[#4367 – Fix `@`‑completion file‑index walk with wall‑clock budget](https://github.com/Hmbown/CodeWhale/pull/4367) [OPEN]**
   Direct fix for #4365 – bounds directory scanning to prevent TUI freezes.

3. **[#4354 – Add MiniMax Messages provider support](https://github.com/Hmbown/CodeWhale/pull/4354) [CLOSED]**
   New provider: MiniMax‑M3 and M2.7 models with verified context, thinking, pricing.

4. **[#4351 – Fix scorecard: bind costs to provider routes](https://github.com/Hmbown/CodeWhale/pull/4351) [CLOSED]**
   Offline scorecard now handles OAuth, local, unpriced routes – essential for accurate API billing.

5. **[#4360 – Fix browser open on BSD systems](https://github.com/Hmbown/CodeWhale/pull/4360) [CLOSED]**
   NetBSD, FreeBSD, OpenBSD, DragonFly now supported for link clicking in TUI.

6. **[#3780 – Expose context compaction gates](https://github.com/Hmbown/CodeWhale/pull/3780) [CLOSED]**
   Closes #3765 – adds `[compaction].enabled` and `[seam_manager].enabled` to `config.toml`.

7. **[#4362 – Make Codewhale public site documentation‑led](https://github.com/Hmbown/CodeWhale/pull/4362) [CLOSED]**
   Homepage redesigned as a compact documentation portal with repository‑derived install guides.

8. **[#4366 – Fix web: align site brand strings and tidy redesign leftovers](https://github.com/Hmbown/CodeWhale/pull/4366) [CLOSED]**
   Follow‑up to #4362: consistent “Codewhale” wordmark across pages.

9. **[#4364 – Add keyword search to docs hub and FAQ pages](https://github.com/Hmbown/CodeWhale/pull/4364) [CLOSED]**
   Client‑side search with / keyboard shortcut, bilingual (EN/ZH).

10. **[#4355 – Persist stateful terminal identity and restart limitations safely](https://github.com/Hmbown/CodeWhale/pull/4355) [CLOSED]**
    Ensures a restarted client does not mistake stale PID for a live shell – part of v0.8.68.

## Feature Request Trends

- **Provider extensibility**: Two recent PRs add new provider ports (MiniMax, Kimi base URL override). Community wants easy self‑serve provider configuration.
- **I18N polish**: Multiple Chinese‑language issues surface translation quality – especially legal/ethical terms (“Constitution” vs “rules”).
- **Underwater/ambient TUI**: v0.8.68 series shows strong demand for aesthetic, calming terminal experiences with motion‑reduction controls.
- **Configurability**: Users want to toggle compaction, seams, and pricing behaviour via config.toml rather than hardcoded defaults.
- **Offline/replay support**: Exec stream receipts (#4356) and scorecard routing (#4351) point toward deeper debugging and cost attribution.

## Developer Pain Points

- **Streaming rendering performance**: Terminal text output cannot keep up with fast models (e.g., DeepSeek V‑flash), causing visual stutter and burst text. Still an open concern.
- **File watcher freeze**: `@`‑mentioning a large directory causes complete TUI unresponsiveness – critical for users with deep project trees.
- **Clipboard pollution**: Unicode decorations in copied text remain a frustration, though a fix is in.
- **Platform gaps**: Android (Termux) build fails due to missing rquickjs bindings; BSD link‑opening now fixed, but other quirks remain.
- **Key binding discoverability**: Non‑English speakers find default shortcuts unintuitive (issue #4345). No resolution yet.
- **I18N consistency**: The Codewhale constitution feature is mistranslated as “宪法” (constitution) – ambiguous and culturally jarring for Chinese users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*