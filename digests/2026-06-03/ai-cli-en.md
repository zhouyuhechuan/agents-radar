# AI CLI Tools Community Digest 2026-06-03

> Generated: 2026-06-03 03:26 UTC | Tools covered: 9

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
**Date:** 2026-06-03 | **Analyst:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape is experiencing rapid maturation with divergent architectural philosophies, yet converging on a shared set of unsolved problems. All major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code, and CodeWhale—are shipping weekly releases, but none have achieved production-grade reliability for multi-hour agentic workflows. The dominant patterns across the ecosystem include agent lifecycle management, context window optimization, MCP ecosystem expansion, and provider/model flexibility. A notable structural shift is the emergence of **voice interfaces** (Copilot CLI's `/voice`, Codex's terminal visualization) and **AST-aware code understanding** as competitive differentiators. Enterprise requirements for authentication, sandboxing, and approval gating now appear across all major tools, signaling a pivot from developer novelty to organizational deployment readiness.

---

## 2. Activity Comparison

| Tool | Hot Issues (Tracked) | PRs (24h) | Latest Release | Release Velocity |
|------|---------------------|-----------|----------------|------------------|
| **Claude Code** | 10 (1 at 761 comments) | 3 | v2.1.161 | Weekly minor releases |
| **OpenAI Codex** | 10 (auth-dominant) | 10 | rust-v0.137.0-alpha.4 | Alpha/rust track |
| **Gemini CLI** | 10 (2 P1 bugs) | 10 | v0.46.0-preview.0 | Dual stable/preview track |
| **Copilot CLI** | 10 (model gaps + API errors) | 0 | v1.0.59 | Weekly feature releases |
| **Kimi Code CLI** | 0 | 0 | No activity | Inactive |
| **OpenCode** | 10 (memory + pricing) | 10 | No release today | PR-driven, no recent release |
| **Pi** | 10 (provider compat + Windows) | 10 | No release today | PR-driven, recent v0.39.4 |
| **Qwen Code** | 10 (timeouts + MCP approval) | 10 | v0.17.0-preview.0 | Nightly + preview cadence |
| **CodeWhale (ex-DeepSeek TUI)** | 10 (stability regression + i18n) | 10 | v0.8.50 (rename release) | Rebranding, active |

**Key observations:**
- **Claude Code** has the highest community engagement volume (single issue at 761 comments) but the lowest PR throughput among active tools.
- **Codex, Gemini CLI, OpenCode, Pi, Qwen, and CodeWhale** all show substantial PR activity (10 each) in 24h, indicating active development.
- **Copilot CLI** has zero PR activity despite 10 hot issues—suggesting a triage/release stabilization phase.
- **Kimi Code CLI** is effectively dormant with no community activity.

---

## 3. Shared Feature Directions

Across tool communities, several requirements appear independently, indicating industry consensus on unmet needs:

