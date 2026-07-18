# AI CLI Tools Community Digest 2026-07-18

> Generated: 2026-07-18 01:49 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report — 2026-07-18

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with all seven major tools shipping security patches, reliability fixes, and new capabilities within a single 24-hour window. A clear pattern emerges: the ecosystem is converging on multi-agent workflows, enterprise access controls, and Windows platform parity as the dominant engineering priorities. However, each tool also reveals distinct architectural philosophies—Claude Code prioritizes collaborative workspaces and permission modeling, OpenAI Codex pushes toward IDE-level intelligence via LSP integration, and Gemini CLI invests in sandbox security and AST-aware analysis. The gap between immature but fast-moving projects (Qwen Code, Pi) and established platforms (Claude Code, Copilot CLI) is narrowing as all tools grapple with similar scaling challenges around agent hang detection, memory management, and cross-platform consistency.

## 2. Activity Comparison

| Tool | Issues Updated (Last 24h) | PRs Updated (Last 24h) | Release Status |
|------|--------------------------|----------------------|----------------|
| **Claude Code** | 10 hot issues (46 total mentioned) | 10 PRs | v2.1.214 (security fixes) |
| **OpenAI Codex** | 10 hot issues | 10 PRs | 3 Rust alpha builds (v0.145.0-alpha.*) |
| **Gemini CLI** | 10 hot issues | 10 PRs | v0.52.0-nightly (triage orchestrator, sandbox) |
| **Copilot CLI** | 10 hot issues | 0 PRs in 24h | v1.0.72-1 (plugin flags) |
| **Kimi Code CLI** | 3 issues updated | 1 PR | No release |
| **OpenCode** | 50+ issues, 50+ PRs | 10 key PRs | No release |
| **Pi** | 10 hot issues | 10 key PRs | No release |
| **Qwen Code** | 10 hot issues | 10 key PRs | v0.19.11-nightly |
| **DeepSeek TUI** | 10 hot issues | 10 key PRs | No release |

**Key observations:**
- OpenCode dominates raw activity volume (50+ issues and PRs each), reflecting rapid iteration on its v2.0 UI and agent infrastructure.
- Claude Code and OpenAI Codex show the highest issue engagement (76-comment billing bugs, 426-vote LSP requests), indicating large, vocal user bases.
- Copilot CLI had zero PR activity in 24h despite four Windows-specific bugs—suggests slower maintenance cadence.
- Kimi Code CLI is the quietest, with only 3 issues and 1 PR updated.

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities, signaling broad developer demand:

