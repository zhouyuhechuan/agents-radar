# AI CLI Tools Community Digest 2026-06-13

> Generated: 2026-06-13 02:42 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report — 2026-06-13

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing simultaneous maturation and fragmentation. Across seven major tools, the dominant themes are **agent reliability** (unbounded recursion, hangs, false successes), **model access instability** (Fable-5 outages, tier confusion), and **cross-platform pain** (Windows sandbox failures, terminal corruption, keyboard layout bugs). While each tool addresses a similar core use case—AI-assisted coding in the terminal—their architectural philosophies diverge sharply: Claude Code and OpenAI Codex pursue proprietary model ecosystems with deep agentic capabilities, while open-source tools like Pi and CodeWhale prioritize multi-provider flexibility. The community is increasingly vocal about **cost transparency**, **configurable context windows**, and **declarative agent definitions**, signaling a shift from "just works" to "works the way I need it to."

## 2. Activity Comparison

| Tool | Hot Issues (today) | Active PRs | Release Status Today | Notable Pattern |
|---|---|---|---|---|
| **Claude Code** | 10 high-severity | 1 merged | v2.1.176–177 | Fable-5 model access crisis; unbounded sub-agent recursion |
| **OpenAI Codex** | 10 open/closed | 10 active | 4 alpha releases (rust-v0.140.0) | Rapid alpha iteration; Windows sandbox instability dominant |
| **Gemini CLI** | 10 open | 10 merged/active | v0.48.0-nightly | Agent hangs; security credential fixes; tmux terminal quirks |
| **GitHub Copilot CLI** | 10 open | 1 open | v1.0.62-1 | YOLO indicator shipped; keyboard layout bugs; ARM64 panic |
| **Kimi Code CLI** | 3 reported | 1 active | None | Low activity; billing transparency crisis; Python 3.13 fix |
| **OpenCode** | 10 open | 10 merged/active | None | Permission UX bugs; doom loops; SQLite repair commands |
| **Pi** | 10 open | 10 merged/active | v0.79.2 | OpenAI Codex connection reliability; Bedrock fixes |
| **Qwen Code** | 10 open | 10 merged/active | v0.18.0 | OAuth policy backlash; daemon mode; long-context degradation |
| **CodeWhale (DeepSeek TUI)** | 10 open/closed | 10 merged/active | v0.8.59 | Rebrand; agent-fleet infrastructure; multi-provider parity |

**Observation:** OpenAI Codex shows the highest PR velocity (10 active, all substantial), while Claude Code has the most urgent crisis-level issues. Kimi Code shows notably low community activity and response.

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating industry-wide developer demand:

