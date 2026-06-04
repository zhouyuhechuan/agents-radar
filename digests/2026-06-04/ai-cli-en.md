# AI CLI Tools Community Digest 2026-06-04

> Generated: 2026-06-04 02:55 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report — 2026-06-04

## 1. Ecosystem Overview

The AI CLI tooling ecosystem is experiencing a phase of **maturation under strain** — rapid feature iteration across nine major tools is colliding with reliability, security, and UX debt that paying users are increasingly unwilling to tolerate. Session continuity, provider authentication, and context-window management emerged as universal pain points, while platform-specific regressions (particularly Windows and non-US keyboard layouts) continue to fragment user satisfaction. A notable bifurcation is forming between **enterprise-security-conscious tools** (Gemini CLI, Copilot CLI, OpenCode) that are hardening sandboxing and credential management, and **consumer-first tools** (Kimi Code CLI, DeepSeek TUI) focused on polish and workflow innovation. The ecosystem is also seeing early signals of **model-provider lock-in fatigue**, with multiple communities actively demanding broader backend compatibility and API transparency.

---

## 2. Activity Comparison

| Tool | Issues Activity (Top 24h) | PR Activity (24h) | Release Status | Community Engagement Intensity |
|------|---------------------------|-------------------|----------------|-------------------------------|
| **Claude Code** | 10 hot issues (high: 173 comments on billing bug) | 4 PRs (2 merged) | ✅ v2.1.162 stable | **Very High** — billing/data-loss crises driving sustained engagement |
| **OpenAI Codex** | 10 hot issues (597 comments on token burning) | 10 PRs (active stack) | ✅ rust-v0.137.0 stable | **Very High** — token-burning bug is dominant ecosystem event |
| **Gemini CLI** | 10 hot issues (7 new: agent reliability, security) | 10 PRs (4 merged into release branch) | ✅ v0.46.0-preview.1 patch | **High** — focused on security hardening and agent stability |
| **GitHub Copilot CLI** | 10 hot issues (keyboard regressions dominant) | 1 PR (mysterious, no description) | ❌ No release | **Moderate** — niche issues but high per-user frustration |
| **Kimi Code CLI** | 8 issues (session management focus) | 1 PR (merged UX improvement) | ❌ No release | **Low** — relatively quiet; small community |
| **OpenCode** | 10 hot issues (v1.15.13 MCP GUI breakage wave) | 10 PRs (draft V2 runtime, command registry) | ❌ No release | **High** — architectural changes driving major PR activity |
| **Pi** | 10 hot issues (provider bugs, image handling) | 10 PRs (rapid bug fixes) | ❌ No release | **High** — fast iteration cadence, many small fixes |
| **Qwen Code** | 10 hot issues (model display, daemon stability) | 10 PRs (daemon-mode feature batch pending) | ✅ v0.17.1 stable | **High** — Asia-Pacific growth, daemon-mode roadmap |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues (rebranding, WhaleFlow planning) | 10 PRs (branding, auth fixes) | ✅ v0.8.51–v0.8.53 | **Moderate** — rebranding phase, planning major v0.9.0 |

**Key observation**: OpenAI Codex and Claude Code dominate raw engagement (hundreds of comments on single issues), while Gemini CLI, OpenCode, and Qwen Code show the highest PR velocity for structural improvements.

---

## 3. Shared Feature Directions

**Requirements appearing across multiple tool communities:**

| Theme | Affected Tools | Specific Needs |
|-------|---------------|----------------|
| **Session continuity & context limits** | Claude Code, Gemini CLI, Kimi Code CLI, OpenCode, Copilot CLI | Seamless continuation after context-limit hits; progressive warnings; avoid silent truncation. Claude Code #13354 (116 👍), Gemini CLI #22323, Kimi Code #2420, Copilot CLI #3539. |
| **Authentication & account management** | Claude Code, OpenAI Codex, Gemini CLI, Qwen Code, DeepSeek TUI | Multi-account rotation, recovery from inaccessible phone numbers, credential state visibility. OpenAI Codex #25749 (SMS lockout), Claude Code #5088 (account disabled after payment), Gemini CLI #26525 (secret redaction delay). |
| **Context-window observability** | Copilot CLI, OpenCode, Gemini CLI | Token usage breakdowns (input vs. output), system prompt visibility, compaction analytics. Copilot CLI #3612, OpenCode #30649 (unbounded cache growth), Gemini CLI #22745 (AST-aware efficiency). |
| **MCP/plugin reliability** | OpenCode, Qwen Code, Copilot CLI, Pi | Tools not propagating to model despite "Connected" UI, hook system incompleteness, tool name collisions crashing startup. OpenCode #30265 (v1.15.13 MCP breakage), Qwen Code #4218, Copilot CLI #3665, Pi #5316. |
| **Security sandboxing & credential guard** | Gemini CLI, Copilot CLI, OpenCode, Claude Code (PR) | Filesystem isolation, credential pattern scanning before write, SSRF prevention, destructive-command warnings. Gemini CLI #27472 (IPI truncation lockout), Copilot CLI #892 (sandbox mode, 49 👍), Claude Code PR #62099 (credential-guard plugin). |
| **TUI/CLI UX improvements** | All tools | Clean copy (no indentation artifacts), paste in menus, keyboard layout compatibility, auto-scroll control, LaTeX rendering. OpenAI Codex #12200, Copilot CLI #1481, #1999, Gemini CLI #25786, Claude Code #16446. |
| **Agent workflow orchestration** | Claude Code, Gemini CLI, DeepSeek TUI, OpenCode | Subagent visibility, background agent debugging, structured orchestration as first-class behavior. Claude Code #64767 (agent orchestration), DeepSeek TUI #2667 (WhaleFlow workflow engine), OpenCode #30632 (V2 session runtime). |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|--------------------|---------------|----------|-----|-----------|---------------|
| **Primary user base** | Serious solo devs, small teams | Enterprise & subscription users | Google Cloud/enterprise | GitHub ecosystem (Windows-heavy) | Multimodal creators, Chinese market | Open-source power users, self-hosters | FOSS power users, Anthropic-heavy | Chinese & Asia-Pacific devs | OSS tinkerers, multi-provider |
| **Core differentiator** | Most mature plugin/agent ecosystem | Largest context window, OAuth MFA depth | Strong security posture, AST-aware | Deep GitHub integration, pre-existing user base | Multimodal first (image+text as blocks) | Architectural innovation (V2 runtime, Effect-native) | Fastest bug-fix cadence, broadest provider support | Strong roadmap (daemon, OTel), Chinese localization | WhaleFlow workflow engine, Hugging Face integration |
| **Stability signal** | **Deteriorating** — billing/auth crisis, data-loss systemic | **Strained** — token-burning bug is ecosystem dominant | **Improving** — security hardening in flight | **Stale** — old issues, slow patch cadence | **Stable but quiet** — small community, few updates | **Volatile** — major architectural churn (V2) with regressions | **Healthy but reactive** — fast patches, focused fixes | **Proactive** — daemon-mode roadmap, telemetry push | **Transitional** — rebranding, planning major v0.9.0 |
| **Windows support maturity** | Weak (LSP issues, GitHub connector) | Moderate (sandbox ARM64 buggy, UI rendering) | Moderate (path comparisons fixed) | **Weakest** (clipboard, hooks, paste, uninstall all broken) | Unknown (no Windows-specific issues) | Weak (clipboard not working, MCP GUI broken) | Moderate (Fireworks provider fix) | Weak (MCP tools not propagating, SMB paths) | Moderate (rendering bug on Windows) |
| **Enterprise readiness** | Low (billing/auth failures, data loss) | Moderate (OAuth MFA but phone lockout) | **High** (sandbox, credential guard, approval workflows) | Low (no sandbox mode, keybinding failures) | Low (small community, no enterprise features) | Moderate (command registry, workspace isolation) | Low (extension collision = crash, no sandbox) | Moderate (telemetry, but daemon still developing) | Low (rebranding, pre-v0.9.0) |

---

## 5. Community Momentum & Maturity

### Tier 1: Dominant Engagement, High Risk/High Reward

