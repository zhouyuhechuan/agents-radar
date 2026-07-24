# AI CLI Tools Community Digest 2026-07-24

> Generated: 2026-07-24 01:59 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-07-24 | **Scope:** All major open-source AI CLI tools

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is entering a **maturation phase** characterized by intense competition across three dimensions: agent reliability, cross-platform support, and integration extensibility (especially via MCP). All nine tools surveyed show active community engagement, but **Windows stability** and **context management** remain universal pain points. The ecosystem is bifurcating between **generalist coding agents** (Claude Code, Codex, Gemini CLI, OpenCode) and **specialized, lightweight alternatives** (Pi, DeepSeek TUI), with Copilot CLI and Kimi Code occupying a middle ground as IDE-integrated assistants. A clear signal is the industry-wide shift from proving agent capability to **hardening production reliability** — billing bugs, network instability, and MCP protocol fragility dominate today's discussions.

---

## 2. Activity Comparison

| Tool | Hot Issues (Today) | Active PRs (24h) | Release Status | Notable Engagement |
|------|-------------------|-----------------|----------------|---------------------|
| **Claude Code** | 10 (47👍 max) | 4 | No release | #29006: 114👍 for remote control |
| **OpenAI Codex** | 10 (72👍 max) | 10 (all merged/closed) | 2 Rust alphas | #20214: 72👍 Windows freeze |
| **Gemini CLI** | 10 (8👍 max) | 10 (all open/merged) | No release | #22323: subagent false-success bug |
| **Copilot CLI** | 10 (5👍 max) | 2 (1 spam) | **v1.0.74 + v1.0.74-4** | #3767 closed after 5 weeks |
| **Kimi Code** | 10 (16👍 max) | 10 (all open) | No release | #1282: 16👍 remote control |
| **OpenCode** | 10 (187👍 max) | 10 (mixed status) | No release | #6231: 187👍 model auto-discovery |
| **Pi** | 10 (N/A) | 10 (mixed status) | No release | #6999: models.json hot-reload |
| **Qwen Code** | 10 (N/A) | 10 (mixed status) | **1 nightly** | #7449: enterprise memory proposal |
| **DeepSeek TUI** | 10 (N/A) | 4 (2 open) | Pre-v0.9.1 | #4716: stop-ship macOS crash |

**Key observations:**
- **OpenCode** has the highest single-issue engagement (187👍 for model discovery) — a clear community-driven feature demand.
- **Codex** and **Gemini CLI** show the most PR pipeline throughput (10 each), though Codex’s are mostly automated infra fixes.
- **Copilot CLI** is the only tool with real patch releases today; most others are in incubation or regession-fix cycles.
- **DeepSeek TUI** (renamed to CodeWhale) has the most raw issues (26 updated in 24h) but lowest engagement per issue — suggests early-stage community or noise.

---

## 3. Shared Feature Directions

Several recurring requirements appear across **multiple tool communities**, indicating industry-wide developer needs:

