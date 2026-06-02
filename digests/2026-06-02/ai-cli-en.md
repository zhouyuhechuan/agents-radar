# AI CLI Tools Community Digest 2026-06-02

> Generated: 2026-06-02 02:52 UTC | Tools covered: 9

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
**Date**: 2026-06-02 | **Prepared for**: Technical Decision-Makers & Developers

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape in mid-2026 is characterized by **rapid feature iteration contrasted with persistent reliability gaps**. The six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (now CodeWhale)—are converging on shared infrastructure challenges: context management, cross-platform stability, and credential handling. However, their release velocities, community engagement levels, and pain point profiles diverge significantly. A notable shift is the **commoditization of MCP (Model Context Protocol)** integration across all tools, alongside growing demand for **local/first-party model support** and **cost transparency**. The ecosystem currently favors tools with strong safety guardrails and deterministic behavior over raw capability, as cascading failures and silent regressions erode user trust.

---

## 2. Activity Comparison

| Tool | Open Issues (Recent) | PRs (Last 24h) | Release Status | Community Signal |
|------|---------------------|----------------|----------------|------------------|
| **Claude Code** | 50+ hot issues; top 10 avg 35 comments | 9 total; 5 substantive | **v2.1.160** (safety-critical) | High engagement (67👍 bug), many regressions |
| **OpenAI Codex** | 10 hot issues; avg 20 comments | 10 notable PRs | **rust-v0.136.0** (TUI improvements) | Strong Windows pain signals (9/10 top issues) |
| **Gemini CLI** | 30 hot issues; top 10 avg 7 comments | 20 updated; 10 key | **v0.45.0-nightly** (no stable) | Moderate activity; agent reliability dominating |
| **GitHub Copilot CLI** | 10 noteworthy; avg 5 comments | 1 PR (spam) | **v1.0.57** (patch) | Low PR throughput; model parity complaints |
| **Kimi Code CLI** | 2 issues updated | 4 PRs | **No release** | Low activity; ecosystem compatibility focus |
| **OpenCode** | ~30 hot issues (MCP regression cluster) | 10 PRs | **No release** (v1.15.13 unbroken) | High; MCP UI regression dominating conversation |
| **Pi** | 43 issues updated | 20 PRs | **No release** | Very high; model integration + TUI fixes |
| **Qwen Code** | 10 hot issues; avg trending | 10 PRs | **v0.17.0-nightly** | Moderate; local model stability focus |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues; avg 10 comments | 10 PRs | **v0.8.49** (rebrand) | Moderate; cost + cache performance concerns |

**Key observation**: OpenAI Codex and Claude Code have the highest issue engagement per bug, while Pi and OpenCode lead in PR throughput. Gemini CLI and Copilot CLI have the lowest PR contribution velocity relative to their issue counts.

---

## 3. Shared Feature Directions

The following needs appear across **3+ tool communities**, indicating ecosystem-wide priorities:

