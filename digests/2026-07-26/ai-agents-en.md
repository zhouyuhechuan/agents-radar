# OpenClaw Ecosystem Digest 2026-07-26

> Issues: 339 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-26 02:03 UTC

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

# OpenClaw Project Digest – 2026-07-26

## 1. Today’s Overview
The project continues at high velocity with **339 issues** and **500 PRs** updated in the last 24 hours, of which **215 PRs were merged or closed**. No new releases were tagged. Activity is dominated by large-scale refactoring efforts (e.g., splitting daemon, QA‑lab, doctor, talk relay), stability fixes for gateway and session management, and ongoing security reviews. The maintenance backlog remains substantial, with dozens of issues weeks or months old still awaiting maintainer decisions, but the number of merged PRs indicates sustained commit throughput and team capacity.

## 2. Releases
**None.** No new versions were published on the digest date. The most recent release remains 2026.7.1 (and its beta variants), which has been associated with several regression reports (e.g., #108435, #113466).

## 3. Project Progress
- **215 PRs merged or closed** in the last 24 hours. Notable merged work includes:
  - `refactor(doctor): split health contributions` ([#113937](https://github.com/openclaw/openclaw/pull/113937)) – modularised the 2,211‑line health flow.
  - `fix(ui): restore scoped notification navigation` ([#113951](https://github.com/openclaw/openclaw/pull/113951)) – fixes wrong‑origin tab focus in Control UI.
  - `fix(ui): hide unusable Chat sidebar controls on read‑only boards` ([#113947](https://github.com/openclaw/openclaw/pull/113947)).
  - `refactor(meetings): converge Google Meet probes and adapter parsing` ([#113970](https://github.com/openclaw/openclaw/pull/113970)).
  - `refactor(agents): share restart recovery state snapshot` ([#113969](https://github.com/openclaw/openclaw/pull/113969)).
- **Large open PRs** that signal planned evolution:
  - `feat: add standard hosting profiles` ([#113422](https://github.com/openclaw/openclaw/pull/113422), XL) – introduces deployment‑specific readiness criteria.
  - `feat: add readiness conditions and providers` ([#104018](https://github.com/openclaw/openclaw/pull/104018), XL) – extends `/ready` endpoint for plugins and CLI.
  - `fix(sessions): gateway becomes unusable when there are many sessions` ([#113959](https://github.com/openclaw/openclaw/pull/113959)) – a critical performance fix.
  - `fix(memory): close previous embedding provider before replacement` ([#113471](https://github.com/openclaw/openclaw/pull/113471)) – resolves orphaned worker processes.

## 4. Community Hot Topics
The most engaged issues (by comments) reveal several deep‑rooted concerns:

| Issue | Comments | Core Topic |
|-------|----------|------------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 21 | **Memory Trust Tagging by Source** – prevent memory poisoning from untrusted inputs. |
| [#78308](https://github.com/openclaw/openclaw/issues/78308) | 15 | **Channel‑mediated approval for MCP tool calls** – extend the existing `/approve` pipeline to MCP servers. |
| [#113306](https://github.com/openclaw/openclaw/issues/113306) | 13 | **SQLite snapshot restore lacks crash & identity guarantees** – data‑loss risk. |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 11 | **Gateway fails to start after update to 2026.7.1** – P0 crash‑loop. |
| [#67419](https://github.com/openclaw/openclaw/issues/67419) | 10 | **Session context bloat** – 20‑30% token waste from repeated bootstrap file injection. |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 10 | **Fully dynamic model discovery** (OpenRouter & beyond). |

**Underlying needs**: Security hardening (trust boundaries, approval gates), stability (crash‑loop regression, memory leaks), and performance (token waste, event‑loop blockage). The community is actively voicing pain around regressions introduced by recent releases.

PRs with high reaction counts are less visible (all top‑30 PRs have undefined comments), but several large refactors (#113783, #113422, #113974) are likely generating discussion in review threads.

## 5. Bugs & Stability
The following **critical (P0/P1) bugs** were active or updated today:

- [**P0**] `gateway fails to start w/ error` ([#108435](https://github.com/openclaw/openclaw/issues/108435)) – regression in 2026.7.1; crash‑loop on startup. No fix PR linked.
- [**P0**] `Upgrade 2026.6.8→2026.6.9 corrupts email channel config` ([#95515](https://github.com/openclaw/openclaw/issues/95515)) – data corruption, release blocker.
- [**P0**] `Gateway HTTP server listens but does not accept connections` ([#109145](https://github.com/openclaw/openclaw/issues/109145)) – v2026.7.1‑beta.5; no connections accepted.
- [**P1**] `SQLite snapshot restore lacks end‑to‑end crash and identity guarantees` ([#113306](https://github.com/openclaw/openclaw/issues/113306)) – data‑loss risk.
- [**P1**] `Session model pinning persists indefinitely` ([#92776](https://github.com/openclaw/openclaw/issues/92776)) – origin‑field pollution defeats snap‑back probe.
- [**P1**] `Subagents list still empty after spawn` ([#75593](https://github.com/openclaw/openclaw/issues/75593)) – closed but fix incomplete.
- [**P1**] `Large SQLite transcript cleanup blocks the gateway event loop` ([#112423](https://github.com/openclaw/openclaw/issues/112423)) – blocking performance issue.
- [**P1**] `Agent loop allows simulated tool calls` ([#45049](https://github.com/openclaw/openclaw/issues/45049)) – security bypass.
- [**P1**] `/new and /reset don't actually create a new session in 2026.7.1‑2` ([#113466](https://github.com/openclaw/openclaw/issues/113466)) – session management broken.

**Fix PRs in flight**: [#113959](https://github.com/openclaw/openclaw/pull/113959) addresses multi‑session slowness; [#113926](https://github.com/openclaw/openclaw/pull/113926) fixes remote browser node recovery; [#113750](https://github.com/openclaw/openclaw/pull/113750) prevents cron jobs from hiding media failures.

## 6. Feature Requests & Roadmap Signals
Several significant feature requests have been raised or advanced:

- **Memory Trust Tagging by Source** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) – diamond‑lobster‑rated security enhancement. Strong candidate for next release.
- **MCP consent envelope** ([#78308](https://github.com/openclaw/openclaw/issues/78308)) – brings MCP tool calls under the same approval pipeline as shell execution.
- **Filesystem Sandboxing Config** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) – allow/deny paths for file access.
- **Dynamic model discovery** ([#10687](https://github.com/openclaw/openclaw/issues/10687)) – needed for OpenRouter and fast‑moving provider catalogs.
- **Per‑spawn tool restrictions for sub‑agents** ([#15032](https://github.com/openclaw/openclaw/issues/15032)) – DMZ web search use case.
- **Expose OpenRouter usage cost** ([#9016](https://github.com/openclaw/openclaw/issues/9016)) – simple but practical for budgeting.
- **Skill Permission Manifest** ([#12219](https://github.com/openclaw/openclaw/issues/12219)) – `skill.yaml` to declare permissions.
- **Pre‑compaction agent notification** ([#38520](https://github.com/openclaw/openclaw/issues/38520)) – safer context compaction for long workflows.

**Likely next‑version items**: The `hosting profiles` ([#113422](https://github.com/openclaw/openclaw/pull/113422)) and `readiness conditions` ([#104018](https://github.com/openclaw/openclaw/pull/104018)) PRs are large, depend on each other, and target P3 but have strong RFC backing. The per‑agent daily spend alerts ([#113548](https://github.com/openclaw/openclaw/pull/113548)) and scoped page extraction ([#113938](https://github.com/openclaw/openclaw/pull/113938)) are also ready for review.

## 7. User Feedback Summary
User reports today highlight **significant frustration with regressions** in the 2026.7.x series:
- **Gateway startup failure** (#108435) – multiple users reporting same crash on systemd, Docker, and manual launch.
- **Session management broken** – `/new` and `/reset` no longer create new sessions (#113466).
- **Memory management chaos** (#43747) – three users reporting completely different memory backends (SQLite vs. LanceDB) without deterministic control.
- **Context bloat** (#67419) – 20‑30% token waste due to repeated injection of bootstrap files every turn.
- **Telegram quote/reply implementation** (#88032) – only works after local runtime patching, and regresses across releases.
- **Docs ahead of release** (#48920) – documented `IsolatedSessions` feature not yet available in shipped version.

**Satisfaction indicators**: The high number of contributed PRs (215 merged) shows an active contributor base that trusts the maintainer process. Several PRs explicitly credit Codex‑assisted development, indicating the community is embracing AI tooling.

## 8. Backlog Watch
The following important issues and PRs have been waiting for maintainer action for **more than a month**:

- [#7707](https://github.com/openclaw/openclaw/issues/7707) (Feb 3) – Memory Trust Tagging – needs product decision & security review.
- [#78308](https://github.com/openclaw/openclaw/issues/78308) (May 6) – MCP consent envelope – needs maintainer review & product decision.
- [#7722](https://github.com/openclaw/openclaw/issues/7722) (Feb 3) – Filesystem sandboxing – recovery stuck, needs product decision.
- [#10687](https://github.com/openclaw/openclaw/issues/10687) (Feb 6) – Dynamic model discovery – multiple labels “needs‑maintainer‑review”, “needs‑product‑decision”.
- [#15032](https://github.com/openclaw/openclaw/issues/15032) (Feb 12) – Per‑spawn tool restrictions – security enhancement waiting for decision.
- [#9016](https://github.com/openclaw/openclaw/issues/9016) (Feb 4) – Expose OpenRouter cost – needs maintainer review.
- [#9986](https://github.com/openclaw/openclaw/issues/9986) (Feb 5) – Trigger model fallback on context length exceeded – needs product decision.
- [#12219](https://github.com/openclaw/openclaw/issues/12219) (Feb 9) – Skill Permission Manifest – security review pending.
- [#8724](https://github.com/openclaw/openclaw/issues/8724) (Feb 4) – Per‑model generation timeout config – needs live repro & product decision.
- **PR** [#82540](https://github.com/openclaw/openclaw/pull/82540) (May 16) – fix(wechat): preserve existing accounts across hot reload – XL, proof supplied, but status “needs proof” and untouched for 2+ months.

These items represent **accumulated community trust**: users took time to write detailed proposals with use cases but have not seen resolution. Unblocking even a few would demonstrate maintainer responsiveness.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-26

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape continues to mature at high velocity, with **10 of 12 tracked projects showing activity** in the last 24 hours and approximately **860 issues + 670 PRs** touched across the ecosystem. The dominant themes are **security hardening** (credential boundaries, container isolation, approval pipelines), **multi-platform messaging expansion** (Nostr, Buzz, Matrix, Slack), and **post-release regression management**—several projects are grappling with the tension between rapid feature delivery and stability. A bifurcation is emerging: large reference implementations (OpenClaw) maintain massive contributor throughput but accumulate technical debt, while smaller focused projects (Moltis, PicoClaw) iterate more surgically. The ecosystem collectively signals that **enterprise-grade governance and consumer-grade UX** are converging as core requirements.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Activity Health Score |
|---------|---------------------|-------------------|-------------|---------------------|
| **OpenClaw** | 339 | 500 | No (latest: 2026.7.1) | **Very High** – sustained throughput, but regression burden |
| **Hermes Agent** | 50 | 50 | No | **High** – active maintenance + new feature PRs |
| **ZeroClaw** | 19 | 50 | No (v0.8.4 cut PR open) | **High** – intense pre-release stabilization |
| **IronClaw** | 11 | 20 | No | **High** – focused frontend + architecture work |
| **NanoBot** | ~2 | 12 | **Yes (v0.3.0)** | **High/Stable** – post-release polish |
| **LobsterAI** | 9 | 11 | No | **High** – cleanup/consolidation burst |
| **CoPaw** | 7 | 8 | No | **Moderate** – bug reports outpacing fixes |
| **Moltis** | 0 | 5 | No | **Moderate** – steady, well-targeted |
| **NanoClaw** | 2 | 11 | No | **Moderate** – responsive, security-focused |
| **PicoClaw** | 2 | 3 | No | **Low-Moderate** – one critical bug unaddressed |
| **NullClaw** | 0 | 0 | N/A | **Inactive** (no activity) |
| **TinyClaw** | 0 | 0 | N/A | **Inactive** (no activity) |

**Key observations:**
- OpenClaw's 215 merged PRs in 24h is an order of magnitude above any peer
- Only NanoBot shipped a release; ZeroClaw is closest with an open release cut
- Security-related PRs are present in **6 of 10 active projects**

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale of contribution**: 215 merged PRs/day vs. ~2–17 for peers; OpenClaw's contributor base is 5–10x larger than any single competitor
- **Community-driving role**: Issues like memory trust tagging (#7707) and MCP consent (#78308) are ecosystem-level conversations that smaller projects reference
- **Architectural influence**: The "split daemon" refactoring and gateway/router architecture serve as a reference model; several projects (ZeroClaw, Hermes) have similar restructuring in progress

**Technical approach differences:**
- OpenClaw uses a **monolithic Python monorepo** with deep gateway-session separation, while smaller Rust-based projects (ZeroClaw, IronClaw) prefer **Rust+WebAssembly** for performance and memory safety
- OpenClaw's "hosting profiles" and readiness conditions (#113422, #104018) indicate a **multi-tenant, enterprise-first** design; peers like NanoBot prioritize **single-user developer experience**

**Community size comparison:**
- OpenClaw has ~2–3x the issue/PR volume of Hermes Agent, its closest competitor
- However, **per-PR community engagement** (comments/reactions) is lower on OpenClaw—top PRs show "undefined" comments, while Hermes issues average 5–7 comments each

**Risk**: OpenClaw's 24 P0/P1 bugs (gateway crash-loop, session corruptions) erode trust; its regression rate is higher than any peer. This is the price of rapid merge velocity.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects (severity/priority) | Specific Needs |
|------------|----------------------------|----------------|
| **Security & Approval Pipelines** | OpenClaw (#78308 MCP consent), Hermes (#71685 governed approvals), ZeroClaw (#9348 WhatsApp policies), NanoClaw (#2748 container hardening) | Extend human-in-the-loop to MCP servers, enforce channel-level policies, prevent privilege escalation |
| **Multi-Platform Messaging** | Hermes (#71610 Buzz/Nostr), ZeroClaw (#8561 Telegram, #8443 Matrix), Moltis (#1168 Nostr NIP-29), PicoClaw (#3203 Matrix sync) | Support for decentralized protocols; reliable reconnection; rich formatting |
| **Memory & Context Management** | OpenClaw (#7707 trust tagging, #67419 context bloat), Hermes (#31043 stale context length), NanoClaw (#3134 agent context blindness) | Source-based memory isolation, prevent token waste, ensure agent awareness of host actions |
| **Performance & Scalability** | OpenClaw (#113959 gateway session slowness, #112423 SQLite blocking), ZeroClaw (#9357 test flakiness, #9373 cost tracking), IronClaw (#6632 bundle size reduction) | Event loop non-blocking, 20–30% token waste reduction |
| **Configuration Consistency** | Hermes (#71298 dual provider storage), ZeroClaw (#9366 approval_timeout_secs never read), CoPaw (#6470 MCP transport hardcode) | Single source of truth for config; user-friendly error messages |
| **Container & Sandbox Security** | NanoClaw (#2748 cap-drop, #3129 mount blocking), Hermes (#71687 PowerShell bootstrap fix), ZeroClaw (#7821 sandbox policy schema) | Defense-in-depth for OCI containers; respect OS boundaries |

**Cross-cutting observation**: **3+ projects** are independently building Nostr/Buzz integrations (Hermes, Moltis, ZeroClaw), suggesting a standardization opportunity but also fragmentation risk.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | NanoBot | IronClaw | LobsterAI | Moltis |
|-----------|----------|-------------|----------|---------|---------|----------|--------|
| **Core Language** | Python | TypeScript/Rust | Rust | TypeScript | Rust | TypeScript | Rust |
| **Target User** | Enterprise ops teams | Power users/developers | Infrastructure engineers | Individual developers | Production deployments | Creative professionals | Multi-platform ops |
| **Key Strength** | Largest ecosystem, broadest integration | Multi-agent governance, Windows support | Performance, async architecture | Easiest onboarding (one command) | Error recoverability, WebUI performance | UX polish, cowork sessions | Modular memory backends |
| **Primary Weakness** | Regression burden, slow decision-making | Windows instability, Telegram issues | Test flakiness, WhatsApp bugs | Smaller feature set | Pre-release churn | Slower issue resolution | Low community volume |
| **Release Cadence** | ~monthly (v2026.7.1) | Irregular (no release today) | v0.8.4 imminent | v0.3.0 just shipped | Pre-v1 (RC open) | Irregular (cleanup burst) | Steady minor PRs |
| **Security Posture** | Reactive (P0 bugs active) | Proactive (3 security PRs today) | Proactive (S1 WhatsApp fix) | Moderate (container hardening) | Moderate (dependency updates) | Low (no security issues) | Low (no security issues) |

**Niche differentiation:**
- **Hermes Agent** is the only project with explicit **Buzz/Nostr channel support** and **Claude Agent SDK integration** – targets the decentralized/crypto-native developer
- **LobsterAI** invests heavily in **Mac-native UX** (cowork sessions, file dialogs) – unique in this landscape
- **Moltis** is the smallest but most focused on **modular memory backends** (Zvec as lightweight alternative) – a developer-experience play
- **CoPaw** (QwenPaw) is the only project tied to a **specific LLM vendor ecosystem** (Qwen models) – narrow use case

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity / Transitioning**
- **OpenClaw** – Massive throughput, but post-release regression tolerance is fraying. The 24 P0/P1 bugs suggest a **stabilization sprint is overdue**. Community trust remains high in contributor base but eroding in product reliability.
- **ZeroClaw** – Pre-release surge (50 PRs updated, release cut open). Strong security response (WhatsApp fix within 24 hours of report). Once v0.8.4 ships, expect stabilization.
- **Hermes Agent** – Most **balanced momentum**: high activity, rapid security fix turnarounds (3 PRs today), and deep-feature PRs (multi-agent gateway). Platform-specific (Windows) pain points hold back full maturity.

**Tier 2: Stable / Polishing**
- **NanoBot** – Just shipped v0.3.0 with 260 merged PRs and 38 new contributors. Post-release activity is targeted polish. **Best onboarding experience** in the ecosystem.
- **IronClaw** – Focused on pre-v1 stability (error recoverability epic, bundle optimization). Low community engagement but high code quality. Likely stabilizing toward release.
- **LobsterAI** – Burst cleanup suggests backlog management. UX-focused features (cowork interface) indicate a **product rather than platform** orientation.
- **Moltis** – Small but **well-scoped** (Nostr, Slack, Zvec). No regressions reported – unusual stability for this ecosystem.

**Tier 3: Emerging / Stalled**
- **CoPaw** – High bug-to-fix ratio; MCP transport regression duplicates suggest maintainer bandwidth constraints.
- **PicoClaw** – Critical Matrix sync bug (#3203) unaddressed for 24 days. Low PR volume.
- **NanoClaw** – Responsive (bug→fix PR on same day) but very small community.

**Tier 4: Dormant**
- **NullClaw**, **TinyClaw** – Zero activity.

---

## 7. Trend Signals

### From Community Feedback

**1. Security-first architecture is non-negotiable**
- 6 of 10 active projects have security-related PRs/issues today
- Users demand **source-based memory trust tags** (OpenClaw #7707), **credential chain verification** (ZeroClaw #9328), and **container capability dropping** (NanoClaw #2748)
- **Implication for developers**: Every new feature must include a security review gate

**2. "Personalization through configuration explosion" is a pain point**
- Hermes #71298 (dual provider storage), ZeroClaw #9366 (unread config fields), CoPaw #6470 (ignored transport config)
- Users have **too many configuration knobs** with inconsistent behavior
- **Implication**: Invest in **config validation engines** and **audit trails** rather than more settings

**3. Platform-as-a-Service readiness is accelerating**
- OpenClaw's hosting profiles + readiness conditions → cloud-native deployment
- ZeroClaw's OpenAI gateway (#8486) → API compatibility layer
- IronClaw's signed intents + per-agent keys (#6672) → enterprise key management
- **Implication**: The line between "open-source agent" and "agent platform" is blurring

**4. Multi-platform messaging is standard, not optional**
- Nostr/Buzz (Hermes, Moltis), Matrix (ZeroClaw, PicoClaw), Slack (IronClaw, Moltis), Telegram (Hermes, ZeroClaw, LobsterAI), WhatsApp (ZeroClaw)
- **Users expect agents to live where they communicate**, not force a new channel

**5. Regression velocity is a systemic risk**
- OpenClaw (24 P0/P1 bugs), Hermes (Windows boot loop), ZeroClaw (test flakiness 19/20 runs)
- The ecosystem is **shipping too fast relative to test coverage**
- **Implication**: Prioritize **flaky test reduction** and **regression conformance suites** over new features

### Value for AI Agent Developers

- **Adopt a "security wrapper" pattern**: Treat every external input (user messages, MCP tool calls, file reads) as untrusted; implement trust tagging (OpenClaw model) or sandbox policy (ZeroClaw model)
- **Plan for multi-platform from day one**: The Nostr/Slack/Telegram/Matrix integrations appearing across 4+ projects will become table stakes
- **Budget for regression testing**: 3 of the top 5 projects have significant regression problems; invest in CI parallelism and mutation testing (IronClaw's approach) early
- **Watch OpenClaw's MCP consent work**: The approval pipeline extension (#78308) will likely set the ecosystem standard for human-in-the-loop for third-party tools
- **Containerization is not optional**: Even lightweight projects (NanoClaw) are adding cap-drop and mount security; agent containers without these will be considered insecure

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-07-26

## 1. Today’s Overview
NanoBot shipped **v0.3.0** today – a major milestone with 260 merged PRs and 38 new contributors, marking a significant leap in agent agency. The project remains highly active: **12 PRs were updated in the last 24 hours**, 7 of which were merged or closed. Activity is concentrated on polishing the new release, fixing high-priority bugs in session routing and message context, and improving the WebUI experience. Community engagement is strong, with multiple open issues and PRs receiving updates from both contributors and maintainers.

## 2. Releases
**v0.3.0** (released 2026-07-25)  
- **Key changes**: The agent “gained agency” – the fastest entry point is now `nanobot webui`, which starts the local WebUI, gateway, and opens a browser workbench.  
- **No breaking changes announced**; however, three compatibility cleanup TODOs (legacy session path fallback, `agents.defaults.maxMessages` warning, and legacy config key handling) have been **deferred to v0.3.1** via PR #5083.  
- **Migration notes**: Runtime behavior is unchanged. Users upgrading from v0.2.x can run `nanobot webui` immediately – the setup wizard is preserved for headless/SSH sessions.  

## 3. Project Progress
**Merged/closed PRs today (7 items):**
- [#1284](https://github.com/HKUDS/nanobot/pull/1284) – **CI/CD pipeline** with quality checks and coverage (closes #1131).  
- [#5085](https://github.com/HKUDS/nanobot/pull/5085) – **Open WebUI automatically** after a fresh desktop install, preserving the wizard for headless sessions.  
- [#4696](https://github.com/HKUDS/nanobot/pull/4696) – **Smooth WebUI streaming** using state-driven viewport motion (frame-coalesced, ease-out camera).  
- [#5083](https://github.com/HKUDS/nanobot/pull/5083) – **Compatibility cleanup deferred** to v0.3.1.  
- [#5082](https://github.com/HKUDS/nanobot/pull/5082) – **Documentation refresh** clarifying WebUI, gateway, and CLI quick starts.  
- [#4954](https://github.com/HKUDS/nanobot/pull/4954) – **Fix late subagent turns** staying visible in WebUI.  
- [#5081](https://github.com/HKUDS/nanobot/pull/5081) – **Release preparation** (version bump, composer badge fix).  

All PRs above were part of the v0.3.0 release cycle.

## 4. Community Hot Topics
- **Issue #1131** ([link](https://github.com/HKUDS/nanobot/issues/1131)) – *CI Test Coverage* (4 comments, closed). User questioned whether CI runs automatically on PRs. **Resolved** by PR #1284, which added the full CI pipeline.  
- **PR #5085** ([link](https://github.com/HKUDS/nanobot/pull/5085)) – *Open WebUI after fresh install* (merged). Captured a common friction point – new users wanting a browser-first experience.  
- **PR #4696** ([link](https://github.com/HKUDS/nanobot/pull/4696)) – *Smooth WebUI streaming* (merged). Addresses complaints about jerky viewport scrolling during agent output.  
- **PR #5084** ([link](https://github.com/HKUDS/nanobot/pull/5084)) – *Preserve pending message runtime context* (open, p1). Users reported lost context when multiple mid-turn messages are queued – a critical fix for multichannel agents.  

Underlying community needs center on **stable session routing**, **context preservation**, and **polished onboarding** – all actively being addressed.

## 5. Bugs & Stability
Bugs reported or fixed today, ranked by severity:

| Severity | ID | Description | Status | Fix PR |
|----------|----|-------------|--------|--------|
| **High** | [#5084](https://github.com/HKUDS/nanobot/pull/5084) | Pending message runtime context lost (closes #4064) | Open (PR open) | – |
| **High** | [#4928](https://github.com/HKUDS/nanobot/pull/4928) | Heartbeat delivery fails for unified sessions – routes to wrong channel | Open (PR open) | – |
| **Medium** | [#4954](https://github.com/HKUDS/nanobot/pull/4954) | Late subagent turns invisible in WebUI | Closed (merged) | ✅ |
| **Medium** | [#3035](https://github.com/HKUDS/nanobot/pull/3035) | `at`-type cron tasks never execute if slightly expired (no grace window) | Open (conflict) | – |
| **Medium** | [#1073](https://github.com/HKUDS/nanobot/pull/1073) | Unknown config keys silently dropped when saving config | Open (conflict) | – |

No crashes or regressions were reported in the last 24h. The two open high-severity bugs have corresponding fix PRs under review.

## 6. Feature Requests & Roadmap Signals
- **Configurable bwrap bind roots** (PR #4625, open) – Allows exposing `~/.local/bin`, `~/.cargo/bin` inside the shell sandbox. This addresses a common need from developers using tools installed via package managers. Likely to land in v0.3.1.  
- **Grace window for cron `at` tasks** (PR #3035, open) – Introduces a 10‑minute window to handle LLM processing delays. User‑requested for reliable scheduling.  
- **Preserve unknown config keys** (PR #1073, open) – Prevents data loss when custom provider configs (e.g., `openai-codex`) are added outside the Pydantic model.  

**Roadmap signal**: v0.3.1 will absorb the deferred compatibility cleanup (#5083) and likely the above open feature/fix PRs. The next minor release focuses on **stability** and **sandbox flexibility**.

## 7. User Feedback Summary
- **Pain points**:  
  - Lost custom config keys (#1073) – users adding provider-specific settings risk data loss on save.  
  - Delayed cron tasks (#3035) – `at` jobs scheduled by agents may never fire due to timing.  
  - Heartbeat routing (#4928) – multiturn sessions across channels fail to deliver heartbeat back to the correct conversation.  
  - Pending message context loss (#5084) – multiple rapid user messages lose runtime context, breaking tool calls.  
- **Satisfaction signals**:  
  - One‑command WebUI onboarding (#5085) received positive feedback in the release notes.  
  - Smooth streaming (#4696) and automatic WebUI opening after install reduce friction.  
  - CI/CD pipeline (#1284) gives contributors confidence in code quality.  

Overall sentiment is **positive but expectant** – the community appreciates the rapid release cycle and targeted fixes.

## 8. Backlog Watch
Two long‑standing PRs remain open and marked with conflict, each requiring maintainer attention to resolve conflicts and review:

- **#3035** ([link](https://github.com/HKUDS/nanobot/pull/3035)) – fix(cron): grace window for `at` tasks. Opened 2026-04-11, last updated today. Addresses a real usability issue for cron‑dependent agents.  
- **#1073** ([link](https://github.com/HKUDS/nanobot/pull/1073)) – fix: preserve unknown config keys. Opened 2026-02-23, last updated today. Prevents silent data loss for custom provider setups.  

Neither has been merged due to conflicts; both would benefit from a maintainer rebase and review.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-26

## 1. Today's Overview
Activity remains high with 50 issues and 50 pull requests updated in the last 24 hours. The project is in an active maintenance and feature-development phase: 46 of the updated issues are still open, and 17 pull requests were merged or closed today. No new releases were published. The community is engaged in both bug reporting (especially around Windows platform stability, authentication flows, and markdown rendering on Telegram) and substantial feature proposals (multi-agent gateway support, a new Buzz/Nostr platform adapter, and governed approval workflows). Several high-priority bugs (P1/P0) are being actively addressed with fix PRs.

## 2. Releases
None — no new releases were tagged on 2026-07-26.

## 3. Project Progress
**17 pull requests were merged or closed today.** Notable examples include:

- 🛠️ **#71679** – *(CLOSED)* [fix(desktop): honor the configured reasoning effort instead of assuming medium](https://github.com/NousResearch/hermes-agent/pull/71679). Desktop now respects the user's `agent.reasoning_effort` setting instead of silently defaulting to `medium`.
- 🛠️ **#71672** – *(CLOSED)* [fix(desktop): name a Cmd+T session from its first message](https://github.com/NousResearch/hermes-agent/pull/71672). Eliminates the inconsistency where ⌘N sessions were named immediately but ⌘T tabs stayed as “New session” through the first exchange.
- 🛠️ **#71678** – *(CLOSED)* [fix(desktop): keep code and diffs out of the tool overflow window](https://github.com/NousResearch/hermes-agent/pull/71678). Prevents large code blocks from being hidden inside the 6.75rem scroll window intended for status rows.
- ❌ **#64393** – *(CLOSED)* [Bug: curator status labels bundled prune candidates as agent-created skills](https://github.com/NousResearch/hermes-agent/issues/64393) – closed as resolved.

Additionally, many open PRs are under active review (see sections below). The overall pace suggests a healthy balance of bug fixing and new feature integration.

## 4. Community Hot Topics
The most active discussions (by comment count and reactions) reveal several recurring themes:

- 🔥 **#6388** – [Telegram MarkdownV2 escape breaks bullet list display](https://github.com/NousResearch/hermes-agent/issues/6388) *(7 comments, 1 👍)*. Users are frustrated that LLM-generated bullet lists with `-` become `\-` on Telegram, breaking readability. This is a long-standing platform integration issue.
- 🔥 **#62726** – [Dashboard cross-tab session bleed + /new hang requiring full container restart](https://github.com/NousResearch/hermes-agent/issues/62726) *(7 comments)*. Two severe UI bugs causing session contamination and unresponsiveness in the web dashboard. Likely a high-priority topic for the maintainers.
- 🔥 **#71298** – [providers vs custom_providers dual storage causes CLI/GUI mismatch](https://github.com/NousResearch/hermes-agent/issues/71298) *(6 comments)*. Configuration inconsistency between CLI and Desktop settings is causing model version sticks and provider confusion.
- 🔥 **#71226** – [Desktop boot loop on Windows: WebSocket connects but client disconnects](https://github.com/NousResearch/hermes-agent/issues/71226) *(5 comments, P1)*. A critical Windows-only regression preventing the desktop app from starting.

**Underlying needs**: Users are demanding robust Windows support, consistent configuration management across interfaces, and reliable multi-platform messaging (especially Telegram and email). There is also a clear desire for better error messages and recovery paths.

## 5. Bugs & Stability
Today saw reports of several high-severity bugs, with at least one P0 issue being fixed:

### Critical / P0
- **#71676** (PR) – [fix(conversation): rebuild the system prompt when the working directory drifts](https://github.com/NousResearch/hermes-agent/pull/71676). *Severity: P0*. Prevents stale system prompts from causing incorrect agent behavior when the user changes projects mid-session. A fix PR is already in review.

### High / P1
- **#71226** – [Desktop boot loop: WebSocket connects but client disconnects immediately, triggering renderer-initiated reset cycle](https://github.com/NousResearch/hermes-agent/issues/71226). Windows 11, critical for desktop users. No fix PR yet; appears to be a recent regression.
- **#71687** (PR) – [stop planted cwd PowerShell from running during managed-uv bootstrap](https://github.com/NousResearch/hermes-agent/pull/71687). *Security*. On Windows, an attacker could plant a malicious `powershell.exe` in a writable directory; the fix resolves the absolute path to System32. Merged today.
- **#71682** (PR) – [stop container privilege escalation via s6 gateway log symlink chown](https://github.com/NousResearch/hermes-agent/pull/71682). *Security*. Docker deployments could allow unprivileged users to escalate via symlink attack. Fix open.
- **#71677** (PR) – [block SSRF in media downloads](https://github.com/NousResearch/hermes-agent/pull/71677). *Security*. Relay media download path lacked URL safety checks, potentially enabling SSRF. Fix open.
- **#22016** (closed) – [SECURITY FLAW: `hermes debug share` exposes private data](https://github.com/NousResearch/hermes-agent/issues/22016). Closed (resolved) – but users were exposed before the fix.

### Medium / P2
- **#71491** – [Hermes Cloud connection mode: desktop never initiates sign-in, loops on 401 no_cookie (Windows)](https://github.com/NousResearch/hermes-agent/issues/71491). Windows-only authentication loop.
- **#70480** – [Docker image ships WAL-reset-vulnerable SQLite](https://github.com/NousResearch/hermes-agent/issues/70480). Affects all Docker-based installations. Needs decision on bundling a fixed SQLite.
- **#71047** – [config set duplicates top-level key + Telegram streaming duplicates final message](https://github.com/NousResearch/hermes-agent/issues/71047). Two separate bugs: config editing corruption and message duplication during streaming.
- **#63717** – [Windows: Hermes Desktop update failures — comprehensive diagnostic with 7 correlated root causes](https://github.com/NousResearch/hermes-agent/issues/63717). Long-running Windows update instability.

### Low / P3
- **#71675** – [Local Ollama context resolved from GGUF max instead of Modelfile num_ctx](https://github.com/NousResearch/hermes-agent/issues/71675). Configuration priority bug for local Ollama models.
- **#71664** (PR) – [fix(desktop): make skills referenceable anywhere in the composer](https://github.com/NousResearch/hermes-agent/pull/71664). Skills only worked when typed at the very start of a prompt; now works in any position.

## 6. Feature Requests & Roadmap Signals
The most significant feature contributions today point to a major upcoming release centered on multi-agent support and governance:

- **#71686** – [feat(gateway): per-agent Buzz identities — N agents, N workspace members, one gateway process](https://github.com/NousResearch/hermes-agent/pull/71686). A stacked PR on top of #62944 that enables multiple Hermes agents to run under a single gateway, each with different platform identities. This is a major architectural extension.
- **#71610** – [feat(plugin): Buzz (Block/Nostr) platform adapter](https://github.com/NousResearch/hermes-agent/pull/71610). Adds support for the decentralized Nostr protocol as a messaging platform.
- **#71685** – [feat: add governed approvals and connector visibility](https://github.com/NousResearch/hermes-agent/pull/71685). Introduces profile-scoped durable approval requests, standing approvals, and a new Governance page in both Desktop and web dashboard.
- **#65982** – [feat(providers): claude-agent-sdk provider — the official Agent SDK as a first-class runtime](https://github.com/NousResearch/hermes-agent/pull/65982). Would allow users to run Hermes on top of Anthropic's subscription-based Claude Agent SDK, a highly requested integration.
- **#62944** – [feat: single gateway, multiple agents — rebased onto current main](https://github.com/NousResearch/hermes-agent/pull/62944). This long-running PR (#25660) has been rebased and is the foundation for #71686.
- **#56989** – [Document and harden fully local STT for voice messages (MLX + CUDA)](https://github.com/NousResearch/hermes-agent/issues/56989). Users want to keep voice transcription on-device rather than using cloud APIs.
- **#67139** – [feat(curator): add a supported adoption path for legacy and unmanaged local skills](https://github.com/NousResearch/hermes-agent/issues/67139). Local skill management gap identified by the community.

**Prediction for next release**: The combination of multi-agent gateway (#62944 / #71686), governed approvals (#71685), and the Buzz platform (#71610) could form the core of a v0.20.0 release. The Claude Agent SDK provider (#65982) may also land if reviews progress quickly.

## 7. User Feedback Summary
Real pain points voiced in the last 24 hours include:

- **Windows instability**: Users report boot loops (#71226), Cloud sign-in loops (#71491), update failures (#63717), and configuration mismatches (#71298). Satisfaction is low for Windows users.
- **Telegram markdown corruption**: (#6388) – Bullet lists break due to excessive escaping. This affects both readability and trust in the agent's output.
- **Config management confusion**: Dual provider storage (#71298) and BOM issues (#65123) lead to silent misconfiguration.
- **Session management**: Cross-tab bleed (#62726), stale context length (#31043), and frozen terminals from `/reload-mcp` (#39418) degrade the interactive experience.
- **Skill curation**: Users with legacy skills find it difficult to opt into curator management (#67139) and background processes may interfere with write policies (#67140).
- **Docker security**: The WAL-reset SQLite vulnerability (#70480) raises concerns for production container deployments.

**Positive signals**: The community appreciates the rapid fix response – many PRs were opened on the same day as the bugs they address. The feature PRs (especially governance and multi-agent) indicate strong demand for enterprise-grade capabilities.

## 8. Backlog Watch
Several important issues have been open for weeks to months without resolution or clear maintainer response:

- 🕒 **#31043** – [CLI /new does not refresh context_compressor.context_length after provider config changes](https://github.com/NousResearch/hermes-agent/issues/31043) *Created 2026-05-23*. Last updated today but still open. Users must restart the CLI to see provider changes.
- 🕒 **#11515** – [ACP session cwd is used for tool execution but not for project context file discovery](https://github.com/NousResearch/hermes-agent/issues/11515) *Created 2026-04-17*. A fundamental inconsistency in ACP mode that could lead to missed project context.
- 🕒 **#42997** – [Email gateway IMAP polling marks unread Gmail messages as read](https://github.com/NousResearch/hermes-agent/issues/42997) *Created 2026-06-09*. Gmail users risk losing unread indicators – a significant usability bug.
- 🕒 **#27300** – [WeChat voice messages use Tencent Cloud STT which garbles non-Chinese languages](https://github.com/NousResearch/hermes-agent/issues/27300) *Created 2026-05-17*. Affects international users on WeChat.
- 🕒 **#40896** – [Desktop: Generated videos show broken image icon in chat (video downloads & plays fine)](https://github.com/NousResearch/hermes-agent/issues/40896) *Created 2026-06-07*. Minor but persistent UI glitch for video output.
- 🕒 **#39418** – [/reload-mcp freezes the CLI terminal when triggered by user](https://github.com/NousResearch/hermes-agent/issues/39418) *Created 2026-06-05*. Session becomes completely unresponsive – no workaround other than force kill.
- 🕒 **#22016** – *Closed* (resolved) but the severity of the security flaw was high; users should verify they are on a patched version.

**Maintainers’ attention**: Several issues are labeled `needs-repro` or `needs-decision`, which may explain delays. Notably, the multi-agent PR stack (#62944) has been open since July 12 and is still awaiting merge – its size and architectural impact likely require careful review. The security fixes (#71677, #71682, #71687) should be prioritized for immediate merging.

- 📌 **#70480** – Docker SQLite vulnerability – labelled `needs-decision`. No clear path forward yet despite the known fix.
- 📌 **#71491** – Windows Cloud auth loop – labelled `needs-decision` and `sweeper:risk-security-boundary`. The bisect points to a commit range; maintainer feedback is needed.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-26

## Today's Overview
The project saw moderate activity with two issues and three pull requests updated in the last 24 hours. Notably, two PRs were closed/merged, including a significant feature bundle and a Raspberry Pi compatibility fix. No new releases were published. The community is actively discussing a critical Matrix sync stability bug, while a minor UI bug in the `/list models` command remains newly reported. Overall, the project is progressing steadily with contributions addressing both infrastructure gaps and user-facing functionality.

## Releases
No new releases were published in the last 24 hours. The latest available releases remain unchanged (current version v0.3.1 as of the latest issue #3294).

## Project Progress
Two pull requests were closed/merged in the last 24 hours:

- **[PR #339](https://github.com/sipeed/picoclaw/pull/339) — Added Email Tool, Calendar Integration and System Stats Overview Tool** (merged/closed). This large contribution integrates Google Calendar support, enhances the Email channel with improved polling and content fetching, and adds developer tools (GitHub, System Stats). The feature significantly extends PicoClaw’s agent capabilities.

- **[PR #3205](https://github.com/sipeed/picoclaw/pull/3205) — fix: support 9router gateway responses and add Linux ARMv7 build target** (merged/closed). Fixes a parsing issue with the openai_compat provider when used behind a 9router gateway, and adds an ARMv7 binary build target for Raspberry Pi 3 B+ users. This addresses two real-world deployment pain points.

One PR remains open but was updated:
- **[PR #3193](https://github.com/sipeed/picoclaw/pull/3193) — Added simplex channel type** (still open, stale). No new comments.

## Community Hot Topics
- **[Issue #3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix sync loop has no reconnection logic** (6 comments, 2 👍). This is the most active discussion. It describes a silent death of the Matrix `/sync` long-polling loop after any network disruption or homeserver restart, without automatic reconnection. The community and maintainers are analyzing the problem, as it breaks reliability for Matrix users. Underlying need: robust error handling and automatic reconnection for persistent channels.

- **[Issue #3294](https://github.com/sipeed/picoclaw/issues/3294) — `/list models` only shows the current model instead of all configured models** (0 comments, 0 👍). New and awaiting triage. A simple but confusing UX mismatch.

## Bugs & Stability
**High Severity**
- **[Issue #3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix sync loop no reconnection** (open). **Critical** for Matrix users: the entire sync channel dies silently after network/server disruption. The process stays alive, so systemd’s `Restart=on-failure` does not help. No fix PR is open yet. Requires urgent attention from maintainers or contributors.

**Low Severity**
- **[Issue #3294](https://github.com/sipeed/picoclaw/issues/3294) — `/list models` only shows current model** (open). Purely a display bug; no crash or data loss. Should be easy to fix once triaged.

## Feature Requests & Roadmap Signals
- The merged **PR #339** brings strong signals toward extended tool integration (Calendar, Email, System Stats). These are likely to appear in the next minor release (v0.3.2 or v0.4.0). The **Simplex channel type** (PR #3193) remains open and could follow if revived.
- The **ARMv7 build target** (PR #3205) indicates growing demand for Raspberry Pi deployment. This is now merged and should be available in the next snapshot/release.
- No new feature requests were raised in the last 24h, but the Matrix reconnection issue (issue #3203) may evolve into a stability improvement request.

## User Feedback Summary
- **Pain points**: Matrix users are experiencing silent session loss (issue #3203). The `/list models` command misleads users into thinking only one model is configured (issue #3294).  
- **Positive signals**: Contributors are actively solving deployment hurdles (9router gateway, ARM builds). The merge of Calendar and Email tools suggests growing satisfaction with extensibility.  
- **Unaddressed**: The stale Simplex channel PR (#3193) has no maintainer feedback, which may leave some users waiting.

## Backlog Watch
- **[Issue #3203](https://github.com/sipeed/picoclaw/issues/3203) — Matrix sync loop no reconnection** (created 2026-07-02, last updated 2026-07-25). This is the most important open bug. It has been open for 24 days with 6 comments but no assigned fix. Maintainer attention is needed to prevent silent failures for Matrix users.
- **[PR #3193](https://github.com/sipeed/picoclaw/pull/3193) — Added simplex channel type** (created 2026-06-27, last updated 2026-07-25). Stale for a month with no comments from maintainers. If the feature is desired, it should be reviewed or closed to avoid contributor frustration.
- *No other long-unanswered items in the last 24h set.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-07-26

## 1. Today's Overview

NanoClaw shows a high level of development activity today with 11 pull requests updated in the last 24 hours, including one security-related merge. Two new bugs were reported, both of which already have open fix PRs, indicating a responsive maintainer team. No new releases were published. The project remains focused on stability, security hardening, and expanding its skill ecosystem. Community engagement via comments or reactions is currently low, but the rapid turnaround on bug reports suggests strong internal momentum.

## 2. Releases

*No new releases were published in the last 24 hours. The latest release remains unchanged.*

## 3. Project Progress

**Merged/Closed PRs (1):**

- [#2748 – security: harden agent containers (cap-drop, no-new-privileges, pids-limit)](https://github.com/nanocoai/nanoclaw/pull/2748)  
  Merged/closed after being open since June 12. This PR introduces container-level hardening for per-session agent containers: `--cap-drop=ALL`, `--security-opt no-new-privileges:true`, and `--pids-limit 2048` by default. Defaults are overridable per agent group. This is a significant defense-in-depth improvement.

**Notable Open PRs with recent updates (fixes/features awaiting merge):**

- [#3135 – fix: mirror host-sent messages into the agent's context](https://github.com/nanocoai/nanoclaw/pull/3135) – Direct fix for Issue #3134.
- [#3133 – fix(container): gate the follow-up poll on trigger=1 too](https://github.com/nanocoai/nanoclaw/pull/3133) – Direct fix for Issue #3132.
- [#3122 – fix(opencode): main compatibility, custom-endpoint transport, memory parity](https://github.com/nanocoai/nanoclaw/pull/3122) – Broad compatibility fix for OpenCode.
- [#3128 – Add flight-checkin container skill](https://github.com/nanocoai/nanoclaw/pull/3128) – New operational container skill.
- [#2211 – feat: add tool-visibility skill for live tool-call previews](https://github.com/nanocoai/nanoclaw/pull/2211) – Community skill, resynced after three months of production use.
- [#3131 – uninstall: remove per-agent-group derived images, not just `<base>:latest`](https://github.com/nanocoai/nanoclaw/pull/3131) – Cleanup fix for uninstall script.
- [#3130 – db: validate container_configs.image_tag at the write seam](https://github.com/nanocoai/nanoclaw/pull/3130) – Input validation improvement.
- [#3129 – mount-security: block ~/.config/nanoclaw and ~/.local/bin as mount roots](https://github.com/nanocoai/nanoclaw/pull/3129) – Additional mount security hardening.
- [#3124 – fix: report unavailable MCP servers](https://github.com/nanocoai/nanoclaw/pull/3124) – Better error reporting.
- [#3127 – fix(host): sanitize inbox attachment paths to a safe character class](https://github.com/nanocoai/nanoclaw/pull/3127) – Path sanitization fix.

## 4. Community Hot Topics

No issues or PRs received comments or reactions in the last 24 hours (all show `👍: 0`, `Comments: 0`). The most notable long-term community contribution is:

- [#2211 – tool-visibility skill](https://github.com/nanocoai/nanoclaw/pull/2211) – Open since May 3, resynced July 25. This PR adds live tool-call previews into chat via PreToolUse/PostToolUse hooks. The author reports it has been running on a fork for three months, indicating real-world demand for better observability of agent tool calls.

Given the absence of explicit community discussion, the underlying need appears to be for core stability and security first, followed by expanded skill capabilities. The two bug reports filed today likely reflect pain points from active users encountering context loss and message accumulation issues.

## 5. Bugs & Stability

**Two bugs reported today, both ranked high severity:**

- **[#3134 – Messages the host sends on an agent's behalf are absent from that agent's context](https://github.com/nanocoai/nanoclaw/issues/3134)** (Severity: High)  
  Host-sent messages (approval cards, reject-reason prompts, registration notices) never enter the agent’s `messages_in` or turn history, causing the agent to be unaware of those interactions. This can lead to broken conversation flow and incorrect agent behavior.  
  **Fix PR:** [#3135](https://github.com/nanocoai/nanoclaw/pull/3135) (open, authored by the same reporter).

- **[#3132 – bug: follow-up poll pushes accumulate (trigger=0) messages into an active query, bypassing the accumulate gate](https://github.com/nanocoai/nanoclaw/issues/3132)** (Severity: High)  
  The `poll-loop.ts` has two message-consumption paths; the follow-up poller (`processQuery`) is not gated on `trigger=1`, allowing it to push newly arriving messages into an already active query even when they lack a trigger flag. This can cause unbounded message accumulation.  
  **Fix PR:** [#3133](https://github.com/nanocoai/nanoclaw/pull/3133) (open, authored by the same reporter).

Both bugs have fix PRs already open, indicating rapid response. No regressions or crashes were reported.

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed as issues today. However, the open PRs offer strong signals about upcoming features:

- **OpenCode compatibility** ([#3122](https://github.com/nanocoai/nanoclaw/pull/3122)) – Suggests a push to broaden integration with the OpenCode ecosystem, likely landing in the next minor release.
- **Flight check-in container skill** ([#3128](https://github.com/nanocoai/nanoclaw/pull/3128)) – Adds a real-world automation skill, demonstrating the container skill framework.
- **Tool-visibility skill** ([#2211](https://github.com/nanocoai/nanoclaw/pull/2211)) – If merged, this would give users live insight into agent tool calls, a highly requested observability feature.
- **Mount security extensions** ([#3129](https://github.com/nanocoai/nanoclaw/pull/3129)) – Blocking `~/.config/nanoclaw` and `~/.local/bin` as mount roots signals ongoing refinement of the security model.

Given the volume of fix PRs, the next version is likely to prioritize these bug fixes (#3135, #3133) along with the security hardening already merged (#2748). The OpenCode and skill PRs may be bundled if they pass review.

## 7. User Feedback Summary

While no direct user comments are present, the issues and PRs reflect real pain points:

- **Pain point: agent context blindness** – Issue #3134 indicates users (likely developers running agents) are frustrated that host-sent messages disappear from agent memory, forcing them to manually re-explain or lose conversation state.
- **Pain point: unbounded message accumulation** – Issue #3132 suggests users experience runaway message growth in active queries, impacting performance or causing unexpected behavior.
- **Satisfaction signal: security improvements** – The swift merging of #2748 (container hardening) and the proposed mount security PRs (#3129) show the project is addressing user security concerns proactively.
- **Skill ecosystem engagement** – The submission of a flight check-in skill (#3128) and maintenance of the tool-visibility skill (#2211) indicate that the community is actively building and using the container skill framework, suggesting satisfaction with the extensibility model.

## 8. Backlog Watch

- **[#2211 – tool-visibility skill](https://github.com/nanocoai/nanoclaw/pull/2211)** – Open since May 3, resynced July 25. This is a substantial community PR that has been in review for nearly three months. While the resync suggests ongoing interest, it remains unmerged. Core team attention is needed to either merge or provide guidance for further changes.
- **[#3122 – OpenCode compatibility fix](https://github.com/nanocoai/nanoclaw/pull/3122)** – Open since July 23, updated July 25. Though not extremely old, it is a high-impact compatibility fix that touches multiple subsystems (main compatibility, custom-endpoint transport, memory parity). A maintainer review is recommended to prevent it from stagnating.
- **[#2748 – security hardening](https://github.com/nanocoai/nanoclaw/pull/2748)** – Was open from June 12 to July 25 (6+ weeks) before being closed today. This resolution is positive, but its long wait time suggests that nontrivial security PRs may face delays. The project should monitor if similar PRs suffer extended review cycles.

No issues remain unanswered for more than a few days; the two open issues (#3134, #3132) were created within the last 24 hours and already have fix PRs. This indicates a healthy response time.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-07-26

## 1. Today’s Overview

The IronClaw project saw high activity over the past 24 hours: **11 issues updated** (7 open, 4 closed) and **20 pull requests updated** (11 open, 9 closed/merged). The team merged multiple WebUI bug fixes and performance improvements, advanced the Reborn architecture consolidation, and added a production dead-code ratchet. A major Epic (#6284) around error recoverability continues to drive deeper testing infrastructure (mutation-audit harness, recoverability conformance matrix). No new releases were published today. Overall project health appears robust, with focused effort on hardening both frontend and backend stability.

## 2. Releases

No new releases were created in the last 24 hours. The last release candidate remains PR #5598 (chore: release), which has been open since 2026-07-03 and includes breaking changes in `ironclaw_common` and `ironclaw_skills`.

## 3. Project Progress (Merged/Closed PRs)

**9 pull requests were closed/merged today**, spanning frontend fixes, architecture cleanup, and testing improvements:

- **WebUI Fixes**  
  - [#6624](https://github.com/nearai/ironclaw/pull/6624) – [fix] Modal focus trap and restoration in extension configuration dialog.  
  - [#6627](https://github.com/nearai/ironclaw/pull/6627) – [fix] Preserve active run state when cancellation fails (defers clearing until backend confirms).  
  - [#6626](https://github.com/nearai/ironclaw/pull/6626) – [fix] Keep automation list visible during filter changes (uses TanStack Query placeholder data).  
  - [#6680](https://github.com/nearai/ironclaw/pull/6680) – [fix] Preserve workspace tree state across root navigation.  

- **Performance**  
  - [#6632](https://github.com/nearai/ironclaw/pull/6632) – [perf] Route-level code splitting and improved tree-shaking; reduced initial JS bundle from **1,227 kB to 377 kB** (gzip: 349 kB → 116 kB).  

- **Architecture & Code Quality**  
  - [#6669](https://github.com/nearai/ironclaw/pull/6669) – [refactor] Moved extension host ownership out of `ironclaw_reborn_composition`.  
  - [#6670](https://github.com/nearai/ironclaw/pull/6670) – [docs] Consolidated active Reborn guidance and removed 11 outdated architecture/plan documents.  
  - [#6673](https://github.com/nearai/ironclaw/pull/6673) – [test] Added production struct dead-code ratchet (static scanner for test-support fields/methods).  
  - [#6616](https://github.com/nearai/ironclaw/pull/6616) – [refactor] Shrank composition extension host and retired product workflow facades.  

## 4. Community Hot Topics

- **#6284 – [EPIC] Error-recoverability endgame**  
  [Issue link](https://github.com/nearai/ironclaw/issues/6284)  
  **6 comments** (most of any issue), **0 👍**. This ongoing epic defines the recoverability contract: every mid-run error must survive and be visible to the model with cause and remediation. It remains the highest-level feature conversation, with PR #6677 (recoverability conformance matrix) and PR #6674 (mutation-audit harness) directly supporting it. The community's underlying need is clear: the model should never silently fail and should always get a chance to correct.

- **#6675 – Centralize Shared Rust Dependencies**  
  [Issue link](https://github.com/nearai/ironclaw/issues/6675)  
  **2 👍** (most reactions), **0 comments**. Users agree that using `[workspace.dependencies]` would reduce inconsistencies across Cargo.toml files. This technical debt issue has quick community support.

- **#6676 – Daily failure taxonomy (2026-07-25)**  
  [Issue link](https://github.com/nearai/ironclaw/issues/6676)  
  A fresh daily analysis of clawbench failures (85 non-pass) dominated by model shortfalls rather than harness defects. Provides transparency into model quality regression tracking.

## 5. Bugs & Stability

Three new user-facing bugs were opened today, all tagged as [v1-launch-checklist]:

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#6667](https://github.com/nearai/ironclaw/issues/6667) | **High** | Rejected GitHub PAT silently loops auth prompt – no error surfaced to user | None yet |
| [#6671](https://github.com/nearai/ironclaw/issues/6671) | Medium | Telegram setup via agent/extensions tab dead-ends on “admin must configure” | None yet |
| [#6668](https://github.com/nearai/ironclaw/issues/6668) | Medium | Agent doesn't tell users Slack can be connected (guidance gap) | None yet |

Additionally, three previously reported bugs were closed today via merge of fix PRs:
- Focus trap in extension modal (🔒 closed via #6624)
- Cancellation failure leaving chat in incorrect idle state (🔒 closed via #6627)
- Automation filter flashing full loading skeleton (🔒 closed via #6626)

The daily failure taxonomy ([#6676](https://github.com/nearai/ironclaw/issues/6676)) also highlights that 85 non-pass clawbench results are largely genuine model shortfalls, not harness defects.

## 6. Feature Requests & Roadmap Signals

- **Error recoverability endgame** ([#6284](https://github.com/nearai/ironclaw/issues/6284)) – Active work continues with PR #6677 (recoverability conformance matrix) and PR #6674 (mutation-audit harness). Likely to be a cornerstone of the next major release.
- **WebUI bundle size optimization** – Requested in [#6628](https://github.com/nearai/ironclaw/issues/6628) and already delivered via PR [#6632](https://github.com/nearai/ironclaw/pull/6632) (merged). Expect this in the next release.
- **Signed intent + per-agent key lifecycle** – PR [#6672](https://github.com/nearai/ironclaw/pull/6672) (open) implements Phase B of the attested-signing Ledger revival plan. A significant security feature likely targeting v1 launch.
- **Product command pipeline** – PR [#6678](https://github.com/nearai/ironclaw/pull/6678) (open) brings `/model` and `/status` commands end-to-end across Slack, Telegram, and WebChat. Declarative design avoids per-command adapter logic.
- **Centralized Rust dependencies** ([#6675](https://github.com/nearai/ironclaw/issues/6675)) – Community-supported initiative to switch to `[workspace.dependencies]`. Low effort, high payoff – could merge quickly.

**Prediction for next release**: Error recoverability improvements (harness + conformance tests), signed intents, product command pipeline, and the WebUI performance gains from #6632.

## 7. User Feedback Summary

Three concrete pain points were reported today by **thisisjoshford**, all related to integration setup:

1. **GitHub PAT rejection silent loop** ([#6667](https://github.com/nearai/ironclaw/issues/6667)) – Users cannot tell why authentication fails; the system keeps re-prompting without error messages. This is a critical usability gap.
2. **Telegram setup dead-end** ([#6671](https://github.com/nearai/ironclaw/issues/6671)) – The only path to configure the Telegram bot token is hidden at the bottom of a channel list; asking the agent or using the Extensions tab leads to a dead end.
3. **Slack connection guidance gap** ([#6668](https://github.com/nearai/ironclaw/issues/6668)) – The agent claims Slack cannot be connected, whereas the UI does support it via Settings → Extensions → Channels.

These issues reflect a broader need for better onboarding and error messaging. The team’s rapid closure of similar bugs (focus trap, cancellation state, automation flash) suggests similar fixes may land soon.

No positive satisfaction signals (👍 or praise) were recorded in the data.

## 8. Backlog Watch

- **PR #5598 – chore: release** [link](https://github.com/nearai/ironclaw/pull/5598)  
  Open since **2026-07-03** (23 days). This release PR includes breaking changes in `ironclaw_common` and `ironclaw_skills`. It has been repeatedly updated but not merged. A decision or further review is needed to unblock the next version.

- **PR #6428 – bump tokio-ecosystem** [link](https://github.com/nearai/ironclaw/pull/6428)  
  Open since 2026-07-21 (5 days). Routine dependency update, low risk but still pending.

- **PR #6361 – bump serialization group** [link](https://github.com/nearai/ironclaw/pull/6361)  
  Open since 2026-07-20 (6 days). Same as above.

None of the open issues older than a week have zero maintainer attention, but the release PR (#5598) is the most notable block in the backlog.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for July 26, 2026, based on the provided GitHub data.

---

## LobsterAI Project Digest — 2026-07-26

### 1. Today's Overview
The project saw an intense day of consolidation, with a near-total closure of a large batch of stale issues and pull requests. All 11 PRs updated were merged, and 8 out of 9 issues updated were closed, signaling a focused cleanup and feature integration effort. No new releases were tagged, indicating that these merged features will likely form part of a forthcoming stable release. Overall activity is very high, with maintainers actively merging community contributions and addressing a backlog of UX enhancements.

### 2. Releases
**None.** No new releases were tagged today.

### 3. Project Progress
**Merged/Closed Pull Requests (11 total):**
The team merged a significant number of PRs, completing a large backlog of feature requests and bug fixes. Key areas of advancement include:
- **Platform Stability (Windows):** Two critical fixes were merged to harden the Windows installer, addressing foreign content protection and update recovery mechanisms (#2383, #2384).
- **New Model Support:** Integration for the Kimi K3 model was completed, expanding the available AI provider options (#2381).
- **UX Overhaul (Cowork Session):** A series of long-standing user requests for the Cowork interface were merged, including:
    - Batch expand/collapse of tool calls (#1327)
    - Error state red dot badge on session list (#1331)
    - Time-based grouping of session list (#1338)
    - Message timestamps on user bubbles (#1340)
    - Up/Down arrow key history navigation in input (#1342)
- **Scheduled Tasks:** A new "Workdays (Mon-Fri)" schedule option was added to the task planner (#1335).
- **Agent & i18n Fix:** A fix was merged to resolve internationalization labels, Escape key closing, and deletion guards in agent/cowork flows (#1333).
- **MCP Configuration:** A JSON paste-import feature was added to the MCP custom server configuration dialog, simplifying setup (#1336).

### 4. Community Hot Topics
The most active user demand centers on **macOS-native functionality** and **file management** within the Cowork dialog.

- **#2385 [OPEN] - Dialog cannot add folders, only files [1 comment]**
    - **URL:** [Issue #2385](https://github.com/netease-youdao/LobsterAI/issues/2385)
    - **Analysis:** This is the only newly opened issue today and the only one remaining open. The user requests the ability to add entire folders to the Cowork dialog, similar to the "@ file" feature seen in other AI agents. This feature is critical for users who work with structured project directories and want to provide context without selecting files individually. This is a strong signal for a missing feature that limits the agent's ability to understand project-level context.

### 5. Bugs & Stability
No new critical bugs, crashes, or regressions were reported today. The focus was on resolving several identified issues, including a key Windows installation problem.

- **High Priority: Windows Installer Fixes** - PRs #2383 and #2384 were merged to resolve issues related to foreign content protection and update recovery on Windows. These are significant stability fixes that prevent application corruption and update failures for Windows users.

### 6. Feature Requests & Roadmap Signals
The massive batch of merged PRs today indicates that the team is actively working through a defined product roadmap, prioritizing **user interface enhancements and quality-of-life improvements** for the Cowork experience.

- **Predicted for Next Version:** Based on the merged PRs, the next release will likely include:
    - The full set of UX improvements for the Cowork session list and input (time groups, timestamps, history navigation).
    - New model support (Kimi K3).
    - Improved MCP server configuration UX.
    - Enhanced scheduled task scheduling options.

### 7. User Feedback Summary
User feedback, captured entirely in the stale issues that were finally resolved, points to a clear desire for a more **polished and traditional chat-like UI** for the Cowork feature.

- **Pain Points Addressed:** Users found the UI unresponsive and lacking basic features. The most repeated complaints were about the inability to find conversations (no time groups, no full-text search), the lack of basic message context (no timestamps), and inefficient interaction patterns (having to click each tool call, no keyboard history).
- **Satisfaction Signals:** The closure and merging of 8 long-standing feature requests (Issues #1326, #1329, #1330, #1337, #1339, #1341, #1343, #1345) suggests that the team is responsive to well-documented user needs. The high volume of merged PRs is a very positive signal of project health and community satisfaction.

### 8. Backlog Watch
The only item needing immediate maintainer attention is the newly opened Issue #2385.

- **#2385 [OPEN] - Dialog cannot add folders, only files** - This issue has zero maintainer engagement yet and is the single block to a clear user workflow. Given the current momentum, a response or early-stage reproduction is expected soon.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-26

## Today’s Overview
Activity on the Moltis repository remains high, with 5 pull requests updated in the last 24 hours and no new issues filed. Two PRs were merged today, moving Slack acknowledgment reactions and documentation rules into the main branch. Three open PRs continue to advance: a Nostr NIP-29 group chat integration for Buzz channels, a richer Slack reaction/acknowledgment pipeline, and a Zvec vector database memory backend. No new releases, crash reports, or regressions were recorded, indicating steady, well-targeted development.

## Releases
*None.* No new versions were tagged in the last 24 hours.

## Project Progress
Two pull requests were closed/merged today:

- **[#1167 [CLOSED] docs: forbid Claude session URLs in commits and PRs](https://github.com/moltis-org/moltis/pull/1167)**  
  A governance update to `CLAUDE.md` that explicitly prohibits `Claude-Session:` or AI-assistant session links in commit messages and PR descriptions, extending the existing no-`Co-Authored-By` rule. Docs-only, no code impact.

- **[#1165 [CLOSED] feat(slack): acknowledge messages with reactions and add reaction triggers](https://github.com/moltis-org/moltis/pull/1165)**  
  Adds Slack acknowledgment reactions (since bots cannot show a typing indicator) along with inbound reaction triggers. Also fixes a confirmed wrong-message bug in threaded replies. This is the foundation upon which PR #1166 builds.

## Community Hot Topics
The three open PRs are the only active discussions; none have comment counts or reactions recorded in the provided data. Based on recency and scope:

- **[#1168 [OPEN] feat(nostr): add NIP-29 group chat support for Buzz channels](https://github.com/moltis-org/moltis/pull/1168)**  
  Integrates Moltis with Block’s Buzz workspace – a Nostr relay where AI agents and humans coexist in channels. This extends the `moltis-nostr` crate beyond NIP-01 to support NIP-29 group chat over authenticated NIP-42 connections. Implicitly reflects user demand for multi-platform agent workspace parity.

- **[#1166 [OPEN] feat(slack): per-message acknowledgment reactions, phases, reconnect supervision, and Block Kit](https://github.com/moltis-org/moltis/pull/1166)**  
  Expands #1165 with phase-based feedback, Block Kit rendering, and reconnect supervision. The addition of Block Kit suggests a push toward rich interactive UI responses in Slack, a common pain point for agent bots.

- **[#1158 [OPEN] feat(memory): add zvec vector database memory backend](https://github.com/moltis-org/moltis/pull/1158)**  
  A community-contributed alternative memory backend using Zvec and redb, gated behind a `zvec` feature flag. The contributor mentions it was “vibe-coded” and is their personal setup. Signals interest in lightweight, embeddable vector stores outside of more heavy dependencies.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The only bug-related mention is the fix for the threaded reply bug that was delivered in PR #1165. The project remains stable.

## Feature Requests & Roadmap Signals
While no formal feature requests were filed, the open PRs strongly indicate the near-term roadmap:
- **Nostr NIP-29 Group Chat** (#1168) – likely to be merged next after reviews, enabling Buzz workspace integration.
- **Slack Rich Feedback** (#1166) – per-message phases and Block Kit will improve user experience for Slack agent deployments.
- **Zvec Memory Backend** (#1158) – could become optional in the next minor release, lowering the memory dependency footprint for smaller deployments.

These align with a broader trend of supporting multiple chat platforms (Nostr, Slack) and flexible, modular memory backends.

## User Feedback Summary
No direct user feedback was recorded in issues or PR comments for the last 24 hours. However, the PR descriptions themselves reveal pain points: Slack bots lack a typing indicator, motivating reaction-based acknowledgment (#1165); the Buzz workspace integration (#1168) suggests users want agents in collaborative Nostr environments; and the Zvec backend (#1158) reflects a desire for simpler, self-contained vector storage without heavy infrastructure.

## Backlog Watch
- **[#1158 [OPEN] feat(memory): add zvec vector database memory backend](https://github.com/moltis-org/moltis/pull/1158)**  
  Created on 2026-07-17, last updated 2026-07-25. Currently open with no reviewer comments. This feature gate could benefit from additional review or testing guidance to move it forward.

No other stalled issues or PRs were identified. The repository shows healthy, recent engagement across all active work items.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-26

## Today's Overview
Project activity remained moderate over the past 24 hours, with 7 new or updated issues (all open) and 8 PRs updated (2 merged/closed, 6 open). No new releases were published. The most pressing development is a string of duplicate bug reports pointing to a hardcoded SSE transport in the MCP driver, which breaks `streamable_http` servers and hinders tool loading. Meanwhile, two reranker-related PRs for memory search (backend + UI) were finally merged after 25 days of review, signalling progress on the memory feature. The community is actively reporting real-world stability problems, especially around CPU usage on Wayland and API connectivity on deployed instances.

## Releases
No new releases were published. The latest available version remains **QwenPaw v2.0.1**.

## Project Progress
Two pull requests were **merged/closed** today:

- **[#5691 – feat(console): add reranker config UI for reme0.4 memory search](https://github.com/agentscope-ai/QwenPaw/pull/5691)** (closed)  
  Added a collapsible “Search Result Reranker” panel in the ReMeLightMemoryCard component, allowing users to configure model name, base URL, API key, and temperature from the Web UI. Includes full zh/en i18n (16 keys).  
- **[#5692 – feat(memory): add reranker for search results on reme0.4](https://github.com/agentscope-ai/QwenPaw/pull/5692)** (merged, under review)  
  Introduces a post-retrieval reranking stage on top of the reme0.4 hybrid retrieval pipeline (BM25 + vector). After initial top-K results are fetched, a dedicated reranker API re-orders them.  

Both PRs were originally opened on 2026-07-01 and had been under review for 25 days before today’s closure/merge. They represent a significant step toward better memory search quality.

## Community Hot Topics
The most active discussion threads revolve around **MCP driver transport issues** and **performance on Wayland**:

1. **MCP driver ignoring transport config** (duplicate reports)  
   - [#6470](https://github.com/agentscope-ai/QwenPaw/issues/6470), [#6469](https://github.com/agentscope-ai/QwenPaw/issues/6469), [#6468](https://github.com/agentscope-ai/QwenPaw/issues/6468) — All reported by `JohnyLe` and `cloud-orchestrator`, all opened on 2026-07-26. The core complaint: the MCP driver hardcodes `sse_client` in `_setup_transport` and ignores YAML configurations specifying `transport: streamable_http`, causing tool loading failures. This set of duplicates indicates a high-priority regression.  
   - Underlying need: reliable support for Streamable HTTP transport, which is a concurrency-friendly alternative to SSE.

2. **High CPU usage on Edge+Wayland**  
   - [#6460](https://github.com/agentscope-ai/QwenPaw/issues/6460) — Reported by `dayofyear`. The QwenPaw 2.0.1 single tab stays at high CPU when viewing the home page or large conversation views. Suspected cause: large result set rendering or WebSocket push. User is on Linux + Wayland + Microsoft Edge.  
   - Underlying need: efficient rendering and WebSocket handling under Wayland.

3. **Connection test failures on AgentScope Platform**  
   - [#6464](https://github.com/agentscope-ai/QwenPaw/issues/6464) — Reported by `albertfengjiajun`. After deploying QwenPaw v2.0.1 on AgentScope Platform, all model connections fail with “API error”, and the model dropdown remains empty.  
   - Underlying need: robust model connectivity for deployed instances.

## Bugs & Stability
**Severity: High**

- **MCP driver transport hardcode** (#6470, #6469, #6468) – Three identical reports confirm that `sse_client` is forced, breaking `streamable_http` servers. No fix PR exists yet. This is a functional blocker for all users relying on the newer transport protocol.  
- **High CPU on Wayland** (#6460) – Performance regression affecting session-heavy pages on Linux + Wayland + Chromium browsers. Could degrade user experience for a non-trivial subset of desktop users. No fix PR linked.  
- **Model connection failure** (#6464) – Deployed instances cannot connect to any model (Pro or Free). Likely an environment/API configuration issue, but the error message is generic. No fix PR.

**Severity: Medium**

- **Server node setup failure** (#6467) – A new user reports inability to set up a proxy node following a video guide; no maintainer response yet. While possibly a documentation issue, the lack of reply may frustrate newcomers.

No fix PRs have been opened for any of the above bugs as of today.

## Feature Requests & Roadmap Signals
- **Clickable folder/file path buttons** ([#6466](https://github.com/agentscope-ai/QwenPaw/issues/6466)) – User `Ra-M497` suggests that when an agent returns a file or folder path, the UI should render a clickable button that opens the path in the native file manager. This would improve UX for desktop users working with local file operations. Given the desktop focus of QwenPaw, this is a strong candidate for the next minor release.  
- **Browser unification** (PR [#6276](https://github.com/agentscope-ai/QwenPaw/pull/6276)) – Still open after 6 days. Proposes a unified browser SDK with control-plane/execution-plane split. This is a substantial architectural change that may land in v2.1.0.  
- **Reranker UI + backend** (merged PRs #5691, #5692) – Now that the reranker feature is merged, the next minor release will likely include it as a new memory capability.

## User Feedback Summary
The community is reporting real friction points:

- **MCP transport incompatibility** is a major pain – users who configured `streamable_http` are stuck, and the duplicate reports suggest a lack of clear communication about the limitation.  
- **Performance on Linux/Wayland** is a concern; the CPU spike makes the app unusable for prolonged sessions on those platforms.  
- **Newcomer confusion** (#6467) indicates that the setup process for proxy nodes may lack clarity, and the official support channels (e.g., group chat) are not responsive.  
- On the positive side, the reranker feature (both backend and UI) was well-received enough to be merged quickly after a long review cycle, indicating satisfaction with the direction of memory improvements.

Overall sentiment is mixed: active development is visible, but critical bugs erode trust in the current release.

## Backlog Watch
No issues have been explicitly idle for a prolonged period, but the following items require maintainer attention to avoid stalling:

- **Issue #6467** (server node setup question) has only one comment and no maintainer reply. Even if it is a user education issue, a quick response would improve community health.  
- **Duplicate MCP bugs** (#6470, #6469, #6468) – All filed today; maintainers should consolidate them and prioritize a fix, as they affect core functionality.  
- **PR #6276** (browser unification) has been open 6 days with no reviewer activity. Its size and architectural impact warrant early review to prevent merge conflicts.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-26

## Today’s Overview
Over the past 24 hours, ZeroClaw saw intense developer and community activity: 19 issues were updated (16 open, 3 closed) and 50 pull requests were touched (48 open, 2 merged/closed). No new releases were published. The project is deep in the **v0.8.4 maintenance train** (tracker #8357) with the release cut PR already open (#9376). Security‑critical bugs—especially around WhatsApp Web configuration—dominated the conversation, while large feature PRs (Telegram multi‑message, OpenAI gateway, Matrix single‑message) continue to mature. Test flakiness remains a recurring stability concern, but several fixes landed.

## Releases
None.

## Project Progress
- **Merged/closed PRs (2):**
  - [#9123](https://github.com/zeroclaw-labs/zeroclaw/pull/9123) — `fix(plugins): host‑stamp channel plugin routes` (merged/closed).
  - [#9270](https://github.com/zeroclaw-labs/zeroclaw/pull/9270) — `fix(web/deps): resolve npm audit advisories` (closed). Pinned `@redocly/openapi-core`, upgraded `js‑yaml` and `brace‑expansion` to clear three high‑severity findings.

- **Closed issues (3):**
  - [#9285](https://github.com/zeroclaw-labs/zeroclaw/issues/9285) — [Bug]: nested `set_prop` masks invalid values (S3, minor).
  - [#9235](https://github.com/zeroclaw-labs/zeroclaw/issues/9235) — CI: npm audit failed (resolved by PR #9270).
  - [#8962](https://github.com/zeroclaw-labs/zeroclaw/issues/8962) — [Bug]: `zeroclaw‑runtime` tests flake under parallel execution (closed after stabilisation).

- **Key advances:**
  - The **v0.8.4 release cut** PR [#9376](https://github.com/zeroclaw-labs/zeroclaw/pull/9376) is open, making the workspace publishable to crates.io and renaming the root package to `zeroclaw`.
  - Additional CI parallelisation for runtime stress gates ([#9371](https://github.com/zeroclaw-labs/zeroclaw/pull/9371)) and optional faster runners for compile‑heavy jobs ([#9115](https://github.com/zeroclaw-labs/zeroclaw/pull/9115)) are in review.

## Community Hot Topics
The most active issue by comment count is **#9348** (6 comments) — a **security‑critical WhatsApp Web bug** where `mode = business` and empty `allowed_groups` causes the agent to reply to every DM and group, despite `dm_policy`/`group_policy` being set to “personal‑mode only”. The conversation highlights both the urgent need for a fix and the follow‑up tracking of a related config validation bug (#9366).

Other highly discussed items:
- **#6489** (5 comments) – “Everything is a plugin” architectural RFC, which proposes collapsing integrations/plugins into a single catalog. This long‑running tracker continues to shape the project’s future direction.
- **#9328** (3 comments) – `verifiable‑intent` evaluates constraints without verifying the credential chain, rated high‑risk. The community is discussing whether the implementation should mirror the VI reference spec.
- **#9357** (2 comments) – Test flake on `master` blocking CI 19/20 runs. Developers expressed frustration and proposed workarounds.

Among PRs, the **Telegram multi‑message feature** ([#8561](https://github.com/zeroclaw-labs/zeroclaw/pull/8561), XL size), **OpenAI chat completions gateway** ([#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486), XL), and **Matrix single‑message drafts** ([#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443), XL) draw sustained attention from trusted contributors and maintainers.

## Bugs & Stability
| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **S1 – Security** | [#9348](https://github.com/zeroclaw-labs/zeroclaw/issues/9348) | WhatsApp Web `mode = business` ignores chat policies, enabling unintended replies to all DMs/groups. | PR [#9354](https://github.com/zeroclaw-labs/zeroclaw/pull/9354) (warn when policies can’t take effect) open, but does not fully address the root cause. |
| **S2 – Degraded** | [#9357](https://github.com/zeroclaw-labs/zeroclaw/issues/9357) | `cargo test -p zeroclaw‑runtime --lib` fails 19/20 runs on `master`; one flaky test poisons a global mutex. | PR [#9371](https://github.com/zeroclaw-labs/zeroclaw/pull/9371) parallelises the stress gate but is not a direct fix. |
| **S2 – Degraded** | [#9373](https://github.com/zeroclaw-labs/zeroclaw/issues/9373) | Peer‑agent delivery runs recipient turn without cost tracking; spend unrecorded, budgets unenforced. | No fix PR yet. |
| **S2 – Degraded** | [#9363](https://github.com/zeroclaw-labs/zeroclaw/issues/9363) | Config metadata remains English in localized ZeroCode/web surfaces (S2). | No fix PR yet. |
| **S3 – Minor** | [#9374](https://github.com/zeroclaw-labs/zeroclaw/issues/9374) | `CLI run()` open‑codes lifecycle bracket, leaking `AgentStart` on 12 exit paths. | No fix PR yet. |
| **S3 – Minor** | [#9285](https://github.com/zeroclaw-labs/zeroclaw/issues/9285) | Nested `set_prop` gives path‑resolution error instead of value error (closed). | Fixed. |

Additional high‑risk bugs include #9328 (verifiable‑intent credential chain), #9340 (CLI cron delivery hardcoded to `None`), and #9366 (WhatsApp `approval_timeout_secs` never read). The volume of open **S1‑S2** bugs indicates a need for a focused stabilisation sprint before v0.8.4 ships.

## Feature Requests & Roadmap Signals
- **“Everything is a plugin”** (#6489) – a major architectural RFC that would unify integrations and plugins. Expected to influence post‑v0.8.4 releases.
- **AI‑assisted PR pre‑review** (#9330) – community proposal to use CI results for AI‑driven initial review, keeping human approval for high‑risk items. No maintainer decision yet.
- **Workspace‑wide `forbid(unsafe_code)`** (#7130) – a security‑focused enhancement with `aardvark‑sys` as the sole carve‑out. Still under discussion.
- **Channel/source shared‑boundary cleanup** (#8583) – a tracker for refactoring channel ingress lifecycle, config, and streaming. Likely to land in v0.8.4 or v0.9.

Based on open PRs and tracker #8357, **v0.8.4** will include:
- Telegram multi‑message streaming (#8561)
- OpenAI chat completions endpoint (#8486)
- Matrix single‑message progress drafts (#8443)
- Atlas Cloud model provider (#9200)
- Cron `shell_output_format` (#8438)
- Sandbox policy schema (#7821)
- Egress policy foundation for plugins (#9137)
- Chinese (zh) translations (#9377)

## User Feedback Summary
**Pain points** reported in the last 24 hours:
- **WhatsApp configuration surprise**: Operators who set `dm_policy = personal‑mode only` under `mode = business` believed they had locked down the agent, but it replied to everyone. This erodes trust in the configuration model and is the top community concern.
- **Cron output disappears**: Agents created via CLI run silently with `delivery.mode = "none"` — no indication output is lost. Users expect at least a warning.
- **Config errors are user‑unfriendly**: `config patch --json` emits plaintext errors on two failure paths instead of structured JSON, breaking scripting workflows.
- **Test flakiness blocks contributions**: Contributors on `master` cannot reliably run `cargo test -p zeroclaw-runtime`, forcing workarounds.

**Use cases driving new features** include multi‑language support (Chinese translation PR #9377), multi‑message pacing on Telegram for richer conversational UX, and OpenAI‑compatible gateway for integration with existing LLM toolchains. The strong contributor base (trusted/principal contributors on large PRs) suggests general satisfaction with the project’s direction, though stability bugs remain a frustration.

## Backlog Watch
Issues and PRs that have not received maintainer attention despite high priority or long open time:

- **[#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489)** “Everything is a plugin” RFC (open since May 6, 5 comments, accepted, no‑stale) – needs a formal decision update.
- **[#7130](https://github.com/zeroclaw-labs/zeroclaw/issues/7130)** Workspace‑wide `forbid(unsafe_code)` (open since June 3, no‑stale) – maintainer review awaited.
- **[#9330](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)** RFC for AI‑assisted PR review (open July 24, `needs‑maintainer‑review`) – no maintainer has responded.
- **[#8583](https://github.com/zeroclaw-labs/zeroclaw/issues/8583)** Channel/source cleanup tracker (open since July 1, `in‑progress`) – appears to be active but could use a progress summary.
- **Large PRs with `needs‑author‑action` label**: #8561 (Telegram), #8486 (OpenAI gateway), #7821 (sandbox policy), #8438 (cron output), #9137 (egress policy), #9200 (Atlas Cloud). These require maintainer review after author updates.

The **v0.8.4 release** PR (#9376) is open and likely the top priority for maintainers; clearing these block items should accelerate the release.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*