# AI CLI Tools Community Digest 2026-06-05

> Generated: 2026-06-05 02:43 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-06-05

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with nine major tools now competing for developer mindshare. Across the board, communities are demanding **interoperability** (universal agent configs like `AGENTS.md`), **platform parity** (Windows, Linux, Wayland), and **stability** over new features. The most urgent shared pain points revolve around authentication reliability, copy/paste regressions, and resource management (memory leaks, context window gating). While each tool carves a distinct niche—from enterprise compliance (Claude Code) to desktop-first UX (Codex) to open extensibility (Pi, OpenCode)—the convergence toward **MCP-based tool integration**, **remote execution**, and **cross-session persistence** signals a rapidly standardizing architecture.

## 2. Activity Comparison (2026-06-05)

| Tool | Issues Updated (notable) | PRs Updated (notable) | Release(s) Today |
|------|--------------------------|------------------------|------------------|
| **Claude Code** | 10 (1 new megathread) | 6 (1 critical fix) | v2.1.163 |
| **OpenAI Codex** | 10 (macOS leak, Windows sandbox) | 10 (retry, OAuth, sandbox) | 4 alpha releases |
| **Gemini CLI** | 10 (symlinks, PTY leaks) | 10 (SSRF fix, CJK, WSL) | v0.45.1 patch, nightly |
| **GitHub Copilot CLI** | 10 (copy/paste, auth) | 2 (spam only) | v1.0.60-0 |
| **Kimi Code CLI** | 7 (403 errors, slowdown) | 6 (auto-scroll fix) | None |
| **OpenCode** | 10 (memory, pricing, bugs) | 10 (compaction, themes, subagents) | None |
| **Pi** | 10 (codex hang, stats crash) | 10 (Vertex provider, keybindings) | v0.78.1 |
| **Qwen Code** | 10 (model-switching, memory) | 10 (ACP parity, /stats, /fork) | v0.17.1-nightly |
| **DeepSeek TUI** | 10 (provider lockout, freezes) | 10 (stabilization, multi-tab) | None |

*Note: “Issues Updated” counts the top hot issues listed; “PRs Updated” counts key PRs. Actual repository activity may be higher.*

## 3. Shared Feature Directions

The following requirements appear **across multiple tools**, indicating strong community consensus:

