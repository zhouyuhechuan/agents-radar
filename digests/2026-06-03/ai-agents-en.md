# OpenClaw Ecosystem Digest 2026-06-03

> Issues: 429 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-03 03:26 UTC

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

# OpenClaw Project Digest — 2026-06-03

## 1. Today's Overview

OpenClaw saw extremely high activity on 2026-06-03, with **429 issues** and **500 PRs** updated in the last 24 hours, though only **277** issues remain open/active and **391** PRs are open. No new releases were published today. The community continues to report deeply coupled session-state, message-delivery, and auth-provider regressions—many originating in the 2026.5.x releases—while maintainers are actively merging fixes for CRIs (critical runtime incidents) and moving several high-impact proposals toward review. The project appears in a period of intense stabilization and feature refinement, not major architectural change.

## 2. Releases

**No new releases** were detected for 2026-06-03. Community issues and PRs reference builds from 2026.5.12 through 2026.5.28, with many regressions first observed after the 2026.5.22 and 2026.5.27 updates.

## 3. Project Progress

In the last 24 hours, **109 PRs were merged or closed**. Notable advancements include:

- **UI/skills toggle stability**: Multiple PRs (#89681, #89670, #89675, #89672) were merged or submitted to fix issue #89661, where skill toggle state transferred incorrectly on list mutations. All approach the fix by adding stable keys to list rendering.
- **Telegram performance**: PR #88963 (closed) optimized `/new` and hard `/reset` session-boundary detection by avoiding broad reset-boundary scans on Telegram.
- **OpenAI Codex OAuth hardening**: PR #89491 (open, waiting on author) improves token exchange and refresh SSRF policy handling for Codex OAuth.
- **Feishu reliability**: PR #89659 (open) adds retry logic for Feishu send rate-limit errors (codes 230020/230006).
- **Memory-core search enhancement**: PR #89584 (open) introduces an optional cross-encoder reranking stage for memory search.
- **Gateway hot-reload fix**: PR #89517 (open) ensures `hot` mode config reloads actually schedule a restart instead of warning.

## 4. Community Hot Topics

| Issue/PR | Title | Comments | Reactions | Core Concern |
|----------|-------|----------|-----------|--------------|
| [#52875](https://github.com/openclaw/openclaw/issues/52875) | Session_send gives no session found (regression) | 21 | 1 👍 | Session-state loss after upgrade; agent-to-agent communication broken. |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Track core session/transcript SQLite migration | 17 | 1 👍 | Architectural plan to migrate session/transcript state to SQLite in small steps to avoid a risky rewrite. |
| [#63918](https://github.com/openclaw/openclaw/issues/63918) | Cron sends thinking=none to OpenAI models that require minimal | 17 | 1 👍 | Model incompatibility in cron tool calls; affects GPT-5-nano. |
| [#67035](https://github.com/openclaw/openclaw/issues/67035) | Windows chat UI regression: input text swallowed, invisible replies | 14 | 0 | Severe UX regression on Windows; streamed replies invisible until refresh. |
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | Add tools.web.fetch.allowPrivateNetwork | 13 | 9 👍 | Users need controlled access to internal network addresses; currently blocked entirely. |

**Analysis**: The most active threads center on **session-state reliability** (#52875, #88838, #67035), **model compatibility mismatches** (#63918), and a long-standing **feature gap for private network access** (#39604). The community is clearly invested in production-quality session management, as multiple high-comment issues involve agents failing to communicate or maintain state across sessions.

## 5. Bugs & Stability

**P1 (Critical) Regressions and Bugs:**

| Issue | Title | Impact | Fix PR Exists? |
|-------|-------|--------|----------------|
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex app-server turn-completion stall (regression of #84076) | session-state, message-loss | PR #89290 (open, waiting on author) |
| [#67035](https://github.com/openclaw/openclaw/issues/67035) | Windows chat UI input/reply rendering failure | session-state, message-loss | PR #89530 (open, ready for maintainer) |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent sends duplicate replies on Telegram (2-10x) | session-state, message-loss | Not directly linked |
| [#80715](https://github.com/openclaw/openclaw/issues/80715) | Slack replies silently dropped (composed, never posted) | message-loss | Not directly linked |
| [#86047](https://github.com/openclaw/openclaw/issues/86047) | Codex plugin approval stalls in Nextcloud Talk | session-state, message-loss | Not directly linked |
| [#55334](https://github.com/openclaw/openclaw/issues/55334) | sessions.json unbounded growth → gateway OOM | session-state, crash-loop | Not linked |
| [#52249](https://github.com/openclaw/openclaw/issues/52249) | ACP parent session stuck until refresh | session-state, message-loss | Not linked |
| [#86090](https://github.com/openclaw/openclaw/issues/86090) | Phantom run on idle agent (no model turn executed) | message-loss | Not linked |
| [#89374](https://github.com/openclaw/openclaw/issues/89374) | Timeout compaction claims success but leaves session unrecoverable | session-state | Not linked |
| [#89549](https://github.com/openclaw/openclaw/issues/89549) | sessions_spawn child runs fail with 401 Missing scopes | session-state, auth-provider | Not linked |

**P1 regressions newly opened today:**
- [#89525](https://github.com/openclaw/openclaw/issues/89525): Telegram `/compact` slash command never appears in commands.log (regression, P2)
- [#89549](https://github.com/openclaw/openclaw/issues/89549): `sessions_spawn` child runs fail with HTTP 401 Missing scopes (P1, needs live repro)

**Summary**: The bug landscape remains dominated by **session-state corruption/disappearance** across multiple channels (Slack, Telegram, Discord, WebChat) and **codex-runtime stalls**. Several P1 bugs have active fix PRs in review but none have been merged yet. The sheer volume of session/message-loss bugs suggests a systemic issue in the session lifecycle management layer, potentially worsened by recent 2026.5.x changes.

## 6. Feature Requests & Roadmap Signals

**High-Community-Interest Features:**

| Issue | Title | 👍 | Status |
|-------|-------|----|--------|
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | Add `tools.web.fetch.allowPrivateNetwork` | 9 👍 | Open, needs security review |
| [#84216](https://github.com/openclaw/openclaw/issues/84216) | Dropdown to minimize recent sessions in UI | 3 👍 | Open, enhancement |
| [#76952](https://github.com/openclaw/openclaw/issues/76952) | Document Realtime Talk voices, voice-agent role, phone bridge | 2 👍 | Closed, but signals user need |
| [#76159](https://github.com/openclaw/openclaw/issues/76159) | Per-job `acceptSilentStop` flag for cron jobs that output nothing | 1 👍 | Open, needs product decision |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | Hook for pre-routing inbound message interception (channel bridging) | 2 👍 | Open, stale |

**Predictions for next release (tentative 2026.6.x):**
- **Private network fetch control** (#39604) has 9 👍 and clear use case—likely to land if security review passes.
- **Cross-encoder reranking for memory search** (PR #89584) shows active development.
- **Opt-in interleaved progress lane for Telegram** (PR #87072) may land if the proof rig passes.
- **Persistent followup queues across restarts** (PR #82572) is large and risky; may slip to a later release.

## 7. User Feedback Summary

**Common Pain Points:**
- **Session state loss after upgrades**: Multiple users report that upgrading between 2026.5.x builds breaks agent-to-agent communication, session persistence, or reply rendering.
- **Message delivery failures in specific channels**: Slack replies silently dropped (#80715), Telegram messages duplicated (#86519), Discord sessions stuck after compaction (#89374), Feishu dispatch broken (#87646).
- **Windows-specific UI regressions**: The Windows chat UI has become nearly unusable for some users (#67035), with input text swallowed and replies invisible until manual refresh.
- **Cron/model compatibility surprises**: Cron jobs send incorrect `thinking` parameters, causing 400 errors on models that don't accept `none` (#63918).
- **OAuth and auth provider fragility**: Multiple users report `doctor --fix` not fully recovering Codex/OAuth state (#87650, #84252), and `secrets audit` false positives for Codex markers (#84376).

**Satisfaction Signals:**
- Users actively request **better documentation** for Realtime Talk (#76952) and **UI polish** (minimizable recent sessions, #84216)—indicating they are engaged with the product and want to use it more effectively.
- The number of contributors submitting fix PRs (over 100 merged/closed today) suggests a healthy maintainer and community contributor pipeline.

## 8. Backlog Watch

**Long-unanswered Issues Needing Maintainer Attention:**

| Issue | Age | Priority | Problem |
|-------|-----|----------|---------|
| [#52875](https://github.com/openclaw/openclaw/issues/52875) | ~72 days (since 2026-03-23) | P2 | Session_send "no session found" regression after upgrade; 21 comments, no linked fix PR. |
| [#55334](https://github.com/openclaw/openclaw/issues/55334) | ~69 days (since 2026-03-26) | P1 | sessions.json unbounded growth causes gateway OOM; 10 comments, needs product decision. |
| [#52249](https://github.com/openclaw/openclaw/issues/52249) | ~73 days (since 2026-03-22) | P1 | ACP parent session stuck until refresh; 9 comments, needs product decision. |
| [#45269](https://github.com/openclaw/openclaw/issues/45269) | ~82 days (since 2026-03-13) | P2 | `apply_patch` treated as unknown/plugin-only tool (regression); 7 comments, needs security review. |
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | ~87 days (since 2026-03-08) | P2 | Private network fetch feature; 13 comments, 9 👍, needs security review and product decision. |
| [#41199](https://github.com/openclaw/openclaw/issues/41199) | ~86 days (since 2026-03-09) | P1 | Agent-to-agent communication tool parameter conflicts; 5 comments, needs product decision. |

**Open PRs Waiting for Maintainer Review (Ready for Look):**
- [#89530](https://github.com/openclaw/openclaw/pull/89530) — fix(ui): preserve visible chat stream text (P1, rating platinum hermit)
- [#89613](https://github.com/openclaw/openclaw/pull/89613) — docs: document auth profile failure policy contract (P3)
- [#89681](https://github.com/openclaw/openclaw/pull/89681) — fix(ui): key skills lists with repeat() (fixes #89661)
- [#89670](https://github.com/openclaw/openclaw/pull/89670) — fix(ui): Issue 89661 skill toggle (platinum hermit)
- [#89673](https://github.com/openclaw/openclaw/pull/89673) — fix(agents): reclaim session write-locks past maxHoldMs
- [#89669](https://github.com/openclaw/openclaw/pull/89669) — fix(agents): contain provider schema hook failures

**Notable**: The backlog contains multiple **P1 session-state bugs** that have remained open for 2–3 months without a fix PR. This indicates either a high difficulty/reproducibility hurdle or a resource bottleneck in the session lifecycle team. The SQLite migration tracking issue (#88838) may be an architectural response to these chronic stability problems.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent & Personal Assistant Open-Source Ecosystem

**Date**: 2026-06-03  
**Analyst**: Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing a period of intense maturation, with the ecosystem simultaneously grappling with session-state reliability issues across multiple major projects while pushing forward on model context protocol (MCP) integration, multi-platform channel support, and agent orchestration capabilities. The dominant pattern across all active projects is a shift from pure feature expansion toward production-grade stability, with session lifecycle management emerging as the single most critical quality bottleneck. Chinese-ecosystem projects (LobsterAI, CoPaw, PicoClaw) are expanding rapidly through WeChat/Feishu/DingTalk integrations, while Western-focused projects (IronClaw, Hermes Agent) are investing heavily in agent safety systems and credential management. The ecosystem is bifurcating between lightweight embeddable runtimes (Moltis, NanoClaw, NullClaw) and full-featured agent platforms (OpenClaw, ZeroClaw, Hermes), with the latter group absorbing the majority of community activity and bug reports.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score |
|---------|---------------------|-------------------|----------------|--------------|
| **OpenClaw** | 429 | 500 | No release; reference 2026.5.x | **Moderate (stabilizing)** – high activity but systemic session bugs |
| **ZeroClaw** | 50 | 50 | **v0.8.0-beta-2** (zerocode TUI) | **Good** – strong merge velocity, major features shipped |
| **Hermes Agent** | 50 | 50 | No release | **Concerning** – high P1 backlog, unaddressed Docker Discord bugs |
| **IronClaw** | 29 | 50 | No release | **Good** – aggressive fix velocity, Reborn loop cleanup |
| **CoPaw** | 36 | 29 | v1.1.11 beta | **Good** – security responsive, channel fixes merged |
| **NanoBot** | 9 | 25 | No release | **Good** – focused fixes, email attachments shipped |
| **PicoClaw** | 3 | 14 | v0.2.9-nightly | **Good** – goroutine leak fixed, provider coverage expanded |
| **LobsterAI** | 0 | 9 | No release | **Good** – small but efficient, all fixes landed same-day |
| **NullClaw** | 1 | 1 | No release | **Moderate** – single PII bug, fix under review |
| **NanoClaw** | 1 | 6 | No release | **Stable** – slow pace, security injection fix merged |
| **Moltis** | 1 | 1 | No release | **Stable** – quiet, UX config request |
| **TinyClaw** | 0 | 0 | No activity | **Inactive** |
| **ZeptoClaw** | 0 | 0 | No activity | **Inactive** |

**Key Insight**: The top four projects by raw activity (OpenClaw, ZeroClaw, Hermes, IronClaw) together account for ~88% of all ecosystem issue and PR activity. The remaining nine projects collectively represent the tail, with varying levels of maintenance diligence.

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Largest community contributor pipeline**: 109 PRs merged/closed in 24 hours (vs. ZeroClaw's 47, Hermes's 6). This suggests a deeper bench of external contributors and more comprehensive community governance.
- **Most mature channel ecosystem**: Telegram, Slack, Discord, Feishu, WebChat, Codex, ACP – no other project covers this breadth of integrations.
- **Architecture reference**: As the core spec repository, OpenClaw defines patterns (session state, SQLite migration, gateway hot-reload) that downstream projects like Hermes, PicoClaw, and CoPaw often emulate.

**Technical approach differences:**
- OpenClaw's session lifecycle is **deeply coupled** – session state, message delivery, auth providers, and compaction are interwoven, causing systemic regression cascade (10+ P1 session-loss bugs). Competitors (PicoClaw, NullClaw) use simpler stateless or lock-based approaches that avoid this class of bugs entirely.
- OpenClaw pursues **architectural migration** (SQLite for session state, PR #88838) as a response to stability problems; Hermes and ZeroClaw instead patch incrementally.

**Community size comparison:**
- OpenClaw's 429 daily issues vs. next-closest 50–55 suggests it has **5–8× more user base** than any individual peer. However, this also means 5–8× more bug surface area. The satisfaction-to-pain ratio appears lower than PicoClaw or LobsterAI, where bugs are fixed within 24 hours.

**Strategic risk**: OpenClaw's dominance in community size is not matched by proportional stability – three 2–3 month old P1 session bugs remain unfixed. If ZeroClaw, IronClaw, or Hermes close their stability gaps, they could attract switching users.

---

## 4. Shared Technical Focus Areas

The following requirements appear across **three or more** projects, indicating industry-wide pain points:

| Theme | Manifestations | Affected Projects |
|-------|---------------|-------------------|
| **Session state reliability** | State loss after upgrades, compaction corruption, OOM from unbounded growth | OpenClaw, Hermes, CoPaw, PicoClaw |
| **MCP integration & stability** | Connection drops, subagent tool inheritance, SSRF hardening, proxy support | NanoBot, IronClaw, NanoClaw, Hermes, CoPaw |
| **Private network & security controls** | `allowPrivateNetwork` fetch flag, SSRF guards, credential zeroization | OpenClaw, NullClaw, IronClaw, NanoClaw, CoPaw |
| **Channel-specific delivery reliability** | Telegram duplicates, Slack silent drops, Discord turn termination, Feishu rate limits | OpenClaw, Hermes, CoPaw, ZeroClaw |
| **Model compatibility & provider flexibility** | Missing `temperature` for Claude Opus, `thinking` param for GPT-5, `response_format` for third-party APIs | OpenClaw, IronClaw, NanoBot, PicoClaw, CoPaw |
| **Agent orchestration & subagent management** | `spawn()` MCP tool inheritance, auto-forking, batch deletion | NanoBot, Hermes, CoPaw, LobsterAI |
| **Cost optimization** | Cache-miss token costs, context compression quality, lazy tool loading | OpenClaw, NanoBot, CoPaw, ZeroClaw |
| **Windows desktop UX** | Input text swallowed, invisible replies, scroll bugs, file upload limits | OpenClaw, Hermes, CoPaw, ZeroClaw |

**Cross-cutting observation**: **MCP** and **session state** are the two pillars the entire ecosystem is struggling to stabilize. Projects that solve session management first (PicoClaw's goroutine fix, ZeroClaw's rapid merge velocity) gain a reliability advantage.

---

## 5. Differentiation Analysis

| Project | Target User | Strengths | Weaknesses |
|---------|-------------|-----------|------------|
| **OpenClaw** | Enterprise / power users needing multi-channel agents | Broadest channel coverage, largest contributor community | Session state fragility, slow fix turnaround for P1 bugs |
| **ZeroClaw** | Developers wanting terminal-native agent UX | Innovative zerocode TUI, strong Rust/Go-based performance, fast iteration | Beta maturity, fewer channel integrations than OpenClaw |
| **Hermes Agent** | Security-conscious enterprises | Credential zeroization, sandbox hardening, detailed RFC proposals | Docker image breakage, Discord/Matrix reliability, maintainer response gaps |
| **IronClaw** | Internal QA teams (NearAI) | Extremely high fix velocity, systematic bug bashes, Reborn architecture | Very new – primarily internal users, needs proof of external adoption |
| **CoPaw** | Chinese enterprise chat (WeChat, WeCom, DingTalk) | Deep Chinese ecosystem support, active security audit program | Context compression issues, Windows startup performance |
| **NanoBot** | API cost-conscious users, LLM app developers | Lightweight, fast email attachments, RAG embedded | Small community, older bugs (Notion MCP) unaddressed |
| **PicoClaw** | Chinese LLM users (Zhipu, MiniMax) on resource-constrained devices | Efficient Go-based runtime, fast goroutine/streaming fixes | Limited to Chinese providers, moderate Web UI polish |
| **LobsterAI** | NetEase/Youdao ecosystem, IM channel operators | Cleanest maintenance record (all fixes same-day), strong MCP caching | Very low community engagement, passive backlog |

**Architecture dichotomy**: OpenClaw/Hermes/CoPaw follow a heavy monolith pattern with deep state coupling; PicoClaw/NullClaw/Moltis favor minimal state with simpler concurrency models. The latter group has fewer regressions but also less feature depth.

---

## 6. Community Momentum & Maturity

**Tier 1 – Rapid Iteration (shipping features weekly)**:
- **ZeroClaw** – Major v0.8.0 release, 47 PRs merged in 24 hours, strong docs investment. Highest momentum-to-bug ratio.
- **IronClaw** – 31 PRs merged, systematic Reborn cleanup. High velocity but still internal-facing.

**Tier 2 – Stabilization Mode (fixing regressions)**:
- **OpenClaw** – High activity but dominated by regression fixes. 109 merged PRs reflect triage rather than innovation.
- **Hermes Agent** – Feature RFCs (subagents, shared memory) signal ambition, but stability debt is accumulating.
- **CoPaw** – Security audit shows maturity; context compression and Windows UX remain pain points.

**Tier 3 – Steady Maintenance (incremental improvements)**:
- **PicoClaw** – Goroutine leak fix, Zhipu compatibility, streaming bugs. Healthy but not breaking new ground.
- **NanoBot** – Email attachments, WebUI persistence, MCP SSRF. Focused on the next 20% of features.
- **LobsterAI** – All bugs fixed same day; mostly dependency bumps and UI polish.

**Tier 4 – Low Activity / Inactive**:
- **NullClaw** – Single PII bug; otherwise quiet. Niche security-focused agent.
- **NanoClaw** – Security fix merged, webchat skill added. Slow but responsive.
- **Moltis** – 1 issue, 1 PR. Minimal community.
- **TinyClaw, ZeptoClaw** – No activity.

**Maturity assessment**: ZeroClaw has the strongest trajectory (major release + high fix velocity); OpenClaw has the largest base but risks losing trust if session bugs persist; Hermes is in a dangerous state where community goodwill is being tested by unaddressed P1/P2 bugs.

---

## 7. Trend Signals

**1. Privacy and redaction are becoming first-class concerns** – NullClaw's aggressive PII redaction and IronClaw's credential zeroization (PR #4372) indicate that agent output safety is no longer optional. Expect more projects to adopt format-aware redaction (dates, IPs, GUIDs) rather than regex-only approaches.

**2. MCP is the new MCP (Model Context Protocol) – but immature** – Every major project is integrating MCP, and every integration is hitting reliability issues (session drops, union type breaks, proxy incompatibility). This is a goldmine for tooling: an MCP conformance test suite would be immediately adopted.

**3. Chinese platform integration is a growth vector, not a side feature** – LobsterAI, CoPaw, PicoClaw, and OpenClaw all saw significant WeChat/Feishu/DingTalk activity. The demand for agent-native IM in China is surging; projects without this capability are missing a large user base.

**4. Cost optimization is the next UX battleground** – Cache-miss token costs (NanoBot #4142), compressed context quality, and prompt preloading (PicoClaw) are emerging as differentiators. Developers are tired of surprise API bills.

**5. Agent safety is converging on "sandbox everything"** – Credential leak prevention, subprocess env scrubbing, browser process isolation, and approval gates are across Hermes, IronClaw, NanoClaw, and CoPaw. The industry is moving beyond "just use Docker" toward

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-06-03

## Today’s Overview

Activity remained high over the past 24 hours, with **9 issues updated** (6 open, 3 closed) and **25 pull requests updated** (8 open, 17 merged/closed). No new releases were cut. The community is actively contributing bug fixes and feature enhancements, especially around MCP (Model Context Protocol) reliability, WebUI improvements, and email channel capabilities. While no critical regressions were introduced, several long-standing stability issues (e.g., session history corruption, read_file offload loops, pip‑based installations under `uv`) received targeted fixes. The project shows strong momentum with multiple contributors submitting PRs for both core and frontend subsystems.

## Releases

None. No new versions were published today.

## Project Progress

**Merged/Closed PRs (17 total):** The following PRs were merged or closed today, reflecting significant forward movement:

- **Email channel attachments** – Two PRs (#4162, #4160) add file attachment support to the email channel, allowing media files to be sent via SMTP with MIME encoding and fallback for unsupported types.
- **Napcat (QQ) channel backport** – PR #4146 adds OneBot v11 Forward WebSocket support for private and group QQ chats, backported from a previous branch.
- **WebUI fixes & improvements** – Several PRs improved the WebUI experience:
  - #4157 bounds startup fetch waits with a timeout helper.
  - #4151 sorts “Chats” groups among projects by recency.
  - #4150 persists refresh location routing (hash‑based).
  - #4149 adds a fallback copy mechanism for assistant replies when Clipboard API fails.
  - #4163 (open) adds “Fork from here” for user messages.
- **Dream refactor** – PR #3990 replaces the two‑phase `Dream` class with a simpler cron‑based flow using `process_direct`.
- **Runner stability** – PR #4155 prevents `read_file` from being offloaded to disk, fixing an infinite loop when tool results were too large.
- **WebUI gateway dependency split** – PR #4115 refactors HTTP routing out of `WebSocketChannel`.
- **Lightweight RAG** – PR #4109 introduces a local‑embedding‑based memory retrieval system.
- **CLI pip fix** – PR #4164 (open) and #4159 (closed auto‑fix) address pip unavailability when installed via `uv tool`.
- **MCP security** – PR #4123 adds SSRF guard validation for MCP SSE/streamable HTTP URLs.
- **Session corruption fix** – PR #4169 recovers hidden history when `last_consolidated` offset is out of range (closes #4066).
- **Email progress messages** – PR #4165 skips empty emails caused by progress marker messages.

**Key advancement:** The email channel now supports attachments, and the WebUI has better state persistence and fallback UX. The Dream subsystem was simplified, reducing maintenance overhead.

## Community Hot Topics

*Most active issues and PRs based on comment count and recent engagement:*

- **#4167 – Image generation fails with OpenAI‑compatible APIs lacking `response_format`** (2 comments)  
  A user reports a `UnsupportedParamsError` when using a third‑party image generation API (Agnes AI). The error occurs because `response_format` is hard‑coded. This is a blocking bug for users relying on custom or non‑standard image providers.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/4167)

- **#4158 – WebUI CLI App pip installs fail under `uv tool`** (1 comment)  
  When NanoBot is installed via `uv tool install`, the integrated CLI App installer cannot find `pip`. This breaks the WebUI’s “install CLI app” flow.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/4158)  
  Fix PRs: #4159 (auto‑fix) and #4164 (fallback to `uv pip`).

- **#4142 – Optimization of usage costs for cache‑miss input tokens** (1 comment)  
  A discussion about reducing API costs, especially with deepseek v4 flash/pro models that charge for cache misses. The user proposes smarter prompt caching strategies.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/4142)

- **#1168 – Notion MCP connection failure** (1 comment, opened 2026‑02‑25)  
  An ongoing issue where a user cannot connect to Notion’s MCP server despite correct credentials. They confirm the same credentials work with Claude. No maintainer response yet. This issue is over three months old.  
  [GitHub](https://github.com/HKUDS/nanobot/issues/1168)

**Underlying needs:** Users are pushing for broader third‑party API compatibility (image generation, MCP integrations) and more robust installation methods. Cost optimization is a growing concern as more users adopt expensive API models.

## Bugs & Stability

Ranked by severity:

1. **Critical – MCP session terminated unexpectedly** (#4168)  
   “After random time, the MCP server cannot be reached, log says `McpError: Session terminated`.” A restart of NanoBot fixes it. No fix PR yet; root cause likely a heartbeat or reconnection bug.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4168)

2. **High – Image generation fails with non‑standard OpenAI API** (#4167)  
   Blocking bug for users of Agnes AI or similar providers. No fix PR yet.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4167)

3. **High – `read_file` cannot recover persisted tool results after offloading** (#4153, CLOSED)  
   When a tool result exceeds `maxToolResultChars`, it is written to disk and then `read_file` fails to load it, causing an offload loop. **Fixed** in PR #4155.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4153)

4. **Medium – MemoryStore duplicate cursors under concurrent writes** (#4081, CLOSED)  
   Concurrent `append_history()` calls could produce duplicate cursors. Root cause was absence of an async lock.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4081)

5. **Low – WebUI pip install fails under `uv tool`** (#4158)  
   Workaround exists; fix PRs #4159 and #4164 are under review.  
   [Issue](https://github.com/HKUDS/nanobot/issues/4158)

Additionally, a fix for session history corruption (#4066) was landed in PR #4169, which resets `last_consolidated` when it is out of range.

## Feature Requests & Roadmap Signals

- **Subagent access to MCP services** (#4166) – A user requests that sub‑agents created via `spawn()` inherit tools from MCP servers. This would enable complex multi‑agent workflows. Likely to be considered for a near‑future release.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4166)

- **Custom image generation provider support** (#4132) – Users want `generate_image` to automatically use providers configured in `config.json` (e.g., Agnes AI). Ties directly to bug #4167.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4132)

- **Cost optimization for cache‑miss input tokens** (#4142) – A discussion that may lead to caching improvements or configurable prompt strategies. Not yet an implementation PR.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4142)

- **Cloud platform deployment (HF Spaces & ModelScope)** – PR #4139 adds a deployment layer for HuggingFace Spaces and ModelScope Studio. Though still open, it signals a clear roadmap direction toward first‑party cloud support.  
  [PR](https://github.com/HKUDS/nanobot/pull/4139)

**Prediction:** The next minor version (if any) will likely include MCP subagent access, custom image provider support, and the cloud deployment layer. The email attachment and Napcat channel features are already merged.

## User Feedback Summary

Real‑world pain points expressed over the last 24 hours:

- **Frustration with MCP reliability** – Issue #4168 describes a repeating disconnection that requires a full restart; user tjc0726 calls it “cannot reach MCP server after random time.” This is a high‑impact stability concern.
- **Third‑party API incompatibility** – gkd2323c (issue #4167) and hesetiema (#4132) both explicitly request support for alternative image generation providers. The error message suggests hard‑coded parameters are the culprit.
- **Installation friction under `uv`** – chengyongru’s report (#4158) highlights that the “install CLI App” feature inside WebUI breaks when NanoBot is launched via `uv tool`. This affects users who prefer uv‑based Python management.
- **Notion integration blind spot** – The oldest open issue (#1168) shows a user who has spent “several hours” checking API keys, yet cannot connect to Notion’s MCP despite success with Claude. No maintainer response to date, which may lead to dissatisfaction.

Satisfaction is visible in the high number of merged PRs from the community – contributors like chengyongru, nblondiau, and yu‑xin‑c are actively improving the project, indicating a healthy contributor ecosystem.

## Backlog Watch

Items that need maintainer attention:

- **#1168 – Notion MCP connection failure** (opened 2026‑02‑25, 0 maintainer comments)  
  This is the oldest open issue without a response. The user needs troubleshooting or a fix.  
  [Issue](https://github.com/HKUDS/nanobot/issues/1168)

- **#4132 – Custom image generation provider** (opened 2026‑06‑01, 0 comments)  
  While related to bug #4167, this feature request has not been triaged by a maintainer.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4132)

- **#4168 – MCP session terminated** (no fix PR yet)  
  New but high severity; no official acknowledgment.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4168)

- **#4166 – Subagent MCP access** (no maintainer response)  
  A well‑motivated enhancement request that could unblock advanced use cases.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4166)

- **#4142 – Cost optimization discussion** (1 user comment)  
  While not a bug, this discussion may inform future architecture decisions. Maintainer input would be valuable.  
  [Issue](https://github.com/HKUDS/nanobot/issues/4142)

*No PRs are critically stalled longer than a week.* The open PR #4139 (cloud deployment) and #4164 (pip fix) appear to be under review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-03

This digest is based on GitHub activity over the past 24 hours. Data from 50 updated issues (42 open, 8 closed) and 50 updated pull requests (44 open, 6 merged/closed) was analysed. No new releases were published.

---

## 1. Today's Overview

Hermes Agent saw very high activity in the last 24 hours. A flood of 50 issues and 50 PRs were updated, indicating intense community engagement and active development. The open issue count remains high (42), with several P1 bugs still unresolved. Two PRs were merged — a MiMo compatibility fix and a security hardening for browser subprocess credential exposure. The community is heavily focused on platform integrations (Feishu, Discord, Matrix), desktop UX polish, and feature proposals for agent-native task relay and shared memory. Overall, project health is busy but with a growing backlog of unaddressed high-priority bugs.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest release remains prior to this date.

---

## 3. Project Progress

**Merged / Closed PRs (6 total, top picks):**

- **[PR #37841 (closed)](https://github.com/nousresearch/hermes-agent/pull/37841)** – **fix: pad empty content on tool-call-only assistant messages for MiMo compatibility**  
  Resolves an API compatibility issue where Xiaomi (MiMo) rejected empty content fields on assistant turns that carried only tool calls.

- **[PR #37259 (closed)](https://github.com/nousresearch/hermes-agent/pull/37259)** – **fix(browser): scrub credentials from browser subprocess env**  
  Security fix: prevents provider credentials, gateway tokens, and GitHub tokens from leaking into the browser subprocess environment. This PR is a duplicate of the still-open #37843.

**Other closed PRs** include smaller doc fixes and test infrastructure changes (e.g., #37848, #37847, #37846). No major feature merges occurred.

---

## 4. Community Hot Topics

The most active discussions (by comment count) highlight key community pain points and future directions:

- **[Issue #25495 (10 comments)](https://github.com/nousresearch/hermes-agent/issues/25495)** – [P1] *Matrix / synapse broken in the official docker image*  
  The gateway for Matrix/Synapse is broken in the latest Docker images. User reports that logs stall at "fixing ownership :1000". This is a high-severity blocker for self-hosted deployments.

- **[Issue #31392 (8 comments)](https://github.com/nousresearch/hermes-agent/issues/31392)** – *RFC: Agent-native task relay with auto-forking subagents + async human approval gates*  
  A detailed proposal for a structured subagent orchestration system, complementing existing delegation features. High interest from the community.

- **[Issue #27221 (6 comments)](https://github.com/nousresearch/hermes-agent/issues/27221)** – [P2] *entrypoint.sh misses chown for ui-tui/ and gateway/ when HERMES_UID is remapped*  
  Docker UID remapping fails to update ownership for key directories, causing permission errors on systems like Unraid/Synology.

- **[Issue #31388 (4 comments)](https://github.com/nousresearch/hermes-agent/issues/31388)** – *RFC: Multi-profile shared memory store with on-demand capsule recall*  
  Proposal for a shared memory layer across profiles, complementing existing session search and Honcho integration.

- **[Issue #16525 (4 comments, 2 👍)](https://github.com/nousresearch/hermes-agent/issues/16525)** – *Expose model_switch as an agent-callable tool*  
  Feature request for autonomous task-complexity-based model routing. The agent currently cannot self-route without slash commands.

- **[Issue #27881 (4 comments)](https://github.com/nousresearch/hermes-agent/issues/27881)** – [P1] *Discord Gateway: Premature conversation turn termination*  
  The Discord gateway frequently stops mid-task, delivering only partial information. Contributor Lacks maintainer response.

- **[Issue #37447 (2 comments, 2 👍)](https://github.com/nousresearch/hermes-agent/issues/37447)** – *Show & Tell: DIKW Memory System*  
  A community-built 4-layer self-healing memory closure on top of Hermes' Holographic memory plugin. Positive reception.

**Underlying needs:** Users are demanding reliable Docker images, multi-platform desktop support, and deeper autonomous orchestration capabilities. The high number of RFCs suggests a strong desire for extensibility (subagents, shared memory, model switching).

---

## 5. Bugs & Stability

**High severity (P1):**
- **[Issue #25495](https://github.com/nousresearch/hermes-agent/issues/25495)** – Matrix/Synapse gateway broken in official Docker image. No fix PR yet.
- **[Issue #27881](https://github.com/nousresearch/hermes-agent/issues/27881)** – Discord Gateway prematurely terminates conversational turns. No fix PR.
- **[Issue #14065](https://github.com/nousresearch/hermes-agent/issues/14065)** – Named custom providers lose inline `api_key` during runtime resolution. Affects v12+ config. No fix PR.
- **[Issue #37827](https://github.com/nousresearch/hermes-agent/issues/37827)** – Windows setup fails with `git checkout main` error. Newly reported, needs repro.

**Medium severity (P2):**
- **[Issue #27221](https://github.com/nousresearch/hermes-agent/issues/27221)** – Docker entrypoint misses chown for ui-tui and gateway when UID remapped. No fix PR.
- **[Issue #24012](https://github.com/nousresearch/hermes-agent/issues/24012)** – Agent wastes tokens by trying unverified alternatives after tool failures. No fix PR.
- **[Issue #37399](https://github.com/nousresearch/hermes-agent/issues/37399)** – (closed) Hermes Desktop remote mode rejects WebSocket origins on non-loopback bind. Fixed? Not clear.

**Other notable bugs (P3):**
- **[Issue #37505](https://github.com/nousresearch/hermes-agent/issues/37505)** – macOS DMG is arm64-only, fails on Intel Macs. No fix PR.
- **[Issue #37813](https://github.com/nousresearch/hermes-agent/issues/37813)** – ACP mode ignores `platform_toolsets`, blocking memory provider tools. A fix PR [#37842](https://github.com/nousresearch/hermes-agent/pull/37842) is open.
- **[Issue #37527](https://github.com/nousresearch/hermes-agent/issues/37527)** – Desktop chat mouse-wheel scroll-up snaps back down in long threads. A fix PR [#37831](https://github.com/nousresearch/hermes-agent/pull/37831) is open.
- **[Issue #37244](https://github.com/nousresearch/hermes-agent/issues/37244)** – `browser_click` fails on SPA elements (React/Vue). No fix PR.

**Security-related:**
- **[PR #37843](https://github.com/nousresearch/hermes-agent/pull/37843) (open)** and **PR #37259 (merged)** address credential leakage from browser subprocess. Important hardening.

---

## 6. Feature Requests & Roadmap Signals

Several feature requests have gathered significant community attention:

- **Agent-native subagents** ([#31392](https://github.com/nousresearch/hermes-agent/issues/31392)) – Could become a flagship orchestration feature.
- **Multi-profile shared memory** ([#31388](https://github.com/nousresearch/hermes-agent/issues/31388)) – Aligns with growing multi-user deployment patterns.
- **Expose `model_switch` as a tool** ([#16525](https://github.com/nousresearch/hermes-agent/issues/16525)) – High-value for autonomous model routing; likely to be implemented soon given 2 👍.
- **`compress_context` as a native tool** ([#12213](https://github.com/nousresearch/hermes-agent/issues/12213)) – Simple but impactful; often requested in skill development.
- **Internal clock for agent time awareness** ([#27742](https://github.com/nousresearch/hermes-agent/issues/27742)) – Foundation for deadline management.
- **Service-account auth for Google Workspace** ([#17272](https://github.com/nousresearch/hermes-agent/issues/17272)) – Enables autonomous, non-interactive deployments.
- **Auditable decision trail for long runs** ([#32507](https://github.com/nousresearch/hermes-agent/issues/32507)) – Inspired by cursor/plugins; governance-focused.
- **Mobile-first Mac chat hub** ([#37835](https://github.com/nousresearch/hermes-agent/issues/37835)) – A PRD submitted, signalling a possible new direction for the desktop app.

**Predictions for next version:**
- Likely: `model_switch` tool and `compress_context` tool are low-hanging fruit.
- Possibly: Shared memory store or service-account auth for Google Workspace.
- Unlikely (but under discussion): Auto-forking subagents, which would require major architectural changes.

---

## 7. User Feedback Summary

**Pain points:**
- Docker image breakage (Matrix/Synapse) is the single most vocal issue (10 comments, 1 👍). Users are unable to self-host reliably.
- UID remapping in Docker (6 comments, 2 👍) frustrates users on NAS systems (Unraid/Synology).
- Discord gateway turn termination disrupts autonomous workflows.
- Windows setup failure (new) and Intel Mac incompatibility (new) degrade platform reach.
- Token waste from guesswork after tool failures frustrates power users.
- Desktop scroll bug and SPA clicking issues reduce UX quality.

**Satisfaction indicators:**
- Community members are actively building and sharing extensions: DIKW memory system (#37447, 2 👍) and RFC-style features (#31392, #31388).
- Several new contributors submitted PRs today (e.g., for Feishu multi-app, i18n, desktop fixes).
- The ecosystem is vibrant, with many non-English users participating (Korean, Chinese, etc.).

**Overall sentiment:** Energetic but frustrated by unresolved P1/P2 bugs that hinder production use. The feature pipeline is strong, but stability needs urgent attention.

---

## 8. Backlog Watch

| Issue / PR | Age | Priority | Comments | Status |
|------------|-----|----------|----------|--------|
| [#14065](https://github.com/nousresearch/hermes-agent/issues/14065) – Custom providers lose api_key | 2026-04-22 (42 days) | P1 | 4 | No maintainer reply |
| [#16525](https://github.com/nousresearch/hermes-agent/issues/16525) – Expose model_switch as tool | 2026-04-27 (37 days) | P3 | 4, 2👍 | No maintainer reply |
| [#5114](https://github.com/nousresearch/hermes-agent/issues/5114) – Autoresearch skill | 2026-04-04 (60 days) | P3 | 3 | No maintainer reply |
| [#12213](https://github.com/nousresearch/hermes-agent/issues/12213) – compress_context as tool | 2026-04-18 (46 days) | P3 | 3 | No maintainer reply |
| [#25495](https://github.com/nousresearch/hermes-agent/issues/25495) – Matrix/Synapse broken in Docker | 2026-05-14 (20 days) | P1 | 10 | No maintainer reply |
| [#27881](https://github.com/nousresearch/hermes-agent/issues/27881) – Discord turn termination | 2026-05-18 (16 days) | P1 | 4 | No maintainer reply |
| [#27221](https://github.com/nousresearch/hermes-agent/issues/27221) – Docker entrypoint chown | 2026-05-17 (17 days) | P2 | 6, 2👍 | No maintainer reply |
| [#37399](https://github.com/nousresearch/hermes-agent/issues/37399) – Desktop remote WebSocket origin | 2026-06-02 (1 day) | P2 | 2 (closed) | Closed but root cause unclear |
| [#37827](https://github.com/nousresearch/hermes-agent/issues/37827) – Windows setup error | 2026-06-03 (0 days) | P1 | 2 | Needs repro; no response yet |
| [#37244](https://github.com/nousresearch/hermes-agent/issues/37244) – SPA clicking fails | 2026-06-02 (1 day) | P3 | 1 | No response |

**Key takeaway:** Several long-standing P1/P2 issues lack any maintainer acknowledgement. The project maintainers are heavily focused on new features and platform integrations (e.g., Feishu, i18n) while critical bugs in Docker, Discord, and config resolution remain unaddressed. Community goodwill is being tested.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-06-03

## 1. Today's Overview
The PicoClaw project saw **high activity** in the last 24 hours, with **14 pull requests** updated and **3 issues** touched. One **automated nightly release (v0.2.9-nightly)** was published, reflecting ongoing work on the `main` branch. Community engagement is moderate, with one enhancement issue (#2404) generating sustained discussion. The maintainer team merged **6 fixes**, addressing goroutine leaks, provider error handling, session history quirks, and Zhipu API compatibility, indicating a strong focus on stability and provider coverage.

## 2. Releases
**Nightly build**: `v0.2.9-nightly.20260603.a502aa7f` (automated, possibly unstable)  
- Contains changes from the `main` branch since the last stable `v0.2.9` (no stable tag update).  
- **No explicit breaking changes or migration notes** are listed.  
- Download link: [GitHub Releases](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260603.a502aa7f)

## 3. Project Progress – Merged/Closed PRs Today
Six PRs were merged or closed on 2026-06-02/03:

| PR | Type | Description |
|----|------|-------------|
| [#2994](https://github.com/sipeed/picoclaw/pull/2994) | docs | Added a self-describing `picoclaw-agent` skill guide (workspace/skills). |
| [#2993](https://github.com/sipeed/picoclaw/pull/2993) | docs | Duplicate of above – closed. |
| [#2991](https://github.com/sipeed/picoclaw/pull/2991) | fix | Retry transient LLM HTTP errors using provider error classifier (improves OpenRouter/OpenAI fallback). |
| [#2989](https://github.com/sipeed/picoclaw/pull/2989) | fix | Added Zhipu API error code `1210` to format error patterns (fixes #2943). |
| [#2986](https://github.com/sipeed/picoclaw/pull/2986) | fix | Added `Stop()` to `SessionManager` to prevent goroutine leak in tests. |
| [#2239](https://github.com/sipeed/picoclaw/pull/2239) | enhancement | Modified Docker Compose to use `privileged` flag (closed after long inactivity). |

**Key fixes merged**:
- **LLM retry logic** now gracefully handles transient HTTP 500 errors.
- **Session goroutine leak** resolved – important for long-running daemons and test suites.
- **Zhipu GLM-5‑Turbo vision API** works again via WeChat channel.

## 4. Community Hot Topics
- **Most commented issue**: [#2404](https://github.com/sipeed/picoclaw/issues/2404) – *"Add in config to send streaming HTTP request"* (10 comments, 1 👍). Users want a simple `"streaming": true` config flag to enable SSE-like streaming from LLM backends (similar to OpenAI’s `stream=True`). The discussion suggests strong demand for streaming UX.
- **Most recent feature request**: [#2984](https://github.com/sipeed/picoclaw/issues/2984) – *"Add explicit turn completion signal for Pico WebSocket clients"* (1 👍, 0 comments). External protocol clients need a deterministic end-of-turn event; currently no signal exists.
- **Resolved bug with community interest**: [#2943](https://github.com/sipeed/picoclaw/issues/2943) – WeChat + GLM-5‑Turbo image error 1210. Closed after fix PR #2989 merged.

**Underlying needs**: Users are pushing for **real-time interaction improvements** (streaming, WebSocket status signals) and **broader provider compatibility** (especially Chinese LLM providers).

## 5. Bugs & Stability
Bugs reported or fixed in the last 24 hours, ordered by severity:

| Issue | Severity | Status | Fix PR |
|-------|----------|--------|--------|
| **Goroutine leak in SessionManager** | **High** – affects long-running servers and tests | Fixed | [#2986](https://github.com/sipeed/picoclaw/pull/2986) (merged) |
| **Zhipu GLM-5‑Turbo image API fails (code 1210)** | **High** – blocks WeChat image forwarding | Fixed | [#2989](https://github.com/sipeed/picoclaw/pull/2989) (merged) |
| **Session history shows only last user message in Web UI** | **Medium** – confuses users viewing multi‑turn conversations | Open PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) | Not merged yet |
| **`/context` command shows wrong compression threshold** | **Medium** – ignores `summarize_token_percent` config | Open PR [#2988](https://github.com/sipeed/picoclaw/pull/2988) | Not merged |
| **`tool_calls` dropped during active streaming** | **Medium** – may break tool-using agents | Open PR [#2987](https://github.com/sipeed/picoclaw/pull/2987) | Not merged |
| **New Web UI sessions inherit old messages after upgrade** | **Medium** – alias promotion bug (#2972) | Open PR [#2992](https://github.com/sipeed/picoclaw/pull/2992) | Not merged |
| **HTTP 400 on OpenAI endpoints with `web_search_preview`** | **Low** – affects some API providers | Open PR [#2951](https://github.com/sipeed/picoclaw/pull/2951) | Not merged |
| **Temperature parameter deprecated for `claude-opus-4-7`** | **Low** – model‑specific, elegantly fixable | Open PR [#2948](https://github.com/sipeed/picoclaw/pull/2948) | Not merged |

**All reported bugs have either been fixed or have an open PR in progress.** No regressions from the nightly release are noted.

## 6. Feature Requests & Roadmap Signals
- **Streaming HTTP config** (#2404) – most‑wished feature, likely to land in next stable (v0.3.0). Implementation seems straightforward (add config key, pass to provider client).
- **WebSocket turn completion signal** (#2984) – new request, could be part of protocol enhancements.
- **Debug trace viewer (picoclaw-tracer)** – open PR [#2945](https://github.com/sipeed/picoclaw/pull/2945). A standalone web UI for LLM call traces; if merged, it will become a powerful debugging tool.
- **Self‑describing agent skill** (PRs #2994/#2993) – documentation improvement that may become part of the official skill repository.

**Predictions for next version (v0.3.0):**
- High likelihood: streaming config support, tracer, session history fix, `/context` threshold fix.
- Medium likelihood: WebSocket turn completion signal.

## 7. User Feedback Summary
- **Pain points**:
  - Confusing context compression thresholds (ignores `summarize_token_percent` – #2968).
  - Missing session history in Web UI (#2796).
  - Tool calls dropped during streaming (#2958).
  - WeChat image forwarding broken with Zhipu GLM-5 (#2943, now fixed).
- **Desired features**:
  - Simple streaming toggle in config (#2404).
  - Deterministic end-of-turn event for external WebSocket clients (#2984).
  - Better debugging/tracing tools (#2945).
- **Satisfaction indicators**: The community actively upvotes requests and provides detailed bug reports; the maintainer team responds quickly with fix PRs – a sign of healthy project governance.

## 8. Backlog Watch
Issues and PRs that have been **stale** (no update in >7 days) or lack maintainer feedback:

| Item | Created | Last Update | Notes |
|------|---------|-------------|-------|
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) – Streaming config | 2026-04-07 | 2026-06-02 | **Stale** – 10 comments but no maintainer assignment or milestone. High demand; should be reviewed for next release. |
| [#2951](https://github.com/sipeed/picoclaw/pull/2951) – Fix `web_search` function type | 2026-05-26 | 2026-06-02 | **Stale** – open PR, no reviewer activity. |
| [#2948](https://github.com/sipeed/picoclaw/pull/2948) – Skip temperature for `claude-opus-4-7` | 2026-05-26 | 2026-06-02 | **Stale** – straightforward fix, awaiting review. |
| [#2945](https://github.com/sipeed/picoclaw/pull/2945) – Debug trace viewer | 2026-05-26 | 2026-06-02 | **Stale** – large feature PR, no maintainer comment. May need design discussion. |

**Recommendation**: Assign reviewers to the three stale PRs and set a milestone for #2404 to gauge priority.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-03

## 1. Today’s Overview
Activity on the NanoClaw repository was moderate, with one new issue opened and six pull requests updated in the last 24 hours. No new releases were published. The project continues to show forward momentum: four PRs were merged or closed, spanning bug fixes, security hardening, and new feature integrations. Community engagement remains low on the single open issue, while the PR queue reflects ongoing work on platform identification, runtime status messaging, and plugin extensibility. Overall project health appears stable, with maintainers actively reviewing and merging contributions.

## 2. Releases
No new releases were published today.

## 3. Project Progress
Four pull requests were merged or closed today, representing a mix of fixes and features:
- **#2674 – Standardize runtime status messages**  
  *Author: pinetreelic*  
  Introduces mechanical labels for long-running runtime status messages, adds metadata and internal-channel guards to prevent self-loops, and includes remaining local runtime/channel updates.  
  [PR #2674](https://github.com/nanocoai/nanoclaw/pull/2674)

- **#1193 – Host-side plugin hook system (onStartup/onShutdown)**  
  *Author: cyber-rye*  
  Adds a `src/plugin-loader.ts` that scans `plugins/*/index.js` for ES modules exporting lifecycle hooks. Plugins can start HTTP servers or other long-running services after channels connect but before the message loop.  
  [PR #1193](https://github.com/nanocoai/nanoclaw/pull/1193)

- **#2069 – Webchat skill v1**  
  *Author: javexed*  
  Adds a feature skill for webchat integration, including source code changes and a `SKILL.md` documentation file.  
  [PR #2069](https://github.com/nanocoai/nanoclaw/pull/2069)

- **#2538 – Validate package names before Dockerfile interpolation**  
  *Author: sebastiondev*  
  Fixes a command injection vulnerability (CWE‑78) in `buildAgentGroupImage()` by adding input validation for package names.  
  [PR #2538](https://github.com/nanocoai/nanoclaw/pull/2538)

## 4. Community Hot Topics
No issues or PRs attracted significant comments or reactions today. The single open issue (**#2673**) has zero comments and zero upvotes. The most actively discussed PRs are:

- **#2187 (open)** – Fix to avoid namespacing CLI bare platform IDs. Created 2026-05-02, last updated 2026-06-02. No comments.  
  [Issue #2187](https://github.com/nanocoai/nanoclaw/pull/2187)

- **#2672 (open)** – Fixes MCP union compatibility and HTTP-only transport for the Codex provider on the `providers` branch. No comments.  
  [PR #2672](https://github.com/nanocoai/nanoclaw/pull/2672)

The lack of community discussion suggests limited user visibility or that these changes are still early in review.

## 5. Bugs & Stability
Two bug fixes were merged today:
- **Critical – Command injection vulnerability (PR #2538)**  
  The fix adds validation of package names passed to Dockerfile interpolation, closing a potential CWE‑78 attack vector. This has been merged and should be included in the next release.

- **Moderate – CLI platform ID namespacing (PR #2187, still open)**  
  Adds a carve-out for the CLI channel to prevent incorrect namespacing of platform identifiers. An existing issue (#2186) is referenced as the root cause.

- **Moderate – MCP union compatibility (PR #2672, still open)**  
  Addresses a breaking change where trunk's `McpServerConfig` evolved into a union type, causing the Codex provider to fail. Also fixes HTTP-only transport behind proxies.

No crashes or regressions were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
- **#2673 – Automated Student Grading System (open)**  
  The issue describes an AI video prompt for a classroom scenario with a smartphone grading spreadsheet. While the description appears more like a user story or use case than a formal feature request, it suggests interest in integrating NanoClaw with educational grading workflows. No comments or votes exist, but it could signal demand for spreadsheet parsing or automated feedback capabilities.

- **#2069 (merged) – Webchat skill**  
  The addition of a webchat integration indicates the project is expanding beyond CLI and messaging channels into browser-based interactions.

- **#1193 (merged) – Plugin lifecycle hooks**  
  This foundational feature enables third-party developers to add custom startup/shutdown logic, which may pave the way for modular extensions in future releases.

Predictions for upcoming releases: The plugin hook system and webchat skill are likely candidates for the next stable release. The Codex MUX fixes in PR #2672 may also be backported if the `providers` branch is merged.

## 7. User Feedback Summary
No direct user feedback (comments, reactions, or reviews) is available in today’s data. However, the patterns of open issues and PRs hint at the following pain points and use cases:
- **Security concerns** – The CVE‑78 fix suggests users or contributors are actively auditing the codebase for injection risks.
- **Cross-platform compatibility** – The fix in PR #2187 addresses a bug where non‑CLI platforms incorrectly inherit namespaces, affecting users who rely on platform‑specific identifiers.
- **Extensibility demand** – Merging the plugin hook system and webchat skill indicates that users want to customise and embed NanoClaw in more environments.

Overall, the absence of negative feedback or unresolved complaints suggests that current users are either satisfied or not vocal.

## 8. Backlog Watch
- **PR #2187 (open since 2026-05-02)** – A straightforward fix for CLI platform ID namespacing that has been awaiting review for over a month. It references issue #2186, which is not listed in today’s data. This PR may require maintainer attention to prevent further delay.

No other issues or PRs have remained unanswered for an extended period. The single open issue (#2673) was created just yesterday and requires initial triage.

*All links are relative to `https://github.com/nanocoai/nanoclaw`.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-03

## 1. Today’s Overview
Activity over the past 24 hours has been low but focused. One new issue (#944) was reported, and one pull request (#945) was opened to address it—both centre on the same bug: the built-in PII redactor aggressively flags ISO-formatted date/time strings as phone numbers. No new releases or merged PRs occurred today. The team appears to be actively triaging the single reported regression, with a fix already under review.

## 2. Releases
*None.* No new releases were published today.

## 3. Project Progress
- **No merged or closed pull requests** today.
- **One open PR** (#945) proposes a targeted fix for the date/time false‑positive phone detection (see §5 for details).

## 4. Community Hot Topics
Only one issue and one PR were active today; neither has accumulated comments or reactions yet, but they form the community’s current focus.

| Item | Author | Created | Comments | 👍 | Link |
|------|--------|---------|----------|----|------|
| #944 (Issue) – PII redactor falsely matches date/time output as phone numbers | vernonstinebaker | 2026-06-02 | 0 | 0 | [Issue #944](https://github.com/nullclaw/nullclaw/issues/944) |
| #945 (PR) – fix(redaction): reject ISO date/time patterns as false-positive phone matches | vernonstinebaker | 2026-06-02 | 0 | 0 | [PR #945](https://github.com/nullclaw/nullclaw/pull/945) |

**Underlying need:** Users of NullClaw who enable PII redaction (default on since commit `41cdb493`) expect telemetry and agent command output to remain readable. The current regex‑based `matchPhone` is too aggressive, breaking system tools like `date`. The community needs a more nuanced redaction that respects structured data formats.

## 5. Bugs & Stability
One regression was reported today:

- **Bug #944** (Severity: **High**)
  - **Description:** PII redactor (enabled by default) replaces date/time sequences (e.g., `2026-06-02 20:17`) with `[PHONE_X]` placeholders, breaking any agent that calls `date` or similar commands.
  - **Impact:** Agent outputs become illegible for timestamps, logs, and scheduling; affects both autonomy and user‑facing messages.
  - **Fix available:** Yes, PR #945 adds a `isDateLike()` guard in `src/redaction.zig` to reject matches conforming to ISO 8601 patterns.
  - **Status:** Open, no comments yet; likely to be merged after review.

No other crashes, performance regressions, or memory issues were reported.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, the fix in PR #945 signals a roadmap priority: **robust PII redaction with format-aware exclusions**. This suggests the team is investing in redaction quality, which could lead to a configurable allowlist of patterns (e.g., dates, GUIDs, IPs) in future releases.

## 7. User Feedback Summary
The single reporter (vernonstinebaker) expressed clear frustration: the default redaction destroys essential agent output. Their pain point is that **default-on features should not break basic system commands**. No expressions of satisfaction were recorded today, but the swift opening of a fix suggests the maintainer (also the issue author) is actively improving the experience.

## 8. Backlog Watch
No long‑unanswered issues or PRs are currently languishing. The only older items (#944 and #945) are recent and already receiving attention. The project backlog appears healthy with no stale items needing maintainer intervention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-03

## 1. Today's Overview
The IronClaw project is in an intense development cycle, with **29 issues updated** and **50 pull requests updated** in the last 24 hours. Activity is dominated by two parallel efforts: a deep hygiene and correctness sweep of the new **Reborn agent loop** (issues L1–L11 and C1–C6) and a **bug bash (P2)** targeting model-specific regressions across Qwen3.6-35B, MiniMax-M2.7, and Claude Opus 4.7/4.8. Of the 31 merged/closed PRs today, most deliver targeted fixes for credential zeroization, subagent safety gating, OAuth flows, and the trigger capability surface. No new releases were published, but the volume of merged code suggests a release candidate is being prepared.

## 2. Releases
No new releases were created in the reporting window.

## 3. Project Progress
**31 PRs were merged or closed** today. Notable merges:

- **#4374** – `memory_search` now accepts aliases (`q`, `text`, `pattern`) alongside the canonical `query` field, exposed in the built-in input schema.  
- **#4357** – Local-dev Reborn mounts are now composite: libSQL root gets a `/memory` mount; fallback to `InMemoryBackend` when libSQL is unavailable.  
- **#4371** – Fixes Codex ChatGPT SSE parsing for `data-only` type events, `[DONE]`, and empty-response fallbacks; recovers Codex tool-call syntax.  
- **#4318** – First-party trigger capabilities (`trigger_create`, `trigger_list`, `trigger_remove`) are now wired into the Reborn runtime.  
- **#4347 / #4346** – Gmail OAuth auth gates now carry explicit least-privilege Google scopes and survive first-party auth failures.  
- **#4345** – Notion DCR OAuth is wired into the Reborn WebUI v2 serve composition.  
- **#4369** – Contract tests for skill-context budget (`safe_summary` / `model_content` split) hardened.  
- **#4372** – HTTP credential carriers zeroize URL and header buffers on drop (fixes #4222).  
- **#4370** – Compaction summary creation made retry-safe by persisting a durable marker before attempting the checkpoint write.  
- **#4373** – Subagent safety gating fixed: instruction safety context is now threaded through host/model prompt paths, flavor allowlist uses shared profile+driver predicate, and capability filter no longer relies on profile-id-only matching (fixes #4351).  

*Closed issues:* **#4355** (newtype client_thread_id / client_response_id on `ThreadExecutionContext`) and **#3806** (old Reborn lane 6 implementation) were both closed.

## 4. Community Hot Topics
Most active items by comment count (all have 0–1 comments, but the following generated clear signal from testers and contributors):

- **#4334** – [Claude Opus 4.7/4.8 unusable: temperature always sent](https://github.com/nearai/ironclaw/issues/4334)  
  Every request fails with a `400 invalid_request_error` because IronClaw unconditionally sends a `temperature` field. This is a **direct blocker** for users of these models.

- **#4341–#4344** – QA-reported bugs (P2) for Qwen3.6-35B-A3B-FP8 and MiniMax-M2.7 by `joe-rlo`. The issues cover thinking chain exposure, message echoing, MCP driver failure, stuck auth modals, and blank validation errors. These reflect real friction during planned QA testing on staging.

- **#3669** – [engine v2: expose channel-supplied thread/response IDs to tools](https://github.com/nearai/ironclaw/pull/3669) (PR, open since May 14, updated today)  
  This large PR restores an engine v1 contract that tools can use correlation IDs for side effects. It has been in review for several weeks, indicating careful validation.

- **#4108** – [Nightly E2E failed](https://github.com/nearai/ironclaw/issues/4108)  
  Automated nightly e2e tests on branch `749f584` failed at 2026-06-02 04:44 UTC. The `v2-engine` job was the specific failure. No root cause comment yet.

## 5. Bugs & Stability
**High severity:**
- **#4334** (Claude Opus 4.7/4.8) – Model unusable due to deprecated `temperature` parameter. No fix PR yet, but the issue is clearly understood (always-sent temperature). This likely requires a model-capability flag or parameter stripping.
- **#4108** – Nightly E2E failure indicates a regression in the v2-engine path. Unresolved.

**Medium severity (P2 QA bugs):**
- **#4341** – Agent thinking chain exposed to user and model stuck in thinking state (Qwen3.6-35B).
- **#4344** – Agent mirrors user message as own response while loading.
- **#4343** – MCP integration acknowledged but driver failure (Notion/GitHub extensions unusable).
- **#4342** – Authentication modal persists after page refresh, blocking chat.
- **#4340** – Content field blank validation error blocks message submission.
- **#4339** – Provider tool calls rejected as `InvalidInvocation` despite valid capability schema (MiniMax).
- **#4338** – Disconnected state shows misleading execution driver error.

No fix PRs are open for these QA bugs yet, but the pace of today’s merges (e.g., MCP negotiation in #4354, prompt safety in #4373) suggests remediation is in progress.

**Low severity fixes already merged:**
- **#4372** – Zeroize HTTP credential carriers (memory safety).
- **#4370** – Make compaction summary retry-safe (data loss risk).
- **#4369** – Harden skill-context budget contract tests.

## 6. Feature Requests & Roadmap Signals
Several issues and PRs point to incoming features:

- **Trigger system** – PR #4318 (trigger_create/list/remove) landed today; #4375 (trigger poller lifecycle) is open. This enables scheduled or event-driven agent runs.
- **Slack Reborn** – PR #4321 (final reply delivery, approval-auth interaction) is open, building on landed Slack adapter-core.
- **Hosted MCP negotiation** – PR #4354 bundles MCP session metadata persistence and OAuth credential reuse for Notion/GSuite.
- **Memory tool improvements** – #4374 (alias support) makes built-in `memory_search` more user-friendly.
- **Claude model compatibility** – #4334 will force a change to omit `temperature` for models that reject it. Likely to be addressed in the next release.

Predictions for next release: Reborn agent loop stability (L1–L11 cleanup), Claude Opus 4.7/4.8 support, Slack final-reply delivery, and further OAuth integration polish.

## 7. User Feedback Summary
Real pain points reported today:

- **Claude Opus 4.7/4.8 users** cannot use the model at all (#4334). This is the loudest feedback, as it blocks a premium model.
- **QA testers** (internal users) found multiple UI/runtime bugs in the staging environment for Qwen and MiniMax models. Their issues highlight that the latest engine v2 still has gaps in message handling, MCP integration, and authentication flows.
- **Memory search query format** was too rigid; the new alias support (#4374) directly addresses that complaint.

Overall satisfaction is likely low for users on recent models, but the development team is responding aggressively.

## 8. Backlog Watch
No issues appear to be genuinely stale. The two open PRs oldest in the set:
- **#3669** (engine v2 thread/response IDs, open 3 weeks) – Updated today, so actively being reviewed.
- **#3548** (DISABLE_TOOLS_LIST config flag, open 3 weeks) – Updated today, also active.

The nightly E2E failure (#4108) is recurring (first occurrence May 27) and should be prioritized to prevent regression creep.

*No long-unanswered community questions or unassigned critical bugs detected.*

---

**Overall project health:** Very active, high contributor velocity, but current model compatibility issues and QA bugs signal that the Reborn rollout needs a stabilization release before broad production deployment.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-03

**Data snapshot**: 0 new issues, 9 PRs updated (3 open, 6 merged/closed), 0 releases. Activity level is moderate, focused on bug fixes and incremental improvements rather than large feature releases. The project shows healthy maintenance velocity, with several critical fixes merged today.

## Releases

No new releases cut today.

## Project Progress

Six PRs were merged/closed today, advancing stability and functionality across multiple areas:

- **Image input support for MiniMax-M3** ([#2093](https://github.com/netease-youdao/LobsterAI/pull/2093)) – Fixed a hardcoded `supportsImage: false` that blocked image input for the newly added MiniMax-M3 model.
- **Hide internal OpenClaw plugins** ([#2096](https://github.com/netease-youdao/LobsterAI/pull/2096)) – Filters runtime-bundled plugin IDs from the plugin management UI to reduce user confusion.
- **Subagent batch deletion** ([#2095](https://github.com/netease-youdao/LobsterAI/pull/2095)) – Extended sidebar batch selection to subagent sessions and improved cleanup concurrency.
- **Share popup UI refinement** ([#2094](https://github.com/netease-youdao/LobsterAI/pull/2094)) – Optimised information hierarchy in the share success popup (Chinese description).
- **Artifacts feature update** ([#2092](https://github.com/netease-youdao/LobsterAI/pull/2092)) – A combined PR touching renderer, docs, main, and artifacts areas (details not fully disclosed).
- **MCP startup optimisation & timing logs** ([#2091](https://github.com/netease-youdao/LobsterAI/pull/2091)) – Pre-resolves and caches npx-based MCP packages to avoid slow startup on every session; adds first-response timing logs for debugging.

## Community Hot Topics

No issues or PRs received any comments or reactions in the last 24 hours. The most notable open items with prolonged activity are:

- **PR #388** ([link](https://github.com/netease-youdao/LobsterAI/pull/388)) – *feat: upgrade MiniMax default model to M3*. Open since March 12, marked stale. While the image support fix (#2093) landed, this broader model upgrade PR remains unmerged, possibly awaiting wider validation.
- **PR #1464** ([link](https://github.com/netease-youdao/LobsterAI/pull/1464)) – *fix(im): add duplicate validation for instance name and credential ID*. Open since April 4, last updated today. Addresses repeated user pain points about creating duplicate IM bots (DingTalk, Feishu, QQ).

**Underlying need**: Users expect robust multi-instance management for IM integrations and up-to-date model support without manual configuration.

## Bugs & Stability

All fixes reported today were resolved in the same day. No new bug reports (issues) were filed.

| Severity | Bug / Fix | Status |
|----------|-----------|--------|
| High     | MiniMax-M3 image input broken due to hardcoded flag | Fixed in [#2093](https://github.com/netease-youdao/LobsterAI/pull/2093) |
| Medium   | Internal plugins shown in user plugin list | Fixed in [#2096](https://github.com/netease-youdao/LobsterAI/pull/2096) |
| Medium   | Subagent transcripts not cleaned up after local deletion | Fixed in [#2095](https://github.com/netease-youdao/LobsterAI/pull/2095) |
| Low      | Unclear share popup info hierarchy | Fixed in [#2094](https://github.com/netease-youdao/LobsterAI/pull/2094) |
| Low      | npx MCP startup path slow every session | Fixed in [#2091](https://github.com/netease-youdao/LobsterAI/pull/2091) |

No regression reports or crashes were noted.

## Feature Requests & Roadmap Signals

While no explicit feature requests were filed, the merged PRs hint at the following roadmap directions:

- **Dependency upgrades**: PR #1277 (still open) bumps Electron from v40 to v42 and electron-builder – likely part of a maintenance cycle.
- **Subagent management**: Batch deletion and cleanup improvements (#2095) suggest the cowok/subagent feature is maturing toward production use.
- **MCP performance**: The npx resolution optimisation (#2091) signals that MCP (Model Context Protocol) integration is a growing priority, likely to be highlighted in the next release.
- **Model refresh**: The MiniMax-M3 image fix and the stalled model upgrade PR (#388) indicate a phased rollout of new default models.

**Prediction**: Next minor release will include MiniMax-M3 as default, MCP startup caching, and subagent UX improvements.

## User Feedback Summary

No direct user comments or issues were filed today. However, the merged PRs address explicit pain points reported in earlier periods:

- **Duplicate IM instances** (#1464) – users creating multiple bots with same App ID leads to message duplication.
- **Model image support confusion** – users enabling image input for MiniMax-M3 but getting no results (fixed in #2093).
- **Plugin clutter** – internal plugins appearing in user lists caused confusion (fixed in #2096).

Overall satisfaction appears high: all fixes landed within 24 hours of being proposed.

## Backlog Watch

Three long-standing PRs require maintainer attention:

1. **#388** – *feat: upgrade MiniMax default model to M3* (opened 2026-03-12, stale). After 2.5 months and with the image fix already merged, this should be reviewed and either merged or superseded.
2. **#1277** – *chore(deps-dev): bump the electron group* (opened 2026-04-02). A dependency bump that may need conflict resolution or testing before merging.
3. **#1464** – *fix(im): add duplicate validation for instance name and credential ID* (opened 2026-04-04). Actively updated today but still open – likely needs code review or final sign-off.

No bug reports remain open, indicating strong responsiveness to stability issues.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-03

## 1. Today's Overview
Project activity was low over the past 24 hours, with only one new issue opened and one existing pull request updated. No releases were published. The single open issue (#1092) proposes a configuration toggle to suppress tool-status messages in channel replies, reflecting ongoing usability refinement. The sole active PR (#1089) continues to mature, aimed at capping persisted tool results during session rehydration. Overall, development appears stable but at a quiet pace, with focus on incremental improvements rather than new features.

## 2. Releases
No new releases were published in the last 24 hours. The latest release remains the previous version; no migration notes or breaking changes to report.

## 3. Project Progress
- **No PRs were merged or closed today.**  
- **PR #1089** (open) – “Cap persisted tool results before rehydration” was updated on 2026-06-03. This PR introduces a capacity limit on `tool` and `tool_result` content when session history is rehydrated into provider-bound messages. It applies to normal chat, streaming chat, retry-after-compaction, prompt inspection, silent memory turns, and LLM-backed compaction prompts, while preserving persisted state. The update suggests the author is actively iterating on this feature; it is a candidate for merging soon.

## 4. Community Hot Topics
- **Issue #1092** (open, 0 comments, 0 👍) – “Add a config option to disable channel Activity log tool-status messages.”  
  - *Link:* [moltis-org/moltis Issue #1092](https://github.com/moltis-org/moltis/issues/1092)  
  - **Analysis:** The user reports that Telegram channel replies include a collapsible HTML “Activity log” block after agent responses whenever tools are used, which can be disruptive, especially when the main answer is already delivered via streaming. The underlying need is for cleaner user-facing output, particularly in channel environments where such logs may be noisy or unwanted. This request signals a desire for higher configurability of UI elements.

- **PR #1089** (open, 0 comments, 0 👍) – “Cap persisted tool results before rehydration.”  
  - *Link:* [moltis-org/moltis PR #1089](https://github.com/moltis-org/moltis/pull/1089)  
  - **Analysis:** While no direct discussion has occurred, this PR addresses a potential stability and memory issue: large tool results could overwhelm session rehydration. The community need is for reliable long-running sessions without performance degradation.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The only open issue is a feature request, and the open PR is an enhancement. Project stability appears good at this time.

## 6. Feature Requests & Roadmap Signals
- **Configurable tool-status output** (#1092): The request to disable Activity log messages in channels is a clear UX improvement. Given the simplicity of the change (a config toggle), it is plausible that this could be included in the next minor release if accepted.  
- **Capping of tool results** (PR #1089): This enhancement directly improves session reliability and memory usage. It is a strong candidate for the upcoming version, possibly the next patch or minor release.

## 7. User Feedback Summary
No explicit user satisfaction or dissatisfaction feedback was recorded today. The single issue (#1092) represents a real pain point: users in channel deployments find the automatic Activity log cluttering and seek a simple way to disable it. This indicates a segment of the user base that values minimal, clean agent responses over diagnostic transparency.

## 8. Backlog Watch
- No issues or PRs were identified as long-unanswered or needing maintainer attention. The project’s backlog appears well-managed, with recent activity focusing on active items.  
- **Note:** PR #1089 has been open since 2026-06-01 (3 days) and received an update today, so it is not stagnant. No other items require escalation.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-03

**Project**: [CoPaw (github.com/agentscope-ai/CoPaw)](https://github.com/agentscope-ai/CoPaw)  
**Data snapshot**: Issues updated in last 24h: 36 (16 open, 20 closed) · PRs updated in last 24h: 29 (19 open, 10 merged/closed) · New releases: 0

---

## 1. Today’s Overview

The project saw high activity with 36 issues and 29 pull requests touched in the last 24 hours, reflecting sustained community engagement and maintainer responsiveness. 10 PRs were merged or closed, and 20 issues were resolved, indicating steady progress on fixes and features. A notable security audit by one contributor resulted in the disclosure and closure of five vulnerabilities (issues #4908–#4914), all of which were accepted and remediated quickly. No new releases were published today; the latest tagged version remains v1.1.10, with a beta bump PR (#4907) merged for v1.1.11b1. Several long-standing open PRs (e.g., sandbox integration #2275, plugin prompt sections #4804) continue to be updated, signalling ongoing review.

## 2. Releases

*None* – no new releases were published on 2026-06-03.

## 3. Project Progress (Merged/Closed PRs)

Ten PRs were merged or closed today. Key changes include:

| PR | Title & Impact |
|----|----------------|
| [#4906](https://agentscope-ai/QwenPaw/pull/4906) | **fix(coding-mode): support browsing all drives on Windows** – Resolves a limitation where the file browser was locked to the C: drive root. Now lists all available drive letters with a virtual root. |
| [#4907](https://agentscope-ai/QwenPaw/pull/4907) | **chore(release): bump version to v1.1.11b1** – Prepares next beta release. |
| [#4883](https://agentscope-ai/QwenPaw/pull/4883) | **fix(channel): cron messages fail to deliver to wechat/wecom with share_session=false** – Closes a critical delivery bug (#4878) for scheduled tasks. |
| [#4850](https://agentscope-ai/QwenPaw/pull/4850) | **fix(wecom): resolve session_id from authenticated sender_id** – Addresses memory isolation issue (#4845) in the WeCom channel. |
| [#4853](https://agentscope-ai/QwenPaw/pull/4853) | **fix(browser): kill entire process tree and clean lock files on Windows** – Fixes persistent browser processes and temp directory locks after session end (closes #4844). |
| [#4772](https://agentscope-ai/QwenPaw/pull/4772) | **optimize Windows startup with lazy loading, caching and progressive initialization** – First-time contributor contribution improving win startup performance. |
| [#4689](https://agentscope-ai/QwenPaw/pull/4689) | **feat(providers): route non-standard generate_kwargs into extra_body** – Enables dashscope `enable_search` and similar provider‑specific params to work correctly. |
| [#1317](https://agentscope-ai/QwenPaw/pull/1317) | **feat(console): add download status notifications for cloudflared** – UX improvement showing real-time download progress. |
| (#4890 related) | [Bug fix for Yuanbao channel missing proto files](https://agentscope-ai/QwenPaw/issue/4890) – Additional package fix (PR details not listed explicitly but issue closed with fix). |
| (#4898 related) | Yuanbao channel protobuf schema fix – Issue #4898 closed; fix ensures `proto/conn.json` and `proto/biz.json` are included in the package. |

---

## 4. Community Hot Topics

### Most commented issues (last 24h)

| Issue | Comments | Topic |
|-------|----------|-------|
| [#4878](https://agentscope-ai/QwenPaw/issues/4878) | 5 | **Bug**: Cron task messages not delivered to WeChat – resolved by PR #4883. |
| [#4908](https://agentscope-ai/QwenPaw/issues/4908) | 4 | **Security**: Unauthenticated `PUT /api/settings/language` allows persistent global settings modification. Closed. |
| [#3985](https://agentscope-ai/QwenPaw/issues/3985) | 4 | **Bug**: DeepSeek `reasoning_content` not passed back in multi‑turn calls causing HTTP 500. Closed. |
| [#4893](https://agentscope-ai/QwenPaw/issues/4893) | 4 | **Feature**: Windows file upload should not be size-limited (local path passing vs. upload). |
| [#4877](https://agentscope-ai/QwenPaw/issues/4877) | 3 | **Bug**: Custom channel stops listening every time settings are saved – root cause identified in `channel/manager.py`. |

**Analysis**: The most active discussions centre on channel delivery reliability (WeChat/WeCom), context compression quality, and UX friction on Windows (file upload limits, chat performance). The security batch of five issues (#4908–#4914) by one researcher generated significant attention but were all accepted and closed quickly, demonstrating strong maintainer responsiveness.

---

## 5. Bugs & Stability

Bugs reported or updated today, ranked by severity:

### Critical
- **Security vulnerabilities (5 closed)**: Path traversal in `system_prompt_files` ([#4913](https://agentscope-ai/QwenPaw/issues/4913)), ToolGuard bypass via `_headless_tool_` ([#4909](https://agentscope-ai/QwenPaw/issues/4909)), workspace export leaking secrets ([#4914](https://agentscope-ai/QwenPaw/issues/4914)), unvalidated timezone causing 500s ([#4912](https://agentscope-ai/QwenPaw/issues/4912)), malformed session_id causing persistent chat creation failure ([#4910](https://agentscope-ai/QwenPaw/issues/4910)). All closed; fix PRs assumed to be merged.

### High
- **Context compression failure** ([#4924](https://agentscope-ai/QwenPaw/issues/4924)): `Failed to compact memory` due to old‑format file blocks. New, no fix PR yet. Potentially affects all long‑running agents.
- **browser_use startup failure on Windows** ([#4919](https://agentscope-ai/QwenPaw/issues/4919)): Managed CDP timeout + Chrome/Edge crash. Workaround via npm playwright-cli reported. No fix PR yet.
- **Custom channel stop on save** ([#4877](https://agentscope-ai/QwenPaw/issues/4877)): Logic bug in `replace_channel` – new channel started before old one stopped, causing port conflict. Root cause identified in issue.

### Medium
- **Permission error after image retrieval via WeChat** ([#4922](https://agentscope-ai/QwenPaw/issues/4922)): Agent enters persistent crash loop. Clean session does not help. No fix PR.
- **MCP tool names with dots break gpt-5.5 calls** ([#4918](https://agentscope-ai/QwenPaw/issues/4918)): Validation error on `tools[].name`. Framework needs sanitization.
- **Images loaded as raw data into context** ([#4921](https://agentscope-ai/QwenPaw/issues/4921)): Base64 images waste tokens – requests to treat as references.

### Low / UX
- Unexpected loading state when switching chats ([#4903](https://agentscope-ai/QwenPaw/issues/4903))
- Up arrow key returns previous message instead of moving cursor ([#4920](https://agentscope-ai/QwenPaw/issues/4920)) – closed as question.
- Chat interface lag with many messages ([#4917](https://agentscope-ai/QwenPaw/issues/4917))

---

## 6. Feature Requests & Roadmap Signals

Top user-requested features from today’s data:

| Feature | Issue | Likelihood for next version |
|---------|-------|----------------------------|
| **Per‑task model selection for `spawn_subagent`** (e.g., cheap model for simple tasks) | [#4901](https://agentscope-ai/QwenPaw/issues/4901) | Medium – aligned with token‑saving roadmap |
| **Tool definition lazy loading** (reduce initial context token overhead by 55–65%) | [#4836](https://agentscope-ai/QwenPaw/issues/4836) | High – performance impact widely felt |
| **Lossless context compression** (DAG‑based summarization + CJK token fix) | [#4551](https://agentscope-ai/QwenPaw/issues/4551) | Medium – complex, but many users affected |
| **Windows: multi‑file drag‑and‑drop upload** | [#4894](https://agentscope-ai/QwenPaw/issues/4894) | High – direct UX request for Windows users |
| **Windows: remove file upload size limit** (local path mode) | [#4893](https://agentscope-ai/QwenPaw/issues/4893) | High – easy fix, waiting for implementation |
| **Simplify sidebar menu** (reduce settings, surface chat sessions) | [#4904](https://agentscope-ai/QwenPaw/issues/4904) | Medium – UX/design effort needed |
| **Plugin‑registered custom channels with schema‑driven config UI** | PR [#4693](https://agentscope-ai/QwenPaw/pull/4693) | High – already under review |

**Prediction**: The next release (v1.1.11) will likely include the Windows file upload fix (#4893), multi‑file drag‑and‑drop (#4894), and potentially the tool definition lazy loading (#4836) given its prominence. The custom channel plugin system (#4693) and prompt section registry (#4804) are also strong candidates.

---

## 7. User Feedback Summary

Based on issue descriptions and comments:

**Positive signals**:
- Users actively experiment with agent capabilities (cron tasks, multi‑channel delivery, sub‑agent spawning).
- Community contributes both bug reports with detailed root‑cause analysis (e.g., #4877, #3985) and feature PRs (e.g., #4902 manage_prd tool).
- Chinese‑language community is very active, providing clear reproductions and logs.

**Pain points**:

- **Channel reliability**: WeChat/WeCom cron delivery fails (#4878 fixed, but general stability concerns remain).
- **Windows experience**: File upload limits (#4893), lack of drag‑and‑drop, browser startup failures (#4919), and chat lag (#4917) frustrate desktop users.
- **Context management**: Both compression failures (#4924) and inflation from images (#4921) degrade long‑session quality. The `reserve_threshold_ratio` of 0.1 is criticised as too aggressive (#4551).
- **Security awareness**: Several users expressed concern about prompt injection risks in multi‑user channels (e.g., #4845). The flurry of closed security issues shows the team takes reports seriously.
- **UI/UX friction**: Sidebar complexity (#4904), unexpected keyboard behaviour (#4920), and missing loading indicators (#4903) are minor but frequently mentioned.

---

## 8. Backlog Watch

These issues and PRs have remained open for extended periods and may need maintainer attention:

| Item | Age | Notes |
|------|-----|-------|
| [PR #2275](https://agentscope-ai/QwenPaw/pull/2275) – feat(sandbox): add E2B and AgentScope sandbox backend integration | 10 weeks (since Mar 25) | Large feature, first‑time contributor, still under review. No recent maintainer comments visible. |
| [PR #4683](https://agentscope-ai/QwenPaw/pull/4683) – fix(desktop): fix Tauri desktop external links | 8 days (since May 26) | Updated today, but still open. Important for desktop distribution. |
| [PR #4804](https://agentscope-ai/QwenPaw/pull/4804) – feat(plugins): prompt section registry | 5 days (since May 29) | Under review, updated today – actively groomed. |
| [Issue #4551](https://agentscope-ai/QwenPaw/issues/4551) – Feature request: lossless context compression | 14 days (since May 20) | Well‑specified, 3 comments, no maintainer response yet. Likely complex but community demand is high. |
| [Issue #4837](https://agentscope-ai/QwenPaw/issues/4837) – v1.1.9 frequent system fallback “unable to process your problem” | 3 days (since May 31) | Multiple users reporting the same symptom; no fix PR yet. |
| [Issue #4845](https://agentscope-ai/QwenPaw/issues/4845) – WeWork channel lack of memory isolation | 2 days (since June 1) | Closed – but the root problem (prompt injection able to leak history) was only partially addressed by PR #4850 (session_id validation). Full isolation may need further work. |

**Recommendation**: Prioritise review of PR #2275 (sandbox) as it has been open longest and represents a major architectural addition. Also investigate issue #4837 (fallback replies) which appears to be a regression affecting many users.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-03

## 1. Today’s Overview
Activity remains high with **50 issues and 50 pull requests updated in the last 24 hours**, of which 33 issues and 47 PRs were closed or merged. The highlight is the **v0.8.0-beta-2 release**, which introduces a full-featured terminal UI (`zerocode`) and a multi-agent runtime – the largest update since v0.7.5. Bug-fix velocity is strong: many high-priority issues (e.g., default_model, WhatsApp protocol bumps, sandbox restrictions) have been resolved. A few open issues around gateway security and provider-specific failures still require attention.

## 2. Releases
- **[v0.8.0-beta-2](https://github.com/zeroclaw-labs/zeroclaw/releases)** – Headliner: **zerocode** – a complete terminal UI for operating agents without leaving the terminal. Ships with the multi-agent runtime for coordinating multiple agents. No explicit breaking changes or migration notes are documented; as a beta, users should expect continued iteration. This release marks the largest feature increment since v0.7.5.

## 3. Project Progress (Merged/Closed PRs Today)
Today saw **47 PRs merged or closed** (out of 50 updated), covering a wide range of improvements:

- **Docs & CI** – Versioned documentation deployment & version selector ([#7023](https://github.com/zeroclaw-labs/zeroclaw/pull/7023)), fix for shared chrome overwrite ([#7124](https://github.com/zeroclaw-labs/zeroclaw/pull/7124)), Python skills quickstart ([#6057](https://github.com/zeroclaw-labs/zeroclaw/pull/6057)), removal of stale CI references ([#6133](https://github.com/zeroclaw-labs/zeroclaw/pull/6133)).
- **Skills** – Whitelist filter & LLM-assisted skill improvement ([#5420](https://github.com/zeroclaw-labs/zeroclaw/pull/5420)), Hermes-style SKILL.md generation ([#5874](https://github.com/zeroclaw-labs/zeroclaw/pull/5874)), restricted audit to structural checks ([#5952](https://github.com/zeroclaw-labs/zeroclaw/pull/5952)), pass `allow_scripts` to skill loader ([#5981](https://github.com/zeroclaw-labs/zeroclaw/pull/5981)), respect `timeout_secs` from SKILL.toml ([#6054](https://github.com/zeroclaw-labs/zeroclaw/pull/6054)).
- **Tools & Channels** – IPv6 support for web tools ([#5450](https://github.com/zeroclaw-labs/zeroclaw/pull/5450)), WhatsApp Web reinstall guidance ([#5075](https://github.com/zeroclaw-labs/zeroclaw/pull/5075)), cron tool-only output handling ([#6026](https://github.com/zeroclaw-labs/zeroclaw/pull/6026)).
- **Config & Observability** – OTel tool spans enriched ([#6009](https://github.com/zeroclaw-labs/zeroclaw/pull/6009)), `allowed_path`/`allowed_paths` aliases for `allowed_roots` ([#6086](https://github.com/zeroclaw-labs/zeroclaw/pull/6086)).
- **Providers** – Sanitized llama.cpp Gemma4 tool schemas ([#5254](https://github.com/zeroclaw-labs/zeroclaw/pull/5254)), stripped media markers in auxiliary LLM calls ([#6114](https://github.com/zeroclaw-labs/zeroclaw/pull/6114)).
- **UI** – Fixes for browser translation crashing chat DOM ([#7077](https://github.com/zeroclaw-labs/zeroclaw/pull/7077)), avoid UTF-8 char-boundary panics in dashboard ([#7123](https://github.com/zeroclaw-labs/zeroclaw/pull/7123)).

## 4. Community Hot Topics
The most commented issues and PRs today reveal three underlying themes:

- **Onboarding & fresh-install friction** – [#6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123) (18 comments, closed) reports `default_model` errors on a fresh LXC setup. Users are confused by provider/model configuration defaults.
- **Shell sandbox blocking realistic Python workflows** – [#5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722) (6 comments, closed) documents how the default sandbox blocks Python skill patterns, triggering workarounds documentation.
- **Channel connectivity regressions** – [#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246) (6 comments, closed) describes a WhatsApp Web protocol bump (server-side) that silently stops message flow. The fix appears to be merged.
- **Ollama provider tool-call failures** – [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) (6 comments, **still open**) blocks tool-using sessions entirely with Ollama; users are waiting for a fix.

Other active items: SkillForge auto-integrator emitting non-schema fields ([#6210](https://github.com/zeroclaw-labs/zeroclaw/issues/6210), closed), ACP cancellation support requested ([#5837](https://github.com/zeroclaw-labs/zeroclaw/issues/5837), closed), and a gateway security bypass for supervised approvals ([#6207](https://github.com/zeroclaw-labs/zeroclaw/issues/6207), closed with fix).

## 5. Bugs & Stability
Several high-severity bugs were resolved today, while others remain open:

| Issue | Severity | Status | Summary |
|-------|----------|--------|---------|
| [#5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722) | S1 – blocked | **Closed** (PR #6057 docs fix) | Default shell sandbox blocks Python/R/Julia skills |
| [#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246) | S1 – blocked | **Closed** | WhatsApp Web channel silent failure after protocol bump |
| [#6207](https://github.com/zeroclaw-labs/zeroclaw/issues/6207) | S1 – blocked | **Closed** | WebSocket gateway bypasses ApprovalManager |
| [#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269) | S2 – degraded | **Closed** | Context compressor drops `reasoning_content` for DeepSeek |
| [#6878](https://github.com/zeroclaw-labs/zeroclaw/issues/6878) | S2 – degraded | **Closed** | Bubblewrap fails on Fedora 43 due to missing /lib64 |
| [#6681](https://github.com/zeroclaw-labs/zeroclaw/issues/6681) | S1 – blocked | **Closed** | `zeroclaw skills install` panics due to blocking reqwest |
| [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | S1 – blocked | **Open** | Ollama provider fails when tools are needed (6 comments) |
| [#6127](https://github.com/zeroclaw-labs/zeroclaw/issues/6127) | S1 – blocked (?) | **Open** (P1) | Gateway silent-fallback hardening after #6099 |
| [#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155) | S1 – blocked | **Open** (P1) | Delegate agents ignore `prompt_injection_mode` |
| [#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120) | S1 – blocked | **Open** (P1) | Onboarding asks for OpenAI API key even for Codex subscription |

Most closed bugs have corresponding fix PRs (e.g., #5981 for allow_scripts, #6054 for timeout_secs). The open issues around Ollama, gateway fallback, delegate injection, and onboarding remain blockers for some users.

## 6. Feature Requests & Roadmap Signals
The v0.8.0-beta-2 release ships the **zerocode TUI**, addressing the long-standing tracker [#6824](https://github.com/zeroclaw-labs/zeroclaw/issues/6824). Other signal-carrying items:

- **Skills from `.well-known` URI** ([#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853), open, P2) – standardizing skill discovery.
- **ACP protocol extensions for diff/file-proposal** ([#6820](https://github.com/zeroclaw-labs/zeroclaw/issues/6820), closed with partial implementation) – enables side-by-side diffs in TUI/web.
- **Move TUI crate to `apps/zerocode`** ([#6821](https://github.com/zeroclaw-labs/zeroclaw/issues/6821), closed) – completed in the release.
- **Skills documentation** ([#5863](https://github.com/zeroclaw-labs/zeroclaw/issues/5863), closed) – created docs for skill format.
- **Skill audit scope documentation** ([#5956](https://github.com/zeroclaw-labs/zeroclaw/issues/5956), closed) – structural checks only.

Likely next: continued refinement of `zerocode` (e.g., approval UI, diff display) and standardized skill registry support.

## 7. User Feedback Summary
Real pain points surfaced in today’s activity:

- **Onboarding friction**: Fresh LXC users hit silent `default_model` errors ([#6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)). The onboarding tool also confuses Codex subscribers by requesting OpenAI API keys ([#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120)).
- **Sandbox restrictions**: Default bubblewrap sandbox blocks almost all practical Python/R/Julia skills ([#5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722)), forcing users to create custom sandbox profiles.
- **Channel reliability**: WhatsApp Web integration broke server-side with no warning ([#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)); Telegram cron delivery also had raw tool calls leaking ([#6026](https://github.com/zeroclaw-labs/zeroclaw/issues/6026)).
- **Provider-specific issues**: Ollama tool calls fail blocking sessions ([#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)); deepseek `reasoning_content` lost during compression ([#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)); zai-cn returns 1214 error with glm-5-turbo ([#5636](https://github.com/zeroclaw-labs/zeroclaw/issues/5636), closed).
- **Security bypass concerns**: WebSocket chat endpoint bypasses approval manager ([#6207](https://github.com/zeroclaw-labs/zeroclaw/issues/6207)); ACP `cwd` changes can lock agents out of skill files ([#6516](https://github.com/zeroclaw-labs/zeroclaw/issues/6516)).
- **Satisfaction**: Users appreciate rapid bug fixes (many issues closed same day), the new TUI, and better documentation for Python skills.

## 8. Backlog Watch
The following high-priority open issues have multiple comments and have not been resolved:

- **[#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962)** (6 comments, P2, in-progress) – Ollama provider tool call failure. A fix is being worked but not yet merged.
- **[#6127](https://github.com/zeroclaw-labs/zeroclaw/issues/6127)** (4 comments, P1, accepted)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*