**Windows Reliability & Platform Parity**
- *Claude Code:* PowerShell permission bypass fixed (#214); Cowork fails on ARM64 (#50674)
- *OpenAI Codex:* HID enumeration hang (#33780), control tab missing (#28919), repeated crash (#33438)
- *Copilot CLI:* Plugin install access denied (#4151), interactive mode blank (#4159), resume hang (#4165)
- *Pi:* No Windows-specific bugs today, but high process-leak concern
- *Qwen Code:* Ctrl+C behavior in PyCharm (#4586), stuck permission dialog (#6992)
- *DeepSeek TUI:* ConPTY resource leaks (#4100), hook process leaks (#4489), rendering glitch (#4479)

**Subagent / Multi-Agent Hang Detection & Recovery**
- *Claude Code:* Auto-mode classifier fail-closed (#74949)
- *OpenAI Codex:* wait_agent ignoring timeout (#24951)
- *Gemini CLI:* Generalist agent hangs (#21409), shell stuck on "Waiting input" (#25166)
- *Copilot CLI:* Zombie process accumulation (#4163)
- *OpenCode:* Subagents hang after bash call (#33028), infinite compaction loop (#27924)
- *Pi:* Memory blowup from tool partial updates (#6755)
- *DeepSeek TUI:* Agent autonomy violations (#4032, #3275)

**Security & Permission Model Hardening**
- *Claude Code:* Directory glob bypass (#214), YAML/path/symlink hardening (PR #76581)
- *Gemini CLI:* Bash variable expansion bypass (PR #28403), TOCTOU race on auth tokens (PR #28330)
- *Copilot CLI:* Permission misclassification (read-only falsely blocked, destructive allowed, #4156, #4160)
- *Qwen Code:* Shell safety classification (PR #7053)
- *Pi:* Orphaned tool_use blocks causing 400 errors (#6761)

**Multi-Workspace & Remote/SSH Connectivity**
- *Claude Code:* Cowork folder management (#40043)
- *OpenCode:* SSH remote server support (#7790)
- *Qwen Code:* Multi-workspace daemon RFC (#6378)
- *Copilot CLI:* Multi-root workspace support (#1826)
- *DeepSeek TUI:* SSH sandbox failure (#1829)

**TUI & Keyboard UX Customization**
- *Claude Code:* Left-arrow agents navigation conflict (#75899), request for rebindable keys
- *Copilot CLI:* vi-style j/k navigation (#4152), text selection (#4154)
- *Qwen Code:* Ctrl+S diff garbled (#6809), Ctrl+C unexpected exit (#4586)
- *Kimi Code CLI:* Markdown list word-splitting (#2379)
- *DeepSeek TUI:* Vim Normal mode space conflict (PR #4477)

**Enterprise OAuth / SSO Compatibility**
- *Claude Code:* Azure AD/Entra ID exclusion (#26675, 31 👍)
- *Copilot CLI:* Custom headers for BYOK (#3399)
- *DeepSeek TUI:* Kimi OAuth device login (#4417), xAI OAuth fix (PR #4505)

**Memory & Performance Under Load**
- *Claude Code:* macOS kernel zone leak (#66020), ugrep OOMs (#67021)
- *Pi:* TUI 100% CPU (#6665), multi-GB RSS (#6755)
- *OpenCode:* Infinite compaction loop (#27924)
- *Qwen Code:* Cold start latency (#4748)
- *Gemini CLI:* 400-tool context limit (#24246), random tmp scripts (#23571)

## 4. Differentiation Analysis

| Tool | Core Differentiation | Target User | Technical Approach |
|------|--------------------|-------------|-------------------|
| **Claude Code** | Cowork collaborative workspaces, hook/plugin ecosystem | Enterprise teams | Permission-matrix agent model, durable session persistence |
| **OpenAI Codex** | LSP-first intelligence, multimodal (audio, inline vis) | Developer power users | Multi-agent orchestration with reasoning model integration |
| **Gemini CLI** | Security sandboxing (Seatbelt profiles), AST-aware analysis | Security-conscious developers | Zero-dependency sandbox, deny-default macOS model |
| **Copilot CLI** | GitHub-native workflow, voice mode, BYOK flexibility | GitHub ecosystem users | Plugin mutation flags, simple permission heuristics |
| **Kimi Code CLI** | Chinese-market focus, OAuth-driven, lightweight TUI | Asian developer audience | Minimal dependencies, Moonshot ecosystem integration |
| **OpenCode** | Extreme extensibility (plugins, model providers), V2 UI | Power users, plugin developers | Subagent depth controls, LiteLLM provider, session blobs |
| **Pi** | Lightweight, personal agent with managed multi-agent vision | Individual developers | Compaction/branch summarization, 15-turn recursive limit |
| **Qwen Code** | Daemon multi-workspace, Web Shell Git integration | Server-side / CI users | Cold-start observability, Fleet Shepherd CI automation |
| **DeepSeek TUI** | Android/Termux support, multi-provider OAuth, open-source clone | Mobile-first, Linux CLI users | Blocking pool auth, platform-specific PTY handling |

**Strategic distinctions:**
- **Security posture:** Gemini CLI is the only tool with a deny-default macOS sandbox model. Claude Code and Copilot CLI show permission bypass regressions, indicating less mature security CI.
- **Platform strategy:** DeepSeek TUI and Qwen Code are the only tools actively targeting mobile/ARM64. Claude Code and OpenAI Codex struggle on Windows-on-ARM.
- **Extensibility philosophy:** OpenCode embraces a plugin marketplace and BYOK model providers; Claude Code and Copilot CLI have plugin systems but with tighter governance.
- **Collaboration:** Claude Code's Cowork feature is unique—no other tool offers persistent shared workspaces with permission scoping.
- **Observability:** OpenAI Codex and Qwen Code are investing in session replay and telemetry; Pi adds usage metadata to compaction events.

## 5. Community Momentum & Maturity

**High momentum, rapid iteration:**
- **OpenCode** leads in raw throughput (50+ issues/PRs daily), driven by v2.0 UI migration and agent infrastructure work. High engagement on model discovery and SSH features suggests strong growth trajectory.
- **Qwen Code** is building infrastructure rapidly: Fleet Shepherd CI, Web Shell Git integration, and multi-workspace daemon RFCs signal a project scaling from experimental to production.
- **DeepSeek TUI** has a dedicated community (35-comment autonomy debates, Termux epic), but maturity is limited by Windows reliability gaps.

**Established, large user bases:**
- **Claude Code** has the highest issue engagement (76-comment billing bug, 25+ upvotes on critical bugs). The volume of platform-specific issues (ARM64, Windows 11 Pro) indicates broad adoption but uneven QA.
- **OpenAI Codex** is the most-requested tool for a single feature (LSP integration, 426 👍). Alpha Rust releases suggest active inner-source development, but community wait times are high.
- **Copilot CLI** has reduced PR velocity but steady issue volume. Windows-specific failures (4 issues today) suggest testing gaps in Windows 11.

**Stable but slower iteration:**
- **Pi** has a focused, technically engaged community (performance bugs, provider expansion). No releases but 10 PRs today signals steady maintenance.
- **Kimi Code CLI** is the quietest. Only 3 issues and 1 PR updated—may reflect smaller user base or slower development cycle.

## 6. Trend Signals

1. **The "agent trust" crisis.** Every tool reports users frustrated by agent autonomy violations: writing scripts without approval, entering self-questioning loops, misreporting failure as success (Gemini CLI #22323), and ignoring user-provided inputs (DeepSeek TUI #4032). The industry is converging on the need for transparent turn budgets, fail-closed safety overrides, and clear agent intent signals. This is the defining UX challenge of 2026 for AI CLI tools.

2. **Terminal → IDE convergence stalls.** Despite OpenAI Codex's 426-vote LSP request, only Codex has a clear roadmap for terminal-to-IDE integration. Claude Code's VSCode extension has prompt contamination bugs. Copilot CLI ignores multi-root workspaces. The promise of CLI tools that match IDE intelligence remains unfulfilled—developers are demanding it, but no tool has delivered.

3. **Windows is the frontier battleground.** Every tool except Pi has at least two open Windows-specific bugs. ConPTY resource leaks, HID enumeration deadlocks, plugin installation failures, and permission dialog hangs dominate bug trackers. The tool that first achieves Windows parity at scale will win a large captive audience.

4. **Mobile/ARM64 is the next wave.** DeepSeek TUI's Termux epic and Claude Code's Snapdragon X Cowork failure signal emerging demand for ARM64-native CLI agents. Qwen Code's multi-workspace daemon suggests server-side ARM deployments. This will accelerate as Apple Silicon and Windows-on-ARM penetrate developer hardware.

5. **Security hardening is reactive, not proactive.** Three permission bypasses (Claude Code v2.1.214), one TOCTOU race (Gemini CLI PR #28330), and one variable expansion bypass (Gemini CLI PR #28403) were patched this week alone. The pace of vulnerability discovery suggests the agent execution model—subagents spawning shell commands, writing scripts, accessing network—is inherently risky and requires architectural sandboxing, not just prompt engineering.

6. **Multi-agent orchestration remains unsolved.** No tool has a production-grade solution for reliable agent lifecycle management: hang detection, recovery, session isolation, and completion notification. Claude Code, OpenAI Codex, and Gemini CLI all have open bugs in this space. Pi's "managed agents" PRD (#6785) and OpenCode's subagent_depth config suggest this is the next major feature frontier.

**Recommendation for evaluators:** If you need collaborative workspaces with permission controls, prioritize Claude Code. If terminal IDE intelligence matters, watch OpenAI Codex's LSP work. If security is paramount, Gemini CLI's sandbox model leads. For mobile/Linux-first workflows, DeepSeek TUI's Android support is unique. All tools share the same growing pains: Windows reliability, agent trust, and memory stability under load.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills | July 18, 2026

---

## 1. Top Skills Ranking

Most-discussed pull requests by community engagement, ranked by comment volume and cross-referenced issues.

### #1298 — fix(skill-creator): run_eval.py always reports 0% recall
**Skill:** Core skill-creator infrastructure (eval/optimization loop)  
**Author:** MartinCajiao | **Status:** Open | **Created:** 2026-06-10  
**Link:** https://github.com/anthropics/skills/pull/1298

This PR addresses a critical systemic bug where `run_eval.py` reports `recall=0%` for every skill description, making the entire description-optimization pipeline optimize against noise. The fix installs the eval artifact as a real skill, resolves Windows stream-reading issues, corrects trigger detection logic, and fixes parallel worker behavior. This is the highest-engagement PR in the repository and directly resolves issues #556 (12 comments, 7 👍) and #1169 (3 comments). The community has independently reproduced the bug 10+ times.

---

### #514 — Add document-typography skill
**Skill:** Typographic quality control for AI-generated documents  
**Author:** PGTBoos | **Status:** Open | **Created:** 2026-03-04  
**Link:** https://github.com/anthropics/skills/pull/514

Prevents orphan word wrap (1–6 words on new lines), widow paragraphs (headers stranded at page bottom), and numbering misalignment in Claude-generated documents. The discussion centers on whether these issues are universal across models and whether the skill should be a default dependency for document-generation workflows. High interest from documentation-heavy users.

---

### #538 — fix(pdf): correct case-sensitive file references in SKILL.md
**Skill:** PDF skill (file reference correction)  
**Author:** Lubrsy706 | **Status:** Open | **Created:** 2026-03-06  
**Link:** https://github.com/anthropics/skills/pull/538

Fixes 8 case-sensitivity mismatches between SKILL.md references (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`) that break on case-sensitive filesystems (Linux/macOS). Discussion highlights that this represents a broader testing gap—skills are primarily developed on Windows/WSL and not validated on native Linux. Related to issue #189 (duplicate skills from overlapping plugins).

---

### #486 — Add ODT skill (OpenDocument text creation, template filling, parse ODT to HTML)
**Skill:** OpenDocument format (.odt/.ods) creation and conversion  
**Author:** GitHubNewbie0 | **Status:** Open | **Created:** 2026-03-01  
**Link:** https://github.com/anthropics/skills/pull/486

Covers full ODT/ODS workflow: creation, template filling, and HTML conversion. Community discussion focuses on whether this should interoperate with the existing DOCX skill or remain standalone, and whether LibreOffice is a required runtime dependency. Strong interest from enterprise and EU public-sector users where ODF is mandated.

---

### #210 — Improve frontend-design skill clarity and actionability
**Skill:** Frontend design guidance  
**Author:** justinwetch | **Status:** Open | **Created:** 2026-01-05  
**Link:** https://github.com/anthropics/skills/pull/210

A comprehensive revision to ensure every instruction is actionable within a single conversation. Discussion praises the structural clarity but raises concerns about bloat—whether 50+ specific instructions fit within Claude's instruction window. Active debate about skill design philosophy: exhaustive vs. minimal.

---

### #83 — Add skill-quality-analyzer and skill-security-analyzer to marketplace
**Skill:** Meta-skills for quality and security analysis of other skills  
**Author:** eovidiu | **Status:** Open | **Created:** 2025-11-06  
**Link:** https://github.com/anthropics/skills/pull/83

Two meta-skills: `skill-quality-analyzer` evaluates structure, documentation, examples, performance, and portability (5 dimensions, weighted scoring); `skill-security-analyzer` reviews code execution, file access, API keys, prompt injection, and dependency risks. Discussion is deeply intertwined with issue #492 (security namespace concerns)—several commenters note these meta-skills should be official Anthropic offerings, not community-contributed, to maintain trust boundaries.

---

### #541 — fix(docx): prevent tracked change w:id collision with existing bookmarks
**Skill:** DOCX skill (document corruption fix)  
**Author:** Lubrsy706 | **Status:** Open | **Created:** 2026-03-06  
**Link:** https://github.com/anthropics/skills/pull/541

Fixes document corruption when tracked changes are applied to documents with existing bookmarks by avoiding hardcoded low IDs in OOXML's shared `w:id` space. Discussion reveals this is a known OOXML specification footgun and calls for a general-purpose OOXML ID management utility skill.

---

### #539 — fix(skill-creator): warn on unquoted description with YAML special characters
**Skill:** skill-creator validation  
**Author:** Lubrsy706 | **Status:** Open | **Created:** 2026-03-06  
**Link:** https://github.com/anthropics/skills/pull/539

Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing `:`, which silently truncates YAML parsing. Companion to PR #361 by Mr-Neutr0n which extends detection to `: # { } [ ]`. Discussion notes this is a frequent contributor pain point—new skill authors routinely hit this on first submission.

---

## 2. Community Demand Trends

From the most-discussed Issues (sorted by comments + 👍 reactions), five clear demand vectors emerge:

### Security & Trust Boundary (Issue #492 — 34 comments, 2 👍)
The dominant concern: community skills distributed under the `anthropic/` GitHub namespace create an illusion of official endorsement. Users may grant elevated permissions (file access, API keys) to skills they believe are Anthropic-vetted. **Demand:** Official signing/verification system for skills, or a clear namespace separation (e.g., `anthropic/skills-official` vs. `community/skills`).

### Enterprise Collaboration (Issue #228 — 14 comments, 7 👍)
Organizations cannot share skills internally without manual file transfer. **Demand:** Org-wide skill library with sharing links, role-based access control, and centralized management in Claude.ai.

### Reliability & Testing (Issues #556, #1169, #1061 — cumulative 18 comments, 10 👍)
The skill-creator's evaluation pipeline is fundamentally broken on Windows and produces false negatives on all platforms. **Demand:** A reliable, cross-platform evaluation framework before the skill marketplace scales further. Contributors are frustrated that optimization is optimizing against noise.

### Agent Memory & State Management (Issue #1329 — 9 comments)
Long-running agents waste context on verbose prose notes. **Demand:** A `compact-memory` skill using symbolic notation for agent state—structured key-value stores, timestamps, and priority markers instead of natural language journaling.

### Agent Governance (Issue #412 — 6 comments)
Proposal for safety patterns: policy enforcement, threat detection, trust scoring, audit trails. **Demand:** Extension of the security meta-skill concept into operational guardrails for agent systems.

---

## 3. High-Potential Pending Skills

These open PRs have sustained community engagement and appear technically complete or close to merge:

| PR | Skill | Author | Created | Notes |
|----|-------|--------|---------|-------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | run_eval.py 0% recall fix | MartinCajiao | 2026-06-10 | Critical blocker for skill optimization; 10+ independent reproductions |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | PGTBoos | 2026-03-04 | Mature, well-scoped, no unresolved technical objections |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT skill | GitHubNewbie0 | 2026-03-01 | Comprehensive; waiting on OOXML ID management decision |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 4444J99 | 2026-03-22 | Full testing stack (unit, React, integration, e2e, a11y) |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel (retro game engine) | kitao | 2026-03-05 | From original Pyxel author; game dev use case |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit (reasoning quality gate) | YuhaoLin2005 | 2026-06-28 | Mechanical verification + 4-dimension reasoning audit |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert | meodai | 2026-06-10 | Comprehensive color naming/systems; low controversy |

**Notable meta-observation:** PRs #362 and #361 (both by Mr-Neutr0n, same dates) are closely related skill-creator fixes covering UTF-8 byte-length validation and YAML special character detection. They are likely to be merged together or superseded by the more recent #539/#1298 work.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill evaluation infrastructure and trust-boundary security, followed by practical content-creation skills (typography, ODF) and governance patterns for agentic systems.**

---

# Claude Code Community Digest — 2026-07-18

## Today's Highlights

Version 2.1.214 ships with two security-critical fixes: a directory glob bypass in permission rules and a PowerShell permission-check bypass on Windows. Meanwhile, the community continues to surface persistent issues around Cowork platform restrictions, memory exhaustion bugs (kernel zone leaks and ugrep OOMs), and OAuth compatibility gaps with enterprise identity providers. A cluster of recent bugs around the auto-mode classifier and session reliability suggests infrastructure pressure as adoption scales.

---

## Releases

**v2.1.214** — [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.214)

- **Fixed:** Single-segment `dir/**` allow rules (e.g., `Edit(src/**)`) no longer auto-approve writes to nested `dir/` directories outside `<cwd>/dir` — closes a permission-boundary bypass.
- **Fixed:** Permission-check bypass affecting commands run in Windows PowerShell 5.1 sessions.
- **Fixed:** Bash permission issue (details truncated in source data).

---

## Hot Issues

1. **[#55982 — Plan upgrade payment fails with PaymentIntent voided immediately](https://github.com/anthropics/claude-code/issues/55982)**  
   *76 comments, 25 👍* — A billing-critical bug: the payment flow cancels the PaymentIntent (`void_invoice`) before confirmation completes. Two months open with high engagement suggests this blocks paid tier upgrades for a significant number of users. No fix commit linked yet.

2. **[#50674 — Cowork fails on ARM64 (Snapdragon X) despite passing readiness check](https://github.com/anthropics/claude-code/issues/50674)**  
   *40 comments* — A platform-specific regression: Cowork readiness checks pass on Snapdragon X hardware, but the feature silently fails at runtime. Impacts the growing Windows-on-ARM user base.

3. **[#47327 — Cowork tab disabled: "unsupported" on Windows 11 Pro x64](https://github.com/anthropics/claude-code/issues/47327)**  
   *21 comments, 3 👍* — Ongoing since March: the Cowork feature is gated on Windows 11 for many users despite meeting documented requirements. The `yukonSilver` string in the error suggests a hardware/capability detection issue.

4. **[#66020 — macOS kernel zone leak from Claude Code CLI panics at ~20 GB](https://github.com/anthropics/claude-code/issues/66020)**  
   *16 comments, 2 👍* — A `data.kalloc.1024` kernel zone leak that scales from 21 to 1,027 allocations/second with agent load, causing kernel panics. This is a serious system-level stability bug for heavy agent users on macOS 26.5.1.

5. **[#40043 — Allow removal of local folders from a Cowork project's context](https://github.com/anthropics/claude-code/issues/40043)**  
   *19 comments, **56 👍*** — The most upvoted open feature request. Cowork projects accumulate local folder references with no way to remove them. The high vote count indicates this is a UX friction point for teams using shared workspaces.

6. **[#26675 — Support pre-configured OAuth client credentials without Dynamic Client Registration](https://github.com/anthropics/claude-code/issues/26675)**  
   *17 comments, 31 👍* — Enterprise users cannot use Azure AD/Entra ID with Claude Code's MCP client because DCR is mandatory even when a `clientId` is pre-configured. This is a blocker for enterprise adoption.

7. **[#74949 — Auto-mode classifier 'temporarily unavailable' in bursts — fail-closed blocks Bash work](https://github.com/anthropics/claude-code/issues/74949)**  
   *6 comments, 3 👍* — Recurring bursts of classifier unavailability fail-closed, blocking all compound bash commands (pipes, `&&`, redirects) during peak windows. Compound commands always require classification, so a backend outage halts all shell work.

8. **[#75899 — Left arrow accidentally navigates to agents screen, not rebindable](https://github.com/anthropics/claude-code/issues/75899)**  
   *7 comments, 9 👍* — A TUI keybinding conflict: the left arrow navigates to the agents/background-tasks screen even when the chat input is focused, and the binding cannot be remapped. Returning from the agents screen breaks the main session view.

9. **[#77327 — VSCode extension injects non-interactive system prompts into interactive sessions](https://github.com/anthropics/claude-code/issues/77327)**  
   *7 comments, 1 👍* — A prompt integrity bug: system prompts designed for non-interactive (agentic) flows leak into interactive chat sessions in the VSCode extension, potentially altering model behavior unexpectedly.

10. **[#66504 — Session URL appended to commit messages and PR descriptions by default](https://github.com/anthropics/claude-code/issues/66504)**  
    *8 comments, **33 👍*** — Every commit and PR auto-includes a session URL. The author argues this should be opt-in rather than default, citing noise in git history. High upvote ratio suggests broad agreement.

---

## Key PR Progress

1. **[#78715 — feat(hookify): add regex_not_match / not_regex_match operator](https://github.com/anthropics/claude-code/pull/78715)**  
   *New, open* — Adds a missing operator to the hookify rule engine. Currently, rules can match regex patterns but cannot explicitly reject them; unknown operators silently pass. This PR closes that gap with `regex_not_match` and `not_regex_match`.

2. **[#29460 — Improve oncall triage recency and engagement criteria](https://github.com/anthropics/claude-code/pull/29460)**  
   *Closed* — Updates the oncall triage CI command to sort issues by engagement recency, not just update timestamp. Addresses a known blind spot where stale-but-active threads were missed.

3. **[#78532 — gateway/gcp: optional internal ALB + PG16 Cloud SQL edition fix](https://github.com/anthropics/claude-code/pull/78532)**  
   *Open* — Fixes a `terraform apply` failure on PG16 instances (API now defaults to ENTERPRISE_PLUS, which rejects shared-core tiers). Adds optional internal ALB support for GCP gateway deployments.

4. **[#76581 — fix(plugins): harden YAML, path, and symlink handling in scripts](https://github.com/anthropics/claude-code/pull/76581)**  
   *Open* — Security hardening: prevents YAML frontmatter breakout, path traversal, and symlink-based credential overwrite in official plugin scripts. Focuses on `ralph-wiggum` setup and similar patterns.

5. **[#78446 — fix(plugin-dev): add the missing .claude-plugin/plugin.json manifest](https://github.com/anthropics/claude-code/pull/78446)**  
   *Open* — The `plugin-dev` example plugin was the only one of 13 in the repo missing its manifest. This PR fixes the inconsistency.

6. **[#78445 — docs: correct plugin descriptions that contradict actual behavior](https://github.com/anthropics/claude-code/pull/78445)**  
   *Open* — Three metadata inaccuracies in plugin README and marketplace, including wrong hook event for `security-guidance` and incorrect pattern count. Verified against source.

7. **[#78441 — fix(devcontainer script): detect native command failures via $LASTEXITCODE](https://github.com/anthropics/claude-code/pull/78441)**  
   *Open* — PowerShell bug: `try/catch` blocks never fire for native executable failures because PowerShell doesn't raise terminating errors on non-zero exit codes. Fix replaces `try/catch` with manual `$LASTEXITCODE` checks.

8. **[#78425 — fix(code-review): require explicit user invocation](https://github.com/anthropics/claude-code/pull/78425)**  
   *Open* — Marks `/code-review` as manual-only to prevent subagents from re-entering the full multi-agent review workflow. Preserves explicit user invocation while blocking programmatic re-entry.

9. **[#77427 — fix(pr-review-toolkit): make code-reviewer a leaf agent](https://github.com/anthropics/claude-code/pull/77427)**  
   *Open* — Restricts the `pr-review-toolkit` code reviewer to repository-inspection tools only, preventing it from invoking additional agents or review workflows. Documents the reviewer as a leaf agent.

10. **[#78371 — Harden ralph-wiggum plugin: bounded iterations, push/publish guard, stop-hook fixes](https://github.com/anthropics/claude-code/pull/78371)**  
    *Open* — Safety hardening: adds bounded iteration limits, guards against unattended push/publish/deploy actions, and fixes stop-hook behavior. Keeps the plugin available for local experimentation while reducing risk.

---

## Feature Request Trends

**1. Cowork workspace management (#40043, #47327, #50674)**  
The most consistent theme. Users want folder-level control in Cowork contexts (removing local folders, not just scoping them) and consistent platform support (ARM64 Windows, Windows 11 Pro detection fixes). The persistence of these issues since March suggests architectural complexity in the Cowork permission model.

**2. Enterprise OAuth / SSO compatibility (#26675)**  
A clear enterprise blocker: Claude Code's MCP client enforces Dynamic Client Registration, making it incompatible with Azure AD/Entra ID and similar OAuth providers that expect pre-configured clients. Users want `clientId`-based flows without DCR. High upvote ratio (31 👍 on 17 comments) suggests a small but passionate enterprise cohort.

**3. Session and commit UX control (#66504)**  
Users want opt-in (not default) session URL injection into git commit messages and PR descriptions. The 33 👍 on 8 comments indicates broad agreement.

**4. Configurable keybindings in TUI (#75899, #78110)**  
Multiple issues ask for remappable keys and control over autocomplete behavior. The left-arrow agents navigation bug has exposed a broader desire for keybinding customization.

**5. CI/interactive prompt isolation (#77327, #78425)**  
Two threads highlight prompt contamination: non-interactive system prompts leaking into interactive chat sessions, and code-review workflows being re-entered by subagents. The PR work (#78425, #77427) shows the team is actively addressing agent boundary enforcement.

**6. UI search and text navigation (#65858, #72005)**  
Users request Ctrl+F in VSCode extension conversations and off-screen result navigation. These are smaller but persistent usability gaps.

---

## Developer Pain Points

**Memory and stability under load** — Three high-severity bugs in the last 24h alone: a macOS kernel zone leak that panics the system at ~20 GB (#66020), bundled ugrep OOMs on regex with bounded intervals (#67021, #78700 duplicate), and the auto-classifier fail-closed blocking bash work (#74949). For teams running heavy agent workloads, these create hard stability ceilings.

**Permission bypasses and security regressions** — The v2.1.214 release fixes two permission bypasses (directory glob expansion, PowerShell 5.1). Combined with ongoing reports of session misrouting (#77599) and credential overwrite vectors in plugins (#76581), this suggests the permission model is under stress from the agent-oriented feature expansion.

**Platform fragmentation** — Cowork works differently (or not at all) across ARM64 Windows, standard Windows 11, and macOS. The "unsupported" gating logic (#47327) visibly confuses users. The "protected host location" server-side persistence bug (#78547) adds another layer of platform inconsistency.

**API reliability and cost unpredictability** — The auto-mode classifier outages (#74949, #78263), mid-response connection drops (#78716), and abnormal token consumption (#78186) point to backend infrastructure issues. Users report running out of API quota in uncharacteristically small windows, which undermines trust in cost controls.

**Agent lifecycle and session isolation** — Background task completion notifications lost after process restart (#75438) and subagent replies delivered to wrong sessions (#77599) are reliability bugs that erode confidence in the agent system for production use.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-18

## Today’s Highlights

The Codex ecosystem sees rapid iteration on Rust alpha builds (v0.145.0-alpha.20–23) while the community continues to push for deeper IDE integration. A long-running LSP feature request now leads all issues with 426 👍 and 58 comments, signaling strong demand for intelligent code assistance. On the Windows side, a new wave of startup-hang and performance bugs—several with 15+ comments—indicates ongoing stability friction for desktop users.

## Releases

Three new Rust alpha releases landed in the last 24 hours:
- [`rust-v0.145.0-alpha.20`](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.20)
- [`rust-v0.145.0-alpha.22`](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.22)
- [`rust-v0.145.0-alpha.23`](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.23)

All are tagged as `Release 0.145.0-alpha.*` with no individual changelogs; likely incremental builds for internal testing.

## Hot Issues *(10 noteworthy)*

1. **[#8745 – LSP integration for Codex CLI](https://github.com/openai/codex/issues/8745)**  
   *enhancement/agent* – 426 👍, 58 comments. The single most-requested feature: auto-detect and auto-install language servers for richer diagnostics and symbol intelligence. Community interest dwarfs all other items.

2. **[#33780 – Windows app hang on HID device enumeration](https://github.com/openai/codex/issues/33780)**  
   *bug/windows* – 19 comments, 2 👍. New bug causing the main process to block forever in `HID.node→hid.dll` when a HID device is unresponsive. Likely affects all Windows users with certain peripherals.

3. **[#28919 – Missing "control other devices" tab on Windows](https://github.com/openai/codex/issues/28919)**  
   *bug/windows* – 17 comments, 23 👍. Windows users cannot enable remote device control via Settings > Connections—a feature that exists on macOS/Linux. Long-standing (since June 18).

4. **[#27915 – Linux users cannot access banked usage resets](https://github.com/openai/codex/issues/27915)**  
   *bug/rate-limits* – 17 comments, 41 👍. The new rate-limit reset mechanism is desktop-app only, locking out Linux CLI users. *Closed* after community uproar, but fix details not yet visible.

5. **[#20851 – First-class Computer Use from CLI](https://github.com/openai/codex/issues/20851)**  
   *enhancement* – 11 comments, 16 👍. Computer Use is currently app-only; developers want parity in the CLI to script GUI automation without leaving the terminal.

6. **[#28161 – Show expiration dates for usage resets](https://github.com/openai/codex/issues/28161)**  
   *enhancement/rate-limits* – 8 comments, 56 👍. Users see “2 resets available” but don’t know when each reset expires, causing confusion during heavy usage periods.

7. **[#33438 – Repeated crash and 2-3s input lag on new task](https://github.com/openai/codex/issues/33438)**  
   *bug/windows/performance* – 8 comments, 5 👍. Specific to build 26.707.9981.0 on Windows 11; opening a new task triggers `0xC06D007F` exceptions and severe lag.

8. **[#33873 – Frequent unresponsiveness after Windows update](https://github.com/openai/codex/issues/33873)**  
   *bug/windows/performance* – 6 comments, 2 👍. Multiple reports of the app freezing on Windows 10 after the latest Store release (26.715.21425). No fix yet.

9. **[#18906 – TUI: Markdown math rendering (LaTeX)](https://github.com/openai/codex/issues/18906)**  
   *enhancement/TUI* – 4 comments, 16 👍. Terminal users want inline/block LaTeX rendered correctly—currently missing from the terminal UI, a blocker for technical documentation workflows.

10. **[#24951 – Subagent wait_agent can block ~7.5h](https://github.com/openai/codex/issues/24951)**  
    *bug/subagent* – 4 comments, 0 👍. `wait_agent` and `spawn_agent` ignore timeout during runtime stalls, leading to multi-hour blocking sessions. Critical for agent orchestration reliability.

## Key PR Progress *(10 important PRs)*

1. **[#33932 – Forward audio inputs to Responses API](https://github.com/openai/codex/pull/33932)**  
   *Closed* – Serializes audio data URLs as `input_audio` content instead of dropping them. Enables voice-driven workflows in CLI/app.

2. **[#33925 – Render inline visualization links in TUI](https://github.com/openai/codex/pull/33925)**  
   *Closed* – Terminal fallback for `::codex-inline-vis` directives; users can open generated artifacts in a browser. Streamlines multimodal output.

3. **[#33926 – Fix quoted hook commands on Windows](https://github.com/openai/codex/pull/33926)**  
   *Closed* – Resolves a long-standing bug where executable paths with spaces (e.g., `C:\Program Files\...`) failed due to escaped quotes.

4. **[#33919 – Allow stable Python SDK releases](https://github.com/openai/codex/pull/33919)**  
   *Closed* – Updates release workflow to accept non-beta tags, unlocking stable `v0.144.4` for the Python SDK.

5. **[#33901 – Support ChatGPT-branded Desktop app builds](https://github.com/openai/codex/pull/33901)**  
   *Closed* – Ensures CLI discovery and TUI handoff work regardless of brand (Codex or ChatGPT) by searching for both executable names.

6. **[#33908 – Allow publishing plugins through share updates](https://github.com/openai/codex/pull/33908)**  
   *Closed* – Adds `LISTED` discoverability to plugin sharing, enabling plugin authors to publish via the share interface.

7. **[#33907 – Occurrence search for paginated threads](https://github.com/openai/codex/pull/33907)**  
   *Closed* – New app-server method `thread/searchOccurrences` for case-insensitive literal search across visible messages without replaying the entire thread.

8. **[#33903 – Route realtime V3 handoffs by response channel](https://github.com/openai/codex/pull/33903)**  
   *Closed* – Adds `codexResponseHandoffMode` to support thinking, commentary, and BEM tags routing for realtime sessions—critical for reasoning model integration.

9. **[#33895 – Add SessionEnd hooks for thread teardown](https://github.com/openai/codex/pull/33895)**  
   *Closed* – Introduces `SessionEnd` hook event for cleanup logic during archive, delete, idle unload, and graceful shutdown.

10. **[#33922 – Allow selecting path-backed agents in TUI picker](https://github.com/openai/codex/pull/33922)**  
    *Closed* – Fixes a bug where the agent picker stopped after status history, preventing selection of path-backed subagents.

## Feature Request Trends

- **Deep LSP integration** (#8745) dominates requests: auto-detect + auto-install language servers for Codex CLI. The community clearly wants Codex to behave like an intelligent IDE from the terminal.
- **Computer Use from CLI** (#20851) continues to gather steam—users want to script GUI automation without the desktop app.
- **Remote host connectivity** (#26846) and **multi-device control** (#28919) reflect demand for Codex as a distributed agent that can be controlled from any device.
- **Rate-limit transparency** (#28161, #32791) is a recurring theme: users want clear expiration dates and consistent visibility of all usage buckets across platforms.
- **Math/LaTeX rendering in TUI** (#18906) is a niche but persistent request from technical users working with formulas.

## Developer Pain Points

- **Windows stability remains the top frustration**: multiple issues report startup hangs (#33780, #33909), WMI Provider Host CPU saturation (#29499, #32562, #33776), and general unresponsiveness (#33873). The HID enumeration deadlock (#33780) is particularly alarming as it blocks the entire app.
- **Linux/macOS parity gaps**: Linux users still cannot access usage resets (#27915) and the Remote-SSH extension frequently hangs (#27597, #32385).
- **Subagent reliability**: `wait_agent` ignoring timeouts (#24951) and `remote-compaction` errors killing long-running goals (#33171) erode trust in multi-agent workflows.
- **Rate-limit confusion**: The disappearance of the 5-hour usage bucket for Pro/Plus users (#32707, #32791) and inconsistent reset availability suggest backend changes are not well communicated.
- **Text rendering bugs**: RTL/LTR mixing (#26250) and missing sidebar timestamps (#32172) are small but visible UX regressions.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-18

## Today’s Highlights

A new nightly release (v0.52.0) ships an LLM-based triage orchestrator for maintenance workflows and tightens macOS sandbox profiles toward a deny-default security model. On the bug front, a P1 issue revealing that subagent `MAX_TURNS` interruptions are misreported as `GOAL` success has drawn significant community attention, while a merged PR now limits recursive reasoning turns to 15 per request to mitigate infinite loops and prompt injection attacks.

## Releases

**v0.52.0-nightly.20260718.gacae7124b** — [Release Notes](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260718.gacae7124b)
- `feat(caretaker-triage)`: Implements an LLM triage orchestrator and its container build, enabling automated issue triage via Antigravity SDK.
- `refactor(cli)`: Updates macOS permissive Seatbelt profiles to align with the deny-default model, adding explicit allow-lists for developer workflows.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 11 comments)  
   The `codebase_investigator` subagent returns `status: "success"` even after hitting its turn limit, misleading users into believing analysis completed. A critical UX bug for multi-step tasks.

2. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing & Post-Execution Intent Routing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, 8 comments)  
   Proposes sandboxing that matches Gemini 3’s native bash capabilities while preserving security. High community interest in safer shell execution.

3. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, 7 comments)  
   An EPIC extending behavioral eval infrastructure from 76 to a broader test suite across 6 models. Foundational for quality assurance.

4. **[#22745 — Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, 7 comments)  
   Investigates whether AST-aware tools can reduce turn count and token usage by precisely targeting method bounds. Potential for significant efficiency gains.

5. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 7 comments, 8 👍)  
   The generalist agent hangs indefinitely on simple tasks like folder creation. Users report working around it by disabling subagent delegation entirely.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments)  
   Anecdotal evidence that custom skills and sub-agents are rarely invoked autonomously, even for closely related tasks. Affects customizability.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments)  
   Auto Memory can loop infinitely on sessions the extraction agent deems low-signal, wasting resources. Highlights a design gap in session state management.

8. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍)  
   Simple CLI commands hang post-execution while the UI reports “Awaiting user input.” A frequent frustration for interactive workflows.

9. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments)  
   The browser agent fails on Wayland with a terminal `GOAL` reason but no useful output. A platform-specific blocker.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 3 comments, 1 👍)  
    The model occasionally uses `git reset --force` or unsafe DB commands when safer alternatives exist. Requests safety-aware prompt refinements.

## Key PR Progress

1. **[#28345 — feat(caretaker-triage): implement LLM triage orchestrator and container build](https://github.com/google-gemini/gemini-cli/pull/28345)** (merged)  
   Core infrastructure for automated issue triage using Antigravity SDK with structured GCS logging.

2. **[#28424 — refactor(cli): align macOS permissive Seatbelt profiles with deny-default model](https://github.com/google-gemini/gemini-cli/pull/28424)** (merged)  
   Replaces permissive macOS profiles with explicit allow-lists, matching the `restrictive-*` and `strict-*` patterns.

3. **[#28429 — fix(core): mitigate infinite ReAct loops and prompt injection loops](https://github.com/google-gemini/gemini-cli/pull/28429)** (merged)  
   Implements a session-level default turn limit of 15 and enhanced loop detection. A key security and reliability fix.

4. **[#28275 — fix(core): make direct GCP telemetry exporters optional](https://github.com/google-gemini/gemini-cli/pull/28275)** (merged, fixes #27100)  
   Moves Google Cloud telemetry dependencies out of core runtime, reducing bundle size for third-party consumers.

5. **[#28164 — fix(core): limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)** (merged)  
   Adds a strict 15-turn recursive reasoning limit per request, protecting CPU and API quota from runaway loops.

6. **[#28346 — Fix trust dialog disclosure for runnable hooks](https://github.com/google-gemini/gemini-cli/pull/28346)** (open, fixes #27901)  
   Prevents the trust dialog from reporting invalid hooks as runnable commands, improving security transparency.

7. **[#28403 — fix(core): block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)** (open)  
   Hardens Bash and PowerShell substitution detection against bypasses of GHSA-wpqr-6v78-jr5g. Defense-in-depth for CI workflows.

8. **[#28240 — Fix #28227: add support for AGENTS.md out of the box](https://github.com/google-gemini/gemini-cli/pull/28240)** (merged)  
   Makes `AGENTS.md` a default context file alongside `GEMINI.md`, improving discoverability for agent definitions.

9. **[#28330 — fix(ide-companion): set token file mode atomically to close TOCTOU window](https://github.com/google-gemini/gemini-cli/pull/28330)** (open, fixes #28278)  
   Eliminates a time-of-check/time-of-use race condition where auth token files were briefly world-readable.

10. **[#28386 — fix(vscode): track activation disposables](https://github.com/google-gemini/gemini-cli/pull/28386)** (open)  
    Fixes a bug where VS Code extension disposables were not properly tracked due to comma-expression misuse.

## Feature Request Trends

- **AST-aware code analysis**: Multiple EPICs ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) call for Abstract Syntax Tree integration to improve file read precision, reduce token waste, and enable smarter codebase mapping.
- **Behavioral evaluation infrastructure**: A major push ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353), [#15300](https://github.com/google-gemini/gemini-cli/issues/15300)) seeks to expand component-level evals from 76 tests to a robust CI-gated suite across all supported models.
- **Agent self-awareness and debugging**: Requests for the CLI to understand its own mechanics ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)) and expose subagent trajectories via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) point to a desire for better transparency and debugging.
- **Subagent autonomy vs. control**: Users want sub-agents to be invoked more autonomously ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) while also retaining the ability to override behavior via `settings.json` ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)). Sprint tracking ([#20195](https://github.com/google-gemini/gemini-cli/issues/20195)) suggests this is an active development area.
- **Security sandboxing enhancements**: Beyond the immediate bash sandboxing proposal ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)), there is growing interest in policy-engine improvements, destructive behavior prevention, and safe-by-default execution patterns.

## Developer Pain Points

- **Agent hangs and indefinite stalls**: Issues [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) (generalist agent) and [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (shell command “Waiting input”) are recurring P1 bugs that block interactive sessions and erode trust.
- **Misleading success signals**: The MAX_TURNS misreporting bug ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) undermines debugging, as failed subagent runs appear successful.
- **Symlink and configuration fragility**: Agent files not recognized as symlinks ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)) and browser agent ignoring settings overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) frustrate power users who rely on flexible setups.
- **Destructive command execution**: The model occasionally runs unsafe operations (`git reset --force`, `rm -rf`) as reported in [#22672](https://github.com/google-gemini/gemini-cli/issues/22672), highlighting a gap in safety-aware prompt engineering.
- **Platform-specific regressions**: Wayland browser agent failures ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)) and terminal corruption on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)) indicate incomplete cross-platform testing.
- **Token waste and context size limits**: The 400+ tools 400 error ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), random tmp script creation ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), and `\n` escape behavior ([#22466](https://github.com/google-gemini/gemini-cli/issues/22466)) reflect underlying token management and context-window constraints.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI Community Digest — 2026-07-18

### Today’s Highlights
Yesterday’s release v1.0.72-1 brings plugin mutation flags and skill removal support. The bug tracker saw a surge of Windows‑specific issues (plugin installation, resume hangs, interactive mode blanking) and a critical regression in voice mode where all bundled ASR models return empty transcriptions. Several feature requests around permissions granularity, session state exposure, and keyboard navigation continue to gather community support.

---

### Releases
- **v1.0.72-1** – [Release](https://github.com/github/copilot-cli/releases/tag/v1.0.72-1)  
  - **Added** `--plugin`, `--mcp`, `--skill` flags for plugin mutations; `copilot plugins remove --skill` to remove a skill.  
  - **Improved** full file path reveals in compact editing rows, deterministic plan‑approval menu, and visibility of `/add-dir` directories.

---

### Hot Issues (10 picked)

1. **[#4024](./copilot-cli/issues/4024)** – **Voice mode: all bundled ASR models fail silently** (area:models)  
   Audio is recorded (level meter active), but every transcription comes back empty for all three offered models. Community has 12 comments and zero reactions; likely a routing bug for `nemotron_speech` in Foundry Local Core. Critical for anyone relying on CLI voice input.

2. **[#3767](./copilot-cli/issues/3767)** – **Oversized attachment permanently wedges session** (area:sessions, area:context‑memory)  
   Attachments exceeding the 5 MB CAPI limit cause an unrecoverable error. No recovery path; closed with 7 comments. Highlights a missing session‑reset mechanism.

3. **[#3762](./copilot-cli/issues/3762)** – **config option `contextTier` does nothing** (area:context‑memory, area:configuration)  
   The setting appears non‑functional until a manual model picker selection is made. 6 comments, no fix yet. Blocks users who rely on long‑context models by default.

4. **[#1826](./copilot-cli/issues/1826)** – **Support multi‑root workspaces via `.code‑workspace`** (area:context‑memory, area:configuration)  
   14 👍 – one of the highest upvoted open issues. The CLI ignores additional root folders when connected via `/ide`, losing instruction files and folder context for multi‑project setups.

5. **[#3399](./copilot-cli/issues/3399)** – **Allow custom headers for BYOK** (area:models, area:configuration)  
   8 👍. Users need to send `X-Tenant-ID` or similar headers to their private LLM servers. A straightforward feature request that would unblock many enterprise deployments.

6. **[#4151](./copilot-cli/issues/4151)** – **plugin install fails with “Access is denied” on Windows** (area:platform‑windows, area:plugins)  
   100% failure on Windows 11 for any source (marketplace, GitHub repo, local). 3 comments, no workaround yet. Blocks all plugin adoption on Windows.

7. **[#4160](./copilot-cli/issues/4160)** – **Plan mode over‑blocks read‑only shell commands** (area:triage)  
   Heuristic incorrectly flags harmless commands (e.g., `cat`, `dir`) as “may modify workspace”. False positives frustrate users who use plan mode for safe exploration.

8. **[#4158](./copilot-cli/issues/4158)** – **Expose queued and active processing state for project sessions** (area:sessions, area:agents)  
   Parent sessions currently cannot tell if a child session is still processing or just idle. Essential for building reliable multi‑session workflows.

9. **[#4163](./copilot-cli/issues/4163)** – **copilot CLI does not reap child processes – zombies accumulate** (area:triage)  
   Zombie processes (~2/min) accumulate under the copilot PID. Observable on Linux; not yet confirmed cross‑platform. System‑health concern for long‑running sessions.

10. **[#4155](./copilot-cli/issues/4155)** – **Gemini models return 400 Bad Request** (area:models)  
    Both `gemini-3.1-pro-preview` and `gemini-3.5-flash` fail with a CAPI error for plain text prompts. Affects users who switch to Google models. No comments beyond the author.

---

### Key PR Progress
No pull requests were updated in the last 24 hours.

---

### Feature Request Trends
- **Permissions granularity** – Several issues ask for path‑prefix‑based file/web permissions (#4157), command identifiers with spaces (#4150), and suppression of low‑credit warnings (#4168).
- **Multi‑session & state visibility** – Requests for exposing queued/active session state (#4158) and better handling of oversized attachments (#3767) indicate a need for more robust session orchestration.
- **Keyboard & terminal UX** – vi‑style `j/k` navigation for multiple‑choice prompts (#4152) and the ability to select text from the TUI (#4154) are small but high‑impact quality‑of‑life improvements.
- **BYOK and customisation** – Custom headers for BYOK (#3399) and the ability to set a default user account (#4166) continue to attract upvotes.
- **Multi‑root workspaces** – The long‑standing #1826 remains the top‑voted feature request.

---

### Developer Pain Points
- **Windows instability** – At least four issues (plugin install #4151, interactive mode blank #4159, resume hang #4165, text selection broken #4154) make the CLI unreliable on Windows 11.
- **Silent failures & regressions** – Voice model transcriptions (#4024), scheduled prompts not firing (#4137), and Gemini 400 errors (#4155) indicate recent regressions in model handling and session logic.
- **Permission misclassification** – Destructive operations like `git branch -D` bypass permission prompts (#4156), while harmless commands are wrongly blocked (#4160).
- **Session recovery gaps** – Oversized attachments wedge sessions with no recovery (#3767), and zombie processes accumulate (#4163) without cleanup.
- **Configuration opacity** – The `contextTier` setting does nothing (#3762), and `max‑ai‑credits=0` is rejected even for local models (#4167), forcing users to work around unintuitive defaults.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-07-18

## Today's Highlights
Three issues and one pull request were updated in the last 24 hours. The community is actively debating the new K2.6 model’s behavior, with many users reporting degraded creativity and increased hallucinations. A critical dependency issue for the Wind plugin on public networks also surfaced, while a PR improves error handling in JSON schema dereferencing.

## Releases
No new releases in the last 24 hours.

## Hot Issues
Only three issues were updated; all are highlighted below.

1. **#1925 – [enhancement] Kimi K2.5 vs K2.6**  
   *Author: herrbasan | Comments: 13*  
   A long-running discussion (since April) where the user requests the ability to switch back to the K2.5 model and its previous system prompt. The complaint: K2.6 “drowns out creativity and increases hallucinations” and “lost all personality.” The 13‑comment thread indicates significant community interest in model selection flexibility.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1925)

2. **#2505 – [Wind plugin] Dependency installation failure**  
   *Author: Steven-DD | Comments: 1*  
   The Wind data plugin (`wind-allskill`) fails with `NETWORK_ERROR` because the required `agent-gw-pysdk` dependency is not bundled and the installation guide points to an internal Moonshot Git server (`dev.msh.team`) unreachable from the public internet. Blocks all Wind data operations on Windows 11 (Git Bash).  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2505)

3. **#2379 – [bug] Markdown list items in TUI drop characters and split words when wrapped**  
   *Author: bdragan | Comments: 1*  
   On Linux (Kimi Code CLI 1.45.0, K2.6 model), markdown list rendering in the TUI breaks lines mid‑word and drops characters. Affects readability for users who rely on terminal output.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2379)

## Key PR Progress
Only one PR was updated in the last 24 hours.

1. **#2506 – fix(kosong): raise a clear error on circular $ref in deref_json_schema**  
   *Author: Sreekant13 | Comments: none*  
   A small self‑contained fix (under 100 lines) that prevents silent infinite recursion when `deref_json_schema` encounters circular `$ref` references. Instead of hanging, a clear error message is now raised. Improves developer‑side debugging for schema processing.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2506)

## Feature Request Trends
The most prominent feature request visible in recent issues is **model version selection** – specifically the ability to choose between K2.5 and K2.6 (and presumably future versions). The feedback indicates that K2.6’s excessive “thinking” mode reduces creativity and introduces hallucinations, suggesting a need for per‑session model switching or user‑adjustable personality/creativity parameters.

## Developer Pain Points
- **Plugin dependency access restricted to internal networks** – The Wind plugin issue (#2505) highlights a recurring pattern where internal-only installation guides or dependencies break public user experience. This is a blocker for developers on Windows who rely on external tools.
- **TUI rendering defects** – Markdown list word‑splitting (#2379) degrades terminal output quality, a low‑severity but irritating usability issue that affects daily workflow.
- **Model behavior dissatisfaction** – The K2.6 vs K2.5 debate (#1925) reflects a broader user frustration with changes in model personality and reasoning style, indicating that users value predictable, creative interactions over excessive internal reasoning.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-18

## Today's Highlights

No new releases were cut in the last 24 hours, but the community remained highly active with 50+ issues and 50 PRs updated. A cluster of bugs around the new v2.0 UI and sub‑agent reliability is drawing developer attention, while long‑standing feature requests for auto‑model discovery and SSH remote support continue to attract upvotes.

## Releases

*None in the last 24 hours.*

---

## Hot Issues

Picked from the top 30 by comment count, focusing on impact, community engagement, and urgency.

1. **[#6231 – Auto-discover models from OpenAI-compatible provider endpoints](https://github.com/anomalyco/opencode/issues/6231)**  
   **182 👍, 21 comments**  
   *Request*: Users want OpenCode to automatically list available models from local providers (LM Studio, Ollama, etc.) instead of manual `opencode.json` entries. Highly upvoted and discussed since Dec 2025.

2. **[#7790 – SSH-based remote server connections to OpenCode Desktop](https://github.com/anomalyco/opencode/issues/7790)**  
   **73 👍, 15 comments**  
   *Request*: First‑class SSH support so desktop users can connect to a remote OpenCode server. Seen as essential for cloud‑based workflows.

3. **[#27924 – Infinite compaction loop when compression fails to reduce context](https://github.com/anomalyco/opencode/issues/27924)**  
   **0 👍, 7 comments**  
   *Bug*: A session can enter an endless `overflow → compact → overflow` loop when compression doesn’t shrink the context below the token limit. A PR (#37584) is already open to fix it.

4. **[#33028 – Subagents hang indefinitely after quick bash tool call](https://github.com/anomalyco/opencode/issues/33028)**  
   **3 👍, 6 comments**  
   *Bug*: Sub‑agents (and the primary agent) freeze after a bash command; the next LLM call never completes. Only pressing `Esc` or killing the process helps. Affects two different models (glm‑5.2, minimax‑m3).

5. **[#24876 – Crash on older Intel Macs (AVX2 incompatibility)](https://github.com/anomalyco/opencode/issues/24876)**  
   **0 👍, 6 comments**  
   *Bug*: The binary crashes immediately on older Intel Macs with `Illegal instruction: 4` due to AVX2 instructions used during init. Blocks a segment of macOS users.

6. **[#37430 – Cannot switch between build and plan modes in new UI](https://github.com/anomalyco/opencode/issues/37430)**  
   **2 👍, 5 comments**  
   *Bug*: The build/plan toggle button is missing in the v1.18.x UI, making it impossible to switch modes once a session starts. Regression in the new UI.

7. **[#31119 – `no such column: name` migration error](https://github.com/anomalyco/opencode/issues/31119)**  
   **11 👍, 13 comments**  
   *Bug*: Users updating from an old version (e.g., 1.16.2) hit a database migration error. The schema mismatch prevents the app from starting.

8. **[#5305 – Plugin Hook for Instant TUI Commands](https://github.com/anomalyco/opencode/issues/5305)**  
   **14 👍, 19 comments**  
   *Feature*: Allow plugins to register instant TUI commands that execute without invoking the agent. Would enable lightweight shortcuts for power users.

9. **[#27303 – Official OpenCode Go/Zen BYOK model provider extension for VSCode Copilot](https://github.com/anomalyco/opencode/issues/27303)**  
   **5 👍, 5 comments**  
   *Feature*: Request to make OpenCode’s model serving available as a BYOK provider in VSCode Copilot, leveraging recent Copilot extension support.

10. **[#34652 – Tool calls fail with SchemaError when Anthropic provider returns nested array as JSON string](https://github.com/anomalyco/opencode/issues/34652)**  
    **0 👍, 5 comments**  
    *Bug*: The `todowrite` tool (and similar) fails with a hard SchemaError when the Anthropic model returns a nested argument as a JSON string instead of a real array. Only affects the native Anthropic provider.

---

## Key PR Progress

Selected from the top 20 PRs updated in the last 24 hours, covering fixes, features, and infrastructure.

1. **[#37584 – fix(session): bound consecutive overflow compaction cycles](https://github.com/anomalyco/opencode/pull/37584)**  
   Targets the infinite‑compaction loop (#27924) by limiting retries and checking compaction effectiveness. Still open.

2. **[#37570 – test(cli): lock managed reconnect ensure-on-first-failure](https://github.com/anomalyco/opencode/pull/37570)**  
   Adds test coverage for the managed‑service reconnection logic. Part of the “scope streams + bound payloads” epic (#36441).

3. **[#37559 – feat(core): bound tool and admitted event payloads via session blobs](https://github.com/anomalyco/opencode/pull/37559)**  
   Introduces session‑scoped blobs for tool and event payloads, improving data flow boundaries. Linked to epic #36441.

4. **[#37486 – feat(server): opt-in location interest for event subscriptions](https://github.com/anomalyco/opencode/pull/37486)**  
   Allows subscribers to filter events by location (directory), reducing noise in multi‑workspace setups.

5. **[#37487 – feat(server): narrow event subscriptions by session interest](https://github.com/anomalyco/opencode/pull/37487)**  
   Complementary to #37486; adds session‑level filtering for event subscriptions.

6. **[#37571 – [closed] fix(tui): bundle parser worker separately](https://github.com/anomalyco/opencode/pull/37571)**  
   Fixes a build collision between OpenCode’s TUI and the OpenTUI 0.4.5 parser worker. Merged quickly after reported regression.

7. **[#37582 – [open] revert(tui): downgrade opentui to 0.4.3](https://github.com/anomalyco/opencode/pull/37582)**  
   Temporary mitigation: reverts the OpenTUI upgrade that caused startup failures. Still open, likely to be superseded by a proper fix.

8. **[#37226 – feat(core): per-agent subagent_depth override](https://github.com/anomalyco/opencode/pull/37226)**  
   Adds an optional `subagent_depth` field to agent configuration. Allows agents to override the global depth limit, giving finer control over sub‑agent chains.

9. **[#36433 – fix(tui): preserve prompts during session hydration](https://github.com/anomalyco/opencode/pull/36433)**  
   Prevents the V2 TUI from dropping the first user prompt when a new session opens or reconnects. Fixes a frustrating UX bug.

10. **[#33907 – fix(app): preserve mobile prompt newlines](https://github.com/anomalyco/opencode/pull/33907)**  
    Treats plain Enter as a newline in the web prompt composer on mobile, while keeping Enter‑to‑submit on desktop. Small but important for mobile users.

Note: Several other PRs (e.g., #14468 for LiteLLM provider, #20491 for Kiro provider) are long‑standing and still open, but not updated in the last 24h.

---

## Feature Request Trends

Distilling the directions implied by this batch of issues:

- **Automatic model discovery** – Users want to stop manually listing models from local/OpenAI‑compatible providers. (#6231, #14468)
- **Remote / SSH connectivity** – High demand for first‑class remote server connections in the Desktop app. (#7790, #33273)
- **Plugin extensibility** – Growing interest in plugin hooks for instant commands, custom sidekicks, and model providers. (#5305, #27303)
- **Deeper agent configuration** – Per‑agent settings (subagent depth, model overrides, context limits) are repeatedly requested. (#37226, #31020)
- **IME / keyboard integration** – Requests for auto‑switching IME when using leader keys, and fixing shortcut regressions. (#37167, #37165)

---

## Developer Pain Points

Recurring frustrations visible in this batch:

- **Database migration errors** – Schema changes between versions cause `no such column` errors, locking users out. (#31119, #35403)
- **UI regressions in the new UI** – Missing build/plan toggle (#37430), invisible agent names (#37565), overly dark text (#37428), and missing command descriptions (#35415).
- **Sub‑agent reliability** – Infinite compaction loops (#27924), indefinite hangs (#33028), and provider‑specific failures (Ollama “Not Found”, Anthropic SchemaError) disrupt multi‑agent workflows.
- **Compatibility gaps** – AVX2 crash on older Intel Macs (#24876), Windows path corruption in WSL (#36902), and Windows/IME shortcut issues (#37165).
- **Dependency breakage** – Upgrades to OpenTUI broke the bundled TUI (#37556), leading to quick reverts (#37571, #37582).
- **Provider divergence** – Models behave differently across providers, especially Anthropic’s nested arguments (#34652) and custom OpenAI‑compatible endpoints (#36834).

---

*Generated from GitHub data for 2026-07-18. All links point to [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode).*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-18

A quiet day for releases but a busy one for bug fixes and quality-of-life improvements. The community focused heavily on performance regressions in long sessions (core pinning, memory blowups) and on expanding provider support (StepFun, Kimi K3 thinking levels). Several important reliability fixes landed, including retry logic for compaction and better handling of edge cases in streaming and auth configuration.

---

## Today's Highlights

No new releases today. The project saw a burst of activity on stability: fixes landed for a 100% CPU bug in the TUI’s markdown renderer and a memory blowup in the agent loop’s tool-update buffering. Provider expansion continued with native StepFun support and deeper Kimi K3 effort-level integration. A major architectual PR proposing “managed agents” was also opened, signaling a push toward multi-agent workflows.

---

## Releases

*No new releases in the last 24 hours.*

---

## Hot Issues

1. **#6747 – API for enhancing agent message markdown** (OPEN, 5 comments)  
   *xl0* requests an extension API to mutate agent message rendering (e.g., for a formula renderer) without altering the LLM payload. This is a clean architectural ask that other extension authors could build on.  
   https://github.com/earendil-works/pi/issues/6747

2. **#6665 – TUI pins a full core while streaming** (OPEN, 3 comments)  
   *axelbaumlisto* reports 100% CPU usage in long streaming sessions, traced to uncached `Intl.Segmenter` calls and per-chunk Markdown rebuilds in the render timer. A high-impact performance bug for anyone running long agent sessions.  
   https://github.com/earendil-works/pi/issues/6665

3. **#6725 – Copilot pricing for GPT-5.6 models is incorrect** (OPEN, 4 comments)  
   *krzyk* finds that cache-write costs are missing from Copilot cost calculations, causing the displayed cost to under-report by roughly a third. Important for users watching their API spend.  
   https://github.com/earendil-works/pi/issues/6725

4. **#6755 – Agent loop retains every tool partial update (multi-GB RSS)** (CLOSED, 4 comments)  
   *andrebreijao* discovers that `executePreparedToolCall` retains all partial updates as promises and runs `Promise.all` over them at the end, causing minutes-long stalls and multi-GB memory usage for long-running tools. A severe but recently fixed bug.  
   https://github.com/earendil-works/pi/issues/6755

5. **#6647 – Compaction fails on a single transient stream drop** (OPEN, 2 comments)  
   *axelbaumlisto* notes that compaction runs a single non-retried summarization call, so a temporary socket death fails the entire compaction. A PR has since been opened to add retry logic.  
   https://github.com/earendil-works/pi/issues/6647

6. **#6652 – TUI crash log hardcodes ~/.pi, ignoring PI_CODING_AGENT_DIR** (OPEN, 2 comments)  
   *luminary19* reports that after moving `.pi` away from home, a TUI crash creates a new `.pi` directory at the home path. A configuration-following bug that breaks portability.  
   https://github.com/earendil-works/pi/issues/6652

7. **#6714 – Config does not sync packages, pi update does not install missing** (CLOSED, 4 comments)  
   *lumenradley* highlights that Git sync of `.pi` config doesn’t propagate packages between machines, and `pi update --extensions` doesn’t fill the gap. A frequent cross-machine setup frustration.  
   https://github.com/earendil-works/pi/issues/6714

8. **#6768 – Compaction using Copilot Enterprise not possible** (CLOSED, 2 comments)  
   *MojangPlsFix* hits 421 Misdirected Request errors when compacting with Copilot Enterprise licenses. Critical for enterprise users relying on compaction to stay within context limits.  
   https://github.com/earendil-works/pi/issues/6768

9. **#6748 – Deprecated together.ai models still listed** (CLOSED, 3 comments)  
   *mcwalrus* reports five together.ai models that are officially deprecated but still selectable via `pi --list-models`. A cleanup issue that could lead users to broken providers.  
   https://github.com/earendil-works/pi/issues/6748

10. **#6761 – Orphaned tool_use blocks reach the API and 400 in long sessions** (CLOSED, 2 comments)  
    *anh-chu* finds that long conversations can leave `tool_use` IDs without matching `tool_result` blocks, causing 400 errors from Anthropic. A final repair pass is proposed.  
    https://github.com/earendil-works/pi/issues/6761

---

## Key PR Progress

1. **#6790 – fix(tui): clear inverted cursor on exit** (CLOSED)  
   *dam9000* prevents a dual-cursor artifact by overwriting the reverse-video cursor with a space before TUI exit. A small but polished UX fix.  
   https://github.com/earendil-works/pi/pull/6790

2. **#6680 – parse extension package name in case of dependent extension** (OPEN)  
   *davidbrai* addresses a bug where dependent extensions aren’t recognized by package-name parsing. Partial fix for #6619, important for the extension ecosystem.  
   https://github.com/earendil-works/pi/pull/6680

3. **#6671 – add usage info to branch summary, compaction and tool result entries** (OPEN)  
   *davidbrai* adds usage metadata to summarization, compaction, and tool result events, enabling better cost tracking and transparency.  
   https://github.com/earendil-works/pi/pull/6671

4. **#6786 – fix(ai): expose Kimi Coding K3 effort levels** (OPEN)  
   *dannote* follows up on #6769 by exposing `low`, `high`, and `max` thinking levels for Kimi K3 (previously only `max`). A direct response to user demand.  
   https://github.com/earendil-works/pi/pull/6786

5. **#6785 – docs: add managed agents separation PRD** (CLOSED)  
   *L-Rocket* opens a product-requirements document for separating managed agents from the main agent loop. Signals a major new feature direction.  
   https://github.com/earendil-works/pi/pull/6785

6. **#6783 – feat(ai): add StepFun providers** (CLOSED)  
   *lit26* adds four native StepFun providers covering Chinese and global API endpoints with prepaid routing. A significant provider expansion for Asian markets.  
   https://github.com/earendil-works/pi/pull/6783

7. **#6779 – feat(ai): support freeform tool calls** (CLOSED)  
   *t0ster* introduces typed JSON and freeform tool definitions across the AI and agent APIs, plus support for OpenAI custom tool calls. Broadens tool-use flexibility.  
   https://github.com/earendil-works/pi/pull/6779

8. **#6775 – retry on compaction/branch summarization retryable failures** (OPEN)  
   *davidbrai* adds retry logic to compaction and branch summarization (fixing #6647), with a question about whether to show UI indication on retries.  
   https://github.com/earendil-works/pi/pull/6775

9. **#6778 – fix: preserve extension provider auth during availability refresh** (CLOSED)  
   *mahdyarief* fixes a regression where extension providers lose auth on `/new` or provider switch because `runAvailabilityRefresh` clears provisional auth entries.  
   https://github.com/earendil-works/pi/pull/6778

10. **#6772 – export missing message and tool execution event types** (OPEN)  
    *davidbrai* exports previously un-exported types from the API layer, fixing #6687. Important for extension authors building on the public API.  
    https://github.com/earendil-works/pi/pull/6772

---

## Feature Request Trends

- **Extension-friendly UI hooks** – Several requests want extensions to mutate agent message rendering (#6747) and to offer collapsed tool card views (#5137), reflecting demand for deeper plugin customisation.
- **Environment-variable configuration** – Users increasingly ask for `PI_MODEL`, `PI_PROVIDER`, and `PI_OFFLINE` support (#6777), seeking parity with CLI flags and easier dev-environment switching.
- **Provider expansion and thinking-level depth** – Requests for new providers (StepFun, #6783) and finer-grained thinking levels (Kimi K3 low/high, #6786; Gemini thought signatures, #6733) show the community actively pushing for broader, more nuanced model support.
- **Managed multi-agent workflows** – The new PRD for managed agents (#6785) suggests the maintainers are exploring how to formalise multiple-agent orchestration, which could become a major feature in coming months.

---

## Developer Pain Points

- **Performance regressions in long sessions** – The TUI pinning 100% CPU (#6665) and agent-loop memory blowups (#6755) are the most severe recurring headaches, affecting anyone running extended agent conversations.
- **Configuration and provider friction** – Copilot pricing mismatches (#6725), deprecated models still listed (#6748), Copilot Enterprise compaction failures (#6768), and hardcoded crash-log paths (#6652) collectively create a bumpy setup experience.
- **Brittle error handling under network stress** – Compaction failures on transient drops (#6647), orphaned tool_use blocks causing 400 errors (#6761), and JSON parse crashes on control chars in SSE streams (#6762) point to a need for more robust retry and repair logic throughout the streaming pipeline.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-18

## Today’s Highlights
The team continues to harden the **daemon multi-workspace** architecture, with a new RFC (Issue #6378) generating significant discussion and a complementary fix landed in tonight’s nightly release. Meanwhile, a **CI Shepherd** (PR #7142) and a **Fan-Out Autofix** (PR #7127) aim to automate bot-PR maintenance and reduce review latency. Several Web Shell and CLI usability fixes (image path resolution, plan-mode toggling, workspace path autocomplete) also moved forward.

## Releases
- **v0.19.11-nightly.20260718.767a32484** — Nightly with two changes:
  - `feat(daemon): Trace cold first-session startup` — improves observability of daemon boot latency.
  - `fix(serve): Harden multi-workspace ownership` — addresses a permission edge case for concurrent workspace usage.

## Hot Issues
1. **#6378 – RFC: Support multiple workspaces in one qwen serve daemon** (29 💬)  
   *[OPEN, daemon]*  
   A foundational design proposal to allow a single daemon process to serve multiple workspaces while preserving single-workspace backward compatibility. High community interest as it enables long-running server setups.

2. **#4748 – Optimize daemon cold start and qwen serve fast-path latency** (6 💬)  
   *[OPEN, daemon]*  
   Tracks remaining latency gaps after initial optimizations. Critical for users relying on the daemon for quick interactive sessions.

3. **#7040 – RFC: Reliable auto-memory recall — timing, quality, and telemetry** (6 💬)  
   *[OPEN, core/roadmap]*  
   Proposes improving memory recall with telemetry and timing, narrowed to impact every user. Signals a push toward smarter context management.

4. **#7051 – VS Code side plugin connection error** (6 💬)  
   *[CLOSED, bug/integration]*  
   Reports `acp` process exit with Electron/Chromium flag warnings. Affected VS Code Companion users on Linux.

5. **#6809 – Ctrl+S diff preview garbled for multi-line edits** (4 💬)  
   *[CLOSED, bug/ui]*  
   Lines concatenated in permission dialog diff view. Reproducible and impacts trust in edit approvals.

6. **#7096 – Main CI failed: E2E Tests** (4 💬)  
   *[CLOSED, autofix/skip]*  
   Bot-reported CI failure indicating flakiness in end-to-end tests. Generated several companion PRs to harden tests.

7. **#4586 – Ctrl+C in PyCharm terminal causes unexpected exit** (3 💬)  
   *[CLOSED, bug/cli]*  
   Single Ctrl+C now exits agent instead of double-tap. Frequent user complaint; `esc` also doesn’t interrupt.

8. **#6806 – Status line context percentage not refreshed after /compress** (3 💬)  
   *[OPEN, bug/ui, welcome-pr]*  
   Stale token count display after compression. A clear UI regression that confuses resource tracking.

9. **#6992 – Chained MCP calls fail silently with permission UI stuck** (3 💬)  
   *[OPEN, bug/ui]*  
   Two distinct bugs: silent failure on chained MCP calls and a stuck permission dialog on Windows. Blocks multi-MCP workflows.

10. **#7128 – Refreshing page concatenates previous messages into input** (2 💬)  
    *[CLOSED, bug/web-shell]*  
    After two sends and a refresh, messages are concatenated and re-inserted. 100% reproducible locally; indicates state management flaw.

## Key PR Progress
1. **#6945 – feat(cli): add daemon Todo stop guard**  
   *[CLOSED]*  
   Introduces opt-in continuation after `todo_write` for daemon sessions, limiting to two additional calls. Reduces dropped work while preventing runaway loops.

2. **#6999 – feat(webshell): replay ChatRecord history in readonly WebShell**  
   *[OPEN]*  
   Adds deterministic replay of persisted chat history into daemon transcripts. Unlocks session restoration for Web Shell.

3. **#7142 – ci(shepherd): add Fleet Shepherd — automated unblocking of bot-PR fleet**  
   *[OPEN]*  
   A janitor workflow that runs every 15 minutes to fix merge conflicts, update branches, and retry autofix loops on bot PRs. Reduces human overhead.

4. **#7048 – feat(core): improve subagent delegation defaults and guardrails**  
   *[OPEN]*  
   Makes one-shot subagents background by default; preserves explicit foreground opt-out. Improves reliability of multi-agent pipelines.

5. **#7116 – feat(cli): toggle plan confirmation expand/collapse with 'e' key**  
   *[OPEN]*  
   Adds inline expand/collapse to the plan-mode exit dialog, letting users read full plans in terminal scrollback. (Implements #7001)

6. **#7053 – refactor(core): Classify shell safety as read-only, write, or unknown**  
   *[OPEN]*  
   Internal three-state safety classification for shell commands, precedence-sensitive. Foundation for smarter auto-approval.

7. **#6579 – fix(cli): keep model switches session-scoped**  
   *[OPEN]*  
   `/model` now only affects the current session; explicit `--default` required to persist. Prevents accidental default changes.

8. **#7123 – fix(acp): resolve textual @ image paths**  
   *[OPEN]*  
   ACP sessions now resolve `@/path/to/image.png` references inside text, respecting workspace boundaries and ignore rules.

9. **#7054 – feat(web-shell): git status chip, visual working-tree diff, and sidebar git status**  
   *[OPEN]*  
   Major Web Shell Git integration: live dirty-state indicator, visual diff viewer, and full sidebar status. Enhances developer workflow.

10. **#7127 – ci(autofix): fan out review targets and stop route-scan starvation**  
    *[OPEN]*  
    Parallelizes autofix review loop and improves scan scheduling; addresses bottleneck where busy repos starved less-active PRs.

## Feature Request Trends
- **Multi-workspace daemon & session management** – Leading trend: #6378 (RFC), with additional requests for workspace-scoped session-info APIs (#7069, #7070, #7071) and ownership semantics for `cd` (#7015).
- **Reliable memory/context recall** – #7040 (auto-memory recall) and #6806 (status line refresh after compression) point to demand for transparent, accurate context tracking.
- **Background automation** – Todo continuation (#6946), subagent background defaults (#7048), and workspace-scoped contact channels (#7103) all aim to reduce manual intervention.
- **Web Shell parity with CLI** – Folder picker (#7102), persistent pagination errors (#7117), roadmap parity for `/goal` (#6561), and Git awareness (#7054).
- **Unified tool path formatting** – Multiple requests (#7007, #7110) to add `formatDisplayPath()` across grep/glob/ripGrep and tool descriptions for better readability.

## Developer Pain Points
- **Terminal signal handling** – Ctrl+C behaviour remains a sore spot: #4586 (single-Ctrl-C exits in PyCharm), #6776 (garbled terminal after Ctrl-C), and the closed #6809 (diff preview corrupted) indicate fragile keybinding state.
- **CI flakiness** – Three main-branch E2E test failures (#7096, #7111, #7086) in one day, despite autofix attempts. The new Fleet Shepherd (#7142) and fan-out autofix (#7127) are direct responses.
- **Silent failures & stuck states** – #6992 (chained MCP calls fail silently), #6927 (classifier deadlock with `auto` approval), and #7128 (message concatenation on refresh) all cause user confusion without clear error communication.
- **UI responsiveness** – Stale status line (#6806), missing right border on skill modal (#7037), and streaming rendering breakage (#7006) suggest rendering logic under higher load is still brittle.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-18

## Today’s Highlights

The community remains focused on the upcoming v0.9.3 cycle, with major work on native Termux/Android support, OAuth authentication for multiple providers, and recurring Windows reliability issues. Maintainers are closing gaps on xAI device login, Kimi K3 support, and auto-routing transparency, while contributors continue to fix TUI rendering glitches and process leaks on Windows.

## Releases

No releases in the last 24 hours.

## Hot Issues

1. **[[#4032] Codewhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032)** — 35 comments. High-severity behavioral bug: the agent consistently writes temporary scripts despite user-provided scripts, and refuses to accept challenges. Community frustration is high; many users report similar autonomy violations.

2. **[[#3275] CodeWhale overly involved — self-questioning and deviating from user intent](https://github.com/Hmbown/CodeWhale/issues/3275)** — 17 comments. A regression from #3061, the agent enters a self-driven loop without waiting for confirmation. Ties directly to agent trust and control concerns.

3. **[[#3192] List CodeWhale on Agent Client Protocol registry](https://github.com/Hmbown/CodeWhale/issues/3192)** — 12 comments. A straightforward integration request that would enable easier installation from Zed and other ACP-compatible editors. Highly requested.

4. **[[#1481] Support OpenCode Go/Zen as DeepSeek provider](https://github.com/Hmbown/CodeWhale/issues/1481)** — 9 comments. Users want access to DeepSeek-V4 via cheap OpenCode endpoints. Open for over two months; maintainers have not yet acted.

5. **[[#4242] v0.9.3: Run Termux runtime QA for shell, PTY, config, and TUI startup](https://github.com/Hmbown/CodeWhale/issues/4242)** — 8 comments. A critical step toward official Android support. Maintainer is actively tracking validation matrix.

6. **[[#4236] v0.9.3: Epic — official Termux / Android arm64 support](https://github.com/Hmbown/CodeWhale/issues/4236)** — 7 comments. Parent epic for Termux. Users have long requested native arm64 builds; this tracks ABI fix and distribution.

7. **[[#4417] v0.9.3: Add first-class Kimi OAuth device login and token lifecycle](https://github.com/Hmbown/CodeWhale/issues/4417)** — 5 comments. Companion to Kimi K3 model support (#4387). Important for users who prefer OAuth over API keys.

8. **[[#4479] TUI rendering glitch — missing / extra spaces, recovers on mouse selection](https://github.com/Hmbown/CodeWhale/issues/4479)** — 4 comments, updated today. Reported on Windows Terminal; intermittent but frustrating. Likely a terminal abstraction or rendering-layer bug.

9. **[[#4100] exec_shell fails with exit code 2147483647 in specific Windows sessions](https://github.com/Hmbown/CodeWhale/issues/4100)** — 4 comments. Catastrophic exit code suggests resource exhaustion or handle leak in Windows ConPTY. Serious reliability issue for Windows users.

10. **[[#4489] Hooks process leak on Windows](https://github.com/Hmbown/CodeWhale/issues/4489)** — 4 comments, updated today. Hook commands that inherit stdin without EOF cause orphaned Node.js processes. A clear resource management bug.

## Key PR Progress

1. **[#4477: fix: don't let Vim Normal mode swallow Space for thinking block expansion](https://github.com/Hmbown/CodeWhale/pull/4477)** — Closed. Small but precise fix: Space now correctly toggles thinking blocks even when in Vim Normal mode.

2. **[#4498: fix(tui): make Ctrl+O inspector complete and draft-safe](https://github.com/Hmbown/CodeWhale/pull/4498)** — Open. Improves pager reliability and moves external-editor access to Ctrl+Shift+O. Addresses #4482.

3. **[#4506: feat(release): publish native Windows ARM64 artifacts](https://github.com/Hmbown/CodeWhale/pull/4506)** — Open. Important for Snapdragon X / Surface Pro users. Includes npm, updater, and docs changes.

4. **[#4505: fix(auth): isolate xAI device login from Tokio](https://github.com/Hmbown/CodeWhale/pull/4505)** — Open. Fixes `auth xai-device` failing with parse error by running synchronous logic on the blocking pool. Addresses #4410.

5. **[#4504: fix(onboarding): support keyless and guided provider setup](https://github.com/Hmbown/CodeWhale/pull/4504)** — Open. Lets first-run users skip API key for self-hosted runtimes (SGLang, vLLM, Ollama) and continue. Addresses #3927.

6. **[#4500: feat(auto): surface routing scope and per-turn receipts](https://github.com/Hmbown/CodeWhale/pull/4500)** — Open. Makes Auto-mode routing transparent by recording receipt and selection scope. Addresses #4405.

7. **[#4499: fix: close v0.9.1 MCP and Fleet truth gaps](https://github.com/Hmbown/CodeWhale/pull/4499)** — Closed. Two commits: one making MCP approval semantics exact in sub-agents, the other distinguishing current-session vs persistent state.

8. **[#4491: fix(runtime): contain hooks and preserve Windows PTY status](https://github.com/Hmbown/CodeWhale/pull/4491)** — Closed. Fixes hook process leak (#4489) and removes lossy exit-status sentinel that hid #4100.

9. **[#4490: fix(mcp): align configured command health with spawn](https://github.com/Hmbown/CodeWhale/pull/4490)** — Closed. Ensures `codewhale doctor` reports MCP server health correctly by matching environment resolution.

10. **[#4508: docs: refresh the Codewhale product screenshot](https://github.com/Hmbown/CodeWhale/pull/4508)** — Open. Updates README and website to a consistent new canonical screenshot, including a contract test for byte-identical PNGs.

## Feature Request Trends

- **Termux / Android arm64 support** — Multiple issues (#4236, #4242, #1135) show strong demand for native Android builds. Maintainers are actively working the epic.
- **Provider diversity and OAuth** — Requests for OpenCode Go/Zen (#1481), Kimi K3 + OAuth (#4387, #4417), xAI device-code OAuth (#4410), and OpenAI Codex OAuth verification (#2984) indicate a push toward first-class OAuth flows and cheaper model endpoints.
- **Localization** — Russian (#3092), Korean, Spanish, Brazilian Portuguese (#3093) are planned for v0.9.2 onward.
- **Agent control & transparency** — Issues like #3192 (ACP registry) and #4415 (hard per-turn tool budgets) reflect demand for better observability and tighter constraints on agent behavior.
- **Remote / US infrastructure** — #1990 asks for a US-equivalent lane (Cloudflare, AWS, Telegram) analogous to the existing Tencent path.

## Developer Pain Points

- **Windows-specific bugs dominate the reliability landscape** — ConPTY resource leaks (#4100), hook process leaks (#4489), TUI rendering glitches (#4479), and Ctrl+O pager truncation (#4482) create a poor Windows experience.
- **Agent autonomy vs. user intent** — Issues #4032 and #3275 highlight a recurring complaint that CodeWhale oversteps, writes scripts without asking, or enters self-questioning loops. Erosion of trust is a clear community pain point.
- **OAuth integration fragility** — Several auth endpoints fail silently or parse wrongly (#4410, #4501). Users expect smooth device-code flows.
- **Sandbox and networking constraints** — SSH failure (#1829) due to outbound TCP 22 blocking in the shell sandbox is a persistent limitation for remote operation.
- **Stale agent state between sessions** — #4416 reports that failed-agent rows from earlier sessions appear in new instances, confusing workspace isolation.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*