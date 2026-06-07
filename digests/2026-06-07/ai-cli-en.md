# AI CLI Tools Community Digest 2026-06-07

> Generated: 2026-06-07 02:50 UTC | Tools covered: 9

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
**Date:** 2026-06-07 | **Analyst:** Senior Technical Analyst, AI Developer Tools

---

## 1. Ecosystem Overview

The AI CLI tools landscape is entering a maturity phase characterized by three simultaneous dynamics: **convergence on core infrastructure patterns** (MCP, agent orchestration, session management), **divergence in provider strategy and community engagement**, and **increasing user sophistication** demanding autonomous, long-running agents rather than session-based assistants. The ecosystem is dominated by Claude Code's sustained high engagement and OpenCode's aggressive refactoring cadence, while smaller tools like Pi and Kimi show targeted, lower-volume innovation. A clear pattern emerges: communities are pushing past "chat with codebase" into "autonomous developer agent" territory, exposing deep reliability and scalability challenges around memory, tool call parsing, and cross-platform stability.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Active PRs (24h) | Release Today | Community Notes |
|---|---|---|---|---|
| **Claude Code** | 10 major (high engagement) | 5 merged/updated | ✅ v2.1.168 | Highest per-issue engagement (97👍, 48 comments) |
| **OpenAI Codex** | 10 major | 10 notable | ✅ rust-v0.138.0-alpha.6 | Balanced PR/issue activity; major refactors in flight |
| **Gemini CLI** | 10 notable | 10 important | ❌ None | High signal: security fixes, subagent reliability |
| **GitHub Copilot CLI** | 10 noteworthy | 0 notable | ❌ None | Low engineering activity; community frustrated with regressions |
| **Kimi Code CLI** | 0 | 2 updated | ❌ None | Quietest in ecosystem; only 2 long-standing PRs touched |
| **OpenCode** | 10 top by relevance | 10 high impact | ❌ None | Intense refactoring: 6 PRs from kitlangton alone |
| **Pi** | 10 | 6 closed | ❌ None | Busiest bug-closure day (9 closed); focused small team |
| **Qwen Code** | 10 of 29 updated | 10 of 33 updated | ✅ v0.17.1-nightly | Highest raw volume: 33 PRs, 29 issues updated |
| **DeepSeek TUI** | 10 by relevance | 10 by impact | ❌ None | Release process in progress; systematic gate-checking |

**Key insight:** The ecosystem splits into two tiers — **high-velocity tools** (OpenCode, Qwen, DeepSeek TUI) driving major architecture changes, and **stabilization-focused tools** (Claude Code, Codex, Gemini) iterating on reliability and UX. Copilot CLI and Kimi show concerningly low engineering activity relative to community demand.

---

## 3. Shared Feature Directions