### a) Context & Session Management
- **Reproducible session resumption** (Claude Code #62063, Qwen Code #4679, DeepSeek TUI #2492, OpenCode #28581)
- **Configurable context limits** (Claude Code #62063, Gemini CLI #24353, Copilot CLI #3623)
- **Auto-compaction control** (Claude Code #63015, Copilot CLI #3621)

### b) MCP Integration Maturity
- **Per-project MCP configuration** (Qwen Code #4615, OpenCode #30104, Claude Code #36411)
- **Approval semantics for MCP tools** (Qwen Code #4615, Claude Code #64610, OpenCode #30085)
- **Cross-platform MCP parity** (Claude Code #40198, OpenCode #30104, DeepSeek TUI #2328)

### c) Platform Parity (Windows & Linux)
- **Windows ARM64 support** (Claude Code #40198, Codex #25203, DeepSeek TUI #1812)
- **Wayland compatibility** (Gemini CLI #21983, DeepSeek TUI #1920)
- **Alpine/musl support** (OpenCode #27589, Copilot CLI #2060)

### d) Permission & Security Hardening
- **Prompt before shell/config writes** (Claude Code v2.1.160, OpenCode #16331, Qwen Code #4572)
- **Deterministic permission profiles** (Codex #25739, OpenCode #30287, Claude Code #64610)

### e) Cost Transparency & Control
- **Configurable usage limits** (Claude Code #62063, OpenCode #28846, DeepSeek TUI #743)
- **Provider-agnostic pricing feedback** (All tools report cost surprises from context defaults)

### f) Local Model & Provider Expansion
- **MiniMax-M3 support** (Pi #5271, Qwen Code #4663)
- **Ollama/local model timeouts** (Qwen Code #4657, Pi #5089)
- **OpenRouter provider fixes** (Pi #5229, Qwen Code #3384)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|--------------|
| **Primary Strength** | Safety guardrails & collaboration | Desktop integration & enterprise | Agent orchestration | GitHub ecosystem | Plugin extensibility | TUI rendering & extensions | Local model support | Cost efficiency |
| **Weakest Area** | Cost surprises & cascading failures | Windows stability & OAuth | Agent hangs & false success | Model parity & clipboard | MCP UI sync stability | TUI regressions & resource leaks | Streaming timeouts | Cache hit rate & token waste |
| **Target User** | Power users/pro users | Enterprise/desktop | Google ecosystem | GitHub teams | Plugin developers | Terminal power users | Qwen/Asian market | Cost-sensitive devs |
| **Release Cadence** | Fast (2-3/week) | Moderate (weekly) | Nightly (unstable) | Slow (patches) | Slow (no stable) | Fast (daily PRs) | Nightly (unstable) | Weekly |
| **Technical Approach** | Python/CLI harness | Rust/desktop app | TypeScript/CLI | Go/CLI | React/TUI | TypeScript/TUI | TypeScript/Node | Rust/TUI |

**Key differentiators**:
- **Claude Code** leads in safety automation (prompts before shell startup edits, build-tool config warnings) but suffers most from parallel tool-call cascading failures.
- **OpenAI Codex** has the strongest desktop experience but the weakest Windows story—9 of 10 top issues are platform-related.
- **Gemini CLI** is the most ambitious in agent orchestration (sub-agents, skills, generalist) but has the most severe reliability bugs (hangs, false success).
- **GitHub Copilot CLI** is the most conservative in feature velocity but benefits from VS Code ecosystem integration—model parity is its existential pain point.
- **Pi** has the highest developer community engagement (43 issues, 20 PRs/day) and leads in TUI extensions, but suffers from rendering regression cycles.
- **Qwen Code** and **DeepSeek TUI** are both carving niches around **local models** and **cost efficiency**, respectively, but struggle with class-leading reliability.

---

## 5. Community Momentum & Maturity

| Tier | Tools | Characteristics |
|------|-------|-----------------|
| **High Momentum, High Maturity** | Claude Code, OpenAI Codex | Large communities, frequent releases, deep issue histories, but regression-prone. Professional-grade user expectations. |
| **High Momentum, Medium Maturity** | Pi, OpenCode | Most PR activity per day; rapidly evolving extension/plugin systems. Community is smaller but highly engaged. TUI quality inconsistent. |
| **Medium Momentum, Medium Maturity** | Gemini CLI, Qwen Code | Nightly release cycles indicate active development, but stable releases are rare. Issues show systemic reliability gaps (hangs, timeouts). |
| **Low Momentum, Low Maturity** | Copilot CLI, DeepSeek TUI (CodeWhale) | Lowest PR throughput; Copilot CLI sees 1 PR/day (often spam). DeepSeek TUI rebrand may increase activity, but current signals are weak. |
| **Low Momentum, Niche** | Kimi Code CLI | 2 issues and 4 PRs updated. Used as a reference/API integration tool rather than actively developed CLI. |

**Maturity markers**:
- **Claude Code** has the most sophisticated bug reporting (reproducers, severity labels, platform tags) and the highest upvote density (67👍 on a single bug).
- **OpenCode** and **Pi** have the fastest triage cycles—multiple PRs merged within hours of issue creation.
- **Gemini CLI** and **Qwen Code** lack stable release channels, making them unsuitable for production workflows despite promising architectures.

---

## 6. Trend Signals

### Ecosystem-Wide Trends (Based on >2 tools reporting)

**1. Context Budget as a First-Class Concern**
- 5 of 9 tools have open issues about unexpected context costs or limits. Users demand configurable, transparent memory accounting. This is shifting from a "nice-to-have" to a **deal-breaker for Pro/paid users**.

**2. Local Model Integration is the New "Table Stakes"**
- Qwen Code, Pi, and DeepSeek TUI are all prioritizing Ollama/VLLM/local model timeouts. The assumption that users want cloud-only is fading; **offline-capable CLIs** are becoming a competitive differentiator.

**3. Tool-Call Reliability is Worse Than Model Quality**
- Across all tools, the #1 pain point is not model intelligence but **tool-call parsing failures, cascading cancellations, and serialization corruption** (Claude Code #22264, #49747; Codex #24300). This suggests the industry needs to invest more in tool-call infrastructure than model benchmarking.

**4. Permission Systems are Inadequate**
- Claude Code, OpenCode, Qwen Code, and Codex all have active issues about permissions being **ignored, bypassed, or non-deterministic**. The pattern of "permissions work in CLI but not desktop" (OpenCode) or "permissions are silently downgraded" (Codex #24300) is eroding trust.

**5. Platform Exclusivity Hurts Adoption**
- Windows users are consistently underserved (Claude Code ARM64 failure, Codex OAuth crash, Gemini Wayland). Tools that **ship cross-platform parity** (Pi, Qwen Code) are gaining favor among team leads deploying heterogeneous environments.

**6. MCP Adoption is Being Blocked by UX**
- Every tool with MCP support sees issues about **inbound notifications broken, UI not reflecting server state, or installation complexity**. MCP is technically present but the "last mile" of user experience is missing.

**7. Developer Tooling → End-User Tooling Shift**
- The surge in installer PRs (CodeWhale NSIS, Codex PAT support, OpenCode Docker publishing) indicates tools are targeting **non-developer users** (educators, enterprise IT, students). This is a strategic pivot from "CLI for devs" to "agent application for everyone."

### Recommendations for Developers & Decision-Makers

| Use Case | Recommended Tool | Risk |
|----------|-----------------|------|
| **Production code generation** | Claude Code (with context limits configured) | Cascading tool failures |
| **Enterprise desktop deployment** | OpenAI Codex (macOS only) | Windows instability |
| **Experimental agent orchestration** | Gemini CLI | Agent hangs |
| **GitHub workflow integration** | Copilot CLI | Model parity gaps |
| **Plugin/extensibility** | OpenCode or Pi | UI regression cycles |
| **Local/private models** | Qwen Code | Streaming timeouts |
| **Cost-sensitive automation** | DeepSeek TUI (CodeWhale) | Token waste, rebrand migration |

**Bottom line**: No tool is production-ready across all dimensions. Claude Code and OpenAI Codex lead in maturity but carry significant regression risk. Pi and OpenCode have the best developer experience momentum but the least professional-grade testing. **The ecosystem is in a "capability sprint" with reliability as the lagging indicator.**

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data Source**: github.com/anthropics/skills | **Snapshot**: 2026-06-02  

---

## 1. Top Skills Ranking  
The following Pull Requests represent the most actively discussed Skill contributions in the repository. Each is **still open** (not yet merged) and has attracted community attention through detailed proposals, technical discussion, or cross-referencing with other issues.

| # | Skill / PR | Functionality | Discussion Highlights |
|---|-----------|---------------|----------------------|
| 514 | **[Document Typography](https://github.com/anthropics/skills/pull/514)** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. | Addresses a universal pain point for Claude-generated reports. Community noted that typographic polish is often overlooked by AI, making this an immediate quality-of-life improvement. |
| 486 | **[ODT Skill](https://github.com/anthropics/skills/pull/486)** | Creates, fills, parses, and converts OpenDocument (.odt, .ods) files; triggers on any mention of ODF/LibreOffice. | High demand for ISO-standard open-source document handling. Discussion centered on template filling and round-trip fidelity. |
| 210 | **[Frontend-Design Clarity](https://github.com/anthropics/skills/pull/210)** | Revises the frontend-design skill to ensure every instruction is actionable within a single conversation and steers Claude’s behavior specifically. | Received deep review on token efficiency and instruction granularity; sets a pattern for skill refactoring across the repo. |
| 83 | **[Skill-Quality & Security Analyzers](https://github.com/anthropics/skills/pull/83)** | Two meta-skills that evaluate other Skills across five quality dimensions (structure, documentation, security, etc.). | Meta-tooling is a growing subcategory. Commenters requested integration with CI pipelines and suggested expanding the security analyzer to cover prompt injection. |
| 181 | **[SAP-RPT-1-OSS Predictor](https://github.com/anthropics/skills/pull/181)** | Wraps SAP’s open-source tabular foundation model for predictive analytics on SAP business data. | Enterprise interest is high. Discussion explored how to handle SAP data privacy and whether to bundle sample data files. |
| 723 | **[Testing Patterns](https://github.com/anthropics/skills/pull/723)** | Covers unit testing (AAA pattern), React Testing Library, integration testing, and testing philosophy (Trophy model). | One of the most requested testing skills. Community debated whether to include end-to-end testing or keep the scope focused on unit+integration. |
| 568 | **[ServiceNow Platform](https://github.com/anthropics/skills/pull/568)** | Broad platform assistant covering ITSM, ITOM, ITAM/SAM, SecOps, FSM, CSDM, and IntegrationHub. | Huge scope raised efficiency concerns; reviewers suggested splitting into multiple domain-specific skills. |
| 444 | **[AURELION Suite](https://github.com/anthropics/skills/pull/444)** | Four skills (kernel, advisor, agent, memory) implementing a structured cognitive framework for knowledge management. | Unique “meta-cognitive” approach. Community asked for benchmarks on context-window overhead and real-world use cases. |

---

## 2. Community Demand Trends  
Analysis of the top Issues (by comment count) reveals several high-demand directions for new or improved Skills:

- **Organizational Skill Sharing** (#228, 13 comments) – Users want a native library or direct sharing link within Claude.ai instead of manual `.skill` file exchange.
- **Skill-Creator Tooling** (#202, 8 comments) – Strong call to refactor the `skill-creator` skill into a concise, operational instruction set rather than verbose developer docs.
- **Security & Trust Boundaries** (#492, 7 comments) – Community skills distributed under the `anthropic/` namespace raise impersonation risks; demand for a security-oriented skill or metadata validation.
- **Agent Governance** (#412, 4 comments) – A proposed skill for policy enforcement, threat detection, and audit trails in AI agent systems has garnered early support.
- **MCP Integration** (#16, 4 comments) – Interest in exposing Skills as MCP tools to create a unified API surface for external tooling.
- **Multi-File Preloading** (#1220, 2 comments, very recent) – Skills split across several reference files are inefficient; users want inline bundling or automatic preload of refs.

**Broader pattern**: Enterprise platform integration (SAP, ServiceNow, ODF) and **meta-tooling** (quality analyzers, skill-creator improvements) are the two strongest currents. Document typography and testing patterns reflect a desire for **skill quality and polish** beyond raw functionality.

---

## 3. High-Potential Pending Skills  
These Pull Requests still have active comment threads and are likely to land soon (sorted by recency or momentum):

- **[#538 – Fix case-sensitive file references in PDF skill](https://github.com/anthropics/skills/pull/538)** – A simple but critical fix for Linux users; low risk, high impact.
- **[#539 – Unquoted YAML detection in skill-creator](https://github.com/anthropics/skills/pull/539)** – Prevents silent parsing failures; complements the existing skill-quality-analyzer.
- **[#541 – DOCX tracked change ID collision fix](https://github.com/anthropics/skills/pull/541)** – Prevents document corruption when bookmarks are present; touches core XML handling.
- **[#1099 – run_eval.py Windows subprocess crash](https://github.com/anthropics/skills/pull/1099)** – Fixes a blocker for Windows users running evaluation scripts; high demand.
- **[#1050 – Windows subprocess + encoding bugs](https://github.com/anthropics/skills/pull/1050)** – Companion fix for CLI launch on Windows.
- **[#361 – YAML special character detection](https://github.com/anthropics/skills/pull/361)** – Overlaps with #539 but adds coverage for unquoted `compatibility` fields; reviewers are converging on a combined approach.
- **[#190 – n8n-builder & n8n-debugger](https://github.com/anthropics/skills/pull/190)** – Four community skills (including faf-expert); production-tested by the author. Discussion focuses on deduplication with existing workflow skills.

---

## 4. Skills Ecosystem Insight  
**The community’s most concentrated demand is for enterprise-grade document handling and platform integration skills, coupled with a parallel push for meta-tooling that improves skill reliability, security, and cross-platform compatibility.**

---

# Claude Code Community Digest – 2026-06-02

## Today's Highlights

Version **v2.1.160** shipped with a safety‑critical change: Claude Code now prompts before modifying shell startup files and build‑tool configs that grant code execution. The community is heavily discussing several bugs, including the long‑running **Windows ARM64 Cowork VM failure** (#40198, 53 comments) and the **Opus 4.7 thinking summaries missing** issue (#49268, 67 👍). A surge of reports about **1M context defaults on Pro plans** and **parallel tool‑call cascading failures** indicates growing frustration with cost and reliability.

---

## Releases

**v2.1.160** – *2026-06-01/02*  
- Added a prompt before writing to shell startup files (`.zshenv`, `.zlogin`, `.bash_login`) and `~/.config/git/` – previously could lead to unintended command execution.  
- `acceptEdits` mode now prompts before writing build‑tool config files that grant code execution (e.g., `.npmrc`).  

These changes improve safety guards for automated file modifications.

---

## Hot Issues (10 selected from 50)

1. **[#40198 – Cowork VM fails to start on Windows ARM64 (Snapdragon)](https://github.com/anthropics/claude-code/issues/40198)**  
   53 comments, 7 👍 | *platform:windows, area:cowork*  
   A blocking bug for Samsung Galaxy Book4 Edge users. Community has been waiting since March; still open.

2. **[#60334 – Image processing failures causing conversation token waste](https://github.com/anthropics/claude-code/issues/60334)**  
   41 comments, 13 👍 | *closed bug*  
   Repeated API errors remove images silently, burning 70% of usage windows. High cost impact.

3. **[#49268 – Thinking summaries missing on Opus 4.7](https://github.com/anthropics/claude-code/issues/49268)**  
   40 comments, 67 👍 | *open, has repro*  
   `display: "summarized"` not set by harness. Most‑upvoted open bug; affects extended‑thinking workflows.

4. **[#62063 – Claude Code defaults to 1M context on fresh session with no workaround on Pro plan](https://github.com/anthropics/claude-code/issues/62063)**  
   37 comments, 21 👍 | *open*  
   Pro users bombarded with unexpected costs. Community demands a configurable default context limit.

5. **[#62123 – Model's tool call could not be parsed (retry also failed)](https://github.com/anthropics/claude-code/issues/62123)**  
   36 comments, 56 👍 | *open*  
   Frequent parsing failures on Opus 4.7, especially with Japanese locale. Blocks productivity.

6. **[#22264 – Parallel tool calls cascade-fail when one sibling errors](https://github.com/anthropics/claude-code/issues/22264)**  
   31 comments, 61 👍 | *open, has repro*  
   All sibling calls cancelled on any single failure, forcing wasteful retries. Long‑standing pain point.

7. **[#49747 – Opus 4.7 mixes legacy XML tool‑use format into JSON tool calls on longer payloads](https://github.com/anthropics/claude-code/issues/49747)**  
   19 comments, 13 👍 | *open, regression*  
   Intermittent serialization corruption causing tool call failures. Affects MCP interactions.

8. **[#36411 – Telegram MCP plugin: inbound notifications never delivered to session](https://github.com/anthropics/claude-code/issues/36411)**  
   17 comments, 16 👍 | *open, area:mcp*  
   Outbound works; inbound channel broken. Stalls MCP adoption for messaging use cases.

9. **[#23620 – Agent team lost when lead's context gets compacted during long session](https://github.com/anthropics/claude-code/issues/23620)**  
   16 comments, 10 👍 | *open*  
   Context compaction silently drops agent team definitions. Data loss in collaborative scenarios.

10. **[#44941 – Auto mode not showing in VS Code extension on Windows](https://github.com/anthropics/claude-code/issues/44941)**  
    14 comments, 6 👍 | *open, regression*  
    Windows VS Code users cannot use auto mode. Platform parity regression.

---

## Key PR Progress (out of 9 total)

1. **[#64607 – Fix: Plugin .mcp.json example incorrectly uses mcpServers wrapper](https://github.com/anthropics/claude-code/pull/64607)**  
   *arnavnagzirkar* – Corrects documentation so `.mcp.json` uses flat format, not `mcpServers` wrapper (which belongs in `plugin.json`). Ready for review.

2. **[#63686 – Bump stale and autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)**  
   *caseyWebb* – Prolongs issue lifecycle to reduce premature closure of valid bugs. Open for discussion.

3. **[#63467 – Docs: add Windows gh CLI install instruction in commit-commands README](https://github.com/anthropics/claude-code/pull/63467)**  
   *weslleyramon001-png* – Adds `winget install --id GitHub.cli` alongside existing macOS instructions.

4. **[#63872 – Docs: fix README capitalization and wording](https://github.com/anthropics/claude-code/pull/63872)**  
   *padmarajnidagundi* – Standardizes product names (`GitHub`, `macOS`) and improves intro sentence punctuation.

5. **[#64489 – updated example file](https://github.com/anthropics/claude-code/pull/64489)**  
   *chiranjeevirawal7-byte* – Adds sample content to example file. Minor contribution, under review.

The remaining PRs (#58673, #61478, #64603, #64602) are spam or trivial “s”-type submissions and were closed or ignored.

---

## Feature Request Trends

- **Windows Computer Use support** – [#64381](https://github.com/anthropics/claude-code/issues/64381) requests Claude Code CLI computer‑use capabilities on Windows (currently unavailable). Growing demand as Windows ARM64 adoption increases.  
- **Documentation of security boundaries** – [#64610](https://github.com/anthropics/claude-code/issues/64610) highlights an undocumented built-in allowlist that bypasses WebFetch `deny` rules. Users need transparent docs to configure network access correctly.  
- **Branch‑aware multi‑session safety** – [#60295](https://github.com/anthropics/claude-code/issues/60295) suggests preventing silent branch swaps when multiple sessions share a repo.

---

## Developer Pain Points

1. **Context exhaustion and cost surprises** – Auto‑compact not triggering (#63015), 1M‑context default on Pro plans (#62063), and context‑usage discrepancies between CLI and web UI (#64034) waste budgets without warning.  
2. **Cascading failures in parallel tool calls** – [#22264](https://github.com/anthropics/claude-code/issues/22264) remains a top‑voted pain point: one failing tool kills all siblings, forcing wasteful retries.  
3. **Opus 4.7 tool‑format regressions** – Mixing XML/JSON (#49747) and parsing failures (#62123) disrupt workflows, especially with non‑English input or long payloads.  
4. **Destructive /rewind UX** – Multiple reports (#27387, #50897, [#64615](https://github.com/anthropics/claude-code/issues/64615)) that Esc‑Esc /rewind defaults to reverting code without confirmation. Accidental data loss is a high‑severity issue.  
5. **Windows platform gaps** – Cowork VM failure on ARM64 (#40198), missing Auto mode in VS Code (#44941), and broken log/events exporter (#64396) fragment the Windows experience.  
6. **MCP integration friction** – Telegram inbound notifications broken (#36411), OAuth `prompt=consent` hardcoded for Entra (#49722), and lack of Computer Use on Windows (#64381) limit real‑world MCP adoption.  
7. **Rate limiting after 5‑hour resets** – [#53922](https://github.com/anthropics/claude-code/issues/53922) describes bulk‑spawning sessions right after limit reset that get rate‑limited, wasting the fresh window.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-02

## Today's Highlights
The Codex team shipped **rust-v0.136.0**, improving TUI markdown rendering with clickable OSC 8 links and automatic table-to-key/value fallback. Windows stability remains the strongest community signal, with nine of the top‑10 hot issues reporting desktop‑app crashes, sandbox failures, or OAuth callback errors. A key PR introduces **v2 personal access token (PAT) support** for CLI authentication, while a stacked series of PRs starts routing credentialed traffic through a managed MITM proxy — both long‑requested infra improvements.

## Releases
**rust-v0.136.0** (published in the last 24 h)  
- TUI markdown now keeps web links clickable (OSC 8 metadata) and converts cramped tables to readable key/value records without losing link targets.  
- Sessions can be archived from the TUI with `/archive` or from the CLI with `codex archive` / `codex u`.  
GitHub release: [openai/codex/releases/tag/rust-v0.136.0](https://github.com/openai/codex/releases/tag/rust-v0.136.0) *(No direct link provided; use the tag name)*

## Hot Issues (10 noteworthy)
1. **#18341** – [Mac app: persistent blurred/translucent overlay below composer](https://github.com/openai/codex/issues/18341)  
   *35 comments, 18 👍* – Widespread visual bug on macOS, affecting 0.122.0-alpha.1. Users report the overlay remains after dismissing the composer.

2. **#20320** – [ChatGPT phone verification loop without sending SMS](https://github.com/openai/codex/issues/20320)  
   *28 comments, 7 👍* – Sign‑up/auth flow asks for phone OTP but never delivers the code; users are locked out of upgrade.

3. **#18993** – [VS Code extension: unable to open past conversation history](https://github.com/openai/codex/issues/18993)  
   *28 comments, 48 👍* – Regression in 1.117.0, affecting Windows and Plus subscribers. No workaround yet.

4. **#25203** – [Windows GitHub OAuth callback: “Unable to find Electron app”](https://github.com/openai/codex/issues/25203)  
   *28 comments, 14 👍* – OAuth flow fails on Windows 11 after logging in; the Electron protocol handler is broken.

5. **#11014** – [TUI scrolling broken over SSH from iOS clients](https://github.com/openai/codex/issues/11014)  
   *19 comments, 4 👍* – 0.98.0 broke scroll for users with iOS terminal apps. Still unresolved.

6. **#25157** – [Windows OAuth “Open in Codex” leads to Electron error](https://github.com/openai/codex/issues/25157)  
   *17 comments, 15 👍* – Pro ($200/mo) users hit this on Windows 11 Pro. The OAuth success redirect is malformed.

7. **#16767** – [macOS: sustained syspolicyd/trustd CPU spikes](https://github.com/openai/codex/issues/16767)  
   *7 comments, 12 👍* – Desktop app triggers high CPU from system security services; impacts battery and performance.

8. **#25249** – [Windows: semi-transparent sidebar causes undrawn regions when maximized](https://github.com/openai/codex/issues/25249)  
   *10 comments* – Aesthetic bug that leaves holes in the window frame.

9. **#25197** – [Windows notification click opens invalid WindowsApps path](https://github.com/openai/codex/issues/25197)  
   *9 comments, 8 👍* – Clicking a turn‑complete notification launches an Electron error instead of the app.

10. **#24638** – [CLI app-server: cwd-scoped environment contract missing](https://github.com/openai/codex/issues/24638)  
    *8 comments* – `codex` vs `codex -c` launches can silently use different env sources, causing confusion.

## Key PR Progress (10 notable)
1. **#25731** – [Support v2 personal access tokens](https://github.com/openai/codex/pull/25731)  
   Adds `codex login --with-access-token` and `CODEX_ACCESS_TOKEN`. Classifies `at-` tokens separately from legacy JWTs; hydrates ChatGPT account metadata.

2. **#25739** – [Derive built-in permission profiles from raw policies](https://github.com/openai/codex/pull/25739)  
   Fixes TOML inheritance for `:workspace` profiles so child keys correctly override parent defaults.

3. **#25738** – [Move code review rules into AGENTS.md](https://github.com/openai/codex/pull/25738) *(merged)*  
   Codex Review now reads repository‑specific rules from `AGENTS.md`, making guidance available alongside the code.

4. **#25732** – [Dependency‑inject code mode session provider](https://github.com/openai/codex/pull/25732)  
   Replaces global state with per‑thread‑tree selection; agents spawned with `AgentControl` inherit the mode.

5. **#25746** – [Add streamable HTTP MCP failure metric](https://github.com/openai/codex/pull/25746)  
   New counter `codex.mcp.streamable_http.post_message.failure` for monitoring MCP reliability.

6. **#22685** – [Add SOCKS5 TCP MITM coverage](https://github.com/openai/codex/pull/22685)  
   Reuses HTTPS MITM path for raw SOCKS5 TCP streams; keeps UDP limited‑mode unchanged.

7. **#22675** – [Route credentialed traffic through MITM proxy](https://github.com/openai/codex/pull/22675)  
   Synthesizes MITM hooks from credentialed routes; rewrites matching HTTPS to the Codex backend proxy.

8. **#25675** – [feat(remote-control): add pairing start](https://github.com/openai/codex/pull/25675) *(merged)*  
   Exposes a narrow RPC to mint short‑lived pairing tokens from an enrolled desktop server.

9. **#24812** – [Show enterprise monthly credit limits in `/status`](https://github.com/openai/codex/pull/24812)  
   Adds optional `spend_control.individual_limit` to the rate‑limit snapshot for enterprise users.

10. **#15730** – [Harden symlinked output and project config writes](https://github.com/openai/codex/pull/15730)  
    Rejects symlinked `--output-last-message` paths with `O_NOFOLLOW` and protects `.codex/config.toml` as read‑only.

## Feature Request Trends
- **Windows first‑class support**: Multiple issues (OAuth, sandbox, crash‑on‑launch, notification handling) show Windows users are disproportionately affected. The community is asking for parity with macOS stability.
- **Better credential management**: The PAT work and credentialed‑routes PR series address long‑standing requests for secure API key and OAuth token handling without browser flows.
- **Enterprise billing visibility**: PR #24812 responds to requests for credit‑limit info directly in the TUI.
- **Remote control / headless operation**: PR #25675 and the remote‑control stack hint at demand for pairing Codex desktop with external controllers.

## Developer Pain Points
- **Windows sandbox failures**: Issues `#25391`, `#24963`, `#24727`, `#25488` all report `windows sandbox failed: spawn setup refresh` breaking Computer Use and browser automation. No fix in sight.
- **Auth friction**: CLI login forces SMS OTP even on hardware‑security‑key accounts (`#25737`); OAuth flows fail on Windows (`#25203`, `#25157`).
- **Unresponsive desktop on long sessions**: Issues `#20867` and `#21761` describe repeated crashes on Windows when resuming long threads with MCP tools enabled.
- **Goal auto‑continuations downgrade permissions**: `#24300` reveals a subtle bug where Full Access threads are silently downgraded to read‑only on continuation turns, undermining trust in permission profiles.
- **macOS resource leaks**: `#25744` documents zombie process accumulation from Computer Use / MCP helpers, causing HID lag and WindowServer stalls.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-02

## Today's Highlights

The team shipped a nightly release that transitions to the flash GA model when the experiment flag is present. Meanwhile, several high-severity bugs continue to dominate the issue tracker: the generalist agent still hangs indefinitely, sub-agents falsely report success after hitting turn limits, and shell commands frequently remain stuck waiting for input. Community activity remains high, with 50 issues and 50 PRs updated in the last 24 hours.

## Releases

**v0.45.0-nightly.20260602.g665228e98**  
- Transition to flash GA model when experiment flag is present (by @DavidAPierce)  
[Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.45.0-nightly.20260530.g013914071...v0.45.0-nightly.20260602.g66522)

No stable release in the last 24 hours.

## Hot Issues (Top 10 of 30 by Comment Count)

1. **#21409 – Generalist agent hangs** (👍 8)  
   The agent hangs forever when deferring to the generalist sub-agent, even for simple tasks like folder creation. Users report workarounds by instructing the model not to use sub-agents.  
   [google-gemini/gemini-cli Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

2. **#22323 – Subagent recovery after MAX_TURNS falsely reports success** (👍 2)  
   `codebase_investigator` sub-agent reports `status: "success"` and `Termination Reason: "GOAL"` even after hitting the turn limit before doing any analysis – a misleading termination bug that breaks trust in agent outputs.  
   [google-gemini/gemini-cli Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

3. **#24353 – Robust component-level evaluations**  
   An EPIC tracking 76 behavioral eval tests across 6 supported Gemini models, aiming to catch regressions at the component level. Community has been asking for more systematic testing.  
   [google-gemini/gemini-cli Issue #24353](https://github.com/google-gemini/gemini-cli/issues/24353)

4. **#25166 – Shell command execution gets stuck with "Waiting input"** (👍 3)  
   Simple commands (e.g., `ls`) hang after completion, showing the shell as active and awaiting input. A persistent reproducibility issue impacting daily workflows.  
   [google-gemini/gemini-cli Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

5. **#21968 – Gemini does not use skills and sub-agents enough**  
   Even with well-described custom skills (gradle, git), the agent rarely invokes them unless explicitly instructed. A significant usability gap for power users relying on automation.  
   [google-gemini/gemini-cli Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

6. **#18292 – Infinite self-referential loop with stream-json output**  
   `gemini -p "hy" --output-format stream-json` triggers an endless loop of internal reasoning and self-corrections (`"I misused write_todos"`). Closed? Still active discussion (5 comments).  
   [google-gemini/gemini-cli Issue #18292](https://github.com/google-gemini/gemini-cli/issues/18292)

7. **#21983 – Browser sub-agent fails in Wayland**  
   The browser sub-agent terminates with "GOAL" but actually fails, making it unusable on Wayland sessions.  
   [google-gemini/gemini-cli Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

8. **#26525 – Add deterministic redaction and reduce Auto Memory logging**  
   Auto Memory sends local transcript content to the model before redacting secrets – a security/privacy concern. Community has flagged the need for deterministic redaction.  
   [google-gemini/gemini-cli Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

9. **#23571 – Model frequently creates tmp scripts in random spots**  
   When shell execution is restricted, the model scatters edit scripts across the workspace, creating a cleanup nightmare.  
   [google-gemini/gemini-cli Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)

10. **#22186 – get-shit-done output hook causes crash**  
    The crash occurs near the end of a "get-shit-done" session when printing the user summary. A regression that disrupts one of the most popular workflows.  
    [google-gemini/gemini-cli Issue #22186](https://github.com/google-gemini/gemini-cli/issues/22186)

## Key PR Progress (10 of 20 most recently updated)

1. **#204 – SANDBOX_PORTS env var**  
   Enables port mapping in the sandboxed execution environment – a frequently requested feature for web app testing.  
   [google-gemini/gemini-cli PR #204](https://github.com/google-gemini/gemini-cli/pull/204)

2. **#203 – Switch to shell tool, deprecating terminal**  
   Replaces the legacy terminal tool with a more reliable shell tool, addressing historical hanging issues.  
   [google-gemini/gemini-cli PR #203](https://github.com/google-gemini/gemini-cli/pull/203)

3. **#201 – env flags SANDBOX_MOUNTS, SANDBOX_ENV**  
   Adds environment variable support for sandbox mounts and environment flags, improving containerized workflow flexibility.  
   [google-gemini/gemini-cli PR #201](https://github.com/google-gemini/gemini-cli/pull/201)

4. **#197 – Publish Docker image alongside npm package**  
   Enables CI-based Docker image publishing, making it easier to run Gemini CLI in containerized environments.  
   [google-gemini/gemini-cli PR #197](https://github.com/google-gemini/gemini-cli/pull/197)

5. **#193 – Colorize code for files about to be written**  
   Syntax-highlights new file content instead of showing a raw diff, significantly improving readability for code generation outputs.  
   [google-gemini/gemini-cli PR #193](https://github.com/google-gemini/gemini-cli/pull/193)

6. **#192 – Update core system prompt with new application workflow**  
   Restructures prompt into distinct workflows ("Software Engineering Tasks" vs "New Application"), with detailed step-by-step guidance – part of ongoing agent behavior improvements.  
   [google-gemini/gemini-cli PR #192](https://github.com/google-gemini/gemini-cli/pull/192)

7. **#190 – Upgrade @google/genai to latest**  
   Gains access to thinking budget configuration for 2.5 thinking models, key to tuning model deliberation time.  
   [google-gemini/gemini-cli PR #190](https://github.com/google-gemini/gemini-cli/pull/190)

8. **#185 – Follow-up fixes from flickering PR**  
   Addresses terminal flickering on resize by refactoring history rendering – a persistent UX annoyance.  
   [google-gemini/gemini-cli PR #185](https://github.com/google-gemini/gemini-cli/pull/185)

9. **#186 – hop into sandbox**  
   Allows quick entry into the sandbox environment, streamlining iterative development and debugging.  
   [google-gemini/gemini-cli PR #186](https://github.com/google-gemini/gemini-cli/pull/186)

10. **#188 – Allow tool groups + following content to be updateable**  
    Fixes a "bleeding" issue where fast tool group transactions could cause stale content to appear, improving UI consistency.  
    [google-gemini/gemini-cli PR #188](https://github.com/google-gemini/gemini-cli/pull/188)

## Feature Request Trends

The most consistent feature demand is **AST-aware tools** – issues #22745, #22746, #22747 call for AST-based file reads, search, and codebase mapping to improve precision and reduce token waste. Closely related is the demand for **better agent orchestration**: skills and sub-agents should be used more autonomously (#21968), and the agent should self-awarely guide users (#21432). Another strong trend is **evaluation infrastructure** – users and maintainers want robust, component-level evals (#24353, #23166) to catch regressions early. Finally, **sandbox improvements** (port mapping, environment variables, Docker publishing) reflect growing interest in containerized development with Gemini CLI.

## Developer Pain Points

- **Agent hangs and false success** – The generalist agent hangs (#21409) and sub-agents report success when they actually hit limits (#22323) are the most frequently upvoted bugs.
- **Shell command stuck after completion** (#25166) breaks basic automation and has caused significant frustration (👍 3).
- **Browser sub-agent incompatibility with Wayland** (#21983) blocks Linux users.
- **Auto Memory security concerns** (#26525) – transcripts are sent to the model before redaction, and invalid patches are silently skipped (#26523, #26522).
- **Settings.json ignored** (#22267) – the browser agent ignores user overrides, undermining configuration expectations.
- **Permission errors with OAuth** (#26405) – 403 errors despite successful login, affecting paid subscribers.
- **Crash on get-shit-done** (#22186) – a key workflow-breaking regression.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-02

## Today’s Highlights
A new patch release v1.0.57 improves error messages during `copilot update` and adds real-time feedback for plugin slash commands. The community is most active around model availability gaps (Copilot CLI missing org-enabled models that VS Code has) and a recurring clipboard-broken-on-Windows issue introduced in v1.0.56. Several new bugs surfaced around context loss with Claude Sonnet 4.6, infinite auto-compaction loops with large instruction files, and shell-specific sentinel errors.

## Releases
Two versions published in the last 24 hours:

- **v1.0.57** (2026-06-01)
  - Actionable error message when GitHub API rate limit is hit during `copilot update`
  - Plugin slash commands (`/plugin install`, `uninstall`, `update`, `marketplace add/remove/browse`) now show immediate feedback while the operation is in progress
  - Canceling a running shell command (Ctrl+C) behaviour improved
- **v1.0.57-5** (2026-06-01)
  - Fixes and changes (no detailed changelog provided)

## Hot Issues (10 Noteworthy)

1. **#1703 – Copilot CLI does not list all org-enabled models (e.g. Gemini 3.1 Pro)**  
   *27 comments, 53 👍* – A persistent mismatch between CLI and VS Code model lists. Users report CLI shows fewer models despite org settings allowing them. High impact for organisations relying on CLI.  
   [GitHub](https://github.com/github/copilot-cli/issues/1703)

2. **#3609 – Cannot copy from console since v1.0.56**  
   *2 comments* – Clipboard notification appears but clipboard is not updated. Regression affecting all platforms.  
   [GitHub](https://github.com/github/copilot-cli/issues/3609)

3. **#3622 – Copy to clipboard silently fails on Windows**  
   *0 comments* – Confirmed separate Windows-specific clipboard bug (works in 1.0.48). Likely related to #3609 but platform-specific.  
   [GitHub](https://github.com/github/copilot-cli/issues/3622)

4. **#3623 – Copilot CLI loses conversation context quickly when using Claude Sonnet 4.6**  
   *0 comments* – Context drops after few exchanges, reducing usefulness for multi-turn tasks.  
   [GitHub](https://github.com/github/copilot-cli/issues/3623)

5. **#3621 – Auto-compaction loops infinitely when instruction files are large**  
   *0 comments* – Large `copilot-instructions.md` files trigger endless compaction, wiping working memory and breaking multi-step workflows.  
   [GitHub](https://github.com/github/copilot-cli/issues/3621)

6. **#3619 – Bash tool exit-code sentinel uses bash $? syntax in fish, breaking exit-code detection**  
   *0 comments* – Fish shell users get error messages from sentinel commands, and exit codes are not read correctly.  
   [GitHub](https://github.com/github/copilot-cli/issues/3619)

7. **#3601 – Bash tool drops non-ASCII characters due to LC_CTYPE=C**  
   *1 comment* – File paths with CJK, accented, or emoji characters become unresolvable. Critical for international users.  
   [GitHub](https://github.com/github/copilot-cli/issues/3601)

8. **#3596 – Error loading model list: Error: Not authenticated when resuming a session**  
   *1 comment, 2 👍* – Session-specific authentication loss. User must start new session to use `/model` command.  
   [GitHub](https://github.com/github/copilot-cli/issues/3596)

9. **#3516 – CLI violates instructions by ignoring mandatory LSP usage**  
   *1 comment* – Model uses grep/glob even when LSP is available and explicitly required. Pattern of instruction non-compliance.  
   [GitHub](https://github.com/github/copilot-cli/issues/3516)

10. **#3620 – Ctrl-c has too many overloads, causing unexpected actions**  
    *0 comments* – Ctrl+C triggers copy, empty prompt line, or cancel depending on context. Users request single clear behaviour.  
    [GitHub](https://github.com/github/copilot-cli/issues/3620)

## Key PR Progress
Only one pull request was updated in the last 24 hours: **#3473** (open, spam – contains promotional content for Temu/GCash). No meaningful engineering PRs were merged or opened today.

## Feature Request Trends
- **Session improvements**: Natural-language session lookup (`copilot --resume "<query>"`, #3615) and `-r` shorthand for `--resume` (#1914) indicate demand for easier session navigation.
- **Model transparency**: Users want full parity between CLI and VS Code model lists (#1703) and support for generic local inference endpoints (BYOM for OpenAI-compatible servers, #3624).
- **Plugin and skill organisation**: Feature requests for subfolder support in skills (#1632) and declarative task-graph for plugin sub-agents (#3613) show growing complexity in plugin ecosystems.
- **UI controls**: Toggle to hide tool call streaming output (#3614) and more granular MCP permission configuration (#3028, #768) are frequently requested.
- **Platform parity**: Better fish shell support (#3619) and aarch64 Linux binary fix (#2060) are recurring themes.

## Developer Pain Points
1. **Model inconsistency**: Models enabled in org settings appear in VS Code but are missing in CLI (#1703). Causes confusion and limits adoption for team workflows.
2. **Clipboard regressions**: Copy-to-clipboard silently fails since v1.0.56, especially on Windows (#3609, #3622). Breaks a core user expectation.
3. **Context management failures**: Rapid context loss (#3623) and infinite compaction loops (#3621) make long sessions unreliable. Both are high-frequency complaints.
4. **Shell compatibility issues**: Bash tool uses bash-specific `$?` in fish (#3619) and sets `LC_CTYPE=C` (#3601), breaking international paths and exit code handling.
5. **Authentication instability**: Session-specific “Not authenticated” errors (#3596) force restarting sessions, disrupting workflows.
6. **Model instruction non-compliance**: The agent ignores configuration rules about tool usage (#3516), undermining trust in deterministic behaviour.
7. **Key binding ambiguity**: Overloaded Ctrl+C (#3620) leads to accidental actions; users want a dedicated cancel key that does not interfere with clipboard copy.

*Generated from data provided for 2026-06-02. Data source: github.com/github/copilot-cli*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-02

## Today’s Highlights

A single new enhancement request (#2416) asks to whitelist Zoo Code, the community fork of Roo Code, as a third-party coding agent—highlighting ongoing interest in ecosystem compatibility. On the PR front, a critical fix for OAuth token persistence (#2414) and a correction to the `/undo` command’s wire-turn mapping (#2386) are nearing completion. No new releases were published today.

## Releases

**None** — The last release remains unchanged. No new versions or tags were created in the past 24 hours.

## Hot Issues

*(Only two issues were updated in the last 24h; both are covered below for completeness.)*

1. **[#2416 – Enhancement: Add Zoo Code to the third-party coding agent API whitelist](https://github.com/MoonshotAI/kimi-cli/issues/2416)** ⬜ Open  
   *Why it matters:* Zoo Code, the active community successor to the abandoned Roo Code project, currently gets a 403 error when calling the Kimi Code API. Users want the same whitelist treatment that Roo Code previously enjoyed. No community reactions yet (0 comments, 0 👍), but the issue signals a demand for backward compatibility with forked tools.

2. **[#1914 – Bug: Installation fails when GitHub is unreachable](https://github.com/MoonshotAI/kimi-cli/issues/1914)** ✔️ Closed  
   *Why it matters:* The `uv` installer fetches binaries from GitHub Releases, breaking installs in regions with restricted access (e.g., China). The closure implies a fix was implemented (likely a mirror or fallback), but the underlying pain point of single-source distribution remains relevant for global teams. 0 comments, 0 👍.

## Key PR Progress

*(All four PRs updated in the last 24h are included.)*

1. **[#1741 – feat: add /copy command for assistant response](https://github.com/MoonshotAI/kimi-cli/pull/1741)** ⬜ Open  
   Adds a shell-level `/copy` command that copies the latest assistant response to the clipboard. Implements `copy_text_to_clipboard()` in `clipboard.py` and adds tab-completion support. A straightforward productivity boost for CLI users.

2. **[#2414 – fix(auth): avoid persisting OAuth token before config validation](https://github.com/MoonshotAI/kimi-cli/pull/2414)** ⬜ Open  
   Validates the returned model list and default-model selection *before* writing OAuth credentials. If config saving fails, the credentials are rolled back. Includes regression tests for failure modes. This prevents auth tokens from being stored with invalid configurations—a critical reliability fix.

3. **[#2386 – fix(session): map undo wire turns to context turns](https://github.com/MoonshotAI/kimi-cli/pull/2386)** ⬜ Open  
   Resolves #1974. The `/undo` and fork operations previously used a `wire.jsonl` `TurnBegin` index for both wire and context truncation, which broke when non‑message turns (e.g., slash commands) existed. Now properly maps wire turns to context turns, ensuring undo works correctly in all session states.

4. **[#2389 – fix(tools): include trailing output in error briefs and render brief as plain text](https://github.com/MoonshotAI/kimi-cli/pull/2389)** ✔️ Closed  
   When a shell command fails, the error brief now includes trailing output (the final lines of stderr/stdout) and is rendered as plain text instead of JSON. Merged, improving error readability for tool-calling workflows.

## Feature Request Trends

Based on the open issues and PR discussions, the community is currently focusing on two areas:

- **Third‑party API whitelisting** – The push to include Zoo Code (and by extension, any active fork of Roo Code) suggests users want seamless integration with popular coding agents rather than being locked into the official Roo Code.
- **CLI usability enhancements** – The `/copy` command proposal (#1741) and ongoing work on `/undo` (#2386) indicate a demand for more interactive, session‑friendly commands that mimic IDE‑like behavior inside the terminal.

## Developer Pain Points

1. **Installation blocked by GitHub access (#1914)** – Users in regions where GitHub is unreachable cannot install the CLI because `uv` downloads binaries exclusively from GitHub Releases. While the issue is closed, a long‑term solution (e.g., alternative mirrors or CDN) has not been discussed publicly.

2. **OAuth config storage hazards (#2414)** – The current authorization flow can write OAuth tokens even when the resulting configuration is invalid, requiring future manual cleanup. This is both a security concern (orphaned tokens) and a reliability issue.

3. **Undo consistency with non‑message turns (#2386)** – The `/undo` command breaks when a slash command or other non‑user action creates a turn without a corresponding context message. Developers using local tools or slash‑commands regularly hit this, making session recovery unreliable.

---

*Generated from GitHub data for `MoonshotAI/kimi-cli` as of 2026-06-02T23:59 UTC.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-02

## Today's Highlights
A major regression in OpenCode Desktop v1.15.13 dominated today’s discussion: MCP servers work correctly via CLI but the desktop UI shows “No MCPs configured” across multiple platforms. The community also rallied for adjusting usage limits after DeepSeek V4 Pro’s permanent 75% price cut. On the PR front, a critical fix for MCP status updates landed, and a new location-based permission service was merged.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#28846 – Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)**  
   *43 comments, 61 👍*  
   A highly upvoted request to pass the steep API price drop to users. The community wants lower subscription caps or cheaper tiers for the Go service.

2. **[#16331 – Permissions ignored](https://github.com/anomalyco/opencode/issues/16331)**  
   *40 comments, 8 👍*  
   A long-standing bug where `opencode.json` permission rules are not always respected. Despite configuration, some operations bypass the allow/deny list.

3. **[#27589 – TUI fails on Alpine Linux (musl) in 1.14.50: getcontext symbol not found](https://github.com/anomalyco/opencode/issues/27589)**  
   *24 comments, 12 👍*  
   Regression introduced in v1.14.50 – the OpenTUI library requires `getcontext` which is unavailable on musl-based systems. Blocks many Linux users.

4. **[#8832 – opencode not respecting permissions](https://github.com/anomalyco/opencode/issues/8832)**  
   *15 comments, 7 👍*  
   A separate report of permission misbehavior: specific bash commands aren’t being restricted as defined in the config, causing security concerns.

5. **[#25940 – Opencode crashes the entire terminal session right after open](https://github.com/anomalyco/opencode/issues/25940)** (reopened)  
   *11 comments, 2 👍*  
   A critical crash that kills the terminal when opening any directory. Reopened after auto-close – still not fully resolved.

6. **[#27436 – permission required cannot select](https://github.com/anomalyco/opencode/issues/27436)**  
   *9 comments, 5 👍*  
   UI bug: “Allow once” and “Reject” buttons are unclickable, “Allow always” loops endlessly, and the text input is disabled. Sessions get stuck.

7. **[#30104 – Desktop app MCP tab shows 'No MCPs configured' despite MCP servers being connected](https://github.com/anomalyco/opencode/issues/30104)**  
   *8 comments, 9 👍*  
   Head of the wave of identical reports: MCP works in CLI but desktop UI shows empty state. Likely a sidecar sync issue introduced in v1.15.13.

8. **[#29992 – Auto-scroll stops working after manually scrolling and returning to bottom](https://github.com/anomalyco/opencode/issues/29992)**  
   *8 comments, 12 👍*  
   A UX regression: after scrolling up, the viewport no longer auto-follows new assistant content – a widely felt annoyance.

9. **[#13456 – TUI model selection gets overwritten by agent default model](https://github.com/anomalyco/opencode/issues/13456)** (closed)  
   *8 comments, 4 👍*  
   A closed bug where manually picking a model is overridden by an `createEffect` – still relevant for users who want manual control.

10. **[#30265 – MCP Broken on v1.15.13](https://github.com/anomalyco/opencode/issues/30265)**  
    *6 comments, 3 👍*  
    Fresh report: after updating to v1.15.13 the MCP list is empty, even though config is unchanged. Confirms the regression pattern.

**Notable mention:** Multiple duplicate MCP visibility reports (#30070, #30130, #30098, #30202, #30141, etc.) underscore the severity of this v1.15.13 bug.

## Key PR Progress
1. **[#30220 – fix(app): restore deferred MCP status updates](https://github.com/anomalyco/opencode/pull/30220)** (closed)  
   Fixes the MCP UI emptiness bug by correcting a race condition in `useQueries()` – a lazy enablement issue. Directly addresses today’s top pain point.

2. **[#30085 – fix(opencode): grant MCP tool permissions in subagent sessions](https://github.com/anomalyco/opencode/pull/30085)** (closed)  
   Solves #16491: subagents spawned via Task tool can now execute MCP tools. Previously permission checks failed even though tools were visible.

3. **[#30287 – feat(core): add location-based permission service](https://github.com/anomalyco/opencode/pull/30287)** (closed)  
   Introduces `PermissionV2` – a scoped permission system with action/resource/decision schemas and pending request handling. Replaces legacy storage.

4. **[#30300 – fix(tui): preserve live parts during session hydration](https://github.com/anomalyco/opencode/pull/30300)** (closed)  
   Stops live streamed content from being overwritten by stale HTTP snapshot data when the TUI initializes. Includes regression tests.

5. **[#29666 – fix(opencode): enforce storage path invariants](https://github.com/anomalyco/opencode/pull/29666)** (closed)  
   Fixes Windows path bugs where backslash rows caused sessions to disappear from lists. Paths are now stored as forward slashes.

6. **[#29977 – fix(core): include git store hash in project ID](https://github.com/anomalyco/opencode/pull/29977)** (open)  
   Prevents independent clones of the same repo from merging into one project by hashing the actual store path.

7. **[#30312 – fix: export v2 stylesheets and declare core node types](https://github.com/anomalyco/opencode/pull/30312)** (closed)  
   Build fix: exports v2 CSS from the UI package and declares Node 24 SQLite types for the core adapter.

8. **[#30307 – docs(ecosystem): add opencode-reflection — judge layer for premature agent stops](https://github.com/anomalyco/opencode/pull/30307)** (open)  
   A community plugin that fires on `session.idle` to detect and correct premature agent stops – claims 78% of stops are premature.

9. **[#30211 – fix(provider): preserve config precedence after model hooks](https://github.com/anomalyco/opencode/pull/30211)** (open)  
   Fixes #25630: after plugin `provider.models()` hooks run, the user’s config-provider precedence was lost. Ensures manual overrides stick.

10. **[#30309 – refactor(core): migrate accounts and load file agents](https://github.com/anomalyco/opencode/pull/30309)** (open)  
    Moves account service, OAuth, token refresh into `@opencode-ai/core/account`. Also loads Markdown-backed agents from config directories.

## Feature Request Trends
- **Dynamic pricing/model limits**: The DeepSeek V4 Pro price drop (#28846) has users demanding proportional adjustments to OpenCode Go usage caps. Expect more requests for flexible, provider-aware billing.
- **Improved MCP UI visibility**: The v1.15.13 regression has amplified calls for a robust MCP status panel that mirrors CLI results in real time.
- **Permission system reboot**: With two long-standing permission bugs (#16331, #8832) and the new `PermissionV2` PR, the community is pushing for a more predictable, scoped permission model (especially for subagents and MCP tools).
- **Better provider/model integration**: Requests for loading approved models from Requesty (#16344), support for Kimi K2.6 thinking headers (#29619), and MiniMax-M3 model addition (#30201) indicate a desire for deeper provider compatibility.
- **Session management improvements**: Features like resuming in the original directory (#28581) and fixing multi-directory session status (#30155) show demand for more robust workspace handling.

## Developer Pain Points
- **Permission system inconsistency**: Multiple reports of `opencode.json` permissions being ignored or causing UI deadlocks. The system lacks clear logging and fails silently.
- **Desktop MCP UI regression in v1.15.13**: Over a dozen duplicates filed today – MCP servers work via CLI but the desktop panel is empty. Workarounds exist but the root cause (lazy sidecar sync) is still being patched.
- **Cross-platform TUI crashes**: Alpine Linux (musl) users are blocked by `getcontext` linking errors. Terminal crashes on startup also plague some Linux configurations.
- **UI/UX regressions**: Auto-scroll breaking, model selection being overridden, and the permission button unclickability degrade the daily experience. Users feel regressions are shipped too often.
- **Windows path normalization**: Sessions disappearing from lists due to backslash vs forward slash mismatch is a recurring friction, partially fixed in #29666 but still affecting open issues.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-02

## Today's Highlights
The Pi ecosystem saw extensive community activity with 43 issues and 20 pull requests updated in the last 24 hours. Model support continues to be a major theme, with multiple contributions adding MiniMax-M3, Gemini 3.5 Flash, and Kimi K2.6 fixes. A cluster of TUI-related bugs — overlay focus, CJK rendering, Kitty images, and hardware cursor handling — received several targeted patches. The platform also saw important architectural improvements: configuration injection, context boundary controls, and a new `ctx.isInteractive` API for extensions.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

### #5089 – [bug] Doesn't seem to respect timeoutMs past a certain value  
**Comments: 22 | 👍: 2**  
Users report that long-running operations (e.g., reading large text files on underpowered hardware) cause timeouts even when a high `timeoutMs` is set. This is a critical reliability bug affecting local model users.  
[Link](https://github.com/earendil-works/pi/issues/5089)

### #4877 – [bug] Session folder collision  
**Comments: 8 | 👍: 2**  
Sessions with different paths (e.g., `/a/b/c/d` vs `/a-b/c-d`) can map to the same folder because of how slashes are replaced with dashes. A simple but potentially confusing design flaw.  
[Link](https://github.com/earendil-works/pi/issues/4877)

### #5271 – Minimax m3 support  
**Comments: 6 | 👍: 0**  
Request to add the newly released MiniMax-M3 model, which boasts 1M-context MSA and native multimodality. Reflects the rapid pace of model integration needed in the community.  
[Link](https://github.com/earendil-works/pi/issues/5271)

### #4180 – [bug] Links not clickable anymore  
**Comments: 6 | 👍: 0**  
A regression after a recent update (likely the coding agent alternate term mode) broke terminal hyperlinks. This degrades the UX for developers relying on clickable URLs in chat output.  
[Link](https://github.com/earendil-works/pi/issues/4180)

### #5229 – [bug] MiniMax on OpenRouter is broken  
**Comments: 6 | 👍: 1**  
OpenRouter returns a 400 error due to `developer` role not being accepted for MiniMax models. A provider compatibility issue that blocks users of this popular free model.  
[Link](https://github.com/earendil-works/pi/issues/5229)

### #2999 – [bug] Expose the available SYSTEM PROMPT variables to custom SYSTEM.md  
**Comments: 6 | 👍: 2**  
Custom `SYSTEM.md` files do not interpolate template variables like the default system prompt does. A long-standing request that limits customization flexibility.  
[Link](https://github.com/earendil-works/pi/issues/2999)

### #5261 – [last read] Inject TUI config instead of reading process.env inside pi-tui  
**Comments: 6 | 👍: 0**  
The TUI class reads `PI_*` environment variables directly at field-initializer time, making testing and bundling difficult. A clean architecture improvement that aligns with modern dependency injection.  
[Link](https://github.com/earendil-works/pi/issues/5261)

### #4449 – Add anthropic-vertex provider  
**Comments: 5 | 👍: 0**  
Users want access to Anthropic models hosted on Vertex AI (now “Gemini Enterprise Agent Platform”). The author has a working local PR, indicating strong demand for this provider.  
[Link](https://github.com/earendil-works/pi/issues/4449)

### #5011 – Add support for Gemini 3.5 Flash on Google Vertex AI  
**Comments: 3 | 👍: 4**  
The newly released Gemini 3.5 Flash is missing from the google-vertex provider, causing a `FailoverError`. With 4 upvotes, this is one of the most-wanted model additions this week.  
[Link](https://github.com/earendil-works/pi/issues/5011)

### #3885 – Provide a mechanism for setting `hyperlinks: true` in tmux  
**Comments: 3 | 👍: 3**  
A recent commit forces `hyperlinks: false` in tmux. Users want an opt-in or auto-detection to restore OSC 8 hyperlink support in multiplexer environments.  
[Link](https://github.com/earendil-works/pi/issues/3885)

---

## Key PR Progress

### #5310 – fix(tui): guard against undefined children in Box and Container render/invalidate loops  
A subtle crash occurs when an extension returns `undefined` from `renderCall`/`renderResult`. This PR adds a guard to prevent `TypeError` on child render.  
[Link](https://github.com/earendil-works/pi/pull/5310)

### #5308 – fix: sanitize local model artifacts in tool prepareArguments  
Local models (Qwen, DeepSeek) often leak YAML frontmatter or produce malformed JSON in tool calls. This PR adds sanitization to avoid validation failures — a direct fix for the widely reported #5307.  
[Link](https://github.com/earendil-works/pi/pull/5308)

### #5302 – Add ui_prompt_start/ui_prompt_end extension events  
Two new events fire when a blocking `ctx.ui` dialog opens / closes, enabling host integrations (status bars, terminal multiplexers) to react to modal state.  
[Link](https://github.com/earendil-works/pi/pull/5302)

### #5269 – feat(coding-agent): add ctx.isInteractive to distinguish TUI from RPC mode  
A regression made RPC mode appear interactive; this PR adds a proper flag so extensions can behave differently in automated vs. manual sessions.  
[Link](https://github.com/earendil-works/pi/pull/5269)

### #5296 – fix(tui): keep Kitty images visible in WezTerm  
Reverts a previous fix that broke Kitty image rendering in WezTerm. Now uses a more targeted cursor-up/down approach only for tall images, solving a visual regression seen since #4461.  
[Link](https://github.com/earendil-works/pi/pull/5296)

### #5235 – Feat/issue 5129 tui overlay focus  
Fixes #5129 where an overlay created without `overlay: true` would steal focus from a sibling overlay, leaving it non-interactive but still visible.  
[Link](https://github.com/earendil-works/pi/pull/5235)

### #5284 – feat(ai): add MiniMax-M3 to minimax and minimax-cn  
Adds the flagship MiniMax-M3 model with 512K context and native multimodal input. A rapid response to the model’s weekend release.  
[Link](https://github.com/earendil-works/pi/pull/5284)

### #5281 – feat(coding-agent): Support keybindings for all commands  
Unifies built-in and extension command keybinding configuration via a `cmd.<name>` convention. Addresses a common gap where extension commands lacked keyboard shortcuts.  
[Link](https://github.com/earendil-works/pi/pull/5281)

### #5277 – feat: add gitContextBoundary setting to stop AGENTS.md ancestor walk at git root  
Prevents a home-directory `AGENTS.md` from leaking into every project when `$HOME` is a git repo. A thoughtful safety measure for users with global context files.  
[Link](https://github.com/earendil-works/pi/pull/5277)

### #5221 – Fix OpenRouter reasoning instruction role  
Changes OpenRouter reasoning system prompts from `developer` to `system` role to match OpenRouter’s API schema, fixing a recurring error for reasoning models.  
[Link](https://github.com/earendil-works/pi/pull/5221)

---

## Feature Request Trends

1. **Model provider expansion** – The strongest signal: requests for MiniMax-M3, Gemini 3.5 Flash, Anthropic Vertex, ZAI Coding Plan China, and Kimi K2.6 compatibility. Users expect Pi to stay current with LLM releases.  
2. **Extension API enrichment** – New events (`ui_prompt_start/end`), `ctx.isInteractive`, and per-command keybindings show demand for tighter integration points between Pi and external tools.  
3. **Session and configuration flexibility** – Custom system prompt interpolation, optional session naming, escape-hatch settings for tmux hyperlinks, and `gitContextBoundary` all point to a desire for more environment-aware and user-customizable behavior.

---

## Developer Pain Points

- **Timeout and timeoutMs failures** – Local model users on underpowered hardware continue to hit hard timeouts even with high or infinite settings (#5089, #5294).  
- **Provider API inconsistencies** – OpenRouter, Bedrock, and GitHub Copilot each have subtle role/field mismatches that break requests (#5229, #4975, #3534).  
- **TUI rendering regressions** – Frequent flickering, broken hyperlinks, mispositioned overlays, and CJK boundary errors suggest the TUI refresher is fragile under extension use (#4180, #5129, #5293, #5311).  
- **Bundled app / SDK packaging** – Issues like runtime `package.json` dependency (#5226) and `getPackageDir()` assumptions cause pain for developers embedding Pi into other tools.  
- **CLI parsing incompatibilities** – Arguments starting with `@` are misinterpreted as file paths (#5267), a small but sharp edge case.  
- **Internationalization** – CJK IME placement, wide-char overlays, and hardware cursor markers remain consistent trouble spots (#5283, #5295).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the **Qwen Code Community Digest** for **2026-06-02**.

---

## Qwen Code Community Digest: 2026-06-02

### Today's Highlights
Today’s activity indicates a strong focus on **hardening local model integrations** and **refining the developer experience (DX)** for the ongoing `v0.17.0` release. A critical fix is in progress for streaming timeouts (Issue #4604), which has been a major pain point for users running local models like Qwen 3.6. Meanwhile, the community continues to push for better **session management** tools (Issue #4679) and improved **UI/UX**, including a fix for Vim mode key leaks (Issue #4675). The PR pipeline is active with targeted fixes for memory, auto-mode safety, and sub-agent concurrency.

### Releases
- **v0.17.0-nightly.20260602.cea15a118**: A routine nightly release. No major feature changes documented. The main-line `v0.17.0` release appears to be in a stabilization phase.

### Hot Issues

1.  **#3384: Unable to add OpenAI-compatible local LLM** [![GitHub Issue](https://img.shields.io/badge/Open-3384-blue)]
    - **Summary**: User cannot connect to a local Qwen 3.6 model served by VLLM via the OpenAI-compatible endpoint, despite following documentation.
    - **Why it matters**: This highlights a recurring onboarding friction for users with self-hosted, private models. The issue has 11 comments and a +1, indicating significant community interest. It remains open, suggesting a configuration or detection bug.
    - [Link](https://github.com/QwenLM/qwen-code/issues/3384)

2.  **#4663: Add MiniMax-M3 and checkbox-based model selection** [![GitHub Issue](https://img.shields.io/badge/Open-4663-blue)]
    - **Summary**: Request to add the official `MiniMax-M3` model ID as a selectable option and replace the comma-separated text input for model IDs with a checkbox/multi-select UI.
    - **Why it matters**: This request reflects a community desire for a more polished, user-friendly API key setup experience, moving away from error-prone free-text fields.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4663)

3.  **#4657: Version v0.17.0 Using Qwen Code + Ollama - Cannot complete tasks** [![GitHub Issue](https://img.shields.io/badge/Open-4657-blue)]
    - **Summary**: After the timeout bug fix, users are still reporting that Qwen Code v0.17.0 cannot complete tasks (e.g., creating an eBook) when using Ollama + Qwen 3.6 locally.
    - **Why it matters**: This is a critical regression for users relying on local models. The 6 comments suggest the fix might be incomplete or introduces new issues.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4657)

4.  **#4669: Statusline ANSI colors washed out and duplicate context indicator** [![GitHub Issue](https://img.shields.io/badge/Closed-4669-ff69b4)]
    - **Summary**: User requests `respectUserColors` and `hideContextIndicator` options for the statusline, noting that ANSI color codes in custom statusline output are not preserved.
    - **Why it matters**: This reflects a demand for deeper customization and theming from advanced users, especially those integrating Qwen Code into tailored terminal environments.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4669)

5.  **#4604: API Error: terminated (cause: Body Timeout Error)** [![GitHub Issue](https://img.shields.io/badge/Open-4604-blue)]
    - **Summary**: User encounters a "Body Timeout Error" when running prompts to process webpages. This is a high-traffic issue with 5 comments.
    - **Why it matters**: This is a core infrastructure problem that affects user experience and stability, particularly for long-running agentic tasks involving web scraping.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4604)

6.  **#4679: SDK: support resuming an unfinished previous turn without a synthetic "continue" prompt** [![GitHub Issue](https://img.shields.io/badge/Open-4679-blue)]
    - **Summary**: Request for a first-class SDK method to resume an interrupted session turn without injecting a fake "continue" message.
    - **Why it matters**: This is a high-value feature for API consumers and tool builders who want clean session resumption logic. It has 2 comments, suggesting early-stage interest.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4679)

7.  **#4615: Add project-scoped .mcp.json support with pending approval semantics** [![GitHub Issue](https://img.shields.io/badge/Open-4615-blue)]
    - **Summary**: Request for project-level `.mcp.json` configuration files with a pending-approval state before any MCP server is started.
    - **Why it matters**: This addresses a key security and workflow concern for teams using MCP, allowing them to control which MCP servers are active per project without global settings.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4615)

8.  **#4676: Auto-mode classifier times out too easily; loosen stage timeouts and disable thinking in all stages** [![GitHub Issue](https://img.shields.io/badge/Open-4676-blue)]
    - **Summary**: The two-stage LLM classifier for auto-approval mode fails "closed" on any timeout, blocking the action. User requests looser timeouts and disabling think tokens in stages.
    - **Why it matters**: This is a usability blocker for the powerful auto-approval mode. It has 1 comment and a +1, indicating community validation of the problem.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4676)

9.  **#4588: Epic: Optimize qwen-code TUI display, spacing, tools, and branding** [![GitHub Issue](https://img.shields.io/badge/Open-4588-blue)]
    - **Summary**: A tracking issue for a TUI optimization pass, covering five recurring problems: normal answers exposing tool outputs, excessive vertical spacing, lack of visual distinctiveness for Qwen, etc.
    - **Why it matters**: This is a comprehensive UX epic that aggregates community feedback on making the CLI feel quieter, denser, and more professional.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4588)

10. **#4686: Bug: Streaming/outputting repetitive garbage with Qwen3.7-max** [![GitHub Issue](https://img.shields.io/badge/Open-4686-blue)]
    - **Summary**: User on v0.17.0 reports that Qwen 3.7-Max, when accessed via DashScope, falls into an infinite repetition loop during response generation.
    - **Why it matters**: This is a critical bug affecting a premium model, impacting output quality and user trust. It can lead to infinite token consumption and wasted API costs.
    - [Link](https://github.com/QwenLM/qwen-code/issues/4686)

### Key PR Progress

1.  **#3557: fix(insight): Harden insight facet normalization and empty qualitative handling** [![GitHub PR](https://img.shields.io/badge/Closed-3557-ff69b4)]
    - **Summary**: Fixes the `/insight` command by adding robust normalization for session facet data and handling empty qualitative sections, preventing crashes and non-functional HTML reports.
    - **Why it matters**: This addresses a long-standing community complaint (Issues #2939, #2658, #3027, #2773) about the `/insight` feature failing to generate proper reports.
    - [Link](https://github.com/QwenLM/qwen-code/pull/3557)

2.  **#4620: feat(cli): add CPU profiling support for Chrome DevTools analysis** [![GitHub PR](https://img.shields.io/badge/Open-4620-blue)]
    - **Summary**: Adds a `cpuProfiler` module that generates `.cpuprofile` files, which can be loaded into Chrome DevTools for performance analysis.
    - **Why it matters**: This is a powerful new tool for developers and advanced users to debug performance bottlenecks, addressing the need for better diagnostic tools.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4620)

3.  **#4577: feat(skills): add triage skill for issue/PR gatekeeping** [![GitHub PR](https://img.shields.io/badge/Open-4577-blue)]
    - **Summary**: Adds a `/triage` project skill that automates GitHub issue classification and PR admission review for CI/GitHub Actions.
    - **Why it matters**: This is a sophisticated automation feature for project maintainers, enabling automated workflows for managing open source contributions.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4577)

4.  **#4520: fix(core): truncate model-facing tool output** [![GitHub PR](https://img.shields.io/badge/Open-4520-blue)]
    - **Summary**: Moves tool-output truncation into `CoreToolScheduler`, so any tool returning string `llmContent` is bounded before being recorded into conversation history.
    - **Why it matters**: This is a critical performance and memory fix, preventing unbounded tool output from destabilizing the session, a common pain point in long-running tasks.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4520)

5.  **#4242: fix(cli): map rewind turns after compression** [![GitHub PR](https://img.shields.io/badge/Open-4242-blue)]
    - **Summary**: Correctly maps rewind targets after conversation compression, preventing issues with history navigation in compressed sessions.
    - **Why it matters**: This is a core fix for the rewind feature, ensuring it works correctly in long, compressed conversations where session management is crucial.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4242)

6.  **#4519: fix(core): honor output language in side queries** [![GitHub PR](https://img.shields.io/badge/Open-4519-blue)]
    - **Summary**: Ensures side queries follow the user's configured output language preference, a feature requested for consistency.
    - **Why it matters**: This is a UX fix for multi-lingual users, ensuring that auto-generated summaries and side-query outputs are in the correct language.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4519)

7.  **#4667: fix(core): add configurable bodyTimeout to prevent streaming timeout with local models** [![GitHub PR](https://img.shields.io/badge/Open-4667-blue)]
    - **Summary**: Adds a configurable `bodyTimeout` field (default 0 = disabled) to fix the 300s default idle timeout that kills slow local model connections during SSE streaming.
    - **Why it matters**: This is a direct fix for the "Body Timeout Error" (#4604) and is critical for users running local models on slower hardware.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4667)

8.  **#4681: fix(ask_user_question): add minLength/maxLength to header JSON Schema** [![GitHub PR](https://img.shields.io/badge/Open-4681-blue)]
    - **Summary**: Adds `minLength: 1` and `maxLength: 12` constraints to the `header` property in the `ask_user_question` tool's JSON Schema.
    - **Why it matters**: This is a small but smart UI fix that prevents LLMs from generating unusably long or empty headers, improving reliability of the interactive tool.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4681)

9.  **#4572: Harden auto mode self-modification checks** [![GitHub PR](https://img.shields.io/badge/Open-4572-blue)]
    - **Summary**: Hardens Auto Mode to prevent writes to Qwen Code configuration and instructions from bypassing the permission classifier and broad allow rules.
    - **Why it matters**: This is a security-critical PR that addresses the specific concerns raised in Issue #4676, preventing accidental or malicious self-modification in auto-approval mode.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4572)

10. **#4680: fix(core): loosen auto-mode classifier timeouts, disable stage-2 thinking** [![GitHub PR](https://img.shields.io/badge/Open-4680-blue)]
    - **Summary**: Closes Issue #4676 by increasing classifier timeouts and disabling thinking tokens in the second stage to prevent auto-mode from blocking legitimate actions.
    - **Why it matters**: This is the functional fix for the classifier timeout bug that was causing user workflow interruptions in auto-mode.
    - [Link](https://github.com/QwenLM/qwen-code/pull/4680)

### Feature Request Trends
- **Local LLM & Provider Integration**: A strong & persistent trend is improving support for local/private LLMs (VLLM, Ollama) and expanding provider options (MiniMax-M3). The community is pushing for better documentation, configurable timeouts, and smoother onboarding.
- **Session & Process Management**: Developers are actively requesting more robust session management, including SDK-level support for resuming interrupted turns, better `--resume` memory handling, and a non-blocking daemon prompt endpoint.
- **Security & Compliance**: Features like project-scoped `.mcp.json` with pending approval and hardened auto-mode self-modification checks highlight a growing demand for granular security controls.
- **UI/UX & Customization**: Requests for statusline customization (ANSI colors, hiding indicators), improved Vim mode handling, and a denser, more professional TUI (Epic #4588) show a community that wants greater control over their terminal experience.
- **Platform Expansion & Integration**: There's a clear interest in better integration with standard developer tools, such as the new CPU profiling tool, the `/triage` skill for GitHub workflows, and improvements to the MCP server stability.

### Developer Pain Points
- **Local Model Timeouts & Instability**: This is the highest-frequency pain point, with multiple issues (#4657, #4604, #4676) reporting timeouts and failed tasks when

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-02

## Today’s Highlights
The project underwent a pivotal identity change: **v0.8.49 renames DeepSeek TUI to CodeWhale**, with legacy binaries shipping as deprecation shims for one cycle. The community response is mixed — while the rebrand addresses long-term positioning, users are demanding performance fixes (input cache hit rate, token consumption) and better migration documentation. The day also saw a surge in PRs focused on i18n, NSIS Windows installer, and shell command shortcuts.

## Releases
**[v0.8.49](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.49)** — Project renamed to **CodeWhale**. Legacy `deepseek` / `deepseek-tui` binaries remain as deprecation shims (print warning + forward) and will be removed in v0.9.0. See `docs/REBRAND.md` for migration details.

## Hot Issues (10 selected)

1. **[#1177](https://github.com/Hmbown/CodeWhale/issues/1177) [bug] Input cache hit rate too low (25 comments)**  
   User compares unfavorably with DeepSeek-Reasonix (95%+ hit rate). *Why it matters*: Cache hit rate directly impacts API cost and latency for heavy users. Community is actively debating root cause.

2. **[#743](https://github.com/Hmbown/CodeWhale/issues/743) [bug] Token consumption increased significantly (14 comments)**  
   Reports 400 million tokens consumed in half a day. *Why it matters*: Suggests chat context is being duplicated or not pruned, leading to runaway costs. Top pain point for heavy users.

3. **[#2487](https://github.com/Hmbown/CodeWhale/issues/2487) [bug] Turn stalled – no completion signal received (11 comments)**  
   YOLO mode freezes with no recovery via `continue`. *Why it matters*: Blocks the core autonomous workflow; multiple users report same pattern.

4. **[#1969](https://github.com/Hmbown/CodeWhale/issues/1969) [question, migration] Will old sessions and skills survive rebrand to CodeWhale? (9 comments)**  
   Users worried about data loss during rename. *Why it matters*: Migration friction could stall adoption; maintainers need to clarify.

5. **[#1556](https://github.com/Hmbown/CodeWhale/issues/1556) [bug] Ghostty terminal flickering on macOS (5 comments)**  
   Render issue with Ghostty emulator. *Why it matters*: macOS users on modern terminal emulators are a growing segment; affects daily usage.

6. **[#1812](https://github.com/Hmbown/CodeWhale/issues/1812) [bug] TUI freeze on Windows 11 – crossterm poll (5 comments)**  
   Intermittent UI freeze, “crossterm poll” in stack traces. *Why it matters*: Windows support is critical for broader adoption; this is a high-impact stability bug.

7. **[#2328](https://github.com/Hmbown/CodeWhale/issues/2328) [bug] `exec_shell` mode inconsistency across Agent/YOLO modes (4 comments)**  
   Tool works in YOLO but fails in Agent mode despite docs claiming universal support. *Why it matters*: Breaks user expectations and forces mode switching.

8. **[#2492](https://github.com/Hmbown/CodeWhale/issues/2492) [bug] No cross-session memory (6 comments)**  
   Session memory is lost on restart; memory writes are not read back. *Why it matters*: Core UX deficiency for agents that need long-term context.

9. **[#2494](https://github.com/Hmbown/CodeWhale/issues/2494) [enhancement] macOS + iTerm2 user experience issues (3 comments)**  
   Compilation of issues: missing macOS keybindings, inability to stop generation, history selection problems. *Why it matters*: macOS is a primary dev platform; these UX gaps drive users away.

10. **[#2369](https://github.com/Hmbown/CodeWhale/issues/2369) [bug] Config paths fragmented across OS / Cygwin (3 comments)**  
    Config migration from `~/.deepseek` to `~/.codewhale` is inconsistent; user edits to legacy files are silently ignored. *Why it matters*: Creates silent data loss and confusion.

## Key PR Progress (10 selected)

1. **[#2568](https://github.com/Hmbown/CodeWhale/pull/2568) **feat(i18n): localize all queue command messages across 7 locales****  
   Adds 15 new MessageId variants for `/queue` commands. *Impact*: Paves way for full CLI internationalization; 7 locales covered.

2. **[#2565](https://github.com/Hmbown/CodeWhale/pull/2565) **chore: add contribution gate workflows****  
   Introduces `APPROVED_CONTRIBUTORS` allowlist + CI gates to close unsolicited external PRs. *Impact*: Defines clear contribution policy; reduces maintainer noise.

3. **[#2558](https://github.com/Hmbown/CodeWhale/pull/2558) **Add configurable `path_suffix` for OpenAI-compatible endpoints****  
   Allows overriding API path (e.g., `/chat/completions` instead of `/v1/...`). *Impact*: Improves compatibility with non-standard OpenAI-proxy providers.

4. **[#2562](https://github.com/Hmbown/CodeWhale/pull/2562) **fix(npm): prefer binary version output****  
   Fixes wrapper reporting stale version when binary is updated locally. *Impact*: Resolves a common confusion point for npm-installed users.

5. **[#2559](https://github.com/Hmbown/CodeWhale/pull/2559) **fix(config): report legacy config migration****  
   Returns migrated paths from `~/.deepseek/config.toml` to `~/.codewhale/config.toml`. *Impact*: Gives users visibility into where configs live post-rebrand.

6. **[#2560](https://github.com/Hmbown/CodeWhale/pull/2560) **feat: add Xiaomi MiMo speech support****  
   New speech tool + configuration for Xiaomi MiMo. *Impact*: Expands ecosystem beyond text-only TUI; voice input for mobile/embedded scenarios.

7. **[#2557](https://github.com/Hmbown/CodeWhale/pull/2557) **feat(tui): add bang shell command shortcut****  
   Adds `! command` / `!command` support in composer, routing to `exec_shell`. Closes #1546. *Impact*: Brings parity with other agent CLIs; reduces friction for quick shell ops.

8. **[#2537](https://github.com/Hmbown/CodeWhale/pull/2537) **fix(subagent): guard truncated tool calls****  
   Raises sub-agent response budget from 4096 to 8192 tokens; halts execution on truncated tool calls. *Impact*: Prevents silent data corruption when sub-agents generate large outputs.

9. **[#2045](https://github.com/Hmbown/CodeWhale/pull/2045) **feat: add NSIS installer and classroom admin checklist****  
   Windows installer for non-technical users (teachers, students). *Impact*: Lowers the barrier for classroom/deployment scenarios; requested in community WeChat group.

10. **[#2314](https://github.com/Hmbown/CodeWhale/pull/2314) **perf(prompts): move environment block below volatile boundary****  
    Optimizes prompt caching by moving platform/shell/pwd info to volatile layer. *Impact*: Reduces cache invalidation churn for multi-session users; performance improvement.

## Feature Request Trends
- **Native memory / long-term context**: Multiple requests for cross-session persistence (`#2492`, `#743` context optimization) — users want the TUI to “remember” between restarts.
- **Better Windows and macOS support**: Issues targeting Ghostty flickering (`#1556`), Windows freeze (`#1812`), and macOS keybinding gaps (`#2494`) indicate platform maturity is a top request.
- **Enhanced model control and tool flexibility**: Requests for custom provider path overrides (`#2558`), deterministic file browsing (`#2368`), and universal Pre/PostToolUse hooks (`#1917`) show users want to tailor the TUI to their exact stack.
- **Simplified onboarding and migration**: The rebrand itself (`#1969`) plus NSIS installer (`#2045`) highlight a demand for zero-friction setup, especially in educational/enterprise contexts.

## Developer Pain Points
- **High / unaccounted token consumption** (`#743`) remains the #1 cost concern — users are surprised by 4x-10x expected usage.
- **Poor input cache hit rate** (`#1177`) compounds the cost problem; users see better numbers from competing tools (DeepSeek-Reasonix).
- **TUI freeze and stalling** (`#2487`, `#1812`) on both Windows and YOLO mode — these are blocking the core “hands-off agent” workflow.
- **Tool inconsistency** (`#2328`, `#2523`) between modes (Agent vs YOLO) and platforms (Linux vs Windows) frustrates users who rely on shell execution.
- **Deeply nested file access failure** (`#2488`) and **missing `tty` controlling terminal** (`#2372`) break real-world workflows for large projects and DevOps tasks.
- **Config migration confusion** (`#2369`) plus **silent Wayland clipboard failure** (`#1920`) erode trust in the tool’s cross-platform polish.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*