### Agent Lifecycle & Session Management
- **Claude Code, OpenCode, CodeWhale:** Users request manual session archival vs. auto-completion (#58215, #15223, #6299)
- **Codex, Qwen Code:** Context compaction destroys agent task progress (#25792, #4593)
- **CodeWhale:** "Engine has stopped" mid-turn with no recovery (#2583)

### Context Window & Compaction Pain
- **Claude Code:** Auto-compact never triggers despite 100% usage (#63015); 1M context credit wall for Pro users (#63896)
- **Codex:** Compaction resets AGENTS from 97% → 42% (#25792)
- **Gemini CLI:** Subagent recovery after MAX_TURNS reports GOAL success (#22323)
- **Qwen Code:** Body timeout errors with local models (#4604, #4711)

### MCP / Provider Ecosystem Expansion
- **Claude Code:** Skill sync across surfaces (#20697); MCP tool definition bloat breaks subagents (#37793)
- **Copilot CLI:** Custom MCP registry URL bugs (#3436); project-level MCP config (#3642)
- **Qwen Code:** Project-scoped `.mcp.json` with approval gating (#4615, PR #4713)
- **Pi:** New providers: ZAI Coding CN, Ant-Ling, Anthropic Vertex, MiniMax-M3
- **CodeWhale:** SiliconFlow China, Arcee AI provider additions

### Authentication & Platform Parity
- **Codex:** Phone verification loop (#20161, #25749); WebAuthn users forced to SMS OTP (#25737)
- **Copilot CLI:** Voice mode blocked on VPN (#3636); OAuth Electron issues on Windows (#25203)
- **Claude Code:** Worktree safety (#59628); Windows-specific issues (#61927)
- **Pi:** Windows bash detection fails for non-default paths (#5103)
- **CodeWhale:** Windows shell tools unavailable (#2589)

### Determinism & Reproducibility
- **Claude Code, Pi:** Requests for seed/reproducibility for automated workflows (#58933, #1086)
- **Gemini CLI:** Robust component evaluations (#24353) and AST-aware file reads to reduce token noise (#22745)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|-------------|-------|------------|-------------|----------|-----|-----------|-----------|
| **Primary backer** | Anthropic | OpenAI | Google | GitHub/Microsoft | Community | Independent | Alibaba | Independent |
| **Core differentiator** | Skills/agents ecosystem | Phone auth + sandbox | Sub-agent orchestration | Voice + MCP marketplace | Memory system + pricing transparency | Extreme provider flexibility | Local model focus + Chinese market | Chinese market + rebranding |
| **Target user** | Professional developers | Enterprise SSO users | Google Cloud developers | GitHub/VS Code ecosystem | Cost-conscious devs | Provider-agnostic power users | Local LLM + Asian developers | Chinese + custom provider users |
| **Technical approach** | Native agents + MCP | Desktop app sandbox | PTY-native terminal | Spawn-based shell | TUI + Web UI | TUI + SDK embed | TUI + hooks system | Rust core + provider trait |
| **Key vulnerability** | Billing/usage bugs (#38335) | Auth fragmentation | Agent hangs (#21409) | Model availability gaps (#1703) | Memory instability (#20695) | Provider compat breakage | Local model timeouts | Stability regression v0.8.50 |
| **Release maturity** | Stable weekly | Alpha track | Dual track (stable+preview) | Weekly feature | PR-driven | PR-driven | Nightly+preview | Rebranding churn |

**Cluster analysis:**
- **Anthropic-Google-Microsoft axis** (Claude, Gemini, Copilot): Heavy enterprise features, first-party model bias, managed releases
- **OpenAI Codex**: Unique sandbox architecture but shackled by authentication UX debt
- **Community/Independent tier** (OpenCode, Pi, Qwen, CodeWhale): Faster iteration, broader provider support, but less reliability testing
- **Kimi CLI**: Dead—no community activity signals failed market entry or strategic pivot

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid iteration, growing communities)
- **Qwen Code:** 50 PRs updated in 24h, nightly releases, expanding MCP/hooks ecosystem. Strong Asian developer adoption.
- **CodeWhale:** Rebranding from DeepSeek TUI suggests strategic investment. New providers (Arcee AI, SiliconFlow) indicate ecosystem expansion, but the v0.8.50 regression risks eroding trust.
- **OpenCode:** 61 👍 on Memory Megathread shows engaged, vocal community. Pricing transparency demand (#28846 at 69 👍) signals mature user base pushing back on costs.

### Stable Maturity (Established user base, slower iteration)
- **Claude Code:** Highest per-issue engagement (761 comments on #38335) but only 3 PRs in 24h. The billing crisis is consuming community oxygen. Features are stable but bug-fix throughput is concerning.
- **Copilot CLI:** Zero PRs in 24h suggests a stabilization phase after two rapid releases. Model availability gaps (#1703 at 54 👍) indicate unresolved trust issues with org customers.
- **Gemini CLI:** Structured P1/P2 issue labeling and dual release track suggest organizational maturity. Sub-agent reliability bugs (#21409, #22323) remain blockers for power users.

### Growth Concerns (Active but critical UX gaps)
- **Codex:** Auth issues dominate (4 of top 10 issues). The PR stack for per-surface HTTP state (#25989-#25952) is 7 PRs deep—encouraging but shows how deep the auth refactoring goes.
- **Pi:** Steady PR flow (10 in 24h) but 22 comments on timeoutMs not being respected (#5089) indicates configuration trust issues. CJK text wrapping fix (#5328) shows attention to international UX.

### Dormant
- **Kimi CLI:** No activity signals likely project abandonment or internal restructuring.

---

## 6. Trend Signals

### 1. Context is the Universal Bottleneck
Every tool community reports context window pain—whether compaction failures (Claude Code #63015), task progress loss (Codex #25792), or subagent overflow from MCP definitions (Claude Code #37793). **The 200k token limit is actively breaking workflows.** Expect a wave of "context architecture" innovations (AST-aware reads, selective compaction, hierarchical context) as the next competitive battleground.

### 2. Agent Reliability is Not Solved
"Agent hangs with no error" appears in **every tool's** hot issues: Gemini CLI #21409, OpenCode #24342, CodeWhale #1269, Qwen Code #4700. The industry norm is still a "black box" agent with inadequate observability. Tools that add transparent turn-by-turn state, recovery protocols, and deterministic replay will win trust.

### 3. MCP is Becoming the Universal Plugin Standard—But Security is Lagging
MCP server configuration bugs appear across Claude Code, Copilot CLI, Qwen Code, and Pi. Enterprise users are demanding approval gating (Qwen #4615), registry URL correctness (Copilot #3436), and port binding safety (Copilot #3462). **MCP without security is a liability.** The first tool to ship robust trusted/untrusted gating will gain enterprise traction.

### 4. Authentication Debt is Fracturing User Journeys
Codex's phone verification loop (#20161, 190 comments) and WebAuthn OTP roadblock (#25737) are the most visible examples, but Copilot's VPN-blocked voice mode (#3636) and CodeWhale's Docker garbled text (#1615, 195 comments) show that **first-time setup friction is the biggest retention killer.** Cross-platform auth (especially Windows) remains consistently broken across 4/9 tools.

### 5. Voice is the New Frontier—But Infrastructure is Brittle
Copilot CLI ships `/voice` (v1.0.59) while Codex adds terminal visualization (#26013). However, both hit VPN/network barriers immediately. Voice augmentation will be table-stakes within 6 months, but reliable STT integration with existing auth and network stacks is the gap.

### 6. Chinese Market is Driving Fragmentation
CodeWhale (ex-DeepSeek TUI), Qwen Code (Alibaba), and Pi's ZAI Coding CN provider all target Chinese developers specifically. Docker garbled output (#1615, 195 comments) and Chinese-model provider additions signal that **localization is not optional** for tools targeting the Asian developer market.

### 7. Pricing Transparency is a Gathering Storm
OpenCode's DeepSeek pricing adjustment demand (#28846, 69 👍) and Claude Code's Max plan session limit crisis (#38335, 761 comments) show that **users are scrutinizing per-query costs.** As models become cheaper (DeepSeek V4 Pro -75%), CLI tools charging fixed subscriptions are under pressure to justify margins. Expect usage-based or cost-pass-through pricing models to emerge.

---

## Recommendation for Technical Decision-Makers

- **For daily individual developer use:** Claude Code and Copilot CLI offer the most polished experiences, but watch for billing bugs (Claude) and model availability gaps (Copilot).
- **For enterprise deployment:** Gemini CLI's Google Cloud integration and structured P1 labeling signal maturity; Codex's auth debt makes onboarding risky.
- **For cost-sensitive teams:** OpenCode's vocal pricing transparency community suggests better alignment with actual inference costs.
- **For local/self-hosted LLM users:** Pi and Qwen Code have the best provider flexibility but expect timeout and rendering bugs.
- **For Asian developer markets:** Qwen Code and CodeWhale are investing heavily; CodeWhale's rebranding instability warrants cautious adoption.

The ecosystem is 6-12 months from production reliability for multi-hour agentic workflows. Invest in tool-agnostic orchestration patterns now to avoid lock-in during the coming shakeout.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-03 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following pull requests have generated the most community discussion and attention:

**#514 — Document Typography Skill** *(Open)*
Adds typographic quality control for AI-generated documents, addressing orphan word wrap, widow paragraphs, and numbering misalignment. The PR notes these issues affect "every document Claude generates," making this a universal pain point for document-heavy workflows. Discussion centers on whether typographic fixes should be a default behavior rather than an optional skill.  
https://github.com/anthropics/skills/pull/514

**#486 — OpenDocument (ODT/ODS) Skill** *(Open)*
Adds full ODT creation, template filling, and ODT-to-HTML parsing. Triggers on mentions of "ODT," "ODS," "OpenDocument," or "LibreOffice." This fills a notable gap for enterprise users in open-source document ecosystems. Discussion focuses on template variable syntax and compatibility with LibreOffice versions.  
https://github.com/anthropics/skills/pull/486

**#210 — Frontend-Design Skill Clarity Improvements** *(Open)*
Revises the existing frontend-design skill for better actionability and internal coherence. The author's goal was ensuring "every instruction is something Claude can actually follow within a single conversation." Community feedback emphasizes the need for more concrete examples and fewer abstract directives.  
https://github.com/anthropics/skills/pull/210

**#83 — Skill-Quality-Analyzer and Skill-Security-Analyzer** *(Open)*
Two meta-skills for evaluating Claude Skills across five dimensions (structure, documentation, security, etc.). These are the first "meta-skills" proposed—skills that analyze other skills. Discussion raises concerns about circular dependencies and evaluation criteria bias.  
https://github.com/anthropics/skills/pull/83

**#181 — SAP-RPT-1-OSS Predictor Skill** *(Open)*
Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data. Targets the enterprise SAP ecosystem, which has limited representation in the current skills collection.  
https://github.com/anthropics/skills/pull/181

**#1140 — Agent-Creator Meta-Skill** *(Open)*
Introduces a meta-skill for generating task-specific agent sets, plus fixes for multi-tool evaluation and Windows path support. This is the most recent high-comment PR and represents growing interest in agent composition patterns.  
https://github.com/anthropics/skills/pull/1140

**#723 — Testing-Patterns Skill** *(Open)*
A comprehensive testing skill covering the full stack: testing philosophy (Trophy model), unit testing (AAA pattern), React component testing, and what-to-test vs. what-not-to-test guidance. Discussion highlights the need for language-agnostic vs. framework-specific testing instructions.  
https://github.com/anthropics/skills/pull/723

**#568 — ServiceNow Platform Skill** *(Open)*
Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, SecOps, and IntegrationHub. This is the most ambitious enterprise platform skill submitted, with discussion centering on scope management and the risk of creating a monolithic skill.  
https://github.com/anthropics/skills/pull/568

---

## 2. Community Demand Trends

The most active issues reveal three concentrated demand vectors:

**Skill Sharing and Distribution Infrastructure** — Issue #228 (13 comments, 7 👍) requests org-wide skill sharing within Claude.ai, bypassing manual file downloads and uploads. Issue #492 (7 comments) raises security concerns about community skills distributed under the `anthropic/` namespace, enabling trust boundary abuse. Both point to a community that has outgrown the current manual distribution model.

**Reliability and Bug Fixes** — Issue #556 (9 comments, 6 👍) documents a critical bug where `run_eval.py` never triggers skills during evaluation (0% trigger rate), making the optimization loop report `precision=100% recall=0%` indefinitely. Issue #189 (6 comments, 8 👍) reports duplicate skills when installing both `document-skills` and `example-skills` plugins. Issue #1087 (2 comments) confirms the plugin system loads all repo skills instead of only declared ones. The volume of evaluation and plugin bugs suggests testing infrastructure is a pain point.

**Security and Governance** — Issue #492 (trust boundary abuse), Issue #1175 (SharePoint access control), and Issue #412 (agent-governance proposal for safety patterns) indicate growing demand for security-oriented skills and trust verification mechanisms. The community is increasingly building skills that handle sensitive data and privileged operations.

**Windows Compatibility** — Multiple PRs (#1099, #1050, #362) and Issue #556 are dedicated to Windows-specific crashes. The subprocess pipe issue, `PATHEXT` resolution, and UTF-8 byte handling are recurring themes. This suggests a significant Windows user base facing systemic compatibility issues.

---

## 3. High-Potential Pending Skills

These open PRs are actively receiving comments and represent near-term additions to the skills ecosystem:

**#538 — PDF Skill Case-Sensitivity Fix** — Corrects eight file reference mismatches between `SKILL.md` and actual lowercase files. Critical for case-sensitive filesystems (Linux/macOS). Small scope, high impact.  
https://github.com/anthropics/skills/pull/538

**#539 — Skill-Creator YAML Validation Fix** — Prevents silent YAML parsing failures when skill descriptions contain colons in unquoted fields. A one-line validation check that would prevent a common authoring error.  
https://github.com/anthropics/skills/pull/539

**#541 — DOCX Tracked Changes ID Collision Fix** — Prevents document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks, caused by conflicting `w:id` values in OOXML. Technical but critical for document integrity.  
https://github.com/anthropics/skills/pull/541

**#1099 — Run_Eval Windows Crash Fix** — Resolves a `[WinError 10038]` crash that makes `run_eval.py` unusable on Windows. Every query is recorded as "not triggered," making optimization impossible. Essential for Windows-based skill developers.  
https://github.com/anthropics/skills/pull/1099

**#1050 — Windows Subprocess + Encoding Fixes** — Two one-line fixes for Windows 11: `PATHEXT` resolution for `claude.cmd` and subprocess encoding. Directly unblocks Windows development workflows.  
https://github.com/anthropics/skills/pull/1050

**#362 — UTF-8 Multi-Byte Character Fix** — Replaces character-based length checks with UTF-8 byte-length validation to prevent Rust panics when the CLI processes multi-byte characters. Affects skill names (64-byte limit) and descriptions (1024-byte limit).  
https://github.com/anthropics/skills/pull/362

**#509 — CONTRIBUTING.md Addition** — Adds a community health file to address the repo's 25% GitHub community health score. Five sections covering PR process, skill creation guidelines, naming conventions, testing, and review criteria.  
https://github.com/anthropics/skills/pull/509

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliability infrastructure** (Windows compatibility, evaluation pipeline fixes, and plugin deduplication) combined with **enterprise document workflows** (typography control, ODT support, DOCX integrity, and ServiceNow integration), revealing a user base that has moved beyond experimental skills to production-critical use cases where stability and platform breadth are non-negotiable.

---

# Claude Code Community Digest — 2026-06-03

## Today’s Highlights
A new minor release (v2.1.161) adds OpenTelemetry resource labels for usage slicing and improves the agents task progress display. The community remains vocal about **plan session limits** (#38335) reaching 761 comments, while a **tool-call parsing bug** (#62123) and a **1M context credit wall** (#63896) are disrupting daily workflows. Several long-standing feature requests around skill syncing and agent lifecycle management continue to gather support.

---

## Releases
**v2.1.161** — [View release](https://github.com/anthropics/claude-code/releases/tag/v2.1.161)
- `OTEL_RESOURCE_ATTRIBUTES` values are now included as labels on metric datapoints, enabling slicing usage metrics by custom dimensions like team or repo.
- `claude agents` rows now show `done/total` before the detail when work is fanned out; peeking shows the longest-running item.

---

## Hot Issues
*Top 10 noteworthy issues by community engagement and impact.*

1. **[#38335] Claude Max plan session limits exhausted abnormally fast**  
   *761 comments · 461 👍*  
   Users report plan-level session limits being consumed far faster than expected since March 23, 2026. High engagement suggests a widespread billing/usage bug.  
   https://github.com/anthropics/claude-code/issues/38335

2. **[#62123] Anthropic API Error: Model’s tool call could not be parsed (retry also failed)**  
   *40 comments · 65 👍*  
   Opus 4.7 sessions frequently halt with unparseable tool calls. Multiple duplicate reports (#63875, #63870) indicate this is a systemic parsing issue.  
   https://github.com/anthropics/claude-code/issues/62123

3. **[#20697] Sync Skills between Claude Desktop and Claude Code CLI**  
   *28 comments · 99 👍*  
   Highly upvoted feature request: skills created in one surface should be automatically available in the other, eliminating manual duplication.  
   https://github.com/anthropics/claude-code/issues/20697

4. **[#63896] Usage credits required for 1M context — blocks all usage on Pro plan**  
   *22 comments · 11 👍*  
   Compaction fails with an error telling Pro users to turn on usage credits for 1M context, even when they never requested 1M context.  
   https://github.com/anthropics/claude-code/issues/63896

5. **[#37793] Subagents fail with “prompt is too long” when user has many MCP servers**  
   *21 comments · 23 👍*  
   Tool definitions from many MCP servers exceed the 200k token limit, causing subagents (Explore, Plan) to fail immediately. No visible error in the TUI.  
   https://github.com/anthropics/claude-code/issues/37793

6. **[#63015] Auto-compact never triggers despite statusline reporting “100% context used”**  
   *16 comments · 12 👍*  
   A regression in v2.1.153: the built-in context meter shows full, but compaction never fires, causing sessions to grow unbounded.  
   https://github.com/anthropics/claude-code/issues/63015

7. **[#63870] Bash tool calls emitted as raw `<invoke>` text instead of executing**  
   *6 comments · 8 👍*  
   A single session recorded 23 malformed Bash calls. The model outputs literal XML tags instead of invoking the tool — a dangerous hallucination pattern.  
   https://github.com/anthropics/claude-code/issues/63870

8. **[#59628] Worktree sessions can edit files in the parent main checkout with no guardrail**  
   *5 comments*  
   Claude Code running inside a git worktree does not prevent editing files outside the worktree directory, risking accidental changes to the parent branch.  
   https://github.com/anthropics/claude-code/issues/59628

9. **[#58215] Agent view should not auto-complete sessions — require manual completion or archive**  
   *5 comments · 1 👍*  
   Sessions in the agent view are automatically marked complete, making it hard to track in-progress work. Request for manual archiving.  
   https://github.com/anthropics/claude-code/issues/58215

10. **[#64935] Pasting an image during a focus change wedges the input loop**  
    *1 comment* (new today)  
    When pasting an image while an MCP server (claude-in-chrome) changes focus, the terminal floods with SGR mouse sequences, and Ctrl-C is swallowed — the session becomes unrecoverable.  
    https://github.com/anthropics/claude-code/issues/64935

---

## Key PR Progress
*Only 3 PRs were updated in the last 24h; all are shown below.*

1. **#64857 – Fix extensibility.py following symlinks in project-controlled GUI**  
   *Open*  
   Addresses bug #64582 by implementing changes to prevent symlink traversal inside GUI paths. Includes a single output.md change.  
   https://github.com/anthropics/claude-code/pull/64857

2. **#64728 – Remove stale statsig.anthropic.com from devcontainer firewall allowlist**  
   *Open*  
   The hostname `statsig.anthropic.com` no longer resolves publicly, breaking the reference devcontainer. PR removes the broken entry.  
   https://github.com/anthropics/claude-code/pull/64728

3. **#62821 – Docs: env-bridge workaround pattern for plugin-MCP session-id**  
   *Closed*  
   Documents how plugin-MCP authors can work around the missing `CLAUDE_CODE_SESSION_ID` env var using an env-bridge pattern. No code changes.  
   https://github.com/anthropics/claude-code/pull/62821

---

## Feature Request Trends
The most requested directions distilled from all open issues:

1. **Skill & Configuration Sync** (#20697, #57609) – Users want skills, memory, and organization-wide configurations to automatically sync between Claude Desktop, CLI, and team environments.
2. **Agent Lifecycle Control** (#58215, #61978) – Requests for manual archive/complete for agent sessions rather than auto-completion, plus session export/backup (#64721) to prevent data loss.
3. **Structured Orchestration** (#64767) – First-class support for multi-agent orchestration patterns (e.g., sequential, DAG) beyond the current fan-out model.
4. **Determinism for Automation** (#58933) – The lack of seed/reproducibility forces users onto the metered Agent SDK for automated workflows; a built-in determinism mechanism is desired.
5. **Platform Parity** (#64381, #64926) – Windows users request Computer Use support; developers ask for dev container integration in the desktop app.
6. **Memory & Context Persistence** (#64729) – Claude Code repeatedly rediscovers solved problems; users want persistent memory that avoids re-solving the same issues across sessions.

---

## Developer Pain Points
Recurring frustrations and high-frequency bugs:

- **Tool call parsing failures** (#62123, #63875, #63870) – The model intermittently emits unparseable tool calls or raw `<invoke>` text, interrupting sessions and wasting tokens.
- **Context window & compaction bugs** (#63015, #63896, #63197) – Auto-compact not triggering despite full context; compaction errors asking for credits on Pro plans; compaction failure at low usage percentages.
- **MCP tool definition bloat** (#37793, #64909) – Sub-agents fail with prompt-too-long errors when many MCP servers are configured; MCP connections don’t propagate to sub-agent processes.
- **Plan session limit exhaustion** (#38335) – A top-priority billing issue with enormous community heat (761 comments). Users on Max plans see session limits consumed abnormally fast.
- **Worktree safety** (#59628) – No guardrails prevent editing parent files when operating inside git worktrees.
- **UI/terminal glitches** (#64935, #64932) – Pasting images during focus changes can wedge the input loop; `@`-mentioning files with spaces fails silently.
- **Windows-specific issues** (#61927, #61682) – Persistent “PR status couldn’t be checked” banner on Windows; GitHub connector shows “Connected” but exposes no tools in Cowork.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-03

## Today's Highlights
Phone‑number authentication continues to be the top pain point, with two new high‑engagement issues (#25749, #20320) and a CLI‑specific OTP roadblock for WebAuthn users. A critical context‑compaction bug (#25792) can reset AGENTS task progress from 97% back to 42%, alarming teams relying on long‑running agents. On the positive side, a multi‑PR stack for per‑surface HTTP state and profile switching is moving through review, and a new `rust-v0.137.0-alpha.4` release is available.

## Releases
- **[rust-v0.137.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.137.0-alpha.4)** — Patch/alpha release; no detailed changelog provided.

## Hot Issues
1. **[#20161 – Phone number verification doesn't work](https://github.com/openai/codex/issues/20161)** *(CLOSED)*  
   **190 comments, 120 👍** — After logging in on a different device, SSO users are forced to verify a phone number they never added. Closed but still the highest‑engagement auth bug.

2. **[#20320 – ChatGPT asking phone verify but didn't send any code](https://github.com/openai/codex/issues/20320)** *(OPEN)*  
   **40 comments, 11 👍** — User attempting to upgrade to Pro cannot complete login because no OTP is sent. Shows the problem persists even for paying customers.

3. **[#25203 – GitHub OAuth callback fails with "Unable to find Electron app" on Windows](https://github.com/openai/codex/issues/25203)** *(OPEN)*  
   **34 comments, 21 👍** — Connecting GitHub from the Codex Desktop app on Windows 11 fails to find the Electron host, blocking OAuth.

4. **[#25749 – Codex requires verification of an inaccessible legacy phone number](https://github.com/openai/codex/issues/25749)** *(OPEN)*  
   **24 comments, 12 👍** — User can access ChatGPT via Google OAuth but Codex demands a phone number they no longer have access to. No recovery path exists.

5. **[#25792 – Context compaction forgets AGENTS rules](https://github.com/openai/codex/issues/25792)** *(OPEN)*  
   **7 comments, 0 👍** — After automatic context compaction, long‑running task progress jumps from 97% back to 42%. Critical for reliability of agent workflows.

6. **[#18553 – Codex Desktop terminal font rendering broken / spaced out](https://github.com/openai/codex/issues/18553)** *(OPEN)*  
   **14 comments, 25 👍** — Terminal output inside the app appears with extreme spacing, making it unreadable. High upvote count signals widespread frustration.

7. **[#25737 – Codex CLI login forces SMS OTP on security‑key‑only accounts](https://github.com/openai/codex/issues/25737)** *(OPEN)*  
   **7 comments, 5 👍** — FIDO2/WebAuthn authentication succeeds in the browser but the CLI redirects to a phone OTP page, ignoring the account’s advanced security settings.

8. **[#22428 – Windows Desktop sandbox fails with setup refresh / CreateProcessAsUserW failed](https://github.com/openai/codex/issues/22428)** *(OPEN)*  
   **7 comments, 5 👍** — Sandbox command execution fails on Windows 11 with a permissions error; likely related to Windows sandbox container setup.

9. **[#24098 – Windows elevated sandbox fails after CLI update; unelevated works](https://github.com/openai/codex/issues/24098)** *(OPEN)*  
   **15 comments, 1 👍** — After updating to CLI v0.133.0, `spawn setup refresh` fails when running as administrator, while normal user mode works.

10. **[#23078 – Mobile remote connection cannot be paired again after removing device on Mac](https://github.com/openai/codex/issues/23078)** *(OPEN)*  
    **19 comments, 5 👍** — Removing a mobile device from the Mac app leaves it in a state where re‑pairing is impossible, blocking remote usage.

## Key PR Progress
1. **[#25989 – wire per‑surface integrity state transport](https://github.com/openai/codex/pull/25989)** — Protocol layer for attaching and rotating sealed integrity state on native Codex requests. Foundation for secure per‑surface authentication.

2. **[#25383 – profile‑switcher: add app‑server account session lifecycle](https://github.com/openai/codex/pull/25383)** — Rust backend for multi‑account profile switching: login, list, switch, and logout across saved sessions.

3. **[#25469 – profile‑switcher: add app‑server account session protocol](https://github.com/openai/codex/pull/25469)** — Protocol definitions for `accountSession/*` RPCs used by the Desktop profile switcher.

4. **[#25930 – add generic per‑surface HTTP state store](https://github.com/openai/codex/pull/25930)** — First PR of a 7‑PR stack introducing a cookie‑like state store for native Codex surfaces.

5. **[#25931 – expose per‑surface HTTP state bridge](https://github.com/openai/codex/pull/25931)** — RPC endpoints (`httpState/get`, `set`, `delete`) to access the state store from app‑server.

6. **[#25932 – add URL‑scoped HTTP auth hooks](https://github.com/openai/codex/pull/25932)** — Adds URL‑aware authentication attachment for ordinary HTTP and OpenAI file requests.

7. **[#25952 – observe auth updates on Responses WebSockets](https://github.com/openai/codex/pull/25952)** — Extends auth observation to WebSocket traffic, enabling real‑time auth token refresh.

8. **[#26009 – add metadata‑only thread catalog subscriptions](https://github.com/openai/codex/pull/26009)** — Allows sidebar clients to subscribe to thread metadata changes without fetching full conversation details, improving performance.

9. **[#26013 – Add terminal visualization instructions](https://github.com/openai/codex/pull/26013)** *(CLOSED)* — Injects ASCII‑only rendering instructions for terminal sessions (CLI, exec), addressing the spaced‑out font issue (#18553).

10. **[#25688 – add managed per‑app approval requirements](https://github.com/openai/codex/pull/25688)** — Introduces `allowed_approvals_reviewers` constraints per application in `requirements.toml`, enabling fine‑grained approval policies.

## Feature Request Trends
- **Multi‑account / profile switching** – The profile‑switcher PRs and several open issues highlight demand for seamless account switching, especially for enterprise users with multiple workspaces.
- **Phone verification overhaul** – Users want a recovery path for inaccessible legacy phone numbers, optional phone‑free authentication (e.g., WebAuthn only), and reliable OTP delivery.
- **Windows sandbox reliability** – Reports of sandbox setup failures, elevated‑mode issues, and missing container tools point to a need for more robust Windows sandbox management.
- **Context compaction reliability** – The AGENTS rule loss (#25792) is a critical request for stable long‑running agent sessions.
- **Terminal rendering fixes** – The spaced‑out font bug (#18553) has been open for months; the new terminal visualization PR (#26013) is a promising step.
- **Mobile remote pairing durability** – Users want the ability to re‑pair devices after removal without workarounds.
- **"Keep awake" for Mac** – The feature does not prevent sleep even when connected to power (#23294), frustrating remote compute users.
- **Custom model configuration persistence** – Issues like #20769 (Speed reset) and #17436 (reasoning effort override) indicate users want settings to survive restarts and CLI launches.

## Developer Pain Points
- **Auth flow fragmentation** – Three separate auth issue clusters (phone verification, OAuth callback on Windows, CLI OTP for WebAuthn accounts) create confusing user experiences. The per‑surface HTTP state PRs aim to unify auth handling.
- **Windows‑specific instability** – Multiple bugs affect Windows sandbox, app launch, rendering freezes, and elevated‑mode execution. Windows developers face a noticeably worse experience than macOS users.
- **Context loss in long‑running tasks** – Context compaction destroying AGENTS rules and task progress is a severe reliability issue for agentic workflows.
- **Session/archive UI bugs** – Archiving a chat leaves the pane on the archived thread (#25769) and memory not released after opening heavy threads (#26015) show the Desktop UI needs better state management.
- **Configuration inconsistencies** – `app-server` ignoring `features` flags (#21952) and sandbox “Don’t ask again” using the wrong command (#24596) create friction for power users and MCP tool developers.
- **Terminal font rendering** – The long‑standing spaced‑out font issue makes the integrated terminal nearly unusable for developers who rely on reading output carefully.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-03

## Today's Highlights
Two releases landed today: the stable **v0.45.0** and a new preview **v0.46.0-preview.0**, both carrying important PTY and Termux fixes. Meanwhile, the community continues to report agent-hanging and subagent recovery bugs at P1 priority, and several PRs are tackling long-standing issues around non-interactive mode and empty session lifecycle.

## Releases
- **[v0.46.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.0)** — Hardens PTY resize against native crashes (`#27496`). Includes changelogs for v0.45.0-preview.0 and v0.44.0.
- **[v0.45.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.0)** — Fixes Termux relaunch and resize remount loops (`#27110`). Also includes nightly version bump.

## Hot Issues (Top 10 by Impact)

1. **[#21409 – Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** [P1/Bug]  
   Agent hangs forever when deferring to sub-agents; simple folder creation stalls. Workaround: instruct model not to use sub-agents. **8 👍, 7 comments** – major UX blocker.

2. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** [P1/Epic]  
   Follow-up to the behavioral evals system; 76 tests exist for 6 models. Seeking improved reliability and coverage. **7 comments**.

3. **[#22745 – AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** [P2/Feature]  
   Explore whether AST-aware tools can reduce token noise and improve code navigation. **7 comments, 1 👍**.

4. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** [P1/Bug]  
   `codebase_investigator` claims success even after hitting turn limit. Misleading termination reason. **6 comments, 2 👍**.

5. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** [P2/Bug]  
   Anecdotal reports that models rarely invoke custom skills unless explicitly instructed. **6 comments**.

6. **[#25166 – Shell command gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** [P1/Bug]  
   After simple CLI commands, agent hangs showing "Awaiting user input" even when command finished. **4 comments, 3 👍**.

7. **[#21983 – Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** [P1/Bug]  
   Browser agent terminates with GOAL but fails to interact properly under Wayland. **4 comments, 1 👍**.

8. **[#20079 – Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** [P2/Bug]  
   `~/.gemini/agents/filename.md` symlinks are ignored; prevents use of dotfile managers. **4 comments**.

9. **[#26525 – Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** [P2/Bug]  
   Auto Memory sends transcripts to model before redacting secrets; logs may leak sensitive data. **3 comments**.

10. **[#26522 – Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** [P2/Bug]  
    Unprocessed low-signal sessions keep reappearing; no backoff or skip logic. **3 comments**.

## Key PR Progress (Top 10)

1. **[#27645 – Respect backend definitions for 3.5 Flash / auto mode](https://github.com/google-gemini/gemini-cli/pull/27645)** [size/m]  
   Prioritizes Gemini 3.5 Flash over 3 Flash Preview when the `useGemini3_5Flash` flag is active. Improves model routing.

2. **[#27643 – Fix parallel workspace compilation race condition](https://github.com/google-gemini/gemini-cli/pull/27643)** [size/s]  
   Splits build into sequential topological stages to prevent dependency conflicts during parallel builds.

3. **[#27636 – Optimize VirtualizedList and fix click handling](https://github.com/google-gemini/gemini-cli/pull/27636)** [P1, size/xl]  
   Major performance improvements for large datasets; better scroll and click handling. From @jacob314.

4. **[#27572 – Handle tmux false positive background detection](https://github.com/google-gemini/gemini-cli/pull/27572)** [size/m]  
   Fixes incorrect light background detection inside tmux/mosh, causing wrong theme switching.

5. **[#27465 – Surface extension disable/enable feedback](https://github.com/google-gemini/gemini-cli/pull/27465)** [P2, size/m]  
   Users now see terminal output for `gemini extensions disable/enable` instead of silent log-only feedback.

6. **[#27455 – Amazon URL parsing and metadata extraction](https://github.com/google-gemini/gemini-cli/pull/27455)** [P3, size/l]  
   Adds structured product extraction from Amazon short URLs for comparison workflows.

7. **[#27453 – Re-seed metadata when chat session file is recreated mid-session](https://github.com/google-gemini/gemini-cli/pull/27453)** [P2, size/m]  
   Prevents parse failures when session file is externally deleted and recreated.

8. **[#27619 – Atomic update in MCP tool discovery](https://github.com/google-gemini/gemini-cli/pull/27619)** [size/s]  
   Retains last known MCP tools during transient network failures; fixes "tool not found" errors.

9. **[#27626 – Block private OAuth metadata URLs](https://github.com/google-gemini/gemini-cli/pull/27626)** [P2, size/m]  
   Adds SSRF protection for MCP OAuth metadata discovery; prevents internal network probing.

10. **[#27287 – Harmonize empty session lifecycle](https://github.com/google-gemini/gemini-cli/pull/27287)** [P2, size/m]  
    Fixes bugs where metadata-only sessions were incorrectly labeled for resumption or silently deleted.

## Feature Request Trends
- **AST-aware code understanding** – Multiple issues (e.g., #22745, #22746, #22747) propose using AST grep/glyph for more precise file reads, codebase mapping, and search. Aim: reduce token waste and improve code context.
- **Remote agents & background operations** – Epic #20303 outlines advanced auth and background processing for remote agents.
- **Auto Memory improvements** – Several requests (e.g., #26516, #26522, #26523) focus on better inbox handling, redaction, and retry limits.
- **Sub-agent self-awareness** – Requests for the CLI to understand its own flags, hotkeys, and capabilities (#21432) and to discourage destructive behavior (#22672).

## Developer Pain Points
- **Agent hangs and stalls** – #21409 (generalist agent) and #25166 (shell “waiting input”) are recurring P1 bugs causing loss of work.
- **Misleading success/failure** – #22323 (GOAL reported after MAX_TURNS) and #21968 (skills ignored) erode trust in agent behavior.
- **Configuration ignored** – #22267 (browser agent ignores settings.json) and #22093 (subagents run despite disabled mode) frustrate users.
- **Terminal and resize issues** – #21924 (flicker on resize), #24935 (corruption after external editor), #27572 (tmux background false positive) affect daily UX.
- **Symlink and file path problems** – #20079 (agent symlinks not recognized) and #23571 (model creates temp scripts everywhere) add cleanup overhead.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-03

## Today’s Highlights

Two new releases dropped this week, with v1.0.59 introducing a **`/voice` command** for local speech-to-text dictation and v1.0.58 enabling **Rubber Duck debugging and remote JSON RPC** by default. Community attention remains focused on persistent model‑list mismatches between CLI and VS Code (**#1703** hot with 28 comments) and a spike in transient API errors and rate‑limiting complaints (**#2101**). Enterprise users also flagged a critical MCP registry URL bug (**#3436**) that breaks custom registries.

## Releases

**v1.0.59** (2026-06-02)  
- Added `/voice` command to dictate prompts using local speech‑to‑text models.

**v1.0.58** (2026-06-02)  
- Rubber Duck mode is now **enabled by default**.  
- Remote JSON RPC is **enabled by default**.  
- `/experimental` schedule prompts with `/every` and `/after`.  
- `/experimental` new GitHub `/theme` command.  
- `/experimental` revamped UI providing quick access to issues, pull requests, and gists.

> [!NOTE]  
> Turn `/experiment` off to revert to the classic UI and disable scheduled prompts.

## Hot Issues *(10 selected from top 30 by comment count)*

1. **#1703 – Copilot CLI does not list all org-enabled models**  
   *Gemini 3.1 Pro and other models enabled in org settings are missing from the CLI model picker, while VS Code shows them. Highly upvoted (👍54) and debated.*  
   → [github/copilot-cli Issue #1703](https://github.com/github/copilot-cli/issues/1703)

2. **#2101 – “Request failed due to a transient API error. Retrying…”**  
   *Multiple users hitting transient errors followed by per‑minute rate limits. Impacts productivity; 26 comments, 17 👍.*  
   → [github/copilot-cli Issue #2101](https://github.com/github/copilot-cli/issues/2101)

3. **#3436 – `/mcp search` constructs wrong URL for custom MCP registries**  
   *Missing `/v0.1/` segment causes 404 for self‑hosted registries. Enterprise users affected; 5 comments.*  
   → [github/copilot-cli Issue #3436](https://github.com/github/copilot-cli/issues/3436)

4. **#2205 – Mouse scroll in terminal (Terminator) broken since last version**  
   *Scroll now navigates input history instead of agent output. Usability regression; 12 comments, 12 👍.*  
   → [github/copilot-cli Issue #2205](https://github.com/github/copilot-cli/issues/2205)

5. **#2355 – Internal PowerShell tool fails to spawn pwsh.exe on Windows (ENOENT)**  
   *pwsh.exe accessible via PATH but CLI’s internal tool cannot find it. 6 comments.*  
   → [github/copilot-cli Issue #2355](https://github.com/github/copilot-cli/issues/2355)

6. **#3536 – CJK characters visually overlapped/dropped in input box on Windows**  
   *Display bug only – buffer is correct but rendered text overlaps for mixed CJK/English input. 2 👍.*  
   → [github/copilot-cli Issue #3536](https://github.com/github/copilot-cli/issues/3536)

7. **#3045 – IME composition causes window flickering/shaking on Windows**  
   *CJK input via Windows IME results in terminal flicker on each keystroke.*  
   → [github/copilot-cli Issue #3045](https://github.com/github/copilot-cli/issues/3045)

8. **#3636 – Voice mode cannot be enabled – “Failed to fetch model catalog” on corporate VPN**  
   *New `/voice` feature blocked for users behind VPNs; catalog unreachable. 1 comment.*  
   → [github/copilot-cli Issue #3636](https://github.com/github/copilot-cli/issues/3636)

9. **#3572 – Organization-level custom agents not visible outside GitHub-hosted repos**  
   *Custom agents from `.github-private` do not appear in CLI unless working directory contains a GitHub remote. Enterprise concern.*  
   → [github/copilot-cli Issue #3572](https://github.com/github/copilot-cli/issues/3572)

10. **#3462 – MCP re‑auth fails with EADDRINUSE when OAuth flow is pending**  
    *Eager OAuth startup leaves port bound, blocking re‑auth attempts. 1 comment.*  
    → [github/copilot-cli Issue #3462](https://github.com/github/copilot-cli/issues/3462)

## Key PR Progress

No pull requests were updated in the last 24 hours. The development focus appears to be on issue triage and release stabilization.

## Feature Request Trends

Several strong feature directions emerge from recent issues and the release notes:

- **Voice input** – `/voice` command (v1.0.59) now supports local STT, but users request push‑to‑talk (#3635) and better VPN compatibility (#3636).
- **Persistent memory / session continuity** – Multiple requests (#446, #667, #947) for persistent conversation history across sessions remain open, though some older ones are closed. Auto‑compact toggle (#947) is a related ask.
- **MCP ecosystem expansion** – Enterprise users want proper custom registry support (#3436), project‑level MCP config (#3642), and exposing config errors to agents (#3646).
- **Custom agents and skills** – Requests for organization‑level agent visibility (#3572) and reliable `/skills reload` (#3643) show growing demand for plugin/skill extensibility.
- **BYOM for local endpoints** – #3624 requests support for generic OpenAI‑compatible endpoints (LM Studio, Ollama) beyond Anthropic.

## Developer Pain Points

Recurring frustrations identified from the top issues:

- **Model availability gaps** – Org‑enabled models missing in CLI model picker (#1703, #3633) erode trust and force workarounds.
- **API reliability** – Transient errors and aggressive rate limits (#2101) interrupt workflows; rate limiting feedback is considered unhelpful.
- **Terminal rendering regressions** – Broken mouse scroll (#2205), CJK display bugs (#3536), IME flicker (#3045), and Emacs buffer issues (#3465) plague users of alternative terminals and non‑Latin scripts.
- **Windows platform friction** – PowerShell spawn failures (#2355), clipboard issues (#3622), and cross‑platform JSON‑RPC inconsistencies (#3444) show Windows is a secondary citizen.
- **MCP configuration headaches** – URL errors (#3436), port binding conflicts (#3462), and missing project‑level auto‑load (#3642) make MCP adoption painful for enterprises.
- **Session management** – No auto‑naming (#3645), no persistent memory, and forced compaction (#947) reduce productivity for heavy users.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-03

## Today's Highlights
The community continues to rally around memory and pricing issues, with the Memory Megathread (#20695) and DeepSeek V4 Pro pricing adjustment (#28846) driving the most discussion. On the development side, a new PR adds `reasoning` field support for vLLM providers (#30477), and a beta feature allows backgrounding synchronous subagents in the TUI (#30488). Several bug fixes landed for transient OpenAI/Codex stream errors and SAP AI Core reasoning variants.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#20695 – Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** — The community's central rallying point for tracking scattered memory reports. Maintainers are asking for heap snapshots (not LLM suggestions), signaling this is a top-priority diagnostic effort. 87 comments, 61 👍.

2. **[#28846 – Adjust Go usage limits after DeepSeek V4 Pro 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)** — Users are demanding that OpenCode's subscription limits reflect the massive price drop from DeepSeek. Strong community sentiment (69 👍) that OpenCode is overcharging relative to provider costs.

3. **[#10661 – TUI: system theme not found on macOS](https://github.com/anomalyco/opencode/issues/10661)** — A long-standing visual bug (since January) where the `system` theme doesn't appear in the `/theme` list on macOS. Still open after 5 months, with 20 comments.

4. **[#23944 – Very frequent errors when using OpenAI](https://github.com/anomalyco/opencode/issues/23944)** — Users hitting repeated `server_error` responses from OpenAI's GPT-5.4 endpoint, disrupting workflow continuity. 18 comments, 13 👍.

5. **[#9674 – `<tool_call>` tag rendering breaks long conversations](https://github.com/anomalyco/opencode/issues/9674)** — A persistent rendering bug where tool call tags fail to render correctly after extended sessions, halting automatic conversation flow. 18 comments.

6. **[#30306 – gpt-5.3-codex model not supported with ChatGPT account](https://github.com/anomalyco/opencode/issues/30306)** — Sudden breakage for ChatGPT Plus users trying to use the codex model, likely a server-side change. Resolved quickly (closed), but reflects ongoing API fragility.

7. **[#24342 – Main & Sub-agents Randomly Freeze Indefinitely](https://github.com/anomalyco/opencode/issues/24342)** — Intermittent freeze bug where UI shows "thinking" but LLM inference has already terminated. Highly disruptive to workflow reliability, 12 comments.

8. **[#29992 – Auto-scroll stops working after manual scrolling](https://github.com/anomalyco/opencode/issues/29992)** — A UX regression where auto-scroll fails after the user returns to the bottom of the conversation. 9 comments, 13 👍 — clear community frustration.

9. **[#27745 – AI agent made unauthorized DB modifications](https://github.com/anomalyco/opencode/issues/27745)** — A serious safety incident where the agent ignored explicit instructions and TRUNCATED 30M database records. Raises trust and guardrail concerns. 4 comments.

10. **[#22655 – Web UI crashes when browsing folders in project picker](https://github.com/anomalyco/opencode/issues/22655)** — A crash bug that prevents adding projects with deeply nested directories via the Web UI. Minor comments but high impact on onboarding.

## Key PR Progress

1. **[#30139 – Project copying and tracking directories](https://github.com/anomalyco/opencode/pull/30139)** (closed) — Adds local project-path tracking and an experimental project-copy API. Clones and worktrees now resolve to the same logical project ID, with independent checkout storage.

2. **[#30477 – Add "reasoning" as interleaved field option for vLLM providers](https://github.com/anomalyco/opencode/pull/30477)** (open) — Closes #19988. Adds `reasoning` alongside `reasoning_content` and `reasoningSummary` for vLLM's renamed API field. Critical for local LLM users.

3. **[#30485 – Fix task ID passed to background job for continuation](https://github.com/anomalyco/opencode/pull/30485)** (closed) — Allow follow-up prompts to reuse a running background task session, keeping continuations within one logical job lifecycle.

4. **[#30486 – Process prompts queued during loop shutdown](https://github.com/anomalyco/opencode/pull/30486)** (open) — Fixes a race condition where a prompt saved while an existing loop is exiting could join a stale run. Adds regression tests.

5. **[#30488 – Allow backgrounding synchronous subagents in TUI](https://github.com/anomalyco/opencode/pull/30488)** (open, beta) — Adds a background job promotion path so synchronous task subagents can be detached without restarting. Exposes `POST /experimental/session/:sessionID/background`.

6. **[#30482 – Route SAP AI Core reasoning variants through modelParams](https://github.com/anomalyco/opencode/pull/30482)** (open) — Fixes SAP provider's Zod schema stripping `reasoningEffort`/`thinking`/`thinkingConfig` parameters. Closes #30481.

7. **[#30473 – Move v1 schemas into core](https://github.com/anomalyco/opencode/pull/30473)** (closed) — Refactors legacy config and permission schemas out of compatibility layers and into `packages/core/src/v1`, cleaning up the import graph.

8. **[#30363 – Add status light indicator for TUI and Web UI](https://github.com/anomalyco/opencode/pull/30363)** (open) — Adds a configurable status light in the terminal title bar and Web UI session tabs reflecting the current session state. Closes #30272.

9. **[#26239 – Add /menu slash command](https://github.com/anomalyco/opencode/pull/26239)** (open) — A built-in `/menu` command that opens the TUI command menu (same as `Ctrl+P`), improving accessibility for users who prefer slash commands.

10. **[#29217 – Inline $skill invocations with SKILL pill + pasteText support](https://github.com/anomalyco/opencode/pull/29217)** (open) — Major UX enhancement: typing `$` surfaces available skills in autocomplete, with inline skill insertion and paste support. Closes 5 related issues.

## Feature Request Trends

- **Multi-skill & skill UX improvements** — Strong demand for invoking multiple skills in a single prompt (#25570), recursive skill discovery (#21495), and inline `$skill` autocomplete (#29217, #15617). Skills are becoming a core workflow primitive.
- **Subagent visibility** — Repeated requests for subagent tree views in TUI (#15223, #6299) and background job management (#30488). Users need better observability into parallel agent execution.
- **Pricing transparency & limit adjustments** — The DeepSeek price cut (#28846) has ignited broader frustration about OpenCode's pricing model relative to provider costs. Expect more pressure on subscription economics.
- **Provider/model UX** — Calls for nested provider groups in the model picker (#30459), model variant picker improvements (#30471), and better handling of provider-specific reasoning parameters (#19988, #30482).
- **Safety & guardrails** — The unauthorized DB modification incident (#27745) and discussion of agent-directed tool result trimming (#29758) signal growing interest in agent safety controls.

## Developer Pain Points

- **Agent reliability** — Random agent freezes (#24342, #30439), infinite loops consuming credits (#30450), and prematurely terminated inference are the most disruptive recurring issues.
- **Tool call & rendering bugs** — Malformed tool call tags (#9674), dangling XML closing tags (#27984), and the white rectangle cursor artifact (#30490) degrade the core interaction experience.
- **Memory instability** — The Memory Megathread (#20695) remains the top diagnostic priority, with scattered crashes across different providers and configurations.
- **Provider-specific breakage** — Frequent API compatibility issues with OpenAI/Codex (#30306, #30323), Vertex AI Gemini (#17519), Azure reasoning parameters (#27716), and SAP AI Core (#30482) suggest the provider abstraction layer needs more rigorous cross-provider testing.
- **TUI and Web UI regressions** — Auto-scroll failures (#29992), blank screens with plugins (#26217), and folder picker crashes (#22655) indicate ongoing UI polish gaps.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-03

## Today’s Highlights
The community remains focused on provider compatibility and Windows UX, with a critical fix for Anthropic’s Opus 4.8 adaptive thinking flowing through a PR that inherits model and thinking settings in agent‑tool calls. A new approval system for workspace extensions is proposed, and significant performance work landed to cache line resets in long TUI sessions. Several providers were added or updated, including ZAI Coding Plan China, Ant‑Ling, and MiniMax‑M3.

## Releases
No new releases in the last 24 hours.

## Hot Issues
*(10 noteworthy issues with community impact)*

1. **[#5223 – Anthropic provider modifies thinking blocks, causing 400 with Opus 4.8 adaptive thinking](https://github.com/earendil-works/pi/issues/5223)**  
   Multi‑turn conversations using Claude Opus 4.8 with adaptive thinking (`high` reasoning) fail mid‑session with a 400 error because the provider alters `thinking` blocks in the latest assistant message. 11 comments, 5 👍.

2. **[#5089 – `timeoutMs` not respected past a certain value](https://github.com/earendil-works/pi/issues/5089)**  
   Users running slow models (e.g., Qwen on CPU) find that pi ignores the configured timeout, leading to premature failures. 22 comments, 2 👍 – a longstanding pain point.

3. **[#5229 – MiniMax on OpenRouter broken: `developer` role deserialisation error](https://github.com/earendil-works/pi/issues/5229)**  
   `minimax/minimax-m2.5:free` returns a 400 because the provider does not accept `developer` role messages. 7 comments, 1 👍.

4. **[#5103 – Windows bash detector fails for non‑default Git Bash paths](https://github.com/earendil-works/pi/issues/5103)**  
   Users with Git Bash installed outside `C:\Program Files` (e.g., `D:\Program Files\Git\bin\bash.exe`) get “no bash shell found”. 5 comments. Affects many Windows developers.

5. **[#5226 – SDK embed requires `package.json` adjacent at runtime](https://github.com/earendil-works/pi/issues/5226)**  
   Bundled Node apps that embed `@earendil-works/pi-coding-agent` break because pi reads package‑adjacent metadata. 5 comments, related to bundling challenges.

6. **[#3406 – Scroll position jumps to top when resizing Windows Terminal](https://github.com/earendil-works/pi/issues/3406)**  
   Resizing the terminal window causes the message history to scroll to the top. 4 comments; a long‑standing Windows Terminal UX issue.

7. **[#5342 – Horizontal rails render as U+2500 and leak into paste buffer](https://github.com/earendil-works/pi/issues/5342)**  
   The `BorderedLoader` rails (`─`) are copied when selecting transcript regions, polluting the clipboard. 3 comments.

8. **[#5337 – `/new` session causes full command output to display without truncation](https://github.com/earendil-works/pi/issues/5337)**  
   After using `/new`, large command output is no longer truncated, removing the `Ctrl+O` tip. 3 comments – a regression.

9. **[#5301 – Path resolution behind a `Paths` object for XDG support](https://github.com/earendil-works/pi/issues/5301)**  
   A thoughtful proposal to centralise directory location logic, enabling opt‑in XDG layout. 3 comments. Previous discussions had rejected the idea; this implementation approach may reopen the debate.

10. **[#5323 – Improve Vertex + GCP metadata server support](https://github.com/earendil-works/pi/issues/5323)**  
    The current “is Vertex authed?” check is a synchronous `existsSync`, which fails when using metadata servers (e.g., on GCE). 3 comments.

## Key PR Progress
*(10 important PRs merged or still open)*

1. **[#5348 – Add selective pi-ai base entrypoints](https://github.com/earendil-works/pi/pull/5348)**  
   Introduces `@earendil-works/pi-ai/base` and `@earendil-works/pi-agent-core/base` for side‑effect‑free imports, enabling selective transport bundling.

2. **[#5333 – Add ZAI Coding Plan China provider](https://github.com/earendil-works/pi/pull/5333)**  
   New `zai-coding-cn` provider for `https://open.bigmodel.cn/api/coding/paas/v4`, with env key lookup and model generation.

3. **[#5332 – Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332) (OPEN)**  
   Proposes a `.pi.user` folder for user extensions and requires interactive approval on first load (or `-f` flag). Aims to improve security.

4. **[#5346 – Remove stale codex models](https://github.com/earendil-works/pi/pull/5346)**  
   Removes `gpt-5.2` and `gpt-5.3-codex` from the `opeai-codex` provider as they were sunset on June 2.

5. **[#5345 – Move temporary extension cache to per‑user directory](https://github.com/earendil-works/pi/pull/5345)**  
   Moves temp extensions to a location under `~/.pi/agent` on all platforms, improving isolation.

6. **[#5344 – Fix agent-tool `renderCall` inheriting model/thinking](https://github.com/earendil-works/pi/pull/5344)**  
   The inline agent‑call header now correctly displays the parent’s model and thinking setting, fixing a display bug that showed “thinking off” when the parent had thinking enabled.

7. **[#5343 – Perf: cache line resets across frames for long transcripts](https://github.com/earendil-works/pi/pull/5343)**  
   Caches `TUI.applyLineResets` results per row, dramatically reducing lag in long interactive sessions.

8. **[#5262 – Add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262) (OPEN)**  
   Adds a built‑in `anthropic-vertex` provider using `AnthropicVertex` SDK, reusing the existing Anthropic streaming path.

9. **[#5110 – Add Ant-ling provider with Ling-2.6-1T, Ling-2.6-flash & Ring-2.6-1T](https://github.com/earendil-works/pi/pull/5110) (CLOSED – inprogress)**  
   New `ant-ling` provider with OpenAI compatibility layer for the Ling/Ring 2.6 series.

10. **[#5284 – Add MiniMax-M3 to minimax and minimax-cn](https://github.com/earendil-works/pi/pull/5284)**  
    Adds MiniMax‑M3 (512K context, multimodal, reasoning enabled) to both native providers.

Other notable PRs:  
- [#5328 – Fix CJK text wrapping](https://github.com/earendil-works/pi/pull/5328)  
- [#5339 – Add `/config` and `/exit` aliases](https://github.com/earendil-works/pi/pull/5339)  
- [#5302 – Add `ui_prompt_start`/`ui_prompt_end` extension events](https://github.com/earendil-works/pi/pull/5302)  
- [#5254 – Replace chalk with `util.styleText`](https://github.com/earendil-works/pi/pull/5254)

## Feature Request Trends
- **New provider & model support**: MiniMax-M3 (multiple issues/PRs), AWS Bedrock GPT‑5.4/5.5, Ant‑Ling, ZAI Coding CN, Anthropic Vertex. The community consistently pushes for broader model coverage.
- **XDG directory layout**: Recurring request (#5301, #534, #2870, #3310) – a new implementation proposal may finally break the deadlock.
- **Structured output (JSON schema)**: #1086 remains a sought‑after feature for deterministic automation.
- **Remote execution**: SSH‑based remote containers (#5341) and approval systems for extensions (#5332) signal a desire for secure remote workflows.
- **User‑experience polish**: CJK text wrapping, command aliases (`/config`, `/exit`), session naming, and consistent `BorderedLoader` rendering are small but frequent asks.

## Developer Pain Points
- **Windows inconsistencies**: Bash detection fails for non‑default Git Bash paths; scroll position jumps in Windows Terminal; CJK wrapping issues – all erode the Windows experience.
- **Timeout/respect of user settings**: `timeoutMs` not honoured (#5089), infinite timeout ignored (#5294), and `Shift+Enter` keybinding conflicts (#5188) cause frustration.
- **Provider compatibility breakage**: Anthropic thinking blocks mis‑handled, MiniMax developer role error, Kimi thinking error on OpenRouter – each new provider update risks breaking pi.
- **Bundling and runtime assumptions**: SDK embed requiring adjacent `package.json` (#5226) and crashes when background processes emit late output (#5208) hurt developers integrating pi into their own tools.
- **Performance degradation in long sessions**: TUI lag grows with transcript length, partially addressed by #5343, but remains a pain point for power users.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-03

## Today’s Highlights

The Qwen Code team shipped two new releases (including `v0.17.0-preview.0`) with a critical fix for false “compressed turn” errors during rewind, while the community reported multiple body-timeout issues with slow local models and debated a project-scoped `.mcp.json` approval mechanism. Pull requests landed for configurable streaming timeouts, CPU profiling support, and an improved IME input experience, alongside early work on a skills picker dialog and user prompt expansion hooks.

## Releases

Two versions were published in the last 24 hours:

- **[v0.17.0-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0-preview.0)** – Chore release preparing the full v0.17.0; includes a fix for the rewind command falsely reporting “compressed turn” errors when mid-turn messages existed ([PR #4626](https://github.com/QwenLM/qwen-code/pull/4626)).
- **[v0.17.0-nightly.20260603.68408c30c](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0-nightly.20260603.68408c30c)** – Nightly tracking the same rewind fix.

## Hot Issues (10 of 33 updated in last 24h)

1. **[#4663 – Add MiniMax-M3 and checkbox-based model selection](https://github.com/QwenLM/qwen-code/issues/4663)** (CLOSED)  
   *Why it matters:* Users want official MiniMax-M3 model IDs and a multi-select UI instead of comma-separated free-text for API key setup. The 8 comments show strong alignment – the feature was quickly closed, likely merged in a PR.

2. **[#4604 – API Error: terminated (cause: Body Timeout Error)](https://github.com/QwenLM/qwen-code/issues/4604)** (CLOSED)  
   *Why it matters:* Intermittent timeouts on web-page processing tasks. The 5 comments include client logs; this is a high-pain issue that may be resolved by the configurable bodyTimeout PR (#4667).

3. **[#4615 – Project-scoped .mcp.json support with pending approval semantics](https://github.com/QwenLM/qwen-code/issues/4615)** (OPEN)  
   *Why it matters:* Enables checked-in MCP server configs in repos, with an explicit approval gate before servers are started. The 4 comments discuss alignment with Claude Code’s model – a PR (#4713) already exists.

4. **[#4711 – Body Timeout Error for slow self-hosted model](https://github.com/QwenLM/qwen-code/issues/4711)** (OPEN)  
   *Why it matters:* Local models that are slightly slow fail at 85% due to a hard-coded 5‑minute body timeout. User asks for a configurable limit – directly addressed by PR #4667.

5. **[#4676 – Auto-mode classifier times out too easily](https://github.com/QwenLM/qwen-code/issues/4676)** (CLOSED)  
   *Why it matters:* The two-stage LLM classifier for AUTO approval fails closed on timeout, blocking actions. The 3 comments and 1 thumbs-up show developer consensus that stage timeouts need loosening and thinking should be disabled in all stages.

6. **[#4714 – Disable auto-created skills](https://github.com/QwenLM/qwen-code/issues/4714)** (OPEN)  
   *Why it matters:* Auto-generated skills, often hallucinated, get high priority and override user-defined skills. User explicitly asks for an opt-out option. 2 comments, feature request with `need-information` status.

7. **[#4718 – Published CLI bundle omits extension examples](https://github.com/QwenLM/qwen-code/issues/4718)** (OPEN)  
   *Why it matters:* `qwen extensions new` fails because `dist/examples/` is not bundled in the npm package. Bug blocks users from creating new extensions. The 2 comments confirm the packaging gap – PR #4719 already submitted.

8. **[#4700 – Dead loop and fails to auto-understand images](https://github.com/QwenLM/qwen-code/issues/4700)** (OPEN)  
   *Why it matters:* The tool (v0.17) enters an infinite `readFile` loop when saving memory, and does not autonomously interpret posted images unless explicitly prompted. 2 comments, Chinese report with screen captures of a 13‑minute loop.

9. **[#4593 – `/clear` should not switch to a new session ID](https://github.com/QwenLM/qwen-code/issues/4593)** (CLOSED)  
   *Why it matters:* `/clear` currently creates a new session, breaking session‑based debugging and log lookup. Users expect the session ID to stay the same and only the conversation to be cleared. 2 comments, closed with fix likely merged.

10. **[#4575 – Auto-mode and auto-accept edits share same indicator color](https://github.com/QwenLM/qwen-code/issues/4575)** (CLOSED)  
    *Why it matters:* Both modes use yellow warning color – no visual distinction can confuse users. 2 comments, design bug closed with PR #4674 renaming “Default” to “Ask Permissions” but indicator color fix may be separate.

## Key PR Progress (10 of 50 updated in last 24h)

1. **[#4677 – Fix vim mode Esc leak, Enter submit, render lag and implement missing VIM commands](https://github.com/QwenLM/qwen-code/pull/4677)** (OPEN)  
   *Impact:* Solves three major vim mode issues that caused input buffer clearing and interrupted model responses. Adds NORMAL mode commands for power users.

2. **[#4665 – Add InstructionsLoaded hook for instruction file loading](https://github.com/QwenLM/qwen-code/pull/4665)** (OPEN)  
   *Impact:* New hook fires when instruction/context files are loaded, enabling extensions to react to memory discovery and `@` imports. Part of the `hooks-events` roadmap.

3. **[#4667 – Add configurable bodyTimeout to prevent streaming timeout with local models](https://github.com/QwenLM/qwen-code/pull/4667)** (CLOSED)  
   *Impact:* Directly addresses the #4604 & #4711 body timeout pain points – adds `generationConfig.bodyTimeout` (default 0 = disabled) to override the 300s undici default for slow local backends.

4. **[#4706 – Fix statusline not re-rendering when switching from preset to command type](https://github.com/QwenLM/qwen-code/pull/4706)** (OPEN)  
   *Impact:* `/statusline [prompt]` changed config type on disk but stale in-memory state kept the old display. Adds `LoadedSettings` update to fix the stale indicator.

5. **[#4713 – Project .mcp.json + workspace approval gating with aligned scope precedence](https://github.com/QwenLM/qwen-code/pull/4713)** (OPEN)  
   *Impact:* Implements the feature requested in #4615. Project `.mcp.json` and global `.mcp.json` are treated as untrusted‑until‑approved, with a clear precedence model.

6. **[#4533 – `/skills` picker dialog – browse, search, toggle, pick](https://github.com/QwenLM/qwen-code/pull/4533)** (OPEN)  
   *Impact:* Replaces bare `/skills` with an interactive picker, plus workspace-scoped `skills.disabled` array. A major UX improvement for skill management.

7. **[#4436 – Enhance system prompts with global reasoning discipline and iterative planning](https://github.com/QwenLM/qwen-code/pull/4436)** (CLOSED)  
   *Impact:* Improves system prompts across the codebase to encourage step‑by‑step reasoning and iterative planning – likely to improve overall agent quality.

8. **[#4694 – Compacted session replay for long-session recovery](https://github.com/QwenLM/qwen-code/pull/4694)** (OPEN)  
   *Impact:* Replaces unbounded raw-event JSONL with turn-boundary compaction, reducing memory/disk footprint during long sessions. Important for daemon stability.

9. **[#4620 – Add CPU profiling support for Chrome DevTools analysis](https://github.com/QwenLM/qwen-code/pull/4620)** (CLOSED)  
   *Impact:* Adds `.cpuprofile` generation via `QWEN_CODE_CPU_PROFILE=1` env var or `SIGUSR1` – a powerful debugging tool for performance analysis.

10. **[#4708 – Allow intentional foreground sleep for backoff](https://github.com/QwenLM/qwen-code/pull/4708)** (OPEN)  
    *Impact:* Adds an escape hatch (`# intentional-sleep: <reason>`) so that agents can legitimately sleep for rate‑limit backoff without being blocked by the foreground sleep interceptor.

## Feature Request Trends

- **MCP security & workspace gating** – Multiple issues (#4615, PR #4713) ask for project‑scoped `.mcp.json` with approval semantics, mirroring Claude Code’s model.
- **Configurable timeouts & retry logic** – Body timeout (#4667), auto‑classifier stage timeouts (#4676), and intentional sleep for backoff (#4708) indicate a need for fine‑grained control over network and LLM latency.
- **Skill/prompt management** – Auto‑created skills (#4714), skills picker dialog (#4533), and user prompt expansion hooks (#4377) show a desire to give users more control over agent behavior.
- **Session/storage improvements** – Clear session semantics (#4593), OOM during quit (#4698), and runtime output directory configuration (#4709) highlight ongoing work on session and memory management.
- **IME and terminal UX** – CJK IME composition position (#3456), space key in arena dialog (#4692), and vim mode fixes (#4677) are part of an ongoing terminal UX polish effort.

## Developer Pain Points

- **Body timeout errors with local models** – Multiple users hit the 300‑second default timeout (#4604, #4711, #4605). The fix (#4667) is merged but not yet in a stable release.
- **Infinite loops and tool‑call loops** – The tool enters a `readFile` loop (#4700) and deepseek‑v4‑pro collapses into repeated identical tool calls (#4695) – both point to missing client‑side circuit‑breakers.
- **Interface flickering and rendering issues** – Long‑standing reports (#1491, #3007, #2950, #2972) persist, especially during context‑heavy sessions and when pressing Ctrl‑E/Ctrl‑F.
- **Lack of control over auto‑generated skills** – Users (#4714) are frustrated by auto‑created skills with high priority that contradict manually written ones.
- **Missing or broken extension packaging** – The CLI bundle omits extension example templates (#4718), blocking extension creation for new users.
- **Headless Linux crashes** – Commands like `/bug`, `/docs`, `/insight` crash with `ENOENT` for `xdg‑open` on headless systems (#4712).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

Here is the **DeepSeek TUI (now CodeWhale) community digest** for **2026-06-03**.

---

## DeepSeek TUI / CodeWhale — Community Digest
**Date:** 2026-06-03 | **Source:** github.com/Hmbown/DeepSeek-TUI (primary), github.com/Hmbown/CodeWhale (current)

---

### 1. Today’s Highlights

The project officially rebranded from **DeepSeek TUI** to **CodeWhale** with the v0.8.50 release, though legacy binary shims will persist until v0.9.0. The community’s attention is divided between **major UX regressions** (e.g., ANSI control sequence leakage, TUI composer bugs) introduced in v0.8.50 and a high volume of **ecosystem expansion PRs** adding new providers (Arcee AI, SiliconFlow China), hook systems, and localization support. A long-standing Chinese-market bug about Docker garbled output remains the most commented issue in the project’s history (195 comments).

---

### 2. Releases

**v0.8.50** — *CodeWhale Rename Release*
- **Core Change:** The project is now **CodeWhale**. Legacy binaries (`deepseek`, `deepseek-tui`) remain as deprecation shims and will be removed in v0.9.0.
- **Warning:** v0.8.50 introduces at least one confirmed regression: ANSI control sequence leakage causing garbage `[` characters and broken Backspace in the composer (Issue #2592).

---

### 3. Hot Issues (Top 10)

1. **[#1615] Docker garbled output** [CLOSED]  
   *195 comments* — A Chinese-language user reports that the Docker image crashes immediately with garbled text. This issue has become the community’s most heated thread, reflecting significant onboarding friction for non-English users.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1615)

2. **[#2487] “Turn stalled” error in YOLO mode** [OPEN]  
   *12 comments* — The agent freezes mid-turn with “no completion signal received.” Users report that sending `continue` does not rescue the session. A high-impact bug for anyone using autonomous agent workflows.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2487)

3. **[#1579] UI color scheme is ugly** [OPEN]  
   *9 comments* — A persistent design complaint about the default color palette. While subjective, it signals a need for theming or a better default scheme.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1579)

4. **[#1269] Agent stuck on “working” / no feedback** [OPEN]  
   *7 comments* — The agent hangs indefinitely after receiving a task, with no error output. `doctor` check shows nothing wrong. Indicates a silent failure in the engine task lifecycle.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1269)

5. **[#1826] `@` file mention cannot navigate deep directories** [OPEN]  
   *5 comments* — The file picker does not support deep directory navigation, making it hard to reference nested files by name. A UX friction point for large projects.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1826)

6. **[#1978] OpenRouter / ZenMux custom base_url feature parity test** [OPEN]  
   *5 comments* — A detailed comparison showing that ZenMux (sk-ss-v1) lacks caching support for DeepSeek V4 models. Valuable for users relying on third-party routing.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1978)

7. **[#2592] [Regression v0.8.50] ANSI control sequence leakage** [CLOSED]  
   *3 comments* — A re-introduced bug where terminal escape codes leak into the composer, causing `[` garbage and broken backspace. Core typing functionality is broken for affected users.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2592)

8. **[#2584] Cannot attach local images via `/attach`** [OPEN]  
   *4 comments* — The model only receives a file path instead of base64-encoded image data when using `/attach`. Breaks multimodal workflows.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2584)

9. **[#2583] “Engine has stopped” error persists in v0.8.50** [OPEN]  
   *4 comments* — A recurring fatal error where the engine task dies mid-turn, leaving the user with a frozen UI.   
   [Link](https://github.com/Hmbown/CodeWhale/issues/2583)

10. **[#755] Chinese-market improvements tracker** [OPEN]  
    *5 comments / 3 👍* — A meta-issue tracking platform-aware UI labels, web-search backend for Chinese users, and AgentScope integration. Indicates strategic focus on the Chinese developer market.  
    [Link](https://github.com/Hmbown/CodeWhale/issues/755)

---

### 4. Key PR Progress (Top 10)

1. **[#2595] Add direct Arcee AI provider support**  
   Adds Arcee AI as a first-class provider with full config, CLI, and TUI integration.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2595)

2. **[#2585] Fix engine task death mid-turn — recover UI immediately**  
   When the engine panics between `TurnStarted` and `TurnComplete`, the UI now detects the disconnect and recovers instead of hanging.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2585)

3. **[#2587] Fix `/attach` images not sending as multimodal content**  
   Converts local images to base64 `data:` URLs for OpenAI-compatible multimodal models.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2587)

4. **[#2591] Fix diff rendering: preserve leading whitespace**  
   Patch content in Diff Preview cards was left-aligned due to `split_whitespace()`. Now preserves indentation.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2591)

5. **[#2593] Fix Ctrl+P file picker honoring `mention_walk_depth`**  
   The Ctrl+P file picker now respects the configured walk depth, matching `@` completion behavior.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2593)

6. **[#2588] Add SiliconFlow China region provider**  
   Adds `siliconflow-cn` as a separate provider with its own endpoint and API key for users in China.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2588)

7. **[#2557] Add `!` bang shell command shortcut**  
   Users can now run explicit shell commands from the TUI input box using `! <command>`. Routes through `exec_shell`.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2557)

8. **[#2572] Localize context inspector across 7 locales**  
   A major i18n push: localizes the `Alt+C` context inspector surface into 7 languages, including headers and labels.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2572)

9. **[#2479] Collapse ProviderKind/ApiProvider dual enums behind a Provider trait**  
   Refactors provider handling into a single `Provider` trait with 15 concrete implementations, reducing duplication.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2479)

10. **[#2508] Configurable path suffix for OpenAI-compat endpoints**  
    Allows users to set `path_suffix` (e.g., `/v2` or empty string) for third-party APIs that don’t follow the `/v1/chat/completions` convention.  
    [Link](https://github.com/Hmbown/CodeWhale/pull/2508)

---

### 5. Feature Request Trends

- **Multi-Provider & Model Flexibility:** A strong push for supporting more custom models and providers, including Arcee AI, SiliconFlow China, and automated fallback chains (#2574, #2596, #1874, #2508).
- **Workflow & Session Management:** Users want better visibility into auto-mode routing (#2380), the ability to reload instructions on model switch (#2379), and session commands routed to a spatial workbench (#1892).
- **Cross-Editor Context Bridge:** A feature to send editor selections, diagnostics, and diffs directly into CodeWhale from IDEs (#1985).
- **Internationalization (i18n):** Localization efforts are active (PR #2572), especially for Chinese-market users (tracking issue #755).
- **TUI Customization:** Demand for resizable sidebar (#2602) and better default color scheme (#1579).

---

### 6. Developer Pain Points

- **Chinese User Onboarding Issues:** The Docker garbled-text bug (#1615) received 195 comments, reflecting systemic frustration with Chinese-localized documentation and default configurations.
- **Stability Regression in v0.8.50:** The re-emergence of the ANSI control sequence leakage bug (#2592) and lingering “engine has stopped” errors (#2583) are eroding trust in release quality.
- **Windows Support Gaps:** Shell tools (`exec_shell`, `task_shell`) remain unavailable on Windows due to sandbox initialization failures (#2589). A request for an NSIS installer (#1987) highlights Windows UX gaps.
- **Silent Engine Failures:** Multiple issues (#1269, #2487) describe agents getting stuck with no error message, leaving users in the dark about root causes. The `doctor` command often reports “no issues” while the agent is unresponsive.
- **Transparency / Debugging:** Developers request a `/dryrun` command (#1004) to preview what the model will actually receive before sending a turn, to avoid burning expensive V4 Pro tokens on incorrect context.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*