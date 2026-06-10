# AI CLI Tools Community Digest 2026-06-10

> Generated: 2026-06-10 02:43 UTC | Tools covered: 9

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
**Analysis Date:** 2026-06-10

## 1. Ecosystem Overview

The AI CLI tools landscape today reflects a maturing but still turbulent ecosystem where rapid feature expansion is colliding with reliability concerns. While all major tools released updates this week—Claude Code with its Fable 5 model, OpenAI Codex with standalone web search, Qwen Code with parallel agent teams—each faces distinct stability challenges: data persistence issues plague Claude Code and OpenAI Codex, Windows compatibility remains inconsistent across nearly every tool, and safety/security regressions surface regularly as model capabilities outpace guardrail maturity. The community is signaling clear priorities: cross-platform parity, session reliability, and developer-controlled agent behavior. Despite the noise, the overall direction is positive, with each tool carving distinct niches in the developer workflow automation space.

---

## 2. Activity Comparison

| Tool | Hot Issues (Past 24h) | Open PRs (Updated) | Releases Today | Notable |
|------|----------------------|--------------------|----------------|---------|
| **Claude Code** | 10 (incl. 4 new today) | 9 (all updated) | v2.1.170 (Fable 5) | Highest community upvotes (406👍 for Linux desktop) |
| **OpenAI Codex** | 10 | 10 | rust-v0.139.0 | Most recurring bugs (chat history, Windows sandbox) |
| **Gemini CLI** | 10 | 10 | v0.46.0, v0.47.0-preview.0 | Steady patch releases, low community engagement |
| **GitHub Copilot CLI** | 10 (30 updated) | 1 | v1.0.61 | Low PR activity, high issue turnover |
| **Kimi Code CLI** | 2 | 1 | None | Lowest activity across all tools |
| **OpenCode** | 10 | 10 | None | High PR volume, no new release |
| **Pi (pi-mono)** | 10 | 10 | v0.79.1 | Balanced feature and fix PRs |
| **Qwen Code** | 10 | 10 | v0.18.0-preview.0/.1 | Largest code churn (115k LOC in daemon merge) |
| **DeepSeek TUI (CodeWhale)** | 10 | 10 | v0.8.55 | Strong i18n community contributions |

**Activity Leaders:** Claude Code, OpenAI Codex, and Qwen Code show the highest community engagement and development throughput.

**Activity Laggards:** Kimi Code CLI has minimal community traction (2 issues, 1 PR updated). GitHub Copilot CLI has only 1 substantive PR despite high issue volume.

---

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities:

