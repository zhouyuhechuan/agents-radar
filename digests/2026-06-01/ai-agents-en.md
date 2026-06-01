# OpenClaw Ecosystem Digest 2026-06-01

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-01 02:55 UTC

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

# OpenClaw Project Digest — 2026-06-01

## 1. Today's Overview

OpenClaw continues to see extremely high activity, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, **216 issues were closed** and **296 PRs were merged or closed**, indicating strong forward momentum on bug fixing and feature development. Four beta releases were shipped (v2026.5.31-beta.1 through beta.4), all focused on recovery resilience and channel stability. Despite this, a significant number of critical (P1 / platinum hermit) bugs remain open, particularly around session context confusion, Codex runtime reliability, and message delivery across Telegram, Matrix, and Discord. The project is clearly in a rapid iteration phase, with maintainers and community contributors pushing hard to stabilise the 2026.5 branch.

## 2. Releases

**4 new versions published today:**  
- `v2026.5.31-beta.1`  
- `v2026.5.31-beta.2`  
- `v2026.5.31-beta.3`  
- `v2026.5.31-beta.4`  

All four carry the same highlights:

- **Agents and CLI-backed runtimes recover more cleanly from:** interrupted tool calls, stale session bindings, compaction handoffs, and media delivery retries.  
- **Channels and mobile delivery are steadier across Telegram, WhatsApp, iMessage, and Slack.**  

No breaking changes or migration notes were announced. The rapid beta cycle suggests the team is iterating quickly on fixes before a stable release.

---

## 3. Project Progress

In the last 24 hours, **216 issues were closed** and **296 PRs were merged or closed**. Notable closed PRs and progress areas (based on top items):

| Area | What advanced |
|------|---------------|
| **Agent runtime** | PR #88820 (ready for maintainer look) clears embedded-run activity after recovery declares lane idle – a key fix for stuck-session diagnostics. |
| **Tool schema normalisation** | PRs #88880, #88878 project nullable and cron tool schemas for provider compatibility, preserving `null` clear sentinels. |
| **Mattermost** | PR #88859 fixes attachment routing through upload path – a long-standing delivery gap. |
| **Telegram** | PR #87072 adds opt-in interleaved progress lane for reasoning and runtime events. |
| **Plugin SDK** | PR #88879 adds a typed `resolve_exec_env` hook for plugin-contributed environment variables. |
| **Memory subsystems** | PR #88806 rejects envelope metadata sludge (fixes marker-free shapes); PR #88504 introduces multi-slot memory role architecture (major feature). |
| **Cron & diagnostics** | PR #88294 ensures job name appears in cron run history UI; PR #88872 attributes spawned subagent task records to the correct agent. |
| **Desktop distribution** | PR #88845 requires signed beta desktop distributions with channel-specific Sparkle appcasts. |

