# OpenClaw Ecosystem Digest 2026-06-08

> Issues: 295 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-08 02:52 UTC

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

# OpenClaw Project Digest — 2026-06-08

## Today's Overview

The OpenClaw repository continues to sustain extremely high activity levels: **295 issues** and **500 pull requests** updated in the last 24 hours, with a healthy closure/merge rate of **115 closed issues** (39%) and **166 merged/closed PRs** (33%). No new releases were published today. The project shows robust engineering throughput but also reveals persistent tensions around security-critical bugs, session state reliability, and message delivery integrity — several diamond-lobster-rated issues remain open with stale labels. Notably, multiple P1 regressions and two new security-tagged issues (#91283, #91212) were filed within the past 24 hours, suggesting the codebase is under active stress from both feature growth and production deployment patterns.

---

## Releases

**None.** No new versions were published on 2026-06-08. The most recent release remains from a prior date.

---

## Project Progress

**Merged/closed PRs today** (selected highlights from the 166 merged/closed):

- **[#91304]** [`fix(agents): strip reasoning_content placeholder signatures from Anthropic replay history`](https://github.com/openclaw/openclaw/pull/91304) — Fixes cross-provider session reloads where OpenAI-compat wire sentinels (`thinkingSignature: "reasoning_content"`) appeared in native Anthropic replay turns.
- **[#87909]** [`fix(inbound-meta): head+tail truncation for reply context body preserves actionable tail content`](https://github.com/openclaw/openclaw/pull/87909) — Closed with maintainer approval; improves multi-paragraph reply sanitization for long bot messages.
- **[#68113]** (Issue `[CLOSED]`) — Mattermost slash commands regression (503 "not yet initialized") resolved, originally filed against v2026.4.15.
- **[#73802]** (Issue `[CLOSED]`) — Discord exec approval cards/buttons regression from #71804 has been fixed.
- **[#88234]** (Issue `[CLOSED]`) — Feishu dispatch TypeError (`Cannot read properties of undefined (reading 'run')`) resolved.

**Notable open PRs with maintainer review requested:**
- **[#90328]** [`Expose model picker agent runtimes`](https://github.com/openclaw/openclaw/pull/90328) — Adds `agentRuntime` metadata to model choices for the WebUI picker. `merge-risk: compatibility`, P2.
- **[#85829]** [`Avoid post-run auth success lane delay`](https://github.com/openclaw/openclaw/pull/85829) — Moves auth bookkeeping off the reply-blocking path, P1, `status: ready for maintainer look`.
- **[#91081]** [`perf(memory): coalesce + cache session-file listings to cut NFS READDIR load`](https://github.com/openclaw/openclaw/pull/91081) — Addresses filesystem I/O overhead for networked deployments, P2.

---

## Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Title | Comments | 👍 |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | 27 | 1 |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Track core session/transcript SQLite migration via accessor seam | 18 | 1 |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | [Regression] Codex app-server turn-completion stall | 14 | 3 |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | Bootstrap files in agentDir silently ignored | 14 | 5 |
| [#90991](https://github.com/openclaw/openclaw/issues/90991) | Cron scheduled trigger contaminates global runtime state | 13 | 1 |

**Analysis of underlying needs:**

The hottest issue (#25592, 27 comments) — "Text between tool calls leaks to messaging channels" — reflects a core UX friction: internal agent processing output (error messages, acknowledgments, narration between tool invocations) is being broadcast as user-visible chat messages. The community is signaling a strong desire for **clean separation of internal agent state from external channel output**, which has implications for how streaming, tool orchestration, and conversation assembly are designed.

Issue #90991 (cron trigger contaminating global runtime state) and #88312 (turn-completion regression on Codex) both point to **reliability regressions in the multi-tenant / multi-session runtime** — systemic failures that affect all sessions, not just the originating one. The 13-comment thread on #90991 includes detailed diagnostic logs and a bisection across upgrade paths (2026.5.12 → 2026.5.26 → 2026.6.1), indicating community members are doing significant investigative work.

### Most Active PRs

- **[#91276](https://github.com/openclaw/openclaw/pull/91276)** — `fix(tui): include pairing approval command in recovery hint` — New today, addresses a TUI disconnect UX gap.
- **[#91303](https://github.com/openclaw/openclaw/pull/91303)** — `fix(npm-shrinkwrap): update hono from 4.12.18 to 4.12.23` — Security vulnerability fix, filed same-day with the issue.
- **[#91299](https://github.com/openclaw/openclaw/pull/91299)** — `fix(memory-core): write ## Deep Sleep summary into DREAMS.md` — Documentation gap closure for the dreaming subsystem.

---

## Bugs & Stability

### Critical (P1, Diamond/Platinum Lobster — highest severity)

| Issue | Title | Status | Fix PR? |
|---|---|---|---|
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | [Regression] Codex app-server turn-completion stall ("Codex stopped before confirming") | **OPEN**, P1, needs-live-repro | No open fix PR |
| [#90991](https://github.com/openclaw/openclaw/issues/90991) | Cron scheduled trigger contaminates global runtime state | **OPEN**, P1, needs-live-repro | No open fix PR |
| [#91212](https://github.com/openclaw/openclaw/issues/91212) | delivery-recovery 0 recovered / N failed after gateway restart | **OPEN**, P1, needs-live-repro, **filed today** | No open fix PR |
| [#91283](https://github.com/openclaw/openclaw/issues/91283) | minSecurity inverted — `security="full"` clamped to `"allowlist"` | **OPEN**, P3 security, **filed today** | No open fix PR |
| [#90639](https://github.com/openclaw/openclaw/issues/90639) | compaction: safeguard mode allows sessions to grow to context ceiling; "Something went wrong" on Slack | **OPEN**, P1, needs-live-repro | No open fix PR |
| [#90428](https://github.com/openclaw/openclaw/issues/90428) | exec tool triggers gateway SIGTERM restart on WSL2 with Node 24 | **OPEN**, P1 regression | No open fix PR |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` tool does not inherit `skills.entries.*.env` environment variables | **OPEN**, P1 regression, security | Linked PR open (#58823 addresses related subagent model issue only) |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | **OPEN**, P1, security | No fix PR; needs product decision |

**New today (highest concern):**
- **#91212** (delivery-recovery 0/N after restart): Messages silently lost when recovery fires before channel transports (WebSocket) reconnect. Artificially-incremented retryCount persists across restarts. **No fix PR yet.**
- **#91283** (minSecurity inverted): `minSecurity()` function ranks `full` as most restrictive (rank 2) instead of least restrictive. Security="full" session override gets clamped to "allowlist" by agent config. **No fix PR yet.**

### Moderate (P2, Silver/Gold Shrimp or Platinum Hermit)

| Issue | Title | Fix PR? |
|---|---|---|
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Session/transcript SQLite migration tracking | No fix PR yet |
| [#87136](https://github.com/openclaw/openclaw/issues/87136) | Compaction absolute token thresholds break across model context windows | No fix PR yet |
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | Pre-compaction memory flush needs bounded append semantics | No fix PR yet |
| [#57326](https://github.com/openclaw/openclaw/issues/57326) | Telegram streaming intermediate text blocks silently lost | No fix PR yet |

---

## Feature Requests & Roadmap Signals

### Strong Community Signal (high reaction count or detailed proposals)

1. **[#86881](https://github.com/openclaw/openclaw/issues/86881) — Gateway-lite mode without an AI harness** (7 comments, filed 2026-05-26): Request for a lightweight deployment mode for deterministic channel gateways, webhooks, and cron — without loading the AI harness. **Likely candidate for next release** given the growing ecosystem of non-AI gateway use cases and cron pressure.

2. **[#90916](https://github.com/openclaw/openclaw/issues/90916) — Topic-session families for one assistant across multiple named context lanes** (7 comments, filed 2026-06-06): Explicit topic isolation within a single assistant persona, with shared durable memory. This addresses a common deployment pattern where agents need to maintain separate conversations (e.g., "work" vs "personal" for a personal assistant). **Moderate candidate** for next release; bears similarity to ongoing subagent work.

3. **[#90354](https://github.com/openclaw/openclaw/issues/90354) — Bounded/validated append semantics for pre-compaction memory flush** (5 comments): Hard guardrails for memory append size and validation. **Likely candidate** given the concurrent compaction reliability work (#90639, #87136).

4. **[#45501](https://github.com/openclaw/openclaw/issues/45501) — Configurable `session.resetPrompt`** (6 comments, stale): Users want to customize the hardcoded startup message that runs after `/new` or `/reset`. **Low probability** of inclusion in next release given current focus on stability.

5. **[#40001](https://github.com/openclaw/openclaw/issues/40001) — Write tool append mode** (11 comments, diamond lobster): Isolated cron sessions destroy shared files by overwriting. **High probability** — linked PR exists (`clawsweeper:linked-pr-open`), and the issue is impacting production users.

### Noteworthy PRs that signal roadmap direction

- **[#90101](https://github.com/openclaw/openclaw/pull/90101) — `feat: add runtime self context config and tool`** (XL, `feature: showcase`): Implements config-backed Runtime Self Context for runtime/offload/scale/cost-awareness. This is a significant architectural addition.
- **[#89712](https://github.com/openclaw/openclaw/pull/89712) — `feat(cron): support command jobs`** (XL, `feature: showcase`): Allows scheduled shell-style cron work without going through an agent/model run, reducing cost and fragility.

---

## User Feedback Summary

**Pain Points consistently reported across multiple issues:**

1. **Message Leakage** (#25592, #87326, #38603): Intermediate agent processing text escaping into final channel output is the most-commented issue. Users want tight control over what the agent broadcasts and when.

2. **State Contamination on Restart** (#90991, #91212, #91283): Multiple reports of state corruption or loss following gateway restarts — cron state bleeding across sessions, delivery recovery timing out, security configuration inversion. This suggests the runtime's lifecycle management has systemic gaps.

3. **Regression Velocity** (#88312, #31583, #73802, #68113): At least four P1 regressions are tracked concurrently. The community is expressing concern ("worked before, now fails" pattern) that the pace of feature development may be outpacing regression coverage.

4. **Security Configuration Confusion** (#91283, #29736, #38622): The `minSecurity` inversion bug (filed today) is notable because it represents a **silent downgrade of security posture** — users who configure `security="full"` are unknowingly getting `allowlist` behavior. Combined with exec-approvals path issues and symlink injection failures, security trust is flagged as degraded.

5. **Cron and Session Isolation** (#40001, #90991): Production users with cron-heavy deployments are reporting data loss (shared file overwrites) and state contamination across scheduled jobs. The "write tool lacks append mode" issue (#40001) now has 11 comments and is diamond-lobster rated.

**Satisfaction signals:**
- Positive reactions on PRs addressing performance (#91081 — NFS READDIR caching) and Localization (#90611 — i18n expansion) suggest the community values both operational efficiency and internationalization.
- The "feature showcase" PRs (#90101, #89712) are receiving constructive review engagement, indicating the community is invested in the architectural direction.

---

## Backlog Watch

### Long-unanswered Issues Needing Maintainer Attention

| Issue | Age | Title | Last Updated | Needs |
|---|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 104 days | Text between tool calls leaks to messaging channels | 2026-06-07 | Product decision, security review, maintainer review |
| [#22358](https://github.com/openclaw/openclaw/issues/22358) | 108 days | Post-subagent completion extension hook | 2026-06-07 | Product decision, security review, maintainer review |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 101 days | Bootstrap files in agentDir silently ignored | 2026-06-07 | Product decision, security review, maintainer review |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | 98 days | `exec` tool env variable inheritance | 2026-06-07 | Product decision, security review |
| [#37634](https://github.com/openclaw/openclaw/issues/37634) | 95 days | sandbox workspaceAccess "none" — workspace mounted read-only | 2026-06-07 | Product decision, security review, maintainer review |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | 92 days | Write tool lacks append mode | 2026-06-07 | Product decision (linked PR open) |

### Long-open PRs Needing Maintainer Look

| PR | Age | Title | Status |
|---|---|---|---|
| [#72984](https://github.com/openclaw/openclaw/pull/72984) | 43 days | fix(subagent): resolve runtime model from subagent default instead of parent primary | Needs maintainer look; waiting on proof |
| [#78441](https://github.com/openclaw/openclaw/pull/78441) | 33 days | feat(subagents): forward toolsAllow from sessions_spawn | Ready for maintainer look (P2) |
| [#58823](https://github.com/openclaw/openclaw/pull/58823) | 68 days | fix(agents): restore global subagent model default priority | Ready for maintainer look (P2) |

**Notable:** The oldest open issue with significant community engagement is **#25592** (104 days, 27 comments), which remains blocked on `needs-product-decision` and `needs-security-review`. This is the most-commented issue across the entire repo and has been open since late February 2026 — a concerning duration for a `P1, diamond lobster` rated issue impacting all users.

---

*Data sourced from openclaw/openclaw GitHub repository, snapshot captured 2026-06-08.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-06-08

## 1. Ecosystem Overview

The personal AI assistant/agent open-source ecosystem is experiencing intense development, with multiple projects shipping daily bug fixes while advancing major architectural overhauls (IronClaw Reborn, ZeroClaw v0.8). Activity is concentrated on **reliability hardening** — session state contamination, message delivery integrity, and security configuration bugs are the most common themes across all repositories. A clear second wave is **multi-agent interoperability**, led by Hermes Agent’s A2A protocol implementation and ZeroClaw’s multi-agent routing requests. Community health is generally strong, but several projects (LobsterAI, CoPaw) show unhealthy backlogs of stale issues, indicating triage capacity gaps. The core OpenClaw project remains the ecosystem’s reference implementation, but its sheer throughput (295 issues, 500 PRs/day) creates regressions that spill into downstream forks.

---

## 2. Activity Comparison (24h to 2026-06-08)

| Project | Issues Updated | PRs Updated | New Release? | Est. Health (1–10) | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 295 (115 closed) | 500 (166 merged) | No | 7 | Very high throughput; P1 regressions + security bugs; 27-comment issue open 104d |
| **NanoBot** | 8 (2 closed) | 19 (4 merged) | No | 8 | Healthy; sandbox + MCP security fixes; low stale backlog |
| **Hermes Agent** | 50 (17 closed) | 50 (12 merged) | No | 8 | High activity; A2A protocol cluster; P1 Matrix bug open 27d |
| **PicoClaw** | 21 (17 closed) | 21 (12 merged) | **Yes** (nightly) | 7 | Systematic error-handling hardening; nightly build risky |
| **NanoClaw** | 2 issues new | 9 (3 merged) | No | 6 | Moderate; security issue (#2711) unpatched; 2-month-old Telegram PR stale |
| **IronClaw** | 50 (8 closed) | 38 (16 merged) | No | 7 | Intense Reborn refactor; 0 new bugs; architectural backlog |
| **LobsterAI** | 15 (0 closed) | 2 (2 merged) | No | 5 | High stale ratio (14/15 issues >60d old); no maintainer response |
| **Moltis** | 1 open issue | 3 (0 merged) | No | 5 | Low activity; mobile UX request unanswered |
| **CoPaw** | 18 (6 closed) | 8 (3 merged) | No | 6 | Enterprise channel bugs; critical config crash fix in review |
| **ZeroClaw** | 50 (18 closed) | 50 (12 merged) | No (v0.8 branch) | 7 | High activity; web dashboard finally fixed; multi-agent routing strong demand |
| **NullClaw** | 0 | 0 | No | 2 | Inactive |
| **TinyClaw** | 0 | 0 | No | 2 | Inactive |
| **ZeptoClaw** | 0 | 0 | No | 2 | Inactive |

*Health score based on: closure rate, regression severity, backlog staleness, security posture, and community engagement.*

---

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Largest community and raw contribution volume** — 295 issues and 500 PRs/day dwarfs all others (Hermes: 50/50, ZeroClaw: 50/50). This creates both faster bug discovery and faster fix rotation, but also higher regression velocity.
- **Feature breadth** — cross-provider session replay, multi-channel gateway, skill system, subagent spawning, compaction, dreaming subsystem. No other project matches this surface area.
- **Reference implementation status** — several projects (NanoBot, PicoClaw, CoPaw) explicitly inherit from or reimplement OpenClaw patterns, making it the de facto standard for the ecosystem.

**Technical approach differences:**
- **Modular monorepo** vs. smaller projects’ focused scopes (e.g., NanoBot: simplified agent; PicoClaw: Go reimplementation; IronClaw: Rust Reborn).
- **High abstraction layers** — uses abstract accessor seams for SQLite migration, polymorphic providers, and plugin-like skills. This increases configurability but also complexity.
- **Security posture lagging** — three P1 security issues currently open (#91283, #31583, #25592) with no fix PRs, whereas NanoBot and Hermes close similar issues faster.

**Community size comparison:**
OpenClaw’s comment counts (e.g., #25592: 27 comments) indicate 5–10× more active participants per issue than Hermes or ZeroClaw typically see. The ecosystem’s “center of gravity” is clearly OpenClaw, but frustration with regression velocity is evident (user: “worked before, now fails”).

---

## 4. Shared Technical Focus Areas

| Common Need | Projects Affected | Details |
|---|---|---|
| **Message leakage / internal state exposure** | OpenClaw, NanoBot, Hermes, PicoClaw, LobsterAI | Tool-call narration, streaming artifacts, reasoning content leaking to channels. OpenClaw’s #25592 (27 comments) is the ecosystem’s top pain point. |
| **Session reliability (state loss, contamination, restart)** | OpenClaw, Hermes, PicoClaw, CoPaw, ZeroClaw | Cron noise, delivery recovery after restart, compaction truncation. OpenClaw #90991 (cron contaminates global state) and ZeroClaw #4627 (file_write silent failure). |
| **Security hardening (sandbox, access control, CVEs)** | OpenClaw, NanoBot, Hermes, PicoClaw, NanoClaw | Bubblewrap fragility (NanoBot #4236), `exec` env inheritance (OpenClaw #31583), `minSecurity` inversion (OpenClaw #91283), `create_agent` ungated (NanoClaw #2711), pinned CVEs (Hermes #40176). |
| **Platform parity (Telegram, Matrix, WeCom, Feishu)** | OpenClaw, NanoBot, Hermes, PicoClaw, CoPaw, ZeroClaw | Matrix 2-person room misclass (Hermes P1), Telegram reply-as-mention (PicoClaw #2975), Feishu topic group (NanoBot), WeCom plugin discovery (CoPaw #4585). |
| **Multi-agent / inter-agent communication** | OpenClaw, Hermes, ZeroClaw, IronClaw | Hermes leads with A2A (#514 → #41711); ZeroClaw has 9👍 on #2767; OpenClaw has subagent but no A2A; IronClaw Reborn adds capability dispatch. |
| **Memory & compaction improvements** | OpenClaw, NanoBot, LobsterAI, ZeroClaw | Compaction preserving active task (IronClaw #4534), dream cursor advancing when disabled (NanoBot #4242), absolute token thresholds (OpenClaw #87136). |
| **UI/UX polish (version display, ANSI rendering, mobile)** | NanoBot, PicoClaw, Moltis, ZeroClaw | Version in WebUI (NanoBot #4233), ANSI output rendering (NanoBot #4240), mobile multiline input (Moltis #1107), color-depth fallback (ZeroClaw #7249). |
| **Cost / token efficiency** | LobsterAI, ZeroClaw, OpenClaw | Repeated text waste (LobsterAI #2121), skill compilation to minimize tokens (ZeroClaw #5146), cron command jobs without LLM (OpenClaw #89712). |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | PicoClaw | IronClaw | LobsterAI | CoPaw | ZeroClaw |
|---|---|---|---|---|---|---|---|---|
| **Primary language** | TypeScript/Node | TypeScript/Node | Python | Go | Rust | TypeScript | Python | TypeScript/Node |
| **Target user** | Core devs, large deployments | Lightweight personal assistant | Multi-agent teams | Embedded/Linux sysadmins | Enterprise (Reborn) | Chinese enterprise (POPO, QQ) | Enterprise (WeCom), Qwen models | TUI-focused power users |
| **Architecture** | Monorepo, plugin skills | Simpler core + MCP | Plugin + A2A adapter | Fork of OpenClaw patterns | Reborn: Rust + capability system | Fork/derivative of OpenClaw | Fork of OpenClaw? (Qwen based) | Monorepo with TUI `zerocode` |
| **Key differentiator** | Broadest feature set, reference impl | Fast bugfix cycle, sandbox hardening | First A2A open-source bridge | Systematic Go hardening, Kagi + Termux | Complete rewrite with product workflow | Token waste visibility | WeCom/Qwen integration, plugin infra | Live model switching, outbound queue |
| **Security posture** | Laggard (3 P1 open) | Strong (swift fix for sandbox) | Moderate (CVE backlog) | Strong (many error checks merged) | Strong (approval leases, containment) | Weak (no response to old bugs) | Moderate (Yuanbao bugs fixed) | Strong (token revocation, many closures) |
| **Community engagement** | Very high (27-comment threads) | High (contributor-driven) | High (A2A discussion) | Moderate (Termux guide well-received) | Moderate (team-internal? few user bugs) | Low (14 stale issues) | Moderate (enterprise user reports) | High (logo design, feature votes) |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid iteration (multiple merges/day, active issue triage):**
- **OpenClaw** — 166 merged PRs in 24h; highest velocity but also highest regression rate. Stabilizing? No — still adding large features (Runtime Self Context, cron command jobs).
- **Hermes Agent** — 12 merged PRs; A2A consolidation signals maturation of that feature line. Platform bugs (Matrix) need resolution.
- **ZeroClaw** — 12 merged PRs; v0.8 branch suggests impending release. Web dashboard fix signals maturation.
- **IronClaw** — 16 merged PRs; still deep in Reborn refactor — not yet stabilizing, but architectural foundation solidifying.

**Tier 2 — Steady development (2–4 merges/day, periodic spikes):**
- **NanoBot** — 4 merged PRs; healthy small-team pace. Sandbox and MCP focus indicates stability-oriented iteration.
- **PicoClaw** — 12 merged PRs (one-time spike from systematic error hardening). Nightly builds indicate unstable but evolving.
- **CoPaw** — 3 merged PRs; fixing enterprise channel bugs. Slow but responsible.

**Tier 3 — Low activity / fragile health:**
- **NanoClaw** — 3 merged PRs; security issue unaddressed; Telegram PR stale 2+ months. Risk of contributor burnout.
- **LobsterAI** — 2 merged PRs; 14 out of 15 updated issues are >60d stale with no maintainer comment. Community trust eroding.
- **Moltis** — 0 merges; single feature request unanswered. Project may be in maintenance mode.

**Tier 4 — Inactive:**
- **NullClaw**, **TinyClaw**, **ZeptoClaw** — no commits, issues, or PRs in 24h. Likely dormant or abandoned.

---

## 7. Trend Signals — Value for AI Agent Developers

1. **Security is becoming a competitive differentiator.** Projects that fix sandbox escapes, CVEs, and access-control bugs fast (NanoBot, PicoClaw, IronClaw) are gaining community trust. OpenClaw’s P1 security stagnation is a red flag for deployment at scale.

2. **Multi-agent coordination is the next frontier.** The A2A protocol (Hermes), multi-agent routing (ZeroClaw #2767), and subagent spawning (OpenClaw, NanoBot) are converging. Developers should plan for inter-agent messaging standards — Hermes’ plugin approach (no core edits) is a model for modular extension.

3. **Enterprise messaging channel reliability is underinvested.** WeCom, Feishu, Matrix, Telegram — every project has platform-specific bugs that block adoption in corporate environments. CoPaw’s WeCom plugin discovery issue (#4585) and Hermes’ Matrix P1 are typical. Expect a wave of channel adapter stabilization in Q3 2026.

4. **Token cost visibility is rising.** Users are demanding to know what the agent is doing and spending. LobsterAI’s #2121 (repeated text wasting tokens) and ZeroClaw’s #5146 (skill compilation to reduce tokens) signal a shift from “does it work?” to “is it economical?”

5. **Mobile UX is the next usability battleground.** Moltis #1107 (multiline input) and NanoBot #4233 (version display) are small but indicate that mobile web interfaces are becoming primary consumption paths. Desktop-first projects (OpenClaw, ZeroClaw’s TUI) will need mobile parity.

6. **Rust and Go are gaining ground as performance differentiators.** IronClaw (Rust Reborn) and PicoClaw (Go) are alternative implementations that target lower latency and better resource isolation. Developers evaluating new projects should consider the runtime’s operational overhead — Node/TypeScript remains dominant but may not suit all deployment scenarios.

7. **Compaction and memory management are maturing.** OpenClaw’s dreaming subsystem, IronClaw’s pluggable compaction strategies, and NanoBot’s microcompact gate all indicate the ecosystem is moving beyond simple context-window truncation toward intelligent retention. Expect session-aware, configurable memory policies to become table stakes.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

**NanoBot Project Digest – 2026-06-08**

---

## 1. Today’s Overview

The NanoBot project saw high activity in the last 24 hours, with **8 issues updated** (6 open, 2 closed) and **19 pull requests updated** (15 open, 4 merged/closed). No new releases were published. Community contributions focused heavily on sandbox reliability, MCP security hardening, and WebUI enhancements. Several critical bugs related to the Bubblewrap sandbox were reported and quickly addressed with corresponding fix PRs. The project remains in a healthy development cycle with a steady stream of quality-of-life improvements and stability fixes.

---

## 2. Releases

*No new releases in the last 24 hours.*

---

## 3. Project Progress – Merged/Closed PRs Today

Four PRs were merged or closed today, advancing features and fixing bugs:

- **[#4240 – feat(webui): render ANSI output in code blocks](https://github.com/HKUDS/nanobot/pull/4240)**  
  Merged. Adds ANSI SGR parsing to the WebUI code block shell, supporting colors, bold, italic, underline, and more. Copying output strips control sequences.

- **[#4227 – fix: preserve empty-string reasoning_content instead of coercing to None](https://github.com/HKUDS/nanobot/pull/4227)**  
  Merged. Fixes a bug where custom providers (e.g., DeepSeek, Kimi) sending `reasoning_content=""` had the empty string converted to `None`, breaking downstream field handling.

- **[#2885 – fix(feishu): resolve mentions data and ensure access token initialization](https://github.com/HKUDS/nanobot/pull/2885)**  
  Merged (date listed as 2026-06-07). Improves Feishu channel by resolving `@_user_n` placeholders to actual user info and ensuring bot access token initialization for group messages.

- **[#2663 – fix(whatsapp): handle LID group mentions](https://github.com/HKUDS/nanobot/pull/2663)**  
  Merged. Fixes WhatsApp group mention detection for LID JIDs and treats swipe replies as bot‑directed when group policy is `mention`.

---

## 4. Community Hot Topics

The most active discussions centered on platform‑specific issues and a critical session management bug:

- **[Issue #2256 – Feishu topic group bot reply (CLOSED, 4 comments)](https://github.com/HKUDS/nanobot/issues/2256)**  
  A feature request that bot replies in topic groups should be posted within the same thread rather than the main channel. Resolved after community discussion.

- **[Issue #4203 – Bug: `find_legal_message_start` drops all messages when orphan tool results follow user message (OPEN, 2 comments)](https://github.com/HKUDS/nanobot/issues/4203)**  
  A logic flaw in session trimming that can silently discard entire message sequences. The fix is already proposed in **PR #4219**.

- **[Issue #4242 – Disabling dream.enabled still injects all chat history into system prompt (OPEN, 0 comments)](https://github.com/HKUDS/nanobot/issues/4242)**  
  A subtle design issue where the dream cursor never advances when disabled, causing unbounded history injection. Likely to attract maintainer attention soon.

- **[PR #4206 – feat(dingtalk): add group_allow_from for group chat allowlist (OPEN)](https://github.com/HKUDS/nanobot/pull/4206)**  
  A new feature to restrict DingTalk group messages by allowlist, with wildcard support. Received no comments yet but is a targeted improvement.

*Underlying needs:* Users require cleaner platform integration (Feishu topics, DingTalk allowlists), reliable session management (tool result handling), and proper handling of disabled features (dream cursor).

---

## 5. Bugs & Stability

Three new bugs were reported today (ranked by severity), all with associated fix PRs:

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **Critical** | [#4236](https://github.com/HKUDS/nanobot/issues/4236) | **bwrap sandbox fails on Ubuntu 24.04** due to restricted user namespaces. Commands abort silently. | No PR yet (reported today) |
| **High** | [#4237](https://github.com/HKUDS/nanobot/issues/4237) | **bwrap sandbox does not reset `HOME` environment variable**, causing tool writes to target the hidden host home. | [#4239](https://github.com/HKUDS/nanobot/pull/4239) (open, proposed fix) |
| **Medium** | [#4242](https://github.com/HKUDS/nanobot/issues/4242) | **Dream system injects all chat history into system prompt when `dream.enabled=false`** because the cursor never advances. | No PR yet |
| **Low** | [#4105](https://github.com/HKUDS/nanobot/issues/4105) | **Custom provider drops empty-string `reasoning_content`** – already fixed in [#4227](#4227) (closed today). | Merged |

Additionally, **PR #4234** (fix(api): remove empty-response retry that duplicates user turns) and **PR #4238** (Gate microcompact by context pressure) are open and address stability concerns in API handling and memory management.

A broader theme is the Bubblewrap sandbox being fragile across Linux distributions. The community is actively patching it.

---

## 6. Feature Requests & Roadmap Signals

Several feature requests indicate community direction for upcoming releases:

| Issue/PR | Request | Status | Likely in Next Version |
|----------|---------|--------|------------------------|
| [#4233](https://github.com/HKUDS/nanobot/issues/4233) | Show NanoBot version in WebUI | Open; PR [#4235](https://github.com/HKUDS/nanobot/pull/4235) implements it | Yes |
| [#4231](https://github.com/HKUDS/nanobot/issues/4231) | Add model parameter to `spawn` tool for subagent override | Open, enhancement | Possibly |
| [#4232](https://github.com/HKUDS/nanobot/pull/4232) | Shared voice input support (transcription) | Open PR | Possibly |
| [#4206](https://github.com/HKUDS/nanobot/pull/4206) | DingTalk group allowlist | Open PR | Yes |
| [#2256](https://github.com/HKUDS/nanobot/issues/2256) | Feishu topic group bot reply (CLOSED) | Already resolved | Already merged? |
| [#4240](https://github.com/HKUDS/nanobot/pull/4240) | ANSI rendering in WebUI (MERGED) | In current | Yes |

Predictions: The next release will likely include version display, ANSI rendering, DingTalk allowlist, and the bwrap `HOME` fix. The subagent model override and shared voice input may follow in a subsequent release.

---

## 7. User Feedback Summary

Real user pain points and satisfaction signals extracted from the data:

- **Sandbox configuration is a pain point**: Two reports on Ubuntu 24.04 and `HOME` variable highlight friction when deploying in modern Linux environments. Users are proactively submitting fixes.
- **Custom provider integration still rough**: Empty-string reasoning content was silently broken; the community fixed it swiftly. Users appreciate the attention to edge cases.
- **Platform parity matters**: Feishu topic group reply and WhatsApp LID mention fixes show users need consistent behavior across chat platforms. The DingTalk allowlist feature also addresses a common need.
- **Minor UI niceties desired**: Request for version display in WebUI (#4233) and ANSI output rendering (#4240) indicate users value visibility and polish.
- **Session management reliability**: Bug #4203 (lost messages) would have been a major source of confusion; its quick fix (PR #4219) shows responsive development.

Overall, users are actively engaged, reporting bugs, and contributing fixes. The project’s openness to community patches (e.g., #4235, #4239) fosters a positive contributor experience.

---

## 8. Backlog Watch

No issues or PRs appear stale beyond a few weeks. However, a few open PRs have been awaiting review for some time:

| Item | Age (from creation) | Last Updated | Notes |
|------|---------------------|--------------|-------|
| [PR #3982](https://github.com/HKUDS/nanobot/pull/3982) – test: add scripted agent runner harness | ~15 days | 2026-06-07 | Foundational testing infrastructure – needs maintainer review |
| [PR #3983](https://github.com/HKUDS/nanobot/pull/3983) – test: cover runner blocked tool-call finish reasons | ~15 days | 2026-06-07 | Companion to #3982, also waiting |
| [PR #4053](https://github.com/HKUDS/nanobot/pull/4053) – fix(tools): keep read-only roots out of write paths | ~10 days | 2026-06-07 | Security hardening, no comments since submission |
| [PR #4119](https://github.com/HKUDS/nanobot/pull/4119) – fix(exec): block relative symlink workspace escapes | ~8 days | 2026-06-07 | Another security fix, pending review |

None of these are critically old, but they represent important testing and security work that would benefit from maintainer attention to avoid rotting. The project’s rapid pace suggests these will be addressed in the coming days.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-08

## Today’s Overview

The project is experiencing high activity: 50 issues and 50 pull requests were updated in the last 24 hours, with 17 issues closed and 12 PRs merged/closed. No new releases were published today. The community is heavily focused on **Agent-to-Agent (A2A) protocol support**, with multiple feature requests, implementations, and documentation efforts converging. Stability bugs — particularly around gateway state management, platform adapter quirks, and dependency CVEs — continue to drive a steady stream of fixes. The overall health is strong, but several high-severity open issues remain, especially around Matrix gateway behavior and Windows compatibility.

## Releases

No new releases today.

## Project Progress

**Merged/closed PRs (12 total)** – notable advancements include:

- **A2A Protocol** – Multiple PRs now merged or closed, consolidating Hermes as the first open‑source framework bridging MCP + ACP + A2A:
  - [#4135](https://github.com/NousResearch/hermes-agent/pull/4135) – Full A2A client/server/orchestration (closes #514)
  - [#11025](https://github.com/NousResearch/hermes-agent/pull/11025) – A2A peer-to-peer communication
  - [#14559](https://github.com/NousResearch/hermes-agent/pull/14559) – A2A microservice adapter (`hermes-bindu`)
  - [#35318](https://github.com/NousResearch/hermes-agent/pull/35318) – Verified v2.6 controller-worker documentation
- **Gateway fixes** – [#40156](https://github.com/NousResearch/hermes-agent/pull/40156) switched Telegram onboarding to `httpx`; multiple gateway crash/stability PRs merged.
- **Core agent improvements** – Conversation compression desync ([#34089](https://github.com/NousResearch/hermes-agent/issues/34089)), KV cache invalidation ([#13631](https://github.com/NousResearch/hermes-agent/issues/13631)), and Kanban DB corruption ([#33169](https://github.com/NousResearch/hermes-agent/issues/33169)) all closed with fixes.

**Closed issues (17 total)** – highlights include resolution of critical bugs: duplicate MCP children, persistent config ignoring, cross-talk cron identity leakage, and the `gpt-5.5` context window.

## Community Hot Topics

| Issue/PR | Type | Comments | Reactions | Description |
|----------|------|----------|-----------|-------------|
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) | [OPEN] Feature | 20 | 👍18 | A2A Protocol Support – top community ask, now with a consolidated implementation PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) |
| [#24114](https://github.com/NousResearch/hermes-agent/issues/24114) | [OPEN] Bug (P1) | 2 | 👍2 | Matrix gateway misclassifies 2-person rooms as DMs, disabling mention gating and auto-threading |
| [#40176](https://github.com/NousResearch/hermes-agent/issues/40176) | [OPEN] Security (P2) | 2 | – | Pinned Python deps with known CVEs (urllib3, python-multipart, etc.) |
| [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) | [OPEN] Bug (P2) | 2 | – | Terminal escape sequences leak into output, cutting first characters |
| [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) | [OPEN] PR | – | – | Consolidated A2A protocol plugin – the main deliverable for the A2A feature cluster |

**Analysis**: The A2A protocol is the dominant theme. Users want Hermes to interoperate with other agent frameworks (OpenClaw, etc.) and run multi‑agent production teams (AI Anime Studio example). The Matrix DM bug is a P1 that blocks group workflows and has been open since May 12 – maintainer attention is needed. The dependency CVE report indicates a pressing need for a security patch release.

## Bugs & Stability

Reported in the last 24h, ranked by severity (P1 highest):

| Issue | Severity | Status | Description | Fix PR? |
|-------|----------|--------|-------------|---------|
| [#24114](https://github.com/NousResearch/hermes-agent/issues/24114) | P1 | **Open** | Matrix gateway misclassifies 2‑person rooms as DMs | No |
| [#41662](https://github.com/NousResearch/hermes-agent/issues/41662) | P2 | **Open** | Windows gateway cron circular dependency + broken `os.kill` – no auto‑recovery | No |
| [#41676](https://github.com/NousResearch/hermes-agent/issues/41676) | P2 | **Open** | macOS `launchctl` fallback gateway not recognized as healthy – repeated restarts | No |
| [#41660](https://github.com/NousResearch/hermes-agent/issues/41660) | P2 | **Open** | WhatsApp send fails with bare phone number (missing JID suffix) | No |
| [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) | P2 | **Open** | Terminal escape sequences leak into response output | No |
| [#40176](https://github.com/NousResearch/hermes-agent/issues/40176) | P2 | **Open** | Multiple pinned Python deps carry known CVEs | No |
| [#40324](https://github.com/NousResearch/hermes-agent/issues/40324) | P2 | **Open** | Webhook subscribe/list shows "platform not enabled" even when connected | No |
| [#39685](https://github.com/NousResearch/hermes-agent/issues/39685) | P3 | **Open** | Xiaomi MiMo vision fast path returns multimodal results – API 400 | No |
| [#41686](https://github.com/NousResearch/hermes-agent/issues/41686) | P3 | **Open** | `terminal_tool.py` crashes with `FileNotFoundError` when worker CWD is missing | No |
| [#41669](https://github.com/NousResearch/hermes-agent/issues/41669) | P3 | **Open** | Unable to attach screenshots/files in Gateway mode (desktop app) | No |

**Note**: Several open PRs directly address related bugs – e.g., [#41716](https://github.com/NousResearch/hermes-agent/pull/41716) (Telegram polling retry), [#41715](https://github.com/NousResearch/hermes-agent/pull/41715) (model/reasoning overrides on topic recovery), [#41714](https://github.com/NousResearch/hermes-agent/pull/41714) (Codex Responses), [#41713](https://github.com/NousResearch/hermes-agent/pull/41713) (terminal shell noise). These are not yet merged.

## Feature Requests & Roadmap Signals

- **A2A Protocol Plugin** – [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) is the flagship feature, consolidating all prior A2A work into a zero‑core‑edit plugin. Expected in next version.
- **Kanban Board Integration in Desktop App** – [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) (P3, open, high demand from multi‑agent workflow users).
- **Auto‑open Preview Attachments** – [#41702](https://github.com/NousResearch/hermes-agent/issues/41702) (P3, open) – assistant messages with `[Preview]` links should open automatically.
- **Render YAML Frontmatter as Table** – [#41701](https://github.com/NousResearch/hermes-agent/issues/41701) (P3, open) – for Obsidian/structured note support.
- **Hover‑reveal Collapsed Sidebars** – [#41670](https://github.com/NousResearch/hermes-agent/pull/41670) (P3, open PR) – desktop UI improvement.

**Prediction**: The next release will almost certainly include the A2A plugin, plus security patches for the reported CVEs. The Kanban integration and frontmatter rendering are strong candidates for the following release.

## User Feedback Summary

**Pain points** (from issues and PRs):
- **Platform‑specific failures**: Windows cron and gateway restarts break workflows; macOS has gateway health‑check issues; WhatsApp bare‑number bug blocks messaging.
- **State management bugs**: Conversation compression desync ([#34089](https://github.com/NousResearch/hermes-agent/issues/34089)), KV cache invalidation ([#13631](https://github.com/NousResearch/hermes-agent/issues/13631)), and cross‑talk cron delivery ([#10769](https://github.com/NousResearch/hermes-agent/issues/10769)) cause data loss and confusion.
- **Dependency and update friction**: Update stalling on macOS ([#38974](https://github.com/NousResearch/hermes-agent/issues/38974)), pinned CVEs.
- **Feature gaps**: Multi‑agent orchestration (A2A), matrix group support, Kanban integration.

**Satisfaction signals**: Many bugs get rapid attention – the close/open ratio today is healthy (17 closed / 50 total). Community members actively contribute fixes (batch salvage PR [#41651](https://github.com/NousResearch/hermes-agent/pull/41651) collects 10 low‑risk fixes). The A2A feature is clearly a high‑value addition that the team is shipping.

## Backlog Watch

Important items that have remained open for some time or lack maintainer response:

| Issue | Created | Status | Notes |
|-------|---------|--------|-------|
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) | 2026-03-06 | **Open** (feature) | Now has a consolidating PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) – may be closed soon |
| [#24114](https://github.com/NousResearch/hermes-agent/issues/24114) | 2026-05-12 | **Open** (bug, P1) | No assignee, no fix PR – Matrix DM misclassification blocks group admins |
| [#6653](https://github.com/NousResearch/hermes-agent/issues/6653) | 2026-04-09 | **Open** (bug, P2) | OpenAI Codex reauthentication loop – still unresolved |
| [#40176](https://github.com/NousResearch/hermes-agent/issues/40176) | 2026-06-05 | **Open** (security) | CVE fixes are straightforward bumps – should be fast to merge |
| [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) | 2026-06-07 | **Open** (feature, P3) | Kanban integration – popular but no implementation yet |

**Recommendation**: Prioritize the P1 Matrix bug ([#24114](https://github.com/NousResearch/hermes-agent/issues/24114)) and the security CVEs ([#40176](https://github.com/NousResearch/hermes-agent/issues/40176)) for the next patch release.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-06-08

## 1. Today’s Overview
The project saw **high activity** over the past 24 hours: 21 issues updated (4 open/active, 17 closed) and 21 pull requests (9 open, 12 merged/closed). A new **nightly build** (v0.2.9-nightly.20260608) was released, signaling ongoing development but cautioning users about potential instability. The flurry of merged PRs – many focused on error handling, type assertion safety, and minor bug fixes – indicates a deliberate push toward code quality and reliability. The community continues to surface both feature requests (e.g., OmniRoute provider) and operational pain points (e.g., Telegram location handling, Matrix `allow_from` parsing).

## 2. Releases
### `nightly` – Nightly Build
- **Version**: `v0.2.9-nightly.20260608.875cf4a2`
- **Changelog**: [Full diff](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **Notes**: Automated nightly build, may be unstable. No breaking changes or migration notes provided.

## 3. Project Progress
**12 pull requests merged or closed today**, reflecting a strong emphasis on defensive coding and edge-case handling:

### Merged / Closed PRs
- **Fix: add ok checks for type assertions** (PR [#3018](https://github.com/sipeed/picoclaw/pull/3018)) – Adds missing `ok` checks in LINE channel, Evolution store, and standalone config parser.
- **Fix: handle os.Getwd() error** (PR [#3042](https://github.com/sipeed/picoclaw/pull/3042)) – Stops silently discarding `Getwd()` errors in Evolution skills recall and drafts.
- **Fix: add ok check for singleflight type assertion** (PR [#3040](https://github.com/sipeed/picoclaw/pull/3040)) – Prevents panic in `runCachedModelProbe`.
- **Fix: check Close() errors** (PRs [#3033](https://github.com/sipeed/picoclaw/pull/3033), [#3034](https://github.com/sipeed/picoclaw/pull/3034), [#3035](https://github.com/sipeed/picoclaw/pull/3035)) – Ensures file close failures are reported after downloads and `io.Copy`.
- **Fix: use canonical Anthropic default model ID** (PR [#3036](https://github.com/sipeed/picoclaw/pull/3036)) – Changes `claude-sonnet-4.6` to `claude-sonnet-4-6` in defaults.
- **Fix(identity): allow_from fallthrough for Matrix user IDs with colon** (PR [#3045](https://github.com/sipeed/picoclaw/pull/3045)) – Fixes #3044.
- **Add native Kagi web search provider** (PR [#3037](https://github.com/sipeed/picoclaw/pull/3037)) – Integrates Kagi Search as a `web_search` provider.
- **Fix(agent): add ok checks for startup info type assertions** (PR [#3046](https://github.com/sipeed/picoclaw/pull/3046))
- **Fix(mcp): reject unknown pre-positional flags in add** (PR [#3048](https://github.com/sipeed/picoclaw/pull/3048))
- **Fix: check strconv.Atoi and json.Unmarshal errors** (PR [#3043](https://github.com/sipeed/picoclaw/pull/3043))
- **Docs: add Android Termux guide** (PR [#2902](https://github.com/sipeed/picoclaw/pull/2902)) – Closes long-standing issue #286.
- **Fix message bus backpressure handling and health visibility** (PR [#2906](https://github.com/sipeed/picoclaw/pull/2906)) – Improves runtime stability.

## 4. Community Hot Topics
The most engaging discussions revolve around **provider integration** and **operational reliability**:

1. **Codex OAuth empty response** – Issue [#2674](https://github.com/sipeed/picoclaw/issues/2674) (8 comments, 4 👍). Users report that when ChatGPT backend streams `response.output_item.done`, assistant replies appear empty. The issue is closed but remains a reference for provider stream handling.

2. **Android Termux guide** – Issue [#286](https://github.com/sipeed/picoclaw/issues/286) (8 comments, 2 👍). A long-requested documentation item, now closed with PR [#2902](https://github.com/sipeed/picoclaw/pull/2902). The community needed a clear upgrade/installation path for Termux.

3. **Feature request for new version release** – Issue [#2952](https://github.com/sipeed/picoclaw/issues/2952) (4 comments). User reports build issues with `exec` commands and QQ channel restarts, implicitly asking for a stable release and better agent.md adherence.

4. **Skill-creator broken** – Issue [#652](https://github.com/sipeed/picoclaw/issues/652) (4 comments). The skill-creator markdown points to a missing script. Closed, but highlights the need for regular skill documentation audits.

5. **Default config seeds invalid Anthropic model ID** – Issue [#2941](https://github.com/sipeed/picoclaw/issues/2941) – Fixed by PR [#3036](https://github.com/sipeed/picoclaw/pull/3036); users encountered HTTP 404 on fresh installs.

## 5. Bugs & Stability
Several bugs reported today, most with corresponding fix PRs:

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | `mcp add` mis-parses global flags into positionals (breaks `http/sse` adds and mis-names stdio servers) | [#3041](https://github.com/sipeed/picoclaw/issues/3041) – Open | [#3048](https://github.com/sipeed/picoclaw/pull/3048) (open) |
| **High** | Telegram channel ignores location messages | [#3049](https://github.com/sipeed/picoclaw/issues/3049) – Open | None yet |
| **High** | `allow_from` fails for Matrix user IDs containing colon | [#3044](https://github.com/sipeed/picoclaw/issues/3044) – Open | [#3045](https://github.com/sipeed/picoclaw/pull/3045) (open) |
| **Medium** | Silent `Close()` errors in file downloads / `io.Copy` | Multiple closed issues (e.g., [#3033](https://github.com/sipeed/picoclaw/issues/3033)) | PRs merged today |
| **Low** | Unchecked type assertions in LINE channel, Evolution store, etc. | Many closed | Merged |

**Overall stability trend**: The project has been systematically hardening error handling, which should reduce silent failures in production.

## 6. Feature Requests & Roadmap Signals
- **OmniRoute provider** – Issue [#2978](https://github.com/sipeed/picoclaw/issues/2978) (open, 1 comment). User requests adding OmniRoute as a provider, with a screenshot showing configuration difficulty. Likely to land in a future minor release given the recent Kagi provider merge.
- **Binary dependency filtering for skills** – PR [#2936](https://github.com/sipeed/picoclaw/pull/2936) (merged). Skills whose required binaries are missing on PATH are now skipped – a stability improvement that may reduce user frustration on low-end devices.
- **Telegram reply-to-bot-as-mention** – PR [#2975](https://github.com/sipeed/picoclaw/pull/2975) (open, stale). Treats Telegram reply as @mention in group chats. Not yet merged but addresses a common usability gap.
- **Update from source / upgrade tutorial** – Issue [#2834](https://github.com/sipeed/picoclaw/issues/2834) (closed). User request for upgrade instructions; partially addressed by the Termux guide.

**Predictions for next stable release (v0.3.0?)**: likely includes Kagi provider, Matrix `allow_from` fix, improved error reporting, and possibly the Termux docs.

## 7. User Feedback Summary
- **Pain Points**:
  - **Empty model responses** with Codex OAuth (#2674) – frustrating for heavy ChatGPT backend users.
  - **Invalid default Anthropic model ID** (#2941) – broke first-use experience.
  - **QQ channel restart loop** (#2952) – required clearing history to fix.
  - **Missing upgrade guides** – especially for Android Termux (#2834, #286) and generic source upgrades.
- **Use Cases**:
  - Running PicoClaw on **Raspberry Pi OS** (ARMv7) (#3049).
  - **Trading bots** – a series of closed issues (#3024-#3032) suggest a new `clawtrade` CLI subproject for exchange connectors and risk management (Binance WebSocket/REST, order book ring buffer, CI/CD pipeline).
- **Satisfaction**: The high number of PRs merging today (12) indicates responsive maintainers. Users appreciate the Kagi integration, Termux guide, and hard fixes.

## 8. Backlog Watch
The following items have been open for a while and may need maintainer attention:

- **Skill-creator audit** – Issue [#652](https://github.com/sipeed/picoclaw/issues/652) (closed only today; previously stale). While marked closed, the underlying need for regular skill documentation checks remains.
- **Stale PRs** – [#2904](https://github.com/sipeed/picoclaw/pull/2904) (agent loop reload stability) and [#2975](https://github.com/sipeed/picoclaw/pull/2975) (Telegram reply-as-mention) have not seen updates in 2+ weeks.
- **OmniRoute provider request** – [#2978](https://github.com/sipeed/picoclaw/issues/2978) – only one comment but no maintainer response yet.
- **Telegram location message missing** – [#3049](https://github.com/sipeed/picoclaw/issues/3049) – filed today, no reply. If the community expects a fix, it should be triaged soon.
- **`mcp add` flag parsing bug** – [#3041](https://github.com/sipeed/picoclaw/issues/3041) – open with a detailed reproduction; a fix PR (#3048) is open but not yet merged.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-08

## Today’s Overview
NanoClaw shows moderate activity over the past 24 hours, with **9 pull requests** receiving updates (3 merged/closed, 6 still open) and **2 new issues** opened. No releases were published. The project is in a healthy development cycle: a mix of bug fixes, documentation improvements, and infrastructure features are moving through review. However, the absence of any closed issues and the presence of a security-related access‑control issue (#2711) suggests maintainers are prioritising PR processing over triage. Community contributions remain strong, with several external authors submitting fixes and features.

## Releases
None in the last 24 hours.

## Project Progress
Three PRs were merged or closed today, advancing the codebase in the following areas:

- **Documentation** – [#2710](https://github.com/nanocoai/nanoclaw/pull/2710) (merged): Adds an “Allowing Prompt Caching” section to `docs/ollama.md`, explaining how to work around slow Claude‑Code‑CLI → Ollama performance by filtering cache‑busting hashes.
- **Upgrade safety** – [#2707](https://github.com/nanocoai/nanoclaw/pull/2707) (merged): Introduces a startup tripwire that refuses to start unless the install has followed a sanctioned upgrade path (`/setup`, `/update-nanoclaw`, `/migrate-nanoclaw`). Raw `git pull` now fails loudly with a self‑healing message, preventing silent breakage.
- **Account rotation (i18n)** – [#2706](https://github.com/nanocoai/nanoclaw/pull/2706) (merged): Fixes account‑rotation logic for Codex/Gemini modes, avoids sending Anthropic notifications to the wrong channels, and adds a SIGTERM → SIGKILL fallback in `killGroup` to prevent lingering processes.

## Community Hot Topics
- **#2711 – `create_agent` MCP tool ungated** (new, 0 comments): The most security‑sensitive issue of the day. `create_agent` is documented as admin‑only but is exposed to every container, allowing any agent container to create new agent groups. This has been present since commit `e83ffbc` (≈ v2.0.64). No fix PR yet, but high visibility.  
  [Issue #2711](https://github.com/nanocoai/nanoclaw/issues/2711)

- **#2312 – CLAUDE.md unconditionally deleted on startup** (2 comments): A long‑standing usability bug causing a permanently dirty working tree after any `git pull`. The file `groups/global/CLAUDE.md` is committed but removed by `migrateGroupsToClaudeLocal()` on every startup. Community discussion is ongoing about whether to keep the file in the repo or move it to a git‑ignored location.  
  [Issue #2312](https://github.com/nanocoai/nanoclaw/issues/2312)

- **#1626 – Telegram topic isolation** (open since April, updated today): A feature skill that adds Telegram topic auto‑registration. No maintainer comments yet; the PR has gathered no reactions but remains open, indicating possible scope/priority uncertainty.  
  [PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626)

## Bugs & Stability
Two bugs were reported or updated today, one of medium severity and one low severity:

- **Medium: #2711 – `create_agent` MCP tool is ungated** – Any container can create agent groups despite documentation claiming admin‑only. This is a privilege‑escalation vector. No fix PR exists yet, but a maintainer response is likely imminent given the severity.  
  [Issue #2711](https://github.com/nanocoai/nanoclaw/issues/2711)

- **Low: #2312 – Dirty working tree due to forced deletion of CLAUDE.md** – Not a crash, but a persistent annoyance for developers and operators pulling the repo. Workaround: use `.gitignore` or a manual reset. A fix would require changing the migration logic or removing the file from version control.  
  [Issue #2312](https://github.com/nanocoai/nanoclaw/issues/2312)

Two open fix PRs also target stability:
- **#2708** – Reaps orphaned agent containers on service stop (setup script fix).  
  [PR #2708](https://github.com/nanocoai/nanoclaw/pull/2708)
- **#2705** – Fixes `use-native-credential-proxy` skill to actually bypass the OneCLI gateway (was silently falling back).  
  [PR #2705](https://github.com/nanocoai/nanoclaw/pull/2705)

## Feature Requests & Roadmap Signals
- **#2709 – DB‑backed env + blocked_hosts for ContainerConfig** (open, submitted today): Adds two DB‑backed JSON columns (`env` and `blocked_hosts`) to container configurations, implementing a previously filed maintainer request (#1867). Likely to be merged soon and may appear in the next minor release.  
  [PR #2709](https://github.com/nanocoai/nanoclaw/pull/2709)

- **#2531 – Fix poll‑loop duplicate text on send_message** (open, updated today): Addresses a user‑visible glitch where duplicate text appears mid‑turn. Though filed as a bug fix, it represents a refinement of the agent conversation flow that many users have implicitly requested.  
  [PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531)

- **#1626 – Telegram topic isolation** (old, still open): Users running multi‑topic Telegram groups have long desired automatic topic isolation. This feature skill is still pending review.

## User Feedback Summary
- **Pain point – Dirty git tree (#2312)**: Operators who pull the repo and restart the service are forced to manually reset the working tree. The issue has received community comments but no clear resolution, indicating frustration with the current development workflow.
- **Pain point – Security boundary (#2711)**: The `create_agent` privilege gap is a clear dissatisfaction with the gap between documentation and reality. Detailed reproduction steps were provided.
- **Satisfaction from merged docs (#2710)**: The Ollama prompt caching documentation was well‑received; the PR follows contribution guidelines and addresses a common complaint about slow inference.
- **Account rotation improvements (#2706)**: Merged fix addresses a Chinese‑language user’s report about account rotation misbehaviour, showing the project listens to international users.

## Backlog Watch
- **#1626 – Telegram topic isolation** (open since 2026-04-04, last updated 2026-06-07): No maintainer comments. This feature skill has waited over two months. Community interest is moderate. A maintainer triage or status update would be beneficial.  
  [PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626)

- **#2312 – CLAUDE.md unconditionally deleted** (open since 2026-05-06, comments: 2): No official response from maintainers. While not a high‑severity bug, the steady stream of duplicate reports could be reduced by a simple decision (remove file from repo or change migration logic). Deserves a maintainer label or comment.  
  [Issue #2312](https://github.com/nanocoai/nanoclaw/issues/2312)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-08

## 1. Today’s Overview
The IronClaw project remains in an intense development phase, with **50 issues updated** (42 open/active, 8 closed) and **38 pull requests updated** (22 open, 16 merged/closed) in the last 24 hours. No new releases were cut today, indicating the team is consolidating the massive “Reborn” architectural overhaul rather than shipping. Activity is concentrated on **WebUI v2 beta features**, **Slack host-beta wiring**, **skill management UI**, and **security hardening** (approval leases, dispatch authority seals, filesystem containment). The pulse is healthy: blockers are being resolved, and multiple feature PRs merged—but a large backlog of architectural issues remains open.

## 2. Releases
**None** — no new versions were published in the last 24 hours.

## 3. Project Progress
Sixteen pull requests were merged or closed today. Highlights include:

- **WebChat v2 thread deletion** ([#4516](https://github.com/nearai/ironclaw/pull/4516)) — added DELETE route scoped to authenticated callers; cross-user IDs return not-found without data leak.
- **Slack host-beta durable stores** ([#4463](https://github.com/nearai/ironclaw/pull/4463)) — wired conversation, outbound, and idempotency state to filesystem-backed stores, with turn-runner wake-up for prompt final replies.
- **Structured model-visible tool observations** ([#4530](https://github.com/nearai/ironclaw/pull/4530)) — supersedes #4526 with cleaner boundary; adds typed `ModelVisibleToolObservation` DTOs under neutral run-profile contract.
- **Skill progressive disclosure** ([#4531](https://github.com/nearai/ironclaw/pull/4531)) — introduced explicit discoverable vs. loaded activation state into Reborn skill context snapshots.
- **Preserve active task during compaction** ([#4534](https://github.com/nearai/ironclaw/pull/4534)) — prevents forced compaction from dropping the latest user boundary; adds pluggable compaction strategies.
- **Feat(slack): wire host-beta durable stores** ([#4463](https://github.com/nearai/ironclaw/pull/4463)) — paired with closed issue [#4488](https://github.com/nearai/ironclaw/issues/4488) that split `ProductWorkflow` into explicit submit/read/subscribe doors.

Other notable merges: CI hermetic local gate ([#3298](https://github.com/nearai/ironclaw/pull/3298)), nightly e2e timeout extension ([#3565](https://github.com/nearai/ironclaw/pull/3565)), and dependency bumps across multiple groups.

**Closed issues of note:** [#3829](https://github.com/nearai/ironclaw/issues/3829) (Google Calendar/Gmail extension-v2 capabilities) and [#4488](https://github.com/nearai/ironclaw/issues/4488) (ProductWorkflow split) were resolved.

## 4. Community Hot Topics
The busiest discussions remain around Reborn architectural foundations:

- **#3280** (7 comments) — “Add ProductWorkflow and InboundTurnService facade” – core shaping of the Reborn product workflow layer. Underlying need: clearly define the boundary between product adapters and host services to enable clean OpenAI-compatible API migration.
- **#3036** (5 comments, 👍1) — “Configuration-as-Code for IronClaw Reborn” – epic for tenant blueprints and use-case harnesses. Community (and core team) expressing strong desire for declarative, schema-driven setup.
- **#3044** (3 comments) – local developer runtime profiles for host workspace/shell – a usability gap for engineers who want `ironclaw run --local`.
- **#3283** (3 comments) – migrating OpenAI-compatible chat and Responses APIs onto Reborn – a critical path to preserve ecosystem compatibility.
- **#3333** (3 comments) – production wiring and missing crates – audit of fake/in-memory seams that need real implementations before Reborn goes live.

These issues all point to the same deep need: **completing the Reborn runtime so it can replace the v1 stack without breaking existing integrations**.

## 5. Bugs & Stability
No new zero-day crashes or regressions were reported today. Stability-related work continues through:

- **Filesystem hardening** – issue [#3956](https://github.com/nearai/ironclaw/issues/3956) tracks `RESOLVE_NO_XDEV` bind-mount containment to block device-crossing traversal; [#3957](https://github.com/nearai/ironclaw/issues/3957) covers third-party hook activation hardening (quarantine surfacing, require-sig by default). Both are deferred but not stalled.
- **NoExposureGuard follow-up** – [#3924](https://github.com/nearai/ironclaw/issues/3924) remains open to improve auditability and coverage boundaries after the initial merge.
- **Configuration scaffolding** – PR [#4517](https://github.com/nearai/ironclaw/pull/4517) seeds a default `config.toml` on first runtime start, reducing misconfiguration risk.

No fix PRs were specifically labeled as bug fixes, but many merged PRs (e.g., credential staging in [#4492](https://github.com/nearai/ironclaw/pull/4492)) directly address stability gaps.

## 6. Feature Requests & Roadmap Signals
Several user-facing features advanced or remain on the roadmap:

- **User-scoped skills settings UI** – PR [#4527](https://github.com/nearai/ironclaw/pull/4527) adds add/edit/delete flows for personal skills. Likely to be part of next release.
- **WebUI session capabilities endpoint** – PR [#4519](https://github.com/nearai/ironclaw/pull/4519) returns authenticated tenant/user capabilities including `isAdmin` flag – essential for role-based UI.
- **Slack allowed-channel picker** – PR [#4532](https://github.com/nearai/ironclaw/pull/4532) merged today, bringing operator-controlled channel filtering to Reborn Slack integration.
- **Outbound delivery preference facade** – PR [#4511](https://github.com/nearai/ironclaw/pull/4511) closed today, adding Phase-1 contracts for user-configurable notification targets.

**Predictions for next release:** The Reborn WebUI beta (tracked in [#3607](https://github.com/nearai/ironclaw/issues/3607)) is the most likely candidate for an alpha cut. Once the composition root ([#3026](https://github.com/nearai/ironclaw/issues/3026)) and no-exposure safeguards ([#3032](https://github.com/nearai/ironclaw/issues/3032)) land, a v0.x release with Reborn turned off-by-default could follow.

## 7. User Feedback Summary
No explicit user comments or survey data were captured in the GitHub dataset. However, the issue track provides indirect signals:

- **Pain point:** Manual configuration of `.env`, JSON, and runtime flags is error-prone – issue [#3036](https://github.com/nearai/ironclaw/issues/3036) directly addresses this with a “Configuration-as-Code” epic.
- **Use case:** Operators want to run IronClaw as a local coding agent with minimal wiring – [#3044](https://github.com/nearai/ironclaw/issues/3044) targets exactly this.
- **Satisfaction:** High engagement on Reborn issues suggests the community (or core team) is invested; the rapid pace of PR closures (16 today) indicates momentum.

No complaints, regressions, or dissatisfaction were recorded in the last 24 hours.

## 8. Backlog Watch
Several high-priority issues have been open for weeks without visible maintainer action:

- **[#3169](https://github.com/nearai/ironclaw/issues/3169)** – “Design process-owned runtime handoff ids for concurrent background fan-out” – Created May 1, suggested P2, last updated June 7 but no assignee or comment from maintainers. Blocks true concurrent capability dispatch.
- **[#3231](https://github.com/nearai/ironclaw/issues/3231)** – “Follow-up architecture deepening after main substrate landing” – Created May 3, intended to be non-blocking but no progress since filing.
- **[#3423](https://github.com/nearai/ironclaw/issues/3423)** – “Add loop input resume and cancellation semantics” – Created May 9, suggested P0, last updated June 7 but no assignee. Critical for deterministic run control.
- **[#3420](https://github.com/nearai/ironclaw/issues/3420)** – “Add Reborn-native capability effect adapter path” – Created May 9, suggested P1, depends on #3090 which is itself open. Could stall the v2 engine integration.

These issues are not abandoned (they receive periodic label/URL updates), but they lack assignees or recent technical discussion. Maintainers should consider triaging them to unblock the Reborn cutover.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-06-08

**Data snapshot (24h to 2026-06-08):** 15 open issues updated (0 closed), 2 PRs merged (0 open), 0 releases.

---

## 1. Today’s Overview

The project shows moderate development activity with two pull requests merged, both addressing backend stability and configuration correctness. Issue tracking remains active but heavily skewed toward staled reports — 14 of the 15 updated issues were created in early April and have gone over two months without resolution. No new releases were published, and the single new issue (#2121) highlights a potential token‑waste concern that may affect user trust. The project’s health is stable in terms of incoming fixes, but the growing backlog of unresolved bugs and feature requests suggests a need for more systematic triage and prioritisation.

---

## 2. Releases

No new releases were recorded in this period.

---

## 3. Project Progress – Merged/Closed Pull Requests

Two pull requests were merged today, both focused on bug fixes and configuration improvements:

- **[PR #2110](https://github.com/netease-youdao/LobsterAI/pull/2110)** – `fix(cowork): guard oversized OpenClaw image payloads`  
  *Author:* liuzhq1986  
  Detects and prevents oversized payloads before sending to the gateway, classifies `1009` gateway failures as message‑size errors, and adds test coverage for payload estimation and error classification.

- **[PR #2117](https://github.com/netease-youdao/LobsterAI/pull/2117)** – `fix(config): preserve deleted provider models after migration`  
  *Author:* liuzhq1986  
  Tracks provider model migration versions to inject default models only once, and ensures user‑deleted provider models survive app restarts. Includes regression tests for all affected providers.

Both PRs are maintenance‑oriented; no new feature work was merged.

---

## 4. Community Hot Topics

The most active issue by comment count is:

- **[#1509](https://github.com/netease-youdao/LobsterAI/issues/1509)** – *skills文件长时间生成阻塞无法感知…* (2 comments, 0 👍)  
  The user reports that skill generation can block indefinitely without any progress indicator or error feedback, and that the same prompt works correctly in another model from OpenClaw. This reflects a **core usability gap** – users need real‑time visibility into long‑running operations.

A newly filed issue is already gaining attention:

- **[#2121](https://github.com/netease-youdao/LobsterAI/issues/2121)** – *对一个现象的疑问（怀疑是bug）* (0 comments, 0 👍, created 2026-06-07)  
  The user suspects repeated output from the AI is wasting tokens. No maintainer response yet, but the concern about token economy is a high‑sensitivity topic for users.

**Underlying need analysis:** Users are increasingly concerned about **operational visibility** (what the system is doing) and **cost efficiency** (token consumption). These are critical for a production AI assistant.

---

## 5. Bugs & Stability

All 15 updated issues are bugs or stability problems. The most critical ones, ranked by severity:

| Severity | Issue | Description | Impact |
|----------|-------|-------------|--------|
| **High** | [#1509](https://github.com/netease-youdao/LobsterAI/issues/1509) | Skill generation blocks with no feedback; wrong model understanding | Core functionality broken, user stuck |
| **High** | [#1500](https://github.com/netease-youdao/LobsterAI/issues/1500) | Disabled skills remain in `activeSkillIds` and are injected into prompts | Unwanted behaviour, data leakage |
| **High** | [#1516](https://github.com/netease-youdao/LobsterAI/issues/1516) | OAuth token lost if settings panel is closed during polling | Authentication credentials silently vanish |
| **Medium** | [#1502](https://github.com/netease-youdao/LobsterAI/issues/1502) | Skill list changes do not sync to active session until agent switch | Confusing UX, state inconsistency |
| **Medium** | [#1504](https://github.com/netease-youdao/LobsterAI/issues/1504) | POPO IM bot AES Key missing required validation | Configuration can be saved without required field |
| **Medium** | [#1506](https://github.com/netease-youdao/LobsterAI/issues/1506) | Scheduled task IM notification silently fails when no session selected | Task runs but notifications never delivered |
| **Low** | [#1512](https://github.com/netease-youdao/LobsterAI/issues/1512) | QQ bot group allowlist missing UI input for adding group IDs | Feature unusable via UI |
| **Low** | [#1513](https://github.com/netease-youdao/LobsterAI/issues/1513) | Terms/information page has formatting inconsistencies | Cosmetic but affects user impression |
| **Low** | [#1518](https://github.com/netease-youdao/LobsterAI/issues/1518) | CI labeler workflow fails due to permissions | CI reliability issue, no code fix needed |

The newly reported [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) (repeated output / token waste) is not yet triaged but could be high severity if confirmed.

**Fix PRs exist** for [#2110](https://github.com/netease-youdao/LobsterAI/pull/2110) (payload size) and [#2117](https://github.com/netease-youdao/LobsterAI/pull/2117) (model config), but none of the issues listed above have associated open PRs.

---

## 6. Feature Requests & Roadmap Signals

Several user‑submitted enhancement requests are present in the updated issue list, all created by `MaoQianTu` on April 7 and still open. They indicate a clear desire for **session management and productivity features**:

| Issue | Request | Likely Priority |
|-------|---------|-----------------|
| [#1525](https://github.com/netease-youdao/LobsterAI/issues/1525) | Color labels for sessions (visual distinction) | Medium – common UX pattern |
| [#1528](https://github.com/netease-youdao/LobsterAI/issues/1528) | Batch export multiple sessions | Medium – data portability |
| [#1532](https://github.com/netease-youdao/LobsterAI/issues/1532) | Local usage statistics panel | Low – nice to have |
| [#1537](https://github.com/netease-youdao/LobsterAI/issues/1537) | Message bookmark/favourite in long conversations | High – improves recall in deep chats |
| [#1541](https://github.com/netease-youdao/LobsterAI/issues/1541) | Session tag classification and filtering | High – scalability for users with many sessions |

**Prediction:** Message bookmarks and tag filtering are likely candidates for the next minor release, as they directly address the “information overload” pain point that appears repeatedly in user feedback.

---

## 7. User Feedback Summary

**Satisfaction drivers:** The two merged PRs improve configuration persistence and prevent silent payload errors, which address technical debt. No new complaints about these areas were filed.

**Dissatisfaction triggers (real user voices):**
- *“Blocking in skill generation – no idea what’s happening”* → [#1509](https://github.com/netease-youdao/LobsterAI/issues/1509)
- *“Disabled skills still called in conversation”* → [#1500](https://github.com/netease-youdao/LobsterAI/issues/1500)
- *“Repeated text eats tokens – is this a bug?”* → [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121)
- *“No way to visually tell sessions apart”* → [#1525](https://github.com/netease-youdao/LobsterAI/issues/1525)
- *“Batch mode only deletes, can’t export”* → [#1528](https://github.com/netease-youdao/LobsterAI/issues/1528)

**Common theme:** Users want **transparency** (what is the AI doing, how many tokens are used, where is my data) and **organisational tools** (labels, bookmarks, tags). The project appears to be shifting from a basic chatbot to a productivity tool, but the backlog shows the core interaction model still needs polish.

---

## 8. Backlog Watch

The following issues have been **open and untouched by maintainers since April 7, 2026** – over 60 days without a single comment from the team. They were updated only due to stale‑bot label refreshes:

- [#1509](https://github.com/netease-youdao/LobsterAI/issues/1509) – Skill generation blocking
- [#1500](https://github.com/netease-youdao/LobsterAI/issues/1500) – Disabled skills still active
- [#1502](https://github.com/netease-youdao/LobsterAI/issues/1502) – Skill list sync issue
- [#1504](https://github.com/netease-youdao/LobsterAI/issues/1504) – Missing field validation
- [#1506](https://github.com/netease-youdao/LobsterAI/issues/1506) – Silent IM notification failure
- [#1512](https://github.com/netease-youdao/LobsterAI/issues/1512) – QQ bot allowlist UI missing
- [#1513](https://github.com/netease-youdao/LobsterAI/issues/1513) – Terms page formatting
- [#1516](https://github.com/netease-youdao/LobsterAI/issues/1516) – OAuth token loss
- [#1518](https://github.com/netease-youdao/LobsterAI/issues/1518) – CI labeler fix
- [#1525](https://github.com/netease-youdao/LobsterAI/issues/1525) – Session colour labels
- [#1528](https://github.com/netease-youdao/LobsterAI/issues/1528) – Batch export
- [#1532](https://github.com/netease-youdao/LobsterAI/issues/1532) – Usage statistics
- [#1537](https://github.com/netease-youdao/LobsterAI/issues/1537) – Message bookmarks
- [#1541](https://github.com/netease-youdao/LobsterAI/issues/1541) – Session tags & filtering

**Action needed:** The project maintainers should triage this 14‑issue backlog, assign severity labels, and either close, defer, or assign them for upcoming milestones. The lack of engagement risks frustrating the community and damaging the project’s reputation. The newly filed [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) (token waste) also needs an immediate response to reassure users.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — 2026-06-08

### 1. Today's Overview

Project activity remained moderate over the past 24 hours, with one open issue and three open pull requests receiving updates. No new releases were tagged, and no PRs were merged or closed. The team is focusing on polishing the Telegram integration, capping large tool results during rehydration, and adding granular activity-log visibility controls. The single active issue points to a mobile UI enhancement request, indicating ongoing community interest in improving the web-based chat interface. Overall, Moltis is in a steady development phase with incremental refinements rather than major feature launches.

### 2. Releases

None.

### 3. Project Progress

No PRs were merged or closed in the last 24 hours. The following PRs saw updates and remain open:

- **[#1113 – hotfix(telegram): stream final replies without completion notify](https://github.com/moltis-org/moltis/pull/1113)**  
  Fixes a regression where the Telegram edit-in-place streaming did not treat the final reply as a streamed response when completion notifications were disabled.  
- **[#1089 – Cap persisted tool results before rehydration](https://github.com/moltis-org/moltis/pull/1089)**  
  Adds content size limits for `tool` and `tool_result` messages during session rehydration, applying to normal chat, streaming, retry-after-compaction, prompt inspection, memory turns, and LLM-backed compaction.  
- **[#1093 – Add channel activity log visibility settings](https://github.com/moltis-org/moltis/pull/1093)**  
  Introduces per-account, per-channel, and per-user settings (`all`, `errors_only`, `off`) for activity‑log visibility in channel reply targets, with a priority chain from user overrides to channel overrides to account defaults.

### 4. Community Hot Topics

- **[Issue #1107 – [Feature]: Multiline text input in the mobile web UI](https://github.com/moltis-org/moltis/issues/1107)**  
  The only issue with recent activity; it has 1 comment and 0 upvotes. The author requests the ability to enter multi-line text (e.g., using `Shift+Enter` or a dedicated button) in the mobile web interface, highlighting a real friction point for users who draft longer messages on phones. The underlying need is to improve the mobile chat experience without forcing users to switch to desktop.

All three open PRs have zero comments from the community, suggesting limited public discussion around these internal improvements.

### 5. Bugs & Stability

No new bugs or crashes were reported today. However, **PR #1113** is a hotfix that addresses a behavioral regression in Telegram streaming: when completion notifications were disabled, the final answer was not streamed correctly. This is a moderate-severity bug because it affects the user experience for Telegram users who rely on real-time streaming. The fix is already in review, so the issue should be resolved in an upcoming release.

### 6. Feature Requests & Roadmap Signals

The only user-requested feature this week is **multiline text input in mobile web UI** (Issue #1107). Given that Moltis already supports the mobile web with basic text input, this enhancement would align with improving mobile usability — a common theme in chatbot assistants. The request is straightforward (likely just a key binding or UI toggle) and could appear in a minor release within the next two sprints. No other roadmap signals are visible from today’s data.

### 7. User Feedback Summary

The issue #1107 directly captures a pain point: mobile users cannot easily enter newlines when typing messages. This suggests that while the core Telegram and desktop web experiences are solid, the mobile web UI lags in convenience. No other explicit satisfaction or dissatisfaction signals were recorded in the last 24 hours.

### 8. Backlog Watch

No issues or PRs appear to be languishing unanswered. The oldest open PR (#1089, created June 1) is actively being updated (last update June 7) and is not stale. The longest-standing issue in this snapshot is #1107 (created June 5), which received its last update on June 7 — maintainers have not yet responded with a label or comment. While not critical, a brief maintainer acknowledgment could help set community expectations for the mobile text input request.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-08

## 1. Today's Overview

Project activity remained moderate over the past 24 hours, with **18 issues updated** (12 open, 6 closed) and **8 pull requests updated** (5 open, 3 merged/closed). No new releases were published. The community continues to report bugs related to enterprise messaging channels (WeCom/企业微信) and stability regressions introduced in recent v1.1.9/v1.1.10 releases. On the development side, a new plugin extension infrastructure is under active discussion (PRs #4996–#4998), and several Yuanbao channel bugs have been fixed and merged. The project shows healthy community engagement, though a few long-standing issues (#4585, #4587) remain unresolved.

## Releases

No new releases were published today. The latest version is v1.1.10 (reported in issues).

## Project Progress

Three pull requests were merged/closed today:

- **[PR #4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) (merged)** – *fix(channels): store connectId from AuthBindRsp for connection tracking* – Resolves issue #4978 where missing `connectId` field caused Yuanbao channel connection failures.
- **[PR #4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) (merged)** – *fix(channels): fix Yuanbao streaming replies silently dropped when streaming_enabled=True* – Fixes issue #4979 where streaming responses were lost in the Yuanbao channel.
- **[PR #4996](https://github.com/agentscope-ai/QwenPaw/pull/4996) (closed – WIP)* – Plugin extension infrastructure (Chinese version). Closed as a duplicate of #4997/#4998; the work continues in those open PRs.

Additionally, a fix for the critical config corruption crash (#4970) was proposed in **[PR #5000](https://github.com/agentscope-ai/QwenPaw/pull/5000)** (open) and is under review.

## Community Hot Topics

- **[Issue #4585](https://github.com/agentscope-ai/QwenPaw/issues/4585)** (5 comments, open since May 21) – Self-developed plugin tools not auto-discovered in WeCom channel conversations. This long-standing bug affects enterprise users relying on custom plugins. No fix PR has been linked yet.
- **[Issue #4587](https://github.com/agentscope-ai/QwenPaw/issues/4587)** (5 comments, closed) – Orphaned backend processes on QwenPaw shutdown. While closed, it indicates ongoing process management concerns.
- **[Issue #4970](https://github.com/agentscope-ai/QwenPaw/issues/4970)** (2 comments, open) – Corrupted `loop_config.json`/`prd.json` crashing the entire agent session. The community strongly reacted to this crash, and a fix PR (#5000) is now open.

The underlying need across these topics is **stability and reliability in enterprise/team messaging environments**, especially when custom plugins and persistent sessions are involved.

## Bugs & Stability

**Critical severity:**

- **[#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970)** – Corrupted config files cause complete agent session crash. PR #5000 provides a fix (graceful degradation via `_safe_json_loads`). Under review.
- **[#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988)** – Windows `MAX_PATH` overflow due to duplicated session ID in filenames. Affects Windows users. No fix PR yet.

**High severity (regressions in v1.1.9/1.1.10):**

- **[#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989)** – Local Qwen model (千问3.6-27B) via vLLM: no response after submitting question in 1.1.9/1.1.10. Works in 1.1.5.post2. No fix PR yet.
- **[#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990)** – WeCom channel returns “抱歉，我无法回答你的问题” when tool invocation info is closed.
- **[#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993)** – Image preview jitter when zooming and dragging (macOS).

**Medium severity:**

- **[#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977), [#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978), [#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979), [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976)** (all closed) – Yuanbao channel protobuf compatibility, missing `connectId`, streaming drop, missing proto files. Fixed by merged PRs #4983 and #4982.

## Feature Requests & Roadmap Signals

Several enhancement requests indicate desired future directions:

- **[#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992)** – *Visual Model Fallback*: support a separate vision model when the main model lacks multimodal capabilities. Likely high priority given the rise of text-only models like DeepSeek-V4.
- **[#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994)** – *Memory System Self-Evolution*: user requests hierarchical memory akin to mainstream agent frameworks.
- **[#4999](https://github.com/agentscope-ai/QwenPaw/issues/4999)** – *Session filtering by title*: basic UX improvement for conversation management.
- **[#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986)** – *Real-time shell command feedback*: show live output during execution (references Cursor, WorkBuddy).
- **[#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985)** – *Approval command content wrapping*: fix long command display in approval prompts.

The **plugin extension infrastructure** (PRs #4997, #4998) signals a major upcoming feature: a unified registration mechanism for menus, routes, UI slots, and chat extensions. This could land in the next minor release (possibly v1.2.0).

## User Feedback Summary

User pain points cluster around **enterprise integration** and **stability**:

- **WeCom plugin discovery** (#4585) and error handling (#4990) frustrate users relying on custom tools in workplace chat.
- **Config corruption** (#4970) is a showstopper for ongoing agent sessions.
- **Windows path overflow** (#4988) blocks deployment on Windows.
- **Model regression** (#4989) affects users upgrading QwenPaw while keeping the same local model backend.
- **Missing visual model support** (#4992) limits use with text-only models.
- **Shell command feedback** (#4986) and **command wrapping** (#4985) are UX gaps that reduce confidence when executing dangerous operations.

Overall, users value QwenPaw for its multi-channel support and plugin flexibility, but expect better error handling, backward compatibility, and smoother UX for power users.

## Backlog Watch

Issues that have not received maintainer attention (no linked fix PRs or recent official comments):

- **[Issue #4585](https://github.com/agentscope-ai/QwenPaw/issues/4585)** (created May 21, updated today) – Self-developed plugin tools not auto-discovered in WeCom. No assignee or PR. Urgent for enterprise users.
- **[Issue #4587](https://github.com/agentscope-ai/QwenPaw/issues/4587)** (closed, but root cause may not be fully addressed) – Orphaned backend processes. The closure might indicate a fix was deployed, but the process management story needs follow-up.

These should be prioritized by the maintainers to reduce enterprise user churn.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-08

## Today's Overview
ZeroClaw saw high activity over the last 24 hours, with 50 issues and 50 pull requests updated. Of those, 18 issues were closed and 12 PRs were merged or closed, indicating steady progress on bug fixes and feature work. Development continues across multiple fronts: gateway improvements, web dashboard functionality, provider fallback chains, and memory strategy migration are all in active motion. No new releases were tagged, but a release-prep branch for v0.8.0 was opened.

## Releases
No new releases were published in this period. The project remains at the previous version; the v0.8.0 release branch (PR #7364) suggests a release may be imminent.

## Project Progress
Several notable pull requests were merged or closed today, advancing key subsystems:
- **Gateway token revocation**: PR #7243 (closed) partially fixes token rotation and device deletion security gaps.
- **Theme enhancements**: PR #7249 (closed) adds color-depth fallback, registry-generated presets, per-agent overrides, and palette swatches to the `zerocode` TUI.
- **Outbound message queue**: PR #7190 (closed) replaces the hard input block during turn response with an outbound message queue and sidebar injection, improving real-time UX.
- **Model/provider live switching**: PR #7209 (closed) adds `/model` and `/model-provider` pickers with live switching in the TUI.
- **Per-alias model-provider fallback**: PR #7178 (closed) re-introduces explicit operator-declared fallback chains on failure.
- **Quickstart modal fix**: PR #7360 (merged) fixes sizing and scroll of quickstart modals in `zerocode`.
- **Documentation CI gate**: PR #7365 (open, WIP) sweeps markdown and quickstart generation, with docs CI gating.

Ongoing PRs of interest include per-alias webhook routing (#7367), MCP/Skills/Plugins dashboard tabs (#7229), and memory strategy migration (#7234).

## Community Hot Topics
The most discussed issues remain long-standing feature requests and blockers:
- **Web dashboard unavailability** (Issue #4866, 28 comments, closed) — users report that the web UI and desktop app both prompt to build from source; this has persisted across versions and was finally closed today.
- **Better logo** (Issue #4710, 11 comments, 2 👍) — a community designer submitted alternative logos; the issue remains open with status `blocked` and `needs-author-action`.
- **Token consumption minimization via skill compilation** (Issue #5146, 9 comments, 1 👍) — a high-risk enhancement to avoid sending full skill definitions on every query.
- **Multi-Agent Routing** (Issue #2767, 6 comments, 9 👍) — strong community demand for isolated agents with separate workspaces and multi-channel support.
- **A2A Protocol Support** (Issue #3566, 6 comments, 7 👍) — inter-agent communication using the open Agent2Agent standard.

Top pull requests by development attention: PR #7229 (MCP dashboard, 0 comments but large scope) and PR #7243 (security fix) are among the most actively reviewed.

## Bugs & Stability
Several bugs were reported or addressed:
- **Severity S0 – Data loss / security risk**: Issue #4627 (open) — `file_write` tool silently fails; files written are invisible on the host filesystem. A fix is in progress (`status:in-progress`).
- **Severity S1 – Workflow blocked**: 
  - Issue #4866 (closed) — web dashboard still unavailable; resolved.
  - Issue #4627 also S1 due to data loss.
  - Issue #5803 (closed) — fallback provider chain ignoring config; fixed.
  - Issue #5155 (closed) — delegate agents ignore prompt_injection_mode; fixed.
  - Issue #4879 (open) — Gemini CLI OAuth broken after authentication; under investigation.
- **Severity S2 – Degraded experience**:
  - Issue #4880 (closed) — `context_compression` not triggered in daemon channel mode; fixed.
  - Issue #5122 (closed) — `web_fetch` `allowed_private_hosts` ineffective for domain names resolving to private IPs; fixed.
  - Issue #4848 (closed) — MCP tools not detected; fixed.
- **New bug reports today**: Issue #4873 (Feishu channel calls LLM instead of agent, S3), Issue #4721 (logging to stdout instead of stderr, S3).

Many bug fix PRs shipped today; the overall stability trend is positive with several high-severity items closed.

## Feature Requests & Roadmap Signals
User-requested features gaining traction include:
- **Token consumption minimization** (#5146) — likely candidate for next release, given PR activity around skill compilation and prompt injection modes.
- **A2A Protocol Support** (#3566) — with 7 👍 and a structured proposal, this may appear in v0.8.x.
- **Multi-Agent Routing** (#2767) — heavy demand, but still in accepted state without a dedicated PR yet.
- **Full Docker image** (#3642) — blocked on dependencies; a community docker compose example was submitted.
- **Provider-scoped model fallback chains** (#4647) — PR #7178 addressed the global fallback, but per-provider scoping remains open.
- **bubblewrap sandbox configurability** (#5127) — for writable paths and network access inside sandbox.

The `RFC` tagged issues (#7184 for translation submodule, #6293 for air-gapped mode) indicate architectural discussions that may shape the roadmap.

## User Feedback Summary
- **Pain points**: The web dashboard unavailability (now closed) was a top frustration. MCP tool detection failures (#4848) and Gemini OAuth issues (#4879) are causing adoption friction. The `file_write` data loss bug (#4627) is a serious trust issue for users relying on file operations.
- **Use cases**: Multi-agent setups (WhatsApp, Telegram, QQ) and inter-agent communication dominate. Users want to run multiple isolated agents with separate channel accounts (#2767). There is strong demand for a simple Docker setup for non-technical users (#3642) and for custom webhook paths (#2467).
- **Satisfaction**: Positive feedback on the new outbound message queue (PR #7190) and live model switching (PR #7209). The community is engaged in logo design and documentation improvements.

## Backlog Watch
Long-unanswered issues that still need maintainer attention:
- **Issue #2503** (created 2026-03-02) — "where is napcat channel?" – no official reply or assignment; community wants OneBot/NapCat support.
- **Issue #2467** (created 2026-03-02) — "Webhook transforms" – blocked, with no recent maintainer comment.
- **Issue #3642** (created 2026-03-15) — "Provide a full docker image" – blocked, but a community docker compose example was given (Issue #6760). Maintainer review needed.
- **Issue #3696** (created 2026-03-16) — "Pre/post message hooks for shell commands" – accepted but no PR yet.
- **PR #6490** (created 2026-05-06) — "human-readable integration category labels" – marked `needs-author-action`, stalled for over a month.
- **Issue #6293** (created 2026-05-03) — "Air-gapped execution mode" RFC – has 4 comments, needs maintainer decision.

These items represent known gaps and community pain points that, if addressed, could significantly improve user experience and project credibility.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*