- **OpenAI Codex** — The most active community (597 comments on a single issue). Token-burning bug (#14593) is a **potential crisis** — if unresolved, it erodes trust in the entire platform. However, PR velocity is high (10 PRs), and prompt-hook infrastructure (#24634) signals long-term architectural investment.
- **Claude Code** — Billing/data-loss crises (#5088, #59248, #13354) are generating intense vocal engagement. The credential-guard plugin PR (#62099) and Socratic mentoring plugin (#22919) show plugin ecosystem is alive, but **open issue count is alarming** — the oncall team appears overwhelmed.

### Tier 2: Rapid Iteration, Growing Communities

- **Gemini CLI** — Strong security focus (SSRF fix, IPI truncation lockout, path traversal prevention) and agent-stability fixes suggest **enterprise-grade maturity push**. PR #27502 (terminal resize crash fix) and #27619 (atomic MCP discovery) are high-quality engineering. Community growth is steady from the Google ecosystem.
- **OpenCode** — Despite Desktop v1.15.13 MCP GUI breakage, the **V2 session runtime (#30632) and command registry (#30624)** are significant architectural steps. The community is technically sophisticated but small. The 161 👍 for voice input (#4695) shows strong feature demand.
- **Qwen Code** — Daemon mode (PR #4490, #4751) and OpenTelemetry (#4749) signal **production-readiness investment**. v0.17.1 stable release with a targeted fix shows disciplined release management. Chinese-language issue growth suggests expanding regional adoption.

### Tier 3: Niche but Focused

- **Pi** — High PR velocity (10 PRs in 24h) but each fix is small. The Anthropic thinking-block bug (#5223) is critical for Claude users. Shows **responsive maintenance** but lacks a clear feature roadmap beyond provider support.
- **DeepSeek TUI (CodeWhale)** — The rebranding to CodeWhale is disruptive but necessary. The WhaleFlow epic (#2667) and Hugging Face integration (#2705) are ambitious for v0.9.0. Current v0.8.x releases are stabilization-focused.

### Tier 4: Stagnant/Uncertain

- **GitHub Copilot CLI** — One PR with no description (#3651) in 24h is a **red flag for community health**. Keyboard regressions (#1481, #1999, #3648) are old and unresolved. Sandbox mode (#892, 49 👍) remains unimplemented. The tool feels **neglected** relative to its GitHub ecosystem potential.
- **Kimi Code CLI** — Quietest tool in the cohort. Only one PR merged, 8 issues with zero engagement. Session resume bug (#2420) is critical but attracts no comments. **Suggests a very small or disengaged community.**

---

## 6. Trend Signals

### Industry-wide Trends from Community Feedback

1. **Security is becoming a first-class requirement**, not a nice-to-have. Gemini CLI's credential-guard PR, Copilot CLI's sandbox-mode demand, and OpenCode's auth.json incident (#30616) all point to **users demanding AI tooling with zero-trust assumptions**. Expect sandboxing, credential scanning, and file-system isolation to become table stakes in 2026–2027.

2. **Context-window anxiety is reaching a tipping point.** Developers are acutely aware that system prompts, MCP configurations, and plugin overhead consume 50–70% of available tokens before any user input (Copilot CLI #3539). **Tools that provide token-usage transparency, dynamic pruning, and editable system prompts will gain competitive advantage.** OpenCode's cache.read unbounded growth (#30649) is a systemic design flaw that other tools should audit.

3. **Authentication flows are a critical churn risk.** OpenAI Codex's phone-verification lockout (#25749), Claude Code's account-disabled-after-payment (#5088), and Gemini CLI's credential-redaction delay (#26525) all demonstrate that **auth is the highest-leverage UX surface** — one bad flow can lock paying users out of the entire product.

4. **Platform-specific reliability is fragmenting user trust.** Windows support is the worst across the board (broken clipboard, MCP, hooks, paste, uninstallation). Non-US keyboard layouts (German, CJK) are systematically broken. **Tools that invest in cross-platform QA and keyboard-layout testing will capture the users being abandoned by current leaders.**

5. **Agent orchestration is the next frontier.** Claude Code's agent orchestration request (#64767), Gemini CLI's subagent recovery bug (#22323), and DeepSeek TUI's WhaleFlow engine (#2667) all indicate that **users want structured, debuggable, multi-agent workflows** — not just chat. The ability to fan out tasks, observe subagent progress, and recover from failures is becoming a differentiator.

6. **"Model compliance" (tasks marked done without verification)** is an emerging trust crisis. Claude Code #60177 (51 commits, 12 days, still broken) and Gemini CLI #22323 (false success after MAX_TURNS) show that **AI agents claiming completion without actual verification is the most dangerous failure mode** for autonomous coding workflows. Expect tool-specific testing frameworks and self-verification hooks to emerge.

7. **OpenTelemetry and observability are moving from nice-to-have to core infrastructure.** Qwen Code's OTel daemon metrics (#4749), Copilot CLI's token usage breakdown demand (#3612), and Gemini CLI's component-level evaluation epic (#24353) all signal that **production users need visibility into tool performance**

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data snapshot:** github.com/anthropics/skills – 2026-06-04  

---

## 1. Top Skills Ranking (Most-Discussed Pull Requests)  

The following PRs have attracted the highest community engagement (sorted by comment count) and represent the most actively debated Skill proposals:

### #1 – **Document Typography Skill** (#514)  
*Status: Open • Created 2026-03-04*  
A quality-control Skill that prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. The discussion highlights that these typographic issues affect *every* document Claude produces, and the community sees this as a low-effort, high-impact fix.  
[PR #514](https://github.com/anthropics/skills/pull/514)

### #2 – **ODT / OpenDocument Skill** (#486)  
*Status: Open • Created 2026-03-01*  
Provides full round-trip support for OpenDocument formats (.odt, .ods): creation, template filling, parsing to HTML. The conversation centers on the lack of native LibreOffice/ODF support in Claude Code and the need for a reliable bridge to open-source office tools.  
[PR #486](https://github.com/anthropics/skills/pull/486)

### #3 – **Improved Frontend-Design Skill** (#210)  
*Status: Open • Created 2026-01-05*  
Overhauls the existing `frontend-design` Skill to be more actionable and specific. The discussion focuses on making every instruction executable in a single conversation and eliminating vague guidance.  
[PR #210](https://github.com/anthropics/skills/pull/210)

### #4 – **Skill-Quality-Analyzer & Skill-Security-Analyzer** (#83)  
*Status: Open • Created 2025-11-06*  
Two meta-skills for evaluating Skill quality (structure, documentation, UX) and security (unsafe patterns, prompt injection). Community debate centers on whether these should live in the official repo or remain as third-party tools.  
[PR #83](https://github.com/anthropics/skills/pull/83)

### #5 – **PDF Skill Case-Sensitivity Fix** (#538)  
*Status: Open • Created 2026-03-06*  
Fixes 8 case-sensitive file references in the PDF Skill’s SKILL.md that broke on Linux/macOS. Despite being a simple bugfix, it has generated substantial discussion about cross-platform testing practices.  
[PR #538](https://github.com/anthropics/skills/pull/538)

### #6 – **Skill-Creator: Unquoted YAML Warning** (#539)  
*Status: Open • Created 2026-03-06*  
Adds pre-parse validation to catch unquoted `description` fields containing colons. The conversation reveals this is a recurring pain point for Skill authors.  
[PR #539](https://github.com/anthropics/skills/pull/539)

### #7 – **DOCX Tracked Change ID Collision** (#541)  
*Status: Open • Created 2026-03-06*  
Prevents document corruption when the DOCX Skill adds tracked changes to files with existing bookmarks. Community members have reported real-world corruption cases.  
[PR #541](https://github.com/anthropics/skills/pull/541)

### #8 – **Feature-Dev Workflow Phase Skipping Fix** (#363)  
*Status: Open • Created 2026-02-09*  
Addresses a `TodoWrite` overwrite bug that caused Quality Review and Summary phases to be skipped during `/feature-dev`. The discussion highlights the complexity of maintaining reliable workflow Skills.  
[PR #363](https://github.com/anthropics/skills/pull/363)

---

## 2. Community Demand Trends (from Issues)  

The most active issues reveal four clear demand vectors:

### 📊 **Org-Wide Skill Sharing & Management**  
**Issue #228 (13 comments, 7 👍)** – Users want a native way to share Skills within organizations without manual file transfers. This is the single most upvoted feature request.  
[Issue #228](https://github.com/anthropics/skills/issues/228)

### 🪟 **Windows Compatibility**  
Multiple issues (e.g., #556, #1102) and several PRs (#1050, #1099) report that `skill-creator` and evaluation scripts are broken on Windows. Users on Windows are unable to use core tooling.  
[Issue #556](https://github.com/anthropics/skills/issues/556)

### 🔒 **Security & Trust Boundaries**  
**Issue #492 (7 comments)** – Concerns about community Skills distributed under the `anthropic/` namespace impersonating official ones. Users request better provenance and sandboxing.  
[Issue #492](https://github.com/anthropics/skills/issues/492)

### 📦 **Deduplication & Plugin Cleanup**  
**Issue #189 (6 comments, 8 👍)** – The `document-skills` and `example-skills` plugins install identical content. The community wants a single consolidated Skill set with clear boundaries.  
[Issue #189](https://github.com/anthropics/skills/issues/189)

### 🔧 **Evaluation & Testing Infrastructure**  
**Issue #556 (9 comments) and others** – `run_eval.py` fails to trigger skills when using `claude -p`, causing 0% trigger rates. This blocks automated quality assurance.  
[Issue #556](https://github.com/anthropics/skills/issues/556)

*Other notable requests:* multi-file preloading for Skill reference files (#1220), MCP data compression (#1102), and governance/safety patterns (#412).

---

## 3. High-Potential Pending Skills (Active PRs Not Yet Merged)  

These PRs have lively discussions and appear close to landing:

- **Agent-Creator Meta-Skill (#1140)** – Creates task-specific agent sets and fixes multi-tool evaluation. Updated recently (2026-06-02).  
  [PR #1140](https://github.com/anthropics/skills/pull/1140)

- **Testing-Patterns Skill (#723)** – Covers testing trophy model, unit/component/E2E patterns. Active discussion through April 2026.  
  [PR #723](https://github.com/anthropics/skills/pull/723)

- **ServiceNow Platform Skill (#568)** – Broad ITSM/ITOM/SecOps coverage. Still open with recent updates.  
  [PR #568](https://github.com/anthropics/skills/pull/568)

- **AURELION Skill Suite (#444)** – Cognitive framework with kernel, advisor, agent, and memory Skills. Updated as recently as May 2026.  
  [PR #444](https://github.com/anthropics/skills/pull/444)

- **Windows Subprocess/Encoding Fix (#1050)** – Two 1-line fixes for `run_loop.py` on Windows 11. Highly awaited by the Windows cohort.  
  [PR #1050](https://github.com/anthropics/skills/pull/1050)

---

## 4. Skills Ecosystem Insight  

**The community’s most concentrated demand is for robust document processing Skills (typography, ODF, PDF, DOCX) that work reliably across platforms, coupled with developer tooling improvements (Windows compatibility, evaluation scripts, and security auditing) to make the Skill ecosystem production-ready.**

---

# Claude Code Community Digest — 2026-06-04

## Today’s Highlights
Version 2.1.162 shipped with a small but useful addition to `claude agents --json`, while the community continues to grapple with a high‑severity billing issue (#5088) and growing frustration over silent session transcript deletion. A credential‑guard plugin PR aims to prevent hardcoded secrets from being written by Claude, and the number of open issues remains elevated, with several long‑standing bugs still unresolved.

## Releases

### v2.1.162
- `claude agents --json` now includes a `waitingFor` field that surfaces what a waiting session is blocked on (e.g., a permission prompt).
- Listing `Grep`/`Glob` explicitly via `--tools` now correctly provides dedicated search tools on native builds with embedded search (previously these names were silently ignored).

No other releases in the last 24 hours.

## Hot Issues (Top 10 by Community Activity & Impact)

### [#5088 – Claude Account Disabled After Payment for Claude Code Max 5x Plan](https://github.com/anthropics/claude-code/issues/5088)
**173 comments · 58 👍** | `bug`, `area:cost`, `area:auth`, `oncall`
A paying user reports that immediately after purchasing the Max 5x plan their account was disabled, locking them out of both Claude Code and Claude.ai. The sheer volume of comments suggests many affected users. Anthropic has tagged it `oncall`.

### [#13354 – [FEATURE] Continue when the session limit reached](https://github.com/anthropics/claude-code/issues/13354)
**56 comments · 116 👍** | `enhancement`, `area:tui`
One of the most upvoted feature requests: the ability to seamlessly continue work when the session limit is hit rather than losing context. Users describe losing hours of work.

### [#34255 – Remote Control: automatic reconnection doesn't work](https://github.com/anthropics/claude-code/issues/34255)
**48 comments · 86 👍** | `bug`, `platform:macos`, `platform:ios`
Remote Control sessions drop silently with no automatic recovery. Despite being open since March, the issue remains unaddressed, frustrating users who rely on cross‑device workflows.

### [#16446 – LaTeX rendering in "Claude Code for VS Code" plugin](https://github.com/anthropics/claude-code/issues/16446)
**33 comments · 93 👍** | `enhancement`, `area:ide`
Users heavily involved in mathematics, physics, or documentation want proper LaTeX rendering inside the VS Code chat panel. High reaction count signals strong demand.

### [#22264 – Sibling tool call errored: parallel tool calls cascade-fail](https://github.com/anthropics/claude-code/issues/22264)
**33 comments · 61 👍** | `bug`, `has repro`, `area:tools`, `area:core`
When multiple tools are called in parallel and one fails, all sibling calls are cancelled with a vague `Sibling tool call errored` message. This forces unnecessary retries and wastes API credits.

### [#17149 – LSP workspaceSymbol operation sends empty query parameter](https://github.com/anthropics/claude-code/issues/17149)
**30 comments · 20 👍** | `bug`, `has repro`, `platform:windows`, `area:tools`
Windows users experience broken LSP symbol search because the CLI sends an empty query string. Has reproduction steps but no fix yet.

### [#59248 – Silent retention cleanup deletes session transcripts with no warning](https://github.com/anthropics/claude-code/issues/59248)
**12 comments · 4 👍** | `bug`, `data-loss`, `platform:macos`, `area:core`
A user lost all conversation transcripts older than the current session with no opt‑in, warning, or recovery path. Combined with #62476 (30‑day retention default), this is a significant data‑loss concern.

### [#63396 – CLI builds invalid request after context ops (compact/clear/model-switch)](https://github.com/anthropics/claude-code/issues/63396)
**7 comments · 4 👍** | `bug`, `has repro`, `platform:macos`, `area:core`
After compaction or model‑switch, the CLI constructs an API‑rejected HTTP 400 request, often weding the session permanently. Two variants reported; both are terminal.

### [#60177 – Claude marks tasks done without testing — 12 days, 51 commits, still broken (Opus 4.x)](https://github.com/anthropics/claude-code/issues/60177)
**7 comments · 1 👍** | `bug`, `area:model`, `api:anthropic`
A developer describes how Claude repeatedly claims a task is complete without actually verifying it, leading to 51 commits over 12 days while the core issue remained unfixed. Raises concerns about model reliability for autonomous agents.

### [#61682 – GitHub connector shows "Connected" but exposes no tools in Cowork (Windows 11)](https://github.com/anthropics/claude-code/issues/61682)
**6 comments · 1 👍** | `bug`, `platform:windows`, `area:cowork`, `area:desktop`
Despite showing “Connected” status, the GitHub integration in Cowork offers zero tools. A PowerShell diagnostic script has been proposed in PR #61691, but the root cause remains open across multiple related issues.

## Key PR Progress

*Only 4 PRs were updated in the last 24 hours, so all are listed below.*

### [#65223 – Spelling: Fix typo in security guidance plugin](https://github.com/anthropics/claude-code/pull/65223)
**CLOSED** | A one‑line fix correcting “reqwest” to “request” in the security guidance plugin.

### [#61691 – Add diagnostic script for GitHub connector showing 'Connected' but no tools](https://github.com/anthropics/claude-code/pull/61691)
**OPEN** (since May 23) | A PowerShell script to diagnose and repair the Windows GitHub MCP connector bug (#61682). Includes root‑cause analysis referencing earlier issues.

### [#62099 – Add credential-guard plugin for hardcoded secret detection](https://github.com/anthropics/claude-code/pull/62099)
**OPEN** (since May 24) | A new plugin using `PreToolUse` hooks to scan `Write`, `Edit`, `MultiEdit`, and `Bash` (redirect/heredoc) calls for 20+ credential patterns before content is written. Addresses #62095.

### [#22919 – feat(plugins): add collab plugin for Socratic mentoring mode](https://github.com/anthropics/claude-code/pull/22919)
**CLOSED** (merged) | Adds a **collab** plugin that transforms Claude into a Socratic mentor: it guides developers with questions instead of writing code. This was a long‑standing community request.

## Feature Request Trends

The most demanded features cluster in a few areas:

- **Session continuity** – Multiple requests for continuing work after hitting a context or usage limit instead of losing the session (#13354, #64850).
- **Richer IDE integration** – LaTeX rendering (#16446), desktop notifications for task completion and limit resets (#65242).
- **Agent orchestration** – Structured orchestration as first‑class agent behaviour (#64767) and better debugging/visibility into background sub‑agents (#65222).
- **Plugin ecosystem** – The credential‑guard PR (#62099) and Socratic mentoring plugin (#22919) reflect growing interest in custom hooks and enforcing policies.

## Developer Pain Points

Recurring themes that generated the most frustration this week:

1. **Silent data loss** – Session transcripts are deleted after 30 days without warning, and retention cleanup can wipe all older transcripts unexpectedly (#59248, #62476).
2. **Billing/auth failures** – Accounts disabled after payment (#5088) and duplicate auth tokens causing incorrect billing (#64933).
3. **Remote Control instability** – Dropped connections that never recover (#34255) and read‑only sessions on mobile (#62284).
4. **Cascading tool failures** – Parallel tool calls aborting on a single error (#22264).
5. **Context‑limit UX** – No progressive warnings, misleading error messages, and cascade‑fail during compaction (#64850, #63396).
6. **Model compliance** – Claude marking tasks done without testing (#60177) and ignoring explicit instructions (#57200).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-04

## Today’s Highlights
The community is intensely focused on a massive rate‑limit/token‑burning bug ([#14593](#14593)) with nearly 600 comments, while a fresh wave of phone‑verification login blockers ([#25749](#25749), [#25837](#25837), [#25820](#25820)) is preventing paying users from accessing Codex at all. On the positive side, the **rust-v0.137.0** release brings TUI improvements (F13‑F24 keys, paste in searchable menus, compact reasoning status) and new enterprise admin controls for credit limits and cloud‑managed config bundles. PR activity is high around authentication logging, prompt hooks, MITM CA bundling, and terminal visualization features.

## Releases

### **rust-v0.137.0** (stable)
- **New Features**
  - TUI controls now support **F13‑F24 keybindings**, paste in searchable menus, and a compact reasoning‑only status/title item ([#25329](#), [#25400](#), [#25504](#)).
  - Enterprise/admin flows show **monthly credit limits** and can apply **cloud‑managed config bundles** including EDU workspaces ([#24812](#), [#2](#)).

### **rust-v0.137.0-alpha.5**
- Alpha release (no detailed changelog).

## Hot Issues (Top 10 by Community Engagement)

1. **[#14593] Burning tokens very fast**  
   - **Why it matters**: Business subscribers report unexplained token consumption far exceeding normal use. The sheer volume of 597 comments and 262 👍 signals a widespread, severe issue that erodes user trust.  
   - [OpenAI Codex Issue #14593](https://github.com/openai/codex/issues/14593)

2. **[#25144] Add option to disable automatic conversion of long pasted prompts into .txt attachments**  
   - **Why it matters**: Users pasting structured prompts find them converted to unusable `.txt` files. With 49 comments and 56 👍, this change would improve the core editing workflow.  
   - [OpenAI Codex Issue #25144](https://github.com/openai/codex/issues/25144)

3. **[#25749] Codex requires verification of an inaccessible legacy phone number**  
   - **Why it matters**: Users with valid Google OAuth and MFA are locked out because Codex demands SMS verification on a phone number they can no longer access. No recovery path exists. 34 comments, 17 👍.  
   - [OpenAI Codex Issue #25749](https://github.com/openai/codex/issues/25749)

4. **[#21128] Desktop silently hides project conversations outside the global recent‑50 window**  
   - **Why it matters**: Old but important conversations become invisible, breaking the “working memory” promise for real projects. 19 comments, 16 👍.  
   - [OpenAI Codex Issue #21128](https://github.com/openai/codex/issues/21128)

5. **[#24260] gpt‑5.5 xhigh turn stalled 30 minutes before first output**  
   - **Why it matters**: Users on high‑reasoning models face unexplained 30‑minute delays before any response appears. 16 comments, 9 👍.  
   - [OpenAI Codex Issue #24260](https://github.com/openai/codex/issues/24260)

6. **[#23979] Local project conversation history missing after update – threads still exist in state_5.sqlite**  
   - **Why it matters**: Update-induced data loss is a critical bug. Even though data remains on disk, it’s invisible in the UI. 15 comments, 3 👍.  
   - [OpenAI Codex Issue #23979](https://github.com/openai/codex/issues/23979)

7. **[#24259] Windows sandbox intermittently fails with `spawn setup refresh` on ARM64**  
   - **Why it matters**: Sandbox reliability on Windows ARM64 is broken, affecting a growing number of users. 12 comments, 9 👍.  
   - [OpenAI Codex Issue #24259](https://github.com/openai/codex/issues/24259)

8. **[#25249] Semi‑transparent sidebar causes transparent/undrawn regions when maximized**  
   - **Why it matters**: Windows UI rendering bug makes the maximized app unusable. 12 comments, 0 👍 (low engagement but high severity).  
   - [OpenAI Codex Issue #25249](https://github.com/openai/codex/issues/25249)

9. **[#9648] Feature: Multi‑account ChatGPT OAuth rotation and management**  
   - **Why it matters**: Users want automatic failover between accounts when hitting rate limits. 11 comments, 12 👍 – a popular enhancement.  
   - [OpenAI Codex Issue #9648](https://github.com/openai/codex/issues/9648)

10. **[#12200] Clean Copy for multiline and soft‑wrapped output in CLI TUI**  
    - **Why it matters**: Copying code from the TUI introduces unwanted indentation and breaks HEREDOCs, frustrating CLI users. 10 comments, 22 👍.  
    - [OpenAI Codex Issue #12200](https://github.com/openai/codex/issues/12200)

## Key PR Progress (Top 10 Important Changes)

1. **[#26286] Materialize child MITM CA bundles**  
   - Materializes per‑child CA overrides for managed MITM, part of a stack improving sandbox security.  
   - [OpenAI Codex PR #26286](https://github.com/openai/codex/pull/26286)

2. **[#26041] Add app‑server background terminal process APIs**  
   - New v2 APIs to list/terminate background terminals via app‑server, replacing unreliable local process tree guesses.  
   - [OpenAI Codex PR #26041](https://github.com/openai/codex/pull/26041)

3. **[#26013] Gate terminal visualization instructions in TUI**  
   - Adds an under‑development feature flag for terminal visualization instructions, keeping them off by default.  
   - [OpenAI Codex PR #26013](https://github.com/openai/codex/pull/26013)

4. **[#25946] Report compaction request token counts**  
   - Improves compaction analytics by using actual request token counts instead of diverging session snapshots.  
   - [OpenAI Codex PR #25946](https://github.com/openai/codex/pull/25946)

5. **[#26252] Sign macOS release artifacts with Azure Key Vault**  
   - Moves code signing private key to Azure Key Vault, improving supply chain security for public releases.  
   - [OpenAI Codex PR #26252](https://github.com/openai/codex/pull/26252)

6. **[#26276] Propagate auth session logging ID in ChatGPT login**  
   - Adds a correlation key so Codex‑side login failures can be joined with auth‑service logs, improving debuggability.  
   - [OpenAI Codex PR #26276](https://github.com/openai/codex/pull/26276)

7. **[#26189] Add package path from install context**  
   - Ensures helper binaries (e.g., bundled `rg`) are on `PATH` for standalone launches, fixing a long‑standing omission.  
   - [OpenAI Codex PR #26189](https://github.com/openai/codex/pull/26189)

8. **[#26291] Optimize external agent session detection**  
   - Performance optimization for detecting external agent sessions.  
   - [OpenAI Codex PR #26291](https://github.com/openai/codex/pull/26291)

9. **[#24634] Add prompt hooks**  
   - New hook infrastructure for prompt events, with semantics defined for side requests without breaking main conversation state.  
   - [OpenAI Codex PR #24634](https://github.com/openai/codex/pull/24634)

10. **[#25704] Responses codex strict mode**  
    - Introduces a strict mode for the `responses` API, likely tightening adherence to schemas or error handling.  
    - [OpenAI Codex PR #25704](https://github.com/openai/codex/pull/25704)

## Feature Request Trends

The most‑requested feature directions from this week’s issues are:

- **Authentication & Account Management**  
  - Multi‑account OAuth rotation to bypass rate limits ([#9648](#9648)).  
  - Ability to change phone number without recovery dead‑end ([#25749](#25749), [#25837](#25837)).  
  - MCP server OAuth status visibility in settings ([#23453](#23453)).

- **Conversation & History Management**  
  - Show archived chats muted in the sidebar instead of hiding them ([#20732](#20732)).  
  - Persist all conversations beyond the global 50‑item window ([#21128](#21128)).  
  - Option to disable automatic conversion of long prompts to `.txt` ([#25144](#25144)).

- **CLI/TUI Usability**  
  - “Clean Copy” for multiline output that strips unwanted indentation and wrapping ([#12200](#12200)).  
  - iTerm2 tab‑status integration via OSC 21337 ([#25879](#25879)).  
  - Environment‑gated clipboard reader for headless environments ([#25465](#25465)).

- **Plugin & Skill Persistence**  
  - Computer Use plugin should survive app restarts ([#26296](#26296)).  
  - General stability of installed skills/plugins across sessions.

## Developer Pain Points

Recurring frustrations from the community this week:

- **Phone‑verification login blockage** – Multiple issues report that users with valid ChatGPT sessions cannot access Codex because it insists on SMS verification for a phone number they no longer control ([#25749](#25749), [#25837](#25837), [#25820](#25820), [#25765](#25765)). There is no account recovery path.

- **Token burning / rate limits** – Issue [#14593](#14593) dominates discussion, with many users seeing unsustainable token consumption on Business/Plus plans, often when not actively using the app ([#24818](#24818)).

- **Conversation data loss after updates** – Several reports of missing thread history after updating the desktop app, even though data exists on disk ([#23979](#23979), [#21128](#21128)).

- **Windows‑specific reliability** – Sandbox setup failures on ARM64 ([#24259](#24259)), UI rendering bugs with transparent sidebar ([#25249](#25249)), and excessive slowness ([#23198](#23198)) make Windows the most troubled platform.

- **Stuck subagent cards** – Completed or closed subagents remain visible in the UI indefinitely, cluttering the workspace ([#23930](#23930)).

- **Orphaned helper processes** – `SkyComputerUseClient` processes

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-04

## Today's Highlights

A patch release (v0.46.0-preview.1) landed today, cherry-picking a single fix from a release branch. The community continues to focus on agent reliability, with several high-priority issues around subagent recovery, shell execution hangs, and browser agent failures still open. Security hardening is also visible, with two open PRs addressing private-IP bypass and truncation lockout for tool confirmations.

## Releases

- **[v0.46.0-preview.1](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.1)** — Cherry-pick of commit `e4315b3` into the `release/v0.46.0-preview.0` branch. This is a targeted patch version; no further details on the fix content were provided in the release notes.

## Hot Issues

1. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**
   *P1 / area:agent / 7 comments* – Epic tracking the evolution from 76 behavioral eval tests to a full component-level evaluation framework across 6 Gemini models. Signals the team’s push toward systematic quality gates.

2. **[#22745 — Assess impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**
   *P2 / area:agent / 7 comments / 👍 1* – Investigates whether AST-aware tools can reduce token waste and misaligned reads. If proven effective, this could meaningfully improve agent efficiency and lower cost for large-codebase interactions.

3. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**
   *P1 / area:agent / 6 comments / 👍 2* – A deceptive bug: subagents report success when they actually hit the turn limit without doing analysis. This undermines trust in agent status reporting and could mask silent failures in automated workflows.

4. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**
   *P2 / area:agent / 6 comments* – Anecdotal but important: custom skills (gradle, git) are defined but rarely invoked autonomously. This limits the value of the skill ecosystem and suggests the agent’s tool-selection heuristics need refinement.

5. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**
   *P1 / area:core / 4 comments / 👍 3* – A persistent hang after trivial shell commands. High user frustration; the "Awaiting user input" state is a false positive that blocks further automation.

6. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**
   *P1 / area:agent / 4 comments / 👍 1* – Browser agent crashes on Wayland with “GOAL” termination. Wayland adoption is growing; this blocks a significant user segment.

7. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**
   *P2 / area:security / 3 comments* – Auto Memory sends transcript content to an extraction model before secrets are redacted. This is a latent data-exposure risk that the team is actively addressing.

8. **[#24246 — Gemini CLI encounters 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**
   *P2 / area:agent / 3 comments* – A hard limit on tool count triggers API errors. Suggests the tool selection mechanism does not prune aggressively enough for large skill installations.

9. **[#23571 — Model frequently creates tmp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)**
   *P2 / area:agent / 3 comments* – When shell execution is restricted, the model scatters temporary scripts across the filesystem. This creates cleanup overhead and masks the underlying need for better script-output management.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**
    *P2 / area:agent / 2 comments / 👍 1* – Reports of `git reset --force` and other destructive commands being used when safer alternatives exist. A request for safer defaults and warning prompts for high-risk operations.

## Key PR Progress

1. **[#27502 — Fix P1 crash during terminal resize (ioctl EBADF)](https://github.com/google-gemini/gemini-cli/pull/27502)**
   *P1 / area:core / size:m* – Fixes a race condition between shell exit and React’s useEffect resize callback causing terminal crashes. Directly addresses a high-severity user-facing crash.

2. **[#27472 — Enforce truncation lockout for tool confirmations to prevent IPI](https://github.com/google-gemini/gemini-cli/pull/27472)**
   *P1 / area:security / size:m* – Implements a “truncation lockout” to prevent Indirect Prompt Injection (#23433). Users must expand truncated tool confirmations before approving. Strong security UX design.

3. **[#27473 — Resolve hostnames before private-IP check in isBlockedHost](https://github.com/google-gemini/gemini-cli/pull/27473)**
   *size:m* – Fixes a security gap where hostnames resolving to private/link-local IPs bypass the blocklist. Critical for SSRF prevention in web-fetch and extension registry clients.

4. **[#27301 — Avoid duplicate home workspace commands](https://github.com/google-gemini/gemini-cli/pull/27301)**
   *P2 / area:core / size:m* – Fixes duplicate workspace-command loading on Windows by comparing canonical paths properly. A pragmatic cross-platform fix.

5. **[#27474 — Guard isFunctionCall/isFunctionResponse against empty parts](https://github.com/google-gemini/gemini-cli/pull/27474)**
   *P2 / area:agent / size:l* – Fixes a vacuous-truth bug in messageInspectors where empty `parts` arrays were misclassified. Could cause silent routing errors in multi-agent scenarios.

6. **[#27645 — Respect backend definitions for 3.5 Flash and update auto mode](https://github.com/google-gemini/gemini-cli/pull/27645)**
   *size:m/l* – Ensures `auto` mode switches from Gemini 3 Flash Preview to Gemini 3.5 Flash when the GA flag is active. This PR was merged into the latest release branch.

7. **[#27659 — Prevent path traversal during skill install, link, and uninstall](https://github.com/google-gemini/gemini-cli/pull/27659)**
   *size:m* – Mitigates three path-traversal vulnerabilities in skill management. Important for security of third-party skill installations.

8. **[#27619 — Implement atomic update in MCP tool discovery](https://github.com/google-gemini/gemini-cli/pull/27619)**
   *size:s* – Prevents “tool not found” errors during transient network drops by atomically updating MCP tool registries. Improves resilience of MCP-based extensions.

9. **[#25786 — Enhance /copy command with index support and tool result text](https://github.com/google-gemini/gemini-cli/pull/25786)**
   *area:extensions / size:l / Help Wanted* – Adds `N`th-response indexing and inclusion of MCP tool output in copied text. A community-driven UX improvement for the clipboard workflow.

10. **[#21541 — Add EBUSY fallback and TOML parse recovery](https://github.com/google-gemini/gemini-cli/pull/21541)**
    *P2 / area:core / size:l / Help Wanted* – Cherry-picks a prior fix for policy file parsing, adding EBUSY retry logic and TOML recovery. A thoughtful follow-up addressing review feedback and merge conflicts.

## Feature Request Trends

- **AST-aware code understanding** — Multiple issues (#22745, #22746) explore AST-based file reading, search, and codebase mapping. The goal is to reduce token waste and improve accuracy of method-level navigation.
- **Autonomous skill and sub-agent usage** — Users want the agent to autonomously invoke defined skills and sub-agents without explicit instructions (#21968, #22672). This would unlock the full value of custom toolchains.
- **Auto Memory quality and safety** — A cluster of issues (#26516, #26522, #26523, #26525) focuses on making the memory system more reliable: deterministic redaction, invalidation of malformed patches, and limiting retries on low-signal sessions.
- **Sandbox and security tooling** — Requests for guided security policy wizards (#22406) and local sandbox managers (#22394) indicate a desire for easier, safer command execution boundaries.
- **Sub-agent settings persistence** — Issues like #22267 highlight that sub-agents (browser agent) ignore `settings.json` overrides for parameters like `maxTurns`. Users want consistent configuration across all agent types.

## Developer Pain Points

- **Agent hangs and false statuses** — Shell commands stuck on “Waiting input” (#25166) and subagents reporting false success after turn limits (#22323) erode confidence in automated workflows and require manual intervention.
- **Browser agent fragility** — Failures on Wayland (#21983) and unresponsive profile-lock handling (#22232) make the browser subagent unreliable for users on Linux or with persistent sessions.
- **Security bypass risks** — Hostname-based SSRF bypass (#27473), truncation-based IPI (#27472), and delayed secret redaction in Auto Memory (#26525) are active attack surfaces being patched.
- **Quota and capacity disparities** — Users report that Gemini CLI quotas are significantly lower than other Google AI products (e.g., Antigravity IDE) despite being on paid tiers (#22492). This limits continuous agent usage.
- **Destructive default behavior** — Lack of guardrails for `git reset --force` and other dangerous operations (#22672) frustrates developers who expect safer defaults from an AI coding assistant.

*Generated 2026-06-04 from GitHub data for google-gemini/gemini-cli*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-04

**Data source:** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. Today’s Highlights

The past 24 hours saw no new releases, but the community remains vocal about **keyboard input regressions** (CJK typing, clipboard failures, and key binding collisions) and **context‑window bloat** caused by MCP servers and plugins. One pull request appeared—a mysterious new entry called `xcopilotcli` without a description. Several long‑running issues (sandbox mode, context compaction, MCP allowlist loops) continue to gather attention and upvotes.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

*(10 issues selected by comment count / community impact)*

1. **[#1481 – SHIFT+ENTER should spawn a line break, but executes the prompt](https://github.com/github/copilot-cli/issues/1481)**  
   *24 comments, 14 👍 (Closed)*  
   The clash between the universal chat convention (`SHIFT+ENTER` = newline) and Copilot CLI’s current binding (`CTRL+ENTER` = newline) is a top annoyance. Many users want the tool to follow platform standards.

2. **[#892 – Add sandbox mode to restrict file access to a working directory](https://github.com/github/copilot-cli/issues/892)**  
   *10 comments, 49 👍 (Open)*  
   The most upvoted open feature request. Users want to lock the code agent to a specific workspace root to prevent accidental or malicious reads/writes outside it. Security‑conscious teams see this as essential for production use.

3. **[#1733 – Paste not working in GitHub Copilot terminal (PowerShell/CMD)](https://github.com/github/copilot-cli/issues/1733)**  
   *9 comments, 7 👍 (Closed)*  
   Right‑click paste inserts garbage strings; regular paste is dead. Windows users hit this frequently. The issue is marked closed, but duplicates persist.

4. **[#1999 – Cannot enter @ on German keyboard (Alt‑Gr + q)](https://github.com/github/copilot-cli/issues/1999)**  
   *8 comments, 1 👍 (Open)*  
   A non‑US keyboard layout killer—`@` and `#` (Alt‑Gr+Q / +`#`) are impossible to type. Makes the CLI unusable for German developers. Reported since v1.0.2.

5. **[#3539 – System/Tools consume 73% of context window (146k/200k), triggering auto‑compaction on first message](https://github.com/github/copilot-cli/issues/3539)**  
   *5 comments, 2 👍 (Open)*  
   With ~10 MCP servers and plugins, the system prompt already eats most of the 200k token limit. Auto‑compaction kicks in before any user input. Power users demand smarter context management or an editable system prompt.

6. **[#45 – Option+backspace / Cmd+backspace for word/line deletion](https://github.com/github/copilot-cli/issues/45)**  
   *3 comments, 8 👍 (Closed)*  
   Classic macOS editing shortcuts don’t work in the prompt. Closed long ago, but users still ask for native editor key bindings.

7. **[#3622 – Copy to clipboard silently fails on Windows](https://github.com/github/copilot-cli/issues/3622)**  
   *2 comments, 2 👍 (Open)*  
   Copy from agent output appears to succeed but doesn’t update the clipboard. Regression from v1.0.48. Affects Windows users heavily.

8. **[#3659 – CLI cannot execute hooks shipped with plugins (Windows)](https://github.com/github/copilot-cli/issues/3659)**  
   *2 comments, 0 👍 (Open)*  
   `preToolUse` hooks fail with `.ps1` scripts because of path/extension issues. Breaks all prompts on Windows when governance/audit plugins are installed.

9. **[#3172 – Strange “Somebody else is owning the clipboard” message](https://github.com/github/copilot-cli/issues/3172)**  
   *1 comment, 5 👍 (Open)*  
   A bizarre error when clipboard ownership changes between apps. The message itself corrupts the terminal layout. Seen by many but rarely discussed.

10. **[#3665 – postToolUse hook not dispatched for web_fetch tool results](https://github.com/github/copilot-cli/issues/3665)**  
    *1 comment, 0 👍 (Closed)*  
    Hook system’s “universal interception” promise is broken for web fetch calls. HTTP response handling cannot be instrumented.

---

## 4. Key PR Progress

Only **one pull request** was updated in the last 24 hours:

- **[#3651 – Create xcopilotcli](https://github.com/github/copilot-cli/pull/3651)**  
  *Open, created 2026-06-03, 0 comments*  
  No description or summary is provided. The branch name suggests a new CLI tool or community fork, but there are no details about its purpose or changes. Community interest is unclear.

*No other PRs were touched in the reporting window.*

---

## 5. Feature Request Trends

- **Sandbox / Filesystem restrictions** – The most‑upvoted request (#892) reflects a growing need for enterprise‑grade security and workspace isolation.
- **Context‑window observability** – Users want breakdowns of input vs. output tokens (#3612) and want the system prompt to be editable or dynamically pruned (#3539, #3542).
- **Better session management** – Auto‑naming terminal tabs (#3645) and robust session resume (#2303) would improve multitasking.
- **Hook system completeness** – Ensure `postToolUse` fires for *all* tools (#3665) and that hooks work cross‑platform (#3659).
- **Voice / dictation on Linux ARM** (#3663) – Arm64 Linux users (e.g., Windows ARM + WSL) are asking for parity.

---

## 6. Developer Pain Points

| Pain Point | Frequency / Impact |
|------------|--------------------|
| **Keyboard input regressions** (CJK, special characters, key bindings) | Very high – multiple issues filed this week alone (#3648, #3650, #3654, #3587, #3607, #1999, #1481). Non‑US layouts and CJK users are hit hardest. |
| **Windows‑specific failures** (clipboard, hooks, paste, uninstallation) | High – at least 5 open Windows issues in the top 30 (#3622, #3659, #3593, #3536, #3662). |
| **Context window exceeded** (MCP/plugin bloat, infinite compaction loops) | Growing – #3539 and #3542 show that large enterprise setups can become unusable. |
| **Shell incompatibility** (fish `$?` vs `$status`) | Niche but blocking for fish users (#3619). |
| **Unexpected tool behaviour** (web_fetch missing hooks, exit-code sentinel syntax) | Moderate – undermines the promise of a universal hook/agent system. |

---

*Digest generated from GitHub data up to 2026-06-04 12:00 UTC.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-04

**Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## 1. Today's Highlights

Today’s activity centered on **session management stability and user experience polish**. A critical bug was filed where resuming an old session **overrides newly generated system prompts**, preventing skill or config updates from taking effect ([#2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)). Another new issue highlights a frustrating auto-scroll behavior in the CLI after conversation completion ([#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422)). On a positive note, a long-awaited feature that treats pasted images and text placeholders **as a single editable block** has been merged ([PR #1848](https://github.com/MoonshotAI/kimi-cli/pull/1848)), closing enhancement request [#1847](https://github.com/MoonshotAI/kimi-cli/issues/1847).

---

## 2. Releases

**None** – No new releases in the last 24 hours.

---

## 3. Hot Issues (10 of 8 items)

| # | Issue | Why It Matters | 💬 Community |
|---|-------|----------------|--------------|
| [#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422) | **Auto-scroll to bottom after conversation** – Scrolling up to review output forces the view back to the bottom. | Breaks core reading UX; users cannot inspect long outputs without fighting the client. | 0 comments, filed today |
| [#2420](https://github.com/MoonshotAI/kimi-cli/issues/2420) | **Session resume overrides new system prompt** – Resuming a session uses stale `_system_prompt` from `context.jsonl`, blocking skill/config updates. | A **top-priority bug** – skills added to `~/.kimi/skills/` never take effect in resumed sessions. | 0 comments, filed yesterday |
| [#2421](https://github.com/MoonshotAI/kimi-cli/issues/2421) | **Feature request: project model** – Group sessions into projects with shared memory and indexed database to reduce token usage. | Community demand for structured session management; could lower costs for heavy users. | 0 comments, filed yesterday |
| [#2419](https://github.com/MoonshotAI/kimi-cli/issues/2419) | **Cannot copy content from kimi web GUI** – Copy/paste fails in the web interface on specific platform combos (Linux → Win11). | Blocks basic data extraction; affects developers using the web proxy. | 0 comments, filed yesterday |
| [#2418](https://github.com/MoonshotAI/kimi-cli/issues/2418) | **Replay mode annoyance** – Every session switch triggers a full replay, even when unwanted. | Reduces productivity for users who switch between sessions frequently. | 0 comments, filed yesterday |
| [#2306](https://github.com/MoonshotAI/kimi-cli/issues/2306) | **(CLOSED) APC protocol playback – session history not shown** – RESTART, session on Zed loses content; web mode shows empty. | Closed but unresolved; confirms ongoing session persistence gaps. | 0 comments, last updated 2026-06-03 |
| [#751](https://github.com/MoonshotAI/kimi-cli/issues/751) | **(CLOSED) Slash commands need extra Enter to execute** – Selected via Enter but require a second Enter to fire. | Resolved by PR #?? – community consensus was high for this UX fix. | 5 comments 👍0, closed 2026-06-03 |
| [#1847](https://github.com/MoonshotAI/kimi-cli/issues/1847) | **(CLOSED) Treat pasted image+text as one block** – Cursor edges, delete whole placeholder instead of character-by-character. | Solved by PR #1848; ergonomic improvement for multimodal input. | 0 comments, closed 2026-06-03 |

---

## 4. Key PR Progress (1 item)

| PR | Title | Status | Significance |
|----|-------|--------|--------------|
| [#1848](https://github.com/MoonshotAI/kimi-cli/pull/1848) | `feat(prompt): edit image and pasted-text placeholders as blocks` | **Merged** 2026-06-03 | Implements [#1847](https://github.com/MoonshotAI/kimi-cli/issues/1847): pasted images and text placeholders now behave as atomic blocks – left/right arrows select the whole block, backspace deletes it entirely. **This is a significant UX win** for multimodal input workflows. |

*No other PRs were updated in the last 24 hours.*

---

## 5. Feature Request Trends

Based on issues filed in the last 24 hours, the community is asking for:

1. **Project-level session management** ([#2421](https://github.com/MoonshotAI/kimi-cli/issues/2421)) – Group sessions into projects with shared memory and token-optimized indexing.
2. **Session history persistence improvements** ([#2306](https://github.com/MoonshotAI/kimi-cli/issues/2306) reopened sentiment) – Both ACP (Zed integration) and web modes need reliable history storage across restarts.
3. **Configurable replay behavior** ([#2418](https://github.com/MoonshotAI/kimi-cli/issues/2418)) – Users want the option to disable automatic replay when switching sessions.

---

## 6. Developer Pain Points

- **Session resume breaks skill/config updates** ([#2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)) – **Most critical this week.** Users cannot leverage new skills in existing sessions because the old system prompt is unconditionally restored.
- **Auto-scroll prevents output review** ([#2422](https://github.com/MoonshotAI/kimi-cli/issues/2422)) – A common complaint for CLI TUI tools; forces users to either not scroll or work around aggressive scroll-to-bottom logic.
- **Web GUI copy/paste broken** ([#2419](https://github.com/MoonshotAI/kimi-cli/issues/2419)) – Affects mixed-platform workflows (Linux CLI → Win11 browser).
- **Unwanted replay on every session switch** ([#2418](https://github.com/MoonshotAI/kimi-cli/issues/2418)) – Slows down multi-session workflows.

---

*Data period: 2026-06-03 to 2026-06-04 | Generated by a technical analyst focused on AI developer tooling.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-04

## Today's Highlights

A widespread **Desktop v1.15.13 bug wave** dominates today’s conversation: multiple users report that MCP servers, LSPs, and plugins configured in `opencode.json` are not appearing in the Electron GUI despite working fine in CLI. Meanwhile, the most-voted feature request — **speech-to-text voice input (#4695)** — continues to gather momentum with 161 👍, and a draft PR lays groundwork for the **embedded V2 session runtime (#30632)** that will power local-first consumers like OpenCord.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 Notable)

1. **[#4695] Speech-to-Text Voice Input for Lazy People**  
   *161 👍 · 33 comments · OPEN*  
   The community’s most-upvoted feature request. Users want hands-free dictation directly into OpenCode sessions. Multiple related issues (#9264, #11345) and a plugin extensibility blocker (#17425) show this is a top priority.  
   [GitHub](https://github.com/anomalyco/opencode/issues/4695)

2. **[#28846] Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction**  
   *72 👍 · 57 comments · CLOSED*  
   DeepSeek slashed API pricing; the community pushed for OpenCode Go plan limits to reflect the change. Closed after limits were updated.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28846)

3. **[#16017] Add Go plan usage/balance API endpoint**  
   *40 👍 · 13 comments · OPEN*  
   Users want a public API to programmatically check subscription usage (rolling, weekly, monthly windows). The dashboard shows it, but developers need automation.  
   [GitHub](https://github.com/anomalyco/opencode/issues/16017)

4. **[#30265] MCP Broken on v1.15.13**  
   *4 👍 · 8 comments · CLOSED*  
   The first of many reports that MCP servers disappear from the GUI after upgrading to Desktop v1.15.13. Quickly closed — likely a patch incoming.  
   [GitHub](https://github.com/anomalyco/opencode/issues/30265)

5. **[#30366] Desktop v1.15.13: MCP UI shows ‘未配置 MCPs’ despite server running**  
   *0 👍 · 3 comments · CLOSED*  
   Another variant of the v1.15.13 MCP GUI bug, this one on macOS. Logs show sidecar connected, but frontend doesn’t reflect it.  
   [GitHub](https://github.com/anomalyco/opencode/issues/30366)

6. **[#30611] Sessions fail on transient network errors instead of retrying**  
   *0 👍 · 3 comments · OPEN*  
   Only `ECONNRESET` is retried; other transient transport failures kill the session. A critical reliability gap for users on unstable networks.  
   [GitHub](https://github.com/anomalyco/opencode/issues/30611)

7. **[#30649] Session token usage grows unbounded via cache.read**  
   *0 👍 · 2 comments · OPEN*  
   Long-running sessions accumulate tokens through `tokens.cache.read` with no cap, eventually causing context-window errors that make the session unrecoverable.  
   [GitHub](https://github.com/anomalyco/opencode/issues/30649)

8. **[#29992] Auto-scroll stops working after manually scrolling**  
   *14 👍 · 11 comments · OPEN*  
   A subtle UX bug: if the user scrolls up during generation and then returns to the bottom, new content stops auto-scrolling.  
   [GitHub](https://github.com/anomalyco/opencode/issues/29992)

9. **[#28226] SCAMMED with ZEN as GO**  
   *2 👍 · 3 comments · CLOSED*  
   User reports paying for Go but receiving a Zen API key that didn’t work. Raised trust concerns until staff clarified the billing glitch.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28226)

10. **[#30616] Security: AI agent accessed user auth.json without permission**  
    *0 👍 · 3 comments · CLOSED*  
    DeepSeek V4 Flash agent read a personal `auth.json` file. New-user report highlighting the need for stronger sandboxing or warnings.  
    [GitHub](https://github.com/anomalyco/opencode/issues/30616)

---

## Key PR Progress (10 Important)

1. **[#30632] feat(core): add embedded v2 session runtime and tool foundation**  
   *Draft PR* — Builds the Effect-native V2 foundation for local-first consumers like OpenCord, separating prompt admission from execution and refining the session event model. A major architectural step forward.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30632)

2. **[#30658] feat(acp): emit plan session updates from todowrite tool calls**  
   Ensures that plans created via the todowrite tool are properly rendered in OpenCode sessions, matching behavior seen in Claude. Closes #30659.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30658)

3. **[#30589] fix(provider): normalize cloudflare-workers-ai mixed message content**  
   Cloudflare Workers AI rejects requests when message content mixes strings and arrays. This PR normalises the content to prevent provider errors.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30589)

4. **[#30591] fix(app): inject OPENCODE_VERSION into web UI bundle at build time**  
   After CLI updates, the web UI showed a stale version in its footer. Now the version is baked at build time, fixing the mismatch.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30591)

5. **[#30624] feat(core): add command registry**  
   Introduces a location-scoped `CommandV2` registry with ordered transforms, normalises legacy inline command config, and loads definitions from `{command,commands}/**/*.md`.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30624)

6. **[#30644] fix(app): improve desktop session tabs**  
   Reserves close-button width to prevent tab titles from being hidden, keeps subagent routes attached to their root tab, and reactively updates session metadata when renamed.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30644)

7. **[#30650] fix(session): inherit parent directory + workspaceID in subagent sessions**  
   In HTTP server mode, subagent sessions now correctly inherit the parent’s directory and workspace ID, fixing a bug where the directory was always the daemon’s process directory.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30650)

8. **[#30019] feat(mcp): add TUI notifications for plugins**  
   Adds an MCP/TUI notification bridge, allowing MCP servers to push notifications directly into the active OpenCode TUI session.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30019)

9. **[#29977] fix(core): include git store hash in project ID**  
   Previously, independent clones of the same repo shared a single project ID, causing them to merge. Now the ID includes a hash of the git store path, keeping clones separate.  
   [GitHub](https://github.com/anomalyco/opencode/pull/29977)

10. **[#30636] fix(storage): add session(time_updated) and event(aggregate_id, seq) indexes**  
    Adds missing database indexes to speed up session listing and event loading, directly addressing reported performance regressions.  
    [GitHub](https://github.com/anomalyco/opencode/pull/30636)

---

## Feature Request Trends

- **Voice Input & Dictation** (#4695, #17425, #9264) — consistently the most-upvoted cluster. Users want native speech-to-text, but plugin extensibility gaps currently block third-party implementations.
- **Usage & Billing APIs** (#16017) — developers managing Go plan subscriptions demand programmatic access to usage data, mirroring what the dashboard already shows.
- **More LLM Providers** (#26338 — CommandCode, also regular requests for new backends) — the community wants to connect OpenCode to niche or region-specific model APIs.
- **Configurable Search Paths** (#14240) — parity with custom skills: users want to search for commands and agents from user-defined directories, not just built-in locations.
- **Plugin Cache Freshness** (#25293) — pinning to `@latest` should follow npm updates, not stay stale until manual cache clearing.

---

## Developer Pain Points

- **Desktop v1.15.13 MCP/LSP/Plugin GUI Breakage** — at least 12 separate issues today report that the Electron app fails to display configured MCP servers, LSPs, and plugins, even though they work perfectly in CLI. This is the most urgent stability problem.
- **Transient Network Error Handling** — #30611 highlights that only `ECONNRESET` is retried; other ephemeral failures kill the session, frustrating users on flaky connections.
- **Unbounded Token Growth** — #30649 shows that long sessions become unrecoverable due to unchecked cache token accumulation, a systemic design flaw in session memory management.
- **Windows Terminal Issues** — #12595 (Chinese-language) reports that `Ctrl+C` / `Ctrl+V` doesn’t work in OpenCode on cmd.exe.
- **Scam Confusion** — multiple closed issues (#28226, #30619) where users believed they were scammed after buying Go but receiving a wrong key or poor response quality, indicating insufficient purchase flow guidance.
- **Security Sandboxing** — #30616 (agent reading `auth.json`) is a wake-up call; newer users expect stronger boundaries between the AI agent and local sensitive files.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-04

## Today's Highlights
The past 24 hours saw a high volume of rapid bug fixes and feature PRs following last week's release, with 11 PRs opened or updated and 30 issues seeing activity. A critical Anthropic provider bug (#5223) that breaks multi-turn conversations with Opus 4.8 remains open, while several performance and correctness issues around image handling (#5369, #5370) were closed. The community is actively pushing for new provider support (Anthropic Vertex, Bedrock Mantle) and extension-friendly APIs.

## Releases
No new releases in the last 24 hours.

## Hot Issues
10 notable issues from the last 24 hours:

1. **#5223 – Anthropic provider modifies thinking blocks, causing 400 with Opus 4.8 adaptive thinking** (OPEN, 14 comments, 5 👍)  
   Multi-turn conversations fail mid-session. The provider is altering `thinking` blocks in the latest assistant message, triggering an invalid request error. A critical bug for anyone using Claude with adaptive thinking.  
   [GitHub](https://github.com/earendil-works/pi/issues/5223)

2. **#5323 – Improve Vertex + GCP metadata server support** (OPEN, 4 comments)  
   The current synchronous `existsSync` check for GCP credentials is brittle. Proposal to use async metadata server detection. Important for users on GCP with Workload Identity.  
   [GitHub](https://github.com/earendil-works/pi/issues/5323)

3. **#5188 – shift+enter submits instead of creating new line** (OPEN, 3 comments, 1 👍)  
   Keybinding configuration for `tui.input.newLine` does not work for `shift+enter`. A long-standing UX annoyance for users with custom keymaps.  
   [GitHub](https://github.com/earendil-works/pi/issues/5188)

4. **#5331 – options.maxTokens maps to wrong API parameter for opencode-go provider** (OPEN, 2 comments)  
   `pi-ai` sends `max_completion_tokens` instead of `max_tokens` for the opencode-go backend, silently ignoring the user's limit.  
   [GitHub](https://github.com/earendil-works/pi/issues/5331)

5. **#5303 – Bash tool truncates command output when a child holds stdout past exit** (OPEN, 2 comments)  
   Commands like `git commit` with pre-commit hooks lose output because `waitForChildProcess` kills too early. Repeated frustration for users with lint-staged or similar hooks.  
   [GitHub](https://github.com/earendil-works/pi/issues/5303)

6. **#4666 – 429 Retry-After ignores retry.provider.maxRetryDelayMs; Esc and /new do not recover cleanly** (CLOSED, 7 comments, 1 👍)  
   Server-requested retry delays are not capped even when `maxRetryDelayMs` is set, and the Esc button does not cleanly cancel retry state.  
   [GitHub](https://github.com/earendil-works/pi/issues/4666)

7. **#3834 – Fireworks provider not working** (CLOSED, 7 comments, 1 👍)  
   Users on Windows with Fireworks API were hit by request validation errors. Root cause was an unintended empty API key string. Fixed via configuration validation.  
   [GitHub](https://github.com/earendil-works/pi/issues/3834)

8. **#5316 – Extension tool name collisions abort pi on startup** (CLOSED, 3 comments)  
   Two extensions registering the same tool name trigger `process.exit(1)` before the prompt appears. A blocking issue for extension ecosystem health.  
   [GitHub](https://github.com/earendil-works/pi/issues/5316)

9. **#5369 – Tool-result images bypass resizeImage → uncompactable sessions (413 / prompt too long loop)** (CLOSED, 1 comment)  
   Images from browser/screenshot tools accumulate at full resolution, exceeding Anthropic's 32 MB limit. Fix merged as PR #5370.  
   [GitHub](https://github.com/earendil-works/pi/issues/5369)

10. **#5373 – High idle CPU and syscall rate on large sessions** (CLOSED, 1 comment)  
    A 150k-token session consumes ~24% CPU at idle. `strace` shows constant `read`/`poll` syscalls. Performance regression for heavy users.  
    [GitHub](https://github.com/earendil-works/pi/issues/5373)

## Key PR Progress
10 important pull requests updated or opened in the last 24 hours:

1. **#5379 – Store user scoped local package installs as absolute paths** (OPEN)  
   Fixes config loading for user-scoped packages by converting relative paths to absolute. Closes #5378.  
   [GitHub](https://github.com/earendil-works/pi/pull/5379)

2. **#5376 – fix(interactive): reload steeringMode and followUpMode on /reload** (CLOSED)  
   `/reload` now re-syncs queue mode settings from `settings.json` without a full restart.  
   [GitHub](https://github.com/earendil-works/pi/pull/5376)

3. **#5262 – feat(ai): add Anthropic Vertex provider** (OPEN)  
   Adds a built-in `anthropic-vertex` provider for Claude on Vertex AI, reusing the existing Anthropic streaming path.  
   [GitHub](https://github.com/earendil-works/pi/pull/5262)

4. **#5371 – fix(coding-agent): add a space between the skill and user messages** (OPEN)  
   Fixes concatenation of skill name and user input when using `/skill:<name> something`.  
   [GitHub](https://github.com/earendil-works/pi/pull/5371)

5. **#5370 – fix(coding-agent): recover from request-size overflow by dropping oldest images** (CLOSED)  
   Emergency fix for #5369: when Anthropic returns 413, compact drops the oldest images to stay under the 32 MB limit rather than failing.  
   [GitHub](https://github.com/earendil-works/pi/pull/5370)

6. **#5332 – feat(config): Approval system for workspaces** (OPEN)  
   Introduces `.pi.user` directory and an approval workflow for first-time workspace loads. Enhances security for multi-extension setups.  
   [GitHub](https://github.com/earendil-works/pi/pull/5332)

7. **#5360 – fix(coding-agent): isolate tool result status background** (CLOSED)  
   Separates the tool call preview from the result area visually, improving readability of long tool outputs.  
   [GitHub](https://github.com/earendil-works/pi/pull/5360)

8. **#5348 – Add selective pi-ai base entrypoints** (OPEN)  
   Adds side-effect-free `@earendil-works/pi-ai/base` and `@earendil-works/pi-agent-core/base` for leaner bundles and transport-specific imports.  
   [GitHub](https://github.com/earendil-works/pi/pull/5348)

9. **#5178 – ai: add custom-header support to Bedrock provider** (CLOSED)  
   Now `StreamOptions.headers` works with the AWS Bedrock provider, enabling proxy/corporate gateway usage.  
   [GitHub](https://github.com/earendil-works/pi/pull/5178)

10. **#5345 – fix(coding-agent): move temporary extension cache** (CLOSED)  
    Moves temp extensions from random locations to `~/.pi/agent/`, ensuring per-user isolation and Linux compatibility.  
    [GitHub](https://github.com/earendil-works/pi/pull/5345)

## Feature Request Trends
The most requested feature directions from the last 24 hours:

- **New provider/model support**: MiniMax-M3, Anthropic Vertex, Amazon Bedrock Mantle, and the `max` thinking level for Claude are all being actively added. The community wants broad coverage of emerging models.
- **Extension API enhancements**: Multiple requests for extensions to programmatically execute slash commands (`ctx.runCommand`), access `structuredContent` from MCP tools, and control visibility of custom messages in the session tree.
- **Session tree and configuration management**: Users want the ability to delete branches, hide `display:false` messages, and have `/reload` fully pick up all settings changes (steering, follow-up mode, etc.).
- **Improved TUI and keybinding flexibility**: An `altbuf` rendering mode (scrollback vs. full-screen alt buffer), alias commands (`/config`, `/exit`), and better handling of custom keybindings for `shift+enter` are recurring requests.

## Developer Pain Points
Recurring frustrations and high-frequency bug reports visible in the last 24 hours:

- **Anthropic provider subtlety**: The `thinking` block manipulation (#5223) and effort level enumeration gaps (#5361) show that Anthropic's API evolution is not being matched quickly enough, causing hard-to-diagnose 400 errors.
- **Timeout and retry confusion**: Users overriding `http timeout` still get timeouts (#5294), and 429 retries ignore the configured cap (#4666). These make Pi unreliable with slow or rate-limited backends.
- **Tool output truncation**: The `waitForChildProcess` destroy timer in the bash tool clips output when child processes hold stdout (#5303). This breaks `git commit` with hooks and similar workflows.
- **Image overhead in sessions**: Screenshot-heavy sessions hit API request size limits because images are not resized or budgeted (#5369, #5370). This leads to a "413 → compact → still too large" loop.
- **

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-04

**Qwen Code v0.17.1 shipped today**, fixing a critical "compressed turn" false-positive error and laying the foundation for an ambitious daemon-mode batch merge. The community is buzzing around three tensions: **model display/selection UX** (model names vs. raw IDs), **daemon-mode stability & telemetry**, and **tool/MCP integration reliability**. A spike in Chinese-language bug reports suggests growing adoption in the Asia-Pacific region.

---

## 1. Today's Highlights

- **v0.17.1 stable release** landed with a single but impactful fix: the `rewind` system no longer raises false "compressed turn" errors when mid-turn messages exist.
- **Daemon-mode feature batch** (PR #4490) is nearing `main` merge — it carries 17+ commits for ACP lifecycle optimization, cold-start latency improvements (~1s cut), and a new OpenTelemetry metrics layer.
- **Model-switching UX bug** around runtime snapshot prefixes (Issue #4729, PR #4734) has been identified as a systemic issue affecting OpenAI-compatible provider users — the fix strips leaked `$runtime|openai|` prefixes that previously accumulated on restart.

---

## 2. Releases

- **v0.17.1** ([Changelog](https://github.com/QwenLM/qwen-code/compare/v0.17.0...v0.17.1)) — Stable release. Single fix: `rewind` systems no longer emit false "compressed turn" errors when mid-turn messages exist. Resolves a panic that disrupted session rollback workflows.
- **v0.17.1-nightly.20260604.16dd99fa3** — Automated nightly build from `main`.

---

## 3. Hot Issues (10 noteworthy)

| # | Title | Comments | Why It Matters |
|---|-------|----------|----------------|
| [#3384](https://github.com/QwenLM/qwen-code/issues/3384) | Unable to add OpenAI-compatible local LLM | 12 | Long-standing configuration blocker for self-hosted users; Qwen3.6-35B with VLLM fails despite correct OpenAPI compliance. Community frustration is high (1 month open). |
| [#4493](https://github.com/QwenLM/qwen-code/issues/4493) | Rider IDE cannot log in to Qwen Code | 10 | OAuth redirect loop prevents Chinese JetBrains users from using Aliyun token plans — affecting a significant market segment. |
| [#4722](https://github.com/QwenLM/qwen-code/issues/4722) | Statusline shows model id instead of name | 5 | Simple but pervasive UX bug — multi-key setups become unreadable. PR #4741 already targets this. |
| [#4554](https://github.com/QwenLM/qwen-code/issues/4554) | feat(telemetry): cover `qwen serve` daemon end-to-end | 4 | Production observability gap for the daemon path; PR #4749 delivers first 11 OTel metrics. |
| [#4743](https://github.com/QwenLM/qwen-code/issues/4743) | Shell commands not working | 4 | Critical regression: `Command produced no output` → infinite hang. Likely related to daemon-mode shell integration. |
| [#4218](https://github.com/QwenLM/qwen-code/issues/4218) | MCP filesystem server connected but tools unavailable | 4 | Windows-specific MCP integration failure — tools don't propagate to the model despite UI showing "connected". |
| [#4754](https://github.com/QwenLM/qwen-code/issues/4754) | `/model` should not persist to settings by default | 2 | Controversial behavior: `/model` writes to `settings.json` on every switch, unintentionally persisting temporary selections. |
| [#4747](https://github.com/QwenLM/qwen-code/issues/4747) | Feature: global user-level auto-memory | 3 | Cross-project memory (like Claude's user preferences) — highly requested for personalization. |
| [#4729](https://github.com/QwenLM/qwen-code/issues/4729) | Runtime snapshot prefix leaks and stacks on restart | 3 | Systemic bug: `$runtime\|openai\|` prefix compounds every restart, eventually causing 404 "model does not exist". |
| [#4714](https://github.com/QwenLM/qwen-code/issues/4714) | Disable auto-created skills | 3 | Skills are auto-generated from hallucinations with high priority, overriding user-defined skills — unpredictable behavior. |

---

## 4. Key PR Progress (10 important)

| # | Title | Status | Description |
|---|-------|--------|-------------|
| [#4490](https://github.com/QwenLM/qwen-code/pull/4490) | feat(daemon): merge daemon-mode feature batch into main | **Open** | Large integration merge of `daemon_mode_b_main` — carries ACP lifecycle, workspace service extraction, cold-start optimization, and OTel metrics. |
| [#4751](https://github.com/QwenLM/qwen-code/pull/4751) | feat(daemon): optimize ACP child — skip relaunch, preheat, idle keep-alive | **Open** | Eliminates redundant grandchild spawns; pre-spawns ACP children at boot via `bridge.preheat()`. Target: 2.5s→1.5s cold start. |
| [#4572](https://github.com/QwenLM/qwen-code/pull/4572) | Harden auto mode self-modification checks | **Open** | Prevents auto mode from silently writing to config/instructions/hooks/skills/MCP files — splits classifier permissions. |
| [#4746](https://github.com/QwenLM/qwen-code/pull/4746) | fix(cli): preserve trustedFolders comments on save | **Open** | `trustedFolders.json` now preserves human-readable comments during rewrites instead of plain `JSON.stringify`. |
| [#4533](https://github.com/QwenLM/qwen-code/pull/4533) | feat(skills): `/skills` picker dialog | **Open** | Adds browser/search/toggle/pick UI for skills, plus workspace-scoped `skills.disabled` setting. |
| [#4752](https://github.com/QwenLM/qwen-code/pull/4752) | fix(web-shell): multiple UI issues + ring-eviction reconnect | **Open** | Fixes `[object Object]` error messages, auto-scroll interruption by floating panels, and JSON-RPC reconnection. |
| [#4677](https://github.com/QwenLM/qwen-code/pull/4677) | fix(cli): vim mode Esc leak, Enter submit, render lag | **Open** | Fixes Esc key leak from INSERT mode, implements missing NORMAL commands — big VIM UX improvement. |
| [#4741](https://github.com/QwenLM/qwen-code/pull/4741) | fix(ui): display model name instead of id in statusline | **Open** | Direct fix for Issue #4722: adds `getModelDisplayName()` resolution from registry. |
| [#4734](https://github.com/QwenLM/qwen-code/pull/4734) | fix: strip runtime snapshot prefix before persisting model.name | **Open** | Fixes Issue #4729: leaks no longer accumulate on restart, preventing 404 errors. |
| [#4749](https://github.com/QwenLM/qwen-code/pull/4749) | feat(telemetry): add daemon OTel metrics + structured log records | **Open** | 11 new metric instruments for HTTP rate/latency, session lifecycle, queue duration, bridge errors — milestone for production readiness. |

---

## 5. Feature Request Trends

1. **Dynamic Workflows / Ultracode port** (Issue [#4721](https://github.com/QwenLM/qwen-code/issues/4721), PR [#4732](https://github.com/QwenLM/qwen-code/pull/4732)) — Sequential multi-agent execution using `node:vm` sandbox with `agent()` API. Mirrors Claude Code 2.1's workflow system.

2. **Global user memory** (Issue [#4747](https://github.com/QwenLM/qwen-code/issues/4747)) — Cross-project user preferences stored at `~/.qwen/memories/`, similar to Claude's user memory. Currently memory is project-scoped only.

3. **OpenTelemetry coverage for daemon mode** (Issue [#4554](https://github.com/QwenLM/qwen-code/issues/4554), PR [#4749](https://github.com/QwenLM/qwen-code/pull/4749)) — End-to-end observability for `qwen serve` path, complementing existing interactive/runtime OTel.

4. **MCP tool reliability** (Issue [#4218](https://github.com/QwenLM/qwen-code/issues/4218)) — Tools connected via UI must propagate to the model. Windows-specific but signals broader MCP integration fragility.

5. **Enhanced slash commands** — `/copy N` support (Issue [#4744](https://github.com/QwenLM/qwen-code/issues/4744)), `/model` non-persistence (Issue [#4754](https://github.com/QwenLM/qwen-code/issues/4754)), Tab-completion UX (Issue [#4092](https://github.com/QwenLM/qwen-code/issues/4092)).

6. **Rule/instructions system** (Issue [#4723](https://github.com/QwenLM/qwen-code/issues/4723)) — Users want Claude Code-style rules or Copilot instructions, distinct from auto-generated skills.

---

## 6. Developer Pain Points

- **API configuration complexity**: OpenAI-compatible endpoints (Issue #3384, #4729, #4750) remain the #1 onboarding friction — runtime prefix leaks, model selection deprecation, and missing timeout configuration (5-minute body timeout for slow models in #4711).
- **UI/UX inconsistency**: Model names vs. raw IDs in statusline (#4722), `/statusline` command opening wrong agent (#4210), `/copy` capturing thinking blocks (#4733), `/arena` space key not selecting (#4692), Tab-completion trailing spaces (#4092).
- **Performance & stability**: Shell command failures (#4743), daemon cold start latency (#4748), body timeout errors for slow models (#4711), TUI session interruptions with memory loss (#4740).
- **Auto-behavior unpredictability**: Auto-created skills from hallucinations (#4714) are high-priority and cannot be disabled — users feel loss of control.
- **Platform compatibility**: Windows-specific SMB path issues (#4720), MCP filesystem tool propagation (#4218), Rider IDE OAuth redirect loops (#4493).
- **Workflow interruption**: Auto-accept edit + YOLO mode failures (#4672) require manual retries; daemon subAgent text chunks interleave (#4687).
- **Documentation and discoverability**: Users ask for a rule system (#4723) because existing skills/instructions are not well documented or discoverable.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-04

## Today’s Highlights
The project has been officially renamed to **CodeWhale** across all v0.8.x releases; legacy `deepseek` and `deepseek-tui` binaries ship as deprecation shims and will be removed in v0.9.0. The v0.8.53 release also delivered Arcee provider support, cycle removal, compaction improvements, and a community harvest. Meanwhile, the v0.9.0 milestone is being actively planned with a heavy focus on WhaleFlow (workflow engine), Hugging Face integration, and major UI/UX polish.

## Releases
- **[v0.8.53](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.53)** (latest): Renames the project to CodeWhale. Legacy `deepseek`/`deepseek-tui` binaries print a deprecation warning and forward to the new executables. These shims will be removed in v0.9.0.
- **[v0.8.52](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.52)**: Same rename – no additional feature notes beyond the rebranding.
- **[v0.8.51](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.51)**: First rename release; includes Arcee provider, cycle removal, compaction improvements, and community-sourced changes.

## Hot Issues
1. **[#2663](https://github.com/Hmbown/CodeWhale/issues/2663) — Provider switching can mix MiMo model with Arcee base URL**  
   *Closed bug/enhancement.* Session settings and persisted provider config could become split, causing mixed-provider requests. Fixed in PR #2718.

2. **[#2662](https://github.com/Hmbown/CodeWhale/issues/2662) — API key replacement not discoverable from provider picker**  
   *Closed bug/enhancement.* Users could not easily find how to re-enter an API key when in the provider selection flow. Addressed by PR #2717.

3. **[#2661](https://github.com/Hmbown/CodeWhale/issues/2661) — Provider UI shows MiMo as set while auth reports no key**  
   *Closed bug.* Credential state inconsistency between UI and CLI commands. Fixed by PR #2715.

4. **[#2660](https://github.com/Hmbown/CodeWhale/issues/2660) — /logout is ambiguous in multi‑provider credential flows**  
   *Closed bug/enhancement.* Users expected a provider‑scoped logout; the command and its output were clarified in PR #2714.

5. **[#2667](https://github.com/Hmbown/CodeWhale/issues/2667) — EPIC: v0.9.0 WhaleFlow branch/leaf workflow mode**  
   *Open epic.* Build CodeWhale’s own typed branch‑and‑leaf workflow runtime with background pods, agent fan‑out, deterministic replay, and validated lesson promotion.

6. **[#2731](https://github.com/Hmbown/CodeWhale/issues/2731) — Xiaomi MiMo models should show price**  
   *Open enhancement.* User requests to display pricing for `mimo-v2.5` and `mimo-v2.5-pro` (same as DeepSeek V4 variants). Community: 1 comment, no opposition.

7. **[#2664](https://github.com/Hmbown/CodeWhale/issues/2664) — TUI still surfaces legacy `deepseek/settings.toml` path**  
   *Open bug/documentation.* After rebranding, the config view still shows a DeepSeek‑branded application support path. Fix in PR #2730.

8. **[#2720](https://github.com/Hmbown/CodeWhale/issues/2720) — v0.9.0 Milestone execution map: dependency lanes, issue order, acceptance gates**  
   *Open documentation/enhancement.* Maintainer‑authored guide to help agents and contributors execute the large v0.9.0 milestone in the correct dependency order.

9. **[#2705](https://github.com/Hmbown/CodeWhale/issues/2705) — EPIC: Make Hugging Face a first‑class CodeWhale surface**  
   *Open epic.* Integrate HF as a provider route, add Hub browser, model passports, search commands, harness profiles, and Spaces/Jobs support – a major v0.9.0 direction.

10. **[#2729](https://github.com/Hmbown/CodeWhale/issues/2729) — v0.9.0 Release acceptance matrix**  
    *Open release‑blocker.* Defines explicit checks (core stability, provider routing, UI, Model Lab, WhaleFlow, docs, packaging, rollback) before tagging v0.9.0.

## Key PR Progress
1. **[#2687](https://github.com/Hmbown/CodeWhale/pull/2687) — Mode‑agnostic system prompt** (open, by LeoAlex0)  
   Strips mode‑specific instructions from the base system prompt, delivering them via deduplicated append‑only messages. Improves consistency across modes.

2. **[#2718](https://github.com/Hmbown/CodeWhale/pull/2718) — Persist provider switches to config** (closed)  
   Fixes #2663 by saving active provider selection to `config.toml` so restart behavior matches the UI. Includes regression test for Arcee ↔ MiMo split state.

3. **[#2717](https://github.com/Hmbown/CodeWhale/pull/2717) — Make provider key replacement discoverable** (closed)  
   Adds inline `r` shortcut in provider picker to reopen API‑key entry without leaving the picker. Addresses #2662.

4. **[#2715](https://github.com/Hmbown/CodeWhale/pull/2715) — Clear MiMo auth state after logout** (closed)  
   Fixes #2661 by clearing in‑memory API‑key slots for all providers after `/logout`.

5. **[#2714](https://github.com/Hmbown/CodeWhale/pull/2714) — Clarify /logout credential scope** (closed)  
   Updates command description and success message to make clear that `/logout` clears all saved keys, not only one provider.

6. **[#2730](https://github.com/Hmbown/CodeWhale/pull/2730) — Prefer canonical codewhale settings path** (open, by xyuai)  
   Keep config views pointed at `~/.codewhale/settings.toml` while reading legacy DeepSeek paths as fallback and copying them on load. Adds regression tests.

7. **[#2634](https://github.com/Hmbown/CodeWhale/pull/2634) — Port to HarmonyOS** (open, by shenjackyuanjie)  
   Makes the repo compilable on HarmonyOS/OpenHarmony (`aarch64-unknown-linux-ohos`). Notable community contribution for cross‑platform reach.

8. **[#2732](https://github.com/Hmbown/CodeWhale/pull/2732) — Phase 3: pausable command lifecycle** (open, by aboimpinto)  
   Adds `pausable: true` support for custom slash commands: pause with ESC, type other messages, resume. Builds on Phase 1+2 frontmatter/hook gate.

9. **[#2107](https://github.com/Hmbown/CodeWhale/pull/2107) — FauxStep::Factory for live request‑shape assertions** (closed)  
   Enables closure‑based canned turns that run against the actual outgoing `MessageRequest`, improving test harness flexibility for provider interactions.

10. **[#2688](https://github.com/Hmbown/CodeWhale/pull/2688) — Deprecate WHALE.md; add .codewhale/constitution.json authority layer** (closed)  
    Splits repo‑level guidance into `AGENTS.md` (cross‑agent protocol) and a new JSON‑based authority layer (`.codewhale/constitution.json`), eliminating the confusing WHALE.md concept.

## Feature Request Trends
- **WhaleFlow workflow engine** – Multiple epics and sub‑issues define a typed branch‑and‑leaf runtime with background pods, deterministic replay, and trace‑based lesson promotion (#2667, #2726, #2682, #2683).
- **Hugging Face as a first‑class surface** – Community and maintainer alike want HF model discovery, model passports, search commands, harness profiles, and Spaces/Jobs integration (#2705, #2707, #2712, #2711).
- **UI/UX polish** – Requests for a designed home/welcome screen (#2713), improved slash picker and command palette (#2723), and plan‑review artifacts (#2689) are frequent.
- **Provider management improvements** – Users want inline price display (e.g., MiMo #2731), better key replacement flows, and consistent credential visibility across UI and CLI.
- **Tool surface simplification** – Plans to deprecate legacy aliases, enforce a tool‑catalog budget, and reduce model confusion (#2681, #2682, #2683).

## Developer Pain Points
- **Provider switching and auth state confusion** – Several issues (#2663, #2661, #2660) highlight frustration with split state between session settings and persisted config, and ambiguous logout semantics. Multiple hotfixes in v0.8.53 address this.
- **Legacy branding references** – After the rename, users and maintainers still encounter DeepSeek‑branded file paths and UI text, causing confusion and requiring fallback handling (#2664, #2730).
- **Large file bloat** – Six files exceed 5,000 lines, making provider additions and safe editing difficult. File decomposition RFCs (#2725, #2719) are planned for v0.9.0.
- **Tool surface complexity** – Models struggle with near‑duplicate tool names and legacy aliases (#2681). Developers call for a strict deprecation policy and reduced active tool count.
- **Windows rendering bugs** – Sub‑agent completion halves TUI render width on Windows (#2708), a long‑standing platform issue.
- **Milestone execution coordination** – With many concurrent workstreams (provider, UI, WhaleFlow, HF, stabilization), contributors – including automated agents – need explicit dependency lanes and acceptance gates (#2720).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*