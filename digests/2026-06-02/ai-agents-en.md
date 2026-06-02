# OpenClaw Ecosystem Digest 2026-06-02

> Issues: 463 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-02 02:52 UTC

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

# OpenClaw Project Digest – 2026-06-02

## Today's Overview
OpenClaw remains in a period of intense maintenance and rapid iteration. Over the last 24 hours, **463 issues** were updated (298 open, 165 closed) and **500 pull requests** were touched (396 open, 104 merged/closed). Two new beta releases (v2026.6.1-beta.1 and v2026.6.1-beta.2) were cut, both focused on improving runtime reliability for agents, CLI backends, and channel delivery. While many bug reports carry P1 severity—especially around Codex runtime stalls, session duplication, and OAuth compaction—the project is also actively landing fixes and gathering community input on feature requests such as native local model support and Telegram bot‑to‑bot capabilities. Overall, activity is high and the project is healthily responsive, though several long‑standing issues remain in the backlog.

## Releases
- **v2026.6.1-beta.2** – Agents and CLI‑backed runtimes recover more cleanly from interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries. Channels and mobile delivery are steadier across Telegram, WhatsApp, and iMe.
- **v2026.6.1-beta.1** – Same core improvements as beta.2, with the additional mention of iMessage and Slack in the channel stability improvements.

No breaking changes or explicit migration notes have been published; these are incremental beta releases.

