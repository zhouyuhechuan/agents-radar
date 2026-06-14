# AI CLI Tools Community Digest 2026-06-14

> Generated: 2026-06-14 02:54 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report

**Date:** 2026-06-14  
**Prepared for:** Technical decision-makers evaluating the AI developer tools landscape

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is entering a phase of hyperactive differentiation, with six major open-source projects and one commercial offering (Claude Code) competing across overlapping but distinct value propositions. The dominant themes across all tools are **MCP ecosystem maturation**, **multi-agent orchestration**, and **persistent memory/state management**—each tool is investing heavily in at least one of these areas. Notably, Claude Code remains the benchmark for feature depth but shows signs of permission-model growing pains, while fast-followers like Qwen Code and OpenCode are aggressively closing the gap with dynamic workflows and MCP client parity. A second cluster of tools (Pi, CodeWhale, Gemini CLI) is pursuing architectural differentiation through headless sub-agent runtimes and provider-agnostic designs, signaling that the market has not yet converged on a dominant architecture.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | PR Activity (24h) | Release Status Today | Key Theme |
|------|------------------|-------------------|---------------------|-----------|
| **Claude Code** | 10 active | 3 (1 merged) | No release | Permission bypass regressions, memory persistence |
| **OpenAI Codex** | 10 (2 closed) | 10 (various) | 2 alpha releases (v0.140.0-alpha.18/.19) | Windows sandbox fixes, safe-check false positives |
| **Gemini CLI** | 10 (2 closed) | 10 (3 merged) | No release | Security patching, MCP & Auto Memory fixes |
| **GitHub Copilot CLI** | 5 (2 closed) | 0 | 2 minor releases (v1.0.62, v1.0.62-2) | UX polish, plugin extensions |
| **Kimi Code CLI** | 2 (both open) | 5 (3 merged) | No release | MCP error suppression, timeout fixes |
| **OpenCode** | 10 (5 closed) | 10 (3 closed) | 2 patch releases (v1.17.5, v1.17.6) | MCP capabilities, `/goal` feature, Cedric workspace |
| **Pi** | 10 (7 closed) | 10 (8 closed) | 1 patch (v0.79.3) | Billing hazard fix, cache retention bug |
| **Qwen Code** | 10 active | 10 (2 merged) | No release | Dynamic Workflows P4a, provider decoupling |
| **DeepSeek / CodeWhale** | 10 active | 8 open | No release (v0.8.60 in progress) | Headless sub-agent runtime, agent fleet orchestration |

**Observations:**
- **Highest release velocity:** OpenAI Codex (2 alphas) and GitHub Copilot CLI (2 releases)
- **Most active issue resolution:** Pi (7/10 issues closed) and OpenCode (5/10 closed)
- **Most architectural change:** DeepSeek/CodeWhale (sub-agent re-architecture) and Qwen Code (Dynamic Workflows P4)
- **Lowest activity:** Kimi Code CLI (only 2 issues, but proportional to smaller community)
- **Security incidents today:** Gemini CLI (command injection fix), OpenCode (OAuth XSS fix), Qwen Code (Trojan false positive)

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating strong market demand:

### 3.1 Persistent Memory & Context Persistence
| Tools | Specific Need | Issue/Reference |
|-------|---------------|-----------------|
| **Claude Code** | Official hooks for context compaction memory | #34556, #47023 (160+ combined 👍) |
| **OpenCode** | Auto-save session records to disk | #1865 |
| **Pi** | `cache_control.ttl` fix for Claude (1h→5m regression) | #5703 |
| **Gemini CLI** | Auto Memory redaction & retry fixes | #26525, #26522 |
| **Qwen Code** | Long-context attention degradation | #5018 |

*Signal:* Users across all tools are demanding **durable, inspectable state** that survives context limits and session restarts. This is the #1 unmet need in the ecosystem.

### 3.2 MCP Ecosystem Parity & Friction
| Tools | Specific Need | Issue/Reference |
|-------|---------------|-----------------|
| **Claude Code** | MCP permission dialogs in remote UI | #60385 |
| **Gemini CLI** | MCP client lacks resources/prompts support | #3816 |
| **GitHub Copilot CLI** | MCP tool preloading (not lazy-loaded) | #3787 |
| **Kimi Code CLI** | MCP connection error suppression | #2434 (merged) |
| **OpenCode** | Full MCP client capabilities (roots, sampling) | #28567 (20 👍) |
| **Pi** | Tool argument validation (JSON→Array coercion) | #5697 |

*Signal:* Every tool treats MCP as strategic infrastructure, but **client-side parity with the MCP specification** (roots, sampling, notifications) remains incomplete. OpenCode and Gemini CLI are furthest behind.

### 3.3 Multi-Agent Orchestration & Agent Teams
| Tools | Specific Need | Issue/Reference |
|-------|---------------|-----------------|
| **Claude Code** | Agent Teams bypassPermissions regression | #26479 |
| **OpenAI Codex** | MultiAgentV2 encryption kills audit trails | #28058 |
| **Qwen Code** | Dynamic Workflows (Claude Code parity) | #5094 (P4a merged) |
| **DeepSeek/CodeWhale** | Headless sub-agent runtime + agent fleet | #3096, #3154 |
| **Pi** | ESC not stopping subagents | #5685 |

