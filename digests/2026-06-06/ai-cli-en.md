# AI CLI Tools Community Digest 2026-06-06

> Generated: 2026-06-06 02:31 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-06-06  
**Scope:** Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI (CodeWhale)

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem on June 6, 2026 exhibits a clear bifurcation between **platform-backed tools** (Claude Code, Codex, Gemini CLI, Copilot CLI) focused on reliability and enterprise readiness, and **community-driven tools** (OpenCode, Pi, CodeWhale) pushing rapid feature innovation. The Kimi Code CLI is in an explicit deprecation/transition phase to its successor `kimi-code`, while Qwen Code and Pi (mono) are aggressively expanding their HTTP API surfaces for IDE integration. A dominant cross-cutting theme this week is **multi-agent orchestration infrastructure**: every tool is grappling with sub-agent lifecycle management, context compaction, and inter-session coordination, suggesting the industry is converging on agent systems as the next major capability frontier. Windows and WSL2 performance remains a persistent pain point across nearly all tools.

---

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Updated (24h) | Release Status | Notable Activity |
|------|---------------------|-------------------|----------------|------------------|
| **Claude Code** | ~10 hot + several new | 4 (all community) | 3 minor releases (v2.1.165–167) | Heavy community engagement on multi-account (#27302, 261 👍) |
| **OpenAI Codex** | 10+ active | 10 merged/active | rusty-v8 v149.2.0, alpha CLI | Strong PR pipeline: MCP, sub-agent, plugin sharing |
| **Gemini CLI** | 10 selected | 10 selected | 2 patches + nightly | Major model update PR (#27705) for Gemini 3.1/3.5 Flash |
| **GitHub Copilot CLI** | 10 active | 0 PRs | v1.0.60 shipped yesterday | Critical WSL2 regression (#3700) and Windows ARM64 crash (#3687) |
| **Kimi Code CLI** | 2 | 6 (4 merged) | v1.47.0 | Final naming polish; transition to new repo |
| **OpenCode** | 10+ active | 10 merged/active | v1.16.0 + v1.16.2 | Heavy feature work: skills toggle, non-interactive MCP, inline skills |
| **Pi (mono)** | 10 selected | 10 selected (mostly merged) | No new release | Self-evolver framework (#5442), workflow extension (#5426) |
| **Qwen Code** | 10 selected | 10 (various stages) | v0.17.1-nightly | Daemon mode merge (#4490, +115k LOC); HTTP API expansion |
| **DeepSeek TUI (CodeWhale)** | 10 selected | 10 (7 merged) | Latest stable v0.8.53 | VS Code extension scaffold (#2811); WhaleFlow multi-agent (#2482) |

**Key observations:**
- **Codex** and **OpenCode** lead in PR throughput (10 each), suggesting active internal development
- **Claude Code** has the most engaged community but relatively few internal PRs visible
- **Gemini CLI** has unusual mixed activity: high-value PRs (model support, ephemeral mode) alongside ongoing pain points
- **Copilot CLI** and **Kimi** show minimal PR activity, indicating team focus elsewhere or consolidation

---

## 3. Shared Feature Directions

### 3.1 MCP Lifecycle Management (Codex, Copilot CLI, OpenCode, Claude Code, CodeWhale)
- **Problem:** MCP servers spawned per-session rather than per-project, leading to resource waste, zombie processes, and memory exhaustion
- **Codex #20883:** Requesting process pooling; **Copilot CLI #3701:** Runaway spawning on Windows; **OpenCode #31054:** Non-interactive MCP add (solved); **Claude Code:** Glob patterns in deny rules; **CodeWhale #2709:** Hugging Face MCP integration
- **Shared need:** Persistent, scoped, and configurable MCP server pools

### 3.2 Sub-Agent Visibility & Lifecycle (Claude Code, Codex, OpenCode, Gemini CLI, Copilot CLI)
- **Claude Code #64651:** Background agent output polluting foreground; **Codex #19197:** Orphaned sub-agents; **OpenCode #22233:** Cannot see running sub-agents; **Gemini #22323:** False success on turn limit; **Copilot CLI #3547:** Background sub-agent hangs
- **Shared need:** Runtime visibility into sub-agent state, clean termination, and parent-child observation

### 3.3 OAuth / Credential Stability (Claude Code, Gemini CLI, Copilot CLI)
- **Claude Code #61912:** OAuth refresh corrupts on transient 5xx; **Gemini #27033:** Tier not reflected in CLI; **Copilot CLI #2101:** Transient API errors → rate limit
- **Shared need:** Robust retry logic, credential recovery without manual intervention, consistent auth state across sessions

### 3.4 Windows / WSL2 Stability (Codex, Copilot CLI, OpenCode, Kimi, Qwen)
- **Codex #25715:** WSL performance (29 👍); **Copilot CLI #3700:** 215% CPU on WSL; **OpenCode #20234:** WSL thinking output one word/line; **Kimi #2435:** WebSocket infinite reload (Windows); **Qwen #4815:** OOM on resume (platform-agnostic but severe)
- **Shared need:** First-class Windows support is still not achieved; sandbox and terminal handling are fragile

### 3.5 Doom Loop / Infinite Tool-Call Detection (OpenCode, Gemini CLI, Claude Code)
- **OpenCode #12716:** Loops undetected during reasoning; **Gemini #22323:** False GOAL success; **Claude Code #63875:** Tool-call parsing crashes (non-deterministic)
- **Shared need:** Robust detection of agent loops, recovery mechanisms, and cross-message pattern analysis

### 3.6 Session Persistence & Portability (Claude Code, Codex, Copilot CLI, CodeWhale)
- **Claude Code #22648:** Settings sync across devices; **Codex:** No explicit issue but compaction problems; **Copilot CLI #3689:** Resume fails on case-sensitive repo name; **CodeWhale #2639:** POST /sessions endpoint for cross-workspace resume
- **Shared need:** Reliable session save/restore across machines, proper portable identifiers

### 3.7 Model Flexibility & Configuration (Gemini CLI, Copilot CLI, Qwen, CodeWhale)
- **Gemini #27705:** Model promotion to GA; **Copilot CLI #2920:** Quick model switching; **Qwen #4814:** Custom provider model wizard; **CodeWhale #2574:** Provider fallback chain
- **Shared need:** Declarative model selection, provider priority chains, and UI for model discovery

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | CodeWhale |
|-----------|-------------|-------|------------|-------------|----------|-----|-----------|
| **Primary Backing** | Anthropic | OpenAI | Google | GitHub/Microsoft | Community | Community | Community |
| **Core Differentiator** | Connector ecosystem, deny rules, Cowork | Plugin sharing, MCP negotiation | Vertex AI integration, AST tooling | GitHub ecosystem, permissions profiles | Dynamic workflows, skill system | Self-evolver, 5D memory, extension API | Cross-platform, multi-provider, HarmonyOS |
| **Target User** | Enterprise teams, multi-account devs | General devs, Windows users | Google Cloud / Vertex users | GitHub-centric developers | Power users, workflow automation | Extension developers, agent researchers | Chinese market, multi-model users |
| **Release Cadence** | Multiple minor releases daily | ~Weekly patches + alpha | Nightly + preview channels | ~Weekly | ~Bi-weekly | No releases this week | Nightly (Qwen), weekly (CodeWhale) |
| **Windows Support** | Good (not highlighted) | **Pain point** | **Pain point** (Wayland also) | **Critical regression** (#3700) | **Pain point** (#2435) | Not highlighted | Not highlighted (Linux/macOS focus) |
| **MCP Maturity** | Deny rules with glob | Full negotiation PRs | Limited | Runaway spawning | Non-interactive MCP add | Not highlighted | Hugging Face integration |
| **Unique Innovation** | `fallbackModel` chain | `Responses Lite` transport | `--ephemeral` mode, AST eval | Config profiles, permissions | Inline `$skill` invocations | 5D gene self-evolution | WhaleFlow, VS Code extension scaffold |

**Strategic takeaways:**
- **Codex** is investing heavily in MCP as a first-class protocol (UI capability negotiation, plugin catalogs) — differentiating as the "MCP-native" tool
- **Pi** is pursuing the most radical architectural innovation with self-evolving agents and 5D genome concepts — high-risk, high-reward
- **Gemini CLI** is the only tool with systematic component-level evaluations (#24353), suggesting a more scientific engineering approach
- **CodeWhale** is uniquely targeting the Chinese market and HarmonyOS platform, giving it geographic differentiation
- **Claude Code** has the most mature enterprise feature set (deny rules, multi-account, fallback models) but also the most frustrated community around auth reliability

---

## 5. Community Momentum & Maturity

| Tool | Community Size | Engagement Quality | Pain Point Intensity | Innovation Velocity | Maturity Level |
|------|---------------|-------------------|---------------------|-------------------|----------------|
| **Claude Code** | ★★★★★ | ★★★★☆ | ★★★★☆ | ★★★☆☆ | **Established** (v2.1.x, enterprise-grade) |
| **Codex** | ★★★★★ | ★★★★★ | ★★★★★ | ★★★★★ | **Rapidly maturing** (alpha CLI, strong PR pipeline) |
| **Gemini CLI** | ★★★★☆ | ★★★☆☆ | ★★★☆☆ | ★★★★☆ | **Growing** (preview channels, nightly cadence) |
| **Copilot CLI** | ★★★★☆ | ★★★★☆ | ★★★★★ | ★★☆☆☆ | **Stable but strained** (critical regressions) |
| **Kimi CLI** | ★★☆☆☆ | ★★☆☆☆ | ★★☆☆☆ | ★★☆☆☆ | **Deprecation phase** (transitioning to `kimi-code`) |
| **OpenCode** | ★★★★☆ | ★★★★☆ | ★★★★☆ | ★★★★★ | **Rapidly iterative** (v1.16.x, frequent releases) |
| **Pi** | ★★★☆☆ | ★★★★☆ | ★★★☆☆ | ★★★★★ | **Maturing niche** (extension ecosystem, self-evolver) |
| **Qwen Code** | ★★★☆☆ | ★★★☆☆ | ★★★☆☆ | ★★★★☆ | **Growing** (v0.17.x, daemon mode merge) |
| **CodeWhale** | ★★★☆☆ | ★★★☆☆ | ★★★☆☆ | ★★★★★ | **Rapidly expanding** (v0.8.x, new identity) |

**Detailed assessment:**

- **Most active community:** Codex (highest issue/PR velocity, engaged discussion on MCP and sub-agents)
- **Most frustrated user base:** Copilot CLI (critical WSL2 regression, Windows ARM64 crash, rate-limit loops) and Claude Code (auth fragility, image processing waste)
- **Most innovative per commit:** Pi (#5442 self-evolver) and OpenCode (#29217 inline skills, #30970 skill toggle)
- **Most stable/enterprise-ready:** Claude Code (despite auth pain, feature set is mature)
- **Most rapidly expanding feature surface:** CodeWhale (HarmonyOS, VS Code extension, WhaleFlow — all within weeks)
- **Most scientific engineering approach:** Gemini CLI (sole tool with systematic eval infrastructure #24353)

---

## 6. Trend Signals

### 6.1 Multi-Agent Orchestration is the New Frontier
Every tool is investing in sub-agent infrastructure — but the *direction* differs:
- **Parallel-first:** Codex, OpenCode, CodeWhale (concurrent sub-agents, WhaleFlow DAG)
- **Hierarchical:** Claude Code (Cowork, background agents), Gemini CLI (parent-child with turn limits)
- **Self-evolving:** Pi (5D genome as agent memory, no parallel skill pool needed)

**Signal:** The next 6 months will see a "Cambrian explosion" of agent architectures. Expect standardization pressure (Agent-to-Agent protocols, as requested in Claude Code #28300).

### 6.2 MCP Becomes the Universal Integration Bus
Four tools (Codex, Copilot CLI, OpenCode, CodeWhale) are actively extending MCP semantics. The trend is:
- From simple tool listing → **UI capability negotiation** (Codex #26686)
- From per-session → **per-project pooling** (Codex #20883)
- From passive → **cost tracking** (CodeWhale #2486, Copilot CLI #3686)

**Signal:** MCP is evolving into a general agent orchestration protocol, not just a tool registry. Tool developers should plan for MCP as a first-class integration point, not an afterthought.

### 6.3 Windows & WSL Are the Achilles' Heel
Nearly every tool has critical Windows issues:
- **Copilot CLI:** 215% CPU on WSL2 (#3700), Windows ARM64 crash (#3687)
- **Codex:** WSL performance degradation (#25715), sandbox spawn failures (#24391)
- **Kimi:** WebSocket daemon infinite reload on Windows (#2435)
- **OpenCode:** WSL thinking output corruption (#20234)

**Signal:** The AI CLI ecosystem is still Linux-first. Windows developers face a 2-3x higher frustration rate. This is a significant market opportunity for a tool that gets Windows right.

### 6.4 Auth & Credential Management is the #1 Reliability Gap
Three clusters of auth bugs appearing across tools:
1. **Transient error amplification:** Transient 5xx → permanent 401 loops (Claude Code #61912)
2. **Subscription/tier mapping:** Paying users seeing wrong tier (Gemini #27033, Copilot #2101)
3. **Session expiration mid-task:** No reconnection logic (Kimi #2430, Claude Code #65761)

**Signal:** User trust is being eroded by auth fragility. OAuth implementations need idempotent refresh flows, credential backup mechanisms, and clear error messages showing which endpoint/credential is failing.

### 6.5 "

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-06-06)

## 1. Top Skills Ranking

Based on most-commented pull requests, the community’s most actively discussed Skills are:

| # | PR | Skill | Description | Status |
|---|-----|-------|-------------|--------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. Broad concern because every generated document suffers from these issues. | Open |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT** | Create, fill, read, and convert OpenDocument Format files (.odt/.ods). Targets LibreOffice users and open-source document workflows. | Open |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design** (improvement) | Revises existing frontend-design skill for clarity, actionability, and internal coherence—every instruction must be directly executable by Claude. | Open |
| 4 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer** + **skill-security-analyzer** | Meta-skills that evaluate other Skills across structure, documentation, security, and performance dimensions. | Open |
| 5 | [#538](https://github.com/anthropics/skills/pull/538) | **pdf** (fix) | Corrects case-sensitive file references in SKILL.md (8 occurrences) to prevent breakage on case-sensitive filesystems. | Open |
| 6 | [#539](https://github.com/anthropics/skills/pull/539) | **skill-creator** (fix) | Adds pre-parse YAML validation to detect unquoted descriptions containing `:` which cause silent truncation. | Open |
| 7 | [#541](https://github.com/anthropics/skills/pull/541) | **docx** (fix) | Prevents `w:id` collision between tracked changes and existing bookmarks, fixing document corruption. | Open |
| 8 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1-OSS predictor** | Wraps SAP’s open-source tabular foundation model for predictive analytics on SAP business data. | Open |

**Discussion highlights**: The typography skill resonates widely because poor document layout is a universal pain point. The meta-skills (quality/security analyzers) sparked debate on how to govern community contributions. Many fix PRs for PDF, DOCX, and skill-creator reflect growing community investment in tooling reliability.

---

## 2. Community Demand Trends

From the most-commented Issues, the community’s unmet needs cluster around four directions:

- **Collaborative skill management** – [#228](https://github.com/anthropics/skills/issues/228) (13 comments) demands org-wide skill sharing without manual file transfers. This is the #1 most-discussed feature request.
- **Skill evaluation reliability** – [#556](https://github.com/anthropics/skills/issues/556) (11 comments) reports that `run_eval.py` never triggers skills, halting optimization workflows.
- **Skill security & trust** – [#492](https://github.com/anthropics/skills/issues/492) (7 comments) flags community skills distributed under the `anthropic/` namespace as a trust-boundary vulnerability.
- **Duplication and packaging** – [#189](https://github.com/anthropics/skills/issues/189) (6 comments) points out that `document-skills` and `example-skills` plugins install identical content, wasting context window.

Other recurring themes: need for a **multi-file preload** feature ([#1220](https://github.com/anthropics/skills/issues/1220)), **MCP exposure** of Skills ([#16](https://github.com/anthropics/skills/issues/16)), and a dedicated **agent-governance** skill ([#412](https://github.com/anthropics/skills/issues/412)).

---

## 3. High-Potential Pending Skills

These open PRs have sustained discussion and appear likely to merge soon:

- **[Agent-creator meta-skill](https://github.com/anthropics/skills/pull/1140)** – PR #1140 (created May 15, updated June 2). Adds a meta-skill for generating task-specific agent sets, plus fixes for multi-tool evaluation and Windows compatibility. *High recent activity.*
- **[Testing-patterns skill](https://github.com/anthropics/skills/pull/723)** – PR #723 (created Mar 22, updated Apr 21). Comprehensive testing skill covering trophy model, unit testing, and React component tests. *Broad applicability, moderate discussion.*
- **[ServiceNow platform skill](https://github.com/anthropics/skills/pull/568)** – PR #568 (created Mar 8, updated Apr 23). Covers ITSM, ITOM, SecOps, ITAM, CSDM, and IntegrationHub. *Large enterprise interest.*
- **[AURELION skill suite](https://github.com/anthropics/skills/pull/444)** – PR #444 (created Feb 21, updated May 6). Four skills: kernel (structured thinking), advisor, agent, and memory. *Ambitious cognitive framework, steady updates.*
- **[n8n-builder / n8n-debugger](https://github.com/anthropics/skills/pull/190)** – PR #190 (created Dec 31, updated May 18). Adds production-tested skills for n8n workflow builder and debugging. *Niche but active community following.*
- **[Feature-dev workflow skill](https://github.com/anthropics/skills/pull/363)** – PR #363 (created Feb 9, updated Jun 3). Fixes a bug where `TodoWrite` overwrites cause workflow phases to be skipped. *Recent update, directly addresses a common issue.*

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **reliable, production-grade tooling around the skill lifecycle**—both meta-skills (creation, quality analysis, security scanning, evaluation) and platform features (org sharing, multi-file bundling, trust boundaries)—rather than for any single domain-specific skill.

---

# Claude Code Community Digest — 2026-06-06

## Today's Highlights

Three minor releases shipped today, the most notable being **v2.1.166** which introduces a `fallbackModel` setting for automatic failover when the primary model is overloaded, plus glob pattern support in deny-rule tool positions. The community is heavily focused on **multi-account Connector support** (Issue #27302, 195 comments, 261 👍) and a persistent **tool-call parsing crash** that interrupts mid-session work (Issue #63875, 42 comments, 62 👍). OAuth credential corruption continues to generate traction, with two new reports today alone.

## Releases

**v2.1.167** — Bug fixes and reliability improvements. [Release notes](anthropics/claude-code)

**v2.1.166** — Two meaningful features landed:
- **`fallbackModel` setting** — configure up to three fallback models tried in order when the primary model is overloaded or unavailable. The `--fallback-model` flag now also applies to interactive sessions.
- **Glob pattern support in deny rules** — the tool-name position now accepts `"*"` to deny all tools (and similar patterns).

**v2.1.165** — Bug fixes and reliability improvements.

## Hot Issues (10 most noteworthy)

- **[Issue #27302 – Support multiple Connector accounts](anthropics/claude-code Issue #27302)** (195 comments, 261 👍) — The #1 community ask. Users need to use the same connector with different personal vs. work accounts on claude.ai/code. Long-running (since Feb 2026), still open.

- **[Issue #60334 – Image processing failures burning token windows](anthropics/claude-code Issue #60334)** (54 comments, 14 👍) — Images silently removed from conversations with "could not be processed" errors, wasting ~70% of a user's 5-hour window. High frustration, closed as duplicate but symptomatic of a broader reliability gap.

- **[Issue #63875 – Tool call parsing error crashes sessions](anthropics/claude-code Issue #63875)** (42 comments, 62 👍) — "The model's tool call could not be parsed (retry also failed)" stops mid-task work with no recovery. Intermittent across sessions, high upvote count suggests widespread impact.

- **[Issue #28300 – Multi-agent collaboration across machines](anthropics/claude-code Issue #28300)** (23 comments) — Agent-to-Agent protocol request for distributed development teams. Long-running but gaining interest.

- **[Issue #22648 – Account-level settings sync across devices](anthropics/claude-code Issue #22648)** (23 comments, 37 👍) — Settings stored in `~/.claude/` with no sync mechanism. Cross-references four prior requests.

- **[Issue #61889 – CVP-approved users blocked on benign queries](anthropics/claude-code Issue #61889)** (23 comments) — False positive blocks on claude.ai during fresh sessions, despite CVP approval. Not a Claude Code CLI bug but raises trust concerns.

- **[Issue #12433 – macOS process name shows version number](anthropics/claude-code Issue #12433)** (19 comments, 22 👍) — Activity Monitor shows `2.0.53` instead of `claude` for processes. Cosmetic, but has been open since Nov 2025.

- **[Issue #63456 – Opus 4.8 not selectable in CLI](anthropics/claude-code Issue #63456)** (17 comments, 11 👍) — `/model` picker caps at Opus 4.5 despite account having Opus 4.8 available. Platform discrepancy between web and CLI.

- **[Issue #64651 – VSCode background agent output pollutes foreground chat](anthropics/claude-code Issue #64651)** (4 comments) — Subagent output streams into the active conversation, disrupting UX. Reported against VSCode extension specifically.

- **[Issue #61912 – OAuth refresh corrupts credentials on 5xx transient errors](anthropics/claude-code Issue #61912)** (4 comments) — Transient Cloudflare errors during OAuth refresh cause persistent 401 loops across sessions. Requires manual credential file deletion to recover.

## Key PR Progress

Only 4 pull requests updated in the last 24 hours, and none are merge candidates from Anthropic internal development (all appear to be community contributions or test submissions):

- **[PR #58673 – Title: "s"](anthropics/claude-code PR #58673)** — Low-information PR, likely a test or accidental submission.

- **[PR #65723 – Claude/subscription debate chat rx ewi](anthropics/claude-code PR #65723)** — Unclear scope; appears experimental.

- **[PR #65666 – Fix dev container issues](anthropics/claude-code PR #65666)** — Fixes broken devcontainer build (DNS domain issues in firewall) and adds env-key injection mechanism. Practical improvement for contributors.

- **[PR #65619 – fix(plugins): align frontend-design author with marketplace entry](anthropics/claude-code PR #65619)** — Fixes malformed `plugin.json` where two authors were packed into single `author.name` and `author.email` fields. Refers to Issue #61785. Clean structural fix for marketplace compatibility.

**Notable absence:** No internal Anthropic PRs surfaced today, suggesting the team is either consolidating for a larger release or working in private branches.

## Feature Request Trends

1. **Multi-account & connector flexibility** — The dominant theme. Users want to manage multiple identities (personal/work, different GitHub accounts) across connectors without manual reconfiguration.
2. **Cross-session and cross-machine agent coordination** — Growing interest in agent-to-agent protocols (#28300), session teams (#65590), and cross-project session handoff (#65456) for multi-repo workflows.
3. **Settings portability** — Account-level sync across devices (#22648) continues to be requested, with five linked issues now.
4. **Model flexibility in Cowork** — Ability to switch models for running Cowork tasks within Projects (#49649) is a moderate-interest ask.
5. **UI/UX polish** — Collapsible diff viewer (#65311), truncated session titles in VSCode Ctrl+Tab (#65776), and branch selector on iOS (#55500) reflect growing maturity expectations.

## Developer Pain Points

- **OAuth credential lifecycle is fragile** — Three new/auth-related bugs today alone: corrupt refresh on transient 5xx (#61912), stale tokens not recoverable by `/login` (#65761), and `auth status` showing logged-in while sessions reject (#65725). Manual credential deletion is the only recovery path.
- **Image handling wastes API budget** — Silent removal of images with "could not be processed" errors (60–70% token window loss) is a high-frustration issue with no clear workaround (#60334, #65757).
- **Model tool-call parsing is non-deterministic** — Sessions abort mid-task with no recovery mechanism (#63875). Intermittent nature makes it hard to reproduce and trust.
- **Platform-specific UI gaps** — macOS process naming (#12433), iOS branch picker (#55500), Windows `claude mcp add` tool surfacing (#65516), and VSCode background agent noise (#64651) indicate platform testing inconsistencies.
- **Cost/credit UX confusions** — "Usage credits required" blockers appearing even with credits enabled, and `fallbackModel` doesn't always trigger gracefully (#65756).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-06

## Today’s Highlights
The community remains heavily focused on Windows and sub‑agent stability, with long‑standing requests for remote development support finally closed but still high on wish lists. On the development side, multiple MCP and plugin‑sharing PRs landed, while the team also fixed a deadlock in MCP tool listing and improved environment capture for `direnv` users. Two new releases (rusty‑v8 and an alpha of the CLI) rolled out, but the main news is the steady stream of Windows sandbox and WSL performance issues requiring attention.

---

## Releases
* **`rusty-v8-v149.2.0`** – Updated V8 dependency for the Rust binding layer. No user‑visible changes.
* **`rust-v0.138.0-alpha.5`** – Pre‑release of the Codex Rust CLI. Intended for testing; release notes not provided.

---

## Hot Issues
* **[[CLOSED] #10450 – Remote Development in Codex Desktop App](https://github.com/openai/codex/issues/10450)**  
  177 comments, 674 👍. A top community request that was closed without implementation, sparking continued discussion about remote‑workspace support.

* **[#18258 – Codex app on macOS shows ‘Computer Use plugin unavailable’](https://github.com/openai/codex/issues/18258)**  
  Active bug with a workaround (set `features.apps = true` in `config.toml`). Many users affected; 39 comments.

* **[#25715 – Codex App Unusable Slow with WSL as Agent environment](https://github.com/openai/codex/issues/25715)**  
  Severe performance degradation on Windows + WSL2. 31 comments, 29 👍. A key pain point for Windows developers.

* **[#24391 – Windows sandbox: spawn setup refresh fails on CLI 0.133.0](https://github.com/openai/codex/issues/24391)**  
  Broken sandbox after an npm update. 27 comments. Critical for Windows CLI users.

* **[#2920 – Change model/thinking through shortcut](https://github.com/openai/codex/issues/2920)**  
  Closed but highly upvoted enhancement (41 👍). Users want quick model switching without `/model` command.

* **[#20883 – MCP process pool per project instead of per session](https://github.com/openai/codex/issues/20883)**  
  Growing concern that MCP servers are not shared across chats, causing resource waste. 10 comments.

* **[#19197 – Orphaned subagents and session freezes](https://github.com/openai/codex/issues/19197)**  
  Sub‑agent lifecycle issues causing persistent “zombie” processes. Affects Pro+ users. 7 comments.

* **[#19891 – Regression: ‘For coding’ view hides edited file names behind summaries](https://github.com/openai/codex/issues/19891)**  
  UX regression in the app: critical details are collapsed. 7 👍, community frustrated.

* **[#4849 – Make config.toml profiles selectable via CLI](https://github.com/openai/codex/issues/4849)**  
  Long‑running enhancement with 23 👍. Users want to switch provider profiles (e.g., LM Studio) from the terminal.

* **[#24618 – Context compaction hangs for 30‑60 minutes](https://github.com/openai/codex/issues/24618)**  
  Automatic compaction uses a separate endpoint and can stall. 5 comments. High impact for long sessions.

---

## Key PR Progress
* **[#26432 – Release MCP manager lock before listing tools](https://github.com/openai/codex/pull/26432)**  
  Fixes a potential deadlock between tool prewarm and session shutdown. Important for MCP reliability.

* **[#26717 – Stop guardian reviews when parent turns are interrupted](https://github.com/openai/codex/pull/26717)**  
  Prevents orphaned guardian sub‑agents after user interruption. Directly addresses sub‑agent lifecycle complaints.

* **[#26715 – Load direnv environment into shell snapshots](https://github.com/openai/codex/pull/26715)**  
  Captures `direnv`‑modified environment variables so commands run inside Codex see the same context as the terminal.

* **[#26719 – Enable standalone web search in code mode](https://github.com/openai/codex/pull/26719)**  
  Exposes a new `/v1/alpha/search` endpoint to code‑mode agents, enabling native web search without manual tool calls.

* **[#26711 – Reduce TUI legacy core dependencies](https://github.com/openai/codex/pull/26711)**  
  Removes local filesystem assumptions from the TUI, making it compatible with remote app‑server sessions.

* **[#26686 – Propagate client UI capabilities via MCP](https://github.com/openai/codex/pull/26686)**  
  Adds semantic UI‑capability negotiation to MCP handshake, allowing servers to adapt to the client’s interface.

* **[#26703 – TUI Plugin sharing – remote plugin catalog sections](https://github.com/openai/codex/pull/26703)**  
  Final PR in a stack that brings remote plugin catalogs to the TUI, with share‑management and deduplication.

* **[#26678 – Permission profiles: expose availability to clients](https://github.com/openai/codex/pull/26678)**  
  Enterprise‑focused: lets clients know which permission profiles are actually selectable given policy constraints.

* **[#26542 – Send ‘Responses Lite’ transport header](https://github.com/openai/codex/pull/26542)**  
  Performance optimization: new header enables lighter response processing for supported models.

* **[#26698 – Deduplicate skill load warnings](https://github.com/openai/codex/pull/26698)**  
  Suppresses repeated warnings for the same broken `SKILL.md`, reducing noise during file‑watcher reloads.

---

## Feature Request Trends
* **Remote & Project‑Scoped Workspaces** – #10450 (closed but still demanded) and others ask for full remote development (SSH, containers). The community clearly wants Codex to replace VS Code’s remote model.
* **MCP Lifecycle Management** – Multiple issues (#20883, #21984, #11324) call for shared MCP processes, lazy startup, and memory limits. Users want MCP to behave more like a per‑project pool rather than per‑chat.
* **Sub‑Agent Parallelism & Visibility** – #22099, #16900, and #19197 ask for parallel‑first sub‑agents, background task management, and better parent‑child observation. The desire is to make multi‑agent workflows predictable.
* **Config Profiles & Model Switching** – #4849 and #2920 reflect a strong desire for CLI‑selectable provider profiles and quick model/thinking toggles without interrupting the flow.

---

## Developer Pain Points
* **Windows Sandbox & WSL Performance** – Issues #25715, #24391, #25799, #25362, and #23137 show a recurring cluster of Windows‑specific sandbox failures, spawn errors, and severe slowdowns. Windows + WSL users are disproportionately affected and frequently blocked.
* **MCP Server Process Accumulation** – #20883, #21984, and #11324 report that MCP servers, especially headed browsers, are not reused or terminated, leading to memory exhaustion and visible window clutter.
* **Sub‑Agent Orphans & Freezes** – #19197, #16900, and #22099 describe sessions that stall because child agents are not properly cleaned up or the parent thread cannot observe their progress. Redundant work burns usage quotas.
* **Context Compaction & Connectivity Hiccups** – #24618, #26600, and #26274 reveal reliability issues: compaction can hang for an hour, quotas drain while idle, and home‑network reconnection loops make the app unusable.
* **UX Regressions & Hidden Information** – #19891 and #26697 show that recent UI changes collapsed critical file details and introduced paste‑related freezes, eroding trust in the desktop experience.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-06

## Today’s Highlights
Two patch releases (v0.46.0-preview.2 and v0.45.2) landed today, both cherry-picking a single fix (f40498d) to stable channels. On the issue tracker, the community continues to surface agent‑loop and sub‑agent‑state bugs, while an important PR series paves the way for Gemini 3.1 Flash Lite GA and Gemini 3.5 Flash support. The nightly pipeline also produced v0.47.0-nightly.20260605.

## Releases
| Version | Type | Key Changes |
|---------|------|-------------|
| [v0.47.0-nightly.20260605](https://github.com/google-gemini/gemini-cli/compare/v0.47.0-nightly.20260604...v0.47.0-nightly.20260605) | Nightly | Routine tag, no changelog details. |
| [v0.46.0-preview.2](https://github.com/google-gemini/gemini-cli/pull/27699) | Preview | Cherry‑picks commit `f40498d` from the main branch into the preview.1 release. |
| [v0.45.2](https://github.com/google-gemini/gemini-cli/pull/27700) | Patch | Same cherry‑pick applied to the v0.45.1 stable line. |

The cherry‑picked fix (`f40498d`) is not described in the release notes, but its rapid inclusion in two channels suggests it addresses a high‑priority regression.

## Hot Issues (10 selected)

1. **[#27033](https://github.com/google-gemini/gemini-cli/issues/27033) – Pro subscription not reflected in CLI tier** (Closed)  
   *Why it matters:* Users paying for Google One AI Pro see their tier as “Google Assist” in the CLI, breaking feature access. The closed status indicates a fix may have been deployed, but the root cause (tier mapping) remains a pain point for subscribers.

2. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) – Robust component‑level evaluations** (Open)  
   *Why it matters:* This epic tracks 76 behavioral eval tests across 6 Gemini models. Community expects higher confidence in agent components; lack of automated evaluations slows iteration for contributors.

3. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) – Subagent recovery after MAX_TURNS reported as GOAL success** (Open, 2 👍)  
   *Why it matters:* A subagent that hits its turn limit incorrectly reports “success”, hiding interruption. This undermines trust in agent orchestration—critical for long‑running tasks.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) – Gemini does not use skills and subagents enough** (Open)  
   *Why it matters:* Users have created custom skills (e.g., Gradle, Git) but the model rarely invokes them unless explicitly told. Reducing the friction of skill adoption is a top community request.

5. **[#27326](https://github.com/google-gemini/gemini-cli/issues/27326) – 403 PERMISSION_DENIED on cloudcode-pa** (Closed)  
   *Why it matters:* Google One AI Pro subscribers are blocked by a persistent 403 error. Two proposed fixes (#25450, #26420) were never merged, causing frustration. Closed status may indicate a workaround or upstream fix.

6. **[#15404](https://github.com/google-gemini/gemini-cli/issues/15404) – False positive stealer detection** (Open, Help wanted)  
   *Why it matters:* Temp files are flagged as malware (Generic.PyStealer) by antivirus, causing quarantine. Users are blocked from normal operation—a significant trust and usability issue.

7. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) – Shell command gets stuck with “Waiting input” after completion** (Open, 3 👍)  
   *Why it matters:* After executing a simple shell command, the CLI hangs indefinitely. This breaks non‑interactive workflows and is a top‑priority (P1) bug.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) – Browser subagent fails in Wayland** (Open, 1 👍)  
   *Why it matters:* Linux users on Wayland cannot use the browser subagent. With growing Linux desktop adoption, this platform gap is increasingly felt.

9. **[#27692](https://github.com/google-gemini/gemini-cli/issues/27692) – Duplicate agent name warning when running from home directory** (Open)  
   *Why it matters:* A false‑positive warning appears when the workspace is `~`. Nuisance for developers who often run CLI from home.

10. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) – AST‑aware file reads, search, and mapping** (Open, 1 👍)  
    *Why it matters:* This epic explores whether AST tools can reduce token usage and improve code navigation. If successful, it could drastically lower costs and improve agent accuracy.

## Key PR Progress (10 selected)

1. **[#27705](https://github.com/google-gemini/gemini-cli/pull/27705) – Promote Gemini 3.1 Flash Lite to GA & support Gemini 3.5 Flash** (Open, Size XL)  
   *Impact:* Replaces retired preview models with stable `gemini-3.1-flash-lite` and adds support for `gemini-3.5-flash`. This is a major model pipeline update.

2. **[#27372](https://github.com/google-gemini/gemini-cli/pull/27372) – Fix crash on PTY resize after process exit** (Closed)  
   *Impact:* Catches `EBADF` when a background shell process exits before a resize event is processed. Stops a frequent UI crash.

3. **[#27375](https://github.com/google-gemini/gemini-cli/pull/27375) – Correct Vertex AI model ID regex** (Closed)  
   *Impact:* Vertex AI users on Gemini 3.1 lost access to tools (e.g., web search) due to a regex that failed on full resource‑path model IDs. Now fixed.

4. **[#27369](https://github.com/google-gemini/gemini-cli/pull/27369) – Prevent `--resume` from hiding sessions** (Closed)  
   *Impact:* Critical UI fix: sessions launched with `--resume` were disappearing from the `/chat` browser. Now restored.

5. **[#27365](https://github.com/google-gemini/gemini-cli/pull/27365) – Add `--ephemeral` session mode** (Closed)  
   *Impact:* New flag for headless/annotation tasks prevents session log flooding. Written by a community contributor.

6. **[#27572](https://github.com/google-gemini/gemini-cli/pull/27572) – Handle tmux false‑positive background detection** (Open)  
   *Impact:* Fixes theme‑switching regression when running inside tmux + mosh. A common setup for remote developers.

7. **[#27568](https://github.com/google-gemini/gemini-cli/pull/27568) – Fall back when ripgrep execution fails** (Open)  
   *Impact:* Graceful degradation to legacy `GrepTool` when `rg` is missing or returns exit 64. Improves reliability in constrained environments.

8. **[#27552](https://github.com/google-gemini/gemini-cli/pull/27552) – Fix `$` substitution in LLM prompt interpolation** (Open)  
   *Impact:* Prevents silent corruption of file content containing `$` characters when building prompts. Affects all template‑based prompts.

9. **[#27701](https://github.com/google-gemini/gemini-cli/pull/27701) – Treat configured `includeDirectories` as optional** (Closed)  
   *Impact:* A missing optional directory (e.g., `.kilocode/rules`) no longer crashes CLI startup—a minor but common annoyance.

10. **[#27708](https://github.com/google-gemini/gemini-cli/pull/27708) – Harden AI prompt around untrusted data** (Open)  
    *Impact:* CI workflow now avoids passing potentially unsafe data directly into an AI prompt, using a middle‑man file instead. Improves security hygiene.

## Feature Request Trends
- **AST‑aware tooling** (#22745, #22746): Community wants the CLI to understand code structure at the AST level for precise edits, reduced token waste, and better codebase mapping.
- **Component‑level evaluation infrastructure** (#24353): Users and maintainers desire automated behavioral tests for every agent component, not just end‑to‑end.
- **Agent autonomy vs. safety** (#21968, #22672): Requests for the model to proactively use custom skills (without explicit instructions) while also avoiding destructive commands (e.g., `git reset --force`).
- **Browser agent resilience** (#22232, #22267): Persistent sessions, lock recovery, and configuration overrides for the browser subagent are high on the wishlist.
- **Memory system improvements** (#26516, #26522, #26523, #26525): Several issues target the Auto Memory feature: better redaction, deterministic logging, and handling of low‑signal sessions.

## Developer Pain Points
- **Agent loops and misreported successes** (#22323, #16295): Subagents repeatedly reporting “GOAL” when actually hitting limits, or falling into infinite loops, erodes trust.
- **Authentication and subscription mapping** (#27033, #27326): Pro subscribers hit 403 errors or see wrong tier; OAuth/permission bugs are common.
- **Shell and terminal handling** (#25166, #27188, #21983): PTY hangs, OpenCL build failures on NVIDIA GPUs, and Wayland incompatibility frustrate Linux users.
- **History and session corruption** (#25646, #27555): Rewind points lost after resume, shell history mangled by backslash merging.
- **False‑positive security alerts** (#15404): Antivirus quarantine of Gemini temp files – a blocker for many Windows users.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-06

## Today’s Highlights
Version **1.0.60** shipped yesterday with a handful of fixes (tab completion for `..`, reasoning effort for Anthropic, screen-resume after sleep). The community is buzzing about a **critical WSL2 CPU regression** (#3700), a **Windows ARM64 crash under load** (#3687), and a **persistent rate-limit / transient API error** pattern (#2101). Several new feature requests around persistent permissions and security hardening also surfaced.

## Releases
- **[v1.0.60](https://github.com/github/copilot-cli/releases/tag/v1.0.60)** — 2026-06-05  
  - Tab completes `..` parent traversal in slash-command path arguments instead of switching tabs  
  - Adds `max reasoning effort` level for Anthropic models; all effort levels now available on every plan  
  - Fixes blank screen after waking from sleep inside a terminal multiplexer  

## Hot Issues (10 noteworthy)

1. **[#2101 – Transient API error → rate limit](https://github.com/github/copilot-cli/issues/2101)** 🟧 OPEN  
   *High community engagement (27 comments, 17 👍).* Users hitting repeated transient API errors that quickly escalate to a rate limit block. Suggests a need for better retry logic or backoff.

2. **[#2334 – Please bring back no-alt-screen](https://github.com/github/copilot-cli/issues/2334)** 🟧 OPEN  
   *28 👍 (highest reaction count).* The alt-screen mode broke scrolling, text search, and clipboard copy. Community strongly wants a `--no-alt-screen` option restored.

3. **[#2398 – Default config file for permissions](https://github.com/github/copilot-cli/issues/2398)** 🟧 OPEN  
   *10 👍.* Setting tool permissions every session is tedious. Request for a global/per-repo config that persists approvals.

4. **[#3687 – copilot.exe fatal abort on Windows ARM64](https://github.com/github/copilot-cli/issues/3687)** 🟧 NEW  
   *0 comments, but severe.* The CLI hard-aborts (BEX64 / 0xc0000409) under load, especially on Windows Terminal tab restore. Reproduced on 1.0.57 and 1.0.60.

5. **[#3700 – 1.0.60 WSL2 regression: 215% CPU while idle, TUI frozen](https://github.com/github/copilot-cli/issues/3700)** 🟧 NEW  
   *High severity (1 👍).* Fresh WSL2 sessions immediately spin the main thread at 215% CPU and freeze output. Must restart to recover. Regression of #2208.

6. **[#3547 – Background sub-agent hangs at total_turns=0 with gpt-5.5](https://github.com/github/copilot-cli/issues/3547)** 🟧 OPEN  
   *0 comments.* When a parent agent spawns a background sub-agent with `model="gpt-5.5"`, the sub-agent never progresses. Indefinite hang.

7. **[#3701 – Runaway MCP server spawning on Windows](https://github.com/github/copilot-cli/issues/3701)** 🟧 NEW  
   *0 comments.* IDE lock-file watcher triggers re-init loop, spawning unbounded child processes. CPU/lag issue.

8. **[#3563 – Tool approvals silently lost in parallel sessions](https://github.com/github/copilot-cli/issues/3563)** 🟧 OPEN  
   *1 comment.* When two CLI sessions run simultaneously and persist "Always allow" approvals, one session’s config can overwrite the other. Leads to confusing permission denials.

9. **[#3697 – Option to disable repository hooks for supply-chain risk](https://github.com/github/copilot-cli/issues/3697)** 🟧 NEW  
   *2 👍.* Inspired by the Miasma worm campaign. Users want a way to disable auto-execution of repo-provided hooks to prevent configuration-injection attacks.

10. **[#2998 – Copying from CLI pastes previous clipboard item](https://github.com/github/copilot-cli/issues/2998)** 🟧 OPEN  
    *0 new comments but longstanding.* Selecting text in the CLI overwrites the clipboard with previously copied content. Still unresolved.

## Key PR Progress
**No pull requests were updated in the last 24 hours.** All community activity was focused on issues and the new release.

## Feature Request Trends
- **Persistent & configurable permissions** — Multiple requests for a default config file for tool approvals (#2398) and for parallel-session-safe permission storage (#3563).  
- **TUI improvements** — Restore “no-alt-screen” mode (#2334), always show session name in rename (#3415), and add `/ot` as a synonym for off-topic prompts (#3702).  
- **Platform expansion** — Add voice-mode support for `linux-arm64` (#3690) and fix auto-update on Alpine Linux (#3696).  
- **Security & supply-chain hardening** — Disable repository hooks (#3697) and add ability to allow-list tools in non-interactive mode (#3699).  
- **Cost transparency** — Expose AI credit consumption via hooks for external tracking (#3686).

## Developer Pain Points (Recurring Frustrations)
- **Rate-limits & transient errors** (#2101) — Retry logic feels insufficient; users frequently blocked.  
- **Clipboard & keyboard conflicts** (#2998, #3693, #2344) — Copy/paste behavior is broken on many terminals, and `Ctrl+Z` unexpectedly closes the CLI.  
- **Parallel session conflicts** (#3563) — Permission config and tool approvals get corrupted when multiple CLI instances run.  
- **Crashes & performance regressions** (#3687, #3700, #3701) — Windows ARM64 aborts, WSL2 CPU spikes, and MCP server leaks are top-of-mind today.  
- **Inconsistent path resolution** (#3688) — Custom agents, skills, and `.mcp.json` are resolved relative to different base directories (git root vs cwd), causing confusion.  
- **Resume / fork failures** (#3689, #3694, #3695) — Case-sensitive repository name mismatch, NAPI string conversion errors, and `chronicle` search not linking to successful resume.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-06

## Today's Highlights

The `kimi-cli` repository saw its **final naming polish** and a **major stability fix** with the 1.47.0 release, which also introduces a gentle upgrade path to the new standalone Kimi Code. A critical bug (#2435) renders the **Work tab** completely unusable on Windows due to a WebSocket daemon infinite reload loop. Meanwhile, the long-running **RalphFlow architecture** PR (#1960) was finally merged, bringing automated iteration with ephemeral contexts and convergence detection to the agent.

## Releases

**[v1.47.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.47.0)** — released 2026-06-05  
- **Error handling improvements**: Trailing output is now included in error briefs, and briefs are rendered as plain text ([PR #2389](https://github.com/MoonshotAI/kimi-cli/pull/2389)).  
- **Project rename**: Documentation now refers to this repository as **Kimi CLI** (Python edition) to avoid name collision with the successor `MoonshotAI/kimi-code` ([PR #2431](https://github.com/MoonshotAI/kimi-cli/pull/2431)).  
- **Upgrade guidance**: New `/upgrade` command installs the standalone Kimi Code, migrates config & sessions automatically, and shows a welcome-screen nudge — no forced prompts or sunset countdown ([PR #2432](https://github.com/MoonshotAI/kimi-cli/pull/2432)).

## Hot Issues

Only two issues were updated in the last 24 hours; both are highlighted below.

1. **[#2435 – Bug: Kimi Work tab "Daimon control WS not ready" + infinite reload at 99%](https://github.com/MoonshotAI/kimi-cli/issues/2435)**  
   **Status:** Open (0 comments, 0 👍)  
   **Why it matters:** The Work tab in `kimi web` is completely blocked. A WebSocket daemon initialization failure causes an infinite reload loop at 99%, making the feature unusable. Reported on Windows 10/11 with CLI version 1.41.0. Community reaction is silent so far, but this is a severe regression for Windows users relying on the Work tab.

2. **[#2430 – Auto logged out in the middle of a task](https://github.com/MoonshotAI/kimi-cli/issues/2430)**  
   **Status:** Closed (resolved)  
   **Why it matters:** A user on Windows 10 using Kimi Code (kimi-k2.6) experienced session expiration mid-task after walking away. The issue was closed without comments, but it highlights authentication persistence problems during long-running operations — a common pain point for developers.

## Key PR Progress

All six PRs updated in the last 24 hours are listed below.

1. **[#1960 – feat(soul): RalphFlow architecture with ephemeral context and convergence detection](https://github.com/MoonshotAI/kimi-cli/pull/1960)**  
   **Status:** Closed (merged)  
   **Description:** Introduces an automated iteration framework that prevents infinite loops in the agent. Runs flow iterations in isolated temporary context files, keeping main context clean. Includes convergence detection for multi-step workflows. This is a foundational architectural change — expect fewer stuck agents in complex tasks.

2. **[#2434 – fix: suppress MCP connection errors and handle LLM double-serialization](https://github.com/MoonshotAI/kimi-cli/pull/2434)**  
   **Status:** Open  
   **Description:** Fixes three issues discovered during heavy MCP (Model Context Protocol) tool usage. Suppresses spurious MCP connection errors (Notion, code-index, etc.) in the crash handler, cleans up event-loop termination, and handles double-serialization of LLM outputs. Essential for stability when using external tools.

3. **[#2429 – fix: prevent idle cursor blink from forcing scroll to bottom in Linux terminals](https://github.com/MoonshotAI/kimi-cli/pull/2429)**  
   **Status:** Open  
   **Description:** Resolves [#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422) — on Linux, after a conversation completes, the terminal auto-scrolls to bottom every ~1 second, making it impossible to read history. The fix stops the idle cursor animation from triggering a scroll. A small UX improvement but impactful for daily use.

4. **[#2433 – chore(release): bump kimi-cli to 1.47.0](https://github.com/MoonshotAI/kimi-cli/pull/2433)**  
   **Status:** Closed (merged)  
   **Description:** Official release bump from 1.46.0 to 1.47.0, syncing the `kimi-code` wrapper. See release notes above.

5. **[#2432 – feat(shell): guide users to upgrade to the new Kimi Code](https://github.com/MoonshotAI/kimi-cli/pull/2432)**  
   **Status:** Closed (merged)  
   **Description:** Adds `/upgrade` command, a welcome-screen nudge, and automatic migration of config & sessions. Designed to be non-intrusive — no forced prompts or apocalyptic language. Highlights the transition strategy for this repository.

6. **[#2431 – docs: rename project to Kimi CLI and link to Kimi Code CLI successor](https://github.com/MoonshotAI/kimi-cli/pull/2431)**  
   **Status:** Closed (merged)  
   **Description:** Cleans up naming in the README, renaming all self-references from "Kimi Code CLI" back to "Kimi CLI" (Python edition) and adding a prominent link to the new `MoonshotAI/kimi-code` repository. Ends ambiguity between the old and new codebases.

## Feature Request Trends

With only two open/closed issues available, clear trend extraction is limited. However, the following directions are hinted:

- **WebSocket/daemon reliability** for the Work tab (Issue #2435) – users need the interactive Work environment to be stable, especially on Windows.
- **Session persistence** during long tasks (Issue #2430) – authentication should not expire mid-session without warning.

Given the low volume, the community may be shifting focus to the new `kimi-code` repository, which is the designated successor.

## Developer Pain Points

- **Windows compatibility** – Both reported issues target Windows 10/11, indicating ongoing platform-specific instability (Work tab WS daemon, auto logout).
- **WebSocket daemon initialization** – The "Daimon control WS not ready" error suggests a root cause in the daemon start-up sequence that can leave the Work tab in a permanent reload loop.
- **Auto-logout during long tasks** – Users lose progress when sessions expire after idle periods; no warning or reconnection logic is evident.
- **Linux terminal scrolling** – A minor but frequent annoyance: idle cursor blinking forces the terminal to scroll to bottom, making history review painful on Linux.

*Note: Data is limited to the last 24 hours. For a broader picture, refer to the full issue tracker and the new `MoonshotAI/kimi-code` repository.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-06

## Today’s Highlights
Two releases landed in the last 24 hours: **v1.16.2** patches reasoning‑summary compatibility, edit‑overwrite safety, and Bedrock session hangs; **v1.16.0** introduces managed workspace cloning, session movement between workspaces, OpenAI models via Bedrock, and skill discovery with file‑based agent loading. Community discussion continues to centre on subagent UI visibility, doom‑loop detection gaps, and a strong push for dynamic workflow automation.

---

## Releases

### [v1.16.2](https://github.com/anomalyco/opencode/releases/tag/v1.16.2)
- Reasoning summaries now only run on providers that support them, preventing GPT‑5 request failures.
- Edit operations refuse loose matches that could overwrite wrong code or replace existing files.
- Fixed Bedrock sessions hanging indefinitely.

### [v1.16.0](https://github.com/anomalyco/opencode/releases/tag/v1.16.0)
- Managed workspace cloning that preserves dirty and untracked files.
- Moving sessions between workspaces and directories.
- Proper OpenAI model support through AWS Bedrock.
- Skill discovery and file‑based agent loading.
- Updated GitHub Copilot usage.

---

## Hot Issues
*(10 of the most active or high‑impact issues; includes both open and closed)*

1. **[Unable to read images for some models #5359](https://github.com/anomalyco/opencode/issues/5359)** — Pasting images stopped working after v1.0.137; affects LiteLLM + Vertex AI. 15 comments, unresolved.

2. **[LM Studio Failure to refresh models #2047](https://github.com/anomalyco/opencode/issues/2047)** — Adding/removing models in LM Studio isn’t reflected in OpenCode even after re‑login. 15 comments, 3 👍.

3. **[Auto‑scroll stops working after manually scrolling #29992](https://github.com/anomalyco/opencode/issues/29992)** — When a user scrolls back to bottom, auto‑scroll ceases; new content arrives but viewport stays fixed. Now closed after 13 comments, 15 👍.

4. **[WSL output one word per line during thinking #20234](https://github.com/anomalyco/opencode/issues/20234)** — Under WSL, thinking output is split word‑by‑word. 9 comments, 4 👍. Still open.

5. **[Doom loop not caught during reasoning or output #12716](https://github.com/anomalyco/opencode/issues/12716)** — Infinite tool‑call loops go undetected. 8 comments, 3 👍. Community reporting similar detection gaps in #25254.

6. **[Add Dynamic workflows for repeatable multi‑step automation #29059](https://github.com/anomalyco/opencode/issues/29059)** — Inspired by Claude Code’s new feature; wants project‑local workflows. 7 comments, 12 👍.

7. **[Improve subagent runtime visibility in chat UI #22233](https://github.com/anomalyco/opencode/issues/22233)** — Cannot see which subagent is running, what it’s doing, or how long. 6 comments, heavily upvoted.

8. **[Desktop cannot see File tree #30545](https://github.com/anomalyco/opencode/issues/30545)** — Enabling advanced settings (File tree) has no effect in Desktop v1.15.13. 6 comments, open.

9. **[Plan Mode + Question tool auto switch to Build mode #7801](https://github.com/anomalyco/opencode/issues/7801)** — After creating a plan, user must manually switch to Build mode; wants automatic transition. 5 comments, 18 👍.

10. **[Multi‑user auth and per‑user provider credentials for web #20067](https://github.com/anomalyco/opencode/issues/20067)** — Shared enterprise deployments need separate credentials per team member. 5 comments, 12 👍.

---

## Key PR Progress
*(10 pull requests merged or under active review)*

1. **[feat(skill): add skill enable/disable toggle with HTTP API and TUI #30970](https://github.com/anomalyco/opencode/pull/30970)** — Adds a toggle UI in the skill dialog, persisted to `skills.json`. Press `space` to enable/disable.

2. **[fix(cli): handle OSC52 clipboard passthrough under GNU screen #28592](https://github.com/anomalyco/opencode/pull/28592)** — Fixes clipboard copying when running inside GNU screen (previously used tmux‑only DCS format). Closes #28590.

3. **[feat(opencode): support non‑interactive MCP add #31054](https://github.com/anomalyco/opencode/pull/31054)** — Merged. `opencode mcp add` now accepts `--env`, `--type`, `--header` directly, enabling scripting.

4. **[fix(provider): keep compacted Anthropic tool histories user‑led #31052](https://github.com/anomalyco/opencode/pull/31052)** — Prevents Anthropic rejection after compaction by ensuring conversations start with a user message. Closes #31048.

5. **[fix(core): settle owned process output #31043](https://github.com/anomalyco/opencode/pull/31043)** — Improves child‑process lifecycle: avoids orphaned pipes and ensures exit‑event clean‑up.

6. **[fix(session): settle pending tool calls on schema errors #30091](https://github.com/anomalyco/opencode/pull/30091)** — When a stream emits a schema‑validation tool‑error, the pending tool is settled to error rather than left hanging. Closes #30093.

7. **[fix(core): omit unavailable host tools #31050](https://github.com/anomalyco/opencode/pull/31050)** — Removes built‑in tools that are not available on the current host, preventing “unknown tool” errors. Adds additive configuration.

8. **[feat(tui): Add inline $skill invocations with SKILL pill + pasteText #29217](https://github.com/anomalyco/opencode/pull/29217)** — Type `$` in the prompt to autocomplete skills; skills can be invoked inline with a pill UI. Closes four related issues.

9. **[fix(desktop): allow choosing Windows install directory #30242](https://github.com/anomalyco/opencode/pull/30242)** — Switches NSIS installer from one‑click to assisted flow; lets users pick install path. Fixes #26818.

10. **[fix(core): make V2 reads media‑aware and binary‑safe #31038](https://github.com/anomalyco/opencode/pull/31038)** — Classifies supported image media before handling binary; rejects unsupported formats without persisting base64. Preserves image results across providers.

---

## Feature Request Trends
The most‑requested directions from the issue tracker are:

- **Subagent visibility and progress indicators** — Multiple requests demand that the TUI show which subagent is running, its status, runtime, and progress bars ([#22233](https://github.com/anomalyco/opencode/issues/22233), [#23784](https://github.com/anomalyco/opencode/issues/23784), [#22153](https://github.com/anomalyco/opencode/issues/22153)).
- **Dynamic workflows** — Project‑local repeatable automation, inspired by Claude Code’s workflow feature ([#29059](https://github.com/anomalyco/opencode/issues/29059)).
- **Plan‑mode to Build‑mode auto‑switch** — After a plan is accepted, the system should automatically switch to Build mode ([#7801](https://github.com/anomalyco/opencode/issues/7801)).
- **MCP improvements** — Non‑interactive `mcp add` (now merged in #31054) and inline argument support (#30175).
- **Multi‑user / enterprise auth** — Per‑user credentials and session isolation for web deployments ([#20067](https://github.com/anomalyco/opencode/issues/20067)).
- **Vision / custom provider support** — Image attachment support for OpenAI‑compatible providers that support vision ([#8875](https://github.com/anomalyco/opencode/issues/8875)).
- **Doom loop detection** — Community wants detection to cover cross‑message repetitions and not just single‑message loops ([#12716](https://github.com/anomalyco/opencode/issues/12716), [#25254](https://github.com/anomalyco/opencode/issues/25254)).

---

## Developer Pain Points
Recurring frustrations and high‑frequency complaints visible in this week’s issues:

- **Terminal quirks** — WSL output is one word per line during thinking ([#20234](https://github.com/anomalyco/opencode/issues/20234)); auto‑scroll breaks after manual scroll ([#29992](https://github.com/anomalyco/opencode/issues/29992)).
- **Doom loop detection blind spots** — Infinite tool‑call loops go undetected, especially when loops span multiple messages ([#12716](https://github.com/anomalyco/opencode/issues/12716), [#25254](https://github.com/anomalyco/opencode/issues/25254)).
- **Process lifecycle bugs** — Orphaned `opencode` processes (~500MB each) when the parent exits ([#13001](https://github.com/anomalyco/opencode/issues/13001)).
- **Provider / vision incompatibility** — Images fail silently with some providers ([#5359](https://github.com/anomalyco/opencode/issues/5359)); custom providers lack vision capability declaration ([#8875](https://github.com/anomalyco/opencode/issues/8875)).
- **Desktop UI glitches** — File tree toggle ineffective ([#30545](https://github.com/anomalyco/opencode/issues/30545)); MCP toggles unresponsive on macOS ([#30996](https://github.com/anomalyco/opencode/issues/30996)).
- **Billing confusion** — Users report double charges and subscription not recognised after payment ([#31028](https://github.com/anomalyco/opencode/issues/31028), [#31008](https://github.com/anomalyco/opencode/issues/31008)).
- **Session portability** — Copying `opencode.db` between OSes leads to invisible sessions in the web UI ([#29799](https://github.com/anomalyco/opencode/issues/29799)).
- **Clipboard passthrough** — OSC52 broken under GNU screen (fix PR in progress #28592).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — June 6, 2026

## Today’s Highlights
The community continues to stabilize the TUI and streaming infrastructure, with fixes for terminal rendering crashes, auto‑compaction state corruption, and retry logic. Extension developers gain new capabilities: `sendUserMessage` now supports `expandPromptTemplates`, and built‑in tools can be excluded via a public API. A major PR introduces a self‑evolving agent framework using the 5D gene concept.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 Noteworthy)

1. **OpenAI‑Codex hangs on `Working…` with zero‑usage aborted turns**  
   `#4945` – [open] – 53 comments, 28 👍  
   The interactive TUI stalls with no output or error; recovery requires Escape. Community suspects a race in the streaming layer.  
   [GitHub](https://github.com/earendil-works/pi/issues/4945)

2. **Add `pi.runWhenIdle()` to schedule work after agent settles**  
   `#2023` – [open] – 12 comments, 5 👍  
   A long‑standing feature request to queue actions like `/reload-runtime` once the agent is fully idle, enabling cleaner extension patterns.  
   [GitHub](https://github.com/earendil-works/pi/issues/2023)

3. **`local-llm` streams die after 5 min due to undici `bodyTimeout`**  
   `#3715` – [closed] – 9 comments, 3 👍  
   Long `Write` tool calls against local LLMs (e.g., vLLM + Qwen3) hit `UND_ERR_BODY_TIMEOUT` regardless of `retry.provider.timeoutMs`.  
   [GitHub](https://github.com/earendil-works/pi/issues/3715)

4. **Links not clickable after alternative term mode update**  
   `#4180` – [closed] – 8 comments  
   Hyperlinks in agent output lost clickability after a `pi-codingagent` term mode change.  
   [GitHub](https://github.com/earendil-works/pi/issues/4180)

5. **`pi-fancy-loader` always marked as updatable**  
   `#5388` – [closed] – 5 comments  
   Repeating “Package updates available” notification even after `pi update`.  
   [GitHub](https://github.com/earendil-works/pi/issues/5388)

6. **Shift+Enter submits instead of creating new line**  
   `#5188` – [open] – 5 comments, 2 👍  
   Custom keybinding `"tui.input.newLine": ["shift+enter"]` does not work; Ctrl+J works.  
   [GitHub](https://github.com/earendil-works/pi/issues/5188)

7. **Auto‑compaction crashes with “Cannot continue from message role: assistant”**  
   `#5420` – [open] – 2 comments, 3 👍  
   After compacting a long session (203k+ tokens), the message list ends with an assistant turn, causing `agent.continue()` to throw.  
   [GitHub](https://github.com/earendil-works/pi/issues/5420)

8. **`_prepareRetry` crashes on retryable error after end_turn**  
   `#5445` – [closed] – 1 comment  
   A race: retry mechanism removes the error message, exposing a prior `end_turn` assistant message, then `continue()` fails.  
   [GitHub](https://github.com/earendil-works/pi/issues/5445)

9. **`sanitizeSurrogates()` invalidates Anthropic signature**  
   `#5416` – [closed] – 2 comments  
   Sanitizing surrogate pairs on thinking blocks modifies the signed payload, causing Anthropic API rejections.  
   [GitHub](https://github.com/earendil-works/pi/issues/5416)

10. **Rendered line exceeds terminal width causes crash**  
    `#5422` – [closed] – 2 comments  
    Uncaught exception when TUI output exceeds terminal width, killing the process.  
    [GitHub](https://github.com/earendil-works/pi/issues/5422)

---

## Key PR Progress (10 Important)

1. **`@pi-mono/self-evolver` – 5D gene/genome equivalent**  
   `#5442` – [closed] – 0 comments  
   Turns pi‑mono into a self‑evolving agent by treating 5D memory as the genome. No parallel skill pool needed.  
   [GitHub](https://github.com/earendil-works/pi/pull/5442)

2. **Codex/native subagents**  
   `#5441` – [closed]  
   Implements native sub‑agent orchestration within Codex, likely addressing multi‑step workflows.  
   [GitHub](https://github.com/earendil-works/pi/pull/5441)

3. **Export coding‑agent package path helpers**  
   `#5439` – [closed]  
   Makes `getPackageDir()`, `getReadmePath()`, etc. available from the public API.  
   [GitHub](https://github.com/earendil-works/pi/pull/5439)

4. **Neutralize `SUMMARIZATION_SYSTEM_PROMPT` for non‑coding agents**  
   `#5437` – [closed]  
   Replaces “AI coding assistant” with “AI assistant” so compaction works in non‑coding contexts.  
   [GitHub](https://github.com/earendil-works/pi/pull/5437)

5. **Validate LLM messages after extension transforms**  
   `#5435` – [closed]  
   Catches invalid message sequences introduced by extension `context` hooks, replacing opaque provider errors with clear diagnostics.  
   [GitHub](https://github.com/earendil-works/pi/pull/5435)

6. **Tolerate extraneous keys in `edits[]` (robustness for noisy models)**  
   `#5434` – [closed]  
   Removes `additionalProperties: false` from inner edit schemas, allowing weaker models to still pass valid edits.  
   [GitHub](https://github.com/earendil-works/pi/pull/5434)

7. **Fix models.json migration error path**  
   `#5429` – [closed]  
   Replaces raw `JSON.parse` crash with a user‑friendly error including the file path.  
   [GitHub](https://github.com/earendil-works/pi/pull/5429)

8. **Add Anthropic Vertex provider**  
   `#5262` – [open]  
   Native provider for Claude on Google Cloud Vertex AI, reusing the existing Anthropic streaming path.  
   [GitHub](https://github.com/earendil-works/pi/pull/5262)

9. **Workflow extension for multi‑agent orchestration**  
   `#5426` – [closed]  
   Introduces `run_workflow` tool + `/workflow` command with context firewall and sub‑agent refactored execution.  
   [GitHub](https://github.com/earendil-works/pi/pull/5426)

10. **Approval system for workspaces**  
    `#5332` – [open] – *in progress*  
    Adds `.pi.user` folder and interactive approval for loading `.pi` / `.pi.user` on first use.  
    [GitHub](https://github.com/earendil-works/pi/pull/5332)

---

## Feature Request Trends

- **WebSocket transport** – Multiple requests to extend WebSocket (or `websocket-cached`) support to OpenAI API endpoints and `openai-responses` provider (issues #3442, #5446). Community wants lower latency and cached responses.
- **Image attachment from CLI** – Request to attach `.jpeg`/`.png` files via typed command, especially for SSH users wanting vision capabilities (issue #5279). Also clipboard image paste currently broken (issue #5438).
- **Composable refactoring** – Desire to extract `runAgentSession` from the monolithic `main.ts` (issue #5444) and merge `ExtensionCommandContext` into `ExtensionContext` (issue #5443) to use `waitForIdle`, `navigateTree` etc. from any handler.
- **Template expansion in `sendUserMessage`** – Adding `expandPromptTemplates` option to `sendUserMessage` so extensions can trigger commands that use `navigateTree` (issue #5448).
- **Configurable TUI output padding** – Request for a `output.paddingX` setting to remove the hardcoded left space for easier copy‑paste (issue #5436).

---

## Developer Pain Points

- **Streaming & TUI stability** – Frequent crashes: terminal width overflows, auto‑compaction state corruption, retry logic exposing invalid assistant messages, and `sanitizeSurrogates` breaking Anthropic signatures.  
- **Keybinding regressions** – Shift+Enter not respecting custom `newLine` bindings, and broken clickable links after term mode changes.  
- **Persistent update notifications** – `pi-fancy-loader` repeatedly marked as updatable despite running `pi update`.  
- **API key / auth friction** – Startup errors about missing API keys for DeepSeek even after saving keys, and `detectCompat` not matching model IDs when using proxies like OpenRouter.  
- **Model session persistence** – Continued sessions restore the correct model but don’t update `defaultModel`, requiring manual settings editing for new sessions.  
- **Long‑running tool timeouts** – Undici’s 5‑minute body timeout cannot be overridden for local LLMs, causing failed long `Write` calls.

---

*This digest was generated from GitHub activity on `earendil-works/pi`. All links point to the actual issues/PRs.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-06

## Today’s Highlights
A nightly release (v0.17.1) ships with a fix for copy output skipping thought parts, while the community continues to report severe OOM crashes and blocks in the daemon/web-shell integration. Two pull requests landed that extend the HTTP API surface for session forking and rewind endpoints, and the triage automation workflow was repaired. Meanwhile, feature requests for multimodal support on `qwen3.7-plus` and a dedicated `web_search` tool signal growing demand for richer model capabilities.

## Releases
- **v0.17.1-nightly.20260606.16c1d9a5a**  
  [Release notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260606.16c1d9a5a) – Prepares the v0.17.1 stable release and includes a CLI fix: `he-yufeng` patched the copy output to filter out thought parts (`#4742`).

## Hot Issues
1. **#4815** – Severe OOM with `qwen --resume` and Escape key broken  
   A critical P1 bug: OOM reappears within ~10 minutes after resume; Escape key becomes completely non-functional. The community has responded with additional repro steps. [Issue](https://github.com/QwenLM/qwen-code/issues/4815)

2. **#4802** – `qwen3.7-plus` should support multimodal (image/video) input  
   The regex-based modality detection misses the Plus variant, causing the model to be treated as text-only. A `welcome-pr` label invites contributions. [Issue](https://github.com/QwenLM/qwen-code/issues/4802)

3. **#4777** – Deferred-tools listing busts prompt cache on every MCP discovery  
   The system prompt grows unnecessarily when deferred tool sets change, defeating prompt caching. Users working with MCP tools are directly affected. [Issue](https://github.com/QwenLM/qwen-code/issues/4777)

4. **#4814** – UI should make it easier for Custom Provider users to add new models  
   After initial setup, adding a new model requires manual editing of `settings.json`. Several users want a guided dialog. [Issue](https://github.com/QwenLM/qwen-code/issues/4814)

5. **#4813** – `modelProviders`: shared `baseUrl` cannot be set once for multiple models  
   Configuration duplication frustrates users running local servers or third‑party providers that share endpoints. [Issue](https://github.com/QwenLM/qwen-code/issues/4813)

6. **#4801** – Add a dedicated `web_search` tool  
   The current `web_fetch` only retrieves specific URLs; users want a tool that performs actual web search queries. [Issue](https://github.com/QwenLM/qwen-code/issues/4801)

7. **#4807** – `desktop-pet` skill for custom pixel-art companions  
   A playful feature request to generate a floating desktop companion from any user‑named character. [Issue](https://github.com/QwenLM/qwen-code/issues/4807)

8. **#4805** – Enable merge queue or require up-to-date branches to prevent stale CI merges  
   PRs with outdated CI checks can introduce semantic breakage. The community asks for branch‑protection hardening. [Issue](https://github.com/QwenLM/qwen-code/issues/4805)

9. **#4794** – Compact mode tool merge causes full-screen flash on every tool batch  
   A UI regression where `compactToolGroups` shrinks history entries, causing Ink to re‑render the entire screen. Users report the flash is jarring. [Issue](https://github.com/QwenLM/qwen-code/issues/4794)

10. **#4748** – Optimize daemon cold start latency (2.5s → ~1.5s)  
    A performance enhancement tracked alongside the daemon mode feature; warm sessions are fast, but the initial boot still trails the CLI. [Issue](https://github.com/QwenLM/qwen-code/issues/4748)

## Key PR Progress
1. **#4820** – `feat(serve): add HTTP rewind endpoints for daemon/web-shell`  
    Adds `GET /session/:id/rewind/snapshots` and `POST /session/:id/rewind`. Enables remote session rewinding without the TUI dialog. [PR](https://github.com/QwenLM/qwen-code/pull/4820)

2. **#4812** – `feat(serve): add POST /session/:id/branch for session forking`  
    Allows programmatic branching of live sessions via HTTP, useful for IDE extensions and web shells. [PR](https://github.com/QwenLM/qwen-code/pull/4812)

3. **#4787** – `ci(triage): Fix Qwen triage workflow prompt`  
    Repairs the CI triage bot that was posting broken comments mid‑execution. Uses direct skill invocation. [PR](https://github.com/QwenLM/qwen-code/pull/4787)

4. **#4819** – `feat(cli): enable /remember, /forget, /dream in ACP mode`  
    Opens up memory slash commands for web‑shell clients by adding `supportedModes` declarations. [PR](https://github.com/QwenLM/qwen-code/pull/4819)

5. **#4798** – `fix(core): inject current date on every user query`  
    Prevents stale temporal context in long-running sessions by refreshing the date on each turn. [PR](https://github.com/QwenLM/qwen-code/pull/4798)

6. **#4799** – `feat(web-shell): add daemon dev launcher`  
    A single command starts the local daemon and web-shell dev server together, simplifying the development workflow. [PR](https://github.com/QwenLM/qwen-code/pull/4799)

7. **#4816** – `feat(serve): add /settings slash command for web-shell`  
    Full‑stack `/settings` support including daemon API routes, React hooks, and a keyboard‑navigable settings panel. [PR](https://github.com/QwenLM/qwen-code/pull/4816)

8. **#4563** – `refactor(serve): extract DaemonWorkspaceService from AcpSessionBridge`  
    Separates workspace‑level operations from session‑specific ones, preparing for the daemon mode feature batch. [PR](https://github.com/QwenLM/qwen-code/pull/4563)

9. **#4736** – `feat(serve): ACP/REST parity wave 1 — session extensions + memory + files + auth (20 methods)`  
    Adds 20+ `_qwen/*` extension methods to the ACP transport, achieving near‑complete REST parity. [PR](https://github.com/QwenLM/qwen-code/pull/4736)

10. **#4490** – `feat(daemon): merge daemon-mode feature batch into main`  
    A large integration merge bringing 46 commits (386 files, +115k/−12k LOC) that form the core daemon mode for v0.16‑alpha. [PR](https://github.com/QwenLM/qwen-code/pull/4490)

## Feature Request Trends
- **Multimodal model support**: Multiple issues (#4802, #4803) call for proper handling of image/video input for `qwen3.7-plus` and other Plus/Max variants.
- **Web search tool**: Users want a genuine search engine integration rather than fetching fixed URLs (#4801).
- **Better custom provider UX**: Adding and configuring models for custom/third‑party providers needs a UI wizard (#4814, #4813).
- **Session and daemon features**: Branching, rewind, and slash commands in web‑shell are highly requested (#4514, #4809, #4819).
- **Skills and desktop enhancements**: A skills picker dialog (#4532) and desktop‑pet skill (#4807) reflect interest in richer interactive experiences.

## Developer Pain Points
- **Out‑of‑memory crashes**: Recurring OOM issues (#4815, #4167, #2982 etc.) especially after resume or long sessions, often linked to `structuredClone` or prompt cache bloat.
- **Slash commands blocked in ACP mode**: 13 CLI slash commands are rejected in web‑shell because they lack `supportedModes: ['acp']` (#4809).
- **Stale CI merges**: PRs can land with green checks that are out of date, introducing silent breaking changes (#4805).
- **Configuration duplication**: `baseUrl` must be repeated for each model even when they share an endpoint (#4813).
- **Flaky UI rendering**: Tool merge in compact mode causes full‑screen flicker (#4794).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-06

## Today’s Highlights
**CodeWhale** (formerly the DeepSeek TUI project) is now clearly under its new identity, with **v0.9.0** development accelerating rapidly. The most significant news today: **the official VS Code extension scaffold has landed** (PR #2811), marking a major milestone for GUI-bound users. Meanwhile, **WhaleFlow — the declarative multi-agent workflow runtime** (PR #2482) — continues to mature, with cost tracking now merging. The community is actively porting to HarmonyOS, and seven issues were closed in the last 24 hours.

## Releases
No new releases in the last 24 hours. The latest stable remains **v0.8.53**.

## Hot Issues (10 picks)

1. **#2766 — UI refactor needed**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2766)  
   The output-copying workflow is broken, and confirmation popups hide crucial UI content. With 8 comments, this is the most active issue — a clear UX priority for v0.9.0.

2. **#1264 — VS Code plugin request**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1264)  
   A long-standing Chinese-language request for OpenCode-like VS Code integration. The PR #2811 directly addresses this, so closure is imminent.

3. **#2621 — Xiaomi MiMo Token Plan API**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2621)  
   Community wants Codewhale to support Xiaomi's new subscription-based Token Plan model (Lite/Standard/Pro/Max), not just pay-as-you-go. 4 comments, active discussion.

4. **#2791 — Refactor command dispatch strategy**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2791)  
   A 200-line monolithic match block in `commands/mod.rs` needs refactoring. This is a maintainability concern for contributors adding new commands.

5. **#2625 — Port to HarmonyOS**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2625)  
   A direct porting effort to OpenHarmony/HarmonyOS Next. The build fails at the `rustyline -> nix` dependency chain due to an ioctl type mismatch. PR #2634 is now open.

6. **#2574 — Provider fallback chain**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2574)  
   Automatic failover between providers on 401/429/5xx errors. The feature request is clear, and PR #2773 is now implementing it. High demand: 3 comments.

7. **#2086 — Contribution gate workflow**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2086)  
   Proposes an allowlist-based PR/issue gating mechanism to reduce maintainer overhead. Relevant as the project scales its contributors.

8. **#2709 — Hugging Face MCP and Hub integration**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2709)  
   Part of v0.9.0 roadmap. Aims to make Hugging Face's MCP server and Hub tools discoverable within CodeWhale. 1 comment, high strategic value.

9. **#2694 — Sidebar detail popovers**  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2694)  
   Sidebar rows (Work/Tasks/Agents) are truncated on narrow terminals. Users want inspectable popovers. Important for daily TUI usability.

10. **#2643 — Release publish recovery checklist**  
    [Link](https://github.com/Hmbown/CodeWhale/issues/2643)  
    The v0.8.51/v0.8.52 release process was messy — this proposes an actionable checklist for Cargo crates, npm packages, and GitHub Release assets.

## Key PR Progress (10 picks)

1. **#2811 — feat(vscode): add local runtime extension scaffold**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2811)  
   **Merged.** Phase 0 VS Code extension with commands to open CodeWhale, start `codewhale serve --http`, and check runtime status. Includes VSIX packaging.

2. **#2634 — feat: porting to HarmonyOS**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2634)  
   **Merged.** Makes the repo compilable on HarmonyOS/OpenHarmony with conditional platform gates. Lays groundwork for official ARM OHOS support.

3. **#2482 — feat: add WhaleFlow declarative multi-agent orchestration**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2482)  
   **Open.** New `crates/whaleflow` with JSON-driven workflow config, topological scheduler, and concurrency control. Large PR with high impact.

4. **#2773 — feat(provider): complete provider fallback chain**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2773)  
   **Open.** Implements #2574 — automatic retryable-error fallback across providers. Configurable via `fallback_providers` in `config.toml`.

5. **#2256 — refactor: consolidate workspace crates 14→11**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2256)  
   **Merged.** Deleted orphaned `tui-core`, merged hooks+agent crates. Zero behavioral change — a healthy cleanup.

6. **#2639 — feat(api): add POST /v1/sessions endpoint**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2639)  
   **Merged.** Saves threads as sessions for cross-workspace resumption. Enables the VS Code extension to persist conversations.

7. **#2113 — feat(tui): independent scroll regions**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2113)  
   **Merged.** Chat and tool output now scroll independently. Mouse wheel events are handled per-region.

8. **#2520 — feat(client): cross-session prompt base cache**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2520)  
   **Merged.** Caches immutable system-prompt base section on disk — improves KV-cache reuse and session-start latency.

9. **#2486 — feat(whaleflow): cost tracking data model**  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2486)  
   **Open.** Adds `tokens_used` and `cost_usd` fields to `SubAgentResult`. Critical for WhaleFlow cost transparency.

10. **#2780 — feat(tui): add HF_BASE_UR and HF_MODE env support**  
    [Link](https://github.com/Hmbown/CodeWhale/pull/2780)  
    **Merged.** TUI now respects environment variables for Hugging Face base URL and model selection.

## Feature Request Trends

1. **VS Code / IDE Integration (Dominant trend)** — Issues #1264, #2580, #461 are all variations of the same ask: CodeWhale needs a graphical IDE companion. The v0.9.0 extension scaffold (#2811) directly addresses this demand.

2. **Multi-provider strategy** — Two distinct asks: automatic failover (#2574) and support for new pricing models like Xiaomi Token Plans (#2621). Users want flexibility without manual switching.

3. **MCP / API extensibility** — Issues #2621, #2580, #2709 all touch on MCP or API-level integration. The Hugging Face MCP Hub integration (#2709) is the most strategically important.

4. **Cross-platform compatibility** — HarmonyOS porting (#2625) and VS Code agent-view adaptation (#2580) represent a push beyond Linux/macOS boundaries.

5. **Accessibility & usability** — Custom notification sounds (#2484) and sidebar popovers (#2694) are quality-of-life requests from engaged users.

## Developer Pain Points

- **Multi-provider configuration friction** — Users find switching providers manually disruptive (#2574, #1874). The auto-fallback chain is a clear demand.

- **API endpoint incompatibility** — Third-party OpenAI-compatible APIs sometimes use `/chat/completions` instead of `/v1/chat/completions`. Multiple issues (#1874, #2735) request configurable endpoint paths.

- **UI/UX gaps in TUI** — Copying output is hard (#2766), scrolling isn't region-aware (#2113), and the sessions CLI incorrectly suggests `--resume` as a top-level flag (#2758). These are low-effort fixes with high user impact.

- **Debugging and observability** — Error messages are too generic (#2665). Users want to see provider endpoints and key sources in auth errors, especially in multi-provider setups.

- **Project-level MCP config not loaded** — Users expect `.codewhale/mcp.json` to be auto-merged, but only global config is read (#2749). This breaks project-specific tool setups.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*