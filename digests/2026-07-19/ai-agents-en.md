# OpenClaw Ecosystem Digest 2026-07-19

> Issues: 390 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-19 01:58 UTC

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

# OpenClaw Project Digest – 2026-07-19

## 1. Today's Overview
OpenClaw shows extremely high development activity, with **390 issues** and **500 pull requests** updated in the last 24 hours. **249 open issues** and **263 open PRs** indicate a large, engaged community and heavy ongoing work. A **new beta release (v2026.7.2-beta.3)** was published, bringing remote coding sessions, native automation improvements, and multi-channel durability work. The project’s maintainers are processing a massive queue of contributions, with 141 issues closed and 237 PRs merged/closed yesterday. While stability remains a focus—many P0/P1 bugs are under active investigation—the rate of feature work (especially around session dashboards, skill previews, and memory tagging) suggests strong forward momentum.

## 2. Releases
### v2026.7.2-beta.3
- **Highlights:**
  - **Remote coding sessions:** Users can now run Control UI sessions on cloud workers, open Codex and Claude catalog sessions in terminals on their owning hosts, and resume OpenCode/Pi sessions directly via terminal.
  - **Native automation & nodes:** The release hints at deeper native automation support (full notes truncated in dataset).
- **Migration notes:** None explicitly stated, but a migration issue (#109867) in the beta.2→beta.3 upgrade path is being addressed (see Bugs section).
- **Status:** Beta. Expected GA after resolving blocker bugs and completing the durable ingress drain rollout.

## 3. Project Progress
Yesterday’s 237 merged/closed PRs advanced multiple areas:
- **Channel fixes:** WhatsApp LID ack (#110053), Telegram client lease leak (#111118), Feishu text preservation (#102399), QQBot abort handling (#109896), SMS phone number normalization (#111111), Google Chat streaming migration (#106018), Discord memory growth (#110954), LINE media polling (#111057), Nostr SecretRef connection (#98337).
- **Extensions & providers:** OpenRouter music generation cleanup (#111056), Amazon Bedrock credentials handling (#109680), OpenRouter dynamic model discovery (#10687, PR #111056), OC-Path config file size caps (#110714), QA Lab runtime parity bounding (#102787).
- **CLI & core:** JSON repair output fix (#111117), dynamic import simplification (#111071, #111074), heartbeat explicit targets (#103711), session dashboard domain (PR #110960 – large feature), skill preview proposals (#103872), grouped Claw agent updates (#102959).
- **Security:** Bounded file reads for approval scripts (#110712), cron quarantine sidecar (#101477), openshell sandbox (#110716), reef legacy state (#110713), config-set-input (#110593).
- **Documentation:** Durable core residual-gap RFC docs (#107375) – part of a 6-PR series.

## 4. Community Hot Topics
The most active issues and PRs reflect strong user demand for multi-platform support, security, and reliability:

- **Issue #75** (113 comments, 81 👍) – **Linux/Windows Clawdbot Apps**  
  Long-standing request for desktop app coverage beyond macOS/iOS. *Underlying need:* parity for non-Apple ecosystems and CI/CD environments. Still open after 6 months.

- **Issue #7707** (17 comments) – **Memory Trust Tagging by Source**  
  Proposal to prevent memory poisoning by tagging entries by origin (user vs. web vs. third-party). *Underlying need:* security against prompt injection via untrusted content.

- **Issue #91009** (14 comments, P1) – **Codex PreToolUse hook spawns CPU-bound processes**  
  Critical bug causing gateway stalls. Active discussion with maintainer involvement. *Need:* stable integration with Codex runtime.

- **Issue #10659** (13 comments) – **Masked Secrets system**  
  Prevents agents from reading raw API keys. *Need:* protection against accidental leaks and injection attacks on credentials.

- **Issue #79077** (11 comments) – **Telegram bot-to-bot / guest-bot modes**  
  User request to support Telegram’s May 2026 API updates. *Need:* compatibility with evolving platform features.

- **Issue #109867** (6 comments, 7 👍, P0) – **Beta.2 migration index/column ordering bug**  
  Blocks gateway startup on upgrade. High urgency, already has fix attempts.

PRs with high engagement (though comment counts undefined):  
- #111117 (fix repair JSON parseable) – practical CLI improvement  
- #110960 (session dashboard domain) – large feature with broad impact  
- #103872 (skill preview proposals) – enhances agent transparency

## 5. Bugs & Stability
**P0 (release-blocking) bugs:**
- **#109867** – Beta.2 state migration creates index before column → gateway startup failure. *Fix PR being developed.*
- **#108435** – Gateway fails to start with error after update to 2026.7.1. *Regression, user reports with systemd and manual launch.*
- **#101763** (closed) – Hosted Molty model selector sends invalid model id. *Fixed but highlights configuration fragility.*
- **#109490** (P1) – Codex app-server turn interrupted after client-delegated message tool result. *Promised work never executes.*

**P1 bugs (reported/updated in last 24h):**
- **#91009** – CPU-bound hooks process (re-staled, still open).
- **#108238** – Session context counts `cacheRead` as totalTokens, causing false compaction triggers. *Reproduced on main.*
- **#96242** – Duplicate Telegram messages via multiple paths.
- **#78562** – Repeated auto-compaction loops after successful compaction.
- **#89147** – Native hook relay starves after long thinking gaps.
- **#99910** – Memory dreaming run pegs event loop for ~10 minutes.
- **#99071** – Repeated Codex Apps plugin discovery causing disk I/O.
- **#86684** – Subagent wake compacts parent at low context usage (regression).
- **#109672** – AWS Guardrail triggers silent “Something went wrong” error.
- **#102399** (PR open) – Feishu text loss with media replies.

**Key patterns:** Context window/budget accounting bugs (multiple reports), Telegram delivery races, Codex integration reliability, memory/database migration issues. Several have linked fix PRs (e.g., #108435, #109867, #96242).

## 6. Feature Requests & Roadmap Signals
High-impact requests likely to land soon:

- **Memory Trust Tagging (#7707)** – Security-critical, aligns with ongoing secret masking (#10659). Could be part of an upcoming security release.
- **Automatic session titling (#99583)** – Low effort, already has slug generator code. Likely to ship in next minor version for UX polish.
- **Model fallback on context overflow (#9986)** – Aligns with recent context accounting fixes; logical next step.
- **WhatsApp sticker support (#7476)** – Small plugin addition, high user demand for a widely-used channel.
- **Telegram quote/reply as durable contract (#88032)** – Reflects broader effort to make channel interactions reliable and testable.
- **Skill Permission Manifest (#12219)** – Security gate for third-party skills; could be coupled with skill preview feature already in progress (#103872).
- **Full dynamic model discovery (#10687)** – Essential for fast-moving providers like OpenRouter; overlaps with PR #111056 (OpenRouter fixes).

## 7. User Feedback Summary
**Pain points (prevalent in issues):**
- **Telegram reliability:** Duplicate messages, failed group replies, HTML parse mode truncation (#96242, #87299, #49104, #88032). Users frustrated by inconsistent behavior.
- **Memory/context management:** “Spurious compaction” and “false context overflow” complaints (#108238, #78562, #86684) – especially vocal among users with long-running sessions.
- **Platform gaps:** Linux/Windows desktop apps (#75) – sentiment that OpenClaw is “macOS first” despite CLI availability.
- **Security concerns:** Users actively request secrets masking (#10659), memory poisoning prevention (#7707), filesystem sandboxing (#7722). Trust in agent actions is a recurring theme.
- **Onboarding friction:** Migration errors (#109867), model discovery not working (#10687), and “Something went wrong” with AWS Guardrail (#109672) reduce confidence.

**Satisfaction signals:**
- High engagement on skill preview proposals (#103872) and session dashboard (#110960) – users eager for better agent oversight.
- The new remote coding sessions feature (v2026.7.2-beta.3) addresses a long-standing request for cloud-worker support.
- Many bug fix PRs are being submitted by community contributors, indicating a healthy open-source ecosystem.

## 8. Backlog Watch
Long-standing important issues needing maintainer attention:

- **Issue #75** – Linux/Windows Clawdbot Apps (6 months open, 113 comments, P2). No progress despite high demand. Could be a candidate for community contribution with maintainer guidance.
- **Issue #7707** – Memory Trust Tagging (5 months, P2, diamond lobster rating). Still needs product decision and security review. Persistent request.
- **Issue #7722** – Filesystem Sandboxing Config (5 months, P2). Comments note that initial implementation failed; no maintainer review yet.
- **Issue #12219** – Skill Permission Manifest (5 months, P2). Important for security, but no fix PR or product decision.
- **Issue #51572** – Fire session-memory hook on session reset (4 months, P2). Could prevent data loss on idle/prune.
- **Issue #9986** – Model fallback on context overflow (5 months, P2). Linked PR open (#111056? unclear), but stalled.
- **PR #110960** – Session dashboard domain (XL, maintainer, P1). Huge change; needs proof but has broad implications. Maintainers should prioritize review.

**Summary:** The backlog contains several security and usability enhancements that have lingered for months. The high ratio of open issues (249 of 390) suggests triage bandwidth is strained. Encouragingly, many recent P0/P1 bugs are getting quick attention.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI agent open-source landscape is characterized by intense, daily feature iteration across multiple independent projects, each vying to become the de facto reference for agentic assistants. The ecosystem is bifurcated: a few large projects (OpenClaw, ZeroClaw, IronClaw) drive massive pull-request throughput with hundreds of changes per day, while smaller or more specialized projects (Hermes Agent, NanoBot, PicoClaw, NanoClaw, Moltis) focus on reliability, platform parity, and security hardening. Common across all projects is a strong push toward multi-channel messaging (Telegram, WhatsApp, Slack, Matrix), memory/context management improvements, and increasing attention to credential safety and sandboxing. The community is highly engaged, with many contributor-submitted fixes and feature PRs, though maintainer bandwidth remains a bottleneck for older issues.

## 2. Activity Comparison

| Project         | Issues Updated (24h) | PRs Updated (24h) | New Release? | Health Score* |
|-----------------|----------------------|-------------------|--------------|---------------|
| OpenClaw        | 390 (249 open)       | 500 (263 open)    | Yes (beta)   | **A** (very high activity, but large backlog) |
| ZeroClaw        | 50                   | 50                | No           | **A** (high, balanced) |
| IronClaw        | 5                    | 50                | No           | **A** (high PR throughput, low issues) |
| NanoBot         | 7 (3 open)           | 30                | No           | **B+** (high fix velocity, small backlog) |
| NanoClaw        | 18 (2 open)          | 26                | No           | **B+** (fast closes, critical fixes) |
| Hermes Agent    | 50 (18 open)         | 50                | No           | **B+** (many P0/P1 closed, active) |
| PicoClaw        | 4                    | 12                | No           | **B** (steady, but two blocking bugs) |
| CoPaw           | 11                   | 7                 | No           | **B** (active community, critical regressions) |
| LobsterAI       | 6                    | 3                 | Yes (patch)   | **B-** (moderate, stale backlog) |
| Moltis          | 0                    | 3 (2 merged)      | No           | **C+** (low activity, but finished work) |
| NullClaw        | 1                    | 0                 | No           | **C** (near-dormant, one old bug) |
| TinyClaw        | 0                    | 0                 | No           | **D** (no activity) |
| ZeptoClaw       | 0                    | 0                 | No           | **D** (no activity) |

*Health Score is a qualitative assessment based on activity volume, responsiveness to bugs, and backlog management (not a formal metric).

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale:** OpenClaw dominates in raw activity (390 issues, 500 PRs, 237 PRs merged/closed in one day), far exceeding any other project.
- **Feature velocity:** The beta release v2026.7.2-beta.3 introduces remote coding sessions, native automation, and multi-channel durability – capabilities not yet seen in other projects.
- **Community size:** The 249 open issues and 263 open PRs indicate a massive, engaged contributor base. Only ZeroClaw and Hermes Agent approach similar counts, but with less than half the volume.
- **Security focus:** Active work on bounded file reads, cron quarantine, sandboxing, and masked secrets shows advanced security posture.

**Technical approach differences:**
- OpenClaw uses a "durable core" architecture with RFC-driven evolution (e.g., residual-gap RFC docs). It prioritizes a single reference implementation with extensive plugin/channel support.
- In contrast, ZeroClaw targets WASM plugins and hardware (ESP32, Pico); IronClaw is in the midst of a "Reborn" architectural simplification; NanoBot emphasizes Git-backed memory and subagent aggregation.

**Community size comparison:**
- OpenClaw's 390 issues/500 PRs per day dwarfs even the next busiest projects (ZeroClaw and Hermes Agent at ~50 each). However, this comes with a higher backlog ratio (64% open issues vs. 36% closed), indicating triage strain.
- ZeroClaw and IronClaw maintain a healthier balance (e.g., IronClaw had 5 issues and 50 PRs updated, with 30 PRs merged/closed – a 60% close rate).

## 4. Shared Technical Focus Areas

Several requirements emerge across multiple projects, indicating ecosystem-wide priorities:

- **Multi-channel reliability** – All major projects are fixing Telegram, WhatsApp, Slack, Discord, Feishu, Matrix, etc.  
  *Projects:* OpenClaw, ZeroClaw, Hermes Agent, PicoClaw, NanoClaw, CoPaw, Moltis.  
  *Specific needs:* Duplicate message handling, typing presence, voice transcription echoes, thread backfill, OAuth refresh concurrency.

- **Memory & context management** – Multiple projects address context overflow, compaction bugs, and memory trust tagging.  
  *Projects:* OpenClaw (#108238, #78562, #86684), NanoBot (#4925, #4627), Hermes Agent (#67240), ZeroClaw (#8505, #6055).  
  *Specific needs:* False compaction triggers, token budget accounting, memory contamination from internal comments.

- **Credential & secrets security** – Plaintext token storage, masked secrets, and supply-chain signing are active topics.  
  *Projects:* OpenClaw (#10659, #110712), IronClaw (#6247), ZeroClaw (#9127, #8857, #9142), NanoClaw (#3065).  
  *Specific needs:* Loopback webhook authentication, bearer token leakage, OAuth store canonicalization.

- **Platform parity (Linux/Windows/mobile)** – Windows and Android/Termux remain underserved.  
  *Projects:* OpenClaw (#75), Hermes Agent (#38216, #51448), NullClaw (#868), ZeroClaw (#7911), CoPaw (#6239).  
  *Specific needs:* Desktop apps for non-macOS, Windows installer crashes, ARM builds, subprocess encoding issues.

- **Sandboxing & file system security** – Bounded file reads, forbidden path patterns, and approval prompts.  
  *Projects:* OpenClaw (#110712, #110716), ZeroClaw (#8424), CoPaw (#6250), NanoClaw (#2496).  
  *Specific needs:* Workspace-relative ignore files, sandbox fallback config, read-only database errors.

## 5. Differentiation Analysis

| Aspect | OpenClaw | ZeroClaw | IronClaw | NanoClaw | Hermes Agent | CoPaw | LobsterAI |
|--------|-----------|-----------|-----------|-----------|---------------|-------|-----------|
| **Primary language** | Go (inferred from ecosystem) | Rust (inferred) | Rust (inferred) | TypeScript/Node | Rust/TypeScript? | Python | TypeScript/Node |
| **Target user** | Power users, multi-platform (macOS-first) | Developers, hardware enthusiasts (ESP32) | Enterprise/self-hosted (Reborn simplification) | Small teams, quick setup | Developers & Windows users | Chinese-language community | Studio/enterprise (Chinese) |
| **Architecture** | Durable core, RFC-driven, heavy plugin system | WASM plugins, hardware protocol crates | Monorepo with Reborn (simplified runtime) | Lightweight, Node.js, Slack-first | Gateway + agent separation, MCP tools | Qwen-based, memory-heavy | OpenClaw engine wrapper |
| **Key differentiator** | Highest feature velocity, largest community | Hardware integration, supply-chain signing | Architecture simplification for enterprise | Slack Socket Mode, credential proxy fixes | Windows focus, voice/Telegram reliability | Chinese ecosystem (Qwen, Feishu, DingTalk) | Studio UI, cowork features |
| **Backlog management** | Strained (64% open) | Balanced (~50% open) | Excellent (~10% open) | Good (fast closes) | Moderate (P0/P1 closed quickly) | Moderate | Poor (stale issues months old) |

## 6. Community Momentum & Maturity

**Tier 1 – Rapid iteration (daily heavy PR flow):**  
OpenClaw, ZeroClaw, IronClaw. These projects are actively reshaping their architectures and adding major features. Community engagement is high but maintainer bandwidth is stretched.

**Tier 2 – Active, stable improvement:**  
NanoBot, NanoClaw, Hermes Agent, PicoClaw. These projects fix bugs and merge small features daily, with strong contributor participation. They are more stable and have fewer regressions.

**Tier 3 – Moderate maintenance:**  
CoPaw, LobsterAI, Moltis. Activity is lower, with periodic releases and slower response to bugs. CoPaw has a spike due to regressions but overall cadence is moderate.

**Tier 4 – Dormant/incubating:**  
NullClaw, TinyClaw, ZeptoClaw. No meaningful development in the last 24 hours; may be abandoned or in hibernation.

**Overall ecosystem trend:** The market is consolidating around a few dominant projects (OpenClaw, ZeroClaw, IronClaw) while smaller projects either specialize (NanoBot on Git-backed memory, CoPaw on Chinese enterprise) or fade. The rapid fix cycles in Tier 2 suggest they are stabilizing toward "boring" reliability, whereas Tier 1 is still racing to deliver new capabilities.

## 7. Trend Signals

Extracted from community feedback and issue discussions across projects:

- **"Agents must know their own capabilities"** – Users expect agents to autonomously schedule tasks (cron), understand their channel scope, and expose self-diagnostics. This is a recurring theme in ZeroClaw (#5862) and OpenClaw (#103711, heartbeat explicit targets).

- **Memory poisoning is the next security frontier** – Multiple projects (OpenClaw #7707, ZeroClaw #9127) are designing memory trust tagging and provenance-aware consolidation. This reflects growing awareness of prompt injection risks.

- **Context overflow handling is a UX crisis** – False compaction, hallucination due to budget mismanagement, and token overruns are top complaints across OpenClaw, NanoBot, and ZeroClaw. Tool-call pairing and fallback chains are emerging solutions.

- **Multi-agent orchestration is nascent** – Projects like OpenClaw (remote coding sessions, skill preview proposals), PicoClaw (Agent Collaboration Bus), and IronClaw (single-gateway multiple agents) are exploring inter-agent communication patterns. This will likely be a major 2027 trend.

- **Hardware integration is real** – ZeroClaw's work on ESP32, Pico, and Nucleo indicates that agent local inference and IoT control are becoming practical. Other projects have not yet followed, creating a differentiation opportunity.

- **Security hardening moves upstream** – Rather than relying on users to configure sandboxes, projects are baking in secret masking, loopback authentication, and supply-chain signing at the architecture level (IronClaw, OpenClaw, ZeroClaw). Expect open-source agents to become more "safe by default."

- **Platform gaps harm adoption** – Lack of Windows desktop apps (OpenClaw #75) and broken Android/Termux builds (NullClaw, ZeroClaw) are repeatedly mentioned. For an ecosystem targeting personal AI assistants, inability to run on common consumer devices is a significant barrier.

**For technical decision-makers:** If choosing a project to build upon, OpenClaw offers the largest ecosystem and fastest innovation but requires careful triage to avoid regression risks. ZeroClaw and IronClaw provide more stable, security-oriented foundations. For lightweight deployments, NanoBot or NanoClaw offer quick setup with good maintenance. The Chinese-language projects (CoPaw, LobsterAI) serve specific regional needs. Overall, the ecosystem is maturing rapidly, and interoperability between projects (e.g., common MCP or ACP protocols) is likely to emerge as a unifying force.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-19

## Today’s Overview
The project shows strong activity with **7 issues updated** (3 still open) and **30 pull requests updated** (16 merged/closed) in the last 24 hours. No new releases were tagged. The community is actively fixing regressions and polishing existing features, with particular attention to reliability around session persistence, Git-backed memory, and subprocess handling on Windows. A wave of bug-fix PRs from multiple contributors indicates healthy collaborative maintenance.

## Releases
*None* – No new versions were released today.

## Project Progress (Merged/Closed PRs)
16 PRs were merged or closed today. Notable advances include:

- **Memory & Agent Loop** – [#4925](https://github.com/HKUDS/nanobot/pull/4925) (fix) guides the agent through recovery when tool results exceed context limits; [#4627](https://github.com/HKUDS/nanobot/pull/4627) (fix) preserves delivery context during consolidation; [#4626](https://github.com/HKUDS/nanobot/pull/4626) adds opt-in eager memory consolidation; [#4621](https://github.com/HKUDS/nanobot/pull/4621) gates archive facts with provenance context.
- **Subagent Improvements** – [#4624](https://github.com/HKUDS/nanobot/pull/4624) adds an aggregated result mode for subagents, replacing the realtime-only behavior.
- **Deployment & Security** – [#4937](https://github.com/HKUDS/nanobot/pull/4937) adds one-click deploy to Render; [#4886](https://github.com/HKUDS/nanobot/pull/4886) (closed) fixed Docker Compose security hardening (AppArmor/seccomp); [#4786](https://github.com/HKUDS/nanobot/pull/4786) (closed) resolved unbounded session cache growth.

## Community Hot Topics
The most discussed issues today, by comment count:

- **[#2343 – Context length error in `run_agent_loop`](https://github.com/HKUDS/nanobot/issues/2343)** (15 comments, now closed) – User reported that the agent does not check `contextWindowTokens` before calling the model, causing token overruns. Discussion centered on how to trim chat history. The fix was merged via [#4925](https://github.com/HKUDS/nanobot/pull/4925) (recovery logic) and [#4956](https://github.com/HKUDS/nanobot/pull/4956) (cap messages at persistence boundary).
- **[#4867 – Ollama caching / extra 60s per turn](https://github.com/HKUDS/nanobot/issues/4867)** (5 comments, now closed) – User reported that Nanobot adds ~60 seconds to every turn when using Ollama locally, due to prompt prefix variations. A follow-up enhancement request for preserving exact prefixes to enable caching was addressed and closed.

## Bugs & Stability
Three open bugs reported today, all with corresponding fix PRs already submitted:

| Issue | Severity | Summary | Fix PR |
|-------|----------|---------|--------|
| [#4980](https://github.com/HKUDS/nanobot/issues/4980) | **High** – GitStore fails to initialise/commit when workspace ≠ process CWD. Relative paths sent to Dulwich cause silent failures. | [#4979](https://github.com/HKUDS/nanobot/pull/4979) resolves paths relative to workspace. |
| [#4975](https://github.com/HKUDS/nanobot/issues/4975) | **High** – CLI subprocess output on Windows non-UTF-8 locales (e.g. CP936) raises `UnicodeDecodeError` because no explicit encoding is set. | [#4976](https://github.com/HKUDS/nanobot/pull/4976) forces UTF-8 decoding. |
| [#4940](https://github.com/HKUDS/nanobot/issues/4940) | **Medium** – Sessions created with legacy filename format lose `workspace_scope` after restart because `read_session_metadata()` has no fallback. | [#4977](https://github.com/HKUDS/nanobot/pull/4977) adds legacy path fallback. |

Additionally, three lower-severity bug-fix PRs were opened today for null/string coercion in triggers and cron stores (coerce null `runAtMs`, `durationMs`, etc.): [#4986](https://github.com/HKUDS/nanobot/pull/4986), [#4985](https://github.com/HKUDS/nanobot/pull/4985), [#4983](https://github.com/HKUDS/nanobot/pull/4983). Two other PRs fix infinite-loop hangs when message-split limits are ≤0 in Feishu and Telegram channels ([#4982](https://github.com/HKUDS/nanobot/pull/4982), [#4981](https://github.com/HKUDS/nanobot/pull/4981)).

## Feature Requests & Roadmap Signals
- **Session-local triggers** – [#4942](https://github.com/HKUDS/nanobot/pull/4942) (open) lets agents create, list, and manage triggers scoped to a single conversation. Likely to be merged soon.
- **RTK command rewriter** – [#4854](https://github.com/HKUDS/nanobot/pull/4854) (open) adds an opt-in exec rewriter for remote task execution, indicating ongoing work on sandboxed execution.
- **WebUI polish** – [#4963](https://github.com/HKUDS/nanobot/pull/4963) (open) replaces raw tool logs with a unified activity language, improving user-facing output. Expect it in the next minor release.

## User Feedback Summary
- **Pain points**: Users face token overrun errors when using the agent with models that have tight context limits (32768 tokens). The workaround is manual, but the fix in [#4925](https://github.com/HKUDS/nanobot/pull/4925) should improve resilience. Ollama users experienced unacceptable latency (~60s per turn) due to missing prompt prefix caching; this is now resolved.
- **Windows users** reported broken CLI subprocess output causing crashes on non-English locales – a fix is underway.
- **Workspace_scope loss** after restart (legacy sessions) frustrated a user relying on custom project paths; the fallback patch in [#4977](https://github.com/HKUDS/nanobot/pull/4977) restores that data.
- Overall, the community is satisfied with the responsiveness of maintainers – all open bugs have matching fix PRs submitted within hours of reporting.

## Backlog Watch
No long-unanswered issues or PRs were identified in today’s snapshot. The oldest open issue updated recently is [#4940](https://github.com/HKUDS/nanobot/issues/4940) (3 days old) which already has a fix PR. Maintainers should continue to monitor older items outside the 24h window, such as open feature PRs [#4854](https://github.com/HKUDS/nanobot/pull/4854) and [#4942](https://github.com/HKUDS/nanobot/pull/4942) which have been open for 11 and 4 days respectively.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-19

## 📋 Today's Overview

Activity remained high with 50 issues and 50 pull requests updated in the last 24 hours. Of the 18 open issues, several are P0/P1 bugs that received fixes or were closed today. No new release was published, but the project shows continuous merge velocity (6 PRs merged/closed) and a strong focus on Windows platform stability, MCP tool lifecycle, and Telegram gateway reliability. The community is actively reporting regressions after recent updates, indicating a period of rapid iteration.

## 🚀 Releases

**None** — No new releases recorded in the last 24 hours.

---

## ✅ Project Progress — Merged/Closed PRs Today

- **#67248** — `fix(gateway): dedupe pending voice transcript echoes`  
  Cherry-picks three contributor commits to fix #61455 (Telegram voice interrupt producing duplicate transcriptions). Merged.  
  [PR #67248](https://github.com/NousResearch/hermes-agent/pull/67248)

- **#66984** — `fix(agent): persist the delivered response when the turn tail is a tool-call row`  
  Ensures the `final_response` is written to the transcript even when the assistant’s last row contains only `tool_calls` (no content). Fixes a SQLite durability regression.  
  [PR #66984](https://github.com/NousResearch/hermes-agent/pull/66984)

- **#67240** — `fix(agent): persist delivered response when turn tail is a tool-call row` (duplicate fix, merged instead of #66984)  
  [PR #67240](https://github.com/NousResearch/hermes-agent/pull/67240)

- **#67241** — `fix(telegram): cause-agnostic wedged-recovery watchdog + bounded drain so the reconnect ladder can't freeze silently`  
  Addresses #66377 (Telegram gateway going silently deaf for hours). Adds a watchdog and bounded drain to prevent the reconnect ladder stall.  
  [PR #67241](https://github.com/NousResearch/hermes-agent/pull/67241)

- **#67243** — `feat(auth): canonical shared xAI OAuth store for multi-profile single-use refresh tokens (#65394)`  
  Solves multi-profile OAuth invalidation for xAI Grok by introducing an opt-in canonical token store.  
  [PR #67243](https://github.com/NousResearch/hermes-agent/pull/67243)

- **#61519** — `fix(gateway): dedupe pending voice transcript echoes` (original PR, superseded by #67248 but closed today)  
  [PR #61519](https://github.com/NousResearch/hermes-agent/pull/61519)

---

## 🔥 Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | Summary |
|-------|----------|---------|
| [#38216](https://github.com/NousResearch/hermes-agent/issues/38216) | 10 | **CLOSED** — Hermes Desktop v40.9.3 crashes on Windows 11 startup (0x80000003 breakpoint exception at consistent offset). P1, Windows-specific. |
| [#66829](https://github.com/NousResearch/hermes-agent/issues/66829) | 7 | **OPEN** — Desktop always preprocesses images through auxiliary vision model even when main model supports vision. Users want native vision pass-through. |
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 6 | **OPEN** — Skills index freshness probe failed: index is 29.8h old (limit 26h). Automated degradation affecting `/docs/skills`. |

**Underlying needs**: Users are frustrated by: (1) Windows desktop crashes that block usage entirely, (2) wasteful image processing pipelines that degrade response quality when the main model already supports vision natively, and (3) stale documentation indexes that impair skill discovery.

### Notable Open PRs with High Activity

- **#66163** — `feat(slack): configurable slash-command namespace prefix`  
  Open, needs decision. Addresses workspace-level slash command conflicts.  
  [PR #66163](https://github.com/NousResearch/hermes-agent/pull/66163)

- **#62944** — `feat: single gateway, multiple agents`  
  A major feature rebased onto current `main`, open for 7 days. High scope and risk.  
  [PR #62944](https://github.com/NousResearch/hermes-agent/pull/62944)

- **#67208** & **#67223** — Two competing fixes for MCP tool re-registration after parked server revival (issue #67187). Community is actively discussing the right approach.  
  [PR #67208](https://github.com/NousResearch/hermes-agent/pull/67208) — [PR #67223](https://github.com/NousResearch/hermes-agent/pull/67223)

---

## 🐛 Bugs & Stability

### Critical (P0)

- **#66994** — Installation didn’t finish error on Windows (`Setup`). `CLOSED` after fix.  
  [Issue #66994](https://github.com/NousResearch/hermes-agent/issues/66994)

- **#67000** — Installer log shows incomplete bootstrap on Windows. `CLOSED`.  
  [Issue #67000](https://github.com/NousResearch/hermes-agent/issues/67000)

### High (P1 / P2)

- **#38216** — Desktop crash on Windows 11 startup (0x80000003). **CLOSED** — fix presumably merged earlier.  
  [Issue #38216](https://github.com/NousResearch/hermes-agent/issues/38216)

- **#66377** — Telegram polling reconnect ladder stalls mid-way; gateway alive but silent. **CLOSED** (fixed via #67241).  
  [Issue #66377](https://github.com/NousResearch/hermes-agent/issues/66377)

- **#67187** — MCP parked server revival reconnects but does not re-register tools. **OPEN** — two fix PRs competing (see above).  
  [Issue #67187](https://github.com/NousResearch/hermes-agent/issues/67187)

- **#67233** — Unable to send image to LLM via Telegram (vision pipeline failure). **CLOSED**.  
  [Issue #67233](https://github.com/NousResearch/hermes-agent/issues/67233)

- **#67120** — Changing model via SSH/hermes config no longer propagates to active gateway sessions after update. **OPEN** — needs decision.  
  [Issue #67120](https://github.com/NousResearch/hermes-agent/issues/67120)

- **#51448** — Hermes Desktop + LM Studio on native Windows fails (“empty stream, no finish_reason”); works under WSL. **OPEN**, unanswered since June.  
  [Issue #51448](https://github.com/NousResearch/hermes-agent/issues/51448)

- **#65631** — Provider error chunk (HTTP-200 SSE carrying a 400) misclassified as “empty stream” and retried forever. **OPEN**.  
  [Issue #65631](https://github.com/NousResearch/hermes-agent/issues/65631)

### Windows-Specific Regressions

A cluster of Windows-only issues appeared today:

- **#67158** — CLI lockfile not cleaned up on exit → ghost lock on multi-instance runs (P3, OPEN).  
- **#67159** — CLI rendering artifacts in legacy `cmd.exe` (P3, CLOSED).  
- **#67161** — Desktop “Unsupported install method” popup fires on editable git installs (P3, CLOSED).

---

## 💡 Feature Requests & Roadmap Signals

- **Smart model routing** (#66860, CLOSED as “not‑planned”) — auto-select model based on task complexity. Requested but not accepted upstream.
- **Temporal metadata for skills** (PR #67242) — adds `created_at`/`updated_at`/`expires_at` to SKILL.md frontmatter with GC. Likely to land in next minor release.
- **File upload support for API** (PR #67246) — enables agent-generated files (reports, charts) to be uploaded to remote servers. Still open with `needs-decision`.
- **Board phase 2 in desktop app** (#66415, CLOSED as “not‑planned”) — a visual board in Electron was declined.
- **Role-based subagents** (#66819, CLOSED as “not‑planned”) — user wanted profile identity inheritance for delegate subagents.

**Prediction for next version**: Skills temporal metadata (PR #67242) and the single-gateway multi-agent feature (PR #62944) are strong candidates. The MCP tool re-registration fix will likely land after community debate resolves.

---

## 🗣️ User Feedback Summary

**Pain points** (from issue descriptions):
- **Windows users**: Repeated installation/startup crashes, lockfile leaks, rendering artifacts, and the persistent LM Studio incompatibility (#51448) are the top frustrations.
- **Vision pipeline inefficiency**: Users running models with native vision (e.g., GPT‑4o) complain that Hermes still routes images through an auxiliary model, slowing responses and losing quality (#66829).
- **Configuration propagation regression**: After the latest `hermes update`, model changes no longer apply to active Telegram sessions; users must restart the gateway (#67120).
- **Gateway reliability**: The Telegram gateway going silently deaf (#66377) and voice transcription duplication (#61455) eroded trust in real-time messaging.
- **MCP tool lifecycle**: Parked servers reviving without tools (#67187) forces manual restarts — a stability issue for multi-server setups.

**Satisfaction signals**: The project maintained high merge velocity; most critical bugs were closed on the same day or within 24 hours. Users acknowledged rapid fixes on issues like desktop crash and installer failures.

---

## ⏳ Backlog Watch — Items Needing Maintainer Attention

| Issue/PR | Age | Problem |
|----------|-----|---------|
| [#51448](https://github.com/NousResearch/hermes-agent/issues/51448) | 26 days | LM Studio on native Windows fails; identical config works under WSL. No maintainer response since June 23. |
| [#65631](https://github.com/NousResearch/hermes-agent/issues/65631) | 3 days | Provider error chunks cause infinite retries. Needs a decision on canonical fix. |
| [#67120](https://github.com/NousResearch/hermes-agent/issues/67120) | 1 day | Model config propagation broken after update. P2, `needs-decision`, multiple sweeper labels. |
| [#67158](https://github.com/NousResearch/hermes-agent/issues/67158) | 1 day | CLI lockfile not cleaned up — Windows multi-instance ghost lock. P3 but affects Windows automation. |
| [PR #62944](https://github.com/NousResearch/hermes-agent/pull/62944) | 7 days | Single gateway, multiple agents — major feature, still open with many labels but no recent review. |
| [PR #66163](https://github.com/NousResearch/hermes-agent/pull/66163) | 2 days | Slack slash-command prefix configuration. `needs-decision` and `sweeper:blast-moderate`. |

**Recommendation**: The Windows LM Studio issue (#51448) is the oldest open bug with no maintainer acknowledgment — it should be triaged to either confirm a known limitation or escalate for a fix. The MCP tool re-registration PRs (#67208, #67223) need a maintainer to pick one direction to avoid community duplication.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-07-19

## 1. Today's Overview

Project activity remains steady, with 4 issues and 12 pull requests updated in the last 24 hours. Two new bugs were reported (a gateway startup crash and a message-splitting infinite loop), while 8 PRs were merged or closed, including significant feature work like native WhatsApp typing presence and a fix for OAuth refresh concurrency. No new releases were published. The team appears focused on closing older feature branches and addressing recent regressions.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release prior to this date is unknown from the provided data.

## 3. Project Progress

**Features advanced or fixed (PRs closed/merged today):**

- **Agent Collaboration Bus** – PR #2937 (afjcjsbx) merged: Introduces a durable inter-agent communication system with per-agent mailboxes, collaboration threads, and permission-aware message delivery. This is a foundational feature for multi-agent workflows.
- **WhatsApp Native Typing Presence** – PR #3242 (As-tsaqib) closed/mereged: Implements `channels.TypingCapable` on `WhatsAppNativeChannel`, sending composing/paused indicators while the agent processes replies.
- **OAuth Refresh Provider-Correct & Concurrency-Safe** – PR #3241 (As-tsaqib) closed/mereged: Fixes `auth.RefreshAccessToken` to send JSON for OpenAI, omit scopes on refresh, and add a 30-second hysteresis lock to prevent races.
- **Default Fallback Chain for Models** – PR #3200 (lc6464) closed/mereged: Adds a configurable default model fallback chain in the web UI, persisted via the backend API.
- **Seed XML Tool Call Recovery** – PR #3165 (Alix-007) closed/mereged: Recovers Volcengine’s `<seed:tool_call>` XML blocks from OpenAI-compatible responses and strips them from visible output.
- **Dependency Updates** – PR #3211 (dependabot) merged: Bumps `eslint` from 10.4.1 to 10.6.0 in `web/frontend`.  
  PR #3208 (dependabot) merged: Bumps `maunium.net/go/mautrix` from 0.27.0 to 0.28.1.
- **Agent-Specific Runtime Overrides** – PR #3225 (xdatafactor) closed/mereged: Allows per-agent `max_tokens`, summarization thresholds, and `split_on_marker` overrides in config.

## 4. Community Hot Topics

The two most active discussion points today are new bug reports:

- **[Issue #3265] Gateway startup fails** – Cipher208 reported that the gateway crashes with an error about the deltachat channel even when deltachat is not configured. No comments or reactions yet, but this blocks all gateway operation.  
  [sipeed/picoclaw Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)

- **[Issue #3264] SplitMessage hangs on oversized fenced-code info string** – floze-the-genius described an infinite loop in `channels.SplitMessage` caused by a fenced code block info string that exceeds the split point. The fallback logic fails to make progress.  
  [sipeed/picoclaw Issue #3264](https://github.com/sipeed/picoclaw/issues/3264)

Additionally, the long-open **PR #3193** “Added simplex channel type” (dim) was updated again today, suggesting continued community interest in supporting the Simplex messaging protocol.  
[sipeed/picoclaw PR #3193](https://github.com/sipeed/picoclaw/pull/3193)

## 5. Bugs & Stability

| ID | Summary | Severity | Fix PR Exists? |
|---|---|---|---|
| [#3265](https://github.com/sipeed/picoclaw/issues/3265) | Gateway fails to start with “unknown type deltachat” error even without deltachat config | **High** – prevents gateway from running | No |
| [#3264](https://github.com/sipeed/picoclaw/issues/3264) | `SplitMessage` loops indefinitely on fenced-code info strings longer than the split point | **High** – causes permanent hang | No |

Both bugs are open with no associated fix PRs yet. The community should watch for responses from maintainers.

Stale issues recently closed (no action needed):

- [#3239](https://github.com/sipeed/picoclaw/issues/3239) – OAuth refresh race condition (fixed by PR #3241)
- [#3240](https://github.com/sipeed/picoclaw/issues/3240) – WhatsApp typing presence (fixed by PR #3242)

## 6. Feature Requests & Roadmap Signals

Based on recently merged PRs and open work, the following features are likely candidates for the next release:

- **Multi-agent collaboration** – The Agent Collaboration Bus (PR #2937) is a major new capability. Next steps may include UI integration or documentation.
- **Default fallback chain for models** (PR #3200) – Users can now configure a fallback chain via the web UI; this will likely be polished before release.
- **Simplex channel support** – PR #3193 remains open. If merged, PicoClaw would gain the ability to communicate over the Simplex protocol.
- **9router compatibility and ARMv7 builds** – PR #3205 (open) adds Linux ARMv7 targets and fixes response parsing for 9router gateways, addressing Raspberry Pi users.
- **ID normalization fixes** – PR #3202 (open) corrects leading/trailing underscore stripping in agent/account IDs, important for routing consistency.

No new feature requests appeared in today’s issues. The direction is toward broader platform support (ARM, Simplex) and better multi-agent orchestration.

## 7. User Feedback Summary

- **Pain points addressed**: Two recent issues (#3239, #3240) were resolved today by contributors As-tsaqib. The OAuth refresh race and missing WhatsApp typing presence were real user complaints that now have fixes.
- **New pain points**: Gateway startup failure (#3265) and message-splitting hang (#3264) are blocking users. Both reports are detailed, giving maintainers clear reproduction steps.
- **Satisfaction signals**: The 9router and ARM support PR (#3205) was motivated by a user’s actual deployment on a Raspberry Pi 3 B+ with 9router, indicating active community use cases beyond standard setups.
- **Overall tone**: Users are engaged, filing clear bug reports and contributing features. The community appears satisfied with the project’s responsiveness, as demonstrated by the quick merging of fixes for earlier issues.

## 8. Backlog Watch

The following items are long-open and may require maintainer attention:

- **[PR #3202](https://github.com/sipeed/picoclaw/pull/3202)** (stale, opened July 1) – Fix for ID normalization leading/trailing underscores. No comments from maintainers. Could cause routing bugs if unmerged.
- **[PR #3248](https://github.com/sipeed/picoclaw/pull/3248)** (stale, opened July 10) – Go version bump to 1.25.12 for security fixes. Stale despite addressing CI issues; should be reviewed to keep builds secure.
- **[Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)** (new) – No reply from maintainers yet. As a startup blocker, it warrants priority triage.
- **[Issue #3264](https://github.com/sipeed/picoclaw/issues/3264)** (new) – No maintainer response yet. A hang is serious and should be triaged quickly.

No PRs or issues older than 30 days outside the stale-label set were updated. The backlog appears manageable, but the two new bugs are urgent.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-19

## Today's Overview
NanoClaw saw intense activity over the last 24 hours with **18 issues updated** (16 closed) and **26 pull requests updated** (17 merged/closed). This reflects a robust development cadence, with fixes spanning multiple adapters (WhatsApp, Slack, credential proxy) and a strong focus on reliability and security. No new releases were tagged today. The community is actively contributing both bug reports and PRs, with core-team members also pushing fixes.

## Releases
*No new releases in this digest period.*

## Project Progress
### Merged/Closed PRs (17 merged/closed)
Key fixes that landed today include:

- **[PR #3087](https://github.com/nanocoai/nanoclaw/pull/3087) — fix(whatsapp): engage mention-mode wirings on typed @-mentions in groups**  
  Addresses the open bug [#3085] where autocomplete-based mentions were required; now plain text `@agent` also triggers wiring.

- **[PR #3086](https://github.com/nanocoai/nanoclaw/pull/3086) — fix(whatsapp): validate recipient exists before sending**  
  Prevents silent message loss when a JID is not registered on WhatsApp.

- **[PR #3077](https://github.com/nanocoai/nanoclaw/pull/3077) — fix(claude): only abort on a rejected rate_limit_event; split rate_limit vs quota**  
  Fixes the false positive "Rate limit (quota)" logging that flooded logs on every normal turn (see [#3016]).

- **[PR #2496](https://github.com/nanocoai/nanoclaw/pull/2496) — fix: open outbound DB with write access in writeOutboundDirect**  
  Resolves a critical silent failure where command‑gate deny responses were never delivered due to `SQLITE_READONLY`.

- **Multiple Slack setup UX PRs by alipgoldberg** ([#2314](https://github.com/nanocoai/nanoclaw/pull/2314), [#2305](https://github.com/nanocoai/nanoclaw/pull/2305), [#2304](https://github.com/nanocoai/nanoclaw/pull/2304), [#2303](https://github.com/nanocoai/nanoclaw/pull/2303), [#2299](https://github.com/nanocoai/nanoclaw/pull/2299), [#2296](https://github.com/nanocoai/nanoclaw/pull/2296)) — plain‑language instructions, better token order, member‑ID fallback, and part‑1/part‑2 labeling.

- **[PR #2702](https://github.com/nanocoai/nanoclaw/pull/2702) — fix(slack): switch adapter to Socket Mode**  
  Eliminates the need for a public webhook URL by using Slack’s Socket Mode.

- **[PR #1267](https://github.com/nanocoai/nanoclaw/pull/1267) / [#1212](https://github.com/nanocoai/nanoclaw/pull/1212) / [#1185](https://github.com/nanocoai/nanoclaw/pull/1185) / [#1100](https://github.com/nanocoai/nanoclaw/pull/1100) — fix: prepend ANTHROPIC_BASE_URL pathname in credential proxy**  
  Multiple contributors (kk17, jiangyunpeng, pengchongfu, npulgh) converged on the same fix to support third‑party Anthropic‑compatible providers.

- **[PR #3084](https://github.com/nanocoai/nanoclaw/pull/3084) — test(runner): drop temporary diagnostics from /clear-abort test**  
  Cleans up instrumentation left in a prior merge.

Advancements also include closed feature issues for **keyword‑based message routing** ([#1681](https://github.com/nanocoai/nanoclaw/issues/1681), [#1679](https://github.com/nanocoai/nanoclaw/issues/1679)) — likely landed earlier.

## Community Hot Topics
Most active discussions (by comment count):

- **[Issue #2506](https://github.com/nanocoai/nanoclaw/issues/2506) — Bug: send_message dedup silently drops responses** (4 comments)  
  Two separate trigger conditions cause agent responses to be dropped and the client to time out. This was closed today, suggesting a fix has been identified.

- **[Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016) — Every rate_limit_event logged as quota error** (3 comments)  
  Caused noisy log spam on completely normal turns. The fix was merged in PR #3077, which was also closed today.

- **[Issue #2482](https://github.com/nanocoai/nanoclaw/issues/2482) — Wizard falsely detects "no systemd" under su -** (3 comments)  
  A common setup pain point for unprivileged containers. The related open issue [#1981] continues to track the same underlying problem.

- **[Issue #2916](https://github.com/nanocoai/nanoclaw/issues/2916) — “hi”** (3 comments)  
  A short test/hello issue, now closed.

Underlying needs: Users are actively reporting edge cases in media handling, adapter configuration, and silent failures, and the community is responding with quick fixes.

## Bugs & Stability
Bugs reported or addressed today, ranked by severity:

| Severity | Bug | Status | Fix PR | Notes |
|----------|-----|--------|--------|-------|
| **Critical** | **Queue‑gate deny responses silently lost** ([#2496](https://github.com/nanocoai/nanoclaw/issues/2496) → fixed) | Closed | [PR #2496](https://github.com/nanocoai/nanoclaw/pull/2496) | `SQLITE_READONLY` caused all command‑gate denials to be dropped. |
| **Critical** | **Loopback webhook lacks authentication** ([GHSA-h9g4-589h-68xv](https://github.com/nanocoai/nanoclaw/issues/3065)) | Fix PR open | [PR #3065](https://github.com/nanocoai/nanoclaw/pull/3065) | Unprivileged processes on the host can forge actions. |
| **High** | **Send_message dedup drops responses** ([#2506](https://github.com/nanocoai/nanoclaw/issues/2506)) | Closed | (no specific PR listed, but issue closed) | Two causes: near‑simultaneous turns and follow‑up during streaming. |
| **Medium** | **WhatsApp mention‑mode only fires on autocomplete** ([#3085](https://github.com/nanocoai/nanoclaw/issues/3085)) | Open | [PR #3087](https://github.com/nanocoai/nanoclaw/pull/3087) (merged today) | Manually typed `@agent` text does not engage; fix landed. |
| **Medium** | **WhatsApp inbound media silently dropped on CDN fetch failure** ([#2894](https://github.com/nanocoai/nanoclaw/issues/2894)) | Closed | Fix likely in earlier cycle | Baileys `catch` swallowed attachment errors. |
| **Medium** | **Rate limit false positive logged on every turn** ([#3016](https://github.com/nanocoai/nanoclaw/issues/3016)) | Closed | [PR #3077](https://github.com/nanocoai/nanoclaw/pull/3077) | Telemetry event misinterpreted as terminal error. |
| **Medium** | **Setup wizard bypasses systemd on headless Linux** ([#1981](https://github.com/nanocoai/nanoclaw/issues/1981) (open) + [#2482](https://github.com/nanocoai/nanoclaw/issues/2482) (closed) | One closed, one open | [PR #2482](https://github.com/nanocoai/nanoclaw/issues/2482) fix provided earlier | Underlying cause: env vars not populated under `su -`. Open issue [#1981] remains. |
| **Low** | **Container‑runner staleness check only watches index.ts** ([#2784](https://github.com/nanocoai/nanoclaw/issues/2784)) | Closed | Fix presumably merged | Misses changes to `ipc-mcp-stdio.ts`. |

## Feature Requests & Roadmap Signals
Several user‑requested features appear near completion or are high‑priority:

- **Keyword‑based pre‑turn model routing** ([#1681](https://github.com/nanocoai/nanoclaw/issues/1681), [#1679](https://github.com/nanocoai/nanoclaw/issues/1679) — both closed)  
  Allows selecting LLM by message keywords (e.g., `code review` → Claude Sonnet, `research` → Gemini Flash). Likely landing in the next minor release.

- **Scheduled tasks CLI** ([#2397](https://github.com/nanocoai/nanoclaw/issues/2397) — closed)  
  Users want `ncl` subcommands to list, run‑now, pause, cancel scheduled tasks. Closed issue suggests implementation is in progress.

- **Group config mount commands** ([#2395](https://github.com/nanocoai/nanoclaw/issues/2395) — closed)  
  Missing `ncl groups config add-mount / remove-mount` after DB migration. Also closed, likely incoming.

- **Utility skill: `ncc` host CLI** ([PR #2971](https://github.com/nanocoai/nanoclaw/pull/2971) — open)  
  A new standalone tool for host operational and health commands. This PR has been open for 12 days and may merge soon.

- **Unarchive agent groups on reference** ([#2517](https://github.com/nanocoai/nanoclaw/issues/2517) — closed)  
  MGA references can point to archived groups; auto‑unarchive and GC logic was merged.

**Prediction for next version:** Keyword routing, scheduled tasks CLI, and group mount CLI are strong candidates. The Slack Socket Mode fix and WhatsApp mention fix are already merged.

## User Feedback Summary
Real user pain points reflected in the data:

- **Setup friction:** Multiple users (glifocat, bromleymindfulness) struggle with systemd detection on headless Linux and unprivileged containers. The wizard falls back to nohup instead of a proper systemd user unit.
- **Log pollution:** Users (glifocat) were alarmed by repeated "quota error" messages that were actually harmless – now fixed.
- **Silent failures:** The `send_message` dedup bug caused timeouts without user‑visible errors; the outbound DB readonly bug meant deny responses never arrived. Both erode trust.
- **WhatsApp media drops:** Inbound images/video silently lost when CDN fetch fails – a significant UX gap now fixed.
- **Slack setup complexity:** Non‑technical users found the Slack setup jargon‑heavy and the two‑card flow confusing. The UI improvements from alipgoldberg directly address this.

Overall, users are actively testing edge cases and the maintainers are responding quickly. Satisfaction appears high given the speed of issue resolution and the large number of community‑submitted PRs (e.g., 4 separate credential‑proxy fix PRs).

## Backlog Watch
Issues and PRs that have been open for an extended period or lack maintainer attention:

- **[Issue #1981](https://github.com/nanocoai/nanoclaw/issues/1981) — v2 setup: systemd misdetected as absent on headless Linux**  
  Opened 2026-04-24, last updated 2026-07-19 (still open). While the related issue [#2482] was closed, the underlying problem persists for certain environments (Ubuntu on Hetzner, SSH sessions). Only 1 comment (from bot?) – deserves a triage and possibly a fix that covers both `su -` and SSH scenarios.

- **[PR #3068](https://github.com/nanocoai/nanoclaw/pull/3068) — Fix scheduled task cross-session visibility and error clarity**  
  Open since 2026-07-16, no review comments yet. Addresses a real confusion where task tools give poor feedback when operated from different sessions.

- **[PR #3065](https://github.com/nanocoai/nanoclaw/pull/3065) — fix(security): authenticate loopback webhook**  
  Open since 2026-07-16, no comments. Given the severity (action forgery), this should be prioritized for review and merge.

None of the above show signs of being stale, but maintainer bandwidth may be stretched given the volume of PRs.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-07-19

## 1. Today's Overview
Project activity remains very low: only one issue was updated in the last 24 hours, with no new pull requests or releases. The single open issue (#868) concerns a build failure on Android/Termux and has been active since April, suggesting a persistent but isolated platform bug. No feature work or merged changes were recorded today. Overall project health appears stable but with minimal community contribution or maintainer response in the short term.

## 2. Releases
*No new releases in the last 24 hours. Latest known release is `v2026.4.17` (referenced in issue #868).*

## 3. Project Progress
*No pull requests were merged, closed, or updated today. No features advanced or fixes were committed.*

## 4. Community Hot Topics
**Issue #868 – [bug] zig build fails on Android/Termux (aarch64)**  
- **Status:** Open  
- **Author:** NOTJuangamer10  
- **Created:** 2026-04-23 | **Updated:** 2026-07-18 | **Comments:** 7 | 👍: 0  
- **URL:** [`nullclaw/nullclaw#868`](https://github.com/nullclaw/nullclaw/issues/868)  

**Summary:** The user reports that `zig build -Doptimize=ReleaseSmall` fails with an `AccessDenied` error when linking `options.zig` into the final binary. Environment details: Android 14 (LineageOS 22.2), Termux, aarch64, Zig 0.16.0, NullClaw v2026.4.17.  
**Underlying need:** Users attempting to build NullClaw natively on mobile/ARM64 devices face a permissions or filesystem limitation in Termux’s sandboxed environment. The issue likely requires either a workaround in the build script (e.g., alternative temporary directory) or a fix in Zig’s linker for Android/Termux. The lack of maintainer response (no assignees, labels, or comments from maintainers) indicates this bug is **unaddressed** and may be blocking Android-based contributions.

## 5. Bugs & Stability
**Only active bug:**  
- **Issue #868** – Build failure on Android/Termux (aarch64) due to `AccessDenied` on `linkat`.  
  - **Severity:** Medium – Blocks native builds on a significant mobile platform, but no crashes or data loss reported.  
  - **Status:** No associated fix PR exists. The error is reproducible with Zig 0.16.0 and likely related to Termux’s restricted filesystem.  
  - **Workaround:** None documented; users may try alternative Zig versions or different build configurations.

*No regressions, crashes, or new stability issues reported today.*

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were made in the last 24 hours. The only community engagement is a build bug, suggesting current users are focused on resolving platform compatibility rather than requesting new functionality.  
**Prediction:** The next release may include adjustments to the build system (e.g., using `--cache-dir`, `--global-cache-dir`, or `fs` permissions workarounds) to support Termux/Android, but no concrete roadmap signals exist.

## 7. User Feedback Summary
- **Pain points:** Native compilation on Android mobile devices (Termux) is broken, blocking users who want to build NullClaw on aarch64 ARM devices. The error message is opaque (`AccessDenied`), and no immediate fix or documentation exists.  
- **Use case:** Building NullClaw directly on a smartphone running LineageOS with Termux – likely for personal development or testing on low-cost ARM hardware.  
- **Satisfaction/Dissatisfaction:** The user reported the issue with a detailed environment description, but the 7 comments (all likely from other users) and zero maintainer responses suggest frustration and a lack of official support for this use case.

## 8. Backlog Watch
**Issue #868** has been open for nearly three months (since 2026-04-23) and remains unassigned, unlabeled, and without any maintainer comment. This is the **only open issue** with recent activity and represents a growing backlog item that could deter potential Android/Termux contributors.  
**Recommendation:** Maintainers should triage this issue, add appropriate labels (e.g., `platform:android`, `build`, `help wanted`), and either provide a known workaround or confirm the bug to set expectations.

---

*All links are to GitHub issue #868 on the `nullclaw/nullclaw` repository. No pull requests or releases were available for linking.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-19

## 1. Today's Overview

IronClaw saw extremely high activity over the past 24 hours, with **50 pull requests** updated (30 merged/closed) and **5 issues** touched (4 still open). The core team led by **ilblackdragon** drove a large batch of architecture-simplification PRs, collapsing runtime adapters, cleaning up dead fields, and laying groundwork for the `CapabilityOutcome` → `Resolution` migration. No new releases were published, but the release workflow is being refactored to be Reborn-compile-only (#6188). A notable security bug was reported (#6247) involving plaintext bearer tokens in MCP server config storage. Community interest remains moderate, with one localization request and several feature parity items waiting for design validation.

## 2. Releases

**None** – no new releases were tagged in the last 24 hours. The ongoing release PR (#5598) remains open, indicating a pending bump for `ironclaw_common` (0.5.0, breaking) and `ironclaw` (0.29.1).

## 3. Project Progress

**30 pull requests were merged or closed today**, reflecting intense development on the Reborn architecture simplification. Key highlights:

- **Architecture simplification (Slice B & C)** — Multiple PRs by ilblackdragon:
  - `#6235` – Deployment mode now a config value; `LocalDev*` family collapsed.
  - `#6240` – `RuntimeAdapter` dyn registry replaced with closed `RuntimeLane` executor.
  - `#6242` – `CapabilityOutcome` → `Resolution` mapping landed additively in `ironclaw_turns`.
  - `#6243` – Persistent `GateRecordStore` for gate payloads during the result collapse.
  - `#6239` – `authorize()` delegating scaffold extracted (security-critical, safe step).
  - `#6241` – Extended `authorize()` fold to cover resume, auth-resume, spawn (open, not yet merged).
  - `#6237` – Result-record vocabulary (`GateRecord`, `DenyRecord`).
  - `#6236` – `SafeSummary` deduplicated to single definition in `host_api`.
  - `#6234` – Dead `trust_decision` field removed from capability request family.
  - `#6233` – W1a wiring for `Authorized` seal and `RuntimeLane::from_runtime_kind`.
  - `#6238` – DTO-collapse ratchet tests (anti-slippage).

- **CI & docs**:
  - `#6188` – Release workflow made Reborn-compile-only (open).
  - `#6176` – Validate Reborn binaries across seven targets (open).
  - `#6253` – Interactive architecture explorer and diagram skill (open).
  - `#6252` – Testing plan for capability state machines (§11.9) (open).

- **Other**:
  - `#6211` – Fixed stubs in `reborn-cli` (channels, hooks, logs) to return explicit errors instead of fake success (open, by sergeiest).
  - `#6251` – OAuth denial lifecycle made channel-neutral (open, by BenKurrek).
  - `#6244` – Agent-market deploy branch: thread-scoped MCP sessions and programmatic MCP config (open, by kirikov).

## 4. Community Hot Topics

Activity in issues and PRs with discussion or reactions remains low, but one issue stands out:

- **[#6158 – Add zh-TW Traditional Chinese localization](https://github.com/nearai/ironclaw/issues/6158)**  
  *2 comments, open since July 16*  
  A user requests Traditional Chinese locale support for WebUI v2. Currently only Simplified Chinese is offered. This is the only issue with any comments, indicating a clear user need for broader i18n.

No other issues or PRs have recorded comments or 👍 reactions in the last 24h. Overall community involvement is low, likely because the current activity is dominated by internal refactoring.

## 5. Bugs & Stability

One high-severity security bug was reported today:

- **[#6247 – MCP server headers persist bearer tokens in plaintext](https://github.com/nearai/ironclaw/issues/6247)**  
  *Author: kirikov*  
  **Severity: HIGH** – `McpServerConfig.headers` is serialized in plaintext into the `mcp_servers` settings DB row (including backups/exports) and also mounted into per-job worker sandboxes. Token leakage could compromise OAuth credentials. No fix PR has been linked yet.

No other crashes or regressions were reported. The closed issue **#6143** (promote Reborn to canonical CLI) is a planned rollout, not a bug.

## 6. Feature Requests & Roadmap Signals

Three feature requests were updated today, all in open state:

- **[#6158 – zh-TW Traditional Chinese localization](https://github.com/nearai/ironclaw/issues/6158)** — Straightforward i18n enhancement. Likely to be included in a future WebUI v2 release.

- **[#6249 – Reborn: extensions-management API parity for MCP servers](https://github.com/nearai/ironclaw/issues/6249)** — The v1 gateway has install/activate/PATCH endpoints; Reborn's webchat v2 lacks them. This is part of the ongoing effort to bring Reborn to feature parity with v1. Likely to be addressed after the current architecture simplification stabilises.

- **[#6248 – Reborn: credential preflight before approval/sandbox](https://github.com/nearai/ironclaw/issues/6248)** — Blocked on `auth_resume` design. This is a core security enhancement to check OAuth account existence before spinning up sandboxes. Given its dependency on the ongoing authorization redesign, it may ship in the next major Reborn release.

All three align with the project's roadmap: Reborn is transitioning from v1 to the canonical CLI, and these features represent remaining gaps.

## 7. User Feedback Summary

No direct user feedback (e.g., comments on closed issues, satisfaction reports) was captured in today's data. The only user-facing signal is the i18n request (#6158), which implies that users with Traditional Chinese locale preferences are forced to fall back to Simplified Chinese or English, a minor but visible gap. The lack of complaints suggests current stability is acceptable for most users, but the plaintext token bug (#6247) could become a pain point if exploited.

## 8. Backlog Watch

The following open items deserve attention:

- **[#5598 – chore: release](https://github.com/nearai/ironclaw/pull/5598)** — Open since July 3, with no comments. This PR bumps multiple crates, including breaking changes in `ironclaw_common` and `ironclaw_skills`. Stale for 16 days; the release may be waiting for Reborn refactoring to land. Should be revisited soon.

- **[#6188 – ci: make release workflow Reborn-compile-only](https://github.com/nearai/ironclaw/pull/6188)** — Open since July 17, no comments. Dependent on #6160 (not listed). Could block future releases if not merged.

- **[#6176 – ci: validate Reborn release binaries across seven targets](https://github.com/nearai/ironclaw/pull/6176)** — Open since July 17. Adds a critical preflight check; delays in merging increase risk of broken releases.

These are all maintainer-driven tasks; no community issues are languishing without response.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-07-19

## 1. Today's Overview
Activity over the past 24 hours shows a moderate level of maintenance work: 6 stale issues received updates (all remain open), 3 pull requests were touched (1 new open, 2 long‑standing ones finally closed/merged), and a new patch release (2026.7.17) was cut. The project appears to be in a steady state with ongoing bug triage and incremental feature delivery, though the backlog of unresolved issues from early April still demands attention. No new critical regressions were introduced, and the closing of two older PRs indicates the team is working through accumulated technical debt.

## 2. Releases
**New version: LobsterAI 2026.7.17** (released 2026-07-17)  
[View release](https://github.com/netease-youdao/LobsterAI/releases)

- **What's Changed**  
  - `feat(cowork): surface structured run failure details in error UI` – provides richer error feedback when cowork sessions fail.  
  - `Feat/2026.7.6 service deployment data persistence` – ensures deployment configurations survive restarts.  
  - `feat(skin): a` – (truncated; likely a UI skinning enhancement).  

No breaking changes, deprecations, or migration notes are mentioned. This release focuses on better user feedback and operational stability.

## 3. Project Progress
Two long‑standing pull requests were closed/merged in the last 24 hours, indicating resolution of features that had been waiting for review:

- **[#1353 – feat(agent): Agent 技能选择器新增全选和清除功能](https://github.com/netease-youdao/LobsterAI/pull/1353)**  
  Added "Select All" and "Clear" buttons to the Agent skill picker, along with a live counter of selected skills. Affects only `AgentSkillSelector.tsx` and `i18n.ts`.

- **[#1464 – fix(im): add duplicate validation for instance name and credential ID](https://github.com/netease-youdao/LobsterAI/pull/1464)**  
  Prevents creation of duplicate IM instances (DingTalk, Feishu, QQ) and duplicate bot credentials by adding validation on save and rename.

Additionally, a **new open PR** is introduced today:

- **[#2358 – fix(cowork): show feedback when session rename fails](https://github.com/netease-youdao/LobsterAI/pull/2358)**  
  Author: `wangxu-dev`. Adds localized error UI when a session rename request fails, fixing issue #670.

## 4. Community Hot Topics
No issues or PRs attracted more than a single comment or reaction in the last 24 hours. The most notable item based on long‑term activity is:

- **[#1293 – 自定义studio http 的mcp无法使用](https://github.com/netease-youdao/LobsterAI/issues/1293)** (👍1)  
  User reports that custom MCP definitions are not picked up by the OpenClaw engine; only SSE‑based MCPs work. This is a recurring concern from April that still lacks a resolution. The underlying need is better MCP engine integration – an area likely to be prioritized in upcoming releases.

## 5. Bugs & Stability
All six open issues updated today are existing bugs, not newly filed. Ranked by severity:

| Issue | Severity | Description | Has Fix PR? |
|-------|----------|-------------|-------------|
| [#1296 –上传长图（3M）解析页面直接报错](https://github.com/netease-youdao/LobsterAI/issues/1296) | **Critical** – Uploading a 3 MB tall image crashes the page and makes the entire task unusable. No workaround reported. | No |
| [#1307 – Cannot edit another model provider config after closing the edit panel](https://github.com/netease-youdao/LobsterAI/issues/1307) | **High** – Edit panel becomes read‑only after opening/closing a provider configuration, blocking further provider changes. | No |
| [#1298 –模型测试连接通过，输入简短文字却提示内容过长](https://github.com/netease-youdao/LobsterAI/issues/1298) | **Medium** – Input length validation incorrectly rejects short queries after a successful connection test. | No |
| [#1305 –定时任务运行成功后删除，历史记录标题名称展示不对](https://github.com/netease-youdao/LobsterAI/issues/1305) | **Medium** – Deleted scheduled tasks show incorrect titles in history. | No |
| [#1293 – 自定义MCP不可用](https://github.com/netease-youdao/LobsterAI/issues/1293) | **Medium** – Custom HTTP MCP not updated in engine. | No |
| [#1302 – 代码块添加行号显示切换按钮](https://github.com/netease-youdao/LobsterAI/issues/1302) | **Low** – Feature request (see next section). | No |

No new regressions surfaced today, but the existing critical bug [#1296] remains unresolved after three months.

## 6. Feature Requests & Roadmap Signals
The only feature request updated today is:

- **[#1302 – 为代码块添加行号显示切换按钮](https://github.com/netease-youdao/LobsterAI/issues/1302)**  
  Wants a line‑number toggle for code blocks (both language‑identified and plain). The request proposes using `react-syntax-highlighter`'s built‑in `showLineNumbers` and a custom `PlainCodeWithLineNumbers` component.

**Roadmap signal:** The merger of PR #1353 (skill selector "select all/clear") indicates the team is investing in Agent‑building UX. The next minor release could plausibly include the line‑number feature and a fix for the long‑standing MCP engine issue (#1293), as they directly impact user daily workflow.

## 7. User Feedback Summary
Real pain points captured from the updated issues:

- **MCP integration confusion**: Users expect custom HTTP MCP definitions to work seamlessly, but only SSE endpoints are supported by the engine. This creates a barrier for users wanting to extend studio capabilities.
- **Image processing fragility**: Uploading a moderately large image (3 MB) crashes the entire UI – a show‑stopper for document‑oriented use cases.
- **Misleading input validation**: Even after a successful model connection test, short text inputs are rejected as “too long,” suggesting a mismatch between model context limits and the frontend validation logic.
- **Configuration lock‑out**: Editing a model provider’s configuration and then switching to another provider leaves the UI in a disabled state, requiring a page reload.
- **Data inconsistency**: Scheduled tasks that are deleted show incorrect names in history, causing confusion when auditing runs.

Overall sentiment appears frustrated by bugs that have persisted for months, though the team’s responsiveness in closing old PRs (#1353, #1464) provides some counterbalance.

## 8. Backlog Watch
Several high‑impact issues from April have seen no maintainer response or fix attempt, despite being updated today (likely due to stale‑bot activity). They urgently need attention:

- **[#1293 – 自定义MCP无法使用](https://github.com/netease-youdao/LobsterAI/issues/1293)** – open since April 2, 2026; no maintainer comment.
- **[#1296 – 上传长图（3M）解析报错](https://github.com/netease-youdao/LobsterAI/issues/1296)** – critical crash, no response.
- **[#1298 – 输入内容过长误报](https://github.com/netease-youdao/LobsterAI/issues/1298)** – logic bug, no response.
- **[#1307 – 编辑面板只读](https://github.com/netease-youdao/LobsterAI/issues/1307)** – high severity UI bug, no response.

These four issues share the `stale` label and have zero maintainer participation. If they remain unaddressed, they risk eroding user trust in the project’s stability. A triage comment or at least a milestone assignment is recommended.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-19

## 1. Today's Overview
The project experienced a low-activity day with no new issues or releases reported in the last 24 hours. Three pull requests were updated, of which two were merged/closed and one remains open. Activity was concentrated on memory backend extensions, Slack API configurability, and a Web UI bug fix. Overall, the project appears stable with incremental feature additions rather than major overhauls.

## 2. Releases
No new releases were published on this date. The latest release remains unchanged.

## 3. Project Progress
Two pull requests were merged/closed today:
- **[PR #1159] feat(slack): support configurable API base URL** — Adds an `api_base_url` field to Slack account configuration (defaulting to `https://slack.com/api`). Routes all Slack client operations through this configurable endpoint.
  [GitHub](https://github.com/moltis-org/moltis/pull/1159)
- **[PR #1157] fix(web): support ACP-only chat setup** — Fixes the Web UI to correctly handle installations where only ACP agents (no LLM models) are configured. Previously this setup was treated as an error.
  [GitHub](https://github.com/moltis-org/moltis/pull/1157)

These changes improve integration flexibility and correct a usage-edge-case in the web interface.

## 4. Community Hot Topics
Only one open pull request received attention:
- **[PR #1158] feat(memory): add zvec vector database memory backend** — An experimental feature-gated backend (`zvec` Cargo feature) that uses Zvec and Redb for memory storage, intended to work with an independently-run llama.cpp embedding server. No comments or reactions were recorded, but the “vibe-coded” description suggests it is a lightweight, community-driven addition.
  [GitHub](https://github.com/moltis-org/moltis/pull/1158)

The absence of discussion on any item indicates low community engagement in the past day. The underlying need here is for alternative, self-hosted memory backends that avoid cloud dependencies—a common request among privacy-conscious users.

## 5. Bugs & Stability
A single bug fix was merged today, addressing a regression in the Web UI:
- **Medium severity**: The ACP-only chat setup (no connected LLM) was incorrectly treated as an error. Fixed in **PR #1157** by showing installed ACP agents during onboarding and auto-selecting an ACP agent when no models are configured.
  [GitHub](https://github.com/moltis-org/moltis/pull/1157)

No new bugs, crashes, or regressions were reported.

## 6. Feature Requests & Roadmap Signals
Two feature-request signals are present in the closed/merged PRs:
- **Configurable Slack API base URL (PR #1159)** — Allows custom Slack API endpoints, useful for enterprise proxies or local development.
- **Zvec vector database memory backend (PR #1158, still open)** — Provides an alternative to cloud-based memory stores.

Both are likely to be included in the next stable release, given that the Slack feature is already merged and the memory backend has a dedicated feature gate.

## 7. User Feedback Summary
No user-reported issues or feedback posts were created in the last 24 hours. The absence of issue activity either suggests general satisfaction or low usage. The two merged PRs addressed specific pain points (Slack API flexibility and ACP-only setup validation) that likely originated from earlier user experiences.

## 8. Backlog Watch
No long-unanswered issues or pull requests were identified. All tracked items are either recently created or have been addressed within the last 48 hours. The project backlog appears to be well-managed.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-19

## 1. Today’s Overview
CoPaw (based on the QwenPaw codebase) saw a moderate spike in activity today with 11 open issues and 7 pull requests updated in the last 24 hours. One PR was merged (a first-time contributor Mattermost integration closed after four months). No new releases were published today; the current stable version remains v2.0.0.post3. The community is actively reporting bugs and regressions, particularly around shell command deadlines, memory search loops, and environment variable handling. Several PRs have been opened to address the most critical stability issues.

## 2. Releases
None. The latest release remains v2.0.0.post3 (packaged as a post-release). No new releases were published in the last 24 hours.

## 3. Project Progress
One pull request was merged/closed today:
- **PR #1071** – [CLOSED] *feat: Introduce Mattermost channel integration for message*  
  Author: 2niuhe (first-time contributor)  
  URL: agentscope-ai/QwenPaw PR #1071  
  This long‑standing feature request was finally merged, adding a new Mattermost integration for message delivery. No other PRs were merged.

## 4. Community Hot Topics
The most active issues by comments and reactions:

- **Issue #6240** – [bug] *末尾出现注释显示* (3 comments)  
  Author: MCQSJ | URL: agentscope-ai/QwenPaw Issue #6240  
  Users report that after prolonged chat, memory‑related comments such as `<!-- ⟦ NEXT_RID 改为 1003 …` appear at the end of conversations. The community suspects a mis‑format of model output or a front‑end display exclusion failure.

- **Issue #6245** – *Session permanently blocked when shell command exceeds coordinator deadline* (2 comments)  
  Author: feng183043996 | URL: agentscope-ai/QwenPaw Issue #6245  
  A regression from the fix in #6056: when a shell command times out, the session becomes permanently blocked – all subsequent messages queue indefinitely until the process is restarted. This is considered a critical stability issue.

- **Issue #4641** – *qwenpaw env set → subprocess can't see it* (2 comments, reopened)  
  Author: manjieqi | URL: agentscope-ai/QwenPaw Issue #4641  
  Persistent pain point: environment variables set mid‑session are not visible to shell subprocesses. The community is asking for `env get KEY` or `env list --json` for runtime access.

The underlying need across these hot topics is **improved state consistency and error recovery** – users want transparent shell environment inheritance, graceful timeout handling, and correct rendering of memory annotations.

## 5. Bugs & Stability
Reports today cover several severity levels:

### Critical
- **Issue #6245** – Session permanently blocked after shell command deadline (regression).  
  Fix PR exists: **PR #6248** (open) by feng183043996 – *fix: distinguish offload vs cancel to prevent subprocess kill on deadline*  
  URL: agentscope-ai/QwenPaw PR #6248

- **Issue #6246** – `_saved_tool_refs` crashes with `OSError: [Errno 36] File name too long` during `recall_history`.  
  Fix PR exists: **PR #6247** (open) by zealonexp – adds try/except around `path.is_file()`.  
  URL: agentscope-ai/QwenPaw PR #6247

### High
- **Issue #6241** – Agent repeat outputs + `memory_search` infinite loop (no fix PR yet).  
  Author: z13645719 | URL: agentscope-ai/QwenPaw Issue #6241  
  The framework lacks a repetition‑detection mechanism strong enough to break the cycle.

### Medium
- **Issue #6242** – Console embedding dimensions setting not sent because `use_dimensions` not exposed.  
  Fix PR exists: **PR #6243** (open, first‑time contributor).  
  URL: agentscope-ai/QwenPaw PR #6243

- **Issue #6250** – Hard‑coded sandbox approval prompt when fallback active; no configurable skip.  
  Author: zhapeng2016 | URL: agentscope-ai/QwenPaw Issue #6250  
  No fix PR yet; user requests a new config option.

- **Issue #6239** – Windows PATH concatenation drops semicolons, breaking npm global access.  
  Author: 604731578 | URL: agentscope-ai/QwenPaw Issue #6239  
  No fix PR yet.

### Low
- **Issue #6249** – Source startup TUI stuck on “warming” (no logs).  
  Author: MojinXkl | URL: agentscope-ai/QwenPaw Issue #6249

## 6. Feature Requests & Roadmap Signals
Two user‑requested features stand out:

- **Issue #6244** – *记忆隔离能力* (memory isolation per project/conversation)  
  Author: yhfeitian | URL: agentscope-ai/QwenPaw Issue #6244  
  The user proposes introducing project‑level memory scopes to improve retrieval quality. This aligns with a common enterprise need and could appear in a future minor release.

- **Issue #6251** – *feat(cli): add scriptable environment reads* (PR, not yet merged)  
  Author: wananing | URL: agentscope-ai/QwenPaw PR #6251  
  Adds `qwenpaw env get KEY` and `qwenpaw env list --json`. This directly addresses the longstanding #4641 pain point and is likely to be merged soon.

Also noteworthy: **PR #6237** (niceIrene) improves Scroll history recall with date‑aware queries and complete conversational turn results – a quality‑of‑life enhancement for memory‑based workflows.

## 7. User Feedback Summary
Users express significant dissatisfaction with:
- **Session deadlocks** (#6245) – “permanently blocked” language shows high frustration.
- **Memory contamination** (#6240) – display of raw internal comments makes the UI unprofessional.
- **Environment isolation** (#4641) – mid‑session `env set` being opaque to child processes hinders automation scripts.
- **Sandbox fallback rigidity** (#6250) – no way to skip approval when sandbox is unavailable.
- **Windows PATH handling** (#6239) – subtle breakage of development tooling (npm) on Windows.

Positive signals: first‑time contributors are submitting meaningful fixes (PR #6243, PR #1071, PR #6247), indicating a healthy onboarding pipeline.

## 8. Backlog Watch
- **Issue #4641** – *qwenpaw env set → subprocess can't see it* (created 2026-05-23, last updated 2026-07-18).  
  This issue has been open for nearly two months. A PR (#6251) now addresses it, but it has not yet been merged. Maintainers should prioritise review.

- **Issue #6223** – *Release Duty: v2.0.0.post3 Installation Verification* (created 2026-07-17, 0 comments).  
  While not a user bug, this release‑duty checklist is past its deadline (2026-07-17) and still open – a sign that final verification may be stalled.

- **PR #6238** – *perf(drivers): initialize handlers concurrently* (open, no comments).  
  A performance optimisation that reduces startup latency. Without maintainer feedback, it risks falling through the cracks.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-19

## 1. Today's Overview

ZeroClaw saw intensive activity in the last 24 hours: **50 issues** and **50 pull requests** received updates. Of these, **11 issues were closed** (most notably bug reports and completed enhancements) and **3 PRs were merged or closed**. No new releases were published. The community remains highly engaged in shaping security infrastructure (key management, forbidden paths, supply‑chain signing), channel integrations (Telegram, Matrix, Slack, Discord), and the emerging WASM plugin system. The project’s health is strong, with rapid iteration on both bug fixes and forward‑leaning RFCs.

## 2. Releases

No new releases today. (Last release: none in the provided data.)

## 3. Project Progress

Three PRs were merged or closed in the last 24 hours, although their details are not shown in the top‑20 list. Among the active PRs, several represent significant advancements that were updated today:

- **Security & Secrets** – [#8857](https://github.com/zeroclaw-labs/zeroclaw/pull/8857) adds scoped secrets and encrypted state for plugins; [#9139](https://github.com/zeroclaw-labs/zeroclaw/pull/9139) introduces a durable scheduler outbox foundation; [#9142](https://github.com/zeroclaw-labs/zeroclaw/pull/9142) materializes named TLS profiles.
- **Agent & Providers** – [#9090](https://github.com/zeroclaw-labs/zeroclaw/pull/9090) enforces tool‑call pairing in a single canonical chokepoint; [#9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) adds native Hailo‑Ollama provider support; [#9102](https://github.com/zeroclaw-labs/zeroclaw/pull/9102) strips unhandled non‑image media markers before dispatch.
- **Gateway & Channels** – [#9026](https://github.com/zeroclaw-labs/zeroclaw/pull/9026) allows selecting the agent via `?agent=` query param in the ACP gateway; [#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443) adds single‑message progress drafts for Matrix.
- **CI & Code Quality** – [#9131](https://github.com/zeroclaw-labs/zeroclaw/pull/9131) makes the comment hygiene gate language‑aware; [#9055](https://github.com/zeroclaw-labs/zeroclaw/pull/9055) makes translation refresh reproducible; [#9115](https://github.com/zeroclaw-labs/zeroclaw/pull/9115) routes compile‑heavy jobs to optional Blacksmith runners.
- **Hardware** – [#9157](https://github.com/zeroclaw-labs/zeroclaw/pull/9157) resynchronises serial response frames; [#8447](https://github.com/zeroclaw-labs/zeroclaw/pull/8447) shares protocol parsing with ESP32 firmware.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal underlying needs for better channel integration, security hardening, and workflow flexibility:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) *(closed)* | 14 | ZeroClaw does not know it can add a cron job – users expect autonomic scheduling awareness. |
| [#8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) *(closed)* | 12 | RFC for supply‑chain signing (hardware PGP, SLSA provenance) – community interest in hardened CI. |
| [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) *(closed)* | 9 | Restore GitHub as a native channel – strong demand for first‑class repo activity monitoring. |
| [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) *(closed)* | 8 | Discord channel `allowed_channels` config – users want finer control over bot scope. |
| [#6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055) *(open)* | 7 | Slack thread history backfill – critical for multi‑turn conversations in threaded channels. |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) *(open)* | 7 | Workspace‑relative forbidden path patterns and `.zeroclawignore` – users need to protect sensitive workspace files. |
| [#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127) *(open)* | 6 | RFC for a `KeySource` trait to classify master‑key material – foundational for secret management. |

## 5. Bugs & Stability

Several bugs were reported or actively discussed in the last 24 hours. Ranked by severity:

| Issue | Severity / Priority | Summary | Fix PR exists? |
|-------|---------------------|---------|----------------|
| [#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505) | **P1** – S1 blocked | Telegram channel cannot be configured; `channels doctor` claims not set up. | Not directly |
| [#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559) | **P1** – S1 blocked | Agents stop work when exiting the web chat window. | In‑progress (status:in‑progress) |
| [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) *(closed)* | **S0** – data loss | `reasoning_content` not passed in tool‑call loops with Xiaomi thinking models. | Closed as fixed? (resolution:completed) |
| [#6558](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) *(closed)* | **S0** – data loss | Custom API provider 405 error for DashScope. | Closed |
| [#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002) | **S1** – blocked | Telegram messages not clearly addressed to assistant in local LLM setup. | Needs‑author‑action, stale |
| [#6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724) | **P3** – high risk | Empty Signal/Voice channel credentials cause crashloop of supervisor. | Accepted, no PR yet |
| [#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911) | **P2** – medium | install.sh selects generic Linux binary on Android/Termux. | Accepted |

Notable fix PRs updated today: [#9090](https://github.com/zeroclaw-labs/zeroclaw/pull/9090) (tool‑call pairing), [#9113](https://github.com/zeroclaw-labs/zeroclaw/pull/9113) (streaming HTTP client idling), [#9110](https://github.com/zeroclaw-labs/zeroclaw/pull/9110) (timing‑safe Lark token check), [#9157](https://github.com/zeroclaw-labs/zeroclaw/pull/9157) (serial response frame resync).

## 6. Feature Requests & Roadmap Signals

The most requested features under active discussion or accepted:

| Issue | Feature | Likelihood for next version |
|-------|---------|---------------------------|
| [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) | GitHub native channel | Likely – accepted, high community interest. |
| [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) | Discord `allowed_channels` | Very likely – accepted, resolution:completed indicates done. |
| [#6055](https://github.com/zeroclaw-labs/zeroclaw/issues/6055) | Slack thread history backfill | Likely – in‑progress, accepted. |
| [#7759](https://github.com/zeroclaw-labs/zeroclaw/issues/7759) | Decouple WebSocket lifetime from turn | In‑progress, high risk – probable for next stable release. |
| [#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) | OpenRouter model fallbacks | Blocked, but high demand – may unblock soon. |
| [#8600](https://github.com/zeroclaw-labs/zeroclaw/issues/8600) | Per‑chat model switching | Accepted – could land soon. |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | Workspace‑relative forbidden paths | Blocked, needs‑author‑action – possible for later release. |
| [#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) | Installing skills from `.well-known` URI | Accepted – could be part of the plugin ecosystem push. |

## 7. User Feedback Summary

**Pain points expressed:**

- **Telegram channel setup is brittle** – users report the bot doesn’t answer on Telegram even after following quickstart, and `channels doctor` gives false negatives ([#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505), [#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002)).
- **Agent task cancellation is too aggressive** – leaving the web chat window kills in‑flight agent turns ([#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)).
- **Context overflow leads to hallucination** – long conversations drift off‑topic ([#6517](https://github.com/zeroclaw-labs/zeroclaw/issues/6517), closed but still a concern).
- **Installation on non‑standard platforms (Android/Termux)** is broken ([#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911)).
- **Users want more natural interaction** – agents should know about their own capabilities (cron, scheduling) without being explicitly told ([#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)).

**Satisfaction signals:**

- The community is actively contributing both bug reports and well‑structured RFCs (e.g., [#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127), [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)).
- Many enhancement requests have been accepted and are in‑progress, indicating maintainer responsiveness.
- The hardware support (ESP32, Pico, Nucleo) is being actively improved, with shared protocol crates and serial frame fixes.

## 8. Backlog Watch

The following issues and PRs have remained open for a longer period and either need maintainer attention or lack recent community input:

| Item | Status | Concern |
|------|--------|---------|
| [#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002) (Telegram addressing) | Stale, needs‑author‑action | No response from author since July 18; blocks S1 workflow. |
| [#6724](https://github.com/zeroclaw-labs/zeroclaw/issues/6724) (Signal/Voice crashloop) | Accepted, open since May 16 | High‑risk bug with no fix PR yet. |
| [#8138](https://github.com/zeroclaw-labs/zeroclaw/issues/8138) (OpenRouter fallback) | Blocked | No progress since June 22, despite high community interest. |
| [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) (Air‑gapped mode RFC) | Blocked | Open

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*