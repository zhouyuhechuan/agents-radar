# AI CLI Tools Community Digest 2026-07-16

> Generated: 2026-07-16 01:55 UTC | Tools covered: 9

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
**Date:** 2026-07-16  
**Prepared for:** Technical decision-makers & developers  

---

## 1. Ecosystem Overview

The AI CLI tools landscape on July 16, 2026 is characterized by **rapid iteration alongside growing reliability concerns**. While nearly all major tools shipped patches or alphas in the past 24 hours, a significant portion of community energy is consumed by **cost-control, safety, and platform compatibility** issues—particularly around subagent orchestration, Windows stability, and MCP protocol friction. OpenAI Codex and Qwen Code are pushing forward with architectural rewrites (Rust migration, daemon multi-workspace), while Claude Code faces a crisis of trust with multiple high-severity bug clusters. Gemini CLI and OpenCode show strong PR velocity but are wrestling with layout regressions and subagent reliability. Copilot CLI remains relatively stable but is held back by MCP authentication gaps. The ecosystem is maturing from “can it generate code?” to “can it do so safely, scalably, and across platforms without burning my budget?”

---

## 2. Activity Comparison (Last 24h)

| Tool               | Hot Issues (activity proxy) | Key PRs (merged/open) | Releases Today     | Notes                                       |
|--------------------|-----------------------------|------------------------|--------------------|---------------------------------------------|
| **Claude Code**    | 10                          | 4 (closed/open)        | 1 patch (v2.1.211) | Crisis mode on subagent recursion & data loss |
| **OpenAI Codex**   | 10                          | 10 (9 closed, 1 open)  | 3 alphas (Rust)    | Heavy PR activity; context indicator missing |
| **Gemini CLI**     | 10                          | 10 (1 merged, 9 open)  | 1 nightly          | Strong pipeline; 400 error fix merged        |
| **Copilot CLI**    | 10                          | 0 (none in 24h)        | 1 patch (v1.0.71)  | Patch-only; MCP issues dominate               |
| **Kimi Code CLI**  | 0                           | 1 open                 | None               | Minimal community activity                     |
| **OpenCode**       | 10                          | 10 (8 closed, 2 open)  | 1 patch (v1.18.2)  | Layout backlash; desktop stability focus       |
| **Pi**             | 10                          | 10 (6 closed, 4 open)  | None               | Codex reliability & Windows stability issues  |
| **Qwen Code**      | 10                          | 10 (all open)          | 2 (driver + nightly)| Daemon & multi-workspace RFC gaining traction |
| **DeepSeek TUI**   | 10                          | 10 (8 closed, 2 open)  | None               | Windows freeze fixes; refactoring toward v0.9 |

*Note: “Hot Issues” are the top 10 highlighted by each digest; “Key PRs” include the most important pull requests reported. Does not reflect total repo counts.*

---

## 3. Shared Feature Directions

Several cross-cutting requirements appear across multiple tool communities, often with overlapping issue numbers and pain points:

| Trend                     | Tools Affected              | Specific Needs                                                                 |
|---------------------------|-----------------------------|--------------------------------------------------------------------------------|
| **Cost safeguards & agent loop prevention** | Claude Code, Gemini CLI, Copilot CLI | Configurable subagent depth/caps, kill switches, cost alerts (Claude #68619, #69578; Gemini #28164; Copilot #1477) |
| **MCP protocol reliability** | Claude Code, Copilot CLI, Qwen Code, Gemini CLI | 256-tool caps (#77704), OAuth tool surfacing (#4096), dot-in-name rejection (#6970), connection timeout (#28410) |
| **Windows stability**     | Claude Code, Codex, Copilot CLI, Pi, DeepSeek TUI | NTFS junction traversal (#75275), ARM64 crash (#33381), git.exe loops (#33450), IME deadlocks (#1835), CLI freeze (#1812) |
| **Context / token usage visibility** | Codex, Copilot CLI, Claude Code (implied) | Persistent status bar (#23794, #2052); users want real-time consumption data before committing to actions |
| **VS Code & IDE parity**  | Claude Code, Gemini CLI, OpenCode | Diff review UI (#33932), inline editing, `/workflows` support (#74585) |
| **Multi-agent orchestration** | Claude Code, Codex, OpenCode, Qwen Code | Subagent messaging (#77950), thread selection (#30813), handoff reliability (#5239) |
| **Session state & compaction** | Claude Code, OpenCode, Pi, Qwen Code | Fork/resume conflicts (#69364), overshoot on compaction (#17340), retry on transient drops (#6647) |
| **Safety & destructive operation warnings** | Claude Code, Gemini CLI, Copilot CLI | `rm -rf` detection (#75275, #33464), `git reset --force` (#22672), forced-command heuristics |

---

## 4. Differentiation Analysis

| Tool             | Primary Focus                          | Target Users               | Technical Approach & Differentiators                                                                 |
|------------------|----------------------------------------|----------------------------|-------------------------------------------------------------------------------------------------------|
| **Claude Code**  | Enterprise agent orchestration (Cowork) | Large teams, heavy automation | Subagent trees, Cowork projects, plugin ecosystem; currently struggling with cost runaway & data loss |
| **OpenAI Codex** | Model compatibility & Rust rewrite      | Multi-model users           | Fast alpha release train; supporting GPT-5.x series; strong on dangerous-command detection            |
| **Gemini CLI**   | A2A protocol & subagent introspection   | Google ecosystem users      | Tighter integration with Gemini models; focus on subagent recovery & cancellation handling            |
| **Copilot CLI**  | Secure enterprise MCP & voice           | GitHub-centric teams        | MCP OAuth bridging; BYOK support; voice mode; conservative release pace                               |
| **Kimi Code CLI**| Minimal activity (telemetry alignment)  | MoonshotAI users            | Very low community velocity; likely internal focus                                                    |
| **OpenCode**     | Desktop UX & V2 plugin architecture     | Desktop-first developers    | Layout stability issues; advanced plugin system; strong push toward V2 with dynamic tools             |
| **Pi**           | Extensibility (extensions, hooks)       | Extension developers        | Node.js/TypeScript stack; TUI rendering; emphasis on provider independence (multiple backends)       |
| **Qwen Code**    | Daemon & Chinese platform integration   | Chinese enterprise users    | Multi-workspace daemon; DingTalk, WeCom channels; safety classifier; strong on CUA (computer use)    |
| **DeepSeek TUI** | Refactoring & Windows i18n              | DeepSeek model users        | Rust TUI; heavy focus on localisation (zh-Hant), IME support; cleaning up technical debt before v0.9 |

---

## 5. Community Momentum & Maturity

**Highest momentum & engagement:**
- **Claude Code** – Largest issue count and community reactions, but driven by **crisis** (cost bugs, data loss). Indicates widespread adoption but fragile trust.
- **OpenAI Codex** – Strong PR velocity (10 key PRs), active Rust rewrite, but missing context indicator remains a top UX regression.
- **Qwen Code** – Growing rapidly in Chinese ecosystem; daemon RFC and multi-workspace features show architectural ambition.

**Rapidly iterating (stable with some friction):**
- **Gemini CLI** – Active development on cancellation, MCP timeout, security; subagent false-success report a lingering concern.
- **OpenCode** – High issue volume with layout changes causing backlash; core feature work (V2 plugins) continues.
- **Pi** – Moderate activity; extension ecosystem developing but Codex reliability hurts adoption.

**Stable but slower community:**
- **Copilot CLI** – Fewer issues but high pain on MCP auth; patch-only release mode suggests stable core.
- **DeepSeek TUI** – Refactoring focus; low issue churn but Windows bugs persist.
- **Kimi Code CLI** – Near-dormant; likely not a priority for MoonshotAI currently.

**Maturity indicators:**
- Safety guards are still immature – almost every tool has open issues about data loss, cost runaway, or security bypasses.
- MCP is emerging as a universal integration layer but exposes protocol-level problems (caps, auth, naming).
- Desktop/TUI parity remains inconsistent – VS Code features lag behind CLI in several tools.

---

## 6. Trend Signals for the Industry

1. **Cost governance is now table stakes** – Multiple high-dollar incident reports (Claude Code $27.60 single run, $600+ reported) show that AI CLI tools must ship hard limits, kill switches, and transparent cost dashboards. Users are running real production workloads and cannot trust agents without financial safeguards.

2. **Subagent orchestration is the next frontier** – The shift from single-turn assistant to multi-agent workflows is exposing fundamental reliability gaps: recursive spawning, missed handoffs, stalls, and lack of monitoring. The tools that solve “reliable agent trees” will win enterprise adoption.

3. **Windows support remains the Achilles’ heel** – Every major tool except Gemini CLI (notably absent from reports) has significant Windows-specific bugs. With developer heterogeneity increasing, cross-platform parity is a hard requirement, not a nice-to-have.

4. **MCP is becoming the universal plugin API but needs standardization** – Issues with tool caps, dot-separated names, authentication bridging, and timeout handling indicate that the Model Context Protocol is hitting real-world constraints. Expect pressure for MCP spec revisions in Q3 2026.

5. **LLM model version fragmentation causes persistent friction** – Codex (GPT-5.3 Spark vs Sol), Gemini (model access tiers), and Copilot (free vs premium) all show issues where model-specific parameters break tool compatibility. Unified parameter interfaces across models remain elusive.

6. **Desktop IDE integration is no longer optional** – The gap between TUI and desktop (VS Code) is a top-3 complaint for Claude Code, Copilot, and OpenCode. Users expect a seamless hybrid experience: CLI for automation, GUI for review and diff management.

7. **Localisation and regional platform support are growing** – DeepSeek TUI’s i18n efforts, Qwen Code’s WeCom/DingTalk integrations, and token cost in CNY show that Asian markets are driving distinct requirements that Western-first tools must consider.

8. **Security hardening is catching up** – OpenCode’s wildcard WebFetch scoping, Qwen’s trusted invocation context, and Codex’s dangerous `rm` detection reflect a maturing mindset. Expect more tools to adopt provenance-tracked execution contexts.

---

**Conclusion:** The ecosystem is in a painful but necessary transition from “demo-level AI assistants” to “production-grade autonomous coding agents.” Trust, cost control, and cross-platform reliability are the gating factors for mainstream adoption. The next 3–6 months will likely see convergence around MCP 2.0, agent tree lifecycle management, and mandatory cost governance features.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-07-16 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking (by Community Discussion Activity)

The following PRs have generated the most engagement through detailed technical discussion and issue cross-referencing:

### 1. `fix(skill-creator): run_eval.py always reports 0% recall` (#1298)
- **Functionality:** Fixes the core evaluation pipeline (`run_eval.py`, `run_loop.py`, `improve_description.py`) that was reporting `recall=0%` for every skill description due to improper eval artifact installation, Windows stream reading failures, and broken trigger detection. This bug blocked all description optimization against real signal.
- **Discussion:** References issue #556 (12 comments, 7 👍) with "10+ independent reproductions." The diagnostic depth is substantial—touches the entire skill-creation feedback loop.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/1298)

### 2. `Add document-typography skill` (#514)
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Targets a universal pain point: typographic defects in all Claude-generated documents.
- **Discussion:** Proposes a skill for a problem no existing skill addresses. The community resonance stems from the universal applicability—"These issues affect every document Claude generates."
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/514)

### 3. `Add self-audit — mechanical verification + four-dimension reasoning quality gate` (#1367)
- **Functionality:** A universal output-audit skill that performs mechanical file verification then a four-dimension reasoning audit in damage-severity priority order. Works across any project, tech stack, and model.
- **Discussion:** A meta-skill that generated cross-reference with issue #1385 proposing a three-gate pipeline. High interest in output quality verification patterns.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/1367)

### 4. `fix(docx): prevent tracked change w:id collision with existing bookmarks` (#541)
- **Functionality:** Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: shared `w:id` space across multiple OOXML constructs.
- **Discussion:** Part of a cluster of DOCX/PDF fixes by contributor Lubrsy706, demonstrating deep OOXML format expertise. High practical value for enterprise document workflows.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/541)

### 5. `Add pyxel skill for retro game development` (#525)
- **Functionality:** Integrates with pyxel-mcp (an MCP server for the Pyxel retro game engine). Covers the full iteration loop: write → run_and_capture → inspect → iterate.
- **Discussion:** Unique among submissions—bridges MCP server capabilities with Claude Skills. Still open with recent activity (updated 2026-07-15), suggesting active development.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/525)

### 6. `Add color-expert skill` (#1302)
- **Functionality:** Comprehensive color expertise for any task involving color: naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway), color spaces with usage tables (OKLCH for scales, OKLAB for gradients, CAM16 for perception), accessibility, and palette generation.
- **Discussion:** Self-contained domain expertise—a model for how specialized knowledge can be packaged as a skill.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/1302)

### 7. `Add skill-quality-analyzer and skill-security-analyzer to marketplace` (#83)
- **Functionality:** Two meta-skills: one evaluates skill quality across five dimensions (Structure & Documentation, examples, resources), the other assesses security posture. Self-referential tooling for the ecosystem itself.
- **Discussion:** Long-lived PR (since 2025-11-06) indicating deliberate review. Represents community investment in quality infrastructure.
- **Status:** OPEN | [View PR](https://github.com/anthropics/skills/pull/83)

---

## 2. Community Demand Trends (from Issues)

### Most-Anticipated Skill Directions

| Trend | Signal | Key Issue |
|---|---|---|
| **Security & Trust** | High urgency: community skills distributed under `anthropic/` namespace create impersonation risk. 34 comments, highest engagement. | [#492](https://github.com/anthropics/skills/issues/492) |
| **Team Collaboration** | Strong demand for org-wide skill sharing without manual file transfer. 14 comments, 7 👍. | [#228](https://github.com/anthropics/skills/issues/228) |
| **Agent Governance** | Proposal for safety patterns: policy enforcement, threat detection, trust scoring, audit trails. No competing skill exists. | [#412](https://github.com/anthropics/skills/issues/412) |
| **Memory Optimization** | compact-memory skill proposed: symbolic notation for compact agent state to reduce context waste. Active discussion (9 comments). | [#1329](https://github.com/anthropics/skills/issues/1329) |
| **Skill-Creator Fixes** | Crowded bug cluster: Windows compatibility (3 separate issues, 3-12 comments each), YAML parsing, recall=0% bug. Multiple contributors independently hitting the same walls. | [#556](https://github.com/anthropics/skills/issues/556), [#1061](https://github.com/anthropics/skills/issues/1061), [#1169](https://github.com/anthropics/skills/issues/1169) |
| **MCP Integration** | Interest in exposing Skills as MCP servers for standardized API interfaces. | [#16](https://github.com/anthropics/skills/issues/16) |

**Key takeaway:** The community is not just requesting *new* skills—they are investing heavily in the *tooling* to build skills (run_eval fixes, validation, Windows support) and the *quality infrastructure* (security analyzers, self-audit, governance). The highest-traffic issue (#492) is about trust, not functionality.

---

## 3. High-Potential Pending Skills (Likely to Land Soon)

These PRs have substantial development investment, active discussion, and address recognized pain points:

| Skill | Contributor | Potential Impact | Status |
|---|---|---|---|
| **document-typography** (#514) | PGTBoos | Universal—every document benefits | Open, no merge blockers visible |
| **self-audit** (#1367) | YuhaoLin2005 | Complements existing reasoning gate proposal (#1385) | Open, cross-referenced with new proposal |
| **color-expert** (#1302) | meodai | Self-contained, low integration risk | Open, recent activity |
| **skill-quality-analyzer + skill-security-analyzer** (#83) | eovidiu | Ecosystem quality infrastructure | Open, long-lived, under review |
| **testing-patterns** (#723) | 4444J99 | Comprehensive testing stack coverage | Open, substantive content |
| **pyxel** (#525) | kitao | Bridges MCP + Skills ecosystem | Open, updated 3 days ago |

**Windows compatibility PRs** (#1099, #1050, #362, #361) form a critical dependency cluster—these are prerequisites for the skill-creator to work on ~30% of developer machines. The parallel fixes suggest maintainers are converging on a solution.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *infrastructure and quality* skills—tools that fix the skill-creation pipeline (especially Windows compatibility and evaluation reliability), enforce output quality (typography, self-audit, security analysis), and establish trust boundaries—rather than for domain-specific content skills.**

---

```json
{
  "digest": {
    "date": "2026-07-16",
    "title": "Claude Code Community Digest — July 16, 2026",
    "sections": {
      "todays_highlights": "A new patch release v2.1.211 ships with subagent text forwarding for stream-json output and permission preview fixes. The community is increasingly alarmed by a cluster of critical bugs involving uncontrolled recursive subagent spawning, which has led to multi-hundred-dollar token burns and data loss on Windows (NTFS junction traversal). Three separate high-severity issues around agent cost explosions have accumulated 70+ comments combined, signaling a top-of-mind reliability crisis.",
      "releases": {
        "summary": "One new release in the last 24 hours.",
        "items": [
          {
            "version": "v2.1.211",
            "url": "https://github.com/anthropics/claude-code/releases/tag/v2.1.211",
            "changes": [
              "Added `--forward-subagent-text` flag and `CLAUDE_CODE_FORWARD_SUBAGENT_TEXT` environment variable to include subagent text and thinking in stream-json output",
              "Fixed permission previews relayed to chat channels not neutralizing bidirectional-override, zero-width, and look-alike characters"
            ]
          }
        ]
      },
      "hot_issues": [
        {
          "id": 53940,
          "title": "Cowork Edit/Write tools silently truncate files via byte-conservation buffer cap",
          "url": "https://github.com/anthropics/claude-code/issues/53940",
          "comments": 43,
          "reactions": 16,
          "why_it_matters": "A deterministic, reproducible bug that silently truncates files at all sizes — particularly dangerous because there is no warning or error shown. 43 comments indicate widespread frustration and difficulty in diagnosing the root cause."
        },
        {
          "id": 33932,
          "title": "VS Code Extension: Diff review UI similar to GitHub Copilot Edits Review",
          "url": "https://github.com/anthropics/claude-code/issues/33932",
          "comments": 34,
          "reactions": 150,
          "why_it_matters": "The most upvoted open feature request (150 reactions). Developers strongly desire a dedicated diff review panel in VS Code, mirroring Copilot's UX for reviewing AI-proposed changes before applying them."
        },
        {
          "id": 68619,
          "title": "Subagent spawning and subagent pattern bugs trigger infinite recursion, infinite token usage",
          "url": "https://github.com/anthropics/claude-code/issues/68619",
          "comments": 31,
          "reactions": 10,
          "why_it_matters": "A critical compound regression: subagents recursively spawn 50+ levels deep, ignore fork-subagent disable flags, and permission denials trigger further spawning. Marked as duplicate but remains open, suggesting upstream fix is pending."
        },
        {
          "id": 60385,
          "title": "Remote Control MCP permission prompts for non-read tools never surface in claude.ai/code web UI",
          "url": "https://github.com/anthropics/claude-code/issues/60385",
          "comments": 20,
          "reactions": 0,
          "why_it_matters": "Blocking bug for remote-control workflows: permission prompts only appear in the TUI, not the web UI, making remote sessions effectively unusable for write/MCP operations. Closed as fixed but with 20 comments suggesting the fix may be incomplete."
        },
        {
          "id": 40043,
          "title": "Allow removal of local folders from a Cowork project's context",
          "url": "https://github.com/anthropics/claude-code/issues/40043",
          "comments": 17,
          "reactions": 55,
          "why_it_matters": "A highly requested Cowork UX improvement. Once a folder is added to a project, users cannot remove it without full project reconfiguration. 55 upvotes show this is a common pain point for team workflows."
        },
        {
          "id": 69578,
          "title": "Uncontrolled sub-agent recursive loop caused ~800k token consumption & $27.60 unexpected charge",
          "url": "https://github.com/anthropics/claude-code/issues/69578",
          "comments": 8,
          "reactions": 1,
          "why_it_matters": "Real-world cost incident report. Sub-agents spawned without depth limit, burning 800K tokens with near-zero useful output. Community is increasingly vocal about missing safeguards around agent orchestration costs."
        },
        {
          "id": 75275,
          "title": "Windows: stale-worktree cleanup rm -rf traverses NTFS junctions and deletes data outside worktree (~800 GB data loss)",
          "url": "https://github.com/anthropics/claude-code/issues/75275",
          "comments": 2,
          "reactions": 0,
          "why_it_matters": "A catastrophic data-loss bug on Windows. The `rm -rf` cleanup does not respect NTFS junctions, descending into linked directories and deleting data outside the worktree. Reported loss of ~800 GB. High-priority label applied."
        },
        {
          "id": 74990,
          "title": "/compact and auto-compaction drop entire Available skills system-reminder; /reload-skills recovers with 'no changes'",
          "url": "https://github.com/anthropics/claude-code/issues/74990",
          "comments": 3,
          "reactions": 1,
          "why_it_matters": "Compaction silently drops the skills system prompt, which means the agent forgets what plugins/skills are available. After reload, it reports 'no changes,' masking the bug. Particularly insidious for users who rely on custom skills."
        },
        {
          "id": 77950,
          "title": "Nested (grandchild) background agents can't message their direct parent — parent stalls indefinitely",
          "url": "https://github.com/anthropics/claude-code/issues/77950",
          "comments": 2,
          "reactions": 0,
          "why_it_matters": "A fresh bug in the agent tree orchestration: grandchild agents' completion messages are not routed to the direct parent, causing indefinite stalls. Indicates a fundamental issue in the agent messaging layer."
        },
        {
          "id": 77704,
          "title": "Custom remote MCP connectors intermittently lose all tools / aggregate tool list capped at exactly 256",
          "url": "https://github.com/anthropics/claude-code/issues/77704",
          "comments": 1,
          "reactions": 0,
          "why_it_matters": "A regression since mid-July: MCP tool lists are capped at 256 tools across all connectors, causing intermittent tool loss. Affects web and desktop, org and personal accounts. Likely a server-side cap that needs urgent re-evaluation."
        }
      ],
      "key_pr_progress": [
        {
          "id": 16680,
          "title": "feat: Add recall plugin for conversation context recovery",
          "url": "https://github.com/anthropics/claude-code/pull/16680",
          "status": "closed",
          "author": "bledden",
          "description": "A community plugin that indexes each message + response pair, enabling semantic search across past conversations. Addresses the pain point of scrolling/copying to recover context — essentially a local memory layer for Claude Code sessions."
        },
        {
          "id": 77916,
          "title": "Add code-quality-pipeline plugin",
          "url": "https://github.com/anthropics/claude-code/pull/77916",
          "status": "open",
          "author": "RonMizrahi",
          "description": "A skill-based plugin defining two quality gates: Gate A for per-file checks (lint, type-check, test) before E2E, and Gate B for post-merge pipeline. Structured as a 4-step sequential pipeline. Shows growing ecosystem of workflow plugins."
        },
        {
          "id": 77709,
          "title": "Add settings example: official marketplace only",
          "url": "https://github.com/anthropics/claude-code/pull/77709",
          "status": "open",
          "author": "hangnality",
          "description": "Adds an example settings file demonstrating `strictKnownMarketplaces` with an official Anthropic marketplace entry. Useful for enterprise deployments that want to restrict plugin sources to vetted repositories only."
        },
        {
          "id": 77705,
          "title": "fix(plugin-dev): validate-settings.sh false-passes marker check on files with no frontmatter",
          "url": "https://github.com/anthropics/claude-code/pull/77705",
          "status": "open",
          "author": "andyleeboo",
          "description": "Fixes a validation script bug where files without any `---` markers incorrectly pass the frontmatter check, emitting a raw Bash error instead of failing gracefully. Prevents malformed plugin settings from being published silently."
        }
      ],
      "feature_request_trends": [
        {
          "trend": "VS Code IDE integration parity",
          "details": "The most recurring theme is the desire for VS Code extension to match the TUI experience. Specific asks include: diff review UI (#33932, 150👍), `/workflows` command support (#74585, #75146), and inline prompt editing. The community expects a first-class IDE experience, not a reduced-feature port.",
          "top_issues": [
            "https://github.com/anthropics/claude-code/issues/33932",
            "https://github.com/anthropics/claude-code/issues/74585",
            "https://github.com/anthropics/claude-code/issues/75146"
          ]
        },
        {
          "trend": "Configurable limits and safeguards for agent costs",
          "details": "Multiple issues request configurable depth limits for subagent spawning, configurable auto-compact thresholds (#70681), and cost caps or kill-switches for runaway agent loops. The series of cost-incident reports ($$$600, $27.60, 800K tokens) has made this a trust-and-safety priority.",
          "top_issues": [
            "https://github.com/anthropics/claude-code/issues/70681",
            "https://github.com/anthropics/claude-code/issues/72732",
            "https://github.com/anthropics/claude-code/issues/69578"
          ]
        },
        {
          "trend": "Cowork project usability improvements",
          "details": "Users want finer-grained control over Cowork project context: removing folders without reconfiguration (#40043, 55👍), better directory tree visualization, and persistent workspace state across sessions.",
          "top_issues": [
            "https://github.com/anthropics/claude-code/issues/40043"
          ]
        },
        {
          "trend": "MCP reliability and transparency",
          "details": "Growing demand for MCP connector health monitoring, tool inventory visibility, and a solution to the 256-tool cap (#77704). The remote-control permission-surface bug (#60385) also highlights the need for consistent UX across web and TUI.",
          "top_issues": [
            "https://github.com/anthropics/claude-code/issues/77704",
            "https://github.com/anthropics/claude-code/issues/60385"
          ]
        }
      ],
      "developer_pain_points": [
        {
          "pain_point": "Runaway subagent costs with no safeguards",
          "frequency": "Very High (6+ open issues, multiple cost incidents)",
          "details": "The #1 pain point this week. Subagents recursively spawn without depth limits, ignore disable flags, and burn thousands of tokens. Multiple users report real monetary losses ($27, $600+). The community is demanding hard caps, kill switches, and better visibility into agent tree depth.",
          "representative_issues": [
            "https://github.com/anthropics/claude-code/issues/68619",
            "https://github.com/anthropics/claude-code/issues/69578",
            "https://github.com/anthropics/claude-code/issues/72732",
            "https://github.com/anthropics/claude-code/issues/77834"
          ]
        },
        {
          "pain_point": "Silent data loss and file corruption",
          "frequency": "High (3+ critical data-loss reports)",
          "details": "A cluster of bugs causes silent data loss: Windows `rm -rf` traversing NTFS junctions (800 GB reported lost), Cowork tools truncating files silently, and model overwriting user's Confluence pages despite explicit instructions. These erode trust in autonomous file operations.",
          "representative_issues": [
            "https://github.com/anthropics/claude-code/issues/75275",
            "https://github.com/anthropics/claude-code/issues/53940",
            "https://github.com/anthropics/claude-code/issues/75685"
          ]
        },
        {
          "pain_point": "Session state management: fork/resume conflicts",
          "frequency": "Moderate-High (3 open issues)",
          "details": "Multiple issues report that `--continue` or `--resume` does not check if a session is already live, leading to two processes acting on the same session concurrently. This causes conflicting writes, lost work, and headless orphan processes burning tokens.",
          "representative_issues": [
            "https://github.com/anthropics/claude-code/issues/69364",
            "https://github.com/anthropics/claude-code/issues/75761",
            "https://github.com/anthropics/claude-code/issues/77463"
          ]
        },
        {
          "pain_point": "MSYS2/PowerShell tooling issues on Windows",
          "frequency": "Moderate (3 open issues)",
          "details": "Windows-specific tooling bugs continue to frustrate developers: PowerShell script blocks bypassing allowlists (#74916), destructive-path guard mis-parsing tokens (#69461), and forced spell-checking with no disable option (#58693). The Windows experience lags behind macOS and Linux.",
          "representative_issues": [
            "https://github.com/anthropics/claude-code/issues/74916",
            "https://github.com/anthropics/claude-code/issues/69461",
            "https://github.com/anthropics/claude-code/issues/58693"
          ]
        },
        {
          "pain_point": "MCP permission prompt failures in remote/web scenarios",
          "frequency": "Moderate (2 issues, one with 20 comments)",
          "details": "MCP permission prompts do not surface in the web UI for remote-control sessions (#60385), and custom remote MCP connectors lose tools due to a 256-cap regression (#77704). Both block non-trivial MCP usage and create a poor developer experience for remote teams.",
          "representative_issues": [
            "https://github.com/anthropics/claude-code/issues/60385",
            "https://github.com/anthropics/claude-code/issues/77704"
          ]
        }
      ]
    }
  }
}
```

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-16

## Today’s Highlights

Three new Rust-based alpha releases (v0.145.0-alpha.13–15) landed, while the community continues to surface critical Windows stability issues, including a crash-loop on ARM64 and serialport native-module failures. The most upvoted topic remains the missing context/token usage indicator in Codex Desktop, and OpenAI merged several high-impact PRs focused on memory migration for external agents, Cursor setup import, and improved dangerous-command detection.

## Releases

- **rust-v0.145.0-alpha.13**, **alpha.14**, **alpha.15** — Three consecutive alpha releases of the Codex CLI Rust version. No detailed changelog was provided; these are likely incremental fixes or feature preparations for the upcoming stable release.  
  [View releases](https://github.com/openai/codex/releases)

## Hot Issues (Top 10 Noteworthy)

1. **[#23794 – Codex Desktop no longer shows visible context/token usage indicator](https://github.com/openai/codex/issues/23794)**  
   *Closed* · 172 comments · 170 👍  
   The most active issue today. Users on Windows and Mac report the removal of the token/context bar after an update. High community engagement signals this is a critical UX regression.

2. **[#33381 – Windows ARM64 app crash-loops on launch](https://github.com/openai/codex/issues/33381)**  
   *Open* · 38 comments · 25 👍  
   The ARM64 desktop app crashes 10–15 seconds after launch due to missing N-API symbols in the bundled serialport addon. Affects all ARM64 Windows users.

3. **[#28969 – Add setting to disable auto-resolve in 60 seconds for questions](https://github.com/openai/codex/issues/28969)**  
   *Open* · 37 comments · 124 👍  
   Strong demand for an opt-out of the 60-second auto-resolve timer in the CLI. Users working on complex tasks want to prevent premature resolution.

4. **[#31846 – GPT-5.3 Codex Spark fails with "Unsupported parameter: reasoning.summary"](https://github.com/openai/codex/issues/31846)**  
   *Open* · 29 comments · 33 👍  
   GPT-5.3 Spark model refuses to accept standard parameters; suspected API compatibility issue between model versions.

5. **[#33375 – Repeated serialport.node delay-load failures cause severe UI lag](https://github.com/openai/codex/issues/33375)**  
   *Open* · 25 comments · 14 👍  
   Windows x64 users experience severe lag as the app repeatedly attempts to load an incompatible native module. Related to #33381.

6. **[#30178 – In-app Browser crashes the main app during webview navigation](https://github.com/openai/codex/issues/30178)**  
   *Open* · 19 comments · 1 👍  
   Navigation in the built-in browser tab causes the entire Codex Desktop to exit without error. Affects Windows builds.

7. **[#30813 – CLI /agent lists subagents but provides no thread selector](https://github.com/openai/codex/issues/30813)**  
   *Open* · 10 comments · 5 👍  
   The `/agent` command shows active subagents but does not allow users to switch between them, limiting multi-agent workflows.

8. **[#32782 – GPT-5.6 Sol root exposes spawn_agent without agent_type](https://github.com/openai/codex/issues/32782)**  
   *Open* · 8 comments · 9 👍  
   Custom agent routing breaks on GPT-5.6 Sol because the spawned agent schema omits the `agent_type` field, preventing selection of configured agents.

9. **[#33450 – Windows app spawns 12–13 git.exe processes per second](https://github.com/openai/codex/issues/33450)**  
   *Open* · 2 comments · 1 👍  
   Newly reported performance bug: the desktop app enters a loop creating invalid empty `.git` directories and spawning excessive git processes.

10. **[#28349 – Cannot login to work Codex account anymore](https://github.com/openai/codex/issues/28349)**  
    *Open* · 5 comments  
    Enterprise users reported login failures due to phone number verification requirements. No workaround yet.

## Key PR Progress (Top 10 Important)

1. **[#33467 – Remove template IDs from MCP tool call metadata](https://github.com/openai/codex/pull/33467)**  
   *Closed* · copyberry[bot]  
   Cleanup of deprecated template identifiers across MCP protocol, app-server, and TypeScript SDK.

2. **[#33464 – Strengthen forced `rm` command detection](https://github.com/openai/codex/pull/33464)**  
   *Closed* · copyberry[bot]  
   Improves dangerous-command heuristics to catch forced `rm` inside complex shell syntax and wrapper variants.

3. **[#33455 – fix(core) expand is_dangerous_command (backport to 0.144)](https://github.com/openai/codex/pull/33455)**  
   *Closed* · dylan-hurd-oai  
   Cherry-picks seven commits enabling dangerous-command detection in danger-full-access mode and adding literal Bash parsing for more forced `rm` patterns.

4. **[#33459 – Allow more time for image generation in code mode](https://github.com/openai/codex/pull/33459)**  
   *Closed* · copyberry[bot]  
   Increases the yield timeout to 120 seconds for image generation, preventing premature timeouts in code-mode workflows.

5. **[#33457 – Use final answers in turn history summaries](https://github.com/openai/codex/pull/33457)**  
   *Closed* · copyberry[bot]  
   Improves summary accuracy by tracking only `final_answer` phase messages and falling back appropriately.

6. **[#33456 – Move external agent migration into its crate](https://github.com/openai/codex/pull/33456)**  
   *Closed* · copyberry[bot]  
   Refactors migration logic into a dedicated `codex-external-agent-migration` crate for better separation.

7. **[#33454 – Track prompt cache write token usage](https://github.com/openai/codex/pull/33454)**  
   *Closed* · copyberry[bot]  
   Adds `cache_write_input_tokens` to usage events, enabling users and tools to see cached prompt savings.

8. **[#33444 – Add external agent memory migration](https://github.com/openai/codex/pull/33444)**  
   *Closed* · copyberry[bot]  
   Feature-gated migration for project‑level Markdown memory files into the Codex memory extension workspace, with rename/delete detection.

9. **[#33426 – Add Cursor support to setup import](https://github.com/openai/codex/pull/33426)**  
   *Closed* · copyberry[bot]  
   Expands the `/import` flow to detect and import settings, MCP servers, hooks, agents, and chat sessions from Cursor (in addition to Claude Code).

10. **[#31781 – Bound executor-controlled HTTP response buffering](https://github.com/openai/codex/pull/31781)**  
    *Open* · jif-oai · *code-reviewed*  
    Security hardening: limits the total buffered response size from remote exec-servers to prevent memory exhaustion via large frames.

## Feature Request Trends

- **Context/Token visibility** – Multiple requests to restore or improve the token usage indicator in the desktop app (Issue #23794).
- **Auto-resolve control** – Strong support for a setting to disable the 60-second auto-resolve timer in CLI (Issue #28969).
- **Full context window for GPT-5.6 Sol** – Users want an opt-in setting to use the full 1.05M context and configure manual compaction (Issue #33306).
- **Custom agent routing** – Demand for stable `agent_type` exposure in spawning APIs to allow custom agent selection (Issues #32782, #31097).
- **Better SSH remote support** – Fixes for keyboard-interactive authentication, symlink‑based remote projects, and “No chats” visibility (Issues #23037, #30808, #27284).
- **Windows ARM64 stability** – Multiple crash and lag reports are pushing for a robust native module strategy (Issues #33381, #33375, #33429, #33119).

## Developer Pain Points

- **Windows native module incompatibility** – Serialport and N-API symbols are repeatedly causing launch crashes, UI lag, and delayed-load failures across Windows x64 and ARM64.
- **Git abuse in Windows app** – Issue #33450 highlights a continuous loop of `git.exe` processes and empty directory creation, causing severe resource drain.
- **SSH authentication gaps** – The desktop app cannot handle keyboard-interactive/PAM factors and fails on symlinked remote projects.
- **False version‑required prompts** – Users on the latest build are told to update (Issue #31826), creating confusion.
- **Missing context indicators** – The removal of the token/context bar (#23794) remains the highest‑friction UX regression.
- **Enterprise login issues** – Phone verification blocks login without alternative flows, affecting Enterprise users.
- **Multi‑agent control limitations** – CLI lacks thread selection for subagents, and GPT-5.5/5.6 enforce MultiAgentV2 or omit agent_type, breaking custom configurations.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-07-16

## Today’s Highlights
A critical fix was merged to prevent the severe **400 Bad Request** that broke chat continuity after cancelling tool calls. A **security patch** for a variable expansion bypass (GHSA-wpqr-6v78-jr5g) was also submitted, alongside a faster MCP tools discovery timeout to avoid CLI freezes at startup. The nightly release `v0.52.0-nightly.20260716` bundles these improvements.

## Releases
**v0.52.0-nightly.20260716.g3ff5ba20f**  
- Fix: groups cancelled tool responses and coalesces consecutive roles to prevent `400 Bad Request` (PR #28407)  
- Automated version bump from previous nightly (#28402)  
[Release details](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260716.g3ff5ba20f)

## Hot Issues (Top 10 by activity & impact)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) – Subagent recovery after MAX_TURNS reported as GOAL success**  
   *Status: Open, 10 comments, 2 👍*  
   A `codebase_investigator` subagent falsely reports success after hitting its turn limit, hiding the interruption. Community calls for clearer termination reasons.

2. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) – Zero-Dependency OS Sandboxing for bash affinity**  
   *Status: Open, 8 comments, 1 👍*  
   Proposal to leverage Gemini 3’s native bash skills via lightweight sandboxing. High potential for safer and more capable codebase exploration.

3. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) – Robust component-level evaluations**  
   *Status: Open, 7 comments*  
   EPIC following up on behavioral evals (76 tests so far). Need more structured evaluation of sub-agent and tool performance.

4. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) – Generalist agent hangs forever**  
   *Status: Open, 7 comments, 8 👍*  
   Repeated reports: instructing the model not to defer to subagents works around the hang. High community frustration (top 👍 count).

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) – Gemini does not use custom skills and sub-agents enough**  
   *Status: Open, 6 comments*  
   Anecdotal but consistent – even when skills are well-described, the main agent rarely invokes them autonomously.

6. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) – Shell command execution stuck with “Waiting input” after completion**  
   *Status: Open, 4 comments, 3 👍*  
   After executing simple CLI commands, the shell state remains active and waiting, blocking further interaction.

7. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) – Browser subagent fails on Wayland**  
   *Status: Open, 4 comments, 1 👍*  
   Linux Wayland users cannot use the browser agent; termination reason shows GOAL but with error.

8. **[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) – Symlinked agent files not recognized**  
   *Status: Open, 4 comments*  
   `~/.gemini/agents/` ignores symlinked markdown files, breaking workflows that rely on symlinks.

9. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) – Auto Memory retries low-signal sessions indefinitely**  
   *Status: Open, 5 comments*  
   Sessions judged low-signal are never marked as processed, causing repeated re-extraction attempts.

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) – Agent should discourage destructive behavior**  
    *Status: Open, 3 comments, 1 👍*  
    The model occasionally uses `git reset --force` or similar dangerous commands when safer alternatives exist.

## Key PR Progress (Top 10 by importance & recency)

1. [**#28407**](https://github.com/google-gemini/gemini-cli/pull/28407) – `fix(core,a2a): group cancelled tool responses and coalesce consecutive roles`  
   *Merged* – Fixes the 400 Bad Request after cancelling tool calls. Critical for chat continuity.

2. [**#28410**](https://github.com/google-gemini/gemini-cli/pull/28410) – `fix(core): shorten MCP tools/list discovery timeout`  
   *Open* – Prevents silent 10-minute freeze when MCP server doesn’t respond correctly.

3. [**#28403**](https://github.com/google-gemini/gemini-cli/pull/28403) – `fix(core): block $VAR and ${VAR} variable expansion bypass`  
   *Open* – Security fix for GHSA-wpqr-6v78-jr5g. Blocks another vector for secret exfiltration.

4. [**#28405**](https://github.com/google-gemini/gemini-cli/pull/28405) – `fix: prevent scroll position jump during content updates`  
   *Open* – Fixes #5009: user scroll-up review interrupted by auto-scroll reset.

5. [**#28406**](https://github.com/google-gemini/gemini-cli/pull/28406) – `fix(availability): apply modelIdResolutions to tool sub-agent model configs`  
   *Open* – Ensures API-key users without preview access don’t get `INVALID_MODEL` errors for web-search, web-fetch, etc.

6. [**#28164**](https://github.com/google-gemini/gemini-cli/pull/28164) – `fix(core): limit recursive reasoning turns per single user request`  
   *Open* – Caps recursive reasoning at 15 turns (configurable) to protect local CPU and API quotas from infinite loops.

7. [**#28408**](https://github.com/google-gemini/gemini-cli/pull/28408) – `refactor(cli): centralize dense payload detection in tool mapping`  
   *Open* – Moves complex detection logic out of UI components, simplifying frontend and reducing backend data coupling.

8. [**#28386**](https://github.com/google-gemini/gemini-cli/pull/28386) – `fix(vscode): track activation disposables`  
   *Open* – Fixes #27790: comma expressions causing missed disposables in VS Code companion activation.

9. [**#28409**](https://github.com/google-gemini/gemini-cli/pull/28409) – `chore(caretaker): update vitest to v3.2.4 and add package-lock.json files`  
   *Open* – Standardises test runner version and adds missing lockfiles for caretaker-agent services.

10. [**#28305**](https://github.com/google-gemini/gemini-cli/pull/28305) – `feat(evals): add tool call formatter and integrate failure summaries`  
    *Open* – Enhances behavioral evals with a numbered timeline of tool calls on failure, improving debuggability.

## Feature Request Trends
- **Agent self-awareness & introspection** – Several requests for the CLI to understand its own flags, hotkeys, and subagent trajectories so it can be its own guide (e.g., `#21432`, `#22598`).
- **AST-aware tools** – Investigations into AST-driven file reads, search, and codebase mapping to reduce token waste and improve subagent precision (`#22745`, `#22746`).
- **Better eval & testability** – Demand for component-level evals and failure summaries to validate subagent behaviour (`#24353`, `#28305`).
- **Destructive operation safeguards** – Need for the agent to avoid or warn before using `git reset --force`, `rm -rf`, etc. (`#22672`).
- **Memory system improvements** – Requests for deterministic redaction, quarantine of invalid patches, and avoiding infinite retries on low-signal sessions (`#26522`, `#26523`, `#26525`).

## Developer Pain Points
- **Agent hangs and freezes** – Generalist agent hangs forever (`#21409`); shell commands stuck on “Waiting input” (`#25166`); MCP tools discovery freeze at startup (PR #28410).
- **400 errors after cancelling tools** – Previously required new chat sessions; now fixed by PR #28407.
- **Tool overload** – >128 tools cause 400 errors; agent doesn’t scope tools intelligently (`#24246`).
- **Subagent configuration ignored** – Browser agent ignores `settings.json` overrides (`#22267`); agents running without permission (`#22093`); symlinked agent files not recognised (`#20079`).
- **Terminal & rendering issues** – Flicker on resize (`#21924`); scroll jump when user scrolls up (`#28405`); emoji split when truncating display strings (PR #28224).
- **Security concerns** – Variable expansion bypass (GHSA-wpqr-6v78-jr5g); secrets logged before redaction (`#26525`).
- **Inconsistent subagent behaviour** – Subagents don’t use custom skills automatically (`#21968`); false success reporting on max turns (`#22323`); browser agent fails on Wayland (`#21983`).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-16

## Today’s Highlights
A patch release (v1.0.71) fixes a hang in `copilot -p --autopilot` with long-lived background processes, and improves settings validation on startup. The issue tracker is dominated by MCP authentication and tool-discovery bugs, with three separate reports about Atlassian MCP OAuth failures failing to surface tools. A high-priority data-loss bug (arrow key hijacking) was filed today.

## Releases
**v1.0.71** (2026-07-16)
- `copilot -p --autopilot` no longer hangs when a background shell/agent outlives a turn; now respects `COPILOT_TASK_WAIT_TIMEOUT_SECONDS` like plain `-p`.
- Reopening the `/subagents` model picker preserves each agent’s reasoning effort and context tier.
- **v1.0.71-3** — Two fixes:
  - Invalid `settings.json` now shows a warning identifying the offending value instead of silently ignoring.
  - `/terminal-setup` no longer skips setup on terminals without real Kitty keyboard support.

## Hot Issues (Top 10 by relevance & community activity)
1. **#223** — *“Copilot Requests” permission for fine-grained tokens should be visible for org-owned tokens*  
   Author: RyanHecht | 👍 76, 💬 31  
   🔗 [Issue #223](https://github.com/github/copilot-cli/issues/223)  
   Enterprise users cannot restrict automations to org-owned tokens. High demand for clearer permission scoping.

2. **#1477** — *“Continuing autonomously (3 premium requests)” after model completion*  
   Author: joshlacal | 👍 18, 💬 11  
   🔗 [Issue #1477](https://github.com/github/copilot-cli/issues/1477)  
   Users confused about premium request billing—free tier model seems to be “autopilot” charging unexpectedly.

3. **#4024** — *Voice mode: all bundled ASR models fail silently (Nemotron RNNT routing bug)*  
   Author: sylvanc | 👍 0, 💬 8  
   🔗 [Issue #4024](https://github.com/github/copilot-cli/issues/4024)  
   `/voice` records audio but returns empty transcription for all three ASR models. Critical for voice users.

4. **#4096** — *Third-party MCP server shows “Connected” but tools missing from CLI sessions*  
   Author: bugale | 👍 2, 💬 5  
   🔗 [Issue #4096](https://github.com/github/copilot-cli/issues/4096)  
   OAuth bridge between app UI and CLI sessions is broken. Multiple duplicates (#4086, #4089).

5. **#1979** — *Remote session support – attach from mobile/browser*  
   Author: DwainTR | 👍 53, 💬 4  
   🔗 [Issue #1979](https://github.com/github/copilot-cli/issues/1979)  
   Feature request: ability to connect to running CLI sessions remotely. Strong community support, similar to Claude Code.

6. **#4016** — *BYOK (COPILOT_PROVIDER_*) still rejected in `--acp` mode*  
   Author: gwexler-msft | 👍 3, 💬 2  
   🔗 [Issue #4016](https://github.com/github/copilot-cli/issues/4016)  
   Regression: custom providers work in `-p` but fail in `--acp` with authentication error. Affects enterprise BYOK setups.

7. **#2052** — *Persistent token/context usage indicator*  
   Author: orenMicrosoft | 👍 19, 💬 3  
   🔗 [Issue #2052](https://github.com/github/copilot-cli/issues/2052)  
   Request for an always-visible status bar showing token consumption and context window usage. High upvotes.

8. **#4147** — *High priority: bare left/right arrow hijacks cursor key for session navigation, discarding input*  
   Author: NedAnd1 | 👍 0, 💬 0 (filed today)  
   🔗 [Issue #4147](https://github.com/github/copilot-cli/issues/4147)  
   Data-loss bug: arrow keys used for session switching, causing input loss. Triaged as high priority.

9. **#4097** — *apply_patch stores deleted binary in session history, permanently exceeding 5 MB limit*  
   Author: Adamkadaban | 👍 1, 💬 2  
   🔗 [Issue #4097](https://github.com/github/copilot-cli/issues/4097)  
   Large binary diffs inflate conversation history; `/compact` cannot recover. Blocks long sessions.

10. **#4034** — *Hook subprocess stdin write-end left open – $(cat) pattern hangs*  
    Author: jens-f | 👍 0, 💬 3  
    🔗 [Issue #4034](https://github.com/github/copilot-cli/issues/4034)  
    Tool-use hooks never send EOF, breaking documented `$(cat)` pattern. Fix needed for custom hooks.

## Key PR Progress
No pull requests were updated in the last 24 hours. The maintainers appear focused on bug fixing and triage; patches are being delivered directly via releases.

## Feature Request Trends
- **Remote/attachable sessions** (#1979, 53 👍) – community strongly wants mobile or web connectivity.
- **Better context & token visibility** (#2052, 19 👍) – always-on status bar for token usage.
- **Larger context windows** – multiple closed issues (#1610, #2785) asking for 1M context on Opus models; still a popular ask.
- **Configurable agent MCP tools** (#4076, 2 comments) – ability to give built-in research agents access to custom MCP servers.
- **Interactive input variables for plugins** (#4042) – `${input:...}` support in `.mcp.json` for secure plugin configuration.

## Developer Pain Points
- **MCP authentication failures** dominate: OAuth-connected servers show “Connected” but no tools appear (#4096, #4086, #4089). Multiple reports across Atlassian, Work IQ, and custom servers.
- **BYOK regression in `--acp` mode** (#4016) – enterprise users relying on custom providers cannot use the `--acp` workflow.
- **Data-loss bugs** – arrow key hijacking (#4147), whitespace collapsing in chat composer (#4136), and deletion of voice dictation if typing during finalize window (#3896).
- **Session state corruption** – large binary deletions permanently bloat conversation history (#4097); duplicate Docker stdio MCP servers on `/resume` (#4049).
- **Hook/stdin semantics** – missing EOF on tool-use hooks (#4034) breaks community hook patterns.
- **TUI hangs on NFS/GPFS** (#4053) – SIGCHLD race condition causes indefinite “Loading: N skills” on distributed filesystems.

---

*Next digest: 2026-07-17 | Data source: [github.com/github/copilot-cli](https://github.com/github/copilot-cli)*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-07-16**

**Today’s Highlights**  
Activity on the Kimi CLI repository was minimal today, with no new releases or issues filed in the last 24 hours. The sole pull request update is PR #2500, which focuses on aligning Python telemetry with the TypeScript rewrite’s event registry and adding trace ID capture—a step toward improved observability and cross‑platform consistency.

**Releases**  
None in the last 24 hours.

**Hot Issues**  
No issues were updated or created in the last 24 hours.

**Key PR Progress**  
1. [#2500 [OPEN] feat(telemetry): align events with TS schema, add trace_id and missing events](https://github.com/MoonshotAI/kimi-cli/pull/2500)  
   *Author: 7Sageer* – Aligns the Python telemetry surface with the `agent-core-v2` `events.ts` schema. Introduces capture of the `x-trace-id` response header for both stream and non‑stream Kimi provider calls, enabling end‑to‑end request tracing. No associated tracking issue; community has not yet commented.

**Feature Request Trends**  
No feature requests were visible in the data for this period.

**Developer Pain Points**  
No recurring pain points or high‑frequency requests surfaced in the last 24 hours.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-16

## Today's Highlights

A patch release (v1.18.2) shipped with critical fixes for subagent behaviour and new tab shortcuts, but the community remains frustrated by the aggressive desktop layout overhaul that has hidden the Plan/Build mode toggle and made session titles unreadable. Meanwhile, several PRs landed to fix overflow timing gaps, web‑fetch permission scoping, and desktop crash on WSL – signalling an active push to stabilise both the v1.18 line and the upcoming V2 branch.

## Releases

**[v1.18.2](https://github.com/anomalyco/opencode/releases/tag/v1.18.2)**  
- **Core bugfixes:** subagents no longer spawn nested subagents by default; added `subagent_depth` config limit. Improved default reasoning depth for Meta models.  
- **Desktop improvements:** `Mod+N` now opens a new tab. No UI layout changes in this patch.

## Hot Issues

1. **[#36936](https://github.com/anomalyco/opencode/issues/36936) – Desktop tab titles don’t fit in new layout**  
   Screenshots show session titles truncated beyond usability. Reverting to v1.17 fixes it. 14 comments, 11 👍 – highest engagement today.

2. **[#36997](https://github.com/anomalyco/opencode/issues/36997) – New layout hides Plan/Build mode toggle**  
   The `newLayoutDesigns: true` flag removes the agent switching UI entirely. Users cannot see which agent is active or switch modes. Tab key also affected.

3. **[#24038](https://github.com/anomalyco/opencode/issues/24038) – Claude support via ACP protocol (closed)**  
   Feature request for Agent Client Protocol support got traction; closed but referenced by other issues.

4. **[#37063](https://github.com/anomalyco/opencode/issues/37063) – Chat history lost after upgrade to v1.18.1**  
   User reports ~1100 chat sessions missing after updating from v1.17.18. 5 comments, no solution listed.

5. **[#37158](https://github.com/anomalyco/opencode/issues/37158) – Plan/Build mode button disappeared (closed)**  
   Duplicate of #36997; merged quickly but highlights the scale of the layout backlash.

6. **[#37144](https://github.com/anomalyco/opencode/issues/37144) – Custom no‑auth providers (e.g. LM Studio) dropped in V2 config**  
   Providers without `env` are silently ignored; only three built‑in LM Studio models appear. Blocks local‑first workflows.

7. **[#32656](https://github.com/anomalyco/opencode/issues/32656) – Compaction output‑budget reservation capped at 20K for `limit.input` models**  
   Undersized reservation risks overflow. Has 3 comments, still open.

8. **[#17340](https://github.com/anomalyco/opencode/issues/17340) – Session compaction fails with “context exceeds model limit”**  
   Models with 128k context overflow before compaction triggers. Long‑standing issue (opened March 2026).

9. **[#37171](https://github.com/anomalyco/opencode/issues/37171) – Desktop crashes on restart: “Notification server not found: wsl:Ubuntu”**  
   Renderer fails to load when WSL notification server is unavailable. Fixed by PR #37190.

10. **[#30337](https://github.com/anomalyco/opencode/issues/30337) – `.opencode/node_modules/` causes startup hang**  
    Scanner does not skip `node_modules` despite .gitignore; freeze on projects containing an `opencode` directory.

## Key PR Progress

1. **[#37194](https://github.com/anomalyco/opencode/pull/37194) – Fix session overflow detection timing gaps**  
   Fixes pending‑context miss, output‑budget cap, missing overflow checks after large tool outputs, and silent compaction stops. Closed.

2. **[#37129](https://github.com/anomalyco/opencode/pull/37129) – Default advanced features for new users**  
   Hides file tree, search, status, and agent selection on fresh installs; enables them for existing profiles. Closed.

3. **[#37198](https://github.com/anomalyco/opencode/pull/37198) – Show selector for custom agents**  
   Forces agent selector visible when project has selectable custom agents; resolves to build agent when hidden. Closed.

4. **[#37182](https://github.com/anomalyco/opencode/pull/37182) – Scope WebFetch always‑allow to domain**  
   Replaces wildcard `*` with origin‑scoped pattern. Adds unit tests. Closed.

5. **[#37190](https://github.com/anomalyco/opencode/pull/37190) – Handle unavailable notification server during init**  
   Adds fallback state for WSL environments – fixes crash #37171. Open.

6. **[#37192](https://github.com/anomalyco/opencode/pull/37192) – Support dynamic Effect tools in V2 plugins**  
   Allows external plugins to register tools without importing opaque host module. Open.

7. **[#36752](https://github.com/anomalyco/opencode/pull/36752) – Fix cache write tokens from raw usage**  
   Anthropic models via OpenAI gateways now report `cache.write` correctly. Open.

8. **[#36850](https://github.com/anomalyco/opencode/pull/36850) – Normalize Cloudflare Workers AI mixed content types**  
   Fixes 400 errors when message content types vary. Open.

9. **[#35311](https://github.com/anomalyco/opencode/pull/35311) – Multiple clones of same repo treated as different projects**  
   Closes 14 related issues. Still open after 12 days.

10. **[#37181](https://github.com/anomalyco/opencode/pull/37181) – Select system prompts through plugins**  
    Moves per‑provider prompt selection into granular built‑in plugins; consolidates GPT/Codex, restores Muse Spark. Closed.

## Feature Request Trends

- **Desktop layout flexibility:** Vertical tabs ([#36942](https://github.com/anomalyco/opencode/issues/36942)), auto‑generated session titles ([#30926](https://github.com/anomalyco/opencode/issues/30926)), and a built‑in file editor ([#26970](https://github.com/anomalyco/opencode/issues/26970)) are top‑voted community asks.
- **Per‑session MCP selection:** Multiple requests for `serve`/`attach` to allow per‑client MCP toggling ([#37168](https://github.com/anomalyco/opencode/issues/37168)).
- **Image display from tool results:** High demand (7 👍) for showing images returned by `webfetch` or MCP servers in the chat UI ([#21227](https://github.com/anomalyco/opencode/issues/21227)).
- **IME bypass for leader key:** Needed for Chinese and other IME users ([#37167](https://github.com/anomalyco/opencode/issues/37167)).

## Developer Pain Points

- **Layout changes breaking workflows:** The new desktop UI (v1.18.x) has hidden the Plan/Build mode toggle, truncated tab titles, and caused widespread confusion. Three duplicate issues were raised in one day.
- **Session compaction failures:** Multiple open issues (e.g., #13946, #14562, #17340, #32656) describe sessions that overflow despite compaction, often stuck on large tool outputs or image attachments. The 20K output‑budget cap and missing overflow checks are recurring sources of frustration.
- **Provider configuration friction:** Custom LM Studio and other local providers are silently dropped in V2 ([#37144](https://github.com/anomalyco/opencode/issues/37144)); the hardcoded model list doesn’t match user installations.
- **Data loss on upgrade:** At least one user lost all chat history after updating from v1.17.18 to v1.18.1 ([#37063](https://github.com/anomalyco/opencode/issues/37063)).
- **Prompt injection risks:** User‑injected instructions and file contents lack boundary markers, making the system vulnerable to injected commands ([#37187](https://github.com/anomalyco/opencode/issues/37187)).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-07-16

## 1. Today’s Highlights
The OpenAI Codex connection reliability remains a top concern, with issue #4945 continuing to draw community attention (30 👍, 75 comments). A critical Windows fix landed in PR #6692 to resolve `spawn("taskkill")` failures on Node.js 24, and a new proposal (#6688) highlights TUI extension selector windowing issues. The community also advanced several feature requests including session management and extension streaming hooks.

## 2. Releases
No new releases in the last 24 hours. Latest stable remains **0.80.7**.

## 3. Hot Issues (10 noteworthy)

1. **#4945 – openai-codex Connection Reliability Issues**  
   *TUI gets stuck on “Working…” with no streaming or errors; only Escape recovers.*  
   High engagement (75 comments, 30 👍). Indicates a fragile integration with the Codex backend.

2. **#6050 – TUI full redraw clears terminal scrollback during rendering**  
   *Scrollback jumps to chat beginning during interactive mode.*  
   14 comments; core renderer bug affecting user experience.

3. **#5263 – Make in-session model/thinking-level changes ephemeral by default**  
   *Proposes ephemeral changes with explicit `/settings` default entry.*  
   7 comments, 7 👍. Strong community support for cleaner UX.

4. **#6657 – Bedrock AWS_PROFILE authentication not working (inprogress)**  
   *AccessDeniedException: 403 persists despite claimed fix in 0.80.7.*  
   Ongoing regression affecting AWS Bedrock users.

5. **#6686 – Pi automatically logs out of GitHub**  
   *Regression from #2725; affects macOS and Linux, interrupts agent mid-turn.*  
   High severity; 4 comments, no official fix yet.

6. **#6619 – On Windows dependent extensions mislabeled with absolute path**  
   *Banner shows absolute paths when installing npm packages with dependencies.*  
   4 comments, inprogress; Windows-specific package management issue.

7. **#6673 – OpenAI Codex exposes raw Cloudflare 520 HTML with client IP**  
   *Security vulnerability: user IP visible in error messages.*  
   Closed but urgent: 3 comments, sensitive data leak.

8. **#6647 – Compaction fails on single transient stream drop (no retry)**  
   *Compaction summarization has no retry; transient failure kills whole operation.*  
   2 comments, inprogress; affects long-running sessions.

9. **#6688 – Extension selector renders all options without viewport windowing**  
   *`ctx.ui.select()` can’t scroll; options go off-screen.*  
   Closed as untriaged but noted as UX regression for extension developers.

10. **#6685 – Intermittent failure to execute tool calls & display thinking blocks**  
    *Model output correct at provider but harness drops events; recovers only after restart.*  
    Critical reliability bug affecting all providers.

## 4. Key PR Progress (10 important PRs)

1. **#6692 – fix: use absolute System32 path for taskkill/rundll32**  
   *Resolves ENOENT on Node.js 24 Windows by using absolute paths and proper error handling.*  
   Direct fix for #6596; merged.

2. **#6681 – windows: reset pi terminal title after checking npm packages**  
   *Narrow fix for #6629; reverts title change after `npm view`.*  
   Merged; improves Windows daily experience.

3. **#6651 – feat: add xAI device OAuth and route grok-4.5 through Responses**  
   *Adds OAuth alongside `XAI_API_KEY`; routes grok-4.5 with reasoning levels.*  
   Open, targets #6461; expands provider support.

4. **#6671 – add usage info to branch summary, compaction and tool result entries**  
   *Adds usage metadata to key logging entries; missing `usage` in tool events noted.*  
   Open; improves observability.

5. **#6683 – fix: accept colon-qualified skill names**  
   *Plugin-namespaced skills like `inc:ship-it` falsely reported as conflicts.*  
   Merged; fixes extension loading false positives.

6. **#6594 – feat: sqlite session storage**  
   *Adds `retainedTail` to compaction entries; changes path traversal to stop at compaction.*  
   Open; significant performance optimization for session persistence.

7. **#6680 – parse extension package name in case of dependent extension**  
   *Partial fix for #6619 (Windows absolute path banner).*  
   Open; improves Windows extension management.

8. **#6533 – fix: Codex compaction returns “Model not found” for gpt-5.6-luna**  
   *Compaction fails via Codex API for newer models; regular chat works.*  
   Merged; fixes a common workflow interruption.

9. **#6216 – feat: Add Amazon Bedrock Mantle OpenAI Responses provider**  
   *New provider using OpenAI’s Bedrock provider; supersedes previous PR.*  
   Open; expands AWS integration.

10. **#6667 – fix(tui): guard null children in Box and Container render/invalidate**  
    *Prevents `TypeError` crashes after extension install/remove.*  
    Merged; stabilizes TUI during extension lifecycle.

## 5. Feature Request Trends

- **Session management & organization** (#6674, #5263): Users want folders, rename, archive, and ephemeral in-session settings.
- **Extended extension hooks** (#6693, #6684): Demand for `stream_chunk` hook and retry controls for real-time advisor patterns.
- **Enhanced provider support** (#6651, #6216): OAuth and new API endpoints for xAI, Bedrock Mantle.
- **Better developer experience** (#6688, #6682): Windowing for extension selector, improved code block rendering in TUI.

## 6. Developer Pain Points

- **Windows stability** — repeated issues with PATH-dependent commands (#6596, #6629), absolute paths in extension banners (#6619), and terminal title corruption.
- **Codex/OpenAI reliability** — connection drops (#4945), raw error page exposure (#6673), model mismatch in compaction (#6533).
- **Authentication regressions** — GitHub auto-logout (#6686), Bedrock AWS_PROFILE still broken (#6657), ChatGPT OAuth overridden by API key (#6689).
- **TUI rendering & scrollback** — invasive redraws (#6050), null-crashes after extension changes (#6667), selector overflow (#6688).
- **Compaction fragility** — no retry on transient errors (#6647) and repeated auto-compaction loops (#6639).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Okay, here is the Qwen Code community digest for 2026-07-16, structured as requested.

---

### Qwen Code Community Digest — 2026-07-16

#### 1. Today's Highlights
The focus remains on stabilizing the daemon for multi-workspace and channel use, with several fixes for CI flakiness and error handling landing today. The `cua-driver-rs v0.7.2` release introduces relative coordinate support, a key feature for more reliable desktop automation. A long-running RFC for multi-workspace daemon support (#6378) continues to gather community input, while the team is actively merging PRs for channel source metadata and a new "Todo Stop Guard" for background sessions.

#### 2. Releases
Two new releases were published in the last 24 hours:
*   **`cua-driver-rs v0.7.2`**: This is a significant update for the Computer Use Agent (CUA) driver, introducing a "relative-coordinate" fork. It pre-built binaries for macOS (codesigned & notarized), Linux, and Windows. This enables more robust UI automation by allowing agents to interact with UI elements based on their relative position rather than fixed screen coordinates.
    *   [Release Link](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.7.2)
*   **`v0.19.10-nightly.20260716`**: A nightly release with primarily documentation and process improvements, including a PR scoping policy for code reviews.
    *   [Release Link](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.10-nightly.20260716.506ce0a1a)

#### 3. Hot Issues
*   **#6378: RFD: Support multiple workspaces in one `qwen serve` daemon.** With 23 comments, this is the most active discussion. It proposes a major architectural change to the daemon, allowing it to serve multiple isolated workspaces from a single process. This is a foundational feature for enterprise use.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6378)
*   **#6928: GitHub App authentication is not injected into newly created workspaces.** A critical bug reported by a user with a private repo. The workspace mounts but lacks necessary GitHub auth, preventing operations like push/pull. The issue is in Spanish, but the technical diagnosis is clear.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6928)
*   **#5239: Subagent and main session communication is weak.** A detailed Chinese-language report highlights a major pain point: the main session has no reliable way to know when a sub-agent has failed or finished a task. This forces users to implement hacky file-based monitoring, directly impacting the reliability of multi-agent setups.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/5239)
*   **#6936: Managed memory wastes context even when disabled.** An important resource-saving bug. Setting `enableManagedAutoMemory: false` disables memory operations but still injects a 7-9 KB instruction block into every system prompt, wasting valuable context window space. A `welcome-pr` label suggests the team is looking for community help.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6936)
*   **#6443: Improve DingTalk channel with interactive cards.** A feature request to improve the DingTalk (钉钉) integration with interactive cards for agent status and stop buttons. The high community engagement (3 comments) shows demand for richer chat-based agent interactions.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6443)
*   **#6927: Safety classifier persistently fail-closes.** A critical bug where the safety classifier enters a permanent "fail-close" state under `tools.approvalMode = "auto"`, blocking all approval-requiring tools and effectively deadlocking the agent. The user cannot even write files to change settings, needing a full restart.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6927)
*   **#6943: Feature Request + Bug: Add "auto" output language mode.** A popular request to allow the model to dynamically follow the user's input language instead of being locked to a single fixed language. The user points out that the current design is both a missing feature and a bug due to its rigid implementation.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6943)
*   **#6939: WeCom group messages are dropped by an unsupported mention-metadata gate.** A bug report for the WeCom (WeChat Work) channel. The code incorrectly enforces a mention requirement that the WeCom protocol doesn't support, causing all group messages to be silently dropped. This is a major blocker for WeCom users.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6939)
*   **#6898: Shell notification on every tool call is excessive.** A user requests that the interactive shell approval prompt only appear at the end of a task, not after every single tool call. This highlights a critical UX friction point for users who want to automate multi-step processes.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6898)
*   **#6970: MCP tool names with dots are rejected by strict providers.** A compatibility issue where tool names from MCP servers (e.g., `database.query_uniprot`) are used as-is, but are rejected by models using OpenAI/Anthropic-compatible specs, which don't allow dots. This is a key interoperability concern.
    *   [Issue Link](https://github.com/QwenLM/qwen-code/issues/6970)

#### 4. Key PR Progress
*   **#6963: CI(web-shell): before/after visual previews.** A CI improvement that makes visual previews for the Web Shell much more useful by showing only the pixel-diff between the PR and the `main` branch, rather than a full set of screenshots.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6963)
*   **#6945: feat(cli): add daemon Todo stop guard (OPEN).** Implements a highly-requested feature for background automation. This PR prevents a daemon session from stopping after creating a Todo with remaining items, allowing it to continue the work chain for up to two additional rounds.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6945)
*   **#6993: fix(headless): run concurrency-safe tool calls in parallel (OPEN).** Fixes a performance gap where headless mode (`qwen -p`) executed parallel tool calls sequentially. This aligns headless mode's performance with the interactive TUI, significantly speeding up batch operations.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6993)
*   **#6994: feat(review): fold the findings list into the verify/reverse-audit prompt (OPEN).** A prompt engineering improvement for the `qwen review` feature, making the verification prompts cleaner and more effective by consolidating findings into a single block.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6994)
*   **#6954: feat(serve): add workspace MCP management (OPEN).** A major feature for the daemon, adding a UI in the Web Shell for workspace-scoped MCP (Model Context Protocol) server management. This allows users to add/edit/remove MCP tools without restarting the daemon.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6954)
*   **#6953: fix(cli): make auto output language follow user input (OPEN).** Directly addresses the hot issue #6943 by making the `auto` language mode dynamically write a prompt instructing the model to follow the user's input language.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6953)
*   **#6937: feat(cli): mouse text selection and copy in VP mode (OPEN).** A significant UX improvement for the terminal UI (VP mode), adding mouse-driven text selection and copy, mimicking the behavior of a standard GUI terminal.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6937)
*   **#6895: feat(core): propagate trusted invocation context (OPEN).** A key security PR that introduces an immutable invocation context (Ingress, session, prompt, client) for the entire lifecycle of a request. This is foundational for fine-grained permission and trust policies, especially in multi-tenant daemon setups.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6895)
*   **#6961: feat(daemon): Aggregate deep health across workspaces.** A companion PR to the multi-workspace RFC (#6378), allowing the daemon's health endpoint to provide a single, aggregated snapshot of all running workspaces.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6961)
*   **#6950: fix(cli): Preserve channel startup failure details.** Addresses the opacity of channel errors by ensuring that the specific reason for a channel startup failure is propagated and displayed to the user, rather than a generic "exited before ready" message.
    *   [PR Link](https://github.com/QwenLM/qwen-code/pull/6950)

#### 5. Feature Request Trends
The community's feature requests are coalescing around several core themes:
*   **Multi-Workspace & Daemon Management:** The desire for a single daemon to handle multiple isolated projects (#6378) is the dominant architectural request. This is directly tied to the need for better multi-project workflows and team usage.
*   **Smarter & Less Intrusive Automation:** Users are pushing for more sophisticated background automation. This includes the "Todo Stop Guard" (#6946) and requests to aggregate shell notifications to only fire at task completion (#6898).
*   **Richer Channel Integrations:** There is strong demand to make chat-based integrations (like DingTalk, #6443) first-class citizens with interactive cards, form inputs, and two-way communication, rather than simple message relays.
*   **Improved Agent-to-Agent Communication:** The weak handoff between main agents and sub-agents (#5239) is a clear pain point, with users wanting built-in notifications, monitoring, and lifecycle management for sub-agents.
*   **AI-Driven Workflow Automation:** Features like the "review" agent and stateless generation SSE (#6947) point towards Qwen Code being used not just as an interactive assistant, but as a programmable code automation engine for CI/CD and complex workflows.

#### 6. Developer Pain Points
*   **CI Flakiness:** There are multiple automated bug reports for CI failures, primarily E2E tests (e.g., #6938, #6940, #6935). While the autofix CI is attempting to address these, the sheer volume indicates a testing suite vulnerable to timing and environment issues.
*   **Configuration Not Respected:** Several bugs show that settings are not being fully honored. Disabled memory features still use context (#6936), and fractional session limits break runs (#6914). This erodes trust in the configuration system.
*   **"Fail Closed" vs. "Fail Open" in Safety:** The classifier deadlock (#6927) and the MCP read-only trust issue (#6917) show opposing but equally problematic behaviors. The classifier is too restrictive, blocking all tools, while the MCP trust logic is too permissive, allowing untrusted tools to bypass confirmation.
*   **Enterprise Protocol Incompatibility:** The WeCom message drop (#6939) and MCP tool name restrictions (#6970) are frustrating for users trying to integrate Qwen Code into their existing enterprise stack, which often relies on specific protocols (e.g., WeCom, specialized MCP servers).
*   **Session & Run Interruptions:** Users are reporting that agents stop mid-response (#6990) or runs terminate prematurely due to fractional session/tool limit settings (#6914). This is a core reliability issue that undermines the agent's ability to complete long tasks.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

**DeepSeek TUI Community Digest — 2026-07-16**

---

## Today’s Highlights
The community continues to focus on hardening the v0.8.x release train: a security-hardening tracker (#3368) remains open with heavy discussion, while a release‑blocking PR (#4332) landed to fix TUI state and routing regressions. Meanwhile, two important infrastructure PRs—performance optimizations (#3902) and startup cleanup deferral (#3761)—were merged, signalling progress toward v0.9 stability.

---

## Releases
No new versions in the last 24 hours.

---

## Hot Issues (10 Noteworthy)

1. **#3368 — [OPEN] v0.8.64: Security hardening/code-scanning fixes**  
   *Public tracker for CodeQL findings and advisory‑class fixes. 29 comments; maintainer‑led coordination.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/3368)

2. **#2487 — [CLOSED] Frequent “Turn stalled – no completion signal received” error**  
   *Causes YOLO mode to freeze. 20 comments; resolved but highlights a critical reliability gap.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2487)

3. **#1812 — [CLOSED] TUI freeze on Windows (crossterm poll)**  
   *UI becomes completely unresponsive on Windows 11. 11 comments; key for Windows users.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1812)

4. **#1607 — [CLOSED] Request: add CNY and other currency units to token cost estimation**  
   *7 comments; popular i18n/practicality request.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1607)

5. **#2261 — [CLOSED] TUI crash on Windows – input spills to PowerShell**  
   *6 comments; serious UX/safety problem when focus is lost.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2261)

6. **#1678 — [CLOSED] Feature: in‑app update check + GitHub link**  
   *5 comments; basic discoverability ask.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1678)

7. **#1835 — [CLOSED] Windows IME deadlock – input field unresponsive**  
   *5 comments; blocks Chinese IME users (Sogou, etc.).*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1835)

8. **#1067 — [CLOSED] glibc 2.38 required; incompatible with Ubuntu 22.04 (2.35)**  
   *4 comments; affects Linux server deployments.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1067)

9. **#3490 — [OPEN] v0.8.71: Legacy follow‑up and dead‑code inventory**  
   *4 comments; maintenance – clean up `allow(dead_code)` markers before v0.9.*  
   [Link](https://github.com/Hmbown/CodeWhale/issues/3490)

10. **#1897 — [OPEN] Refactor roadmap: ownership map and extraction plan**  
    *4 comments; maintainer‑grade factorization audit for the large App struct.*  
    [Link](https://github.com/Hmbown/CodeWhale/issues/1897)

---

## Key PR Progress (10 Important)

1. **#4332 — [CLOSED] fix: make v0.8.68 TUI state and routing truthful**  
   *Release‑blocking repair for regressions in provider configuration and sidebar routing.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4332)

2. **#3902 — [CLOSED] fix five render/input hot paths**  
   *Fixes #3896–#3900: sidebar double‑render, footer flicker, message list cascade, etc. Performance improvement.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/3902)

3. **#4087 — [OPEN] refactor(hooks): split config and executor modules**  
   *Splits monolithic hooks.rs into config/ and executor/, improving reviewability.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4087)

4. **#4084 — [CLOSED] fix(fleet): reject retired profile loadout aliases**  
   *Removes deprecated TOML fields `model_class_hint` and `route_tier`.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4084)

5. **#4044 — [CLOSED] fix(onboarding): localize dynamic welcome steps**  
   *Localises first‑run screens through `MessageId` registry, including zh‑Hant.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4044)

6. **#3969 — [CLOSED] Add per‑sub‑agent provider routing**  
   *Held for v0.8.68 fleet lane; paves the way for per‑profile provider/model config.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/3969)

7. **#3818 — [CLOSED] fix(tui): expand active tool run summaries**  
   *Covers edge case where in‑flight tool runs were missed during dense expansion.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/3818)

8. **#3761 — [CLOSED] defer startup maintenance cleanup**  
   *Moves stale‑output pruning and session cleanup to a background thread, improving startup latency.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/3761)

9. **#4088 — [CLOSED] fix(tui): preserve native selection without mouse capture**  
   *Fixes #4026 – alternate‑scroll mode disabled when mouse capture is off, enabling native drag selection.*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4088)

10. **#4370 — [OPEN] feat: add TelecomJS provider support**  
    *Adds a new custom provider. Model picker still limited – `refresh_catalog_cache` not invoked in production.*  
    [Link](https://github.com/Hmbown/CodeWhale/pull/4370)

---

## Feature Request Trends

Several distinct directions emerge from the issue landscape:

- **Localisation & i18n** – Requests for additional currencies in cost display (#1607), Chinese IME support (#1835), and full translation of onboarding (#4044) and slash‑command help (#1890) show a strong non‑English user base.
- **Configuration UX** – Users want to edit and persist config keys from within the TUI (#3303), and discover settings without reading `config.toml` manually.
- **Slash‑command ecosystem** – A major planned refactor (#1890, #1892, #1887) aims to make slash commands more visible, documented, and persistent (e.g., `$<skill>`, `/goal`, `/task`).
- **Provider extensibility** – The TelecomJS PR (#4370) and issues around model catalog caching point to demand for easier custom provider integration.
- **Performance & maintainability** – The maintainer is actively refactoring monoliths (App god object, runtime API, MCP transports) to improve code health before v0.9 (#3306, #3314, #3310, etc.).

---

## Developer Pain Points

Recurring frustrations and high‑frequency issues reported by the community:

- **Windows‑specific freezes and crashes** – Multiple reports of TUI becoming unresponsive (#1812), input leaking to PowerShell (#2261), and IME deadlocks (#1835). These are the most critical bugs affecting non‑Linux users.
- **Reliability of long‑running turns** – The “Turn stalled – no completion signal received” error (#2487) disrupts YOLO/agent workflows; even sending `continue` often fails.
- **Incomplete output and rendering** – Output truncated (#864), mouse scroll not showing model output (#1512), and visual line breaks copied to clipboard (#1853) interfere with everyday use.
- **Compatibility with older Linux** – The glibc 2.38 requirement (#1067) prevents deployment on Ubuntu 22.04 LTS, a common server environment.
- **Garbled CJK output** – Agent real‑time output shows mojibake for Chinese text (#1675).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*