A large portion of the day’s work involved CI, documentation, and schema snapshot refreshes (PRs #88876, #88875, #88881).

---

## 4. Community Hot Topics

The following issues and PRs generated the most discussion and reactions:

### Most commented issues

- **#32296** – [Bug]: Agent replies to previous message (session context confusion)  
  *13 comments, platinum hermit, P1, open since March*  
  → Core session state bug that causes conversational misalignment. Users report high frustration; the bug persists across months.  
  [Link](https://github.com/openclaw/openclaw/issues/32296)

- **#87307** – Matrix thread replies sent as normal replies after 2026.5.22 upgrade  
  *11 comments, P1, open*  
  → Regression after stable release; `/status` and `/model` also silent. Community requesting urgent fix.  
  [Link](https://github.com/openclaw/openclaw/issues/87307)

- **#13583** – Pre-response enforcement hooks (hard gates) for mandatory tool-call / policy rules  
  *11 comments, platinum hermit, open since February*  
  → High-demand feature for security-conscious (finance, operations) deployments. Soft prompt instructions deemed insufficient.  
  [Link](https://github.com/openclaw/openclaw/issues/13583)

- **#78308** – Channel-mediated approval for MCP tool calls (consent envelope)  
  *11 comments, platinum hermit, open*  
  → Users want MCP servers to use the same `/approve <id>` pipeline already used for shell-exec.  
  [Link](https://github.com/openclaw/openclaw/issues/78308)

- **#88788** – GHCR 2026.5.28 image emits stale Discord progress commentary config schema  
  *9 comments, P2, opened yesterday*  
  → Docker image schema mismatch between what’s built and what’s shipped; causes runtime rejections.  
  [Link](https://github.com/openclaw/openclaw/issues/88788)

### Notable PR discussions

- **#86953** – Block untrusted workspace setup-only channel loads (security, waiting on author)  
- **#88820** – Clear embedded-run activity on lane idle (ready for maintainer look)  
- **#88859** – Fix Mattermost attachment routing (ready for maintainer look)  

**Underlying needs**: Users are most vocal about session reliability (messages going to wrong targets), regression in Matrix after minor version bumps, and the need for hard security gates to prevent LLM bypass of mandatory rules. The MCP consent envelope feature is widely desired.

---

## 5. Bugs & Stability

Critical (Platinum Hermit / P1) bugs reported or updated in the last 24 hours:

| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| #32296 | P1, Platinum Hermit | Agent replies to previous message (session context confusion) | No |
| #87307 | P1, Gold Shrimp | Matrix thread replies regression on 2026.5.22 | No |
| #88788 | P2, Platinum Hermit | GHCR image emits stale Discord progress commentary config schema | No |
| #83959 | P1, Platinum Hermit | Codex app-server startup retries exhaust before replacement ready | No |
| #85251 | P1, Diamond Lobster | Codex app-server emits turn/started then goes silent – session wedges 360s | No |
| #45494 | P1, Platinum Hermit | Cron jobs silently time out on sustained LLM API outages instead of fast-failing | No |
| #86047 | P1, Platinum Hermit | Codex approval stalls cause interrupted turns in Nextcloud Talk | No |
| #86996 | P1, Platinum Hermit | Active Memory + Codex app-server path causes long latency, hook timeouts, event-loop stalls | No |
| #87616 | P2, Platinum Hermit | GatewayClientRequestError: LLM request times out in ~3 seconds despite configuration | No |
| #85888 | P2, Diamond Lobster | Cron jobs consistently fail with MiniMax 503 during early morning hours | No |
| #88020 | P1, Diamond Lobster (closed) | REPLAY_INVALID_RE missing Anthropic ‘Invalid signature in thinking block’ – hard failure instead of retry | Closed as fixed |

Multiple high-severity Codex and Codex app-server issues (#83959, #85251, #86047, #86996) indicate a systemic weakness in the Codex native runtime path, especially around startup and approval handoffs. These are likely the top priority for the team.

**Regressions** reported this period: #87307 (Matrix thread replies), #88020 (Anthropic thinking signature handling, now fixed).

---

## 6. Feature Requests & Roadmap Signals

Top feature requests active in the last 24 hours:

- **#13583** – Pre-response enforcement hooks (hard gates) – long-standing, high demand.  
- **#78308** – MCP tool call consent envelope – would bring parity with shell-exec security.  
- **#8441** – Per-skill `thinking` and `model` config overrides (planned since Feb).  
- **#32496** – Support `frequency_penalty` / `presence_penalty` for OpenAI-compatible providers.  
- **#79458** – i18n for slash command descriptions (Discord, Telegram).  
- **#73699** – Bridge Discord voice I/O to text-channel agent session.  
- **#88504** – Multi-slot memory role architecture (PR open, feature: ✨ showcase) – likely to land next version.  

**Prediction**: The multi-slot memory feature (#88504) is already in a PR and ready for maintainer review and could debut in the next stable release. The MCP consent envelope (#78308) and pre-response hooks (#13583) have strong community support and are likely roadmapped for the 2026.6 cycle.

---

## 7. User Feedback Summary

Pain points frequently voiced across top issues:

- **Session context confusion** (#32296): “Agent replies to previous message” – multiple users report misalignment that makes the assistant unusable for ongoing conversations.  
- **Matrix regression** (#87307): Upgrading from 2026.5.20 to 2026.5.22 broke thread replies; users demand immediate fix.  
- **Codex runtime latency** (#83959, #85251, #86996): Codex-native agents are slower than standalone Codex and suffer from startup failures and timeouts.  
- **Cron reliability** (#45494, #85888): Cron jobs fail silently on transient outages, causing missed scheduled tasks.  
- **Media delivery gaps** (#88788, #88245): Discord config schema mismatches, WhatsApp media routing issues.  
- **Plugin loading silence** (#78301): Users lose hours debugging opaque plugin failures; want better load-time validation.  

Positive signals: The rapid beta iteration (4 versions in one day) and quick closure of regressions (#88020, #81214) show responsiveness. Users appreciate the frequent updates.

---

## 8. Backlog Watch

Long-unanswered critical issues and PRs that have been open for weeks or months without closing:

| Issue (#) | Age | Summary | Status |
|-----------|-----|---------|--------|
| #32296 | Since 2026-03-02 | Agent replies to previous message (session context confusion) | Open, no fix PR, needs maintainer review / product decision. |
| #13583 | Since 2026-02-10 | Pre-response enforcement hooks (hard gates) | Open, needs security review and product decision. |
| #45494 | Since 2026-03-13 | Cron jobs silent timeout on provider outages | Open, needs live repro. |
| #51628 | Since 2026-03-21 | Telegram delivery queue replays / duplicate entries | Open, needs product

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**2026-06-01 | Ecosystem Analysis for Technical Decision-Makers**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem continues its rapid maturation, with **12 tracked projects** showing divergent evolutionary paths. Activity remains concentrated in a core group of high-velocity projects (OpenClaw, Hermes Agent, CoPaw, ZeroClaw) that serve as technology bellwethers for the space. A clear dichotomy is emerging: **enterprise-focused features** (RBAC, consent envelopes, multi-tenancy) compete with **consumer UX improvements** (voice recording, mobile deployment, conversation rollback) as primary development drivers. The ecosystem is heavily influenced by the OpenAI Codex reference implementation, with every major project either integrating or extending its patterns. Critically, **session reliability, channel delivery consistency, and security gating** appear as universal pain points across all active projects, suggesting foundational infrastructure issues remain unresolved despite rapid iteration.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Health Score |
|---------|----------------------|-------------------|--------------|--------------|
| **OpenClaw** | 500 | 500 | ✅ 4 betas | 🔴 High activity, critical bugs |
| **Hermes Agent** | 50 | 50 | ❌ | 🟡 High activity, regressions |
| **ZeroClaw** | 43 | 50 | ❌ | 🟡 High activity, maintainer bottleneck |
| **CoPaw** | 27 | 9 | ❌ | 🟡 Active, windows UX issues |
| **IronClaw** | 3 | 25 | ❌ | 🟡 Reborn refactor, low community |
| **NanoBot** | 6 | 18 | ❌ | 🟢 Responsive, quick fixes |
| **PicoClaw** | 7 | 10 | ✅ 1 nightly | 🟢 Steady, tight community |
| **NanoClaw** | 3 | 8 | ❌ | 🟡 Critical reliability gaps |
| **LobsterAI** | 0 | 1 | ❌ | 🟢 Quiet but stable |
| **NullClaw** | 2 | 0 | ❌ | 🟢 Minimal activity |
| **Moltis** | 0 | 1 | ❌ | 🟢 Quiet, single PR |
| **TinyClaw** | 0 | 0 | ❌ | ⚫ No activity |
| **ZeptoClaw** | 1 | 0 | ❌ | 🟢 Maintenance only |

**Key observations:**
- **OpenClaw dominates** raw volume (500 issues + 500 PRs) — 10x the next busiest project
- Only **2 projects** shipped releases today (OpenClaw: 4 betas, PicoClaw: 1 nightly)
- **Health distribution**: 2 projects with concerning reliability (OpenClaw critical bugs, NanoClaw host freezes), 5 with stable trajectories, 3 effectively dormant
- **Maintainer bandwidth** appears constrained across ZeroClaw, Hermes, and CoPaw despite high engagement

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Structural modularity** — Plugin SDK (`resolve_exec_env` hooks), multi-slot memory architecture (#88504), and channel abstraction layers are ahead of peers; Hermes and ZeroClaw are still converging on similar patterns
- **Release velocity** — 4 beta releases in 24 hours demonstrates CI/CD maturity unmatched by any peer (closest: PicoClaw's 1 nightly)
- **Community scale** — 500 daily issues/PRs vs. next closest (Hermes at 50) suggests ~10x contributor base; this compounds debugging and feature velocity
- **Review rigor** — PRs explicitly tagged `ready-for-maintainer-review` with clear acceptance criteria; ZeroClaw and IronClaw PRs languish in `needs-maintainer-review` for weeks

**Technical approach differences:**
- **Codex runtime** is deeper integrated than Hermes (which has systemic startup failures) or ZeroClaw (which is still designing its TUI)
- **Session context** is more sophisticated (embedded-run cleanup, envelope metadata rejection) but also more fragile — the #32296 confusion bug is open since March, suggesting architectural tradeoffs
- **Channel support** is broadest (Telegram, Matrix, Discord, WhatsApp, iMessage, Slack) but each has known regressions — Matrix #87307 broke after a minor version bump

**Weaknesses vs. peers:**
- **Codex app-server reliability** is a systemic vulnerability (#83959, #85251, #86047, #86996) — NanoBot and PicoClaw have resolved similar issues more decisively
- **Cron job robustness** trails CoPaw and ZeroClaw — silent timeouts (#45494) and MiniMax 503 failures (#85888) persist
- **Backlog stagnation** — #32296 session confusion, #13583 hard gates, and #45494 cron timeouts have been open 3-4 months without maintainer decisions

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across **multiple projects**, indicating ecosystem-wide needs:

| Requirement | Projects Affected | Specific Needs |
|-------------|-------------------|----------------|
| **Session reliability & context hygiene** | OpenClaw (#32296), NanoBot (#4128), Hermes (#33075), PicoClaw (Codex empty response) | Preventing message duplication, preserving conversation alignment across restarts, correctly discarding stale state |
| **Hard security gates / consent envelopes** | OpenClaw (#13583, #78308), NanoBot (#4103 WS token auth), ZeroClaw (#6876, #6914) | Pre-response enforcement hooks, MCP tool call approval, `allowed_tools` enforcement for all providers |
| **MCP protocol lifecycle management** | OpenClaw (#78308 consent envelope), NanoClaw (PR #2662 HTTP/SSE MCP), NullClaw (#2923 activation failure), IronClaw (#2923 stdio MCP bug), ZeroClaw (#4467 resources/prompts) | Transport diversity (stdio, HTTP, SSE), OAuth-based authorization, resource/prompt support beyond tools |
| **Cross-channel delivery consistency** | OpenClaw (Matrix regression #87307), NanoBot (Feishu heartbeat #4111), PicoClaw (Telegram rich delivery #2856), ZeroClaw (#6647 cron output routing, #5866 Telegram mentions) | Typing indicators, media attachment routing, thread reply fidelity, channel-specific configuration |
| **Scheduled task (cron) hardening** | OpenClaw (#45494 silent timeout), Hermes (#25281 dashboard deletes cron), NanoClaw (ghost sessions PR #1465), CoPaw (#4653 message interruption), NullClaw (#941 agent cron no subprocess) | Transactional execution, channel output delivery, visual audit trails, fail-fast on provider outages |
| **Platform parity (Windows, ARM, Docker)** | OpenClaw (desktop signed betas), CoPaw (#4829 CMD flash, #4844 process locks), ZeroClaw (#4842 aarch64 update), Hermes (#35835 Docker update failure) | Native Windows UX, ARM64 binary distribution, Docker container compatibility |
| **Multi-tenancy & access control** | ZeroClaw (#5982 per-sender RBAC, #6915 skill-scoped tools), Hermes (multi-profile dashboard), NanoBot (#4125 Azure AAD) | Enterprise-grade user isolation, role-based tool activation, SAML/SSO integration |

**Cross-cutting insight:** Security and reliability are not secondary concerns — they are the **primary blocker** for production deployments. Every project has at least one open security gap or reliability regression that would prevent enterprise adoption.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | CoPaw | NanoBot | PicoClaw |
|-----------|----------|--------------|----------|-------|---------|----------|
| **Primary architecture** | Modular reference w/ plugin SDK | OpenAI Codex-aligned | Rust-based, modular channels | Desktop-first, agentic UI | TypeScript, WebSocket-centric | Lightweight Go, embedded-target |
| **Target user** | Developers, integrators, power users | AI-assisted coders | Enterprise ops, IoT | Consumer desktop users | Developers, CI/CD pipelines | Tinkerers, low-resource deployers |
| **Key differentiator** | Broadcast channel support, plugin extensibility | Codex provider compatibility, TUI-first | Hardware/IoT integration, RBAC | Windows/macOS desktop UX, cron-first | Security-first, Azure AAD | Minimal footprint, nightly releases |
| **Maturity stage** | Rapid iteration, stabilization needed | Feature-complete, regression-heavy | Feature development, maintainer bottleneck | UI polish, cron stabilization | Quick-fix responsive, enterprise features | Steady incremental, low noise |
| **Community contribution style** | High-volume bug reports + large PRs | Detailed RFCs + targeted fixes | Substantial feature PRs (hardware, email) | Bug reports + feature requests | Small, focused bug fix PRs | Contributor-driven patches |
| **Risk profile** | High: critical bugs in core session logic | Medium: Codex compatibility ce BIM | Medium-high: maintainer capacity, security gaps | Medium: Windows regression velocity | Low: responsive, quick closure | Low: controlled scope, nightly validation |

**Underappreciated differentiators:**
- **Moltis** is quietly solving session rehydration memory bloat — a problem only OpenClaw and NanoBot have addressed otherwise
- **IronClaw's "Reborn" refactor** is the most ambitious architecture change in the ecosystem; if successful, it could leapfrog OpenClaw's flexibility
- **NullClaw** and **ZeptoClaw** are effectively dormant but may represent "finished" implementations for narrow use cases

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid iteration, high engagement, but unstable:**
- **OpenClaw** (busiest, 4 betas/day) — clear ecosystem leader, but needs a stabilization release
- **Hermes Agent** (50 issues/day) — vocal community, but regressions eroding trust
- **CoPaw** (27 issues/day) — Windows user frustration indicates product-market fit but UX debt
- **ZeroClaw** (43 issues/day) — most ambitious feature set, but maintainer bandwidth is the bottleneck

**Tier 2 — Steady contributors, focused scope:**
- **NanoBot** — responsive maintainers, enterprise features, security-first posture
- **IronClaw** — architectural refactor with low community noise; may emerge stronger
- **PicoClaw** — reliable incremental progress, community of tinkerers

**Tier 3 — Quiet but functional:**
- **NanoClaw** — critical reliability gaps need triage
- **LobsterAI** — stable but ghost session bug neglected
- **Moltis** — focused session hygiene work

**Tier 4 — Dormant / Minimal:**
- **TinyClaw, NullClaw, ZeptoClaw** — either completed, abandoned, or waiting for maintainer attention

**Velocity comparison:** OpenClaw's 4 releases in 24 hours is **10x** the release cadence of any peer. The next closest (PicoClaw: 1 nightly/week) suggests a **significant gap in CI maturity**. However, this velocity comes at a cost — OpenClaw has the most critical open bugs of any project.

---

## 7. Trend Signals

**Industry trends extracted from 2026-06-01 community feedback:**

**1. Session resilience is table stakes, not a differentiator**
Every active project has a session confusion or rehydration bug. Users expect conversations to be *exactly reproducible* across restarts. This is the #1 barrier to autonomous agent adoption in production.

**2. Security regulation is coming to AI agents**
Consent envelopes (#78308), hard gates (#13583), MCP authorization (#2923), and RBAC (#5982) are not "nice to haves" — they are regulatory requirements emerging from enterprise deployments. Projects without security roadmaps will be excluded from finance, healthcare, and operations.

**3. Voice and mobile are underestimated distribution channels**
PicoClaw's Android Termux guide (PR #2902), ZeroClaw's TTS/voice note support (#7050), and NanoBot's WebUI voice recording (PR #4122) signal **mobile-first agent deployment** as a growing pattern. Desktop-only agents will lose relevance.

**4. Local LLMs are a growing but underserved niche**
LM Studio integration requests (#28 in PicoClaw), Ollama tool call failures (#5962 in ZeroClaw), and local model provider friction suggest **air-gapped / offline agent operation** is a real use case that no project fully supports.

**5. MCP is becoming the universal tool protocol — but implementation is fragmented**
MCP appears in every project (stdio, HTTP, SSE, OAuth) but **no project** has complete MCP lifecycle support (tools + resources + prompts + authorization). The ecosystem needs a shared MCP reference implementation.

**6. Windows is the pain point that won't go away**
CoPaw's CMD flash (#4829), ZeroClaw's process locks (#4844), and Hermes' Docker update failure (#35835) show that **Windows UX is consistently the weakest platform** across the ecosystem. Projects targeting developers (who often use macOS/Linux) deprioritize Windows at their peril.

**7. Cron / scheduling is becoming a core workflow engine**
At least 6 projects have open cron bugs. Scheduled agent tasks are not "nice to have" — they are **how agents become autonomous**. The ecosystem is still treating scheduling as an afterthought.

**8. The "Codex dependency" is both a blessing and a curse**
Projects aligned with OpenAI Codex (Hermes, OpenClaw, PicoClaw) inherit both compatibility and instability. Every Codex API change cascades through the ecosystem. Projects diversifying providers (ZeroClaw with hardware, NanoBot with Azure AAD) are investing in multi-provider resilience.

---

**Recommendations for technical decision-makers:**
- **Evaluate OpenClaw** for broadest integration capabilities, but budget for session reliability engineering
- **Consider NanoBot** for security-sensitive deployments (Azure AAD, WS auth, heartbeat hardening)
- **Watch ZeroClaw** for next-generation architecture (RBAC, hardware integration, MCP lifecycle)
- **Avoid** projects in Tier 3-4 unless requirements exactly match their narrow scope
- **Invest** in session resilience, security gates, and multi-channel delivery regardless of project choice — these are ecosystem-wide gaps, not project-specific issues

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-01

## 1. Today's Overview

The project saw **high activity** over the past 24 hours, with **6 issues** and **18 pull requests** updated. Four issues were closed (mostly bug reports with quick fixes), leaving **2 open issues**. Of the 18 PRs, **7 were merged or closed** and **11 remain open** under active development. No new releases were published. The community continues to drive both stability improvements (crash fixes, security hardening) and new capabilities (Azure AAD auth, voice recording, MCP safety). The maintainers responded quickly to several high-severity bugs reported in the last few days.

---

## 2. Releases

**No new releases** on this date. The latest available version remains from an earlier tag (no release data provided).

---

## 3. Project Progress (Merged/Closed PRs Today)

Seven pull requests were merged or closed, fixing bugs and advancing features:

- **[#4127] fix(agent): extend sustained goal iteration budget**  
  Adds internal continuation for `/goal` workflows that hit the normal tool‑call limit, with a clean boundary in `nanobot.session.turn_continuation`.  
  [PR #4127](https://github.com/HKUDS/nanobot/pull/4127)

- **[#4121] feat(webui): polish chat rendering and host runtime**  
  Stabilises streamed chat rendering, ensures reasoning deltas form ordered Thought blocks, and keeps WebUI host behaviour capability‑checked without desktop‑specific naming.  
  [PR #4121](https://github.com/HKUDS/nanobot/pull/4121)

- **[#4117] fix(webui): handle undefined language in code blocks**  
  Fixes the white‑screen crash (issue #4116) by defaulting to `"text"` when a fenced code block has no language specifier.  
  [PR #4117](https://github.com/HKUDS/nanobot/pull/4117)

- **[#4112] fix(heartbeat): fail closed on internal checks**  
  Makes the notification evaluator configurable so heartbeat can fail closed while user reminders stay fail‑open; suppresses proactive message‑tool delivery during internal checks.  
  [PR #4112](https://github.com/HKUDS/nanobot/pull/4112)

- **[#4103] fix: Require auth for WebSocket token issuance**  
  Patches the security hole reported in #4077 by requiring `Authorization` on the token issue route when a static WebSocket token is configured.  
  [PR #4103](https://github.com/HKUDS/nanobot/pull/4103)

- **[#4114] fix(heartbeat): skip empty HEARTBEAT.md and fail closed on delivery**  
  Closes #4111 by skipping heartbeat when only template headers/comments exist and by failing closed on delivery to prevent false "All clear." notifications.  
  [PR #4114](https://github.com/HKUDS/nanobot/pull/4114)

- **[#4118] Test push** (trivial test PR, closed without impact)

---

## 4. Community Hot Topics

While discussion volume is currently low, two items stand out:

- **[#4120] Vest × HKUDS: tool recommendations or monetization angle**  
  [Issue #4120](https://github.com/HKUDS/nanobot/issues/4120) – An external contributor proposes a “Vest MCP Integration” to help agents recommend SaaS tools, framed as both a user‑value improvement and a potential revenue opportunity. No maintainer response yet.

- **[#4125] Enhancement: Add support for Azure AAD Based Auth for Azure OpenAI Provider**  
  [Issue #4125](https://github.com/HKUDS/nanobot/issues/4125) – A user wants token‑based (Azure Identity) auth to comply with enterprise policies. A companion PR [#4126](https://github.com/HKUDS/nanobot/pull/4126) has already been submitted, showing strong community alignment.

Neither issue has significant reaction counts, but both address real infrastructure needs (enterprise auth, monetisation).

---

## 5. Bugs & Stability

| Issue | Severity | Status | Description | Fix PR? |
|-------|----------|--------|-------------|---------|
| **#4128** — User messages duplicated in session archive | **High** | Open | In `retain_recent_legal_suffix`, the `else` branch can cause user messages to appear in both `archive` and `kept`, leading to LLM context inconsistency. | Not yet (but #4129 is a related fix) |
| **#4116** — WebUI white‑screen on code blocks without language | **High** | Closed | Crashed the entire WebUI when loading a session with bare ``` blocks. | Fixed by #4117 |
| **#4077** — Unauthenticated WebSocket token minting | **High** | Closed | Static token configured but empty `tokenIssueSecret` allowed anyone to mint short‑lived tokens. | Fixed by #4103 |
| **#4111** — Heartbeat sends false “All clear.” to Feishu | **Medium** | Closed | Cron job reported even when `HEARTBEAT.md` contained only template text. | Fixed by #4114 |
| **#4123** (PR) — MCP unsafe HTTP URLs before probe | **High** | Open (PR) | Currently MCP SSE/HTTP URLs are probed without SSRF guards; proposed fix validates early and fails closed. | #4123 |
| **#4119** (PR) — Symlink workspace escape via relative paths | **High** | Open (PR) | `cat link.txt` could escape workspace if symlink points outside. | #4119 |
| **#4124** (PR) — XML tool calls from mimo/glm models leak to channels | **Medium** | Open (PR) | Raw XML like `<function=exec>...` appears in chat because models emit tool calls as text instead of structured `tool_calls`. | #4124 |

Most reported bugs received fixes within 1–2 days. The open issue **#4128** about message duplication is the most urgent unresolved stability concern.

---

## 6. Feature Requests & Roadmap Signals

Strong signals for the next release include:

- **Azure AAD‑based authentication** ([#4125](https://github.com/HKUDS/nanobot/issues/4125) + PR [#4126](https://github.com/HKUDS/nanobot/pull/4126)) – Already implemented, likely to ship soon.
- **Voice recording and local ASR transcription** ([PR #4122](https://github.com/HKUDS/nanobot/pull/4122)) – Adds WebUI composer recording with FunASR integration. Tagged `enhancement, invalid` (possibly mis-labelled), but the feature code is submitted.
- **GatewayHTTPHandler refactor** ([PR #4115](https://github.com/HKUDS/nanobot/pull/4115)) – Extracts HTTP routing from `WebSocketChannel` as a step toward hot‑reload support. Part of an ongoing architecture improvement.
- **Dream skill ownership markers** ([PR #4101](https://github.com/HKUDS/nanobot/pull/4101)) – Prevents Dream from overwriting user‑created skills without explicit `dream_managed: true`.
- **Filesystem extra roots kept read‑only** ([PR #4099](https://github.com/HKUDS/nanobot/pull/4099)) – Security hardening for write‑capable tools.

Based on activity and maintainer responsiveness, the next minor version will likely include **Azure AAD auth**, **WebUI voice recording**, **session message duplication fix**, and **MCP URL safety checks**.

---

## 7. User Feedback Summary

- **Pain points expressed:**
  - Azure OpenAI users blocked by strict subscription policies requiring Azure Identity auth (no API keys allowed). (Issue #4125)
  - WebUI completely unusable when loading sessions with unlabelled code blocks (#4116).
  - Heartbeat cron spamming Feishu with irrelevant “All clear.” messages (#4111).
  - Lack of WebSocket token security could expose internal agents (#4077).
  - Session manager’s archive logic can corrupt context by duplicating user messages (#4128).

- **Positive signals:**
  - Quick turnaround on critical bugs (e.g., white‑screen crash closed within hours).
  - Willingness to accept external contributions (e.g., Vest partnership proposal, Azure AAD PR from a new contributor).

The overall sentiment appears constructive, with users actively reporting and patching issues. No strong dissatisfaction was voiced beyond the specific bugs noted.

---

## 8. Backlog Watch

These items remain open and may need maintainer attention:

- **[#1443] feat: decouple heartbeat reasoning from notification**  
  [PR #1443](https://github.com/HKUDS/nanobot/pull/1443) – Opened **2026-03-02**, no comments, no maintainer review. Proposes making heartbeat reasoning silent by default with a `sendReasoning` config flag. This long‑standing PR touches core heartbeat behaviour and should be evaluated for merge or closure.

- **[#3990] refactor(dream): replace two-phase Dream class with simple cron + process_direct**  
  [PR #3990](https://github.com/HKUDS/nanobot/pull/3990) – Opened 2026-05-24, no comments. A significant refactor of the Dream subsystem; without maintainer feedback it risks bit‑rotting.

- **[#4120] Vest × HKUDS: tool recommendations or monetization angle** – While only 1 day old, this is a partnership/proposal issue that would benefit from a maintainer response to set expectations.

- **Open bugs without associated fix PRs:**  
  - [#4128](https://github.com/HKUDS/nanobot/issues/4128) (message duplication) – No fix PR yet, though [#4129](https://github.com/HKUDS/nanobot/pull/4129) partially addresses the same file.

---

*Generated from public GitHub data for HKUDS/nanobot on 2026-06-01.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-01

## 1. Today's Overview
Project activity remains high, with **50 issues** and **50 PRs** updated in the last 24 hours (42 open / 8 closed each). No new releases were published. The community is actively reporting regressions (especially around `openai-codex` instability, terminal freezes, and configuration mismatches) while maintainers are merging fixes for several P1/P2 bugs. Feature requests around cloud sync, mobile apps, and sub-agent orchestration continue to gather strong support. Overall, the project is in an intense iterative phase — rapid bug fixes land alongside significant feature proposals.

## 2. Releases
**None.** No new versions were released today.

## 3. Project Progress
Eight PRs were merged/closed today; the most notable changes:

- **Model bump** → [PR #36191](https://github.com/NousResearch/hermes-agent/pull/36191) (closed): Updated MiniMax model identifier to `minimax/minimax-m3` in OpenRouter and Nous portal catalogs.
- **Kanban architecture docs** → [PR #36203](https://github.com/NousResearch/hermes-agent/pull/36203) (closed): Added architecture overview and data flow documentation for the Kanban subsystem.
- **Model capability hook** → [PR #23014](https://github.com/NousResearch/hermes-agent/pull/23014) (closed): Introduced a provider-level hook to declare model capabilities (approved after earlier review).
- **Feishu Drive comment validation** → [PR #36206](https://github.com/NousResearch/hermes-agent/pull/36206) (open): Tightened `file_type` enum for Feishu Drive comment tools.

Closed issues include several high-impact bugs (see §5), suggesting maintainers are actively triaging regressions.

## 4. Community Hot Topics
| Issue | Comments | 👍 | Summary |
|-------|----------|----|---------|
| [#33075](https://github.com/NousResearch/hermes-agent/issues/33075) *[closed]* | 14 | 11 | `openai-codex` / `gpt-5.5` still unstable in v0.14.0 – subagents hit `APIConnectionError` / TTFB timeouts while official Codex CLI works. |
| [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) | 8 | 2 | Long-standing `openai-codex` failure on same machine/network where official CLI works (older issue, still open). |
| [#31392](https://github.com/NousResearch/hermes-agent/issues/31392) | 7 | 0 | RFC: Agent-native task relay with auto-forking subagents + async human approval gates. |
| [#33961](https://github.com/NousResearch/hermes-agent/issues/33961) | 5 | 0 | `/new`, `/clear`, `/reset` commands freeze the terminal session. |
| [#20510](https://github.com/NousResearch/hermes-agent/issues/20510) | 4 | 9 | Feature request: cloud sync for all Hermes configurations across devices. |
| [#25267](https://github.com/NousResearch/hermes-agent/issues/25267) | 4 | 13 | Feature request: Claude Agent SDK provider with subscription OAuth (Codex-style). |
| [#21910](https://github.com/NousResearch/hermes-agent/issues/21910) | 2 | 5 | Feature: rewind/edit-and-resubmit (like Claude Code’s double-Esc). |

**Underlying needs:** Users are deeply frustrated by the gap between official Codex CLI stability and Hermes’ `openai-codex` provider — a recurrent theme across two major issues. At the same time, there is strong demand for cross-device configuration sync, subscription-based Claude access (to avoid double-billing), and better session editing capabilities.

## 5. Bugs & Stability
Bugs reported or updated today (ranked by severity):

### Critical (P1)
- **[#36151](https://github.com/NousResearch/hermes-agent/issues/36151)** – `bedrock_adapter`: Opus 4.7/4.8 temperature parameter deprecated → 400 error. *No fix PR yet.*
- **[#25281](https://github.com/NousResearch/hermes-agent/issues/25281)** – Update button in dashboard deletes all scheduled cron jobs (P1, open since May 13).
- **[#34554](https://github.com/NousResearch/hermes-agent/issues/34554) *[closed]*** – `claude-opus-4-8` HTTP 400 “thinking.type.enabled” not supported. *Fixed in recent commits.*

### High (P2)
- **[#33961](https://github.com/NousResearch/hermes-agent/issues/33961)** – Slash commands `/new`, `/clear`, `/reset` freeze the terminal (Ctrl+C doesn’t recover). *No fix PR.*
- **[#36144](https://github.com/NousResearch/hermes-agent/issues/36144)** – Agent session `HOME` points to wrong path; tools look in Hermes profile instead of user’s actual home. *New today.*
- **[#36149](https://github.com/NousResearch/hermes-agent/issues/36149)** – UI cron/schedules component fails due to API endpoint mismatch (frontend calls `/api/cron/jobs`, backend defines `/api/jobs`). *New today.*
- **[#36108](https://github.com/NousResearch/hermes-agent/issues/36108)** – Discord gateway adapter not registered for non-default profiles (open since May 31).
- **[#35835](https://github.com/NousResearch/hermes-agent/issues/35835)** – `hermes update` doesn’t work inside Docker containers.
- **[#36091](https://github.com/NousResearch/hermes-agent/issues/36091)** – `minimax-oauth` auxiliary client returns raw Anthropic SDK instead of wrapper (open since May 31).
- **[#32049](https://github.com/NousResearch/hermes-agent/issues/32049)** – Docker terminal backend lets file tools write to sandbox mirror of authoritative profile state (follow-up to #31290).
- **[#31263](https://github.com/NousResearch/hermes-agent/issues/31263)** – Holographic memory context injection never fires (v0.14.0).
- **[#29066](https://github.com/NousResearch/hermes-agent/issues/29066) *[closed]*** – Local multimodal/vision failure with LM Studio. *Fixed.*
- **[#13834](https://github.com/NousResearch/hermes-agent/issues/13834)** – `openai-codex` fails while official CLI works (open since April 22, P2).
- **Fix PRs live today:** [#36199](https://github.com/NousResearch/hermes-agent/pull/36199) (persist context_length after `/model` switch), [#36193](https://github.com/NousResearch/hermes-agent/pull/36193) (tolerate inaccessible cwd during cleanup), [#36187](https://github.com/NousResearch/hermes-agent/pull/36187) (defer background review during TUI turns), [#36200](https://github.com/NousResearch/hermes-agent/pull/36200) (translate MSYS/WSL/Cygwin drive paths on Windows), [#36194](https://github.com/NousResearch/hermes-agent/pull/36194) (apply gateway lifecycle block to cronjob tool), [#36188](https://github.com/NousResearch/hermes-agent/pull/36188) (clean gateway restart flow), [#36186](https://github.com/NousResearch/hermes-agent/pull/36186) (keep clarify prompts visible when embeds hidden), [#36197](https://github.com/NousResearch/hermes-agent/pull/36197) (preserve video media intake order for Feishu).

## 6. Feature Requests & Roadmap Signals
Notable feature proposals with sustained community support:

| Issue | 👍 | Description |
|-------|----|-------------|
| [#25267](https://github.com/NousResearch/hermes-agent/issues/25267) | 13 | Claude Agent SDK provider with subscription OAuth (avoid double-billing). |
| [#20510](https://github.com/NousResearch/hermes-agent/issues/20510) | 9 | Cloud sync for Hermes configurations across devices. |
| [#21910](https://github.com/NousResearch/hermes-agent/issues/21910) | 5 | Rewind/edit-and-resubmit (Claude Code double-Esc equivalent). |
| [#31392](https://github.com/NousResearch/hermes-agent/issues/31392) | 0 (RFC) | Agent-native task relay with auto-forking subagents + human approval gates (detailed proposal). |
| [#11911](https://github.com/NousResearch/hermes-agent/issues/11911) | 0 | Native mobile app (iOS & Android) with voice calling. |
| [#20622](https://github.com/NousResearch/hermes-agent/issues/20622) | 0 | Multi-profile dashboard — surface cron jobs across all profiles. |
| [#27877](https://github.com/NousResearch/hermes-agent/issues/27877) | 0 | Add `enabled` toggle for auxiliary tasks (e.g., title generation). |
| [#36113](https://github.com/NousResearch/hermes-agent/issues/36113) | 0 | Add `categories` parameter to `web_search_tool`. |

**Prediction:** Given the momentum, **Claude OAuth support** (#25267) and **cloud sync** (#20510) are strong candidates for the next minor release (v0.15.0). The subagent relay RFC (#31392) may land as an experimental feature if maintainers accept the design.

## 7. User Feedback Summary
**Pain points highlighted by users:**
- Repeated `openai-codex` instability across Windows/macOS – official Codex CLI works while Hermes fails, causing workflow breaks.
- Terminal freezing on basic slash commands (`/new`, `/clear`, `/reset`) – no recovery except killing the process.
- Slack integration cannot open DMs by username – only existing conversation IDs work.
- Cron jobs silently deleted when using the “Update Hermes” dashboard button.
- Auxiliary task failures (e.g., title generation) cannot be disabled individually – forces a full config change.
- Docker container users cannot run `hermes update` – have to rebuild images.
- Non-default Discord gateway adapter fails to load after updates.

**Satisfaction signals:** Users actively proposing detailed RFCs (subagent relay, cloud sync) and submitting PRs (architecture diagram skill, Feishu improvements) indicate a committed power-user base. The quick closure of several P1/P2 bugs (Claude Opus thinking schema, canonical dispatcher wedge) also suggests maintainer responsiveness.

## 8. Backlog Watch
Issues and PRs that have gone unanswered or need maintainer attention:

| Issue/PR | Opened | Age | Priority | Status |
|----------|--------|-----|----------|--------|
| [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) – `openai-codex` failure | 2026-04-22 | 40 days | P2 | Open, no update since May 25. Duplicate nature of #33075 (closed) suggests a root cause exists but not fully fixed. |
| [#11911](https://github.com/NousResearch/hermes-agent/issues/11911) – Native mobile app | 2026-04-18 | 44 days | P3 | Open, no maintainer response. |
| [#13142](https://github.com/NousResearch/hermes-agent/issues/13142) – `execute_code` returns 0 tool calls on Docker | 2026-04-20 | 42 days | P2 | Open, workaround known but no fix. |
| [#19236](https://github.com/NousResearch/hermes-agent/issues/19236) – Slack DM cannot open conversation | 2026-05-03 | 29 days | P2 | Open, no triage. |
| [#21910](https://github.com/NousResearch/hermes-agent/issues/21910) – Rewind feature | 2026-05-08 | 24 days | P3 | Open, 5👍, no maintainer comment. |
| [#22064 PR](https://github.com/NousResearch/hermes-agent/pull/22064) – Fix sweep task leak on startup | 2026-05-08 | 24 days | P2 | Open, no review activity. |
| [#20510](https://github.com/NousResearch/hermes-agent/issues/20510) – Cloud sync | 2026-05-06 | 26 days | P3 | Open, 9👍, no official response. |
| [#

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-01

## 1. Today’s Overview
The project shows sustained activity with 7 issues and 10 PRs updated in the last 24 hours, including one new nightly release. The team merged/closed 3 PRs and 3 issues, highlighting progress on a long-standing Codex OAuth empty‑response bug and the first iteration of media‑aware outbound messaging. A new nightly build (v0.2.9‑nightly) was published, though it is marked as potentially unstable. Overall, the project is healthy with active community contributions and maintainer responsiveness.

---

## 2. Releases

| Version | Notes |
|---------|-------|
| **nightly** (v0.2.9-nightly.20260601.ba806592) | Automated nightly build. **May be unstable.** Full changelog: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main) |

No breaking changes or migration notes have been provided. Users should test before deploying in production.

---

## 3. Project Progress (Merged/Closed PRs Today)

Three PRs were merged or closed in the last 24 hours:

- **#2967** – [fix(codex): preserve streamed output text deltas](https://github.com/sipeed/picoclaw/pull/2967)  
  Closes the empty‑response bug when using the OpenAI Codex OAuth provider. The fix accumulates `output_text.delta` events even when the final `response.completed` payload contains `null` for `response.output`.

- **#2856** – [feat(message): support media attachments and Telegram rich delivery](https://github.com/sipeed/picoclaw/pull/2856)  
  Implements feature request #2855. The `message` tool now supports a single outbound payload with both text and media, eliminating the need for agents to split sends across separate channels.

- **#2980** – [chore: gitignore debug output files](https://github.com/sipeed/picoclaw/pull/2980)  
  Housekeeping to ignore local debug artifacts.

---

## 4. Community Hot Topics

The most active discussions (by comments and reactions) are:

- **#28** – [Feat Request: LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28)  
  *Comments: 21, 👍: 2* – Closed today after months of discussion. The user requested a simplified way to connect PicoClaw to LM Studio. While closed, it signals ongoing interest in local model providers.

- **#2674** – [Codex OAuth: empty assistant response](https://github.com/sipeed/picoclaw/issues/2674)  
  *Comments: 7, 👍: 4* – Open but now has a fix (PR #2967). Community members actively identified that the ChatGPT Codex backend emits non‑standard streaming events. The underlying need is reliable integration with OpenAI’s official and third‑party endpoints.

---

## 5. Bugs & Stability

| Issue | Severity | Summary | Fix Exists? |
|-------|----------|---------|-------------|
| [#2674](https://github.com/sipeed/picoclaw/issues/2674) (open) | **High** | OpenAI Codex OAuth returns empty responses because `response.output_text.delta` stream events are ignored. Affects all ChatGPT‑backend users. | Yes – PR #2967 merged today |
| [#2968](https://github.com/sipeed/picoclaw/issues/2968) (open) | **Medium** | `/context` always displays “Compress at: 76800 tokens” regardless of actual context size. Occurs with MiniMax providers on FreeBSD. | No PR yet |
| [#2952](https://github.com/sipeed/picoclaw/issues/2952) (open) | **Low** | User reports three separate issues: `exec` command missing default action; QQ channel restart loop; model interface not showing saved key providers. No clear reproducer for each. | No |

The most critical bug (Codex empty response) has been fixed and will be included in the next stable release.

---

## 6. Feature Requests & Roadmap Signals

Several feature requests have been submitted or advanced in the last 24 hours, indicating likely roadmap candidates:

- **Easy LM Studio Connect** (closed #28) – Though closed, the demand for simplified local provider setup persists. Maintainers may revisit with a configuration wizard or auto‑detect.
- **OmniRoute as provider** (#2978) – New request to add the OmniRoute proxy as a provider. The user also asked how to add custom combos via configuration.
- **Cron tool `get`/`update` actions** (PR #2977) – Open PR adds inspection and partial updates for cron jobs, preventing full remove‑recreate cycles. Likely to land in next nightly.
- **Telegram reply‑as‑mention** (PR #2975) – Treats replying to a bot message as a mention in group chats. Already open and active.
- **Android Termux guide** (PR #2902) – Documentation for running PicoClaw on ARM64 Android devices. Shows growing mobile interest.
- **Skill binary dependency filtering** (PR #2936) – Skips skills whose `requires.bins` binaries are not on PATH, preventing unusable tool advertisements.

**Predictions for next version (v0.3.0):** Media‑aware messaging, Telegram reply‑as‑mention, cron tool improvements, and the Codex fix are all strong candidates. The LM Studio feature may be revisited after the current nightly stabilises.

---

## 7. User Feedback Summary

- **Pain points**  
  - Codex OAuth empty responses – multiple users with 4 👍 on #2674 and a separate issue #2953. Fixed today.
  - `/context` showing constant token count (#2968) – confuses users about actual compression.
  - Model interface ignoring saved provider keys (#2952) – forces repetitive re‑entry.
  - QQ channel restart loop (#2952) – destroys bot state after restart.
  - Request for LM Studio integration (#28) – shows desire for local LLM workflows.

- **Satisfaction signals**  
  - The media‑attachment message tool (#2856) directly addresses a long‑standing workflow pain point.
  - Nightly builds provide early access to fixes, e.g., the Codex patch.

- **Use cases**  
  - Multi‑platform agent bots (Telegram, QQ, Web).
  - Local model experimentation (MiniMax, LM Studio).
  - Android Termux deployment (new guide PR).
  - Scheduled tasks via cron tool enhancements.

---

## 8. Backlog Watch

The following items require maintainer attention due to age or lack of response:

- **#2952** – User report with three bugs (exec, QQ restart, model UI). Created 2026-05-27, updated 2026-05-31 but no maintainer comment. Needs triage and reproduction steps.
- **#2936** – PR [feat(skills): skip skills with missing binaries](https://github.com/sipeed/picoclaw/pull/2936) – Open since 2026-05-24, marked stale. Awaiting review and merge.
- **#2906** – PR [Fix message bus backpressure handling](https://github.com/sipeed/picoclaw/pull/2906) – Open since 2026-05-20, stale. Critical for runtime stability but lacks maintainer feedback.
- **#2904** – PR [Fix agent loop reload and panic cleanup](https://github.com/sipeed/picoclaw/pull/2904) – Same author, same staleness. Addresses goroutine leaks.
- **#2902** – PR [docs: add Android Termux guide](https://github.com/sipeed/picoclaw/pull/2902) – Documentation improvement, open since 2026-05-20, stale but low risk.

These items are not blocked by technical issues but need maintainer bandwidth for review and merge.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-01

## Today's Overview
The NanoClaw project saw moderate activity in the last 24 hours with 3 new open issues and 8 pull requests (2 merged/closed, 6 open). No new releases were published. Activity is concentrated on critical reliability fixes (host freeze, file descriptor exhaustion) and infrastructure enhancements (HTTP/SSE MCP support, per‑group skill wiring). The high number of open PRs suggests a focused development sprint, while three unaddressed high‑severity issues indicate stability gaps that need maintainer attention.

## Releases
*None.*

---

## Project Progress
Two pull requests were merged/closed today:

- **#2648** – *feat: add `/upload-trace` command to upload session trace to Hugging Face* (merged)  
  Adds a new utility skill that lets users upload Claude Code session traces directly to Hugging Face for sharing or debugging.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2648)

- **#2658** – *Actual deployment* (merged)  
  A contribution that improves the deployment process, likely fixing configuration or container orchestration issues.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2658)

---

## Community Hot Topics
*No issues or PRs received comments or reactions in the last 24 hours.* The discussions remain technical and low‑volume.

**Most impactful open issues** (by severity, not by activity):

- **#2665** – *Single-threaded host can be frozen by unbounded/synchronous ops* – describes a design flaw where blocking calls on the Node.js event loop freeze the entire host and render `/health` unresponsive.  
  [GitHub](https://github.com/nanocoai/nanoclaw/issues/2665)

- **#2655** – *OneCLI gateway hard‑exits on fd exhaustion (1024 soft limit)* – a production outage risk under burst load.  
  [GitHub](https://github.com/nanocoai/nanoclaw/issues/2655)

- **#2657** – *Self‑healing: supervise the OneCLI gateway dependency + fail‑fast agent containers on connection loss* – highlights a lack of automated failure recovery.  
  [GitHub](https://github.com/nanocoai/nanoclaw/issues/2657)

These three issues were all created on 2026‑05‑31 and share a common theme: the system has good failure **detection** but weak **reaction**. They represent core reliability pain points.

---

## Bugs & Stability
Three new bugs were reported, all opened on 2026‑05‑31:

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| #2665 | **Critical** | Single‑threaded host freezes due to unbounded `await` or sync blocking; `/health` becomes unresponsive. | No |
| #2655 | **High** | OneCLI gateway hard‑exits with `os error 24` under burst load due to default 1024 file‑descriptor soft limit, causing total agent outage. | No |
| #2657 | **Medium** | Lack of self‑healing: failed agent containers and dead OneCLI processes remain unresolved after detection. | No (but related PR #2659 addresses container reaping) |

**Additional stability fixes in open PRs:**

- **#2659** – *fix: reap containers via host PID when daemon refuses to stop them* – addresses orphan container leaks on unprivileged hosts.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2659)

- **#2656** – *fix(add‑mnemon): run mnemon setup in index.ts main(), not entrypoint.sh* – fixes a configuration bug where a skill’s setup never executed inside the container.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2656)

No regressions were reported.

---

## Feature Requests & Roadmap Signals
Several open PRs indicate upcoming features and architectural improvements:

- **HTTP/SSE MCP server support** (PR #2662) – extends `McpServerConfig` to accept HTTP and SSE transports, enabling remote MCP servers. Likely to land in the next patch or minor release.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2662)

- **Per‑group skills as slash commands** (PR #2661) – wires group‑specific skills into Claude Code’s slash command discovery. A usability enhancement for multi‑agent setups.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2661)

- **Mount external symlink targets for per‑group skills** (PR #2660) – fixes a limitation preventing symlinked skills from working inside containers. Essential for shared skill libraries.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2660)

- **Browser scraping sidecar** (PR #2664) – runs `cf-fetch`/`nodriver` inside the v2 container, with additional skill integrations (Web fetch, NotebookLM, Mer audio, Paris rental). Suggests a push toward richer autonomous browsing abilities.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2664)

Predicted next‑version inclusions: MCP transport expansion, per‑group skill improvements, and the browser sidecar.

---

## User Feedback Summary
No explicit user comments or reactions were recorded in the last 24 hours. However, the three open issues reveal concrete pain points:

- **Host freeze under heavy operations** (#2665): users expect `/health` to always respond, even under load.
- **Abrupt agent outages under burst traffic** (#2655): fd exhaustion leads to silent total failure, indicating production scaling limitations.
- **Lack of automated recovery** (#2657): manual intervention is required to restart failed components, causing frustration in long‑running deployments.

Satisfaction appears moderate: the community is actively contributing fixes (6 open PRs), but critical reliability issues have not yet been addressed by maintainers.

---

## Backlog Watch
All three open issues (#2655, #2657, #2665) were created on 2026‑05‑31 and have **zero comments** or maintainer responses. They are high‑severity and have no associated fix PRs yet. These should be prioritized for triage to prevent build‑up of unresolved reliability debt.

No old unanswered PRs or issues were identified in the provided data.

---

*Generated from GitHub activity on nanocoai/nanoclaw, updated 2026‑06‑01.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-01

## Today’s Overview
Project activity remains low, with no releases, no pull requests, and only two newly opened issues in the last 24 hours. Both issues were created by the same contributor (weissfl) and describe distinct bugs in the Telegram integration. No closed issues or merged PRs were recorded, indicating a quiet period without active code changes. The overall project health appears stable but with a slight uptick in user-reported problems.

## Releases
*None.* No new versions were published in the reporting period.

## Project Progress
No pull requests were merged, closed, or opened today. No code changes or feature advancements were recorded.

## Community Hot Topics
The only active discussions are the two issues opened yesterday. Neither has received comments or reactions yet, but both represent the most (and only) current community engagement.

- **[#942 – Telegram: missing typing indicator when pressing inline buttons](https://github.com/nullclaw/nullclaw/issues/942)**  
  User `weissfl` reports that the “typing…” indicator does not appear when interacting with inline buttons (e.g., `nc_choices`), while it works correctly for regular text messages. This is a UX inconsistency that affects user feedback during processing.

- **[#941 – Agent‑type cron jobs don't spawn a subprocess — Telegram delivery never happens](https://github.com/nullclaw/nullclaw/issues/941)**  
  Scheduled tasks with `job_type: "agent"` and proper delivery configuration (`delivery_mode: "always"`, `delivery_channel: "telegram"`) are marked as completed but the agent subprocess never starts, resulting in no Telegram message delivery. This is a functional regression.

## Bugs & Stability

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#941](https://github.com/nullclaw/nullclaw/issues/941) | **High** | Agent‑type cron jobs fail to start subprocess; Telegram delivery never occurs. Core scheduling functionality is broken for this job type. | None |
| [#942](https://github.com/nullclaw/nullclaw/issues/942) | **Medium** | Missing “typing…” indicator for inline button interactions. Affects user experience but does not prevent message delivery. | None |

No fix pull requests have been submitted for either issue.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, issue [#942](https://github.com/nullclaw/nullclaw/issues/942) implies a desire for consistent UX feedback across all interaction methods (inline buttons vs. text messages). This could be a candidate for a minor UI enhancement in the next release if the development team prioritises Telegram polish.

## User Feedback Summary
The sole reporter, `weissfl`, is encountering two distinct pain points:
- **Telegram inline button interactions lack visual feedback** – leads to uncertainty whether the bot is processing.
- **Agent cron jobs do not execute at all** – complete failure of a scheduled delivery mechanism, likely causing missed notifications.

The user’s issues indicate dissatisfaction with reliability and consistency in the Telegram module. No positive or satisfaction signals were recorded.

## Backlog Watch
No longstanding unanswered issues or pull requests are present in the current data. Both issues were created on 2026-05-31 and have not yet received any maintainer response. Prompt acknowledgment and triage would be advisable to prevent backlog buildup.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-01

**Repository**: [github.com/nearai/ironclaw](https://github.com/nearai/ironclaw)  
**Generated**: 2026-06-01  

---

## 1. Today’s Overview

The IronClaw project saw **high activity** over the past 24 hours, with **25 PRs updated** (7 merged/closed, 18 open) and **3 issues updated** (2 open, 1 closed). No new releases were published. The majority of merged PRs advanced the **“Reborn” architecture**, including a libSQL trigger repository backend, an outbound communication resolution engine, and WebUI v2 OAuth card integration. Concurrently, dependency upgrades (46 packages in one PR) and a nightly E2E pipeline failure indicate active maintenance and ongoing regression tracking. The most contentious open issue remains a **stdio MCP activation bug** (#2923) that was prematurely closed in a previous cycle and has been re-opened for investigation.

---

## 2. Releases

*None.* No new releases were created today.

---

## 3. Project Progress (Merged/Closed PRs)

Seven pull requests were merged or closed in the last 24 hours (5 fully merged, 2 dependency bumps that were closed in favor of newer versions). Significant merged items include:

- **`#4263` (closed/merged)** — feat(triggers): add libSQL repository  
  First durable `TriggerRepository` backend for Reborn triggers. Implements trigger persistence inside `ironclaw_triggers` without wiring the poller or composition lifecycle. [PR #4263](https://github.com/nearai/ironclaw/pull/4263)

- **`#4262` (closed/merged)** — feat(outbound): add resolution engine  
  P0 outbound communication resolution engine inside `ironclaw_outbound`. Handles candidate selection (typed `CommunicationDeliveryCandidate` or `NoDelivery`), intentionally excluding validation and rendering. [PR #4262](https://github.com/nearai/ironclaw/pull/4262)

- **`#4257` (closed/merged)** — feat(reborn): wire AuthPromptView challenge enrichment + WebUI OAuth card  
  Implements Rust wire-shape changes and WebUI v2 components for GSuite OAuth, Notion MCP OAuth, and GitHub PAT auth flows. [PR #4257](https://github.com/nearai/ironclaw/pull/4257)

- **`#4033` (closed/merged)** — chore(deps): bump the everything-else group (45 updates)  
  Dependency upgrades including `agent-client-protocol`, `postgres-types`, and many others. [PR #4033](https://github.com/nearai/ironclaw/pull/4033)

- **`#4000` (closed/merged)** — chore(deps): bump serde_json to 1.0.150  
  [PR #4000](https://github.com/nearai/ironclaw/pull/4000)

Two additional dependency PRs (likely #4033 replacement and a serialization group bump) were also closed. Merged work strongly focuses on the **Reborn refactor** (triggers, outbound, product-auth) and dependency hygiene.

---

## 4. Community Hot Topics

The most active discussion centers on a **bug re-report** regarding stdio MCP activation. No PRs had comment counts reported, but several large changes attracted reviewer attention.

### Most active issue
- **#2923 ([OPEN] Bug: stdio MCP activation fails)**  
  *4 comments, 1 thumbs-up*  
  Re-opened version of #2474. The reporter (rajulbhatnagar) clarifies that stdio transport **is** wired end-to-end in v0.25.0, but the activation pre-flight fails with “Failed to discover authorization endpoints.” The issue highlights confusion around maintainer triage—previously closed based on a non-maintainer claim.  
  [Issue #2923](https://github.com/nearai/ironclaw/issues/2923)

### High-impact open PRs with significant scope
- **#4035** — feat(slack): add Reborn ProductAdapter core (XL, risk: medium)  
  First reviewable Slack Reborn boundary slice; establishes adapter crate, inbound normalization, outbound reply rendering.  
  [PR #4035](https://github.com/nearai/ironclaw/pull/4035)

- **#4270** — feat(triggers): add postgres repository parity (L, risk: low)  
  Second durable trigger backend, mirroring the libSQL repository.  
  [PR #4270](https://github.com/nearai/ironclaw/pull/4270)

- **#4280 (not listed but inferred)** — several large product-auth PRs (#4269, #4239, #4184) continue the “Reborn” migration of credential and OAuth flow logic.

---

## 5. Bugs & Stability

Two notable stability concerns were raised or updated today:

| Issue | Severity | Description | Fix PR? | Status |
|-------|----------|-------------|---------|--------|
| #2923 | **High** | stdio MCP activation fails due to pre-flight OAuth discovery. Affects v0.25.0 despite transport support. | None linked | Open since Apr 24; re-opened May 31 |
| #4108 | **Medium** | Nightly E2E scheduled run failed (Full E2E / extensions). Commit 749f584. | None | Open; no comments from maintainers |

**#4108** is a recurring nightly failure. The specific job “E2E (extensions)” is failing, indicating a potential regression in the extensions integration test suite. No immediate fix PR has been opened.

**#2923** remains the most impactful reported bug. Its premature closure in a prior cycle has eroded user confidence in maintainer triage. The reporter explicitly requests a re-open and re-test. A maintainer comment or fix is overdue.

---

## 6. Feature Requests & Roadmap Signals

Based on today’s merged PRs and active open work, the following features appear likely for the next release (presumably v0.26.0 or v0.25.1):

- **Slack as a Reborn product adapter** (#4035, #4272) — Host ingress for Slack Events API and ProductAdapter core. Expected to ship with Webhook runner wiring.
- **Durable triggers** (#4263, #4270) — Both libSQL and Postgres backends are now functional; the poller and lifecycle wiring are next.
- **Outbound resolution engine** (#4262) — Candidate selection for communication delivery; will receive validation (PR #4271) and rendering in subsequent phases.
- **WebUI v2 authentication overhaul** (#4257, #4239, #4269) — Migration to typed auth-flow, secret broker, and provider-agnostic OAuth cards. GitHub SSO is pending (#4229).
- **Unified diff display previews** (#4184) — For `write_file` and `apply_patch` capabilities, visible in WebUI v2.

The “Reborn” label dominates the PR titles. After several months of refactoring, the project appears close to integrating multiple new product adapters and trigger systems. No minor version release has been tagged this cycle, but the volume of merged XL changes suggests a release candidate may be imminent.

---

## 7. User Feedback Summary

Direct user feedback is sparse, but one clear pain point emerges:

- **#2923** — A user reports that stdio MCP activation is broken in v0.25.0, and the bug was dismissed incorrectly by a non-maintainer. The user expresses frustration: “Stdio **is** wired end-to-end … the bug is strictly in the activation pre-flight.” This indicates that the MCP transport feature is desired but the activation flow needs a fix. Users likely rely on stdio for local tool integration.

Beyond this, no other user-reported issues were updated today. The nightly E2E failure (#4108) signals potential regressions that may not yet have been visible to end users.

---

## 8. Backlog Watch

The following issues or PRs require maintainer attention:

- **#2923 (Bug: stdio MCP activation)** — Open since April 24, re-opened May 31. No maintainer comment or fix PR. Priority should be high as it blocks a core MCP workflow.  
  [Issue #2923](https://github.com/nearai/ironclaw/issues/2923)

- **#4108 (Nightly E2E failure)** — No comments, no fix. The extensions job is failing consistently. A triage or temporary disable is needed.  
  [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

- **Flaky dependency PRs** — Multiple open Dependabot PRs (#4002, #4001, #4032, #4267, #4268) have been open without merge for 1–2 weeks. While low risk, long-lived dependency updates can lead to merge conflicts and missed security patches.

- **#4229 (GitHub SSO)** — Open since May 29, no maintainer activity. This is a requested user feature (native GitHub OAuth for WebChat v2) and could be bundled with the upcoming WebUI v2 release.

---

**Overall health**: Active development, but bug triage and release management remain weak points. The Reborn refactor is making measurable progress, yet the project has not shipped a new release since v0.25.0, while blocking bugs persist. Attention to the stdio MCP bug and nightly pipeline stability would improve contributor and user confidence.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI Project Digest – 2026-06-01

### 1. Today's Overview
Project activity remained very low on June 1, with no new issues or releases. One pull request (#2080) was merged, covering a general chore that touches the renderer, documentation, main, and cowork areas. Another long‑standing PR (#1465) addressing a ghost session bug in scheduled tasks is still open and marked as stale. Overall, the project appears to be in a quiet phase, with no urgent community discussions or new feature work visible.

### 2. Releases
No new releases were published today or in the recent past. No migration notes or breaking changes to report.

---

### 3. Project Progress
- **Merged PR: #2080 – `chore: optimize kits and upload file ui`**  
  Author: fisherdaddy  
  Areas: renderer, docs, main, cowork  
  This is a maintenance change aimed at improving the UI/UX around kits and file uploads. No functional changes or bug fixes were detailed.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/2080)

No other merged or closed PRs were recorded.

---

### 4. Community Hot Topics
No issues or PRs received comments or reactions in the last 24 hours. The only item with sustained attention is:
- **PR #1465** (open since April 4, updated May 31) – Fixes a bug where deleted scheduled tasks reappear as ghost sessions after restart. Although it has zero comments, the underlying issue (#1359) likely affects users who rely on scheduled tasks. The PR is currently stale and may require maintainer review to move forward.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1465)

---

### 5. Bugs & Stability
**No new bugs were reported today.**  
The only active bug‑related item is the existing ghost session issue in scheduled tasks (PR #1465). The problem is described as:
- **Severity**: Medium – users who delete a scheduled task see it reappear as an empty “ghost” session after an application restart.
- **Root cause**: The delete process only removes the task from the gateway’s cron list but does not clean up the associated local SQLite session record.
- **Status**: A fix is proposed in #1465 but has not yet been merged. The PR is stale and may need rebasing or renewed attention.

No other crashes, regressions, or stability concerns surfaced.

---

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were captured in the data today. The merged chore (#2080) hints at ongoing UI polish, possibly in response to prior user feedback on the file upload experience. No roadmap signals or new feature proposals are visible.

---

### 7. User Feedback Summary
No direct user feedback (comments, reactions) was posted today. However, the persistence of the ghost session bug (PR #1465) indicates a known pain point for users managing scheduled tasks. The frustration of repeatedly deleting tasks that reappear after restart is clearly a source of dissatisfaction. The project’s quiet state may imply either a lull in usage or that maintainers are focusing on internal work not reflected in public activity.

---

### 8. Backlog Watch
The following item requires maintainer attention:

- **PR #1465** (`fix(scheduled-tasks): ghost session on restart`) – Open since April 4, updated May 31, but now stale. No comments from maintainers or further activity. The fix is important for task reliability, yet it has been waiting over two months.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1465)

No other long‑unanswered issues or PRs were identified.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-01

## Today’s Overview
Activity on the Moltis repository has been minimal over the past 24 hours. No new issues were opened or updated, and no releases were published. A single pull request (#1089) was opened today, targeting a stability improvement for session history rehydration. The project appears to be in a quiet phase, with maintainer attention likely focused on the open PR and ongoing development.

## Releases
No new releases were recorded today. The latest available release remains unchanged.

## Project Progress
No pull requests were merged or closed today. The one new PR, **#1089**, is still open and proposes a fix to cap persisted tool and tool_result content during session rehydration. This change would affect normal chat, streaming chat, retry-after-compaction, prompt inspection, silent memory turns, and LLM-backed compaction prompts. If merged, it will reduce memory bloat and improve stability when restoring agent sessions.

## Community Hot Topics
The only activity today is **PR #1089** (“Cap persisted tool results before rehydration”), authored by s-salamatov. It has no comments or reactions yet, but its technical substance suggests a growing need to manage large session histories efficiently. The PR focuses on avoiding runaway memory consumption when tool results are rehydrated into provider-bound `ChatMessage` objects.  
🔗 [PR #1089](https://github.com/moltis-org/moltis/pull/1089)

## Bugs & Stability
No new bugs or crashes were reported today. Recent development (via the open PR) indicates that session rehydration without proper capping may have caused memory or performance issues for some users, but no bug reports were filed in the last 24 hours.

## Feature Requests & Roadmap Signals
No explicit feature requests were submitted today. The open PR hints at an ongoing effort to improve session history handling, which is a common prerequisite for longer-running agent interactions. Future releases may include more robust compaction and memory management strategies based on the patterns introduced in #1089.

## User Feedback Summary
No user feedback (comments, reactions, or issue reports) was recorded today. The absence of complaints could signal overall satisfaction, but the low activity also suggests limited community engagement over the past day.

## Backlog Watch
No long-unanswered issues or PRs were identified. The repository appears to have a clean backlog with no pending items requiring immediate maintainer attention beyond the newly opened PR #1089.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the GitHub data provided for CoPaw (github.com/agentscope-ai/CoPaw), here is the project digest for **2026-06-01**.

---

### 1. Today's Overview

Project activity remains high, with 27 issues and 9 pull requests updated in the last 24 hours, indicating a healthy and responsive development cycle. Community interaction is strong, particularly around bug reporting and feature requests, though no new release was published today. The development team is actively addressing a cluster of critical bugs related to the Cron job system and Windows shell execution, while also processing a significant number of feature requests for UI/UX improvements.

### 2. Releases

**None.** No new versions or releases were published on this date.

### 3. Project Progress

Today saw 1 pull request merged and 6 issues closed, reflecting steady progress in fixing bugs and community-driven improvements.

- **Merged/Closed PRs:**
    - **[PR #4810] feat(console): improve chat slash skill suggestions** `(Under Review -> CLOSED)` - Enhanced the console UI by adding skill suggestions to the slash-command popup, limiting the display to 5 items, and improving the user experience for activating skills in chat.
- **Closed Issues:**
    - **[#4789] [Feature] Support per-chat deletion and rollback** - A popular feature request for conversation history management was closed, likely to be addressed in a future version.
    - **[#4653] [Bug] Cron tasks interrupted by user messages** - A critical bug affecting timed task reliability was resolved.
    - **[#4649] [Bug] Orphaned cron jobs from jobs.json updates** - A related cron stability fix was also closed.
    - **[#4833] [Bug] 'Failed to compact memory' error** - A code-level bug causing session crashes was fixed.
    - **[#4828] [Bug] Windows CMD window flash on shell execution** - A duplicate of a known Windows UX bug.
    - **[#4829] [Bug] Windows CMD window flash on shell execution** - The main report for this severe UX bug was closed. Fixes are present in open PRs.

### 4. Community Hot Topics

The community is most engaged with features that enhance usability and system stability, with several issues generating significant discussion.

- **Most Active:**
    - **[Issue #4789]** *"I hope qwenpaw can also, like trae, delete and rollback to each conversation..."* **(8 Comments, 1 👍)** - This is a top priority for the community. Users want greater control over the conversation context, mirroring features in competitor products like Trae. The core request is for granular, file-aware session management.
    - **[Issue #4653]** *"Cron tasks interrupted by user messages"* **(8 Comments)** - High engagement signals that this is a common pain point for users relying on automation features.

- **Analyzing Underlying Needs:**
    - **Context Management:** The desire for per-chat deletion/rollback ([#4789](agentscope-ai/QwenPaw Issue #4789)) and the "Interrupt, Queue, Insert" modes ([#4843](agentscope-ai/QwenPaw Issue #4843)) show a deep need for more sophisticated, user-controlled management of the agent's context window and execution flow.
    - **Cron Reliability:** The cluster of issues around cron jobs ([#4653](agentscope-ai/QwenPaw Issue #4653), [#4649](agentscope-ai/QwenPaw Issue #4649), [#4835](agentscope-ai/QwenPaw Issue #4835)) indicates that automation is a critical feature for users, but the current implementation is fragile and requires hardening.

### 5. Bugs & Stability

A significant number of bugs were reported today, with a strong focus on Windows platform stability and the Cron system. Several fix PRs are already in the pipeline.

#### Critical / High Severity:

- **[#4837] System Fallback Message ("unable to process")** - A severe regression in v1.1.9 where the system incorrectly blocks valid agent responses. *(No fix PR yet, high priority)*
- **[#4835] Invalid Cron Job Crashes Entire Workspace** - Single validation error leads to total service failure. *(No fix PR yet)*
- **[#4653] Cron Tasks Interrupted by User Messages** - Software behavior can lead to data loss or incomplete automation. *(Closed, fix implemented)*

#### Medium Severity:

- **[#4829] / [#4832] Windows CMD Window Flash** - A severe UX issue that triggers a visible, flashing CMD window for every shell command. *(Fix PR: #4829 is closed, likely resolved)*
- **[#4666] Models Configuration Lost on New Session** - A significant configuration management bug requiring a full restart to recover. *(No fix PR yet)*
- **[#4833] Memory Compaction Crash** - A core session crash triggered by a specific message format. *(Closed, fix implemented)*
- **[#4818] Cron Agent 'share_session=true' Produces Empty Traces** - Cron tasks fail silently, providing a false "success" status. *(Fix PR: #4822 is open)*
- **[#4844] Browser Process & Temp Locks on Windows** - Processes remain after sessions, causing cascading failures in backups. *(No fix PR yet)*
- **[#4834] MCP Server Processes Accumulate on Restart** - Leads to resource exhaustion and slow console loading. *(No fix PR yet)*

### 6. Feature Requests & Roadmap Signals

User feature requests are concentrated on enhancing the desktop experience and providing more granular control over the agent's behavior. These requests are likely to shape the next minor release (v1.2.0).

- **Highly Likely for Next Version:**
    - **Conversation Rollback/Deletion ([#4789](agentscope-ai/QwenPaw Issue #4789)):** The most popular feature request. Given the community demand and the prototype-like solutions available, a formal implementation is a strong candidate.
    - **Configurable Chat Modes (Interrupt/Queue/Insert) ([#4843](agentscope-ai/QwenPaw Issue #4843)):** A logical next step for managing concurrent conversations, directly addressing the "Interrupt" mode that currently causes problems.
    - **Thinking Effort Level Selector ([#4840](agentscope-ai/QwenPaw Issue #4840)):** A UI-focused feature that is relatively low-risk and high-impact for user experience, following patterns seen in other platforms.

- **Lower Probability but Significant:**
    - **Token Usage Display ([PR #4433](agentscope-ai/QwenPaw PR #4433)):** This PR has been under review for over two weeks, suggesting it may require significant changes or has been deprioritized for internal testing.
    - **On-Demand Tool Loading ([#4836](agentscope-ai/QwenPaw Issue #4836)):** A major architectural change that would efficiently reduce token consumption but is complex to implement.

### 7. User Feedback Summary

- **Pain Points:**
    - **Windows UX:** Users are highly frustrated by the CMD window flash issue ([#4829](agentscope-ai/QwenPaw Issue #4829), [#4832](agentscope-ai/QwenPaw Issue #4832)), which severely degrades the Desktop experience.
    - **System Stability:** Users on v1.1.9 report a new and frequent "system fallback" error that blocks legitimate requests, causing significant confusion ([#4837](agentscope-ai/QwenPaw Issue #4837)).
    - **Configuration Management:** The loss of model configuration on new sessions ([#4666](agentscope-ai/QwenPaw Issue #4666)) and the fragility of the cron job system ([#4835](agentscope-ai/QwenPaw Issue #4835]) are major usability barriers.

- **Use Cases:**
    - **Automation & Scheduling:** A large number of issues originate from users relying on QwenPaw for timed automations (cron jobs), including data scraping and task reminders. This is a core user persona.
    - **Development Tool:** Users are integrating QwenPaw with coding tools like Claude Code ([#4824](agentscope-ai/QwenPaw Issue #4824)), indicating a developer-centric use case for code generation and review.

- **Sentiment:**
    - The community is highly engaged, but also clearly reporting a significant number of regressions. The sentiment is a mix of excitement for new features and frustration with recent stability issues, especially on Windows.

### 8. Backlog Watch

The following issues and PRs have not been recently updated by maintainers, potentially stalling progress or causing user frustration.

- **[PR #4433] Add token usage info output in each conversation** *(Last update: 2026-05-15)* - A highly requested feature that has been under review for over two weeks without clear progress or feedback on the next steps.
- **[Issue #4808] Agent [person_stat_skill] not exists** *(Created: 2026-05-29)* - This is a user-facing help request that may indicate a documentation gap or a bug in the Skill loading mechanism. It lacks a final confirmation or solution from maintainers.
- **[Issue #4845] WeWork channel lacks memory isolation** *(Created: 2026-06-01)* - A security-relevant issue reporting a potential privacy leak in the enterprise WeChat channel. It has received no comments from maintainers and requires urgent triage.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest – 2026-06-01

## Today's Overview
The ZeptoClaw project had minimal activity in the last 24 hours. One issue was closed, and no pull requests or new releases were recorded. The closed issue (#609) involved a repository‑wide Codex security scan, indicating ongoing security hygiene work rather than feature development or bug fixing. Overall, the project appears to be in a quiet maintenance phase with no urgent community or development signals.

## Releases
No new releases were published in the last 24 hours.

## Project Progress
No pull requests were merged or closed today. No feature advancements or fixes were recorded.

## Community Hot Topics
The only issue updated in the last 24 hours is **#609 [CLOSED] – chore(security): repository-wide Codex Security scan for webhook identity routing** ([link](https://github.com/qhkm/zeptoclaw/issues/609)).  
- **Author:** daneschneider-oai  
- **Comments:** 1  
- **Reactions:** 0  
- **Summary:** The issue requested a repository‑wide Codex security scan focusing on the webhook request identity flow through admission and routing. It was closed after the scan was presumably completed.  
- **Analysis:** This was an internal operational task rather than a user‑driven discussion. No significant community engagement was observed.

## Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The only closed issue was a proactive security scan, not a defect. Project stability appears unchanged.

## Feature Requests & Roadmap Signals
No feature requests were submitted or discussed in the last 24 hours. No roadmap signals can be inferred from the available data.

## User Feedback Summary
No user feedback, pain points, or satisfaction/dissatisfaction signals were recorded. The project saw no new user interactions beyond the automated security scan issue.

## Backlog Watch
There are no long‑unanswered or stale issues or pull requests requiring maintainer attention in the data provided. The project backlog is currently clean.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – June 1, 2026

## 1. Today's Overview
ZeroClaw remains highly active with **43 issues** and **50 pull requests** updated in the last 24 hours. Of these, 12 issues were closed and 10 PRs were merged or closed. No new releases were published today, but a major integration PR (#6848) for the `zerocode` TUI and v0.8.0-beta-2 is open for first-round feedback. The community continues to push for security, multi-tenancy, and hardware support, while maintainer bandwidth appears stretched, with several enhancement PRs marked `needs-maintainer-review`.

## 2. Releases
*No new releases today.* The last tagged release remains v0.8.0-beta-1 (as referenced in issues).

## 3. Project Progress
**Merged/Closed PRs (last 24h):**
- [#7044 – refactor(cargo): extract channels-all aggregate feature](https://github.com/zeroclaw-labs/zeroclaw/pull/7044) (closed) – Simplifies feature flags for channel support.
- [#7029 – fix(zerocode): refresh empty states after setup](https://github.com/zeroclaw-labs/zeroclaw/pull/7029) (closed) – Fixes a TUI usability issue where empty states were not cleared after initial setup.

**Notable closed issues (high-activity, now resolved):**
- [#6647 – Cron job output not routed to configured channels](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) (S1, closed) – A critical bug that prevented scheduled task results from reaching Telegram/other channels.
- [#5847 – Document use of `gateway.web_dist_dir`](https://github.com/zeroclaw-labs/zeroclaw/issues/5847) – Documentation gap resolved.
- [#6883 – RFC: Shared reply-message constructor on SendMessage](https://github.com/zeroclaw-labs/zeroclaw/issues/6883) – Routing improvement accepted and merged.
- [#5289 – Bedrock provider sends API_KEY causing 403](https://github.com/zeroclaw-labs/zeroclaw/issues/5289) – Authentication fix for AWS Bedrock.
- [#5731 – Add manifest as a provider](https://github.com/zeroclaw-labs/zeroclaw/issues/5731) – Feature implemented.

**Other progress signals:**
- Multiple PRs by @Rhoahndur and @mov-xound-glitch are advancing hardware simulation, TTS transcoding (OGG/Opus), email XOAUTH2, and output modality preferences (see next sections).

## 4. Community Hot Topics
**Most active issues (by comment count):**
- [#5937 – [Feature]: refactor: Unify providers architecture and reqwest client management](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) (9 comments, still open) – Calls for a major refactoring of the providers module to reduce duplication and standardise configuration. High risk/priority.
- [#5982 – Per-sender RBAC for multi-tenant agent deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) (8 comments, open) – Request for role-based access control, reflecting growing enterprise adoption.
- [#5847 – Document the use of `gateway.web_dist_dir`](https://github.com/zeroclaw-labs/zeroclaw/issues/5847) (8 comments, closed) – High user need for clear documentation.
- [#4842 – `update` command downloads wrong architecture binary on aarch64](https://github.com/zeroclaw-labs/zeroclaw/issues/4842) (7 comments, closed) – Platform parity fix.

**Most upvoted issues:**
- [#4467 – Add MCP resource and prompt support](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) (4👍) – Community strongly desires full MCP client capabilities beyond tools.
- [#4879 – Gemini CLI OAuth is simply not working](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) (2👍, S1, open since March) – A persistent pain point for Google Gemini users.
- [#3100 – [Mattermost] oncall mode instead of single-channel listening](https://github.com/zeroclaw-labs/zeroclaw/issues/3100) (2👍, open since March) – Feature request for Mattermost parity with OpenClaw.

**Underlying needs:**
- Security & multi-tenancy (#5982, #6914, #6915, #6876) – Administrators need granular control over tools and access.
- Provider reliability (#5937, #4879, #5962) – Inconsistent configuration and authentication failures block workflows.
- Output routing flexibility (#6954, #6969, #6883) – Users want to control where and how replies are delivered (voice, text, per-channel).

## 5. Bugs & Stability
**Critical/S1 bugs updated today:**
- [#7043 – [Bug]: zerocode TUI never reconnects after daemon close; UI wedges](https://github.com/zeroclaw-labs/zeroclaw/issues/7043) (S1, new) – TUI becomes permanently unresponsive after daemon restart. No fix PR yet.
- [#6876 – `risk_profile.allowed_tools` does not restrict MCP tools](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) (P1, S2) – Security gap: MCP tools bypass allowed_tools. Documentation or design fix needed.
- [#6914 – feat: enforce allowed_tools/denied_tools in main agent loop](https://github.com/zeroclaw-labs/zeroclaw/issues/6914) (P1, blocked) – Enhancement to close the gap, but still under review.
- [#6916 – feat: process-memory limits on shell/skill_tool subprocess execution](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) (P1, blocked) – OOM vulnerability in production.

**Medium-severity bugs updated today:**
- [#5866 – Telegram group bot ignores replies when mention_only=true](https://github.com/zeroclaw-labs/zeroclaw/issues/5866) (S1, open) – Reply-to-bot not working in groups.
- [#6720 – `context_aware_tools` config field is declared but unread (dead code)](https://github.com/zeroclaw-labs/zeroclaw/issues/6720) – Config option does nothing.
- [#4879 – Gemini CLI OAuth broken](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) (S1, open since March) – No fix PR in sight.

**Fix PRs in flight:**
- [#7029 – fix(zerocode): refresh empty states after setup](https://github.com/zeroclaw-labs/zeroclaw/pull/7029) (closed) – Addresses UI wedge symptom.
- [#7047 – fix(hardware): surface pin_devices and description in hardware_capabilities tool](https://github.com/zeroclaw-labs/zeroclaw/pull/7047) – Fixes dropped fields in hardware tool.

## 6. Feature Requests & Roadmap Signals
**High-value user requests likely to shape v0.8.0+:**

- **Multi-tenant RBAC** (#5982) – Drive for production deployments.
- **Computer-use support (screen interaction)** (#6909) – Inspired by OpenAI Codex, with existing PoC.
- **Unified output routing** (#6969) – Per-peer modality preference and `send_via` tool.
- **Skill-scoped tool activation** (#6915) – Temporary elevation during skill execution.
- **MCP resource/prompt support** (#4467) – Long-standing, high 👍, essential for MCP parity.
- **Hardware integration** (#6148, #7045–#7048) – Smart-room IoT control with ESP32 simulator.

**Predictions for next release (v0.8.0-beta-2):**
- The `zerocode` TUI (PR #6848) with RPC socket transport and `DenyWithEdit` approval will likely form the core of the next beta.
- Email channel improvements (XOAUTH2, read-only IMAP tools, #7021) are almost ready.
- TTS voice note support for Telegram/WhatsApp (#7050) appears merge-ready.
- Versioned documentation deployment (#7023) will improve user experience.

## 7. User Feedback Summary
**Pain points voiced in the last 24h:**
- **Gemini OAuth still broken** (#4879) – Users are blocked from using Gemini with CLI authentication; no maintainer activity for weeks.
- **Ollama tool calls fail** (#5962) – Session-blocking when tools are needed.
- **Telegram mention-only mode ignores replies** (#5866) – Inconsistency breaks expected bot interaction.
- **`web_fetch` private host whitelist ineffective** (#5122) – Domain-based allowlist does not work for DNS-resolved private IPs; security vs usability tension.
- **Cron output routing** (#6647) – Now closed, but the root cause was the scheduler bypassing the orchestrator pipeline – a systemic design issue.

**Positive signals:**
- The community is actively contributing hardware demos (ESP32, #6148) and channel improvements (Twilio, Linq multi-tenant).
- New contributors (e.g., @mov-xound-glitch, @Rhoahndur) are pushing substantial RFCs and code, indicating healthy open-source engagement.

## 8. Backlog Watch
**Issues needing maintainer attention (open, high priority, stale or blocked):**
- [#4879 – Gemini CLI OAuth broken](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) (P1, open since March, 2👍) – No fix PR, no maintainer comment in weeks.
- [#5122 – web_fetch allowed_private_hosts useless for domain names resolving to private IPs](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) (P1, open since March) – Security feature not working as documented.
- [#6074 – audit: track 153 commits lost in bulk revert](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) (P2, open since April) – Require recovery planning.
- [#3100 – [Mattermost] oncall mode](https://github.com/zeroclaw-labs/zeroclaw/issues/3100) (P2, open since March) – Feature parity with OpenClaw.
- [#4467 – Add MCP resource and prompt support](https://github.com/zeroclaw-labs/zeroclaw/issues/4467) (P2, open since March, 4👍) – High community demand, no progress.

**PRs blocked on maintainer review:**
- [#6914 – enforce allowed_tools/denied_tools in main agent loop](https://github.com/zeroclaw-labs/zeroclaw/pull/6914) (P1, needs-maintainer-review)
- [#6915 – skill-scoped tool activation](https://github.com/zeroclaw-labs/zeroclaw/pull/6915) (P2, blocked)
- [#6916 – process-memory limits on subprocess execution](https://github.com/zeroclaw-labs/zeroclaw/pull/6916) (P1, blocked)
- [#6917 – honor action-scope filter in Composio tool dispatch](https://github.com/zeroclaw-labs/zeroclaw/pull/6917) (P2, blocked)
- [#6148 – feat(hardware): smart-room ESP32 demo](https://github.com/zeroclaw-labs/zeroclaw/pull/6148) (needs-author-action) – Author has been asked to split per AGENTS.md.

**Overall project health:** High activity with strong community contributions, but maintainer responsiveness is a bottleneck for several security-critical and high-value features. The upcoming beta-2 release may alleviate some pressure if the integration branch lands.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*