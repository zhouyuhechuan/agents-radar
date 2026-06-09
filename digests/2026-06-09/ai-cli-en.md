# AI CLI Tools Community Digest 2026-06-09

> Generated: 2026-06-09 02:30 UTC | Tools covered: 9

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

# AI CLI Developer Tools Cross-Tool Comparison Report
**Date:** 2026-06-09

## 1. Ecosystem Overview

The AI CLI developer tools landscape in June 2026 shows a market maturing from experimental prototypes to production-grade infrastructure, but stability gaps remain significant across the board. Seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (now CodeWhale)—are competing fiercely, with each tool exhibiting distinct strengths and pain points. A clear trend is the convergence toward shared capabilities (MCP support, multi-agent workflows, session management) while tools differentiate on model ecosystem integration, customization depth, and platform reliability. The market is also witnessing a **branding and restructuring wave**—Kimi Code is migrating from Python to TypeScript, and DeepSeek TUI has fully rebranded to CodeWhale—signaling that identity and clarity matter as the user base expands beyond early adopters.

## 2. Activity Comparison (Last 24 Hours)

| Tool | Issues Updated | PRs Updated | Release Status |
|---|---|---|---|
| **Claude Code** | ~10 notable issues, high activity | 5 PRs (3 open, 2 closed) | **Released** v2.1.169 |
| **OpenAI Codex** | ~10 notable issues, high activity | 10 PRs (9 open, 1 merged) | **No stable release** (2 alpha pre-releases) |
| **Gemini CLI** | ~10 notable issues, high activity | 10 PRs (6 open, 4 closed) | **Nightly** v0.47.0-nightly |
| **GitHub Copilot CLI** | 30 issues updated; 10 notable | 1 PR (closed) | **No release** |
| **Kimi Code CLI** | 4 notable issues | 0 PRs | **No release** |
| **OpenCode** | ~10 notable issues, high activity | 10 PRs (9 open, 1 merged incl. experimental) | **No release** |
| **Pi** | ~10 notable issues, high activity | 10 PRs (9 open, 1 merged) | **Released** v0.79.0 |
| **Qwen Code** | ~10 notable issues, high activity | 10 PRs (7 open, 1 merged) | **Release failed** (v0.18.0-preview CI failure) |
| **DeepSeek TUI (CodeWhale)** | ~10 notable issues, growing | 10 PRs (9 open, 1 merged) | **Released** v0.8.54 (branding launch) |

**Key observations:**
- **Claude Code, OpenCode, Qwen Code, and Pi** are the most actively developed today—each with strong PR backlogs and releases.
- **GitHub Copilot CLI** has the most total issues (30) but only 1 PR, indicating a **support-maintenance phase** rather than rapid iteration.
- **Kimi Code CLI** is critically quiet (0 PRs, 4 issues), suggesting either a team focus on internal rewrite or community disengagement.
- **Gemini CLI and Pi** both released new versions today, showing ongoing commitment to regular delivery.

## 3. Shared Feature Directions

The following requirements appear across **multiple tool communities**:

