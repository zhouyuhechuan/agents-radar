# OpenClaw Ecosystem Digest 2026-06-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-15 02:59 UTC

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

# OpenClaw Project Digest – 2026-06-15

A data-driven summary of the OpenClaw open‑source AI agent framework, based on GitHub activity over the last 24 hours.

---

## 1. Today's Overview

OpenClaw saw **exceptional community engagement** today, with **500 issues** and **500 pull requests** updated—the platform remains in a highly active maintenance and development phase. Of those, 437 issues and 429 PRs are still open, while 63 issues and 71 PRs were closed or merged. A **new beta release (v2026.6.8‑beta.1)** landed, focusing on richer and more reliable delivery for Telegram and WhatsApp channels. The project continues to address a high volume of P1/P2 bugs, with many “needs‑maintainer‑review” tags indicating a backlog of triage awaiting core team attention. Community users are reporting real‑world pain points around message truncation, session stalls, and provider overload, all of which are actively being investigated.

---

## 2. Releases

**v2026.6.8‑beta.1** (tag: `2026.6.8‑beta.1`)

**Highlights from release notes:**
- **Telegram** – structured rich text with tables, lists, expandable blockquotes; prompt‑preserving CLI backend delivery; retired native draft migration; safer rich‑media boundaries.
- **WhatsApp** – richer delivery with improved brittleness handling.

The release is labelled beta and appears to be a stability/delivery improvement release. No breaking changes or migration notes were mentioned.

---

## 3. Project Progress

In the last 24 hours, **71 PRs were merged or closed**, indicating sustained development velocity. While the provided data does not include a detailed list of merged PRs, several open PRs show meaningful progress toward resolving long‑standing issues:

- [**#93076**](https://github.com/openclaw/openclaw/pull/93076) – Preserve WhatsApp Web auth on terminal disconnects (P2, ready for maintainer).
- [**#85932**](https://github.com/openclaw/openclaw/pull/85932) – Suppress duplicate OpenAI greeting in voice calls (fixes #85846).
- [**#92340**](https://github.com/openclaw/openclaw/pull/92340) – Handle Feishu VC meeting invites as synthetic DM turns.
- [**#88810**](https://github.com/openclaw/openclaw/pull/88810) – Silently skip empty‑text sends in Telegram.
- [**#85104**](https://github.com/openclaw/openclaw/pull/85104) – “Fast talks auto mode” with dynamic fallback retiering (large feature, with video proof).

The merged/closed count suggests that several bug fixes and small features were integrated, but the majority of open work remains under review or awaiting maintainer decision.

---

## 4. Community Hot Topics

The most active issues (by comment count and reactions) reveal three major user concerns:

### 🥇 Cron reliability & provider overload
- **Issue #85888** (12 comments, 1👍) – “Cron jobs consistently fail with MiniMax 503 overload during early morning (05:00‑07:30 CST), manual triggers succeed.” Users report a systematic scheduling‑layer issue, not pure API unavailability.  
  [https://github.com/openclaw/openclaw/issues/85888](https://github.com/openclaw/openclaw/issues/85888)

### 🥇 Silent message truncation in Codex app‑server
- **Issue #84516** (11 comments, 2👍) – “Codex app‑server: long agent replies silently truncated at ~1000‑1100 chars (stop=null, aborted=false).” A high‑impact data‑loss bug for headless usage.  
  [https://github.com/openclaw/openclaw/issues/84516](https://github.com/openclaw/openclaw/issues/84516)

### 🥇 Provider fallback chain not triggered on quota exhaustion
- **Issue #85103** (9 comments, 1👍) – “Model fallback chain not triggered on provider‑wide quota exhaustion + EmbeddedAttemptSessionTakeoverError.” This affects users relying on multi‑provider redundancy.  
  [https://github.com/openclaw/openclaw/issues/85103](https://github.com/openclaw/openclaw/issues/85103)

Other highly discussed issues:
- **#85251** – Codex app‑server turn/started silent wedge (8 comments).  
- **#85126** – Wrong authProfileOverride auto‑selection in TUI/WebChat (8 comments).  
- **#85030** – MCP tools not injected into subagent sessions (8 comments, 3👍).  
- **#84903** – Single stalled agent blocks entire Gateway event loop (8 comments, 2👍).  
- **#88951** – Duplicate message content after upgrade (8 comments).  

The underlying needs are clear: **reliable job scheduling**, **no silent data loss**, and **robust multi‑provider fallback**.

---

## 5. Bugs & Stability

Over the last 24 hours, the project tracked dozens of bugs. Below are the most severe (P0/P1) with no immediate fix PRs:

### P0 – Data loss
- **#84882** – “memory‑core Dreaming silently deletes daily memory files (memory/YYYY‑MM‑DD.md)” – reported May 21, still open.  
  [https://github.com/openclaw/openclaw/issues/84882](https://github.com/openclaw/openclaw/issues/84882)

### P1 – Message loss / session crashes
- **#84516** – Truncated Codex replies (see above). No new fix PR.
- **#85103** – Fallback chain not triggered (see above). No new fix PR.
- **#85251** – Codex app‑server turn wedge (see above). No new fix PR.
- **#84903** – Gateway event loop isolation failure. No new fix PR.
- **#83184** – Heartbeat‑driven replies leave `pendingFinalDelivery` stuck, blocking subsequent heartbeats. No new fix PR.
- **#88951** – Duplicate messages after upgrade 2026.5.4→5.27. No new fix PR.
- **#83959** – Codex app‑server startup retries can exhaust before replacement is ready. No new fix PR.
- **#84569** – WhatsApp session stalls on long model call (incomplete turn). No new fix PR.
- **#90886** – Gateway hangs with missing provider credentials (regression, fixed? Actually closed on June 15). ✅ This one is now closed.
- **#91016** – DeepSeek Prompt Cache失效 after upgrade, costing ~$6/hour. Closed? Actually listed as CLOSED (status indicates closed). That was resolved.

Many of these carry the `clawsweeper:no-new-fix-pr` tag, meaning no pull request has been created yet. The core team appears to be collecting evidence and discussing solutions.

### Regressions
- **#45494** (March 13) – Cron jobs silently time out on sustained API errors instead of fast‑failing. Still open.
- **#81484** – Discord guild reply regression with malformed payloads (May 13).

### Fix PRs in review
- **#93076** – WhatsApp auth preservation.
- **#91886** – Feishu streaming mode fix (closed today).
- **#88810** – Telegram empty‑text send skip.

---

## 6. Feature Requests & Roadmap Signals

Several user‑requested enhancements indicate where the project may head next:

| Issue | Description | Likelihood for next release |
|-------|-------------|----------------------------|
| [#74077](https://github.com/openclaw/openclaw/issues/74077) | Slash command to set streaming mode per session | Medium – relatively simple UX change, existing interest |
| [#56781](https://github.com/openclaw/openclaw/issues/56781) | Fallback model chain for compaction & LCM summaryModel | High – directly addresses user reliability concerns |
| [#81913](https://github.com/openclaw/openclaw/issues/81913) | Expose stable plugin SDK for installed skill workflows | Medium – needed for ecosystem growth |
| [#44395](https://github.com/openclaw/openclaw/issues/44395) | Heading‑aware chunking + entity extraction for memory search | Medium – memory quality improvement |
| [#92105](https://github.com/openclaw/openclaw/issues/92105) | Configurable page groups for memory‑wiki | Low – niche, but asked by multiple users |
| [#85332](https://github.com/openclaw/openclaw/issues/85332) | Slim Docker image with configurable APT packages | Low – infrastructure, few 👍 |

**Most probable near‑term addition:** the **fallback chain for compaction** (issue #56781) aligns with the current focus on reliability and has been open since March. Also the **fast talks auto mode** (PR #85104) is already submitted with video proof and likely to be merged soon.

---

## 7. User Feedback Summary

Real user pain points extracted from recent issues:

- **Cron scheduling fragility** – Jobs fail only at certain times (05:00‑07:30 CST) but manual triggers succeed, suggesting a scheduling‑layer race condition. Users are losing routine automation.
- **Silent truncation / data loss** – Headless (`openclaw message`) users report replies cut off with no error. This erodes trust in the Codex integration.
- **Provider fallback not working** – Users who carefully configure fallback chains (e.g., opeanai → deepseek → kimi) still hit quota errors that should have been avoided.
- **Upgrade regressions** – Several reports of features working in one version and breaking after upgrade (e.g., #88951 duplicate messages, #91016 prompt cache cost explosion).
- **Stale session isolation** – One blocked agent can halt the entire Gateway, affecting multi‑agent deployments.
- **Channel‑specific quirks** – WhatsApp stalls, Feishu card rendering, Telegram group reply context loss – each platform has its own “death by a thousand cuts.”

Positive feedback is less visible, but the new release v2026.6.8‑beta.1 specifically addresses Telegram/WhatsApp delivery brittleness, which has been a repeated complaint.

---

## 8. Backlog Watch

The following long‑standing, important issues and PRs remain unresolved and may need maintainer intervention:

| Item | Type | Age | Status | Why it matters |
|------|------|-----|--------|----------------|
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | Bug (P1) | March 13 (3 months) | Open, no fix PR | Cron jobs waste timeouts on definitive API errors; affects all cron users |
| [#56781](https://github.com/openclaw/openclaw/issues/56781) | Feature (P2) | March 29 (2.5 months) | Open | Compaction silently fails when single model is unavailable |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Bug (P1) | May 20 (26 days) | Open, `needs‑live‑repro` | Silent truncation – high user impact |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | Bug (P1) | May 21 (25 days) | Open, `needs‑live‑repro` | Fallback chain bypassed – core reliability issue |
| [#84903](https://github.com/openclaw/openclaw/issues/84903) | Bug (P1) | May 21 (25 days) | Open | Event loop isolation failure |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | Bug (P1) | May 21 (25 days) | Open | MCP tools ignored in subagents – blocks advanced use cases |
| [#83964](https://github.com/openclaw/openclaw/issues/83964) | Bug (P1) | May 19 (27 days) | Open, `needs‑live‑repro` | Codex `ERR_MODULE_NOT_FOUND` unless openclaw installed locally |
| [#83419](https://github.com/openclaw/openclaw/issues/83419) | Bug (P1) | May 18 (28 days) | *Closed* (resolved on June 15) | Group chat user‑role message breaking Anthropic API |

**Observation:** Several P1 bugs are waiting for `needs‑live‑repro` or `needs‑maintainer‑review` labels. The core team may be bandwidth‑constrained. Community users who can provide reliable reproduction steps or video proof (as some PRs do) may accelerate resolution.

---

*Digest generated from openclaw/openclaw public GitHub data. All links use canonical openclaw/openclaw repository.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

**Date:** 2026-06-15  
**Prepared for:** Technical decision-makers and developers evaluating AI agent frameworks.

---

## 1. Ecosystem Overview

The open‑source personal AI agent landscape remains in a rapid growth phase, with over a dozen actively maintained projects competing on feature breadth, channel support, and security maturity. Today’s digest shows **exceptional overall activity**: across 13 tracked projects, more than 1,100 issues and 1,100 pull requests were updated, with several hundred merged or closed. The ecosystem is driven by two strong forces: the **demand for reliable multi‑provider agent infrastructure** (cron, fallbacks, token accounting) and the **urgent need for security hardening** (credential leaks, shell approval bypasses, file exfiltration). Projects like OpenClaw, Hermes Agent, IronClaw, and ZeroClaw dominate the conversation, while smaller projects focus on niche use‑cases (edge devices, Chinese markets, Azure enterprise). The overall mood is constructive but impatient—users expect stability as a prerequisite for adoption.

---

## 2. Activity Comparison

| Project | Issues Updated | Issues Closed | PRs Updated | PRs Merged/Closed | Release This Period | Health Score* |
|---------|---------------|--------------|-------------|-------------------|---------------------|---------------|
| OpenClaw | 500 | 63 | 500 | 71 | Beta v2026.6.8‑beta.1 | 3/5 |
| NanoBot | 5 | 3 | 46 | 28 | None | 4/5 |
| Hermes Agent | 50 | 8 | 50 | 8 | None | 3/5 |
| PicoClaw | 5 | 1 | 9 | 5 | Nightly v0.2.9‑nightly | 3/5 |
| NanoClaw | 7 | – | 10 | 5 | None | 3/5 |
| NullClaw | 1 | 0 | 0 | 0 | None | 1/5 |
| IronClaw | 39 | 7 | 44 | 17 | None | 4/5 |
| LobsterAI | 2 (updated) | 0 | 3 (open) | 1 | None | 2/5 |
| TinyClaw | 0 | 0 | 0 | 0 | None | 1/5 |
| Moltis | 1 (new) | 0 | 0 | 0 | None | 1/5 |
| CoPaw | 17 | 0 | 12 | 0 | None | 2/5 |
| ZeptoClaw | 0 | 0 | 0 | 0 | None | 1/5 |
| ZeroClaw | 42 | 28 | 50 | 3 | None | 5/5 |

*Health Score: composite of activity volume, issue closure rate, maintainer responsiveness, and severity of unresolved bugs. 1=minimal, 5=excellent.

---

## 3. OpenClaw’s Position

**Advantages:**
- **Largest community volume** – 500 issues/500 PRs per day, indicating the widest user base and most extensive contributor pool.
- **Reference implementation status** – serves as the core framework many others fork or extend.
- **Broadest channel coverage** – Telegram, WhatsApp, Feishu, Discord, CLI, WebChat; the beta release today specifically improves Telegram/WhatsApp delivery.

**Technical approach differences:**
- OpenClaw emphasises **provider fallback chains**, **memory‑core Dreaming**, and **cron reliability**, but these exact areas remain the source of its highest‑severity bugs (e.g., #85888 cron failures, #84516 silent truncation).
- Peers like **NanoBot** focus on **OpenAI‑compatible endpoints** and **token accounting**—areas where OpenClaw lags (no token usage reporting).
- **Hermes Agent** and **IronClaw** invest heavily in **desktop security** (credential store isolation, shell approval hardening) which OpenClaw has not addressed at the same depth.

**Community size comparison:**
- OpenClaw’s activity dwarfs all others in raw issue/PR counts, but its closure rate (12.6% for issues, 14.2% for PRs) is lower than **ZeroClaw** (66.7% issues closed) or **NanoBot** (60% issues closed). This suggests a **triage bottleneck** rather than a lack of engagement.

**Verdict:** OpenClaw is the ecosystem’s center of gravity, but its reliability debt and backlog of P1 bugs (memory deletion, cron timeouts, fallback bypass) open a window for competitors.

---

## 4. Shared Technical Focus Areas

The following requirements appear across **three or more projects**, indicating ecosystem‑wide needs:

| Requirement | Projects Affected | Specific Signals |
|-------------|------------------|------------------|
| **Provider fallback reliability** | OpenClaw, NanoClaw, Hermes Agent, CoPaw | OpenClaw #85103 (fallback chain not triggered), NanoClaw #2751 (budget exhaustion drop), Hermes #43083 (silent routing), CoPaw #5163 (Gemini regression) |
| **Cron / scheduling robustness** | OpenClaw, PicoClaw, CoPaw, ZeroClaw | OpenClaw #85888 (503 overload), CoPaw #5174 (heartbeat timeout), ZeroClaw #7384 (pause/resume toggle) |
| **Silent data loss prevention** | OpenClaw, NanoClaw, Hermes Agent, CoPaw | OpenClaw #84516 (truncation), NanoClaw #2751 (budget drop), Hermes #7237 (truncation), CoPaw #5171 (context compression loss) |
| **Security hardening** | Hermes, NanoClaw, IronClaw, ZeroClaw | Hermes #43083 (password leakage), NanoClaw #2760‑#2762 (file exfiltration, approval bypass), IronClaw #4861‑#4865 (shell bypass), ZeroClaw #7470 (delegate agentic mode) |
| **Cross‑platform channel parity** | OpenClaw, NanoBot, PicoClaw, CoPaw, ZeroClaw | All projects have platform‑specific bugs (Telegram block splitting, WhatsApp stalls, Matrix E2EE, Feishu streaming) |
| **Token / cost accounting** | NanoBot, OpenClaw, Hermes Agent | NanoBot #4309 (zero tokens), OpenClaw #91016 (prompt cache cost), Hermes #46090 (slow agent) |
| **Desktop UX polish** | Hermes Agent, CoPaw, ZeroClaw | Hermes #44140 (auto‑scroll, sidebar), CoPaw #5047 (Windows startup 10min), ZeroClaw #6808 (work lanes RFC) |

These themes indicate that **reliability** (cron, fallback, no silent drops) and **security** are the two largest gaps the ecosystem must address to move from “demo‑ready” to “production‑ready”.

---

## 5. Differentiation Analysis

| Project | Primary Differentiator | Target User | Technical Architecture |
|---------|----------------------|-------------|------------------------|
| **OpenClaw** | Broadcast channel support, reference framework | Power users, multi‑platform deployers | Monolithic core + channel adapters, memory‑core recall |
| **NanoBot** | OpenAI API drop‑in compatible, high PR velocity | Developers needing a local OpenAI‑compatible endpoint | Lightweight HTTP server, minimal dependencies |
| **Hermes Agent** | Desktop security (credential isolation, shell protection) | Security‑conscious enterprises | Desktop app (Tauri), strict permission model, session isolation |
| **PicoClaw** | Lightweight embedded/edge agent | IoT, low‑resource devices | Go implementation, minimal footprint, nightly builds |
| **NanoClaw** | Provider plug‑in seam with vault‑only auth | Multi‑provider orchestrators | Registry + installer pattern, health audits |
| **NullClaw** | Azure identity‑based authentication | Azure‑native enterprise | Single feature focus (Azure OpenAI DefaultTokenCredential) |
| **IronClaw** | Reborn (next‑gen) agent stack, engineering productivity | Dogfooding AI‑native development | WebSocket‑based Reborn, observability seams, shell approval system |
| **LobsterAI** | Co‑work session management, Chinese localization | Chinese users, team collaboration | SQLite‑based session persistence, Feishu integration |
| **CoPaw** | Qwen desktop client, Windows GUI automation | Chinese desktop users, plugin ecosystem | Tauri + Python backend, built‑in PRD/CRUD tools |
| **ZeroClaw** | Extreme integration breadth (50+ providers, channels, tools) | Integrators wanting one‑stop agent | Rust/Core, type‑driven config enums, RFC governance |

**Key insight:** The ecosystem is fragmenting by **security posture** (Hermes, NanoClaw, IronClaw) vs. **integration breadth** (OpenClaw, ZeroClaw) vs. **platform focus** (CoPaw, LobsterAI, NullClaw). No single project dominates all axes.

---

## 6. Community Momentum & Maturity

**Tier 1 – Rapid iteration (high activity, frequent merges, strong maintainer response):**
- **ZeroClaw** (5/5 health) – 42 issues/50 PRs, 28 issues closed, 3 PRs merged today. Structured RFC process, many feature integrations (providers, SMS channels).
- **IronClaw** (4/5) – 39 issues/44 PRs, 7 issues closed, 17 PRs merged today. Strong engineering dogfooding, but shell security issues unresolved.
- **NanoBot** (4/5) – Low issue count but high PR merge rate (28/46). Responsive to bugs (Anthropic deprecation fixed same day).
- **OpenClaw** (3/5) – Highest raw activity but low closure rate. Many P1 bugs without fix PRs (e.g., memory deletion, cron timeouts). Maintainers are overwhelmed.

**Tier 2 – Stabilizing / moderate cadence:**
- **Hermes Agent** (3/5) – Active but 42 open issues, 42 open PRs. Security issues (password leak, shell bypass) under investigation.
- **PicoClaw** (3/5) – Steady bug‑fix merges, but no major features. Nightly builds indicate maintenance mode.
- **NanoClaw** (3/5) – Feature PRs merging (provider selection, Codex v2), but three critical security bugs need triage.

**Tier 3 – Low activity / dormant:**
- **LobsterAI** (2/5) – Two stale UI bugs (72 days), low PR throughput. Chinese‑focused but slow.
- **CoPaw** (2/5) – High issue/PR count *but zero merges today*. Several regressions in latest release (Gemini, local providers). Maintainers appear blocked.
- **NullClaw, Moltis, TinyClaw, ZeptoClaw** – Essentially inactive in the last 24 hours.

**Conclusion:** The ecosystem’s **innovation engine** is ZeroClaw, IronClaw, and NanoBot. OpenClaw remains the largest but risks losing edge to faster‑moving peers if its bug

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest – 2026-06-15

## 1. Today's Overview
The NanoBot project is in a **high-activity phase**: 46 pull requests were updated in the last 24 hours (28 merged/closed), and 5 issues received updates (3 closed, 2 new). The development cadence points to a maturing codebase with systematic refactoring, improved WebUI parity, and focused bug fixes. No new releases were tagged today, but the sheer volume of merged PRs suggests an imminent stable release is being prepared.

---

## 2. Releases
*No new releases today.* Previous stable version remains the latest.

---

## 3. Project Progress
**28 PRs merged/closed today** (including the 20 shown in the top-by-comment list). Key advancements:

- **WebUI parity and mobile responsiveness** – [#4313](https://github.com/HKUDS/nanobot/pull/4313) added write endpoints for temperature, tool limits, dream, channels, and memory; [#4339](https://github.com/HKUDS/nanobot/pull/4339) tightened mobile layout and heatmap display.
- **Agent loop robustness** – [#4269](https://github.com/HKUDS/nanobot/pull/4269) finalizes max-iteration turns with a concise message; [#4274](https://github.com/HKUDS/nanobot/pull/4274) scopes recent history by session; [#4299](https://github.com/HKUDS/nanobot/pull/4299) binds cron automations to sessions.
- **Tool configuration and execution** – [#4273](https://github.com/HKUDS/nanobot/pull/4273) added `exec.pathPrepend`; [#4138](https://github.com/HKUDS/nanobot/pull/4138) added `tools.file.enable` toggle; [#4314](https://github.com/HKUDS/nanobot/pull/4314) broke tool config schema import cycles.
- **Desktop and client stability** – [#4210](https://github.com/HKUDS/nanobot/pull/4210) fixed desktop restart token and WebSocket replay gaps; [#4277](https://github.com/HKUDS/nanobot/pull/4277) lazy-loaded Lark SDK to avoid gateway startup hangs.
- **Documentation and onboarding** – [#4177](https://github.com/HKUDS/nanobot/pull/4177) reworked docs for beginners; [#4245](https://github.com/HKUDS/nanobot/pull/4245) removed obsolete nightly branch guidance.
- **Validation and error handling** – [#4275](https://github.com/HKUDS/nanobot/pull/4275) fails fast on invalid config files; [#4248](https://github.com/HKUDS/nanobot/pull/4248) fixed token heatmap timezone rendering.

---

## 4. Community Hot Topics
Most active discussions (by comment count and cross-references):

- **[#4309](https://github.com/HKUDS/nanobot/issues/4309) – Zero usage tokens in `/v1/chat/completions`** – A user reports that the OpenAI-compatible endpoint always returns `0` for all token counts, even though the agent loop tracks real usage. This is a **blocker for developers relying on token accounting** (e.g., cost tracking, rate limiting). Only 1 comment so far; no associated PR yet.

- **[#4345](https://github.com/HKUDS/nanobot/issues/4345) / [#4346](https://github.com/HKUDS/nanobot/pull/4346) – Image-strip fallback leaks file path** – A newly filed bug (today) reveals that when an image is stripped due to model errors, the fallback text includes the full local file path, which is a **potential information leak**. A fix PR [#4346](https://github.com/HKUDS/nanobot/pull/4346) was submitted immediately by the reporter, suggesting strong community ownership and quick triage.

- **[#4333](https://github.com/HKUDS/nanobot/issues/4333) – Anthropic deprecated `temperature` for opus-4-8** – Closed yesterday after a corresponding fix was merged. This was a critical issue breaking all requests for users of Claude Opus‑4‑8 / Fable; the community quickly flagged it and the team responded.

- **[#4250](https://github.com/HKUDS/nanobot/issues/4250) – Telegram `split_message` breaks fenced code blocks** – Closed today. The fix ensures that long code blocks are not split mid-fence, which was breaking rendering for users on Telegram. Medium engagement but high practical impact.

**Underlying needs**: Users are demanding **strict API compatibility** (token counting, parameter adherence), **security hardening** (path leaks), and **platform-specific polish** (Telegram, mobile).

---

## 5. Bugs & Stability
### High severity
- **[#4345](https://github.com/HKUDS/nanobot/issues/4345) – Image-strip fallback leaks file path**  
  *Status*: Open, fix PR [#4346](https://github.com/HKUDS/nanobot/pull/4346) in review.  
  *Impact*: Anyone using image-provider fallback risks exposing local filesystem paths in the model’s response. Security-critical.

### Medium severity
- **[#4309](https://github.com/HKUDS/nanobot/issues/4309) – Zero usage tokens in `/v1/chat/completions`**  
  *Status*: Open, no fix PR yet.  
  *Impact*: Breaks cost accounting and integration with external logging. The fix should be straightforward (pass real token counts from the agent loop).

### Low severity (closed/fixed)
- [#4333](https://github.com/HKUDS/nanobot/issues/4333) – Anthropic `temperature` deprecated (fixed in recent merge).
- [#4250](https://github.com/HKUDS/nanobot/issues/4250) – Telegram code block splitting (fixed today).
- Open PRs addressing validation gaps: [#4343](https://github.com/HKUDS/nanobot/pull/4343) (reject unknown builtin parameters), [#4337](https://github.com/HKUDS/nanobot/pull/4337) (ignore empty injected payloads).

**Conclusion**: The project has strong bug triage – one security issue emerged today and was immediately PR’d. The token usage bug remains the most pressing unresolved issue.

---

## 6. Feature Requests & Roadmap Signals
**Merged today**:
- `tools.file.enable` toggle ([#4138](https://github.com/HKUDS/nanobot/pull/4138)) – powers deployments that restrict filesystem access.
- `exec.pathPrepend` config ([#4273](https://github.com/HKUDS/nanobot/pull/4273)) – simplifies tool directory PATH management.
- Automation session binding ([#4299](https://github.com/HKUDS/nanobot/pull/4299)) – ensures cron jobs respect per-session history.

**Open PRs likely to land in next release**:
- [#4330](https://github.com/HKUDS/nanobot/pull/4330) – **Automation management view** in WebUI (list, filter, run, pause/delete).
- [#4344](https://github.com/HKUDS/nanobot/pull/4344) – **Config and agent loop refactor** – moves tool config models out of runtime imports, a sign of architectural cleanup before a major release.
- [#4343](https://github.com/HKUDS/nanobot/pull/4343) – **Reject unknown tool parameters** – tightens validation for built-in tools.

**User-requested signals**:
- [#4262](https://github.com/HKUDS/nanobot/issues/4262) (closed) asked for `botIcon` to be used at agent startup – accepted and likely in next release.
- The zero-token bug ([#4309](https://github.com/HKUDS/nanobot/issues/4309)) is a silent blocker for API consumers; its resolution is likely a high priority.

**Predictions**: The next version will include the WebUI automation view, tighter parameter validation, and the image-strip security fix. Token usage accounting in the API endpoint should be addressed soon.

---

## 7. User Feedback Summary
- **Pain points**:
  - “Every `/v1/chat/completions` response returns zero tokens” – blocks cost monitoring.
  - “Image-strip fallback reveals my file paths” – privacy concern.
  - “Telegram code blocks render broken” – fixed today.
  - “Anthropic Claude 4.8 gives 400 errors” – fixed yesterday.
- **Use cases**: Users are deploying NanoBot as an OpenAI drop‑in, relying on token counters; using Telegram as a primary client; and configuring filesystem access per deployment.
- **Satisfaction signals**: Quick turnaround on reported issues (e.g., Anthropic fix, Telegram fix) and active community-driven fix PRs (image leak) indicate a healthy, responsive maintainer–community relationship.

---

## 8. Backlog Watch
No long‑lived unanswered issues or PRs were identified in the provided data set (all items were updated within the last 3 days). The project maintainers appear to be keeping pace with submissions. The absence of any issue with more than 1 comment suggests that the community is small but focused, or that issues are resolved before extensive discussion.  

*One item to monitor*: **[#4309](https://github.com/HKUDS/nanobot/issues/4309)** (zero usage tokens) has been open for 3 days without a fix PR – if it remains untouched for another week, it may warrant a community ping.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-15

## Today’s Overview
Project activity remains exceptionally high, with **50 issues and 50 pull requests updated** in the last 24 hours (42 open issues, 8 closed; 42 open PRs, 8 merged/closed). No new releases were published today. The community is heavily engaged around **security hardening, credential isolation, and stability fixes** for both the core agent and its desktop application. Several critical‑priority bugs have been reported (token‑leaking in sessions, Matrix E2EE resource exhaustion, unauthenticated credential file reads), and maintainers have already merged countermeasures for workflow‑token permissions and file‑preview guarding. The project is clearly in a rapid iteration phase with strong contributor participation.

## Releases
No new releases were recorded for this date.

## Project Progress
Eight pull requests were merged or closed today, reflecting both security hardening and targeted bug fixes:

- **Workflow token permissions hardened** – Two PRs (#46422, #46425 by Veritas‑7) limit default GitHub Actions token scope to read‑only, move write permissions to specific jobs, and disable credential persistence for read‑only checkouts.
- **MCP timeout validation added** – #45915 (merged) ensures `timeout` values in MCP server configs are validated as finite integers, preventing silent crashes.
- **Signal platform fixes** – Three merged PRs from lkz‑de:
  - #46387 preserves non‑media Signal attachments (documents).
  - #46389 scopes `group:` target parsing to Signal, avoiding misrouting on other platforms.
  - #46387 and #46389 are companion fixes improving document and group handling.
- **Auxiliary client lifecycle isolated** – #46390 (merged) prevents reuse/leak of short‑lived clients used during title generation.
- **Auth store corruption handling** – #46421 (open) preserves corrupt `auth.json` instead of overwriting it; not yet merged.

These changes improve security posture, platform reliability, and developer workflow safety.

## Community Hot Topics
The most active discussions and highest‑reacted issues reveal deep user concerns:

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) *[CLOSED]* | 46 | 👍6 | **Response truncation**: Long outputs are repeatedly cut mid‑stream with `Error: Response truncated due to output length limit`. Affects CLI, Telegram, Discord, Slack. Closed but no resolution visible in logs. |
| [#45058](https://github.com/NousResearch/hermes-agent/issues/45058) *[CLOSED]* | 7 | 👍15 | **Silent routing to Parallel.ai**: `web_search`/`web_extract` now route unconfigured traffic to Parallel.ai without notifying the user. 15 upvotes highlight strong privacy/trust concerns. |
| [#43083](https://github.com/NousResearch/hermes-agent/issues/43083) *[OPEN]* | 7 | – | **Password leakage through conversation history**: `***` masking is applied, but model reads back its own tool‑call history and re‑exposes credentials on second calls. Labelled P1. |
| [#44560](https://github.com/NousResearch/hermes-agent/issues/44560) *[OPEN]* | 5 | – | **WebSocket timeout due to synchronous HTTP calls**: `model.options` handler blocks on slow custom provider endpoints, breaking real‑time connections. P2. |
| [#44140](https://github.com/NousResearch/hermes-agent/issues/44140) *[OPEN]* | 3 | 👍3 | **Desktop UI pain points**: no auto‑scroll during streaming, sidebar overlap with scrollbar, no custom session groups. |
| [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) *[OPEN]* | 2 | – | **Concurrent session cross‑contamination**: shared memory injection and git worktree cause profile‑less interference. P2. |
| [#46192](https://github.com/NousResearch/hermes-agent/issues/46192) *[OPEN]* | 4 | – | **Feature request**: `Keep` option in `base_url` setup to avoid copy‑pasting common URLs. |

**Underlying need**: Users are demanding **isolation** (credential, session, memory, provider routing) and **transparency** (no silent backend changes, clear failure signals). The high reaction count on #45058 suggests trust in default behaviour is fragile.

## Bugs & Stability
New or updated bugs reported today, ranked by severity:

**P1 (Critical)**
- [#46310](https://github.com/NousResearch/hermes-agent/issues/46310) – **Matrix media path reconnects E2EE per message**: Full login + key share cycle per media send, exhausting recipient one‑time keys under burst. No fix PR yet.
- [#43083](https://github.com/NousResearch/hermes-agent/issues/43083) – **Passwords leak via history re‑reading**: Already noted above; no fix PR.

**P2 (High)**
- [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) – **Concurrent session cross‑contamination**: Shared memory injection, shared git worktree across Desktop sessions. No fix PR.
- [#46332](https://github.com/NousResearch/hermes-agent/issues/46332) – **Windows cron jobs fail with `.sh` scripts**: WSL bash preferred over Git Bash; backslashes eaten by MSYS. No fix PR.
- [#45963](https://github.com/NousResearch/hermes-agent/issues/45963) *(CLOSED)* – **Docker `profile create` auto‑starts doomed gateways** causing token‑conflict zombies.
- [#44560](https://github.com/NousResearch/hermes-agent/issues/44560) – **WebSocket timeout from synchronous HTTP providers** (see above). No fix PR.

**P3 (Medium/Low)**
- [#46090](https://github.com/NousResearch/hermes-agent/issues/46090) – **Agent becomes extremely slow** even for trivial tasks; `needs-repro` label.
- [#46131](https://github.com/NousResearch/hermes-agent/issues/46131) – **Ollama reasoning models return empty content** because of missing `reasoning_effort` parameter. No fix PR.
- [#46265](https://github.com/NousResearch/hermes-agent/issues/46265) – **SimpleX adapter silently drops DM replies** – `@<contactId>` resolved as display name. No fix PR.
- [#46413](https://github.com/NousResearch/hermes-agent/issues/46413) – **Desktop file preview can read Hermes credential stores** (auth.json, OAuth tokens). **Fix PR #46430** (liuhao1024) extends `sensitiveFileBlockReason()` to block these paths.
- [#46411](https://github.com/NousResearch/hermes-agent/issues/46411) – **`read_file` can exfiltrate credential stores from sibling profiles** – blocks only active `HERMES_HOME`. No fix PR yet.

**Observations**: Today’s bug reports cluster around **security boundaries** (file access, credential leakage) and **platform compatibility** (Windows, Docker, Matrix). Fixes for credential‑store exposure are already in progress.

## Feature Requests & Roadmap Signals
New and updated feature requests from the community:

| Issue | Summary | Likelihood for Next Release |
|-------|---------|-----------------------------|
| [#46192](https://github.com/NousResearch/hermes-agent/issues/46192) (P3) | `Keep` option for model’s `base_url` in CLI setup | **High** – small change, high QoL value. |
| [#46253](https://github.com/NousResearch/hermes-agent/issues/46253) (P3) | GBrain as a memory provider plugin (semantic memory backend) | **Medium** – aligns with plugin architecture, but requires integration work. |
| [#44140](https://github.com/NousResearch/hermes-agent/issues/44140) (P3) | Desktop auto‑scroll, sidebar overlap fix, custom session groups | **High** – top‑voted UI request; likely to be addressed soon. |
| [#45103](https://github.com/NousResearch/hermes-agent/issues/45103) (P3) | Desktop sidebar hover cards with AI‑generated session summaries | **Low** – large new module, but contributor offered to implement. |
| [#41553](https://github.com/NousResearch/hermes-agent/issues/41553) (P3) | Official integration of `outsourc-e/hermes-workspace` into Desktop | **Medium** – community tool already exists; official support would boost adoption. |
| [#23094](https://github.com/NousResearch/hermes-agent/issues/23094) (P3) | Configurable fallback‑model session stickiness | **Low** – no recent maintainer activity, but config addition. |
| [#13490](https://github.com/NousResearch/hermes-agent/issues/13490) (P3) | Configurable TUI status bar (fields, layout, skin colors) | **Low** – niche, requires UI redesign. |
| [#12020](https://github.com/NousResearch/hermes-agent/issues/12020) (P3) | Switch to suppress `hermes.tool.progress` events in API responses | **Medium** – frequently requested by front‑end integrators. |

**Prediction**: The next minor release will likely include **UI QoL improvements** (auto‑scroll, Keep option), **security hardening** (credential‑store blocking), and **platform fixes** (Windows cron, Ollama reasoning). The GBrain plugin and session summaries may appear as experimental features.

## User Feedback Summary
Real pain points expressed today:

- **Trust erosion**: “Silent routing to Parallel.ai” (#45058) without user opt‑in is the highest‑reacted issue (👍15). Users expect explicit consent before external API calls.
- **Isolation frustration**: Concurrent session cross‑contamination (#46303) and shared memory injection break multi‑session workflows.
- **Desktop UI friction**: No auto‑scroll during streaming, model switcher not showing custom providers (#40480), inability to remove accounts (#45865), scrollbar covered by preview rail (#44140).
- **Reliability under load**: Response truncation (#7237), Matrix E2EE exhaustion (#46310), WebSocket timeouts (#44560).
- **Security anxiety**: Two new security issues (#46413, #46411) about credential file exposure show users are actively auditing the codebase. PR #46430 is already up – but users note that sibling‑profile exfiltration remains unfixed.
- **Configuration pain**: “Copy‑pasting base URL every time” (#46192), “no way to hide unconfigured providers” (#46304), “cron jobs broken on Windows” (#46332).

Overall sentiment is **active but wary** – the community is highly engaged in fixing problems, but the number of unresolved P1/P2 bugs (password leakage, cross‑contamination, silent routing) suggests the project needs to stabilise before adding more features.

## Backlog Watch
Issues that have been open for a longer period without visible maintainer traction:

| Issue | Created | Age | Priority | Why It Matters |
|-------|---------|-----|----------|----------------|
| [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) | 2026‑04‑10 | 66 days | – | 46 comments – response truncation was closed but no fix commit is visible; users still encounter the problem. Needs re‑evaluation. |
| [#12020](https://github.com/NousResearch/hermes-agent/issues/12020) | 2026‑04‑18 | 58 days | P3 | Suppress tool‑progress events – frequently requested by front‑end developers, no maintainer response. |
| [#13490](https://github.com/NousResearch/hermes-agent/issues/13490) | 2026‑04‑21 | 55 days | P3 | Configurable TUI status bar – author expressed clear use‑case; no follow‑up from maintainers. |
| [#23094](https://github.com/NousResearch/hermes-agent/issues/23094) | 2026‑05‑10 | 36 days | P3 | Fallback model stickiness config – relevant for production deployments; no activity. |
| [#42651](https://github.com/NousResearch/hermes-agent/issues/42651) | 2026‑06‑09 | 6 days | P3 | Desktop shows all cronjobs for every profile – cross‑profile leak, no maintainer comment. |
| [#40480](https://github.com/NousResearch/hermes-agent/issues/40480) | 2026‑06‑06 | 9 days | P3 | Custom provider models not shown in Desktop dropdown – blocks configuration workflow; no response. |

**Recommendation**: Maintainers should triage #7237 (re‑open or document fix), comment on #12020 and #13490 to set expectations, and address #40480 as it affects everyday Desktop usage. The long‑dormant feature requests may be candidates for community‑contributed PRs.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-15

## 1. Today’s Overview
The project saw moderate activity with **5 issues updated** (4 open, 1 closed) and **9 pull requests touched** (4 open, 5 merged/closed). A **new nightly build** (v0.2.9-nightly) was published, though it is marked as potentially unstable. The merged PRs all target stability and code quality: agent loop reload panic, TTS error handling, filesystem close-error hygiene, and structured logging. Community engagement remains visible through bug reports and feature requests, while maintainers are actively reviewing and merging fixes. Overall project health is stable, with a healthy cadence of bug squashing and incremental improvements.

## 2. Releases
- **[Nightly Build v0.2.9-nightly.20260615.13a38bd1](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260615.13a38bd1)** – Automated build from `main`; may be unstable.  
  **Full Changelog:** [compare v0.2.9…main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  No breaking changes or migration notes are included. Users are advised to use with caution.

## 3. Project Progress
Five pull requests were **merged or closed** today, all targeting stability and code quality:

- [#2904](https://github.com/sipeed/picoclaw/pull/2904) – **Fix agent loop reload and panic cleanup stability** – avoids blocked goroutines by making the reload path synchronous with `defer/recover`.
- [#3124](https://github.com/sipeed/picoclaw/pull/3124) – **fix(tts): handle `io.ReadAll` error in error response path** – prevents silent degradation when the TTS API returns a non‑200 status.
- [#3123](https://github.com/sipeed/picoclaw/pull/3123) – **fix(filesystem): explicitly ignore Close() error on directory file descriptor** – makes intentional error discard explicit, matching existing patterns.
- [#3122](https://github.com/sipeed/picoclaw/pull/3122) – **fix(evolution): capture Close() error on write file in `appendJSONLRecords`** – surfaces delayed write failures (e.g., disk full, NFS errors).
- [#3121](https://github.com/sipeed/picoclaw/pull/3121) – **refactor(openai_compat): replace `log.Printf` with structured logger** – removes the last raw `log.Printf` in the file, aligning with project conventions.

**Open feature PRs** under active development:
- [#3118](https://github.com/sipeed/picoclaw/pull/3118) – Add remote Pico WebSocket mode to `picoclaw agent` (new remote behavior).
- [#3120](https://github.com/sipeed/picoclaw/pull/3120) – `feat(config): add RegisterChannelSettings hook for out-of-tree channels` (extensibility without forking).
- [#3126](https://github.com/sipeed/picoclaw/pull/3126) – `fix(web): improve launcher allowlist bypass diagnostics` (clearer startup logs).
- [#2975](https://github.com/sipeed/picoclaw/pull/2975) – `feat(telegram): treat reply to bot message as mention in group chats` (stale but open).

## 4. Community Hot Topics
The most active Issues (by comments/reactions) are:

- [#3044](https://github.com/sipeed/picoclaw/issues/3044) – **Bug: `allow_from` fails for Matrix user IDs containing colon** (1 comment) – Matrix users cannot be whitelisted using the standard `@localpart:domain` format.  
- [#3041](https://github.com/sipeed/picoclaw/issues/3041) – **`mcp add` mis-parses global flags into positionals** (1 comment) – breaks `http/sse` adds and misnames stdio servers.  
- [#3090](https://github.com/sipeed/picoclaw/issues/3090) – **Panel does not work on Safari on iOS <16.4** (1 comment) – rendering failure on older iOS devices.  
- [#3125](https://github.com/sipeed/picoclaw/issues/3125) – **`web_search` tool fails silently when using Brave API key from `.security.yml`** (0 comments, posted today) – immediate “No results” response after key migration.

These issues reflect three core pain points: **configuration parsing**, **cross‑platform compatibility**, and **regression in API key handling**.

## 5. Bugs & Stability
New bugs reported today, ranked by severity:

| Issue | Summary | Severity | Fix PR exists? |
|-------|---------|----------|----------------|
| [#3125](https://github.com/sipeed/picoclaw/issues/3125) | `web_search` tool silently fails with Brave API key from new `.security.yml` | **High** – breaks a core tool without error logging | No |
| [#3041](https://github.com/sipeed/picoclaw/issues/3041) | `mcp add` mis‑parses global flags | **Medium** – prevents correct configuration of MCP servers | No |
| [#3044](https://github.com/sipeed/picoclaw/issues/3044) | `allow_from` fails for Matrix user IDs with colon | **Medium** – breaks Matrix channel access control | No |
| [#3090](https://github.com/sipeed/picoclaw/issues/3090) | Panel not working on Safari iOS <16.4 | **Low** – affects legacy browser versions | No |

**Stability patches** merged today (see Section 3) fixed a potential agent panic, TTS error handling, and multiple unhandled file‑close errors. The project is actively addressing technical debt.

## 6. Feature Requests & Roadmap Signals
- **[#2978](https://github.com/sipeed/picoclaw/issues/2978) – Add omniroute as provider** (closed as stale, 2 comments) – user requested a new provider; maintainers may reconsider if interest resurfaces.
- **[#3118](https://github.com/sipeed/picoclaw/pull/3118) – Remote Pico WebSocket mode** – likely to land in the next minor version, enabling headless/remote agent operation.
- **[#3120](https://github.com/sipeed/picoclaw/pull/3120) – `RegisterChannelSettings` hook** – a significant extensibility improvement for third‑party channel support, likely to be merged soon.
- **[#2975](https://github.com/sipeed/picoclaw/pull/2975) – Telegram reply‑as‑mention** – stale but low‑risk; could ship in a future release if revived.

**Predicted next release focus:** remote agent mode, extensible channel config, and fixes for the critical `web_search` regression.

## 7. User Feedback Summary
- **Pain points:**  
  - `web_search` tool completely broken after `.security.yml` migration ([#3125](https://github.com/sipeed/picoclaw/issues/3125)).  
  - `mcp add` command unusable with certain flags ([#3041](https://github.com/sipeed/picoclaw/issues/3041)).  
  - Matrix channel access control incorrectly rejects standard user IDs ([#3044](https://github.com/sipeed/picoclaw/issues/3044)).  
  - Safari users on older iOS cannot access the panel ([#3090](https://github.com/sipeed/picoclaw/issues/3090)).  
- **Feature desires:** omniroute provider integration ([#2978](https://github.com/sipeed/picoclaw/issues/2978)).  
- **Satisfaction:** The high merge rate (5 PRs in one day) and responsiveness to bug reports indicate an active maintainer team that values stability.

## 8. Backlog Watch
Items that have been open for ⩾1 week without maintainer response or significant activity:

- **[#2975](https://github.com/sipeed/picoclaw/pull/2975) – Telegram reply‑as‑mention** – open since May 30, no recent maintainer interaction.  
- **[#3041](https://github.com/sipeed/picoclaw/issues/3041) – `mcp add` flag mis‑parsing** – stale since June 7, no assignee.  
- **[#3044](https://github.com/sipeed/picoclaw/issues/3044) – Matrix `allow_from` bug** – stale since June 7, one user comment but no maintenance update.  
- **[#3090](https://github.com/sipeed/picoclaw/issues/3090) – Safari iOS <16.4 panel issue** – stale since June 10, no resolution.

These items may require maintainer triage to assign priority or request additional information. The **`web_search` regression** (#3125) opened today should be fast‑tracked given its severity.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-15

## 1. Today’s Overview

NanoClaw saw elevated activity on **2026-06-14**, with 7 issues and 10 pull requests updated. The project is in a **feature+hardening phase**: three critical security vulnerabilities were reported (file exfiltration, local approval bypass, hidden MCP server arguments), a long-standing budget-drop bug now has a fix PR, and two major feature PRs — operator-driven provider selection and the Codex agent provider v2 — were merged to trunk. Documentation fixes and a container infrastructure change (data-driven CLI installs) also landed. No new releases were cut. Overall, maintainer attention is split between urgent security patches and preparing the provider-selection seam for v2 providers.

---

## 2. Releases

*None.* No new releases were published in the last 24 hours.

---

## 3. Project Progress

Five pull requests were merged or closed today:

- **#2764 `docs(CLAUDE.md): fix two relocated Key Files paths`** (by glifocat) — Closes #2763. Corrects stale file references in the Key Files table of `CLAUDE.md`.  
- **#2769 `docs(add-codex): flag interactive auth step + add host-restart step`** (by Koshkoshinsk) — Documentation-only update to the `/add-codex` skill, noting that `provider-auth codex` requires an interactive TTY session and that host restart is needed after installation.  
- **#2757 `feat(codex): Codex agent-provider payload v2 — app-server on capability seams, vault-only auth`** (by omri-maya) — Replaces the old Codex payload with v2, treating Codex as a full agent provider authenticated solely through OneCLI’s vault. Only Codex-specific files are changed; OpenCode payload is untouched.  
- **#2756 `feat(providers): operator-driven provider selection, switching, and memory migration`** (by omri-maya) — Introduces the provider seam: a registry, setup picker, installer, vault auth walkthrough, and memory-migration skill. Non-default provider payloads (starting with Codex) are installed from separate branches.  
- **#2758 `feat(container): data-drive global CLI installs from cli-tools.json`** (by gavrielc) — Replaces hardcoded `ARG`/`RUN` blocks in the Dockerfile with a `container/cli-tools.json` manifest. Skills add a JSON row to install a new CLI tool, improving maintainability.

---

## 4. Community Hot Topics

Although none of the issues or PRs accumulated comments or reactions (all show `0`), the following items drew clear attention from maintainers (multiple related PRs and cross-references):

- **#2762 `[Security] NanoClaw add_mcp_server approval flow allows hidden args and env`** (by YLChen-007) — A security advisory detailing how an attacker-controlled agent can hide `args` and `env` from the human approver during MCP server addition. Underlying need: **approval transparency for agent self-modification operations**.  
- **#2761 `[Security] Local gateway approval bypass via unauthenticated loopback webhook`** (by YLChen-007) — The Chat SDK gateway bridge starts an unauthenticated localhost webhook, allowing any local process to forward forged events. Underlying need: **proper authentication for internal webhooks**.  
- **#2760 `[Security] Arbitrary local file exfiltration via send_file absolute path handling`** (by YLChen-007) — The `send_file` MCP tool copies files from absolute paths without constraint, enabling exfiltration of any readable file. Underlying need: **path sanitization or whitelisting in file tools**.  
- **#2751 `Budget-exhausted LLM turns are silently dropped — user gets no reply`** (by assapin) — Unhandled `spending limit reached` errors cause silent message loss. A fix PR #2759 is open. Underlying need: **error handling for budget/token exhaustion should notify the user**.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix status |
|----------|-------|-------------|------------|
| **Critical** | #2762 | Hidden `args`/`env` in MCP server approval | No PR yet; under triage |
| **Critical** | #2761 | Unauthenticated loopback webhook bypass | No PR yet; under triage |
| **Critical** | #2760 | Arbitrary file exfiltration via `send_file` | No PR yet; under triage |
| **High** | #2751 | Budget-exhausted turns silently dropped | PR #2759 open (fix) |
| **Low** | #2763 | Stale file paths in CLAUDE.md (closed) | Fixed in #2764 |

The three security issues (#2762, #2761, #2760) are the highest priority due to their potential for privilege escalation and data leakage. All three were reported by the same researcher (YLChen-007) and are currently open with no linked fix PR. The budget-drop bug (#2751) has an active fix PR (#2759) that delivers the error to the user instead of dropping it.

---

## 6. Feature Requests & Roadmap Signals

- **#2768 `Enable prompt caching by default in Claude provider`** — A small but impactful request to set `enablePromptCaching` in the Claude SDK, saving tokens for agents with large system prompts. Likely to be included in the next minor release once validated.  
- **#2767 `Telegram: legacy-Markdown sanitizer is obsoleted by @chat-adapter/telegram@4.30.0`** — Marks a legacy workaround as unnecessary after an upstream fix. The sanitizer should be removed or gated.  
- **Provider selection & Codex v2** (from merged PRs #2756, #2757) — These features establish NanoClaw’s architecture for pluggable LLM providers. The next release will likely include the provider registry UI/CLI and the Codex payload v2.  
- **Health audit fixes** (PR #2732, still open) — A broad hardening PR from a multi-agent security audit. If merged, it will address a range of medium-severity issues in the host and agent-runner.

**Prediction for next version (v0.x)** : Expect prompt caching toggle, Telegram MarkdownV2 adoption, budget error delivery, and the merged provider-selection seam + Codex v2. Security fixes for the three critical issues may ship as a patch release.

---

## 7. User Feedback Summary

Real user pain points evident from today’s data:

- **Silent failures** (budget exhaustion, #2751) — users send a message and get no reply, eroding trust. The fix PR #2759 addresses this directly.  
- **Security concerns** (#2760, #2761, #2762) — users operating agents with MCP tools or on multi-tenant deployments face real risks of data exfiltration and approval bypass. There is no indication of exploitation, but the severity demands immediate attention.  
- **Documentation friction** (#2763) — stale paths in CLAUDE.md cause confusion for AI coding assistants and human readers. The fix was merged same day, showing responsive maintainer attitude.  
- **Complex onboarding** (add-codex skill, #2769) — users attempting to set up the Codex provider hit a missing interactive auth step and a needed host restart. The docs PR clarifies the workflow.

Satisfaction signals: The prompt caching request (#2768) and Telegram improvement (#2767) are optimisation/quality-of-life requests rather than complaints, suggesting that core functionality is stable enough for users to want polishing.

---

## 8. Backlog Watch

- **PR #2732 `Harden host + agent-runner from health audit findings`** — Open since 2026-06-11, with 19 files changed. Addresses multiple security and stability issues from an adversarial audit. Needs maintainer review to avoid conflict with the three newly reported security issues.  
- **Issue #2751 `Budget-exhausted LLM turns silently dropped`** — Created 2026-06-12, still open but with an active fix PR #2759. No signs of maintainer delay.  
- **Security issues #2760, #2761, #2762** — All created 2026-06-14, no assignee yet. They should be triaged within the next 48 hours to avoid prolonged exposure.

No issues over a week old remain unanswered. Overall backlog health is good, but the sudden influx of security reports will require dedicated attention to avoid backlog growth.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-06-15

## 1. Today’s Overview
Project activity is minimal today. Only one issue (#955) was updated, and no pull requests or releases were recorded. The sole open item is a feature request for identity‑based authentication in the Azure OpenAI LLM provider. With zero PR activity and no merged changes, the repository appears to be in a low‑activity phase. Maintainer engagement or community contributions have been absent in the last 24 hours.

## 2. Releases
No new releases exist for this period.

## 3. Project Progress
- **Merged/Closed PRs today:** None  
- **Features advanced or fixed:** None  

No pull requests were updated, merged, or closed today.

## 4. Community Hot Topics
The only active issue is **#955**, but it has **0 comments** and **0 reactions**, so it does not qualify as a “hot topic.” The community shows no active discussion or engagement on any item.

- **#955** [OPEN] [enhancement] Identity based authentication support for Azure OpenAI LLM Provider  
  *Author: kunalk16* | Created/Updated: 2026-06-15  
  [Link to issue](https://github.com/nullclaw/nullclaw/issues/955)

**Underlying need:** Users want to leverage `DefaultTokenCredential` (via Azure CLI login) for authentication, likely to comply with organizational security policies that restrict API‑key usage.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The project shows no stability issues in this snapshot.

## 6. Feature Requests & Roadmap Signals
The only feature request is **#955** – identity‑based authentication for Azure OpenAI. Given the single issuance and lack of community discussion, it is unlikely to appear in the next release unless the maintainer acts on it soon. However, similar security‑driven requests could gain traction if broader Azure‑based usage grows.

## 7. User Feedback Summary
- **Real pain points:** One user (kunalk16) explicitly cites security policies that prevent API‑key usage in Azure subscriptions, highlighting a friction point for enterprise deployments of the Azure OpenAI provider.  
- **Use cases:** Enterprise environments requiring managed identities or developer credentials from `az login`.  
- **Satisfaction/dissatisfaction:** No direct satisfaction signals; the absence of any other feedback suggests either limited active user base or that existing functionality meets most needs.

## 8. Backlog Watch
No long‑unanswered important issues or stale PRs requiring maintainer attention were identified. The single open issue was created today, so it is not yet a backlog concern. Continued dormancy could, however, signal a need for maintainer response to encourage further contribution.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-15

## 1. Today's Overview
IronClaw continues at a high activity cadence, with **39 issues** and **44 pull requests** updated in the last 24 hours. 7 issues were closed and 17 PRs were merged or closed, reflecting steady progress on both feature work and urgent security fixes. No new releases were published. The project’s focus remains on hardening the Reborn stack (attachments, observability, non‑breaking runtime context) while addressing a wave of **shell tool approval bypass vulnerabilities** that surfaced over the past 48 hours. The simultaneous push on **engineering productivity** (dogfooding IronClaw to improve its own development lifecycle) signals a maturing AI‑native workflow.

## 2. Releases
*None.* No new versions were cut. The next release (PR [#3708](https://github.com/nearai/ironclaw/pull/3708)) has been open since 2026-05-16 and carries breaking changes in `ironclaw_common` and `ironclaw_skills`.

## 3. Project Progress
**Merged / closed pull requests (from top 20 by engagement):**

- [#4738](https://github.com/nearai/ironclaw/pull/4738) **[CLOSED]** – feat(reborn): attachment web UX on the WebChat v2 SPA. Wires upload UX for the attachment pipeline, closing a critical gap in the Reborn front‑end.
- [#4836](https://github.com/nearai/ironclaw/pull/4836) **[CLOSED]** – feat(runtime-context): surface connected channels, delivery state, and run origin. Informs the model about communication state at each loop start.
- [#4873](https://github.com/nearai/ironclaw/pull/4873) **[CLOSED]** – test(slack): re­home approval→auth→final-reply delivery e2e. Restores a previously broken Slack integration test.

Additional closed items (not in top 20 but part of the 17 merged/closed PRs) include dependency bumps and smaller fixes. The rate of closed PRs indicates active merging despite the open security investigations.

**Issues closed today:**
- [#4851](https://github.com/nearai/ironclaw/issues/4851) – trusted‑trigger origin laundering through strings (design fix).
- [#4848](https://github.com/nearai/ironclaw/issues/4848) – auth‑resume identity matching by `input_ref`.
- [#4847](https://github.com/nearai/ironclaw/issues/4847) – re‑home Slack e2e test (resolved by PR #4873).
- [#4751](https://github.com/nearai/ironclaw/issues/4751) – large response request failure (tool arguments >16KB, closed as fixed).
- [#3515](https://github.com/nearai/ironclaw/issues/3515) – WeChat channel docs (closed after merge).

## 4. Community Hot Topics

- **Security: Shell Approval Bypasses**  
  Five related security advisories filed by **YLChen-007** ([#4861](https://github.com/nearai/ironclaw/issues/4861) through [#4865](https://github.com/nearai/ironclaw/issues/4865)) detail ways to evade the `shell` tool’s risk classification: newline‑chained commands, `env`/`sort --compress-program` wrappers, and prior auto‑approval inheritance. These have the highest severity and are generating significant internal attention (no fix PRs yet). The community need is immediate: a hardened command risk classifier that cannot be bypassed by trivial shell grammar tricks.

- **Engineering Productivity Initiative**  
  A set of five issues authored by **think-in-universe** ([#4878](https://github.com/nearai/ironclaw/issues/4878) – #4883) proposes using IronClaw itself to accelerate its own development – coding agents, preview deployments, automated code review, and test coverage tracking. This reflects a desire to shift toward an AI‑native development loop and is likely to guide the project’s tooling roadmap for the coming weeks.

- **Reborn Attachment Pipeline (Issue #4644)**  
  The “universal attachments” meta‑issue ([#4644](https://github.com/nearai/ironclaw/issues/4644)) continues to attract interest. The v1 attachment pipeline has been wired into Reborn via merged PR #4738, and a follow‑up PR [#4871](https://github.com/nearai/ironclaw/pull/4871) adds actual image pixel transmission for vision‑capable models. The underlying need is a consistent attachment experience across all channel surfaces.

## 5. Bugs & Stability

| Severity | Bug | Status |
|----------|-----|--------|
| **Critical** | Multiple `shell` tool approval bypasses (newline chains, wrapper commands, symlink escapes) [#4861](https://github.com/nearai/ironclaw/issues/4861)–[#4865](https://github.com/nearai/ironclaw/issues/4865) plus existing `write_file` dangling symlink escape [#4797](https://github.com/nearai/ironclaw/issues/4797) | No fix PRs yet; under investigation |
| **High** | WebChat v2 “Illegal invocation” on plain HTTP from non‑localhost host [#4874](https://github.com/nearai/ironclaw/issues/4874) | Open; likely a `navigator.mediaDevices` permission issue |
| **Medium** | Reborn WebSocket helper uses `?token=` auth while v2 auth contract rejects query tokens on WS route [#4870](https://github.com/nearai/ironclaw/issues/4870) | Open; workaround noted |
| **Low** | Settings provider action buttons clip offscreen on mobile [#4868](https://github.com/nearai/ironclaw/issues/4868); Clean state incorrectly shows NEAR AI provider as Active [#4857](https://github.com/nearai/ironclaw/issues/4857); Shell command not visible in approval dialog [#4852](https://github.com/nearai/ironclaw/issues/4852) | Open; cosmetic and UX issues |
| **Low** | Google Calendar OAuth flow requests access token instead of guiding flow [#4884](https://github.com/nearai/ironclaw/issues/4884) | Open; new issue |

The shell security bugs are the most pressing stability risk. The project is responding with targeted PRs (e.g., [#4835](https://github.com/nearai/ironclaw/pull/4835) fixing persistent approval scope, [#4840](https://github.com/nearai/ironclaw/pull/4840) reordering credential gate before approval gate), but a comprehensive shell approval redesign may be needed.

## 6. Feature Requests & Roadmap Signals

- **Image attachment support for vision models** – PR [#4871](https://github.com/nearai/ironclaw/pull/4871), follow‑on to [#4644](https://github.com/nearai/ironclaw/issues/4644), likely to land in next release.
- **Observability seams for benchmarking** – PR [#4588](https://github.com/nearai/ironclaw/pull/4588) adds trajectory observer and LLM provider injection for external evaluation (nearai‑bench).
- **Non‑borking Reborn failures** – PR [#4841](https://github.com/nearai/ironclaw/pull/4841) aims to explain and recover from run‑terminal errors instead of crashing.
- **Gated final‑answer nudge** – PR [#4837](https://github.com/nearai/ironclaw/pull/4837) prevents empty/canned turn endings in Reborn.
- **Google Calendar extension** – two open issues [#4884](https://github.com/nearai/ironclaw/issues/4884) and [#4885](https://github.com/nearai/ironclaw/issues/4885) highlight OAuth flow and findings; likely to be addressed in a Reborn extension polish cycle.
- **Slack as product‑adapter extension** – PR [#4778](https://github.com/nearai/ironclaw/pull/4778) removes Slack from hardcoded channel list, moving it to an extension manifest.

These features suggest the next minor release (0.29.x or 0.30.0) will include:
- Reborn attachment UX (images + formats)
- Observability hooks for external tooling
- Better failure handling in Reborn
- Security fixes for the shell tool
- Slack as an extension

## 7. User Feedback Summary

- **Positive:** The engineering team is dogfooding their own product, filing detailed local usability reports ([#4879](https://github.com/nearai/ironclaw/issues/4879), [#4692](https://github.com/nearai/ironclaw/issues/4692)). This shows confidence in Reborn as a daily‑driver agent.
- **Pain points:** Security researcher **YLChen-007** has uncovered systemic flaws in the shell approval classifier. Users on Reborn report missing command details in approval dialogs and non‑intuitive OAuth flows for Google Calendar. Mobile UI clipping and WebSocket auth mismatches also degrade the user experience.
- **Usability friction:**  The “Illegal invocation” error on non‑localhost HTTP and the clean‑state provider mislabeling can confuse first‑time users, especially those setting up Reborn over a network.
- **Satisfaction:** Active PR throughput (44 updated in 24h) and rapid closure of issues (7 closed) indicate a responsive maintainer team. The engineering productivity initiative (#4878) suggests the team is serious about long‑term velocity.

## 8. Backlog Watch

- **Release PR [#3708](https://github.com/nearai/ironclaw/pull/3708)** – Open since 2026-05-16, this automated release PR contains breaking changes in `ironclaw_common` and `ironclaw_skills`. It has not been merged for a month, suggesting blockers or a deliberate hold. This may delay delivery of many in‑flight features.
- **Dependency update PRs** – Several large dependency bumps (e.g., [#4876](https://github.com/nearai/ironclaw/pull/4876) with 43 updates, [#4002](https://github.com/nearai/ironclaw/pull/4002) with 16 updates) have been open for weeks. While not blocking, they carry security risk (e.g., `rustls` and `agent-client-protocol` updates).
- **Observing PR [#4588](https://github.com/nearai/ironclaw/pull/4588)** – Open since 2026-06-09 (6 days), this XL‑sized feature for observability seams may require careful review before merging.
- **Security issues** – The five shell approval bypass issues have no assigned fix PRs yet. Given their criticality, maintainer attention is urgently needed.

*All links are to the GitHub repository `github.com/nearai/ironclaw`. Issue/PR numbers are clickable.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-15

## 1. Today's Overview
Activity on 2026-06-15 was low, with no new issues or pull requests created in the last 24 hours. Two existing issues and three open PRs were updated on 2026-06-14, and one long-standing PR (#1465) was finally closed. The project appears stable, with feature development (in-session search, power‑save blocking, session timer) advancing in the open PR pipeline, but several user‑reported UI bugs remain unresolved for over two months. No new releases were published.

## 2. Releases
*None.* No new releases were tagged or published in the reported period.

## 3. Project Progress
**Merged / Closed PRs** (last 24h):
- **PR #1465** – [CLOSED] `fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现`  
  Author: linlihua | [GitHub](https://github.com/netease-youdao/LobsterAI/pull/1465)  
  *Fix:* After deleting a scheduled task, the corresponding local session record in SQLite was not removed, causing the task to reappear as a ghost session after restart. The fix now cleans up the `cowork_sessions` entry during task deletion. This resolves a long‑standing reliability issue (associated Issue #1359).

No other PRs were merged today. Three open PRs (#1429, #1430, #1431) remain under review, all targeting the cowork session experience.

## 4. Community Hot Topics
**Most commented / reacted issues and PRs** (last 24h updates):
- **Issue #1434** – [OPEN] [stale] 语言为中文时，搜索无数据显示英文提示  
  Author: xuzx-code | [GitHub](https://github.com/netease-youdao/LobsterAI/issues/1434)  
  Comments: 1 | 👍: 0  
  *Analysis:* English UI strings persist even when LobsterAI is set to Chinese, breaking localization expectations for the agent skill search page. This indicates incomplete i18n coverage for empty‑state components.

- **Issue #1435** – [OPEN] [stale] 新建自定义agent时，名称过长超出弹框  
  Author: xuzx-code | [GitHub](https://github.com/netease-youdao/LobsterAI/issues/1435)  
  Comments: 1 | 👍: 0  
  *Analysis:* No character limit or truncation on agent name input leads to visual overflow in the creation dialog. A minor UI bug that degrades first‑impression usability.

Both issues were raised on 2026-04-03 and have received only one comment each (likely from the reporter), reflecting a possible lack of maintainer responsiveness.

## 5. Bugs & Stability
No new bug reports were filed today. Two existing bugs (see above) remain open and unchanged:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#1434](https://github.com/netease-youdao/LobsterAI/issues/1434) | Medium | Chinese locale shows English empty‑state text in agent skill tab | No |
| [#1435](https://github.com/netease-youdao/LobsterAI/issues/1435) | Low | Agent name overflow in creation dialog | No |

No crashes or regressions were reported in the last 24h. The previously closed ghost‑session bug (PR #1465) was the most significant stability issue recently addressed.

## 6. Feature Requests & Roadmap Signals
No explicit user feature requests were posted today. However, three open feature PRs (all stale since April) indicate the team’s roadmap priorities for the cowork session experience:
- **In‑session message search** [#1429](https://github.com/netease-youdao/LobsterAI/pull/1429) – real‑time keyword highlighting via `mark.js`
- **Power‑save prevention** [#1430](https://github.com/netease-youdao/LobsterAI/pull/1430) – keeps system from sleeping during long agent runs
- **Session elapsed timer** [#1431](https://github.com/netease-youdao/LobsterAI/pull/1431) – real‑time timer in StreamingActivityBar

These features (if merged) would be strong candidates for the next minor release. The lack of user‑driven requests today suggests the project is currently in a “polish and ship” phase rather than ideation.

## 7. User Feedback Summary
The two open issues provide direct user pain points, both from the same reporter (xuzx-code):
- **Localization gaps** – Chinese users encounter English UI elements, reducing trust and accessibility.
- **Form overflow** – No input validation on agent name length leads to an unpolished experience when creating custom agents.

No positive feedback or use‑case stories were visible in the data. The project appears to be used for automated agent tasks (indicated by the cowork session timer and scheduled task features), but user satisfaction signals are absent from the last 24 hours.

## 8. Backlog Watch
Several important items have languished without maintainer action for over two months:

| Item | Type | Last Updated | Days Stale | Notes |
|------|------|--------------|------------|-------|
| [#1434](https://github.com/netease-youdao/LobsterAI/issues/1434) – i18n bug | Issue | 2026-06-14 | 72 | Only comment is from reporter; no assignee |
| [#1435](https://github.com/netease-youdao/LobsterAI/issues/1435) – name overflow | Issue | 2026-06-14 | 72 | Same as above |
| [#1429](https://github.com/netease-youdao/LobsterAI/pull/1429) – message search | PR | 2026-06-14 | 72 | Pending review; conflicts may exist |
| [#1430](https://github.com/netease-youdao/LobsterAI/pull/1430) – power save block | PR | 2026-06-14 | 72 | Pending review |
| [#1431](https://github.com/netease-youdao/LobsterAI/pull/1431) – session timer | PR | 2026-06-14 | 72 | Pending review |

All of these were created or last active on 2026-04-03 or 2026-04-04. The closed PR #1465 (ghost sessions) took more than two months to merge. This pattern suggests a stretched maintenance capacity. The community would benefit from an update or triage on these long‑standing items.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-15

## 1. Today's Overview
Activity on the Moltis codebase over the past 24 hours has been minimal: one new enhancement issue was filed, no pull requests were opened or merged, and no new releases were published. The project appears to be in a quiet state, with no signs of urgent maintenance or ongoing feature work visible from the public tracker. The single open issue suggests the community is still actively proposing ideas, but the lack of merged changes or closed items indicates low development throughput today.

## 2. Releases
None. No new releases were published in the last 24 hours, and no pre-existing releases were updated.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. No feature advances or bug fixes were committed to the repository based on the provided data.

## 4. Community Hot Topics
The only item updated in the last 24 hours is:

- **#1123 (open, enhancement) – Add pure-Rust turbovec as an alternative memory backend for extreme edge compression**  
  Author: joeblew999 | Created/Updated: 2026-06-14 | Comments: 0 | 👍: 0  
  **Link:** [moltis-org/moltis Issue #1123](https://github.com/moltis-org/moltis/issues/1123)

While currently without comments or reactions, this proposal addresses a clear community desire for lower-footprint vector storage, especially for edge-device deployments. The request suggests introducing a pure-Rust backend (turbovec) to improve compression without sacrificing performance. Given that similar “memory backend” issues are common in vector database projects, this signals growing interest in Rust-native, minimal-dependency components.

## 5. Bugs & Stability
No bug reports, crashes, or regressions were filed in the last 24 hours. The project shows no active stability concerns based on the data.

## 6. Feature Requests & Roadmap Signals
The only feature request today is **#1123** (see above). If the maintainers are receptive to alternative memory backends, this could be a candidate for inclusion in a future minor release (v0.x). The request’s emphasis on “extreme edge compression” aligns with trends in on-device AI and embedded systems, making it a plausible roadmap item. No other requests were raised, so the roadmap outlook remains unchanged from previous days.

## 7. User Feedback Summary
No user complaints, satisfaction comments, or specific use-case descriptions were posted in the tracker today. The absence of discussion may indicate that the current release meets most users’ needs, or that the community is waiting for updates to engage more actively.

## 8. Backlog Watch
No long-unanswered important issues or outstanding PRs requiring maintainer attention were identified from the provided data. The single open issue (#1123) is only one day old, so it does not yet qualify as backlog. The project appears to have a clean, low-traffic issue tracker at this moment.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-15

## 1. Today's Overview

The CoPaw repository (QwenPaw desktop client and agent framework) shows **high community activity** with 17 issues and 12 pull requests updated in the last 24 hours. No new releases were published. The project is in a **bug-fix and feature-acceleration phase** following the recent v1.1.11.post2 release. Several regressions and user-reported blockers (Gemini tool calling, Windows startup slowdown, local model provider visibility) are under active investigation, while a wave of first-time contributors is driving quality-of-life improvements (Vietnamese locale, session filtering, cron heartbeat fixes). The maintainers have not merged any PRs today, indicating a review or testing backlog.

## 2. Releases

**No new releases** were published in the last 24 hours. The latest available version remains **v1.1.11.post2**, which is the subject of several reported regressions (see **Bugs & Stability**).

## 3. Project Progress

**No pull requests were merged or closed today.** All 12 open PRs are still awaiting review or further changes. Notable PRs that represent progress toward feature delivery and bug fixes include:

- **Desktop port persistence** ([#5051](https://github.com/agentscope-ai/QwenPaw/pull/5051)) – fixes localStorage reset on Windows restart (issue #4733).
- **Cron/heartbeat timeout increase and autonomous context prompt** ([#5180](https://github.com/agentscope-ai/QwenPaw/pull/5180)) – addresses silent failures in multi-step cron tasks.
- **Multi-agent collaboration skill keyword expansion** ([#5179](https://github.com/agentscope-ai/QwenPaw/pull/5179)) – improves trigger reliability.
- **Vietnamese locale support** (two PRs: [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175) and superseding [#5186](https://github.com/agentscope-ai/QwenPaw/pull/5186)) – full 40-section translation.
- **Built-in PRD CRUD tool with frontend** ([#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902)) – replaces plugin-based tool.
- **Windows GUI automation with UIA + Tauri Control Mode** ([#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)) – new `computer_use` builtin tool.
- **Session filter by title** ([#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178)).
- **Request payload transforms via host SDK** ([#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188)).
- **Plugin command suggestions with cross-tab language sync** ([#5189](https://github.com/agentscope-ai/QwenPaw/pull/5189)).
- **Tool card loading spinner fixes** ([#5141](https://github.com/agentscope-ai/QwenPaw/pull/5141)).
- **Approval command word-break fix** ([#5176](https://github.com/agentscope-ai/QwenPaw/pull/5176)).

## 4. Community Hot Topics

The most active issues and PRs (by comment count) reflect three major areas of community concern:

### a) Local model provider not showing after update ([#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184))
- **Comments:** 2 | **Status:** Open  
- User reports that locally created model providers introduced in v1.1.11 are not displayed in v1.1.11.post2. This is a high-visibility regression for users who rely on local LLMs.

### b) Request for kimi-for-coding / uv whitelist ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156))
- **Comments:** 5 | **Status:** Open  
- Users subscribed to Kimi coding plans cannot use the service through QwenPaw because only the official API is supported. The request asks for whitelisting `kimi-for-coding` and `uv`. This signals a clear demand for broader model provider ecosystem integration.

### c) Windows Tauri desktop startup slowness ([#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047))
- **Comments:** 5 | **Status:** Closed (question answered?)  
- The switch from Python packaging to Tauri caused startup times to balloon from 1–2 minutes to **10+ minutes** on Windows 11, with frequent unresponsiveness. While closed, the underlying issue may not be fully resolved – users still report slow startups in other threads.

Other active threads: Python 3.13 plugin installation failure (`imghdr` missing, [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166), 2 comments), long conversation freeze ([#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161), 2 comments), and Wayland pet feature incompatibility ([#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183), 2 comments).

## 5. Bugs & Stability

**Severity: High**

| Bug | Issue | Impact | Fix PR Exists? |
|-----|-------|--------|----------------|
| **Gemini tool calling regression** in v1.1.11.post2 | [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) – 1 comment | Tool calling broken for Gemini users; known good version was v1.1.10 | No |
| **Local model providers not showing** | [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184) – 2 comments | Cannot use locally configured models after upgrade | No |
| **Context compression loss** – removes all context when persona file token threshold is exceeded | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) – 1 comment | Task interruption, complete information loss | No |
| **Long conversation freeze** – agent stops responding after many turns | [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) – 2 comments | Core usability broken for power users | No |
| **Cron/heartbeat agent not executing heavy tasks** | [#5174](https://github.com/agentscope-ai/QwenPaw/issues/5174) – 1 comment | Scheduled automation ineffective | Yes – [#5180](https://github.com/agentscope-ai/QwenPaw/pull/5180) |
| **Plugin pip install spam cmd windows** on Windows when PyPI unreachable | [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) – 1 comment | Desktop flashing, resource waste | No |
| **Wayland desktop pet feature broken** | [#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183) – 2 comments | Pet functionality unusable on Niri WM | No |
| **DingTalk channel messages not recorded in chats.json** | [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177) – 1 comment | Sessions invisible in console frontend | No |
| **Python 3.13 TeamChat plugin failure** (`imghdr` removed) | [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) – 2 comments | Plugin installation fails on Python 3.13 | No |
| **Packaged build white screen** (spec references non-existent modules) | [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165) – 1 comment | Exe built but unusable | No |
| **Thinking loop bug** | [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) – 1 comment | Agent stuck in infinite thinking | No |

**Severity: Medium**

- Desktop port randomization resets localStorage on every restart ([PR #5051](https://github.com/agentscope-ai/QwenPaw/pull/5051) open for fix).
- Cron/heartbeat timeout too short for multi-step operations ([PR #5180](https://github.com/agentscope-ai/QwenPaw/pull/5180) open).
- Multi-agent collaboration keyword missing ([PR #5179](https://github.com/agentscope-ai/QwenPaw/pull/5179) open).
- Feishu CardKit streaming slow for long replies ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)).

## 6. Feature Requests & Roadmap Signals

Strong community demand for:

- **More model provider integrations** – specifically `kimi-for-coding` and `uv` ([#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)). This aligns with the PR [#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188) (request payload transforms), which could facilitate custom provider adapters.
- **Real-time HH:MM:SS timestamp in agent context** ([#5185](https://github.com/agentscope-ai/QwenPaw/issues/5185)) – to avoid extra tool calls for time.
- **Official Zalo Bot channel** ([#5168](https://github.com/agentscope-ai/QwenPaw/issues/5168)) – demand from Vietnamese users; note that a full Vietnamese locale PR is already submitted.
- **Feishu CardKit streaming optimization** ([#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)) – performance-tuned incremental updates.
- **Unified model configuration** for vector, text, audio/video models ([#5182](https://github.com/agentscope-ai/QwenPaw/issues/5182)).
- **Windows GUI automation** is already being addressed by PR [#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) (`computer_use` tool).
- **Plugin command suggestions** and cross-tab language sync (PR [#5189](https://github.com/agentscope-ai/QwenPaw/pull/5189)).

**Prediction for next version:** The next release is likely to include the desktop port persistence fix, cron/heartbeat improvements, multi-agent collaboration reliability, Vietnamese locale, session filtering, and possibly the PRD CRUD tool and plugin command suggestions. The Gemini regression and Windows startup slowness may require further investigation before inclusion.

## 7. User Feedback Summary

**Satisfaction:**
- Community is actively contributing (multiple first-time PRs).
- Feishu integration works but has performance caveats.
- Agent functionality (DingTalk, cron) generally works but has edge cases.

**Dissatisfaction / Pain Points:**
- **Windows desktop startup time** is the #1 complaint – 10+ minutes is unacceptable for desktop users.
- **Regressions in v1.1.11.post2** – multiple features that worked in v1.1.10 are now broken (Gemini tool calling, local model providers).
- **Plugin ecosystem friction** – Python 3.13 incompatibility, pip dependency window spam, and lack of `kimi-for-coding` support.
- **Core stability issues** – context compression losing data, long conversation freezes, thinking loops, and cron/heartbeat unreliability.
- **Missing channel support** – Zalo users feel left out; DingTalk sessions not appearing in console is confusing.
- **Feishu streaming** is too slow for long replies, degrading user experience.

## 8. Backlog Watch

Several important issues have received few comments but require maintainer attention:

| Issue | Days Open | Potential Impact | Notes |
|-------|-----------|------------------|-------|
| [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) – Gemini regression | 3 | Breaks core functionality for Gemini users | No fix PR yet; critical to revert or patch. |
| [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) – Context compression loss | 2 | Data loss, task interruption | No fix PR. |
| [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) – Long conversation freeze | 3 | Core usability barrier | No fix PR. |
| [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) – Thinking loop | 3 | Agent unusable in some scenarios | No fix PR. |
| [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177) – DingTalk session not saved | 2 | Channel integration broken | No fix PR. |
| [#5165](https://

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-15

## Today’s Overview

The ZeroClaw project continues at a high velocity, with 42 issues and 50 pull requests updated in the last 24 hours. Of those, 28 issues were closed and 3 PRs were merged, indicating sustained triage and delivery velocity despite a bulk of open PRs (47) awaiting review. No new releases were cut today; the latest release remains the v0.7.5-debian Docker image referenced in closed issue #6760. The community remains highly engaged, with several multi-comment RFCs and bug reports driving both architectural discussions and concrete fixes. Project health appears strong, with a clear pattern of rapid feature integration (especially new providers, tools, and channels) alongside active stability work.

## Releases

No new releases in the last 24 hours.

## Project Progress

Three pull requests were merged or closed today:

- **PR #7594 (merged)** — `feat(config): type-driven alias-ref pickers and self-declaring config enums` (size: XL, risk: high). This large internal refactor eliminates hardcoded per-path special-casing in configuration field UX, making field behavior derive from Rust types. On-disk TOML and runtime behavior are unchanged.  
  [zeroclaw-labs/zeroclaw PR #7594](https://github.com/zeroclaw-labs/zeroclaw/pull/7594)

- **PR #7384 (merged)** — `feat(cron): add a pause/resume toggle to scheduled tasks` (size: S, risk: medium). Adds a UI toggle for pausing cron jobs from the dashboard, leveraging existing data model support.  
  [zeroclaw-labs/zeroclaw PR #7384](https://github.com/zeroclaw-labs/zeroclaw/pull/7384)

- **Third merged/closed PR** (not listed in top 20) likely contributed to the overall count but its details are not available in the sampled data.

Additionally, **Issue #7415**, the RFC for unifying the three agent turn engines, was **closed** as implemented via a consolidation PR (#7540), signaling a significant architectural achievement.

## Community Hot Topics

The most active threads by comment count and community engagement:

- **Issue #6808 (open, 11 comments)** — RFC: Work Lanes, Board Automation, and Label Cleanup. This governance RFC proposes lightweight PR lanes and board-owned issue labeling to reduce maintainer overhead. The discussion reflects a maturing desire for structured workflows as the project scales.  
  [zeroclaw-labs/zeroclaw Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

- **Issue #3642 (closed, 13 comments, 3 👍)** — Feature request for a “full” Docker image with all feature flags enabled (e.g., WhatsApp). The high comment count and upvotes highlight a strong user demand for a lower-friction onboarding experience.  
  [zeroclaw-labs/zeroclaw Issue #3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)

- **Issue #7470 (open, 7 comments)** — Bug report on delegate agentic mode rejecting empty `allowed_tools` and profile gating. This S1 severity issue blocks practical multi-agent setups and has attracted detailed community debugging.  
  [zeroclaw-labs/zeroclaw Issue #7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **Issue #6293 (open, 5 comments)** — RFC for an air-gapped execution mode with a companion daemon over a Unix socket. This security-focused proposal is generating architectural discussion and is flagged `needs-maintainer-review`.  
  [zeroclaw-labs/zeroclaw Issue #6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)

- **Issue #1458 (closed, 7 comments)** — Feature request for local CA certificates for custom inference providers. Though closed, the discussion indicates enterprise/self-hosted use cases where TLS trust is a barrier.  
  [zeroclaw-labs/zeroclaw Issue #1458](https://github.com/zeroclaw-labs/zeroclaw/issues/1458)

## Bugs & Stability

Three critical or high-severity bugs were actively discussed in the last 24 hours:

- **Issue #7470 (S1 – workflow blocked)** — Delegate agentic mode rejects empty `allowed_tools` and same-profile gating blocks stricter targets. This is a regression in the delegate path that prevents multi-agent reviewer/research setups. No fix PR yet, but the issue is `in-progress`.  
  [zeroclaw-labs/zeroclaw Issue #7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **Issue #5528 (S0 – data loss / security risk, now closed)** — Improper logic in email channel config. The bug was patched earlier but the closure today indicates the fix is confirmed.  
  [zeroclaw-labs/zeroclaw Issue #5528](https://github.com/zeroclaw-labs/zeroclaw/issues/5528)

- **Issue #5662 (open, risk: medium)** — QQ channel voice messages processed multiple times, creating duplicate entries in `brain.db`. The `in-progress` status suggests a fix is being developed.  
  [zeroclaw-labs/zeroclaw Issue #5662](https://github.com/zeroclaw-labs/zeroclaw/issues/5662)

- **Issue #6856 (open, S2 – degraded behavior)** — `show_tool_calls` missing from channel schema v3. A regression that reduces channel usability.  
  [zeroclaw-labs/zeroclaw Issue #6856](https://github.com/zeroclaw-labs/zeroclaw/issues/6856)

Several fix PRs were opened today:

- **PR #7616** — Strips assistant reasoning on outbound replay for Groq (fixes provider incompatibility).  
- **PR #7608** — Exposes deferred MCP tools to delegates (fixes #6136).  
- **PR #7640** — Skips global credential fallback for OAuth target providers (prevents API key mismatch).  
- **PR #7583** — Honors profile tool iteration limits for cron/CLI runs.  
- **PR #7549** — Aligns plugin install/discovery paths and adds legacy migration.

## Feature Requests & Roadmap Signals

The project is absorbing a flood of new integration requests, most of which were closed as merged in the past month:

- **Provider additions (closed, all risk: medium)** — Arcee AI, Inception Labs (Mercury), Lambda AI Inference, Featherless AI, Upstage Solar. These indicate a deliberate strategy to support diverse model sources, including novel architectures (diffusion-based models from Inception Labs).  
- **SMS channel family (closed, all risk: high)** — Vonage, Sinch, Plivo, Telnyx joined the already-merged Twilio channel, giving operators four new two-way SMS gateways.  
- **Tool integrations (closed)** — Sonos, Shazam, Spotify, 8Sleep, Philips Hue, all moved from “Coming Soon” to active, signaling a push toward smart home and entertainment integrations.

**Active roadmap signals:**

- **Issue #6808 (RFC)** — Work lanes and board automation, suggesting the maintainers are planning to scale governance and issue/PR triage.  
- **Issue #7415 (implemented)** — Turn engine unification reduces code complexity, freeing maintainer capacity for other features.  
- **Issue #5842 (open)** — Tracking validation/allowlist for `extra_args` in Codex CLI config, addressing a security-sensitive area.  
- **Issue #6074 (open, help wanted)** — Audit of 153 commits lost in a bulk revert; a significant cleanup task that may block other work.  

Predicting near-future releases: the next minor version (likely 0.80-beta1 per RFC #6808) will probably include the new providers, SMS channels, turn engine consolidation, and the config alias-ref picker (#7594). The air-gapped mode (#6293) is still in RFC stage and may land in a later release.

## User Feedback Summary

**Pain points:**

- **Onboarding friction** – Issue #3642 (full Docker image) and Issue #6847 (WhatsApp QR failure) both highlight that non-technical users struggle with feature flags and channel setup. The request for a “full” image and the explicit “thanks for the hard work – best tool out there” sentiment in #6847 show high satisfaction with the concept but frustration with setup.
- **Configuration confusion** – Issues #6856 (missing `show_tool_calls`), #5528 (email config logic), and PR #7617 (extra-nested provider aliases) all reveal that TOML-based configuration is error-prone, especially for new users.
- **Reliability & duplication** – Issue #5662 (QQ voice duplicates) and Issue #6474 (LLM invoked twice per request) erode trust in channel processing. Both are being addressed.

**Satisfaction signals:**

- The rapid closure of many feature requests (e.g., multiple provider and SMS channel adds) indicates a responsive maintainer team that listens to community demands.
- The RFC process (#6808, #6293, #7415) is healthy, with constructive multi-comment discussions and clear acceptance paths.
- User comments in #6847 explicitly praise the project as “best tool out there.”

## Backlog Watch

Several important items are stalled or need maintainer attention:

- **Issue #6293 (open, blocked, needs-maintainer-review)** – Air-gapped execution mode RFC. Has 5 comments but no official maintainer response beyond labeling. Critical for security-conscious deployments.  
  [zeroclaw-labs/zeroclaw Issue #6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)

- **Issue #6074 (open, help wanted)** – Audit tracking 153 lost commits. This is a deep technical debt issue that may cause regression risk if not resolved. Labeled `in-progress` but no recent activity.  
  [zeroclaw-labs/zeroclaw Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)

- **PR #6693 (open, size: XL, needs-author-action)** – “Dream mode” for periodic memory consolidation. A large feature that hasn’t seen updates since May 16. With the new turn-engine consolidation merged, this may be a candidate for re-review.  
  [zeroclaw-labs/zeroclaw PR #6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693)

- **PR #5892 (open, size: L, needs-author-action, stale-candidate)** – Fix for two production blockers (empty tool_choice and orphaned tool_use). Despite being rebased onto the latest turn engine, it has not been merged and is now marked as a stale candidate.  
  [zeroclaw-labs/zeroclaw PR #5892](https://github.com/zeroclaw-labs/zeroclaw/pull/5892)

- **PR #7616, #7617, #7610, #7609, #7637, #7638** – All have `needs-author-action` label, indicating the authors need to respond to review feedback. These include critical fixes for Groq compatibility, config validation, quickstart flows, and i18n.  

Maintainers should prioritize reviewing the `needs-maintainer-review` items (#6293) and the stale PR #5892 to avoid accumulation of technical debt.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*