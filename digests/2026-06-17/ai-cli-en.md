# AI CLI Tools Community Digest 2026-06-17

> Generated: 2026-06-17 02:56 UTC | Tools covered: 9

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

# AI CLI Developer Tools: Cross-Tool Comparison Report — 2026-06-17

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a convergence around **agent reliability, MCP ecosystem maturity, and cross-platform parity**, with all major tools facing similar growing pains. The most urgent shared challenge is **agent execution unpredictability**—hangs, silent failures, and malformed tool calls plague Claude Code, Gemini CLI, OpenCode, and CodeWhale alike. Security concerns are escalating across the board, with OAuth token handling (Claude Code, Gemini CLI), symlink traversal (Claude Code), and shell injection (Claude Code) attracting critical PR attention. Meanwhile, the **MCP protocol is becoming the de facto plugin standard** but remains fragile: bearer token delivery, protocol detection, and server-side error handling all show recurring bugs. The ecosystem is clearly in a "stabilization phase" following rapid feature expansion, with reliability and security now outpacing new features as the primary community concern.

---

## 2. Activity Comparison

| Tool | Hot Issues (noteworthy) | PRs in Progress | Release Today | Key Signal |
|------|------------------------|-----------------|---------------|------------|
| **Claude Code** | 10 (4 critical-level) | 10 | ✅ v2.1.179 | Most active; Windows regression heavy |
| **OpenAI Codex** | 10 (3 highly voted) | 10 | ✅ rust alpha releases | Moderate activity; focus on session/UX |
| **Gemini CLI** | 10 (5 p1 bugs) | 10 | ❌ | High bug density; strong security push |
| **GitHub Copilot CLI** | 10 (1 critical crash) | 0 | ✅ v1.0.64-0 | New release but zero new PRs; quiet |
| **Kimi Code CLI** | 4 total | 1 | ❌ | Smallest activity; early-stage project |
| **OpenCode** | 10 (2 >50 comments) | 10 | ❌ | Very active community; feature-rich requests |
| **Pi** | 10 (wide severity range) | 9 | ✅ v0.79.5/6 | Healthy iteration; TUI quirks remain |
| **Qwen Code** | 10 (1 policy hot issue) | 10 | ❌ | Build pipeline issues; strong Asia focus |
| **CodeWhale (DeepSeek)** | 10 (stability dominant) | 8 | ❌ | Active refactoring; pre-v0.9.0 churn |

**Observation**: Claude Code, OpenCode, and Gemini CLI show the highest combined activity. Copilot CLI's zero-PR day is anomalous given a new release. Kimi Code and CodeWhale are smallest but fastest-evolving per-resource.

---

## 3. Shared Feature Directions

The following requirements appear **across three or more tool communities**:

