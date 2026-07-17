# OpenClaw Ecosystem Digest 2026-07-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-17 01:59 UTC

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

# OpenClaw Project Digest – 2026-07-17

## 1. Today's Overview
Project activity remains extremely high, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, 327 issues are open/active and 173 closed; 314 PRs are open and 186 have been merged or closed. No new releases were published today. The update cycle is dominated by bug reports and regressions following the recent `2026.7.1` release, alongside a steady stream of CI fixes and channel-specific improvements. The maintainer team is actively reviewing and merging PRs, but several critical stability issues (gateway crash-loops, session stalls, tool schema incompatibilities) remain unresolved and are drawing high community attention.

---

## 2. Releases
**No new releases** today. The latest published version remains **2026.7.1**, which is the subject of many regression reports in this digest.

---

## 3. Project Progress
**Merged/closed PRs today (selected):**

- [#109481 fix(scripts): preserve emoji in request log previews](https://github.com/openclaw/openclaw/pull/109481) – Fixes malformed Unicode in mock E2E logs.
- [#108120 fix(matrix): reject oversized piped recovery keys](https://github.com/openclaw/openclaw/pull/108120) – Security hardening for Matrix CLI.
- [#109480 refactor(channels): centralize mention and group activation decisions](https://github.com/openclaw/openclaw/pull/109480) – Unifies mention logic across Matrix, Telegram, and QQBot.
- [#109024 fix(tailscale): bound whois identity cache growth](https://github.com/openclaw/openclaw/pull/109024) – Prevents unbounded cache in Tailscale identity verification.
- [#109393 fix(ui): prevent generated locale rebase conflicts](https://github.com/openclaw/openclaw/pull/109393) – Reduces merge conflicts in Control UI locale files.
- [#108172 fix(release): preserve emoji in ClawHub error details](https://github.com/openclaw/openclaw/pull/108172) – Surrogate-safe truncation for release diagnostics.

**Notable open PRs progressing toward merge:**
- [#102296 feat: add plan-first Claw status and remove (XL)](https://github.com/openclaw/openclaw/pull/102296) – Experimental `claws status` and safe `claws remove`.
- [#89783 feat(feishu): bot-to-bot conversation support](https://github.com/openclaw/openclaw/pull/89783) – Adds @mention handling for Feishu.
- [#109212 feat: add native inline widget support](https://github.com/openclaw/openclaw/pull/109212) – Extends `show_widget` to iOS/Android/macOS.
- [#95604 feat(discord): show subagent progress](https://github.com/openclaw/openclaw/pull/95604) – Opt-in Discord progress feedback.

---

## 4. Community Hot Topics
The most engaged issues this cycle:

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#75 Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 114 | 81👍 | Long-standing request for desktop apps beyond macOS/iOS. |
| [#88312 [Regression] Codex turn-completion stall](https://github.com/openclaw/openclaw/issues/88312) | 20 | 5👍 | `2026.5.27` regression blocking Codex multi-tool turns. |
| [#7707 Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) | 17 | 0👍 | Feature to prevent memory poisoning from untrusted sources. |
| [#104721 All tool results return "(see attached image)"](https://github.com/openclaw/openclaw/issues/104721) | 17 | 1👍 | P0 regression: literal placeholder string instead of actual data. |
| [#87744 Codex-backed Telegram turns time out](https://github.com/openclaw/openclaw/issues/87744) | 15 | 3👍 | Turns do work but never reach `turn/completed` on 2026.5.27. |
| [#94518 DeepSeek cache hit rate <10% after 6.x upgrade](https://github.com/openclaw/openclaw/issues/94518) | 11 | 10👍 | Boundary-aware caching breaks prefix matching, destroying cache utility. |
| [#10659 Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) | 13 | 4👍 | Prevent agent from seeing raw API keys. |
| [#90916 Topic-session families](https://github.com/openclaw/openclaw/issues/90916) | 8 | 2👍 | Isolated context lanes for one assistant. |

**Underlying needs:** Users are demanding cross-platform parity (Linux/Windows apps), better security primitives (masked secrets, memory trust tags), and urgent fixes for regressions that break core functionality (Codex stalls, tool output corruption, cache performance). The high reaction count on #75 and #94518 shows widespread frustration with platform gaps and provider degradation.

---

## 5. Bugs & Stability
**Critical (P0) regressions reported or escalated today:**

- [#104721 (P0) Tool results return literal "(see attached image)"](https://github.com/openclaw/openclaw/issues/104721) – *Closed* (likely fixed or dup). Affects all file reads.
- [#107220 (P0) Gateway crash-loop: legacy memory sidecar conflicts fatal](https://github.com/openclaw/openclaw/issues/107220) – *Closed*. Upgrade from 2026.6.11 → 2026.7.1 causes crash on startup.
- [#107694 (P0) Gateway fails to start due to strict migration guard](https://github.com/openclaw/openclaw/issues/107694) – *Closed*. Benign legacy migration skips block startup.
- [#106920 (P0) openclaw 2026.7.1 can't restart gateway](https://github.com/openclaw/openclaw/issues/106920) – *Closed*. Upgrade fails to restart gateway.
- [#107930 (P0) Improve upgrade experience when Node.js version changes](https://github.com/openclaw/openclaw/issues/107930) – *Open*. Users hit manual upgrade steps.

**High-severity (P1) regressions:**

- [#88312 (P1) Codex turn-completion stall regression (still open)](https://github.com/openclaw/openclaw/issues/88312) – Multiple users affected; fix PR #85107 was incomplete.
- [#87744 (P1) Codex Telegram turns time out (still open)](https://github.com/openclaw/openclaw/issues/87744) – Turns never reach completion.
- [#91009 (P1) Codex PreToolUse hook relay spawns CPU-bound processes (still open)](https://github.com/openclaw/openclaw/issues/91009) – Gateway RPC stalls.
- [#94518 (P1) DeepSeek cache hit rate <10% (closed)](https://github.com/openclaw/openclaw/issues/94518) – Fixed? PR linked.
- [#108182 (P1) Control UI is worse (open)](https://github.com/openclaw/openclaw/issues/108182) – Missing navigation after 2026.7.1.
- [#108075 (regression) LLM request rejected schema/tool payload (open)](https://github.com/openclaw/openclaw/issues/108075) – Provider rejection after upgrade.
- [#107449 (P1) cron tool JSON Schema incompatible with llama.cpp (closed)](https://github.com/openclaw/openclaw/issues/107449) – Pattern `\S` breaks local models.
- [#108473 (regression) cron tool schema breaks llama.cpp tool-calling (open)](https://github.com/openclaw/openclaw/issues/108473) – Similar issue persists.
- [#92769 (P1) Reasoning details dropped for MiniMax M3 via OpenRouter (open)](https://github.com/openclaw/openclaw/issues/92769) – Caused by `:floor` suffix.
- [#108238 (P1) Context usage miscounts cacheRead as totalTokens (open)](https://github.com/openclaw/openclaw/issues/108238) – False compaction trigger.
- [#107873 (P1) Embedded prompt-lock session takeover aborts WebChat (open)](https://github.com/openclaw/openclaw/issues/107873) – No retry after tool failure.
- [#106231 (P1) Loop detection blocks exec but doesn’t terminate agent (open)](https://github.com/openclaw/openclaw/issues/106231) – Resource burn.
- [#37616 (P1) OpenClaw leaks unreaped child processes (open)](https://github.com/openclaw/openclaw/issues/37616) – Zombie accumulation.

**Fix PRs in progress:** Many of these issues have linked PRs (e.g., #88312, #87744, #91009). The volume suggests the `2026.7.1` release introduced several interacting regressions in the gateway, Codex integration, and tool schema generation.

---

## 6. Feature Requests & Roadmap Signals
- **Cross-platform apps** (#75) – Linux/Windows Clawdbot Apps remain the #1 requested feature. Likely targeted for next major release.
- **Memory security** (#7707, #10659, #7722) – Trust tagging, masked secrets, filesystem sandboxing. Growing demand as agents gain autonomy.
- **Session architecture** (#90916, #96975, #11665) – Topic-session families, subagent isolation, webhook multi-turn. Reflects need for production-grade session management.
- **Telegram/WhatsApp enhancements** (#10944, #7476, #11460) – parseMode config, sticker support, reaction queries.
- **Model fallback improvements** (#9986) – Fallback on context length exceeded, not just API errors.
- **Voice streaming** (#8355) – Sentence-level TTS pipeline for voice calls.
- **Self-compact tool** (#6757) – Agent-triggered context compaction.

**Prediction:** The next minor release (2026.7.x) will likely prioritize bugfixes for the above regressions, while the next feature release may include Linux/Windows app support (based on #75 momentum) and memory security features (many `clawsweeper:needs-product-decision` labels suggest active design discussions).

---

## 7. User Feedback Summary
**Satisfaction signals:**
- High engagement with feature requests indicates a proactive community.
- Successful merges of CI reliability fixes (emoji preservation, timeout bounding) show responsiveness.

**Dissatisfaction/pain points:**
- **Regression fatigue:** Multiple users report “worked before, now fails” after 2026.7.1 upgrade. Specific complaints: “completely broken” (#104721), “reliably fails” (#88312), “crash-loops on startup” (#107220).
- **Missing platforms:** “We have apps for macOS, iOS and Android… Linux and Windows are missing” (#75) – a recurring theme for months.
- **Channel-specific regressions:** Matrix thread replies broken (#87307), Telegram timeout (#87744), LINE table messages dropped (#65656), Discord cross-context heartbeat (#102206).
- **Provider incompatibility:** DeepSeek cache hit rate plummet (#94518), llama.cpp schema breakage (#107449), MiniMax reasoning loss (#92769).
- **Poor upgrade experience:** Node.js version changes require manual intervention (#107930).

**Use cases driving feedback:**
- Multi-platform deployment (enterprise/lab environments need Linux).
- Production reliability (session persistence, subagent abort, memory management).
- Security-conscious deployments (secrets exposure, filesystem access, memory poisoning).
- Chat platform integration (Matrix, Telegram, Discord, LINE, WhatsApp).

---

## 8. Backlog Watch
Issues that have languished for months with maintainer attention needed:

| Issue | Created | Last Update | Comments | Status |
|-------|---------|-------------|----------|--------|
| [#75 Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | 2026-07-17 | 114 | Open, help wanted, needs product decision |
| [#7707 Memory Trust Tagging](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | 2026-07-16 | 17 | Open, needs maintainer + product review |
| [#10659 Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | 2026-07-16 | 13 | Open, needs security review |
| [#7722 Filesystem Sandboxing](https://github.com/openclaw/openclaw/issues/7722) | 2026-02-03 | 2026-07-17 | 9 | Open, needs maintainer + product review |
| [#11665 Webhook multi-turn](https://github.com/openclaw/openclaw/issues/11665) | 2026-02-08 | 2026-07-17 | 11 | Open, linked PR open but stale |
| [#8299 Suppress sub-agent announce](https://github.com/openclaw/openclaw/issues/8299) | 2026-02-03 | 2026-07-16 | 7 | Open, needs product decision |
| [#90916 Topic-session families](https://github.com/openclaw/openclaw/issues/90916) | 2026-06-06 | 2026-07-16 | 8 | Stale, needs maintainer + security review |
| [#38091 WebSocket reconnect terminates session](https://github.com/openclaw/openclaw/issues/38091) | 2026-03-06 | 2026-07-17 | 7 | Open, needs live repro |

**What’s blocking these?** Most carry `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`. The sheer volume of new regressions is likely diverting maintainer attention from long-standing enhancements. A dedicated triage session for these older issues would be beneficial.

---

*Data as of 2026-07-17, based on GitHub activity (openclaw/openclaw). All links point to the official repository.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant Ecosystem
**Date:** 2026-07-17 | **Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing a maturity phase, characterized by post-release stabilization cycles, architectural consolidation, and growing community expectations around production reliability. The core reference project (OpenClaw) is recovering from a regression-heavy release, while specialized forks and derivatives are carving distinct niches—Hermes Agent focuses on desktop/CLI power users, IronClaw pursues a ground-up rewrite ("Reborn"), and CoPaw/NanoClaw prioritize channel integration breadth. The ecosystem-wide pattern shows that maintaining a general-purpose agent is increasingly complex, driving differentiation around platform support, memory management, provider flexibility, and security primitives. Developer mindshare is fragmented but largely orbits OpenClaw's conventions, with several projects explicitly aligning their interfaces to OpenClaw's architectural patterns.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score | Status Summary |
|---------|-------------|-----------|----------------|--------------|----------------|
| **OpenClaw** | 500 (327 open) | 500 (314 open) | 2026.7.1 (regression reports) | 🟡 | High activity, regression crisis |
| **Hermes Agent** | 50 (42 open) | 50 (44 open) | Pre-release | 🟡 | Active development, many parallel tracks |
| **ZeroClaw** | 25 (23 open) | 50 (46 open) | v0.8.3 (next: v0.8.4) | 🟢 | Rapid feature iteration, good structure |
| **IronClaw** | 18 (open) | 39 (open) | Pre-release (Reborn) | 🟡 | Deep rewrite, architectural debt focus |
| **LobsterAI (CoPaw)** | 43 (23 open) | 46 (21 open) | 2.0.0.post2 (regression reports) | 🟡 | High merge rate, v2 stabilization |
| **NanoClaw** | 4 (3 open) | 19 (16 open) | None | 🟢 | Focused maintenance, targeted fixes |
| **NanoBot** | 1 (open) | 12 (11 open) | None | 🟢 | Low activity, community-maintained |
| **PicoClaw** | 2 (1 open) | 9 (all open) | 0.3.1 | 🟡 | Stalled contributions, maintainer bottleneck |
| **Moltis** | 0 | 3 (merged) | 20260716.01 | 🟢 | Clean backlog, well-scoped patches |
| **NullClaw** | 1 (critical) | 0 | v2026.5.29 | 🔴 | Critical unpatched crash, no activity |
| **TinyClaw** | 0 | 0 | N/A | ⚪ | Dormant |
| **ZeptoClaw** | 5 (closed) | 0 | None | 🟢 | Security documentation only |

**Health Scale:** 🟢 Stable | 🟡 Active with issues | 🔴 Critical concern | ⚪ Inactive

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale:** 5×+ the activity of any peer—500 issues/500 PRs in 24h demonstrates unmatched community engagement and contributor pool.
- **Platform coverage:** Has existing macOS, iOS, Android, and Web clients; the #1 feature request (#75) for Linux/Windows desktop apps signals clear path for growth.
- **Integration breadth:** Matrix, Telegram, QQBot, Discord, LINE, WhatsApp, Feishu—the widest channel support in the ecosystem.
- **Reference status:** Architectural patterns (gateway, memory sidecar, tool schema, channel adapters) are adopted by derivatives like NanoClaw, PicoClaw, and Hermes Agent.

**Technical Approach Differences:**
- **Monolithic vs. modular:** OpenClaw's codebase is more monolithic than ZeroClaw (plugin-architecture) or IronClaw (ground-up "Reborn" redesign). This enables rapid feature iteration but causes regression cascades (2026.7.1 release broke Codex, DeepSeek caching, tool schemas, and gateway startup).
- **Memory architecture:** OpenClaw uses a sidecar pattern for memory management; Hermes Agent has reportedly deprecated its sidecar in favor of in-process memory. ZeroClaw is actively separating conversation history from long-term memory (RFC #9048).
- **Provider abstraction:** OpenClaw's provider layer is mature but shows strain—DeepSeek cache hits dropped <10% after a "boundary-aware caching" change (#94518). ZeroClaw and Hermes Agent have active refactoring to unify provider clients.

**Community Size Indicators:**
- OpenClaw's #1 feature request (#75, Linux/Windows) has 114 comments and 81 reactions—more engagement than some entire project repositories.
- Regression issues in OpenClaw (e.g., #88312, 20 comments) often exceed total community engagement in smaller projects like NanoBot or Moltis.
- OpenClaw maintains a dedicated triage label system (`clawsweeper:needs-product-decision`) that other projects lack, indicating more mature governance processes.

**Vulnerability:** The sheer volume of regressions is eroding trust. Multiple "worked before, now fails" complaints post-2026.7.1 suggest quality assurance processes are not scaling with feature velocity. Competitors (Hermes, ZeroClaw) are gaining developer mindshare specifically because they offer more stable experiences for specific platforms.

---

## 4. Shared Technical Focus Areas

The following requirements appear across **three or more** projects, indicating ecosystem-wide priorities:

| Requirement | Appears In | Specific Needs |
|-------------|-----------|----------------|
| **Memory security & governance** | OpenClaw, Hermes Agent, ZeroClaw, CoPaw | Memory trust tagging (#7707, OpenClaw); masked secrets (#10659, OpenClaw); filesystem sandboxing (#7722, OpenClaw); persistent memory tracker (#8891, ZeroClaw); session context loss (#6074, CoPaw); memory poisoning prevention (multiple projects) |
| **Provider-agnostic model routing** | OpenClaw, ZeroClaw, Hermes Agent, Moltis | Unified provider client (#5937, ZeroClaw); LLM fallback on context length exceeded (#9986, OpenClaw); Claude SDK OAuth (#25267, Hermes); Codex ↔ Claude quota fallback (#3057, NanoClaw); Kimi K3 support (#1156, Moltis) |
| **Cross-platform parity** | OpenClaw, Hermes Agent, CoPaw, NullClaw | Linux/Windows desktop apps (#75, OpenClaw); ARM64 support (#976, NullClaw; #3260, PicoClaw); Windows admin elevation fix (#6161/6127, CoPaw); multi-arch CI builds (#6160, IronClaw) |
| **Session/context management** | OpenClaw, ZeroClaw, Hermes Agent, CoPaw | Topic-session families (#90916, OpenClaw); conversation history vs. long-term memory separation (#9048, ZeroClaw); cross-platform session sharing (#4335, Hermes); session context loss on agent switch (#6074, CoPaw); in-memory session cache bounds (#4957, NanoBot) |
| **Production reliability** | OpenClaw, ZeroClaw, NanoClaw, CoPaw, NullClaw | Silent message drops (#5995, CoPaw); gateway crash-loops (#107220, OpenClaw); zombie processes (#37616, OpenClaw; #3060, NanoClaw); SIGSEGV on aarch64 (#976, NullClaw); token drain anomalies (#6158, CoPaw); retry-after-delays fixes (#4959, NanoBot) |
| **Platform-specific channel enhancements** | OpenClaw, NanoClaw, Hermes Agent, PicoClaw | Telegram timeout (#87744, OpenClaw); WhatsApp Cloud adapter (#2913, NanoClaw); Slack worker progress (#65634, Hermes); Signal image attachments (#2695, NanoClaw); LINE table messages (#65656, OpenClaw); Dial channel (SMS + AI voice, #3041, NanoClaw) |
| **Documentation & onboarding** | OpenClaw, ZeroClaw, NanoBot, IronClaw | Capability-aware agent docs (#8367, ZeroClaw); Reborn NUX demo (#5565, IronClaw); community maintenance docs (#4950, NanoBot); README updates across projects |
| **Continuous integration & testing** | OpenClaw, CoPaw, IronClaw, ZeroClaw | E2E test adaptation for UI changes (#6185, CoPaw); nightly CI coverage (#6194, CoPaw); shared OAuth conformance suite (#6114, IronClaw); CI bottleneck from deps/ signing (#9101, ZeroClaw) |

**Cross-cutting insight:** Memory security and provider agnosticism are the two most consistent themes across the ecosystem. All projects are grappling with how to give agents autonomy while preventing data leaks or unexpected costs. The "unbounded memory" pattern—where agents accumulate context indefinitely—is a top concern being addressed through explicit memory compaction, trust tagging, and session architecture changes.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | IronClaw (Reborn) | CoPaw (LobsterAI) | NanoClaw | Moltis |
|-----------|----------|--------------|----------|-------------------|--------------------|----------|---------|
| **Primary user** | General developers, multi-platform | Desktop/CLI power users | Plugin/extensibility developers | Enterprise, security-focused | Windows/Desktop users, integration | Channel integrators | Minimalist developers |
| **Architecture** | Monolithic with sidecars | Modular, process-per-desktop | Plugin-host (WASM channels) | "Reborn" ground-up Rust rewrite | Python + Tauri desktop | OpenClaw-aligned adapter pattern | Clean, minimal core |
| **Key strength** | Broadest ecosystem & integrations | Best desktop UX, Claude SDK focus | Plugability, memory refactor | Security-centric redesign | Fast iteration, Windows focus | Rapid bugfixes, channel agility | Zero-backlog discipline |
| **Key weakness** | Regression-prone, QA pressure | Desktop-only, no mobile | Maintainer bandwidth, configuration complexity | Architectural churn, OAuth instability | Post-v2 regression fatigue, token anomalies | Low engagement, scaling unknown | Low community contribution |
| **Release cadence** | Frequent (monthly minor) | Continuous | Planned (v0.8.4 target Jul 31) | Pre-release | Rapid (2.0.0.post2) | Ad-hoc | Patch-driven |
| **Provider strategy** | Broadest support, multiple models | Claude-centric + OpenAI | Unified client refactor | Reborn: new provider layer | DeepSeek + OpenAI | Host-orchestrated fallback | Kimi + OpenAI |
| **Community model** | Large, somewhat chaotic | Active, contributor-friendly | RFC-driven, structured | Small, core-team heavy | Moderate, welcoming | Small, maintainer-responsive | Minimal, maintainer-only |

**Niche Players:**
- **NullClaw:** Minimal activity, Telegram-focused with critical ARM bug
- **PicoClaw:** Embedded/RISC-V focus (NanoKVM), stalled
- **ZeptoClaw:** Security classification tooling, not a general agent
- **TinyClaw:** Dormant
- **NanoBot:** Community-maintained, minimal engagement

---

## 6. Community Momentum & Maturity

**Tier 1: High Momentum, Scaling Challenges**
- **OpenClaw** — Largest and most active, but struggling with quality control as feature velocity outpaces testing. The regression crisis post-2026.7.1 is a cautionary tale for the ecosystem. Emerging need: dedicated QA/release infrastructure.
- **Hermes Agent** — Strong momentum, particularly around desktop experience and Claude integration. Growing contributor diversity. Could challenge OpenClaw's dominance in the desktop/professional segment if it adds mobile and web channels.
- **ZeroClaw** — Highest signal-to-noise ratio in current activity. Plugin architecture (WASM channels) is architecturally ambitious and could define the next generation of agent extensibility. Memory refactoring is well-scoped.

**Tier 2: Rapid Iteration, Post-Release Stabilization**
- **IronClaw** — Deep architectural work on "Reborn" shows ambition but carries risk of prolonged instability. The OAuth lifecycle reversion (#6166) signals tension between velocity and reliability.
- **CoPaw (LobsterAI)** — Merged 25 PRs in 24h, the highest merge rate observed. Strong response to post-v2 regressions. Windows focus is a differentiating strength given OpenClaw's lack of Windows desktop apps. Risk: token cost transparency concerns could trigger user trust issues.

**Tier 3: Stable/Contained**
- **NanoClaw** — Low activity but targeted, well-executed fixes (WhatsApp Cloud collision resolved in <24h). Room for growth if more contributors surface.
- **Moltis** — Cleanest project in the ecosystem: zero open issues/PRs, consistent small releases. Likely an internal team project with low community reliance.
- **ZeptoClaw** — Narrow scope (security docs) but consistent execution. Not a general agent—more of a security tool.

**Tier 4: Stalled/Dormant**
- **PicoClaw** — Maintainer bottleneck visible: 9 open PRs aging 7–35 days with no review. The NanoKVM bug (#3195) is a missed opportunity for embedded agent use cases.
- **NullClaw** — Critical ARM crash unaddressed. Single-developer risk.
- **NanoBot** — Community-maintained but no active maintainer engagement. Depends on contributor-driven fixes.
- **TinyClaw** — No activity. Effectively archived.

---

## 7. Trend Signals

### 1. Agent reliability is the #1 unmet need
Across every project, the most commented issues are about **agents that don't behave reliably**: silent message drops (CoPaw, OpenClaw), crash loops (NullClaw, OpenClaw), stalled turns (OpenClaw), zombie processes (multiple projects), and token drains (CoPaw). Users are hitting trust ceilings—they're willing to accept imperfect AI reasoning if the agent infrastructure is deterministic and predictable. **Implication:** Projects that solve reliability (Moltis' approach, or ZeroClaw's structured RFC process) will differentiate as the ecosystem matures.

### 2. Security is accelerating from nice-to-have to table-stakes
Memory trust tagging, masked secrets, filesystem sandboxing, UAC elevation fixes, and provider permission granularity are all appearing simultaneously. This is driven by agents gaining more autonomy (tool execution, code generation, file access). **Implication:** A security audit or design document from any project will be a competitive advantage. The absence of security features (NullClaw, TinyCl

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-07-17

## Today's Overview
Activity in the NanoBot repository over the past 24 hours was moderate, with 12 pull requests updated (11 open, 1 merged) and only 1 active issue. No new releases were published. The project’s focus appears to be on stability and bug fixing, with several high‑priority (p1) PRs addressing session cache bounds, message caps, Docker security hardening, and subagent visibility in the WebUI. The lone merged PR was a documentation update reflecting the project’s community maintenance model. Community discussion remains quiet, with zero comments on both the new issue and the open PRs.

## Releases
No new releases were created in the last 24 hours. The last known release remains unchanged.

## Project Progress – Merged Pull Requests
- **#4950** – [docs(readme): reflect community maintenance](https://github.com/HKUDS/nanobot/pull/4950)  
  Merged. A documentation‑only change that updates the README contact section to explicitly state that NanoBot is now maintained collaboratively with open‑source contributors.

No other PRs were merged or closed. All remaining PRs are still open and under review.

## Community Hot Topics
The only active issue and all open PRs have **zero comments and zero reactions**. There is no visible discussion or controversy to report. The most recently updated items are:

- **Issue #4948** – [WebUI loses visibility when a late subagent completion starts a system turn](https://github.com/HKUDS/nanobot/issues/4948)  
  Reports a UI lifecycle bug. No comments yet; a companion fix PR (#4954) has been submitted.

- **PR #4959** – [fix: add one second to retry after delays](https://github.com/HKUDS/nanobot/pull/4959)  
  Addresses repeated “requests limit reached” warnings by adjusting retry timing.

The absence of community engagement may indicate that the submitted issues and PRs are well‑scoped, or that the community is waiting for maintainer feedback before joining the conversation.

## Bugs & Stability
Several critical bug fixes were proposed today, all ranked priority p1 by their authors:

| Rank | Bug / Issue | Fix PR | Summary |
|------|-------------|--------|---------|
| **High** | **Issue #4948**: WebUI loses visibility on late subagent completion | **#4954** – fix(webui): keep late subagent turns visible | The agent’s lifecycle stops updating the UI when a subagent finishes after the mid‑turn injection limit. PR #4954 preserves WebUI delivery metadata for subagent results. |
| **High** | **PR #4960**: Real cancellation lost in MCP/AnyIO integrations | *(self‑fix)* – fix: preserve real cancellation in MCP paths | Introduces a helper to distinguish external task cancellation from leaked `CancelledError` signals; fixes silent swallowing. |
| **High** | **PR #4957**: Unbounded in‑memory session cache | *(self‑fix)* – fix(session): bound the in‑memory session cache | Adds a 128‑entry LRU cache + weak overflow to prevent memory exhaustion. |
| **High** | **PR #4956**: Messages exceeding 2,000 cap ignored | *(self‑fix)* – fix(session): cap messages at persistence boundary | Enforces the file cap at save time, binding the agent’s raw‑memory archiver. |
| **Medium** | **PR #4955**: Default Docker Compose insecure (SYS_ADMIN, unconfined AppArmor) | *(self‑fix)* – (fix docker) Harden default Docker Compose security | Removes dangerous capabilities; adds opt‑in `bwrap` configuration. |
| **Medium** | **PR #4952**: UTF‑16 surrogates cause `UnicodeEncodeError` | *(self‑fix)* – fix(providers): sanitize UTF‑16 surrogates | Strips lone surrogates before sending requests to LLM providers. |
| **Low** | **PR #4959**: Retry after delays too short for rate limits | *(self‑fix)* – fix: add one second to retry after delays | Adds a small buffer to match actual rate limit windows. |

All reported bugs have associated fix PRs, indicating active maintenance.

## Feature Requests & Roadmap Signals
The following open PRs introduce new features or enhancements:

- **#4937** – [feat: add one‑click Deploy to Render support](https://github.com/HKUDS/nanobot/pull/4937)  
  Adds a Render Blueprint for one‑click deployment with persistent session history and memory. Likely to be merged after review.

- **#4958** – [Improve zh‑TW Traditional Chinese locale](https://github.com/HKUDS/nanobot/pull/4958)  
  Improves translation quality; low risk, likely accepted soon.

- **#4953** – [feat(webui): support native folder picker bridges](https://github.com/HKUDS/nanobot/pull/4953)  
  Enables external native hosts to provide a folder‑picker UI bridge for the WebUI.

- **#4951** – [feat(web): add Nimble search provider](https://github.com/HKUDS/nanobot/pull/4951)  
  Adds Nimble as a new web search provider following existing REST patterns.

These features align with improving deployment, localization, WebUI interactions, and search capabilities. The Render deployment and Nimble search are likely candidates for the next minor release.

## User Feedback Summary
No direct user feedback (comments, reactions, or personal reports) was recorded in issues or PRs today. The lack of discussion on the four new feature PRs and the single bug report suggests either low community engagement or that the changes are straightforward and uncontroversial. The only expressed pain point is the subagent UI visibility loss (issue #4948), which has a corresponding fix.

## Backlog Watch
No long‑standing unanswered issues or PRs were updated today. All items in the backlog are recent (within the last 24–48 hours). Maintainers are advised to review **PR #4937** (Render deploy) and the high‑priority bug fixes (#4954, #4957, #4960) for prompt merging to keep the project stable and responsive.

---

*Generated from GitHub activity on 2026-07-17.*  
*Data source: [github.com/HKUDS/nanobot](https://github.com/HKUDS/nanobot)*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-17

## Today's Overview

The project remains exceptionally active, with **50 issues** and **50 pull requests** updated in the last 24 hours—of which **42 issues and 44 PRs remain open**. Only **8 issues** and **6 PRs** were closed or merged today. Activity spans multiple components (agent core, gateway, desktop, CLI, providers, tools) and includes a mix of bug fixes, feature implementations, and community-submitted enhancements. No new releases were published today, but the volume of ongoing work suggests a near-term patch or minor release is likely. The community continues to engage strongly, especially around provider integration (Anthropic, OpenAI-compatible, Z.ai) and session/cross-platform usability.

---

## Releases

**No new releases** were published today. The latest available version remains the prior release (v2026.7.7.x line); the project appears to be in a development cycle focused on accumulating fixes and features for a future release.

---

## Project Progress

Today **6 pull requests were merged/closed** (all closed, some merged), and **8 issues were closed**. Notable merged/closed contributions include:

- **PR #53222 (merged):** `fix(memory): gate auto recall + scrub inline-echoed recall block` — Fixes a memory context leak where internal recall blocks could appear in customer-facing replies. This had been flagged as P2 with multiple risk labels.
- **PR #65634 (merged):** `feat(slack): render structured worker progress` — Adds bounded progress cards and sanitized preview links for Slack gateway runs, improving user experience on that platform.
- **PR #65925 (merged):** `fix(cli): only mark speech-to-text messages as voice input` — Corrects voice mode labelling so that non-STT messages are not incorrectly marked as voice input.
- **Issues #61284 & #54489 (closed):** Dashboard WebSocket regression and `hermes setup` disabling `basic` plugin were confirmed fixed.
- **Issue #52470 (closed):** Dashboard auto-restart silent failure due to environment variable inheritance was resolved.

Additionally, several duplicate and low-value issues were closed (e.g., #66022, #66019). The “cron session context isolation” fix (PR #43370) remains open but is under active discussion.

---

## Community Hot Topics

### 1. [Feature] Claude Agent SDK model provider with subscription OAuth (#25267)
- **Comments:** 11 | **👍:** 41  
- **Summary:** Users want to run Hermes with Claude while staying on their existing Claude subscription (billed via OAuth/Codex-style), avoiding double payment (subscription + per-token API).  
- **Link:** [NousResearch/hermes-agent Issue #25267](https://github.com/NousResearch/hermes-agent/issues/25267)  
- **Analysis:** This is the most popular open feature request, reflecting widespread demand for seamless integration with consumer Claude subscriptions. It touches on provider architecture, OAuth, and billing models.

### 2. [Bug] Hermes sends extremely large prompts to local OpenAI-compatible models (#61265)
- **Comments:** 6 | **👍:** 1  
- **Summary:** Large prompts cause multi-minute stalls across model sizes, even without model swapping.  
- **Link:** [NousResearch/hermes-agent Issue #61265](https://github.com/NousResearch/hermes-agent/issues/61265)  
- **Analysis:** A performance-critical bug affecting users running local models. Has `P2` priority and a `needs-decision` label; no fix PR yet.

### 3. [Feature] Cross-platform session context sharing (CLI ↔ Telegram) (#4335)
- **Comments:** 6 | **👍:** 1  
- **Summary:** Users want the same agent session to be accessible from multiple platforms (CLI, Telegram, etc.) without losing context.  
- **Link:** [NousResearch/hermes-agent Issue #4335](https://github.com/NousResearch/hermes-agent/issues/4335)  
- **Analysis:** A long-standing request (opened March 31) that would greatly improve multi-platform UX. No maintainer response visible.

### 4. [Bug] Desktop App creates new session on every message with non-default profile (#65384)
- **Comments:** 4 | **👍:** 0  
- **Summary:** Desktop app connected to a remote `hermes serve` backend fails to maintain session continuity for non-default profiles.  
- **Link:** [NousResearch/hermes-agent Issue #65384](https://github.com/NousResearch/hermes-agent/issues/65384)  
- **Analysis:** A fresh P2 bug (opened yesterday, updated today) that breaks a core use case. No fix PR identified.

---

## Bugs & Stability

### Critical / High Severity (P2)

| Issue | Component | Summary | Fix PR? |
|-------|-----------|---------|---------|
| #65384 | Desktop | Desktop creates new session per message for non-default profile | No |
| #65787 | Agent / MCP | MCP keepalive uses `list_tools()` – O(tool-count) timeout + reconnect loop | No |
| #53002 | Provider / Z.ai | 429/code 1305 persists on `chat/completions` path; previous fix only covered Anthropic adapter | No |
| #65650 | CLI | `/model` picker slow (~5s) when custom providers have `discover_models: true` | No |
| #65854 | CLI | `uninstall` can delete other packages from shared Python folder | No |
| #58745 | Agent / Compression | `context_length` semantics conflict leads to per-turn compression loop | No |
| #61265 | Agent / Tools | Large prompts cause multi-minute stalls on local models | No |
| #53491 | Security / Skills | `guard_agent_created` off by default; `ask` policy leaks findings | No |

### Medium / Low Severity (P3)

- #54115 – BG Review OOM with local llama.cpp server (updated today)
- #15985 – Skills forgotten when using Gemma 4 via Ollama (updated today)
- #65746 – MoA/local calls crash after 30s due to `float infinity to integer` (updated today)
- #58345 – xAI grok-4.3 drops optional multiline string args in MCP calls (updated July 16)
- #66008 – Desktop “Read aloud” times out on long replies (regression)
- #66012 – Desktop ignores per-profile TTS/voice config on Windows
- #65949 – Google Cloud Vertex provider not recognized in `hermes doctor`
- #66019 – `hermes -z` ignores `terminal.backend` (sandbox bypass) – closed as duplicate

### Notable Fix PRs Submitted Today

- **#65935** – `fix(desktop/windows): free all venv holders on Update hand-off` (P2, Windows-specific)
- **#65897** – `fix(desktop): retain shown notifications so clicks reach their handlers` (P3, Windows)
- **#66029** – `fix(gateway): reply to first-contact /start with a welcome instead of silence` (P2)
- **#66036** – `fix(delegation): enforce child authority and completion contract` (P2)
- **#66035** – `fix(acp): honor configured tool and turn budgets` (P4)
- **#66033** – `perf(desktop): kill the layout-thrash cascade on session switch` (P2)
- **#66038** – `fix(coding-context): bound the post-kill cleanup in the Windows git probe`

---

## Feature Requests & Roadmap Signals

The following features are most likely to influence the next minor release:

1. **Claude subscription OAuth provider** (#25267) – Strong community demand (41 👍). Implementation would require new provider adapter and subscription auth flow.
2. **Cross-platform session sharing** (#4335) – High utility for multi-platform users. Would touch the gateway and session store architecture.
3. **Multi-gateway connections with per-gateway tabs in desktop** (#45779) – 4 👍. Adds ability to manage multiple remote backends from one desktop UI.
4. **`skip_parameters` config for auxiliary tasks** (#26881) – Helps users working with OpenAI-compatible proxies that reject standard parameters.
5. **Context-aware orchestrator model routing** (#66020) – Agent self-routes tasks to optimal models. Newly filed today with `needs-decision` label.
6. **`models_url` in custom providers** (#65481) – Decouples model discovery from inference base URL, useful for proxy setups.
7. **Structured session tracing** (#6741) – Add start/end timestamps to session traces for profiling.
8. **Plugin `on_status_bar_render` hook** (#8642) – Allows plugins to contribute TUI status bar fragments.

PRs merged today also indicate progress on:
- **Slack worker progress rendering** (#65634) – Likely to ship soon.
- **OpenAI image generation improvements** (#65323) – Configurable endpoint, credential routing, and proxy bypass (fixes #65309).
- **Unreal Engine MCP companion skill** (#65989) – Experimental, but signals growing ecosystem integration.

---

## User Feedback Summary

The community is actively using Hermes in a variety of deployment scenarios and reports both satisfaction and frustration.

**Satisfaction signals:**
- Continued high level of feature requests and PRs shows strong adoption.
- Multiple fixes for desktop and gateway stability are being contributed by the community themselves.
- Users appreciate platform support (Discord, Telegram, Slack, Desktop) and are requesting more integrations.

**Pain points expressed:**
- **Desktop session loss** with non-default profiles (#65384) is a significant blocker for remote backend users.
- **Large prompt performance** (#61265) remains unresolved and affects local model deployments.
- **MCP keepalive design** (#65787) causes repeated timeouts with large tool servers.
- **Uninstall safety** (#65854) – risk of accidentally deleting unrelated packages.
- **Voice/TTS configuration** ignores per-profile settings (#66012) on Windows.
- **Model picker latency** (#65650) makes model switching cumbersome.
- **Security defaults** for skills (#53491) leave new users vulnerable to persistent unsafe agent-created skills.
- **Billing double payment** (#25267) – Claude users feel penalised by API-only mode.

Overall sentiment is constructive; users are willing to file detailed reports and even produce fixes. Several reports are AI-generated (e.g., #58345), indicating a sophisticated user base that leverages Hermes itself.

---

## Backlog Watch

The following issues and PRs have been open for an extended period without visible maintainer resolution or decision:

1. **#25267** – Claude SDK provider (opened May 13, 11 comments, 41 👍) – Highly voted but no maintainer response.
2. **#4335** – Cross-platform session sharing (opened March 31, 6 comments) – No maintainer response.
3. **#6741** – Structured session tracing (opened April 9, 3 comments) – No maintainer response.
4. **#8642** – Plugin TUI status bar hook (opened April 12, 2 comments) – No maintainer response.
5. **#15985** – Skills forgotten with Gemma 4 via Ollama (opened April 26, 5 comments) – Updated today but no resolution.
6. **#43370** – Fix cron session context isolation (PR opened June 10, multiple sweeper labels) – Still open, needs decision.
7. **#50472** – Restore `memory_monitor` startup/shutdown wiring (PR opened June 21) – No maintainer review.
8. **#53392** – Desktop GUI model picker wrong provider name for kimi-coding-cn (PR opened June 27) – Needs decision.
9. **#56770** – Prevent crash from unhandled exceptions in fatal error handlers (PR opened July 2, P2) – Not yet merged.

These items represent areas where community investment is high but maintainer bandwidth may be limited. Prompt attention could reduce frustration and accelerate feature parity with competing agents.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

## PicoClaw Project Digest – 2026-07-17

### 1. Today’s Overview
Project activity remained moderate, with 2 issues and 9 pull requests updated in the last 24 hours. However, no pull requests were merged or closed today, indicating a pause in feature integration. All 9 open PRs are either dependency bumps (7) or feature branches (2) that have remained untouched for several days. The single open bug (#3195) has been stale for over two weeks, while a second bug (#3260) was closed without maintainer comment. Overall, the project is in a maintenance-heavy phase with growing community contributions waiting for review.

### 2. Releases
No new releases were published today. The latest available version remains **picoclaw 0.3.1** (build 2026-07-03).

### 3. Project Progress
**No pull requests were merged or closed today.** The only code-related activity is an open localisation PR (#3261) and two stale feature PRs (#3118, #3115). The eight dependency-bump PRs (e.g., #3238, #3237, #3236, #3235, #3262, #3263) are pending review but do not introduce functional changes.

### 4. Community Hot Topics
The most active discussion is around **Issue #3195** ([sipeed/picoclaw#3195](https://github.com/sipeed/picoclaw/issues/3195)) – a bug report about OpenAI GPT not working on NanoKVM with the default configuration. This issue has **3 comments** and has been open since June 30. The user followed the official documentation but received errors when trying to configure `gpt-5.4`. The underlying need is clearer documentation or configuration fixes for the new NanoKVM 2.4.0 integration.

All other issues and PRs have zero comments or reactions, indicating limited community engagement on other topics today.

### 5. Bugs & Stability
| Issue | Status | Severity | Summary |
|-------|--------|----------|---------|
| [#3195](https://github.com/sipeed/picoclaw/issues/3195) | Open / Stale | **Medium** – OpenAI GPT fails on NanoKVM; blocks a key use case. No fix PR exists. |
| [#3260](https://github.com/sipeed/picoclaw/issues/3260) | Closed | **Low** – ARM64 launcher missing on Raspberry Pi; likely resolved by the user or a silent fix. |

**#3195** is the more concerning bug because it affects a new hardware platform (NanoKVM) and has no associated pull request. The issue remains unsolved for over two weeks, which may frustrate early adopters.

### 6. Feature Requests & Roadmap Signals
- **Localisation** – PR [#3261](https://github.com/sipeed/picoclaw/pull/3261) adds Traditional Chinese (zh-TW) translations. This signals growing international demand and could be merged soon.
- **Remote Agent Mode** – Stale PR [#3118](https://github.com/sipeed/picoclaw/pull/3118) proposes a WebSocket remote mode for the `picoclaw agent` command. If revived, this would enable network-attached Pico devices, a significant roadmap feature.
- **Media Extraction Fix** – Stale PR [#3115](https://github.com/sipeed/picoclaw/pull/3115) fixes a session-history corruption bug when tools return base64 data URLs. Though a bug fix, it’s also a stability improvement likely for the next minor release.

Given the current activity, the next version (0.3.2 or 0.4.0) may include the localisation PR and one or both of the stale feature PRs if maintainers review them.

### 7. User Feedback Summary
- **Pain Point:** Setup complexity on specialised hardware. In [#3195](https://github.com/sipeed/picoclaw/issues/3195), the user followed the official docs but could not connect to OpenAI GPT on NanoKVM. This suggests either a documentation gap or a runtime incompatibility.
- **Satisfaction:** The closed bug [#3260](https://github.com/sipeed/picoclaw/issues/3260) was resolved (likely by the user), indicating that ARM64 support works after manual intervention.
- **General Sentiment:** Minimal user feedback overall, but the lack of merge activity and stale issues may indicate a bottleneck in maintainer bandwidth.

### 8. Backlog Watch
Several items require maintainer attention:

| Item | Type | Age | Why it matters |
|------|------|-----|----------------|
| [#3195](https://github.com/sipeed/picoclaw/issues/3195) | Bug | 17 days | Blocks NanoKVM + OpenAI use case; no response from maintainers. |
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) | Feature PR | 35 days | Remote WebSocket agent mode – high value, but stale since June 12. |
| [#3115](https://github.com/sipeed/picoclaw/pull/3115) | Fix PR | 35 days | Prevents session history corruption; critical for tool users. |
| [#3238–#3235](https://github.com/sipeed/picoclaw/pulls?q=is%3Apr+author%3Adependabot+is%3Aopen) | Deps bumps | 7 days | Outdated dependencies may cause build or security issues if left too long. |

All open PRs and issues are waiting for maintainer review. The project would benefit from a triage session to merge or close stale items.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-17

## 1. Today’s Overview
NanoClaw is in a high-activity phase. Over the last 24 hours, 4 issues were updated (3 open, 1 closed) and 19 pull requests were touched (16 open, 3 merged/closed). Three PRs were merged, fixing a critical WhatsApp channel collision and improving documentation. Community discussion is focused on a misleading rate-limit logging bug and a silent adapter startup failure, while several feature PRs (LLM fallback, new Dial channel) signal roadmap momentum. No new releases were published today.

## 2. Releases
*None.* No new versions were tagged in the reporting period.

## 3. Project Progress (Merged/Closed PRs Today)
Three PRs were merged or closed:

- **[#2913] fix(whatsapp-cloud): register bridge under distinct 'whatsapp-cloud' instance key** (merged)  
  *Resolves the WhatsApp Cloud collision with native WhatsApp by assigning a unique adapter key.*  
  https://github.com/nanocoai/nanoclaw/pull/2913

- **[#2914] docs(add-whatsapp-cloud): document webhook route + state-namespace migration** (merged)  
  *Follow-up documentation for the WhatsApp Cloud fix.*  
  https://github.com/nanocoai/nanoclaw/pull/2914

- **[#3061] [follows-guidelines] Custom** (closed – likely placeholder/cleanup)  
  https://github.com/nanocoai/nanoclaw/pull/3061

The corresponding issue **[#2911]** (WhatsApp Cloud collision) was also closed.  
https://github.com/nanocoai/nanoclaw/issues/2911

## 4. Community Hot Topics

| Item | Type | Comments | Reactions | Key Discussion |
|------|------|----------|-----------|----------------|
| [#3016] `rate_limit_event` logged as quota error even when allowed | Issue | 2 | 0 | User reports 82 occurrences in a week, all on successful turns. Underlying need: distinguish real quota exhaustion from transient rate limits. |
| [#2916] “hi” | Issue | 2 | 0 | Low-signal “hello” post – likely a test or new-user greeting. No substance. |
| [#3069] Host-orchestrated fallback to backup LLM provider | PR (open) | – | – | Feature PR with detection logic; community may weigh in on design. |
| [#3057] Automatic Claude↔Codex quota fallback + channel adapters | PR (open) | – | – | Another LLM fallback approach, overlapping with #3069; possible consolidation needed. |

**Analysis:** The rate-limit logging annoyance (#3016) is the most active discussion. Users expect meaningful error logs, not false positives. Both LLM-fallback PRs suggest the community and maintainers are prioritizing resilience against provider usage limits.

## 5. Bugs & Stability

### Critical (fix in progress)
- **[#3064] Channel adapter startup failure swallowed** – If a channel’s `setUp()` fails, `initChannelAdapters()` only logs the error; the host reports “running” but is deaf.  
  *Fix PR: [#3067] (open) – propagates startup failure as a fatal error.*  
  https://github.com/nanocoai/nanoclaw/issues/3064  
  https://github.com/nanocoai/nanoclaw/pull/3067

### High
- **[#3016] rate_limit_event logged as quota error** – Misleading log floods subscription installs with false errors. Not a crash, but causes user confusion.  
  No dedicated fix PR yet; likely related to PR [#2965] (not in today’s data).  
  https://github.com/nanocoai/nanoclaw/issues/3016

### Medium (open PRs)
- **WhatsApp sender identity divergence** (PR [#3070]) – Baileys and Cloud paths assign different user IDs for the same phone number.  
- **Scheduled task cross-session visibility** (PR [#3068]) – Task tools give inadequate feedback across sessions in the same agent group.  
- **Container zombie process accumulation** (PR [#3060]) – Missing `--init` flag prevents PID 1 from reaping zombies.  
- **Signal image attachment path** (PR [#2695]) – Container can’t read host path for inbound images.  
- **Signal read receipts** (PR [#3062]) – Senders never see messages marked read.  
- **Loopback webhook authentication** (PR [#3065]) – Security vulnerability (CWE-306) on forwarded-gateway server.  
- **Test pollution from abandoned poll loops** (PR [#2851]) – Stale loops steal messages from later tests.

### Resolved
- **[#2911] WhatsApp Cloud collision** – fixed by PR [#2913] (merged).

## 6. Feature Requests & Roadmap Signals

Several substantial feature PRs are open, indicating near-term roadmap priorities:

| Feature | PR | Status |
|---------|----|--------|
| Host-orchestrated LLM fallback (Claude → backup) | [#3069] | Open |
| Agent-group‑level Claude ↔ Codex quota fallback + channels | [#3057] | Open |
| Unify approval holds under one lifecycle contract | [#3040] | Open |
| Add Dial channel (SMS + AI voice calls) – picker/skills | [#3050] | Open |
| Add Dial channel adapter (core integration) | [#3041] | Open |

**Prediction:** At least one LLM-fallback mechanism (likely combining ideas from #3069 and #3057) and the Dial channel integration are strong candidates for the next minor release. The approval lifecycle unification (#3040) may also land if testing completes.

## 7. User Feedback Summary

- **Pain point (logging):** “Every rate_limit_event is logged as a quota error, even when the status is ‘allowed’” (#3016). User *glifocat* reports 82 instances on perfectly normal turns – logs are noise.
- **Pain point (reliability):** “Channel adapter that fails to start is swallowed … host reports healthy but runs deaf” (#3064). User *plongth* highlights a silent failure mode that makes debugging difficult.
- **Satisfaction (responsiveness):** The swift merge of the WhatsApp Cloud collision fix (#2913 → closed) and its companion docs (#2914) shows maintainers are responsive to high-impact bugs.
- **Use case diversity:** PRs for Signal read receipts (#3062), Dial channel (#3041, #3050), and WhatsApp improvements indicate a community deploying across multiple messaging platforms.

## 8. Backlog Watch

Long‑standing issues and PRs that remain open and may require maintainer attention:

| Item | Age | Last Update | Description |
|------|-----|-------------|-------------|
| [#2695] Fix Signal image attachment path | Since Jun 6 | Jul 16 | Container can’t read inbound Signal images; fix PR open but stalled. |
| [#2851] Fix test abandoned poll loops | Since Jun 24 | Jul 16 | Test infrastructure bug polluting CI runs; fix PR needs review. |
| [#2798] Expand CHANGELOG for v2.1.17 | Since Jun 17 | Jul 16 | Documentation PR – low urgency but should be merged before next release. |
| [#2916] “hi” | Since Jul 2 | Jul 16 | Likely spam; should be closed or labelled appropriately. |

*All links are in the `nanocoai/nanoclaw` repository (https://github.com/nanocoai/nanoclaw).*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-17

## 1. Today's Overview
Project activity is minimal today, with only one new issue and no pull requests or releases. The sole development signal is a critical crash bug affecting aarch64 Linux users. The repository appears stable in terms of routine contributions, but the reported severity of the bug suggests a need for urgent maintainer attention. Overall project health is currently neutral but skewed by a single high-impact stability concern.

## 2. Releases
No new releases were published in the last 24 hours. The latest available version remains **v2026.5.29**.

## 3. Project Progress
No pull requests were merged or closed today. No feature advancements, code fixes, or documentation improvements were recorded.

## 4. Community Hot Topics
The only active discussion is around the single open issue:

- **[Issue #976: SIGSEGV on every inbound Telegram message — inbound worker thread spawned with a ~512 KB stack overflows](https://github.com/nullclaw/nullclaw/issues/976)**  
  *Author: wonhotoss | Created: 2026-07-16 | Updated: 2026-07-16 | Comments: 1*  
  The issue describes a segfault on aarch64 Linux when nullclaw receives any Telegram message. The user notes that the crash happens consistently and causes a systemd service crash-loop, dropping every incoming message. The single comment (likely from the author or a maintainer) does not yet indicate a fix or root-cause analysis. The underlying need is **reliability for Telegram gateway functionality**, which is a core use-case for NullClaw.

No other issues or PRs have any comments or reactions.

## 5. Bugs & Stability
One critical bug was reported today:

- **Issue #976** (Severity: **Critical**) — A SIGSEGV crash on every inbound Telegram message on aarch64 Linux. The stack overflow caused by a ~512 KB thread stack suggests a misconfiguration or regression in threading code for that architecture. The crash prevents the gateway from processing any messages, essentially breaking Telegram integration for affected users. No associated fix PR exists yet.  
  **Impact**: High – message loss, service unavailability, poor user experience.  
  **Urgency**: Immediate – maintainer response needed to triage and patch.

No other stability issues were reported.

## 6. Feature Requests & Roadmap Signals
No feature requests or roadmap signals were recorded today. The community focus is entirely on bug resolution rather than new capabilities.

## 7. User Feedback Summary
The only user feedback from this period is captured in Issue #976. The user (wonhotoss) expresses clear dissatisfaction: the gateway is unusable on aarch64, messages are silently dropped, and the crash-loop behavior worsens the experience. The pain point is **system-level reliability on ARM hardware**, a platform increasingly common in low-power/home-server deployments. There are no expressions of satisfaction or praise in today’s data.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified. Issue #976 is recent (less than 48 hours old) and already has attention, but it remains unassigned and without a fix pull request. The maintainer should prioritize this issue to avoid it turning into a stale backlog item. No other open issues or PRs beyond #976 exist in the dataset.

---

*Generated from GitHub data for nullclaw/nullclaw on 2026-07-17.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-17

## Today’s Overview
Activity remained high with **18 issues** and **39 PRs** updated in the last 24 hours. The project is deep in the *Reborn* transition: three closed PRs shipped model‑selection/cost tracking (#6111), an OAuth conformance suite (#6114), and an onboarding/NUX demo (#5565). At the same time, a critical OAuth lifecycle fix (#6130) was applied and then **reverted** (#6166) for reconsideration, signalling ongoing tension between fast iteration and stability. No new releases were published. The *canary* signal‑reporting pipeline is being hardened (#6171), and the **god‑crate** refactoring (#6168) remains the largest architectural item.

## Releases
*None* – no new versions were cut in this window.

## Project Progress (Merged/Closed PRs)
**11 PRs** were closed or merged in the past day. Standout items:

- **#6111** – Feat(reborn): WebChat v2 model selection + per‑run usage/cost. Ships two key capabilities (model picker and cost display) for the regular WebChat API, reusing backend plumbing.
- **#6114** – Test(auth): shared OAuth‑flow conformance suite over fake and durable `AuthFlowManager`. Closes the disjoint‑suite gap, preventing behavioral divergence.
- **#6130** – Fix(auth): OAuth flow‑lifecycle hygiene (supersede‑on‑start, durable PKCE verifiers, expiry‑honest projections). *Merged then immediately reverted by #6166 for further review.*
- **#5565** – Feat(gateway): onboarding/NUX demo with intent handoff, OAuth entry, chat‑first workspace, and mock‑backed Vercel demo (13 self‑contained commits).
- **#6115** – Build(deps): 25 dependency updates across the workspace.
- **#6166** – OAuth Reversion: reverts #6130 completely, restoring previous OAuth flow‑lifecycle behaviour.

## Community Hot Topics
| Item | Type | Comments | Description |
|------|------|----------|-------------|
| [#6168](https://github.com/nearai/ironclaw/issues/6168) | Issue | 2 | Shrink `ironclaw_reborn_composition` god‑crate from 24% → ~10% of production code. Charter‑bound to be assembly‑only but has accreted >156k LOC. Core architectural debt. |
| [#6155](https://github.com/nearai/ironclaw/issues/6155) | Issue | 2 | Follow‑up messages receive no response after a failed run (P2). Chat becomes unresponsive without error feedback. |
| [#6126](https://github.com/nearai/ironclaw/issues/6126) | Issue | 2 | First message in new chat has no loading/streaming state. UI appears frozen. |
| [#6127](https://github.com/nearai/ironclaw/issues/6127) | Issue | 2 | Routine incorrectly displays “Previous run still in progress” on first execution. |
| [#4471](https://github.com/nearai/ironclaw/issues/4471) | Issue | 1 | Track Reborn runtime decomposition – `runtime.rs` exceeds 3,000‑line budget. |
| [#6158](https://github.com/nearai/ironclaw/issues/6158) | Issue | 1 | Request to add zh‑TW Traditional Chinese localization (currently only zh‑CN). |
| [#6164](https://github.com/nearai/ironclaw/issues/6164) | Issue (closed) | 1 | Slack connection epoch state machine is redundant with auth‑flow layer; active bug source. |

The highest‑engagement issues centre on **user‑visible regressions** (no response after failure, missing loading indicators) and the **ongoing architectural extraction** of the monolithic composition crate.

## Bugs & Stability
**Ranked by severity:**

- **🔴 High – #6170** – *Remove user access to file system via shell*. On multi‑tenant instances, users can ask the agent to run arbitrary shell commands (e.g., `ls -all`) unbounded to the user’s workspace. **Security vulnerability** – no fix PR visible yet.
- **🟡 Medium – #6155** – *Follow‑up messages receive no response after a failed run*. Conversation deadlock after a model‑provider error. No known fix PR.
- **🟡 Medium – #5602** – *Can’t connect Slack from chat*. Agent reports connection success but DM returns pairing code instead of completing the flow. Open since 2026‑07‑03.
- **🟢 Low – #6126** – *No loading/streaming state on first message*. Blank UI until full response appears.
- **🟢 Low – #6127** – *“Previous run still in progress” shown on first execution*. Status panel contradiction.
- **🟢 Low – #6149** – *Workspace download failures silently ignored*. Error caught with no user feedback.
- **🟢 Low – #6145** – *Toasts not dismissible, 2.6s auto‑dismiss, no pause on hover*.
- **🟢 Low – #6117** – *Workspace displays untranslated region names and raw byte sizes* (fixed by already‑closed issue).

Note: the OAuth lifecycle fix (#6130) was reverted, meaning the bugs it addressed are **still live** on `main`; a revised fix is expected.

## Feature Requests & Roadmap Signals
Several user‑facing and infrastructure features surfaced:

| Issue/PR | Description | Likely Impact |
|----------|-------------|---------------|
| [#6158](https://github.com/nearai/ironclaw/issues/6158) | Add zh‑TW Traditional Chinese locale | UI i18n expansion – likely to land in next minor release. |
| [#6146](https://github.com/nearai/ironclaw/issues/6146) | Add theme selection controls to Appearance settings | Low effort, high UX gain – near‑term candidate. |
| [#6142](https://github.com/nearai/ironclaw/issues/6142) | Serve WebUI at root path instead of `/v2` | Renaming/deprecation signal as v1 is retired. |
| [#6143](https://github.com/nearai/ironclaw/issues/6143) | Promote `ironclaw-reborn` CLI to `ironclaw` | Product naming consolidation post‑Reborn. |
| [#6160](https://github.com/nearai/ironclaw/issues/6160) | Build Reborn binaries for multiple CPU architectures | Release pipeline enhancement – needed for cross‑platform distribution. |
| [#6159](https://github.com/nearai/ironclaw/pull/6159) | Telegram channel extension (Reborn) | New entrypoint – admin bot, WebGeneratedCode pairing, DM flow. |
| [#6162/6163](https://github.com/nearai/ironclaw/pull/6162) | Agent workspace redesign + chat‑first onboarding (split PRs) | Major UI overhaul – design system application. |
| [#6157](https://github.com/nearai/ironclaw/pull/6157) | Terminal UI (ratatui) + service install (`launchd`/`systemd`) | Headless deployment story for Reborn. |

The most likely features to ship in the next version are **Telegram integration** (#6159), **multi‑arch CI builds** (#6160), and the **workspace redesign** (#6162/6163). The CLI rename (#6143) and root‑path serving (#6142) are blockers for v1 retirement.

## User Feedback Summary
Reported pain points from the community and testers:

- **Unresponsive chat after failures** (#6155) – the conversation becomes a black hole with no error message or recovery path.
- **Missing visual feedback on first message** (#6126) – users think the app is frozen.
- **Slack connection flow never completes** (#5602) – agent returns a silent pairing code instead of finalising the integration.
- **Workspace download failures invisible** (#6149) – no toast or error message.
- **Inconsistent “Previous run in progress”** (#6127) – confusing status for new users.
- **No per‑user secret management in Admin UI** (#6118, closed) – administrators lack UI for provisioning credentials.
- **No zh‑TW locale** (#6158) – users preferring Traditional Chinese have to fall back to Simplified Chinese or English.

Overall, satisfaction with feature velocity is high (Telegram, TUI, workspace redesign all in flight), but **core reliability bugs** are eroding trust in the chat experience.

## Backlog Watch
Items that have been open for an extended period without resolution:

| Item | Open Since | Description | Status |
|------|------------|-------------|--------|
| [#4471](https://github.com/nearai/ironclaw/issues/4471) | 2026‑06‑04 | Track Reborn runtime decomposition (`runtime.rs` > 3k lines) | 1 comment; no PR linked. |
| [#5602](https://github.com/nearai/ironclaw/issues/5602) | 2026‑07‑03 | Can’t connect Slack from chat | 1 comment; remains unaddressed. |
| [#5978](https://github.com/nearai/ironclaw/pull/5978) | 2026‑07‑11 | Require read‑before‑edit and reject stale edits in reborn coding tools (stack 3/4) | 0 comments; open 6 days. |
| [#6144](https://github.com/nearai/ironclaw/issues/6144) | 2026‑07‑16 | Daily failure taxonomy 2026‑07‑16 | Recurring meta‑issue; no actionable resolution. |

**Maintainer attention needed** on #4471 (the god‑crate decomposition is actively blocking further extraction – #6168 is the current proposal) and #5602 (Slack connectivity is a core integration that hasn’t worked for two weeks).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-17

## 1. Today's Overview
The project shows strong development momentum with **17 pull requests updated** in the last 24 hours, of which **14 were merged or closed** — a high merge rate indicating active feature work and bug fixing. Three issues were also updated, all with **stale** tags created in April; one was closed. No new official release was tagged, but the **release branch `Release/2026.7.16`** (PR #2344) was merged, effectively shipping a new version. The focus remains on the Cowork module (steer queue, attachments, scroll stability, Windows UI polish) and on stabilizing existing functionality.

## 2. Releases
No new version tags were published in the last 24 hours. However, the **release PR #2344** (`Release/2026.7.16`) was merged, which bundles the numerous fixes and features listed below. Users can expect a build with improved Cowork steer handling, Windows title bar support, folder context attachments, and several stability fixes. No migration notes are required.

## 3. Project Progress
The following merged/closed PRs (updated in the last 24h) advanced the codebase:

| PR | Area | Description |
|----|------|-------------|
| [#2343](https://github.com/netease-youdao/LobsterAI/pull/2343) | renderer, cowork | Refactored clipboard attachment extraction into a testable helper |
| [#2339](https://github.com/netease-youdao/LobsterAI/pull/2339) | renderer | Fixed update card header alignment and showed full titles in narrow sidebars |
| [#2329](https://github.com/netease-youdao/LobsterAI/pull/2329) | renderer, cowork | Prevented conversation scroll jumps during streaming by respecting manual scrolling |
| [#2289](https://github.com/netease-youdao/LobsterAI/pull/2289) | main | Cleared stalled compaction retry maintenance with regression tests |
| [#2292](https://github.com/netease-youdao/LobsterAI/pull/2292) | renderer, docs, main, cowork | Stabilized steer follow-up routing: added queued steer, replaced temporary sessions, scoped streaming state |
| [#2300](https://github.com/netease-youdao/LobsterAI/pull/2300) | renderer, cowork | Added attachment support in steer queue (files, images, text selections) with lightweight snapshots |
| [#2302](https://github.com/netease-youdao/LobsterAI/pull/2302) | renderer, cowork | Added a Windows-only branded title bar with native controls and moved sidebar actions into it |
| [#2310](https://github.com/netease-youdao/LobsterAI/pull/2310) | renderer, main, cowork | Added folder context attachments: paste/drop folders as prompt attachments, sent as paths to OpenClaw |
| [#2313](https://github.com/netease-youdao/LobsterAI/pull/2313) | renderer, cowork | Fixed queued steer submission to process only the selected item, preserving FIFO |
| [#2307](https://github.com/netease-youdao/LobsterAI/pull/2307) | renderer, cowork | Refined prompt modes: removed Plan Mode switch, moved Goal/Steer status bars, fixed queued steer follow-ups |
| [#1362](https://github.com/netease-youdao/LobsterAI/pull/1362) | cowork | Added ESC key support to close permission modal |
| [#1364](https://github.com/netease-youdao/LobsterAI/pull/1364) | cowork | Added model selector in the new task input toolbar (in addition to header) |
| [#1367](https://github.com/netease-youdao/LobsterAI/pull/1367) | scheduled-task | Added duplicate task name validation & detection |

**Key theme:** The Cowork module received extensive refinements — better queue management, attachment handling, UI streamlining, and platform-specific improvements.

## 4. Community Hot Topics
The most discussed items (by comment count) are all **stale** issues and PRs created in April, which received updates but no maintainer response:

- **[Issue #1361](https://github.com/netease-youdao/LobsterAI/issues/1361)** *(closed, 2 comments)*: User reported a Chinese localization issue — the "delete" button on custom agent pages shows English "delete" instead of Chinese. A fix was presumably merged (it's now closed), but the discussion highlights ongoing i18n gaps.

- **[Issue #1317](https://github.com/netease-youdao/LobsterAI/issues/1317)** *(open, 1 comment)*: Feature request to show keyboard shortcut hints (`<kbd>` badges) on sidebar buttons. The companion PR [#1318](https://github.com/netease-youdao/LobsterAI/pull/1318) has been open for 3 months.

- **[Issue #1319](https://github.com/netease-youdao/LobsterAI/issues/1319)** *(open, 1 comment)*: Request for skeleton loading in the session list to differentiate "loading" from "empty". Companion PR [#1320](https://github.com/netease-youdao/LobsterAI/pull/1320) is also open.

**Underlying need:** Users want a more polished, discoverable UI with clear feedback during loading states and consistent localization. The stale status suggests these improvements are lower priority for the maintainers.

## 5. Bugs & Stability
No new bug reports were filed in the last 24 hours. However, several **fixes were merged** today addressing previously reported issues:

- **Conversation scroll jumps** (#2329) — fixes auto-scroll during streaming interfering with manual scrolling. *Critical for live chat UX.*
- **Stalled compaction retry** (#2289) — prevents context maintenance from being left uncleared. *Medium severity (potential memory/resource leak).*
- **Steer follow-up routing** (#2292) — ensures follow-ups are correctly routed to active sessions. *High severity (functional breakage without this).*
- **Settings overlay persistence** (#1321) — modal overlays could remain after switching tabs, making UI appear read-only. *Medium severity.*
- **Duplicate scheduled task names** (#1367) — validation was missing, leading to silent failures. *Low severity but good hygiene.*

All these fixes have been merged, indicating good stability hygiene.

## 6. Feature Requests & Roadmap Signals
The most notable pending feature requests are the two skeleton loading and keyboard shortcut hints (see #1317, #1319). These PRs are fully implemented but await maintainer review. Additionally, the recent merged PRs signal the **next version's direction**:

- **Platform-aware UI** (#2302): Windows title bar with app branding — likely a stepping stone for cross-platform windowing improvements.
- **Folder context attachments** (#2310): Allows users to drop entire folders as context — a **power-user feature** that enhances code/file analysis workflows.
- **Steer queue attachment & refinement** (#2300, #2307, #2313): Codify a "Codex-like" interaction model where users can queue multiple follow-ups with attachments during active turns.

Given the rate of Cowork development, the next minor release will likely include these steer queue enhancements, Windows title bar, and folder attachments, while the older UI polish requests may be deferred.

## 7. User Feedback Summary
User feedback is limited but reveals consistent pain points:

- **Localization gaps** (#1361): The UI still has untranslated English strings (e.g., "delete") even in Chinese locales, hurting usability for non-English speakers.
- **Missing affordances** (#1317, #1319): Users expect keyboard shortcut hints and proper loading states — signs that the app's information density and responsiveness need refinement.
- **Workflow friction** (implied by multiple steer fixes): Multiple PRs aim to make the "steer" (follow-up) experience smooth — users likely experienced dropped or misrouted messages.

Overall satisfaction appears acceptable (no major complaints), but the stale community PRs suggest a **moderate backlog of user-requested improvements** that have not been merged.

## 8. Backlog Watch
The following items have been **open for 3+ months without maintainer response** and are at risk of being overlooked:

| Item | Type | Created | Last Update | Notes |
|------|------|---------|-------------|-------|
| [#1317](https://github.com/netease-youdao/LobsterAI/issues/1317) — Shortcut hint badges | Issue | 2026-04-02 | 2026-07-16 | PR [#1318](https://github.com/netease-youdao/LobsterAI/pull/1318) ready but unreviewed |
| [#1319](https://github.com/netease-youdao/LobsterAI/issues/1319) — Skeleton loading for sessions | Issue | 2026-04-02 | 2026-07-16 | PR [#1320](https://github.com/netease-youdao/LobsterAI/pull/1320) ready but unreviewed |
| [#1321](https://github.com/netease-youdao/LobsterAI/pull/1321) — Settings overlay fix | PR | 2026-04-02 | 2026-07-16 | Fix was merged? Actually open and stale — likely needs rebase |

The maintainer team is clearly active on internal branches (many PRs from `liuzhq1986`), but community contributions are accumulating. A review of these three PRs would unblock valuable UX improvements and encourage further community participation.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-17

## Today’s Overview
Project activity was low but focused, with no new issues opened in the last 24 hours and three pull requests closed/merged. A single patch release (`20260716.01`) was published. The merged PRs address both feature expansion (Kimi K3 provider support) and UX fixes (sandbox status feedback, fallback display). No regressions or critical bugs were reported, and the repository currently has zero open issues or pull requests, indicating maintainers are keeping the backlog well-managed.

## Releases
**New release: [`20260716.01`](https://github.com/moltis-org/moltis/releases/tag/20260716.01)**  
- No changelog details were provided in the data, but the release is associated with the three merged PRs below.  
- Breaking changes: None reported.  
- Migration notes: Not applicable.

## Project Progress
Three pull requests were merged today (2026-07-16):

- **PR #1155** – *Improve agent and sandbox status feedback*  
  Broadcasts external-agent session metadata once session IDs become available, persists external-agent history from full context requests, and treats installed external agents as available chat backends (includes Apple Container status).  
  → [PR #1155](https://github.com/moltis-org/moltis/pull/1155) (merged)

- **PR #1156** – *Add Kimi K3 provider support*  
  Adds Kimi K3 and Kimi K2.7 Code Highspeed to the Moonshot/Kimi Code model catalogs, updates reasoning-effort handling, provider setup defaults, config templates, documentation, and key-help links. Includes onboarding end-to-end coverage for Moonshot.  
  → [PR #1156](https://github.com/moltis-org/moltis/pull/1156) (merged)

- **PR #1154** – *fix(web): show direct mode when sandbox is unavailable*  
  When no real sandbox backend is available, the chat header now shows “direct” instead of “sandboxed”. The sandbox toggle and image selector are disabled when only non-isolated fallback execution is present. Includes E2E test coverage.  
  → [PR #1154](https://github.com/moltis-org/moltis/pull/1154) (merged)

---

**Summary of feature advancement:**  
- New AI provider integration (Kimi K3 / K2.7).  
- Better sandbox fallback UX in the web interface.  
- More reliable external-agent session handling and history persistence.

## Community Hot Topics
No issues or pull requests received comments or reactions in the last 24 hours. The project shows no active community discussion threads at this time. This may indicate a quiet period following recent releases, or that users are satisfied with the current stability.

## Bugs & Stability
- **PR #1154** fixed a UX bug where the sandbox status toggle incorrectly showed “sandboxed” when the backend was unavailable.  
- No new bugs, crashes, or regressions were reported in the last 24 hours.  
- Severity: Low (visual/UX error) – resolved in the same release.

## Feature Requests & Roadmap Signals
- **Kimi K3/K2.7 support** (PR #1156) is now merged, fulfilling a likely user request for broader Chinese AI model compatibility.  
- No explicit feature requests were filed today. Given the pattern of PRs, future iterations may focus on additional provider backends or sandbox isolation improvements.

## User Feedback Summary
No direct user feedback was captured in the data (issues or PR comments with zero reactions). The merged PRs suggest internal team priorities rather than external user bug reports. The absence of open issues implies that users are either not encountering problems or have not yet surfaced them on GitHub.

## Backlog Watch
- **Open issues:** 0  
- **Open pull requests:** 0  
Maintainers have cleared the backlog entirely. No items require immediate attention at this time. The project is in a healthy state with a clean slate.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-17

## 1. Today's Overview

CoPaw saw very high activity over the past 24 hours, with **43 issues updated** (23 open, 20 closed) and **46 PRs** (21 open, 25 merged/closed). No new release was cut, but the development team is clearly sprinting on the aftermath of the **v2.0.0.post2** launch. Many bug reports concern **Windows administrative privileges**, **timezone handling**, **session/memory consistency**, and **token consumption anomalies**. Several high‑impact fixes have already been merged or are under review, indicating a rapid response cycle. The community is actively reporting regressions, and the project is in a **stabilisation phase** with a focus on cross‑platform compatibility and reliability.

## 2. Releases

**None** – no new releases were published in the last 24 hours.

## 3. Project Progress

In the last 24 hours, **25 PRs were merged or closed**. Notable fixes and improvements:

- **UAC elevation fix** ([#6127](https://github.com/agentscope-ai/QwenPaw/issues/6127), open) – conditional elevation for Windows so VBS headless launchers stay windowless.
- **Streaming whitespace preservation** ([#6166](https://github.com/agentscope-ai/QwenPaw/issues/6166), merged) – missing spaces and line feeds in thinking blocks are now preserved during stream.
- **Session `updated_at` refresh** ([#6180](https://github.com/agentscope-ai/QwenPaw/issues/6180), merged) – chat list now correctly reorders after new messages on queue‑based channels.
- **Cron update field preservation** ([#6200](https://github.com/agentscope-ai/QwenPaw/issues/6200), merged) – `qwenpaw cron update` no longer resets fields like `max_concurrency`.
- **Docker timezone sync** ([#6192](https://github.com/agentscope-ai/QwenPaw/issues/6192), merged) – mounts host `/etc/localtime` and `/usr/share/zoneinfo` so container time matches host.
- **Dream schedule toggle** ([#6171](https://github.com/agentscope-ai/QwenPaw/issues/6171), merged) – adds explicit `dream_cron_enabled` switch to avoid unintended default scheduling.
- **Channel memory leak fixes** ([#6168](https://github.com/agentscope-ai/QwenPaw/issues/6168), merged) – bounds unbounded state sets in Mattermost, OneBot, XiaoYi channels.
- **E2E test adaption** ([#6185](https://github.com/agentscope-ai/QwenPaw/issues/6185), merged) – selectors updated for v2.0.0 UI redesigns.
- **CI coverage expansion** ([#6194](https://github.com/agentscope-ai/QwenPaw/issues/6194), merged) – nightly full sweep now includes console vitest test suite with coverage.
- **Tool registration unification** ([#6190](https://github.com/agentscope-ai/QwenPaw/issues/6190), open) – moves toward `@tool_descriptor` and `PluginApi.register_tool` for single‑source governance.
- **`nvidia-smi` probe removal** ([#6204](https://github.com/agentscope-ai/QwenPaw/issues/6204), open, first‑time contributor) – drops redundant `nvidia-smi` call in VRAM detection.
- **Windows `tasklist` timeout** ([#6203](https://github.com/agentscope-ai/QwenPaw/issues/6203), open, first‑time contributor) – bounds and hides process liveness probe.

Overall, the team is actively fixing **regressions introduced in v2.0.0** and hardening security, timezone, and memory handling.

## 4. Community Hot Topics

The most active issues (by comment count) reveal several pain points:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#6116](https://github.com/agentscope-ai/QwenPaw/issues/6116) (closed) | 6 | Doom loop: agent repeatedly calls the same tool in a single turn |
| [#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161) (open) | 5 | Windows update broke QwenPaw for non‑admin users – hangs on “Waiting for HTTP ready...” |
| [#6158](https://github.com/agentscope-ai/QwenPaw/issues/6158) (open) | 5 | Token usage anomaly: 28M tokens consumed from DeepSeek with no user interaction |
| [#6196](https://github.com/agentscope-ai/QwenPaw/issues/6196) (closed) | 5 | Container logs always UTC, ignoring configured `user_timezone` |
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) (open) | 5 | Messages silently dropped when session is busy – no queue, no error |
| [#6048](https://github.com/agentscope-ai/QwenPaw/issues/6048) (open) | 5 | Request for CIDR‑range support in whitelisted hosts |
| [#6129](https://github.com/agentscope-ai/QwenPaw/issues/6129) (closed) | 5 | Missing spaces and line feeds in streaming thinking blocks |

**Underlying needs**:
- Reliability of agent execution (doom loops, silent drops)
- Windows compatibility without admin elevation
- Transparency in token/API cost accounting
- Proper timezone handling across Docker and logs
- Network‑level flexibility (CIDR whitelist)

## 5. Bugs & Stability

**Critical bugs reported in the last 24 hours** (ranked by severity):

1. **Windows: forced admin elevation** ([#6161](https://github.com/agentscope-ai/QwenPaw/issues/6161), [#6169](https://github.com/agentscope-ai/QwenPaw/issues/6169)) – QwenPaw 2.0.0.post2 refuses to start without “Run as Administrator” after a Windows update. **Fix PR [#6127](https://github.com/agentscope-ai/QwenPaw/issues/6127) under review**.
2. **Session context loss on agent switch** ([#6074](https://github.com/agentscope-ai/QwenPaw/issues/6074)) – switching agents in console loses all conversation history.
3. **Unexplained token drain** ([#6158](https://github.com/agentscope-ai/QwenPaw/issues/6158)) – 28M tokens consumed without user activity; possible background process or cron misconfiguration.
4. **Docker timezone mismatch** ([#6188](https://github.com/agentscope-ai/QwenPaw/issues/6188)) – container always UTC; **fix [#6192](https://github.com/agentscope-ai/QwenPaw/issues/6192) merged**.
5. **QQ channel crash on local image paths** ([#6152](https://github.com/agentscope-ai/QwenPaw/issues/6152), closed) – Pydantic `AnyUrl` validation fails after upgrade.
6. **Desktop progressive render broken** ([#6202](https://github.com/agentscope-ai/QwenPaw/issues/6202)) – skill navigation list only shows 20 items, no scroll loading.
7. **`nvidia-smi` hang on startup** ([#6197](https://github.com/agentscope-ai/QwenPaw/issues/6197)) – frozen binary blocks when NVIDIA driver hangs. **Fix PR [#6204](https://github.com/agentscope-ai/QwenPaw/issues/6204) open**.
8. **Memory loss / truncation after v2.0 upgrade** ([#6148](https://github.com/agentscope-ai/QwenPaw/issues/6148), [#6155](https://github.com/agentscope-ai/QwenPaw/issues/6155)) – sessions forget prior context, `/compact` appears ineffective.
9. **Silent message drops** ([#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995)) – incoming messages are discarded when session is busy, no queue mechanism.
10. **Clash proxy conflict** ([#6156](https://github.com/agentscope-ai/QwenPaw/issues/6156)) – startup fails when Clash proxy is active.

Several of these have associated fix PRs in the pipeline, showing a responsive maintainer team.

## 6. Feature Requests & Roadmap Signals

**New feature requests filed today**:

- **CIDR whitelist** ([#6048](https://github.com/agentscope-ai/QwenPaw/issues/6048)) – allow CIDR‑notation in “no‑auth host” list. High demand from enterprise users.
- **Policy management UI** ([#5880](https://github.com/agentscope-ai/QwenPaw/issues/5880)) – ability to clear/invalidate “always allow” rules from the web console.
- **Reusable workflow orchestration with audit trail** ([#6163](https://github.com/agentscope-ai/QwenPaw/issues/6163)) – multi‑step agent pipelines with structured outputs.
- **Standalone Python environment** ([#6160](https://github.com/agentscope-ai/QwenPaw/issues/6160)) – QwenPaw Desktop should bundle its own Python for script execution.
- **Windows 7 support** ([#6076](https://github.com/agentscope-ai/QwenPaw/issues/6076)) – request for a non‑Tauri variant or Win7 workaround.
- **Input suggestion toggle** ([#6165](https://github.com/agentscope-ai/QwenPaw/issues/6165)) – option to disable English autocomplete popup for non‑English users.

Most likely to land in the next minor release:
- CIDR support (already a well‑structured request)
- Policy UI (complements existing “always allow” feature)
- Timezone fixes (already merged)

## 7. User Feedback Summary

**Repeated pain points**:
- **Windows admin requirement** – multiple users reported that v2.0.0.post2 is unusable on standard user accounts; workarounds require granting admin rights or disabling UAC.
- **Memory and context loss** – several users describe “amnesia” and truncation after upgrading, with `/compact` not working as expected.
- **Token cost surprises** – users see large token bills without active usage, raising trust concerns about background processes.
- **Docker timezone issues** – cron jobs and logs misaligned by 8 hours for Asia users.
- **QQ channel breakage** – agents that capture screenshots or use local images crash the bot entirely.

**Positive signals**: the team is merging fixes quickly, and first‑time contributor PRs (e.g., [#6203](https://github.com/agentscope-ai/QwenPaw/issues/6203), [#6204](https://github.com/agentscope-ai/QwenPaw/issues/6204)) are being reviewed, indicating a welcoming community.

## 8. Backlog Watch

**Issues that have been open for several days without a maintainer response or clear fix**:

| Issue | Opened | Last Update | Status |
|-------|--------|-------------|--------|
| [#5880](https://github.com/agentscope-ai/QwenPaw/issues/5880) | 2026-07-09 | 2026-07-16 | No maintainer comment; request for policy management UI |
| [#5995](https://github.com/agentscope-ai/QwenPaw/issues/5995) | 2026-07-12 | 2026-07-16 | Silent message drops – no assignee or PR linked yet |
| [#6047](https://github.com/

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

**ZeptoClaw Project Digest — 2026-07-17**

---

## 1. Today’s Overview
ZeptoClaw saw low but focused activity today: five issues were closed, all authored by YLChen-007 in the `docs(security)` category. These issues deal with classifying the “D2 trigger way” for specific CVEs (Issues #264, #466, #329, #268, #271) by source-verifying prompt-mediated paths and updating JSON evidence files. No pull requests or releases were published, and no new community discussion emerged. Overall project activity is stable but narrow, centered on internal security documentation tasks.

## 2. Releases
No new releases were created in the last 24 hours. The latest release remains the previous version (none listed in data).

## 3. Project Progress
No pull requests were merged or closed today. The five closed issues represent completed documentation updates:
- **#631** – Classify D2 trigger for Issue 264 ([link](https://github.com/qhkm/zeptoclaw/issues/631))
- **#635** – Classify D2 trigger for Issue 466 ([link](https://github.com/qhkm/zeptoclaw/issues/635))
- **#634** – Classify D2 trigger for Issue 329 ([link](https://github.com/qhkm/zeptoclaw/issues/634))
- **#632** – Classify D2 trigger for Issue 268 ([link](https://github.com/qhkm/zeptoclaw/issues/632))
- **#633** – Classify D2 trigger for Issue 271 ([link](https://github.com/qhkm/zeptoclaw/issues/633))

These issues advance the project’s security classification workflow, specifically filling in the `d2_xclaw_trigger_way` field in issue-security JSON files.

## 4. Community Hot Topics
No issues or pull requests attracted significant community attention today. The five closed issues each received one comment (from the author) and zero reactions. There are no active threads for discussion. The project currently shows no signs of external community engagement in the last 24 hours.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The closed issues are documentation tasks, not bug reports. Stability appears unchanged.

## 6. Feature Requests & Roadmap Signals
No feature requests were submitted today. The closed issues indicate a continuing effort to standardize and automate security trigger classification, which may hint at future tooling improvements (e.g., automated JSON validation or prompt-to-tool analysis pipelines). However, no explicit roadmap signals emerged.

## 7. User Feedback Summary
No user feedback, pain points, or satisfaction reports were recorded in the data. All activity is internal (contributor YLChen-007). There are no observable user concerns or use-case mentions.

## 8. Backlog Watch
No long-unanswered important issues or PRs were identified. The five issues closed today were handled promptly (created and closed on the same day). The repository appears well-maintained with no stale items requiring maintainer attention.

---

*Generated from qhkm/zeptoclaw GitHub data collected on 2026-07-17.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-17

## Today’s Overview

The ZeroClaw repository is in a period of intense development velocity, with **25 issues** and **50 pull requests** updated in the last 24 hours. Of those, **23 issues remain open** (two closed) and **46 PRs are open** (four merged/closed). The release pipeline is paused (no new releases), but feature work is accelerating across the board, particularly in the **channel‑plugin runtime stack**, **memory subsystem redesign**, and **provider/unified-client refactoring**. Technical debt is being addressed through RFCs and trackers, while several S1‑severity bugs (browser hang, pgvector panic) are actively being triaged. Maintainer bandwidth is stretched, as evidenced by a growing backlog of “needs‑author‑action” and “needs‑maintainer‑review” items.

---

## Releases

*None.* No new releases were created in the last 24 hours. The last tagged release was v0.8.3 (see closed tracker #7320 for closeout details). The next planned maintenance release is v0.8.4, target date July 31 2026 (tracker #8357).

---

## Project Progress

No details are available for the four PRs merged/closed in the last 24 hours (they are not among the top 20 listed). However, the **two closed issues** provide signal:

- **[#8798 (closed, wontfix)](https://github.com/zeroclaw-labs/zeroclaw/issues/8798)** — RFC to consolidate `/ws/chat` and `/acp` onto a single wire protocol. The `wontfix` label indicates the maintainers decided against this consolidation, likely in favor of maintaining separate protocols.
- **[#7320 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/7320)** — Tracker for the v0.8.3 milestone, now closed. All planned work merged, final release validation remains.

Notably, the open PR stack from **JordanTheJet** (PRs #8949, #8863, #8862, #8857, #8855, #8852, #8923) is laying the foundation for **plugin‑based channels** – a major feature that will allow third‑party WASM channel plugins to run inside the daemon.

---

## Community Hot Topics

The most active discussions (by comment count) reveal key areas of community interest:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | 11 | Unify providers architecture and reqwest client management |
| [#7952](https://github.com/zeroclaw-labs/zeroclaw/issues/7952) | 7 | Publish optional `channels-full` prebuilt bundles |
| [#9101](https://github.com/zeroclaw-labs/zeroclaw/issues/9101) | 5 | Consolidate release attestation mechanisms (three signing stories) |
| [#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832) | 5 | RFC: Gateway-local Kanban board for agent work |
| [#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) | 5 | RFC: Separate conversation history from agent‑curated long‑term memory |

**Underlying needs:**
- **#5937**: Contributors are frustrated by duplicated, inconsistent provider configuration – the community wants a single, clean abstraction.
- **#7952**: Operators of niche channel backends (e.g., Matrix) cannot use the prebuilt binary because their channels are excluded; a complementary “full” bundle would reduce friction.
- **#9101**: Redundant provenance tooling is wasting CI minutes and confusing external auditors – a single signing story is demanded.
- **#8832**: Users running many agents need a visual dashboard to answer “what is my agent doing right now”.
- **#9048**: Memory confusion – session history and long‑term memory are conceptually separate but implementation still mixes them, causing unintended memory growth.

---

## Bugs & Stability

Several bugs were updated in the last 24h, ranked by severity:

- **S1 – Workflow blocked**
  - **[#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560)**: `browser_open` hangs the agent turn when the launcher cannot open a window (unbounded subprocess wait). Also affects robot‑kit TTS and channels `ffmpeg`. *Status: in‑progress, fix PR not yet identified.*
  - **[#9085](https://github.com/zeroclaw-labs/zeroclaw/issues/9085)**: Nested runtime panic in `try_enable_pgvector` when pgvector is enabled at startup – gateway/agent fails to start. *Status: accepted, no fix PR yet.*
- **S2 – Degraded behavior**
  - **[#9046](https://github.com/zeroclaw-labs/zeroclaw/issues/9046)**: `models_cache.json` is read but never written – the “run zeroclaw models refresh” hint cannot resolve the missing cache. *Status: in‑progress, PR likely needed.*
  - **[#9078](https://github.com/zeroclaw-labs/zeroclaw/issues/9078)**: Serial transport remains desynchronized after a non‑matching response ID; hardware peripheral communication degrades. *Status: accepted.*
  - **[#9089](https://github.com/zeroclaw-labs/zeroclaw/issues/9089)**: Tool output supports `[IMAGE:]` markers but not `[AUDIO:]` – audio file markers appear as literal text to the model. *Status: accepted.*

Additionally, two fix PRs are in progress:
- **[#8902](https://github.com/zeroclaw-labs/zeroclaw/pull/8902)** – Fix bidirectional RPC for `ask_user` and `poll`.
- **[#9105](https://github.com/zeroclaw-labs/zeroclaw/pull/9105)** – Fix Lucid memory connector ARM cold‑start timeouts and make timeouts configurable.

---

## Feature Requests & Roadmap Signals

The most significant feature‑related activity centres around these RFCs and PRs:

### Likely candidates for the next release (v0.8.4 train)
- **Channel plugin system** – A stack of 7 open PRs (#8949, #8863, #8862, #8857, #8855, #8852, #8923) enabling host‑mediated WebSocket, raw TCP/TLS, and webhook ingress for WASM channel plugins. **This is the biggest infrastructure change in flight.**
- **Memory refactor** – RFC [#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) (separate conversation history from long‑term memory) and tracker [#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891) are driving a multi‑PR effort to wire memory curation, relevance, and operability.
- **Provider unified client** – Issue #5937 has widespread agreement; a refactor of `reqwest` builder and model construction is expected to land soon.
- **Gateway Kanban** – RFC [#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832) for an opt‑in Kanban board on the web dashboard, inspired by OpenClaw and Hermes Agent.

### Longer‑term / exploratory
- Gemini Live realtime speech channel ([#8780](https://github.com/zeroclaw-labs/zeroclaw/issues/8780))
- A2A outbound client ([#9106](https://github.com/zeroclaw-labs/zeroclaw/issues/9106))
- Separate authoritative memory from enrichment connectors ([#9103](https://github.com/zeroclaw-labs/zeroclaw/issues/9103))
- In‑app upgrade with environment‑aware restart ([#8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170))
- Capability‑aware documentation for agent‑visible features ([#8367](https://github.com/zeroclaw-labs/zeroclaw/issues/8367))

---

## User Feedback Summary

Real user pain points captured in this data:

- **Configuration complexity** – Users are confused when a channel they want is not compiled into the prebuilt binary (#7952). The inconsistency in provider configuration (#5937) forces manual workarounds.
- **Agent reliability** – Hangs (browser_open, #8560) and panics (pgvector, #9085) directly block workflows. Users are demanding better timeout handling and error recovery.
- **Memory confusion** – Users expect session history and long‑term memory to behave differently, but the current implementation merges them, causing unexpected behaviour (#9048).
- **Tool output limitations** – Agents cannot return audio to the user because the `[AUDIO:]` marker is not parsed (#9089); this hinders voice‑focused use cases.
- **Observability gap** – The lack of a unified “what is my agent doing” view (Kanban, #8832) forces users to dig through logs.
- **Plugin permissioning** – Coarse‑grained `PluginPermission` enum provides no per‑feature granularity (#8398); plugin authors want a more expressive model.

Conversely, satisfaction signals: the community is actively contributing RFCs and PRs, suggesting strong engagement with the project’s direction.

---

## Backlog Watch

Several important items are blocked or awaiting maintainer/author action:

| Issue | Status | Why it matters |
|-------|--------|----------------|
| [#8541](https://github.com/zeroclaw-labs/zeroclaw/issues/8541) | `blocked`, `needs‑maintainer‑review` | Matrix thread‑scoped history – 2 comments, no traction since June 30. Critical for Matrix users. |
| [#8367](https://github.com/zeroclaw-labs/zeroclaw/issues/8367) | `blocked`, `needs‑maintainer‑review` | Capability‑aware docs – a foundational design decision for agent usability. |
| [#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891) | `needs‑maintainer‑review` | Persistent memory tracker – coordinates multiple PRs; review bottleneck may delay the whole memory refactor. |
| [#8398](https://github.com/zeroclaw-labs/zeroclaw/issues/8398) | `needs‑author‑action` | Plugin permission RFC – questions about granularity still open. |
| PRs with `needs‑author‑action` | #8486, #8571, #7960, #8966, #8384, #8905 | These PRs are stalled because the author hasn’t responded to review feedback. They represent features like OpenAI compatibility, OAuth delegation, pipeline tool gating, and the Inkbox channel. |

**Maintainer bandwidth is a bottleneck.** The removal of `@singlerider` from CODEOWNERS (PR #9107) after their departure will increase pressure on remaining maintainers. The project would benefit from additional reviewers to unblock the “needs‑maintainer‑review” queue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*