# AI CLI Tools Community Digest 2026-07-26

> Generated: 2026-07-26 02:03 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem

**Date:** 2026-07-26 | **Scope:** 7 major tools analyzed

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing a maturation phase characterized by standardization debates, platform reliability challenges, and growing demand for multi-agent interoperability. Claude Code dominates in raw community engagement (4,451 upvotes on a single `AGENTS.md` issue), while OpenAI Codex leads in engineering velocity with 10 closed PRs in 24 hours. A clear pattern emerges: all tools are grappling with session state persistence failures, context compaction reliability, and cross-platform stability—particularly on Windows. The ecosystem is bifurcating between vendor-specific configuration formats (`CLAUDE.md`) and emerging cross-agent standards (`AGENTS.md`), with Kimi Code and Pi already adopting the latter. Meanwhile, the rise of sub-agent orchestration, MCP server integration, and workflow automation signals a shift from simple chat interfaces to agentic development platforms.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Key PRs (24h) | Release Status | Notable Metric |
|------|-----------------|---------------|----------------|----------------|
| **Claude Code** | 10 (4,451 👍 peak) | 5 active | No release | #6235: 4,451 upvotes (cross-agent standard) |
| **OpenAI Codex** | 10 | 10 closed | `rust-v0.146.0-alpha.10` | #10450: 690 👍 (remote dev, now closed) |
| **Gemini CLI** | 10 (P1 bugs) | 10 landed | `v0.54.0-nightly` | #22323: subagent false success (P1) |
| **GitHub Copilot CLI** | 10 | 2 (spam/closed) | No release | #4251: OOM regression in 1.0.74 |
| **Kimi Code CLI** | 2 | 4 merged | No release | 3 critical bug fixes merged overnight |
| **OpenCode** | 10 | 10 (5 open, 5 closed) | No release | #37012: 31 👍 for legacy layout retention |
| **Pi** | 10 | 10 (7 closed) | **v0.82.1** (today) | Opus 5 support shipped today |
| **Qwen Code** | 10 | 10 (1 closed, 9 open) | `v0.21.0-nightly` | 9 open features in active development |
| **DeepSeek TUI** | 10 | 10 active | No release | v0.9.2 sprint in progress |

**Key observations:**
- **Codex** has the highest PR throughput (10 closed in 24h), all by bot/copyberry.
- **Pi** is the only tool with a feature release today (v0.82.1, Opus 5 support).
- **Claude Code** has the highest community engagement by a wide margin (single issue at 4,451 👍).
- **DeepSeek TUI** has the most active nascent development (10 PRs, v0.9.2 sprint).

---

## 3. Shared Feature Directions

