# OpenClaw Ecosystem Digest 2026-06-05

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-05 02:43 UTC

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

# OpenClaw Project Digest — 2026-06-05

## Today’s Overview

The project remains in high activity, with 500 issues and 500 pull requests updated in the past 24 hours. Of these, 350 issues are open/active and 150 were closed; on the PR side, 109 were merged or closed while 391 remain open. No new releases were published today, but critical work continues on the SQLite session/transcript migration, the Codex runtime parity effort, and a wide range of connectivity and stability regressions. The issue tracker is heavily loaded with P1 and P2 bugs affecting message delivery, session state, and provider compatibility – many of which have been open for weeks and are tagged `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-product-decision`, indicating a maintenance bottleneck.

## Releases

No new releases today. The project is between versions, with the stable track at `2026.5.22` / `2026.5.28` and a `2026.6.1` release that appears to have introduced several regressions (see Bugs & Stability).

## Project Progress

109 pull requests were merged or closed today. Notable closed items include:

- **CI fix** [#90287](openclaw/openclaw PR #90287) – scoped PR merge diff checks to first parent to avoid false positives from synthetic merge commits.  
- **Codex runtime parity** – several QA-lab tracking issues closed: [#80171](openclaw/openclaw Issue #80171) (Codex-vs-Pi parity harness RFC), [#80397](openclaw/openclaw Issue #80397) (token-efficiency proof), [#80365](openclaw/openclaw Issue #80365) (standalone Codex plugin wrapper). These indicate the parity effort is nearing a milestone.  
- **Connectivity regressions** – [#79794](openclaw/openclaw Issue #79794) (Discord gateway READY event regression, closed), [#87177](openclaw/openclaw Issue #87177) (QQBot message duplication, closed), [#88039](openclaw/openclaw Issue #88039) (session-selected model incorrectly in fallback list, closed), [#88234](openclaw/openclaw Issue #88234) (Feishu dispatch TypeError, closed), [#84820](openclaw/openclaw Issue #84820) (unclosed FileHandle on JSONL lock crashing gateway on Node ≥24, closed).  
- **Stuck session recovery and Telegram issues** – [#74822](openclaw/openclaw Issue #74822) (Telegram "Something went wrong" requiring manual restart, closed), [#73802](openclaw/openclaw Issue #73802) (Discord exec approval cards not delivered, closed).

Key open PRs advancing features and fixes include:

- **Session reset carryover** [#90259](openclaw/openclaw PR #90259) – adds carryover summaries for reset sessions.  
- **Tool definition snapshots** [#90411](openclaw/openclaw PR #90411) – freezes tool registrations before provider exposure to avoid runtime drift.  
- **Live provider model catalog** [#90029](openclaw/openclaw PR #90029) – adds guarded `/models` discovery with TTL caching.  
- **Feishu rate-limit retry** [#89659](openclaw/openclaw PR #89659) – retries on `230020`/`230006` errors.  
- **Discord DM allowlist fix** [#90522](openclaw/openclaw PR #90522) – allows DM reads for allowlisted peers.

## Community Hot Topics

The most active discussions this period:

- **[#72808](openclaw/openclaw Issue #72808) (20 comments, 3 👍) – Silent Slack connection loss**  
  A P1 diamond-lobster bug that has been open since April 27. Users experience silent disconnection from Slack without any notification. The issue remains open with no fix PR linked, suggesting a deep architectural problem in the Slack transport.

- **[#88838](openclaw/openclaw Issue #88838) (17 comments, 1 👍) – SQLite migration tracking**  
  A maintainer-driven issue tracking the branch-by-abstraction approach to migrating session/transcript state to SQLite. This is a key infrastructure change aimed at avoiding a single large rewrite.

- **[#80171](openclaw/openclaw Issue #80171) (15 comments, 1 👍) – Codex-vs-Pi runtime parity QA harness**  
  Closed today. The community is actively engaged in ensuring the switch to Codex as the default OpenAI runtime doesn’t degrade functionality. Multiple sub-issues and PRs were spawned from this RFC.

- **[#90083](openclaw/openclaw Issue #90083) (11 comments, 3 👍) – ChatGPT Responses transport failure with gpt-5.4/5.5**  
  A critical P1 bug from June 4 affecting users who upgraded to `2026.6.1`. OpenAI Responses transport returns `invalid_provider_content_type` for the latest models.

- **[#90093](openclaw/openclaw Issue #90093) (7 comments, 2 👍) – Encrypted reasoning breaks next turn**  
  Also P1 and `2026.6.1`-specific. The native Codex replay sends encrypted reasoning back, causing `400 invalid_encrypted_content` on subsequent turns.

- **[#90072](openclaw/openclaw Issue #90072) (5 comments, 3 👍) – Cron state wiped during SQLite migration**  
  Upgrading to `2026.6.1` silently dropped 44 of 45 cron jobs. High user frustration due to lack of warning or backup.

**Underlying needs:** Users are demanding more robust transport resilience (Slack, Matrix, Discord), better upgrade safety (SQLite migration backups, cron preservation), and faster turnaround on regressions introduced in the latest release.

## Bugs & Stability

### Critical / P1 (with fix PRs)

- **OpenAI ChatGPT Responses transport failure** [#90083](openclaw/openclaw Issue #90083) – `invalid_provider_content_type` for gpt-5.4/5.5. No fix PR yet; still needs maintainer review.  
- **Encrypted reasoning breaks next turn** [#90093](openclaw/openclaw Issue #90093) – native Codex replay sends invalid encrypted content. No fix PR.  
- **Active-memory circuit breaker too aggressive** [#90082](openclaw/openclaw Issue #90082) – fallback prompt pollutes main session. No fix PR.  
- **Cron state silently wiped** [#90072](openclaw/openclaw Issue #90072) – migration drops crons. No fix PR.  
- **Session model route drifts** [#90036](openclaw/openclaw Issue #90036) – Telegram session drifts from `openai/gpt-5.5` to `openai-codex/gpt-5.5` after Codex turn. No fix PR.

### High severity (P1/P2, with fix PRs or activity)

- **Discord oversized-session reset** – PR [#90514](openclaw/openclaw PR #90514) clears stale fallback model state on `/new`/`/reset`.  
- **Subagent kill-vs-complete race** – PR [#90505](openclaw/openclaw PR #90505) fixes task rows stuck in `running` after `markSubagentRunTerminated`.  
- **Moonshot duplicate tool_call_id** – PR [#87596](openclaw/openclaw PR #87596) rewrites duplicate IDs on replay.  
- **WebChat workspace rail shown by default** [#90359](openclaw/openclaw Issue #90359) – Fix PR [#90498](openclaw/openclaw PR #90498) hides it by default.  
- **Gateway drain during supervised restarts** – PR [#90305](openclaw/openclaw PR #90305) adds `KillMode=mixed` and 330s stop budget.  
- **Restart continuation recovery** – PR [#90490](openclaw/openclaw PR #90490) retries deferred entries after startup.  
- **Event-loop stall during embedded_run** – PR [#89040](openclaw/openclaw PR #89040) – addresses 14–22 second stalls causing message loss.

### Long-standing P1/P2 without fix PRs (unchanged)

- **Slack silent disconnect** [#72808](openclaw/openclaw Issue #72808) – open since April 27.  
- **Heartbeat isolated mode regressions** [#65161](openclaw/openclaw Issue #65161) – stalls, mislabeled events, missing writer.  
- **Hard resets despite high reserveTokensFloor** [#63216](openclaw/openclaw Issue #63216) – context overflow loop.  
- **Subagent completion delivery lost** [#67777](openclaw/openclaw Issue #67777) – can fail on timeout/drain/prune.  
- **Mattermost slash commands 503** [#68113](openclaw/openclaw Issue #68113) – not yet initialized since April 17.  
- **Matrix thread replies regression** [#87307](openclaw/openclaw Issue #87307) – sent as normal replies.

## Feature Requests & Roadmap Signals

- **Sensitive data masking** [#64046](openclaw/openclaw Issue #64046) – user request for API keys, tokens, secrets to be hidden in configs, logs, and UI. Rated diamond lobster; pending product decision. Likely to be addressed in a future release to improve security posture.  
- **Anthropic advisor tool support** [#63930](openclaw/openclaw Issue #63930) – adding the beta server-side tool for Claude. Would enable multi-model mid-inference consultation.  
- **Multi-index embedding memory** [#63990](openclaw/openclaw Issue #63990) – resilient failover across embedding models without mixing vector spaces.  
- **Mattermost robust threading** [#65729](openclaw/openclaw Issue #65729) – DM parity, history persistence, WebSocket keepalive.  
- **Control UI plugin contribution slots** [#71736](openclaw/openclaw Issue #71736) – RFC for allowing plugins to add chat modes, approval cards, etc.  
- **Separate internal service identity from user auth** [#69066](openclaw/openclaw Issue #69066) – RFC for cleaner gateway authentication.  
- **Discord access lists with roles** [#69748](openclaw/openclaw Issue #69748) – replace `requireMention/users` with role-based bypass/deny lists.  
- **Live provider model catalog** – PR [#90029](openclaw/openclaw PR #90029) implements guarded `/models` discovery. This is a strong roadmap signal: OpenClaw is building a dynamic model registry to reduce hardcoded catalogs.  
- **Local editor schema** – PR [#89992](openclaw/openclaw PR #89992) writes a JSON schema for `openclaw.json` to improve config discoverability.  
- **Config/plugin migration safety** – The cron wipe [#90072](openclaw/openclaw Issue #90072) and other migration regressions will likely drive better backup/hooks in the SQLite migration path.

**Predictions for next release:**  
- A hotfix for `2026.6.1` regressions (OpenAI Responses, cron migration, circuit breaker) is urgent.  
- The SQLite migration will continue via branch-by-abstraction (tracked in [#88838](openclaw/openclaw Issue #88838)).  
- The Codex runtime parity will reach general availability for all OpenAI models.  
- The live provider catalog helper will be merged, allowing plugins to declare models dynamically.

## User Feedback Summary

**Pain points expressed by users:**

- **Silent failures** – Slack disconnection without notice ([#72808](openclaw/openclaw Issue #72808)), lost connections to Matrix/Discord.  
- **Upgrade breakage** – The `2026.6.1` upgrade introduced multiple regressions (cron wipe, OpenAI transport fail, encrypted reasoning, circuit breaker pollution). Users report frustration with the lack of migration warnings and backup options.  
- **Session bloat and context waste** – Bootstrap files re-injected every turn ([#67419](openclaw/openclaw Issue #67419)), excessive metadata in Telegram messages ([#72704](openclaw/openclaw Issue #72704)).  
- **Message duplication** – QQBot channel duplication ([#87177](openclaw/openclaw Issue #87177)), assistant text-tool rendering duplicates in WebChat ([#72341](openclaw/openclaw Issue #72341)).  
- **Language localization** – Non-English users see untranslated technical metadata in Control UI ([#79034](openclaw/openclaw Issue #79034)).  
- **Installation issues** – Installer hangs with `curl | bash` ([#73814](openclaw/openclaw Issue #73814)).  
- **Telegram** – Thread reply context loss ([#82002](openclaw/openclaw Issue #82002)), heartbeat interruptions ([#64810](openclaw/openclaw Issue #64810)).  
- **Mattermost** – Slash commands not initialized ([#68113](openclaw/openclaw Issue #68113)), cleartext callback URLs exposing tokens ([#65624](openclaw/openclaw Issue #65624)).

**Satisfaction signals:** The community is actively contributing PRs for fixes (e.g., Discord startup priority [#89744](openclaw/openclaw PR #89744), Feishu rate-limit retry [#89659](openclaw/openclaw PR #89659)). The QA-lab and Codex parity efforts show a proactive approach to quality. However, the sheer number of open P1/P2 bugs with long staleness suggests user patience is being tested.

## Backlog Watch

Issues and PRs that are important, long unanswered, or awaiting maintainer action:

- **P1 diamond lobster** – [#72808](openclaw/openclaw Issue #72808) (Slack silent disconnect, open since April 27, 20 comments, no fix).  
- **P1 platinum hermit** – [#63216](openclaw/openclaw Issue #63216) (hard resets despite high reserveTokensFloor, since April 8).  
- **P1 platinum hermit** – [#67777](openclaw/openclaw Issue #67777) (subagent completion delivery lost, since April 16).  
- **P1 diamond lobster** – [#64046](openclaw/openclaw Issue #64046) (

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-06-05 | **Prepared by:** Senior Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is undergoing a rapid maturation phase, characterized by aggressive iteration on reliability, multi-provider integration, and production-grade observability. Projects are converging on common infrastructure patterns—MCP (Model Context Protocol) tooling, SQLite-based session migration, and dynamic model catalogs—while differentiating on architectural choices (Rust versus Go versus TypeScript, monorepo versus modular). Community activity is heavily concentrated in a few high-velocity projects (OpenClaw, IronClaw, ZeroClaw, CoPaw), with the ecosystem split between "core reference" implementations and specialized forks targeting specific deployment contexts (embedded, desktop, Chinese cloud providers). A notable signal: emerging requests for A2A (Agent-to-Agent) protocol support, computer-use capabilities, and structured observability indicate the next frontier beyond basic chat completion.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Today | Health Score | Notes |
|---------|-------------|-----------|---------------|--------------|-------|
| **OpenClaw** | 500 (350 open) | 500 (391 open) | None | **Moderate** – High throughput but severe maintenance bottleneck; 150 issues/109 PRs closed but long-standing P1s unresolved |
| **NanoBot** | 6 (2 open) | 75 (16 open) | None | **High** – 59 PRs merged, rapid issue closure, responsive maintainers |
| **Hermes Agent** | N/A | N/A | N/A | **Unknown** – Summary generation failed |
| **PicoClaw** | 6 (2 open) | 22 (10 open) | Nightly v0.2.9 | **High** – 12 PRs merged, 4 issues closed, maintainers responsive |
| **NanoClaw** | 1 (1 open) | 8 (5 open) | None | **Moderate** – Low volume but quality work on Signal/WhatsApp channels |
| **NullClaw** | 0 | 0 | None | **Inactive** |
| **IronClaw** | 39 (25 open) | 50 (32 open) | None | **High** – 14 issues closed, 8 PRs merged, intense Reborn migration |
| **LobsterAI** | 1 (1 open) | 16 (0 open) | None | **High** – All 16 PRs merged; focus on Cowork and MCP |
| **TinyClaw** | 0 | 0 | None | **Inactive** |
| **Moltis** | 2 (2 open) | 3 (3 open) | None | **Low** – No PRs merged, no releases, low community engagement |
| **CoPaw** | 32 (15 open) | 33 (10 open) | v1.1.11-beta.1 | **Very High** – 17 issues closed, 23 PRs merged; strongest community engagement |
| **ZeptoClaw** | 0 | 0 | None | **Inactive** |
| **ZeroClaw** | 32 (27 open) | 50 (35 open) | None | **High** – 15 PRs merged, 5 bugs closed, active RFC discussions |

**Health Score Methodology:** Based on throughput (merged PRs + closed issues), issue/PR closure rate, maintainer responsiveness, and severity of open blockers. "Inactive" projects receive no score.

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale and breadth:** 500 issues/PRs daily dwarfs all other projects—no other ecosystem participant operates at this volume. OpenClaw is the de facto reference implementation.
- **Integration surface:** Supports Discord, Slack, Telegram, Feishu, QQBot, Matrix, Mattermost, WebChat; no other project matches channel diversity.
- **Codex runtime parity:** The ongoing parity effort between Codex and Pi runtimes is unique and strategically important as OpenAI migrates to Codex.
- **SQLite migration:** Systematic branch-by-abstraction approach to session persistence is more disciplined than ad-hoc fixes seen in other projects.

**Technical approach differences:**
- OpenClaw uses a **monolithic TypeScript** codebase with plugin architecture, contrasting with **IronClaw's Rust** (performance-focused), **ZeroClaw's Rust** (lightweight agent runtime), and **PicoClaw's Go** (embedded-friendly).
- Higher abstraction level: OpenClaw abstracts provider differences through a runtime parity layer; ZeroClaw and PicoClaw work closer to the metal.

**Community size comparison:**
- OpenClaw has the largest community by absolute numbers (350 open issues, 391 open PRs), but this creates **bottlenecks**—many P1 bugs remain unaddressed for weeks (Slack silent disconnect since April 27).
- **CoPaw** exhibits the healthiest community dynamics (32 issues, 33 PRs, rapid closure) despite smaller absolute volume.
- **ZeroClaw** shows strong engagement with 32 issues and 50 PRs, with higher closure efficiency than OpenClaw.
- **NanoBot** (59 PRs merged) and **IronClaw** (8 PRs merged) demonstrate high per-developer throughput.

**Verdict:** OpenClaw is the ecosystem's cornerstone but is showing signs of **maintenance overload**. Its position is secure as the most comprehensive reference, but the community's patience is being tested by long-standing regressions. Fork projects (PicoClaw, NanoClaw) are exploiting OpenClaw's complexity to target specific niches.

---

## 4. Shared Technical Focus Areas

Multiple projects are converging on the following requirements—these constitute **ecosystem-wide priorities**:

| Focus Area | Projects Involved | Specific Needs |
|------------|------------------|----------------|
| **MCP (Model Context Protocol) reliability** | OpenClaw, NanoBot, LobsterAI, ZeroClaw | SSRF guards, reconnection logic, tool inheritance by subagents, managed installs with node awareness |
| **Provider compatibility & parity** | OpenClaw, NanoBot, PicoClaw, LobsterAI, CoPaw | OpenAI Responses transport, Azure AAD auth, Volcano Engine, DeepSeek caching, MiniMax image support, Ollama stability |
| **Session state management** | OpenClaw, PicoClaw, ZeroClaw, Moltis | SQLite migration, cron job preservation, session reset carryover, compaction stability, history capping |
| **Transport reliability** | OpenClaw, NanoClaw, PicoClaw | Silent disconnection (Slack, Matrix), DM registration (Signal, WhatsApp), message duplication, reconnect logic |
| **Security hardening** | NanoBot, LobsterAI, ZeroClaw, OpenClaw | Symlink workspace escapes, SSRF guards, sensitive data masking, shell command confirmation tiers |
| **Multi-agent orchestration** | OpenClaw, NanoBot, IronClaw, LobsterAI, CoPaw | Subagent completion delivery, MCP tool inheritance, durable execution, trigger lifecycle hooks |
| **Observability & debugging** | ZeroClaw, IronClaw, OpenClaw | Structured observability, loop exit tracing, compaction outcome logging, OTel correlation |
| **UI/UX improvements** | OpenClaw, CoPaw, ZeroClaw, LobsterAI | Slash commands, tool call display, i18n consistency, progress indicators, session tags |
| **Desktop/hardware integration** | Moltis, ZeroClaw, PicoClaw | Browser automation (Shadow DOM), local STT, ESP32 simulator, WASM component model |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | IronClaw | ZeroClaw | CoPaw | PicoClaw |
|-----------|----------|---------|----------|----------|-------|----------|
| **Primary language** | TypeScript | Python | Rust | Rust | TypeScript | Go |
| **Target user** | Power users/developers | Developers (Python ecosystem) | Production operators | CLI-first developers | UI-first power users | Embedded/lightweight deployers |
| **Architecture** | Monolithic + plugins | Modular (agents, hooks) | Microservice (Reborn) | Lightweight runtime | Full-stack (web + desktop) | Minimal gateway |
| **Key strength** | Channel breadth, provider parity | Memory management, run hooks | Durability, subagent scalability | Resource efficiency, WASM | Desktop UX, community engagement | Low footprint, fast iteration |
| **Key weakness** | Maintenance bottleneck, regression risk | Smaller community, fewer channels | Pre-release, limited external feedback | Under development, few channels | Chinese-centric issues (Feishu) | Limited features vs OpenClaw |
| **Release cadence** | Weekly stable + nightly | Unclear (no release today) | No tagged release | Between v0.8.0 milestones | Beta patches | Nightly builds |
| **Community dynamic** | Large but strained | Contributor-friendly | Internal team-focused | Active RFC process | Most engaged | Rapid bug turnaround |

**Key insight:** The ecosystem is **fragmenting by language and deployment target** while **converging on functionality**. IronClaw and ZeroClaw are betting on Rust for performance and safety; PicoClaw chooses Go for simplicity; OpenClaw maintains TypeScript dominance through sheer scale. This fragmentation creates portability challenges for users but drives healthy competition.

---

## 6. Community Momentum & Maturity

**Tier 1 – High velocity, rapid iteration:**
- **IronClaw** – Most intense development cycle; Reborn migration is a ground-up rewrite. High core-team throughput but no external community contributions visible. Pre-release stage—high risk, high reward.
- **ZeroClaw** – Fast-moving with 50 PRs daily; strong RFC culture (A2A, observability). Between minor releases; structured release planning.
- **CoPaw** – Best community health score. 23 PRs merged + 17 issues closed in 24h. Beta patches indicate stabilization phase.
- **NanoBot** – 59 PRs merged, high community contributor engagement (Azure AAD by external contributor). Maturing but still feature-adding.

**Tier 2 – Moderate momentum, stabilizing:**
- **OpenClaw** – Paradoxically both the most active and most bottlenecked. High issue churn but low resolution rate for P1s. The project is **too large for its governance model**. Users are vocal about regressions.
- **LobsterAI** – All 16 PRs merged; Cowork and MCP features signal productization. Moderate volume but high quality.
- **PicoClaw** – Rapid bug turnaround (12 merged PRs) but small scope. Nightly builds indicate aggressive testing.

**Tier 3 – Low activity, niche focus:**
- **NanoClaw** – Low volume but quality work on WhatsApp and Signal channels.
- **Moltis** – Lowest engagement; 0 PRs merged, 2 feature requests with no maintainer response. Risk of stagnation.

**Inactive:** NullClaw, TinyClaw, ZeptoClaw.

**Maturity assessment:**
- **Most production-ready:** NanoBot, CoPaw (beta), LobsterAI
- **Most innovative (but unstable):** IronClaw (Reborn), ZeroClaw (WASM, A2A)
- **Most mature (but creaky):** OpenClaw

---

## 7. Trend Signals

### From community feedback, the following industry trends are validated:

1. **Shift from "chat" to "reliable agent infrastructure"** – Users consistently demand durability (subagent completion delivery, session survival across restarts), not just conversational polish. Projects that address this (IronClaw, OpenClaw's SQLite migration) lead.

2. **Multi-provider flexibility is table stakes** – No project can afford vendor lock-in. The top requests span Azure AAD, OpenAI Codex, DeepSeek, Volcano Engine, Ollama, Gemini, MiniMax. Dynamic model catalogs (OpenClaw PR #90029, ZeroClaw #7100) are the emerging solution.

3. **Security and safety are rising priorities** – SSRF guards (NanoBot), shell command confirmation tiers (ZeroClaw), workspace escape prevention (NanoBot), and sensitive data masking (OpenClaw) show the ecosystem maturing from "it works" to "it's safe."

4. **MCP is the universal integration standard** – Five of seven active projects (OpenClaw, NanoBot, LobsterAI, ZeroClaw, CoPaw) are investing in MCP reliability. MCP SSRF guards, re

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-05

## 1. Today's Overview

NanoBot saw extremely high development activity over the past 24 hours, with 75 pull requests updated (59 merged or closed) and 6 issues updated (2 still open). This burst of work signals maintainers are aggressively landing features, bug fixes, and test improvements. No new releases were cut, but the volume of merged code suggests a release may be imminent. Two open issues remain active: a long-standing feature request for task-specific model configuration (#912) and a newly filed request for Volcano Engine image generation (#4196). The community continues to be responsive, with several bug reports closed the same day via linked PRs.

## 2. Releases

No new releases today.

## 3. Project Progress

The following key features and fixes were merged or closed in the last 24 hours:

- **Azure AAD Authentication** – PR [#4126](https://github.com/HKUDS/nanobot/pull/4126) (closed) adds support for Azure Identity‑based auth for the Azure OpenAI provider, resolving issue [#4125](https://github.com/HKUDS/nanobot/issues/4125).
- **Run‑Level Agent Hooks** – PR [#4176](https://github.com/HKUDS/nanobot/pull/4176) (closed) introduces `before_run`, `after_run`, `on_error`, and `on_finally` callbacks for agent runs, with `CompositeHook` fan‑out support.
- **CLI WebUI Fix under uv** – PR [#4164](https://github.com/HKUDS/nanobot/pull/4164) (closed) makes `CliAppManager` fall back to `uv pip` when `pip` is unavailable, fixing issue [#4158](https://github.com/HKUDS/nanobot/issues/4158).
- **Memory Management Enhancement** – PR [#4191](https://github.com/HKUDS/nanobot/pull/4191) (closed, title in Chinese: “增强memory管理”) improves memory handling.
- **MCP Reconnection Fix** – PR [#4027](https://github.com/HKUDS/nanobot/pull/4027) (closed) resets `_mcp_connected` on session drop and adds reconnect callbacks.
- **OpenAI‑Compatible Tool Call IDs** – PR [#3984](https://github.com/HKUDS/nanobot/pull/3984) (closed) stops replacing provider‑returned tool call IDs, fixing ID mismatches for GLM‑4.7 / Kimi 2.6.
- **WebUI Fork‑From‑Here** – PR [#4163](https://github.com/HKUDS/nanobot/pull/4163) (closed) adds a fork icon for user messages, allowing revision and provenance tracking.
- **New Chat Keyboard Shortcut** – Issue [#4178](https://github.com/HKUDS/nanobot/issues/4178) (closed) added `Cmd/Ctrl+Shift+O` to start a new chat in WebUI (good first issue).
- **Deterministic Tests** – PR [#4189](https://github.com/HKUDS/nanobot/pull/4189) (closed) replaced timing‑based waits with deterministic patterns across command, agent, and channel tests.

Open PRs that have been active for several days and are likely to land soon include:

- [#4123](https://github.com/HKUDS/nanobot/pull/4123) – MCP SSRF guard for unsafe HTTP URLs
- [#4119](https://github.com/HKUDS/nanobot/pull/4119) – Block relative symlink workspace escapes
- [#3968](https://github.com/HKUDS/nanobot/pull/3968) – `/skill` slash command to list enabled skills
- [#4192](https://github.com/HKUDS/nanobot/pull/4192) – Allow subagents to inherit MCP tools
- [#4190](https://github.com/HKUDS/nanobot/pull/4190) – Stricter tool call validation

## 4. Community Hot Topics

The most engaging issues and PRs by comment count and reactions:

- **Issue #912 – Task‑Specific Model Configuration**  
  [Issue #912](https://github.com/HKUDS/nanobot/issues/912) (4 comments, 3 👍)  
  *Needs:* Allow separate model configs for conversational, tool‑use, and browser‑use tasks. This is the longest‑standing open feature request (since Feb 2026). Users want granularity beyond a single global model.

- **Issue #1121 – Fallback Model Not Triggered on Timeout**  
  [Issue #1121](https://github.com/HKUDS/nanobot/issues/1121) (3 comments, 3 👍)  
  *Needs:* When the primary model returns a timeout/503, fallback models are ignored. This reliability issue was closed with a fix (likely in PR #4176 or related hook changes).

- **PR #3968 – `/skill` Command**  
  [PR #3968](https://github.com/HKUDS/nanobot/pull/3968) (multiple updates, ongoing)  
  *Needs:* Users requested a way to discover enabled skills (linked to issue #3959). The PR is still open but has seen recent maintainer activity.

- **Issue #4196 – Volcano Engine Image Generation**  
  [Issue #4196](https://github.com/HKUDS/nanobot/issues/4196) (new, 0 comments yet)  
  *Needs:* A user wants support for the `Seedream 5.0 Lite` image model from Volcano Engine. This indicates demand for more regional/Chinese AI providers.

## 5. Bugs & Stability

Four bugs were reported/updated today, all with corresponding fixes (merged or in open PRs). Ranked by severity:

1. **Medium‑High: Fallback model not triggered on LLM timeout**  
   [#1121](https://github.com/HKUDS/nanobot/issues/1121) (closed) – Primary model failures (Gemini 503) were not falling back. Fixed via run‑level hook lifecycle [#4176](https://github.com/HKUDS/nanobot/pull/4176) and likely additional changes.

2. **Medium: MCP HTTP URL SSRF vulnerability**  
   [#4123](https://github.com/HKUDS/nanobot/pull/4123) (open PR) – Unsafe HTTP URLs in MCP SSE/streamable connections could bypass SSRF checks. A shared guard and `httpx` request hook are being added.

3. **Medium: Relative symlink workspace escape**  
   [#4119](https://github.com/HKUDS/nanobot/pull/4119) (open PR) – Restricted exec commands could follow relative symlinks outside the workspace. Proposed fix blocks relative path symlink traversal.

4. **Low: WebUI CLI App fails under `uv tool`**  
   [#4158](https://github.com/HKUDS/nanobot/issues/4158) (closed) – `pip` not available when NanoBot is installed via uv. Fixed in [#4164](https://github.com/HKUDS/nanobot/pull/4164) by falling back to `uv pip`.

Additionally, PR [#4197](https://github.com/HKUDS/nanobot/pull/4197) (open) fixes DM pairing issues for Weixin and Telegram, including a routing problem for denied senders.

## 6. Feature Requests & Roadmap Signals

Active requests likely to shape the next release:

- **Task‑Specific Model Configuration** (#912) – The most‑voted issue. Given its age and continued discussion, it may be included in the upcoming version.
- **Azure AAD Authentication** – Already merged (#4126), so production users with Azure policies can now use identity‑based auth.
- **Volcano Engine Image Generation** (#4196) – Filed today; if the community shows interest, it could be added soon (the existing provider architecture makes it relatively straightforward).
- **Subagent MCP Tool Inheritance** (#4192, open PR) – Enables spawned subagents to reuse the parent’s MCP tools, a common request for complex multi‑agent flows.
- **Improved Tool Call Validation** (#4190, open PR) – Makes near‑miss tool names and scalar arguments produce explicit errors instead of silently guessing, increasing reliability.
- **Desktop Shell** (#4195, open PR) – A new “desktop host” surface that shares the WebUI experience. This may be the first step toward a standalone desktop application.
- **Memory Lifecycle Test Harness** (#4193, open PR) – Adds scripted tests for the full memory pipeline (sessions → Consolidator → GitStore). Indicates the team is hardening the memory subsystem.

## 7. User Feedback Summary

User sentiment is generally positive, with several pain points being addressed quickly:

- **Pain points expressed:**
  - *Fallback failure*: “The configured fallback models are not triggered” – a core reliability concern that is now fixed.
  - *Missing skill discoverability*: “No way to discover which skills are available” – resolved by the `/skill` command (PR #3968).
  - *Corporate auth restrictions*: “Azure subscriptions do not allow API key‑based auth” – solved by the Azure AAD PR.
  - *Installation difficulty under uv*: “No module named pip” – fixed by the uv‑aware fallback.
  - *New provider request*: “NanoBot does not support Volcengine’s Seedream 5.0 Lite” – a new feature request indicating users want broader model access.

- **Satisfaction signals:**
  - Multiple issues closed within hours of being reported (#4158, #4178).
  - High number of merged PRs (59) shows maintainers are actively responding.
  - Community contributors are landing non‑trivial changes (e.g., Azure AAD auth by @kunalk16, MCP reconnection by @bjoshuanoah).

## 8. Backlog Watch

The following items have been open for an extended period or lack recent maintainer attention:

- **Issue #912 – Task‑Specific Model Configuration**  
  Created February 20, 2026. Last updated June 4, 2026. While it has recent activity, it remains open and is marked `[stale]`. It is the most‑voted feature request and should be a priority for the maintainers.

- **PR #3968 – `/skill` Command**  
  Created May 23, 2026. Still open despite being a relatively small change. It has `[enhancement, valid]` labels but no maintainer merge. May need final review.

- **PRs #3982, #3983 – Agent Runner Harness and Tool‑Call Finish Reasons**  
  Both created May 24, 2026. These are test‑only PRs that have been updated recently but not merged. They may be waiting on other refactors or review bandwidth.

- **No maintainer response on #4196 yet** – Filed today, but given the high activity it may be addressed quickly.

Overall, the backlog is manageable; the main concern is the long‑dormant #912 which could become a user frustration if left unresolved much longer.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw Project Digest — 2026-06-05

### 1. Today's Overview
The project saw **very high activity** over the last 24 hours, with **22 pull requests updated** (12 merged/closed) and **6 issues updated** (4 closed). A new **nightly build** (v0.2.9-nightly) was released, reflecting an intense focus on bug fixing and code quality improvements. The maintainer team has been responsive, merging fixes for high-impact bugs such as the singleton PID crash loop, Codex OAuth tool‑call drops, and a broken OneBot group‑chat reply. Two open issues remain (a context display bug and a OneBot routing error), each with an associated open PR. Overall project health is strong, with rapid turnover of both issues and PRs.

### 2. Releases
- **nightly (v0.2.9-nightly.20260605.5224b9a4)** — Automated nightly build, potentially unstable. No migration notes are provided; this is primarily a pre‑release snapshot for testing.

### 3. Project Progress
The following notable fixes were merged today:

- **PID singleton crash loop** – [#3000](https://github.com/sipeed/picoclaw/pull/3000) verifies that a process with the stored PID is actually a picoclaw gateway, preventing startup failure when the PID has been reused.
- **Codex OAuth tool‑call loss** – [#3007](https://github.com/sipeed/picoclaw/pull/3007) preserves function calls emitted by Codex streaming responses even when the final output array is empty.
- **Makefile build fix** – [#2999](https://github.com/sipeed/picoclaw/pull/2999) and [#2976](https://github.com/sipeed/picoclaw/pull/2976) handle spaces in `go env GOVERSION` (e.g., `go1.25.10 X:nodwarf5`).
- **JSON marshalling errors** – [#2996](https://github.com/sipeed/picoclaw/pull/2996) replaces 7 silent `json.Marshal` failures in shell tool responses with proper error handling.
- **Dependency bumps** – Updated larksuite SDK (v3.7.5 → v3.9.4, with breaking‑change fix in [#3008](https://github.com/sipeed/picoclaw/pull/3008)), AWS bedrockruntime SDK, SQLite, and Anthropic SDK.

**Open PRs** (not yet merged) include fixes for OneBot group‑chat routing ([#3009](https://github.com/sipeed/picoclaw/pull/3009)), the `/context` display bug ([#2985](https://github.com/sipeed/picoclaw/pull/2985)), and workspace guard improvements ([#3001](https://github.com/sipeed/picoclaw/pull/3001)).

### 4. Community Hot Topics
- **`/context` always shows `Compress at: 76800 tokens`** ([#2968](https://github.com/sipeed/picoclaw/issues/2968)) — Users are confused because only the hard compression threshold is shown, not the soft summarization trigger. The issue has **4 comments** and **1 👍**. A fix is in progress (PR [#2985](https://github.com/sipeed/picoclaw/pull/2985)) that will display both thresholds.
- **OneBot group‑chat uses wrong API** ([#3002](https://github.com/sipeed/picoclaw/issues/3002)) — New user report (0 comments yet) about group replies being sent as private messages. PR [#3009](https://github.com/sipeed/picoclaw/pull/3009) addresses the root cause (missing `group:` prefix in chat ID).

### 5. Bugs & Stability
| Severity | Bug | Status & Fix PR |
|----------|-----|-----------------|
| **High** | Stale PID causes gateway crash loop on startup | Fixed by [#3000](https://github.com/sipeed/picoclaw/pull/3000) (merged) |
| **High** | Codex OAuth GPT-5.5 drops tool calls (empty response) | Fixed by [#3007](https://github.com/sipeed/picoclaw/pull/3007) (merged) |
| **Medium** | OneBot group replies sent via `send_private_msg` | Fix in [#3009](https://github.com/sipeed/picoclaw/pull/3009) (open) |
| **Medium** | `/context` only shows compression threshold, not summarization | Fix in [#2985](https://github.com/sipeed/picoclaw/pull/2985) (open) |
| **Low** | Workspace guard blocks scheme‑less URLs (e.g., `curl wttr.in/Beijing`) | Fix in [#3001](https://github.com/sipeed/picoclaw/pull/3001) (open) |
| **Low** | Unchecked type assertions could cause panics in several paths | Fixes in [#3011](https://github.com/sipeed/picoclaw/pull/3011) and [#3010](https://github.com/sipeed/picoclaw/pull/3010) (open) |
| **Fixed** | Web UI message chaos after upgrade to v0.2.9 | Closed [#2972](https://github.com/sipeed/picoclaw/issues/2972) |

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. The current development rhythm is clearly **bug‑fix oriented**, with emphasis on **stability** and **edge‑case hardening**. Signals for future releases include:
- Improved **workspace guard** flexibility for non‑HTTP URLs ([#3001](https://github.com/sipeed/picoclaw/pull/3001)).
- **WhatsApp native mode** support via `use_native` flag ([#2934](https://github.com/sipeed/picoclaw/pull/2934), open since May 24).
- **Anthropic model ID fix** for `claude-sonnet-4-6` ([#2947](https://github.com/sipeed/picoclaw/pull/2947), open since May 26).
- **Documentation update** for v0.2.9 changes ([#2981](https://github.com/sipeed/picoclaw/issues/2981), closed today).

These suggest that v0.3.0 may include more robust channel handling and better self‑diagnostics.

### 7. User Feedback Summary
Reported pain points centre on **upgrade regressions** (Web UI history chaos after v0.2.9), **provider‑specific tool‑call issues** (Codex), and **configuration confusion** (display of compress vs. summarise thresholds). One user on **FreeBSD** and **MiniMax** provider reported multiple issues ([#2968](https://github.com/sipeed/picoclaw/issues/2968), [#2972](https://github.com/sipeed/picoclaw/issues/2972)), indicating cross‑platform testing is active. The maintainer team has been **responsive**, merging fixes for the most critical issues within 24 hours. Overall sentiment appears positive, as users see their bug reports acted upon swiftly.

### 8. Backlog Watch
The following open Issues/PRs have been unresolved for a week or more and may need maintainer attention:

- **PR [#2813](https://github.com/sipeed/picoclaw/pull/2813)** (PID verification) — Open since **May 7**. A more complete fix (PR [#3000](https://github.com/sipeed/picoclaw/pull/3000)) was merged today, so this older PR should likely be closed.
- **PR [#2947](https://github.com/sipeed/picoclaw/pull/2947)** (Anthropic model ID) — Open since **May 26**, marked `[stale]`. Small fix, but no activity.
- **PR [#2934](https://github.com/sipeed/picoclaw/pull/2934)** (WhatsApp native mode) — Open since **May 24**, marked `[stale]`. Adds valuable functionality.
- **PR [#2956](https://github.com/sipeed/picoclaw/pull/2956)** (Channel enabled state merge) — Open since **May 27**, needs review.
- **Issue [#2968](https://github.com/sipeed/picoclaw/issues/2968)** (`/context` display) — Open since **May 30**; fix PR [#2985](https://github.com/sipeed/picoclaw/pull/2985) is open and should be merged soon.
- **Issue [#3002](https://github.com/sipeed/picoclaw/issues/3002)** (OneBot group chat) — Opened yesterday; fix PR [#3009](https://github.com/sipeed/picoclaw/pull/3009) exists and should be prioritised.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-05

## Today’s Overview  
NanoClaw maintained a moderate activity level on 2026-06-04, with 8 pull requests updated and 1 new issue opened. Three PRs were closed or merged, addressing WhatsApp session bugs, voice transcription infrastructure, and type safety improvements. No new releases were published. The single open issue is a low-effort travel request, while the PR pipeline shows concentrated work on Signal and WhatsApp channel stability, plus documentation for recently shipped features. Overall, the project appears healthy, with maintainers actively reviewing contributions.

## Releases  
No new releases today.

## Project Progress  
Three pull requests were closed or merged in the last 24 hours:

- **[#2687 – [follows-guidelines] Trip agent](https://github.com/nanocoai/nanoclaw/pull/2687)** (closed) — A new skill for trip planning was contributed. The PR follows contributing guidelines and is likely being evaluated for inclusion.
- **[#2633 – Fix/whatsapp self destruct and shutdown auth wipe](https://github.com/nanocoai/nanoclaw/pull/2633)** (closed) — Fixes two structural bugs in `src/channels/whatsapp.ts` that caused WhatsApp authentication to be wiped on Baileys 7.x, making paired sessions unreliable when `WHATSAPP_PHONE_NUMBER` is set.
- **[#104 – fix: replace `as any` casts with proper BoomError type](https://github.com/nanocoai/nanoclaw/pull/104)** (closed) — Improves type safety by defining a `BoomError` interface and removing unsafe `as any` casts in WhatsApp disconnect handling.

These merges indicate ongoing investment in WhatsApp channel robustness and code quality.

## Community Hot Topics  
No issues or PRs attracted comments or reactions today, so attention is inferred from technical substance:

- **[#2688 – fix(whatsapp): stop translating group participants to phone JIDs](https://github.com/nanocoai/nanoclaw/pull/2688)** — This open PR addresses a silent failure (ack error 421) when WhatsApp groups migrate to LID (LinkedID) participant addressing. The fix is critical for bot reliability and is actively discussed.
- **[#2689 – fix(signal): set isMention for DMs and use signal: prefix for platform IDs](https://github.com/nanocoai/nanoclaw/pull/2689)** — Fixes Signal DM registration where first messages were dropped because `isMention` wasn’t set. A foundational fix for Signal support.
- **[#2685 – docs(signal): group typing, outbound reactions, quote-reply fix](https://github.com/nanocoai/nanoclaw/pull/2685)** — Documentation updates reflecting new Signal capabilities (group typing indicators, outbound reactions) that were recently shipped.

These PRs highlight core channel integration work that is vital for users relying on Signal and WhatsApp.

## Bugs & Stability  
No new bug reports were filed today, but multiple PRs target stability issues:

- **High severity**: [PR #2688](https://github.com/nanocoai/nanoclaw/pull/2688) prevents silent message drops in LID-addressed WhatsApp groups. Without this fix, bot replies never arrive and an error 421 is logged. A corresponding fix PR exists.
- **Medium severity**: [PR #2689](https://github.com/nanocoai/nanoclaw/pull/2689) resolves Signal DM registration failures where the first message was silently discarded.
- **Medium severity**: [PR #2633](https://github.com/nanocoai/nanoclaw/pull/2633) (already merged) fixes self-destructing WhatsApp auth.
- **Low severity**: [PR #2405](https://github.com/nanocoai/nanoclaw/pull/2405) (still open) prevents malformed XML output after auto-compaction in the poll loop.

Overall, the WhatsApp and Signal channels are receiving targeted fixes to eliminate silent failures.

## Feature Requests & Roadmap Signals  
- **[#2687 – Trip agent](https://github.com/nanocoai/nanoclaw/pull/2687)** — A new skill for travel planning was contributed, suggesting user interest in agent capabilities beyond chat.
- **[#2459 – feat(skill): add /add-voice-transcription-chat-sdk](https://github.com/nanocoai/nanoclaw/pull/2459)** — This PR (still open) adds on-device voice transcription for Discord, Slack, Teams, Webex, and Google Chat via local whisper.cpp. It requires no cloud API, signaling a strong community desire for privacy-preserving audio features.
- **[#2685 – docs(signal): group typing, outbound reactions, quote-reply fix](https://github.com/nanocoai/nanoclaw/pull/2685)** — Documents features that have already been implemented, indicating that Signal group typing and reactions will be in the next release if not already.

Given the momentum, the next release is likely to include Signal group typing/reactions, WhatsApp LID support fix, and the voice transcription skill if #2459 is merged.

## User Feedback Summary  
The only user-created item today is Issue [#2686 – Traveling](https://github.com/nanocoai/nanoclaw/issues/2686), which simply states “I want to travel to Canada.” This lacks context and may be a test or low-effort request. No other feedback, pain points, or satisfaction indicators were recorded today.

## Backlog Watch  
Two open PRs have been awaiting review or revision for several weeks:

- **[#2405 – fix(poll-loop): deliver unwrapped output to sole destination after compaction](https://github.com/nanocoai/nanoclaw/pull/2405)** — Created 2026-05-11, updated 2026-06-04. Addresses a recurring issue where the model drops XML wrapping after compaction, causing malformed messages. This fix could improve agent reliability for all channels.
- **[#2459 – feat(skill): add /add-voice-transcription-chat-sdk](https://github.com/nanocoai/nanoclaw/pull/2459)** — Created 2026-05-13, updated 2026-06-04. A substantial feature addition with broad channel support. Its prolonged open status may reflect complexity or maintainer bandwidth.

These items would benefit from a maintainer review to keep the project moving forward.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-05

## 1. Today's Overview

The IronClaw project remains in an intense, high‑velocity development phase, with **39 issues updated** and **50 pull requests updated** in the last 24 hours. Of those, **14 issues were closed** and **18 PRs were merged or closed**, reflecting a sustained push toward the “Reborn” architecture migration. Activity is concentrated on **durable subagent completion delivery**, **trigger lifecycle correctness**, **compaction stability**, and **Slack/WebUI v2 feature integration**. No new releases were published today, but the volume of merged code (8 PRs closed) and the resolution of several long‑standing bugs signal that a stable cut is approaching. The team is firing on all cylinders, with core contributors (henrypark133, serrrfirat, zmanian, italic‑jinxin, danielwpz) dominating the commit stream.

## 2. Releases

No new releases were created today. The project continues to operate without a tagged version; the latest published release remains `None`.

## 3. Project Progress

Eight pull requests were merged or closed today, advancing several critical feature areas:

- **[Slack Integration]** PR #4476 wires Slack actor/subject identity separation, allowing channel routes to execute under the configured subject while preserving the Slack sender as the actor. PR #4478 adds auth‑setup links to Slack prompts so users are guided to OAuth when capabilities require a missing credential.
- **[WebUI v2]** PR #4477 redesigns the LLM Providers settings panel to group providers by setup status, replacing a dense wall of metadata with a progressive‑disclosure UI. PR #4480 fixes provider grouping review feedback (collapsed inactive cards, defensive guards).
- **[Compaction & Stability]** PR #4440 introduces `LoopCompactionOutcome` to defer compaction on unstable transcript ranges, avoiding hard errors. PR #4467 caps model‑visible `builtin.http` results with body/header/size limits to prevent budget overruns.
- **[Trigger Lifecycle]** PR #4466 pairs the trigger creator during `builtin.trigger_create`, adding a lifecycle hook for composition‑owned side effects and rolling back triggers on hook failure.
- **[Dependencies / Security]** PR #3719 bumps `rustls‑webpki`, `ring`, and `aws‑lc‑rs` to address multiple security advisories (RUSTSEC‑2026‑0104, RUSTSEC‑2026‑0098, etc.).

Corresponding issue trackers that were closed today include the background subagent durability effort (#4348, #4349, #4350, #4358, #4437, #4438), trigger‑completion policy fix (#4420), one‑time trigger support (#4473), activation‑state for trigger creation (#4472), and Google OAuth token refresh (#4160).

## 4. Community Hot Topics

Most open issues and PRs have low comment counts (1–6), indicating that discussion stays within small core‑team threads. The single most‑commented issue is:

- **#3280** (6 comments, open since 2026‑05‑06) — [Reborn] Add ProductWorkflow and InboundTurnService facade. This is a parent issue for the entire Reborn product‑facing migration and remains a critical architectural item with multiple dependencies.

Other notable recent conversations:

- **#4424** (4 comments, closed) — “Reborn: builtin.spawn_subagent advertised but absent from structured tools.” This bug was quickly fixed, but the underlying need for **tool‑definition / surface‑text parity** is now tracked by open regression‑test issue #4431.
- **#4427** (2 comments, open) — “Loop exit reason invisible — LoopFailureKind never traced.” Operators cannot debug loop terminations; this is a direct user‑pain point for anyone running Reborn in production.
- **#3283** (2 comments, open) — Migrate OpenAI‑compatible chat/Responses APIs onto Reborn. A key roadmap item that will enable external API compatibility.

PRs have no visible comments, but the sheer volume (32 open PRs) suggests active review cycles, particularly around the **hooks framework** (PRs #3951, #3941, #3936, #3937, #3933, #3938) where no maintainer feedback has been posted recently.

## 5. Bugs & Stability

The following bugs were reported or updated today, ranked by severity:

| Severity | Issue | Symptom | Fix Status |
|----------|-------|---------|------------|
| **High** | #4424 (closed) | `spawn_subagent` tool advertised but not callable | Fixed via PR (merged) |
| **High** | #4427 (open) | Loop exit reason never logged; operators blind to termination cause | No fix PR yet |
| **High** | #4366 (open) | Compaction hard‑errors on UI‑only messages instead of deferring | Addressed by PR #4440 (merged today) |
| **Medium** | #4464 (open) | Compaction retry lacks stabilization metadata; unstable ranges can be retried indefinitely | Follow‑up tracked |
| **Medium** | #4431 (open) | No regression test for tool‑callability parity | New test needed |
| **Medium** | #4368 (open) | Six required fields made optional; `debug!` used in hot path | Architecture hygiene issue |
| **Low** | #4084 (closed) | Background subagent results never delivered to parent | Fixed via durable delivery series |
| **Low** | #4160 (closed) | Google OAuth refresh token not implemented | Fixed via follow‑up PR |

Several high‑severity issues were closed today, including the background subagent durability chain (#4348, #4349, #4350, #4358, #4437, #4438) and the trigger‑completion policy fix (#4420). The project’s stability posture is improving, but the open loop‑exit tracing issue (#4427) remains a significant operational gap.

## 6. Feature Requests & Roadmap Signals

All feature requests visible in today’s data originate from the core development team, not external users. The following features are in active implementation or planning, and may appear in the next release:

- **Durable Background Subagent Execution** — issue #4474 consolidates the umbrella for making subagent completions survive restarts and become observable. The design doc is already written; implementation PRs are being stacked.
- **Trigger Lifecycle Correctness** — issue #4475 consolidates completion, activation, and one‑time runs. PR #4466 (merged today) lays the foundation; follow‑ups for activation state and terminal cleanup are open.
- **Reborn Identity Resolver** — PR #4461 (open) introduces `ironclaw_reborn_identity` to provide a canonical user resolution layer for OAuth and external actors, replacing the Web‑specific `LibSqlUserStore`.
- **IronHub Skill/Extension Port** — PR #4479 (open) brings signed catalog verification, artifact downloads, and install flow to Reborn.
- **WebChat v2 First‑Run Onboarding** — PR #4481 (open) adds a provider‑choice screen for new users with NEAR AI / Codex login or API‑key entry.

These features align with the broader Reborn roadmap: making the agent framework production‑ready for multi‑platform, multi‑identity, long‑running scenarios.

## 7. User Feedback Summary

No direct user‑feedback comments were recorded (all issues are filed by the core team). However, the _nature_ of the bugs reported reveals common pain points for anyone deploying IronClaw‑based agents:

- **Tool‑callability confusion** (#4424): Model advertises capabilities it cannot actually invoke — a fundamental reliability issue.
- **Invisible loop exits** (#4427): Operators cannot determine why a turn ended, hampering debugging.
- **Compaction failures** (#4366): Users see hard errors where the system should gracefully defer.
- **Trigger misfires** (#4420): Triggers configured to fire once reappear every scheduled occurrence.
- **Subagent result loss** (#4084): Background tasks complete but parent never notified — a concurrency‑durability gap.

All of these are being actively addressed, and the closed bugs today suggest the team is responsive. The lack of external community comments likely reflects the project’s pre‑release stage — most interaction is internal.

## 8. Backlog Watch

Several important issues and PRs have received no recent maintainer attention and may require escalation:

- **#3280** (open, 2026‑05‑06) — [Reborn] Add ProductWorkflow and InboundTurnService facade. This is a parent with 12+ dependencies and no comments since update. It may be blocked or deprioritized.
- **#3283** (open, 2026‑05‑06) — Migrate OpenAI‑compatible APIs onto Reborn. Same age as #3280; stalled despite being a key roadmap item.
- **#4238** (open, 2026‑05‑29) — Project product‑auth accounts into CredentialAccountStore. Only one comment (author’s own); no review activity.
- **Open Hooks PRs (#3951, #3941, #3936, #3937, #3933, #3922, #3938)** — all from 2026‑05‑23, no new reviews or comments in over two weeks. These represent a significant feature area (durable predicate backends, third‑party hooks, security audit sinks) and may be at risk of bit‑rot.
- **#4381** (open, 2026‑06‑03) — Add canonical Reborn identity resolver. Opened alongside PR #4461; the PR is moving, but the issue itself lacks feedback.

Given the project’s current velocity, these items should be reassigned or re‑triaged to prevent them from lingering. The hooks stack, in particular, has multiple open PRs with no movement — a sign that reviewers may be overloaded by the Reborn integration wave.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-05

## Today's Overview
Project activity remains high, with **16 pull requests merged or closed** in the past 24 hours and zero open PRs. The majority of changes focus on **MCP reliability**, **Cowork voice & subagent improvements**, and **i18n polish**. A single open issue (#769) about an OpenClaw gateway startup failure persists without resolution. No new releases were cut today, though the `2026.5.28` release branch was merged back into `main`, indicating the team is consolidating recent feature work into a stable base.

## Releases
**No new releases** today. The most recent version is **2026.5.28**, whose release branch was merged into `main` via PR #2090. That release includes **73 commits** covering the Kit expert toolkit marketplace, Cowork session local forking, plugin manual updates, and assorted MCP/Gateway/Artifacts stability fixes. No breaking changes or migration notes have been issued.

## Project Progress
All 16 PRs updated in the last 24 hours are closed/merged. Key areas of progress:

- **Release consolidation**  
  [#2090](https://github.com/netease-youdao/LobsterAI/pull/2090): Merge `release/2026.5.28` to `main`.

- **MCP (Model Context Protocol) improvements**  
  - [#367](https://github.com/netease-youdao/LobsterAI/pull/367): Import `userData/mcp.json` into SQLite MCP store; clarify SSE vs Streamable HTTP UI.  
  - [#2091](https://github.com/netease-youdao/LobsterAI/pull/2091): Optimise npx MCP startup by pre-resolving packages; add first‑response timing logs.  
  - [#2100](https://github.com/netease-youdao/LobsterAI/pull/2100): Ensure managed MCP installs are node‑aware; fallback to raw stdio if managed launch fails.  
  - [#2103](https://github.com/netease-youdao/LobsterAI/pull/2103): Validate remote MCP server URLs with shared logic and user‑visible error messages.

- **Cowork (multi‑agent collaboration) fixes & features**  
  - [#2111](https://github.com/netease-youdao/LobsterAI/pull/2111): Split voice input modules (ASR IPC, recording, encoding) into focused modules.  
  - [#2110](https://github.com/netease-youdao/LobsterAI/pull/2110): Guard oversized OpenClaw image payloads with payload estimation and error classification.  
  - [#2095](https://github.com/netease-youdao/LobsterAI/pull/2095): Subagent batch deletion – include subagent sessions in sidebar selection and async transcript cleanup.  
  - [#1536](https://github.com/netease-youdao/LobsterAI/pull/1536): System notifications when Cowork sessions complete or fail.  
  - [#1538](https://github.com/netease-youdao/LobsterAI/pull/1538): Bookmark/favourite AI replies with star icon and persistent storage.  
  - [#1542](https://github.com/netease-youdao/LobsterAI/pull/1542): Session tag classification system – create, delete, auto‑suggest, and filter tags in sidebar.

- **Model support**  
  - [#2093](https://github.com/netease-youdao/LobsterAI/pull/2093): Enable image input for MiniMax-M3 (was incorrectly hardcoded as `supportsImage: false`).

- **Plugins & UI fixes**  
  - [#2096](https://github.com/netease-youdao/LobsterAI/pull/2096): Hide internal OpenClaw runtime‑bundled plugins from management UI.  
  - [#1540](https://github.com/netease-youdao/LobsterAI/pull/1540): Fix missing i18n for “edit” button in memory module settings.  
  - [#1543](https://github.com/netease-youdao/LobsterAI/pull/1543): Fix hardcoded Chinese strings in approval dialogs (e.g., Cowork dangerous operations) when app language is English.  
  - [#1544](https://github.com/netease-youdao/LobsterAI/pull/1544): Stop GitHub Copilot OAuth polling when Settings panel is closed, preventing background abuse and silent token loss.

## Community Hot Topics
The only open issue receiving any interaction is:

- **[#769 [Open] OpenClaw 网关未能在规定时间内启动成功](https://github.com/netease-youdao/LobsterAI/issues/769)**  
  Created 2026-03-24, updated 2026-06-04, 1 comment. The user posted a screenshot (1200x800) and asked “这是什么问题啊？” (What is this issue?). The underlying need is **reliable OpenClaw gateway startup** – a potential blocker for users who depend on the gateway for MCP or Cowork operations. The project has since merged multiple MCP/gateway‑related fixes (e.g., payload size guards, URL validation), but the original startup timeout has not been explicitly addressed.

No other issues or PRs have attracted reactions or additional comments in the past 24 hours.

## Bugs & Stability
The following bugs were fixed today (all merged):

| Bug | Severity | Fix PR |
|-----|----------|--------|
| OpenClaw gateway fails to start (#769) – **unresolved** | **High** – blocks gateway‑dependent features | No fix yet |
| Oversized image payloads cause `1009` max‑payload failure in OpenClaw | Medium | [#2110](https://github.com/netease-youdao/LobsterAI/pull/2110) |
| MiniMax-M3 image input disabled due to hardcoded `false` | Medium | [#2093](https://github.com/netease-youdao/LobsterAI/pull/2093) |
| Subagent sessions not deletable in batch | Low | [#2095](https://github.com/netease-youdao/LobsterAI/pull/2095) |
| Internal OpenClaw plugins visible to users | Low | [#2096](https://github.com/netease-youdao/LobsterAI/pull/2096) |
| MCP managed installs lost node awareness when Electron shim differed | Medium | [#2100](https://github.com/netease-youdao/LobsterAI/pull/2100) |
| Remote MCP server URLs accepted without validation | Medium | [#2103](https://github.com/netease-youdao/LobsterAI/pull/2103) |
| i18n missing for “edit” button in memory module | Low | [#1540](https://github.com/netease-youdao/LobsterAI/pull/1540) |
| Hardcoded Chinese strings in approval dialogs break English mode | Medium | [#1543](https://github.com/netease-youdao/LobsterAI/pull/1543) |
| GitHub Copilot OAuth polling continues after Settings panel close | Medium | [#1544](https://github.com/netease-youdao/LobsterAI/pull/1544) |

Additionally, a stale fix [#367](https://github.com/netease-youdao/LobsterAI/pull/367) improved MCP config import, potentially resolving misconfiguration issues.

## Feature Requests & Roadmap Signals
The following user‑visible features have been implemented in the **2026.5.28 release** (merged today) and are likely to appear in the next stable version:

- **Kit (Expert Toolkit) Marketplace** – browse, install, uninstall kits with try‑asking integration.
- **Cowork Session Local Fork** – duplicate a Cowork session locally for experimentation.
- **Plugin Manual Update** – trigger plugin updates on demand.
- **Bookmark AI Messages** – star important replies for quick reference.
- **Session Tags** – categorise Cowork conversations with custom tags.
- **System Notifications for Cowork** – real‑time alerts when a multi‑agent task finishes or fails.

These features directly address user requests for **better organisation** (tags, bookmarks), **visibility** (notifications), and **manageability** (kits, plugin updates). Given the team’s pace, the next release may include further MCP performance improvements (npx pre‑resolution) and the voice input refactor (#2111) now in `main`.

## User Feedback Summary
Only one piece of direct user feedback surfaced today – the reporter of issue #769 who is experiencing **OpenClaw gateway startup timeout**. This appears to be a recurring pain point (issue opened 2+ months ago) that the team has partially addressed through image payload handling and URL validation, but the root cause of the gateway failing to start in time remains unclear.

Other indirect signals from merged PRs indicate users were frustrated by:

- i18n inconsistencies (English UI showing Chinese text).
- Copilot OAuth polling lingering after closing settings.
- Inability to batch‑delete subagent sessions.
- Internal plugins cluttering the plugin management UI.

Satisfaction is likely high for the Cowork improvements (tags, bookmarks, notifications) and MCP startup speed gains, as these directly improve daily workflows.

## Backlog Watch
- **[Issue #769](https://github.com/netease-youdao/LobsterAI/issues/769) – OpenClaw gateway startup failure**  
  Open since 2026-03-24, updated but **unresolved**. The project has merged several gateway‑adjacent fixes (payload size, URL validation) but none that explicitly address the startup timeout. This issue should be considered **high‑priority** as it blocks all features that depend on the OpenClaw gateway (Cowork subagents, MCP remote servers). Maintainers have not commented recently. A dedicated investigation and fix are overdue.

No other issues or PRs show signs of long‑term neglect. The 16 merged PRs today clear the current queue effectively.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-05

## 1. Today’s Overview
The Moltis repository saw moderate activity over the last 24 hours, with **2 new or updated issues** and **3 pull requests** receiving updates (all still open). No PRs were merged or closed, and no new releases were published. Development effort appears concentrated on improving the browser automation tool’s ability to interact with Shadow DOM elements (PRs #1100 and #1103) and on capping persisted tool results to prevent memory/resource issues (PR #1089). Meanwhile, the community is requesting expanded speech-to-text engine support and new messaging channels (SMS, LINE). Overall, the project is actively maintained, though no code has been integrated today.

## 2. Releases
*No new releases were published on or before 2026-06-05.* None to detail.

## 3. Project Progress
**No PRs were merged or closed today.** Three PRs remain open and under review:

- **#1103** – `fix(browser): pierce shadow DOM lookups efficiently` (alternative to #1100, includes review fixes)  
- **#1100** – `fix(browser): pierce open shadow roots in snapshot and ref lookups` (initial fix)  
- **#1089** – `Cap persisted tool results before rehydration` (capping tool/tool_result content for session history, memory turns, compaction prompt, etc.)

These represent ongoing work to stabilise the browser tool’s interaction with web components and to manage session history sizes—both important for reliability and performance.

## 4. Community Hot Topics
Neither of the two active issues nor any of the three PRs have received comments or reactions (👍) yet. No discussion threads have gained traction in the past 24 hours. The project may benefit from maintainers engaging with these new submissions to encourage broader community input.

## 5. Bugs & Stability
Two PRs directly address a **stability bug** in the browser tool:

- **#1100** ([PR](https://github.com/moltis-org/moltis/pull/1100)) and **#1103** ([PR](https://github.com/moltis-org/moltis/pull/1103)):  
  * Problem: `document.querySelectorAll` and `document.querySelector` do not traverse Shadow DOM boundaries, causing the browser tool to miss interactive elements rendered inside web components (e.g., Salesforce Lightning components).  
  * Severity: **High** – this bug can break core browser automation functionality on modern web apps.  
  * Status: Fix exists but not merged; two competing PRs with similar aim.

Additionally, **PR #1089** ([PR](https://github.com/moltis-org/moltis/pull/1089)) addresses a resource-management concern: without capping, large tool results during session rehydration could cause excessive memory usage or crashes, especially during compaction and memory turns. Severity: **Medium**.

## 6. Feature Requests & Roadmap Signals
Two feature requests were opened on 2026-06-04:

- **#1102** – `Feature: Add FunASR/SenseVoice as local STT engine` ([Issue](https://github.com/moltis-org/moltis/issues/1102))  
  Summary: The user requests integration of [FunASR](https://github.com/modelscope/FunASR) or [SenseVoice](https://github.com/FunAudioLLM/SenseVoice) for ultra‑fast local speech-to-text (SenseVoice-Small ~70ms for 10s audio) and native streaming via Paraformer.  
  *Likely roadmap impact:* Adding a local STT option would align with the project’s focus on privacy and off‑first assistants. Could appear in a future minor release if maintainers prioritize multi‑engine support.

- **#1101** – `[enhancement] Feature: Add SMS and LINE channels (moltis-sms, moltis-line)` ([Issue](https://github.com/moltis-org/moltis/issues/1101))  
  Summary: The user proposes official channel integrations for SMS and LINE messaging, following the pattern of existing channels.  
  *Likely roadmap impact:* If the project aims to become a universal assistant platform, messaging channel plugins are a natural expansion. May be considered for the next major version or as separate plugins.

No formal roadmap or milestone tags are visible in these issues, but both are clear signals of user desire for broader input/output modalities.

## 7. User Feedback Summary
While no explicit satisfaction/dissatisfaction statements have been posted in the last 24 hours, the two new issues reveal concrete user needs:

- **Voice assistant users** want more choice for local STT engines, citing speed and streaming capabilities as key differentiators for on‑device usage.  
- **Multi‑channel users** request the ability to interact with Moltis via SMS and LINE, indicating a desire for asynchronous, mobile‑friendly interaction beyond web chat.  

These suggestions highlight that the community values both **performance optimisation** (local STT) and **platform reach** (messaging channels). No negative feedback (bugs, crashes) was received from users directly, but the shadow DOM bug (see §5) could be affecting real-world usage.

## 8. Backlog Watch
No issues or PRs in the provided data are flagged as **long‑unanswered** or **stale**. All items are recent (created/updated within the last 5 days). However, the two shadow-DOM fix PRs (#1100, #1103) are competing alternatives; a maintainer decision and merge would be beneficial to avoid duplication and to close the bug quickly. PR #1089 (capping) has been open since 2026-06-01 and has received no maintainer feedback—prompt review is recommended to prevent memory issues from affecting user sessions.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the provided GitHub data from CoPaw (github.com/agentscope-ai/CoPaw), here is the project digest for 2026-06-05.

# CoPaw Project Digest: 2026-06-05

## 1. Today's Overview

The CoPaw project exhibits **very high activity and a healthy maintenance rhythm** over the last 24 hours. With 32 issues and 33 pull requests updated, the community is highly engaged, and the core team is responding rapidly. A significant number of issues (17 closed) and PRs (23 merged/closed) were actioned, indicating robust issue triage and a steady stream of fixes and improvements. A new beta patch release (`v1.1.11-beta.1`) was published, focusing on minor fixes, while major feature integrations like a new data-analysis plugin and a Tauri auto-updater are actively under review. The community is strongly focused on core agent stability (execution interruption, cron jobs), observability (token usage, context size), and UX enhancements (tool call display, skill auto-completion).

## 2. Releases

- **Version:** `v1.1.11-beta.1`
- **What's Changed:**
    - `fix(config)`: Added a `ProviderManager` fallback to `get_model_max_input_length`. This improves resilience when fetching model configuration fails.
    - `refactor(cron)`: Disabled "push bubbles" (desktop notifications) for cron jobs of type `agent` to reduce noise.
- **Impact:** This is a minor patch with no breaking changes or migration notes expected. It primarily targets backend stability and user experience for scheduled tasks.

## 3. Project Progress (Merged/Closed PRs)

The following key PRs were merged or closed, advancing project features and stability:

- **MCP Tool Naming Fix** ([PR #4958](agentscope-ai/QwenPaw PR #4958)): Critical fix for MCP tools with names containing `.` (e.g., `pat.batch_plan`). The system now sanitizes tool names automatically to comply with OpenAI/Anthropic's API validation regex (`^[a-zA-Z0-9_-]+$`), fixing a bug that prevented tool calls entirely for certain models.
- **Sub-Agent Tool** ([PR #4806](agentscope-ai/QwenPaw PR #4806)): Added the `spawn_subagent` built-in tool, enabling an agent to delegate ephemeral sub-tasks within its own workspace. This provides a new collaboration mode for complex, multi-step tasks.
- **Feishu Channel Enhancement** ([PR #4879](agentscope-ai/QwenPaw PR #4879)): Added support for extracting text content from Feishu "interactive" cards (`msg_type=interactive`), significantly expanding the channel's compatibility with rich message formats.
- **QQ Channel Authorization** ([PR #4848](agentscope-ai/QwenPaw PR #4848)): Introduced QR code-based authorization for the QQ channel, simplifying the credential setup process by allowing users to scan a code with the QQ app.
- **Frontend Testing Milestone** ([PR #4332](agentscope-ai/QwenPaw PR #4332)): The frontend unit test milestone was completed, adding ~100 new test cases across 10 files to cover previously untested modules (constants, contexts, layouts, etc.).
- **Context Compaction Bug Fixes** ([PR #4953](agentscope-ai/QwenPaw PR #4953), [PR #4956](agentscope-ai/QwenPaw PR #4956)): Two bugs causing `/compact` to crash with `'str' object has no attribute 'get'` were identified and resolved. These occurred when message content contained mixed-type lists or during the `pre_reasoning` hook.

## 4. Community Hot Topics

The issues with the most community engagement highlight key areas of user demand:

- **[#4644] Tool Calls Not Displayed Until Refresh** (`Closed`): A long-standing bug where tool calls in the Console UI are not displayed in real-time. This had **20 comments**, indicating it was a significant and well-documented UX pain point. The closure suggests a fix may be in the pipeline or was identified.
- **[#4961/#4964] Request to Interrupt Agent Execution** (`Open`): A user repeatedly requested the ability to abort an ongoing agent execution by sending a new message. This is a high-value feature for productivity, as it prevents users from waiting for an agent to finish an incorrect or unnecessary task.
- **[#4950/#4963] Support Direct Script/Shell Execution in Cron** (`Open`): Users want cron jobs to be able to run scripts directly, bypassing the AI agent. This reflects a use case for simple, deterministic scheduled tasks where the overhead of an LLM call is unnecessary.
- **[#4640] Session Auto-Summary Hook** (`Closed`): A feature request for a "pre-hook memory archiving" mechanism, where the system automatically extracts and saves key decisions and "pitfalls" at the end of a session. This points to a desire for a more intelligent and self-managing memory system.
- **[#3891] DeepSeek Prefix Cache Optimization** (`Open`): This ongoing issue about low DeepSeek prefix cache hit rates (~95%) is a high-impact, cost-related concern. It has 1 👍, suggesting it's a priority for users sensitive to API costs.

## 5. Bugs & Stability

Several bugs were reported and fixed today, indicating a focus on improving stability:

- **Critical: Agent Execution Deadlock** ([#4967](agentscope-ai/QwenPaw Issue #4967), `Open`): A user reported the agent entering an infinite loop from which it cannot exit. This is a **high-severity** issue that can render the agent unusable. No fix PR is linked yet.
- **High: DeepSeek Response Folding** ([#4962](agentscope-ai/QwenPaw Issue #4962), `Open`): A bug where DeepSeek API responses are incorrectly folded into the "thinking process" section, requiring the user to expand the section to see the actual reply. This is a notable UX regression for DeepSeek users.
- **Medium: Console UI Tool Call Display** ([#4644](agentscope-ai/QwenPaw Issue #4644), `Closed`): A described bug where tool calls were not displayed until manual page refresh. The issue is now closed, suggesting a fix was merged.
- **Medium: /compact Command Crashes** ([#4937](agentscope-ai/QwenPaw Issue #4937), `Open` & [#4953](agentscope-ai/QwenPaw Issue #4953), `Closed`): An open bug reports that `/compact` respects the model's max_input_length, and a related crashing bug was fixed today.
- **Low: Latex Formula Display** ([#4959](agentscope-ai/QwenPaw Issue #4959), `Open`): An issue with abnormal display of LaTeX formulas in the frontend, affecting users who work with mathematical content.

## 6. Feature Requests & Roadmap Signals

- **High Priority (Likely Next Version):**
    - **Agent Execution Interruption** ([#4961](agentscope-ai/QwenPaw Issue #4961)): The highly specific request and its duplicate (4964) signal strong user need.
    - **Cron Script Execution** ([#4950](agentscope-ai/QwenPaw Issue #4950)): A clear and simple feature that adds direct utility for system administrators.
    - **Token & Context Usage Display** ([#4767](agentscope-ai/QwenPaw Issue #4767)/[#4433](agentscope-ai/QwenPaw PR #4433)): A related PR is already under review, making this a strong candidate for inclusion soon.
    - **Provider Auto-Failover** ([#4757](agentscope-ai/QwenPaw Issue #4757)): This feature is highly relevant to cost management and reliability, aligning with the project's recent stability focus.

- **Medium Priority (Future Iterations):**
    - **Memory System Enhancements** ([#4652](agentscope-ai/QwenPaw Issue #4652)): The request for a "summarize, associate, remind" mechanism is robust but complex to implement.
    - **Skill Auto-Completion in Chat** ([#4796](agentscope-ai/QwenPaw Issue #4796)): A classic UX improvement inspired by other mainstream agents.
    - **Unified UI for Similar Providers** ([#4965](agentscope-ai/QwenPaw Issue #4965)): A request to reduce UI clutter by merging multiple cards from the same provider into a single dropdown.
    - **DataPaw Plugin** ([PR #4622](agentscope-ai/QwenPaw PR #4622)): This is a substantial new feature under review, suggesting "plugin-ecosystem" as a potential roadmap direction.

## 7. User Feedback Summary

The data reveals a **technically sophisticated but impatient user base** that expects high reliability and efficiency:

- **Pain Points:** The most significant frustration is the inability to interrupt an agent (high urgency). Users also express annoyance at manual tasks like re-installing packages after updates ([#4875](agentscope-ai/QwenPaw Issue #4875)) or navigating folders to open generated files ([#4786](agentscope-ai/QwenPaw Issue #4786)).
- **Use Cases:** Users are clearly leveraging CoPaw for complex workflows (multi-turn tool calls, sub-agent delegation) and want it to function as a reliable system tool (cron jobs for scripts). The multiple requests for token/context size visibility suggest users are actively managing LLM costs and context windows.
- **Satisfaction:** The rapid closing of PRs and issue responses suggests the core team is responsive to community feedback, likely contributing to user satisfaction. The enthusiasm for features like "spawn_subagent" and "QR code auth" indicates positive reception for new capabilities.
- **Requests for Improvement:** There is a strong desire for the system to be more "intelligent" and self-managing, moving from a tool that stores information to one that learns and reminds (see memory and skill auto-completion requests).

## 8. Backlog Watch

The following open issues/PRs require maintainer attention due to their age, importance, or lack of recent activity:

- **[#3891] DeepSeek Prefix Cache Optimization** ([Issue](agentscope-ai/QwenPaw Issue #3891)): Created over a month ago (2026-04-27) with 4 comments and 1 👍. This is a **high-impact cost optimization** issue that has not received a solution yet.
- **[#4757] Automatic Provider Degradation** ([Issue](agentscope-ai/QwenPaw Issue #4757)): Created on 2026-05-28, this is a strategic feature for reliability that, if implemented, could solve multiple connected issues (e.g., [#4181](agentscope-ai/QwenPaw Issue #4181)). It remains open with no assigned developer.
- **[#4622] DataPaw Plugin** ([PR #4622](agentscope-ai/QwenPaw PR #4622)): A major community contribution (first-time contributor, Under Review) that has been open since 2026-05-22. This represents significant potential value but requires thorough review and integration.
- **[#4669] Tauri Auto Updater** ([PR #4669](agentscope-ai/QwenPaw PR #4669)): Another major feature PR, open since 2026-05-25. As a core infrastructure piece for the desktop client, its progress is important for the project's roadmap.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw Project Digest – 2026-06-05

### 1. Today's Overview
ZeroClaw is in a period of intense activity with **32 issues and 50 pull requests updated in the last 24 hours**, indicating a healthy, fast-moving open‑source project. The community focus is split between stabilising the upcoming **v0.8.0 release** (tracked in [#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)) and preparing integration/channel/tool additions for **v0.8.1** (tracked in [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)). Five bugs were closed today, and several high‑risk RFCs are under active discussion. No new releases were published today.

### 2. Releases
No new releases in the last 24 hours. The project appears to be between tag cycles, with `v0.8.0` blockers still being resolved.

### 3. Project Progress
**Merged / closed PRs today (5 items from the 24h total of 15):**
- **[#7231](https://github.com/zeroclaw-labs/zeroclaw/pull/7231)** – `fix(ollama): restore compiling master build`. Two latent compilation errors in the Ollama provider were fixed, unblocking master after a prior PR ran CI against a stale base.
- Other closed PRs are not shown in the top-20 list but the overview reports 15 merged/closed today. Likely includes small fixes, doc tweaks, and the issues that were closed (e.g., #7069 Twitter/X fix – see Bugs section).

**Open PRs that made substantial progress:**
- **[#7222](https://github.com/zeroclaw-labs/zeroclaw/pull/7222)** – `fix(gateway): clear backend history on "Clear all" + don't resurrect deleted session`. Solves the stale‑session problem (#7126) by wiring the web UI button to a backend `DELETE` call.
- **[#7221](https://github.com/zeroclaw-labs/zeroclaw/pull/7221)** – `fix(gateway): block observability telemetry from chat WS by default`. Root‑cause fix for the “unknown” tool card bug (#7151).
- **[#7223](https://github.com/zeroclaw-labs/zeroclaw/pull/7223)** – `feat(web): support slash commands in gateway web chat input`. Adds `/clear`, `/help`, `/model`, etc. to the browser UI.
- **[#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229)** – `feat(web): MCP, Skills, Plugins & Providers dashboard tabs`. A significant new web management interface.
- **[#7233](https://github.com/zeroclaw-labs/zeroclaw/pull/7233)** – `feat(observability): Structured Observability Enhancement`. Implements rich event context and OTel trace correlation (RFC #7232).

### 4. Community Hot Topics
**Most commented issues (last 24h):**
- **[#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)** – `[Bug]: Ollama Provider call failed when tools are needed` (6 comments, now closed). The bug blocked entire sessions; the community helped diagnose and it was resolved.
- **[#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)** – `[Feature]: computer-use support` (5 comments). Taps into the desire for desktop GUI interaction, comparing with OpenAI Codex and Peekaboo.
- **[#3566](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** – `[Feature][interop]: A2A (Agent-to-Agent) Protocol Support` (5 comments, 7 👍). The most upvoted feature request; inter‑agent communication is a key roadmap item.
- **[#7069](https://github.com/zeroclaw-labs/zeroclaw/issues/7069)** – `Twitter/X channel not available in pre‑built binary` (3 comments, now closed). User frustration with missing channel; maintainers confirmed the bug and fixed it.
- **[#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)** – `[Feature]: Add a per‑execution confirmation tier for high‑risk shell commands` (2 comments). Shows user demand for finer‑grained safety controls.

**Underlying needs:**
The community is pushing for **industrial‑grade agent interoperability** (A2A), **safety controls** (shell command policies), and **richer web/tooling experience** (computer‑use, LSP support, web dashboard tabs). The Ollama provider reliability fix and the Twitter channel availability bug highlight the importance of provider parity and binary completeness.

### 5. Bugs & Stability
**High‑severity bugs reported today (ranked by severity S1):**
- **[#7227](https://github.com/zeroclaw-labs/zeroclaw/issues/7227)** – `[Bug]: zerocode Quickstart hardcodes model-provider alias to 'default', colliding with existing providers` (S1). Blocks onboarding for multi‑alias setups. **No fix PR yet.**
- **[#7125](https://github.com/zeroclaw-labs/zeroclaw/issues/7125)** – `[Bug]: TUI (zerocode) freezes entirely when daemon disconnects` (S1). Reproduced, labelled `in‑progress`. No fix PR visible.
- **[#7179](https://github.com/zeroclaw-labs/zeroclaw/issues/7179)** – `[Bug]: ZeroClaw Reaps Idle RPC Sessions at 10 Minutes` (S1, now closed). The 10‑minute timeout broke background workflows. Fix was merged as part of the session management PR chain.

**Medium‑severity bugs:**
- [#7225](https://github.com/zeroclaw-labs/zeroclaw/issues/7225) – WhatsApp Web `mention_only` ignores replies (S2). No fix PR.
- [#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) – Web UI “Clear all” only wipes frontend (S2). A fix PR [#7222](https://github.com/zeroclaw-labs/zeroclaw/pull/7222) is open.
- [#7151](https://github.com/zeroclaw-labs/zeroclaw/issues/7151) – Observability telemetry leaks onto chat WS (S2). Fix PR [#7221](https://github.com/zeroclaw-labs/zeroclaw/pull/7221) open.
- [#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232) – RFC for structured observability enhancements (addressed via PR #7233).

**Closed bugs today (5):** #5962, #7069, #7179, #7211, #7083. Notably #7083 (Windows shell double‑quote mangling) was a critical S1 blocking Windows users; fix merged.

### 6. Feature Requests & Roadmap Signals
**New feature requests today (with high engagement or maintainer acceptance):**
- **Per‑model capability & context‑window config** ([#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100), P1, needs maintainer review). Would give users fine‑grained control over vision and context budget per model – likely to land in v0.8.0 or soon after.
- **Per‑execution confirmation tier for shell commands** ([#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155), P1, needs maintainer review). Mirrors Claude Code’s `allow/ask/deny` pattern; strong candidate for v0.8.1.
- **A2A agent discovery** ([#7218](https://github.com/zeroclaw-labs/zeroclaw/issues/7218)) – defines `/.well-known/agent-card.json` for multi‑agent setups. Signals roadmap commitment to inter‑op.
- **i18n git submodule** ([#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184)) – low risk, accepted; will reduce translation churn in main repo.

**Features already in PR stage:**
- Web dashboard tabs (MCP, Skills, Plugins, Providers) – [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) – likely merges after review.
- WASM Component Model support (FND-001) – [#7212](https://github.com/zeroclaw-labs/zeroclaw/pull/7212) – shifts from Extism to wasmtime for ARM32 support.
- ESP32 simulator example – [#7048](https://github.com/zeroclaw-labs/zeroclaw/pull/7048) – hardware focus.

**Likely for next release (v0.8.0):** Config correctness, schema cleanup, shell safety, per‑model config, observability enhancements. v0.8.1 will pick up MCP dashboard, A2A groundwork, and channel improvements.

### 7. User Feedback Summary
**Pain points expressed today:**
- **Ollama provider failures** when tools are needed – user @ufkabakan described blocked workflows (closed, fixed).
- **Twitter/X channel missing** in pre‑built binaries – user @theonlyhennygod reported that the feature existed in source but not in dist (closed, fixed).
- **Windows shell command quoting** – user @NiuBlibing noted all commands with double quotes fail on Windows (closed, fixed).
- **Session reaping at 10 minutes** – user @tidux called it a workflow blocker for long‑running agents (closed, fixed).
- **Web UI shortcomings** – several users (NiuBlibing, xianshishan) complained about missing slash commands, broken “Clear all”, timestamp rendering inside bubbles, and persistent drift banners. Some fixes are already in open PRs.
- **Repo size** – user @APX103 filed a light‑hearted but valid S3 bug about repository size.

**Satisfaction signals:**
- User @sbenedetto praised ZeroClaw as “a Rust‑based agent runtime that is much lighter on resources than many other agent systems” (in [#7143](https://github.com/zeroclaw-labs/zeroclaw/issues/7143)), even while reporting a bug.
- The high number of feature requests and the engagement on A2A / computer‑use indicate strong interest in expanding ZeroClaw’s capabilities.

### 8. Backlog Watch
**Important issues/PRs that have been unanswered for a while or need maintainer attention:**
- **[#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)** – `[audit]: track 153 commits lost in bulk revert` (2026-04-24). Labeled `priority:p2`, `status:in-progress`. No activity for over a month. This audit is critical for repo integrity.
- **[#5797](https://github.com/zeroclaw-labs/zeroclaw/pull/5797)** – `feat(providers): add tls_ca_cert_path support` (since 2026-04-16). A risk‑high, months‑old PR that enables corporate PKI. Still under review. May need maintainer push.
- **[#7019](https://github.com/zeroclaw-labs/zeroclaw/pull/7019)** – `fix(channels): deliver non‑opus TTS via sendAudio` (2026-05-30). Depends on another PR (#6968). Blocked review.
- **[#3566](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)** – A2A protocol support (7 👍, 5 comments). Accepted but blocked for a long time. May need a dedicated owner to unblock.

---

*Digest generated from GitHub data for zeroclaw-labs/zeroclaw on 2026-06-05.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*