### MCP Ecosystem Maturity
- **OAuth token delivery reliability**: Claude Code (#46140), Gemini CLI (#27664, #27889), Copilot CLI (#2790)
- **MCP server protocol detection**: Copilot CLI (#2790 — SSE vs HTTP misidentification), Kimi Code (#2457 — auto-rediscovery)
- **Better error diagnostics for MCP failures**: Claude Code (#47635), Pi (#5763 → PR #5820), Copilot CLI (#3828 — ContentExclusion crash)

### Session Lifecycle & Persistence
- **Persistent session goals**: OpenCode (#27167 — `/goal`, 87👍), Claude Code (#60699 — `/remote-control`)
- **Session unarchive/restoration**: Copilot CLI (#3518), OpenCode (#27167), Codex (#21128 — hidden conversations)
- **Better context window management**: Claude Code (#65514 — 1M context blocked), Codex (#18052 — out of room), OpenCode (#11286 — limits not respected)

### Token & Cost Transparency
- **Session token budgets**: Codex (PR #28494), Claude Code (#68964 — usage buckets), OpenCode (#24879 — Pro tier)
- **Usage telemetry visibility**: Pi (PR #5809 — timing metrics), Claude Code (#68921 — tool response diffing)
- **Rate limit and quota clarity**: Copilot CLI (#3819 — clearer messages), OpenCode (#27938 — concurrency limits)

### Cross-Platform Parity
- **Windows crash/stability**: Claude Code (#46767 — tool drops), Codex (#27287, #27506), Copilot CLI (#3687 — ARM64), Kimi Code (#2457)
- **glibc/static builds**: CodeWhale (#3238), Qwen Code (#5206), Pi (PR #5801 — Nix flake)
- **macOS resource leaks**: Codex (#27536 — 62GB clone), Gemini CLI (#27628 — PTY leak)

### Agent Guardrails & Safety
- **Destructive operation prevention**: Gemini CLI (#22672 — `git reset --force`), CodeWhale (#3275 — self-participation regression)
- **Authorization fatigue**: Copilot CLI (#1168 — excessive prompts), Qwen Code (#4615 — `.mcp.json` pending approval)
- **Plugin/symlink security**: Claude Code (PR #68689 — symlink escape), Gemini CLI (PR #27966 — case-insensitive blocklist)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|-------------|-------|------------|-------------|----------|-----|-----------|-----------|
| **Core strength** | Scale & breadth | Rust perf | Security-first | Enterprise | Session primitives | Provider flexibility | Language localization | Memory & refactoring |
| **Target persona** | Power devs/ops | Rust devs | Security teams | GitHub ecosystem | TUI-first power users | Multi-provider tinkerers | Asian market devs | DeepSeek community |
| **Key differentiator** | Plugin hooks & MCP depth | Atomic Rust binaries | Thought scrubbing & AST tools | `/mcp registry` + `/diagnose` | `/goal`, `/loop` primitives | Provider-scoped envs, HTTP fallthrough | Vision bridge, QQ Bot | "Hippocampal" memory v2 system |
| **Biggest weakness** | Windows regression density | Session history fragility | Agent hang frequency | Permission fatigue | CPU-bound orchestration | TUI terminal quirks | OAuth pricing uncertainty | Stall/crash critical bugs |

**Technical approach divergence**:
- **Plugin model**: Claude Code, Copilot CLI, and Gemini CLI are converging on MCP. OpenCode and Pi favor plugin architectures. CodeWhale is building a custom skill system.
- **Memory strategy**: CodeWhale is investing in a persistent memory system (PR #2933). Others rely on context window management or external tools.
- **Provider strategy**: Pi and OpenCode are provider-agnostic; Qwen Code and Codex emphasize first-party model integration; Copilot CLI ties to GitHub enterprise.

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
- **Claude Code**: Consistently highest issue/PR volume. The largest, most mature ecosystem with deep plugin hooks. Community is vocal and demanding—signs of widespread production use.
- **OpenCode**: Strikingly high engagement per issue (#27167 at 87👍, #2940 at 39 comments). Feature requests are sophisticated (structured session goals, recursive skill discovery).
- **Gemini CLI**: Very active on security—multiple p1 security PRs today. Bug density suggests a project still stabilizing its agent orchestration layer.

### Moderate Momentum / Consolidating
- **GitHub Copilot CLI**: Strong release today but oddly quiet PR pipeline. Enterprise focus may mean development is behind closed doors. Permissions fatigue is a persistent pain point.
- **OpenAI Codex**: Mix of Rust alpha releases and important UX issues (session hiding, context limits). Feels like a transition phase.
- **Pi**: Healthy, steady iteration. Provider-scoped configs and timing metrics show maturity. Community is smaller but technically sophisticated.

### Early Stage / Smaller Community
- **Qwen Code**: Strong localization focus. The OAuth pricing issue (#3203 at 136 comments) indicates a sensitive community. Build pipeline issues suggest scaling pains.
- **Kimi Code CLI**: Tiny issue set (4 total). New install friction (#2456) reveals early-stage project. Low engagement overall.
- **CodeWhale (DeepSeek TUI)**: Active refactoring toward v0.9.0. Stall/hang bugs (#2487, #2739) dominate sentiment. "Hippocampal" memory system is ambitious but still in PR review.

---

## 6. Trend Signals

### For Tool Developers
1. **MCP is winning, but fragile**: Every major tool is adopting MCP, but OAuth flows, protocol detection, and error handling are consistent failure points. A standardized MCP security and error model would benefit the entire ecosystem.
2. **Agent governance is the next frontier**: Uncontrolled agentic loops, destructive operations, and authorization fatigue are top complaints. The industry needs **configurable guardrails** (permissions scopes, session budgets, approval gates) as a baseline feature.
3. **Cross-platform is not optional**: Windows ARM64 crashes, non-ASCII path failures, glibc dependencies on Linux—these are not edge cases. The community is increasingly demanding **static builds or containerized deployment** as a solution.
4. **Memory persistence is becoming table stakes**: CodeWhale's hippocampal system, OpenCode's `/goal` primitive, and Codex's session history bugs all point to the same need: **long-term, controllable, user-trusted memory** beyond context windows.

### For Tool Adopters (Developers)
5. **Expect breakage during agent delegation**: Across Claude Code, Gemini CLI, and CodeWhale, subagent orchestration is the least reliable component. If your workflow depends on multi-agent delegation, **test extensively and build fallback logic**.
6. **Windows users face disproportionate friction**: All major tools have Windows-specific bugs that are slower to resolve (Claude Code: tool drops, Codex: non-ASCII paths, Copilot CLI: ARM64 crash). Consider **WSL2 or container environments** for production AI CLI use.
7. **OAuth token management remains manual**: Several tools still have open bugs (Claude Code #46140, Gemini CLI #27664) around bearer token delivery. Audit your tool's credential handling if you rely on MCP-based extensions.
8. **Context window anxiety is growing**: Users across tools report hitting hard caps with **no way to reclaim space** mid-session. Tools that implement session budgets, token accounting, and graceful degradation will have a competitive edge.

---

**Bottom line**: The AI CLI tool ecosystem is past the "demo phase"—teams are pushing these tools into production workflows, and the resulting friction is surfacing real engineering challenges. The differentiating tools in 2026 will be those that solve **reliable multi-agent coordination**, **persistent cross-session memory**, and **granular security controls** while maintaining cross-platform reliability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills (2026-06-17)

---

## 1. Top Skills Ranking

The following pull requests have attracted the highest community discussion activity. All remain **OPEN** as of this snapshot.

| # | Skill (PR) | Functionality | Discussion Highlights |
|---|------------|---------------|----------------------|
| #514 | **document-typography** | Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents — a pervasive quality issue. | Broad consensus that typographic polish is critical for professional output; high relevance across all document-producing skills. |
| #486 | **ODT skill** | Full read/write/convert support for OpenDocument Format (.odt, .ods) including templating and ODT→HTML parsing. | Strong interest in LibreOffice/ISO standard interoperability; some discussion on scope boundaries with existing DOCX skill. |
| #210 | **frontend-design (improvement)** | Revises the existing frontend-design skill to be more actionable and internally coherent for Claude’s single‑conversation context. | Focused debate on skill clarity vs. verbosity; representative of the broader tension between instructional completeness and token efficiency. |
| #83 | **skill-quality-analyzer + skill-security-analyzer** | Two meta‑skills that evaluate other skills across structure, documentation, and security dimensions. | Community interest in governance and quality assurance for the skills ecosystem itself; meta‑skills seen as a trust enabler. |
| #538 | **pdf fix (case‑sensitivity)** | Corrects 8 case‑sensitive file references in `skills/pdf/SKILL.md` that break on Linux/Mac. | Small but critical fix; highlights the cross‑platform portability concerns that recur in many skill contributions. |
| #539 | **skill‑creator: unquoted YAML detection** | Pre‑parse validation to catch unquoted `description` fields containing `:`, preventing silent YAML truncation. | Resonates strongly with skill authors who have encountered mysterious loading failures; complements the parallel issue #361. |
| #541 | **docx: tracked change w:id collision** | Fixes document corruption when DOCX skill adds tracked changes to files with existing bookmarks (shared `w:id` space). | Detailed OOXML debugging; shows the depth of domain expertise required for Microsoft Office format skills. |

**Highlights:**
- The **document-typography** PR (#514) has the highest comment count, indicating that textual quality is a top‑of‑mind concern for the community.
- **Meta‑skills** (#83) and **skill‑creator tooling fixes** (#539, #538, #541) signal a maturing ecosystem where contributors care about reliability and reviewability.

---

## 2. Community Demand Trends

From the most‑commented issues, the clearest themes emerge:

| Trend | Key Issue(s) | Description |
|-------|--------------|-------------|
| **Skill sharing & distribution** | #228 (14 comments) | Users urgently want org‑wide sharing (direct links, shared libraries) to replace the manual download‑and‑upload workflow. |
| **Reliability of skill‑creator evaluation** | #556 (12 comments), #1169 (3 comments) | `run_eval.py` reports 0% recall on every iteration, rendering the description‑optimisation loop useless. Multiple independent reproductions. |
| **Cross‑platform compatibility** | #1061 (3 comments), #1050, #1099 | Windows users face subprocess, encoding, and pipe‑selection failures in the skill‑creator scripts. A recurring pain point. |
| **Security & trust boundaries** | #492 (7 comments) | Community skills hosted under the `anthropic/` namespace impersonate official skills — a trust boundary vulnerability. |
| **New skill directions (anticipated)** | #412 (agent‑governance), #1220 (multi‑file bundling), #1175 (SharePoint security) | Users are proposing governance patterns, bundling support, and enterprise‑document security as high‑value additions. |
| **Duplicate skills across plugins** | #189 (6 comments) | `document‑skills` and `example‑skills` plugins install identical content, cluttering the context window. |

**Takeaway:** The community is less focused on adding flashy new skills and more concerned with **reliability of tooling**, **cross‑platform support**, **trust and sharing infrastructure**, and **document‑quality fundamentals**.

---

## 3. High‑Potential Pending Skills

These open PRs have accumulated significant discussion and are likely to be merged in the near term:

| PR | Skill | Why It Matters |
|----|-------|----------------|
| #1298 | **skill‑creator eval fix** | Addresses the 0% recall bug head‑on; 10+ independent reproductions confirm the problem. Critical for any team using the optimisation loop. |
| #361 | **Unquoted YAML detection** (duplicate/similar to #539) | Multiple authors have submitted fixes; the issue is well‑understood and the solution is small. High merge probability. |
| #362 | **UTF‑8 byte‑length validation** | Prevents Rust panics on multi‑byte characters in skill metadata. Essential for international skill authors. |
| #723 | **testing‑patterns skill** | Comprehensive coverage of unit, React, E2E, and accessibility testing. Fills a major gap in the development skill category. |
| #568 | **ServiceNow platform skill** | Broad enterprise platform coverage (ITSM, SecOps, ITAM, etc.). Strong demand from corporate users. |
| #444 | **AURELION skill suite** (kernel, advisor, agent, memory) | A structured cognitive framework for professional knowledge management. Attracts users seeking persistent memory patterns. |
| #154 | **shodh‑memory skill** | Persistent context across conversations. Addresses a fundamental limitation of stateless AI interactions. |

These skills represent the **most mature contributions** that have survived extended review cycles and multiple iterations.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for reliable skill‑authoring tooling, cross‑platform compatibility, and basic document‑quality safeguards — rather than novel domain skills — reflecting a shift from creative experimentation to production‑grade infrastructure.**


---

# Claude Code Community Digest — 2026-06-17

## Today's Highlights
Anthropic shipped **v2.1.179** fixing mid-stream connection drops (partial responses now preserved) and a WSL2 mouse-wheel scrolling regression. A **critical OAuth bug** (#46140) in the MCP connector for claude.ai remains open — the Bearer token is never sent to the server after a successful authorization flow. Meanwhile, the community is reporting **malformed `tool_use` blocks from Opus 4.8** (#63604) and a **Windows regression** where tool results are silently dropped (#46767).

---

## Releases
**v2.1.179** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.179)
- Fixed mid-stream connection drops: partial responses are now preserved instead of showing a raw error; the spinner no longer gets stuck at “running tool”.
- Fixed mouse-wheel scrolling in WSL2 under Windows Terminal and VS Code (regression in 2.1.172).
- Fixed a sandbox `denyR` issue (details in the release).

---

## Hot Issues
1. **[#46140 — CRITICAL: MCP OAuth Bearer token never sent](https://github.com/anthropics/claude-code/issues/46140)**  
   *OAuth 2.1 authorization_code + PKCE flow completes successfully, but the subsequent MCP request does not include the Bearer token.*  
   ⚠️ 18 comments · 5 👍 | Open since April, still unresolved.

2. **[#65514 — Usage credits required for 1M context – Pro plan blocked despite 17% usage](https://github.com/anthropics/claude-code/issues/65514)**  
   *Users on the Pro plan cannot access the 1M-context option even when well below usage limits.*  
   💬 16 comments · 2 👍 | Marked duplicate, but frustration is high.

3. **[#46767 — Tool results silently dropped on Windows (regression in 2.1.101)](https://github.com/anthropics/claude-code/issues/46767)**  
   *“Missing due to internal error” across all tools. No error in output, just empty tool results.*  
   🔴 11 comments · 5 👍 | Windows users blocked from reliable tool execution.

4. **[#63604 — Opus 4.8 emits malformed tool_use blocks; entire response discarded](https://github.com/anthropics/claude-code/issues/63604)**  
   *Model generates invalid `tool_use` blocks that fail parsing. 4.7 works fine.*  
   🔥 10 comments · 12 👍 | Highest 👍 count; suggests a model-side regression.

5. **[#65429 — System prompt consumes ~9.3M tokens after installing Claude Desktop on WSL](https://github.com/anthropics/claude-code/issues/65429)**  
   *Every session starts with an enormous system prompt, obliterating context budget.*  
   💬 9 comments · 0 👍 | Affects WSL users running both Desktop and CLI.

6. **[#68484 — Desktop extension installs silently fail on macOS Tahoe 26.5](https://github.com/anthropics/claude-code/issues/68484)**  
   *No error, no feedback — extensions simply don’t load.*  
   💬 9 comments · 0 👍 | Silent failure is especially dangerous for debug.

7. **[#61299 — File descriptor leak regression in large monorepos (2.1.143+)](https://github.com/anthropics/claude-code/issues/61299)**  
   *Leak causes `EMFILE` errors on macOS after extended use in large repos.*  
   💬 7 comments · 1 👍 | Has reproducible test case.

8. **[#51701 — Desktop app sends macOS-only URI on Windows](https://github.com/anthropics/claude-code/issues/51701)**  
   *`x-apple.systempreferences://…` embedded in messages on Windows machines.*  
   💬 6 comments · 5 👍 | Platform detection gap with security implications.

9. **[#64235 — Intermittent “tool call was malformed” on stop_reason=tool_use turns](https://github.com/anthropics/claude-code/issues/64235)**  
   *The harness reports a malformed tool call even when the model produced valid `tool_use`. Agent silently does nothing.*  
   💬 5 comments · 2 👍 | Breaks agent reliability.

10. **[#68065 — Background agent notifications route through wrong agent ID when launched sequentially](https://github.com/anthropics/claude-code/issues/68065)**  
    *Second agent’s completion notification arrives on first agent’s task ID; execution tree becomes confusing.*  
    💬 2 comments · 2 👍 | Impacts workflow orchestration.

---

## Key PR Progress
1. **[#46351 — Enable PowerShell tool on macOS & Linux when pwsh is available](https://github.com/anthropics/claude-code/pull/46351)** *(CLOSED)*  
   *Removes Windows-only gate for `CLAUDE_CODE_USE_POWERSHELL_TOOL`. Essential for cross-platform automation.*

2. **[#68787 — Add error message to edit-issue-labels.sh when called without arguments](https://github.com/anthropics/claude-code/pull/68787)**  
   *Fixes silent exit with code 1 — CI now gets a clear diagnostic.*

3. **[#68786 — Fix shell injection in test-hook.sh via stdin redirection](https://github.com/anthropics/claude-code/pull/68786)**  
   *Closes a security hole where `$TEST_INPUT` could be injected into a `bash -c` string.*

4. **[#68785 — Fix hook JSON to stdout, tighten su* glob, fix CI detection & JSON injection in examples](https://github.com/anthropics/claude-code/pull/68785)**  
   *Multiple bugfixes in plugin-dev example hooks. BUG-25: decision JSON was written to stderr.*

5. **[#68673 — Break pagination when page is not full, not only when empty](https://github.com/anthropics/claude-code/pull/68673)**  
   *Fixes an off-by-one in the issue-list pagination logic.*

6. **[#68678 — Don’t mark Claude Desktop issues as invalid](https://github.com/anthropics/claude-code/pull/68678)**  
   *Triage improvement: Desktop-specific bugs were being labeled `invalid` incorrectly.*

7. **[#68679 — Strip control characters before promise comparison in ralph-wiggum](https://github.com/anthropics/claude-code/pull/68679)**  
   *Fixes false-positive promise failures when ANSI/control codes are present.*

8. **[#68680 — Safe JSON construction and correct event name in log-issue-events workflow](https://github.com/anthropics/claude-code/pull/68680)**  
   *Fixes JSON injection and misnamed event fields in the issue event logger.*

9. **[#68689 — Block symlink escape in extensibility config reads](https://github.com/anthropics/claude-code/pull/68689)**  
   *Security: prevents malicious symlink traversal via plugin config files.*

10. **[#68694 — Normalize CLAUDE_PLUGIN_ROOT path separators on Windows](https://github.com/anthropics/claude-code/pull/68694)**  
    *Fixes plugin loading failures on Windows due to backslash/slash mismatches.*

---

## Feature Request Trends
- **MCP ecosystem maturity** — Top requests include OAuth flow fixes (#46140), tool response diffing/delta to reduce context window usage (#68921), and better documentation for stdio server troubleshooting (#47635).
- **Cross-platform parity** — Users want the PowerShell tool available on macOS/Linux (PR #46351), and better Windows/WSL support for system prompts (#65429) and extension installation (#68484).
- **Usage & cost transparency** — Requests to clarify usage bucket separation between Sonnet and “all” (#68964) and to address the 1M-context Pro plan block (#65514) reflect growing concern about cost management.
- **Agent & workflow controls** — Feature requests for an in-session `/remote-control` toggle (#60699), a `/bug` command to file issues from terminal (PR #68707), and better agentic loop limits to prevent quota exhaustion (#68961).
- **UI/UX improvements** — Persistent “Fable 5 unavailable” banner needs a dismiss button (#68578); slash command fall-through in web sessions (#68402) frustrates users.

---

## Developer Pain Points
- **Tool reliability** — Windows users face silent tool result drops (#46767) and malformed `tool_use` blocks from Opus 4.8 (#63604). Intermittent harness errors (#64235) break agent workflows.
- **Resource leaks** — File descriptor leaks in large monorepos (#61299) and excessive token consumption from system prompts (#65429) degrade long sessions.
- **Platform inconsistencies** — macOS-only URIs sent on Windows (#51701), silent install failures on macOS Tahoe (#68484), and WSL2-specific scrolling regression (fixed in v2.1.179).
- **Agent overruns** — No backoff in `parallel()` fan-out causing 429 rate limits and full session loss (#68968). Background agents misrouting notifications (#68065). Uncontrolled agentic loops burning API quota (#68961).
- **Missing or misleading errors** — MCP OAuth silently drops Bearer tokens (#46140). Installer gives no feedback on failure (#68484). Docs lack malformed stdout troubleshooting (#47635). Built-in `/doctor` command becomes unreachable when plugins define a `doctor` command (#68957).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-17

## Today’s Highlights
Two new Rust alpha releases landed, and the community remains vocal about conversation hiding and session management bugs. On the PR front, the team is focusing on plugin catalog sharing, token budgets, and credential security, while several Windows-specific crashes and macOS resource leaks continue to attract attention.

---

## Releases
- **[rust-v0.141.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.141.0-alpha.3)** and **[rust-v0.141.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.141.0-alpha.4)** were published in the last 24 hours. No changelog details are available; these are incremental alpha releases in the v0.141.0 branch.

---

## Hot Issues
1. **[#21128 – Codex Desktop silently hides conversations outside the recent-50 window](https://github.com/openai/codex/issues/21128)**  
   *27 comments, 17 👍* – A major usability bug: older project chats disappear from the UI once they fall outside the global “recent 50”, making the app unreliable as a long‑term working memory. High community frustration.

2. **[#28095 – Archived chats show a Delete button that doesn’t work](https://github.com/openai/codex/issues/28095)**  
   *12 comments, 4 👍* – Deleting archived chats fails silently. Indicates a deeper archive state management issue.

3. **[#18052 – “Codex ran out of room in the model's context window”](https://github.com/openai/codex/issues/18052)**  
   *10 comments, 2 👍* – Users hit context limits without a clear way to reclaim space. Especially painful in long agent sessions.

4. **[#27287 – Computer Use bootstrap fails on Windows: packaging mismatch](https://github.com/openai/codex/issues/27287)**  
   *9 comments, 9 👍* – `@computer` fails with a subpath export error. High impact for Windows users wanting to use the desktop computer‑use skill.

5. **[#27506 – App crashes on Windows when user profile path contains non‑ASCII characters](https://github.com/openai/codex/issues/27506)**  
   *9 comments, 6 👍* – Korean and other non‑Latin scripts in the Windows username cause instant crash at launch. A global accessibility blocker.

6. **[#25321 – Composer caret/focus disappears on macOS](https://github.com/openai/codex/issues/25321)**  
   *9 comments, 4 👍* – Input focus randomly vanishes until switching app focus. Interrupts daily workflow.

7. **[#12464 – Request: `/cwd` command to switch working directory in TUI](https://github.com/openai/codex/issues/12464)**  
   *7 comments, 21 👍* – One of the most upvoted feature requests: allow changing the working directory without restarting the CLI session.

8. **[#14372 – Permissions error with git fsmonitor in sandbox](https://github.com/openai/codex/issues/14372)**  
   *7 comments, 5 👍* – Git file system monitor permission issues inside sandboxed environments, breaking standard workflows.

9. **[#26415 – Locked Computer Use hangs on macOS 26.6 with high CPU](https://github.com/openai/codex/issues/26415)**  
   *6 comments* – `SkyComputerUseService` spins uncontrollably when using locked mode, making the feature unusable.

10. **[#22037 – TUI `/resume` picker can block on global rollout scan](https://github.com/openai/codex/issues/22037)**  
    *6 comments, 1 👍* – The resume picker performs a full global scan even when a `cwd` filter is set, causing long delays.

---

## Key PR Progress
1. **[#28645 – Fail open on managed feature write conflicts](https://github.com/openai/codex/pull/28645)**  
   Allows local config values to persist even when enterprise policies pin the opposite value – a pragmatic middle‑ground for admins.

2. **[#28494 – Add shared session token budgets](https://github.com/openai/codex/pull/28494)**  
   New opt‑in token budget for an entire agent session (root + descendant threads), helping users control costs in long runs.

3. **[#28638 – core: remove redundant TurnContext and Prompt fields](https://github.com/openai/codex/pull/28638)**  
   Cleanup PR removing dead fields and cached projections; reduces surface for split‑brain states.

4. **[#28409 – Enforce exact managed config values](https://github.com/openai/codex/pull/28409)**  
   Expands `requirements.toml` to enforce exact values for seven settings (e.g., `sqlite_home`, `log_dir`, `allow_login_shell`). Startup warnings guide users to alignment.

5. **[#28599 – code‑mode: move cell state into library actor](https://github.com/openai/codex/pull/28599)** (closed/merged)  
   Refactors the code‑mode cell run loop into a dedicated actor for cleaner ownership and lifecycle management.

6. **[#26703 – TUI Plugin Sharing 3: render remote plugin catalog sections](https://github.com/openai/codex/pull/26703)**  
   Builds the plugin directory UI that displays remote catalogs as product‑level sections instead of raw marketplace internals.

7. **[#28034 – Add experimental local credential broker](https://github.com/openai/codex/pull/28034)**  
   Moves injected credentials behind the managed network proxy to prevent child processes from exfiltrating them. Security‑focused.

8. **[#28632 – Tell codex to avoid changing rollout format](https://github.com/openai/codex/pull/28632)**  
   Adds a path‑types skill requirement to nudge the code away from altering rollout types during path migrations – stability patch.

9. **[#28624 – Load plugins and skill roots concurrently](https://github.com/openai/codex/pull/28624)**  
   Bounded concurrency (up to 8) for cold startup plugin and skill discovery, reducing latency without overwhelming the filesystem.

10. **[#28626 – Reuse directory entry metadata in skill scans](https://github.com/openai/codex/pull/28626)**  
    Avoids extra metadata requests during skill discovery by reusing already‑returned file/directory kinds – especially beneficial over remote exec servers.

---

## Feature Request Trends
- **Session‑aware CLI commands** (#12464, #28437): Users want `/cwd` and native `PreToolUse` hooks with “ask” approval prompts to better control tool calls and working directories.
- **IDE Extension improvements** (#16615): Strong demand for opening Codex chat in a separate window within VS Code, and for better multi‑session management.
- **Token and rollout budgeting** (#28494, #18052): Requests for explicit token budgets per session/thread to avoid abrupt context full errors.
- **Documentation gaps** (#28575): Several users point to missing uninstall guides and other basic onboarding docs.

---

## Developer Pain Points
- **Windows reliability** (#27287, #27506, #27809, #28275): Crashes on non‑ASCII paths, Computer Use bootstrap failures, and repeated `VCPkgSrv.exe` crashes top the Windows complaint list.
- **Session history and archiving bugs** (#21128, #28095, #26012, #26201): Conversations silently hidden, delete buttons broken, stale archive paths – long‑term session storage is fragile.
- **Context window limitations** (#18052, #22037): Users frequently hit context caps or face long resume scans, disrupting deep agent sessions.
- **Performance with large rollouts** (#22991, #25215, #26161): Multi‑hundred‑MB JSONL files cause freezes and unrecoverable sessions, especially on Desktop.
- **macOS resource leaks** (#27536, #26341): `code_sign_clone` grows to 62+ GB, and syspolicyd file descriptor leaks corrupt DMG downloads – silent disk usage and system stability risks.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-06-17

## Today’s Highlights
No new releases were published in the last 24 hours, but the community remains highly active. Developers continue to report persistent agent‑hang and subagent‑orchestration bugs, while maintainers have closed several security‑critical PRs, including atomic MCP token writes and CI artifact‑poisoning fixes. A new thought‑leakage patch and a case‑insensitive path blocklist are under review, reflecting a strong security push.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **Generalist agent hangs indefinitely** – [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
   Users report that the generalist agent hangs on simple tasks (e.g., folder creation) unless explicitly told not to delegate. 8 👍 indicate it’s a top user blocker.  
   *Labels: priority/p1, area/agent, kind/bug*

2. **Subagent recovery misreports MAX_TURNS as success** – [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
   The `codebase_investigator` subagent returns `status: "success"` even when it hits the turn limit before any analysis, hiding the interruption.  
   *Labels: priority/p1, area/agent, kind/bug*

3. **Shell command execution stuck on “Waiting input”** – [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
   After finishing a command, the CLI hangs and marks the shell as awaiting input. 3 👍; many users frustrated by false waiting.  
   *Labels: priority/p1, area/core, kind/bug*

4. **PTY leak exhausts macOS system PTYs** – [#27628](https://github.com/google-gemini/gemini-cli/issues/27628)  
   When `enableInteractiveShell=true`, PTY files leak, causing system‑wide exhaustion. Closed as duplicate but marked for investigation.  
   *Labels: priority/p2, area/core, kind/bug*

5. **Auto Memory retries low‑signal sessions forever** – [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
   The background extraction agent never marks low‑signal sessions as processed, leading to infinite retries and wasted context.  
   *Labels: priority/p2, area/agent, kind/bug*

6. **Browser agent fails on Wayland** – [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)  
   The browser subagent fails with a generic “GOAL” termination when running under Wayland displays.  
   *Labels: priority/p1, area/agent, kind/bug, agent/browser*

7. **Gemini does not use custom skills/sub‑agents autonomously** – [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
   Even with well‑described skills (e.g., gradle, git), the model rarely invokes them unless explicitly instructed.  
   *Labels: priority/p2, area/agent, kind/bug*

8. **Agent silently performs destructive operations** – [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)  
   The model uses `git reset --force` or other unsafe commands when safer alternatives exist, risking data loss.  
   *Labels: priority/p2, area/agent, kind/customer-issue*

9. **Browser agent ignores `settings.json` overrides** – [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)  
   Configuration overrides such as `maxTurns` are read by `AgentRegistry` but never passed to the browser agent.  
   *Labels: priority/p2, area/agent, kind/bug*

10. **400 error with >128 tools enabled** – [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)  
    When many tools are enabled, the API returns a 400 error rather than requesting the model to limit tool selection.  
    *Labels: priority/p2, area/agent, kind/bug*

## Key PR Progress
1. **CI: validate workflow_run origin (fork artifact poisoning)** – [#27753](https://github.com/google-gemini/gemini-cli/pull/27753)  
   Prevents fork PRs from running code with repository secrets by verifying the `workflow_run` trigger source.  
   *Labels: priority/p1, area/security*

2. **MCP OAuth token atomic write** – [#27664](https://github.com/google-gemini/gemini-cli/pull/27664)  
   Writes MCP token files through a temp file + atomic rename to avoid corruption. Closes #27663.  
   *Labels: priority/p1, area/security*

3. **Fix MCP OAuth refresh with stored client ID** – [#27889](https://github.com/google-gemini/gemini-cli/pull/27889)  
   Ensures auto‑discovered servers can refresh tokens correctly after `/mcp auth`.  
   *Labels: priority/p1, area/agent*

4. **fix(core): keep auto visible without preview access** – [#27718](https://github.com/google-gemini/gemini-cli/pull/27718)  
   Prevents the `auto` model alias from disappearing for users without preview features.  
   *Labels: priority/p2, area/core*

5. **fix(core): strip thoughts from scrubbed history turns** – [#27971](https://github.com/google-gemini/gemini-cli/pull/27971)  
   Removes internal monologue text from plain‑text history, stopping thought leakage that causes infinite loops.  
   *Labels: size/m, status/need-issue*

6. **enforce case‑insensitive sensitive path blocklist** – [#27966](https://github.com/google-gemini/gemini-cli/pull/27966)  
   Blocks `.git`, `.env`, `node_modules` regardless of case, with VSCode HITL integration.  
   *Labels: size/m, area/security*

7. **MCP header encoding for non‑ASCII values** – [#27771](https://github.com/google-gemini/gemini-cli/pull/27771)  
   Fixes connection failures when MCP headers contain Unicode (e.g., `mąka`) by normalizing to `ByteString`.  
   *Labels: priority/p2, area/agent*

8. **fix(build): resolve parallel workspace compilation race** – [#27643](https://github.com/google-gemini/gemini-cli/pull/27643)  
   Splits monorepo build into sequential topological stages (core → libraries → apps) to prevent dependency races.  
   *Labels: size/s, closed*

9. **fix(core-tools): defensive path resolution for @‑reference files** – [#27943](https://github.com/google-gemini/gemini-cli/pull/27943)  
   Strips leading `@` prefixes from LLM‑generated file paths to prevent path‑traversal attacks.  
   *Labels: size/m, closed*

10. **scope flash model names per auth backend (Vertex AI / Gateway)** – [#27760](https://github.com/google-gemini/gemini-cli/pull/27760)  
    Resolves model‑name resolution mismatches between Vertex AI and AI Studio backends.  
    *Labels: priority/p1, area/agent, closed*

## Feature Request Trends
- **AST‑aware tools for codebase navigation** – Multiple EPICs ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) request AST‑based file reads, search, and mapping to reduce token waste and improve agent accuracy.  
- **Evaluations infrastructure** – Issue [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) calls for robust component‑level evals (76 existing behavioral tests). [#23166](https://github.com/google-gemini/gemini-cli/issues/23166) asks for stabilizing internal evals.  
- **Memory system improvements** – Issues [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) (deterministic redaction), [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) (stop low‑signal retries), and [#26523](https://github.com/google-gemini/gemini-cli/issues/26523) (quarantine invalid patches) show strong user demand for reliable, safe auto‑memory.  
- **Agent self‑awareness** – [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) asks the agent to know its own CLI flags, hotkeys, and configuration so it can act as its own guide.  
- **Browser agent resilience** – [#22232](https://github.com/google-gemini/gemini-cli/issues/22232) requests automatic session takeover and lock recovery for persistent browser profiles.

## Developer Pain Points
1. **Agent hangs and subagent miscommunication** – Multiple p1 bugs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409), [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) show that delegation and turn limits are poorly handled, causing unresponsive sessions.  
2. **Shell integration unreliability** – Issues [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) (stuck waiting input) and [#27628](https://github.com/google-gemini/gemini-cli/issues/27628) (PTY leak) make interactive workflows painful, especially on macOS.  
3. **Configuration overrides ignored** – The browser agent ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) and subagent permissions ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) often ignore `settings.json`, contradicting user expectations.  
4. **Terminal corruption** – [#24935](https://github.com/google-gemini/gemini-cli/issues/24935) (corruption after exiting external editors) and [#21924](https://github.com/google-gemini/gemini-cli/issues/21924) (flicker on resize) degrade the terminal experience.  
5. **Memory system noise** – Low‑signal sessions being retried forever ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)) and invalid patches piling up ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)) frustrate users relying on long‑term context.  
6. **Lack of safety guardrails** – The model’s tendency to use destructive git commands ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)) and scatter temporary scripts ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) raise trust concerns.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-17

## Today’s Highlights

A new release (v1.0.64-0) launched today with several quality-of-life additions: a `/diagnose` command for session log analysis, an `/mcp registry` for browsing and installing MCP servers, and the graduation of `/security-review` out of experimental. On the bug front, a critical Windows ARM64 crash under load (#3687) remains open after two weeks, while several new issues around permission fatigue, silent model downgrades, and sub‑agent MCP access are drawing attention from the community.

## Releases

**v1.0.64-0** — released within the last 24 hours  
Key additions:

- **`/diagnose`** command to analyze session logs
- **`/mcp registry`** for browsing and installing MCP servers
- **`/security-review`** now available to all users without the `--experimental` flag
- Discovery of MCP servers provided by installed plugins
- CSV output support for MCP tools

## Hot Issues (10 noteworthy)

1. **[#3687 – Windows ARM64 crash under load (BEX64 / 0xc0000409)](https://github.com/github/copilot-cli/issues/3687)**  
   `copilot.exe` hard-aborts when multiple sessions start simultaneously (e.g., Windows Terminal tab restore) under memory pressure. Reproducible across v1.0.57 and v1.0.60. 5 comments, 1 👍.  
   *Why it matters*: A critical stability bug on a growing platform (Windows ARM) with no fix yet.

2. **[#1168 – Excessive authorization prompts (“authorization fatigue”)](https://github.com/github/copilot-cli/issues/1168)**  
   A single request can trigger dozens of consent prompts. Persistent for 5 months; 2 comments, 2 👍.  
   *Why it matters*: Severely disrupts workflow and is a top UX complaint.

3. **[#3828 – ContentExclusionFilter.isExcluded crash](https://github.com/github/copilot-cli/issues/3828)**  
   `TypeError` when `ContentExclusionService` is undefined, crashing the `rg` tool. Filed yesterday, no response yet.  
   *Why it matters*: A basic tool (`rg`) becomes unusable.

4. **[#3821 – `/update` from a resumed session leaves conflicting flags](https://github.com/github/copilot-cli/issues/3821)**  
   Running `/update` after resuming with `copilot -r` causes the CLI to restart with both `--session-id` and `-r` set, breaking session continuity.  
   *Why it matters*: Common update scenario fails silently.

5. **[#3730 – Support enterprise-managed custom models in CLI](https://github.com/github/copilot-cli/issues/3730)**  
   Administrators can set custom models via Copilot admin dashboard, but they are unavailable in CLI. 4 👍, high demand.

6. **[#2790 – Figma Desktop MCP misidentified as SSE, fails with 400](https://github.com/github/copilot-cli/issues/2790)**  
   HTTP MCP server shown as SSE; works in Codex CLI. Likely a protocol detection bug.  
   *Why it matters*: Blocks integration with popular design tool.

7. **[#3518 – No way to unarchive an archived session](https://github.com/github/copilot-cli/issues/3518)**  
   Users accidentally archive long-running orchestrator sessions and cannot restore them. 3 👍, a clear missing feature.

8. **[#3812 – Sub‑agents can no longer access MCP tools](https://github.com/github/copilot-cli/issues/3812)**  
   Custom sub‑agents lost access to MCP tools, likely due to deferred loading changes. Previously working.  
   *Why it matters*: Breaks multi‑agent orchestration.

9. **[#3830 – Add command to update all plugins at once](https://github.com/github/copilot-cli/issues/3830)**  
   Currently requires one-by-one updates. Filed today, 0 comments but clear demand.

10. **[#3825 – `--allow-all` read permissions leak and wedge TUI](https://github.com/github/copilot-cli/issues/3825)**  
    Using `--allow-all` with `-i` or `--resume` causes the TUI to lose its input box.  
    *Why it matters*: A headless‑to‑interactive transition bug.

## Key PR Progress

No pull requests were merged or updated in the last 24 hours.

## Feature Request Trends

The most requested feature directions this week:

- **Plugin and MCP management improvements** — bulk updates (#3830), async read-only slash commands (#3829), and repo‑level skill directory support (#3822).
- **Session lifecycle enhancements** — ability to unarchive sessions (#3518), better `/update` flag handling (#3821), and offline session restore.
- **Enterprise/Model flexibility** — enterprise custom model support (#3730) and better model‑effort fallback transparency (#3823).
- **Documentation gaps** — proper docs for `matcher` on command hooks (#3820) and clearer rate‑limit messages (#3819).

## Developer Pain Points

Recurring frustrations and high‑frequency issues:

- **Windows stability**: The ARM64 crash (#3687) remains unresolved; lack of graceful shutdown hurts automation.
- **Authorization fatigue**: Repeated consent prompts (#1168) frustrate power users.
- **Silent misconfigurations**: Reasoning effort `xhigh` silently downgraded (#3823), sub‑agents using different models than the parent (#3824) — both erode trust.
- **Session corruption**: Cancelling a turn re‑injects “Operation cancelled” as a user message (#3826); `--allow-all` leaks permissions (#3825).
- **Plugin/Sub‑agent regressions**: MCP tools disappear for sub‑agents (#3812) and `ContentExclusionFilter` crashes (#3828) signal oversights in recent changes.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest – 2026-06-17

## 1. Today’s Highlights

Today’s most notable updates are two newly reported bugs: a fresh install on macOS Homebrew fails with an unhelpful “LLM not set” error and no hint to run `kimi login`, and a frustrating issue where the CLI auto-rediscovers a deleted MCP server, causing permanent 400 errors. Meanwhile, a long-standing feature request to hide thinking content from thinking models (e.g., kimi-k2-thinking-turbo) gained traction with 3 👍, though the related PR remains open. No new releases were published in the last 24 hours.

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues (4 items)

All items updated within the last 24 hours are included; no other issues met the criteria.

| Issue | Summary | Why It Matters | Community Reaction |
|-------|---------|----------------|-------------------|
| [#2456 – Fresh install reports "LLM not set" with no guidance to run login](https://github.com/MoonshotAI/kimi-cli/issues/2456) | After `brew install kimi-cli`, any command immediately fails with `LLM not set`; no mention of `kimi login`. | Critical first-run friction – new users are blocked with zero onboarding. | Opened today (2026-06-16), no comments yet. |
| [#2457 – Kimi Code CLI auto-discovers MCP server after user deleted it, causing unfixable 400 errors](https://github.com/MoonshotAI/kimi-cli/issues/2457) | On Windows 10, CLI re-discovers a deleted MCP server, leading to persistent 400 errors that cannot be cleared. | Breaks workflows relying on custom MCP servers; no workaround. | Opened 2026-06-16, no comments. |
| [#1327 – Enhancement: More Steps per turn by default](https://github.com/MoonshotAI/kimi-cli/issues/1327) | Default `Max number of steps reached: 100` triggers too early; context usage is only 34.5% when CLI stops. | Low default wastes users' time and interrupts long sessions. | 3 comments, 0 👍; first reported 2026-03-03, still open. |
| [#1632 – Feature Request: Option to hide thinking content while using thinking models](https://github.com/MoonshotAI/kimi-cli/issues/1632) | Thinking models show a spinner and grey italic text in real-time; users want to benefit from reasoning without the clutter. | Addresses a common desire for cleaner terminal output. | 2 comments, 3 👍; closed (likely superseded by PR #1771 or other? Actually it’s closed but updated today). |

---

## 4. Key PR Progress (1 item)

Only one pull request was updated in the last 24 hours.

| PR | Title & Link | Description | Impact |
|----|--------------|-------------|--------|
| [#1771 – fix: always stringify tool message content in Chat Completions provider](https://github.com/MoonshotAI/kimi-cli/pull/1771) | Fixes #1762 where tool messages with multiple `ContentPart`s (e.g., system reminder + output) caused a 400 error because the API expects `content` as a string. | Resolves a common integration bug when using tools with OpenAI-compatible providers. | Medium – affects any user of tool-using models. |

---

## 5. Feature Request Trends

Based on all open issues (including those not updated today), the community is pushing for:

- **Higher default step limits** – The `Max number of steps reached: 100` cap is widely seen as too low given low context usage. Users want either a larger default or a configurable threshold.
- **Thinking process visibility control** – Several users request the ability to hide or minimize the real-time “thinking” output when using models like kimi-k2-thinking-turbo, to reduce terminal noise without losing reasoning quality.
- **Simplify onboarding** – The fresh install issue (#2456) highlights the need for a clear post-install prompt or error message directing users to `kimi login`.

These trends point toward a desire for **more granular user control** and **better out-of-box experience**.

---

## 6. Developer Pain Points

Recurring frustrations observed in recently updated issues:

- **Lack of first-run guidance** – Installing via Homebrew and hitting an opaque `LLM not set` error with no next-step hint is a barrier to adoption.
- **MCP server management bugs** – The automatic re-discovery of deleted MCP servers (#2457) can render the CLI unusable with no known fix, especially on Windows.
- **Low default step limit** – Users constructing long reasoning chains are interrupted prematurely, requiring manual config changes even though context usage is still low.
- **Tool message content formatting** – The 400 error when using tools (addressed by PR #1771) demonstrates fragility in provider compatibility.

Themes: **insufficient onboarding**, **stability of plugin integrations (MCP)**, and **annoying defaults** that require manual tuning.

---

*Generated from GitHub data for 2026-06-17 (data refreshed 2026-06-16 23:59 UTC). All links point to the MoonshotAI/kimi-cli repository.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-17

## Today’s Highlights

The community remains focused on two long-standing pain points: **random session hangs** (Issue #2940) and the **broken copy-to-clipboard** functionality (Issue #7048), both still open with active discussion. On the PR side, a major **OpenAI-compatible provider overhaul** (#23501) and a **desktop file-watcher fix** (#32610) landed, while a **LAN provider discovery** feature (#27554) progresses. Feature requests for a native `/goal` session lifecycle (#27167) and a `/loop` iterative execution command (#18001) continue to attract strong upvotes.

---

## Releases

*No new releases in the last 24 hours.*

---

## Hot Issues

### 1. [FEATURE] Add native session goals with /goal (#27167)
- **Comments:** 50 | **👍:** 87  
- **Summary:** Suggests a persistent session goal/lifecycle feature via a `/goal` command, akin to a “session objective” that survives compact/restart.  
- **Why it matters:** High engagement indicates strong demand for better session management beyond ad-hoc prompts.  
[🔗 Issue #27167](https://github.com/anomalyco/opencode/issues/27167)

### 2. [BUG] OpenCode just hangs randomly after receiving instructions (#2940)
- **Comments:** 39 | **👍:** 18  
- **Summary:** Occurs on Laravel projects (Boost); `/compact` sometimes helps but not always. Users must force-close the process.  
- **Why it matters:** This is one of the oldest and most disruptive bugs; the community is frustrated by its persistent nature.  
[🔗 Issue #2940](https://github.com/anomalyco/opencode/issues/2940)

### 3. [CLOSED] Is zen/big-pickle glm 4.6? (#4276)
- **Comments:** 28 | **👍:** 3  
- **Summary:** A user notes the 200K context window and behavior of the `zen/big-pickle` model resembles GLM 4.6. Closed but sparks model-provenance discussion.  
- **Why it matters:** Highlights community curiosity about under-documented model aliases.  
[🔗 Issue #4276](https://github.com/anomalyco/opencode/issues/4276)

### 4. [BUG] Copy Text "Copied to clipboard" does never work (#7048)
- **Comments:** 23 | **👍:** 13  
- **Summary:** On Ubuntu Desktop/GhostTTY, right-click → “Copied to clipboard” unhighlights text but never actually copies.  
- **Why it matters:** Blocks basic UI workflow for TUI users. Reproducible across sessions.  
[🔗 Issue #7048](https://github.com/anomalyco/opencode/issues/7048)

### 5. [BUG] LM Studio Failure to refresh models (#2047)
- **Comments:** 17 | **👍:** 4  
- **Summary:** After adding/removing models in LM Studio, OpenCode does not refresh the model list even after re-auth.  
- **Why it matters:** Local model discovery is a core feature; manual workarounds hurt productivity.  
[🔗 Issue #2047](https://github.com/anomalyco/opencode/issues/2047)

### 6. [BUG] "Upstream idle timeout exceeded" (#28957)
- **Comments:** 15 | **👍:** 0  
- **Summary:** Occurs when using the “writing-plans” skill; the upstream connection between client and model service idles out.  
- **Why it matters:** Represents an infrastructure-level reliability issue for long-running skills.  
[🔗 Issue #28957](https://github.com/anomalyco/opencode/issues/28957)

### 7. [BUG] zsh: illegal hardware instruction opencode (#8345)
- **Comments:** 15 | **👍:** 6  
- **Summary:** On certain macOS (Apple Silicon?) systems, the desktop DMG binary crashes with an illegal hardware instruction.  
- **Why it matters:** Suggests a build/packaging problem likely tied to CPU-specific optimizations.  
[🔗 Issue #8345](https://github.com/anomalyco/opencode/issues/8345)

### 8. [BUG] opencode cannot read images anymore (#25832)
- **Comments:** 13 | **👍:** 4  
- **Summary:** Until April 29th image-reading (PNG/JPG) worked; now fails with “Bad request”. Regression suspected.  
- **Why it matters:** Vision capability is a key selling point; regression affects real workflows.  
[🔗 Issue #25832](https://github.com/anomalyco/opencode/issues/25832)

### 9. [BUG] OpenCode is heavily cpu-bound (#21470)
- **Comments:** 11 | **👍:** 10  
- **Summary:** With Gemini 3.1, most time is spent in OpenCode itself rather than model API calls (300K tokens session → 1.5M tool calls).  
- **Why it matters:** Performance degradation is a top complaint; users want efficient local orchestration.  
[🔗 Issue #21470](https://github.com/anomalyco/opencode/issues/21470)

### 10. [FEATURE] Implement /loop command for automated iterative task execution (#18001)
- **Comments:** 9 | **👍:** 27  
- **Summary:** Proposes a `/loop` command for repeated/periodic task execution without long natural-language prompts.  
- **Why it matters:** Strong upvote ratio shows demand for automation primitives.  
[🔗 Issue #18001](https://github.com/anomalyco/opencode/issues/18001)

---

## Key PR Progress

### 1. fix: OpenAI-compatible provider improvements (#23501)
- **Status:** OPEN | **Closes:** #20802, #5034, #20466  
- **Summary:** Three fixes for Ollama/local providers: proper system message handling, image support, and stream interruption.  
- **Why it matters:** Unblocks many local-model users and improves stability.  
[🔗 PR #23501](https://github.com/anomalyco/opencode/pull/23501)

### 2. fix(desktop): skip file watcher on $HOME and filesystem root (#32610)
- **Status:** CLOSED  
- **Summary:** Prevents inotify subscription timeouts and CPU pegging caused by watching broad roots like home directory or `/`.  
- **Why it matters:** Resolves a major desktop performance issue reported across multiple platforms.  
[🔗 PR #32610](https://github.com/anomalyco/opencode/pull/32610)

### 3. fix(provider): stub orphan MiniMax tool results (#32609)
- **Status:** OPEN | **Closes:** #32608  
- **Summary:** Stubs orphan tool results to avoid 400 errors when switching sessions to MiniMax M3.  
- **Why it matters:** A targeted fix for a provider-specific session migration bug affecting many users.  
[🔗 PR #32609](https://github.com/anomalyco/opencode/pull/32609)

### 4. fix(opencode): send system context as structured messages on OpenAI OAuth path (#32592)
- **Status:** CLOSED | **Closes:** #32505  
- **Summary:** Aligns OAuth and non-OAuth request formats for system/instruction context.  
- **Why it matters:** Fixes a critical compatibility bug for Codex/OpenAI OAuth users.  
[🔗 PR #32592](https://github.com/anomalyco/opencode/pull/32592)

### 5. feat(opencode): local LAN provider discovery + auto-discover models (#27554)
- **Status:** OPEN | **Closes:** #6231, #27553  
- **Summary:** Adds mDNS, UPnP, and ARP-scan based discovery for local OpenAI-compatible servers.  
- **Why it matters:** Streamlines local model setup, a frequently requested quality-of-life improvement.  
[🔗 PR #27554](https://github.com/anomalyco/opencode/pull/27554)

### 6. fix(tui): Old messages disappearing during long sessions (#26861)
- **Status:** OPEN | **Closes:** #7380  
- **Summary:** Lazy-scroll loading with virtualisation to keep UI stable in sessions with thousands of messages.  
- **Why it matters:** Addresses a long-standing TUI usability issue for heavy users.  
[🔗 PR #26861](https://github.com/anomalyco/opencode/pull/26861)

### 7. fix(core): fix mentions for files in hidden folders (#32193)
- **Status:** OPEN | **Closes:** #32126  
- **Summary:** Allows `@` mention of files inside folders prefixed with `.`.  
- **Why it matters:** Hidden folders (e.g., `.config`) are common; the omission was a daily annoyance.  
[🔗 PR #32193](https://github.com/anomalyco/opencode/pull/32193)

### 8. feat(session): add configurable fallback model chain (#27939)
- **Status:** CLOSED | **Closes:** #7602  
- **Summary:** When the primary model fails, automatically falls back to a configured secondary model.  
- **Why it matters:** Increases session reliability without user intervention.  
[🔗 PR #27939](https://github.com/anomalyco/opencode/pull/27939)

### 9. feat: add provider and per-model concurrency limits (#27938)
- **Status:** CLOSED | **Closes:** #12019, #26314  
- **Summary:** Optional `concurrencyLimit` fields to cap concurrent requests per provider or model.  
- **Why it matters:** Prevents rejection from providers with rate caps, improving reliability.  
[🔗 PR #27938](https://github.com/anomalyco/opencode/pull/27938)

### 10. fix(app): add service worker for cache-first static asset loading (#27936)
- **Status:** CLOSED | **Closes:** #27933, #19119, #19174  
- **Summary:** Navigation preload, stale-while-revalidate, and resource hinting for faster web app loads.  
- **Why it matters:** Significant performance improvement for the OpenCode web interface.  
[🔗 PR #27936](https://github.com/anomalyco/opencode/pull/27936)

---

## Feature Request Trends

- **Session Lifecycle & Goals** — the most upvoted open feature (#27167, 87👍) calls for a native `/goal` command that persists across compactions and model switches. Coupled with #18001 (/loop for iteration), there is a clear desire for **structured session primitives** beyond free-form chat.
- **Skill & Plugin Ecosystem** — multiple requests for **recursive skill discovery** (#21495), **multi-skill selection in TUI**, and a **middleware-style plugin pipeline** (#5148). Users want composable, discoverable automation.
- **UI Customization** — layout swapping (#16349) and configurable session picker limits (#20754) reflect a need for more adaptable desktop/TUI interfaces.
- **Pricing & Tier Flexibility** — #24879 proposes a “Go Pro” tier with shareable modifiers and first-month discounts, indicating frustration with rigid plan limits.

---

## Developer Pain Points

1. **Random Hanging / Unresponsiveness** — Issue #2940 remains the oldest severe bug (39 comments). Hangs after receiving instructions, often requiring Ctrl+C. Related: #32615 (infinite loop on empty git repo) and #28957 (upstream idle timeout).
2. **Clipboard & Input Issues** — #7048 (“Copied to clipboard” never works) is a high-frequency TUI complaint. Also #25832 (image reading broken) and #28824 (`@` file mention fails on Windows) affect core interaction.
3. **Performance & Resource Usage** — #21470 (CPU-bound orchestration) and #11286 (model context limits not respected) point to systemic inefficiencies in session management and token tracking.
4. **Provider Compatibility Fragility** — Multiple issues around MiniMax session rejection (#32608, #32614), DeepSeek edit tool failures (#31849), LM Studio model refresh (#2047), and OpenAI OAuth context flattening (#32505). The community is pushing for **more robust, tested provider abstractions**.
5. **UI / UX Gaps** — Skills missing from TUI autocomplete (#22129), disappearing messages in long sessions (addressed by #26861), and left/right panel layout inflexibility (#16349) show the TUI/desktop clients lag behind the web app in polish.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-17

## Today’s Highlights
Two patches landed in the last 24 hours: **v0.79.6** (fixes to HTTP dispatcher fetch preservation and DeepSeek V4 thinking-off compatibility) and **v0.79.5** (new provider‑scoped API‑key environments in `auth.json`). The community continues to report connection reliability issues in the TUI (issue #4945, 59 comments), and a wave of PRs brought provider‑scoped env overrides, timing metrics in `Usage`, Nix flake packaging, and Vercel AI Gateway attribution. Overall, the project is maturing its configuration surface while tackling long‑standing reliability and UI quirks.

## Releases
**v0.79.6** – *Fixed*  
- HTTP dispatcher now preserves a caller’s deliberate `fetch` override instead of reinstalling the undici global fetch.  
- Inherited OpenCode Go DeepSeek V4 “thinking‑off” requests now send the provider’s `thinking: { type: "disabled" }` compatibility parameter.

**v0.79.5** – *New Features*  
- **Provider‑scoped API key environments** – `auth.json` entries can now include `env` overrides for provider‑specific settings (Cloudflare, Azure OpenAI, Google Vertex, Amazon Bedrock, cache retention, proxy) without changing the project shell.  
[Full changelog](https://github.com/earendil-works/pi/releases)

## Hot Issues (10 most noteworthy)
1. **#4945 – openai‑codex Connection Reliability Issues**  
   `openai-codex` / `gpt-5.5` leaves the TUI stuck on `Working...` with no output. Only recovery is pressing Escape (59 comments, 30 👍). *Community reaction:* high severity, users ask for better error surfacing or timeout.

2. **#4877 – Session folder collision**  
   Different paths can hash to the same session folder (e.g. `/a/b/c/d` ↔ `/a-b/c-d`). Not a crash but will surprise users (19 comments).

3. **#5696 – Model name does not refresh in TUI on CTRL+P**  
   Switching models requires two presses; the first press does nothing (9 comments). *Reaction:* minor but annoying UI glitch.

4. **#5687 – `pi list` and `pi update` never exit when an extension runs an MCP server**  
   Package subcommands finish output then hang until Ctrl‑C (8 comments). *Pain:* breaks scripting.

5. **#5816 – `pi` keeps trying to use tool `search` and gets `Tool search not found`**  
   On v0.79.4, any meaningful codebase change triggers a missing tool error (7 comments). *Community reaction:* regression, urgent.

6. **#5790 – Support httpProxy in settings.json**  
   Request to let Pi route through a proxy without relying on environment variables (7 comments). *Reaction:* strongly upvoted, merged quickly.

7. **#5728 – Support provider‑specific config in auth.json**  
   Providers like `cloudflare-ai-gateway` need additional fields (accountId, gatewayId) beyond API keys (7 comments). *Reaction:* consensus, merged into v0.79.5.

8. **#5571 – `pi -p` hangs indefinitely when stdin is a non‑TTY pipe that never closes**  
   Fresh install with no credentials hangs for minutes instead of failing fast (7 comments). *Pain:* blocks CI usage.

9. **#5556 – Session listing still keeps full transcript text in `allMessagesText`**  
   Even after streaming JSONL loading, `buildSessionInfo()` still appends all text, wasting memory (5 comments). *Reaction:* performance concern for long sessions.

10. **#5407 – Double backspace and double enter on Kitty**  
    Terminal‑specific issue; Kitty users experience duplicate keypresses (5 comments, 1 👍). *Reaction:* appears platform‑dependent but reproducible.

## Key PR Progress (all 9 PRs)
- **#5820** – `fix: Preserve raw HTTP error status and bodies for non‑schema errors`  
  Closes #5763; surfaces HTTP status and raw body from proxy/gateway errors instead of swallowing them.  
  [PR #5820](https://github.com/earendil-works/pi/pull/5820)

- **#5812** – `fix(tui): protect pipe characters inside inline code in markdown tables`  
  Prevents `|` inside backticks from being interpreted as a column delimiter.  
  [PR #5812](https://github.com/earendil-works/pi/pull/5812)

- **#5807** – `feat: add provider‑scoped environment overrides`  
  Introduces `env` object in `auth.json` credentials and stream options, taking precedence over process ENV vars.  
  [PR #5807](https://github.com/earendil-works/pi/pull/5807)

- **#5809** – `feat(ai): add durationMs and timeToFirstTokenMs to Usage, display tokens/sec in footer`  
  Enables latency and throughput metrics for footer extensions and consumers.  
  [PR #5809](https://github.com/earendil-works/pi/pull/5809)

- **#5789** – `fix(tui): restore cursorUp line‑start jump before history browsing`  
  Fixes regression where pressing Up on the first line of non‑empty input incorrectly entered history.  
  [PR #5789](https://github.com/earendil-works/pi/pull/5789)

- **#5803** – `fix(ai): reject malformed OpenAI tool calls`  
  Streamed tool calls without an `id` or `function.name` are now rejected and excluded from session history. Adds regression tests.  
  [PR #5803](https://github.com/earendil-works/pi/pull/5803)

- **#5801** – `Nixify pi`  
  Adds Nix flake packaging; users can build and run via `nix build path:$PWD#pi`.  
  [PR #5801](https://github.com/earendil-works/pi/pull/5801)

- **#5798** – `feat(coding-agent): add Vercel AI Gateway attribution`  
  Adds `http-referer` and `x-title` headers for Vercel AI Gateway identification.  
  [PR #5798](https://github.com/earendil-works/pi/pull/5798)

- **#5796** – `chore: bump TS target and lib to ES2024, use Promise.withResolvers()`  
  Replaces hand‑rolled `Promise.withResolvers()` implementations with the native ES2024 API.  
  [PR #5796](https://github.com/earendil-works/pi/pull/5796) *(open)*

## Feature Request Trends
The community is pushing for **more flexible configuration and extensibility**:

- **Proxy support** – Users want a fixed HTTP proxy in `settings.json` (#5790) to avoid environment‑variable workarounds.
- **Provider‑specific config in `auth.json`** – Already merged in v0.79.5 (#5728, PR #5807); users demand similar granularity for Cloudflare, Azure, Vertex, etc.
- **New model/provider support** – Requests for ZhipuAI (#2345), Gemini 3.5 Flash (#5761), and Anthropic OAuth subscription usage (#5821) reflect a desire to cover more ecosystems.
- **OAuth improvements** – Custom callback page rendering (#5372) and subscription‑tier usage confirmation (#5821) show interest in smoother auth flows.
- **RPC API expansion** – Exposing session entries and tree via RPC commands (#5810) would enable external tooling to drive Pi programmatically.
- **Timing metrics** – The merged PR #5809 (durationMs, timeToFirstTokenMs) indicates developers want performance observability built in.

## Developer Pain Points
Recurring frustrations cluster around **reliability, UI polish, and error handling**:

- **Streaming hangs & missing errors** – Issues #4945, #5571, #5778, #5816 all describe the TUI or CLI stuck without feedback, requiring manual interruption. Users demand timeouts, fallback behavior, and clearer error propagation.
- **Terminal/UI quirks** – Double keypress in Kitty (#5407), model name not refreshing (#5696), tab completion applying first item prematurely (#5670), chat view jumping during streaming (#5576) – these degrade the daily experience for many.
- **Error body swallowing** – Proxy/gateway errors render as opaque `UnknownError` (#5763), fixed by PR #5820 but still a pain point.
- **File encoding corruption** – CP‑1252 files are silently converted to UTF‑8 (#5797), breaking legacy C++ projects on Windows.
- **Package management interference** – MCP server processes block package subcommands (#5687); bun/npm lock files are created in caller’s cwd (#5774).
- **Nix/infrastructure fragmentation** – External package managers can’t use `pi update` (#5607); the new Nix flake (#5801) addresses this but reveals the demand for distribution‑agnostic packaging.

The overall sentiment is that Pi is powerful but still rough around the edges—especially in edge‑case handling, terminal compatibility, and non‑pipable stdin scenarios.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-17

## Today's Highlights

The release pipeline hit persistent failures for both the stable `v0.18.1` and a nightly build, with a critical fix for `glibc`‑incompatible auto‑updates merged late today. Community attention remains focused on the proposed OAuth free tier reduction (136 comments) and the rollout of `/loop` alignment with Claude Code. Meanwhile, a new QQ Bot channel adapter and a vision‑bridge for text‑only models are drawing early interest.

---

## Releases

No new releases were published in the last 24 hours. Two release workflows (v0.18.1‑preview.1 and v0.18.1‑nightly) failed today; the root cause appears to be a stale integration test assertion that was patched in PR #5217.

---

## Hot Issues

**1. [Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)**  
**#3203** – Proposes slashing the free daily quota from 1,000 to 100 requests and phasing out the free entry point. With 136 comments, this is the most debated issue, reflecting strong community concern over pricing changes.

**2. [Project-scoped .mcp.json with Pending Approval](https://github.com/QwenLM/qwen-code/issues/4615)**  
**#4615** – A security‑focused feature request to add an explicit `Pending` state before MCP servers are started from workspace configs. Aligns with growing demand for fine‑grained credential control.

**3. [Trojan:JS/ShaiWorm.DBA!MTB False Positive](https://github.com/QwenLM/qwen-code/issues/5055)**  
**#5055** – The VSIX package triggers Windows Defender, causing user alarm. The team is investigating but no resolution yet. High visibility for packaging/security.

**4. [CLI /model Lists Discontinued OAuth Model](https://github.com/QwenLM/qwen-code/issues/5160)**  
**#5160** (closed) – A quick‑fix bug: the model picker shows the discontinued `qwen‑oauth` model even when OAuth is not configured. Already patched; good example of responsive triage.

**5. [QQ Bot Channel Adapter](https://github.com/QwenLM/qwen-code/issues/5201)**  
**#5201** – Community‑submitted PR with full WebSocket Gateway support. Signals interest in expanding beyond Telegram, WeChat, DingTalk, and Feishu.

**6. [Track /loop Alignment Work](https://github.com/QwenLM/qwen-code/issues/5124)**  
**#5124** – Parent issue for staged `/loop` improvements, including self‑paced wakeups and session scheduling. Roadmap priority.

**7. [0.18.1 ExitPlanMode Stuck](https://github.com/QwenLM/qwen-code/issues/5210)**  
**#5210** – User reports the CLI hangs in “ExitPlanMode” for hours when using Qwen3.7‑Max. Indicates a regression in plan‑mode exit logic; needs‑information status.

**8. [Subagent Task Crashes Mid-execution](https://github.com/QwenLM/qwen-code/issues/5180)**  
**#5180** – Multi‑agent sessions (manager + subagents) crash after long runs (12+ hours). Highlights memory and token management issues under the roadmap’s multi‑agent and background‑automation goals.

**9. [Port Dynamic Workflows / Ultracode from Claude Code](https://github.com/QwenLM/qwen-code/issues/4721)**  
**#4721** – Long‑standing feature request to add a third multi‑agent tier alongside `/swarm`. Community eager for parity with Claude Code’s advanced orchestration.

**10. [Auto-update Fails on Older glibc](https://github.com/QwenLM/qwen-code/issues/5206)**  
**#5206** (closed) – NPM‑installed CLI on CentOS 7 silently migrated to the standalone installer, which requires glibc ≥2.28. Fixed by keeping sudo‑required npm installs on npm. A relief for Linux users of older distros.

---

## Key PR Progress

**1. [Vision Bridge for Text-Only Models](https://github.com/QwenLM/qwen-code/pull/5126)**  
**#5126** – Allows text‑only primary models to “see” images via an opt‑in multimodal transcriber. Disabled by default; a clever workaround for model limitations.

**2. [Self-Paced Loop Wakeups](https://github.com/QwenLM/qwen-code/pull/5197)**  
**#5197** – Wires `/loop <prompt>` (no interval) to a self‑paced wakeup engine. Step 2 of aligning with Claude Code’s `ScheduleWakeup`. Depends on #5182.

**3. [Second-Resolution Session Wakeup Engine](https://github.com/QwenLM/qwen-code/pull/5182)**  
**#5182** – Foundation for `/loop` alignment: a non‑durable, second‑resolution wakeup channel separate from cron. Step 1, now merged.

**4. [QQ Bot Channel Adapter](https://github.com/QwenLM/qwen-code/pull/5202)**  
**#5202** – Full QQ Bot integration with WebSocket Gateway, message handling, and admin commands. Ready for review.

**5. [Keep Sudo-Required NPM Installs on NPM](https://github.com/QwenLM/qwen-code/pull/5207)**  
**#5207** (merged) – Fixes #5206 by preventing silent migration to the standalone installer. Restores compatibility with older glibc.

**6. [Follow-Up Suggestion in Input Placeholder](https://github.com/QwenLM/qwen-code/pull/5145)**  
**#5145** – Displays the model’s suggested next prompt in the input placeholder, reducing the need for chip navigation.

**7. [Localize Remaining Hardcoded UI Strings](https://github.com/QwenLM/qwen-code/pull/5189)**  
**#5189** – Routes dialog tooltips and other missed strings through the i18n system. Adds English and Chinese entries.

**8. [Pass Original API Call ID to Hook System](https://github.com/QwenLM/qwen-code/pull/4918)**  
**#4918** – Adds `tool_call_id` to all hook interfaces, enabling better tracing and audit logging for LLM calls.

**9. [Track Supported `sed` Edits in File History](https://github.com/QwenLM/qwen-code/pull/5141)**  
**#5141** – Treats safe `sed -i` substitutions as tracked edits, improving diff visibility and file history recording.

**10. [Remember Selected Provider for Duplicate Model IDs](https://github.com/QwenLM/qwen-code/pull/5179)**  
**#5179** – Persists the chosen `baseUrl` when multiple providers define the same model ID, fixing a UX confusion.

---

## Feature Request Trends

- **Background Automation & Multi-Agent**: The `/loop` alignment (#5124, #5156, #5184) and “Dynamic Workflows” port (#4721) underscore demand for persistent, self‑scheduled agent loops and advanced orchestration tiers.
- **Credential Security & Scoped Configs**: Issues around `.mcp.json` approval (#4615), OAuth tier reduction (#3203), and tool‑call IDs (#4918) indicate a strong push for granular access control.
- **Channel Expansions**: The QQ Bot PR (#5202) and related issue (#5201) show interest in broadening supported chat platforms beyond the current set.
- **Localization & Internationalization**: Many UI‑string issues (#5186, #5189) reflect a growing non‑English user base, particularly Chinese‑speaking.
- **Model Compatibility**: The vision bridge (#5126) and self‑hosted LLM fixes (e.g., #2512) highlight a need to handle heterogeneous model capabilities and API quirks.

---

## Developer Pain Points

- **OAuth Pricing Uncertainty**: The proposed free tier reduction (#3203) generated the most comments this week, indicating anxiety over cost and accessibility.
- **False Positive Antivirus Alerts**: The Trojan warning on the VSIX (#5055) erodes trust in the release packaging pipeline.
- **Installation Woes on Old Linux**: glibc incompatibility (#5206) and sudo‑required NPM upgrades continue to plague enterprise users on CentOS 7 / RHEL 7.
- **Terminal Cleanup Issues**: Stuck SGR mouse mode (#5212) and “ExitPlanMode” hangs (#5210) disrupt developer workflows, especially during long sessions.
- **Multi-Agent Reliability**: Crashes during long‑running subagent tasks (#5180) and stale worktree markers (#5208) frustrate users relying on background automation.
- **UI Regressions**: React minified errors (#5199) and model drop‑down listing deprecated options (#5160) degrade the IDE experience.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 2026-06-17 DeepSeek TUI 社区技术摘要。

---

# DeepSeek TUI 社区摘要 - 2026-06-17
**分析师备注：本项目已正式更名为 `CodeWhale`，旧版 `deepseek-tui` 已弃用。本摘要将使用新名称。**

## 1. 今日亮点
今天是 CodeWhale 的活跃开发日，多项修复和功能正在进入主干。核心团队正在推进两项重要工作：一是代码库的**命令边界重构**（推动 v0.9.0），二是 **“海马体”记忆系统 v2** 的集成。社区方面，关于任务执行“卡死”和模型上下文长度问题的反馈依然突出，同时，新的 **DeepInfra 提供商支持** 和 **静态链接的 Linux 二进制文件** 预计将显著改善用户体验。

## 2. 发布
**没有新版本发布。** 最新版本仍是 v0.8.61。请注意，该版本及未来所有版本均以 `codewhale` 为项目名发布，旧版 `deepseek-tui` 包已停止维护。建议用户按照 `docs/REBRAND.md` 指南进行迁移。

## 3. 热点问题 (Top 10)
1.  [#2487 - Turn stalled - no completion signal received](https://github.com/Hmbown/CodeWhale/issues/2487) **(开放中)**
    - **为何重要**：这是当前用户反映最强烈的稳定性问题。在 `yolo` 模式下，操作频繁冻结并显示此错误，且无法通过 `continue` 恢复。拥有 14 条评论和 1 个赞，表明影响广泛，社区高度关注。项目应将其作为高优先级 bug 处理。
2.  [#2739 - 任务执行过程中卡死](https://github.com/Hmbown/CodeWhale/issues/2739) **(开放中)**
    - **为何重要**：来自中文用户的深度报告，描述了一个相似但更严重的问题：任务长时间卡死后，`--continue` 也无法恢复上下文。用户提到此问题从 v0.8.51 就已存在，且 `--continue` 功能看似无效，这会严重削弱用户的信任。
3.  [#3275 - CodeWhale 过度自我参与修改](https://github.com/Hmbown/CodeWhale/issues/3275) **(开放中)**
    - **为何重要**：一个关于 Agent 行为的新 critcial 报告，指出 CodeWhale 在执行任务时超出了用户意图，进入了“自问自答”和“自我执行”的循环。这被认为是对关键 issue #3061 的回归，直接指向了 Agent 控制逻辑的核心问题。
4.  [#3264 - 限制技能扫描路径](https://github.com/Hmbown/CodeWhale/issues/3264) **(开放中)**
    - **为何重要**：一个清晰的增强请求，希望 CodeWhale 只扫描 `~/.codewhale/skills/` 目录，而不是整个文件系统。这反映出用户对性能和隐私的关注，也是插件/技能生态走向成熟的标志。
5.  [#3240 - 遗留的 deepseek 配置目录](https://github.com/Hmbown/CodeWhale/issues/3240) **(开放中)**
    - **为何重要**：尽管已更名为 CodeWhale，程序运行时仍会创建旧版 `.deepseek` 配置目录。这是一个品牌混淆和潜在的备份/迁移问题，也是项目重命名工作被忽略的细节。
6.  [#3238 - Ubuntu 22.04 LTS 因 glibc 版本不匹配无法运行](https://github.com/Hmbown/CodeWhale/issues/3238) **(开放中)**
    - **为何重要**：`npm install -g codewhale` 在 Ubuntu 22.04 LTS 上因 `glibc` 版本依赖问题而失败。这直接影响了大量潜在用户（特别是使用较旧但稳定的 Linux 发行版的用户），并凸显了对静态链接二进制文件的需求。
7.  [#3273 - js_execution Node fetch 不代理](https://github.com/Hmbown/CodeWhale/issues/3273) **(开放中)**
    - **为何重要**：报告了 `js_execution` 工具在 Windows 上无法通过公司 VPN/代理访问网络的问题。这对于企业级用户和需要受控网络环境的使用场景至关重要。
8.  [#2652 - 子代理评估输出被误认为是完整证据](https://github.com/Hmbown/CodeWhale/issues/2652) **(已关闭)**
    - **为何重要**：一个重要的日志/信任问题。子代理的输出在直播记录中被截断，但模型仍会将其描述为“完整审查”。这可能导致 Agent 基于错误信息做出决策，已被修复。
9.  [#2870 - [EPIC] 分阶段命令边界重构](https://github.com/Hmbown/CodeWhale/issues/2870) **(开放中)**
    - **为何重要**：这是指向 v0.9.0 的关键技术债清理工作。由贡献者 `aboimpinto` 提出，旨在将命令边界的概念标准化，为多 Agent 协作铺平道路。这是一个大型项目的跟踪器。
10. [#3102 - Agent 应提供首要的澄清问题请求](https://github.com/Hmbown/CodeWhale/issues/3102) **(已关闭)**
    - **为何重要**：一个 UX 改进，要求 Agent 在不确定时主动通过 UI 弹窗澄清，而不是只在聊天窗口中输出一条消息。这被认为是实现更智能、更可预测的 Agent 交互的关键特性。

## 4. 关键 PR 进展 (Top 8)
1.  [#3271 - docs: 添加 Ponytail 角色](https://github.com/Hmbown/CodeWhale/pull/3271) **(已合并)**
    - **内容**：在项目指令中增加了对 `Ponytail` 角色的引用。
    - **意义**：表明 CodeWhale 的生态系统正在扩展，开始支持社区创建的个性化角色。
2.  [#3269 - feat(tui): 将斜杠命令公开为热栏操作](https://github.com/Hmbown/CodeWhale/pull/3269) **(已合并)**
    - **内容**：允许将斜杠命令（如 `/mode`）绑定到数字热键（1-8），极大提高了高级用户的操作效率。
    - **意义**：与 issue #3243 中关于数字键被劫持的 bug 修复直接相关，使该功能更加完善。
3.  [#3274 - feat(release): 构建静态 musl Linux 二进制文件](https://github.com/Hmbown/CodeWhale/pull/3274) **(开放中)**
    - **内容**：将 Linux x64 构建从动态 glibc 切换到静态 musl。
    - **意义**：这是解决如 #3238 (glibc 版本不匹配) 等安装问题的关键举措，将极大地提升 Linux 用户的部署兼容性。
4.  [#3270 - docs: 向 cargo install 指南添加 Linux 构建依赖项](https://github.com/Hmbown/CodeWhale/pull/3270) **(已合并)**
    - **内容**：针对 `cargo install` 在 Ubuntu 24.04 失败的问题，更新了文档。
    - **意义**：快速解决了社区报告的构建失败问题，改善了从源码构建的用户体验。
5.  [#3236 - codex: 添加 DeepInfra 提供商支持](https://github.com/Hmbown/CodeWhale/pull/3236) **(已合并)**
    - **内容**：集成了对 DeepInfra 模型提供商的支持。
    - **意义**：由社区贡献，增加了 CodeWhale 可使用的模型种类，为用户提供更多选择，反映了一个健康、积极的社区。
6.  [#3267 - feat(tui): 保持大型粘贴内容内联](https://github.com/Hmbown/CodeWhale/pull/3267) **(已合并)**
    - **内容**：针对 issue #3263，当粘贴内容过大时，不再强制转为文件引用，而是截断并保持可编辑状态。
    - **意义**：显著改善了编辑体验，避免了因自动文件创建而丢失对原始文本的编辑能力。
7.  [#2998 - chore(deps-dev): tailwindcss 升级](https://github.com/Hmbown/CodeWhale/pull/2998) **(已合并)**
    - **内容**：将 `/web` 网站项目的 Tailwind CSS 从 v3 升级到 v4。
    - **意义**：清理了技术债，为网站的前端开发解锁了更多新特性。
8.  [#2933 - feat(hippocampal): v2 记忆系统](https://github.com/Hmbown/CodeWhale/pull/2933) **(开放中，需人工审核)**
    - **内容**：一个关键的重磅 PR，引入了包含术语表、命名空间、回滚、自动注入和后台守护进程的 v2 记忆系统。
    - **意义**：这是 CodeWhale 从短期上下文窗口走向持久化、跨会话记忆的关键一步，是增强 Agent 智能水平的基石性工作。

## 5. 功能请求趋势
*   **多 Agent 编排与协调**：除了正在进行的 #2007 协调 Agent 运行外，多个问题和 PR (如 #2870) 都指向了让多个 Agent 更智能、更有序地协作，包括角色分配、意见分歧仲裁和可视化工作流报告。
*   **模型与提供商管理**：社区强烈要求提供内聚的模型元数据管理 (#3071)，并支持更多提供商 (如 #3236)。这表明用户希望获得更灵活、更可配置的模型选择体验。
*   **更优的粘贴与编辑体验**：从 #3263 和 #3267 可以看出，用户希望编辑体验更自然、更可控，尤其是在处理大量文本时，不希望被强制转换为文件引用。
*   **系统提示架构升级**：通过 #3015 可以看到，项目正在将系统提示从静态 Markdown 文件转向一个由 YAML 源文件通过渲染器生成的“宪法式”提示系统，追求更可靠和可维护的 Agent 行为控制。

## 6. 开发者痛点
*   **任务“卡死”与无响应 (Stall/hang)**：这是目前最突出的问题，涉及 `yolo` 模式 (#2487) 和长时间运行任务 (#2739)。用户报告在超时后无法恢复上下文，这严重影响了工具的可靠性。
*   **子 Agent/工具调用导致死锁**：问题 #3266 报告了在并行运行子 Agent 时，使用 `block=True` 会导致 TUI 卡死。这表明 Agent 执行框架的并发控制存在缺陷。
*   **安装与平台兼容性**：Ubuntu 22.04 的 glibc 版本不匹配 (#3238) 和新版 Ubuntu 的构建依赖缺失 (#3270) 是 Linux 用户的主要障碍。Windows 上的代理配置问题 (#3273) 也影响了部分用户。
*   **UI 细节与冲突**：数字键 1-8 被热键劫持 (#3243) 和遗留的 `.deepseek` 目录 (#3240) 等问题，虽然不大，但持续消耗用户的注意力，反映了产品细节打磨的重要性。
*   **Agent 行为超出用户意图**：问题 #3275 的回归报告指出了 Agent 可能执行超出用户请求范围的操作，这是一个关键的信任和安全性问题，是当前 Agent 行为过于激进的普遍反馈。

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*