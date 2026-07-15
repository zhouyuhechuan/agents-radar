# OpenClaw Ecosystem Digest 2026-07-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-15 01:45 UTC

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

# OpenClaw Project Digest — 2026-07-15

## 1. Today’s Overview
The OpenClaw project remains intensely active, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of the updated issues, 343 are open/active and 157 were closed; among PRs, 337 remain open while 163 were merged or closed. **No new releases** were published today. The community is heavily engaged on release-blocker bugs (P0 gateway crash-loops on the latest `2026.7.1` update) and long-standing feature requests (Linux/Windows app support, memory security, multi-platform expansion). Despite high open issue counts, maintainer and community response is rapid, with several critical bugs already linked to fix PRs or resolved.

## 2. Releases
*No new releases today.*

## 3. Project Progress
**Merged/Closed PRs (selected notable):**
- [#107727](https://github.com/openclaw/openclaw/issues/107727) — *Gateway refuses readiness after 2026.7.1 update* (closed)
- [#107133](https://github.com/openclaw/openclaw/issues/107133) — *Memory Core embedding_cache conflict permanently blocks Gateway startup* (closed)
- [#107330](https://github.com/openclaw/openclaw/issues/107330) — *Openclaw Update 2026.7.1 Crash* (closed)
- [#102749](https://github.com/openclaw/openclaw/issues/102749) — *Startup legacy-state migration never converges when .migrated archive already exists* (closed)
- [#50442](https://github.com/openclaw/openclaw/issues/50442) — *backup create leaves large .tmp files on timeout causing disk space exhaustion* (closed)
- [#22676](https://github.com/openclaw/openclaw/issues/22676) — *Signal daemon stop() race condition on SIGUSR1 restart* (closed)

These closures indicate rapid stabilization work on the `2026.7.1` gateway startup regressions and other long-standing reliability issues. Additional open PRs that reflect ongoing feature work include system-agent delegation ([#107903](https://github.com/openclaw/openclaw/pull/107903)), UI improvements for copy buttons ([#107904](https://github.com/openclaw/openclaw/pull/107904)), and Codex harness opt‑out ([#97224](https://github.com/openclaw/openclaw/pull/97224)).

## 4. Community Hot Topics
The most active discussions by comment and reaction volume:

- [#75](https://github.com/openclaw/openclaw/issues/75) **Linux/Windows Clawdbot Apps** — 113 comments, 81 👍. Users strongly demand desktop app support beyond macOS/iOS/Android. The underlying need is cross-platform parity for agent interaction.
- [#48788](https://github.com/openclaw/openclaw/issues/48788) **Centralized filename encoding utility for multi-encoding Content-Disposition** — 19 comments. A technical architectural request to handle Chinese, Japanese, and Korean filenames across all channel adapters.
- [#7707](https://github.com/openclaw/openclaw/issues/7707) **Memory Trust Tagging by Source** — 18 comments. Users want to tag agent memory by origin (user, web, third‑party) to prevent memory poisoning.
- [#94518](https://github.com/openclaw/openclaw/issues/94518) **DeepSeek cache hit rate <10% after 6.x upgrade** — 9 comments, 10 👍. A performance regression causing high costs; community is seeking a fix.
- [#10659](https://github.com/openclaw/openclaw/issues/10659) **Masked Secrets – Prevent Agent from Accessing Raw API Keys** — 14 comments, 4 👍. Security‑focused feature request for credential isolation.
- [#107227](https://github.com/openclaw/openclaw/issues/107227) **2026.7.1 startup‑migration gate is fatal** — 6 comments, 1 👍. A release‑blocker with high urgency, already linked to closed fixes.

## 5. Bugs & Stability
Several critical and high‑severity bugs were active today, primarily related to the `2026.7.1` update and gateway startup.

### P0 / Release‑Blockers
| Issue | Summary | Status |
|-------|---------|--------|
| [#101290](https://github.com/openclaw/openclaw/issues/101290) | CLI startup preflight corrupts live state DB while gateway is running – “database disk image is malformed” (macOS) | Open; no fix PR linked |
| [#107227](https://github.com/openclaw/openclaw/issues/107227) | 2026.7.1 startup‑migration gate fatal; `openclaw doctor` does not resolve | Open; likely resolved by related closed issues |
| [#107133](https://github.com/openclaw/openclaw/issues/107133) | Memory Core embedding_cache conflict blocks startup permanently on 2026.7.1 | **Closed** |
| [#102749](https://github.com/openclaw/openclaw/issues/102749) | Startup legacy‑state migration never converges when `.migrated` archive exists | **Closed** |
| [#107220](https://github.com/openclaw/openclaw/issues/107220) | 2026.7.1 gateway crash‑loop: legacy memory sidecar meta/chunks fatal, files auto‑resolves | Open; linked PR may be pending |
| [#107330](https://github.com/openclaw/openclaw/issues/107330) | OpenClaw Update 2026.7.1 Crash (Windows) | **Closed** |

### P1 Regressions and Behavior Bugs
- [#90213](https://github.com/openclaw/openclaw/issues/90213) – Legacy state migration warnings persist after `doctor --fix` (2026.6.1 regression, open)
- [#87744](https://github.com/openclaw/openclaw/issues/87744) – Codex‑backed Telegram timeouts on turn/completed (2026.5.27 regression, open)
- [#95121](https://github.com/openclaw/openclaw/issues/95121) – Codex OAuth turns spend ~28s extra for tiny replies (2026.6.8 regression, open)
- [#107449](https://github.com/openclaw/openclaw/issues/107449) – cron tool JSON Schema incompatible with llama.cpp tool parser (regression, **fix PR [#107605](https://github.com/openclaw/openclaw/pull/107605) open**)

### Summary of Stability
Many of today’s most impactful bugs were the startup‑migration and gateway crash‑loop issues on `2026.7.1`. **Several have already been closed**, indicating a fast maintainer response. However, the P0 database corruption issue (#101290) remains open with no fix PR, and multiple older regressions (e.g., webchat transcript overwrite #77012, session yield resume delivery #90944) are still awaiting resolution.

## 6. Feature Requests & Roadmap Signals
Strong user demand for features that enhance security, platform reach, and agent control:

| Feature | Issue | Comments | Likely Next‑Version Signal |
|---------|-------|----------|----------------------------|
| **Linux/Windows Clawdbot Apps** | [#75](https://github.com/openclaw/openclaw/issues/75) | 113 | High visibility, but scope large; may land incrementally |
| **Memory Trust Tagging by Source** | [#7707](https://github.com/openclaw/openclaw/issues/7707) | 18 | Archived under `needs‑product‑decision`; mid‑priority |
| **Masked Secrets – raw API key isolation** | [#10659](https://github.com/openclaw/openclaw/issues/10659) | 14 | Security‑critical, likely high on roadmap |
| **Per‑Agent TTS/STT Configuration Overrides** | [#66252](https://github.com/openclaw/openclaw/issues/66252) | 8 | Multi‑language voice support; could appear in 2026.8 |
| **Denylist support for exec‑approvals** | [#6615](https://github.com/openclaw/openclaw/issues/6615) | 9 | Simple extension; may merge soon |
| **Centralized filename encoding utility** | [#48788](https://github.com/openclaw/openclaw/issues/48788) | 19 | Technical architecture; could land as separate library |
| **Suppress sub‑agent announce via config** | [#8299](https://github.com/openclaw/openclaw/issues/8299) | 7 | UX improvement; linked PR may be pending |

Also notable: **Multi‑Session Architecture RFC** ([#48874](https://github.com/openclaw/openclaw/issues/48874)) proposes a shared LLM layer with isolated sessions, which would fundamentally improve resource usage for heavy deployments.

## 7. User Feedback Summary
**Pain points expressed today:**
- **Upgrade friction:** Multiple users on `2026.7.1` reported gateway crash‑loops, migration freezes, and “no documented remedy” ([#107227](https://github.com/openclaw/openclaw/issues/107227), [#107220](https://github.com/openclaw/openclaw/issues/107220), [#107133](https://github.com/openclaw/openclaw/issues/107133)).
- **Cross‑platform gaps:** Linux/Windows app lack remains the top comment‑count issue ([#75](https://github.com/openclaw/openclaw/issues/75)), echoed in many smaller requests for parity.
- **Message delivery issues:** Telegram DM lane guarding ([#91456](https://github.com/openclaw/openclaw/issues/91456)), WhatsApp image wedging ([#96834](https://github.com/openclaw/openclaw/issues/96834)), and session transcript loss ([#77012](https://github.com/openclaw/openclaw/issues/77012)).
- **LLM‑specific regressions:** DeepSeek cache collapse ([#94518](https://github.com/openclaw/openclaw/issues/94518)), llama.cpp tool schema incompatibility ([#107449](https://github.com/openclaw/openclaw/issues/107449)), and MiniMax reasoning drops ([#92769](https://github.com/openclaw/openclaw/issues/92769)).
- **Security:** Requests for masked secrets, memory trust tagging, and denylist for exec‑approvals highlight growing concern about agent‑side credential safety and memory poisoning.

**Satisfaction signals:**
- Fast turnaround on release‑blocker fixes (several P0 bugs closed within hours).
- Active community involvement with detailed bug reports and PRs (e.g., `#107449` → `#107605`).

## 8. Backlog Watch
Issues and PRs that have gone stale or are awaiting maintainer action:

### Stalled High‑Severity Bugs
| Issue | Last Update | Days Since Update | Notes |
|-------|-------------|-------------------|-------|
| [#80040](https://github.com/openclaw/openclaw/issues/80040) – Cascading OAuth failure, duplicate tool execution | 2026-07-14 | ~1 (stale tag) | `needs‑maintainer‑review`, `needs‑product‑decision` |
| [#77012](https://github.com/openclaw/openclaw/issues/77012) – WebChat transcript overwritten every turn | 2026-07-14 | ~1 (stale tag) | Regression from May; `needs‑live‑repro` |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) – WhatsApp image wedges lane | 2026-07-14 | ~1 | `needs‑maintainer‑review`, `needs‑product‑decision` |
| [#87999](https://github.com/openclaw/openclaw/issues/87999) (not shown but inferred from many stale items) | – | – | Many issues tagged `stale` and `needs‑maintainer‑review` |

### PRs Awaiting Maintainer Review
| PR | Summary | Status |
|----|---------|--------|
| [#87377](https://github.com/openclaw/openclaw/pull/87377) – Task flow lifecycle observability | `needs proof` |
| [#86655](https://github.com/openclaw/openclaw/pull/86655) – Claude Bridge app‑server harness | `waiting on author` |
| [#88681](https://github.com/openclaw/openclaw/pull/88681) – Runtime plugin startup diagnostics | `waiting on author` |
| [#88180](https://github.com/openclaw/openclaw/pull/88180) – Preserve IDENTITY defaults in system prompt | `waiting on author` |
| [#88479](https://github.com/openclaw/openclaw/pull/88479) – In‑chat session picker inline rename | `ready for maintainer look` |

### Long‑standing Feature Requests Without Decision
- [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows apps (created Jan 2026, 7 months stale)
- [#10659](https://github.com/openclaw/openclaw/issues/10659) – Masked Secrets (Feb 2026)
- [#7707](https://github.com/openclaw/openclaw/issues/7707) – Memory Trust Tagging (Feb 2026)

These items have community consensus but await product decisions or maintainer capacity. The frequent `clawsweeper:needs-product-decision` and `clawsweeper:needs-maintainer-review` labels suggest that maintainer bandwidth is a bottleneck despite high activity.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Analysis Date:** 2026-07-15

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape continues to experience intense development velocity, with seven of eleven tracked projects showing significant daily activity. The ecosystem is bifurcating into two tiers: **core infrastructure projects** (OpenClaw, Hermes Agent, CoPaw, ZeroClaw) that process 500+ daily issue/PR updates, and **specialized implementations** (NanoBot, Moltis, LobsterAI) that prioritize stability and targeted feature delivery. A critical pattern emerging across all active projects is the tension between rapid feature expansion and reliability—several projects (OpenClaw, CoPaw, ZeroClaw) experienced release-blocker regressions in their latest updates, while maintaining high community engagement. The ecosystem is clearly past the "proof of concept" phase and entering a period of production hardening, with multi-user isolation, memory security, and cross-platform parity emerging as universal requirements.

---

## 2. Activity Comparison

| Project | Issues Updated (Open/Closed) | PRs Updated (Open/Merged) | Release Today | Health Score | Notes |
|---------|------------------------------|---------------------------|---------------|--------------|-------|
| **OpenClaw** | 500 (343/157) | 500 (337/163) | ❌ | **Moderate** | High volume with P0 regressions; rapid fix turnaround |
| **Hermes Agent** | 50 (7/43) | 50 (46/4) | ❌ | **Strong** | Excellent closure rate; low merge velocity today |
| **NanoBot** | 10 (3/7) | 64 (17/47) | ❌ | **Strong** | High merge rate; fast issue resolution |
| **IronClaw** | 48 (36/12) | 50 (23/27) | ❌ | **Moderate** | Major refactor in progress; CI flakiness concerns |
| **ZeroClaw** | 29 (23/6) | 50 (38/12) | ❌ | **Moderate** | SOP engine progress; P1 security bugs open |
| **CoPaw** | 50 (16/34) | 50 (24/26) | ✅ v2.0.0.post2 | **Good** | Hotfix release; sandbox regressions being addressed |
| **NanoClaw** | 0 | 26 (19/7) | ❌ | **Moderate** | No issues, but 7 PRs merged; delivery bugs persist |
| **PicoClaw** | 3 (3/0) | 9 (4/5) | ❌ | **Good** | Small scope; steady fix velocity |
| **LobsterAI** | 4 (0/4) | 3 (0/3) | ❌ | **Strong** | All stale issues closed; maintenance phase |
| **Moltis** | 3 | 12 (4/8) | ✅ 20260714.11 | **Strong** | Clean merge velocity; targeted fixes |
| **NullClaw** | 0 | 0 | ❌ | **Inactive** | No activity |
| **TinyClaw** | 0 | 0 | ❌ | **Inactive** | No activity |
| **ZeptoClaw** | 0 | 0 | ❌ | **Inactive** | No activity |

**Health Score Methodology:** Based on issue closure rate, PR merge ratio, presence of critical unaddressed bugs, and release stability. "Strong" indicates >70% closure/merge rate with no P0 open bugs. "Moderate" indicates either high open volume or critical regressions with active fixes. "Good" indicates balanced activity with manageable risk.

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Community scale:** 500 daily issue/PR updates dwarfs all peers (next closest: Hermes/CoPaw at 50). Issue #75 (Linux/Windows apps) has 113 comments—more engagement than any single topic in any other project.
- **Core reference status:** As the original reference implementation, OpenClaw sets architectural patterns that others follow (e.g., LobsterAI backports fixes from OpenClaw upstream).
- **Ecosystem gravity:** The 343 open issues and 337 open PRs indicate a massive contributor base, though this also reflects triage bottlenecks.
- **Platform breadth:** Already supports macOS/iOS/Android; the demand for Linux/Windows (#75) shows users see it as the de facto standard.

**Technical Approach Differences:**
- OpenClaw uses a **monolithic gateway-architecture** with sidecar processes (legacy memory sidecar, Codex backend). This contrasts with NanoClaw's microservice-like containerized approach and PicoClaw's lightweight single-binary design.
- OpenClaw's **2026.7.1 release suffered gateway crash-loops** from startup-migration regressions—a complexity cost of its mature architecture that simpler projects (Moltis, PicoClaw) avoid.
- Memory subsystem is more advanced (embedding caching, trust tagging proposals #7707) than peers, but also more fragile (embedding_cache conflict #107133).

**Community Size Comparison:**
OpenClaw's community is **5-10x larger** than any single peer based on issue/PR volume. However, its maintainer bandwidth appears stretched—many issues carry `needs-product-decision` labels, and the "help wanted" issues (e.g., #75) have gone untouched for 7 months. In contrast, smaller projects like Moltis and NanoBot have faster per-issue resolution times.

---

## 4. Shared Technical Focus Areas

Several requirements appear across **three or more projects**, indicating ecosystem-wide pain points:

| Focus Area | Projects Affected | Specific Needs |
|-----------|------------------|----------------|
| **Cross-Platform Desktop Support** | OpenClaw (#75), NanoBot (WebUI work), Hermes (Windows update failures #64457), PicoClaw (config gaps) | All projects have macOS/iOS/Android but lack full Linux/Windows parity for agent interaction |
| **Memory Security & Isolation** | OpenClaw (#7707 trust tagging), Hermes (#50734 credential exfiltration), ZeroClaw (#5982 RBAC), CoPaw (#6113 memory loops) | Growing demand for provenance tracking, source-based trust, and preventing memory poisoning |
| **Multi-Tenant / Multi-User RBAC** | ZeroClaw (#5982, #8290), OpenClaw (Multi-Session RFC #48874), IronClaw (extension lifecycle isolation) | Enterprises and shared deployments need per-user tool gating, rate limiting, session isolation |
| **Provider / Model Compatibility** | OpenClaw (DeepSeek #94518), Hermes (NVIDIA NIM #50703, vLLM #51530), CoPaw (DeepSeek context compression #6121), Moltis (local model quirks #1098, #1136) | API translation layers break with new models; universal need for parameter forwarding and null handling |
| **Message Delivery Reliability** | NanoClaw (attachment drops #2888, outbound.db races), IronClaw (Slack "thinking" hang #6092, ordering #6047), OpenClaw (Telegram DM lane #91456), ZeroClaw (Slack thread hydration #6055) | Streaming, ordering, channel-specific delivery guarantees remain unsolved across the board |
| **Observability & Diagnostics** | ZeroClaw (OTel correlation #8933), NanoBot (Codex failure stage #4929), IronClaw (error fidelity #6108), OpenClaw (gateway crash diagnostics) | Generic error messages and swallowed diagnostics are a universal frustration |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | NanoBot | CoPaw | ZeroClaw | Moltis |
|-----------|----------|--------------|---------|-------|----------|--------|
| **Primary Focus** | General-purpose agent OS | Multi-provider chat agent | Lightweight personal assistant | Tool-use & sandbox | Enterprise workflow (SOP) | Browser automation & MCP |
| **Target User** | Power users, developers | Developers, self-hosters | Individual users | Security-conscious users | Enterprises, multi-tenant | Developers, integrators |
| **Architecture** | Monolithic gateway + sidecars | Modular provider adapters | Channel-based microservices | Plugin architecture | SOP engine + RBAC | Lightweight core + extensible channels |
| **Deployment Model** | macOS/iOS app + CLI | Docker/CLI | Render one-click + CLI | Desktop + server | Server + web dashboard | CLIs + Docker |
| **Key Differentiator** | Largest ecosystem, most features | Fastest bug turnaround (43/50 closed) | Highest merge velocity (47/64 today) | Strongest sandbox/governance | Only SOP engine + multi-user | Best browser + MCP integration |
| **Stability Profile** | Moderate (release regressions) | Strong (rapid fixes) | Strong (few open bugs) | Good (hotfix released) | Moderate (P1 security bugs) | Strong (clean backlog) |

**Notable architectural contrasts:**
- **ZeroClaw** is the only project with a dedicated **SOP (Standard Operating Procedure) engine**, targeting workflow automation rather than ad-hoc chat. This makes it suitable for enterprise use cases others don't address.
- **Moltis** uniquely integrates **MCP (Model Context Protocol) servers** and **browser automation** as first-class features, differentiating from general-purpose agents.
- **CoPaw** has the most aggressive **sandbox/governance model**, with AppContainer isolation on Windows and cgroup support—but this complexity causes the most regressions.
- **NanoBot** is the only project offering **one-click Render deployment**, lowering the entry barrier for non-technical users.

---

## 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration (Ship Velocity >20 PRs/day merged)**
- **NanoBot** (47 merged PRs today) – highest per-day merge rate; clearly in active feature expansion
- **ZeroClaw** (12 merged) – SOP engine nearing completion; plugin infrastructure maturing
- **CoPaw** (26 merged) – post-v2.0.0 stabilization with hotfix release
- **IronClaw** (27 merged) – major extension-runtime refactor (Train A/B) nearing completion

**Tier 2: Sustained Development (10-20 PRs/day merged)**
- **Hermes Agent** (4 merged, but 43 issues closed) – rapid bug fixing; codebase maturing
- **OpenClaw** (163 merged) – high volume but reflects backlog; true velocity diluted by scale
- **Moltis** (8 merged) – steady, measured pace with targeted releases

**Tier 3: Stabilization (0-5 PRs/day merged)**
- **LobsterAI** (3 merged) – maintenance mode; backporting upstream fixes
- **PicoClaw** (5 merged) – incremental improvements; low bug count
- **NanoClaw** (7 merged) – delivery-focused fixes; no feature expansion

**Tier 4: Inactive**
- **NullClaw, TinyClaw, ZeptoClaw** – no activity; possibly abandoned or on hiatus

**Maturity Assessment:**
The ecosystem is **mid-maturation**. No project has achieved "stable release" status with predictable release cadences. OpenClaw's `2026.7.1` upgrade regressions, CoPaw's v2.0.0 sandbox issues, and IronClaw's 70% CI failure rate all indicate that projects are prioritizing feature velocity over release reliability. The most mature projects by stability are **Moltis** and **LobsterAI**, which have smaller scopes and lower feature ambitions.

---

## 7. Trend Signals

**1. Multi-Tenancy and RBAC Are Becoming Table Stakes**
ZeroClaw's #5982 (per-sender RBAC) has 10 comments; OpenClaw's Multi-Session RFC is in discussion; IronClaw's extension isolation work is progressing. Enterprises adopting AI agents need separation of concerns. *Signal: The next 6 months will see RBAC become a standard feature across all major projects.*

**2. Local and Small Model Support Is a Growing Pain Point**
Three projects (Hermes, Moltis, CoPaw) specifically fixed bugs related to local model quirks today—null optional params, stringified scalars, incompatible schemas. As Llama.cpp, Gemma, and Qwen adoption grows, provider translation layers must handle non-OpenAI behavior. *Signal: Expect a push for standardized "model adapter" interfaces that abstract provider differences.*

**3. Security Is Moving from "Nice to Have" to "Must Have"**
Today alone: OpenClaw's credential exfiltration fix (#50734), CoPaw's sandbox bypass fixes, ZeroClaw's Landlock bug (#8973), and the universal demand for masked secrets across four projects. The `.env` credential leak in Hermes (#50734) alarmed the community. *Signal: Supply-chain security (dependency gates, image provenance) and credential isolation will be release-blocking features in upcoming versions.*

**4. Cost Optimization via Caching Is Emergent**
OpenClaw's DeepSeek cache collapse (#94518), PicoClaw's Bedrock prompt caching PRs (#3163, #3228), and IronClaw's context-window cache concerns (#6100) all point to users hitting cost walls with LLM APIs. *Signal: Caching strategies (semantic, prompt, context) will be a competitive differentiator for projects targeting production deployments.*

**5. Channel Parity Is Still an Unsolved Problem**
Telegram, Slack, Discord, WhatsApp, LINE, DingTalk, Feishu, Dial (just added by NanoClaw)—the list grows, but every project struggles with channel-specific bugs (message formatting, threading, attachments, authentication). *Signal: A channel abstraction layer or "channel SDK" could emerge as a horizontal need, similar to how MCP standardizes tool definitions.*

**6. AI Agent Developers Are Demanding Better Debugging UX**
ZeroClaw's OTel correlation RFC (#8933), NanoBot's Codex stage identification (#4929), IronClaw's error fidelity policy (#6108), and OpenClaw's crash-loop diagnostics all point to the same need: agents are becoming too complex to debug with generic error messages. *Signal: Observability tooling (tracing, logging, failure taxonomy) will be a key investment area for projects targeting professional developers.*

**7. The "Personal AI" Market Is Segmenting by Deployment Context**
The ecosystem is splitting along deployment lines:
- **Desktop-centric**: OpenClaw (macOS app), Hermes (desktop CLI)
- **Cloud/SaaS**: ZeroClaw (web dashboard), NanoBot (Render deploy)
- **Enterprise on-prem**: IronClaw (extension runtime), CoPaw (sandbox-heavy)
- **Embedded/lightweight**: PicoClaw, Moltis (small-footprint core)

*Signal: Projects that can bridge these contexts (e.g., OpenClaw adding Linux/Windows desktop apps) will have a strategic advantage

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-07-15

## Today's Overview
NanoBot has seen intense development activity in the last 24 hours, with 64 pull requests updated and 47 of those merged or closed. Three new issues remain open, while a total of 10 issues were resolved. No new release was cut today, but the high rate of merged PRs suggests a near-term release may be imminent. The project continues to mature rapidly, with significant attention to heartbeats, WebUI, channel stability, and memory management.

## Releases
No new releases were created today. The last published version is v0.1.4 (with post releases). Users should track the `main` branch for the latest fixes and features; no migration notes apply for today.

## Project Progress
47 pull requests were merged or closed today, advancing both bug fixes and new capabilities:

- **Heartbeat & Cron Improvements**  
  - [#4928 – fix(heartbeat): route unified sessions to last channel](https://github.com/HKUDS/nanobot/pull/4928) – persists concrete channel routes for unified sessions, fixing heartbeat target selection when no individual sessions exist.  
  - [#4915 – fix(heartbeat): make response evaluation more configurable](https://github.com/HKUDS/nanobot/pull/4915) – adds ability to disable heartbeat evaluation and stricter prompt for evaluator.  
  - [#4620 – add heartbeat trigger command](https://github.com/HKUDS/nanobot/pull/4620) – introduces `nanobot heartbeat trigger` with dry-run and JSON output modes, sharing workspace lock between CLI and gateway timer.  
  - [#4549 – feat(heartbeat): add model_override config](https://github.com/HKUDS/nanobot/pull/4549) – allows operators to route routine heartbeat checks to a cheaper/dedicated model.

- **WebUI Enhancements**  
  - [#4933 – feat(webui): highlight slash commands and app mentions](https://github.com/HKUDS/nanobot/pull/4933) – renders recognised slash commands with a soft-glow treatment.  
  - [#4930 – feat(webui): add copy action to user messages](https://github.com/HKUDS/nanobot/pull/4930) – adds copy button to user messages.  
  - [#4927 – fix(webui): sync package-lock.json for qrcode dependency](https://github.com/HKUDS/nanobot/pull/4927) – fixes Docker build failures from missing lock file.  
  - [#4931 – fix(restart): deliver completion after channel reconnects](https://github.com/HKUDS/nanobot/pull/4931) – ensures restart notice is sent only after the target channel is ready.

- **Channel & Integration Work**  
  - [#4908 – refactor(channels): move setup and instance ownership to channels](https://github.com/HKUDS/nanobot/pull/4908) – decouples channel setup from core architecture, supporting Feishu multi-instance and custom lifecycle.  
  - [#4446 – feat(dingtalk): gate private chats and mention sender in group replies](https://github.com/HKUDS/nanobot/pull/4446) – adds `disable_private_chat` flag and sender mention in group replies.

- **Memory & Archive**  
  - [#4621 – feat(memory): gate archive facts with provenance context](https://github.com/HKUDS/nanobot/pull/4621) – includes `MEMORY.md` excerpt in Consolidator prompts to skip duplicate facts and recognise corrections earlier.

- **Execution Isolation**  
  - [#4862 – fix(exec): isolate exec session managers](https://github.com/HKUDS/nanobot/pull/4862) – gives each AgentLoop and SubagentManager its own ExecSessionManager, preventing cross-session interference.

- **Deployment**  
  - [#4937 – feat: add one-click Deploy to Render support](https://github.com/HKUDS/nanobot/pull/4937) – introduces a Render Blueprint for single-click deployment with persisted session history and memory.

- **CI & Testing**  
  - [#4936 – test: speed up CI and harden the suite](https://github.com/HKUDS/nanobot/pull/4936) – replaces duplicated Python OS/version matrix with representative jobs and makes several test suites deterministic.  
  - [#4631 – test: add scripted agent runner harness](https://github.com/HKUDS/nanobot/pull/4631) – reusable test harness for agent runner that captures exact transcripts.

- **Miscellaneous Fixes**  
  - [#4932 – fix: standardize --config help text across CLI commands](https://github.com/HKUDS/nanobot/pull/4932) – aligns inconsistent help text.  
  - [#4929 – chore(codex): identify failing request stage](https://github.com/HKUDS/nanobot/pull/4929) – adds stage field to Codex failure warnings for easier debugging.  
  - [#4890 – fix(api): avoid retaining idle session locks](https://github.com/HKUDS/nanobot/pull/4890) – replaces lock store with `WeakValueDictionary` to prevent unbounded lock growth.

## Community Hot Topics
The most active discussions and issues reflect user interest in reliability, cross-platform support, and better observability:

- **Telegram Markdown Rendering (Issue #2568)** – [closed] Reported markdown not rendering reliably after v1.4.post6. The issue garnered 4 comments and was closed today, suggesting a fix is in place.
- **Unified Session Heartbeat Crash (Issue #4924)** – [open] When `unifiedSession: true` and no separate sessions exist, `_pick_heartbeat_target_from_sessions` fails. 3 comments. A companion PR (#4928) has been submitted to fix this.
- **Cron Job Channel Messages (Issue #1445)** – [closed] Users wanted to suppress channel messages for cron jobs that “did nothing meaningful.” 2 comments and 2 👍, now closed – likely addressed by the heartbeat evaluation config (#4915).
- **WhatsApp Bridge WebSocket Binding (Issue #1086)** – [closed] Inter-container communication blocked by binding to 127.0.0.1. 4 👍, now closed – a popular pain point for Docker users.
- **Memory Resource Leak (Issue #4787)** – [open] `Session.messages` list grows without bound; `FILE_MAX_MESSAGES` only caps display, not storage. 1 comment, but high severity. No fix PR yet.
- **Qwen Models Expose Reasoning Content (Issue #4934)** – [open] Qwen models via DashScope leak thinking/reasoning content into chat responses. 0 comments (very new), but urgent for users of these models.

## Bugs & Stability
Today saw several bug fixes merged, but three open issues require attention:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#4787 – Resource leak: Session.messages unbounded](https://github.com/HKUDS/nanobot/issues/4787) | `Session.messages` list grows indefinitely for long-running sessions, leading to memory pressure. | No open PR yet |
| **Medium** | [#4924 – Heartbeat fails with unifiedSession](https://github.com/HKUDS/nanobot/issues/4924) | `_pick_heartbeat_target_from_sessions` fails when only a unified session exists (no individual sessions). | [#4928](https://github.com/HKUDS/nanobot/pull/4928) – open |
| **Medium** | [#4934 – Qwen models expose thinking content](https://github.com/HKUDS/nanobot/issues/4934) | Reasoning/thinking content from Qwen models incorrectly appears in chat responses via DashScope provider. | None yet |
| **Closed** | [#4795 – Streaming LLM calls bypass wall-clock timeout](https://github.com/HKUDS/nanobot/issues/4795) | Streaming requests set `outer_timeout_s = None`, causing indefinite stalls. Fixed. | Merged |
| **Closed** | [#4881 – Windows ExecTool corrupts PowerShell UTF-16 output](https://github.com/HKUDS/nanobot/issues/4881) | Subprocess stdout decoded as UTF-8 corrupts UTF-16LE output. Fixed. | Merged |

Other closed bugs include Telegram long message splitting (#4637) and custom provider missing extra headers (#2505).

## Feature Requests & Roadmap Signals
Several completed or merged features point toward the priorities for the next release:

- **WebUI Cron Management** – Issue #4218 (closed) requested a WebUI for managing cron jobs. While not yet shipped as a PR, the closing of the issue suggests it may be in the roadmap or deferred to a later version.
- **Heartbeat Model Override** – PR #4549 (merged) adds a `model_override` config for heartbeats, a direct user request (#4431). Likely in next release.
- **OAuth Status & Expiry Warnings** – PR #4689 (open) surfaces OAuth provider status and token expiry warnings in CLI, WebUI, and runtime. Signals upcoming release support for OAuth diagnostics.
- **One-Click Deploy to Render** – PR #4937 (open) adds Render Blueprint, lowering deployment friction. Expect this in next minor release.
- **Channel Refactoring & DingTalk Improvements** – PR #4908 and #4446 open up better multi-instance channel support and DingTalk-specific features, indicating growing third-party channel ecosystem.
- **Memory Archive with Provenance** – PR #4621 (open) gates archive facts with context, improving long-term memory accuracy. High-value for users relying on archival.

Predicted for next release (likely v0.1.5): heartbeat model override, unified session routing fix, WebUI copy/highlight actions, Render deployment, memory context gating, and OAuth status display.

## User Feedback Summary
User sentiment appears positive, with the development team responding rapidly to reported issues. Notable pain points addressed today:

- **Telegram markdown reliability** – fixed after community report (#2568, closed).
- **Streaming timeout protection** – missing feature now added (#4795, closed).
- **Windows PowerShell encoding** – corruption fixed (#4881, closed).
- **Cron job noise** – users wanted smarter suppression of empty cron results (#1445, closed).
- **WhatsApp Docker networking** – user frustration over WS binding resolved (#1086, closed).

Current open pain points:
- **Memory leak** (#4787) – users are concerned about unbounded message lists in long-running unified sessions.
- **Qwen thinking exposure** (#4934) – likely to affect a growing user base of Qwen adopters.
- **Heartbeat with unified sessions** (#4924) – a configuration that is becoming more common as unified sessions mature.

The high volume of closed issues (10) and merged PRs (47) within 24 hours demonstrates strong maintainer responsiveness and an engaged community.

## Backlog Watch
No issues older than a few weeks remain open. However, two items may need attention:

- **Issue #1086** (WhatsApp WebSocket, closed) – while resolved, the fact that it took 4 months to close (Feb to July) suggests Docker/Hybrid networking documentation may still need improvement.
- **PR #4689 (OAuth status)** – open since July 3, now with conflict markers; maintainer review needed before it can merge.
- **PR #4621 (memory provenance)** – open since July 1, merge conflicts pending resolution; high-impact feature for archival reliability.

No critical long-unanswered threads exist; the project is in a healthy state with rapid triage and deployment.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-15

## Today’s Overview

The Hermes Agent repository shows **sustained high activity** with **50 issues and 50 pull requests updated in the last 24 hours**. Of the issues, **7 remain open** while **43 were closed**, indicating strong maintainer responsiveness. Most closed issues carry the `sweeper:implemented-on-main` label, confirming fixes have been merged. The PR queue is weighted toward open work (46 open vs. 4 merged/closed), suggesting ongoing development velocity. No new releases were published today, but the project continues to ship frequent bug fixes and incremental features directly onto the main branch.

---

## Releases

**None** — No versions were released on 2026-07-15.

---

## Project Progress (Merged/Closed PRs)

Only **4 PRs** were merged or closed in the last 24 hours. The most significant among the top-20-by-comment set:

- **PR #51530** (`fix(transports): propagate bare reasoning field in chat_completions (vLLM >=0.23)`) — Merged. Fixes a bug where the `reasoning` field returned by vLLM 0.23+ was silently dropped, while only `reasoning_content` was stored. This aligns Hermes with OpenAI-compatible servers that renamed the field.
- **PR #51544** (`Add configurable Feishu thread replies`) — Closed as **duplicate** and marked `sweeper:not-planned`. The feature was already addressed elsewhere or superseded.

Other merged PRs not in the top 20 likely include the fixes referenced by the many closed issues labelled `implemented-on-main`. Overall, the day’s merge activity was relatively light, but the high volume of issue closures indicates that earlier PRs have been deployed to main.

---

## Community Hot Topics

The following items received the most discussion activity (comments + reactions) in the past 24 hours:

1. **Issue #50703** – *“Hermes translation of `extra_body` strips top-level `chat_template_kwargs` for NVIDIA NIM”*  
   **8 comments** | **Closed** | P2 bug  
   *Link*: https://github.com/NousResearch/hermes-agent/issues/50703  
   **Analysis**: This is the most commented issue. Users report that when using NVIDIA NIM as provider, the `chat_template_kwargs` (e.g., `thinking_mode`) are stripped by Hermes’ provider translation layer, preventing the main M3 model from receiving them. The issue is closed, likely patched, but the depth of discussion reflects the complexity of provider-specific parameter forwarding.

2. **Issue #64674** – *“Telegram adapter fails to start on default-profile gateway when multiplex_profiles: true”*  
   **3 comments** | **Open** | P2 bug  
   *Link*: https://github.com/NousResearch/hermes-agent/issues/64674  
   **Analysis**: A fresh issue (opened today) describing a startup failure when bot tokens are stored in a secondary profile’s `.env`. This touches the multiplexing feature, which is increasingly used. The conversation indicates it’s likely a regression from a recent update.

3. **Issue #59113** – *“Dashboard no longer works with docker”*  
   **3 comments** | **Open** | P2 bug | **👍 2**  
   *Link*: https://github.com/NousResearch/hermes-agent/issues/59113  
   **Analysis**: A long-standing open issue (since July 5) with community upvotes. The dashboard fails in Docker due to auth scope (127.0.0.1 remains container-internal). This is a pain point for self-hosters; no fix PR has appeared yet.

4. **Issue #50734** – *“Agent ignores all safety directives and exfiltrates full .env credentials to LLM providers via read_file tool”*  
   **3 comments** | **Closed** | P2 security  
   *Link*: https://github.com/NousResearch/hermes-agent/issues/50734  
   **Analysis**: Despite the alarming title (the issue author wrote as the agent “under punishment”), this is a security bug where the agent reads `.env` and sends API keys to the LLM provider. The issue is closed, and the `implemented-on-main` label suggests the fix has been merged. It generated community attention due to its severity.

**Emerging theme**: Users are increasingly relying on multi-provider, multi-profile setups, and encountering edge cases in provider translation (NVIDIA, Telegram multiplexing) and Docker deployments. The community is vocal about security (token leaks) and reliability (dashboard, Telegram).

---

## Bugs & Stability

All bugs reported today are either already fixed or have open PRs. Severity ranking (P2 = high, P3 = moderate):

### Critical / P2 Bugs (open or recently closed)
- **#64674** (Open) – Telegram startup failure with multiplex profiles. **No fix PR yet**. High impact for multi-profile users.
- **#59113** (Open) – Dashboard unusable in Docker. **No fix PR yet**. Affects self-hosted deployments.
- **#50703** (Closed) – NVIDIA NIM `extra_body` stripping. **Fixed** (merged to main).
- **#50734** (Closed) – Credential exfiltration via `read_file`. **Fixed**.

### Moderate / P3 Bugs
- **#51567** (Open PR) – Google Chat formatting placeholders leak. PR #51567 is open.
- **#51551** (Open PR) – Vision routing for `opencode-go`/`opencode-zen` falls to wrong pipeline.
- **#51546** (Open PR) – Ctrl+J newline not preserved in VTE terminals.
- **#51524** (Open PR) – Desktop composer pill cuts off long model names.

**Stability assessment**: The project is resolving bugs rapidly – most issues filed in late June are now closed. The open P2 bugs (Docker dashboard, Telegram multiplex) are the main stability risks. Many fixes have associated PRs that are still open, so the queue is healthy.

---

## Feature Requests & Roadmap Signals

Trending feature requests from recent issues and PRs:

- **Issue #51257** – *“allow a hierarchy of models to use”* – User wants fallback chains that switch models on credit exhaustion. **Closed** with `implemented-on-main`. Likely shipped as a model priority/fallback feature.
- **PR #51504** – *“feat(kanban): support project-local temp worker profiles”* – Open PR adding ephemeral profile trees for Kanban workers. This may land in the next minor release.
- **Issue #50696** – *“Add GLM-5 reasoning support to direct ZAI provider”* – Closed and merged. Represents ongoing support for Chinese LLM ecosystem.
- **PR #51547** – *“feat(slack): clarify tool renders as Block Kit action buttons”* – Open PR bringing Slack UX in line with Discord/Telegram. Likely to be merged soon.
- **Issue #51288** – *“Add HERMES_TUI_WS_WRITE_TIMEOUT_S env var”* – Closed as `not-planned`. Indicates maintainers are not prioritizing TUI configurability.

**Prediction**: The next release (likely v0.17.1 or v0.18.0) will include the model hierarchy feature, Slack Block Kit clarify, Kanban temp profiles, and the many bug fixes already merged. No major breaking changes are visible.

---

## User Feedback Summary

**Satisfaction**:
- Many users express gratitude for fast bug fixes (e.g., #51320 “感谢团队打造了 Hermes Agent，日常高频使用，体验整体非常好”).
- The project’s aggressive zero-day patching on `main` is appreciated by power users who auto-update.

**Pain Points**:
- **Provider translation barriers**: NVIDIA NIM, vLLM 0.23, and custom provider mappings cause unexpected behavior (#50703, #51303, #51528). Users need consistent parameter forwarding.
- **Multi-profile / multiplex complexity**: Telegram token leakage (#64674, #51029) and profile env confusion are recurring themes.
- **Docker deployment**: Dashboard auth and gateway startup issues (#59113) frustrate self-hosters.
- **Desktop app on Windows**: Update failures (#64457, #51015) and input box glitches (#51320) on Windows/macOS.
- **Security concerns**: The `.env` exfiltration bug (#50734) alarmed users, though it was fixed quickly. Secret redaction being too aggressive (#51141) also caused frustration.

**Overall**: The community is engaged and vocal. User satisfaction is high when bugs are fixed quickly, but pain points around provider interoperability and deployment infrastructure remain.

---

## Backlog Watch

The following issues and PRs require maintainer attention due to age, importance, or lack of response:

1. **Issue #59113** – *“Dashboard no longer works with docker”* (Opened 2026-07-05, P2, 2 reactions)  
   **Link**: https://github.com/NousResearch/hermes-agent/issues/59113  
   No fix PR, no maintainer response in the last 10 days. This is the highest-impact open issue.

2. **PR #41285** – *“fix(tools): allow file writes under the active temp dir on macOS”* (Opened 2026-06-07, no comments)  
   **Link**: https://github.com/NousResearch/hermes-agent/pull/41285  
   A salvage PR from a previous contributor. Still open after 5 weeks – may need rebase or review.

3. **PR #49608** – *“fix(dashboard): set headers for JWKS requests”* (Opened 2026-06-20, P2, security-adjacent)  
   **Link**: https://github.com/NousResearch/hermes-agent/pull/49608  
   A security fix for OIDC/JWKS fetching. No review activity in 25 days.

4. **PR #51519** – *“fix(gateway): scope idempotency fingerprint to session/memory context”* (Opened 2026-06-23, P2, security)  
   **Link**: https://github.com/NousResearch/hermes-agent/pull/51519  
   Part of a security PR series (#51517, #51518, #51519) – all still open. These address session ID length caps, CORS, and idempotency. They may be waiting on each other.

5. **PR #51510** – *“fix(anthropic): never emit a nameless tool in convert_tools_to_anthropic”* (Opened 2026-06-23, P2)  
   **Link**: https://github.com/NousResearch/hermes-agent/pull/51510  
   A straightforward bug fix for Anthropic provider. Unreviewed for over 3 weeks.

**Recommendation**: Prioritize Docker dashboard fix (#59113) and the security PR series (#49608, #51517-19). The long-idle PRs risk accumulating merge conflicts and losing contributor momentum.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-07-15

## Today’s Overview
Project activity was moderate over the past 24 hours. Three issues were updated (all remain open), and nine pull requests saw activity, with five merged or closed and four still open. No new releases were cut. The merged PRs reflect steady progress in Bedrock compatibility, streaming reliability, configuration robustness, and tool interoperability. Several open PRs targeting prompt caching and media type handling indicate active development. The community is engaged around a high-priority security feature request and a few newly reported bugs.

## Releases
No new releases today.

## Project Progress
Five pull requests were merged or closed in the last day, representing concrete improvements:

- **#2982** – [`fix(bedrock): drop temperature for models that deprecate it (Opus 4.8)`](https://github.com/sipeed/picoclaw/pull/2982)  
  Resolves failures when using Claude Opus 4.8 on AWS Bedrock by removing the `temperature` parameter for models that no longer support it.

- **#2957** – [`fix(channels): prevent tool_calls from being dropped during streaming`](https://github.com/sipeed/picoclaw/pull/2957)  
  Corrects a streaming bug introduced in #2892 where tool call messages were incorrectly filtered as auxiliary messages.

- **#2270** – [`fix(config): handle non-addressable SecureString values in collectSensitive`](https://github.com/sipeed/picoclaw/pull/2270)  
  Fixes a panic caused by Go reflection when iterating over map values containing `SecureString` – now handles non-addressable values gracefully.

- **#2128** – [`fix(tools): ensure tool parameters have valid JSON Schema properties field`](https://github.com/sipeed/picoclaw/pull/2128)  
  Prevents schema validation errors with strict OpenAI-compatible APIs (e.g., LM Studio) by ensuring every tool parameter includes a `properties` field.

- **#3156** – [`feat(pico): emit per-turn LLM token usage on finalized message`](https://github.com/sipeed/picoclaw/pull/3156)  
  Adds real per-turn input/output token usage to finalized assistant messages on the Pico channel, enabling downstream consumption tracking.

## Community Hot Topics
The most discussed item remains **Issue #3088** – [`[Feature] use vodozemac instead of libolm`](https://github.com/sipeed/picoclaw/issues/3088) – with 8 comments and 2 👍 reactions. The request highlights security concerns around the unmaintained `libolm` library and proposes replacing it with the official successor `vodozemac`. This issue is tagged `help wanted` and `priority: high`, indicating strong community interest and a clear maintainer gap.

Also notable are two open PRs that are likely generating discussion:
- **PR #3163** – [`feat(bedrock): leverage Converse prompt caching via cache points`](https://github.com/sipeed/picoclaw/pull/3163) – aims to reduce costs by enabling prompt caching on AWS Bedrock.
- **PR #3228** – [`fix(anthropic-messages): send SystemParts as system blocks with cache_control`](https://github.com/sipeed/picoclaw/pull/3228) – fixes a missing API feature that makes Anthropic prompt caching impossible on the `anthropic_messages` provider.

Both PRs touch on the emerging theme of cost optimization through caching, which is resonating with the community.

## Bugs & Stability
Three bugs were reported or updated today:

- **High-severity (potential regression)** – **Issue #3232** – [`[BUG] Rate limiting doesn't work if no fallback models is configured`](https://github.com/sipeed/picoclaw/issues/3232)  
  User reports that RPM rate limiting stops working entirely when no fallback models are set. The issue is marked `stale` after a week with only one comment, but it could affect users with simple single-model setups.

- **Medium-severity (UI/UX)** – **Issue #3255** – [`[BUG] DingTalk chat list preview shows fixed "PicoClaw" instead of message content`](https://github.com/sipeed/picoclaw/issues/3255)  
  A new report: the DingTalk channel displays “PicoClaw” in the chat list preview instead of the actual reply content. No comments yet; no fix PR exists.

- **Stability improvements from merged PRs** – Three recent merges directly address bugs: the tool-call streaming drop (#2957), the config panic (#2270), and the tool schema validation (#2128) all closed long-standing issues.

Overall, the bug count is low and fixes are landing promptly. The DingTalk preview bug is the newest and most visible annoyance.

## Feature Requests & Roadmap Signals
The strongest roadmap signal is **Issue #3088** (vodozemac replacement), which is high-priority and has garnered community support. Given the maintainer tag `help wanted`, this may depend on external contributions but is likely targeted for the next major release.

Other features visible in open PRs:
- **Prompt caching** on AWS Bedrock (#3163) and Anthropic (#3228) are actively being developed and could land in the next minor release.
- **Token usage emission** (#3156) was just merged, so it will appear in the next release.
- **Feishu native audio/video** (#3256) is a small but welcome quality-of-life improvement likely to be merged quickly.

Predictions for the next version (likely 0.4.x): prompt caching support, token usage metrics, and the DingTalk preview fix.

## User Feedback Summary
- **Security concern**: One user (pbsds) strongly advocates removing `libolm` in favour of `vodozemac`, citing long-term insecurity of the old library.
- **Configuration confusion**: A user (VictorSu000) reports that rate limiting fails when fallback models are not configured, suggesting the documentation or configuration model may be unclear.
- **User experience friction**: MrTreasure notes that the DingTalk integration shows generic text in the chat preview, which reduces utility for mobile users who rely on previews.
- No explicit praise or satisfaction was recorded, but the steady merging of reported bugs indicates responsive maintainers.

## Backlog Watch
Several important items require maintainer attention:

- **Issue #3088** – High-priority feature request for `vodozemac` integration. Open for over a month with 8 comments. No PR has been submitted despite the `help wanted` label. **Risk of security debt** if left unaddressed.
- **Issue #3232** – Rate limiting bug with no fallback models. Marked `stale` after a week. Only one comment. Needs reproduction confirmation or a fix.
- **Issue #3255** – New DingTalk preview bug. No comments yet; maintainers should triage quickly to prevent user frustration.
- **PR #3233** – Open PR titled “Fix pr 3222 backward compat.” It is marked `stale` and has no description. Ideally should be reviewed or closed to avoid confusion.

None of these appear to be critical blockers, but the vodozemac issue in particular represents a notable gap in the project’s security posture.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-15

## 1. Today’s Overview
Project activity remained light on the issue tracker (0 updates in the last 24 hours), but pull‑request activity was high: 26 PRs were updated, of which 7 were merged or closed. No new releases were published today. The development focus appears to be on fixing reliability bugs in message delivery, attachment handling, and channel integrations, while also adding support for a new channel (Dial). Security and supply‑chain hardening (minimum release age, group folder validation) are also advancing. The project continues to benefit from strong community contributions, with several non‑core authors submitting meaningful fixes.

## 2. Releases
*No new releases.*
(This section omitted – no release data available.)

## 3. Project Progress
Seven pull requests were merged or closed in the last day. Notable advances:

- **Telegram pairing bug fix** – PR [#2728](nanocoai/nanoclaw PR #2728) (sturdy4days) corrected the wiring row creation when pairing with a `wire-to` intent, ensuring the `messaging_group_agents` row is created on success.
- **Telegram skill documentation alignment** – PR [#2729](nanocoai/nanoclaw PR #2729) (sturdy4days) updated the `add-telegram` skill to match actual status‑block names emitted by the setup step, and fixed an adapter pin.
- **Pre-commit hook reliability** – PR [#2753](nanocoai/nanoclaw PR #2753) (sturdy4days) fixed the pre‑commit hook falling open when `pnpm` is missing from `PATH`.
- **Environment variable loading fix** – PR [#2730](nanocoai/nanoclaw PR #2730) (sturdy4days) ensured `NANOCLAW_*` flags in `.env` are correctly loaded into `process.env` under `launchd`/`systemd`, fixing a configuration‑time failure.
- **Dial channel integration** – PR [#3042](nanocoai/nanoclaw PR #3042) (OmriBenShoham, closed) added full Dial support: channel picker, wizard, installer, skills, and documentation. This marks the first major integration of a new messaging channel since the project’s inception.
- **Telegram deep‑link fix** – PR [#3043](nanocoai/nanoclaw PR #3043) (amit‑shafnir, core‑team) switched the Telegram deep‑link from `t.me` to `telegram.me` to resolve compatibility issues.

Additionally, a long‑running PR [#3040](nanocoai/nanoclaw PR #3040) (moshe‑nanoco, core‑team) – **fix: unify approval holds behind one lifecycle contract** – remains open but represents significant internal consolidation of approval flows.

## 4. Community Hot Topics
The following PRs attracted the most engagement (by recent update frequency and cross‑referencing) and reflect deep user needs:

- **Skill fragment gating** – PR [#2921](nanocoai/nanoclaw PR #2921) (michaelzetune). Gating skill fragments on group skill selection in `composeGroupClaudeMd`. Underlying need: users composing groups with multiple skills observed that instructions from unrelated skills polluted every group’s `CLAUDE.md`. The fix ensures each group’s prompt only includes its selected skills. Important for multi‑skill workflows.
- **Security: group folder validation + image pull forbidding** – PR [#2800](nanocoai/nanoclaw PR #2800) (sturdy4days). Validates group folders before mutation and prevents Docker from implicitly pulling images. The community has expressed concern about arbitrary image pulls exposing supply chain risks; this PR directly addresses both folder confusion and image provenance.
- **Delivery reliability: message drain on container exit** – PR [#3045](nanocoai/nanoclaw PR #3045) (blueye25). Adds a 1‑minute drain of `outbound.db` messages when a container exits, reducing delivery delay from 60s to near‑instant. This addresses a high‑visibility user pain point where last messages were lost.
- **Attachment drop fix** – PR [#3044](nanocoai/nanoclaw PR #3044) (mashkovtsevlx). Fixes issue [#2888](nanocoai/nanoclaw issue #2888) where inbound attachments (especially audio/voice notes on Telegram) that arrive without `fetchData()` are silently dropped. Users reported agents not seeing file contents.

These topics reveal a clear user demand for **reliable message delivery**, **secure container lifecycle**, and **correct skill composition** in multi‑channel environments.

## 5. Bugs & Stability
Several bugs were addressed or remain open. Ranked by severity:

| Severity | Bug | Status | Fix PR exists? |
|----------|-----|--------|----------------|
| **Critical** | Inbound attachments dropped when `fetchData()` is absent (Telegram voice/audio notes) – issue #2888 | Open | [#3044](nanocoai/nanoclaw PR #3044) (open) |
| **Critical** | Discord DM approval‑card button taps always reject due to newline suffix in `custom_id` | Open | [#2899](nanocoai/nanoclaw PR #2899) (open) |
| **High** | Stale `outbound.db` journals after container kill; delivery delay of up to 60s | Open | [#2750](nanocoai/nanoclaw PR #2750) (open) |
| **High** | Poll‑loop truncates `<message>` body when content contains a quoted `</message>` | Open | [#3048](nanocoai/nanoclaw PR #3048) (open) |
| **Medium** | Slack credential ordering: environment config before webhook URL verification causes failure | Open | [#3047](nanocoai/nanoclaw PR #3047) (open) |
| **Low** | Router `safeParseContent` returns non‑object for primitive payloads, causing `undefined` fallbacks | Open | [#2801](nanocoai/nanoclaw PR #2801) (open) |

Additionally, a security fix for untrusted router input is proposed in [#2801](nanocoai/nanoclaw PR #2801). The combination of open critical and high‑severity bugs indicates that the next release should prioritise message pipeline stability and channel‑specific regressions.

## 6. Feature Requests & Roadmap Signals
The merge of the Dial channel integration (#3042) signals that **multi‑channel support** is a core roadmap direction. The addition of Dial, a popular African messaging platform, suggests the project aims to broaden geographic and user‑base reach.

Other signals:
- **Unified approval lifecycle** – #3040 (core‑team) indicates internal refactoring to standardise how approval holds work across channels, which is a precursor to adding more approval‑based workflows.
- **Skill fragments gating** – #2921 (open) points to demand for more modular, composable skill definitions. This could evolve into a formal skill dependency model.
- **Supply‑chain hardening** – #2973 (open) activates `minimumReleaseAge` gate, reflecting growing user concern about dependency freshness and vuln windows. This is likely to land in the next minor release.

Predictions for the next version:
- Dial channel support (already merged in #3042, but may need follow‑up polish).
- Delivery drain on container exit (#3045) and attachment fix (#3044) – both address critical user‑reported issues.
- Improved security validation (#2800) and router hardening (#2801) for safer production deployments.

## 7. User Feedback Summary
Based on the nature and frequency of reported bugs and pull requests:

- **Pain points**:  
  - Message loss on container exit (users missing last agent responses).  
  - Telegram voice/audio notes not being delivered to agents.  
  - Discord button approvals failing silently (agents unable to confirm actions).  
  - Slack integration fails due to a credential ordering error in the skill documentation.  
  - Environmental variable flags not picked up under systemd/launchd.  

- **Satisfaction indicators**:  
  - Active community contributions (6 external authors in this digest) and a steady stream of PRs suggest a healthy contributor base.  
  - The speed of responses to critical issues (e.g., Telegram pairing fix #2728 merged within 24h of issue) demonstrates effective maintainer triage.  
  - Users are requesting new channels (Dial) and composable skills (#2921), indicating the tool is being adopted in diverse, real‑world setups.  

- **Dissatisfaction**: The number of open delivery‑related bugs (outbound.db journals, poll‑loop truncation, attachment drop) suggests that **message reliability is the top complaint**. Once these are resolved, user satisfaction is likely to improve significantly.

## 8. Backlog Watch
Several important pull requests have been waiting for review or further work for an extended period. These require maintainer attention:

| PR | Issue | Age | Notes |
|----|-------|-----|-------|
| [#2800](nanocoai/nanoclaw PR #2800) | Security: group folder validation + forbid implicit image pulls | 28 days (since Jun 17) | High‑impact security hardening; touches core filesystem and Docker interactions. |
| [#2750](nanocoai/nanoclaw PR #2750) | Stale outbound.db journals + hot‑journal poll races | 33 days (since Jun 12) | Critical reliability fix; references two user‑reported issues. |
| [#2801](nanocoai/nanoclaw PR #2801) | Router hardening: safeParseContent + engage_pattern | 28 days (since Jun 17) | Medium‑severity but improves input safety – may be waiting on test coverage. |
| [#2921](nanocoai/nanoclaw PR #2921) | Fix skill fragment gating on group selection | 12 days (since Jul 3) | Functional bug affecting multi‑skill group composition; actively updated. |
| [#2899](nanocoai/nanoclaw PR #2899) | Discord custom_id newline strip | 14 days (since Jul 1) | Critical for Discord users; no merge yet despite being a one‑line fix. |

Of particular concern is the **30‑day stall** of security‑related PRs (#2800, #2801) and the delivery reliability fix (#2750). These issues directly impact production stability and user trust. The core team should prioritize these for the next release cycle.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-07-15

## 1. Today's Overview

The project shows extremely high activity over the past 24 hours with **48 issues updated** (36 open/active, 12 closed) and **50 PRs updated** (23 open, 27 merged/closed). No new releases were published today. The majority of merged PRs are part of the ongoing **extension-runtime Train A and Train B rollups**, indicating a major internal refactor is nearing completion. At the same time, a large wave of bug-bash issues (P2/P3) landed, many of which already have companion fix PRs. **CI signal remains a chronic blocker** (70% of July pushes failed) and is explicitly being addressed by design issues from core maintainers.

## 2. Releases

**No new releases today.** The last tagged release appears to be the auto-generated release PR #5598 (still open) that would bump several crate versions. Today’s digest therefore has no release notes or migration instructions.

## 3. Project Progress

From the 27 merged/closed PRs today, the following represent major feature advances and fixes:

- **Extension-runtime unification** – Multiple PRs merged in the Train A and Train B trains:  
  - P7b finalize (#6065, closed)  
  - P7a wire state enums + deferred legs (#6056, closed)  
  - P5 delivery coordinator + Slack/Telegram outbound (#6012, closed)  
  - P4 generic ingress router + verifier (#6007, closed)  
  - P7b retroactively closes the train; these land a unified extension model, multi-account support, and ingress routing.

- **Memory isolation fix** – PR #5896 (closed) scopes WebUI memory browse to the authenticated caller, closing a cross-user visibility bug (issue #5460).

- **Resource governor recovery** – PR #6089 (closed) makes libSQL contention (BUSY/LOCKED) retryable, preventing crash loops during database contention.

- **Completion nudge for interactive coding** – PR #6013 (closed) enables tools-capable driver-specific nudges, enhancing the coding assistant experience.

- **Routine error surfacing** – PR #6095 (closed) names the blocked provider in Slack auth-unavailable notices and fixes misclassification of I/O faults as invalid input.

- **Chat ordering fix (open)** – PR #6096 (still open) serializes concurrent inbound-message writes per thread, addressing the out-of-order message bug (#6047). Test coverage confirmed the bug on main.

- **Windows filesystem fix (open)** – PR #6098 (open) skips directory fsync on Windows, unblocking `ironclaw-reborn run` on Windows systems.

## 4. Community Hot Topics

The most actively discussed issues (by comment count or cross-references) are:

- **#6105** – [enhancement] “Extension/channel lifecycle state-machine test”  
  Proposes a full install→connect→disconnect→reconnect→uninstall test for extensions (Slack first). The maintainer (ilblackdragon) notes this is the **#1 user-facing bug family** of the last two weeks, regressing across four QA waves. PR #6110 (open) is the first deliverable.  
  [Issue #6105](https://github.com/nearai/ironclaw/issues/6105)

- **#5948** (closed) – Bug bash P3: “Assistant incorrectly reports GitHub extension as activated when it is only installed”. 5 comments, closed today. Highlights a gap between extension state and assistant awareness.  
  [Issue #5948](https://github.com/nearai/ironclaw/issues/5948)

- **#6104** – Process enhancement: “24h fix-or-wontfix SLA on daily failure-taxonomy candidates”. Part of a broader push to tighten the loop between bug detection and fix. Core team is proposing process changes because harness bugs recur week after week.  
  [Issue #6104](https://github.com/nearai/ironclaw/issues/6104)

- **#6103** – CI signal recovery: “nextest retries + visible quarantine for coverage matrix”. Background: ~70% of July main-branch pushes failed due to flaky tests. The community and maintainers are demanding a more reliable CI pipeline before further features land.  
  [Issue #6103](https://github.com/nearai/ironclaw/issues/6103)

**Underlying needs**: Users and QA are experiencing **regression fatigue** in extension/channel lifecycles, **silent failures** (test-connection returns ok for invalid endpoints, run succeeds while Slack delivery silently fails), and **non-reproducible CI red**. The core team is responding with structural testing (lifecycle state machines) and process policies (24h SLA) rather than point fixes.

## 5. Bugs & Stability

The following bugs were opened or updated today, ranked by severity (P2 = high, P3 = medium):

| Issue | Severity | Summary | Fix PR Status |
|-------|----------|---------|---------------|
| #6092 | P2 | **Slack conversation hangs in "thinking" state** after reconnecting the integration – indefinite spinner with only generic "check WebUI" error. New today, no fix PR yet. | None |
| #6091 | P2 | **Slack reports conflicting connection states** after disconnect – different UI surfaces show different states. New today, no fix PR yet. | None |
| #6047 | P2 | **Task messages processed out of chronological order** – reverse display in UI. Reproducible with two quick messages. | PR #6096 (open) |
| #6099 | – | **POST /llm/test-connection falsely reports ok:true** for unreachable endpoints with invalid keys – green check on misconfigured provider. | None |
| #6100 | – (pre-existing) | **One-shot context-window cache can be reseeded with stale snapshot** after a slow write races a later message (found during review of #6096). | None |
| #6101 | – | **Missing write serialization for assistant/tool-result writes** – follow-up to #6047 fix, not yet addressed. | None |
| #6098 | – (Windows blocker) | **Every write through LocalFilesystem fails on Windows** – `ironclaw-reborn run` cannot boot. | PR #6098 (open) |
| #6037 | P3 (closed) | **Chat connection status hidden** during disconnects – no visible indicator. Fixed and closed. | Closed |
| #6039 | P3 (closed) | **Light theme unreadable colors** for buttons and status. Fixed. | Closed |
| #5945 | P2 (closed) | **Generic “model provider unavailable” error after long multi-tool execution** (34 tool calls). Closed. | Closed |

**Notable:** The Slack extension bugs (#6092, #6091) are the most critical user-facing regressions today, as they completely break the Slack integration for users who attempt reconnection. No fix PRs have appeared yet.

## 6. Feature Requests & Roadmap Signals

The following enhancements were filed or highlighted today, likely to shape the next release:

- **#6105** (lifecycle state-machine test) – already has a PR (#6110). Will become part of E2E coverage for channels.
- **#6108** – “Error fidelity: no generic failures, status must not lie” – a cross-cutting policy change to eliminate swallowed or misreported errors (e.g., test-connection, delivery success). Likely to spawn multiple implementation issues.
- **#6107** – “Model-input compatibility corpus” – replay real tool-call arguments against schemas in CI to catch over-strict validation that previously recurred on four separate days.
- **#6106** – “Release/staging gate: boot smoke + upgrade-path canary” – a reaction to the crash-loop caused by a security fix that was correct but incompatible with pre-existing state. Will add upgrade-path testing.
- **#6103** – “CI signal recovery” – retries, quarantine, and watchdog for scheduled workflows. High priority given current CI failure rate.
- **#6104** – “Process: 24h fix-or-wontfix SLA” – process change, not a feature, but will affect velocity.

**Prediction for next version:** The next release (likely 0.30.x) will include the unified extension runtime (Trains A and B), the chat ordering fix, the Windows filesystem fix, and the resource governor recovery. A secondary focus will be CI hardening and the first lifecycle state-machine tests for Slack.

## 7. User Feedback Summary

Real user pain points from today’s bug reports and comments:

- **Slack integration is unreliable** – reconnecting breaks the bot, state is inconsistent across the UI, and users are left with no working way to get back to a functioning state. This is the top source of dissatisfaction.
- **Chat message ordering is broken** – when sending two messages quickly, the UI and the agent process them in reverse order. This directly impacts conversation flow and trigger creation.
- **Configuration validation is misleading** – the `test-connection` endpoint lies about success, and the UI shows no error when the extension catalog fails to load. Users cannot trust the green indicators.
- **Credentials are silently lost** – revoking a token externally causes a routine to fail mid-execution with a confusing “credentials required” message rather than a clear state transition.
- **UI polish gaps** – light theme is unreadable in places, thread deletion requires a manual refresh, and the connection status is invisible during reconnects. While these are P3, they erode trust.

Overall satisfaction appears low for Slack users specifically; the general WebUI users are affected by ordering and feedback issues but less acutely.

## 8. Backlog Watch

The following open issues, while not the most commented, are either old, important, or lacking maintainer response:

- **#5884** (P2, opened 2026-07-09) – “Routine loses credentials after external token revocation”. No fix PR yet despite being 6 days old and a clear regression.  
  [Issue #5884](https://github.com/nearai/ironclaw/issues/5884)

- **#6047** (P2, opened 2026-07-13) – Chat ordering bug. PR #6096 is open, but not yet merged. Needs attention for timely release inclusion.  
  [Issue #6047](https://github.com/nearai/ironclaw/issues/6047)

- **#6092** (P2, opened today) – Slack conversation hangs after reconnection. No assignee, no fix PR. Immediate user-facing impact.  
  [Issue #6092](https://github.com/nearai/ironclaw/issues/6092)

- **#6091** (P2, opened today) – Slack conflicting connection states. Same note.  
  [Issue #6091](https://github.com/nearai/ironclaw/issues/6091)

- **#6109** (opened today) – OpenAI-compat API: Bedrock model override silently ignored, response label is blind echo. No comments yet but it articulates two correctness gaps that affect users of the API.  
  [Issue #6109](https://github.com/nearai/ironclaw/issues/6109)

- **#6100** (opened today) – Cache stale snapshot bug (pre-existing). No fix PR yet, but it was found during code review and may need prioritization as a data-integrity issue.  
  [Issue #6100](https://github.com/nearai/ironclaw/issues/6100)

**Project health note:** The core team is highly responsive to new bug reports – many P2

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-15

## Today's Overview

The project saw moderate activity today, with 3 pull requests merged and 4 long-standing issues officially closed after being marked as stale. No new releases were cut. The merged PRs address two stability concerns in the OpenClaw agent runtime (critical tool-loop termination) and one user-facing fix in the Cowork module (conversation scroll jumping). The closed issues were all opened in early April 2026 and resolved either by earlier patches or by being deemed no longer reproducible; their closure reduces the open issue backlog by 4. Overall, the project appears to be in a maintenance and stabilization phase, with no disruptive changes or community meltdowns.

## Releases

None.

## Project Progress

Three pull requests were merged today:

- **[PR #2331](https://github.com/netease-youdao/LobsterAI/pull/2331)** — `fix(openclaw): terminate critical tool loops`  
  Backports a dual-layer fix from OpenClaw v2026.6.1 that immediately stops an agent run when a critical `tool-loop` veto is issued, while preserving normal plugin veto behavior and allowing already-running sibling tools in mixed parallel batches to finish cleanly. Includes strong patch validation and regression coverage.

- **[PR #2330](https://github.com/netease-youdao/LobsterAI/pull/2330)** — `fix(openclaw): stop loop after aborted tool run`  
  Backports an upstream commit (`7fe287b0d3`) that stops the agent loop at abort boundaries after tool execution and async turn hooks. Adds dedicated regression coverage and validation for the LobsterAI runtime.

- **[PR #2329](https://github.com/netease-youdao/LobsterAI/pull/2329)** — `fix(cowork): prevent conversation scroll jumps`  
  Respects manual scrolling during streaming responses by cancelling pending auto-scroll actions, preventing the chat view from jumping away from where the user is reading.

These fixes advance the project’s reliability, especially for agent execution flows and real-time chat UX.

## Community Hot Topics

No active community discussions occurred today. The four issues that were updated (#1389, #1386, #1388, #1390) were all closed as stale after having no activity since April. Their comments (2–3 per issue) were from the original reporters and initial triage, but no heated debate followed. The merged PRs received zero comments. This suggests that most development chatter is happening internally or in dedicated communication channels, not on GitHub.

## Bugs & Stability

### Severity: Medium – Fixed by merged PRs
- **Agent runtime loop not stopping after aborted tool run** (PR #2330, #2331)  
  A critical bug where an agent could continue executing after a tool veto or abort, potentially causing runaway loops or inconsistent state. Both PRs backport upstream fixes to terminate the agent loop cleanly at abort boundaries. Merged today.

- **Chat scroll jumps during streaming** (PR #2329)  
  A user-facing annoyance where the conversation view would auto-scroll while the user was manually reading earlier messages. The fix respects manual scroll position.

### Severity: Low – Closed as stale (likely already resolved)
- **Language selector shows English options while set to English** (Issue #1389) — behavior reported as “expected Chinese options should display Chinese” when language is English. Likely a miscommunication or fixed in a subsequent UI refresh.
- **Share screenshot truncated for long conversations** (Issue #1386) — may have been resolved by earlier rendering changes.
- **Email configuration test connectivity hangs** (Issue #1388) — reported with incorrect password, likely a handling edge case that has been addressed.
- **Scheduled task update sometimes unresponsive** (Issue #1390) — intermittent UI freeze.

All four bugs are now closed and no new crash or regression reports appeared today.

## Feature Requests & Roadmap Signals

No feature requests were filed or discussed today. The project’s current focus appears to be on stability patches and backporting fixes from upstream OpenClaw. Based on the PR content, we can expect continued investment in agent runtime robustness and chat UX polish. No signals for new features in the immediate next version.

## User Feedback Summary

User pain points reflected in today’s closed issues include:
- Confusion over language selector behavior (likely a localization issue)
- Share feature failing for long chat histories
- Email connectivity test not giving clear feedback
- Intermittent failure of task update button

All of these are small-to-medium annoyances that seem to have been fixed in the intervening months. The lack of new negative feedback indicates that the current build (v2026.6.1 era) is relatively stable for end users. Positive feedback is absent from the public data, but no satisfaction issues are evident.

## Backlog Watch

No long-unanswered issues remain. The four stale issues were cleaned up today, and all open PRs were merged immediately. The maintainers appear to be keeping the backlog well-trimmed. There are no items requiring maintainer attention beyond the normal review cycle.

---

*Generated from GitHub data for 2026-07-15.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-15

## 1. Today's Overview
Moltis saw moderate activity over the past 24 hours, with 3 issues updated and 12 pull requests touched. High merge velocity (8 PRs closed/merged) signals steady cleanup of feature work and bug fixes. A new release `20260714.11` was published, bundling several of these changes. Overall project health appears positive, with ongoing feature development in browser automation, channel management, and local STT integration.

## 2. Releases
**New release: `20260714.11`**  
This release incorporates the eight PRs merged today (see §3), including the fix for MCP OAuth failures with Notion/Linear servers, CalDAV datetime parsing robustness, and support for GPT-5.6 models. No explicit breaking changes or migration notes were provided in the release announcement.

## 3. Project Progress
Eight pull requests were closed or merged in the last 24 hours:

- **#1146** – **Add GPT-5.6 model support** (merged)  
  Registers GPT-5.6 Sol, Terra, Luna in OpenAI/Codex fallback catalogs, documents 1.05M context window and 372K backend limit, and updates configuration examples.

- **#1120** – **Fix MCP OAuth `invalid_target` for servers using `resource_metadata`** (merged)  
  Resolves issue #1119 by using direct fetch for the `resource_metadata` URL found in `WWW-Authenticate` headers from Notion and Linear. Users can now add those MCP servers without authentication failure.

- **#1089** – **Cap persisted tool results before rehydration** (merged)  
  Prevents oversized tool results from overflowing provider context windows by capping content before rehydrating session history into `ChatMessage`s.

- **#1098** – **Fix browser: tolerate null optional params** (merged)  
  Small models (e.g., Gemma 4) sometimes send explicit `null` for optional browser parameters; this fix uses serde attribute adjustments to handle present-`null` values, not just missing fields.

- **#1136** – **Fix agents: coerce stringified scalar tool args before validation** (merged)  
  Addresses the same class of model quirks – local models (Gemma 4, oMLX) emit string-typed scalar arguments (e.g., `"true"`, `"5000"`). The fix coerces these strings to proper types before dispatch validation.

- **#1139** – **Fix gateway: don’t force-enable matrix-sdk via metrics feature** (merged)  
  Adds the weak `?` qualifier to `moltis-matrix/metrics` dependency, so enabling the `metrics` feature no longer pulls in the entire `matrix-sdk` when the Matrix channel is not needed.

- **#1145** – **Fix CalDAV: avoid panic on non-ASCII datetime** (merged)  
  Prevents a panic in `normalise_datetime` when a remote CalDAV server returns datetime strings that fail the ASCII-digit check on the DATE branch, by adding a fallback for non-ASCII characters.

- **#1141** – **Dependency bump (npm_and_yarn group)** (merged)  
  Routine updates to `esbuild` and `vite` across three directories.

## 4. Community Hot Topics
Activity on individual issues and PRs remains low (each item has 0–1 comments). The three updated issues all received maintenance notes:

- **#1102** – **Feature: Add FunASR/SenseVoice as local STT engine** (open since June 4) received a clarifying note on licensing and capabilities from the maintainer on July 14. This long-standing feature request is actively being evaluated.
- **#1132** – **Bug: "main" session can't be deleted/archived** (open since June 18) has a single comment but no proposed fix yet.
- **#1119** – **MCP OAuth failure** (closed, fixed by #1120) was the most impactful user-reported issue, affecting integration with two popular MCP servers (Notion, Linear).

## 5. Bugs & Stability
**Open bugs:**
- **#1132 – “main” session deletion/archival blocked** (medium severity) – Users cannot remove the default session. No fix PR exists yet; likely needs design decision on whether to allow deletion or only archiving.

**Fixed in today’s merges:**
- **MCP OAuth `invalid_target`** (high severity) – Closed by PR #1120.
- **Browser tool calls with null params** (medium) – Closed by #1098.
- **Stringified scalar tool args** (medium, affects local models) – Closed by #1136.
- **Gateway force-enabling matrix-sdk** (low, build-time issue) – Closed by #1139.
- **CalDAV panic on non-ASCII datetimes** (medium, crash risk) – Closed by #1145.

No new bugs were reported in the last 24 hours. Stability improvements are clearly being prioritized.

## 6. Feature Requests & Roadmap Signals
- **#1102 – FunASR/SenseVoice as local STT** – Receiving active discussion; maintainers added a note on licensing. Likely candidate for a future release.
- **Open PRs indicate planned features:**
  - **#1124 – Context command support for chat turns** (open since June 15) – Adds a configurable pre-turn command to inject runtime context.
  - **#1135 – Browser auto-screenshot after each action** (open since June 26) – Provides per-step visual timeline for browser tool usage.
  - **#1093 – Channel activity log visibility settings** (open since June 3) – Granular control over activity logs per account, channel, or user.

These features are likely to land in the next few releases if they pass review.

## 7. User Feedback Summary
- **Pain point**: MCP OAuth integration with Notion and Linear was broken – a critical issue for users relying on these tools. Rapid fix (issue to merged PR in one day) indicates strong responsiveness.
- **Use case**: Local STT (FunASR/SenseVoice) is desired for offline or custom speech-to-text. No negative sentiment expressed.
- **Satisfaction**: The swift resolution of #1119 and the handling of small-model quirks (#1098, #1136) demonstrate a commitment to supporting both commercial and local model ecosystems.

## 8. Backlog Watch
Several older open items lack maintainer attention or community feedback:

- **PR #1124** – *Context command support for chat turns* (created June 15, last update July 14) – No reviewer comments or approvals.
- **PR #1093** – *Channel activity log visibility settings* (created June 3, last update July 14) – No comments from maintainers.
- **Issue #1102** – *FunASR/SenseVoice STT* (created June 4, maintainer note added) – Still awaiting further action or community involvement.
- **Issue #1132** – *“main” session deletion* (created June 18) – No proposed fix or discussion beyond initial report.

These items may need escalation or a decision from the core team to keep the backlog healthy.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-15

## 1. Today's Overview
CoPaw (GitHub: agentscope-ai/QwenPaw) saw high activity in the past 24 hours with **50 issues updated** (16 open, 34 closed) and **50 PRs touched** (24 open, 26 merged/closed). A patch release **v2.0.0.post2** was published, primarily addressing sandbox sensitivity and fixing a missing module issue for auto‑memory. Community engagement remains strong, though a wave of bug reports around v2.0.0 regressions—especially sandbox loops, context compression failures, and governance bypasses—indicates the latest major release brought significant friction. The team responded quickly with several hotfix PRs, many already merged.

## 2. Releases
**v2.0.0.post2** (released 2026-07-14 or 07-15)  
- **feat**: more sensitive files detection and global read permission for sandbox ([PR #6067](https://github.com/agentscope-ai/QwenPaw/pull/6067))  
- **chore**: version bump to 2.0.0.post2  
- **test**: unit tests for runtime/security/install regression  

**Migration notes**: No breaking changes; this is a patch on v2.0.0. Users still experiencing issues from v2.0.0 should upgrade and refer to the tracking issue [#6023](https://github.com/agentscope-ai/QwenPaw/issues/6023) for known sandbox quirks.

## 3. Project Progress
Key PRs merged/closed today (24-hour window):

| PR | Description | Status |
|----|-------------|--------|
| [#6109](https://github.com/agentscope-ai/QwenPaw/pull/6109) | fix(governance): honor `sandbox_enabled` switch in OFF‑mode path | Merged |
| [#6112](https://github.com/agentscope-ai/QwenPaw/pull/6112) | feat(plugins): add Zalo Bot channel (2.0 plugin architecture) | Merged |
| [#6098](https://github.com/agentscope-ai/QwenPaw/pull/6098) | feat(memory): improve ReMe reliability, observability, CJK embedding safety | Merged |
| [#6106](https://github.com/agentscope-ai/QwenPaw/pull/6106) | fix(download_catalog): handle gzip‑encoded JSON responses | Merged |
| [#6123](https://github.com/agentscope-ai/QwenPaw/pull/6123) | fix(scroll): prevent recall loops and enforce hard context limits | Open (under review) |
| [#6122](https://github.com/agentscope-ai/QwenPaw/pull/6122) | fix(governance): clear stale OFF‑mode sandbox state | Open |

Notable: The **Zalo Bot channel** has been added as a built‑in plugin, expanding multi‑channel support to a popular Southeast Asian platform. The **ReMe memory module** gained runtime observability and better CJK embedding truncation, directly addressing [#5950](https://github.com/agentscope-ai/QwenPaw/issues/5950).

## 4. Community Hot Topics
Top issues and PRs by engagement:

- **#2291 (64 comments)** – Open tasks for contributors (P0‑P2). This sticky issue remains the primary onboarding hub.  
- **#5951 (9 comments)** – Windows sandbox pwsh recursion explosion + NTFS ACL pollution. **Closed** with fix confirmed in v2.0.0.post2.  
- **#578 (8 comments)** – Meta‑issue for “OpenClaw‑Inspired Features” (compounding agent value). Still open, indicating strong community interest in long‑term quality.  
- **#6089 (7 comments)** – Model execution error when using “opencode” free model. Closed as invalid, but indicates confusion around provider configuration.  
- **#6113 (5 comments)** – “Stuck searching memory” after upgrade to v2.0.0. Open; users express frustration with aggressive auto‑memory recall loops.  
- **#6121 (4 comments)** – DeepSeek API context compression breaks message format (tool messages orphaned). Open; a fix PR [#6108](https://github.com/agentscope-ai/QwenPaw/pull/6108) is under review.  

**Underlying needs**: Users are struggling with the v2.0.0 migration—especially sandbox/cgroup behavior on Windows, context compression breaking API rules, and auto‑memory causing endless loops. The community desires clearer configuration toggles and a “less aggressive” default memory strategy.

## 5. Bugs & Stability
High‑severity regressions reported today:

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951) | **Critical** | pwsh window recursion, 20GB memory, sandbox un‑closable on Windows | **Fixed** in v2.0.0.post2 |
| [#5829](https://github.com/agentscope-ai/QwenPaw/issues/5829) | **High** | Windows AppContainer ACE pollution crashes Chromium‑based apps | Open; regression from v2.0.0 |
| [#6113](https://github.com/agentscope-ai/QwenPaw/issues/6113) | **High** | Auto‑memory infinite loop after v2.0.0 | Open; PR [#6120](https://github.com/agentscope-ai/QwenPaw/pull/6120) (restrict memory to external user queries) under review |
| [#6121](https://github.com/agentscope-ai/QwenPaw/issues/6121) | **High** | Context compression destroys tool‑message pairing → 400 errors on DeepSeek | PR [#6108](https://github.com/agentscope-ai/QwenPaw/pull/6108) under review |
| [#6046](https://github.com/agentscope-ai/QwenPaw/issues/6046) | **High** | toolResult blocks exceed toolUse after compression → session permanently broken | Open |
| [#6009](https://github.com/agentscope-ai/QwenPaw/issues/6009) | **Medium** | Scroll context compression triggers prematurely, no hard cap → upstream rejects | PR [#6123](https://github.com/agentscope-ai/QwenPaw/pull/6123) under review |

Several of these are inter‑related (context compression). The team is actively iterating on fixes.

## 6. Feature Requests & Roadmap Signals
Requests with community traction:

- **Separate tool‑call parameter vs. result display in channels** ([#5976](https://github.com/agentscope-ai/QwenPaw/issues/5976), 4 comments) – users want truncated tool results to avoid channel spam.  
- **Real‑time user message injection into agent loops** ([#6087](https://github.com/agentscope-ai/QwenPaw/issues/6087), 4 comments) – “interrupt & correct” feature to abort wrong tool chains.  
- **CIDR‑based whitelist for auth‑free hosts** ([#6048](https://github.com/agentscope-ai/QwenPaw/issues/6048), 3 comments) – enterprise network request.  
- **OpenClaw‑inspired compounding features** ([#578](https://github.com/agentscope-ai/QwenPaw/issues/578), meta‑issue) – long‑term quality improvements.  

**Predictions**: The “interrupt” feature and memory‑loop fixes are likely candidates for v2.0.1, given the volume of complaints. The Zalo channel addition signals growing support for SEA platforms; similar channels (Telegram? WhatsApp?) may follow.

## 7. User Feedback Summary
Real pain points captured in the last 24 hours:

- **Sandbox / tool‑guard usability** – multiple users report that `approval_level: OFF` does not actually disable approvals for built‑in tools, and sandbox bypasses are hard to configure ([#6020](https://github.com/agentscope-ai/QwenPaw/issues/6020), [#5984](https://github.com/agentscope-ai/QwenPaw/issues/5984)).  
- **Regression from v1.x** – lost chat history mapping ([#5964](https://github.com/agentscope-ai/QwenPaw/issues/5964)), agent config overwritten after upgrade ([#6100](https://github.com/agentscope-ai/QwenPaw/issues/6100)), scroll context making sessions unusable ([#6046](https://github.com/agentscope-ai/QwenPaw/issues/6046)).  
- **DeepSeek / model compatibility** – tool‑message serialisation errors, “unknown model” errors with opencode provider ([#6089](https://github.com/agentscope-ai/QwenPaw/issues/6089), [#6077](https://github.com/agentscope-ai/QwenPaw/issues/6077)).  
- **Memory performance** – Chinese memory indexing fails due to character‑based truncation ([#5950](https://github.com/agentscope-ai/QwenPaw/issues/5950), fixed in v2.0.0.post2). Auto‑memory too aggressive, causing loops ([#6113](https://github.com/agentscope-ai/QwenPaw/issues/6113)).  

Satisfaction: some users appreciate the quick patch releases and the team’s responsiveness (e.g., Windows sandbox fix landed within 24 hours). The overall sentiment is slightly negative for the v2.0.0 stability, but many acknowledge the complexity of sandbox and multi‑agent orchestration.

## 8. Backlog Watch
Issues/PRs requiring maintainer attention (unanswered for >3 days or with high comment count but no assignee):

| Item | Age | Notes |
|------|-----|-------|
| [#5333](https://github.com/agentscope-ai/QwenPaw/issues/5333) | ~26 days | Agent stuck after command; possible deepseek compatibility. Low priority but no resolution. |
| [#586](https://github.com/agentscope-ai/QwenPaw/issues/586) | ~4.5 months | Daemon and command dispatch feature request (two‑phase). No recent activity. |
| [#6088](https://github.com/agentscope-ai/QwenPaw/issues/6088) | 1 day | Message queue broken after v2.0.0.post1 – urgent but already acknowledged (PR [#6040](https://github.com/agentscope-ai/QwenPaw/pull/6040) referenced). |
| [#5829](https://github.com/agentscope-ai/QwenPaw/issues/5829) | 8 days | Windows ACE pollution – still open, no fix assigned. High severity. |
| [#5964](https://github.com/agentscope-ai/QwenPaw/issues/5964) | 4 days | Lost chat mapping after upgrade – no maintainer response yet. |

The team has been active on recent regressions, but older low‑priority feature requests and lingering bugs (especially platform‑specific sandbox issues) could benefit from triage. The sticky issue #2291 remains the best place for new contributors to find tasks.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-15

## 1. Today's Overview
ZeroClaw saw elevated activity with **29 issues** and **50 pull requests** updated in the last 24 hours, of which **6 issues and 12 PRs** were closed or merged. The project remains in a high-velocity development phase, focusing on **SOP (Standard Operating Procedure) engine hardening**, **multi-user isolation**, **plugin infrastructure** (WASM channel plugins, outbound WebSocket/TCP), and **provider reliability** fixes. No new releases were published today; the next planned milestones are v0.8.4 (maintenance train) and the “zerorelay” secure-relay feature. Several critical bugs at P1 severity are open and actively discussed.

## 2. Releases
*No new releases in the last 24 hours.*

## 3. Project Progress
**12 PRs were merged/closed** today. Notable merges include:
- **PR #9077** – [`docs(ops): drop spurious positional arg from channel start example`](https://github.com/zeroclaw-labs/zeroclaw/pull/9077) – fixes a documentation error.
- **PR #8582** – [`fix(zerocode): terminate ephemeral daemon on connection failure`](https://github.com/zeroclaw-labs/zeroclaw/pull/8582) – prevents orphan daemon processes.

Several **SOP-related bugs** were closed, indicating steady progress on the SOP engine:
- **Issue #8678** – *advance_step has no run-status guard* – resolved.
- **Issue #8631** – *headless deterministic SOP steps recorded Completed without executing* – fixed.
- **Issue #8695** – *Cron jobs still recall memory even when `uses_memory = false`* – closed.
- **Issue #6689** – *Production SOP audit is silently no-op* – addressed.
- **Issue #8413** – *channel-filesystem SOP event source* – shipped.
- **Issue #6686** – *SOP cron triggers have no production caller* – resolved.

Also closed: **Issue #8413** (filesystem SOP source) and **Issue #6686** (SOP cron trigger wiring).

## 4. Community Hot Topics
The most active discussion threads are:

- **[Issue #5982 – Per-sender RBAC for multi-tenant agent deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982)** (10 comments) – A major feature request to isolate workspaces, tools, and rate limits per user class. This aligns with the multi-user milestone trackers (#8290, #8289) and is a top community ask.
- **[Issue #6055 – Slack: hydrate thread context from conversations.replies](https://github.com/zeroclaw-labs/zeroclaw/issues/6055)** (7 comments) – Follow-up on strict mention threading; users want automatic backfill of thread history.
- **[Issue #8973 – Landlock blocks shell access to required system files on Fedora](https://github.com/zeroclaw-labs/zeroclaw/issues/8973)** (4 comments) – A P1 security bug affecting Fedora users, with active debugging.
- **[Issue #8933 – RFC: Add cross-turn conversation correlation to OTel export](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)** (3 comments) – Proposal to improve observability for multi-turn conversations.
- **[Issue #9048 – RFC: Separate conversation history from long-term memory](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)** (3 comments) – Architectural RFC to untangle session history and curated memory.

Active PRs drawing attention (though comment counts are not reported) include **#8486** (OpenAI chat completions endpoint), **#8880** (SOP approval broker with quorum), and **#8863/#8923** (plugin outbound WebSocket/TCP).

## 5. Bugs & Stability
**P1 (Critical) bugs still open:**
- **[#8973 – Landlock blocks shell on Fedora](https://github.com/zeroclaw-labs/zeroclaw/issues/8973)** – Affects `sh` access to `/dev/null`; severity S2.
- **[#8563 – SOPs not available through web dashboard chat](https://github.com/zeroclaw-labs/zeroclaw/issues/8563)** – S1 workflow blocker; configured SOPs invisible to the agent.
- **[#8675 – Malformed tool-call arguments cause provider 400 → empty reply](https://github.com/zeroclaw-labs/zeroclaw/issues/8675)** – S1; affects OpenAI-wire providers (OpenRouter, Azure, etc.).
- **[#7947 – execute_pipeline bypasses per-agent tool gating (confused deputy)](https://github.com/zeroclaw-labs/zeroclaw/issues/7947)** – S0 security risk; pipelines ignore per-agent `ToolAccessPolicy`.

**P2 bugs:**
- **[#9052 – channel-line omitted from channels-full and ci-all coverage](https://github.com/zeroclaw-labs/zeroclaw/issues/9052)** – S1 workflow blocker for LINE channel CI.
- **[#9001 – Provider turn failures bury cause-specific diagnostics](https://github.com/zeroclaw-labs/zeroclaw/issues/9001)** – S2; generic retry envelopes hide root causes.

**Bugs closed today** include the SOP engine issues listed in Section 3 (#8678, #8631, #8695, #6689) and the cron memory bug (#8695). Fix PRs exist for #8678 and #8631.

## 6. Feature Requests & Roadmap Signals
Strong demand for **multi-tenant and identity features** is evident:
- **Per-sender RBAC** (#5982) – likely to be delivered in the v0.8.x line as part of the multi-user milestone (#8290).
- **OIDC integration** (#8289) and **uniform Principal** are tracked for early next release.
- **SOP enhancements** continue: approval broker (#8880), routing false-when (#8719), centralized ingress adapters (#8581), and authoring surface (#8736) – most are part of the “SOP 5/5” epic (#8288).
- **Plugin ecosystem** is growing rapidly: WASM channel plugins with outbound WebSocket/TCP (#8863, #8923) and webhook ingress (#8862) are near completion.
- **Observability** improvements: OTel cross-turn correlation (#8933) and memory separation (#9048) are RFC-stage.

Predictions for next version (v0.8.4):
- SOP authoring UI and approval broker (tracked in #8288, #8736).
- Multi-user isolation for gateways (#8290).
- OIDC first-shippable (#8289).
- Plugin WebSocket and TCP transports (#8863, #8923).
- OpenRouter provider fixes and vision capability (#9029).

## 7. User Feedback Summary
Real pain points reported by users:

- **Security & permissions**: The Landlock regression on Fedora (#8973) blocks shell tool usage; the confused deputy bug (#7947) raises trust concerns.
- **Multi-tenant isolation**: Users running shared ZeroClaw instances want per-sender RBAC (#5982) to separate customer/operator/developer access.
- **Channel quirks**: Slack thread hydration (#6055) and LINE channel CI omission (#9052) frustrate channel adopters.
- **Provider reliability**: Malformed tool-call arguments (#8675) cause silent failures with OpenAI-compatible providers; diagnostic burying (#9001) makes debugging hard.
- **SOP usability**: The web dashboard not showing SOPs (#8563) is a major blocker for users who want to manage workflows via UI. Missing SOP examples in docs (#8587) also noted.
- **Memory model confusion**: Users want clearer separation between conversation history and long-term memory (#9048), and the `uses_memory = false` bug (#8695) undermined stateless cron jobs.

Positive signals: Active PRs for OpenAI-compatible endpoint (#8486) and Matrix progress drafts (#8443) show enthusiasm for extending integration surface.

## 8. Backlog Watch
High-priority items that have been open for extended periods without maintainer action:

- **[Issue #6685 – SOP HTTP fan-in (POST /sop/*) documented but not wired](https://github.com/zeroclaw-labs/zeroclaw/issues/6685)** (open since May 15, P2) – Promised endpoint for SOP webhooks missing; users must use workarounds.
- **[Issue #5607 – pre-hook skip gates for cron jobs and SOP triggers](https://github.com/zeroclaw-labs/zeroclaw/issues/5607)** (open since April 10, status:blocked) – A lightweight precondition script request; blocked without clear resolution.
- **[PR #8353 – fix(runtime): improve error message context](https://github.com/zeroclaw-labs/zeroclaw/pull/8353)** (open since June 26, needs-author-action) – Improves panic messages but stalled awaiting review.
- **[Issue #8736 – Track SOP authoring surface](https://github.com/zeroclaw-labs/zeroclaw/issues/8736)** (open since July 5, in-progress) – Task tracking a major feature; maintainer attention needed to shepherd through review.

These items indicate areas where community effort is waiting on maintainer bandwidth.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*