# OpenClaw Ecosystem Digest 2026-06-16

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-16 02:59 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-16

## Today’s Overview
OpenClaw saw exceptionally high activity today, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, **30 issues were closed** and **84 PRs were merged or closed**, reflecting a very active development cycle. A new beta release `v2026.6.8-beta.2` shipped with significant Telegram and WhatsApp channel delivery improvements. The community remains highly engaged, with long-standing feature requests and critical bugs continuing to attract discussion. Overall project health appears strong, though several high-severity issues (memory leaks, security regressions, session corruption) remain open and require maintainer intervention.

---

## Releases

### v2026.6.8-beta.2  
[View release](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.2)

**Highlights** (from release notes):
- **Telegram and WhatsApp channel delivery** are now richer and less brittle: structured rich text with tables, lists, expandable blockquotes, preserved intentional line breaks, and safer rich-media handling.
- Native draft migration support; CLI backend delivery improvements.
- No breaking changes or migration notes were reported in the release summary.

*Note: No other new releases were recorded in the 24‑hour window.*

---

## Project Progress

- **84 pull requests were merged or closed today**, indicating rapid iteration. Among the notable closed/merged PRs (from the top 30 by comment count):
  - `#90861` (closed) — fix `sessions_yield` over MCP being lost on CLI‑backed MCP turns.
  - `#68936` (closed) — added PR review autofix pipeline + Windows daemon for automated gateway supervision.
- Open PRs with significant activity:
  - `#89985` – preserve local package overrides during updates (XL size, maintainer ready for review).
  - `#93265` – streamline setup with agent‑assisted configuration (XL, ready for maintainer look).
  - `#92220` – fix large inbound PDFs not being extracted for text‑only agents (L, ready).
  - `#91800` – propagate external content provenance to policy hooks (M, needs proof).
  - `#92016` – fix global plugin hook registry not firing for tool‑call hooks (M, ready).
  - `#90946` – preserve inherited gateway PID across reparent during cleanup (M, ready).

Several PRs target stability, channel integrations, and security boundary handling. The project is particularly active in the **gateway, agents, and channel plugin** areas.

---

## Community Hot Topics

The most active discussions (by comment count) reveal deep community interest in platform support, security, and agent behavior.

