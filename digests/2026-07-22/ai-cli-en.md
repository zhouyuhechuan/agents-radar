# AI CLI Tools Community Digest 2026-07-22

> Generated: 2026-07-22 01:56 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem — Cross-Tool Comparison Report
**Date:** 2026-07-22  
**Analyst:** Senior Technical Analyst, AI Developer Tools

---

## 1. Ecosystem Overview

The AI CLI tools landscape is entering a **stabilization-and-maturity phase**, characterized by intense competition on reliability, platform parity, and enterprise readiness. Most tools have shipped significant feature releases in the past 72 hours—Claude Code v2.1.217, OpenAI Codex v0.145.0, Gemini CLI nightly security patches, Pi v0.81.x, and Qwen Code v0.20.1—while GitHub Copilot CLI and Kimi Code CLI move more conservatively. A **shared pain point across all tools is Windows stability**, with every major project reporting multiple critical platform-specific regressions. Meanwhile, **sub-agent orchestration, MCP ecosystem integration, and session persistence** have emerged as the three dominant competitive battlegrounds, with each tool taking distinct architectural approaches. The community signal is clear: developers value reliability and cross-platform consistency over feature velocity, and those tools that fail to address foundational stability will see user trust erode rapidly.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Active PRs (24h) | Release Status | Notable Release (Today) |
|---|---|---|---|---|
| **Claude Code** | 50 updated (10 selected) | 13 updated (10 selected) | ✅ Released | v2.1.217 (emoji autocomplete, transcript warnings) |
| **OpenAI Codex** | Not fully enumerated (10 selected) | 10 selected | ✅ Released | v0.145.0 (paginated threads, `/import` expansion) |
| **Gemini CLI** | 10 selected | 10 selected | ⚠️ Nightly | v0.52.0-nightly (critical RCE fix) |
| **GitHub Copilot CLI** | 10 selected | None in 24h | ✅ Released | v1.0.74-0 (`/model plan` command) |
| **Kimi Code CLI** | 5 total | 1 total | ❌ No release | — |
| **OpenCode** | 10 selected | 10 selected | ❌ No release | — |
| **Pi** | 10 selected | 10 selected | ✅ 2 releases | v0.81.1 (source archives), v0.81.0 (llama.cpp) |
| **Qwen Code** | 10 selected | 10 selected | ✅ Released | v0.20.1 (autofix takeover, CUA driver) |
| **DeepSeek TUI (CodeWhale)** | 10 selected | 10 selected | ⚠️ Pre-release | v0.9.1 finalizing (integration PR #4675) |

**Key Observations:**
- **High-velocity cluster:** Pi, DeepSeek TUI, Qwen Code, and OpenCode show the highest PR throughput
- **Conservative cluster:** GitHub Copilot CLI and Kimi Code CLI show minimal release activity
- **Stable releases today:** Claude Code, OpenAI Codex, GitHub Copilot CLI, Pi, Qwen Code
- **Nightly/pre-release:** Gemini CLI (security fix), DeepSeek TUI (v0.9.1 RC)
- **Sub-agent model mutation:** Appears across Qwen Code (P1), OpenAI Codex (#28058), Gemini CLI (#22323), and Claude Code (#75757) — indicating a systemic challenge

---

## 3. Shared Feature Directions

The following requirements appear **across multiple tool communities**, suggesting strong market demand:

### 3.1 MCP Ecosystem Completeness
- **Tools affected:** Claude Code, GitHub Copilot CLI, Kimi Code CLI, DeepSeek TUI, OpenCode
- **Specific needs:**
  - MCP resource/subscription support beyond tools (Copilot #1518, Claude Code implicit demand)
  - OAuth/token-based MCP authentication (Copilot #1305, Pi #6927)
  - Schema validation against provider-specific JSON Schema flavors (Kimi #2531, DeepSeek TUI #4613)
  - Silent token refresh and mid-turn tool list consistency (Copilot #4203, #3125)
  - MCP tool call reliability across platforms (Claude Code #79992 macOS silent drops)

### 3.2 Sub-Agent Reliability & Auditability
- **Tools affected:** All major tools
- **Specific needs:**
  - False success reporting when sub-agents hit turn limits (Gemini #22323, Qwen Code #7156)
  - Spend limit bypass during sub-agent execution (Claude Code #75757, OpenCode #37790/#38195)
  - Encrypted sub-agent payloads breaking audit trails (Codex #28058, 99👍)
  - Session state mutation by sub-agents (Qwen Code #7156 — P1, Gemini #21968)
  - Background agent roster persistence on session restore (Qwen Code #7459, Copilot #2595)

### 3.3 Windows Platform Parity
- **Tools affected:** Claude Code, OpenAI Codex, GitHub Copilot CLI, Pi, DeepSeek TUI, Qwen Code, OpenCode
- **Specific needs:**
  - Update mechanisms that don't brick the app (Claude #76357, Codex #32149)
  - Process cleanup / orphan prevention (Codex #34260, Copilot #4163, DeepSeek TUI)
  - Fullscreen scrollbar and rendering issues (Claude #72215)
  - Path separator handling for `find`/glob (Pi #6817)
  - WSL sidecar integration stability (OpenCode #37481, Codex)
  - Slow cold-start on Windows (Claude #79999)
  - Numpad key event handling (Kimi #2529)

### 3.4 Session & Context Management
- **Tools affected:** Claude Code, OpenAI Codex, GitHub Copilot CLI, Pi, Qwen Code, OpenCode, DeepSeek TUI
- **Specific needs:**
  - Paginated thread history with efficient resume (Codex v0.145.0, Qwen Code #7302 @mention)
  - Auto-compaction that prevents provider overflow (Pi #6879, Copilot #4183)
  - Session freeze/deadlock resolution (Claude Code #79921, Codex)
  - Cost transparency per sub-agent (Copilot #4207)
  - Session naming and organization (OpenCode #38163, Claude Code)

### 3.5 Token & Authentication Infrastructure
- **Tools affected:** Claude Code, OpenAI Codex, OpenCode, Pi, Qwen Code
- **Specific needs:**
  - Deterministic rate-limit resets (Codex #9508, 31👍)
  - Long-lived token support for headless/CI usage (Claude Code #79360)
  - Bearer token persistence across page refreshes (Qwen Code #7301)
  - Subscription state synchronization (OpenCode #37790 cluster)
  - Provider credential rotation and fallback (Gemini CLI #28472)

### 3.6 Local/First-Party Model Support
- **Tools affected:** Pi, Gemini CLI, Kimi Code CLI, Qwen Code, OpenCode
- **Specific needs:**
  - Local model management via llama.cpp (Pi v0.81.0)
  - AST-aware file reads to reduce token waste (Gemini #22745)
  - Dynamic model discovery from OpenAI-compatible providers (OpenCode #6231, 182👍)
  - Self-hosted model output limit configuration (DeepSeek TUI #4656)
  - Model affinity through zero-dependency sandboxing (Gemini #19873)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | Pi | OpenCode | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|---|
| **Core Differentiator** | Enterprise MCP ecosystem + Plugin framework | Sub-agent memory + `/import` migration | Security-first + A2A server | GitHub ecosystem integration | Moonshot API compatibility | Local model (llama.cpp) + verifiable builds | Multi-provider flexibility + layout options | CUA driver + cron/AI scheduler | Sub-agent orchestration + permission contracts |
| **Target User** | Enterprise devs, CI/CD heavy users | Multi-agent power users | Security-conscious teams | GitHub-centric workflows | Chinese market, Moonshot users | Privacy-focused, local-first | Open-source community, provider-agnostic | Qwen ecosystem, web shell users | Heavy automation, agent coordination |
| **Technical Approach** | Plugin/hookify framework + transcript persistence | Rust rewrite + encrypted MultiAgentV2 | Nightly security patches + evals | Slow, deliberate releases | Minimal feature set, bug-focused | Fast release cycle + community contribution | Middleware-style provider abstraction | Autofix/takeover + daemon channels | Permission contracts + truthful UI |
| **Community Model** | Active but structured | High-engagement, vocal | Engineering-focused | Measured, enterprise | Small, bug-report heavy | Fast triage + community PRs | Feature request intensive | Coordinated, CI-heavy | High-velocity community contributions |
| **Platform Weakness** | macOS MCP drops, Windows stability | Windows process storms, macOS Crashpad | Wayland browser agent, shell hangs | Linux zombies, MCP reliability, tmux | MCP schema validation, k2.5 model | Windows path issues, dependency duplication | WSL crashes, Windows ARM64 TUI | Windows stability, token persistence | Enter-key freeze, provider config |

### Key Strategic Differences:

1. **Plugin/Hook Architecture:** Claude Code leads with the most mature plugin framework (hookify), while Pi and DeepSeek TUI are catching up with extension APIs and AgentHarness abstractions. OpenAI Codex and Copilot CLI offer less extensibility.

2. **Agent Coordination Models:** 
   - DeepSeek TUI is pioneering **permission contracts and neutral fan-in** for parallel agent work
   - OpenAI Codex leads on **sub-agent memory and paginated session history**
   - Qwen Code has **CUA driver with relative coordinates** for UI automation
   - Gemini CLI takes a **security-first approach** with workspace trust and task isolation

3. **Local Model Strategy:** 
   - Pi has the most advanced local LLM support (llama.cpp management, Hugging Face integration)
   - Qwen Code, Kimi Code, and OpenCode focus on provider compatibility
   - Claude Code, Codex, and Copilot are cloud-only

4. **Release Philosophy:**
   - Pi and DeepSeek TUI ship frequently with community contributions
   - Claude Code and Codex ship stable releases with regression risk
   - Gemini CLI uses nightly channels for security fixes
   - Copilot CLI ships slowly — reliability over velocity

5. **Sandbox/Security:**
   - Gemini CLI has the strongest security posture (RCE fix, variable expansion hardening)
   - Codex and Copilot are addressing sandbox regressions (bubblewrap, Windows job objects)
   - Claude Code sandbox regressions (#79606, #79997) show fragility

---

## 5. Community Momentum & Maturity

| Tool | Community Activity | Iteration Velocity | Issue Closure | Maturity Level |
|---|---|---|---|---|
| **Claude Code** | 🔥 High (50 issues/13 PRs today) | Moderate (stable releases) | Moderate — critical bugs persist | ✅ Mature but fragile |
| **OpenAI Codex** | 🔥 High (#28058: 99👍, 26 comments) | High (v0.145.0 with alpha track) | Good — multiple regressions fixed | ✅ Mature (Rust rewrite) |
| **Gemini CLI** | 🔥 High (security fix community engaged) | Very High (daily nightlies) | Good — fast security patches | 🔄 Growth phase |
| **GitHub Copilot CLI** | 🟡 Moderate (MCP issues dominate) | Low (minor release today) | Slow — critical bugs unresolved | ✅ Mature but slow iteration |
| **Kimi Code CLI** | 🔴 Low (5 issues, 1 PR) | Very Low (no release) | Poor — small team | 🟠 Early stage |
| **OpenCode** | 🔥 High (119 comments on mem megathread) | High (10 PRs today) | Good — active PR pipeline | 🔄 Growth phase |
| **Pi** | 🔥 Very High (2 releases + 10 PRs today) | Very High (multiple daily releases) | Excellent — fast triage, crash bugs closed same day | 🔄 Growth phase |
| **Qwen Code** | 🟡 Moderate (10 issues/10 PRs) | High (v0.20.1 + previews) | Good — P1 bugs closed quickly | 🔄 Growth phase |
| **DeepSeek TUI** | 🔥 Very High (20+ blockers closed, 10 PRs daily) | Very High (v0.9.1 finalizing) | Excellent — 20+ blocker closure in one day | 🔄 Pre-mature (v0.9.1) |

### Community Maturity Assessment:

- **Mature Leaders:** Claude Code, OpenAI Codex, GitHub Copilot CLI — established user bases, stable APIs, but wrestling with platform-specific regressions
- **Fastest Iteration:** Pi, DeepSeek TUI — shipping multiple releases daily with strong community contribution models
- **Highest Engagement per Issue:** OpenAI Codex (#28058: 99👍) and OpenCode (#20695: 119 comments, 90👍) — indicate deeply invested user bases
- **Most Fragile at Scale:** Claude Code (5 regression/blocker issues simultaneously) and Copilot CLI (unresolved zombie processes, MCP failures)
- **Best Triage Response:** Pi — 3 crash bugs filed and closed within hours of v0.81.0 release
- **Most Coordinated Release:** DeepSeek TUI — closing 20+ release-blocker issues in a single day before v0.9.1

---

## 6. Trend Signals

### 6.1. MCP Is Table Stakes, Not a Moat
Every major tool now supports MCP, but **the competitive differentiation is moving toward MCP reliability and completeness**. Claude Code's silent macOS MCP drops (#79992), Copilot's connection failures (#2282), and Kimi's schema rejection (#2531) show that basic connectivity is still broken. The next frontier: **MCP resource subscriptions, OAuth support, and tool list consistency** (Copilot #1518, #4203). Developers evaluating tools should audit MCP reliability on their target platforms before committing.

### 6.2. Windows Is the Min-Platform; Linux Dominates for Power Users
The data is stark: **every single tool** has critical Windows-specific bugs. Claude Code's MSIX update bricking (#76357), Codex's 500+ orphan `taskkill.exe` processes (#34260), Pi's broken `find` tool (#6817), and OpenCode's WSL crash (#37481) make Windows a second-class experience. Meanwhile, Linux sandboxing (bubblewrap) and Wayland compatibility (Gemini #21983) are also fragile. **macOS remains the most reliable platform across all tools**, though Crashpad dumps (Codex #25921, +5GB/day) and MCP drops (Claude Code #79992) show it's not immune.

### 6.3. Sub-Agent Reliability Is the #1 Trust Builder
False success reporting, spend limit bypasses, and session state corruption by sub-agents are **the most dangerous category of bug** because they undermine trust without immediate visibility. A sub-agent that silently changes a model (Qwen Code #7156, P1), reports "success" after turn limits (Gemini #22323), or continues billing after spend limits (Claude Code #75757) erodes user confidence. Tools that prioritize sub-agent observability (OpenAI Codex's paginated history, DeepSeek TUI's truthful work queues, Pi's compaction retry policy) will win long-term trust.

### 6.4. The Local Model Renaissance Is Real
Pi's llama.cpp integration and OpenCode's auto-discovery request (182👍) signal **strong demand for hybrid cloud/local workflows**. Developers want to run local models for privacy, latency, and cost control, but need seamless integration with cloud models for complex tasks. Tools that bridge this gap (Pi, Gemini 3's native bash affinity in #19873) will capture the privacy-conscious segment.

### 6.5. Predictability Beats Features
OpenAI Codex's #9508 (deterministic rate-limit resets, 31👍), Claude Code's spend limit bypass (#75757), and Copilot's background agent completion retention (#2595) all point to a single truth: **developers value predictable, auditable behavior over new features**. The most upvoted features across all tools are about reliability, transparency, and control—not AI capabilities

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-07-22 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Pull Requests represent the most-discussed Skill submissions. All remain **Open** unless noted.

### #1 — Fix: `run_eval.py` reports 0% recall across all queries
**PR [#1298](https://github.com/anthropics/skills/pull/1298)** by MartinCajiao
- **Functionality:** Repairs the skill-creator's evaluation pipeline (`run_eval.py`) which silently reported `recall=0%` for every skill description (#556, 10+ independent reproductions). Fixes include: installing eval artifacts as real skills, Windows stream reading, trigger detection, and parallel worker handling.
- **Discussion highlights:** This is the third major attempt to fix the `run_eval` recall bug. The issue (#556) has 12 comments and 7 👍. Multiple community members confirmed independent reproduction across platforms.
- **Status:** Open (created 2026-06-10, updated 2026-06-23)

### #2 — Add `document-typography` skill
**PR [#514](https://github.com/anthropics/skills/pull/514)** by PGTBoos
- **Functionality:** Typographic quality control for AI-generated documents — prevents orphan word wrap, widow paragraphs, and numbering misalignment. Targets a universal pain point in Claude-generated documents.
- **Discussion highlights:** Zero explicit PR comments (the system sorts by total issue+PR engagement), but the linked issue ecosystem around document quality (#189, duplicate skill concerns) suggests broad interest.
- **Status:** Open (created 2026-03-04, updated 2026-03-13)

### #3 — Add `testing-patterns` skill
**PR [#723](https://github.com/anthropics/skills/pull/723)** by 4444J99
- **Functionality:** Comprehensive testing stack coverage — Testing Trophy philosophy, AAA pattern unit tests, React Testing Library guidance, E2E with Playwright. Covers unit, integration, component, and end-to-end testing patterns.
- **Discussion highlights:** Addresses a clear gap in the skills collection. No explicit PR blockers noted.
- **Status:** Open (created 2026-03-22, updated 2026-04-21)

### #4 — Add `pyxel` skill (retro game development)
**PR [#525](https://github.com/anthropics/skills/pull/525)** by kitao
- **Functionality:** Integration with Pyxel retro game engine. Covers MCP server workflow: write → run_and_capture → inspect → iterate. Targets pixel-art/8-bit game creation with Python.
- **Discussion highlights:** Author is the Pyxel engine maintainer. Skill bridges creative coding and game development. No significant objections; likely to land.
- **Status:** Open (created 2026-03-05, updated 2026-07-15)

### #5 — Add `self-audit` skill (v1.3.0)
**PR [#1367](https://github.com/anthropics/skills/pull/1367)** by YuhaoLin2005
- **Functionality:** Two-stage AI output auditing: (1) mechanical file verification, (2) four-dimension reasoning audit in damage-severity priority order. Universal across projects and tech stacks.
- **Discussion highlights:** Part of a broader "reasoning quality gate" proposal (#1385) with 3 comments. Represents growing community concern about output quality verification.
- **Status:** Open (created 2026-06-28, updated 2026-07-02)

### #6 — Add ODT skill (OpenDocument text)
**PR [#486](https://github.com/anthropics/skills/pull/486)** by GitHubNewbie0
- **Functionality:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods). Covers LibreOffice/ISO standard document production, template filling, and ODT-to-HTML conversion.
- **Discussion highlights:** Addresses enterprise demand for open-source document formats. No major blocking issues.
- **Status:** Open (created 2026-03-01, updated 2026-04-14)

### #7 — Improve `frontend-design` skill
**PR [#210](https://github.com/anthropics/skills/pull/210)** by justinwetch
- **Functionality:** Revises the frontend-design skill for clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation with specific, behavior-steering guidance.
- **Discussion highlights:** Exemplifies the community's focus on skill quality over quantity. Addresses the "verbose educational tone" problem identified in issue #202.
- **Status:** Open (created 2026-01-05, updated 2026-03-07)

---

## 2. Community Demand Trends

From the top Issues (sorted by engagement), five concentrated demand directions emerge:

### 🔴 Critical Pipeline Reliability (Issue #556 — 12 comments, 7 👍)
The `run_eval.py` recall bug is the community's most acute pain point. Multiple contributors (#1298, #1099, #1050, #1323, #362, #361) have submitted fixes, but the issue persists across Windows and macOS environments. **Demand:** Stable, cross-platform skill evaluation tooling.

### 🔴 Security & Trust Boundary (Issue #492 — 43 comments, 2 👍)
Community skills distributed under the `anthropic/` namespace create impersonation risk. The reporter documented a comprehensive compromise scenario involving `fs-read`, `bash-exec`, `computer-use-alice`, and `stealth-memory`. **Demand:** Namespace separation, verification badges, or security audit requirements for community skills.

### 🟡 Enterprise Skill Sharing (Issue #228 — 14 comments, 7 👍)
Users want org-wide skill distribution without manual file sharing. Current workflow (download → Slack → Settings → Capabilities → Upload) is friction-heavy. **Demand:** Shared skill libraries or direct sharing links within Claude.ai.

### 🟡 Agent Governance & Safety (Issue #412 — 6 comments)
Proposal for governance patterns: policy enforcement, threat detection, trust scoring, audit trails. **Demand:** Skills that teach Claude how to build safe AI agent systems.

### 🟡 Memory Optimization (Issue #1329 — 9 comments)
Proposal for a `compact-memory` skill using symbolic notation to reduce context overhead for long-running agents. **Demand:** Skills that optimize Claude's own operational efficiency.

### 🟡 Deduplication & Plugin Management (Issue #189 — 6 comments, 9 👍)
`document-skills` and `example-skills` plugins ship identical content, causing duplicates. **Demand:** Clearer plugin boundaries and deduplication logic.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are nearing merge readiness. All are **Open** with updates within the last 30 days:

| PR | Skill | Author | Last Update | Why It's Close |
|----|-------|--------|-------------|----------------|
| [#1367](https://github.com/anthropics/skills/pull/1367) | `self-audit` (reasoning quality gate) | YuhaoLin2005 | 2026-07-02 | Mechanical verification + 4-dimension audit; addresses broader #1385 proposal. Follow-up proposal suggests pipeline evolution. |
| [#1302](https://github.com/anthropics/skills/pull/1302) | `color-expert` | meodai | 2026-07-21 | Color naming systems, spaces, contrast, accessibility. Recently updated (7 days ago). |
| [#525](https://github.com/anthropics/skills/pull/525) | `pyxel` (retro game dev) | kitao | 2026-07-15 | Author is project maintainer; strong domain authority. |
| [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` | 4444J99 | 2026-04-21 | Addresses clear community gap; comprehensive test pyramid coverage. |
| [#514](https://github.com/anthropics/skills/pull/514) | `document-typography` | PGTBoos | 2026-03-13 | Universal document quality issue; low risk, high value. |

**Watch also:** The `skill-creator` fix train (#1298, #1099, #1050, #1323) — any single successful merge will likely unblock the entire evaluation pipeline.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliability tooling* — skills that fix, audit, verify, or secure the output of both Claude and the skill development pipeline itself — rather than for domain-specific content skills.**

The data tells a clear story: the top-engagement PRs (#1298, #1099, #1050, #1323, #362, #361) all target the `skill-creator` evaluation loop. The highest-engagement Issue (#492) is about security trust boundaries. The trend is not "I want a skill for X domain" but rather **"I want the skill system to work correctly, verifiably, and safely."**

---

# Claude Code Community Digest — 2026-07-22

## Today’s Highlights

Version **2.1.217** ships emoji autocomplete in the prompt input and warnings for transcript write failures. A critical new bug (#79992) silently drops MCP filesystem tool calls on macOS, while two sandbox regressions in 2.1.216 (#79606, #79997) break Bash on both root and non‑root installs. On the plugin side, a wave of fixes for the hookify framework addresses import, encoding, and quoting issues.

## Releases

**v2.1.217** — [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.217)
- Added emoji shortcode autocomplete (`:heart:` → ❤️, `:hea` for suggestions; disable via `emojiCompletionEnabled` setting)
- Added warnings when transcript writes are failing (e.g., disk full) or when session saving is off due to an inherit

## Hot Issues (10 of 50 updated in the last 24h)

1. **#79360 — Fable 5 gated behind usage credits on Max when using `setup-token`**  
   [Issue](https://github.com/anthropics/claude-code/issues/79360) — 30👍, 5 comments  
   _Why it matters:_ Users authenticated via long‑lived tokens on a Max plan cannot access Fable 5 because the inference‑only scope cannot read entitlements. Affects CI/CD workflows. High community demand for a fix.

2. **#54670 — [FEATURE] VSCode extension: Copy chat response as markdown source**  
   [Issue](https://github.com/anthropics/claude-code/issues/54670) — 18👍, 9 comments  
   _Why it matters:_ Users want a one‑click way to copy raw markdown from chat responses for reuse or documentation. The most upvoted feature request on this week’s radar.

3. **#72181 — Desktop app: No way to remove entries from the “Recent” folders list**  
   [Issue](https://github.com/anthropics/claude-code/issues/72181) — 10👍, 5 comments  
   _Why it matters:_ Old project folders accumulate and clutter the task composer picker. A basic UX gap that affects daily workflow.

4. **#45810 — Marketplace update button is disabled even when version is outdated**  
   [Issue](https://github.com/anthropics/claude-code/issues/45810) — 6👍, 15 comments  
   _Why it matters:_ The “Update” button is greyed out and non‑interactive, preventing plugin updates. Duplicate reports suggest it’s a persistent UI bug.

5. **#72215 — Fullscreen render mode: no scrollbar and scrolling broken on Windows**  
   [Issue](https://github.com/anthropics/claude-code/issues/72215) — 4👍, 6 comments  
   _Why it matters:_ Once output exceeds one screen, users cannot scroll at all — making long outputs inaccessible. A severe platform‑specific bug.

6. **#76357 — Windows MSIX update fails with “Another program is using this file” — app unlaunchable until reboot**  
   [Issue](https://github.com/anthropics/claude-code/issues/76357) — 4👍, 6 comments  
   _Why it matters:_ Every update bricking Claude Desktop until the next reboot is a showstopper for Windows users.

7. **#79992 — macOS: filesystem‑class MCP tool calls silently dropped**  
   [Issue](https://github.com/anthropics/claude-code/issues/79992) — 0👍, 3 comments (filed 2026‑07‑22)  
   _Why it matters:_ New critical bug: tools pass the approval gate but never reach the local MCP server. Persists across rollbacks/reinstalls. Coordination‑heavy debugging ongoing.

8. **#79921 — Sessions freeze locally until another session receives input (Desktop & VS Code only)**  
   [Issue](https://github.com/anthropics/claude-code/issues/79921) — 0👍, 3 comments  
   _Why it matters:_ A nondeterministic deadlock that affects multi‑session power users. The Web UI is unaffected, suggesting a client‑side IPC issue.

9. **#75037 — Background agent sessions: fast termination, crash‑loop on attach, lost completion records**  
   [Issue](https://github.com/anthropics/claude-code/issues/75037) — 0👍, 3 comments  
   _Why it matters:_ Reported together as three distinct bugs in `claude --bg` / `claude agents` workflows. Background agents are a core CI feature; reliability is paramount.

10. **#75757 — Subagents billed after monthly spend limit exceeded; false clean review on agent failures**  
    [Issue](https://github.com/anthropics/claude-code/issues/75757) — 0👍, 3 comments  
    _Why it matters:_ Billing integrity issue — subagents continue to consume credits after a spend limit is hit, and the review result is incorrectly reported as “clean”.

## Key PR Progress (10 of 13 updated in the last 24h)

1. **#79898 — Add Claude Apps Gateway on AWS example deployment assets**  
   [PR](https://github.com/anthropics/claude-code/pull/79898) — Closed  
   _Deploy reference for Claude Apps Gateway with Amazon Bedrock. Sibling to the existing GCP examples._

2. **#79889 — fix(hookify): make hook entrypoints runnable without `CLAUDE_PLUGIN_ROOT`**  
   [PR](https://github.com/anthropics/claude-code/pull/79889) — Open  
   _Silent skip of `sys.path` insertion when the env var is missing broke hook scripts. Now path setup is unconditional._

3. **#79873 — fix(hookify): `event: prompt` rules never fire (payload key is `prompt`)**  
   [PR](https://github.com/anthropics/claude-code/pull/79873) — Open  
   _Rules for `UserPromptSubmit` never matched because the code looked for `user_prompt` instead of `prompt`. Fixes a dead feature._

4. **#78532 — gateway/gcp: optional internal ALB + PG16 Cloud SQL edition fix**  
   [PR](https://github.com/anthropics/claude-code/pull/78532) — Open  
   _Fixes failing `terraform apply` on PG16 due to default `ENTERPRISE_PLUS` tier rejection of shared‑core machines. Adds docs for internal ALB._

5. **#79647 — fix(hookify): resolve imports independent of the plugin directory name**  
   [PR](https://github.com/anthropics/claude-code/pull/79647) — Open  
   _Fixes #69665: imports like `from hookify.core.config_loader` broke when the plugin folder wasn’t literally named `hookify`._

6. **#79645 — fix(hookify): read rule and transcript files as UTF‑8**  
   [PR](https://github.com/anthropics/claude-code/pull/79645) — Open  
   _Encoding root cause of #77270: on Windows `cp1252` cannot decode shipped UTF‑8 example files containing arrows/emoji. Explicit UTF‑8 read._

7. **#79644 — fix: quote `${CLAUDE_PLUGIN_ROOT}` in plugin hook commands**  
   [PR](https://github.com/anthropics/claude-code/pull/79644) — Open  
   _Fixes #78490: macOS `Application Support` path contains a space; unquoted variable caused shell word‑splitting and hook failure._

8. **#79643 — docs(commit-commands): align `/commit-push-pr` description with behavior**  
   [PR](https://github.com/anthropics/claude-code/pull/79643) — Open  
   _The command injects only `git status`, `git diff HEAD`, and `git branch --show-current`, not full branch history. Docs now match reality._

9. **#79640 — fix(ralph-wiggum): use `disable-model-invocation` to keep commands user‑only**  
   [PR](https://github.com/anthropics/claude-code/pull/79640) — Open  
   _The plugin used an undocumented frontmatter key (`hide-from-slash-command-tool`); switched to the official `disable-model-invocation` key._

10. **#79620 — feat: Add text‑to‑speech read‑aloud hook for accessibility**  
    [PR](https://github.com/anthropics/claude-code/pull/79620) — Open  
    _Implements a TTS hook (Piper/say/PowerShell) that reads assistant responses aloud, with markdown‑aware extraction and code‑skip heuristics. Addresses #79542._

## Feature Request Trends

- **History & folder management** – Requests to delete recent folder entries (#72181) and hide the weekly usage indicator (#79994) show a growing desire for personalization of the task composer and prompt area.
- **Chat formatting output** – “Copy as markdown” (#54670) and better clipboard controls remain the top unmet UX need.
- **Accessibility** – The TTS read‑aloud hook (#79620) and general keyboard‑navigation improvements are gaining traction.
- **Developer self‑documentation** – A community “show & tell” (#79818) demonstrates teaching Claude Code to auto‑log its own work to a self‑hosted issue tracker, hinting at demand for built‑in session continuity tools.

## Developer Pain Points

- **Windows reliability** – Update bricking (#76357), fullscreen scroll breakage (#72215), and extremely slow cold‑start (#79999) make Windows a second‑class platform.
- **Sandbox regressions in v2.1.216** – Two separate issues (#79606 for root installs, #79997 for non‑root) broke Bash tool execution due to stricter `--cap-drop ALL` defaults. Temporarily blocked many users.
- **Background agent instability** – Sessions crash‑loop (#75037), spend limit bypass (#75757), and subagent 8000‑token caps (#78460) undermine CI/background workflows.
- **MCP infrastructure fragility** – Tool calls silently dropped on macOS (#79992), session freezes tied to input focus (#79921), and unrecoverable 1M‑context compaction (#74544) show transport‑layer reliability gaps.
- **Plugin/hook framework friction** – Intermittent skill resolution (#75224), encoding issues on Windows (#79645), and silent hook failures due to path quoting (#79644) and import structure (#79647) add friction for plugin developers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-22

## Today's Highlights
The `0.145.0` stable release landed today with experimental paginated thread history, sub-agent memory support, and a major `/import` expansion covering Cursor and Claude Code migrations. A high‑impact regression in encrypted MultiAgentV2 messages (#28058, 99 👍) continues to draw heavy community attention, while Windows stability remains a major pain point with four new critical bugs filed in the last 48 hours.

## Releases
**`rust-v0.145.0`** — Stable release featuring:
- **Experimental paginated thread history** with efficient resume, search, persisted names, sub‑agent support, and memories (PRs #33364, #33907, #34085, #34229, #34386).
- **Expanded `/import` command** now migrates Cursor and Claude Code settings, MCP servers, plugins, sessions, commands, and project configurations.
- Accompanying alpha releases `0.145.0-alpha.27` through `0.145.0-alpha.30` were also published.

## Hot Issues

1. **[#28058 — Regression: encrypted MultiAgentV2 messages remove readable task audit trail](https://github.com/openai/codex/issues/28058)**  
   *99 👍, 26 comments, OPEN*  
   Since #26210 merged (post-0.137.0), encrypted sub‑agent payloads prevent users from reviewing task decision logs. The top‑voted open bug signals a critical trust/auditability gap for multi‑agent workflows.

2. **[#9508 — Make Weekly Limit Reset Deterministic](https://github.com/openai/codex/issues/9508)**  
   *31 👍, 46 comments, OPEN*  
   A long‑running request for predictable rate‑limit reset timing. Users report that unpredictable resets disrupt planned usage cycles, with frustration echoed in related issue #16423.

3. **[#14919 — bwrap: Failed RTM_NEWADDR: Operation not permitted](https://github.com/openai/codex/issues/14919)**  
   *48 👍, 44 comments, CLOSED*  
   Linux bubblewrap sandbox regression introduced in 0.115.0. Closed today after multiple related issues (#15057, #12572), but the high engagement indicates the Linux sandbox remains fragile.

4. **[#32149 — Windows setup fails before UAC prompt](https://github.com/openai/codex/issues/32149)**  
   *5 👍, 24 comments, OPEN*  
   Fresh install on Windows is completely blocked — both setup options non‑functional. A severity‑high issue for Windows users.

5. **[#34260 — Windows Desktop: unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)**  
   *8 👍, 14 comments, OPEN*  
   Hundreds of orphaned `taskkill.exe` processes grind the system to a halt. Filed just two days ago and already a top concern for Windows Desktop users.

6. **[#26478 — Windows spellcheck shows “No Guesses Found”](https://github.com/openai/codex/issues/26478)**  
   *23 👍, 11 comments, OPEN*  
   Spellcheck detects errors but offers zero suggestions, while native Windows spellcheck works in Notepad. A puzzling regression affecting daily compose‑time UX.

7. **[#25921 — Crashpad pending dumps grow without limit: +5GB/day](https://github.com/openai/codex/issues/25921)**  
   *5 👍, 15 comments, OPEN*  
   macOS Desktop silently consumes disk space via unbounded Crashpad dump accumulation — 54,504 files and 4.9GB in one day on the reporter’s machine.

8. **[#34471 — Computer Use 1.0.1000451 cannot load @oai/sky on macOS 26](https://github.com/openai/codex/issues/34471)**  
   *0 👍, 3 comments, OPEN*  
   Filed yesterday; the Computer Use plugin fails to initialize because `nodeRepl.env` is empty on macOS 26.5.1. Early‑stage but potentially blocks plugin functionality.

9. **[#34227 — Windows pet overlay hit region desynchronizes from visible mascot](https://github.com/openai/codex/issues/34227)**  
   *0 👍, 4 comments, OPEN*  
   Click detection drifts away from the pet animation over time. Low votes but represents a recurring “pets” quality issue alongside #30158 (black background instead of transparency).

10. **[#34061 — Insane Codex Disk Usage from Subagents](https://github.com/openai/codex/issues/34061)**  
    *1 👍, 6 comments, OPEN*  
    Sub‑agents on macOS cause unbounded disk growth. Filed 4 days ago and quickly gaining traction as a performance liability.

## Key PR Progress

1. **[PR #34645 — Always assign response item IDs](https://github.com/openai/codex/pull/34645)**  
   Ensures every response item (streamed, forked, compacted, or from third‑party providers) gets a stable ID, fixing gaps in conversation continuity.

2. **[PR #34641 — Harden managed proxy setup for sandboxed executions](https://github.com/openai/codex/pull/34641)**  
   Makes Linux `bubblewrap` sandbox directories readable, routes `WS_PROXY`/`WSS_PROXY` through the managed proxy bridge—directly addresses the long‑running sandbox network failures (#14919 family).

3. **[PR #34624 — Terminate Windows process trees with job objects](https://github.com/openai/codex/pull/34624)**  
   Assigns Windows pipe, ConPTY, and sandbox processes to job objects so killing a session also stops child processes—tackles the root cause of orphaned process storms (#34260).

4. **[PR #34625 — Fix Windows TUI navigation key handling](https://github.com/openai/codex/pull/34625)**  
   Keeps the Windows console in input‑record mode, preventing navigation keys from being misinterpreted as escape bytes. Targets a long‑standing TUI pain point.

5. **[PR #34629 — Harden Windows elevated sandbox startup](https://github.com/openai/codex/pull/34629)**  
   Checks DACL permissions and refreshes ACLs when SIDs are missing required access—critical for reliable Windows sandbox launches.

6. **[PR #34626 — Scale skill metadata budgets with model context windows](https://github.com/openai/codex/pull/34626)**  
   Moves from a fixed character limit to a 2%‑of‑context‑window budget (capped at 4K tokens), aligning metadata with each model’s actual capacity.

7. **[PR #34636 — Keep the TUI open when starting a turn fails](https://github.com/openai/codex/pull/34636)**  
   Prevents the TUI from exiting on `turn/start` failures; instead shows the error in the transcript and resumes input. A UX improvement for intermittent server errors.

8. **[PR #34644 — Verify Git plugin SHA checkouts](https://github.com/openai/codex/pull/34644)**  
   Resolves `HEAD` after checkout to verify the pinned commit SHA matches, preventing branch‑name collision attacks in marketplace plugins.

9. **[PR #34621 — Load paginated model context across rollout lineages](https://github.com/openai/codex/pull/34621)**  
   Reverse‑scans rollout lineage segments to load paginated thread context correctly—a foundational fix for the new paginated thread history feature.

10. **[PR #34650 — Require auth managers to receive routing configuration](https://github.com/openai/codex/pull/34650)**  
    Mandates `AuthRouteConfig` for `AuthManager` construction, ensuring auth requests use the application’s resolved HTTP client factory instead of fallback proxies.

## Feature Request Trends
Three clear themes emerge from recent issues:
- **Predictability & Reliability**: Deterministic rate‑limit resets (#9508) and configurable weekly cycles remain the most‑upvoted feature request. Users need to plan their quota usage precisely.
- **Persistence & Session Management**: Background terminal sessions (#3968), window/session restore after restart (#27104), and pinned/persistent local task visibility (#33579) are recurring asks for production‑grade CLI and Desktop usage.
- **Customizability & Integration**: Adding custom editors to “Open In” (#10428), pinning the TUI input box to the bottom (#26311), and integrating with more IDEs/terminals.

## Developer Pain Points
- **Windows‑specific regressions dominate**: Five of the top ten hot issues involve Windows — setup failures (#32149), process‑cleanup storms (#34260), spellcheck (#26478), pet overlay desync (#34227), and black‑background pets (#30158). The Windows Desktop experience is currently the weakest platform.
- **Linux sandbox fragility**: The `bwrap: RTM_NEWADDR` error keeps resurfacing across Ubuntu/Arm64 setups, and AppArmor interactions remain unresolved despite multiple closed duplicates.
- **Audit‑trail loss with encryption**: The MultiAgentV2 encryption regression (#28058) is a blocker for any team relying on sub‑agent logs for debugging or compliance.
- **Unbounded resource leaks**: Crashpad dumps (macOS, +5GB/day) and sub‑agent disk growth (#34061) indicate systemic memory/resource management issues under sustained use.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-22

## Today’s Highlights
A **critical RCE fix** lands in tonight’s nightly release (`v0.52.0-nightly`), enforcing workspace trust and task isolation in the A2A server. Parallel security hardening continues with a PR closing a variable-expansion bypass (GHSA-wpqr-6v78-jr5g). Meanwhile, the community remains focused on agent reliability: subagent false-success reporting, shell command hangs, and the generalist agent hanging indefinitely remain persistent pain points.

## Releases
- **v0.52.0-nightly.20260722.gc776c665b** — patches `a2a-server` to prevent zero-click Remote Code Execution (RCE) by enforcing workspace trust and task-level isolation.  
  [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260721.gacae7124b...v0.52.0-nightly.20260722.gc776c665b)

## Hot Issues (10 selected)

1. **#22323** – Subagent recovery after MAX_TURNS falsely reports `"success"` with `Termination Reason: "GOAL"`, masking the real interruption. High engagement (12 comments), affects `codebase_investigator`.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#21409** – Generalist agent hangs forever on simple tasks (e.g., folder creation). Users work around by instructing the model not to use sub‑agents. 8 comments, 8 👍.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#19873** – Epic proposal to use Gemini 3’s native bash affinity with zero‑dependency OS sandboxing and post‑execution intent routing. Could radically improve safety and UX. 8 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/19873)

4. **#24353** – Component‑level evaluations epic, tracking 76 behavioral eval tests across 6 models. Core to quality assurance. 7 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

5. **#22745** – AST‑aware file reads, search, and mapping to reduce token waste and improve navigation precision. High potential to improve agent effectiveness. 7 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

6. **#21968** – Gemini rarely uses custom skills or sub‑agents on its own, even when explicitly instructed. Undermines the value of custom agents. 6 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

7. **#26522** – Auto‑Memory retries low‑signal sessions indefinitely because they’re never marked as processed. 5 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

8. **#25166** – Shell commands hang with `"Waiting input"` after completion. Happens with trivial commands, causing frequent user frustration. 4 comments, 3 👍.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

9. **#21983** – Browser agent fails on Wayland (terminates with `GOAL`). Linux‑only, critical for Wayland users. 4 comments.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

10. **#22672** – Agents occasionally use destructive commands (`git reset`, `--force`) when safer alternatives exist. Requests safety‑first behavior for database/git operations. 3 comments.  
    [Issue](https://github.com/google-gemini/gemini-cli/issues/22672)

## Key PR Progress (10 selected)

1. **#28470** (merged) – fix(a2a-server): enforce workspace trust and task isolation to prevent RCE. Critical security fix included in tonight’s nightly.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28470)

2. **#28403** – fix(core): block `$VAR`/`${VAR}` variable expansion bypass (GHSA-wpqr-6v78-jr5g). Hardens shell substitution detection.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28403)

3. **#28472** – fix(core): sequentially verify cached credentials and restore `GOOGLE_APPLICATION_CREDENTIALS` fallback. Resolves VS Code Agent Mode crash (exit code 41).  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28472)

4. **#28469** – fix(core): rotate session ID on model fallback to prevent stateful API errors when retrying with `gemini-2.5-flash`.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28469)

5. **#28433** – feat(pr-generator-orchestrator): iterative bug‑fixing state machine and container worker entrypoint. Part of the SSR pipeline project.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28433)

6. **#28431** – feat(pr-generator-infra): Cloud Run job, Workflows definition, and Dockerfile for the SSR pipeline.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28431)

7. **#28468** – feat(caretaker): add triage Cloud Run job workflow, orchestrated via Pub/Sub. Improves issue triage automation.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28468)

8. **#28305** – feat(evals): add tool‑call timeline formatting and failure summary diagnostics to behavioral evals. Better debugging for failing tests.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28305)

9. **#28169** – feat(evals): add `eval:coverage` command to report coverage of built‑in tools.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28169)

10. **#28397** – fix(core): remove synchronous I/O from shell tool critical path, eliminating terminal stuttering from blocking filesystem calls.  
    [PR](https://github.com/google-gemini/gemini-cli/pull/28397)

## Feature Request Trends
- **AST‑aware tooling** – Multiple issues (#22745, #22746) propose AST-aware file reading and codebase mapping to reduce token waste and improve navigation precision.
- **Better agent self‑awareness** – Users want the CLI to accurately describe its own flags, hotkeys, and ability to self‑execute (#21432).
- **Subagent trajectory sharing** – Visibility into what sub‑agents did, via `/chat share` or similar (#22598).
- **Destructive behavior prevention** – Agents should avoid unsafe git/database commands and prefer safer alternatives (#22672).
- **Zero‑dependency sandboxing** – Leverage Gemini 3’s native bash affinity for secure, intent‑routed execution (#19873).

## Developer Pain Points
- **Agent hangs & false positives** – The generalist agent hangs indefinitely (#21409); sub‑agents falsely report success after hitting turn limits (#22323).
- **Shell execution flakiness** – Commands frequently get stuck in `"Waiting input"` (#25166), and the model generates temp scripts in random directories (#23571).
- **Browser agent issues** – Fails on Wayland (#21983), ignores `settings.json` overrides (#22267), and struggles with locked profiles (#22232).
- **Configuration & permissions ignored** – Sub‑agents run even when disabled in config (#22093); symlinked agent files are not recognized (#20079).
- **Memory system bugs** – Auto‑Memory retries low‑signal sessions indefinitely (#26522), and secret redaction happens after content is already sent to the model (#26525).
- **Tool overload** – Enabling more than 128 tools causes a 400 error (#24246); the agent also fails to invoke existing custom skills (#21968).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest • 2026-07-22

## Today’s Highlights
A minor release (v1.0.74-0) landed with a new `/model plan` command for per-session model selection and improved resume search matching. Community attention is focused on MCP connectivity regressions, a plan-mode regression that blocks shell commands, and growing calls for richer MCP resource/subscription support. Several critical bugs—including zombie process accumulation and a 5 MB CAPI body limit—remain unresolved.

## Releases
**v1.0.74-0** – [Release notes](https://github.com/github/copilot-cli/releases/tag/v1.0.74-0)  
- **Added**: `/model plan` (or `/model --plan`) to pick a model for plan mode; pass `off` to reset, or no id to open a picker. Reverts to session model when leaving plan mode.  
- **Improved**: Resume search now matches session titles even when whitespace differs.

## Hot Issues (Top 10 by activity & impact)

1. [#2282 – Not Able to connect to MCP servers](https://github.com/github/copilot-cli/issues/2282)  
   *Closed* | 11 comments | 🏷️ area:mcp  
   Windows users reported MCP server connection failures after WinGet installation. Suggested workaround led to a fix; now closed.

2. [#1305 – Support CIMD for Remote OAuth MCP Servers](https://github.com/github/copilot-cli/issues/1305)  
   *Open* | 4 comments | 👍 26 | 🏷️ authentication, mcp  
   Request to enable Device Code (CIMD) flow for OAuth-protected MCP servers, beyond the current DCR-only support. High community demand.

3. [#4188 – Regression on plan-mode](https://github.com/github/copilot-cli/issues/4188)  
   *Open* | 3 comments | 👍 2 | 🏷️ permissions, tools  
   Latest version blocks shell commands during plan mode – a regression from prior behavior where `gh` CLI was used to create issues as part of planning.

4. [#2193 – Default model configuration for /fleet subagents](https://github.com/github/copilot-cli/issues/2193)  
   *Open* | 3 comments | 👍 14 | 🏷️ agents, models  
   Users want global or project-level default models for `/fleet` spawned subagents to avoid repeating model preference in every prompt.

5. [#4183 – Auto-compaction doesn’t prevent CAPI 5 MB failure](https://github.com/github/copilot-cli/issues/4183)  
   *Open* | 2 comments | 👍 5 | 🏷️ context-memory, models  
   Long tool-heavy sessions can hit the independent 5 MB serialized request body limit even when within token budget. Auto-compaction is insufficient.

6. [#4163 – Zombie child process accumulation](https://github.com/github/copilot-cli/issues/4163)  
   *Open* | 2 comments | 👍 0 | 🏷️ platform-linux, tools  
   CLI 1.0.71 fails to reap finished subprocesses, causing zombies (~2/minute) under the copilot PID. Affects long-running sessions.

7. [#1518 – Support MCP resources and prompts](https://github.com/github/copilot-cli/issues/1518)  
   *Open* | 2 comments | 👍 14 | 🏷️ mcp  
   Users request support for the two remaining MCP primitives beyond tools: `resources` (data exposure) and `prompts` (templates). Long-standing, high demand.

8. [#4012 – BYOK reasoning effort not supported for model "glm-5.2:cloud"](https://github.com/github/copilot-cli/issues/4012)  
   *Open* | 2 comments | 👍 16 | 🏷️ models, configuration  
   Using `--reasoning-effort max` with a custom BYOK model fails with an error claiming the model doesn’t support it, despite valid config.

9. [#2595 – Background agent completion retention](https://github.com/github/copilot-cli/issues/2595)  
   *Open* | 2 comments | 👍 0 | 🏷️ agents  
   Completed background agents are purged almost immediately, causing `read_agent` to return “not found” after a successful completion notification.

10. [#4206 – Environment footer stuck on "Loading:" forever](https://github.com/github/copilot-cli/issues/4206)  
    *Open* | 1 comment | 👍 1 | 🏷️ triage  
    Built-in GitHub MCP handshake stalls under org MCP policy, leaving the footer permanently in “Loading” state despite everything being loaded.

## Key PR Progress
No notable pull requests were updated or merged in the last 24 hours beyond one unrelated item. The community is awaiting fixes for the high-priority issues listed above.

## Feature Request Trends
- **MCP completeness**: Repeated requests for MCP `resources/read`, `resources/subscribe`, and `prompts` primitives ([#1518](https://github.com/github/copilot-cli/issues/1518), [#1803](https://github.com/github/copilot-cli/issues/1803), [#3073](https://github.com/github/copilot-cli/issues/3073)).
- **Model configuration flexibility**: Default models for subagents ([#2193](https://github.com/github/copilot-cli/issues/2193)), quick model/effort switching ([#4190](https://github.com/github/copilot-cli/issues/4190)), and BYOK reasoning effort support ([#4012](https://github.com/github/copilot-cli/issues/4012)).
- **Agent chaining & tool aliases**: Explicit inline agent invocation and custom agent access to `skill` tool ([#4208](https://github.com/github/copilot-cli/issues/4208), [#4209](https://github.com/github/copilot-cli/issues/4209)).
- **Usage transparency**: Per-subagent AI credit breakdown in `/usage` ([#4207](https://github.com/github/copilot-cli/issues/4207)).
- **Workspace-level customization**: Extend `.agents` discovery from skills to instructions, agents, and hooks in any opened folder ([#4204](https://github.com/github/copilot-cli/issues/4204)).

## Developer Pain Points
- **MCP reliability**: Frequent connection failures ([#2282](https://github.com/github/copilot-cli/issues/2282)), OAuth token refresh not silent ([#4203](https://github.com/github/copilot-cli/issues/4203)), and mid-turn tool list changes not reflected ([#3125](https://github.com/github/copilot-cli/issues/3125)).
- **Regression in plan mode**: Shell commands blocked, breaking workflows that relied on utilities like `gh` ([#4188](https://github.com/github/copilot-cli/issues/4188)).
- **Memory & context limits**: CAPI 5 MB body limit not mitigated by compaction ([#4183](https://github.com/github/copilot-cli/issues/4183)).
- **Process management**: Zombie process accumulation under Linux ([#4163](https://github.com/github/copilot-cli/issues/4163)).
- **Terminal rendering issues**: Invisible UI in tmux ([#4212](https://github.com/github/copilot-cli/issues/4212)), clipboard access broken in tmux/WSL ([#4191](https://github.com/github/copilot-cli/issues/4191)), and key input drops when terminal unfocused ([#4213](https://github.com/github/copilot-cli/issues/4213)).
- **BYOK / custom model friction**: Unsupported features, serialization errors with BigInt in MCP responses ([#4211](https://github.com/github/copilot-cli/issues/4211)), and transient API errors due to `reasoning_content` in streaming deltas ([#4196](https://github.com/github/copilot-cli/issues/4196)).
- **Enterprise policy blocks**: Registry policies rejecting MCP configs with required runtime headers ([#4205](https://github.com/github/copilot-cli/issues/4205)), and billing entity selection failing for memory saves ([#4005](https://github.com/github/copilot-cli/issues/4005)).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-22

## Today's Highlights
A new PR (#2530) fixes a critical shell-mode hang caused by detached child processes, directly addressing a community-reported issue. Two high-severity bugs emerged today: MCP tool schemas are being rejected by the Moonshot API (HTTP 400), requiring client-side sanitization, and the k2.5 model shows a complete tool calling failure with infinite loops in goal mode. No new releases were published in the last 24 hours.

## Releases
None. No new versions of Kimi Code CLI were released in the last 24 hours.

## Hot Issues
Due to the limited dataset (5 items), all open issues updated in the last 24h are covered:

**#2531** — **MCP tool names & schemas rejected by Moonshot API (HTTP 400)**  
Author: sbdsam  
Severity: High – blocks all MCP tool calls on the Moonshot API. The error indicates `tools.function.parameters` does not conform to a “moonshot flavored json schema”, specifically when using `anyOf`. Community reaction: 0 comments, 0 👍, but the issue is critical for anyone using custom MCP tools.  
Link: [#2531](https://github.com/MoonshotAI/kimi-cli/issues/2531)

**#2527** — **[bug] k2.5 model tool calling completely invalid + goal mode infinite loop**  
Author: lesteryan  
Severity: Critical – the k2.5 model cannot execute any tool calls and loops endlessly in goal mode. The reporter tried multiple string formats (including `functions_Bash`, `functions_Bash_0`, and JSON) — all fail with “Tool not found”. Community reaction: 0 comments, 0 👍, but severity warrants immediate attention.  
Link: [#2527](https://github.com/MoonshotAI/kimi-cli/issues/2527)

**#2474** — **[bug] CLI interface keeps shaking / re-rendering full conversation**  
Author: yudichimiantiao  
Severity: Medium – UI stability issue on Linux. The terminal UI flickers and resets to the beginning of conversation history without user action. Has been open since June 25 with 1 comment and 2 👍, indicating persistent community interest.  
Link: [#2474](https://github.com/MoonshotAI/kimi-cli/issues/2474)

**#2528** — **[bug] shell mode output is too long**  
Author: wenli7363  
Severity: Medium – when using `!` in shell mode, output floods the terminal without truncation, degrading UX. No comments yet.  
Link: [#2528](https://github.com/MoonshotAI/kimi-cli/issues/2528)

**#2529** — **[bug] right-side number keypad not responding**  
Author: woai3c  
Severity: Low – Windows users cannot input numbers via the numeric keypad; likely missing Numpad key event listeners. No comments yet.  
Link: [#2529](https://github.com/MoonshotAI/kimi-cli/issues/2529)

## Key PR Progress
Only one PR was updated in the last 24h:

**#2530** — **fix(shell): stop blocking until timeout when a detached child holds the pipes**  
Author: ayaangazali  
Status: Open  
Summary: Fixes a hang in foreground shell mode where `_run_shell_command` waits for stdout/stderr EOF before checking exit codes. Commands like `some_daemon & echo done` keep pipes open indefinitely, causing a timeout. The fix ensures the exit code is checked earlier, resolving the blocking behavior.  
Link: [#2530](https://github.com/MoonshotAI/kimi-cli/pull/2530)

## Feature Request Trends
Given the small issue set (5 items, all bug reports), no explicit feature requests were filed today. However, the patterns suggest unmet needs around:

- **MCP tool compatibility** – the need for robust schema validation and broader tool name format support (raised by #2531, #2527).
- **Shell mode UX improvements** – output truncation and subprocess lifecycle management are recurring themes (#2528, #2530).
- **Input device parity** – missing key event handling for numeric keypads (#2529) implies a desire for full keyboard hardware support.

## Developer Pain Points
- **Model-specific tool calling regressions**: The k2.5 model’s complete failure to use tools (#2527) is a blocker for anyone relying on goal mode or MCP integration. The “Tool not found” error across multiple naming formats suggests a deeper mismatch between model output and runtime function registration.
- **MCP API schema validation**: The Moonshot API’s strict JSON Schema requirements (especially with `anyOf`) are causing `400` errors, forcing developers to sanitize schemas client-side (#2531). This adds an extra integration burden and unclear error messages.
- **UI instability**: The persistent conversation re-rendering bug (#2474) on Linux continues to disrupt workflow, with no fix in sight for nearly a month.
- **Shell mode blocking**: The hang-on-detached-child issue (#2468/#2530) is a classic but painful async I/O problem that can stall interactive sessions indefinitely.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-22

## Today's Highlights
The community remains heavily focused on the long-running **Memory Megathread (#20695)**, which continues to accumulate heap snapshot reports and debugging discussion. A cluster of **OpenCode Go subscription billing issues** (#37790, #38195, #38208) has emerged over the past 48 hours, with multiple users reporting paid subscriptions being treated as "Insufficient balance." On the PR side, infrastructure work is progressing on **Copilot API endpoint discovery** (#38184), **clock-skew response loop fixes** (#38213), and **MiniMax M3 thinking mode routing** (#38214).

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **#20695 — Memory Megathread**  
   *Author: thdxr | Comments: 119 | 👍: 90*  
   Central debugging hub for scattered memory reports. The thread explicitly discourages LLM-generated solution suggestions and requests manual heap snapshots. Remains the most active issue by far.  
   🔗 [Issue #20695](https://github.com/anomalyco/opencode/issues/20695)

2. **#6231 — Auto-discover models from OpenAI-compatible providers**  
   *Author: ochsec | Comments: 26 | 👍: 182*  
   The most upvoted open request. Users want automatic model discovery for LM Studio, Ollama, llama.cpp, etc., rather than manual listing in `opencode.json`. High demand underscores friction in local provider workflows.  
   🔗 [Issue #6231](https://github.com/anomalyco/opencode/issues/6231)

3. **#37012 — Keep legacy layout option**  
   *Author: darkine24th | Comments: 26 | 👍: 27*  
   Strong sentiment for preserving the old layout. Arguments include easier access to features from the main window and workspace support that the new "tabs on top" design lacks.  
   🔗 [Issue #37012](https://github.com/anomalyco/opencode/issues/37012)

4. **#37790 — Go subscription paid, workspace shows "Insufficient balance"**  
   *Author: ahdkabeerhadi | Comments: 10 | 👍: 0*  
   Payment successfully processed via Stripe, but workspace refuses access. Blocks all Go model usage. First report in a growing cluster.  
   🔗 [Issue #37790](https://github.com/anomalyco/opencode/issues/37790)

5. **#38195 — 401 AuthError: Request blocked by upstream provider**  
   *Author: faustkuroki | Comments: 2 | 👍: 8*  
   Active Go subscription but all Go models return 401. Free models work normally. Reproduces across multiple machines and clients. Likely linked to #37790.  
   🔗 [Issue #38195](https://github.com/anomalyco/opencode/issues/38195)

6. **#19130 — Windows ARM64 native: OpenTUI fails with bun:ffi dlopen TinyCC error**  
   *Author: Carliquiss | Comments: 12 | 👍: 8*  
   Native ARM64 binary works for CLI commands but TUI initialization fails. Blocks Windows ARM64 users from interactive sessions.  
   🔗 [Issue #19130](https://github.com/anomalyco/opencode/issues/19130)

7. **#37481 — Desktop fatal crash on WSL sidecar server reference**  
   *Author: Shana-AE | Comments: 7 | 👍: 1*  
   Persisted window tabs referencing WSL sidecars cause fatal errors on launch because the renderer resolves the server before WSL finishes booting. Leaves app unusable.  
   🔗 [Issue #37481](https://github.com/anomalyco/opencode/issues/37481)

8. **#38190 — Request blocked by upstream provider**  
   *Author: sosigboys | Comments: 7 | 👍: 5*  
   Generic "Request blocked" error when sending messages. Likely related to the Go subscription auth issues. Multiple users reporting similar symptoms.  
   🔗 [Issue #38190](https://github.com/anomalyco/opencode/issues/38190)

9. **#37056 — Go provider returns 400/401/500 for subscribed models**  
   *Author: 123456789cm | Comments: 6 | 👍: 0*  
   Detailed breakdown: 400 for large DeepSeek requests, 401 for intermittent API key rejection, 500 for internal errors. Suggests multiple root causes.  
   🔗 [Issue #37056](https://github.com/anomalyco/opencode/issues/37056)

10. **#38124 — Web: existing profiles not eligible for layout transition toggle**  
    *Author: dleopold | Comments: 3 | 👍: 1*  
    `layoutTransitionEligible` flag only initialized during desktop onboarding, so Web users with existing profiles cannot access the grace-period toggle to switch layouts.  
    🔗 [Issue #38124](https://github.com/anomalyco/opencode/issues/38124)

## Key PR Progress

1. **#38214 — fix(provider): route MiniMax M3 thinking controls**  
   Sends NVIDIA and Lilac MiniMax M3 toggles through `chat_template_kwargs.thinking_mode` and normalizes reasoning toggles for Kilo/Vercel gateways. Preserves `thinking.type: adaptive` for direct passthrough.  
   🔗 [PR #38214](https://github.com/anomalyco/opencode/pull/38214)

2. **#38213 — fix: stop clock-skew response loops**  
   Closes two issues (#24476, #25270). Prevents incorrect server responses when client and server clocks differ.  
   🔗 [PR #38213](https://github.com/anomalyco/opencode/pull/38213)

3. **#38184 — fix(core): discover Copilot API endpoint**  
   Discovers account-specific Copilot API endpoint during V2 OAuth, persists it, and uses it for model discovery and inference — without adding a request to normal provider startup.  
   🔗 [PR #38184](https://github.com/anomalyco/opencode/pull/38184)

4. **#37832 — fix(app): prevent Solid cleanNode crash on session switch**  
   Fixes `TypeError: Cannot read properties of undefined` that freezes/crashes desktop app during session switches.  
   🔗 [PR #37832](https://github.com/anomalyco/opencode/pull/37832)

5. **#37620 — fix(desktop): use custom titlebar on Linux**  
   Previously fell back to native GTK decorations. Now applies custom titlebar configuration for Linux Electron windows.  
   🔗 [PR #37620](https://github.com/anomalyco/opencode/pull/37620)

6. **#38188 — fix(core): reject malformed patch hunks**  
   Rejects invalid add/delete/update hunk body lines, empty hunks, and misplaced EOF markers with line-specific errors. Preserves Codex-compatible implicit update chunks.  
   🔗 [PR #38188](https://github.com/anomalyco/opencode/pull/38188)

7. **#37833 — fix(provider): add NVIDIA NIM DeepSeek request compatibility**  
   Fixes hang with DeepSeek V4 models on NVIDIA NIM. DeepSeek V4 Flash and Pro now stream correctly.  
   🔗 [PR #37833](https://github.com/anomalyco/opencode/pull/37833)

8. **#38206 — fix(provider): cache all system messages instead of only first 2**  
   `applyCaching()` previously sliced system messages to first 2. This caused loss of plugin system messages and MCP instructions. Now caches all.  
   🔗 [PR #38206](https://github.com/anomalyco/opencode/pull/38206)

9. **#38172 — feat(codemode): support generator functions**  
   Adds sync/async generator support with lazy yield, delegation, finally completion, and FIFO async request semantics.  
   🔗 [PR #38172](https://github.com/anomalyco/opencode/pull/38172)

10. **#38183 — feat(core): render CodeMode catalog deltas from structured snapshots**  
    Moves Code Mode catalog prompting out of `@opencode-ai/codemode` so core owns model-facing instruction text. Upgrades to skill-style semantic deltas.  
    🔗 [PR #38183](https://github.com/anomalyco/opencode/pull/38183)

## Feature Request Trends

**Layout flexibility** dominates the feature landscape. Multiple issues (#37012, #37546, #38124) request either a legacy layout toggle, workspace/worktree support in the new layout, or better transition controls for existing Web users. The community clearly values the old layout's single-window access and workspace integration.

**Model discovery & subscription management** is the second major theme. Issue #6231 (auto-discover models, 182 👍) leads all requests by a wide margin. The OpenCode Go billing/auth problems (#37790, #38195, #37056, #38208) are generating urgent feature requests for better subscription state management and error messaging.

**Session management improvements** appear in #38163 (auto-name sessions from first message), #37381 (prompt queue and interrupt controls), and #4925 (total cost display for multi-agent sessions).

**Mobile/PWA support** is surfacing through #35480 (iOS safe-area handling for PWA), while **MCP integration** continues with #11948 (sampling/createMessage support) and #38176 (long-term memory search CLI).

## Developer Pain Points

**OpenCode Go billing/subscription bugs** are the most acute pain point this week. At least three distinct issues report paid subscriptions that fail to grant access — payments go through but workspaces show zero balance. The auth errors (401/400/500) for Go models suggest either stale provisioning state or upstream provider configuration drift.

**Upstream provider errors** ("Request blocked by upstream provider") are spiking — issues #38190, #38195, #37056, and #38215 all report similar symptoms. The root cause appears linked to the Go subscription auth layer rather than individual models.

**WSL/Windows compatibility** remains fragile: the WSL sidecar crash (#37481) makes the desktop app completely unusable for affected Windows users, while the ARM64 TUI failure (#19130) blocks an entire platform.

**Layout transitions** are causing real workflow disruption. Users who upgrade past v1.17.19 on Web lose workspace/worktree support with no way to revert (#37546), while desktop users report the legacy layout toggle only works for new installations (#38124).

**Memory and performance** concerns persist, with the Memory Megathread (#20695) serving as a long-running collection point. The terminal 100% CPU bug (#13899) for Web users remains unresolved.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-07-22

## Today’s Highlights
Two releases landed within 24 hours: **v0.81.0** adds local model management via llama.cpp, and **v0.81.1** ships verifiable release source archives for standalone builds. A flurry of crash bugs filed against v0.81.0 (issues #6915, #6918, #6920) were quickly closed, reflecting the team’s fast triage response. Compaction reliability also saw multiple fixes merged today.

## Releases

- **[v0.81.1](https://github.com/earendil-works/pi/releases/tag/v0.81.1)** — Deterministic checksummed source archives with rebuild instructions for standalone binaries.  
- **[v0.81.0](https://github.com/earendil-works/pi/releases/tag/v0.81.0)** — Local llama.cpp model management: connect to a router, search/download Hugging Face models, and load/unload with live progress.

## Hot Issues (10 selected)

1. **[#3357: Official local LLM provider extension (CLOSED)](https://github.com/earendil-works/pi/issues/3357)** — Request to dynamically fetch model list from `{baseUrl}/models`. 30 comments, 43 👍. Closed, likely superseded by llama.cpp support in v0.81.0.

2. **[#6278: Bug: New Claude models fail ~20% edits with tool validation errors (CLOSED)](https://github.com/earendil-works/pi/issues/6278)** — Extra keys in `edit[]` elements cause dropouts. 23 comments, high impact on Sonnet 4.5 users.

3. **[#5653: Move off Shrinkwrap (OPEN)](https://github.com/earendil-works/pi/issues/5653)** — Duplicate module copies when installing both `pi-ai` and `pi-coding-agent`. 19 comments. Blocking clean dependency management.

4. **[#6915: Pi crashes with uncaughtException after updating to 0.81.0 (CLOSED)](https://github.com/earendil-works/pi/issues/6915)** — `streamFunction is not a function` on session resume. 14 comments. Fixed in v0.81.1.

5. **[#6747: API for enhancing agent message markdown (OPEN)](https://github.com/earendil-works/pi/issues/6747)** — Allow extensions to mutate rendered markdown without affecting LLM payload. 7 comments. Needed for formula renderers and custom UIs.

6. **[#6774: Ctrl+G external editor slow when os.tmpdir() crowded (OPEN)](https://github.com/earendil-works/pi/issues/6774)** — Temp file collision in shared tmpdir. 7 comments. Affects Wayland/bwrap users.

7. **[#6879: Auto-compaction never triggers until provider overflow (OPEN)](https://github.com/earendil-works/pi/issues/6879)** — Context grows past 100% without compaction; only fires after API rejection. 3 comments. Serious UX issue for long agentic turns.

8. **[#6911: OpenAI SDK retry sleeps full Retry-After, Escape cannot abort (CLOSED)](https://github.com/earendil-works/pi/issues/6911)** — Multi-day retry delays blockkill. Fixed in PR #6912.

9. **[#6920: Autocomplete crash on `/` when provider returns non-string (CLOSED)](https://github.com/earendil-works/pi/issues/6920)** — `TypeError: value.startsWith is not a function`. 3 comments.

10. **[#6817: `find` returns no results for path patterns like `src/**/*.ts` on Windows (OPEN)](https://github.com/earendil-works/pi/issues/6817)** — Path separator parsing broken. Windows users blocked.

## Key PR Progress (10 selected)

1. **[#6913: Add release source archives (CLOSED)](https://github.com/earendil-works/pi/pull/6913)** — Merged into v0.81.1. Deterministic archives with checksums for binary verification.

2. **[#6901: Compaction & branch summarization follow retry policy (CLOSED)](https://github.com/earendil-works/pi/pull/6901)** — Fixes #6647. Retries transient failures during compaction; emits retry events for TUI.

3. **[#6912: Never enable OpenAI/Anthropic SDK Retry-After sleeps (CLOSED)](https://github.com/earendil-works/pi/pull/6912)** — Forces `maxRetries=0` to prevent days-long freezes. Critical fix.

4. **[#6928: Generate models: use reasoning options from models.dev (OPEN)](https://github.com/earendil-works/pi/pull/6928)** — Syncs model thinking levels from upstream catalog. Affects Claude, GPT-5, etc.

5. **[#6927: Add native OpenRouter OAuth support (OPEN)](https://github.com/earendil-works/pi/pull/6927)** — PKCE flow with localhost callback. Simplifies OpenRouter authentication.

6. **[#6903: Speed up external editor launch (OPEN)](https://github.com/earendil-works/pi/pull/6903)** — Moves temp file into private `mkdtemp` subdirectory. Addresses #6774.

7. **[#6881: Use provider-reported cost when available (OPEN)](https://github.com/earendil-works/pi/pull/6881)** — Reads `usage.cost` from OpenAI responses; improves billing accuracy.

8. **[#6916: Add AgentHarness execution tools (OPEN)](https://github.com/earendil-works/pi/pull/6916)** — Abstraction for agent tool execution with arbitrary app-specific context. Foundation for custom integrations.

9. **[#6654: Add promptCacheKey stream option (OPEN)](https://github.com/earendil-works/pi/pull/6654)** — Replaces `sessionId` as cache key for OpenAI providers. Enables shared prompt caching across sessions.

10. **[#6594: SQLite session storage (CLOSED)](https://github.com/earendil-works/pi/pull/6594)** — Adds `retainedTail` for compaction; reduces tree traversal. Merged, improves session persistence performance.

## Feature Request Trends

- **Local/first-party LLM support** – After v0.81.0’s llama.cpp integration, related requests focus on dynamic model discovery (#3357) and server-side fallbacks (#6886). Community clearly wants to reduce cloud dependency.
- **Extension API improvements** – Issues #6747 (markdown mutation), #6552 (deferred reload), and #6757 (tool event hooks) show demand for richer extension capabilities. The `AgentHarnessTool` PR (#6916) aligns with this.
- **Session management** – Archive shortcuts (#6917), SQLite storage (#6594), and dedicated temp directories for editor (#6774) indicate a move toward more robust session handling.
- **Provider diversity** – Bedrock Mantle (#6216), OpenRouter OAuth (#6927), and prompt cache key overrides (#6654) highlight the need for flexible model access.

## Developer Pain Points

- **Crashes on v0.81.0 update** – At least three crash reports (#6915, #6918, #6920) immediately after release, all related to `streamFunction` or autocomplete. Quickly patched but eroded trust.
- **Compaction unreliability** – Compaction fails on single transient dropout (#6647) and never triggers until overflow (#6879). Retry policies now applied but still a pain point.
- **Windows compatibility** – `find` tool broken with path patterns (#6817) and potential path separator issues remain unresolved.
- **Dependency duplication** – Shrinkwrap causes duplicate module instances (#5653), creating subtle state bugs.
- **External editor slowness** – Crowded `os.tmpdir()` stalls Ctrl+G (#6774); a fix is in review.
- **SDK retry blocking** – Non-abortable multi-day Retry-After from OpenAI/Anthropic SDK (#6911) – now fixed but a classic “silent hang” frustration.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the **Qwen Code Community Digest** for **2026-07-22**, based on the latest project activity.

---

### 1. Today's Highlights

Today marks the release of **Qwen Code v0.20.1**, which ships with a new label-driven autofix takeover system and an updated CUA driver supporting relative coordinates. The community is actively addressing a cluster of critical bugs around sub-agent model mutation and OpenAI tool-call schema incompatibility, while infrastructure work continues to harden telemetry initialization and startup performance.

---

### 2. Releases

**v0.20.1**
- **Highlights:** This stable release introduces a label-driven autofix takeover-and-release mechanism, along with fixes for forced-dispatch green no-ops.
- **Breaking Changes:** None known.
- **Other:** The release also includes **cua-driver-rs v0.7.3**, a vendored binary for relative-coordinate mode, with signed binaries for macOS, and unsigned binaries for Linux and Windows.
- **Full Changelog:** [QwenLM/qwen-code Release v0.20.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.1)

**v0.20.0-preview.0** and **v0.20.0-nightly.20260722** were also published, containing the same telemetry test changes from PR #7456.

---

### 3. Hot Issues

1.  **[#7156](https://github.com/QwenLM/qwen-code/issues/7156) [CLOSED] Subagent mutates main session model — context overflow recurrence** (Priority: P1)
    - **Why it matters:** This is a critical regression where a fix for model-override clearing (#7119) was bypassed by a different code path, causing the main session's model to still be silently swapped during subagent execution.
    - **Community:** High engagement (11 comments); closed as fixed.

2.  **[#7316](https://github.com/QwenLM/qwen-code/issues/7316) [CLOSED] OpenAI toolCall special behavior breaks subAgent entirely** (Priority: P2)
    - **Why it matters:** OpenAI-compatible models returning empty strings for optional fields (like `working_dir`) caused the `agent` tool to fail, blocking a core workflow for a significant user segment.
    - **Community:** Active discussion (5 comments); closed.

3.  **[#7056](https://github.com/QwenLM/qwen-code/issues/7056) [OPEN] Qwen ACP process exits unexpectedly on VS Code startup** (Priority: P2)
    - **Why it matters:** A persistent integration blocker for Windows users where the VS Code Companion fails to connect. High visibility due to poor onboarding UX.
    - **Community:** Needs more information from the author (5 comments).

4.  **[#7427](https://github.com/QwenLM/qwen-code/issues/7427) [OPEN] Web-shell: Artifact panel spams 'Load artifacts failed: Failed to fetch'** (Priority: P2)
    - **Why it matters:** A UI noise issue that degrades the web shell experience, particularly for users with large or auto-refreshing sessions.
    - **Community:** 4 comments; labeled as a welcome PR.

5.  **[#7306](https://github.com/QwenLM/qwen-code/issues/7306) [OPEN] Harden tool-output budgeting, observability, and artifact lifecycle** (Priority: P2)
    - **Why it matters:** An umbrella issue for a multi-phase project to improve system robustness and debuggability for large tool outputs.
    - **Community:** Phase 1 merged; discussion continues on future phases (4 comments).

6.  **[#7433](https://github.com/QwenLM/qwen-code/issues/7433) [OPEN] Local model usage shows "qwen-oauth" as currentModel in SDK** (Priority: P2)
    - **Why it matters:** A confusing bug for users running local models (e.g., via `llama.cpp`), as the SDK reports an incorrect, non-existent model name from the Qwen platform.
    - **Community:** Fresh report (2 comments); needs triage.

7.  **[#7452](https://github.com/QwenLM/qwen-code/issues/7452) [OPEN] cronParser: `*/N` deviates from vixie-cron semantics** (Priority: P2)
    - **Why it matters:** A subtle compatibility bug in the cron parser's OR-vs-AND rule for day fields, which could lead to schedules running at unexpected times.
    - **Community:** Detailed technical report (2 comments); labeled as welcome PR.

8.  **[#7287](https://github.com/QwenLM/qwen-code/issues/7287) [OPEN] Auto-memory MEMORY.md not registered in FileReadCache** (Priority: P2)
    - **Why it matters:** A nasty paper-cut for the auto-memory feature: the first attempt to update the memory file always fails because the system doesn't register its initial read.
    - **Community:** Clear reproduction and expected behavior described (2 comments).

9.  **[#7332](https://github.com/QwenLM/qwen-code/issues/7332) [CLOSED] BadRequestError sent to thinking-only models** (Priority: P1)
    - **Why it matters:** A critical integration bug where internal operations sent `enable_thinking=false` to models that require thinking, causing a 400 error.
    - **Community:** 2 comments; quickly closed as fixed.

10. **[#7377](https://github.com/QwenLM/qwen-code/issues/7377) [OPEN] Session tool call parameters lost** (Priority: P2)
    - **Why it matters:** A frustrating bug causing tool call failures and retry loops due to parameter loss, impacting productivity in longer sessions.
    - **Community:** Report details a multi-step reproduction (2 comments).

---

### 4. Key PR Progress

1.  **[#7456](https://github.com/QwenLM/qwen-code/pull/7456) [CLOSED] test(telemetry): Cover daemon metrics init ordering**
    - **Why it matters:** A crucial follow-up to the lazy telemetry SDK work. It adds a test for daemon metrics initialization ordering, preventing a race condition.
    - **Status:** Merged. Also used in the nightly and preview releases.

2.  **[#7403](https://github.com/QwenLM/qwen-code/pull/7403) [CLOSED] fix: Normalize empty working_dir when isolation:worktree is set**
    - **Why it matters:** Directly addresses the OpenAI tool-call schema issue (#7316 & #7315) by normalizing an empty string to `unset`, fixing sub-agent launch for a wide range of models.
    - **Status:** Merged.

3.  **[#7455](https://github.com/QwenLM/qwen-code/pull/7455) [CLOSED] perf(startup): Load undici lazily**
    - **Why it matters:** A significant performance win for ACP cold starts. Moves the 2 MiB undici HTTP client out of the eager startup closure, reducing initialization time.
    - **Status:** Merged.

4.  **[#7454](https://github.com/QwenLM/qwen-code/pull/7454) [OPEN] fix(core): Advertise completed task revival**
    - **Why it matters:** Improves UX by making the ability to revive completed background tasks visible to the model, enabling a long-requested feature (#5540).
    - **Status:** Open; seeking review.

5.  **[#7388](https://github.com/QwenLM/qwen-code/pull/7388) [OPEN] feat(daemon): Add explicit channel delivery**
    - **Why it matters:** A major infrastructure PR introducing a formal channel delivery contract for daemon notifications, improving reliability and composability for scheduled tasks.
    - **Status:** Open (autofix/takeover).

6.  **[#7393](https://github.com/QwenLM/qwen-code/pull/7393) [OPEN] feat(core): Add memory recall delivery telemetry**
    - **Why it matters:** Enhances observability for the auto-memory feature by distinguishing *selection* from *delivery*, helping debug cases where selected memories are not actually used.
    - **Status:** Open (autofix/takeover).

7.  **[#7268](https://github.com/QwenLM/qwen-code/pull/7268) [OPEN] feat(serve): Hot-reload workspace trust changes**
    - **Why it matters:** Eliminates the need for a daemon restart when workspace trust policies are updated, improving operational efficiency for multi-tenant or security-sensitive setups.
    - **Status:** Open (autofix/takeover).

8.  **[#7390](https://github.com/QwenLM/qwen-code/pull/7390) [CLOSED] feat(web-shell): Add workspace selector button**
    - **Why it matters:** Fulfills a major feature request (#6700) for the web shell, allowing users to switch or register workspaces directly from the UI composer.
    - **Status:** Merged.

9.  **[#7459](https://github.com/QwenLM/qwen-code/pull/7459) [OPEN] feat(core): Restore background agent roster**
    - **Why it matters:** A critical fix for session persistence: ensures that background agents (interrupted or completed) are retained and visible when the parent session is reopened.
    - **Status:** Open.

10. **[#7302](https://github.com/QwenLM/qwen-code/pull/7302) [OPEN] feat(cli): Reference prior sessions via @ and add completion tabs**
    - **Why it matters:** A powerful CLI enhancement that allows users to quickly reference and inject summaries of past sessions using `@mention` completion, improving cross-session context.
    - **Status:** Open (autofix/takeover).

---

### 5. Feature Request Trends

- **Session Management & Persistence:** The highest-demand direction. Users heavily request the ability to **resume completed background sub-agents** ([#5540](https://github.com/QwenLM/qwen-code/issues/5540)) and for sessions to **retain their agent rosters** upon restoration.
- **Web Shell Usability & Tooling:** Strong demand for a richer web shell UI, specifically **workspace selectors** ([#6700](https://github.com/QwenLM/qwen-code/issues/6700)), **context selectors** (local vs. worktree startup) ([#6701](https://github.com/QwenLM/qwen-code/issues/6701)), and sub-agent detail panels.
- **Cross-Platform & Provider Compatibility:** A growing need for better handling of **OpenAI-compatible providers**, specifically around tool-call schema validation and optional parameters.
- **Observability & Debugging:** Feature requests and enhancements for **telemetry** ([#7393](https://github.com/QwenLM/qwen-code/pull/7393)) and **tool-output budgeting** ([#7306](https://github.com/QwenLM/qwen-code/issues/7306)) indicate a strong desire from power users for more insight into system internals.

---

### 6. Developer Pain Points

- **Sub-Agent Model Mutation (P1):** The fact that a sub-agent can silently change the main session's model remains a top frustration, highlighting the fragility of the session state management during concurrent agent execution.
- **OpenAI Tool-Call Schema Incompatibility (P1/P2):** Several bugs ([#7316](https://github.com/QwenLM/qwen-code/issues/7316), [#7315](https://github.com/QwenLM/qwen-code/issues/7315)) point to a painful recurring issue where the `agent` tool schema is not tolerant of unexpected null or empty string values from newer LLMs.
- **Session Context and State Loss:** Issues with `send_message` failing on completed tasks ([#5540](https://github.com/QwenLM/qwen-code/issues/5540)), missing background agent rosters on session restore ([#7459](https://github.com/QwenLM/qwen-code/pull/7459)), and parameter loss during tool calls ([#7377](https://github.com/QwenLM/qwen-code/issues/7377)) create a recurring theme of workflow interruption.
- **Token & Authentication Pain:** The web shell losing its bearer token on page refresh ([#7301](https://github.com/QwenLM/qwen-code/issues/7301), [#7398](https://github.com/QwenLM/qwen-code/issues/7398)) is a consistent point of friction for users of token-based auth.
- **Windows Stability:** The combination of a missing SHA-256 verification during installation ([#7118](https://github.com/QwenLM/qwen-code/issues/7118)) and Docker sandbox path issues ([#7139](https://github.com/QwenLM/qwen-code/issues/7139)) makes the Windows user experience particularly rough.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-07-22

*Based on data from the CodeWhale repository (github.com/Hmbown/CodeWhale), the terminal UI project for DeepSeek development tools.*

## Today's Highlights

The `v0.9.1` release enters its final fan-in phase: a major integration PR lands base runtime simplifications, empty-Work fixes, and a polished TUI color grammar. Community contributors shipped fixes for long-standing annoyances—Enter‑key lag (200–1200ms freeze) and sub‑agent worktree cwd issues—while maintainers closed 20+ release‑blocker issues in a single day. The project continues to see high velocity with 10+ PRs daily and an active focus on agent coordination, truthful UI state, and permission contracts.

## Releases

No new releases in the last 24 hours. The team is finalizing `v0.9.1` via the integration PR #4675.

## Hot Issues

1. **[#4032 – Codewhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032)** (41 comments)  
   *bug, release‑blocker, agent‑ready, subagents*  
   Community frustration: the AI agent consistently ignores provided scripts and writes temporary ones. User challenges are brushed off. Points to deeper issues in tool‑policy enforcement. Closed today.

2. **[#2870 – EPIC: staged command‑boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)** (15 comments)  
   *documentation, release‑blocker, cleanup*  
   Tracking EPIC breaking the large command‑strategy refactor into mergeable layers. Still open; multiple sub‑issues and reference PRs (e.g., #2851) are active proof‑of‑concept branches.

3. **[#4227 – Help map the CodeWhale tsunami](https://github.com/Hmbown/CodeWhale/issues/4227)** (11 comments)  
   *enhancement, workflow‑runtime, subagents*  
   Community member JayBeest proposes a skill/workflow to sync dev environments with `main`. High project velocity (10+ PRs/day) makes it hard to contribute without constant rebasing.

4. **[#2766 – UI refactor needed](https://github.com/Hmbown/CodeWhale/issues/2766)** (9 comments)  
   *UI, usability*  
   Persistent complaint: output is hard to copy and confirmation pop‑ups obscure key data. Open since June; multiple duplicates link here.

5. **[#2889 – Work Agent rows: real sub‑agent details](https://github.com/Hmbown/CodeWhale/issues/2889)** (7 comments)  
   *agent‑ready, tui, subagents, ux*  
   Restored from a deleted issue. Calls for the sidebar to show true agent activity and structured task status instead of raw tool noise.

6. **[#4410 – Restore xAI device‑code OAuth](https://github.com/Hmbown/CodeWhale/issues/4410)** (7 comments)  
   *bug, release‑blocker*  
   `/auth xai-device` fails due to a hard‑coded path mismatch with the official Grok CLI. Fixed today.

7. **[#4650 – v0.9.1 completion board & final dogfood](https://github.com/Hmbown/CodeWhale/issues/4650)** (3 comments)  
   *release‑blocker, tools*  
   Owns final integration evidence, exact rebuilt/local dogfood, and the stop line for v0.9.1. Intentionally not `agent‑ready`.

8. **[#4636 – Make Work one truthful queue with clear Agents, activity, diffs](https://github.com/Hmbown/CodeWhale/issues/4636)** (4 comments)  
   *agent‑ready, tui, subagents, ux*  
   Goal: render one ordered Work projection with active/needs‑input count, unambiguous agent rows, and compact semantic activity.

9. **[#4647 – Coordinate decisions, context, write scopes, neutral fan‑in](https://github.com/Hmbown/CodeWhale/issues/4647)** (4 comments)  
   *context, workflow‑runtime, subagents*  
   Contract for bounded decision records, scope collision detection, and neutral reconciliation for parallel work.

10. **[#4605 – Enter key send lag – UI freezes 200–1200ms](https://github.com/Hmbown/CodeWhale/issues/4605)** (3 comments)  
    *bug, performance, regression*  
    Unfixed across ≥3 minor versions. Pressing Enter to send freezes the UI. Fixed today by PR #4654.

## Key PR Progress

1. **[#4675 – Integrate CodeWhale v0.9.1 runtime and release surface](https://github.com/Hmbown/CodeWhale/pull/4675)**  
   Lands the final runtime simplification, empty‑Work fix, and new TUI color grammar (cool mode colors, warm permission echoes). The core release integration.

2. **[#4673 – fix(shell): default no‑cwd shell commands to context.workspace](https://github.com/Hmbown/CodeWhale/pull/4673)**  
   Fixes #4674: sub‑agent BashTool runs commands in parent checkout when `cwd` is omitted. Now defaults to sub‑agent worktree.

3. **[#4654 – fix(tui): acknowledge Enter before slow send prep](https://github.com/Hmbown/CodeWhale/pull/4654) by @SamhandsomeLee**  
   Addresses #4605: UI now shows a “Preparing” state immediately on Enter, clearing the lag perception. Community contribution.

4. **[#4653 – test(tui): lock long‑output transcript scrolling with PTY scenario](https://github.com/Hmbown/CodeWhale/pull/4653)**  
   Adds end‑to‑end test for long output (#4603) using a sealed loopback – verifies scrolling works across ≥3 viewports.

5. **[#4652 – feat(cli): add public `--no-project-config` for reproducible headless exec](https://github.com/Hmbown/CodeWhale/pull/4652)**  
   Enables deterministic config surface for headless use, supporting the Verifiers harness integration (issue #4641).

6. **[#4658 – feat(runtime-api): add provider registry + switch endpoints](https://github.com/Hmbown/CodeWhale/pull/4658) by @gaord**  
   Three new endpoints for dynamic provider/model picker – replaces fragile `setConfig` flow. Community contribution.

7. **[#4657 – fix(streaming): report progress on idle timeouts](https://github.com/Hmbown/CodeWhale/pull/4657) by @h3c-hexin**  
   Emits byte‑count and timing telemetry on Chat Completions SSE idle‑timeout, distinguishing prefill stalls from mid‑stream failures.

8. **[#4656 – fix(route): honor explicit limits for unknown local models](https://github.com/Hmbown/CodeWhale/pull/4656) by @h3c-hexin**  
   Self‑hosted alias routes no longer capped at 4K fallback; explicit output limits are respected. Fixes #4655.

9. **[#4613 – fix(tui): sanitize Moonshot tool parameters per MFJS spec](https://github.com/Hmbown/CodeWhale/pull/4613) by @bistack**  
   Removes root‑level `anyOf`/`oneOf` from tool schemas – Moonshot/Kimi requires `type:"object"` root. Community contribution.

10. **[#4046 – Layer 5.1: User command registry and loading boundary](https://github.com/Hmbown/CodeWhale/pull/4046) by @aboimpinto**  
    Verifies user‑defined Markdown/frontmatter command boundary already satisfies all acceptance criteria – no production code changes needed.

## Feature Request Trends

- **UI/UX improvements:** Copy output, pop‑up visibility, long‑output scrolling, and send‑lag elimination dominate recent requests. The v0.9.1 cycle addresses several but open issues remain.
- **Permission & modality contracts:** Multiple issues propose typed permission resolution (Ask/Auto‑Review/Full Access) and durable mode state – central to the agent‑ready roadmap.
- **Sub‑agent orchestration:** Truthful work queues, decision coordination, scope collision detection, and unified Bash tool are being consolidated into a single contract.
- **Provider flexibility:** Self‑hosted model limits, dynamic provider switching, and local model catalog updates (e.g., TelecomJS, Kimi‑style config) are recurring themes.
- **Skill & workflow management:** `/skills` as the single surface for discovery, install, audit, and trust; also automated dev‑environment sync skills.

## Developer Pain Points

- **Enter‑key freeze** – a multi‑version regression (0.6.x through 0.9.0) that finally received a fix today.
- **Sub‑agent worktree isolation** – `BashTool` ignoring `context.workspace` forced contributors to work around the bug; now patched.
- **Provider configuration fragility** – the multi‑step `setConfig` process clobbers settings; new runtime API endpoints aim to replace it.
- **Model output limits for self‑hosted routes** – unknown aliases incorrectly capped at 4K tokens, causing silent truncation.
- **Tool parameter incompatibility** – Moonshot/Kimi rejects standard JSON Schema compositions, requiring sanitisation.
- **High project velocity** – 10+ PRs/day makes it hard for new contributors to stay in sync; the proposed dev

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*