| Pattern | Tools Demonstrating | Specific Community Needs |
|---|---|---|
| **Autonomous Orchestrators** | Claude Code (#56913), OpenCode (#31173 task tool), Gemini CLI (#22323 subagent), DeepSeek TUI (#2666 telemetry) | Tiered model brains + worker agents, persistent state, long-running background tasks, task delegation with observability |
| **MCP/Plugin Maturity** | Claude Code (allowed-tools docs), Codex (#26234 namespace flattening), Copilot CLI (#3028 permissions, #3701 spawning), Kimi (#1769 graceful degradation), Qwen (#4713 approval gating), OpenCode (#28662 filtering) | Permission systems, graceful failure, non-OpenAI provider compatibility, OAuth lifecycle management, session ID persistence |
| **Extended Thinking / Reasoning Transparency** | Claude Code (#49268, #49322, #63358), Qwen (#4686 repetitive garbage) | Proper rendering of thinking blocks, model selection indicators, user visibility into reasoning state |
| **Session & History Management** | Codex (#13018 thread deletion, #23979 history loss), OpenCode (#16270 session picker, #4704 undo reliability), Qwen (#4825 sessions list), Pi (#5291 session hangs) | Real deletion (not archiving), long-session resilience, CLI-based listing, reliable undo across git/non-git projects |
| **Cross-Platform Reliability** | Copilot CLI (#3700 WSL CPU regression), OpenCode (#27749 Windows terminal death, #26846 NixOS segfault), Qwen (#4720 Windows SMB paths), Gemini CLI (#27385 Node 20/Windows symlinks) | WSL performance, Windows terminal behavior, macOS freezes, NixOS compatibility, SMB path handling |
| **Cost & Model Flexibility** | Copilot CLI (#3707 open-weight models, #3705 free tier), Gemini CLI (#27718 model alias visibility), OpenCode (#9281 usage tracking) | Cheaper model options, bring-your-own-key, provider switching, usage/cost dashboards |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Qwen Code |
|---|---|---|---|---|---|---|
| **Primary Focus** | Autonomous orchestration & extended thinking | App architecture & extension APIs | Agent reliability & memory subsystem | GitHub ecosystem integration | Core architecture refactoring | Daemon mode & ACP protocol |
| **Target User** | Professional developers (paid agents) | OpenAI ecosystem users | Google ecosystem developers | GitHub/VS Code users | Multi-provider power users | Qwen model ecosystem |
| **Technical Approach** | Monolithic agent with subagents | Modular crate architecture | Component-level evaluations | Thin CLI over Copilot API | Effect-ts functional architecture | Daemon + ACP REST/WS |
| **Pain Point Ownership** | Tool call parsing fragility | Thread lifecycle gaps | Subagent false success reporting | WSL2 CPU regressions | Windows terminal management | OOM crashes |
| **Community Engagement** | Very high (deep issue discussion) | High (structured issue tracker) | Moderate (focused on P1/P2) | Low (5 PRs/month avg) | Very high (refactor-driven) | Very high (raw volume leader) |
| **Release Cadence** | Frequent minor patches | Regular alpha releases | No daily releases | No daily releases | No daily releases | Nightly + feature batches |
| **Differentiator** | Longest-running autonomous agent vision | Strongest extension API | Best security practices (command injection fixes) | Deepest IDE integration | Most aggressive architecture cleanup | Fastest protocol expansion (ACP) |

**Notable:** Pi differentiates on **workspace security** (#5332 approval system) and minimal footprint. DeepSeek TUI differentiates on **multi-platform** (VS Code Agent View, AWS Lightsail bridge) and Chinese-language community engagement. Kimi is undifferentiated — effectively in maintenance mode.

---

## 5. Community Momentum & Maturity

| Tier | Tool | Momentum Signal | Maturity Assessment |
|---|---|---|---|
| **Tier 1: Most Active** | **Claude Code** | Sustained high engagement on core bugs (thinking rendering, tool call parsing). Deep feature debates on autonomous agents. | Mature product with growing pains. Community driving roadmap direction. |
| | **OpenCode** | kitlangton's 6 refactoring PRs in parallel. Bedrock regression fixed in same release cycle. | Rapidly maturing architecture. Leading in functional programming patterns for agent tools. |
| | **Qwen Code** | 33 PRs + 29 issues updated in 24h. Daemon mode batch merge (+115k LOC). Highest raw velocity. | Early-major: building core infrastructure rapidly. Stability lagging behind feature velocity. |
| **Tier 2: Steady** | **OpenAI Codex** | 10 PRs including security fix (#26713), global instruction refactor (#26834). Balanced feature/bug ratio. | Mature architecture, methodical evolution. Not chasing flashy features. |
| | **Gemini CLI** | Security-first culture (command injection patches). Subagent reliability improvements. | Production-grade stability focus. Lower feature velocity but high reliability. |
| | **DeepSeek TUI** | v0.9.0 release process with formal acceptance matrix. Command refactor layered approach. | Systematic engineering. Building platform features before community demands them. |
| **Tier 3: Stabilizing** | **Pi** | 9 bugs closed in one day. Approval system merged. | Small, well-scoped tool. Healthier than volume suggests. |
| **Tier 4: At Risk** | **Copilot CLI** | 0 notable PRs. WSL regression unresolved. Low issue engagement (2👍 on critical bug). | Community interest outstripping engineering response. MCP integration gaps widening. |
| | **Kimi Code CLI** | 0 issues created/updated. 2 stale PRs touched. | Effectively dormant. Community may be migrating. |

---

## 6. Trend Signals

### Emerging Industry Requirements

1. **Thinking Transparency is Table Stakes** — Across Claude Code and Qwen, users demand visible, reliable extended thinking rendering. This is no longer a "nice to have"; it's a core UX expectation for reasoning models. Tools that fail here (Claude Code's repeated regressions) lose trust fast.

2. **Autonomous Agent Orchestration is the Next Battleground** — The most forward-leaning feature requests across every major tool envision Claude Code/OpenCode/Gemini as 24/7 orchestrators: tiered models, background workers, persistent state, task delegation with observability. The CLI is becoming an agent runtime, not a chat interface.

3. **MCP Standardization is Fractured But Converging** — Every tool implementing MCP hits the same pain points: permission models, OAuth credential reuse, namespace serialization for non-OpenAI providers, graceful failure on port conflicts. The ecosystem needs a shared best-practice document; currently each tool reinvents the wheel.

4. **Daemon Mode Shifts the Architecture** — Qwen's ACP WebSocket/REST work and OpenCode's server API refactoring signal a shift from CLI-only to CLI + persistent daemon + protocol adapters. This enables IDE integration, remote control, and CI/CD embedding. Expect more tools to follow.

5. **Windows/WSL is the Tipping Point** — Copilot CLI's WSL CPU regression, OpenCode's terminal death, Qwen's SMB issues: Windows remains the weakest platform. As AI CLI tools target enterprise developers (many on Windows), cross-platform reliability is a competitive differentiator.

6. **Cost Consciousness Drives Model Selection Features** — Users are demanding cheaper model options, BYOK, usage tracking, and free tiers. Tools that provide transparent cost/usage dashboards (OpenCode #9281, Copilot CLI #3707) will win price-sensitive developers.

7. **Session as a First-Class Entity** — Codex (#13018 thread deletion), OpenCode (#16270 session picker), and Qwen (#4825 sessions list) all treat session management as a core feature, not an afterthought. Long-lived, resumable, queryable sessions are becoming the standard.

8. **Declarative Agent Definitions** — Claude Code's `.claude/agents/*.md` pattern is being requested as a native feature in Qwen (#4821) and DeepSeek TUI. This pattern (YAML frontmatter + markdown instructions) reduces friction for custom agent creation without TypeScript changes.

### Actionable Insights for Developers

- **If you value stability:** Choose Gemini CLI (security-focused) or Pi (well-scoped, high bug-fix velocity).
- **If you want cutting-edge orchestration:** Watch OpenCode (best architecture for autonomous agents) and Claude Code (most mature vision, despite bugs).
- **If you need cross-platform reliability:** Avoid Copilot CLI on WSL until #3700 is resolved. OpenCode has known Windows terminal issues. Claude Code and Codex are most cross-platform mature.
- **If you're building on MCP:** Expect to handle edge cases yourself. None of the tools have perfect MCP integration. Gemini CLI's security patches are a reference for command injection prevention.
- **If you care about cost:** Copilot CLI's multi-model support is weakest. OpenCode and Claude Code offer the most flexibility for provider switching. Monitor Qwen for local/Ollama performance (#4657).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-07 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

**Most discussed Skills by community attention (PRs)**

**#514 — document-typography** *(Open)*
- **Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents
- **Discussion highlights**: Addresses pervasive quality issues affecting virtually every Claude-generated document. Strong resonance with users producing long-form content.
- **Status**: Open since 2026-03-04, actively discussed
- 🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

**#486 — ODT Skill** *(Open)*
- **Functionality**: OpenDocument text creation, template filling, and ODT-to-HTML conversion for LibreOffice/ISO-standard workflows
- **Discussion highlights**: First-class ODF support fills a major interoperability gap for enterprise and open-source toolchain users.
- **Status**: Open since 2026-03-01, extensive discussion
- 🔗 [PR #486](https://github.com/anthropics/skills/pull/486)

**#210 — frontend-design improvement** *(Open)*
- **Functionality**: Revises the existing frontend-design skill for clarity, actionability, and single-conversation coherence
- **Discussion highlights**: Focus on making instructions Claude-can-follow rather than human-readable documentation. Quality-of-life improvement for the Skill itself.
- **Status**: Open since 2026-01-05, active community input
- 🔗 [PR #210](https://github.com/anthropics/skills/pull/210)

**#83 — skill-quality-analyzer + skill-security-analyzer** *(Open)*
- **Functionality**: Meta-skills evaluating Skills across five dimensions (Structure, Security, Documentation, etc.)
- **Discussion highlights**: Self-referential quality tooling signals the community's interest in Skills governance and hardening.
- **Status**: Open since 2025-11-06, sustained conversation
- 🔗 [PR #83](https://github.com/anthropics/skills/pull/83)

**#181 — SAP-RPT-1-OSS predictor** *(Open)*
- **Functionality**: Wraps SAP's open-source tabular foundation model for predictive analytics on SAP business data
- **Discussion highlights**: Enterprise AI integration — first SAP-specific Skill, appeals to the ERP/analytics community.
- **Status**: Open since 2025-12-28
- 🔗 [PR #181](https://github.com/anthropics/skills/pull/181)

**#723 — testing-patterns** *(Open)*
- **Functionality**: Comprehensive testing guidance including Testing Trophy model, AAA pattern, React Testing Library, and bug reproduction
- **Discussion highlights**: Broad developer demand for structured test generation and quality assurance guidance within Claude.
- **Status**: Open since 2026-03-22
- 🔗 [PR #723](https://github.com/anthropics/skills/pull/723)

**#568 — ServiceNow platform skill** *(Open)*
- **Functionality**: Broad ServiceNow assistant covering ITSM, ITOM, ITAM, SecOps, HRSD, SPM, IntegrationHub, and CSDM
- **Discussion highlights**: Largest-scope enterprise Skill submitted; covers nearly the entire ServiceNow ecosystem.
- **Status**: Open since 2026-03-08
- 🔗 [PR #568](https://github.com/anthropics/skills/pull/568)

**#190 — n8n-builder / n8n-debugger** *(Open)*
- **Functionality**: Skills for building n8n automation workflows from scratch and debugging existing ones (plus faf-expert and related tools)
- **Discussion highlights**: Automation workflow creation is a recurring theme; n8n as a platform has strong community pull.
- **Status**: Open since 2025-12-31, recently updated
- 🔗 [PR #190](https://github.com/anthropics/skills/pull/190)

---

## 2. Community Demand Trends

*Derived from Issues with highest engagement and reaction counts*

**🔹 Organizational Skill Sharing & Management** (Issue #228 — 13 comments, 7 👍)
The most-voted feature request: direct org-wide skill sharing without manual file transfer. Users want shared libraries and distribution links within Claude.ai. This signals that Skills are moving from individual experimentation to team-scale deployment.

**🔹 Evaluation & Tooling Reliability** (Issue #556 — 11 comments, 6 👍; Issue #202 — 8 comments)
Multiple reports that `run_eval.py` cannot actually trigger Skills during testing (0% trigger rate). The community is demanding robust evaluation tooling before submitting production Skills. Issue #202 calls for skill-creator itself to be rewritten as an operational instruction set rather than developer documentation.

**🔹 Security & Namespace Trust** (Issue #492 — 7 comments, 2 👍)
Concerns about community Skills distributed under `anthropic/` namespace creating trust boundary abuse. Users want clear provenance and permission boundary enforcement — a sign of Skills entering sensitive enterprise environments.

**🔹 Duplicate/Installation Management** (Issue #189 — 6 comments, 8 👍)
Installation of `document-skills` and `example-skills` plugins creates identical Skill entries. Users want deduplication and cleaner dependency management; the "most-voted" reaction (8 👍) indicates broad frustration.

**🔹 Agent Governance & Safety Patterns** (Issue #412 — 4 comments)
Proposal for an agent-governance Skill covering policy enforcement, threat detection, and audit trails. No existing Skill addresses this — represents a gap the community is identifying.

**🔹 Multi-file Skill Bundling** (Issue #1220 — 2 comments)
As Skills grow in complexity, users want reference files bundled inline rather than split across SKILL.md + external refs. Maintainability vs. performance tension.

---

## 3. High-Potential Pending Skills

*Active-comment PRs not yet merged — likely to land soon based on development momentum*

| PR | Skill | Last Updated | Why It's Close |
|----|-------|-------------|----------------|
| [#1140](https://github.com/anthropics/skills/pull/1140) | **agent-creator** (meta-skill) | 2026-06-02 | Fixes #1120; includes Windows support and multi-tool evaluation fix; very recent activity |
| [#363](https://github.com/anthropics/skills/pull/363) | **feature-dev** workflow fix | 2026-06-03 | Fixes TodoWrite overwrite bug causing phase skipping; most recently updated of all open PRs |
| [#568](https://github.com/anthropics/skills/pull/568) | **ServiceNow platform** | 2026-04-23 | Large, well-structured enterprise Skill; sustained discussion |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | 2026-04-21 | Comprehensive scope; fills a clear developer need |
| [#444](https://github.com/anthropics/skills/pull/444) | **AURELION suite** (kernel, advisor, agent, memory) | 2026-05-06 | Four interconnected Skills for cognitive framework + persistent memory; ecosystem-level contribution |
| [#1099](https://github.com/anthropics/skills/pull/1099) | **skill-creator** Windows fix | 2026-05-24 | Critical bug fix for cross-platform usability; blockers for Windows contributors |
| [#1050](https://github.com/anthropics/skills/pull/1050) | **skill-creator** Windows subprocess fix | 2026-05-24 | Companion to #1099; both address Windows platform paralysis |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *enterprise document workflow Skills* (typography, ODT, ServiceNow, SAP) combined with *reliable Skill development tooling* (evaluation, Windows support, deduplication, security scoping)** — the ecosystem is maturing from individual productivity hacks toward production-grade, organization-wide deployment, and the infrastructure to support it.

---

# Claude Code Community Digest — 2026-06-07

## Today’s Highlights

A minor bugfix release (v2.1.168) landed, but the real story is the community’s growing frustration with Opus 4.x extended thinking rendering: two high-engagement issues (#49322, #49268) remain open for over a month, and a new Opus 4.8 regression (#63358) rehashes the same pattern. Meanwhile, a bold feature request for “tiered Opus brains + Sonnet workers” (#56913) signals deep interest in running Claude Code as a long-running autonomous orchestrator, not just a chat interface.

## Releases

**v2.1.168** — *Bug fixes and reliability improvements*. No detailed changelog provided.  
[Release link](https://github.com/anthropics/claude-code/releases/tag/v2.1.168)

## Hot Issues (10 of note)

1. **#62123** — [Bug] Model’s tool call could not be parsed (retry also failed)  
   MacOS / VS Code. Opus 4.7 generates tool calls that fail parsing, stopping workflows. 48 comments, 97 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/62123)

2. **#49322** — [BUG] Opus 4.7 thinking summaries not rendered in VS Code extension  
   Extended thinking summaries never appear in the VS Code chat panel. 44 comments, 39 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/49322)

3. **#49268** — Thinking summaries missing on Opus 4.7 — harness doesn’t set display: “summarized”  
   Deep technical root cause identified: API default changed. 44 comments, 70 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/49268)

4. **#23377** — [BUG] GitHub Issue Prompt Too Long  
   Reproducible on Windows; may cause crashes or memory issues. 42 comments, 34 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/23377)

5. **#56913** — [Enhancement] Make autonomous Claude Code viable: tiered Opus brains + Sonnet workers + persistent state  
   Bold vision for long-running agent orchestrator. 26 comments, 0 👍 (but high discussion activity).  
   [Issue](https://github.com/anthropics/claude-code/issues/56913)

6. **#22685** — Claude Desktop App stuck in login loop with ‘Invalid authorization’ error  
   Affects macOS; magic-link login fails repeatedly. 26 comments, 21 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/22685)

7. **#29223** — [BUG] Plan upgraded but limit is not reset in sessions  
   Billing/reset logic bug; after upgrading a plan, usage limits are not refreshed for existing sessions. 20 comments, 27 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/29223)

8. **#28571** — Remote control session fails to resync after connection drop  
   iOS ↔ local Claude Code; messages silently fail after network interruption. 17 comments, 50 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/28571)

9. **#63358** — Opus 4.8 returns empty thinking blocks — no thinking shown in chat (same regression as Opus 4.7 #49268)  
   Fresh regression on Opus 4.8; thinking blocks have empty `thinking` field. 10 comments, 10 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/63358)

10. **#28986** — [FEATURE] Show active model and thinking mode indicators in the VS Code extension panel  
    Popular UX request (37 👍) for more transparency on the active model/settings.  
    [Issue](https://github.com/anthropics/claude-code/issues/28986)

## Key PR Progress (5 merged/updated in last 24h)

1. **#65919** — docs(agent-development): document ${CLAUDE_PLUGIN_ROOT} limitation in subagents  
   Informs about unresolved path variable issue (≤ 2.1.166); adds Known Limitations to SKILL.md.  
   [PR](https://github.com/anthropics/claude-code/pull/65919)

2. **#65916** — docs(mcp-integration): clarify allowed-tools vs agent tools: enforcement  
   Differentiates auto-approval (`allowed-tools`) from hard capability boundary (`tools:` in subagent frontmatter).  
   [PR](https://github.com/anthropics/claude-code/pull/65916)

3. **#65666** — Fix dev container issues (CLOSED)  
   Fixes DNS/firewall domains and adds mechanism to inject API key into dev container.  
   [PR](https://github.com/anthropics/claude-code/pull/65666)

4. **#65875** — fix: Forward ANTHROPIC_BASE_URL to agentic_review child process  
   Critical for users behind proxies/gateways (LiteLLM, Bifrost); prevents OAuth failure in advisor child process.  
   [PR](https://github.com/anthropics/claude-code/pull/65875)

5. **#61584** — Use workload identity federation for Claude auth in CI workflows (CLOSED)  
   Switches to OIDC token exchange instead of static API key; improves security.  
   [PR](https://github.com/anthropics/claude-code/pull/61584)

## Feature Request Trends

The community is pushing for:

- **Autonomous, long-running agents** — #56913 (tiered models + persistent state) and #48465 (MCP servers as memory backends) seek to make Claude Code a 24/7 orchestrator rather than a session-based assistant.
- **Third-party provider parity** — #46416 (context window detection fallback) and #65966 (re-raise of multiple stale-closed provider issues) show demand for full Anthropic API compatibility with proxies/LiteLLM.
- **Deeper VS Code integration** — #28986 (model/thinking indicators), #65857 (customizable message styling), and #45625 (LSP cross-project references) reflect a desire for tighter IDE cohesion.
- **UI/UX polish** — #31413 (UI localization to support non-English users) and the thinking-summary rendering bugs indicate that surface-level presentation is a growing priority.
- **Agent / subagent improvements** — Issues like #65768 (unresolved `CLAUDE_PLUGIN_ROOT`) and PR #65919 highlight the complexity of building with subagents.

## Developer Pain Points

- **Extended thinking breakage** — Opus 4.7 and 4.8 both exhibit missing/empty thinking summaries (#49268, #49322, #63358). High engagement and multiple duplicates suggest this is the most frustrating issue across recent versions.
- **Tool call parsing fragility** — #62123 reports frequent “could not be parsed” errors, and #65965 identifies a new variant where long-form text before a tool call corrupts it.
- **Session corruption from in-flight commands** — #63375 and #65938 detail how slash commands (`/usage`, `/goal`) injected mid-`advisor()` roundtrip produce malformed JSONL, permanently 400-ing the session.
- **Authentication and billing friction** — #22685 (login loop), #29223 (plan upgrade not resetting limits), and #65942 (capacity limitations) create roadblocks for paid users.
- **Windows / cross-platform inconsistencies** — #23377 (prompt too long on Windows), #59114 (LSP `uv_spawn` PATH issue), #62706 (mouse reporting in SSH terminals on WSL) underscore platform-specific rough edges.
- **High token usage and cost** — #42647 (redundant context resubmission loops) and #62016 (ripgrep `-rn` parsing bug silently corrupting output) waste tokens and annoy users.
- **Stale-closed issues** — #65966 re-raises five issues closed without triage, showing that the existing bug-tracking workflow is failing to keep up with community reports.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-07

## Today’s Highlights

A minor Rust alpha release landed today, while the community remains focused on two major themes: thread lifecycle management (real deletion, not just archiving) and better CLI ergonomics for isolated sessions. On the engineering side, OpenAI is actively refactoring global instruction loading into a modular contributor API, and fixing critical MCP OAuth credential reporting. Performance regressions—particularly on Windows and macOS with image-heavy workflows—continue to generate the most bug reports.

---

## Releases

- [rust-v0.138.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.6) — Minor alpha release for the Rust toolchain. No detailed changelog provided.

---

## Hot Issues

1. **[#13018 – Allow to delete threads in the Codex app](https://github.com/openai/codex/issues/13018)** — *CLOSED, 103 👍, 23 comments*  
   The most upvoted issue this period. Users are frustrated by having to manually delete archived session files from `~/.codex/archived_sessions/`. Closed, likely shipped.

2. **[#12862 – CLI: add --worktree and --tmux flags](https://github.com/openai/codex/issues/12862)** — *OPEN, 71 👍, 16 comments*  
   A highly-requested developer workflow improvement. Many users already script this manually — first-class support would eliminate fragile shell wrappers.

3. **[#23979 – Conversation history missing after update](https://github.com/openai/codex/issues/23979)** — *OPEN, 4 👍, 16 comments*  
   Data-loss bug: local project threads vanished from the UI post-update, even though data still exists in `state_5.sqlite`. High severity for desktop users.

4. **[#17827 – Customizable status line for TUI](https://github.com/openai/codex/issues/17827)** — *OPEN, 59 👍, 15 comments*  
   Feature parity request with Claude Code. Users want configurable display of token usage, model, rate limits, and git branch in the terminal status bar.

5. **[#26600 – Quota decreases while not actively using Codex](https://github.com/openai/codex/issues/26600)** — *OPEN, 1 👍, 15 comments*  
   Alarming: usage quota drains in the background. Possible stuck tasks or auto-refresh loops. Needs urgent investigation.

6. **[#26234 – MCP namespace tools flattened for non-OpenAI providers](https://github.com/openai/codex/issues/26234)** — *OPEN, 22 👍, 14 comments*  
   Critical for local/OSS model users: Codex serializes MCP tools in a proprietary `"type": "namespace"` format that Ollama, LM Studio, and OpenRouter cannot parse, making tools entirely unusable.

7. **[#24510 – High CPU from unbounded active thread metadata](https://github.com/openai/codex/issues/24510)** — *OPEN, 0 👍, 13 comments*  
   Performance bug: large title/preview metadata in `state_5.sqlite` causes sustained high CPU/GPU. Affects users with many active threads.

8. **[#25500 – "No chats" shown for projects with older conversations](https://github.com/openai/codex/issues/25500)** — *OPEN, 0 👍, 10 comments*  
   UI bug on Windows: non-archived conversations invisible in the sidebar. Update likely broke index/query logic.

9. **[#25820 – CLI login blocked by phone verification rate limit](https://github.com/openai/codex/issues/25820)** — *OPEN, 1 👍, 10 comments*  
   Pro subscribers locked out of CLI authentication. Rate limiting on phone verification is catching legitimate users.

10. **[#21232 – Freezes on Windows with image-heavy projects](https://github.com/openai/codex/issues/21232)** — *OPEN, 14 👍, 9 comments*  
    Recurring Windows performance issue: app becomes Not Responding when opening projects with many generated images. Multiple duplicate reports.

---

## Key PR Progress

1. **[#26840 – Add typed cross-platform path URIs](https://github.com/openai/codex/pull/26840)** — *OPEN*  
   Foundational for remote environments: creates stable path identifiers that don't misinterpret foreign path syntax. Core infrastructure for multi-host workflows.

2. **[#26713 – Report unusable MCP OAuth credentials as logged out](https://github.com/openai/codex/pull/26713)** — *OPEN*  
   Fixes a UX footgun: expired tokens with no refresh path now show as "logged out" instead of misleading "authenticated." Directly addresses MCP auth confusion.

3. **[#26834 – Adopt global instructions contributors](https://github.com/openai/codex/pull/26834)** — *OPEN*  
   Completes migration of global instruction loading out of `Config` into the extension API. Enables fresh semantics for thread creation, resume, and forks.

4. **[#26839 – Block project config permission overrides](https://github.com/openai/codex/pull/26839)** — *OPEN*  
   Security fix: prevents project-level config from bypassing approval policies, sandbox mode, and work permissions. Covers Linux, macOS, Windows.

5. **[#25704 – Normalize Codex images for Responses strict mode](https://github.com/openai/codex/pull/25704)** — *OPEN*  
   Feature-flagged: converts local/data URLs into a prepared format before sending to `/responses`. Paves way for stricter image handling.

6. **[#26686 – Propagate MCP client UI capabilities](https://github.com/openai/codex/pull/26686)** — *OPEN*  
   Semantic MCP app UI capabilities are now preserved across thread start, resume, fork, and review. TUI advertises an explicit empty profile.

7. **[#26804 – Send Codex product SKU to plugin service](https://github.com/openai/codex/pull/26804)** — *CLOSED*  
   Bug fix: remote plugin requests were missing the `OAI-Product-Sku: codex` header, causing product-specific plugins to be filtered out.

8. **[#26719 – Enable standalone web search in code mode](https://github.com/openai/codex/pull/26719)** — *OPEN*  
   Consumes plaintext search output and exposes `web.run` to code-mode JavaScript. Integration tests cover both direct and code-mode paths.

9. **[#26287 – Refine Guardian prompt for indirect exfiltration](https://github.com/openai/codex/pull/26287)** — *OPEN*  
   Security hardening: reorganizes policy guidance around sensitive data, authorization, and egress. Preserves trusted-user approvals.

10. **[#26832 – Add CODEX_HOME instructions contributor](https://github.com/openai/codex/pull/26832)** — *OPEN*  
    Moves CODEX_HOME instruction discovery from core into a dedicated crate. Part of the larger global instruction lifecycle refactor.

---

## Feature Request Trends

- **Delete (not just archive) threads** — #13018's 103 👍 signals overwhelming demand for full thread lifecycle control.
- **First-class CLI isolation** — #12862's 71 👍 for `--worktree`/`--tmux` flags shows deep developer need for sandboxed sessions.
- **Customizable TUI status line** — #17827 (59 👍): Claude Code parity request for token/model/git info.
- **MCP/OAuth usability** — Multiple issues (#26234, #24103, #26710) request better MCP tool serialization for non-OpenAI providers and OAuth credential lifecycle improvements.
- **In-app prompt management** — #26467 proposes a Prompt Snippets panel for saving/inserting frequent prompts.
- **Working directory updates** — #26836 requests thread path updating after project folder renames.
- **Remote Control for general chats** — #22947 asks for exposing host's projectless chat surfaces in remote-control flows.

---

## Developer Pain Points

1. **UI freezes and performance regressions** — Windows users report app freezes with image-heavy projects (#21232, #19936) and transparent/invisible UI components after updates (#26310, #26790). macOS users see high CPU from thread metadata bloat (#24510) and runaway disk writes from long-running sessions (#26843).

2. **Data loss and UI state bugs** — Conversation history disappearing after updates (#23979) and projects showing "No chats" for existing threads (#25500) erode trust in local storage.

3. **Auth and quota friction** — CLI login blocked by phone verification rate limits (#25820), background quota drainage (#26600), and MCP OAuth credentials that report "authenticated" but are unusable (#26713) create frustrating authentication loops.

4. **MCP integration fragility** — Custom model providers (Ollama, LM Studio, OpenRouter) cannot call MCP tools due to namespace serialization (#26234). MCP auth resets when multiple server entries share the same URL (#26710).

5. **Windows-specific shell lock-in** — #16717 (configurable agent shell) remains the top Windows pain point: hardcoded PowerShell produces worse commands than bash.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-07

## Today’s Highlights
No new releases in the past 24 hours, but the community is actively refining core agent reliability and security. Notable progress includes a fix for subagent false‑success reporting after turn limits, a patch for shell command hangs, and multiple PRs addressing command injection, terminal rendering, and LLM prompt corruption. The memory subsystem continues to receive focused attention, with several issues tracking deterministic redaction and retry logic improvements.

## Releases
*None in the last 24h.*

---

## Hot Issues (10 notable)

1. **[#1689 – Run blocking/long running shell commands in background](https://github.com/google-gemini/gemini-cli/issues/1689)**  
   *23 comments | 20 👍 | Closed*  
   Agent fails to handle commands that block (e.g., GPG signing). User reports major workflow interruption when the CLI freezes. Community strongly supports background execution.

2. **[#20586 – `read_file` tool enforces `.gitignore` even when negated in `.geminiignore`](https://github.com/google-gemini/gemini-cli/issues/20586)**  
   *7 comments | 2 👍 | Closed*  
   The `read_file` tool incorrectly blocks access to files excluded from `.gitignore` via `.geminiignore`. Impacts developer productivity when using custom ignore rules.

3. **[#20445 – Bundle build missing native extensions](https://github.com/google-gemini/gemini-cli/issues/20445)**  
   *7 comments | 2 👍 | Closed*  
   `npm run bundle` omits `node-pty` and `keytar`, breaking packaging for downstream distributions. A recurring pain point for Linux packagers.

4. **[#24353 – Robust component level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *7 comments | P1 | Open*  
   Epic for building behavioral evaluation tests. Critical for measuring agent quality across different Gemini models.

5. **[#22745 – Assess impact of AST‑aware file reads, search, and mapping (EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *7 comments | 1 👍 | Open*  
   Investigating AST‑driven tools to reduce turns and token noise. High potential for smarter codebase navigation.

6. **[#27363 – `/usage` cache fails to update when quota is 100%](https://github.com/google-gemini/gemini-cli/issues/27363)**  
   *6 comments | Closed*  
   API omits `remainingAmount` at full quota, causing stale cached usage display. Simple but disruptive for users monitoring rate limits.

7. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *6 comments | P1 | Open*  
   `codebase_investigator` subagent falsely reports `"success"` after hitting max turns. Hides real failures and misleads users.

8. **[#21968 – Gemini does not use skills and sub‑agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments | P2 | Open*  
   Anecdotal reports that custom skills are rarely invoked autonomously. Users want the agent to leverage available tools more intelligently.

9. **[#26525 – Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *5 comments | P2 | Open*  
   Auto Memory sends transcripts to the model before redaction. Requests deterministic secret redaction and less aggressive logging.

10. **[#26522 – Stop Auto Memory from retrying low‑signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
    *5 comments | P2 | Open*  
    Low‑signal sessions remain unprocessed and are repeatedly surfaced. Causes wasted API calls and user frustration.

---

## Key PR Progress (10 important)

1. **[#27718 – fix(core): keep auto visible without preview access](https://github.com/google-gemini/gemini-cli/pull/27718)**  
   *Open | size/s*  
   Ensures the `auto` model alias stays visible when dynamic model config is enabled, even for users without preview access. Adds regression tests.

2. **[#27405 – fix(core): parse tools.callCommand before discovered tool execution](https://github.com/google-gemini/gemini-cli/pull/27405)**  
   *Closed | priority/p2 | size/m*  
   Prevents raw command string from being passed to sandbox; parses into program+argv beforehand. Fixes an execution order bug.

3. **[#27398 – fix(acp): accept string protocolVersion during initialize](https://github.com/google-gemini/gemini-cli/pull/27398)**  
   *Closed | priority/p2 | size/m*  
   Normalizes date‑style `protocolVersion` strings sent by older clients, improving backward compatibility.

4. **[#27395 – docs: clarify GEMINI_CLI_HOME settings path](https://github.com/google-gemini/gemini-cli/pull/27395)**  
   *Closed | priority/p3 | size/xs*  
   Documents that user settings stay under `.gemini/settings.json` even when `GEMINI_CLI_HOME` is set. Clarifies isolation semantics.

5. **[#27385 – Fix Node 20 Compatibility and Windows symlink Test Failures](https://github.com/google-gemini/gemini-cli/pull/27385)**  
   *Closed | size/s*  
   Resolves a production crash under Node 20 (deprecated `URL.parse`) and fixes flaky Windows symlink tests.

6. **[#27591 – fix(cli): fall back for oversized bug report URLs](https://github.com/google-gemini/gemini-cli/pull/27591)**  
   *Open | priority/p2 | size/m*  
   `/bug` command on Android/Termux can exceed intent limits; PR degrades gracefully for large reports.

7. **[#27580 – fix(at‑command): prevent stack overflow from regex backtracking on large inputs](https://github.com/google-gemini/gemini-cli/pull/27580)**  
   *Open | priority/p1 | size/m*  
   Replaces a complex regex with an iterative scanner to avoid catastrophic backtracking when pasting large content.

8. **[#27575 – fix(security): prevent command injection in findCommand via safe spawnSync](https://github.com/google-gemini/gemini-cli/pull/27575)**  
   *Open | priority/p2 | size/m*  
   Replaces `execSync` with `spawnSync` in two locations to eliminate shell metacharacter injection risk.

9. **[#23490 – Support global cross‑folder session resume](https://github.com/google-gemini/gemini-cli/pull/23490)**  
   *Closed | size/xl*  
   Enables `gemini --resume <session-id>` to work across different project directories, with improved interactive UX.

10. **[#27505 – Prevent extra spaces on width‑0 CJK continuation cells](https://github.com/google-gemini/gemini-cli/pull/27505)**  
    *Open | priority/p2 | size/s*  
    Fixes rendering bugs where spurious spaces appear between CJK characters, improving cross‑platform terminal display.

---

## Feature Request Trends
- **Agent Autonomy & Reliability**: Strong demand for smarter subagent recovery (no false successes), background shell execution, and better self‑awareness of available skills (issues #22323, #1689, #21968, #21432).
- **Code Understanding**: Interest in AST‑aware file reads, search, and codebase mapping to reduce token waste and improve navigation (epics #22745, #22746).
- **Memory System Overhaul**: Multiple requests for deterministic secret redaction, avoiding infinite retries, and surfacing invalid patches (issues #26525, #26522, #26523).
- **Evaluation Infrastructure**: Growing push for robust component‑level behavioral evaluations and stabilized internal project evals (#24353, #23166).
- **Browser Agent Resilience**: Users want automatic session takeover, lock recovery, and settings.json overrides to be respected (#22232, #22267).

---

## Developer Pain Points
- **False Self‑Diagnosis**: Subagents report success after hitting turn limits, hiding real failures (#22323).
- **Shell Execution Flakiness**: Blocking commands freeze the CLI, and shell history gets corrupted by backslash‑ending lines (#1689, #25166, #27555).
- **Ignored Configuration**: Browser agent and skills are not consistently respecting user‑set overrides or `.geminiignore` rules (#22267, #20586).
- **Build & Packaging**: `npm run bundle` missing native extensions forces downstream distributors to carry full `node_modules` (#20445).
- **Terminal & I/O Issues**: Vim `cc` breaks on multi‑line buffers, CJK rendering adds extra spaces, and external editor corruption occurs in terminalBuffer mode (#27554, #27505, #24935).
- **Security & Privacy**: Auto Memory sends transcripts to model before redaction, and command injection vulnerabilities persist (#26525, #27575).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-07

## Today’s Highlights
The community is facing a high‑severity CPU regression on WSL2 (Issue #3700) that freezes the TUI, while the long‑standing request for image pasting in prompts (Issue #1276) continues to attract attention. Several MCP‑related issues point to growing pains in the protocol integration, and a new affordability discussion (#3707) reflects user concerns about token‑based costs.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues
*[Picked 10 noteworthy items from 17 updates; ordered by community impact and severity.]*

1. **#1128 – Feature: `awaitingUserInput` hook type**  
   *👍 27 · Comments 4*  
   Users need a hook that fires when the CLI is waiting for input, enabling actions like auto‑triggering.  
   [Link](https://github.com/github/copilot-cli/issues/1128)

2. **#3700 – [High] WSL2 regression: 215% CPU while idle, TUI frozen**  
   *👍 2 · Comments 1*  
   Fresh sessions immediately lock the UI; a reboot of the CLI is required. Regression from #2208.  
   [Link](https://github.com/github/copilot-cli/issues/3700)

3. **#1276 – Paste images from system clipboard into prompts**  
   *👍 8 · Comments 11*  
   Screenshots of code, UI bugs, or logs cannot be pasted directly – a gap for visual debugging.  
   [Link](https://github.com/github/copilot-cli/issues/1276)

4. **#3701 – [Closed] MCP server spawning loop on Windows**  
   *Closed 2026‑06‑06*  
   IDE lock‑file watcher re‑initiated MCP servers infinitely, causing resource exhaustion. Fix released?  
   [Link](https://github.com/github/copilot-cli/issues/3701)

5. **#3028 – MCP permissions configuration**  
   *👍 4 · Comments 6*  
   Users want per‑tool trust settings for MCP servers, similar to VS Code’s `trustedFolders`.  
   [Link](https://github.com/github/copilot-cli/issues/3028)

6. **#3547 – Background sub‑agent hangs at total_turns=0 with model `gpt-5.5`**  
   *Comments 5*  
   Agent dispatches successfully but never progresses; no completions or errors.  
   [Link](https://github.com/github/copilot-cli/issues/3547)

7. **#3282 – Multiple BYOK model support**  
   *👍 3 · Comments 2*  
   Only one bring‑your‑own‑key model can be set via env var; switching in TUI requires restart.  
   [Link](https://github.com/github/copilot-cli/issues/3282)

8. **#3652 – WSL startup delays (40–80 s) from `listSessions`**  
   *Comments 2*  
   Copilot Chat in WSL (VS Code) becomes unusably slow due to session list query time.  
   [Link](https://github.com/github/copilot-cli/issues/3652)

9. **#3707 – Support lower‑cost / open‑weight models for affordability**  
   *New, no comments yet*  
   Token‑based pricing feels expensive; requests for cheaper alternatives to reduce barriers.  
   [Link](https://github.com/github/copilot-cli/issues/3707)

10. **#3705 – Copilot Free only offers Claude Haiku 4.5**  
    *New*  
    Sonnet and Opus models are locked behind paid plans; users ask for wider free tier access.  
    [Link](https://github.com/github/copilot-cli/issues/3705)

## Key PR Progress
No notable pull requests were merged or updated in the last 24 hours.

## Feature Request Trends
- **Rich media input** – Image pasting into prompts (#1276) is the most‑upvoted open request.
- **MCP maturity** – Permissions (#3028), OAuth session reuse (#3706), and header persistence (#3668) are all active demands.
- **Model flexibility** – Multi‑BYOK (#3282), open‑weight model support (#3707), and broader free‑tier model access (#3705) reflect a desire for cost control and choice.
- **Hook system enhancements** – The `awaitingUserInput` hook (#1128) would enable automation around user‑input states.
- **Agent behavior controls** – Escape cancellation (#3692), scope‑creep prevention (#3655), and sub‑agent reliability (#3547) are recurring themes.

## Developer Pain Points
- **High CPU / frozen TUI on WSL2** (#3700) – reproducible and severe, blocking everyday use.
- **Startup delays on WSL** (#3652) – session listing causing multi‑second hangs.
- **Model availability limitations** – paid‑only models and single‑BYOK restrictions frustrate power users.
- **MCP session management** – losing session IDs (#3668) and repeated OAuth flows (#3706) break remote MCP integrations.
- **Keyboard / input quirks** – Ctrl+Enter inserting newline instead of submitting (#1437), and RTL text displayed LTR (#3704) hinder non‑English workflows.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-07

**Data source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## Today’s Highlights

No new releases or issues were created or updated in the last 24 hours. The only activity comes from two long-standing pull requests that were updated today: **#1769** improves graceful degradation when MCP servers fail to connect, and **#2183** fixes a race condition where dropped image paths were not eagerly attached to prompts. These changes address two persistent stability and usability concerns in the CLI.

---

## Releases

*No new versions were published in the last 24 hours.*

---

## Hot Issues

*No issues were updated or created in the last 24 hours. The community is currently stable with no open bug reports or feature requests receiving attention today.*

---

## Key PR Progress

Two pull requests were updated on 2026-06-07. Neither has been merged yet.

### [#1769 – fix: graceful degradation when MCP server fails to connect](https://github.com/MoonshotAI/kimi-cli/pull/1769)
| Field | Value |
|-------|-------|
| **Author** | he-yufeng |
| **Created** | 2026-04-06 |
| **Last updated** | 2026-06-07 |
| **Status** | Open |
| **Description** | Catches `MCPRuntimeError` in `_agent_loop()` to prevent an unhandled exception when an MCP server fails to start (e.g., due to port conflicts between TUI and Web UI sessions). Previously, the error would crash the worker and leave the frontend stuck in “thinking” forever. This PR adds a graceful fallback so the agent continues without the failed server. |
| **Why it matters** | Addresses a critical reliability issue that hangs the entire session; essential for multi-session environments. |

### [#2183 – fix(shell): attach dropped image paths eagerly](https://github.com/MoonshotAI/kimi-cli/pull/2183)
| Field | Value |
|-------|-------|
| **Author** | he-yufeng |
| **Created** | 2026-05-07 |
| **Last updated** | 2026-06-07 |
| **Status** | Open |
| **Related Issue** | #2182 |
| **Description** | Prompt submission now scans literal user text for local image paths when the selected model supports image input. The image is read immediately and sent as an `ImageURLPart`, instead of relying on a short-lived path that `ReadMediaFile` might fail to resolve later. |
| **Why it matters** | Fixes a race condition where dropped images would silently disappear from the prompt, improving reliability of multimodal interactions. |

*No other pull requests were updated in the last 24 hours.*

---

## Feature Request Trends

*No new feature requests were filed or updated today. The community has not surfaced any new directional demands in the last 24 hours.*

---

## Developer Pain Points

While no new issues were opened, the two active PRs highlight recurring pain points in the current codebase:

- **MCP server instability (#1769):** Workers crashing silently when an MCP server fails to start is a frustrating experience, especially when multiple sessions (TUI + Web UI) compete for the same ports. The absence of graceful degradation leaves users with a hung terminal.
- **Image path race condition (#2183):** Dropping an image into the shell that is not immediately resolved causes the image to be silently discarded. This undermines the core value of multimodal support and forces workarounds like explicit file path typing.

Both issues have been open for several weeks, indicating they are non-trivial to fix but are now being actively addressed by the same author. The community has not yet voiced additional concerns in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-07

## Today’s Highlights

No new releases landed today, but the ecosystem saw intense engineering activity: **kitlangton** submitted a series of core refactors (provider turn runner, tool architecture V2 unification, retry logic) that signal a major push toward stability and extensibility. At the same time, two critical regressions — the **Windows terminal death** (exit kills shell) and a **Bedrock SSO breakage** in v1.16 — continued to draw community attention. The long-running **sandboxing request** (#2242) remains the most commented issue, underscoring a top community priority for agent security.

## Releases

*None in the last 24 hours.*

## Hot Issues (Top 10 by Relevance)

1. **#2242 – Sandbox agent terminal commands**  
   *53 comments, 51 👍*  
   User asks for a seatbelt mechanism to restrict agent file access outside the current directory, similar to `gemini-cli` / `codex-cli`. No equivalent exists in OpenCode yet.  
   [anomalyco/opencode Issue #2242](https://github.com/anomalyco/opencode/issues/2242)

2. **#4704 – `/undo` and `/timeline undo` don’t revert file edits**  
   *19 comments, 16 👍*  
   Undo command fails even in git-tracked projects. Attached logs show the action is logged but file content unchanged. A blocker for safe agent usage.  
   [anomalyco/opencode Issue #4704](https://github.com/anomalyco/opencode/issues/4704)

3. **#16270 – `/sessions` TUI only shows ~5 recent sessions**  
   *11 comments, 2 👍*  
   Session picker ignores hundreds of historical conversations. Root cause traced to a hardcoded 30-day time window in `sync.tsx`.  
   [anomalyco/opencode Issue #16270](https://github.com/anomalyco/opencode/issues/16270)

4. **#9281 – Unified usage tracking via `/usage`**  
   *10 comments, 26 👍*  
   Feature request to view plan limits for OpenAI, Copilot, and Claude inside the TUI. A `Usage.Service` already exists but not exposed to users.  
   [anomalyco/opencode Issue #9281](https://github.com/anomalyco/opencode/issues/9281)

5. **#27749 – `/exit` or `/quit` kills the parent terminal on Windows PowerShell**  
   *6 comments, 1 👍*  
   Instead of returning to the shell prompt, the whole terminal tab closes. Reported for both `bun run dev` and bundled binary on Windows 11.  
   [anomalyco/opencode Issue #27749](https://github.com/anomalyco/opencode/issues/27749)

6. **#31147 – Regression: Bedrock provider broken with SSO login in v1.16**  
   *5 comments, 0 👍*  
   Error `E is not a function (E is a Symbol)` — credential provider fails for AWS SSO. Breaks inference for all Bedrock users.  
   [anomalyco/opencode Issue #31147](https://github.com/anomalyco/opencode/issues/31147)

7. **#26846 – Segfault on NixOS+WSL**  
   *5 comments, 8 👍*  
   `opencode` crashes with segmentation fault on NixOS under WSL. Users cannot even run `--version`.  
   [anomalyco/opencode Issue #26846](https://github.com/anomalyco/opencode/issues/26846)

8. **#30858 – Bedrock provider hangs indefinitely in v1.16.0**  
   *4 comments, 0 👍* (CLOSED)  
   Complimentary to #31147; all model calls hang despite correct AWS CLI credentials. Likely related to the same v1.16 regression.  
   [anomalyco/opencode Issue #30858](https://github.com/anomalyco/opencode/issues/30858)

9. **#29272 – `/simplify` skill for automated code review**  
   *3 comments, 0 👍*  
   Request for a command that launches concurrent agents to simplify/review code, similar to Claude Code’s `/simplify`.  
   [anomalyco/opencode Issue #29272](https://github.com/anomalyco/opencode/issues/29272)

10. **#30906 – Desktop v1.16.0 freezes when computing diff of large files**  
    *2 comments, 1 👍*  
    Electron renderer becomes unresponsive on large file diffs. Regressed from v1.15.13.  
    [anomalyco/opencode Issue #30906](https://github.com/anomalyco/opencode/issues/30906)

## Key PR Progress (Top 10 by Impact)

1. **#31176 – Refactor core: isolate provider turn runner**  
   *kitlangton* – Extracts turn preparation, streaming, tool settlement, and overflow retry from the session activity runner. Keeps durable scheduling and step limits in `llm.ts`. Foundational for testability.  
   [anomalyco/opencode PR #31176](https://github.com/anomalyco/opencode/pull/31176)

2. **#31177 – Publish terminal session run failures**  
   *kitlangton* – Emits `session.next.run.failed` event after an advisory wake exhausts its bounded retry. Distinguishes step-limit exhaustion from other failures.  
   [anomalyco/opencode PR #31177](https://github.com/anomalyco/opencode/pull/31177)

3. **#31112 – Retry failed session wakes**  
   *kitlangton* – Applies one automatic retry on advisory wake failure, preferring newer work over stale retries, and hides first failure from `awaitIdle`.  
   [anomalyco/opencode PR #31112](https://github.com/anomalyco/opencode/pull/31112)

4. **#31171 – Harden unified tool runtime**  
   *kitlangton* – Durable failure of unsettled calls before propagating operational errors, atomic registration against interruption, and no double-counting of structured projections.  
   [anomalyco/opencode PR #31171](https://github.com/anomalyco/opencode/pull/31171)

5. **#31173 – V2 background task tool**  
   *kitlangton* – New `task` tool that creates one-off child sessions with validated subagent configuration. Supports foreground (await results) and background (fire-and-forget) modes.  
   [anomalyco/opencode PR #31173](https://github.com/anomalyco/opencode/pull/31173)

6. **#31052 – Fix compacted Anthropic tool histories user-led**  
   *codeg-dev* – Strips trailing assistant prefill for affected Claude models, normalizing message histories sent to Anthropic.  
   [anomalyco/opencode PR #31052](https://github.com/anomalyco/opencode/pull/31052)

7. **#31049 – Refactor server API to canonical names**  
   *thdxr* – Promotes experimental server API to stable route groups, with standardized service layers for authorization and session-location middleware.  
   [anomalyco/opencode PR #31049](https://github.com/anomalyco/opencode/pull/31049)

8. **#30091 – Fix settling pending tool calls on schema errors**  
   *codeg-dev* – Marks pending tool parts as error when the stream later emits a matching schema-validation error. Prevents orphaned tool calls.  
   [anomalyco/opencode PR #30091](https://github.com/anomalyco/opencode/pull/30091)

9. **#31168 – Unify V2 tool architecture**  
   *kitlangton* – Introduces a single `Tool<Input, Output>` carrier, replaces separate attachment/contribution shapes with `tools.register(...)`, and passes durable invocation identity.  
   [anomalyco/opencode PR #31168](https://github.com/anomalyco/opencode/pull/31168)

10. **#31165 – Isolate image normalization**  
    *kitlangton* – Extracts image processing from `ReadTool` into a Location-scoped `Image.Service`, loading the Photon adapter only when needed. Falls back gracefully on resizer failures.  
    [anomalyco/opencode PR #31165](https://github.com/anomalyco/opencode/pull/31165)

## Feature Request Trends

From the latest issues, five major directions have emerged:

1. **Security & Permission Controls** – Sandboxing agent commands (#2242), per-agent MCP tool filtering (#28662), and external symlink consent (#30788) dominate the discussion. Users want granular control over file system and tool access.

2. **Session & History Management** – Paginated message loading (#6548), TUI session picker showing full history (#16270), and reliable undo (#4704) reflect a need to handle long-lived sessions gracefully.

3. **Provider Reliability & Integration** – AWS Bedrock SSO regressions (#31147, #30858), Windows terminal exit behavior (#27749, #28673), and GBK encoding on Windows (#30055) indicate cross-platform provider stability is a sore point.

4. **UI/UX Improvements** – Desktop file tree visibility (#30545), send-button‑only mode (#16226), alphabetical provider sorting (#30902), and Chinese localization gaps (#30883 PR) show the community cares about polish and accessibility.

5. **Tooling Enhancements** – Dynamic/lazy loading of MCP schemas (#17482), a `/simplify` code review skill (#29272), background task tool (already implemented in #31173), and environment information plug-in API (#31158) point toward a richer, more composable agent system.

## Developer Pain Points

- **Windows terminal management**: `/exit`, `/quit`, and `Ctrl+C` consistently kill the parent shell (pwsh, cmd, psmux) instead of returning to prompt. Multiple reports (#27749, #28673, #30495) across different OpenCode versions.
- **Bedrock regression in v1.16**: Two separate but related issues — SSO credential failure (#31147) and indefinite hangs on all model calls (#30858) — make the Amazon Bedrock provider unusable for a large portion of users.
- **Segfaults on NixOS+WSL**: #26846 shows the CLI is completely non-functional on this platform, blocking adoption for NixOS developers in WSL.
- **Desktop UI freezes**: Large file diffs cause Electron renderer lockups (#30906), and the file tree setting has no effect (#30545).
- **Undo reliability**: `/undo` and timeline undo do not revert file edits (#4704), shaking confidence in agent‑driven changes.
- **JSON parsing and encoding bugs**: #31175 (parsing failure), #30055 (GBK encoding cause garbled Chinese) highlight edge cases in data handling.

*Digest generated from GitHub data on 2026-06-07. For the full list of issues and PRs, visit [anomalyco/opencode](https://github.com/anomalyco/opencode).*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-07

## Today's Highlights

The busiest day in weeks: **nine bugs were closed** (including a critical auto-compaction crash and a markdown rendering regression), while the **approval system for workspaces** (PR #5332) has been merged and a **Tab autocomplete submission fix** landed. On the issue tracker, a severe **shift+enter binding conflict** (Issue #5188) and a **3–5 minute latency with local models** (Issue #5464) have drawn significant community attention.

## Releases

_No new releases in the last 24 hours._

## Hot Issues

1. **[#5188 — `shift+enter` submits instead of creating a new line](https://github.com/earendil-works/pi/issues/5188)**  
   _open, 7 comments, 👍2_  
   Despite explicit key binding config, `shift+enter` triggers `submit`. `ctrl+j` works. Community suspects the event handler order is wrong. A long-standing pain point for TUI users.

2. **[#5291 — Sessions hang on "Working" with Anthropic subscription](https://github.com/earendil-works/pi/issues/5291)**  
   _closed, 4 comments, 👍1_  
   Users on Anthropic Enterprise experience intermittent stalls. Interrupt/resume is unreliable. Root cause likely rate-limit or timeout handling.

3. **[#5464 — Local models: 3–5 minute "Working" latency mid-session](https://github.com/earendil-works/pi/issues/5464)**  
   _closed, 1 comment, 👍0_  
   Basic messages take minutes when using Ollama models (e.g. `ministral3:8b`). Reported today; likely a regression in context projection or token counting.

4. **[#5463 — Auto-compaction after final turn throws error](https://github.com/earendil-works/pi/issues/5463)**  
   _closed, 1 comment, 👍0_  
   Agent crashes with `Cannot continue from message role: assistant` when compaction triggers after an assistant response. Fix merged quickly.

5. **[#5462 — Markdown code blocks render literal triple-backtick fences](https://github.com/earendil-works/pi/issues/5462)**  
   _closed, 1 comment, 👍0_  
   Fence lines appear verbatim in the TUI, making rendered Markdown indistinguishable from raw text. Simpler fix expected soon.

6. **[#5418 — Invalid `models.json` crashes without showing the file path](https://github.com/earendil-works/pi/issues/5418)**  
   _open, 2 comments, 👍0_  
   Raw `JSON.parse` stack trace on startup; no mention of which file is broken. Highly unhelpful for new users.

7. **[#5459 — Add UI & validation metadata for spirit prompt arguments](https://github.com/earendil-works/pi/issues/5459)**  
   _open, 1 comment, 👍0_  
   Proposed extension of `{{ ... }}` placeholders to declare field type, requiredness, and hidden flags. Would enable better forms in KiOS.

8. **[#5461 — Allow extensions to durably evict injected context mid-session](https://github.com/earendil-works/pi/issues/5461)**  
   _closed, 1 comment, 👍0_  
   Extensions need a way to remove previously injected context without breaking compaction or reload. Linked to #4216.

9. **[#5460 — `roll attest` can’t reach evidence files in dynamic `runDir`](https://github.com/earendil-works/pi/issues/5460)**  
   _closed, 1 comment, 👍0_  
   Externally prepared evidence (screenshots etc.) cannot be referenced by `ac-map.json` because `runDir` is timestamped at runtime. Needs path resolution change.

10. **[#5455 — Export `RpcExtensionUIRequest` / `RpcExtensionUIResponse` from public API](https://github.com/earendil-works/pi/issues/5455)**  
    _closed, 1 comment, 👍0_  
    These RPC types are the only part of the protocol not publicly exported, blocking third-party extension authors.

## Key PR Progress

1. **[#5458 — Merge pull request #1 from earendil-works/main](https://github.com/earendil-works/pi/pull/5458)**  
   _closed_ – Routine upstream merge.

2. **[#5332 — Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332)**  
   _closed_ – Adds `.pi.user` folder and interactive approval for new workspaces. Merged; major security/UX improvement.

3. **[#5440 — Codex/native subagents](https://github.com/earendil-works/pi/pull/5440)**  
   _closed_ – Experimental sub‑agent support using Codex.

4. **[#5441 — Codex/native subagents (duplicate)](https://github.com/earendil-works/pi/pull/5441)**  
   _closed_ – Likely a rebase of the same feature.

5. **[#5452 — Codex/readme install rewrite](https://github.com/earendil-works/pi/pull/5452)**  
   _closed_ – Updated installation documentation for Codex integration.

6. **[#5451 — Fix security issue in vitest](https://github.com/earendil-works/pi/pull/5451)**  
   _closed_ – Patched a vulnerability in the test runner dependency.

7. **[#5450 — Fix: Tab submits slash commands from autocomplete](https://github.com/earendil-works/pi/pull/5450)**  
   _closed_ – Tab now submits `/settings` and similar commands instead of leaving them in the input field.

## Feature Request Trends

- **Workspace reproducibility & team collaboration**  
  #2908 (CREAM/Nix‑like workspaces) and #5332 (approval system) signal a push toward deterministic, shareable agent configurations. Expect more declarative workspace models.

- **Extension API completeness**  
  Four issues this week (#5455, #5461, #5460, #4776) touch on gaps in the extension API: exporting types, durable context eviction, dynamic path support, and shell completion generators.

- **Configuration persistence**  
  #3254 (prevent model switches from overwriting defaults) and #5301 (opt‑in XDG paths) highlight demand for more predictable, user‑controlled settings.

- **TUI / KiOS polish**  
  #5459 (prompt argument metadata), #5457 (copy button), and #5454 (fix arrow‑key navigation) show a steady stream of UX enhancements for the terminal interface.

## Developer Pain Points

- **Input handling confusion** – `shift+enter` does not respect key bindings (#5188); arrow keys conflict with prompt navigation (#5454). High frustration for power users.
- **Unhelpful error messages** – Invalid `models.json` crashes with a raw stack trace instead of a human‑readable file path (#5418).
- **Unreliable session execution** – Sessions hang with Anthropic (Enterprise) and local models (#5291, #5464). The "Working" spinner becomes a black box.
- **Rendering regressions** – Markdown fences shown literally (#5462) and stale npm readmes on package pages (#5453) degrade the user experience.
- **Missing autocomplete workflow** – Tab not submitting slash commands until today’s fix (#5450) shows how small UX gaps can break common flows.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-07

## Today's Highlights
The daemon-mode feature batch (#4490) has been merged into `main`, bringing 46 commits across 386 files and delivering the core `qwen serve` infrastructure toward v0.16-alpha. Critical memory-pressure compaction (#4824) landed to fix severe OOM crashes when using `--resume`, while the nightly v0.17.1 release includes a fix for skipped thought parts in copy output. ACP/REST parity continues to advance with 29 new `_qwen/*` methods (#4827) and a WebSocket transport (#4773).

---

## Releases
**v0.17.1-nightly.20260607.cef26a86a**  
[Release notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260607.cef26a86a)  
- `chore(release): v0.17.1`  
- `fix(cli): skip thought parts in copy output` by @he-yufeng  

---

## Hot Issues (10 of 29 updated in last 24h)

1. **[#4815 – Severe OOM with `qwen --resume` and Escape key broken](https://github.com/QwenLM/qwen-code/issues/4815)**  
   `priority/P1, type/bug, category/performance` – 8 comments  
   **Why it matters:** Reproducible old-space exhaustion within minutes of restoring a session; Escape completely non-functional. Community reports crash logs showing GC failures. Fixed by PR #4824.

2. **[#4794 – Compact mode tool merge causes full-screen flash on every tool batch](https://github.com/QwenLM/qwen-code/issues/4794)**  
   `priority/P2, type/bug, category/ui` – 3 comments  
   **Why it matters:** `mergeCompactToolGroups` shrinks history arrays, causing Ink to re-render the full screen each batch. Highly disruptive for users who rely on compact mode.

3. **[#4675 – Vim INSERT mode Esc key leak, Enter not sending in NORMAL mode](https://github.com/QwenLM/qwen-code/issues/4675)**  
   `type/bug, category/ui` – 3 comments  
   **Why it matters:** Multiple keybinding regressions – Esc in INSERT mode triggers app-level handler instead of exiting insert; NORMAL mode Enter fails to send messages. Impacts all vim-mode users.

4. **[#4657 – v0.17.0 using Qwen Code + Ollama cannot complete tasks](https://github.com/QwenLM/qwen-code/issues/4657)**  
   `type/bug, category/performance` – 7 comments  
   **Why it matters:** Task creation (e.g., HTML Ebook) hangs or times out with local LLM via OpenAI-compatible endpoint. Community suspects timeout regression, still unresolved.

5. **[#4720 – qwen code cannot access SMB shared folders, adds spaces in absolute paths](https://github.com/QwenLM/qwen-code/issues/4720)**  
   `type/bug, category/tools, scope/windows` – 3 comments  
   **Why it matters:** Windows SMB paths are misparsed, inserting spaces into absolute paths. Breaks file operations on network shares.

6. **[#4700 – v0.17.0 infinite loop reading files; image understanding not triggered automatically](https://github.com/QwenLM/qwen-code/issues/4700)**  
   `type/bug, category/tools, scope/memory` – 3 comments  
   **Why it matters:** Agent gets stuck in a `readFile` loop for 10+ minutes without progressing; `@` image attachments require explicit prompting to be interpreted.

7. **[#4686 – Qwen3.7-max streaming repetitive garbage via DashScope](https://github.com/QwenLM/qwen-code/issues/4686)**  
   `type/bug, model/long-context, category/ui` – 2 comments  
   **Why it matters:** With thinking enabled, model intermittently enters infinite repetition loop. Affects high-reasoning-effort usage.

8. **[#4825 – Feature request: `qwen sessions list` subcommand with `--json`, `--tag`, and date filters](https://github.com/QwenLM/qwen-code/issues/4825)**  
   `priority/P2, type/feature-request, roadmap/session-management` – 3 comments  
   **Why it matters:** Users want script-friendly session enumeration from `~/.qwen/history/`. Straightforward CLI extension with community support.

9. **[#4782 – Tracking: ACP Streamable HTTP transport – implementation status & upgrade plan](https://github.com/QwenLM/qwen-code/issues/4782)**  
   `type/feature-request, daemon` – 2 comments  
   **Why it matters:** Qwen Serve now implements ACP at `/acp`, enabling zero-adapter connections from Zed, Goose, JetBrains. Key milestone for v0.16-alpha.

10. **[#4821 – Declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)**  
    `priority/P2, type/feature-request, roadmap/subagents-tools` – 3 comments  
    **Why it matters:** Users want Claude Code-like `.claude/agents/*.md` pattern. Would allow custom agents without TypeScript changes.

---

## Key PR Progress (10 of 33 updated in last 24h)

1. **[#4490 – Merge daemon-mode feature batch into main](https://github.com/QwenLM/qwen-code/pull/4490)**  
   **46 commits, 386 files (+115k / −12k LOC)**. Periodic integration of `daemon_mode_b_main` into `main`. Includes core daemon-mode feature set for v0.16-alpha.

2. **[#4824 – Fix(core): prevent OOM by compacting API history, UI history, and triggering under memory pressure](https://github.com/QwenLM/qwen-code/pull/4824)**  
   Three targeted fixes: enable microcompaction on Hook messages (goal-mode), inline history trimming, forced GC compaction when heap exceeds threshold. Closes #4815.

3. **[#4827 – Feat(serve): ACP/REST parity — 29 new `_qwen/*` methods + production hardening](https://github.com/QwenLM/qwen-code/pull/4827)**  
   +935 lines covering session extensions (recap, btw, shell, context_usage), file operations, diff preview, and more. Replaces #4736.

4. **[#4773 – Feat(serve): ACP WebSocket transport (RFD Streamable HTTP phase 2)](https://github.com/QwenLM/qwen-code/pull/4773)**  
   Extracts `TransportStream` interface, adds `WsStream` adapter. Depends on #4827. Still WIP with `connectionRegistry` widening pending.

5. **[#4816 – Feat(serve): add `/settings` slash command for web-shell](https://github.com/QwenLM/qwen-code/pull/4816)**  
   Full-stack: daemon API routes, SDK client, React hooks (`useSettings`), event wiring, keyboard-navigable UI.

6. **[#4822 – Feat(serve): add hooks diagnostic HTTP/ACP surface (issue #4514 T3.9)](https://github.com/QwenLM/qwen-code/pull/4822)**  
   Two read-only endpoints for workspace and session hooks, enabling remote clients to query hook configuration.

7. **[#4764 – Feat(memory): add user-level auto-memory at `~/.qwen/memories/`](https://github.com/QwenLM/qwen-code/pull/4764)**  
   Cross-project user preferences/working style storage, mirroring Claude Code's private/team scope. Reuses existing 4-type taxonomy.

8. **[#4713 – Feat(mcp): project `.mcp.json` + workspace approval gating with aligned scope precedence](https://github.com/QwenLM/qwen-code/pull/4713)**  
   Adds approval gating for untrusted checked-in MCP sources. Aligns with Claude Code's `.mcp.json` handling. Refs #4615.

9. **[#4665 – Add InstructionsLoaded hook for instruction file loading](https://github.com/QwenLM/qwen-code/pull/4665)**  
   Fires event when instruction/context files are loaded during memory discovery and `@` imports. Payload includes file path, source type, load reason.

10. **[#4596 – Fix(core): recurse into submodule files when crawling git repos](https://github.com/QwenLM/qwen-code/pull/4596)**  
    Fixes #4568 – `git ls-files` now uses `--recurse-submodules` so submodule contents are crawled correctly.

---

## Feature Request Trends
- **Daemon & ACP Parity**: Multiple issues request richer daemon HTTP/ACP surfaces – hooks diagnostics (#4782), rewind endpoints (#4514), WebSocket transport (#4773), and full REST parity (#4827). This is the dominant theme for v0.16-alpha.
- **Session Management Enhancements**: Users want `qwen sessions list` with JSON output, tags, and date filters (#4825); also better session interruption recovery.
- **Declarative Agent Definitions**: Pattern from Claude Code – YAML frontmatter in `.claude/agents/*.md` – requested as a native feature (#4821).
- **Smart Model Routing**: Local model for simple tasks, API for complex ones (#4640). Also simplification of `modelProviders` to share `baseUrl` (#4813).
- **UI/UX Improvements**: Custom provider model addition should be easier in the first-run wizard (#4814); compact mode flashing and scrolling fixes.
- **Memory & Hooks**: User-level auto-memory (#4764), InstructionsLoaded hook (#4665), and telemetry hardening (#3731) indicate growing interest in extensibility.

---

## Developer Pain Points
- **OOM Crashes**: Severe out-of-memory with `--resume` and long-running sessions is the top pain point. PR #4824 addresses it, but community reported 10+ minute crashes.
- **UI Flashing & Freezing**: Compact mode full-screen flash on every tool batch (#4794), UI hangs during bulk file edits (#4442), and constant choppiness with long conversations.
- **Escape Key Malfunctions**: Multiple reports of Esc not working as expected – either triggers app-level clear instead of mode switch (#4675) or becomes completely non-functional (#4815).
- **Model Interruption & Context Loss**: TUI mode models interrupt mid-response and lose context on resume (#4740). Qwen3.7-max enters infinite repetition loops (#4686).
- **Windows & SMB Issues**: Inability to access SMB shared folders, spaces inserted in absolute paths (#4720). Also flash issues specific to Windows (#4561).
- **Infinite Loops / Stuck Tasks**: Agents repeatedly read files without progressing (#4700), or get stuck on a single task description (#4506). Users forcibly Ctrl+C after 13+ minutes.
- **CLI Surprise Exits**: Ctrl+C in PyCharm terminal causes immediate exit instead of double-press (#4586); sleep interception blocks legitimate retry backoff (#4707).
- **Offline / LAN Initialization**: Hangs on startup if no internet access, with no skip option (#4550).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-07

## Today's Highlights

The v0.9.0 release process is in full swing: maintainer Hmbown is systematically closing acceptance gates with documented smoke tests and rollback instructions, while a major command-dispatch refactor (#2791, #2870) is moving forward in staged layers. Multiple keyboard-layout bugs (French AZERTY, AltGr) were fixed, and the multi-tab system core has been merged into the codebase.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues
*(Top 10 by comment count & relevance)*

1. **[#2729 – v0.9.0 Release acceptance matrix](https://github.com/Hmbown/CodeWhale/issues/2729)** (15 comments)  
   The roadmap for the v0.9.0 release — defines core stability, provider routing, UI, Model Lab, WhaleFlow, docs, packaging, and rollback checks. Community is actively discussing what must be verified before tagging.

2. **[#2580 – FR: Adapt CodeWhale to VSCode Agent View](https://github.com/Hmbown/CodeWhale/issues/2580)** (9 comments)  
   A popular feature request asking for native VS Code integration using the new Agent View API. The request is in Chinese, indicating strong interest from Chinese-speaking developers.

3. **[#2791 – Refactor command dispatch to strategy pattern](https://github.com/Hmbown/CodeWhale/issues/2791)** (6 comments)  
   A structural improvement that breaks monolithic command handling into focused modules. The epic tracking (#2870) was opened today, signalling this is a priority cleanup for v0.9.

4. **[#2722 – v0.9.0 Open PR harvest](https://github.com/Hmbown/CodeWhale/issues/2722)** (6 comments)  
   A housekeeping issue to review long-lived PRs and either merge, supersede, or close them before the release. This helps avoid reimplementing features that already exist in pending branches.

5. **[#2870 – EPIC: staged command-boundary refactor for #2791](https://github.com/Hmbown/CodeWhale/issues/2870)** (2 comments, opened today)  
   Organizes the command refactor into smaller mergeable layers. The first layer (#2871) was already submitted and closed today.

6. **[#2666 – Telemetry: agents need visible token/resource usage](https://github.com/Hmbown/CodeWhale/issues/2666)** (2 comments)  
   During long-running tasks, agents lack visibility into token budget, context pressure, and cost. This is a core UX gap for multi-agent workflows.

7. **[#2847 – Abnormal stop working / stream read error](https://github.com/Hmbown/CodeWhale/issues/2847)** (2 comments)  
   A user reports `Error: Warn Stream read error: error decoding response body` during coding sessions. Could be a provider or network issue; community is waiting for reproduction steps.

8. **[#2787 – TUI status bar displays MCP count error](https://github.com/Hmbown/CodeWhale/issues/2787)** (2 comments)  
   A bug on `v0.9.0-stewardship` where the status bar shows incorrect MCP server counts when both global and local configs are present.

9. **[#2872 – CI process hangs at verify step (Smoke Tests)](https://github.com/Hmbown/CodeWhale/issues/2872)** (1 comment, opened today)  
   A new user reports CI hanging during curl health checks against localhost. Likely a resource timeout issue in automated testing environments.

10. **[#2863 – French AZERTY @ key conflicts with Alt-@ sidebar shortcut](https://github.com/Hmbown/CodeWhale/issues/2863)** (1 comment)  
    Reported today and already closed — the TUI composer interprets `AltGr+0` (which produces `@` on AZERTY) as the sidebar shortcut. A fix was merged in PR #2867.

## Key PR Progress
*(Top 10 by merge activity and feature impact)*

1. **[#2762 – v0.9.0 stewardship integration (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2762)**  
   The main integration branch for all v0.9.0 work — harvests PRs from contributors, stabilizes, and prepares for release. No tag or publish requested yet.

2. **[#2871 – Layer 1: clean command support boundaries (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2871)**  
   First layer of the command refactor: removed public helpers that weren’t used outside a single module, cleaned up `clap` subcommand alignment. Merged today.

3. **[#2869 – fix(tui): list saved models from all providers in /model picker (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2869)**  
   🐛 **Bug fix**: The model picker previously only showed the active provider’s models; now custom models saved under different providers are visible.

4. **[#2868 – feat(vscode): show thread git metadata (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2868)**  
   Adds Git branch and dirty status to the VS Code Agent View thread rows — a direct response to the #2580 request.

5. **[#2864 – feat(tui): add multi-tab system core (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2864)**  
   Merged the narrow tab-core and persistence slice (sister to #2753). Adds the `tab` module under `crates/tui/src/tui/` without affecting the host yet.

6. **[#2866 – feat(tui): add hotbar action registry foundation (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2866)**  
   Introduced the hotbar action trait and registry, registering built-in app actions for the future hotbar UI (#2063).

7. **[#2867 – fix(tui): prevent AltGr from swallowing @/#/$/!/% characters (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/2867)**  
   Solves the keyboard conflict for European layouts where AltGr is delivered as Ctrl+Alt. Now sidebar shortcuts only trigger via plain Alt.

8. **[#2865 – Modernize toward latest Claude Code (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2865)**  
   A large PR that closes the gap between DeepSeek TUI and Claude Code’s latest behavior, hooks, skills, agents, and UI. Still open for review.

9. **[#2808 – feat(runtime-api): session save, undo/retry, snapshot endpoints for GUI (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2808)**  
   Adds new runtime API endpoints (`/v1/sessions`, undo/retry, snapshot) to enable GUI capabilities that previously only existed in the TUI.

10. **[#2851 – Refactor TUI command groups into focused implementations (OPEN)](https://github.com/Hmbown/CodeWhale/pull/2851)**  
    The proof-of-concept PR for the command-strategy refactor. Restructures code without removing features, putting command behavior next to its owning group.

## Feature Request Trends

- **IDE / GUI integration** (esp. VS Code Agent View) remains the most-requested direction. Issues #2580, #1584, and PRs #2868, #2808 show high community interest.
- **WhaleFlow** (workflow engine) dominates the v0.9.0 milestone — typed IR, Starlark authoring, replay, teacher/harness loops, and external memory are all being actively designed.
- **Multi-tab and hotbar UI** improvements are gaining traction: #2864 and #2866 lay the foundation for tabbed sessions and a customizable hotbar.
- **Model Lab / Hugging Face** integration is becoming a priority: #2727 outlines an ordered MVP including provider polish, search, and passports.
- **Remote workbench** (AWS Lightsail + Telegram bridge) is a niche but concrete request for always-on VM control (#2724).

## Developer Pain Points

1. **Keyboard layout conflicts** — Multiple reports of AltGr/Alt conflicts with TUI shortcuts on European keyboards (French AZERTY, German QWERTZ). Fixed in #2867 but indicates a systemic issue with modifier key handling.
2. **CI reliability** — The CI smoke test hangs (issue #2872) and “Warn Stream read error” (issue #2847) point to flaky network or provider timeout handling.
3. **MCP configuration confusion** — The status bar display error (#2787) suggests the tool’s understanding of MCP server counts from multiple config files is not robust.
4. **Command dispatch complexity** — The ongoing refactor (#2791, #2870) is a direct response to maintainers and contributors finding the command codebase hard to extend without breaking things.
5. **Lack of resource visibility for agents** — Issue #2666 highlights that during long multi-agent tasks, developers and agents themselves have no insight into token consumption, context pressure, or cost. This is a blocker for production usage of the agentic features.

---

*Digest generated from GitHub data for 2026-06-07. Project repository: [Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale) (also known as DeepSeek TUI).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*