1. **#75 – Linux/Windows Clawdbot Apps**  
   [Issue link](https://github.com/openclaw/openclaw/issues/75)  
   *Enhancement, P2, 109 comments, 79 👍*  
   The oldest and most‑voted issue: users strongly want desktop apps for Linux and Windows. No merged PR exists; still awaiting product decision.

2. **#25592 – Text between tool calls leaks to messaging channels**  
   [Issue link](https://github.com/openclaw/openclaw/issues/25592)  
   *P1, security, 32 comments*  
   Internal processing output (error handling, acknowledgments) being routed as visible messages. A critical UX/security issue with high community concern.

3. **#9443 – Prebuilt Android APK releases**  
   [Issue link](https://github.com/openclaw/openclaw/issues/9443)  
   *Enhancement, P2, 25 comments*  
   Users ask for compiled APK downloads; currently only source code is provided.

4. **#32473 – Control UI requires HTTPS/localhost secure context**  
   [Issue link](https://github.com/openclaw/openclaw/issues/32473)  
   *Bug, regression, P2, 17 comments*  
   VPS/Docker users hit a brick wall after configuring Brave key – no workaround documented.

5. **#22676 – Signal daemon stop() race condition on SIGUSR1 restart**  
   [Issue link](https://github.com/openclaw/openclaw/issues/22676)  
   *P1, message loss & crash loop, 17 comments*  
   Orphaned processes and send failures on gateway restarts.

**Underlying needs**: The community consistently pushes for **cross‑platform desktop clients**, **security hardening** (leak prevention, secure context enforcement), and **better release distribution** (Android APKs). The intense interest in #25592 shows that message‑level contamination during tool execution is a highly visible pain point.

---

## Bugs & Stability

### Critical (P0)
- **#91588 – Gateway Memory Leak** (RSS grows from 350MB to 15.5GB over days, OOM kills)  
  [Issue link](https://github.com/openclaw/openclaw/issues/91588)  
  12 comments, reported 2026-06-09. No fix PR visible. This is the highest‑severity open bug; likely caused by uncollected session state or cached media.

### High (P1)
- **#25592 – Text between tool calls leaks to channels** (security, message loss) – no fix PR linked.
- **#22676 – Signal daemon race condition** (message loss, crash loops) – open PRs may exist but not linked.
- **#32296 – Agent replies to previous message** (session context confusion) – no fix PR.
- **#31583 – `exec` tool does not inherit `skills.entries.*.env` variables** (regression, security) – open.
- **#38439 – Webchat avatar endpoint returns 404** (regression) – live repro needed.
- **#41201 – Control UI avatar broken / 404** (regression) – duplicate of #38439.
- **#38327 – “Cannot convert undefined or null to object” with Google Vertex** (regression after 2026.3.2) – no fix.
- **#40611 – Heartbeat drift fix (PR #39182) blocks Telegram during active conversations** – linked PR open.

### Medium (P2)
- **#29387 – Bootstrap files in `agentDir` silently ignored** – user confusion, 14 comments.
- **#31331 – Docker Sandbox cannot access workspace** – file system mounting issue.
- **#37966 – `cacheRetention` ignored for LiteLLM Anthropic models** – behavior bug.
- **#34528 – Feishu reaction suffix causes 400 error** – message ID parsing bug.

### Observations
Many regressions relate to configuration (env vars, avatar, sandbox) and channel‑specific behaviors (Telegram, Feishu, Discord). Several have linked PRs with “needs proof” status, indicating fixes are proposed but not yet validated. The memory leak (#91588) and the tool‑text leak (#25592) are the two most urgent stability threats.

---

## Feature Requests & Roadmap Signals

A large number of feature requests received community traction and maintainer labeling. Likely candidates for the next minor release:

| Issue | Feature | Priority | Prediction |
|-------|---------|----------|------------|
| #39604 | `allowPrivateNetwork` config for `web_fetch` | P2 | High demand (9👍), simple opt‑in – likely soon |
| #10659 | Masked secrets to hide raw API keys from agents | P1 | Security critical, may land with security review |
| #22438 | Tiered bootstrap file loading for progressive context | P2 | Strong design discussion (17 comments) – next major |
| #12602 | Slack Block Kit support | P2 | Community wants richer Slack replies |
| #6731 | Safe/unsafe ClawdBot (sandbox mode) | P1 | Tied to Rust rewrite proposal, longer term |
| #20786 | Telegram Business Bot support | P2 | 6👍, clear use case – could be pushed |
| #13583 | Pre‑response enforcement hooks (hard gates) | P2 | Financial/security use cases, high interest |
| #13616 | Backup/restore utility | P2 | Repeatedly requested for environment migration |
| #14785 | Reduce tool schema token overhead (~3,500 tok/session) | P2 | Cost savings for all users – smart optimization |
| #42026 | Distributed agent runtime (split control plane) | P2 | RFC with 6 comments, architecturally heavy |
| #40418 | Automatic session memory preservation on `/new` | P2 | Addresses “forgetfulness” – likely after context improvements |

**Trend**: The community is asking for **security hardening** (masked secrets, sandbox, network access control), **scalability** (distributed runtime, memory preservation), and **UX polish** (tool schema overhead, Block Kit, backup/restore). The “safe/unsafe” proposal suggests a Rust rewrite, but that appears distant.

---

## User Feedback Summary

**Satisfaction**:  
- Release `v2026.6.8-beta.2` brings welcome improvements to Telegram/WhatsApp rich messaging, which has been a long‑standing request.
- Several active PRs (e.g., for PDF extraction, hook registry fixes) demonstrate responsive maintainers.

**Pain points**:
- **Memory leak** (#91588) is causing production outages – OOM kills disrupt workflow.
- **Tool output leaking** (#25592) undermines trust and risks data exposure.
- **No Linux/Windows apps** (#75) – the oldest and most‑upvoted issue remains unaddressed.
- **Android absence** (#9443) blocks mobile users.
- **Configuration friction** – users report being unable to fix avatar, bootstrap files, environment variables, or HTTPS requirement.
- **Race conditions** in Signal, Telegram, and gateway restarts cause message loss.
- **Security concerns**: secrets visible to agents, no denylist for exec approvals, private network access blocked by default.

**Positive signals**: Users are actively contributing PRs (84 merged today), and many issues have productive discussions with workarounds. The community is invested in improving the project.

---

## Backlog Watch

Issues that are important, have been open for months, and still lack a merged fix or maintainer decision:

| Issue | Created | Priority | Status |
|-------|---------|----------|--------|
| #75 – Linux/Windows apps | 2026-01-01 | P2 | 109 comments, 79👍 – needs product decision |
| #25592 – Text leak between tool calls | 2026-02-24 | P1 | 32 comments, security impact – needs maintainer review |
| #22676 – Signal daemon race condition | 2026-02-21 | P1 | 17 comments, crash loop – needs maintainer review |
| #29387 – Bootstrap files ignored | 2026-02-28 | P1 | 14 comments – needs product decision |
| #32473 – Control UI HTTPS requirement | 2026-03-03 | P2 | 17 comments, regression – needs product decision |
| #9443 – Prebuilt Android APK | 2026-02-05 | P2 | 25 comments – needs product decision |
| #91588 – Memory leak | 2026-06-09 | **P0** | 12 comments, critical – no fix PR yet |
| PR #39065 – Configurable unpaired DM responses | 2026-03-07 | P1 | Waiting on author for months |
| PR #12581 – Emit session prune lifecycle event | 2026-02-09 | P2 | Stale, needs maintainer attention |

These items are blocking user adoption and causing reliability issues. Immediate attention from maintainers is recommended for the memory leak (#91588) and the tool‑text leak (#25592), followed by the Signal race condition and the Linux/Windows desktop gap. The number of “needs product decision” labels suggests that several important enhancements lack a clear directive, which could be slowing progress.

---

*This digest was generated from GitHub data (issues, PRs, releases) updated in the 24 hours ending 2026-06-16.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

**Date:** 2026-06-16  
**Scope:** 8 active projects in the personal AI assistant / agent framework space

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is experiencing a phase of rapid maturation, characterized by high issue throughput, frequent patch cycles, and converging architectural patterns around MCP (Model Context Protocol), multi-agent orchestration, and channel abstraction layers. Projects are actively battling reliability regressions—particularly memory leaks, OAuth flow breaks, and session corruption—while simultaneously shipping new features for context compression, token visibility, and rich media handling. The ecosystem is bifurcating between "reference implementations" (OpenClaw) that prioritize completeness and "lightweight derivatives" (PicoClaw, NanoClaw, NullClaw) that emphasize minimal resource footprints or specific deployment scenarios. Community engagement remains high across the top-tier projects, though maintainer bandwidth appears to be a bottleneck for several second-tier codebases.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases Today | Health Score (1-10) | Dominant Activity Type |
|---------|----------------------|-------------------|----------------|---------------------|------------------------|
| **OpenClaw** | 500 | 500 | 1 (beta) | 7 | High-velocity iteration, critical bugs open |
| **NanoBot** | 5 | 25 | None | 6 | Targeted bug fixes, incremental features |
| **Hermes Agent** | 50 | 50 | None | 6 | Stability patches, gateway adapter fixes |
| **PicoClaw** | 3 | 13 | 1 (nightly) | 7 | Code hardening, security advisory resolved |
| **NanoClaw** | 0 | 12 | None | 5 | Infrastructure upgrades, fix PRs pending |
| **NullClaw** | 2 | 1 | None | 3 | Near-stagnant, 2 unresolved bugs |
| **IronClaw** | 44 | 50 | None | 7 | Reborn stabilization, attachments epic |
| **CoPaw** | 50 | 50 | None | 6 | Rapid iteration, regressions from v1.1.11 |
| **Moltis** | 0 | 2 | None | 4 | Low activity, 2 new PRs |
| **LobsterAI** | 0 | 11 | None | 5 | Dictation/artifact refinements, stale bugs |
| **ZeroClaw** | 50 | 50 | None | 7 | Bug fixes + RFCs, v0.8.1 prep |
| **TinyClaw** | 0 | 0 | None | 2 | Inactive |
| **ZeptoClaw** | 0 | 0 | None | 2 | Inactive |

**Notes:**  
- OpenClaw's 500/500 figures represent the highest raw volume in the ecosystem by a wide margin.  
- Health score is a composite of bug severity, merge throughput, community responsiveness, and backlog age.  
- "Dominant Activity" reflects the primary type of contribution in the 24h window.

---

## 3. OpenClaw's Position

**Advantages vs peers:**  
- **Community scale:** 109+ comments on oldest feature request (#75), largest contributor base.  
- **Release velocity:** Beta releases with structured channel improvements (Telegram/WhatsApp rich text).  
- **Bug discovery rate:** High issue count surfaces edge cases faster than any peer, though at the cost of maintainer overload.  
- **Architecture maturity:** Gateway, plugin hooks, session management infrastructure is more extensive than NanoClaw, PicoClaw, or NullClaw.

**Technical approach differences:**  
- OpenClaw adopts a **monolithic core + plugins** model, while NanoBot and Hermes Agent favor **modular agent loops** with explicit skill routing.  
- CoPaw and ZeroClaw are pursuing **multi-agent routing** (A2A, agent discovery) more aggressively than OpenClaw.  
- OpenClaw's memory leak (#91588, P0) is the ecosystem's most severe single bug, indicating potential architectural debt in session state management.

**Community size comparison:**  
- OpenClaw's issue #75 (Linux/Windows desktop apps) has 79 👍, far exceeding any single feature request in other projects (Hermes' #18715: 15👍; ZeroClaw's #2767: 9👍).  
- However, NanoBot and Hermes Agent show proportionally higher per-issue contribution quality (more fix PRs per reported bug).

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across **multiple** projects, indicating ecosystem-wide priorities:

| Focus Area | Projects Affected | Specific Needs |
|------------|-------------------|----------------|
| **Security hardening** | OpenClaw, Hermes, ZeroClaw, CoPaw | Masked secrets, tool-call leak prevention (#25592, #10659), prompt injection mode per agent (#7749) |
| **Context & token optimization** | CoPaw, ZeroClaw, Hermes, NanoBot | Headroom compression (#5063), native compression decorator (#7673), token usage UI (#4284), context sliding window fixes |
| **Multi-agent / A2A orchestration** | ZeroClaw, Hermes, IronClaw, NanoBot | Agent discovery RFC (#7218), agent-to-agent protocol plugin (#41711), conversation handoff |
| **OAuth / credential reuse** | IronClaw, ZeroClaw, NanoBot | Cross-thread OAuth reuse (#4913, #4935), retry on transient OAuth failures (#7739), credential scoping |
| **Channel reliability** | OpenClaw, Hermes, PicoClaw, NanoClaw | Telegram polling conflicts (#29325, #46996), Signal daemon race (#22676), WhatsApp media routing (#2778) |
| **Cross-platform desktop clients** | OpenClaw, Hermes, CoPaw | Linux/Windows apps (#75), macOS compilation failure (#40187), desktop crash loop on ARM (#5209) |
| **Configuration ergonomics** | ZeroClaw, OpenClaw, NullClaw | Alias renaming (#7468), rate-limit documentation (#957), config round-trip loss (#7532) |
| **Observability** | IronClaw, CoPaw, NanoBot | Trace-commons agent onboarding (#4929), Langfuse/OpenTelemetry (#5009), audit tool for tool calls (#4320) |

**Underlying driver:** Users demand production-grade reliability (retry, isolation, monitoring) as agents move from experimental to operational use.

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architecture Distinctive | Key Strategic Gap |
|---------|---------------|-------------|--------------------------|-------------------|
| **OpenClaw** | Complete feature reference | Advanced users, integrators | Rich channel plugins, gateway abstraction | Desktop app, memory leak |
| **NanoBot** | Production agent reliability | Developers, automation | WebUI parity, automation management | Empty-response fallback logic |
| **Hermes Agent** | Enterprise-grade agent ops | Ops teams, enterprise | A2A protocol, approval delegation | Desktop compilation, context bloat |
| **PicoClaw** | Lightweight embedded agent | Embedded/IoT users | Minimal footprint, nightly builds | Windows QQ integration broken |
| **NanoClaw** | Media + MCP extensibility | MCP plugin developers | Remote MCP server support, WhatsApp | Fix PR backlog (7+ days stale) |
| **NullClaw** | Minimal headless runtime | CLI-first users | Alpine-based Docker, low deps | Near-stagnant, local model broken |
| **IronClaw** | Next-gen agent loop (Reborn) | Early adopters, vision users | Attachments epic, Wasmtime security | OAuth resume broken, automations fail |
| **CoPaw** | Chinese ecosystem + enterprise | Chinese-market users | Feishu, WeChat, XiaoYi channels | Desktop crash, attachment 404 regression |
| **Moltis** | External agent integration | Agent aggregators | External-agent model/effort selection | No community engagement |
| **LobsterAI** | Cowork dictation + artifacts | Knowledge workers | Document artifact sharing, voice input | Skill management UX broken (74 days) |
| **ZeroClaw** | Next-gen security + multi-agent | Security-conscious, advanced | WASM-first, A2A discovery, compression | MCP scoping broken, session race |

**Key differentiation axes:**  
- **Scope:** OpenClaw, ZeroClaw, IronClaw aim for full-stack agent platforms; PicoClaw, NanoClaw, NullClaw are purpose-built.  
- **Geography:** CoPaw and LobsterAI prioritize Chinese channels and language; others are global.  
- **Architecture:** ZeroClaw's WASM-first approach and A2A focus is unique; Hermes' approval delegation mechanism is the most enterprise-ready.

---

## 6. Community Momentum & Maturity

**Tier 1: High-Maturity, High-Velocity**  
These projects have large contributor bases, frequent releases, and are addressing systemic bugs while shipping new features:  
- **OpenClaw** — Dominant by volume, but critical debt (memory leak, tool leak) undermines reliability.  
- **IronClaw** — Strong stability focus (18 PRs merged today), attachments epic advancing.  
- **CoPaw** — Very active, but regressions from rapid iteration (v1.1.11.post2) erode trust.  
- **ZeroClaw** — Methodical progress toward v0.8.1/v0.9.0, active RFC reviews.

**Tier 2: Active, Niche-Stable**  
These projects are maturing but have specific pain points that slow adoption:  
- **NanoBot** — Steady iteration on automation and observability, but empty-response fallback gap.  
- **Hermes Agent** — Enterprise features advancing (approval delegation, A2A), but desktop/macOS issues persist.  
- **PicoClaw** — Solid code-hardening phase, but Windows QQ bug unresolved.  

**Tier 3: Low-Activity, Maintenance Mode**  
These projects risk stagnation:  
- **NanoClaw** — Fix PRs accumulating without review (7-20 days stale), low community engagement.  
- **LobsterAI** — Core skill management bugs untouched for 74 days, though voice/dictation features move.  
- **NullClaw** — Only 2 open issues, both unresolved; no merged PRs in weeks.  
- **Moltis** — No community interaction; 2 open PRs with zero comments.  

**Tier 4: Dormant**  
- **TinyClaw**, **ZeptoClaw** — No activity.  

**Momentum signals:**  
- OpenClaw's beta release cadence indicates *toward* stabilization, but P0 bugs delay general availability.  
- ZeroClaw's RFC-driven development shows mature planning.  
- CoPaw's rapid feature merges reflect *growth*, but regression frequency suggests need for QA process investment.

---

## 7. Trend Signals

### Industry Trends Extracted from This Week's Data

**1. Security is the #1 user concern**  
Every major project has at least one open security-related issue with high community engagement:  
- Tool-call output leaks (OpenClaw #25592, 32 comments)  
- Prompt injection per-agent control (ZeroClaw #7749)  
- Approval delegation gaps (Hermes #37771, IronClaw #4764)  
- Secret masking (OpenClaw #10659)  

*Value for developers:* Implement output sanitization as a cross-cutting concern, not a per-channel fix.

**2. Context optimization is the top performance bottleneck**  
Requests for token compression, context visibility, and sliding windows appear across CoPaw, ZeroClaw, Hermes, and NanoBot. Users report OOM kills, session drop, and excessive costs.  

*Value for developers:* Integrate compression decorators early; provide real-time token usage in UI.

**3. Multi-agent orchestration is moving from research to production**  
ZeroClaw's A2A discovery RFC (#7218), Hermes' A2A protocol plugin (#41711), and CoPaw's Agent OS Driver (#5067) all signal a shift toward agent interoperability standards.  

*Value for developers:* Build agent discovery and handoff protocols now; adopt MCP as the baseline.

**4. OAuth complexity is a recurring friction point**  
IronClaw, ZeroClaw, and CoPaw all have open issues about OAuth flows failing silently, not resuming after authentication, or not sharing credentials across sessions.  

*Value for developers:* Build OAuth handling with explicit retry, cross-session credential reuse, and visible error feedback.

**5. The desktop client gap is the largest single unmet need**  
OpenClaw's #75 (79👍), Hermes' #40187 (macOS), and CoPaw's #5209 (desktop crash) show that users expect native desktop experiences. The absence of polished Linux/Windows clients is a recurring complaint across the ecosystem.  

*Value for developers:* Invest in Tauri/Electron-based desktop shells; prioritize M1/M2 macOS and Wayland Linux compatibility.

**6. Chinese ecosystem integration is a growing differentiator**  
CoPaw (XiaoYi, Feishu, WeChat), LobsterAI (Chinese dictation), and PicoClaw (QQ channel) are explicitly targeting Chinese users. This is a separate market from the global English-first ecosystem.  

*Value for developers:* Consider localization and channel support for WeChat, Feishu, and QQ if targeting APAC markets.

**7. Reliability regression cycles are lengthening as projects grow**  
Both OpenClaw and CoPaw show patterns where new releases fix old bugs but introduce new regressions (e.g., CoPaw's v1.1.11.post2 attachment 404; OpenClaw's session loss). Community frustration is rising.  

*Value for developers:* Invest in integration test suites, canary releases, and feature flags to decouple deployment from breakage.

---

**Bottom line for technical decision-makers:**  
- **Choose OpenClaw** for maximum feature breadth and community support, but budget for stability work.  
- **Choose ZeroClaw or Hermes** for production-grade security and multi-agent needs.  
- **Choose CoPaw** for Chinese market and rich channel integration.  
- **Avoid** NullClaw, TinyClaw, ZeptoClaw for new deployments until they show resumed activity.  
- **Invest in** context compression, OAuth reliability, and desktop clients—these are the ecosystem-wide gaps that will define the next generation of agent platforms.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-16

## Today's Overview
Activity remains high: 5 issues were updated in the last 24 hours (4 open, 1 closed) and 25 pull requests saw updates (21 open, 4 merged/closed). No new releases were published today. Development is focused on bug fixes and incremental feature additions, with significant attention to agent reliability, provider compatibility, and WebUI parity. The community is actively testing edge cases and reporting regressions, while core contributors are merging improvements for session handling, tool integrations, and observability.

## Releases
None.

## Project Progress
Four pull requests were merged or closed in the last 24 hours. One notable merged fix is:
- **[#4348 [CLOSED] fix(session): keep auto compact suffix on user turn](https://github.com/HKUDS/nanobot/pull/4348)** – Changes idle auto-compaction to retain at least the recent suffix and extend backward to the containing user turn, preventing partial tool turns from being trimmed. Also adds regression tests.

Other merged/closed PRs (not individually listed in the top 20) contribute to stability improvements across the codebase.

## Community Hot Topics
The most discussed issues (by comment count) are:

- **[#4287 [OPEN] Empty model responses not triggering fallback](https://github.com/HKUDS/nanobot/issues/4287)** (2 comments) – Users report that when DeepSeek returns empty completions, the agent classifies the error as “non-fallbackable,” preventing automatic retry with alternative models. This is a core reliability gap for production deployments. A related fix PR [#4358](https://github.com/HKUDS/nanobot/pull/4358) addresses duplicate user turns during retry but does not yet solve the fallback classification.

- **[#4286 [OPEN] Missing "sustained goal" context](https://github.com/HKUDS/nanobot/issues/4286)** (1 comment) – A user reports that after assigning a long-running goal (article creation), the agent repeatedly loses track of the objective. A PR [#4359](https://github.com/HKUDS/nanobot/pull/4359) aims to resolve this by refreshing goal context lazily.

- **[#4322 [OPEN] NameError: `session_key` not defined](https://github.com/HKUDS/nanobot/issues/4322)** (1 comment) – A regression introduced by merging branches that refactored `_build_memory_context`. Stale but still unresolved.

No PRs accumulated comments today; most discussion happens in issue threads.

## Bugs & Stability
Several bugs reported today, ranked by severity:

1. **Critical – Installer failure on fresh Docker container** [#4360](https://github.com/HKUDS/nanobot/issues/4360) (new today) – `pip` syntax error during install on `debian:13`. Blocks new users from deploying. No fix PR yet.

2. **High – Empty model responses not triggering fallback** [#4287](https://github.com/HKUDS/nanobot/issues/4287) – See Hot Topics. A partial fix PR [#4358](https://github.com/HKUDS/nanobot/pull/4358) exists but does not address the core classification issue.

3. **Medium – Missing sustained goal context** [#4286](https://github.com/HKUDS/nanobot/issues/4286) – PR [#4359](https://github.com/HKUDS/nanobot/pull/4359) is open and directly targets this.

4. **Medium – Zero token usage in `/v1/chat/completions`** [#4309](https://github.com/HKUDS/nanobot/issues/4309) – Closed; fix likely merged.

5. **Low/Stale – NameError from `fix/prompt-caching` merge** [#4322](https://github.com/HKUDS/nanobot/issues/4322) – No fix PR identified yet.

Additionally, PRs under review address related stability concerns:  
- Audio transcription failure for `.ogg`/`.opus` (PR [#4353](https://github.com/HKUDS/nanobot/pull/4353))  
- Missing blue ticks in WhatsApp bridge (PR [#4354](https://github.com/HKUDS/nanobot/pull/4354))  
- Replay-window trimming breaking user turns (PR [#4349](https://github.com/HKUDS/nanobot/pull/4349))  
- Capped digest by characters instead of tokens (PR [#4352](https://github.com/HKUDS/nanobot/pull/4352))

## Feature Requests & Roadmap Signals
The following pull requests signal near-term roadmap priorities:

- **Automation management UI** [#4330](https://github.com/HKUDS/nanobot/pull/4330) – Adds a WebUI surface for listing, filtering, running, pausing/resuming, and deleting automations. Strongly requested for production workflows.
- **Audit tool for agent actions** [#4320](https://github.com/HKUDS/nanobot/pull/4320) – Low-overhead observability for agent tool calls, with configurable scope.
- **Silent cron jobs** [#4357](https://github.com/HKUDS/nanobot/pull/4357) – Allows scheduled jobs to run without auto-delivering a response unless there is something to report.
- **Keenable search provider** [#4350](https://github.com/HKUDS/nanobot/pull/4350) – Adds a new web search backend for research-heavy use cases.
- **Better Mistral support** [#4351](https://github.com/HKUDS/nanobot/pull/4351) – Fixes `reasoning_effort` values, system message handling, and max-completion-tokens mapping for Mistral models.
- **WebUI / config.json parity** [#4313](https://github.com/HKUDS/nanobot/pull/4313) – Closes the gap between UI settings and `config.json` with new write endpoints for temperature, tool limits, memory, etc.

These suggest the next minor release will likely include automation management, audit capabilities, and widened provider compatibility.

## User Feedback Summary
Real user pain points reported today:
- **Production reliability**: Empty responses from popular models (DeepSeek) not handled gracefully – user @glebov describes a degraded experience during peak hours (Issue #4287).
- **Long-running tasks broken**: @fablau encountered repeated loss of sustained-goal context, making multi-step assignments fail (Issue #4286).
- **Installation friction**: @The-Markitecht hit a syntax error on a fresh Debian container, highlighting missing test coverage for official base images (Issue #4360).
- **API completeness**: @alx1379 reported that the OpenAI-compatible endpoint always returns zero token usage, breaking cost tracking (resolved in #4309).

Satisfaction signals: Several feature PRs (automation, audit, silent jobs) show that contributors and users are actively shaping the product for more mature deployment scenarios.

## Backlog Watch
Issues and PRs that need maintainer attention:

- **[#4322 (NameError in context.py)](https://github.com/HKUDS/nanobot/issues/4322)** – Stale for 3 days with only a root-cause analysis but no fix branch. Affects users on the `fix/prompt-caching` branch who merge `main`.
- **[#4303 (MCP generator crash)](https://github.com/HKUDS/nanobot/pull/4303)** – Open for 5 days, addresses a `RuntimeError` during server reconnect. No recent updates despite being critical for streamableHttp MCP users.
- **[#4287 (empty response fallback)](https://github.com/HKUDS/nanobot/issues/4287)** – Growing attention but the underlying fallback logic remains unchanged; PR #4358 only addresses a side effect.

No long-unanswered questions were identified among the top 20 PRs. The project maintainers appear responsive, but these items may block users on specific branches or configurations.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — Project Digest for 2026-06-16

## 1. Today’s Overview

The Hermes Agent project remains highly active, with **50 issues and 50 PRs updated in the last 24 hours**. Activity is concentrated around stability fixes for gateway adapters (Telegram polling conflicts, Slack Socket Mode) and multi-session isolation. Two PRs were merged/closed today, and seven issues were closed. The community continues to raise concerns about desktop app compilation on macOS, skill-bloat in context windows, and enterprise security gaps (approval delegation). No new releases were published.

## 2. Releases

**No new releases today.** The latest tagged release remains v0.16.0 (2026-06-05). Users awaiting desktop updates should monitor the `hermes update` command and the build pipeline (see known macOS issue #40187).

## 3. Project Progress

Two pull requests were merged/closed today:

- **#30785** (`fix(tui): include devDependencies in npm install for esbuild`) — Resolves an `ERR_MODULE_NOT_FOUND` error when running `hermes --tui` under CI environments by adding `--include=dev` to the npm install command. [[PR](https://github.com/NousResearch/hermes-agent/pull/30785)]
- **#46996** (`fix(telegram): isolate getUpdates polling transport`) — Mitigates repeated Telegram `409 Conflict` polling loops by disabling HTTP keep-alive on the polling transport and adding environment-variable timeouts. [[PR](https://github.com/NousResearch/hermes-agent/pull/46996)]

Additionally, two issues were closed: **#46973** (appears to be a product research note in Chinese) and **#47000** (a sysops incident report in German, likely internal). No further merged PRs were recorded.

## 4. Community Hot Topics

The most active discussions and highest-reaction issues:

- **#7237** (50 comments, 6 👍) — [Bug] `Response truncated due to output length limit` when generating long responses in CLI, Telegram, Discord, or Slack. This is a long-standing (April 2026) issue affecting users who rely on verbose or analytical outputs. [[Issue](https://github.com/NousResearch/hermes-agent/issues/7237)]
- **#18715** (4 comments, 15 👍) — Feature request for remote Hermes Agent with local tool execution. High demand indicates a strong use case for heterogeneous compute setups. [[Issue](https://github.com/NousResearch/hermes-agent/issues/18715)]
- **#40187** (8 comments) — Desktop app compilation failure on macOS (`hermes update` / `hermes desktop`). Still open with 0 👍, but frequent discussion. [[Issue](https://github.com/NousResearch/hermes-agent/issues/40187)]
- **#22620** (5 comments) — Skill list bloat causing massive context window inflation; requests for vector‑based routing or lazy loading. [[Issue](https://github.com/NousResearch/hermes-agent/issues/22620)]

The **MCP server misconfiguration** issue (#31246) continues to see activity, highlighting the need for better user-facing error messages when MCP packages are missing.

## 5. Bugs & Stability

Several bugs reported today (updated 2026-06-16) are ranked by severity:

### P1 / Critical
- **#46675** — Max OAuth requests rejected as third‑party (HTTP 400) due to single‑underscore `mcp_` tool‑name prefix on Anthropic’s Claude Max. This is a fundamental authentication blocker for enterprise users. No fix PR exists yet. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46675)]
- **#40691** — Telegram Gateway freezes after polling conflict recovery; passive routing stops entirely (process remains running but unresponsive). PR #29326 (still open) attempts to address this. [[Issue](https://github.com/NousResearch/hermes-agent/issues/40691)]

### P2 / High
- **#46303** — Concurrent sessions cross‑contaminate shared memory and git worktrees, causing data corruption. No isolation implemented. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46303)]
- **#46934** — Stale `resume_pending` sessions bypass idle reset after gateway restart, causing context bleed. Fix PR **#46997** is open. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46934) | [PR](https://github.com/NousResearch/hermes-agent/pull/46997)]
- **#46941** — Terminal commands truncated in code blocks on Feishu (Lark) due to `tool_preview_length` hard‑limit. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46941)]
- **#46897** — Background‑review emits “Skill created” notification solely on tool success, without verifying the skill is loadable from the session’s search root. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46897)]
- **#46917** — Forced response even when zero output is desired (“silence” issue). [[Issue](https://github.com/NousResearch/hermes-agent/issues/46917)]
- **#31246** — MCP server misconfiguration is invisible (errors logged at DEBUG only). [[Issue](https://github.com/NousResearch/hermes-agent/issues/31246)]

### P3 / Moderate
- **#46975** — Zombie dashboard processes accumulate when switching profiles, consuming ~700 MB RAM after days of use. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46975)]
- **#46989** — `replaceTextPart` causes visible flicker in TUI when messages complete (text disappears and reappears). [[Issue](https://github.com/NousResearch/hermes-agent/issues/46989)]
- **#46961** — Model switch from bottom bar silently fails with no visual feedback in Desktop app. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46961)]
- **#46918** — “Trigger now” button in cron jobs dashboard does not execute the job. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46918)]

**Fix PRs opened today** to address some of these issues: #46993 (subdirectory hints alignment), #46995 (Windows MSYS path normalization), #46999 (malformed session index entries), #47001 (web_extract with ddgs package), #47003 (Slack Socket Mode backend preference).

## 6. Feature Requests & Roadmap Signals

Significant feature requests discussed today:

- **#22620** (P3) — Vector‑based skill routing / lazy loading to prevent context window inflation. Likely to be part of the next minor release (v0.17) given sustained interest. [[Issue](https://github.com/NousResearch/hermes-agent/issues/22620)]
- **#18715** (P3, 15 👍) — Remote agent with local tool execution. Could become a major architectural change; may appear as a plugin or config option. [[Issue](https://github.com/NousResearch/hermes-agent/issues/18715)]
- **#46097** (P3, 2 👍) — Desktop font size setting. A simple UI fix that has been deferred. [[Issue](https://github.com/NousResearch/hermes-agent/issues/46097)]
- **#44761** (P3) — Global maximum concurrent usage lock for self‑hosted LLMs. [[Issue](https://github.com/NousResearch/hermes-agent/issues/44761)]
- **#46908** (P3) — Config gate to suppress background‑review notifications (mirror `display.tool_progress`). [[Issue](https://github.com/NousResearch/hermes-agent/issues/46908)]

**PRs indicating roadmap direction:**
- **#37771** — Approval delegation mechanism v2 (enterprise security gap). [[PR](https://github.com/NousResearch/hermes-agent/pull/37771)]
- **#41711** — Consolidated A2A (Agent‑to‑Agent) protocol plugin. [[PR](https://github.com/NousResearch/hermes-agent/pull/41711)]
- **#46554** — System‑browser OIDC sign‑in supporting passkeys / WebAuthn. [[PR](https://github.com/NousResearch/hermes-agent/pull/46554)]

These suggest the next version will emphasize **enterprise security, multi‑agent interoperability, and authentication improvements**.

## 7. User Feedback Summary

**Pain points** voiced today:

- **Desktop installation blocked by network restrictions** — Users in China report infinite hangs when installing the desktop app because GitHub (Electron) downloads are blocked, even when a proxy is configured (#46839, #42882, #46939). Workaround requires switching proxy to global / virtual network card mode.
- **macOS compilation failure** persists for `hermes update` and `hermes desktop` (#40187) — affects users with M1/M2 Macs.
- **Custom provider models invisible in Desktop dropdown** (#40480) — inconsistent UX between CLI and GUI.
- **Memory and context explosion** with many skills or long sessions (#46303, #22620) — power users report degraded performance.
- **Telegram bot unreliability** — 409 conflicts, silent freezing, and passive routing stops (#29325, #40691, #46934) frustrate users relying on group chat routing.

**Satisfaction signals** are scarce in today’s data, but the high number of open PRs (~44) indicates active contributor engagement. Users praise the extensibility (MCP, plugins) but demand better error messages and isolation.

## 8. Backlog Watch

Issues and PRs that have remained open for extended periods without maintainer resolution:

- **#7237** (Issue, Apr 10) — Response truncated due to output length limit. High comments (50) but no fix PR. Closed? (Status shows CLOSED, but no linked PR). Needs re‑evaluation. [[Issue](https://github.com/NousResearch/hermes-agent/issues/7237)]
- **#18715** (Feature, May 2) — Remote agent with local tool execution. 15 👍, but no progress. [[Issue](https://github.com/NousResearch/hermes-agent/issues/18715)]
- **#29325** (Bug, May 20) — Telegram polling conflict without duplicate gateway. PR #29326 exists but remains open. [[Issue](https://github.com/NousResearch/hermes-agent/issues/29325) | [PR](https://github.com/NousResearch/hermes-agent/pull/29326)]
- **#31246** (Bug, May 24) — MCP server misconfiguration invisible (DEBUG‑only logs). Unassigned. [[Issue](https://github.com/NousResearch/hermes-agent/issues/31246)]
- **#13420** (PR, Apr 21) — Make Telegram lifecycle reactions configurable by chat type. Awaiting review. [[PR](https://github.com/NousResearch/hermes-agent/pull/13420)]
- **#16889** (PR, Apr 28) — Feishu stream edit rotation for message limits. Stalled. [[PR](https://github.com/NousResearch/hermes-agent/pull/16889)]

Maintainers should prioritize **#31246** (MCP misconfiguration) and **#29325** (Telegram polling) as they directly impact usability and have reproducible fixes ready.

---

*Generated from GitHub data retrieved on 2026-06-16. All links are to NousResearch/hermes-agent.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-16

## 1. Today’s Overview

Activity remains high, with **13 pull requests** and **3 issues** updated in the last 24 hours. One new **nightly release** (v0.2.9-nightly) was published. The project shows a strong focus on code quality and stability: a dozen open PRs address error-handling lapses, missing type-assertion checks, and unprotected goroutines. A security advisory involving the launcher’s `allowed_cidrs` was resolved, and a UI enhancement (Shift+Enter hint) was merged. Community engagement is moderate; one Windows-specific bug remains open.

## 2. Releases

**nightly (v0.2.9-nightly.20260616.c1ff5aa6)**  
- Automated nightly build, marked as potentially unstable.  
- No breaking changes or migration notes provided.  
- Full changelog: https://github.com/sipeed/picoclaw/compare/v0.2.9...main  

This is a rolling snapshot from the `main` branch; users should treat it as a preview.

## 3. Project Progress (Merged/Closed PRs Today)

Three pull requests were merged or closed:

- **#3096** (`docs: add PicoPaw banners to READMEs`) – Documentation update to include branding banners.  
  https://github.com/sipeed/picoclaw/pull/3096  
- **#3126** (`fix(web): improve launcher allowlist bypass diagnostics`) – Adds logging to detect when `allow_localhost_bypass` is omitted/null, closes the security issue described in #3069.  
  https://github.com/sipeed/picoclaw/pull/3126  
- **#3097** (`feat: add shift-enter hint below chat composer`) – Web UI improvement: shows a “Shift+Enter” hint when the user types content, reducing confusion about newline behaviour.  
  https://github.com/sipeed/picoclaw/pull/3097  

Additionally, issues **#2887** (stale .deb/OpenAI bug on RISC-V) and **#3069** (security bypass) were closed.

## 4. Community Hot Topics

**#2887 – [BUG] .deb version on RISC-V is not functional with OpenAI model**  
10 comments | closed as stale  
https://github.com/sipeed/picoclaw/issues/2887  
Users reported that the .deb package on RISC-V cannot connect to OpenAI models. The issue was closed without a fix; this may indicate limited support for that architecture or a need for maintainer clarification.

**#3015 – [BUG] QQ channel connection failure on Windows**  
3 comments | still open  
https://github.com/sipeed/picoclaw/issues/3015  
A Windows user reports that `picoclaw gateway` fails with a token retrieval timeout when connecting to QQ channels. Pico channel works normally. This is the only unresolved bug in the recent window and may require Windows-specific debugging.

**#3069 – [Security] launcher `allowed_cidrs` bypass**  
0 public comments | closed via PR #3126  
https://github.com/sipeed/picoclaw/issues/3069  
The security advisory was swiftly addressed; diagnostics were improved to detect misconfigurations.

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| Medium | #3015 – QQ channel connection fails on Windows | Open | No fix PR yet; Windows auth/token path may need investigation. |
| Medium | #2887 – .deb on RISC-V not functional with OpenAI | Closed (stale) | No resolution recorded; may affect RISC-V users. |
| Low | Several PRs fixing ignored `Close()` errors, missing type assertions, and panic-recovery gaps | In review | PRs #3127, #3128, #3129, #3130, #3131, #3132 improve code robustness. A panic in a goroutine could crash the process – PR #3132 adds defer-recover to core paths. |

No regressions were reported today. The project is actively hardening error handling and concurrency safety.

## 6. Feature Requests & Roadmap Signals

The only feature-oriented pull request currently open is:

- **#2975** (`feat(telegram): treat reply to bot message as mention in group chats`) – Extends Telegram group behaviour: replying to a bot message now triggers a response even if `mention_only: true` is set.  
  https://github.com/sipeed/picoclaw/pull/2975  

This is likely to be merged in the next minor release. No other user-requested features appeared in the recent issue stream. The merged **#3097** (Shift+Enter hint) shows the team is investing in Web UI polish.

## 7. User Feedback Summary

- **Pain point:** Windows QQ channel integration broken for at least one user (#3015).  
- **Pain point:** RISC-V .deb users faced a blocking issue (#2887) with no published fix before closure.  
- **Positive feedback (implicit):** The security bypass fix (#3069/ #3126) was handled transparently, with improved diagnostics.  
- **Use case:** Teams relying on the launcher behind reverse proxies will benefit from the enhanced allowlist logging.  
- **Community sentiment:** Active contribution from multiple developers, especially on code quality (e.g., `chengzhichao-xydt`). No signs of widespread dissatisfaction.

## 8. Backlog Watch

| Item | Type | Age | Status | Attention Needed |
|------|------|-----|--------|-----------------|
| #3015 – QQ channel Windows bug | Issue | 10 days | Open, stale | Awaiting maintainer or contributor investigation |
| #3059 – Fix ignored `Close()` errors | PR | 8 days | Open, stale | Can be merged after review |
| #3054 – Fix LINE channel type assertions | PR | 8 days | Open, stale | Low risk, could merge |
| #3047 – Restore full JSONL history | PR | 9 days | Open, stale | Important for session detail API, needs review |
| #2975 – Telegram reply-as-mention | PR | 17 days | Open, stale | Feature with clear utility, could be merged soon |

The stale label on several issues and PRs suggests maintainer bandwidth is a bottleneck. While no urgent crisis exists, #3015 and #3047 deserve priority attention to keep Windows users and API consumers satisfied.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-16

## Today’s Overview

No new releases or issues were created in the last 24 hours, but pull request activity was high: 12 PRs were updated, with 3 merged/closed and 9 still open. The closed PRs addressed infrastructure upgrades, conversation archiving, and documentation cleanup. Open PRs show an active development push around WhatsApp media handling, remote MCP server support, and new skills (Strava). The absence of open issues suggests the current pipeline is focused on code contributions rather than bug reports, though several long-standing fix PRs remain open.

---

## Releases

No new releases.

---

## Project Progress

Three pull requests were merged or closed today:

- [**#2774** feat(update-nanoclaw): upgrade OneCLI gateway when its pinned version moves](https://github.com/nanocoai/nanoclaw/pull/2774)  
  Merged. Adds version-pin tracking and automatic gateway/CLI upgrade when `update-nanoclaw` runs, preventing silent mismatches between new code and the running gateway.

- [**#2772** fix(codex): per-thread conversation archive (CDX-004)](https://github.com/nanocoai/nanoclaw/pull/2772)  
  Merged. Fixes Codex history management: from many single-exchange files to a single per-thread archive, reducing fragmentation and improving compaction behavior.

- [**#2773** docs(add-codex): drop redundant TTY warning in auth note](https://github.com/nanocoai/nanoclaw/pull/2773)  
  Closed. A documentation-only cleanup that removes a duplicated warning about non-interactive terminal usage.

---

## Community Hot Topics

No issues or PRs have comments or reactions today, so explicit community engagement is low. However, the following open PRs are likely to draw attention once reviewed:

- [**#2778** fix(whatsapp): route inbound media through shared session inbox](https://github.com/nanocoai/nanoclaw/pull/2778) — addresses a critical gap (media never reaching the agent).  
- [**#2777** feat: add /add-strava skill for official Strava MCP](https://github.com/nanocoai/nanoclaw/pull/2777) — introduces a popular external service integration.  
- [**#2776** feat: support remote HTTP/SSE MCP servers](https://github.com/nanocoai/nanoclaw/pull/2776) — a foundational infrastructure change for MCP extensibility.

---

## Bugs & Stability

Several bug fixes are in progress or were merged today. Ranked by severity:

**High Severity**
- [**#2778** fix(whatsapp): inbound media never reaches the agent](https://github.com/nanocoai/nanoclaw/pull/2778)  
  Open. Inbound WhatsApp media (images, video, audio, documents) is downloaded to the host but not mounted into agent containers, resulting in silent failure. Fix routes media through the shared session inbox.

- [**#2759** fix(agent-runner): deliver budget/billing error turns instead of dropping them](https://github.com/nanocoai/nanoclaw/pull/2759)  
  Open. When an LLM call exhausts budget/tokens, the error is silently dropped, confusing agents. Fix ensures the error turn is delivered properly.

**Medium Severity**
- [**#2626** fix(signal): replace silent restartService failure with explicit error](https://github.com/nanocoai/nanoclaw/pull/2626)  
  Open (since May 27). A `launchctl kickstart` call fails silently when the plist is not loaded, leaving the setup wizard in a broken state.

- [**#2627** fix(reactions): align MCP add_reaction schema with channel reality + Slack bridge translation](https://github.com/nanocoai/nanoclaw/pull/2627)  
  Open (since May 27). Reactions silently fail because emoji shortcodes are passed verbatim to channels expecting Unicode. Fix adds translation.

**Low Severity**
- [**#2628** fix(cli): honor user-supplied --id in `ncl groups create` and friends](https://github.com/nanocoai/nanoclaw/pull/2628)  
  Open (since May 27). The `--id` flag is documented as auto-generated but is always overridden; user-provided IDs are ignored.

- [**#2771** perf(container): --shm-size=1g + --init for agent containers](https://github.com/nanocoai/nanoclaw/pull/2771)  
  Open. Addresses Chromium crashes in headless browser due to insufficient shared memory, plus zombie process cleanup.

---

## Feature Requests & Roadmap Signals

The following PRs indicate strong roadmap directions:

- **Remote MCP servers** ([#2776](https://github.com/nanocoai/nanoclaw/pull/2776)) — adds support for HTTP/SSE MCP servers beyond stdio; likely to appear in the next minor release.
- **Strava integration** ([#2777](https://github.com/nanocoai/nanoclaw/pull/2777)) — a full skill with OAuth and auto-refreshing tokens; signals growing ecosystem of third-party MCP connections.
- **OneCLI gateway auto-upgrade** ([#2774](https://github.com/nanocoai/nanoclaw/pull/2774), merged) — improves infrastructure reliability; suggests that version-pinning and automated upgrades are becoming standard.

No user-requested feature issues were opened today, but the open feature PRs likely stem from internal roadmap items.

---

## User Feedback Summary

No new issues or comments were filed today, so direct user feedback is absent. However, the open fix PRs point to real pain points experienced by users:

- Inbound WhatsApp media silently failing (reported in #2778).
- Budget/billing errors being dropped instead of surfaced (#2759).
- Inability to set a custom group ID (#2628).
- Reaction emojis not working across WhatsApp/Discord/Telegram (#2627).
- Signal restart failures without error feedback (#2626).

These indicate that while the project is advancing, several usability and reliability issues remain unresolved.

---

## Backlog Watch

The following open PRs have been inactive or awaiting review for an extended period and may need maintainer attention:

- [**#2628** fix(cli): honor user-supplied --id in `ncl groups create`](https://github.com/nanocoai/nanoclaw/pull/2628) — open since May 27; last updated June 15.
- [**#2627** fix(reactions): align MCP add_reaction schema](https://github.com/nanocoai/nanoclaw/pull/2627) — open since May 27; last updated June 15.
- [**#2626** fix(signal): replace silent restartService failure](https://github.com/nanocoai/nanoclaw/pull/2626) — open since May 27; last updated June 15.
- [**#2759** fix(agent-runner): deliver budget/billing error turns](https://github.com/nanocoai/nanoclaw/pull/2759) — open since June 14; awaiting review.

These are all fix-oriented PRs from external contributors. Their age suggests a bottleneck in code review pipeline.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-16

## Today's Overview
Activity on the NullClaw repository remains low, with only two open issues and one open pull request updated in the last 24 hours. No new releases or merged contributions were recorded, indicating a period of slowed development or maintainer focus on other priorities. The most pressing concerns involve configuration (rate limiting) and model integration (incomplete local model responses). A single dependency bump PR (Alpine 3.23 → 3.24) suggests ongoing maintenance efforts, but no functional progress is visible today.

## Releases
No new releases were published. This section is omitted.

## Project Progress
No pull requests were merged or closed in the last 24 hours. The only PR updated is:

- **[#956 – ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956)** – A dependency update opened by Dependabot. This PR is still open and has no comments.

No features or fixes advanced today.

## Community Hot Topics
Both open issues attracted recent activity (comments within the last day):

- **[#957 – “Rate limit issue”](https://github.com/nullclaw/nullclaw/issues/957)** – Opened by jacktang on June 15. The user is using NullClaw as an agent runtime without memory and receives the message “The config reader hit a rate limit.” They ask for an explanation of the rate limit configuration and how to modify the threshold. The only comment is likely from the author or a maintainer; no resolution yet.

- **[#952 – [bug] Local model using ollama returns incomplete answers](https://github.com/nullclaw/nullclaw/issues/952)** – Opened June 11 by bloodgroup-cplusplus. Reports that after pulling Gemma via Ollama, the agent does not answer in complete sentences. A screenshot is attached. An update on June 15 may be a follow‑up comment. No fix or workaround has been posted.

**Underlying needs:** Users require clear configuration documentation (rate limit) and reliable integration with local Ollama models. Both issues point to gaps in user‑facing settings and model output handling.

## Bugs & Stability
Two stability‑related issues are currently open, both updated within the last 24 hours. Neither has a fix PR.

| Issue | Severity | Description |
|-------|----------|-------------|
| [#952 – Incomplete answers with Ollama](https://github.com/nullclaw/nullclaw/issues/952) | **High** | Agent returns truncated sentences when using local models (Gemma). Affects core usability for local‑model users. |
| [#957 – Rate limit configuration](https://github.com/nullclaw/nullclaw/issues/957) | **Medium** | “The config reader hit a rate limit” error blocks JSON output generation. Hard to diagnose because the configuration is undocumented. |

**Root cause analysis:** #952 may be a token‑limit, stop‑sequence, or context‑window issue specific to the Ollama integration. #957 likely refers to a built‑in rate limiter for configuration reads; the user cannot find documentation or threshold settings. No regression is indicated; these are likely existing issues now surfacing in user reports.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the configuration‑related question in #957 implicitly requests:

- **Expose and document rate‑limit parameters** – A configurable threshold value for the config reader.
- **Provide a user‑facing setting for output buffering or completion** – In response to #952, users may want control over max tokens or truncation policies.

Given the low activity and lack of maintainer responses, these are not likely to be addressed in the next minor version unless the project shifts focus to polish and documentation.

## User Feedback Summary
- **User pain points:**  
  - Lack of documentation for internal rate‑limiting configuration.  
  - Local models (Ollama) producing incomplete answers, making the agent unusable for real workloads.  
  - No clear contact point or response from maintainers on either issue.  
- **Use cases:**  
  - Using NullClaw as an agent runtime without memory (headless, JSON output).  
  - Running local models for offline/private agent tasks.  
- **Sentiment:** Frustrated but constructive – users provide detailed steps, ask for clarification, and attach screenshots. No signs of abandonment yet, but urgency is rising.

## Backlog Watch
The following issue has been open for 5 days without a maintainer response:

- **[#952 – [bug] Local model using ollama returns incomplete answers](https://github.com/nullclaw/nullclaw/issues/952)** – Opened June 11, last update June 15. No comment from the core team. This bug directly impacts a key feature (local model support) and is one of the most active items in the backlog.

No pull requests appear to be awaiting maintainer review or merge beyond the Dependabot PR #956.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-06-16

**Generated from GitHub data: Issues (44 updated), PRs (50 updated), releases (0).**

---

## 1. Today's Overview

Project activity remains high, with **44 issues** and **50 PRs** updated in the last 24 hours. The team is deeply engaged in stabilizing the **Reborn** next-generation agent loop and Web UI, addressing a wave of UX/onboarding bugs across Google, GitHub, and Notion extensions. An important security vulnerability in Wasmtime (RUSTSEC-2026-0182) prompted two urgent patch PRs today. On the feature side, the **attachments epic (#4644)** advanced with merged vision support for inline images, and a new **Slack user-token tool** was proposed. Overall, the project is in a strong maintenance and polish phase ahead of what appears to be a broader Reborn rollout.

---

## 2. Releases

**No new releases today.** No releases exist in the data for this date.

---

## 3. Project Progress

The following **18 PRs were merged or closed** today (based on PR status change in last 24h). Notable among them:

- **PR #4947** – *ci(bench): validate /benchmark suite against benchmarks main, not a stale pin* – Fixed a CI issue where custom benchmark suites were rejected by the `/benchmark` command.
- **PR #4929** – *fix(traces): resolve #4559 main-merge conflicts + tenant-scoped trace-credits test* – Unblocked trace-commons agent onboarding work.
- **PR #4871** – *feat(attachments): image attachment support for vision-capable models* – Merged after post-merge review follow-ups (#4945). This is step 4 of the attachments epic (#4644), enabling real multimodal image content for vision models.
- **PR #4780** – *Steer routine delivery through outbound targets* – Added model-visible guidance for routine/trigger creation and outbound delivery tool discovery.
- Several **small bug fix PRs** closed: #4928 (Notion OAuth redirect fix), #4917 (automations never run), #4915 (automations panel polish), #4867, #4854, #4886, #4800, #4759, #4807, #4890 – a mix of UX, OAuth, and extension issues.

---

## 4. Community Hot Topics

Most discussed issues and PRs (by comment count) this period:

- **#4825** (CLOSED) – *Reborn: persist "always allow" approvals across threads* – 3 comments. The fix was merged; this was a core UX issue where users had to re-approve capabilities per thread. Closes a long-standing frustration.
- **#4908** (OPEN) – *Google Calendar extension shows "Activate" action after already being active* – 3 comments. Highlights confusion in extension activation state. Underlying need: better state synchronisation between UI and backend for installed extensions.
- **#4880** (OPEN) – *Automate Code Review and Review Comment Resolution* – 2 comments. Part of a broader “coding agent cloud workflow” (#4878). Community interest in AI-assisted PR review and automated resolution of review comments.
- **#4907** (OPEN) – *Reborn: Run may fail after successful Google OAuth instead of resuming* – 2 comments. Critical for OAuth-dependent workflows; the model's execution is not resumed after successful auth, breaking the user flow.
- **#4764** (OPEN) – *Denying shell approval leaves tool invocation pending* – 2 comments. A denial should produce feedback, but the UI hangs. Demonstrated pattern of Reborn approval UX gaps.

**Reactions:** None of the top issues had 👍 reactions reported (all 0). This may reflect the API data limitation, but community engagement appears focused on bug reports rather than feature upvotes.

---

## 5. Bugs & Stability

**High severity:**

- **Wasmtime security vulnerability (RUSTSEC-2026-0182)** – Broken CI (`cargo-deny` failing on `main`). Two PRs fix it: #4950 (bump wasmtime 44.0.2 → 44.0.3) and #4949 (same patch). Immediate blocker for all other PRs.
- **#4907 – OAuth success does not resume execution** – Run fails after successful Google OAuth. No fix PR yet. Blocks Google Calendar/Gmail workflows.
- **#4942 – Tool calls failed not appearing until re-fetch** – SSE/WebUI real-time update issue. Affects user experience when GSuite or other tools fail.
- **#4887 – Provider-backed MCP tool approval resume fails with stale capability input_ref** – Approved capability cannot be resumed, results in error. Follow-up: #4931 adds test infrastructure.
- **#4921 – Gmail extension fails after successful authorization** – No response produced after auth. Likely related to #4907.

**Medium severity:**

- **#4761 – Agent stops after repeated tool failures instead of recovering** – Agent gives up rather than retrying or explaining failure. Mitigation PR #4841 is open (PR #4841 – "no run-borking failures").
- **#4764 – Denying shell approval leaves pending invocation** – UI freezes, no user feedback. Fix needed for fundamental approval UX.
- **#4917 – Automations never run** – Scheduled automations stuck at "SCHEDULED" and never fire. Closed as a bug with no PR fix visible; might have been fixed by other changes.
- **#4857 – Clean state incorrectly shows NEAR AI provider as Active** – Misleading inference provider status.
- **#4925 – NEAR AI MCP shows "SETUP NEEDED" despite being ready** – False positive in MCP server status.
- **#4913 – Google Calendar authorization not reused across conversations** – Cross-thread credential reuse broken.

**Low severity / UX polish:**

- #4923 – Logs/Docs icons need text labels
- #4926 – Expanding capabilities stretches all cards in a row
- #4886 – Installed extensions lack post-install guidance (closed)
- #4890 – Extension setup flow fragmented (closed)
- #4915 – Automations panel summary-card layout (closed)
- #4884 – Google Calendar auth prompt asks for access token instead of OAuth flow (still open)
- #4854 – GitHub extension excessive approval prompts (closed)

---

## 6. Feature Requests & Roadmap Signals

- **#4882 – Build Coding Agent Cloud Workflow** – Parent issue #4878. Proposes an AI coding agent that takes issues or mentions to produce PRs. PR #4801 (operator diagnostics) and PR #4876 (large dep bump) are related infrastructure. Likely in development for next release.
- **#4880 – Automate Code Review and Review Comment Resolution** – Close neighbor to #4882. Suggests AI-driven PR review comments and automated resolution. Could land as a beta feature.
- **#4935 – Credentials are owner-scoped, not thread-scoped** – This architectural change is being implemented in PR #4939. It will fix cross-thread OAuth reuse and is a prerequisite for many UX improvements. Likely to ship in the next minor release.
- **#4644 – Universal attachments across all channels** – The main attachments epic is progressing (PR #4871 merged, PR #4902 open for OpenAI-compat vision, PR #4945 follow-ups). Remaining steps: file upload/download UX (#4933 open), extensible format registry, polished web UX. Expected to complete over the next two sprints.
- **#4941 – Slack personal (user-token) tool** – New WASM tool for user-context Slack actions. Community contribution from sergeiest.
- **#4946 – Slack approval/auth UX overhaul** – PR #4946 in review, aims to fix recency gate resolution, busy hints, OAuth-only auth. Shows Slack channel is receiving UX investment.

**Roadmap signals:** The project is clearly focusing on **Reborn stability**, **extension onboarding UX**, **OAuth flow robustness**, and **attachment/image support**. No major version release is imminent, but the next release will likely include the credential scoping fix (PR #4939), the broken-run recovery (PR #4841), and the image attachment pipeline.

---

## 7. User Feedback Summary

Reported pain points (from issue descriptions):

1. **“Always allow” approval is not persisted across threads** (#4825) – Closed by #4825. Users expect one-time approvals to apply globally.
2. **Extension activation states are confusing** (#4908, #4886, #4890) – Inconsistent display of “ACTIVE” vs “SETUP NEEDED” vs “AUTH NEEDED”. Users cannot tell if an extension is ready.
3. **OAuth flows do not resume execution** (#4907, #4921, #4800) – After successful Google login, the original run fails silently. User is left with a dead conversation.
4. **Approval denials produce no feedback** (#4764) – Clicking “Deny” on a shell or tool approval leaves the tool in “RUN” state, user sees a spinning icon.
5. **Automations never fire** (#4917) – Users who create schedules see “SCHEDULED” but no runs ever occur, with no explanatory message.
6. **Workspace path duplication** (#4759) – Using `workspace/` prefix duplicates the path, creating incorrect file locations.
7. **GitHub tool returns issues mixed with pull requests** (#4807) – Closed by #4807.
8. **Provider status misleading on clean install** (#4857) – “NEAR AI” provider appears as ACTIVE when not configured.

**Positive signals:** None directly reported in the data, but the high number of closed bug fixes (13 issues closed today) indicates the team is responsive.

---

## 8. Backlog Watch

- **PR #3705** – *chore(deps): bump rand in /channels-src/wechat* – Opened 2026-05-16, still open after a month. Low-risk dep bump but appears stuck in review or CI. Minor concern for dependency hygiene.
- **Issue #4644** – *Universal attachments across all channels* – 2 comments, last updated 2026-06-15. While progress is being made, the core issue remains open and the full feature is not yet complete. Should be tracked as an epic.
- **Issue #4761** – *Agent stops after repeated tool failures instead of recovering* – No fix PR directly targeting this issue, though PR #4841 (no run-borking) addresses part of it. Needs explicit resolution.
- **Issue #4880** – *Automate Code Review and Review Comment Resolution* – Parent issue #4878 is closed? Actually #4878 is mentioned but not shown. The child issues #4880 and #4882 are still open with no PR merged yet. Might need maintainer attention if those are sprint priorities.
- **Issue #4931** – *test-support: teach MockAgentLoopDriverHost approval_resume scripting* – Open, no PR yet. This is a test infrastructure request to avoid large bespoke host implementations in tests. Low urgency but important for long-term maintainability.

**No issues appear to be abandoned** – all top issues have recent activity. The project maintainers are actively triaging and closing bugs.

---

*End of digest.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-16

## Today’s Overview

LobsterAI saw moderate activity over the last 24 hours, with **11 pull requests updated** (5 merged/closed) and **2 open issues** (both stale). No new releases were published. The development focus is on refining the cowork dictation experience, adding document artifact sharing and preview, and cleaning up CI/CD dependencies. The two remaining open issues—both related to local skill management (no success feedback, duplicate skill registration)—have been open since early April and remain unaddressed. Overall, the project is in a healthy state with frequent contributions, though some long-standing user-facing bugs need attention.

## Releases

No new releases were recorded today.

## Project Progress

The following **5 PRs were merged or closed** today, representing concrete progress:

- **[#2163](https://github.com/netease-youdao/LobsterAI/pull/2163)** – **feat(voice-input): refine dictation recording UI**  
  Refines the cowork dictation recording experience and ASR quota handling for the 2026.6.11 release branch.

- **[#2162](https://github.com/netease-youdao/LobsterAI/pull/2162)** – **fix(cowork): preserve voice input cancel guard after merge**  
  Resolves a merge conflict by keeping the release branch’s realtime-only ASR flow while preserving draft ownership, stale callback guards, and session-switch cancellation.

- **[#2160](https://github.com/netease-youdao/LobsterAI/pull/2160)** – **fix(voice-input): keep only realtime asr**  
  Removes the short ASR upload flow and legacy recognition mode settings, making Cowork voice input always start realtime ASR. Includes spec updates.

- **[#2159](https://github.com/netease-youdao/LobsterAI/pull/2159)** – **feat(artifacts): 支持文档 Artifact 分享与预览优化**  
  Adds document file sharing via artifacts: supports DOCX, PPTX, XLSX, PDF, CSV, TSV packaging, type validation, size limits, optimized rendering (pagination, PDF fallback, table auto-width). Includes design docs and CSP adjustments.

- **[#2161](https://github.com/netease-youdao/LobsterAI/pull/2161)** – **chore: update about**  
  Minor cleanup/update of the “About” dialog.

## Community Hot Topics

The two **open issues** are both stale (created April 3, last updated June 15) with 1 comment each and no reactions:

- **[#1426](https://github.com/netease-youdao/LobsterAI/issues/1426)** – Uploading a local skill provides no success prompt, and the skill list is not refreshed.  
- **[#1427](https://github.com/netease-youdao/LobsterAI/issues/1427)** – Uploading the same skill repeatedly results in duplicate skills.  

These issues highlight a clear user pain point: **poor feedback and lack of deduplication when managing skills locally**. No fix PRs have been opened, and the lack of activity suggests they may be deprioritised.

Among PRs, the open feature PR **[#1428](https://github.com/netease-youdao/LobsterAI/pull/1428)** (*feat(cowork): 会话完成/报错时推送系统通知 – system notification on session complete/error when window unfocused*) is also stale (created April 3). It has no comments or reactions but addresses a usability gap compared to tools like Claude Code and Cursor.

## Bugs & Stability

**High severity** – Two usability bugs remain open:

1. **No success prompt after skill upload** ([#1426](https://github.com/netease-youdao/LobsterAI/issues/1426)) – Blocks user awareness of successful operation.
2. **Duplicate skill registration** ([#1427](https://github.com/netease-youdao/LobsterAI/issues/1427)) – Allows invalid state (multiple skills with same name).

No fix PRs exist for either. A regression was avoided in today’s merged PRs (e.g., [#2162](https://github.com/netease-youdao/LobsterAI/pull/2162) preserved cancel guards after a merge conflict). No new crashes or regressions were reported.

## Feature Requests & Roadmap Signals

- **System notifications for session completion/error** (PR [#1428](https://github.com/netease-youdao/LobsterAI/pull/1428)) remains the most prominent feature request. Given the project’s emphasis on cowork UX (today’s voice input refinements and artifact preview enhancements), this feature is likely to be included in the next release to improve background task awareness.
- **Document artifact support** ([#2159](https://github.com/netease-youdao/LobsterAI/pull/2159)) is now merged, signalling that rich document sharing and preview are part of the upcoming road map.

## User Feedback Summary

- **Pain points**: Lack of feedback when adding skills; duplicate skill entries; inability to receive system notifications when sessions complete/error in background.
- **Use cases**: Users want to manage custom skills reliably and be notified of async session outcomes without manually checking the window.
- **Satisfaction**: The rapid merging of voice input and artifact features suggests core development is meeting power-user needs, but the long-unresolved skill management issues indicate a gap in localisation/front-end quality.

## Backlog Watch

Items that have been stale for over two months and require maintainer attention:

| Item | Age (days) | Last Updated | Notes |
|------|------------|--------------|-------|
| [#1426](https://github.com/netease-youdao/LobsterAI/issues/1426) | 74 | 2026-06-15 | Skill upload no feedback – no assignee |
| [#1427](https://github.com/netease-youdao/LobsterAI/issues/1427) | 74 | 2026-06-15 | Duplicate skills – no assignee |
| [#1428](https://github.com/netease-youdao/LobsterAI/pull/1428) | 74 | 2026-06-15 | Feature PR for notifications – needs review/merge |
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | 75 | 2026-06-15 | Dependency bump (electron 40→42) – open since April |

These items, especially the two skill bugs, should be prioritised to avoid accumulating technical debt and user dissatisfaction.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-16

## Today’s Overview
Activity on the Moltis repository was light over the past 24 hours, with no new issues, no closed pull requests, and no releases. Two pull requests were updated, both opened yesterday (2026-06-15) and still open. The project appears to be in a steady state of incremental development, with maintainers focusing on expanding external agent integration and session context management. No urgent bugs or regressions were reported.

## Releases
No new releases were published today. The most recent release remains the previous version (not specified in the data).

## Project Progress
No pull requests were merged or closed today. There are no completed features or fixes to report in this period.

## Community Hot Topics
Both updated PRs (#1124, #1125) have zero comments and zero reactions, so there is no clear community discussion to highlight. These PRs are nonetheless the only active contributions.

- **[PR #1125 – Support model and effort selection for external agents](https://github.com/moltis-org/moltis/pull/1125)**  
  Adds first-class model and effort selection for external-agent providers inside the `/model` system. This includes configuration arrays (`models = [...]`, `efforts = [...]`) and grouping under `external-agent/<kind>` in the model listing. The feature addresses the need for users to specify different external agent models and effort levels from a single interface.

- **[PR #1124 – Add context command support for chat turns](https://github.com/moltis-org/moltis/pull/1124)**  
  Introduces an optional `chat.context_command` that runs before each chat turn and appends its stdout to the prompt context. This allows deployments to inject dynamic runtime context without manual pasting. The implementation touches config schema, validation, and template handling.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project shows no stability concerns from the data.

## Feature Requests & Roadmap Signals
No user-submitted feature requests were opened today. However, the two open PRs themselves signal the maintainers’ priorities:
- **External agent flexibility** (PR #1125) – enabling per-provider model and effort selection, likely to be included in the next minor release.
- **Session context automation** (PR #1124) – improving developer experience by reducing manual context injection, a quality-of-life enhancement suitable for the next version.

Both PRs are authored by a core contributor (gptme-thomas) and appear to be nearing readiness (updated yesterday). They are strong candidates for the next release.

## User Feedback Summary
No user feedback, complaints, or satisfaction signals were recorded in the data (no issues, no comments on PRs). There is no observable user sentiment to report.

## Backlog Watch
No long-standing issues or PRs were identified. The repository has zero open issues and only two open PRs, both recently created. No items require maintainer attention beyond normal review of the current PRs.

---
*Generated from Moltis GitHub data (2026-06-16).*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-16

**Repository:** [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)  
*Note: Issues and PRs reference the QwenPaw repo (renamed from CoPaw). Links below point to `agentscope-ai/QwenPaw`.*

---

## 1. Today’s Overview

The project remains highly active with **50 issues** and **50 pull requests** updated in the last 24 hours. Of those issues, 32 are open/active and 18 were closed; PRs show a healthy merge rate with 32 merged/closed and 18 still open. No new releases were published. The community is engaged across a wide range of topics—from detailed bug reports on desktop crashes and file download failures to ambitious feature requests for context compression, token usage displays, and self-evolution mechanisms. The volume of open issues (especially those with multiple comments) indicates the project is in a rapid iteration phase with many users actively reporting regressions after the recent `v1.1.11.post2` release.

---

## 2. Releases

**None** – No new versions were published in the last 24 hours.

---

## 3. Project Progress

Key merged/closed PRs that advanced the codebase today:

- **#5146** – `fix(skill): Improve skill-slash-inject and display` (closed) — Resolves the issue where skill slash invocation displayed raw SKILL.md content in the console.  
- **#5067** – `feat(driver): introduce Agent OS Driver` (closed) — Unifies external capability invocation (MCP, A2A, ACP) under a common abstraction. A major architectural improvement.  
- **#5123** – `feat(skill): Update skill-market ... improve UI` (closed) — Adds the QwenPaw platform skill market endpoint and better category/preview UI.  
- **#4310** – `feat(console): show context usage` (closed) — Backend & frontend support for displaying real-time context window usage in the chat header.  
- **#5130** – `feat(chat): add per-turn token and context usage popover` (closed) — Extends the response card with token usage and context ring visualization.  
- **#5031** – `[Bug]: Skill slash invocation displayed as expanded SKILL.md` (closed) — Fixed by #5146.  
- **#5137** – `[Bug]: 向量模型自动记忆搜索配置丢失` (closed) — Vector model auto-search configuration persistence fixed.  
- **#5138** – `[Bug]: Windows客户端进程持续增加` (closed) — Windows client process leak addressed.

Additionally, several open PRs are under review, including #5040 (tolerate invalid cron jobs), #5041 (skip unreadable files in backup), #4622 (new DataPaw plugin), and #5097 (UI fix for Shield icon centering).

---

## 4. Community Hot Topics

The most active discussions (by comment count) reveal core user frustrations and feature desires:

| Issue # | Title | Comments | Summary |
|---------|-------|----------|---------|
| [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) | [channel] 小艺 | **22** | Huawei XiaoYi channel integration: agent appears on phone but returns “开小差” errors. User unsure if CoPaw or XiaoYi bug. No maintainer resolution yet. |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | [Bug]: v1.1.11.post2 附件下载还是有问题 | **6** | Attachment download for non‑text files (docx, pdf) returns 404. Repeated user frustration across versions. |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | [Bug]: MiniMax-M2.5 思考过程 XML 格式不兼容 | **5** | MiniMax model returns reasoning in XML format, breaking agent execution. Affects v1.1.7–1.1.8. |
| [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) | [Bug]: 插件依赖安装导致 cmd 窗口持续弹窗 | **5** | Plugin dependency pip install spawns visible cmd.exe windows, creating infinite retry loops on network failures. |
| [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | [Bug]: 上下文压缩保留缺少按条数保留 | **4** | Context compression can drop all content when character file token exceeds threshold, causing task loss. |
| [#4284](https://github.com/agentscope-ai/QwenPaw/issues/4284) | [Feature]: 对话窗口实时上下文用量显示 | **4** | Requesting real-time token/context usage in chat UI — now implemented by #4310 and #5130. |
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | [Feature]: Integrate Headroom for 60–95% token reduction | **4** | Proposal to add Headroom compression as an optional plugin. High interest from power users. |
| [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167) | [enhancement]: Feishu CardKit streaming optimization | **4** | Long replies refresh very slowly; user suggests optimization for better UX. |

The strong demand for **token/context visibility** (issues #4284, #3366, #5103, #4435, #4782, #4647) is now being addressed by merged PRs, which should improve user satisfaction.

---

## 5. Bugs & Stability

Bugs reported in the last 24 hours, ranked by severity:

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **Critical** | [#5209](https://github.com/agentscope-ai/QwenPaw/issues/5209) | **QwenPaw Desktop (Tauri) crash loop on macOS ARM64** – SIGSEGV every ~1 minute. No fix PR yet. | Open |
| **High** | [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) | **Plugin dependency installation causes infinite cmd window popups** – blocks users with unstable PyPI access. | Open |
| **High** | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | **Attachment download 404 for non‑text files** – persists across post2. | Open |
| **High** | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | **Context compression can erase all context** – causes complete task interruption. | Open |
| **High** | [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | **MiniMax XML reasoning breaks agent** – no fix reported. | Open |
| **Medium** | [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) | **Windows client process keeps growing** – memory leak. | Closed (fixed) |
| **Medium** | [#5207](https://github.com/agentscope-ai/QwenPaw/issues/5207) | **Path resolution inconsistency between file tools and shell** – @appshare vs @apps/share mismatch. | Open |
| **Medium** | [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184) | **Local model providers not showing in v1.1.11.post2** | Open |
| **Low** | [#5104](https://github.com/agentscope-ai/QwenPaw/issues/5104) | **copaw → qwenpaw rename legacy issues** – plugin install failures, path confusion. | Closed |

Several bugs have corresponding fix PRs:  
- #5146 fixes skill display (#5031).  
- #5040 and #5041 improve cron job and backup resilience.  
- #5138 (Windows process leak) was fixed.

However, the most severe desktop crash (#5209) and the attachment download issue (#5140) remain open.

---

## 6. Feature Requests & Roadmap Signals

Major feature requests with high community engagement:

- **Token/Context usage display** – Issues #4284, #3366, #5103, #4435, #4782, #4647. **Now merged** via PRs #4310 and #5130 – likely in the next release.
- **Headroom context compression** ([#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063)) – High interest. Could become an optional plugin.
- **Conversation queue** ([#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103)) – Allow user to queue prompts while agent is still processing. An open PR [#5158](https://github.com/agentscope-ai/QwenPaw/pull/5158) (Not Ready) hints this is under development.
- **Agent self‑evolution mechanism** ([#5205](https://github.com/agentscope-ai/QwenPaw/issues/5205)) – Learn from mistakes and auto-correct behavior. Early discussion.
- **Desktop UI layout improvement** ([#5211](https://github.com/agentscope-ai/QwenPaw/issues/5211)) – Reduce top nav space, improve screen utilization.
- **Feishu CardKit streaming optimization** ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)) – Addressing slow long‑reply refresh.
- **Observability integration** ([#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009)) – Request for Langfuse/OpenTelemetry; no concrete roadmap signal yet.
- **Models page overhaul** – PR [#5203](https://github.com/agentscope-ai/QwenPaw/pull/5203) proposes provider aggregation, unified card UI, and a new Aliyun Token Plan provider.

**Prediction for next version:** Token/context display, skill market improvements, and Agent OS Driver are likely to ship. Conversation queue and Feishu optimization may follow.

---

## 7. User Feedback Summary

Real user pain points and use cases from the last 24h:

- **Attachment handling remains broken** – multiple users (#5140, #5199) report that downloading non‑text files (docx, pdf) still returns 404 in `v1.1.11.post2`. User “renzhong424” is especially frustrated, having raised this repeatedly.
- **Desktop stability on macOS** – User “GroAries” reports a crash loop making the app unusable. No workaround given.
- **Plugin installation UX** – User “Sclifftop” complains about visible cmd windows during pip install, plus infinite retry loops when PyPI is unreachable.
- **Context compression data loss** – User “MCQSJ” describes a scenario where compression removes all context when a character file’s token count exceeds the retention threshold, causing task abortion.
- **MiniMax model users** – User “dcxj163” flags XML reasoning output that breaks agent execution; no fix in sight.
- **Enterprise WeChat access control** – User “shanghai‑Jerry” reports that enabling access control offers no approval UI, blocking legitimate use.
- **Rename legacy pain** – User “quchenchen” documents leftover `~/.copaw` directories causing plugin install failures and path chaos.
- **Positive signals:** The merged token/context display feature (#4284) was highly requested. Users also appreciate the skill market improvements.

Overall, satisfaction is tempered by recurring regressions, while the rapid pace of feature merges shows strong maintainer engagement.

---

## 8. Backlog Watch

Items needing maintainer attention:

| Issue/PR | Created | Last Updated | Comments | Reason for Watch |
|----------|---------|--------------|----------|------------------|
| [#1911](https://github.com/agentscope-ai/QwenPaw/issues/1911) | 2026-03-20 | 2026-06-15 | **22** | Huawei XiaoYi channel bug – oldest high‑comment issue with no fix. May need maintainer repro/input. |
| [#4625](https://github.com/agentscope-ai/QwenPaw/issues/4625) | 2026-05-22 | 2026-06-16 | **5** | MiniMax XML incompatibility – affects multiple versions; no linked PR. |
| [#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025) | 2026-06-08 | 2026-06-15 | **4** | `submit_to_agent` file path bug – reported 8 days ago, no maintainer response. |
| [#5089](https://github.com/agentscope-ai/QwenPaw/issues/5089) | 2026-06-10 | 2026-06-15 | **3** | Session return failure after new session – unclear repro, no maintainer comment. |
| [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184) | 2026-06-14 | 2026-06-15 | **3** | Local model providers invisible in post2 – affects new feature introduced in v1.1.11. |
| [#5207](https://github.com/agentscope-ai/QwenPaw/issues/5207) | 2026-06-15 | 2026-06-16 | **2** | Path resolution inconsistency (file tools vs shell) – could cause subtle work failures. |
| PR [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) | 2026-05-22 | 2026-06-16 | 0 | DataPaw plugin PR – under review for 25 days; may need final approval. |
| PR [#5040](https://github.com/agentscope-ai/QwenPaw/pull/5040) | 2026-06-09 | 2026-06-16 | 0 | Cron job resilience fix – under review for 7 days. Labeled `first-time-contributor`; could benefit from maintainer guidance. |

These items represent either long‑standing user pain points or contributions that risk stagnation. Early attention to #1911 and #4625 would reduce community frustration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-16

## 1. Today's Overview

The project saw very high activity over the last 24 hours, with **50 issues** and **50 pull requests** updated. Of these, **4 issues were closed** and **1 PR was merged**, indicating steady forward momentum despite a large backlog of open work. The majority of updates were concentrated on bugs, security-related features, and infrastructure improvements (CI, multi-database backends). No new releases were published today. The development pace suggests the team is preparing for the upcoming `v0.8.1` and `v0.9.0` milestones, with several RFCs and trackers actively discussed.

## 2. Releases

No new releases were published today.

## 3. Project Progress

**Merged/Closed Pull Requests (1):**
- [#7669](https://github.com/zeroclaw-labs/zeroclaw/pull/7669) – **ci(workflows): run macOS and Windows build legs as cargo check** – Reduces CI time by linking only on Linux while still verifying cross-platform compilation via `cargo check`. This improvement directly addresses build pipeline bottlenecks.

**Closed Issues (4):**
- [#1458](https://github.com/zeroclaw-labs/zeroclaw/issues/1458) – **Add support for local CA certificates** – Closed; solution presumably merged in a prior PR.
- [#6683](https://github.com/zeroclaw-labs/zeroclaw/issues/6683) – **skill_manage `patch` ignores cooldown** – Closed; rate limiting for skill patches now enforced.
- [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) – **`ask_user` fails instantly with "Channel closed" in Web dashboard** – Closed with fix (PR likely merged earlier).
- [#7005](https://github.com/zeroclaw-labs/zeroclaw/issues/7005) – **Quickstart CLI strings still bare** – Closed; i18n string cleanup completed.

These closures reflect tangible improvements in configuration, skill management, and user-facing polish.

## 4. Community Hot Topics

The most active discussions (by comment count and reactions) reveal key areas of interest:

- **#2767 – Multi-Agent Routing** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/2767)) – 9 👍, 6 comments. This long-standing feature request for running isolated agents with separate workspace/channel bindings received strong community backing. It is labeled `priority:p2` and `status:accepted`, indicating it is on the roadmap.

- **#1458 – Local CA certificates** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/1458)) – 8 comments, now closed. Users want to specify custom root CAs for self-signed inference endpoints.

- **#6067 – Configurable reply-intent precheck** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/6067)) – 5 comments. Desire to use a lightweight model for intent classification to avoid blocking the main agent turn.

- **#551 – Allow insecure HTTPS to OpenAI-compatible endpoints** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/551)) – 4 comments. Complements the CA certificate request; users need SSL cert bypass for self-signed endpoints. This issue is blocked.

- **#6970 – v0.8.1 Integration tracker** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)) – 3 comments. Operational tracker for the next release’s integration queue.

- **#7218 – A2A agent discovery RFC** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)) – 3 comments. Defines how multi‑agent installs expose `.well‑known/agent‑card.json` for inter‑agent discovery.

- **#7673 – RFC: Native context compression decorator** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7673)) – 3 comments (today). Proposes a `CompressionDecorator` model provider wrapper to reduce token usage. This is a new RFC reflecting interest in cost reduction.

**Underlying needs:** Users are demanding greater flexibility in agent orchestration (multi-agent, A2A), custom infrastructure integration (CA, SSL, local providers), and performance tuning (lighter intent checks, compression).

## 5. Bugs & Stability

Several new or updated bugs of high severity were reported today. The most critical are:

- **#7753 – Session persistence ordering race** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7753)) – `risk: high`. Messages for the same sender are processed concurrently, causing race conditions in session-store mutations. No fix PR yet.

- **#7733 – MCP scoping is a silent no‑op** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7733)) – `risk: high`. Parsed `mcp_bundles` configuration is never enforced at runtime, breaking per‑agent isolation of MCP tools. No fix PR yet.

- **#7741 – Response cache not skipping multimodal markers** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7741)) – `risk: high`. Cache lookup fails to exclude prompts containing `[IMAGE:...]` markers, leading to stale responses. No fix PR yet.

- **#7742 – System prompt not refreshed after tool dispatcher swap** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7742)) – `risk: high`. Mid‑session tool dispatcher changes leave stale tool instructions in agent history. No fix PR yet.

- **#7542** (closed) – `ask_user` failure in Web dashboard – fixed.

- **#7038 – `zeroclaw check` 11/11 websocket 401** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7038)) – `risk: medium`. WebSocket health check fails even when manual bearer token works. Stalled with `needs-author-action`.

- **#7739 – Email OAuth retry missing** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7739)) – `risk: medium`. No retry/backoff on transient OAuth refresh failures, unlike other providers.

- **#7738 – Email UID fallback uses random UUID** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7738)) – `risk: medium`. Missing `Message-ID` generates non‑deterministic identifiers, causing duplicate processing on reconnect.

- **#7749 – Per‑agent `prompt_injection_mode`** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7749)) – `risk: medium` (feature, but also a bug when mixing modes). Currently global only, which prevents running `full` and `compact` agents in one install.

**Pull Requests addressing bugs:**
- #7424 – Fix `allowed_private_hosts = ["*"]` not covering DNS‑resolved private hosts (risk: high)
- #7640 – Skip global credential fallback for OAuth target providers during delegation (risk: high)
- #7485 – Pass config context when validating custom model providers in doctor (risk: high)
- #7532 – Align serde defaults with struct Default to prevent config save round-trip loss (risk: medium)
- #7727 – Surface config warnings in `zeroclaw doctor` (risk: low)
- #7732 – Authenticate websocket handshake probe in self-test (risk: high for false negatives)

## 6. Feature Requests & Roadmap Signals

New and updated enhancement requests indicate the following likely directions:

**Short‑term (v0.8.1):**
- #6970 (tracker) – Integration/channel/provider/tool queue for v0.8.1.
- #6067 – Configurable reply‑intent precheck (light model + timeout).
- #6055 – Slack thread history hydration.
- #7468 – Allow alias renaming in TUI.
- #7467 – More flexible edit string navigation.

**Medium‑term (v0.9.0):**
- #7432 (tracker) – Auth, security, gateway, and breaking changes.
- #7743 – Explicit target‑profile authority for delegate handoffs (deny‑by‑default).
- #7218 – A2A agent discovery RFC (foundation for multi‑agent interoperable installs).
- #7675 – Hardened CI pipeline with supply‑chain scanning, provenance, SBOM.
- #7674 – WebAssembly‑first, eliminate Node.js from build and runtime.

**Long‑term / RFC (needs maintainer review):**
- #7673 – Native context compression decorator (reduce token usage).
- #2767 – Multi‑agent routing (high community interest, accepted but not yet started).

**Prediction for next release:** The v0.8.1 tracker (#6970) plus the many pending bug‑fix PRs suggest a bug‑fix and minor feature release within a few weeks. v0.9.0 with breaking changes (auth, security, possibly multi‑agent routing) appears targeted for later this summer.

## 7. User Feedback Summary

Today’s data reveals several recurring pain points and unmet needs:

- **Certificate and SSL issues** – Users with self‑signed or private CAs on inference endpoints are blocked (#551, #1458). The closure of #1458 is positive, but #551 remains blocked.
- **Session and state management** – Concurrent session processing causes ordering races (#7753); email channel lacks deterministic IDs (#7738); MCP tool scoping is broken (#7733).
- **Configuration ergonomics** – Users want alias renaming (#7468), non‑destructive string editing (#7467), and per‑agent injection modes (#7749).
- **Delegation and multi‑agent** – Strong demand for multi‑agent routing (#2767, #7743) and better control over delegation permissions.
- **Performance** – Requests for lighter intent classification (#6067) and token compression (#7673) indicate users are hitting cost or latency limits.
- **CI and testing reliability** – Closed issue #7542 and ongoing fix #7732 show WebSocket auth tests were unreliable. Users also reported platform‑specific test gaps (#7486, #7669).

Overall, the community appears engaged and vocal about security, flexibility, and performance improvements. The project’s rapid issue/PR turnover suggests the team is responsive, though some important bugs (e.g., #7733) lack visible fix PRs.

## 8. Backlog Watch

The following high‑impact issues and PRs require urgent maintainer attention or have stalled:

- **#551 – Allow insecure HTTPS to OpenAI‑compatible endpoints** – `priority:p2`, `status:blocked`. Long‑standing, affects users with self‑signed certs. Maintainers should unblock or commit to an alternative.
- **#7038 – websocket 401 despite valid auth** – `status:blocked`, `needs-author-action`. Lack of repro blocks investigation.
- **#7098 – Mattermost WebSocket listener mode (PR)** – `needs-author-action`, `stale-candidate`. Large feature PR (size L) stalled for two weeks.
- **#7215 – fix(quickstart): surface port field for webhook** – `needs-author-action`. Quickstart FTUE fix waiting on author.
- **#7532 – fix config serde defaults** – `needs-author-action`. Could cause data loss, but author not responding.
- **#7638 – fix(cli): route status strings through i18n** – `needs-author-action`. Minor but blocks i18n completeness.
- **#6074 – audit: track 153 commits lost in bulk revert** – `priority:p2`. Recovery of lost code still unresolved; no action since April.
- **#7673, #7675, #7674** – New RFCs (`needs-maintainer-review`). These require maintainer feedback to shape the next architecture decisions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*