- **Universal Agent Configuration (`AGENTS.md`)**  
  *Tools:* **Claude Code** (#6235, 4,060 👍), **DeepSeek TUI** (PR #2745 LLM-generated AGENTS.md)  
  *Need:* A cross-tool standard for codebase understanding, replacing tool-specific files (CLAUDE.md).

- **Persistent User Configuration / Permissions**  
  *Tools:* **Copilot CLI** (#2398, 10 👍), **Pi** (PR #5332 approval system), **Qwen Code** (#4754, #4764 user-level auto-memory)  
  *Need:* Save permissions, model selections, and memory across sessions without repeated prompts.

- **Cross-Session Usage Tracking & Dashboards**  
  *Tools:* **Qwen Code** (#4779 interactive `/stats`), **DeepSeek TUI** (#2666 token/resource visibility), **OpenCode** (#7763 persistent cost)  
  *Need:* Real-time and historical analytics on token consumption, usage limits, and model performance.

- **Remote Execution / SSH / WSL Support**  
  *Tools:* **Claude Code** (#65527 remote context clarity), **Gemini CLI** (PR #27354 WSL bypass), **Pi** (#5341 remote containers), **Kimi Code** (WSL2 issues)  
  *Need:* Clear indicators of execution context and robust support for remote and containerized environments.

- **Copy/Paste Reliability**  
  *Tools:* **Copilot CLI** (#2082, #3260, #3666), **DeepSeek TUI** (#1920 Wayland), **Kimi Code** (#2422 auto-scroll)  
  *Need:* Cross-platform clipboard consistency, especially in terminals and SSH sessions.

- **Authentication Token Lifecycle Management**  
  *Tools:* **Copilot CLI** (#3596, #3682), **Kimi Code** (#2425, #2427 403 errors), **OpenCode** (#12789 model not supported)  
  *Need:* Silent token refresh without restart, secure storage, and graceful fallback on failure.

- **MCP Tool Integration & Plugin Ecosystems**  
  *Tools:* **Gemini CLI** (MCP discovery), **DeepSeek TUI** (#2744 underscore bug), **Pi** (extension commands), **Qwen Code** (#4777 prompt cache busting)  
  *Need:* Reliable MCP tool listing, workspace-specific config merging, and minimal prompt overhead.

- **Vim Mode / TUI Interaction**  
  *Tools:* **Copilot CLI** (vim navigation in diff), **Qwen Code** (#4677 comprehensive vim fix), **Pi** (#5188 shift+enter)  
  *Need:* Consistent, bug-free keyboard navigation and terminal input behaviors.

## 4. Differentiation Analysis

| Tool | Primary Focus | Target Users | Technical Approach |
|------|--------------|--------------|-------------------|
| **Claude Code** | Enterprise compliance, plugin system | Large teams, compliance-heavy orgs | Version gating, managed settings, `.claude/skills/` |
| **OpenAI Codex** | Desktop application, sandbox isolation | macOS/Windows developers, security-conscious | Rust-based runtime, Seatbelt sandbox, OAuth |
| **Gemini CLI** | Security hardening, PTY stability | Enterprise Linux users, CI/CD pipelines | SSRF prevention, strict PTY management, WSL interop |
| **GitHub Copilot CLI** | GitHub-centric workflow, copilot ecosystem | GitHub-heavy developers, PR reviews | Tight GH integration, session resume, diff review |
| **Kimi Code CLI** | Chinese market, lightweight CLI | Developers in China, arm64 Linux | Minimal releases, fast iteration on 403 errors |
| **OpenCode** | Open-source flexibility, subagents | Power users, self-hosters | Memory compaction, agent variants, vLLM support |
| **Pi** | Extensibility, multi-provider support | Developers using multiple backends | Extension API, provider aliases, theme system |
| **Qwen Code** | Daemon/ACP compliance, context persistence | Zed/JetBrains users, multi-project teams | ACP REST parity, user-level auto-memory, `/fork` background agents |
| **DeepSeek TUI** | Multi-tab & pipeline workflows | Developers needing task orchestration | Tab manager, cross-tab delegation, credential rollback |

**Key Differentiator:** Claude Code and Gemini CLI lead in **enterprise hardening**; Codex leads in **desktop sandboxing**; OpenCode and Pi lead in **open extensibility**; Qwen Code leads in **daemon-based integration**.

## 5. Community Momentum & Maturity

- **Highest Engagement:** **Claude Code** dominates with a single issue (#6235, 4,060 👍) and a bustling PR pipeline (though many fix scripts). **OpenCode**’s memory megathread (#20695, 63 👍) shows strong collaborative debugging.
- **Most Rapid Iteration:** **Qwen Code** saw 10 substantial PRs (ACP parity, `/stats`, `/fork`) alongside a nightly release—evidence of fast-moving development. **Pi** released v0.78.1 with 10 PRs covering providers, keybindings, and fixes.
- **Stability Concerns:** **OpenAI Codex** faces the most severe regressions (macOS `syspolicyd` freeze, Windows sandbox failures) with high-severity, platform-wide impacts. **Copilot CLI** struggles with copy/paste reliability (3+ outstanding issues) and spam PRs, indicating maintainer bandwidth constraints.
- **Emerging but Small:** **Kimi Code CLI** and **DeepSeek TUI** have smaller communities but active issue/PR throughput. Both are targeting niche pain points (403 errors, provider lockout) that could hinder adoption if unresolved.
- **Maturity Leaders:** **Claude Code** and **Gemini CLI** show mature release processes (version gating, patch releases) and proactive security fixes (SSRF, permission profiles). **Copilot CLI** has a stable release cadence but remains reactive to regressions.

## 6. Trend Signals

Several industry trends emerge from community feedback that are valuable for developers evaluating tool adoption:

1. **Universal Agent Configs (AGENTS.md) is inevitable.** The overwhelming response to Claude Code’s issue (#6235) and DeepSeek TUI’s LLM-generated `AGENTS.md` suggest that 2026 will see a de facto standard for agent–codebase communication—akin to how `Dockerfile` unified container builds.

2. **Context window gating is a major UX failure.** Claude Code’s “1M context credit” bugs (#63060 et al.) and Copilot CLI’s truncated long-context models (#3677) highlight that model capacity and billing are poorly communicated. Expect tooling to add explicit warnings or opt-out mechanisms.

3. **Platform parity remains elusive.** Windows and Linux users consistently face worse experiences: missing clipboard, broken sandboxes (Codex on Windows), PTY crashes (Gemini CLI), and WSL performance regressions. Developers on non-macOS should scrutinize each tool’s platform support matrix.

4. **MCP is the new plugin standard—but brittle.** Nearly every tool is adopting MCP, but parsing bugs (DeepSeek TUI #2744), prompt cache busting (Qwen Code #4777), and enterprise proxy issues (Copilot CLI #3636) indicate the ecosystem is still pre-1.0.

5. **Telemetry and usage transparency are demanded.** Issues like OpenCode’s persistent cost tracking (#7763) and DeepSeek TUI’s token visibility (#2666) show that developers want consumption data they can trust—without hidden background drain (Codex #24818).

6. **Remote execution is moving from nice-to-have to must-have.** Claude Code, Gemini CLI, and Pi all have active issues related to SSH, WSL, and remote context. As hybrid workflows grow, tools that cannot clearly communicate which machine is being acted upon will lose trust.

**Bottom Line for Decision-Makers:** For enterprise compliance, choose **Claude Code** or **Gemini CLI**. For desktop-first development with strong sandboxing, **OpenAI Codex** (once stability improves). For open ecosystem and provider flexibility, **Pi** or **OpenCode**. For deep GitHub integration, **Copilot CLI** (despite copy/paste woes). For Chinese market or lightweight needs, **Kimi Code**. For daemon-based IDE integration, **Qwen Code**. For complex multi-tab workflows, **DeepSeek TUI** (if stabilization gates are cleared).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026-06-05 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The most-discussed Skill proposals (by comment activity) are all open PRs, reflecting a community actively shaping the Skills collection.

| # | Skill PR | Description | Discussion Highlights | Status |
|---|----------|-------------|----------------------|--------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) – *document-typography* | Typographic quality control for AI-generated documents – fixes orphan words, widows, and numbering misalignment. | Addresses a universal pain point in Claude output. Community feedback centers on edge cases (e.g., CJK text) and whether the skill should be part of a broader “document-quality” bundle. | Open (created 2026-03-04) |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) – *ODT skill* | Create, fill, read, and convert OpenDocument files (.odt, .ods) with LibreOffice integration. | High interest from enterprise users who rely on open‑source document formats. Requests for template‑filling examples and ODS spreadsheet support. | Open (created 2026-03-01) |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) – *frontend-design revision* | Improves clarity and actionability of the existing frontend‑design skill; ensures instructions are executable in a single conversation. | Strong sentiment that the original skill was too vague. The PR proposes specific prompts and constraints; reviewers are negotiating scope vs. brevity. | Open (created 2026-01-05) |
| 4 | [#83](https://github.com/anthropics/skills/pull/83) – *skill-quality-analyzer + skill-security-analyzer* | Meta‑skills that evaluate other skills across five quality dimensions and security patterns. | Pioneers “Skills about Skills”. Debate on whether these should live in the main repo or in a dedicated quality‑assurance plugin. | Open (created 2025-11-06) |
| 5 | [#538](https://github.com/anthropics/skills/pull/538) – *case‑sensitive file references fix (pdf)* | Fixes 8 case‑sensitivity mismatches in `skills/pdf/SKILL.md` that break on Linux. | Small but critical – highlights the lack of cross‑platform testing in the repo. Reviewers call for a broader case‑sensitivity CI check. | Open (created 2026-03-06) |
| 6 | [#539](https://github.com/anthropics/skills/pull/539) – *unquoted YAML validation* | Pre‑parse check in `quick_validate.py` to catch unquoted `description` fields with colons. | Prevents silent YAML parsing failures that have plagued multiple skill authors. Community wants this integrated into the standard lint‑on‑PR check. | Open (created 2026-03-06) |
| 7 | [#541](https://github.com/anthropics/skills/pull/541) – *DOCX tracked‑change ID collision* | Prevents document corruption when adding tracked changes to docs with existing bookmarks by avoiding shared `w:id` collisions. | Reproduces a bug many users encountered. Fix uses dynamic ID generation; reviewers are verifying the fix against complex OOXML documents. | Open (created 2026-03-06) |
| 8 | [#181](https://github.com/anthropics/skills/pull/181) – *SAP‑RPT‑1‑OSS predictor* | Uses SAP’s open‑source tabular foundation model for predictive analytics on SAP business data. | Niche but enthusiastic reception from SAP ecosystem. Discussion focuses on model license compliance and data privacy concerns when interacting with enterprise data. | Open (created 2025-12-28) |

*Note: All PRs are open; none have been merged yet.*

---

## 2. Community Demand Trends

From the most‑commented Issues, four clear demand patterns emerge:

- **Cross‑platform compatibility** – Issues [#556](https://github.com/anthropics/skills/issues/556) (0% trigger rate on Windows) and the several PRs fixing Windows subprocess bugs reveal that many contributors and end‑users work on Windows and Linux. The community wants skills and tooling that work reliably across platforms.

- **Skill lifecycle management** – Issues [#228](https://github.com/anthropics/skills/issues/228) (org‑wide sharing) and [#62](https://github.com/anthropics/skills/issues/62) (skills disappearing) signal a need for better distribution, versioning, and import/export workflows. Users want a Skill library, not just single‑file downloads.

- **Security and trust boundaries** – Issue [#492](https://github.com/anthropics/skills/issues/492) raises alarm about community skills distributed under the `anthropic/` namespace, creating trust‑boundary risks. This is the most critical security discussion in the tracker.

- **Evaluation and quality tooling** – Issue [#556](https://github.com/anthropics/skills/issues/556) and Issue [#202](https://github.com/anthropics/skills/issues/202) (skill‑creator best practices) show demand for robust, cross‑platform evaluation harnesses (`run_eval.py`) and clear authoring guidelines. The community wants to “test” Skills as rigorously as unit tests.

---

## 3. High‑Potential Pending Skills

These open PRs have active review threads and mature code – they are likely to be merged soon:

1. **[[#1140](https://github.com/anthropics/skills/pull/1140)] – agent‑creator meta‑skill**  
   Creates task‑specific agent sets and includes critical fixes for multi‑tool evaluation and Windows compatibility. Updated as recently as 2026‑06‑02. The first “meta‑skill” that dynamically builds agent configurations.

2. **[[#1099](https://github.com/anthropics/skills/pull/1099)] – Windows subprocess fix for `run_eval.py`**  
   Solves a showstopper on Windows where every query is recorded as “not triggered”. One‑line fix that restores usability for the entire evaluation pipeline.

3. **[[#1050](https://github.com/anthropics/skills/pull/1050)] – Windows subprocess + encoding fixes**  
   Complementary to [#1099], addresses `PATHEXT` resolution and encoding bugs. Both PRs together will make the skill‑creator toolset fully Windows‑compatible.

4. **[[#723](https://github.com/anthropics/skills/pull/723)] – testing‑patterns skill**  
   Covers testing trophy philosophy, unit testing, React component testing, API testing, and fuzzing. Clean, well‑structured skill with high relevance for developer‑facing Claude use cases.

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is **cross‑platform robustness with enterprise‑grade document handling** – users want skills that work on Windows, macOS, and Linux equally, and they consistently prioritize skills that manipulate real‑world file formats (ODT, DOCX, PDF, typography fixes) without corruption or platform‑specific bugs.

---

# Claude Code Community Digest — 2026-06-05

## Today's Highlights

A new release (v2.1.163) introduces enterprise-grade version gating via `requiredMinimumVersion`/`requiredMaximumVersion` managed settings and a `/plugin list` command. The community is heavily debating the **AGENTS.md** standard (Issue #6235, 4,060 👍), signalling a potential shift toward interoperability across coding agents. Meanwhile, a cluster of high-severity bugs around 1M context credits and tool-call parsing failures (Issues #63060, #61869, #62063, #62123) continue to frustrate users on Pro plans.

## Releases

**v2.1.163** — [GitHub](https://github.com/anthropics/claude-code/releases/tag/v2.1.163)

- `requiredMinimumVersion` / `requiredMaximumVersion` managed settings — Claude Code will refuse to start if its version is outside the allowed range, directing users to an approved version. Useful for enterprise compliance.
- `/plugin list` command — lists installed plugins with `--enabled`/`--disabled` filtering.

## Hot Issues

1. **#6235 — [ENHANCEMENT] Support AGENTS.md**  
   [GitHub](https://github.com/anthropics/claude-code/issues/6235)  
   *4,060 👍 · 310 comments · OPEN*  
   The most upvoted issue ever. Users want a universal `AGENTS.md` format (already adopted by Codex, Amp, Cursor) for cross-agent codebase understanding, rather than Claude-specific `CLAUDE.md`. Signals a strong desire for ecosystem interoperability.

2. **#63060 — [BUG] API Error: Usage credits required for 1M context**  
   [GitHub](https://github.com/anthropics/claude-code/issues/63060)  
   *19 👍 · 63 comments · OPEN*  
   macOS users hitting credits errors when trying to use the 1M context window. Often paired with Pro plan limitations.

3. **#61869 — [BUG] Same credits error on Linux with opus-plan model**  
   [GitHub](https://github.com/anthropics/claude-code/issues/61869)  
   *14 👍 · 56 comments · CLOSED*  
   Closed as duplicate of #63060, but highlights the cross-platform nature of the credit-gating issue.

4. **#62063 — [BUG] Claude Code defaults to 1M context on fresh session with no workaround on Pro plan**  
   [GitHub](https://github.com/anthropics/claude-code/issues/62063)  
   *35 👍 · 54 comments · OPEN*  
   Pro users cannot opt out of 1M context, leading to unexpected usage credit depletion. High frustration.

5. **#62123 — [BUG] Model's tool call could not be parsed (retry also failed)**  
   [GitHub](https://github.com/anthropics/claude-code/issues/62123)  
   *91 👍 · 45 comments · OPEN*  
   Opus 4.7 users on macOS/VSCode frequently hit unrecoverable tool-call parsing errors. Reproducible, no workaround.

6. **#63875 — [BUG] Recurring tool call parsing error on Windows**  
   [GitHub](https://github.com/anthropics/claude-code/issues/63875)  
   *45 👍 · 32 comments · OPEN*  
   Same error pattern across platforms; sessions abort mid-task. Affects both Windows and, by relation, other OSes.

7. **#53940 — [BUG] Cowork Edit/Write tools silently truncate files via byte-conservation buffer cap**  
   [GitHub](https://github.com/anthropics/claude-code/issues/53940)  
   *11 👍 · 22 comments · OPEN*  
   Deterministic data loss: regardless of file size, a buffer cap truncates writes without warning. Serious integrity issue for Cowork mode.

8. **#33932 — [FEATURE] VS Code Extension: Diff review UI akin to GitHub Copilot Edits Review**  
   [GitHub](https://github.com/anthropics/claude-code/issues/33932)  
   *81 👍 · 18 comments · OPEN*  
   Community wants a proper diff review panel before applying changes. High upvote count indicates strong demand for IDE-integrated approval workflows.

9. **#36497 — [BUG] `.claude/skills/` edits prompt for permission despite being documented as exempt (regression in 2.1.79)**  
   [GitHub](https://github.com/anthropics/claude-code/issues/36497)  
   *10 👍 · 8 comments · OPEN*  
   Regression that breaks self-modifying skills workflows. Users rely on this exemption for dynamic skill updates.

10. **#65527 — [ENHANCEMENT] Remote sessions don't clearly indicate which machine commands execute on**  
    [GitHub](https://github.com/anthropics/claude-code/issues/65527)  
    *0 👍 · 3 comments · OPEN*  
    New issue highlighting UX confusion: when local and remote sessions coexist in the same project group, there's no persistent indicator of execution context. Could cause destructive actions on the wrong machine.

## Key PR Progress

1. **#65344 — fix(scripts): correct premature return in markStale and add --debug flag to auto-close-duplicates**  
   [GitHub](https://github.com/anthropics/claude-code/pull/65344)  
   Fixes a pagination bug in stale-issue marking that could skip large batches of old issues. Also improves duplicate auto-closure logging.

2. **#44742 — fix: diagnostic tool + root cause analysis for session persistence data loss (#12908)**  
   [GitHub](https://github.com/anthropics/claude-code/pull/44742)  
   *CLOSED*  
   Adds a diagnostic script (`scripts/diagnose-session-persistence.ts`) to address a critical VS Code extension bug where conversation history disappears on IDE restart. Ties together 12+ duplicate reports since Dec 2025.

3. **#58673 — s**  
   [GitHub](https://github.com/anthropics/claude-code/pull/58673)  
   *OPEN, single-character description*  
   Minimal PR; likely a test or accidental submission. No meaningful changes visible.

4. **#65286 — fix(plugins): add missing plugin.json manifest for plugin-dev**  
   [GitHub](https://github.com/anthropics/claude-code/pull/65286)  
   Corrects the developer plugin's manifest, enabling proper discovery and installation via the plugin system.

5. **#65314 — scripts: add detect-theme-color-issues to cluster light-theme color violations**  
   [GitHub](https://github.com/anthropics/claude-code/pull/65314)  
   New triage script that scans issues for invisible/unreadable text on light terminal themes, grouping them under the known `color7`/`color0` collision family. Helpful for reducing duplicate maintenance.

6. **#65223 — Spelling: Fix typo in security guidance plugin**  
   [GitHub](https://github.com/anthropics/claude-code/pull/65223)  
   *CLOSED*  
   Minor fix: "reqwest" → "request" in the security guidance plugin.

## Feature Request Trends

- **AGENTS.md interoperability (#6235, 4,060 👍)** — Overwhelming demand for a universal agent configuration standard. This dwarfs all other feature requests.
- **VS Code diff review UI (#33932, #31888)** — Strong preference for a batch-review panel similar to Cursor's native agent and GitHub Copilot Edits, allowing developers to approve changes in bulk before they're applied.
- **Programmatic session customization (#58588)** — Allow `/rename` and `/color` to be set at session start via CLI flags or config, enabling automated workflows and multi-session management.
- **Unlimited retention / archiving (#65533)** — Community wants `cleanupPeriodDays` to default to no retention limit, with archival instead of deletion.
- **Remote session context clarity (#65527)** — New request for persistent indicators showing which machine (local vs remote) is being acted upon.

## Developer Pain Points

1. **1M Context credit gating (Issues #63060, #61869, #62063)** — Pro plan users consistently hitting "usage credits required" errors when the tool defaults to 1M context. No option to downgrade context size. High volume of duplicates suggests a systemic UX failure.

2. **Tool-call parsing errors (#62123, #63875)** — Intermittent but session-aborting failures with "The model's tool call could not be parsed (retry also failed)". Occurs across platforms and models, no clear workaround.

3. **Cowork data loss (#53940)** — Silent file truncation due to byte-conservation buffer caps. Erodes trust in the file-writing subsystem.

4. **Session persistence loss (PR #44742, linked issues)** — VS Code extension fails to save conversations to disk, causing history loss on restart. Over 12 duplicates filed since December 2025.

5. **Permission regression for skills (#36497)** — `.claude/skills/` edits now prompt for permission after v2.1.79, breaking automated skill updates that were documented as exempt.

6. **Orphaned `claude` processes (#65540)** — Removing a session from history in VS Code does not terminate its underlying process, leading to accumulation of zombie processes, especially under Remote-SSH.

7. **Non-GitHub remote warnings (#65522)** — "Pull request status couldn't be checked" fires on every interaction for GitLab/Bitbucket/Gitea repos, polluting the UX with irrelevant warnings.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-05

*Data source: [github.com/openai/codex](https://github.com/openai/codex)*

---

## Today’s Highlights

Four new Rust alpha releases (v0.138.0-alpha.1–.4) landed, but the community’s attention is firmly on desktop stability: macOS users are reporting a severe `syspolicyd` file descriptor leak that freezes app launches system‑wide, while Windows users face sandbox setup failures and WSL performance regressions. On the PR side, the team is pushing improvements in sandbox policy derivation, OAuth token refresh, and CI speed, alongside a new deep‑link feature for opening workspaces on Windows.

---

## Releases

- **[rust‑v0.138.0‑alpha.1](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.1)**, **[.2](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.2)**, **[.3](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.3)**, **[.4](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.4)** – Four incremental alpha releases of the Rust‑based Codex runtime. No detailed changelog provided; likely contain fixes and preparation for the next stable CLI release.

---

## Hot Issues

1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   97 comments, 476 👍. The most‑voted feature request. Users want a native Linux app to escape macOS power/thermal issues and to leverage powerful Linux desktops. Still open since February.

2. **[#20741 – Desktop chat histories disappeared after recent update](https://github.com/openai/codex/issues/20741)**  
   26 comments. Multiple Pro users report lost project chat histories on macOS after updating to build 2345. High impact for daily workflows.

3. **[#24391 – Windows sandbox: spawn setup refresh fails on CLI 0.133.0](https://github.com/openai/codex/issues/24391)**  
   22 comments. After updating the npm package, shell commands fail due to sandbox setup errors. Affects Windows users with npm global install.

4. **[#25715 – Codex App is unusably slow with WSL as agent environment](https://github.com/openai/codex/issues/25715)**  
   21 comments, 22 👍. Routine turns take excessive time on Windows + WSL. A common configuration for developers.

5. **[#25719 – macOS `syspolicyd` / `trustd` CPU and memory runaway](https://github.com/openai/codex/issues/25719)**  
   14 comments. Codex Desktop triggers persistent high CPU/memory in system security processes. Linked to a broader file descriptor leak.

6. **[#25882 – macOS app relaunches own binary in tight loop, exhausting `syspolicyd`](https://github.com/openai/codex/issues/25882)**  
   12 comments. Even more severe: Codex repeatedly launches its own binary, causing system‑wide app freeze. Pro users affected.

7. **[#25249 – Windows semi‑transparent sidebar causes transparent/undrawn regions when maximized](https://github.com/openai/codex/issues/25249)**  
   13 comments. UI rendering bug – enabling the semi‑transparent sidebar option makes parts of the window invisible.

8. **[#25220 – Bundled plugins unavailable on Windows due to EFS‑encrypted files](https://github.com/openai/codex/issues/25220)**  
   12 comments. Computer Use, Browser, Chrome, LaTeX plugins fail to install because of Windows file encryption restrictions.

9. **[#20683 – Computer Use crashes `SkyComputerUseService` when inspecting Outlook on macOS](https://github.com/openai/codex/issues/20683)**  
   11 comments. `get_app_state` call causes service crash. Affects macOS users automating Outlook.

10. **[#26363 – Custom `.codex/agents` no longer selectable in CLI v0.137.0](https://github.com/openai/codex/issues/26363)**  
    3 comments, 5 👍. Regression: custom agent definitions are ignored; subagents inherit the parent model instead of the configured one. Reported as a blocker for power users.

---

## Key PR Progress

1. **[#26490 – Use standalone tools for Responses Lite](https://github.com/openai/codex/pull/26490)**  
   Routes web search and image generation through Codex‑owned executors for the new “Responses Lite” model path. Internal infrastructure for upcoming model optimizations.

2. **[#25147 – Retry streamable HTTP initialize failures](https://github.com/openai/codex/pull/25147)**  
   Adds retry logic for transient HTTP failures during RMCP startup and `tools/list`. Improves reliability of MCP tool integrations.

3. **[#26482 – Fix: refresh expired OAuth tokens before startup](https://github.com/openai/codex/pull/26482)**  
   Fixes a bug where an already‑expired OAuth token would be treated as zero‑lifetime, causing authentication failures. Merged.

4. **[#26499 – Derive exec policy filesystem policy from profile](https://github.com/openai/codex/pull/26499)**  
   Removes a separate `FileSystemSandboxPolicy` in favor of using `PermissionProfile`’s own sandbox policy. Reduces split states and aligns production permission model.

5. **[#26023 – Add managed macOS sandbox capabilities](https://github.com/openai/codex/pull/26023)**  
   Adds typed macOS Seatbelt capabilities to managed permission profiles. Prepares for better sandboxing on macOS while preserving debug flags.

6. **[#26307 – Respect Windows sandbox backend in exec policy](https://github.com/openai/codex/pull/26307)**  
   Fixes a gap where Windows managed read‑only permissions were not backed by the real sandbox, causing benign commands to be blocked. Important for Windows users.

7. **[#26500 – Open Windows app workspaces via deep link](https://github.com/openai/codex/pull/26500)**  
   Enables `codex app PATH` to directly open a workspace in Codex Desktop using `codex://` deep links, instead of showing a manual instruction.

8. **[#26496 – Make auto‑review on‑request prompt more proactive](https://github.com/openai/codex/pull/26496)**  
   Tunes the prompt for auto‑reviewed approval policies so that likely sandbox blocks are escalated earlier, reducing failed commands inside sandbox.

9. **[#26256 – Keep Bazel startup options stable across commands](https://github.com/openai/codex/pull/26256)**  
   Fixes unnecessary Bazel server restarts caused by mismatched remote repo cache flags. Speeds up repeated development commands.

10. **[#26479 – Speed up local nextest runs](https://github.com/openai/codex/pull/26479)**  
    Allows bounded parallel execution of integration tests on developer machines, significantly cutting local test suite time without affecting CI.

---

## Feature Request Trends

- **Linux Desktop App** – Issue [#11023](https://github.com/openai/codex/issues/11023) (476 👍) remains the top request. Users urge OpenAI to release a native Linux build to avoid macOS thermal/power issues.
- **Auto‑resume CLI sessions after quota reset** – Issue [#21073](https://github.com/openai/codex/issues/21073) (9 👍). Users want the CLI to automatically continue paused tasks when usage limits reset, especially overnight.
- **Improved CLI copy‑paste** – Issue [#24685](https://github.com/openai/codex/issues/24685) (1 👍). Annoyance with multi‑line copy from the terminal UI; a common quality‑of‑life request.
- **Custom agent / subagent model selection fix** – Issue [#26363](https://github.com/openai/codex/issues/26363) (5 👍). Regression in v0.137.0 prevents custom agents from being used; developers rely on this for specialized workflows.

---

## Developer Pain Points

- **macOS system‑level resource leaks** – Multiple issues ([#25719](https://github.com/openai/codex/issues/25719), [#25882](https://github.com/openai/codex/issues/25882), [#26117](https://github.com/openai/codex/issues/26117), [#26341](https://github.com/openai/codex/issues/26341)) describe Codex causing `syspolicyd` file descriptor exhaustion, leading to system‑wide freezes and “damaged” DMG errors. This is the most urgent stability concern.
- **Windows sandbox & WSL performance** – Issues [#24391](https://github.com/openai/codex/issues/24391), [#25715](https://github.com/openai/codex/issues/25715), [#23277](https://github.com/openai/codex/issues/23277) highlight persistent sandbox setup failures and 20‑second first‑token delays under WSL. Windows developers face a degraded experience.
- **Memory / file handle leaks** – Bugs [#26015](https://github.com/openai/codex/issues/26015) (memory not released on Windows) and [#25243](https://github.com/openai/codex/issues/25243) (“Too many files opened”) indicate resource management issues across platforms.
- **Plugin & browser integration fragility** – [#25220](https://github.com/openai/codex/issues/25220) (bundled plugins blocked by EFS), [#24814](https://github.com/openai/codex/issues/24814) (browser blocked by enterprise policy), and [#25271](https://github.com/openai/codex/issues/25271) (Chrome URL detection failure) show that bundled tooling remains brittle on Windows.
- **Unexplained usage drain** – [#24818](https://github.com/openai/codex/issues/24818) reports usage limit being consumed even when the app/CLI is idle, raising concerns about background activity or telemetry overhead.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-05

## Today’s Highlights

A **critical patch release (v0.45.1)** addresses a high-impact bug from v0.45.0, while the latest nightly (v0.47.0-nightly) focuses on CI pipeline improvements. The community is seeing a surge of P1/P2 PRs targeting **PTY crash stability**, **SSRF prevention**, and **Windows/WSL interop**, reflecting a strong push toward hardening the CLI for enterprise use. Meanwhile, longstanding issues around **symlink handling** and **terminal responsiveness** continue to gather community attention.

---

## Releases

### v0.45.1 (Patch)
- Cherry-pick of a critical fix from the main branch to address a regression in v0.45.0
- **Direct link:** [v0.45.1 Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.45.1)

### v0.47.0-nightly.20260604
- CI workflow optimizations: PR size labeler and batch workflows added
- Fix for fork PR write access using `pull_request_target` trigger
- **Direct link:** [Nightly Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.47.0-nightly.20260604.g4196596f7)

---

## Hot Issues

1. **[#22171 — BFS file search & grep silently skip symbolic links](https://github.com/google-gemini/gemini-cli/issues/22171)**  
   *P1, Core, Bug* — Silent omission of symlinks during file discovery and grep operations. In symlink-heavy monorepos, this means linked `GEMINI.md` files and documentation are invisible to the agent. Community has flagged this as a major blind spot for complex project structures.

2. **[#24098 — CLI becomes unresponsive after `/copy` command](https://github.com/google-gemini/gemini-cli/issues/24098)**  
   *P2, Core, Bug* — `/copy` copies content but leaves the command text in the input field and halts further interaction. Frustrating UX break for a frequently used feature.

3. **[#21597 — Workspace root detection fails in Mercurial repos](https://github.com/google-gemini/gemini-cli/issues/21597)**  
   *P2, Enterprise, Bug* — CLI requires a `.git` directory to anchor policies; Mercurial (Hg) users get incomplete configuration loading. Enterprise teams using non-Git VCS are effectively second-class citizens.

4. **[#22520 — Usage tracking shows preview model at 82% before use](https://github.com/google-gemini/gemini-cli/issues/22520)**  
   *P2, Core, Bug* — Model usage metrics report non-zero consumption for models the user hasn’t invoked. Confusing and erodes trust in the billing/rate-limit display.

5. **[#24264 — Requests to ANY model get stuck forever](https://github.com/google-gemini/gemini-cli/issues/24264)**  
   *P2, Enterprise, Bug* — Complete request hang with no error messages, affecting all models. 5 👍 reactions indicate widespread impact. Community suspects a networking or authentication layer issue in enterprise proxy configurations.

6. **[#21662 — Dreadful startup time on HDDs (77 sec cold start)](https://github.com/google-gemini/gemini-cli/issues/21662)**  
   *P1, Core, Bug* — Cold startup measured at 77 seconds; even warm starts are slow. A major barrier for developers on older hardware or CI environments.

7. **[#24039 — Silent model fallback on 429 capacity errors](https://github.com/google-gemini/gemini-cli/issues/24039)**  
   *P2, Agent, Bug* — When a pinned model hits capacity, CLI silently switches to a different model without user notification. Breaks deterministic workflows and can corrupt critical tasks. 3 👍 — clearly a trust issue.

8. **[#27334 — Embedded terminal freezes after background commands on Windows](https://github.com/google-gemini/gemini-cli/issues/27334)**  
   *P1, Core, Bug* — PTY terminal becomes glitched/frozen after running shell commands inside Gemini’s embedded terminal. Windows-specific, linked to process management and build execution.

9. **[#27155 — PTY memory and file descriptor leak in ShellExecutionService](https://github.com/google-gemini/gemini-cli/issues/27155)**  
   *P2, Core, Bug* — Long-running background processes (e.g., MCP servers) leak `ptyProcess` and `headlessTerminal` instances if the log stream fails to emit `end()`. Resource exhaustion risk for heavy users.

10. **[#27030 — AfterAgent hook payload contains duplicated/corrupted streaming text](https://github.com/google-gemini/gemini-cli/issues/27030)**  
    *P2, Extensions, Bug* — Hook payloads meant for downstream processing contain duplicated chunks from the streaming buffer. Breaks reliability for integrations depending on clean prompt_response data.

---

## Key PR Progress

1. **[#27505 — Fix extra spaces on width-0 CJK continuation cells](https://github.com/google-gemini/gemini-cli/pull/27505)**  
   *Open, P2, Core* — Fixes a rendering bug where wide CJK characters get spurious whitespace injected. Critical for international users and copy-paste accuracy.

2. **[#27341 — Strip functionCall.id / functionResponse.id before API call](https://github.com/google-gemini/gemini-cli/pull/27341)**  
   *Closed, P2, Agent* — Resolves a 400 error on any turn following a tool call. Internal IDE-only IDs were leaking to the Gemini API payload.

3. **[#27354 — Bypass node-pty on WSL for Windows executables](https://github.com/google-gemini/gemini-cli/pull/27354)**  
   *Closed, P2, Core* — Implements a fallback to standard `child_process` when running `.exe` files inside WSL, fixing PTY interop issues on that platform.

4. **[#27348 — Wrap Ajv validate() in try/catch to prevent crash on malformed schemas](https://github.com/google-gemini/gemini-cli/pull/27348)**  
   *Closed, P1, Agent* — Prevents a crash when the LLM sends unexpected parameter shapes; Ajv’s internal traverser was throwing on undefined.

5. **[#27349 — Strip CJK characters from model thought output](https://github.com/google-gemini/gemini-cli/pull/27349)**  
   *Closed, P2, Agent* — Filters non-English (CJK) characters from the model’s internal thought text to prevent leaked foreign text in English sessions.

6. **[#27347 — Add command validation to prevent natural language from being saved as shell commands](https://github.com/google-gemini/gemini-cli/pull/27347)**  
   *Closed, P2, Core* — Stops MCP/discovered commands like “mostrar diretório” from being written directly into `settings.json`.

7. **[#27335 — Prevent SSRF via open redirect in web-fetch tool](https://github.com/google-gemini/gemini-cli/pull/27335)**  
   *Closed, Core* — Critical security fix: HTTP redirects were followed without URL validation, enabling SSRF attacks against internal metadata endpoints.

8. **[#27329 — Skip missing includeDirectories instead of crashing CLI startup](https://github.com/google-gemini/gemini-cli/pull/27329)**  
   *Closed, P1, Core* — One missing `includeDirectories` entry would abort the entire CLI startup. Now gracefully skips missing paths.

9. **[#27343 — Persist A2A task workspaces from settings](https://github.com/google-gemini/gemini-cli/pull/27343)**  
   *Closed, Core* — Ensures A2A task workspaces archive from the configured settings path rather than the process-global CWD. Adds regression tests.

10. **[#27511 — Correct settings.json filename in max session turns message](https://github.com/google-gemini/gemini-cli/pull/27511)**  
    *Open, P2, Core* — Fixes an error message referencing `setting.json` (singular) instead of the actual `settings.json` filename, addressing confusion reported in #25889.

---

## Feature Request Trends

- **Enterprise VCS support** — Mercurial (Hg) workspace detection is a recurring ask; teams outside the Git ecosystem need equal policy support.
- **Behavioral evaluation framework** — Multiple issues request a formal `gemini eval` subcommand for regression testing, hallucination detection, and instruction-following benchmarks.
- **Higher token/context limits** — Users working on large projects consistently push for increased context windows and parallel agent execution.
- **Optimistic MCP tool execution in Plan Mode** — A `trustReadOnlyHint` opt-in setting would allow read-only MCP tools to skip the approval dialog, streamlining read-heavy workflows.
- **Corporate proxy / custom LLM gateway documentation** — Enterprise users need explicit network configuration docs for proxies, gateways, and self-hosted models.

---

## Developer Pain Points

- **Silent failures and invisible state** — The CLI often fails silently: missing include directories abort startup without a helpful message, model fallback on 429 errors happens without warning, and symlinks are silently ignored. Trust erodes when the tool hides its own actions.
- **Terminal/PTY instability** — Frequent reports of terminal freezing on Windows, PTY leaks, and crashes after SSH disconnects. The embedded terminal experience remains fragile, especially on non-Linux platforms.
- **Windows and WSL interop issues** — WSL PTY problems, `.exe` execution failures, and process management glitches create a poor experience for the large Windows developer audience.
- **Session log recursion** — Agent search tools scan `.gemini/tmp/` by default, creating a feedback loop where the agent indexes its own past session logs, bloating context and confusing behavior.
- **CJK and internationalization bugs** — Spurious whitespace in CJK output, leaked non-English thought text, and broken character rendering undermine global usability.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-05

## Today's Highlights

A new release (v1.0.60-0) shipped with several quality-of-life improvements, including vim-style navigation in the diff view and a `-r` shorthand for `--resume`. However, the community is grappling with a wave of regressions: copy/paste remains broken on Linux (issue #2082, now 3 months old with 19 comments), and a new session-listing regression (#3676) was rapidly reported and closed. Meanwhile, the "Not authenticated" error on resumed sessions (#3596) continues to frustrate users, with 8 upvotes in just five days.

## Releases

### v1.0.60-0 — 2026-06-05
- **Added** a `billing` help topic explaining AI credit usage features
- **Added** vim-style navigation keys (`g`, `G`, `Ctrl+D`, `Ctrl+U`) to the `/diff` view
- **Added** Mission Control sharing status display in the `/session info` view
- **Added** `-r` as a shorthand for `--resume`
- **Changed** LSP server configuration (details referenced as "config a" in changelog, likely a partial log)

## Hot Issues

1. **#2082 — `ctrl+shift+c` doesn't copy to clipboard on Linux**  
   *[OPEN] | 19 comments | 8 👍*  
   A 3-month-old regression that blocks the most basic copy workflow for Linux users. Despite workarounds (ctrl+c, right-click), the community remains vocal about the lack of a fix.  
   [Link](github/copilot-cli Issue #2082)

2. **#3260 — Copy/paste broken in SSH + tmux sessions to Windows Server 2025**  
   *[OPEN] | 6 comments*  
   A niche but severe cross-platform regression introduced in v1.0.47. Demonstrates how copy/paste reliability is a top concern across environments.  
   [Link](github/copilot-cli Issue #3260)

3. **#3659 — CLI cannot execute hooks shipped with plugins (Windows)**  
   *[OPEN] | 3 comments*  
   Blocking all prompts for Windows users with governance- or security-hook plugins. The error is a preToolUse hook failure, effectively making the CLI unusable on Windows for affected teams.  
   [Link](github/copilot-cli Issue #3659)

4. **#3529 — Copilot PR review error loop**  
   *[OPEN] | 3 comments | 3 👍*  
   Users are stuck in a retry cycle with no actionable feedback. The error occurs across both CLI and UI, suggesting a backend or quota issue.  
   [Link](github/copilot-cli Issue #3529)

5. **#3666 — Copying wrapped output removes spaces (e.g., `var c` → `varc`)**  
   *[CLOSED] | 3 comments*  
   A terminal-rendering bug that corrupts source code during copy-paste. Closed quickly, but the root cause (wrapping breaks space characters) remains a concern for code users.  
   [Link](github/copilot-cli Issue #3666)

6. **#2398 — Support a default config file for permissions**  
   *[OPEN] | 3 comments | 10 👍*  
   The most-upvoted feature request. Users find session-level permission prompts too tedious and want a persistent, defaults-based permission system.  
   [Link](github/copilot-cli Issue #2398)

7. **#3596 — "Error loading model list: Not authenticated" on session resume**  
   *[OPEN] | 2 comments | 8 👍*  
   Resuming a session loses the authentication context for the model picker. A high-severity bug: users can talk to previous models but can't switch models in a resumed session.  
   [Link](github/copilot-cli Issue #3596)

8. **#3636 — Voice mode fails on corporate VPN (catalog unreachable)**  
   *[OPEN] | 2 comments | 3 👍*  
   Voice mode is completely blocked behind corporate networks. The CLI hard-requires the model catalog before activation, with no offline or proxy fallback.  
   [Link](github/copilot-cli Issue #3636)

9. **#3677 — claude-opus-4.7-1m-internal triggers compaction at 18% of real capacity**  
   *[OPEN] | 1 comment*  
   A core context-window bug: the CLI reads model capacity from two sources and picks the smaller value, cutting long-context models to 128K instead of 936K. High impact for heavy code-context users.  
   [Link](github/copilot-cli Issue #3677)

10. **#3676 — `/session` no longer lists other sessions**  
    *[CLOSED] | 1 comment*  
    A regression in v1.0.59 that hid sessions from other workspaces. Rapidly reported and closed; the fix likely targets session enumeration.  
    [Link](github/copilot-cli Issue #3676)

## Key PR Progress

Only **2 PRs** were updated in the last 24 hours. Both appear to be spam or low-quality contributions:

1. **#3651 — `Create xcopilotcli`** (OPEN) — No description; likely a test or spam PR.  
   [Link](github/copilot-cli PR #3651)

2. **#3473 — Update project name in README** (OPEN) — Contains a phishing-style GCash/Temu referral link.  
   [Link](github/copilot-cli PR #3473)

**Note:** No significant or functional PRs were active in the last 24 hours. Most code changes appear to be shipping directly as releases.

## Feature Request Trends

1. **Persistent Permission Configuration** — The highest-upvoted request (#2398, 10 👍) asks for a default config file to avoid per-session permission prompts. Users want to grant directory access and tool permissions once, across sessions.

2. **BYOK/Authentication Reliability** — Multiple requests (#3682, #3596, #2783) ask for better token lifecycle management: short-lived credentials should be refreshable without restarting the CLI, and OAuth tokens for MCP servers should be stored securely, not as plaintext JSON.

3. **Agent Configuration Depth** — Users want to configure model effort, context length, and retrieval-augmented generation (RAG) settings per agent (#3678), not just pick a model name.

4. **Localization** — A new request (#3681) asks for Spanish translations of command descriptions, suggesting growing international use.

5. **Machine-Level Custom Slash Commands** — Users want personal commands available across all repos (#3343), mirroring IDE-level customization.

## Developer Pain Points

- **Copy/Paste is Broken Everywhere** — Three active issues (#2082, #3260, #3666) cover Linux, SSH/tmux, and terminal rendering. This is the #1 reliability complaint.
- **Authentication Tokens Expire Silently** — Resumed sessions lose model access (#3596), BYOK providers require process restart (#3682), and OAuth tokens are stored insecurely (#2783).
- **Context Window Mismanagement** — Long-context models are incorrectly truncated (#3677). Users lose 80%+ of usable capacity without warning.
- **Windows is Falling Behind** — Hooks don't execute (#3659), console handles are missing (#3683), and tilde expansion fails in hook `cwd` (#3664). Windows users face a disproportionate number of blockers.
- **Spam PRs Overwhelm the Queue** — Both PRs updated today are non-functional or malicious, suggesting a lack of maintainer capacity for triaging low-quality contributions.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-06-05**.

---

## 1. Today’s Highlights

The community is experiencing a surge of authentication-related “403 Forbidden” errors, suggesting a potential backend configuration or token scope change is affecting many users. Concurrently, a major UI/UX bug in Linux terminals—where scrolling through past conversation history is forcibly interrupted by an auto-scroll cursor blink—has been submitted and already patched by the community in a same-day PR. Developers are also widely reporting a perceived performance regression (slower response times) specifically in the latest `v1.46.0` release, especially when using the `kimi-k2.6` model.

## 2. Releases

**No new releases in the last 24 hours.**
The last publicly available version remains `v1.46.0`.

## 3. Hot Issues

**Seven issues were updated in the last 24 hours. All are listed below due to their direct impact on daily workflows.**

1.  **#2425 – 403 Forbidden Error for Coding Agents**
    URL: `MoonshotAI/kimi-cli Issue #2425`
    - **Symptom**: Every request returns `403 Kimi For Coding is currently only available for Coding Agents`.
    - **Why it matters**: This is the most significant blocker today. It is actively discussed (10 comments, 3 👍). Users retrying with different models or accounts are hitting a paywall or misconfiguration. This points to either a server-side authorization issue or a strict enforcement of subscription tiers.
    - **Community Reaction**: User `zhongyr` reports the issue affects version `0.9.0` with the `kimi-for-coding` model.

3.  **#2427 – 403 Error via Login**
    URL: `MoonshotAI/kimi-cli Issue #2427`
    - **Symptom**: Getting the same “Kimi For Coding is only available for Coding Agents” error when using the `/login` flow.
    - **Why it matters**: This suggests the issue is not limited to direct API key usage but also affects account-based (browser/login) authentication paths.
    - **Community Reaction**: Users are stuck trying to authenticate from WSL2/Debian.

5.  **#2422 – Auto-Scroll Bug in Linux Terminals**
    URL: `MoonshotAI/kimi-cli Issue #2422`
    - **Symptom**: After a conversation ends, scrolling up to read previous output is impossible as the terminal auto-scrolls to the bottom every ~1 second.
    - **Why it matters**: This breaks the ability to review large code outputs and historical logs. Likely caused by an idle cursor blink or a UI re-render polling interval.
    - **Community Reaction**: High visibility; quickly linked to a fix in PR #2429.

7.  **#2430 – Auto Logout Mid-Task**
    URL: `MoonshotAI/kimi-cli Issue #2430`
    - **Symptom**: The CLI logs out automatically in the middle of a long-running task.
    - **Why it matters**: This causes loss of session state and forces users to restart work, which is critical for developers relying on long background tasks.
    - **Community Reaction**: User mentions it happens “when they go do something else,” implying a session timeout or token refresh failure.

9.  **#2428 – ‘/title’ Command Missing in VS Code Extension**
    URL: `MoonshotAI/kimi-cli Issue #2428`
    - **Symptom**: The `/title` slash command works in the standalone CLI but is unavailable in the VS Code Kimi Code extension.
    - **Why it matters**: Indicates feature parity gaps between the CLI and the IDE extension.
    - **Community Reaction**: User on Linux RHEL expects consistent behavior across interfaces.

11. **#2424 – “Engine Overloaded” Errors**
    URL: `MoonshotAI/kimi-cli Issue #2424`
    - **Symptom**: Receiving “engine overloaded” errors persistently, particularly with the `k2.5` model.
    - **Why it matters**: Indicates backend capacity issues or recent infrastructure changes that are degrading service availability for certain model tiers.
    - **Community Reaction**: User notes this has been happening “over the past couple of days,” suggesting a systemic rather than transient issue.

13. **#2423 – Latest Versions Are Slower**
    URL: `MoonshotAI/kimi-cli Issue #2423`
    - **Symptom**: Version `1.46.0` is significantly slower than previous versions for the `Kimi-k2.6` model.
    - **Why it matters**: This is a performance regression affecting response times and developer productivity.
    - **Community Reaction**: User on `arm64` Linux reports a stark drop in speed, contrasting with earlier performance.

## 4. Key PR Progress

**Six pull requests were updated in the last 24 hours. All are included here due to their relevance to current bugs.**

1.  **#2429 – Fix: Prevent Idle Cursor Blink from Forcing Scroll to Bottom**
    URL: `MoonshotAI/kimi-cli PR #2429`
    - **Fix**: Addresses Issue #2422. It stops the terminal from jumping back to the bottom when the user scrolls up to read history on Linux.
    - **Status**: Open. Community response time is excellent (same day as the bug report).

3.  **#2388 – Fix(shell): Persist Pasted Text Placeholders**
    URL: `MoonshotAI/kimi-cli PR #2388`
    - **Fix**: Long pasted text is folded into placeholder references. This PR ensures those placeholders persist correctly after session history recall, preventing broken prompts.
    - **Status**: Open, awaiting review.

5.  **#2387 – Fix(tools): Preserve Shell Command Headline Details**
    URL: `MoonshotAI/kimi-cli PR #2387`
    - **Fix**: Improves the `Used Shell (...)` headline display. Previously, long commands were aggressively truncated (`shorten_middle`), making them unreadable. This PR likely uses a smarter truncation or expands the width limit.
    - **Status**: Open.

7.  **#2386 – Fix(session): Map Undo Wire Turns to Context Turns**
    URL: `MoonshotAI/kimi-cli PR #2386`
    - **Fix**: Resolves `/undo` and fork actions breaking when used after local slash-commands. It fixes a bug where the index for wire truncation didn’t align with the context log.
    - **Status**: Open. Related to Issues #1974 and #2049.

9.  **#2383 – Fix(soul): Repair Orphan Tool Calls When Replaying History**
    URL: `MoonshotAI/kimi-cli PR #2383`
    - **Fix**: Prevents crashes when loading a session that was killed mid-turn (e.g., OOM, kill -9). It cleans up orphaned tool_call messages in the `context.jsonl`.
    - **Status**: Open. Critical for resilience.

11. **#2382 – Fix(file): Convert Unsupported Image Formats to PNG**
    URL: `MoonshotAI/kimi-cli PR #2382`
    - **Fix**: The `ReadMediaFile` tool now converts `.ico` (and other unsupported formats) to `.png` before sending to the LLM API.
    - **Status**: Open. Resolves Issue #2017.

## 5. Feature Request Trends

The current issue dataset does not contain explicit feature requests. The community focus is entirely on **bug fixing** and **stability recovery**, particularly around authentication (403 errors) and UI/UX standards (auto-scroll, parity with VS Code).

## 6. Developer Pain Points

1.  **Frequent 403 Errors / Authentication Barriers**: The most critical pain point. Developers are unable to use the tool at all due to either backend enforcement of “Coding Agent” tiers or a broken token validation flow.

2.  **Session Instability**: Users are experiencing unexpected logouts and mid-task disconnections (#2430). This disrupts workflow continuity, especially for long-running tasks.

3.  **Performance Regressions**: Users are noticing a clear drop in speed moving from older versions to `v1.46.0`, particularly on `arm64` architectures and with the `k2.6` model (#2423).

4.  **Platform Inconsistency**: The CLI behaves differently from the VS Code extension. Missing slash commands (`/title`) and UI inconsistencies create friction for users switching between environments (#2428).

5.  **Backend Capacity Issues**: “Engine overloaded” messages (#2424) suggest that the backend serving the `k2.5` (and potentially other) models is either rate-limiting or struggling with load, impacting reliability.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-05

## Today’s Highlights
A **Memory Megathread** (#20695) continues to centralise heap snapshot collection, while a proposed **DeepSeek V4 Pro price reduction** (#28846) sparks debate around usage‑limit adjustments. Meanwhile, a burst of issues from user `LifetimeVip` uncovers critical gaps in **read‑before‑edit enforcement** and **compaction context loss**, signalling that the team is likely deep in a stability‑focused sprint.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues
1. **[Issue #20695 – Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)**  
   *90 comments · 63 👍* – Long‑running central thread collecting heap snapshots. The maintainers explicitly ask users **not to run LLM suggestions**, making this a rare hands‑on debugging collaboration.

2. **[Issue #28846 – Adjust Go usage limits after DeepSeek V4 Pro price reduction](https://github.com/anomalyco/opencode/issues/28846)**  
   *69 comments · 74 👍* – A popular feature request to pass on DeepSeek’s permanent 75% API price drop to OpenCode Go subscribers. High engagement suggests strong demand for provider‑aligned pricing.

3. **[Issue #27589 – TUI fails on Alpine Linux (musl)](https://github.com/anomalyco/opencode/issues/27589)**  
   *27 comments · 12 👍* – Regression in 1.14.50: `getcontext` symbol missing on musl‑based systems. Blocks Docker users and lightweight Linux deployments.

4. **[Issue #27530 – Error: 4 of 5 requests failed: config.providers: Unexpected server error](https://github.com/anomalyco/opencode/issues/27530)**  
   *26 comments · 16 👍* – App fails to start on some configurations. Root cause unclear but affects multiple provider setups.

5. **[Issue #590 – Local models (Ollama) cannot write files](https://github.com/anomalyco/opencode/issues/590)**  
   *18 comments · 1 👍* – Long‑standing open issue: tool calls produce JSON but files are never written. Particularly frustrating for local‑model users.

6. **[Issue #12789 – “The requested model is not supported”](https://github.com/anomalyco/opencode/issues/12789)**  
   *16 comments · 10 👍* – Claude models via Copilot fail while others work. Re‑authentication doesn’t help – likely a provider‑mapping bug.

7. **[Issue #20118 – Failed to run query ‘PRAGMA journal_mode = WAL’](https://github.com/anomalyco/opencode/issues/20118)**  
   *10 comments · 10 👍* – Downgrading OpenCode corrupts the SQLite schema. Better error handling requested.

8. **[Issue #1168 – Feature Request: Make Links Clickable](https://github.com/anomalyco/opencode/issues/1168)**  
   *6 comments · 91 👍* – Despite being open since mid‑2025, this remains the most upvoted piece of UX feedback. `Ctrl+click` to open URLs in the TUI.

9. **[Issue #17169 – Subagent infinite retry loop on tool failure](https://github.com/anomalyco/opencode/issues/17169)**  
   *4 comments · 0 👍* – A single failed `edit` call can cause $15+ in API costs before the loop is detected. Cost‑control alarm for heavy users.

10. **[Issue #30811 – Code quality degrades as conversations get longer](https://github.com/anomalyco/opencode/issues/30811)**  
    *6 comments · 0 👍* – User identifies five specific problems: compaction throws away context, no automatic verification after edits, over‑eager compression, missing sandbox checks, and lack of isolated error‑recovery. Touches the core of OpenCode’s long‑session strategy.

## Key PR Progress
1. **[PR #30836 – fix: finish errored compaction summaries](https://github.com/anomalyco/opencode/pull/30836)**  
   Ensures compaction summaries that fail are still marked as finished, preventing retry loops. Directly tackles part of #30834.

2. **[PR #30837 – fix: optimize first-time snapshot tracking & add UI clarity](https://github.com/anomalyco/opencode/pull/30837)**  
   Closes three issues (#3176, #18072, #30386) and partially addresses snapshot‑dir bloat. A significant UX and performance improvement.

3. **[PR #24962 – fix: apply agent variant when no explicit model is configured](https://github.com/anomalyco/opencode/pull/24962)**  
   Resolves #21632: subagent `variant` settings were parsed but ignored at runtime since v1.4.0.

4. **[PR #30789 – feat: persist v2 session context epochs](https://github.com/anomalyco/opencode/pull/30789)**  
   Stores immutable baseline + structured source snapshots per context epoch, improving session fidelity across restarts.

5. **[PR #30832 – feat: attach global native tools](https://github.com/anomalyco/opencode/pull/30832)**  
   Opens a public native API for embedding applications to define same‑process tools. Enables richer plugin ecosystems.

6. **[PR #30678 – feat: improve desktop multi-server support](https://github.com/anomalyco/opencode/pull/30678)**  
   Adds per‑server home screen focus, session filtering by project, and server‑isolated state – a major desktop UX upgrade.

7. **[PR #30824 – feat: color themes](https://github.com/anomalyco/opencode/pull/30824)**  
   Merged – introduces runtime v2 theme tokens and a static palette‑to‑token mapping. Brings theming parity to the TUI/desktop.

8. **[PR #30477 – feat: add “reasoning” as interleaved field option for vLLM](https://github.com/anomalyco/opencode/pull/30477)**  
   Allows `reasoning` alongside `reasoning_content`, unblocking newer vLLM‑served models that use different field names.

9. **[PR #30488 – feat: allow backgrounding synchronous subagents](https://github.com/anomalyco/opencode/pull/30488)**  
   Adds a `/experimental/session/:sessionID/background` endpoint and TUI hints (`ctrl+b`). Lets users detach long‑running subagents.

10. **[PR #7763 – fix: add persistent cost to prevent under-reporting](https://github.com/anomalyco/opencode/pull/7763)**  
    Long‑standing fix: session cost was only computed from the last 100 messages, causing under‑reporting in lengthy sessions.

## Feature Request Trends
- **Provider‑aware pricing** – #28846 (DeepSeek price pass‑through) and #30819 (Bedrock GPT‑5.x) show users want per‑provider rate adjustments.
- **Long‑session resilience** – #30811, #30805, and #30834 highlight demand for compaction that preserves context, avoids retry loops, and verifies edits.
- **Better local model support** – #590 (Ollama file writes), #21214 (vLLM breakage), and #12789 (Copilot model mapping) signal that self‑hosted and third‑party providers remain brittle.
- **Session management** – #18569 (resume by name), #16562 (disappearing sessions), #30347 (local timestamps) all ask for more robust, user‑friendly session handling.
- **Terminal integration** – #1168 (clickable links), #27749 (exit kills terminal), #28673 (regression on Windows) indicate the TUI still has rough edges compared to classic terminal workflows.

## Developer Pain Points
- **Memory & stability** – #20695 is still the top pain point; heap snapshots are hard to collect and memory consumption remains unpredictable.
- **Silent failures & retry loops** – #17169, #30834, and #30805 show that subagents and compaction can loop indefinitely, burning API credits.
- **Platform incompatibilities** – #27589 (musl), #27530 (server error), and #27749 (Windows terminal) frustrate users on non‑mainstream or newer OS versions.
- **Security gaps** – #30799 (prompt injection via `<system-reminder>`) and #30791 (no read‑before‑edit enforcement) are critical – code integrity and user data could be at risk.
- **Cost transparency** – #7763 and #28846 reflect a common desire for accurate cost tracking and fair provider pass‑through.
- **Regressions** – #21632 (variant parsing) and #28673 (Windows exit) show that new releases can break previously working features, highlighting a need for more comprehensive CI.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-05

## Today’s Highlights
Release v0.78.1 landed with expanded provider support (Ant Ling, NVIDIA NIM, MiniMax-M3) and richer extension context (`ctx.mode`, `ctx.getSystemPromptOptions()`). The community saw heavy discussion around an OpenAI Codex hang bug (#4945, 52 comments) and a new crash in `getSessionStats()` for Ollama models (#5386). Several PRs advanced remote execution, keybinding universalization, and provider aliasing.

## Releases
- **v0.78.1**  
  - Added built-in providers: **Ant Ling**, **NVIDIA NIM** (see [Providers](docs/providers.md))  
  - Added **MiniMax-M3** support for direct MiniMax providers  
  - Extended extension context with `ctx.mode` and `ctx.getSystemPromptOptions()`

## Hot Issues (10 noteworthy)

1. **#4945** – [openai-codex can hang on `Working...` with zero-usage aborted turns](https://github.com/earendil-works/pi/issues/4945)  
   *High engagement (52 comments, 27 👍). No streamed text, tool call, or error; only Escape recovers. Affects gpt-5.5.*

2. **#5323** – [Improve Vertex + GCP metadata server support](https://github.com/earendil-works/pi/issues/5323)  
   *Synchronous `existsSync` check fails on metadata-sourced credentials. Important for GCP users relying on default service accounts.*

3. **#5386** – [Crash in getSessionStats() when assistant message has no usage field (Ollama)](https://github.com/earendil-works/pi/issues/5386)  
   *`Cannot read properties of undefined (reading 'input')` – Ollama models missing token counts break session stats.*

4. **#5341** – [Port coding-agent to use ExecutionEnv + support for remote containers over SSH](https://github.com/earendil-works/pi/issues/5341)  
   *Feature request to route OS interactions to remote hosts. Noticed existing SSH extension, wants full remote session support.*

5. **#4643** – [Support OpenAI Codex Fast mode](https://github.com/earendil-works/pi/issues/4643)  
   *Request for a Pi-native toggle for Codex Fast mode, separate from thinking level. Popular among power users.*

6. **#5188** – [shift+enter submits and does not create new line](https://github.com/earendil-works/pi/issues/5188)  
   *Keybinding bug: `shift+enter` not mapped to new line despite config. `ctrl+j` works but `shift+enter` doesn’t.*

7. **#5373** – [High idle CPU and syscall rate on large sessions](https://github.com/earendil-works/pi/issues/5373)  
   *~24% CPU idle on 150k+ token sessions. strace shows heavy `read` syscalls – performance regression.*

8. **#5363** – [Add amazon-bedrock-mantle provider for OpenAI-compatible models](https://github.com/earendil-works/pi/issues/5363)  
   *Bedrock Mantle uses OpenAI-compatible API, not Converse. New provider needed.*

9. **#5331** – [options.maxTokens maps to wrong API parameter for opencode-go provider](https://github.com/earendil-works/pi/issues/5331)  
   *`max_completion_tokens` sent instead of `max_tokens`, silently ignored by backend.*

10. **#4728** – [Mouse support in TUI (clicks, scroll, hover)](https://github.com/earendil-works/pi/issues/4728)  
    *Long-standing request for pointer interaction. Extensions cannot implement due to core blockers.*

## Key PR Progress (10 important)

1. **#5262** – [feat(ai): add Anthropic Vertex provider](https://github.com/earendil-works/pi/pull/5262) – *Open. Thin adapter for Claude on GCP Vertex AI, reuses existing Anthropic streaming path.*

2. **#5281** – [feat(coding-agent): Support keybindings for all commands](https://github.com/earendil-works/pi/pull/5281) – *Merged. Unifies built-in and extension command keybinding via `cmd.<name>` convention.*

3. **#5412** – [fix(coding-agent): alias firepass model references](https://github.com/earendil-works/pi/pull/5412) – *Merged. Normalizes `firepass/…` to `fireworks/…` for model resolution.*

4. **#5385** – [feat(coding-agent): detect first-run terminal theme](https://github.com/earendil-works/pi/pull/5385) – *Open. Queries terminal via OSC to set light/dark theme on first launch.*

5. **#5379** – [Store user scoped local package installs as absolute paths](https://github.com/earendil-works/pi/pull/5379) – *Merged. Closes #5378; uses absolute paths for user-level local packages to avoid relative path issues.*

6. **#5410** – [fix: persist restored session model as default for new sessions](https://github.com/earendil-works/pi/pull/5410) – *Merged. Updates `defaultModel`/`defaultProvider` when continuing a session.*

7. **#5332** – [feat(config): Approval system for workspaces](https://github.com/earendil-works/pi/pull/5332) – *Open. Adds `.pi.user` folder and interactive approval for workspace configurations.*

8. **#5400** – [fix(ai): map maxTokens to max_tokens for opencode providers](https://github.com/earendil-works/pi/pull/5400) – *Merged. Fixes #5331 by correcting the API parameter for opencode providers.*

9. **#5399** – [fix(extensions): surface deferred-extension commands in autocomplete](https://github.com/earendil-works/pi/pull/5399) – *Merged. Updates autocomplete dynamically so deferred extension commands appear.*

10. **#5397** – [fix: Alt+Delete word deletion on Mac OS](https://github.com/earendil-works/pi/pull/5397) – *Merged. Adds expected word-delete behavior (Alt+Delete) on macOS.*

## Feature Request Trends
- **Provider expansion** – Multiple requests for new cloud-specific providers (Anthropic Vertex, Bedrock Mantle, Fireworks aliasing, OpenRouter routing fixes). Users want first-class support for non‑OpenAI APIs.
- **Remote execution** – SSH/MCP remote container support (#5341, #5350) and ExecutionEnv generalization are gaining traction.
- **TUI interactivity** – Mouse support (#4728), altbuf rendering mode (#5357), and customizable working loader (#5411) reflect desire for richer terminal UX.
- **Extension API polish** – Public command execution (#5367), deferred extension command surfacing (#5399), and tool operation customization (#5354, #5364) show extension‑driven workflows.
- **Session tree management** – Branch deletion (#5366) and model persistence (#5410) indicate users want more control over session state.

## Developer Pain Points
- **Hangs and crashes**: openai-codex hang (#4945) and `getSessionStats()` crash (#5386) are top frustrations, especially with Ollama and large sessions.
- **Provider integration quirks**: Wrong `maxTokens` parameter for opencode (#5331), `developer` role rejection for DeepSeek via proxy (#5384), and Fireworks JSON Schema errors (#5352).
- **Performance degradation**: High idle CPU on large sessions (#5373) impacts daily workflow.
- **Configuration surprises**: `settings.json` being rewritten on provider switch (#5355), relative path resolution breaking Windows‑to‑Linux remote file ops (#5350).
- **Installation and update annoyances**: `pi-fancy-loader` always shows as updatable (#5388), Bun installation still uses Node runtime (#5365).
- **Keybinding and input issues**: `shift+enter` not respecting config (#5188), phantom follow‑up prompts (#5368), Alt+Delete not working on Mac (#5397).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-06-05

A quiet but meaningful day in the Qwen Code repo: a nightly patch shipped, a flurry of triage-process PRs landed, and several long-running features — ACP parity, cross-session stats, memory scoping — reached observable progress milestones. Community energy is concentrated on **model-switching UX**, **memory persistence models**, and **headless-Linux compatibility**.

---

## Today’s Highlights

- **v0.17.1-nightly** released with a single fix: `/copy` no longer includes thinking blocks in clipboard output.  
- **ACP / REST parity** work continues with a 24-method extension wave (#4736) and a child-lifecycle optimization PR (#4751).  
- Two highly-requested features — **cross-session `/stats`** (#4779) and **user-level auto-memory** (#4764) — both received implementation PRs today.  
- The community flagged a concerning regression: background auto-update can replace code chunks mid-session, breaking auth-type-based model switching (#4758).

---

## Releases

- **[v0.17.1-nightly.20260605.715266537](https://github.com/QwenLM/qwen-code/releases/tag/v0.17.1-nightly.20260605.715266537)**  
  - **Fix**: `/copy` no longer captures internal reasoning/thinking blocks; only visible assistant output is copied to clipboard.  
  - No other changes in this nightly.

---

## Hot Issues (10 picks)

1. **[#4758 – Background auto-update replaces chunks mid-session, breaking cross-authType model switching](https://github.com/QwenLM/qwen-code/issues/4758)** (Bug, CLI)  
   A critical regression: switching providers via `/model` (e.g., `anthropic` → `openai`) can fail with “Cannot find module” after an auto-update replaces chunks mid-session. No comments yet, but high impact.

2. **[#4754 – `/model` should not persist to settings by default](https://github.com/QwenLM/qwen-code/issues/4754)** (Feature, CLI, **closed**)  
   Community member `zzhenyao` argues that `/model` should be session-scoped only. The current behavior writes to `settings.json`, which may surprise users. 5 comments, merged as a fix.

3. **[#4722 – Statusline shows model id instead of human-readable name](https://github.com/QwenLM/qwen-code/issues/4722)** (Bug, UI, **closed**)  
   Also filed by `zzhenyao`. The status bar displays raw model IDs (e.g., `qwen3-coder-plus`) rather than display names. Same PR likely fixed this. 5 comments.

4. **[#4747 – Feature: Support global user-level auto-memory at ~/.qwen/memories/](https://github.com/QwenLM/qwen-code/issues/4747)** (Feature, Memory)  
   User `nblog` requests cross-project memory (like Claude’s “user memory”). Currently memories are isolated per project. An implementation PR (#4764) was opened the same day — fast turnaround.

5. **[#4597 – Enhance `/stats` with cross-session usage tracking](https://github.com/QwenLM/qwen-code/issues/4597)** (Feature, Telemetry)  
   `BenGuanRan` proposes persistent usage history, an interactive dashboard, and trend analysis. The PR #4779 landed today. 4 comments, 👍1.

6. **[#4777 – Deferred-tools listing in system prompt busts prompt cache on every MCP discovery](https://github.com/QwenLM/qwen-code/issues/4777)** (Bug, Performance)  
   `qqqys` identifies a subtle but impactful prompt-cache invalidation: deferred MCP tools are embedded in the cached system prompt, so any discovery call forces a re-encode. A fix PR (#4781) opened same day.

7. **[#4584 – Auto mode startup text: remove emoji and simplify copy](https://github.com/QwenLM/qwen-code/issues/4584)** (Enhancement, UI)  
   `qqqys` requests removing the redundant emoji from auto-mode startup. 👍1, 1 comment — small but widely felt UX nit.

8. **[#4723 – Does Qwen Code support Rules or Instructions now?](https://github.com/QwenLM/qwen-code/issues/4723)** (Question)  
   `niheaven` asks about rule/instruction systems like Claude Code or Copilot. 5 comments — community is clearly looking for first-class rule support, not just skills/hooks.

9. **[#4782 – ACP Streamable HTTP transport implementation status](https://github.com/QwenLM/qwen-code/issues/4782)** (Feature, Daemon)  
   `chiga0` tracks the Qwen-Code Daemon’s ACP compliance. This is a developer-facing infra feature enabling native connections from Zed, Goose, JetBrains. Important for ecosystem integration.

10. **[#4419 – Standardize file naming to kebab-case with ESLint enforcement](https://github.com/QwenLM/qwen-code/issues/4419)** (Enhancement, Dev Experience)  
    `pomelo-nwu` proposes enforcing kebab-case across core and CLI packages, with automated linting and docs. Low priority but high codebase health impact.

---

## Key PR Progress (10 picks)

1. **[#4736 – ACP/REST parity wave 1: 24 extension methods](https://github.com/QwenLM/qwen-code/pull/4736)**  
   Adds session extensions, memory, file operations, and auth endpoints to the ACP dispatch. Depends on #4563. This is the most substantial new capability PR of the day.

2. **[#4751 – Optimize ACP child lifecycle: skip relaunch, preheat, idle keep-alive](https://github.com/QwenLM/qwen-code/pull/4751)**  
   Eliminates redundant grandchild spawns and adds pre-spawning for ACP children. Significant performance improvement for daemon-mode.

3. **[#4781 – Keep deferred-tools listing out of cached system prompt](https://github.com/QwenLM/qwen-code/pull/4781)**  
   Moves MCP tool listing to a per-turn `<system-reminder>` injection. Directly addresses prompt-cache busting (#4777).

4. **[#4780 – Add `/fork` background-agent command](https://github.com/QwenLM/qwen-code/pull/4780)**  
   Implements a non-blocking fork that spawns an agent in the background, inheriting full context. Responds to long-standing user requests for parallel agent workflows.

5. **[#4779 – Interactive `/stats` dashboard with cross-session tracking](https://github.com/QwenLM/qwen-code/pull/4779)**  
   Three-tab dashboard: Session (live), Activity (trends), Efficiency (performance). Addresses #4597. Major UX improvement.

6. **[#4764 – Add user-level auto-memory at ~/.qwen/memories/](https://github.com/QwenLM/qwen-code/pull/4764)**  
   Mirrors Claude’s private/team scoping. Reuses existing 4-type taxonomy. Addresses #4747. Fast implementation from PR to open in one day.

7. **[#4677 – Fix vim mode Esc leak, Enter submit, render lag, missing VIM commands](https://github.com/QwenLM/qwen-code/pull/4677)**  
   Comprehensive vim mode fix: prevents Esc from triggering AppContainer’s handler, fixes Enter submission, improves render performance, adds missing NORMAL commands. High user-impact PR.

8. **[#4755 – Prevent selection dialog flicker](https://github.com/QwenLM/qwen-code/pull/4755)**  
   Constrains interactive dialogs within visible terminal frame. Fixes a subtle but annoying visual glitch in CLI.

9. **[#4572 – Harden auto mode self-modification checks](https://github.com/QwenLM/qwen-code/pull/4572)**  
   Prevents auto-mode from bypassing classifier for writes to config, instructions, hooks, MCP config. Also splits classifier permits into granular rules. Security-focused refactor.

10. **[#4766 – Preserve non-ASCII git paths in file crawler](https://github.com/QwenLM/qwen-code/pull/4766)**  
    Fixes Git path quoting so non-ASCII tracked filenames are returned as UTF-8. Adds regression tests. Important for international users.

---

## Feature Request Trends

- **Persistent Usage Stats & Dashboards** – The `/stats` enhancement (#4597) and its implementation (#4779) show strong demand for session-to-session tracking, trend analysis, and dashboard UIs beyond current ephemeral metrics.
- **Memory Scoping & Rules** – Multiple requests for cross-project user memory (#4747, #4764) and a generic “Rules” system (#4723) indicate the community wants Qwen Code to learn once and remember across projects, similar to Claude Code.
- **Background / Fork Agents** – The `/fork` PR (#4780) and related feature requests (#4757) reflect a desire for non-blocking parallel agents that can work on sub-tasks while the main conversation continues.
- **ACP / REST API Parity** – With #4736, #4782, and #4490, the daemon-mode ACP compliance is clearly a major internal focus. The ecosystem benefit (Zed, Goose, JetBrains native integration) is a strong motivator.
- **Local Diagnostics Framework** – #4421 (ring buffer + diagnostic bundle) signals growing interest in local-first, user-controlled debugging without telemetry.

---

## Developer Pain Points

- **Model Switching UX** – Issues #4722 (raw ID in statusline), #4754 (unwanted persistence), and #4758 (chunk replacement breaking auth-type) show that model-switching remains a fragile and confusing area.
- **npm Root Permissions** – #4627 and #4643 highlight that auto-update still fails for users who installed with `sudo npm install -g`. The fix (#4643) adds a fallback to standalone binary, but the underlying EACCES experience is clearly frustrating.
- **Headless / Container Environments** – #4712 (xdg-open crash) and #4716 (fix PR) confirm that Qwen Code’s browser-opening commands still break on headless Linux. The community is actively working on a fix.
- **Auto-Update Unpredictability** – #4758 is a serious regression where auto-update replaces chunks mid-session, breaking model switching. This creates a trust issue: users cannot rely on auto-update as a safe, background process.
- **Vim Mode Quality** – #4677 touches multiple vim mode bugs (Esc leak, Enter submission, render lag). The fact that a single PR addresses 4+ distinct bugs suggests the feature has accumulated technical debt.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-06-05

## Today’s Highlights
- The `v0.9.0` stabilization gate issue (#2721) is now live, consolidating Windows, large-repo, subagent, and live-state blockers into a single release-blocking lane – critical for the upcoming feature release.
- A major provider-switch lockout bug (#2754) – where switching to Kimi K2.6 causes an unrecoverable auth failure – has been addressed by PR #2755, which rolls back the provider upon authentication failure.
- The long-standing clipboard copy failure on non-wlroots Wayland compositors (niri) (#1920) remains open; the issue has garnered 4 comments but no fix yet, affecting a niche but vocal group of Wayland users.

## Releases
No new releases in the last 24 hours. The latest stable version remains v0.8.53 (as of 2026-06-04).

## Hot Issues (Top 10 Noteworthy)

1. **#1920 – Clipboard copy silently fails on non-wlroots Wayland (niri)**  
   *Why it matters*: Affects copy/paste workflow on popular Wayland compositors like niri. Community has suggested workarounds but no fix committed.  
   👥 4 comments | [Issue](https://github.com/Hmbown/CodeWhale/issues/1920)

2. **#2739 – Task execution freezes indefinitely, connection timeout on cancel**  
   *Why it matters*: A regression that makes long-running tasks unusable. User reports losing session context after force-quitting. v0.8.52’s “300s auto-cancel” fix apparently insufficient.  
   👥 2 comments | [Issue](https://github.com/Hmbown/CodeWhale/issues/2739)

3. **#2758 – `codewhale sessions` footer shows wrong resume command**  
   *Why it matters*: Confuses users by suggesting `--resume` which is not a valid top-level flag. An easy documentation/UX fix that has been reported.  
   👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2758)

4. **#2721 – v0.9.0 Stabilization gate: Windows, large-repo, subagent, live-state blockers**  
   *Why it matters*: The project’s lead (@Hmbown) is triaging all blockers before the feature release. Essential for release quality.  
   👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2721)

5. **#2754 – Switching to Kimi K2.6 locks IDE, cannot switch back to DeepSeek**  
   *Why it matters*: Critical UX bug – once broken, the entire IDE is unusable. PR #2755 is already in review.  
   👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2754)

6. **#2744 – MCP tool name parsing breaks when server name contains underscores**  
   *Why it matters*: Underscore in MCP server names (e.g., `my_db`) causes misrouting. Affects users with custom MCP configurations.  
   👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2744)

7. **#2641 – `read_file` on PDF without `pages` parameter hangs and closes channel**  
   *Why it matters*: A seemingly simple PDF extraction crashes the tool. Only works when pages are explicitly specified.  
   👥 2 comments | [Issue](https://github.com/Hmbown/CodeWhale/issues/2641)

8. **#2648 – Deferred tool hydration renders as completed run**  
   *Why it matters*: Misleading UI – a tool that was never executed appears as “run done.” Confuses users during multi-step tasks.  
   👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2648)

9. **#2735 – MiMo endpoint configuration error**  
   *Why it matters*: Xiaomi MiMo provider integration has incorrect endpoint URLs, breaking API calls. Open PR #2627 attempts to fix it.  
   👥 2 comments | [Issue](https://github.com/Hmbown/CodeWhale/issues/2735)

10. **#2666 – Telemetry: agents need visible token/resource usage during long tasks**  
    *Why it matters*: Agents lack visibility into token budget and context pressure, leading to wasted runs. A notable quality-of-life request from power users.  
    👥 1 comment | [Issue](https://github.com/Hmbown/CodeWhale/issues/2666)

## Key PR Progress (Top 10 Important PRs)

1. **#2762 – v0.9.0 stewardship integration** (OPEN)  
   *Summary*: Integration branch for all v0.9.0 stabilization work. No release artifacts, just PR check surface.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2762)

2. **#2755 – Roll back provider after auth failure** (OPEN)  
   *Summary*: Fixes #2754 by keeping a pending provider-switch snapshot and restoring previous provider on auth failure.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2755)

3. **#2751 – Merge workspace MCP config** (OPEN)  
   *Summary*: Merges `.codewhale/mcp.json` with global config, workspace overrides same-name entries. Addresses #2749.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2751)

4. **#2763 – Refresh branch status after shell changes** (CLOSED)  
   *Summary*: Fixes stale workspace branch display after shell tool completions.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2763)

5. **#2764 – Gate shell child kill helper off Windows** (CLOSED)  
   *Summary*: Fixes Windows CI compilation warning by conditionally compiling `ShellChild::kill`.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2764)

6. **#2745 – LLM-powered codebase analysis for AGENTS.md generation** (CLOSED)  
   *Summary*: Replaces template-based `/init` with deep analysis that generates custom AGENTS.md. Likely to become the default onboarding flow.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2745)

7. **#2753 – Multi-tab system with cross-tab collaboration** (OPEN)  
   *Summary*: Adds `TabManager`, cross-tab task delegation, and persistency. A large feature PR with potential UI complexity.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2753)

8. **#2627 – Support Xiaomi MiMo Token Plan mode** (OPEN)  
   *Summary*: Adds provider mode with cluster aliases. Addresses #2735 and #2621.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2627)

9. **#2687 – Mode-agnostic system prompt** (OPEN)  
   *Summary*: Strips mode instructions and approval policies from base system prompt, delivering them as append-only messages. Cleaner architecture.  
   [PR](https://github.com/Hmbown/CodeWhale/pull/2687)

10. **#2636 – Cache project-context by mtime signature** (CLOSED)  
    *Summary*: Performance improvement – avoids repeated filesystem walks by caching per-file mtime signatures.  
    [PR](https://github.com/Hmbown/CodeWhale/pull/2636)

## Feature Request Trends
- **Provider flexibility**: Strong demand for fallback chains (#2581), support for Xiaomi MiMo token plans (#2627), and adapting Claude Code skill ecosystem (#2743).
- **Workflow / pipeline support**: Multiple issues request run trace exports (#2752), multi-tab collaboration (#2753), and Model Lab/WhaleFlow integrations – all pointing toward a more sophisticated orchestration layer.
- **Better MCP / tooling integration**: Auto-merge of project-level MCP configs (#2749), consistent MCP name parsing (#2744), and workspace MCP merging (#2751) reflect growing reliance on MCP-based tools.
- **Telemetry & visibility**: Agents need real-time token/resource usage (#2666) and deferred tool hydration transparency (#2648) – a clear call for better observability.

## Developer Pain Points
- **Stability regressions**: Tasks freezing (#2739) and provider lockouts (#2754) are high-frequency complaints, especially after recent version bumps. Users express frustration with lost sessions.
- **CLI UX inconsistencies**: Wrong resume command in sessions footer (#2758) and PDF extraction hangs (#2641) degrade the experience for newcomers and power users alike.
- **Cross-platform gaps**: Clipboards failing on non-wlroots Wayland (#1920) and Windows shell process handling (#2498, #2708) show that Linux and Windows users still face platform-specific friction. HarmonyOS port (#2634) is being explored but has low adoption.
- **Configuration fragility**: Underscore in MCP server names (#2744) and provider endpoint errors (#2735) indicate that configuration parsing and validation need hardening.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*