# AI CLI Tools Community Digest 2026-06-11

> Generated: 2026-06-11 02:53 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Ecosystem Comparison Report
**Date:** 2026-06-11 | **Prepared by:** Senior Technical Analyst

---

## 1. Ecosystem Overview

The AI CLI tools landscape in mid-2026 is marked by a tension between rapid feature expansion and foundational stability gaps. Seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and CodeWhale (formerly DeepSeek TUI)—are all actively competing for developer mindshare, yet every tool exhibits unresolved regressions in memory management, cross-platform compatibility, and model behavior reliability. A clear convergence is emerging around multi-agent workflows, provider fallback chains, and context budget transparency, but no tool has achieved production-grade maturity across all operating systems. The community is increasingly vocal about trust issues—silent failures, fabricated model intents, and unresponsive maintainers on critical bugs are driving users toward self-hosted alternatives and forks.

---

## 2. Activity Comparison (Last 24 Hours)

| Tool | Hot Issues | Key PRs | Releases (24h) | Community Signal |
|---|---|---|---|---|
| **Claude Code** | 10 active | 10 merged/updated | v2.1.172 | High engagement; #18435 (580👍) remains top pain point |
| **OpenAI Codex** | 10 active | 10 open | rust-v0.140.0-alpha.4 & .7 | Token burn (#14593, 604 comments) dominating discourse |
| **Gemini CLI** | 10 active | 10 (3 closed, 7 open) | None | PR velocity high; P1 shell hang fix landing |
| **GitHub Copilot CLI** | 10 active | 0 updated | None | Low maintainer responsiveness; #53 unanswered 6 months |
| **Kimi Code CLI** | 3 active | 8 merged, 2 open | None | Bug-fix cycle focused on Windows/Nix parity |
| **OpenCode** | 10 active | 10 open | v1.17.0–1.17.3 | High release velocity; desktop crash fix urgent |
| **Pi** | 10 active | 10 (7 closed, 3 open) | None | Provider integration pace high; TUI fragility |
| **Qwen Code** | 10 active | 10 (3 closed, 7 open) | None | Daemon-mode feature batch (115k LOC) in review |
| **CodeWhale (DeepSeek TUI)** | 10 active | 10 open | v0.8.57 (rebrand) | Rebrand migration causing config confusion |

**Key observation:** OpenCode leads in release cadence (4 versions today), while GitHub Copilot CLI shows the lowest maintainer responsiveness. Gemini CLI and Qwen Code have the highest PR throughput relative to issues.

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities:

| Shared Need | Affected Tools | Specific Requirements |
|---|---|---|
| **Multi-account / profile switching** | Claude Code (#18435, 580👍), Copilot CLI (#223, 76👍) | One-click account switching without re-authentication |
| **Cross-platform parity (Windows)** | Claude Code (#50674, ARM64), Codex (#13553, non-ASCII usernames; #23198, slow), Kimi Code CLI (log collisions, console font), OpenCode (#6490, folder browsing), Pi (#4160, Bun), Qwen Code (#4901, SYSTEM install) | Windows is consistently a second-class citizen; many bugs unaddressed for 3+ months |
| **Context/token budget visibility** | Codex (#14593, token burn; #27518, context-remaining tool; #27488, new context-window tool), Pi (#5603, cache pricing), OpenCode (#450, reasoning effort UI), Qwen Code (#4951, token count accuracy) | Users demand real-time token consumption feedback and proactive compaction |
| **Sub-agent reliability & autonomy** | Claude Code (#64260, fabricated intents), Gemini CLI (#21409, hangs; #22323, false success), Copilot CLI (#3547, hangs at turn=0), Qwen Code (#4876, image reading failures), CodeWhale (#1806, 120s timeouts) | Sub-agents fail silently, over-report success, or hang indefinitely |
| **Provider fallback / multi-provider routing** | CodeWhale (#2574, auto-fallback on API failure), Pi (#5605, MiniMax caching issue), OpenCode (#31247, Opus 4.8 tool-call leaks), Gemini CLI (#24246, >128 tool limit) | Automatic failover on quota exhaustion or provider errors |
| **MCP/plugin ecosystem stability** | Claude Code (#64607, incorrect .mcp.json), Copilot CLI (#1707, MCP blocked by policy), Kimi Code CLI (#2355, MCP startup failures), OpenCode (#6330, generic UI intent channel) | MCP integration points are fragile and inconsistently documented |
| **Clipboard / input handling** | Claude Code (#66192, macOS copy-paste), Copilot CLI (#2082, Ctrl+Shift+C on Linux), Pi (#5598, multiline paste in Termux), Qwen Code (#4974, SGR mouse leaks) | All platforms affected; regressions in basic terminal I/O |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|
| **Primary strength** | Deep sub-agent recursion (5 levels); MCP hook system | Token budget tools; context-awareness | Security hardening (IPI protection, path traversal) | VS Code parity; enterprise auth | Feature velocity (4 releases/day) | Provider-agnostic; 10+ backend support | Daemon mode; ACP/REST parity | User-configurable provider chains |
| **Primary weakness** | Memory leaks (129GB); model compliance issues | Windows crashes; token burn unpredictability | Agent hangs; sub-agent under-utilisation | Maintainer unresponsiveness; model list disparity | Recent stability regressions (CPU, crashes) | TUI fragility; stream timeouts | Input handling fragility; sub-agent confusion | Rebrand migration pain; config fragmentation |
| **Target user** | Enterprise teams on macOS/Linux | Power users needing cross-platform | Security-aware developers | GitHub ecosystem users | Hackers/early adopters | Multi-provider power users | Asian/global devs; multi-model | Cloud-native devs; US VPS runners |
| **Technical approach** | Deep agent hierarchy + plugin SDK | Context compaction + model metadata | AST-aware tooling + HITL protection | VS Code extension parity | Plugin architecture + Zen account | Provider abstraction layer | Daemon-mode + ACP protocol | Remote workbench + Telegram integration |

---

## 5. Community Momentum & Maturity

| Tool | Momentum | Maturity Level | Signal |
|---|---|---|---|
| **Claude Code** | 🔥 High | **Adolescent** – Many features but critical reliability gaps | 580👍 issue indicates strong demand but unresolved pain |
| **OpenAI Codex** | 🔥 High | **Adolescent** – Token burn anxiety is systemic | 604 comments on #14593 shows deep trust erosion |
| **Gemini CLI** | 📈 Strong | **Maturing** – Security posture strong; hang issues remain | PR velocity suggests active dev investment |
| **Copilot CLI** | 🟡 Weak | **Stagnating** – No response on top issue (6 months) | Community forking signals abandonment risk |
| **Kimi Code CLI** | 🟢 Growing | **Early** – Focused on Windows parity; small community | Low issue volume indicates smaller but engaged user base |
| **OpenCode** | 📈 Strong | **Maturing quickly** – High release cadence but stability regressions | 4 versions in 24h suggests rapid iteration |
| **Pi** | 🟢 Growing | **Maturing** – Provider diversity strong; TUI needs polish | 10+ provider integrations; active PR pipeline |
| **Qwen Code** | 🟢 Growing | **Adolescent** – Daemon mode signals enterprise ambitions | 115k LOC feature batch indicates major investment |
| **CodeWhale** | 🟢 Growing | **Early/Transitioning** – Rebrand causing friction but autonomous agent vision clear | Remote workbench + Telegram control is a unique differentiator |

**Maturity scale:** *Early → Transitioning → Adolescent → Maturing → Mature*

---

## 6. Trend Signals (Key Takeaways for Developers)

1. **Cross-platform parity is the #1 unresolved systemic issue.** Every Windows-specific bug reported today (non-ASCII usernames, ARM64 crashes, console font resets, log file collisions) has been open for 3+ months. Teams targeting Windows developers should factor in significant platform friction.

2. **Token consumption anxiety is reaching a tipping point.** With Codex (#14593) and Pi (#5603) both generating high engagement around unpredictable billing, the market is ready for transparent, real-time cost telemetry tools. Expect this to become a product differentiator in H2 2026.

3. **Sub-agent orchestration remains immature across the board.** False success reports (Gemini #22323, CodeWhale #2989), silent hangs (Copilot #3547, Gemini #21409), and fabricated intents (Claude #64260) indicate that multi-agent coordination is still a research-level problem. Do not yet rely on sub-agents for safety-critical workflows.

4. **Model behavior compliance is deteriorating with newer model versions.** Multiple tools report that Opus 4.8, Fable 5, and GPT-5-series models increasingly skip user-defined workflows, fabricate intents, or produce false safety triggers. Agentic code generation tools need better model-locking and deterministic behavior guarantees.

5. **MCP ecosystem is growing but fragile.** Incorrect documentation (Claude Code #64607), policy blocks (Copilot #1707), and startup failures (Kimi #2355) are common. The MCP standard lacks robust tool validation and schema enforcement—as Qwen Code's #4966 (numeric string rejection) shows.

6. **Rebranding and migration cause disproportionate friction.** CodeWhale's rebrand from DeepSeek TUI has triggered config fragmentation, missing changelogs, and confused error messages. Teams considering rebranding should budget 2–3 months of migration support.

7. **Self-hosted/autonomous agent infrastructure is emerging as a distinct category.** CodeWhale's DigitalOcean + Telegram remote workbench and Pi's push for headless agent harnesses signal a shift from interactive CLIs to unattended agent runners. This is likely the next battleground.

---

**Bottom line for technical decision-makers:** No current AI CLI tool is production-ready across all operating systems. OpenCode offers the best feature velocity for early adopters; Gemini CLI has the strongest security posture; Pi provides the widest provider flexibility. For enterprise deployments requiring reliability, wait for memory leak fixes (Claude #11315) and cross-platform stability improvements (Codex, Copilot CLI). The tools with the highest community engagement are also the ones with the most unresolved pain—this is a market still finding its product-market fit.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-11 from github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following open Pull Requests represent the most-discussed Skill submissions, ranked by community engagement (comments and attention). All remain open as of the snapshot date.

### #1 – Document Typography Skill (`document-typography`)
**PR:** [#514](https://github.com/anthropics/skills/pull/514)  
**Author:** PGTBoos · Opened: 2026-03-04 · Updated: 2026-03-13  

**Functionality:** Prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment in AI-generated documents. Addresses a universal pain point across all Claude-generated content.

**Discussion highlights:** The skill strikes a chord with users who frequently encounter typographic issues in document outputs. The PR’s summary argues these defects affect every document Claude generates yet are rarely requested explicitly by users.

**Status:** Open

---

### #2 – ODT Skill (`odt`)
**PR:** [#486](https://github.com/anthropics/skills/pull/486)  
**Author:** GitHubNewbie0 · Opened: 2026-03-01 · Updated: 2026-04-14  

**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Triggers on mentions of “ODT”, “ODS”, “ODF”, “OpenDocument”, or “LibreOffice document”.

**Discussion highlights:** Fills a gap in the document-skills collection for ISO-standard open-source formats. The broad trigger set and conversion features attracted attention from users working with LibreOffice and enterprise document workflows.

**Status:** Open

---

### #3 – Frontend Design Skill Clarity & Actionability (`frontend-design`)
**PR:** [#210](https://github.com/anthropics/skills/pull/210)  
**Author:** justinwetch · Opened: 2026-01-05 · Updated: 2026-03-07  

**Functionality:** Revises the existing `frontend-design` skill to improve clarity, actionability, and internal coherence. Ensures every instruction is something Claude can follow within a single conversation, with specific guidance to steer behavior.

**Discussion highlights:** The PR sparked conversation about skill design philosophy—balancing prescriptive instructions with adaptability. Multiple reviewers weighed in on wording and scope.

**Status:** Open

---

### #4 – Meta-Skills: Quality Analyzer & Security Analyzer (`skill-quality-analyzer`, `skill-security-analyzer`)
**PR:** [#83](https://github.com/anthropics/skills/pull/83)  
**Author:** eovidiu · Opened: 2025-11-06 · Updated: 2026-01-07  

**Functionality:** Two meta-skills for evaluating other skills: quality analyzer scores structure, documentation, reliability, usability, and portability across five dimensions; security analyzer checks for unsafe patterns, prompt injection, and exfiltration vectors.

**Discussion highlights:** One of the earliest meta-skill proposals. Community interest centered on the need for a standardised quality baseline as the skill ecosystem grows. The security analyzer addresses a growing concern around trust-boundary abuse (see Issue #492).

**Status:** Open

---

### #5 – SAP Predictive Analytics Skill (`SAP-RPT-1-OSS`)
**PR:** [#181](https://github.com/anthropics/skills/pull/181)  
**Author:** amitlals · Opened: 2025-12-28 · Updated: 2026-03-16  

**Functionality:** Integrates SAP’s open-source tabular foundation model (SAP-RPT-1-OSS) for predictive analytics on SAP business data. Enables Claude to leverage the model for forecasting and analysis within enterprise contexts.

**Discussion highlights:** A niche but highly specific enterprise skill. Discussion focused on the skill’s integration approach and the potential for similar “model-bridging” skills.

**Status:** Open

---

### #6 – Testing Patterns Skill (`testing-patterns`)
**PR:** [#723](https://github.com/anthropics/skills/pull/723)  
**Author:** 4444J99 · Opened: 2026-03-22 · Updated: 2026-04-21  

**Functionality:** Covers the full testing stack: testing philosophy (Testing Trophy model), unit testing (AAA pattern, naming, edge cases), React component testing with Testing Library, and guidance on what to test vs. what not to test.

**Discussion highlights:** High demand for a dedicated testing skill was evident. The PR received constructive feedback on balancing comprehensiveness with token efficiency.

**Status:** Open

---

### #7 – Sensory Skill (macOS Automation via AppleScript, `sensory`)
**PR:** [#806](https://github.com/anthropics/skills/pull/806)  
**Author:** AdelElo13 · Opened: 2026-03-29 · Updated: 2026-04-02  

**Functionality:** Teaches Claude to use `osascript` (AppleScript) for native macOS automation, replacing screenshot-based computer use. Features a two-tier permission system: Tier 1 works out-of-the-box (direct app scripting), Tier 2 requires Accessibility permissions for System Events UI scripting.

**Discussion highlights:** The skill’s permission model and the move away from vision-based automation generated significant debate. It addresses a core performance bottleneck for macOS users.

**Status:** Open

---

### #8 – Codebase Inventory Audit Skill (`codebase-inventory-audit`)
**PR:** [#147](https://github.com/anthropics/skills/pull/147)  
**Author:** p19dixon · Opened: 2025-12-16 · Updated: 2026-02-04  

**Functionality:** Systematic 10-step workflow for identifying orphaned code, unused files, documentation gaps, and infrastructure bloat. Produces a single `CODEBASE-STATUS.md` source-of-truth document.

**Discussion highlights:** One of the most pragmatic skills for maintaining large codebases. The structured workflow approach was well-received, though some raised concerns about token consumption in large repositories.

**Status:** Open

---

## 2. Community Demand Trends

Analysis of the top Issues by comment count reveals the community’s most-anticipated Skill directions and ecosystem needs:

| Direction | Evidence |
|-----------|----------|
| **Organisational skill sharing & management** | Issue [#228](https://github.com/anthropics/skills/issues/228) (13 comments) requests org-wide skill sharing in Claude.ai. Users want to distribute skills without manual file transfers. |
| **Skill development tooling & reliability** | Issue [#556](https://github.com/anthropics/skills/issues/556) (12 comments) reports zero trigger rate in `run_eval.py`. Issues [#202](https://github.com/anthropics/skills/issues/202) and [#1169](https://github.com/anthropics/skills/issues/1169) further highlight friction in the skill creation/optimisation pipeline. |
| **Security & trust boundaries** | Issue [#492](https://github.com/anthropics/skills/issues/492) (7 comments) raises the risk of community skills impersonating official Anthropic skills under the `anthropic/` namespace. Demand for security-aware skills and namespace governance is clear. |
| **Duplicate skill detection / deduplication** | Issue [#189](https://github.com/anthropics/skills/issues/189) (6 comments) notes that `document-skills` and `example-skills` plugins install identical content. A deduplication or conflict-resolution skill is implicitly demanded. |
| **Agent governance patterns** | Issue [#412](https://github.com/anthropics/skills/issues/412) (4 comments, closed) proposed an `agent-governance` skill covering policy enforcement, threat detection, trust scoring, and audit trails. Though closed, the topic resonates. |
| **Platform portability (Bedrock, Windows)** | Issue [#29](https://github.com/anthropics/skills/issues/29) (4 comments) asks about Bedrock compatibility; multiple Windows-bug PRs (e.g., [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050)) indicate cross-platform demand. |
| **MCP integration** | Issue [#16](https://github.com/anthropics/skills/issues/16) (4 comments) proposes exposing Skills as MCP tools. This would allow Skills to interoperate with the broader MCP ecosystem. |
| **Multi-file reference bundling** | Issue [#1220](https://github.com/anthropics/skills/issues/1220) (2 comments) requests inline bundling of supplementary reference files (e.g., `refs/*.md`) into a single `SKILL.md` to avoid delivery gaps. |

**Bottom line:** The community is demanding **infrastructure and governance**—skills for managing, sharing, securing, and quality-checking other skills—over new domain-specific skills.

---

## 3. High-Potential Pending Skills

Several open PRs have active discussion and are likely to be merged in the near term:

| Skill (PR) | Why It May Land Soon |
|------------|----------------------|
| **Frontend Design Clarity** ([#210](https://github.com/anthropics/skills/pull/210)) – Long-running PR (since Jan 2026) with sustained updates; consensus-forming appears advanced. |
| **Meta-Quality & Security Analyzers** ([#83](https://github.com/anthropics/skills/pull/83)) – Oldest open skill PR (Nov 2025); foundational for ecosystem health. |
| **Testing Patterns** ([#723](https://github.com/anthropics/skills/pull/723)) – Fills a clear gap; few structural objections; active maintainer. |
| **Sensory / macOS Automation** ([#806](https://github.com/anthropics/skills/pull/806)) – Novel approach to computer use; permission design well-considered. |
| **Agent Creator** ([#1140](https://github.com/anthropics/skills/pull/1140)) – Addresses Issue #1120 with critical stability fixes, including Windows support and multi-tool evaluation. |
| **Codebase Inventory Audit** ([#147](https://github.com/anthropics/skills/pull/147)) – Practical, well-defined workflow; minimal technical controversy. |
| **Shodh-Memory Persistence** ([#154](https://github.com/anthropics/skills/pull/154)) – Addresses the cross-conversation memory gap; unique proposition. |
| **Windows Compatibility Fixes** ([#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050)) – Simple, targeted patches for critical bugs in `run_eval.py` and subprocess handling. Likely to be fast-tracked. |

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for meta-skills and infrastructure—tooling to create, validate, share, and secure skills—rather than new application-domain skills, reflecting an ecosystem that is maturing from creative experimentation toward production-grade governance and reliability.**

---

# Claude Code Community Digest — 2026-06-11

## Today's Highlights
Claude Code v2.1.172 shipped today with deep sub‑agent recursion (up to 5 levels), smarter AWS region resolution, and a mark‑browser search bar. The community reported a slew of critical model‑behavior regressions (Fable 5 false positives, Opus 4.8 fabricated intents) and renewed memory‑leak complaints that have drawn 64+ comments. A popular feature request for multi‑account profile switching remains the #1 upvoted issue at 580 👍.

## Releases
**v2.1.172** — [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.172)
- Sub‑agents can now spawn up to 5 levels of child agents (not just 1).
- Amazon Bedrock region now falls back to `~/.aws/config` when `AWS_REGION` is unset; `/status` displays the region source.
- Added a search bar when browsing a mark (presumably for markdown navigation / file picker).

## Hot Issues (10)

1. **#18435 — Multi‑account profile switching**  
   [Link](https://github.com/anthropics/claude-code/issues/18435)  
   The top‑requested enhancement (580 👍, 109 comments). Users want to manage several Claude accounts inside the Desktop app with one‑click switching. Still open after five months.  
   *Why it matters:* Enterprise teams and freelancers sharing a workstation need this for billing/org separation.

2. **#11315 — Critical memory leak (129 GB consumed)**  
   [Link](https://github.com/anthropics/claude-code/issues/11315)  
   A severe leak that froze a 16 GB machine, forcing a hard reboot. 64 comments, 52 👍. Still open since Nov 2025.  
   *Why it matters:* Unrecoverable system lockups undermine trust in long‑running agent sessions.

3. **#12513 — Disable automatic worktree creation**  
   [Link](https://github.com/anthropics/claude-code/issues/12513)  
   Closed after 46 comments. Solo devs wanted to opt out of git worktrees in the standalone macOS interface. Resolution pending final verification.

4. **#50674 — Cowork fails on ARM64 Windows (Snapdragon X)**  
   [Link](https://github.com/anthropics/claude-code/issues/50674)  
   Cowork passes readiness check but then silently fails on Qualcomm‑based Windows machines. 19 comments, no workaround known.

5. **#26996 — Edit tool converts tabs → spaces**  
   [Link](https://github.com/anthropics/claude-code/issues/26996)  
   The edit tool silently normalises tab‑indented files, causing repeated search‑and‑replace failures. 15 comments, 27 👍. A subtle but frustrating productivity killer for users with strict tab‑based style.

6. **#46767 — Tool results silently dropped on Windows (“missing due to internal error”)**  
   [Link](https://github.com/anthropics/claude-code/issues/46767)  
   Regression in v2.1.101 — all tools may lose their output without warning. 10 comments, 5 👍. Still open; affects Windows users disproportionately.

7. **#64260 — Opus 4.8 fabricated user intent**  
   [Link](https://github.com/anthropics/claude-code/issues/64260)  
   Model invented a present‑tense user request and persisted on an unrelated task context. 9 comments. Raises serious reliability concerns for agentic workflows.

8. **#49933 — Native WSL remote integration**  
   [Link](https://github.com/anthropics/claude-code/issues/49933)  
   Feature request for seamless Windows ↔ WSL development inside Claude Desktop. 55 👍, 9 comments. Duplicate of older requests.

9. **#66192 — Copy‑paste broken on macOS TUI**  
   [Link](https://github.com/anthropics/claude-code/issues/66192)  
   Recent version broke clipboard operations. 8 comments, 5 👍. High priority for daily use.

10. **#63909 — Bash tool ENOSPC on temp filesystem**  
    [Link](https://github.com/anthropics/claude-code/issues/63909)  
    Subprocess stdout captured to `/private/tmp` fills the (small) ramdisk, producing bogus ENOSPC errors. 8 comments, 16 👍. Impacts every command with non‑trivial output.

## Key PR Progress (10)

1. **[#66416] — fix(plugin‑dev): validator scripts abort on first finding due to `set -e`**  
   [PR](https://github.com/anthropics/claude-code/pull/66416)  
   Three validator scripts fail early when `set -euo pipefail` triggers on first error, instead of reporting all findings. Fixes a developer experience issue in the plugin SDK.

2. **[#67084] — Hookify prompt fields and warning context**  
   [PR](https://github.com/anthropics/claude-code/pull/67084)  
   Maps legacy `event: prompt` + `pattern:` rules to the new payload field, adds backward‑compatible alias, and includes additional context in warning responses for hook events.

3. **[#63382] — Fix Hookify tests example semantics**  
   [PR](https://github.com/anthropics/claude-code/pull/63382)  
   Clarifies that `not_contains` is substring‑based, not regex. Splits chained example into separate checks to avoid confusion.

4. **[#63460] — docs: update deprecated npm install instructions**  
   [PR](https://github.com/anthropics/claude-code/pull/63460)  
   Replaces `npm install -g` with recommended curl/irm methods; adds deprecation note.

5. **[#63686] — Bump stale and autoclose timeouts from 14 to 90 days**  
   [PR](https://github.com/anthropics/claude-code/pull/63686)  
   Responds to community feedback that 14 days was too aggressive for issue closure. Stale/autoclose thresholds increased six‑fold.

6. **[#64607] — Fix `.mcp.json` example incorrectly using `mcpServers` wrapper**  
   [PR](https://github.com/anthropics/claude-code/pull/64607)  
   The documentation showed a nested `mcpServers` key that belongs in `plugin.json`, not `.mcp.json`. Corrects the flat‑structure syntax.

7. **[#65286] — fix(plugins): add missing plugin.json manifest for plugin‑dev**  
   [PR](https://github.com/anthropics/claude-code/pull/65286)  
   The plugin‑dev plugin lacked a `plugin.json`, preventing discovery and installation through normal plugin channels.

8. **[#65875] — fix: Forward ANTHROPIC_BASE_URL to agentic_review child process**  
   [PR](https://github.com/anthropics/claude-code/pull/65875)  
   Proxy/gateway setups (LiteLLM, Bifrost) with OAuth tokens failed because the advisor child process didn’t inherit `ANTHROPIC_BASE_URL`. Critical for self‑hosted deployments.

9. **[#65916] — docs: clarify allowed‑tools vs agent tools enforcement**  
   [PR](https://github.com/anthropics/claude-code/pull/65916)  
   Documents that `allowed-tools` is an auto‑approve filter (not a capability boundary), while `tools:` in subagent frontmatter is a hard restriction.

10. **[#66372] — fix(devcontainer): detect Docker daemon failures via $LASTEXITCODE**  
    [PR](https://github.com/anthropics/claude-code/pull/66372)  
    PowerShell’s `try/catch` doesn’t catch native command failures. Replaces with explicit `$LASTEXITCODE` check so offline Docker Desktop is correctly reported.

## Feature Request Trends

- **Multi‑account/profile management** (#18435, 580 👍) — by far the most wanted. Users need to switch between personal, work, and team Claude accounts without re‑authentication.
- **WSL remote integration** (#49933, 55 👍) — Windows developers want Claude Desktop to natively connect to WSL environments, avoiding the friction of SSH workarounds.
- **Disable automatic worktree creation** (#12513, closed) — solo developers on macOS want granular control over git workflow automation.
- **Improved model‑behavior documentation & guardrails** — several recent issues (#54117, #49259, #65951) ask for better compliance with user‑defined workflows (plan → review → test → ship). This is a cross‑model trend.

## Developer Pain Points

- **Model non‑compliance with user workflows** — Opus 4.6–4.8 repeatedly skip multi‑step gates defined in `CLAUDE.md`. Three separate issues spanning months (#49259, #54117, #65951) with 41+ logged violations.
- **Fable 5 over‑blocking** — false safety flags on legitimate security research, CTI, and bug reproduction steps (#67305, #67304, #67302). Fable 5’s safety filter triggers on nearly every task, forcing fallback to Opus 4.8.
- **Memory leaks** (#11315, 129 GB; plus the ‘!yes’ crash #65789 that fills temp storage) remain a critical unresolved class of bugs.
- **Tool‑level regressions** — tab‑to‑space conversion (#26996), silent output drops on Windows (#46767), copy‑paste broken on macOS (#66192), and bash ENOSPC on temp filesystems (#63909) erode daily usability.
- **Permissions approval spam** — the system prompt encourages shell command substitution (`$(...)`), which triggers repeated permission dialogs (#31373). A systemic prompt‑engineering issue.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-11

## Today’s Highlights
Today’s data reveals a continued focus on stability and performance, with two minor alpha releases and a flood of Windows-specific crash reports. The most discussed issue remains **#14593** (token burning) with over 600 comments and 265 👍, reflecting ongoing community anxiety around usage costs. Notable pull requests push forward context-awareness tools (compaction hash, context window tool) and improve TUI goal handling for images and long text, signaling a push toward smarter resource management.

## Releases
- **rust-v0.140.0-alpha.7** and **rust-v0.140.0-alpha.4** – Both are labelled only as “Release 0.140.0-alpha.*” with no detailed changelog. Likely daily builds for the Rust-based CLI; no breaking changes or feature announcements surfaced.

## Hot Issues (10 noteworthy)
1. **#14593 – Burning tokens very fast** – 604 comments, 265 👍.  
   The community’s top pain point: users on Business/Pro subscriptions see aggressive token consumption even with light use. OpenAI has not yet provided a root cause or mitigation.  
   [GitHub](https://github.com/openai/codex/issues/14593)

2. **#26867 – GitHub PR review still uses deactivated workspace after migration** – 13 comments.  
   A migration bug: switching from Business to Personal Pro leaves the GitHub integration pointing at a deactivated workspace, blocking PR reviews. Affects account transitions.  
   [GitHub](https://github.com/openai/codex/issues/26867)

3. **#25463 – Desktop project threads disappear from views while session JSONL remains** – 12 comments.  
   Local conversations become invisible in the UI but remain on disk. Several duplicate reports exist (#20833, #22796). Likely a session indexing bug.  
   [GitHub](https://github.com/openai/codex/issues/25463)

4. **#17642 – “gpt-5.3-codex-spark” model not supported with ChatGPT account** – 12 comments.  
   CLI users on Pro plan receive a 400 error when trying the Spark model. Model-account compatibility mismatch.  
   [GitHub](https://github.com/openai/codex/issues/17642)

5. **#23198 – Codex Desktop on Windows extremely slow** – 12 comments, 31 👍.  
   Performance degradation isolated to the Windows desktop app, unrelated to machine load. Affects day-to-day development sessions.  
   [GitHub](https://github.com/openai/codex/issues/23198)

6. **#13553 – Windows Store app fails to start for usernames with non-ASCII characters** – 11 comments.  
   Long-standing bug (since March) – crashes on first launch for users with e.g. Korean, Chinese characters in their Windows username. Still unaddressed.  
   [GitHub](https://github.com/openai/codex/issues/13553)

7. **#27175 – Desktop crashes / becomes inaccessible after update 26.602.71036** – 8 comments.  
   Windows 11 users (Pro plan) report blank or crashing app after latest update, even with empty sessions. Crashpad dumps generated.  
   [GitHub](https://github.com/openai/codex/issues/27175)

8. **#27491 – Severe streaming slowdown in Fast mode** – 6 comments.  
   macOS Pro user sees only a few characters every several seconds then stalls. Occurs with GPT-5.5 Fast mode on Apple Silicon.  
   [GitHub](https://github.com/openai/codex/issues/27491)

9. **#27296 – Fn global dictation hotkey stops working after update** – 4 comments, 9 👍.  
   macOS update to 26.608.12217 breaks the system-wide dictation hotkey. Likely a key interception bug in the Codex renderer.  
   [GitHub](https://github.com/openai/codex/issues/27296)

10. **#26743 – Locked Computer Use stays on loginwindow** – 4 comments.  
    When Mac is locked, Computer Use can only see `loginwindow`. Temporary unlock path not triggered for allowed apps.  
    [GitHub](https://github.com/openai/codex/issues/26743)

## Key PR Progress (10 important)
1. **#27266 – Preserve image metadata when resizing prompt images** – Open.  
   Stops stripping ICC profiles and EXIF orientation during resize (PNG/JPEG/WebP). Important for design workflows.  
   [GitHub](https://github.com/openai/codex/pull/27266)

2. **#27518 – Add context remaining tool** – Open.  
   Allows the model to query remaining token budget on demand, rather than relying on injected notices.  
   [GitHub](https://github.com/openai/codex/pull/27518)

3. **#27510 – Support images in TUI goals** – Open (3 of 3 stack).  
   Enables `/goal` to accept and pass image inputs within the CLI. Complements the long-text PRs below.  
   [GitHub](https://github.com/openai/codex/pull/27510)

4. **#27509 – Support long pasted text in TUI goals** – Open.  
   Handles large text pastes in the TUI composer by using a placeholder + pending metadata pattern.  
   [GitHub](https://github.com/openai/codex/pull/27509)

5. **#27508 – Support long raw TUI goal objectives** – Open.  
   Removes the 4000-character limit on `/goal` objective text.  
   [GitHub](https://github.com/openai/codex/pull/27508)

6. **#27454 – Add cross-platform filesystem adapter coverage** – Open.  
   Extends exec-server file tests to Windows, improving parity for path handling.  
   [GitHub](https://github.com/openai/codex/pull/27454)

7. **#27520 – Compact when `comp_hash` changes** – Open.  
   Persists compaction-compatibility hash across turns and triggers recompaction when the model configuration changes.  
   [GitHub](https://github.com/openai/codex/pull/27520)

8. **#27519 – Add `comp_hash` to model metadata** – Open.  
   Adds an opaque compaction identifier to `ModelInfo`, enabling the logic in #27520.  
   [GitHub](https://github.com/openai/codex/pull/27519)

9. **#27488 – Add new context window tool** – Open.  
   Lets the model request a fresh context window instead of spending tokens on compaction summaries.  
   [GitHub](https://github.com/openai/codex/pull/27488)

10. **#27415 – Surface runtime warnings in `codex exec`** – Open.  
    Prevents silent dropping of thread-scoped warnings (e.g., unreadable `AGENTS.md`). Improves debugging for CLI users.  
    [GitHub](https://github.com/openai/codex/pull/27415)

## Feature Request Trends
- **Context & budget management**: Multiple issues and PRs revolve around better visibility and control of token consumption (see #14593, #27518, #27488, #21777). The “auto compaction” request (#21777) is a clear signal: users want agents to proactively compact before filling the window.
- **Cross-platform parity**: Windows-specific issues dominate the bug list. Requests for feature parity (e.g., Computer Use bundled plugin visibility #27493) and stable file system handling (#27454) reflect a push for Windows to be a first-class platform.
- **Subagent & tool reliability**: Several issues (#26753, #23496, #23971) highlight confusion around subagent schema, skill instructions, and agent loop crashes. Users want transparent and reliable multi-agent workflows.
- **Account/workspace integration**: Migration bugs (#26867) and auth model mismatches (#17642) indicate a need for smoother transitions between personal and business accounts.

## Developer Pain Points
- **Windows crash spiral**: The most acute frustration. Crashes on startup (#13553, #25807, #27320, #27175), especially after updates and with non-ASCII usernames (#27506), make the app unusable for a significant minority.
- **Invisible sessions**: Reports of project conversations disappearing from the UI while data remains on disk (#25463, #20833, #22796, #27363) erode trust in local storage reliability.
- **Performance regressions**: Slow streaming (#27491) and general Windows slowness (#23198) are not isolated incidents – users feel updates degrade performance.
- **Token consumption anxiety**: The top-voted issue (#14593) shows that even with paid subscriptions, unpredictable token burn is a major blocker for everyday use.
- **Lock-in to specific models/accounts**: Users who upgrade or change accounts face opaque errors (#17642, #26867) that halt workflows entirely.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-11

**Today's Highlights**  
The team landed a critical fix for long-standing shell command hangs (PR #27842) and merged several security patches covering hostname resolution, HITL bypass protection, and path traversal during skill install. Meanwhile, community frustration around agent hang and “thinking too long” scenarios continues, with a new high‑engagement issue (#27785) reported yesterday.

---

## Releases  
*No new releases in the last 24 hours.*

---

## Hot Issues (10 selected)

1. **#21409 – Generalist agent hangs**  
   *Priority P1, 8 👍, 7 comments*  
   The CLI hangs indefinitely when deferring to the generalist agent. Workaround: instruct the model not to use sub‑agents. This remains one of the most upvoted bugs.  
   https://github.com/google-gemini/gemini-cli/issues/21409

2. **#25166 – Shell command execution gets stuck with “Waiting input”**  
   *Priority P1, 3 👍, 4 comments*  
   After a simple CLI command finishes, the shell indicator still shows “awaiting user input”. A fix is already in review (PR #27842).  
   https://github.com/google-gemini/gemini-cli/issues/25166

3. **#22323 – Subagent recovery after MAX_TURNS is reported as GOAL success**  
   *Priority P1, 2 👍, 6 comments*  
   The `codebase_investigator` subagent reports success even when it hit the turn limit without any analysis, hiding the interruption.  
   https://github.com/google-gemini/gemini-cli/issues/22323

4. **#21968 – Gemini does not use skills and sub‑agents enough**  
   *Priority P2, 6 comments*  
   Users report that custom skills and sub‑agents are rarely invoked autonomously. Explicit instructions are required, defeating the purpose.  
   https://github.com/google-gemini/gemini-cli/issues/21968

5. **#24246 – 400 error with >128 tools**  
   *Priority P2, 3 comments*  
   The CLI hits a 400 error when more than ~128 tools are available. Expectation: smarter tool limiting.  
   https://github.com/google-gemini/gemini-cli/issues/24246

6. **#27785 – “thinking too long, do nothing”**  
   *Priority P2, 3 comments (created 2026-06-10)*  
   User reports the CLI stays stuck on “Thinking …” with no output. No chat log attached yet.  
   https://github.com/google-gemini/gemini-cli/issues/27785

7. **#26525 – Add deterministic redaction and reduce Auto Memory logging**  
   *Priority P2, 5 comments*  
   Sensitive content is sent to the model before redaction; the extraction agent logs existing skills. A security‑privacy concern.  
   https://github.com/google-gemini/gemini-cli/issues/26525

8. **#22267 – Browser Agent ignores settings.json overrides**  
   *Priority P2, 3 comments*  
   `maxTurns` and other settings defined in `settings.json` are not respected by the browser sub‑agent.  
   https://github.com/google-gemini/gemini-cli/issues/22267

9. **#22093 – Subagents running without permission since v0.33.0**  
   *Priority P2, 2 comments*  
   Sub‑agents are activated even when agent mode is disabled in all configurations. Regression after update.  
   https://github.com/google-gemini/gemini-cli/issues/22093

10. **#22672 – Agent should stop/discourage destructive behavior**  
    *Priority P2, 1 👍, 2 comments*  
    The model occasionally issues destructive commands (e.g., `git reset --force`) when safer alternatives exist.  
    https://github.com/google-gemini/gemini-cli/issues/22672

---

## Key PR Progress (10 selected)

1. **#27842 – fix(core): never let shell exit results hang on the output drain**  
   *P1, size/L, opened today*  
   Directly addresses #25166. Prevents the CLI from staying stuck after a shell command completes by adding error handling and a bound to the PTY output‑processing chain.  
   https://github.com/google-gemini/gemini-cli/pull/27842

2. **#27473 – fix(security): resolve hostnames before private‑IP check**  
   *size/M, closed*  
   `isBlockedHost()` now resolves hostnames to IPs before validating, preventing DNS‑based private‑IP bypass.  
   https://github.com/google-gemini/gemini-cli/pull/27473

3. **#27502 – fix(core): resolve P1 crash during terminal resize (ioctl EBADF)**  
   *P1, size/M, closed*  
   Fixes a race condition where the PTY resize callback fires after the shell has exited, causing an `ioctl EBADF` crash.  
   https://github.com/google-gemini/gemini-cli/pull/27502

4. **#27474 – fix(core): guard isFunctionCall/isFunctionResponse against empty parts**  
   *P2, size/L, closed*  
   `Array.prototype.every([])` returned `true`, incorrectly classifying messages with empty parts as function calls/responses.  
   https://github.com/google-gemini/gemini-cli/pull/27474

5. **#27472 – fix(ui): enforce truncation lockout for tool confirmations to prevent IPI**  
   *P1, size/M, closed*  
   Implements a “truncation lockout” to prevent indirect prompt injection (IPI) by requiring users to expand truncated commands/diffs before confirming.  
   https://github.com/google-gemini/gemini-cli/pull/27472

6. **#27648 – feat(core): support list format in trustedFolders.json**  
   *P3, size/M, open*  
   Adds support for a JSON array format alongside the existing object format, making manual maintenance easier.  
   https://github.com/google-gemini/gemini-cli/pull/27648

7. **#27767 – fix(cli): prevent path traversal vulnerabilities during skill install**  
   *size/M, open*  
   Mitigates three path traversal issues in `installSkill`, `linkSkill`, and `uninstallSkill`.  
   https://github.com/google-gemini/gemini-cli/pull/27767

8. **#27753 – ci: validate workflow_run origin before consuming the E2E artifact**  
   *size/S, open*  
   Prevents fork PR artifact poisoning in the chained E2E pipeline by verifying `repo.full_name` and `sha`.  
   https://github.com/google-gemini/gemini-cli/pull/27753

9. **#27839 – fix(core): make read_background_output delay abort‑aware**  
   *size/S, open*  
   When ESC is pressed to cancel a `read_background_output` call, the tool’s `setTimeout` now respects the abort signal, preventing queued prompts.  
   https://github.com/google-gemini/gemini-cli/pull/27839

10. **#27698 – fix(core): Ensure zero‑quota limits fail fast to prevent retry loop hang**  
    *size/S, open*  
    Prevents a 10‑attempt retry loop when hitting a hard zero‑quota limit (e.g., unbilled free‑tier accounts).  
    https://github.com/google-gemini/gemini-cli/pull/27698

---

## Feature Request Trends

- **AST‑aware tooling** – Several issues (#22745, #22746, #22747) propose using Abstract Syntax Tree aware file reads, search, and codebase mapping to improve agent precision and reduce token waste.
- **Remote agents & background operations** – Epic #20303 tracks advanced auth and background processing for remote agents; #22741 asks for the ability to send local sub‑agents to the background (Ctrl+B).
- **Browser agent resilience** – Request for automatic session takeover and lock recovery (#22232) to handle stale browser profiles.
- **Better agent self‑awareness** – #21432 calls for the CLI to accurately know its own flags, hotkeys, and execution mechanics so it can guide users.
- **Evaluation infrastructure** – #24353 (component‑level evaluations) and #23166 (stabilize internal evals) reflect a push to make testing more reliable and actionable.
- **Memory system improvements** – Issues #26516 and #26525 indicate demand for deterministic secret redaction, handling of low‑signal sessions, and quarantine of invalid memory patches.

---

## Developer Pain Points

- **Agent hangs** – Both the generalist agent (#21409) and silent “thinking” hangs (#27785) are top frustrations, with no clear feedback to users.
- **Shell command lifecycle** – Commands completing but leaving the UI stuck in “awaiting input” (#25166) is a common complaint.
- **Sub‑agent unreliability** – Sub‑agent recovery masking turn limits (#22323), running without permission (#22093), and under‑utilisation of skills (#21968) erode trust.
- **Configuration ignored** – Browser agent ignoring `settings.json` overrides (#22267) and agent mode settings being bypassed (#22093) break user control.
- **Tool limits & errors** – The 400 error with >128 tools (#24246) and the zero‑quota retry loop (#27698) block productivity.
- **Safety concerns** – Destructive commands (#22672

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-11

## Today’s Highlights
A significant outage of community patience is visible: the most‑reacted issue [#53](#53) (75 👍, 34 comments) has received no official response in six months, prompting users to roll their own CLI replacements. Model disparity between the CLI and VS Code continues to frustrate, with Gemini models missing from the CLI despite being enabled in organization policies. Recent version v1.0.60 introduced a plugin regression that broke context injection, and multiple reports of garbled streaming output and broken clipboard behavior are piling up.

## Releases
No new releases in the last 24 hours.

## Hot Issues
*10 noteworthy issues from the last 24h updates, chosen by community engagement and technical impact.*

- **[#53 – Bring back GitHub Copilot in the CLI commands to not break workflows](https://github.com/github/copilot-cli/issues/53)**  
  *75 👍, 34 comments* | This six‑month‑old issue is the most reacted. The community has started maintaining forks (e.g. `shell-ai`) due to the lack of official response. **Why it matters:** signals a trust gap and unmet need for backward‑compatibility.

- **[#1703 – Copilot CLI does not list all org-enabled models (e.g. Gemini 3.1 Pro) while VS Code does](https://github.com/github/copilot-cli/issues/1703)**  
  *54 👍, 31 comments* | Model list parity issue, closed but still unresolved for many. **Why it matters:** directly impacts enterprise users who pay for certain models.

- **[#223 – “Copilot Requests” permission missing for org‑owned fine‑grained tokens](https://github.com/github/copilot-cli/issues/223)**  
  *76 👍, 29 comments* | Organizations cannot create fine‑grained tokens with the Copilot permission scope. **Why it matters:** blocks enterprise automation without using personal PATs.

- **[#2082 – Ctrl+Shift+C no longer copies to clipboard on Linux](https://github.com/github/copilot-cli/issues/2082)**  
  *8 👍, 21 comments* | Keyboard shortcut conflicts with terminal standard. **Why it matters:** a regression that breaks a core workflow for Linux users.

- **[#1707 – 3rd party MCP servers disabled despite “no such policy”](https://github.com/github/copilot-cli/issues/1707)**  
  *0 👍, 9 comments* | Duplicated in [#3756](#3756). Users on personal accounts hit a policy block that doesn’t exist in VS Code. **Why it matters:** inconsistent policy enforcement erodes trust.

- **[#2334 – Please bring back no‑alt‑screen](https://github.com/github/copilot-cli/issues/2334)**  
  *28 👍, 7 comments* | The new alt‑screen mode disables scrollback and find. **Why it matters:** degrades terminal usability for reviewing long outputs.

- **[#2434 – Restore support for Gemini Pro](https://github.com/github/copilot-cli/issues/2434)**  
  *10 👍, 7 comments* | v1.0.14 dropped `gemini-3-pro-preview`. **Why it matters:** model choice was a key CLI differentiator; removal forces users to alternatives.

- **[#3547 – Background sub‑agent hangs at total_turns=0 with model=”gpt-5.5″](https://github.com/github/copilot-cli/issues/3547)**  
  *0 👍, 7 comments* | Silent hang when dispatching a background agent. **Why it matters:** breaks multi‑agent workflows with no error feedback.

- **[#3596 – Error loading model list: Not authenticated (session resume)](https://github.com/github/copilot-cli/issues/3596)**  
  *10 👍, 5 comments* | `/model` fails when resuming a session. **Why it matters:** session management is unreliable for long‑running tasks.

- **[#3727 – Regression in v1.0.60: userPromptSubmitted hook context no longer injected](https://github.com/github/copilot-cli/issues/3727)**  
  *0 👍, 3 comments* | A plugin regression broke custom context injection exactly at the v1.0.60 release boundary. **Why it matters:** shows inadequate testing for plugin API changes.

## Key PR Progress
No pull requests were updated or merged in the last 24 hours.

## Feature Request Trends
- **Model parity**: Users want the same model selection in the CLI as in VS Code, especially Gemini 3.1 Pro/Flash and other organisation‑enabled models ([#1664](#1664), [#821](#821), [#2550](#2550), [#2854](#2854)).
- **MCP improvements**: Requests for direct MCP tool invocation syntax, tab‑completion, and bypassing policy blocks ([#3752](#3752)).
- **Terminal rendering control**: A strong push to revert or make optional the alt‑screen mode and to fix streaming corruption ([#2334](#2334), [#3749](#3749), [#3755](#3755)).
- **Agent UX**: Better agent picklist scroll positioning ([#3751](#3751)) and audible task completion notifications ([#3748](#3748)).
- **Worktree safety**: Demand to disable worktree creation by default to avoid git chaos ([#2243](#2243)).

## Developer Pain Points
1. **Model availability inconsistency** – models enabled in org policy appear in VS Code but not in CLI, leading to confusion and wasted time.
2. **Authentication/session fragility** – `Not authenticated` errors when resuming sessions, especially after sensitive errors (image prompts, network failures).
3. **Clipboard breakage** – `Ctrl+Shift+C` on Linux and copy on Windows silently fail (regressions).
4. **MCP policy mismatches** – personal/org accounts falsely blocked from using third‑party MCP servers, no workaround short of downgrading.
5. **Plugin API stability** – v1.0.60 broke hook‑based context injection with no deprecation warning, eroding trust.
6. **Terminal output corruption** – streamed text contains doubled/truncated characters, making reasoning output unusable.
7. **Worktree over‑automation** – CLI creates thousands of worktrees without user consent, difficult to clean up.
8. **Lack of communication** – the longest‑standing, most‑voted issue [#53](#53) remains unanswered after six months, driving users to self‑hosted solutions.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-11

## Today's Highlights

No new releases landed in the last 24 hours, but the project saw active bug triage and a large batch of recently merged fixes being closed out. Two critical bugs were reported: the `--yolo` mode is failing to skip approval prompts, and the final todo item in agent runs never completes — both likely affecting users relying on fully autonomous workflows. On the PR side, several long-standing Windows-specific issues (console font reset, log file collisions, UTF-8 filename handling) have been merged and are now being finalised.

## Releases

*No new releases in the last 24 hours.*

## Hot Issues

1. **[#2448 – Kimi CLI is prompting for approval in yolo mode](https://github.com/MoonshotAI/kimi-cli/issues/2448)**  
   *Open, reported by iaindooley*  
   `--yolo` mode is supposed to run without manual intervention, but the user reports persistent approval prompts. This undermines the whole purpose of yolo mode for unattended automation. Zero comments so far, but likely to gather attention.

2. **[#2447 – Final Todo item never completes](https://github.com/MoonshotAI/kimi-cli/issues/2447)**  
   *Open, reported by iaindooley*  
   When the agent uses the “…” (presumably the final task marker), the last todo item hangs indefinitely. This points to a possible race condition or missing termination signal in the agent loop. Same reporter as #2448, suggesting a systematic testing effort.

3. **[#2173 – [enhancement] ! (title only)](https://github.com/MoonshotAI/kimi-cli/issues/2173)**  
   *Closed, reported by odellus*  
   Minimal description; likely a placeholder or test issue. No actionable insight into community feature requests.

## Key PR Progress

1. **[#2335 – docs: fix Notification hook matcher example](https://github.com/MoonshotAI/kimi-cli/pull/2335)**  
   *Merged* – Corrects broken documentation examples so that hook configs actually work with background-task notifications.

2. **[#2355 – fix: continue after deferred MCP startup failures](https://github.com/MoonshotAI/kimi-cli/pull/2355)**  
   *Merged* – Prevents an MCP server startup failure from aborting the entire interactive turn; the CLI now logs the error and continues without the unavailable server.

3. **[#2354 – fix: avoid shared rotating logs on Windows](https://github.com/MoonshotAI/kimi-cli/pull/2354)**  
   *Merged* – Introduces per-process log files (`kimi.<pid>.log`) on Windows to prevent concurrent CLI/web/worker processes from corrupting the same log file.

4. **[#2334 – fix(kosong): sanitize surrogates before Kimi requests](https://github.com/MoonshotAI/kimi-cli/pull/2334)**  
   *Merged* – Strips lone UTF-16 surrogate code units from prompts and tool-call arguments, preventing API rejections on certain malformed multi-byte sequences.

5. **[#2327 – fix: terminate shell process trees on timeout](https://github.com/MoonshotAI/kimi-cli/pull/2327)**  
   *Merged* – Shell commands now run in their own process group, so a timeout or cancellation kills the entire subprocess tree instead of leaving orphans.

6. **[#2289 – fix: avoid Windows console font reset](https://github.com/MoonshotAI/kimi-cli/pull/2289)**  
   *Merged* – Stops Kaos local subprocesses from inadvertently resetting the Windows console font by passing `CREATE_NO_WINDOW`.

7. **[#2288 – fix: avoid resending web uploads after restart](https://github.com/MoonshotAI/kimi-cli/pull/2288)**  
   *Merged* – Persists a “sent” marker so that already-uploaded files are not re-attached to a text-only prompt after a session restart.

8. **[#2239 – fix: continue latest persisted session](https://github.com/MoonshotAI/kimi-cli/pull/2239)**  
   *Merged* – Makes `--continue` fall back to the newest non-empty session for the working directory when the stored session ID is stale or missing.

9. **[#2387 – fix(tools): preserve shell command headline details](https://github.com/MoonshotAI/kimi-cli/pull/2387)**  
   *Open* – Long shell command headlines are currently truncated at 50 characters; this PR preserves the full command text in the UI for better debugging.

10. **[#2383 – fix(soul): repair orphan tool_calls when replaying history](https://github.com/MoonshotAI/kimi-cli/pull/2383)**  
    *Open* – If a session is killed mid-turn, the persisted `context.jsonl` can contain an orphan `tool_calls` entry that breaks replay. This PR adds proper recovery logic.

## Feature Request Trends

Only one enhancement issue (#2173) appears in the last 24 hours, and its title is a bare “!” — likely a mispost. The data suggests the community is currently focused on **stability and correctness** rather than new features. No clear pattern of feature requests can be derived from today’s data.

## Developer Pain Points

- **Yolo mode unreliability** – Approval prompts still appear even in `--yolo` mode, defeating fully automated pipelines.  
- **Todo completion stuck** – The last todo item never finishes, requiring manual intervention.  
- **Windows ecosystem friction** – Console font resets, log file collisions, and UTF-8 filename handling continue to plague Windows users. PRs addressing these are now merged, so relief is coming.  
- **Session persistence issues** – Mid-turn crashes leave orphaned tool calls that break subsequent replays; session continuation logic is fragile when the metadata is stale.  
- **MCP startup brittleness** – Failed MCP servers could abort entire turns; now fixed in #2355.  
- **Shell subprocess management** – Timeouts were not killing child processes, hanging the CLI; fixed in #2327.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-11

## Today's Highlights

Three patch releases landed today, with **v1.17.3** primarily fixing a desktop crash introduced in v1.17.2. The community is closely watching several open issues: a highly-upvoted request for clipboard paste of images, a lingering bug with free-tier models incorrectly claiming exhausted credits, and a new concern about high CPU usage in recent versions. On the PR front, a large TUI 2.0 overhaul and multiple contributor-driven bug fixes are moving through review.

## Releases

Four versions were published in the last 24 hours:

- **[v1.17.3](https://github.com/anomalyco/opencode/releases/tag/v1.17.3)** — Urgent fix for the desktop crash introduced in 1.17.2.
- **[v1.17.2](https://github.com/anomalyco/opencode/releases/tag/v1.17.2)** — Core: recovered from expired remote config auth without failing, restored subagent permission isolation. Desktop: fixed Linux launcher/icon identity so pinned apps work.
- **[v1.17.1](https://github.com/anomalyco/opencode/releases/tag/v1.17.1)** — Core: references now include usage descriptions, deprecated `reference` config entries are migrated to `references` key automatically.
- **[v1.17.0](https://github.com/anomalyco/opencode/releases/tag/v1.17.0)** — Core: faster file search via `fff`-backed tool, `X-Session-Id` headers for proxy setups, Cohere North model support, `reasoning` as interleaved field.

## Hot Issues (10 noteworthy)

1. **[#906 — Feature request: Paste to attach image](https://github.com/anomalyco/opencode/issues/906)**  
   _36 comments · 22 👍_  
   Users want clipboard paste support (Ctrl+V) for images instead of only drag-and-drop. This is the most commented open feature request and reflects a clear UX gap for workflows with tools like Excalidraw.

2. **[#14273 — [bug] Free usage exceeded when using Zen free models](https://github.com/anomalyco/opencode/issues/14273)**  
   _27 comments · 1 👍 (CLOSED)_  
   Users with an active Zen balance see a false “Free usage exceeded” error when using free-tier models (Kimi K2.5, MiniMax2.5). Despite being closed, the high engagement signals it remains a pain point.

3. **[#6330 — [FEATURE] Generic UI Intent Channel](https://github.com/anomalyco/opencode/issues/6330)**  
   _17 comments · 8 👍_  
   Proposes a protocol-level “UI intent” event type enabling plugins to trigger UI actions across clients. The community sees this as foundational for rich plugin-driven UX.

4. **[#450 — Support for reasoning_effort parameter in UI](https://github.com/anomalyco/opencode/issues/450)**  
   _12 comments · 26 👍_  
   Despite being closed, this is the most thumbed-up issue in the list. Users want a UI toggle for reasoning effort (OpenAI, Gemini, DeepSeek). It may have been partially addressed but remains a hot topic.

5. **[#25038 — Long-running shell commands hang after completion](https://github.com/anomalyco/opencode/issues/25038)**  
   _11 comments · 6 👍_  
   Gradle builds (and similar) can appear stuck even after “BUILD SUCCESSFUL”. The community is looking for a fix to detect command completion properly.

6. **[#26762 — Cerebras zai-glm-4.7 fails on follow-up turn with reasoning_content](https://github.com/anomalyco/opencode/issues/26762)**  
   _10 comments · 2 👍_  
   A provider-specific regression: multi-turn conversations with reasoning + tool calls break because `reasoning_content` is unsupported in that context. Active debugging by the reporter.

7. **[#6490 — Web UI cannot browse folders outside default user profile](https://github.com/anomalyco/opencode/issues/6490)**  
   _10 comments · 12 👍_  
   Windows users on `opencode web` are locked to system folders (Downloads, Contacts). A significant number of thumb-ups suggest this affects many developers working on D: drives or network paths.

8. **[#30086 — High CPU usage in newer versions](https://github.com/anomalyco/opencode/issues/30086)**  
   _9 comments · 1 👍_  
   Reports of dramatic CPU spikes in the last week, making multiple sessions impossible. This is a recent regression and likely a top priority for maintainers.

9. **[#28370 — Error: Unexpected server error](https://github.com/anomalyco/opencode/issues/28370)**  
   _9 comments · 4 👍_  
   A generic server crash with no clear cause, affecting users across versions. The error stack trace points to the renderer, suggesting a UI/front-end issue.

10. **[#31247 — Opus 4.8 via GitHub Copilot leaks tool-call text](https://github.com/anomalyco/opencode/issues/31247)**  
    _8 comments_  
    A model-specific bug: `claude-opus-4.8` sometimes outputs raw tool invocation markup as assistant text, polluting conversation history. Serious for reliability.

## Key PR Progress (10 important)

1. **[#31796 — TUI 2.0](https://github.com/anomalyco/opencode/pull/31796)**  
   A major rewrite of the terminal UI. This is the largest PR in the batch and will likely reshape the TUI experience. Currently open with no comment count.

2. **[#31823 — Simplify processor layer wiring (test infrastructure)](https://github.com/anomalyco/opencode/pull/31823)**  
   Refactors the session processor test environment to use a single `LayerNode` root, improving test maintainability. By @jlongster.

3. **[#31822 — v2 session API endpoints](https://github.com/anomalyco/opencode/pull/31822)**  
   Adds v2 location resolution, session create/get, and session-scoped pending question listing. Also regenerates the JavaScript SDK. Foundational for future client improvements.

4. **[#31805 — Fix TUI exit epilogue during scoped shutdown](https://github.com/anomalyco/opencode/pull/31805)**  
   Fixes a bug where cleanup cleared the session epilogue before it could be printed. Small but important UX fix for the TUI.

5. **[#31819 / #31814 — Retry on xfyun engine busy](https://github.com/anomalyco/opencode/pull/31819)**  
   Two related PRs (one closed, one open) that add retry logic for “engine busy” errors from the xfyun provider. Community-driven robustness fix.

6. **[#13610 — Desktop keyboard shortcuts to switch projects (Cmd+1–9)](https://github.com/anomalyco/opencode/pull/13610)**  
   Long-standing feature PR adding project switching shortcuts, similar to browser tabs. Still open after several months but recently updated.

7. **[#31817 — Fix compaction key detection in isV1](https://github.com/anomalyco/opencode/pull/31817)**  
   Fixes a config migration bug where `compaction` fields with `preserve_recent_tokens` were silently dropped. Prevents data loss.

8. **[#31329 — Graceful error handling for PDF/image file read failures](https://github.com/anomalyco/opencode/pull/31329)**  
   Prevents session crashes when unreadable PDFs or images are encountered. Important for stability with large attachments.

9. **[#31809 — Fix misleading Read prerequisite in tool descriptions](https://github.com/anomalyco/opencode/pull/31809)**  
   Corrects tool docs that falsely claimed Write/Edit tools require a prior Read call. Minor but reduces agent confusion.

10. **[#31798 — Reuse source git objects to avoid re-hashing huge repos](https://github.com/anomalyco/opencode/pull/31798)**  
    Critical performance fix for opening sessions in large repos (e.g., Chromium). Avoids a hang caused by `git add --all` by reusing existing git objects.

## Feature Request Trends

Based on the most active issues, the community is pushing for:

- **Clipboard paste for images** (#906, #31791) — The single most-requested UX improvement.
- **Reasoning control** (#450, #24610, #27555) — Users want UI toggles for reasoning effort and to disable thinking mode (especially for translation workloads).
- **Folder selection in Web UI** (#6490) — Windows users need to browse arbitrary paths.
- **Plugin/Server extensibility** (#6330, #31821, #31820) — Generic UI intents, programmatic `ensureServer()`, and auto-approve permissions from localhost.
- **Session-level model selection via ACP** (#31750) — Enables per-session model choice for external agents.

## Developer Pain Points

Recurring frustrations visible in issue comments and upvotes:

1. **Performance regressions** — High CPU (#30086) and general slowness (#16438) in recent versions, with 16GB snapshot files reported.
2. **Timeout and hanging** — Headers timeout with local providers (#26602), long shell commands not properly detecting completion (#25038).
3. **Stale permission dialogs** — TUI gets stuck on permission prompts that already resolved (#28312).
4. **Crashes on startup** — Due to malformed agent files (#31481) or generic server errors (#28370).
5. **Caching issues** — Direct MiniMax API caching broken (#31755), snapshot growth unmanaged.
6. **Account management** — Inability to delete Zen account (#18016) and misleading “free usage exceeded” errors (#14273).
7. **MCP/oauth cross-platform issues** — IPv6/IPv4 mismatch on Windows (#31824), OAuth callback failures.

The overall sentiment is that while OpenCode’s feature velocity is high, recent releases have introduced stability and performance issues that the community is eager to see addressed.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-11

## Today's Highlights

A wave of provider‑compatibility fixes and TUI stability patches dominated the past 24 hours. The team landed a new **Palantir Foundry** provider and a fix for Anthropic stream finalization, while several crash‑reporting issues highlighted lingering TUI fragility. Community feedback on the recently shipped **trust gating** feature (#5514) is mixed, with users requesting opt‑out workflows.

## Releases

No new releases in the last 24 hours.

## Hot Issues

*10 noteworthy issues updated in the last 24h*

1. **#5514 – Project Trust Feature Feedback**  
   *Author: markg85 | Comments: 25 | 👍 13*  
   The new trust‑gating feature receives strong pushback; users want a way to permanently trust projects and skip the prompt. The maintainer is evaluating opt‑out configuration.  
   [earendil-works/pi#5514](https://github.com/earendil-works/pi/issues/5514)

2. **#3715 – `local-llm` streams terminate at 5 min due to undici `bodyTimeout`**  
   *Author: LooSik | Comments: 10 | 👍 4*  
   Long tool calls against local OpenAI‑compatible backends (vLLM, llama.cpp) are killed after exactly 5 minutes. The `retry.provider.timeoutMs` setting doesn’t override undici’s default – a known bug that frustrates users of local LLMs.  
   [earendil-works/pi#3715](https://github.com/earendil-works/pi/issues/3715)

3. **#4160 – pi extensions do not play nice with Bun**  
   *Author: 8549 | Comments: 9*  
   Using Bun as runtime without Node.js causes extension installation to fail because `pi` seeks `npm` in `$PATH`. The community would like Bun‑native support.  
   [earendil-works/pi#4160](https://github.com/earendil-works/pi/issues/4160)

4. **#3372 – `pi` can no longer work with Claude subscription**  
   *Author: totoroot | Comments: 7*  
   A regression breaks Claude subscription login; the user reports that switching to OpenAI/Codex works well, but Anthropic integration is problematic. High interest among Enterprise subscribers.  
   [earendil-works/pi#3372](https://github.com/earendil-works/pi/issues/3372)

5. **#5291 – Sessions hang on "Working" with Anthropic subscription**  
   *Author: eyalroth | Comments: 5 | 👍 1*  
   Intermittent session hangs when using an Anthropic Enterprise subscription. Interrupt/resume helps only sometimes. A critical reliability bug for heavy users.  
   [earendil-works/pi#5291](https://github.com/earendil-works/pi/issues/5291)

6. **#5611 – GitLab Duo Anthropic streams hit ~90s cutoff before `message_stop`**  
   *Author: jetnet | Comments: 3*  
   Anthropic streams via GitLab Duo can end prematurely, triggering retries that amplify costs. The issue reveals deeper stream‑finalization logic gaps.  
   [earendil-works/pi#5611](https://github.com/earendil-works/pi/issues/5611)

7. **#5605 – MiniMax-M3: `cache_control` ignored on Anthropic endpoint**  
   *Author: nimitbhardwaj | Comments: 2*  
   MiniMax-M3 is routed to the Anthropic‑compatible API which ignores `cache_control`, leading to full‑price billing and no caching benefit. Provider‑specific nuance that needs better routing.  
   [earendil-works/pi#5605](https://github.com/earendil-works/pi/issues/5605)

8. **#5536 – Split‑turn compaction sends parallel summarization requests causing 429 on single‑concurrency backends**  
   *Author: mforce | Comments: 2*  
   Auto‑compaction launches two concurrent summary requests that overwhelm single‑slot local backends (e.g., `llama.cpp`). The workaround is to disable split‑turn compaction.  
   [earendil-works/pi#5536](https://github.com/earendil-works/pi/issues/5536)

9. **#5604 – WorkflowEditor crash: `TypeError: value.startsWith is not a function`**  
   *Author: YrFnS | Comments: 1*  
   A hard crash in the TUI when autocomplete suggestions contain non‑string `value` fields. Completely terminates the pi process – high severity for users who rely on workflow editor.  
   [earendil-works/pi#5604](https://github.com/earendil-works/pi/issues/5604)

10. **#5603 – Cost reporting: 1‑hour prompt‑cache writes priced at 5‑minute rate**  
    *Author: ishinder | Comments: 1*  
    Anthropic’s 1‑hour cache retention (2× base input cost) is not reflected in Pi’s cost reporting. All cache writes are billed at the 5‑minute rate (1.25×), underreporting actual spend.  
    [earendil-works/pi#5603](https://github.com/earendil-works/pi/issues/5603)

## Key PR Progress

*10 important pull requests updated in the last 24h*

1. **#5609 – New provider: Palantir Foundry LLM proxy** *(closed)*  
   Adds support for Palantir Foundry AIP proxy, including OAuth token flow and support for Anthropic, Google, xAI, and OpenAI models through the proxy.  
   [earendil-works/pi#5609](https://github.com/earendil-works/pi/pull/5609)

2. **#5600 – Honor Codex SSE header timeout setting** *(open)*  
   Fixes hardcoded 10‑second SSE header timeout for Codex; now respects user‑configured `timeoutMs`/`httpIdleTimeoutMs`.  
   [earendil-works/pi#5600](https://github.com/earendil-works/pi/pull/5600)

3. **#5594 – Fix Anthropic stream finalization on `message_stop`** *(closed)*  
   Treats `message_stop` as the logical end of an assistant message, cancelling the body reader instead of waiting for transport EOF. Resolves issue #5592.  
   [earendil-works/pi#5594](https://github.com/earendil-works/pi/pull/5594)

4. **#5509 – New provider: Amazon Bedrock Mantle (OpenAI Responses API)** *(open)*  
   Adds support for AWS Bedrock Mantle’s OpenAI‑compatible endpoint, currently supporting GPT 5.5 and 5.4. Modeled after the existing Azure OpenAI provider.  
   [earendil-works/pi#5509](https://github.com/earendil-works/pi/pull/5509)

5. **#5583 – Preserve clickable subscription login URLs** *(closed)*  
   Fixes a formatting issue where default left‑padding caused long login URLs to be broken across lines, making them non‑clickable.  
   [earendil-works/pi#5583](https://github.com/earendil-works/pi/pull/5583)

6. **#5561 – Link AWS data retention docs in Bedrock validation errors** *(closed)*  
   Improves error messaging when Claude Fable 5 requires data retention to be enabled on Bedrock, directing users to the relevant documentation.  
   [earendil-works/pi#5561](https://github.com/earendil-works/pi/pull/5561)

7. **#5585 – Wrap CJK text at character boundaries in editor** *(closed)*  
   Fixes TUI editor wrapping for CJK characters, which previously split characters mid‑grapheme.  
   [earendil-works/pi#5585](https://github.com/earendil-works/pi/pull/5585)

8. **#5562 – Separate list items with blank lines in loose lists** *(closed)*  
   Ensures CommonMark‑compliant rendering of `loose` lists by inserting blank lines between items when applicable.  
   [earendil-works/pi#5562](https://github.com/earendil-works/pi/pull/5562)

9. **#5560 – Parse `:thinking` suffix from custom model IDs in fallback path** *(closed)*  
   Allows custom model IDs appended with `:thinking` to correctly enable extended thinking. Falls back gracefully when the suffix is not a valid level.  
   [earendil-works/pi#5560](https://github.com/earendil-works/pi/pull/5560)

10. **#5586 – Use resolved `apiKey` as bearer‑token fallback for Bedrock** *(closed)*  
    Enables authentication via `models.json` `apiKey` when using a gateway in front of Bedrock, which was previously ignored.  
    [earendil-works/pi#5586](https://github.com/earendil-works/pi/pull/5586)

## Feature Request Trends

The community’s strongest feature signals this week are:

- **Provider expansion** – New provider contributions (Palantir Foundry, AWS Bedrock Mantle) and requests for better support of non‑standard backends (MiniMax‑M3 caching, GitLab Duo streaming).  
- **Extensibility & hooks** – Requests for custom events on command execution (#5608), a `clear_queue` RPC command (#5606), and ability to override generated system prompts (#5577) indicate a desire to treat Pi as a programmable agent harness.  
- **TUI & UX polish** – Multi‑select list components (#5025), custom OAuth callback pages (#5372), and zero‑padding configuration (#3454) show that power users want more UI control.  
- **Trust & first‑run experience** – The new trust gating (#5514) is polarising; an experimental first‑time setup flow (#5587) suggests the team is exploring onboarding improvements.

## Developer Pain Points

Recurring themes from today’s issues:

- **Stream timeout unpredictability** – Multiple reports of streams dying before logical completion (5‑min undici timeout, 90‑s GitLab Duo cutoff, Anthropic streams not waiting for `message_stop`). These force expensive retries and break long‑running tasks.  
- **Provider‑specific incompatibilities** – Claude/Anthropic subscription login issues, MiniMax‑M3 caching, Kimi K2.6 JSON schema conflicts – each addition introduces a new edge case.  
- **TUI crashes as hard failures** – Several `TypeError` crashes in Box.render, WorkflowEditor, and `getTextOutput` that terminate the entire pi process. Users expect graceful fallbacks.  
- **Configuration gaps** – Undici timeout cannot be overridden, cost reporting uses wrong cache pricing, `maxTokens` not passed through for some OpenAI‑completions providers, and themes uninstalled break `/share` exports.  
- **Runtime environment friction** – Bun compatibility (#4160) and Android Termux multiline paste auto‑submission (#5598) highlight that Pi’s assumption of a standard Node.js environment causes pain in alternative setups.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-11

## Today’s Highlights
The community is actively shaping terminal UX and sub-agent workflows. Critical input handling bugs (SGR mouse leaks, cooked-mode drops, VP scroll conflicts) are being addressed alongside a major daemon-mode feature batch merging into `main`. Several PRs harden team collaboration and memory/performance boundaries.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 Noteworthy)

1. **#4942** – [OPEN] VP mode scroll input conflicts with Composer input  
   *Priority P2. Users cannot scroll chat history when Composer is active. Affects core interaction.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4942)

2. **#4597** – [CLOSED] Enhanced `/stats` with cross-session global usage tracking (reference Claude Code)  
   *Request for persistent usage stats. Closed with implementation likely merged.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4597)

3. **#4876** – [CLOSED] Subagent reading images returns unrelated content  
   *Bug: subagents fail to correctly interpret image files, undermining their utility for vision tasks.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4876)

4. **#4877** – [OPEN] OpenWork cannot distinguish same model from different providers  
   *UI/configuration bug blocking multi-provider model selection. Active discussion.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4877)

5. **#4882** – [OPEN] Add `terminalSequence` field on hooks (inspired by Claude Code)  
   *Allows hooks to emit terminal-side effects (notifications, title updates).*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4882)

6. **#4891** – [OPEN] Terminal resize during streaming leaves fragmented content in scrollback  
   *Rendering glitch corrupts scrollback on resize. Three comments, still open.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4891)

7. **#4974** – [OPEN] SGR mouse wheel sequences leak as typed text into input box  
   *Double-consumption of mouse events causes visible escape codes. Affects all SGR mouse users.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4974)

8. **#4966** – [OPEN] SchemaValidator missing numeric string coercion causes MCP tool failures  
   *LLMs emit numbers as strings; strict MCP servers reject them. Frustrating for Playwright users.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4966)

9. **#4928** – [OPEN] Allow background subagents to queue permission prompts to parent session  
   *Currently auto-denies; feature request to surface approval requests interactively.*  
   [Link](https://github.com/QwenLM/qwen-code/issues/4928)

10. **#4930** – [CLOSED] `env` in read-only command allowlist enables arbitrary command execution  
    *Security vulnerability: `env` can execute commands. Fixed.*  
    [Link](https://github.com/QwenLM/qwen-code/issues/4930)

---

## Key PR Progress (10 Important Pull Requests)

1. **#4490** – [OPEN] Merge daemon-mode feature batch (46 commits, 115k LOC)  
   *Massive integration of daemon mode into `main`. Brings session isolation, REST APIs, and more.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4490)

2. **#4827** – [CLOSED] ACP/REST parity – 29 new `_qwen/*` methods + production hardening  
   *Achieves full feature parity between ACP and REST transports. Foundation for websocket PR.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4827)

3. **#4773** – [OPEN] ACP WebSocket transport (RFD Streamable HTTP phase 2)  
   *Adds WebSocket transport coexisting with SSE. Depends on #4827.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4773)

4. **#4952** – [CLOSED] Fix SSE reconnection stability, error routing, and toast API  
   *Improves resilience of web-shell/webui SSE connections. Session preservation on retry.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4952)

5. **#4979** – [OPEN] Preserve teammate identity when resuming a tool call after approval  
   *Fixes attribution bug in team workflows where messages were mislabeled.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4979)

6. **#4981** – [OPEN] Serialize team task claims per agent with mailbox lock parity  
   *Prevents concurrent assignment of two tasks to the same agent.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4981)

7. **#4598** – [OPEN] Collapsible thinking blocks with duration timer (TUI)  
   *Streams reasoning in a fixed-height window that collapses on completion.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4598)

8. **#4971** – [OPEN] Reduce retained interactive tool output memory  
   *Compacts large tool-output display metadata to lower memory pressure.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4971)

9. **#4902** – [OPEN] Cursor-based pagination for session list (REST + ACP)  
   *Adds `?cursor` and `?size` params for efficient session listing.*  
   [Link](https://github.com/QwenLM/qwen-code/pull/4902)

10. **#4965** – [OPEN] `POST /workspace/reload` for unified settings hot-reload  
    *Single endpoint to reload all settings to idle sessions. Replaces narrower `reload-env`.*  
    [Link](https://github.com/QwenLM/qwen-code/pull/4965)

---

## Feature Request Trends

- **Enhanced usage statistics**: Persistent cross-session stats and dashboards (#4597, #4954).
- **Richer hooks**: `terminalSequence` field for terminal-side effects (#4882).
- **Sub-agent autonomy**: Permission bubbling, default fork subagent, background task approval queues (#4928, #4956).
- **Terminal UX improvements**: Timestamps/time awareness in responses (#4899), collapsible thinking blocks (#4598), git branch display in desktop UI (#4769).
- **Configuration granularity**: Disable auto-memory recall (#4374), `deniedMcpServers` policy (#4940), file I/O shortcuts (grep satisfies read-before-edit, #4939).
- **Scaling awareness**: QWEN.md length warning proportional to model context window (#4941).

## Developer Pain Points

- **Input handling fragility**: SGR mouse leaks (#4974), cooked-mode drops (#4973), scroll conflicts with Composer (#4942), terminal resize fragmentation (#4891).
- **Memory and token management**: Auto-memory recall interferes with CLI calls (#4976), hard/auto threshold identical (#4945), statusline token count accuracy questioned (#4951), MaxListenersExceededWarning (#4423).
- **Sub-agent reliability**: Image reading failures (#4876), truncation recovery (#4964), tool-result microcompaction skipped in hook continuations (#4838).
- **Model switching confusion**: Same model from different providers indistinguishable (#4877), inability to switch to new model versions (#4904).
- **MCP integration friction**: Schema validation rejects numeric strings (#4966).
- **Windows installation**: `qwen` not found in new sessions when installed as SYSTEM (#4901).
- **CI/security**: Weak branch protection allowed broken PRs to merge (#4864); `env` command exploit (#4930).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest — 2026-06-11

## Today's Highlights
The project officially rebranded to **CodeWhale** with the release of v0.8.57 — the legacy `deepseek-tui` npm package is deprecated. A major v0.8.58 branch (PR #3034) has opened, carrying a constitution refactor, Codex reliability fixes, and sidebar improvements. Community attention remains focused on provider fallback chains, rebrand migration pain, and UI clutter reduction.

## Releases
- **v0.8.57** — Rebranded to CodeWhale. All canonical assets, commands, and npm packages now use the name `codewhale`. Users on legacy `deepseek` / `deepseek-tui` should follow `docs/REBRAND.md`.
- **v0.8.56** — "Community Harvest": localization for 7 locales, provider improvements, prefix-cache stability, and assorted fixes.

## Hot Issues (10 noteworthy)
- [#2369 Config Paths Fragmented Across OS and Cygwin (Plus Silent Migration Bug)](https://github.com/Hmbown/CodeWhale/issues/2369) — High‑impact migration blocker; config files end up in different locations depending on OS and terminal, making rebrand updates unreliable.
- [#1679 SSE multi‑agent parallel timeout on Windows 11 + UI corruption](https://github.com/Hmbown/CodeWhale/issues/1679) — Persistent 45‑second timeout when running multiple sub‑agents, forcing fallback to solo mode; also triggers display glitches.
- [#1806 Sub‑agent 120s API timeout renders agent_open nearly unusable (v0.8.39)](https://github.com/Hmbown/CodeWhale/issues/1806) — All 5 sub‑agents fail with identical timeout errors when processing a large document; the feature’s advertised parallel offload is broken in practice.
- [#2574 Feature Request: Provider fallback chain — auto‑switch on API failure](https://github.com/Hmbown/CodeWhale/issues/2574) — Most‑upvoted enhancement; users want automatic fallback to backup providers when quotas/exhausted or 4xx/5xx errors occur, avoiding manual `/provider` commands.
- [#1990 Remote workbench: evaluate US‑first Cloudflare/AWS/Telegram lane](https://github.com/Hmbown/CodeWhale/issues/1990) — Strategic request for a non‑China infrastructure path (DigitalOcean + Telegram) for global users who cannot use Tencent/Lighthouse.
- [#2969 CHANGELOG missing v0.8.55 entry](https://github.com/Hmbown/CodeWhale/issues/2969) — Community found the release notes for v0.8.55 were omitted, breaking changelog continuity.
- [#2964 Ship DigitalOcean + Telegram remote‑workbench setup (v0.8.56)](https://github.com/Hmbown/CodeWhale/issues/2964) — Targeted implementation of #1990, already working with a ~15‑minute setup script.
- [#3007 TUI provider rejection blames `--provider` flag the user never passed](https://github.com/Hmbown/CodeWhale/issues/3007) — Confusing error message when a provider from config/env is not TUI‑capable; suggests removing a flag the user never typed.
- [#2893 siliconflow provider config error](https://github.com/Hmbown/CodeWhale/issues/2893) — `siliconflow-CN` alone fails unless the same values are duplicated in `[providers.siliconflow]`; unnecessary redundancy.
- [#2989 Ollama + qwen3-coder agent stops prematurely but reports "completed"](https://github.com/Hmbown/CodeWhale/issues/2989) — Agent halts mid‑task but marks status as done, misleading users about actual progress.

## Key PR Progress (10 important)
- [#3034 v0.8.58: Constitution refactor, Codex fixes, sidebar improvements](https://github.com/Hmbown/CodeWhale/pull/3034) — Stack of three commits: YAML‑based constitution generation, provider error improvements, split Model/Provider sidebar panels.
- [#3038 fix(tui): make Ctrl+B directly background active shell](https://github.com/Hmbown/CodeWhale/pull/3038) — Removes two‑step menu; one‑key backgrounding improves workflow speed.
- [#3046 fix(reasoning): add Moonshot/Kimi to reasoning‑content support](https://github.com/Hmbown/CodeWhale/pull/3046) — Kimi thinking traces now render as dedicated Thinking blocks instead of leaking into plain answer.
- [#3044 feat(remote‑smoke): bump to v0.8.57, add gh CLI, swapfile, autonomous loop docs](https://github.com/Hmbown/CodeWhale/pull/3044) — Infrastructure for unattended DigitalOcean agent loop used by v0.8.58 milestone.
- [#3043 feat(docs): agent‑task issue template, labels, and runner protocol](https://github.com/Hmbown/CodeWhale/pull/3043) — Standardises how remote agents autonomously execute milestone issues.
- [#3041 fix: harvest error‑message fixes from community PR #2933](https://github.com/Hmbown/CodeWhale/pull/3041) — Better tool denial and subagent conflict messages, addressing three related issues.
- [#3039 feat(tui): OSC 8 out‑of‑band hyperlink infrastructure](https://github.com/Hmbown/CodeWhale/pull/3039) — Enables clickable links in transcript without breaking ratatui’s buffer.
- [#3037 fix(tui): compact tool‑call transcript rendering — suppress boilerplate](https://github.com/Hmbown/CodeWhale/pull/3037) — Hides "(no output)" lines and sub‑second timings; expands on hover.
- [#3042 feat(exec): add `--allowed-tools`, `--disallowed-tools`, `--max-turns`, `--append-system-prompt`](https://github.com/Hmbown/CodeWhale/pull/3042) — Brings `codewhale exec` to parity with `claude -p` / `codex exec` for CI/benchmark use.
- [#3048 feat(prompts): parameterize model‑specific facts — context window, pricing, thinking](https://github.com/Hmbown/CodeWhale/pull/3048) — Substitutes hardcoded DeepSeek‑V4 claims with runtime lookups, critical for multi‑model support.

## Feature Request Trends
1. **Model‑agnostic support** — Issues repeatedly ask for dropping hardcoded DeepSeek assumptions in auto‑router, subagent model selection, constitution prompts, and provider capabilities (#3018, #3025, #3014).
2. **Provider fallback & reliability** — Automatic fallback chains on API failure (#2574) and better retry logic for OpenAI Codex (#3019) are top demands.
3. **UI/UX refinements** — Compact tool‑call view, clickable sidebar rows, hide internal IDs, persistent session panel, inspector for low‑information rows (#3031, #3040, #3036, #2934, #2018).
4. **Remote workbench & autonomous agents** — Many contributions aim at turning CodeWhale into a headless agent runner on cheap US VPSes, controlled via Telegram (#1990, #2964, #3027).
5. **Rebrand migration polish** — Remaining legacy path references, missing changelogs, and silent migration bugs need to be resolved (#2644, #2969, #2960).
6. **Security & secrets management** — Dynamic API key resolution from scripts (e.g. KeepassXC) and avoiding plaintext in dotfiles (#3004).
7. **Localization** — Sandbox dialog and other hardcoded English strings being internationalised (#2892).

## Developer Pain Points
- **Config fragmentation** across OS family and Cygwin (#2369) — causes silent failure during migration.
- **Sub‑agent timeouts** (SSE on Windows, 120s API) make parallel agent workflows unusable (#1679, #1806).
- **Rebrand confusion** — TUI still surfaces `deepseek` paths and error messages blame nonexistent `--provider` flags (#2664, #3007).
- **Provider quirks** — Siliconflow region config duplicates required (#2893); Moonshot/Kimi thinking not wired (#3046 PR fix in progress).
- **TTY not controlling** — `task_shell_start tty:true` breaks `/dev/tty`‑dependent tools like `sshpass` (#2372).
- **Ollama compatibility** — Agent stops prematurely but reports "completed", deceiving users (#2989).
- **Release channel inconsistency** — npm, crates.io, and GitHub releases show different versions, confusing update flows (#2988).
- **Stream errors on sleep** — Active turn dies with broken body on laptop wake, losing work (#2990).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*