# AI CLI Tools Community Digest 2026-06-15

> Generated: 2026-06-15 02:59 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report — 2026-06-15

## 1. Ecosystem Overview

The AI CLI tool landscape is experiencing rapid maturation alongside growing pains in reliability, cost management, and cross-platform parity. Seven major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and CodeWhale—are all grappling with sub-agent lifecycle bugs, session state corruption, and silent data loss, indicating systemic under-investment in agent runtime robustness. A clear divide is emerging between tools focused on enterprise-grade stability (Claude Code, Gemini CLI) and those prioritizing feature velocity and extensibility (OpenCode, Pi, CodeWhale). Token consumption transparency has become a universal concern, with users across all platforms demanding better cost visibility and fair billing. Platform-specific breakages—particularly on Windows and Linux—remain a persistent frustration, suggesting that cross-platform investment is lagging behind feature development.

## 2. Activity Comparison

| Tool | Hot Issues Listed | Key PRs Listed | Release Today |
|------|------------------|----------------|---------------|
| Claude Code | 10 (2 CRITICAL) | 5 | None |
| OpenAI Codex | 10 | 10 | None |
| Gemini CLI | 10 (3 P1 bugs) | 10 | None |
| GitHub Copilot CLI | 8 (1 spam) | 0 | None |
| Kimi Code | 3 | 4 | None |
| OpenCode | 10 | 10 | **v1.17.7** |
| Pi | 10 | 10 | None |
| Qwen Code | 10 | 10 | None |
| CodeWhale | 10 | 10 | **v0.8.60** (rebrand) |

