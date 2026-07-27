# AI CLI Tools Community Digest 2026-07-27

> Generated: 2026-07-27 02:11 UTC | Tools covered: 9

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
**Date**: 2026-07-27

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with the major players—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—all demonstrating active development alongside persistent stability challenges. The ecosystem is bifurcating: mature tools (Claude Code, Codex, Copilot CLI) focus on security hardening and enterprise integration, while newer entrants (DeepSeek TUI, Pi) prioritize rapid feature iteration and performance optimization. Cross-cutting concerns around MCP authentication reliability, sandbox isolation, cross-platform parity, and silent failure modes dominate community discussions across all projects, signaling a collective maturation from "can it work?" to "can we trust it in production?"

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | PRs Updated (24h) | Release (24h) | Community Scale Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 7 | None | Moderate (15 👍 on top issue) |
| **OpenAI Codex** | 10 | 10 | None | Very high (852 👍 on #11023) |
| **Gemini CLI** | 10 | 10 | **v0.54.0-nightly** | Moderate (8 👍 on top bug) |
| **GitHub Copilot CLI** | 10 | 0 | None | Low–Moderate (3 👍 on #4163) |
| **Kimi Code CLI** | 1 | 0 | None | Very low (0 👍 on #2559) |
| **OpenCode** | 10 | 10 | None | High (83 👍 on #28846) |
| **Pi** | 10 | 10 | None | Moderate–High (2 👍 on top issue, but 35 issues filed) |
| **Qwen Code** | 10 | 10 | **v0.21.0-nightly** | Moderate (2 P1 security issues closed) |
| **DeepSeek TUI** | 10 | 10 | None (v0.9.2 WIP) | High (10+ PRs/day, 17 comments on #3793) |

**Key observations**:
- Codex commands the highest raw community demand (852 👍 for Linux desktop), but Gemini CLI and DeepSeek TUI show the highest *development velocity* (10 PRs each, daily releases for Gemini).
- Copilot CLI had zero PR activity—a notable pause for a major GitHub-backed tool.
- Kimi Code is effectively dormant for this reporting period (1 issue, 0 PRs, 0 releases).

---

## 3. Shared Feature Directions

The following requirements appear consistently across ≥3 tool communities:

| Requirement | Appears In | Specific Examples |
|---|---|---|
| **Conversation/transcript portability** | Claude Code (#28791), OpenCode (#39033), DeepSeek TUI (#2934) | Bidirectional sync between CLI/desktop; full transcript export including system prompts |
| **MCP authentication reliability** | Copilot CLI (#4203), Codex (#31573, PRs #30295–#30416), Qwen Code (#7768, #7771) | OAuth refresh token handling; persistent config loading; authorization enforcement |
| **Sandbox isolation and security** | Claude Code (#81421), Codex (#30712), Pi (#7049), Qwen Code (#7770) | Fail-closed sandbox defaults; IPv6 egress blocking; preventing sandbox bypass via MCP proxy |
| **Windows stability parity** | Claude Code (#81306, #81484), Codex (#34260, #34133), Copilot CLI (#4217), Pi (#7064), Qwen Code (#7726) | Crash recovery; GPU driver compatibility; MSIX package corruption; WSL path handling |
| **Silent failure elimination** | Claude Code (#76870, #81518), Gemini CLI (#22323), OpenCode (#38990), Pi (#7136, #7150) | False success reporting; tool truncation with no error; dropped RPC messages |
| **Subagent/child session transparency** | Claude Code (#80798), Gemini CLI (#22598), OpenCode (#39010), Codex (#34061) | Trajectory visibility; per-subagent cost tracking; resource management |
| **Cost/usage optimization** | Codex (#35050), Copilot CLI (#4256), OpenCode (#28846), Claude Code (#80199), DeepSeek TUI (#1004) | Prompt caching; explicit batching controls; dry-run mode; usage meter accuracy |
| **Cross-platform customization** | Claude Code (#41015), Gemini CLI (#21983), Qwen Code (#7684), Pi (#7064) | Configurable install paths; Wayland browser support; macOS IME positioning |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | DeepSeek TUI | Pi | Qwen Code |
|---|---|---|---|---|---|---|---|
| **Primary user** | Enterprise devs, Pro subscribers | Large model users, desktop-first | Agentic workflows, subagent orchestration | GitHub-integrated teams, CI/CD users | Cost-sensitive power users, multilingual | Experimental/research, autonomous agents | Chinese-ecosystem devs, DingTalk/WeChat |
| **Unique strength** | Auto-mode classifier, plan mode | Massive community demand (852 👍 Linux), OAuth reliability focus | AST-aware tooling investigation, bash-native sandboxing | Enterprise MCP authentication, `.agents` convention | Best streaming performance fix (PR #4903), localization breadth | 35 issues/day velocity, experimental loadout management | Security patch velocity (2 P1 issues closed/day), DingTalk integration |
| **Key weakness** | Regression-prone (auto-mode #80716), Windows stability | GPU/driver conflicts, log bloat, no Linux desktop | Agent false success (#22323), indefinite hangs (#21409) | TUI hangs on NFS, zombie leaks, Windows exit crash | v0.9.2 instability, O(N²) streaming (now fixed) | CPU pinning (#6665), compacted data loss | E2E CI flakiness, SDK confusion |
| **Release cadence** | Stable (no daily releases) | Stable (no daily releases) | Nightly (daily) | Stable (no daily releases) | Pre-release (v0.9.2 WIP) | Nightly (daily commits) | Nightly (daily) |
| **Technical approach** | TypeScript, LSP integration, MSIX packaging | Rust backend, Chrome DevTools MCP, SQLite | Node.js, GenAI SDK, Chrome MCP 0.19→1.6 | Rust, Tokio async, Tokio + Tokio | Rust, TUI-first architecture | TypeScript, LLM abstractions, Electron desktop | Electron desktop, Web Shell, dingtalk/weixin |

**Notable differentiators**:
- **Gemini CLI** is the only tool actively investigating AST-aware codebase navigation (#22745) as a first-class feature.
- **DeepSeek TUI** stands out for localization breadth (17 languages) and the most aggressive streaming performance optimization (quadratic parse fix).
- **Pi** has the highest raw bug-filing velocity (35 issues/day), suggesting either aggressive testing or early-stage instability.
- **Qwen Code** leads on security patch turnaround—2 P1 issues closed in 24h—and is the only tool with dedicated Chinese ecosystem integrations (DingTalk, WeChat).

---

## 5. Community Momentum & Maturity

| Tool | Maturity Stage | Community Momentum | Risk Profile |
|---|---|---|---|
| **Claude Code** | Mature | Moderate—stable user base, regressions cause frustration | Medium: regression-prone core features (auto-mode, edit tool) |
| **OpenAI Codex** | Mature | Very high—852 👍 indicates massive latent demand, but feature delivery lags | High: no Linux desktop after long demand; Windows GPU crashes unresolved |
| **Gemini CLI** | Growth | High—daily nightlies, 10 PRs/day, active subagent investigation | Medium: false success reporting erodes trust |
| **Copilot CLI** | Mature | Low (this window)—no PRs, but issues show enterprise adoption | Medium: NFS hangs, zombie leaks affect enterprise deployment |
| **Kimi Code** | Stagnant | Very low—1 issue, no PRs, no releases | High: risk of abandonment without development activity |
| **OpenCode** | Growth | High—83 👍 on pricing issue, active TUI and multi-repo work | Medium: v1.18.5 regression cluster |
| **Pi** | Early | Very high—35 issues/day, 10 PRs/day, experimental features | High: silent data loss (RPC drops, compaction invalidation) concerning for autonomous use |
| **Qwen Code** | Growth | High—nightly releases, security-focused, growing Chinese ecosystem | Medium: E2E CI flakiness, SDK confusion |
| **DeepSeek TUI** | Pre-release (v0.9.2) | Very high—10+ PRs/day, strong multilingual community | Medium: pre-release instability expected, but velocity is promising |

**Velocity leaders**: Gemini CLI, DeepSeek TUI, Pi, Qwen Code  
**Stability leaders**: Claude Code (despite regressions), Copilot CLI (despite NFS hang)  
**At risk**: Kimi Code

---

## 6. Trend Signals

Seven industry-relevant signals from community feedback:

1. **Authentication is the new blocker**. MCP OAuth refresh token handling is the #1 cross-cutting pain point (Copilot #4203, Codex #31573, Qwen #7768, #7771). Teams integrating private MCP servers face consistent friction. *Signal*: Expect toolchain standardization around RFC 6749 §6 compliance.

2. **"Silent failure" is the most dangerous bug class**. Across 4 tools, the top frustration is agents reporting success when operations fail (Gemini #22323, Pi #7136, #7150, OpenCode #38990). *Signal*: Community is demanding deterministic error visibility—tools that swallow errors lose trust.

3. **Windows is still an afterthought**. Despite broad adoption, every tool except Qwen Code (which has WeChat/Windows integrations) reports *critical* Windows-specific crashes: MSIX corruption (Claude #81306), GPU driver conflicts (Codex #34133), exit crashes (Copilot #4217), WSL path mishandling (Pi #7064). *Signal*: The Windows gap is a competitive opportunity for whichever tool invests first in full platform parity.

4. **GPU/driver conflicts are enterprise blockers**. Multiple reports of bundled vk_swiftshader.dll being rejected by Windows Code Integrity (Codex #34133, #35352) affect enterprise deployments. *Signal*: Tools bundling GPU dependencies need vendor-certified driver signatures or fallback paths.

5. **Performance regressions hit core workflows**. The most impactful bugs are not obscure edge cases but fundamental operations breaking (Claude auto-mode misclassification #80716, DeepSeek TUI O(N²) streaming #4903, Gemini indefinite hangs #21409). *Signal*: Community tolerance for regression is low—automated regression testing for core workflows is table stakes.

6. **Cost optimization is a first-class requirement**. Explicit batching reducing usage 27–45% (Codex #35050), DeepSeek V4 Pro price cuts triggering quota renegotiation (OpenCode #28846), prompt caching requests (Copilot #4256), dry-run modes (DeepSeek TUI #1004) all point to token cost being a primary UX friction. *Signal*: Tools that surface cost transparency and control will win price-sensitive power users.

7. **Subagent orchestration is the next frontier**. Claude Code (#80798), Gemini CLI (#22598), OpenCode (#39010), DeepSeek TUI (#4022) all have active requests around subagent lifecycle management—promotion/demotion, trajectory visibility, separate cost tracking. *Signal*: The "agent-of-agents" pattern is emerging as a standard UX pattern, requiring standardized visibility and control surfaces.

---

*Report generated from community digest data as of 2026-07-27. All metrics reflect 24-hour windows unless otherwise noted.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-07-27 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The most-discussed Pull Requests on the repository reveal a clear pattern: the community is laser-focused on **tooling reliability** for skill development, followed by domain-specific content skills.

### 1. `fix(skill-creator): run_eval.py always reports 0% recall` (#1298)
**Author:** MartinCajiao | **Status:** Open  
**Functionality:** Fixes the skill-creator evaluation pipeline (`run_eval.py` → `run_loop.py` → `improve_description.py`), which was reporting `recall=0%` for every skill description regardless of content. Root cause: the eval artifact was not installed as a real skill. Also addresses Windows stream reading, trigger detection, and parallel worker issues.  
**Discussion highlights:** References Issue #556 (12 comments, 7 👍) with over 10 independent reproductions. This is the single most impactful blocker for the skill-optimization workflow.  
**Link:** https://github.com/anthropics/skills/pull/1298

### 2. `Add document-typography skill` (#514)
**Author:** PGTBoos | **Status:** Open  
**Functionality:** A quality-control skill that prevents orphan word wrap (1–6 words on new lines), widow paragraphs (stranded section headers), and numbering misalignment in AI-generated documents. Covers a problem "every document Claude generates" faces but few users explicitly request.  
**Discussion highlights:** Addresses a universal pain point in document generation. The skill directly reduces user correction burden.  
**Link:** https://github.com/anthropics/skills/pull/514

### 3. `fix(pdf): correct case-sensitive file references in SKILL.md` (#538)
**Author:** Lubrsy706 | **Status:** Open  
**Functionality:** Fixes 8 case-sensitivity mismatches between `SKILL.md` references and actual filenames (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`). Breaks on case-sensitive filesystems (Linux/macOS).  
**Discussion highlights:** Multiple authors contributed related fixes (#541 for DOCX `w:id` collision, #539 for YAML validation), suggesting systematic quality assurance for existing skills.  
**Link:** https://github.com/anthropics/skills/pull/538

### 4. `Add ODT skill — OpenDocument text creation and template filling` (#486)
**Author:** GitHubNewbie0 | **Status:** Open  
**Functionality:** Full-featured skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods). Triggers on any mention of ODT/ODS/ODF/OpenDocument/LibreOffice. Includes parsing ODT to HTML.  
**Discussion highlights:** Expands the document-format coverage (beyond PDF and DOCX). Community interest in LibreOffice interoperability is evident.  
**Link:** https://github.com/anthropics/skills/pull/486

### 5. `Add skill-quality-analyzer and skill-security-analyzer to marketplace` (#83)
**Author:** eovidiu | **Status:** Open  
**Functionality:** Two meta-skills: a quality analyzer evaluating Structure & Documentation (20%), Skill Logic (25%), Usage Guidance (20%), Test Coverage (20%), and Error Handling (15%); a security analyzer for permission auditing and code review patterns.  
**Discussion highlights:** The oldest high-comment PR still open (since Nov 2025). Represents the community's desire for self-improving skill development tooling.  
**Link:** https://github.com/anthropics/skills/pull/83

### 6. `feat(skills): add self-audit — mechanical verification + reasoning quality gate` (#1367)
**Author:** YuhaoLin2005 | **Status:** Open  
**Functionality:** A universal audit skill that performs mechanical file verification (claim every output exists) followed by a four-dimension reasoning audit in damage-severity priority order. Works with any project or tech stack.  
**Discussion highlights:** Accompanied by Issue #1385 proposing a full "Reasoning Quality Gate Pipeline" with pre-task calibration and adversarial review. Indicates growing demand for output quality assurance.  
**Link:** https://github.com/anthropics/skills/pull/1367

### 7. `Add testing-patterns skill` (#723)
**Author:** 4444J99 | **Status:** Open  
**Functionality:** Comprehensive skill covering the full testing stack: Testing Trophy model, AAA pattern for unit tests, React Testing Library, Playwright for E2E, and testing philosophy (what to test vs. what not to).  
**Discussion highlights:** Strong community interest in test generation and quality enforcement as a Claude skill.  
**Link:** https://github.com/anthropics/skills/pull/723

### 8. `Add color-expert skill` (#1302)
**Author:** meodai | **Status:** Open  
**Functionality:** Self-contained color expertise for any task involving color knowledge: naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912), color space guidance (OKLCH for scales, OKLAB for gradients, CAM16 for perception), and color theory.  
**Discussion highlights:** Active, recent updates (last update 2026-07-21). Niche but demonstrates the breadth of domain skills the community values.  
**Link:** https://github.com/anthropics/skills/pull/1302

---

## 2. Community Demand Trends

The most active Issues reveal five concentrated demand areas:

| Trend | Signal | Key Issue |
|---|---|---|
| **Skill toolchain reliability** | 3+ independent reports of `run_eval.py` returning 0% recall; Windows incompatibility blockers | #556 (12 comments, 7👍), #1169, #1061 |
| **Security & trust boundaries** | Community skills distributed under `anthropic/` namespace create impersonation risk; permission audit requests | #492 (43 comments, 2👍) — highest-comment issue overall |
| **Organizational skill sharing** | Users want direct sharing links or shared skill libraries instead of manual `.skill` file transfers via Slack | #228 (16 comments, 8👍) |
| **Duplicate skill deduplication** | Installing multiple plugins installs identical skills, bloating context windows | #189 (6 comments, 9👍) |
| **Reasoning quality gates** | Proposals for structured verification pipelines: mechanical checks → adversarial review → delivery audit | #1385, #1329 |

**Emerging pattern:** The community is shifting from "build more skills" to **"ensure existing skills work reliably, can be shared safely, and produce auditable quality output."**

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to be merged soon:

- **`fix(skill-creator): run_eval trigger detection misses real skill name` (#1323)** — Polluelo978. Addresses the same 0% recall bug as #1298 but from a different root cause (early bail on non-Skill tools). Critical for the entire skill-optimization workflow.  
  *Link: https://github.com/anthropics/skills/pull/1323*

- **`skill-creator: fix Windows subprocess + encoding bugs` (#1050)** — gstreet-ops. Two 1-line fixes for `PATHEXT` not honored and console encoding. Companion PRs #1099 and #1061 confirm Windows is a major friction point.  
  *Link: https://github.com/anthropics/skills/pull/1050*

- **`Fix skill-creator UTF-8 panic on multi-byte characters` (#362)** — Mr-Neutr0n. Replaces character-based length checks with UTF-8 byte-length validation. Essential for non-English skill descriptions.  
  *Link: https://github.com/anthropics/skills/pull/362*

- **`Detect unquoted YAML special characters in description fields` (#361)** — Mr-Neutr0n. Prevents silent YAML parsing failures when descriptions contain `:`, `#`, `{`, `}`. Directly paired with #362.  
  *Link: https://github.com/anthropics/skills/pull/361*

- **`Add pyxel skill for retro game development` (#525)** — kitao. Integrates the Pyxel MCP server for retro/pixel-art game creation. Niche but well-scoped.  
  *Link: https://github.com/anthropics/skills/pull/525*

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand at the Skills level is not for new domain skills, but for a reliable, cross-platform, auditable skill-creator toolchain**—the `run_eval.py` evaluation pipeline is the single largest pain point (4+ PRs, 3+ Issues, all converging on 0% recall and Windows failures), and resolving it would unblock the entire skill-optimization loop that powers skill quality improvement across the ecosystem.

---

# Claude Code Community Digest — 2026-07-27

## Today's Highlights
The community is buzzing about an auto-mode classifier regression in plan mode (#80716, 7 comments) that forces repeated manual approval on read-only operations, frustrating users who rely on autonomous workflows. A critical Windows crash (#81306) that wedged the MSIX package and destroyed local user data is being actively discussed. No new releases landed in the past 24 hours.

---

## Releases
**None** in the last 24 hours.

---

## Hot Issues

1. **[#80716] Auto-mode classifier incorrectly detects permission mode change in plan mode** — A regression in v2.1.218 where read-only tool calls (cd, file reads, git status/grep) that pass the auto-mode classifier trigger repeated fallback to manual approval. Community notes this breaks the otherwise smooth plan-mode experience. 7 comments, 15 👍.

2. **[#28791] [FEATURE] Sync conversation history between CLI and Claude Code desktop app** — The most-upvoted request in the tracker (107 👍, 27 comments). Users want seamless continuity when switching between terminal and desktop interfaces. No official response yet.

3. **[#44380] Channel messages don't wake idle sessions (--channels plugin)** — Telegram plugin messages appear in the terminal but do not interrupt the REPL prompt. The session passively displays incoming messages but never processes them until the user hits Enter. 11 comments.

4. **[#41015] [FEATURE] Allow configuring or disabling the URL Handler app install location** — Currently hardcoded to `~/Applications/` on macOS with no opt-out. 34 👍 indicate strong demand for flexibility around app registration.

5. **[#72027] Individual Pro subscriber blocked from Claude Code: 'organization disabled' → 'Max or Pro required'** — An entitlement sync bug that permanently locks Pro subscribers out of the CLI. The error state persists even after re-authentication. 6 comments, ongoing frustration.

6. **[#80199] Max X5 Usage Instantly Reaches 100% After Software Update** — Users on Max plans report their usage caps hit immediately post-update, suggesting a meter reset or counting bug triggered by version bumps.

7. **[#64479] Edit tool fails on mixed literal/escape Unicode in multi-line old_string** — A long-standing bug (originally #52813) that remains reproducible. The Edit tool silently fails when a multi-line old_string contains the same Unicode character as both a literal codepoint and a `\uXXXX` escape.

8. **[#71500] VS Code extension: sessions sidebar omits externally-created session transcripts** — Regression in 2.1.187–2.1.191 where files created or modified outside the extension are no longer listed in the Local sessions sidebar. Affects users who manage transcripts via CLI or file sync.

9. **[#76870] LSP tool returns silently incomplete results (cold-index race + stale file state)** — Two distinct bugs: the first LSP query in a session races against workspace indexing, returning truncated results; subsequent queries may serve stale symbol data from a cached state.

10. **[#81306] Windows: Desktop crash wedged the MSIX package; recovery required manual package removal** — A crash during Claude Desktop usage corrupted the MSIX installation to the point where recovery required `rmdir /s` of the entire app directory, destroying all local data (tab assignments, crash dumps). 3 comments.

---

## Key PR Progress
*(Only 7 PRs updated in the last 24h; all are listed)*

1. **#81500 — Fix 404 walkthrough links in the AWS gateway example** — Seven hardcoded URLs in `examples/gateway/aws` point to a non-existent path (`code.claude.com/docs/en/claude-apps-gateway-on-aws`). Small but important fix for new users following the tutorial.

2. **#38167 — Use authenticated request to GitHub API in devcontainer firewall script** — When `GH_TOKEN` is set, the init-firewall script now uses bearer auth for GitHub API calls, preventing rate-limit failures in shared-IP or CI environments.

3. **#81426 — Support Windows venv layout in security-guidance reviewer** — Removes a hard `SKIP_WIN32` early-return in the agentic commit reviewer bootstrap, enabling full security scanning on Windows via correct venv detection.

4. **#81423 — Block IPv6 egress in devcontainer firewall** — The init-firewall script only configured `iptables` (IPv4), leaving all IPv6 traffic unrestricted. Adds `ip6tables` rules to close the bypass.

5. **#68693 — Fix duplicate label setter: add label additively** — The `closeIssueAsDuplicate` bot action was replacing the entire label set with just `[duplicate]`, erasing platform/area/priority labels. Now adds the duplicate label without destroying existing ones.

6. **#81421 — Make bash-sandbox example fail closed** — The example settings file for bash sandboxing omitted `failIfUnavailable`, meaning Claude Code would silently proceed without sandbox enforcement. Adds the flag so the tool fails safely when the sandbox can't initialize.

7. **#20448 — Add web4-governance plugin for AI governance** — A contribution introducing lightweight AI governance via T3 trust tensors, entity witnessing, and R6 audit trails for cryptographic provenance in agentic workflows.

---

## Feature Request Trends

**Conversation portability** (#28791, 107 👍) dominates this week: users want bidirectional sync between CLI sessions and the desktop app, including full transcript history. **Localization** (#69078) has steady support, particularly for Russian and Western European languages. **Multi-agent orchestration** (#80798) is a newer theme: the ability to promote a subagent to a full session (and demote it back) to reclaim context or intervene mid-workflow. **Sandboxing configurability** (#41015, #81421) reflects growing enterprise interest in controlling where and how tools execute. Several issues request better **channel/wake semantics** (#44380) so incoming MCP and plugin messages can interrupt idle sessions rather than pile up silently.

---

## Developer Pain Points

**Silent failures** are the most consistent complaint this week: the Edit tool no-ops after context compaction (#81518), the LSP tool returns truncated results with no warning (#76870), hook launch failures (exit 127) are swallowed with no visible signal (#81458), and the auto-mode classifier misclassifies read-only operations (#80716). **Quota/entitlement bugs** remain painful — Pro subscribers are locked out entirely (#72027), and Max plan usage meters trigger unexpectedly (#80199, #70758). **State corruption during crashes** (#81306, #74386) is a recurring concern, especially around worktree cleanup destroying other sessions' uncommitted work. **Windows-specific regressions** (#81484 — `claude.exe` hangs, #80087 — PATH detection false positives with non-ASCII usernames) suggest the Windows port is still catching up to macOS/Linux in stability.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-27

## Today’s Highlights
No new releases were published in the last 24 hours, but the community remains highly active on long-standing pain points. The single most‑upvoted issue – a Linux desktop app request – now has over 850 reactions, reflecting strong demand for platform parity. Windows stability continues to dominate the bug tracker, with multiple reports of GPU crashes, process‑cleanup storms, and sandbox bypasses, while recent PRs focus on MCP OAuth reliability and TUI history improvements.

## Releases
*None in the last 24 hours.*

## Hot Issues
*10 Issues selected from the top 30 by comment count and community impact.*

1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Comments: 187 · 👍 852*  
   The most‑requested feature on the tracker. Users report macOS power‑consumption issues and want a native Linux app. High engagement indicates strong community demand.

2. **[#34260 – Windows Desktop: unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)**  
   *Comments: 32 · 👍 10*  
   A critical Windows bug where hundreds of `taskkill` processes accumulate, exhausting WMI and freezing the system. Reported just one week ago, it already has 32 comments.

3. **[#17320 – Excessive SQLite WAL writes during streaming due to TRACE logs ignoring RUST_LOG](https://github.com/openai/codex/issues/17320)**  
   *Comments: 27 · 👍 39*  
   Trace logging writes to SQLite even when `RUST_LOG` is set to a lower level, causing high disk I/O during streaming. Affected users report performance degradation on Linux.

4. **[#31573 – OAuth authentication fails at issuer validation](https://github.com/openai/codex/issues/31573)**  
   *Comments: 24 · 👍 55*  
   Free‑tier CLI users cannot authenticate because the OAuth flow rejects the issuer. Blocks all MCP and API access; upvotes indicate broad impact.

5. **[#24948 – Codex session logs grow to 700MB–2GB from repeated compaction history and raw tool output](https://github.com/openai/codex/issues/24948)**  
   *Comments: 23 · 👍 1*  
   Session log bloat slows down the TUI and wastes disk space. While few upvotes, the high comment count reflects a persistent pain for Pro users.

6. **[#34133 – [Windows] Page.captureScreenshot crashes GPU process after Code Integrity Event 3033 rejects bundled vk_swiftshader.dll](https://github.com/openai/codex/issues/34133)**  
   *Comments: 20 · 👍 0*  
   In‑app browser screenshots trigger a GPU crash when Windows Code Integrity blocks the bundled SwiftShader DLL. Symptom of a deeper driver‑compatibility issue.

7. **[#30712 – Codex desktop app on Windows injects split writable roots, causing apply_patch to fail](https://github.com/openai/codex/issues/30712)**  
   *Comments: 14 · 👍 13*  
   Sandbox isolation breaks file patching, forcing agents to fall back to PowerShell file writes – a workaround that bypasses security. Affects Pro users.

8. **[#35050 – GPT-5.6 often serializes independent Code Mode calls; explicit batching reduced weighted usage by 27–45%](https://github.com/openai/codex/issues/35050)**  
   *Comments: 13 · 👍 15*  
   Model behavior analysis: the agent serializes parallel tool calls, wasting tokens. Users who batch requests see significant usage reduction, highlighting a model‑level inefficiency.

9. **[#32530 – VS Code Codex panel intermittently stuck loading on Linux: local webview assets fail with net::ERR_FAILED](https://github.com/openai/codex/issues/32530)**  
   *Comments: 12 · 👍 12*  
   A regression on Ubuntu 26.04 that makes the Codex sidebar unusable. Affects VS Code extension users with Pro subscriptions.

10. **[#34061 – Insane Codex Disk Usage from Subagents](https://github.com/openai/codex/issues/34061)**  
    *Comments: 12 · 👍 1*  
    Subagent sessions create massive disk footprints on macOS. The issue invites a systematic review of sub‑agent resource management.

## Key PR Progress
*10 PRs selected from the 15 updated in the last 24 hours.*

1. **[#35530 – Track model and personality in world state](https://github.com/openai/codex/pull/35530)** *(closed)*  
   Adds model‑switch and personality instructions to the world‑state snapshot, ensuring consistency across replays. A core improvement for agent memory.

2. **[#35525 – Skip inactive TUI threads without pending user interaction](https://github.com/openai/codex/pull/35525)** *(closed)*  
   Only collects buffered requests from threads with pending user input, reducing noise and improving TUI responsiveness in multi‑thread sessions.

3. **[#35524 – Preserve terminal turn errors in replayed history](https://github.com/openai/codex/pull/35524)** *(closed)*  
   Fixes a bug where error‑embedded turn completions were lost during history rebuild, hiding model‑overload warnings from the user.

4. **[#35523 – Shut down the in-process outbound router explicitly](https://github.com/openai/codex/pull/35523)** *(closed)*  
   Prevents the app‑server’s outbound router from staying alive during shutdown by adding an explicit signal, fixing a hang on close.

5. **[#30295 – Serialize MCP OAuth login and logout](https://github.com/openai/codex/pull/30295)** *(closed)*  
   First PR in the MCP OAuth stack. Ensures concurrent login/logout operations do not corrupt state. Part of a larger initiative to fix authentication reliability.

6. **[#30294 – Route MCP OAuth recovery through Codex](https://github.com/openai/codex/pull/30294)** *(closed)*  
   Channels OAuth recovery flows (e.g., token refresh) through the Codex controller, enabling centralised error handling and retry logic.

7. **[#30416 – Serialize authoritative MCP OAuth refresh transactions](https://github.com/openai/codex/pull/30416)** *(closed)*  
   Adds transaction‑level serialisation for refresh operations, preventing race conditions that caused stale or lost tokens.

8. **[#30089 – [rmcp-client] Test MCP OAuth concurrency and recovery](https://github.com/openai/codex/pull/30089)** *(closed)*  
   Comprehensive test suite for the OAuth stack, covering concurrent logins, token refresh races, and error recovery. Superseded by later PRs but foundational.

9. **[#30985 – [app-server] let idle auto-attached threads unload](https://github.com/openai/codex/pull/30985)** *(open)*  
   Introduces a distinction between implicit observer attachments and explicit subscriptions, allowing core‑created threads to be unloaded after 30 minutes of inactivity.

10. **[#30296 – Report MCP OAuth Auto store drift](https://github.com/openai/codex/pull/30296)** *(closed)*  
    Adds monitoring for inconsistencies between the local OAuth store and the server’s expectation, enabling early detection of corruption.

## Feature Request Trends
- **Linux desktop app** – Issue [#11023](https://github.com/openai/codex/issues/11023) dominates with 852 👍 and 187 comments. Users cite macOS power issues and a desire for native Linux support.
- **Context window customisation** – Issue [#34619](https://github.com/openai/codex/issues/34619) requests restoring the 372k context window (or an opt‑in setting) for GPT‑5.6 Sol.
- **Performance and batching control** – Issue [#35050](https://github.com/openai/codex/issues/35050) highlights that explicit batching reduces token usage by 27‑45%, pointing to demand for more user‑controllable parallelism.
- **Cross‑platform parity** – Numerous Windows‑specific bugs (GPU crashes, WMI exhaustion, sandbox issues) and the missing Linux app show that users want equally stable experiences across all desktop OSes.

## Developer Pain Points
- **Windows GPU and driver conflicts** – Multiple reports of crashes caused by Code Integrity rejecting `vk_swiftshader.dll` (e.g., [#34133](https://github.com/openai/codex/issues/34133), [#35352](https://github.com/openai/codex/issues/35352), [#27828](https://github.com/openai/codex/issues/27828)) and general GPU process failures.
- **Excessive disk I/O and log growth** – SQLite WAL writes (##17320), session log bloat (##24948), and subagent disk usage (##34061) indicate debugging infrastructure that hurts performance.
- **Authentication and OAuth fragility** – OAuth issuer validation (##31573) and MCP OAuth race conditions (multiple PRs) continue to frustrate CLI and MCP users.
- **Sandbox bypass on Windows** – Issue [#30712](https://github.com/openai/codex/issues/30712) shows that `apply_patch` fails, forcing agents to write files outside the sandbox – a security concern.
- **macOS kernel panic** – Issue [#16866](https://github.com/openai/codex/issues/16866) (still open after 3 months) reports `os_refcnt` overflows that crash the entire system.
- **VS Code extension instability on Linux** – Issue [#32530](https://github.com/openai/codex/issues/32530) describes a stuck‑loading panel caused by local webview asset failures.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-27

## 1. Today's Highlights
The nightly release **v0.54.0-nightly.20260727** rolls in alongside a major dependency shift, with `@google/genai` jumping from v1.30.0 → v2.12.0 and a 75-package bulk update landing. On the bug front, a critical subagent recovery bug (#22323) continues to draw attention: agents hitting `MAX_TURNS` are falsely reporting success, masking interruptions and eroding trust in agentic workflows. A long-standing generalist agent hang (#21409) also remains active, with community users reporting hour-long stalls on trivial tasks like folder creation.

---

## 2. Releases
**v0.54.0-nightly.20260727.g3818efbbf** — Nightly build with automated version bump.  
[Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.54.0-nightly.20260726.g3818efbbf...v0.54.0-nightly.20260727.g3818efbbf)

---

## 3. Hot Issues (Top 10 by Community Attention)

1. **#22323 — Subagent recovery after MAX_TURNS falsely reports GOAL success**  
   *12 comments, 👍 2*  
   The `codebase_investigator` subagent signals `success` and `Termination Reason: "GOAL"` even after exhausting its turn limit without analysis. This undermines debugging and creates false confidence in agent output.  
   [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#21409 — Generalist agent hangs indefinitely**  
   *8 comments, 👍 8*  
   A top-voted bug: simple commands (e.g., folder creation) cause the generalist agent to stall for up to an hour. Workaround: explicitly disable subagent delegation. Indicates deeper issue with agent orchestration.  
   [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#25166 — Shell command stuck with "Waiting input" after completion**  
   *4 comments, 👍 3*  
   Common frustration: CLI commands finish executing but Gemini persists in showing "Awaiting user input", freezing the workflow. Suggests terminal-buffer state management issues.  
   [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **#19873 — Leverage bash affinity via OS sandboxing**  
   *8 comments, 👍 1*  
   Epic proposal to exploit Gemini 3's native bash chaining (`grep`/`sed`/`awk`) through zero-dependency sandboxing and intent routing. Could unlock significant performance gains but requires careful security design.  
   [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)

5. **#26522 — Auto Memory retries low-signal sessions indefinitely**  
   *5 comments*  
   Background extraction agent re-queues low-signal transcripts, causing infinite loops. Users report sessions stuck in "unprocessed" state with no path to dismissal.  
   [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)

6. **#26525 — Deterministic redaction & reduced Auto Memory logging**  
   *4 comments*  
   Privacy concern: Auto Memory sends transcript content to the extraction model before redacting secrets. The ask is for pre-context redaction and logging reduction to prevent accidental exposure.  
   [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)

7. **#21968 — Gemini doesn't use skills/sub-agents autonomously**  
   *6 comments*  
   Users report custom skills and sub-agents are ignored unless explicitly invoked. Anecdotal evidence: even when a "gradle" skill is defined, Gemini opts for raw shell commands.  
   [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)

8. **#22745 — Assess AST-aware file reads, search, and mapping**  
   *7 comments, 👍 1*  
   Tracking investigation into AST-aware tooling for precise method-bound reads, reducing token waste and turn count. Could complement `codebase_investigator`.  
   [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)

9. **#21983 — Browser subagent fails on Wayland**  
   *4 comments, 👍 1*  
   Linux Wayland users encounter immediate `Termination Reason: GOAL` failure. Platform-specific blocker affecting desktop Linux users.  
   [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)

10. **#22186 — "Get-shit-done" output hook causes crash**  
    *3 comments*  
    Crash on near-completion of GSD output summary. Reported repeatedly; suggests race condition in final rendering phase.  
    [#22186](https://github.com/google-gemini/gemini-cli/issues/22186)

---

## 4. Key PR Progress (Top 10)

1. **#28403 — Block `$VAR` and `${VAR}` variable expansion bypass (GHSA-wpqr-6v78-jr5g)**  
   *Security fix — Open*  
   Patches incomplete detection in `detectBashSubstitution()`/`detectPowerShellSubstitution()`. Also hardens CI workflow. Blocks a confirmed security advisory bypass.  
   [#28403](https://github.com/google-gemini/gemini-cli/pull/28403)

2. **#28543 — Bump `@google/genai` 1.30.0 → 2.12.0**  
   *Dependencies — Merged*  
   Major version bump for the core GenAI SDK. Likely brings new model capabilities, breaking changes, and performance improvements.  
   [#28543](https://github.com/google-gemini/gemini-cli/pull/28543)

3. **#28539 — Bulk dependency update (75 packages)**  
   *Dependencies — Merged*  
   Large batch update covering `simple-git`, `@modelcontextprotocol/sdk`, `typescript`, and 72 others. Critical for staying current with upstream fixes.  
   [#28539](https://github.com/google-gemini/gemini-cli/pull/28539)

4. **#28359 — Fix `stripShellWrapper` for login/interactive shells**  
   *Bug fix — Merged*  
   Prior logic only recognized bare `-c` after `sh`/`bash`/`zsh`. Now correctly strips `bash -lc "..."`, `bash -l -c "..."`, `zsh --login -c "..."`. Allows policy engine to re-check wrapped payloads.  
   [#28359](https://github.com/google-gemini/gemini-cli/pull/28359)

5. **#28523 — Enforce explicit tag length validation in file keychain**  
   *Security — Open*  
   Adds 128-bit (16-byte) tag enforcement for crypto operations in credential storage. Protects against misaligned tag sizes across Node.js runtimes.  
   [#28523](https://github.com/google-gemini/gemini-cli/pull/28523)

6. **#28386 — Track activation disposables in VS Code companion**  
   *Bug fix — Open*  
   Fixes comma-expression bug where `context.subscriptions.push(...)` only tracked the last Disposable. Fixes #27790 — VS Code activation memory leak.  
   [#28386](https://github.com/google-gemini/gemini-cli/pull/28386)

7. **#28438 — Trim tool names before registry lookup**  
   *UX fix — Open*  
   Whitespace-padded tool names now resolve correctly. Includes regression test. Small but prevents silent "tool not found" errors from accidental whitespace.  
   [#28438](https://github.com/google-gemini/gemini-cli/pull/28438)

8. **#28544 — Nightly version bump**  
   *Chore — Open*  
   Automated release update for v0.54.0-nightly.20260727.  
   [#28544](https://github.com/google-gemini/gemini-cli/pull/28544)

9. **#28541 — Bump `execa` 9.6.1 → 10.0.0**  
   *Dependencies — Merged*  
   Breaking major release for process execution library. Requires Node.js version bump.  
   [#28541](https://github.com/google-gemini/gemini-cli/pull/28541)

10. **#28540 — Bump `chrome-devtools-mcp` 0.19.0 → 1.6.0**  
    *Dependencies — Merged*  
    Major version jump for the Chrome DevTools MCP server, likely unlocking improved browser agent capabilities.  
    [#28540](https://github.com/google-gemini/gemini-cli/pull/28540)

---

## 5. Feature Request Trends

- **AST-aware tooling for codebase navigation** (#22745, #22746): Multiple issues propose using Abstract Syntax Trees to narrow file reads to method/class boundaries, reducing token consumption and improving search precision. "tilth" and "glyph" are mentioned as starting points.

- **Subagent trajectory visibility** (#22598, #21763): Users want subagent decision traces to be accessible via `/chat share` and bug reports. Currently subagent context is opaque, hampering debugging and evaluation.

- **Agent self-awareness** (#21432): Request for Gemini CLI to understand its own CLI flags, hotkeys, and subagent structure accurately — essentially acting as its own documentation.

- **Bash-native sandboxing** (#19873): Leverage Gemini 3's native command-line proficiency through zero-dependency OS sandboxing, instead of forcing JSON tool calls. Could improve execution speed and reduce hallucination in file operations.

- **Memory system quality** (#26516, #26522, #26523, #26525): The Auto Memory system is under heavy scrutiny for privacy (pre-redaction logging), reliability (infinite retry loops), and transparency (silently skipping invalid patches). A coordinated quality push is emerging.

---

## 6. Developer Pain Points

- **Agent false success reporting** (#22323): Agents hitting limits reporting `GOAL` success is consistently cited as the most dangerous class of bug — it erodes trust and makes debugging nearly impossible.

- **Indefinite hangs on trivial tasks** (#21409, #25166, #22465): Pattern of agents freezing on simple commands (folder creation, interactive prompts, completed shell commands). Users report waiting 30–60 minutes before killing sessions.

- **Subagent autonomy gap** (#21968, #22093): Agents either ignore defined skills entirely or — worse — activate without permission after updates (#22093). Inconsistent behavior makes configuration unpredictable.

- **Browser agent fragility** (#21983, #22232, #22267): Wayland incompatibility, ignored `settings.json` overrides, and fail-fast lock recovery make the browser agent unreliable, especially on Linux.

- **Secret exposure via Auto Memory** (#26525): The extraction pipeline sends user data to the model *before* redaction, and logs contain secrets from existing skills. Community wants deterministic, pre-context redaction.

- **VS Code scripting failure** (#28386): Registration disposal being silently broken (comma-expression bug) caused memory leaks and extension instability — hard to detect without deep debugging.

- **Corruption on terminal resize** (#21924) and external editor exit (#24935): Users experience screen flicker and visible corruption when resizing terminals or closing external editors, indicating unfinished Ink/RenderStatic migration.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-07-27

## Today’s Highlights
No new releases or pull requests landed in the last 24 hours, but the community surfaced several critical bugs and regressions. A zombie-process leak on Linux, a TUI hang on shared filesystems (NFS/GPFS), and a Windows exit crash are drawing attention. Additionally, a flurry of feature requests around MCP authentication, `.agents` conventions, and caching hints signals growing demand for enterprise-ready customization.

## Releases
No new releases in the last 24 hours. The most recent stable version remains **1.0.75**.

## Hot Issues (10 noteworthy)

1. [**#4163** – Zombie accumulation on Linux](https://github.com/github/copilot-cli/issues/4163)  
   *Area: platform-linux, tools* – `copilot CLI 1.0.71` fails to reap child processes, leaving ~2 zombies per minute. 3 👍 and 4 comments; community identifies this as a long-standing process‑management gap. *Closed – awaiting fix.*

2. [**#4053** – TUI hangs on NFS/GPFS due to SIGCHLD race](https://github.com/github/copilot-cli/issues/4053)  
   *Area: platform-linux, MCP* – The TUI freezes at “Loading: N skills” when home directories reside on NFS/GPFS. The root cause appears to be a race condition when Tokio spawns `which gh` with 30+ concurrent threads. *Triaged; still open.*

3. [**#4263** – Responses disappear in Windows Terminal vertical splits](https://github.com/github/copilot-cli/issues/4263)  
   *Triage* – Content vanishes mid-scroll when using vertical split panes. Only the first screen is visible until a new command is submitted. Reported by `csharpfritz` with 2 comments. *Open.*

4. [**#4258** – `-i` startup prompt ignored with BYOK providers](https://github.com/github/copilot-cli/issues/4258)  
   *Triage* – In interactive TTY mode, the `-i` flag is not auto‑submitted when a custom/BYOK provider is configured. Works with the standard provider in the same tmux session. *Open.*

5. [**#4202** – `view` tool reports “Path does not exist” for existing files (regression)](https://github.com/github/copilot-cli/issues/4202)  
   *Triage* – CLI version 1.0.73 (and 1.0.72) broke the built‑in `view` tool; 1.0.71 works correctly. User `matanSchaumberg` provides a controlled repro. *Open.*

6. [**#4264** – Extension slash commands fire multiple times](https://github.com/github/copilot-cli/issues/4264)  
   *Triage* – Custom local slash commands sometimes queue 3–5 duplicate invocations behind the first command. No comments yet, but the impact on workflow automation is significant. *Open.*

7. [**#4260** – Desktop app ignores `askUser: false` setting](https://github.com/github/copilot-cli/issues/4260)  
   *Triage* – The desktop app host never reads the CLI setting `askUser: false` in `~/.copilot/settings.json`, offering no way to disable the `ask_user` tool. *Open.*

8. [**#4259** – `--resume` replays orphaned permission prompts](https://github.com/github/copilot-cli/issues/4259)  
   *Triage* – On resume, the CLI re‑presents `permission.requested` events that were never resolved, causing an infinite replay loop. *Open.*

9. [**#4203** – Remote MCP (OAuth) ignores refresh token, forces interactive re‑auth](https://github.com/github/copilot-cli/issues/4203)  
   *Area: authentication, MCP* – When an access token expires, the CLI drops the server’s tools instead of attempting an [RFC 6749 §6](https://datatracker.ietf.org/doc/html/rfc6749#section-6) silent refresh. User `ulugbekna` reports a valid refresh token is cached but never used. *Open.*

10. [**#4217** – Windows crash on exit (`FAST_FAIL_FATAL_APP_EXIT`)](https://github.com/github/copilot-cli/issues/4217)  
    *Area: platform-windows* – `copilot.exe` consistently crashes during teardown with a fatal fail‑fast. Work completes normally; the crash occurs only at exit. 1 👍, analysis via WinDbg points to `uv_async_send` on a closing handle. *Open.*

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **Caching & Cost Optimization**: [#4256](https://github.com/github/copilot-cli/issues/4256) requests Anthropic `cache_control` breakpoints to reuse expensive context, reducing cost and latency.
- **`.agents` Convention Expansion**: [#4204](https://github.com/github/copilot-cli/issues/4204) asks to extend the `.agents` discovery mechanism to instructions, agents, and hooks in any opened folder (not just Git repos).
- **MCP Configuration Flexibility**: [#4205](https://github.com/github/copilot-cli/issues/4205) highlights inability to add required runtime headers to MCP server configs when those headers are rejected by the registry’s allowlist.
- **Desktop App Parity**: [#4260](https://github.com/github/copilot-cli/issues/4260) and multiple comments in other threads call for feature parity between the CLI and desktop client, especially around settings and tool disablers.
- **Session Resilience**: The `--resume` replay issue ([#4259](https://github.com/github/copilot-cli/issues/4259)) and orphaned permission events point to a desire for more robust session recovery without infinite loops.

## Developer Pain Points
- **Process Management on Linux**: Zombie leaks ([#4163](https://github.com/github/copilot-cli/issues/4163)) and TUI hangs on shared filesystems ([#4053](https://github.com/github/copilot-cli/issues/4053)) erode trust in long-running sessions, especially in enterprise environments.
- **Platform-Specific Crashes**: Windows users face a consistent exit crash ([#4217](https://github.com/github/copilot-cli/issues/4217)), while Windows Terminal pane handling causes content loss ([#4263](https://github.com/github/copilot-cli/issues/4263)).
- **Regressions in Core Tools**: The `view` tool regression ([#4202](https://github.com/github/copilot-cli/issues/4202)) and the ignored `-i` prompt with BYOK providers ([#4258](https://github.com/github/copilot-cli/issues/4258)) disrupt established workflows.
- **MCP Authentication Holes**: The OAuth refresh token failure ([#4203](https://github.com/github/copilot-cli/issues/4203)) and registry header rejection ([#4205](https://github.com/github/copilot-cli/issues/4205)) frustrate teams integrating private MCP servers.
- **Extension Reliability**: Duplicate slash command invocations ([#4264](https://github.com/github/copilot-cli/issues/4264)) and lack of `askUser` control in the desktop app ([#4260](https://github.com/github/copilot-cli/issues/4260)) reduce the predictability of custom automation.

*All links point to the official `github/copilot-cli` repository.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest — 2026-07-27**

**1. Today's Highlights**  
Community activity was minimal over the past 24 hours. The only update is a closed bug report (#2559) describing intermittent image paste failures in the Web interface, where pasted images are replaced with a placeholder text. No new releases or pull requests were recorded, indicating a quiet development cycle.

**2. Releases**  
*None in the last 24 hours.*

**3. Hot Issues**  
*Only one issue was updated in the reporting period.*

- **#2559 — [Bug] Web: pasted images intermittently dropped; model only receives placeholder**  
  *Author: nothankyouzzz | Updated: 2026-07-26 | Comments: 1 | 👍: 0*  
  **Why it matters:** This bug affects the core image‑handling workflow in Kimi Code Web. Users paste images expecting them to be sent to the model, but the model receives only `[image omitted for provider compatibility; re-read the file to view it or get conversion guidance]`. The intermittent nature makes it hard to reproduce, and the placeholder message suggests a provider‑side compatibility issue that may require deeper debugging. The community has not yet weighed in (0 upvotes, 1 comment), but the issue is relevant to any developer relying on multi‑modal chat.  
  [GitHub Link](https://github.com/MoonshotAI/kimi-cli/issues/2559)

**4. Key PR Progress**  
*No pull requests were updated in the last 24 hours.*

**5. Feature Request Trends**  
With only a single bug report in the window, no clear feature request direction can be inferred. The absence of feature proposals may indicate that users are currently focused on stability rather than new functionality.

**6. Developer Pain Points**  
The immediate pain point is image paste reliability in the Web client. The placeholder text hints at a possible incompatibility with certain provider APIs or image formats, which could frustrate developers who frequently share screenshots or diagrams. The intermittent nature adds uncertainty, making it difficult to trust the image‑paste feature for consistent workflows.

---

*Digest generated from [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) data as of 2026-07-27.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode Community Digest — 2026-07-27

A quiet day for releases, but the community is actively surfacing critical bugs around the v1.18.5 desktop update and raising important feature requests for multi‑repo workspaces and TUI enhancements. The most discussed item remains the DeepSeek V4 Pro price cut and its implications for Go subscription limits. Several PRs are landing to fix mobile SSE reconnection, CORS handling, and model cost tracking.

---

### Releases
No new releases in the last 24 hours.

---

### Hot Issues (Top 10)

1. **#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction**  
   *Author: icocoon | Comments: 95 | 👍: 83*  
   A heavily upvoted feature request to align OpenCode Go subscription quotas with the dramatic price drop of DeepSeek V4 Pro. Community expects either increased usage limits or reduced pricing.  
   [View Issue](https://github.com/anomalyco/opencode/issues/28846)

2. **#38789 — Desktop v1.18.5: UnsupportedContentType error on project reload after update**  
   *Author: Start-Gao | Comments: 13 | 👍: 5*  
   A reproducible bug where upgrading to v1.18.5 breaks project loading with `UnsupportedContentType` errors. Root cause traced to generated client SDK.  
   [View Issue](https://github.com/anomalyco/opencode/issues/38789)

3. **#36506 — All paid OpenCode Zen models fail with 'Upstream request failed' — free models work**  
   *Author: vicmuchina | Comments: 10 | 👍: 2*  
   Paid Zen models (MiniMax-M3, deepseek-v4-flash) are unusable while free models and Go models work normally. Ongoing server‑side issue.  
   [View Issue](https://github.com/anomalyco/opencode/issues/36506)

4. **#38801 — message="exiting loop" in TUI**  
   *Author: josephtingiris | Comments: 10 | 👍: 0*  
   A long‑running frustration where the TUI exits unexpectedly with `message="exiting loop"`. Only workaround found is setting `step=80`.  
   [View Issue](https://github.com/anomalyco/opencode/issues/38801)

5. **#34184 — Auto-renewed Go subscription quota not reset (showing 1-day wait time)**  
   *Author: suzhenghui-sky | Comments: 7 | 👍: 0*  
   After successful auto‑renewal, usage quota does not refresh, leaving users artificially locked out. Payment flow appears broken.  
   [View Issue](https://github.com/anomalyco/opencode/issues/34184)

6. **#37762 — Problems with responses (Ollama + Gmail setup)**  
   *Author: jcrosby10 | Comments: 7 | 👍: 0*  
   Users running local models (Ollama) on Windows report inconsistent response quality, especially when integrating with email tools.  
   [View Issue](https://github.com/anomalyco/opencode/issues/37762)

7. **#15789 — Portable wrapper scripts for running OpenCode without global installation**  
   *Author: jek-bao-choo | Comments: 5 | 👍: 6*  
   A popular feature request for official portable scripts (e.g., via npx or download‑and‑run) to avoid global npm installs.  
   [View Issue](https://github.com/anomalyco/opencode/issues/15789)

8. **#38990 — DeepSeek Integration Ignoring User Prompts and Overriding Intent**  
   *Author: pixelcreatives | Comments: 5 | 👍: 0*  
   DeepSeek model frequently ignores user requests entirely, generating unrelated code or content. Closed as “not planned” but community is vocal.  
   [View Issue](https://github.com/anomalyco/opencode/issues/38990)

9. **#34398 — Workspace folders with per‑repo snapshot tracking — /undo fails silently in multi‑repo sessions**  
   *Author: Duo-Huang | Comments: 5 | 👍: 0*  
   `/undo` does nothing when working with multiple Git repos in one session. The feature request proposes proper per‑repo snapshot tracking.  
   [View Issue](https://github.com/anomalyco/opencode/issues/34398)

10. **#39035 — Desktop toast "UnsupportedContentType" — /api/mcp returns text/html instead of JSON**  
    *Author: westwindstories2026 | Comments: 1 | 👍: 0*  
    A newly filed critical regression in v1.18.5 where MCP API endpoints return HTML, causing the bootstrap loader to fail.  
    [View Issue](https://github.com/anomalyco/opencode/issues/39035)

---

### Key PR Progress (Top 10)

1. **#39015 — feat: add model‑gated auto‑approve mode**  
   Introduces an optional classifier that only auto‑approves tool calls from trusted models, with fallback to normal permission dialogs. Closes #37564.  
   [View PR](https://github.com/anomalyco/opencode/pull/39015)

2. **#39010 — feat(session): add subagents tab with status and cost tracking**  
   Adds a dedicated “Subagents” panel showing child sessions, status icons, and cost for each sub‑agent. Addresses #37267.  
   [View PR](https://github.com/anomalyco/opencode/pull/39010)

3. **#39008 — fix(llm): enable Anthropic prompt caching on the OpenRouter route**  
   Ensures `cache_control` is sent for Anthropic models routed through OpenRouter, reducing per‑turn costs. Fixes #39009.  
   [View PR](https://github.com/anomalyco/opencode/pull/39008)

4. **#39027 — fix(ui): keep mutable selects open**  
   Prevents duplicate Kobalte selection events from closing Shell/Theme dropdowns prematurely. Fixes #39026.  
   [View PR](https://github.com/anomalyco/opencode/pull/39027)

5. **#39028 — fix(web): reconnect SSE stream when mobile tab becomes visible**  
   Re‑establishes the SSE connection when returning from another app on mobile browsers, solving frozen chat. Fixes #39030.  
   [View PR](https://github.com/anomalyco/opencode/pull/39028)

6. **#39016 — fix(app): add scroll to project selector dropdown**  
   Adds `overflow-y: auto` to the project dropdown so users with many projects can scroll. Fixes #37149.  
   [View PR](https://github.com/anomalyco/opencode/pull/39016)

7. **#39021 — fix(server): treat undefined origin as non‑CORS, reject empty origin string**  
   Tightens CORS validation: empty `Origin` header is now rejected, while absent header remains allowed. Security fix.  
   [View PR](https://github.com/anomalyco/opencode/pull/39021)

8. **#39020 — fix(core): propagate download failures as Effect errors in skill discovery**  
   Replaces silent `return` with `Effect.fail` when skill file downloads fail, preventing stale cached skills from being used unknowingly.  
   [View PR](https://github.com/anomalyco/opencode/pull/39020)

9. **#39019 — fix(core): resolve npm edge by package name instead of first entry**  
   Fixes a bug where peer dependencies were returned as the primary package, causing incorrect install paths.  
   [View PR](https://github.com/anomalyco/opencode/pull/39019)

10. **#38999 — fix(core): align grep behavior and guidance**  
    Improves the `grep` tool: requires approval for paths outside the active directory, surfaces readable error messages, and clarifies documentation.  
    [View PR](https://github.com/anomalyco/opencode/pull/38999)

---

### Feature Request Trends

- **Multi‑root / multi‑repo workspaces** — Multiple issues (#38984, #34398) ask for first‑class support of sessions spanning several repositories, with per‑repo snapshot tracking and unified undo.
- **TUI and desktop UX improvements** — Requests for portable scripts (#15789), sub‑agent status views (#37267), MCP server management from TUI (#38993), and better scroll behavior in dialogs (#37149).
- **Localisation & accessibility** — Users want non‑English interface strings, keybinding hints, and error messages (#38280).
- **Export enhancements** — Including the system prompt in conversation exports (#39033).
- **Cost & quota optimisation** — Adjusting limits after DeepSeek price cuts (#28846) and enabling prompt caching for third‑party router paths (#39009).

---

### Developer Pain Points

- **Persistent “exiting loop” in TUI** (#38801) – A long‑standing issue that forces users to work around instead of using the TUI reliably.
- **Desktop v1.18.5 regressions** – Multiple reports of `UnsupportedContentType` errors on project load (#38789) and MCP endpoints returning HTML (#39035).
- **Paid model unreliability** – Zen paid models fail with “Upstream request failed” (#36506), and auto‑renewal doesn’t reset quotas (#34184).
- **Model behavior problems** – DeepSeek ignores user prompts (#38990) and GLM‑5.2 fails to write large files (#38978).
- **Mobile and remote session issues** – SSE streams disconnect when switching apps on mobile (#39030), mouse scroll wheel misbehaves over SSH (#39029).
- **Windows‑specific bugs** – TUI can’t paste via `Ctrl+V` (#38455), and Shell/Theme selects stop opening after a change (#39026).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-07-27

**Data source:** github.com/earendil-works/pi

## Today's Highlights

No new releases arrived in the last 24 hours, but the community remains highly engaged, filing and triaging 35 issues and merging 10 pull requests. The most critical discussions center on a CPU‑pinning TUI bug (uncached `Intl.Segmenter`), a security fix for `brace-expansion` (CVE-2026-14257), and several reports of silent data loss during compaction and RPC interactions. On the positive side, experimental loadout management and cross‑platform path normalisation PRs show steady progress toward a more robust agent.

## Releases

No new versions were published in the last 24 hours.

## Hot Issues

_Picked for impact, community attention, or broader relevance._

1. **[#4877] Session folder collision**  
   _Closed_ | 21 comments, 2 👍  
   Paths like `/a/b/c/d` and `/a-b/c-d` map to the same session folder. While harmless, it could surprise users.  
   https://github.com/earendil-works/pi/issues/4877

2. **[#6665] TUI pins a full core while streaming**  
   _Open, in progress_ | 8 comments  
   `Intl.Segmenter` (ICU BreakIterator) is called uncached per chunk, combined with a per‑chunk Markdown rebuild. Causes 100% CPU on one core during long sessions.  
   https://github.com/earendil-works/pi/issues/6665

3. **[#7090] Regenerate shrinkwrap with brace-expansion 5.0.8+**  
   _Closed_ | 5 comments  
   `minimatch@10.2.5` pulled `brace-expansion@5.0.7`, which is vulnerable to a memory‑exhaustion DoS (CVE-2026-14257). Pinning to 5.0.8 resolves it.  
   https://github.com/earendil-works/pi/issues/7090

4. **[#7064] WSL absolute windows paths are mishandled**  
   _Open_ | 5 comments, 1 👍  
   `read`/`write`/`edit` tools fail on WSL2 when given absolute Windows paths, forcing fallback to raw command‑line workarounds.  
   https://github.com/earendil-works/pi/issues/7064

5. **[#7049] Upgrade Undici to 8.8.0 for plain‑HTTP proxy forwarding**  
   _Open_ | 3 comments  
   `proxyTunnel: true` default in Undici 8.5.0 causes CONNECT on plain HTTP targets, breaking MCP/API calls through `HTTP_PROXY`.  
   https://github.com/earendil-works/pi/issues/7049

6. **[#7138] MiniMax-M3: messy thinking output, compaction breaks reasoning**  
   _Closed_ | 3 comments  
   The `pi-ultra-compact` extension mangles reasoning content; a `reasoning_split` parameter is proposed to fix it.  
   https://github.com/earendil-works/pi/issues/7138

7. **[#7154] Compaction invalidates extension runtime**  
   _Closed_ | 1 comment  
   After `ctx.newSession()` / `fork()` / `compaction`, captured `pi` throws “stale after session replacement” with no recovery path. Three independent long‑running sessions hit this.  
   https://github.com/earendil-works/pi/issues/7154

8. **[#7150] RPC prompt during in‑flight compaction silently dropped**  
   _Closed_ | 1 comment  
   A `prompt` command submitted over RPC while compaction is in flight returns `success: true` but the message is never ingested – silent data loss.  
   https://github.com/earendil-works/pi/issues/7150

9. **[#7149] Standalone linux-x64 binary SIGILL on pre‑Haswell CPUs**  
   _Closed_ | 1 comment  
   The official binary uses BMI2 instructions (`shlx`), causing illegal instruction crashes on Sandy Bridge / Ivy Bridge. npm‑installed package works.  
   https://github.com/earendil-works/pi/issues/7149

10. **[#7136] bash tool silently truncates long commands**  
    _Closed_ | 1 comment  
    Commands over a certain length are cut off mid‑stream with no error, leading to partial execution – dangerous for autonomous agents.  
    https://github.com/earendil-works/pi/issues/7136

## Key PR Progress

_All 10 merged or opened in the last 24 hours are highlighted._

1. **[#7156] fix(ai): rename OpenCode Zen Go to OpenCode Go**  
   Corrects a provider display name.  
   https://github.com/earendil-works/pi/pull/7156

2. **[#7151] feat(ai): expose pending stop reason while streaming**  
   Allows consumers to detect “final answer” phase early by predicting `stopReason: 'stop'`.  
   https://github.com/earendil-works/pi/pull/7151

3. **[#7148] feat(coding-agent): Experimental loadout management**  
   `/loadout` command to enable/disable extensions mid‑session, persisted across resume. Needs user confirmation.  
   https://github.com/earendil-works/pi/pull/7148

4. **[#7145] Dev**  
   Generic development PR (likely a merge).  
   https://github.com/earendil-works/pi/pull/7145

5. **[#7131] Set AI_AGENT for child process attribution**  
   Sets `AI_AGENT=pi` in CLI and RPC entry points – an emerging cross‑agent convention used by Claude Code, GitHub CLI, and Vercel.  
   https://github.com/earendil-works/pi/pull/7131

6. **[#7129] tui: raise visibleWidth cache to 4096 entries, use LRU eviction**  
   The 512‑entry FIFO cache thrashes on real agent sessions (CJK, emoji, box‑drawing). LRU with 4096 entries keeps hot segments.  
   https://github.com/earendil-works/pi/pull/7129

7. **[#7124] fix(coding-agent): normalize path separators in footer for cross‑platform display**  
   Uses forward slash always for the cwd footer, fixing Windows display (`~\project` → `~/project`).  
   https://github.com/earendil-works/pi/pull/7124

8. **[#7112] fix(coding-agent): normalize path separators in formatCwdForFooter**  
   Similar fix (earlier iteration).  
   https://github.com/earendil-works/pi/pull/7112

9. **[#7122] fix(tools): correct byte count in write, false limit warning in find, surrogate pairs in truncateLine**  
   Three independent tool fixes: UTF‑8 byte count for `write`, overly strict limit warning in `find`, and surrogate‑pair handling in `truncateLine`.  
   https://github.com/earendil-works/pi/pull/7122

10. **[#7120] feat(coding-agent): show SYSTEM.md and APPEND_SYSTEM.md in startup [Context] banner**  
    Gives users visibility into whether these prompt‑modifying files are active.  
    https://github.com/earendil-works/pi/pull/7120

## Feature Request Trends

From all opened issues (most are closed/untriaged), the community is pushing for:

- **Structured output and deterministic JSON** – #1086 (JSON schema support), #7152 (auth preflight command), #7146 (token usage in workflow events).
- **Extension hooks and lifecycle** – #7137 (pre_response gate), #7127 (durable compaction strategy lifecycle), #7144 (mouse‑click API for overlays).
- **Better model integration** – #7135 (OpenAI Pro modes), #7133 (Anthropic refusals as distinct signal), #7143 (Z.AI `max_completion_tokens` fix).
- **User experience polish** – #7141 (themeable block cursor), #7126 (session rename UX), #7130 (Kitty backspace issue), #7139 (flag‑swallowing prompt bug).

The common thread is **extensibility**: developers want to hook into the agent pipeline, manage extensions dynamically, and get consistent, inspectable data from the platform.

## Developer Pain Points

Recurring frustrations seen across multiple issues:

- **Platform fragmentation** – Path handling on Windows/WSL (#7064, #7124, #7112) and CPU compatibility (#7149) continue to trip up users.
- **Silent failures and data loss** – The most alarming: `bash` tool truncation (#7136), RPC drop during compaction (#7150), and extension runtime invalidation (#7154). These undermine trust in autonomous operation.
- **Performance regressions** – Uncacheg `Intl.Segmenter` pinning a core (#6665) and a thrashing cache (#7129) show that streaming efficiency is a hot topic.
-

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-27

## Today's Highlights
A security-focused day: three high‑priority (P1) issues around MCP tool authorization and desktop IPC bridges were closed, alongside a security hardening report on Electron `webPreferences`. On the positive side, the nightly release brings local‑time insight measurement, and a series of PRs improve terminal history, sidebar width, and Web Shell git workflows. Several E2E CI failures on main indicate ongoing stability challenges.

## Releases
**v0.21.0-nightly.20260727.c003e1718**  
- `fix(cli): measure insight days and hours in local time everywhere` by @ComplexSimply  
- `refactor(autofix): ext` (incomplete note)  
[Nightly release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260727.c003e1718)

## Hot Issues (top 10 by discussion activity)
1. **[#7585] Proposal: Add a direct external context provider profile**  
   Community wants an extension to let one CLI process share repository context via an external memory service without touching Qwen Core. 8 comments, marked `need-discussion`.  
   [Issue #7585](https://github.com/QwenLM/qwen-code/issues/7585)

2. **[#7769] MCP tool denial bypassed when a new SSE session is created**  
   P1 security: denying an MCP tool call in Desktop doesn’t stick if the AI opens a new SSE session. Closed with high urgency.  
   [Issue #7769](https://github.com/QwenLM/qwen-code/issues/7769)

3. **[#7768] Desktop IPC bridge executes MCP tools without enforcing user authorization**  
   P1 security: `mcp_client_tool_call` IPC method bypasses permission checks. Closed.  
   [Issue #7768](https://github.com/QwenLM/qwen-code/issues/7768)

4. **[#7264] Cold-start follow-ups: remaining lazy-loading candidates**  
   Performance enhancement (P2). esbuild audit found 17.24 MiB parsed before first `initialize`. Closed after PR merges.  
   [Issue #7264](https://github.com/QwenLM/qwen-code/issues/7264)

5. **[#7750] SDK selection: qwen-code-sdk vs qoder-agent-sdk**  
   User confusion around overlapping SDKs. Community seeks clarity on which product is canonical. 6 comments.  
   [Issue #7750](https://github.com/QwenLM/qwen-code/issues/7750)

6. **[#7684] Command mode statusline multi‑line IME positioning**  
   On macOS, when statusline spans multiple lines, input method candidate box is far from cursor. Welcome PR. 5 comments.  
   [Issue #7684](https://github.com/QwenLM/qwen-code/issues/7684)

7. **[#7687] feat(dingtalk): support outbound image delivery**  
   Feature request to let agent send local images via DingTalk (closed after PR #7698 merged).  
   [Issue #7687](https://github.com/QwenLM/qwen-code/issues/7687)

8. **[#7772] Qwen Desktop BrowserWindow uses insecure Electron webPreferences**  
   Security hardening: `sandbox: false` and other weak settings in main window. 4 comments, no fix yet.  
   [Issue #7772](https://github.com/QwenLM/qwen-code/issues/7772)

9. **[#7771] Persisted mcp_config not loaded into main-process MCP proxy at startup**  
   After restart, IPC calls fail because config is not reloaded. Bug, open.  
   [Issue #7771](https://github.com/QwenLM/qwen-code/issues/7771)

10. **[#7770] Code interpreter sandbox can write to host when MCP proxy is internet‑exposed**  
    Sandbox has outbound internet; if user exposes MCP proxy via SSH, an attacker can write files. Security bug, open.  
    [Issue #7770](https://github.com/QwenLM/qwen-code/issues/7770)

## Key PR Progress (top 10)
1. **[#7698] feat(dingtalk): support outbound image delivery**  
   DingTalk channel now validates and uploads local images, replacing `[IMAGE: …]` markers with Markdown. Merged.  
   [PR #7698](https://github.com/QwenLM/qwen-code/pull/7698)

2. **[#5396] fix(ui): reduce UI flicker — throttle + startTransition + batch**  
   Five targeted changes to eliminate flicker across streaming and UI updates. Open, awaiting review.  
   [PR #5396](https://github.com/QwenLM/qwen-code/pull/5396)

3. **[#7749] feat(review): script-lint — run linters over a diff’s executable scripts**  
   New required step in review workflow: automatically lints shell scripts in diffs. Merged.  
   [PR #7749](https://github.com/QwenLM/qwen-code/pull/7749)

4. **[#7776] fix(core): scope the timeout veto to the fragment it appears in**  
   `getContextLengthExceededInfo` now avoids classifying errors from non‑timeout fragments as timeout. Merged.  
   [PR #7776](https://github.com/QwenLM/qwen-code/pull/7776)

5. **[#7774] fix(core): read the stash reflog from the common git dir**  
   Corrects `countStashEntries` for linked worktrees. Open.  
   [PR #7774](https://github.com/QwenLM/qwen-code/pull/7774)

6. **[#7724] fix(web-shell): allow shell commands in new tasks without a session**  
   Typing `!` in a fresh web shell task now lazily creates a session. Open.  
   [PR #7724](https://github.com/QwenLM/qwen-code/pull/7724)

7. **[#5738] fix(cli): default to virtualized terminal history**  
   Turns on in‑app scrollable history by default for all new CLI sessions. Open.  
   [PR #5738](https://github.com/QwenLM/qwen-code/pull/5738)

8. **[#7778] feat(web-shell): allow widening sidebar up to half the window width**  
   Dynamic max width based on window size. Open.  
   [PR #7778](https://github.com/QwenLM/qwen-code/pull/7778)

9. **[#7751] feat(review): script-lint as a deterministic gate**  
   Moves script lint from agent‑driven to deterministic compose‑review. Strengthens CI pipeline. Open.  
   [PR #7751](https://github.com/QwenLM/qwen-code/pull/7751)

10. **[#7726] fix(weixin): create the account credential file already private**  
    Avoids race condition where credential file is briefly world‑readable. Merged.  
    [PR #7726](https://github.com/QwenLM/qwen-code/pull/7726)

## Feature Request Trends
- **MCP & Security Integration** – Multiple requests for MCP permission enforcement, external context providers, and sandbox isolation improvements.
- **Web Shell Enhancement** – Voice controls, git branch picker, PR creation flow, and wider sidebar are active development themes.
- **Automated CI/Tooling** – Script‑lint, repo‑hygiene bots, and deterministic review gates seek to reduce manual toil.
- **Subagent Model Selection** – Allow users to pick model grades for spawned subagents at runtime.
- **Cross‑Platform Parity** – DingTalk image delivery, WeChat credential safety, and macOS IME fixes reflect community diversity.

## Developer Pain Points
- **CI Instability** – Multiple E2E test failures on main (issues #7755, #7773, #7777, #7780) suggest flaky tests or race conditions.
- **Terminal & UI Bugs** – IME candidate misplacement, Kitty keyboard flags left active after teardown, and skill autocomplete breaking after updates (issues #7684, #7779, #7717).
- **Tooling Edge Cases** – Gitignore pattern parsing fails with trailing slashes, leading whitespace, and backslash escapes. Sed simulation diverges from actual `sed`. (PRs #7764, #7765, #7763, #7775).
- **Sandbox/Docker Confusion** – Runtime selection picks “docker” even when daemon is unavailable, hiding a working “podman” (issue #7732).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-27

## Today’s Highlights
The project continues its rapid v0.9.2 development cycle with a surge of performance and UX fixes. A critical O(N²) streaming bug that re-parsed the entire growing message on each chunk was finally addressed (PR #4903), and the team landed a substantial efficiency win by caching live transcript snapshots (PR #4892). On the feature side, `@git` and `@diff` mentions now let models reference git context without a separate round‑trip (PR #4899), and background shell completion delivery was wired up (PR #4894). The community also saw the first merges of localization updates for Chinese and new provider support for OpenCode Zen.

## Releases
No new releases in the last 24 hours. The latest tagged version remains v0.9.2 (pre‑release work in progress). Recent activity centres on hardening the runtime, fixing performance regressions, and expanding the skill‑pack ecosystem.

## Hot Issues
(10 noteworthy issues, selected from the top 30 by comment count or community impact.)

1. **[#3793 – Guided localized constitution creator](https://github.com/Hmbown/CodeWhale/issues/3793)** (17 comments)  
   The most‑discussed issue this week. Proposes replacing the blank prompt editor with a step‑by‑step “constitution creator” that respects language, autonomy, and runtime security separation. Community feedback has been positive, with several users offering translation and UI suggestions.

2. **[#4227 – Help JayBeest map the CodeWhale tsunami](https://github.com/Hmbown/CodeWhale/issues/4227)** (13 comments)  
   A meta‑issue from a contributor asking for a streamlined dev‑environment setup workflow. The project’s high velocity (10+ PRs/day) makes onboarding newcomers difficult; this issue has sparked discussion about automated tooling for `cargo build`, feature flags, and branching strategies.

3. **[#2934 – Sidebar sessions panel with auto‑resume](https://github.com/Hmbown/CodeWhale/issues/2934)** (10 comments)  
   Persistent request for a dedicated sidebar to browse and resume past sessions (currently only `Ctrl+R` picker). Users want a visual overview of all conversations. The community agrees friction is high for long‑running users.

4. **[#3792 – Make first‑run feel like starting CodeWhale, not editing config](https://github.com/Hmbown/CodeWhale/issues/3792)** (9 comments)  
   Complements #3793. Emphasises that the onboarding flow should feel like launching a productive session, not filling out a config file. Several commenters shared anecdotes of new users being intimidated.

5. **[#2494 – macOS + iTerm2 user issues](https://github.com/Hmbown/CodeWhale/issues/2494)** (6 comments, **closed**)  
   A Chinese‑language bug report listing macOS‑specific problems: wrong keyboard shortcuts in docs, pasting newlines causing multiple sends, inability to stop a running prompt, and session history navigation. While closed, it still reflects lingering Mac pain points.

6. **[#1004 – `/dryrun` – preview next chat completion without sending](https://github.com/Hmbown/CodeWhale/issues/1004)** (5 comments)  
   Highly requested by DeepSeek V4 Pro users to avoid burning expensive tokens on debugging. The lack of a dry‑run mode is a concrete cost issue. Community has suggested JSON preview and estimated token count.

7. **[#4022 – CLI/TUI parity for subagent and runtime controls](https://github.com/Hmbown/CodeWhale/issues/4022)** (5 comments)  
   Technical design issue: the TUI now has rich subagent management, but those controls are not accessible via CLI or API. The team is discussing how to expose them without duplicating UI logic.

8. **[#3983 – Make Work state model‑visible on parent turns](https://github.com/Hmbown/CodeWhale/issues/3983)** (4 comments)  
   While the TUI shows “To‑do” and “Strategy context”, the model itself cannot see its own work state during a turn. This limits autonomous agents from inspecting progress. Community supports making the state part of the prompt context.

9. **[#3091 – Website parity with Japanese and Vietnamese README locales](https://github.com/Hmbown/CodeWhale/issues/3091)** (4 comments)  
   The project has excellent README translations but only English/Chinese on the website. Volunteers have stepped up to contribute web translations, but technical integration for language‑routed pages is still pending.

10. **[#3928 – No in‑app way to read the constitution; custom override fails silently](https://github.com/Hmbown/CodeWhale/issues/3928)** (3 comments)  
    A frustrating UX bug: the constitution is the core base prompt, but users cannot view it inside the app. Custom overrides via env var are silently ignored. The issue is prioritised as “v0.9.2” and has multiple upvotes.

## Key PR Progress
(10 important pull requests merged or ready for review in the last 24h.)

1. **[#4905 – Stop writing terminal control bytes to non‑terminals](https://github.com/Hmbown/CodeWhale/pull/4905)** (merged)  
   Fixed the OSC 9;4 and OSC 0 escape sequences being written unconditionally, which caused garbled output when piping or redirecting stdout. Partial fix toward #4847.

2. **[#4904 – Fix composer menu limit and git mentions](https://github.com/Hmbown/CodeWhale/pull/4904)** (open)  
   Follow‑up to #4899 fixing a regression where `mention_menu_limit = 0` disabled the popup incorrectly. Ensures git mentions are resolved once per keystroke.

3. **[#4903 – Stop re‑parsing committed markdown while streaming](https://github.com/Hmbown/CodeWhale/pull/4903)** (merged, refs #3897)  
   The quadratic parse bug: now only parses newly streamed chunks, reusing previously rendered parts. Dramatic improvement for long responses.

4. **[#4902 – Pin cacheable prefix across unchanged turns](https://github.com/Hmbown/CodeWhale/pull/4902)** (merged, closes #3738)  
   Investigated the prompt‑cache hit‑rate regression. Found that per‑turn `<turn_meta>` blocks were the culprit; the PR stabilises the prefix to maximise DeepSeek cache savings.

5. **[#4863 – Persist exact repo‑scoped allow grants](https://github.com/Hmbown/CodeWhale/pull/4863)** (merged)  
   Harvested from @greyfreedom’s work. Approval cards now let users remember safe shell/file‑write commands as persistent `allow` rules scoped to the workspace.

6. **[#4894 – Deliver tracked completions to waiting turns](https://github.com/Hmbown/CodeWhale/pull/4894)** (merged, refs #3874)  
   Core plumbing for background shell completion. Completed jobs now appear as internal events at the next turn boundary, enabling the model to continue without polling.

7. **[#4900 – Make policy narrowing observable](https://github.com/Hmbown/CodeWhale/pull/4900)** (merged, closes #3947)  
   When runtime policy narrows a turn’s authority (e.g., blocking a tool), the decision is now recorded and exposed to the model and user, improving debugging and trust.

8. **[#4899 – Add `@git` and `@diff` mentions](https://github.com/Hmbown/CodeWhale/pull/4899)** (merged, closes #4067)  
   Allows users to tag git status and diffs directly in the composer, saving the model a round‑trip to `git_diff`. Supports `@git` (summary) and `@diff` (unstaged/staged changes).

9. **[#4897 – Fix context‑menu hover rows](https://github.com/Hmbown/CodeWhale/pull/4897)** (merged)  
   Corrected hit‑testing in borderless context menus so the hover state matches the item under the cursor. Added regression tests.

10. **[#4805 – Update Chinese translations](https://github.com/Hmbown/CodeWhale/pull/4805)** (merged)  
    Synchronised 17 message keys in `zh-Hans.json` to catch up with `en.json`. Community contribution from @SparkofSpike.

## Feature Request Trends
The most‑requested feature directions this week, distilled from all open issues:

- **Localisation expansion** – Many issues target adding or improving translations: Korean, Spanish, Brazilian Portuguese, Russian, French, German, Catalan, Indonesian. The community clearly wants the TUI to speak their language.
- **Onboarding & setup simplification** – A cluster of issues (#3793, #3792, #3927, #3937, #3409) advocate making first‑run feel like a guided product experience rather than a configuration exercise. The “constitution creator” and “make it yours” personalisation are popular design proposals.
- **Agent & workflow runtime** – Issues #2974, #3983, #3832, #4411, #4397 all push for transparent agent state, bounded auto‑mode loops, cross‑provider routing, and a multi‑session dashboard. The project is moving toward deeper autonomous support.
- **TUI performance & UX** – #2934 (sidebar sessions), #3897 (streaming performance), #3904 (snapshot caching) show growing attention to smooth, low‑latency interaction. Community tests on large repos and long conversations are driving these requests.
- **CLI/API parity** – #4022, #1004, #1888 stress that all TUI features must be accessible via command line or remote API for headless automation.
- **Security & runtime control** – Issues like #3793 (constitution must not override runtime security), #3928 (read constitution in‑app), and #4411 (consent for auto routing) reflect developer demand for clear, auditable security boundaries.

## Developer Pain Points
Common frustrations expressed across the top issues:

- **O(N²) streaming performance** – Long messages become progressively slower as they grow. Now fixed by PR #4903, but the pain was acute for users generating multi‑thousand‑line responses.
- **No dry‑run mode** – DeepSeek V4 Pro users cannot see what will be sent before it is sent, leading to wasted tokens and unexpected costs (#1004).
- **Silent failures for custom configuration** – Custom constitution overrides, environment flags, and skill markers can fail without any user‑visible error (#3928, #3927, #4698).
- **macOS/iTerm2 keyboard mismatch** – Documentation still shows Windows shortcuts, and `Ctrl+C` behaviour is non‑standard on macOS (#2494).
- **Hidden features** – Powerful personalisation (12 themes, custom backgrounds, Hotbar) is never discovered because the onboarding doesn’t showcase them (#3937).
- **Unclear update process** – Users report that rebuilding from `main` can leave stale state, and there is no clear migration path for skill version markers (#4698, #4876).
- **In‑app documentation gap** – The constitution, the skill system, and provider routing details are only available as external documentation, not inside the TUI (#3928, #1888, #2026).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*