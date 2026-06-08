# AI CLI Tools Community Digest 2026-06-08

> Generated: 2026-06-08 02:52 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Analysis Date:** 2026-06-08

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem in mid-2026 is marked by **intense community engagement around reliability and cost transparency**, while major platform gaps (Linux desktop, Windows sandbox) remain unaddressed. Usage-limit bugs and billing surprises dominate the highest-traffic issues across Claude Code, Codex, and OpenCode, eroding trust among paying subscribers. A clear **"compaction crisis"** unites Claude Code, Gemini CLI, Copilot CLI, and Pi — all face silent context-management failures that break long sessions. Meanwhile, the ecosystem is bifurcating: established tools (Claude Code, Codex) face scaling pains with large userbases, while newer entrants like Qwen Code and Pi demonstrate faster iteration cycles and more responsive development. The emergence of **declarative agent definitions** (Qwen Code, DeepSeek TUI) and **session persistence across devices** (Kimi Code, Pi) signals the next wave of feature demands.

---

## 2. Activity Comparison

| Tool | Release Today | Hot Issues (selected) | PR Activity (24h) | Top Issue Engagement | Maturity Signal |
|------|:---:|:---:|:---:|:---:|:---:|
| **Claude Code** | None | 10 | 2 updated | 691 👍, 1476 comments (#16157) | Largest community, scaling pains |
| **Codex (OpenAI)** | None | 10 | 10 picked (20+ total) | 510 👍 (#11023 Linux app) | Steady engineering, Windows focus |
| **Gemini CLI** | None | 10 | 10 picked | 8 👍 (#21409 agent hangs) | Active triage, reliability focus |
| **Copilot CLI** | None | 10 | 1 (non-functional) | 4 👍 (#333 SSL proxies) | Low engagement, enterprise niche |
| **Kimi Code** | None | 7 (all recent) | 1 | 5 comments (#2269 handoff) | Post-migration turmoil, trust erosion |
| **OpenCode** | None | 11 | 11 picked | 51 👍, 63 comments (#2242 sandbox) | High engagement, diverse bug reports |
| **Pi** | None | 10 | 8 merged | 6 👍 (#5223 Opus 4.8) | Fast iteration, contributor-driven |
| **Qwen Code** | **Nightly v0.17.1** | 10 | 10 picked | 12 comments (#4514 daemon gaps) | Ambitious, rapid feature velocity |
| **DeepSeek TUI** (CodeWhale) | None | 10 | 10 picked | 24 comments (#1177 caching) | Active bug fixing, i18n push |

**Key observations:**
- **Claude Code** dominates raw engagement (nearly 1,500 comments on a single issue)
- **Codex** and **OpenCode** have the most PR activity in the last 24h
- **Qwen Code** is the only tool with a release today (nightly)
- **Copilot CLI** shows the lowest community activity and PR throughput
- **Pi** has the highest PR merge rate relative to its community size

---

## 3. Shared Feature Directions

Cross-tool requirements appearing in multiple communities:

### Linux Desktop Support
- **Claude Code** (#65697, 313 👍) — most-upvoted feature request
- **Codex** (#11023, 510 👍) — highest-voted open issue
- **Gemini CLI** (#21983) — browser sub-agent fails on Wayland

### Context Compaction & Window Management
- **Claude Code** (#63015) — auto-compact never triggers at 100%
- **Codex** (#7808) — running out of context kills chat thread with no warning
- **OpenCode** (#3099) — rules lost after compaction
- **Pi** (#5480) — post-compaction context showing `null` (now fixed)

### Usage Limits & Billing Transparency
- **Claude Code** (#16157, 691 👍) — Max subscribers hit caps instantly
- **Codex** (#12299, #26512) — false "usage limit" errors, unexplained quota drain
- **OpenCode** (#15585) — ambiguous "free usage exceeded" errors
- **Gemini CLI** (#25179) — 429 "No capacity" for popular models

### Windows WSL & Sandbox Compatibility
- **Codex** (#25715) — WSL2 unusably slow; (#25362) — error 740 on Windows
- **OpenCode** (#31095) — WSL desktop bugs (distro init, server removal)
- **Claude Code** (#58510) — MCP servers fail on Windows with `spawn ENOENT`
- **Copilot CLI** (#3712) — ReFS/Dev Drive local-sandbox limitation

### Session Persistence & Remote Control
- **Kimi Code** (#2269) — multi-device session handoff (top feature request)
- **Claude Code** (#32982) — Remote Control sessions die after ~20 min idle
- **Gemini CLI** (#20303, PR #15674) — remote agents with advanced auth
- **Pi** (#5479) — service reuse on same-CWD session switch
- **Qwen Code** (#4833) — session idle reaper for automatic cleanup

### MCP & Plugin Ecosystem Maturity
- **Codex** (#17265) — MCP OAuth tokens not auto-refreshed
- **OpenCode** (#31271) — respect MCP servers without `tools/list`
- **Pi** (#5469) — collapse MCP tool results by default
- **Claude Code** (#58510) — MCP failures on Windows

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|-------|------------|-------------|-----------|----------|-----|-----------|--------------|
| **Core approach** | Generalist agent | Agent sandbox focus | Sub-agent orchestration | GitHub-ecosystem tight | Cloud-backed session | Multi-provider agnostic | Lightweight, extensible | Daemon-first architecture | Multi-mode agent (Plan/Agent/YOLO) |
| **Target user** | Power users, Max subscribers | Pro developers, enterprise | Cloud-native devs | GitHub enterprise | Developer workstation | Self-hosted, platform-agnostic | Local-first, customization | Cloud & enterprise | Cost-sensitive, local-model users |
| **Platform strength** | macOS, CLI-first | Linux/Codex App | Cloud CLI | GitHub Actions | All platforms (beta) | VSCode + cross-platform | Cross-platform TUI | REST daemon, ACP | macOS/Linux TUI |
| **Key differentiator** | Largest community, most features | Strongest sandbox security | Google model exclusivity | GitHub integration | Session portability | Provider flexibility | Fastest bug-to-fix cycle | Daemon mode & ACP | Chinese developer community |
| **Current pain point** | Usage limits at scale | Windows sandbox | Agent reliability | Enterprise proxy gaps | Migration confusion | Local provider bugs | Cold start latency | Air-gapped init | Token consumption cost |
| **Community size** | Very large | Large | Medium | Small | Small | Medium | Medium-small | Small | Medium (CN-heavy) |

---

## 5. Community Momentum & Maturity

### Most Mature & Largest Communities
**Claude Code** remains the ecosystem benchmark with the highest issue engagement and feature density, but is showing **community fatigue** — the usage limit bug (#16157) has nearly 1,500 comments with no resolution, and multiple regressions (compaction, model quality) have gone unaddressed for weeks. The 313-vote Linux desktop request signals a platform gap that competitors could exploit.

### Rapidly Iterating (High Velocity)
- **Qwen Code** — shipped a nightly release today, merged daemon-mode ACP support, and has the most ambitious PR pipeline (session branching, idle reaper, declarative agents). Highest feature velocity in the ecosystem.
- **Pi** — 8 PRs merged in 24 hours, with contributor `dyyz1993` landing three quality-of-life improvements. The fastest bug-to-fix cycle observed.
- **Codex** — consistent engineering output (10+ active PRs), focused on sandbox hardening, caching, and API stability. Closed two approved-fix PRs today.

### Stability Concerns
- **Kimi Code** — the migration from `kimi-cli` to `kimi-code` has triggered **trust erosion** (users reconsidering subscriptions). Installation confusion, quality regression reports, and a closed issue about "community division" are red flags.
- **DeepSeek TUI (CodeWhale)** — high token consumption and prefix-cache issues are driving cost-sensitive users away. The rebranding to CodeWhale has created migration friction without clear documentation.
- **Copilot CLI** — lowest activity among all tools examined. The one open PR is non-functional, and the top issue (#333 SSL proxies) has 4 upvotes — suggesting very low active user engagement.

### Emerging Contenders
**Pi** and **Qwen Code** are building distinctive technical identities (extensibility vs. daemon-mode power) and have the most responsive development cycles. **OpenCode** has strong community engagement around security and provider flexibility but struggles with documentation gaps.

---

## 6. Trend Signals

### 🟢 Positive Signals

**1. Declarative Agent Definitions** — Both Qwen Code (#4821) and DeepSeek TUI (AGENTS.md from `~/.agents/`) are adopting YAML/Markdown-based agent specs, mirroring Claude Code's pattern. This **vendor-neutral agent format** could become an ecosystem standard.

**2. Daemon/Server Mode Expansion** — Qwen Code's ACP Streamable HTTP transport and session management (branching, idle cleanup) represent a **major architectural shift** from CLI-only to service-oriented design. Pi's session-reuse optimization supports this trend.

**3. Multi-Model & Fallback Support** — Growing demand across Qwen Code, OpenCode, and Pi for dynamic model switching, BYOK providers, and graceful fallback. Users want **resilience across model failures**, not hard crashes.

**4. Internationalization** — DeepSeek TUI's i18n PRs (7 locales) signal that Chinese-first tools are expanding globally. This ecosystem is becoming **multilingual** beyond English and Chinese.

**5. Sandbox Security Hardening** — Codex's `deny_read` enforcement, Gemini CLI's redaction improvements, and Pi's mandatory bash descriptions show a shared commitment to **security-by-default** execution policies.

### 🔴 Red Flags

**1. The Billing Crisis** — Claude Code, Codex, and OpenCode all face community backlash over **opaque usage limits and false quota errors**. This is the #1 trust-destroying issue in the ecosystem. Tools that solve transparent metering first will win subscriber confidence.

**2. Compaction as a Universal Failure Point** — Every major tool except Kimi Code reports compaction/context-management bugs. This is a **fundamental architectural challenge** that no tool has fully solved. Users are hitting walls in long sessions across the board.

**3. Windows Neglect** — Despite a significant Windows developer base, issues with WSL2, sandbox errors, and clipboard gaps remain unfixed for months (Codex error 740, Claude Code drag-and-drop, OpenCode LF line endings). This creates a **platform parity crisis** that leaves Windows users as second-class citizens.

**4. Agent Reliability Is Not Production-Grade** — Gemini CLI agents hang indefinitely (#21409), Copilot CLI enters infinite directory loops (#3216), DeepSeek TUI crashes mid-refactoring (#2620). The **agent reliability threshold** has not been crossed for production use cases.

**5. Post-Migration Trust Erosion** — Both Kimi Code and DeepSeek TUI are experiencing **community fragmentation** after rebranding or product pivots. Users interpret these moves as instability, and recovery requires transparent communication.

### 📈 Recommendations for Developers

- **Evaluate Pi or Qwen Code** if you want a rapidly improving tool with responsive maintainers and fresh architectural thinking
- **Watch Claude Code** for resolution of the billing crisis — if fixed, its ecosystem and feature depth remain unmatched
- **Monitor OpenCode** for provider-agnostic workflows, especially if you use local models or multiple API providers
- **Avoid Kimi Code and DeepSeek TUI** until migration/documentation issues stabilize
- **All tools** need better compaction and context management — factor this into your session length expectations
- **Windows users** should budget for platform friction regardless of tool choice

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-08 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following PRs attracted the most community discussion and attention:

- **#514 – document-typography** — Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Discussion flagged this as a universal pain point affecting *every* document Claude generates. **Status:** Open | [PR #514](https://github.com/anthropics/skills/pull/514)

- **#486 – ODT skill** — OpenDocument text creation, template filling, and ODT-to-HTML conversion. This addresses LibreOffice interoperability, a gap for enterprise users on non-Microsoft stacks. **Status:** Open | [PR #486](https://github.com/anthropics/skills/pull/486)

- **#210 – Improve frontend-design skill clarity** — Comprehensive rewrite to make every instruction actionable within a single conversation. Discussion centered on specificity vs. verbosity tradeoffs in SKILL.md design. **Status:** Open | [PR #210](https://github.com/anthropics/skills/pull/210)

- **#83 – skill-quality-analyzer & skill-security-analyzer** — Meta-skills that evaluate skills across structure, documentation, and security dimensions. The community sees this as foundational for the ecosystem's quality baseline. **Status:** Open | [PR #83](https://github.com/anthropics/skills/pull/83)

- **#538/#539/#541 – Cross-platform bug fixes (Lubrsy706)** — A cluster of small, targeted PRs fixing case-sensitive file references on Linux, YAML parsing edge cases, and DOCX `w:id` collisions. These received sustained discussion around operating system compatibility. **Status:** Open | [PR #538](https://github.com/anthropics/skills/pull/538) | [PR #539](https://github.com/anthropics/skills/pull/539) | [PR #541](https://github.com/anthropics/skills/pull/541)

- **#1140 – agent-creator meta-skill** — A meta-skill for generating task-specific agent sets, with fixes for multi-tool evaluation and Windows AppData path support. Discussion highlighted demand for composable agent architectures. **Status:** Open | [PR #1140](https://github.com/anthropics/skills/pull/1140)

- **#723 – testing-patterns skill** — Covers the full testing stack (unit, React, E2E, API) with the Testing Trophy model. Community interest signals a need for Claude to understand modern testing philosophy, not just syntax. **Status:** Open | [PR #723](https://github.com/anthropics/skills/pull/723)

- **#568 – ServiceNow platform skill** — Broad ServiceNow assistant covering ITSM, ITOM, SecOps, ITAM/SAM, FSM, SPM, CSDM, and IntegrationHub. Reflects demand for enterprise platform integration. **Status:** Open | [PR #568](https://github.com/anthropics/skills/pull/568)

---

## 2. Community Demand Trends

Analysis of the top Issues reveals six clear demand axes:

1. **Org-wide skill sharing and management** — Issue #228 (13 comments, 7 👍) calls for native organization-wide skill distribution instead of manual `.skill` file sharing via Slack/Teams. This is the most-upvoted issue and indicates enterprise deployment friction.

2. **Evaluation tooling reliability** — Issues #556 and #1169 report that `run_eval.py` yields 0% recall across all queries, making the optimization loop useless. The community needs robust CI-grade evaluation before broader adoption.

3. **Security and trust boundaries** — Issue #492 (7 comments) flags that community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability. This is a structural concern for the repository's governance model.

4. **Skill-creator quality and pedagogy** — Issue #202 (8 comments) argues the official `skill-creator` reads like developer documentation rather than an operational instruction set. The community wants the tool to eat its own dog food.

5. **Cross-platform parity** — Multiple issues reference Windows and Bedrock compatibility gaps. The `run_eval.py` Windows crash (Issue #556) and Bedrock integration (Issue #29) represent adoption blockers for non-macOS users and enterprise AWS customers.

6. **Multi-file reference bundling** — Issue #1220 proposes inline bundling for skills split across multiple reference files, addressing a practical friction point for complex skills.

---

## 3. High-Potential Pending Skills

These active PRs show strong community engagement and are likely to land soon:

- **#1099, #1050 – Windows subprocess and encoding fixes** — Two complementary PRs fixing `run_eval.py` and `run_loop.py` on Windows. Both have been actively updated through May 2026 and address the critical 0% recall bug. | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050)

- **#363 – feature-dev workflow fix** — Fixes TodoWrite overwrite that skips Quality Review and Summary phases. Updated as recently as June 3, 2026, indicating active maintenance. | [PR #363](https://github.com/anthropics/skills/pull/363)

- **#444 – AURELION skill suite** — Four skills (kernel, advisor, agent, memory) delivering a structured cognitive framework. Niche but technically deep; last updated May 6. | [PR #444](https://github.com/anthropics/skills/pull/444)

- **#190 – n8n-builder and n8n-debugger** — Four production-tested community skills including n8n workflow building and `.faf` format expertise. Updated through May 2026; represents the automation workflow demand. | [PR #190](https://github.com/anthropics/skills/pull/190)

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is shifting from **domain-specific skill content** to **meta-infrastructure**: evaluation tooling reliability, cross-platform compatibility, security governance, and org-wide distribution — indicating the ecosystem is maturing from individual experimentation toward production deployment at scale.

---

# Claude Code Community Digest – 2026-06-08

## Today's Highlights

The community remains heavily focused on a long-running usage limit bug (#16157) that has now accumulated nearly 1,500 comments and almost 700 upvotes — a critical pain point for Max subscribers. A new issue reporting that simply saying "hi" triggers an API usage policy violation (#60366) signals potential false positives in the safety layer. Meanwhile, the demand for an official Linux Desktop build (#65697) gained 313 upvotes in just a few days, making it the most upvoted feature request this week.

## Releases

No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)

1. **[#16157 – Instantly hitting usage limits with Max subscription](https://github.com/anthropics/claude-code/issues/16157)**
   - **Community reaction**: 691 👍, 1476 comments — by far the most discussed issue.
   - **Why it matters**: Max subscribers report hitting usage caps immediately, often with minimal activity. The sheer volume suggests a systemic billing or quota enforcement problem that directly impacts paying users.

2. **[#60366 – Saying "hi" returns API Error: violates Usage Policy](https://github.com/anthropics/claude-code/issues/60366)**
   - **Community reaction**: 20 👍, 81 comments.
   - **Why it matters**: A basic greeting triggers a policy violation error. Likely an over-aggressive safety filter. Developers rely on Claude Code for daily work; false positives erode trust and productivity.

3. **[#63896 – Usage credits required for 1M context; compaction error on Windows](https://github.com/anthropics/claude-code/issues/63896)**
   - **Community reaction**: 21 👍, 36 comments.
   - **Why it matters**: Users with large context windows hit an opaque credit wall. The error message references a settings page but the fix isn’t well-documented.

4. **[#45937 – Dispatch conversation permanently offline despite Cowork tasks working](https://github.com/anthropics/claude-code/issues/45937)**
   - **Community reaction**: 12 👍, 33 comments.
   - **Why it matters**: The main Dispatch thread shows “offline” on mobile while Cowork tasks run fine — a confusing and blocking bug for remote workflows.

5. **[#63015 – Auto-compact never triggers at 100% context used](https://github.com/anthropics/claude-code/issues/63015)**
   - **Community reaction**: 17 👍, 25 comments.
   - **Why it matters**: The statusline reports full context, but compaction never fires. Users are forced to manually intervene, breaking long sessions. A regression after v2.1.153.

6. **[#65697 – Official Linux Desktop build (Ubuntu/Debian)](https://github.com/anthropics/claude-code/issues/65697)**
   - **Community reaction**: 313 👍, 23 comments — strongest upvote count in the dataset.
   - **Why it matters**: Linux desktop support is the most-requested platform feature. Many developers work on Linux and currently lack a native GUI experience.

7. **[#25128 – Drag and drop broken in VS Code extension](https://github.com/anthropics/claude-code/issues/25128)**
   - **Community reaction**: 39 👍, 19 comments.
   - **Why it matters**: A long-standing regression (since v2.1.6) in the VS Code chat panel. Drag-and-drop works in the terminal CLI but not in the extension — a major UX gap for IDE users.

8. **[#62466 – Repeated image processing errors consuming usage limit](https://github.com/anthropics/claude-code/issues/62466)**
   - **Community reaction**: 16 👍, 18 comments.
   - **Why it matters**: “Image couldn’t be processed” errors waste API calls and tokens. Users are billed for failed requests — a double penalty.

9. **[#32982 – Remote Control sessions die after ~20 min idle](https://github.com/anthropics/claude-code/issues/32982)**
   - **Community reaction**: 59 👍, 12 comments.
   - **Why it matters**: Remote Control sessions silently drop due to server TTL ignoring keepalives. Critical for CI/CD and long-running agent workflows.

10. **[#63604 – Opus 4.8 emits malformed tool_use blocks; entire response discarded](https://github.com/anthropics/claude-code/issues/63604)**
    - **Community reaction**: 8 👍, 4 comments (duplicate, open).
    - **Why it matters**: A model regression where Opus 4.8 produces invalid tool calls, forcing full response discards. Opus 4.7 works fine — suggests a recent model-side issue.

## Key PR Progress

Only two pull requests were updated in the last 24 hours, indicating a quiet development day on the repository:

- **[#58673 – (unlabeled PR) "s"](https://github.com/anthropics/claude-code/pull/58673)**  
  *Status*: Open (created 2026-05-13, updated 2026-06-07)  
  Summary lacks detail; likely a minor or placeholder change.

- **[#39370 – feat(plugins): add frontend-design-system plugin](https://github.com/anthropics/claude-code/pull/39370)**  
  *Status*: Closed (merged 2026-06-07?)  
  Adds a plugin that generates design specs (wireframes, OKLCH color theory, design tokens) before code implementation. Complements the existing `frontend-design` plugin.

## Feature Request Trends

From the enhancement-labeled issues and upvote patterns, the community is pushing for:

1. **Linux Desktop Build** (#65697, 313 👍) — by far the loudest request. Developers on Linux want parity with macOS and Windows Desktop experiences.
2. **Better usage/credits management** — multiple issues around Max plan limits (#16157), 1M context credits (#63896), and capped plans (#51141 – request for a “100x” tier). Users want clearer metering and higher ceilings.
3. **Improved Remote Control reliability** (#32982, 59 👍) — keepalive handling, idle timeouts, and session persistence are top of mind.
4. **Memory system consistency** (#59529, #66143) — users report that saved memories are ignored across sessions, forcing repeated corrections.
5. **TTS and voice mode** (#42700, 12 👍) — accessibility feature requested for Remote Control sessions.
6. **Third-party provider compatibility** (#46416) — context window detection fails for Anthropic-compatible endpoints, limiting flexibility.
7. **Plugin/MCP ecosystem stability** (#58510, #64799) — Windows spawn issues, sandbox failures on merged-usr Linux.

## Developer Pain Points

Recurring frustrations from the last 24 hours of issue activity:

- **Usage/cost surprises**: Max plan users hit invisible limits (#16157), failed image requests still count against quotas (#62466), and credits are required for large contexts without clear notification (#63896).
- **Context compaction silent failures**: Auto-compact doesn’t trigger even at 100% (#63015), and manual compaction fails with confusing credit errors.
- **Remote Control unreliability**: Sessions drop after ~20 min of idle (#32982), main Dispatch shows offline while Cowork tasks work (#45937).
- **Windows and Linux platform gaps**: Drag-and-drop missing in VS Code on any platform (#25128), Windows lacks clipboard image paste (#66119), MCP servers fail on Windows with `spawn ENOENT` (#58510), Linux sandbox broken on Arch (#64799).
- **Model quality regressions**: Opus 4.8 produces malformed tool calls (#63604), “hi” triggers policy violation (#60366), and memory directives are ignored (#59529).
- **Authentication inconsistencies**: `claude auth status` says logged in but CLI requires re-login (#65725), organizational policies block personal subscriptions (#63886).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-06-08

## Today’s Highlights
No new releases landed in the last 24 hours. Community attention is focused on persistent Windows sandbox and plugin reliability issues, with **os error 740** appearing in multiple threads. The top-voted issue—a **Linux desktop app request**—crossed 500 👍, signaling strong demand for cross-platform support. On the PR side, OpenAI engineers continue hardening the agent sandbox and plugin caching, while two approved-fix PRs for unified-exec permissions are now closed.

## Releases
None in the last 24 hours.

---

## Hot Issues (10 picked from top 30)

1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Enhancement, 100 comments, 510 👍*  
   The most-liked open issue. User requests a native Linux desktop app after macOS power consumption issues made Codex App unusable on their Mac. Community upvotes reflect broad Linux user demand.

2. **[#25715 – Codex App unusably slow with WSL as agent environment](https://github.com/openai/codex/issues/25715)**  
   *Bug, 36 comments, 34 👍*  
   Windows users on WSL2 report routine turns take minutes. Performance regression appears tied to recent sandbox changes. Pro subscribers affected.

3. **[#12299 – “You’ve hit your usage limit” despite 10% rate limit remaining](https://github.com/openai/codex/issues/12299)**  
   *Bug, 19 comments*  
   Plus subscribers show quota draining incorrectly. User reports rationing weekly limit but still hitting false ceilings. Likely a billing or counter bug.

4. **[#26892 – gpt-5.5 listed as available but requests fail with 404 Model not found](https://github.com/openai/codex/issues/26892)**  
   *Bug, 17 comments, 9 👍*  
   Critical for developers relying on the latest model. Local metadata shows `gpt-5.5` available, but responses endpoint returns 404. Workaround: use `gpt-5.4`. Opened yesterday, already 17 comments.

5. **[#11881 – GitHub PR review fails: “To use Codex here, create a Codex account…”](https://github.com/openai/codex/issues/11881)**  
   *Bug, 16 comments, 28 👍*  
   Auth connector enabled but Codex still refuses to review PRs. Users have revoked and reconnected multiple times. Impacts CI/CD workflows.

6. **[#17265 – MCP OAuth tokens not auto-refreshed even with stored refresh_token](https://github.com/openai/codex/issues/17265)**  
   *Bug, 13 comments, 20 👍*  
   Codex persists refresh tokens but never uses them. MCP tool calls silently fail after access token expiry. Developers must manually restart or re-auth.

7. **[#23131 – TypeScript SDK JSONL parser fails on multiline MCP tool results](https://github.com/openai/codex/issues/23131)**  
   *Bug, 11 comments*  
   Business workspace users encounter silent failures when MCP tools return multi-line strings. A patch is available in the thread but not yet merged.

8. **[#25362 – Windows sandbox setup refresh OS error 740](https://github.com/openai/codex/issues/25362)**  
   *Bug, 9 comments, 5 👍*  
   Computer Use on Windows fails with `spawn setup refresh` error. Users on Windows 11 25H2 affected. Multiple duplicates (see #24050, #25419).

9. **[#7808 – Running out of context window is immediately fatal to chat thread](https://github.com/openai/codex/issues/7808)**  
   *Bug, 9 comments, 8 👍*  
   Long-running chats end abruptly when context fills; no warning or graceful degrade. Users want progressive compaction or summarization.

10. **[#26512 – Pro 5x weekly limit dropped after June 1; quota drains passively](https://github.com/openai/codex/issues/26512)**  
    *Bug, 4 comments*  
    $100/month Pro 5x users report unexplained quota consumption and a sudden limit drop. Suggests a backend migration issue or meter bug.

---

## Key PR Progress (10 picked from top 20)

1. **[#26937 – Test Windows managed deny-read enforcement](https://github.com/openai/codex/pull/26937)**  
   *Fixes a security hole where Python subprocess could bypass `deny_read` permission. Adds sandbox-level enforcement.*

2. **[#26934 – Prune stale curated plugin caches](https://github.com/openai/codex/pull/26934)**  
   *Removes cached plugins no longer in the curated marketplace. Solves the “stale Google Sheets plugin” problem.*

3. **[#26932 – Use cached remote plugin catalog for plugin list](https://github.com/openai/codex/pull/26932)**  
   *Improves UI responsiveness by serving plugin listings from local cache instead of blocking on remote API.*

4. **[#26662 – Filter threads by parent](https://github.com/openai/codex/pull/26662)**  
   *Enables apps to query child threads of a parent. Needed for subagent coordination and recovery after missing live events.*

5. **[#26920 – Add Python SDK goal turns](https://github.com/openai/codex/pull/26920)**  
   *Exposes `goal=True` on Python `run` and `turn`. Supports atomic goal start and rollover-aware control for long-running agent tasks.*

6. **[#26923 – Add HTTP window ID to Responses client metadata](https://github.com/openai/codex/pull/26923)**  
   *Sends window ID as `client_metadata` for backend tracing. Assists debugging rollback and compaction lineage.*

7. **[#25232 – Derive window generation from effective rollout lineage](https://github.com/openai/codex/pull/25232)**  
   *Fixes incorrect `x-codex-window-id` after rollback. Ensures compaction windows correctly reflect history forks.*

8. **[#26831 – Add global instructions contributor API](https://github.com/openai/codex/pull/26831)**  
   *Introduces an explicit extension point for hosts to supply global instructions without coupling to Config.*

9. **[#25976 – Use stable item IDs for Responses API calls](https://github.com/openai/codex/pull/25976)**  
   *Stabilizes item IDs for round-tripping between Codex and the Responses API. Reduces session drift.*

10. **[#24982 – Honor parent approvals for intercepted execs](https://github.com/openai/codex/pull/24982)**  
    *Fixes an approval UX bug: once a parent sandbox override is approved, child `execv` calls should not prompt again. Now closed (merged).*

---

## Feature Request Trends

- **Linux Desktop App** (#11023, 510 👍): By far the highest-voted feature. macOS performance issues are driving Linux users to request native support.
- **Non-Programmer Mode** (#26556): A proposal for a simplified UI with claim-gating and less technical feedback, aimed at domain experts.
- **Better MCP OAuth Lifecycle** (#17265, #15122): Automatic token refresh and persistence across restarts is repeatedly requested.
- **Context Window Management** (#7808): Users want graceful truncation/compaction instead of hard termination.
- **Cross-Session Project Persistence** (#25500, #25463): Silent disappearance of project threads from UI while data remains on disk is a top usability concern.

---

## Developer Pain Points

- **Windows Sandbox error 740** (7+ open issues): Permissions/helper-path failures plague Windows desktop users, especially with Computer Use and MCP tools. Multiple duplicates (#25362, #24050, #25419, #26929).
- **WSL Performance** (#25715): Agents running in WSL2 are unusably slow. Heavy impact on Windows developer workstation users.
- **Plugin & Connector Instability** (#25809, #25962, #23805): Plugins and browser extensions lose connectivity after restart or short idle periods; Chrome native host manifest disappears.
- **Rate Limit Discrepancies** (#12299, #26512): False “usage limit” errors and inexplicable quota drain erode trust in billing/metering.
- **Model Unavailability** (#26892): `gpt-5.5` shows as available but returns 404. Model rollout mismatches frustrate power users.
- **OAuth Token Non-Refresh** (#17265): MCP OAuth tokens expire silently; no auto-refresh despite stored refresh tokens.
- **macOS Dock Badge** (#10605): Unread notification badge persists with no way to clear within the app. Minor but persistent annoyance.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-08

## Today's Highlights

The gemini-cli repository saw no new releases today but remained active with significant issue triage and several important PRs merging or opening. A long-standing 429 capacity error for the `gemini-3.1-pro-preview` model was closed as a possible duplicate after extensive community discussion, while multiple agent reliability and memory system bugs continue to dominate the open issue tracker. Notably, PRs landed to fix binary content handling in `read_file`, stabilize non-interactive shell execution, and prevent MCP image MIME type misreporting.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#25179 – Frequent 429 "No capacity" for `gemini-3.1-pro-preview`**  
   *Closed as possible duplicate; 9 comments, 2 👍*  
   Users are hitting capacity limits even on trivial prompts. This was the most-discussed issue today and was triaged as a possible duplicate, suggesting the team has an internal resolution path.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/25179)

2. **#21409 – Generalist agent hangs forever**  
   *Open, P1; 7 comments, 8 👍*  
   A critical reliability bug: the generalist sub-agent hangs indefinitely on simple tasks (e.g., folder creation). Workaround exists (instruct model not to use sub-agents), but this is the highest-voted open bug and a clear community pain point.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#22323 – Subagent false success after MAX_TURNS**  
   *Open, P1; 6 comments, 2 👍*  
   `codebase_investigator` incorrectly reports `status: "success"` after hitting the turn limit, masking real failures. Erodes trust in agent output.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22323)

4. **#21968 – Gemini doesn't use custom skills and sub-agents autonomously**  
   *Open, P2; 6 comments*  
   Users have built custom skills (e.g., for Gradle, Git) but the model rarely invokes them unprompted. Points to a gap in tool selection logic.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21968)

5. **#26525 – Add deterministic redaction and reduce Auto Memory logging**  
   *Open, P2; 5 comments*  
   Auto Memory sends transcript content to the model before redaction occurs, and logs existing skill data. Security concern: secrets may be exposed in model context or logs.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/26525)

6. **#26522 – Auto Memory retries low-signal sessions indefinitely**  
   *Open, P2; 5 comments*  
   Sessions the extraction agent declines to read remain "unprocessed" and are resurfaced repeatedly, creating a feedback loop. Needs a marking mechanism for dismissed content.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/26522)

7. **#25166 – Shell command execution stuck on "Waiting input" after completion**  
   *Open, P1; 4 comments, 3 👍*  
   After trivial commands finish, the CLI still shows the shell as awaiting input. High impact for interactive users.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/25166)

8. **#21983 – Browser sub-agent fails on Wayland**  
   *Open, P1; 4 comments, 1 👍*  
   `browser_agent` terminates with `GOAL` but fails silently in Wayland environments. Linux desktop users are affected.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21983)

9. **#22672 – Agent should stop/discourage destructive behavior**  
   *Open, P2; 2 comments, 1 👍*  
   The model occasionally uses `git reset --force` or other dangerous commands when safer alternatives exist. Community is asking for built-in guardrails.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22672)

10. **#24246 – 400 error with >128 tools**  
    *Open, P2; 3 comments*  
    When too many tools are enabled, requests fail with a 400 error. Users expect the agent to prune tool scope automatically.  
    [Link](https://github.com/google-gemini/gemini-cli/issues/24246)

---

## Key PR Progress

1. **#27418 – Non-interactive shell respects `enableInteractiveShell: false`**  
   *Closed, P1*  
   Fixes shell execution service to honor config settings and improves native bridge stability for non-UTF-8 payloads.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/27418)

2. **#27412 – Prevent model fabrication on binary `read_file`**  
   *Closed, P2*  
   When `read_file` returns binary content (e.g., PDFs), the CLI now returns a bare descriptive string instead of injecting a synthetic model "thought" that could mislead reasoning.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/27412)

3. **#27409 – Fix performance test timeout**  
   *Closed, P1*  
   Resolves flaky CI by fixing a timeout in the performance test suite.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/27409)

4. **#23647 – Open Plugins agents support (Stale, closed)**  
   *Size M*  
   Implements automatic discovery, namespacing, and variable expansion for sub-agents inside Open Plugins. Marked stale and closed without merge.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/23647)

5. **#22586 – Programmatic extension search command (Stale, closed)**  
   *Size L*  
   Adds `/extensions search <query>` to both ACP and interactive mode, enabling discovery without the browser UI. Closed as stale.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/22586)

6. **#22585 – `/teleport` command for portable session management (Stale, closed)**  
   *Size XL*  
   Would allow moving active sessions between machines (e.g., laptop to remote server). Closed as stale.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/22585)

7. **#22461 – Visual validation and TTY smoke test framework (Stale, closed)**  
   *Size M*  
   Adds high-fidelity terminal snapshots and integration loop tests for UI regression detection. Closed as stale.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/22461)

8. **#27735 – Changelog generation guide**  
   *Open, Size M*  
   Adds a troubleshooting guide for the automated release notes system to aid maintainer handoff.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/27735)

9. **#27733 – Sniff MCP image MIME types**  
   *Closed, Size M*  
   Detects actual image format via magic bytes before sending MCP images as inline data, fixing WebP/PNG/JPEG/GIF misreporting.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/27733)

10. **#27729 – Truncate telemetry metric attributes to 1024 chars**  
    *Open, P2*  
    Prevents GCP export errors by truncating long attribute values, stopping Node.js stack traces from flooding the terminal during JSON output.  
    [Link](https://github.com/google-gemini/gemini-cli/pull/27729)

---

## Feature Request Trends

- **AST-aware tooling**: Multiple issues (e.g., #22745, #22746, #22747) propose using AST-aware CLI tools for file reads, codebase mapping, and search to improve agent precision and reduce token waste.
- **Agent self-awareness and safety**: Users want the CLI to understand its own mechanics (#21432), avoid destructive commands (#22672), and enforce safe defaults for git/DB operations.
- **Memory system quality improvements**: Auto Memory (issues #26516, #26522, #26523, #26525) needs better redaction, retry logic, and patch validation to prevent leaks and wasted processing.
- **Evaluation and test reliability**: Engineering requests for stabilized internal evals (#23166) and "always pass" steering tests (#23313) show a focus on making testing trustworthy and actionable.
- **Remote and background agents**: Sprint-level work on remote agents with advanced auth (#20303) and background task execution (PR #15674) indicate ongoing investment in distributed execution.

---

## Developer Pain Points

- **Agent reliability**: The most frequent frustrations involve agents hanging (#21409), returning false success after turn limits (#22323), or ignoring user-configured skills (#21968).
- **Model capacity limits**: 429 errors for popular models (#25179) disrupt workflows, though this appears to be a known internal capacity issue rather than a CLI bug.
- **Configuration inconsistencies**: Browser agent ignores `settings.json` overrides (#22267), and sub-agents run despite being disabled (#22093), undermining user control.
- **Terminal and UI glitches**: Shell execution gets stuck on "Waiting input" (#25166), terminal resize causes flicker (#21924), and exiting external editors corrupts display (#24935).
- **Destructive behavior**: The model occasionally uses forceful or irreversible commands (#22672) without prompting for confirmation, raising trust and safety concerns in production environments.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-08

## Today’s Highlights  
Corporate networking remains the top friction point: an open issue (#333) around SSL inspection proxies continues to draw attention, and a new feature request (#3477) asks for enterprise‑grade OTel authentication. Meanwhile, a long‑standing bug (#3216) where the agent enters an infinite directory‑listing loop during long sessions has sparked a refund request, highlighting reliability concerns for power users. On the platform side, a package‑licensing question (#2294) from Arch Linux maintainers and a FreeBSD install‑script bug (#3710) underscore ongoing distribution challenges.

## Releases  
No new releases in the last 24 hours.

## Hot Issues  
1. **[#333 – SSL inspection failure in corporate environments](https://github.com/github/copilot-cli/issues/333)**  
   *Open*, labeled `area:authentication`, `area:enterprise`, `area:networking`. The CLI cannot connect behind MITM proxies even with system certificates installed. 4 👍, 5 comments – a persistent blocker for enterprise adopters.

2. **[#2828 – Weekly rate limiting – better messaging](https://github.com/github/copilot-cli/issues/2828)**  
   *Closed*. Request to include actionable suggestions when the weekly rate limit is hit. Community agrees that “wait for reset” is unhelpful without guidance.

3. **[#3216 – Infinite compaction/directory loop on long sessions](https://github.com/github/copilot-cli/issues/3216)**  
   *Open*, labeled `area:sessions`, `area:context-memory`. After ~136 turns with a PDF attachment, the agent loops in directory listing and memory compaction. User requests a refund. Low engagement (2 comments) but signals a critical edge‑case.

4. **[#3477 – Enterprise OTel auth: mTLS and dynamic headers](https://github.com/github/copilot-cli/issues/3477)**  
   *Open*, labeled `area:enterprise`, `area:networking`. Only static `OTEL_EXPORTER_OTLP_HEADERS` is supported; request parity with Claude Code’s dynamic auth and mTLS. 1 comment.

5. **[#2294 – License clarification for Linux distro packaging](https://github.com/github/copilot-cli/issues/2294)**  
   *Open*, labeled `area:platform-linux`. Arch Linux maintainers ask whether Section 2 of the license permits packaging in non‑commercial distro repos. Only 2 👍 but strategically important for Linux distribution.

6. **[#3709 – `/model` should support BYOK/local providers](https://github.com/github/copilot-cli/issues/3709)**  
   *Open*, [triage]. Currently the `/model` picker only lists GitHub‑hosted models, ignoring local BYOK providers. User wants to switch models freely within a session.

7. **[#3712 – ReFS / Dev Drive local‑sandbox limitation on Windows](https://github.com/github/copilot-cli/issues/3712)**  
   *Open*, [triage]. A friendly question asking for documentation about local‑sandbox incompatibility with ReFS or Dev Drive volumes. No comments yet.

8. **[#3711 – Copilot CLI version not updated in Windows Registry](https://github.com/github/copilot-cli/issues/3711)**  
   *Open*, [triage]. After `/update` to v1.0.60, the Registry entry still shows the old version. Likely a packaging glitch.

9. **[#3710 – Install script misidentifies FreeBSD as Windows](https://github.com/github/copilot-cli/issues/3710)**  
   *Open*, [triage]. `curl -fsSL https://gh.io/copilot-install | bash` fails on FreeBSD because the script assumes any non‑Linux, non‑Darwin is Windows. 0 comments but a clear bug.

10. **[#3396 – Confusing error when `GITHUB_TOKEN` (Actions token) is set](https://github.com/github/copilot-cli/issues/3396)**  
    *Closed*. In GitHub Actions, an installation token is silently picked up and forwarded to the Copilot backend, resulting in a 400 error. No comments – likely fixed, but the scenario remains confusing for CI users.

## Key PR Progress  
Only one PR was updated in the last 24 hours:  
- **[#3708 – “Add files via upload”](https://github.com/github/copilot-cli/pull/3708)**  
  *Open*, created by a user with a suspicious naming pattern. No description, no comments, 0 👍. Appears to be a non‑functional upload and is unlikely to be merged. No meaningful code changes to report.

## Feature Request Trends  
- **Enterprise networking & authentication**: Multiple issues demand better support for corporate proxies (#333), dynamic OTel headers and mTLS (#3477), and improved token handling in CI (#3396).  
- **Model flexibility**: Users want the `/model` command to include BYOK/local providers (#3709), not just GitHub‑hosted models.  
- **Linux distribution**: The licensing ambiguity (#2294) is a blocker for packaging in distro repositories like Arch Linux’s.  
- **Rate limit UX**: Request for actionable feedback when hitting limits (#2828).  

## Developer Pain Points  
- **SSL/TLS proxy incompatibility** (#333) – the #1 enterprise blocker, with no clear workaround.  
- **Long‑session instability** (#3216) – infinite loops and excessive memory compaction erode trust for heavy users.  
- **Confusing authentication errors** (#3396) – silent fallback to `GITHUB_TOKEN` causes mysterious 400 failures in CI.  
- **Install script fragility** (#3710) – FreeBSD misdetected as Windows prevents non‑Linux users from getting started.  
- **Windows Registry sync** (#3711) – version mismatches after update create confusion for enterprise deployment tools.  
- **Sandbox platform limits** (#3712) – undocumented ReFS/Dev Drive incompatibility on Windows forces users to guess why local sandbox fails.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-06-08**.

---

## Kimi Code CLI Community Digest
**Date:** 2026-06-08
**Source:** github.com/MoonshotAI/kimi-cli

### 1. Today's Highlights
The community is in a state of transition, with significant feedback surfacing around the migration from `kimi-cli` (v1.x) to the new `kimi-code` (v0.x). A spike of seven issues in the last 24 hours highlights confusion over state migration, quota attribution, and installation quirks, alongside frustration regarding the product's strategic pivot. The most active feature request pushes for **multi-device session handoff**, signaling a desire for a cloud-connected, persistent workflow.

### 2. Releases
*No new releases in the last 24 hours.*

### 3. Hot Issues
*(All 7 recent issues are included below; none met the 10-item threshold for exclusion)*

1.  **[#2269] [Feature Request] Remote Control / Multi-Device Session Handoff**
    - **Why it matters:** The top-voted feature request (5 comments) emphasizes a critical workflow gap. Users want to start a session on a laptop and resume it on a phone or web UI. This is a high-impact ask for a CLI tool aiming for developer ubiquity.
    - **Link:** MoonshotAI/kimi-cli Issue #2269

2.  **[#2381] [CLOSED] Community Division & Product Strategy**
    - **Why it matters:** A user expresses strong frustration over the creation of `kimi-code` as a separate entity, accusing the team of splitting the community. The issue was closed, but the sentiment (4 comments) reflects a significant trust risk among existing users who viewed `kimi-cli` as a long-term productivity investment.
    - **Link:** MoonshotAI/kimi-cli Issue #2381

3.  **[#2437] [OPEN] Migration Feedback: Unclear State & Quality Regression**
    - **Why it matters:** This is a deep-dive bug report detailing confusion during the `kimi-cli -> kimi-code` migration. The user reports unclear state storage, quota attribution issues, and a perceived drop in agent quality. This is a critical signal for the engineering team regarding onboarding and maintainability.
    - **Link:** MoonshotAI/kimi-cli Issue #2437

4.  **[#2440] [OPEN] Clickable Symbol / Line References in Chat Panel**
    - **Why it matters:** A UX improvement request. While inline file paths are clickable, the inability to click on function/method names to jump to definition breaks a core IDE-like workflow, creating friction for code review and navigation.
    - **Link:** MoonshotAI/kimi-cli Issue #2440

5.  **[#2439] [BUG] Compaction Error with Local Ollama Model**
    - **Why it matters:** A blocking bug for users running the tool with local models. The `compaction.unable` error when reviewing a project suggests a backend compatibility issue or a missing fallback for non-cloud providers.
    - **Link:** MoonshotAI/kimi-cli Issue #2439

6.  **[#2438] [BUG] Unknown Status & Inability to Dive into Agentic Session**
    - **Why it matters:** A core functionality failure. The agent session status is reported as "unknown," preventing users from reviewing or rerunning previous agentic steps. This severely impacts debugging and iterative development.
    - **Link:** MoonshotAI/kimi-cli Issue #2438

7.  **[#2436] [BUG] Installation Failed / Indecisive State**
    - **Why it matters:** A confusing UX bug where an installation script reports both a success ("The new Kimi Code is installed ✓") and a failure state simultaneously. This erodes confidence in the installer's reliability.
    - **Link:** MoonshotAI/kimi-cli Issue #2436

### 4. Key PR Progress
*(Only 1 PR was updated in the last 24h)*

1.  **[#774] [CLOSED] fix: correct module-name type in pyproject.toml**
    - **Description:** A straightforward fix for a TOML parsing error (`invalid type: sequence, expected a string`) that was blocking `make prepare` during development setup.
    - **Significance:** Though small, this fix addresses a developer workflow barrier that prevents new contributors from building the project.
    - **Link:** MoonshotAI/kimi-cli PR #774

### 5. Feature Request Trends
The most requested direction is **session continuity and multi-device workflows**. Issue #2269 (Remote Control / Handoff) is the standout request, indicating a strong desire for Kimi to function as a cloud-backed, persistent coding assistant rather than a strictly local session. The follow-up request for **clickable symbol references** (#2440) points to a community that expects IDE-level interaction quality from the chat panel.

### 6. Developer Pain Points
The dominant pain point this week is the **confusing and seemingly premature migration** from `kimi-cli` to `kimi-code`. Recurring frustrations include:
- **Unclear migration state:** Users don't know which binary is running or where their data is stored (#2436, #2437).
- **Perceived quality regression:** Reports of agent quality dropping post-migration (#2437) and "unknown" agentic session states (#2438).
- **Local model compatibility:** The `kimi-code` agent fails when pointing at local Ollama models (#2439), damaging trust for users who prefer local/offline workflows.
- **Community trust erosion:** The product strategy pivot is causing active subscription reevaluation (#2381), a high-risk signal for user retention.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-08

## Today's Highlights

The OpenCode community remains active with strong discussion around sandboxing and model compatibility. A long-standing request for terminal sandboxing (#2242) continues to attract engagement, while multiple reports of issues with free model usage limits and the new Gemma 4 family are dominating recent conversations. Several important regressions, including a broken AWS Bedrock SSO provider in v1.16 and WSL desktop bugs, have been addressed through incoming PRs.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[Sandbox agent terminal access (#2242)](https://github.com/anomalyco/opencode/issues/2242)** — 63 comments, 51 👍. Community asks for a way to restrict agent terminal commands to the current directory, citing macOS seatbelt equivalents in other CLIs. High engagement suggests this is a top security/UX concern.

2. **[Free model "free usage exceeded" error (#15585)](https://github.com/anomalyco/opencode/issues/15585)** — 47 comments, 12 👍. Users report all three free models return usage-limit errors. The author spent 6+ hours in sessions before hitting this. Confusion persists about whether OpenCode enforces free usage caps.

3. **[Context awareness not working (#3472)](https://github.com/anomalyco/opencode/issues/3472)** — 37 comments, 25 👍. Despite VSCode extension claiming context awareness, selected lines are not recognized by agents. Community recommends improving documentation and behavior — a key UX gap.

4. **[Gemma 4 (e4b) tool calling fails via Ollama (#20995)](https://github.com/anomalyco/opencode/issues/20995)** — 26 comments, 47 👍. Model returns correct `tool_calls` in streaming responses, but OpenCode fails to recognize them. Second-highest upvote count today. Affects local Ollama users wanting to use Gemma 4 for tool-driven workflows.

5. **[Agent ignores rules after session compaction (#3099)](https://github.com/anomalyco/opencode/issues/3099)** — 25 comments, 1 👍. User with GitOps/FluxCD setup reports agent violates explicit no-commit rules post-compaction. Highlights a critical reliability issue in stateful session management.

6. **[Gemma-4-26b/31b tool loop failures (#21034)](https://github.com/anomalyco/opencode/issues/21034)** — 18 comments, 19 👍. Even with latest tokenizer fixes and patched engines (LM Studio, llama.cpp), Gemma 4 models are unusable in OpenCode. Community is actively testing provider-side patches.

7. **[OpenCode 1.4.3 hangs with local Ollama provider (#22132)](https://github.com/anomalyco/opencode/issues/22132)** — 9 comments, 4 👍. Simple prompts hang while `/v1/chat/completions` works directly. Suggests a compatibility layer issue between OpenCode and the OpenAI-compatible adapter for Ollama.

8. **[Azure Foundry OpenAI setup unclear (#31239)](https://github.com/anomalyco/opencode/issues/31239)** — 11 comments. User tried many combinations with no success connecting to Azure OpenAI endpoint. Despite machine connectivity verified independently, OpenCode fails to authenticate — indicates a configuration-guidance gap.

9. **[Regression: AWS Bedrock SSO broken in v1.16 (#31147)](https://github.com/anomalyco/opencode/issues/31147)** — 6 comments. Error about credential provider failure (`E is not a function`) blocks all inference. A clear regression affecting enterprise users on SSO.

10. **[Orchestration leakage during compaction (#28355)](https://github.com/anomalyco/opencode/issues/28355)** — 4 comments. On Windows, after sending minimal prompts ("hi", "banana") in Build mode, orchestration state leaks into compacted sessions. Points to a subtle state management bug.

11. **[Prune clears read results causing re-attachment (#30807)](https://github.com/anomalyco/opencode/issues/30807)** — 4 comments. Two bugs in pruning: compacted state skips instruction files, and early-exit skips older prunable tools. Affects long-running sessions with auto-attached instruction files like AGENTS.md.

---

## Key PR Progress

1. **[TUI transcript filtering (#31294)](https://github.com/anomalyco/opencode/pull/31294)** — Adds web-oriented transcript visibility mode, filtering out internal steps, snapshots, patches, and pending states. Requires compliance review. Likely to improve TUI readability for power users.

2. **[JDTLS/KotlinLS LSP timeout fix (#25649)](https://github.com/anomalyco/opencode/pull/25649)** — Increases LSP initialize timeout from default to handle Gradle sync (60–180s). Closes #23982. Critical for Java/Kotlin developers using JVM-based projects.

3. **[Respect MCP server capabilities (#31271)](https://github.com/anomalyco/opencode/pull/31271)** — Keeps prompt-only and resource-only MCP servers connected without requiring `tools/list`. Logs discovery gracefully. Fixes compatibility with many existing MCP servers.

4. **[OpenCode Connector ecosystem docs (#31183)](https://github.com/anomalyco/opencode/pull/31183)** — Adds a community VSCode extension to the ecosystem page across 17 locale translations. Low-effort, high-impact documentation improvement.

5. **[Fix WSL desktop bugs (#31095)](https://github.com/anomalyco/opencode/pull/31095)** — Fixes `can't access distroReady before initialization`, server removal from sidebar, and stale version reporting. Closes #31097. Important for Windows/Linux hybrid users.

6. **[Snapshot sidecar lifecycle fix (#31283)](https://github.com/anomalyco/opencode/pull/31283)** — Stabilizes Git-based snapshot capture: no longer stuck behind stale index lock, early Git failures no longer terminate Desktop server, and server state is properly cleaned up.

7. **[Node.js compatibility for TUI debounce (#31211)](https://github.com/anomalyco/opencode/pull/31211)** — Replaces `@solid-primitives/scheduled` with manual debounce to fix no-op behavior under `conditions: ["node"]`. Closes #31182. Fixes TUI responsiveness in Node.js environments.

8. **[Retry empty stream truncations (#26167)](https://github.com/anomalyco/opencode/pull/26167)** — When upstream provider streams end without `stop_reason`, AI SDK emits zero-token finish. This PR retries and discards partial parts. Closes #26170. Stabilizes long-running sessions with flaky providers.

9. **[Cache unsupported MCP prompt lists (#28301)](https://github.com/anomalyco/opencode/pull/28301)** — Caches `-32601` responses from MCP servers that don't implement `prompts/list`. Prevents repeated errors. Closes #27477.

10. **[Strip reasoning from OpenAI-compatible history (#28308)](https://github.com/anomalyco/opencode/pull/28308)** — Removes non-standard `reasoning` fields from chat history sent to OpenAI-compatible providers that reject them. Closes #27852. Fixes compatibility with stricter provider implementations.

11. **[MiniMax trailing tool_call leak fix (#30849)](https://github.com/anomalyco/opencode/pull/30849)** — Adds a targeted sanitizer for MiniMax responses where assistant text leaks a tool-call marker suffix. Closes #30684. Addresses a specific provider artifact that causes parsing errors.

---

## Feature Request Trends

- **Session management enhancements**: Multiple requests for manual session renaming ([#25848](https://github.com/anomalyco/opencode/issues/25848)), /rename command, and better session organization.
- **Local model ecosystem support**: Strong demand for Gemma 4 compatibility improvements ([#20995](https://github.com/anomalyco/opencode/issues/20995), [#21034](https://github.com/anomalyco/opencode/issues/21034)), Ollama hang fixes ([#22132](https://github.com/anomalyco/opencode/issues/22132)), and MiniMax thinking mode variants ([#31180](https://github.com/anomalyco/opencode/issues/31180)).
- **Sandboxing and security**: [#2242](https://github.com/anomalyco/opencode/issues/2242) (sandbox agent) is the most-upvoted feature request today. Users want path-restricted terminal execution for agents.
- **Context awareness improvements**: [#3472](https://github.com/anomalyco/opencode/issues/3472) and [#3095](https://github.com/anomalyco/opencode/issues/3095) both highlight that selected lines in editors are not passed to agents. Community wants automatic context inclusion.
- **MCP and resource management**: Better handling of MCP servers that only implement prompts or resources (no tools), and fixing empty MCP lists in web UI ([#30487](https://github.com/anomalyco/opencode/issues/30487)).
- **LaTeX rendering in web UI**: [#24426](https://github.com/anomalyco/opencode/issues/24426) requests browser-based LaTeX rendering for math blocks.

---

## Developer Pain Points

- **Free model confusion**: Users repeatedly hit ambiguous "free usage exceeded" errors ([#15585](https://github.com/anomalyco/opencode/issues/15585), [#14273](https://github.com/anomalyco/opencode/issues/14273), [#26145](https://github.com/anomalyco/opencode/issues/26145)), with unclear documentation on actual free-tier limits.
- **Local provider instability**: Ollama hangs ([#22132](https://github.com/anomalyco/opencode/issues/22132)), Gemma 4 tool-call failures ([#20995](https://github.com/anomalyco/opencode/issues/20995), [#21034](https://github.com/anomalyco/opencode/issues/21034)), and upstream idle timeouts on reasoning models ([#30002](https://github.com/anomalyco/opencode/issues/30002), [#28957](https://github.com/anomalyco/opencode/issues/28957)) are top friction points for self-hosted users.
- **Provider configuration friction**: Azure Foundry ([#31239](https://github.com/anomalyco/opencode/issues/31239)) and AWS Bedrock SSO ([#31147](https://github.com/anomalyco/opencode/issues/31147)) lack clear setup guidance, with the latter being a regression.
- **Session compaction and pruning bugs**: Rules being lost after compaction ([#3099](https://github.com/anomalyco/opencode/issues/3099)), orchestration leakage ([#28355](https://github.com/anomalyco/opencode/issues/28355)), and pruning clearing read results ([#30807](https://github.com/anomalyco/opencode/issues/30807)) undermine user trust in long-running sessions.
- **Cross-platform inconsistencies**: Windows-specific issues include LF line endings breaking batch files ([#31224](https://github.com/anomalyco/opencode/issues/31224)) and blank code blocks in TUI on CentOS 7 ([#28656](https://github.com/anomalyco/opencode/issues/28656)). Chinese input support is also broken in TUI ([#31217](https://github.com/anomalyco/opencode/issues/31217)) and autocompletion ([#27290](https://github.com/anomalyco/opencode/issues/27290)).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-06-08

**Repository:** [earendil-works/pi](https://github.com/earendil-works/pi)  
**Data snapshot:** Issues and PRs updated in the last 24h.

---

## 1. Today's Highlights

A burst of activity from contributor `dyyz1993` landed three quality‑of‑life improvements in the `coding‑agent` package: required bash descriptions with default timeouts, post‑compaction context‑usage estimation, and service reuse when switching sessions in the same working directory. Meanwhile, a new native provider for Requesty was added, and the system prompt now includes the day of the week to help smaller models avoid date hallucinations. The issue tracker remains busy with discussions around slow cold starts, local‑model latency, and the ongoing push to make extension APIs more composable.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues (10 selected)

1. **[#5223 – Anthropic provider modifies thinking blocks in latest assistant message, causing 400 with Opus 4.8 adaptive thinking](https://github.com/earendil-works/pi/issues/5223)**  
   *15 comments, 6 👍*  
   Multi‑turn conversations with Claude Opus 4.8 fail when the provider incorrectly rewrites `thinking` blocks in the last assistant message. A high‑severity interoperability bug for users relying on adaptive thinking. Closed after investigation.

2. **[#3834 – [bug] Fireworks provider not working](https://github.com/earendil-works/pi/issues/3834)**  
   *9 comments, 1 👍*  
   Windows PowerShell users cannot use Fireworks AI despite valid API keys – error cites “5 request validation issues”. Remains closed but highlights a gap in provider error messaging.

3. **[#5188 – [bug] shift+enter submits and does not create new line](https://github.com/earendil-works/pi/issues/5188)**  
   *8 comments, 2 👍*  
   User‑configured keybindings (`shift+enter` → new line) are ignored; the binding still submits. Affects TUI multiline editing. Community suggestion: enforce keybinding precedence.

4. **[#5469 – Feature request: Collapse MCP tool results by default (with `settings.json` opt‑out)](https://github.com/earendil-works/pi/issues/5469)**  
   *3 comments*  
   Heavy MCP tool users want verbose tool outputs (fetch, Brave search) collapsed by default. No configuration hook exists yet. Gaining traction among agent‑heavy workflows.

5. **[#5464 – [bug] Local models: 3‑5 minute “Working” status latency on basic messages mid‑session](https://github.com/earendil-works/pi/issues/5464)**  
   *3 comments*  
   Using Ollama (`ministral3:8b`) introduces multi‑minute “Working” delays even for trivial messages. A major friction point for local‑first users; likely linked to compaction or context window management.

6. **[#5431 – [bug] Error: No API key found for deepseek](https://github.com/earendil-works/pi/issues/5431)**  
   *4 comments*  
   API key saved in `auth.json` is not recognised on restart. Re‑saving works temporarily but fails again. Suggests a credential‑caching regression.

7. **[#5402 – Slow cold start: eager loading of provider SDKs adds ~2.4s](https://github.com/earendil-works/pi/issues/5402)**  
   *2 comments*  
   Node.js loads 138 MB of provider SDK dependencies at import time before any code runs. Community request: lazy‑load providers or allow selective imports.

8. **[#5428 – [bug] Refining a plan leads to error using plan mode from examples](https://github.com/earendil-works/pi/issues/5428)**  
   *3 comments, 1 👍*  
   Extensions that use the example plan mode crash when the user refines a plan – `Agent is already processing`. Related to message queue handling (#5062). Closed with a fix.

9. **[#5456 – [bug] openai‑responses provider ignores compat.supportsDeveloperRole](https://github.com/earendil-works/pi/issues/5456)**  
   *3 comments*  
   The `openai‑responses` API style sends system prompts as `role: "developer"` even when the model explicitly disables it, causing 400 errors on providers like Together AI.

10. **[#5485 – Include day of week in 'Current date' system prompt injection](https://github.com/earendil-works/pi/issues/5485)**  
    *2 comments*  
    Smaller models consistently hallucinate the day of week. Suggestion: inject `Tuesday, 2026‑06‑08` instead of bare date. Already addressed by PR #5486 (see below).

---

## 4. Key PR Progress (8 merged/closed)

1. **[#5486 – fix: include day of week in Current date system prompt](https://github.com/earendil-works/pi/pull/5486)**  
   *Author: andrea‑tomassi*  
   Adds the day name (e.g., `Tuesday`) to the system prompt date injection, fixing hallucinations on smaller models. Quick turnaround from issue to PR in under 24h.

2. **[#5479 – perf(coding‑agent): reuse services on same‑cwd session switch](https://github.com/earendil-works/pi/pull/5479)**  
   *Author: dyyz1993*  
   Avoids recreating settings, model registry, and auth storage when switching sessions in the same working directory. Reduces overhead during session hopping.

3. **[#5481 – feat(coding‑agent): require bash descriptions and default timeout](https://github.com/earendil-works/pi/pull/5481)**  
   *Author: dyyz1993*  
   Mandates a short description for every `bash` tool call and enforces a default timeout (configurable). Improves auditability and prevents zombie processes.

4. **[#5480 – fix(coding‑agent): estimate context usage after compaction instead of showing null](https://github.com/earendil-works/pi/pull/5480)**  
   *Author: dyyz1993*  
   After compaction, `getContextUsage()` now computes an estimate based on remaining messages instead of returning `null`, so the footer shows meaningful token counts.

5. **[#5472 – feat(ai,coding‑agent): add Requesty as native provider](https://github.com/earendil-works/pi/pull/5472)**  
   *Author: Thibaultjaigu*  
   Requesty, an AI gateway with 60k+ users, is now a first‑class provider. Models under `requesty/…` work out of the box without generic OpenAI endpoint configuration.

6. **[#5471 – fix(coding‑agent): don't unconditionally continue after compaction](https://github.com/earendil-works/pi/pull/5471)**  
   *Author: vifar*  
   Fixes #5463: after auto‑compaction, the agent only continues if there are queued messages (steer/follow‑up), preventing a thrown error when no work is pending.

7. **[#5467 – Include models.json path in migration parse errors](https://github.com/earendil-works/pi/pull/5467)**  
   *Author: cnYui*  
   Malformed `models.json` migration errors now include the absolute file path, making debugging easier. Includes a regression test.

8. **[#5465 – feat: add mineru document‑parsing skill](https://github.com/earendil-works/pi/pull/5465)**  
   *Author: GGzili*  
   Adds a `mineru` skill (Agent Skills standard) for parsing documents (URL/local file upload, polling, extraction). Provides SKILL.md, shell script, and API reference.

---

## 5. Feature Request Trends

- **Configurable collapsing of MCP tool results** – users want a `settings.json` toggle to collapse verbose tool outputs by default.
- **Better session & working directory management** – persistent CWD bridges, session tree auto‑horizontal‑scroll, and ability to change session CWD from extensions.
- **Provider flexibility** – native support for Requesty (just added), cost unit customisation for non‑USD/credit‑based providers, and model‑listing updates for OpenRouter.
- **Exportable public API surface** – repeated requests to expose `RpcExtensionUIRequest`/`RpcExtensionUIResponse`, `waitForIdle`, and other `ExtensionCommandContext` methods from `ExtensionContext`.
- **Slow start mitigation** – proposals to lazy‑load provider SDKs and extract composable `runAgentSession` from the monolithic `main.ts`.

---

## 6. Developer Pain Points

- **Cold start overhead** – ~2.4 seconds spent loading all provider SDKs eagerly; users want selective imports or lazy loading.
- **Local model latency** – several‑minute “Working” delays with Ollama, likely tied to compaction logic or context‑window reset.
- **API key persistence** – credentials saved in `auth.json` are sometimes not read on next launch (DeepSeek, Fireworks).
- **UI inconsistencies** – `shift+enter` binding ignored, literal triple‑backtick fences rendered in Markdown, and clipboard images not attached to model requests in interactive mode.
- **Extension ecosystem friction** – plan‑mode extensions break on refinement, `npm` is required even when using Bun, and built‑in tools cannot be excluded from the sandbox.
- **Session compaction confusion** – post‑compaction context usage showing `null` (now fixed) and auto‑continue triggering errors without queued messages (now fixed).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-08

## 1. Today's Highlights

The Qwen Code team shipped a **nightly release (v0.17.1-nightly)** with a critical CLI fix for copy output in read-only mode, resolving a long-standing pain point from issue #1388 (**read-only mode line numbers bleeds into copied code**). Additionally, a community-driven feature request to support **declarative agent definitions via frontmatter files** (Issue #4821, inspired by Claude Code's pattern) has gained significant attention. A major parallel PR stream is focusing on daemon mode hardening, with **ACP Streamable HTTP transport** achieving full REST parity and a new **session idle reaper** for automatic cleanup landing today.

## 2. Releases

**v0.17.1-nightly.20260608.aea34fa2c**  
Changelog includes:  
- `chore(release): v0.17.1`  
- `fix(cli): skip thought parts in copy output` — directly addresses issue #1388, where read-only mode copied line numbers along with code, making paste unusable.

This nightly release consolidates multiple community contributions and bug fixes, though no stable full release is cut today.

## 3. Hot Issues

1. **#4514 – Daemon capability gaps & prioritized backlog (post v0.16-alpha)**  
   *Author: doudouOUC | 12 comments | 🔥 High engagement*  
   Tracks remaining gaps in the `qwen serve` HTTP/SSE surface after slash-command passthrough. Critical for remote client compatibility (ACP).  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4514)

2. **#4821 – Declarative agent definitions via frontmatter files**  
   *Author: qqqys | 4 comments*  
   Proposes Markdown files with YAML frontmatter for agent definitions, mirroring Claude Code 2.1.167. A high-demand feature for simplifying custom agent creation.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4821)

3. **#1388 – Read-only mode copies line numbers with code (now CLOSED via nightly)**  
   *Author: SunMendi | 3 comments*  
   Long-standing bug finally resolved in today's nightly release. The fix (`/copy code` subcommand) extracts clean code blocks without line numbers.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/1388)

4. **#4782 – ACP Streamable HTTP transport: implementation status & upgrade plan**  
   *Author: chiga0 | 2 comments*  
   Tracks daemon's `/acp` endpoint for ACP-native editors (Zed, Goose, JetBrains). Now merged to achieve full REST parity.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4782)

5. **#4830 – Fallback model support for resilient long-running sessions**  
   *Author: qqqys | 2 comments (CLOSED as duplicate)*  
   Proposed fallback to compatible models when primary is unavailable. Deemed duplicate but reflects growing demand for session reliability.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4830)

6. **#4550 – LAN initialization stuck without internet access**  
   *Author: sotex | 2 comments*  
   Bug report: Qwen CLI hangs on initialization in air-gapped networks. Requires configuration to skip startup checks.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4550)

7. **#1206 – Dynamic multi-model support for OpenAI-compatible APIs**  
   *Author: benzntech | 2 comments, 👍 1*  
   Requests ability to fetch/switch models dynamically from OpenAI-compatible endpoints via `/auth` command, avoiding hardcoded model limits.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/1206)

8. **#4538 – Harden AUTO mode against self-modification and denial bypass**  
   *Author: qqqys | 1 comment (CLOSED), 👍 1*  
   Proposes stronger policy boundaries around agent self-modification and bypass attempts. Important for security/capabilities balance.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4538)

9. **#4568 – Submodule file completion missing in `@` suggestion**  
   *Author: undici77 | 1 comment (CLOSED)*  
   Bug: `@` file completion shows submodule folders but no files inside. Affects IDE and CLI workflows with Git submodules.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4568)

10. **#4744 – `/copy N` to copy Nth-last message**  
    *Author: huww98 | 1 comment (CLOSED)*  
    Request to extend `/copy` command with numeric argument (e.g., `/copy 2` for second-to-last). Merged feature in nightly.  
    [GitHub](https://github.com/QwenLM/qwen-code/issues/4744)

## 4. Key PR Progress

1. **#4779 – Interactive `/stats` dashboard with cross-session tracking**  
   *Author: BenGuanRan | OPEN*  
   Adds three-tab dashboard (Session, Activity, Efficiency) for live CLI metrics. High value for power users.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4779)

2. **#4704 – Honor skill `allowedTools` by auto-approving declared tools**  
   *Author: tanzhenxin | OPEN*  
   Makes `allowedTools` field functional: tools declared in skill frontmatter are auto-approved, reducing friction for skill execution.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4704)

3. **#2838 – Add Bun runtime support**  
   *Author: euxaristia | CLOSED (merged)*  
   Brings 3-5x faster startup, lower memory, native TS support. Significant for performance-sensitive users.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/2838)

4. **#4570 – Supplement triage skill with gate model, intake rules, CI trigger**  
   *Author: yiliang114 | OPEN*  
   Enhances automated issue triage with better maintainer decisions and community follow-up.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4570)

5. **#4732 – Workflow tool P1: minimal `node:vm` sandbox + sequential agent()**  
   *Author: LaZzyMan | OPEN*  
   First phase of Dynamic Workflows: model-authored JS scripts in a sandbox with sequential agent execution.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4732)

6. **#4810 – Fix OpenAI SDK abort listener leak with per-request child controllers**  
   *Author: yiliang114 | OPEN*  
   Isolates SDK's internal listener leak via `createChildAbortController`. Critical for long-running sessions.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4810)

7. **#4812 – `POST /session/:id/branch` for session forking**  
   *Author: doudouOUC | OPEN*  
   Adds HTTP route to fork live sessions without history replay, enabling programmatic branching.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4812)

8. **#4827 – ACP/REST parity: 29 new `_qwen/*` methods + production hardening**  
   *Author: chiga0 | OPEN*  
   Achieves full ACP/REST coverage including session extensions, context usage, dynamic tools, and model switching.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4827)

9. **#4833 – Session idle reaper for automatic cleanup**  
   *Author: chiga0 | OPEN*  
   Adds periodic scanner to close idle sessions (default 30 min TTL), preventing resource leaks.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4833)

10. **#4665 – Add InstructionsLoaded hook for instruction file loading**  
    *Author: qqqys | OPEN*  
    Fires event when instruction/context files are loaded, enabling tool integrations and custom workflows.  
    [GitHub](https://github.com/QwenLM/qwen-code/pull/4665)

## 5. Feature Request Trends

The community is converging on four major directions:

1. **Daemon/Server Mode Expansion** (Issues #4514, #4782, #4827, #4833) — Users demand full ACP Streamable HTTP transport, session management (branching, idle cleanup), and REST parity for remote client integration.

2. **Declarative Agent Extensibility** (Issues #4821, #4704, #4570) — Strong push for YAML/Markdown-based agent definitions, skill auto-approval, and triage enhancements that reduce coding overhead.

3. **Multi-Model & Fallback Support** (Issues #1206, #4830) — Growing need for dynamic model switching, endpoint configuration, and fallback to compatible models for session resilience.

4. **Session & Clipboard UX** (Issues #4744, #4779) — Users want richer `/copy` and `/stats` commands for better productivity and introspection.

## 6. Developer Pain Points

Several recurring friction points emerge:

- **Air-gapped network initialization** (#4550) — CLI hangs when no internet, with no clear configuration to skip startup checks. High impact for enterprise/offline users.
- **Read-only mode line numbers in clipboard** (#1388) — This long-standing bug (now fixed in nightly) made copy-paste from read-only sessions unusable, requiring manual cleanup.
- **Submodule file resolution** (#4568) — IDE `@` completion fails to list files inside Git submodules, breaking navigation in multi-repo projects.
- **Self-hosted LLM parameter type coercion** (#4793) — Self-hosted models return non-string values for tool parameters, causing schema validator rejections for core operations like `edit_file`.
- **Abort controller listener leaks** (#4810) — Long sessions accumulate SDK listeners, causing memory bloat — a subtle but critical performance issue.
- **Session resilience gaps** (#4830) — No fallback when primary model fails, causing hard failures in long-running agent sessions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

Here is the **DeepSeek TUI Community Digest** for **2026-06-08**, based on the provided GitHub data from the `Hmbown/CodeWhale` repository.

---

### 1. Today's Highlights

A major wave of community-driven bug fixes and refactoring landed yesterday, with a batch of five PRs from contributor **HUQIANTAO** targeting concurrency, security, and error-handling issues. A significant caching optimization PR (#2874) was also merged, moving policy descriptions out of the main prompt to improve prefix-cache hit rates. Despite the development activity, no new official release was cut in the last 24 hours.

### 2. Releases

**No new releases in the last 24 hours.** The current stable version remains at **v0.8.52**, with the **v0.9.0** stewardship integration branch (#2762) still open.

### 3. Hot Issues

*(Selected for impact, community engagement, and frequency of mention)*

1.  **[#1177] [bug] 输入缓存命中率太低了** – **24 Comments**
    - *Why it matters:* This is the most active issue in the project. The community is directly comparing CodeWhale's caching performance against a competitor (DeepSeek-Reasonix), which achieves >95% hit rates. The large discrepancy is a critical performance concern that directly impacts API costs.
    - *Community Reaction:* High expectations for improvement; the urgency is palpable.
    - **[Link](Hmbown/CodeWhale Issue #1177)**

2.  **[#743] [bug] token消耗增大了很多** – **13 Comments**
    - *Why it matters:* Users are reporting extreme token consumption ("4亿 tokens in half a day"). This is likely related to the caching issue (#1177) and is a major blocker for cost-sensitive users.
    - *Community Reaction:* Frustration with request density and a clear call for optimizing conversational context.
    - **[Link](Hmbown/CodeWhale Issue #743)**

3.  **[#1969] [question] 程序更名成code whale之后，原先的会话、技能都还在吗** – **8 Comments**
    - *Why it matters:* This is a high-priority migration concern for existing users. The lack of clear documentation on how to migrate sessions and skills from the old name to "CodeWhale" is creating significant friction.
    - *Community Reaction:* Uncertainty and a need for official guidance.
    - **[Link](Hmbown/CodeWhale Issue #1969)**

4.  **[#1579] [enhancement] 这个颜色真的很丑** – **8 Comments**
    - *Why it matters:* Aesthetic feedback is often a sign of a maturing product. While subjective, this issue highlights that the default UI theme is a pain point for users.
    - *Community Reaction:* Users are actively requesting customization or a design refresh.
    - **[Link](Hmbown/CodeWhale Issue #1579)**

5.  **[#2492] [bug] 不具备跨会话记忆** – **5 Comments**
    - *Why it matters:* The lack of persistent memory across sessions undermines the agent's ability to maintain context. This is a core feature request for an AI coding agent.
    - *Community Reaction:* Users note that the agent doesn't read or write memory reliably, making long-term tasks difficult.
    - **[Link](Hmbown/CodeWhale Issue #2492)**

6.  **[#2328] [bug, enhancement] exec_shell 模式可用性不一致** – **4 Comments**
    - *Why it matters:* A critical functionality bug. The `exec_shell` tool works in YOLO mode but fails in Agent mode, contradicting documentation. This is a workflow-breaking inconsistency for users who rely on Agent mode.
    - *Community Reaction:* A documented feature not working correctly is a high-priority fix.
    - **[Link](Hmbown/CodeWhale Issue #2328)**

7.  **[#1620] [enhancement] 思考过程巨慢无比，一个字吐半天** – **5 Comments**
    - *Why it matters:* Performance degradation in the "thinking" phase is a frustrating UX issue. This could be related to the model provider or API endpoint configuration.
    - *Community Reaction:* Users are reporting this as a severe slowdown.
    - **[Link](Hmbown/CodeWhale Issue #1620)**

8.  **[#1556] [bug] deepseek 在 macOS 下的 ghostty 下 会一直闪屏** – **3 Comments**
    - *Why it matters:* Terminal-specific rendering bugs create a poor experience for macOS users of Ghostty, a popular terminal emulator.
    - *Community Reaction:* A clear environment-specific crash investigation is needed.
    - **[Link](Hmbown/CodeWhale Issue #1556)**

9.  **[#2620] [bug] 在执行一个重构任务时，突然之间卡住了** – **3 Comments**
    - *Why it matters:* A "hang-and-crash" scenario during a critical task (refactoring) is a worst-case experience, leading to data loss and user frustration. This has been a recurring theme in the community.
    - *Community Reaction:* Users are becoming "unable to tolerate" this behavior.
    - **[Link](Hmbown/CodeWhale Issue #2620)**

10. **[#2261] [bug] TUI 对话中进程崩溃，输入内容泄漏到 PowerShell 终端** – **3 Comments**
    - *Why it matters:* A security and UX concern. A crash leaking input into the shell could lead to accidental command execution or data exposure.
    - *Community Reaction:* A worrying bug requiring immediate attention.
    - **[Link](Hmbown/CodeWhale Issue #2261)**

### 4. Key PR Progress

*(Selected for impact on stability, performance, and new features)*

1.  **#2892 [OPEN] feat(i18n): localize sandbox elevation dialog across 7 locales** (gordonlu)
    - *Significance:* A major step in internationalization, moving UI dialogs from hardcoded English to a `MessageId`-based translation system. This improves accessibility for the global user base.
    - **[Link](Hmbown/CodeWhale PR #2892)**

2.  **#2874 [CLOSED] feat(cache): slim runtime_prompt to minimal tag, move policy descriptions to system prompt** (LeoAlex0)
    - *Significance:* **Merged.** A critical fix for the caching issue. By moving mode/policy descriptions out of the per-turn prompt, this directly addresses the prefix-cache invalidation problem reported in #1177. This should significantly improve token efficiency and reduce latency.
    - **[Link](Hmbown/CodeWhale PR #2874)**

3.  **#2877 [CLOSED] fix(cache): set temp spillover root in cache_inspect test to survive nix sandbox** (LeoAlex0)
    - *Significance:* **Merged.** A targeted fix for a flaky test in Nix build environments, ensuring CI stability and reliable builds for NixOS users.
    - **[Link](Hmbown/CodeWhale PR #2877)**

4.  **#2107 [CLOSED] feat(tui): FauxStep::Factory for live request-shape assertions** (mvanhorn)
    - *Significance:* **Merged.** An advanced testing utility that allows developers to write assertions against real outgoing `MessageRequest` objects. This is a powerful tool for ensuring request integrity in test suites.
    - **[Link](Hmbown/CodeWhale PR #2107)**

5.  **#2236 [CLOSED] feat: read global AGENTS.md from ~/.agents/ as vendor-neutral fallback** (mvanhorn)
    - *Significance:* **Merged.** A user-experience improvement that allows a global `AGENTS.md` file to be read from `~/.agents/`, providing a vendor-agnostic fallback for `CLAUDE.md`. This simplifies configuration for users who switch between tools.
    - **[Link](Hmbown/CodeWhale PR #2236)**

6.  **#2883 [OPEN] fix: concurrency bugs - mutex handling, thread spawning, and resource management** (HUQIANTAO)
    - *Significance:* Fixes 5 critical concurrency bugs that could cause cascading panics and thread exhaustion. Essential for application stability, especially during multi-agent or MCP sessions.
    - **[Link](Hmbown/CodeWhale PR #2883)**

7.  **#2882 [OPEN] fix: security bugs in execution policy, approval mapping, and tool input validation** (HUQIANTAO)
    - *Significance:* Addresses 5 security vulnerabilities, including a whitespace bypass in the deny rule and a log injection flaw. This is a critical PR for maintaining a secure execution environment.
    - **[Link](Hmbown/CodeWhale PR #2882)**

8.  **#2880 [OPEN] fix: critical bugs in tools, client, and commands** (HUQIANTAO)
    - *Significance:* Resolves 9 critical bugs, including a UTF-8 boundary panic in `clean_pdf_text` and data-related panics. These are direct fixes for user-reported crashes.
    - **[Link](Hmbown/CodeWhale PR #2880)**

9.  **#2888 [OPEN] refactor(commands): extract registry and parser helpers** (aboimpinto)
    - *Significance:* The third layer of a major command-boundary refactor (#2870, #2791). This prepares the internal command structure for future extensibility without changing current behavior.
    - **[Link](Hmbown/CodeWhale PR #2888)**

10. **#2891 [OPEN] feat(i18n): localize approval dialog surface across 7 locales** (gordonlu)
    - *Significance:* Complements #2892 by localizing the approval widget. This further solidifies the planned i18n system for a broader audience.
    - **[Link](Hmbown/CodeWhale PR #2891)**

### 5. Feature Request Trends

- **Persistent Memory & Context:** Users strongly desire the ability to maintain memory across sessions. Issues like #2492 point to a need for a robust, persistent memory system (e.g., semantic memory or file-based recall) that allows the agent to "remember" past tasks.
- **Mode Awareness for AI Agents:** A growing trend is for the AI agent to be fully aware of the current mode (Plan, Agent, YOLO). Issue #2346 highlights that the agent often tries to write files while in Plan mode or fails to switch context efficiently, leading to reduced performance.
- **UI Customization & Polish:** Feedback like #1579 (color scheme) and issues about output/input layout (e.g., #1357, #2244) indicate a strong desire for a more customizable and polished TUI experience, including better scrolling and widget layouts.
- **Multi-Agent & Long-Running Task Reliability:** Users are pushing more complex tasks, such as large-scale refactoring (#2620) and parallel agent processing (#1679). There is a clear need for better handling of long-running, resource-intensive, and parallel agent workflows without crashes or timeouts.
- **Internationalization (i18n):** The recent PRs from `gordonlu` indicate active community interest in making the tool accessible in multiple languages (including Japanese, Vietnamese, Portuguese, and Spanish).

### 6. Developer Pain Points

- **High Token Consumption & Caching:** This is the single biggest pain point. Users are experiencing unsustainable API costs due to poor prefix caching (#1177) and extreme token consumption (#743). This makes the tool expensive and inefficient for frequent use.
- **Application Freezes & Crashes:** A recurring theme is the application becoming unresponsive during long tasks, losing conversation progress (#2739, #1830, #2620). This is a critical trust issue; users are frustrated by losing work mid-session.
- **Terminal-Specific Rendering Bugs:** Users on various terminal emulators (Ghostty, Windows Terminal, Alacritty) report glitches including screen tearing (#1556), UI overlap (#1357), text overflow (#2244, #2620), and input leakage (#2261). This reflects a challenge in maintaining compatibility across all major terminal environments.
- **Inconsistent Tool Behavior:** The difference in `exec_shell` behavior between Agent and YOLO modes (#2328) is a source of confusion and bugs, highlighting the need for clearer mode-to-tool mapping.
- **Windows & WSL2 Compatibility:** A consistent stream of issues (e.g., #1816, #1596) report installation and runtime problems on Windows, particularly within the WSL2 environment, suggesting lower priority given to the Windows ecosystem.
- **Post-Rebrand Migration Confusion:** The project’s rename to "CodeWhale" has introduced significant navigation and documentation issues (#1969), with users unsure how to migrate their existing sessions and skills. This is causing trust erosion among existing users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*