**Key observations:**
- **OpenCode** and **CodeWhale** shipped releases today—both showing high iteration velocity.
- **Gemini CLI** and **Qwen Code** have the most significant CI/CD churn (53+ dependency updates, nightly release failures).
- **Copilot CLI** is notably quiet: zero PR activity and only 8 issues updated.
- **Claude Code** has the highest-severity open bugs (data loss, kernel panics, runaway costs).
- **OpenAI Codex** has the most community engagement by comment/upvote volume (#14593: 607 comments, 268👍).

## 3. Shared Feature Directions

Several requirements appear consistently across tool communities:

| Theme | Tools Affected | Specific Need |
|-------|---------------|---------------|
| **Non-interrupting message queuing** | Claude Code (#50246, 92👍), Qwen Code (related), Pi (#5700) | Users want to queue prompts without derailing active agent work |
| **Token/cost transparency** | OpenAI Codex (#14593, 268👍), Qwen Code (#4564, #5118), Kimi Code (#2123), Claude Code (#32544) | Per-task breakdowns, usage dashboards, rate-limit visibility |
| **Linux desktop app** | OpenAI Codex (#11023, 568👍) | Most-requested feature for any tool; performance/power benefits |
| **Clipboard/copy-paste fixes** | OpenCode (#13984, 20👍), Pi (#5736—Escape interrupt), CodeWhale (#1812—freeze) | TUI basic usability on Linux and macOS |
| **MCP/plugin infrastructure** | OpenCode (#28567, 21👍), Claude Code (tools), Pi (#5678), CodeWhale (#3225) | Full MCP spec support, streaming, resources, prompts |
| **Agent permission guardrails** | Qwen Code (#5102), Gemini CLI (#22672), CodeWhale (#1186), Kimi Code (#2451) | Configurable safety boundaries, sudo handling, side-effect contracts |
| **Cross-platform parity** | All 9 tools | Windows clipboard, WSL integration, Wayland support, glibc compatibility |

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|------|---------------|-------------|-------------------|
| **Claude Code** | Reliability & cost control | Enterprise power users | Subagent architecture; heavy tool ecosystem; Anthropic model lock-in |
| **OpenAI Codex** | Model depth & safety | Professional developers | Proprietary models; safety-heavy heuristics; deep IDE integration |
| **Gemini CLI** | Agent orchestration | Google ecosystem users | Multi-agent delegation; Auto Memory; evaluation-first quality |
| **Copilot CLI** | GitHub workflow integration | GitHub-native developers | Tightly coupled to GH issues/PRs; skills/agent system; BYOK flexibility |
| **Kimi Code** | Lightweight CLI | Chinese market developers | MoonshotAI model; smaller community; Windows parity improving |
| **OpenCode** | Extensibility & plugins | Tinkerers and plugin developers | Plugin-first architecture; rapid release cadence; multi-provider support |
| **Pi** | Extensions & maintainability | Developer tool builders | Extension API as first-class citizen; behavior-preserving refactoring |
| **Qwen Code** | Compliance & CI/CD | Alibaba Cloud ecosystem | Permission contracts; workflow orchestration; token plan billing |
| **CodeWhale** | Multi-agent orchestration | Power CLI users | Rebranding to CodeWhale; WhaleFlow orchestration; voice input; provider fallback |

**Key differentiators:**
- **Maturity level**: Claude Code and OpenAI Codex are grappling with systemic reliability issues at scale; OpenCode and CodeWhale are prioritizing feature velocity.
- **Platform investment**: Pi leads on cross-platform polish (terminal theme detection, Windows paste fixes); Claude Code and OpenAI Codex have platform-specific blockers that are actively harming users.
- **Ecosystem lock-in**: Claude Code and OpenAI Codex require their own models; Gemini CLI requires Google infra; Qwen Code requires Alibaba Cloud. Copilot CLI and OpenCode are the most provider-agnostic.
- **Agent orchestration**: Gemini CLI and CodeWhale are investing in multi-agent coordination (swarm synthesis, fleet ledger); Claude Code suffers from runaway recursion in the same pattern.

## 5. Community Momentum & Maturity

| Tool | Community Size (Proxy) | Iteration Velocity | Stability Signal |
|------|----------------------|--------------------|-----------------|
| **OpenCode** | High (v1.17.7 today) | Very high | Regression in v1.17.7 (EditBuffer destroyed) |
| **CodeWhale** | Medium (v0.8.60 today) | High | Rebranding friction; "turn stalled" bug unresolved |
| **Claude Code** | Very high | Moderate | 2 CRITICAL bugs (subagent recursion, kernel panic) |
| **OpenAI Codex** | Very high (#14593 has 607 comments) | Moderate | Token consumption anger high; Linux app demand unaddressed |
| **Gemini CLI** | Medium | Moderate (53 dep updates) | 3 P1 bugs; auto memory inefficiency |
| **Pi** | Medium | High (10 PRs) | Regression fixes dominate; good maintenance culture |
| **Qwen Code** | Medium | Moderate | CI pipeline fragile; security concerns rising |
| **Kimi Code** | Low | Low (4 PRs) | Rate limit complaints; small community |
| **Copilot CLI** | Low | Very low (0 PRs) | Session poisoning; agent skill path bugs |

**Maturity assessment:**
- **Most active communities**: OpenAI Codex (by engagement) and OpenCode (by release velocity)
- **Most stable/well-maintained**: Pi and OpenCode show disciplined PR workflows; Pi's behavior-preserving refactoring signals mature engineering
- **Most at risk**: Copilot CLI (zero PR activity) and Kimi Code (small community, unresolved rate-limit anger)
- **Rapidly iterating**: CodeWhale (rebrand + major new features) and OpenCode (daily releases)
- **Concerning stability**: Claude Code (kernel panics, data loss outpace features) and OpenAI Codex (token consumption crisis eroding trust)

## 6. Trend Signals

1. **Sub-agent lifecycle is the #1 systemic risk** — Unbounded recursion (Claude Code #68430, #68110), orphaned agents (OpenAI Codex #25179), and misleading termination status (Gemini CLI #22323) indicate that agent spawning and cleanup are not adequately governed. This is a fundamental safety and cost control gap.

2. **Token/cost transparency is now table stakes** — Communities across all model-locked tools are demanding real-time cost visibility, per-task breakdowns, and rate-limit reset mechanisms. OpenAI Codex (#14593) and Kimi Code (#2123) show that cryptic billing erodes trust faster than feature gaps.

3. **Windows and Linux parity is overdue** — Platform-specific TUI freezes (CodeWhale #1812, OpenCode clipboard #13984), missing binaries (OpenAI Codex #28103, Claude Code #51143), and glibc version locks (CodeWhale #1067) are blocking significant user segments. The gap between macOS-first development and cross-platform production use remains wide.

4. **Guardrails over safety theater** — Users are rejecting binary safety heuristics (OpenAI Codex #27817: false cybersecurity flags) and instead requesting permission contracts with tool/path scope (Qwen Code #5102, CodeWhale #1186). "Allow always" toggles and typed persistent rules are preferred over opaque blocks.

5. **Extensibility is a competitive moat** — OpenCode and Pi are winning developer mindshare through plugin hooks, MCP support, and extension APIs that allow customization without waiting for core team. Claude Code and OpenAI Codex are comparatively closed, risking disintermediation.

6. **Rebranding causes real user friction** — CodeWhale’s rebrand from deepseek-tui has generated asset confusion (#3208), command update failures (#2917), and npm issues. Users are loyal to tools, not names; rename costs must be mitigated with clear migration documentation.

7. **Enterprise compliance concerns are rising** — Trojan false positives (Qwen Code #5055), OAuth port leaks (OpenCode #32245), and environment variable exposure (OpenCode #31778) indicate that security posture is not keeping pace with feature development—a red flag for enterprise adoption.

8. **Evaluation infrastructure is maturing** — Gemini CLI’s component-level evaluations EPIC (#24353), Qwen Code’s CI pipeline modularization (#4866), and OpenCode’s non-invasive UX testing framework (#23030) signal industry recognition that benchmarks are insufficient. Systematic behavioral evaluation is becoming a development priority.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-06-15)

## 1. Top Skills Ranking

The following Pull Requests have generated the most discussion and attention in the community. All remain **open** at time of analysis.

**#514 – Add document-typography skill**  
*[GitHub](https://github.com/anthropics/skills/pull/514)*  
A quality-control skill that fixes orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Discussion focused on its broad applicability—every Claude-generated document suffers these issues—and the need for minimal false positives. Created Mar 4, 2026; last updated Mar 13.

**#486 – Add ODT skill (OpenDocument text creation, template filling, parse to HTML)**  
*[GitHub](https://github.com/anthropics/skills/pull/486)*  
Enables creation, filling, reading, and conversion of `.odt`/`.ods` files. Community interest centered on LibreOffice compatibility and ISO standard compliance. Created Mar 1, 2026; last updated Apr 14.

**#210 – Improve frontend-design skill clarity and actionability**  
*[GitHub](https://github.com/anthropics/skills/pull/210)*  
A revision of the existing frontend-design skill to make instructions specific enough to steer Claude behavior within a single conversation. Discussion highlighted the tension between brevity and precision in skill definitions. Created Jan 5, 2026; last updated Mar 7.

**#83 – Add skill-quality-analyzer and skill-security-analyzer to marketplace**  
*[GitHub](https://github.com/anthropics/skills/pull/83)*  
Two meta-skills: one evaluates skills across five quality dimensions (structure, documentation, examples, etc.), the other checks for security issues. Community debated whether meta-skills belong in the official repo or should remain as example-skills. Created Nov 6, 2025; last updated Jan 7, 2026.

**#538 – Fix case-sensitive file references in PDF skill**  
*[GitHub](https://github.com/anthropics/skills/pull/538)*  
Fixes eight mismatches between `SKILL.md` and actual filenames (`REFERENCE.md` vs `reference.md`). A small but critical fix that generated attention due to impacts on case-sensitive file systems. Created Mar 6, 2026; last updated Apr 29.

**#181 – Add SAP-RPT-1-OSS predictor skill**  
*[GitHub](https://github.com/anthropics/skills/pull/181)*  
Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data. Discussion focused on model licensing (Apache 2.0) and integration complexity. Created Dec 28, 2025; last updated Mar 16, 2026.

**#1140 – Implement agent-creator skill and fix multi-tool evaluation**  
*[GitHub](https://github.com/anthropics/skills/pull/1140)*  
Adds a meta-skill for building task-specific agent sets, alongside critical stability fixes for evaluation scripts and Windows support. The PR addresses a popular feature request (Issue #1120). Created May 15, 2026; last updated Jun 2.

## 2. Community Demand Trends

Analysis of the top 15 Issues by comment volume reveals five clear demand clusters:

| Demand Theme | Representative Issues | Signal |
|--------------|----------------------|--------|
| **Org-wide skill sharing & management** | #228 (14 comments), #189 (6 comments) | Strongest signal: users want shared skill libraries, direct sharing links, and elimination of duplicate skills when installing plugins. |
| **Skill evaluation/optimization tooling fixes** | #556 (12 comments), #1169 (3 comments), #1061 (3 comments) | `run_eval.py` is broken for many setups (0% recall, Windows incompatibility), blocking the skill-creation feedback loop. |
| **Security & trust boundaries** | #492 (7 comments) | Community skills distributed under the `anthropic/` namespace create trust abuse vulnerabilities. |
| **Cross-platform compatibility** | #1061 (3 comments), #29 (4 comments) | Consistent demand for AWS Bedrock support and Windows-native tooling. |
| **Governance & safety patterns for agents** | #412 (6 comments) | Proposal for an agent-governance skill covering policy enforcement, threat detection, and audit trails. |

The most anticipated new Skill directions are **organization-wide skill distribution**, **reliable evaluation infrastructure**, and **security/governance meta-skills**.

## 3. High-Potential Pending Skills

These open PRs have active discussion and appear close to merge based on update frequency and community engagement:

- **#1298 – Fix `run_eval.py` 0% recall (recall=0% on all queries)**  
  *[GitHub](https://github.com/anthropics/skills/pull/1298)*  
  Addresses the most-blocking bug in the skill-creator pipeline. The fix installs the eval artifact as a real skill and fixes Windows stream reading, trigger detection, and parallel workers. Last updated Jun 11, 2026.

- **#723 – Add testing-patterns skill**  
  *[GitHub](https://github.com/anthropics/skills/pull/723)*  
  Covers the full testing stack (unit, React component, integration, E2E) with the Testing Trophy model. Strong community interest in standardizing test patterns. Last updated Apr 21, 2026.

- **#444 – Add AURELION skill suite (kernel, advisor, agent, memory)**  
  *[GitHub](https://github.com/anthropics/skills/pull/444)*  
  A structured cognitive + memory framework with four skills. Discussion on integration depth and namespace conflicts. Last updated May 6, 2026.

- **#1050 & #1099 – Windows compatibility fixes for skill-creator scripts**  
  *[GitHub #1050](https://github.com/anthropics/skills/pull/1050) · [GitHub #1099](https://github.com/anthropics/skills/pull/1099)*  
  Two complementary PRs fixing subprocess `PATHEXT`, encoding, and pipe reading issues on Windows. These are blockers for a significant portion of the community.

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, well-tested meta-skills and infrastructure that enable skill creation, evaluation, and sharing at scale—the "tools to build tools" layer—rather than new domain-specific skills alone.**

---

# Claude Code Community Digest — 2026-06-15

## Today's Highlights
Two critical subagent recursion bugs (#68430, #68110) and a memory-leak kernel panic on macOS (#66020) dominate the conversation, echoing deeper reliability concerns around Cowork file truncation (#53940) and billing errors (#32544). The community continues to push for a non-interrupting message queue mode (#50246, 92👍), while the team merges a fix to prevent premature closure of assigned issues (#68423).

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 Notable)
1. **[#53940 – Cowork Edit/Write silently truncates files](https://github.com/anthropics/claude-code/issues/53940)** (31 comments, 12👍) — Byte-conservation buffer cap causes silent data loss; has repro, affects all file sizes, Windows users hit hardest.
2. **[#50246 – Message queue mode](https://github.com/anthropics/claude-code/issues/50246)** (28 comments, 92👍) — Highly requested feature to queue prompts instead of interrupting active tasks; no official response yet.
3. **[#41458 – cleanupPeriodDays: 99999 ignored](https://github.com/anthropics/claude-code/issues/41458)** (16 comments, 1👍) — Explicit setting ignored, 490 sessions silently deleted; regression and data-loss flagged.
4. **[#32544 – Extra usage charged despite available plan capacity](https://github.com/anthropics/claude-code/issues/32544)** (15 comments, 14👍) — False rate-limit errors lead to overbilling; users report Linux but likely cross-platform.
5. **[#51143 – Blank/white screen on Windows Desktop](https://github.com/anthropics/claude-code/issues/51143)** (13 comments, 12👍) — Cowork unusable; multiple reinstalls ineffective, ongoing.
6. **[#63870 – Bash tool calls emitted as raw `<invoke>` text](https://github.com/anthropics/claude-code/issues/63870)** (11 comments, 13👍) — Model hallucinates XML output instead of executing commands; detailed JSONL evidence provided.
7. **[#66192 – Copy-paste not working](https://github.com/anthropics/claude-code/issues/66192)** (11 comments, 10👍) — macOS TUI regression; basic workflow broken.
8. **[#68430 – Subagent infinite recursion & token burn](https://github.com/anthropics/claude-code/issues/68430)** (7 comments, CRITICAL) — Subagents spawn 50+ child agents, ignore `CLAUDE_CODE_FORK_SUBAGENT=0`, fetch individual files via HTTP; catastrophic costs.
9. **[#66020 – macOS kernel zone leak (data.kalloc.1024)](https://github.com/anthropics/claude-code/issues/66020)** (7 comments, 0👍) — claude.exe panics at ~20GB; leak rate scales 21→1027/sec with agent load; serious stability risk.
10. **[#68110 – Subagent recursive exponential fan-out](https://github.com/anthropics/claude-code/issues/68110)** (4 comments, 2👍) — General-purpose sub-agents have access to Agent tool and spawn unbounded children; related to #68430, same root cause.

## Key PR Progress (5 Open/Merged)
1. **[#68423 – fix(scripts): don't auto-close assigned issues in sweep](https://github.com/anthropics/claude-code/pull/68423)** — Prevents stale-label automation from closing issues with active assignments; improves triage hygiene.
2. **[#67699 – [baobao] Bounty fix: Claude autonomously ran background scripts calling a paid external](https://github.com/anthropics/claude-code/pull/67699)** ($29 bounty) — Automated fix via NVIDIA AI for issue #67654; addresses unauthorized API calls.
3. **[#67409 – [baobao] Bounty fix: Account downgraded due to billing error](https://github.com/anthropics/claude-code/pull/67409)** ($200 bounty) — Automated fix for billing accuracy regression; high-value bounty reflects user frustration.
4. **[#67722 – [CLOSED] Claude autonomously ran background scripts calling a paid external](https://github.com/anthropics/claude-code/pull/67722)** — Earlier attempt; superseded by #67699.
5. **[#1 – Create SECURITY.md](https://github.com/anthropics/claude-code/pull/1)** — Long-closed initial repository setup.

## Feature Request Trends
The most vocal demand is **non-interrupting message queuing** (#50246, #64204), enabling users to chain follow-ups without derailing active work. Other rising themes:
- **`cwd` parameter for the Task tool** (#12748, 23👍) to support Git worktrees and multi-repo workflows.
- **Appshot-style window capture** (#68498) mimicking OpenAI Codex’s full-window text extraction via macOS accessibility APIs.
- **Project-scoped conversation listing** (#68495) to separate sessions across different directories.

## Developer Pain Points
- **Silent data loss & truncation** — Cowork file edits (#53940) and session cleanup (#41458) cause irreversible data corruption.
- **Runaway costs** — Subagent recursion (#68430, #68110) and unbounded token burn are the #1 financial risk; billing inaccuracies (#32544) compound distrust.
- **Resource exhaustion** — pty leaks on Desktop (#65995, #66434) and macOS kernel zone leaks (#66020) force system restarts.
- **Model reliability regressions** — Bash tool calls printed as raw XML (#63870), malformed `call`/`court` tokens (#68354), and silent empty turns on Opus 4.8 (#68510) break core functionality.
- **Platform-specific blockers** — Windows blank screen (#51143) and packaging regression (#68504) make Claude Code unusable on that platform; WSL users hit mislabeled overload errors (#68502).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-15

A busy day for the Codex community: token consumption concerns dominate discussion, false‑positive cybersecurity flags continue to frustrate users, and the long‑standing request for a Linux desktop app remains the most‑upvoted issue. On the engineering side, several stacked PRs are laying groundwork for async hooks, rate‑limit reset credits, and improved MCP timeout handling.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#14593 – [OPEN] [bug, rate‑limits] Burning tokens very fast**  
   [openai/codex/issues/14593](https://github.com/openai/codex/issues/14593)  
   *607 comments, 268 👍*  
   The longest‑running active issue. Users on Business and Pro plans report unexpectedly high token consumption even during trivial tasks. No official resolution yet, and the community is growing impatient.

2. **#11023 – [OPEN] [enhancement, app] Codex desktop app for Linux**  
   [openai/codex/issues/11023](https://github.com/openai/codex/issues/11023)  
   *107 comments, 568 👍*  
   The most‑requested feature. Power users cite both power‑saving and performance benefits on Linux. After months of inactivity, the community is eager for a public roadmap.

3. **#27979 – [OPEN] [bug, windows‑os, app] Windows Codex App 26.609.4994.0 no longer opens after update**  
   [openai/codex/issues/27979](https://github.com/openai/codex/issues/27979)  
   *21 comments, 6 👍*  
   A recent update bricks the Windows desktop app for some users. No workaround documented yet.

4. **#25500 – [OPEN] [bug, app, session] Codex Desktop Projects sidebar shows "No chats" for projects with older non‑archived conversations**  
   [openai/codex/issues/25500](https://github.com/openai/codex/issues/25500)  
   *18 comments, 2 👍*  
   A data‑visibility bug that makes thousands of conversations appear lost, causing confusion and repeated re‑creation.

5. **#27817 & #28015 – [OPEN] [bug, safety‑check] False positive cybersecurity flags**  
   [openai/codex/issues/27817](https://github.com/openai/codex/issues/27817)  
   [openai/codex/issues/28015](https://github.com/openai/codex/issues/28015)  
   *16 comments each, 0 and 0 👍*  
   Users performing legitimate finance/tax work or local repo maintenance are repeatedly interrupted by “cybersecurity risk” warnings. The safety mechanism is generating enough false positives to erode trust.

6. **#28180 – [CLOSED] [bug, model‑behavior, app, performance] Remotion causes Codex syspolicyd and trustd CPU usage to hit 100%**  
   [openai/codex/issues/28180](https://github.com/openai/codex/issues/28180)  
   *5 comments*  
   A macOS‑specific bug where generating animations with Remotion drives system processes to 100% CPU. Closed without public explanation, which may frustrate affected users.

7. **#28103 – [OPEN] [bug, windows‑os, app] WSL binary missing in MSIX build**  
   [openai/codex/issues/28103](https://github.com/openai/codex/issues/28103)  
   *5 comments, 9 👍*  
   The Microsoft Store build of Codex Desktop is missing the Linux `codex` binary, breaking the “Run agent in WSL” feature. A regression that directly impacts Windows developers relying on WSL.

8. **#27353 – [OPEN] [bug, app, session] Project chat history disappeared after latest Codex app update**  
   [openai/codex/issues/27353](https://github.com/openai/codex/issues/27353)  
   *7 comments, 3 👍*  
   A data‑loss issue following the June 9 update. Users report that entire project histories vanish from the sidebar, though the files may still exist on disk.

9. **#28244 – [OPEN] [bug, app, performance] macOS: Codex spawns ~100 zombie child processes per 5 seconds at startup**  
   [openai/codex/issues/28244](https://github.com/openai/codex/issues/28244)  
   *1 comment*  
   A newly filed high‑impact bug on Apple Silicon. The app immediately exhausts the per‑user process limit (`kern.maxprocperuid=2666`), making the system unresponsive.

10. **#25431 – [OPEN] [enhancement, windows‑os, app] Expose spell‑check toggle in Windows desktop settings**  
    [openai/codex/issues/25431](https://github.com/openai/codex/issues/25431)  
    *5 comments, 14 👍*  
    A small but popular quality‑of‑life request. Users want a simple on/off switch for the built‑in spellchecker, which currently cannot be disabled.

---

## Key PR Progress

1. **#28235 – [code‑reviewed] Add request user input auto‑resolution timer**  
   [openai/codex/pull/28235](https://github.com/openai/codex/pull/28235)  
   Introduces a 60‑second grace + 60‑second visible countdown for CLI prompts that require user input. If the user doesn’t respond, an empty answer is submitted automatically. Improves non‑interactive scripting.

2. **#28154 – [OPEN] feat(tui): add rate‑limit reset redemption to /usage**  
   [openai/codex/pull/28154](https://github.com/openai/codex/pull/28154)  
   The `/usage` TUI command can now display and redeem personal rate‑limit reset credits – a direct response to the token‑burning complaints seen in #14593.

3. **#28143 – [OPEN] feat(app‑server): expose rate‑limit reset credits**  
   [openai/codex/pull/28143](https://github.com/openai/codex/pull/28143)  
   Backend API foundation for the TUI redemption flow. Extends the `account/rateLimits/read` endpoint with a nullable `rateLimitResetCredits` field.

4. **#28234 – [OPEN] [mcp] Increase default tool timeout to 300 seconds**  
   [openai/codex/pull/28234](https://github.com/openai/codex/pull/28234)  
   Raises the MCP tool‑call timeout from 120s to 300s, addressing complaints about premature timeouts during long‑running operations.

5. **#27794 – [OPEN] Remove terminal resize reflow flag gates**  
   [openai/codex/pull/27794](https://github.com/openai/codex/pull/27794)  
   Marks `terminal_resize_reflow` as always‑on and removes the disabled code paths. Stabilizes a feature that was already rolled out.

6. **#27640 – [OPEN] Support multi‑tool install requests**  
   [openai/codex/pull/27640](https://github.com/openai/codex/pull/27640)  
   Enables the model to request installation of multiple plugins in a single turn, simplifying multi‑tool workflows.

7. **#28232 – [OPEN] [oai] Add workspace headline statusline item**  
   [openai/codex/pull/28232](https://github.com/openai/codex/pull/28232)  
   Enterprise‑facing: adds a persistent workspace message (e.g., company announcements) to the TUI status line, refreshing every 10s.

8. **#27452 – [OPEN] [codex] Run async hooks and deliver output on accepted requests**  
   [openai/codex/pull/27452](https://github.com/openai/codex/pull/27452)  
   Activates asynchronous hook execution. Output from background hooks can be delivered to later model requests, unlocking more responsive agent pipelines.

9. **#27771 – [OPEN] [codex] Add a bounded runtime for async hooks**  
   [openai/codex/pull/27771](https://github.com/openai/codex/pull/27771)  
   Provides session‑scoped ownership with resource limits and deterministic delivery gates for async hooks. Prerequisite for #27452.

10. **#27666 – [OPEN] [codex] Add managed field support to requirements.toml**  
    [openai/codex/pull/27666](https://github.com/openai/codex/pull/27666)  
    Extends the `requirements.toml` configuration layer to enforce managed authentication, storage, telemetry, shell, feedback, and Windows settings – improving enterprise deployability.

---

## Feature Request Trends

- **Linux desktop app** (still the #1 ask with 568 👍).  
- **Task/thread renaming** (closed #12564, but the desire for better history navigation persists).  
- **Spellcheck toggle** in Windows desktop (#25431).  
- **Persistent terminal title markers** in CLI (#21958) to distinguish multiple AI terminals.  
- **Rate‑limit transparency and reset credits** – the PRs this week indicate OpenAI is listening, but users want real‑time visibility.  
- **Multi‑agent and workspace management** (e.g., workspace headline, project hierarchy).  
- **MCP timeout configurability** (the PR increasing default timeout addresses this).

---

## Developer Pain Points

1. **Token consumption & rate limiting** – #14593 exemplifies a broad frustration: users feel they are paying for excessive token burn on simple tasks.  
2. **False‑positive safety flags** – Legitimate work is blocked by cybersecurity heuristics (#27817, #28015, #28230), eroding trust in the safety system.  
3. **App crashes and data loss** – Windows app post‑update failures (#27979, #27367, #25807), macOS zombie process flood (#28244), and disappearing project histories (#27353, #25500) cause significant productivity loss.  
4. **Performance regressions** – High GPU/CPU usage (#20840, #28180) and slow model responses (#21527) remain common complaints.  
5. **Missing WSL integration** – The MSIX build missing the Linux binary (#28103) breaks a key workflow for Windows developers.  
6. **Shell environment gaps** – Codex CLI does not inherit zsh aliases (#16551), forcing users to re‑create configuration.  
7. **Stale subagent management** – Long sessions leave orphaned subagents in the UI (#25179) that cannot be closed.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-15

## Today's Highlights

No new releases landed today, but the project saw significant maintenance activity with a large batch of dependency updates (53 npm packages, plus major bumps for Puppeteer and the GenAI SDK) closing simultaneously. Agent reliability remains the dominant theme in open issues, with three long-standing P1 bugs—generalist agent hangs, subagent recovery misreporting, and shell command stalling—still actively discussed. The evaluation infrastructure workstream continues to advance, with the component-level evaluations EPIC gathering steam.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** [P1, kind/bug]
   Users report `gemini-cli` hangs indefinitely when deferring to the generalist agent, even for trivial tasks like folder creation. The workaround (disabling sub-agent delegation) implies a fundamental routing or initialization failure. **8 👍** — high community impact.

2. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** [P1, kind/bug]
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when hitting the maximum turn limit before doing any analysis. This masks the failure and undermines trust in agent reporting. **2 👍**

3. **[#22745 — Assess impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** [P2, kind/feature]
   An EPIC investigating whether AST-aware tools (e.g., tilth, glyph) can improve agent quality by reducing misaligned reads and token noise. This could fundamentally change how the agent understands code structure. **1 👍**

4. **[#25166 — Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** [P1, kind/bug]
   Simple CLI commands that don't require user input still show "Awaiting user input" after completion, causing the agent to hang. A core I/O handling issue that breaks workflows. **3 👍**

5. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** [P1, area/agent]
   EPIC tracking the next phase of behavioral evaluations after the initial 76 tests. Critical for ensuring quality as the agent ecosystem grows.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** [P2, area/security]
   Auto Memory currently sends transcript content to the model before redaction, meaning secrets could be exposed in model context. A clear security concern.

7. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** [P2, kind/bug]
   Auto Memory only marks sessions as processed after a successful `read_file`. Low-signal sessions that the agent chooses to skip remain unprocessed and are repeatedly surfaced — a wasteful and annoying loop.

8. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** [P1, kind/bug]
   The browser subagent crashes on Wayland despite reporting "GOAL" termination. Linux users on modern display servers are effectively blocked from browser-based automation.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** [P2, kind/customer-issue]
   Users report agents using `git reset`, `--force`, and dangerous database operations when safer alternatives exist. The community is asking for guardrails, not just warnings. **1 👍**

10. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** [P2, kind/bug]
    A hard platform limit causes failures when tool count exceeds 128. Users expect the agent to scope tools dynamically rather than hitting API constraints.

## Key PR Progress

1. **[#27729 — Fix telemetry metric truncation](https://github.com/google-gemini/gemini-cli/pull/27729)** [P2, area/enterprise]
   Truncates telemetry metric attributes to 1024 characters to prevent GCP export errors that currently flood the terminal with stack traces during JSON output.

2. **[#27730 — Fix: keep array tool results out of structuredContent](https://github.com/google-gemini/gemini-cli/pull/27730)** [P1, area/extensions]
   Prevents `McpComplianceTransport` from copying JSON arrays into `structuredContent`, preserving original text content for array-valued tool results. Fixes #27725.

3. **[#27718 — Fix(core): keep auto visible without preview access](https://github.com/google-gemini/gemini-cli/pull/27718)** [P2, area/core]
   Marks the top-level `auto` alias as non-preview so it remains visible in `/model` when dynamic model configuration is enabled — an important UX fix for non-preview users.

4. **[#23030 — feat(cli): implement non-invasive UX Journey testing framework](https://github.com/google-gemini/gemini-cli/pull/23030)** [size/l]
   Introduces a "White Box" testing framework for terminal UI, enabling verification of React component presence and visual state without manual instrumentation. Recently marked as Stale but represents a significant QA investment.

5. **[#22456 — feat(ui): add new interactive policies dialog](https://github.com/google-gemini/gemini-cli/pull/22456)** [P1, size/xl]
   Replaces text-based `/policies` output with an interactive `PoliciesDialog` featuring searchable, tabbed categorization (Allow, Ask, Deny). Also marked Stale but a major UI improvement.

6. **[#27925 — chore(deps): bump the npm-dependencies group with 53 updates](https://github.com/google-gemini/gemini-cli/pull/27925)** [size/xl]
   A massive dependency refresh including SDK, octokit, and ESLint plugin updates. Closed today — signals the project is keeping pace with upstream changes.

7. **[#27929 — chore(deps): bump @google/genai from 1.30.0 to 2.8.0](https://github.com/google-gemini/gemini-cli/pull/27929)** [size/m]
   Major version bump for the GenAI SDK. This brings in new capabilities and breaking changes that will affect tool execution and model interaction.

8. **[#27931 — chore(deps): bump puppeteer-core from 24.39.0 to 25.1.0](https://github.com/google-gemini/gemini-cli/pull/27931)** [size/l]
   Major browser automation dependency bump. Relevant to ongoing browser subagent reliability issues (see #21983).

9. **[#27926 — chore(deps): bump google-auth-library from 9.15.1 to 10.7.0](https://github.com/google-gemini/gemini-cli/pull/27926)** [size/m]
   Auth library major version bump. Important for enterprise and 1P agent authentication flows.

10. **[#27928 — chore(deps): bump undici from 7.24.5 to 8.4.0](https://github.com/google-gemini/gemini-cli/pull/27928)** [size/m]
    HTTP client major version bump. Relevant to network-related tool execution reliability.

## Feature Request Trends

- **AST-aware code analysis**: Multiple issues (#22745, #22746, #22747) explore replacing naive file reads and searches with AST-aware tools to improve precision, reduce token waste, and enable smarter codebase mapping.
- **Agent self-awareness**: #21432 requests that the agent understand its own CLI flags, hotkeys, and execution model well enough to act as its own expert guide — essentially, "dogfooding" improvements.
- **Robust evaluation infrastructure**: #24353 (component-level evals) and #23166 (internal project eval stabilization) show a concerted push toward systematic quality measurement beyond benchmarks.
- **User-controlled safety boundaries**: #22672 (discourage destructive behavior) and #21000 (native file tools for task tracking) indicate demand for better guardrails and user-configurable boundaries on agent actions.

## Developer Pain Points

- **Agent hangs and unreliability**: Three P1 bugs (#21409, #22323, #25166) all involve agents hanging or misreporting termination status. The pattern suggests systemic issues in sub-agent lifecycle management and shell I/O handling.
- **Subagent configuration ignored**: Issues #22267 (Browser Agent ignores `settings.json`), #22093 (subagents running without permission), and #21968 (model doesn't use custom skills) point to a gap between intended configuration and agent behavior.
- **Auto Memory inefficiency**: #26522 (infinite retry of low-signal sessions), #26525 (secrets exposed before redaction), and #26523 (invalid patches silently skipped) paint a picture of a memory system that is both wasteful and insecure.
- **Browser agent fragility**: #21983 (Wayland failure) and #22232 (session lock recovery) highlight the browser subagent as a particularly brittle component.
- **Tooling edge cases**: #24246 (400 error with >128 tools), #23571 (tmp scripts in random spots), and #22466 (incorrect `\n` escape behavior) show accumulated rough edges in tool execution and output formatting.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-06-15

## Today’s Highlights
No new releases or pull requests landed in the past 24 hours, but the issue tracker saw activity around two emerging themes: **agent skill execution reliability** and **session poisoning by malformed attachments**. The community is also asking for better BYOK/custom provider support and deeper Azure DevOps integration via the “Up next” panel.

## Releases
*None in the last 24 hours.*

## Hot Issues
All 8 issues updated in the last 24 hours are listed below. One was closed as invalid/spam and is noted separately.

1. **#956 – [area:agents] Agent skills scripts executed in wrong folder**  
   *[OPEN]* – Author: msundman78 | Updated: 2026-06-14 | 👍: 2  
   When a skill references a script via `scripts/myscript.sh` (as per spec), Copilot CLI runs it from an unexpected directory. This breaks workflows that rely on relative paths. Community comments (6) suggest this is a regression.  
   🔗 [github/copilot-cli Issue #956](https://github.com/github/copilot-cli/issues/956)

2. **#3558 – [area:context-memory, area:models] Duplicate Item Errors**  
   *[OPEN]* – Author: psulightning | Updated: 2026-06-14 | 👍: 7  
   After an initial prompt, users get `CAPIError: 400` with `"Duplicate item found with id fc_call_...".` The session becomes unusable. High 👍 count signals a widespread frustration.  
   🔗 [github/copilot-cli Issue #3558](https://github.com/github/copilot-cli/issues/3558)

3. **#3797 – [triage] Different prompt input box layout in two cmd tabs in the same window**  
   *[OPEN]* – Author: kunalk16 | Updated: 2026-06-15 | 👍: 0  
   UI inconsistency: the input box renders with different widths/heights across terminal tabs. Likely a rendering bug in the TUI layer.  
   🔗 [github/copilot-cli Issue #3797](https://github.com/github/copilot-cli/issues/3797)

4. **#3796 – [invalid] hhhhhhh (spam)**  
   *[CLOSED]* – Author: TAREQ097H | Updated: 2026-06-14  
   No valid content. Closed as invalid.  
   🔗 [github/copilot-cli Issue #3796](https://github.com/github/copilot-cli/issues/3796)

5. **#3795 – [triage] Feature request: opt-in model discovery for BYOK / custom providers**  
   *[OPEN]* – Author: aosama | Updated: 2026-06-14 | 👍: 0  
   When using BYOK (custom provider) mode, users must manually set `COPILOT_MODEL` or pass `--model`. The CLI does not query the provider’s available models. The request is for opt-in auto-discovery.  
   🔗 [github/copilot-cli Issue #3795](https://github.com/github/copilot-cli/issues/3795)

6. **#3794 – [triage] Add Azure DevOps work items to “Up next”**  
   *[OPEN]* – Author: OmerMicro | Updated: 2026-06-14 | 👍: 0  
   The cross-session “Up next” panel currently only surfaces GitHub issues/PRs. For projects backed by Azure DevOps, it remains empty. Request to also show assigned ADO work items.  
   🔗 [github/copilot-cli Issue #3794](https://github.com/github/copilot-cli/issues/3794)

7. **#3791 – [triage] Malformed attachment poisons session; all subsequent turns fail with 400**  
   *[OPEN]* – Author: jay-tau | Updated: 2026-06-14 | 👍: 0  
   A password‑protected `.xlsx` attachment causes a CAPI 400 on first turn. Even after removing the attachment, all later turns in the same session continue failing with the same error.  
   🔗 [github/copilot-cli Issue #3791](https://github.com/github/copilot-cli/issues/3791)

8. **#3793 – [triage] 590A:31190E:55961D:614135:6A2E7EBC … (crash dump)**  
   *[OPEN]* – Author: ja552588 | Updated: 2026-06-14 | 👍: 0  
   No description or steps provided; only memory addresses. Possibly a segmentation fault or buffer overflow. Without more context, triage will be difficult.  
   🔗 [github/copilot-cli Issue #3793](https://github.com/github/copilot-cli/issues/3793)

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
Two distinct feature directions emerged from recent issues:

- **BYOK model discovery** ( #3795 ) – Users want the CLI to automatically fetch available models from custom providers rather than requiring manual model identifiers.
- **Cross‑platform work‑item integration** ( #3794 ) – Expanding the “Up next” inbox to support Azure DevOps alongside GitHub, reflecting the growing number of mixed‑platform teams.

## Developer Pain Points
Three recurring frustrations stand out from the issues updated this period:

- **Session state corruption** – A malformed attachment ( #3791 ) or duplicate‑item errors ( #3558 ) can permanently poison a session, forcing a restart. This disrupts long interactive workflows.
- **Agent skill path resolution** ( #956 ) – Relative script paths defined in SKILLS.md are not honored, breaking portability of skill definitions.
- **UI inconsistencies** ( #3797 ) – Different terminal tab renderings of the input box reduce predictability, especially for power users with multi‑window setups.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-15

## Today's Highlights

A new bug report (#2451) reveals that Kimi Code CLI’s built-in system prompt can override user-provided guidelines, raising concerns about workflow control. Meanwhile, community frustration over aggressive rate limiting continues to grow (#2123). On the positive side, a PR (#2452) improves the reliability of multi-edit file operations by failing early when hunks are unmatched, and several Windows-specific fixes have been merged (e.g., Alt+V paste, per-process log files).

## Releases

*No new releases in the last 24 hours.*

## Hot Issues

**#850** (CLOSED) – [Feature Request] Auto-load project context/rules (e.g., AGENTS.md, .cursorrules) at session start  
*Author: Al4ric · Updated: 2026-06-14*  
This feature request, inspired by Claude Code’s `CLAUDE.md` auto-detection, asks Kimi Code to read project-level configuration files on startup. It was closed after discussion, indicating that the team may have a different approach planned or deemed it out of scope. The single 👍 suggests moderate interest.  
[Issue #850](https://github.com/MoonshotAI/kimi-cli/issues/850)

**#2123** (OPEN) – 限速，限额严重 (Severe rate limiting and quota issues)  
*Author: littlePoBoy · Updated: 2026-06-14*  
A Chinese-language complaint alleging that actual API request limits are far below the advertised “300–1200 requests per 5 hours” (user reports ~60+ calls). The user accuses Moonshot of non-transparent quota disclosure and poor refund policy, referencing consumer protection laws. This issue remains open and has 2 comments, reflecting ongoing dissatisfaction.  
[Issue #2123](https://github.com/MoonshotAI/kimi-cli/issues/2123)

**#2451** (OPEN) – [bug] System prompt conflicting with my desired workflow  
*Author: iaindooley · Created: 2026-06-14*  
The user reports that Kimi Code’s system prompt (built-in) overrides their own explicit guidelines, making it impossible to enforce strict coding conventions. No comments yet, but this is a fresh, high-signal bug that could affect many power users.  
[Issue #2451](https://github.com/MoonshotAI/kimi-cli/issues/2451)

## Key PR Progress

**#2452** (OPEN) – fix(tools): fail StrReplaceFile when a multi-edit hunk is unmatched  
*Author: Osamaali313 · Updated: 2026-06-14*  
Fixes a subtle bug where `StrReplaceFile` would silently succeed if the total string was changed, even if individual edits made no replacements. The fix now fails early with a clear error when a hunk doesn’t match, improving reliability in multi-edit scenarios.  
[PR #2452](https://github.com/MoonshotAI/kimi-cli/pull/2452)

**#2018** (CLOSED) – feat: add Alt+V paste support for Windows Terminal  
*Author: LittleDrinks · Updated: 2026-06-14*  
Adds `Alt+V` as a fallback paste keybinding because Windows Terminal intercepts `Ctrl+V`. Merged after a Devin review, improving the CLI experience on Windows.  
[PR #2018](https://github.com/MoonshotAI/kimi-cli/pull/2018)

**#2020** (CLOSED) – fix: use per-process log filenames to prevent rotation lock on Windows  
*Author: LittleDrinks · Updated: 2026-06-14*  
When multiple `kimi` processes run, log rotation on Windows fails with `PermissionError`. This PR renames logs to `kimi.{pid}.log` to eliminate file contention. Merged.  
[PR #2020](https://github.com/MoonshotAI/kimi-cli/pull/2020)

**#839** (CLOSED) – feat(shell): add configurable shell support for Windows  
*Author: HamzaETTH · Updated: 2026-06-14*  
Adds configuration to use different shells (e.g., PowerShell, cmd) on Windows. Merged after maintainer discussion, enabling better Windows integration.  
[PR #839](https://github.com/MoonshotAI/kimi-cli/pull/839)

## Feature Request Trends

- **Auto‑load project context files**: The top feature request (#850) asks for automatic detection of project-specific rules (e.g., `AGENTS.md`, `.cursorrules`), mirroring Claude Code’s `CLAUDE.md` workflow. This is a clear signal that users want Kimi Code to respect shared project conventions without manual setup.
- **Transparent rate limits**: Issue #2123 highlights demand for clear, detailed disclosure of Code Plan quotas and rate‑limit behavior. Users want predictability and a “no surprises” billing model.
- **System prompt customization**: Issue #2451 implies users want the ability to completely override or inject their own system prompts without interference from built-in instructions.

## Developer Pain Points

- **Aggressive rate limiting / insufficient quota**: The most vocal pain point (#2123) – developers report that the actual usable request count is far below advertised numbers, making the “Code Plan” subscription unusable for real work. Lack of official documentation exacerbates frustration.
- **System prompt conflicts**: Users with strict coding guidelines find that Kimi Code’s built-in prompt clobbers their own instructions (#2451). This creates a mismatch between user intent and model behavior.
- **Windows‑specific friction**: While recent PRs have addressed paste (`Alt+V`) and log rotation, the Windows experience still lags behind Linux/macOS. Community contributions (like #839 and #2018) show ongoing demand for parity.
- **Multi‑edit reliability**: The bug fixed in #2452 (silent failures on hunks) points to a broader need for robust file editing primitives that give clear feedback when partial edits fail.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-15

## Today's Highlights

A tight release cadence continues with **v1.17.7** shipping critical plugin session fixes and MCP improvements. The community is heavily discussing a **permanent 75% price drop for DeepSeek V4 Pro** (#28846, 77 comments) and the long-standing **CLI copy/paste blocker** (#13984, 48 comments). Meanwhile, PRs are landing to resolve **OAuth callback port leaks**, **MCP tool error handling**, and **Linux clipboard selection** — reflecting a strong push toward stable, extensible infrastructure.

---

## Releases

### v1.17.7 (last 24h)
[View release](https://github.com/anomalyco/opencode/releases/tag/v1.17.7)

**Bugfixes**
- Plugin client requests now reuse the active server instead of assuming default local port.
- ACP shell tool calls display the command and working directory from the start.
- Plugin-provided shell environment variables now apply to PTY sessions.

**Improvements**
- MCP client alignment: improvements to OAuth callback lifecycle and tool result error routing.

**Note:** A new regression surfaced in this version — `EditBuffer destroyed` errors on macOS Tahoe (#32348) — under active investigation.

---

## Hot Issues

1. **#28846 – Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction**  
   *Author: icocoon | Comments: 77 | 👍 79*  
   Community overwhelmingly supports passing the API cost savings to subscribers. The high engagement signals pricing sensitivity and expectations for rapid adjustments.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28846)

2. **#13984 – Cannot copy and paste in OpenCode CLI**  
   *Author: hongyesuifeng | Comments: 48 | 👍 20*  
   A persistent TUI usability blocker (open since Feb). No official fix yet, but PR #32370 (Linux clipboard selection) targets the X11 part.  
   [GitHub](https://github.com/anomalyco/opencode/issues/13984)

3. **#15585 – "free usage exceed" when using free models**  
   *Author: Howard-Zhou-77 | Comments: 48 | 👍 13*  
   Users report hard limits even on free-tier models, creating confusion. Closed but still debated — may need clearer documentation.  
   [GitHub](https://github.com/anomalyco/opencode/issues/15585)

4. **#5305 – Plugin Hook for Instant TUI Commands**  
   *Author: malhashemi | Comments: 18 | 👍 13*  
   Request for a plugin hook that registers commands executing without agent involvement. Core to extending the TUI.  
   [GitHub](https://github.com/anomalyco/opencode/issues/5305)

5. **#28957 – "Upstream idle timeout exceeded"**  
   *Author: VENAXIS | Comments: 13 | 👍 0*  
   Session timeouts when using the `writing-plans` skill, possibly related to macOS Tahoe 26.5. Infrastructure-level concern.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28957)

6. **#28567 – Full MCP client capabilities**  
   *Author: Arcadi4 | Comments: 11 | 👍 21*  
   Calls to catch up with latest MCP spec (streaming, resources, prompts). Very high community consensus.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28567)

7. **#32172 – Add GLM-5.2 model support for Z.AI provider**  
   *Author: phalla-doll | Comments: 7 | 👍 0*  
   Z.AI's newest reasoning model request. Relatively new issue but reflects constant demand for provider diversity.  
   [GitHub](https://github.com/anomalyco/opencode/issues/32172)

8. **#28202 – Plugin async prompts overlap with Web prompt_async**  
   *Author: ririnto | Comments: 6 | 👍 4*  
   Concurrent async prompts create duplicate assistant siblings in the Web UI. Now closed after a plugin-side fix in PR #28152.  
   [GitHub](https://github.com/anomalyco/opencode/issues/28202)

9. **#26412 – Custom OpenAI-compatible provider: "Expected 'function.name' to be a string"**  
   *Author: mazingerzzz | Comments: 6 | 👍 0*  
   Streaming tool call chunks break with vLLM backends. Blocks self-hosted users.  
   [GitHub](https://github.com/anomalyco/opencode/issues/26412)

10. **#11829 – Recursive Language Model (RLM) Context Management**  
    *Author: chindris-mihai-alexandru | Comments: 6 | 👍 11*  
    A novel approach to context window limits using external queryable environment. Research-backed and gaining traction.  
    [GitHub](https://github.com/anomalyco/opencode/issues/11829)

---

## Key PR Progress

1. **#32370 – Linux clipboard selection**  
   *Author: bornmw*  
   Adds `linux_clipboard_selection` config for PRIMARY buffer support. Fixes the long-standing copy-paste issue for Linux TUI.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32370)

2. **#31848 – Use server-side picker for all HTTP connections**  
   *Author: zhizhizheng*  
   Fixes native file picker inconsistencies when using remote connections. Closes #25264.  
   [GitHub](https://github.com/anomalyco/opencode/pull/31848)

3. **#31993 – Restore desktop "Open in" menu**  
   *Author: PatrickLarocque*  
   Fixes two regressions that broke the session header's directory picker.  
   [GitHub](https://github.com/anomalyco/opencode/pull/31993)

4. **#32245 – Stop idle OAuth callback server**  
   *Author: rekram1-node*  
   Releases port 19876 after authentication completes, preventing cross-instance CSRF errors.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32245)

5. **#32241 – Render move errors inline**  
   *Author: rekram1-node*  
   Keeps error states inside `DialogSelect` instead of breaking the UI flow. Improved UX for MCP tool failures.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32241)

6. **#31867 – Improve DeepSeek prompt cache reuse**  
   *Author: ChangedenCZD*  
   Removes date injection from system prompt to boost cache hit rates, reducing API costs.  
   [GitHub](https://github.com/anomalyco/opencode/pull/31867)

7. **#32367 – Fix worktrees from empty git repos**  
   *Author: wgu9*  
   `git worktree add` now works on repos with no commits. Fixes #20910.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32367)

8. **#32302 – Forward parent attachments to subagents**  
   *Author: 21pounder*  
   Solves attachment handoff failure for `@mention` subagents in the `task` path.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32302)

9. **#32364 – Reset terminal modes on TUI shutdown**  
   *Author: wgu9*  
   Ensures `raw` mode and title are cleaned up, preventing terminal corruption after crashes.  
   [GitHub](https://github.com/anomalyco/opencode/pull/32364)

10. **#32238 – Avoid search retention for file reads**  
    *Author: hereswilson*  
    Prevents unnecessary search state initialization when reading files, reducing memory overhead.  
    [GitHub](https://github.com/anomalyco/opencode/pull/32238)

---

## Feature Request Trends

- **MCP Client Parity** (#28567, #5305): Strong demand for full MCP spec support — streaming, resources, prompts, and plugin hooks for instant commands.
- **Model & Provider Expansion** (#28846, #32172, #31475): Users expect rapid integration of new models (DeepSeek V4 Pro price changes, GLM-5.2, Composer 2.5) and flexible pricing adjustments.
- **Context & Session Management** (#11829, #32368, #24017): Interest in RLM-style external context, revertible compaction, and bookmark/save capabilities for conversations.
- **TUI/UX Enhancements** (#30763, #19528): User-defined session flags ("statuses"), toggleable "Allow always" confirmation, and better visual feedback.
- **Remote & Workspace Features** (#31901, #30355): SSH directory references and proper subagent workspace inheritance for multi-machine workflows.

---

## Developer Pain Points

- **Clipboard & Terminal Oddities** (#13984, #16521, #32370): Copy/paste failures in CLI and blank-line collapsing remain high-friction for daily use.
- **Plugin System Instability** (#28037, #29894, #28202): Silent drops of permission replies, aborts not cancelling turns, and async prompt overlaps erode trust.
- **Timeout & Crash Spikes** (#28957, #32346, #32334): Model idle timeouts, Qwen 3.7 freezes, and `EditBuffer destroyed` errors after upgrades frustrate users.
- **Security & Environment Leaks** (#31778, #23563): MCP subprocesses receive full `process.env`; OAuth callbacks not cleaned up — both are vectors for credential exposure.
- **Build & Compatibility** (#32358, #26412, #31002): Arch package failures, custom provider streaming errors, and AJV schema warnings for non-standard `format` values.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi community digest – 2026-06-15

## Today’s Highlights
The community is focused on a wave of **regression fixes and maintainability improvements**. A long‑standing Windows bash detector bug (#5103) and a **broken Escape key interrupt** (#5736) are getting urgent attention, while the **Shrinkwrap dependency duplication** issue (#5653) is driving a planned migration. On the PR side, a **behaviour‑preserving refactor of the model‑registry generator** (#5743) landed in response to a detailed maintainability report (#5702), and a **first‑run terminal‑theme detection** (#5385) is nearing completion. No new releases were published in the last 24 hours.

## Releases
No new versions in the last 24h.

## Hot Issues
1. **[#5103 – Windows bash detector fails when Git Bash is on non-default path](https://github.com/earendil-works/pi/issues/5103)**  
   Open, 18 comments. The built‑in bash detection hard‑codes `C:\Program Files`, causing false negatives for users with Git Bash on other drives. Community wants a PATH‑based fallback. No likes yet, but high discussion.

2. **[#5653 – Move off Shrinkwrap (duplicate dependency copies)](https://github.com/earendil-works/pi/issues/5653)**  
   Open, 9 comments. Installing both `pi-ai` and `pi-coding-agent` as direct deps leads to two module‑level `Map` instances, breaking API provider registry. Flagged as `inprogress` – the team is planning to replace Shrinkwrap.

3. **[#5702 – prompt_cache_retention sent to providers that reject it + maintainability of generate-models.ts](https://github.com/earendil-works/pi/issues/5702)**  
   Closed, 6 comments. A thorough bug report that uncovered a cascading issue: `cache_control` TTL gets sent to models that don’t support it, and the model‑generation script is hard to maintain. PR #5743 addresses the latter.

4. **[#5736 – Escape no longer interrupts active interactive task](https://github.com/earendil-works/pi/issues/5736)**  
   Open (inprogress), 6 comments. A critical UX regression – the advertised cancel key doesn’t work reliably. Co‑authored with gpt‑5.5, likely to be high priority.

5. **[#5671 – ~/.pi and cwd/.pi overlap](https://github.com/earendil-works/pi/issues/5671)**  
   Open, 5 comments, 👍3. Raised by mitsuhiko: when `$HOME` is also the working directory, global and project settings collide. Simple fix proposed (rename global folder), but impacts many users.

6. **[#5654 – Add `excludeFromContext` to custom messages](https://github.com/earendil-works/pi/issues/5654)**  
   Open, 6 comments, 👍1. Extensions want to send invisible messages (e.g., status updates) that don’t consume context. PR #5678 already implements this.

7. **[#5700 – Support multiple live agent sessions with TUI switching](https://github.com/earendil-works/pi/issues/5700)**  
   Open, 4 comments. A feature request to allow concurrent agent sessions, switching between them in the TUI without tearing down. Popular among power users.

8. **[#5303 – Bash tool truncates output when child holds stdout past exit](https://github.com/earendil-works/pi/issues/5303)**  
   Open (inprogress), 3 comments. A long‑standing bug that silently loses output (e.g., git commit with lint‑staged). References #2630 – community wants a reliable fix.

9. **[#5575 – kimi‑k2.6 via OpenCode Go fails with JSON Schema conflict](https://github.com/earendil-works/pi/issues/5575)**  
   Closed, 4 comments. A provider‑specific 400 error when tools are enabled. Already resolved in the latest commit, but highlights ongoing compatibility issues with third‑party providers.

10. **[#5728 – Support provider‑specific config in auth.json](https://github.com/earendil-works/pi/issues/5728)**  
    Open, 2 comments. Users need to pass `accountId`/`gatewayId` for providers like Cloudflare AI Gateway. Currently only env vars are supported – a common pain point for multi‑account setups.

## Key PR Progress
1. **[#5743 – refactor(ai): decompose generate-models.ts into a data‑driven generator](https://github.com/earendil-works/pi/pull/5743)**  
   Closed. Behaviour‑preserving refactor addressing the maintainability concerns from #5702. Replaces ~30‑branch cascades with declarative descriptors. Draft was well received.

2. **[#5738 – fix(ai): price anthropic 1h cache writes at 2x input](https://github.com/earendil-works/pi/pull/5738)**  
   Open. Fixes cost undercount for 1‑hour cache writes (was using 5‑minute rate). Reads `ephemeral_1h_input_tokens` correctly.

3. **[#5678 – Add `excludeFromContext` for custom messages](https://github.com/earendil-works/pi/pull/5678)**  
   Open. Implements the feature requested in #5654. Also teaches compaction and branch summarization to skip excluded messages.

4. **[#5735 – fix(coding-agent): defer extension reload requests safely](https://github.com/earendil-works/pi/pull/5735)**  
   Open. Makes `ctx.reload()` safe from any extension context, not just slash commands. Uses deferral to avoid mid‑task reloads.

5. **[#5732 – feat(extensions): support `allowCommands` option in `sendUserMessage`](https://github.com/earendil-works/pi/pull/5732)**  
   Closed. Extensions can now programmatically trigger slash commands (e.g., session resets) by enabling prompt template expansion.

6. **[#5711 – feat(coding-agent): add extension prompt guideline API](https://github.com/earendil-works/pi/pull/5711)**  
   Open. Implements `pi.setPromptGuidelines()` from #5710, allowing extensions to inject project‑specific instructions.

7. **[#5385 – feat: detect first‑run terminal theme](https://github.com/earendil-works/pi/pull/5385)**  
   Closed (inprogress). Queries the terminal via OSC for light/dark theme and persists to settings. A quality‑of‑life improvement for new users.

8. **[#5731 – feat(coding-agent): Add tool instrumentation for execution profiling](https://github.com/earendil-works/pi/pull/5731)**  
   Closed. Adds timing/logging for tool execution – useful for performance tuning and extension developers.

9. **[#5708 – Wrap question extension text instead of truncating](https://github.com/earendil-works/pi/pull/5708)**  
   Closed. Fixes #5707 – long extension prompts are now wrapped instead of cut off.

10. **[#5714 – add xAI Grok account OAuth login](https://github.com/earendil-works/pi/pull/5714)**  
    Closed. Adds built‑in OAuth support for xAI Grok, including device‑code login and refresh tokens. Expands provider options.

## Feature Request Trends
- **Extension API expansion**: Multiple requests for richer extension capabilities – `excludeFromContext`, `allowCommands`, `setPromptGuidelines`, and raw provider response hooks (`after_provider_response`) – indicate a growing ecosystem of third‑party extensions.
- **Multiple concurrent sessions**: Users want to run background agents while switching between sessions in the TUI, without teardown (#5700).
- **Provider‑specific configuration**: Interest in carrying provider‑specific parameters (e.g., account ID, gateway ID) in `auth.json`, not just environment variables (#5728).
- **Model‑specific compaction**: Users want per‑model compaction token limits instead of global settings, especially for small local models (#5722).
- **First‑run experience**: Terminal theme detection (#5385) and improved help formatting (#5055) suggest a push for smoother onboarding.

## Developer Pain Points
- **Escape key interrupt unreliability** (#5736, #5685) – a core UX fader that frustrates daily use.
- **Bash tool output truncation** (#5303) – silent data loss during git commits and similar child‑process scenarios.
- **Windows bash detector broken on non‑default paths** (#5103) – a recurring Windows‑specific issue.
- **Duplicate dependency copies due to Shrinkwrap** (#5653) – leads to subtle bugs in module‑level state.
- **Terminal rendering issues**: WezTerm image breaks (#5618), chat scroll jumps on Windows (#5576), CJK overlay misalignment (#5297) – cross‑platform polish gaps.
- **`generate-models.ts` maintainability** (#5702, #5743) – the monolithic model‑registry generator is a pain point for contributors adding new providers.
- **Interactive mode hangs with local LLMs** (#5706) – blocking at summary approval when using local backends, while cloud providers work fine.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-15

## Today's Highlights
A notable uptick in security and compliance issues dominated the conversation, with a Trojan false-positive report on the VSIX package (issue #5055) and a permission‑contract side‑effect bypass (#5102) raising community concern. On the development front, two nightly release workflows failed (v0.18.0‑nightly), while PRs advanced toward token‑aware task details (#5118) and dynamic workflow meta‑extraction (#5094). The long‑running OAuth free‑tier policy debate (#3203) remains active with 135+ comments.

## Releases
No new releases were published in the last 24 hours.

## Hot Issues

1. **[#3203 – Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)**  
   *Type: Feature request / Status: Open*  
   Proposes reducing the daily free quota from 1,000 to 100 requests and eventually closing the free tier. With 135 comments, this is the most discussed issue — community reactions are polarized between concerns about accessibility and calls for a viable Pro plan.

2. **[#5055 – Trojan:JS/ShaiWorm.DBA!MTB detected in VSIX](https://github.com/QwenLM/qwen-code/issues/5055)**  
   *Type: Bug / Priority P1 / Status: Open*  
   Windows users report that Microsoft Defender flags the `qwen-code-vscode-ide-companion-0.18.0-win32-x64.vsix` as a Trojan. The team is investigating the false positive, but the issue affects trust and adoption on Windows.

3. **[#5102 – Permission‑contract side effect executed despite probe](https://github.com/QwenLM/qwen-code/issues/5102)**  
   *Type: Bug / Priority P2 / Status: Open*  
   A provider‑requested shell command writes a side‑effect file during the permission probe itself, defeating the contract mechanism. This raises serious security implications for non‑interactive CLI usage.

4. **[#5080 – API key mixup with Token Plan endpoints](https://github.com/QwenLM/qwen-code/issues/5080)**  
   *Type: Bug / Priority P2 / Status: Open*  
   Using a standard Alibaba Cloud API key after selecting a Token Plan provider causes a 401 error. Users expect seamless switching between connection modes.

5. **[#5101 – Repeated large tool results balloon context](https://github.com/QwenLM/qwen-code/issues/5101)**  
   *Type: Bug / Priority P1 / Status: Open*  
   When a provider repeatedly requests a command with large output, Qwen Code keeps sending full tool‑result records, eventually exhausting context limits. Underlying token management is stressed.

6. **[#5119 – No sudo command handling in permission dialogue](https://github.com/QwenLM/qwen-code/issues/5119)**  
   *Type: Feature request / Status: Open*  
   Agents attempting `sudo` commands fail ungracefully, forcing users to manually copy–paste. A smoother prompt to allow elevation is requested.

7. **[#4218 – MCP filesystem connected but tools unavailable](https://github.com/QwenLM/qwen-code/issues/4218)**  
   *Type: Bug / Status: Open*  
   The UI shows the `filesystem` MCP server as connected, but the model cannot invoke its tools. Windows users are especially affected, and the root cause is still under triage.

8. **[#5052 – CI PR review job reports green on API error](https://github.com/QwenLM/qwen-code/issues/5052)**  
   *Type: Bug / Priority P2 / Status: Closed*  
   The `review-pr` job exits 0 when the model connection drops mid‑review, posting no comments. A “false success” undermines CI trust.

9. **[#4369 – RAM leak and reliance on AI‑generated fixes](https://github.com/QwenLM/qwen-code/issues/4369)**  
   *Type: Bug / Status: Closed*  
   A user complains that manual memory‑leak debugging is hindered by AI‑generated patches. Suggests streaming display and file‑based history instead of in‑memory bloat.

10. **[#5117 – Nightly release failed for v0.18.0](https://github.com/QwenLM/qwen-code/issues/5117)**  
    *Type: CI / Status: Open*  
    The nightly release workflow failed (same for #5068 on 2026‑06‑13). Repeated failures may delay feature delivery and signal CI pipeline fragility.

## Key PR Progress

1. **[#5094 – Workflow P4a: extractAndStripMeta + meta on RunOutcome](https://github.com/QwenLM/qwen-code/pull/5094)**  
   *Author: LaZzyMan*  
   Implements the first half of dynamic workflow meta‑extraction, building on the merged P1–P3. Essential for future multi‑step agent orchestration.

2. **[#5118 – Per‑task token & time detail on completed todos](https://github.com/QwenLM/qwen-code/pull/5118)**  
   *Author: wenshao*  
   Expands the web‑shell todo list to show start/end times, elapsed duration, and token breakdowns (input, output, cached). Improves cost visibility.

3. **[#5121 – Fix release integration env controls](https://github.com/QwenLM/qwen-code/pull/5121)**  
   *Author: yiliang114*  
   Restores implicit debug‑log and Docker sandbox controls that broke after recent logging changes. Directly addresses the nightly release failures.

4. **[#5120 – Skip auto‑title generation when history has no user message](https://github.com/QwenLM/qwen-code/pull/5120)**  
   *Author: yuanyuanAli*  
   Prevents `tryGenerateSessionTitle` from running on empty or prompt‑only sessions. Reduces unnecessary API calls for daemon‑created sessions.

5. **[#4866 – Split PR triage into 4‑job pipeline](https://github.com/QwenLM/qwen-code/pull/4866)**  
   *Author: yiliang114*  
   Refactors the monolithic triage workflow into a staged pipeline with separate jobs for resolve, product‑decision, code‑review, and merge. Improves CI modularity.

6. **[#4850 – Interactive multi‑tab extensions manager](https://github.com/QwenLM/qwen-code/pull/4850)**  
   *Author: BZ‑D*  
   Turns `/extensions` into a three‑tab interface (Installed, Discover, Sources) covering the full lifecycle of extensions and MCP servers. A major UX upgrade.

7. **[#4564 – Token usage statistics for cost visibility](https://github.com/QwenLM/qwen-code/pull/4564)**  
   *Author: shenyankm*  
   Adds persisted daily/monthly token usage with model/auth‑type breakdowns, plus CSV/JSON export. Directly addresses the long‑standing need for cost tracking.

8. **[#4653 – Configurable agent ignore files](https://github.com/QwenLM/qwen-code/pull/4653)**  
   *Author: shenyankm*  
   Supports `.agentignore` and `.aiignore` alongside `.qwenignore`, with a new `context.ignoreFiles` config option. Useful for mixed‑tool projects.

9. **[#5001 – Optional [HH:MM:SS] timestamps before assistant turns](https://github.com/QwenLM/qwen-code/pull/5001)**  
   *Author: ZijianZhang989*  
   Adds a `output.showTimestamps` setting to display real‑time timestamps in CLI output. Helps users track session duration.

10. **[#4943 – `--safe-mode` flag for troubleshooting](https://github.com/QwenLM/qwen-code/pull/4943)**  
    *Author: DennisYu07*  
    Disables all customizations (hooks, extensions, skills, MCP servers, etc.) to create a clean baseline. A long‑requested debug tool for isolating user‑config issues.

## Feature Request Trends
- **Pricing and tiering**: The free‑tier reduction (#3203) and lack of a purchasable Pro plan (#3272) are the most vocal requests. Users want clear, affordable upgrade paths.
- **Rule/instruction system**: Multiple users ask for a persistent rule system akin to Claude Code’s rules or Copilot’s instructions (e.g., #4723) to enforce coding style across sessions.
- **Sudo and privileged command support**: #5119 and similar comments highlight the need for agent‑side elevation handling rather than manual copy‑paste.
- **Token and cost transparency**: #4564, #5118, and #5101 reflect strong demand for per‑task token breakdowns, usage limits, and cost dashboards.
- **UI/UX polish**: Requests include status line wrapping (#5064), showing the active model in the footer (#5104), and LaTeX math rendering (#3439).

## Developer Pain Points
- **Security false positives and bypasses**: The Trojan alert (#5055) and permission‑contract side‑effect (#5102) erode trust, especially for enterprise users.
- **API key and model confusion**: Mixing Alibaba Cloud standard keys with Token Plan endpoints (#5080) causes 401 errors — the authentication layer is error‑prone.
- **MCP integration brittleness**: The filesystem MCP connection with disconnected tools (#4218) and duplicate tool‑call IDs (#5099) point to systemic MCP protocol handling issues.
- **CI reliability**: False‑green PR reviews (#5052) and repeated nightly release failures (#5117, #5068) frustrate contributors and delay releases.
- **Memory and context bloat**: Repeated large tool results (#5101), RAM leaks (#4369), and truncation recovery (#4964) are recurring pain points for long‑running sessions.
- **Daemon and packaging issues**: Segfaults on Ubuntu (#5114) and build environment diagnostics (#5113) suggest daemon module maturity gaps.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-06-15

## Today's Highlights
The project officially rebrands from `deepseek-tui` to **CodeWhale** with the v0.8.60 release, deprecating the legacy npm package. A critical "turn stalled" bug affecting YOLO mode continues to draw community attention, while the maintainer merges a large v0.8.61 branch that bundles community harvests, a Windows freeze fix, and foundational WhaleFlow orchestration work. Multiple PRs are landing for voice input, VS Code extension scaffolding, and provider fallback chains.

## Releases
**v0.8.60** – *CodeWhale* is now the canonical name for the project, CLI, npm package, and release assets. The legacy `deepseek-tui` npm package is deprecated and will receive no further updates. Users migrating from v0.8.x legacy names should follow `docs/REBRAND.md`.

## Hot Issues
*(Top 10 by community activity and severity)*

1. **#2487 – Frequent "Turn stalled – no completion signal received"**  
   High-impact bug where YOLO mode freezes unresponsive. 12 comments, users report `continue` cannot resume.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/2487)

2. **#1186 – Typed persistent permission rules**  
   Community-requested enhancement to extend execpolicy with tool/command/path scope and allow/deny/ask decisions. 8 comments, targeted for v0.9.0.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/1186)

3. **#3147 – MSBuild FileTracker fails in CodeWhale shell**  
   Windows-specific bug blocking `cmake --build` inside the managed shell. 7 comments, user reports VS2022 environment.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/3147)

4. **#1812 – TUI freeze on Windows (crossterm poll)**  
   Intermittent complete UI lockup on Windows 11, process stays alive. 5 comments with log analysis.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/1812)

5. **#2475 – YOLO mode broken when connecting to Burp (MCP)**  
   MCP prompt interrupts tasks in YOLO mode, preventing completion. 4 comments.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/2475)

6. **#1806 – Sub-agent 120s API timeout renders `agent_open` unusable**  
   All sub-agents fail with hard timeout; parallel task offload unusable. 4 comments, triggers deeper checkpointing discussion.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/1806)

7. **#2211 – Sub-agent fanout + hidden worktrees saturate TUI**  
   Max-agents sidebar filled during release work. Maintainer identifies compounded pressure from shell work and sub-agents. 4 comments.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/2211)

8. **#2629 – 401 authentication error with SiliconFlow and Tencent Cloud**  
   Chinese users blocked by incorrect API key handling for OpenAI-compatible providers. 3 comments.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/2629)

9. **#1067 – glibc 2.39 required, breaks on Ubuntu 22.04**  
   Binary compiled against newer glibc; server users on 2.35 cannot run. 3 comments, repeated in #3207.  
   [Issue link](https://github.com/Hmbown/CodeWhale/issues/1067)

10. **#3102 – Add first-class clarification question requests for agents**  
    Feature to let agents ask the user through UI modals instead of chat messages. 3 comments, tied to secrets/permissions UX.  
    [Issue link](https://github.com/Hmbown/CodeWhale/issues/3102)

## Key PR Progress
*(Top 10 by importance and recency)*

1. **#3225 – v0.8.61: community harvest + freeze fix + WhaleFlow foundation**  
   Maintainer’s aggregate branch with 28 commits: fixes Windows TUI freeze, adds WhaleFlow foundation layer, and harvests community tool deferral, auth diagnostics, and Hugging Face support.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/3225)

2. **#3051 – `/voice` slash command for speech-to-text input**  
   Inspired by MiMo Code; enables one-shot recording and AI transcription using existing provider API.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/3051)

3. **#2811 – VS Code local runtime extension scaffold**  
   Official VS Code extension with commands to open CodeWhale, serve HTTP, and check runtime status. Phase 0 scaffold.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2811)

4. **#2102 – Defer low-value native tools by default**  
   Reduces tool catalog startup cost; adds `[tools] always_load` config to opt tools back in.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2102)

5. **#2779 – Dormant provider fallback chain**  
   Adds `fallback_providers` config parsing and `ProviderChain` helper; runtime still uses primary provider.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2779)

6. **#3197 – Rename DeepSeek blue consumers to whale accent**  
   Adds `WHALE_ACCENT_PRIMARY` semantic color token, keeps old name as deprecated alias.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/3197)

7. **#2796 – `/sidebar` slash command**  
   Toggle/show/hide sidebar with optional `--save` persistence for transcript-heavy workflows.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2796)

8. **#2802 – Hugging Face MCP helpers**  
   Adds `/hf mcp status`, `/hf mcp setup`, and related commands for offline MCP configuration.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2802)

9. **#2103 – Fix mouse capture keeping history arrows on Windows**  
   Removes blanket Windows override; restores arrow-key navigation in empty composer.  
   [PR link](https://github.com/Hmbown/CodeWhale/pull/2103)

10. **#2795 – Enrich auth errors with request context**  
    Provides provider, base URL, model, key source/fingerprint in authentication failure messages.  
    [PR link](https://github.com/Hmbown/CodeWhale/pull/2795)

## Feature Request Trends
- **Provider flexibility** – Strong demand for fallback chains (#2574), third-party providers like DeepInfra (#3231), and reasoning_style overrides for non-DeepSeek models (#3222).
- **Multi-agent orchestration** – WhaleFlow swarm synthesis (#3230) and fleet ledger (#3229) indicate growing interest in coordinated sub-agent work with checkpointing and reduce passes.
- **Transparency & telemetry** – Agents need visible token budgets, context pressure, and cost tracking for non-DeepSeek models (#2666, #3066). Users want sub-agent results clearly marked as self-reports (#719) and clipped output warnings (#2652).
- **UX improvements** – First-class clarification questions (#3102), voice input (#3051), and persistent permission rules (#1186) are recurring themes for smoother human-in-the-loop workflows.
- **Platform compatibility** – Native glibc 2.35 support (#1067, #3207), better Windows TUI stability (#1812), and packaging for agent client protocols (#3192).

## Developer Pain Points
- **“Turn stalled” / connection timeouts** – The most frequently reported issue (#2487, #2739, #1786) where YOLO mode or long-running tasks freeze indefinitely; `continue` often fails to recover.
- **Windows UI freezes** – The TUI becomes completely unresponsive, especially with cross-terminal shells and sub-agent activity (#1812, #1679).
- **Sub-agent reliability** – Hard 120s API timeout (#1806) and missing checkpoint/resume (#2029) make parallel tasks unreliable. Output clipping (#2652) can mislead the model.
- **glibc version locked** – Binary requires glibc 2.39+, excluding Ubuntu 22.04 and older server environments (#1067, #3207).
- **Third-party provider auth** – 401 errors with SiliconFlow, Tencent Cloud, and others (#2629) frustrate users outside the default DeepSeek ecosystem.
- **Rebranding friction** – Users stuck with `deepseek-tui` commands after update (#2917), confusing release assets (`codewhale-linux-x64` vs `.tar.gz`) (#3208), and npm update failures (#2924).
- **MSBuild environment** – Windows C++ developers hit FileTracker initialization failures when using CodeWhale’s managed shell (#3147).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*