## Project Progress
Of the 104 closed/merged PRs in the last 24 hours, several stand out:
- [openclaw/openclaw#77894](https://github.com/openclaw/openclaw/pull/77894) – **fix(memory): preserve phase signal store on read errors** – Prevents accidental loss of dreaming‑phase signals.
- [openclaw/openclaw#87641](https://github.com/openclaw/openclaw/pull/87641) – **Closed** – Multi‑turn rejection against `opencode-go/kimi-k2.6` resolved.
- [openclaw/openclaw#88499](https://github.com/openclaw/openclaw/pull/88499) – **Closed** – `openai‑responses` provider 404 on `previous_response_id` when `store=false` fixed.
- [openclaw/openclaw#87072](https://github.com/openclaw/openclaw/pull/87072) – **Open but ready for maintainer look** – Feat(telegram): opt‑in interleaved progress lane for reasoning events.

Numerous smaller dependency bumps (Dependabot) and documentation updates also moved forward.

## Community Hot Topics
These issues attracted the most discussion and reactions:

1. **[openclaw/openclaw#80171](https://github.com/openclaw/openclaw/issues/80171)** – *Codex‑vs‑Pi runtime parity QA harness (RFC + tracking)*  
   **15 comments, 👍1** – Closed but highly referenced. The community is actively tracking the gap between the two runtimes, especially token efficiency.

2. **[openclaw/openclaw#80380](https://github.com/openclaw/openclaw/issues/80380)** – *Feature: update to Gemini 3.1 Flash‑Lite GA*  
   **14 comments, 👍4** – Users are eager for the switch from preview to stable. Likely to land in the next minor release.

3. **[openclaw/openclaw#88838](https://github.com/openclaw/openclaw/issues/88838)** – *Track core session/transcript SQLite migration via accessor seam*  
   **12 comments, 👍1** – A maintainer‑led planning issue to avoid a risky monolithic rewrite. Signals a major architectural shift ahead.

4. **[openclaw/openclaw#84038](https://github.com/openclaw/openclaw/issues/84038)** – *doctor --fix silently migrates config, breaking PI+OAuth runtime and causing 3–4× token inflation*  
   **12 comments, 👍3** – A critical regression that highlights the tension between the two runtimes and the need for better migration tooling.

**Underlying need:** Users are increasingly adopting the Codex runtime but encountering tool‑call reliability, token cost, and authentication issues. There is a strong desire for parity between Codex and Pi, and for safer automated migrations.

## Bugs & Stability
Several high‑impact regressions were reported or updated today. Listed in descending severity:

- **P1: Codex turn‑completion stall** ([openclaw/openclaw#88312](https://github.com/openclaw/openclaw/issues/88312)) – Multi‑tool agent turns reliably fail with *“Codex stopped before confirming the turn was complete”* on 2026.5.27. No fix PR yet.  
- **P1: Codex‑backed Telegram timeouts** ([openclaw/openclaw#87744](https://github.com/openclaw/openclaw/issues/87744)) – Turns never reach `turn/completed`, blocking final answers.  
- **P1: Agent repeats identical replies on Telegram** ([openclaw/openclaw#86519](https://github.com/openclaw/openclaw/issues/86519)) – Duplicate responses after 2026.5.20, partially mitigated but not fully fixed.  
- **P1: Isolated cron self‑conflicts** ([openclaw/openclaw#88369](https://github.com/openclaw/openclaw/issues/88369)) – `EmbeddedAttemptSessionTakeoverError` on 2026.5.28.  
- **Critical crash: Feishu dispatch TypeError** ([openclaw/openclaw#88234](https://github.com/openclaw/openclaw/issues/88234)) – `Cannot read properties of undefined (reading 'run')` on private message dispatch.  
- **Session‑selected model in fallback list** ([openclaw/openclaw#88039](https://github.com/openclaw/openclaw/issues/88039)) – regression causing incorrect fallback behavior.  
- **Feishu DM session rebuild races** ([openclaw/openclaw#87938](https://github.com/openclaw/openclaw/issues/87938)) – Duplicate keys and maintenance pruning after gateway restart.

**Fix PRs in flight:**  
- [openclaw/openclaw#89290](https://github.com/openclaw/openclaw/pull/89290) – Keep Codex waiting after raw reasoning progress (addresses the stall).  
- [openclaw/openclaw#89287](https://github.com/openclaw/openclaw/pull/89287) – Verify completion delivery target (tightens ACP delivery accounting).  
- [openclaw/openclaw#89285](https://github.com/openclaw/openclaw/pull/89285) – Hide tool failure details in public channels.  
- [openclaw/openclaw#89027](https://github.com/openclaw/openclaw/pull/89027) – Prevent `empty_response` failover for thinking‑only turns.  
- [openclaw/openclaw#89038](https://github.com/openclaw/openclaw/pull/89038) – Skip setup‑only channel plugins on QQbot reconnection.  
- [openclaw/openclaw#89289](https://github.com/openclaw/openclaw/pull/89289) – Aggregate archived session usage.  
- [openclaw/openclaw#89288](https://github.com/openclaw/openclaw/pull/89288) – Prune stale session cleanup archives.

## Feature Requests & Roadmap Signals
Several enhancement requests gained traction today:

- **[openclaw/openclaw#80380](https://github.com/openclaw/openclaw/issues/80380)** – Switch to Gemini 3.1 Flash‑Lite GA (4👍). Likely to be included in the next stable release.
- **[openclaw/openclaw#79077](https://github.com/openclaw/openclaw/issues/79077)** – Support Telegram bot‑to‑bot and guest‑bot modes (7👍). A popular request after Telegram’s May 2026 platform update.
- **[openclaw/openclaw#89265](https://github.com/openclaw/openclaw/issues/89265)** – More local providers – treat local models as first‑class citizens. Reflects the broader trend toward self‑hosted AI.
- **[openclaw/openclaw#78308](https://github.com/openclaw/openclaw/issues/78308)** – Channel‑mediated approval for MCP tool calls (consent envelope). Security‑focused, likely to appear in a mid‑June release.
- **[openclaw/openclaw#79458](https://github.com/openclaw/openclaw/issues/79458)** – i18n for slash‑command descriptions – important for international users.
- **[openclaw/openclaw#35203](https://github.com/openclaw/openclaw/issues/35203)** – Multi‑agent collaboration enhancement (RFC) – a longer‑term roadmap item.

**Prediction:** The Gemini GA switch and the Telegram bot‑to‑bot feature have strong community backing and relatively clear implementation paths; both could land in v2026.6.x stable.

## User Feedback Summary
Users are expressing mixed satisfaction:

- **Positive:** The new beta releases are perceived as stabilizing channels and handling tool‑interruption cleanup. Several users noted improved Telegram delivery (though duplicates persist).
- **Frustrations:**  
  - OAuth compaction failures and token inflation (especially with Codex) remain top pains.
  - Session duplication and timeouts on Telegram and Feishu are eroding trust in reliability.
  - The `doctor --fix` migration that silently breaks PI+OAuth setups has caused significant disruption.
  - Webchat’s cache‑killing per‑message agent runs frustrate users relying on prompt caching.

Overall, the community is engaged and contributing detailed bug reports, but stability regressions are taking a toll on user experience.

## Backlog Watch
Several longstanding issues and PRs remain open without recent maintainer movement:

- **[openclaw/openclaw#51871](https://github.com/openclaw/openclaw/issues/51871)** – *(March 2026)* Cron jobs not displayed in dashboard – P2, closed but unresolved for months.
- **[openclaw/openclaw#42820](https://github.com/openclaw/openclaw/issues/42820)** – *(March 2026)* Feishu send action polluted by poll schema – P1, open with linked PR but stalled.
- **[openclaw/openclaw#44870](https://github.com/openclaw/openclaw/issues/44870)** – *(March 2026)* Cannot verify Codex from transfer station – P2, no recent activity.
- **[openclaw/openclaw#63685](https://github.com/openclaw/openclaw/issues/63685)** – *(April 2026)* Cannot run Gemma 4 from Google AI Studio – P2, awaiting maintainer.
- **[openclaw/openclaw#75767](https://github.com/openclaw/openclaw/issues/75767)** – *(May 2026)* Gateway restart hangs on macOS with SMB mounts – P2, needs‑live‑repro.
- **[openclaw/openclaw#65301](https://github.com/openclaw/openclaw/pull/65301)** – *(April 2026)* Fix/send poll intent detection – P1, marked `needs proof` for months.
- **[openclaw/openclaw#75961](https://github.com/openclaw/openclaw/pull/75961)** – *(May 2026)* Discord slash command deploy – large PR, needs proof.
- **[openclaw/openclaw#83988](https://github.com/openclaw/openclaw/pull/83988)** – *(May 2026)* TTS text settlement fix – telegrams visible proof required.

These items would benefit from maintainer prioritization to avoid accumulating technical debt and user frustration.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Personal Assistant Open-Source Ecosystem

## June 2, 2026

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing an intense period of maturation, with every major project shipping multiple fixes and features daily while racing toward production reliability. Activity levels range from hyperactive (500+ PRs/day) to dormant, signaling a bifurcation between core reference implementations and specialized forks. Three dominant themes emerge across all active projects: **multi-channel delivery stabilization** (Telegram, Discord, QQ, Feishu), **runtime parity between inference engines** (Codex vs. Pi, legacy vs. Reborn), and **cost optimization** (token minimization, provider fallback, skill compilation). The ecosystem is transitioning from experimental to operational, with users demanding production-grade reliability, configuration persistence, and clear migration paths. Overall health is strong but fragmented, as the community navigates architectural debt while expanding feature surfaces.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Today | Health Score | Primary Focus |
|---------|---------------|-------------|---------------|--------------|---------------|
| **OpenClaw** | 463 (298 open, 165 closed) | 500 (396 open, 104 merged) | v2026.6.1-beta.1, beta.2 | ⚠️ **High intensity / regressions** | Core runtime parity, channel stabilization |
| **Hermes Agent** | 50 (33 open, 17 closed) | 50 (28 open, 22 merged) | None | ✅ **High activity, responsive** | Kanban, cron resilience, MCP robustness |
| **ZeroClaw** | 36 (28 open, 8 closed) | 37 (24 open, 13 merged) | None | ✅ **High activity, focused** | v0.8.0 integration, email/Discord/ eval harness |
| **CoPaw** | 50 (42 open, 8 closed) | 34 (25 open, 9 merged) | v1.1.10, v1.1.10-beta.2 | ✅ **High activity, releasing** | Sub-agents, cron bugs, AgentScope 2.0 migration |
| **NanoBot** | 29 (4 open, 25 closed) | 31 (14 open, 17 merged) | v0.2.1 | ✅ **Very healthy, fast closure** | WebUI workbench, DingTalk, local whisper |
| **IronClaw** | 12 (11 open, 1 closed) | 46 (14 open, 32 merged) | None | ✅ **Intense dev / E2E caution** | Reborn architecture, OAuth, budgets |
| **LobsterAI** | 1 (1 open) | 50 (0 open, 50 merged) | v2026.6.1 | ✅ **Shipping fast** | Expert Kit Store, plugin updates, UX polish |
| **ZeptoClaw** | 1 (1 new open) | 18 (1 open, 17 merged) | None | ✅ **Stable maintenance** | Binary-size gate, advisory clearing, provider fix |
| **PicoClaw** | 7 (all open) | 11 (6 open, 5 merged) | Nightly v0.2.9-nightly | ⚠️ **Moderate, backlog risks** | Bedrock fix, cron tool, SC3Bot channel |
| **NanoClaw** | 3 (2 new open, 1 closed) | 6 (5 open, 1 merged) | None | ⚠️ **Low activity, critical bugs** | A2A routing fix, crash-loop transcript bug |
| **Moltis** | 0 | 3 (all merged) | None | ✅ **Quiet, stable** | Provider capabilities, NEAR AI, Codex compat |
| **NullClaw** | 0 | 1 (open) | None | ✅ **Very quiet** | Telegram typing indicator fix |
| **TinyClaw** | 0 | 0 | None | ⚠️ **Dormant** | No activity |

**Health Score Legend:** ✅ = healthy cadence with responsiveness; ⚠️ = active but with regressions, unresolved critical bugs, or backlog accumulation.

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale:** 463 issues + 500 PRs in 24 hours—dwarfs the next largest project (Hermes/ZeroClaw at ~50 each). OpenClaw is the strategic reference implementation, with the broadest contributor base and integration surface.
- **Channel coverage:** Explicitly targeting Telegram, WhatsApp, iMessage, Slack, iMe, Feishu—more delivery backends than any peer.
- **Two-runtime architecture:** The Codex-vs-Pi runtime parity project (#80171) is unique; no other project has built two independent agent loops and is methodically closing the gap.
- **Release velocity:** Two betas shipped today, demonstrating operational agility despite volume.

**Technical Approach Differences:**
- **Session/SQLite migration via accessor seam** (#88838) signals a planned architectural decomp risk—OpenClaw is proactively avoiding monolithic rewrites, unlike IronClaw's "Reborn" full redesign.
- **OAuth compaction** (#84038) and `doctor --fix` migration bugs reveal a tension between power-user tooling and runtime stability that peers are not yet handling at scale.

**Community Comparison:**
- OpenClaw's community is the most vocal (highest issue volume, most reactions) but also the most frustrated (P1 regressions, token inflation, session duplication).
- Hermes Agent has stronger user engagement on specific features (multi-role routing, MongoDB memory) with fewer complaints.
- NanoBot's community is the most self-sufficient: 17 new contributors in v0.2.1, fast issue closure (86% closed in 24h).
- ZeroClaw's community is actively building the future (WIT files, eval harness) rather than firefighting.

**Verdict:** OpenClaw is the ecosystem's center of gravity but carries the highest operational debt. Peer projects are more stable per-commit, but none match OpenClaw's breadth.

---

## 4. Shared Technical Focus Areas

These requirements emerge as cross-cutting patterns across multiple projects, indicating ecosystem-wide priorities:

| Focus Area | Projects Affected | Specific Needs |
|------------|-------------------|----------------|
| **Reliability: Codex / stream / turn-completion stalls** | OpenClaw, Hermes, ZeroClaw | Tool-call hang detection, `turn/completed` delivery guarantees, stream fallback paths |
| **Cost optimization: token waste from skill injection** | OpenClaw, ZeroClaw, PicoClaw, NanoBot | Skill compilation, cached catalogs, heartbeat LLM skip when idle |
| **Stability: cron / scheduled tasks** | OpenClaw, Hermes, CoPaw, NanoBot | Non-dict `cron/jobs.json` crashes, cron sessions sharing user context, ghost jobs, empty traces |
| **Platform-specific: Telegram** | OpenClaw, Hermes, NullClaw, ZeroClaw | Bot-to-bot mode (Telegram May 2026 update), duplicate response fix, typing indicator, scratchpad leak |
| **Platform-specific: Discord** | OpenClaw, Hermes, ZeroClaw | Attachment type validation, timeout on slash sync, silent tool response drops |
| **Platform-specific: QQ / WeCom / Feishu** | NanoBot (Napcat QQ), CoPaw (Feishu), Hermes (WeCom) | Channel integration, group isolation, reconnection races |
| **Provider parity: Gemini, Kimi, Bedrock** | OpenClaw, ZeroClaw, PicoClaw, NanoBot | Temperature deprecation handling, `assistant first turn` invariant, rate limiting |
| **Security: OAuth / credential management** | OpenClaw, ZeroClaw, IronClaw, LobsterAI | Silent migration breaking OAuth, SMTP fallback, bot token refresh |
| **Scalability: multi-agent / session routing** | OpenClaw, Hermes, NanoClaw, CoPaw | A2A session mis-routing, agent-scoped credentials, shared MCP pool |
| **Observability: dashboards / admin panels** | Hermes (Kanban), OpenClaw, ZeroClaw (eval harness) | Executor board, active workers, agent trace replay, system stats |
| **Config persistence: model pages, skill toggles** | CoPaw, PicoClaw, NanoBot | Lost config on session creation, skill disable/enable required (not delete only) |
| **Binary size / footprint** | ZeptoClaw, ZeroClaw | Sub-7MB targets, lean channel bundles |

**Cross-cutting user demand:** *“I want my agent to work reliably across platforms without infinite token bills or silent failures.”*

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | CoPaw | NanoBot | IronClaw | LobsterAI |
|-----------|----------|--------------|----------|-------|---------|----------|-----------|
| **Target user** | Core reference integrators, multi-channel deployers | Mid-scale developers, Discord/WhatsApp users | Advanced users wanting orchestration, eval | Desktop/workspace agents, coding workflows | Hobbyist-to-SMB, low-friction setup | Cloud-native scaling, multi-tenant | Consumer desktop (macOS), Expert Kit Store |
| **Architecture** | Two runtimes (Codex, Pi), SQLite accessor seam | Legacy stable + UI overhaul (Kanban) | Modular, v0.8.0 integration, WASI plugin future | AgentScope 2.0 migration, sub-agent spawning | Full workbench WebUI, event-bus refactor | **Reborn**: stateless, cloud-native rebuild | Electron desktop, npm/clawhub plugin ecosystem |
| **Primary release target** | Beta → stable every week | v0.15.x → v0.16 | v0.8.0 beta → v0.8.1 | v1.1.x → v1.2 | v0.2.x → v0.3 | Reborn integration → RC | v2026.6.x |
| **Key innovation** | Codex/Pi parity framework, Telegram bot-to-bot | Kanban dashboard, multi-role auto-routing | Agent evaluation harness, WIT plugin interfaces | `spawn_subagent` tool, Open Directory tab | Local whisper, WebUI inline edit, Napcat QQ | Cost-based budgets, EventStreamManager, GSuite OAuth | Expert Kit Store, thinking level controls |
| **Risk profile** | Operational debt from scale | Regressions in CDP, Discord | P1 Gemini/Ollama bugs unresolved | Windows resource leaks, AgentScope migration risk | Few critical bugs, fast closure | Nightly E2E failure, compaction bugs | Subscription credit trust issue |
| **Community modeling** | Large, vocal, mixed satisfaction | Engaged, contributor batch merges | Forward-looking, building infrastructure | Active skill proposals, dedicated Windows reports | Self-sufficient, many new contributors | Core dev team, external interest growing | Silent users, low issue volume |
| **Platform strength** | Broadcast spectrum (7+ channels) | Discord, WhatsApp, Docker | Email, Gemini, Discord, Jina AI | Desktop, Tauri, Coding Mode | DingTalk, Telegram, Napcat (QQ) | GSuite, Slack, GitHub, Feishu | macOS native, IM bot management |

**Key insight:** There is no "winner"—projects are carving niches. OpenClaw owns breadth and community gravity. Hermes and ZeroClaw lead in reliability infrastructure. CoPaw and LobsterAI own desktop/consumer UX. IronClaw is the ambitious cloud-native bet.

---

## 6. Community Momentum & Maturity

### Tier 1: Hyperactive / Rapid Growth
- **OpenClaw** – Ecosystem leader, highest absolute volume, but stability oscillations.
- **Hermes Agent** – Healthy merge cadence, batch fixes, Kanban signals platform ambition.
- **ZeroClaw** – Fast bug closure, community building eval harness and WIT plugins—mature for v0.8.
- **CoPaw** – Shipping releases daily, sub-agent tool is a genuine innovation. High satisfaction.

### Tier 2: Healthy / Feature Delivery
- **NanoBot** – Highest closure rate (86% of issues closed), best contributor onboarding. Model of sustainable development.
- **LobsterAI** – Polished consumer product with store. Lowest issue volume suggests stable user base.
- **IronClaw** – Intense dev (46 PRs) but nightly E2E failure and compaction bugs indicate pre-release friction.

### Tier 3: Stable / Maintenance
- **PicoClaw** – Nightly builds, moderate backlog (exec tool bug open 90 days). Healthy but needs leader attention.
- **ZeptoClaw** – Minimal activity but targeted: provider fix, binary gate, advisory clearing. Efficient.
- **NanoClaw** – Small team, critical bugs fixed (A2A routing) but new crash-loop bug emerged. Growing pains.
- **Moltis** – Quiet, stable. PRs close without discussion. Likely small user base.
- **NullClaw** – Single open PR. Near-dormant but attentive to Telegram fixes.

### Tier 4: Dormant
- **TinyClaw** – No activity. Potential abandonment or full stability.

### Trend: Consolidation Phase
Projects are converging on similar fixes (cron, token cost, Telegram) while diverging architecturally (IronClaw's Reborn vs. OpenClaw's accessor seam vs. ZeroClaw's WASI). The market is signaling that **reliable multi-platform delivery + cost visibility** are table stakes; differentiation will come from **evaluation tooling, plugin ecosystems, and cloud-native scaling**.

---

## 7. Trend Signals

**1. The "Invisible Infrastructure" Demand is Real**
Across every active project, users want agents to work **without constant intervention**:
- ZeroClaw's #5962 (Ollama tool failures block workflows for weeks)
- CoPaw's #4888 (Dream agent overwriting shared MEMORY.md)
- OpenClaw's #88312 (Codex stall)
These aren't feature requests—they are reliability demands. **The ecosystem is learning that AI agents must be more trustworthy than typical web apps.**

**2. Token Costs are the #1 Silent Killer**
Every project except NullClaw has at least one cost-minimization issue:
- OpenClaw: token inflation from OAuth migration
- ZeroClaw: skill compilation (#5146)
- NanoBot: heartbeat LLM skip, skill tool usage reduction
- PicoClaw: catalog caching
The market is realizing that naive "send all skills every turn" is financially unsustainable at scale. **Skill compilation and prompt budgets will be mandatory within 6 months.**

**3. Multi-Platform is No Longer Optional**
Telegram

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-02

## 1. Today's Overview

NanoBot is in a highly active maintenance and feature development phase. In the last 24 hours, 29 issues were updated (25 closed) and 31 pull requests were touched (17 merged/closed), indicating strong community engagement and rapid resolution of reported problems. A new minor release **v0.2.1** was published, emphasizing WebUI improvements for a more productive interaction surface. The project shows healthy momentum with multiple concurrent contributions across channels, tools, and stability fixes.

## 2. Releases

### v0.2.1

- **84 PRs merged** since last release, **17 new contributors**
- **Headline feature**: WebUI becomes a full workbench — live file edits now appear as activity, tool traces render more clearly, and the chat surface is smoother and faster.
- No breaking changes or migration notes were announced.

[[Release details]](https://github.com/HKUDS/nanobot/releases/tag/v0.2.1)

## 3. Project Progress

**17 PRs merged/closed** in the last 24 hours. Key advancements:

| PR # | Title | Status | Impact |
|------|-------|--------|--------|
| [#4016](https://github.com/HKUDS/nanobot/pull/4016) | feat(dingtalk): add group_user_isolation to separate sessions per user | Merged | Resolves cross-user context contamination in DingTalk group chats |
| [#3723](https://github.com/HKUDS/nanobot/pull/3723) | Local whisper transcription via faster-whisper | Merged | Enables offline voice transcription without API keys |
| [#4135](https://github.com/HKUDS/nanobot/pull/4135) | Refactor WebUI runtime state onto event bus | Merged | Decouples WebUI from core loop, improves testability |
| [#4143](https://github.com/HKUDS/nanobot/pull/4143) | Refactor session retention result | Merged | Returns structured `RetentionResult` for clearer archive semantics |
| [#4124](https://github.com/HKUDS/nanobot/pull/4124) | fix(provider): handle XML tool call emissions from mimo/glm models | Merged | Prevents raw XML leaking into chat channels and server errors with certain models |
| [#3126](https://github.com/HKUDS/nanobot/pull/3126) | keep cron runs silent until final output | Merged | Reduces noise from scheduled tasks by suppressing intermediate messages |
| [#2482](https://github.com/HKUDS/nanobot/pull/2482) | skip heartbeat LLM call when HEARTBEAT.md has no active tasks | Merged | Saves tokens by avoiding unnecessary LLM calls |
| [#3509](https://github.com/HKUDS/nanobot/pull/3509) | feat(channels): Add Napcat (QQ) channel | Merged | Provides OneBot v11 Forward WebSocket support for QQ private/group chat |

## 4. Community Hot Topics

The most discussed issues (by comments) reveal two central pain points:

- **[#2880](https://github.com/HKUDS/nanobot/issues/2880)** (18 comments, closed) — All messages return an error; user reports “无论发什么消息都回复报错”. This was a high-severity bug affecting normal operation, now resolved in `v0.15`? (issue tagged “stale” but closed).
- **[#1932](https://github.com/HKUDS/nanobot/issues/1932)** (8 comments, closed) — Feature request for skill disable/enable toggle instead of only delete. Users want flexible configuration without losing skill definitions.
- **[#101](https://github.com/HKUDS/nanobot/issues/101)** (6 comments, closed) — Interest in using free APIs (Google, Grok) as defaults instead of OpenRouter. Underlying need: reducing operational costs.

The active PR [#4146](https://github.com/HKUDS/nanobot/pull/4146) (Napcat QQ channel, backported from #3509) is likely to generate continued discussion as QQ is a major platform.

## 5. Bugs & Stability

**Critical:**

- **[#4006](https://github.com/HKUDS/nanobot/issues/4006)** (open) — Orphaned tool results in conversation history after tool_call_id fix. Breaks API compatibility with strict providers (OpenAI, Anthropic). *No fix PR yet.*
- **[#4133](https://github.com/HKUDS/nanobot/issues/4133)** (closed) — Agent completes tool calls but final response never delivered to Telegram. Persisted after previous fix (#4080). *Closed with investigation ongoing likely.*
- **[#4128](https://github.com/HKUDS/nanobot/issues/4128)** (closed) — `retain_recent_legal_suffix` bug causes duplicate archiving of user messages, leading to LLM context inconsistency. *Fix included in PR #4129 (merged).*
- **[#3633](https://github.com/HKUDS/nanobot/issues/3633)** (closed) — GPT model returns “Duplicate item found with id” error, causing agent loop to hang. *Likely fixed.*

**Moderate:**

- **[#4069](https://github.com/HKUDS/nanobot/issues/4069)** (closed) — Dream cron job registered without enable/manual-memory gate – could cause unintended runs. *Fixed.*

**New fix PRs today:**

- [#4147](https://github.com/HKUDS/nanobot/pull/4147) — Serialize cursor allocation in `append_history` to prevent duplicate messages (closes #4081).
- [#4145](https://github.com/HKUDS/nanobot/pull/4145) — Resolve issue #3958 for the Weather Skill (still open? but PR submitted).

## 6. Feature Requests & Roadmap Signals

**New feature requests** (all from June 1–2):

| Issue/PR | Request | Likelihood for next release |
|----------|---------|------------------------------|
| [#4132](https://github.com/HKUDS/nanobot/issues/4132) | Support custom image generation provider (e.g., Agnes AI) | Medium – aligns with existing provider extensibility |
| [#4138](https://github.com/HKUDS/nanobot/pull/4138) | Add `tools.file.enable` toggle to disable built-in filesystem tools | High – already a PR, consistent with `exec`/`web` pattern |
| [#4142](https://github.com/HKUDS/nanobot/issues/4142) | Optimize API costs for cache-miss input tokens (DeepSeek V4, etc.) | High – cost saving is a recurring community theme |
| [#4146](https://github.com/HKUDS/nanobot/pull/4146) | Add Napcat (QQ) channel | Very high – already merged in branch, being backported to main |
| [#4148](https://github.com/HKUDS/nanobot/pull/4148) | WebUI inline edit button for sent messages | High – improves UX directly |

**Predictions for v0.3.0:**  
- Custom image generation providers, file tool toggling, cost optimizations for input tokens, and QQ channel support.

## 7. User Feedback Summary

**Pain Points (expressed in issues):**
- “无论发什么消息都回复报错” (#2880) – all messages error out (now fixed).
- “技能不支持禁用，只能删除” (#1932) – lack of toggle for skills frustrates dynamic configuration.
- “心跳触发时重复创建了定时任务” (#3028) – heartbeat duplicates cron tasks, causing spam.
- “Cron tasks send intermediate thinking messages” (#3064) – noise from scheduled tasks, now partially fixed by #3126.
- “Heartbeat LLM call wastes tokens when no tasks” (#2406) – addressed by #2482/#2435.

**Satisfaction Indicators:**
- High issue closure rate (25 of 29 closed today).
- Active contributions from 17 new contributors in v0.2.1.
- Users propose and implement features themselves (e.g., Napcat channel, local whisper, Volcengine search provider).

**Underlying Needs:**
- **Cost control** (token waste, free API support).
- **Configurability** (skill toggle, file tool enable/disable).
- **Reliability** (message delivery, duplicate handling, MCP reconnection).

## 8. Backlog Watch

Most issues are being triaged quickly. A few items that may need attention:

- **[#4006](https://github.com/HKUDS/nanobot/issues/4006)** (open, orphaned tool results) – no fix PR yet; critical for API compliance.
- **[#4136](https://github.com/HKUDS/nanobot/issues/4136)** (open, refactor session retention result) – addressed by PR #4143, but still open for further discussion.
- **[#4142](https://github.com/HKUDS/nanobot/issues/4142)** (open, cost optimization) – still in discussion, no PR.
- **[#4122](https://github.com/HKUDS/nanobot/pull/4122)** (open, WebUI recording + local ASR) – might need maintainer review to decide on merge.

No long-abandoned issues were identified; the project team is clearly responsive.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent – Project Digest for 2026-06-02

## 1. Today’s Overview

Hermes Agent is experiencing **very high activity**, with **50 issues and 50 PRs updated in the last 24 hours**. Of those, **33 issues remain open/active** and **28 PRs are still open**, indicating a steady stream of bug fixes and feature work. **17 issues were closed** and **22 PRs were merged/closed**, reflecting a healthy merge cadence. **No new releases** were published today. The project is clearly in an intense development phase, with notable attention to stability (cron, MCP, gateway), platform support (WhatsApp, WeCom, Discord), and the upcoming Kanban orchestration dashboard.

## 2. Releases

*No new releases today.* The last known version is **v0.15.1** (2026-05-29), referenced in several bug reports.

## 3. Project Progress

**22 PRs merged/closed today.** Key advancements and fixes include:

- **Cron subsystem resilience** – [#37065](https://github.com/NousResearch/hermes-agent/pull/37065) fixes a crash when `cron/jobs.json` contains non-dict JSON; [#37066](https://github.com/NousResearch/hermes-agent/pull/37066) and [#37139](https://github.com/NousResearch/hermes-agent/pull/37139) fix WhatsApp `dm_policy`/`group_policy` not being honored.
- **MCP robustness** – Three PRs ([#36064](https://github.com/NousResearch/hermes-agent/pull/36064), [#36058](https://github.com/NousResearch/hermes-agent/pull/36058), and the merged combination [#37133](https://github.com/NousResearch/hermes-agent/pull/37133)) let misconfigured HTTP MCP endpoints fail fast (<1 s) instead of hanging for the full 60 s timeout.
- **Batch of small fixes** – [#37146](https://github.com/NousResearch/hermes-agent/pull/37146) (merged) bundles 8 surgical fixes from @kyssta-exe, covering web API error codes, file descriptor hygiene, and more.
- **Gateway and platform fixes** – [#37069](https://github.com/NousResearch/hermes-agent/pull/37069) fixes WeCom `ALLOWED_USERS` env variable being ignored; [#37147](https://github.com/NousResearch/hermes-agent/pull/37147) fixes the `doctor` command’s home directory lookup.
- **TUI cleanups** – [#37112](https://github.com/NousResearch/hermes-agent/pull/37112) removes the duplicate `/provider` command and unifies the Sessions overlay.
- **Dashboard admin panel** – [#36736](https://github.com/NousResearch/hermes-agent/pull/36736) (open) is a comprehensive addition of MCP catalog, toggles, hook creation, and system stats to the admin UI.

## 4. Community Hot Topics

The most engaged discussions (by comments or reactions) reveal clear community desires:

- **Multi-role auto-routing** – [#5143](https://github.com/NousResearch/hermes-agent/issues/5143) (14 👍, 5 comments) is a v2 proposal for contextual classification and misroute recovery, adapted to v0.14.0 architecture. High demand.
- **MongoDB memory provider** – [#5495](https://github.com/NousResearch/hermes-agent/issues/5495) (1 👍, 3 comments) requests an official MongoDB-backed memory store; it was **closed today** (likely as “wontfix” or already addressed?).
- **Gemini Flex Inference** – [#12700](https://github.com/NousResearch/hermes-agent/issues/12700) (6 👍, 2 comments) asks for `service_tier: "flex"` support for cost savings on background tasks.
- **WebSocket rejection** – [#35322](https://github.com/NousResearch/hermes-agent/issues/35322) (7 comments) describes a bug where WebSocket upgrades fail when the dashboard is bound to `0.0.0.0` with `--insecure`. Closed as duplicate.
- **No auxiliary LLM provider configured** – [#10149](https://github.com/NousResearch/hermes-agent/issues/10149) (16 👍, 1 comment) is a confusing warning message; it was closed, indicating a fix or documentation update.

**Underlying need**: Users want better observability, configuration flexibility, and support for multi-profile/multi-backend setups. The high reaction count on `#10149` and `#5143` shows that configuration friction and complex routing are key pain points.

## 5. Bugs & Stability

Several new bug reports were filed or updated today, ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **P1** (critical) | [#36867](https://github.com/NousResearch/hermes-agent/issues/36867) (closed) | Non-dict `cron/jobs.json` crashes entire cron subsystem. | ✅ Fixed by [#37065](https://github.com/NousResearch/hermes-agent/pull/37065) |
| **P1** (critical) | [#36208](https://github.com/NousResearch/hermes-agent/issues/36208) (closed) | Docker container fails to start from v2026.5.28. | Closed without explicit fix PR, but likely resolved. |
| **P1** (critical) | [#29346](https://github.com/NousResearch/hermes-agent/issues/29346) (closed) | Discord silently drops tool-using responses. | Closed, fixed previously. |
| **P2** | [#29711](https://github.com/NousResearch/hermes-agent/issues/29711) (open) | Discord attachments with mixed types cause 400 errors for invalid image data URLs. | No PR yet. |
| **P2** | [#36211](https://github.com/NousResearch/hermes-agent/issues/36211) (open) | Chrome CDP DOM operations broken in v0.15.1 (regression from v0.15.0). | None yet. |
| **P2** | [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) (open) | Bedrock+Claude wizard accepts Bearer-only but runtime fails for IAM; region picker broken. | None yet. |
| **P2** | [#19776](https://github.com/NousResearch/hermes-agent/issues/19776) (open) | Discord gateway timeout too short when slash sync >30 s. | None yet. |
| **P2** | [#11665](https://github.com/NousResearch/hermes-agent/issues/11665) (open) | Memory char limits ignored via CLI/MCP dispatch path. | None yet. |
| **P3** | [#36650](https://github.com/NousResearch/hermes-agent/issues/36650) (open) | Benchmark cleanup masks setup failures with `NameError`. | None yet. |
| **P3** | [#37036](https://github.com/NousResearch/hermes-agent/issues/37036) (open) | `skills_guard` false-positive blocks community skill installation. | None yet. |
| **P3** | [#37105](https://github.com/NousResearch/hermes-agent/issues/37105) (closed) | Bedrock static context window incorrectly reports 200K for Claude 4.x (should be 1M). | Closed as fixed? |

**Summary**: The **cron crash** and **Docker regression** were critical and already addressed. The **Discord attachment bug** (#29711) and **Chrome CDP regression** (#36211) are the most pressing open P2 bugs. The **memory char limits** issue (#11665) has been open for over six weeks with no fix.

## 6. Feature Requests & Roadmap Signals

Strong signals for the next release (likely v0.15.2 or v0.16.0):

- **Kanban dashboard enhancements** – Two new issues opened today: [#37109](https://github.com/NousResearch/hermes-agent/issues/37109) (Executor Board active worker panel) and [#37108](https://github.com/NousResearch/hermes-agent/issues/37108) (align dashboard columns with scheduled/review statuses). Combined with the existing umbrella [#35986](https://github.com/NousResearch/hermes-agent/issues/35986), Kanban is clearly a near-term priority.
- **Dashboard admin panel** – PR [#36736](https://github.com/NousResearch/hermes-agent/pull/36736) (open) is feature-complete and likely to land soon.
- **Native audio routing** – PR [#37149](https://github.com/NousResearch/hermes-agent/pull/37149) (open) adds `audio_routing.py` for multimodal models and fixes Feishu. Could appear in the next minor release.
- **Multi-profile shared memory** – RFC [#31388](https://github.com/NousResearch/hermes-agent/issues/31388) (3 comments) is gaining traction; upstreaming is under consideration.
- **Gemini Flex** – [#12700](https://github.com/NousResearch/hermes-agent/issues/12700) (6 👍) is a low-effort addition that could easily land for cron/subagent cost savings.
- **Telegram Managed Bots** – Two PRs ([#10589](https://github.com/NousResearch/hermes-agent/pull/10589) and [#28272](https://github.com/NousResearch/hermes-agent/pull/28272)) are still open after weeks. The Worker API version (#28272) seems closer to merge – may ship together.

**Prediction**: The next version will focus on **Kanban stability and UI**, **MCP resilience** (already merged), and **platform-specific bug fixes** (WhatsApp, WeCom, Discord). Audio routing and admin panel are strong candidates for inclusion.

## 7. User Feedback Summary

- **Configuration frustration**: Users report that working directory settings are not respected (`#11312` closed), `terminal.cwd` not injected into system prompt (`#24882` closed), and “no auxiliary LLM provider” warning confusion (`#10149` closed, 16 👍). These point to a need for clearer configuration validation and better error messages.
- **Platform-specific pain**: Discord users see timeout issues (`#19776`) and silent response drops (`#29346` closed); Bedrock users face auth and region problems (`#28156`); Docker users had startup failures (`#36208` closed). Satisfaction improves when fixes arrive quickly.
- **Regressions cause friction**: The Chrome CDP regression in v0.15.1 (`#36211`) upset an automation user who had to downgrade. Such regressions erode trust.
- **Community contributions valued**: Batch fix PRs from community contributors (e.g., @kyssta-exe) are being merged quickly, indicating a healthy contributor ecosystem.
- **Desired features with strong thumbs-up**: Multi-role routing (14 👍), MongoDB memory (though closed), Gemini Flex (6 👍), and multi-profile memory (RFC). Users want more scalability and cost optimization.

## 8. Backlog Watch

Issues and PRs that have been open for a notable time without maintainer response or resolution:

- **Feature: Multi-role auto-routing** – [#5143](https://github.com/NousResearch/hermes-agent/issues/5143) – Created **2026-04-04** (59 days), 14 👍, updated 2026-06-01. High demand but no assignee or milestone. Risk of stagnation.
- **Feature: Gemini Flex** – [#12700](https://github.com/NousResearch/hermes-agent/issues/12700) – Created **2026-04-19** (44 days), 6 👍. Low complexity; should be actionable.
- **PR: Telegram Managed Bots (original PoC)** – [#10589](https://github.com/NousResearch/hermes-agent/pull/10589) – Created **2026-04-16** (47 days), still open despite a follow-up PR (#28272) that is more recent. Needs a decision.
- **PR: Telegram Managed Bots (Worker API)** – [#28272](https://github.com/NousResearch/hermes-agent/pull/28272) – Created **2026-05-19** (14 days), no maintainer comments visible. A newer alternative may supersede.
- **Bug: Discord timeout too short** – [#19776](https://github.com/NousResearch/hermes-agent/issues/19776) – Created **2026-05-04** (29 days), no assignment.
- **Bug: Memory char limits ignored** – [#11665](https://github.com/NousResearch/hermes-agent/issues/11665) – Created **2026-04-17** (46 days), P2, no fix PR, multiple users affected (2 comments).
- **Feature: Multi-profile shared memory** – [#31388](https://github.com/NousResearch/hermes-agent/issues/31388) – Created **2026-05-24** (9 days), not

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-06-02

## 1. Today's Overview
The project saw **high activity** over the past 24 hours with **7 issues** updated (all still open) and **11 pull requests** updated (6 open, 5 merged/closed). A **nightly build** (`v0.2.9-nightly.20260602.426046fc`) was released automatically, incorporating recent changes from the `main` branch. Community engagement remains robust, particularly around path validation bugs and configuration compatibility for newer Anthropic models. Several important fixes landed today, including a Bedrock temperature deprecation patch and enhancements to the cron tool.

## 2. Releases

**Nightly Build v0.2.9-nightly.20260602.426046fc**  
This is an automated, potentially unstable build. Full changelog: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main).  
- **No breaking changes** explicitly noted, but users should test before deploying in production.  
- The build includes all fixes and features merged to `main` up to the release timestamp.

## 3. Project Progress – Merged/Closed PRs Today
Five pull requests were closed or merged:

- **[PR #2982 – fix(bedrock): drop temperature for models that deprecate it (Opus 4.8)](https://github.com/sipeed/picoclaw/pull/2982) (closed)**  
  Resolves a 400 error on AWS Bedrock when using `claude-opus-4.8` by omitting the deprecated `temperature` field.

- **[PR #2977 – feat(cron): add get and update actions to cron tool](https://github.com/sipeed/picoclaw/pull/2977) (closed)**  
  Allows agents to inspect and partially modify cron jobs without recreating them, reducing unnecessary task removals.

- **[PR #2893 – feat: add Server酱³ Bot (SC3Bot) channel support](https://github.com/sipeed/picoclaw/pull/2893) (closed)**  
  Introduces a new notification channel for the Chinese service Server酱³, supporting both polling and webhook modes.

- **[PR #2890 – fix: resolve symlinks in cwdPath on macOS to fix path validation](https://github.com/sipeed/picoclaw/pull/2890) (closed)**  
  Fixes test failures caused by `/var` → `/private/var` symlink inconsistency on macOS.

- **[PR #2781 – perf: reduce skill catalog token usage on tool iterations and subsequent turns](https://github.com/sipeed/picoclaw/pull/2781) (closed)**  
  Optimises LLM token consumption by caching or suppressing the full skill catalog on intermediate tool calls.

| PR # | Title | Status | Impact |
|------|-------|--------|--------|
| 2982 | fix(bedrock): drop temperature for Opus 4.8 | Merged | Critical for Bedrock users |
| 2977 | feat(cron): add get/update actions | Merged | Improves cron tool flexibility |
| 2893 | feat: Server酱³ Bot channel | Merged | New channel integration |
| 2890 | fix: resolve symlinks on macOS | Merged | Fixes path validation |
| 2781 | perf: reduce skill catalog token usage | Merged | Reduces LLM costs |

## 4. Community Hot Topics

- **[Issue #1042 – exec工具guardCommand方法问题](https://github.com/sipeed/picoclaw/issues/1042)**  
  **15 comments, 2 👍** – Most active issue. The `exec` tool’s `guardCommand` method incorrectly blocks commands like `curl "wttr.in/Beijing?T"` because it misinterprets the URL as a relative path. Users are frustrated by false-positive safety blocks that prevent legitimate tool usage.

- **[Issue #2887 – .deb version on RISC-V not functional with OpenAI model](https://github.com/sipeed/picoclaw/issues/2887)**  
  **8 comments** – A RISC-V user reports that the `.deb` package fails to work with OpenAI models (gpt-5.4). The exact cause is still under discussion; likely build or dependency issue for this architecture.

- **[Issue #2720 – Singleton PID check doesn't verify process identity](https://github.com/sipeed/picoclaw/issues/2720)**  
  **7 comments** – High-priority bug causing crash loops when a stale PID is reused by another process (e.g., `systemd-resolved`). A fix PR (#2813) is open but not yet merged.

- **[Issue #2796 – 历史记录只能查看到最后一条用户消息](https://github.com/sipeed/picoclaw/issues/2796)**  
  **5 comments** – History display only shows the last user message in a multi-message conversation. Users expect all messages to be visible.

**Underlying needs:** Users are demanding better path validation logic, cross-platform reliability (RISC-V), robust singleton process management, and improved UI/UX for conversation history.

## 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR |
|----------|-------|---------|--------|
| **High** | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | Stale PID causes crash loop | [PR #2813](https://github.com/sipeed/picoclaw/pull/2813) (open) |
| **Medium** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` tool guardCommand false positive | None open |
| **Medium** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | .deb on RISC-V incompatible with OpenAI | None yet |
| **Low** | [#2939](https://github.com/sipeed/picoclaw/issues/2939) | `temperature` deprecated for `claude-opus-4-7` | [PR #2940](https://github.com/sipeed/picoclaw/pull/2940) (open) |
| **Low** | [#2941](https://github.com/sipeed/picoclaw/issues/2941) | Default config uses dots instead of hyphens for claude-sonnet-4.6 | [PR #2942](https://github.com/sipeed/picoclaw/pull/2942) (open) |

**New bugs today:**  
- No new bugs were filed today; all updated issues are pre-existing.  
- One new task ([#2981](https://github.com/sipeed/picoclaw/issues/2981)) requests documentation updates for v0.2.9.

**Regression note:** The Bedrock temperature issue (#2982) was fixed and merged today – that was a regression after bumping to Opus 4.8.

## 6. Feature Requests & Roadmap Signals

**Recently merged/closed features:**
- **SC3Bot channel** (#2893) – new notification integration for Chinese users.
- **Cron tool enhancements** (#2977) – `get` and `update` actions make agent cron management more robust.

**Open feature PRs (likely candidates for next release):**
- **[PR #2937 – Agent Collaboration Bus](https://github.com/sipeed/picoclaw/pull/2937)** – Adds per-agent mailboxes and structured inter-agent communication. This is a major architectural change that could appear in v0.3.0.
- **[PR #2917 – NEAR AI Cloud provider](https://github.com/sipeed/picoclaw/pull/2917)** – Integrates a new TEE-capable LLM provider, expanding model choice.
- **[PR #2942 – Fix default claude-sonnet model ID](https://github.com/sipeed/picoclaw/pull/2942)** & **[PR #2940 – Omit temperature for opus-4-7](https://github.com/sipeed/picoclaw/pull/2940)** – Both are config fixes, likely to be merged soon.

**User-requested features from issues:**
- Complete history display (multi-message conversations) – issue #2796.
- Updated documentation for v0.2.9 – issue #2981.

**Prediction:** The next minor release (v0.3.0) may include agent collaboration (if stable), NEAR AI provider, and accumulated config fixes. The cron tool enhancements are already merged.

## 7. User Feedback Summary

**Pain points expressed in issues/PRs:**
- **False-positive security blocks** (#1042) – Users find the `exec` tool’s path guard too aggressive, blocking safe commands like `curl`.
- **Platform-specific failures** (#2887) – RISC-V users cannot use the official `.deb` package with OpenAI models.
- **Configuration friction** (#2939, #2941) – Wrong model IDs and deprecated parameters cause immediate failures on first use.
- **History truncation** (#2796) – Multi-turn conversations lose prior user messages after switching conversations.
- **Crash-loop on stale PID** (#2720) – Affects gateway reliability, especially after unexpected shutdowns.

**Satisfaction signals:**
- The community actively contributes fixes (e.g., #2982, #2890, #2893, #2977, #2781) – a sign of a healthy open-source ecosystem.
- Discussions are constructive and focused on reproducibility.

**Overall sentiment:** Mixed – users appreciate the rapid fixes but are frustrated by recurring regression and config issues that could be caught by better testing or linting.

## 8. Backlog Watch

Items that have been open for an extended period or have high importance but lack maintainer response:

- **[Issue #1042 – exec tool guardCommand bug](https://github.com/sipeed/picoclaw/issues/1042)** – Created 2026-03-04, 15 comments, no fix PR. **Longest-standing open issue with high community engagement.** Needs maintainer triage and a proposed fix.

- **[Issue #2720 – Stale PID crash loop](https://github.com/sipeed/picoclaw/issues/2720)** – Created 2026-04-30, high priority. A fix PR (#2813) has been open since 2026-05-07 but not merged. Review and merge are overdue.

- **[Issue #2796 – History missing previous user messages](https://github.com/sipeed/picoclaw/issues/2796)** – Created 2026-05-07, 5 comments. No associated PR yet. A clear UX bug that should be addressed.

- **[Issue #2887 – .deb on RISC-V broken](https://github.com/sipeed/picoclaw/issues/2887)** – Created 2026-05-17, 8 comments. No response from maintainers. Platform-specific but blocks an entire architecture.

- **[PR #2813 – fix(pid): verify gateway identity](https://github.com/sipeed/picoclaw/pull/2813)** – Open since 2026-05-07, addressing the high-priority issue #2720. Awaiting review/merge.

Maintainers are encouraged to prioritise the PID fix and the `exec` tool false-positive bug, as both affect reliability and user trust.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-06-02

## 1. Today's Overview

NanoClaw saw moderate activity in the past 24 hours with 3 issues updated (1 closed, 2 new open) and 6 pull requests touched (5 open, 1 closed). No new releases were published. The project continues to focus on reliability and operational robustness: a high-priority A2A session routing bug was closed, while two new critical bugs surfaced—a crash loop on corrupt transcripts and a missing per-tool timeout. Several fix PRs are already in review, indicating a responsive maintainer team. Overall, the project's health is stable but showing typical growing pains for an AI agent orchestration platform.

## 2. Releases

*None in this period.*

## 3. Project Progress

**Merged/Closed PRs (1):**  
- [PR #2664](https://github.com/nanocoai/nanoclaw/pull/2664) – **Closed** – Run browser scraping sidecar in v2 container. This advance integrates the scraping sidecar into the agent container runtime, a step toward richer browser automation capabilities.

**Closed Issue:**  
- [Issue #2331](https://github.com/nanocoai/nanoclaw/issues/2331) **(closed)** – Bug fix: `findSessionByAgentGroup` was routing A2A replies to wrong sessions in multi-channel groups by using a recency-only sort. The fix ensures correct session selection.

Other PRs remain open and under review (see below).

## 4. Community Hot Topics

Activity was concentrated around reliability and container compatibility. No single thread generated multiple comments or reactions, but the following items attracted the most developer attention:

- **[Issue #2669](https://github.com/nanocoai/nanoclaw/issues/2669)** – Open: `agent-runner` crash loop on corrupted resumed transcript. The session becomes permanently stuck, requiring manual intervention. This directly impacts production deployments and has a fix PR already submitted (#2670). Underlying need: self-healing mechanisms for agent sessions.

- **[PR #2666](https://github.com/nanocoai/nanoclaw/pull/2666)** – Open: Provider failure recovery with rollback, replay, in-turn ack, and friendly fallback. This large PR aims to make agent runs resilient to provider API failures, addressing a long-standing pain point in multi-provider setups.

- **[PR #2667](https://github.com/nanocoai/nanoclaw/pull/2667)** – Open: Rootless Podman support for container user. This is a prerequisite for #2666 and addresses deployment constraints on LXC and similar environments.

## 5. Bugs & Stability

Two new bugs were reported today, both high-severity:

| # | Issue | Severity | Fix PR? | Summary |
|---|-------|----------|---------|---------|
| 1 | **[#2669](https://github.com/nanocoai/nanoclaw/issues/2669)** – Corrupt resumed transcript crash loop | Critical – session stuck forever | Yes ([#2670](https://github.com/nanocoai/nanoclaw/pull/2670)) | Agent-runner polls indefinitely with 400 errors when `thinking` blocks cannot be modified. No self-healing triggers. |
| 2 | **[#2668](https://github.com/nanocoai/nanoclaw/issues/2668)** – No per-tool timeout | High – session blocked up to 30 minutes | None yet | A hung MCP tool call inside a synchronous turn blocks the entire agent session until a cold-kill timeout. |

Both bugs were opened within the last 24 hours. The previously reported high-priority bug #2331 (A2A session routing) was closed with a fix. No regressions from recent releases have been noted.

## 6. Feature Requests & Roadmap Signals

No new feature requests were filed as issues. However, two development directions are clear from PRs and the bugs themselves:

- **Provider failure recovery** ([PR #2666](https://github.com/nanocoai/nanoclaw/pull/2666)) – Rollback and replay of agent turns after a provider error. This is the most substantial feature in the pipeline and is likely to land in the next minor release.
- **Per-tool timeout** – Implicitly requested via bug [#2668](https://github.com/nanocoai/nanoclaw/issues/2668). Although not yet implemented, the severity of the issue suggests it will be prioritized. A configurable per-tool timeout (e.g., 30–60 seconds) could appear in the next release.
- **Rootless Podman support** ([PR #2667](https://github.com/nanocoai/nanoclaw/pull/2667)) – Required for certain deployment environments. Likely to merge soon as it’s a dependency for other features.

## 7. User Feedback Summary

Real user-reported pain points from the latest issues:

- **Session routing in multi-channel groups** – A user reported that A2A replies were delivered to the wrong session (closed with fix).
- **Unreliable agent resumption** – A corrupted transcript leaves the agent stuck in a crash loop with no automatic recovery. The user (ddaniels) expressed frustration with the “crash-loop forever” behavior.
- **Tool timeout frustration** – User mshirel reports a single hung tool call can block a session for up to 30 minutes, making the system unreliable for long-running or externally-dependent tool calls.

Overall satisfaction appears mixed: the project is actively fixing bugs, but users are encountering stability issues in production deployments, particularly around session resumption and tool orchestration.

## 8. Backlog Watch

- **[PR #2346](https://github.com/nanocoai/nanoclaw/pull/2346)** – Open since 2026-05-08 (25 days). Fix for unknown slash commands being silently dropped. No recent comments or maintainer updates. This PR addresses a user-facing bug where chat messages starting with an unrecognized slash command are lost. It may require maintainer attention to move forward.
- **[Issue #2669](https://github.com/nanocoai/nanoclaw/issues/2669) and #2668** are recent and already getting attention (fix PR for #2669, no fix yet for #2668). Not backlogged.

**Maintainers:** Please consider reviewing PR #2346, as it has been open for nearly a month and addresses a silent data loss issue.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-06-02

## 1. Today's Overview
The NullClaw repository saw minimal activity over the past 24 hours. No new issues were opened or closed, and only one pull request (#943) was updated—remaining open with no merge activity. No new releases were published. Despite the quiet day, the single open PR addresses a user-facing Telegram integration issue, indicating continued incremental maintenance work. Overall project health appears stable but with low short-term momentum.

## 2. Releases
No new releases were created on this date. The latest available release remains the previous version (none specified in data). There are no migration notes or breaking changes to report.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The only open PR (#943) is still awaiting review and merge:
- **#943 [OPEN]** *fix(telegram): show typing indicator during callback-query processing* – Submitted by `raskevichai`, created and updated on 2026-06-01. This PR addresses a missing "typing…" indicator when users press inline buttons in Telegram, improving user feedback during model calls.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/pull/943)

## 4. Community Hot Topics
With zero issues and only one PR carrying no comments or reactions, there are no particularly active discussions today. The sole PR #943 is the only recent contributor activity, though it has not yet attracted community engagement.

## 5. Bugs & Stability
One confirmed bug is being addressed by the open PR:
- **Bug #942** (referenced by PR #943): Telegram inline button presses (e.g., `nc_choices` options, any `callback_query`) leave the chat completely silent while the agent processes the choice—no "typing…" indicator appears.  
  **Severity:** Medium (affects user experience but not functionality).  
  **Fix status:** PR #943 is available and (once merged) will resolve the issue by displaying a typing indicator during callback-query processing. No other bugs or regressions were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
No new feature requests were submitted today. The project’s roadmap signals remain unchanged from previous periods. The fix in PR #943 does not introduce new features, but it improves an existing Telegram interaction path, which may hint at ongoing refinement of messaging platform integrations.

## 7. User Feedback Summary
The only actionable user pain point from today’s data is the silent Telegram experience when using inline buttons. This was likely reported as an issue (closed #942) and prompted the fix in PR #943. No other user feedback, satisfaction or dissatisfaction signals are available in the current data window.

## 8. Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention were identified. The repository currently has zero open/active issues, and the one open PR (#943) is relatively recent and still being processed. No items are stuck in the backlog.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-02

## Today's Overview

IronClaw remains in an intense development phase with **46 pull requests** updated in the last 24 hours, **32 of which were merged or closed**, and **12 issues** receiving updates (all but one open). The majority of activity continues to center on the **Reborn architecture overhaul** — a stateless agent model with cloud-native deployment — with contributions spanning event streaming, trigger pollers, OAuth integration, and model governance. No new releases were cut today, but the volume of merged PRs suggests a near-term release candidate is being assembled. **One nightly E2E test run failed**, a recurring stability signal that warrants attention.

## Releases

No new releases were published today. The project is in an active integration window, with many Reborn features landing in the `reborn-integration` branch.

---

## Project Progress

Today saw **32 merged/closed PRs**, advancing several major work streams:

- **Trigger Poller Core & Seams** (PR #4301, #4308, #4292, #4303 follow-up) — The backend-agnostic trigger poller `tick_once` and materialization seams were merged, along with harness coverage for crash/replay and trusted poller boundaries. A follow-up issue (#4303) requests splitting the monolithic `worker.rs` (~2500 lines).
- **OAuth & Identity** (PR #4297, #4294, #4300, #4287) — GSuite OAuth setup/recovery, Notion OAuth provider, and Google/GitHub OAuth for WebUI v2 all landed. The WebUI login page is now functional outside tests.
- **Capability Surface** (PR #4293, #4280, #4305, #4306) — GitHub capabilities ported to Reborn, GSuite capabilities surfaced to the model, provider tool-call input validation added, and Reborn skill activation context progressively disclosed.
- **Budgets & Credits** (PR #3899, #4286) — All follow-ups from the cost-based budgets foundation (#3841) are now closed, including real token usage in provider calls and carrier-grade credit exhaustion handling.
- **Events & Streaming** (PR #4272, #3281 closed) — Slack Events API host ingress added, and the `EventStreamManager` for durable projection fanout was merged.
- **Extension Lifecycle** (PR #4299, #4307) — Bundle manifest hash migration on startup and WebUI v2 extension registry management routes are in.
- **Docs & Plans** (PR #4302, #4304) — A crate-level AGENTS.md reconciliation and a reviewed implementation plan for runtime context prompt stage were contributed by a new contributor and a core developer respectively.

**Notable closed PRs with broad scope:** PR #3899 (budgets follow-ups) touched 28+ scope areas and includes a DB migration. PR #4293 (GSuite capabilities) and PR #4280 (GitHub capabilities) each touched 30+ scope areas with DB migrations.

---

## Community Hot Topics

1. **#4279 — Inquiry regarding Reborn roadmap and cloud-native architecture** (0 comments, 0 👍)  
   *User liaoqianchuan* asks about stateless agent model, multi-tenant scaling, and timeline for Reborn stabilization. No maintainer response yet. This signals growing external interest in the Reborn branch.

2. **#4278 — Unbounded conversation growth in ENGINE_V2** (0 comments)  
   *Same user* identifies a potential scalability issue with all session messages stored as a single JSON object in `memory_documents`. Though no engagement yet, this echoes known context-window exhaustion concerns.

3. **#4310 — Context-overflow recovery emits ShrinkContext but executor retries without shrinking** (0 comments)  
   A bug filed by core contributor *henrypark133* highlights a regression in Reborn’s recovery path. The issue is detailed and likely to be prioritized given its impact on reliability.

4. **#4108 — Nightly E2E failure** (0 comments)  
   Automated failure report from GitHub Actions. The v2-engine job failed, commit `749f584`. No linked PR or comment yet — this is a recurring alert (previous failures observed).

---

## Bugs & Stability

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **High** | #4108 | Nightly E2E (v2-engine) failed. No root cause identified. | None |
| **High** | #4310 | Context-overflow `ShrinkContext` not applied during retry — agent may keep oversizing prompts. | No |
| **High** | #4309 | Compaction summary write can outlive failed `BeforeModel` checkpoint, blocking retries. | No |
| **Medium** | #4311 | Budget governance failures collapsed into `ContextOverflow`, losing distinction. | No |
| **Medium** | #4314 | `CompactionLeakDetected` milestone never emitted — dead code. | No |
| **Low** | #4312 | No live projection/WebUI updates for compaction progress. | No |

The nightly E2E failure (#4108) is the most critical stability signal, as it blocks CI confidence. The three high-severity bugs (#4310, #4309, #4311) all relate to compaction and retry logic in the Reborn agent loop — likely blockers before a release.

---

## Feature Requests & Roadmap Signals

- **OAuth for WebUI** (#4287, #4294) — Now implemented and merged after community request.
- **Slack / Feishu integration** (#4272, #4178) — New event intake channels for Slack and Feishu; not yet merged for Feishu (#4178 is open).
- **MiniMax M3 model** (#4298) — Default model upgrade proposed by a regular contributor, open but low risk.
- **User-requested roadmap clarification** (#4279) — External user requesting timeline for Reborn and cloud-native features. Project may need to publish a public roadmap or respond to this inquiry.
- **Conversation history optimization** (#4278) — Potential performance issue; may become a design request if validated.

---

## User Feedback Summary

**Positive signals:** Community member *liaoqianchuan* expressed admiration for the Reborn architecture shift and cloud-native direction, calling it “essential for scaling to multi-tenant environments.” This indicates external validation of the project’s core design choice.

**Pain points:** The same user raised a concrete concern about unbounded conversation growth in `ENGINE_V2` — a real scalability risk for long-running agents. The lack of response to this and the roadmap inquiry (#4279) may disappoint engaged users.

**Overall satisfaction:** High activity and rapid feature delivery suggest strong maintainer momentum. However, the nightly E2E failure and the accumulation of compaction/budget bugs may pressure developers before a stable release.

---

## Backlog Watch

- **#4108 — Nightly E2E failure** (updated 2026-06-01) — No maintainer comment or linked PR. If this failure is recurring, it should be triaged with higher urgency.
- **#4279 — Roadmap inquiry** (updated 2026-06-01) — No response. A maintainer reply would help community trust.
- **#4278 — Unbounded conversation growth** (updated 2026-06-01) — No engagement yet. This is a potential design-debt item that could become critical as agents run longer.
- **#4178 — Feishu websocket event intake** (open since 2026-05-28) — Large PR with 0 reviews/no activity in last 24h. May need a reviewer assignment.

**Long-running items:** Issue #3281 (EventStreamManager) was only now closed after a month of development — a positive sign that complex Reborn features are reaching completion.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-02

## 1. Today’s Overview
LobsterAI saw extremely high merge activity in the past 24 hours, with **50 pull requests closed/merged** and a new **v2026.6.1 release** published. Only **1 open issue** was updated, reflecting a strong maintainer focus on code integration rather than new bug reports. The release introduces an Expert Kit Store, plugin update checks from npm/clawhub, and a fix for MCP tooling. Overall project health is robust, with the team executing on multiple fronts: UI polish, security improvements, and integration stability.

## 2. Releases
**New version: [LobsterAI 2026.6.1](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.1)**  
- **What’s Changed:**
  - **feat:** Expert Kit Store and Conversation Integration ([#2060](https://github.com/netease-youdao/LobsterAI/pull/2060))
  - **feat:** Plugin update check for npm/clawhub sources ([#2069](https://github.com/netease-youdao/LobsterAI/pull/2069))
  - **fix(mcp):** k (note: summary truncated, likely a fix for the MCP module)
- **Breaking changes:** None noted.
- **Migration notes:** Not provided; users are advised to update from the previous build via the usual update channel.

## 3. Project Progress
The following merged PRs illustrate recent feature advancements and bug fixes (top 20 by comment count, all closed in the last 24h):

- **Voice permission UX** – macOS speech input now shows a toast when accessibility permission is denied ([#1952](https://github.com/netease-youdao/LobsterAI/pull/1952))
- **Security monitoring toggle** – Added nsp-clawguard hot-toggle in Settings ([#1962](https://github.com/netease-youdao/LobsterAI/pull/1962))
- **Thinking level control** – New dropdown for chat sessions (Off/Minimal/Low/Medium/High/Adaptive) ([#1985](https://github.com/netease-youdao/LobsterAI/pull/1985))
- **Openclaw compaction & tool results** – Fixed retries and result gaps ([#2015](https://github.com/netease-youdao/LobsterAI/pull/2015))
- **Gateway restart avoidance** – No more restart on token refresh ([#2018](https://github.com/netease-youdao/LobsterAI/pull/2018))
- **Artifacts UX** – Lazy-loaded source preview, theme adaptation, file existence check ([#2022](https://github.com/netease-youdao/LobsterAI/pull/2022))
- **Browser/webfetch stability** – Improved success rate ([#2023](https://github.com/netease-youdao/LobsterAI/pull/2023))
- **IM bot management UI** – Redesigned bot configuration interface ([#2025](https://github.com/netease-youdao/LobsterAI/pull/2025))
- **Model switch fix** – Custom model switch error resolved ([#2032](https://github.com/netease-youdao/LobsterAI/pull/2032))
- **Qwen coding plan fix** – Updated for Qwen 3.6 Plus ([#2035](https://github.com/netease-youdao/LobsterAI/pull/2035))
- **Markdown local resource path** – Fixed relative image display in preview ([#2002](https://github.com/netease-youdao/LobsterAI/pull/2002))
- **Many UI/icon/copy updates** – Continuous polish by multiple contributors.

## 4. Community Hot Topics
The only **open issue** updated is **[#2081: 订阅 (Subscription)](https://github.com/netease-youdao/LobsterAI/issues/2081)**. The user complains that subscribed credits (5500 points) were reset at the end of the month without being used. This has **1 comment** (no maintainer reply yet) and **0 👍**. Underlying need: clearer credit expiry policies or rollover options. Despite low engagement, this is a high-signal topic because it touches monetization and user trust.

No PRs received more than 0 reactions or comments in the displayed data, suggesting that the community is mostly silent on active code changes, or that the digest’s PR list did not include reaction counts.

## 5. Bugs & Stability
| Severity | Issue | Status | Fix PR Exists? |
|----------|-------|--------|----------------|
| **High** | Subscription credits reset unexpectedly ([#2081](https://github.com/netease-youdao/LobsterAI/issues/2081)) | Open | No |
| **Medium** | macOS voice input permission denial gave no feedback | Fixed | [#1952](https://github.com/netease-youdao/LobsterAI/pull/1952) (merged) |
| **Medium** | Openclaw tool result gaps / compaction retries | Fixed | [#2015](https://github.com/netease-youdao/LobsterAI/pull/2015) (merged) |
| **Low** | Browser config invalid / model switch error with custom models | Fixed | [#2031](https://github.com/netease-youdao/LobsterAI/pull/2031), [#2032](https://github.com/netease-youdao/LobsterAI/pull/2032) (merged) |
| **Low** | Markdown preview local resource path not resolved | Fixed | [#2002](https://github.com/netease-youdao/LobsterAI/pull/2002) (merged) |

No critical regressions or crashes were reported in the last 24h.

## 6. Feature Requests & Roadmap Signals
The **credit reset complaint** (#2081) implicitly requests better credit management (rollover, notification before expiry, usage logs). This could become a feature in an upcoming patch. Meanwhile, the merged PRs show strong signals for the next major version:

- **Expert Kit Store** (v2026.6.1) – indicates a marketplace for AI agent kits.
- **Thinking level control** (#1985) – deeper model configuration for power users.
- **Security monitoring** (#1962) – proactive security plugin integration.
- **IM bot UI redesign** (#2025) – improved user experience for chat bots.

These suggest the team is moving toward a plugin/extension ecosystem and fine-grained user controls.

## 7. User Feedback Summary
- **Dissatisfaction:** One user expressed frustration about lost subscription credits, calling the policy “ridiculous” (translated). No other explicit pain points were recorded in the last 24h.
- **Satisfaction:** No direct positive feedback appeared, but the sheer volume of bug fixes and UX improvements (voice, artifacts, IM) indicates the team is addressing common pain points.

## 8. Backlog Watch
There are **no long-unanswered issues or PRs** requiring maintainer attention. The only open issue (#2081) is recent (created 2026-06-01) and has no maintainer response yet. It should be monitored for escalation. No stale PRs are present; all 50 updated PRs were closed.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-02

## Today's Overview
The Moltis project saw no new issues or releases in the last 24 hours, with zero open issues or pull requests currently awaiting action. Three pull requests were merged or closed on June 1, indicating continued steady progress on provider integration, capabilities handling, and OpenAI Codex compatibility. Overall project activity remains moderate but focused, with no unresolved blockers or regressions reported.

## Releases
No new releases were published. All recent changes remain in `main`.

## Project Progress
Three pull requests were merged or closed today:

- **PR #1090 — refactor(providers): use explicit OpenAI capabilities**  
  Replaces heuristic URL/name checks for OpenAI‑compatible providers with a declarative capability policy system. Built‑in providers and resolved models now register their capabilities explicitly, while custom providers receive strict defaults. Includes regression tests for known provider URLs and model names.  
  *(by penso, merged 2026-06-01)*

- **PR #1031 — Add NEAR AI Cloud provider**  
  Integrates NEAR AI Cloud as a new OpenAI‑compatible provider using `NEARAI_API_KEY` and endpoint `https://cloud-api.near.ai/v1`. Models are discovered from the public `/v1/model/list` catalog, and TEE‑aware recommendations and capabilities are surfaced. Also updates provider setup, onboarding documentation, and language listings.  
  *(by PierreLeGuen, merged 2026-06-01)*

- **PR #1088 — [codex] Handle OpenAI Codex final tool‑call arguments**  
  Fixes argument‑delta handling in the OpenAI Codex provider by recording `response.function_call_arguments.done` payloads and synthesizing a streaming delta from final arguments when no intermediate deltas were emitted. Prevents “missing‑argument” errors during decode diagnostics by keeping empty accumulated argument strings flowing.  
  *(by s-salamatov, merged 2026-06-01)*

## Community Hot Topics
No issues or pull requests attracted comments or reactions in the last 24 hours. The three merged PRs had no discussion threads, indicating routine technical work with no community debate.

## Bugs & Stability
No bugs, crashes, or regressions were reported today. The Codex fix (PR #1088) proactively addresses a potential decode‑time error scenario, but no user reports triggered it.

## Feature Requests & Roadmap Signals
No new feature requests were filed. The addition of NEAR AI Cloud (PR #1031) and the refactoring of provider capabilities (PR #1090) suggest the team is actively expanding provider coverage and hardening the provider abstraction layer—both likely to be part of the next minor release.

## User Feedback Summary
No user feedback or pain points were recorded in the last 24 hours. The project continues to receive low issue volume, which may indicate stable usage or a small active user base.

## Backlog Watch
No open issues or pull requests require maintainer attention. All three recently updated PRs have been resolved. The project’s backlog is effectively empty, with no unanswered items remaining.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-02

## 1. Today's Overview

CoPaw (QwenPaw) remains in a high-activity phase with **50 issues** and **34 pull requests** updated in the last 24 hours, reflecting strong community engagement and rapid development. Two new releases were published today – stable **v1.1.10** and **v1.1.10-beta.2** – bringing a new sub‑agent spawning tool and several bug fixes. The project is actively addressing a cluster of cron‑job and session‑sharing bugs, while a major backend migration to AgentScope 2.0 has entered the implementation stage with a dedicated PR. Overall project health is good, though Windows‑specific resource leaks and configuration‑persistence issues remain the most frequently reported pain points.

## 2. Releases

Two versions were released today:

- **v1.1.10** (stable)  
  ✨ **Agent System**: Added `spawn_subagent` tool for ephemeral in‑workspace sub‑agent execution.  
  ✨ **Coding Mode**: New “Open Directory” tab to reference local files.  
  No breaking changes are mentioned in the release notes; no migration steps required for existing users.

- **v1.1.10-beta.2**  
  🐛 Fixed website header styling and added auto‑continue video.  
  🐛 Fixed skill tag preservation and enable/disable behaviour.

## 3. Project Progress

Today **9 PRs were merged or closed**, including:

- **MCP server process pooling** – [PR #4849](https://github.com/agentscope-ai/QwenPaw/pull/4849) (merged) introduces `SharedMCPPool` to reuse MCP servers across agents, directly addressing the resource explosion issue reported in [#4842](https://github.com/agentscope-ai/QwenPaw/issues/4842).
- **Release chore** – [PR #4867](https://github.com/agentscope-ai/QwenPaw/pull/4867) (closed) bumps version to v1.1.10 and updates release notes.
- **Test coverage** – [PR #4852](https://github.com/agentscope-ai/QwenPaw/pull/4852) (open) adds 153 unit and contract tests for runner and routers, targeting issue #4340.

Additionally, open PRs advancing key fixes:
- **Context window defence** – [PR #4787](https://github.com/agentscope-ai/QwenPaw/pull/4787): prevents oversized shell output from blowing up the context window.
- **Cron agent empty traces** – [PR #4822](https://github.com/agentscope-ai/QwenPaw/pull/4822): fixes share_session cron agent tasks producing no execution trace.
- **Windows browser cleanup** – [PR #4853](https://github.com/agentscope-ai/QwenPaw/pull/4853): kills process tree and cleans lock files on Windows after browser session ends.
- **AgentScope 2.0 migration** – [PR #4846](https://github.com/agentscope-ai/QwenPaw/pull/4846) (WIP): backend dependency upgrade.

## 4. Community Hot Topics

The most active discussions centre on **cron‑job reliability** and **backend architecture**:

- **#4653** ([CLOSED, 9 comments](https://github.com/agentscope-ai/QwenPaw/issues/4653)) – Bug report stating that cron tasks sharing a session with user messages get interrupted when a new user message arrives. The underlying need is for **dedicated cron sessions** to guarantee task completion.
- **#4666** ([OPEN, 6 comments](https://github.com/agentscope-ai/QwenPaw/issues/4666)) – Models configuration page is lost after creating a new session, requiring a restart. Indicates a front‑end state persistence issue that frustrates users.
- **#4649** ([CLOSED, 6 comments](https://github.com/agentscope-ai/QwenPaw/issues/4649)) – Orphaned cron jobs not cleaned up when `jobs.json` is updated, causing ghost tasks. The community is asking for a **robust scheduler lifecycle**.
- **#4727** ([OPEN, 5 comments, 2 👍](https://github.com/agentscope-ai/QwenPaw/issues/4727)) – Proposal to migrate backend from AgentScope 1.x to 2.0. This roadmap item has attracted visibility and a corresponding PR now exists.

## 5. Bugs & Stability

**High severity:**

- **#4888** ([OPEN, 1 comment](https://github.com/agentscope-ai/QwenPaw/issues/4888)) – Dream agent uses relative path `write_file("MEMORY.md")` and overwrites another workspace’s MEMORY.md. **Potential data loss**; needs urgent path isolation.
- **#4844** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4844)) – Browser processes and temp directory locks persist on Windows after session end, blocking backups. Fix PR #4853 is open.
- **#4834** ([OPEN, 3 comments](https://github.com/agentscope-ai/QwenPaw/issues/4834)) – MCP server processes accumulate across restarts, slowing console loading. Fix already merged in PR #4849.

**Medium severity:**

- **#4872** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4872)) – New session loads raw context without compression, causing infinite context inflation.
- **#4877** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4877)) – Custom channel replace_channel stops listening on save; a fix PR (#4884) has been opened.
- **#4875** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4875)) – Upgrading via installation script resets the uv virtual environment, requiring reinstallation of packages.

**Low severity / closed:**

- **#4874** ([CLOSED, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4874)) – Tauri desktop cannot download files from `return-file` skill (workaround: use browser‑based version).
- **#4864** ([CLOSED, 3 comments](https://github.com/agentscope-ai/QwenPaw/issues/4864)) – v1.1.9 sends no response after installation (likely model configuration issue).
- **#4714** ([CLOSED, 3 comments](https://github.com/agentscope-ai/QwenPaw/issues/4714)) – v1.1.9-beta.1 queue issues fixed in later releases.

## 6. Feature Requests & Roadmap Signals

Requests shaping the next releases:

- **AgentScope 2.0 migration** – [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) with PR #4846 already in progress; likely to land in a future major version.
- **Agent‑scoped web login accounts** – [#4859](https://github.com/agentscope-ai/QwenPaw/issues/4859) wants per‑agent credentials in multi‑agent deployments; could be included in v1.2.
- **Before You Build skill proposal** – [#4841](https://github.com/agentscope-ai/QwenPaw/issues/4841) asks for a skill that makes agents pause before implementation and review requirements. Community contribution pending.
- **Font size adjustment** – [#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154) (open since May 9) requests Ctrl‑scroll zoom and system DPI awareness for Desktop mode. Long‑standing quality‑of‑life need.
- **Windows desktop session persistence** – [#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733) wants the desktop app to remember the last used agent and conversation after restart.

## 7. User Feedback Summary

**Pain points:**

- **Cron‑job unreliability** remains the top frustration: tasks are interrupted, ghost jobs persist, and share‑session mode produces empty traces.
- **Configuration loss** after session creation or upgrade (models page, disabled skills reset, env resets) erodes user trust.
- **Windows‑specific resource leaks** (MCP processes, browser locks) are repeatedly reported, though fixes are in flight.
- **UI/UX regressions** (e.g., cannot switch conversations in Coding Mode, input box focus lost) affect daily workflows.

**Satisfaction signals:**

- The new `spawn_subagent` tool and “Open Directory” tab are well‑received.
- Fast turnaround on critical bugs (e.g., MCP pooling merged today) demonstrates responsive development.
- Users actively propose skills and config improvements, indicating a healthy contributor community.

## 8. Backlog Watch

Issues or PRs that need maintainer attention:

- **#4154** (Font size adjustable) – Open since May 9 with 2 comments; no maintainer response yet. Affects Desktop users daily.
- **#4731** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4731)) – Browser launch fails with Edge exit code 21 on Windows 11; no fix PR linked, may need platform investigation.
- **#4875** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4875)) – uv virtual environment reset on upgrade; no PR yet.
- **#4818** ([OPEN, 2 comments](https://github.com/agentscope-ai/QwenPaw/issues/4818)) – Cron share_session agent tasks produce empty traces; PR #4822 exists but is still open.
- **#4666** ([OPEN, 6 comments](https://github.com/agentscope-ai/QwenPaw/issues/4666)) – Models config page missing after new session; no PR yet despite being a high‑impact bug.
- **#4888** ([OPEN, 1 comment](https://github.com/agentscope-ai/QwenPaw/issues/4888)) – Dream agent overwriting other workspaces’ MEMORY.md – urgent but not yet assigned.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-02

## 1. Today's Overview

ZeptoClaw saw moderate activity over the past 24 hours, with 18 pull requests updated—17 of which were merged or closed—and one new issue opened. The maintenance cadence remains healthy, driven primarily by dependency bumps (12 dependabot PRs) and two non-trivial bugfix cherries merged. One CI policy change (binary-size gate) is still pending review. The project’s single open issue tracks a binary-size drift against the strategic 7 MB target, indicating an ongoing focus on build artifacts and binary footprint. No new releases were cut today.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

**Merged/closed PRs advancing the codebase:**

- **Provider keyword fallback fix**  
  [#592](https://github.com/qhkm/zeptoclaw/pull/592) (submitted by *Sisuthros*) and its cherry-picked copy [#610](https://github.com/qhkm/zeptoclaw/pull/610) (merged today) correct a critical logic error: `infer_provider_name_for_model` could return a provider the user had not configured, leading to a 100% error rate on certain NIM-served models. This is a direct stability improvement.

- **RUSTSEC advisory clearing**  
  [#594](https://github.com/qhkm/zeptoclaw/pull/594) bumped `lettre` to 0.11.22 and `diesel` to 2.3.8 to resolve six fresh advisories, restoring green CI across all open PRs.

- **Dependency updates** (12 automerge-friendly PRs):  
  - Rust: `uuid 1.23.0→1.23.1`, `bcrypt 0.19.0→0.19.1`, `clap 4.6.0→4.6.1`, `mail-parser 0.11.2→0.11.3`, `tower-http 0.6.8→0.6.10`  
  - JS tooling: `astro` bumped in two documentation landing sites (`6.1.6→6.3.1`, `6.1.9→6.3.3`), `@astrojs/starlight` bumped in both landing sites (`0.38.x→0.39.2`), `eslint 10.0.2→10.3.0` in the panel  
  - GitHub Actions: `taiki-e/install-action 2.77.3→2.78.2`, `EmbarkStudios/cargo-deny-action 2.0.17→2.0.18`  
  - Docker: `rust 1.93-slim-trixie→1.95-slim-trixie`, `debian base image SHA update`

**Open PR under review:**  
- [#611](https://github.com/qhkm/zeptoclaw/pull/611) – Promotes `binary-size` job from a post-mortem to a PR gate at a 7.5 MB ceiling (with a strategic target of 7 MB). This is actively discussed in the linked issue.

## 4. Community Hot Topics

The most active item in terms of cross-referencing and impact is the **provider keyword fallback bug** chain:

- **Issue (none directly, but PRs generated fix)** – The bug was first surfaced in PR [#592](https://github.com/qhkm/zeptoclaw/pull/592) by external contributor *Sisuthros*, solving a production outage causing 100% errors on a NIM-served Photon instance. The maintainer cherry-picked it via [#610](https://github.com/qhkm/zeptoclaw/pull/610) because the fork branch could not be rebased cleanly. This indicates a real-world pain point that motivated a quick-resolution path.

- **Binary-size gate debate**  
  Issue [#612](https://github.com/qhkm/zeptoclaw/pull/612) (open, 0 comments yet) calls for auditing an ~800 KB binary-size drift since the 6.2 MB low-water mark and tightening the CI gate to 7 MB. While it has no comments, it is the only open issue and directly relates to Open PR #611, making it the focal point of current CI policy discussions.

No issues with high reaction counts or lengthy discussions were recorded in the sample.

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | `infer_provider_name_for_model` returns unconfigured provider via keyword fallback, causing 100% error rate on some NIM models | Fixed and merged (today) | [#592](https://github.com/qhkm/zeptoclaw/pull/592) / [#610](https://github.com/qhkm/zeptoclaw/pull/610) |
| Medium | ~800 KB binary-size drift since 6.2 MB low water mark; current stripped size 6.98 MB (21 KB under 7 MB target) | Under investigation | Open Issue [#612](https://github.com/qhkm/zeptoclaw/pull/612) — no fix PR yet |
| Low | Several RUSTSEC advisories (lettre, diesel) blocked CI across all open PRs | Fixed (merged days ago, but cleared blockers for today's merges) | [#594](https://github.com/qhkm/zeptoclaw/pull/594) |

The provider bug fix is the most impactful stability improvement of the day.

## 6. Feature Requests & Roadmap Signals

- **Binary-size CI gate** – PR [#611](https://github.com/qhkm/zeptoclaw/pull/611) and Issue [#612](https://github.com/qhkm/zeptoclaw/pull/612) signal a strong maintainer push to enforce a strict binary-size limit. The current 7.5 MB ceiling is a tactical compromise; the strategic goal is 7 MB. This is likely to be the next merged feature (pending audit results).

- No explicit user-requested features were filed today. The absence suggests that recent infrastructure improvements (binary size, advisory clearing) are absorbing attention.

## 7. User Feedback Summary

While no direct user feedback was posted in issues or PRs during this window, the prompt resolution of the provider fallback bug (PR #592) indicates a clear pain point: when a model ID contains a keyword like `openai/`, ZeptoClaw could incorrectly claim an unconfigured provider, rendering a production instance unusable. The rapid cherry-pick (PR #610) and advisory clearing (PR #594) demonstrate maintainer responsiveness to real-world incidents.

The binary-size gate discussion (Issue #612) suggests some users or contributors may have observed bloat; the author explicitly references a “drift” that needs auditing.

## 8. Backlog Watch

- **No long-unanswered issues or PRs** were identified. The oldest open PR is [#611](https://github.com/qhkm/zeptoclaw/pull/611) (created 2026-06-01), still under review. The only open issue [#612](https://github.com/qhkm/zeptoclaw/pull/612) is from the same day. All other items were closed/merged today.

- **Dependabot PRs** are automatically handled and do not require maintainer manual attention.

**Project health indicator:** Green – bugs are fixed promptly, CI is clean, and the maintainer is actively shaping quality gates.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-02

## 1. Today's Overview
The project is in a period of **high activity**, with 36 issues and 37 PRs updated in the last 24 hours. No new releases were tagged. The community is actively reporting and fixing bugs — 8 issues were closed and 13 PRs were merged/closed, including several critical severity fixes. Development momentum is concentrated on quality-of-life improvements (email channel, web fetch, Discord), the v0.8.0 integration branch (#6848), and the early stages of an agent evaluation harness. Several P1 bugs remain open, indicating ongoing stability work.

## 2. Releases
No releases were published in the last 24 hours. The most recent activity is around the **v0.8.0-beta-2** pre-release branch (#6848) and the **v0.8.1** integration tracker (#6970).

## 3. Project Progress
**Merged/closed PRs (13 total)** include a mix of bug fixes and feature additions:

- **Email channel**: Fixed blank SMTP credential overrides — `smtp_username`/`smtp_password` now fall back to shared credentials when empty (#6979, closed).  
- **Web fetch**: `web_fetch.allowed_private_hosts` now correctly resolves DNS names against the private host allowlist (#6974, closed).  
- **Image info tool**: Paths are now resolved through the security policy, re‑covering a previously reverted fix (#6972, closed).  
- **Discord**: Delivery failure logs no longer echo raw marker targets (security redaction) (#7031, closed).  
- **Channel date context**: Restored the missing date-time + UTC offset prompt context, improving prompt cache stability (#6931, closed).  
- **Lean default channel bundle**: Default builds now include only ACP server, webhook, email, and Telegram — reducing binary size (#6904, closed, corresponding issue #6895).  
- **Jina AI web search**: Added as a new `web_search` provider (#6833, closed).  
- **Kimi temperature fix**: `OpenAiCompatibleModelProvider` now omits `temperature` for kimi‑k2 models, fixing 400 errors (#7049, closed).  
- **Stream error recovery**: Restored conservative fallback to non‑streaming path when provider stream fails before visible output (#6983, closed).  
- **Reply‑intent precheck**: Opt‑out classifier call lowers LLM cost for single‑bot DM deployments (#5979, closed).  
- **Memory strategy refactor**: Replaced `Agent::memory_loader` with `MemoryStrategy` trait (second slice of decoupling, #6850) (#7053, open, ready for review).  
- **Agent evaluation harness**: Phase 0 — deterministic replay of trace fixtures through the real agent loop (#7067, open).  
- **WIT interface files**: Defined WASI Component Model files for Tool, Channel, and Memory plugins (#7060, open).  
- **Documentation**: mdBook reskin to match web dashboard (#7055, open); versioned documentation deployment (#7023, open); localization updates for Spanish/Chinese (#7039, open).

## 4. Community Hot Topics
- **#5146 (Feature: Token consumption minimization via skill compilation)** — 8 comments, 1 👍. The core issue of sending hundreds of lines of skill prose with every prompt remains a high‑risk design challenge. Community discussion points to skill compilation or pre‑reflection to reduce LLM overhead.  
  [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)

- **#5962 (Bug: Ollama Provider call fails when tools are needed)** — 6 comments. Workflow‑blocking (S1) regression for Ollama users; status is “in‑progress”. No fix PR yet.  
  [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)

- **#6378 (Feature: Discord Bot respond only in specific channels)** — 6 comments. Users want `allowed_channels` akin to Matrix/Nextcloud. Accepted but not yet implemented.  
  [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)

- **#6302 (Bug: Gemini 400 — assistant tool_call emitted as first non‑system turn)** — 4 comments. P1, in‑progress. A strict Gemini API invariant violation that breaks many Gemini deployments.  
  [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)

- **#7068 (Bug: Telegram channel receives Codex scratchpad/tool transcript as final response)** — new, 1 comment. A user reports internal scratchpad being sent as the final answer, indicating a channel/agent loop integration bug.  
  [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/7068)

## 5. Bugs & Stability
**High‑severity bugs reported/updated in the last 24 hours:**

| Issue | Severity | Status | Summary |
|-------|----------|--------|---------|
| #6302 | P1 | in‑progress | Gemini 400 — conversation history invariant violation. No fix PR yet. |
| #6472 | P1 | in‑progress | Gateway cannot use Postgres — runtime panic. No fix PR yet. |
| #5155 | P1 | in‑progress | Delegate agents ignore `prompt_injection_mode` and always inject full skills. |
| #6350 | P1 | in‑progress | WhatsApp Web — `allowed‑numbers` bypass for LID‑based contacts, silent drops. |
| #7068 | S1 (blocked) | open | Telegram channel sends scratchpad/tool transcript as final response. |
| #7063 | high | open | Channel‑served agents bypass per‑agent tool allowlist (`start_channels` skips `apply_policy_tool_filter`). |
| #7059 | S2 | open | Default model provider credential fallback in channel orchestrator must be excised. |
| #7022 | S1 | fixed via #7049 (merged) | Kimi‑k2.x fails with 400 because `compatible.rs` forces `temperature:0.7`. |

**Fix PRs merged today:** #6983 (stream error fallback), #6979 (email credentials), #6974 (web fetch), #6972 (image info), #6931 (date context), #7031 (Discord redaction), #7049 (Kimi temperature). Overall, the project is responsive in patching reported issues, but several P1 bugs remain unresolved.

## 6. Feature Requests & Roadmap Signals
- **#7065 (#7067): Agent evaluation harness** — Strong signal: a real `zeroclaw eval` command (replay and live modes) is under implementation with an open PR. Likely to land in v0.8.1.  
- **#7060: WIT interface files for plugins** — Aligns with the WASI‑based plugin architecture (FND‑001). Community‑driven, early stage.  
- **#7055: Documentation reskin** — Improves user onboarding. Low risk, likely merges soon.  
- **#7039: i18n for Spanish/Chinese** — Shows commitment to internationalisation; will follow the #6848 branch.  
- **#5146: Token consumption minimization** — High‑risk, accepted enhancement. Will be a **major performance landmark** when implemented, but no PR yet.  
- **#6378: Discord allowed channels** — Accepted, waiting for implementation.  
- **#6391: Real heartbeat tracking for daemon nodes** — Blocked on architecture decisions.  
- **#6289: Prompt‑triggered install suggestions for missing skills** — Accepted, would improve discoverability.  
- **#6365: Dashboard “Update ZeroClaw” button** — In‑progress, will improve UX for web users.  

**Roadmap focus:** The v0.8.0‑beta‑2 branch (#6848) is the biggest pending integration, and v0.8.1 tracker (#6970) lists channel/provider/tool additions.

## 7. User Feedback Summary
- **Pain points:**  
  - Token waste from full skill injection (#5146) is a recurring concern.  
  - Ollama provider broken when tools are needed (#5962) blocks a significant user group.  
  - Gemini users hit a strict API invariant (#6302) — no workaround.  
  - WhatsApp users experience silent message drops due to LID bypass (#6350).  
  - Email channel misconfigured SMTP credentials (#6881, now fixed).  
  - Telegram users receiving internal tool transcripts (#7068) creates a poor UX.  
- **Satisfaction signals:**  
  - Jina AI addition (#6833) was well‑received.  
  - The lean default channel bundle (#6904) shows the project listens to concerns about bloat.  
  - The agent evaluation harness (#7065) was requested by multiple community members.  
- **Use cases:** users are deploying ZeroClaw on private infrastructure (Postgres, custom TLS certificates #5797), multi‑bot group chats (#5979), and corporate environments with private DNS (#6974).

## 8. Backlog Watch
- **#5146 (Feature: Token minimization via skill compilation)** — open since 2026‑03‑29, 8 comments, accepted but no assignee.  
- **#4853 (Feature: Installing skills from `.well-known` URI)** — open since March, accepted, ties to industry standardization.  
- **#5962 (Bug: Ollama tool call failure)** — open since 2026‑04‑21, in‑progress but no fix PR; needs maintainer attention.  
- **#5797 (PR: add `tls_ca_cert_path` support)** — open since 2026‑04‑16, no recent maintainer activity.  
- **#6315? Not listed but #6320?** (no, note #6391 is blocked).  
- **#6683 (Bug: skill_manage patch ignores cooldown)** — open since May, in‑progress but no assigned maintainer.  

**Recommendation:** The project should prioritise addressing the **P1 Gemini and Ollama bugs**, as they block significant user workflows and have been open for weeks. The token compilation feature (#5146) would unlock substantial cost savings and is a marquee enhancement.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*