| Feature / Need | Tools Expressing Demand | Specific Requests |
|---|---|---|
| **Multi-session / tab management** | Claude Code (#30154), OpenAI Codex (#22321, #12029), GitHub Copilot CLI (#2966), DeepSeek TUI (#2753) | Enable simultaneous sessions, cross-tab collaboration, and personal/corporate account switching |
| **Model flexibility & BYOK** | GitHub Copilot CLI (#3709, #3707), OpenCode (#30332), Pi (#5363), Kimi Code CLI (#2442) | Support for lower-cost, open-weight, and local models; ability to switch mid-session |
| **File rollback/checkpoints** | OpenCode (#5474), Pi (#5521), Qwen Code (#4871) | `/undo` should revert file changes, not just conversation; session rewind with file restoration |
| **AST-aware / precise code understanding** | Gemini CLI (#22745, #22746), Pi (indirect via tool optimization) | Use AST-based reads for reduced token waste and improved navigation precision |
| **MCP & tool integration improvements** | Claude Code (#61044, #64521), GitHub Copilot CLI (#3436, #3701), OpenCode (#15535), Gemini CLI (#27619, #27438) | SSRF protection, atomic tool discovery, per-tool-call timeout, and resource/read support |
| **AI Safety & defensive programming** | Claude Code (#66408, #66397), Gemini CLI (#27397), Qwen Code (#4815, #4838) | Prevent confabulation, destructive file I/O, and out-of-memory crashes; enforce tool-result microcompaction |
| **User-level / cross-project memory** | Claude Code (#66352), Qwen Code (#4747, now merged) | Store user preferences and skills across all projects, not per-folder |
| **Windows & WSL stability** | Claude Code (#5674, #27897), OpenAI Codex (#25715, #26149), GitHub Copilot CLI (#3652), OpenCode (#31329) | Resolve ECONNRESET, scan overhead, and startup latency on Windows/WSL |
| **i18n / multilingual support** | DeepSeek TUI (#2919, #2918, #2901) | Localize configuration, tool labels, and UI for non-English users |
| **Declarative agent configuration** | Qwen Code (#4821, #4842), DeepSeek TUI (#2482, WhaleFlow) | Define agents via YAML frontmatter or JSON; enable multi-agent DAG workflows |

**Emerging convergence:** MCP protocol support is now expected, not a differentiator. The new battleground is **session lifecycle management**, **agent safety**, and **declarative workflow orchestration**.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI (CodeWhale) |
|---|---|---|---|---|---|---|---|---|
| **Primary Focus** | Plugin ecosystem, desktop interop | Desktop agent with local image gen | Agent safety, evaluation infrastructure | GitHub integration, MCP extensibility | Headless/CI agent with OpenRouter | Lightweight, local-first TUI | Multi-agent teams, declarative config | Multi-vendor, i18n, fast iteration |
| **Target User** | Power users, plugin developers | Enterprise teams, macOS users | Research-oriented, safety-conscious | GitHub user base, modal-editor fans | CI/CD engineers, OpenRouter users | Local-model advocates, Linux | Team leads, declarative config fans | Broad community, multilingual |
| **Technical Approach** | Python/TypeScript hybrid; CLI + Desktop | Rust-based CLI + Desktop app | Go-based CLI with nightly regime | Go-based CLI; GitHub ecosystem | TypeScript CLI + Desktop (sidecar PoC) | Go-based TUI; high release cadence | TypeScript CLI; daemon bridge + ACP transport | Rust-based TUI; cargo distribution |
| **Model Ecosystem** | Anthropic Claude (primary) | OpenAI models (GPT-5.5, etc.) | Google Gemini models | Multi-model (Claude, GPT, etc.) | Multi-provider (OpenAI, Anthropic, OpenRouter) | Multi-provider (OpenAI, Azure, Ollama, Bedrock) | Qwen (primary) + external | DeepSeek, Together AI, OpenAI Codex (experimental) |
| **Release Cadence** | Regular minor releases | Stable + alpha tracks | Nightly + alpha | Slow (maintenance mode) | No recent stable; active branch | Rapid (v0.79.0 today) | Preview-driven (CI failure today) | Branding launch; active branch |
| **Unique Strength** | Rich plugin/skill/hooks system | Desktop handoff; local image gen | Evaluation infrastructure; SSRF protection | GitHub ecosystem lock-in | Headless JSON output; OpenRouter optimization | Lightweight; fast bug fixing | Declarative agents; Agent Team mode | Multi-vendor; community i18n efforts |
| **Unique Weakness** | macOS ECONNRESET; plugin fragility | Windows + WSL severe latency; auth instability | Catastrophic data loss incident; agent hangs | Background agent hangs; MCP URL errors | SQLite constraint errors; Bedrock instability | Project trust backlash; session export failures | OOM crashes; CI/release reliability | Migration confusion; PDF handling issues |

**Key takeaway:** **Claude Code** is the most **feature-rich and extensible**, but also has the **most complex failure surface**. **Pi** is the **fastest iteration** with 20 PRs+ today, but user trust is shaken by the new Project Trust feature. **Gemini CLI** leads in **safety infrastructure** (SSRF, quota limits, atomic MCP) but suffers from a catastrophic data loss incident. **OpenCode** excels in **CI/headless use cases** but struggles with database migrations. **Qwen Code** is pushing **multi-agent frontiers** (Agent Team, Dynamic Workflows) but has reliability gaps.

## 5. Community Momentum & Maturity

| Tool | Community Momentum | Maturity Indicators | Risk Signals |
|---|---|---|---|
| **Claude Code** | **High**—165 👍 on top issue; 55 comments on multi-window | Mature plugin ecosystem; regular releases; active PR review | Persistent macOS bug (#5674) unfixed for months; model confabulation reports |
| **OpenAI Codex** | **High**—76 comments on GPT-5.5 404; strong Windows/WSL discussion | Stable releases + alpha tracks; active PR pipeline (10 open) | GPT-5.5 availability confusion; WSL performance is a critical blocker |
| **Gemini CLI** | **Medium**—nightly releases; active safety-focused PRs | Evaluation infrastructure (#24353) shows systematic QA thinking | Data loss incident (#27397) is an existential trust crisis; subagent false successes |
| **GitHub Copilot CLI** | **Low**—30 issues but only 1 PR; maintenance mode | Stable, but not innovating; vi-mode (#13) has 63 👍 but no action | Background agent hangs; MCP registry bugs; hooks not firing |
| **Kimi Code CLI** | **Very Low**—0 PRs; 4 issues; silent regressions | In migration (Python → TypeScript); documentation deprecation banner added | Users don’t know which binary they’re running; API key auth silently removed |
| **OpenCode** | **Very High**—10 PRs today; 65 👍 on `/goal` | Strong feature velocity; active bug fixing (SQLite, Bedrock, PDF) | Database constraint errors from recent migrations; UI polish regressions |
| **Pi** | **Very High**—20 PRs today; v0.79.0 released | Rapid iteration with 20 PRs; active community feedback | Project Trust backlash (#5514); release notes with broken links (#5516) |
| **Qwen Code** | **High**—10 PRs today; multi-agent frontier | Declarative agents (#4842); Agent Team (#4844) are innovative | OOM crashes; CI failure for v0.18.0-preview; keybinding conflicts |
| **DeepSeek TUI (CodeWhale)** | **Medium**—branding transition; active PRs but closed/reopened churn | i18n effort is systematic; multi-vendor expansion is bold | Migration confusion (#2917); DSML call errors; FreeBSD timeout |

**Overall ranking of momentum (today):**
1. **OpenCode** & **Pi** (both extremely active with 10+ PRs and strong community engagement)
2. **Claude Code** & **Qwen Code** (large feature pushes but stability gaps)
3. **Gemini CLI** (safety-focused but trust recovery needed)
4. **OpenAI Codex** (strong PR pipeline but Windows/WSL as critical blockers)
5. **DeepSeek TUI (CodeWhale)** (branding transition, wait-and-see)
6. **GitHub Copilot CLI** (maintenance mode, low innovation)
7. **Kimi Code CLI** (transitional phase, minimal activity)

## 6. Trend Signals

### For Tool Developers

1. **Agent safety is the #1 risk factor.** The Gemini CLI data loss incident (#27397) and Claude Code confabulation reports (#66408, #66397) show that users will not tolerate agents performing destructive file I/O without guardrails. Expect **mandatory confirmation gates for file deletion/writing**, **tool-result microcompaction** (Qwen #4840), and **defensive programming patterns** to become table-stakes features.

2. **Declarative agent configuration is the next frontier.** Qwen Code (#4821, #4842) and DeepSeek TUI (#2482 WhaleFlow) are leading the shift from imperative agent definitions (scripts, prompts) to **declarative YAML/JSON-based agent teams**. This mirrors the shift from procedural programming to configuration-driven infrastructure. Tools without declarative agent support risk looking legacy in 6–12 months.

3. **Session persistence and lifecycle management are underserved.** Multi-window (#30154, Claude Code), session handoff (#66199, Claude Code), and cross-tab collaboration (#2753, DeepSeek TUI) are top requests across tools. Users want **persistent, inspectable, and recoverable sessions**—not ephemeral conversations. This is a clear unmet need.

4. **MCP is now a commodity, not a differentiator.** Every major tool supports MCP. The differentiator is now **MCP quality**: SSRF protection (Gemini #27626), atomic discovery (Gemini #27619), per-tool-call timeout (Gemini #27438), and approval consistency (Claude Code #64521, #61044).

5. **Windows + WSL is the hardest platform.** Every tool reports Windows/WSL issues (Claude Code #5674, #27897; OpenAI Codex #25715, #26149; GitHub Copilot CLI #3652; OpenCode #31329). The investment in cross-platform reliability separates mature tools from startups.

### For Developer Users

6. **Model availability confusion is epidemic.** OpenAI Codex (#26892), GitHub Copilot CLI (#2867), and Kimi Code CLI (#2442) all report models listed but unavailable, or silent removal of authentication methods. **Do not assume model availability—always verify with a test call.**

7. **Performance predictability is a key criterion.** Gemini CLI (#25166), OpenAI Codex (#25715, #26149), and Pi (#5464) all report **agent hangs** or **multi-minute delays** on simple operations. When evaluating tools, benchmark **time-to-first-response** and **session recovery speed** in your environment.

8. **The best tools are the ones that fail gracefully.** OpenCode’s retry logic (#31440), Gemini’s zero-quota fast-fail (#27698), and Pi’s `alwaysTrust` setting (#5515) show that **error handling design** is becoming a competitive advantage. Tools that crash on edge cases (Qwen OOM, GitHub Copilot background agent hang) lose trust quickly.

### Summary Outlook

- **Most investment-worthy for enterprise teams:** **OpenCode** (CI/headless strength, active development) or **Claude Code** (richest ecosystem, but require macOS ECONNRESET resolution).
- **Most innovative in multi-agent space:** **Qwen Code** with Agent Team and Dynamic Workflows.
- **Most promise for local-first users:** **Pi** (rapid iteration, local model support, lightweight) if it resolves Project Trust backlash.
- **Most at risk of stagnation:** **Kimi Code CLI** (silent regressions, migration confusion, zero PRs) and **GitHub Copilot CLI** (maintenance mode, community frustration with vi-mode).
- **Watch closely:** **DeepSeek TUI (CodeWhale)** — the branding reset and multi-vendor push could either catalyze growth or confuse users further.

**final thought:** The AI CLI tool market is converging on a core set of capabilities (MCP, session management, agent safety) while diverging on user experience and extensibility. The tools that will win are not the ones with the most features, but the ones that **combine power with reliability**—where agents do not hang, do not delete data, and do not require workarounds for basic operations. Today, **no tool fully delivers on this promise**, but OpenCode, Pi, and Claude Code are closest.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data from github.com/anthropics/skills — as of June 9, 2026*

---

## 1. Top Skills Ranking

The following skill proposals have generated the most community discussion. All remain **open** and pending review.

**#514 – document-typography**  
*Typographic quality control for AI-generated documents*  
Prevents orphan word wrap, widow paragraphs, and numbering misalignment — issues that affect every generated document. The community discussion highlights that this is a universal pain point, with multiple users noting that even simple typographic fixes dramatically improve output readability.  
[anthropics/skills/pull/514](https://github.com/anthropics/skills/pull/514)

**#486 – ODT (OpenDocument) skill**  
*Create, fill, read, and convert .odt/.ods files*  
Triggers on mentions of “ODT”, “ODS”, “ODF”, or “OpenDocument”. Discussion centers on LibreOffice integration and the need for open-source document format support alongside the existing DOCX skill. Some contributors want template-filling features to be split into a separate reference file.  
[anthropics/skills/pull/486](https://github.com/anthropics/skills/pull/486)

**#210 – frontend-design clarity & actionability**  
*Revision of the existing frontend-design skill*  
Aims to make every instruction executable within a single conversation and to provide specific, behavior-steering guidance. The thread reveals a broader community desire for skills that are “Claude-proofed” — i.e., not just documentation but actionable prompts.  
[anthropics/skills/pull/210](https://github.com/anthropics/skills/pull/210)

**#83 – skill-quality-analyzer & skill-security-analyzer**  
*Meta-skills for evaluating other skills*  
Adds two tools: one scores skills across structure, documentation, and examples; the other audits for security vulnerabilities (hardcoded secrets, prompt injection patterns, path traversal). Discussion reflects strong interest in quality assurance and trust boundaries for the ecosystem.  
[anthropics/skills/pull/83](https://github.com/anthropics/skills/pull/83)

**#1140 – agent-creator meta-skill**  
*Task-specific agent sets + multi-tool evaluation fixes*  
Resolves Issue #1120 and includes Windows path support for `recalc.py`. This PR is one of the most recent (May 2026) and has drawn attention for its meta-skill approach — enabling Claude to dynamically create specialized sub-agents.  
[anthropics/skills/pull/1140](https://github.com/anthropics/skills/pull/1140)

**#723 – testing-patterns skill**  
*Comprehensive testing coverage (unit, React, integration, visual, etc.)*  
Covers the Testing Trophy model, AAA pattern, and component testing with Testing Library. Discussion highlights that while testing skills exist, none have been as thorough; some users request additional sections for e2e testing with Playwright.  
[anthropics/skills/pull/723](https://github.com/anthropics/skills/pull/723)

**#568 – ServiceNow platform skill**  
*Broad ServiceNow assistant (ITSM, ITOM, SecOps, HRSD, etc.)*  
One of the largest skill proposals, covering the entire Now Platform. Community feedback focuses on balancing breadth with token efficiency; several contributors suggest splitting into domain-specific sub-skills.  
[anthropics/skills/pull/568](https://github.com/anthropics/skills/pull/568)

**#190 – n8n-builder & n8n-debugger (+ faf-expert)**  
*Workflow automation skills for n8n*  
Four production-tested skills. The n8n skills are particularly popular among DevOps and automation engineers, with discussions around MCP server integration and persistent project context via .faf files.  
[anthropics/skills/pull/190](https://github.com/anthropics/skills/pull/190)

---

## 2. Community Demand Trends

From the top-voted and most-commented Issues, five clear demand directions emerge:

| Demand Theme | Key Issues | Signal |
|---|---|---|
| **Org-wide skill sharing & management** | #228 (+7👍, 13 comments) – users want direct sharing links or a shared library instead of manual .skill file transfers | Strongest feature request |
| **Evaluation & testing tooling reliability** | #556 (+7👍, 11 comments) – `run_eval.py` returns 0% trigger rate on all skills; #202 – skill-creator needs overhaul; #1169 – 0% recall in optimization loop | Critical blocking issue for skill authors |
| **Windows compatibility** | #1099, #1050, #1140 (fixes) – subprocess, PATHEXT, and encoding bugs make skill-creation scripts unusable on Windows | Repeated, urgent demand |
| **Trust & security boundary control** | #492 (+2👍, 7 comments) – community skills under `anthropic/` namespace create impersonation risk; #1175 – SharePoint document handling raises permission concerns | Growing concern as adoption scales |
| **Multi-file bundling & portability** | #1220 – inline reference files; #1156 – honest portability labels across projects | Emerging design discussion |

Other notable mentions: MCP exposure of skills (#16), Bedrock compatibility (#29), and a proposed **agent-governance** safety pattern (#412, now closed but sparked debate).

---

## 3. High-Potential Pending Skills

These PRs are actively receiving comments and are likely to land soon:

- **#363 – feature-dev workflow fix** (TodoWrite overwrite bug) – directly addresses a reported regression that causes quality review and summary phases to be skipped. The fix is small and already well-reviewed.  
  [anthropics/skills/pull/363](https://github.com/anthropics/skills/pull/363)

- **#1140 – agent-creator meta-skill** – part of a wave of “meta” skills; multiple maintainers have expressed interest in merging after the Windows path fix is verified.  
  [anthropics/skills/pull/1140](https://github.com/anthropics/skills/pull/1140)

- **#568 – ServiceNow platform skill** – despite its size, the PR has generated several rounds of constructive feedback; the author has responded to all structural comments.  
  [anthropics/skills/pull/568](https://github.com/anthropics/skills/pull/568)

- **#509 – CONTRIBUTING.md** – community health gap closure; this is a non-code addition that is high impact and low risk.  
  [anthropics/skills/pull/509](https://github.com/anthropics/skills/pull/509)

- **#154 – shodh-memory (persistent context)** – a novel approach to cross-session memory; the author has been actively updating based on feedback about YAML structure.  
  [anthropics/skills/pull/154](https://github.com/anthropics/skills/pull/154)

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand at the Skills level is for reliable, cross-platform evaluation tooling (the `run_eval.py` / `skill-creator` toolchain) and for organizational governance features (sharing, security boundaries, and Windows support) that unlock skills as a collaborative enterprise asset rather than a solo developer tool.**

---

# Claude Code Community Digest — 2026-06-09

## Today’s Highlights
Claude Code v2.1.169 shipped with a new `--safe-mode` troubleshooting flag and `/cd` command for directory switching without cache loss. The community is heavily demanding multi-window desktop support (#30154, 55 comments) and continues to struggle with persistent ECONNRESET errors on macOS (#5674). Several fresh bugs appeared around tool-call parsing, model confabulation, and VSCode model picker mismatches.

## Releases
**v2.1.169** ([link](https://github.com/anthropics/claude-code/releases/tag/v2.1.169))
- Added `--safe-mode` flag and `CLAUDE_CODE_SAFE_MODE` env var to start with all customizations (CLAUDE.md, plugins, skills, hooks, MCP servers) disabled — useful for troubleshooting.
- Added `/cd` command to move a session to a new working directory without breaking the prompt cache.

## Hot Issues (Top 10 by community activity)

1. **Multi-window support for Desktop** [#30154](https://github.com/anthropics/claude-code/issues/30154) — 165 👍, 55 comments. Single-window sidebar session manager forces users to switch between sessions; request to open multiple windows simultaneously. Strong demand.

2. **Persistent ECONNRESET errors on macOS** [#5674](https://github.com/anthropics/claude-code/issues/5674) — 36 👍, 41 comments. Long-standing network issue causing connection drops and task interruptions. Reproducible only on macOS, not on Windows/Linux on same network.

3. **Cowork VM broken on Windows 11 Insider (MSIX)** [#27897](https://github.com/anthropics/claude-code/issues/27897) — 14 👍, 35 comments. EXDEV rename bug blocks usage on Windows 11 Insider builds. Regression in v1.1.4010, still unresolved.

4. **Agent tool isolation: “worktree” ignored for team agents** [#33045](https://github.com/anthropics/claude-code/issues/33045) — 9 👍, 19 comments. Agent runs in main repo despite `--worktree` flag. Affects Linux/WSL users relying on isolated workspaces.

5. **Claude creating too many files (filesystem bug) on long sessions** [#29573](https://github.com/anthropics/claude-code/issues/29573) — 22 👍, 16 comments. Over time, Claude creates excessive temp files leading to quota issues. Impact on users with long-running sessions.

6. **Chrome MCP tools: “Navigation to this domain is not allowed”** [#43255](https://github.com/anthropics/claude-code/issues/43255) — 7 👍, 13 comments. Regression in v1.0.66 where MCP browser tools block all domains. Blocks web automation workflows.

7. **Conversation Branching (fork/merge/tree navigation)** [#32631](https://github.com/anthropics/claude-code/issues/32631) — 30 👍, 9 comments. Consolidated spec for branching beyond basic `/fork`. High upvote ratio suggests strong desire for richer session management.

8. **MCP tool calls in Routines fail with no approval UI** [#61044](https://github.com/anthropics/claude-code/issues/61044) — 3 👍, 6 comments. Routines silently fail when MCP tools require approval; no UI appears and reconnect doesn’t help. Critical for autonomous workflows.

9. **User-level skills discovery** [#66352](https://github.com/anthropics/claude-code/issues/66352) — 0 👍, 4 comments. Request to support `~/.agents/skills/` for cross-agent single-source-of-truth. Low votes but demonstrates growing ecosystem need.

10. **CLI ignores claude.ai MCP “approval required” settings** [#64521](https://github.com/anthropics/claude-code/issues/64521) — 0 👍, 3 comments. Imported MCP connectors from web UI don’t inherit per-tool approval toggles in CLI. Security and consistency gap.

## Key PR Progress (all 5 PRs updated in last 24h)

1. **fix(plugins): add missing plugin.json manifest for plugin-dev** [#65286](https://github.com/anthropics/claude-code/pull/65286) — Open. Adds required manifest so `plugin-dev` can be discovered and installed through normal plugin mechanisms. Small but important for plugin ecosystem health.

2. **fix(plugins): align frontend-design author with marketplace entry** [#65619](https://github.com/anthropics/claude-code/pull/65619) — Closed. Fixes malformed `author` fields (two emails in one string). Resolves #61785.

3. **fix(devcontainer): detect Docker daemon failures via $LASTEXITCODE** [#66372](https://github.com/anthropics/claude-code/pull/66372) — Open. Fixes false-positive Docker daemon check on Windows when Docker Desktop is not running. PowerShell try/catch doesn’t catch native command exit codes.

4. **docs: add rules frontmatter paths syntax examples and validation hook** [#26914](https://github.com/anthropics/claude-code/pull/26914) — Closed. Adds correct/incorrect examples for frontmatter `paths:` syntax and a PostToolUse hook to detect broken paths. Addresses silent failure root cause.

5. **fix(extensibility.py): follow symlinks in project-controlled gui** [#66171](https://github.com/anthropics/claude-code/pull/66171) — Open. Security fix for symlink following in GUI. Includes vulnerability analysis, reproduction guide, and secure implementation. Reviewed but pending merge.

## Feature Request Trends
- **Multi-window Desktop**: #30154 dominates with 165 👍. Users want true window-level concurrency, not just sidebar sessions.
- **Conversation branching**: #32631 (30 👍) consolidates multiple older requests. Users seek full fork/merge/tree navigation beyond basic `/fork`.
- **User-level skills & cross-agent workflows**: #66352, #66373. Demand for reusable skill discovery and session handoff (local→web) is growing as multi-agent usage increases.
- **Customizable keybindings**: #66399 requests ability to bind file opening (e.g., settings.json) to keyboard shortcuts.
- **Folder/bins for normal chat**: #66405 — organization feature inspired by other chat UIs.

## Developer Pain Points
1. **Network reliability on macOS** — #5674 ECONNRESET remains unfixed, affecting many Mac users daily. Workaround on Windows/Linux not always available.
2. **Agent isolation gaps** — #33045 shows worktree flag is ignored for team agents; no per-agent model/effort configuration (#66402).
3. **MCP approval inconsistencies** — Approval settings from claude.ai are ignored in CLI (#64521), and Routines fail silently when approval is needed (#61044).
4. **Context loss during upgrades** — #66406 reports complete session loss after clicking software upgrade. Critical UX regression.
5. **Tool-call parsing failures** — #66400: intermittent “malformed” tool calls with markup rendered as chat text. Affects reliability on long sessions.
6. **Model confabulation issues** — #66408 (fabricated conversation turns, false file operations) and #66397 (fabricated user message) report safety-critical hallucinations in Opus 4.8.
7. **Windows-specific bugs** — Japanese text corruption (#66396), missing cursor in agents view (#66398), VSCode model picker mismatch (#66403), Cowork model silently changed after update (#66407). Windows remains a less stable platform.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-09

## Today’s Highlights
The `rust-v0.138.0` release went stable, bringing CLI‑to‑Desktop handoff on macOS/Windows and local image support. A critical bug report (#26892) exploded to 76 comments after `gpt‑5.5` became unavailable despite being listed – the community is actively investigating. Meanwhile, Windows + WSL performance continues to dominate issue traffic, with multiple reports of severe latency and resource leaks driving a wave of backend fixes in today’s PRs.

---

## Releases
No stable releases were cut in the last 24 hours; the latest stable remains **rust-v0.138.0** (released earlier). Two alpha pre‑releases were published:

- **rust-v0.139.0-alpha.1** – pre‑release of the next minor version  
- **rust-v0.138.0-alpha.7** & **rust-v0.138.0-alpha.8** – incremental alphas on the stable branch  

**Changelog highlights for v0.138.0 (from previous days):**  
- The `/app` command can now hand off the current CLI thread into Codex Desktop on macOS and native Windows.  
- Windows workspace launches can open directly into Desktop instead of stopping at a manual prompt.  
- Local image attachments and standalone image generation are now supported.

---

## Hot Issues (Top 10 by Community Activity)

1. **[#26892] gpt‑5.5 listed as available but requests fail with 404**  
   *76 comments, 28 👍*  
   The model is shown in local metadata but actual API calls return “Model not found”. Affects both Desktop and CLI on Windows. Community suspects a stale model catalogue or a server‑side rollout glitch.  
   [https://github.com/openai/codex/issues/26892](https://github.com/openai/codex/issues/26892)

2. **[#25144] Option to disable automatic conversion of long pasted prompts into .txt attachments**  
   *52 comments, 65 👍*  
   A highly‑requested UX feature. Users find the behaviour disruptive for structured prompts that are not meant to be files.  
   [https://github.com/openai/codex/issues/25144](https://github.com/openai/codex/issues/25144)

3. **[#25203] GitHub OAuth callback fails with “Unable to find Electron app” on Windows**  
   *37 comments, 21 👍*  
   Auth flow is broken for many Windows users, blocking integration with GitHub. Likely a protocol‑handler registration issue.  
   [https://github.com/openai/codex/issues/25203](https://github.com/openai/codex/issues/25203)

4. **[#25715] Codex App unusably slow with WSL as agent environment**  
   *36 comments, 36 👍*  
   Routine operations become sluggish. Multiple users confirm performance is fine inside WSL CLI but not through the Desktop app.  
   [https://github.com/openai/codex/issues/25715](https://github.com/openai/codex/issues/25715)

5. **[#25719] Codex Desktop on macOS triggers `syspolicyd`/`trustd` CPU/memory runaway**  
   *20 comments, 20 👍*  
   Persistent high CPU usage after launch – impact extends beyond Codex to the entire system.  
   [https://github.com/openai/codex/issues/25719](https://github.com/openai/codex/issues/25719)

6. **[#24675] Stale app connector link after reauth‑required 401**  
   *21 comments, 16 👍*  
   Connec­tors (e.g., Linear) keep using old auth tokens even after reauthentication. Manual cache clear required.  
   [https://github.com/openai/codex/issues/24675](https://github.com/openai/codex/issues/24675)

7. **[#26149] Windows + WSL repeatedly scanning `.codex/.tmp/plugins` over `/mnt/c`**  
   *10 comments, 16 👍*  
   Causes severe per‑command latency. `strace` shows a recursive scan; CLI inside WSL works fine.  
   [https://github.com/openai/codex/issues/26149](https://github.com/openai/codex/issues/26149)

8. **[#21671] `/compact` fails with unknown `service_tier` parameter (regression in 0.129.0)**  
   *25 comments (closed)*  
   While closed, the issue generated discussion about API‑key auth misconfigured with provider‑scoped keys.  
   [https://github.com/openai/codex/issues/21671](https://github.com/openai/codex/issues/21671)

9. **[#12029] Ability to use more than one account across Codex surfaces**  
   *9 comments, 43 👍*  
   Multi‑account support (personal + corporate) is a top feature request, especially for VS Code extension users.  
   [https://github.com/openai/codex/issues/12029](https://github.com/openai/codex/issues/12029)

10. **[#8758] Image generation from Codex**  
    *23 comments (closed), 55 👍*  
    Although closed, the strong upvote count signals ongoing demand for native image creation capabilities.  
    [https://github.com/openai/codex/issues/8758](https://github.com/openai/codex/issues/8758)

---

## Key PR Progress (Top 10)

1. **#26880 – Preserve fsmonitor for worktree Git reads**  
   Fixes a performance regression where Codex disabled Git’s built‑in fsmonitor, causing full‑scan reads in large repos. *Code‑reviewed, open.*  
   [https://github.com/openai/codex/pull/26880](https://github.com/openai/codex/pull/26880)

2. **#27109 – Add Guardian catalog diagnostics metadata**  
   Adds fields to track whether `codex‑auto‑review` is in the client‑side model catalog, helping debug fallback behaviour. *Open.*  
   [https://github.com/openai/codex/pull/27109](https://github.com/openai/codex/pull/27109)

3. **#27094 – Add spans to `build_tool_router`**  
   Instrumentation to measure `append_tool_search_executor` costs (~113ms avg) – first step toward optimisation. *Code‑reviewed, open.*  
   [https://github.com/openai/codex/pull/27094](https://github.com/openai/codex/pull/27094)

4. **#27106 – Remove remote compaction failure log**  
   Cleanup after removing the only consumer of `log_remote_compact_failure`. *Merged.*  
   [https://github.com/openai/codex/pull/27106](https://github.com/openai/codex/pull/27106)

5. **#27101 – Load user instructions through an injected provider**  
   Decouples `codex‑core` from `$CODEX_HOME` – embedders supply user instructions. Improves modularity. *Open.*  
   [https://github.com/openai/codex/pull/27101](https://github.com/openai/codex/pull/27101)

6. **#25704 – Normalize Codex images for Responses strict mode**  
   Feature‑flagged support for preparing image inputs (local/data URLs, re‑encoding) before sending to `/responses`. *Open.*  
   [https://github.com/openai/codex/pull/25704](https://github.com/openai/codex/pull/25704)

7. **#27039 – Add detached async command hooks**  
   Enables hooks to run asynchronously without blocking the main lane – a long‑awaited capability for complex workflows. *Open.*  
   [https://github.com/openai/codex/pull/27039](https://github.com/openai/codex/pull/27039)

8. **#27017 – Fix Windows `deny‑read` across exec runtimes**  
   Resolves a security/permission gap where `deny_read` restrictions were not applied in `shell_command` / `exec_command` on Windows. *Code‑reviewed, open.*  
   [https://github.com/openai/codex/pull/27017](https://github.com/openai/codex/pull/27017)

9. **#17931 – Support encrypted local secrets for keyring auth**  
   Works around Windows Credential Manager’s 2,560‑byte limit on generic credential blobs by encrypting large auth payloads. *Open.*  
   [https://github.com/openai/codex/pull/17931](https://github.com/openai/codex/pull/17931)

10. **#27091 – Eagerly compact Guardian threads between reviews**  
    Schedules compaction for reused Guardian review sessions immediately after a review when the context exceeds threshold – reduces token waste. *Open.*  
    [https://github.com/openai/codex/pull/27091](https://github.com/openai/codex/pull/27091)

---

## Feature Request Trends

- **Multi‑account & multi‑session management** – Support for simultaneously logged‑in personal/corporate accounts (#12029) and a TUI‑based Agent View for parallel sessions (#22321).  
- **Enhanced image handling** – Native image generation (#8758, closed but strongly upvoted) and better control over pasted prompt conversion (#25144).  
- **Advanced hook parity** – Full Claude Code hook compatibility (#21753) including async (#27039 already merged) and lifecycle coverage.  
- **User‑controlled context clearing** – First‑class ability to persist session IDs while clearing context for task switching (#23218).  
- **Git worktree support** – Allow Codex to use worktrees created outside the app (#12863).  
- **Non‑interactive MCP tool approval** – Provide a safe way to approve MCP calls without sacrificing sandbox restrictions (#24135).

---

## Developer Pain Points

- **Windows + WSL performance** – Three separate issues (#25715, #26149, #22185) report severe latency, scan overhead over `/mnt/c`, and `CreateProcess` failures.  
- **Authentication & session instability** – GitHub OAuth fails on Windows (#25203), stale connector links (#24675), and complete loss of conversations after restart (#19615, #27104).  
- **Model availability confusion** – GPT‑5.5 shows as available but returns 404 (#26892), causing workflow disruption.  
- **macOS resource leaks** – `syspolicyd`/`trustd` CPU runaway (#25719) and locked‑mode Computer Use hanging (#26415).  
- **Subagent / Guardian brittleness** – Subagent close requests kill agent loops (#23971), Guardian review failures are not retried (now addressed in #27062), and hook post‑GC compaction needs optimisation (#27091).  
- **UI rendering problems on Windows** – Semi‑transparent sidebar causes undrawn regions (#25249), and the in‑app browser stops responding to commands (#23222).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-09

## Today's Highlights

A critical incident involving catastrophic data loss (Issue #27397) continues to dominate community discussion, highlighting fundamental safety gaps in the agent's file I/O reasoning. The nightly release v0.47.0-nightly.20260609 ships with minor housekeeping, while the PR queue shows meaningful progress on PTY robustness, SSRF protection for MCP OAuth, and a new per-tool-call timeout configuration. Several high-priority bug fixes around shell command hanging and subagent false-success reporting remain open and await retesting.

## Releases

A single nightly release shipped today:
- **[v0.47.0-nightly.20260609.g0567b25a2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-nightly.20260609.g0567b25a2)** — Two changes: an update capping the Antigravity transition banner display frequency ([PR #27676](https://github.com/google-gemini/gemini-cli/pull/27676)), and removal of the "experimental" label from browser agent documentation ([PR #27746](https://github.com/google-gemini/gemini-cli/pull/27746)).

## Hot Issues

1. **[#27397 — Catastrophic Data Loss by Agent Reasoning (CLOSED)](https://github.com/google-gemini/gemini-cli/issues/27397)** — *8 comments.* The most severe issue this week. A generated Node.js script permanently deleted 1.2 TB of curated media. Community reaction is tense; the failure is attributed to the agent's lack of defensive programming. The issue is now closed, but broader safety implications remain.

2. **[#21409 — Generalist Agent Hangs Indefinitely (OPEN)](https://github.com/google-gemini/gemini-cli/issues/21409)** — *7 comments, 8 👍.* Users report that any task deferring to the generalist agent hangs "for up to an hour." A workaround exists (instructing the model not to defer), but no fix has landed. High community frustration.

3. **[#22323 — Subagent False Success After MAX_TURNS (OPEN)](https://github.com/google-gemini/gemini-cli/issues/22323)** — *6 comments.* The `codebase_investigator` subagent reports `status: "success"` / `"GOAL"` even when it exhausted its turn limit before performing any analysis. This masking of failures undermines debugging.

4. **[#22745 — AST-Aware File Reads & Codebase Mapping (OPEN)](https://github.com/google-gemini/gemini-cli/issues/22745)** — *7 comments, 1 👍.* An ongoing investigation into whether AST-aware tools can reduce token waste and improve navigation precision. A longer-term architecture improvement with significant potential.

5. **[#24353 — Robust Component-Level Evaluations (OPEN)](https://github.com/google-gemini/gemini-cli/issues/24353)** — *7 comments.* An EPIC tracking 76 behavioral eval tests across 6 models, aiming to replace brittle manual testing with automated component-level coverage. Important for quality assurance.

6. **[#21968 — Gemini Doesn't Use Custom Skills/Sub-Agents (OPEN)](https://github.com/google-gemini/gemini-cli/issues/21968)** — *6 comments.* Anecdotal but widely confirmed: the agent rarely invokes user-installed skills or sub-agents unless explicitly instructed, even for closely related tasks.

7. **[#21983 — Browser Agent Fails on Wayland (OPEN)](https://github.com/google-gemini/gemini-cli/issues/21983)** — *4 comments, 1 👍.* The browser subagent crashes on Wayland with `Termination Reason: GOAL` but no useful output. Blocks Linux users from browser automation.

8. **[#25166 — Shell Command Hangs After Completion (OPEN)](https://github.com/google-gemini/gemini-cli/issues/25166)** — *4 comments, 3 👍.* A high-frustration issue: simple commands finish but the agent hangs, showing "Awaiting user input." Occurs even with trivial commands.

9. **[#27421 — `autoConfigureMemory` Ignores `GEMINI_CLI_HOME` (CLOSED)](https://github.com/google-gemini/gemini-cli/issues/27421)** — *5 comments.* A bootstrap path reads settings before the full settings system loads, causing configuration to be ignored. Fixed in PR #27425.

10. **[#26525 — Auto Memory: Deterministic Redaction & Reduced Logging (OPEN)](https://github.com/google-gemini/gemini-cli/issues/26525)** — *5 comments.* Security concern: Auto Memory sends transcript content to a model before redaction, and the service may log existing skill contents. Needs deterministic redaction upstream.

## Key PR Progress

1. **[#27428 — Fix Docker `imageExists` via Exit Code (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/27428)** — Fixes false negatives in sandbox image detection by switching from stdout parsing to `docker inspect --type=image` exit code, addressing DOCKER_BUILDKIT stderr output.

2. **[#27429 — Handle EBADF in `resizePty` (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/27429)** — Fixes crash on `--resume` when PTY file descriptor is stale. Treats `EBADF` the same as `ESRCH`, preventing an unhandled exception.

3. **[#27626 — Block Private OAuth Metadata URLs (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27626)** — Adds SSRF protection to MCP OAuth metadata discovery by preventing `fetch()` calls on private/reserved IPs from remote server responses.

4. **[#27619 — Atomic MCP Tool Discovery (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27619)** — Ensures MCP tools are retained during transient network failures by implementing an atomic update pattern. Prevents "tool not found" errors after brief drops.

5. **[#27438 — Configurable Per-Tool-Call Timeout (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/27438)** — Introduces `tools.callTimeout` configuration, a global timeout enforced in `ToolExecutor` via a reusable `withTimeout()` utility. A long-requested reliability feature.

6. **[#27747 — Fix Infinite Loop in Ghost Text Wrapping (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27747)** — Fixes a terminal freeze when an `@filename:line` completion is active and the terminal is too narrow for a wide character (e.g., emoji). Solves a niche but frustrating UI hang.

7. **[#27603 — Platform-Aware Shell Guidance (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27603)** — Adds Windows-specific shell command examples to the operational prompt instead of Unix-only examples. Useful for cross-platform parity.

8. **[#27744 — Resolve DNS Before SSRF Guard (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27744)** — Prevents SSRF bypass via wildcard DNS services (e.g., `127.0.0.1.nip.io`) by resolving hostnames before performing private-IP checks.

9. **[#27729 — Truncate Telemetry Attributes (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27729)** — Fixes GCP export errors by truncating telemetry metric attributes to 1024 characters. Stops noisy stack traces when requesting `--format json` output.

10. **[#27698 — Fail Fast on Zero-Quota Limits (OPEN)](https://github.com/google-gemini/gemini-cli/pull/27698)** — Prevents a 10-attempt retry loop when hitting a hard quota limit of 0 (e.g., on unbilled free-tier accounts). A quality-of-life fix for new users.

## Feature Request Trends

- **AST-Aware Code Understanding** — Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) investigate using AST-aware tools for precise file reads, search, and codebase mapping to reduce token waste and improve agent precision.
- **Better Agent Self-Awareness & Configuration** — Users want the agent to accurately describe its own flags, hotkeys, and capabilities ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)). Also requested: the agent should understand and respect `settings.json` overrides (e.g., `maxTurns`) ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).
- **Improved Evaluation Infrastructure** — EPIC [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) calls for robust component-level eval tests across models, while [#23166](https://github.com/google-gemini/gemini-cli/issues/23166) seeks to stabilize internal project evals against "bleed" and unreliability.
- **Memory System Robustness** — The Auto Memory feature is under active scrutiny: requests include deterministic redaction upstream ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), preventing retries on low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), and quarantining invalid patches ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)).
- **Sub-Agent and Skill Adoption** — The agent rarely uses custom skills or sub-agents unless explicitly told ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)). Community strongly desires better automatic reasoning about when to delegate.

## Developer Pain Points

- **AI Agents Causing Data Loss** — The catastrophic data loss incident ([#27397](https://github.com/google-gemini/gemini-cli/issues/27397)) has shaken user trust. The community demands fundamental defensive programming in file I/O, especially for destructive operations.
- **Agent Unreliability: Hangs & False Successes** — Multiple issues report the generalist agent hanging indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), sub-agents falsely reporting success after hitting turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), and shell commands hanging after completion ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)). These are daily workflow blockers.
- **Configuration Overrides Being Ignored** — Issues like [#27421](https://github.com/google-gemini/gemini-cli/issues/27421) (`autoConfigureMemory` ignoring `GEMINI_CLI_HOME`) and [#22267](https://github.com/google-gemini/gemini-cli/issues/22267) (browser agent ignoring `settings.json`) show that settings propagation across initialization paths is fragile.
- **Tool & MCP Integration Friction** — `wait_for_previous` being forwarded to MCP servers ([#27403](https://github.com/google-gemini/gemini-cli/issues/27403)), shell commands being treated as literal executable paths ([#27404](https://github.com/google-gemini/gemini-cli/issues/27404)), and sub-agents running without permission since v0.33.0 ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) point to significant integration quality issues.
- **400 Errors with >128 Tools** — When too many tools are available, Gemini CLI hits API errors ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)). Users want smarter tool scoping to avoid hitting provider limits.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI Community Digest — 2026-06-09

### Today’s Highlights
No new releases landed in the past 24 hours, but the community remains highly active with 30 issues and one pull request updated. The most notable discussions center on long‑standing feature requests (vi‑mode input, pause/resume sessions) and critical bugs affecting background sub‑agents and MCP custom registries. A single closed PR improves the install script for authenticated environments.

---

### Releases
No new versions of `github/copilot-cli` were published in the last 24 hours.

---

### Hot Issues (10 Noteworthy)

1. **#1928 – Allow to pause copilot work**  
   Author: laeubi | Comments: 9 | 👍: 2  
   [Link](https://github.com/github/copilot-cli/issues/1928)  
   The ability to pause a session mid‑execution and inject additional context is a recurring pain point. This request has the highest comment count today, indicating strong interest.

2. **#13 – CLI input should have a vi/vim input mode**  
   Author: RyanHecht | Comments: 7 | 👍: 63  
   [Link](https://github.com/github/copilot-cli/issues/13)  
   By far the most upvoted issue, reflecting a persistent demand from modal‑editor users for efficient keyboard‑driven navigation inside the interactive CLI.

3. **#3547 – Background sub‑agent silently hangs at total_turns=0 when model="gpt-5.5"**  
   Author: ravisha22 | Comments: 6 | 👍: 0  
   [Link](https://github.com/github/copilot-cli/issues/3547)  
   A reliability bug that renders background agent tasks non‑functional with a specific model. Community concern is high because background tasks are a marquee feature.

4. **#3436 – /mcp search constructs wrong URL for custom MCP registries**  
   Author: lvthillo | Comments: 5 | 👍: 1  
   [Link](https://github.com/github/copilot-cli/issues/3436)  
   A hard 404 for self‑hosted MCP registries due to a missing `/v0.1/` segment. This breaks enterprise deployments relying on custom registries.

5. **#2867 – Claude Opus 4.6 (high) returns "model not supported" after quota wait**  
   Author: jeffreybulanadi | Comments: 5 | 👍: 1  
   [Link](https://github.com/github/copilot-cli/issues/2867)  
   Users prompted to wait for quota reset are then locked out permanently. This misleading user experience frustrates Pro+ subscribers.

6. **#2540 – Plugin‑defined preToolUse hooks do not fire in main session or subagents**  
   Author: solvaholic | Comments: 4 | 👍: 3  
   [Link](https://github.com/github/copilot-cli/issues/2540)  
   A core hook extension point is completely broken, undermining the plugin system’s promise of custom tool‑use logic.

7. **#2201 – sessionStart hook doesn't print to terminal and doesn't run at CLI startup**  
   Author: samuelcho‑msft | Comments: 3 | 👍: 2  
   [Link](https://github.com/github/copilot-cli/issues/2201)  
   Another hooks issue: the session‑start lifecycle event is not triggered as documented, making audit‑log and banner scripts unreliable.

8. **#3652 – 40‑80 second startup delays in WSL due to listSessions**  
   Author: vishalnarayan2809 | Comments: 3 | 👍: 0  
   [Link](https://github.com/github/copilot-cli/issues/3652)  
   Severe latency on WSL users, directly attributed to a single API call. This impacts developer productivity in mixed‑OS environments.

9. **#3701 – Runaway MCP server spawning (IDE lock‑file watcher re‑init loop)**  
   Author: wibjorn | Comments: 2 | 👍: 0  
   [Link](https://github.com/github/copilot-cli/issues/3701)  
   A resource‑exhaustion bug on Windows where MCP servers are spawned repeatedly, causing IDE integration to degrade. Closed as a confirmed bug.

10. **#2966 – Built‑in tooling for managing multiple concurrent CLI sessions**  
    Author: JoshLove‑msft | Comments: 2 | 👍: 0  
    [Link](https://github.com/github/copilot-cli/issues/2966)  
    Power users running many parallel sessions (e.g., with `--yolo --autopilot`) lack first‑class session management, highlighting a gap in the CLI’s workflow model.

---

### Key PR Progress

**#1960 – install: use GITHUB_TOKEN for authenticated GitHub requests**  
Author: devm33 | State: Closed  
[Link](https://github.com/github/copilot-cli/pull/1960)  
This clean PR makes the install script respect the `GITHUB_TOKEN` environment variable to avoid rate limits and support private‑repo installations. The change covers curl, wget, and git ls‑remote. Only one pull request received updates in the last 24 hours.

---

### Feature Request Trends

Common themes across the 30 recent issues:

- **Input & interaction improvements** – vi‑mode input (#13), session pause/resume (#1928), stash half‑typed commands via `ESC ESC` (#3720), visual delimiters around agentic iterations (#3718).
- **Model flexibility & cost** – Ability to switch between models mid‑session, including BYOK/local models (#3709), support for lower‑cost / open‑weight models (#3707), and an option to disable streaming for BYOK providers (#3717).
- **Session & workflow management** – First‑class multi‑session management (#2966), cron‑style scheduled tasks (#3714), and better feedback on agentic loop progress.
- **Enterprise & integration** – OTel auth with mTLS and dynamic headers (#3477), consistent resolution paths for custom agents vs. skills (#3688), and fixes for custom MCP registry URLs (#3436).
- **Plugin/hooks extensibility** – Hooks that can modify the user prompt (#3713), and fixes for hooks not triggering in subagents or at startup (#2540, #2201).

---

### Developer Pain Points

Recurring frustrations from the bug reports and feature gaps:

1. **Background agent reliability** – Sub‑agents hang silently with `total_turns=0` for certain models (#3547).
2. **MCP integration brittleness** – Wrong registry URLs (#3436), runaway server spawning on Windows (#3701), agent‑level tool whitelist not enforced (#2638).
3. **Model availability after quota** – Permanent “model not supported” after being told to wait (#2867).
4. **Hooks not firing** – `preToolUse` hooks do not fire in subagents (#2540); `sessionStart` hook does not run at startup (#2201).
5. **Windows‑specific quirks** – Copy‑on‑select clipboard feature circumvented (#3724), uninstall failure (#3662), `~` in `/add-dir` path not handled (#3719), ReFS/Dev‑Drive sandbox limitation (#3712).
6. **Inconsistent UX** – `/model` picker uses arrow‑keys for model selection but numeric input for effort/context (#3715), `ask_user` text formatting issues (#3722).
7. **Installation breakage** – FreeBSD misidentified as Windows (#3710); `--available-tools` flags ignored in ACP mode (#2948).
8. **Configuration discovery mismatch** – Custom agents resolved against git root, but skills and `.mcp.json` against `cwd` (#3688).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-09

## Today's Highlights

No new releases landed in the last 24 hours, but the community flagged two critical regressions in the 0.11.0 version: **silent removal of API key authentication** from the “Kimi Code” product, and the **disappearance of the `@filename` file attachment syntax** introduced in earlier Python-based CLI builds. Additionally, an installation anomaly (#2436) shows the terminal reporting both failure and success, causing confusion about the correct version string (1.47.0 vs. 0.11.0). A documentation enhancement (#2376) was closed, adding a deprecation banner to redirect users from the Python-based `kimi-cli` to the TypeScript rewrite.

## Releases

*No new versions published in the last 24 hours.*

## Hot Issues

### 1. Installation failed – ambiguous success/failure state  
**#2436** – [OPEN] [[bug] Installation failed. The new Kimi Code is installed ✓ Kimi can't seem to make up her mind.](https://github.com/MoonshotAI/kimi-cli/issues/2436)  
**Author:** pleabargain | **Comments:** 1 | **👍:** 0  
**What’s happening:** After running the installer, the terminal prints both a failure message and a success checkmark. The reporter’s `-V` shows `1.47.0`, which may be the Python CLI, while other issues mention `0.11.0` for the TypeScript rewrite. This inconsistency suggests the installer may be mixing binaries or failing to cleanly replace the old version.  

### 2. Broken Workflow – API key authentication silently removed  
**#2442** – [OPEN] [[bug] Broken Workflow](https://github.com/MoonshotAI/kimi-cli/issues/2442)  
**Author:** andrew-sz | **Comments:** 0 | **👍:** 0  
**What’s happening:** A regression in the “Kimi Code” product (TypeScript rewrite, v0.11.0) has silently dropped support for API‑key‑based authentication. Users who rely on programmatic login without a web browser are blocked. The issue is tagged as a regression, and no workaround is provided yet.  

### 3. `@filename` no longer supported in new version  
**#2441** – [OPEN] [[bug] 新版本现在连@filename都不支持了？ / The new version does not even support @filename now?](https://github.com/MoonshotAI/kimi-cli/issues/2441)  
**Author:** Liufangyu | **Comments:** 0 | **👍:** 0  
**What’s happening:** The user reports that the new v0.11.0 (presumably the TypeScript rewrite) no longer recognizes the `@filename` syntax for file attachment, a feature that existed in the Python `kimi-cli`. This breaks existing workflows and scripts that relied on inline file referencing. The issue is filed in the same repository but may affect the new product line.  

### 4. Deprecation banner added for Python CLI docs  
**#2376** – [CLOSED] [[enhancement] [Docs] Add deprecation banner on GitHub Pages: redirect users to kimi-code (TypeScript rewrite)](https://github.com/MoonshotAI/kimi-cli/issues/2376)  
**Author:** MengyangGao | **Comments:** 0 | **👍:** 0  
**What’s happening:** This enhancement was merged and closed. It adds a visible banner to the Python `kimi-cli` documentation site, alerting users that the project is superseded by the TypeScript rewrite (`kimi-code`). This should reduce confusion, though the version inconsistency observed in #2436 indicates the transition is not yet seamless.

## Key PR Progress

*No pull requests were updated in the last 24 hours.*

## Feature Request Trends

The most prominent request direction from the week’s issues is **feature parity and migration clarity** between the Python `kimi-cli` and the TypeScript `kimi-code` rewrite. Users expect the new version to maintain core functionality (e.g., `@filename` attachment, API‑key auth) while the repository still houses both products under the same name. The deprecation banner (#2376) addresses the documentation gap, but the two regressions (#2441, #2442) show that feature parity is not yet achieved. There is also an undercurrent of desire for **clear version reporting** to distinguish which binary is installed.

## Developer Pain Points

- **Version confusion:** The same repository produces two different products with overlapping names, and the installed version string (`1.47.0` vs. `0.11.0`) does not clearly tell users which CLI they are running.  
- **Silent regressions:** API‑key authentication was removed without notice in v0.11.0, breaking CI/CD and headless setups.  
- **Feature removal without migration path:** The `@filename` syntax was a beloved onboarding feature; its disappearance in the new version forces users to re‑learn file handling.  
- **Installation reliability:** Mixed success/failure output (#2436) erodes trust in the setup process, especially when users cannot confirm which binary took effect.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-06-09

## Today's Highlights

A wave of SQLite `NOT NULL constraint failed: session_message.seq` errors is disrupting sessions that trigger agent switches or use `opencode run` / HTTP endpoints, with multiple reports filed in the last 24 hours. Meanwhile, Bedrock Mantle provider issues (empty responses, signature mismatches) are blocking users of GPT‑5.5 and Bedrock‑compatible gateways. On the PR side, fixes for JSON streaming output, config directory crashes, and network retry logic are moving quickly.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#27167 – Native session goals with /goal**  
   Persistent session lifecycle feature requested with 65 👍 and 37 comments. Community strongly desires a built‑in `/goal` command to set and track objectives across turns, reducing reliance on external agent plugins.  
   https://github.com/anomalyco/opencode/issues/27167

2. **#5474 – `/undo` only rolls back conversation, not file changes**  
   Long‑standing (since Dec 2025) mismatch between UI revert and actual file system state. 28 comments, 12 👍. Developers report confusion when “undo” leaves edited code in place.  
   https://github.com/anomalyco/opencode/issues/5474

3. **#29548 – OpenAI provider header timeout regression**  
   After upgrading to 1.15.11, requests fail with “Provider response headers timed out after 10000ms”. Fixed by increasing `headerTimeout`. 11 comments, 0 👍 – likely under‑reported due to niche environment.  
   https://github.com/anomalyco/opencode/issues/29548

4. **#30948 – Amazon Bedrock provider returns empty output against gateway**  
   Version 1.16.0 broke Bedrock‑compatible gateways that worked previously. 8 comments, 4 👍. Users are blocked on non‑AWS Bedrock endpoints.  
   https://github.com/anomalyco/opencode/issues/30948

5. **#31247 – Opus 4.8 via GitHub Copilot leaks tool‑call text**  
   In long sessions, assistant messages contain literal `call read`, `call write`, etc. triggers prefilling errors. 6 comments.  
   https://github.com/anomalyco/opencode/issues/31247

6. **#15535 – Support MCP Resources in addition to Tools**  
   Feature request to expose `resources/read` from MCP servers. 16 👍, 6 comments. Enables richer context retrieval from external systems.  
   https://github.com/anomalyco/opencode/issues/15535

7. **#16960 – Compaction loses AGENTS.md/CLAUDE.md context**  
   When sessions are compacted, the compaction LLM receives an empty system prompt, discarding project instructions. 5 comments, 2 👍. Impacts long‑running agent workflows.  
   https://github.com/anomalyco/opencode/issues/16960

8. **#31204 – session_message.seq NOT NULL constraint on agent‑switched sessions**  
   New projection table migrations (June 3‑5) cause crashes when `appendMessage()` is called during agent switches. 4 comments, 2 👍.  
   https://github.com/anomalyco/opencode/issues/31204

9. **#31430 – Bedrock Mantle empty successful responses**  
   GPT‑5.5 via Bedrock Mantle intermittently returns empty responses, halting agentic tasks without error. 3 comments.  
   https://github.com/anomalyco/opencode/issues/31430

10. **#31441 – Folder and nav buttons missing in UI**  
    User reports that folder and navigation buttons disappeared from top menu in v1.16.x (regression from 1.14). 4 comments.  
    https://github.com/anomalyco/opencode/issues/31441

## Key PR Progress

1. **#31434 / #31446 – `opencode run --format json` drain pending events**  
   Fixes race where idle event cuts off text/step‑finish events in JSONL output. Critical for CI/containerized headless use.  
   https://github.com/anomalyco/opencode/pull/31434  
   https://github.com/anomalyco/opencode/pull/31446

2. **#31447 – Ensure config directory exists before writing .gitignore**  
   Prevents crash on startup when `OPENCODE_CONFIG_DIR` points to a wiped directory.  
   https://github.com/anomalyco/opencode/pull/31447

3. **#31448 / #31438 – Fix rounded bottom corners in v2 layout**  
   UI polish: adds `overflow-hidden` and `rounded-b-[10px]` to chat panel and dock.  
   https://github.com/anomalyco/opencode/pull/31448  
   https://github.com/anomalyco/opencode/pull/31438

4. **#31329 – Graceful error handling for PDF/image read failures**  
   Stops session crashes when PDF files are corrupted or permissions are wrong. Closes #21390.  
   https://github.com/anomalyco/opencode/pull/31329

5. **#31444 – Skip spinner animation in non‑TTY environments**  
   Prevents `@clack/prompts` spinner from emitting raw ANSI garbage in CI/piped output.  
   https://github.com/anomalyco/opencode/pull/31444

6. **#31442 – Paginate MCP catalogs**  
   Follows MCP cursors when listing tools, prompts, and resources, with tolerance for repeated cursors and 1000‑page cap.  
   https://github.com/anomalyco/opencode/pull/31442

7. **#30332 – Generate reasoning variants for all OpenRouter models**  
   Fixes missing reasoning variants for non‑GPT models. Closes #30216.  
   https://github.com/anomalyco/opencode/pull/30332

8. **#30190 – Make OpenRouter prompt cache 1h TTL opt‑in**  
   Adds env‑controlled option to extend cache TTL from 5min to 1h. Addresses #16848.  
   https://github.com/anomalyco/opencode/pull/30190

9. **#31440 – Retry transient network errors**  
   Implements automatic retry for ECONNRESET, ECONNREFUSED, fetch failures instead of surfacing raw errors. Closes multiple issues.  
   https://github.com/anomalyco/opencode/pull/31440

10. **#31431 – Start desktop app without sidecar (PoC)**  
    Experimental PR to run OpenCode Desktop without the local sidecar process. Early stage.  
    https://github.com/anomalyco/opencode/pull/31431

## Feature Request Trends

- **Persistent session lifecycle** – The `/goal` command (#27167) tops the charts with 65 👍. Users want built‑in goal tracking, not just slash commands.
- **MCP Resources** – Support for `resources/read` (#15535, 16 👍) would enable richer data retrieval from third‑party MCP servers.
- **Clickable file:line references** – Both in web UI (#13430) and built‑in editor (#31406). Users want to jump directly to code locations from chat.
- **Payment options** – Crypto payment for OpenCode Go (#23153, 15 👍) and Chinese VAT invoices (#30716) reflect expanding global user base.
- **Documentation preservation during compaction** – AGENTS.md/CLAUDE.md context loss (#16960) is a recurring concern for teams using system instruction files.

## Developer Pain Points

- **Database constraint errors** – Multiple issues (#31204, #31413, #31412) report `NOT NULL constraint failed: session_message.seq` after recent migrations, affecting agent switches, headless runs, and HTTP APIs.
- **Bedrock/Mantle integration instability** – Empty responses (#31430), signature mismatches (#31349), and gateway incompatibility (#30948) are blocking Bedrock users, especially those testing GPT‑5.5.
- **Gboard autocomplete duplication** – On Android/web‑based TUIs, Gboard suggestions duplicate or malform input (#31427, #31428).
- **Missing UI elements** – Navigation buttons disappearing (#31441) and regression in rounded corners (#31448) show UI polish regressions.
- **Stale plugin cache** – `@latest` pinned to old npm version (#25293) forces manual cache cleanup, frustrating plugin developers.

*Generated from GitHub data: 2026-06-09*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-09

## Today’s Highlights
Version **v0.79.0** landed with a controversial new **Project Trust** feature that gates local project files, sparking immediate community backlash in [#5514](https://github.com/earendil-works/pi/issues/5514) (14 comments). The day saw a flurry of bug fixes and enhancements: a quadratic-performance bug in large sessions was squashed, Azure OpenAI got a critical stateless-mode fix, and several quality-of-life PRs (file checkpoints, configurable clipboard storage, first-run theme detection) were merged. Overall, 20 PRs and dozens of issues were processed, reflecting a highly active development cadence.

## Releases
- **[v0.79.0](https://github.com/earendil-works/pi/releases/tag/v0.79.0)** — Introduced **Project Trust**: Pi now prompts before loading project-local settings, resources, instructions, and packages. Users can save decisions and use `--approve` / `--no-approve` flags for non‑interactive modes.  
  *Note: Release notes contain broken links (see [#5516](https://github.com/earendil-works/pi/issues/5516)).*

## Hot Issues (Top 10)

1. **#5514 — [OPEN] Project Trust Feature Feedback**  
   *Author: markg85*  
   User immediately finds the trust gating annoying — especially across multiple PCs. Requests a way to disable it. 14 comments, 4 👍.  
   [Issue](https://github.com/earendil-works/pi/issues/5514)

2. **#4180 — [CLOSED] Links not clickable anymore**  
   *Author: Thinkscape*  
   After an update that made Pi use alternate term mode, hyperlinks in the TUI became unclickable. 10 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/4180)

3. **#5464 — [CLOSED] Local models: 3‑5 minute “Working” status latency**  
   *Author: DuckTapeKiller*  
   Running Pi with local Ollama models (e.g., ministral3:8b) introduces multi-minute delays on every message. High impact for local‑first users. 6 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5464)

4. **#5363 — [OPEN] Add amazon‑bedrock‑mantle provider**  
   *Author: tasadurian*  
   Bedrock Mantle models use an OpenAI‑compatible API, distinct from the existing Converse‑based provider. 3 👍, 6 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5363)

5. **#5427 — [OPEN] OpenAI Codex transport issues**  
   *Author: cperion*  
   After a while, Codex SSE responses time out after 10s repeatedly. Seems to be a regression from v0.78.1. 4 👍, 3 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5427)

6. **#5530 — [OPEN] `azure‑openai‑responses` missing `store: false`**  
   *Author: Jaxkr*  
   Unlike the other OpenAI‑compatible providers, Azure OpenAI runs in stateful mode, causing reasoning objects to be dropped server‑side. 2 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5530)

7. **#5492 — [CLOSED] High CPU in interactive TUI on large sessions**  
   *Author: somjik-api*  
   Quadratic session‑branch traversal (62k nodes) caused ~100% CPU while idle. Already fixed in PR #5493. 3 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5492)

8. **#5478 — [CLOSED] cwd bridge captures directory changes but never propagates**  
   *Author: vifar*  
   The `bash` tool records the effective working directory, but the value is never read back by callers — so `cd` inside bash is silently ignored by the rest of the system. 3 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5478)

9. **#5535 — [CLOSED] Repo description still mentions removed web UI**  
   *Author: rahimnathwani*  
   Trivial but notable: the GitHub repo description still lists “web UI library” even though the web UI workspace was removed in a previous commit. 2 comments.  
   [Issue](https://github.com/earendil-works/pi/issues/5535)

10. **#5433 — [OPEN] Extension OAuth login mirrors active prompt input**  
    *Author: balcsida*  
    When an extension calls `onPrompt()` multiple times during OAuth, the current prompt input gets mirrored into previous rows. UI glitch with screen‑recording evidence. 2 comments.  
    [Issue](https://github.com/earendil-works/pi/issues/5433)

## Key PR Progress (Top 10)

1. **#5537 — `beforeModel` hook and reactive compaction**  
   New optional callbacks in `AgentLoopConfig`: allows modifying context, blocking requests, and triggering compaction mid‑turn.  
   [PR](https://github.com/earendil-works/pi/pull/5537)

2. **#5524 — Fix Azure OpenAI Responses: send `store: false`**  
   Three‑line fix to make Azure OpenAI use stateless mode, preventing dropped reasoning objects.  
   [PR](https://github.com/earendil-works/pi/pull/5524)

3. **#5521 — Restore files on rewind (checkpoints)**  
   Adds “Restore files to this point?” prompt when rewinding conversation, so file edits are also rolled back.  
   [PR](https://github.com/earendil-works/pi/pull/5521)

4. **#5515 — Add `alwaysTrust` setting to bypass project trust gating**  
   Directly addresses #5514 feedback: a flag to completely disable trust gating (disabled by default).  
   [PR](https://github.com/earendil-works/pi/pull/5515)

5. **#5518 — Configurable clipboard image storage path**  
   Lets users set `images.storagePath` in `settings.json` instead of always writing to `os.tmpdir()`.  
   [PR](https://github.com/earendil-works/pi/pull/5518)

6. **#5513 — Enforce context window mid‑turn**  
   Wires auto‑compaction to stop cleanly after a tool turn exceeds the threshold, preventing runaway context growth.  
   [PR](https://github.com/earendil-works/pi/pull/5513)

7. **#5509 — Amazon Bedrock Mantle OpenAI Responses provider**  
   New provider for Bedrock Mantle’s OpenAI‑compatible API (supports GPT 5.5/5.4). Modeled after Azure provider.  
   [PR](https://github.com/earendil-works/pi/pull/5509)

8. **#5503 — MiniMax‑M3 adaptive thinking**  
   Flags MiniMax‑M3 as supporting adaptive thinking format (`thinking: { type: "adaptive" }`), identical to Claude Opus 4.6+.  
   [PR](https://github.com/earendil-works/pi/pull/5503)

9. **#5493 — Avoid quadratic session branch traversal**  
   Fixes the high‑CPU issue (#5492) by replacing O(n²) traversal with a linear algorithm. Performance improvement for large sessions.  
   [PR](https://github.com/earendil-works/pi/pull/5493)

10. **#5488 — Word‑wrap option labels and descriptions**  
    Replaces truncation with proper word‑wrap in the TUI, preserving all content and ANSI styling.  
    [PR](https://github.com/earendil-works/pi/pull/5488)

## Feature Request Trends

- **Trust gating customisation** — The new Project Trust feature is divisive; users want a simple `alwaysTrust` flag or per‑machine persistence (see #5514, PR #5515).
- **More LLM providers** — Strong demand for Amazon Bedrock Mantle (#5363, PR #5509), Azure Cognitive Services (PR #3799), and generic OpenAI‑compatible endpoints.
- **File checkpoints / rewind restore** — Users want `Esc Esc` to also roll back file edits, not just conversation history (#5522, PR #5521).
- **Configurable storage** — Clipboard images should be stored in a user‑defined directory instead of the temporary directory (#5520, PR #5518).
- **Terminal theme detection** — First‑run experience should automatically match the terminal’s light/dark theme (PR #5385, still open).

## Developer Pain Points

- **Project trust prompts feel intrusive** — Even on known machines, the trust gating is perceived as friction for local work.
- **Session export failures** — Missing `template.{css,js}` in binary distributions (#5534, #5240) repeatedly blocks users.
- **Provider‑specific regressions** — OpenAI Codex timeouts (#5427), Azure stateful mode (#5530), Gemini parallel tool‑call failures (#5528) indicate fragile provider implementations.
- **Performance on large sessions** — Quadratic branch traversal (#5492) and missing mid‑turn context guards (#5512) cause high CPU and context overruns.
- **Missing bash metadata** — The `bash` tool lacks a required description field and default timeout, making audit and resource control harder (#5484).
- **Keybinding inflexibility** — The `app.message.submit` / steer action is not exposed in the keybinding system, limiting customisation (#5490).

---

*Data source: [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono) — Digest for 2026-06-09.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-09

## Today’s Highlights
A packed day of infrastructure and feature work: the v0.18.0-preview.0 release workflow failed on CI, but the team landed several high-value PRs including daemon session-idle reaping, a `enter_plan_mode` tool, and the first slice of declarative agent frontmatter. A severe OOM bug (`--resume` + Escape key) was closed after a deep investigation that also uncovered a Hook-continuation memory leak in `/goal` loops, now fixed in an open PR.

## Releases
No new versions were published in the last 24 hours. The automated release for **v0.18.0-preview.0** failed ([#4875](https://github.com/QwenLM/qwen-code/issues/4875)) – details in the CI run. All feature work described below is expected to land in the next preview.

## Hot Issues
1. **[#4815 – Severe OOM with `--resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)** – A critical memory bug causing Node heap exhaustion within 10 minutes of session restore. The Escape key becomes unresponsive. *Closed* with a root cause found (Hook-continuation compaction gap, see [#4838](#4838)).  
2. **[#4821 – Declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)** – Request to port Claude Code’s `.claude/agents/*.md` pattern: define agents via YAML frontmatter in Markdown. Strong community interest (6 comments); a PR is already open.  
3. **[#4747 – Global user-level auto-memory](https://github.com/QwenLM/qwen-code/issues/4747)** – Currently memories are per-project; users want cross-project preferences stored at `~/.qwen/memories/`. *Closed* – merged in PR [#4764](#4764).  
4. **[#4801 – Dedicated `web_search` tool](https://github.com/QwenLM/qwen-code/issues/4801)** – Qwen Code is the only major code agent CLI without a built-in web search tool. The underlying platform already supports it; community is asking for a simple passthrough.  
5. **[#4782 – ACP Streamable HTTP transport implementation status](https://github.com/QwenLM/qwen-code/issues/4782)** – Tracks the `/acp` endpoint that lets ACP-native editors (Zed, JetBrains) connect to `qwen serve` without adapters. Useful reading for anyone building external integrations.  
6. **[#4675 – Vim INSERT mode Esc leak and Enter not sending in NORMAL](https://github.com/QwenLM/qwen-code/issues/4675)** – A bundle of terminal-mode bugs: Esc key triggers app-level handlers (clear, interrupt) instead of switching modes; Enter key is ignored in NORMAL mode. *Closed* with multiple fixes merged.  
7. **[#4838 – Hook continuations skip tool-result microcompaction in long `/goal` loops](https://github.com/QwenLM/qwen-code/issues/4838)** – Discovered during the [#4815] investigation. `/goal` loops re-enter via Hook continuations that never call `microcompactHistory()`, leading to unbounded history growth. Tagged `welcome-pr`.  
8. **[#4864 – CI: enable required status checks on main branch](https://github.com/QwenLM/qwen-code/issues/4864)** – A PR with failing CI was merged into `main`, breaking `tsc --build`. The community is pushing for mandatory checks to prevent regression merges.  
9. **[#4854 – Launch process from another location to avoid self-kill](https://github.com/QwenLM/qwen-code/issues/4854)** – Users report that when the agent kills a dev server, it can kill its own parent shell. Suggests starting Qwen Code at a path separate from the project working directory.  
10. **[#4872 – Automated CHANGELOG](https://github.com/QwenLM/qwen-code/issues/4872)** – Requests a `CHANGELOG.md` synced with releases, inspired by Claude Code’s changelog. Low friction way to improve release communication.

## Key PR Progress
1. **[#4840 – Fix Hook-continuation microcompaction](https://github.com/QwenLM/qwen-code/pull/4840)** – Applies periodic tool-result microcompaction in `/goal` loops, directly addressing the OOM root cause from [#4838](#4838). *Open* – under review.  
2. **[#4853 – `enter_plan_mode` tool and Plan Approval Gate](https://github.com/QwenLM/qwen-code/pull/4853)** – The model can now self-lower into plan mode for complex tasks; `exit_plan_mode` runs a single-approval gate when in AUTO/YOLO mode. Reduces ad-hoc plan switching.  
3. **[#4871 – Remove GitService, migrate `/restore` to FileHistoryService](https://github.com/QwenLM/qwen-code/pull/4871)** – Unifies two parallel file-recovery systems (`/restore` and `/rewind`) under one backend. Cleans up ~2k lines of shadow-git code.  
4. **[#4870 – Full YAML parser for skill frontmatter](https://github.com/QwenLM/qwen-code/pull/4870)** – Fixes block scalar descriptions (`>` / `|`) that were being parsed as literal characters. Falls back to simple YAML parser on malformed input.  
5. **[#4842 – Declarative agent frontmatter v1](https://github.com/QwenLM/qwen-code/pull/4842)** – Ports `permissionMode`, `maxTurns`, and a color allowlist from Claude Code 2.1.168 – basic compatibility so CC agent files work in Qwen Code.  
6. **[#4764 – User-level auto-memory](https://github.com/QwenLM/qwen-code/pull/4764)** – Implements the global memory directory requested in [#4747](#4747). Cross-project facts about the user are stored once. *Merged*.  
7. **[#4732 – Workflow tool P1: `node:vm` sandbox + sequential `agent()`](https://github.com/QwenLM/qwen-code/pull/4732)** – First step of the Dynamic Workflows port: runs model-authored JavaScript in a sandbox with `args`, `phase`, `log`, and sequential sub-agent calls. *Open*.  
8. **[#4833 – Session idle reaper for daemon](https://github.com/QwenLM/qwen-code/pull/4833)** – Two-layer cleanup: close-on-last-detach (immediate) + configurable idle timeout. Stops sessions from accumulating in the daemon bridge.  
9. **[#4844 – Experimental Agent Team mode](https://github.com/QwenLM/qwen-code/pull/4844)** – The model can create a named team with parallel sub-agents that share a task list and message each other. Parallel coordination proof-of-concept.  
10. **[#4850 – Multi-tab `/extensions` dialog](https://github.com/QwenLM/qwen-code/pull/4850)** – Upgrades from a linear wizard to a Discover/Installed/Marketplaces tabbed view, aligning with Claude Code's `/plugin` command.

## Feature Request Trends
- **Declarative agent configuration** – Several issues request YAML frontmatter agent files (matching Claude Code’s pattern) and the ability to define agent teams declaratively.  
- **Global/persistent memory** – Cross-project user memory is now merged; remaining asks centre on team-shared memory and integration with external databases.  
- **Web search + MCP tooling** – A dedicated `web_search` tool and better MCP-server management are the top missing capabilities compared to Claude Code.  
- **Daemon & external integrations** – The ACP transport is live; follow-ups focus on session lifecycle, replay correctness, and documentation for editor integration.  
- **Multi-agent execution** – Dynamic Workflows (P1 merged) and Agent Team (experimental) are both in progress, with community demand for background fork agents and `/swarm` improvements.

## Developer Pain Points
- **Out-of-memory crashes** – Two separate bugs (`--resume` heap exhaustion and `/goal` history bloat) caused users to hit Node’s 4 GB limit. Both are now addressed.  
- **CI/release reliability** – A PR with failing checks was merged, and the v0.18.0-preview release failed. The community is calling for mandatory CI gates and automated changelogs.  
- **Keybinding conflicts** – Vim mode has recurring issues with Esc leaking to app handlers, the Escape clear/interrupt interactions, and cursor movement at wrapped lines.  
- **Configuration path inconsistency** – Several features (auto-memory, runtime output) hardcode `~/.qwen/` and ignore `runtimeOutputDir` / `QWEN_RUNTIME_DIR`, causing surprises in custom setups.  
- **File ownership in shared environments** – Atomic file writes using `rename` reset ownership in Docker/shared workspaces, requiring a post-release mitigation.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，作为一名专注于AI开发者工具的技术分析师，以下是根据您提供的GitHub数据生成的DeepSeek TUI（现已更名为CodeWhale）社区摘要。

---

### DeepSeek TUI (CodeWhale) 社区摘要 — 2026-06-09

**注意：** 项目现已正式更名为 **CodeWhale**，并已在 `v0.8.54` 版本中生效。旧的 `deepseek-tui` 软件包已弃用。以下所有内容均针对 `Hmbown/CodeWhale` 仓库。

---

### 1. 今日亮点

项目完成了品牌重塑，`v0.8.54` 作为 **CodeWhale** 的首个版本发布，所有开发者都需要注意从 `deepseek-tui` 迁移到 `codewhale-cli` 和 `codewhale-tui`。同时，`v0.8.55` 版本的发布冲刺正在进行中，重点在于增加两个重量级新供应商支持（Together AI和OpenAI Codex/ChatGPT），以及大量的模型目录更新和社区贡献的整合。此外，社区围绕基准测试框架、TUI国际化（i18n）和声明式工作流编排提出了多个高质量的PR，显示出项目生态的活跃度。

### 2. 发布

- **[v0.8.54](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.54) — CodeWhale 品牌重塑首个版本**
  - **核心变更**：项目名称从 `DeepSeek TUI` 正式更名为 **CodeWhale**，对应的CLI和UI包均已变更。
  - **主要亮点**：
    - **基准测试集成**：引入了 `SWE-bench`、`Terminal-Bench` 和 `PinchBench` 的测试自动化框架，并内置了LLM评分评估功能。
    - **Whaleflow 基础**：为即将到来的声明式多智能体工作流编排（WhaleFlow）奠定了基础。
    - **其他**：集成了 Paulo 的测试框架，并优化了 MiMo 基准测试路由。
  - **迁移须知**：用户必须通过 `cargo install codewhale-cli codewhale-tui --locked` 进行全新安装。

- **[v0.8.55 (PR #2916)](https://github.com/Hmbown/CodeWhale/pull/2916) — 正在制作中**
  - 计划发布两个新供应商：**Together AI** 和 **OpenAI Codex (ChatGPT OAuth)**。
  - 将新增多个模型到目录中，包括 Qwen 3.7 Max、MiniMax 2.7、NVIDIA Nemotron 3 Ultra 等。

### 3. 热门问题 (Top 10 分析)

本周问题列表显著增长，反映了品牌重塑和功能扩展期的阵痛。以下是10个值得关注的问题：

1.  **[#2490](https://github.com/Hmbown/CodeWhale/issues/2490) 不能编译UE工程**：用户报告工具无法编译Unreal Engine项目，且未提供更多文字描述。这对游戏开发者是严重的阻断问题，目前尚未有官方回复。

2.  **[#1327](https://github.com/Hmbown/CodeWhale/issues/1327) FreeBSD x86_64: Turn dispatch timed out**：一个持续多日的FreeBSD支持问题。用户通过OpenRouter使用DeepSeek模型时，每次都能稳定复现引擎超时。这暴露了在非主流操作系统上的兼容性风险。

3.  **[#2641](https://github.com/Hmbown/CodeWhale/issues/2641) issue_pdf_bug**：`read_file` 工具在读取PDF文件且未指定 `pages` 参数时会导致 `channel closed` 错误。这是一个明确的工具使用缺陷，影响用户处理文档的体验。指定 `pages` 则正常，说明问题出在默认逻辑上。

4.  **[#2596](https://github.com/Hmbown/CodeWhale/issues/2596) TUI /model Picker 不显示其他供应商的自定义模型**：用户在其他供应商（如Moonshot）下配置的自定义模型，不会显示在当前供应商（如DeepSeek）的模型选择器中。这是一个常见的UX痛点，迫使需要手动输入模型名称。

5.  **[#2893](https://github.com/Hmbown/CodeWhale/issues/2893) siliconflow provider config error**：用户报告`siliconflow-CN`和`siliconflow`两个配置段无法独立工作，必须同时配置。这是一个不合理的配置行为，很可能是一个验证逻辑的Bug。

6.  **[#2917](https://github.com/Hmbown/CodeWhale/issues/2917) Cargo distribution: error: failed to spawn `codewhale`**：从旧版 `deepseek-tui` 升级到新版 `codewhale` 后无法启动程序。这是一个严重的迁移事故，显示自动更新路径未正确处理二进制名称变更。

7.  **[#2914](https://github.com/Hmbown/CodeWhale/issues/2914) TUI: fix large-paste .deepseek writes and long status readability**：一个标记为 `release-blocker` 的问题，指出TUI在处理长时间运行任务和大量粘贴时，底部状态栏和提示信息难以辨认，影响基本可用性。

8.  **[#2904](https://github.com/Hmbown/CodeWhale/issues/2904) Feature request: Persistent agent state and KV cache capsules**：一个极具前瞻性的功能请求，提议为长时间运行的编码任务实现持久化的智能体状态，未来甚至支持签名的压缩KV缓存。社区对该想法的反响较为积极。

9.  **[#2900](https://github.com/Hmbown/CodeWhale/issues/2900) DSML调用错误**：用户反馈模型将DSML（可能是领域特定标记语言）调用当作普通文本输出，导致上下文被非结构化文本严重占用。这是一个影响Agent可靠性的核心Bug。

10. **[#2906 - #2912](https://github.com/Hmbown/CodeWhale/issues?q=is%3Aissue+is%3Aopen+label%3Amodel-lab)** 模型目录系列问题：这一系列问题（Together AI、Qwen 3.7 Max、Nemotron 3 Ultra等）表明官方正在大规模扩张模型支持矩阵，但不同模型的兼容性和路由细节仍有待验证。这是当前社区关注的焦点。

### 4. 关键PR进展 (Top 10 分析)

本周PR活动非常活跃，涵盖了Bug修复、新特性、国际化以及底层架构改进。

1.  **[#2920](https://github.com/Hmbown/CodeWhale/pull/2920) fix(tui): write oversized paste files to .codewhale/pastes/**：修复了品牌重塑后，大型粘贴文件仍写入旧的 `.deepseek/pastes/` 目录的遗留问题。对迁移体验至关重要。

2.  **[#2919](https://github.com/Hmbown/CodeWhale/pull/2919) / [#2918](https://github.com/Hmbown/CodeWhale/pull/2918) feat(i18n): localize ConfigEdit/ConfigSection labels**：社区贡献者 `gordonlu` 持续推动国际化工作，这次本地化了配置编辑和配置区块的标签（共22个消息ID）。显著增强了非英语用户的体验。

3.  **[#2916](https://github.com/Hmbown/CodeWhale/pull/2916) v0.8.55 — Together AI provider + experimental OpenAI Codex (ChatGPT) provider**：维护者 `Hmbown` 正在推进的新供应商集成PR，连接了多个模型目录更新，是下一版本的核心。

4.  **[#2903](https://github.com/Hmbown/CodeWhale/pull/2903) feat: build static linux x64 binaries with musl**：贡献者 `wavezhang` 实现了使用 musl 编译静态Linux二进制文件，消除了对 `glibc` 等动态库的依赖。对容器化部署和Linux用户非常友好。

5.  **[#2482](https://github.com/Hmbown/CodeWhale/pull/2482) feat: add WhaleFlow — declarative multi-agent workflow orchestration**：一个大型新特性PR，引入了声明式的JSON配置驱动多智能体工作流编排（WhaleFlow），包括DAG调度和文件范围控制。虽已关闭，但已为基础架构做出贡献。

6.  **[#2884](https://github.com/Hmbown/CodeWhale/pull/2884), [#2883](https://github.com/Hmbown/CodeWhale/pull/2883), [#2881](https://github.com/Hmbown/CodeWhale/pull/2882)** 一系列Bug修复PR：贡献者 `HUQIANTAO` 修复了客户端连接池、Mutex死锁、并发线程耗尽以及错误处理静默失败等17个Bug，显著提升了应用的健壮性。

7.  **[#2869](https://github.com/Hmbown/CodeWhale/pull/2869) fix(tui): list saved models from all providers in /model picker**：社区贡献者 `ousamabenyounes` 提交了针对Issue #2596的修复，让模型选择器能展示所有供应商保存的自定义模型。

8.  **[#2753](https://github.com/Hmbown/CodeWhale/pull/2753) feat(tui): multi-tab system with cross-tab collaboration**：一个雄心勃勃的PR，引入了多标签页系统，并支持跨标签页的任务委派。因其复杂性，社区讨论热度较高，有的担心其稳定性。

9.  **[#2901](https://github.com/Hmbown/CodeWhale/pull/2901) / [#2899](https://github.com/Hmbown/CodeWhale/pull/2899) feat(i18n)**：`gordonlu` 继续推进国际化，本地化了工具族词汇和子代理（SubAgents）模态框的界面文本（共29个消息ID）。

10. **[#2777](https://github.com/Hmbown/CodeWhale/pull/2777) feat(config): add provider fallback chain data model**：社区贡献者 `idling11` 实现了供应商故障切换链的配置数据模型，为未来实现自动切换提供商提供了基础。

### 5. 功能请求趋势

当前社区最强烈的功能请求趋势可以归纳为以下几点：

1.  **模型目录与供应商扩展**：这是最大的增长点。社区强烈要求支持更多模型（如 Qwen 3.7 Max, MiniMax 2.7, Nemotron 3 Ultra）和更多供应商（如 Together AI, OpenAI Codex)。这是一个“越多越好”的通用需求。
2.  **国际化 (i18n)**：社区贡献者正在系统性地对各个界面进行本地化。这显示项目正在从单语种工具向国际化开发者工具转变。
3.  **多标签页与工作流增强**：用户不满足于单一的对话线程，希望通过多标签页管理不同任务，并通过声明式工作流（如WhaleFlow）编排复杂的多智能体任务。
4.  **持久化状态与上下文管理**：用户希望编码会话的上下文（尤其是长会话的KV Cache）能被持久化或导出，以实现低成本恢复和更高效的Agent操作。

### 6. 开发者痛点

从问题追踪和反馈中可以提炼出高频出现的痛点：

1.  **版本迁移阵痛**：从 `deepseek-tui` 到 `codewhale` 的迁移过程充满挑战，包括启动失败、路径错误和软件包重命名。官方文档和升级路径需要更清晰的说明。
2.  **供应商配置不一致**：不同供应商的配置逻辑（如 `siliconflow`）不一致且难以排查。用户期望一个统一、可预测的配置体验。
3.  **PDF处理问题**：`read_file` 工具处理PDF文件时默认行为有严重Bug，导致工具挂起和上下文溢出。这说明对非代码文件的处理仍需打磨。
4.  **DSML格式不稳定**：Agent将结构化标记语言作为普通文本输出，是影响Agent任务可靠性的致命缺陷，尤其是在模型切换或高负载时。
5.  **性能和稳定性**：在FreeBSD等非主流系统上以及长时间运行的任务中，出现超时、引擎停止、并发崩溃等问题。工具在边缘情况下的健壮性有待验证。

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*