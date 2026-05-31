# AI CLI Tools Community Digest 2026-05-31

> Generated: 2026-05-31 06:56 UTC | Tools covered: 9

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
**Date: 2026-05-31**

---

## 1. Ecosystem Overview

The AI CLI tools landscape is in a phase of **intense stabilization** following rapid feature expansion. Across all seven tools surveyed, two dominant themes emerge: **session/state management fragility** and **tool-call reliability regressions**. The ecosystem shows signs of maturation—tools are moving beyond novelty toward production readiness—but each platform is wrestling with the same core challenges: how to make long-running agent sessions durable, how to handle parallel tool execution safely, and how to enforce project-level configuration consistently. Notably, **no tool shipped a stable release today**, though nightly and patch releases continue for Copilot CLI, OpenCode, and Qwen Code. The community sentiment reflects **frustration with reliability** rather than feature gaps, suggesting the market is now prioritizing robustness over speed.

---

## 2. Activity Comparison

| Tool | Hot Issues (Last 24h) | Key PRs (Last 24h) | Release Status |
|---|---|---|---|
| **Claude Code** | 10 | 4 (documentation only) | No release; latest v2.1.158 has regressions |
| **OpenAI Codex** | 10 | 10 (active development) | No release |
| **Gemini CLI** | 10 | 10 (high velocity) | No release |
| **GitHub Copilot CLI** | 10 | 0 | **v1.0.57-3** (patch) |
| **Kimi Code CLI** | 7 | 3 | No release; latest v1.46 has login bug |
| **OpenCode** | 10 | 10 (rapid) | **v1.15.13** (bugfix) |
| **Pi (pi-mono)** | 10 | 10 (merging) | No release |
| **Qwen Code** | 10 | 10 (high velocity) | **v0.17.0-nightly** |
| **DeepSeek TUI (CodeWhale)** | 10 | 10 (active) | No release; latest v0.8.47 |

**Key insight:** Gemini CLI and OpenCode show the highest PR velocity with substantial architectural work. Claude Code and Copilot CLI show the lowest PR activity, indicating either stabilization or stagnation. Qwen Code and Gemini are investing heavily in memory/durability infrastructure.

---

## 3. Shared Feature Directions

Requirements appearing across **3+ tool communities**:

| Requirement | Affected Tools | Specific Needs |
|---|---|---|
| **Session continuation past limits** | Claude Code (#13354), Codex (#14076), Gemini (implicit), Copilot (#3595) | Graceful resume, no hard cutoffs, idle continuation |
| **Subdirectory support for skills/plugins** | Claude Code (#10238), Copilot (#1632), CodeWhale (#755) | Flat layouts don't scale for enterprise repos |
| **MCP/plugin reliability** | Copilot (#3576, #3583), Qwen (#4641), CodeWhale (#2362), Kimi (#2364) | Windows spawn failures, token refresh, tool inheritance |
| **Session history persistence** | Codex (#20741, #23979), OpenCode (#29823), Pi (#5231, #5044) | Data survives updates, project moves, large file handling |
| **Plan/read-only mode enforcement** | OpenCode (#25263, #30039), Codex (implicit), Gemini (implicit) | Agent should not write files in read-only mode |
| **Cross-platform parity** | Claude Code (macOS model picker), Codex (Windows installer), Gemini (Wayland), Copilot (German keyboard) | Platform-specific bugs are accumulating |
| **Configuration discoverability** | CodeWhale (#2309), Kimi (#2155), OpenCode (#12143) | UIs should expose all options, not just existing config values |

**Notable:** The **session lifecycle** is the single most universal pain point—every tool has at least one major issue about sessions being lost, unrecoverable, or bounded in frustrating ways.

---

## 4. Differentiation Analysis

### Feature Focus
| Tool | Primary Differentiator |
|---|---|
| **Claude Code** | Brand recognition, Claude model access, enterprise "Max" plan |
| **OpenAI Codex** | Desktop integration, app-server architecture, multi-agent orchestration |
| **Gemini CLI** | Agent ecosystem (codebase_investigator, browser), evaluation infrastructure |
| **GitHub Copilot CLI** | VS Code integration, conservative iteration, accessibility improvements |
| **Kimi Code CLI** | Chinese market focus, ACP protocol innovation, but strategic turmoil |
| **OpenCode** | Performance optimization, skill invocation, plan mode enforcement |
| **Pi (pi-mono)** | Terminal multiplexing (cmux), worktree agents, configurable tool permissions |
| **Qwen Code** | OOM/long-session durability, JetBrains integration, memory pressure monitoring |
| **DeepSeek TUI (CodeWhale)** | Chinese-market localization, cache-maximalism, "hunt" recovery vocabulary, slop tracking |

### Technical Approach Differences
- **Codex** and **Gemini** are investing in **queue-based architectures** (app-server queues, subagent dispatch) for better concurrency control.
- **Qwen** and **Gemini** are leading on **memory/durability**: Qwen's atomic write rollout (#4333) and memory pressure monitor (#4403); Gemini's auto-memory PR stack.
- **Claude Code** and **Codex** are the most **enterprise-oriented**, with billing/plan issues dominating their communities.
- **CodeWhale** is uniquely focused on **cache-maximalism**—systematic KV-cache stability is their core architectural thesis.
- **Pi** and **CodeWhale** are the only tools exploring **terminal multiplexer integration** (cmux).
- **Copilot CLI** is the most **conservative**—small patches, few architectural changes, leaning on Microsoft's existing ecosystem.

### Target Users
| Tool | Primary Audience |
|---|---|
| Claude Code | Enterprise teams (Max plan), general developers |
| OpenAI Codex | Desktop-first developers, multi-agent workflows |
| Gemini CLI | Power users, agent-heavy workflows, evaluation-focused |
| Copilot CLI | VS Code ecosystem users, conservative adopters |
| Kimi Code | Chinese developers, ACP protocol enthusiasts |
| OpenCode | Performance-focused developers, multi-model users |
| Pi | Terminal power users, extension developers |
| Qwen Code | JetBrains users, Chinese market, local LLM enthusiasts |
| CodeWhale | DeepSeek ecosystem, Chinese market, cache-optimized workflows |

---

## 5. Community Momentum & Maturity

### High Momentum (rapid iteration, active PRs, growing community)
- **Gemini CLI**: 10 PRs/day, addressing deep architectural issues (PTY leaks, concurrent edits, MCP OAuth). Strong signal of ongoing investment. Evaluation infrastructure (#24353) shows maturation thinking.
- **OpenCode**: 10 PRs/day, shipping v1.15.13 with notable performance fixes. Community is vocal about GPT latency (#29079) but the team is responsive.
- **Qwen Code**: 10 PRs/day, nightly releases, focused on durability. The memory pressure monitor and atomic write initiatives are production-readiness signals.
- **OpenAI Codex**: 10 PRs/day, but PRs are architectural (MCP startup redesign, queue system). High quality, but desktop data-loss bugs (#20741) are a maturity concern.

### Stable but Strained (active community, slower PR velocity)
- **Claude Code**: Largest community (742 comments on #38335), but only 4 documentation PRs today. The session-limit crisis is eroding trust. No code PRs suggests team is in firefighting mode or slow cycle.
- **Pi (pi-mono)**: 10 PRs merged, good velocity, but 5 open issues on crashes/OOM. Talented community but limited resources.
- **CodeWhale**: 10 PRs, clear vision (cache-maximalism, Chinese market), but issue count is growing faster than fixes.

### Low Momentum (few PRs, unresolved regressions)
- **GitHub Copilot CLI**: 0 PRs today. Patch release (v1.0.57-3) but German keyboard bug (#1999) has been open since v1.02. Windows MCP regression (#3576) is critical. Community engagement is low relative to issue count.
- **Kimi Code CLI**: 3 PRs, no release. Strategic turmoil (#2381) and login regression (#2403) suggest team bandwidth is split between `kimi-cli` and `kimi-code`.

### Maturity Indicators
- **Evaluation infrastructure**: Only **Gemini** is explicitly building component-level evaluations (#24353). Others rely on community bug reports.
- **Security posture**: **CodeWhale** (slop ledger, security bypass fixes) and **Qwen** (atomic writes) are ahead. **C**laude Code has an unenforced instruction compliance issue (#53223).
- **Platform parity**: **Copilot CLI** and **Claude Code** have the most cross-platform gaps (Windows/Mac/Linux keyboard, installer, model picker).

---

## 6. Trend Signals

### What the Data Tells Developers

1. **Agent reliability is the #1 market problem.** Every tool has users reporting hangs (#21409 Gemini, #25038 OpenCode), spurious success (#22323 Gemini), or fabricated outputs (#64065 Claude Code). The industry is still figuring out how to make agents trustable.

2. **Session continuity is table stakes.** Users expect to pick up where they left off—across crashes, updates, and project moves. Losing chat history (#20741 Codex) or session state (#38335 Claude) is the fastest way to lose user trust.

3. **Multi‑model and BYO‑provider is non‑negotiable.** OpenCode (#28846), Qwen (#2724), and CodeWhale (#2247) all have active requests to use their own models or pricing. The era of vendor lock-in for AI CLIs is ending.

4. **Windows and Linux parity is still an afterthought.** German keyboard (#1999 Copilot), Wayland browsers (#21983 Gemini), WSL2 clipboard (#27588 Gemini), Windows MCP spawn (#3576 Copilot)—platform-specific bugs are treated as lower priority, which limits adoption.

5. **The "plan mode" pattern is emerging but unenforced.** Multiple tools offer read-only/plan modes (OpenCode #25263, Codex implicit). But agents routinely violate them. This is a trust-critical feature that needs architectural enforcement, not just prompts.

6. **Memory management is the next frontier.** Qwen (#4403), Gemini (auto-memory), and CodeWhale (cache keys) are all investing in memory systems. The tools that solve long-session reliability will win power users.

7. **Chinese ecosystem is diverging.** CodeWhale and Qwen are building for Chinese users (local search, CNY display, platform-aware keybindings). This is creating a parallel feature track that Western tools may need to match for global adoption.

8. **MCP is becoming a standard—but fragile.** MCP integration is everywhere (Copilot, Qwen, Gemini, Codex, CodeWhale), but every tool has MCP-specific bugs: spawn failures, OAuth issues, tool inheritance gaps. The standard is spreading faster than its implementation quality.

---

**Bottom line for developers:** If you need **stability today**, OpenCode and Pi are shipping the most reliable patches. If you want **long-term architectural investment**, Gemini and Qwen are building the right foundations. If you're in the **Chinese market**, CodeWhale and Qwen are your best bets. If you're **enterprise**, Claude Code has the brand but the highest frustration right now. No tool has solved the session-continuity and tool-reliability problems—choose based on which ecosystem you're already in, and budget for hiccups.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026-05-31 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking (Most-Discussed Pull Requests)

| Rank | PR # | Skill | Status | Summary |
|------|------|-------|--------|---------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Open | Typographic quality control: prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point. |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **odt** | Open | OpenDocument (.odt/.ods) creation, template filling, and conversion to HTML. Targets LibreOffice/ISO-standard document workflows. |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design** (improvement) | Open | Revises existing skill for clearer, actionable instructions that Claude can follow within a single conversation. High community interest in skill quality. |
| 4 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer** + **skill-security-analyzer** | Open | Meta‑skills that evaluate other skills across structure, documentation, and security dimensions. Important for ecosystem governance. |
| 5 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1-OSS predictor** | Open | Integrates SAP’s open‑source tabular foundation model for predictive analytics on business data. Enterprise focus. |
| 6 | [#444](https://github.com/anthropics/skills/pull/444) | **AURELION skill suite** (kernel, advisor, agent, memory) | Open | Structured cognitive/memory framework with a 5‑floor thinking template and professional knowledge management. Broad and ambitious. |
| 7 | [#568](https://github.com/anthropics/skills/pull/568) | **ServiceNow platform skill** | Open | Comprehensive coverage of ITSM, ITOM, ITAM, FSM, HRSD, SecOps, and IntegrationHub. Targets the large ServiceNow ecosystem. |
| 8 | [#154](https://github.com/anthropics/skills/pull/154) | **shodh-memory** | Open | Persistent context/memory system for AI agents across conversations. Addresses a core agentic need. |

*Note: All listed PRs remain open. Discussion highlights are inferred from the volume of comments and the detailed summaries provided by authors. The top eight represent the most active conversations in the repository.*

---

## 2. Community Demand Trends (From Issues)

| Issue | Title | Comments | Top Concern |
|-------|-------|----------|-------------|
| [#228](https://github.com/anthropics/skills/issues/228) | Enable org-wide skill sharing in Claude.ai | 13 | **Collaboration**: need for shared skill libraries/direct sharing links to replace manual file transfer. |
| [#62](https://github.com/anthropics/skills/issues/62) | All my skills have disappeared | 10 | **Reliability**: skills vanishing after file renaming; unclear state management. |
| [#556](https://github.com/anthropics/skills/issues/556) | run_eval.py never triggers skills | 9 | **Tooling**: evaluation script broken – 0% trigger rate undermines skill development. |
| [#492](https://github.com/anthropics/skills/issues/492) | Security: community skills under anthropic/ namespace | 6 | **Trust & Security**: impersonation risk; need clear namespace separation. |
| [#189](https://github.com/anthropics/skills/issues/189) | document-skills and example-skills plugins install duplicate content | 6 | **Plugin quality**: duplicate skills waste context window; poor packaging. |
| [#202](https://github.com/anthropics/skills/issues/202) | skill-creator should be updated to best practice | 8 | **Skill quality**: existing meta‑skill too verbose, not action‑oriented; needs rewrite. |

**Additional recurring themes:**
- **MCP integration** ([#16](https://github.com/anthropics/skills/issues/16)) – exposing skills as MCP tools.
- **AWS Bedrock compatibility** ([#29](https://github.com/anthropics/skills/issues/29)) – running skills on Bedrock.
- **Multi‑file skill support** ([#1220](https://github.com/anthropics/skills/issues/1220)) – bundling reference files for larger skills.
- **Context window management** ([#1102](https://github.com/anthropics/skills/issues/1102)) – preventing data bloat from MCP calls.

**Most‑anticipated new skill directions:**  
- Enterprise platform integration (SAP, ServiceNow)  
- Document quality & typography  
- Memory/persistence for agents  
- Security analysis and governance  
- Skill authoring tooling and validation  

---

## 3. High-Potential Pending Skills (Likely to Land Soon)

These open PRs have active discussion and mature implementations. They address major gaps and should be watched for merging:

| PR | Skill | Why It May Land Soon |
|----|-------|----------------------|
| [#1140](https://github.com/anthropics/skills/pull/1140) | **agent-creator** | Adds meta‑skill for task‑specific agent sets plus critical fixes for evaluation and Windows support. Updated within days of report date. |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Comprehensive testing skill (unit, React, E2E, contract) – a common request. |
| [#190](https://github.com/anthropics/skills/pull/190) | **n8n-builder / n8n-debugger / faf-expert** | 4 production‑tested skills for workflow automation and persistent project context. |
| [#1050](https://github.com/anthropics/skills/pull/1050) | skill‑creator: Windows fixes | 1‑line fixes for `run_loop.py` on Windows – low risk, high impact. |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill‑creator: Windows subprocess fix | Fixes `run_eval.py` crash on Windows (0% trigger rate) – directly addresses [#556](https://github.com/anthropics/skills/issues/556). |
| [#335](https://github.com/anthropics/skills/pull/335) | **masonry-generate-image-and-videos** | Image/video generation skill (Imagen 3.0, Veo 3.1) – taps into growing media generation demand. |
| [#147](https://github.com/anthropics/skills/pull/147) | **codebase-inventory-audit** | 10‑step codebase cleanup workflow – popular for maintenance tasks. |

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for reliable, tool‑tested, and collaboratively shareable skills that integrate with enterprise platforms and improve the quality of AI‑generated documents and agent memory.**

---

# Claude Code Community Digest — 2026-05-31

## Today's Highlights

No new releases shipped in the last 24 hours, but the community remains highly engaged in two protracted conversations: the controversial session-limit exhaustion on the Claude Max plan (Issue #38335) continues to dominate with 742 comments and 458 reactions, and a cluster of regressions in v2.1.158 around tool-call reliability and model behavior (spiralling, invented outputs) is drawing urgent attention. Meanwhile, four long-standing documentation PRs finally closed, and a security architecture report about CLAUDE.md enforcement is accumulating supporting reports.

## Releases

No releases in the last 24 hours. The latest usable version remains **v2.1.158**, which is itself the subject of several newly filed regressions (see Hot Issues below).

## Hot Issues

1. **[#38335 — Session limits exhausted abnormally fast since March 23](https://github.com/anthropics/claude-code/issues/38335)** – The single most-commented issue on the repo. 742 comments, 458 👍. Users on the Max plan report burning through their 5-hour session window in under an hour with no heavy usage. Anthropic has acknowledged the severity but no fix has shipped. Remains open since March 24.

2. **[#13354 — Continue when the session limit is reached](https://github.com/anthropics/claude-code/issues/13354)** – 52 comments, 115 👍. A widely-requested feature asking for a seamless "continue" workflow rather than hard session cutoffs. Signals deep user frustration with the current limit design.

3. **[#10238 — Add support for subdirectories in skills](https://github.com/anthropics/claude-code/issues/10238)** – 44 comments, 154 👍. Teams adopting skills at scale want to organize them into subdirectories. Currently everything must be flat, which doesn't scale for enterprise repos.

4. **[#60334 — Image processing failures causing token waste](https://github.com/anthropics/claude-code/issues/60334)** – 33 comments. A cost-related bug where the API silently drops images and reburns the same tokens, consuming up to 70% of the usage window. Closed but still generating discussion about transparency in error handling.

5. **[#22264 — Parallel tool calls cascade-fail when one fails](https://github.com/anthropics/claude-code/issues/22264)** – 28 comments, 49 👍. An architectural concern: when Claude Code issues multiple tool calls in parallel, a single failure cancels all siblings. Forces wasteful retries. No consensus on fix yet.

6. **[#62063 — Claude Code defaults to 1M context on Pro plan](https://github.com/anthropics/claude-code/issues/62063)** – 21 comments. New sessions silently select the 1M context window, which is not available on Pro plans, causing immediate session errors. Plan detection appears broken.

7. **[#53915 — Server temporarily limiting requests (rate limiting)](https://github.com/anthropics/claude-code/issues/53915)** – 17 comments. Users on Windows and VSCode hitting server-side throttling that is not a usage-limit, suggesting Anthropic infrastructure is struggling under load.

8. **[#53223 — CLAUDE.md instruction compliance is architecturally unenforced](https://github.com/anthropics/claude-code/issues/53223)** – 13 comments. A security report documenting that model behavior is not reliably bound by project instructions. Multiple independent reports now linked. Low reaction count but high severity.

9. **[#63456 — Opus 4.8 not selectable in CLI `/model`](https://github.com/anthropics/claude-code/issues/63456)** – 12 comments. A platform discrepancy where the CLI picker doesn't list Opus 4.8 despite it being available on the web app. Affects macOS users on Max plans.

10. **[#63935 — Regression in 2.1.158: tool call spirals during file reads](https://github.com/anthropics/claude-code/issues/63935)** – 3 comments, but 3 👍 and filed as a regression. Version 2.1.157 was clean; 2.1.158 introduces redundant/invented tool calls. Several companion issues filed on the same day (#64136, #64047, #63881) paint a picture of a problematic release.

## Key PR Progress

Only **4 PRs** were updated in the last 24 hours, none of which are code changes to the engine itself. This is an unusually quiet day for merges.

1. **[#39043 — Remove "retro-futuristic" recommendation from Frontend Design Skill](https://github.com/anthropics/claude-code/pull/39043)** – Opened by t3dotgg. A small but humorously-framed PR to remove a questionable design prompt. Still open since March 25.

2. **[#45156 — Fix strikethrough in Korean Tool Search docs](https://github.com/anthropics/claude-code/pull/45156)** – Closed. A documentation fix for accidental markdown formatting in the Korean locale. Contributed by hilyfux.

3. **[#45150 — Expand CLAUDE_CODE_ACCESSIBILITY docs with screen reader guidance](https://github.com/anthropics/claude-code/pull/45150)** – Closed. Adds a new Accessibility section to the README, documenting how `CLAUDE_CODE_ACCESSIBILITY=1` synchronizes the terminal cursor with dialog tab focus.

4. **[#45151 — Add FORCE_HYPERLINK environment variable documentation](https://github.com/anthropics/claude-code/pull/45151)** – Closed. Documents the `FORCE_HYPERLINK` env var for users in tmux, screen, and custom terminal emulators where hyperlink auto-detection fails.

## Feature Request Trends

Three clear themes emerge from this week's issue stream:

- **Session lifecycle management** – Users want to continue past session limits gracefully (#13354), start ephemeral/incognito sessions that don't persist state (#42159, #64141), and have clear privacy controls (#64141). The current all-or-nothing session model is the top complaint.

- **Skills & configuration at scale** – Support for nested skill directories (#10238) and better hooks/agent lifecycle (#64120, #42159) are driving demand from professional teams. The flat skills model and lack of subdirectory support are cited as adoption blockers for larger codebases.

- **TUI and accessibility polish** – Multiple requests for visual state indicators: a window-title "LED" showing prompt state (#64139), better multi-line cursor navigation (#63670), and improved screen reader support (now partially addressed by #45150).

## Developer Pain Points

1. **Cost/session limit anxiety** – The #38335 saga remains unresolved. Users are burning session windows without clear attribution, and the lack of granular usage diagnostics makes debugging impossible. This is the single largest source of community anger.

2. **Tool-call reliability regression** – v2.1.158 introduced a cluster of tool-call bugs: spiralling redundant calls (#63935), cascade failures from parallel execution (#22264), hanging on Bash errors (#63881), and invisible tool results (#64140). Several reports self-diagnose the issue in conversation but the model cannot self-correct.

3. **Build output hallucination** – A new category of issue (#64065) where Opus 4.8 at high effort confidently asserts tool-output values *before* the tool calls return. The model is fabricating results and then discovering the contradiction. Multiple reporters call this a regression from earlier Opus versions.

4. **Platform parity gaps** – Windows users hit unique server throttling (#53915) and locale rendering bugs (#64111). macOS users can't select Opus 4.8 (#63456). Linux users face instruction-enforcement gaps (#53223). The cross-platform experience remains uneven.

5. **Instruction compliance is fragile** – The security report on CLAUDE.md enforcement (#53223) has collected 10+ independent corroborations. Users report that model behavior diverges from project guidelines unpredictably, undermining trust in agentic autonomy.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-31

## Today’s Highlights
No new releases landed in the last 24 hours, but the repository is buzzing with activity: a cluster of high‑impact bugs – especially chat‑history loss after updates on both macOS and Windows – continues to draw community attention. On the development side, a coordinated 6‑part series of PRs is reshaping how MCP servers are started (lazy, non‑blocking), and the long‑awaited app‑server queue system for follow‑up turns is progressing through several stacked PRs.

---

## Releases
No new releases or tags in the last 24 hours.

---

## Hot Issues
*10 notable issues updated in the last 24h, selected for impact and community engagement.*

1. **[#13993 – Support standalone Windows installer (`codex-setup.exe`)](https://github.com/openai/codex/issues/13993)**  
   *54 comments, 125 👍*  
   The most upvoted open issue. Windows users blocked by Microsoft Store restrictions, corporate policies, or offline environments are demanding a traditional `.exe` installer. This request has been open since March and is gaining momentum.

2. **[#20741 – Codex Desktop project chat histories disappeared after recent update](https://github.com/openai/codex/issues/20741)**  
   *23 comments, 13 👍*  
   A major regression on macOS Tahoe. After an update, all local project conversations are gone from the UI, though data remains on disk. Multiple related duplicates exist (e.g., #23979, #23193, #19290, #20493) – a clear pattern of migration bugs.

3. **[#12840 – Auto set light/dark theme variants based on OS preference](https://github.com/openai/codex/issues/12840)**  
   *12 comments, 2 👍*  
   Request for Codex CLI to respect macOS appearance settings automatically. Small but long‑standing (since Feb 2026), reflects desire for better desktop integration.

4. **[#8258 – Remove leading two-space indent from prompts](https://github.com/openai/codex/issues/8258)**  
   *10 comments, 27 👍*  
   Annoying UX: every prompt line has a 2‑space indent that breaks copy‑paste. Users want it removed. High support given its simplicity.

5. **[#23979 – Codex Desktop conversation history missing after update (state_5.sqlite intact)](https://github.com/openai/codex/issues/23979)**  
   *9 comments, 2 👍*  
   Another data‑loss report on macOS (May 22 update). User confirmed SQLite rows exist but UI doesn’t show them. Highlights a core session‑migration bug.

6. **[#22099 – Parallel-first subagents and nonblocking background task management](https://github.com/openai/codex/issues/22099)**  
   *8 comments, 0 👍*  
   A feature request from a fork (“Open Codex CLI”) that wants proactive multi‑subagent parallelism. Even without many likes, the discussion touches core architecture.

7. **[#24438 – Computer use disabled for individual account in Central Asia (Tajikistan)](https://github.com/openai/codex/issues/24438)**  
   *7 comments, 0 👍*  
   Geographic restriction issue. The computer‑use feature is blocked on a Pro account in Tajikistan – raises concerns about regional feature gating.

8. **[#21781 – [Windows] Browser plugin fails with "browser-client is not trusted"](https://github.com/openai/codex/issues/21781)**  
   *7 comments, 3 👍*  
   A persistent Windows‑specific bug. Even the advertised Chrome and iab backends produce trust errors, blocking browser automation. Related to #25247 and #23831.

9. **[#25355 – Proposal: repo-local project-state tools for cross-session agent coherence](https://github.com/openai/codex/issues/25355)**  
   *5 comments, 0 👍*  
   Fresh proposal for tools that let long‑running Codex agents persist state (handoff notes, ledgers) across sessions. A thoughtful design idea from the community.

10. **[#22099 – (app‑server queue follow‑ups)](https://github.com/openai/codex/issues/22099)** – already covered above.

---

## Key PR Progress
*10 important PRs updated in the last 24h, selected for architectural significance and feature completeness.*

1. **[#25018 – Add app-server `thread/delete` API](https://github.com/openai/codex/pull/25018)**  
   Permanent thread deletion on the server side, including cleanup of subagent threads. Essential for full session lifecycle management.

2. **[#25060 – Add goal extension idle continuation](https://github.com/openai/codex/pull/25060)**  
   Small core primitive: allows a goal extension to request a normal model turn when the thread becomes idle, unlocking resumable goals.

3. **[#25351 – Lock multi-agent runtime version per thread](https://github.com/openai/codex/pull/25351)**  
   Prevents resumed/forked threads from picking up a different multi‑agent system than they started with. Critical for deterministic behavior.

4. **[#25364 – Add SessionStart hook environment overlays](https://github.com/openai/codex/pull/25364)**  
   Structured, shell‑agnostic way for setup hooks to export environment variables to subsequent shell commands. A foundation for improved project bootstrapping.

5. **[#24812 – Show enterprise monthly credit limits in status](https://github.com/openai/codex/pull/24812)**  
   Enterprise users will see their credit cap in `/status` – a small but important transparency improvement.

6. **[#23620 – Dispatch queued turns from app-server](https://github.com/openai/codex/pull/23620)**  
   Together with #25258, this brings durable follow‑up queues to the app‑server. Turns can be stored and executed serially when the thread becomes idle.

7. **[#25283 – Synchronize runtime workspace roots in thread settings](https://github.com/openai/codex/pull/25283)**  
   Ensures queued dispatch sees the same workspace context as direct turns. Needed for the queue system to work correctly.

8. **[#25232 – Keep window generation stable across rollback and resume](https://github.com/openai/codex/pull/25232)**  
   Prevents stale WebSocket state after rollback and ensures `x-codex-window-id` persists. Related to #21986.

9. **[#25214–#25212–#25338 – 6‑part MCP startup series](https://github.com/openai/codex/pulls?q=is%3Apr+label%3Amcp+updated%3A%3E%3D2026-05-30)**  
   A coordinated redesign: lazy tool registration (#25211), background startup hidden by default (#25212), atomic header handoff (#25213), explicit MCP dependency readiness (#25214), and workspace mutation approvals (#25338). Moves MCP initialization off the critical path.

10. **[#25335 – Add workspace directory commands to TUI](https://github.com/openai/codex/pull/25335)**  
    Adds `/cwd` and related TUI commands for inspecting/changing the thread workspace directory, plus exposing the runtime workspace in `/status`.

---

## Feature Request Trends
From all open issues, the most demanded feature directions are:

- **Standalone Windows installer** – #13993, by far the highest‑voted request.
- **Better session management** – `/archive` command (#14076), ability to delete conversations from sidebar (#23837), and a resume picker that matches CLI semantics (#19603).
- **Subagent parallelism** – Non‑blocking parallel subagents (#22099), lane/orchestration mode (#19398).
- **Improved TUI** – Light/dark OS theme detection (#12840), remove prompt indent (#8258), interactive `/diff` explorer (#18149), image paste support (#19143), custom statusline API (#14043).
- **Context transparency** – Show context usage and limits similar to Claude Desktop (#18201).
- **Cross‑session coherence** – Repo‑local project‑state tools (#25355) and goal extension idle continuation (#25060).
- **Queued follow‑ups** – Multiple PRs now implementing app‑server queue; community interest in not losing ideas while a turn is running.

---

## Developer Pain Points
Recurring frustrations visible in the issue tracker:

- **Chat history disappearing after updates** – A flood of reports (#20741, #23979, #23193, #19290, #20493, #20506) on both macOS and Windows. Users’ local data remains on disk but the UI no longer surfaces it. This is the #1 stability pain point.
- **Windows‑specific trust/certificate errors** – The browser plugin repeatedly fails with “browser‑client is not trusted” (#21781, #25247, #23831), and the Chrome plugin sometimes vanishes from the marketplace after an update (#23831).
- **Windows path quoting** – Codex generates unquoted paths with parentheses (e.g., Next.js route groups) that break in PowerShell (#21667).
- **macOS `open -a` workspace regression** – Recent app update broke launching Codex with a workspace from the command line (#25166).
- **WSL path migration mismatches** – Project histories disappear after update due to incompatible WSL `cwd` paths (#24364).
- **Enterprise/geographic access** – Computer‑use disabled in some regions (#24438); browser use blocked by enterprise policies even for harmless sites (#24814).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-31

## Today's Highlights

The Gemini CLI repository saw no releases in the past 24 hours, but significant activity continues across both issue tracking and pull requests. Several long-standing bugs around agent hangs, subagent recovery misreporting, and PTY memory leaks received fixes or renewed attention. The community remains focused on agent reliability, AST-aware tooling, and memory system robustness.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#21409 — Generalist agent hangs**  
   *Priority: P1 | Area: agent | Kind: bug*  
   The agent hangs indefinitely when asked to perform simple tasks (e.g., folder creation), requiring users to explicitly instruct the model not to defer to sub-agents. With **8 👍** from the community, this is one of the most impactful reliability issues.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/21409)

2. **#22323 — Subagent recovery after MAX_TURNS reported as GOAL success**  
   *Priority: P1 | Area: agent | Kind: bug*  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the maximum turn limit without doing any analysis. This misreporting hides critical interruptions from the user.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/22323)

3. **#25166 — Shell command execution gets stuck with "Waiting input" after command completes**  
   *Priority: P1 | Area: core | Kind: bug*  
   Simple CLI commands (that do not prompt for input) frequently leave the shell in a hanging state, showing "Awaiting user input." Affects even trivial commands. 3 👍 from the community.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **#24353 — Robust component level evaluations**  
   *Priority: P1 | Area: agent | Kind: customer-issue*  
   An EPIC tracking the evolution from 76 behavioral eval tests to more robust component-level evaluations. The project now runs tests for 6 supported Gemini models, indicating maturation of the evaluation infrastructure.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/24353)

5. **#21983 — Browser subagent fails in Wayland**  
   *Priority: P1 | Area: agent | Kind: bug*  
   The browser subagent fails on Wayland with `Termination Reason: GOAL` but no meaningful output. A significant platform compatibility issue for Linux users.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/21983)

6. **#26525, #26523, #26522 — Auto Memory bugs (security/quality)**  
   *Priority: P2 | Area: security/agent | Kind: bug*  
   A cluster of issues from SandyTao520: secrets redaction happens after content is already sent to the model (#26525), the memory inbox silently skips invalid patches (#26523), and Auto Memory retries low-signal sessions indefinitely (#26522). These are critical for the memory system's reliability and security posture.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/26525) | [#26523](https://github.com/google-gemini/gemini-cli/issues/26523) | [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)

7. **#24246 — 400 error with > 128 tools**  
   *Priority: P2 | Area: agent | Kind: bug*  
   Gemini CLI encounters a 400 error when more than 400 tools are available, revealing a lack of tool-scoping intelligence in the agent.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/24246)

8. **#23571 — Model frequently creates tmp scripts in random spots**  
   *Priority: P2 | Area: agent | Kind: bug*  
   When restricted to shell execution, the model generates multiple edit scripts across various directories, creating significant workspace cleanup overhead.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/23571)

9. **#22267 — Browser Agent ignores settings.json overrides**  
   *Priority: P2 | Area: agent | Kind: bug*  
   The Browser Agent completely ignores `settings.json` configuration overrides (e.g., `maxTurns`), despite the AgentRegistry correctly reading and merging these settings during initialization.  
   [GitHub](https://github.com/google-gemini/gemini-cli/issues/22267)

10. **#22186 — `get-shit-done` output hook causes crash**  
    *Priority: P1 | Area: agent | Kind: bug*  
    The GSD output hook crashes Gemini CLI when it is almost finished printing the user summary. Repeatedly reproducible.  
    [GitHub](https://github.com/google-gemini/gemini-cli/issues/22186)

## Key PR Progress

1. **#27153 — fix(core): serialize concurrent edits to the same file**  
   *Priority: P1 | Area: agent*  
   Fixes a race condition where `EditTool` and `WriteFileTool` could stomp on each other's edits when dispatched concurrently via `Promise.all`. Implements per-file locking. A critical reliability fix.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27153)

2. **#27147 — fix(core): upgrade pty dependencies**  
   *Priority: P1 | Area: core*  
   Upgrades PTY dependencies to pick up the upstream macOS `/dev/ptmx` leak fix from microsoft/node-pty#882. Addresses resource leaks under macOS.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27147)

3. **#27154 — fix(core): prevent PTY memory leak by synchronously deleting active entries**  
   *Priority: P2 | Area: core*  
   Fixes a critical memory and file descriptor leak where PTY entries and headless terminals were never garbage collected because `activePtys.delete()` was wrapped inside a Promise `.then()` that could never resolve.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27154)

4. **#27137 — fix(cli): make --skip-trust actually load workspace settings**  
   *Priority: P2 | Area: core*  
   Fixes the `--skip-trust` flag which was documented to trust the current workspace but silently dropped hooks, extensions, MCP servers, and similar configuration from `.gemini/settings.json`.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27137)

5. **#27139 — fix(core): validate MCP OAuth resources from metadata URL**  
   *Priority: P2 | Area: extensions*  
   Fixes #20017 by deriving the expected protected resource from the metadata URL that returned OAuth resource metadata, rather than guessing. Improves MCP OAuth reliability.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27139)

6. **#27151 — feat(acp): add /compress slash command**  
   *Priority: P2 | Area: agent*  
   Adds `/compress` as a first-class ACP slash command, allowing long-running ACP sessions to compact their history before hitting context-window limits — previously only worked in the TUI.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27151)

7. **#27329 — fix(core): skip missing includeDirectories instead of crashing CLI startup**  
   *Priority: P1 | Area: core*  
   Prevents a single missing directory in `settings.json` (`context.includeDirectories`) from aborting CLI startup with `Error: Directory does not exist`. Gracefully skips invalid paths instead.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27329)

8. **#27505 — fix(core): prevent extra spaces on width-0 CJK continuation cells**  
   *Priority: P2 | Area: core*  
   Fixes a rendering bug where extra spaces were incorrectly injected between CJK (wide) characters in shell output, ensuring correct cross-platform terminal serialization for international users.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27505)

9. **#27591 — fix(cli): fall back for oversized bug report URLs**  
   *Priority: P2 | Area: core*  
   Fixes `/bug` on Android/Termux where oversized GitHub issue URLs (encoding title, client info, and full problem description) exceed the deep-link/intent limit, causing crashes. Falls back to splitting when the URL is too long.  
   [GitHub](https://github.com/google-gemini/gemini-cli/pull/27591)

10. **#27588 — fix(cli): support WSL2 clipboard image paste**  
    *Priority: P2 | Area: core*  
    Adds WSL2 clipboard support by using PowerShell interop to read the Windows clipboard and save images as PNG files, fixing an environment-specific gap. Fixes #22274.  
    [GitHub](https://github.com/google-gemini/gemini-cli/pull/27588)

## Feature Request Trends

Three dominant feature directions emerge from the issue backlog:

1. **AST-aware tooling** — Multiple issues (#22745, #22746, #22747) propose using AST-aware CLIs for file reads, searches, and codebase mapping. The hypothesis is that AST-aware tools can reduce turns, tokens, and noise while improving precision (e.g., reading method bounds in a single call). Tilth and glyph are mentioned as starting points.

2. **Remote agent infrastructure** — The "Remote Agents: Sprint 2" EPIC (#20303) and related issues (#22741) indicate growing demand for backgroundable agents, task-level auth, and cross-repository agent support. Users want agents that persist across sessions and operate asynchronously.

3. **Agent self-awareness and safety** — Issue #21432 asks for accurate self-reporting of CLI flags, hotkeys, and execution capabilities. Issue #22672 asks for built-in safeguards against destructive operations (e.g., `git reset --force`, dangerous DB modifications). These reflect a desire for agents that understand their own boundaries.

## Developer Pain Points

- **Agent reliability** is the top frustration: agents hang indefinitely (#21409), report spurious success (#22323), ignore settings (#22267), crash during output (#22186), and fail on specific platforms (#21983).
- **Tool execution problems** plague users: shell commands get stuck waiting for input that will never come (#25166), concurrent edits race (#27153), >128 tools cause 400 errors (#24246), and temporary scripts litter workspaces (#23571).
- **Configuration and permission issues** surface regularly: subagents running despite being disabled in all configs (#22093), workspace settings silently dropped by flags (#27137), and browser agents ignoring `settings.json` overrides (#22267).
- **Cross-platform gaps** persist: Wayland browser failures (#21983), WSL2 clipboard incompatibility (#27588), Android/Termux URL length crashes (#27591), and Node 20.x `URL.parse` compatibility crashes (#27385).
- **Evaluation infrastructure** remains immature: tests "bleed" or are unreliable (#23166), the steering eval test had to be commented out to pass CI (#23313), and component-level evaluations are still being designed (#24353).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI Community Digest — 2026-05-31

### Today’s Highlights
A patch release v1.0.57-3 improves accessibility with higher-contrast diff backgrounds and fixes session resume after crashes. The community is reacting sharply to several regressions: German keyboard input still broken (#1999), MCP servers fail to spawn on Windows (#3576), and a flurry of keybinding and copy-paste issues surfaced in the last 24 hours. Meanwhile, long-standing feature requests around autopilot mode control and plugin organization continue to attract strong support.

### Releases
**[v1.0.57-3](https://github.com/github/copilot-cli/releases/tag/v1.0.57-3)** – 1.0.57-3  
- **Improved:** High-contrast diff backgrounds now use darker colors to enhance text readability.  
- **Fixed:** Session resume works correctly after a crash that left partial data in the session log.

### Hot Issues (10 Noteworthy)
1. **[#1999 – German keyboard @ input still broken](https://github.com/github/copilot-cli/issues/1999)**  
   *Area: input-keyboard | Upvoted: 1 | Comments: 7*  
   Users on German layouts cannot type `@` (AltGr+Q) or `#`. The issue has persisted since v1.02, making the CLI nearly unusable for affected users. Community frustration is high, with repeated workarounds failing.

2. **[#1632 – Support subfolders for skills](https://github.com/github/copilot-cli/issues/1632)**  
   *Area: plugins | Upvoted: 14 | Comments: 6*  
   Request to allow organizing skills into subdirectories. With 10+ skills, flat structure becomes unwieldy. High upvote count indicates strong demand.

3. **[#2203 – Allow switching to autopilot mode mid-task](https://github.com/github/copilot-cli/issues/2203)**  
   *Area: agents | Upvoted: 9 | Comments: 1*  
   Pre-v0.0.421, users could press Shift+Tab to toggle autopilot while the agent worked. The removal broke an established workflow. Users want it back to allow review-before-approval workflows.

4. **[#3595 – Autopilot should pause for user input on decisions](https://github.com/github/copilot-cli/issues/3595)**  
   *Area: permissions, agents | Upvoted: 0 | Comments: 0*  
   In code review scenarios, users want to approve fixes one-by-one. Current autopilot selects automatically. Feature request gaining traction.

5. **[#3580 – cmd+click opens links twice on macOS](https://github.com/github/copilot-cli/issues/3580)**  
   *Area: input-keyboard | Upvoted: 0 | Comments: 1*  
   Copilot CLI differs from VS Code terminal behavior: `cmd+click` opens links once but then also triggers a normal click, opening it twice. Usability bug.

6. **[#3590 – PreToolUse hook “ask” permission auto-approved](https://github.com/github/copilot-cli/issues/3590)**  
   *Area: permissions, plugins | Upvoted: 1 | Comments: 0*  
   Since v1.0.53, `PreToolUse` hooks returning `permissionDecision: "ask"` show the permission dialog for milliseconds and then auto-approve. Critical security issue for plugin developers.

7. **[#3588 – Long sessions fail with “Failed to get response from AI model”](https://github.com/github/copilot-cli/issues/3588)**  
   *Area: context-memory, models | Upvoted: 1 | Comments: 0*  
   Very long sessions cause repeated retries and eventual failure. Logs show `session.error` with no clear recovery path. Affects heavy users.

8. **[#3576 – Windows: stdio MCP servers fail to spawn (npx ENOENT)](https://github.com/github/copilot-cli/issues/3576)**  
   *Area: platform-windows, mcp | Upvoted: 0 | Comments: 0*  
   Regression in v1.0.56-1 breaks all stdio MCP servers using `npx` or other `.cmd` scripts on Windows. Worked in v1.0.51. High impact for Windows developers.

9. **[#3583 – MCP silent token refresh sends wrong scope → AADSTS90009](https://github.com/github/copilot-cli/issues/3583)**  
   *Area: authentication, mcp | Upvoted: 0 | Comments: 0*  
   After ~60 minutes idle, token refresh uses `resource=<clientId>` instead of `scope=`, causing Azure AD error. MCP servers with Entra OAuth break after idle period.

10. **[#3546 – Plugin skill silently dropped from /skills list](https://github.com/github/copilot-cli/issues/3546)**  
    *Area: plugins | Upvoted: 0 | Comments: 1*  
    Installing a plugin with 9 skills shows “Installed 9 skills” but `/skills list` shows only 8. The same skill (`slim-apply`) consistently missing – a silent data loss.

### Key PR Progress
No pull requests were merged or updated in the last 24 hours. The community is waiting for fixes to the above regressions to land.

### Feature Request Trends
- **Autopilot Mode Control** – Users want granular control: mid-task switching (#2203), decision-point pauses (#3595), and a default agent to avoid repeated `/agent` commands (#3571).
- **Plugin & Skill Organization** – Subfolder support for skills (#1632) and project-scoped hooks in monorepos (#3579) are top requests, driven by users with many custom plugins.
- **MCP Reliability** – Requests to honor `"disabled": true` (#3582), allow mid-turn tool list rebuild after enable/disable (#3577), and fix token refresh (#3583). Windows MCP spawn is a critical blocker.
- **Keyboard & Input Consistency** – Many users are asking for predictable keybinding behavior across platforms and terminals, especially macOS/VS Code terminal parity.

### Developer Pain Points
- **Input-keyboard regressions** – Multiple open issues report broken `@` on German keyboards (#1999), lost copy/paste in Linux since v1.0.49 (#3586), broken `ctrl+c`/`ctrl+shift+j` in tmux (#3587), and inconsistent link click behavior (#3580, #3592).
- **Session & crash resilience** – Windows OS crashes corrupting `events.jsonl` (#3593), long sessions hitting unrecoverable AI model failures (#3588), and silent skill drops (#3546) erode trust in session persistence.
- **MCP and plugin integration** – Windows spawn failures (#3576), token refresh errors (#3583), disabled flags ignored (#3582), and PreToolUse permission bypass (#3590) make MCP/plugin development frustrating.
- **Accessibility and visual regressions** – Bell character ignored despite config (#3573), removal of user prompt background highlight (#3591), and high-contrast diff improvements only partially address broader accessibility needs.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-31

## Today's Highlights

The community is experiencing significant turbulence following the strategic pivot from `kimi-cli` to `kimi-code`, with a heated issue (#2381) questioning the decision to split the project. Meanwhile, a new login regression in version 1.46 (#2403) is blocking users on Linux, adding to the tension. On the development side, the ACP (Agent Communication Protocol) stack sees continued progress with two stacked PRs (#2363, #2364) aimed at session history replay and permission mode switching.

## Releases

No new releases in the last 24 hours. The latest available version remains v1.46 (referenced in bug reports).

## Hot Issues

1. **#2381 — Community fragmentation concern (OPEN)**  
   A strongly-worded post from community member `QuantumLiu` criticizes MoonshotAI’s decision to abandon `kimi-cli` and rebuild from scratch as `kimi-code`. The user argues that the old CLI was functional and questions why the team chose to change functionality rather than iterate. With 4 comments and 0 likes (suggesting moderate but not majority support), this reflects genuine frustration from users who have invested their workflows.  
   🔗 [Issue #2381](https://github.com/MoonshotAI/kimi-cli/issues/2381)

2. **#2403 — Login broken after upgrade to v1.46 (OPEN)**  
   User `AmooEbrahim` reports a complete login failure on Linux 6.14.0-37 after the version bump. No error details are provided in the summary, but this is a critical blocker for any user who upgraded today. Only 1 comment so far, suggesting it may have been reported recently.  
   🔗 [Issue #2403](https://github.com/MoonshotAI/kimi-cli/issues/2403)

3. **#2402 — API request rejected as "high risk" (OPEN)**  
   User `thoughtworld` on Windows 10 reports a 400 error from the Kimi backend rejecting their compaction request as "high risk." This appears to be a safety/rate-limiting false positive on the server side, potentially blocking legitimate usage.  
   🔗 [Issue #2402](https://github.com/MoonshotAI/kimi-cli/issues/2402)

4. **#2404 — Feature request: /goal command (OPEN)**  
   A new feature proposal from `wintrover` suggests adding a `/goal` CLI command that sets a high-level mission objective and allows the agent to autonomously complete it without repeated user confirmations. No comments yet, but aligns with the industry trend toward "agentic" workflows.  
   🔗 [Issue #2404](https://github.com/MoonshotAI/kimi-cli/issues/2404)

5. **#2401 — Support CLAUDE.md alongside AGENTS.md (OPEN)**  
   `JIRBOY` requests that Kimi CLI load `CLAUDE.md` files (the standard used by Claude Code) in addition to its own `AGENTS.md`. This would allow developers who switch between the two tools to maintain a single set of project instructions. Practical and highly requested in multi-tool environments.  
   🔗 [Issue #2401](https://github.com/MoonshotAI/kimi-cli/issues/2401)

6. **#2155 — Configurable prompt symbols (CLOSED, updated recently)**  
   `sdkks` filed this request to allow users to customize the hardcoded emoji prompt symbols (✨, 💫, 📋) in `config.toml`. The practical motivation: users can't easily type the sparkles emoji when searching for past prompts. Closed without resolution — possibly considered too minor, but the recent update activity (May 30) suggests it may be revisited.  
   🔗 [Issue #2155](https://github.com/MoonshotAI/kimi-cli/issues/2155)

7. **#2154 — PermissionRequest hook for auto-approval (CLOSED)**  
   Another feature request from `sdkks` seeking a `PermissionRequest` event hook that would allow programmatic auto-approval of safe tool operations, reducing friction during scripted or trusted workflows. Received 1 👍, indicating some community support. Closed — likely deferred or replaced by the ACP permission work in PR #2364.  
   🔗 [Issue #2154](https://github.com/MoonshotAI/kimi-cli/issues/2154)

## Key PR Progress

1. **#2388 — Fix shell paste text placeholder persistence (OPEN)**  
   `Pluviobyte` addresses a bug (#1946) where long pasted text, folded into `[Pasted text #1]` placeholders, is lost after session history recall. The fix ensures the placeholder handler persists its state. Critical for any user working with large code blocks or logs.  
   🔗 [PR #2388](https://github.com/MoonshotAI/kimi-cli/pull/2388)

2. **#2364 — ACP permission mode switching (OPEN)**  
   `huntharo` introduces protocol-level ACP permission mode switching (default vs. strict). This is the second PR in a stack (building on #2363) and directly addresses the ability to control tool-use permissions dynamically. Important for security-conscious deployments.  
   🔗 [PR #2364](https://github.com/MoonshotAI/kimi-cli/pull/2364)

3. **#2363 — Fix ACP session history replay (OPEN)**  
   The foundational PR in the ACP stack from `huntharo`. It upgrades the ACP SDK to 0.10.0 and ensures that loaded session history is properly replayed via the ACP protocol. Without this, restored sessions would be effectively empty.  
   🔗 [PR #2363](https://github.com/MoonshotAI/kimi-cli/pull/2363)

## Feature Request Trends

The most-requested feature directions from this week's issues point to three clear themes:

- **Autonomous agent workflows**: The `/goal` command request (#2404) signals strong demand for less interactive, more goal-driven operation — the "set and forget" model.
- **Multi-tool compatibility**: Requests to support `CLAUDE.md` (#2401) and customizable prompt symbols (#2155) reflect a community that uses multiple AI coding CLI tools and wants frictionless switching.
- **Programmatic control**: The PermissionRequest hook (#2154) and ACP permission mode work (#2364) show a desire for fine-grained, scriptable control over tool approval, especially in CI/automation contexts.

## Developer Pain Points

Recurring developer frustrations based on this week's data:

- **Strategic whiplash**: Issue #2381 captures raw frustration with the project's direction change. Users who adopted `kimi-cli` as a production dependency feel betrayed by the "split" into `kimi-code`. This is a trust issue that MoonshotAI will need to address with clear communication and migration support.
- **Login instability**: The v1.46 login bug (#2403) is a hard blocker, and its recency suggests either insufficient QA coverage or a rushed release.
- **Server-side false positives**: The 400 "high risk" rejection (#2402) points to overly aggressive backend safety checks that can confuse users and break workflows without clear error messaging.
- **Session history fragility**: The paste placeholder bug (#2388) highlights that session persistence — a core feature for productivity — is still not fully reliable, undermining trust in the tool's memory.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-31

## Today's Highlights

A busy weekend brings **v1.15.13** with critical Anthropic Opus adaptive reasoning fix and new session metadata API support. Meanwhile, community attention is split between **GPT model latency** (Issue #29079, 113 comments) and a long‑running **agent sandboxing feature request** (Issue #2242, 40 comments). Performance‑wise, a **quadratic‑time streaming bug** (Issue #30060) that caused thinking‑mode sessions to hang has already been fixed in PR #30058.

---

## Releases

**v1.15.13** (Core)
- **Bugfix**: Gateway Anthropic Opus 4.7+ adaptive reasoning now correctly retains summarized thinking instead of returning empty thinking blocks.
- **Improvements**:
  - Sessions can store custom metadata via API/SDK (@shantur).
  - Config now loads from the opened location upward, improving multi‑directory setups.

[Release Details](https://github.com/anomalyco/opencode/releases/tag/v1.15.13)

---

## Hot Issues (10 noteworthy)

| Issue | Title | Comments | 👍 | Why it matters |
|-------|-------|----------|----|----------------|
| [#29079](https://github.com/anomalyco/opencode/issues/29079) | GPT Models take too long to respond | 113 | 48 | Severe intermittent latency – even simple commands like “update graphify” can take minutes. Top complaint by far. |
| [#2242](https://github.com/anomalyco/opencode/issues/2242) | Is there a way to sandbox the agent? | 40 | 50 | Long‑standing request for restricting agent file/command access outside the project directory. Comparable to `seatbelt` on macOS. |
| [#28846](https://github.com/anomalyco/opencode/issues/28846) | Adjust Go usage limits after DeepSeek V4 Pro 75% price cut | 34 | 50 | Community asking for lower OpenCode Go subscription caps after DeepSeek permanently slashed API pricing. |
| [#8345](https://github.com/anomalyco/opencode/issues/8345) | `zsh: illegal hardware instruction opencode` | 14 | 6 | Binary crash on CPUs without AVX2 support (e.g., older Macs). Reported on v1.1.19 but still unresolved for some users. |
| [#25038](https://github.com/anomalyco/opencode/issues/25038) | Long‑running shell commands hang after success | 8 | 5 | Gradle/Android builds complete but OpenCode does not return control. Race condition in shell output handling. |
| [#27079](https://github.com/anomalyco/opencode/issues/27079) | MCP tools called with incorrect escaping for parameters | 5 | 1 | Schema validation error when tool arguments contain extra quotes. Affects Qwen 3.6 and likely others. |
| [#25263](https://github.com/anomalyco/opencode/issues/25263) | File Write Executed in Plan Mode | 5 | 0 | Critical violation: agent writes files despite read‑only plan mode constraint. Multiple duplicates (e.g., #30039). |
| [#18757](https://github.com/anomalyco/opencode/issues/18757) | Tool execution frequently fails with ‘Tool execution aborted’ | 4 | 0 | Recurring abort on bash/edit/read tools – forces session restart. v1.3.0 but still reported in later versions. |
| [#12143](https://github.com/anomalyco/opencode/issues/12143) | Plugin without version defaults to “latest” causing semver error | 4 | 1 | Configuration edge case: omitting `@version` in `opencode.json` breaks parsing. Easy to hit for new users. |
| [#29823](https://github.com/anomalyco/opencode/issues/29823) | Desktop chat logs unrecoverable after archiving / moving project | 4 | 0 | Session data tied to absolute path – moving or renaming project folder loses all history. Duplicate #29825. |

---

## Key PR Progress (10 important pull requests)

1. **[#30058](https://github.com/anomalyco/opencode/pull/30058)** — `fix(opencode): O(N²)→O(N) text/reasoning delta accumulation`  
   Fixes the quadratic‑time hang (#30060) in streaming thinking‑mode sessions. Essential for Anthropic extended‑thinking and Qwen3‑thinking users.

2. **[#30046](https://github.com/anomalyco/opencode/pull/30046)** — `fix(session): preserve Anthropic thinking signature across different models`  
   Prevents API error when `thinking` / `redacted_thinking` blocks appear in non‑initial assistant messages after model switch.

3. **[#29217](https://github.com/anomalyco/opencode/pull/29217)** — `feat(tui): Add inline $skill invocations with SKILL pill + pasteText`  
   Long‑requested feature: type `$` in prompt composer to select and invoke skills inline, with autocomplete support.

4. **[#29965](https://github.com/anomalyco/opencode/pull/29965)** — `fix(opencode): Legacy message display`  
   Fixes blank screen when loading older sessions that lack `agent` or `model` fields. Addresses #29908 and #29989.

5. **[#28637](https://github.com/anomalyco/opencode/pull/28637)** — `fix(session): use server timestamps instead of IDs in runLoop exit condition`  
   Solves a long‑standing subtle race where message ID ordering could cause infinite loops or skipped responses.

6. **[#28584](https://github.com/anomalyco/opencode/pull/28584)** — `fix(command): fetch MCP prompts dynamically instead of caching at init`  
   Prevents stale MCP prompt data after `init` – prompts are now fetched per‑session, improving dynamic MCP server integration.

7. **[#30051](https://github.com/anomalyco/opencode/pull/30051)** — `feat(tui): add synthetic scenario previews`  
   Adds `--scenario` flags to preview TUI with realistic agent/sub‑agent turns, useful for theme/UI developers.

8. **[#30042](https://github.com/anomalyco/opencode/pull/30042)** — `fix(session): use parentID instead of ID ordering for loop exit condition`  
   Another take on loop exit fix – uses parent‑message references for correctness across all provider types.

9. **[#30040](https://github.com/anomalyco/opencode/pull/30040)** — `fix(opencode): cap session‑level retries and export MAX_SESSION_RETRIES`  
   Prevents runaway retries in session processor causing resource exhaustion. Adds configurable cap.

10. **[#30003](https://github.com/anomalyco/opencode/pull/30003)** — `fix(opencode): wait for shell output before returning`  
    Fixes a race where shell process exits before stdout/stderr drains – root cause of many “hanging” shell commands (#30001).

---

## Feature Request Trends

Based on all 50+ issues updated in the last 24h:

- **Agent sandboxing & security** – #2242, plus discussion around `permissions/arity.ts` (#30057), shows strong demand for restricting file/command access.
- **Session & chat data persistence** – #29823, #29703 (re‑linkable project paths), #29825 – users want stable session storage independent of folder location.
- **Dynamic workflows / multi‑step automation** – #29059 mirrors Claude Code’s “dynamic workflows” for repeatable project‑local automations.
- **Model provider flexibility** – #28846 (usage limit adjustments), #27692 (explicit context caching for Alibaba / DashScope), #29885 (more detailed provider management in desktop UI).
- **Plan mode enforcement** – #25263 and #30039 highlight that read‑only mode is not always respected; community wants stronger guarantees.
- **MCP / plugin integration** – #30019 (TUI notifications for plugins), #30059 (mic/STT plugin) show interest in richer plugin ecosystem.
- **Performance & caching** – #29079 (GPT latency), #18757 (tool aborts) drive requests for more reliable streaming and cancellation handling.

---

## Developer Pain Points

1. **Intermittent latency** – GPT models can take minutes for trivial tasks (#29079). No clear pattern yet – team investigating.
2. **CPU compatibility** – `illegal hardware instruction` on older Macs/CPUs without AVX2 (#8345, #13379) persists despite previous fixes.
3. **Tool execution reliability** – “Tool execution aborted” errors (#18757) and hanging shell commands (#25038) degrade workflow.
4. **MCP parameter escaping** – Schema errors caused by extra quotes in tool arguments (#27079) affect multiple models.
5. **Data loss on archive/move** – Desktop app loses all chat history when project path changes (#29823, #29703).
6. **False antivirus positives** – Microsoft Defender SmartScreen flags installer since v1.14.42 (#26587), causing installation friction.
7. **Configuration gotchas** – Plugin version defaults to `"latest"` which fails semver parsing (#12143). Also `YAML` indentation errors in docs (#30044).
8. **Plan mode enforcement failures** – Agent writes files despite explicit read‑only directive (#25263) – undermines trust in safety modes.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest · 2026-05-31

## Today’s Highlights
No releases landed today, but the community shipped several high-impact fixes. Infinite loop protection for `AgentHarness` was merged after community complaints about hanging agents, and a critical TUI crash on oversized lines was patched. Windows users got relief from a viewport lock during rendering, and a long-standing issue with session export from binary builds was resolved.

---

## Releases
*None in the last 24 hours.*

---

## Hot Issues

1. **[#5089 – timeoutMs not respected for long operations](https://github.com/earendil-works/pi/issues/5089)**  
   *19 comments, closed*  
   Users on underpowered machines (CPU-only, Llama.cpp) found Pi ignoring `timeoutMs` during long reads. The bug was acknowledged and closed after a fix.

2. **[#4942 – coding-agent CLI hangs after main()](https://github.com/earendil-works/pi/issues/4942)**  
   *12 comments, closed*  
   The CLI never exited because the async `main()` promise was discarded. Node kept the process alive with a pending async operation. Fixed.

3. **[#4210 – Bedrock empty `end_turn` treated as success](https://github.com/earendil-works/pi/issues/4210)**  
   *10 comments, closed*  
   Bedrock’s occasional null responses caused agents to trail off silently. A local extension was built to remediate; the core issue was closed as part of a larger refactor.

4. **[#5223 – Anthropic provider corrupts thinking blocks on multi-turn](https://github.com/earendil-works/pi/issues/5223)**  
   *4 comments, open*  
   Claude Opus 4.8 with adaptive thinking fails mid-session with a 400 error because Pi modifies `thinking` blocks in the latest assistant message. Two upvotes signal interest.

5. **[#5055 – `/tree` help badly formatted](https://github.com/earendil-works/pi/issues/5055)**  
   *2 comments, open*  
   The help text for `/tree` doesn’t wrap, making it useless in narrow terminals. An image shows the problem. Still awaiting UI work.

6. **[#5231 – Crash on 600MB session file](https://github.com/earendil-works/pi/issues/5231)**  
   *2 comments, closed*  
   Opening very large session files caused `Cannot create a string longer than 0x1fffffe8 characters`. Closed quickly with a fix.

7. **[#5044 – OOM on `pi --resume` with large sessions](https://github.com/earendil-works/pi/issues/5044)**  
   *2 comments, open*  
   `buildSessionInfo` reads entire 200+ MB jsonl sessions into memory just for listing. Request for streamed implementation.

8. **[#5084 – Allow/disallow built-in tools in settings.json](https://github.com/earendil-works/pi/issues/5084)**  
   *2 comments, closed*  
   Feature request to control tool allowance (e.g., `read`, `write`) via config instead of CLI flags. Two upvotes, accepted.

9. **[#5208 – Crash on background process late output](https://github.com/earendil-works/pi/issues/5208)**  
   *2 comments, open*  
   `uncaughtException` when `stdout` events fire after `ProcessRegistry` calls `output.finish()`. Needs careful ordering fix.

10. **[#5242 – Overflow auto-compaction fails with undefined abort signal](https://github.com/earendil-works/pi/issues/5242)**  
    *2 comments, closed*  
    Context overflow recovery crashed because `this._autoCompactAbortController` was `undefined`. Fixed by adding a guard.

---

## Key PR Progress

1. **[#5247 – Infinite loop protection for AgentHarness](https://github.com/earendil-works/pi/pull/5247)**  
   *Merged*  
   Adds `maxTurns` and unbound tool detection to prevent agent hangs (fixes #5016, #3960). Core reliability improvement.

2. **[#5246 – Worktree agent extension example](https://github.com/earendil-works/pi/pull/5246)**  
   *Merged*  
   New extension that spawns child `pi` agents in isolated Git worktrees. Useful for parallel review workflows.

3. **[#5245 – cmux bridge extension](https://github.com/earendil-works/pi/pull/5245)**  
   *Merged*  
   Integrates with the `cmux` terminal multiplexer for session and tool lifecycle updates. Non-fatal when `cmux` is absent.

4. **[#5241 – Fix session export from binary builds](https://github.com/earendil-works/pi/pull/5241)**  
   *Merged*  
   Includes `template.css` and `template.js` in the binary copy step so `pi --export` works from the dist folder (fixes #5240).

5. **[#5237 – Avoid continue after pre-prompt compaction](https://github.com/earendil-works/pi/pull/5237)**  
   *Open*  
   Removes `agent.continue()` path after threshold compaction; adds regression test. Addresses session corruption.

6. **[#5235 – TUI overlay focus fix](https://github.com/earendil-works/pi/pull/5235)**  
   *Open*  
   Prevents overlay from losing interactivity when focus returns to editor. Fixes #5129.

7. **[#5233 – Kitty images render correctly in WezTerm](https://github.com/earendil-works/pi/pull/5233)**  
   *Open*  
   Regression from #4461 caused Kitty inline images to show only a top strip. This PR uses reserved rows for correct placement.

8. **[#5234 – `command_start` hook for extensions](https://github.com/earendil-works/pi/pull/5234)**  
   *Merged*  
   New lifecycle hook fires before any registered command runs, allowing cancellation via `{ cancel: true }`.

9. **[#5221 – Fix OpenRouter reasoning role](https://github.com/earendil-works/pi/pull/5221)**  
   *Open*  
   Changes OpenRouter reasoning requests to use `system` role instead of `developer`, aligning with their API schema.

10. **[#5224 – TUI truncates oversized lines instead of crashing](https://github.com/earendil-works/pi/pull/5224)**  
    *Merged*  
    Replaces crash-on-exceed with graceful truncation. Solves width-tracking drift from ANSI/OSC sequences.

---

## Feature Request Trends

- **Configurable tool permissions** – Users want to whitelist/blacklist built-in tools in `settings.json` instead of reusing `--tools` CLI flags (#5084).
- **Persistent caching for `-e` installs** – Running `pi -e npm:pkg` every time re-installs; a keyed cache would reduce overhead (#5222).
- **Better compaction control** – Requests for ratio-based compaction (`keepRecentTokens: 20%`) and clearer event reasons for extensions (#5238, #5217).
- **Richer model selector** – Display pricing and context size alongside model names (#5230).
- **Streamed session loading** – `--resume` and export should handle multi-hundred MB files without OOM (#5044).

---

## Developer Pain Points

- **Large session files are fragile** – Both opening (+600 MB) and listing (+200 MB) cause crashes or OOM. Streamed I/O is urgently needed (#5231, #5044).
- **TUI is crash-prone** – Overlong rendered lines (#5228) and tab character miscalculations (#5218) kill the process. The newly merged truncation fix should help, but more testing is needed.
- **Provider-specific quirks** – Bedrock’s null responses (#4210), Anthropic’s thinking block mutation (#5223), and OpenRouter’s role mismatch (#5229) force users into workarounds.
- **CLI lifecycle issues** – Async promise discarding (#4942) and background output after cleanup (#5208) continue to cause hangs and crashes.
- **Update discovery** – The `pi update` command failed to find the v0.78.0 tag (#5220), suggesting infrastructure or version detection bugs.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the **Qwen Code Community Digest** for **2026-05-31**, based on the latest repository activity.

---

# Qwen Code Community Digest – 2026-05-31

## 1. Today's Highlights

The Qwen Code community saw a high volume of activity this week, with the release of **v0.17.0-nightly** and a strong focus on stability and reliability. Key developments include a series of fixes for **OAuth authentication deadlocks** in JetBrains IDEs, a robust new **memory pressure monitor** to prevent OOM crashes in long sessions, and multiple contributions aimed at improving the **durability and resilience** of session history and file writes.

## 2. Releases

- **v0.17.0-nightly.20260531.c699738f9** [Changelog](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.0-nightly.20260531.c699738f9)
  - This nightly release includes the `v0.17.0` release candidate.
  - **Key fix**: Resolved a critical bug where a "compressed turn" error was falsely triggered when a mid-turn message was interrupted.

## 3. Hot Issues (Top 10)

1.  **#4493 [rider无法登录qwen code]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4493)
    A critical login deadlock for Rider users where the plugin enters a redirect loop during OAuth login, preventing token plan usage. High community engagement with 8 comments, indicating a widespread roadblock for JetBrains users.

2.  **#4637 [fix(acp): discontinued qwen-oauth still returned in authMethods]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4637)
    Files a bug where the discontinued `qwen-oauth` method traps users in a dead-end authentication state in JetBrains IDEs, rendering the plugin unusable. This is a high-priority fix for a broken UX.

3.  **#2724 [Qwen Code agent not working with local ollama in IntelliJ 2026.1]**
    [Link](https://github.com/QwenLM/qwen-code/issues/2724)
    Community frustration as local models via Ollama fail to connect in IntelliJ 2026.1, while working in Rider and WebStorm. The 3 👍 indicate this is a notable regression for users preferring local LLMs.

4.  **#3757 [JetBrains AI 401 error]**
    [Link](https://github.com/QwenLM/qwen-code/issues/3757)
    Users are hitting 401 errors in JetBrains AI, unsure if it's a quota or config issue. This topic remains active, highlighting pain points around authentication and plan management.

5.  **#4363 [Oversized resumed history can fail with Invalid string length]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4363)
    Reports a boundary condition where long-session resume fails catastrophically. This is a critical stability issue, having already been fixed in PR #4531, showing the team's agile response to memory bugs.

6.  **#4627 [Auto-update fails with EACCES]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4627)
    A significant usability bug for macOS users with global npm installations; auto-update fails due to permission issues. A detailed root cause analysis (spawning npm as a non-root user) is provided by the reporter.

7.  **#4651 [feat(core): auto-dump memory diagnostics to disk on pressure detection]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4651)
    A feature request to automatically collect memory diagnostics upon pressure detection, addressing the pain point of losing all diagnostic info after a crash. This is a strategic move to improve debuggability of OOM errors.

8.  **#3511 [JetBrainsAI集成]**
    [Link](https://github.com/QwenLM/qwen-code/issues/3511)
    A request for a simpler, API-key-only integration method for JetBrain’s ACP registry, bypassing the mandatory Qwen OAuth. This reflects a desire for a more standard, friction-free setup.

9.  **#4642 [CLI loading 提示语 能关掉吗？]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4642)
    While closed, this bug report about annoying CLI loading tips (e.g., "忙着搬砖") received a clear "WON'T FIX" from the team, which may lead to feature requests for a toggle in the future.

10. **#4641 [MCP 稳定性]**
    [Link](https://github.com/QwenLM/qwen-code/issues/4641)
    Reports that MCP servers are unstable on Windows, with connection success being non-deterministic across sessions. A clear bug for the Windows/MCP user segment with high reproducibility details.

## 4. Key PR Progress (Top 10)

1.  **#4639 [fix(acp): drop discontinued Qwen OAuth method]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4639)
    **Status:** Open. This PR directly addresses the authentication deadlock in JetBrains by discontinuing the old `qwen-oauth` method, providing a fallback to valid methods. A critical maintainability fix.

2.  **#4403 [feat(core): add memory pressure monitor]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4403)
    **Status:** Closed. Implements a low-overhead monitor to handle memory pressure in long-running sessions, using cgroup-aware RSS/V8 heap data to evict cache entries. This is a major step toward long-session stability.

3.  **#4531 [fix(core): guard oversized resumed history sends]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4531)
    **Status:** Closed. Adds a hard guard to prevent oversized histories from being sent after compression, directly fixing the `Invalid string length` crash in issue #4363.

4.  **#4644 [fix(core,cli): replace full-history structuredClone with shallow/tail variants]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4644)
    **Status:** Open. Replaces deep clones of entire chat histories (up to 500+ turns) with shallow or tail variants to prevent OOM on resume. A highly targeted performance optimization.

5.  **#4649 [feat(core): inject context env vars into shell subprocesses]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4649)
    **Status:** Open. Implements a feature request (#4645) to inject `SESSION_ID`, `AGENT_ID`, and `PROMPT_ID` environment variables into subprocesses, enabling better tracing for scripts.

6.  **#4505 [fix(core): emit enable_thinking on DashScope when reasoning is disabled]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4505)
    **Status:** Closed. Fixes a bug where the `enable_thinking` signal for Qwen3 models was silently dropped. A critical fix for users who disable chain-of-thought in their workflow.

7.  **#4333 [feat(core): atomic write rollout for credentials, memory, config, JSONL]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4333)
    **Status:** Open. Implements Phase 2 of a durability initiative, replacing bare `fs.writeFile` calls with atomic helpers in all security-sensitive paths to prevent data corruption on crash.

8.  **#4563 [refactor(serve): extract DaemonWorkspaceService from AcpSessionBridge]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4563)
    **Status:** Open. A clean-up refactor to separate session-level and workspace-level logic in the daemon, unblocking further architectural improvements.

9.  **#4646 [feat(daemon): clamp oversized inline media on the prompt path]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4646)
    **Status:** Open. Adds a clamp for inline media (images/audio) exceeding 10 MB, replacing them with a placeholder to prevent blowing up request sizes and token budgets.

10. **#4647 [fix(clipboard): use platform-native tools for image paste on Linux]**
    [Link](https://github.com/QwenLM/qwen-code/pull/4647)
    **Status:** Open. Fixes clipboard image paste on WSL2+Wayland by replacing the X11-dependent native module with `wl-paste`/`xclip`. Closes two long-standing issues (#3517, #2885).

## 5. Feature Request Trends

- **Smart Model Routing:** Multiple requests (e.g., #4640) call for a feature that routes simple tasks to local models and complex ones to powerful cloud APIs. This reflects a strong community desire for cost and latency optimization.
- **Automatic Memory Diagnostics:** Users are asking for automated crash documentation (#4651), showing a need for better self-service debugging of OOM errors.
- **Simpler JetBrains Authentication:** There is a clear trend toward bypassing the mandatory OAuth for JetBrains IDEs, with users asking for a simple API key flow (#3511) or reporting that the existing flow is broken (#4493).
- **Context-Aware SubAgent Scripts:** Feature #4645 (now landed in PR #4649) highlights a growing use case: users want their scripts to be aware of their session/agent context for observability.

## 6. Developer Pain Points

- **Authentication Hell:** Authentication remains the single biggest pain point, especially for JetBrains users. Deadlocks ("stuck in redirect loop," #4493), usage of discontinued OAuth (#4637), and configuration errors (401s, #3757) are top frustrations.
- **OOM and Long-Session Instability:** The community is actively suffering from memory-related crashes in long sessions, leading to data loss (#4363, #4651). While fixes are in progress, the frequency shows this is a high-impact area.
- **JetBrains/Local LLM Incompatibility:** The inability to use local models (Ollama) with IntelliJ 2026.1 is a notable regression ( #2724 ), blocking a key use case for power users.
- **CLI Update & Installation Friction:** Auto-update failures due to permission issues on macOS (#4627) and the inability to disable UI elements (loading tips, #4642) are minor but persistent quality-of-life issues for CLI users.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

Here is the **DeepSeek TUI Community Digest** for 2026-05-31.

*Note: The project has been officially renamed from `DeepSeek-TUI` to **CodeWhale**. All references below use the new canonical repository name `Hmbown/CodeWhale`.*

---

# DeepSeek TUI (CodeWhale) Community Digest — 2026-05-31

**Project:** [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI) (Canonical name: **CodeWhale**)

## Today’s Highlights
The community is focused on two major themes: **Chinese-market expansion** (localized web search, platform-aware UX) and **cache-maximalism** (systematic KV-cache stability). A flurry of merged PRs this week has introduced a durable SlopLedger for tracking architectural residue, a `hunt`-based recovery vocabulary replacing the old goal system, and multiple new API provider integrations (Volcengine, Baidu AI Search). However, several high-priority bugs remain open, including sub-agent MCP tool inheritance and TUI layout corruption on long outputs.

## Releases
No new releases in the last 24 hours. The latest stable version is **v0.8.47** (published 2026-05-27).

## Hot Issues (Top 10)
1.  **[#2353] [Bug] Memory function not working despite correct config** `[CLOSED]`
    - **Why it matters:** Users reported that adding `[memory] enabled = true` to `config.toml` did not activate memory, causing frustration. The 8 comments indicate the bug was tricky because environment variable overrides (`DEEPSEEK_MEMORY=on`) conflicted with the config file setting.
    - **Reaction:** High engagement; closure suggests a patch was merged, but community requested clearer documentation.
    - [Issue #2353](https://github.com/Hmbown/CodeWhale/issues/2353)

2.  **[#755] Chinese-market improvements tracker** `[OPEN]`
    - **Why it matters:** This is the master tracking issue for platform-aware keybindings (Mac Alt→Opt), Chinese web-search backends, and AgentScope harness integration. With 3 👍, it’s the most-voted open feature request.
    - **Reaction:** Community actively linking new Chinese-market bugs (like #1901) back to this issue.
    - [Issue #755](https://github.com/Hmbown/CodeWhale/issues/755)

3.  **[#2247] Support custom DeepSeek-compatible API providers** `[CLOSED]`
    - **Why it matters:** Users wanted to use third-party DeepSeek compatible models or local deployments. The 5 comments show strong demand for flexibility beyond the official API.
    - **Reaction:** Feature was implemented; closure likely means a directive to integrate with the new Volcengine provider (PR #1993).
    - [Issue #2247](https://github.com/Hmbown/CodeWhale/issues/2247)

4.  **[#2127] Slop Ledger: make architectural residue visible** `[CLOSED]`
    - **Why it matters:** A v0.9.0 design issue to track untracked technical debt left by agents (compatibility shims, dead paths). This is foundational for autonomous reliability.
    - **Reaction:** Merged via PR #2161; community discussion centered on defining “what counts as slop”.
    - [Issue #2127](https://github.com/Hmbown/CodeWhale/issues/2127)

5.  **[#2374] Terminal rendering corruption** `[CLOSED]`
    - **Why it matters:** Users reported that after continuous use, the TUI output became garbled (overlapping text, broken scrolling). This affects daily workflow for heavy users.
    - **Reaction:** 3 comments; the bug was quickly replicated and fixed.
    - [Issue #2374](https://github.com/Hmbown/CodeWhale/issues/2374)

6.  **[#2362] Sub-agents cannot use MCP tools** `[OPEN]`
    - **Why it matters:** A fundamental limitation: child agents spawned via `agent_open` lose access to MCP tools (Brave Search, Tavily). This breaks the agent-fanout pattern.
    - **Reaction:** Active discussion (3 comments) with workarounds suggested but no fix yet.
    - [Issue #2362](https://github.com/Hmbown/CodeWhale/issues/2362)

7.  **[#2303] `allow_shell` default false blocks `exec_shell` but not `task_shell_start`** `[CLOSED]`
    - **Why it matters:** A security bypass: the `allow_shell` gate was intended to block shell commands, but `task_shell_start` ignored it. This is a release-blocker for security-conscious users.
    - **Reaction:** Quick recognition and fix merged.
    - [Issue #2303](https://github.com/Hmbown/CodeWhale/issues/2303)

8.  **[#1901] Cost display inconsistency: USD in config, CNY in UI** `[CLOSED]`
    - **Why it matters:** For zh-Hans users, the footer showed CNY costs, but `/config` still displayed `cost_currency = usd`. This undermined trust in billing transparency.
    - **Reaction:** Part of the Chinese-market improvements; merged quickly.
    - [Issue #1901](https://github.com/Hmbown/CodeWhale/issues/1901)

9.  **[#2230] Terminal background image lost when opening TUI** `[CLOSED]`
    - **Why it matters:** Aesthetics issue: when launching the TUI from a new terminal tab, the terminal’s background image was replaced by a solid color.
    - **Reaction:** 3 comments; considered low impact but fixed.
    - [Issue #2230](https://github.com/Hmbown/CodeWhale/issues/2230)

10. **[#2309] `/statusline` picker hides undiscovered options** `[OPEN]`
    - **Why it matters:** The picker only shows items already in the config, making new status-line chips invisible. This breaks discoverability for new users.
    - **Reaction:** Low engagement but a clear UX design issue.
    - [Issue #2309](https://github.com/Hmbown/CodeWhale/issues/2309)

## Key PR Progress (Top 10)
1.  **[#2392] Stabilize project-context pack ordering** `[OPEN]`
    - **Description:** Replaces lexical sorting with explicit ordering (README > config > source > directories > other), normalizing Windows/Unix path separators.
    - **Why it matters:** Ensures deterministic cache keys across platforms, crucial for cache hit rates.
    - [PR #2392](https://github.com/Hmbown/CodeWhale/pull/2392)

2.  **[#2391] Track cache warmup keys** `[OPEN]`
    - **Description:** Adds a `CacheWarmupKey` covering provider, model, base URL, static prefix, tool catalog, project pack, and skills hashes.
    - **Why it matters:** Makes cache inspection reliable; `/cache inspect` now shows whether warmup matches the current session.
    - [PR #2391](https://github.com/Hmbown/CodeWhale/pull/2391)

3.  **[#2388] Stop compacting tool outputs on session save/load** `[CLOSED]`
    - **Description:** Removes `compact_session_tool_outputs` from save/load paths to preserve message fidelity for KV-cache hits on resume.
    - **Why it matters:** Fixes a cache-thrashing bug where compaction broke cache continuity across sessions.
    - [PR #2388](https://github.com/Hmbown/CodeWhale/pull/2388)

4.  **[#2389] Show intent summary before file approval prompt** `[OPEN]`
    - **Description:** When the model invokes write/modify/delete tools, its preceding text is extracted as an "intent summary" and displayed in the approval view.
    - **Why it matters:** Implements #2381; gives users context for why a change is being made before reviewing the diff.
    - [PR #2389](https://github.com/Hmbown/CodeWhale/pull/2389)

5.  **[#2283] Recover from stalled in-progress turns** `[CLOSED]`
    - **Description:** Fixes watchdog blind spot where a turn stuck in `"in_progress"` left `is_loading` permanently `true`. Adds a 5-minute stall timeout.
    - **Why it matters:** Resolves a common hang scenario for long-running agent sessions.
    - [PR #2283](https://github.com/Hmbown/CodeWhale/pull/2283)

6.  **[#1993] Add Volcengine provider** `[CLOSED]`
    - **Description:** Adds Volcano Engine Ark as a provider for DeepSeek-V4-Pro and Flash via Coding API.
    - **Why it matters:** First third-party provider integration; directly addresses #2247 (custom API support).
    - [PR #1993](https://github.com/Hmbown/CodeWhale/pull/1993)

7.  **[#2387] Add `/purge` slash command for context pruning** `[CLOSED]`
    - **Description:** New `/purge` command lets the agent surgically remove or rewrite conversation history via a `purge_context` tool call.
    - **Why it matters:** Critical for long sessions where context window fills with noise.
    - [PR #2387](https://github.com/Hmbown/CodeWhale/pull/2387)

8.  **[#2306] Rename `/goal` → `/hunt` with HuntVerdict + trophy cards** `[CLOSED]`
    - **Description:** Implements #2092: renames goal system to hunt vocabulary (quarry → verdict), adds trophy cards for session recovery.
    - **Why it matters:** Ships the recovery-state vocabulary needed for interruptible, resumable agent work.
    - [PR #2306](https://github.com/Hmbown/CodeWhale/pull/2306)

9.  **[#1968] Restore mobile control page** `[CLOSED]`
    - **Description:** Adds `codewhale serve --mobile` as a lightweight mobile/LAN entry point over the runtime HTTP/SSE API.
    - **Why it matters:** Re-enables mobile access to the TUI after the v0.8.41 rebrand.
    - [PR #1968](https://github.com/Hmbown/CodeWhale/pull/1968)

10. **[#2161] Add durable SlopLedger** `[CLOSED]`
    - **Description:** Implements #2127: a durable store that makes invisible architectural residue visible and queryable across agent sessions.
    - **Why it matters:** Critical for autonomous agents to track and clean up their own technical debt.
    - [PR #2161](https://github.com/Hmbown/CodeWhale/pull/2161)

## Feature Request Trends
- **Custom API provider support:** Strong demand (Issues #2247, #2337) for plugging in third-party DeepSeek compatible endpoints. Volcengine (#1993) and Baidu AI Search (#2371) integrations are direct responses.
- **Chinese-market localization:** Multiple requests for platform-aware keybindings (#755), CNY cost display (#1901), and China-accessible web search backends (Baidu AI Search in #2371).
- **Cache-maximalism:** Users want systematic prefix-cache stability (#2264) and better diagnostics (#2124, #2391). The `cache` module is seeing heavy PR activity.
- **Internationalization (i18n):** Vietnamese localization added (#2358), with users requesting more languages and better visual differentiation of user vs. AI messages (#1672).
- **Agent reliability:** Requests for session recovery (#2127, #2082), stall detection (#2283), and context pruning (/purge in #2387) are driving core architecture changes.

## Developer Pain Points
- **Configuration confusion:** The memory-enable bug (#2353) and currency display inconsistency (#1901) show that config system documentation lags behind implementation, causing user frustration.
- **Security bypasses:** The `allow_shell` gate being incomplete (#2303) and shell commands failing due to missing controlling terminal (#2372) are high-severity issues for power users running automation scripts.
- **Sub-agent limitations:** Child agents not inheriting MCP tools (#2362) and fanout causing TUI saturation (#2211) are blocking users who rely on multi-agent workflows.
- **Terminal/TUI rendering:** Garbled output after continuous use (#2374), status line covering output (#2244), and background image loss (#2230) point to an ongoing battle with terminal emulator compatibility.
- **Cache stability:** Users are frustrated by cache misses due to tool output compaction (#2388) and misleading warmup/inspect diagnostics (#2393). The community is actively pushing for deterministic, byte-stable caching.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*