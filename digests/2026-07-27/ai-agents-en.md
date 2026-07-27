# OpenClaw Ecosystem Digest 2026-07-27

> Issues: 347 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-27 02:11 UTC

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

# OpenClaw Project Digest – 2026-07-27

## 1. Today's Overview
OpenClaw continues to show very high development velocity with **347 issues** and **500 pull requests** updated in the last 24 hours. The project closed 104 issues and merged/closed 343 PRs, indicating a strong focus on bug fixes and incremental improvements. No new releases were published today, but the sheer volume of activity—especially on stability and regression fixes—signals a push toward hardening after recent beta updates. The most impactful discussions center around session state corruption, message loss, and platform gaps (Linux/Windows apps), with several critical P1 bugs still unresolved.

## 2. Releases
*None today.* (Last release mentioned in data: 2026.7.2-beta.4, but no official release notes in today's snapshot.)

## 3. Project Progress
**343 PRs were merged or closed today.** Notable ones include:

- **Fix for plugin-state namespace eviction** ([#87254](https://github.com/openclaw/openclaw/pull/87254)) – Merged. Prevents Telegram message‑cache namespace from starving sibling namespaces.
- **Codex false completion stalls** ([#87781](https://github.com/openclaw/openclaw/pull/87781)) – Merged. Prevents premature `turn/completed` on native Codex streams by counting forwarded deltas as active activity.
- **Build: stale agent‑core dts warnings** ([#87915](https://github.com/openclaw/openclaw/pull/87915)) – Merged. Avoids relative module augmentations in generated declarations.
- **Keep command text in progress drafts** ([#93711](https://github.com/openclaw/openclaw/pull/93711)) – Merged. Preserves command text across Telegram/Slack/Discord progress updates.
- **Fix Telegram OAuth emails in rich entity detection** ([#95900](https://github.com/openclaw/openclaw/pull/95900)) – Merged. Prevents `RICH_MESSAGE_EMAIL_INVALID` rejection.
- **Refactor: share turn accounting and recovery** ([#114220](https://github.com/openclaw/openclaw/pull/114220)) – Merged. Unifies stranded‑reply recovery logic for foreground and queued turns.
- **Fix scripts: local fallback for changed checks** ([#114225](https://github.com/openclaw/openclaw/pull/114225)) – Merged. Implements local execution when remote CI backend is unavailable.
- **Fix plugins: report empty npm install failures** ([#114215](https://github.com/openclaw/openclaw/pull/114215)) – Open but ready for review; fixes unhelpful “npm install failed:” messages.

## 4. Community Hot Topics

| Issue / PR | Comments | Reactions | Summary |
|------------|----------|-----------|---------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows Clawdbot Apps | 115 | 👍 80 | Long‑standing enhancement request for desktop clients on Linux and Windows, currently blocked on maintainer product decision and security review. |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) – Tool outputs as image attachments | 24 | 👍 2 | Agent loses ability to read ANSI‑heavy tool stdout when it collapses to an image placeholder. High impact on session state and message loss. |
| [#102020](https://github.com/openclaw/openclaw/issues/102020) – Second message fails with “reply session initialization conflicted” | 15 | 👍 1 | Cross‑channel (Signal, da…) regression after first turn. Still awaiting maintainer review. |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) – Latency with Active Memory + Codex | 13 | 👍 2 | Deployments using `active‑memory` and `lossless‑claw` experience long response times, hook timeouts, and event‑loop stalls. |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) – Duplicate replies on Telegram (2‑10x) | 12 | 👍 1 | Regression after 5.20 update; partially mitigated in 5.22 but not resolved. |

**Underlying needs:** The community is primarily concerned with **session reliability** (loss of messages, duplicate replies, agent wedging) and **cross‑platform availability** (desktop apps for Linux/Windows). The tool output encoding bug (#99241) undermines agent autonomy in complex workflows.

## 5. Bugs & Stability

High‑severity bugs reported or discussed today:

- **P1 – Codex sessions.reset reuses retired session ID; RAM exhaustion** ([#113434](https://github.com/openclaw/openclaw/issues/113434)) – On Windows 11, repeated Codex catalog/file scans cause Gateway OOM crashes. Fix in progress? Not yet linked.
- **P1 – Telegram inbound update permanently lost** ([#113315](https://github.com/openclaw/openclaw/issues/113315)) – Offset advanced but no ingress or dispatch, message never delivered.
- **P1 – Control UI regressions in multi‑agent setup** ([#112696](https://github.com/openclaw/openclaw/issues/112696)) – Avatar loading fails and session list broken after 2026.7.1‑2.
- **P1 – Telegram DM replies fall back after stale DM‑scope cleanup** ([#111519](https://github.com/openclaw/openclaw/issues/111519)) – Regression in 2026.7.2‑beta.3; source‑reply ownership lost.
- **P1 – MCP loopback transport not auto‑reconnecting** ([#98435](https://github.com/openclaw/openclaw/issues/98435)) – After gateway restart, CLI side reports `recovered=1` but MCP transport is dead.
- **P1 – prompt‑cache prefix churn on OpenAI models** ([#95610](https://github.com/openclaw/openclaw/issues/95610)) – Per‑turn dynamic content defeats prefix caching, increasing costs for high‑volume users.
- **P1 – Additive column migration runs before canonical schema assertion** (PR [#111365](https://github.com/openclaw/openclaw/pull/111365)) – Fix open for review; addresses startup failure after beta upgrade.
- **P1 – Voice Wake migration conflict loops** (PR [#112871](https://github.com/openclaw/openclaw/pull/112871)) – Fix ready for maintainer look; prevents deterministic startup refusal.

Several fix PRs are in flight or already merged, but the sheer number of P1 regressions indicates that the recent beta series (7.x) has introduced notable instability, especially in session management and inter‑process communication.

## 6. Feature Requests & Roadmap Signals

Most‑requested features from today's issue list:

- **Linux/Windows Clawdbot Apps** ([#75](https://github.com/openclaw/openclaw/issues/75)) – 115 comments, 80 👍. Likely the next major platform push if product decision resolves.
- **Per‑spawn tool restrictions for sub‑agents** ([#15032](https://github.com/openclaw/openclaw/issues/15032)) – PR [#78441](https://github.com/openclaw/openclaw/pull/78441) already open; this may land in the next minor release.
- **WhatsApp sticker send support** ([#7476](https://github.com/openclaw/openclaw/issues/7476)) – Minor but highly visible UX gap.
- **Denylist for exec‑approvals** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) – “Allow everything except X” policy; linked PR open.
- **Mid‑stream message injection (soft steer)** ([#10960](https://github.com/openclaw/openclaw/issues/10960)) – Real‑time steering without waiting for tool boundaries.

**Predictions for next release:** The sub‑agent tool restriction (#15032) and the state migration fix (#111365) are likely candidates. The Linux/Windows app (#75) remains a large effort unlikely in the next release given the backlog of stability fixes.

## 7. User Feedback Summary

- **Pain points (high frequency):** Duplicate replies (#86519), silent message drops (#113315), session corruption after upgrade (#111519, #90378), and high memory usage (#113434, #67413).
- **Satisfaction drivers:** The community acknowledges the beta pace and appreciates ongoing improvements to Telegram delivery and Codex streaming.
- **Workarounds sought:** Multiple users report falling back to pinned versions (2026.5.x) to avoid regressions.

Overall, the feedback reflects a **mixed sentiment**: enthusiasm for the project's ambition tempered by frustration with regression churn after each update.

## 8. Backlog Watch

Long‑unresolved but important items requiring maintainer attention:

| Issue | Age | Last Activity | Why Concern |
|-------|-----|---------------|-------------|
| [#75 – Linux/Windows Apps](https://github.com/openclaw/openclaw/issues/75) | 7 months | 2026‑07‑27 | 115 comments, blocks a major platform; requires product decision and security review. |
| [#6615 – Denylist for exec-approvals](https://github.com/openclaw/openclaw/issues/6615) | 5 months | 2026‑07‑26 | Linked PR open but maintainer review stalled. |
| [#42026 – Distributed Agent Runtime RFC](https://github.com/openclaw/openclaw/issues/42026) | 4 months | 2026‑07‑26 | Architectural proposal with no design decision. |
| [#11665 – Webhook multi‑turn session reuse](https://github.com/openclaw/openclaw/issues/11665) | 5 months | 2026‑07‑26 | Documented feature doesn't work; linked PR open but not merged. |
| [#86519 – Duplicate replies regression](https://github.com/openclaw/openclaw/issues/86519) | 2 months | 2026‑07‑26 | High‑impact, multiple workarounds attempted, still not fully resolved. |

These items represent either architectural decisions (apps, distributed runtime) or lingering regressions that erode user trust. Addressing the duplicate replies and session‑state bugs should be the top priority for the next stable release.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
## Personal AI Assistant Open-Source Landscape — 2026-07-27

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem continues to evolve rapidly, with **thousands of commits per day** across active projects and a clear tension between **feature velocity** and **regression stability**. The landscape is characterized by a small number of dominant reference implementations (notably OpenClaw and ZeroClaw) surrounded by a long tail of smaller, more specialized projects. Cross-cutting themes include a universal push toward **MCP (Model Context Protocol) maturity**, **session reliability**, and **platform expansion** (Linux/Windows desktop apps). The community is increasingly demanding **asynchronous agent behaviors**, **observable tool execution**, and **security hardening** — especially in credential handling and sandbox enforcement. While the "beta churn" frustrates some users, the overall development pace signals a healthy, competitive ecosystem that is rapidly closing gaps with commercial offerings.

---

## 2. Activity Comparison — 24-Hour Snapshot (2026-07-27)

| Project | Issues Updated | PRs Updated | PRs Merged/Closed | New Release? | Activity Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 347 | 500 | 343 | No | ⚠️ **High** (very active, but 12+ P1 bugs) |
| **ZeroClaw** | 50 | 50 | 2 | No | ⚠️ **High** (intense triage, critical bugs) |
| **Hermes Agent** | 50 | 50 | 5 | No | ✅ **High** (active review, 1 P0 fixed) |
| **NanoBot** | 9 | 29 | 24 | No | ✅ **High** (rapid bug turnaround) |
| **NanoClaw** | 2 | 8 | 2 | No | ✅ **Active** (targeted fixes) |
| **CoPaw** | 12 | 9 | 0 | No | ✅ **Active** (community PRs, no merges) |
| **IronClaw** | 5 | 18 | 6 | No | ✅ **High** (focused on recoverability epic) |
| **Moltis** | 0 | 8 | 0 | No | ✅ **Active** (architectural features) |
| **PicoClaw** | 4 | 7 | 1 | No | ✅ **Moderate** (security fixes) |
| **LobsterAI** | 2 | 8 | 1 | No | ⚠️ **Low** (stalled April PRs, critical bug) |
| **NullClaw** | 1 | 0 | 0 | No | 🔴 **Critical** (unresolved SIGSEGV, 10 days) |
| **TinyClaw** | 0 | 0 | 0 | No | 🔴 **Inactive** |
| **ZeptoClaw** | 0 | 0 | 0 | No | 🔴 **Inactive** |

*\*Health Score: Qualitative assessment combining commit volume, bug-fix velocity, maintainer responsiveness, and remaining open severity.*

### Key Observations:
- **OpenClaw dominates raw volume** — but the sheer number of open P1 bugs (12+) suggests velocity is outpacing quality assurance.
- **NanoBot shows the best PR throughput-to-bug ratio** — 24 of 29 PRs merged with all critical bugs fixed except one (`/stop` message loss).
- **NullClaw, TinyClaw, and ZeptoClaw** are effectively stalled, with NullClaw's 10-day-old SIGSEGV being a critical red flag for its user base.
- **LobsterAI** has a cluster of stale PRs from April 2026 that remain unmerged — a sign of review bottleneck.

---

## 3. OpenClaw's Position

### Advantages Over Peers
- **Scale and Community**: 347 issues + 500 PRs/day reflects a massive contributor base and ecosystem gravity. No other project approaches this volume.
- **Feature Breadth**: Telegram, Slack, Discord, Codex, Active Memory, MCP support, plugin architecture — OpenClaw's feature surface is the widest in the ecosystem.
- **Reference Implementation Status**: As `github.com/openclaw/openclaw`, it functions as the de facto standard against which others are compared.
- **Recovery & Turn Accounting**: Uniquely advanced work on session recovery (#114220) and prefix caching (#95610 discussions) shows architectural depth.

### Disadvantages vs. Peers
- **Regression Churn**: 12+ P1 bugs per digest, including session corruption (#111519), message loss (#113315), and memory exhaustion (#113434). This erodes trust — multiple users report pinning to v2026.5.x.
- **Cross-Platform Gap**: Issue #75 (Linux/Windows desktop apps) has been open for 7 months with 115 comments and 80 👍 — a glaring hole that smaller projects (NanoClaw, Hermes Desktop) are filling.
- **Review Velocity**: 500 PRs but only 343 merged suggests a growing review backlog, which may slow future releases.

### Technical Approach Differences
OpenClaw's architecture centers on a **microkernel plugin model** with strict namespace eviction and session state management. This contrasts with:
- **ZeroClaw**: Uses Landlock sandboxing and deeper OS integration — more security-forward.
- **NanoBot**: Lighter weight, Python-centric, with Dream no-op handling and unified sessions — favors simplicity over extensibility.
- **Hermes Agent**: Heavy focus on gateway and profile isolation — targets multi-tenancy and enterprise use cases.

### Community Size Comparison
| Metric | OpenClaw | ZeroClaw | Hermes Agent | NanoBot |
|---|---|---|---|---|
| Issues/day | 347 | 50 | 50 | 9 |
| PRs/day | 500 | 50 | 50 | 29 |
| Top issue engagement | 115 comments | 14 comments | 15 comments | 4 comments |
| Maintainer response time | ~1-2 days (P1) | ~1-3 days (P1) | ~1 day (P0 closed) | ~Same day |

OpenClaw's community is an order of magnitude larger than any peer, but **engagement per issue is shallower** — suggesting a "submit and move on" culture rather than deep collaborative debugging.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across **3+ projects** in today's digests, indicating ecosystem-wide priorities:

| Focus Area | Projects Affected | Specific Needs |
|---|---|---|
| **Session Reliability** | OpenClaw, NanoClaw, Hermes Agent, ZeroClaw | Duplicate replies, silent message drops, in_reply_to corruption, session ID reuse, migration boot loops |
| **MCP/Tool-Configuration Maturity** | NanoBot, PicoClaw, ZeroClaw, IronClaw | Transport selection (SSE vs. Streamable HTTP), `$ref` schema normalization, zombie MCP processes, auto-reconnect |
| **Cross-Platform Desktop Clients** | OpenClaw (#75), Hermes (Desktop fix), LobsterAI (#273) | Linux/Windows apps for Clawdbot, GUI-only Desktop installation, Ubuntu support |
| **Security Hardening** | NanoBot, PicoClaw, Moltis, ZeroClaw | SSRF gating (image downloads), credential placeholder sanitization, privileged command gating (``/sh``), runtime options leak |
| **Async Workflow Support** | CoPaw, OpenClaw, IronClaw, NanoClaw | ``notice_after_complete`` tool, non-blocking sub-agents, send_message without freezing conversation |
| **Provider/Credential Resilience** | ZeroClaw, CoPaw, Hermes Agent, NanoBot | OAuth profile support, credential rotation after rate limits, prompt-cache prefix compatibility |
| **CI/Test Matrix Expansion** | ZeroClaw (#7462), OpenClaw (covered) | Windows/macOS test coverage, cross-platform path semantics, console encoding |

### Surprising Absences
- **No project** today showed significant work on **federated agent discovery** or **cross-project ACP interoperability**, despite Moltis and IronClaw each landing ACP-related features independently.
- **No active work on model-preference learning** or **personalization** — the ecosystem is still in a "plumbing" phase rather than an "intelligence" phase.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | NanoBot | Hermes Agent | IronClaw | Moltis |
|---|---|---|---|---|---|---|
| **Core Philosophy** | Extensibility via plugins & namespaces | Security-first, OS-level integration | Lightweight Python, rapid iteration | Enterprise multi-tenancy, gateway-centric | Error-recoverability, formal verification | Integration hub (ACP, Nostr, Slack) |
| **Target User** | Power users, self-hosters | Security-conscious ops teams | Raspberry Pi / resource-constrained users | Teams, organizations | Research/development teams | Buzz ecosystem, cross-platform users |
| **Key Strength** | Largest community, widest feature set | Strongest sandbox (Landlock) | Best bug-fix turnaround (24/29 PRs merged) | Profile isolation, Desktop support | Architectural rigor (conformance matrices) | Interoperability (ACP agent mode) |
| **Key Weakness** | Regression churn, review bottleneck | Critical Windows/Telegram bugs | Fewer features, smaller community | Long-standing security issues (#12651) | Stalled release PR (24 days) | No issues updated; silent community |
| **Programming Language** | Multi-language (Go, TypeScript, Rust) | Rust | Python | TypeScript | Rust | Rust |
| **Release Cadence** | Weekly beta (high churn) | Monthly stable (v0.8.3) | Semiregular (v0.2.2) | Ongoing (no release today) | Blocked (release PR stalled) | Unclear |
| **Unique Feature** | Active Memory + Codex streaming | Landlock sandboxing | Dream no-op handling | Nous Portal prompt caching | RecoverabilityClass enum | Zvec + Redb vector memory |

### Bottom Line
**OpenClaw** remains the ecosystem's **"Linux kernel"** — broad, community-driven, but prone to regression. **ZeroClaw** is the **"OpenBSD"** — security-hardened but slower-moving. **NanoBot** is the **"Raspberry Pi OS"** — lean, reliable, targeted. Each serves a distinct user profile, and none is a direct substitute for another.

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity with Stability Concerns
- **OpenClaw** — Massive throughput but P1 regression count is alarming. The community trusts the beta pace but is impatient for a stable release.
- **ZeroClaw** — Intense triage with critical bugs (Windows, MCP, Landlock). The upcoming v0.8.4 release will be a turning point.

### Tier 2: Rapid Iteration, Good Stability
- **NanoBot** — Best bug-fix velocity in the ecosystem. A strong choice for users who value reliability over features.
- **PicoClaw** — Small but responsive. Security hardening and native Exa search signal maturity.
- **Moltis** — Architectural features (ACP, vector memory) suggest long-term planning rather than rapid iteration.

### Tier 3: Active but Review-Bottlenecked
- **Hermes Agent** — Healthy bug reporting but 45 open PRs and a cluster of stale issues (#12651, #3506) indicate review lag.
- **CoPaw** — Strong community PR pipeline (4 first-time contributor PRs today) but zero merges suggests maintainers are overwhelmed.
- **IronClaw** — Focused engineering but the 24-day-old release PR is blocking downstream consumers.

### Tier 4: Stalled or Low Activity
- **LobsterAI** — Stale April PRs, a critical gateway restart bug, and low community engagement suggest a project that needs maintainer re-engagement.
- **NullClaw** — Single critical SIGSEGV with no maintainer response for 10 days. Users are effectively abandoned on aarch64.
- **TinyClaw, ZeptoClaw** — Effectively inactive.

---

## 7. Trend Signals

### Emerging Industry Trends (from Community Feedback)

1. **The "Async Agent" Imperative**  
   Users across CoPaw, OpenClaw, and IronClaw are demanding **non-blocking agent behaviors** — long-running tasks should not freeze the conversation. The ``notice_after_complete`` pattern (CoPaw #6475) and IronClaw's error-recoverability epic (#6284) point toward a future where agents are truly background-capable.

2. **MCP Standardization is Immature**  
   Five projects (NanoBot, PicoClaw, ZeroClaw, IronClaw, CoPaw) hit MCP-level bugs today — wrong transport selection, zombie servers, schema normalization failures. The Model Context Protocol is **not yet a solved problem** at the ecosystem level, and every integration is a bespoke effort.

3. **Security is Shifting Left**  
   The proliferation of SSRF gating (NanoBot #5095, ZeroClaw #8826), credential placeholder sanitization (Hermes #12651), and privileged command gating (Moltis #1170) signals a **collective hardening phase**. Credential leaks via error messages (ZeroClaw #9386) are being caught and fixed proactively.

4. **Cross-Platform is the Unmet Need**  
   OpenClaw's 7-month-old desktop app issue (#75), LobsterAI's Linux request (#273), and ZeroClaw's Windows CI expansion (#7462) all point to a **universal desire for first-class Linux and Windows support**. The ecosystem still favors headless/server deployments, but desktop apps are the next frontier.

5. **Observability is a Gap**  
   Users repeatedly ask, "How do I verify X is working?" (CoPaw #6342 — embedding model; Hermes — profile isolation; ZeroClaw — test failures). The ecosystem lacks **transparent status tools** for configuration validation, which erodes trust.

### Value for AI Agent Developers

- **For reliability-focused use cases** (production bots, customer-facing agents): **NanoBot** or **PicoClaw** offer the best stability-to-feature ratio today.
- **For cutting-edge experimentation** (multi-modal, active memory, Codex): **OpenClaw** is the playground, but expect regression churn. Plan for pinned version deployment.
- **For security-sensitive deployments** (enterprise, personal data handling): **ZeroClaw** with Landlock is the strongest choice, but evaluate Windows/Telegram bugs first.
- **For multi-platform integration** (Buzz, Slack, ACP): **Moltis** is uniquely positioned, though it's early-stage.
- **For self-hosted on ARM** (Raspberry Pi): **NanoBot** (fixed idle CPU issue) or **PicoClaw** (Go binary) are recommended. **Avoid NullClaw** on aarch64 until Issue #976 is resolved.

The ecosystem is **fragmented but converging** — expect consolidation around MCP, async patterns, and cross-platform support over the next 3–6 months.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-07-27

## Today's Overview
The project saw very high activity over the past 24 hours: 9 issues updated (7 closed, 2 open) and 29 pull requests updated (24 merged/closed, 5 open). No new releases were published. The bulk of work focused on security hardening, bug fixes, and infrastructure improvements, with several `priority: p1` fixes merged. The community continues to provide detailed bug reports, and maintainers are responding quickly. Two long-standing feature PRs remain in conflict/unmerged, suggesting ongoing discussion.

## Releases
No new releases today. The last published version remains `nanobot-ai==0.2.2` (based on issue #5051 reference).

## Project Progress
- **Security**: PR [#5095](https://github.com/HKUDS/nanobot/pull/5095) hardens image URL downloads by validating redirect hops and capping stream size. PR [#5101](https://github.com/HKUDS/nanobot/pull/5101) honors provider proxy configuration for image URLs.
- **Channel & Heartbeat Fixes**: PR [#4928](https://github.com/HKUDS/nanobot/pull/4928) fixes heartbeat routing for unified sessions; PR [#5069](https://github.com/HKUDS/nanobot/pull/5069) prevents saving credentials from cancelled QR connections; PR [#5084](https://github.com/HKUDS/nanobot/pull/5084) preserves pending message runtime context; PR [#5100](https://github.com/HKUDS/nanobot/pull/5100) fixes mobile webUI layout widening.
- **Agent & Memory**: PR [#5054](https://github.com/HKUDS/nanobot/pull/5054) advances Dream cursor after no-op batches; PR [#5056](https://github.com/HKUDS/nanobot/pull/5056) preserves output across length recovery; PR [#5099](https://github.com/HKUDS/nanobot/pull/5099) protects unprocessed Dream history from compaction.
- **MCP & Tools**: PR [#5057](https://github.com/HKUDS/nanobot/pull/5057) normalizes local schema refs to fix Kimi/Moonshot provider compatibility; PR [#4625](https://github.com/HKUDS/nanobot/pull/4625) adds configurable extra bwrap bind roots.
- **CLI & Codex**: PR [#4939](https://github.com/HKUDS/nanobot/pull/4939) adds Codex OAuth flow in Quick Start.
- **Data Robustness**: PRs [#5087](https://github.com/HKUDS/nanobot/pull/5087), [#5088](https://github.com/HKUDS/nanobot/pull/5088), [#5089](https://github.com/HKUDS/nanobot/pull/5089) fix null-handling crashes in triggers, pairing, and Feishu card extraction.
- **DingTalk Channel**: PR [#4446](https://github.com/HKUDS/nanobot/pull/4446) adds `disable_private_chat` flag and sender mention in group replies.
- **Idle Compaction**: PR [#5036](https://github.com/HKUDS/nanobot/pull/5036) makes scan interval configurable, reducing CPU usage on low-power devices.

## Community Hot Topics
- **Most discussed issue**: [#4924](https://github.com/HKUDS/nanobot/issues/4924) (4 comments) – bug in heartbeat target selection when `unifiedSession: true`. Now closed via PR #4928.
- **Stale but still open**: [#1012](https://github.com/HKUDS/nanobot/issues/1012) (2 comments) – request for subagent profiles with configurable tools/skills. No maintainer response since February 2026.
- **Open bug**: [#4792](https://github.com/HKUDS/nanobot/issues/4792) (2 comments) – `/stop` silently discards queue messages. No fix PR yet.
- **Unresolved discussion**: PR [#5098](https://github.com/HKUDS/nanobot/pull/5098) (open, with `conflict` label) – unified extension platform; comments not shown but listed as open.
- **Likely needed clarification**: PR [#4301](https://github.com/HKUDS/nanobot/pull/4301) (open, `conflict`) – caching skills loader entries has been open since June.

## Bugs & Stability
A large batch of `priority: p1` bugs were reported and fixed this cycle:

| Severity | Bug (Issue) | Fix PR |
|----------|-------------|--------|
| **Critical** | Security: unfiltered image URL downloads could lead to SSRF/redirect attacks [#5095](https://github.com/HKUDS/nanobot/pull/5095) | #5095 |
| **High** | `/stop` permanently loses pending messages [#4792](https://github.com/HKUDS/nanobot/issues/4792) | *No fix yet* |
| **High** | Dream no-op batches starve later history [#5041](https://github.com/HKUDS/nanobot/issues/5041) | #5054 |
| **High** | Token-length recovery loses early content segments [#5051](https://github.com/HKUDS/nanobot/issues/5051) | #5056 |
| **High** | MCP tool `$ref` collapses entire model on Kimi/Moonshot [#5040](https://github.com/HKUDS/nanobot/issues/5040) | #5057 |
| **Medium** | Pending mid-turn messages lose runtime context [#4064](https://github.com/HKUDS/nanobot/issues/4064) | #5084 |
| **Medium** | `unifiedSession` heartbeat fails with no sessions [#4924](https://github.com/HKUDS/nanobot/issues/4924) | #4928 |
| **Low** | Null values in `pairing.json`, `triggers.json`, Feishu card fields crash loaders [various] | #5087, #5088, #5089 |
| **Low** | Mobile webUI thread widening on long messages | #5100 |

All except #4792 have been closed. The `/stop` message loss bug remains open and warrants prompt attention.

## Feature Requests & Roadmap Signals
- **Recently delivered**: Configurable bwrap extra bind roots (PR #4625, from issue #4107) and idle compaction interval (PR #5036).
- **Open feature PRs that are likely to land in next version**:
  - [#5098](https://github.com/HKUDS/nanobot/pull/5098) – Unified extension platform. This is a major architectural addition that would make extensions first-class citizens. Currently has conflicts.
  - [#4301](https://github.com/HKUDS/nanobot/pull/4301) – Skills caching to avoid repeated directory scans. Also has conflicts.
- **Long-standing request**: Subagent profiles (issue #1012) – still no movement; may require more community demand or architectural design.

## User Feedback Summary
- **Pain points**: 
  - Users running on resource-constrained hardware (Raspberry Pi) report high idle CPU usage; the configurable compaction interval (PR #5036) directly addresses this.
  - MCP tool users on Kimi/Moonshot experienced total model rejection due to incompatible `$ref` schemas – fixed in #5057.
  - The `/stop` command losing messages is a critical usability issue for chat workflows (#4792).
  - Null field crashes in pairing/triggers/Feishu indicate data format fragility – now patched.
- **Satisfaction**: Quick turnaround on security, image proxy, and heartbeat fixes shows active maintainer engagement. Several users contributed bug reports and PRs, indicating a healthy open-source ecosystem.

## Backlog Watch
The following items need maintainer attention:

- **Issue #1012** (Feb 22, 2026) – Subagent profiles. No maintainer response in 5 months. May need roadmap decision or closure.
- **Issue #4792** (Jul 6, 2026) – `/stop` message loss. Open with no fix PR despite high severity.
- **PR #5098** – Unified extension platform. Conflicts need resolution; if accepted, it will be a major feature for the next release.
- **PR #4301** – Skills caching. Conflicts similarly need updating.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-27

## Today’s Overview

The project saw extremely high activity with **50 issues and 50 pull requests updated in the past 24 hours**, reflecting a busy development and community engagement day. Of those, **3 issues were closed** and **5 PRs were merged/closed**, while the vast majority remain open (47 open issues, 45 open PRs). No new releases were published. The high number of open items suggests substantial ongoing work across bug fixes, feature development, and community contributions. Key areas of focus include gateway adapter reliability, tool configuration, security hardening, and user-requested integrations.

## Releases

None.

## Project Progress

While the exact list of merged/closed PRs was not provided, the closed issues indicate progress on two significant items:

- **Nous Portal caching fix (P0)** – Issue #71576 ([link](https://github.com/NousResearch/hermes-agent/issues/71576)) was closed. The bug caused Anthropic models routed through Nous Portal to achieve only a 39% prompt-cache hit rate (vs. 100% on OpenRouter), resulting in ~2.3x cost. This has been resolved.
- **Desktop find feature (P3)** – Issue #46169 ([link](https://github.com/NousResearch/hermes-agent/issues/46169)) was closed after implementing Ctrl+F/Cmd+F search across chat and UI editors in Hermes Desktop.

Several PRs submitted today target critical fixes (e.g., cron kill branch anchoring, gateway env var expansion, file mutation verification) and are moving through review.

## Community Hot Topics

| Issue/PR | Comments | Reactions | Summary |
|---|---|---|---|
| [#68871](https://github.com/NousResearch/hermes-agent/issues/68871) – [OPEN] | 15 | 👍 13 | **Feature request**: Integrate Buzz (Block’s self-hosted workspace for humans & AI agents) as a new messaging platform. High interest from community. |
| [#62936](https://github.com/NousResearch/hermes-agent/issues/62936) – [OPEN] | 7 | 👍 0 | **Bug**: Telegram uploads >~15 MB always fail with TimedOut; `HERMES_TELEGRAM_HTTP_WRITE_TIMEOUT` has no effect on media uploads. Users frustated with hard limit. |
| [#12651](https://github.com/NousResearch/hermes-agent/issues/12651) – [OPEN] (since Apr 19) | 5 | 👍 0 | **Bug**: `.env` sanitizer fails to remove `KEY=***` placeholders, causing them to be treated as real credentials. Long-standing config safety issue. |
| [#51184](https://github.com/NousResearch/hermes-agent/issues/51184) – [OPEN] | 4 | 👍 0 | **Bug**: Cron jobs report false‑positive delivery when LINE adapter is in a broken state. Reliability concern for scheduled messages. |
| [#3506](https://github.com/NousResearch/hermes-agent/issues/3506) – [OPEN] (since Mar 28) | 4 | 👍 0 | **Feature**: Durable Feedback Routing – more consistent use of memory, skills, and follow‑up planning. Long‑requested capability for learning from user feedback. |

The community is actively pushing for integrations (Buzz), deeper configuration control (reaction emojis, profile cloning), and improvements to adapter reliability (Telegram, LINE, Discord). The high number of comments on the Buzz feature signals strong interest in expanding Hermes’ platform support.

## Bugs & Stability

**Today’s most critical bugs (ranked by severity):**

1. **P0 – Closed** – Nous Portal prompt‑cache miss with Anthropic models (#71576) – *fixed.*
2. **P2 – [NEW]** – `video_analyze` ignores auxiliary vision model, sends video to main model instead (#72371 – [link](https://github.com/NousResearch/hermes-agent/issues/72371))
3. **P2 – [NEW]** – GPT-5.6 auto-title sends unsupported `temperature` parameter, causing rejection (#72351 – [link](https://github.com/NousResearch/hermes-agent/issues/72351))
4. **P2 – [NEW] – Security** – Discord adapter allow/deny gates are process-global, breaking per-profile isolation under `multiplex_profiles` (#72348 – [link](https://github.com/NousResearch/hermes-agent/issues/72348))
5. **P2 – [NEW] – Regression** – CLI/TUI: `/whoami` shows in autocomplete but prints ‘Unknown command’ (#35892 – [link](https://github.com/NousResearch/hermes-agent/issues/35892)) – back from May 31, still unresolved.
6. **P2 – Open** – Cron inactivity timeout closes SessionDB while agent worker is still running → intermittent silent session‑write loss (#65208 – [link](https://github.com/NousResearch/hermes-agent/issues/65208))

**Fix PRs submitted today:**
- #72375 ([link](https://github.com/NousResearch/hermes-agent/pull/72375)) – parse “exceeds maximum output tokens” error for retry (DeepSeek/Novita)
- #72384 ([link](https://github.com/NousResearch/hermes-agent/pull/72384)) – anchor kill branch so `SKILL=` is not treated as a gateway lifecycle command
- #72386 ([link](https://github.com/NousResearch/hermes-agent/pull/72386)) – expand `${VAR}` env refs in gateway config
- #72387 ([link](https://github.com/NousResearch/hermes-agent/pull/72387)) – content‑transition file mutation verifier
- #72388 ([link](https://github.com/NousResearch/hermes-agent/pull/72388)) – desktop perf: hold 60fps under load

## Feature Requests & Roadmap Signals

High‑engagement feature requests reveal the community’s priorities:

- **Buzz messaging integration** (#68871) – Could be expedited given strong community support.
- **Durable Feedback Routing** (#3506) – Aims to make memory and skills more consistent; could shape next agent behavior improvements.
- **GUI-only Desktop installation** (#50643) – Users want a standalone Desktop GUI connecting to a remote gateway, without the full CLI/agent bundle.
- **Configurable Telegram reaction emojis** (#49570) – Small UX win that would make Telegram interactions more customizable.
- **Separate profile cloning from backup/restore** (#72383) – Proposed restructuring of profile lifecycle; could appear in a minor version.

The PR introducing a **shared localization framework** (#23243 – [link](https://github.com/NousResearch/hermes-agent/pull/23243)) and the **tool activity explanation** PR (#70398 – [link](https://github.com/NousResearch/hermes-agent/pull/70398)) indicate ongoing work toward internationalization and better transparency for tool usage. These are likely candidates for the next feature release.

## User Feedback Summary

**Pain points reported today:**
- Telegram media uploads >15 MB are silently failing; timeout config is ignored.
- `.env` placeholder sanitization still broken after months (issue #12651).
- Cron jobs deliver false‑positive success when LINE adapter is down.
- Profile switching not reflected in `hermes gateway run` without restart.
- MCP `--env` flags are silently dropped if multiple are used.
- `reasoning_effort` values `minimal` and `max` fall back to `medium` on Anthropic providers.
- Video analysis ignores auxiliary vision model configuration.

**Satisfaction indicators:**
- Users are actively reporting bugs and proposing detailed solutions (e.g., MCP schema normalization, ACP session snapshot).
- The Buzz integration request received 13 thumbs‑up in 6 days – strong demand for new platform support.
- Multiple PRs from external contributors are being reviewed, showing a healthy community.

## Backlog Watch

Several important issues remain unanswered or have been open for months without resolution or maintainer decision:

| Issue | Age | Pending since | Status |
|---|---|---|---|
| [#12651](https://github.com/NousResearch/hermes-agent/issues/12651) – .env sanitizer fails | ~3 months | Apr 19 | No PR; labelled `needs-decision` |
| [#3506](https://github.com/NousResearch/hermes-agent/issues/3506) – Durable Feedback Routing | ~4 months | Mar 28 | No maintainer comment; `P3`, `area/memory` |
| [#9812](https://github.com/NousResearch/hermes-agent/issues/9812) – ACP sessions drop provider snapshot on first persist | ~3.5 months | Apr 14 | No PR; `P2`, `area/sessions` |
| [#20577](https://github.com/NousResearch/hermes-agent/issues/20577) – `<think>` blocks stripped from history on replay to vLLM | ~2.5 months | May 6 | No maintainer reply; `P2` |
| [#30626](https://github.com/NousResearch/hermes-agent/issues/30626) – `hermes gateway run` profile-blind | ~2 months | May 22 | `P2`, needs maintainer decision on architecture |
| [#42727](https://github.com/NousResearch/hermes-agent/issues/42727) – Agent-led self‑configuration can persist redacted credentials | ~1.5 months | Jun 9 | `P2` security, no PR yet |
| [#65208](https://github.com/NousResearch/hermes-agent/issues/65208) – Cron inactivity timeout closes SessionDB while agent worker still running | ~12 days | Jul 15 | No maintainer reply; `P2` |

These long‑standing items, especially the security‑related #42727 and the configuration reliability #12651, would benefit from maintainer prioritisation and/or community contributions.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw Project Digest — 2026-07-27

### 1. Today's Overview
PicoClaw shows moderate activity with 4 issues and 7 PRs updated in the last 24 hours. One bug fix PR was merged, and a security hardening PR was submitted. The community submitted a new feature (native Exa web search provider) and a feature request (AI Router provider preset). Several older “stale” items remain open, indicating some areas of the project require ongoing maintainer attention.

### 2. Releases
No new releases were published in the last 24 hours. The latest stable version remains unchanged.

### 3. Project Progress
- **Merged/Closed PR:** [#3248](https://github.com/sipeed/picoclaw/pull/3248) — Bumped Go toolchain to 1.25.12 to remediate two stdlib vulnerabilities (`crypto/tls` and `os`). This improves supply-chain security.
- **New Feature (open):** [#3299](https://github.com/sipeed/picoclaw/pull/3299) — Adds native Exa web search provider with `tools.web` / `web_search` support, including configurable date range filters.
- **Bug Fixes (open):**
  - [#3295](https://github.com/sipeed/picoclaw/pull/3295) — Fixes `SplitMessage` hang on oversized fence header (linked to Issue #3264).
  - [#3297](https://github.com/sipeed/picoclaw/pull/3297) — Security hardening for remote prompt and exec boundaries (schema v4 migration, default-disabled remote exec, per-call approval).
  - [#3267](https://github.com/sipeed/picoclaw/pull/3267) — Fixes token refresh scope bug for antigravity auth provider (stale but updated recently).
- **Localization:** [#3296](https://github.com/sipeed/picoclaw/pull/3296) — Completes Czech code wrap labels.

### 4. Community Hot Topics
- **Feature Request:** [#3298](https://github.com/sipeed/picoclaw/issues/3298) — Add native AI Router provider preset. No comments yet, but raised by the project maintainer of AI Router, suggesting external interest in easier provider integration.
- **Bug Discussion:**
  - [#3265](https://github.com/sipeed/picoclaw/issues/3265) — Gateway startup fails with `channel deltachat has unknown type` even when deltachat is not configured. Received one comment; likely a config parsing edge case.
  - [#3264](https://github.com/sipeed/picoclaw/issues/3264) — `SplitMessage` hangs on oversized fence header. One comment and a matching fix PR (#3295) now available.
- **Older but active:** [#3252](https://github.com/sipeed/picoclaw/issues/3252) — `splitKnownProviderModel` strips prefix incorrectly (closed as stale after 2 comments). The fix may be pending in an unreleased version.

### 5. Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **High** | [#3264](https://github.com/sipeed/picoclaw/issues/3264) | `SplitMessage` infinite loop on oversized fence code info string — leads to indefinite hang. | Yes ([#3295](https://github.com/sipeed/picoclaw/pull/3295)) |
| **High** | [#3265](https://github.com/sipeed/picoclaw/issues/3265) | Gateway fails to start with unknown deltachat channel type, even without deltachat config. Blocks gateway usage for some users. | No |
| **Medium** | [#3252](https://github.com/sipeed/picoclaw/issues/3252) | `splitKnownProviderModel` strips provider prefix incorrectly when model ID contains known alias. Closed as stale; may be fixed in codebase but not confirmed. | Unknown |
| **Low** | [#3202](https://github.com/sipeed/picoclaw/pull/3202) | ID normalization fails to strip leading/trailing underscores (open PR, stale). | N/A (PR is the fix) |

No new regressions were reported today beyond the ones above.

### 6. Feature Requests & Roadmap Signals
- **Native AI Router Provider Preset ([#3298](https://github.com/sipeed/picoclaw/issues/3298))**  
  Currently users must manually set `api_base` and cannot select a named provider. This would improve UX for AI Router users. Likely to be considered for the next minor release if the contributor provides implementation.
- **Native Exa Web Search Provider ([#3299](https://github.com/sipeed/picoclaw/pull/3299))**  
  Already submitted as a PR, bringing first-class web search support. High probability of inclusion in an upcoming release.
- **Security Hardening ([#3297](https://github.com/sipeed/picoclaw/pull/3297))**  
  Though a fix, it introduces a schema v4 migration and new security boundaries — signals that remote agent safety is a focus area. This may land as a breaking change in the next minor version.

### 7. User Feedback Summary
- **Pain Points:**
  - Gateway startup failure when deltachat is not configured (Issue #3265) — confusion and blocked setup.
  - SplitMessage infinite loop (Issue #3264) — core channel functionality affected.
  - Token refresh failures with antigravity (PR #3267) — authentication reliability issue.
- **Use Cases:**
  - Exa web search integration (PR #3299) — users want richer web search capabilities.
  - AI Router as a preset (Issue #3298) — convenience for multi-provider routing.
  - Czech localization (PR #3296) — non-English user community is active.
- **Satisfaction:** The presence of multiple fix PRs suggests the maintainers are responsive. Stale items (e.g., #3252, #3265) may cause minor dissatisfaction if not addressed quickly.

### 8. Backlog Watch
The following items have been open for over a week without maintainer response or closure:

- **Issue [#3265](https://github.com/sipeed/picoclaw/issues/3265)** — Gateway startup failure (created 2026-07-19, last updated 2026-07-26). No assignee, no fix PR.
- **Issue [#3264](https://github.com/sipeed/picoclaw/issues/3264)** — SplitMessage hang (created 2026-07-18, last updated 2026-07-26). A fix PR (#3295) was opened today but not yet reviewed.
- **PR [#3202](https://github.com/sipeed/picoclaw/pull/3202)** — Routing normalization underscore stripping (created 2026-07-01, last updated 2026-07-26). Stale, awaiting maintainer review.

These items would benefit from maintainer prioritization, especially the gateway startup bug which could affect new users.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-27

## Today’s Overview
Activity remains high with 8 pull requests updated and 2 new issues filed in the last 24 hours. The project is in an active development cycle: two PRs were merged—a fix for duplicate replies and a feature for per-agent‑group timezone overrides—while six open PRs address messaging reliability, channel compatibility, and engagement controls. Two newly reported bugs related to silent message drops after a breaking change and incorrect `in_reply_to` assignment are urgent and lack fix PRs yet. No new releases were published today, and the maintainer team is heavily involved (four PRs carry the `core‑team` label).

## Releases
No new releases in the past 24 hours. The last breaking change mentioned in issues (explicit-destinations migration) appears to have been released earlier; the project is now dealing with its fallout.

## Project Progress
Two pull requests were merged/closed today:

- **[#3028 – Fix: avoid duplicate replies after send_message](https://github.com/nanocoai/nanoclaw/pull/3028)**  
  (merged, by ogarciarevett)  
  Stops the agent from emitting a second reply when `send_message()` already wrote a response to the triggering channel. A straightforward reliability fix for multi‑turn conversations.

- **[#3125 – Feat: per‑agent‑group timezone override](https://github.com/nanocoai/nanoclaw/pull/3125)**  
  (merged, core‑team, by Koshkoshinsk)  
  Adds an optional IANA timezone override per agent group, stored via `container_configs` (migration 020). Configuration is approval‑gated and resolution follows a fallback chain: group override → install global → UTC. This unblocks time‑sensitive agent behaviours without touching each skill.

## Community Hot Topics
All issues and PRs currently have 0 comments and 0 reactions, so no single thread dominates discussion. However, the following items have drawn core‑team attention and reflect pressing community needs:

- **[Issue #3140 – Explicit‑destinations migration breaks pre‑existing wirings](https://github.com/nanocoai/nanoclaw/issues/3140)**  
  Every reply in long‑standing chat groups is silently dropped after updating to require a named `to` destination. The absence of a migration path or error message for existing configurations is causing silent data loss.

- **[Issue #3136 – `sendToDestination` stamps foreign `in_reply_to`](https://github.com/nanocoai/nanoclaw/issues/3136)**  
  When a destination has no inbound history, `sendToDestination()` falls back to the waking batch’s `in_reply_to`, corrupting A2A return‑path routing. Reported by JoshuaJFogg, this explains lost messages in multi‑hop agent chains.

- **[PR #3137 – Fix engagement consistency and expose self‑serve wiring controls](https://github.com/nanocoai/nanoclaw/pull/3137)**  
  Introduces accumulated message context without triggering warm‑container turns, and lets group‑scoped agents inspect their wirings and request policy updates. This addresses a long‑standing power‑user request for finer‑grained engagement control.

## Bugs & Stability
Two high‑severity bugs were reported today:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#3140 – Silent drops after explicit‑destinations update](https://github.com/nanocoai/nanoclaw/issues/3140) | **Critical** – all replies in pre‑existing chat groups silently lost. No warning or error. | The mandatory `to` destination field was absent from old wirings, but the code silently drops the message rather than failing visibly. | ❌ No fix PR. |
| [#3136 – Foreign `in_reply_to` causes lost messages](https://github.com/nanocoai/nanoclaw/issues/3136) | **High** – corrupt routing metadata causes messages to disappear or arrive at wrong destinations. | `sendToDestination()` reuses the waking batch’s `in_reply_to` when the target destination has no inbound history, breaking A2A routing. | ❌ No fix PR. |

Additionally, an older bug (duplicate replies) was fixed today via PR #3028. The fix for WhatsApp shared‑number mode (PR #3139) is still open, and the team is working on a fix for delivering silence/thinking content (PR #3126).

## Feature Requests & Roadmap Signals
- **Per‑agent‑group timezone** (PR #3125, merged) – now live in `main`.
- **Dial channel integration** (PR #3050, open since July 14) – adds Dial as a channel in the setup wizard. Still awaiting review.
- **Opencode compatibility / custom‑endpoint transport** (PR #3122, open since July 23) – core‑team effort to fix memory parity and transport issues.
- **Self‑serve wiring controls** (PR #3137, open) – likely to be merged in the coming week, given its core‑team sponsorship and clear demand from advanced users.

Next minor release can be expected to bundle the timezone feature, the duplicate‑reply fix, and (if merged in time) the engagement consistency improvements.

## User Feedback Summary
- **Pain points:** The explicit‑destinations migration (recent breaking change) is causing silent message loss for users with existing wirings – no deprecation warning or migration guide. The `in_reply_to` bug creates confusing lost-message scenarios in multi‑agent setups.
- **Use cases:** Real‑world deployments with chat groups, WhatsApp shared‑number mode, and A2A agent chains are most affected.
- **Satisfaction:** No explicit positive feedback in the data, but the rapid core‑team response (multiple fix PRs open within hours) suggests a responsive project that values stability.

## Backlog Watch
| Item | Age | Status | Concern |
|------|-----|--------|---------|
| [PR #3050 – Dial channel integration](https://github.com/nanocoai/nanoclaw/pull/3050) | Opened July 14 (13 days) | Open, no core‑team review | Long‑dormant feature skill; may need attention to avoid merge conflicts. |
| [PR #3122 – Opencode compatibility](https://github.com/nanocoai/nanoclaw/pull/3122) | Opened July 23 (4 days) | Open, core‑team labelled | Active but no recent updates; compatibility fixes are critical for users on that platform. |
| [Issue #3136 – `sendToDestination` routing bug](https://github.com/nanocoai/nanoclaw/issues/3136) | Opened July 26 (1 day) | New, no fix yet | High severity; if no PR is raised within 48h, maintainers should prioritise. |

*All data as of 2026‑07‑27, sourced from the NanoClaw GitHub repository.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-27

## 1. Today's Overview
NullClaw saw minimal activity over the past 24 hours: one open issue was updated but remains unresolved, no pull requests were touched, and no new releases were published. The project’s surface-level momentum is low, but a critical crash bug (Issue #976) continues to affect users on aarch64 Linux, requiring urgent attention. Without any merged fixes or release candidates in sight, the stability of the `nullclaw gateway` service on ARM systems remains the primary concern.

## 2. Releases
No new releases were published today or in the recent past. The latest stable version remains **v2026.5.29** as referenced in the open crash report. No migration notes are available.

## 3. Project Progress
No pull requests were merged, closed, or even opened in the last 24 hours. No feature work or bug fixes have been officially integrated into the codebase.

## 4. Community Hot Topics
**Issue #976** [OPEN]  
*SIGSEGV on every inbound Telegram message — inbound worker thread spawned with a ~512 KB stack overflows*  
- Author: wonhotoss  
- Created: 2026-07-16 | Updated: 2026-07-26 | Comments: 3  
- Link: [nullclaw/nullclaw Issue #976](https://github.com/nullclaw/nullclaw/issues/976)

This is the only active discussion. The reporter describes a persistent segfault on aarch64 Linux that occurs with every inbound Telegram message. The thread stack size (512 KB) is suspected to be insufficient, causing a stack overflow when Telegram messages are processed. The three comments suggest community diagnosis is still ongoing; no maintainer commit or fix branch has been referenced.

**Underlying need**: Users running NullClaw on ARM hardware (common in self-hosted setups, e.g., Raspberry Pi) cannot reliably receive Telegram messages. The crash-loop pattern (the systemd service restarts but drops messages) makes the gateway effectively unusable. The community is seeking either a configurable stack size or a code-level fix in the inbound worker thread.

## 5. Bugs & Stability
- **Critical** — Issue #976: **SIGSEGV on every inbound Telegram message** (aarch64). The crash is consistent and prevents any Telegram interaction on ARM systems. The absence of a fix PR or a maintainer response increases the severity. A potential workaround (increasing thread stack size via configuration or runtime flags) has not been proposed by the team. This is the highest-priority stability concern in the project currently.

No other bugs, regressions, or crashes were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. The only signal from the community is the desire for a **configurable worker thread stack size** or a **safe default for aarch64**. If the maintainers act on Issue #976, the next patch release (maybe v2026.5.30 or v2026.6.x) is likely to include a stack size adjustment or a refactor of Telegram message handling to avoid deep recursion.

## 7. User Feedback Summary
- **Pain point**: aarch64 users (e.g., Raspberry Pi, ARM servers) cannot use NullClaw as a Telegram gateway because every message triggers a segfault. The crash-loop drops all messages, leading to total dissatisfaction with the service.
- **Use case affected**: Automated Telegram bots or personal assistants relying on `nullclaw gateway` for messaging.
- **Satisfaction**: Frustration is evident from the detailed crash report and the fact that the issue has been open for 10 days without a maintainer’s acknowledgment or a fix in progress.

## 8. Backlog Watch
No other long-unanswered issues or PRs appear in the data snapshot. Issue #976 is the sole item needing maintainer attention, and its 10-day age without a reply indicates a potential lack of active triage on this critical defect. Immediate outreach from the core team to at least acknowledge the problem would improve project health perception.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-27

## 1. Today’s Overview
High activity across the board: **5 open issues** and **18 PRs** touched in the last 24 hours, with **6 PRs merged/closed**. Development continues to focus on the error-recoverability epic (#6284), with two related PRs (#6684, #6681) advancing the failure vocabulary consolidation and mutation testing. A critical user-facing bug (#6690) was reported: the chat interface hangs forever when a user runs out of credits, with no notification. No new releases were cut. The project remains in heavy active development, with substantial architectural changes (credential security, signed intents, per-user MCP discovery) landing as PRs.

## 2. Releases
**No new releases** in this period. The most recent release candidate PR (#5598, opened July 3) is still open and pending final review.

## 3. Project Progress — Merged/Closed PRs Today
Six PRs were merged or closed (all but one appear to be actual merges):

- **#6679** — Harden struct ratchet and remove dead Gemini API. Uses `syn` parsing for multi-line attribute checking and adds regression coverage. *(core, merged)*
- **#6677** — Compile-forced recoverability conformance matrix (§11.7, essential for epic #6284). Adds `RecoverabilityClass` enum and exhaustive classifier for seven error enums. *(core, merged)*
- **#6640** — Bulk dependency bump (31 updates in the `everything-else` group). *(dependabot, merged)*
- **#4032** — WASM group dependency update (`wit-component` from 0.245.1 to 0.253.0). *(dependabot, merged)*
- **#5369** — Fix: suppress Cranelift debug log floods in Reborn, plus regression test. *(contributor: new, merged)*
- **#6365** — Reference PR for P2b per-user hosted-MCP discovery (closed, superseded by **#6683** which rebases on clean `main`). *(closed as superseded)*

**Notable progress on epic #6284:** The failure-kind enum collapse (#6684) and mutation test harness fix (#6681) remain open but signal strong forward motion.

## 4. Community Hot Topics

| Item | Comments | Topic |
|------|----------|-------|
| [Issue #6284](https://github.com/nearai/ironclaw/issues/6284) | **8 comments** | Epic: Error-recoverability endgame — model must recover from 100% of errors seen. |
| [Issue #6690](https://github.com/nearai/ironclaw/issues/6690) | 0 (new) | Chat hangs forever on empty credits, no user feedback. |
| [PR #6683](https://github.com/nearai/ironclaw/pull/6683) | 0 | Per-user hosted-MCP discovery (rebase of #6365). Large feature (XL). |

**Analysis:** The error-recoverability epic (#6284) is the dominant thread, driving at least three open PRs today (#6684, #6681, #6677 merged). This is an architectural push to guarantee that every runtime error is surfaced to the model with enough context to recover automatically — a foundational reliability feature for autonomous agents. No community discussion beyond the issue author and maintainers; the work appears internal.

## 5. Bugs & Stability

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#6690](https://github.com/nearai/ironclaw/issues/6690) | **Critical** | Out-of-credits causes chat to hang on “thinking…” indefinitely, with no notification. User is left in the dark. | ❌ No |
| [#6686](https://github.com/nearai/ironclaw/issues/6686) | Low | Dead code identification: `DockerProcessSandboxBackend` is uninstantiated and should be removed. | Possible removal PR pending. |
| [#6682](https://github.com/nearai/ironclaw/issues/6682) | Medium | Daily failure taxonomy report — identifies many model-quality partial completions as the dominant failure mode. Not a code bug, but a signal. | N/A |

**Priority:** #6690 is the most urgent — it directly blocks users from understanding why the agent stopped responding. No fix PR has been created yet.

## 6. Feature Requests & Roadmap Signals

Several architectural features in flight suggest near-future direction:

- **Credential security (#6689)** — A sandbox credential placeholder registry that ensures real secrets never enter the container. Likely to land in next release (size XL, risk low).
- **Attested signing Phase B (#6672)** — Signed intent + per-agent key lifecycle for Ledger integration. Important for verifiable agent actions; size XL, risk low.
- **Per-user hosted MCP discovery (#6683)** — Allows worker agents to get per-hire connector tools. Rebase of #6365 onto `main` — indicates this feature is a high priority.
- **Unified safe text (#6688)** — Collapses redundant model-visible text wrappers across several crates. Cleanup and standardisation work.

**Prediction for next release (based on open release PR #5598):** At least the credential registry (#6689) and safe text unification (#6688) are candidates, along with the error-recoverability conformance matrix already merged (#6677).

## 7. User Feedback Summary

Direct user feedback is sparse in this batch. Key pain points inferred from issues:

- **Credit exhaustion is invisible** — The report of chat hanging (#6690) indicates a critical usability gap. Users expect a clear error message when credits run out, not a silent freeze.
- **No other explicit user complaints** — Activity is dominated by internal engineering (dependency bumps, refactors). The daily failure taxonomy (#6682) suggests maintainers are proactively monitoring model quality, but user satisfaction data is absent.

## 8. Backlog Watch

| Item | Age | Issue |
|------|-----|-------|
| [PR #5598](https://github.com/nearai/ironclaw/pull/5598) | **24 days open** (since July 3) | Release PR for `ironclaw_common` (0.4.2→0.5.0, breaking) and `ironclaw_skills` (0.3.0→0.4.0, breaking). Stalled — no comments from maintainers after initial CI checks. This is blocking all downstream users from consuming new features. |
| [PR #5664](https://github.com/nearai/ironclaw/pull/5664) | 22 days open | Bulk update of 16 GitHub Actions (including `actions/checkout` from v4→v7, Claude code action). Could be important for CI reliability. |
| [PR #6428](https://github.com/nearai/ironclaw/pull/6428) | 6 days open | Tokio ecosystem bump (4 updates). Low risk, but older versions may carry unpatched issues. |
| [Issue #6284](https://github.com/nearai/ironclaw/issues/6284) | 8 days open (since July 19) | Epic with 8 comments but no assignee beyond the author. Despite active related PRs, the issue itself hasn't been formally assigned or triaged with milestones. |

**Maintainer attention needed:** The release PR #5598 is the highest-priority stale item — without it, users cannot benefit from the many improvements merged in the last three weeks.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-27

## 1. Today's Overview

LobsterAI shows a low-activity day with only 2 issues and 8 pull requests updated in the last 24 hours. No new releases were published. Development continues on the OpenClaw gateway stability, cowork UI improvements, and scheduled task features, but most PRs are stale (created in April 2026) and only one was closed today. The community remains quiet, with no significant spike in engagement. The project appears to be in a maintenance phase with incremental fixes rather than major feature launches.

## 2. Releases

*No new releases have been published.*

## 3. Project Progress

One pull request was closed/merged today:

- **PR #1325** (closed) — *feat(ui): add hover tooltip for “New Conversation” icon button*  
  Adds `title` attributes to the icon-only “New Conversation” button in sidebar, cowork view, session detail, agents view, and MCP view to improve discoverability. This is a small UX polish.

The remaining 7 open PRs were updated but remain open. They cover:

- **Gateway stability**: PR #1247 (fix OpenClaw model switch recovery after provider limits) and PR #1259 (refactor OpenClaw bundling and dependency handling) could help address the frequent restart bug reported in issue #1243.
- **Cowork diff rendering**: PR #1249 fixes the DiffView not rendering for Edit tool calls from Claude SDK and OpenClaw.
- **Scheduled task UX**: PRs #1252, #1256, and #1258 add unsaved-change confirmation dialogs, natural language scheduling, and cross-agent session migration for task forms.
- **i18n**: PR #1257 adds missing `edit` and `delete` translation keys.

None of these have been merged yet, suggesting need for further review.

## 4. Community Hot Topics

Activity in issues and PRs is very low. The only items with comments in the last 24 hours are:

- **Issue #273** (closed) — *[Suggestion] Can you develop an Ubuntu Linux version?*  
  Created in March 2026, the author requests Linux support. It has 2 comments and was closed (likely not yet planned). Link: [Issue #273](https://github.com/netease-youdao/LobsterAI/issues/273)

- **Issue #1243** (open, stale) — *[BUG] qwen-portal-auth plugin configuration loop write causes gateway frequent restart*  
  This critical bug report has 1 comment and significant impact on usability. The user describes the gateway restarting every 5–20 minutes. No maintainer response is visible. Link: [Issue #1243](https://github.com/netease-youdao/LobsterAI/issues/1243)

The lack of active discussion suggests the community is either satisfied or underserved. The few comments indicate users are reporting blockers but are not receiving prompt engagement.

## 5. Bugs & Stability

**High severity:**

- **Issue #1243**: Gateway restart loop triggered by `qwen-portal-auth` plugin config writes. Affects all versions on Windows 10/11. Reproducible with any model. This is a stability-critical regression that would severely impact production use. No dedicated fix PR exists, but PRs #1247 and #1259 may indirectly address aspects of gateway restart behavior. Maintainers should prioritize this.

**Low severity:**

- No other bugs reported today.

## 6. Feature Requests & Roadmap Signals

- **Linux support** (Issue #273) — The only explicit feature request. User demand for Ubuntu Linux compatibility remains unaddressed. Given the project’s Windows focus, this is likely not on the immediate roadmap unless community contributions emerge.
- **Natural language scheduling** (PR #1256) — If merged, this will allow users to describe task schedules in plain language (e.g., “every Monday at 9 AM”) and have it converted to cron expressions. This is a UX-enhancing feature expected in a future release.
- **Unsaved changes protection** (PRs #1252, #1258) — User interfaces for scheduled tasks will become safer. Likely to land together.

None of these are fully accepted, so no firm roadmap commitment yet.

## 7. User Feedback Summary

- **Pain point**: The gateway restart bug (Issue #1243) is the most vocal user complaint — it renders the application unusable for extended periods. The user mentioned a "popup saying 'AI engine is starting gateway…'" indicating poor error handling.
- **Satisfaction**: No positive feedback observed today. The tooltip improvement (PR #1325) was merged, suggesting maintainers are attentive to UI polish.
- **Unmet need**: The Linux request (Issue #273) remains unaddressed, likely disappointing some users.

Overall sentiment appears neutral to negative, dominated by the unresolved stability issue.

## 8. Backlog Watch

The following high-impact items are stale (last updated July 26, but created April 1–2, 2026) and deserve maintainer attention:

- **Issue #1243** (open since Apr 1) — Critical bug with gateway restart loop. No response from maintainers yet.
- **PR #1247** (open since Apr 1) — Fix for OpenClaw model switch recovery; could address #1243 but is blocked.
- **PR #1249** (open since Apr 1) — Fix for cowork DiffView; simple but stalled.
- **PR #1252** (open since Apr 1) — Scheduled task unsaved changes; useful UX but awaiting review.
- **PR #1256** (open since Apr 1) — Natural language scheduling; moderate complexity.
- **PR #1257** (open since Apr 1) — Missing i18n keys; trivial but stuck.
- **PR #1258** (open since Apr 1) — Duplicate of #1252; could be consolidated.
- **PR #1259** (open since Apr 1) — Gateway bundling refactor; may unblock other PRs.

The cluster of stale PRs from early April suggests a review bottleneck. Maintainers should triage these to either merge, request changes, or close as obsolete.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-27

## Today’s Overview

No issues were updated in the last 24 hours, and no new releases were cut. However, **eight pull requests** received updates, all remaining open and under review. Development activity is focused on expanding Moltis’s integration surface (ACP agent role, Nostr NIP-29 support, Slack Block Kit), hardening security (privileged tool gating), and improving the PWA user experience. The project is in a phase of **broad feature addition with simultaneous bug fixing** – a sign of active refinement alongside growth.

## Releases

No new releases today. The latest release remains the previous version; a version bump is likely once the pending PRs are merged.

## Project Progress

No PRs were merged or closed in the last 24 hours. All eight items remain open, but they represent concrete work toward:

- **New memory backend** – PR [#1158](https://github.com/moltis-org/moltis/pull/1158) adds an experimental Zvec + Redb vector database memory backend, gated behind a Cargo feature.
- **PWA notification reliability** – PR [#1173](https://github.com/moltis-org/moltis/pull/1173) fixes silent replacement of chat notifications and ensures non-disruptive alerts.
- **Model selector UI** – PR [#1171](https://github.com/moltis-org/moltis/pull/1171) integrates ACP client selection into the chat model picker, removing a redundant header selector.
- **ACP agent exposure** – PR [#1169](https://github.com/moltis-org/moltis/pull/1169) enables Moltis to act as an ACP agent over stdio, allowing external harnesses (Zed, buzz-acp) to use it.
- **Slack integration** – PR [#1166](https://github.com/moltis-org/moltis/pull/1166) adds per-message acknowledgment reactions, phase feedback, reconnect supervision, and Block Kit rendering.
- **Cron UI polish** – PR [#1172](https://github.com/moltis-org/moltis/pull/1172) hides archived cron sessions by default and adds Playwright regression tests.
- **Security hardening** – PR [#1170](https://github.com/moltis-org/moltis/pull/1170) gates the `/sh` command and other privileged tools behind a per-account operators list.
- **Nostr NIP-29 support** – PR [#1168](https://github.com/moltis-org/moltis/pull/1168) adds group chat support for Buzz channels via NIP-29 and NIP-42 authentication.

## Community Hot Topics

None of the eight PRs received comments or reactions in the last 24 hours. However, the topics themselves indicate strong community-aligned needs:

- **Security** – The `/sh` gating (PR [#1170](https://github.com/moltis-org/moltis/pull/1170)) addresses a real concern for Discord guilds and group chats.
- **Reliable push notifications** – PR [#1173](https://github.com/moltis-org/moltis/pull/1173) tackles a UX bug that silently dropped alerts, likely a high-impact pain point for PWA users.
- **Cross-platform agent usability** – PR [#1169](https://github.com/moltis-org/moltis/pull/1169) makes Moltis usable as an agent by external tools, expanding its ecosystem relevance.

## Bugs & Stability

Three PRs directly address bugs. Ranked by severity:

1. **Critical – Unauthorized command execution** ([#1170](https://github.com/moltis-org/moltis/pull/1170)): The `/sh` command was reachable by any chat member who passed the channel’s access gate, enabling arbitrary host command execution. A fix exists and is under review.
2. **High – Silent notification replacement** ([#1173](https://github.com/moltis-org/moltis/pull/1173)): PWA push notifications without `renotify` silently replaced earlier messages, losing sound and alert. Fix included.
3. **Medium – Cluttered cron UI** ([#1172](https://github.com/moltis-org/moltis/pull/1172)): Archived cron sessions were always visible; now hidden by default with a toggle.

No crashes or regressions were reported in the last 24 hours.

## Feature Requests & Roadmap Signals

The open PRs themselves are the strongest roadmap signals for the next release:

- **Vector database backend** (Zvec + Redb) – provides an alternative to pgvector, useful for self-hosted setups without PostgreSQL.
- **ACP agent mode** – makes Moltis a first-class citizen in the ACP ecosystem, likely enabling new integration patterns.
- **Nostr NIP-29 group chat** – aligns with the growing Buzz workspace ecosystem, targeting agent-human team communication.
- **Slack Block Kit** – brings rich interactive messages and proper phase feedback, improving Slack UX.

These features suggest the next version will emphasize **interoperability** (ACP, Nostr), **UI/UX polish** (PWA, Slack, Cron), and **security** (operator lists).

## User Feedback Summary

No direct user feedback was recorded in issues or PR comments today. However, the fixes and features clearly target reported pain points:

- **Pain**: “Notifications silently disappear” → addressed by [#1173](https://github.com/moltis-org/moltis/pull/1173).
- **Pain**: “Anyone on the server can run arbitrary commands via `/sh`” → addressed by [#1170](https://github.com/moltis-org/moltis/pull/1170).
- **Pain**: “Archived cron sessions clutter the list” → addressed by [#1172](https://github.com/moltis-org/moltis/pull/1172).
- **Use case**: “I want to use Moltis inside Buzz / with external ACP harnesses” → addressed by [#1169](https://github.com/moltis-org/moltis/pull/1169) and [#1168](https://github.com/moltis-org/moltis/pull/1168).

Satisfaction signals are implicit in the continued development of these features; no expressions of dissatisfaction were posted.

## Backlog Watch

No long-unanswered issues exist (zero issues in the last 24 hours). Among open PRs, **#1158** (zvec memory backend) was created on **2026-07-17** – 10 days ago – and has not been merged. Its experimental nature may require more review. All other PRs are from the last three days and are actively maintained. No item currently appears neglected.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-27

## 1. Today's Overview

The CoPaw project (QwenPaw repository) saw moderate activity over the past 24 hours: 12 issues were updated (11 still open, 1 closed) and 9 pull requests were updated (all still open, none merged). No new releases were published. The community remains engaged, with several bug reports affecting core functionality — notably the MCP transport configuration being ignored and the `view_video` tool silently failing to deliver video content to the model. Encouragingly, multiple first-time contributors submitted fix PRs (e.g., for the cron misfire bug and for adding Traditional Chinese localization), signalling a healthy contributor pipeline. However, no PRs were merged today, suggesting maintainers may be in a review-heavy phase.

## 2. Releases

No new releases today. The latest publicly available version remains 2.0.1 (as referenced in several recent issue reports).

## 3. Project Progress

No pull requests were merged or closed today. However, several open PRs directly address recently reported bugs and represent tangible progress toward stability and feature completion:

- **#6481** (fix/crons) — Adds a keepalive task to prevent cron job misfires when the asyncio event loop is idle (fixes #6471).
- **#6483** (test/MCP transport) — Adds regression tests for the streamable HTTP transport selection (addresses #6470). The current `main` branch already contains a partial fix; this PR locks it down.
- **#6484** (i18n) — Implements Traditional Chinese (zh-TW) localization for the console and website (closes #6478).
- **#6477** (docs) — Aligns Chinese FAQ sub-section headings with the English version (cosmetic fix).
- **#6479** (providers) — Updates the hardcoded MiniMax model lists to match the current official lineup.

Other long-standing feature PRs (#6456 Visual Compact, #6387 on-demand channel installation, #6276 unified browser, #6284 QwenPaw Creator app) remain open and under review.

## 4. Community Hot Topics

The most active discussion this period centers on **Issue #6470** (4 comments) — the MCP driver hardcodes `sse_client` and ignores the `transport: streamable_http` configuration, breaking connectivity for servers using the Streamable HTTP protocol. The issue has attracted a fix PR (#6483) from a first-time contributor, which suggests the community is actively collaborating on root-cause analysis.

Another noteworthy thread is **Issue #6342** (3 comments, closed, 1 👍) — a user asking how to verify that the ReMe embedding model is actually being used. The maintainers provided guidance, but the underlying desire for observable vector storage files hints at a documentation gap.

**Issue #6239** (3 comments) — Windows PATH concatenation drops the semicolon separator between User and Machine PATH entries, causing child processes to lose npm global directories. This affects developers using Node.js tools inside QwenPaw. No fix PR has emerged yet.

The only PR with explicit contributor notes is **#6456** (Visual Compact) — a relatively large feature that has been open for several days and may be nearing the top of the review queue.

## 5. Bugs & Stability

Today’s bug reports span a range of severities:

| Severity | Issue | Title | Fix PR exists? |
|----------|-------|-------|----------------|
| **Critical** | #6470 | MCP driver ignoring `transport` config — broken Streamable HTTP | Yes (#6483) |
| **Critical** | #6474 | `view_video` returns success but video is never sent to the LLM | No |
| **High** | #6471 | Cron tasks misfire after long idle periods (APScheduler AsyncIOScheduler) | Yes (#6481) |
| **High** | #6473 | Plugin “Agent Kanban” fails to install on Desktop 2.0.1 due to missing module | No |
| **Medium** | #6476 | Matrix end-to-end encryption broken (olm/vodozemac installation fails) | No |
| **Medium** | #6480 | `nohup` / background shell commands never return agent to idle state | No |
| **Medium** | #6482 | Console UI lags when switching chat/agent and shows stale content | No |
| **Low** | #6472 | JSON files in programming mode lost line numbers after upgrade to 2.0.1 | No |

The most critical is #6474: the `view_video` tool declares success, but no formatter serializes a video DataBlock into the LLM API request. This means models capable of video understanding never actually receive the video — a silent data loss bug that undermines the multimodality promise.

The three bugs with associated fix PRs (#6470, #6471) are likely to be resolved soon if the PRs are merged.

## 6. Feature Requests & Roadmap Signals

The strongest roadmap signal comes from **Issue #6475** — a user request for a `notice_after_complete` tool that would allow agents to start a long-running task (e.g., shell command, sub‑agent), immediately reply to the user, and then push a completion notification later. This feature would enable true asynchronous multi-turn workflows. Given its alignment with QwenPaw’s ongoing agent orchestration improvements (see PR #6456 Visual Compact and the async‑capable browser SDK #6276), it is a plausible candidate for the next minor release (2.1.0).

**Issue #6478** (Traditional Chinese) was already implemented by the same user who submitted PR #6484 — a good example of community-driven localization that will likely be merged this week.

Other signals:
- **Windows-specific enhancements** (#6239 PATH fix, #6482 UI lag) remain unaddressed but are frequently reported pain points.
- **Plugin ecosystem** demand is growing: the failure of an official plugin to install (#6473) highlights the need for better dependency management — exactly what PR #6387 (on-demand channel installation) aims to solve.

## 7. User Feedback Summary

User feedback this period reveals a mix of pain and contribution:

- **Configuration confusion**: Users struggle to verify that embedding models (#6342) or transport settings (#6470) are actually applied. The lack of observable artifacts (e.g., vector store files) and silent misbehaviour (MCP connection failures) erodes trust.
- **Windows struggles**: At least two distinct issues (#6239, #6482) are Windows-specific (PATH concatenation, UI lag). One user reported that switching agents in the Console causes persistent ghost content — a UX regression in 2.0.1.
- **Asynchronous workflow desire**: Multiple users (#6475, #6480) want agents to handle long-running tasks without freezing the conversation. The current blocking behaviour is a major workflow blocker.
- **Positive community engagement**: First-time contributors submitted PRs for i18n (#6484), cron fix (#6481), test coverage (#6483), and provider updates (#6479). This indicates a welcoming environment and clear documentation of how to contribute.

## 8. Backlog Watch

The following items have been open for several days without a maintainer response or fix PR:

- **Issue #6239** (Windows PATH concatenation) — open since July 18, last updated July 26, 3 comments, no PR. Affects users relying on Node.js/npm tools. Maintainer attention needed.
- **Issue #6342** (closed) — though closed, the underlying question of embedding verification suggests a documentation improvement. The community answer was “check logs”, but no explicit guide exists.
- **PR #6276** (unified browser) — open since July 20, last commented July 26. A large architectural change with no review activity for 6 days. May be blocked awaiting feedback.
- **PR #6284** (QwenPaw Creator app) — open since July 20, last activity July 26. Marked “Under Review” but no reviewer comments. Potential integration with upcoming release.

No critical issue has been left completely unattended: the most severe bugs (#6470, #6471) already have open fix PRs.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-27

## 1. Today's Overview
The project is experiencing **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. No new releases were cut, but the repository shows intense collaborative effort around critical bug fixes, security hardening, and release preparation. Two PRs were merged/closed, including a landlock sandbox fix (#9233). All 50 issues remain open, indicating a strong focus on triage and resolution rather than closure. The **CI and cross-platform compatibility** (especially Windows) are the most prominent pain points, alongside memory-safety and sandbox enforcement issues.

## 2. Releases
**None.** No new releases were published in the last 24 hours. The latest release remains v0.8.3 (no data provided beyond this digest’s scope).

## 3. Project Progress
Only **2 PRs were merged/closed** in the last 24 hours. The most notable is:
- **#9233 [CLOSED]** – *fix(runtime/security): Prevent landlock locks zeroclaw itself* – Merged a critical fix that prevents the Landlock sandbox from locking the ZeroClaw daemon itself. This is a high-risk, size-M PR that addresses a regression reported in issue #8973.  
  [zeroclaw-labs/zeroclaw PR #9233](https://github.com/zeroclaw-labs/zeroclaw/pull/9233)

Other PRs remain open and in review, covering security, channel fixes, release automation, and documentation.

## 4. Community Hot Topics
The most active discussions revolve around **cross-platform testing failures** and **release attestation consolidation**:

- **Issue #7462** (14 comments) – *[Bug]: 74 test failures on Windows* – Generated intense debate about CI coverage and path semantics. The user community is pressing for Windows/macOS test matrix inclusion.  
  [zeroclaw-labs/zeroclaw Issue #7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)

- **Issue #9101** (7 comments) – *Consolidate release attestation mechanisms* – A high-priority initiative to reduce CI redundancy from three parallel signing mechanisms down to one, freeing CI time and reducing asset count from 53 to ~20.  
  [zeroclaw-labs/zeroclaw Issue #9101](https://github.com/zeroclaw-labs/zeroclaw/issues/9101)

Among PRs, several are drawing attention:
- **PR #8826** – *fix(tools): gate image_gen download URL against SSRF* – A security-sensitive fix for a potential server-side request forgery via fal.ai responses.  
  [zeroclaw-labs/zeroclaw PR #8826](https://github.com/zeroclaw-labs/zeroclaw/pull/8826)

- **PR #9420** – *fix(anthropic): support stored OAuth profiles* – Adds explicit OAuth support for Anthropic while preserving legacy API key aliases.  
  [zeroclaw-labs/zeroclaw PR #9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420)

- **PR #9376** – *chore(release): cut v0.8.4 — crates.io publishing, changelog, crate removals* – A major release preparation PR aiming to make the workspace publishable to crates.io for the first time since the microkernel split.  
  [zeroclaw-labs/zeroclaw PR #9376](https://github.com/zeroclaw-labs/zeroclaw/pull/9376)

## 5. Bugs & Stability
Several **high-severity bugs** are active, many with fix PRs in progress:

| Bug | Severity | Description | Fix Status |
|-----|----------|-------------|------------|
| **#7462** | S2 (degraded) | 74 test failures on Windows due to Unix-only commands, path semantics, console encoding | No fix PR yet; tracked by #7461 (CI matrix) |
| **#8654** | S1 (workflow blocked) | Skill-review fork panics with out-of-range slice → SIGSEGV after tool-heavy turn | In progress |
| **#8559** | S1 (workflow blocked) | Agents stop when exiting web chat window, breaking long-running tasks | In progress |
| **#8973** | S2 (degraded) | Landlock blocks shell access to /dev/null on Fedora | Fixed by #9233 (merged); follow-up #9114 open |
| **#9386** | S1 (workflow blocked?) | Gemini API key leaked via reqwest error display into user-facing chat | Newly reported, no fix yet |
| **#8642** | S1 (workflow blocked) | MCP/tool-schema cloning causes unbounded RSS growth in agent loop | In progress |
| **#8731** | S2 (degraded) | Stdio-based MCP servers accumulate as zombie processes | In progress |
| **#9085** | S1 (workflow blocked) | Nested panic in `try_enable_pgvector` when pgvector enabled | In progress |
| **#8560** | S1 (workflow blocked) | `browser_open` hangs indefinitely on headless hosts | In progress |
| **#9035** | S1 (workflow blocked) | Docker Compose gateway remains loopback-bound behind published port | In progress |

**Notable fix PRs:** #9233 (merged, landlock fix), #9114 (landlock follow-up), #8826 (SSRF gate), #9385 (WhatsApp approval enforcement), #9181 (Nextcloud Talk bot API fix), #9410 (default command audit logging disabled).

## 6. Feature Requests & Roadmap Signals
Several features indicate the direction of the next release (likely v0.8.4):

- **#9101** – *Consolidate release attestation mechanisms* – High-priority CI simplification.
- **#7108** – *Improve cached Rust builds and CI critical path* – Performance improvement for CI.
- **#7461** – *Run test suite on Windows and macOS in CI* – Expanding test matrix.
- **#8409** – *cron shell jobs raw stdout output* – User-requested feature for job output flexibility.
- **#8337** – *herdr agent reporting integration* – Observability integration.
- **#7099** – *Route zeroclaw status output through CLI i18n* – Localization improvement.
- **#9420** – *Anthropic OAuth profiles* – Provider authentication enhancement.
- **#9419** – *Rotate live credentials after rate limits* – Resilience improvement for provider rate limiting.
- **#9418** – *Multiplex stdio MCP calls without replaying unknown outcomes* – MCP concurrency fix.

These suggest the next version will focus on **CI reliability, security hardening, provider credential management, and cross-platform support**.

## 7. User Feedback Summary
Users report **severe pain points** that block workflows:

- **Windows users** cannot reliably run tests or the daemon due to 74 test failures and CI blind spots (Issue #7462).
- **Telegram users** report that sending multiple images triggers per-image agent responses instead of a single multimodal turn (Issue #5514).
- **Nextcloud Talk users** cannot send replies correctly because the wrong bot API is used (Issue #6157; fix PR #9181 open).
- **Docker users** find the gateway unreachable behind published ports (Issue #9035).
- **Landlock sandbox** breaks shell access on Fedora (Issue #8973), now fixed in #9233.
- **MacOS desktop app** can reopen blank or without a window (Issue #7527), still waiting for reproduction.
- **Users of Bedrock Nova 2 Lite** hit random cache errors that cannot be disabled via config (Issue #8720).
- **Several users** report memory leaks and zombie processes from MCP servers (Issues #8642, #8731).

Overall, the community is **active and engaged** but encountering **production-blocking issues** that require immediate attention. The maintainers are responsive, with many fix PRs in flight.

## 8. Backlog Watch
The following important issues have been open for **weeks** without resolution or significant progress:

- **#7462** (Windows test failures) – Open since June 10; despite high comments and priority, no fix PR exists.
- **#5514** (Telegram media groups) – Open since April 8; a low-severity but long-standing UX issue.
- **#6157** (Nextcloud Talk API) – Open since April 27; fix PR #9181 is awaiting author action.
- **#6350** (WhatsApp allowed-numbers bypass) – Open since May 3; high-risk security bug.
- **#7527** (macOS blank window) – Open since June 12; blocked on reproduction.
- **#7828** (UTF-8 truncation audit) – Open since June 17; tracker issue with no visible progress.
- **#7870** (Runtime options leak) – Open since June 17; another tracker.
- **#7911** (Android/Termux install) – Open since June 18; user waiting for binary selection.
- **#8519** (CVE reconciliation) – Open since June 30; security-related but not moving.

These items deserve **maintainer prioritization**, especially the ones with security implications (#6350, #8519) and those blocking whole platforms (#7462, #7911).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*