**Multi-Agent Orchestration & Autonomy**
- Claude Code: Tiered Opus/Sonnet worker architecture, extended thinking for sub-agents (#56913, #14321)
- Gemini CLI: Generalist agent hangs, skill/sub-agent underutilization (#21409, #21968)
- OpenCode: Doom loops in agent reasoning and tool calls (#12716, #18108)
- CodeWhale: Fleet scheduler, leases, heartbeats, worker backpressure (#3159)

**Cross-Platform & Windows Reliability**
- OpenAI Codex: Sandbox failures, UAC elevation, EFS encryption, update crashes (multiple overlapping issues)
- Gemini CLI: Wayland browser agent failure (#21983)
- Claude Code: Windows installer HRESULT 0x80073CF6 (#49917)
- Kimi Code: WebSocket failure on Windows 10/11 (#2435)
- Qwen Code: Antivirus false positives on VSIX (#5055), `printf` not found on Windows (#5010)

**Context Window Management & Token Awareness**
- Copilot CLI: Configurable system prompt to reduce 20.5K fixed overhead (#2627, 17👍)
- OpenAI Codex: Context exhaustion on fresh threads (#9046)
- Kimi Code: K2.6 excessive chain-of-thought token burn (#1994)
- Qwen Code: Long-context attention degradation (#5018)
- Pi: `excludeFromContext` flag for custom messages (#5654)

**Custom Slash Commands & Declarative Agent Definitions**
- Copilot CLI: Per-repo `.github/prompts/` custom commands (#618, 99👍)
- Qwen Code: `/import-config` from Claude (#4845), Markdown+YAML agent definitions (#4821)
- CodeWhale: JSON decision contracts for hooks (#3049)
- Gemini CLI: SKILL.md frontmatter parsing (#27873)

**Session Management & History**
- OpenAI Codex: Thread/issue renaming for history navigation (#12564, 111👍)
- Qwen Code: `qwen sessions list` with JSON output and filters (#4825)
- OpenCode: JSON→SQLite migration reliability (#16885)
- Pi: Tab completion refinement (#5670), `parentId` chain integrity on `/fork` (#5669)

**Cost & Billing Transparency**
- Claude Code: Tier confusion with Fable-5 access loss; users feel misled
- Kimi Code: kimiCode usage calculation opaque; K2.6 token drain (#1994)
- Qwen Code: OAuth free tier reduction backlash (#3203, 127 comments)
- OpenCode: Pricing transparency for provider markup models (#32116)

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Model** | Proprietary (Claude) | OpenAI (GPT-5.5) | Gemini | GitHub Copilot | Moonshot K2.6 | Multi-provider | Multi-provider | Qwen | Multi-provider |
| **Target User** | Power users, Max plan | Developers, Pro | GCP/Vertex ecosystem | GitHub enterprise | Chinese devs | OSS contributors | Tinkerers | Chinese & global devs | CLI power users |
| **Key Strength** | Deep agentic capabilities | Rapid alpha iteration | Vertex AI integration | GitHub ecosystem integration | Local LLM support | Permission system | Extensibility | Daemon mode | AI lab pioneer |
| **Weakness** | Opacity; Windows issues | Windows sandbox fragility | Agent reliability | Keyboard input bugs | Low activity | Permission complexity | Stream reliability | Long-context quality | Rebrand friction |
| **Tech Approach** | Proprietary stack | Rust rewrite | Go-based CLI | Rust-based CLI | Python/JS hybrid | TypeScript | TypeScript multi-pkg | Python/TypeScript | Rust/TUI (ratatui) |
| **Community Support** | High engagement | Active, vocal | Moderate | High, forking | Low | Moderate | Moderate | Moderate | Active rebase |

**Key Differentiators:**
- **Claude Code** is the most feature-rich but most opaque—its proprietary model access crises erode trust.
- **OpenAI Codex** is iterating fastest (4 alpha releases/day) but its Windows instability is a critical blocker.
- **Gemini CLI** has strong security focus (Gateway auth, credential caching) but agent reliability gaps undermine its platform value.
- **Copilot CLI** is conservative (1 PR today) but its YOLO indicator and `/` search show incremental UX investment.
- **OpenCode** and **Pi** are architecting for extensibility (permission systems, multi-provider, MCP), appealing to power users who want control.
- **CodeWhale** is aggressively building agent-fleet infrastructure—a differentiator in autonomous multi-agent orchestration.

## 5. Community Momentum & Maturity

**High Momentum (Rapidly Iterating):**
- **OpenAI Codex**: 4 alpha releases today, 10 substantial PRs. The Rust rewrite signals long-term investment. However, the alpha velocity suggests instability—Windows users report frequent regressions.
- **CodeWhale (DeepSeek TUI)**: Rebrand + 10 PRs in one day. The agent-fleet infrastructure (leases, heartbeats, workers) is ambitious and unique. Strong contributor activity.
- **Pi**: 10 PRs, 1 release. Stream reliability fixes and Anthropic Vertex provider competition show high community demand and responsiveness.

**Moderate Momentum (Stable but Active):**
- **Claude Code**: High engagement but crisis-driven. The Fable-5 outage (7+ issues in 24h) is a reputational risk. Only 1 PR merged—development velocity may be constrained by triage load.
- **Gemini CLI**: 10 PRs, all fixes. Security credential work and terminal quirks suggest maturing codebase, but the agent hang bug (#21409, since March) undermines confidence.
- **OpenCode**: 10 PRs, strong focus on database health (db doctor/repair) and MCP session recovery. Permission system complexity is a known friction.

**Lower Momentum (Maintenance Mode?):**
- **Kimi Code CLI**: 3 issues, 1 PR, no release. Community feedback on billing opacity and long-standing bugs (#640, open 5 months) suggests user trust is eroding.
- **Copilot CLI**: 1 PR (scaffold), 1 release. While YOLO indicator and `/` search are welcome, the community is forking (`shell-ai`) due to perceived stagnation.

## 6. Trend Signals

**1. Multi-Provider Architecture Is Becoming Table Stakes**
Pi, OpenCode, and CodeWhale all support multiple LLM backends. Qwen Code is adding provider differentiation (id+baseUrl). Users increasingly expect to "bring their own model" and switch providers without losing tool features (reasoning, tool calls, sub-agents). This is a competitive differentiator against single-provider tools like Claude Code and Copilot CLI.

**2. Agentic Autonomy Demands Guardrails**
Unbounded recursion (#68110 in Claude Code), doom loops (#12716 in OpenCode), and false success reports (#22323 in Gemini CLI) show that agentic tools need **depth limits, early exit detection, and recovery callbacks**. The industry is learning that "agentic" without safety nets is dangerous (and expensive).

**3. Windows Parity Remains Unsolved**
Every tool except Copilot CLI has significant Windows-specific issues (sandbox, UAC, EFS, installer failures, keyboard layouts). This is the #1 platform friction point. Teams investing in robust Windows support (path abstraction, cross-OS testing) will capture the underserved enterprise Windows developer market.

**4. Token Awareness Is No Longer Optional**
Users are demanding **configurable system prompts** (Copilot CLI #2627), **excludeFromContext** flags (Pi #5654), **token usage dashboards** (Qwen Code #5066), and **alerting on token burnout** (Claude Code #67609). Tools that fail to give users control over context consumption will lose power users to those that do.

**5. Declarative Agent Definitions Win**
The push for Markdown+YAML agent definitions (Qwen Code), `.github/prompts/` (Copilot CLI), SKILL.md frontmatter (Gemini CLI), and JSON decision contracts (CodeWhale) reflects a shift from imperative to declarative configuration. Developers want to version-control agent behavior, not just prompts.

**6. Cost Transparency Is a Trust Issue**
Kimi Code's billing opacity (#1994, 7👍) and Qwen Code's OAuth reduction backlash (#3203, 127 comments) demonstrate that **unexpected cost behavior erodes trust fast**. The industry needs standardized token accounting, burn-rate estimates, and tier bridging (e.g., Claude Code's "Max 20x" demand).

**7. Security Audits Are Becoming Standard Practice**
OpenCode's comprehensive security audit (#32134, 17 findings across 2,561 files) and CodeWhale's JSON decision contracts for hooks (#3049) indicate growing maturity in security-aware tooling. Expect more tools to publish security postures as enterprise adoption scales.

---

**Summary for Decision-Makers:** If you need stability today, watch Claude Code's Fable-5 situation closely and test Copilot CLI's new YOLO mode. If you prioritize multi-provider flexibility and active development, Pi and OpenCode are strong bets—but expect Windows friction. OpenAI Codex is moving fastest but at the cost of reliability. The industry is converging on **agentic guardrails, cross-platform support, and cost transparency** as the next competitive frontier.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-13 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

### #1: `skill-creator` Bugfix Cluster — `run_eval.py` 0% Recall Crisis
**PR #1298** (MartinCajiao) — The most critical active PR in the repository, addressing a systemic bug where `run_eval.py` reports `recall=0%` for every skill description. Root causes include the evaluation artifact not being installed as a real skill, Windows stream reading failures, broken trigger detection, and parallel worker issues. This bug has been independently reproduced 10+ times (Issues #556, #1169). The PR represents a comprehensive fix that unblocks the entire description-optimization pipeline.
- **Status:** Open, last updated 2026-06-11
- **Link:** [#1298](https://github.com/anthropics/skills/pull/1298)

### #2: `testing-patterns` — Comprehensive Test Generation Skill
**PR #723** (4444J99) — A full-stack testing skill covering the Testing Trophy model, AAA pattern, React component testing with Testing Library, and guidance on what *not* to test. Addresses a clear community gap: the original skills collection lacked structured testing expertise.
- **Status:** Open, last updated 2026-04-21
- **Link:** [#723](https://github.com/anthropics/skills/pull/723)

### #3: `color-expert` — Color Systems & Space Expertise
**PR #1302** (meodai) — A self-contained color expertise skill covering ISCC-NBS, Munsell, XKCD, RAL, CSS named colors, and color space selection tables (OKLCH for scales, OKLAB for gradients, CAM16 for perception). Notable for its author's broad color standards knowledge.
- **Status:** Open, last updated 2026-06-12
- **Link:** [#1302](https://github.com/anthropics/skills/pull/1302)

### #4: `agent-creator` — Meta-Skill for Task-Specific Agent Sets
**PR #1140** (SyedaQurratAI) — Introduces a meta-skill for creating agent sets for specific tasks, along with critical fixes to `evaluation.py` for parallel tool calls and Windows `recalc.py` support. Directly addresses Issue #1120.
- **Status:** Open, last updated 2026-06-02
- **Link:** [#1140](https://github.com/anthropics/skills/pull/1140)

### #5: `n8n-builder` & `n8n-debugger` — Workflow Automation Skills
**PR #190** (Wolfe-Jam) — Four production-tested community skills including `n8n-builder` (workflow construction) and `n8n-debugger` (troubleshooting, error recovery, webhook debugging). The N8N automation tooling has been a sustained community focus.
- **Status:** Open, last updated 2026-05-18
- **Link:** [#190](https://github.com/anthropics/skills/pull/190)

### #6: `frontend-design` Clarity Overhaul
**PR #210** (justinwetch) — A substantial revision of the existing `frontend-design` skill to improve actionability, coherence, and single-conversation usability. Focuses on ensuring every instruction produces executable Claude behavior.
- **Status:** Open, last updated 2026-03-07
- **Link:** [#210](https://github.com/anthropics/skills/pull/210)

### #7: `document-typography` — Quality Control for Generated Documents
**PR #514** (PGTBoos) — Targets orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point: every document Claude generates risks typographic defects that users rarely request fixing.
- **Status:** Open, last updated 2026-03-13
- **Link:** [#514](https://github.com/anthropics/skills/pull/514)

---

## 2. Community Demand Trends

### Most Pressing: `skill-creator` Reliability (Issues #556, #1169, #1061)
The dominant theme across Issues is the broken `run_eval.py`/`run_loop.py` optimization pipeline. **12 comments and 7 👍** on Issue #556 confirm this is the community's single biggest blocker — skill creators cannot validate their descriptions, rendering the entire skill development workflow non-functional on Windows and producing false negatives on all platforms.

### Enterprise & Org Sharing (Issue #228)
**14 comments, 7 👍** — The most-commented Issue overall. Users want org-wide skill libraries and direct sharing links, not manual `.skill` file Slack sharing. This indicates skills are moving from individual experimentation to team-scale deployment.

### Security & Trust Boundary (Issue #492)
**7 comments** — Community skills distributed under the `anthropic/` namespace create a trust vulnerability. Users may grant elevated permissions to unofficial skills. The community is demanding clear provenance and namespace separation.

### Duplicate Skill Content (Issue #189)
**6 comments, 8 👍** — `document-skills` and `example-skills` plugins contain identical content, causing context window waste. Users want clear separation between skill categories.

### Agent Governance & Safety Patterns (Issue #412)
A proposal for policy enforcement, threat detection, and audit trails for AI agent systems — a gap in the current collection's enterprise security coverage.

### MCP / Skills Convergence (Issue #16)
An early, prescient request to expose Skills as MCP tools, creating a unified API surface for AI-software interaction.

---

## 3. High-Potential Pending Skills

These active PRs show sustained or recent comment activity and are likely to land soon:

| Skill | PR | Author | Last Updated | Key Signal |
|---|---|---|---|---|
| `skill-creator` complete overhaul | [#1298](https://github.com/anthropics/skills/pull/1298) | MartinCajiao | 2026-06-11 | Fixes the 0%-recall crisis; addresses 3 root causes |
| Windows compatibility fixes | [#1050](https://github.com/anthropics/skills/pull/1050) | gstreet-ops | 2026-05-24 | PATHEXT + cp1252 encoding; 1-line fixes |
| Windows subprocess fix | [#1099](https://github.com/anthropics/skills/pull/1099) | joshuawowk | 2026-05-24 | Fixes silent `[WinError 10038]` crashes |
| `agent-creator` + multi-tool eval | [#1140](https://github.com/anthropics/skills/pull/1140) | SyedaQurratAI | 2026-06-02 | Addresses #1120; includes Windows fix |
| `color-expert` | [#1302](https://github.com/anthropics/skills/pull/1302) | meodai | 2026-06-12 | Very recent; strong domain coverage |
| DOCX tracked-change collision fix | [#541](https://github.com/anthropics/skills/pull/541) | Lubrsy706 | 2026-04-16 | Prevents document corruption on `w:id` collisions |
| YAML special-character detection | [#361](https://github.com/anthropics/skills/pull/361) | Mr-Neutr0n | 2026-06-10 | Prevents silent YAML parse failures in descriptions |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliable tooling that supports itself* — fixing the skill-creator evaluation pipeline dominates activity, followed by automation skills (N8N, agents) and document quality assurance, revealing a two-tier ecosystem where meta-tooling reliability is the prerequisite for all downstream skill innovation.**

---

# Claude Code Community Digest — 2026-06-13

## Today's Highlights

Two minor patch releases shipped, including session-language support and a new `footerLinksRegexes` setting. The community is abuzz with **widespread reports of `claude-fable-5` model access being lost mid-session**, triggering dozens of bug tickets within hours. The only PR merged today fixes an issue triage bot flaw that auto-closed issues despite human activity.

## Releases

Two updates were published in the last 24 hours:

- **[v2.1.177](https://github.com/anthropics/claude-code/releases/tag/v2.1.177)** – No changelog attached.
- **[v2.1.176](https://github.com/anthropics/claude-code/releases/tag/v2.1.176)** – Session titles now use the language of the conversation (can be pinned via `language` setting). Added `footerLinksRegexes` for regex‑matched link badges in the footer. Improved Bedrock credential handling.
- **[v2.1.175](https://github.com/anthropics/claude-code/releases/tag/v2.1.175)** (previous) – Added `enforceAvailableModels` managed setting to constrain the Default model and prevent widening by user/project settings.

## Hot Issues

*(10 noteworthy issues from the last 24 hours, ordered by relevance and community reaction)*

1. **[#68129 – [BUG] Fable is not available](https://github.com/anthropics/claude-code/issues/68129)** – Fresh report of `claude-fable-5` being inaccessible. 9 comments, high duplication. Likely a broader outage or access policy change.

2. **[#68126 – Anthropic API Error: Invalid or Inaccessible Model Configuration](https://github.com/anthropics/claude-code/issues/68126)** – Mid‑session model rejection on macOS. User reports error with `claude-fable-5`. 8 comments.

3. **[#68131 – Model access lost without changes: claude-fable-5 unavailable on max plan](https://github.com/anthropics/claude-code/issues/68131)** – User on Max plan lost access to Fable‑5 after a trial, still had tokens. 5 comments, closed as duplicate but indicates confusion.

4. **[#68128 – “There's an issue with the selected model (claude-fable-5)”](https://github.com/anthropics/claude-code/issues/68128)** – Short, heavily upvoted (👍8). Symptom of the same access problem.

5. **[#68121 – Duplicate: Anthropic API Error for claude-fable-5](https://github.com/anthropics/claude-code/issues/68121)** – Another instance on macOS with iTerm. 5 comments.

6. **[#68110 – General-purpose sub-agents recursively spawn unbounded child agents](https://github.com/anthropics/claude-code/issues/68110)** – Critical usability bug: sub‑agents can spawn new `Agent` calls, causing exponential token burn. No depth limit. 2 comments, but high impact for agentic workflows.

7. **[#67609 – Advisor tool returns “unavailable” on claude-fable-5 above ~100K tokens](https://github.com/anthropics/claude-code/issues/67609)** – Server‑side advisor tool fails on Fable‑5 when transcript exceeds ~100K tokens. 2 comments, 👍6. Important for long sessions.

8. **[#14321 – Enable extended thinking for subagents](https://github.com/anthropics/claude-code/issues/14321)** – Feature request with 👍25. Sub‑agents cannot use extended thinking, limiting complex multi‑step tasks.

9. **[#49917 – Windows installer fails with AddPackage HRESULT 0x80073CF6](https://github.com/anthropics/claude-code/issues/49917)** – Long‑standing bug (since Apr) with inconsistent package state after failed install. 26 comments, 👍6.

10. **[#56913 – Make autonomous Claude Code viable: tiered Opus brains + Sonnet workers + persistent state](https://github.com/anthropics/claude-code/issues/56913)** – High‑engagement feature request (26 comments) proposing a multi‑model architecture for persistent, long‑running autonomous agents.

## Key PR Progress

Only one pull request was updated in the last 24 hours:

- **[#26360 – Fix issues being auto-closed despite human activity](https://github.com/anthropics/claude-code/pull/26360)** (closed) – Author: chrislloyd. Addresses a triage bot bug where issues with `stale`/`autoclose` labels were closed even after human comments. Fix adds label‑removal logic and updates the `closeExpired()` function in the sweep workflow. Merged after 4 months in review.

No other PRs were active; this PR represents the sole code change beyond the releases.

## Feature Request Trends

The most‑requested feature directions from recent issues:

- **Autonomous multi‑agent orchestrators** – Users want Claude Code to act as a persistent “brain” with tiered models (Opus for reasoning, Sonnet for workers) and durable state (#56913, #14321). Demand for extended thinking in sub‑agents is a recurring ask (👍25).
- **Better cost/plan tiers** – Power users need a “Max 20x” equivalent on Team plans (#47509, 👍37). Many feel the current Premium tier (6.25x) is insufficient for heavy CLI usage.
- **Consistent model access controls** – Requests for clearer documentation and enforcement of `availableModels` per environment (#31353, #32682). The Fable‑5 outage today underscores this need.
- **Durable scheduled tasks** – Users want `CronCreate` with `durable:true` to actually persist across sessions (#50911).
- **Documentation gaps** – Multiple issues (8 total) highlight missing or outdated docs for Agent SDK tools, permissions, remote control session archiving, and plugin discovery.

## Developer Pain Points

Recurring frustrations and high‑frequency requests from the last 24 hours:

- **Fable‑5 model access instability** – At least 7 distinct issues opened today (#68129, #68126, #68131, #68128, #68121, #68120, #68122) describing sudden loss of `claude-fable-5` mid‑session. Users on Max plan feel misled. Some report being silently downgraded to Opus with vague “content policy” reasons. Community reaction: frustration and confusion, with many duplicates.
- **Unbounded agent recursion** – The `Agent` tool allows sub‑agents to spawn more agents without depth limits, leading to massive token burn (#68110). Urgent fix needed.
- **Windows installation fragility** – The `AddPackage` error (0x80073CF6) persists (#49917), and `.mcpb` silent hangs on Windows (#67865) block local plugin development.
- **Invalid Unicode in Bash output** – Issue #16294 (16 comments) remains open since January; API errors from non‑surrogate‑pair characters in terminal output plague users.
- **Worktree naming surprises** – `claude --worktree` silently prepends “worktree-“ and checks out origin/default instead of parent HEAD (#62309), breaking multi‑session conventions.
- **Background token consumption** – Reports of session usage increasing without active prompts (#67587), indicating possible background polling or heartbeat issues.

— *Generated from GitHub data for 2026-06-13.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-13

## Today's Highlights
Four new Rust alpha versions (v0.140.0-alpha.14 through .17) were released, continuing rapid iteration on the CLI. The community is heavily focused on Windows sandbox reliability, with a cluster of issues around `spawn setup refresh` failures and UAC elevation errors. Meanwhile, several PRs are laying groundwork for cross-OS path handling (PathUri) and unified execution environments, signalling a push toward better heterogeneous platform support.

## Releases
Four alpha releases of the Rust-based CLI were pushed in the last 24 hours:
- **rust-v0.140.0-alpha.14** – no changelog provided
- **rust-v0.140.0-alpha.15** – no changelog provided
- **rust-v0.140.0-alpha.16** – no changelog provided
- **rust-v0.140.0-alpha.17** – no changelog provided

No new stable or app releases are mentioned.

## Hot Issues
1. **#12564** – [CLOSED] [enhancement] Allow renaming task/thread titles for history navigation  
   *Author: dirshaye* – 79 comments, 111 👍 – The most upvoted issue, requesting a basic UX improvement. Closed but widely requested.  
   https://github.com/openai/codex/issues/12564

2. **#24391** – [CLOSED] [bug] Windows sandbox: `spawn setup refresh` fails on Codex CLI 0.133.0  
   *Author: Lyellr88* – 46 comments, 26 👍 – Core Windows regression; many users forced to roll back to 0.132.0.  
   https://github.com/openai/codex/issues/24391

3. **#9046** – [OPEN] [bug] Context window exhaustion message on fresh threads  
   *Author: swoiow* – 25 comments – Users hit context limits even with single queries. Remains open.  
   https://github.com/openai/codex/issues/9046

4. **#22423** – [OPEN] [bug] Unable to locate Codex CLI binary; `CODEX_CLI_PATH` or Electron resource issue  
   *Author: Adaozuishuai* – 20 comments – Affects app users after WSL configuration.  
   https://github.com/openai/codex/issues/22423

5. **#25243** – [OPEN] [bug] macOS Codex relaunch loop exhausts `syspolicyd` file descriptors, blocking app launches  
   *Author: guidedways* – 20 comments, 2 👍 – macOS-specific crash that prevents the app from starting.  
   https://github.com/openai/codex/issues/25243

6. **#24098** – [CLOSED] [bug] Windows elevated sandbox fails with `spawn setup refresh` after CLI update  
   *Author: JoeGideon1979* – 18 comments, 6 👍 – Duplicate of #24391 but adds model version details.  
   https://github.com/openai/codex/issues/24098

7. **#25220** – [OPEN] [bug] Windows bundled plugins (Computer Use, Browser, Chrome, LaTeX) unavailable due to EFS-encrypted WindowsApps files  
   *Author: lumingfei334-create* – 16 comments, 3 👍 – Store-installed app cannot copy plugin binaries to encrypted directories.  
   https://github.com/openai/codex/issues/25220

8. **#27175** – [OPEN] [bug] Codex Desktop Windows 26.602.71036 crashes after update even with empty sessions  
   *Author: SocialK* – 15 comments, 3 👍 – Pro subscriber reports total inaccessibility after automatic update.  
   https://github.com/openai/codex/issues/27175

9. **#27817** – [OPEN] [bug] False positive cybersecurity flag on authorized finance/tax filing work  
   *Author: jyongchul* – 12 comments – Safety checks incorrectly flag normal tax readiness conversations.  
   https://github.com/openai/codex/issues/27817

10. **#27979** – [OPEN] [bug] Windows Codex App 26.609.4994.0 no longer opens after June 12 update  
    *Author: SocialK* – 7 comments – Another update breakage affecting Pro subscribers.  
    https://github.com/openai/codex/issues/27979

## Key PR Progress
1. **#28012** – [OPEN] Add fail-closed plugin script resolver  
   *Author: kmbroai* – Parses and validates plugin script commands with trusted path canonicalization.  
   https://github.com/openai/codex/pull/28012

2. **#27459** – [CLOSED] Gate plugin MCP servers by auth route  
   *Author: felixxia-oai* – Moves auth-aware surface projection into `PluginsManager` for consistent effective plugin views.  
   https://github.com/openai/codex/pull/27459

3. **#28014** – [OPEN] unified-exec: launch remote commands without host sandbox  
   *Author: anp-oai* – Launches remote commands directly via `exec-server`, skipping host sandbox construction.  
   https://github.com/openai/codex/pull/28014

4. **#28002** – [OPEN] [codex] Send turn state through compact requests  
   *Author: aibrahim-oai* – Inline compaction now includes turn state in `/responses/compact` requests for consistency.  
   https://github.com/openai/codex/pull/28002

5. **#27819** – [OPEN] path-uri: render native paths across platforms  
   *Author: anp-oai* – Introduces `PathUri` to avoid exposing URI encoding to public APIs, essential for cross-OS exec-server.  
   https://github.com/openai/codex/pull/27819

6. **#27996** – [OPEN] [codex] Send request-scoped turn state over WebSocket  
   *Author: aibrahim-oai* – Replaces connection-scoped upgrade headers with per-request turn state in WebSocket messages.  
   https://github.com/openai/codex/pull/27996

7. **#28006** – [OPEN] core: retain executor environment identity  
   *Author: anp-oai* – Preserves cwd, shell, and path convention across resume/fork for multi-OS orchestration.  
   https://github.com/openai/codex/pull/28006

8. **#28011** – [OPEN] unified-exec: resolve shell and workdir for target  
   *Author: anp-oai* – Resolves command paths using the selected environment’s conventions rather than app-server host syntax.  
   https://github.com/openai/codex/pull/28011

9. **#27989** – [OPEN] path-uri: parse and resolve paths by explicit convention  
   *Author: anp-oai* – Adds `NativePathString` deserialization with POSIX, Windows drive, UNC, and root-relative support.  
   https://github.com/openai/codex/pull/27989

10. **#27713** – [OPEN] [do not merge, prototype] Prototype multi-provider workload identity authentication  
    *Author: cooper-oai* – Replaces Azure-only authentication with a multi-provider system; marked as prototype.  
    https://github.com/openai/codex/pull/27713

## Feature Request Trends
- **Thread management**: The most upvoted request (#12564) asks for renaming task/thread titles to improve history navigation. This reflects a broader desire for better organisation in long-running sessions.
- **Context window improvements**: Issue #9046 and several others highlight the need for smarter context compression or clearer indicators when the model is about to run out of room.
- **Plugin MCP reliability**: Multiple open issues request stable plugin loading on Windows, especially for Computer Use, Browser, and Chrome plugins. Users want these to survive app restarts and sandbox refreshes.
- **Cross-OS execution**: The flood of PRs around `PathUri` and `unified-exec` indicates a strong push to let users seamlessly work across Windows, macOS, and Linux without path mangling.
- **Telemetry and observability**: PRs #28008 and #28009 add import progress accounting and telemetry for external agent imports, hinting at growing demand for transparent import workflows.

## Developer Pain Points
- **Windows sandbox instability**: The single biggest pain point – multiple layered issues (UAC elevation, os error 740, EFS encryption, `spawn setup refresh`) prevent basic features like `node_repl`, Computer Use, and in-app browser from working.
- **Update breaks**: Frequent regressions after app updates (#27175, #27979, #25243 on macOS) force users to roll back or lose functionality. The community is frustrated with the lack of stable release channels.
- **False positive safety flags**: Security checks incorrectly flag legitimate financial/tax work (#27817), disrupting productivity and eroding trust in automated moderation.
- **CLI binary discovery**: Both app and CLI users encounter `Unable to locate Codex CLI binary` errors (#22423, #16408), often after switching to WSL or installing from the Microsoft Store.
- **Context window limits without recovery**: Users hitting “ran out of room” even on fresh threads (#9046) without clear guidance on how to proceed.

---

*Generated from GitHub data for openai/codex on 2026-06-13. Digest curated for technical developers.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-13

## Today’s Highlights
A fresh nightly release (`v0.48.0-nightly.20260613`) lands with an atomic MCP tool discovery fix and a Vertex AI model mapping correction. Agent reliability remains the top concern: the generalist hang bug (#21409) still affects users, and a security PR series closed today addresses Gateway authentication and credential caching issues. The community also sees progress on long-standing terminal quirks (tmux background detection, vim `cc` behaviour, shell history corruption).

---

## Releases
**v0.48.0-nightly.20260613.g9e5599c32**  
[View release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-nightly.20260613.g9e5599c32)

What’s changed:
- `fix(core): implement atomic update in MCP tool discovery` by @luisfelipe-alt
- `Vertex ai model mapping fix` by @DavidAPierce
- Added documentation and migration command

---

## Hot Issues
*(10 noteworthy issues, ordered by comment count)*

1. **#21409 – Generalist agent hangs**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21409) | 👍 8 | 7 comments  
   The agent hangs forever when deferring to the generalist agent. Instructing the model not to use sub-agents works around it. High community frustration (8 thumbs-up) – ongoing since March.

2. **#22323 – Subagent recovery after MAX_TURNS reported as GOAL success**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22323) | 👍 2 | 6 comments  
   A subagent that hits its turn limit reports `status: "success"` and `Termination Reason: "GOAL"`, masking the interruption. This undermines trust in agent results.

3. **#25166 – Shell command execution stuck after completion**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/25166) | 👍 3 | 4 comments  
   Simple shell commands (e.g., `ls`) show “Awaiting user input” even after finishing. Users report this repeatedly.

4. **#21983 – Browser subagent fails on Wayland**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21983) | 👍 1 | 4 comments  
   The browser subagent terminates with “GOAL” but fails without meaningful work. Wayland-specific – affects Linux users.

5. **#24353 – Robust component level evaluations (EPIC)**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24353) | 7 comments  
   Follow-up to introduce systematic component-level behavioural evals. Currently 76 eval tests exist; the epic aims to scale and formalise them.

6. **#22745 – AST-aware file reads, search, and mapping (EPIC)**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22745) | 👍 1 | 7 comments  
   Investigating whether AST-aware tools can improve precision of file reads, reduce turns, and cut token noise. Highly strategic for agent code understanding.

7. **#26525 – Add deterministic redaction and reduce Auto Memory logging**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26525) | 5 comments  
   Auto Memory sends transcripts to the model before redaction – a security gap. Requests deterministic pre-redaction and less logging.

8. **#26522 – Stop Auto Memory from retrying low-signal sessions indefinitely**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26522) | 5 comments  
   Sessions that the extraction agent skips (low signal) remain unprocessed forever, causing infinite retries. Needs a processed flag or TTL.

9. **#20003 – Gemini CLI Companion not working in Theia IDE**  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/20003) | 👍 1 | 5 comments  
   The `/ide` integration detection fails in Theia, breaking the companion extension. Community workaround unclear.

10. **#21968 – Gemini does not use skills and sub-agents enough**  
    [Issue](https://github.com/google-gemini/gemini-cli/issues/21968) | 6 comments  
    Anecdotal but consistent: custom skills and sub-agents are rarely invoked even when the task matches their descriptions. Affects the value of the agent platform.

---

## Key PR Progress
*(10 PRs closed or open with high relevance)*

1. **#27572 – fix(cli): handle tmux false positive background detection**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27572)  
   Fixes incorrect light-background detection when running inside tmux + mosh, which caused unwanted theme switching and compatibility warnings.

2. **#27553 – fix(cli): add GATEWAY auth type to validateAuthMethod**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27553)  
   Security fix – Gateway authentication was rejected when `GOOGLE_GEMINI_BASE_URL` was set. Now properly supported.

3. **#27555 – fix(cli): stop merging shell history commands ending in backslash**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27555)  
   Shell history corrupted Windows paths (e.g., `dir C:\`). Now correctly preserves backslash-terminated lines.

4. **#27552 – fix(core): insert content literally into LLM prompts to avoid $ substitution**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27552)  
   Critical bug – `String.replace` special patterns caused `$` in values to be silently corrupted before reaching the model. Now uses literal insertion.

5. **#27568 – fix(core): fall back when ripgrep execution fails**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27568)  
   Gracefully falls back to legacy `GrepTool` when `rg` is missing or exits with code 64, improving compatibility.

6. **#27870 – fix(core): cap pending tool responses**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27870)  
   Designed to prevent crashes or hangs when a tool returns a very large result. Important for agent stability.

7. **#27873 – fix(core): improve SKILL.md frontmatter parsing robustness**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27873)  
   Adds BOM support, trims trailing whitespace, normalises non-string YAML values. Resolves issue #25693.

8. **#27872 – fix(core): strip line/range suffix from at-command paths**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27872)  
   Prevents CLI hangs when users type `@file:12` or similar. Also improves `/clear` command documentation.

9. **#27871 – fix(core): merge existing refresh token when caching credentials**  
   [PR](https://github.com/google-gemini/gemini-cli/pull/27871)  
   Fixes issue #21691 where credential caching would overwrite the stored refresh token instead of merging.

10. **#27467 – fix(core): handle multi-line escaped quotes in stripShellWrapper**  
    [PR](https://github.com/google-gemini/gemini-cli/pull/27467)  
    Replaces manual parsing with `shell-quote` to correctly handle escaped quotes across multiple lines (e.g., `bash -c "hg commit -m \"title\n\nbody\""`).

---

## Feature Request Trends
The most requested directions from recent issues and epics:

- **AST-aware code understanding** – Several epics (#22745, #22746) call for AST-based file reads, search, and codebase mapping to reduce token waste and improve precision.
- **Agent self-awareness and autonomy** – Users want the agent to know its own capabilities, hotkeys, and CLI flags (#21432), and to proactively use custom skills and sub-agents (#21968).
- **Robust evaluation framework** – The push for component-level evaluations (#24353) and stabilised internal project evals (#23166) shows a need for systematic quality metrics.
- **Better memory system control** – Issues around Auto Memory (#26525, #26522, #26523) demand redaction before model exposure, deterministic session processing, and patch validation.
- **IDE and terminal integration** – Support for Theia (#20003), better terminal resize behaviour (#21924), and external editor handling (#24935) are recurring themes.

---

## Developer Pain Points
Recurring frustrations expressed by the community:

- **Agent hangs and silent failures** – The generalist agent hangs indefinitely (#21409), subagents report false success (#22323), and shell commands remain stuck in “waiting” state (#25166).
- **Configuration ignored** – Browser agent ignores `settings.json` overrides (#22267), and subagents run even when disabled (#22093).
- **Tool and skill underutilisation** – The model often fails to use custom skills or sub-agents even for well-described tasks (#21968).
- **Destructive behaviour** – The agent occasionally uses `git reset --force` or writes temp scripts in random directories (#22672, #23571).
- **Terminal quirks** – Vim `cc` behaves incorrectly (#27554), shell history gets corrupted (#27555), and terminal resize causes flicker (#21924).
- **Security and credential issues** – Auto Memory leaks content before redaction (#26525), Gateway authentication was broken (#27553), and credential caching overwrites refresh tokens (#27871).
- **Scalability limits** – More than 128 tools cause a 400 error (#24246), and large tool results can crash the agent (#27870).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-13

## Today’s Highlights

Copilot CLI **v1.0.62-1** shipped today with a long-awaited **YOLO/allow-all indicator** and server-side search for Issues/PR tabs. The community remains vocal: the most-reacted open issue (#53) has now spawned community forks like `shell-ai`, while **terminal rendering corruption** and **keyboard input bugs** (German/Polish layouts) continue to dominate new bug reports. A critical **panic on Linux ARM64** (#3784) appeared within hours of the release.

---

## Releases

### v1.0.62-1
[View release](https://github.com/github/copilot-cli/releases/tag/v1.0.62-1)

**Added**
- Show **YOLO (allow all) indicator** in footer, plus `allow-all` state for custom `statusLine.command`
- Press `/` on Issues or Pull Requests tab to **GitHub server-side filtering**
- **Session-scoped extensions and canvases** — enables per-session isolation for plugins
- Allow SDK clients to **configure session memory thresholds**

*Note: No bug fixes or performance improvements were called out in this release.*

---

## Hot Issues (10 noteworthy)

These issues are selected for community impact, recency, or both.

### #53 — [OPEN] Bring back Copilot CLI commands (community fork ecosystem)
**Comments:** 37 | **👍:** 75  
**URL:** [Issue #53](https://github.com/github/copilot-cli/issues/53)  
**Why it matters:** After six months of silence from GitHub on this top-voted issue, the community started building alternative CLI clients. The leading fork `shell-ai` by @Deltik is gaining traction. This signals deep dissatisfaction with the CLI's direction or stability.

### #618 — [CLOSED] Custom slash commands from `.github/prompts/`
**Comments:** 31 | **👍:** 99  
**URL:** [Issue #618](https://github.com/github/copilot-cli/issues/618)  
**Why it matters:** The most-upvoted feature request of all. Users want per-repo prompt files (like VS Code's `.github/prompts/`). It was closed — likely implemented or declined. Community will want to know the outcome.

### #1481 — [CLOSED] SHIFT+ENTER should insert line break, not execute
**Comments:** 26 | **👍:** 15  
**URL:** [Issue #1481](https://github.com/github/copilot-cli/issues/1481)  
**Why it matters:** A fundamental UX mismatch; most chat apps use Shift+Enter for newline, Ctrl+Enter for send. The bug was closed — presumably fixed. Many users were annoyed.

### #3749 — [OPEN] Terminal streaming renderer corrupts output (doubled/truncated)
**Comments:** 5 | **👍:** 7  
**URL:** [Issue #3749](https://github.com/github/copilot-cli/issues/3749)  
**Why it matters:** Reports of `copilot` streaming garbage characters (doubled words, truncated tokens). Multiple similar reports (#3755, #3769, #3780). Underlying renderer issue is creating a terrible user experience.

### #3755 — [OPEN] Reasoning display garbles text with duplicated overlapping chunks
**Comments:** 5 | **👍:** 2  
**URL:** [Issue #3755](https://github.com/github/copilot-cli/issues/3755)  
**Why it matters:** Same class as #3749 but specific to the `showReasoning: true` phase. Reasoning output becomes unreadable — undermines trust in the tool.

### #1999 — [OPEN] Cannot type `@` on German keyboard (AltGr+q)
**Comments:** 9 | **👍:** 1  
**URL:** [Issue #1999](https://github.com/github/copilot-cli/issues/1999)  
**Why it matters:** Core input bug affecting non‑US layouts. `@` is critical for agents, slash commands, etc. Also affects `#` and other AltGr characters. Similar to #2920 (Polish).

### #2306 — [OPEN] “Not authorized” error intermittently for enterprise users
**Comments:** 6 | **👍:** 3  
**URL:** [Issue #2306](https://github.com/github/copilot-cli/issues/2306)  
**Why it matters:** Enterprise customers see auth failures 2–3 times per week, then they disappear. No progress from GitHub — blocks productivity and erodes trust in Copilot for business use.

### #3784 — [OPEN] v1.0.62-1 panics on Linux ARM64 (Tokio reactor)
**Comments:** 1 | **👍:** 0  
**URL:** [Issue #3784](https://github.com/github/copilot-cli/issues/3784)  
**Why it matters:** Brand new crash after today's release. The CLI aborts before completing the first message. Critical for ARM64 users (e.g., Raspberry Pi, Apple Silicon via Docker).

### #2627 — [OPEN] Configurable system prompt to reduce fixed token overhead
**Comments:** 2 | **👍:** 17  
**URL:** [Issue #2627](https://github.com/github/copilot-cli/issues/2627)  
**Why it matters:** Users are frustrated that ~20,500 tokens (10% of 200K context) are consumed by instructions they may not need. Coupled with large tool definitions, it limits effective context window. High demand for customization.

### #3782 — [OPEN] MCP stdio server respawns in unbounded tight loop (1.0.61+)
**Comments:** 0 | **👍:** 0  
**URL:** [Issue #3782](https://github.com/github/copilot-cli/issues/3782)  
**Why it matters:** Possibly a regression. MCP stdio servers are spawned hundreds of times per minute with no backoff. Could cause system resource exhaustion. No workaround yet.

---

## Key PR Progress

Only **one pull request** was updated in the last 24 hours.

### #3771 — Initial project setup
**Status:** OPEN | **Updated:** 2026-06-12  
**URL:** [PR #3771](https://github.com/github/copilot-cli/pull/3771)  
**Description:** No details provided. Appears to be a scaffold or infrastructure PR (e.g., documentation, CI). Not a feature or fix. Activity is low — this may signal a quiet development cycle.

---

## Feature Request Trends

The community is pushing for **customization, better MCP control, and observability**. Top directions from today’s issues:

1. **Custom slash commands / per‑repo prompts** (#618, closed, but clearly a top want)
2. **Configurable system prompt** to reduce token overhead (#2627, 17 👍)
3. **Long‑running goals via `.copilot/goals.md`** (#3364) — cross‑session persistence
4. **Auto‑update plugins** from marketplace (#3331)
5. **Keyboard shortcut for session picker** (#3779)
6. **Enable/disable MCP servers from UI** (#3564)
7. **OpenTelemetry cost metrics** (#3778) — parity with Claude Code’s billing tracking

**Theme:** Users want *more control, less overhead, and better integration with existing workflows.*

---

## Developer Pain Points

Recurring frustrations that are damaging user trust:

- **Terminal rendering corruption** — multiple open issues (#3749, #3755, #3769, #3780, #982) describe garbled, repeated, or truncated streaming output. The “thinking” phase is particularly broken. A core rendering bug.
- **Keyboard input bugs** — German (#1999), Polish (#2920), and Shift+Enter (#1481) problems remain unsolved for many. Makes CLI unusable for non‑US layouts.
- **Intermittent authentication failures** (#2306) — enterprise users hit weekly auth walls with no clear cause.
- **Platform instability** — Linux ARM64 panic in latest release (#3784), Windows MCP fetch failures (#3455), scroll‑bar misalignment (#3501).
- **Session hangs and compaction loops** — 8‑minute freezes (#1614), infinite compaction with large instruction files (#3621).
- **MCP server abuse** — no backoff on stdio server respawn (#3782), no policy to disable third‑party MCP (#3756).

**Bottom line:** The CLI is powerful when it works, but reliability and input handling are holding it back.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区摘要 - 2026-06-13

## 今日亮点

今日Kimi Code CLI无新版本发布。社区主要聚焦于国内用户长期反馈的**kimiCode用量计算不透明**及**底层核心模型（如K2.6）Token消耗过高**的问题，同时，Work标签页的**WebSocket连接故障**也引起了新关注。一项针对Python 3.13兼容性的关键PR仍在推进中。

## 发布

暂无新版本发布。

## 热点问题

由于数据仅包含3个问题，已全部列出并分析。

1.  **[#640] [bug] Kimi CLI stuck in reading one file again and again and stuck in a loop** - *问题*：使用自定义Anthropic端点（模型：mimo-v2-flash）时，Kimi CLI陷入反复读取同一文件的死循环。 *影响*：严重影响开发效率，导致工具完全无法使用。 *社区反应*：该问题已存在近5个月，评论8条，但未见官方明确回复或修复计划，令用户担忧。 [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/640)

2.  **[#1994] kimiCode用量计算有问题 || There is a problem with kimiCode usage calculation** - *问题*：用户反映订阅2小时的额度，仅完成2个任务就被耗尽。经分析，底层模型（如K2.6）的思维链过长，导致Token消耗远超预期。用户质疑官方宣传的“API请求次数”与实际Token计费模式不符。 *影响*：直接引发用户对计费透明度和产品价值的信任危机。 *社区反应*：获7个👍，评论6条，是近期社区关注度最高的问题之一，中文用户群体反应强烈。 [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/1994)

3.  **[#2435] [Bug] Kimi Work tab: "Daimon control WS not ready" + infinite reload at 99%** - *问题*：在Windows 10/11上，Kimi CLI Web端的Work标签页因WebSocket守护进程初始化失败而完全无法使用，界面显示错误并陷入无限加载循环。 *影响*：核心工作流功能（Work标签页）对部分用户完全不可用。 *社区反应*：新近创建（2026-06-06）且已获1条评论，问题比较严重，但可能仍处于早期确认阶段。 [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2435)

## 关键PR进展

数据仅包含一个PR，已列出分析。

1.  **[#1597] fix: guard trafilatura import to prevent cascading tool load failure on Python 3.13** - *修复*：在Python 3.13环境下，`trafilatura`依赖的`charset-normalizer`库因mypyc编译的`.so`二进制文件不兼容，导致导入失败。此PR通过保护性导入，防止了工具链级联失败。 *价值*：对使用Python 3.13的开发者和部署环境至关重要，确保了工具的向后兼容性。 [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/1597)

## 功能请求趋势

基于现有Issues，当前最核心的功能请求方向不是新增功能，而是**计费模式透明化与优化**。用户强烈要求：
- **明晰API消耗机制**：区分“API请求次数”与“Token消耗”的关系，并在官方文档中明确声明。
- **增加Token消耗预警**：在任务启动时预估并显示可能消耗的Token量。
- **支持更经济的模型**：提供对短思维链、低成本模型的优先支持或开关选项。

## 开发者痛点

1.  **计费模型与宣传不一致**：用户普遍感觉被误导，认为按Token计费的方式导致实际使用成本远高于预期，严重影响了深度使用和付费意愿。
2.  **核心功能稳定性不足**：包括文件处理逻辑错误（#640）和WebSocket服务不可用（#2435）在内的bug，直接阻塞了用户的核心工作流，降低了工具的可靠性。
3.  **问题响应与修复缓慢**：部分关键Bug（如#640）长期存在（近5个月未关闭），社区对其修复时效性存在疑虑。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-13

## Today’s Highlights
No new releases landed in the last 24 hours, but the community continues to surface and fix critical issues. A major permissions bug (#27436) remains a hot topic with users stuck in an approval loop, while a new security audit PR (#32134) maps 17 findings across 2,561 files. On the fix side, PR #32093 introduces native `db doctor`/`repair` commands to address persistent database corruption, and #32128 resolves a stale “working” indicator bug that could leave sessions stuck forever.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **[#27436 – Permission required cannot select](https://github.com/anomalyco/opencode/issues/27436)**  
   A critical UX bug: clicking “Allow once” has no effect, “Allow always” loops endlessly, and “Reject” blocks submission. The session becomes completely stuck. 16 comments, 11 👍.

2. **[#31996 – Invalid JSON Schema Due to Regex Lookaround (GPT 5.5)](https://github.com/anomalyco/opencode/issues/31996)**  
   Closed bug where OpenCode generated unsupported regex lookaround in file key patterns, causing all requests to fail with providers like GPT 5.5. Affects any OpenAI-compatible endpoint. 11 comments.

3. **[#12716 – Doom loop not caught during reasoning/output](https://github.com/anomalyco/opencode/issues/12716)**  
   When an agent is asked to “think about a word 100 times,” OpenCode never detects the infinite loop. The session runs forever with no escape. 9 comments.

4. **[#14187 – Feature: Markdown preview toggle in file viewer](https://github.com/anomalyco/opencode/issues/14187)**  
   Highly requested (22 👍) enhancement to render `.md` and `.mdx` files as rich previews instead of raw markdown in the sidebar viewer.

5. **[#16885 – JSON→SQLite migration reruns on channel‑specific DBs](https://github.com/anomalyco/opencode/issues/16885)**  
   A startup migration runs every launch for non-`latest` channels (e.g., local/dev), causing repeated conversion and potential data loss. 8 comments.

6. **[#16610 – Hang at startup when inotify user instances exhausted](https://github.com/anomalyco/opencode/issues/16610)**  
   On Linux, if `fs.inotify.max_user_instances` is too low, OpenCode hangs completely when opening a repo with a `.git` directory. No graceful fallback. 8 comments, 7 👍.

7. **[#24335 – Permission wildcard “*” overwrites lower rules](https://github.com/anomalyco/opencode/issues/24335)**  
   Contradicts the documented “last matching rule wins” behavior: the catch-all `*` rule incorrectly overrides more specific rules placed after it. 7 comments.

8. **[#31204 – NOT NULL constraint failed on agent-switched sessions](https://github.com/anomalyco/opencode/issues/31204)**  
   After recent June migrations, any session that triggers an agent switch crashes with `session_message.seq NOT NULL constraint failed`. Affects users running latest updates. 6 comments.

9. **[#18108 – Truncated tool calls misclassified as invalid, doom loop](https://github.com/anomalyco/opencode/issues/18108)**  
   When tool call JSON exceeds `maxOutputTokens`, the truncated output is misclassified as an “invalid tool call.” No truncation signal is sent to the model, leading to silent exit or an unrecoverable loop. 6 comments.

10. **[#27302 – Warp mode + interactive Q&A captures all input](https://github.com/anomalyco/opencode/issues/27302)**  
    In warp mode, when the agent triggers `question` tool, mouse clicks and keyboard are fully captured—user can only force-close the terminal. 3 comments, 6 👍.

---

## Key PR Progress

1. **[#32135 – fix(mcp): refresh expired OAuth tokens](https://github.com/anomalyco/opencode/pull/32135)**  
   Prevents MCP server failures when session tokens expire. Fresh merge; no issue linked yet.

2. **[#31529 – fix(plugin): prevent spinner garbage in non-TTY](https://github.com/anomalyco/opencode/pull/31529)**  
   Closes #27908: spinner animation output (◓,◑,◒,◐) now suppressed when running in CI/CD or PowerShell non-interactive mode.

3. **[#32134 – docs: add comprehensive security audit report (17 findings)](https://github.com/anomalyco/opencode/pull/32134)**  
   Adds `SECURITY_AUDIT.md` covering 2,561 TypeScript files. Identifies issues like plaintext credential exposure in logs and permission bypass via symlinks.

4. **[#32128 – fix(app): reconcile session_status in bootstrap so stale busy clears](https://github.com/anomalyco/opencode/pull/32128)**  
   Closes #17657: The “working” indicator that never cleared is now properly reconciled at startup, preventing sessions from appearing stuck forever.

5. **[#21056 – fix(json→sqlite migration on every run)](https://github.com/anomalyco/opencode/pull/21056)**  
   Closes #16885 and #21057: The JSON→SQLite startup migration now correctly detects whether migration is needed on channel-specific databases.

6. **[#32093 – feat: add db doctor and repair commands](https://github.com/anomalyco/opencode/pull/32093)**  
   Brings native CLI tooling to diagnose and repair common SQLite database issues—addresses multiple related bugs (#31204, #19191, etc.).

7. **[#32125 – fix(sdk): normalize scheme-less base URLs](https://github.com/anomalyco/opencode/pull/32125)**  
   Closes #32077: `opencode attach localhost:4096` now correctly applies query parameters; previously failed silently.

8. **[#31993 – fix(app): restore desktop open menu](https://github.com/anomalyco/opencode/pull/31993)**  
   Fixes two regressions in the desktop session header “Open in” control, closing #29875 and #29951.

9. **[#32117 – fix: classify fetch timeouts as retryable](https://github.com/anomalyco/opencode/pull/32117)**  
   Closes #32118 (implied): `DOMException` `TimeoutError` from `AbortSignal.timeout` now triggers retry logic instead of hard failure.

10. **[#32088 – fix(opencode): recover expired MCP sessions](https://github.com/anomalyco/opencode/pull/32088)**  
    Locally patches MCP SDK to re‑initialize sessions after a 404 on streamable HTTP, coalescing concurrent stale‑session requests into a single recovery.

---

## Feature Request Trends

The community is pushing for **better visibility and control** over the tool’s inner workings. Top themes include:
- **Markdown preview** in the file viewer (#14187, 22 👍)
- **Dynamic window titles** showing the active project/session (#31423)
- Live **token throughput** display (#30164)
- **Database health tools** (now addressed by PR #32093)
- **Pricing transparency** for provider markup models (#32116)

Several requests also target **ecosystem discovery** – adding community plugins/projects to official docs (#32112) and integrating an **ads/kickback system** for brand partnerships (#32106).

---

## Developer Pain Points

Recurring frustrations cluster around **permissions and infinite loops**:
- The permission system has multiple inconsistencies: wildcards overriding specific rules (#24335) and `external_directory: "allow"` ignoring `edit: "deny"` (#18441). Some users question if it’s “intentionally broken” (#24429).
- **Doom loops** (infinite retries) plague agent reasoning (#12716), tool calls (#18108), subagent task tools (#17169), and agent‑browser commands (#25938).
- **Startup hangs** due to inotify limits (#16610) and **stale “working” indicators** (#32127) disrupt daily development.
- Windows users face **auto-update directory loss** (#26818) and unavailability of Winget‑based upgrades (#30026).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-13

## Today's Highlights
A busy day across the ecosystem with **v0.79.2 shipping** with improved Bedrock validation error messaging. The **OpenAI Codex connection reliability issue (#4945)** continues to dominate community discussion with 55 comments, pointing to a systemic streaming stability problem. On the PR front, two competing **Anthropic Vertex provider** implementations (#5262, #5679) signal strong community demand for GCP-native Claude access, while the **first-time setup flow (#5587, #5385)** shows the team investing in onboarding UX.

---

## Releases
**v0.79.2** — Patch release with clearer Amazon Bedrock validation guidance: data retention validation errors now link directly to AWS documentation. Minor addition (Ad).  
[View Release](https://github.com/earendil-works/pi/releases/tag/v0.79.2)

---

## Hot Issues

1. **#4945 — OpenAI Codex Connection Reliability** (55 comments, 30 👍)  
   Critical stream stability issue: `openai-codex` / `gpt-5.5` sessions hang on `Working...` with no output or error. Recovery requires pressing Escape. Still open; high community engagement.  
   [Issue](https://github.com/earendil-works/pi/issues/4945)

2. **#5363 — Request: `amazon-bedrock-mantle` provider** (12 comments, 3 👍)  
   AWS Bedrock Mantle models use OpenAI-compatible API, incompatible with existing Converse-based Bedrock provider. Community needs a new provider adapter.  
   [Issue](https://github.com/earendil-works/pi/issues/5363)

3. **#5633 — Kimi 2.6 reasoning error on session continuation** (6 comments)  
   `reasoning_content` missing in resumed sessions causes 400 errors. Impacts users of the Kimi model family in long-running conversations.  
   [Issue](https://github.com/earendil-works/pi/issues/5633)

4. **#5667 — Bash overflow crash via TMPDIR macOS placeholder** (6 comments)  
   When bash tool output exceeds ~50KB, spill to `$TMPDIR` fails with `EACCES` if it's macOS's non-writable placeholder. Uncaught exception crashes Pi.  
   [Issue](https://github.com/earendil-works/pi/issues/5667)

5. **#5653 — Duplicate `pi-ai` installs split provider registry** (5 comments)  
   Installing both `pi-ai` and `pi-coding-agent` as direct deps creates two module-level provider registries. Core architecture issue needing shrinkwrap migration.  
   [Issue](https://github.com/earendil-works/pi/issues/5653)

6. **#5595 — `maxTokens` not passing through for OpenAI-completions providers** (4 comments)  
   Together.ai / DeepSeek v4pro truncates due to ignored token limits. Affects reasoning models via the completions path.  
   [Issue](https://github.com/earendil-works/pi/issues/5595)

7. **#5654 — Request: `excludeFromContext` for custom messages** (3 comments)  
   `sendMessage()` lacks `excludeFromContext` flag unlike bash executions. Needed for `/status`-style status-only messages that shouldn't pollute LLM context. Promptly implemented in PR #5678.  
   [Issue](https://github.com/earendil-works/pi/issues/5654)

8. **#5657 — Single `+` rendered as `-` in TUI** (3 comments)  
   Pure UI bug: single plus character appears as minus in sent message history. Minor but confusing display issue.  
   [Issue](https://github.com/earendil-works/pi/issues/5657)

9. **#5673 — Request: `vllm-deepseek` thinking format** (3 comments)  
   vLLM-proxied DeepSeek models need `chat_template_kwargs: { thinking: true }`. Existing `deepseek` format incompatible with vLLM.  
   [Issue](https://github.com/earendil-works/pi/issues/5673)

10. **#5670 — Tab completion grabs first item when narrowing ambiguous menu** (2 comments)  
    Editor UX issue: typing to narrow suggestions then pressing Tab auto-selects first item instead of keeping menu open.  
    [Issue](https://github.com/earendil-works/pi/issues/5670)

---

## Key PR Progress

1. **#5587 — First-time setup flow** (Closed, 2026-06-13)  
   Behind `PI_EXPERIMENTAL=1`: terminal theme detection dialog, dark/light preview, analytics opt-in. Merged today.  
   [PR](https://github.com/earendil-works/pi/pull/5587)

2. **#5681 — AiGameAgent integration** (Closed, 2026-06-13)  
   New `packages/aigameagent`: HTML5/WeChat/Douyin mini-game workflow with OpenAI-compatible HTTP API. 263 boss working-tree edits imported.  
   [PR](https://github.com/earendil-works/pi/pull/5681)

3. **#5262 — Anthropic Vertex provider** (Open, 2026-05-31)  
   Long-running PR adding Claude on Google Cloud Vertex AI via `AnthropicVertex` SDK. Reuses existing Anthropic streaming path. Strong community demand.  
   [PR](https://github.com/earendil-works/pi/pull/5262)

4. **#5679 — Anthropic Vertex provider (alternative)** (Closed, 2026-06-12)  
   Different implementation: ADC/ambient Google auth, wired into model registration + picker. Competing with #5262.  
   [PR](https://github.com/earendil-works/pi/pull/5679)

5. **#5634 — Normalize generated model costs** (Closed, 2026-06-12)  
   Fixes floating-point artifacts in OpenRouter/Vercel Gateway price conversion. Rounds to 6 decimal places.  
   [PR](https://github.com/earendil-works/pi/pull/5634)

6. **#5526 — Require terminal events for OpenAI Responses streams** (Open, 2026-06-08)  
   Fixes random stream stops by requiring terminal response events. Context counter fix included.  
   [PR](https://github.com/earendil-works/pi/pull/5526)

7. **#5678 — `excludeFromContext` for custom messages** (Open, 2026-06-12)  
   Implements #5654: flag for custom messages that shouldn't consume context. Preserved through session persistence and compaction.  
   [PR](https://github.com/earendil-works/pi/pull/5678)

8. **#5674 — Avoid project trust prompt for `pi update`** (Closed, 2026-06-12)  
   Fixes `~/.pi` vs `cwd/.pi` overlap when run from home directory. Prevents unnecessary trust dialog.  
   [PR](https://github.com/earendil-works/pi/pull/5674)

9. **#5675 — Fix compaction after reload** (Closed, 2026-06-12)  
   Stabilizes compaction: preserves token boundaries across reloads, fixes `prevCompaction is not defined` failures.  
   [PR](https://github.com/earendil-works/pi/pull/5675)

10. **#5600 — Honor Codex SSE header timeout setting** (Closed, 2026-06-12)  
    Hardcoded 10s timeout replaced with configurable `timeoutMs`/`httpIdleTimeoutMs`. Fixes slow/unstable connections.  
    [PR](https://github.com/earendil-works/pi/pull/5600)

---

## Feature Request Trends

**Provider Expansion** dominates requests: Amazon Bedrock Mantle (#5363), Anthropic Vertex (#5262, #5579), and vLLM DeepSeek thinking format (#5673). Users want to bring their own infrastructure and cloud backends without losing Pi's agent features.

**Non-Coding Use Cases** are emerging: "persona override" (#5577) would let users customize system prompts for security, QA, research roles. Extensions API improvements (#5654's `excludeFromContext`) and reload-runtime workarounds (#4754) show users pushing beyond pure coding.

**Onboarding & First-Run Experience**: Terminal theme detection (#5587, #5385), trust dialog refinement (#5674), and analytics opt-in workflows signal maturity — the project is investing in new-user experience alongside advanced features.

---

## Developer Pain Points

**Stream Reliability** is the #1 pain: OpenAI Codex connections hang (#4945), Anthropic streams wait for EOF after `message_stop` (#5592), and streaming calls stall without deadline (#5558). Multiple PRs (#5526, #5600) attempt fixes but root cause persists.

**Credential/Auth Confusion**: Bedrock `apiKey` ignored (#5584), unauthenticated providers hang instead of failing fast (#5571), uppercase header values falsely treated as env vars (#5661). Authentication paths are inconsistent across providers.

**Edge Cases in Core Logic**: TUI rendering quirks (`+` → `-`, #5657), compaction failure after reload (#5675, #5676), `parentId` orphan chains on `/fork` (#5669), and symlink duplication (#5648). The agent session model has subtle state bugs.

**Process & Runtime Issues**: `pi update` hangs after completion (#5619, #5645), Bun compatibility broken (#4160), shell commands use wrong shell (#5578). These degrade the user experience for non-standard setups.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for 2026-06-13.

---

# Qwen Code Community Digest — 2026-06-13

## Today's Highlights

The community is actively engaged around two major themes: **policy change feedback** (OAuth free tier reduction) and **developer experience for long-running sessions** (model degradation, tool call loops, and session management). The v0.18.0 release landed with a key fix for copy operations in the CLI. Several pull requests show strong momentum in improving the daemon mode, Web Shell, and cross-provider model identity handling.

## Releases

**v0.18.0** was released in the last 24 hours. This is a patch release that fixes a CLI issue where "thought parts" were incorrectly included in copy output.
[Release Link](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0)

## Hot Issues

1. **[#3203 – Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** (127 comments)
   A highly debated feature request to drastically reduce the free daily quota from 1,000 to 100 requests and phase out the free tier entirely. This is the most commented issue in the last 24 hours and reflects significant community concern about access.

2. **[#4514 – Daemon Capability Gaps & Backlog](https://github.com/QwenLM/qwen-code/issues/4514)** (15 comments)
   A detailed tracking issue for remaining gaps in the `qwen serve` HTTP/SSE surface. This is a critical roadmap item for developers building on top of the daemon, covering ACP-compatible slash command passthrough.

3. **[#4488 – VS Code Plugin Not Displaying in Newer VSCode](https://github.com/QwenLM/qwen-code/issues/4488)** (7 comments)
   A high-impact bug report for VS Code users on version 1.120.0+ where the Qwen Code sidebar plugin flashes and disappears. This affects users on the latest editor versions.

4. **[#5018 – Long-context Task Attention Degradation](https://github.com/QwenLM/qwen-code/issues/5018)** (3 comments)
   A user reports significant "forgetfulness" and lack of focus in long-running tasks. This is a core model quality issue that affects developer trust in complex workflows.

5. **[#4976 – Auto-generated Memory Interfering with CLI Calls](https://github.com/QwenLM/qwen-code/issues/4976)** (3 comments)
   A user reports that automatic memory generation is interfering with normal CLI invocations, leading to wasted rounds and incorrect tool calls.

6. **[#4877 – OpenWork Cannot Distinguish Same Model from Different Providers](https://github.com/QwenLM/qwen-code/issues/4877)** (4 comments)
   A configuration UI bug where models with the same ID from different providers (e.g., `glm-5`) appear as duplicates, making selection impossible. This is a key blocker for multi-provider users.

7. **[#4825 – `qwen sessions list` Subcommand Request](https://github.com/QwenLM/qwen-code/issues/4825)** (4 comments)
   A welcome-PR labeled feature request for a script-friendly session listing tool with `--json` and date filters. This would improve automation and session lifecycle management.

8. **[#4845 – `/import-config` for Claude Migration](https://github.com/QwenLM/qwen-code/issues/4845)** (3 comments)
   A feature request for a one-click import of MCP servers, instructions, and custom commands from Claude Code/Desktop. This targets a friction point for developers switching tools.

9. **[#5067 – Focus-Jump Bug with Agent Panel](https://github.com/QwenLM/qwen-code/issues/5067)** (2 comments)
   A complex UI bug where keyboard focus navigation targets hidden or expired agents in the LiveAgentPanel, creating phantom selection states. This is a follow-up to a prior fix.

10. **[#5055 – Antivirus False Positive on VSIX](https://github.com/QwenLM/qwen-code/issues/5055)** (2 comments)
    A user reports that Windows Defender flags the v0.18.0 VSIX as a trojan. This is a packaging/security concern that needs immediate resolution for Windows users.

## Key PR Progress

1. **[#5069 – Revamp Floating Todo Panel Interactions (Web Shell)](https://github.com/QwenLM/qwen-code/pull/5069)** (New)
   Reworks the "Current tasks" panel from a static display into an interactive component. Addresses jumbled numbering and lack of progress status.

2. **[#5040 – DaemonTransport Abstraction Layer](https://github.com/QwenLM/qwen-code/pull/5040)** (New)
   Adds a pluggable transport layer (`DaemonTransport`) for the daemon client, enabling REST+SSE, ACP HTTP+SSE, or ACP WebSocket without forking infrastructure. A major architecture improvement for the daemon mode.

3. **[#5066 – Web Shell Improvements: Token Usage, Settings, Retry](https://github.com/QwenLM/qwen-code/pull/5066)** (New)
   Adds structured token usage tracking, a full settings panel with i18n (Chinese/English), theme/language pickers, and compact mode persistence for the daemon web shell.

4. **[#5003 – Remove Tool Group Borders & Collapse Tool Results](https://github.com/QwenLM/qwen-code/pull/5003)** (Updated)
   UI simplification removing borders from tool groups and collapsing completed results to a single-line header. Aims to reduce visual clutter in the TUI.

5. **[#4894 – Fix FIFO Blocking on Startup](https://github.com/QwenLM/qwen-code/pull/4894)** (Updated)
   Fixes a blocking issue when `--json-file` points to a FIFO with no reader, switching to non-blocking open. This is critical for headless/automated workflows.

6. **[#5039 – Precise Model Identity via id+baseUrl](https://github.com/QwenLM/qwen-code/pull/5039)** (New)
   Solves the model identity ambiguity problem (see issue #4877) by storing `model.id`, `model.baseUrl`, and `model.provider` in settings.

7. **[#5071 – Fix Tool Result Handoff Race in CLI](https://github.com/QwenLM/qwen-code/pull/5071)** (New)
   Fixes a race condition where very fast tool completions could be dropped after the model stream ended. Uses synchronous ref counting to ensure reliable callbacks.

8. **[#5063 – Detect Incomplete Qwen Review Runs in CI](https://github.com/QwenLM/qwen-code/pull/5063)** (New)
   Tightens CI checks so that a PR review workflow fails when the output contains an API error, rather than reporting a green job. Improves CI reliability.

9. **[#5057 – Persist File History Snapshot Updates](https://github.com/QwenLM/qwen-code/pull/5057)** (New)
   Makes file-history snapshot updates durable during a turn by recording immediately after an edit, preventing loss of backup state.

10. **[#5061 – Preserve Background Agent Launch Flags](https://github.com/QwenLM/qwen-code/pull/5061)** (Closed/Merged)
    Preserves launch-time flags (approval mode, bare mode) for background agents across process restarts, ensuring interrupted agents resume with correct configuration.

## Feature Request Trends

- **Declarative Agent Definitions**: Multiple requests (e.g., #4821) ask for Markdown + YAML frontmatter agent definitions, mirroring the Claude Code pattern.
- **Extended Session Management**: High interest in a `qwen sessions list` command with JSON output and filtering (#4825).
- **Data Export & Migration**: Requests for `/import-config` from Claude (#4845) and general session data export capabilities.
- **Precise Multi-Provider Model Switching**: A strong pattern of requests for better handling of identical model IDs from different providers (#4877, #1206).

## Developer Pain Points

- **Model/Long-Context Quality**: Recurring reports of "forgetfulness," "intelligence degradation," and repetitive tool call loops in long-running sessions (#5018, #5019, #5029).
- **Platform Compatibility**: Issues with Windows (`printf` command not found in #5010) and antivirus false positives (#5055) create friction for non-macOS/Linux users.
- **UI/UX Regressions**: Focus-jump bugs (#5067) and viewport rendering issues in "Virtualized History" mode (#4921, #4942) are recurring friction points after new UI features are shipped.
- **Tool Call Interference**: Users report that automatic memory generation (#4976) or post-cancellation execution (#5016) interferes with expected CLI behavior, leading to wasted time and confusion.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (Now CodeWhale) Community Digest — 2026-06-13

## Today’s Highlights
The project officially **rebrands to CodeWhale** with the release of **v0.8.59**, deprecating the legacy `deepseek-tui` npm package. A massive wave of **agent-fleet infrastructure** lands—leases, heartbeats, workers, alerts, and task specs—while **TUI UX quality-of-life** improvements (clickable sidebar, compact transcripts, hyperlinks, Ctrl+B background) and **multi-provider fixes** (Anthropic adapter, Moonshot reasoning, un-hardcoded model IDs) continue to stabilize the codebase for v0.9.0.

---

## Releases
**v0.8.59** — CodeWhale becomes the canonical name.  
The legacy `deepseek-tui` npm package is deprecated; all users should migrate following `docs/REBRAND.md`.  
No further releases under the old name.  
_Link: [v0.8.59 release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.59)_

---

## Hot Issues (10 noteworthy)

1. **[#2584 – Bug: Can't upload local images](https://github.com/Hmbown/CodeWhale/issues/2584)**  
   When using `/attach` with a local image, the model receives the raw file path instead of base64. Community flagged immediately (8 comments), closed. Critical for multi-modal workflows.

2. **[#1871 – QoL: Taskbar progress, animated spinner, completion sound](https://github.com/Hmbown/CodeWhale/issues/1871)**  
   Popular enhancement (5 comments, 1 👍) asking for alt-tab friendly feedback. Still open, awaiting implementation.

3. **[#431 – Exa web-search route](https://github.com/Hmbown/CodeWhale/issues/431)**  
   Open enhancement for v0.9.0: if `EXA_API_KEY` is set, route `web_search` through Exa MCP; fallback to DDG/Bing. Note: community prefers graceful fallback.

4. **[#1722 – Auto-compact threshold with Ctrl+L](https://github.com/Hmbown/CodeWhale/issues/1722)**  
   Closed – fixed context-saturation freeze (3 comments). The TUI became unresponsive at ~99.6% memory. Root cause was dual guardrails starving the event loop.

5. **[#2606 – Sidebar checklist status not updating](https://github.com/Hmbown/CodeWhale/issues/2606)**  
   Bug: after `checklist_write`, the Work panel shows stale data. Root cause: sidebar doesn't refresh on completion events. Closed.

6. **[#2787 – MCP count error in status bar](https://github.com/Hmbown/CodeWhale/issues/2787)**  
   When both global and project-level MCP config exist, the status bar shows an incorrect MCP count. Closed with v0.9.0‑stewardship fix.

7. **[#3018 – Un-hardcode DeepSeek from auto-router](https://github.com/Hmbown/CodeWhale/issues/3018)**  
   Auto‑model and subagent model selection only worked on DeepSeek; OLLaMA, OpenAI, Moonshot, etc. got a guaranteed 400. Closed with PR #3045.

8. **[#471 – EPIC: Web UI scaffold](https://github.com/Hmbown/CodeWhale/issues/471)**  
   Open epic for v0.9.0: SolidJS/React+Vite web UI that talks to `codewhale serve --http`. Multiple sub-issues (composer, file browser, approval, auth). High demand.

9. **[#3159 – Fleet scheduler leases, heartbeats, backpressure](https://github.com/Hmbown/CodeWhale/issues/3159)**  
   Closed – implements scheduler‑level resilience for the agent fleet: leases, heartbeats, stuck‑worker recovery. Part of the new fleet infrastructure.

10. **[#2656 – Subagent session‑name conflicts](https://github.com/Hmbown/CodeWhale/issues/2656)**  
    Agents can't easily diagnose session-name collisions (2 comments). Closed with better error messages via PR #3041.

---

## Key PR Progress (10 important)

1. **[PR #3036 – Hide internal IDs from normal UI](https://github.com/Hmbown/CodeWhale/pull/3036)**  
   Replaces raw UUIDs/hex IDs with stable labels in sidebar and transcript; full identifiers remain in hover detail. Closes #3030.

2. **[PR #3034 – v0.8.58: Constitution refactor, Codex fixes, sidebar improvements](https://github.com/Hmbown/CodeWhale/pull/3034)**  
   Major branch: YAML‑based constitution production, rebrand fixes, split tools/model panels in sidebar.

3. **[PR #3035 – Throttle AgentProgress redraws](https://github.com/Hmbown/CodeWhale/pull/3035)**  
   Prevents TUI freeze when 4+ subagents run concurrently. Full redraw on every progress event was saturating the render loop.

4. **[PR #3040 – Clickable sidebar rows](https://github.com/Hmbown/CodeWhale/pull/3040)**  
   Mouse click dispatch for Tasks and Agents panels: click to inspect/cancel jobs. Adds mouse‑driven workflow.

5. **[PR #3042 – exec CLI flags: allowed‑tools, max‑turns, append‑system‑prompt](https://github.com/Hmbown/CodeWhale/pull/3042)**  
   Four new flags for unattended/CI use. Enables fine‑grained control over tool access and turn limits.

6. **[PR #3037 – Compact tool‑call transcript rendering](https://github.com/Hmbown/CodeWhale/pull/3037)**  
   Suppresses boilerplate (“(no output)”, sub‑second timings) in default compact view. Reduces visual noise.

7. **[PR #3039 – OSC 8 hyperlink infrastructure](https://github.com/Hmbown/CodeWhale/pull/3039)**  
   Builds emission path for working hyperlinks bypassing ratatui's buffer (which strips ESC bytes). Foundation for clickable links.

8. **[PR #3038 – Ctrl+B directly backgrounds shell](https://github.com/Hmbown/CodeWhale/pull/3038)**  
   One‑key shortcut to move foreground shell command to background, replacing two‑step menu.

9. **[PR #3049 – JSON decision contract for hooks](https://github.com/Hmbown/CodeWhale/pull/3049)**  
   Hooks can emit `{"decision": "allow"|"deny"|"ask", ...}` on stdout, plus glob matchers and project‑local hooks. Closes #3026.

10. **[PR #3054 – Native Anthropic Messages API adapter](https://github.com/Hmbown/CodeWhale/pull/3054)**  
    Adds third provider dialect: `cache_control`, thinking blocks, tool streaming. Use `--provider anthropic` with `ANTHROPIC_API_KEY`. Closes #3014.

---

## Feature Request Trends

- **Multi‑provider parity** – The community repeatedly asks that features work across providers (Ollama, OpenAI, Moonshot, Anthropic). Issues #3018, #3045, #3047, #3050, #3054 directly address this. Expect more PRs on reasoning, model‑specific templates, and tool‑call differences.
- **Web/IDE integration** – The Web UI epic (#471) and VS Code extension (#461) are major open requests. Users want a GUI beyond the TUI for onboarding and remote work.
- **Agent fleet orchestration** – A dozen issues/PRs this week (e.g., #3155–#3162) define fleet protocols, leases, alerts, and worker adapters. This is clearly the priority for v0.8.60.
- **TUI UX polish** – Features like configurable keymaps (#436), OSC8 hyperlinks (#3039), clickable sidebar (#3040), and completion sounds (#1871) show strong demand for a smoother developer experience.
- **Permission and safety controls** – Issues #411, #412, #414 (external directory gate, permission memory, subagent permission derivation) indicate a push toward finer‑grained security, especially for autonomous agents.

---

## Developer Pain Points

- **Context saturation freezing** – Issue #1722 (now fixed) highlighted a critical UX pain: the TUI becoming completely unresponsive when memory nears 100%. Community contributed to root‑cause analysis.
- **Subagent session name conflicts** – #2656 and #2657 show agents struggle to diagnose tool unavailability and session collisions. PR #3041 improves error messages but deeper diagnostics are still needed.
- **Double invocation of `agent_eval`** – #2605 reports that the first call often returns a “deferred and now loaded” message, requiring a retry. Workaround known but not yet patched.
- **MCP configuration confusion** – #2787 reveals errors when both global and local `mcp.json` exist; display count is wrong. Fixed, but indicates complexity in multi‑config management.
- **Rebrand migration friction** – The v0.8.59 release deprecates `deepseek-tui` and requires docs migration (`REBRAND.md`). Expect short‑term confusion for existing users not following the repository.
- **Cross‑provider feature gaps** – Several issues (e.g., #3018, #3050) complain about hardcoded DeepSeek‑only paths for reasoning, subagent model selection, and capability detection. The project is actively closing these gaps, but legacy configs may need updating.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*