| Requirement | Tools Expressing Need | Specific Signals |
|-------------|----------------------|------------------|
| **Linux Desktop Support** | Claude Code (#65697, 406👍), Qwen Code, Pi | Dominant demand; users want native `.deb`/`.rpm` builds, not just CLI |
| **Windows Stability** | ALL except Kimi Code | Recurring: file locks (Claude #42776), sandbox crashes (Codex #24391), shell hangs (Gemini #25166), font blur (Pi), clipboard broken (Copilot #2082, OpenCode #13984) |
| **Chat History Persistence** | OpenAI Codex (5+ issues), Claude Code (#66734), Qwen Code (#4514) | UI fails to list existing sessions; data loss in JSONL truncation |
| **Subagent/Model Coordination** | Claude Code (#66773), OpenAI Codex (#27127), Gemini (#22323), Qwen Code (#4844, #4876) | Subagents misreporting success, ignoring instructions, incorrect model routing |
| **MCP/Plugin Integration** | Copilot CLI (#3436, #3701), OpenCode (#31595), Qwen Code (#4615), Claude Code (#66750) | Registry URL errors, runaway server spawning, approval workflow gaps |
| **Sandboxing & Security** | OpenCode (#2242, 53👍), Gemini (#22672), Claude Code (#66773), Qwen (#4615) | Agent isolation, destructive operation guardrails, substring trigger vulnerabilities |
| **Copy/Paste & TUI Usability** | Claude Code (#62699), Copilot (#2082), OpenCode (#13984), Pi (#4180), Qwen Code (#4888) | Clipboard broken on Linux; text copy failing across platforms |
| **Context/Memory Expansion** | DeepSeek TUI (#2935), Claude Code (#66762), Gemini (#27391) | Cross-session memory, compaction transparency, infinite context proposals |
| **Model Provider Flexibility** | OpenCode (#5674), Pi (#5363), DeepSeek TUI (#2925), Qwen Code (#4904) | Ability to use non-default models, custom endpoints, API key rotation |
| **Usage Visibility** | Claude Code (#66762), OpenAI Codex (#19585), OpenCode (#27698), Qwen Code (#4252) | Real-time token/cost metrics, rate-limit awareness, breakdown per turn |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Qwen Code | DeepSeek TUI |
|-----------|-------------|-------------|------------|--------------------|-----------|--------------|
| **Core Differentiator** | Frontier model quality (Fable 5) | VS Code / enterprise ecosystem | Google Cloud / Vertex AI integration | GitHub ecosystem lock-in | Daemon-mode & ACP protocol | CN developer focus & remote workbench |
| **Target User** | Power users seeking best model | Enterprise, Pro subscribers | GCP customers, researchers | GitHub-centric teams | Chinese & open-source developers | Chinese developers, remote workers |
| **Model Strategy** | Anthropic-only (Opus, Fable) | OpenAI + limited BYOK | Gemini-native + Vertex | Multi-model (Copilot catalog) | Qwen-native + OpenAI compat | Multi-provider (7+ backends) |
| **Key Release Today** | Fable 5 (new model class) | Web search from code mode | PTY resize crash fix | Agents picker, /settings dialog | Agent Team (parallel sub-agents) | Together AI provider, Model Catalog |
| **Technical Approach** | Plugin ecosystem (marketplace) | Session/thread persistence | Session resumption, skills | MCP/plugin hooks | ACP protocol, daemon-first architecture | i18n-first, Telegram bridge |
| **Pain Point Peak** | Data loss (#66734), Windows lock (#42776) | Chat history disappear (#20741), usage drain (#19585) | Agent overruling user (#27417), "Thinking Bug" (#27766) | Backward compat (#53), clipboard (#2082) | Daemon parity gaps (#4514), model switching (#4904) | Agent self-action (#2942), update confusion (#2924) |

**Notable Strategic Differences:**

- **Claude Code** is betting on model excellence (Fable 5) to justify a closed ecosystem but struggles with platform reliability and safety false positives.
- **OpenAI Codex** focuses on session persistence and enterprise-grade UX but faces the most severe data-quality regressions this week.
- **Gemini CLI** emphasizes sub-agent orchestration but users report agents ignoring explicit instructions and context management gaps.
- **GitHub Copilot CLI** relies on GitHub ecosystem stickiness but has the weakest PR throughput relative to issue volume.
- **Qwen Code** is the most architecturally ambitious—parallel agent teams, daemon-mode, ACP protocol—with the largest single PR (115k LOC).
- **DeepSeek TUI (CodeWhale)** uniquely targets Chinese developers with remote workbench (Telegram bridge) and extensive i18n, but rebrand confusion is hampering adoption.

---

## 5. Community Momentum & Maturity

| Tool | Community Size Signal | Iteration Velocity | Maturity Indicators |
|------|----------------------|-------------------|---------------------|
| **Claude Code** | Very High (406👍 top issue, 86 comments on Windows bug) | High (v2.1.170 today, 9 PRs) | Mature: plugin marketplace, safety systems, but regressions emerging |
| **OpenAI Codex** | High (125👍 for multi-root, 44 comments on sandbox) | Medium (10 PRs, 1 release) | Mature with legacy debt: recurring chat history bugs suggest architectural issues |
| **Gemini CLI** | Medium (12 comments max) | Medium (10 PRs, 4 releases today) | Maturing: Vertex AI focus, but "Thinking Bug" signals performance regression |
| **GitHub Copilot CLI** | High (75👍 for backward compat, 54👍 for model listing) | Low (1 PR only) | Mature but stagnant: low PR velocity relative to issue volume; community building workarounds |
| **Kimi Code CLI** | Very Low (2 issues, 1 PR) | Low (no release) | Nascent: minimal adoption, persistent unresolved bugs (file loop since January) |
| **OpenCode** | High (91 comments on memory, 64👍 on sandboxing) | Very High (10 PRs, major refactors) | Maturing: Active memory management, provider flexibility, but prompt quality concerns |
| **Pi (pi-mono)** | Medium (24 comments on trust, 13 on EPIPE crash) | High (10 PRs, v0.79.1) | Mature: Structured RFC process, experimental feature guards, strong model support |
| **Qwen Code** | Medium-High (14 comments on daemon gaps) | Very High (10 PRs, biggest code churn) | Maturing rapidly: Daemon mode, Agent Teams, Workflow tool—architectural leaps |
| **DeepSeek TUI** | Medium (6 comments on self-action bug) | High (10 PRs, v0.8.55) | Maturing: Active i18n community, but rebrand confusion and Telegram bridge gaps |

**Velocity Leaders:** Qwen Code (largest code changes), Claude Code (highest community engagement), OpenCode (active refactoring).

**Maturity Gaps:** Kimi Code CLI is the clear outlier—lowest activity, unresolved critical bugs. GitHub Copilot CLI has high demand but insufficient engineering response.

---

## 6. Trend Signals

### For Technical Decision-Makers

1. **Fable 5 / Model Churn Creates Ecosystem Disruptions**
   Anthropic's new model class caused immediate compatibility breaks across tools: Pi had to patch `thinking:disabled` to avoid 400 errors, OpenCode saw validation errors from new response fields (#31579, #31560). Expect a 1-2 week stabilization window for any tool integrating Claude Fable 5. **Action:** Pin models during transitions; test fallback behaviors.

2. **Cross-Platform Parity is Not Optional**
   Windows and Linux users are receiving unequal attention. Every tool has at least one critical Windows-specific bug. Claude Code (#42776) and OpenAI Codex (#24391) have months-old Windows issues still unresolved. Linux usability gaps (clipboard, Wayland) are consistently lower priority. **Action:** Evaluate tool trial on your primary OS before adoption; demand Linux/Windows parity in vendor selection.

3. **Data Persistence is the #1 Trust Eroder**
   Chat history disappearing, session JSONL truncation, and invisible threads are the most damaging class of bugs—they erode foundational trust. OpenAI Codex has 5+ open issues on this, Claude Code has a new data-loss bug (#66734). **Action:** Implement local session backups; avoid relying solely on tool-managed history for long-running projects.

4. **Subagent Orchestration is Moving from Niche to Core**
   Qwen Code's Agent Teams (#4844), Gemini's sub-agent focus, and Claude Code's workflow triggers (#66773) all signal that multi-agent coordination is becoming a baseline expectation, not a premium feature. **Action:** Evaluate subagent reliability (false success reports are common—Gemini #22323, Qwen #4876) before building workflows against agent hierarchies.

5. **MCP Supply Chain is Immature**
   Across Copilot CLI (#3436, #3701), OpenCode (#31595), and Claude Code (#66750), MCP integration remains fragile—wrong URLs, runaway spawning, missing approval flows. The "app store" vision is real but the plumbing is still inconsistent. **Action:** Treat MCP plugins as experimental; test thoroughly in staging before production workflows.

6. **Non-Functional Requirements Are the Real Differentiator**
   Usage visibility (Claude #66762, Codex #19585, Qwen #4252), context compaction transparency, and rate-limit-aware scheduling are rising in importance as tools consume more tokens. Users are demanding to understand *why* their quotas are exhausted. **Action:** Prioritize tools with native cost/usage telemetry; demand per-turn token breakdown as a standard feature.

7. **Chinese Developer Ecosystem is Diverging**
   Qwen Code and DeepSeek TUI (CodeWhale) are building features (i18n-first UIs, Telegram bridges, Tencent cloud integration) that serve CN developers explicitly. These tools are architecturally distinct from Western counterparts. **Action:** For CN-market workflows, evaluate Qwen Code's daemon-mode and DeepSeek TUI's remote workbench as potential fits; for global teams, verify English/UTF-8 support quality.

### Bottom Line

The AI CLI tool market is converging on core feature needs (cross-platform, reliable persistence, subagent orchestration, usage transparency) while diverging in strategic bets (model exclusivity, cloud ecosystem lock-in, daemon vs. terminal-first architecture). No single tool dominates across all dimensions. For risk-averse teams, Claude Code and OpenAI Codex offer the most complete experiences but demand tolerance for platform-specific regressions. For teams prioritizing architectural flexibility, Qwen Code and OpenCode show the fastest iteration velocity. The Kimi Code CLI and GitHub Copilot CLI, despite different reasons, represent the highest risk of stagnation.

**Watch list for next week:** Whether Claude Code resolves the #66734 data loss regression, whether OpenAI Codex merges a fix for the chat history bugs (multiple PRs on resizing images/Paths point in this direction), and whether Qwen Code's Agent Team feature graduates from experimental to stable.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the **anthropics/skills** repository, based on activity as of **2026-06-10**.

---

### 1. Top Skills Ranking

The following 6 Pull Requests generated the most community discussion (by comment volume). All remain **Open**.

1.  **document-typography** ([PR #514](https://github.com/anthropics/skills/pull/514))
    - **Functionality:** Prevents orphan word wraps, widow paragraphs, and numbering misalignment in AI-generated documents. Focuses on print-level quality control.
    - **Discussion:** High engagement driven by the universal pain point of document formatting. The core value proposition—”issues that affect every document Claude generates”—resonated strongly.
    - **Status:** Open (since March 2026).

2.  **ODT Skill** ([PR #486](https://github.com/anthropics/skills/pull/486))
    - **Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Targets the LibreOffice and open-source document ecosystem.
    - **Discussion:** Interest from users who need to produce standardized, open-format documents. Represents a clear demand for escaping proprietary formats.
    - **Status:** Open (since March 2026).

3.  **AURELION Skill Suite** ([PR #444](https://github.com/anthropics/skills/pull/444))
    - **Functionality:** Four skills (kernel, advisor, agent, memory) forming a structured cognitive and memory framework for professional knowledge management.
    - **Discussion:** The most ambitious "meta-skill" submission. Discussion focused on the complexity of installing a 4-skill suite versus a single skill.
    - **Status:** Open (since February 2026).

4.  **feature-dev Workflow Fix** ([PR #363](https://github.com/anthropics/skills/pull/363))
    - **Functionality:** Fixes a `TodoWrite` overwrite bug causing Quality Review and Summary phases to be skipped during the `/feature-dev` workflow.
    - **Discussion:** Very high attention from developers using structured agentic workflows. This is a critical bug fix for any team using multi-phase software development with Claude Code.
    - **Status:** Open (since February 2026). Last updated June 2026—likely closing soon.

5.  **Skill-Quality & Security Analyzers** ([PR #83](https://github.com/anthropics/skills/pull/83))
    - **Functionality:** Meta-skills for evaluating other Skills across dimensions (Structure, Documentation, Security). A tool for the developer experience.
    - **Discussion:** Significant long-term interest. This is the oldest active PR in the top rankings, suggesting ongoing community desire for skill vetting/QA tooling.
    - **Status:** Open (since November 2025).

6.  **SAP-RPT-1-OSS Predictor** ([PR #181](https://github.com/anthropics/skills/pull/181))
    - **Functionality:** Integrates SAP’s open-source tabular foundation model for predictive analytics on business data.
    - **Discussion:** Enterprise-focused interest. Represents a niche but highly specialized domain where a targeted Skill provides immense value.
    - **Status:** Open (since December 2025).

---

### 2. Community Demand Trends

The top Issues reveal five clear, pressing demand directions:

1.  **Org-Wide Skill Management** ([Issue #228](https://github.com/anthropics/skills/issues/228)): The most-upvoted feature request (👍7). Users want a shared skill library or direct sharing links for teams, rather than manual file sharing.
2.  **Evaluation & Tooling Reliability** ([Issues #556](https://github.com/anthropics/skills/issues/556), #1169, #189): A systemic pain point: the `run_eval.py` tool is broken, scoring 0% recall reliably. The community is frustrated that the evaluation infrastructure itself is unreliable.
3.  **Security & Trust Boundaries** ([Issue #492](https://github.com/anthropics/skills/issues/492)): Growing awareness that community skills live under the `anthropic/` namespace, creating a trust boundary vulnerability. Demand for clear provenance/security grading.
4.  **Agent Governance** ([Issue #412](https://github.com/anthropics/skills/issues/412)): Proposal for safety patterns (policy enforcement, audit trails) for AI agent systems. Indicates the community is moving from single-tool skills to multi-agent orchestration.
5.  **MCP & Portability** ([Issue #16](https://github.com/anthropics/skills/issues/16), #1156): Desire to expose Skills as MCP servers and maintain portability labels so skills work across different projects without manual re-verification.

---

### 3. High-Potential Pending Skills

These **Open PRs** have active discussion and critical fixes, making them likely to merge soon:

- **[agent-creator Skill](https://github.com/anthropics/skills/pull/1140)** (PR #1140): Adds a meta-skill for task-specific agent sets. Addresses multi-tool evaluation and adds Windows support. Last updated June 2—actively maintained.
- **[Windows Compatibility Fixes](https://github.com/anthropics/skills/pull/1050)** (PR #1050): A 1-line fix for `subprocess.Popen` failing on Windows due to `PATHEXT` issues. Essential for non-MacOS users.
- **[testing-patterns Skill](https://github.com/anthropics/skills/pull/723)** (PR #723): Comprehensive testing guidance (Trophy model, React Testing Library, edge cases). Directly addresses a community need for test generation.
- **[n8n-builder / n8n-debugger](https://github.com/anthropics/skills/pull/190)** (PR #190): Four production-tested skills for building and debugging n8n workflows. High real-world utility for automation engineers.

---

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for robust, enterprise-grade reliability tooling (evaluation, security scanning, and Windows compatibility) to transform Skills from experimental features into a trusted, shareable platform.**

---

# Claude Code Community Digest — 2026-06-10

## Today’s Highlights
Anthropic rolled out **v2.1.170** featuring **Claude Fable 5**, a new Mythos-class model described as the most capable general‑use model to date. The community is highly engaged: the long‑standing Windows relaunch bug (#42776) reached 86 comments, while the Linux Desktop feature request (#65697) scored 406 👍, the highest on record. Several critical data‑loss and security‑related bugs emerged today, including session transcript truncation (#66734), a “fallback” content‑block API error that makes sessions unrecoverable (#66760), and a workflow‑trigger substring‑match vulnerability (#66773).

---

## Releases
- **v2.1.170** — Introduces **Claude Fable 5** (Mythos‑class model) and a session stability fix. [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.170)

---

## Hot Issues (Top 10 by Community Impact)

1. **[BUG] Claude Code Desktop fails to Relaunch on Windows due to orphaned process file lock**  
   [#42776](https://github.com/anthropics/claude-code/issues/42776) — 86 comments, 31 👍  
   Long‑standing Windows blocker. Orphaned process holds file lock, preventing relaunch. High frustration for Windows users.

2. **[FEATURE] Official Claude Desktop build for Linux (Ubuntu LTS / Debian)**  
   [#65697](https://github.com/anthropics/claude-code/issues/65697) — 31 comments, **406 👍**  
   By far the most upvoted request. Linux developers demand native desktop integration, not just CLI.

3. **[BUG] CVP‑approved user blocked on benign, non‑security queries**  
   [#61889](https://github.com/anthropics/claude-code/issues/61889) — 29 comments, 3 👍  
   Trust & safety friction: approved users hit false‑positive blocks on fresh sessions. Erodes confidence in safety systems.

4. **[FEATURE] Enable Remote Control for Claude Code sessions in Desktop**  
   [#29006](https://github.com/anthropics/claude-code/issues/29006) — 28 comments, 94 👍  
   Growing desire to manage headless/background sessions from the desktop app.

5. **[BUG] Text cannot be copied from output via `Ctrl+Shift+C` or right‑click on Linux**  
   [#62699](https://github.com/anthropics/claude-code/issues/62699) — 10 comments, 7 👍  
   Basic terminal usability broken on Linux TUI. Low complexity but high annoyance.

6. **[BUG] Cowork VM disk full on session start — ENOSPC blocks all Bash commands**  
   [#37581](https://github.com/anthropics/claude-code/issues/37581) — 6 comments, 5 👍  
   Critical for Cowork users: session starts in a completely unusable state.

7. **[BUG] Opus 4.8: forced balance‑slot criticism, critique‑for‑its‑own‑sake in CoT**  
   [#66273](https://github.com/anthropics/claude-code/issues/66273) — 5 comments  
   Behavioral pathology report detailing self‑favoring skepticism and context collapse.

8. **[BUG] API 400: harness emits content block with type “fallback” — session unrecoverable**  
   [#66760](https://github.com/anthropics/claude-code/issues/66760) — 4 comments  
   New today: a malformed API request freezes the session permanently. Affects core harness.

9. **[BUG] Session JSONL rewritten in‑place to metadata‑only stub — user data lost**  
   [#66734](https://github.com/anthropics/claude-code/issues/66734) — 2 comments, fresh today  
   **Data loss**: all user/assistant messages vanish. High severity; linked to recent installer migration.

10. **[BUG] `claude.yml` workflow triggers on substring match — fires on incidental `@claude*` strings**  
    [#66773](https://github.com/anthropics/claude-code/issues/66773) — 1 comment, today  
    Trigger condition `contains(…, '@claude')` fires on quoted text, causing workflow pollution and potential unintended actions.

---

## Key PR Progress (All 9 Open PRs Updated in Last 24h)

1. **fix(pr‑review‑toolkit): use full author name in plugin manifest**  
   [#66650](https://github.com/anthropics/claude-code/pull/66650) — Author name inconsistency fixed across bundled plugins.

2. **fix(#66592): False positive Usage Policy block on lattice gauge theory question (Fable 5, v2.1.170)**  
   [#66608](https://github.com/anthropics/claude-code/pull/66608) — Automated fix by REAPR tool addressing safety classifier false positive.

3. **fix(#66595): Fable 5 safety classifier auto‑switches to Opus mid‑session**  
   [#66607](https://github.com/anthropics/claude-code/pull/66607) — Another REAPR fix for safety classifier instability during authorized security testing.

4. **fix(marketplace): sync security‑guidance version and description with plugin.json**  
   [#66577](https://github.com/anthropics/claude-code/pull/66577) — Marketplace metadata drift corrected (version 1.0.0 → 2.0.0).

5. **fix(pr‑review‑toolkit): use full author name in plugin.json**  
   [#66575](https://github.com/anthropics/claude-code/pull/66575) — Companion fix to #66650 in the plugin’s own metadata.

6. **fix(ralph‑wiggum): restore dead error handlers broken by `set -euo pipefail`**  
   [#66573](https://github.com/anthropics/claude-code/pull/66573) — Silent exits before error handling in stop‑hook.sh; crucial for plugin reliability.

7. **[WIP] Repeated “Image couldn’t be processed” API errors consuming usage limit**  
   [#66572](https://github.com/anthropics/claude-code/pull/66572) — Work‑in‑progress addressing billing waste from image processing failures.

8. **Claude/subscription debate chat rx ewi**  
   [#65723](https://github.com/anthropics/claude-code/pull/65723) — PR title appears unintentional; unclear scope. Likely requires triage.

9. **fix(plugin‑dev): validator scripts abort on first finding due to `set -e`**  
   [#66416](https://github.com/anthropics/claude-code/pull/66416) — Three validator scripts stop early, hiding cascading plugin validation errors.

---

## Feature Request Trends

- **Linux Desktop Support** (#65697, 406 👍) — Dominates demand. Developers want a native `.deb`/`.rpm` build.
- **Remote Session Control** (#29006, 94 👍) — Second most‑voted. Need to attach/detach and manage sessions remotely.
- **Rate‑Limit‑Aware Deferred Scheduling** (#59634) — Users hit usage limits mid‑task and want graceful continuation.
- **Model Flexibility** (#66757) — Requests to use non‑Opus models (e.g., Mythos) inside Claude Code.
- **Hooks for Assistant Text Output** (#37243) — Currently only tool call hooks exist; devs need hooks for raw text generation.
- **Cost/Usage Visibility** (#66762) — “Ultracode mode” silently consumes entire usage windows via subagent fleets; users want granular cost breakdowns.
- **Re‑add `/history` Command** (#66754) — Removal broke session recovery after interruption.
- **Domain‑Specific Agentic Reasoning** (#66744) — Sports‑science users want better handling of technical document analysis.

---

## Developer Pain Points

- **Windows instability**: #42776 (file lock), #66772 (HCS VM failure), #66398 (cursor invisible in agents) — Windows remains the most bug‑ridden platform.
- **Data loss**: #66734 (session JSONL truncated), #66763 (PR monitor chips never retire) — Users losing work erodes trust.
- **Plugin marketplace friction**: #66750 (marketplace not pre‑registered for headless users) and #66577/#66650 (metadata drift) complicate plugin management.
- **Safety system misfires**: #61889 (benign queries blocked), #66641 (Fable 5 classifier auto‑switches to Opus), #66273 (hallucination of user messages) — Safety mechanisms cause false positives and model confusion.
- **Behavioral pathology**: #66273 and #64991 (Opus forced criticism, self‑favoring skepticism) — Advanced users reporting model misbehaviors that reduce output quality.
- **Workflow pollution**: #66773 (substring match triggers), #66745 (agents writing status reports instead of file content) — Workflow reliability is a concern.
- **Missing basic usability**: #62699 (no text copy on Linux), #65777 (inline LaTeX not rendering) — Small gaps that compound for daily drivers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-10

## Today’s Highlights
Multiple critical bugs around chat history disappearance and Windows sandbox failures continue to dominate community discussion, with no clear fix merged yet. A new `rust-v0.139.0` release enables standalone web search from code mode and preserves complex tool schemas (`oneOf`/`allOf`). Internal PRs focus on telemetry spans, image handling optimizations, and a systematic migration to `PathUri` for cross-platform file paths.

## Releases
- **[rust-v0.139.0](https://github.com/openai/codex/releases/tag/rust-v0.139.0)**: Code mode can now call standalone web search directly, including from nested JavaScript tool calls, returning plaintext results (#26719). Tool and connector input schemas now preserve `oneOf` and `allOf`; large schemas maintain more shallow structure when compacted.
- **alpha pre‑releases** (no notable changes beyond version bumps):
  - `rust-v0.140.0-alpha.2`
  - `rust-v0.139.0-alpha.3`
  - `rust-v0.139.0-alpha.2`

## Hot Issues (10 items)
1. **[#24391 – Windows sandbox: spawn setup refresh fails on CLI 0.133.0](https://github.com/openai/codex/issues/24391)**
   - 44 comments, 25 👍. PowerShell-based sandbox setup fails after update. Users are blocked on Windows; many have rolled back to 0.132.0.

2. **[#20741 – Desktop project chat histories disappeared after recent update](https://github.com/openai/codex/issues/20741)**
   - 33 comments, 14 👍. Persistent UI regression – threads still exist on disk but are hidden from the sidebar. Affects macOS and Windows.

3. **[#19585 – Pro weekly usage limit depletes unusually fast on 5.5](https://github.com/openai/codex/issues/19585)**
   - 29 comments, 26 👍. Token-efficiency regression causing Pro users to hit limits faster. Strong community frustration.

4. **[#21128 – Desktop silently hides project conversations outside global recent-50 window](https://github.com/openai/codex/issues/21128)**
   - 23 comments, 16 👍. UI truncation rather than true data loss, but makes the app unreliable for long‑term project memory.

5. **[#23979 – Conversations missing after update; threads still in state_5.sqlite](https://github.com/openai/codex/issues/23979)**
   - 20 comments, 4 👍. Similar root cause to #20741 but on a later update (26.519.22136).

6. **[#17540 – Windows app: older local threads disappear after restart](https://github.com/openai/codex/issues/17540)**
   - 19 comments, 6 👍. Reproducible on Windows; threads remain on disk but sidebar/search fail to index them.

7. **[#25500 – Projects sidebar shows “No chats” for older non-archived conversations](https://github.com/openai/codex/issues/25500)**
   - 17 comments, 2 👍. Yet another manifestation of the chat‑hiding bug.

8. **[#26493 – Context compaction fails with `invalid_enum_value` for `context_compaction`](https://github.com/openai/codex/issues/26493)**
   - 16 comments, 4 👍. Remote compaction attempts error out; workaround proposed in #27267.

9. **[#24287 – App accepts prompt but UI stays stuck in Thinking; Stop fails](https://github.com/openai/codex/issues/24287)**
   - 14 comments. Turn can become invisible after restart – a scary UX dead‑end.

10. **[#2909 – Support for multi-root workspaces (VS Code extension)](https://github.com/openai/codex/issues/2909)**
    - 9 comments, 125 👍. The most‑voted feature request. Many developers using VS Code multi‑root setups are unable to use Codex effectively.

## Key PR Progress (10 items)
1. **[#27107 – Add spans to `run_turn`](https://github.com/openai/codex/pull/27107)**
   - Improves app‑server tracing by adding `run_turn.*` spans for orchestration, sampling‑request preparation, and tool loading.

2. **[#27285 – Fix goal analytics thread source ownership](https://github.com/openai/codex/pull/27285)**
   - Fixes a Rust compilation error (`E0507`) caused by a non‑`Copy` `ThreadSource` being moved in goal analytics reducer.

3. **[#27247 – Resize all history images behind a feature flag](https://github.com/openai/codex/pull/27247)**
   - Core change to reduce token consumption by resizing images in conversation history (behind a flag).

4. **[#27266 – Preserve metadata when resizing prompt images](https://github.com/openai/codex/pull/27266)**
   - Companion to #27247 – ensures EXIF/metadata is not stripped during resize.

5. **[#27246 – Strip image detail from Responses Lite requests](https://github.com/openai/codex/pull/27246)**
   - Removes image‑detail fields from lightweight request paths, reducing payload size.

6. **[#27280 – Add `PathUri` native conversion APIs](https://github.com/openai/codex/pull/27280)**
   - Centralizes path conversion (`from_abs_path`, `to_abs_path`) to prepare for ExecutorFileSystem migration.

7. **[#27282 – Migrate ExecutorFileSystem to PathUri](https://github.com/openai/codex/pull/27282)**
   - Refactors the shared exec‑server file abstraction to use `PathUri`, keeping wire format unchanged for now.

8. **[#27261 – Make MCP connection startup fallible](https://github.com/openai/codex/pull/27261)**
   - Moves required‑MCP validation from `McpConnectionManager` internals into `Session::new`, improving error handling.

9. **[#27127 – Forward assistant output to realtime through handoffs](https://github.com/openai/codex/pull/27127)**
   - Ensures voice realtime sessions receive all user‑facing Codex messages, making the assistant feel coherent.

10. **[#27055 – Add parent turn ID to Codex turn analytics](https://github.com/openai/codex/pull/27055)**
    - Drops `parent_turn_id` into analytics events for multi‑agent spawns, CSV workers, and Guardian review, enabling better traceability.

## Feature Request Trends
- **Persistent project chat history** – The most urgent theme: users want sidebar/search to reliably show all conversations, not just the recent 50. Many issues (e.g., #21128, #25500) are effectively feature requests for a proper indexing system.
- **Multi‑root workspace support** (#2909, 125 👍) – High demand from VS Code users working with complex project structures.
- **Configurable Windows agent shell** (#16717, closed but still requested) – Ability to switch from PowerShell to Git Bash or other shells.
- **Better context compaction transparency** – Users want to understand when/why compaction fails and how tokens are consumed (#19585, #26493).

## Developer Pain Points
1. **Chat history disappearance after updates** – The #1 pain point across 10+ issues. Recurring on both macOS and Windows; threads remain on disk but UI fails to list them. Community workarounds involve manual SQLite queries.
2. **Windows sandbox instability** – `os error 740` / `CreateProcessAsUserW` failures in CLI and Desktop. Forces rollback to 0.132.0. Multiple open issues (#24391, #26158, #27278).
3. **Context compaction errors** – `invalid_enum_value` and `context_length_exceeded` errors disrupt long sessions. Workarounds like #27267 exist but no permanent fix.
4. **Unpredictable usage limit consumption** – Pro users report depleting weekly limits 2–3× faster than expected, with no clear breakdown of token usage per turn.
5. **Stuck “Thinking” UI** – Turns get stuck, Stop button fails, and the thread may become invisible after a restart (#24287). Lacks recovery mechanism.

*Digest generated from `github.com/openai/codex` data as of 2026-06-10.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-10

## Today's Highlights
Three patch releases and a new preview rolled out today, highlighted by a critical PTY resize crash fix in v0.46.0 and a backend definition alignment in v0.47.0-preview.0. Community attention is on a recurring issue where the agent overrules user actions (#27417, 12 comments) and a newly reported "Thinking Bug" (#27766) that leaves the agent stuck for minutes on simple tasks.

## Releases
- **[v0.47.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-preview.0)** — Respect backend definition; version bump from nightly builds.
- **[v0.46.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0)** — Fix: harden PTY resize against native crashes. Includes changelogs from v0.45.0-preview.0 and v0.44.0.
- **[v0.46.0-preview.3](https://github.com/google-gemini/gemini-cli/releases/tag/v0.46.0-preview.3)** — Cherry-pick `f08b4af` (Vertex AI model mapping fix) into preview branch.
- **[v0.45.3](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.3)** — Same cherry-pick backported to the stable v0.45.x line.

## Hot Issues
1. **[#27417 — Gemini overrules user action and does what it wants](https://github.com/google-gemini/gemini-cli/issues/27417)** — *CLOSED, 12 comments*. User reports CLI ignoring explicit instructions. High community frustration; labelled `need-information` and `possible-duplicate`.

2. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — *OPEN, 6 comments, 👍2*. Critical reliability bug: `codebase_investigator` returns "success" even when hitting turn limits, masking failures. Maintainers flagged `need-retesting`.

3. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — *OPEN, 6 comments*. User reports custom skills are ignored unless explicitly invoked. Echoes broader concern about agent tooling utilization.

4. **[#27766 — Thinking Bug](https://github.com/google-gemini/gemini-cli/issues/27766)** — *OPEN, 4 comments, created yesterday*. CLI gets stuck "thinking" for 7+ minutes on tasks normally taking 1–2 minutes. Fresh issue, likely to trend.

5. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** — *OPEN, 4 comments, 👍3*. Frequent report: simple commands hang, showing "Awaiting user input" after completion. Priority P1.

6. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — *OPEN, 4 comments, 👍1*. Browser agent does not function on Wayland. User reports termination reason "GOAL" despite failure.

7. **[#22093 — (Sub)agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** — *OPEN, 2 comments*. User had agents disabled in config, but v0.33.0 silently re-enabled subagents. Privacy/control concern.

8. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** — *OPEN, 2 comments, 👍1*. Model uses `git reset`/`--force` when safer alternatives exist. Request for built-in guardrails.

9. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** — *OPEN, 3 comments*. Agent hits API limits when too many MCP/shell tools are registered. Suggests tool pruning needed.

10. **[#21432 — Improve Agent "Self-Awareness": Accurate CLI Flags, Hotkeys, and Self-Execution](https://github.com/google-gemini/gemini-cli/issues/21432)** — *OPEN, 2 comments*. Feature request: CLI should understand its own flags and hotkeys to act as its own guide.

## Key PR Progress
1. **[#27749 — Vertex AI model mapping fix](https://github.com/google-gemini/gemini-cli/pull/27749)** — Refactors model mapping for `gemini-3.5-flash` under non-API-key auth paths. Cherry-picked into v0.46.0-preview.3 and v0.45.3.

2. **[#27767 — Prevent path traversal vulnerabilities during skill install](https://github.com/google-gemini/gemini-cli/pull/27767)** — Security fix: fully mitigates three traversal vectors in `installSkill`, `linkSkill`, and `uninstallSkill`.

3. **[#27771 — Fix MCP header encoding for non-ASCII values](https://github.com/google-gemini/gemini-cli/pull/27771)** — Fixes #25668: MCP HTTP transport discovery no longer fails when custom headers contain Unicode (e.g., `mąka`).

4. **[#27643 — Fix parallel workspace compilation race condition](https://github.com/google-gemini/gemini-cli/pull/27643)** — Splits workspace build into sequential stages (core → libs → apps) to prevent inter-package compilation races.

5. **[#23948 — Prevent infinite re-render loop in useFlickerDetector and useSessionResume](https://github.com/google-gemini/gemini-cli/pull/23948)** — Fixes a critical UI lockup where missing dependency arrays caused infinite React re-renders.

6. **[#27391 — Filter internal session context from history during resumption](https://github.com/google-gemini/gemini-cli/pull/27391)** — Stops `<session_context>` XML blocks from appearing as user messages in resumed sessions.

7. **[#27772 — Standardize tool output formatting](https://github.com/google-gemini/gemini-cli/pull/27772)** — Introduces `wrapUntrusted` helper for consistent text formatting across MCP, shell, and web-fetch outputs.

8. **[#27453 — Re-seed metadata when chat session file is recreated mid-session](https://github.com/google-gemini/gemini-cli/pull/27453)** — Fixes parsing failure when session `.jsonl` is deleted and recreated externally.

9. **[#27465 — Surface extension disable/enable feedback to the user terminal](https://github.com/google-gemini/gemini-cli/pull/27465)** — Previously `extensions disable <name>` produced zero terminal output, making it appear broken.

10. **[#27631 — Add static eval source analyzer](https://github.com/google-gemini/gemini-cli/pull/27631)** — New tooling to parse `.ts` eval files with TypeScript AST, extracting helper names, base evals, and tags for evaluation development.

## Feature Request Trends
- **AST-aware codebase understanding** — Multiple requests for parsing code at the AST level (#22745, #22746) to improve file reads, method bounds, and navigation, potentially reducing token usage and turn count.
- **Agent self-awareness** — Users want the CLI to document its own flags, hotkeys, and capabilities so it can answer questions about itself (#21432).
- **Memory system improvements** — Active workstream on Auto Memory: deterministic redaction (#26525), stop retrying low-signal sessions (#26522), and quarantine invalid patches (#26523).
- **Browser agent resilience** — Requests for automatic session takeover (#22232) and Wayland support (#21983).
- **Destructive operation guardrails** — Community asks for built-in warnings before risky commands like `git reset --force` or database modifications (#22672).
- **Better subagent utilization** — Users want the main agent to autonomously use custom skills without explicit instruction (#21968).

## Developer Pain Points
- **Agent hallucinates completion** — Subagent reports "GOAL" success even when hitting MAX_TURNS (#22323). Reliability issue undermines trust in autonomous workflows.
- **Shell hangs after command finish** — The "Waiting input" stuck state (#25166) is a recurring P1 issue affecting core terminal interaction.
- **Wayland incompatibility** — Browser subagent is unusable on Wayland (#21983), blocking Linux users adopting the browser tool.
- **Performance degradation** — The "Thinking Bug" (#27766) and general slowness reports indicate increasing latency regressions.
- **Config overrides ignored** — Both browser agent settings (#22267) and agent enablement flags (#22093) are sometimes silently disregarded, eroding user control.
- **Tool overload** — >128 registered tools cause 400 errors (#24246); the agent lacks built-in tool-scoping logic.
- **Missing user feedback** — Extension management (disable/enable) and session resumption lacked any terminal output until recent PRs (#27465, #27391).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-10

## Today’s Highlights
- **v1.0.61 released** (June 9) with a polished agents picker, a new `/settings` dialog, and a fix for blank screen on session resume.  
- **Critical regression reports** are piling up: clipboard breakage on Linux, authentication failures on session resume, and a wave of MCP‑related startup loops.  
- **Long‑standing issue #53** (bring back `github copilot` CLI commands) continues to simmer with 75 👍 and 31 comments – the community has begun rolling their own alternatives.

## Releases
### [v1.0.61](https://github.com/github/copilot-cli/releases) — 2026-06-09
- **Polish:** Consistent borders, headers, and styled inputs in the agents picker and “Create New Agent” wizard.  
- **Bug fix:** Resuming a session no longer leaves the screen blank.  
- **New feature:** `/settings` interactive dialog lets users browse and edit all settings in one place.  
- **Bug fix:** Resuming a local session with … *(description truncated in source)*.

## Hot Issues (10 of 30 updated in last 24h)
1. **[#53 – Bring back the GitHub Copilot in the CLI commands to not break workflows](https://github.com/github/copilot-cli/issues/53)** (75 👍, 31 comments)  
   *After six months of silence, the community is building their own forks. This is the most vocal backward‑compatibility request.*  
2. **[#1703 – Copilot CLI does not list all org‑enabled models (e.g. Gemini 3.1 Pro)](https://github.com/github/copilot-cli/issues/1703)** (54 👍, 29 comments)  
   *VS Code sees the models, CLI doesn’t – confusing for enterprise users who rely on consistency.*  
3. **[#2082 – ctrl+shift+c no longer copies to clipboard on Linux](https://github.com/github/copilot-cli/issues/2082)** (8 👍, 20 comments)  
   *A fundamental terminal shortcut broken since v1.0.4, causing daily frustration for Linux developers.*  
4. **[#2050 – Claude Sonnet 4.6 errors with HTTP/2 GOAWAY / 503](https://github.com/github/copilot-cli/issues/2050)** (4 👍, 8 comments)  
   *Model‑specific connection failures that require multiple retries – especially painful for long running tasks.*  
5. **[#3596 – Error loading model list: “Not authenticated” on session resume](https://github.com/github/copilot-cli/issues/3596)** (10 👍, 3 comments)  
   *Authentication state is lost when resuming a specific session, making `/model` unusable.*  
6. **[#1613 – Feature request: Built‑in git worktree lifecycle management](https://github.com/github/copilot-cli/issues/1613)** (31 👍, 2 comments)  
   *Developers want Copilot to automatically create and clean up git worktrees – high demand, moderate priority.*  
7. **[#2243 – Worktrees are a nightmare, should be disabled by default](https://github.com/github/copilot-cli/issues/2243)** (8 👍, 2 comments)  
   *The counterpoint: automatic worktrees cause merge chaos. Users demand opt‑in only.*  
8. **[#3436 – /mcp search constructs wrong URL for custom MCP registries](https://github.com/github/copilot-cli/issues/3436)** (1 👍, 7 comments)  
   *Missing `/v0.1/` segment in the URL leads to 404. Breaks enterprise MCP setups.*  
9. **[#2540 – Plugin‑defined preToolUse hooks never fire](https://github.com/github/copilot-cli/issues/2540)** (3 👍, 7 comments)  
   *plugins/hooks.json is silently ignored, both in main sessions and sub‑agents.*  
10. **[#3701 – Runaway MCP server spawning (IDE lock‑file watcher re‑init loop)](https://github.com/github/copilot-cli/issues/3701)** (4 comments)  
    *On Windows, MCP servers are spawned repeatedly, exhausting resources. A serious stability hole.*  

## Key PR Progress
Only one pull request was updated in the last 24 hours:  
- **[#3737 – Jigg empire ai](https://github.com/github/copilot-cli/pull/3737)** (by j2030aiNotez)  
  *Summary: “Let’s try this new method”. Appears to be a low‑effort or non‑substantive contribution. No meaningful changes are introduced.*  

*PR activity remains very low this period; most development work is reflected in the v1.0.61 release and ongoing issue triage.*

## Feature Request Trends
Based on the latest issues, the community is consistently asking for:
- **Git worktree integration** (create/destroy as part of the workflow) – #1613, but also strong pushback for it to be opt‑in (#2243).
- **MCP supply chain improvements** – custom registry URL fix (#3436), one‑click enablement of `github-mcp-server` (#3548), support for remote MCP OAuth without repeated re‑auth (#3706).
- **Enterprise custom model support** – centrally configured models should appear in CLI (#3730).
- **Session sharing across machines** – allow local sessions to be synced (#3729).
- **Restored network access** – an option to re‑enable `web_fetch` on private networks (#3731).
- **Telemetry & observability** – skill‑level spans in OpenTelemetry traces (#3725).

## Developer Pain Points
Several high‑frequency frustrations emerge from the last 24h of activity:
- **Backward compatibility broken** – Issue #53 highlights that the CLI commands changed and never reverted, forcing users to maintain workarounds or switch to forks.
- **Authentication fragility** – Session resume can break auth (#3596), and BYOK models never show thinking tokens (#3736).
- **Character encoding bugs** – Three separate issues report corruption of non‑ASCII characters: bash tool `LC_CTYPE=C` (#3601), edit tool corrupting legacy bytes (#3732), and Chinese output double‑encoded (#3726).
- **MCP instability** – Runaway server spawning on Windows (#3701), OAuth fan‑out (#3706), and missing URL segments (#3436) make MCP integrations unreliable.
- **Plugin hook dead zones** – `preToolUse` hooks (#2540) and `userPromptSubmitted` context injection (#3727) are broken, eroding the plugin ecosystem.
- **Windows‑specific regressions** – Ctrl+G launching code‑insiders (#3733), zoom circumvented (#3735), and uninstall failure (#3662).

---

*Digest generated from github.com/github/copilot-cli data as of 2026-06-10. All dates/times are UTC.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-10

## Today's Highlights
Activity on the repository remains low today with no new releases, one open pull request, and two open issues updated in the last 24 hours. The community continues to report stability issues with file processing loops and edit tool failures, while a promising PR aims to improve hook-to-LLM communication. Although the volume is quiet, these signals point to ongoing developer friction around reliability and tool integration.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues
Only two issues were updated recently. Both are highlighted below:

1. **[Bug] Kimi CLI stuck in reading one file again and again and stuck in a loop**  
   *Issue #640* – Opened Jan 2026, updated today. Reports that Kimi CLI v0.76 enters an infinite loop repeatedly reading the same file when using a custom Anthropic endpoint with the `mimo-v2-flash` model on Arch Linux. Has 7 comments and 1 👍.  
   **Why it matters:** Loop bugs directly block productivity and can waste API credits. The long duration (since January) suggests this is a persistent, hard-to-reproduce issue.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/640)

2. **[Bug] Edit tool keeps failing in new kimi-code**  
   *Issue #2443* – Created yesterday (June 9). User reports that the edit tool fails frequently in Kimi Code v0.12.0 using the `k2.6` model on Debian. No comments yet and no reactions.  
   **Why it matters:** The edit tool is a core workflow feature for code modifications. Recurring failures erode developer trust and force workarounds.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2443)

## Key PR Progress
Only one pull request was active today:

1. **feat(hooks): surface PostToolUse hook stderr to LLM context**  
   *PR #2445* – Author: zwpdbh. Changes `PostToolUse` hook from fire-and-forget to awaited, enabling stderr output to be collected and appended to the tool result message. This gives the LLM immediate visibility into hook output after a tool call.  
   **Why it matters:** This improves observability for custom hooks, which is critical for developers building agentic workflows or integrating external services.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2445)

## Feature Request Trends
Due to the low number of open issues, clear feature request trends are minimal. The community has not explicitly requested new features in the past 24 hours. The existing issues are bug reports rather than feature proposals. However, the presence of a PR adding hook stderr visibility hints at an unspoken demand for better debugging and integration capabilities in custom extension points.

## Developer Pain Points
Recurring frustrations based on the active issues:

- **Infinite file-reading loops** – The oldest open issue (#640) highlights a critical stability problem where the CLI locks up by repeatedly reading a single file. This is especially painful for users on Linux with custom endpoints, and the lack of resolution for nearly five months suggests a tricky root cause.
- **Edit tool reliability** – The newest issue (#2443) reports frequent failures of the edit tool in Kimi Code v0.12.0. Without workarounds or a quick fix, developers may struggle to adopt the tool for routine code modifications.
- **Limited diagnostics for hooks** – While not a direct bug report, the PR addressing hook stderr visibility indicates that developers find it hard to debug hook behavior, which can slow down custom integrations.

These pain points collectively signal that while the platform is evolving, core stability and tool reliability remain top concerns for the developer community.

---
*Digest generated from GitHub data for MoonshotAI/kimi-cli. Data snapshot: 2026-06-10.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-10

## Today's Highlights

The community is buzzing over a scathing review of the developer prompt quality (#31498), while two new Anthropic‑compatibility bugs (#31579, #31560) emerged after the Fable 5 rollout. On the PR side, a round‑robin API key rotation feature (#31596) and ACP client staging support (#31392) are advancing, and a major filesystem search refactor (#31566) was merged. No new releases today.

## Releases

None in the last 24 hours.

## Hot Issues

1. **#20695 — Memory Megathread**  
   The go‑to place for heap snapshot collection. 91 comments, 64 👍. Central coordination for memory leaks.  
   [Link](https://github.com/anomalyco/opencode/issues/20695)

2. **#2242 — Sandbox the agent**  
   Long‑standing request for terminal command sandboxing (seatbelt on macOS). 64 comments, 53 👍. Security is a top community concern.  
   [Link](https://github.com/anomalyco/opencode/issues/2242)

3. **#13984 — Can’t copy/paste in CLI**  
   Clipboard broken for many users. 45 comments, 20 👍. Basic usability blocker.  
   [Link](https://github.com/anomalyco/opencode/issues/13984)

4. **#3472 — Context awareness not working (closed)**  
   Selected lines not passed to agent in VSCode. 38 comments, 26 👍. Feature advertised but not functioning.  
   [Link](https://github.com/anomalyco/opencode/issues/3472)

5. **#5674 — Custom OpenAI‑compatible options ignored**  
   `baseURL` and `apiKey` from config not sent to API. 23 comments, 13 👍. Breaks all custom providers.  
   [Link](https://github.com/anomalyco/opencode/issues/5674)

6. **#20802 — Image attachments fail with custom providers**  
   Vision input not reaching models via custom endpoints. 15 comments, 7 👍. Hurts multimodal workflows.  
   [Link](https://github.com/anomalyco/opencode/issues/20802)

7. **#31498 — Extremely bad developer prompt**  
   Viral complaint: agent over‑thinking simple file moves. 7 comments, 1 👍. Highlights prompt engineering debt.  
   [Link](https://github.com/anomalyco/opencode/issues/31498)

8. **#30662 — Auto session title fails for opencode provider**  
   Silent failure for `big-pickle` models. 5 comments. Root cause traced to missing small model config.  
   [Link](https://github.com/anomalyco/opencode/issues/30662)

9. **#31525 — Prompt loop reloads all messages, breaks cache**  
   Byte‑identity lost every iteration, hurting Anthropic prompt caching. 4 comments. Performance regression.  
   [Link](https://github.com/anomalyco/opencode/issues/31525)

10. **#31579 — Anthropic usage validation error with fallbacks**  
    `@ai-sdk/anthropic@3.0.71` rejects `"fallback_message"` type. Breaks Fable 5 fallback. 2 comments.  
    [Link](https://github.com/anomalyco/opencode/issues/31579)

## Key PR Progress

1. **#31596 — Round‑robin API key rotation**  
    `apiKey` arrays per provider for load balancing. Closes #29085.  
    [Link](https://github.com/anomalyco/opencode/pull/31596)

2. **#31392 — Stage edits for ACP native review**  
    Enables file‑review in Zed/Devin via staged changes. Related to #4240, #30913.  
    [Link](https://github.com/anomalyco/opencode/pull/31392)

3. **#28592 — Fix clipboard passthrough under GNU screen**  
    `writeOsc52` now correctly handles screen’s DCS passthrough.  
    [Link](https://github.com/anomalyco/opencode/pull/28592)

4. **#31595 — Make MCP client creation failure‑safe**  
    Graceful error boundaries for SDK defects, proper cleanup on failure.  
    [Link](https://github.com/anomalyco/opencode/pull/31595)

5. **#31515 — Add iFlow provider for web tools**  
    Opt‑in backend for `websearch`/`webfetch` via iFlow.  
    [Link](https://github.com/anomalyco/opencode/pull/31515)

6. **#28936 — Fix TUI question dialog takeover**  
    Prevents question prompt from usurping open dialogs.  
    [Link](https://github.com/anomalyco/opencode/pull/28936)

7. **#31591 — Fix CLI error message output**  
    `.fail()` now displays yargs errors instead of showing help silently.  
    [Link](https://github.com/anomalyco/opencode/pull/31591)

8. **#30682 — Preserve orphan sessions on project ID drift**  
    After `git rebase`, sessions stay attached. Closes #30683.  
    [Link](https://github.com/anomalyco/opencode/pull/30682)

9. **#31589 — Use v2 filesystem search for pickers**  
    Migrates file pickers from legacy endpoint to new `v2.fs.find`.  
    [Link](https://github.com/anomalyco/opencode/pull/31589)

10. **#31581 — Sync models.dev reasoning options**  
    Standardised `toggle | effort | budget_tokens` reasoning capabilities.  
    [Link](https://github.com/anomalyco/opencode/pull/31581)

## Feature Request Trends

- **Sandboxing & security** (#2242) – persistent demand for restricting agent file access and terminal commands.
- **Local model tuning** (#31433, #30662) – ability to set context‑window limits and small‑model fallbacks for local providers.
- **TUI customisation** (#31582, #24822) – configurable widths and tmux window naming.
- **Provider flexibility** – round‑robin API keys (#31596), iFlow support (#31515), env‑var forwarding to server (#9428).
- **Usage visibility** (#27698) – show plan usage stats directly in the CLI.

## Developer Pain Points

- **Memory consumption** (#20695) remains the most commented issue, with users collecting heap snapshots.
- **Custom provider incompatibility** (#5674, #20802, #26412) – options ignored, image attachments broken, streaming errors with vLLM.
- **Context awareness in VSCode** (#3472, #22235) – feature advertised but often non‑functional.
- **TUI bugs** – clipboard broken (#13984), stderr leaking into input field (#31588), session titles not updating (#31592).
- **Prompt performance** – full message reload every loop (#31525), bad prompt structure (#31498), sequential subtask execution (#14195).
- **Anthropic API churn** – validation errors from new response fields (#31579, #31560) after Fable 5 release.

---

*Generated from [anomalyco/opencode](https://github.com/anomalyco/opencode) data as of 2026-06-10.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-10

## 1. Today's Highlights
Yesterday saw the release of **Pi v0.79.1** with support for Anthropic’s Claude Fable 5 (adaptive thinking, `xhigh` effort) and prompt template default arguments. The community has been highly engaged around the new **project trust gating** feature – issue [#5514](https://github.com/earendil-works/pi/issues/5514) attracted 24 comments and 12 upvotes, with many users requesting a smoother opt-out experience. Multiple pull requests landed to integrate Fable 5 on Anthropic, Bedrock, and Bedrock Mantle providers, while the first implementation of an **experimental feature guard** (RFC 0043) was merged.

## 2. Releases
**Pi v0.79.1** was published in the last 24 hours. Key changes:
- **Claude Fable 5** – Added as a supported model for Anthropic and Amazon Bedrock providers, including adaptive thinking and `xhigh` effort levels.
- **Prompt template defaults** – Templates can now specify optional positional arguments using `${1:-default}` syntax.

## 3. Hot Issues (10 noteworthy)
1. **#5514 – Project Trust Feature Feedback**  
   *Closed, 24 comments, 12 👍*  
   Users find the trust prompt intrusive and want a way to permanently trust folders or disable the feature. The PR [#5549](https://github.com/earendil-works/pi/pull/5549) already addresses some concerns.  
   [Issue](https://github.com/earendil-works/pi/issues/5514)

2. **#4180 – Links not clickable anymore**  
   *Closed, 13 comments*  
   After a recent update, hyperlinks in agent output became inert. Marked as `closed-because-bigrefactor`.  
   [Issue](https://github.com/earendil-works/pi/issues/4180)

3. **#4984 – Interactive mode crash on transient terminal EPIPE**  
   *Closed, 13 comments*  
   `edit` tool calls trigger `EPIPE` crashes. A regressive bug affecting users with certain terminal configurations.  
   [Issue](https://github.com/earendil-works/pi/issues/4984)

4. **#4877 – Session folder collision**  
   *Open, 11 comments*  
   Different absolute paths can hash to the same session folder (e.g., `/a/b/c/d` vs `/a-b/c-d`). Minor but surprising.  
   [Issue](https://github.com/earendil-works/pi/issues/4877)

5. **#4185 – Zsh/tmux installation – bad colors/contrast**  
   *Closed, 10 comments, 6 👍*  
   Terminal colour issues on first run, especially in tmux and zsh.  
   [Issue](https://github.com/earendil-works/pi/issues/4185)

6. **#5363 – Add amazon-bedrock-mantle provider for OpenAI-compatible models**  
   *Open, 7 comments, 3 👍*  
   Request to support Bedrock Mantle’s OpenAI-compatible API (GPT-5.5/5.4). PR [#5509](https://github.com/earendil-works/pi/pull/5509) is open.  
   [Issue](https://github.com/earendil-works/pi/issues/5363)

7. **#5464 – Local models: 3–5 minute "Working" status latency**  
   *Closed, 7 comments*  
   High latency with Ollama-backed models during “Working” status, making interactive use nearly impossible.  
   [Issue](https://github.com/earendil-works/pi/issues/5464)

8. **#5350 – SDK: custom tool operations receive host-OS-resolved paths**  
   *Open, 6 comments*  
   Custom file tools over SSH from Windows break because paths are resolved to host OS format instead of remote.  
   [Issue](https://github.com/earendil-works/pi/issues/5350)

9. **#4841 – Footer ignores `modelOverrides.name`**  
   *Closed, 5 comments, 1 👍*  
   The footer displays model ID instead of the user-friendly name set in `models.json` overrides.  
   [Issue](https://github.com/earendil-works/pi/issues/4841)

10. **#5326 – CJK text wraps only at spaces, never between characters**  
    *Closed, 3 comments*  
    Long CJK runs without spaces are not wrapped, causing display overflow.  
    [Issue](https://github.com/earendil-works/pi/issues/5326)

## 4. Key PR Progress (10 important)

1. **#5567 – fix(ai): mark Claude Fable 5 thinking off unsupported**  
   *Closed* – Removes `thinking.type: "disabled"` payload for Fable, preventing 400 errors from Anthropic API.  
   [PR](https://github.com/earendil-works/pi/pull/5567)

2. **#5561 – feat(ai): add Claude Fable 5 to Amazon Bedrock provider**  
   *Open* – Adds effort-based adaptive thinking and `xhigh` support for Bedrock.  
   [PR](https://github.com/earendil-works/pi/pull/5561)

3. **#5563 / #5564 – feat(ai): add Claude Fable 5 and Mythos 5 models**  
   *Closed* – Two PRs adding model metadata, always-adaptive thinking flag, and signature preservation on replay.  
   [PR #5563](https://github.com/earendil-works/pi/pull/5563) | [#5564](https://github.com/earendil-works/pi/pull/5564)

4. **#5509 – feat: Add Amazon Bedrock Mantle OpenAI Responses provider**  
   *Open* – New provider for GPT-5.5/5.4 via Bedrock Mantle API, modelled after Azure provider.  
   [PR](https://github.com/earendil-works/pi/pull/5509)

5. **#5553 – Add prompt template argument defaults**  
   *Closed* – Implements `${N:-default}` syntax for positional defaults in templates.  
   [PR](https://github.com/earendil-works/pi/pull/5553)

6. **#5549 – feat(ui): Improved project approval settings**  
   *Closed* – Adds global trust flag, parent folder inheritance, and VS Code‑like “trust parent” option.  
   [PR](https://github.com/earendil-works/pi/pull/5549)

7. **#5547 – feat(coding-agent): add experimental feature guard**  
   *Closed* – Implements RFC 0043 guard `PI_EXPERIMENTAL=1` to gate untested features.  
   [PR](https://github.com/earendil-works/pi/pull/5547)

8. **#5385 – feat: detect first-run terminal theme**  
   *Open* – Queries terminal for light/dark theme via OSC and persists it to settings.  
   [PR](https://github.com/earendil-works/pi/pull/5385)

9. **#5283 – fix(tui): keep hardware cursor marker during slash-command autocomplete**  
   *Closed* – Fixes CJK IME candidate‑window placement when autocomplete menu is shown.  
   [PR](https://github.com/earendil-works/pi/pull/5283)

10. **#5544 – fix(model-registry): inherit cost from built-in model for custom OpenRouter models**  
    *Closed* – Corrects $0.00 cost display for custom models without explicit `cost` field.  
    [PR](https://github.com/earendil-works/pi/pull/5544)

## 5. Feature Request Trends
- **Project Trust UX** – Multiple requests to simplify trust flows: disable globally, trust parent folders, and expose trust state to extensions ([#5514](https://github.com/earendil-works/pi/issues/5514), [#5523](https://github.com/earendil-works/pi/issues/5523)).
- **New Provider Support** – Strong interest in adding Bedrock Mantle (OpenAI-compatible) and extending existing providers (Together AI model updates, Azure GPT-5.5 context fix) ([#5363](https://github.com/earendil-works/pi/issues/5363), [#5559](https://github.com/earendil-works/pi/issues/5559)).
- **In‑Session Slash Commands** – Users want `/update` to avoid exiting TUI, `/about` to show startup info when quiet mode is enabled ([#4714](https://github.com/earendil-works/pi/issues/4714), [#5548](https://github.com/earendil-works/pi/issues/5548)).
- **Extensibility** – Expose internal APIs (e.g., `isProjectTrusted`) for extension authors, use Markdown instead of XML for skills catalog ([#5523](https://github.com/earendil-works/pi/issues/5523), [#5546](https://github.com/earendil-works/pi/issues/5546)).

## 6. Developer Pain Points
- **Latency with Local Models** – Ollama‑backed models suffer a 3–5 minute “Working” delay on every message, making interactive use impractical ([#5464](https://github.com/earendil-works/pi/issues/5464)).  
- **Terminal and Platform Incompatibilities** – Colour issues in tmux/zsh ([#4185](https://github.com/earendil-works/pi/issues/4185)), viewport lock on Windows ([#5192](https://github.com/earendil-works/pi/issues/5192)), special key handling in Kitty ([#3967](https://github.com/earendil-works/pi/issues/3967)).  
- **Crash on EPIPE / Crashes during Streaming** – Uncaught `write EPIPE` errors and crashes in `getSessionStats()` when token usage is missing ([#4984](https://github.com/earendil-works/pi/issues/4984), [#5386](https://github.com/earendil-works/pi/issues/5386)).  
- **Model‑Specific API Misfires** – Sending unsupported `thinking:disabled` to adaptive‑thinking models ([#5569](https://github.com/earendil-works/pi/issues/5569)), or wrong `max_completion_tokens` parameter for certain providers ([#5331](https://github.com/earendil-works/pi/issues/5331)).  
- **CJK / IME Rendering** – Text wrapping only at spaces breaks CJK display ([#5326](https://github.com/earendil-works/pi/issues/5326)); hardware cursor misplacements during autocomplete have been fixed but underline continued need for full IME support.  
- **Configuration Confusion** – Invalid `models.json` crashes without showing the file path ([#5418](https://github.com/earendil-works/pi/issues/5418)); session folder collisions due to hash collisions ([#4877](https://github.com/earendil-works/pi/issues/4877)).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-10

## Today's Highlights

Qwen Code released two pre-release versions (v0.18.0-preview.0 & v0.18.0-preview.1) today, both including a fix for thought parts appearing in CLI copy output. A significant new **Agent Team** feature for parallel sub-agent coordination has landed as an experimental PR, while the daemon-mode feature batch continues to integrate into main with ACP WebSocket transport and session reaper improvements. Meanwhile, two release workflow failures (v0.17.1-preview.0 and nightly) signal potential CI instability that warrants attention.

## Releases

**v0.18.0-preview.0 & v0.18.0-preview.1**  
([Release v0.18.0-preview.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0-preview.1) | [Release v0.18.0-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0-preview.0))

Both releases share identical changelogs: a `chore(release): v0.17.1` commit from the CI bot, plus a fix from `@he-yufeng` that skips thought parts in CLI copy output (`fix(cli): skip thought parts in copy output`). Notably, these releases appear to have been cut from the same commit and may represent duplicate or retagged artifacts — possibly related to the CI failures tracked in issues #4913 and #4912.

## Hot Issues

1. **[#4514 — tracking(serve): daemon capability gaps & prioritized backlog](https://github.com/QwenLM/qwen-code/issues/4514)**  
   *Author: doudouOUC | 14 comments*  
   A detailed tracking issue for remaining gaps in `qwen serve` HTTP/SSE surface after slash-command passthrough. Includes a full backlog of ACP-compatible command support. Active discussion suggests the team is methodically closing daemon parity gaps.

2. **[#4782 — tracking(serve): ACP Streamable HTTP transport status & upgrade plan](https://github.com/QwenLM/qwen-code/issues/4782)**  
   *Author: chiga0 | 4 comments*  
   Tracks implementation status of the ACP Streamable HTTP transport at `/acp`, enabling native connections from Zed, Goose, and JetBrains. The community is closely watching this as the path to daemon interoperability.

3. **[#4615 — Add project-scoped .mcp.json support with pending approval semantics](https://github.com/QwenLM/qwen-code/issues/4615)**  
   *Author: qqqys | 5 comments*  
   Proposes a security-first MCP server configuration model where workspace `.mcp.json` entries show as `Pending` until explicitly approved. Addresses growing demand for safer MCP server management across projects.

4. **[#4252 — Add Generation Timing Metrics (TPS, TTFT) to /stats](https://github.com/QwenLM/qwen-code/issues/4252)**  
   *Author: Alphapage | 3 comments*  
   Requests real-time TPS and TTFT metrics — a heavily upvoted feature for users comparing providers or debugging performance regressions. Tagged `welcome-pr`, suggesting community contributions are encouraged.

5. **[#4888 — [bug] ask_user_question in IDEA plugin shows no text or input](https://github.com/QwenLM/qwen-code/issues/4888)**  
   *Author: byx1728 | 3 comments*  
   IDEA plugin users cannot see question text or type answers when the model asks a question. Only Submit/Cancel buttons appear. A P2 bug affecting the IDE integration experience.

6. **[#4876 — Using subagent to read images returns incorrect content](https://github.com/QwenLM/qwen-code/issues/4876)**  
   *Author: MachineXu | 3 comments*  
   Subagents (e.g., "image analyst") return completely unrelated content when using `read_file` on images, while the main agent handles the same task correctly. Opens questions about subagent model routing.

7. **[#4907 — Down arrow requires 2 presses to reach subagent content from input](https://github.com/QwenLM/qwen-code/issues/4907)**  
   *Author: pomelo-nwu | 2 comments*  
   A UI navigation bug: the first down arrow lands on an invisible tab bar before reaching actual subagent content. Tagged `welcome-pr`, making it an accessible fix for new contributors.

8. **[#4891 — Terminal resize during streaming leaves fragmented content in scrollback](https://github.com/QwenLM/qwen-code/issues/4891)**  
   *Author: tanzhenxin | 2 comments*  
   During streaming generation, resizing the terminal produces output rendered at mixed widths in scrollback. A P2 rendering bug that degrades the interactive experience on macOS.

9. **[#4904 — qwencode cannot switch to new model](https://github.com/QwenLM/qwen-code/issues/4904)**  
   *Author: Cities2000 | 2 comments*  
   Users of qwen3.7-plus through the Coding Plan cannot select it in qwencode (only 3.6-plus shows). The error reveals hardcoded model availability lists per auth type — a configuration integration issue.

10. **[#4727 — Dual Output mode TUI no response](https://github.com/QwenLM/qwen-code/issues/4727)**  
    *Author: yumiao5279 | 5 comments*  
    When using FIFO-based Dual Output mode (`--json-file` / `--input-file`), the TUI becomes completely unresponsive. A critical bug for users relying on non-interactive pipe-based workflows.

## Key PR Progress

1. **[#4490 — feat(daemon): merge daemon-mode feature batch into main](https://github.com/QwenLM/qwen-code/pull/4490)**  
   *Author: doudouOUC | +115k / -12k LOC across 46 commits*  
   The big one: merging `daemon_mode_b_main` into main for v0.16-alpha. Includes all core daemon features — session management, ACP transport, extension support. This is the primary integration point for the daemon initiative.

2. **[#4844 — feat: add Agent Team experimental feature](https://github.com/QwenLM/qwen-code/pull/4844)**  
   *Author: tanzhenxin*  
   Enables models to create named teams of sub-agents ("teammates") working in parallel — communicating, sharing task lists, and consolidating results. A major expansion of the agent orchestration model.

3. **[#4732 — feat(core): Workflow tool P1 — minimal node:vm sandbox](https://github.com/QwenLM/qwen-code/pull/4732)**  
   *Author: LaZzyMan*  
   Implements the first phase of Dynamic Workflows: a `Workflow` tool running model-authored JS in a `node:vm` sandbox with `agent()` support. Lays groundwork for programmable multi-step agent pipelines.

4. **[#4773 — feat(serve): ACP WebSocket transport (RFD Streamable HTTP phase 2)](https://github.com/QwenLM/qwen-code/pull/4773)**  
   *Author: chiga0*  
   Completes the ACP WebSocket transport layer, adding `wsStream.ts`, connection registry, and lifecycle hooks. Coexists with SSE transport for maximum client compatibility.

5. **[#4827 — feat(serve): ACP/REST parity — 29 new _qwen/* methods](https://github.com/QwenLM/qwen-code/pull/4827)**  
   *Author: chiga0 | +935 lines*  
   Adds 29 new dispatch methods for full ACP/REST parity: session recap, shell, detach, context_usage, rewind, and many more. Required dependency for PR #4773.

6. **[#4850 — feat(extensions): interactive multi-tab /extensions manager](https://github.com/QwenLM/qwen-code/pull/4850)**  
   *Author: BZ-D*  
   Transforms `/extensions` into a full interactive manager with Installed / Discover / Sources tabs, covering the entire extension lifecycle. Highly anticipated by the community.

7. **[#4810 — fix(core): isolate OpenAI SDK abort listener leak](https://github.com/QwenLM/qwen-code/pull/4810)**  
   *Author: yiliang114*  
   Wraps AbortSignal in per-request child controllers to prevent the OpenAI SDK's listener leak from accumulating. A stability fix for long-running sessions.

8. **[#4894 — fix(dual-output): prevent FIFO blocking on startup](https://github.com/QwenLM/qwen-code/pull/4894)**  
   *Author: chiga0*  
   Fixes the #4727 unresponsiveness issue by opening FIFO with `O_RDWR | O_NONBLOCK` and adding a 1 MB buffer. Directly addresses the Dual Output mode blocking bug.

9. **[#4903 — fix(installer): auto-detect SYSTEM account and default PATH scope to machine](https://github.com/QwenLM/qwen-code/pull/4903)**  
   *Author: yiliang114*  
   When the Windows installer runs under SYSTEM, `PATH_SCOPE` now defaults to `machine` (HKLM). Fixes the #4901 issue where `qwen` was not found in new terminal sessions.

10. **[#4917 — fix(openai): default splitToolMedia to true](https://github.com/QwenLM/qwen-code/pull/4917)**  
    *Author: LaZzyMan*  
    Flips the `splitToolMedia` runtime default so tool-returned images (e.g., from `read_file`) properly reach strict OpenAI-compatible backends instead of being rejected.

## Feature Request Trends

1. **Core Protocol & Daemon Expansion (highest volume)**  
   Requests continue around ACP transport completeness (#4782, #4773), daemon capability gaps (#4514), and MCP server configuration (#4615). The community is pushing for full daemon-mode parity with native editor integration.

2. **User Experience & UI Refinement**  
   Multiple requests target improving the interactive experience: safe mode troubleshooting flag (#4883), file display in sidebar panels instead of full-screen (#4885), timestamps in CLI responses (#4899), and keyboard shortcut improvements (#4882).

3. **Parallel & Workflow Execution**  
   Agent Team mode (#4844), Workflow tool sandbox (#4732), and `/cd` session directory changes (#4879) all point toward a desire for more sophisticated multi-agent orchestration and session management.

4. **Cross-Platform & CI/CD**  
   Windows installer improvements (#4901, #4903), automated CHANGELOG generation (#4872), and PR review queue status feedback (#4846) reflect growing demand for enterprise-grade deployment and transparency.

5. **Developer SDK & Extension Ecosystem**  
   In-process MCP server support for the Python SDK (#4889) and archive/URL extension installation (#4910) signal increasing interest in programmatic extensibility and SDK maturity.

## Developer Pain Points

1. **Model Switching & Provider Configuration**  
   Multiple bugs (#4904, #4729, #4758) reveal friction when switching between models or providers — especially with authentication type prefixes leaking into settings and hardcoded model availability lists. This is the single most frequently surfaced stability issue this week.

2. **Dual Output / Non-Interactive Mode Reliability**  
   Issues #4727 (TUI unresponsive with FIFOs) and #4894 (FIFO blocking) show that pipe-based workflows — critical for CI/CD integration — remain fragile. The community is actively invested in fixes here.

3. **Subagent & Multi-Agent Correctness**  
   Bug #4876 (subagent returns unrelated image content) and navigation issues like #4907 (double-press to reach subagent content) indicate that the agent hierarchy UX and model routing for subagents still needs hardening.

4. **Windows & SYSTEM Account Support**  
   Issues #4901 (PATH not set for SYSTEM installs), #4910 (archive extension install), and the Windows CI failures (#4915) highlight ongoing friction for Windows-first and server-deployment use cases.

5. **Release & CI Reliability**  
   Two release workflows failing on the same day (#4912, #4913) — combined with ongoing Windows CI red status — erodes trust in the release pipeline. The community will be watching for a postmortem.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-10

## Today's Highlights

The **CodeWhale** project (formerly `deepseek-tui`) released **v0.8.55**, introducing Together AI provider support, an OpenAI Codex comparison harness, and an expanded Model Catalog. The community is buzzing with substantial i18n progress (localization PRs for mode-pickers, command outputs, and preview widgets) and a major architectural proposal for a **hippocampal memory system** to overcome the 1M-token context window limit. Meanwhile, key bug fixes are in flight addressing YOLO mode verbosity, shell tool blockers, and macOS keyboard normalization.

## Releases

- **v0.8.55** ([release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.55)): Adds **Together AI** as a canonical provider, **OpenAI Codex** provider support, and a **Model Catalog** feature. This is the first release under the **CodeWhale** brand — the legacy `deepseek-tui` npm package is deprecated. Users should follow `docs/REBRAND.md` to migrate.

## Hot Issues

1. **[#2942 — [bug] Codewhale会自问自答](https://github.com/Hmbown/CodeWhale/issues/2942)** (6 comments) — A critical user-facing bug where the agent executes unsolicited actions without instruction. High-urgency with potential to disrupt user projects. No reproduction steps yet.

2. **[#2922 — [enhancement, question] YOLO模式确认行为](https://github.com/Hmbown/CodeWhale/issues/2922)** (4 comments) — A UX concern: the agent repeatedly announces YOLO mode before each atomic action. Community confused whether this is intentional. PR #2933 now addresses this by suppressing redundant mode announcements.

3. **[#2935 — [bug] 海马记忆系统提案（无限上下文）](https://github.com/Hmbown/CodeWhale/issues/2935)** (2 comments) — Proposes a hippocampal memory layer (compaction, recall, cross-session persistence) to supplement the 1M-token window. Received significant design attention from maintainers.

4. **[#2969 — CHANGELOG缺了0.8.55](https://github.com/Hmbown/CodeWhale/issues/2969)** (1 comment) — Quick documentation gap: v0.8.54 changelog blocks have been updated but v0.8.55 entry is missing. Minor but affects release communication.

5. **[#2490 — [bug] 不能编译UE工程](https://github.com/Hmbown/CodeWhale/issues/2490)** (5 comments, closed) — Unreal Engine build integration fails. Closed but possibly needs a more permanent fix.

6. **[#1990 — [enhancement] Remote workbench：美国云基础设施](https://github.com/Hmbown/CodeWhale/issues/1990)** (3 comments) — Strategic initiative to build a US/global cloud workbench (DigitalOcean, AWS, Telegram) as an alternative to the existing Tencent/CN path. Issue #2964 is the implementation slice.

7. **[#1846 — [enhancement] 审批面板遮挡diff差异](https://github.com/Hmbown/CodeWhale/issues/1846)** (1 comment, 👍1) — UI flow issue: approval panel obscures proposed changes diff, preventing informed decisions. Community agrees this needs redesign.

8. **[#2924 — [bug] npm更新失败](https://github.com/Hmbown/CodeWhale/issues/2924)** (1 comment, 👍1) — User reports inability to update via npm after v0.8.55 release. Related to rebrand migration path (#2960 is tracking this).

9. **[#2931 — [bug, enhancement] 自动版本检测更新通知](https://github.com/Hmbown/CodeWhale/issues/2931)** (3 comments, closed) — Proposed auto-update notification mechanism with HTTP GET background check. Closed after community feedback and implementation planning.

10. **[#889 — [enhancement] 集成Paseo ACP协议](https://github.com/Hmbown/CodeWhale/issues/889)** (2 comments, 👍2) — Long-standing request to support the Paseo remote task protocol, allowing programming tasks from mobile. Gaining traction as remote workbench interest grows.

## Key PR Progress

1. **[#2925 — feat: Together AI provider + config + picker](https://github.com/Hmbown/CodeWhale/pull/2925)** (OPEN) — Implements Together AI as a first-class provider: config, CLI/TUI, auth, doctor output, model registry. A major new integration for v0.8.55.

2. **[#2933 — feat: hippocampal memory system + YOLO verbosity fix + tool error improvements](https://github.com/Hmbown/CodeWhale/pull/2933)** (OPEN) — Packed PR: adds memory compaction, improved error messages, and the YOLO mode verbosity fix from issue #2922.

3. **[#2932 — i18n: mode-picker localization (7 locales)](https://github.com/Hmbown/CodeWhale/pull/2932)** (OPEN) — Localizes 8 mode-picker message IDs across all 7 shipped locales. Strong community interest in i18n completeness.

4. **[#2940 — i18n: Cmd command output localization (15 MessageIds)](https://github.com/Hmbown/CodeWhale/pull/2940)** (OPEN) — Localizes all command output strings (/task, /trust, error prefixes) across 7 locales.

5. **[#2943 — fix: macOS SUPER (Cmd) → CONTROL normalization](https://github.com/Hmbown/CodeWhale/pull/2943)** (OPEN) — Fixes inconsistent keyboard shortcut handling on macOS (Cmd vs Ctrl for shortcuts like Ctrl+B).

6. **[#2947 — fix: guide long shell work to background](https://github.com/Hmbown/CodeWhale/pull/2947)** (OPEN) — Fixes #2939: adds >5 second threshold guidance in model prompt, improves `exec_shell` background schema.

7. **[#2905 — fix: name allow_shell blocker for shell tools](https://github.com/Hmbown/CodeWhale/pull/2905)** (OPEN) — Improves diagnostic error messages when shell tools are blocked, naming the exact `allow_shell` blocker.

8. **[#2949 — refactor: decouple allow_shell from static prefix](https://github.com/Hmbown/CodeWhale/pull/2949)** (OPEN) — Moves `allow_shell` into per-turn `<runtime_prompt>` tag to allow DeepSeek prefix cache reuse and reduce token waste.

9. **[#2927 — feat: add Qwen 3.7 Max to OpenRouter catalog](https://github.com/Hmbown/CodeWhale/pull/2927)** (OPEN) — Adds the new Qwen model with alias resolution and test coverage. Shows rapid model catalog expansion.

10. **[#2898 — fix: PDF hang via per-page extraction](https://github.com/Hmbown/CodeWhale/pull/2898)** (OPEN) — Critical fix for PDF tool hanging on certain files. Switches from `extract_text` to `extract_text_by_pages` to avoid deadlock-prone code paths.

## Feature Request Trends

1. **Remote Workbench & Phone Control (Cloud + Chat Bridge)** — Multiple issues (#1990, #2964, #2965, #2968, #2967, #889) converge on building a remote development workbench using cheap VPS and Telegram bridge for phone-controlled AI agent execution. This is the highest-priority strategic direction.

2. **Memory System (Infinite Context / Cross-Session Recall)** — Issue #2935 and related discussion around hippocampal memory, compaction, and session persistence. The 1M-token limit is seen as insufficient for long-running projects.

3. **Localization (i18n) Expansion** — A wave of PRs (#2932, #2940, #2929) localizing UI elements into 7 languages. Community actively expanding accessibility for non-English speaking developers.

4. **Model Provider Diversity** — Requests for new providers: Together AI, DeepSeek V4 via Anthropic API (#2963), Qwen models (#2927, #2930), Siliconflow CN (#2895), and Paseo protocol integration (#889).

5. **Approval UX Improvements** — Persistent theme: approval panel obscuring diffs (#1846), trust-level confusion (#2657), mode toggling friction. Developers want faster, more transparent approval workflows.

## Developer Pain Points

1. **Agent Over-Action / Unauthorized Execution** — Bug #2942 ("自问自答") highlights a critical trust issue where agents act without instruction. Combined with YOLO mode verbosity (#2922), developers are frustrated by unpredictable agent behavior.

2. **Update/Migration Confusion** — The CodeWhale rebrand from `deepseek-tui` is causing installation and update pain (#2924, #2960). Users can't update via npm, and CHANGELOG gaps (#2969) worsen the experience.

3. **Session & Context Management** — Agents struggle with session name conflicts (#2656), sub-tasks blocking new sessions (#2603), and context window limitations (#2935). No sidebar session browser (#2934) for easy navigation.

4. **Telegram Bridge Reliability** — Live smoke tests (#2964) revealed serial update dispatch deadlocks (#2966) and streaming/resilience gaps (#2967) in the remote workbench Telegram bridge.

5. **Performance & UX Rough Edges** — PDF tools hanging (#2898), hotbar rendering incomplete (#2945), shell background cancellation not syncing (#2941), and inconsistent keyboard shortcuts on macOS (#2943).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*