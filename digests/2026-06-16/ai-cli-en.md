# AI CLI Tools Community Digest 2026-06-16

> Generated: 2026-06-16 02:59 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report – 2026-06-16

## 1. Ecosystem Overview

The AI CLI developer tools landscape remains highly active, with six of the nine major tools shipping a release in the last 24 hours. Community engagement is strong across all projects, with hundreds of issues and pull requests updated daily. The dominant themes cutting across tools are persistent memory/shared context, multi-model flexibility, MCP (Model Context Protocol) integration, cross-platform stability (especially Windows and ARM), and agent reliability. Meanwhile, developer pain points consistently cluster around false-positive safety filters, post-sleep session loss, memory/resource consumption, and silent failures that erode trust in autonomous workflows.

## 2. Activity Comparison

| Tool | Key Issues (hot/top) | Key PRs (last 24h) | Release (last 24h) |
|------|----------------------|--------------------|--------------------|
| **Claude Code** | ~10 (hot) | 10 | v2.1.178 |
| **OpenAI Codex** | ~10 (hot) | 10 | v0.140.0 |
| **Gemini CLI** | 50 updated | 10 | None |
| **GitHub Copilot CLI** | ~10 (hot) | 1 (spam) | v1.0.63 & v1.0.63-0 |
| **Kimi Code CLI** | 4 | 2 | None |
| **OpenCode** | ~10 (hot) | 10 | None |
| **Pi** | ~10 (hot) | 10 | v0.79.4 |
| **Qwen Code** | ~10 (hot) | 10 | v0.18.1 & desktop-v0.0.4 |
| **DeepSeek TUI** | ~10 (hot) | 10 | None |

**Note:** Issue and PR counts are based on highlighted items in each digest, not total repository activity. Gemini CLI reported the highest raw issue churn (50 updated). Claude Code, OpenAI Codex, OpenCode, Pi, Qwen Code, and DeepSeek TUI all had 10+ significant PRs in the last day.

## 3. Shared Feature Directions

Several product requirements appear across **three or more** tool communities:

