# OpenClaw Ecosystem Digest 2026-06-10

> Issues: 442 | PRs: 488 | Projects covered: 13 | Generated: 2026-06-10 02:43 UTC

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

# OpenClaw Project Digest — 2026-06-10

## 1. Today’s Overview
OpenClaw saw extremely high activity in the last 24 hours: **442 issues** were updated (314 open/active, 128 closed) and **488 PRs** were touched (355 open, 133 merged/closed). Two releases were published — v2026.6.5 (stable) and v2026.6.5-beta.6 — both focused on cleaning up leaked model reasoning content in messaging channels. The community is deeply engaged, with many severe regressions and security-related issues still awaiting maintainer decisions. Despite the volume, the project shows signs of healthy iteration, though several long‑standing P1/P2 bugs remain unresolved.

## 2. Releases
**v2026.6.5** (stable) and **v2026.6.5-beta.6** were released today. Both share the same highlight:

- **QQBot**: Model reasoning/thinking scaffolding (e.g., `<thinking>` tags) is now stripped before native delivery, preventing raw internal content from leaking into channel replies. (#89913, #90132 – thanks @openperf)
- **MCP tool results**: Now coerce `resource_link`, `resource`, `audio`, malformed image, and future non‑standard result types into normalised delivery.

No breaking changes or migration notes are mentioned in the release highlights.

## 3. Project Progress
**133 PRs were merged/closed** today, indicating strong engineering momentum. Key improvements delivered:

- **Codex session stability**: PR #91590 (merged) fixes context‑engine compaction ownership for Codex sessions, keeping the owning context‑engine primary and treating native Codex thread compaction as a bounded secondary step.
- **iMessage channel hardening**: PR #91783 (merged) adds configurable `sendTransport` (auto/bridge/applescript) and stops monitor final replies from reusing the long‑lived watch RPC client. PR #91785 (merged) surfaces inbound startup diagnostics for dropped echo/reflection rows.
- **Cron one‑shot fallback**: PR #91811 (merged) queues a heartbeat request instead of marking one‑shot runs as skipped when heartbeat is disabled.
- **Voice call path tightening**: PR #91784 (merged) fixes a WebSocket routing issue where sibling paths could incorrectly match the realtime voice handler.
- **Stuck session lane recovery**: PR #91801 (merged) resets session lanes when an active embedded/reply run aborts and drains cleanly but the diagnostic session still reports queued work.

Several other fixes (e.g., #89017 for WebChat session reset, #90759 for stale reply after queued messages, #91227 for empty memory database after index swap) are open and await maintainer review.

## 4. Community Hot Topics
The most active discussions highlight three recurring pain points:

1. **Message leakage to channels**  
   - **#25592** (29 comments, 💎 diamond lobster): “Text between tool calls leaks to messaging channels” – internal processing output, error handling, and narration are sent as visible messages. Still open, P1, with security impact.
   - **#44905** (10 comments): Discord leaks internal tool‑call traces (`NO_REPLY`, commentary, raw JSON) to channels. P1, security‑related.
   - **#54531** (10 comments): Agent fails to reply to originating channel (Telegram/Discord/WhatsApp). P1, message‑loss impact.

2. **Session‑state and turn‑completion regressions**  
   - **#88312** (15 comments, 🐚 platinum hermit): Codex app‑server turn‑completion stall returns “Codex stopped before confirming the turn was complete” – a regression of #84076. P1, beta release blocker.
   - **#87307** (14 comments): Matrix thread replies sent as normal replies on 2026.5.22; `/status` and `/model` silent. P1, session‑state and message‑loss impact.
   - **#48003** (12 comments): Steer mode does not inject messages mid‑turn for main sessions. P1, undelivered messages.

3. **Platform‑specific breakage**  
   - **#54253** (13 comments, 4 👍): OpenClaw fails on RISC‑V64 with “LLM Request Failed”. Stale, P2.
   - **#86599** (13 comments, closed): Windows beta – local model calls block gateway event loop, trivial inference takes ~4 minutes. (Was a beta release blocker; now closed.)

These issues indicate that users are struggling with reliability across diverse messaging platforms and runtimes. The project’s priority labelling is consistent, but many P1 issues remain open for months.

## 5. Bugs & Stability
**Critical (P1, impact: session‑state / message‑loss / security):**

- **#88312** – Codex turn‑completion stall (regression). *Fix PR #91590 merged today* – should be resolved in next release.
- **#86508** (8 comments) – `EmbeddedAttemptSessionTakeoverError` during Discord runs: session file changed while embedded prompt lock was released. *Fix PR #91801 merged today*.
- **#89315** (5 comments, 3 👍) – Gateway heap grows unbounded over time, killed by cgroup OOM on long‑running Linux systemd‑user deployments. *No fix PR yet.*
- **#84569** (5 comments, 3 👍) – WhatsApp session stalls on long model_call: incomplete turn with payloads=0, reply never delivered. *No fix PR yet.*
- **#86538** (5 comments) – Session write‑lock timeouts block subagent delivery lanes. *No fix PR yet.*
- **#87299** (6 comments) – Spurious “Something went wrong” and Codex app‑server failures in large Telegram direct sessions. *Waiting for live repro.*
- **#86996** (7 comments) – Active Memory + Codex path causes long latency, hook timeouts, startup aborts, and gateway event‑loop stalls. *No fix PR yet.*

**High (P2, impactful):**

- **#87307** – Matrix thread regression (thread replies broken, `/status` silent). *Still open, needs maintainer info.*
- **#73424** (closed) – “Failed to optimize image” error in VLM pipeline. *Closed stale, likely fixed.*
- **#53628** (13 comments) – `${XDG_CONFIG_HOME}` not expanded when installing a skill. *Stale, P2, linked PR open.*
- **#50442** (6 comments) – `backup create` leaves large `.tmp` files on timeout, causing disk exhaustion. *Stale, P2, fix PR pending.*

**Regressions reported today (as `regression` label):**  
- **#88312** (Codex stall) – fix merged.  
- **#86508** (Discord session takeover) – fix merged.  
- Others: #60546 (microsoft‑foundry provider routes Claude via wrong endpoint, closed), #44599 (OPENCLAW_CONFIG_DIR whitespace, closed), #48920 (live docs ahead of release, open), #52186 (TTS elevenlabs provider plays OpenAI voice instead, open), #53486 (Feishu card JSON regression, open).

Overall stability is improved by the merged fixes, but several critical vulnerabilities (message leaks, OOM, session stalls) remain unaddressed.

## 6. Feature Requests & Roadmap Signals
The top user‑requested features, sorted by potential impact:

1. **Per‑channel / per‑group model override** (#53638, 5 comments, 2 👍) – Requested to avoid manual runtime switches. Likely to be prioritised given the growing multi‑channel usage.
2. **Persistent task‑status surface** (#52640, 7 comments) – For long‑running channel turns (Discord first). Could be combined with heartbeat improvements.
3. **Session labels / nicknames** (#55249, 5 comments) – To distinguish many sessions in listings.
4. **Telegram Inline Query support** (#54794, 5 comments) – `@botname query` in any chat.
5. **Bounded memory flush during pre‑compaction** (#90354, 6 comments) – Guardrails for append size.
6. **Context provenance metadata** (#54373, 6 comments) – To help agents distinguish old vs. new context.
7. **MathJax/LaTeX rendering in Control UI** (#42840, 7 comments, 6 👍) – Strong user demand for scientific communication.
8. **Configurable file permissions** (#56263, 6 comments) – For multi‑user container setups.

From today’s open PRs, we see advanced features being built: **Microsoft Teams voice/video calls** (#91438, XL, P2), **group:core tool group** (#79982, S, P2), and **provider/model/trigger context in overloaded error messages** (#55851, S, P2). These indicate the roadmap is expanding toward enterprise/team use.

**Prediction for next version (v2026.6.x or v2026.7.x):**  
- Per‑channel model override is highly requested and technically feasible.  
- Persistent task status surfaces may appear as an extension of heartbeat improvements.  
- MathJax support could land in the web UI given the PR #91557 (iPad/iPhone control surfaces) improving rendering infrastructure.  
- Context provenance and bounded memory flush are deeper changes that may take longer.

## 7. User Feedback Summary
**Pain points expressed repeatedly:**

- **Message leaks**: Users are unhappy that internal processing, tool calls, and thinking content are visible to channel participants (#25592, #44905, #54531, #39406). This is the most vocal feedback area, affecting Telegram, Discord, and soon Matrix.
- **Session unreliability**: “Codex stopped before confirming the turn,” “session file changed,” “heartbeat‑driven replies stuck” – these create a “bot unresponsive” experience.
- **Regressions**: Users report that features that worked in 2026.5.20 – 2026.5.26 break in later versions (Matrix threads, Feishu cards, Codex completion, TTS provider).
- **Cross‑platform gaps**: RISC‑V64 not supported (#54253), Windows event loop blocking (#86599), whitespace in config paths (#44599).
- **OOM and resource exhaustion**: Long‑running deployments (systemd‑user) face unbounded memory growth (#89315, #50442).

**Positive signals:**
- Users appreciate the fast release cycle and willingness to fix regressions (e.g., QQBot thinking stripping merged quickly).
- The diamond lobster rating (highest severity) is consistently applied, indicating good prioritisation awareness.
- Several users provide detailed steps to reproduce and logs, helping maintainers.

## 8. Backlog Watch
Issues and PRs that are important (P1/P2) but have been stale or waiting for maintainer action for more than two months:

| Issue/PR | Age | Status | Why Stalled |
|----------|-----|--------|-------------|
| **#25592** (P1, security, message‑leak) | Created 2026-02-24 | Needs maintainer review, product decision, security review | 3.5 months open; no fix PR despite high impact |
| **#88312** (P1, regression) | Created 2026-05-30 | Needs live repro | Fix merged, but repro still pending |
| **#87307** (P1, Matrix regression) | Created 2026-05-27 | Needs info | Awaiting user logs/config |
| **#54253** (P2, RISC‑V64) | Created 2026-03-25 | Needs info | Stale, no maintainer response in weeks |
| **#53628** (P2, config variable) | Created 2026-03-24 | Needs maintainer review, linked PR open | 2.5 months, PR awaiting merge |
| **#48003** (P1, steer mode) | Created 2026-03-16 | Linked PR open | 3 months, PR not merged |
| **#56263** (P2, file permissions) | Created 2026-03-28 | Needs security review | Over 2 months, no decision |
| **PR #55851** (provider context in errors) | Created 2026-03-27 | Waiting on author | Author has not responded to review comments |
| **PR #79982** (group:core tools) | Created 2026-05-09 | Waiting on author | 1 month, needs author update |
| **PR #89028** (web_fetch fix) | Created 2026-06-01 | Waiting on author | 9 days, but no update |

These items represent **high‑value work that is stuck** – especially #25592 (message leakage) and #48003 (steer mode) which directly affect user trust and reliability. Community members are watching these closely.

---

## Cross-Ecosystem Comparison

# Cross-Project AI Agent Ecosystem Comparison Report
**Date:** 2026-06-10 | **Analyst:** Senior AI Agent Ecosystem Analyst

---

## 1. Ecosystem Overview

The open-source personal AI assistant and agent landscape is experiencing **unprecedented activity and fragmentation**, with nine actively developing projects tracked in this report. The ecosystem is undergoing a rapid maturation phase where **reliability, security, and cross-platform parity** have emerged as the primary battlegrounds—overtaking raw feature velocity. A clear divide is forming between **reference/benchmark implementations** (OpenClaw), **specialized vertical agents** (Hermes Agent, LobsterAI), and **foundation-building projects** (IronClaw, CoPaw) that are prioritizing architectural overhauls over feature expansion. The community is vocal about three universal pain points: **message leakage and context pollution**, **session state unreliability**, and the **lack of flexible model routing** (per-channel or per-conversation model overrides). Security hardening is accelerating across all projects, driven by both user demand and coordinated vulnerability disclosures—most notably the 11-advisory batch filed against PicoClaw.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score | Primary Activity Pattern |
|---------|---------------------|--------------------|----------------|-------------|------------------------|
| **OpenClaw** | 442 (314 open) | 488 (355 open) | ✅ v2026.6.5 stable + beta | ⚠️ Moderate | High churn; bug-fix heavy with many P1 regressions |
| **IronClaw** | 46 | 50 | 🚫 No release | ✅ Good | Focused epic-driven development (Reborn cutover) |
| **CoPaw** | 39 (19 open) | 34 (19 open) | ✅ v1.1.11-beta.2 | ✅ Good | Feature + migration prep (AgentScope 2.0) |
| **ZeroClaw** | 50 (48 open) | 50 (49 open) | 🚫 No release | ✅ Good | Sustained high-volume development |
| **Hermes Agent** | 50 (46 open) | 50 (44 open) | 🚫 No release | ⚠️ Moderate | Feature-rich but P1 bug resolution slow |
| **NanoBot** | 6 (6 open) | 23 (13 open) | 🚫 No release | ✅ Good | Fast-iteration cleanup sprint |
| **PicoClaw** | 20 | 17 | ✅ Nightly build | ⚠️ Pressured | Reactive security patch cycle |
| **NanoClaw** | — | 44 (40 merged) | 🚫 No release | ✅ Strong | Massive backlog cleanup (40 PRs closed) |
| **NullClaw** | 5 (1 open) | 8 (7 merged) | 🚫 No release | ✅ Strong | Focused bug-fix sprint |
| **LobsterAI** | 2 | 5 (4 merged) | 🚫 No release | ✅ Stable | Targeted feature delivery |
| **TinyClaw** | 0 | 0 | — | 🟢 Inactive | No activity |
| **Moltis** | 0 | 0 | — | 🟢 Inactive | No activity |
| **ZeptoClaw** | 0 | 0 | — | 🟢 Inactive | No activity |

**Health Score Definitions:** *Strong* (fast fix turnaround, low critical bugs), *Good* (active with manageable issues), *Moderate* (high volume but significant unresolved P1s), *Pressured* (security-driven reactive cycle), *Inactive* (no recent activity).

---

## 3. OpenClaw's Position

### Competitive Advantages
- **Scale and maturity:** With 442 issues and 488 PRs in a single day, OpenClaw commands the largest community and highest contribution velocity in the ecosystem—nearly **10x the activity level** of the next busiest project (IronClaw/ZeroClaw at ~50 each).
- **Reference implementation status:** As the core reference (`github.com/openclaw/openclaw`), it sets the standard that other projects (PicoClaw, NanoClaw, NullClaw) explicitly or implicitly fork or emulate.
- **Release discipline:** Two releases published today alone (stable v2026.6.5 + beta), demonstrating mature CI/CD and versioning practices that peers lack (most projects had zero releases).
- **Diamond lobster severity system:** A sophisticated, community-trusted priority framework that enables consistent triage across thousands of issues.

### Technical Approach Differences
- **Architecture:** OpenClaw employs a **context-engine compaction model** with Codex session ownership (PR #91590), whereas peers like NanoBot use simpler memory cursors and IronClaw is building a "Reborn" EventStreamManager. This makes OpenClaw's session management more robust but also more complex to debug.
- **Provider abstraction:** OpenClaw has a mature provider layer with configurable `sendTransport` for iMessage, while ZeroClaw is still unifying provider architectures (#5937) and IronClaw is blocking on strict-mode provider compatibility (#4642).

### Community Size Comparison
| Metric | OpenClaw | Next Largest (IronClaw/ZeroClaw) | Ratios |
|--------|----------|-----------------------------------|--------|
| Daily Issues | 442 | ~48 | **9.2x** |
| Daily PRs | 488 | ~50 | **9.8x** |
| P1 Bugs Open | ~15 | ~4 | **3.7x** |
| Security Advisories | Elevated | Low | Higher surface area |

**Key Insight:** OpenClaw's dominance in activity volume is both an asset and a liability—it attracts the most contributors and bug reports, but also accumulates **the largest backlog of unresolved critical issues** (e.g., message leakage #25592, open for 3.5 months, P1 with security impact).

---

## 4. Shared Technical Focus Areas

Nine cross-project requirements emerging across multiple implementations:

| Requirement | Affected Projects | Specific Need |
|-------------|-------------------|---------------|
| **Model routing flexibility** | OpenClaw (#53638), NanoBot (#4253), CoPaw (#4992), Hermes Agent (#13107) | Per-channel, per-conversation, or per-session model overrides; independent vision model fallback |
| **Message leakage prevention** | OpenClaw (#25592, #44905, #54531), NanoBot (#4259), CoPaw (#5031) | Internal tool traces, thinking content, and cross-session context leaking to users or channels |
| **Context/session reliability** | OpenClaw (#88312, #86508), Hermes Agent (#43083), ZeroClaw (#6034), CoPaw (#5052) | Turn-completion stalls, session takeovers, password redaction breaking tool calls, cron delivery failures |
| **Memory & context management** | OpenClaw (#90354), NanoBot (#4264), ZeroClaw (#5844), CoPaw (#4994, #4937) | Bounded memory flush, idle compaction preserving corrections, context budget handling, self-evolving memory |
| **Cross-platform channel parity** | ZeroClaw (#6378), OpenClaw (#87307), Hermes Agent (#7507), PicoClaw (#3063) | Discord channel restrictions, Matrix reply quoting, DeltaChat gateway, consistent inline button delivery |
| **Security hardening** | PicoClaw (#3068–3078), NullClaw (#944), NanoClaw (#2722), IronClaw (#88) | SSRF bypasses, authorization loopholes, CSPRNG pairing codes, credential redaction |
| **Observability & debugging** | IronClaw (#4632), ZeroClaw (#7385), NanoClaw (#1202), CoPaw (#4057) | Turn metadata OTel spans, agent trace recording, E2E test coverage, external monitoring integration |
| **Deployment flexibility** | NanoClaw (#1285), OpenClaw (#54253), CoPaw (#5047) | Direct runner mode (no Docker), RISC-V64 support, Windows performance fixes |
| **Enterprise/multi-tenant support** | ZeroClaw (#5982), IronClaw (#4628, #4663), OpenClaw (#56263) | Per-sender RBAC, admin-shared tools, project-scoped agent ownership |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | IronClaw | CoPaw | ZeroClaw | NanoBot |
|-----------|----------|--------------|----------|-------|----------|---------|
| **Target user** | Power users, self-hosters | Developers, tool builders | Enterprise, platform teams | Chinese market, local LLM users | General purpose, multi-instance | Fast-iteration enthusiasts |
| **Primary strength** | Reference stability, community lens | Skill ecosystem, Telegram features | Architectural overhaul (Reborn) | Localization, Qwen integration | Configurability, webhooks | Quick fixes, lightweight |
| **Weakness** | Critical bug backlog | P1 fix velocity | Immature production readiness | Windows performance | High complexity overhead | Limited feature depth |
| **Architecture phase** | Mature, iterative fixing | Feature expansion | Core rebuild (Reborn) | Migration (AgentScope 2.0) | Feature + security | Cleanup sprint |
| **Release cadence** | Daily stable + beta | No releases tracked | No releases tracked | Beta releases | No releases tracked | No releases tracked |
| **Provider support** | Broad, mature | Expanding (Volcengine) | Growing (OpenAI-compat) | Qwen-focused | Broad, unifying | Growing (StepFun ASR) |

### Key Strategic Differences

- **OpenClaw** prioritizes **stability through standardization** (the diamond lobster system, reference implementation status) but struggles with execution speed on critical bugs.
- **Hermes Agent** is the most **feature-aggressive** (Telegram guest bots, 15+ new skills in one day), appealing to developers who value extensibility over reliability.
- **IronClaw** is executing a **controlled gambit**—investing heavily in a production cutover (Reborn) that will fundamentally reshape its architecture. Current instability (#4642, #4548) is tolerated for long-term gain.
- **CoPaw** owns the **Chinese-AI-first** niche with strong Qwen model integration and local LLM support, but desktop performance regressions risk alienating its core user base.
- **NanoBot** and **NullClaw** are **lightweight, reactive** projects that fix bugs within hours of reporting but lack the feature depth of larger peers.

---

## 6. Community Momentum & Maturity

### Activity Tier Matrix

| Tier | Projects | Daily PR Velocity | Maturity Signal | Risk Profile |
|------|----------|-------------------|-----------------|--------------|
| **Tier 1: Hyperactive** | OpenClaw, IronClaw, ZeroClaw, CoPaw | 34–488 PRs | High-volume bug reporting; architectural overhauls in progress | Burnout risk; technical debt accumulation |
| **Tier 2: High-Activity** | Hermes Agent, PicoClaw, NanoClaw | 17–50 PRs | Feature expansion + security response | Security-driven reactive cycles (PicoClaw) |
| **Tier 3: Stable Iteration** | NanoBot, NullClaw, LobsterAI | 5–23 PRs | Fast fix turnaround; low critical bug count | Limited feature velocity may miss market shifts |
| **Tier 4: Inactive** | TinyClaw, Moltis, ZeptoClaw | 0 PRs | No community engagement | Likely abandoned or on extended hiatus |

### Maturity Trajectories

- **Rapidly iterating (high risk, high reward):** OpenClaw, IronClaw, ZeroClaw, CoPaw—all pushing significant architectural changes (Reborn cutover, AgentScope 2.0, unified providers) that could either catapult them ahead or introduce destabilizing regressions.
- **Stabilizing:** NanoBot, NullClaw, LobsterAI—focusing on bug-fix sprints and incremental improvements rather than major rewrites. Lower risk, lower upside.
- **Security-driven:** PicoClaw—the 11-advisory batch has forced a reactive posture; future releases will be judged on how quickly vulnerabilities are patched.
- **Backlog clearing:** NanoClaw—closed 40 long-stalled PRs in one day, signaling a "clean house before new construction" strategy. Watch for an imminent major release.

### Community Health Indicators
- **Maintainer responsiveness:** NullClaw (all but one bug fixed within 24h) and NanoBot (GPT-5 fix same day) lead. OpenClaw and Hermes Agent have slower turnaround on P1 issues.
- **Community retention risk:** Projects with open P1 bugs >2 months (OpenClaw #25592, Hermes Agent #7507) may lose power users who encounter these blockers repeatedly.
- **Contributor diversity:** IronClaw shows high external contributor engagement (`Dannye013`, `abbyshekit`), while CoPaw's community is more concentrated among Chinese developers.

---

## 7. Trend Signals

### Industry Trends Extracted from Community Feedback

1. **Agent self-awareness is the next frontier.**  
   Multiple projects (CoPaw #5017, ZeroClaw #5862) have users asking: *"My agent doesn't know it can add cron."* The ability for agents to self-document, expose their own capabilities as tools, and discover system features is emerging as a key differentiator. Developers should invest in **introspective agent design**—where the agent's system prompt includes a self-inventory of available commands and skills.

2. **Multi-model orchestration is becoming table stakes.**  
   Users across OpenClaw, NanoBot, CoPaw, and LobsterAI are demanding per-conversation model overrides and independent vision model fallback. The era of "one model to rule them all" is ending; the winning platforms will enable **seamless routing across fast/slow, cloud/local, and text/vision models** without complex configuration.

3. **Security is shifting from optional to mandatory.**  
   PicoClaw's 11-advisory batch, NullClaw's PII redactor fix, and NanoClaw's CSPRNG migration all signal that **security audits are becoming routine for open-source agent projects**. Developers should adopt **defense-in-depth** patterns:

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-06-10

---

## 1. Today's Overview

NanoBot saw **heavy development activity** in the last 24 hours: **23 pull requests** were updated (13 open, 10 merged/closed) and **6 issues** remain open. The project is in a **healthy, fast iteration cycle** with responsive maintainers—several bug fixes were merged within hours of being reported. No new release was cut today, but the high merge velocity signals a feature-rich version may be imminent. Community engagement is strong, with users reporting real-world pain points around **context isolation, model flexibility, and provider compatibility**.

---

## 2. Releases

**No new releases** on 2026-06-10. The last release (if any) predates this digest.

---

## 3. Project Progress

The **10 merged/closed PRs** today indicate solid progress across multiple fronts:

| Merged/Closed PR | What advanced |
|---|---|
| [#4208](https://github.com/HKUDS/nanobot/pull/4208) | **WebUI: “Fork from here”** for assistant replies – users can branch a conversation at any assistant response. |
| [#4177](https://github.com/HKUDS/nanobot/pull/4177) | **Documentation overhaul** – beginner-friendly setup, CLI chooser, provider recipes, deployment guides. |
| [#4265](https://github.com/HKUDS/nanobot/pull/4265) | **Cron adjustment** for `daily-english-read` skill (daily → every 2 days). |
| [#3434](https://github.com/HKUDS/nanobot/pull/3434) | **Feishu channel LaTeX rendering** via CodeCogs – no new dependencies. |
| [#3400](https://github.com/HKUDS/nanobot/pull/3400) | **Dream constrol** – users can now prevent Dream from editing `SOUL.md` / `USER.md` (new `allow_edit_identity_files` flag). |
| [#4034](https://github.com/HKUDS/nanobot/pull/4034) | **GitAgent Protocol support** – `agent.yaml` + `SOUL.md` for portable AI agents. |
| [#4190](https://github.com/HKUDS/nanobot/pull/4190) | **Tool call validation** – stricter argument parsing (no silent repair of malformed JSON). |
| Others | Several test harness PRs (memory lifecycle, runner) remain open but are near-complete. |

Key features that **advanced but are still open** include: [memory cursor monotonic fix](https://github.com/HKUDS/nanobot/pull/4256), [symlink workspace escape prevention](https://github.com/HKUDS/nanobot/pull/4119), [read-only root separation](https://github.com/HKUDS/nanobot/pull/4053), [fenced-code-aware message splitting](https://github.com/HKUDS/nanobot/pull/4257), and [StepFun ASR provider](https://github.com/HKUDS/nanobot/pull/4260).

---

## 4. Community Hot Topics

### Most discussed issues (by comment count)

- **[#4253 – Support overriding model per conversation](https://github.com/HKUDS/nanobot/issues/4253)** (3 comments)  
  *User request:* A user who switches between a fast OpenRouter model and a private local model wants to toggle per conversation, not globally. This is a common **workflow flexibility** need.

- **[#4259 – history.jsonl cross-session context pollution](https://github.com/HKUDS/nanobot/issues/4259)** (2 comments)  
  *Bug report:* All session histories are injected into the system prompt of any active session, causing **context leakage**. This is a **critical data isolation issue** – no fix PR exists yet.

- **[#4061 – OpenAI-compatible text tool calls not parsed](https://github.com/HKUDS/nanobot/issues/4061)** (1 comment)  
  Some providers emit tool calls as plain text; NanoBot ignores them. **Blocks tool usage** for those providers.

### Most active PR (by recent updates)

- **[#4268](https://github.com/HKUDS/nanobot/pull/4268) & [#4263](https://github.com/HKUDS/nanobot/pull/4263) – Fix `max_completion_tokens` for GPT-5 models**  
  Both opened within hours of [#4261](https://github.com/HKUDS/nanobot/issues/4261). Shows **fast maintainer response** to provider compatibility bugs.

---

## 5. Bugs & Stability

| Priority | Issue | Description | Fix available? |
|----------|-------|-------------|----------------|
| **Critical** | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | Cross-session history injection → context pollution, potential data leakage. | ❌ No |
| **High** | [#4261](https://github.com/HKUDS/nanobot/issues/4261) | GPT-5 models reject `max_tokens`; must use `max_completion_tokens`. | ✅ Yes – PR #4268, #4263 |
| **High** | [#4061](https://github.com/HKUDS/nanobot/issues/4061) | Text-format tool calls not parsed → tools fail silently. | ❌ No |
| **Medium** | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | `idleCompact` removes last 8 messages, so important corrections may be omitted from summaries. | ❌ No |
| **Low** | [#4262](https://github.com/HKUDS/nanobot/issues/4262) | Agent mode shows default puppy icon instead of configured `botIcon` at first load. | ❌ No |
| **Low** | [#4257](https://github.com/HKUDS/nanobot/pull/4257) | `split_message` can break fenced code blocks (PR open but not merged). | ✅ Partial fix in PR |

**Note:** The context pollution bug ([#4259](https://github.com/HKUDS/nanobot/issues/4259)) is the most severe – it affects all multi-session users and has no merged fix. Maintainers should prioritise it.

---

## 6. Feature Requests & Roadmap Signals

### Likely to land in next release

- **Model per conversation** ([#4253](https://github.com/HKUDS/nanobot/issues/4253)) – high community demand, relatively isolated change.
- **On-demand version check** ([#4255](https://github.com/HKUDS/nanobot/pull/4255)) – removes background polling; small, non-breaking.
- **StepFun ASR provider** ([#4260](https://github.com/HKUDS/nanobot/pull/4260)) – adds speech-to-text support; seems well-tested.

### Stretch goals

- **Session fork from WebUI** – merged today ([#4208](https://github.com/HKUDS/nanobot/pull/4208)), already in main.
- **Dream identity file protection** – merged ([#3400](https://github.com/HKUDS/nanobot/pull/3400)).
- **`split_message` code-block awareness** – PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) near-complete.

### Roadmap signals

Multiple PRs add **test harnesses** (memory lifecycle, runner), indicating a push for **stability and regression coverage** before the next release. The **GitAgent Protocol** merge suggests an interest in interoperability standards.

---

## 7. User Feedback Summary

### Pain points

- **Model inflexibility** – Users want to switch models (e.g., local vs cloud) per conversation, not globally ([#4253](https://github.com/HKUDS/nanobot/issues/4253)).
- **Context pollution** – Multi-session users see other conversations' summaries injected into their current session ([#4259](https://github.com/HKUDS/nanobot/issues/4259)).
- **Broken tool calls** – Providers that emit text-format tool calls are unusable ([#4061](https://github.com/HKUDS/nanobot/issues/4061)).
- **Branding friction** – Agent mode ignores user-defined `botIcon` ([#4262](https://github.com/HKUDS/nanobot/issues/4262)).
- **Version awareness** – Users want a lightweight way to check for updates without background polling ([#4255](https://github.com/HKUDS/nanobot/pull/4255), [#4235](https://github.com/HKUDS/nanobot/issues/4235)).

### Satisfaction signals

- **Positive reaction** to the forking feature (PR merged quickly).
- **Quick fixes** – The `max_tokens` bug was patched the same day it was reported.
- **LaTeX in Feishu** and **Dream identity protection** demonstrate responsiveness to niche but valuable user requests.

---

## 8. Backlog Watch

### Issues needing maintainer attention

| Issue | Age | Priority | Status |
|-------|-----|----------|--------|
| [#4061](https://github.com/HKUDS/nanobot/issues/4061) – Text tool calls not parsed | 12 days | **High** – breaks functionality for some providers | No PR, no assignee |
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) – Cross-session context pollution | 1 day | **Critical** – new, but no fix yet | No PR yet |
| [#4264](https://github.com/HKUDS/nanobot/issues/4264) – `idleCompact` skips corrections | 1 day | **Medium** – affects summary quality | No PR yet |

### Long-standing open PRs without recent activity

- [#4119](https://github.com/HKUDS/nanobot/pull/4119) – Symlink workspace escape fix (open 10 days, last updated 2026-06-09) – appears ready for review.
- [#4053](https://github.com/HKUDS/nanobot/pull/4053) – Read-only root separation (open 12 days) – important security fix.
- [#3983](https://github.com/HKUDS/nanobot/pull/3983) – Runner blocked tool-call tests (open 17 days) – waiting for review.

**Recommendation:** Prioritise [#4259](https://github.com/HKUDS/nanobot/issues/4259) (context pollution) and [#4061](https://github.com/HKUDS/nanobot/issues/4061) (tool call parsing) to prevent regressions for current users. The security-focused PRs #4119 and #4053 should also be merged soon.

---

*Generated from GitHub data snapshot: 2026-06-10, last 24h activity.*  
*Data source: [HKUDS/nanobot](https://github.com/HKUDS/nanobot)*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-10

## 1. Today’s Overview
Hermes Agent is experiencing very high activity: **50 issues** and **50 pull requests** were updated in the last 24 hours, with 4 issues closed and 6 PRs merged/closed. The community is actively debating new features (Telegram guest bots, per‑tool configuration, provider additions) while also reporting critical bugs (password redaction breaking multi‑turn calls, cron delivery failures, stale‑stream retry loops). The project shows strong momentum in skills bundling (multiple PRs adding 15+ new skills) and platform integration, but several P1/P2 stability bugs remain unmerged. Overall, the project is healthy but would benefit from faster resolution of high‑severity issues.

---

## 2. Releases
**No new releases** in the last 24 hours. The latest version remains at 0.16.0 (as referenced in issues #42780, #42989).

---

## 3. Project Progress
**6 PRs were merged/closed today** (details not available from the provided data). Among the **open PRs**, the following represent significant improvements that are being actively reviewed:

- **#43222 / #43231** – Two concurrent fixes for stale‑stream escalation (escalate consecutive kills to trigger provider fallback). Both address **#43211** (P2 bug).
- **#43223** – Cron security: do not strict‑scan script‑injected output in no‑skills jobs (fixes a false‑positive security check).
- **#43221** – Remove red‑team skills (`godmode`, `obliteratus`) that trip Anthropic’s output classifier, causing session failures.
- **#43229** – Adds inline “Reply & unblock” banner for blocked kanban tasks (feature from #43216).
- **#43235** – Fix dashboard host validation for remote hosts (Tailscale, reverse proxy setups).
- **#43234** – Fix desktop default project directory not being honored for new sessions.

Additionally, **3 skill‑bundling PRs** (#43173, #43174, #43179, #43180) together add 15+ new skills (Canvas LMS, ARM64 deployment, TypeScript patterns, Linux admin, etc.), signalling a strong push toward expandable skill ecosystem.

---

## 4. Community Hot Topics
The most active discussions (by comment count and reactions):

- **#21587** [Feature: Telegram Guest Bots, Bot‑to‑Bot, Stickers and Chat Automation] – 9 comments, 1 👍  
  Users are excited about Telegram’s May 2026 AI bot update; they want Hermes to leverage guest bots, stickers, and automation for multi‑agent workflows.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/21587)

- **#43083** [Bug: Passwords replaced by *** but model reads back its own conversation history and fails on second tool call] – 6 comments, P1  
  A critical password‑masking defect that breaks tool calls across turns. The reporter provides a specific code reference and a defence‑in‑depth suggestion.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/43083)

- **#42006** [Bug: macOS launchd_restart missing bootout before bootstrap, gateway falls back to detached after update] – 5 comments, P2  
  A recurring restart loop on macOS after `hermes update`. The community has identified the root cause (missing `launchctl bootout`), but no fix PR is yet attached.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/42006)

- **#13107** [Feature: support command description override via config.yaml] – 4 comments  
  Users want locale‑aware bot command descriptions on Telegram/Discord.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/13107)

- **#29331** [Feature: Add Volcengine (火山引擎) as built‑in provider] – 3 comments, 1 👍  
  Growing demand for ByteDance’s platform, which already has an official Hermes integration guide.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/29331)

- **#42086** [Bug: Gemini 2.5/2.0 not supported in `_supports_media_in_tool_results`] – 3 comments  
  Vision tool fails for older Gemini models; a PR may already be in progress.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/42086)

- **#43014** [Bug: cron deliver=origin fails to resolve delivery target in CLI sessions] – P1, 2 comments  
  Cron jobs with `deliver=origin` produce no delivery target; user cannot receive output.  
  [Link](https://github.com/NousResearch/hermes-agent/issues/43014)

---

## 5. Bugs & Stability
High‑severity bugs reported or updated today:

| ID | Severity | Description | Fix PR exists? |
|----|----------|-------------|----------------|
| #43083 | **P1** | Passwords redacted in history cause model to read back its own output, failing second tool call. | No (discussion only) |
| #43014 | **P1** | Cron `deliver=origin` never resolves a target; delivery fails silently. | No |
| #43211 | **P2** | Stale stream errors silently retry on same provider instead of falling back. | Yes: #43222 & #43231 (open) |
| #42006 | **P2** | macOS gateway restart loop after update (launchctl bootstrap without bootout). | No |
| #43165 | **P2** | Discord voice inactivity timeout fires under `/voice off`, spamming channel. | Yes: #43165 (open) |
| #42780 | **P3** | Self‑hosted OIDC callback ignores `HERMES_DASHBOARD_PUBLIC_URL` in Docker/reverse proxy. | No |
| #41744 | **P3** | `auxiliary.title.enabled: false` config is ignored; title generation always runs. | No |
| #42992 | **P3** | Desktop UI clips multi‑line user messages (only first 2 lines visible). | No |
| #42962 | **P3** | Desktop doesn’t refresh when same session is updated from Telegram gateway. | No |
| #42084 | **P3** | WeChat Silk voice messages cannot be transcribed (no format conversion). | Yes (duplicate of existing fix?) |
| #43042 | **P3** | Desktop file browser shows ENOENT when `session.info` event fires in remote gateway mode. | No |
| #43122 | **P3** | Messaging provider icons (Matrix, Slack) not dark‑theme friendly. | No |
| #34070 | **P3** | Honcho memory prefetch hangs on fresh CLI subprocess (regression from v0.15.0). | No |

**Stability note:** Two competing PRs (#43222 and #43231) both try to fix #43211, which may cause merge conflicts; the community would benefit from a unified approach.

---

## 6. Feature Requests & Roadmap Signals
Notable user‑requested features that may appear in the next release:

- **Telegram Guest Bots & Bot‑to‑Bot (#21587)** – Highly requested; if merged, would unlock multi‑agent Telegram workflows.
- **Volcengine Built‑in Provider (#29331)** – Already documented externally; likely to be added soon.
- **Per‑tool enable/disable below toolset level (#31375)** – Many users want to disable `web_search` while keeping `web_extract`; a clean config improvement.
- **Context Selection/Routing as first‑class engine (#36765)** – An RFC proposing to separate context routing from compression; could reshape the `ContextEngine` API.
- **Disable `execute_code` approval prompts in YOLO mode (#42921)** – Users want full autonomy; currently blocked by hardcoded prompt.
- **Local provider overlay / env var (#43052)** – Simplify configuring local endpoints like vLLM.
- **Kanban Review Transition (#42896)** – Move tasks into “review” status; currently missing from CLI lifecycle.
- **Kanban inline “Reply & unblock” (#43216)** – Already implemented in PR #43229; likely to ship next.
- **Cron failure diagnostic context (#43177)** – Adds error details to cron notifications; helpful for debugging.

**Prediction:** The next minor release (0.17.0) will likely include skill bundling (15+ new skills), the kanban inline unblock, stale‑stream escalation fixes, and possibly the Volcengine provider. The Telegram guest bot feature may take longer due to complexity.

---

## 7. User Feedback Summary
Real pain points expressed by the community:

- **Password handling (#43083)** – “defence‑in‑depth: redact credentials from tool call arguments before they enter conversation history” – user provided a code patch suggestion.
- **macOS update reliability (#42006)** – “gateway falls back to detached mode; no upgrade without manual intervention” – frustrated users.
- **Cron delivery (#43014)** – “deliver=origin fails every time with no error explanation” – user had to SSH and manually find logs.
- **Desktop‑gateway sync (#42962, #42989)** – “new messages are persisted but the Desktop chat view remains stale” – multiple reports.
- **Matrix reply quoting (#7507)** – “every response includes `m.in_reply_to` creating clutter” – user wants configurable quoting.
- **Gemini 2.5 vision gap (#42086)** – “Gemini 2.0 users also affected” – a duplicate bug signals multiple users hitting this.
- **Ollama spinner timeout (#43028)** – “local model progress spinner hangs for 30 seconds; no way to suppress” – user wants quiet mode.
- **Skill security false positive (#43221)** – “red‑team skill descriptions trip Anthropic classifier and kill unrelated work” – prompt injection risk acknowledged; fix PR submitted.

Overall sentiment is **positive** (many feature requests and bug reports are constructive), but there is clear dissatisfaction with **unresolved P1 bugs** and **slow rotation of stale streams** that can lead to silent failures.

---

## 8. Backlog Watch
Issues and PRs that have been open for an extended period without maintainer response or progress:

| ID | Age | Severity | Issue | Status |
|----|-----|----------|-------|--------|
| #7507 | Since Apr 11 (2 months) | P2 | Matrix reply quoting configurability | No recent maintainer comment |
| #13107 | Since Apr 20 (1.5 months) | P3 | Command description override via config | No assignee |
| #20307 | Since May 5 (1 month) | P3 | Plugin hook for `transform_api_message` | No activity from maintainers |
| #34070 | Since May 28 (2 weeks) | P3 | Honcho memory prefetch hang on fresh subprocess | No PR; user suggests regression from #27190 |
| #36765 | Since Jun 1 (9 days) | P3 | RFC: context selection as first‑class engine | No follow‑up from core team |
| #31375 | Since May 24 (2 weeks) | P3 | Per‑tool enable/disable config | No assignee or milestone |

These items may require maintainer prioritisation. The `transform_api_message` hook (#20307) is particularly important for plugin developers, as noted by the community.

---

*Generated from GitHub data for Hermes Agent (github.com/nousresearch/hermes-agent) as of 2026-06-10.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-10

## 1. Today's Overview
The project is experiencing very high activity, with **20 issues** and **17 pull requests** updated in the last 24 hours. A batch of **11 security advisories** (issues #3068–#3078) was filed yesterday by security researcher YLChen-007, covering SSRF bypasses, authorization loopholes, and launcher access control weaknesses — most remain open and unpatched. Concurrently, the core team merged **5 PRs** (including a major agent collaboration bus, two Anthropic model fixes, and a config migration safety fix) and published a nightly build. The project is in a reactive and patching-heavy phase, balancing new features (DeltaChat gateway, NEAR AI provider, streaming config) with urgent security hardening. Overall health is **active but pressured**, with a clear need for rapid triage on the reported vulnerabilities.

## 2. Releases
- **nightly (v0.2.9-nightly.20260610.b9a8fad6)**: Automated nightly build based on the `main` branch. May be unstable. No breaking changes or migration notes are provided in the release itself.  
  [Full changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

One stable release remains at v0.2.9; this nightly tracks ongoing development.

## 3. Project Progress
**Merged/closed PRs today (5):**
- [#2937](https://github.com/sipeed/picoclaw/pull/2937) – **Feat/agent collaboration**: Introduces an internal Agent Collaboration Bus with per-agent mailboxes, collaboration threads, and structured messaging. (Closed/merged)
- [#2942](https://github.com/sipeed/picoclaw/pull/2942) – **fix(config): use canonical hyphenated model ID for default claude-sonnet entry** – Prevents first-launch failures for Anthropic users. (Closed)
- [#2940](https://github.com/sipeed/picoclaw/pull/2940) – **fix(providers): omit temperature for claude-opus-4-7** – Resolves HTTP 400 errors when using the newer Claude Opus model. (Closed)
- [#3064](https://github.com/sipeed/picoclaw/pull/3064) – **fix(config): add ok check for type assertion in migration model name indexing** – Prevents panic on malformed config entries. (Closed)
- [#3086](https://github.com/sipeed/picoclaw/pull/3086) – **docs: update wechat qrcode** – Minor documentation update. (Closed)

**Notable open PRs that advanced today:**
- [#3063](https://github.com/sipeed/picoclaw/pull/3063) – Feat: add DeltaChat gateway (new channel integration)
- [#3087](https://github.com/sipeed/picoclaw/pull/3087) – Fix: allow workspace-relative exec paths (fixes false positive in exec guard)
- [#3084](https://github.com/sipeed/picoclaw/pull/3084) – Fix: normalize `.gitignore` encoding (repository hygiene)
- [#3083](https://github.com/sipeed/picoclaw/pull/3083) – Feat: harden launcher access control (adds proxy trust configuration)
- [#3085](https://github.com/sipeed/picoclaw/pull/3085) – Fix: block `198.18.0.0/15` in SSRF guard

## 4. Community Hot Topics
- **#2404 – [Feature] Add streaming HTTP request config** – 11 comments, 1 👍, open since April. Users are requesting a `"streaming": true` config option to enable SSE-style streaming from LLM backends (like OpenAI client). This is the most discussed open feature request.  
  [Issue link](https://github.com/sipeed/picoclaw/issues/2404)

- **#2796 – [BUG] History shows only last user message** – 6 comments, closed today via PR #2990. Users reported that multi-message conversations in history were truncated. The fix ensures full session history is read for the Web UI.  
  [Issue link](https://github.com/sipeed/picoclaw/issues/2796)

- **#3088 – [Feature] Use vodozemac instead of libolm** – 0 comments but new (filed yesterday). Highlights a security/maintainability concern: replacing the unmaintained `libolm` with its official successor. No maintainer response yet.  
  [Issue link](https://github.com/sipeed/picoclaw/issues/3088)

- **#2984 – [Feature] Add explicit turn completion signal for Pico WebSocket clients** – 1 comment, 1 👍. Request for a deterministic “turn end” event in the WebSocket protocol, indicating a potential design gap for external clients.  
  [Issue link](https://github.com/sipeed/picoclaw/issues/2984)

## 5. Bugs & Stability
**Critical (Security):** The most severe bugs reported today are the 11 security issues filed by YLChen-007 (#3068–#3078). They cover:

- **SSRF bypasses** in the `web_fetch` tool (#3074, #3077, #3078) – via ISATAP IPv6, special-use IPv4 `198.18.0.0/15`, and environment-configured HTTP proxies.
- **Authorization bypasses** – Feishu reply-context `allow_from` bypass (#3082), MQTT `client_id` spoofing (#3068), WeCom group trigger bypass (#3076).
- **Launcher control-plane takeover** – CSRF on first-run password setup (#3072), `allowed_cidrs` bypass via loopback proxying (#3069, #3080), and WebSocket `/reload` privilege escalation (#3071).
- **Other** – Symlink race in approval hook (#3081), auto-loading of untrusted `skills/` into system prompt (#3075), LINE webhook replay (#3073), OneBot media fetch (#3070).

Most are **unpatched** as of today. However, two fix PRs were opened concurrently:  
- `#3085` blocks the `198.18.0.0/15` range in SSRF guard.  
- `#3083` hardens launcher access control (proxy trust, localhost bypass config).

**Moderate bugs (non-security):**
- **#2796 (history truncation)** – Fixed via merged PR #2990.  
- **#2939 (temperature deprecation for claude-opus-4-7)** – Closed, fixed via #2940.  
- **#3087 (exec false positive for relative workspace paths)** – Open, fix PR #3087 submitted.

**Low-severity:**  
- `.gitignore` encoding issue (#3084) – PR submitted.  
- Windows console flashes (#3061) – PR open.  
- `dm_scope` config not saving (#3067) – PR open.

## 6. Feature Requests & Roadmap Signals
- **Streaming HTTP config (#2404)** – High demand, likely to land in next stable release given its simplicity and community interest.
- **DeltaChat gateway (#3063)** – Adds a new messaging channel (email-based chat). Signals continued expansion of integration surface.
- **NEAR AI Cloud provider (#2917)** – Another OpenAI-compatible provider, part of the provider-ecosystem growth. Still open after 20 days.
- **Vodozemac migration (#3088)** – Security-driven dependency swap. Could be fast-tracked given the project’s current security focus.
- **Agent collaboration (#2937)** – Already merged; this is a major architectural feature that will enable multi-agent workflows.
- **Explicit turn completion signal (#2984)** – Likely needed for third-party WebSocket clients; may be prioritized once security issues are resolved.

Prediction for next stable (v0.3.0): Streaming config (#2404), security patches for the most critical SSRF and authorization bypasses (#3074, #3077, #3078, #3068), and the agent collaboration bus.

## 7. User Feedback Summary
- **Pain points:**
  - “Temperature is deprecated for claude-opus-4-7” – user blocked entirely until fix (#2939).
  - “History only shows last user message” – UX regression for multi-turn conversations (#2796).
  - “Exec safety guard blocks relative workspace paths” – affects skill developers using scripts in subdirectories (#3087).
  - “`dm_scope` setting cannot be saved” – config UI inconsistency (#3067).
- **Use cases expressed:**
  - Streaming HTTP responses for real-time LLM interactions (#2404).
  - Multi-agent collaboration and inter-agent mailboxes (PR #2937).
  - Integration with DeltaChat, WeCom, Feishu, LINE, OneBot, MQTT – show demand for enterprise/group-chat deployments.
- **Satisfaction/Dissatisfaction:**
  - The quick closure of #2939 (temperature bug) and #2796 (history bug) indicates responsive maintainers for breaking issues.
  - However, the batch of security disclosures reveals that users (or security auditors) consider the project’s network controls and authorization layers insufficient. No advisory has been acknowledged or mitigated yet as of this digest.

## 8. Backlog Watch
| Item | Type | Age | Status | Notes |
|------|------|-----|--------|-------|
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) – Streaming HTTP config | Enhancement | ~2 months | Open, 11 comments | High community interest, no maintainer response in weeks. |
| [#2984](https://github.com/sipeed/picoclaw/issues/2984) – Turn completion signal | Feature | 8 days | Open, 1 comment | Protocol design gap; needs maintainer decision. |
| [#2917](https://github.com/sipeed/picoclaw/pull/2917) – NEAR AI Cloud provider | PR (feature) | 20 days | Open, stale label | No recent activity from maintainers or author. |
| [#2983](https://github.com/sipeed/picoclaw/pull/2983) – Retry empty LLM response | PR (fix) | 9 days | Open, stale label | Important robustness fix; may have been deprioritized. |
| [#2988](https://github.com/sipeed/picoclaw/pull/2988) – Fix `summarize_token_percent` config | PR (fix) | 8 days | Open, stale label | Addresses configuration correctness. |
| [#3061](https://github.com/sipeed/picoclaw/pull/3061) – Hide Windows console flashes | PR (fix) | 2 days | Open | Windows usability fix, not critical but waiting for review. |
| [#3088](https://github.com/sipeed/picoclaw/issues/3088) – Vodozemac migration | Feature | 1 day | Open | Security-driven; should be fast-tracked. |

All open security issues (#3068–#3082) are essentially new (1 day old) and should be considered the highest-priority backlog items for maintainers.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-06-10

## 1. Today’s Overview

Today marks a significant cleanup sprint for NanoClaw: **44 pull requests were updated**, of which **40 were merged or closed** – many were long‑stalled items finally resolved. Activity is extremely high, with a single open issue (#1690) drawing community attention. No new releases were cut, but the volume of merged PRs suggests a release candidate may be near. Overall project health is strong, with maintainers actively addressing both security fixes and feature backlogs.

## 2. Releases

No new releases are available in the reporting period. No version changes, breaking changes, or migration notes to report.

## 3. Project Progress

The following notable PRs were merged or closed today (all 40 closed/merged PRs updated in the last 24h). Highlights include:

- **🛠 Feature: Finance DD Agent** – PR #2723 (closed). Adds a due‑diligence skill for financial analysis.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2723)

- **🩹 Fix: Feishu zombie card cleanup** – PR #2718 (closed). Resolves a production bug where interactive cards stayed stuck on “running” after agent‑runner timeout.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2718)

- **🔐 Security Fix: Telegram pairing codes (CSPRNG)** – PR #2722 (open). Switches from `Math.random` to `crypto.randomInt` for pairing codes.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2722)

- **🌐 Web UI Control Panel** – PR #212 (closed). Unblocks a full dashboard at `localhost:3100` after months of being blocked.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/212)

- **📜 Trace Observability** – PR #1202 (closed). Adds agent trace recording and a local web UI on port 3001.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/1202)

- **⚡ Direct Runner Mode (no Docker)** – PR #1285 (closed). Introduces `NANOCLAW_DIRECT_RUNNER=1` for in‑process Claude SDK execution.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/1285)

- **🧩 Skill Marketplace/Registry** – PR #1309 (closed). CLI commands to discover and install skills from GitHub repos.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/1309)

- **📦 Plugin System** – PR #1387 (closed). Adds a plugin architecture analogous to channels.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/1387)

- **🧹 Documentation & Infrastructure** – Multiple docs PRs merged: security audit report (#214), JSDoc improvements (#379, #380), container sandbox design (#1084), group‑level CLAUDE.md examples (#481), and a `/setup-dev` skill (#1161).

## 4. Community Hot Topics

The **single open issue** updated today is **#1690** (“Multi‑runtime agent SDK abstraction”) by *chiptoe-svg*. It proposes a modular abstraction allowing Claude, Codex, and local models to be installed as skills – mirroring the channel pattern. With **5 comments** and **3 thumbs‑up** in two months, it reflects a strong community desire for multi‑provider flexibility.  
[GitHub](https://github.com/nanocoai/nanoclaw/issues/1690)

Other hot PRs (closed today) include the Web UI (#212) and finance DD agent (#2723), both of which garnered community discussion (comments not shown but implied by their long lifecycle).

## 5. Bugs & Stability

- **Critical (fixed today): Feishu zombie active cards** – PR #2718. Cards remained stuck on “运行中” for 50+ minutes after agent‑runner was killed. Fix now cleans up on abnormal exit.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2718)

- **High (open): Telegram pairing code predictability** – PR #2722. `Math.random` could allow attacker to guess codes and gain owner privileges. Fix proposes CSPRNG.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2722)

No new bug reports or regressions were filed in the last 24h besides these two. The prompt trace logging (#337) and seed file injection (#357) were also merged after long blocks, indicating past stability concerns are resolved.

## 6. Feature Requests & Roadmap Signals

The most prominent feature request is **#1690 – multi‑runtime abstraction** (modular SDK support). Given its alignment with the existing skill/channel pattern and the recent merge of a plugin system (#1387) and skill marketplace (#1309), a multi‑runtime skill is highly likely to be included in the next release.

Other signals:
- **Web UI** (#212) is now unblocked and will likely ship as a first‑class control panel.
- **Direct runner mode** (#1285) enables lightweight deployments without Docker – a common pain point.
- **Agent trace observability** (#1202) provides debugging and audit capabilities.
- **Finance due diligence** (#2723) shows continued growth in domain‑specific skills.

Predict next release will include: Web UI, direct runner, observability dashboard, and possibly the multi‑runtime abstraction if #1690 is adopted soon.

## 7. User Feedback Summary

Based on issue #1690 comments and the nature of merged PRs, users are expressing:

- **Desire for model flexibility** – want to switch between Anthropic Claude, OpenAI Codex, and local open‑source models without major rewrites.
- **Concerns about Docker overhead** – direct runner mode (#1285) directly addresses this.
- **Need for better debugging** – prompt trace logging (#337) and trace observability (#1202) were community‑driven.
- **Security awareness** – the Telegram pairing code fix (#2722) shows users are paying attention to auth hardening.

Satisfaction appears high given the number of contributions being merged; dissatisfaction stems mainly from slow resolution of blocked PRs (now mostly closed).

## 8. Backlog Watch

Today’s massive cleanup closed **many long‑stale PRs** (PRs #212, #337, #357, #379, #380, #481, #1084, #1161, #1192, #1202, #1245, #1285, #1309, #1333, #1387 – all older than 2 months). This indicates maintainers are actively reducing the backlog.

The **only remaining open item** with potential stagnation is **#1690** (created 2026-04-07, last updated today). While it has comments and reactions, it has not yet been assigned or labelled with a milestone. Maintainers should consider acknowledging it with a status label (e.g., “needs review” or “planned”) to set community expectations.

No other unanswered issues or PRs were detected in the last 24h.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-10

## 1. Today’s Overview
The project saw a burst of activity over the past 24 hours, with **5 issues** and **8 pull requests** updated. Four issues were closed, and seven PRs were either merged or closed — suggesting a focused sprint on bug fixes and minor features. One new PR remains open (targeting the agent-cron delivery bug). No new releases were cut. Overall project health appears strong, with maintainers responding quickly to user-reported problems.

## 2. Releases
No new releases in the last 24 hours.

## 3. Project Progress
Seven pull requests were merged or closed today:

- **#945** — `fix(redaction): reject ISO date/time patterns as false-positive phone matches`  
  Closes #944. Adds a date‑like guard to prevent PII redactor from mistaking timestamps for phone numbers.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/945)

- **#946** — `fix(agent): filter tools in system prompt text by tool_filter_groups`  
  Ensures the text‑based system prompt only includes built‑in and always‑active MCP tools; dynamic‑group MCP tools remain available via native API calls.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/946)

- **#947** — `feat(providers): add Evolink as an OpenAI-compatible provider`  
  Adds Evolink, a multi‑model gateway, as a first‑class provider.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/947)

- **#943** — `fix(telegram): show typing indicator during callback-query processing`  
  Resolves #942. The typing “…” indicator now appears when users press inline buttons.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/943)

- **#940** — `fix(models): query base_url for custom OpenAI-compatible providers`  
  Fixes #936. Custom providers are now queried for their actual model list instead of falling back to hardcoded Claude models.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/940)

- **#939** — `fix(agent): honor compact_context flag instead of always compacting`  
  Closes #937. The `compact_context` flag in agent config is now actually read at runtime.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/939)

- **#711** — `Feat/cross memory`  
  A large feature PR adding deterministic memory event streams for cross‑agent memory synchronisation. Merged after a long development cycle.  
  [View PR](https://github.com/nullclaw/nullclaw/pull/711)

## 4. Community Hot Topics
The most active item today is **Issue #941** (open), which reports that agent‑type cron jobs never spawn a subprocess for Telegram delivery. It has one comment and has been open since May 31. Users are waiting for a resolution — the attached fix PR (#948) is still open.  
[View Issue #941](https://github.com/nullclaw/nullclaw/issues/941)

Older issues (#936, #937, #942, #944) have all been closed by the PRs above, indicating the community’s pain points are being actively addressed.

## 5. Bugs & Stability
Bugs reported or fixed today, ranked by severity:

- **High – #941 (open): Agent‑type cron jobs don’t spawn subprocess**  
  Scheduled agent jobs that should send via Telegram never run. No fix has been merged yet; PR #948 is open.  
  [View Issue](https://github.com/nullclaw/nullclaw/issues/941) | [View Fix PR](https://github.com/nullclaw/nullclaw/pull/948)

- **Medium – #944 (closed, fix merged): PII redactor falsely matches date/time as phone numbers**  
  Already fixed in PR #945.

- **Medium – #942 (closed, fix merged): Telegram typing indicator missing for inline buttons**  
  Already fixed in PR #943.

- **Low – #936 (closed, fix merged): Custom OpenAI provider falls back to Claude models**  
  Already fixed in PR #940.

- **Low – #937 (closed, fix merged): Dead `compact_context` flag in agent config**  
  Already fixed in PR #939.

No regressions were reported today.

## 6. Feature Requests & Roadmap Signals
- **Cross‑agent memory** (PR #711) — merged today. This adds the infrastructure for synchronising memory across agent instances, a feature that had been in development since March. It unlocks use cases like shared preferences and context between separate agents.  
- **First‑class provider support** — PR #947 adds Evolink. Users may request more provider additions (e.g., Ollama, vLLM) in the future.  
- **Custom provider model listing** — Issue #936 (now fixed) highlighted the need for dynamic model discovery; this pattern may be extended to other provider types.

The next release will likely include all the merged fixes and possibly refinements to the cross‑memory feature.

## 7. User Feedback Summary
- **Pain points**:  
  - Cron‑based agent delivery bugs (Issue #941).  
  - PII redactor false positives on timestamps (Issue #944).  
  - Missing UX feedback in Telegram (Issue #942).  
  - Provider configuration not working as documented (Issue #936).

- **Satisfaction indicators**:  
  - All but one of the reported bugs were fixed within 24 hours of being updated.  
  - The typing indicator fix (#943) addresses a frequently‑mentioned UX annoyance.  
  - The addition of Evolink (#947) expands multi‑model choices without extra configuration.

## 8. Backlog Watch
- **Issue #941** (open, created May 31) remains the most pressing unresolved bug. It has a proposed fix in PR #948, which is still open and awaiting review/merge. Maintainers should prioritise this to prevent workflow breaks for users relying on scheduled agent jobs.  
  [View Issue](https://github.com/nullclaw/nullclaw/issues/941) | [View PR](https://github.com/nullclaw/nullclaw/pull/948)

All other previously open issues have been closed within the last 24 hours, suggesting the maintainers are clearing the backlog efficiently. No other long‑unanswered items were observed.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-10

## 1. Today’s Overview

IronClaw is in a period of intense activity, with **46 issues** and **50 pull requests** updated in the last 24 hours. The project is heavily focused on **Reborn production cutover** (epic #3026) and **WebUI v2 end-to-end coverage** (epic #4632). Two recent PRs were merged/closed, though the majority of PRs remain open and under active review. No new releases were cut. The overall health is strong, but several **critical blockers** (e.g., strict-mode provider incompatibility, duplicate `model` field in requests) demand immediate attention to maintain stability across the first-party tool ecosystem.

## 2. Releases

*No new releases in the last 24 hours.*

## 3. Project Progress

### Merged/Closed PRs Today
- **2 pull requests** were closed or merged in the last 24 hours (details not present in the top-20 list). The closed issues below represent completed work that likely corresponds to those PRs.

### Closed Issues (Resolved by PRs)
- **#4604** — [Reborn WebUI v2 lacks a browser-driven full-stack E2E](https://github.com/nearai/ironclaw/issues/4604) – Identified the gap; coverage now being built via #4632.
- **#4609** — [Reborn WebUI v2 audit & test authentication parity](https://github.com/nearai/ironclaw/issues/4609) – All v1 auth paths catalogued and covered in WebChat v2.
- **#4591** — [Operator command-plane foundation for setup/config/diagnostics/lifecycle APIs](https://github.com/nearai/ironclaw/issues/4591) – Typed `RebornServicesApi` facade and handler shells planted.
- **#4447** — [Close OpenAI-compatible API migration with compatibility & security tests](https://github.com/nearai/ironclaw/issues/4447) – Final acceptance for the #3283 migration.
- **#4446** — [Translate projection streams to OpenAI-compatible SSE](https://github.com/nearai/ironclaw/issues/4446) – Streaming over Reborn EventStreamManager shipped.

### Key Open PRs Advancing Features
- **#4670** – [Bridge inbound bytes into transcript AttachmentRefs](https://github.com/nearai/ironclaw/pull/4670) – Track 6 of universal attachments (#4644).
- **#4654** – [Extensible attachment format registry](https://github.com/nearai/ironclaw/pull/4654) – First track of #4644, replacing four scattered lists.
- **#4600** – [Slack personal DM outbound targets](https://github.com/nearai/ironclaw/pull/4600) – Phase 4 of trigger delivery default outbound plan.
- **#4544** – [Scoped lifecycle admin foundation for Reborn capabilities](https://github.com/nearai/ironclaw/pull/4544) – Multi-tenant shared tools.
- **#4663** – [Project-scoped automation ownership core model](https://github.com/nearai/ironclaw/pull/4663) – Foundation for project-scoped agents.

## 4. Community Hot Topics

### Most Active Issues (by comment count)
- **#3026** (3 comments) – [Epic: Reborn production wiring and cutover readiness](https://github.com/nearai/ironclaw/issues/3026).  
  *Underlying need*: The entire production cutover plan is gated on this epic. Engineers need clarity on how the production graph is built, validated, and prevented from serving traffic when services are missing or unverified.
- **#4642** (1 comment) – [Strict-mode providers’ null-for-unset-optionals rejected by capability-port validation](https://github.com/nearai/ironclaw/issues/4642).  
  *Underlying need*: This affects **most first-party tools** when used with strict-mode LLMs (e.g., DeepSeek). A fix is urgently needed to restore tool functionality.
- **#88** (1 comment) – [Security hardening (device pairing, elevated mode, safe bins, media URL validation)](https://github.com/nearai/ironclaw/issues/88).  
  *Underlying need*: Safety critical; several OpenClaw security features are still missing from IronClaw.
- **#4551** (1 comment) – [Reborn: wire production Postgres storage config](https://github.com/nearai/ironclaw/issues/4551).  
  *Underlying need*: PostgreSQL support exists but the standalone `ironclaw-reborn` binary lacks the glue to use it in production.
- **#4548** (1 comment) – [Chat completion serializes duplicate top-level `model` field when tools included](https://github.com/nearai/ironclaw/issues/4548).  
  *Underlying need*: Blocks DeepSeek API usage entirely; reported by user `darren2013`.

### Most Active Pull Requests
- **#4600** (no comments listed) – [Slack personal DM outbound targets](https://github.com/nearai/ironclaw/pull/4600) – High-density PR with broad implications for Slack channel routing.
- **#4588** – [Observability seams: trajectory observer + LLM provider injection](https://github.com/nearai/ironclaw/pull/4588) – Critical for external hosts like `nearai-bench`.
- **#4671** – [Extra-capabilities seam for host-supplied tools](https://github.com/nearai/ironclaw/pull/4671) – Opens the door for custom host capability registration.

## 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **Critical** | [#4642](https://github.com/nearai/ironclaw/issues/4642) | Strict-mode providers send `null` for unset optionals; validator rejects against non-nullable schema → **all first-party tools break with strict LLMs**. | No PR yet |
| **High** | [#4548](https://github.com/nearai/ironclaw/issues/4548) | Duplicate `model` field in request body when tools are included → **DeepSeek rejects with HTTP 400**. | No PR yet |
| **Medium** | [#4640](https://github.com/nearai/ironclaw/issues/4640) | `google-calendar list_events` returns oldest events (no `timeMin`, missing ordering) → **wrong results for “upcoming meetings”**. | No PR yet |
| **Low** | [#4673](https://github.com/nearai/ironclaw/issues/4673) | NEAR AI provider config cannot be saved after successful test connection → **onboarding fails silently**. | No PR yet |

**Observations**: No fix pull requests have been opened for any of these bugs in the top-20 PR list. The two critical bugs (#4642, #4548) impact core functionality and should be prioritized.

## 6. Feature Requests & Roadmap Signals

Strong signals for the next minor release (likely 0.6.x):

- **Universal attachments for all channels** ([#4644](https://github.com/nearai/ironclaw/issues/4644)) – Multi-track effort already with 7 stacked PRs. Will enable images, documents, and CSV uploads in Reborn WebChat and Slack.
- **Unified (omni) search** ([#4647](https://github.com/nearai/ironclaw/issues/4647)) – Requested by `ilblackdragon` to search threads, skills, extensions, memory. Predicted for v0.6.
- **Slack channel-routed personal & team agents** ([#4625](https://github.com/nearai/ironclaw/issues/4625)) – High demand for a single Slack app supporting both DM and team interactions.
- **Admin-shared tools & skills** ([#4628](https://github.com/nearai/ironclaw/issues/4628)) – Multi-tenant capability management for enterprise deployments.
- **Ask-gated capability approvals in REPL** ([#4667](https://github.com/nearai/ironclaw/issues/4667)) – Developer tooling gap for testing capabilities that require user approval.
- **Extra-capabilities seam** ([#4671](https://github.com/nearai/ironclaw/pull/4671)) – Allows hosts to register custom tools as Reborn capabilities; likely to land soon.

**Prediction**: The next release will likely include the complete attachment pipeline (#4644), project-scoped automation ownership (#4662–#4664), and the extra-capabilities seam (#4671). The Reborn production cutover (#3026) is still in progress and may slip to a subsequent release.

## 7. User Feedback Summary

### Pain Points (from issues and PRs)
- **“Attachments silently dropped in Reborn”** – Users on the v2 WebChat cannot upload files; the transcript is text-only and bytes never persisted (see #4644).
- **“Search is fragmented and dishonest”** – The frontend-only command palette cannot search across agents, extensions, or memory (see #4647).
- **“Slack team agents require separate app”** – Current architecture forces each team to install a new Slack app; users want a single multi-tenant app (see #4625).
- **“Google OAuth tokens are per-extension”** – Users authenticate once but are prompted again for different Google APIs (see #4657).
- **“NEAR AI provider setup fails silently”** – Test connection passes but Save does nothing; users cannot proceed (see #4673).

### Satisfaction Signals
- **Strong developer engagement** – 50 PRs in 24h, many from core contributors and external contributors (e.g., `Dannye013`, `abbyshekit`).
- **Transparent roadmap** – Epics like #3026 and #4644 are well-documented with dependency graphs, splitting issues, and stacked PRs.
- **Stability culture** – Closeout issues (#4447, #4446) prove the team is investing in compatibility and security tests before declaring features shipped.

## 8. Backlog Watch

### Long-Unanswered Issues Requiring Maintainer Attention
- **#88** (created 2026-02-14) – [Security hardening](https://github.com/nearai/ironclaw/issues/88) – Open for **4 months** with only 1 comment. This covers device pairing, elevated mode, safe bins, and media URL validation – a significant gap in safety features. No PR has been linked.
- **#3026** (created 2026-04-28) – [Reborn production cutover epic](https://github.com/nearai/ironclaw/issues/3026) – Despite many sub-issues, the epic itself lacks a clear owner and checklist progress. Blocking production deployment.
- **#4548** (created 2026-06-08) – [Duplicate `model` field bug](https://github.com/nearai/ironclaw/issues/4548) – No assignee, no fix PR. High impact for DeepSeek users.
- **#4642** (created 2026-06-09) – [Strict-mode provider rejection](https://github.com/nearai/ironclaw/issues/4642) – Filed by core contributor `BenKurrek` but not yet triaged. Should be escalated to **P0**.
- **#4666** (created 2026-06-10) – [File-size cap on slack_host_state.rs](https://github.com/nearai/ironclaw/issues/4666) – Tracking per architecture rules; no decomposition PR in progress. A refactoring candidate that could languish.

### PRs Stalling
- **#4521** (open 4 days) – [JSON cleaner](https://github.com/nearai/ironclaw/pull/4521) by a new contributor (`Dannye013`). Needed: maintainer review and guidance on tests/scope.

---

*Data snapshot: 2026-06-10 23:59 UTC. All links are from the [nearai/ironclaw repository](https://github.com/nearai/ironclaw).*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-10

## Today's Overview

The project saw high development activity with **5 pull requests updated in the last 24 hours**, of which **4 were merged or closed**, signalling a focused push toward feature completion and bug fixing. Two open issues were raised, indicating continued community engagement around multi‑model orchestration and agent extensibility. No new releases were cut today. The rapid merge rate, especially for task completion notifications and data backup features, suggests the team is sprinting toward a stable release candidate.

## Releases

*No new releases were published today. Omit section.*

## Project Progress

Four PRs were merged/closed today, advancing three functional areas:

- **Data Backup & Migration** — PRs [#2136](https://github.com/netease-youdao/LobsterAI/pull/2136) (feature) and [#2135](https://github.com/netease-youdao/LobsterAI/pull/2135) (chore: temporary close) landed, adding persistent backup capabilities. The temporary close suggests a quick rollback or refinement, but the feature is live.
- **Task Completion Notifications** — PR [#2130](https://github.com/netease-youdao/LobsterAI/pull/2130) (feat) and [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) (restore from notification) were merged. These add privacy‑safe system notifications (macOS Dock badge, Windows taskbar badge) for Cowork sessions and allow restoring the app from a notification even when the main window is closed.
- **Fix in Progress** — PR [#2133](https://github.com/netease-youdao/LobsterAI/pull/2133) (fix) remains open, targeting export and code copy bugs in the renderer/cowork areas.

The overall trajectory shows a strong focus on making LobsterAI more reliable and user‑friendly when running in the background.

## Community Hot Topics

Two open issues attracted community attention, though neither has heavy discussion yet:

- **#2131** [OPEN] *LobsterAI 支持 hermes agent有计划吗？* — User asks whether Hermes agent support is planned. [Link](https://github.com/netease-youdao/LobsterAI/issues/2131)  
- **#2132** [OPEN] *跨模型子任务调用的问题* — Detailed analysis of cross‑model sub‑task collaboration, including a proposed fix and detection of gateway‑level function calls not handled by the existing sub‑agent system. [Link](https://github.com/netease-youdao/LobsterAI/issues/2132)

The underlying need is clear: users want **multi‑model orchestration** (e.g., M3 for planning + DeepSeek for execution) and support for additional agent types (Hermes). These are likely to drive roadmap decisions in the coming weeks.

## Bugs & Stability

No new crash reports or regressions were recorded today. The only bug‑fix activity is **PR #2133** (still open), which addresses export and code copy issues. Based on the description, these are likely low‑severity cosmetic or functional glitches in the renderer. No critical stability concerns emerged.

## Feature Requests & Roadmap Signals

Two feature requests surfaced:

1. **Hermes Agent Support** ([#2131](https://github.com/netease-youdao/LobsterAI/issues/2131)) — Signals user desire for a broader agent ecosystem beyond the current built‑in models.
2. **Cross‑Model Sub‑Task Collaboration** ([#2132](https://github.com/netease-youdao/LobsterAI/issues/2132)) — A detailed, engineering‑level request for improving inter‑model communication. The author even provides a diagnostic method and a two‑point improvement plan (same‑model vs. cross‑model notification handling).

Given the current PRs focus on background notifications and task completion, the next version (likely v0.9.x) may include **cross‑model sub‑task status synchronization** as a logical next step. Hermes support might arrive later, pending plugin architecture extensions.

## User Feedback Summary

Real pain points from today’s activity:

- **“My main task (M3) can’t reliably learn when a sub‑task (DeepSeek) finishes or stalls”** — This is the core of issue #2132. The user discovered that gateway‑level function calls are not registered as sub‑agents, breaking the task completion flow.
- **“I want to use Hermes as an agent alongside existing models”** — From issue #2131, indicating a desire for model diversity.
- **Positive signal:** The merged task‑completion notifications (PR #2130) directly address a common frustration: missing completed‑task alerts when the app is backgrounded.

Overall, users are vocal about **orchestration reliability** and **model choice**, while the team is successfully delivering background‑aware UX improvements.

## Backlog Watch

Both open issues were created yesterday (2026‑06‑09) and have received maintainer activity (issue assignments and labels visible in the raw data). No long‑unanswered items currently exist. The most notable item to watch is **PR #2133** (fix), which if merged soon will close the day’s only known bug ticket.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-10

## 1. Today's Overview

The project saw a high level of activity in the last 24 hours, with **39 issues updated** (19 open/active, 20 closed) and **34 pull requests updated** (19 open, 15 merged/closed). A new **beta release (v1.1.11-beta.2)** was published, primarily focusing on browser control improvements. The community is actively reporting bugs and proposing features, with a strong emphasis on desktop performance, model compatibility, and channel integrations (WeChat, DingTalk). Several critical bugs have been addressed by incoming PRs, and the team is making steady progress on the AgentScope 2.0 migration and new plugin infrastructure.

## 2. Releases

### [v1.1.11-beta.2](https://github.com/agentscope-ai/QwenPaw/releases/tag/1.1.11-beta.2)

**Changes:**
- **feat(browser):** Add page coordinate click support to `browser_control` – enables more precise UI automation.
- **fix(browser):** Add CDP timeout parameter and browser profile isolation for cross-browser switching – improves stability when switching between different browser instances.

**Migration notes:**  
No breaking changes are documented for this release. Upgrading should be straightforward via `pip install qwenpaw==1.1.11b2` or the Docker image. The new browser features are backward-compatible with existing automation scripts.

## 3. Project Progress

Merged/closed PRs today (2026-06-10):

- **[#5062](https://github.com/agentscope-ai/QwenPaw/pull/5062) (closed):** Fix E2E test for token usage overview when data is empty – improves test reliability.
- **[#5050](https://github.com/agentscope-ai/QwenPaw/pull/5050) (closed):** Fix system theme toggle icon (computer → sun) – small UX improvement.
- **[#4615](https://github.com/agentscope-ai/QwenPaw/pull/4615) (closed):** Fix ACP orphan process after close – prevents zombie processes from lingering.
- **[#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857) (closed):** Enhanced make-skill flow to support self-evolving skill creation – a major feature for agent skill improvement.
- **[#5056](https://github.com/agentscope-ai/QwenPaw/pull/5056) (closed):** Removed redundant channel-tests CI workflow – streamlines CI pipeline.
- **[#5043](https://github.com/agentscope-ai/QwenPaw/pull/5043) (closed):** Add OpenSandbox plugin with MCP protocol – introduces sandboxed code execution.
- **[#5021](https://github.com/agentscope-ai/QwenPaw/pull/5021) (closed):** Fix `/compact` and auto-compaction ignoring model's `max_input_length` when `active_model` is unset – solves context compression bug.
- **[#5055](https://github.com/agentscope-ai/QwenPaw/pull/5055) (closed):** Bump version to v1.1.11b2 – release preparation.

Additionally, **7 new test files with 129 test cases** were contributed in PR [#4973](https://github.com/agentscope-ai/QwenPaw/pull/4973) (still open, but addition is substantial).

## 4. Community Hot Topics

The most actively discussed issues (by comment count) reveal strong demand for better memory, performance, and multi-model support:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) *(closed)* | 10 | Suggestion to adopt Hermes Agent's "learning loop" for self-evolving skills (👍3) |
| [#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003) *(closed)* | 8 | `coding plan` stuck with Qwen3.7-plus – usability issue |
| [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) *(closed)* | 7 | Models config page lost after new session – critical UX bug |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) *(open)* | 7 | **Breaking change**: Migrate backend from AgentScope 1.x → 2.0 (👍2) |
| [#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878) *(closed)* | 6 | WeChat push failure for cron tasks – channel reliability |
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) *(closed)* | 5 | `/compact` ignores model's `max_input_length` (fixed in #5021) |
| [#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015) *(open)* | 5 | Windows desktop frontend lag during task execution |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) *(open)* | 4 | Local Qwen 3.6 model not responding after v1.1.9 – regression |
| [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994) *(closed)* | 3 | Request for memory system self-evolution (👍1) |
| [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) *(open)* | 3 | Feature request: independent visual model fallback (👍1) |

**Underlying needs:** Users want a more **adaptive and performant** agent – better memory, support for multiple models per session, and smoother desktop experience. The popularity of the Hermes Agent "learning loop" reflects a desire for agents that improve from their own actions.

## 5. Bugs & Stability

Bugs reported today (updated in last 24h) ranked by severity:

| Severity | Issue | Description | Fix PR / Status |
|----------|-------|-------------|-----------------|
| **Critical** | [#5031](https://github.com/agentscope-ai/QwenPaw/issues/5031) *(open)* | Skill slash invocation expands raw SKILL.md content instead of executing – breaks skill UX. | No known PR yet. |
| **Critical** | [#5052](https://github.com/agentscope-ai/QwenPaw/issues/5052) *(open)* | Tool calls fail after several rounds with "unexpected keyword argument 'arguments'" – prevents long conversations with tool use. | No known PR yet. |
| **Critical** | [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) *(open)* | Windows Tauri desktop startup extremely slow (10+ minutes) – regression from Python packaging. | No fix in sight. |
| **High** | [#5030](https://github.com/agentscope-ai/QwenPaw/issues/5030) *(open)* | Double reply in WeChat channel when proactive mode is on – duplicates responses. | Workaround: disable proactive mode. |
| **High** | [#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025) *(open)* | `submit_to_agent` fails with `FileNotFoundError` due to duplicate session_id in file path. | PR [#5036](https://github.com/agentscope-ai/QwenPaw/pull/5036) addresses similar duplication issue. |
| **Medium** | [#5039](https://github.com/agentscope-ai/QwenPaw/issues/5039) *(closed)* | Tag-derived tool calls overwrite each other in OpenAI-compat stream parser – affects multi-tool responses. | Closed; fix assumed in codebase. |
| **Medium** | [#5044](https://github.com/agentscope-ai/QwenPaw/issues/5044) *(closed)* | Tauri desktop: external links not opening, file downloads blocked – caused by architecture (start page → backend redirect). | Closed; workaround or fix applied. |
| **Medium** | [#5042](https://github.com/agentscope-ai/QwenPaw/issues/5042) *(closed)* | Windows: "Open Directory" only works for C: drive – fails for code on other drives. | Closed; likely fixed. |
| **Low** | [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) *(closed)* | PAT tool naming with dots (e.g., `pat.batch_plan`) rejected by DeepSeek API – naming convention conflict. | Closed; should be renamed. |
| **Low** | [#5060](https://github.com/agentscope-ai/QwenPaw/issues/5060) *(closed)* | WeChat channel returns `session_id` instead of `user_id` when session exists – cron delivery fails. | Closed; fix applied. |

Two critical issues remain open with no obvious fix PR: the skill content leak and the tool call keyword error. The Windows desktop startup regression is a significant usability blocker.

## 6. Feature Requests & Roadmap Signals

Notable feature requests from the community:

| Issue | Request | Likely for Next Version |
|-------|---------|------------------------|
| [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994) *(closed)* | **Memory system self-evolution** – hierarchical memory framework. | High interest (👍1). Team already working on skill self-evolution (#4857). Could be extended to memory. |
| [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) *(open)* | **Independent visual model fallback** – when main model lacks vision, use a separate vision model. | Likely soon, as it aligns with multi-model support. |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) *(closed)* | **One-click session switching** (sidebar) – reduces clicks to switch sessions. | PR [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) already implements customizable column order; sidebar might be next. |
| [#4951](https://github.com/agentscope-ai/QwenPaw/issues/4951) *(closed)* | **OpenSandbox support** for sandboxed code execution. | Already implemented in PR [#5043](https://github.com/agentscope-ai/QwenPaw/pull/5043) – included in upcoming release. |
| [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) *(open)* | **AgentScope tracing initialization** – connect to external monitoring (e.g., Arize Phoenix). | Likely to be addressed as part of AgentScope 2.0 migration (#4727). |
| [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) *(closed)* | **Hermes Agent learning loop** – agents that create and iterate skills from behavior. | The team already merged self-evolving skills (#4857). This confirms direction. |

**Roadmap signal:** The AgentScope 2.0 migration ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)) is the most significant upcoming change, touching backend architecture and APIs. It will likely ship in a major version (e.g., 2.0.0). Plugin infrastructure (#4997, #5033) is also progressing.

## 7. User Feedback Summary

**Satisfaction signals:**
- Users praise QwenPaw's **localization** and **out-of-box experience** for Chinese users (#5017: "国内用起来特别舒服").
- The project is actively incorporating community suggestions (e.g., OpenSandbox, self-evolving skills).

**Pain points (dissatisfaction):**
- **Desktop performance regressions:** Tauri-based desktop is significantly slower than the previous Python-packaged version (#5047: "ten minutes to start").
- **Streaming UI lag:** Long streaming replies cause browser/system-wide stutter (#4792, closed).
- **Channel delivery issues:** WeChat cron notifications fail; double replies in proactive mode (#4878, #5030).
- **Model compatibility:** DeepSeek API rejects tool names with dots; some models' reasoning content not displayed (#4962, #5013, #5045).
- **Context compression not respecting model limits:** Despite fixes, some users still encounter issues (#4937, fixed in #5021).
- **Many small UX bugs:** Image preview jitter (#4993), theme icon ambiguity (#5050, already fixed), slow session switching with many messages (#4917).

Overall, the community is enthusiastic about the project's direction but frustrated by regressions introduced in recent releases, especially on Windows desktop.

## 

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-10

## Today’s Overview

Activity remains very high: **50 issues and 50 PRs were updated in the last 24 hours**, with 48 issues open and 49 PRs still in progress. Two issues were closed (#4710, #7117) and one PR was merged/closed (#7425). No new releases were published today. The project is in a healthy, fast-moving development cycle, with substantial energy going into bug fixes, observability, and cross-channel improvements. The community is actively contributing both bug reports and code, and the maintainers are responding quickly.

## Releases

No new releases today.

## Project Progress

**Merged / Closed PRs Today:**

- **#7425** (closed) – *fix(runtime): resolve channel pricing via bare-type fallback in cost lookup* – fixes a silent cost-tracking bug that left per-day budget enforcement inert for every channel agent.
- **#7442** (open, but listed as updated today – likely pending merge) – *fix(runtime): make parallel SubAgents and Delegates return reliably* – exempts re-entrant agent-spawning tools from the duplicate-call guard, enabling intentional fan-out.

**Closed Issues Today:**

- **#4710** – Logo improvement request (closed after community design contributions).
- **#7117** – Config UX parity across CLI, Quickstart, zerocode, and web surfaces (accepted, closed as implemented or superseded).

Other notable open PRs that advanced features or fixes include:  
- **#7365** – Reworks the documentation book and auto-derives provider/config surfaces from source.  
- **#7385** – Adds turn metadata to observer events and correlates OTel spans by `turn_id` – a key observability improvement.  
- **#7367** – Routes inbound webhooks per channel alias (multi-instance WhatsApp, etc.).  
- **#7350** – Wires `reasoning_effort` into the dedicated Azure OpenAI provider.  
- **#7348** – Honors `catch_up_on_startup = false` to skip overdue cron jobs on startup.  
- **#7361** – Implements per-turn output routing via `send_via` and fixes voice delivery bugs (RFC-6969).

## Community Hot Topics

The most active discussions (by comment count) highlight several recurring themes:

1. **#4710 – Logo design** (19 comments, 2 👍)  
   Community-driven design for a better logo. Shows engagement in branding.

2. **#5862 – ZeroClaw doesn’t know it can add cron** (12 comments)  
   Users want better tool discovery; the agent doesn’t expose the `zeroclaw cron` command. Suggests a need for self-documenting capabilities.

3. **#5937 – Unify providers architecture** (10 comments)  
   High-risk refactor to eliminate code duplication around `reqwest` and model construction. Underlying need for maintainable multi-provider support.

4. **#5982 – Per-sender RBAC for multi-tenant deployments** (9 comments)  
   Users need role-based access control to serve different user classes (customers, operators) with isolated workspaces.

5. **#6378 – Discord bot respond only in specific channels** (7 comments)  
   Consistency request: `allowed_channels` for Discord, matching Matrix and Nextcloud Talk patterns.

6. **#5844 – Too much emphasis on memory** (6 comments)  
   Repeated complaint that system prompt over-prioritises memory over current instructions, especially in cron jobs.

These collectively indicate demand for better usability, discoverability, security control, and channel parity.

## Bugs & Stability

**Critical / High Severity (S1 – workflow blocked):**

- **#6034** – User messages lost in single/multi-turn conversations – all providers fail with 400 error  
  *Fix PR: not yet linked*
- **#5808** – Default 32k context budget exceeded by system prompt + tool definitions on first iteration – perpetual trimming  
  *Fix PR: #7440 (skip futile trim when system prompt exceeds budget)*
- **#6646** – `web_search_tool` and `web_fetch` not firing via Telegram channel in v0.7.5  
  *Fix PR: #7438 (telegram delivery prompt no longer discourages tool use)*
- **#6721** – `tool_search` not in `default_auto_approve` causes 120s hang then auto-deny in webhook mode  
  *No fix PR yet*
- **#6687** – Two independent `SopEngine` instances: MQTT-started runs invisible to agent `sop_status`  
  *No fix PR yet*
- **#6862** – Gateway SPA fallback serves `index.html` for unimplemented `/api/*` routes – breaks dashboard  
  *No fix PR yet*
- **#6037** – Cron jobs launched repeatedly while still running (no lock) – *status: in-progress*
- **#6916** – Shell/skill subprocess can OOM container – *feature/enhancement, not yet fixed*

**Medium Severity (S2 – degraded behavior):**

- **#5844** – Memory emphasis too high – degrades cron job performance
- **#6002** – ZeroClaw not clearly addressed in Telegram – confusion on which messages trigger response
- **#6584** – OpenAI-compatible provider ignores `reasoning` field (only reads `reasoning_content`) – *Fix PR: #7423*
- **#7376** – zerocode Dashboard hides error states, labels history as active sessions – *Fix PR: #7444*
- **#7377** – zerocode dark themes inherit unreadable terminal foreground text
- **#7378** – macOS Cmd-C copy triggers quit chord instead
- **#7253** – Web console Config page shows JSON parse error

**Low Severity (S3):**

- **#7400** – zerocode locale selection does nothing until restart and download

Several fix PRs are already open for today’s bugs, indicating responsive maintainers.

## Feature Requests & Roadmap Signals

Prominent feature requests this week:

- **#5982** – Per-sender RBAC (multi-tenant) – high risk, accepted. Likely a candidate for v0.9.
- **#5937** – Unify providers architecture – high risk, accepted. Refactoring groundwork for better provider extensibility.
- **#6378** – Discord channel restriction parity – accepted, relatively low complexity, could land soon.
- **#6916** – Process memory limits on shell/skill subprocesses – high risk, accepted. Security hardening.
- **#7248** – Persist cached input tokens for cost accounting – accepted, improves observability.
- **#6917** – Honor action-scope filter in Composio dispatch – blocked, but design is clear.
- **#7410** – Read gateway webhook signing secrets from live config instead of caching at startup – accepted, follow-up from #7367.

Recent PRs indicate that the next minor release (v0.8.x) will likely include:  
- Webhook routing per alias (#7367)  
- Observability enhancements (turn metadata, OTel spans) (#7385)  
- Azure reasoning effort support (#7350)  
- Per-turn output routing (#7361)  
- Cron job catch-up fix (#7348)  

These align with the roadmap for better security, multi-instance support, and observability.

## User Feedback Summary

**Pain Points (direct from bugs & comments):**

- “ZeroClaw doesn’t know it can add cron.” – Users expect the agent to expose its own scheduling tool.
- “Too much emphasis on memory” – System prompt overvalues stored memories, degrading current-task performance.
- “web_search_tool and web_fetch not firing via Telegram” – Integration failures with self-hosted models.
- “Telegram delivery instructions discourage tool use” – Wording makes the model skip tool calls.
- “Default context budget exceeded immediately” – Users with many tools cannot run first turn without trimming.
- “Dashboard hides error states” – TUI doesn’t communicate loading/error clearly.
- “zerocode dark theme unreadable on light terminal” – Theme inheritance bug.
- “Cmd-C treated as quit on macOS” – Basic usability issue.
- “Web console Config page shows JSON parse error” – Broken frontend-backend communication.

**Satisfaction signals:**  
- High community participation in PRs and bug reports.  
- Quick response from maintainers – many bugs have fix PRs within the same day.  
- The logo discussion (#4710) shows community pride and engagement.

## Backlog Watch

Issues/PRs that have been open for a while and may need maintainer attention:

- **#4853** – Installing skills from `.well-known` URI (created 2026-03-27, accepted but blocked). Industry standardisation is brewing; should be revisited as skills ecosystem matures.
- **#5775** – Per-skill security permissions (created 2026-04-15, accepted, blocked). Critical for secure multi-skill deployments.
- **#5842** – Track `extra_args` validation for security-affecting Codex CLI flags (created 2026-04-17, accepted). Needs implementation.
- **#6250** – Extract `require_auth` to route-layer middleware (created 2026-05-01, accepted, no-stale). Important for security hardening of admin APIs.
- **#6917** – Honor action-scope filter in Composio dispatch (created 2026-05-25, accepted, blocked). Depends on composio SDK updates.
- **#6973** – Fix WhatsApp LID JID handling (created 2026-05-27, still open). Affects WhatsApp web channel reliability.
- **#6037** – Cron jobs repeated while running (created 2026-04-23, status in-progress). Still no fix merged; important reliability issue.

These items represent technical debt or blockers that could become community frustration if left unattended for several more weeks.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*