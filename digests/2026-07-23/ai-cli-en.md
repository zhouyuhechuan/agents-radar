# AI CLI Tools Community Digest 2026-07-23

> Generated: 2026-07-23 02:04 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report — 2026-07-23

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem shows a mature but fractious landscape. Seven major tools — Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI (CodeWhale) — are all actively shipping releases, but community sentiment reveals systemic reliability problems across the board. Persistent issues around MCP lifecycle management, subagent resource leaks, cross-platform stability (especially Windows), and authentication regressions dominate developer pain points. The strongest signal is a converging demand for multi-agent cost control and per-agent model selection, indicating the ecosystem is moving beyond single-model, single-agent workflows toward composable, cost-optimized agent architectures.

## 2. Activity Comparison

| Tool | Hot Issues (today) | Key PRs (today) | Releases (last 24h) | Community Engagement Level |
|---|---|---|---|---|
| Claude Code | 10 (50 active) | 10 | v2.1.218 (stable fix) | High — 9-month bug #39523 boiling, 6 docs issues filed by single contributor |
| OpenAI Codex | 10 | 10 | 4 Rust v0.146.0-alpha releases | Very High — #28969 (151 👍) shows strong stakeholder demand for timeouts |
| Gemini CLI | 10 | 10 | v0.52.0 stable + nightly + preview | Moderate — 2 long-standing agent bugs (#22323, #21409) dominate |
| GitHub Copilot CLI | 10 | 1 (likely spam) | 3 patch releases (v1.0.74-1/2/3) | Moderate — low PR velocity, but regressions being addressed |
| Kimi Code CLI | 5 | 3 | None | Low — small community, 2 critical bugs surfaced today |
| OpenCode | 10 | 10 | pr-38252-videos (asset only) | High — subscription outage (#38218) with global duplicates, active triage |
| Pi | 10 | 10 | None (latest stable v0.80.7) | High — 29 PRs + 50 issues touched, but many closed with "no-action" |
| Qwen Code | 10 | 10 | Internal prerelease only | Moderate — side-query thinking bug fixed, CI red blocking PRs |
| DeepSeek TUI (CodeWhale) | 10 | 10 | None (v0.9.1 integration) | High — 17-discussion epic on command-boundary refactor |

**Key observations:**
- **Top engagement:** OpenAI Codex (#28969 with 151 reactions), OpenCode (#6231 with 185 reactions on model auto-discovery).
- **Highest release velocity:** OpenAI Codex (4 alpha releases), GitHub Copilot CLI (3 patches), Claude Code (1 stable).
- **Worst stability signals:** Claude Code (permissions bypass open 9+ months, Task/Todo regression), OpenCode (global subscription outage), Pi (multiple “no-action” closures on active bugs).

## 3. Shared Feature Directions

Several requirements appear across two or more tool communities, indicating converging industry needs:

**Per-Agent / Sub-Agent Model Selection (4 tools)**
- Kimi Code (#2533): Request to run sub-agents on different models for cost-tiered workflows.
- Gemini CLI (#21968): Users want models to self-select and invoke custom skills without explicit prompting.
- GitHub Copilot CLI (#4218): Users want to constrain which models Auto mode can pick for cost predictability.
- Claude Code (#80359): Model‑specific plan modes (“fableplan” analogous to “opusplan”).

**Subagent Billing & Usage Transparency (3 tools)**
- GitHub Copilot CLI (#4207): Per-subagent AI credit usage breakdown in `/usage`.
- Claude Code: Task/Todo tool availability gating confuses account-level billing expectations.
- Kimi Code (#2533): Implicit cost-awareness through model-tier selection.

**MCP Lifecycle & Resource Leak Fixes (4 tools)**
- OpenAI Codex (#12491, #26984): Zombie processes, pipe-fd exhaustion, 37 GB memory leaks.
- GitHub Copilot CLI (#4163): Zombie child processes on Linux (~2/min accumulation).
- Claude Code (#80404): Event-loop starvation causing 200% CPU spin after sleep/resume.
- Gemini CLI: Subagent hang and false-success bugs (#22323, #21409).

**Cross-Platform Stability — Windows Specific (4 tools)**
- GitHub Copilot CLI (#4222, #4217, #4219): React render loop, exit crash, notification crash.
- Kimi Code (#2532): Unicode encoding crash on Chinese-locale Windows.
- Qwen Code (#6577): Alt+V paste bug in Windows Terminal.
- DeepSeek TUI (#4685): Windows installer overwrites user PATH instead of appending.

**Agent Orchestration & Session Management (3 tools)**
- Claude Code (#71726): Mid-task message injection parity between desktop and CLI.
- OpenAI Codex (#34845): Multi-agent mode persistence in world state.
- Pi (#6967, #6916): Session metadata exposure to bash tools and AgentHarness execution tools.

**Prompt/Context Optimization (2 tools)**
- DeepSeek TUI (#4704): “Context Diet” epic to audit and shrink model-facing prompts.
- Pi (#6621): Prevent cache invalidation from dynamic system prompts on unified memory devices.

**AST-Aware Code Understanding (2 tools)**
- Gemini CLI (#22745): Assess AST-aware file reads and codebase mapping for precision.
- Claude Code: Indirectly through skill/subagent documentation gaps filed today.

## 4. Differentiation Analysis

### Feature Focus

| Tool | Core Differentiator | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Deep tool ecosystem (Fable, plugins, subagent skills) | Full-stack devs, power users | Heavy MCP plugin architecture, multi-model orchestration, background subagents |
| **OpenAI Codex** | Rust performance, Guardian review, plugin catalog | Performance-sensitive teams, security-conscious | Rust-native CLI, Guardian security model, bundled plugin catalog |
| **Gemini CLI** | Google ecosystem, enterprise eval infrastructure | Google Cloud developers, enterprise | Triage orchestrator, AST-aware tooling, component-level evaluations |
| **GitHub Copilot CLI** | GitHub integration, sandboxed execution | GitHub-centric teams, enterprise | Built-in sandbox, ACP mode, Auto mode model pool |
| **Kimi Code CLI** | Moonshot API, Chinese market | Asian developers, Moonshot API users | Minimalist, provider-specific optimizations |
| **OpenCode** | Local model support, V2 architecture | Hobbyists, local-first developers | OpenAI-compatible provider discovery, V2 server architecture |
| **Pi** | Provider diversity, constrained sampling | Advanced users, multi-provider workflows | 10+ providers, OAuth flows, prompt caching optimization |
| **Qwen Code** | Alibaba Cloud integration, enterprise channels | Chinese enterprises, Alibaba ecosystem | ARMS telemetry, workspace channel management (DingTalk/WeCom/Feishu) |
| **DeepSeek TUI (CodeWhale)** | Theming, skills management, rapid iteration | Enthusiasts, customizable workflows | Bundled skill packs, theme system, “Context Diet” optimization |

### Key Technical Divergences
- **Security approach:** OpenAI Codex relies on Guardian review with model-limit enforcement; Claude Code has a long-unresolved `bypassPermissions` bug; Gemini CLI just patched variable expansion bypass; GitHub Copilot CLI offers sandboxed execution.
- **Provider strategy:** Pi supports widest provider diversity via OAuth; Kimi Code is Moonshot-focused with leakage bugs to third-party APIs; Qwen Code is tightly integrated with Alibaba services.
- **Architecture:** OpenCode is moving toward V2 server architecture with dynamic model loading; Codex is Rust-native for performance; CodeWhale uses a TUI-first approach with bundled skill packs.
- **Community openness:** DeepSeek TUI has the most active community relative to team size (29 PRs/day); Claude Code and Codex have large communities but high frustration from unresolved long-standing bugs.

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
- **DeepSeek TUI (CodeWhale):** 29 PRs and 50 issues touched in 24 hours. v0.9.1 integration merging unified skills, theming, release blockers. Small team but high community engagement. Risk: rapid pace may leave quality debt.
- **OpenAI Codex:** 4 Rust alpha releases and 10 PRs today. Active automated patch infrastructure (copyberry). Large community (151 👍 on a single feature request). Mature but alpha-stage Rust rewrite keeps momentum.
- **Pi:** 29 PRs touched, strong feature velocity (OpenRouter OAuth, StepFun providers, AgentHarness). However, 50 issues touched with many “no-action” closures suggests triage bandwidth strain.

### Stable but Frustrated
- **Claude Code:** Regular stable releases (v2.1.218), but 9-month permissions bypass bug (#39523) and Task/Todo regression (#80210, #80213) erode user trust. Documentation gaps receiving attention but not yet resolved. Community engagement is high but negative.
- **OpenCode:** Active triage (many closed issues), but global subscription outage (#38218) is a critical P0. V2 server performance issues (#36677) suggest architectural debt. Strong feature requests (model auto-discovery with 185 👍) indicate unmet core needs.

### Moderate Activity
- **Gemini CLI:** 3 releases today including stable. Security infrastructure hardening (GHSA patch). Community engagement is moderate; the two persistent agent bugs (#22323, #21409) are top pain points but not generating high-volume discussion.
- **GitHub Copilot CLI:** Low PR velocity (1 PR, likely spam) but 3 patch releases. Regressions being patched quickly. Community requests are pragmatic (model control, billing transparency).
- **Qwen Code:** Active but smaller community. Internal CI infrastructure getting heavy investment (Fleet Shepherd, autofix retry logic). Region-specific (Chinese enterprise).
- **Kimi Code CLI:** Smallest community with only 5 issues today. Critical bugs (#2534, #2532) but low engagement. Likely lower adoption.

## 6. Trend Signals

### Strong Signal: Multi-Agent Cost Control
The convergence of per-agent model selection requests across Kimi Code, Gemini CLI, Copilot CLI, and Claude Code signals a maturing understanding that different agent tasks have different cost/value profiles. Developers want to route simple tasks to cheap/fast models and complex tasks to capable models, all within the same session. This implies:
- CLI tools need model routing layers that are transparent to users.
- Billing telemetry must be per-agent, not aggregated.
- Session orchestration must support heterogeneous model pools.

### Strong Signal: MCP Lifecycle Management Is Unsolved
Four of nine tools report zombie processes, file-descriptor leaks, or memory balloons from MCP servers. This is a systemic architecture problem: the CLI tool community standardized on MCP without sufficiently standardizing its lifecycle contracts (shutdown, reaping, resource limits). Expect:
- Industry push for MCP lifecycle specification (SIG or working group).
- Tool-specific retry/abort layers (as Pi just did with its abortable retry helper).
- Sandboxed MCP execution in response to security bugs (variable expansion bypass in Gemini).

### Emerging Signal: “Context Diet” as a Feature Category
DeepSeek TUI’s v0.9.2 epic (#4704) explicitly calls for auditing and shrinking model-facing prompts. Pi (#6621) addresses cache invalidation from dynamic prompts. As context windows grow but costs remain, optimizing prompt payloads becomes a competitive advantage. Expect:
- Automated prompt compression / deduplication features in CLI tools.
- Caching strategies that account for dynamic content (date/time, session state).
- Model-specific prompt tuning to maximize cache reuse across tool families (e.g., Anthropic vs. OpenAI).

### Emerging Signal: Windows Is the Achilles’ Heel
Every major tool except Pi and Gemini has at least one Windows-specific stability bug in today’s reports. Path overwrites (CodeWhale), Unicode crashes (Kimi), render loops (Copilot CLI), event-loop spins (Claude Code), and notification crashes (Copilot CLI). Windows developer adoption requires tool teams to invest in:
- Windows-specific CI/CD gates.
- Native Windows file system (long path support, Unicode) and terminal (VT sequence) testing.
- Integration with WSL and remote containers (several bugs around SSH/remote contexts).

### Persistent Pain: Trust in Agent Outputs
- **False success reports:** Gemini subagent (#22323) reports GOAL after MAX_TURNS; Claude Code Fable 5 (#80348) claims “verified, copy changed” against user’s correct “no change.”
- **False positive safety checks:** Codex CLI (#28015) blocking ordinary git operations; Copilot CLI (#4221, #4220) misclassifying `git log -L` arguments as directory paths.
- **File corruption:** OpenCode subagent (#38356) writing null bytes to HTML files.

These erode developer confidence in autonomous agent workflows. The industry needs:
- Confidence scoring / uncertainty signals in agent outputs.
- Mandatory human-in-the-loop for destructive operations (already present in some tools but bypassable).
- Transparent audit trails for agent decision traces.

### Weak Signal: Terminal UI Renaissance
CodeWhale’s theming system (`/uwu`, `/debt` aliases, resizable work chrome) and OpenCode’s TUI syntax migration (#38397) suggest a shift toward richer terminal experiences. Developers are asking for scrollable sidebars, timestamps on tool calls, and FPS limiters for remote desktop performance. The terminal is not dying; it’s being redesigned for multi-agent, multi-model workflows.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-07-23 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### 1. **skill-creator: run_eval.py fix** (#1298)
**Functionality:** Repairs the evaluation pipeline (`run_eval.py` → `run_loop.py` → `improve_description.py`) that consistently reports 0% recall for all skill descriptions—effectively optimizing against noise. Fixes include installing the eval artifact as a real skill, Windows stream reading, trigger detection, and parallel worker handling.
**Discussion highlights:** References issue #556 with 10+ independent reproductions. This is a blocker for any workflow relying on the description-optimization loop. The PR has received wide community attention (50 total PRs ranked by comments).
**Status:** [Open](https://github.com/anthropics/skills/pull/1298)

### 2. **document-typography skill** (#514)
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.
**Discussion highlights:** Addresses a universal pain point—typographic defects affect every document Claude generates, yet users rarely request fixes proactively. Strong community resonance for a "hygiene" skill.
**Status:** [Open](https://github.com/anthropics/skills/pull/514)

### 3. **ODT skill** (#486)
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods) including template filling and ODT-to-HTML parsing.
**Discussion highlights:** Targets the LibreOffice/ISO-standard document ecosystem, a significant gap given Claude's existing DOCX and PDF skills.
**Status:** [Open](https://github.com/anthropics/skills/pull/486)

### 4. **frontend-design skill improvement** (#210)
**Functionality:** Revises existing frontend-design skill for clarity, actionability, and internal coherence, ensuring every instruction is executable within a single conversation.
**Discussion highlights:** Raises the broader question of skill quality standards and the need for actionable rather than verbose instructions.
**Status:** [Open](https://github.com/anthropics/skills/pull/210)

### 5. **skill-quality-analyzer & skill-security-analyzer** (#83)
**Functionality:** Meta-skills that evaluate other skills across five dimensions (Structure, Documentation, Clarity, Security, Testing) and perform security analysis including prompt injection, data validation, and dependency scanning.
**Discussion highlights:** Proposes a community quality assurance layer. Addresses the lack of review scaffolding for the growing skills marketplace.
**Status:** [Open](https://github.com/anthropics/skills/pull/83)

### 6. **pyxel skill** (#525)
**Functionality:** Integrates with the Pyxel retro game engine MCP server, covering the full workflow from writing code to iteration via screenshot capture.
**Discussion highlights:** Represents the gaming/creative coding direction. Created by the Pyxel maintainer (kitao), lending authority.
**Status:** [Open](https://github.com/anthropics/skills/pull/525)

### 7. **color-expert skill** (#1302)
**Functionality:** A self-contained color expertise skill covering naming systems (ISCC-NBS, Munsell, RAL), color spaces with usage guidance (OKLCH/OKLAB for scales vs. gradients), and accessibility references.
**Discussion highlights:** Technically dense skill addressing a common gap in LLM color knowledge. Recently updated (2026-07-21), suggesting active refinement.
**Status:** [Open](https://github.com/anthropics/skills/pull/1302)

### 8. **testing-patterns skill** (#723)
**Functionality:** Comprehensive testing guidance: Trophy model, unit testing (AAA pattern, edge cases), React component testing, integration, and E2E patterns.
**Discussion highlights:** Covers a full testing philosophy rather than isolated patterns. Indicates demand for structured quality assurance in LLM outputs.
**Status:** [Open](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

### 🔴 Critical: Skill-Creator Tooling Stability
**Issue #556** (12 comments, 7 👍) and **#1169** (3 comments) report that `run_eval.py` consistently achieves 0% trigger rate across all queries, making the description-optimization loop non-functional. **Issue #1061** (3 comments, 2 👍) details Windows compatibility failures (subprocess PATHEXT, cp1252 encoding, select-on-pipes). The skill-creator pipeline is effectively broken on Windows and yields false results on Linux/macOS. This is the highest-urgency concern.

### 🔴 High: Trust & Security Boundaries
**Issue #492** (43 comments, 2 👍) identifies that community skills are distributed under the `anthropic/` namespace, creating trust boundary vulnerabilities where users may grant elevated permissions to unofficial skills. This is the most-commented issue in the repository, indicating strong community unease with the current distribution model.

### 🟡 Medium: Organizational Skill Sharing
**Issue #228** (14 comments, 7 👍) requests org-wide skill sharing via direct links or a shared library, versus the current manual file-transfer workflow. Related to team adoption friction.

### 🟡 Medium: Document Format Expansion
ODT (PR #486) and improved DOCX handling (PR #541) point to demand for office document ecosystem parity. PDF fixes (PR #538) highlight the gap between file-naming conventions and case-sensitive filesystems.

### 🟢 Emerging: Meta-Quality & Governance
**Issue #412** (proposal: agent-governance) and PR #83 (skill-quality-analyzer) signal interest in a quality/review layer for the skills ecosystem itself. **Issue #1385** proposes a three-gate reasoning quality pipeline.

---

## 3. High-Potential Pending Skills

These PRs have active comment threads and address clear community pain points:

| PR | Skill | Why It's High-Potential |
|----|-------|------------------------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator run_eval fix | **The blocker** for the entire optimization workflow. Multiple maintainers contributing fixes (MartinCajiao, Polluelo978, joshuawowk, gstreet-ops, Mr-Neutr0n). |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit (v1.3.0) | Novel approach: mechanical file verification + four-dimension reasoning audit in damage-severity order. Universal applicability. |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert | Recently updated (2026-07-21), technically dense, authored by meodai. |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | Comprehensive testing stack coverage. Complements the quality/safety trend. |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill-creator Windows fix | Direct follow-on from issue #1061. Multiple independent reproductions. |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | Universal applicability—every document user benefits. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill-creator tooling (fixing the 0% recall bug that paralyzes description optimization) combined with trust-boundary security reforms, before expanding into new domains like document typography, ODT support, and testing-pattern skills.**

---

# Claude Code Community Digest – 2026-07-23

## Today's Highlights
Version **v2.1.218** ships a critical fix: `/code-review` now runs as a background subagent, no longer filling conversation history and keeping stacked slash commands as its review target. Meanwhile, the community continues to rally around a 9‑month‑old permissions bypass bug (#39523) and a growing number of users report that the new **Task/Todo tools** have suddenly stopped being exposed in CLI sessions—two separate issues (#80210, #80213) with similar symptoms suggest a server‑side gating regression. A flurry of documentation gap reports (six filed by a single contributor) also signals that the skill/subagent/workflow docs need urgent polish.

## Releases
**v2.1.218** – [View release](https://github.com/anthropics/claude-code/releases/tag/v2.1.218)
- `/code-review` now runs as a background subagent, so review work no longer fills your conversation and keeps stacked slash commands as its review target.
- Added screen‑reader announcements of deleted text for word and line deletions (`Option+Delete`, `Ctrl+W`, `Cmd+Backspace`).

## Hot Issues (10 selected from 50 active)

1. **[#80002 – macOS: Claude Desktop never dispatches tools/call to Filesystem extension](https://github.com/anthropics/claude-code/issues/80002)**  
   *56 comments, +25* – A show‑stopper for desktop users relying on the first‑party Filesystem MCP server. `tools/list` succeeds but no `tools/call` appears in any log. High visibility.

2. **[#39523 – [META] Bypass permissions mode is fundamentally broken](https://github.com/anthropics/claude-code/issues/39523)**  
   *33 comments, +18* – 9‑month trail, 12+ duplicates. The `bypassPermissions` flag simply does not work in many scenarios. Still unresolved on v2.1.84+ – community frustration is boiling.

3. **[#50842 – Chrome MCP silently denies non‑pre‑approved domains](https://github.com/anthropics/claude-code/issues/50842)**  
   *13 comments, +6* – No user‑facing approval path exists. Users cannot navigate to any domain not pre‑approved—a security UX disaster for browser automation.

4. **[#71726 – Desktop app: inject queued messages mid‑task between tool calls (CLI parity)](https://github.com/anthropics/claude-code/issues/71726)**  
   *9 comments, +16* – CLI users can “steer” Claude mid‑turn; desktop users must wait for a full turn to finish. Popular feature request with strong demand.

5. **[#78933 – Remote Control never connects: “Cannot read properties of undefined”](https://github.com/anthropics/claude-code/issues/78933)**  
   *8 comments* – Desktop app `/remote-control` fails with a cryptic getter error. Windows users affected.

6. **[#77966 – OAuth loop on Linux/IntelliJ: state parameter dropped](https://github.com/anthropics/claude-code/issues/77966)**  
   *7 comments, +6* – Login flow redirects to “sign in again” infinitely. Affects Linux and IntelliJ platform users.

7. **[#80348 – Fable 5: “verified, copy changed” against user’s correct “no change”](https://github.com/anthropics/claude-code/issues/80348)**  
   *3 comments* – Fable 5 confidently claimed verification of a change that was never made, and told the user their correct observation was wrong. Trust‑eroding hallucination pattern.

8. **[#80213 – Task tools unavailable in top‑level CLI despite CLAUDE_CODE_ENABLE_TASKS=true](https://github.com/anthropics/claude-code/issues/80213)**  
   *2 comments, +1* – Same account, same version – TaskCreate/TaskList/TaskUpdate work in desktop but vanish in CLI. Points to a client‑side capability negotiation bug.

9. **[#80210 – Task/Todo tools regressed around 2026‑07‑21; appears account‑gated](https://github.com/anthropics/claude-code/issues/80210)**  
   *1 comment, +3* – Tools stopped being exposed mid‑day; `todoFeatureEnabled` is true. Another symptom of the same gating regression.

10. **[#80404 – Event‑loop starvation causing ~200% CPU spin after hibernate/resume (Windows)](https://github.com/anthropics/claude-code/issues/80404)**  
    *0 comments* – High CPU consumption until self‑termination after tens of minutes. Likely the Windows analog of a previously closed macOS bug (#62308). Impacts workstation reliability.

## Key PR Progress (10 items)

1. **[#18217 – feat(plugins): add /planwith command for inline plan mode prompts](https://github.com/anthropics/claude-code/pull/18217)**  
   *Closed* – Would allow `plan` to accept inline arguments, removing the two‑step toggle‑then‑type workflow. Not merged yet but a long‑standing design discussion.

2. **[#80353 – docs(gcp): stop on checksum mismatch](https://github.com/anthropics/claude-code/pull/80353)**  
   *Open* – Hardens the GCP gateway deployment sequence to halt when binary checksum verification fails. Small but important reliability improvement.

3. **[#80326 – Add account profiles plugin](https://github.com/anthropics/claude-code/pull/80326)**  
   *Open* – Experimental plugin for managing isolated `CLAUDE_CONFIG_DIR` environments per account (personal / work / client). Addresses a common multi‑account pain point.

4. **[#80294 – docs: fix 1 broken link(s) via archive.org](https://github.com/anthropics/claude-code/pull/80294)**  
   *Open* – Automated fix for a dead npmjs link using Wayback snapshots. Part of an ongoing LinkMedic clean‑up.

5. **[#80241 – fix: Console scrolling top of history when claude adds text](https://github.com/anthropics/claude-code/pull/80241)**  
   *Open* – Autonomous PR fixing a scroll‑to‑top annoyance during streaming output.

6. **[#80229 – docs: fix 1 broken link(s) via archive.org](https://github.com/anthropics/claude-code/pull/80229)**  
   *Open* – Another Wayback fix for a dead npmjs link.

7. **[#80196 – fix: Auto‑compact never triggers despite “100% context used”](https://github.com/anthropics/claude-code/pull/80196)**  
   *Open* – Bug fix: auto‑compact would not fire even when context was full, leading to unnecessary manual intervention.

8. **[#80195 – fix: Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/pull/80195)**  
   *Open* – Addresses a bug where Max plan users hit usage limits immediately after starting a session.

9. **[#80112 – Make devcontainer firewall init resilient to DNS resolution failures](https://github.com/anthropics/claude-code/pull/80112)**  
   *Open* – Prevents a single transient DNS failure from aborting the entire firewall setup in devcontainers.

10. **[#80008 – Add twilight plugin: spec‑first design/implement skills](https://github.com/anthropics/claude-code/pull/80008)**  
    *Open* – Demonstrates a strategy pairing design, implement, and focus‑stack to unlock durable, multi‑step functionality. Not intended as an immediate merge but as a technical demo.

## Feature Request Trends
From this week’s issues, the community is asking for:
- **Desktop / CLI parity for mid‑task steering** (#71726) – the ability to inject messages while Claude is working, without waiting for a turn to finish.
- **Session lifecycle management** – marking background agents as “completed” or dismissing them from the agent view (#66202).
- **Model‑specific plan modes** – “fableplan” analogous to “opusplan” for token‑efficient planning tasks (#80359).
- **Task/Todo tool consistency** – users expect TaskCreate and friends to be available everywhere, not gated by account or platform.
- **Documentation completeness** – six separate “DOCS” issues filed today (#80394–#80399) highlight missing details on subagent naming, skill booleans, fast‑mode switching, and deep‑research invocation.

## Developer Pain Points
Several recurring frustrations stand out:
- **Permissions bypass broken for 9+ months** (#39523) – the single most upvoted meta‑bug. Developers who rely on `bypassPermissions` for CI or power‑user workflows have no working solution.
- **Silent failure modes in browser automation** (#50842) and **false verification from Fable 5** (#80348) erode trust in the model’s output accuracy.
- **Focus mode hides substantive answers** (#50894) – intended to hide tool logs, but the model often streams direct answers between tool calls that are then hidden.
- **Event‑loop and UI freezes** after sleep/resume (#80404, #80403) – impact workstation stability across macOS and Windows.
- **Task/Tool unavailability regressions** (#80210, #80213, #80401) – multiple users report tools vanishing mid‑session or never appearing, with no clear user action to restore them.
- **Documentation gaps** force developers to reverse‑engineer feature behavior (e.g., subagent naming colon restriction, `context: fork` running in background by default).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-23

## Today’s Highlights
Four Rust v0.146.0-alpha releases landed today, though no release notes were provided beyond version bumps. The community is grappling with several persistent MCP process‑leak bugs (zombie children, pipe‑fd exhaustion, 37 GB memory leaks) and a high‑profile request to disable the 60‑second auto‑resolve prompt. On the PR side, a steady stream of automated copyberry patches adds thread pinning, plugin catalog caching, and Guardian model limit handling, alongside a fix for preserving user input when MCP startup is interrupted.

## Releases
Four Rust alpha releases were published, all with the generic message “Release 0.146.0-alpha.*”. No further details are available from the provided data.

- [rust-v0.146.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.4)
- [rust-v0.146.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.3)
- [rust-v0.146.0-alpha.2](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.2)
- [rust-v0.146.0-alpha.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.1)

## Hot Issues
*(10 of the most active issues from the last 24 hours)*

1. **[#28969 – Add setting to disable auto-resolve in 60 seconds](https://github.com/openai/codex/issues/28969)**  
   *51 comments, 151 👍*  
   A widely supported request to give users control over the CLI’s automatic resolution prompt. Many developers find the timeout disruptive during complex reasoning sessions.

2. **[#12491 – MCP child processes not reaped → 1300+ zombies, 37 GB memory leak](https://github.com/openai/codex/issues/12491)**  
   *27 comments, 5 👍*  
   Long‑standing (Feb 2026) memory and process‑management bug in the GUI wrapper, still unresolved. Highlights a systemic issue with MCP lifecycle cleanup.

3. **[#21639 – Hooks no longer run after Codex Desktop update](https://github.com/openai/codex/issues/21639)**  
   *23 comments, 6 👍*  
   Regression in hook execution after an app update, affecting automation workflows. Community reports it persists across several CLI versions.

4. **[#16815 – WSL agent mode fails: AbsolutePathBuf deserialized without a base path](https://github.com/openai/codex/issues/16815)**  
   *22 comments, 13 👍*  
   Windows + WSL users blocked from using the Agent environment. The error appears on task creation, making the feature unusable for many Business plan subscribers.

5. **[#28015 – False positive cybersecurity safety check blocks normal repo maintenance](https://github.com/openai/codex/issues/28015)**  
   *22 comments, 3 👍*  
   Codex CLI repeatedly flags ordinary Git operations (e.g., hygiene tasks) as security risks, interrupting paid sessions. Users call for better distinction between security work and routine devops.

6. **[#27597 – IDE extension fails to load in VS Code Remote‑SSH](https://github.com/openai/codex/issues/27597)**  
   *16 comments, 4 👍*  
   Codex extension cannot initialise when connecting via Remote-SSH, while the standalone CLI works fine. Affects remote development setups.

7. **[#10599 – Way to configure location of worktrees](https://github.com/openai/codex/issues/10599)**  
   *16 comments, 66 👍*  
   Strong demand (66 upvotes) for customisable Git worktree paths. Currently Codex always creates worktrees under a hardcoded directory, causing clutter for power users.

8. **[#22428 – Windows sandbox setup refresh failed / CreateProcessAsUserW failed](https://github.com/openai/codex/issues/22428)**  
   *15 comments, 10 👍*  
   Sandbox execution on Windows 11 fails after a refresh attempt. One of several Windows‑specific sandbox stability reports.

9. **[#26984 – MCP stdio servers leak pipe fds + orphan children → EMFILE](https://github.com/openai/codex/issues/26984)**  
   *14 comments, 3 👍*  
   Cumulative file‑descriptor leak over long‑running sessions eventually crashes Codex with “Too many open files”. Related to the broader MCP lifecycle issues.

10. **[#29122 – Stable IDE extension ships prerelease CLI with under‑development “Code mode” silently active](https://github.com/openai/codex/issues/29122)**  
    *4 comments, 0 👍*  
    A critical report that the stable Visual Studio Code extension bundles a CLI alpha that enables a hidden “Code mode”, breaking long MCP calls and burning tokens. Despite low engagement, the impact is high for Plus users.

## Key PR Progress
*(10 significant pull requests merged or updated today)*

1. **[#34852 – Wake sleeping threads for queued agent mail](https://github.com/openai/codex/pull/34852)**  
   Idle threads with durable sleep now resume when agent mail arrives. Fixes a class of stuck‑state bugs in multi‑agent workflows.

2. **[#34851 – Use batch metadata for plugin app summaries](https://github.com/openai/codex/pull/34851)**  
   Loads app metadata through the authenticated batch API (batches of 100) for plugin read/install responses. Improves performance for users with many plugins.

3. **[#34850 – Disable image generation for Free‑plan accounts](https://github.com/openai/codex/pull/34850)**  
   Hides the `image_generation` tool for Free users, reducing confusion and unnecessary API calls.

4. **[#34849 – Cache remote plugin catalogs by scope](https://github.com/openai/codex/pull/34849)**  
   Disk‑caches global/user/workspace plugin catalogs with a 3‑hour TTL. Speeds up `plugin/list` and reduces load on the remote catalog service.

5. **[#34847 – Use Guardian model limits for review sessions](https://github.com/openai/codex/pull/34847)**  
   Ensures Guardian review uses the actual selected model’s context limits, not overrides from parent sessions. Prevents unexpected truncation during security reviews.

6. **[#34846 – Allow custom providers to opt into standalone web search](https://github.com/openai/codex/pull/34846)**  
   Adds a `supports_standalone_web_search` provider setting (defaults `false`). Opens web‑search tool use for custom Responses providers.

7. **[#34845 – Track multi‑agent mode in world state](https://github.com/openai/codex/pull/34845)**  
   Persists the effective multi‑agent mode in world state so it survives history changes without re‑emitting setup hints. Improves reliability of multi‑agent sessions.

8. **[#34840 – Add persisted thread pinning to the app server](https://github.com/openai/codex/pull/34840)**  
   Allows pinning/unpinning of threads using `thread/metadata/update` and exposes `isPinned` filters. Enables users to save important threads at the top of their list.

9. **[#34839 – Preserve user input when MCP startup is interrupted](https://github.com/openai/codex/pull/34839)**  
   Fixes a bug where interrupting a turn while MCP tools were still starting would lose the submitted user input. The input is now recorded in conversation history before starting tool setup.

10. **[#34835 – Track compaction time in turn profiles](https://github.com/openai/codex/pull/34835)**  
    Adds `compaction_ms` to turn analytics, measuring time spent in context compaction separately from idle time. Helps developers understand performance bottlenecks during long sessions.

## Feature Request Trends
The most‑requested improvements from recent issues include:

- **Configurable auto‑resolve timeout** (#28969) – A strong desire to turn off or extend the 60‑second automatic resolution, especially for complex plan‑mode or multi‑agent sessions.
- **Customisable worktree location** (#10599) – Users want to place Git worktrees outside the default `~/.codex` directory to match their workflow and disk organisation.
- **Headless remote Linux hosts for mobile** (#23200) – Mobile users want to connect directly to always‑on Linux servers without keeping a desktop app online.
- **Persist side chats as child threads** (#26227) – Side‑chat context is lost on app restart; many developers want durable child threads attached to the main conversation.
- **Thread pinning** (now addressed by PR #34840) – A long‑standing request to keep important threads accessible. The PR merged today delivers this feature.

## Developer Pain Points
Recurring frustrations visible across the top issues:

- **MCP process and resource leaks** – Zombie processes, pipe‑fd exhaustion, and memory leaks (issues #12491, #26984) are a systemic problem that undermines long‑running sessions.
- **Windows‑specific instability** – WSL path deserialisation errors (#16815), sandbox refresh failures (#22428), Store update exits (#33321), and cold‑launch freezes (#34025) make Windows the most troubled platform.
- **False positive safety checks** (#28015) – Interrupting normal local repository operations with unnecessary security prompts wastes time and tokens.
- **Regression in hooks** (#21639) – Breaking changes after updates erode trust in the release pipeline.
- **Rate‑limit confusion** (#32791) – Disappearing hourly usage limits and unclear plan caps frustrate Plus subscribers.
- **Extension/CLI version mismatch** (#29122) – Bundling prerelease CLI in stable IDE extensions silently activates experimental features, causing unexpected behavior and token waste.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-23

## Today’s Highlights
Three releases shipped this cycle, including the stable **v0.52.0** with CI config exclusion and foundational triage infrastructure. A critical security PR closes a variable expansion bypass (GHSA-wpqr-6v78-jr5g). Meanwhile, the community continues to be affected by two long‑standing bugs: subagents falsely reporting success after hitting `MAX_TURNS` (#22323) and the generalist agent hanging indefinitely (#21409).

---

## Releases

| Version | Summary |
|---------|---------|
| **v0.52.0-nightly.20260723** | Fix cached credentials fallback for `GOOGLE_APPLICATION_CREDENTIALS`; add `eval coverage report` command. |
| **v0.53.0-preview.0** | Fix 400 Bad Request when cancelled tool responses coalesce consecutive roles; introduce LLM triage orchestrator. |
| **v0.52.0 (stable)** | Refactor to exclude transient CI files from workspace context; add triage worker core modules. |

🔗 [v0.52.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0) | [v0.52.0-nightly](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260723.g9681621c6) | [v0.53.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.0-preview.0)

---

## Hot Issues

1. **#22323** – Subagent recovery after `MAX_TURNS` reports `GOAL` success, hiding the actual interruption.  
   *12 comments, 2 👍* — Community hit a false‑positive scenario that undermines trust in agent outcomes.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#21409** – Generalist agent hangs forever on simple tasks (e.g., folder creation). Workaround: disable subagents.  
   *8 comments, 8 👍* — A top pain point; users are forced to disable a core feature to avoid blocking.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#24353** – Epic for robust component‑level evaluations, building on behavioral eval infra.  
   *7 comments* – Tracks 76+ eval tests and aims to formalize evaluation pipelines.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

4. **#22745** – Assess AST‑aware file reads, search, and codebase mapping for better precision.  
   *7 comments* – Could reduce token use and turnaround by letting the agent read only method bounds.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

5. **#27191** – (CLOSED) Quota shows 100% used despite no actual usage; CLI stops responding.  
   *6 comments* — Addressed and closed; likely a backend issue, but affected many users.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/27191)

6. **#21968** – Gemini does not use custom skills / sub‑agents autonomously.  
   *6 comments* — Even with clear descriptors, the model rarely invokes them unless explicitly told.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

7. **#26522** – Auto Memory retries low‑signal sessions indefinitely, wasting resources.  
   *5 comments* — Sessions with no valuable content are re‑processed because the extraction agent skips them.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

8. **#25166** – Shell command execution gets stuck “Waiting input” after completing.  
   *4 comments, 3 👍* — Simple commands hang; the shell process appears to stay alive incorrectly.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

9. **#22232** – Enhance browser agent resilience with automatic session takeover and lock recovery.  
   *4 comments* — Fail‑fast strategy on locked profiles forces users to manually kill orphaned processes.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22232)

10. **#21983** – Browser subagent fails on Wayland (`Termination Reason: GOAL`).  
    *4 comments, 1 👍* — Wayland users cannot use browser automation at all.  
    [Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

---

## Key PR Progress

1. **#28403** – Fix `$VAR` / `${VAR}` expansion bypass (GHSA-wpqr-6v78-jr5g).  
   Blocks a security gate weakness; also hardens the issue dedup workflow.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28403)

2. **#28469** – Rotate session ID on model fallback to avoid stateful API errors.  
   When falling back to `gemini-2.5-flash`, a new session ID prevents `"Please submit a new query"` errors.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28469)

3. **#28485** – Add `gemini-3.5-flash` to model selector for all users.  
   Fixes a regression where the new model was invisible in the UI despite being configured.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28485)

4. **#28509** – Filter out `thought` parts from history turns when context management is off.  
   Prevents duplicate reasoning blocks and reduces noise in conversation history.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28509)

5. **#28506** – Propagate `AbortSignal` in `/compress` command.  
   Allows cancellation of background compression, preventing dangling requests.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28506)

6. **#28169** – Add `eval coverage report` command.  
   Cross‑references tool references in eval tests with the tool registry to highlight coverage gaps.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28169)

7. **#28431** – Cloud Run job + Workflows + Dockerfile for PR generator pipeline.  
   Infrastructure to automate code generation and PR creation via Eventarc triggers.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28431)

8. **#28446** – Use native `fetch` for OAuth token exchange to fix “Premature close” errors on headless VPS.  
   Replaces `node-fetch` with native fetch to avoid TLS issues in constrained environments.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28446)

9. **#28447** – Add Windows PowerShell troubleshooting for `gemini` command not found.  
   Documents common PATH issues after global npm install on Windows.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/28447)

10. **#28505** – Fix six broken cross‑reference links in `policy-engine.md` and `reference.md`.  
    Adds missing `.md` extensions and corrects site‑absolute paths.  
    [PR](https://github.com/google-gemini/gemini-cli/pull/28505)

---

## Feature Request Trends

- **AST‑aware tooling** (#22745, #22746) – Users want the agent to understand code structure (method boundaries, imports) to reduce turns and token waste.
- **Better subagent autonomy** – Requests for models to self‑select and invoke custom skills without explicit prompting (#21968, #21432).
- **Auto Memory improvements** – Deterministic redaction of secrets (#26525), quarantine of invalid patches (#26523), and smarter skipping of low‑signal sessions (#26522).
- **Browser agent resilience** – Automatic profile lock recovery, persistent session takeover, and Wayland support (#22232, #21983).
- **Enhanced eval infrastructure** – Component‑level evaluations (#24353), visible subagent trajectories via `/chat share` (#22598), and coverage reports (merged in #28169).

---

## Developer Pain Points

- **Agent hangs and false successes** – Generalist agent hangs forever (#21409); subagents report `GOAL` after `MAX_TURNS` (#22323). Workarounds exist but degrade the experience.
- **Security and permission issues** – Variable expansion bypass needed urgent patching (#28403); subagents executing without permission since v0.33.0 (#22093).
- **Shell command execution bugs** – Commands hang after completion (#25166); interactive prompts (e.g., `create vite app`) stuck (#22465).
- **Configuration inconsistencies** – Browser agent ignores `settings.json` overrides (#22267); symlinks in `~/.gemini/agents/` not recognized (#20079).
- **Tool / model management** – 400 errors with >128 tools (#24246); model selector missing `gemini-3.5-flash` (#28483, fixed in today’s PR).
- **Destructive behavior** – Agent occasionally uses `git reset --force` and other dangerous commands when safer alternatives exist (#22672).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-23

## Today’s Highlights

Three patch releases landed today (v1.0.74-1 through -3), including support for **Gemini 3.6 Flash** and a first-run sandbox opt-in splash. Community attention remains focused on a cluster of regressions: the BYOK authentication block in ACP mode (#4016), a returning React/Ink render loop (#4222), and persistent Windows-specific crashes (#4217, #4219). Several feature requests around model‑pool control (#4218) and subagent billing transparency (#4207) also gained traction.

## Releases

**v1.0.74-1, v1.0.74-2, v1.0.74-3** (all in last 24h)  
- **Added**: First‑run splash to opt into the default sandbox; support for `gemini-3.6-flash`.  
- **Improved**: Session multiplexing no longer leaks dialogs; the `$` interactive shell shortcut now works correctly.  
- **Fixes**: The subsequent releases (-2, -3) include additional bug fixes (details not broken out per release).  

[Full release list](https://github.com/github/copilot-cli/releases)

## Hot Issues

1. **#443 – Built-in PDF Reading Support**  
   *6 comments, 33 👍*  
   The highest‑voted issue. Users want native PDF handling for academic papers and technical docs without external tools.  
   [Issue #443](https://github.com/github/copilot-cli/issues/443)

2. **#4016 – BYOK (COPILOT_PROVIDER_*) still rejected in --acp mode**  
   *5 comments, 4 👍*  
   A regression that blocks login‑free custom providers in Agent Client Protocol mode. Regressed across v1.0.61–1.0.68.  
   [Issue #4016](https://github.com/github/copilot-cli/issues/4016)

3. **#4163 – Zombie child processes on Linux**  
   *3 comments, 2 👍*  
   Finished subprocesses accumulate as zombies under the copilot PID (~2/min), leading to PID exhaustion over long sessions.  
   [Issue #4163](https://github.com/github/copilot-cli/issues/4163)

4. **#4161 – task_complete tool unavailable after switching back to autopilot mode**  
   *2 comments, 1 👍*  
   Regression of a previously fixed issue (#1523). The `task_complete` tool is filtered out in autopilot mode despite the documented fix.  
   [Issue #4161](https://github.com/github/copilot-cli/issues/4161)

5. **#4222 – Regression of #2802: Infinite React/Ink render loop on Windows**  
   *0 comments, 0 👍 (new)*  
   The dreaded “Maximum update depth exceeded” loop returns on v1.0.72+ in VS Code integrated terminal. UI freezes, output swallowed.  
   [Issue #4222](https://github.com/github/copilot-cli/issues/4222)

6. **#4217 – Crash on exit (Windows) – libuv uv_async_send on closing handle**  
   *0 comments, 1 👍 (new)*  
   Consistent fatal fail‑fast (`FAST_FAIL_FATAL_APP_EXIT`) during teardown. Session work completes but exit crashes.  
   [Issue #4217](https://github.com/github/copilot-cli/issues/4217)

7. **#4218 – Allow users to configure the model pool used by Auto mode**  
   *0 comments, 6 👍 (new)*  
   Fast‑rising request: users want to define which models Auto mode can select from, for cost and behavior predictability.  
   [Issue #4218](https://github.com/github/copilot-cli/issues/4218)

8. **#4207 – Show per-subagent AI credit usage breakdown in /usage**  
   *0 comments, 6 👍 (new)*  
   Cumulative session credit usage hides individual agent costs. Request to break out per‑subagent billing.  
   [Issue #4207](https://github.com/github/copilot-cli/issues/4207)

9. **#4206 – MCP handshake stalls under org MCP policy**  
   *1 comment, 2 👍*  
   Environment footer stuck on “Loading:” forever when built‑in GitHub MCP handshake stalls. Affects enterprise setups.  
   [Issue #4206](https://github.com/github/copilot-cli/issues/4206)

10. **#4219 – Windows crash when `notifications` is enabled**  
    *0 comments, 0 👍 (new)*  
    Native access violation when OS toast notifications are turned on. Critical for Windows users.  
    [Issue #4219](https://github.com/github/copilot-cli/issues/4219)

## Key PR Progress

Only one pull request was updated in the last 24 hours:

- **#3163 – ViewSonic monitor (spam/unrelated)**  
  *Author: tijuks | Created: 2026-05-06*  
  This appears to be a non‑code PR (likely spam) referencing a monitor and GitHub action runners. No meaningful development impact.  
  [PR #3163](https://github.com/github/copilot-cli/pull/3163)

No other PRs were updated. The low PR volume may indicate maintainer bandwidth is focused on the three micro‑releases today.

## Feature Request Trends

- **Model‑Pool Control** (#4218 – 6 👍): Users want to constrain which models Auto mode can pick, citing unpredictable costs and behavior.
- **Subagent Billing Transparency** (#4207 – 6 👍): Breakdown of AI credit usage per subagent call is the top billing request.
- **Agent Chaining & Inline Invocation** (#4208 – 3 👍): Clear way to invoke specific custom agents mid‑prompt while preserving context.
- **Configurable Retry Logic** (#4210): Make Copilot Autopilot request‑error retry count configurable (mirroring VS Code request).
- **PDF Reading** (#443 – 33 👍): Old but still the most upvoted – native PDF support remains a frequently requested capability.
- **Terminal Shell Integration** (#3428): Emit OSC 133 sequences for easier scrollback navigation in terminals that support it.
- **Skill Tool Alias for Custom Agents** (#4209): Let custom agents use the `skill` tool via frontmatter aliases.

## Developer Pain Points

- **Authentication Regressions**: BYOK providers blocked in ACP mode (#4016) – a recurring issue that affects teams relying on custom model endpoints.
- **Process Management**: Zombie child processes on Linux (#4163) cause long‑session resource leaks.
- **UI/Rendering Regressions**: The React/Ink render loop (#4222) is back, alongside tmux dark‑on‑dark rendering (#4212) and Windows resume hangs (#4165).
- **Windows Stability**: Two new crash reports – on exit (#4217) and when notifications are enabled (#4219) – indicate deeper Node/libuv integration issues on Windows.
- **MCP & Agent Reliability**: MCP handshake stalls (#4206), BigInt serialization failures (#4211), and subagent server errors (#4226) erode trust in multi‑agent workflows.
- **False Positives in Permission Scanner & Plan Mode**: `git log -L` arguments misclassified as directory paths (#4221) and `gh api GET` blocked as “may modify workspace” (#4220) – these add friction for developers using standard CLI tools.
- **Remote Container Context Ignored**: Agent View initializes on host instead of inside SSH dev containers (#4216), breaking remote development workflows.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-07-23**

## Today's Highlights
Two critical bugs surfaced today: `prompt_cache_key` bleeding into third-party APIs (causing HTTP 400 errors) and a Windows startup crash due to Unicode encoding. A timely PR (#2535) already addresses the cache-key issue, while a new feature request for per-agent model selection signals growing demand for cost-tiered multi-agent workflows. No new releases were published in the last 24 hours.

## Releases
*None in the last 24 hours.*

## Hot Issues
1. **[#2534] Model API error 400 Validation: Unsupported parameter(s): `prompt_cache_key`**  
   *Author: dewrama · Created: 2026-07-23 · 0 comments*  
   A regression after the latest update broke compatibility with third‑party APIs (e.g., Nvidia NIM). The CLI now sends Moonshot‑specific parameters to endpoints that reject them. This has immediate impact for users relying on alternative providers.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2534)

2. **[#2532] `kimi web` crashes at startup on Windows when stdout is redirected: UnicodeEncodeError (gbk)**  
   *Author: BFour666 · Created: 2026-07-22 · 0 comments*  
   On Chinese‑locale Windows, redirecting stdout triggers a `UnicodeEncodeError` because the startup banner contains the `➜` character (U+279C), which cannot be encoded in GBK. Blocks piped workflows and CI integrations.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2532)

3. **[#2531] MCP tool names & schemas rejected by Moonshot API (HTTP 400)**  
   *Author: sbdsam · Created: 2026-07-22 · 1 comment*  
   When MCP tools produce schemas using `anyOf`, the Moonshot API returns `400` – it expects a simplified “moonshot‑flavored” JSON schema. Users must sanitize client‑side, adding unnecessary complexity. The issue has only 0 upvotes but highlights an API compatibility gap.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2531)

4. **[#2318] [bug] request reached organization TPD rate limit, current: 1505241**  
   *Author: globalvideos272-lab · Created: 2026-05-18 · Updated: 2026-07-22 · 1 comment · 👍 2*  
   A long‑standing rate‑limit miscalculation bug with kimi‑cli 2.6 on Moonshot’s platform. The “TPD” count seems inflated, causing premature throttling. Community interest is modest (2 thumbs up), but the issue remains open for 2 months.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2318)

5. **[#2533] Feature Request: Per-agent model selection for sub-agents**  
   *Author: bob0x‑ai · Created: 2026-07-23 · 0 comments*  
   Requests the ability to run sub-agents on different models than the session default, enabling cost‑tiered multi‑agent workflows (cheap models for simple tasks, capable models for complex ones). No community reaction yet, but aligns with mature MCP/agent patterns.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2533)

## Key PR Progress
1. **[#2535] fix(llm): scope prompt cache keys to Moonshot APIs**  
   *Author: Sanjays2402 · Created: 2026-07-23 · 0 comments*  
   Resolves #2534 by ensuring `prompt_cache_key` is only sent to official Moonshot/Kimi endpoints. Third‑party APIs are no longer polluted. This is a critical hotfix for users of alternative providers.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/pull/2535)

2. **[#2524] fix(tools): count StrReplaceFile replacements against the running content**  
   *Author: Sreekant13 · Created: 2026-07-20 · Updated: 2026-07-22 · 0 comments*  
   Fixes a bug where `StrReplaceFile` reported replacement counts based on the original file content instead of the (already modified) running content. Chain edits were miscounted. No community discussion yet, but important for accurate telemetry.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/pull/2524)

3. **[#2530] fix(shell): stop blocking until timeout when a detached child holds the pipes**  
   *Author: ayaangazali · Created: 2026-07-21 · Updated: 2026-07-22 · 0 comments*  
   Addresses #2468: in the foreground shell path, `_run_shell_command` waited for stdout/stderr EOF before checking exit code. Commands like `some_daemon & echo done` left detached children holding pipes, causing timeouts. This PR ensures the shell command completes promptly.  
   [GitHub Link](https://github.com/MoonshotAI/kimi-cli/pull/2530)

## Feature Request Trends
The most prominent direction is **multi‑agent flexibility**. Issue #2533 explicitly asks for per‑agent model selection, suggesting users want to mix cheap and powerful models within a single session. No other feature requests were filed in the last 24 hours, but the growing complexity of sub‑agent workflows (MCP tools, parallel tasks) will likely drive more demand for model‑level orchestration.

## Developer Pain Points
1. **API parameter leakage** – Third‑party endpoints receive Moonshot‑specific parameters (e.g., `prompt_cache_key`), breaking HTTP 400 validation. (#2534)
2. **Unicode encoding on Windows** – Non‑ASCII characters in startup banners crash the CLI when stdout is redirected in non‑UTF‑8 locales (GBK). (#2532)
3. **Schema incompatibility with Moonshot API** – MCP tools generating `anyOf` schemas are rejected; users must manually flatten schemas. (#2531)
4. **Rate‑limit miscalculation** – TPD counters appear inflated, causing early throttling for some users. (#2318)
5. **Shell command hangs** – Detached child processes holding pipes block the CLI until a timeout. (#2530, fixed in PR #2530)
6. **File replacement counting** – Chained `StrReplaceFile` edits produce incorrect replacement counts. (#2524, fixed in PR #2524)

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-07-23

**Data source:** [`anomalyco/opencode`](https://github.com/anomalyco/opencode)

---

## Today’s Highlights

The community is facing a **widespread subscription‑blocking bug** (`Request blocked by upstream provider`) that prevents all `opencode‑go` users from completing requests, with multiple duplicate reports in multiple languages. A long‑standing **high‑CPU‑while‑idle issue** (#19466) continues to draw attention, while several new PRs aim to improve **model response handling** and **session‑mode reminders**. The volume of closed issues today suggests active triage, but several critical bugs remain unresolved.

---

## Releases

**pr‑38252‑videos** – Published verification recordings for [PR #38252](https://github.com/anomalyco/opencode/pull/38252). No new version tag was cut; this is a supporting asset release.

---

## Hot Issues (10 most noteworthy)

1. **#6231 – Auto‑discover models from OpenAI‑compatible providers**  
   *Author: ochsec · 28 comments · 185 👍*  
   Users must manually list models for local providers (LM Studio, Ollama, etc.), which is error‑prone as models change. This feature request has strong community support.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/6231)

2. **#38218 – All subscription models return “Request blocked by upstream provider”**  
   *Author: 1335907208 · 22 comments · 5 👍*  
   The most critical bug of the day: every `opencode‑go` call fails with this error. Duplicates in Chinese (#38293) and Portuguese (#38368) indicate it’s a global outage.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/38218)

3. **#19466 – opencode using CPU for doing nothing**  
   *Author: Jaaaky · 15 comments · 11 👍*  
   While waiting for API rate‑limit retries, the process consumes ~50% of a CPU core. Unacceptable for an idle tool.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/19466)

4. **#27018 – v1.14.48 localserver disconnects**  
   *Author: sReplay · 12 comments · 2 👍*  
   Desktop version loses connection after sending a message (green → red indicator). Regression from earlier versions.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/27018)

5. **#37970 – Plan/Build mode missing in latest version**  
   *Author: BillyJack76 · 10 comments · 1 👍*  
   The ability to toggle between plan and build modes appears to have been removed or is inconsistent. Replicated by multiple users (#38421, #38364).  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/37970)

6. **#18011 – LM Studio shows only 3 of 9 models**  
   *Author: firexrwt · 6 comments · 4 👍*  
   Auto‑discovery picks up only a subset of models from the `/v1/models` endpoint. Related to #6231.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/18011)

7. **#26220 – Infinite loop after tool calls complete**  
   *Author: Dvalin21 · 6 comments · 3 👍*  
   The process hangs indefinitely after finishing tool execution, requiring a restart. Potentially related to the V2 server allocation loop (#36677).  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/26220)

8. **#36677 – Long‑lived V2 server enters persistent allocation loop**  
   *Author: opencode‑agent[bot] · 2 comments*  
   A fresh server is fine, but after hours of idle time CPU and memory balloon (1.1–1.3 GB RSS). This is a core performance bug for the V2 architecture.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/36677)

9. **#34407 – LaTeX math rendered as raw text in CLI**  
   *Author: yearzen1 · 4 comments*  
   Formulas are displayed as raw markup instead of being rendered. Reduces readability for technical users.  
   [🔗 Issue](https://github.com/anomalyco/opencode/issues/34407)

10. **#38356 – Subagent corrupts files with null bytes**  
    *Author: Cowa‑Tech · 2 comments*  
    The `task` subagent wrote null bytes instead of actual content, corrupting HTML files. A reliability concern for agent workflows.  
    [🔗 Issue](https://github.com/anomalyco/opencode/issues/38356)

---

## Key PR Progress (10 important PRs)

1. **#38423 – feat(ai): preserve raw finish reasons**  
   Exposes provider‑native finish reasons (e.g., `max_output_tokens`, `content_filter`) in the event stream. Improves observability for terminal and API consumers.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38423)

2. **#38067 – fix(session): edge‑trigger build‑switch reminder**  
   Replaces full‑history scanning with a simple flag to decide when to show the “plan→build” reminder. Reduces overhead and avoids repeated reminders.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38067)

3. **#37732 – fix(opencode): surface empty model responses**  
   When a provider finishes with `stop` and usage but emits no text/tool call, OpenCode now records an empty assistant message instead of silently dropping it. Closes #37735.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/37732)

4. **#38374 – fix(ai): handle incomplete responses without reasons**  
   Gracefully handles OpenAI responses that omit the optional `reason` field (e.g., `content_filter` without a reason).  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38374)

5. **#38420 – feat(opencode): add `--no-project-instructions` and env var**  
   Adds a CLI switch to disable project instructions for automation scenarios where repository‑provided instructions should be treated as untrusted input.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38420)

6. **#38418 – fix(web): fix model not replying when client time is behind server time**  
   Fixes a bug caused by comparing timestamps using local time instead of a common `created` field. Web mode now works even if the client clock is slightly off.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38418)

7. **#38397 – refactor(tui): generate syntax from V2 theme**  
   Migrates the TUI’s syntax styling to use V2 theme tokens, removing the parallel V1 resolution. Preserves all 101 existing scopes.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38397)

8. **#38401 – fix(core): load dynamic models for `/api/generate`**  
   Ensures stateless API requests can use dynamically‑loaded provider packages (e.g., `opencode/gemini-3.5-flash`). Previously failed with “Unsupported package”.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38401)

9. **#38408 – fix: pr‑standards falsely flags v2 PRs**  
   Corrects the `closingIssuesReferences` check to work on non‑default branches, preventing false positives on V2‑targeted PRs.  
   [🔗 PR](https://github.com/anomalyco/opencode/pull/38408)

10. **#38406 – fix(core): retry failed location boot instead of caching failure**  
    A location that fails to boot once would serve the cached failure for the full 60‑minute TTL. This PR adds proper retry logic.  
    [🔗 PR](https://github.com/anomalyco/opencode/pull/38406)

---

## Feature Request Trends

Several strong signals emerged from today’s issues and PRs:

- **Auto‑discovery of models** – Users want OpenCode to query OpenAI‑compatible `/v1/models` endpoints and automatically list available models (#6231, #18011). This reduces manual configuration for local providers.
- **Portable / USB execution** – A request (#38391) for a portable version to run on air‑gapped or locked‑down machines without installation.
- **UI enhancements** – Requests for: a user‑message quick‑jump sidebar (#32165), timestamps on tool execution blocks (#22144), and an FPS limiter for remote desktop performance (#13817).
- **Plan/Build mode retention** – Multiple users (#37970, #38421, #38364) insist that the toggle between Plan and Build modes must be re‑introduced or made more explicit.
- **Project configuration controls** – The new `OPENCODE_DISABLE_PROJECT_INSTRUCTIONS` flag (#38420) reflects a need for fine‑grained automation and security controls.

---

## Developer Pain Points

The following recurring frustrations are most evident from today’s data:

- **Subscription / provider errors** – The `Request blocked by upstream provider` bug (#38218 and its duplicates) is blocking all paid users, including those in non‑English markets.
- **High CPU while idle** – #19466 shows that rate‑limit backoff loops are computationally expensive (>50% CPU). Developers expect idle tools to be near zero.
- **Infinite loops after tool use** – Both #26220 and the V2 allocation loop (#36677) indicate the process can stall or leak memory after extended sessions.
- **Local server instability** – The Desktop app losing connection mid‑conversation (#27018, #38419) breaks workflow continuity.
- **Mode toggle regression** – Removing or breaking the Plan/Build mode switch (#37970) forces power users to rely on ambiguous prompts.
- **File corruption by subagents** – #38356 shows that agent chains can write null bytes, which undermines trust in automated file editing.
- **UI regressions** – Multiple complaints about the new interface being “ugly” or “laggy” (#38416, #38412) suggest the recent UI overhaul introduced performance and usability issues.

---

*Generated from `anomalyco/opencode` community data – 2026-07-23*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-07-23

## Today’s Highlights
The Pi codebase saw a flurry of activity with 29 PRs and 50 issues touched in the last 24 hours. A critical bug where the OpenAI SDK’s retry logic could sleep for **days** on a 429 response (#6911) was fixed by replacing SDK retries with an abortable helper. Meanwhile, the old issue of auto-logout from GitHub (#6686) remains unresolved despite a prior fix. On the feature side, native OpenRouter OAuth support (#6927) and several new providers (StepFun, Bedrock Mantle) landed, while a proposed constrained sampling API (#6341) sparked discussion.

## Releases
No new releases in the last 24 hours. The latest stable is v0.80.7 (as referenced in some issues).

## Hot Issues
*(10 most noteworthy issues, selected for impact, community engagement, or severity)*

1. **#6686 – Pi automatically logs out of GitHub**  
   *Status: CLOSED (no-action)*  
   A long-standing regression – users re-report that Pi drops GitHub authentication after a few minutes. The team closed it as “no-action” (likely a duplicate or platform issue), but comment count (10) shows frustration.  
   [GitHub](https://github.com/earendil-works/pi/issues/6686)

2. **#6768 – Compaction using Copilot Enterprise not possible**  
   *Status: OPEN*  
   **8 reactions** – Users with Copilot Enterprise licenses cannot compact context (errors: 421 Misdirected Request for OpenAI, failure for Anthropic). High demand for a fix.  
   [GitHub](https://github.com/earendil-works/pi/issues/6768)

3. **#6911 – OpenAI SDK retries sleep full Retry-After (days) and Escape cannot abort**  
   *Status: CLOSED*  
   A severe bug: when `maxRetries > 0`, SDK sleeps the entire `Retry-After` header (e.g. a day) with no cap, and the sleep ignores AbortSignal. Fixed today in PR #6980.  
   [GitHub](https://github.com/earendil-works/pi/issues/6911)

4. **#6210 – /scoped-models cannot select model ids containing brackets**  
   *Status: OPEN (inprogress)*  
   Custom model IDs like `custom/bracketed-model[1m]` are rejected because bracket parsing breaks the selector. No workaround.  
   [GitHub](https://github.com/earendil-works/pi/issues/6210)

5. **#6621 – Prevent accidental cache invalidation due to dynamic system prompt**  
   *Status: CLOSED*  
   On unified memory devices (e.g. AMD Strix Halo), dynamic system prompts (like date/time) ruin prompt caching. Proposal to add a stable system prompt hash for cache reuse. 6 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/6621)

6. **#6940 – OpenRouter cache breakpoint stops before tool results**  
   *Status: CLOSED (last-read)*  
   With Anthropic models via OpenRouter, cache breakpoints stop advancing after consecutive tool-use turns, leading to growing uncached tokens.  
   [GitHub](https://github.com/earendil-works/pi/issues/6940)

7. **#6678 – Regression: getTextOutput still crashes on undefined content**  
   *Status: CLOSED (no-action)*  
   An old crash (reading `.content` on undefined) persists in v0.80.7 despite two previous fixes being rejected. Affects users with certain streaming edge cases.  
   [GitHub](https://github.com/earendil-works/pi/issues/6678)

8. **#6989 – [P0] File mutation preconditions run before the per-file queue**  
   *Status: CLOSED (untriaged)*  
   In parallel tool execution, `beforeToolCall` preconditions (like file reads) execute for every sibling call *before* any actual edit starts. This can cause order-dependent race conditions.  
   [GitHub](https://github.com/earendil-works/pi/issues/6989)

9. **#6957 – aws-bedrock provider ignores profile when AWS_* env vars present**  
   *Status: CLOSED*  
   Environment variables override the configured `profile`. The provider falls back to `process.env` credentials even when a profile is explicitly set.  
   [GitHub](https://github.com/earendil-works/pi/issues/6957)

10. **#6979 – OAuth-authenticated Anthropic requests get billed as metered API, not Pro/Max**  
    *Status: CLOSED (untriaged)*  
    Users logged in via OAuth (not API key) are incorrectly charged per-token instead of using their Pro subscription. Likely a header-mapping issue.  
    [GitHub](https://github.com/earendil-works/pi/issues/6979)

## Key PR Progress
*(10 important PRs, merged or open, that drive the project forward)*

1. **#6980 – fix(ai): make provider retries abortable**  
   *Status: OPEN*  
   Replaces OpenAI/Anthropic SDK retries with a custom helper that caps retry delay and respects AbortSignal. Fixes #6911 (the “days-long sleep” bug).  
   [GitHub](https://github.com/earendil-works/pi/pull/6980)

2. **#6927 – Add native OpenRouter OAuth support**  
   *Status: CLOSED (merged)*  
   Implements PKCE OAuth flow for OpenRouter, allowing users to authenticate via browser instead of pasting API keys.  
   [GitHub](https://github.com/earendil-works/pi/pull/6927)

3. **#6341 – feat(ai): support constrained sampling**  
   *Status: OPEN*  
   A major feature – tools can request provider-side constrained generation (JSON schema, regex). Opens up safer tool calls. Discussion in progress.  
   [GitHub](https://github.com/earendil-works/pi/pull/6341)

4. **#6987 – fix(tui): align grapheme widths with terminal cells**  
   *Status: OPEN*  
   Addresses long-standing display issues with emoji and wide characters. Author notes the complexity but provides a best-effort fix.  
   [GitHub](https://github.com/earendil-works/pi/pull/6987)

5. **#6967 – feat(coding-agent): expose session metadata to bash tools**  
   *Status: CLOSED (merged)*  
   Passes session ID, provider, model, etc. as environment variables to bash commands – useful for extensions and scripts.  
   [GitHub](https://github.com/earendil-works/pi/pull/6967)

6. **#6916 – feat(agent): add AgentHarness execution tools**  
   *Status: CLOSED (merged)*  
   New abstraction for running tools with application-specific context (e.g. execution environment, session ID). Foundation for more advanced orchestration.  
   [GitHub](https://github.com/earendil-works/pi/pull/6916)

7. **#6960 – feat(ai): add StepFun providers**  
   *Status: CLOSED (merged)*  
   Four new providers for the StepFun API (China/Global/prepaid). Expands model reach.  
   [GitHub](https://github.com/earendil-works/pi/pull/6960)

8. **#6984 – feat(ai): honor compat.forceAdaptiveThinking in bedrock-converse-stream**  
   *Status: CLOSED (merged)*  
   Fixes a crash where certain Claude models (e.g. sonnet-5) on Bedrock required adaptive thinking but weren’t detected.  
   [GitHub](https://github.com/earendil-works/pi/pull/6984)

9. **#6881 – feat(ai): use provider-reported cost when responses include it**  
   *Status: OPEN*  
   When the API returns actual cost (e.g. from Bedrock, Vercel AI Gateway), use it instead of catalog rates. Improves billing accuracy.  
   [GitHub](https://github.com/earendil-works/pi/pull/6881)

10. **#6965 – fix: isolate test environment**  
    *Status: OPEN*  
    Makes test runs more reproducible by setting an explicit environment allowlist, guarding against state pollution (home dir, temp, npm, etc.).  
    [GitHub](https://github.com/earendil-works/pi/pull/6965)

## Feature Request Trends
- **OAuth & Authentication** – Multiple requests for native OAuth (OpenRouter merged, Anthropic OAuth billing issue #6979).  
- **Provider Extensibility** – New providers (StepFun, Bedrock Mantle) and request for constrained sampling (#6341) to improve tool safety.  
- **Session & Metadata Exposure** – Exposing session info to bash tools (#6967) and agent harness (#6916) for better extension integration.  
- **UI/UX Improvements** – MRU model switching (#6982), per-block thinking labels (#6988), and grapheme width fixes (#6987).  
- **Cache & Performance** – Avoiding cache invalidation from dynamic prompts (#6621) and better retry handling (#6911).  
- **Package Ecosystem** – VS Code extension proposal (#6985) and requests for the official package gallery.

## Developer Pain Points
1. **Retry & Timeout Confusion** – The OpenAI SDK’s 429 handling caused “sleep-for-days” scenarios (#6911). Lack of user-abort during retries.
2. **Provider Configuration Leaks** – Environment variables override explicit profile settings (#6957). AWS_Bedrock and similar providers are fragile.
3. **OAuth Billing Misclassification** – OAuth users of Anthropic are charged metered API rates instead of their subscription (#6979).
4. **Cache Breakpoint Failures** – OpenRouter with Anthropic models loses caching after tool calls (#6940), inflating costs.
5. **File Race Conditions** – Parallel tool execution runs precondition hooks before per-file queuing, causing order bugs (#6989).
6. **Extension Dialog Hangs** – Concurrent extension dialogs can leave promises unresolved (#6978), locking the TUI.
7. **Temp File Cleanup** – `--no-session` leaves orphaned session directories (#6924). External editor temp files in crowded /tmp cause slowness (#6774).
8. **Compaction for Copilot Enterprise** – Entirely blocked (#6768), with no workaround.
9. **Model ID Parsing** – Bracket characters break model selection (#6210), hindering custom models.
10. **Crash Log Location** – Hardcoded `~/.pi/agent/pi-crash.log` ignores `PI_CODING_AGENT_DIR` (#6652), fixed today in PR #6958.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-23

## 1. Today’s Highlights
The community fixed two critical blockers: the **side-query `enable_thinking` bug** (Issue #7284) that broke `web_fetch` and other tool endpoints, and a **test-suite red on `main`** (Issue #7537) that was blocking all PRs. Meanwhile, multiple **update‑check failures** (Issues #7515, #7520, #7543) point to deeper compatibility issues with npm 12 and managed‑update artifacts. On the automation front, the **Fleet Shepherd Dashboard** (#7167) and new autofix retry logic (#7490) show continued investment in CI‑CD reliability.

## 2. Releases
No product release was published today. The only tagged artifact is `v0.0.0-benchmark-poc.20260722.1` – an internal prerelease used to validate the GitHub Actions → ECS benchmark worker pipeline. Not a user-facing version.

## 3. Hot Issues (10 noteworthy)
1. **[#7284] – side-query forces `enable_thinking=false`** (P1, closed)  
   `runSideQuery` always sends `enable_thinking: false`, causing 400 errors on DashScope/TokenPlan endpoints that require it `true`. Five comments; urgent fix in progress.  
   https://github.com/QwenLM/qwen-code/issues/7284

2. **[#7306] – Harden tool‑output budgeting & artifact lifecycle** (P2, open)  
   Proposes formal observability and finalization contracts. Gained 4 comments; phase 1 already merged (#7323, #7470).  
   https://github.com/QwenLM/qwen-code/issues/7306

3. **[#7449] – Enterprise external‑memory integration profile** (P3, open)  
   A provider‑neutral proposal to define an official memory integration contract. 4 comments; documentation‑first approach.  
   https://github.com/QwenLM/qwen-code/issues/7449

4. **[#7404] – CLI update‑check timeout too short** (P3, closed)  
   The startup update check times out when loading long sessions. 4 comments; community frustration with usability.  
   https://github.com/QwenLM/qwen-code/issues/7404

5. **[#7167] – Fleet Shepherd Dashboard** (open)  
   Automatically maintained dashboard tracking CI scan ages, syncs, and PR states. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/7167

6. **[#7516] – Main CI failed: E2E Tests** (open)  
   A main‑branch E2E test run failed, blocking all open PRs. Labeled `autofix/skip`. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/7516

7. **[#6577] – Windows Alt+V paste bug** (P2, open, `welcome‑pr`)  
   `Alt+V` fails to paste clipboard screenshots in Windows Terminal. 3 comments; affects v0.19.8+.  
   https://github.com/QwenLM/qwen-code/issues/6577

8. **[#5958] – Web Shell input editor not working on mobile** (P2, open, `welcome‑pr`)  
   CodeMirror editor in mobile browsers (iOS/Android) is non‑functional. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/5958

9. **[#7264] – Cold‑start lazy‑loading candidates** (P2, open)  
   Follow‑up from esbuild audit: 17.24 MiB of eager static imports in ACP child process. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/7264

10. **[#7489] – VS Code file picker: `@filename` inserted but image not attached** (open)  
    When attaching an image via the file picker, only the file name is inserted as text; the model never receives the image. 3 comments.  
    https://github.com/QwenLM/qwen-code/issues/7489

## 4. Key PR Progress (10 important)
1. **[#7551] – feat(web-shell): add selective Shadow DOM isolation**  
   Allows opt‑in isolation of plugin manager & shared portal tree.  
   https://github.com/QwenLM/qwen-code/pull/7551

2. **[#7522] – fix(acp): hide discontinued OAuth model for other auth types**  
   Removes the built‑in Qwen OAuth model from selectors when another auth type is active.  
   https://github.com/QwenLM/qwen-code/pull/7522

3. **[#7490] – fix(autofix): retry a skipped‑Prepare instead of stranding**  
   Prevents infrastructure failures from permanently blocking healthy PRs.  
   https://github.com/QwenLM/qwen-code/pull/7490

4. **[#7550] – fix(cli): say review coverage gaps in author’s units**  
   `/review` now displays chunk‑level gaps using the PR author’s own labels instead of internal chunk IDs.  
   https://github.com/QwenLM/qwen-code/pull/7550

5. **[#7514] – feat(serve): persist workspace channel configuration**  
   First part of channel‑management for #7209: add serializable metadata for DingTalk, WeCom, Feishu.  
   https://github.com/QwenLM/qwen-code/pull/7514

6. **[#7512] – perf(startup): lazy‑load Google GenAI SDK**  
   Removes `@google/genai` from ACP bootstrap static closure; uses package‑local implementation for sync surfaces.  
   https://github.com/QwenLM/qwen-code/pull/7512

7. **[#7268] – feat(serve): Hot‑reload workspace trust changes**  
   Trust‑policy changes now take effect without restarting the daemon.  
   https://github.com/QwenLM/qwen-code/pull/7268

8. **[#7536] – feat(core): Align GenAI telemetry with ARMS**  
   Maps Qwen Code span attributes to Alibaba Cloud ARMS LLM Trace conventions.  
   https://github.com/QwenLM/qwen-code/pull/7536

9. **[#7501] – fix(cli): open the actual serve fallback port**  
   Prevents `--open` from launching the wrong port after `EADDRINUSE` fallback.  
   https://github.com/QwenLM/qwen-code/pull/7501

10. **[#7528] – Fix(cli): use `npm view` for update check**  
    Replaces broken `update-notifier` logic with `npm view @qwen-code/qwen-code version`. Addresses #7515.  
    https://github.com/QwenLM/qwen-code/pull/7528

## 5. Feature Request Trends
- **Enterprise external‑memory integration** (#7449) – formal API for plugging in third‑party memory providers.
- **Web Shell enhancements** – git mode selector (#7471), start‑in context selector (#6701), Shadow DOM isolation (#7551).
- **Tool fallback automation** – `web_fetch` should fall back to curl + local parsing on failure (#7298).
- **Subagent/todo plan visualization** – DAG view linking plan nodes to live executions (#7525).
- **Managed npm update disk cleanup** – safe removal of staging directories after interrupted updates (#7524).
- **Channel management** – per‑workspace configuration for DingTalk/WeCom/Feishu (#7514, #7209).

## 6. Developer Pain Points
- **`enable_thinking` parameter restrictions** – side‑query force‑disables thinking, breaking providers that require it (#7284, #7440, #7534).
- **Update‑check fragility** – fails with “registry error” on npm 12 global mode (#7520), mise bash wrapper (#7543), and registry timeouts (#7515). Multiple fixes in flight (#7528).
- **Main CI test suite red** – core test failing (`fork dispatch` never sees `registry.complete`), blocking all PRs (#7537).
- **Flickering in terminal emulators** – xterm/tmux flicker on Linux (#6137), plus `RuntimeError: memory access out of bounds` (#6820).
- **Inconsistent date handling** – `/insight` heatmap mixed UTC/local (#6835).
- **Stale port wrong `--open`** – after fallback, browser opens original port (#7500, fixed in #7501).
- **Image attachment issues** – VS Code file picker inserts filename but not image (#7489); Windows Alt+V does nothing (#6577).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-23

## Today's Highlights
The CodeWhale v0.9.1 release is in final integration with a wave of closed release-blocker issues and PRs landing unified skill management (`/skills`), the `uwu` theme, and a fail-closed fix for Kimi K3 model-ID cross-pairings. Simultaneously, the community has kicked off a major **Context Diet** epic (v0.9.2) to audit and shrink every model-facing prompt and payload. Meanwhile, several open bugs around Windows PATH overwrites, custom provider failures, and macOS Dropbox file access are drawing developer attention.

---

## Releases (last 24h)
None. The repository has not published a new tag in the past 24 hours; the active integration branch is targeting v0.9.1.

---

## Hot Issues (10 noteworthy)

1. **EPIC: staged command-boundary refactor** [#2870](https://github.com/Hmbown/CodeWhale/issues/2870)  
   *Author: aboimpinto | Comments: 17*  
   Tracks the decomposition of the large command-boundary refactor (#2791) into smaller mergeable layers. The community is actively discussing how to split routing changes without breaking ongoing work.

2. **Help JayBeest map the CodeWhale tsunami** [#4227](https://github.com/Hmbown/CodeWhale/issues/4227)  
   *Author: JayBeest | Comments: 12*  
   A skill/workflow proposal to keep contributor dev environments in sync with the high‑velocity `main` branch (10+ PRs/day). The issue has attracted design input for automating `cargo build` and health checks.

3. **macOS Dropbox file provider blocks reads/writes** [#4085](https://github.com/Hmbown/CodeWhale/issues/4085)  
   *Author: Watcher24 | Comments: 4*  
   CodeWhale cannot access files under `~/Library/CloudStorage/Dropbox/` despite ad‑hoc signing with zero entitlements. Community suspects a File Provider framework restriction; workaround needed.

4. **`danger-full-access` does not disable tools-layer workspace boundary** [#4684](https://github.com/Hmbown/CodeWhale/issues/4684)  
   *Author: AnonymousUser443 | Comments: 2*  
   Setting `sandbox_mode = "danger-full-access"` fails to bypass the `read_file`/`grep_files` boundary check, breaking global skill access on Windows. Users request a clear boundary override.

5. **Windows installer overwrites user PATH** [#4685](https://github.com/Hmbown/CodeWhale/issues/4685)  
   *Author: MuRongMoQing | Comments: 1*  
   `CodeWhaleSetup.exe` replaces the user `PATH` instead of appending, destroying existing entries. A prompt fix is expected from the v0.9.1 pipeline.

6. **Wrong DeepSeek completions URL (flaky)** [#4683](https://github.com/Hmbown/CodeWhale/issues/4683)  
   *Author: demian-welt | Comments: 1*  
   Intermittent network errors hitting `https://api.deepseek.com/v1/chat/completions`. The issue appears after long idle periods; model routing retry logic is being investigated.

7. **Custom provider causes launch failure** [#4682](https://github.com/Hmbown/CodeWhale/issues/4682)  
   *Author: e792a8 | Comments: 1*  
   Setting `/provider` to a custom name prevents CodeWhale from launching. The bug affects users relying on community‑maintained provider configs.

8. **`<turn_meta>` blocks displayed when reopening a session** [#4681](https://github.com/Hmbown/CodeWhale/issues/4681)  
   *Author: e792a8 | Comments: 1*  
   Hidden metadata tags reappear after closing and reopening a session, cluttering the transcript. Likely a serialization/state restoration bug.

9. **v0.9.1 security gate: deep scan and dependency alerts** [#4713](https://github.com/Hmbown/CodeWhale/issues/4713)  
   *Author: Hmbown | Comments: 0*  
   Release gate requiring disposition of 17 Dependabot alerts (7 high, 10 moderate) before tagging v0.9.1. Affected npm packages include `axios`, `brace-expansion`, and `js-yaml`.

10. **Context Diet epic: minimize every model-facing prompt** [#4704](https://github.com/Hmbown/CodeWhale/issues/4704)  
    *Author: Hmbown | Comments: 0*  
    The umbrella issue for v0.9.2’s “context diet” – audit and reduce system prompts, tool descriptions, and context layers to improve portability across model families. Several sub‑issues (e.g., #4705, #4709) are already open.

---

## Key PR Progress (10 important)

1. **feat(skills): unified `/skills` manager with audit and owned mutations** [#4679](https://github.com/Hmbown/CodeWhale/pull/4679)  
   *Author: SamhandsomeLee | Merged*  
   Delivers the Skills lane for v0.9.1: one command to discover, install, update, remove, and trust skills across project and global roots.

2. **feat(skills): default CodeWhale skill pack (bundled v5)** [#4695](https://github.com/Hmbown/CodeWhale/pull/4695)  
   *Author: Hmbown | Merged*  
   Ships a first‑party skill pack (interview, plan, implement, debug, review, etc.) comparable to Kimi Code or Claude Code workflows.

3. **feat(tui): ship staged `/uwu` theme** [#4696](https://github.com/Hmbown/CodeWhale/pull/4696)  
   *Author: Hmbown | Merged*  
   Implements the `uwu` (aliases `owo`, `kawaii`) theme with soft colors and a blush whale mark. Theme‑native composer rails land in the same PR.

4. **fix(kimi): fail closed on K3 model-ID cross-pairings** [#4694](https://github.com/Hmbown/CodeWhale/pull/4694)  
   *Author: Hmbown | Merged*  
   Treats base‑URL + model‑ID as one route identity, preventing silent usage of wrong model IDs with MoonShot/Kimi endpoints.

5. **fix(tui): Work summary lifecycle, actionable title, and top-area hierarchy** [#4693](https://github.com/Hmbown/CodeWhale/pull/4693)  
   *Author: Hmbown | Merged*  
   Fixes three v0.9.1 release blockers: expiring recent summary after 4s, showing actionable titles, and proper top‑chrome hierarchy.

6. **fix(tui): focus v0.9.1 chrome on todos and agents** [#4711](https://github.com/Hmbown/CodeWhale/pull/4711)  
   *Author: Hmbown | Merged*  
   Replaces the generic Work strip with a resizable To‑do + Sub‑agent bar; hides completed internal coordination.

7. **Integrate CodeWhale v0.9.1 runtime and release surface** [#4675](https://github.com/Hmbown/CodeWhale/pull/4675)  
   *Author: Hmbown | Merged*  
   The mega‑PR that integrates v0.9.1’s runtime simplifications, empty‑Work fix, color grammar, and public release surface. Basis for all subsequent release‑blocker fixes.

8. **fix(tui): register debt compatibility aliases** [#4680](https://github.com/Hmbown/CodeWhale/pull/4680)  
   *Author: nightt5879 | Merged*  
   Adds `/slop` and `/canzha` as `/debt` aliases, unifying dispatch and typo suggestions. Removes a pre‑registry special case.

9. **feat(minimax): add China / Token Plan provider routes** [#4686](https://github.com/Hmbown/CodeWhale/pull/4686)  
   *Author: ffaacceelee | Open*  
   Adds `minimax-cn` and `minimax-anthropic-cn` targets for `api.minimaxi.com`, expanding regional provider support.

10. **docs: refresh the CodeWhale product screenshot** [#4508](https://github.com/Hmbown/CodeWhale/pull/4508)  
    *Author: Hmbown | Merged*  
    Updates the canonical README and website screenshot to match v0.9.1 visuals; includes a byte‑identity contract test.

---

## Feature Request Trends
- **Unified skill/workflow management** – Multiple issues and PRs push for a single `/skills` command to install, audit, and remove skill packs, echoing workflows in Kimi Code and Claude Code.
- **Context diet / prompt optimization** – A new v0.9.2 epic (#4704) calls for stripping redundant system prompt layers, shortening tool descriptions, and deduplicating project/route/locale context. Community interest in cross‑model portability.
- **Expanded provider support** – Requests for custom provider routing (TelecomJS, Minimax‑China, Kimi K3 fixes) and better fallback logic for flaky DeepSeek completions.
- **TUI polish and theming** – Custom themes (`/uwu`), theme‑native composer rails, resizable work chrome, and transcript visual rhythm indicate demand for a more “composed” terminal experience.
- **Windows and macOS platform fixes** – Issues around installer PATH handling, Dropbox file access, and sandbox boundary overrides point to a need for better cross‑platform testing.

---

## Developer Pain Points
- **Windows installer corrupts user PATH** – A recurring frustration (#4685) that breaks other tools. Urgent hotfix expected.
- **Custom provider configuration crashes on launch** – Users cannot use `custom` provider names (#4682); the issue blocks adoption of community‑maintained provider lists.
- **Metadata leakage in session history** – `<turn_meta>` blocks reappearing on reopen (#4681) degrades the reading experience for long‑running sessions.
- **Sandbox boundary override incomplete** – `danger-full-access` does not truly disable the tools‑layer workspace check (#4684), forcing users to work around read/write limitations.
- **Flaky DeepSeek completions URL** – Intermittent network errors (#4683) interrupt workflows, with no clear retry/diagnostics.
- **17 open dependency alerts** – The v0.9.1 security gate (#4713) lists 7 high‑severity npm vulnerabilities that must be resolved before release.
- **High maintenance overhead from rapid development** – The “CodeWhale tsunami” (#4227) highlights the difficulty of keeping local environments in sync with 10+ PRs per day.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*