- **Persistent / shared memory & context.** Claude Code (#47023, #38536), OpenCode (session goals #27167), Gemini CLI (Auto Memory hardening #26522–26525), and Pi (session sorting #5784) all have open issues demanding hooks, archival, or team-wide memory. Users want context to survive sessions and be shareable across a team.

- **Multi-model & BYOK flexibility.** Claude Code (#68165 per-message model selection), GitHub Copilot CLI (#3282 multiple BYOK models), Qwen Code (#5173 provider disambiguation), and Pi (#5728 provider-specific config) all request the ability to switch models or bring custom endpoints within a single session.

- **MCP protocol alignment & reliability.** OpenCode (#28567 MCP client capabilities), Claude Code (#64366 MCP fan-out crash), GitHub Copilot CLI (#3756 MCP policy), Pi (#5687 MCP blocking commands), Qwen Code (#4966 MCP schema validation), and DeepSeek TUI (provider registry #3192) all highlight MCP integration as a top priority.

- **Cross-platform stability (Windows, Linux, ARM).** Every tool has at least one open issue for Windows-specific bugs (path handling, terminal input, encoding). Claude Code (#12953 mousewheel), OpenAI Codex (#12661 links, #28094 WSL), Gemini CLI (#27615 keyboard), GitHub Copilot CLI (#3776 UTF-8), Kimi Code (#2455 proxy), OpenCode (#30869 encoding), Pi (#5103 git-bash), Qwen Code (#5159 trackpad), DeepSeek TUI (#1812 freeze) – cross-platform parity remains the single largest surface of developer friction.

- **Agent reliability & safety controls.** Claude Code (Tool permission matching), OpenAI Codex (multi_agent_v2 #27331), GitHub Copilot CLI (agent permissions #953), Gemini CLI (agent hangs #21409, subagent misreporting #22323), OpenCode (sandboxing #2242), DeepSeek TUI (sub-agent reliability #1806) – every community reports agents that fail silently, hang indefinitely, or bypass intended restrictions.

## 4. Differentiation Analysis

| Tool | Feature Focus | Target User | Technical Approach |
|------|---------------|-------------|-------------------|
| **Claude Code** | Anthropic ecosystem hooks, MCP permission matching, compact memory | Claude power users, skill developers | Plugin/hook architecture with parameter-based tool rules |
| **OpenAI Codex** | Cross-IDE integration, safety filters, VS Code extension | Multi-platform developers, enterprise | Desktop app + CLI with Guardian safety layer |
| **Gemini CLI** | Agent orchestration, sub-agents, AST-aware tools | Google Cloud / Gemini users | Modular agent architecture with behavioral evals |
| **GitHub Copilot CLI** | Enterprise policy, MCP server management, BYOK | GitHub Enterprise customers | Policy-first design, deferred tools, `/diff` |
| **Kimi Code CLI** | Minimalist shell integration, hook extensibility | MoonshotAI users, scripters | Lightweight hooks, session resume |
| **OpenCode** | Open-source, MCP spec alignment, plugin ecosystem | Community power users, plugin authors | Plugin system with PR identity, lazy loading |
| **Pi** | Lightweight TUI, provider-agnostic, extension API | Multi-provider users, AWS/Bedrock fans | Small core with registered provider registry |
| **Qwen Code** | `/loop` automation, Qwen model optimization, daemon mode | Qwen model users, async automation | Daemon session shell, workflow phases |
| **DeepSeek TUI** | Minimalist terminal, provider-agnostic, persistent permissions | Terminal purists, security-conscious | Rust TUI with i18n, skill scoping |

**Key differentiators:** Claude Code leads in permission granularity (tool parameter matching). OpenAI Codex invests most in safety assurance (Guardian). Gemini CLI is the only tool actively exploring AST-aware code intelligence. GitHub Copilot CLI is the only tool with explicit enterprise policy management. OpenCode and Pi have the strongest plugin/extension ecosystems. Qwen Code differentiates with daemon background automation and `/loop`. DeepSeek TUI stands out for its minimalist philosophy and persistent typed permission rules.

## 5. Community Momentum & Maturity

- **Highest momentum (rapid iteration, frequent releases):** **Claude Code**, **OpenAI Codex**, **Qwen Code**, and **Pi** all shipped releases within the last 24 hours. Claude Code had the most substantive new feature (tool parameter matching). OpenAI Codex introduced `/usage` dashboards. Qwen Code pushed both CLI and desktop updates. Pi added first-run theme detection.
- **Highest community engagement (issue volume, reaction counts):** **OpenAI Codex** (583 👍 for Linux desktop app), **Claude Code** (163 👍 for VS Code auto-attach toggle), and **OpenCode** (84 👍 for `/goal`) have the most‑upvoted feature requests. Gemini CLI saw 50 issues updated in one day, indicating high churn but lower per‑issue engagement.
- **Maturing but slower cadence:** **GitHub Copilot CLI** and **DeepSeek TUI** continue to evolve but with fewer releases and lower issue volume. **Kimi Code CLI** remains small but has active bug‑fix PRs.
- **Indicators of fragility:** Claude Code’s ENOSPC false positives, OpenAI Codex’s syspolicyd CPU spikes, and Gemini CLI’s agent hangs are generating the most repeated duplicate reports, suggesting systemic regressions that have not yet been fully addressed.

## 6. Trend Signals

Five industry‑level signals emerge from the aggregated community data:

1. **Memory as a first‑class primitive.** The push for persistent, shared, and hook‑intercepted memory (Claude Code, OpenCode, Gemini CLI, Pi) indicates that transient sessions are no longer acceptable for serious development workflows. Expect native memory APIs to become a standard feature across CLI tools within the next 6–12 months.

2. **Multi‑provider BYOK becomes table‑stakes.** With users demanding the ability to run Claude, OpenAI, Gemini, or custom models in the same session, tools that do not support dynamic model switching and provider fallback will lose adoption. This is a direct response to cost‑sensitivity and provider reliability concerns.

3. **MCP is the new plugin standard.** Every major tool either supports MCP or is actively integrating it. The community is coalescing around MCP for server‑side tooling, but implementations still vary wildly (fan‑out crashes, schema mismatches, policy gaps). Standardization efforts are likely in 2026 H2.

4. **Safety filters are a double‑edged sword.** False‑positive disruptions (OpenAI Codex blocking tax filing, Claude Code’s ENOSPC false positive) are generating more user frustration than security breaches. The industry needs configurable sensitivity, per‑task allowlists, and transparent audit trails – not just opaque blocking.

5. **Windows and ARM parity remains the #1 adoption blocker.** All nine tools have open Windows‑specific bugs, and several (OpenAI Codex, DeepSeek TUI) also have ARM64 or Linux compatibility gaps. Developers with heterogeneous setups or Windows‑based CI systems are disproportionately impacted, limiting the addressable market for these tools.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills | 2026-06-16

---

## 1. Top Skills Ranking

**1. Add document-typography skill** — #514 (Open)
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — issues that affect every document Claude produces.
- **Discussion:** The PR's summary resonates broadly ("Users rarely ask for good typography"). Discussion orbits around where to draw the line between helpful formatting and overreach.
- **Link:** https://github.com/anthropics/skills/pull/514

**2. Add ODT skill** — #486 (Open)
- **Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on any mention of LibreOffice or ISO-standard document formats.
- **Discussion:** The ISO-standard angle attracts enterprise users who need Office-agnostic document pipelines. Volume of attention reflects a significant underserved format gap.
- **Link:** https://github.com/anthropics/skills/pull/486

**3. Improve frontend-design skill clarity and actionability** — #210 (Open)
- **Functionality:** Rewrites the existing `frontend-design` skill so every instruction is executable within a single conversation, eliminating vague or aspirational guidance.
- **Discussion:** The revisionist approach — improving an existing skill rather than adding a new one — generated debate about skill maintenance lifecycle and quality thresholds.
- **Link:** https://github.com/anthropics/skills/pull/210

**4. skill-quality-analyzer + skill-security-analyzer** — #83 (Open)
- **Functionality:** Two meta-skills. The quality analyzer evaluates Skills across Structure, Documentation, Examples, Clarity, and Resource usage (20% each). The security analyzer audits prompt injection risks and privilege escalation vectors.
- **Discussion:** Meta-skills (skills that evaluate other skills) attracted sustained interest as a potential quality gate for the marketplace.
- **Link:** https://github.com/anthropics/skills/pull/83

**5. Add SAP-RPT-1-OSS predictor skill** — #181 (Open)
- **Functionality:** Wraps SAP's open-source tabular foundation model (Apache 2.0, released at TechEd 2025) for predictive analytics on SAP business data.
- **Discussion:** Enterprise AI practitioners see this as a bridge between Claude's general reasoning and SAP's domain-specific forecasting. Interest is steady but niche.
- **Link:** https://github.com/anthropics/skills/pull/181

**6. Add testing-patterns skill** — #723 (Open)
- **Functionality:** Comprehensive coverage of the Testing Trophy model, AAA unit tests, React Testing Library patterns, and guidance on what to test vs. what not to test.
- **Discussion:** Developers consistently request testing-related Skills. This PR consolidates a fragmented conversation across multiple Issues into a concrete submission.
- **Link:** https://github.com/anthropics/skills/pull/723

**7. Add shodh-memory skill (persistent context)** — #154 (Open)
- **Functionality:** Persistent memory system that maintains context across conversations using a `proactive_context` tool. Structured memories include metadata, importance scores, and cross-references.
- **Discussion:** Long-running agent conversations are a recurring pain point. This skill's approach to memory surfaced debate about context window management and tool-calling overhead.
- **Link:** https://github.com/anthropics/skills/pull/154

**8. Add AURELION skill suite** — #444 (Open)
- **Functionality:** Four skills (kernel, advisor, agent, memory) implementing a structured 5-floor cognitive framework for professional knowledge management and AI collaboration.
- **Discussion:** The sustainability of multi-skill suites vs. single-purpose Skills generated the most architectural debate in this cohort.
- **Link:** https://github.com/anthropics/skills/pull/444

---

## 2. Community Demand Trends

The Issues board reveals five concentrated demand vectors:

| Demand Vector | Signal Issues | Implication |
|---|---|---|
| **Org-wide skill sharing** | #228 (14 comments, 7 👍) | Enterprise teams cannot operationalize Skills without distribution mechanism. Top-voted feature request. |
| **Reliable evaluation infrastructure** | #556 (12 comments, 7 👍), #1169, #1061 | `run_eval.py` reports 0% recall for all queries — the optimization loop is optimizing against noise. Multiple independent reproductions. |
| **Security & trust boundaries** | #492 (community Skills under `anthropic/` namespace), #1175 (SPO permissions in SKILL.md) | Growing awareness that Skills inherit Claude's trust level. Two distinct threat models identified. |
| **Windows compatibility** | #1061 (3 issues, multiple PRs) | The skill-creator toolchain (subprocess, encoding, pipe select) is Unix-only. Repeated Windows-blocked contributions. |
| **Skill quality governance** | #202 (skill-creator reads like docs), #189 (plugin duplicates) | Community wants a quality standard for Skills themselves, not just what Skills teach Claude to produce. |

**Most-anticipated new Skill directions** (from Issues and cross-referencing PRs):
- **Agent governance & safety** (#412 — 6 comments) — policy enforcement, threat detection, audit trails for multi-agent systems
- **SharePoint Online integration** (#1175) — access-control logic embedded in SKILL.md for enterprise document pipelines
- **MCP-exposed Skills** (#16) — packaging Skills as MCP tools for broader toolchain interoperability
- **Multi-file reference bundling** (#1220) — inline preload of `SKILL.md` support files to avoid invocation-time gaps

---

## 3. High-Potential Pending Skills

These PRs have sustained comment activity and address widely-reported pain points. They are likely to merge in the near term:

- **fix(pdf): correct case-sensitive file references** — #538 (Open, updated 2026-04-29)
  Fixes 8 case-sensitive path mismatches that break on Linux. Small change, high impact.
  https://github.com/anthropics/skills/pull/538

- **fix(skill-creator): warn on unquoted YAML with special characters** — #539 (Open, updated 2026-04-16)
  Pre-parse validation catches silent description truncation. Directly enables correct skill evaluation.
  https://github.com/anthropics/skills/pull/539

- **fix(docx): prevent tracked change w:id collision** — #541 (Open, updated 2026-04-16)
  Root-cause fix for document corruption when DOCX skills interact with existing bookmarks. OOXML shared ID space.
  https://github.com/anthropics/skills/pull/541

- **skill-creator: fix Windows subprocess + encoding bugs** — #1050 (Open, updated 2026-05-24)
  Two one-line fixes (PATHEXT lookup for `claude.cmd`, cp1252 encoding) that unblock Windows users.
  https://github.com/anthropics/skills/pull/1050

- **feat: implement agent-creator skill** — #1140 (Open, updated 2026-06-02)
  Meta-skill for task-specific agent sets, plus Windows support for `recalc.py`. Addresses Issue #1120.
  https://github.com/anthropics/skills/pull/1140

- **fix(skill-creator): run_eval.py always reports 0% recall** — #1298 (Open, updated 2026-06-11)
  Comprehensive fix for the evaluator: installs the eval artifact as a real skill, fixes stream reading, trigger detection, and parallel workers. Addresses the #556 bug cluster.
  https://github.com/anthropics/skills/pull/1298

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable, shareable document generation Skills** (typography, ODT, DOCX integrity) paired with a **functional skill-development toolchain** (run_eval recall fix, YAML validation, Windows support) — the ecosystem cannot scale adoption until the measurement infrastructure is trustworthy and the output quality is professional-grade.

---

# Claude Code Community Digest – 2026-06-16

## Today's Highlights

Version **2.1.178** lands with a powerful new `Tool(param:value)` permission syntax, enabling parameter‑based tool matching. A wave of bug‑fix PRs has landed from community contributor AZERDSQ131, addressing ENOSPC false positives, MCP step‑up auth handling, and several Windows compatibility issues. Meanwhile, the community continues to push for persistent memory hooks and per‑message model selection.

## Releases

### [v2.1.178](https://github.com/anthropics/claude-code/releases/tag/v2.1.178)
- **Tool parameter matching** – Permission rules can now filter on tool input parameters using `Tool(param:value)` syntax, with `*` wildcard support (e.g., `Agent(model:opus)` to block Opus subagents).
- **Nested skill loading** – Skills placed in `.claude/skills` subdirectories now load when working on files inside those directories; a name clash prefers the nested skill.

## Hot Issues

1. **[#24726 – VS Code: setting to disable auto‑attach of open file/selection](https://github.com/anthropics/claude-code/issues/24726)**  
   *Open for 4 months, 53 comments, 163 👍*  
   A long‑standing request from users who find the automatic context‑attachment intrusive. The high reaction count makes it the most‑upvoted open issue.

2. **[#47023 – Expose compact/session lifecycle hooks for external memory](https://github.com/anthropics/claude-code/issues/47023)**  
   *22 comments, 4 👍*  
   Proposes official hooks for transcript access and compact interception, referencing five open persistence issues. Community is building bespoke solutions; this would standardise the interface.

3. **[#38536 – Shared team memory](https://github.com/anthropics/claude-code/issues/38536)**  
   *13 comments, 6 👍*  
   Extends the individual‑only memory system to enable knowledge sharing across team members. Important for larger organisations adopting Claude Code.

4. **[#64366 – Unbounded MCP server fan‑out crashes macOS](https://github.com/anthropics/claude-code/issues/64366)**  
   *12 comments, 0 👍*  
   Critical stability bug: MCP server instances multiply across Cowork/agent sessions, exhausting RAM and causing kernel panics on an M2 Max with 32 GB.

5. **[#63909 – ENOSPC on subprocess output despite free disk](https://github.com/anthropics/claude-code/issues/63909)**  
   *12 comments, 19 👍*  
   A noisy, repeatable bug where Bash tool reports “temp filesystem full (0MB free)” yet disk space is available. Affects macOS. Multiple duplicates exist.

6. **[#63358 – Opus 4.8 returns empty thinking blocks](https://github.com/anthropics/claude-code/issues/63358)**  
   *10 comments, 10 👍*  
   Extended thinking is invisible in chat with `claude-opus-4-8` because the model sends empty `thinking` fields. Regression from Opus 4.7.

7. **[#12953 – Mousewheel scrolls input history instead of chat on Windows](https://github.com/anthropics/claude-code/issues/12953)**  
   *16 comments, 14 👍*  
   A persistent UI friction in the TUI – mousewheel behaviour is inverted, causing accidental command history navigation instead of scroll.

8. **[#48334 – Desktop app update deletes session history](https://github.com/anthropics/claude-code/issues/48334)**  
   *16 comments, 3 👍*  
   Data‑loss bug: updating from 2.1.34/63/92 to 2.1.101 wipes `sessions-index.json` and `.jsonl` files. High severity.

9. **[#51537 – 10K‑char limit on hook additionalContext is non‑configurable](https://github.com/anthropics/claude-code/issues/51537)**  
   *5 comments, 4 👍*  
   Since v2.1.89, hook output is silently truncated. The limit cripples memory‑layer implementations; users demand it be raised, removed, or made configurable.

10. **[#63423 – CLI 2.1.154 breaks with API Error 422 (“system” role)](https://github.com/anthropics/claude-code/issues/63423)**  
    *8 comments, 2 👍*  
    Regression where the CLI sends an invalid `"system"` message role, causing a 422 error from the Anthropic API. Only affects certain configurations.

## Key PR Progress

1. **[#68678 – Don’t mark Claude Desktop issues as invalid](https://github.com/anthropics/claude-code/pull/68678)**  
   Fixes a triage bot that incorrectly labelled Desktop bug reports as `invalid` because its validity check explicitly excluded “Claude Desktop/Mobile apps”.

2. **[#68707 – `/bug` command to file GitHub issues from terminal](https://github.com/anthropics/claude-code/pull/68707)**  
   New plugin with a `/bug` slash command that auto‑collects environment data and opens a GitHub issue form without leaving the CLI.

3. **[#68672 – Hookify: load only event:all rules for unknown tools](https://github.com/anthropics/claude-code/pull/68672)**  
   Fixes a bug where `event` variable remained `None` for unknown tools, causing all rules to be loaded instead of just `event:all` rules.

4. **[#68671 – Hookify: PostToolUse hooks cannot return deny](https://github.com/anthropics/claude-code/pull/68671)**  
   Corrects the rule engine to allow `deny` from `PostToolUse` hooks (previously both Pre and Post returned deny, but the Post case was broken).

5. **[#68679 – ralph‑wiggum: strip control characters before promise comparison](https://github.com/anthropics/claude-code/pull/68679)**  
   Fixes a stop‑hook that failed to detect `<promise>` tokens when the transcript contained terminal escape sequences.

6. **[#68681 – Correct pagination break condition and HTTP 2xx check](https://github.com/anthropics/claude-code/pull/68681)**  
   Fixes two workflow bugs: premature break when last page is not empty but <100 items, and incorrect HTTP status code check.

7. **[#68699 – Hookify: add Python wrapper and normalize paths on Windows](https://github.com/anthropics/claude-code/pull/68699)**  
   Makes hookify functional on Windows by fixing backslash path issues and ensuring `python3` resolves correctly (not the Microsoft Store stub).

8. **[#68700 – learning‑output‑style: add bash prefix and normalize path for Windows](https://github.com/anthropics/claude-code/pull/68700)**  
   Fixes a SessionStart hook that failed on Windows due to backslashes in `CLAUDE_PLUGIN_ROOT` and missing `bash` prefix.

9. **[#68693 – Add duplicate label additively, don’t replace existing labels](https://github.com/anthropics/claude-code/pull/68693)**  
   Prevents `closeIssueAsDuplicate()` from overwriting all existing issue labels when marking an issue as duplicate.

10. **[#68701 – security‑guidance: strip CRLF from Python version probe on Windows](https://github.com/anthropics/claude-code/pull/68701)**  
    Fixes a silent failure on Windows where `\r` remained after command substitution, causing version checks to always fail.

## Feature Request Trends

- **Persistent / shared memory** – Multiple issues (#47023, #38536, #14227, #32627, #34192) call for hooks or built‑in support for long‑term, team‑wide context storage. The community is building custom solutions (knowledge graphs, markdown architectures) and wants official APIs.
- **Per‑message model selection** – Issue #68165 requests the ability to switch models mid‑conversation (e.g., use Opus for complex reasoning, Sonnet for routine edits) to manage cost and performance.
- **Conversation management** – #65615 asks for archive/delete conversation features in the CLI, reflecting growing usage where session lists become unwieldy.
- **Configurable hook constraints** – #51537 and related requests demand removal or configurability of the 10K‑char limit on `additionalContext` in hooks.
- **VS Code extension polish** – #24726 (disable auto‑attach) and #49739 (inverted thinking toggle) highlight ongoing UI/UX refinement for the IDE integration.

## Developer Pain Points

- **ENOSPC false positives on macOS** – A cluster of issues (#63909, #65166, #65915, #68383, #65067) report Bash tool erroneously claiming the temp filesystem is full when disk space is available. Root cause appears related to `statfs().bsize=0` on Intel Macs and racing cleanup deletes. Very disruptive for daily workflows.
- **Desktop session loss on update** – Issue #48334 describes a recurring data‑loss scenario where updating the Desktop app wipes session history. Low confidence in upgrades.
- **Unbounded resource consumption** – MCP server fan‑out (#64366) and VM image growth (#65577) cause macOS kernel panics and disk fill‑ups. Severity high, especially for users of Cowork/agent modes.
- **Model‑specific regressions** – Empty thinking blocks in Opus 4.8 (#63358) and CLI API 422 error (#63423) point to integration fragility after model updates.
- **Windows compatibility gaps** – Multiple PRs this week fix backslash path issues, CRLF line endings, and missing bash prefixes, indicating the Windows experience still lags behind macOS/Linux.
- **Silent failures and data loss** – #51537 (hook truncation) and #68689 (symlink escape in security config) show risks where errors are swallowed or output is silently discarded.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-16

## Today’s Highlights
OpenAI released Codex CLI **v0.140.0** featuring new `/usage` token-activity dashboards and improved `/goal` handling for oversized content. The community is clamoring for a native Linux desktop app (Issue #11023, 583 👍), while several Windows and macOS performance regressions dominate the bug tracker. A flurry of pull requests aims to fix session-creation latency, add interruptible sleep for models, and improve cross-OS path handling.

---

## Releases
- **v0.140.0** — New `/usage` views for daily, weekly, and cumulative token activity; `/goal` now preserves oversized text, large pasted blocks, and image attachments (including in remote app-server sessions); permanent session deletion added.  
- **v0.141.0-alpha.1 / alpha.2** — Pre-release alpha versions published (no changelog details).

> [Full release history](https://github.com/openai/codex/releases)

---

## Hot Issues (Top 10)

1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Community request* (113 comments, 583 👍). Users need a native Linux app due to macOS power/performance issues. Remains the most upvoted open feature request.

2. **[#12661 – Markdown `file://` links open in Edge instead of VS Code on Windows](https://github.com/openai/codex/issues/12661)**  
   *Bug* (47 comments, 43 👍). Windows users report that local Markdown links in Codex responses open in the default browser instead of the VS Code editor. Affects workflow for documentation-heavy tasks.

3. **[#3355 – Error after MacBook sleeps](https://github.com/openai/codex/issues/3355)**  
   *Bug* (37 comments, 19 👍). Codex CLI fails to reconnect after lid-close on macOS, losing long-running tasks. Several users report similar connectivity breaks.

4. **[#21527 – Codex is really too slow](https://github.com/openai/codex/issues/21527)**  
   *Performance* (32 comments, 17 👍). Broad complaint about slow model responses in both VS Code extension and desktop app on Windows. Impact on Pro subscribers.

5. **[#25719 – `syspolicyd` / `trustd` CPU runaway on macOS](https://github.com/openai/codex/issues/25719)**  
   *Performance* (26 comments, 33 👍). Codex Desktop triggers persistent system daemon CPU spikes, making the app unusable. Multiple duplicates reported.

6. **[#27817 & #28015 – False positive cybersecurity flags](https://github.com/openai/codex/issues/27817)**  
   *Safety* (18+18 comments). Authorized tax filing and local repo maintenance are incorrectly blocked by the cybersecurity safety check. User frustration with interruption of legitimate work.

7. **[#28094 – WSL path rewriting on Windows](https://github.com/openai/codex/issues/28094)**  
   *Bug* (13 comments). Codex Desktop rewrites `/home` paths to `C:\home`, breaking project chat associations for WSL users. After the latest update.

8. **[#28190 – `rg` blocked by macOS](https://github.com/openai/codex/issues/28190)**  
   *Bug* (9 comments, 6 👍). Codex CLI v0.139.0 on macOS fails when trying to use `rg` (ripgrep) due to macOS security restrictions. Blocks code search workflows.

9. **[#25709 – Windows app extremely sluggish after update](https://github.com/openai/codex/issues/25709)**  
   *Performance* (9 comments, 2 👍). Post-update Windows Desktop app becomes unusably slow; user suspects Windows firewall interference.

10. **[#27331 – `multi_agent_v2` breaks every turn with 400 error](https://github.com/openai/codex/issues/27331)**  
    *Regression* (4 comments, 5 👍). Enabling `multi_agent_v2` in config.toml causes API validation failure on every turn, even without sub-agent usage. Sev3 for dogfooders.

---

## Key PR Progress

1. **[#28421 – Bind shell snapshots to retained thread environments](https://github.com/openai/codex/pull/28421)**  
   Fixes session-scoped shell snapshots so they persist per-turn environment, enabling snapshot reuse across restarts.

2. **[#28429 – Add interruptible sleep tool](https://github.com/openai/codex/pull/28429)**  
   Built-in `sleep` tool under feature flag allows models to pause without blocking a shell process; respects new turn input.

3. **[#28307 – Queue TUI follow-ups through app-server](https://github.com/openai/codex/pull/28307)**  
   Proof-of-concept for durable follow-up queuing from TUI, enabling idle-path dispatch when User Message Queue is enabled.

4. **[#27982 – Start guardian child session when parent session starts](https://github.com/openai/codex/pull/27982)**  
   Pre-creates the Guardian reviewer session during parent initialization to reduce first-review latency.

5. **[#20702 – Support `PreToolUse permissionDecision: ask`](https://github.com/openai/codex/pull/20702)** *(Closed)*  
   Allows pre-hooks to escalate an allowed tool call to explicit human approval, adding a middle ground between deny and allow.

6. **[#28426 – Share resumed rollout history](https://github.com/openai/codex/pull/28426)**  
   Reduces deep-clone copies of persisted rollout history, improving memory and startup performance when resuming threads.

7. **[#26334 – Retry transient Guardian reviewer failures](https://github.com/openai/codex/pull/26334)** *(Closed)*  
   Treats capacity/rate-limit/timeout errors as retryable, preventing infrastructure blips from blocking safe actions.

8. **[#28034 – Add local credential broker](https://github.com/openai/codex/pull/28034)**  
   Extends network proxy with credential_broker to inject dummy tokens into child processes, keeping real credentials inside the MITM proxy.

9. **[#28367 – Use `ApiPathString` in app-server filesystem permission paths](https://github.com/openai/codex/pull/28367)** *(Closed)*  
   Enables cross-OS sandbox config paths (e.g., Linux app-server + Windows executor) by moving from `AbsolutePathBuf` to `PathUri`.

10. **[#28260 – Add internal auto-compaction opt-out](https://github.com/openai/codex/pull/28260)**  
    Adds `auto_compaction` feature flag as an escape hatch; preserves manual `/compact` and native context-window error reporting.

---

## Feature Request Trends
- **Native Linux Desktop App** – The single most-requested feature (#11023, 583 👍). Users cite macOS power/performance issues as motivation.
- **Improved Cross-Platform Path Handling** – Multiple issues request better support for WSL, Windows ↔ macOS remote sessions, and path normalization (e.g., #28094, #28152, #28146).
- **Sub-agent / Multi-Agent Stability** – Feature flag `multi_agent_v2` remains unstable (#27331); users want reliable sub-agent spawning.
- **Customizable Safety Filter Calibration** – False positive cybersecurity flags (#27817, #28015) drive demand for user-controllable sensitivity or an allowlist for authorized tasks.
- **Performance & Latency** – Broad calls for faster model responses, especially on Windows Desktop (#21527, #25709).

---

## Developer Pain Points
- **False Positive Safety Flags** – Multiple users report repeated interruption of legitimate work (tax filing, local repo maintenance) by the cybersecurity filter.
- **macOS `syspolicyd` / `trustd` CPU Spikes** – Codex Desktop on macOS triggers system daemon runaway, requiring reboot (#25719, #28071).
- **Windows WSL Path / Agent Failures** – WSL integration is fragile: paths rewritten, CLI not found, sandbox helper missing (#28094, #28086, #27125).
- **Post-Sleep Connectivity Loss** – macOS users lose long-running sessions after lid-close (#3355).
- **Rate-Limit Confusion** – Users report stuck “out of messages” state despite having available credits (#23258).
- **Performance Regressions** – Updates often bring sluggishness on Windows (#25709) and persistent slowness across platforms (#21527).

*All data sourced from [github.com/openai/codex](https://github.com/openai/codex).*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-16

## Today's Highlights

No new releases were published today, but the community remains highly active with 50 issues and 27 PRs updated in the last 24 hours. The team is making progress on critical agent reliability fixes—most notably PRs that prevent SSRF attacks via DNS hostnames and improve subagent execution stability. Long-running bugs like the generalist agent hang (#21409) and subagent success misreporting (#22323) continue to draw community attention, with several users actively upvoting and commenting.

---

## Releases

*(No new releases in the last 24 hours.)*

---

## Hot Issues

1. **#21409 – Generalist agent hangs**  
   *priority/p1, 7 comments, 8 👍*  
   The agent defers to a subagent and never returns. Workaround: instruct the model not to use subagents.  
   https://github.com/google-gemini/gemini-cli/issues/21409

2. **#22323 – Subagent recovery after MAX_TURNS reported as GOAL success**  
   *priority/p1, 6 comments, 2 👍*  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even after hitting the max-turn limit with zero analysis.  
   https://github.com/google-gemini/gemini-cli/issues/22323

3. **#25166 – Shell command execution stuck with "Waiting input" after command completes**  
   *priority/p1, 4 comments, 3 👍*  
   Simple CLI commands finish but the tool remains active, falsely awaiting user input.  
   https://github.com/google-gemini/gemini-cli/issues/25166

4. **#22745 – Assess AST-aware file reads, search, and mapping**  
   *priority/p2, 7 comments, 1 👍*  
   Epic to evaluate whether AST-aware tools (e.g., tilth, glyph) can reduce turns, noise, and misaligned reads for codebase operations.  
   https://github.com/google-gemini/gemini-cli/issues/22745

5. **#24353 – Robust component level evaluations**  
   *priority/p1, 7 comments*  
   Follow-up on behavioral evals; already 76 tests written across 6 Gemini models. Needs to scale and harden.  
   https://github.com/google-gemini/gemini-cli/issues/24353

6. **#26525 – Add deterministic redaction and reduce Auto Memory logging**  
   *priority/p2, 5 comments*  
   Secrets may leak before redaction because extraction prompt runs on already-sent content. Also logs skill results unintentionally.  
   https://github.com/google-gemini/gemini-cli/issues/26525

7. **#26522 – Stop Auto Memory from retrying low-signal sessions indefinitely**  
   *priority/p2, 5 comments*  
   Low-signal sessions are never marked processed, leading to infinite re-extraction attempts.  
   https://github.com/google-gemini/gemini-cli/issues/26522

8. **#21968 – Gemini does not use skills and sub-agents enough**  
   *priority/p2, 6 comments*  
   Custom skills (e.g., gradle, git) are ignored unless explicitly instructed. Community requests better tool-use prompting.  
   https://github.com/google-gemini/gemini-cli/issues/21968

9. **#21983 – Browser subagent fails in Wayland**  
   *priority/p1, 4 comments, 1 👍*  
   BrowserAgent crashes on Wayland; termination reason reported as GOAL but no useful result.  
   https://github.com/google-gemini/gemini-cli/issues/21983

10. **#27615 – Cmd+Backspace deletes entire input without undo**  
    *priority/p2, 3 comments*  
    Mac shortcut deletes all text, with no undo (Cmd+Z). Community proposes word-level deletion as standard Mac behavior.  
    https://github.com/google-gemini/gemini-cli/issues/27615

---

## Key PR Progress

1. **#27956 – Support GDC air-gapped Service Identity**  
   *area/security, size/m*  
   Passes `universe_domain` to Google Auth library to enable token exchange in air-gapped environments.  
   https://github.com/google-gemini/gemini-cli/pull/27956

2. **#27572 – Fix tmux false positive background detection**  
   *size/m, closed*  
   Corrects theme switching regression inside tmux (especially via mosh) by ignoring tmux’s fake `#ffffff` background.  
   https://github.com/google-gemini/gemini-cli/pull/27572

3. **#27603 – Platform-aware shell guidance**  
   *area/agent, size/m, closed*  
   Adds Windows-specific shell commands to the preview-model prompt, fixing #27751.  
   https://github.com/google-gemini/gemini-cli/pull/27603

4. **#27626 – Block private OAuth metadata URLs (SSRF protection)**  
   *area/security, size/m, closed*  
   Prevents SSRF by blocking OAuth metadata URLs that resolve to private IPs during MCP discovery.  
   https://github.com/google-gemini/gemini-cli/pull/27626

5. **#27744 – Resolve DNS before SSRF guard**  
   *size/l, open*  
   Synchronous `isPrivateIp` fails on hostnames like `127.0.0.1.nip.io`. This PR adds async DNS resolution to the SSRF check.  
   https://github.com/google-gemini/gemini-cli/pull/27744

6. **#27739 – Prevent SSRF via DNS hostnames and redirects**  
   *size/l, open*  
   Additional fixes for SSRF bypass through DNS aliases and redirect chains.  
   https://github.com/google-gemini/gemini-cli/pull/27739

7. **#24478 – Add top-level `/reload` command**  
   *size/m, closed*  
   Consolidates all reload subcommands (skills, agents, MCP, memory, settings) into a single `/reload` action.  
   https://github.com/google-gemini/gemini-cli/pull/24478

8. **#27939 – Fix nightly release CI stall**  
   *priority/p1, size/xs, closed*  
   Switches scheduled nightly releases from `prod` environment (requires manual approval) to an internal unprotected environment.  
   https://github.com/google-gemini/gemini-cli/pull/27939

9. **#27948 – Pin dependencies and enforce 14-day update cooldown**  
   *size/xl, open*  
   Strips version ranges, pins all direct deps to exact versions, and enforces a 14-day cooldown for automated updates.  
   https://github.com/google-gemini/gemini-cli/pull/27948

10. **#27854 – Fix pending tools and trust overrides**  
    *size/l, closed*  
    Prevents premature state progression while waiting for user tool approvals, forces sequential file writes, and fixes a config bug for trust overrides.  
    https://github.com/google-gemini/gemini-cli/pull/27854

---

## Feature Request Trends

- **AST-aware code intelligence**: Multiple issues (#22745, #22746, #22747) propose integrating AST-based tools for file reads, search, and codebase mapping to reduce token usage and improve agent accuracy.  
- **Robust evaluation infrastructure**: #24353 and #23166 call for scalable, stable behavioral and internal evals that can be trusted for regression detection.  
- **Agent self-awareness**: #21432 asks the CLI to understand its own flags, hotkeys, and capabilities so it can guide users or self-execute tasks.  
- **Subagent and skill usage improvement**: #21968 and #22672 highlight the need for better heuristics to invoke subagents/skills and to discourage destructive operations (e.g., `git reset --force`).  
- **Memory system hardening**: A cluster of issues (#26516, #26522, #26523, #26525) requests deterministic redaction, infinite-loop prevention, and quarantine of invalid patches in Auto Memory.

---

## Developer Pain Points

- **Agent hangs and silent failures**: The generalist agent hang (#21409) and subagent success misreporting (#22323) erode trust in autonomous workflows.  
- **Shell execution glitches**: Command complete but tool remains "Waiting input" (#25166) and OS-specific input handling bugs (e.g., #27615) disrupt local development flows.  
- **Memory system quirks**: Unprocessed low-signal sessions (#26522), leaked secrets before redaction (#26525), and silent disk-full disabling (#27277) make the memory feature unreliable.  
- **Browser agent instability**: Wayland crashes (#21983), ignore of settings overrides (#22267), and lack of session lock recovery (#22232) limit cross-platform use.  
- **High resource consumption**: High memory usage reported (#27938) and flicker issues on terminal resize (#21924) affect long coding sessions.  
- **Configuration and tool bypass**: Subagents running without permission (#22093), 400 errors with >128 tools (#24246), and MCP allowlist bypass (#27605/27626) indicate brittleness.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-16

## Today’s Highlights
Two patch releases (v1.0.63 and v1.0.63-0) landed yesterday, focusing on better error messaging for blocked images, alphabetically sorted `--help` output, and a new `deferTools` option for MCP server configuration. The community remains active on enterprise permission concerns and a regression in the `userPromptSubmitted` hook, while a high‑demand feature request for multi‑BYOK model support continues to gain traction.

## Releases
**v1.0.63** (2026-06-15) — [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.63)
- Blocked image attachments now display a clear explanation with actionable steps (enable vision via policy, switch to a vision‑capable model, or try a different image) instead of a confusing error.
- Options in `--help` output are now sorted alphabetically, including options that have two dashes.

**v1.0.63-0** (2026-06-15) — [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.63-0)
- **Added:** Press `w` in `/diff` to hide whitespace‑only changes.
- **Added:** New `deferTools` option in MCP server config to keep tools always available even when tool search is enabled.
- **Improved:** Reliability of OpenAI, Anthropic, and Azure OpenAI requests.
- **Experimental:** `/rewind` no longer … (details cut off in source).

## Hot Issues
1. **#953 – Over excessive permissions** [OPEN]  
   *Enterprise* – Users cannot restrict Copilot’s access to specific repos/areas. 7 comments, 3 👍.  
   [Issue #953](https://github.com/github/copilot-cli/issues/953)

2. **#3727 – Regression: userPromptSubmitted hook no longer injects additionalContext** [OPEN]  
   *Plugins / Context memory* – Working in v1.0.59, broken in v1.0.60. 4 comments.  
   [Issue #3727](https://github.com/github/copilot-cli/issues/3727)

3. **#3282 – Add multiple BYOK model capability** [OPEN]  
   *Configuration* – Currently only one Bring‑Your‑Own‑Key model via env var. 3 comments, 8 👍 (highest 👍 count).  
   [Issue #3282](https://github.com/github/copilot-cli/issues/3282)

4. **#3781 – Session unrecoverable after pasting image with non‑multimodal model** [CLOSED]  
   *Sessions / Models* – Every prompt fails with HTTP 400 once an image is attached. 3 comments.  
   [Issue #3781](https://github.com/github/copilot-cli/issues/3781)

5. **#3756 – Third‑party MCP servers disabled by organization policy** [CLOSED]  
   *Enterprise / MCP* – Users blocked despite needing 3rd‑party servers. 3 comments.  
   [Issue #3756](https://github.com/github/copilot-cli/issues/3756)

6. **#2966 – Built‑in tooling for multiple concurrent CLI sessions** [OPEN]  
   *Sessions* – Power users need first‑class support for managing many sessions. 3 comments.  
   [Issue #2966](https://github.com/github/copilot-cli/issues/2966)

7. **#3776 – UTF‑8 mojibake when pasting from WSL/Ubuntu terminal to Windows** [OPEN]  
   *Input / Cross‑platform* – Correct display but corrupted paste. 2 comments.  
   [Issue #3776](https://github.com/github/copilot-cli/issues/3776)

8. **#3784 – Tokio reactor panic on Linux ARM64** [CLOSED]  
   *Platform / Linux* – Crash after first message on ARM64. 2 comments.  
   [Issue #3784](https://github.com/github/copilot-cli/issues/3784)

9. **#3769 – Thread problems in terminal output** [CLOSED]  
   *Rendering* – Output mangled until response completes. 2 comments, 3 👍.  
   [Issue #3769](https://github.com/github/copilot-cli/issues/3769)

10. **#3716 – [Regression] Function call fails** [CLOSED]  
    *Models / Tools* – Invalid JSON schema error starting in v1.0.60. 1 comment.  
    [Issue #3716](https://github.com/github/copilot-cli/issues/3716)

## Key PR Progress
Only one PR was updated in the last 24 hours, and it appears to be non‑substantive (spam).  
- **#3817** – `kCreate "#"` with summary “aquellos” – [PR #3817](https://github.com/github/copilot-cli/pull/3817) (no meaningful changes).

No significant pull requests to report this week.

## Feature Request Trends
Based on open issues, the top community‑requested directions are:

- **Multi‑model / BYOK flexibility** – Support for multiple BYOK models concurrently, custom HTTP headers per model, and prompt caching for Claude to reduce latency/cost.
- **Session management** – First‑class support for multiple concurrent sessions, content‑based `/resume` search, and unification with VS Code Copilot Chat history via `/chronicle`.
- **MCP improvements** – Granular enterprise policies for third‑party MCP servers, better tool access for sub‑agents, and OAuth retry backoff.
- **Platform compatibility** – Correct UTF‑8 handling across WSL/Windows, Windows standalone executable reliability, and indication of git worktrees in the UI.

## Developer Pain Points
Recurring frustrations reported this period:

- **Regressions** – The `userPromptSubmitted` hook and function call validation broke in v1.0.60, forcing downgrades or workarounds.
- **Unrecoverable session errors** – Pasting an image into a non‑multimodal model or attaching an oversized document permanently wedges a session; manual editing of `events.jsonl` is the only escape.
- **Platform crashes** – ARM64 Tokio panic (fixed in later patch) and Windows executable extraction failure (`EPERM`) block users on specific systems.
- **Encoding woes** – Copy–paste of non‑ASCII text produces mojibake on Windows terminals and VS Code’s integrated terminal.
- **MCP server instability** – Unbounded respawn loops in stdio servers and excessive OAuth fan‑out waste resources and hit rate limits.
- **AI consumption despite failures** – Failed requests still count toward AIC quota, leaving users with no recourse but to open support tickets.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-16

## Today’s Highlights
No new releases landed today, but two important PRs fix long‑standing bugs: one resolves `kimi --continue` failing to find sessions (#2222), and another ensures the `UserPromptSubmit` hook receives actual user input instead of an empty string (#2303). Meanwhile, a fresh bug report (#2455) highlights a proxy‑unaware `FetchURL` that breaks under restrictive network environments, and an older issue (#2402) about compaction failures due to “high risk” API rejections remains open with no fix yet.

## Releases
No new releases in the last 24 hours. The latest stable version remains **1.44.0** (as referenced in issue #2303).

## Hot Issues
*All four open issues updated in the last 24h are listed. Since the total is less than 10, every one is included.*

- **#2402 – [bug] Error: [compaction.failed] APIStatusError: 400 “high risk”**  
  Author: `thoughtworld` · Created: 2026-05-30 · Updated: 2026-06-16 · Comments: 2  
  The API rejected a compaction request as “high risk”, blocking the workflow. No resolution yet; community speculation points to rate‑limiting or misuse detection.  
  [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2402)

- **#2303 – [bug] UserPromptSubmit hook receives empty prompt from shell UI**  
  Author: `AkaCoder404` · Created: 2026-05-15 · Updated: 2026-06-15 · Comments: 1  
  Regex‑based prompt hooks never match because the hook payload always contains `"prompt": ""`. A fix PR (#2454) is now open.  
  [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2303)

- **#2222 – [bug] `kimi --continue` reports “No previous session found” despite visible history**  
  Author: `LiPingFeel` · Created: 2026-05-11 · Updated: 2026-06-15 · Comments: 1  
  Running `kimi` (without `--continue`) shows the last session, but `--continue` fails. The missing session ID lookup logic is being addressed in PR #2453.  
  [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2222)

- **#2455 – [bug] FetchURL does not read system proxy; fails in blocked environments**  
  Author: `KuangYin-Z` · Created: 2026-06-15 · Updated: 2026-06-15 · Comments: 0  
  Using Kimi Code CLI behind a firewall, `FetchURL` bypasses system proxy settings, while `shell/curl` work fine. Affects users in restricted networks. No PR yet.  
  [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2455)

## Key PR Progress
*Two pull requests were updated in the last 24h.*

- **#2454 – fix(hooks): pass prompt text to UserPromptSubmit from structured input**  
  Author: `logicwu0` · Created: 2026-06-15 · Comments: 0  
  Fixes #2303 by correctly deriving the hook text from the actual user input in `KimiSoul._turn` instead of an empty placeholder.  
  [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2454)

- **#2453 – fix(session): resume latest session when last_session_id is missing**  
  Author: `logicwu0` · Created: 2026-06-15 · Comments: 0  
  Fixes #2222 by implementing a fallback that locates the most recent session for the working directory when `Session.continue_` cannot find an explicit `last_session_id`.  
  [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2453)

## Feature Request Trends
None of the recent issues contain explicit feature requests; all are bug reports. However, the recurring pattern of network‑related blockers (¶ #2455) and session‑handling fragility (¶ #2222) suggests a need for better network configurability and more robust session tracking. The hook bug (#2303) indicates that developer‑tool extensibility (hooks) is used but not fully tested for all input paths.

## Developer Pain Points
- **API rejections without clear cause** (#2402): Users hit 400 errors with “high risk” labels but no documentation or retry guidance.  
- **Session resumption inconsistency** (#2222): The `--continue` flag behaves differently than plain `kimi` in the same directory, confusing developers.  
- **Proxy ignorance** (#2455): `FetchURL` ignores system proxy settings, blocking users behind corporate or national firewalls.  
- **Hook reliability** (#2303): Custom prompt hooks break silently when input comes from the shell UI, undermining automation workflows.  

All four bugs affect developer productivity directly, with two already receiving fixes in PRs.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

Here is the **OpenCode Community Digest** for **2026-06-16**, generated from the latest GitHub activity.

---

## OpenCode Community Digest — 2026-06-16

### 1. Today's Highlights

Community attention remains focused on a high-volume **memory and performance megathread** (#20695) and longstanding requests for **agent sandboxing** (#2242). A critical discussion has emerged around **Anthropic OAuth usage leading to account bans** (#6930), raising significant developer trust concerns. On the feature front, a highly-upvoted proposal for **native session goals** (`/goal` command, #27167) and a deep-dive on **MCP client capabilities** (#28567) are driving the conversation.

### 2. Releases

**No new versions were released in the last 24 hours.**

---

### 3. Hot Issues

1.  **[#20695 – Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)**
    - **Why it matters:** A central hub for scattered memory leak reports. The maintainer has explicitly asked users to collect heap snapshots rather than suggesting fixes. High engagement (97 comments) indicates this is a critical stability blocker.
    - **Reaction:** Heavily upvoted (65 👍); the community is mobilized for debugging but requires clear action from the team.

2.  **[#2242 – Is there a way to sandbox the agent?](https://github.com/anomalyco/opencode/issues/2242)**
    - **Why it matters:** A critical security request to restrict agent terminal access (e.g., macOS Seatbelt emulation). This has been open for ~10 months with high community interest (69 comments, 53 👍).
    - **Reaction:** A recurring pain point; the lack of sandboxing is a barrier for enterprise adoption.

3.  **[#27167 – Native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167)**
    - **Why it matters:** Proposes a persistent, built-in session lifecycle feature (`/goal`). This would be a major UX improvement over relying on manual prompts.
    - **Reaction:** Very high demand (84 👍), suggesting this is the most desired new feature.

4.  **[#6930 – Using OpenCode with Anthropic OAuth violates ToS & results in ban](https://github.com/anomalyco/opencode/issues/6930)**
    - **Why it matters:** A severe, high-impact issue. Users who followed OpenCode’s documented OAuth flow are getting their Claude accounts banned. The OAuth integration may be misconfigured or violate Anthropic’s terms.
    - **Reaction:** Closed but contentious; likely a top priority for maintainers to mitigate reputational damage.

5.  **[#27906 – v1.15.1+ Breaks Bun Installs](https://github.com/anomalyco/opencode/issues/27906)**
    - **Why it matters:** A recent release broke global package installation with Bun (a fast-growing alternative to Node). This is a compatibility regression.
    - **Reaction:** 18 comments and 13 👍, highlighting the frustration of a breaking change in a popular environment.

6.  **[#5374 – Show tokens/second](https://github.com/anomalyco/opencode/issues/5374)**
    - **Why it matters:** Enables users to benchmark LLM providers directly within the TUI. Essential for cost/performance optimization.
    - **Reaction:** One of the highest upvoted feature requests (81 👍) with 17 comments—clearly a core need for power users.

7.  **[#28567 – Full MCP client capabilities](https://github.com/anomalyco/opencode/issues/28567)**
    - **Why it matters:** OpenCode’s MCP implementation is falling behind the standard. This issue tracks aligning with the latest spec (e.g., `InitializeResult.instructions`).
    - **Reaction:** 14 comments and 22 👍. A key integration gap that is attracting active PRs.

8.  **[#28957 / #31456 – "Upstream idle timeout exceeded"](https://github.com/anomalyco/opencode/issues/28957)**
    - **Why it matters:** A recurring error during long-running tasks, particularly with the "writing-plans" skill. Multiple reports suggest a systemic session management bug.
    - **Reaction:** Frustrated users; no workaround provided.

9.  **[#30869 – Hardcoded UTF-8 decoding on non-UTF-8 systems](https://github.com/anomalyco/opencode/issues/30869)**
    - **Why it matters:** A localization bug causing garbled output on Windows systems using CJK encodings (GBK). Affects a significant non-English userbase.
    - **Reaction:** Low activity but high severity; a quick fix is warranted.

10. **[#32420 – Paid Go subscription—charged but not activated](https://github.com/anomalyco/opencode/issues/32420)**
    - **Why it matters:** A billing/fulfillment bug with multiple reports of users being charged but unable to access their subscription. No response from support (help@anoma.ly).
    - **Reaction:** Negative sentiment; potential legal/compliance risks mentioned in related issues.

---

### 4. Key PR Progress

1.  **[#32490 – `feat(mcp): append server instructions to context`](https://github.com/anomalyco/opencode/pull/32490)**
    - **Description:** Implements part of the MCP standard by reading `InitializeResult.instructions` from MCP servers and injecting them into the LLM context.
    - **Impact:** Critical for MCP spec alignment; references the major feature request #28567.

2.  **[#32494 – `fix(opencode): include PR identity in github context`](https://github.com/anomalyco/opencode/pull/32494)**
    - **Description:** Adds PR number and URL to the `<pull_request>` context for `opencode github run`.
    - **Impact:** Enables PR-comment runs to know their own identity, fixing a real workflow bug.

3.  **[#32499 – `fix(opencode): allow clearing session archive time`](https://github.com/anomalyco/opencode/pull/32499)**
    - **Description:** Introduces a UI to clear (un-archive) a session, previously an irreversible operation.
    - **Impact:** Solves a long-standing UX pain point for developers managing long sessions.

4.  **[#29150 – `fix(opencode): break auto-compact loop when compaction makes no progress`](https://github.com/anomalyco/opencode/pull/29150)**
    - **Description:** Prevents an infinite compaction loop when a model’s reported context limit is smaller than reality.
    - **Impact:** Directly addresses a "spinning forever" bug that wastes tokens and freezes sessions.

5.  **[#32489 – `fix(opencode): sanitize OpenAI MCP tool schemas`](https://github.com/anomalyco/opencode/pull/32489)**
    - **Description:** Clean JSON Schema keywords from MCP tool parameters to prevent OpenAI API rejections.
    - **Impact:** Improves compatibility with the OpenAI provider, closing a recent regression.

6.  **[#31644 – `fix(acp): register compact and summarize commands for visibility`](https://github.com/anomalyco/opencode/pull/31644)**
    - **Description:** Adds `/compact` and `/summarize` to command autocomplete and `/help`.
    - **Impact:** Addresses a discoverability issue for core session management features.

7.  **[#29150 – `fix(opencode): break auto-compact loop`](https://github.com/anomalyco/opencode/pull/29150)**
    - **Description:** (See above) A high-priority fix for a critical session management loop.
    - **Impact:** Reduces token waste and improves session stability.

8.  **[#29006 – `docs(ecosystem): add opencode-datarobot-skills plugin`](https://github.com/anomalyco/opencode/pull/29006)**
    - **Description:** Adds a new open-source plugin for DataRobot’s AI skill library.
    - **Impact:** Grows the ecosystem; provides enterprise-grade skills to the community.

9.  **[#28466 – `fix(opencode): ignore MCP resource file downloads`](https://github.com/anomalyco/opencode/pull/28466)**
    - **Description:** Prevents the tool from downloading files when a user `@`-mentions an MCP resource.
    - **Impact:** Resolves multiple user complaints about unintended downloads.

10. **[#27800 – `refactor(opencode): lazy-load top-level CLI commands`](https://github.com/anomalyco/opencode/pull/27800)**
    - **Description:** Deferred-loads command modules to make `--help` and `--version` faster.
    - **Impact:** Improves CLI startup latency for non-task operations—a subtle but welcome perf win.

---

### 5. Feature Request Trends

- **Native Session Goals & Lifecycle:** The `/goal` feature (#27167) dominates, with 84 upvotes. Users want persistent, declarative objectives that survive across turns.
- **Full MCP Integration:** Strong push for alignment with the latest MCP spec (#28567), including instructions injection, resource handling, and better tool schema support.
- **LLM Performance Metrics:** High demand (81 👍) for displaying tokens/second (#5374) to benchmark providers.
- **Agent Sandboxing & Permissions:** Repeated requests for file system and network sandboxing (#2242, #16914) to prevent agent escape.
- **Skill & Tool Scoping:** Users want agents to only load relevant skills (#19344) and to be explicitly aware of their own capabilities (#32457).

---

### 6. Developer Pain Points

- **Memory Leaks & Session Stability:** The memory megathread (#20695) and infinite compaction loops (#29150) are top pain points, causing frequent session freezes.
- **Unresponsive Support & Billing:** Charged but non-functional subscriptions (#32420, #32482) and reports of "no contact" from support are eroding trust.
- **Bun/Non-NPM Package Manager Compatibility:** The recent breaking change with Bun postinstall scripts (#27906) is a major regression for alternative toolchains.
- **Anthropic OAuth Readiness:** The risk of account bans via the official OAuth flow (#6930) is a critical reputation risk.
- **ID Timeouts & Freezing:** "Upstream idle timeout" errors (#28957, #31456) and CLI freeze after build completion (#19252) indicate poor timeout handling.
- **Non-English Encoding Issues:** Hardcoded UTF-8 decoding in `bash.ts` (#30869) breaks CJK users on Windows.
- **Windows Desktop Crashes:** The renderer unresponsive on startup (#32452) and clipboard image paste failure in TUI (#32479) degrade the Windows UX.
- **Missing Command Discoverability:** Users struggle to find features like `/compact` (#31644) and scrollbars (#27795), hinting at a need for UI/UX polish.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-16

## Today's Highlights

Version **v0.79.4** shipped with an automatic first-run theme selector and other improvements. A major regression (Escape not interrupting tasks) was fixed, and the community pushed critical provider‑related PRs (Bedrock Mantle, ZAI‑CN, Gemini‑3.5). Ongoing stability work addressed stream hangs, session sorting, and TUI rendering crashes.

---

## Releases

**v0.79.4** – [Release notes](https://github.com/earendil-works/pi/releases/tag/v0.79.4)
- Automatic first-run theme selection – `pi` detects terminal background on first run and defaults to `dark` or `light`.
- Standalone binary improvements (details in the release).

---

## Hot Issues

1. **[#4945](https://github.com/earendil-works/pi/issues/4945) – OpenAI Codex connection reliability**  
   GPT‑5.5 leaves the TUI stuck on “Working…” with no error; only Escape recovers. 57 comments, 30 👍. High impact for all Codex users.

2. **[#5103](https://github.com/earendil-works/pi/issues/5103) – Windows git‑bash not detected from PATH**  
   Built‑in bash tool fails to find Git Bash even when installed. 21 comments. Frustrating for Windows users.

3. **[#4877](https://github.com/earendil-works/pi/issues/4877) – Session folder collision**  
   Different paths can map to the same session folder due to hashing (e.g., `/a/b/c/d` vs `/a-b/c-d`). 15 comments. Low priority but potential confusion.

4. **[#5363](https://github.com/earendil-works/pi/issues/5363) – Add Amazon Bedrock Mantle provider**  
   Newer Bedrock Mantle models use OpenAI‑compatible API, incompatible with existing Converse‑based provider. 13 comments, 3 👍. Wanted by AWS users.

5. **[#5653](https://github.com/earendil-works/pi/issues/5653) – Move off Shrinkwrap**  
   When using both `pi-ai` and `pi-coding-agent` packages, duplicate module copies cause API provider registry issues. 10 comments. Core packaging problem.

6. **[#5702](https://github.com/earendil-works/pi/issues/5702) – `prompt_cache_retention` sent to rejecting providers**  
   OpenCode/Zen reject requests because the model registry sends unsupported fields. 8 comments. Affects multiple providers.

7. **[#5696](https://github.com/earendil-works/pi/issues/5696) – Model name not refreshing in TUI on CTRL+P**  
   Switching models via keyboard shortcut shows stale name or skips positions. 8 comments. Usability annoyance.

8. **[#5687](https://github.com/earendil-works/pi/issues/5687) – `pi list` / `pi update` never exit when extension runs an MCP server**  
   Long‑lived MCP server keeps the process alive, blocking CI/scripting. 7 comments. Critical for extension users.

9. **[#5736](https://github.com/earendil-works/pi/issues/5736) – Escape no longer interrupts active task**  
   Solved in today’s PRs but generated 7 comments. Regressed from a previous fix; co‑authored by GPT‑5.5.

10. **[#5728](https://github.com/earendil-works/pi/issues/5728) – Support provider‑specific config in `auth.json`**  
    Some providers (e.g., Cloudflare AI Gateway) need accountId/gatewayId beyond API key. 6 comments, 0 👍 but important for multi‑provider setups.

---

## Key PR Progress

1. **[#5789](https://github.com/earendil-works/pi/pull/5789) – fix(tui): restore cursorUp start‑of‑line jump**  
   Fixes regression where Up arrow always opened history instead of jumping to line start when editor non‑empty.

2. **[#5675](https://github.com/earendil-works/pi/pull/5675) – fix: stabilize compaction after reload**  
   Preserves token boundaries during repeated compaction and fixes harness copy. Closed.

3. **[#5784](https://github.com/earendil-works/pi/pull/5784) – fix(coding‑agent): sort threaded sessions by latest activity**  
   Sessions now ordered by subtree activity, not root modification date. Open.

4. **[#5779](https://github.com/earendil-works/pi/pull/5779) – feat(coding‑agent): XML‑structure /review prompt responses**  
   Converts `/review` to XML envelopes, adds coverage‑aware workflow. Closed.

5. **[#5776](https://github.com/earendil-works/pi/pull/5776) – Fix agent wedge on unresponsive streams & tool executions**  
   Addresses indefinite hangs when LLM stream stalls or tool promise never resolves. Fixes #2381. Closed.

6. **[#5758](https://github.com/earendil-works/pi/pull/5758) – feat(coding‑agent): diagnose when child holds stdio open past exit**  
   Follow‑up to #5753; adds diagnostics for bash timeouts. Closed.

7. **[#5587](https://github.com/earendil-works/pi/pull/5587) – feat(coding‑agent): experimental first‑time setup flow**  
   Behind `PI_EXPERIMENTAL=1`, shows theme picker and analytics opt‑in on first launch. Closed.

8. **[#5509](https://github.com/earendil-works/pi/pull/5509) – feat: Add Amazon Bedrock Mantle OpenAI Responses provider**  
   New provider for GPT‑5.5/5.4 using Mantle’s OpenAI‑compatible API. Open.

9. **[#5765](https://github.com/earendil-works/pi/pull/5765) – feat(d‑pi): split `createDPiExtension` into two focused extensions**  
   Separates multi‑agent orchestration from remote executor. Closed.

10. **[#5752](https://github.com/earendil-works/pi/pull/5752) – fix: `pi.sendUserMessage`/`sendMessage` return Promise**  
    Extension API now properly awaits agent completion. Closed.

---

## Feature Request Trends

- **Provider expansion** – Multiple requests for new backends: Amazon Bedrock Mantle, ZAI‑CN (Bigmodel), Gemini‑3.5‑Flash, and improved Cloudflare AI Gateway support.
- **Extension API improvements** – Exposing diff utilities, making `sendMessage` awaitable, adding custom OAuth callback rendering.
- **First‑time experience** – Automatic theme detection and setup dialog (merged) reduce onboarding friction.
- **UI/UX polish** – Smarter session sorting, model name refresh, vim‑like modal editor (merged prototype), and better Markdown rendering.
- **Supply chain hardening** – Requests to pin dependencies (AWS SDK) and remove dangerous `--min-release-age=0` flag.

---

## Developer Pain Points

- **Connection reliability** – OpenAI Codex / GPT‑5.5 still leaves users with a silent hang; only Escape recovers.
- **Windows integration** – Git‑bash detection from PATH fails, and standalone `.zip` builds need improvement.
- **Dependency duplication** – Shrinkwrap causes duplicate module copies when both `pi-ai` and `pi-coding-agent` are installed.
- **Provider‑specific configuration** – Lack of `auth.json` support for extra parameters forces reliance on environment variables.
- **TUI crashes** – Long extension status text exceeds terminal width; Markdown backticks rendered raw.
- **Unexpected process hangs** – MCP servers block package commands; child processes holding stdin prevent clean exit.
- **Regressions in core UX** – Escape key interrupt broke, then fixed; spinner reappears after session switch.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-16

## Today's Highlights
The `v0.18.1` stable release shipped, bringing daemon session shell opt-in and a fix for oversized context warnings. The `/loop` command is receiving a major overhaul with multiple feature-request issues and PRs aligning its behavior (self-paced loops, task files, cancellation). A notable bug regarding model-provider disambiguation when multiple providers share the same model ID was also raised and quickly addressed in PR #5179.

## Releases
- **v0.18.1** – Stable release containing the daemon direct session shell gated behind explicit opt-in and other fixes. [View release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1)
- **v0.18.1-preview.0** – Preview including oversized context instruction warning and documentation fixes for stale defaults/CLI syntax. [View release](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.1-preview.0)
- **desktop-v0.0.4** – Desktop app update fixing MCP server removals persistence and model-derived defaults. [View release](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.0.4)

## Hot Issues
1. **#5142** – `bug(cli): Virtualized History Mode where history is not visible` – A UI regression where the input box disappears and history only shows on key press. High impact for interactive users. [Issue](https://github.com/QwenLM/qwen-code/issues/5142)
2. **#5160** – `bug(cli): /model lists discontinued qwen-oauth coder-model even when OAuth is not configured` – Confusing CLI output for non-OAuth users. [Issue](https://github.com/QwenLM/qwen-code/issues/5160)
3. **#5173** – `bug: Model provider disambiguation fails when multiple providers share the same model id` – Model selection doesn't persist across sessions when providers share IDs (e.g., `qwen3.7-max`). Already fixed in PR #5179. [Issue](https://github.com/QwenLM/qwen-code/issues/5173)
4. **#4966** – `bug: SchemaValidator missing numeric string coercion causes MCP tool failures` – MCP tools reject numeric parameters sent as strings by LLMs, causing frequent failures. [Issue](https://github.com/QwenLM/qwen-code/issues/4966)
5. **#5147** – `bug: OOM after /quit when managed auto-memory builds transcript from large text-only history` – Out-of-memory crashes even after `structuredClone` fix, linked to background auto-memory. [Issue](https://github.com/QwenLM/qwen-code/issues/5147)
6. **#5101** – `bug: Qwen Code carries repeated large tool results through provider history` – Context explosion when LLMs repeatedly request large-output commands. [Issue](https://github.com/QwenLM/qwen-code/issues/5101)
7. **#4941** – `feat: Add QWEN.md length warning that scales with model context window` – Request to warn users when context files are too large, improving performance awareness. [Issue](https://github.com/QwenLM/qwen-code/issues/4941)
8. **#5176** – `feat: allow sub-agent max parallel count setting and put the rest in queue` – Needed for resource-constrained local LLMs. [Issue](https://github.com/QwenLM/qwen-code/issues/5176)
9. **#5124** – `feat: Track /loop alignment work` – Parent issue for the multi-part /loop overhaul (self-paced loops, tick templates, cancellation). [Issue](https://github.com/QwenLM/qwen-code/issues/5124)
10. **#4939** – `feat: Let grep/egrep/fgrep satisfy the read-before-edit check` – Reduces unnecessary read calls, improving edit efficiency. [Issue](https://github.com/QwenLM/qwen-code/issues/4939)

## Key PR Progress
1. **#5094** – `feat: Workflow P4 — meta + /workflows + phase-tree` – Major step in the Dynamic Workflows port, adding meta extraction and workflow management. [PR](https://github.com/QwenLM/qwen-code/pull/5094)
2. **#4850** – `feat: interactive multi-tab /extensions manager` – Replaces flat list with Installed/Discover/Sources tabs for extension lifecycle. [PR](https://github.com/QwenLM/qwen-code/pull/4850)
3. **#4943** – `feat: add --safe-mode flag` – Disables all customizations for troubleshooting, helpful for isolating configuration issues. [PR](https://github.com/QwenLM/qwen-code/pull/4943)
4. **#5175** – `feat: web-shell mid-turn messages` – Allows interrupting a running turn with new input, improving interactive responsiveness. [PR](https://github.com/QwenLM/qwen-code/pull/5175)
5. **#5148** – `feat: align /loop command surface and add task-file reader` – First slice of /loop rework, adding task-file support and command aliases. [PR](https://github.com/QwenLM/qwen-code/pull/5148)
6. **#5179** – `fix: remember selected provider when multiple share a model id` – Quick fix for issue #5173, persisting provider selection per model. [PR](https://github.com/QwenLM/qwen-code/pull/5179)
7. **#5174** – `feat: Add daemon status API` – New read-only endpoint for monitoring daemon health (sessions, rate limits, etc.). [PR](https://github.com/QwenLM/qwen-code/pull/5174)
8. **#5171** – `fix: auto-retry transport stream errors before the first chunk` – Improves reliability for transient network failures during streaming. [PR](https://github.com/QwenLM/qwen-code/pull/5171)
9. **#5155** – `fix: make forking explicit; keep omitted subagent_type awaitable` – Clarifies subagent dispatch, preventing accidental forks. [PR](https://github.com/QwenLM/qwen-code/pull/5155)
10. **#5145** – `feat: show follow-up suggestion in input placeholder` – Displays suggested next prompt after model response, using fast model for generation. [PR](https://github.com/QwenLM/qwen-code/issues/5145)

## Feature Request Trends
- **`/loop` rework (background automation)** – Multiple issues (#5124, #5130–#5136) request self-paced loops, wakeup scheduling, task files, cancellation, and tick templates—signaling a push to make loop-based automation more flexible and resource-aware.
- **Model & provider management** – Requests for easier disambiguation of models shared across providers (#5173, #5176), and for safely handling discontinued models (#5160).
- **Context & memory optimization** – Issues like #4941 (QWEN.md length warnings), #4966 (MCP param coercion), #5101 (tool result deduplication) show developer demand for smarter context budgeting.
- **Enhanced terminal/interactive UX** – Better scroll handling (#5159), virtualized history fixes (#5142), and in-place suggestion display (#5145) reflect a desire for polished terminal interactions.

## Developer Pain Points
- **OOM and memory leaks** – #5147 (OOM after `/quit` with large history) and #5101 (context bloat from repeated tool results) remain recurring pain points, especially with local LLMs.
- **Provider confusion** – Multiple providers using the same model ID causes session persistence issues (#5173); also the discontinued OAuth model appearing in selection lists confuses users (#5160).
- **MCP tool parameter validation** – Schema errors when LLMs send numeric params as strings (#4966) waste turns and frustrate users.
- **Terminal input interference** – Trackpad scroll history navigation in tmux (#5159), and flash screen in Ghostty after plan mode (#3979) degrade the interactive experience.
- **Configuration isolation** – Users need a clean way to troubleshoot without customizations (#4943).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-16

## Today's Highlights

No new releases were cut in the last 24 hours, but the repo saw heavy triage activity with several long-standing issues updated. The most active discussion surrounds a persistent `Turn stalled` error (#2487) that freezes YOLO mode and requires manual intervention. Meanwhile, the maintainer closed the v0.8.59 release tracker (#3063) after shipping the mouse-report input leak fix and resolved several sub-agent reliability issues (#2029, #2058, #2211). New feature requests emerged around provider registry integration (#3192), skill scanning scoping (#3264), and moonshot API compatibility (#3265).

## Releases

None in the last 24 hours. The latest stable release is v0.8.61 (inferred from issue labels). The v0.8.62 release is in progress with active PRs and tracking issues.

## Hot Issues

1. [#2487 – `Turn stalled` error in YOLO mode](Hmbown/CodeWhale Issue #2487)  
   **Open, 13 comments.** Users report that sending `continue` after a stall does not resume operation. The community suspects a race condition in the completion signal dispatch. This is the highest-commented issue.

2. [#3063 – v0.8.59 release tracker](Hmbown/CodeWhale Issue #3063)  
   **Closed, 11 comments.** This tracker captured the TUI mouse-report input leak fix (macOS) and the triage queue before shipping v0.8.59. A model for future release management.

3. [#1186 – Typed persistent permission rules](Hmbown/CodeWhale Issue #1186)  
   **Open, 9 comments.** A long-standing enhancement to add `allow`/`deny`/`ask` rules scoped by tool, command prefix, and path. Foundation for safer sub-agent execution.

4. [#3192 – Agent Client Protocol registry](Hmbown/CodeWhale Issue #3192)  
   **Open, 6 comments.** Being listed in the ACP registry would allow tools like Zed to install DeepSeek TUI as an agent, broadening the ecosystem. High interest from the community.

5. [#1812 – TUI freeze on Windows (crossterm-poll)](Hmbown/CodeWhale Issue #1812)  
   **Open, 6 comments.** Intermittent full UI hangs on Windows 11 with detailed thread‑state analysis. A critical reliability issue for Windows users.

6. [#2574 – Provider fallback chain](Hmbown/CodeWhale Issue #2574)  
   **Open, 4 comments.** Automatic fallback when a provider returns 401/429/5xx. Configurable via `fallback_providers` in `config.toml`. Needed for production setups.

7. [#2629 – 401 error with SiliconFlow / TokenHub](Hmbown/CodeWhale Issue #2629)  
   **Open, 4 comments.** Users on Windows 11 cannot use these OpenAI‑compatible backends. Likely a header or endpoint format mismatch.

8. [#3102 – First‑class clarification questions](Hmbown/CodeWhale Issue #3102)  
   **Open, 4 comments.** Agents currently emit messages to ask questions – a modal UI would be much clearer. Part of v0.8.62 planning.

9. [#3264 – Restrict skill scanning to `~/.codewhale/skills/`](Hmbown/CodeWhale Issue #3264)  
   **Open, 2 comments. NEW.** Users want to limit skill discovery to avoid scanning unrelated directories. Simple config toggle requested.

10. [#3265 – Moonshot/Kimi API requires `parameters.type = "object"`](Hmbown/CodeWhale Issue #3265)  
    **Open, 1 comment. NEW.** Every request fails with HTTP 400 because tool definitions lack the required `type` field. Pending fix for v0.8.60+.

## Key PR Progress

1. [#3005 – Refactor provider metadata into data‑driven registry](Hmbown/CodeWhale PR #3005)  
   **Closed.** Extracts ~100 hand-maintained match arms into a static `PROVIDER_REGISTRY`. Improves maintainability and eases adding new providers.

2. [#3244 – Retry release lookups and downloads](Hmbown/CodeWhale PR #3244)  
   **Closed.** Adds retry logic for transient GitHub API failures during `codewhale update`, with a fallback to deterministic asset URL construction.

3. [#3241 – Accept `$skill‑name` aliases in composer](Hmbown/CodeWhale PR #3241)  
   **Closed.** Allows activating skills via `$skill-name` syntax alongside `/skill`. Backward‑compatible, improves discoverability.

4. [#3235 – Add DeepInfra provider support](Hmbown/CodeWhale PR #3235)  
   **Closed.** Enables use of DeepInfra’s OpenAI‑compatible API with 100+ models including DeepSeek V4.

5. [#3233 – Persist ask‑only permission rules atomically](Hmbown/CodeWhale PR #3233)  
   **Closed.** Foundation for the persistent permission system (#1186). Adds `ConfigStore::append_ask_rules` without changing approval semantics.

6. [#3206 – WeChat bridge via Feishu + Tencent OpenClaw](Hmbown/CodeWhale PR #3206)  
   **Closed.** Community contribution to run CodeWhale from WeChat using the existing Feishu Bridge infrastructure.

7. [#3257 – Make app‑server the canonical runtime API entrypoint](Hmbown/CodeWhale PR #3257)  
   **Closed.** Delegates `codewhale app-server --http/--mobile` to the existing serve runtime, preserving legacy behavior. Adds smoke tests.

8. [#3242 – Add `workspace_follow_symlinks` setting](Hmbown/CodeWhale PR #3242)  
   **Open.** Allows tool operations to follow symbolic links during directory traversal. Useful for projects with linked files.

9. [#3239 – Documentation for Atlas Cloud as OpenAI‑compatible backend](Hmbown/CodeWhale PR #3239)  
   **Open.** Docs‑only PR adding a provider section for Atlas Cloud (59 models). Quick‑start and `.env.example` included.

10. [#2239 – i18n Phase 1–4b wiring + rebase fixes](Hmbown/CodeWhale PR #2239)  
    **Open.** Massive PR (47 files) that wires MessageId translations into the UI layer, fixing 109 compile errors from the rebase. Community‑driven.

## Feature Request Trends

- **Provider resilience**: Multiple requests for automatic fallback chains (#2574), dynamic API key fetching (#3004), and broader provider compatibility (SiliconFlow, TokenHub, DeepInfra, Atlas Cloud).  
- **Permission & safety**: Persistent typed permission rules (#1186), sub-agent permission inheritance (#414), and skill scanning scoping (#3264) show a growing focus on secure agent execution.  
- **UI/UX improvements**: Clarification question modals (#3102), TUI freeze fixes (#1812), word wrap (#963), and mid‑turn intervention (#874). The community wants a more polished terminal experience.  
- **Ecosystem integration**: Agent Client Protocol registry (#3192), WeChat bridge (#3206), and i18n (#2239) aim to make CodeWhale usable from more platforms and locales.  

## Developer Pain Points

- **Sub‑agent reliability** is the top frustration: timeouts (120s ceiling, #1806), SSE multi‑agent hangs (#1679), and incomplete output clipping (#2652). Many users report tasks freezing and requiring a restart.  
- **Cross‑platform stability** remains a concern: Windows TUI freezes (#1812), glibc incompatibility on older Linux (#1067), and occasional macOS mouse‑input leaks (now fixed in #3063).  
- **Error handling gaps** – the “Turn stalled” error (#2487) and “401 invalid api key” (#2629) are frequently reported but not yet resolved. Users also struggle with synchronous tools blocking cancellation (#1791).  
- **Configuration friction**: API keys stored in plaintext (#3004), no dynamic fallback, and tool parameter strictness (moonshot #3265) add setup overhead.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*