### Cross-Agent Standardization (Claude Code, Kimi Code)
- **Claude Code #6235** (4,451👍): Move from `CLAUDE.md` to `AGENTS.md` for interoperability
- **Kimi Code #2519** (merged): Already supports `AGENTS.md` changes on session resume
- **Pi**: Scanning for `AGENTS.md` in resource loader (PR #7106)
- **Conclusion**: The ecosystem is coalescing around `AGENTS.md` as the de facto standard; Claude Code's vendor lock-in is increasingly untenable.

### Session State Persistence (All tools)
- **Claude Code**: #76844/#80871 — task IDs reset on `--resume`; #77554 — orphaned sub-agent tasks
- **Codex**: #29356 — context compaction loses operational steps; #30408 — MCP process leaks
- **Copilot CLI**: #4251 — OOM on session resume; #4183 — CAPI 5MB limit
- **Kimi Code**: #2520/#2519/#2518 — three fixes for context truncation, stale prompts, file re-upload
- **OpenCode**: #38901 — defer auto-compaction to next model input
- **Pi**: #7020 — hangs after compaction; #6768 — compaction fails with Copilot Enterprise
- **DeepSeek TUI**: #4831 — test suite writes to real config (state isolation failure)

### Context Compaction & Token Management (All except DeepSeek TUI)
- Multiple tools report compaction as disruptive, lossy, or broken. **Codex** wants last 5 steps preserved verbatim (#29356). **OpenCode** defers compaction scheduling (PR #38901). **Pi** has compaction state machine bugs (#7020).

### MCP Server Integration (Codex, Gemini CLI, Qwen Code, DeepSeek TUI)
- **Codex**: #30408 — MCP process leaks unbounded memory
- **Gemini CLI**: #28481 — MCP OAuth token refresh with stored client ID
- **Qwen Code**: #7697 — Unity MCP fails in Qwen but works in Claude Code
- **DeepSeek TUI**: #4756 — don't retry failed qualified MCP calls

### Platform Stability (Windows focus: Codex, Copilot CLI, OpenCode, Pi)
- **Codex**: GPU crashes (#34133), conhost storms (#33776)
- **Copilot CLI**: No Windows-specific issues today
- **OpenCode**: ripgrep not bundled on Windows (#34442)
- **Pi**: WSL path handling broken (#7064)

---

## 4. Differentiation Analysis

### Feature Focus & Technical Approach

| Tool | Differentiator | Target User | Technical Philosophy |
|------|---------------|-------------|---------------------|
| **Claude Code** | Anthropic ecosystem lock-in; deepest reasoning model (Opus 5) | Power users needing complex reasoning | Model-centric; system prompt injection (controversial `heron_brook`) |
| **Codex** | VS Code integration; highest PR velocity | Enterprise/VS Code users | Engineering rigor; bot-driven automation |
| **Gemini CLI** | MCP-first; robust eval infrastructure | Google ecosystem developers | Systematic; component-level eval (#24353) |
| **Copilot CLI** | GitHub integration; lightweight | GitHub-centric developers | Minimalist; slower iteration (2 PRs today) |
| **Kimi Code** | AGENTS.md-native; rapid bug fixing | Cross-platform users | Pragmatic; fix-first approach (3 merged fixes today) |
| **OpenCode** | TUI-focused; plugin ecosystem | Terminal power users | Community-driven; feature-rich (dynamic workflows) |
| **Pi** | Compact, extensible (extensions API) | Developers wanting minimal tool | Modular; extension-first architecture |
| **Qwen Code** | Sandbox & subagent orchestration | Qwen model users | Research-forward; sandbox probing, model grade selection |
| **DeepSeek TUI** | Rust-based; polyglot localization | DeepSeek model users | Polyglot; 8 TUI languages, CI-gated locale drift |

### Key Tensions

1. **Vendor lock-in vs. open standards**: Claude Code pushes `CLAUDE.md`; Kimi Code and Pi already adopt `AGENTS.md`. The market is voting with issues.
2. **Feature velocity vs. stability**: Codex ships 10 PRs/day but has Windows stability issues. Pi ships a release today but TUI performance is degraded.
3. **Model ecosystem lock-in**: Gemini CLI ties to Google; Qwen Code to Qwen models; DeepSeek TUI to DeepSeek. Cross-provider parity is a growing pain point (#4829 in DeepSeek).
4. **Desktop vs. TUI vs. CLI-only**: OpenCode and DeepSeek TUI invest in rich TUI; Codex doubles down on VS Code integration; Copilot CLI stays minimal.

---

## 5. Community Momentum & Maturity

### Active Communities (High engagement, growth trajectory)

| Tool | Community Signal | Maturity Level |
|------|-----------------|----------------|
| **Claude Code** | #6235 at 4,451👍 (single largest issue across all tools) | **Mature, polarized** — large community but deep frustrations |
| **Codex** | #10450 at 690👍 (remote dev, now closed) | **Mature, high velocity** — enterprise adoption, bot-driven |
| **OpenCode** | #37012 at 31👍, 33 comments (UI debate) | **Growth phase** — strong community voice, feature-rich |
| **Gemini CLI** | Multiple P1 bugs with sustained discussion | **Systematic maturity** — focusing on eval infrastructure |

### Rapidly Iterating (Fewer users but high development velocity)

| Tool | Velocity Signal |
|------|----------------|
| **DeepSeek TUI** | 10 active PRs, v0.9.2 sprint in progress (smallest user base but highest relative activity) |
| **Qwen Code** | 10 PRs, 9 open; sandbox probing, subagent model grades (research-heavy trajectory) |

### Slow / Stabilizing

| Tool | Signal |
|------|--------|
| **Copilot CLI** | 2 PRs (both non-functional/spam); 10 open bugs with low community engagement (0-14👍) |
| **Kimi Code** | Small issue volume (2 bugs); 3 merged fixes suggest maintenance mode |

### Maturity Assessment
The ecosystem is **pre-mature** in terms of reliability but **mature** in community expectations. Users are demanding production-grade stability (session persistence, compaction, cross-platform support) while vendors are still shipping alpha-quality features. The most mature aspect is the **evaluation infrastructure** (Gemini CLI component-level eval, Codex test automation), while the least mature is **cross-agent standardization** (still debating `AGENTS.md` vs proprietary formats).

---

## 6. Trend Signals

### 1. Standardization Pressure Is Building
The 4,451-upvote `AGENTS.md` issue in Claude Code signals that **vendor lock-in is becoming a liability**. Kimi Code already supports it; Pi scans for it. Developers want to use multiple agents on the same codebase without maintaining 3+ config files. **Action**: If your team evaluates AI CLI tools, prioritize those that support cross-agent standards—or at minimum have plans to adopt them.

### 2. Session Durability Is the #1 Developer Pain Point
Across all 7 tools, the most common complaint is **state loss across session boundaries**: orphaned sub-agents, lost task IDs, broken compaction, OOM on resume, stale system prompts. This is the single largest blocker for production use. **Action**: For long-running orchestration workflows (CI/CD, multi-day reviews), expect to work around session limitations. Tools with explicit session management (Pi's extension context-clear API, OpenCode's deferred compaction) are ahead.

### 3. Windows Support Remains an Afterthought
Multiple GPU crashes (`vk_swiftshader.dll` failures, Chrome GPU exit codes), PowerShell spawning storms, WSL path handling bugs, and offline installer breakage. Windows users are underserved across the board. **Action**: If your team is Windows-dominant, budget for extra friction. Codex and Pi have the most Windows-specific fixes in progress.

### 4. Agent Transparency Is Non-Negotiable
The `heron_brook` prompt-injection incident (#80988, Claude Code) crystallized a broader concern: users demand to know **why** their agent behaves differently between versions. Opus 4.8/Fable 5 regressions, silent thinking-mode failures, and invisible configuration overrides are eroding trust. **Action**: Demand per-model changelogs, model version pinning, and clear reasoning for model behavior shifts. Tools that provide this (Gemini CLI's eval infrastructure, Qwen Code's logging) will build trust faster.

### 5. MCP (Model Context Protocol) Is Becoming Infrastructure
MCP server process leaks, OAuth refresh bugs, and sandbox integration issues appear in 4 of 9 tools. The protocol is becoming critical infrastructure but remains fragile. **Action**: Standardize on MCP for tool integration but expect growing pains. Test MCP server lifecycle thoroughly (process cleanup, token refresh, sandbox compatibility).

### 6. Performance Optimization Is the Next Frontier
Lazy-loading (Qwen Code #7686), TUI CPU pinning (Pi #6665), allocation loops (OpenCode #36677), and memory regressions (Copilot CLI #4251) show that **initial implementation is done; optimization is the next wave**. **Action**: For resource-constrained environments (laptops, VMs), benchmark tools on startup time and memory footprint before committing. Qwen Code's lazy-loading and Pi's TUI perf fixes are signs of this focus.

### 7. Specialization Is Increasing
- **Pi**: Extensible via extensions (context-clear API, callback-driven)
- **Qwen Code**: Sandbox runtime probing, model-grade selection for sub-agents
- **DeepSeek TUI**: Polyglot localization (6+ languages), workflow runtime
- **OpenCode**: Dynamic workflows (matching Claude Code's `/workflow`)
- **Gemini CLI**: Robust evaluation harnesses (component-level evals, behavioral evals)

**Action**: Choose a tool that aligns with your team's specialization needs—not just model quality but extensibility, evaluation, and localization.

---

## Summary for Decision-Makers

| If your priority is... | Consider... | Because... |
|------------------------|-------------|------------|
| **Best reasoning quality** | Claude Code (Opus 5) | But accept vendor lock-in, prompt injection risks |
| **VS Code integration** | OpenAI Codex | Highest engineering velocity, but Windows issues |
| **Cross-provider flexibility** | Kimi Code or Pi | Both adopt AGENTS.md, multiple provider support |
| **Extensibility / plugins** | OpenCode or Pi | Plugin ecosystems, dynamic workflows, extension APIs |
| **MacOS/Headless workflow** | Pi (OpenRouter OAuth fix) or DeepSeek TUI | Headless login support, TUI-first design |
| **Long-running orchestrations** | OpenCode (deferred compaction) or Pi (context-clear API) | Better session state management |
| **Container/sandbox workflows** | Qwen Code | Sandbox runtime probing, subagent model grades |
| **GCP/Google ecosystem** | Gemini CLI | Eval infrastructure, MCP-first, but P1 bugs |
| **Lightweight, GitHub-centric** | Copilot CLI | Minimal, stable, but limited growth |

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data from github.com/anthropics/skills | 2026-07-26 snapshot*

---

## 1. Top Skills Ranking

The following are the most-discussed Skill proposals (by comment activity), reflecting where the community is investing attention:

### #1298 — fix(skill-creator): run_eval.py always reports 0% recall
**Status:** Open | **Author:** MartinCajiao | **[PR link](https://github.com/anthropics/skills/pull/1298)**
A critical bugfix for the skill-creator evaluation pipeline. The `run_eval.py` script—and by extension the entire description-optimization loop (`run_loop.py`, `improve_description.py`)—reports `recall=0%` for every skill description, rendering the optimizer effectively blind. This PR addresses the eval artifact installation, Windows stream reading, trigger detection logic, and parallel worker issues. **Discussion highlights:** This is the most actively commented PR, directly connected to Issue #556 (12 comments, multiple independent reproductions). The community is deeply engaged because the bug makes skill optimization impossible—any description appears equally "bad." The PR represents a systemic fix rather than a surface patch.

### #514 — Add document-typography skill
**Status:** Open | **Author:** PGTBoos | **[PR link](https://github.com/anthropics/skills/pull/514)**
A quality-control skill targeting typographic problems in AI-generated documents: orphan word wrap (1–6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment. **Discussion highlights:** The proposer argues these issues affect "every document Claude generates," positioning this as a universal fix that users rarely explicitly request. The community engagement centers on whether typographic rules should be a Skill or built into document-generation tools themselves.

### #538 — fix(pdf): correct case-sensitive file references in SKILL.md
**Status:** Open | **Author:** Lubrsy706 | **[PR link](https://github.com/anthropics/skills/pull/538)**
Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` were referenced in uppercase but the actual filenames are lowercase. **Discussion highlights:** While a simple fix, the sustained comment activity reflects broader community frustration with cross-platform compatibility—this bug breaks the PDF skill entirely on case-sensitive file systems (Linux, macOS).

### #486 — Add ODT skill
**Status:** Open | **Author:** GitHubNewbie0 | **[PR link](https://github.com/anthropics/skills/pull/486)**
A comprehensive skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods, .odf). Covers LibreOffice document production and ODT-to-HTML conversion. **Discussion highlights:** Community interest stems from the strong demand for open-source document format support. Discussion has focused on template-filling edge cases and whether the skill should integrate with existing DOCX infrastructure or remain independent.

### #210 — Improve frontend-design skill clarity and actionability
**Status:** Open | **Author:** justinwetch | **[PR link](https://github.com/anthropics/skills/pull/210)**
A substantial revision to the frontend-design skill to ensure every instruction is actionable within a single conversation, with guidance specific enough to steer behavior without over-constraining. **Discussion highlights:** This PR represents a meta-discussion about skill design philosophy—how prescriptive should Skills be? The community debate centers on balancing specificity with flexibility, and whether Skills should teach principles or enforce patterns.

### #83 — Add skill-quality-analyzer and skill-security-analyzer to marketplace
**Status:** Open | **Author:** eovidiu | **[PR link](https://github.com/anthropics/skills/pull/83)**
Two meta-skills: a comprehensive quality analysis tool evaluating Structure & Documentation (20%), Correctness & Completeness (20%), Instruction Clarity (15%), and other dimensions; and a security analyzer for community Skills. **Discussion highlights:** Significant interest in self-policing the Skills ecosystem. Discussion has touched on whether meta-Skills should be officially maintained by Anthropic, and how to prevent conflicts when a quality-analyzer evaluates itself.

### #541 — fix(docx): prevent tracked change w:id collision with existing bookmarks
**Status:** Open | **Author:** Lubrsy706 | **[PR link](https://github.com/anthropics/skills/pull/541)**
Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. In OOXML, `w:id` is a shared ID space across bookmarks, tracked changes, comments, and move ranges; hardcoded low IDs in SKILL.md examples caused collisions. **Discussion highlights:** The community has noted this as an example of why Skill examples must be production-hardened—simple demo code can silently corrupt user documents.

### #539 — fix(skill-creator): warn on unquoted description with YAML special characters
**Status:** Open | **Author:** Lubrsy706 | **[PR link](https://github.com/anthropics/skills/pull/539)**
Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing `:`, preventing silent YAML parsing failures where descriptions are truncated or split into multiple keys. **Discussion highlights:** This PR has attracted cross-references from multiple other issues, as YAML parsing bugs cascade into the 0% recall problem. The community sees this as a foundational fix that should be merged before any other skill-creator improvements.

---

## 2. Community Demand Trends

Analysis of the most-commented Issues reveals several concentrated demand directions:

| Demand Theme | Key Issue(s) | Signal |
|---|---|---|
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (43 comments) | The top issue overall. Community Skills distributed under `anthropic/` namespace create trust-boundary abuse vulnerabilities. Users want clear official vs. community labeling, permission scoping, and audit trails. |
| **Org-Wide Skill Sharing** | [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 8 👍) | Currently users must manually download `.skill` files and share via Slack/Teams. Demand for a shared skill library or direct sharing links within organizations is the most-upvoted feature request. |
| **Skill-Creator Pipeline Reliability** | [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169), [#1061](https://github.com/anthropics/skills/issues/1061) | Systematic bugs (0% recall, Windows incompatibility, YAML misparsing) are blocking skill development. The community is asking for a stable, cross-platform evaluation loop more than any new Skill. |
| **Agent Governance & Safety** | [#412](https://github.com/anthropics/skills/issues/412), [#1385](https://github.com/anthropics/skills/issues/1385) | Growing interest in safety patterns for AI agent systems: policy enforcement, threat detection, trust scoring, audit trails, and reasoning quality gates. |
| **Deduplication & Namespace Hygiene** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 9 👍) | `document-skills` and `example-skills` plugins install identical content, causing duplicates. The community wants clear boundaries between skill bundles. |

**Key insight:** Demand is bimodal—half the community wants *infrastructure* (reliable skill creation, secure distribution, organizational sharing), while the other half wants *specialized domain skills* (typography, ODT, Pyxel, compact-memory notation, color expertise).

---

## 3. High-Potential Pending Skills

These open PRs have sustained comment activity and represent Skills likely to land in the near term:

- **[#1367 — feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate (v1.3.0)](https://github.com/anthropics/skills/pull/1367)** — A skill that audits AI output before delivery: mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Universal across projects and tech stacks. Recently updated (2026-07-02).

- **[#1302 — Add color-expert skill](https://github.com/anthropics/skills/pull/1302)** — Self-contained color expertise for any task involving color knowledge: naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912), color spaces with "what to use when" guidance (OKLCH for scales, OKLAB for gradients, CAM16 for perception). Updated 2026-07-21, suggesting active iteration.

- **[#723 — feat: add testing-patterns skill](https://github.com/anthropics/skills/pull/723)** — Comprehensive testing coverage from philosophy (Testing Trophy model) through unit testing (AAA pattern, naming conventions), React component testing (Testing Library), integration, E2E, and visual regression. Still open with ongoing discussion.

- **[#525 — Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525)** — Integrates with pyxel-mcp (an MCP server for the Pyxel retro game engine). Covers a write→run_and_capture→inspect→iterate workflow for pixel-art/8-bit games. Long-lived PR (since March) but recently updated July 15.

- **[#1099 / #1050 — Windows compatibility fixes for skill-creator](https://github.com/anthropics/skills/pull/1099)** — Two PRs addressing the same root issue: `run_eval.py` is unusable on Windows (subprocess PATHEXT, cp1252 encoding, select on pipes). These are prerequisites for any Windows developer to participate in skill creation.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is not for any single new Skill, but for a reliable, cross-platform, security-aware skill creation and distribution pipeline—the ecosystem's "plumbing" must be fixed before users trust building on top of it.**

---

# Claude Code Community Digest — 2026-07-26

## Today's Highlights

A major standardization debate is simmering: **Issue #6235** calling for `AGENTS.md` support has exploded to **4,451 upvotes and 344 comments** as developers push for cross-agent codebase documentation, challenging Claude Code's `CLAUDE.md` exclusivity. Meanwhile, **Opus 4.8 / Fable 5 model-behavior regressions** dominate the bug tracker with six new reports today alone, including the `heron_brook` prompt-injection override (#80988) and silent thinking-mode failures (#79798). The community is also increasingly frustrated by **session-resume state loss** for task lists, background workflows, and sub-agent contexts.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 most noteworthy)

### 1. [🔝 #6235] Feature Request: Support AGENTS.md
- **Why it matters:** The single most-upvoted issue in this digest (4,451 👍). Competitors like Codex, Amp, and Cursor are standardizing around `AGENTS.md` for cross-agent codebase understanding. `CLAUDE.md` is seen as too Anthropic-specific, locking users into the Claude ecosystem.
- **Community reaction:** Heated debate. Supporters want multi-agent collaboration; critics worry about fragmentation. 344 comments indicate strong polarization.
- **Link:** [Issue #6235](https://github.com/anthropics/claude-code/issues/6235)

### 2. [🚨 #68429] Unauthorized Pro→Max upgrade led to permanent account+data deletion; refund stuck in Fin loop
- **Why it matters:** A critical billing and data-loss bug with no human escalation path. User reports permanent account deletion triggered by an unintended upgrade. Likely a legal/compliance escalation risk.
- **Community reaction:** Low comment count (12), but severity is extreme. Zero upvotes suggests limited visibility — possibly a niche configuration issue.
- **Link:** [Issue #68429](https://github.com/anthropics/claude-code/issues/68429)

### 3. [🐛 #79798] `alwaysThinkingEnabled` not translated to `thinking:{type:"adaptive"}` on Opus 4.8
- **Why it matters:** Users who enable extended thinking in settings get silent no-thinking sessions. 400 errors on `xhigh` effort with WebSearch. Configuration mismatch between settings.json and actual API payload.
- **Community reaction:** 7 comments, moderate engagement. Affects power users relying on deep reasoning.
- **Link:** [Issue #79798](https://github.com/anthropics/claude-code/issues/79798)

### 4. [🧠 #18027] Native context visibility for self-regulating multi-context workflows
- **Why it matters:** Claude Code lacks awareness of its own context saturation across multiple working contexts. Developers want the agent to automatically adjust strategy (split tasks, summarise, checkpoint) when approaching context limits.
- **Community reaction:** 11 comments, 8 👍. Modest but consistent interest from advanced multi-context users.
- **Link:** [Issue #18027](https://github.com/anthropics/claude-code/issues/18027)

### 5. [⚠️ #80988] `heron_brook` prompt section silently overrides user delegation policy on Opus 5
- **Why it matters:** A hard-coded system prompt section (`heron_brook`) injects "Do not call the AgentTool unless the user requested it" for Opus 5 only, overriding user-configured delegation preferences with no opt-out. This breaks workflows that rely on autonomous sub-agent delegation.
- **Community reaction:** 3 comments, concern about opaque prompt engineering. No Anthropic response visible.
- **Link:** [Issue #80988](https://github.com/anthropics/claude-code/issues/80988)

### 6. [🐛 #77554] Background tasks started by sub-agents become permanently orphaned
- **Why it matters:** A core agentic workflow bug. Sub-agents that spawn background tasks (bash `run_in_background: true`, nested agents) lose references to those tasks when the sub-agent's turn ends. Long-running orchestrations silently fail.
- **Community reaction:** 3 comments, but technical severity is high. Version 2.1.208.
- **Link:** [Issue #77554](https://github.com/anthropics/claude-code/issues/77554)

### 7. [🔄 #76844 / #80871] Task lists and task IDs do not survive session resume
- **Why it matters:** Two independent reports (same underlying bug). `TaskCreate`/`TaskUpdate` IDs are reset on `--resume`, rendering ongoing task tracking useless. Status updates queued for end-of-work progress reports are silently lost.
- **Community reaction:** 2-3 comments each. Low noise but high impact for multi-session workflows.
- **Links:** [Issue #76844](https://github.com/anthropics/claude-code/issues/76844) / [Issue #80871](https://github.com/anthropics/claude-code/issues/80871)

### 8. [💥 #77768 / #81275] Desktop GPU-process crashes on Windows (Chrome GPU process exit code 101457950)
- **Why it matters:** Two reports of identical crash pattern — opening the in-app Browser pane triggers a GPU process crash (exit code `0x60C201E`) that kills the entire app. No recovery, no crash dump. Timing suggests a recent Chromium integration regression.
- **Community reaction:** 2-3 comments each. Affects both Intel and NVIDIA hardware plus WARP software rendering — not GPU-specific.
- **Links:** [Issue #77768](https://github.com/anthropics/claude-code/issues/77768) / [Issue #81275](https://github.com/anthropics/claude-code/issues/81275)

### 9. [🐌 #78313] Sub-agents hang on first tool call (Linux VM, Opus 4.8)
- **Why it matters:** Intermittent hang that leaves parent agents waiting forever. No error message, zero tool uses. Reproducible on Hyper-V Linux VMs with no clear trigger. Suggests a race condition or resource contention in agent dispatch.
- **Community reaction:** 2 comments, likely under-reported due to intermittent nature.
- **Link:** [Issue #78313](https://github.com/anthropics/claude-code/issues/78313)

### 10. [🔬 #81178] Fable 5 self-review blind spot in long agentic sessions
- **Why it matters:** A detailed model-behavior report from a real OSS contribution (parsedmarc PR #839). Fable 5 failed to self-correct when its own generated code introduced subtle bugs during multi-agent delegation. User provides a concrete mitigation suggestion (structured self-review passes).
- **Community reaction:** 2 comments, but the report is well-researched and actionable.
- **Link:** [Issue #81178](https://github.com/anthropics/claude-code/issues/81178)

---

## Key PR Progress (5 tracked)

### [🟢 #81262] Log closed issues as closure events in Statsig
- **What it does:** Fixes a telemetry bug where closing an issue emitted a duplicate `github_issue_created` event instead of a `github_issue_closed` event.
- **Status:** Open, created yesterday.
- **Link:** [PR #81262](https://github.com/anthropics/claude-code/pull/81262)

### [🟢 #81261] Handle worktree paths with spaces in `/clean_gone`
- **What it does:** Fixes a path-parsing bug in the `/clean_gone` command that failed on Git worktrees with spaces. Switches to `git worktree list --porcelain -z` for reliable parsing.
- **Status:** Open, created yesterday.
- **Link:** [PR #81261](https://github.com/anthropics/claude-code/pull/81261)

### [🟢 #39043] Remove "retro-futuristic" recommendation from Frontend Design Skill
- **What it does:** Simple cleanup — removes an outdated aesthetic recommendation from the Frontend Design prompt skill. Author: t3dotgg (notable community figure).
- **Status:** Open (since March 2026 — languishing).
- **Link:** [PR #39043](https://github.com/anthropics/claude-code/pull/39043)

### [✅ #15727] Fix Python import paths in hookify plugin
- **What it does:** Fixes `No module named 'hookify'` error by correcting relative import paths. The `CLAUDE_PLUGIN_ROOT` path layout didn't match the import expectations.
- **Status:** Closed (merged recently). Low risk, targeted fix.
- **Link:** [PR #15727](https://github.com/anthropics/claude-code/pull/15727)

### [✅ #49596] Extract shared GitHub API client into `github-api.ts` with tests
- **What it does:** Refactors duplicated GitHub API client logic into a shared module with test coverage. Clean engineering improvement.
- **Status:** Closed (merged). A well-received internal quality PR.
- **Link:** [PR #49596](https://github.com/anthropics/claude-code/pull/49596)

---

## Feature Request Trends

1. **Cross-agent standardisation (`AGENTS.md`)** – The dominant theme. The community wants an agent-agnostic codebase documentation format (#6235, 4,451 👍). This signals frustration with vendor lock-in and a desire for multi-agent development workflows.

2. **Session state persistence** – Three independent requests for task ID stability across session resumes (#76844, #80871, #80249). Users want background workflows, task lists, and sub-agent contexts to survive compaction and resumption without losing references.

3. **Context awareness and self-regulation** – Growing demand for agents to understand their own context limits, automatically splitting or summarising long sessions (#18027). Users report multi-day sessions where context saturation degrades output quality without any agent-side awareness.

4. **Model behaviour transparency** – Several requests for clearer reasoning about model choices: effort levels, thinking mode activation, and prompt section overrides (#80988, #79798). Users want to know *why* the model behaves differently between versions.

5. **Timezone and localization defaults** – Better handling of local timezones for reporting times (#64988) and more intuitive status indicators (uploading progress, model-speculative status strings in #81287, #81286) — a lower-priority but recurring quality-of-life theme.

---

## Developer Pain Points

1. **State loss across session boundaries** — The most painful recurring issue. Background workflows die at compaction (#80249), task IDs reset on resume (#76844, #80871), and sub-agent context is lost after turn switches (#77554). For users running long orchestration runs, this is a daily blocker.

2. **Prompt injection / invisible configuration overrides** — The `heron_brook` incident (#80988) crystallized a broader concern: silently injected system prompt sections can override user preferences with no opt-out, no logging, and no documentation. Users feel they can't trust that their configuration is being honoured.

3. **Model-specific regressions without warning** — Multiple reports of Opus 4.8 and Fable 5 introducing silent behaviour changes: thinking mode not applied (#79798), arithmetic refusal (#81285), false safety flags on legitimate research (#81288, #74293, #81284). Users want per-model changelogs or model version pinning.

4. **Desktop reliability on Windows** — GPU-process crashes when opening the Browser pane (#77768, #81275) and the `git-credential-proxy` 403 errors since July 24 (#81282) suggest a broader desktop integration regression. Windows users feel underserved.

5. **Opaque errors and unrecoverable failures** — Generic tool errors on control-character commands (#81289), contradictory error responses (`is_error: true, subtype: success` in #81285), and billing bugs with no human escalation path (#68429) erode trust in the error-handling layer.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-26

## Today's Highlights
Windows stability remains the dominant concern, with multiple high-severity bugs reported around GPU process crashes, excessive process spawning, and authentication failures in the VS Code extension. A long-running feature request for **Remote Development in the Codex Desktop App** (Issue #10450, 178 comments) was finally closed, signaling an upcoming feature release. Meanwhile, the team continues to land patches improving MCP server resource management, including raising recursion limits and fixing process leak paths.

## Releases
- **rust-v0.146.0-alpha.10.1** and **rust-v0.146.0-alpha.10** — No detailed changelog available; minor alpha releases.
  - [GitHub Release](https://github.com/openai/codex/releases)

## Hot Issues

1. **[#10450 — Remote Development Support for Codex Desktop App](https://github.com/openai/codex/issues/10450)** *(CLOSED)*  
   The most-upvoted issue this quarter (690 👍, 178 comments). Community has been requesting SSH/remote project support since the desktop app launched. Closure suggests this feature is rolling out.

2. **[#33776 — Windows: ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe](https://github.com/openai/codex/issues/33776)** *(OPEN)*  
   A critical Windows performance bug — 287 taskkill.exe processes observed, causing WMI storms and DWM degradation. 24 comments, 21 👍. High priority for Windows users.

3. **[#1457 — Python UV fails in Codex sandbox](https://github.com/openai/codex/issues/1457)** *(CLOSED)*  
   Long-standing sandbox compatibility issue with the `uv` Python package manager. 61 comments, closed after a year of discussion.

4. **[#30408 — MCP server processes leak unboundedly](https://github.com/openai/codex/issues/30408)** *(OPEN)*  
   Global MCP server processes spawned per-thread are never cleaned up, accumulating 9+ GB RSS over time. 17 comments. A key resource management concern.

5. **[#25453 — Windows: powershell.exe spawned every second for process polling](https://github.com/openai/codex/issues/25453)** *(OPEN)*  
   High CPU usage on Windows due to continuous powershell.exe polling for process lists. 16 comments. Impacts daily workflow on Windows machines.

6. **[#30132 — Azure OpenAI endpoint fails with `oneOf` in root JSON schema](https://github.com/openai/codex/issues/30132)** *(CLOSED)*  
   Tool call schema parsing error specific to Azure endpoints. 21 comments, likely affecting enterprise Azure users.

7. **[#35058 — Codex Diff crashes with "Oops, an error occurred" in VS Code on macOS](https://github.com/openai/codex/issues/35058)** *(OPEN)*  
   Extension diff viewer is completely broken on macOS Apple Silicon. 12 comments, 11 👍. Blocks code review workflow.

8. **[#29356 — Context compaction loses operational continuity](https://github.com/openai/codex/issues/29356)** *(OPEN)*  
   Automatic context compaction in long tasks loses the last few operational steps. 20 comments. Community requests preserving the last 5 steps verbatim.

9. **[#31864 — GPT-5.6 Sol sessions fail with `collaboration.spawn_agent` reserved tool error](https://github.com/openai/codex/issues/31864)** *(OPEN)*  
   All multi-agent Sol sessions fail due to a reserved function name conflict. 14 👍, blocks usage of the latest model for agentic workloads.

10. **[#34133 — Windows: in-app browser screenshot crashes GPU process](https://github.com/openai/codex/issues/34133)** *(OPEN)*  
    Code Integrity rejects bundled `vk_swiftshader.dll`, crashing the GPU process. 14 comments. Affects Windows 10 users.

## Key PR Progress

1. **[#35414 — Raise MCP server recursion limit to 256](https://github.com/openai/codex/pull/35414)** *(CLOSED, copyberry bot)*  
   Prevents stack overflow in MCP server by raising Rust recursion limit. Also populates `started_at_ms` in test fixtures.

2. **[#35408 — Ignore generated system skills in skills watcher](https://github.com/openai/codex/pull/35408)** *(CLOSED, copyberry bot)*  
   Excludes system-level skill cache from recursive file watching, reducing overhead on skill installation.

3. **[#35375 — Make keymap action menu responsive](https://github.com/openai/codex/pull/35375)** *(CLOSED, copyberry bot)*  
   UI improvement: stacks action descriptions below labels on narrow terminals so the keymap menu remains readable.

4. **[#35365 — Keep unified mention results fresh](https://github.com/openai/codex/pull/35365)** *(CLOSED, copyberry bot)*  
   Fixes stale autocomplete results in the unified mention popup by restarting file search on each open.

5. **[#35364 — Bound Code Mode metadata compatibility headers](https://github.com/openai/codex/pull/35364)** *(CLOSED, copyberry bot)*  
   Prevents unbounded HTTP/WebSocket header growth by omitting `code_mode_tool_names` from the compatibility header while retaining it in the canonical metadata.

6. **[#35363 — Include item start times in completion events](https://github.com/openai/codex/pull/35363)** *(CLOSED, copyberry bot)*  
   Adds `started_at_ms` field to `ItemCompletedEvent` for better telemetry and timing analysis.

7. **[#35359 — Handle exec-server network policy requests in client](https://github.com/openai/codex/pull/35359)** *(CLOSED, copyberry bot)*  
   Implements client-side validation and decision routing for exec-server network policy (allow/deny/ask).

8. **[#31582 — Expose thread-selected skills from `skills/list`](https://github.com/openai/codex/pull/31582)** *(CLOSED, jif-oai)*  
   API enhancement: returns skills from executor capability roots selected by the thread, plus warnings when environments are unavailable.

9. **[#30228 — Notify clients when thread-selected skills change](https://github.com/openai/codex/pull/30228)** *(CLOSED, jif-oai)*  
   Adds invalidation signals for skill availability changes (environment ready, recovery, failure).

10. **[#31810 — perf(core): pipeline ancestor discovery](https://github.com/openai/codex/pull/31810)** *(CLOSED, jif-oai)*  
    Performance optimization for remote project startup: parallelizes ancestor directory scanning instead of serial one-at-a-time checks.

## Feature Request Trends
- **Remote Development / SSH Support**: Issue #10450 (690 👍) dominated discussion. Community wants full remote project workflows in the desktop app, likely the next major feature.
- **Context Compaction Intelligence**: Multiple issues (#29356, #23257, #35226) request smarter compaction that preserves operational steps instead of blindly truncating context.
- **Usage Limit Visibility**: Issue #32195 (6 👍) requests persistent display of 5-hour and weekly usage limits in the desktop app status bar.
- **Accessibility**: Issue #34211 reports screen reader (JAWS) not reading chat names or headings on Windows.

## Developer Pain Points
1. **Windows platform instability** — #33776, #25453, #34133, #35352, #32094: GPU process crashes, taskkill/conhost storms, and Code Integrity failures are the top source of bugs.
2. **MCP server process leaks** — #30408: Orphaned MCP processes accumulate unboundedly, consuming memory.
3. **Context compaction ruining long sessions** — #29356, #35226, #23257: Auto-compaction loses progress and consumes paid credits, especially in image-heavy or agentic tasks.
4. **VS Code extension breakage on update** — #35162, #35240: Authentication and login flow fails after extension updates, requiring rollback.
5. **Azure endpoint tool-call incompatibility** — #30132: `oneOf` schema root causes hard failures; custom provider compatibility also fragile (#24973).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-07-26

## Today’s Highlights
The nightly `v0.54.0-nightly.20260726.g3818efbbf` was published with version bumps and changelog updates. On the issue tracker, two long‑standing `p1` agent hang bugs (#21409, #22323) remain open, while the team is making progress on shell output bounding (#28401) and MCP OAuth token refresh (#28481). A flurry of PRs from the new “SSR Pipeline” project (PR generator) landed this week, signaling a push toward automated issue‑to‑PR generation.

## Releases
- **v0.54.0‑nightly.20260726.g3818efbbf** – Automated nightly release. Contains only version bump and changelog updates ([#28536](https://github.com/google-gemini/gemini-cli/pull/28536)). No new user‑facing features.

## Hot Issues (10 noteworthy)
1. **Subagent recovery after `MAX_TURNS` reports success** [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) – `codebase_investigator` marks itself as “GOAL success” even when it hit the turn limit before doing any work. Misleading status reduces trust in agent traces. (12 comments, P1)
2. **Generalist agent hangs forever** [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) – The CLI hangs when deferring to the generalist agent; users report waiting up to an hour. Workaround: disable sub‑agents. (8 comments, P1, 8 👍)
3. **Component‑level evaluations** [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) – Epic to extend behavioral evals to individual agent components. Already 76 tests exist; this tracks expansion. (7 comments, P1)
4. **AST‑aware file reads & codebase mapping** [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) – Investigating whether AST‑aware tools can reduce token waste and improve navigation. (7 comments, P2)
5. **Gemini does not use skills/sub‑agents enough** [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) – Even when custom skills are defined, the model rarely invokes them autonomously. (6 comments, P2)
6. **Auto Memory retries low‑signal sessions indefinitely** [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) – Sessions that are skipped by the extraction agent are never marked “processed,” so they keep appearing. (5 comments, P2)
7. **Deterministic redaction & excessive logging in Auto Memory** [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) – Secrets are sent to the model before redaction; logs may expose sensitive content. (4 comments, P2)
8. **Shell command hangs with “Waiting input” after completion** [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) – Simple commands (e.g., `ls`) leave the terminal in a hung state. (4 comments, P1, 3 👍)
9. **Browser agent fails on Wayland** [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) – Terminal reason shows “GOAL” but the agent fails to start on Wayland. (4 comments, P1)
10. **Subagents running without permission since v0.33.0** [#22093](https://github.com/google-gemini/gemini-cli/issues/22093) – Agents that were explicitly disabled are re‑enabled after update. (3 comments, P2)

## Key PR Progress (10 important)
1. **fix: use resolveRipgrepPath in perf test global setup** [#28535](https://github.com/google-gemini/gemini-cli/pull/28535) – Replaces removed `canUseRipgrep()` to keep performance tests compatible.
2. **fix(CI): retry staging‑tmp dist‑tag removal after npm publish** [#28534](https://github.com/google-gemini/gemini-cli/pull/28534) – Prevents nightly release failures when npm hasn’t propagated the tag yet.
3. **fix(core): refresh MCP OAuth tokens with stored client ID** [#28481](https://github.com/google-gemini/gemini-cli/pull/28481) – Fixes token refresh for dynamically registered MCP servers; previously refresh would silently delete credentials.
4. **fix(shell): bound command output sent to the model** [#28401](https://github.com/google-gemini/gemini-cli/pull/28401) – Caps shell tool output to avoid injecting hundreds of KB of logs into context.
5. **fix(a2a‑server): prevent path traversal in restore command** [#28353](https://github.com/google-gemini/gemini-cli/pull/28353) (closed) – Defense‑in‑depth fix for a path injection vulnerability in the A2A checkpoint restore.
6. **fix: resolve MaxListenersExceededWarning and infinite auth loop** [#28348](https://github.com/google-gemini/gemini-cli/pull/28348) (closed) – Fixes two critical bugs: event listener leak and infinite OAuth loop on Windows.
7. **feat(pr‑generator‑core): environment config parser, command executor, GitHub REST API** [#28435](https://github.com/google-gemini/gemini-cli/pull/28435) – Foundational modules for the SSR Pipeline.
8. **feat(pr‑generator‑orchestrator): iterative bug‑fixing state machine** [#28433](https://github.com/google-gemini/gemini-cli/pull/28433) – Implements the AI coding loop with Firestore concurrency and ESLint checks.
9. **feat(pr‑generator‑agent): Antigravity agent runner and prompt templates** [#28434](https://github.com/google-gemini/gemini-cli/pull/28434) – System prompts for headless code generation & quality assurance.
10. **feat(pr‑generator‑infra): Cloud Run job, Workflows, Dockerfile** [#28431](https://github.com/google-gemini/gemini-cli/pull/28431) – Cloud infrastructure to run the pipeline on Eventarc triggers.

## Feature Request Trends
The community is calling for **better agent reliability and transparency**:
- **AST‑aware tools** for precise code navigation and reduced token overhead ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745)).
- **Improvements to sub‑agent adoption** – the model should autonomously use custom skills and sub‑agents more often ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)).
- **Robust evaluation infrastructure** – component‑level evals, behavioral evals, and trajectory sharing for debugging ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353), [#22598](https://github.com/google-gemini/gemini-cli/issues/22598)).
- **Memory system overhaul** – deterministic redaction, skip low‑signal sessions, quarantine invalid patches ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523)).
- **Agent self‑awareness** – accurate CLI flags, hotkey help, and safe execution defaults ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).
- **Destructive behavior prevention** – discourage `git reset --force` and similar dangerous operations ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).

## Developer Pain Points
- **Hangs and false success** – The generalist agent hangs indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), and sub‑agents report “success” even when they fail ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). This undermines trust in automation.
- **Shell command issues** – Commands that finish remain in “awaiting input” state ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and the model creates tmp scripts in random directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)).
- **Configuration ignored** – Browser agent overrides in `settings.json` are ignored ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and symlinked agent files are not recognized ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)).
- **Browser agent fragility** – Fails on Wayland ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), and locked profiles cause “fail‑fast” errors instead of recovery ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).
- **Security concerns** – Auto Memory sends secrets to the model before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and the A2A server had a path traversal vulnerability (fix merged in [#28353](https://github.com/google-gemini/gemini-cli/pull/28353)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-26

## Today's Highlights

No new releases landed in the last 24 hours, but the community is actively reporting several blocking regressions. A critical memory regression in session resume (issue #4251) and a persistent CAPI 5 MB limit failure despite auto-compaction (#4183) are the most‑voted open bugs. Additionally, a long‑standing skill‑selection limitation (#1464) continues to frustrate users with many installed skills.

## Releases

No new releases in the last 24 hours.

## Hot Issues (10 selected)

1. **#2205 – Scroll usability broken in terminal**  
   *Status: OPEN | 👍 14*  
   Mouse scroll no longer navigates agent output history; instead it scrolls through input history, making long sessions hard to review. Community strongly agrees this is a UX regression.  
   [github/copilot-cli Issue #2205](https://github.com/github/copilot-cli/issues/2205)

2. **#17 – CLI should offer IDE extensions to light up diffs**  
   *Status: CLOSED | 👍 15*  
   A popular feature request: automatic diff highlighting when Copilot CLI runs inside an IDE terminal pane. Closed but often referenced as a desired integration.  
   [github/copilot-cli Issue #17](https://github.com/github/copilot-cli/issues/17)

3. **#1464 – Skills beyond alphabetical position ~32 unreachable**  
   *Status: OPEN | 👍 5*  
   When >63 skills are installed, only the first 32 are visible to the model due to token limits. Skills sorted later are never selected, severely limiting extensibility.  
   [github/copilot-cli Issue #1464](https://github.com/github/copilot-cli/issues/1464)

4. **#1996 – Plugin marketplace install fails on schema validation**  
   *Status: OPEN | 👍 1*  
   Installing `anthropics/claude-plugins-official` fails with `marketplace.json` validation error. Blocks adoption of third‑party plugin marketplaces.  
   [github/copilot-cli Issue #1996](https://github.com/github/copilot-cli/issues/1996)

5. **#4183 – Auto‑compaction does not prevent CAPI 5 MB limit**  
   *Status: OPEN | 👍 10*  
   Long sessions with many tool calls can hit the 5 MB serialized request body limit even after compaction. A hard scaling ceiling that disrupts heavy workflows.  
   [github/copilot-cli Issue #4183](https://github.com/github/copilot-cli/issues/4183)

6. **#4241 – Password masking interferes with agents**  
   *Status: OPEN | 👍 0*  
   Passwords in files get masked from the agent, forcing it to read raw bytes via Python, wasting tokens and causing confusion. Usability and security friction.  
   [github/copilot-cli Issue #4241](https://github.com/github/copilot-cli/issues/4241)

7. **#4244 – Support `/rename` in VS Code agent sessions**  
   *Status: OPEN | 👍 0*  
   The `/rename` command works in terminal CLI but not in VS Code’s agent window. Feature parity request with community appetite.  
   [github/copilot-cli Issue #4244](https://github.com/github/copilot-cli/issues/4244)

8. **#4246 – `archive_session` timeout leaves orphaned worktrees**  
   *Status: OPEN | 👍 0*  
   During teardown of large repositories, the 60‑second timeout can leave sessions and worktrees behind, consuming disk space and preventing branch reuse.  
   [github/copilot-cli Issue #4246](https://github.com/github/copilot-cli/issues/4246)

9. **#4251 – Resume large session OOMs (regression in 1.0.74)**  
   *Status: OPEN | 👍 0*  
   Resuming a long‑lived session after upgrading to 1.0.74 causes 3–4× memory increase and CPU grinding for ~70 minutes. Severe regression for daily users.  
   [github/copilot-cli Issue #4251](https://github.com/github/copilot-cli/issues/4251)

10. **#4252 – Session exit overwrites `settings.json` model selection**  
    *Status: OPEN | 👍 0*  
    On exit, sessions write the launch‑time `model` back to config, silently reverting manual edits or other sessions’ changes. Data‑loss scenario for multi‑session users.  
    [github/copilot-cli Issue #4252](https://github.com/github/copilot-cli/issues/4252)

## Key PR Progress

Only two pull requests were updated in the last 24 hours, both closed:

- **#23 – “Create monad.yml”** (CLOSED)  
  Appears to be a spam/empty PR with no meaningful code changes.  
  [github/copilot-cli PR #23](https://github.com/github/copilot-cli/pull/23)

- **#4228 – “Withdrawn: incorrect scope for #3534”** (CLOSED)  
  Was intended to address a clipboard runtime issue but changed documentation instead. Withdrawn and source branch deleted.  
  [github/copilot-cli PR #4228](https://github.com/github/copilot-cli/pull/4228)

No active or merged PRs this week; community focus is on bug reports.

## Feature Request Trends

- **Improved IDE integration** – Users want `/rename` and other CLI commands to work natively inside VS Code agent sessions (#4244), and automated diff highlighting when CLI runs in an IDE terminal pane (#17).
- **Better skill/plugin management** – The token‑based skill limit (#1464) and marketplace installation validation errors (#1996, #4247) block larger plugin ecosystems. More robust registration persistence is needed.
- **Session isolation and stability** – Issues around session state leaking across conversations (#4249), safe teardown of large worktrees (#4246), and preventing config overwrites (#4252) point to a desire for more robust session lifecycle management.

## Developer Pain Points

- **Scaling and reliability regressions** – The OOM regression on session resume (#4251) and the CAPI 5 MB limit (#4183) are top blockers for power users who rely on long‑running sessions.
- **Plugin ecosystem friction** – Installing third‑party marketplaces fails (#1996) and registrations are not persisted (#4247), wasting developer time.
- **Terminal UX regressions** – The broken mouse scroll (#2205) and password masking interfering with agents (#4241) degrade daily workflow.
- **SSH and remote support gaps** – The `/pr` command fails with SSH host aliases (#4248), and `/ask` frequently returns no result (#4253), undermining trust in core commands.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-07-26

## Today’s Highlights
Three critical bug fixes were merged overnight, addressing session context truncation, stale system prompts on resume, and duplicate file uploads after server restarts. A new dead-loop bug report (#2557) emerged for Kimi Code subscription users, while the long-standing remote control feature request (#1282) continues to draw community support (16 👍). The test suite also received a cross-platform compatibility patch for Windows.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues

1. **#1282 – [Enhancement] Remote Control – Continue local sessions from any device**  
   *Author: CatKang | Created: 2026-02-27 | Updated: 2026-07-25 | Comments: 8 | 👍: 16*  
   **Why it matters:** This feature request proposes the ability to resume a local Kimi CLI session from a phone, tablet, or browser, enabling seamless workflow transitions away from the desk. The high upvote count and sustained discussion (8 comments over 5 months) indicate strong community demand for cross-device session continuity.  
   [GitHub Issue #1282](https://github.com/MoonshotAI/kimi-cli/issues/1282)

2. **#2557 – [Bug] Dead Loop**  
   *Author: zxpdemonio | Created: 2026-07-25 | Updated: 2026-07-25 | Comments: 0 | 👍: 0*  
   **Why it matters:** A new report describes an infinite loop condition in `kimi-cli 1.44.0` when using a Kimi Code subscription. No replies yet, but the lack of workaround suggests a blocking issue for affected users. The bug could be linked to recent context or session logic changes.  
   [GitHub Issue #2557](https://github.com/MoonshotAI/kimi-cli/issues/2557)

## Key PR Progress

1. **#2520 – [CLOSED] fix(session): align fork/undo context truncation to wire turns**  
   *Author: Nas01010101 | Merged: 2026-07-25*  
   **Description:** Resolves #2517 and related issues (#1974, #2049) by correcting the cut logic for wire turns during fork and undo operations. Prevents history mismatches and shifted undo points.  
   [GitHub PR #2520](https://github.com/MoonshotAI/kimi-cli/pull/2520)

2. **#2519 – [CLOSED] fix(app): refresh stale frozen system prompt on session resume**  
   *Author: Nas01010101 | Merged: 2026-07-25*  
   **Description:** Fixes #2420 where resumed sessions ignored skills added to `~/.kimi/skills/` or changes to `AGENTS.md`. Now the system prompt is correctly updated on session resume rather than using a frozen copy.  
   [GitHub PR #2519](https://github.com/MoonshotAI/kimi-cli/pull/2519)

3. **#2518 – [CLOSED] fix(web): persist uploads .sent marker so restarts do not re-send files**  
   *Author: Nas01010101 | Merged: 2026-07-25*  
   **Description:** Addresses #2413 where `kimi web` would re-upload every previously sent file (including images) after a server restart, polluting the session. The fix persists a `.sent` marker to avoid redundant uploads.  
   [GitHub PR #2518](https://github.com/MoonshotAI/kimi-cli/pull/2518)

4. **#2558 – [OPEN] fix(tests): improve Windows cross-platform test compatibility**  
   *Author: panandicoding | Created: 2026-07-25*  
   **Description:** Two Windows test suite issues: `Path.write_text()` without `newline=""` causing `\n` → `\r\n` conversion in `test_background_tools.py`, and … (additional details in PR summary). Small fix (<100 lines) with no prior issue.  
   [GitHub PR #2558](https://github.com/MoonshotAI/kimi-cli/pull/2558)

## Feature Request Trends
- **Cross-device session continuity** (#1282) stands out as the only feature request in the active issue set. Users want to start a CLI session on a desktop and continue it from a phone, tablet, or browser without losing context. The conversation suggests this would require a lightweight remote agent or web relay. No other feature requests appeared in the last 24 hours.

## Developer Pain Points
- **Session durability & state management** – Three merged PRs (#2520, #2519, #2518) directly address regressions in session context (truncation, stale system prompts, file re-upload). The dead-loop bug (#2557) may also relate to context handling, indicating that session logic remains a fragile area.
- **Configuration drift** – The frozen system prompt issue (#2420, fixed in #2519) shows that skill directory and `AGENTS.md` changes were not reflected in resumed sessions, wasting developer time.
- **Windows cross-platform test failures** (#2558) – Line-ending and other platform-specific issues continue to affect the test suite, reducing CI reliability for Windows contributors.
- **Lack of mobility** – The remote control request (#1282) implies frustration with being tethered to a single workstation, a pain point for developers who need to switch contexts frequently.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-26

## Today's Highlights

No new releases landed in the last 24 hours, but the community is buzzing over two long-running frustrations: a CPU usage regression (#30086) that makes even three concurrent sessions laggy, and growing demand for a **"keep legacy layout"** option (#37012) as the redesigned UI continues to polarize users. Meanwhile, a wave of v1.18.5 desktop bugs—freezes on project close, "UnsupportedContentType" errors—has flooded the tracker, with several users reporting the app becomes completely unresponsive after attempting to delete a project.

## Releases

*None in the last 24 hours.*

---

## Hot Issues (Top 10 by community engagement)

1. **[#30086 – High CPU usage in newer versions of OpenCode](https://github.com/anomalyco/opencode/issues/30086)**  
   *36 comments, 👍19*  
   A performance regression that spikes CPU usage dramatically; users report being unable to run more than 3 sessions comfortably. The issue has been open for nearly two months and remains unresolved, causing growing frustration.

2. **[#37012 – [FEATURE] keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)**  
   *33 comments, 👍31*  
   Strong demand for retaining the old UI layout. Users argue the new version forces excessive navigation for common actions and removes workspace flexibility. The high reaction count signals a significant UX divide.

3. **[#15760 – [bug, opentui] Mouse selection unreliable in VSCode terminal](https://github.com/anomalyco/opencode/issues/15760)**  
   *9 comments, closed*  
   Click-and-drag text selection in the TUI output fails most of the time. Though closed, the issue re-emerges frequently, and many still encounter it.

4. **[#38789 – [Bug] Desktop v1.18.5: UnsupportedContentType on project reload](https://github.com/anomalyco/opencode/issues/38789)**  
   *7 comments*  
   After upgrading to v1.18.5, the desktop app shows an error on startup caused by the generated client SDK not recognizing a content type. A clear regression.

5. **[#38801 – message="exiting loop"](https://github.com/anomalyco/opencode/issues/38801)**  
   *6 comments*  
   A recurring `exiting loop` error when using various OpenAI-compatible APIs. Workaround exists (step=80), but the underlying issue persists, making the TUI unusable for many.

6. **[#31217 – [BUG] TUI prompt input fail on Enter](https://github.com/anomalyco/opencode/issues/31217)**  
   *6 comments, 👍1*  
   After typing a prompt and pressing Enter, text disappears but the message isn’t submitted. Affects both Chinese and English input; slash commands still work.

7. **[#38791 – Run loop can never exit when message IDs are not time-sortable](https://github.com/anomalyco/opencode/issues/38791)**  
   *3 comments*  
   `SessionPrompt.runLoop` compares message IDs as plain strings, breaking with imported sessions where IDs don't sort chronologically. Can cause infinite loops until the provider returns a 400 error.

8. **[#36677 – [bug, perf, core, 2.0] Long-lived V2 server enters persistent allocation loop](https://github.com/anomalyco/opencode/issues/36677)**  
   *3 comments*  
   A long-running `opencode2 serve` process consumes ~1 CPU core and 1.1–1.3 GB RSS while idle. A fresh server with same config stays cold, pointing to a memory/GC leak.

9. **[#38773 – [2.0] TUI input area covered by black rectangle during heavy tool-call/reasoning](https://github.com/anomalyco/opencode/issues/38773)**  
   *2 comments*  
   In v2 TUI, the input field is intermittently hidden by a solid black rectangle when the model performs many tool calls. Workaround requires re-entering the TUI.

10. **[#34442 – Windows Desktop installer offline broken: ripgrep not bundled](https://github.com/anomalyco/opencode/issues/34442)**  
    *2 comments, 👍3*  
    On air-gapped Windows machines, core tools (`grep`, `glob`, `skill`) and the built-in `customize-opencode` skill all fail because ripgrep is not bundled and cannot be downloaded.

---

## Key PR Progress (Top 10 impactful PRs)

1. **[#38906 – feat(app): Add progress bar to TUI startup screen](https://github.com/anomalyco/opencode/pull/38906)** (open)  
   Adds staged startup progress (terminal, settings, workspace, theme, plugins) to address the frozen-looking startup. Closes #36195.

2. **[#38802 – feat(app): Improve aesthetics and debuggability – progress bar to TUI start…](https://github.com/anomalyco/opencode/pull/38802)** (closed)  
   Same feature as above, but was closed – likely superseded by #38906.

3. **[#33734 – feat(tui): Publish tui.session.select / tui.session.deselect on session focus changes](https://github.com/anomalyco/opencode/pull/33734)** (closed)  
   Bus events are now emitted when users switch sessions in the TUI, enabling plugin/subscriber integrations. Closes #31051.

4. **[#38433 – feat(opencode): Add roll-call command](https://github.com/anomalyco/opencode/pull/38433)** (open)  
   Introduces a `roll-call` command that tests multiple text models for connectivity and latency. Very useful for debugging provider issues. Closes #13711.

5. **[#38905 – docs: Add PR conventions pointer section to AGENTS.md](https://github.com/anomalyco/opencode/pull/38905)** (open)  
   Adds a missing section so future contributor and agent PRs follow the pull request template. Triggered by PR #38903 which was auto-closed for missing template sections.

6. **[#38903 – feat(plugin): Route ChatGPT OAuth inference via codexApiEndpoint option](https://github.com/anomalyco/opencode/pull/38903)** (open)  
   Makes the ChatGPT inference endpoint configurable instead of hardcoded to `https://chatgpt.com/backend-api/codex/responses`. Important for custom proxies or future endpoint changes.

7. **[#36550 – fix(tui): Resolve keyboard deadlock in question mode](https://github.com/anomalyco/opencode/pull/36550)** (open)  
   Fixes a deadlock in `QuestionPrompt` where two `useBindings` calls with mutually exclusive conditions could lock keyboard input. Closes #36382 and #30517.

8. **[#29789 – feat(opencode): Add Dynamic workflows (new Claude Code feature)](https://github.com/anomalyco/opencode/pull/29789)** (open)  
   Adds project-local workflows invocable via `/workflow <name> arg=value`. This matches Claude Code’s workflow system and is a major new capability.

9. **[#38901 – fix(session): Defer auto-compaction until the next model input](https://github.com/anomalyco/opencode/pull/38901)** (closed, needs compliance)  
   Automatic context compaction was scheduled immediately after an assistant step, causing disruptions. Now deferred until next model input for smoother UX.

10. **[#38200 – feat: Add support for Solidity file type and highlighting](https://github.com/anomalyco/opencode/pull/38200)** (open)  
    Adds Solidity syntax highlighting – useful for Web3 developers. Merge still pending.

---

## Feature Request Trends

Several recurring themes emerge from the last 24 hours:

- **UI/UX preferences** – The strongest signal is the desire to keep the legacy layout (#37012). Also requested: font size adjustment (#38884), scroll-to-top button in chat (#38876), and a more intuitive desktop UI (#38875).
- **Billing & Enterprise** – Requests for annual subscription plans and official invoices (#20252) indicate growing enterprise adoption.
- **Session management** – Display session name in TUI status bar (#38881), ability to force immediate reading of queued messages (#24298).
- **Developer tools** – Dynamic workflows (PR #29789), roll-call command (PR #38433), and Solidity syntax highlighting (PR #38200) show a desire for extensibility and debugging aids.
- **Offline/air-gapped installs** – The broken Windows offline installer (#34442) highlights the need for bundled dependencies.

---

## Developer Pain Points

The most pressing frustrations reported in the last 24 hours:

- **Desktop freezes and crashes** – v1.18.5 causes freezes when closing a project (#38844, #38885, #38895) and "Internal Server Error" on many models (#38873, #38874).
- **TUI responsiveness** – Mouse selection unreliable (#15760), prompt text swallowed on Enter (#31217), input area hidden by black rectangle (#38773), keyboard deadlocks (#36550).
- **Performance regressions** – High CPU usage (#30086) and persistent allocation loops in the v2 server (#36677).
- **Provider compatibility** – Xiaomi MiMo rejects list-type tool message content (#32613), Lan-hosted Ollama not connecting on macOS (#38854), and `exiting loop` when using varied OpenAI APIs (#38801).
- **Core logic bugs** – Session run loop never exits with non-time-sortable IDs (#38791), subagent stream errors masked as empty task results (#38866), and auto-compaction scheduled disruptively (PR #38901).
- **Offline installation** – ripgrep not bundled on Windows (#34442) makes core tools unusable without internet.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-26

## Today’s Highlights
Pi **v0.82.1** shipped today, adding **Claude Opus 5** with adaptive thinking support on Anthropic and Bedrock. Several hot issues around compaction reliability and TUI performance continued to attract community discussion, while a flurry of PRs addressed cross‑platform path handling, OpenRouter OAuth on remote machines, and a new extension context‑clear API.

---

## Releases

**v0.82.1** ([release notes](https://github.com/earendil-works/pi/releases/tag/v0.82.1))  
- **Claude Opus 5** — now available on Anthropic and Amazon Bedrock, with adaptive thinking (`xhigh`), inference profiles, and prompt caching.  
- Additional provider documentation updates.

---

## Hot Issues (10 noteworthy)

1. **[Issue #4877 – Session folder collision](https://github.com/earendil-works/pi/issues/4877)** *(CLOSED, 21 comments, 👍2)*  
   Suggests path‑to‑folder slugging can collide (e.g., `/a/b/c/d` ↔ `/a-b/c-d`). Low severity but a lurking UX surprise.

2. **[Issue #6050 – TUI full redraw clears terminal scrollback](https://github.com/earendil-works/pi/issues/6050)** *(CLOSED/no‑action, 15 comments)*  
   Frequent full‑screen redraws cause scrollback jumps in interactive mode – a core renderer problem that frustrates long sessions.

3. **[Issue #6768 – Compaction with Copilot Enterprise fails](https://github.com/earendil-works/pi/issues/6768)** *(OPEN, 13 comments, 👍11)*  
   High‑impact: Copilot Enterprise users hit `421 Misdirected Request` on compaction. Community upvotes reflect widespread need for enterprise LLM support.

4. **[Issue #6665 – TUI pins a full core while streaming](https://github.com/earendil-works/pi/issues/6665)** *(OPEN/inprogress, 7 comments)*  
   `Intl.Segmenter` + per‑chunk Markdown rebuild causes 100% CPU. Performance fix eagerly awaited.

5. **[Issue #5990 – TUI flickers when dialog taller than terminal](https://github.com/earendil-works/pi/issues/5990)** *(OPEN/inprogress, 5 comments, 👍3)*  
   Continuous repaint when confirm/select dialogs exceed viewport – a long‑standing visual annoyance.

6. **[Issue #7090 – Shrinkwrap includes vulnerable brace-expansion v5.0.7](https://github.com/earendil-works/pi/issues/7090)** *(CLOSED/no‑action, 4 comments)*  
   CVE‑2026‑14257 in `brace-expansion` / `minimatch`. Fix available in 5.0.8; prompt for rebuild.

7. **[Issue #7020 – Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)** *(OPEN/inprogress, 4 comments, 👍1)*  
   Long‑running “coordinator” sessions hang post‑compaction. Underlying compaction state machine bug.

8. **[Issue #6948 – llama.cpp default model not applied at startup (race)](https://github.com/earendil-works/pi/issues/6948)** *(CLOSED, 4 comments)*  
   Async model refresh races with session init; model shows in `/model` but not active. Fixed by caching in PR #7072.

9. **[Issue #7064 – WSL absolute Windows paths mishandled](https://github.com/earendil-works/pi/issues/7064)** *(OPEN, 3 comments)*  
   `read`/`write`/`edit` tools fail on WSL2 because path handling doesn’t translate Windows paths – critical for Windows developers on WSL.

10. **[Issue #7077 – “Working…” status persists after task done](https://github.com/earendil-works/pi/issues/7077)** *(CLOSED/no‑action, 3 comments)*  
    Spinner freezes while agent already awaits input – confusing UX feedback.

---

## Key PR Progress (10 important)

1. **[PR #7118 – Expose extension context clear callback](https://github.com/earendil-works/pi/pull/7118)** *(CLOSED)*  
   Adds a runtime API for extensions to clear session context without generating a summary – enables safe hand‑off tools.

2. **[PR #7117 – Extension creation eval](https://github.com/earendil-works/pi/pull/7117)** *(OPEN)*  
   New `vitest-evals` harness for coding agent smoke tests, including isolated extension‑creation evaluation.

3. **[PR #7031 – Run coding-agent tests offline by default](https://github.com/earendil-works/pi/pull/7031)** *(OPEN)*  
   Sets `PI_OFFLINE=1` for all coding‑agent tests; re‑enables online only where needed. Reduces test flakes.

4. **[PR #7116 – Truncate over‑width TUI lines instead of crashing](https://github.com/earendil-works/pi/pull/7116)** *(CLOSED)*  
   Prevents session‑killing crashes when a line exceeds terminal width – e.g., from long JSON in permission banners.

5. **[PR #7114 – Manual redirect URL fallback for OpenRouter OAuth](https://github.com/earendil-works/pi/pull/7114)** *(OPEN)*  
   Enables `/login openrouter` on SSH/headless machines by supporting manual paste of callback URL.

6. **[PR #7112 – Cross‑platform footer path separator](https://github.com/earendil-works/pi/pull/7112)** *(CLOSED)*  
   Forces forward slash in footer CWD display, fixing `~\project` vs `~project` on Windows.

7. **[PR #7111 – Durable external tool results](https://github.com/earendil-works/pi/pull/7111)** *(CLOSED)*  
   Generic `defer: true` mechanism for tools that need to wait for out‑of‑process results without fabricating tool messages.

8. **[PR #7110 – Prevent duplicate messages after session switch](https://github.com/earendil-works/pi/pull/7110)** *(OPEN)*  
   Fixes duplicate assistant messages when switching sessions during startup.

9. **[PR #7106 – Exclude directories from resource loader](https://github.com/earendil-works/pi/pull/7106)** *(CLOSED)*  
   Suppresses `EISDIR` warning when scanning for AGENTS.md – a common annoyance.

10. **[PR #7091 – Reject overlapping user bash commands](https://github.com/earendil-works/pi/pull/7091)** *(CLOSED)*  
    Prevents concurrent RPC bash commands from the same user, avoiding race conditions and confusing output.

---

## Feature Request Trends

- **Model‑switch validation** – Multiple requests (#7065, #7067) to check context window fit, convert thinking blocks, and validate before mid‑session switch.
- **Cost visibility** – Proposals for cost‑preview columns in the model selector (#7101) and accurate OpenRouter alias cost reporting (#7109).
- **Session‑affinity headers for custom providers** – Several duplicate issues (#7104, #7107, #7108) asking to forward `session_id` / `x-session-affinity` to user‑defined OpenAI‑compatible providers.
- **Configurable truncation limits** – #7066 asks for tool output truncation to be user‑configurable, especially for local models.
- **OpenRouter headless login** – Support manual paste of callback URL (PR #7114, issue #7078) for users on remote/SSH machines.

---

## Developer Pain Points

- **Compaction reliability** – Multiple issues (#6768, #7020, #7048) report compaction failures or hangs, especially with Copilot Enterprise and long‑running sessions.
- **TUI performance** – CPU spikes (#6665), scrollback clearing (#6050), and flickering dialogs (#5990) remain open, impacting daily use.
- **Cross‑platform path handling** – Windows/WSL absolute path breaks (#7064), and footer path separators (#7112) highlight ongoing gaps.
- **Model validation after upgrade** – Several users report sudden tool validation failures after updating to 0.82.0 (#7069, #7056).
- **OpenRouter cost reporting** – Dynamic routing aliases report zero cost (#7109) – a blocker for budget‑conscious users.
- **Model catalog race conditions** – Race between model refresh and session init (#6948) causes “default model not applied” frustration.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-26

## Today's Highlights

A nightly release (`v0.21.0-nightly`) landed with a CLI fix for consistent local-time measurement and an autofix refactoring. The community is actively debating a proposal for a direct external context provider (#7585), while several UI bugs (IME cursor misalignment, multi-line statusline) and MCP integration issues (Unity, sandbox detection) dominate the issue tracker. Key PRs introduce lazy-loading for performance, sandbox runtime probing, and model grade selection for subagents — signalling a focus on both developer experience and system reliability.

## Releases

- **[v0.21.0-nightly.20260726.9d19eafa9](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260726.9d19eafa9)**  
  - `fix(cli): measure insight days and hours in local time everywhere` — ensures time-based metrics respect the user’s locale.  
  - `refactor(autofix): ext` — refactors the autofix extension machinery.

## Hot Issues (10 selected)

1. **#7585** [OPEN] [feature-request] *Add a direct external context provider profile*  
   A proposal for a Qwen extension that lets one CLI process retrieve repository-shared context from an administrator-bound external memory service. 6 comments, active discussion around architecture and MCP integration.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7585)

2. **#7665** [OPEN] [bug] *Error code 520/522*  
   User reports being unable to continue coding after installation. High frustration (image included). 5 comments.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7665)

3. **#7684** [OPEN] [bug] *IME candidate window misplaced when statusline spans multiple lines (macOS)*  
   Command mode input method overlay appears far from cursor. 5 comments, welcome for contribution.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7684)

4. **#7719** [OPEN] [feature-request] *CLI does not display token usage or usage percentage*  
   Users want real-time token consumption monitoring. 3 comments, reflects demand for better resource visibility.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7719)

5. **#7732** [OPEN] [bug] *Sandbox runtime selected on PATH presence alone, ignores unusable Docker*  
   If Docker is installed but unreachable, Podman is not tried. 2 comments, creates blocking workflow for container-based sandbox users.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7732)

6. **#7717** [OPEN] [bug] *Skill auto-complete broken when multiple skills mentioned continuously*  
   Only the first skill triggers autocomplete after update. 2 comments, welcome for contribution.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7717)

7. **#7697** [OPEN] [bug] *Qwen Code VS Code extension cannot connect to Unity MCP, but Claude Code can*  
   MCP integration failure specific to Unity. 4 comments, highlights cross-tool compatibility gaps.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7697)

8. **#7659** [CLOSED] [bug] *`tool_choice: "required"` rejected in DashScope thinking mode*  
   Fixed in PR #7661. Memory recall side queries were broken when a model had thinking enabled. 3 comments.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/7659)

9. **#6801** [OPEN] [feature-request] *Pinned/ memory directory — read-only files protected from /dream consolidation*  
   Proposal for a `pinned/` subdirectory to preserve critical memory files. 3 comments, strong community interest.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/6801)

10. **#7700** [OPEN] [feature-request] *Define explicit, source-preserving math authoring contract*  
    Proposes portable syntax for model-authored inline math to avoid rendering ambiguities. 3 comments.  
    [GitHub](https://github.com/QwenLM/qwen-code/issues/7700)

## Key PR Progress (10 selected)

1. **#7686** [OPEN] *perf(core): Lazy-load first-use dependencies*  
   Reduces startup time by deferring import of heavy modules until first use. Important for CLI responsiveness.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7686)

2. **#7733** [OPEN] *feat(review): redefine medium effort as a balanced verified pass*  
   Changes `--effort medium` from a thin inline pass to a verified pass with subagent-based build/test verification.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7733)

3. **#7734** [OPEN] *fix(cli): probe sandbox runtime before selecting it*  
   Directly addresses issue #7732 — now probes Docker/Podman with `version` before committing to a sandbox runtime.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7734)

4. **#7710** [OPEN] *feat(triage): add sandboxed /verify deep-verification lane*  
   Enables maintainer-grade evidence rounds (build diff, test vacuity, wire-oracle) against PRs via `@qwen-code /verify`.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7710)

5. **#7731** [OPEN] *feat(web-shell): add git branch picker, commit dialog, and create PR flow*  
   IntelliJ-style branch popover with checkout, commit, and PR creation — significant UX uplift for the web shell.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7731)

6. **#7702** [OPEN] *feat(core): add model grade selection for subagent spawn (#7685)*  
   Implements `model` parameter on the `agent` tool, letting AI choose between small/medium/high/super grades defined in settings.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7702)

7. **#7714** [OPEN] *feat(memory): protect pinned files during forked Dream*  
   Adds a permission gate to deny write/edit on paths under `pinned/` and skips them during consolidation. Addresses #6801.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7714)

8. **#7711** [OPEN] *fix(cli): keep IME cursor aligned after footer updates*  
   Resolves the multi-line statusline IME misalignment on macOS (#7684) by reasserting cursor position in Ink’s render phase.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7711)

9. **#7661** [CLOSED] *fix(core): avoid required tools in DashScope thinking*  
   Fixes #7659 — stops sending `tool_choice: "required"` when thinking is enabled for DashScope.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/7661)

10. **#7620** [OPEN] *fix(web-shell): parse 256-color and truecolor SGR sequences in parseAnsi*  
    Properly consumes arguments of extended color codes (`38;5;…`, `38;2;…`), fixing broken color rendering in web shell.  
    [GitHub](https://github.com/QwenLM/qwen-code/pull/7620)

## Feature Request Trends

- **External context & memory** — Proposals for direct external context providers (#7585), pinned memory directories (#6801), and protecting memory from dream consolidation.  
- **Model & agent configurability** — Subagent model grade selection at spawn time (#7685), overridable `defaultDisabled` for skills (#7347), and configurable stream rate-limit retry delays (#7658).  
- **Observability** — Token usage display in CLI (#7719), generation timing metrics (TPS/TTFT) in `/stats` (#4252).  
- **UI/UX enhancements** — Math authoring contract for markdown rendering (#7700), git branch picker and PR flow (#7731), IME alignment fixes.  
- **MCP & integration improvements** — Direct external context via MCP, Unity MCP connectivity, OAuth callback documentation for remote MCP (#7503).

## Developer Pain Points

- **CLI rendering glitches** — IME candidate overlay misplaced when statusline spans multiple lines (#7684), terminal auto-scroll on every keystroke (#7713).  
- **Sandbox detection fragile** — Runtime chosen based on PATH only, not actual availability (#7732).  
- **MCP integration gaps** — Unity MCP works in Claude Code but not in Qwen Code (#7697); session restore broken after bridge restart (#7721).  
- **Skill autocomplete regressions** — Multiple consecutive skills only complete the first (#7717).  
- **Hardcoded behaviours** — Rate-limit retry delays not configurable (#7658); stop hooks missing on loop detection exit (#7588).  
- **CI instability** — Flaky E2E tests (tool-control) and self-resolving CI failures causing noise (#7725, #7712).  
- **Authentication/configuration friction** — Unclear OAuth redirect for remote MCP (#7503), error codes 520/522 from installation (#7665).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-26

## Today’s Highlights
The v0.9.2 development sprint is in full swing, with infrastructure PRs landing for workflow per-worker telemetry (#4842) and a comprehensive localization docs update (#4839). A cluster of critical bugs surfaced: the test suite intermittently writes to the developer’s real config (#4831), the new macOS “underwater” shell breaks `open`/`osascript` (#4828), and config validation outright rejects non-DeepSeek providers (#4829). Meanwhile, the community continues to push for cross-provider parity, plugin ecosystems, and performance improvements.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)

- **#4520 – Configurable session token breakdown in header bar**  
  *enhancement, UX*  
  Users miss the old verbose input/cache-hit/output token breakdown after PR #2411 compacted it to a single cumulative total. The author argues this should be an optional toggle.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/4520)

- **#4831 – Full test suite intermittently writes to real `~/.codewhale/config.toml`**  
  *bug, reliability*  
  Running `cargo test --workspace` twice on the same tree gave different results tied to writes to the developer’s actual config file. This is a serious CI/reproducibility concern.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/4831)

- **#2743 – FR: Adapt Claude Code skill ecosystem**  
  *enhancement*  
  The `skill-installer` does imperfect translations of Claude Code‑only skills. Request for native compatibility so CodeWhale can run skills like `understand-anything` without loss.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/2743)

- **#1172 – Plugin/workflow migration from Cursor, CC, Codex**  
  *enhancement*  
  A user with a plugin‑based workflow wants to migrate to CodeWhale. The community votes for a plugin + hook system (session start/end, etc.) to unlock existing ecosystems.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/1172)

- **#3927 – Explicit provider‑independent offline path for onboarding**  
  *UX, onboarding*  
  Even after provider choice (including keyless Ollama/SGLang), every path still activates some network activity. Users want a true offline “look around” mode.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/3927)

- **#3314 – Extract `App` god object into owned submodules**  
  *refactor, architecture*  
  The `App` struct now has ~252 public fields and ~236 methods across 4,450 lines in one file. This is a long‑standing tech debt item blocking maintainability.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/3314)

- **#3091 – Website parity with Japanese/Vietnamese README locales**  
  *localization, UX*  
  README translations exist for Japanese and Vietnamese but the website only ships English/Chinese. Community wants the website to reflect all translated content.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/3091)

- **#2974 – Wire model‑facing workflow tool and run driver**  
  *workflow, v0.9.2*  
  The workflow runtime compiles and tests, but the TUI has no normal user path to trigger a workflow run. This remains a top blocker for the v0.9.2 feature set.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/2974)

- **#4828 – macOS underwater shell breaks open/osascript/launchctl (exit code -54)**  
  *bug, macOS*  
  After upgrading to v0.9.0, shell commands via `exec_shell` fail with “operation not permitted” on macOS. Downgrade to v0.8.67 works. High impact on macOS users.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/4828)

- **#4833 – Light‑background TUI renders default text at near‑background contrast**  
  *bug, UX*  
  A v0.9.1 user reports the default text colour on light terminals is extremely pale grey, making it illegible.  
  [GitHub](https://github.com/Hmbown/CodeWhale/issues/4833)

## Key PR Progress (10 important)

- **#4842 – Workflow per‑worker usage telemetry and bounded run‑record payloads**  
  *feature, workflow*  
  Ports two missing halves of #2974 onto `main`: `task_completed` carrier and bounded payload serialisation. Critical for v0.9.2 workflow release.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4842)

- **#4841 – Remove retired `--no-alt-screen` compatibility flag**  
  *cleanup*  
  The flag was a hidden no‑op; removing it reduces CLI surface.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4841)

- **#4839 – Describe TUI locale packs and gate locale drift in CI**  
  *docs, localization*  
  Updates `LOCALIZATION.md` to cover `crates/tui/locales/` (8 languages) and adds CI logic to prevent drift between translation files.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4839)

- **#4686 – Add China/Token Plan provider routes for minimaxi.com**  
  *feature, providers*  
  Adds four new provider identifiers (`minimax-cn`, `minimax-anthropic-cn` etc.) targeting the Chinese API endpoint. Community contributed by `ffaacceelee`.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4686)

- **#4566 – Update TUI Cargo.toml for HarmonyOS build**  
  *portability*  
  Moves `portable-pty` to Unix‑only and updates dependencies so CodeWhale compiles and runs on HarmonyOS PC.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4566)

- **#4743 – Fix 45s SSE open timeout for non‑streaming chat requests**  
  *bug fix*  
  `codewhale exec` (plain, without `--auto`) was aborting after 45 seconds on non‑streaming backends. Now the timeout only applies to actual SSE streams.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4743)

- **#4722 – Show complete edit previews in details pager**  
  *UX, TUI*  
  Keeps the compact `edit_file` approval card bounded, then builds the full search/replace diff lazily in the Alt+V details view. Includes regression tests.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4722)

- **#4724 – Archive completed background shell output**  
  *fix, TUI*  
  When a background shell job reaches a terminal state, its final stdout/stderr tail is archived into the originating `ExecCell`, and live output is cleared.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4724)

- **#4742 – Preserve hashes in fleet strings**  
  *fix, parser*  
  Fixes a fleet parser bug that treated `#` characters inside quoted values as comments, breaking issue references and role values.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4742)

- **#4756 – Do not retry failed qualified MCP tool calls**  
  *fix, MCP*  
  Returns the fast‑path error from a qualified MCP server directly instead of retrying, avoiding duplicate invocations. Regression test added.  
  [GitHub](https://github.com/Hmbown/CodeWhale/pull/4756)

## Feature Request Trends

- **Token visibility** – Multiple users want the ability to see input/cache/output token breakdown in the header (re‑enable the old verbose format as an option).
- **Cross‑provider ecosystem** – Strong demand to support Claude Code skills natively, and to allow plugin‑based workflows from Cursor/CC/Codex to migrate with hooks and a marketplace.
- **Multi‑language website** – The community expects the website to mirror the README localizations already shipped (Japanese, Vietnamese, Korean, Spanish, Portuguese, Russian).
- **Offline first class** – Onboarding should allow exploring the TUI without any provider or network connection.
- **Workflow runtime** – Users are watching #2974 closely; the ability to compose and run workflows from within the TUI is the marquee v0.9.2 feature.
- **Performance** – Recurring requests to optimise the TUI render loop: eliminate synchronous `fs::metadata` calls on every frame, cache token estimates, and offload the Ctrl+P file picker’s `git status` subprocess.

## Developer Pain Points

- **Test flakiness** – The test suite writing to the real config file (#4831) erodes trust and blocks reliable CI.
- **macOS compatibility** – The “underwater” shell v0.9.0 regression (#4828) breaks fundamental shell commands. High frustration for Mac users.
- **Non‑DeepSeek provider friction** – Config validation rejects models that aren’t DeepSeek families (#4829), and `codew model set` silently ignores non‑DeepSeek providers (#4838). Makes the tool effectively single‑provider for many users.
- **UI regressions** – Light‑background colour contrast (#4833) and the Script Editor icon for macOS notifications (#4834) are polish issues that affect daily use.
- **Performance during large sessions** – The Ctrl+P file picker blocks the event loop, and token estimation re‑serialises the entire history every frame (#3904–#3907). Heavy project users hit these bottlenecks repeatedly.
- **Onboarding confusion** – No way to read the constitution in‑app (#3928) and the offline path still forces network activity (#3927) frustrate new users evaluating the tool.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*