*Signal:* The industry is converging on **nested, hierarchical agent execution** with sub-agent orchestration. Challenges include cost control (#68285 in Claude Code), auditability (#28058 in Codex), and configuration inheritance (#26479 in Claude Code).

### 3.4 Bring Your Own Model / Provider Flexibility
| Tools | Specific Need | Issue/Reference |
|-------|---------------|-----------------|
| **GitHub Copilot CLI** | Ollama API key support in BYOM | #3789 |
| **Pi** | Configurable timeout/retry for local models | #3627 |
| **Qwen Code** | Decouple protocol from provider identity | #5089 (PR) |
| **DeepSeek/CodeWhale** | First-party Z.ai, StepFlash providers | #3191 (merged) |
| **Gemini CLI** | OAuth refresh for auto-discovered MCP | #27889 (PR) |

*Signal:* **Provider-agnostic architecture** is a competitive differentiator. Qwen Code's PR #5089 explicitly separates authentication type from protocol, enabling custom providers—a pattern others are likely to follow.

### 3.5 IDE & Editor Integration
| Tools | Specific Need | Issue/Reference |
|-------|---------------|-----------------|
| **Claude Code** | JetBrains plugin request | #47166 |
| **Claude Code** | VS Code auto-attach toggle | #24726 (159 👍) |
| **OpenCode** | Zed native changes review | #4240 (19 👍) |
| **Kimi Code CLI** | VS Code extension freezing reported | #2450 |

*Signal:* **Editor integration remains fragmented.** Claude Code and OpenCode have the most mature IDE stories, but each platform (VS Code, JetBrains, Zed) has gaps. No tool supports all three equally.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek/CodeWhale |
|-----------|-------------|--------------|------------|--------------------|----------|-----|-----------|-------------------|
| **Primary Differentiator** | Feature depth, largest community | Windows sandbox, Rust rewrite | Security-first, Google ecosystem | VS Code/GitHub integration | MCP ecosystem pioneer | Provider-agnostic modularity | Multi-provider convenience, China market | Headless sub-agent architecture |
| **Target User** | Power user, CI/CD | Enterprise Windows, safety-sensitive | Google Cloud ecosystem | GitHub Enterprise | Tool-switcher (from Claude) | OSS enthusiast, local models | QwenLM ecosystem, Asia | TUI-first, experimental |
| **Architecture** | Monolithic Node.js | Rust rewrite in progress | Node.js | Node.js | Modular (MCP client) | Modular JS (Shrinkwrap?) | Go-based | Rust (TUI + headless runtime) |
| **MCP Maturity** | Most complete | Partial | Partial (no resources/prompts) | Minimal (MCP tools emerging) | Most ambitious (roots, sampling) | Moderate | Moderate | Moderate |
| **Windows Support** | Lags (cowork lockups, OneDrive) | Best-in-class (Rust + Wine) | Limited | Good (VS Code ecosystem) | Issues (UNC, cache persistence) | Partial | Partial (CLI, but VSCode flagged) | N/A (Rust, cross-platform) |
| **Cost Model** | Usage-based + auto-purchase | Token-based | Google Cloud billing | Copilot license | Usage-based | Provider pass-through | Free tier scaling back | Config-gated Pro Plan |
| **Sub-Agent Design** | In-process agent teams | MultiAgentV2 encrypted | Browser subagent | Not present | Not present | Background agents | Dynamic Workflows (P1-P4) | **Headless worker runtime** (proposed) |

**Key insight:** DeepSeek/CodeWhale's headless sub-agent proposal (#3096) is architecturally the most forward-looking—it addresses the fundamental tension between "UI-shaped" agent processes and scalable orchestration. If implemented, it could leapfrog Claude Code's current in-process agent team model.

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek/CodeWhale |
|--------|-------------|--------------|------------|-------------|----------|-----|-----------|-------------------|
| **Github Stars (approx.)** | ~70k+ | ~200k+ (original) | ~20k | ~10k | ~15k | ~5k | ~10k | ~2k |
| **Issue Velocity (24h)** | High | High | High | Low | High | Moderate | Very High | Very High |
| **PR Velocity (24h)** | Low | High | High | None | High | Very High | High | Moderate |
| **Release Cadence** | Slowing (beta maturity) | **Alpha every ~2 days** | Weekly+ | Weekly | Weekly | Weekly+ | Daily+ | v0.8.60 in progress |
| **Community Engagement** | 159 👍 on top issue | 52 comments on top issue | 6 comments average | 0-4 comments | 20 👍 on top issue | 8 comments average | **129 comments** (OAuth policy) | 6-7 comments average |
| **Contribution Health** | Forks + workarounds | Community troubleshooting | PRs from core team | 0 PRs today | Diverse PR authors | Mix of core + community | Growing contributor base | Active community PRs (#3201, #3196) |

**Maturity Assessment:**
- **Mature/Stable:** Claude Code, OpenAI Codex (original), GitHub Copilot CLI
- **Rapidly Iterating:** Qwen Code (daily alpha equivalent), Gemini CLI, OpenCode, Pi
- **Early/Architecting:** DeepSeek/CodeWhale (pre-v0.8.60), Kimi Code CLI (smallest community)

**Velocity leaders:** Qwen Code and Pi have the highest PR throughput. OpenAI Codex is unusual—high release velocity for alpha (2/day) but focused on incremental fixes rather than new features.

---

## 6. Trend Signals & Developer Recommendations

### Six Industry Trends from Community Feedback

**1. Agent Architecture is Decoupling from UI**
DeepSeek/CodeWhale's headless sub-agent proposal (#3096) and Qwen Code's Dynamic Workflows (#5094) signal that **the next frontier is not just "better agents" but "agent orchestration runtimes"**. Decision-makers should evaluate tools not just on chat quality but on their ability to compose agents programmatically.

**2. MCP is Becoming the Universal Adapter**
The fact that every tool is investing in MCP—and that gaps in MCP support are the top-voted feature requests (OpenCode #28567, Gemini CLI #3816, Copilot #3787)—indicates **MCP is replacing proprietary plugin APIs** as the standard integration layer. Tools that lag on MCP client parity (Gemini CLI, Copilot CLI) risk ecosystem exclusion.

**3. Cost Transparency is a Critical UX Requirement**
The Claude Code workflow fan-out incident (#68285, ~$1k overrun) and Pi's billing hazard fix (#5703) demonstrate that **unpredictable costs erode trust faster than technical bugs**. Cross-tool, expect built-in cost ceilings and per-agent budgets to become table stakes.

**4. Security and Permission Models are Under Stress**
Every major tool has at least one active permission bypass regression (Claude Code #26479, #36497; Gemini CLI #27576; Qwen Code #5055). The **tension between "autonomous agents" and "safe defaults" remains unresolved**. Expect industry-wide hardening in H2 2026.

**5. Long-Context Reliability Remains The Core Challenge**
Qwen Code (#5018), OpenCode (#30649), and Claude Code (#34556) all report attention degradation, token bloat, or memory loss

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-06-14 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Pull Requests attracted the most community discussion (sorted by comment volume).

| Rank | PR | Skill / Change | Status | Description & Discussion Highlights |
|------|----|----------------|--------|--------------------------------------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Open | Typographic quality control for AI-generated documents: orphan word wrap, widow paragraphs, numbering misalignment. Community noted these defects affect every document Claude produces – highly practical demand. |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT skill** (OpenDocument) | Open | Create, fill, read, and convert `.odt`/`.ods` files. Discussion centered on LibreOffice/ISO standard compliance and the need for robust template filling. |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design** (clarity overhaul) | Open | Revises the existing frontend-design skill for better actionability. Goal: every instruction must be executable within a single conversation. High interest from web developers. |
| 4 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer** + **skill-security-analyzer** | Open | Meta‑skills that evaluate other skills across structure, documentation, and security. Discussion highlighted the need for tooling to maintain ecosystem quality. |
| 5 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1-OSS predictor** | Open | Integrates SAP’s open‑source tabular foundation model for predictive analytics on business data. Interest from enterprise users; discussion around model size and deployment. |
| 6 | [#1140](https://github.com/anthropics/skills/pull/1140) | **agent-creator** meta‑skill | Open | Generates task‑specific agent sets, plus fixes for multi‑tool evaluation and Windows compatibility. Community sees this as a building block for composing workflows. |
| 7 | [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Open | Comprehensive testing skill covering unit, React component, integration, and E2E testing. Discussion focused on aligning with the Testing Trophy model and real‑world coverage. |
| 8 | [#147](https://github.com/anthropics/skills/pull/147) | **codebase-inventory-audit** | Open | 10‑step workflow for orphaned code, unused files, documentation gaps, and infrastructure bloat. Valued by maintenance teams for producing a single source of truth. |

---

## 2. Community Demand Trends

From the most active Issues, the community’s top unmet needs cluster into five areas:

- **Skill sharing and collaboration** ([#228](https://github.com/anthropics/skills/issues/228), 14 comments) – Users want org‑wide skill libraries and direct sharing links instead of manual file transfers.
- **Reliable skill evaluation** ([#556](https://github.com/anthropics/skills/issues/556), 12 comments; [#1169](https://github.com/anthropics/skills/issues/1169), 3 comments) – The `run_eval.py` script consistently reports 0% recall, making description optimization against noise. This is the ecosystem’s most critical bug.
- **Security and trust** ([#492](https://github.com/anthropics/skills/issues/492), 7 comments) – Community skills distributed under the `anthropic/` namespace create a trust‑boundary vulnerability. Users request namespace verification and permission scoping.
- **Governance for AI agents** ([#412](https://github.com/anthropics/skills/issues/412), 6 comments) – A dedicated “agent‑governance” skill for policy enforcement, threat detection, and audit trails is actively proposed.
- **Platform interoperability** ([#29](https://github.com/anthropics/skills/issues/29), 4 comments; [#16](https://github.com/anthropics/skills/issues/16), 4 comments) – Requests for AWS Bedrock support and exposing Skills as MCPs (Model Context Protocol) signal demand for multi‑platform portability.

Issues around duplicate skill installations ([#189](https://github.com/anthropics/skills/issues/189)) and Windows compatibility ([#1061](https://github.com/anthropics/skills/issues/1061)) also appear repeatedly.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon. They represent the next wave of community‑driven skills:

| PR | Skill | Why it may merge soon |
|----|-------|-----------------------|
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | Clear, pervasive problem; no competing PRs. |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT (OpenDocument) | Strong demand for LibreOffice compatibility; author actively responding. |
| [#83](https://github.com/anthropics/skills/pull/83) | skill-quality-analyzer / skill-security-analyzer | Meta‑skills that help maintain the whole collection; maintainer‑friendly. |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Enterprise interest; dedicated to a specific, well‑defined model. |
| [#1140](https://github.com/anthropics/skills/pull/1140) | agent-creator | Fixes several blocking evaluation bugs; ties into the “agentic” trend. |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | Addresses a gap in the skill collection; well‑structured and comprehensive. |
| [#361](https://github.com/anthropics/skills/pull/361) | YAML validation fixes (#361, #539) | Bug‑fixes for a core scripting tool (`quick_validate.py`); maintainers likely to accept. |
| [#1298](https://github.com/anthropics/skills/pull/1298) | run_eval.py recall fix | Directly fixes the #556 bug; multiple reproductions and a clear solution. |

---

## 4. Skills Ecosystem Insight

*The community’s most concentrated demand is for **infrastructure and quality‑of‑life skills** that improve the skill‑creation pipeline itself (validation, evaluation, security scanning) as well as **document‑format handling** (typography, ODT, DOCX) — reflecting a practical need to make Claude Code production‑ready in document‑heavy workflows.*

---

# Claude Code Community Digest — 2026-06-14

## Today's Highlights

No release happened in the last 24 hours, but the community remains highly active on long-standing pain points. The top-voted issue—a request to disable auto-attach in VS Code—continues to gather traction (159 👍, 52 comments), while a surge of reports around **memory persistence** and **permission bypass regressions** dominate the conversation. Persistent memory across context compactions remains the most demanded feature, with multiple open issues and user-built workarounds.

## Releases
*No new versions published in the last 24 hours.*

---

## Hot Issues

1. **[#24726 – VS Code: add setting to disable auto-attach of open file / selection](https://github.com/anthropics/claude-code/issues/24726)**  
   *Comments: 52 | 👍: 159*  
   The most upvoted open issue. Users want control over automatic file-context injection in the sidebar. The high reaction count signals strong consensus.

2. **[#34556 – Persistent Memory Across Context Compactions](https://github.com/anthropics/claude-code/issues/34556)**  
   *Comments: 43 | 👍: 3*  
   After 59 compactions, a user built their own memory persistence system. The issue calls for official hooks to avoid re-inventing the wheel—now cited by five related issues.

3. **[#36179 – Unsupported content type: redacted_thinking on Windows](https://github.com/anthropics/claude-code/issues/36179)**  
   *Comments: 27 | 👍: 18*  
   Frequent plugin errors on Windows with “redacted_thinking” content type. Impacts both VS Code extension and API, causing session interruptions.

4. **[#47166 – JetBrains plugin request](https://github.com/anthropics/claude-code/issues/47166)**  
   *Comments: 23 | 👍: 1*  
   Community asking for a proper Claude AI Assist plugin for JetBrains IDEs. Marked as duplicate of older request, but still generates discussion.

5. **[#47023 – Expose compact/session lifecycle hooks for external memory layers](https://github.com/anthropics/claude-code/issues/47023)**  
   *Comments: 22 | 👍: 4*  
   Proposal to expose hooks so users can integrate external memory stores without forking Claude Code. Directly addresses the #34556 pain point.

6. **[#60385 – Remote Control: MCP permission prompts never surface in web UI](https://github.com/anthropics/claude-code/issues/60385)**  
   *Comments: 19 | 👍: 0*  
   Critical for `--remote-control`: permission dialogs for non-read MCP tools only appear in the local TUI, blocking remote sessions.

7. **[#29937 – Terminal rendering corruption in tmux](https://github.com/anthropics/claude-code/issues/29937)**  
   *Comments: 17 | 👍: 38*  
   Text overlaps and overwrites in tmux sessions. Affects Linux users heavily, with a reliable reproducer provided.

8. **[#26479 – Agent Teams ignore bypassPermissions for Bash](https://github.com/anthropics/claude-code/issues/26479)**  
   *Comments: 12 | 👍: 14*  
   `bypassPermissions` mode works for the primary agent but not for teammates, breaking CI/CD use cases. Also fails to inherit project settings.

9. **[#36497 – `.claude/skills/` edits prompt permission despite being exempt (regression in 2.1.79)](https://github.com/anthropics/claude-code/issues/36497)**  
   *Comments: 9 | 👍: 11*  
   A regression that forces prompts for skills directory edits, contradicting documentation. Combined with #37253 and #53888 shows ongoing permission confusion.

10. **[#68285 – Workflow fan-out cost overrun of ~$1k](https://github.com/anthropics/claude-code/issues/68285)**  
   *Comments: 6 | 👍: 0*  
   A premium-tier default in workflow fan-out caused auto-purchased charges. Though the initial root cause was corrected, the issue highlights the need for per-agent cost ceilings.

---

## Key PR Progress

Only three pull requests were updated in the last 24 hours:

- **[#1 – Create SECURITY.md](https://github.com/anthropics/claude-code/pull/1)** (CLOSED)  
  A long-dormant administrative PR adding a security policy, finally resolved after more than a year.

- **[#68239 – Project-theme plugin for per-project theme settings](https://github.com/anthropics/claude-code/pull/68239)** (OPEN)  
  Adds a `SessionStart` hook that reads `theme` or `color` from `.claude/settings.json`. Closes #43216, which requested per-project persistent color/theme.

- **[#58673 – s](https://github.com/anthropics/claude-code/pull/58673)** (OPEN)  
  Minimal PR with a single character subject—likely a test or placeholder. Low activity in the PR queue suggests focus remains on bug triage rather than new feature merges.

---

## Feature Request Trends

The most-requested directions, distilled from open enhancement issues:

1. **Persistent Memory & External Memory Hooks**  
   Multiple issues (#34556, #47023, #46138, #32627) demand official APIs to persist state across context compactions. Users are already building custom solutions (3-tier markdown, knowledge graphs) and want lifecycle hooks to avoid forking.

2. **Improved IDE Integration**  
   #24726 (disable auto-attach), #47166 (JetBrains plugin), and #8504 (customize input highlighting) show demand for finer-grained control in editor extensions.

3. **Remote Control Parity**  
   #28379 (slash commands in remote UI) and #60385 (MCP permission surfacing) highlight gaps when driving Claude Code from web or mobile.

4. **Per-Project Theme / Personalization**  
   #43216 (now closed by PR #68239) and #59970 (disable microphone sound) indicate interest in UI customization.

5. **Parallel Task Spawning**  
   #68333 proposes non-interrupting parallel task creation—a UI pattern that many power users expect from modern AI coding tools.

---

## Developer Pain Points

Recurring frustrations from bug reports and community feedback:

- **Permission Bypass Inconsistencies**  
  `bypassPermissions` mode still prompts for `.claude/` files (#37253), skills directory (#36497), and Agent Team members (#26479). This erodes trust in the security model.

- **Terminal Rendering Issues**  
  tmux corruption (#29937) and CJK mojibake (#66269) degrade the TUI experience for non-English users. Workarounds exist (non-fullscreen renderer) but are not default.

- **Windows-Specific Failures**  
  Cowork lockups (#67780), OneDrive cross-device errors (#45178), and VM service issues (#64592) suggest the Windows desktop experience lags behind macOS/Linux.

- **Model Hallucinations & Confabulation**  
  #64048 and #67847 report models fabricating tool executions or results—a critical reliability concern for production use.

- **Data Loss**  
  File checkpointing stashing and resetting working tree (#68315) caused uncommitted edit loss. Combined with the Write-tool full-replacement default (#67917), users are wary of automatic state management.

- **Cost Surprises**  
  The workflow fan-out incident (#68285) highlights the need for transparent cost ceilings and default tier warnings, especially in auto-purchased scenarios.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-14

## Today’s Highlights

Two Rust‑based alpha releases (v0.140.0-alpha.18 and .19) landed today, narrowing the gap to the next stable CLI. A long‑running Windows sandbox bug ([#24391](https://github.com/openai/codex/issues/24391)) was finally closed after 52 comments, while a new wave of false‑positive cybersecurity safety checks ([#28015](https://github.com/openai/codex/issues/28015), [#27817](https://github.com/openai/codex/issues/27817)) drew attention for interrupting legitimate workflows. On the infrastructure side, a multi‑PR effort from @anp‑oai is bringing hermetic Windows process testing and remote‑environment path handling to production quality.

## Releases

Two pre‑release versions were published in the last 24 hours, both for the Rust‑based CLI (`rust-v0.140.0-alpha.18` and `rust-v0.140.0-alpha.19`). No detailed changelog was provided; these appear to be incremental alpha builds ahead of the 0.140.0 stable release.

## Hot Issues (10 noteworthy)

1. **[Issue #24391](https://github.com/openai/codex/issues/24391)** – [CLOSED] Windows sandbox: spawn setup refresh fails on Codex CLI 0.133.0  
   *52 comments, 26 👍*  
   A critical bug affecting Windows users after updating to 0.133.0. Fixed in today’s alpha releases after extensive community troubleshooting.

2. **[Issue #28015](https://github.com/openai/codex/issues/28015)** – [OPEN] False positive cybersecurity safety check blocks normal local repo maintenance  
   *15 comments*  
   Repeatedly flags DevOps tasks (e.g., checking branches, pruning) as security risks, interrupting paid sessions. Users call for better heuristics.

3. **[Issue #24428](https://github.com/openai/codex/issues/24428)** – [OPEN] Codex responds too slowly  
   *14 comments, 25 👍*  
   Latency increases, especially when falling back from WebSocket to SSE. Affects both CLI and Pi CLI. High community demand for performance improvements.

4. **[Issue #24246](https://github.com/openai/codex/issues/24246)** – [OPEN] macOS shows “Malware Blocked” alert for Codex helper  
   *11 comments, 9 👍*  
   System popup falsely identifying Codex helper as malware. Erratic occurrence; likely related to code signing or notarization issues.

5. **[Issue #20204](https://github.com/openai/codex/issues/20204)** – [OPEN] Inconsistent PreToolUse hook coverage across tool handlers  
   *10 comments, 1 👍*  
   Only shell, unified_exec, apply_patch, and MCP tools emit hook events; all other tools bypass the hook system, hindering custom workflows.

6. **[Issue #26158](https://github.com/openai/codex/issues/26158)** – [CLOSED] Windows sandbox regression in Codex CLI 0.138.0: os error 740  
   *10 comments, 5 👍*  
   Regression where `CreateProcessAsUserW` fails. Users rolled back to 0.132.0. Fixed in current alphas.

7. **[Issue #18896](https://github.com/openai/codex/issues/18896)** – [OPEN] macOS: Computer Use approval denied via MCP for every app  
   *8 comments, 1 👍*  
   Persistent denial of Computer Use control even after granting Screen Recording & Accessibility permissions. Suspected entitlement mismatch.

8. **[Issue #21134](https://github.com/openai/codex/issues/21134)** – [OPEN] Codex Desktop becomes unusable on long active threads  
   *5 comments*  
   Memory and TRACE log churn from large conversation state. Causes near‑freeze after extended sessions.

9. **[Issue #25431](https://github.com/openai/codex/issues/25431)** – [OPEN] Expose settings for spellchecking in app settings (Windows Desktop)  
   *4 comments, 13 👍*  
   Popular request to make spellcheck an optional toggle; currently forced on with no configuration.

10. **[Issue #28058](https://github.com/openai/codex/issues/28058)** – [OPEN] Regression: encrypted MultiAgentV2 messages remove readable task audit trail  
    *2 comments, 3 👍*  
    After merging message encryption for multi‑agent V2, users lose the ability to audit sub‑agent logs, a critical feature for debugging and compliance.

## Key PR Progress (10 important)

1. **[PR #28146](https://github.com/openai/codex/pull/28146)** – app‑server: preserve remote environment cwd  
   Fixes path rejection when a Windows cwd is targeted from a non‑Windows app‑server host, enabling remote Windows execution.

2. **[PR #28148](https://github.com/openai/codex/pull/28148)** – add managed Amazon Bedrock login and logout  
   Extends provider‑scoped auth to allow users to establish/remove Codex‑managed Bedrock credentials via RPC.

3. **[PR #28122](https://github.com/openai/codex/pull/28122)** – exec‑server honors remote environment cwd and shell  
   Supports passing a Windows cwd and native shell to the exec‑server, closing a gap for cross‑OS testing.

4. **[PR #27607](https://github.com/openai/codex/pull/27607)** (CLOSED) – Dedupe plugin MCPs by app declaration name  
   Prevents duplicate MCP servers when an app declares the same plugin as ChatGPT/SIWC, part of the plugin auth‑routing stack.

5. **[PR #27602](https://github.com/openai/codex/pull/27602)** – Preserve plugin apps in connector listings  
   Keeps plugin‑provided MCP servers visible in connector listings even after deduplication, improving discoverability.

6. **[PR #28118](https://github.com/openai/codex/pull/28118)** – feat(tui): add rate‑limit reset redemption to `/usage`  
   Lets CLI users view and redeem personal rate‑limit reset credits without leaving the terminal.

7. **[PR #28143](https://github.com/openai/codex/pull/28143)** – feat(app‑server): expose rate‑limit reset credits  
   Backend foundation for the TUI redemption flow; adds API for reading and redeeming reset credits.

8. **[PR #27953](https://github.com/openai/codex/pull/27953)** – Load app‑bundled internal hooks from Codex Desktop  
   Forces OpenAI‑bundled plugins to use hooks shipped with the Desktop app, hiding them from review UI while retaining telemetry.

9. **[PR #28131](https://github.com/openai/codex/pull/28131)** – Refresh SSH agent for app‑server proxy  
   Prevents stale `SSH_AUTH_SOCK` paths after the launching SSH session exits, fixing agent forwarding for long‑running app‑servers.

10. **[PR #28120](https://github.com/openai/codex/pull/28120)** – bazel: add PowerShell to Wine test harness  
    Adds an x86_64 PowerShell binary to the Bazel Wine environment, enabling more faithful cross‑OS testing of Windows shell scenarios.

## Feature Request Trends

- **Safety‑check improvements**: Multiple issues call for better classification of normal DevOps and finance‑related tasks to avoid false positive cybersecurity flags.
- **Side‑chat persistence**: Users want ephemeral side chats to be saved as child threads, surviving session restarts and app updates.
- **Customizable spellcheck**: A clear demand for on/off toggle for spellcheck in the Windows Desktop app (13 👍).
- **Hook system expansion**: Request for all tool handlers to emit `PreToolUse`/`PostToolUse` events, enabling richer custom automation.
- **Rate‑limit visibility**: Desire for accurate usage meters that start at 100% rather than 99%, and for easier access to reset credits.
- **Worktree UX**: Complaints about the worktree button being moved without notice; users request improved discoverability.

## Developer Pain Points

- **Windows sandbox fragility**: Two high‑profile regressions this month (sandbox setup refresh, os error 740) forced users to roll back and wait for fixes.
- **False‑positive safety gates**: Legitimate tasks (repo maintenance, personal finance) interrupted by security prompts, disrupting flow and wasting paid session time.
- **Performance degradation on long sessions**: Memory leaks and excessive logging in the Desktop app make extended use nearly impossible.
- **macOS permission friction**: Malware false alerts and persistent Computer Use denial degrade trust and require repeated manual intervention.
- **WSL integration breakage**: Path mangling (`/home` → `C:\home`), missing bundled CLI detection, and general instability after updates.
- **Lack of auditability after encryption**: Multi‑agent V2 encryption removed the readable task log, hampering debugging and compliance for advanced users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-14

## Today's Highlights

A security-focused day: a command injection vulnerability in `findCommand()` was patched, and a regex stack overflow in the `@`-command parser was fixed. Meanwhile, the backlog shows ongoing tension between agent autonomy and reliability—subagents falsely reporting success after hitting turn limits and the browser agent ignoring settings.json remain open. Auto Memory continues to generate a cluster of fix requests around redaction, retry logic, and patch validation.

## Releases

*None in the last 24 hours.*

## Hot Issues

1. **#27576 – Security: Command injection in findCommand via shell-interpolated execSync** [🔒]
   A confirmed injection vector in `ide-installer.ts`. Uses `execSync()` with string interpolation on both Unix and Windows. Two comments, no community reaction yet, but the associated PR was merged.
   *Why it matters:* Direct shell interpolation on untrusted command names is a classic supply-chain attack surface.
   [Link](https://github.com/google-gemini/gemini-cli/issues/27576)

2. **#22323 – Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption** [p1]
   A subagent terminates after hitting `MAX_TURNS` yet reports `status: "success"` and `Termination Reason: "GOAL"`. Two 👍 reactions; 6 comments. The community clearly feels this breaks trust in agent output.
   *Why it matters:* False-positive success signals make debugging downstream failures nearly impossible.
   [Link](https://github.com/google-gemini/gemini-cli/issues/22323)

3. **#25166 – Shell command execution gets stuck with "Waiting input" after command completes** [p1]
   Gemini hangs after executing trivial shell commands (e.g., `ls`), showing "Awaiting user input" indefinitely. Three 👍 reactions—indicating a widespread frustration.
   *Why it matters:* A core workflow (shell execution) becomes unusable without manual intervention.
   [Link](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **#27582 – Critical extension instability: freezing, crashing VS Code, edit failures, context blindness** [p2, closed as possible-duplicate]
   Multiple severe issues reported simultaneously: freezing VS Code, failing automated edits, ignoring file context, and chat duplication. Four comments, zero reactions—likely an outlier environment, but the symptom cluster is alarming.
   *Why it matters:* If reproducible, this would make the VS Code extension effectively broken for some users.
   [Link](https://github.com/google-gemini/gemini-cli/issues/27582)

5. **#3816 – Gemini CLI MCP client does not support resources or prompts from MCP servers** [closed]
   MCP servers expose three primitives (tools, resources, prompts), but the client only consumes tools. One 👍 reaction; 3 comments.
   *Why it matters:* Limits MCP ecosystem integration—users cannot leverage resource-driven or prompt-driven servers.
   [Link](https://github.com/google-gemini/gemini-cli/issues/3816)

6. **#24246 – Gemini CLI encounters 400 error with > 128 tools** [p2]
   A hard API limit when the agent discovers more than ~128 tools. Three comments; no reactions. The expected behavior is smarter scoping.
   *Why it matters:* Large MCP setups or custom skills will silently fail at the API boundary without clear diagnostics.
   [Link](https://github.com/google-gemini/gemini-cli/issues/24246)

7. **#21983 – Browser subagent fails on Wayland** [p1]
   The browser subagent terminates immediately with `GOAL` on Wayland display servers. One 👍; 4 comments.
   *Why it matters:* Wayland is the default on modern Linux distributions—this blocks a major agent capability for a significant user segment.
   [Link](https://github.com/google-gemini/gemini-cli/issues/21983)

8. **#26525 – Add deterministic redaction and reduce Auto Memory logging** [p2, 🔒]
   Secrets are sent to the model before redaction happens; the service also logs existing skill transcripts. Five comments; no reactions.
   *Why it matters:* A privacy and compliance risk—sensitive data may persist in logs and model context before any sanitization.
   [Link](https://github.com/google-gemini/gemini-cli/issues/26525)

9. **#26522 – Stop Auto Memory from retrying low-signal sessions indefinitely** [p2, 🔒]
   The extraction agent only marks a session as processed after a successful `read_file`. Low-signal sessions that are skipped remain unprocessed and are re-surfaced endlessly. Five comments.
   *Why it matters:* Wastes API calls and tokens on content the model already determined is not useful.
   [Link](https://github.com/google-gemini/gemini-cli/issues/26522)

10. **#27587 – Bug: /executeCommand SSE stream omits blank-line event delimiters** [p2, closed]
    The A2A server writes SSE with a single trailing `\n` instead of the spec-required `\n\n`. Three comments.
    *Why it matters:* Breaks all spec-compliant SSE clients; effectively a protocol compliance bug.
    [Link](https://github.com/google-gemini/gemini-cli/issues/27587)

## Key PR Progress

1. **#27575 – fix(security): prevent command injection in findCommand via safe spawnSync** [p2, size/m]
   Replaces `execSync` with `spawnSync`/`spawn` in two files, eliminating shell metacharacter injection. Closed.
   *Why it matters:* A direct security vulnerability that could allow arbitrary command execution.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27575)

2. **#27580 – fix(at-command): prevent stack overflow from regex backtracking on large inputs** [p1, size/m]
   Replaces a complex regex parser with an iterative scanner to prevent catastrophic backtracking. Closed.
   *Why it matters:* Large pasted inputs could crash the CLI—a denial-of-service vector.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27580)

3. **#27889 – fix(core): refresh MCP OAuth with stored client ID** [p1, size/m]
   Fixes OAuth refresh for auto-discovered MCP servers that lack a static `oauth.clientId` in settings. Open.
   *Why it matters:* Auto-discovered servers would fail on token refresh, breaking long-running MCP sessions.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27889)

4. **#27888 – fix(core): normalize MCP tool schemas to root type object** [p2, size/m]
   Adds a root `type: "object"` to tool schemas that omit it, fixing Vertex AI strict mode rejections. Open.
   *Why it matters:* Many MCP servers omit the root type; downstream APIs reject the schema as invalid.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27888)

5. **#27886 – fix(core): respect .gitignore and .geminiignore in session_context directory tree** [p2, size/s]
   Passes ignore rules into `getDirectoryContextString()`, previously missing them. Open.
   *Why it matters:* The `<session_context>` tree could expose ignored files (e.g., `node_modules`) to the model.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27886)

6. **#27887 – fix(cli): honor custom theme border.default when terminal reports OSC 11 background** [p2, size/m]
   Two code paths were preventing custom border colors from applying. Open.
   *Why it matters:* Documented theme feature was silently broken on most modern terminals.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27887)

7. **#27870 – fix(core): cap pending tool responses** [p1, size/m]
   Prevents a large tool result from being the pending `functionResponse` indefinitely. Open.
   *Why it matters:* Large MCP tool outputs could block subsequent tool calls or cause timeouts.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27870)

8. **#27878 – fix(core): sniff MCP image MIME types** [p1, size/l]
   Implements local binary signature sniffing for PNG, JPEG, GIF, and WebP to correct mis-declared MIME types. Open.
   *Why it matters:* Figma MCP was sending WebP as `image/png`, causing HTTP 400 from the Gemini API.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27878)

9. **#27885 – fix(vscode-ide-companion): register all activate() disposables** [p2, size/s]
   Two disposables were missing from `context.subscriptions`, causing a resource leak. Open.
   *Why it matters:* Silent memory leak in the VS Code extension could degrade editor performance over time.
   [Link](https://github.com/google-gemini/gemini-cli/pull/27885)

10. **#27711 – fix(core): add image-grounding hint in function response for image at…** [size/m, size/l]
    Adds a grounding hint when the model returns image-attributed function responses. Open.
    *Why it matters:* Improves image attribution accuracy in multi-modal agent workflows.
    [Link](https://github.com/google-gemini/gemini-cli/pull/27711)

## Feature Request Trends

**1. AST-aware codebase understanding (#22745, #22746)**
A recurring theme is that the CLI's file reading and codebase mapping are too naive. Investigators are tracking whether AST-aware reads (method bounds, type-aware search) could reduce turn count and token waste.

**2. Robust component-level evaluations (#24353)**
A major EPIC tracking 76+ behavioral eval tests across 6 Gemini models. The community is pushing for a formal evaluation infrastructure that goes beyond end-to-end tests and drills into sub-agent, tool-use, and memory interactions.

**3. Better tool & skill governance (#24246, #22672, #21968)**
Multiple requests for the agent to:
- Limit active tools when the count exceeds API constraints
- Understand that some operations (git reset, force pushes, DB mutations) are destructive
- Proactively use custom skills without explicit user instruction

**4. Enhanced browser agent resilience (#22232, #22267)**
Users want the browser subagent to:
- Respect `settings.json` overrides (e.g., `maxTurns`)
- Handle orphaned browser profiles gracefully instead of failing fast
- Support automatic session takeover

## Developer Pain Points

**Agent autonomy vs. reliability.** Subagents ignore configuration, falsely report success after failure, and run without user permission. The community is frustrated that "smart" defaults override explicit settings.

**Security and data exposure.** Command injection in core utilities (#27576), secrets sent to the model before redaction (#26525), and sensitive data in logs—all erode trust in the CLI for production use.

**Shell integration fragility.** The CLI hangs after trivial commands (#25166), corrupts backslash-terminated history (#27585), and crashes on certain output hook patterns (#22186). The shell is a primary interaction surface, and these bugs block daily use.

**MCP ecosystem friction.** Limited MCP client capabilities (no resources/prompts), schema validation failures, mis-declared MIME types, and OAuth refresh issues—MCP is a priority feature but still rough around the edges.

**Auto Memory inefficiency.** The memory system retries low-signal sessions indefinitely (#26522), patches are silently invalid (#26523), and redaction is post-hoc rather than pre-emptive (#26525). This wastes tokens and risks privacy leaks.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-14

## Today’s Highlights
Two minor releases landed (v1.0.62 and v1.0.62-2) with notable UX improvements—dialogs now scroll in sync with the timeline, and the diff view gains content search with `n`/`N` navigation. On the community front, a long‑standing issue about missing AI models (Gemini, Raptor mini, Goldeneye) was finally closed, while new feature requests for Ollama API‑key support and preloaded MCP tools signal a growing appetite for local and custom model integration.

## Releases
Two versions were published on 2026-06-13:

### v1.0.62
- **Ask/elicitation dialogs** now scroll together with the timeline instead of overlaying the screen; users can scroll up to read earlier agent output and back down to the dialog.
- Blank lines are preserved between reasoning summary sections.
- Minor fix: “Show user‑ty” (likely a truncated changelog entry; see release notes for full details).

### v1.0.62-2
- **Plugins** can now ship extensions, making them installable via the plugin marketplace.
- **Diff view** adds content search, match highlighting, and `n`/`N` navigation.
- New **`/app`** slash command opens the GitHub app (or a browser fallback).
- **Subagent model, reasoning effort, and context** can now be configured.

---

## Hot Issues (5 items)
*Only 5 issues were updated in the last 24h. All are covered below.*

| # | Title & Link | Status | Why It Matters | Community Reaction |
|---|--------------|--------|----------------|-------------------|
| #2550 | [Not all models are available from Copilot](https://github.com/github/copilot-cli/issues/2550) | **CLOSED** | Users reported that Gemini, Raptor mini, and Goldeneye models weren’t listed in `/model`, despite being documented as supported. The closure suggests a fix or clarification has been applied. | 4 comments, 6 👍 – high engagement; closed after ~2 months. |
| #3788 | [Invalid issue (#3788)](https://github.com/github/copilot-cli/issues/3788) | **CLOSED** | Empty bug report (no description, steps, or version). Likely spam or accidental creation. | 1 comment, 0 👍 – no impact. |
| #3789 | [Request: Ollama API Key return to Bring Your Own Model](https://github.com/github/copilot-cli/issues/3789) | **OPEN** | User wants to use a remote Ollama server with an API key in the BYOM menu. Currently only local connections are straightforward. | No comments yet – early request, but aligns with growing self‑hosted model interest. |
| #3787 | [Preload MCP server tools into the initial agent function list](https://github.com/github/copilot-cli/issues/3787) | **OPEN** | MCP tools are lazy‑loaded, causing agents that don’t know to probe for them to miss them entirely. Preloading would make them visible from session start. | 0 comments – a technical design request from a power user. |
| #3785 | [Clarify/support .copilotignore semantics in Copilot CLI](https://github.com/github/copilot-cli/issues/3785) | **OPEN** | Nested `.copilotignore` files are not well‑documented or working as expected in the CLI. This is a subset of a broader SDK issue. | 0 comments – mirrors wider demand for consistent ignore‑file behavior. |

---

## Key PR Progress
No pull requests were updated in the last 24 hours.

---

## Feature Request Trends
- **Bring Your Own Model (BYOM) extension**: Issue #3789 requests API‑key support for Ollama to enable remote model hosting. This echoes earlier requests for flexibility in model sourcing.
- **MCP tool preloading**: Issue #3787 asks for eager discovery of MCP tools instead of lazy loading—a sign that agent interoperability is becoming a priority for advanced users.
- **`.copilotignore` semantics**: Issue #3785 seeks clearer documentation and support for nested ignore files; similar requests appear in the broader Copilot SDK ecosystem.

---

## Developer Pain Points
- **Missing models**: Issue #2550 (now closed) highlighted that several documented models (Gemini, Raptor mini, Goldeneye) were not visible in the CLI. The closure suggests a fix, but users may need to verify.
- **Empty/invalid issues**: Issue #3788 (blank report) is a minor nuisance but indicates a need for better issue‑template enforcement.
- **Configuration friction**: The `.copilotignore` ask (#3785) and the need for environment‑variable driven API keys (#3789) point to ongoing friction when customizing Copilot CLI behaviour for local setups.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-14

## Today's Highlights
A batch of three stability-focused PRs merged, addressing MCP connection error suppression, double‑encoded JSON in tool calls, and a missing timeout for the OpenAI client. Meanwhile, a fresh screen‑width crash in the TUI (#2450) was opened, and an older file‑reading loop bug (#640) remains active after six months with no resolution. No new releases were published.

## Releases
*None in the last 24 hours.*

## Hot Issues
*(Only two issues were updated in the last 24h. All are listed.)*

| Issue | Summary | Why It Matters |
|-------|---------|----------------|
| [#640](https://github.com/MoonshotAI/kimi-cli/issues/640) – [bug] Kimi CLI stuck in reading one file again and again and stuck in a loop | User on Arch Linux using a custom Anthropic endpoint reports infinite file‑reading cycle with `0.76` and `mimo-v2-flash`. 13 comments, 1 👍. | Long‑standing (since Jan 2026) with no fix merged. Indicates a potential deadlock or stdin handling issue that affects headless/automated workflows. Community engaged but no clear resolution path. |
| [#2450](https://github.com/MoonshotAI/kimi-cli/issues/2450) – [bug] Uncaught Pi TUI exception due to screen width | On Debian with `kimi-code v0.12.0` and `k2.6` model, the TUI crashes when terminal width is too narrow. No comments yet. | Fresh report highlighting missing boundary checks in the TUI rendering loop. Could affect users in constrained terminal environments (e.g., CI, small panes). |

## Key PR Progress
*(All PRs updated in the last 24h are covered, 5 total.)*

| PR | Status | Description |
|----|--------|-------------|
| [#2324](https://github.com/MoonshotAI/kimi-cli/pull/2324) – fix(web): handle BrokenPipeError in SessionProcess.send_message | **Open** | Guards `process.stdin.drain()` against subprocess exit during write. Fixes a race condition in the web runner that could cause silent failures. |
| [#2434](https://github.com/MoonshotAI/kimi-cli/pull/2434) – fix: suppress MCP connection errors and handle LLM double‑serialization | **Merged** | Three fixes: (1) suppresses noisy MCP connection errors in telemetry, (2) handles double‑serialized `function.arguments` from LLMs, (3) ensures clean event loop teardown after MCP drops. |
| [#2407](https://github.com/MoonshotAI/kimi-cli/pull/2407) – fix: handle double‑encoded JSON in tool call arguments (Moonshot API) | **Merged** | Fixes [#2406](https://github.com/MoonshotAI/kimi-cli/issues/2406) where Moonshot API returns nested JSON strings inside `function.arguments`. Previously caused Pydantic validation failures for tools like `SetTodoList`. |
| [#2409](https://github.com/MoonshotAI/kimi-cli/pull/2409) – fix(kosong): add default 120s timeout to create_openai_client | **Merged** | Replaces the default 600s timeout with 120s to avoid long hangs when upstream proxies (e.g., MiMo) timeout earlier. |
| [#2449](https://github.com/MoonshotAI/kimi-cli/pull/2449) – fix(string): strip newlines in shorten_middle before the length check | **Open** | Ensures `shorten_middle` collapses newlines before truncation, fixing garbled single‑line summaries of tool‑call key arguments. |

## Feature Request Trends
Based on recent issues and PRs, the community is prioritizing:
- **Better MCP server resilience** – connection drops, error suppression, and clean shutdown are recurring themes.
- **Improved error handling in TUI** – screen‑width crashes and uncaught exceptions need better guardrails.
- **Timeout configurability** – the default OpenAI client timeout is too long for many proxy setups; users want control.

## Developer Pain Points
- **Stalled old bugs** – Issue #640 (infinite file read loop) has zero activity from maintainers since January, frustrating users on niche platforms.
- **Double‑encoded JSON** – A recurring issue with Moonshot API’s `function.arguments` forced three PRs in the last two weeks; developers demand more consistent API responses.
- **Missing edge‑case handling** – TUI screen‑width crashes, the `BrokenPipeError` race, and newline‑insensitive string truncation all point to insufficient testing on real‑world terminal/pipe environments.
- **Default timeout too aggressive** – The fix from #2409 (120s vs 600s) shows that users frequently hit proxy timeouts; community wants knobs for both connect and read timeouts.

---

**Next digest:** 2026-06-15. Stay tuned for more updates from the MoonshotAI/kimi-cli repository.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-06-14

## Today's Highlights
Two patch releases landed (v1.17.5 / v1.17.6) with MCP compatibility fixes and Snowflake OAuth support. The community is increasingly focused on MCP ecosystem completeness—requests and PRs for client roots, tool error routing, and OAuth callback handling dominate the board. A major "Cedric" multi-tab workspace PR and a new native `/goal` feature signal the project is moving toward richer session management and UI ergonomics.

## Releases

### v1.17.6
- **Core – Bugfixes:** Declared OpenCode's supported MCP client capabilities to improve MCP server compatibility.  
  [GitHub Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.6)

### v1.17.5
- **Core – Improvements:** Added external browser OAuth for the Snowflake Cortex provider (@santigc6); improved project copy management and move-session flows in v2.
- **Core – Bugfixes:** Recovered expired MCP sessions instead of leaving MCP tools disconnected; cleared closed MCP clients to prevent stale connections.  
  [GitHub Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.5)

## Hot Issues (10 Notable)

1. **[OPEN] #28567 – Full MCP client capabilities**  
   *20 👍, 6 comments*  
   Community is demanding parity with the latest MCP standard—specifically roots, sampling, and notifications. This is the most-upvoted open feature request.  
   [Issue #28567](https://github.com/anomalyco/opencode/issues/28567)

2. **[CLOSED] #4240 – No native Zed changes review support**  
   *19 👍, 16 comments*  
   Users migrating from Gemini CLI to OpenCode miss the ability to review changes inside Zed. The high engagement suggests this is a critical gap for Zed-native workflows.  
   [Issue #4240](https://github.com/anomalyco/opencode/issues/4240)

3. **[CLOSED] #1865 – Auto-save session records to disk**  
   *12 comments*  
   A long-standing feature request for session persistence, comparable to Claude Code's autosave. Closed but still referenced by the community.  
   [Issue #1865](https://github.com/anomalyco/opencode/issues/1865)

4. **[OPEN] #28957 – "Upstream idle timeout exceeded" with writing-plans skill**  
   *12 comments*  
   A session-level timeout on macOS Tahoe (Apple M4) when using the "writing-plans" skill. Users report the model service connection idles out without recovery.  
   [Issue #28957](https://github.com/anomalyco/opencode/issues/28957)

5. **[CLOSED] #32231 – "Option to Start Terminal" removed**  
   *4 comments*  
   A quick regression in v1.17.x—the CLI/Terminal option disappeared from the UI. Closed quickly after community noise.  
   [Issue #32231](https://github.com/anomalyco/opencode/issues/32231)

6. **[OPEN] #21090 – Model tried to call unavailable tool**  
   *5 👍, 6 comments*  
   A fundamental usability pain: users cannot get the model to analyze codebases without manual copy-paste. Indicates tool routing issues for basic file operations.  
   [Issue #21090](https://github.com/anomalyco/opencode/issues/21090)

7. **[CLOSED] #32252 – Built-in skill 'customize-opencode' not resolvable**  
   *2 comments*  
   The skill is declared in system prompts but the `skill` tool fails to load it. A clear declaration/resolution mismatch.  
   [Issue #32252](https://github.com/anomalyco/opencode/issues/32252)

8. **[OPEN] #30649 – Unbounded token growth via cache.read**  
   *3 comments*  
   Long-running sessions accumulate `tokens.cache.read` without bound, leading to unrecoverable context-window errors. A critical reliability issue for heavy users.  
   [Issue #30649](https://github.com/anomalyco/opencode/issues/30649)

9. **[OPEN] #23595 – `<system-reminder>` moving breaks llama.cpp caching**  
   *8 👍, 2 comments*  
   OpenCode moves the system reminder position in the prompt, invalidating KV caches on llama.cpp and causing massive reprocessing overhead.  
   [Issue #23595](https://github.com/anomalyco/opencode/issues/23595)

10. **[CLOSED] #32248 – Cache/sessions persist after `opencode uninstall` on Windows**  
    *1 comment*  
    Users expecting a clean uninstall find sessions and cache remain. Points to inadequate cleanup logic in the Windows desktop build.  
    [Issue #32248](https://github.com/anomalyco/opencode/issues/32248)

## Key PR Progress (10 Important)

1. **#32230 – MCP client roots support (CLOSED)**  
   Advertises the `roots` capability and handles `roots/list` with the project directory. A foundational step toward full MCP client parity.  
   [PR #32230](https://github.com/anomalyco/opencode/pull/32230)

2. **#32239 – Native `/goal` with persisted per-session goals (CLOSED)**  
   Adds a full goal system: active/paused/completed status, optional token budget, and usage accounting via REST API. Implements a long-requested productivity feature.  
   [PR #32239](https://github.com/anomalyco/opencode/pull/32239)

3. **#32235 – Cedric multi-tab workspace release (CLOSED)**  
   A major UI overhaul: browser, file, code, markdown, terminal, and side chat in tabs; background tasks lifecycle; persisted snapshots; and context handoffs.  
   [PR #32235](https://github.com/anomalyco/opencode/pull/32235)

4. **#29132 – Await event loop in non-interactive run (CLOSED)**  
   Fixes `opencode run --format json` exiting before the event loop completes. Critical for CI/CD and automation pipelines.  
   [PR #29132](https://github.com/anomalyco/opencode/pull/29132)

5. **#32193 – Fix mentions for files in hidden folders (OPEN)**  
   Users could not `@mention` files or folders starting with `.`. Fix adds hidden folder support to the mention resolver.  
   [PR #32193](https://github.com/anomalyco/opencode/pull/32193)

6. **#32238 – Avoid search retention for file reads (OPEN)**  
   Prevents repeated file reads from retaining and re-initializing search state—fixes a performance regression in the file explorer.  
   [PR #32238](https://github.com/anomalyco/opencode/pull/32238)

7. **#32244 – Handle MCP tool result errors (OPEN)**  
   Routes `CallToolResult.isError` through the AI SDK error path, surfacing structured diagnostics when MCP tools fail.  
   [PR #32244](https://github.com/anomalyco/opencode/pull/32244)

8. **#32242 – Escape OAuth callback errors (OPEN)**  
   Sanitizes provider-controlled OAuth error messages before rendering HTML—fixes an XSS vector in the MCP OAuth flow.  
   [PR #32242](https://github.com/anomalyco/opencode/pull/32242)

9. **#32243 – Use SDK protocol version in debug (OPEN)**  
   Aligns the manual debug initialize probe with the latest MCP SDK protocol version, reducing false negatives during MCP server debugging.  
   [PR #32243](https://github.com/anomalyco/opencode/pull/32243)

10. **#32254/#32255 – Unify PostgreSQL/SQLite schemas via dialect shim (OPEN)**  
    Introduces a dialect shim pattern to eliminate duplicate `.pg.ts` files. A compliance-tagged refactor for multi-database backend support.  
    [PR #32254](https://github.com/anomalyco/opencode/pull/32254) | [PR #32255](https://github.com/anomalyco/opencode/pull/32255)

## Feature Request Trends

- **MCP Ecosystem Parity:** The dominant theme. Users want full MCP client capabilities (roots, sampling, notifications) and better error handling/reporting when MCP tools fail.
- **Zed Editor Deep Integration:** Native changes review (#4240) and FIM support for `edit_predictions` (#26911) are repeatedly requested.
- **Session Autosave & Persistence:** Automatic session recording (#1865) and per-session goals (#27167, now implemented in #32239) reflect a desire for durable, inspectable work traces.
- **New Model Providers & Models:** Requests for GLM-5.2 (Z.AI), configurable OpenRouter Fusion presets, and Kimi K2.7 model name corrections show community is actively testing newer models.
- **TUI & UI Modernization:** RTL support (#32247), tiled session panels (#32214), and the Cedric workspace PR (#32235) indicate demand for a more flexible, accessible desktop experience.

## Developer Pain Points

- **MCP Instability & Stale Connections:** Recurring reports of disconnected MCP sessions, unavailable tools, and idle timeouts (#28957, #21090, v1.17.5 changelog). The MCP experience still feels fragile.
- **Context Window Bloat:** Unbounded token growth via `cache.read` (#30649) and `<system-reminder>` repositioning that breaks KV caches (#23595) make long sessions unreliable.
- **Windows & Cross-Platform Gaps:** UNC path issues with WSL (#19473), cache persistence after uninstall (#32248), certificate errors in desktop but not TUI (#32250) – Windows users face friction.
- **Skill Resolution Failures:** Built-in skills sometimes declared but not resolvable (#32252), highlighting a mismatch between prompt construction and skill loading logic.
- **UI Regressions & Missing UX:** The removal of the terminal start option (#32231), missing agent picker in v2 layout (#30360), and Vim keybinding hardcoding (#32198) frustrate power users who rely on consistent UI.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-14

## Today’s Highlights
Patch release **v0.79.3** fixes a critical billing hazard for OpenAI GPT‑5.4/5.5 users: the context‑window metadata now correctly reflects the 272k‑token Codex backend limit, preventing cost spikes from oversize prompts. Meanwhile, a high‑impact cache‑retention bug for Anthropic Claude models was identified and closed (issue #5703), and a major dependency‑duplication problem caused by Shrinkwrap (#5653) continues to draw community attention.

## Releases
**v0.79.3** — [Release Notes](https://github.com/earendil-works/pi/releases/tag/v0.79.3)  
- **Fixed:** Inherited OpenAI GPT‑5.4/‑5.5 and Codex model context‑window metadata now use the observed 272k‑token Codex backend limit. This avoids billing spikes from prompts that exceed Codex’s accepted limit (reported by [@trethore](https://github.com/trethore)).

---

## Hot Issues (10 most noteworthy)

1. **[#5703 – Inprogress, Closed]** Fix(ai): 1h cache retention silently degraded to 5m for Claude models, inflating Anthropic cache costs  
   *Pi sets `cache_control.ttl: "1h"` but never sends the required `extended-cache-ttl-2025-04-11` beta header.*  
   **Why it matters:** Directly impacts operational cost for every Claude user. 8 comments, quickly resolved.  
   [Issue #5703](https://github.com/earendil-works/pi/issues/5703)

2. **[#5653 – Open]** Move off Shrinkwrap  
   *Installing both `pi-ai` and `pi-coding-agent` as direct deps results in two identical copies on disk because of module‑level `Map` for the API provider registry.*  
   **Why it matters:** Fundamental dependency management problem that breaks provider discovery. 7 comments, high priority.  
   [Issue #5653](https://github.com/earendil-works/pi/issues/5653)

3. **[#5644 – Closed]** GPT 5.5 in API/Codex has incorrect context window size  
   *Claims 400K for Codex and 1M for API, but Pi uses wrong default. Blocks adoption of the latest models.*  
   **Why it matters:** Users cannot take full advantage of the new GPT‑5.5. 6 comments.  
   [Issue #5644](https://github.com/earendil-works/pi/issues/5644)

4. **[#3627 – Closed]** Expose timeout and retry settings on OpenAI providers  
   *Currently defaults to 10‑minute timeout, making it unusable with slower local inference.*  
   **Why it matters:** Long‑standing request (2 👍) affecting everyone running local models via OpenAI‑compatible endpoints. 6 comments.  
   [Issue #3627](https://github.com/earendil-works/pi/issues/3627)

5. **[#5571 – Closed]** `pi -p` hangs indefinitely with unauthenticated default provider  
   *No credentials → hangs 3+ minutes instead of failing fast.*  
   **Why it matters:** Terrible first‑run UX. Makes fresh installations frustrating. 5 comments.  
   [Issue #5571](https://github.com/earendil-works/pi/issues/5571)

6. **[#5702 – Closed]** `prompt_cache_retention` sent to providers that reject it (OpenCode/Zen 400)  
   *Sending unsupported parameter causes request failures; also raises maintainability concerns in `generate‑models.ts`.*  
   **Why it matters:** Breaks compatibility with alternative providers. 4 comments.  
   [Issue #5702](https://github.com/earendil-works/pi/issues/5702)

7. **[#5671 – Open]** `~/.pi` and `cwd/.pi` overlap  
   *Global and project‑local settings share the same directory name under `$HOME`, causing potential confusion.*  
   **Why it matters:** Design concern raised by core contributor. 4 comments, 2 👍.  
   [Issue #5671](https://github.com/earendil-works/pi/issues/5671)

8. **[#5685 – Closed]** Pressing Escape does not stop subagent/background agent  
   *ESC should cancel, but subagent continues running.*  
   **Why it matters:** Control flow broken for multi‑agent workflows. 4 comments.  
   [Issue #5685](https://github.com/earendil-works/pi/issues/5685)

9. **[#5597 – Closed]** TUI crash: Box.render fails when child component is undefined  
   *`Box.render` throws `TypeError: Cannot read properties of undefined (reading 'render')`.*  
   **Why it matters:** Unhandled crash kills the process. 3 comments.  
   [Issue #5597](https://github.com/earendil-works/pi/issues/5597)

10. **[#5463 – Open]** Auto‑compaction after final turn throws error  
    *`agent.continue()` fails with “Cannot continue from message role: assistant” after normal turn.*  
    **Why it matters:** 5 👍, points to a deeper state‑management bug. 2 comments.  
    [Issue #5463](https://github.com/earendil-works/pi/issues/5463)

---

## Key PR Progress (all 10 PRs updated in last 24h)

1. **[#5526 – Open]** Require terminal events for OpenAI Responses streams  
   *Fixes random streaming stops by ensuring OpenAI Responses streams end with a terminal event.*  
   [PR #5526](https://github.com/earendil-works/pi/pull/5526)

2. **[#5708 – Open]** Wrap question extension text instead of truncating  
   *Closes #5707 – improves readability of question extensions in the TUI.*  
   [PR #5708](https://github.com/earendil-works/pi/pull/5708)

3. **[#5701 – Closed]** Fix Minimax‑M3 context size (1M → 524288)  
   *Corrects maximum context length based on OpenRouter error.*  
   [PR #5701](https://github.com/earendil-works/pi/pull/5701)

4. **[#5704 – Closed]** Feat: add capture system for auto‑storing tool results  
   *Implements the Capture phase of Veil context management – auto‑caches Read, Bash, WebSearch results with deduplication.*  
   [PR #5704](https://github.com/earendil-works/pi/pull/5704)

5. **[#5693 – Closed]** Merging official repo updates  
   *Regular upstream sync.*  
   [PR #5693](https://github.com/earendil-works/pi/pull/5693)

6. **[#5690 – Closed]** Feat: add configurable chat‑template thinkingFormat for vLLM‑hosted models  
   *Adds `thinkingFormat: "chat-template"` for OpenAI‑compatible providers behind vLLM/LiteLLM.*  
   [PR #5690](https://github.com/earendil-works/pi/pull/5690)

7. **[#5262 – Open]** Feat: add Anthropic Vertex provider  
   *Native Claude on Google Cloud Vertex AI support using existing Anthropic streaming infrastructure.*  
   [PR #5262](https://github.com/earendil-works/pi/pull/5262)

8. **[#5688 – Closed]** Fix(deps): force safe esbuild resolution  
   *Ensures transitive `esbuild` is pinned above patched version `0.28.1`.*  
   [PR #5688](https://github.com/earendil-works/pi/pull/5688)

9. **[#5640 – Closed]** Feat: paste clipboard images via Ctrl+V on Windows terminal  
   *Windows terminal swallows Ctrl+V; adds image‑paste support using Alt+V and Win32 API alternative.*  
   [PR #5640](https://github.com/earendil-works/pi/pull/5640)

10. **[#5665 – Closed]** Fix: handle `setActiveTools(undefined)` restoring all tools  
    *Prevents `TypeError: toolNames is not iterable` when called with `undefined`.*  
    [PR #5665](https://github.com/earendil-works/pi/pull/5665)

---

## Feature Request Trends

- **Multi‑session management** (#5700, #5685): Users want to run multiple concurrent agent sessions and switch between them in the TUI without teardown.
- **Custom slash commands** (#289): Extend the command system beyond LLM communication to include UI, logic, and permission‑based actions.
- **Context control for custom messages** (#5654): Add `excludeFromContext` flag to custom messages, mirroring existing bash‑execution behaviour.
- **Official core extensions & marketplace** (#5686): Request for curated productivity features, ratings, and categorization in the extension marketplace.
- **Performance monitoring** (#5684): Real‑time token‑per‑second display in the status bar, especially valuable for local model users.
- **Configurable timeout/retry** (#3627): Expose low‑level HTTP settings for OpenAI‑compatible providers to support slow local inference.

---

## Developer Pain Points

- **Billing hazards and model parameter mismatches** – Repeated issues with incorrect context windows (GPT‑5.5, Minimax‑M3) and cache‑retention headers (Anthropic) that silently inflate costs or cause request failures.
- **Dependency duplication and discovery failures** – The Shrinkwrap problem (#5653) and semver‑range package loading (#5695) create confusion and break provider resolution.
- **Hanging and silent failures** – Commands like `pi -p` with missing credentials (#5571) and `pi list`/`pi update` when an MCP server runs (#5687) hang indefinitely without error.
- **TUI stability** – Crashes from undefined children (#5597) and state‑management errors after auto‑compaction (#5463) disrupt long sessions.
- **Tool argument validation gaps** – JSON‑encoded strings are not coerced to arrays/objects (#5697), causing intermittent failures with MCP tools.
- **Inconsistent model parameter handling** – Missing `thinkingLevelMap.off` on DeepSeek models (#5699) and uppercase header values being treated as env‑var references (#5661) demonstrate validation gaps in the model registry.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-14

## Today's Highlights

The Qwen Code project continues active development with **no new releases** in the last 24 hours but significant PR and Issue activity. The most notable development is the **first half of Dynamic Workflows phase P4** (PR #5094) landing on `main`, bringing the project closer to parity with Claude Code 2.1.160's multi-agent execution model. Meanwhile, the **v0.18.0 nightly release pipeline failed** on June 14 (Issue #5092), and a **long-standing Windows CRLF handling fix** for paste in passthrough mode (PR #1456) was finally merged after months, indicating the project is clearing technical debt. Community attention remains focused on **long-context performance degradation** and **authentication configuration confusion** across providers.

---

## Releases
None.

---

## Hot Issues (10 Selected)

1. **#3203 — Qwen OAuth Free Tier Policy Adjustment**  
   Proposal to slash the daily free quota from 1,000 to 100 requests/day and eventually phase out the free tier. With **129 comments**, this is the most-discussed issue this week. The community is sharply divided: some advocate for a sustainable business model, others fear it will kill small-scale experimentation. [Link](https://github.com/QwenLM/qwen-code/issues/3203)

2. **#5083 — TUI Freeze Due to Zombie Child Process**  
   A critical `P2` bug where the TUI becomes completely unresponsive because a zombie `bash` child process is never reaped. Diagnosis includes a zombie process lasting ~4 minutes. This directly impacts developer productivity in long sessions. [Link](https://github.com/QwenLM/qwen-code/issues/5083)

3. **#4845 — `/import-config` for Claude User Config Migration**  
   A feature request (with `welcome-pr` tag) to allow one-click migration of MCP servers, instructions, permissions, and custom commands from Claude Code/Desktop to Qwen Code. High-value for tool-switchers. [Link](https://github.com/QwenLM/qwen-code/issues/4845)

4. **#5018 — Long-Context Attention Degradation**  
   A recurring complaint: during long-running tasks, the model suffers "massive forgetting" and attention loss. The reporter explicitly requests "strengthened long-range task focus." This is a sign that the current model's context window management still underperforms in practical coding agents. [Link](https://github.com/QwenLM/qwen-code/issues/5018)

5. **#5055 — False Positive Trojan Detection in VSCode Extension**  
   Antivirus flags the VSCode extension `0.18.0` as `Trojan:JS/ShaiWorm.DBA!MTB`. Tagged `P1/security` — a serious trust-damaging issue if not resolved quickly. Community expects a signed or clean build. [Link](https://github.com/QwenLM/qwen-code/issues/5055)

6. **#5080 — 401 Error When Mixing Standard API Key with Token Plan Endpoint**  
   Configuring a standard API key (`sk-xxx`) and then selecting a Token Plan provider causes a 401. The root cause is that provider identity and protocol are conflated in the current architecture. PR #5089 directly addresses this. [Link](https://github.com/QwenLM/qwen-code/issues/5080)

7. **#5064 — Status Line Overflow: No Word Wrap**  
   When the CLI statusline exceeds available terminal width, content is truncated or overlapped. A small but persistent UX pain point that PR #5093 now fixes. [Link](https://github.com/QwenLM/qwen-code/issues/5064)

8. **#5075 — Plan Gate Error on ExitPlanMode**  
   Exiting planning mode causes a gate failure that only shows a partial plan summary instead of the full plan. This disrupts a core workflow for developers relying on the planning/agent loop. [Link](https://github.com/QwenLM/qwen-code/issues/5075)

9. **#5007 — ACP Mode Does Not Expose Skills from `~/.qwen/skills`**  
   When using Qwen Code through ACP mode (e.g., from Zed), custom skills installed in the user directory are invisible. This limits extensibility for IDE-integrated workflows. [Link](https://github.com/QwenLM/qwen-code/issues/5007)

10. **#5019 — Repetitive Tool Calls in Long-Running Tasks**  
    The model repeatedly calls the identical tool with the same arguments, triggering `400: Repetitive tool calls detected` and terminating the session. This is a critical performance and reliability blocker for long-term agents. [Link](https://github.com/QwenLM/qwen-code/issues/5019)

---

## Key PR Progress (10 Selected)

1. **#5094 — feat(core): Workflow P4a — extractAndStripMeta + meta on RunOutcome**  
   Lands the first half of Dynamic Workflows phase P4, adding meta-extraction logic. Built on merged P1–P3, this brings the project significantly closer to Claude Code parity. [Link](https://github.com/QwenLM/qwen-code/pull/5094)

2. **#5089 — refactor(core): extract Protocol enum and decouple model identity from auth type**  
   A draft PR that separates `protocol` (OPENAI/GEMINI/ANTHROPIC/QWEN_OAUTH) from `providerId`. Directly addresses the 401 confusion in Issue #5080 and enables custom provider support. [Link](https://github.com/QwenLM/qwen-code/pull/5089)

3. **#5093 — fix(cli): wrap long status lines**  
   A clean fix for Issue #5064: long status lines now wrap instead of being truncated, with a cap on rendered lines. [Link](https://github.com/QwenLM/qwen-code/pull/5093)

4. **#5088 — feat(web-shell): reveal full tool detail and auto-collapse finished tools**  
   Improves web-shell transcript readability by removing the 120-char hard cap on tool descriptions and auto-collapsing completed tools. [Link](https://github.com/QwenLM/qwen-code/pull/5088)

5. **#1456 — fix(cli): treat CRLF as paste in passthrough mode**  
   After five months, this Windows paste fix for stdin passthrough mode is finally merged. Treats standalone `\r\n` as a paste event to prevent accidental submits during multi-line pastes. [Link](https://github.com/QwenLM/qwen-code/pull/1456)

6. **#5085 — fix(acp): add internal Kind.Agent, keep ACP wire on 'other'**  
   Gives the sub-agent tool its own `Kind.Agent` enum value internally while mapping to `'other'` on the ACP wire, ensuring no regression in backward compatibility. [Link](https://github.com/QwenLM/qwen-code/pull/5085)

7. **#5051 — feat(core): migrate Computer Use to cua-driver (cross-platform)**  
   A major migration: replaces the experimental `open-computer-use` backend with `cua-driver-rs`, a Rust-based native driver that is background-only and does not steal focus. Marked as experimental. [Link](https://github.com/QwenLM/qwen-code/pull/5051)

8. **#5091 — fix(webui): defer DaemonClient disposal to survive React StrictMode**  
   Fixes a "Loading..." loop in web-shell dev mode. The `DaemonClient` was being disposed during React StrictMode double-mount; this defers disposal to prevent stale connections. [Link](https://github.com/QwenLM/qwen-code/pull/5091)

9. **#5036 — fix(core): hard-stop repeated identical tool calls**  
   Moves the repetitive-tool-call detection into the core stream loop, away from the TUI hook, making it deterministic across all interfaces. Direct fix for Issue #5019. [Link](https://github.com/QwenLM/qwen-code/pull/5036)

10. **#5020 — fix(cli): drop tool calls after cancellation**  
    Ensures that if a stream is cancelled after yielding a tool call request, the pending tool call is discarded and never dispatched. Essential for preventing side effects from interrupted sessions. [Link](https://github.com/QwenLM/qwen-code/pull/5020)

---

## Feature Request Trends

The most demanded feature directions emerging from current issues are:

- **Multi-Client Configuration Migration**: Several requests (e.g., `#4845`) ask for tools to import/export settings from Claude Code, Cursor, and other AI coding assistants. This reflects Qwen Code's positioning as a multi-model, multi-provider tool that must coexist with competitors.
- **Session and Agent Management**: Requests for persistent session sidebars (`#5074`), dynamic workflows port (`#4721`), and better session lifecycle control show that developers want richer session management beyond the basic terminal.
- **Dynamic Workflows / Multi-Agent Orchestration**: The P4a PR (#5094) and Issue #4721 signal strong interest in multi-agent execution patterns similar to Claude Code's latest features.
- **Skill and Configuration Discoverability**: Users want skills to work across all modes (`#5007`), custom providers with arbitrary IDs (`#5090`), and better git integration (`#4769`).
- **Desktop UI Enhancements**: Demands for prominent git branch display, configurable timestamps (`#5001`), and responsive layouts indicate the desktop app is becoming a primary touchpoint.

---

## Developer Pain Points

Recurring frustrations from the community include:

- **Long-Context Performance Degradation**: Multiple reports (`#5018`, `#5019`, `#5029`) describe models "losing attention" or "getting dumber" after long sessions, with repetitive tool calls and forgotten context being the top symptoms.
- **Authentication and Provider Confusion**: Mixing standard API keys with Token Plan endpoints causes silent 401 errors (`#5080`). The architecture conflating provider identity with SDK protocol is a common footgun.
- **Session Interruption and Cancellation Bugs**: Cancelling a streaming tool call still executes the tool (`#5016`), and exiting plan mode shows only partial plans (`#5075`). These destroy the trust that the tool respects user intent.
- **File Update Staleness**: In YOLO mode, automatic edits can fail silently, requiring a second instruction to actually write changes (`#4672`). This feels like the tool "pretended" to edit but didn't.
- **Cross-Platform Gaps**: Linux SSH clipboard (`#4926`), VSCode Windows extension being flagged as malware (`#5055`), and TUI freezes on Linux (`#5083`) show that non-macOS platforms still have first-class support issues.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-14

> *Note: The project now lives as **CodeWhale** (github.com/Hmbown/CodeWhale), retaining its DeepSeek‑TUI lineage. All links below point to the current repository.*

---

## Today’s Highlights

The final push toward **v0.8.60** is dominating activity, with a major architectural proposal to split sub‑agents into a headless worker runtime and several new TUI commands (`/swarm`, `/experiments`). Community contributions are accelerating: a fix for cost tracking on non‑DeepSeek models landed, keyboard shortcuts were improved, and the build system received a compatibility patch.

---

## Releases

No new releases in the last 24 hours. The team is deep in the v0.8.60 release cycle, with dozens of closed issues converging on that milestone.

---

## Hot Issues (10 selected)

**#3096 – Split sub‑agents into a headless worker runtime with lightweight TUI projections**  
*Open | Author: Hmbown | Updated: 2026‑06‑13*  
Proposes a fundamental re‑architecture: sub‑agents become cheap, async headless tasks with thin UI wrappers instead of the current “UI‑shaped” in‑process runtime. This is the most consequential architectural discussion of the week.  
[https://github.com/Hmbown/CodeWhale/issues/3096](https://github.com/Hmbown/CodeWhale/issues/3096)

**#3082 – Group background tasks into workflows with phase summaries and collapsed Bash runs**  
*Closed | Author: Hmbown | Updated: 2026‑06‑13*  
Addresses visual clutter from many verification commands. Adds workflow‑level cards with title, elapsed time, and agent count – a clear UX win for multi‑agent sessions. Attracts positive comments (6).  
[https://github.com/Hmbown/CodeWhale/issues/3082](https://github.com/Hmbown/CodeWhale/issues/3082)

**#3142 – Add agent run ledger with follow‑up, takeover, and artifact receipts**  
*Closed | Author: Hmbown | Updated: 2026‑06‑13*  
Research‑driven design inspired by Cursor’s “operational run” model. Formalises how background work is presented and tracked, including receipts for cloud runs.  
[https://github.com/Hmbown/CodeWhale/issues/3142](https://github.com/Hmbown/CodeWhale/issues/3142)

**#3178 – Add `/swarm` as a Whaleflow‑backed dynamic multi‑agent mode**  
*Closed | Author: Hmbown | Updated: 2026‑06‑13*  
Introduces the user‑facing command for dynamic multi‑agent work, backed by the new headless subagent lanes. Decision: keep the name `/swarm`, avoid resurrecting the old code.  
[https://github.com/Hmbown/CodeWhale/issues/3178](https://github.com/Hmbown/CodeWhale/issues/3178)

**#3154 – Agent Fleet control plane for always‑running verifiable work**  
*Open | Author: Hmbown | Updated: 2026‑06‑13*  
Epic tracking the Cursor‑style agent‑fleet pattern: a manager agent orchestrates many workers, monitors progress, restarts stuck work, and escalates only to humans. High strategic value.  
[https://github.com/Hmbown/CodeWhale/issues/3154](https://github.com/Hmbown/CodeWhale/issues/3154)

**#3066 – Cost tracking dead for all non‑DeepSeek models**  
*Open | Author: Hmbown | Updated: 2026‑06‑13*  
A frustrating regression: `pricing_for_model` returns `None` for Kimi, Qwen, GLM, OpenAI, etc. Every per‑turn/session cost display is broken. Community member **@mvanhorn** immediately submitted a PR (#3201).  
[https://github.com/Hmbown/CodeWhale/issues/3066](https://github.com/Hmbown/CodeWhale/issues/3066)

**#3198 – `cargo install codewhale‑tui` fails**  
*Closed | Author: RektLead | Updated: 2026‑06‑13*  
Rust compilation error due to trait bound `HashTable<usize>: Allocative` in the `starlark_map` dependency. Quickly closed, but highlights potential CI/dependency lock‑in gaps.  
[https://github.com/Hmbown/CodeWhale/issues/3198](https://github.com/Hmbown/CodeWhale/issues/3198)

**#2972 – Direction: how much Claude Code convergence is right for CodeWhale?**  
*Closed | Author: Hmbown | Updated: 2026‑06‑13*  
A healthy community debate. PR #2865 proposed convergence with Claude Code, but users pushed back, valuing CodeWhale’s simplicity and customisability. The conversation informed the design of `/swarm` and Whaleflow.  
[https://github.com/Hmbown/CodeWhale/issues/2972](https://github.com/Hmbown/CodeWhale/issues/2972)

**#3203 – Make queued steering reliable and add Ctrl+S send**  
*Open | Author: Hmbown | Updated: 2026‑06‑13*  
In v0.8.60 testing, Cmd+Enter sometimes fails to submit steering messages when the model/agent is busy. Adding Ctrl+S as an alternative. A critical UX fix for real‑time agent steering.  
[https://github.com/Hmbown/CodeWhale/issues/3203](https://github.com/Hmbown/CodeWhale/issues/3203)

**#2982 – Clearly display busy or free**  
*Open | Author: anodsvsing | Updated: 2026‑06‑13*  
Users find the busy/idle status too subtle. Proposes colour blocks, traffic‑light icons, or motion indicators. Underlines a broader need for better HUD visibility.  
[https://github.com/Hmbown/CodeWhale/issues/2982](https://github.com/Hmbown/CodeWhale/issues/2982)

---

## Key PR Progress (all 8)

**#3201 – fix: revive cost tracking for non‑DeepSeek models**  
*Open | Author: mvanhorn*  
A community PR that expands `pricing_for_model` to cover Kimi, Qwen, GLM, OpenAI, MiniMax, and others. Directly fixes #3066.  
[https://github.com/Hmbown/CodeWhale/pull/3201](https://github.com/Hmbown/CodeWhale/pull/3201)

**#2808 – feat(runtime‑api): add session save, undo/retry, and snapshot endpoints**  
*Open | Author: gaord*  
A large addition aligning GUI capabilities with the TUI. Adds `POST /v1/sessions`, `PUT /v1/sessions/undo`, and snapshot endpoints. Still needs review.  
[https://github.com/Hmbown/CodeWhale/pull/2808](https://github.com/Hmbown/CodeWhale/pull/2808)

**#3199 – feat(runtime‑api): add PUT /v1/sessions endpoint for engine‑based session save**  
*Open | Author: gaord*  
A focused slice of #2808, adding a oneshot‑channel endpoint to save the current engine state. Ready for targeted review.  
[https://github.com/Hmbown/CodeWhale/pull/3199](https://github.com/Hmbown/CodeWhale/pull/3199)

**#3197 – Rename DeepSeek blue consumers to whale accent**  
*Open | Author: nightt5879*  
Closes #3069. Adds `palette::WHALE_ACCENT_PRIMARY` as the semantic colour token, keeps `DEEPSEEK_BLUE` as a deprecated alias. A branding/deprecation PR.  
[https://github.com/Hmbown/CodeWhale/pull/3197](https://github.com/Hmbown/CodeWhale/pull/3197)

**#3196 – feat(tui): Ctrl+P / Ctrl+N navigate slash‑command autocomplete**  
*Open | Author: 1Git2Clone*  
Adds standard Emacs‑style keyboard navigation for the slash‑command popup, including a guard on global Ctrl+P file‑picker.  
[https://github.com/Hmbown/CodeWhale/pull/3196](https://github.com/Hmbown/CodeWhale/pull/3196)

**#3195 – fix(telegram): keep polling while turns stream**  
*Open | Author: cyq1017*  
Fixes #2966: long‑running Telegram event streams should not block `getUpdates`. Starts turns in background tasks and re‑attaches on stale ACKs.  
[https://github.com/Hmbown/CodeWhale/pull/3195](https://github.com/Hmbown/CodeWhale/pull/3195)

**#3193 – Add config‑gated Pro Plan routing profile**  
*Open | Author: dumbjack*  
Revives the Pro Plan concept from #1865 as a config‑gated routing profile (default disabled). No default mode change.  
[https://github.com/Hmbown/CodeWhale/pull/3193](https://github.com/Hmbown/CodeWhale/pull/3193)

**#3191 – feat(config): add first‑party Z.ai and StepFlash/StepFun provider routes**  
*Closed | Author: Hmbown*  
Merged quickly. Adds Z.ai (GLM Coding Plan) and StepFun/StepFlash as first‑class providers, matching their own API specs instead of routing through OpenRouter.  
[https://github.com/Hmbown/CodeWhale/pull/3191](https://github.com/Hmbown/CodeWhale/pull/3191)

---

## Feature Request Trends

Several clear themes emerge from the 30 issues:

1. **Headless sub‑agent runtime and agent fleets** – The dominant direction: making sub‑agents light, headless, and orchestratable via a control plane (issues #3096, #3154, #3178, #3167).
2. **New provider support** – Repeated requests for Z.ai, StepFlash, MiniMax, and better OpenRouter integration (#3187, #1310, #3192).
3. **TUI polish and discoverability** – Better status indicators, keyboard shortcuts, helper hints, and command autocomplete (#2982, #3194, #3196, #3203).
4. **Cost and usage transparency** – Expanding pricing tables beyond DeepSeek, fixing per‑model cost tracking (#3066, #3202).
5. **Workflow authoring** – TypeScript/JavaScript surface for WhaleFlow (#3097, #3163) and visual grouping of background tasks (#3082).
6. **Contribution on-ramp** – Issue #2890 reopens the contribution gate workflow, and #3192 pushes for listing in the ACP registry.

---

## Developer Pain Points

- **Installation reliability** – `cargo install` fails due to Rust dependency issues (#3198). The `starlark_map` trait bound error is a recurring pain point for newcomers.
- **Cost tracking gaps** – Pricing for all non‑DeepSeek models returns `None`, making session costs and cache savings invisible (#3066).
- **TUI blocking during background work** – Even long‑running shell commands feel blocking; the UI does not stay responsive (#3200).
- **Steering unreliability** – Cmd+Enter does not always submit while the model is busy; users resort to workarounds (#3203).
- **Context window errors without warning** – The TUI shows incorrect context‑window metadata, leading to `context_length_exceeded` errors with no preflight check (#3204).
- **Busy/idle ambiguity** – The agent status display is too subtle; users cannot tell if work is still running (#2982).

---

*Digest generated from github.com/Hmbown/DeepSeek‑TUI (current repo: Hmbown/CodeWhale) on 2026‑06‑14.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*