| Theme | Tools Expressing Need | Specific Requirements |
|-------|----------------------|----------------------|
| **MCP Session Identification** | Claude Code (#41836), Copilot CLI (#4211, #4143) | Transmit conversation/session ID to MCP servers for stateful tool interactions; BigInt serialization support |
| **Remote Control / Session Continuity** | Claude Code (#29006, 114👍), Kimi Code (#1282, 16👍), Codex (#13036, #31973) | Attach/monitor CLI sessions from desktop or mobile; background sync for phone users |
| **Context Compaction Visibility** | Codex (#22220, #35032), Qwen Code (#6806), Claude Code (token efficiency requests) | Show when/why compaction fires, how much context is retained, % stuck after compression |
| **AST-Aware Code Navigation** | Gemini CLI (#22745, #22746), Claude Code (permission granularity) | Reduce token waste by precisely reading method/function bounds instead of whole files |
| **Multi-Session / Multi-Chat** | Codex (#13036), Claude Code (#29006), Copilot CLI (#4233), Gemini CLI (#22598) | Concurrent session management for multi-tasking; session renaming (OpenCode #25848) |
| **Model Auto-Discovery** | OpenCode (#6231, 187👍), Pi (#6886, #6951), Kimi Code (implicit via MCP fixes) | Dynamically list models from OpenAI-compatible providers; configurable reasoning tiers |
| **Provider/Fallback Flexibility** | Pi (#6886, #6948), Qwen Code (#7449), Claude Code (#79337 billing bug) | Server-side fallback between models; enterprise external-memory profiles; transparent provider routing |

**Notable:** Remote session control and MCP protocol hardening appear in **5+ tool communities** — this is the dominant infrastructure-level demand of 2026.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|------------|-------|------------|-------------|-----------|----------|-----|-----------|--------------|
| **Primary user** | Enterprise agent | IDE-integrated agent | Multi-agent orchestrator | Plugin-first assistant | Lightweight integrator | Power-user TUI | Minimalist coder | Enterprise + multimodal | Experimenter/learner |
| **Platform stability** | Poor (ECONNRESET, WSL) | Poor (Windows freeze, CPU) | Moderate (Wayland issues) | Moderate (WSL clipboard) | Moderate (Windows plugin crash) | Moderate (Windows `@` broken) | Good (Wayland fixed) | Good (CI flaky) | **Critical** (macOS crash) |
| **Agent complexity** | High (subagents, MCP) | High (world state, mcp) | **Very High** (generalist + subagents) | Medium (plugin orchestration) | Medium (MCP + plugins) | High (codemodes, subagents) | Low (single-agent focus) | High (channels, SSE) | Low-Medium (basic TUI) |
| **MCP maturity** | Maturing (session IDs missing) | Advanced (transport abstraction) | Early (tool limit bug) | **Maturing** (plugin spec v1) | Early (re-init bugs) | Early (plugin meta forwarding) | Early (constrained sampling) | Advanced (SSE, Java SDK) | **Broken** (stub responses) |
| **Unique strength** | Max plan model management | Proxy routing infrastructure | PR generator pipeline | Open Plugin Spec v1 | Cross-domain discussion (#2555) | **Highest community engagement** | Constrained tool sampling | Enterprise memory profile | Security policy engine |
| **Auto-update efficiency** | Poor (265 MB per session) | Not mentioned | Not mentioned | Stale process leak | Not mentioned | Not mentioned | Not mentioned | npm 12 breakage | Not mentioned |
| **Billing/Usage issues** | #79337 (Fable 5) | #35032 (compaction waste) | #22093 (unpermitted subagents) | #4097 (binary diffs) | Not prominent | **#35475 ($20 blocked output)** | Not prominent | Not prominent | Not prominent |

**Key differentiation insight:** 
- **OpenCode** has the most committed community (187👍 on feature requests) but suffers from the most egregious billing/filter bugs.
- **Gemini CLI** is pursuing the most ambitious multi-agent architecture but pays for it with reliability problems.
- **Copilot CLI** has the cleanest plugin story (Open Plugin Spec v1) but weakest PR pipeline — they ship via releases, not collaborative PRs.
- **DeepSeek TUI** is the least mature but has the most focused security-first design (denied_prefixes, config validation).

---

## 5. Community Momentum & Maturity

### Mature (high engagement, stable core, active maintainers)
| Tool | Signal | Verdict |
|------|--------|---------|
| **Claude Code** | 114👍 on feature request; 50 comments on ECONNRESET | **High engagement, slow fixes** – community is frustrated but invested |
| **OpenAI Codex** | 72👍 on Windows freeze; 10 PRs merged in 24h | **High throughput, regressing** – rapid infra work masks UX problems |
| **Copilot CLI** | v1.0.74 shipped; #3767 closed after 5 weeks | **Stable release cycle** – most mature patch management of the group |

### Growing (active community, increasing issue count)
| Tool | Signal | Verdict |
|------|--------|---------|
| **OpenCode** | 187👍 on model discovery; 10 PRs active | **High-velocity community** – users are heavily invested |
| **Kimi Code** | 16👍 on remote control; 10 PRs from single contributor | **One-developer-driven growth** – quality-of-life fixes outpacing features |
| **Pi** | 10 PRs active; multiple closed issues | **Steady improvement** – focused on provider flexibility and tool compatibility |
| **Qwen Code** | Enterprise memory proposal + nightly releases | **Enterprise pivot** – shifting from general agent to knowledge-integration platform |

### Early / Experimental
| Tool | Signal | Verdict |
|------|--------|---------|
| **Gemini CLI** | 8👍 max engagement; 4 PRs from automated bot | **Low community heat** – infrastructure-focused, less user pain |
| **DeepSeek TUI** | 26 issues in 24h but 0 comments on most | **Noise over signal** – early adopter feedback but low validation |

**Momentum leaderboard:** OpenCode > Claude Code > Codex > Copilot CLI > Kimi Code > Qwen Code > Pi > Gemini CLI > DeepSeek TUI

---

## 6. Trend Signals

Five actionable industry trends emerge from today's cross-tool data:

### 1. Context Window Management is the New UX Frontier
Tools that fail to provide **transparent, user-controllable context management** are losing user trust. Copilot CLI's 5MB CAPI limit wedges sessions; Codex's auto-compaction fires repeatedly at 80% fill; Qwen Code's `/compress` doesn't refresh the status line. The demand is for **always-visible context health** — not just a percentage, but breakdown of tokens by source (tool output vs conversation vs system prompt).

### 2. MCP Protocol Fragility is Blocking Enterprise Adoption
Every single tool reported MCP-related bugs today: 
- Claude Code: session IDs missing
- Copilot CLI: BigInt serialization, server-specific handshake failures
- Kimi Code: re-initialization loops, deferred startup crashes
- DeepSeek TUI: stub MCP server response (completely broken)
- Qwen Code: SSE timeouts, tool listing timeouts

**The industry needs a consolidated MCP transport layer** — the current state of bespoke client implementations is creating a support tax that slows ecosystem growth.

### 3. Windows Support Remains the Achilles' Heel
Five of nine tools have critical Windows issues open:
- **Codex**: #34879 (CPU saturation, P0), #20214 (freezes), #28074 (WSL broken)
- **Claude Code**: #69415 (WSL VSCode connections), #80016 (filesystem MCP)
- **Copilot CLI**: #3534 (WSL ARM64 clipboard), #4165 (resume hang)
- **Kimi Code**: #2553 (plugin crash, TypeError)
- **OpenCode**: #29859 (`@` symbol broken on Windows)

Developers targeting Windows should expect degraded performance; Linux/macOS are the primary supported platforms.

### 4. Subagent Reliability is the #1 Trust Eroder
When subagents lie about success (Gemini CLI #22323), run without permission (#22093), spawn orphan child processes (OpenCode #38564), or hang indefinitely (#21409), **user trust in autonomous mode collapses**. The industry needs standard subagent lifecycle auditing — at minimum: a kill guarantee, a logging trail, and a permission boundary that cannot be bypassed.

### 5. Billing Transparency is a Governance Time Bomb
Three tools have active billing-bug fires:
- **Claude Code**: Max plan users charged for Fable 5 (#79337)
- **OpenCode**: $20 charged for content-filtered output (#35475)
- **Codex**: Compaction wasting usage credits (#35032)

For enterprise adopters, these bugs represent **financial and compliance risk**. Tool maintainers who do not fix billing bugs will lose institutional trust faster than those who ship missing features.

---

## Recommendation for Developers

| If you... | Consider... | Because... |
|-----------|-------------|------------|
| **Need stable enterprise agent** | Copilot CLI or Qwen Code | Regular releases, enterprise-focused features |
| **Value community & rapid iteration** | OpenCode or Claude Code | Highest engagement, most feature requests |
| **Work primarily on macOS/Linux** | Claude Code or Gemini CLI | Better platform support; avoid Windows pain |
| **Want minimal, hackable tool** | DeepSeek TUI or Pi | Lower complexity, extensible architecture |
| **Need multi-agent orchestration** | Gemini CLI (with caution) or Codex | Most advanced subagent infrastructure (but expect bugs) |

**Bottom line:** No tool is "mature" by traditional software standards. The ecosystem is moving fast — pick the one whose **pain points you can tolerate** rather than the one with the most features.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026-07-24 | Source: github.com/anthropics/skills*

## 1. Top Skills Ranking

The following pull requests have drawn the most community attention (by comment volume) and represent the most-discussed skill submissions in the repository. All are currently **open**.

1. **[#1298 – fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298)**  
   *Functionality:* Repairs the `run_eval.py` script so that the description-optimisation loop (`run_loop.py`, `improve_description.py`) correctly detects skill trigger rates instead of always returning `recall=0%`. Fixes include installing the eval artifact as a real skill, Windows stream handling, trigger detection logic, and parallel worker support.  
   *Discussion highlights:* Rooted in issue #556 (10+ independent reproductions), this PR is the central fix for a critical workflow blocker. Community members have verified the problem across multiple OS and environment setups.  
   *Status:* Open, last updated 2026-06-23.

2. **[#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514)**  
   *Functionality:* Prevents common typographic defects in AI-generated documents: orphan word wrap, widow paragraphs, and numbering misalignment. Designed to run automatically after document generation.  
   *Discussion highlights:* High interest from users who frequently produce long-form content. The skill addresses a subtle but pervasive quality issue that users rarely request proactively.  
   *Status:* Open, last updated 2026-03-13.

3. **[#1367 – feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate](https://github.com/anthropics/skills/pull/1367)**  
   *Functionality:* A universal skill that audits AI output before delivery — first verifying every claimed file exists, then scoring reasoning quality across four dimensions (completeness, consistency, safety, clarity) in damage-severity priority order.  
   *Discussion highlights:* Proposes a systematic approach to output quality; sparked follow-up discussion in issue #1385 about a multi-gate pipeline.  
   *Status:* Open, last updated 2026-07-02.

4. **[#525 – Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525)**  
   *Functionality:* Integrates the Pyxel retro game engine via `pyxel-mcp`, enabling Claude to create pixel-art/8-bit games with a write → run_and_capture → inspect → iterate workflow.  
   *Discussion highlights:* Popularity driven by the novelty of game creation with Claude; the author is also the Pyxel creator, lending authority.  
   *Status:* Open, last updated 2026-07-15.

5. **[#1302 – Add color-expert skill](https://github.com/anthropics/skills/pull/1302)**  
   *Functionality:* A self-contained color expertise skill covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, etc.), color spaces with usage guides (OKLCH for scales, OKLAB for gradients, CAM16 for perception), and palette generation.  
   *Discussion highlights:* Appeals to designers, data visualizers, and front-end developers. The breadth of references and practical “what to use when” tables received praise.  
   *Status:* Open, last updated 2026-07-21.

6. **[#723 – feat: add testing-patterns skill](https://github.com/anthropics/skills/pull/723)**  
   *Functionality:* Comprehensive coverage of testing philosophy (Testing Trophy model), unit testing (AAA, naming, pure functions), React component testing (Testing Library, queries), and integration/end-to-end patterns.  
   *Discussion highlights:* Addressed a clear gap – the skills collection had no dedicated testing guidance. Community feedback focused on expanding beyond JavaScript.  
   *Status:* Open, last updated 2026-04-21.

7. **[#486 – Add ODT skill — OpenDocument text creation and template filling](https://github.com/anthropics/skills/pull/486)**  
   *Functionality:* Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Supports template filling and ODT-to-HTML conversion.  
   *Discussion highlights:* High demand for LibreOffice/ISO-standard document support. Discussion noted overlap with existing document skills but confirmed distinct ODF-specific functionality.  
   *Status:* Open, last updated 2026-04-14.

## 2. Community Demand Trends

Analysis of the most-commented issues reveals several clear demand directions:

- **Core Tooling Reliability (skill-creator)** – Issues #556, #1169, and #1061 all report `recall=0%` and Windows compatibility failures in the skill description optimization loop. This is the #1 pain point: the pipeline that helps authors improve skill descriptions is fundamentally broken for many users.
- **Security & Trust Boundaries** – Issue #492 (43 comments, 2 👍) highlights that community skills distributed under the `anthropic/` namespace create a trust vulnerability. Users want clear separation between official and community skills, and possibly a signing/review mechanism.
- **Organizational Sharing** – Issue #228 (14 comments, 7 👍) requests org-wide skill sharing in Claude.ai, eliminating the manual .skill file transfer process. This is the most-upvoted feature request.
- **New Skill Domains** – Proposals gaining traction include:
  - **Agent governance** (#412) – safety patterns, policy enforcement, audit trails.
  - **Compact memory** (#1329) – symbolic notation for reducing agent context overhead.
  - **Reasoning quality gates** (#1385) – pre-task calibration, adversarial review, delivery verification.
- **Platform Expansion** – Requests for Bedrock compatibility (#29) and exposing skills as MCP servers (#16) indicate a desire to use skills outside the Claude Code CLI.
- **Duplicate & Install Cleanup** – Issue #189 (6 comments, 9 👍) reports that `document-skills` and `example-skills` plugins install identical content, wasting context window space.

## 3. High-Potential Pending Skills

These pull requests have active discussion and are likely to land soon:

- **[#1298 – run_eval.py 0% recall fix](https://github.com/anthropics/skills/pull/1298)** – The most critical fix in the repo. Merging will unblock all skill-creator users on Windows and Linux.
- **[#1099 – Fix run_eval.py crash on Windows](https://github.com/anthropics/skills/pull/1099)** – A narrower fix for the same underlying issue; may be superseded by #1298.
- **[#1367 – Self-audit skill (v1.3.0)](https://github.com/anthropics/skills/pull/1367)** – A polished proposal with mechanical verification and reasoning audit. Follow-on issue #1385 suggests a pipeline, indicating ongoing refinement.
- **[#1302 – color-expert skill](https://github.com/anthropics/skills/pull/1302)** – Updated very recently (2026-07-21); likely close to final review.
- **[#525 – pyxel skill](https://github.com/anthropics/skills/pull/525)** – Updated 2026-07-15; sustained interest over several months.
- **[#514 – document-typography skill](https://github.com/anthropics/skills/pull/514)** – A well-scoped, low-risk skill that fills a clear quality gap; has been open since March but discussion appears settled.

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is fixing and trusting the skill-creator toolchain** – multiple open issues and overlapping PRs all target the same broken evaluation pipeline, while the top security issue reveals a parallel need for trust boundaries around community-contributed skills.

---

# Claude Code Community Digest – 2026-07-24

**Data source:** [anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## Today’s Highlights

No new releases were published in the last 24 hours. The community is focused on two major pain points: a bug that forces Max plan users to use usage credits for the Fable 5 model (causing silent downgrades), and network-level errors (`ECONNRESET` / “connection closed mid-response”) affecting macOS, Linux, and WSL/VSCode environments. A highly upvoted feature request for **remote control of Claude Code sessions** from the Desktop app continues to gain traction (114 👍).

---

## Releases

*None in the last 24 hours.*

---

## Hot Issues

*(10 noteworthy issues, ordered by community engagement)*

1. **[#5674 – Persistent ECONNRESET Errors on macOS Network Connections](https://github.com/anthropics/claude-code/issues/5674)**  
   *Open, 50 comments, 47 👍*  
   Repeated connection resets on macOS that disrupt tasks and cause disconnections. Does not occur on Windows or Linux on the same network. Strong community resonance.

2. **[#79337 – Fable 5 prompts 'usage credits required' on Max plan (2026-07-20)](https://github.com/anthropics/claude-code/issues/79337)**  
   *Open, 40 comments, 12 👍*  
   From the day Fable 5 became standard on Max plans, Claude Code downgrades sessions to Opus 4.8 and claims Fable 5 requires usage credits. High impact for paying users.

3. **[#29006 – Enable Remote Control for Claude Code sessions in Claude Desktop App](https://github.com/anthropics/claude-code/issues/29006)**  
   *Open, 35 comments, 114 👍*  
   Feature request to allow controlling CLI sessions from the desktop app. Most upvoted open issue; indicates strong desire for multi-surface integration.

4. **[#69415 – API Error: Connection closed mid-response (VSCode/WSL)](https://github.com/anthropics/claude-code/issues/69415)**  
   *Open, 33 comments, 65 👍*  
   Frequent connection closures mid-stream, rendering Claude Code unusable on VSCode with WSL. Affects a large segment of Windows developers.

5. **[#41836 – No session/conversation identifier sent to MCP servers](https://github.com/anthropics/claude-code/issues/41836)**  
   *Open, 14 comments, 24 👍*  
   HTTP MCP servers cannot distinguish concurrent sessions, making per-conversation state impossible. Impacts multi-session workflows.

6. **[#37628 – VSCode: Renaming session via sidebar pencil icon doesn't sync terminal tab title](https://github.com/anthropics/claude-code/issues/37628)**  
   *Open, 11 comments, 14 👍*  
   Custom session names overwritten on next message. UX annoyance for VSCode users who manage multiple sessions.

7. **[#69336 – API Error: Connection closed mid-response (Linux)](https://github.com/anthropics/claude-code/issues/69336)**  
   *Open, 9 comments, 11 👍*  
   Similar to #69415 but on Linux; occurs immediately in a new context window. Suggests a server-side or API client issue.

8. **[#80016 – Windows: Filesystem extension handshake succeeds but tools/call never dispatched](https://github.com/anthropics/claude-code/issues/80016)**  
   *Open, 9 comments*  
   MCP handshake works but tool invocations are never forwarded. Users report reinstallation does not fix; mirrors closed issue #22299.

9. **[#49985 – Conversation rendered/duplicated multiple times in terminal (Windows)](https://github.com/anthropics/claude-code/issues/49985)**  
   *Open, 8 comments, 22 👍*  
   Display bug in the TUI that duplicates conversation text; disrupts reading and scrolling.

10. **[#79341 – Fable 5 incorrectly requires usage credits on Max 20x plan](https://github.com/anthropics/claude-code/issues/79341)**  
    *Open, 7 comments, 10 👍*  
    Duplicate of #79337, but specifically reports the issue on Max 20x plans despite unused weekly Fable allowance.

---

## Key PR Progress

*(All 4 open/updated PRs in the last 24 hours)*

1. **[#41611 – add the missing source to claude code](https://github.com/anthropics/claude-code/pull/41611)** *(Open)*  
   A small documentation/data patch to include an omitted source reference. Still unmerged after several months.

2. **[#42604 – Remove "retro-futuristic" recommendation from Frontend Design Skill](https://github.com/anthropics/claude-code/pull/42604)** *(Closed)*  
   Community-driven cleanup to remove an outdated or disliked design suggestion. Merged or declined? Status shows closed.

3. **[#80508 – fix(scripts): paginate comments and reactions in auto-close-duplicates](https://github.com/anthropics/claude-code/pull/80508)** *(Open)*  
   Fixes a bug in the issue triage script that only read the first 30 comments/reactions, causing duplicate detection to miss later activity. Important for repository maintainers.

4. **[#80495 – fix(ralph-wiggum): stop parsing /ralph-loop prompt text as shell code](https://github.com/anthropics/claude-code/pull/80495)** *(Open)*  
   Fixes a security/functionality issue where `/ralph-loop` substituted user text directly into a shell command, causing parsing failures. Addresses long-standing issue #16037.

---

## Feature Request Trends

The most frequently requested feature directions, distilled from open issues tagged `enhancement`:

- **Remote control / session management** – [#29006](https://github.com/anthropics/claude-code/issues/29006) (114 👍) and others: ability to attach, monitor, and control CLI sessions from the Desktop app or browser.
- **VS Code integration polish** – Syntax highlighting in chat panel ([#64968](https://github.com/anthropics/claude-code/issues/64968), 21 👍), custom spinner verbs setting ([#80742](https://github.com/anthropics/claude-code/issues/80742)), and general IDE parity.
- **Token efficiency** – [#80449](https://github.com/anthropics/claude-code/issues/80449): PDF reading should not send both text and rendered images, which wastes tokens.
- **MCP session identification** – [#41836](https://github.com/anthropics/claude-code/issues/41836): transmit a session/conversation ID to MCP servers for stateful tool interactions.
- **Permission granularity** – Several issues request finer-grained control over Bash/read-only commands to reduce unnecessary prompts.

---

## Developer Pain Points

Recurring themes from the most active issues:

1. **Network instability** – `ECONNRESET` and “connection closed mid-response” errors persist across macOS, Linux, and WSL. Affects all major platforms and makes continuous use unreliable.
2. **Fable 5 billing confusion** – Max plan users are being incorrectly charged usage credits or downgraded to Opus 4.8. Multiple reports (e.g., [#79337](https://github.com/anthropics/claude-code/issues/79337), [#79341](https://github.com/anthropics/claude-code/issues/79341), [#80382](https://github.com/anthropics/claude-code/issues/80382)) suggest a systemic entitlement-check bug.
3. **MCP tool dispatch failures** – On Windows, filesystem MCP servers handshake but never receive tool execution, effectively making the filesystem extension unusable ([#80016](https://github.com/anthropics/claude-code/issues/80016)).
4. **Auto-updater inefficiency** – Every running session downloads the full ~265 MB binary independently, causing bandwidth spikes and failed 0-byte version files ([#79942](https://github.com/anthropics/claude-code/issues/79942)). Multi-session workflows amplify the problem.
5. **Session/UI fragility** – Duplicated conversation text in TUI ([#49985](https://github.com/anthropics/claude-code/issues/49985)), rename sync failures in VSCode ([#37628](https://github.com/anthropics/claude-code/issues/37628)), and lost focus on alt-tab ([#80743](https://github.com/anthropics/claude-code/issues/80743)) degrade everyday usage.

---

*Digest generated from GitHub data as of 2026-07-24 23:59 UTC.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – July 24, 2026

## Today’s Highlights
The repository saw two new Rust alpha releases and a flurry of infrastructure PRs, many from the automated `copyberry[bot]` targeting proxy routing, tool attribution, and environment registry improvements. Meanwhile, Windows performance and context compaction issues continued to dominate the issue tracker, with a critical CPU‑saturation regression (#34879) and a long‑standing mixed‑line‑endings bug (#4003) still open.

---

## Releases
- **`rust-v0.146.0-alpha.5`** – Minor bump in the Rust client library; no detailed changelog.
- **`rust-v0.146.0-alpha.3.1`** – Patch release on the `v0.146.0-alpha.3` line.

Both are incremental alpha updates; no breaking changes or new features announced.

---

## Hot Issues (10 Noteworthy)

1. **#20214 – Codex App frequently freezes/stutters on Windows 11 Pro**  
   Widely upvoted (👍72, 75 comments). Users report the app becomes unresponsive despite ample resources (Ryzen 5, 32 GB RAM). A top priority for the Windows team.  
   [OpenAI/Codex#20214](https://github.com/openai/codex/issues/20214)

2. **#4003 – Patched files have mixed line endings on Windows**  
   Long‑standing bug (since Sept 2025, 👍71). Codex does not respect native line endings when applying patches, causing Git noise. Frequent request for fix.  
   [OpenAI/Codex#4003](https://github.com/openai/codex/issues/4003)

3. **#22220 – Conversation Compaction Telemetry / Context Health**  
   Enhancement request (👍12, 19 comments). Users want visibility into when and why compaction fires, and how much context is retained. High demand for better UX around context management.  
   [OpenAI/Codex#22220](https://github.com/openai/codex/issues/22220)

4. **#35032 – Desktop auto‑compaction leaves thread ~80% full, causing repeat cycles**  
   New regression (13 comments). After compaction the context meter stays nearly full, wasting usage credits on successive compactions. Affects long tool‑heavy sessions.  
   [OpenAI/Codex#35032](https://github.com/openai/codex/issues/35032)

5. **#13036 – Support display of multiple chats**  
   Popular request (👍8, 12 comments). Users need concurrent chat sessions for multi‑tasking and multi‑agent workflows.  
   [OpenAI/Codex#13036](https://github.com/openai/codex/issues/13036)

6. **#27284 – SSH remote project shows “No chats” while threads exist**  
   Desktop app fails to list remote sessions after reconnecting (11 comments). Disrupts workflow for remote development.  
   [OpenAI/Codex#27284](https://github.com/openai/codex/issues/27284)

7. **#28074 – WSL integration broken even with fresh installs**  
   Repeated reports (👍8, 11 comments). After uninstall/reinstall the app cannot detect WSL, blocking Windows Linux users.  
   [OpenAI/Codex#28074](https://github.com/openai/codex/issues/28074)

8. **#31973 – Windows Remote Control permanently stuck in “Reconnecting…”**  
   No recovery path (10 comments). QR‑pairing users cannot regain remote access without restarting the host app.  
   [OpenAI/Codex#31973](https://github.com/openai/codex/issues/31973)

9. **#34879 – [P0] Windows launch saturates all CPU cores via WmiPrvSE**  
   Critical regression (5 comments, 👍0). Launching the app immediately pegs CPU at 100% – machine becomes unusable.  
   [OpenAI/Codex#34879](https://github.com/openai/codex/issues/34879)

10. **#34290 – Intermittent multi‑minute `apply_patch` hangs on Windows**  
    Sporadic blocking of tool calls (4 comments). Even with powerful hardware, patch application can stall for minutes.  
    [OpenAI/Codex#34290](https://github.com/openai/codex/issues/34290)

---

## Key PR Progress (10 Important Merges/Opens)

1. **#35063 – Track deferred tool namespaces in world state**  
   New feature (closed). Exposes deferred tool namespaces to the model via a `<tools>` section, enabling better model awareness of available tools.  
   [OpenAI/Codex#35063](https://github.com/openai/codex/pull/35063)

2. **#35059 – Decouple exec‑server HTTP from reqwest types**  
   Infrastructure (closed). Switches to neutral HTTP types, improving transport agnosticism and maintainability.  
   [OpenAI/Codex#35059](https://github.com/openai/codex/pull/35059)

3. **#35056 – Route exec‑server WebSockets through configured proxies**  
   Networking (closed). Ensures remote environment WebSocket connections honor Codex’s outbound proxy policy.  
   [OpenAI/Codex#35056](https://github.com/openai/codex/pull/35056)

4. **#35054 – Allow disabling the `update_plan` tool**  
   Configurability (closed). Adds a toggle to remove the `update_plan` tool from the agent’s toolset, requested by users for simpler workflows.  
   [OpenAI/Codex#35054](https://github.com/openai/codex/pull/35054)

5. **#35049 – Register the Guardian V2 feature flag**  
   Feature (closed). Adds a disabled‑by‑default flag for the next major Guardian review system.  
   [OpenAI/Codex#35049](https://github.com/openai/codex/pull/35049)

6. **#35036 – Preserve Windows sandbox proxy settings in guardian sessions**  
   Fix (closed). Prevents loss of proxy configuration when Guardian runs commands in Windows sandboxed sessions.  
   [OpenAI/Codex#35036](https://github.com/openai/codex/pull/35036)

7. **#35034 – Route environment registry requests through the shared HTTP client**  
   Infrastructure (closed). Makes noise‑registry calls follow the same proxy rules as the rest of Codex.  
   [OpenAI/Codex#35034](https://github.com/openai/codex/pull/35034)

8. **#35033 – Expose Browser Use requirements through the app server**  
   Feature (closed). Parses new `browser_use.disable_auto_review` setting and exposes it to the UI.  
   [OpenAI/Codex#35033](https://github.com/openai/codex/pull/35033)

9. **#35031 – Enforce writer ownership for thread archive and deletion**  
   Concurrency fix (closed). Prevents data races when multiple app‑server processes try to archive/delete the same thread.  
   [OpenAI/Codex#35031](https://github.com/openai/codex/pull/35031)

10. **#35017 – Release 0.146.0‑alpha.3**  
    Release (closed). Cut of the `v0.146.0-alpha.3` version, though quickly followed by .5 and .3.1.  
    [OpenAI/Codex#35017](https://github.com/openai/codex/pull/35017)

---

## Feature Request Trends
The community is pushing for **better context visibility** (#22220) to understand when and why compaction occurs. **Multiple simultaneous chat sessions** (#13036) are a recurring theme, along with **importing ChatGPT transcripts** (#30636) as trusted context. Users also request **UI customisation options** such as disabling sidebar expansion on hover (#31538) and opting out of the `update_plan` tool (#35054). The common thread is a desire for more **user‑controlled transparency** over agent behaviour.

---

## Developer Pain Points
**Windows stability** remains the top pain point: the app freezes (#20214), saturates CPU on launch (#34879), and has flaky WSL (#28074) and remote‑access (#31973) support. **Context compaction inefficiency** (#35032, #22220) wastes usage credits and baffles users. **Subagent lifecycle** issues (stale subagents #25179, spawning drain #14116) plague long sessions. **Plugin/file persistence** bugs (skills deleted #19265, plugin marketplace reset #29103) break setups after restart. The long‑standing **mixed line endings** bug (#4003) continues to annoy Windows Git users. Overall, developers are frustrated by regressions and a lack of reliable background context management.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-07-24

## Today’s Highlights
No new releases landed in the past 24 hours, but the project saw sustained activity on long-running agent reliability issues, especially the subagent false‑success bug (#22323) and the generalist agent hang (#21409). On the pull request side, several security‑focused fixes merged or opened – including HTTPS enforcement for credential auth (#28517) and MCP OAuth token refresh improvements (#28481). The PR generator pipeline for automated issue‑to‑PR from the 2026 intern project continues to make progress with four large PRs now open.

## Releases
No releases in the last 24 hours.

## Hot Issues
1. **Subagent recovery after MAX_TURNS reported as GOAL success**  
   #22323 – The `codebase_investigator` subagent mistakenly reports `status: "success"` after hitting the turn limit, hiding the interruption. 12 comments, 2 👍.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **Generalist agent hangs indefinitely**  
   #21409 – Users report that the generalist agent hangs on simple tasks (e.g. folder creation) until manually cancelled. Workaround: instruct the model not to use subagents. 8 comments, 8 👍.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **Component‑level evaluations needing improvement**  
   #24353 – An epic tracking the need for robust component evals, building on existing behavioral eval framework. 7 comments.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/24353)

4. **AST‑aware file reads, search, and mapping**  
   #22745 – Epic to investigate whether AST‑aware tools can reduce turn count and token noise by precisely reading method bounds. 7 comments.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22745)

5. **Gemini does not use skills and sub‑agents enough**  
   #21968 – Anecdotal evidence that custom skills (e.g. gradle, git) are rarely invoked automatically. 6 comments.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21968)

6. **Auto Memory retries low‑signal sessions indefinitely**  
   #26522 – Sessions judged “low‑signal” are not marked as processed, causing infinite retries. 5 comments.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/26522)

7. **Shell command execution gets stuck after completion**  
   #25166 – Even simple CLI commands leave the shell in “Waiting input” state after finishing. 4 comments, 3 👍.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/25166)

8. **Browser subagent fails in Wayland**  
   #21983 – Browser agent crashes or fails on Wayland display servers. 4 comments, 1 👍.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21983)

9. **Subagents running without permission since v0.33.0**  
   #22093 – Users with agents mode disabled still see subagents active, particularly the generalist agent. 3 comments.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22093)

10. **400 error when >128 tools are available**  
    #24246 – Gemini CLI returns a 400 error when the model is exposed to more than 128 tools. Suggests smarter tool scoping. 3 comments.  
    [Link](https://github.com/google-gemini/gemini-cli/issues/24246)

## Key PR Progress
1. **fix(core): prevent infinite auth loop** (#28519) – Awaits credential save and forces consent to break the OAuth loop.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28519)

2. **fix(core): enforce explicit tag length in file keychain** (#28523) – Adds validation for authentication tag lengths in credential storage.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28523)

3. **feat(caretaker‑triage): prompt hill‑climbing & orchestrator updates** (#28524) – Improves triage worker prompts and introduces a `code_explorer` skill.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28524)

4. **feat(pr‑generator‑orchestrator): iterative bug‑fixing state machine** (#28433) – Large PR implementing the orchestration layer for the SSR pipeline.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28433)

5. **feat(pr‑generator‑db): Firestore concurrency dual‑locking** (#28432) – Adds transactional locking for issue‑to‑PR code generation.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28432)

6. **fix(core): filter out thought parts from history** (#28509) – Prevents reasoning blocks from leaking into history turns when context management is disabled.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28509)

7. **fix(vscode‑ide‑companion): preserve terminal focus** (#28183) – Maintains focus in the integrated terminal after closing diff tabs.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28183)

8. **fix(core): enforce HTTPS for GoogleCredentialsAuthProvider** (#28517) – Prevents cleartext transmission of ADC tokens.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28517)

9. **fix(core): refresh MCP OAuth tokens with stored client ID** (#28481) – Fixes token refresh failures that previously deleted credentials.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/28481)

10. **fix(auth): use native fetch for OAuth token exchange** (#28446) – Resolves “Premature close” errors on headless VPSes.  
    [Link](https://github.com/google-gemini/gemini-cli/pull/28446)

## Feature Request Trends
- **AST‑aware code navigation** (#22745, #22746): Multiple issues propose using AST parsing to improve file reads, search, and codebase mapping – potentially reducing token usage and turn counts.
- **Agent self‑awareness** (#21432): Requests that the CLI understand its own hotkeys, flags, and configuration to act as its own guide.
- **Subagent trajectory sharing** (#22598): Users want to share subagent traces via `/chat share` for debugging and evaluation.
- **Destructive operation prevention** (#22672): Agents should discourage or block dangerous commands (e.g. `git reset --force`) when safer alternatives exist.
- **Browser agent resilience** (#22232): Automatic session takeover and lock recovery for the browser subagent when using persistent profiles.

## Developer Pain Points
- **Agent reliability**: The most frequent complaints involve subagents misreporting success (#22323), hanging indefinitely (#21409), or running without permission (#22093). These erode trust in autonomous mode.
- **Shell command handling**: The CLI often gets stuck waiting for input after simple commands finish (#25166) or creates tmp scripts in random directories (#23571).
- **Configuration overrides ignored**: Browser agent and other subagents ignore `settings.json` overrides like `maxTurns` (#22267).
- **Tool explosion**: With more than 128 tools, the model hits a 400 error; users need smarter tool scoping (#24246).
- **Memory system quirks**: Auto Memory retries low‑signal sessions forever (#26522) and silently skips invalid patches (#26523), while also potentially logging sensitive content (#26525).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-24

## Today’s Highlights
Two patch releases (v1.0.74 and v1.0.74‑4) landed yesterday with support for **Open Plugin Spec v1** manifests and improved subagent timeline attribution. On the issue tracker, a critical regression in Ctrl‑C interrupt handling was reported, while a long‑standing session‑wedging bug caused by oversized attachments was finally closed after five weeks. The community is also actively discussing how Copilot CLI should inherit MCP tools from connected IDE instances.

## Releases
- **v1.0.74** (2026‑07‑23) — [Release link](https://github.com/github/copilot-cli/releases/tag/v1.0.74)  
  - Added support for Open Plugin Spec v1 plugin manifests and `mcp.json` configuration.  
  - IDE integration now reconnects reliably after MCP server reloads or directory changes.  
  - Fixed a bug where typing `?` while the search bar was open would enter the character instead of opening quick help.  
  - Multi‑turn subagent improvements (details truncated in data).  

- **v1.0.74‑4** (2026‑07‑23) — [Release link](https://github.com/github/copilot-cli/releases/tag/v1.0.74-4)  
  - All v1.0.74 changes plus: subagent timelines now identify whether prompts came from the main agent or another subagent.

## Hot Issues
*10 notable issues from the last 24 hours (sorted by community interest and impact).*

1. **[#3767 – Oversized attachment permanently wedges session](https://github.com/github/copilot-cli/issues/3767)** *(CLOSED)*  
   Attachments exceeding CAPI’s 5 MB native limit cause an unrecoverable turn failure. After 5 weeks and 12 comments, a fix was deployed. This is a critical session‑killer for users working with large files.

2. **[#3534 – WSL2 ARM64: `/copy` fails with `clip.exe exited with code 1`](https://github.com/github/copilot-cli/issues/3534)** *(OPEN, 5 comments, 👍4)*  
   A quoting bug in the `cmd.exe` wrapper breaks clipboard writes on ARM64 WSL2. Widely upvoted; impacts Windows on ARM users daily.

3. **[#4097 – `apply_patch` stores deleted binaries in session history, permanently exceeding 5 MB limit](https://github.com/github/copilot-cli/issues/4097)** *(OPEN, 4 comments, 👍5)*  
   When a binary file is deleted, its entire content is kept as a textual diff in conversation history, causing every subsequent request to hit the CAPI size limit. `/compact` does not help. A frequent pain point for repos containing binaries.

4. **[#4089 – Atlassian MCP server: OAuth succeeds but zero tools exposed](https://github.com/github/copilot-cli/issues/4089)** *(OPEN, 4 comments)*  
   The official Atlassian MCP server connects and authenticates but never makes tools available to agents, while other HTTP MCP servers work fine. Points to a server‑specific parsing or handshake issue.

5. **[#4165 – `copilot --resume` hangs at “Resuming session” on Windows cold start](https://github.com/github/copilot-cli/issues/4165)** *(OPEN, 3 comments, 👍1)*  
   Resuming a session from a cold start in PowerShell gets stuck forever. Users can work around it by starting a session first, but the hang is a blocking bug for workflows that rely on session persistence.

6. **[#4206 – Environment footer stuck on “Loading: …” forever under org MCP policy](https://github.com/github/copilot-cli/issues/4206)** *(OPEN, 3 comments, 👍2)*  
   When built‑in GitHub MCP handshake stalls due to organization MCP policies, the status footer never completes loading, even though `/env` shows everything is loaded. Affects enterprise users.

7. **[#4122 – Subagents resolve relative markdown links against cwd instead of agent file directory](https://github.com/github/copilot-cli/issues/4122)** *(CLOSED, 2 comments, 👍2)*  
   Custom agent definitions that reference relative paths fail to load linked docs. Quickly closed, indicating the fix was trivial—but it previously broke many custom agent setups.

8. **[#4233 – Emit `usage_update` in `--acp` mode for context window and AI credit parity](https://github.com/github/copilot-cli/issues/4233)** *(OPEN, 1 comment, 👍2)*  
   A feature request with strong community support: `copilot --acp` (used by editors like Zed) currently omits the usage update that the interactive CLI shows in its status line. Editors can’t display context‑window or credit usage without it.

9. **[#4235 – Ctrl+C no longer cancels/interrupts an active agent run (regression)](https://github.com/github/copilot-cli/issues/4235)** *(OPEN)*  
   A newly reported regression—Ctrl+C no longer aborts an ongoing agent turn. Previously it worked; now the keypress is ignored. High urgency for daily interactive use.

10. **[#4211 – Copilot CLI cannot handle BigInt in structured MCP response](https://github.com/github/copilot-cli/issues/4211)** *(OPEN, 1 comment)*  
    When an MCP server returns a large number (BigInt), serialization fails with `TypeError: Do not know how to serialize a BigInt`. All ongoing tasks are aborted. Points to missing big‑number support in the CLI’s MCP client.

## Key PR Progress
Only two pull requests were updated in the last 24 hours, neither representing active feature work:

- **[PR #3163 – “ViewSonic monitor”](https://github.com/github/copilot-cli/pull/3163)** *(OPEN)*  
  Appears to be a test or spam PR referencing unrelated GitHub actions. No substantive code changes.

- **[PR #4228 – Withdrawn: incorrect scope for #3534](https://github.com/github/copilot-cli/pull/4228)** *(CLOSED, withdrawn)*  
  Attempted to fix the WSL2 clipboard quoting bug but only changed documentation instead of the private clipboard runtime. Author deleted the branch.

No meaningful PRs are in flight today beyond the already‑released patch versions.

## Feature Request Trends
From the issue tracker, several recurring feature directions are visible:

- **MCP & Plugin Integration**  
  - Inherit MCP tools from a connected VS Code instance ([#4143](https://github.com/github/copilot-cli/issues/4143))  
  - Support `resources/subscribe` and notifications for autonomous agent workflows ([#3073](https://github.com/github/copilot-cli/issues/3073))  
  - Allow MCP servers launched from plugins to resolve the active project directory ([#4234](https://github.com/github/copilot-cli/issues/4234))

- **Session & Context Improvements**  
  - Emit usage updates in `--acp` mode ([#4233](https://github.com/github/copilot-cli/issues/4233))  
  - Scope auto‑injected instructions with domain tags (not just `applyTo` globs) ([#4231](https://github.com/github/copilot-cli/issues/4231))  
  - Allow hooks to modify the user prompt before it reaches the model ([#3713](https://github.com/github/copilot-cli/issues/3713))

- **Clipboard & Terminal UX**  
  - Support X11/Wayland PRIMARY selection for `copyOnSelect` ([#4236](https://github.com/github/copilot-cli/issues/4236))  
  - Make `Ctrl+G` (edit in `$EDITOR`) work during `ask_user` question prompts ([#4230](https://github.com/github/copilot-cli/issues/4230))

## Developer Pain Points
The following frustrations appear repeatedly across issues and comments:

- **Session size limits** – The CAPI 5 MB limit regularly causes irreversible session wedging when large files or binary diffs are included ([#3767](https://github.com/github/copilot-cli/issues/3767), [#4097](https://github.com/github/copilot-cli/issues/4097)).
- **WSL2 clipboard breakage** – A `cmd.exe` quoting bug makes `/copy` unusable on ARM64 WSL2 ([#3534](https://github.com/github/copilot-cli/issues/3534)).
- **Windows resume hang** – `copilot --resume` never completes on Windows cold start ([#4165](https://github.com/github/copilot-cli/issues/4165)).
- **Stale processes & memory leaks** – Idle sessions hold ~460 MB indefinitely, and old binaries remain running after an in‑CLI update ([#4199](https://github.com/github/copilot-cli/issues/4199)).
- **Loading stalls** – Environment footer hangs on “Loading:” under enterprise MCP policies ([#4206](https://github.com/github/copilot-cli/issues/4206)).
- **MCP reliability** – BigInt serialization errors ([#4211](https://github.com/github/copilot-cli/issues/4211)), tool changes not visible until next turn ([#3125](https://github.com/github/copilot-cli/issues/3125)), and server‑specific incompatibilities (Atlassian, [#4089](https://github.com/github/copilot-cli/issues/4089)).
- **Regression in interrupt handling** – Ctrl+C no longer aborts agent runs ([#4235](https://github.com/github/copilot-cli/issues/4235)).
- **Rendering quirks** – MCP server labels rendered one character per line on failure ([#4238](https://github.com/github/copilot-cli/issues/4238)), raw JSON shown instead of diff view for hook‑driven “ask” decisions ([#4135](https://github.com/github/copilot-cli/issues/4135)).

---

*Generated from GitHub data for 2026-07-24. All links point to issue/PR pages on github.com/github/copilot-cli.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-24

## Today’s Highlights

A burst of quality-of-life fixes landed today, led by lihailong00 with 12 PRs tackling MCP session reuse, Windows UTF‑8 support, shell completion limits, and more. Meanwhile, the community flagged a critical plugin crash on Windows and a worker‑pool deadlock on Linux, while the long‑standing “Remote Control” feature request (#1282) continues to garner strong interest (16 👍). No new releases were published in the last 24 hours.

## Releases

No new releases in the past 24 hours.

## Hot Issues

1. **[#1282 – Remote Control: Continue local sessions from any device](https://github.com/MoonshotAI/kimi-cli/issues/1282)** (👍16)  
   *Created Feb 2026, updated Jul 23*  
   The most‑popular open feature request. Users want to seamlessly resume a Kimi CLI session from a phone, tablet, or browser. Six comments indicate strong interest in workflow continuity.

2. **[#2555 – Discussion: A‑share quantification + AI Agent practice](https://github.com/MoonshotAI/kimi-cli/issues/2555)**  
   *New today, 0 comments*  
   A community member shares insights from building a financial‑trading agent using Hermes Agent (220k⭐). Highlights the importance of real PnL feedback loops and parameter‑driven over hardcoded strategies. Early but promising cross‑domain discussion.

3. **[#2553 – /plugins crashes with TypeError when 2+ plugins installed (v0.29.0, Windows)](https://github.com/MoonshotAI/kimi-cli/issues/2553)**  
   *Opened Jul 23*  
   `/plugins` screen crashes with `Cannot read properties of undefined (reading 'value')` when ≥2 plugins are installed. Works fine with 0 or 1 plugin. A high‑priority bug for Windows users.

4. **[#2552 – Poor font kerning for Cyrillic text in Kimi Desktop](https://github.com/MoonshotAI/kimi-cli/issues/2552)**  
   *Opened Jul 23*  
   Cyrillic letters in markdown blocks exhibit uneven spacing, making text hard to read on Windows. Affects localization UX for Russian/Ukrainian users.

5. **[#2545 – Synchronize queued prompts to backend for phone users](https://github.com/MoonshotAI/kimi-cli/issues/2545)**  
   *Opened Jul 23*  
   Phone users who switch apps or lock the screen lose queued prompts because they aren’t sent when the browser is backgrounded. Requests background sync to improve mobile experience.

6. **[#2538 – kimi‑datasource plugin worker pool blocks all sessions on timeout](https://github.com/MoonshotAI/kimi-cli/issues/2538)**  
   *Opened Jul 23*  
   When multiple sessions use the `kimi-datasource` (yahoo_finance) plugin, a single timeout in the worker pool blocks all sessions simultaneously. A concurrency bottleneck affecting multi‑session workflows.

## Key PR Progress

1. **[#2548 – fix(mcp): reuse initialized client sessions](https://github.com/MoonshotAI/kimi-cli/pull/2548)**  
   Prevents re‑initialization of MCP clients on every tool call. Keeps sessions open via `AsyncExitStack`, fixing a strict‑stdio MCP server that rejected duplicate `initialize` messages.

2. **[#2547 – fix(windows): configure stdio as utf‑8](https://github.com/MoonshotAI/kimi-cli/pull/2547)**  
   Sets Windows stdout/stderr to UTF‑8 at startup when the stream supports reconfigure. Resolves broken rendering on cp936 terminals without affecting redirected output.

3. **[#2537 – fix(shell): support numeric keypad input](https://github.com/MoonshotAI/kimi-cli/pull/2537)**  
   Recognizes DEC application‑keypad sequences from Windows Terminal, allowing digit keys on the numeric keypad to be inserted into the prompt buffer.

4. **[#2542 – fix(logging): isolate Windows process log files](https://github.com/MoonshotAI/kimi-cli/pull/2542)**  
   Uses `kimi.<pid>.log` on Windows to avoid log file rotation conflicts when multiple Python processes run concurrently.

5. **[#2551 – fix(shell): search past file completion limit](https://github.com/MoonshotAI/kimi-cli/pull/2551)**  
   Improves `@` file completion to search beyond the first 1000 filesystem entries while keeping result/bound budgets at 1000/10000.

6. **[#2549 – fix(shell): index tracked vendor files](https://github.com/MoonshotAI/kimi-cli/pull/2549)**  
   Allows Git‑tracked files under `vendor/` to appear in `@` completions, while still filtering `node_modules` and untracked vendor trees.

7. **[#2539 – fix(mcp): normalize tools for Moonshot API](https://github.com/MoonshotAI/kimi-cli/pull/2539)**  
   Generates stable Moonshot‑compatible aliases for MCP tool names and fixes schema shapes for `anyOf`/`required` to align with the Moonshot API.

8. **[#2541 – fix(mcp): continue after deferred startup failure](https://github.com/MoonshotAI/kimi-cli/pull/2541)**  
   Catches `MCPRuntimeError` during background MCP startup so an optional failure doesn’t abort the interactive turn.

9. **[#2546 – fix(print): escape markup in echoed stdin prompts](https://github.com/MoonshotAI/kimi-cli/pull/2546)**  
   Renders user stdin prompts literally (e.g., `[/login]`) instead of interpreting them as Rich markup, keeping the model’s input unchanged.

10. **[#2540 – fix(media): normalize ICO images to PNG](https://github.com/MoonshotAI/kimi-cli/pull/2540)**  
   Converts ICO image payloads to PNG before sending to the model, preserving metadata while ensuring compatibility.

## Feature Request Trends

- **Remote session continuity** – [#1282](https://github.com/MoonshotAI/kimi-cli/issues/1282) (remote control) and [#2545](https://github.com/MoonshotAI/kimi-cli/issues/2545) (background prompt sync) both target the ability to start a session on one device and continue on another, especially from phone to desktop.  
- **Plugin ecosystem stability** – The growing number of plugins (datasource, MCP) is driving requests for better isolation, timeout handling, and UI reliability.  
- **Cross‑domain AI agent integration** – [#2555](https://github.com/MoonshotAI/kimi-cli/issues/2555) shows interest in applying Kimi’s agent architecture to financial trading, hinting at demand for more generic agent frameworks.

## Developer Pain Points

- **Plugin crashes on Windows** – [#2553](https://github.com/MoonshotAI/kimi-cli/issues/2553) shows a specific `/plugins` TypeError that only appears when more than one plugin is installed, making the plugin management UI unusable on Windows.  
- **Concurrency deadlocks in plugin workers** – [#2538](https://github.com/MoonshotAI/kimi-cli/issues/2538) highlights a worker pool design that can block all sessions when a single plugin call times out — a critical issue for multi‑tasking users.  
- **Localisation / font issues** – [#2552](https://github.com/MoonshotAI/kimi-cli/issues/2552) (Cyrillic kerning) underscores that rendering quality for non‑Latin scripts is still lacking in the desktop client.  
- **MCP initialization fragility** – Multiple PRs ([#2548](https://github.com/MoonshotAI/kimi-cli/pull/2548), [#2541](https://github.com/MoonshotAI/kimi-cli/pull/2541), [#2539](https://github.com/MoonshotAI/kimi-cli/pull/2539)) address bugs where MCP sessions fail to reuse, crash on deferred startup, or produce incompatible tool schemas — reflecting a still‑maturing MCP integration.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-07-24

## Today’s Highlights
No new releases landed in the last 24 hours, but the community remains highly active with critical billing bugs and long-requested usability improvements. The hottest threads revolve around false-positive content filters charging users for blocked outputs (#35475) and a long-standing request to auto-discover models from OpenAI-compatible providers (#6231, 187 👍). On the PR side, contributors are making progress on stabilizing tool definitions, fixing session-change panels, and improving subagent attachment handling, while several 2.0 performance issues continue to gather attention.

## Releases
No releases in the last 24 hours.

## Hot Issues
1. **[#6231 – Auto-discover models from OpenAI-compatible provider endpoints](https://github.com/anomalyco/opencode/issues/6231)**  
   *Open • 30 comments • 187 👍*  
   The most upvoted open issue. Users must manually list models for local providers like LM Studio and Ollama, which breaks each time models change. A model‑discovery feature would dramatically improve the onboarding and day‑to‑day experience.

2. **[#37012 – [FEATURE] keep legacy layout option](https://github.com/anomalyco/opencode/issues/37012)**  
   *Open • 29 comments • 30 👍*  
   Many long‑time users prefer the old layout’s one‑click access to everything. The new navigation requires extra clicks, and the workspace feature is missed. This is a hot topic in the UI debate.

3. **[#37716 – Internal Server Error](https://github.com/anomalyco/opencode/issues/37716)**  
   *Closed • 26 comments*  
   A widespread crash when using OpenCode Go with various models. The error stack suggests a generic server issue; closed but still referenced in other threads.

4. **[#25848 – [FEATURE]: add session renaming](https://github.com/anomalyco/opencode/issues/25848)**  
   *Open • 11 comments*  
   A simple but frequently requested quality‑of‑life feature: the ability to rename sessions manually via `/rename` or CLI. No thumbs, but consistent demand.

5. **[#35475 – False positive content-filter on claude-fable-5 — charged ~$20 for blocked output](https://github.com/anomalyco/opencode/issues/35475)**  
   *Open • 10 comments*  
   A serious billing bug: benign queries trigger the content filter, yet the full generation cost (≈$6.69 per call) is charged. Combined with #35643, this is a top priority for the team.

6. **[#37326 – math equations not rendered](https://github.com/anomalyco/opencode/issues/37326)**  
   *Open • 7 comments*  
   Mathematical output (e.g., LaTeX) is not rendered in the Desktop app. A blocker for scientific and educational users.

7. **[#26220 – Bug: OpenCode enters infinite loop after tool calls complete (Zen/big-pickle)](https://github.com/anomalyco/opencode/issues/26220)**  
   *Open • 7 comments • 3 👍*  
   A hard hang that locks the process after tool execution. Affects older versions; users are eager for a fix.

8. **[#36285 – [bug, perf, 2.0] 2.0: managed-service restart causes reconnect herd and resource spikes](https://github.com/anomalyco/opencode/issues/36285)**  
   *Closed • 5 comments*  
   A V2 performance bug where automatic updates trigger a “reconnect herd,” cold‑booting many location graphs and causing slow rendering. Parent of benchmark issue #38569.

9. **[#38255 – Discrepancy between different opencode go usage dashboard](https://github.com/anomalyco/opencode/issues/38255)**  
   *Open • 5 comments*  
   Users see 100% monthly usage but only ~$10 in the granular view. A confusing billing inconsistency that needs alignment.

10. **[#38564 – Subagent termination does not kill spawned child processes (disk abuse risk)](https://github.com/anomalyco/opencode/issues/38564)**  
    *Open • 2 comments*  
    When a subagent is cancelled, PowerShell child processes continue running at 100% I/O. A serious resource leak reported by a new contributor.

## Key PR Progress
1. **[#38594 – feat(app): add reasoning and token limits to custom providers](https://github.com/anomalyco/opencode/pull/38594)**  
   *Open • New*  
   Adds configuration fields for “Enable Reasoning”, “Context Size”, etc. to custom provider forms. Addresses #38593.

2. **[#38592 – fix: session changes panel always empty](https://github.com/anomalyco/opencode/pull/38592)**  
   *Open • New*  
   Restores session‑level diff computation so the “Session Changes” panel shows modified files. Affects TUI, Desktop, and Web.

3. **[#38590 – fix(core): stabilize tool definition ordering](https://github.com/anomalyco/opencode/pull/38590)**  
   *Closed*  
   Emits tool definitions in canonical order to produce byte‑identical arrays regardless of plugin registration order – stabilizes provider prompt‑cache prefixes.

4. **[#38584 – fix(opencode): recover projects moved to a new path](https://github.com/anomalyco/opencode/pull/38584)**  
   *Open • New*  
   When a Git repository is moved, the stored project now correctly tracks the live path instead of keeping the missing original worktree.

5. **[#38588 – fix(codemode): stabilize catalog ordering](https://github.com/anomalyco/opencode/pull/38588)**  
   *Closed*  
   Renders Code Mode discovery catalogs in canonical dotted‑path order to prevent false `core/codemode` instruction updates.

6. **[#38581 – fix(opencode): preserve grep symlink paths](https://github.com/anomalyco/opencode/pull/38581)**  
   *Open • New*  
   Grep no longer canonicalizes symlinked search paths, so subsequent tool calls find the correct files. Closes #38582.

7. **[#32302 – fix(opencode): forward parent attachments to subagents](https://github.com/anomalyco/opencode/pull/32302)**  
   *Open • 2 months old*  
   Fixes attachment handoff when using `@mention` subagents in the task path. Closes #25553.

8. **[#38183 – feat(core): render CodeMode catalog deltas from structured snapshots](https://github.com/anomalyco/opencode/pull/38183)**  
   *Open • New*  
   Moves Code Mode catalog prompting into core and upgrades instruction source from whole‑string replacement to semantic delta rendering. Part of #36196.

9. **[#38579 – feat(mcp): forward plugin request metadata](https://github.com/anomalyco/opencode/pull/38579)**  
   *Open • New*  
   Allows plugins to pass optional `_meta` fields to MCP tool calls. Closes #17084; builds on earlier work (#21624).

10. **[#38539 – fix(tui): preview written file content](https://github.com/anomalyco/opencode/pull/38539)**  
    *Open • New*  
    Render file writes as block cards with real before/after diffs, instead of single‑line tool rows. Distinguishes new files from overwrites.

## Feature Request Trends
The most‑requested feature categories from this week’s issues are:

- **Model & Provider Management**: Auto‑discovery of models from OpenAI‑compatible endpoints (#6231) and configurable reasoning/token limits for custom providers (#38594).
- **UI Customisation**: Keeping the legacy layout (#37012), session renaming (#25848), and dedicated sub‑agent output views (#37267).
- **Display & Internationalisation**: Rendering of math equations (#37326), support for RTL languages (#6284), and showing reasoning levels for sub‑agents (#26266).
- **Mobile Integration**: Connecting a mobile device to monitor terminal output and send tasks (#33163).

## Developer Pain Points
Several recurring frustrations stand out:

- **Billing & filtering issues**: Content filters that block output but still charge users (#35475, #35643) and inconsistent usage dashboards (#38255) are causing financial mistrust.
- **Platform‑specific bugs**: The `@` symbol for file references is completely broken on Windows (#29859), and the npm package rejects FreeBSD (#38591). These block users on non‑mainstream platforms.
- **Performance and stability hangs**: Infinite loops after tool calls (#26220), UI freezes on single core (#38565), and reconnect herds in V2 (#36285) degrade the daily experience.
- **Sub‑agent and permission reliability**: Subagent cancellation leaves orphan child processes (#38564), `--auto` hang on permission requests (#36868), and “Always Allow” not persisting (#37880) undermine automation workflows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-24

---

## Today’s Highlights
The community is focused on better model configuration reliability and provider ergonomics: a fix for the lost hot-reload of `models.json` (PR #7036) and a new constrained sampling feature for tools (PR #6341) are under active review. Clipboard handling on Wayland and hard‑coded token limits for llama.cpp have been addressed by multiple contributors, while requests for a built‑in SiliconFlow provider and Qwen‑compatible reasoning tiers signal growing demand for model‑provider diversity.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **#6306 – Support Strict Tools / Grammar** [CLOSED]  
   *Important discussion on adding grammar‑aware “free form” or “strict” tool input generation, similar to OpenAI’s `strict` parameter. The conversation ties into constrained sampling and LARK/Rust regex patterns.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6306)

2. **#3252 – Add setting to prevent `/model` from overwriting the persistent default model** [CLOSED]  
   *Users want a way to switch models for a session without changing the startup default in `settings.json`. A recurring request for better model state management.*  
   [View Issue](https://github.com/earendil-works/pi/issues/3252)

3. **#6886 – Support Anthropic’s server‑side Fable‑to‑Opus fallback in pi‑ai** [CLOSED]  
   *Enabling server‑side fallback when using Fable requests to Anthropic. The author plans to implement if approved, reflecting demand for flexible provider routing.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6886)

4. **#5013 – TUI transcript rewrites ordered‑list numbers** [CLOSED]  
   *A subtle bug where the TUI reformats ordered lists in the transcript, causing confusion in collaborative writing. Highlights the need for faithful markdown rendering.*  
   [View Issue](https://github.com/earendil-works/pi/issues/5013)

5. **#6951 – Qwen3.8‑max‑preview reasoning effort mapping mismatch** [OPEN]  
   *Pi’s reasoning effort tiers (`minimal`, `low`, `medium`, `high`) don’t match Qwen’s API (`low`, `medium`, `xhigh`). A simple but critical compatibility issue for Qwen users.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6951)

6. **#6999 – Restore models.json hot‑reload on `/model` after v0.80.8+** [OPEN]  
   *Post‑ModelRuntime update removed the ability to edit `models.json` mid‑session without restarting. Users rely on this workflow for dynamic provider configuration.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6999)

7. **#6994 – Llama provider has a hardcoded maxTokens limit** [CLOSED]  
   *`maxTokens` capped at 16,384 with no way to override. Affects users with models that have larger context windows. Fixed by PR #7034.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6994)

8. **#6749 – API error response bodies are sometimes ignored** [CLOSED]  
   *When connecting Pi to OpenAI‑compatible backends, validation errors are sometimes displayed as `(no body)`, making debugging nearly impossible.*  
   [View Issue](https://github.com/earendil-works/pi/issues/6749)

9. **#7012 – `wl‑copy` exit code never awaited** [CLOSED]  
   *Wayland clipboard failures go unnoticed because the spawn is `unref()’d`. The function reports success even when `wl‑copy` crashes, blocking fallback to `xclip`.*  
   [View Issue](https://github.com/earendil-works/pi/issues/7012)

10. **#6948 – Default model not applied at startup due to race condition** [OPEN]  
    *When `defaultProvider` and `defaultModel` are set, the session starts with the wrong model because the async model refresh hasn’t completed. Frustrating for new users.*  
    [View Issue](https://github.com/earendil-works/pi/issues/6948)

---

## Key PR Progress

1. **#6341 – feat(ai): support constrained sampling** [CLOSED]  
   *Adds an opt‑in `constrainedSampling` config for tools, enabling provider‑side strict tool input generation (JSON‑schema or grammar‑based). A long‑awaited feature for deterministic tool calls.*  
   [View PR](https://github.com/earendil-works/pi/pull/6341)

2. **#7036 – fix(coding‑agent): reload model config in picker** [OPEN]  
   *Directly addresses #6999 by restoring mid‑session hot‑reload of `models.json` when opening the model picker. Author suggests a cleaner API for `reloadConfig`.*  
   [View PR](https://github.com/earendil-works/pi/pull/7036)

3. **#7034 – fix(coding‑agent): use llama context for output limit** [CLOSED]  
   *Removes the hardcoded 16,384‑token cap for llama.cpp providers; now derives the limit from each loaded model’s context window. Fixes #6994.*  
   [View PR](https://github.com/earendil-works/pi/pull/7034)

4. **#7032 – fix(coding‑agent): expose unavailable scoped models** [OPEN]  
   *Model resolution now surfaces structured diagnostics for configured models that are no longer available. Allows users to view and remove stale entries from `/scoped‑models`.*  
   [View PR](https://github.com/earendil-works/pi/pull/7032)

5. **#7017 – feat(tui): Experimental support for limited repainting** [CLOSED]  
   *Adds a setting to limit repainting of the entire transcript for very long sessions. A performance boost for power‑users with extensive conversation histories.*  
   [View PR](https://github.com/earendil-works/pi/pull/7017)

6. **#7011 – fix(coding‑agent): share host modules with native esm extensions** [OPEN]  
   *Fixes a module duplication issue where ESM extensions load private copies of Pi packages, causing state divergence. Intercepts native imports to reuse host modules.*  
   [View PR](https://github.com/earendil-works/pi/pull/7011)

7. **#7009 – fix: await wl‑copy exit code and fall through to xclip on failure** [CLOSED]  
   *Rolls up fixes for #7012 and #6872: `/copy` now checks `wl‑copy`’s exit code before claiming success, enabling fallback to `xclip`/OSC 52 when Wayland is unavailable.*  
   [View PR](https://github.com/earendil-works/pi/pull/7009)

8. **#6980 – fix(ai): make provider retries abortable** [CLOSED]  
   *Replaces Anthropic/OpenAI SDK internal retries with a common helper that respects `maxRetrayDelayMS` and is interruptible via `AbortSignal`. Improves responsiveness during network hiccups.*  
   [View PR](https://github.com/earendil-works/pi/pull/6980)

9. **#6965 – fix: isolate test environment** [CLOSED]  
   *Hardens the test suite by running from an explicit environment allowlist, isolating home, temp, Git, npm, and XDG state. Prevents flaky failures from contaminated environments.*  
   [View PR](https://github.com/earendil-works/pi/pull/6965)

10. **#5735 – fix(coding‑agent): defer extension reload requests safely** [OPEN]  
    *Makes extension reload calls safe from any context (not just slash commands) by deferring them to safe boundaries. Enables `ctx.reload()` with coordination by `AgentSession`.*  
    [View PR](https://github.com/earendil-works/pi/pull/5735)

---

## Feature Request Trends

- **Provider Flexibility** – Requests for built‑in support for SiliconFlow (aggregator similar to OpenRouter), configurable Anthropic server‑side fallback, and Qwen‑compatible reasoning effort tiers. Users want easy onboarding without manual `models.json` hacks.  
- **Tool & Argument Handling** – Demand for strict/grammar‑constrained tool sampling, `argument‑hint` frontmatter for skills (mirroring prompts), and normalized optional object schemas for OpenAI‑compatible providers.  
- **Session & Model Management** – Persistent default model control, hot‑reload of model configs mid‑session, and per‑provider scope refresh (as requested in #7040).  
- **TUI Text Editing** – Standard keyboard text selection (non‑Vim), CJK/wide‑character cursor positioning fixes, and better markdown fidelity (e.g., ordered‑list rewriting).  
- **Security & Credential Handling** – Better OAuth scopes for OpenAI Codex token refresh, and avoiding token invalidation when used alongside other tools (e.g., Copilot LSP).

---

## Developer Pain Points

1. **Clipboard Failures in Restricted Environments** – Multiple issues (#7012, #6872, #7009) report `/copy` silently failing under sandboxed or headless setups because `wl‑copy` exit codes were ignored. The community fixed this with proper fallback logic.  
2. **Hard‑coded Provider Limits** – llama.cpp’s 16k output cap (#6994) and Qwen reasoning effort mismapping (#6951) show that provider‑specific defaults need to be documented and overridable.  
3. **API Error Bodies Discarded** – #6749 highlights a debugging nightmare: error responses from OpenAI‑compatible endpoints often show `(no body)` because the response parsing bypasses the body.  
4. **Model Configuration Race Conditions** – #6948 and #6999 demonstrate that model state is brittle on startup and mid‑session, forcing restarts or manual interference.  
5. **Unicode & Locale Handling** – CJK text breaks vertical cursor movement (#7021) and home‑path abbreviation (#7006) misinterprets directory names. These are classic encoding‑sensitive bugs.  
6. **Extension & Package Management** – Malformed package manifests crash‑loop the session (#7033), and extensions that register `resource_discover` corrupt skill scopes (#6968). The ecosystem needs better validation and isolation.  
7. **Shared State Across Git Worktrees** – `.pi/workflow.json` is tracked and shared across branches (#7039), blocking task creation when switching contexts. A request for workspace‑scoped state.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-24

## Today‘s Highlights

The Qwen Code project shipped a nightly release focused on telemetry robustness and performance. Community discussion centered on a major proposal for an **enterprise external-memory integration profile** and a growing frustration with **E2E test flakiness** on the main branch. Several important bugs were closed, including fixes for npm 12 update-check compatibility and MCP server transport timeouts.

---

## Releases

- **v0.20.1-nightly.20260724.7d17c44a3** — Test coverage for daemon metrics initialization ordering and a general `perf` improvement. No notable user-facing changes.
    - [Release Notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.1-nightly.20260724.7d17c44a3)

---

## Hot Issues (Top 10)

| # | Issue | Why It Matters |
|---|-------|----------------|
| 1 | [#5736 – More full prompt reprocessing in recent update?](https://github.com/QwenLM/qwen-code/issues/5736) | Users are seeing **increased full-prompt re-evaluation** (via llama.cpp) when merely continuing a conversation. Community upvoted and closed with welcome-pr — suggests a caching regression. |
| 2 | [#7147 – MCP server never successfully get tool and resource listing](https://github.com/QwenLM/qwen-code/issues/7147) | Fastmail MCP server integration **times out** during tool listing. Authentication succeeds but tool discovery fails — blocks a popular third-party integration. |
| 3 | [#7599 – Workspace artifacts created via record_artifact have no managedId](https://github.com/QwenLM/qwen-code/issues/7599) | Internally created workspace files (e.g., HTML) **lack a managedId**, breaking the SSE artifact_changed event. Impacts downstream tooling that relies on managed-artifact contracts. |
| 4 | [#7449 – Proposal: Enterprise external-memory integration profile](https://github.com/QwenLM/qwen-code/issues/7449) | A **provider-neutral specification** for connecting Qwen Code to enterprise knowledge stores. Documentation-first approach with incremental compatibility tests — has strong consensus from maintainers. |
| 5 | [#7516 – Main CI failed: E2E Tests](https://github.com/QwenLM/qwen-code/issues/7516) | Repeated **E2E failures on main** are causing noise and blocking merges. Labels suggest auto-fix is skipped, leaving a growing pile of flaky-test issues. |
| 6 | [#7485 – TUI: large blank area between last message and input prompt after resume](https://github.com/QwenLM/qwen-code/issues/7485) | After `qwen resume`, the terminal UI shows an **unusable blank gap** pushing the input field far from the conversation. Triggered across multiple terminal emulators. |
| 7 | [#7264 – Cold-start follow-ups: remaining lazy-loading candidates](https://github.com/QwenLM/qwen-code/issues/7264) | An audit found **17.24 MiB / 2420 modules** eagerly loaded on every cold start of the ACP child process. Tracks leftover candidates after earlier lazy-loading improvements — performance-critical for CLI startup. |
| 8 | [#6014 – New version no longer shows what file the agent read](https://github.com/QwenLM/qwen-code/issues/6014) | UI regression: `read 1 file` replaced specific file names. Community feels this is a **downgrade in transparency** — the issue has gone unanswered for weeks. |
| 9 | [#6806 – Status line context usage % does not refresh after /compress](https://github.com/QwenLM/qwen-code/issues/6806) | After running `/compress` or `/compress-fast`, the **context percentage stays stuck** at the pre-compression value until the next model request — misleading for power users managing long sessions. |
| 10 | [#7520 – npm 12 compatibility: view command returns an array, breaking update check](https://github.com/QwenLM/qwen-code/issues/7520) | **npm 12 (Node 26)** changed the `npm view` output format, causing Qwen Code’s update check to always fail with *registry error*. Quick community fix merged. |

---

## Key PR Progress (Top 10)

| # | PR | What It Does |
|---|----|--------------|
| 1 | [#7268 – Hot-reload workspace trust changes](https://github.com/QwenLM/qwen-code/pull/7268) | Enables **runtime workspace trust policy changes** without daemon restart. Uses semantic snapshots and generation reconciliation — a foundational change for multi-tenant setups. |
| 2 | [#7497 – Native video input in /learn](https://github.com/QwenLM/qwen-code/pull/7497) | Adds **MP4/WebM/MOV video support** to the `/learn` command, gated on model video modality. Opens up rich-media learning workflows. |
| 3 | [#7632 – GitHub polling adapter with notification-as-wakeup](https://github.com/QwenLM/qwen-code/pull/7632) | A **GitHub channel adapter** that polls GitHub notifications and responds to @mentions via comments. Redesigned from scratch using a wakeup architecture — promising for bot/automation use cases. |
| 4 | [#7607 – Configurable image generation models](https://github.com/QwenLM/qwen-code/pull/7607) | Users can now **select a separate image-generation model** via `/model --image`, with built-in approval-gated tooling — expands multimodal capabilities. |
| 5 | [#7589 – Show tool descriptions in multi-tool compact summaries](https://github.com/QwenLM/qwen-code/pull/7589) | Fixes a UI regression where **grouped tool summaries** (e.g., “Read 2 files”) hid the actual file paths — restores transparency in agent actions. |
| 6 | [#7302 – Reference prior sessions via @ and add completion tabs](https://github.com/QwenLM/qwen-code/pull/7302) | Introduces **`@session:` references** in the interactive shell, with completion tabs and read-only transcript injection — powerful for context reuse. |
| 7 | [#7594 – Propagate compile cache to ACP children](https://github.com/QwenLM/qwen-code/pull/7594) | Passes Node’s compile-cache directory to **ACP child processes**, reducing cold-start parse time. Follows the recent 17 MiB eager-closure audit. |
| 8 | [#7603 – Harden Java SDK daemon transport reliability](https://github.com/QwenLM/qwen-code/pull/7603) | Adapts the Java SDK to the **restart-safe event cursor contract**, adding `eventEpoch` + `lastEventId` pairing — critical for production daemon resilience. |
| 9 | [#7195 – Use dedicated undici fetch for MCP Streamable HTTP](https://github.com/QwenLM/qwen-code/pull/7195) | Fixes **SSE stream timeout** by switching MCP HTTP transport to undici’s own fetch with relaxed timeout defaults — resolves a long-standing integration pain point. |
| 10 | [#6506 – Optimize large paste performance and add progress indicator](https://github.com/QwenLM/qwen-code/pull/6506) | Intercepts bracketed-paste markers to **bypass per-character event firing**, reducing 260K-char paste processing from ~1.7s to near-instant — a major UX win for power users. |

---

## Feature Request Trends

- **External Memory & Enterprise Integration** – Two complementary proposals ([#7449](https://github.com/QwenLM/qwen-code/issues/7449), [#7585](https://github.com/QwenLM/qwen-code/issues/7585)) seek to standardize how Qwen Code connects to external knowledge stores, targeting enterprise deployment.
- **Channel & Bot Enhancements** – Strong interest in **GitHub polling adapters** ([#7632](https://github.com/QwenLM/qwen-code/pull/7632)), **Telegram topic routing** fixes ([#7609](https://github.com/QwenLM/qwen-code/issues/7609)), and **WeChat channel** support ([#7590](https://github.com/QwenLM/qwen-code/issues/7590)).
- **Rich Media Input** – Requests for **native video learning** ([#7497](https://github.com/QwenLM/qwen-code/pull/7497)) and **image generation models** ([#7607](https://github.com/QwenLM/qwen-code/pull/7607)) indicate growing demand for multimodal agent workflows.

---

## Developer Pain Points

- **E2E Test Flakiness on Main** – A recurring frustration ([#7516](https://github.com/QwenLM/qwen-code/issues/7516), [#7559](https://github.com/QwenLM/qwen-code/issues/7559), [#7605](https://github.com/QwenLM/qwen-code/issues/7605), [#7616](https://github.com/QwenLM/qwen-code/issues/7616)): non-deterministic model API responses and slow docker sandboxes cause false CI failures, blocking merges and eroding trust.
- **Update Check Breakage** – The npm 12 compatibility issue ([#7520](https://github.com/QwenLM/qwen-code/issues/7520), [#7543](https://github.com/QwenLM/qwen-code/issues/7543)) caused *registry error* for users upgrading to Node 26, mirroring a separate mise-path bug — two distinct update failures in two days.
- **Session Resumption & UI Regressions** – The **TUI blank gap** after resume ([#7485](https://github.com/QwenLM/qwen-code/issues/7485)), **stale context percentage** ([#6806](https://github.com/QwenLM/qwen-code/issues/6806)), and **missing file names** in agent reads ([#6014](https://github.com/QwenLM/qwen-code/issues/6014)) are eroding the interactive experience.
- **Memory & Artifact Consistency** – Auto-memory not registered in FileReadCache ([#7287](https://github.com/QwenLM/qwen-code/issues/7287)) and workspace artifacts lacking managedId ([#7599](https://github.com/QwenLM/qwen-code/issues/7599)) point to deeper integration gaps between memory, caching, and artifact tracking.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-24

## Today's Highlights
The CodeWhale repository (formerly DeepSeek TUI) saw a burst of 15+ issues filed in the last 24 hours, exposing significant reliability and security gaps ahead of the v0.9.1 release. Key themes include concurrent corruption in JSONL logging, silent config parsing failures, and a stop-ship TUI crash on macOS. Four PRs advanced UI fixes, with two merged and two still open. No new releases were tagged today.

## Releases
No new releases were published in the last 24 hours. The latest candidate is **v0.9.1 (0dfe9170)** which is under a security gate review (Issue #4713).

## Hot Issues (10 of 26 updated in last 24h)

1. **#4741** — [CLOSED] `JsonlHookSink` lacks write synchronization; concurrent tool calls corrupt JSONL logs. Quick fix merged.  
   *Why it matters*: Race condition in core logging can silently lose event data. Community commented once (merged quickly).  
   [GitHub](Hmbown/CodeWhale Issue #4741)

2. **#4716** — [OPEN, stop-ship] `codew` TUI exits immediately with "[Process completed]" on fresh macOS Terminal.  
   *Why it matters*: Blocks all TUI usage on Mac Studio. No fix yet. 1 comment.  
   [GitHub](Hmbown/CodeWhale Issue #4716)

3. **#4719** — [OPEN] Composer pastes large prompts get byte-corrupted before submission (paths truncated, lines mangled).  
   *Why it matters*: Downstream agents act on corrupted input – dangerous. 2 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4719)

4. **#4727** — [OPEN] `codewhale mcp-server` never spawns real MCP servers; always returns fabricated stub responses.  
   *Why it matters*: Documented CLI command is completely broken. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4727)

5. **#4733** — [OPEN] Malformed project `config.toml` silently treated as "no config".  
   *Why it matters*: Users may think their custom settings are applied when they are not. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4733)

6. **#4734** — [OPEN] SQLite connection lacks `busy_timeout`/WAL mode; concurrent processes fail hard.  
   *Why it matters*: Multi-process workflows (Fleet, MCP) will deadlock. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4734)

7. **#4738** — [OPEN] stdio JSON-RPC loop is sequential and uncancellable; shutdown cannot abort in-flight turns.  
   *Why it matters*: Graceful shutdown is impossible, leading to zombie processes. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4738)

8. **#4740** — [OPEN] `denied_prefixes` rules bypassed by inserting a flag before the subcommand (e.g., `git --verbose push`).  
   *Why it matters*: Security policy evasion – high severity. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4740)

9. **#4729** — [OPEN] MCP tool name sanitization can cause collisions across differently-named servers (e.g., `server-a` and `server_a` become identical).  
   *Why it matters*: Ambiguous tool selection could invoke wrong server’s tool. 0 comments.  
   [GitHub](Hmbown/CodeWhale Issue #4729)

10. **#4736** — [OPEN] Session-index compaction can silently drop entries appended by concurrent processes.  
    *Why it matters*: Data loss under concurrent use. 0 comments.  
    [GitHub](Hmbown/CodeWhale Issue #4736)

## Key PR Progress (4 updated in last 24h)

1. **#4724** — [OPEN] `fix(tui): archive completed background shell output` — Finalizes shell job output into its originating cell, freezes duration. Improves UI consistency. By qinlinwang.  
   [GitHub](Hmbown/CodeWhale PR #4724)

2. **#4346** — [CLOSED] `fix: sanitize tool input_schema for Anthropic adapter` — Prevents HTTP 400 when `input_schema` contains `oneOf`/`anyOf`/`allOf`. Critical for Anthropic users. By qinlinwang.  
   [GitHub](Hmbown/CodeWhale PR #4346)

3. **#4722** — [OPEN] `fix(tui): show complete edit previews in details` — Keeps compact approval card but renders full diff in Alt+V pager. Adds regression test. By nightt5879.  
   [GitHub](Hmbown/CodeWhale PR #4722)

4. **#4610** — [OPEN] `feat(tui): add configurable session token header` — Adds opt-in token breakdown to TUI header (input, cache, output). References #4520. By XhesicaFrost.  
   [GitHub](Hmbown/CodeWhale PR #4610)

## Feature Request Trends
- **Dynamic provider/model switching** – multiple issues (#4720, #4717) call for clearer, more intentional behavior when runtime switches providers (e.g., DeepSeek → ZAI).
- **Customizable header items** – PR #4610 reflects community desire for token counters and other contextual info in the TUI header.
- **Concurrent-safe state & logging** – Several issues (#4734, #4735, #4736) implicitly request WAL-mode SQLite, read-write locks, and atomic compaction to support multi-process workflows.
- **Security hardening** – Frequent requests for proper denial-of-service protections (#4740, #4726, #4725) and tool name collision avoidance (#4729).
- **Platform-friendly keyboard handling** – #4723 requests Windows AltGr key support for non-US layouts.

## Developer Pain Points
- **Silent failures** – Malformed configs (#4733), corrupted prompts (#4719), and broken MCP subcommand (#4727) all fail without clear error messages, wasting developer time.
- **Concurrency bugs** – Unsynchronized file writes (#4741, #4739), non-cancellable RPC (#4738), and race conditions in state (#4734) cause hard-to-reproduce data corruption.
- **Security bypasses** – Workarounds for denied prefixes (#4740) and allowlist drift (#4730) frustrate teams relying on policy enforcement.
- **TUI usability** – High information density (#4718), immediate crash on macOS (#4716), and legacy DeepSeek branding (#4717) degrade the developer experience.
- **Inconsistent naming** – Sanitized MCP tool names (#4729) collide; workflow branch cleanup never deletes Git branches (#4731).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*