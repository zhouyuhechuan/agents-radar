# OpenClaw Ecosystem Digest 2026-07-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-22 01:56 UTC

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

# OpenClaw Project Digest — 2026-07-22

## Today's Overview

The project remains extremely active, with **500 issues** and **500 pull requests** updated in the last 24 hours. Of these, **395 issues are still open** (105 closed) and **336 PRs are open** (164 merged/closed). No new releases were published, indicating the team is focused on bug fixes, feature development, and stabilization. The high volume of open issues (395) and PRs (336) suggests both heavy community engagement and a growing backlog that may require priority triage. Several critical regression bugs and long-standing feature requests continue to dominate discussion, particularly around security, data integrity, and session management.

## Releases

**None** – No versions were tagged today.

## Project Progress

In the past 24 hours, **105 issues** and **164 PRs** were closed or merged. Among the notable changes visible in the top activity items:

- **PR #102228** (closed) – Installs ClawHub packages for new Claw agents, with exact digest revalidation and trust decisions.
- **PR #110739** (closed) – Caps the `sessions_list` tool limit before gateway dispatch, preventing pathological values from causing resource exhaustion.
- **PR #112471** (closed) – Fixes a gateway bug where plugin widget descriptors vanished from the control-UI hello payload after the first agent turn.
- **PR #112457** (closed) – Enforces Claude CLI cron tool policies, isolating restricted runs from user/project hooks, plugins, and local configs.
- **Issue #98437** (closed) – MCP loopback bundle warning spam consolidated at build time, reducing thousands of “conflicting schema definitions” logs per day.
- **Issue #91383** (closed) – Telegram reply broke when starting with Markdown links; fix likely addresses message splitting.
- **Issue #95441** (closed) – Resolved persistence of `thinkingSignature` encrypted content after previous fixes, restoring LLM request flows for GitHub Copilot model.

## Community Hot Topics

The most active discussions (by comment count) reveal strong community concern around security, data corruption, and tool integration:

- **Issue #10659** (15 comments, 4 👍) – Masked secrets to prevent agents from accessing raw API keys. High security relevance; tagged `P1`, `diamond lobster` priority.
- **Issue #101290** (13 comments, 1 👍) – Critical `P0` regression: CLI preflight corrupts SQLite state DB while gateway runs. “Database disk image is malformed” reported multiple times. Fix status still pending maintainer review.
- **Issue #86996** (11 comments, 2 👍) – Active Memory + Codex path causes long latency, hook timeouts, and gateway event-loop stalls. `P1` with `diamond lobster` severity.
- **Issue #85030** (11 comments, 5 👍) – MCP tools not injected into subagent sessions, ignoring allowlist configuration. `P1`, security implications.
- **Issue #106779** (11 comments, 2 👍) – `2026.7.1` release breaks local llama.cpp provider with “Unable to generate parser for this template.” Mixed reports: ChatGPT works, local fails.
- **Issue #7722** (10 comments, 4 👍) – Filesystem sandboxing config (`tools.fileAccess`) feature request remains open for over 5 months with no maintainer decision.
- **Issue #20786** (9 comments, 6 👍) – Telegram Business Bot support – highest 👍 count among top issues, indicating strong demand.

On the PR side, comment counts are not shown in the provided data, but the most active PRs include **#112339** (feat(ui): show chat run startup status), **#112433** (fix(ui): allow direct sessions in non-Git folders), and **#112357** (fix(ui): keep chat author identity readable), all with multiple active discussions.

## Bugs & Stability

Several high-severity bugs are under active community scrutiny:

| Issue | Severity | Bug Type | Status | Summary |
|-------|----------|----------|--------|---------|
| [#101290](https://github.com/openclaw/openclaw/issues/101290) | **P0** / Platinum Hermit | Regression | Open, needs maintainer review | CLI preflight corrupts SQLite DB while gateway runs (macOS 2026.6.6) – “database disk image is malformed” |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | **P1** / Platinum Hermit | Behavior bug | Open, needs live repro | Write/exec tool parameters silently dropped after long conversations (15+ turns) |
| [#108473](https://github.com/openclaw/openclaw/issues/108473) | Bug / Regression | Open | Need info | `cron` tool schema breaks llama.cpp tool-calling due to unanchored regex pattern |
| [#90840](https://github.com/openclaw/openclaw/issues/90840) | **P1** / Regression | Diamond Lobster | Open | Subagent raw output delivered to user instead of parent summary |
| [#95612](https://github.com/openclaw/openclaw/issues/95612) | **P1** / Platinum Hermit | Authentication | Open | cli-backend agent returns 401 against Anthropic while `claude` works in shell |
| [#88562](https://github.com/openclaw/openclaw/issues/88562) | **P1** / Diamond Lobster | Security behavior | Open | models.json generator writes `apiKey` as plain string instead of secret-ref object |
| [#111498](https://github.com/openclaw/openclaw/issues/111498) | **P1** / Regression | Blocking | Open | Main agent blocked by persistent workspace-state migration after Anthropic auth recovery |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | **P1** / Diamond Lobster | Security bug | Open | MCP tools not injected into subagent sessions, allowlist ignored |

**Related fix PRs exist** for several of these:  
- [#105806](https://github.com/openclaw/openclaw/pull/105806) (fix recovery for stuck sessions) addresses terminal-phase reply wedge.  
- [#108287](https://github.com/openclaw/openclaw/pull/108287) (fix sqlite: allow verified shared wal backports) may help with #101290 by enabling distro backports for WAL-reset corruption fix.  
- [#102296](https://github.com/openclaw/openclaw/pull/102296) (add plan-first Claw status and remove) touches session state management.

## Feature Requests & Roadmap Signals

The community continues to push for security, sandboxing, and enterprise-ready features. Top enhancement requests (by comment count and thumbs-up) indicate:

1. **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – Prevent agents from seeing raw API keys; 15 comments, 4 👍. Likely to be prioritized given P1 and security review labels.
2. **Telegram Business Bot support** ([#20786](https://github.com/openclaw/openclaw/issues/20786)) – 9 comments, 6 👍. High user demand; may land in next minor release.
3. **Filesystem Sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) – 10 comments, 4 👍. Long open (since Feb 3), still awaiting maintainer decision. Could be part of a security-themed release.
4. **Tool schema token overhead reduction** ([#14785](https://github.com/openclaw/openclaw/issues/14785)) – 9 comments. ~3,500 tokens saved per session; significant UX improvement.
5. **Backup/restore utility** ([#13616](https://github.com/openclaw/openclaw/issues/13616)) – 9 comments. Disaster recovery and migration needs.
6. **Onboarding wizard with Memory setup** ([#16670](https://github.com/openclaw/openclaw/issues/16670)) – 9 comments, 1 👍. Critical UX gap for new users.
7. **Auto-update with schedule and confirmation** ([#12855](https://github.com/openclaw/openclaw/issues/12855)) – 8 comments. Production deployment necessity.
8. **Capability-based permissions for skills/tools** ([#12678](https://github.com/openclaw/openclaw/issues/12678)) – 6 comments. Default-deny high-risk actions.

Many of these have been open for months (since February) and are tagged with `clawsweeper:needs-product-decision` or `needs-maintainer-review`, suggesting the maintainers are still evaluating scope. The next release may bundle several of these into a security-focused milestone.

## User Feedback Summary

Real user pain points observed from issue and PR descriptions:

- **Data integrity anxiety**: The SQLite corruption bug (#101290) has affected multiple users on macOS, causing repeated data loss even without crashes. Users express frustration that vanilla SQLite control tests do not reproduce the issue.
- **Security leaks**: Users are concerned about plaintext API keys in generated configs (#88562), raw credential exposure to agents (#10659), and insufficient sandboxing (#7722, #12678).
- **Tool integration friction**: MCP tools not inherited by subagents (#85030) breaks workflows; silent parameter dropping (#53408) causes unpredictable failures; cron schema breaking llama.cpp (#108473) impacts local model users.
- **Session management**: Lack of manual session snapshots (#13700), group session consolidation (#7524), and announcement suppression (#8299, #13911) are repeatedly requested.
- **Onboarding gaps**: New users hit confusion without embedding provider setup in onboarding (#16670) and lack of clear error messages (#9409).
- **Production readiness**: Need for safer self-update (#14526), configurable delivery queue TTL (#16555), and per-model cost tracking (#13219) are voiced by operators.

## Backlog Watch

Several important issues and PRs have been open for extended periods without maintainer resolution, risking stagnation:

- **Issue #7722** (Filesystem Sandboxing Config) – Open since Feb 3, 10 comments, 4 👍, still `needs-product-decision`. High security impact.
- **Issue #14785** (Reduce tool schema token overhead) – Open since Feb 12, 9 comments, `needs-product-decision`. Significant UX win.
- **Issue #13616** (Backup/restore utility) – Open since Feb 10, 9 comments, `needs-product-decision` and `needs-security-review`. Critical for disaster recovery.
- **Issue #20786** (Telegram Business Bot) – Open since Feb 19, 9 comments, 6 👍, `needs-product-decision` and `linked-pr-open`. Developer interest is high.
- **Issue #13219** (Per-model usage logging) – Open since Feb 10, 6 comments, `needs-product-decision`. Cost tracking is a core enterprise need.
- **PR #83933** (fix cron deleteAfterRun and counters) – Open since May 19, 6+ weeks, `needs proof`. Addresses a one-shot cron job consumption bug.
- **PR #102296** (Add plan-first Claw status and remove) – Open since July 8, still `needs proof`. Large change with potential compatibility risk, but needed for session state management.
- **Issue #9409** (Improve context overflow error message) – Open since Feb 5, 5 comments, 3 👍, `needs-product-decision`. Simple UX fix that could benefit many users.

The maintainer team is encouraged to review these items for inclusion in the next minor release cycle, especially those with overlapping security or stability impact.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI agent open-source landscape remains in a phase of intense, concurrent evolution, characterized by rapid feature iteration, growing security awareness, and significant architectural divergence. The ecosystem spans from massive, community-driven monoliths like OpenClaw (500+ daily issues/PRs) to highly specialized, lower-traffic projects such as Moltis and PicoClaw. A clear tension has emerged between the need for production-grade reliability—reflected in recurring SQLite corruption, memory leaks, and OAuth failures—and the drive to add ambitious new capabilities like model routing, multi-agent governance, and real-time speech. Notably, the projects collectively signal a community-wide pivot from demo-level usability toward enterprise-grade requirements: sandboxing, secrets management, backup/recovery, and per-model cost tracking. Meanwhile, new paradigm-shifting architectural patterns, such as IronClaw's complete monolith rewrite ("Reborn") and ZeroClaw's multi‑agent orchestration, indicate that no single design has yet achieved dominance, leaving room for further fragmentation or eventual convergence.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Score (subjective 1–10) | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500 (395 open) | 500 (336 open) | None | **8** | Extremely high volume; heavy backlog backlog; community-driven |
| **NanoBot** | 10 (1 open) | 33 (11 open) | None | **9** | High closure rate; responsive maintainer |
| **Hermes Agent** | 50 (46 open) | 50 (46 open) | None | **7** | Active but P1 bugs linger; desktop/TUI focus |
| **PicoClaw** | 8 (4 open) | 8 (5 open) | None | **6** | Moderate; stale security-critical issue |
| **NanoClaw** | 1 | 12 (9 open) | None | **7** | Steady feature PRs; small but engaged |
| **NullClaw** | 0 | 0 | None | **2** | Inactive |
| **IronClaw** | 41 (27 open) | 50 (33 open) | **v1.0.0-rc.1** | **9** | Intense rearchitecture; disciplined staging |
| **LobsterAI** | 1 | 10 (5 open) | None | **7** | Moderate; steady bugfix + feature PRs |
| **TinyClaw** | 0 | 0 | None | **1** | Inactive |
| **Moltis** | 1 | 1 | None | **3** | Very low activity; single enhancement |
| **CoPaw** | 42 (21 open) | 50 (20 open) | **v2.0.1-beta.1** | **8** | High velocity; v2.0 stability regressions |
| **ZeptoClaw** | 0 | 0 | None | **1** | Inactive |
| **ZeroClaw** | 50 (47 open) | 50 (41 open) | None | **7** | Very high velocity but PR merge lag; S0 bugs |

**Key observations:**
- **OpenClaw, Hermes Agent, CoPaw, ZeroClaw** dominate raw volume.
- **NanoBot** punches above its weight on closure efficiency.
- **IronClaw** leads in architectural ambition with a release candidate.
- **NullClaw, TinyClaw, ZeptoClaw** are essentially dead (0 activity).
- **Moltis** is maintenance-only with no feature churn.

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale:** OpenClaw is the largest project in the ecosystem by a significant margin (500 daily issues + 500 PRs). Its community engagement dwarfs all others, providing a vast pool of contributors, bug reports, and feature requests.
- **Maturity as a reference implementation:** It is explicitly positioned as the "core reference" project. Many other projects (NanoClaw, PicoClaw) derive from or are inspired by it.
- **Comprehensive feature surface:** Covers agent runtime, gateway, MCP tool integration, session management, and multi-channel support (Telegram, etc.) in a single repository.

**Technical approach differences:**
- OpenClaw follows a **monolithic, PR-heavy, community-governed model** with high tolerance for open issues. This contrasts with IronClaw's disciplined "Reborn" rewrite and NanoBot's maintainer-driven triage.
- OpenClaw appears more **config-driven** (e.g., `tools.fileAccess`, `models.json`), whereas IronClaw is moving to a **witness authority / store-graph** architecture and ZeroClaw is exploring **policy-based governance** with sub-agent allowlists.
- OpenClaw's session management and state persistence (SQLite) are mature but currently under strain—witness the P0 SQLite corruption bug (#101290) not yet seen in other projects' reports.

**Community size comparison:**
- OpenClaw's community is the largest by both activity and raw numbers. However, its **open issue backlog (395)** and **open PR count (336)** suggest that maintainer bandwidth may be insufficient to keep pace. In contrast, NanoBot's maintainer responds quickly; IronClaw's core team is executing a tightly coordinated plan.
- The `needs-product-decision` label on many long-standing OpenClaw features indicates a bottleneck in product direction, while smaller projects like NanoBot ship decisions faster.

**Bottom line:** OpenClaw is the ecosystem's central hub but risks gridlock if triage velocity does not improve. Its future depends on scaling maintainer capacity or adopting more aggressive issue/PR hygiene.

---

## 4. Shared Technical Focus Areas

The following requirements emerge across **multiple projects**, indicating broad industry consensus on what the ecosystem needs next:

| Requirement | Projects Affected | Description |
|---|---|---|
| **Secret / API key protection** | OpenClaw (#10659), NanoBot (#5010, #4803), ZeroClaw (#88562) | Masking raw keys from agents, atomic config writes, secret-ref objects. **Cross-cutting security push.** |
| **Filesystem sandboxing / workspace confinement** | OpenClaw (#7722), NanoBot (#5013, #4987), ZeroClaw (#9247, #85030) | Symlink escapes, shell command confirmation, O_NOFOLLOW, workspace boundary enforcement. |
| **Tool execution permission granularity** | Hermes Agent (#68964, #25083), OpenClaw (#12678), ZeroClaw (#8279) | Per-function tool filtering, immutable skills, allowlist bypass fixes. |
| **Sub-agent / delegation model hardening** | OpenClaw (#85030, #90840), Hermes Agent (#68915), ZeroClaw (#8279) | MCP tools not inherited by subagent sessions, worker deadlocks, sub-agent allowlist bypass. |
| **Model routing / per-session overrides** | Moltis (#574), ZeroClaw (#8600), NanoBot (#4866), CoPaw (#5992) | Per-chat model switching, topic-based routing, model preset binding. |
| **Prompt caching for local models** | NanoBot (#4867), OpenClaw (#108473) | Ollama latency improvement, llama.cpp schema compatibility. |
| **Data integrity / backup / recovery** | OpenClaw (#101290, #13616), Hermes Agent (#68474), ZeroClaw (#9240) | SQLite corruption, state.db zeroing, silent write drops. |
| **Channel adapter maturity** | OpenClaw (#20786), ZeroClaw (#8505), PicoClaw (#3203, #3255) | Telegram, Matrix reconnection, DingTalk preview, Discord slash sync. |
| **Observability / cost tracking** | OpenClaw (#13219), ZeroClaw (#9228), NanoClaw (#3114) | Per-model usage logging, eval dashboards, Langfuse tracing. |
| **Onboarding UX** | OpenClaw (#16670), ZeroClaw (#8718), LobsterAI (#1861) | Setup wizards, image/model switching, config defaults that don't break features. |

**Implication:** No single project has solved these well—they are **ecosystem-wide pain points** that downstream consumers (enterprises, tool builders) should monitor across all projects.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | IronClaw | ZeroClaw | CoPaw | LobsterAI |
|---|---|---|---|---|---|---|---|
| **Primary target user** | Developers / self-hosters | Developers (API-first) | Desktop + TUI power users | Enterprise operators | Advanced orchestrators | End-users (workflow) | Vision/cowork users |
| **Architecture** | Monolithic, config-driven | Modular, maintainer-curated | Multi-surface (Desktop/TUI/Terminal) | Rebuilt monolith ("Reborn") | Multi-agent orchestration | Channel-first, AM compliant | Monolithic, cowork-first |
| **Key differentiator** | Largest community & plugin ecosystem | Fastest triage; prompt caching focus | Rich desktop & TUI experience | Ground-up rearchitecture with governance | Policy & security-first (S0 bugs) | Workflow modes & creator app | Browser annotation & artifact sharing |
| **Platform support** | CLI, gateway, Telegram, Subagents | CLI, Web UI, skills | Desktop (macOS/Windows), TUI, Discord, Telegram | CLI, Web UI, Slack, WeCom, Telegram | CLI, Telegram (buggy), Mattermost | Feishu, Web, mobile web | Desktop, Web, Cowork |
| **Maturity phase** | Stable but **backlog-constrained** | Stable, high throughput | Unstable (P1 bugs); fast feature churn | Pre-v1 release candidate; high discipline | Unstable (S0 bugs); high feature churn | v2.0 releasing; stability regressions | Moderate, steady |
| **Community model** | Open PR flood | Maintainer-gated | Contributor + core team | Core-team-driven | RFC-heavy | Contributor + help-wanted | Small, focused |

**Key takeaway:** The ecosystem is **fragmenting by use case**: IronClaw targets enterprise operators with disciplined staging; ZeroClaw pursues multi-agent orchestration at the cost of stability; Hermes Agent optimizes for desktop UX while accumulating bugs; NanoBot prioritizes API cleanliness and developer ergonomics. **No project has yet achieved both stability and feature breadth.**

---

## 6. Community Momentum & Maturity

### Tier 1: High-velocity, rapid iteration
- **OpenClaw, Hermes Agent, CoPaw, ZeroClaw** — massive daily issue/PR volumes. All are adding features faster than closing bugs. CoPaw and OpenClaw have released stable versions recently; Hermes and ZeroClaw are more volatile.
- **IronClaw** — intense, but disciplined toward a v1 goal. Momentum is high but concentrated in a core team.

### Tier 2: Moderate, steady
- **NanoBot, NanoClaw, LobsterAI** — smaller but responsive. NanoBot stands out for high closure efficiency and quick triage. These projects may be more attractive for low-risk adoption.

### Tier 3: Low / maintenance-only
- **PicoClaw, Moltis** — very low activity. PicoClaw has a critical security issue (libolm → vodozemac) stale for weeks; Moltis has one open feature. Likely not under active development.

### Tier 4: Inactive / dead
- **NullClaw, TinyClaw, ZeptoClaw** — zero activity. Should be considered unsupported.

**Maturity assessment:**
- **Stabilizing:** NanoBot (few open bugs, fast closures), LobsterAI (steady bugfix PRs).
- **Rapidly iterating but unstable:** Hermes Agent, ZeroClaw, CoPaw (new v2.0 regressions).
- **Pre-production:** IronClaw (RC1), PicoClaw (stale key dependency).
- **Legacy / dormant:** NullClaw, TinyClaw, ZeptoClaw, Moltis.

---

## 7. Trend Signals

From cross-cutting community feedback and issue patterns, the following industry trends are evident for AI agent developers:

1. **Security is no longer optional** — Raw API key storage, missing sandboxing, and sub-agent allowlist bypasses are now treated as **S0/P0** priority bugs. Expect projects to ship **secrets masking, atomic config writes, and workspace confinement** as default features within 2-3 releases.

2. **Local model support is a top-tier pain point** — OpenAI-compatible adapters (ZeroClaw #8603, CoPaw #5992) and prompt caching for Ollama (NanoBot #4867) are high-demand. The ecosystem is converging on **OpenAI-compatible API as the universal integration target**, while addressing local inference latency.

3. **Multi-agent orchestration is the next frontier** — Goal mode (ZeroClaw #8303), Mixture-of-Agents (ZeroClaw #8568), sub-agent governance (OpenClaw #85030, Hermes #68915), and agent delegation workflows are all actively debated. This suggests **agent-to-agent coordination** will be a key differentiator in 2027.

4. **Production readiness demands observability** — Cost tracking per model (OpenClaw #13219), eval dashboards (ZeroClaw #9228), Langfuse integration (NanoClaw #3114), and structured logging (CoPaw #6183) are all being built in parallel. **Instrumentation is becoming table stakes for enterprise adoption.**

5. **Channel integration remains fragile** — Telegram, Discord, Matrix, DingTalk, Feishu, and Mattermost all have reported connectivity bugs or missing features across projects. **Multi-channel deployment is still a first-class headache**, and cross-project learning (e.g., Telegram fixes in OpenClaw benefiting PicoClaw) is minimal, suggesting a need for a shared channel adapter library.

6. **Data portability and disaster recovery are neglected** — Only OpenClaw (#13616) and Hermes (#68474) have explicit backup/restore issues. The rest assume users accept fragility. As these tools move from labs to production, **state backup and migration utilities will become critical**.

7. **UI is diverging** — Hermes Agent invests heavily in desktop TUI and desktop app; CoPaw builds a mobile web console; IronClaw focuses on Web UI with design tokens; OpenClaw remains CLI-centric. The **lack of a unified, polished frontend** means developers must choose between feature depth and UX polish.

**For AI agent developers:** The ecosystem is vibrant but fragmented. If you prioritize stability, start with **NanoBot** or **LobsterAI**. If you need the richest feature set and can tolerate triage delays, **OpenClaw** or **CoPaw** are your best bets. For multi-agent orchestration and policy-based security, watch **ZeroClaw** closely—but prepare for instability. **IronClaw** is the most promising for enterprise deployments if the Reborn release achieves its goals.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-22

## 1. Today’s Overview

NanoBot saw a high-velocity day with **10 issues updated** (9 closed, 1 open) and **33 pull requests updated** (22 merged/closed, 11 open). No new releases were published. The project maintained a strong closure rate, indicating active triage and continuous integration. The open issue focuses on a Qwen model rendering bug, while the backlog of merged PRs addresses security hardening, provider support, and stability fixes. Overall project health appears robust, with the maintainer and contributor team demonstrating responsiveness to both bugs and feature requests.

## 2. Releases

No releases were published in the last 24 hours.

## 3. Project Progress

22 pull requests were merged or closed today. Notable advances include:

- **Security & Configuration**: [#4984](https://github.com/HKUDS/nanobot/pull/4984) makes `config.json` writes atomic via temp+replace, preventing truncated files on crash. [#5010](https://github.com/HKUDS/nanobot/pull/5010) updates `SECURITY.md` to recommend environment‑variable references for API keys.

- **Provider Support**: [#4965](https://github.com/HKUDS/nanobot/pull/4965) adds ModelScope as a built‑in provider (OpenAI‑compatible endpoint). [#5019](https://github.com/HKUDS/nanobot/pull/5019) supports Codex Fast Mode via `service_tier: "priority"`.

- **Bug Fixes**: [#4663](https://github.com/HKUDS/nanobot/pull/4663) sanitizes invalid tool results (fixes #4058). [#4952](https://github.com/HKUDS/nanobot/pull/4952) prevents `UnicodeEncodeError` from UTF‑16 surrogates. [#4811](https://github.com/HKUDS/nanobot/pull/4811) logs suppressed `prepare_call` exceptions instead of silently swallowing them. [#4989](https://github.com/HKUDS/nanobot/pull/4989) resolves `${VAR}` env references in transcription API keys. [#4983](https://github.com/HKUDS/nanobot/pull/4983) coercing string fields in `jobs.json` to int prevents `TypeError`.

- **Web UI / UX**: [#5020](https://github.com/HKUDS/nanobot/pull/5020) highlights `$skillname` references in sent user messages.

## 4. Community Hot Topics

- **Most commented issue**: [#4867](https://github.com/HKUDS/nanobot/issues/4867) — *“Preserve exact prompt prefix to enable caching in Ollama and others”* (22 comments). Users report that Ollama adds ~60 seconds per turn, making local models unusable. The underlying need is for prompt‑prefix caching to improve latency in local inference.

- **Open issue with engagement**: [#4934](https://github.com/HKUDS/nanobot/issues/4934) — *“Qwen models expose thinking/reasoning content in chat responses”* (2 comments, still open). Users experience leaked system‑level reasoning in the visible response.

- **Feature request with thumbs‑up**: [#4911](https://github.com/HKUDS/nanobot/issues/4911) — *“A guarded tool gateway seam so channels can run the agent’s tools”* (1 👍). This reflects demand for voice/real‑time channels to invoke agent tools.

- **New user‑safety request**: [#5013](https://github.com/HKUDS/nanobot/issues/5013) — *“Shell execution requires user confirmation”* (1 comment). Users want a human‑in‑the‑loop safeguard for shell commands, similar to LangChain’s middleware.

## 5. Bugs & Stability

| Severity | Issue | Description | Status | Fix PR |
|----------|-------|-------------|--------|--------|
| High | [#4934](https://github.com/HKUDS/nanobot/issues/4934) | Qwen models leak thinking/reasoning content in responses | **Open** | [#5023](https://github.com/HKUDS/nanobot/pull/5023) (open) adds model‑level thinking style mapping |
| Medium | [#4785](https://github.com/HKUDS/nanobot/issues/4785) | `read_file` loads entire file before truncation → OOM on large files | Closed | PR [#4987](https://github.com/HKUDS/nanobot/pull/4987) (open) binds workspace checks to opened file handles |
| Medium | [#4787](https://github.com/HKUDS/nanobot/issues/4787) | `Session.messages` unbounded; long‑running sessions accumulate messages | Closed | No dedicated PR yet – likely part of broader session cleanup |
| Medium | [#4794](https://github.com/HKUDS/nanobot/issues/4794) | Exec sessions lack shutdown cleanup; child processes become orphans | Closed | PR [#5021](https://github.com/HKUDS/nanobot/pull/5021) (open) cascades exec termination on `/stop` |
| Medium | [#4803](https://github.com/HKUDS/nanobot/issues/4803) | API keys stored as plaintext in `~/.nanobot/config.json` | Closed | PR [#4984](https://github.com/HKUDS/nanobot/pull/4984) (atomic writes) and [#5010](https://github.com/HKUDS/nanobot/pull/5010) (documentation) address this |
| Low | [#4788](https://github.com/HKUDS/nanobot/issues/4788) | `except BaseException` in tool runner catches `KeyboardInterrupt`/`SystemExit` | Closed | Merged in [#4811](https://github.com/HKUDS/nanobot/pull/4811) (replaced with specific exception logging) |

## 6. Feature Requests & Roadmap Signals

- **Prompt caching (Ollama)**: [#4867](https://github.com/HKUDS/nanobot/issues/4867) — critical for local LLM usability. Likely to appear in a near‑term release.
- **Tool gateway for channels**: [#4911](https://github.com/HKUDS/nanobot/issues/4911) — important for voice/real‑time integrations.
- **Model‑preset binding to sessions**: PR [#4866](https://github.com/HKUDS/nanobot/pull/4866) (open) persists per‑session model overrides. This is a high‑priority feature that could ship next.
- **Cancel‑goal command**: PR [#5022](https://github.com/HKUDS/nanobot/pull/5022) (open) adds `/cancel-goal` to break sustained‑goal loops – directly addresses user frustration with agent stuck in verification loops.
- **Skills context loading**: PR [#5018](https://github.com/HKUDS/nanobot/pull/5018) (open) allows explicit skills loading, improving flexibility for developers.
- **Web UI polish**: PR [#4963](https://github.com/HKUDS/nanobot/pull/4963) (open) unifies tool logs and improves Streamdown rendering; PR [#4399](https://github.com/HKUDS/nanobot/pull/4399) (open) adds hidden config sections for simplified UI.

## 7. User Feedback Summary

- **Pain point: Slow local inference** – Users with Ollama and 32 GB VRAM report 60‑second startup per turn ([#4867](https://github.com/HKUDS/nanobot/issues/4867)). The community is eager for prompt‑prefix caching.
- **Security concerns** – Plaintext API key storage ([#4803](https://github.com/HKUDS/nanobot/issues/4803)) and lack of user confirmation for shell commands ([#5013](https://github.com/HKUDS/nanobot/issues/5013)) are recurring themes.
- **Stability issues** – Large‑file OOM ([#4785](https://github.com/HKUDS/nanobot/issues/4785)), resource leaks ([#4787](https://github.com/HKUDS/nanobot/issues/4787)), orphan processes ([#4794](https://github.com/HKUDS/nanobot/issues/4794)), and improper exception handling ([#4788](https://github.com/HKUDS/nanobot/issues/4788)) indicate users are pushing the project beyond demos into production use.
- **Satisfaction** – High comment activity on fixes and quick merges suggests the community appreciates the rapid turnaround of bug reports.

## 8. Backlog Watch

The following issues and PRs have remained open for an extended period or lack maintainer interaction despite clear impact:

| Item | Age (days) | Summary | Impact | Maintainer action needed |
|------|------------|---------|--------|--------------------------|
| [#4399](https://github.com/HKUDS/nanobot/pull/4399) | 34 | Add `hidden_settings_sections` for simplified Web UI | Reduces noise for non‑technical users | Needs review and conflict resolution |
| [#4594](https://github.com/HKUDS/nanobot/pull/4594) | 23 | Fix shell guard regex to block `=`‑delimited paths (e.g., `curl --output=/etc/passwd`) | Security – workspace escape | Needs review; security‑critical |
| [#4866](https://github.com/HKUDS/nanobot/pull/4866) | 12 | Bind model presets to sessions | High value feature for multi‑model setups | Needs testing and merge decision |
| [#4941](https://github.com/HKUDS/nanobot/pull/4941) | 7 | Fallback to legacy session paths in metadata reads | Fixes WebUI workspace scope after restart | Needs review and merge |
| [#4987](https://github.com/HKUDS/nanobot/pull/4987) | 3 | Bind workspace checks to opened file handles (O_NOFOLLOW, fstat) | Prevents symlink‑based escapes and OOM | Under review; high severity |
| [#5023](https://github.com/HKUDS/nanobot/pull/5023) | 1 | Add Qwen thinking style mapping | Direct fix for open issue #4934 | Fresh; needs prompt review |

The oldest open item is PR [#4399](https://github.com/HKUDS/nanobot/pull/4399) (34 days), which would improve the Web UI for multi‑instance deployments. PR [#4594](https://github.com/HKUDS/nanobot/pull/4594) (23 days) is a security fix for the shell workspace guard. Both deserve maintainer attention soon.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-22

## 1. Today's Overview
Activity remains high with 50 issues and 50 pull requests updated in the last 24 hours, indicating a vibrant community and ongoing development. Four issues were closed and four PRs were merged/closed during this period, but no new releases were published. The project shows a healthy mix of bug fixing, feature development, and community engagement, though several high-severity bugs (P1 and P2) continue to demand attention. Desktop and terminal experience improvements dominate recent PRs, while the issue tracker reflects growing demands for configurability, stability, and platform support.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Four pull requests were closed or merged today. Notable among the top-20-by-comment PRs:
- **#68999** (CLOSED) – **fix(ui-tui): widget-grid hardening — review fast-follow for #20379** – Addressed MCP revision acknowledgment, grid‑layout race conditions, and multiple high‑severity findings from a deep review. (https://github.com/NousResearch/hermes-agent/pull/68999)
- **#69037** (OPEN) – **fix(kanban): re‑probe DB health on initialized paths** – Improves database health‑check caching with a 30‑second TTL and safer initialization locking. (https://github.com/NousResearch/hermes-agent/pull/69037)
- **#69036** (OPEN) – **fix(kanban): harden auto‑triage and worker process cleanup** – Ensures reclaimed workers do not leave orphaned process groups; filters block‑loop triage rows from auto‑decomposition. (https://github.com/NousResearch/hermes-agent/pull/69036)
- **#69035** (OPEN) – **fix(tui): make Kanban delivery and prompt ownership durable** – Adds lineage‑aware session ownership and transactional cursor rollback for Kanban events. (https://github.com/NousResearch/hermes-agent/pull/69035)
- **#69034** (OPEN) – **fix(codex): preserve Kanban app‑server runtime continuity** – Inherits card budgets and live model selection in Codex turns. (https://github.com/NousResearch/hermes-agent/pull/69034)
- **#69032** (OPEN) – **fix(tui): preserve Thai combining marks in streamed cell‑diff rendering (#68990)** – Closes the long‑standing rendering corruption for Thai text. (https://github.com/NousResearch/hermes-agent/pull/69032)
- **#69011** (OPEN) – **fix(agent): delimit continuation prompts as system instructions (#69000)** – Prevents models from misinterpreting truncation notices as user input. (https://github.com/NousResearch/hermes-agent/pull/69011)
- **#69030** (OPEN) – **fix(desktop): stop renderer OOM from session.info heartbeat churn** – Prevents memory exhaustion caused by unnecessary nanostore updates. (https://github.com/NousResearch/hermes-agent/pull/69030)

These PRs advance desktop, TUI, Kanban, agent, and security areas. Additionally, the closed PR #68999 represents a fast‑follow hardening of a previously merged change.

## 4. Community Hot Topics
The most discussed issues (by comment count) reveal core user needs:

- **#47349** (13 comments) – *Feature: Configurable Memory Backends* – Users want to rename `memory.md` to `rules.md` and allow using `honcho`/`fact_store` only. High engagement shows strong demand for flexible memory architecture. (https://github.com/NousResearch/hermes-agent/issues/47349)
- **#27683** (8 comments, CLOSED) – *web_tools.py: missing plugin discovery causes web tools to silently fail* – A sweeping bug on fresh installs, now fixed on main. (https://github.com/NousResearch/hermes-agent/issues/27683)
- **#25083** (7 comments) – *Feature: Immutable/protected skills* – Users want to prevent agents from modifying critical skills without approval. (https://github.com/NousResearch/hermes-agent/issues/25083)
- **#68915** (5 comments) – *Worker deadlocks when agent backgrounds a server via shell `&`* – A P1 bug causing permanent worker hang; top priority for maintainers. (https://github.com/NousResearch/hermes-agent/issues/68915)
- **#64900** (5 comments) – *Allow plugins to extend send_message with platform-specific schema* – Demand for tighter platform plugin integration. (https://github.com/NousResearch/hermes-agent/issues/64900)

Underlying themes: users want more granular control over agent behavior (memory, skills, tool permissions) and robust reliability in the plugin/terminal systems.

## 5. Bugs & Stability
Several high‑severity bugs were reported or saw activity today:

**P1 bugs:**
- **#68915** – Worker deadlocks when agent backgrounds a server via `&`. Orphaned subshell holds stdout pipe open. No fix PR yet. (https://github.com/NousResearch/hermes-agent/issues/68915)
- **#68474** – `state.db` zeroed (95 MB null bytes) during desktop update to v0.19.0 on Windows. No fix PR yet. (https://github.com/NousResearch/hermes-agent/issues/68474)

**P2 bugs:**
- **#68920** – Desktop/TUI sessions leak active‑session leases, blocking new sessions over time. (https://github.com/NousResearch/hermes-agent/issues/68920)
- **#68979** – Long‑thread reconciliation re‑stacks recent messages at thread bottom after compression. (https://github.com/NousResearch/hermes-agent/issues/68979)
- **#68858** – v0.19 compaction + FTS maintenance saturates disk I/O and wedges gateway shutdown. (https://github.com/NousResearch/hermes-agent/issues/68858)
- **#69033** – Local terminal tool orphans bash children on Windows (missing process‑group detachment). (https://github.com/NousResearch/hermes-agent/issues/69033)
- **#69008** – OpenRouter deepseek‑v4‑flash tool continuation fails: `content[].thinking` must be passed back. (https://github.com/NousResearch/hermes-agent/issues/69008)
- **#68990** – Thai combining marks dropped/doubled in TUI during streaming (stored content correct). Fix PR #69032 exists. (https://github.com/NousResearch/hermes-agent/issues/68990)
- **#68944** – `hermes mcp add` silently absorbs `--env` into `--args`. (https://github.com/NousResearch/hermes-agent/issues/68944)
- **#68911** – Gateway force‑redacts E.164 phone numbers with no trusted‑profile opt‑in. (https://github.com/NousResearch/hermes-agent/issues/68911)

**P3 bugs:**
- **#65868** – Desktop crashes in Rust→V8 IPC bridge (renderer SIGTRAP + main‑process abort). (https://github.com/NousResearch/hermes-agent/issues/65868)
- **#68963** – Discord slash‑command sync does not retry; exits until reconnect. (https://github.com/NousResearch/hermes-agent/issues/68963)
- **#68989** – Telegram adapter hangs indefinitely at "Connecting" only inside full gateway process. (https://github.com/NousResearch/hermes-agent/issues/68989)
- **#68937** – Desktop (macOS) PDF/file links fail to open; falls back to reveal‑in‑Finder. (https://github.com/NousResearch/hermes-agent/issues/68937)

Several of these bugs have corresponding fix PRs in review (e.g., #69032 for Thai marks, #69030 for OOM, #68999 for TUI grid). The worker deadlock (#68915) and state.db corruption (#68474) are the most critical without immediate fixes.

## 6. Feature Requests & Roadmap Signals
Notable feature proposals from today's issue activity:

- **#47349** – Configurable memory backends (rename memory.md → rules.md, optional files). Likely to gain traction given high comments. (https://github.com/NousResearch/hermes-agent/issues/47349)
- **#25083** – Immutable/protected skills. Strong user interest for safety. (https://github.com/NousResearch/hermes-agent/issues/25083)
- **#64900** – Plugin‑extensible `send_message` schema/handlers. Aligns with platform plugin roadmap. (https://github.com/NousResearch/hermes-agent/issues/64900)
- **#68964** – Per‑function tool filtering (finer than toolset‑level). (https://github.com/NousResearch/hermes-agent/issues/68964)
- **#68970** – Searchable timezone dropdown in Desktop Settings (PR #68969 already open). (https://github.com/NousResearch/hermes-agent/issues/68970)
- **#69025** – Settings search bar for Desktop (PR #69023 already open). (https://github.com/NousResearch/hermes-agent/issues/69025)
- **#68951** – Support Atomic Hermes (mobile) as a `send_message` target. (https://github.com/NousResearch/hermes-agent/issues/68951)
- **#68701** – Inject trusted network context into smart‑approval guard LLM prompt. (https://github.com/NousResearch/hermes-agent/issues/68701)
- **#61042** – TUI `/compress` should allow type‑ahead and queue next message. (https://github.com/NousResearch/hermes-agent/issues/61042)

Based on PR activity, Desktop UI improvements (searchable settings, timezone dropdown) and cross‑surface theming (#68857) are likely candidates for the next release. The memory backend and skill protection features may follow in later versions.

## 7. User Feedback Summary
Users report significant pain points in several areas:

- **Reliability:** Worker deadlocks and session‑lease leaks make long‑lived sessions fragile. The state.db zeroing during updates is a severe trust issue for desktop users on Windows.
- **Internationalization:** Thai text rendering corruption (stored correct, display wrong) frustrates Thai‑speaking users, though a fix PR is now open.
- **Plugin ecosystem:** Discord and Telegram adapters have connectivity issues that only manifest in production (not isolation), hampering multi‑platform deployments.
- **Granular control:** Repeated requests for finer‑grained tool permissions (per‑function, not per‑toolset) and immutable skills indicate users want safer autonomous operation.
- **Desktop experience:** Settings surfacing (80+ fields) is hard to navigate; users welcome the proposed search bar and searchable dropdowns. PDF/file link opening failure on macOS is a daily friction.
- **Provider compatibility:** OpenRouter with DeepSeek models fails on tool continuations; users want seamless reasoning model support.

Overall satisfaction remains high given the feature velocity, but stability regressions (especially the state.db corruption and deadlock) are eroding trust for production use.

## 8. Backlog Watch
Long‑standing issues that still lack maintainer attention or decisions:

- **#47349** (created 2026‑06‑16) – Configurable memory backends. High comments, needs maintainer decision on acceptance. (https://github.com/NousResearch/hermes-agent/issues/47349)
- **#25083** (created 2026‑05‑13) – Immutable/protected skills. Waiting on `needs-decision` label for over two months. (https://github.com/NousResearch/hermes-agent/issues/25083)
- **#23207** (created 2026‑05‑10) – How to use web search/fetch with Ollama cloud models. Unanswered question with three comments; perhaps needs better documentation. (https://github.com/NousResearch/hermes-agent/issues/23207)
- **#61042** (created 2026‑07‑08) – TUI `/compress` type‑ahead. Accepted as enhancement but unassigned. (https://github.com/NousResearch/hermes-agent/issues/61042)
- **#64900** (created 2026‑07‑15) – Plugin‑extensible `send_message`. Labeled `needs-decision`; no resolution yet. (https://github.com/NousResearch/hermes-agent/issues/64900)
- **#68964** (created 2026‑07‑21) – Per‑function tool filtering. Already identified as a duplicate, but the underlying need is still unaddressed. (https://github.com/NousResearch/hermes-agent/issues/68964)

These items represent community‑desired features that have not moved forward, suggesting maintainers may need to triage priorities or provide design feedback.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-22

## 1. Today's Overview
PicoClaw shows moderate activity with **8 issues** (4 open, 4 closed) and **8 pull requests** (5 open, 3 merged/closed) updated in the last 24 hours. No new release was published. The project continues to process both bug fixes and feature enhancements, with several critical OAuth and provider compatibility patches merged. A notable high-priority feature request to replace the unmaintained `libolm` library remains open and stale, while new bugs affecting Matrix reconnection and Web UI performance signal ongoing stability concerns.

## 2. Releases
**None.** No new versions were tagged in the reporting period.

## 3. Project Progress
Three pull requests were closed or merged today:

- **[PR #3282](sipeed/picoclaw PR #3282) – `feat(nodes): add policy-gated system exec`** (merged)  
  Adds an optional `system.exec.v1` capability to the slim node companion, enforcing strict security policies (executable ownership, working root, environment, timeouts, output limits) before executing commands without a shell.

- **[PR #3233](sipeed/picoclaw PR #3233) – `Fix pr 3222 backward compat`** (merged)  
  Resolves a backward compatibility issue introduced by an earlier fix (PR #3222), ensuring existing configurations continue to work.

- **[PR #303](sipeed/picoclaw PR #303) – `fix: make bot greeting name configurable via bot_name setting`** (merged)  
  Allows users to customize the bot’s identity in Telegram and DingTalk greetings via a new `bot_name` field, instead of the hardcoded “PicoClaw”.

Additionally, four issues were closed:
- [#3153](sipeed/picoclaw Issue #3153) – Volcengine Doubao Seed tool call leakage (fixed in a prior release).
- [#3232](sipeed/picoclaw Issue #3232) – Rate limiting broken when no fallback models configured.
- [#3274](sipeed/picoclaw Issue #3274) – Antigravity provider `INVALID_ARGUMENT` regression on `main`.
- [#3278](sipeed/picoclaw Issue #3278) – Google OAuth policy compliance block (see Bugs section).

## 4. Community Hot Topics
The most active discussions in the last 24 hours:

- **Feature: Replace `libolm` with `vodozemac`**  
  [#3088](sipeed/picoclaw Issue #3088) (9 comments, 2 👍) – This high-priority, `help wanted` issue asks to move away from the unmaintained `libolm` library to the official replacement `vodozemac`. The discussion includes compile-time feature flagging and remains open with no maintainer response. The community is clearly concerned about security.

- **Matrix sync loop silently dies after network disruption**  
  [#3203](sipeed/picoclaw Issue #3203) (4 comments, 1 👍) – Users report that the Matrix `/sync` long-polling loop never reconnects after transient failures, leaving the bot unresponsive. The issue lacks a maintainer reply and is flagged as `stale`. This is a high-impact reliability bug.

- **Antigravity OAuth blocked by Google**  
  [#3278](sipeed/picoclaw Issue #3278) (1 comment) – Quickly identified and closed today after a companion PR (#3280) was submitted to fix browser OAuth flow resilience.

**Underlying needs:** The community demands more robust network handling (Matrix), provider compatibility (Google OAuth updates), and modern, secure cryptography (vodozemac).

## 5. Bugs & Stability
New and active bugs reported today, ranked by severity:

| Severity | Issue | Description | Status & Fix |
|----------|-------|-------------|--------------|
| **High** | [#3203](sipeed/picoclaw Issue #3203) | Matrix sync loop has no reconnection logic – silent death after network/server disruption. | Open, stale, no fix PR yet. |
| **High** | [#3281](sipeed/picoclaw Issue #3281) | Web UI chat input becomes very laggy when session history grows moderately long. | Open, reported today, no fix yet. |
| **Medium** | [#3274](sipeed/picoclaw Issue #3274) (closed) | Antigravity provider `INVALID_ARGUMENT` on `main` after v0.3.1 regression. Was caused by tool schema `simple` no longer sufficient. | Closed (likely fixed in main or by another commit). |
| **Medium** | [#3278](sipeed/picoclaw Issue #3278) (closed) | Google OAuth login blocked due to policy compliance. Workaround proposed in PR #3280. | Closed; fix PR [#3280](sipeed/picoclaw PR #3280) opened. |
| **Low** | [#3255](sipeed/picoclaw Issue #3255) | DingTalk chat list preview hard-codes “PicoClaw” instead of actual message content. | Open, stale, no fix PR. |
| **Low** | [#3153](sipeed/picoclaw Issue #3153) (closed) | Volcengine Doubao Seed tool calls leak as raw `<seed:tool_call>` text. | Closed, presumably fixed. |

**Notable fix PRs in flight:**
- [#3280](sipeed/picoclaw PR #3280) – Makes browser OAuth login survive real-world callback conditions (addresses #3274/#3278).
- [#3279](sipeed/picoclaw PR #3279) – Prevents tool-call format leakage into LLM summaries (seahorse variant).
- [#3256](sipeed/picoclaw PR #3256) – Sends Feishu audio/video as native message types instead of generic file.

## 6. Feature Requests & Roadmap Signals
Open feature requests with active discussion or recent PRs:

- **Vodozemac integration** ([#3088](sipeed/picoclaw Issue #3088)) – High priority, labeled `help wanted`. Replacing `libolm` is a security-mandated move. Likely candidate for next minor release if a contributor steps up.
- **Configurable default fallback chain** ([#3200](sipeed/picoclaw PR #3200)) – A UI-driven workflow to set and reorder fallback models. PR is stale but would significantly improve model management.
- **Anthropic prompt caching with `cache_control`** ([#3228](sipeed/picoclaw PR #3228)) – Enables cache markers for Anthropic’s `system` blocks. Important for performance-conscious users.
- **Feishu native media types** ([#3256](sipeed/picoclaw PR #3256)) – Maps audio/video to native Feishu message types. Improves UX for Feishu users.
- **Policy-gated system exec** ([#3282](sipeed/picoclaw PR #3282)) – Already merged; a security feature allowing controlled command execution in node companion.

**Prediction:** The next patch version will likely include fixes for the Antigravity/provider regressions and DingTalk preview issue. Vodozemac integration (if contributed) could land in a minor release within 2–4 weeks.

## 7. User Feedback Summary
Real pain points expressed in recent issues and PRs:

- **Reliability:** Matrix users are frustrated with the bot becoming unresponsive after network glitches (#3203). One user noted that systemd’s `Restart=on-failure` does not help because the process stays alive.
- **OAuth complexity:** Several users reported difficulties authenticating with Google (Antigravity) and other OAuth providers, especially on headless/remote setups (#3278, #3274). The fix in PR #3280 addresses multiple separate root causes.
- **Performance:** The Web UI becomes sluggish with longer chat histories (#3281), impacting user experience for heavy conversational sessions.
- **Provider-specific quirks:** Volcengine Doubao Seed tool-call leakage (#3153) and Anthropic prompt caching limitations (#3228) show that provider-specific integration quality varies.
- **Configuration friction:** The rate limiting bug (#3232) without fallback models and the hardcoded bot name in DingTalk (#3255) indicate that configurability gaps still exist.

Overall, users are actively reporting and fixing issues, indicating an engaged community but also a need for maintainer attention on several stale items.

## 8. Backlog Watch
Long-unanswered or stale items that require maintainer focus:

| Item | Type | Status | Last Update | Reason for Concern |
|------|------|--------|-------------|-------------------|
| [#3088](sipeed/picoclaw Issue #3088) – vodozemac | Issue | Open, high priority, stale | 2026-07-21 | Security-critical dependency; no maintainer comment since creation. |
| [#3203](sipeed/picoclaw Issue #3203) – Matrix reconnection | Issue | Open, stale | 2026-07-21 | Silent bot death after network disruption; no fix PR. |
| [#3255](sipeed/picoclaw Issue #3255) – DingTalk preview | Issue | Open, stale | 2026-07-21 | Low priority but affects UX across a popular channel. |
| [#3200](sipeed/picoclaw PR #3200) – Fallback chain UI | PR | Open, stale | 2026-07-21 | Feature that would simplify model configuration; no review in 3 weeks. |
| [#3228](sipeed/picoclaw PR #3228) – Anthropic cache_control | PR | Open, stale | 2026-07-21 | Important for Anthropic provider efficiency; no maintainer feedback. |
| [#3256](sipeed/picoclaw PR #3256) – Feishu native media | PR | Open, stale | 2026-07-21 | Clean fix for media delivery; waiting for review. |

These items collectively represent the most critical gaps in reliability, security, and feature completeness. Maintainer engagement on at least the vodozemac and Matrix reconnection issues would significantly de-risk the project’s health.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-22

**Project Health: 🟢 Active** — Strong community engagement with 12 PRs updated in the last 24 hours, 3 merged/closed, and 9 open. One new feature issue (#3096) sparks discussion. No new releases today.

---

## 1. Today's Overview

NanoClaw saw a normal-to-high activity day. Three pull requests were merged/closed (including a sync PR and a Langfuse tracing skill), while nine remain open spanning fixes, documentation, and new channel integrations. One new issue proposes adding LINE as a communication channel, drawing 3 comments and indicating growing interest in Asian-market messengers. The project shows steady submission volume for container/operational fixes (WhatsApp media, SELinux, Gmail port blocking) and documentation improvements (Taiwanese README, branch maintenance guide). No new releases were cut, but the pipeline of merged PRs suggests the next release may be accumulating several fixes.

---

## 2. Releases

No new releases as of this digest. The last three closed PRs (#3116, #3114, #3095) may become part of a future minor release.

---

## 3. Project Progress (Merged/Closed PRs)

Three PRs were closed in the last 24 hours:

- **#3116 – `[follows-guidelines] sync pr`**  
  Author: ericsherrill-made4net  
  Routine sync PR (no substantive description). Likely aligns fork or main branch.

- **#3114 – Langfuse tracing skill pr**  
  Author: dtanikella  
  Adds a new utility/integration skill for Langfuse tracing. Strengthens observability for agent runs.

- **#3095 – `[PR: Docs, follows-guidelines, core-team] docs: rewrite branch maintenance guide for the registry-branch model`**  
  Author: glifocat  
  Core-team documentation update improving maintainability guidance.

These merges indicate ongoing investment in both developer experience (docs) and feature expansion (tracing).

---

## 4. Community Hot Topics

**Most active issue:**  
- **#3096 – `feat: Add /add-line skill for LINE Official Account channel support`**  
  Author: joshm1230212 | Updated: 2026-07-21 | Comments: 3  
  [Link to issue](https://github.com/nanocoai/nanoclaw/issues/3096)  
  *Underlying need:* The README’s Request for Skills (RFS) process flagged LINE as missing. LINE dominates Japan, Taiwan, and Thailand – users want a channel adapter that respects existing community conventions. The 3 comments suggest early debate on implementation approach or package availability.

**Notable PRs with ongoing discussion (though no comment counts provided):**  
- **#3095** (closed, but active prior) – documentation rewrite signals community desire for clearer branch workflows.  
- **#3112** – Port collision documentation shows real-world user pain.  
- **#3115** – Gmail API block for OneCLI (security/workflow).

---

## 5. Bugs & Stability

Several open PRs address bugs and regressions. Ranked by severity:

| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| 🔴 High | **#2896** (open) `fix(whatsapp): apply media-failure note at the inbound boundary` | Regression on pending‑question path – approval answers lose media-failure notes. Follow-up to #2895. | PR open 21 days, updated today. |
| 🟠 Medium | **#3113** (open) `fix(whatsapp): stage inbound media where the container can read it` | WhatsApp media inaccessible in container; needs proper staging. | PR opened today. |
| 🟠 Medium | **#1530** (open) `fix: add SELinux :z label to Docker volume mounts` | Volume mounts fail on Fedora/RHEL SELinux-enforcing systems. | PR open 115 days, still no merge. |
| 🟠 Medium | **#2236** (open) `fix(container): align WORKDIR with actual group mount path` | Container `WORKDIR` points to empty artifact dir instead of agent workspace. | PR open 80 days. |
| 🟡 Low | **#3115** (open) `fix(onecli): block legacy Gmail API routes` | OneCLI may allow traffic to deprecated Gmail endpoints. | PR opened today. |
| 🟡 Low | **#3111** (open) `Protect URLs from Telegram legacy-Markdown delimiter stripping` | GitLab-style URLs containing `_` break Telegram messages. | PR opened today. |

No crashes or regressions reported in the last 24h beyond the already-tracked #2896 regression.

---

## 6. Feature Requests & Roadmap Signals

- **#3096 – `/add-line` skill for LINE** (open issue, 3 comments)  
  High alignment with RFS process; likely to be implemented in next release if community contributes the adapter.

- **#3050 – `feat(setup): add Dial to the channel picker + wizard/skills`** (open PR, 7 days)  
  Adds another messaging channel (Dial) with full setup wizard support. Indicates broadening channel ecosystem.

- **#3114 (merged) – Langfuse tracing skill**  
  Observability integration now merged; could be bundled in next release for agent debugging.

- **#2950 – Traditional Chinese README (zh-TW)** (open PR, 18 days)  
  Demonstrates outreach to Taiwanese/Chinese-speaking users, likely to be merged as project expands internationally.

**Prediction for next version:** LINE skill (#3096) if a volunteer picks it up; Dial channel (#3050) is already code-complete; Langfuse tracing (#3114) should appear; possible bugfix releases for the WhatsApp media regression (#2896).

---

## 7. User Feedback Summary

From PRs and issues:

- **Pain point – Port collision with local PostgreSQL (#3112):**  
  Users running their own PostgreSQL on 5432 cannot run `onecli setup` without manually changing ports. Author damenOvernz documented the workaround, reflecting a common complaint.

- **Pain point – WhatsApp media handling (#2896, #3113):**  
  Two PRs in two weeks targeting the same area. Users running WhatsApp channels in containers hit persistent media delivery failures and a subtle regression when approving messages.

- **Pain point – Docker/SELinux (#1530):**  
  Still unmerged after 115 days. This likely frustrates Fedora/RHEL users, as `:z` label is trivial to add and safe.

- **Satisfaction – Community channel skills (LINE, Dial) and tracing (#3114):**  
  Positive signal: developers are contributing new skills and integrations, indicating the project is meeting real needs.

- **Satisfaction – Documentation improvements (#3095, #2950):**  
  Users volunteering to translate README and rewrite maintenance guides shows healthy community buy-in.

---

## 8. Backlog Watch

These issues/PRs have been open for weeks to months without maintainer merge/close:

- **#1530 – `fix: add SELinux :z label to Docker volume mounts`** (open since 2026-03-29, 115 days)  
  Simple, low-risk fix. Maintainer attention needed to unblock Fedora/RHEL users.

- **#2236 – `fix(container): align WORKDIR with actual group mount path`** (open since 2026-05-03, 80 days)  
  Clear bug description; would improve container behavior for all users.

- **#2896 – `fix(whatsapp): apply media-failure note at the inbound boundary`** (open since 2026-06-30, 22 days)  
  Regression fix with ongoing discussion; marked as follow-up to a merged PR. Needs final review.

- **#2950 – `docs: add Traditional Chinese README (README_zh-TW.md)`** (open since 2026-07-04, 18 days)  
  Documentation only; likely waiting on code review bandwidth.

- **#3050 – `feat(setup): add Dial to the channel picker`** (open since 2026-07-14, 8 days)  
  Large feature PR; may require more testing or maintainer sign-off.

**No new unanswered issues with zero maintainer response** were identified in today’s data; the project appears responsive overall.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-07-22

## 1. Today's Overview
IronClaw remains in an intense rearchitecture phase, with the `Reborn` branch nearing its v1 release candidate. Yesterday’s activity was exceptionally high: 41 issues were updated (27 still open), 50 pull requests were touched (17 merged/closed), and the team cut the first release candidate of the rebuilt monolith (`ironclaw-v1.0.0-rc.1`). Core contributors are executing a tightly coordinated landing plan (tracked in [#2987](https://github.com/nearai/ironclaw/issues/2987)), consolidating stores, unifying runtime graphs, and hardening error recovery. The project shows strong momentum and disciplined staging, though the volume of in-flight work (33 open PRs) suggests the next few days will be critical for landing before a stable v1.

## 2. Releases
**`ironclaw-v1.0.0-rc.1`** (released 2026-07-20)  
- **Full rearchitecture**: the binary is now the rebuilt `Reborn` CLI—a ground-up rewrite of the agent runtime, storage, extension host, and web UI.  
- **Breaking changes**: This is **not** an incremental update from the 0.29.x line. Existing configurations and integrations likely require migration; official migration notes are expected in a follow-up document.  
- **No detailed changelog** was published with the RC – the team refers to the `Reborn` epic (#2987) for the full scope.

## 3. Project Progress
**Merged/closed PRs today (17 total):**  
- **Store consolidation** – [#6430](https://github.com/nearai/ironclaw/pull/6430) removed in-memory ratchet stores, migrating to filesystem-backed stores (subagent goals, OpenAI-compatible refs, instruction materialization).  
- **Witness authority** – [#6432](https://github.com/nearai/ironclaw/pull/6432) completed the “witness always-present” pattern, routing sealed mounts/reservations through the witness authority.  
- **Unified generic extension runtime** – [#6116](https://github.com/nearai/ironclaw/pull/6116) reconciled the unified extension runtime branch with 92 new commits from `main`.  
- **Security fix** – [#6196](https://github.com/nearai/ironclaw/pull/6196) bumped `dompurify` (JavaScript dependency) from 3.2.3 to 3.4.11, addressing a known XSS vulnerability.  
- **Other**: `dependabot` bumps for Tokio ecosystem, serialization libraries, and Rust toolchain.

**Open PRs of note moving forward:**  
- [#6442](https://github.com/nearai/ironclaw/pull/6442) – Unifies runtime store graph selection (production vs. local-dev).  
- [#6438](https://github.com/nearai/ironclaw/pull/6438) – Seals process redispatch authority, replacing DTO-based dispatch with witness-only routing.  
- [#6437](https://github.com/nearai/ironclaw/pull/6437) – Makes model-visible failures recoverable (key to error-recoverability endgame).  
- [#6425](https://github.com/nearai/ironclaw/pull/6425) – Fixes WebUI SSE streams surviving navigation between threads.

## 4. Community Hot Topics
| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#2987](https://github.com/nearai/ironclaw/issues/2987) – [OPEN] | 44 | **Reborn architecture landing strategy**. The most active thread—tracks the entire delivery plan with grouped PRs. Community and core contributors are following for cutover timing. |
| [#6263](https://github.com/nearai/ironclaw/issues/6263) – [CLOSED] | 10 | **Final in-memory store consolidation**. High-value cleanup; closed via #6430. |
| [#6389](https://github.com/nearai/ironclaw/issues/6389) – [OPEN] | 10 | **Collapse of `build_local_runtime` and `build_production_shaped`** into one `build_runtime(cfg)`. Debate centers on the right `DeploymentConfig` shape. |
| [#2767](https://github.com/nearai/ironclaw/issues/2767) – [CLOSED] | 7 | Epic: separate engine v2 capability background from callable tool schemas. Closed – signals the Reborn product surface is ready. |

**Underlying need**: The community is closely tracking the Reborn landing because it affects every operator and plugin developer. The high engagement on store consolidation (#6263, #6389) reflects staff-level desire for a clean, unified runtime that removes legacy debt.

## 5. Bugs & Stability
- **No critical crash bugs reported today**.  
- **Dogfooding bug-fix epic** [#6394](https://github.com/nearai/ironclaw/issues/6394) (open, created 07/21) explicitly tracks bug fixes for 07/20–07/24, suggesting the team is actively hunting regressions from the RC.  
- **SSE stream fix** – PR [#6425](https://github.com/nearai/ironclaw/pull/6425) addresses a WebUI bug where Server-Sent Events were lost during navigation between threads/tabs while a run was active. This is a moderate-severity UX regression for multi-conversation users.  
- **Error-recoverability work** – PR [#6437](https://github.com/nearai/ironclaw/pull/6437) and epic [#6284](https://github.com/nearai/ironclaw/issues/6284) aim to make 100% of mid-run errors recoverable, which directly improves stability.

**Severity ranking**: SSE bug (moderate) → recoverability gaps (lower, being fixed proactively).

## 6. Feature Requests & Roadmap Signals
- **Dedicated custom instructions / master prompt** – [#6433](https://github.com/nearai/ironclaw/issues/6433) (opened 07/21, 0 comments). A user asks for a UI section akin to ChatGPT/Claude for setting persistent personalization. This is a low-effort, high-value UX improvement likely to be picked up post-v1.  
- **Per-user hosted MCP discovery** – PR [#6365](https://github.com/nearai/ironclaw/pull/6365) (draft) adds connector tools for worker agents. Though still in reference state, it signals the direction toward multi-agent MCP integration.  
- **Design system tokens + /playground** – PR [#5563](https://github.com/nearai/ironclaw/pull/5563) from contributor `achalvs` is pausing deeper integration while the team specs a design system for WebUI v2. This may land in the next RC.

**Prediction for next version (v1.0.0-rc.2 or stable)**: custom instructions UI, design system tokens, and further error-recoverability hardening.

## 7. User Feedback Summary
- **Pain points**: The lack of a master-prompt feature (#6433) highlights that IronClaw currently expects users to bake preferences into chat context – a friction point compared to commercial AI assistants.  
- **Use cases**: The activity around extensions (Google, MCP) and multi-channel support (#2392) shows operators are integrating IronClaw into real Slack/Telegram/WeCom workflows.  
- **Satisfaction**: The high number of closed issues (14 today) and merged PRs (17) suggests contributors are responsive, and the RC release implies the team is confident enough to cut a candidate. However, the dogfooding bug epic (#6394) indicates the team expects to fix rough edges before graduation.

## 8. Backlog Watch
| Issue | Age | Status |
|-------|-----|--------|
| [#2355](https://github.com/nearai/ironclaw/issues/2355) – Persistent multi-identity Chrome browsing | Opened 2026-04-12 (3 months ago) | Still open, no recent activity. This feature is complex (sandbox, CDP integration) and may be deferred past v1. |
| [#2392](https://github.com/nearai/ironclaw/issues/2392) – Host-level multi-account support for messaging channels | Opened 2026-04-13 | Epic with no comments but labeled `scope: channel`. No maintainer response yet; could block real deployments with WeCom. |
| [#2599](https://github.com/nearai/ironclaw/issues/2599) – Enforce gateway feature boundaries | Opened 2026-04-17 | Low engagement (2 comments). Likely waiting for the Reborn product surface migration to settle. |
| [#3773](https://github.com/nearai/ironclaw/issues/3773) – Crate boundary & ownership audit | Opened 2026-05-19 | No contributor traction; audit document exists but no follow-up PRs. |

These items are not actively blocking v1 but represent technical debt that will need addressing in subsequent releases. Maintainers may want to comment on timelines or close them as obsolete if Reborn renders them moot.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-22

---

## 1. Today's Overview

Moderate development activity was observed in the last 24 hours, with 1 issue updated and 10 pull requests (PRs) actively handled. Of those PRs, 5 were merged or closed, signaling steady progress on bug fixes and feature enhancements. The most notable improvement is a fix for image attachment state not syncing when switching between vision and non-vision models (PR #2373), which directly addresses a user-reported bug. Meanwhile, three stale dependency update PRs remain open without maintainer response, indicating a slight backlog in housekeeping tasks.

---

## 2. Releases

No new releases were published today.

---

## 3. Project Progress

**Merged/Closed PRs (5)**  

- **#2372** — Fix for OpenClaw token proxy SSE truncation. Author: fisherdaddy. [PR #2372](https://github.com/netease-youdao/LobsterAI/pull/2372)  
- **#2371** — Improved browser annotation handling within cowork mode: now supports style-only changes without comments, shows original-to-new value in prompt, clears draft annotations properly, and retains screenshot metadata. Author: liugang519. [PR #2371](https://github.com/netease-youdao/LobsterAI/pull/2371)  
- **#2370** — Unified subscription‑intercept dialogs for artifact sharing and local service deployment; separate login/subscription prompts and improved test coverage. Author: liugang519. [PR #2370](https://github.com/netease-youdao/LobsterAI/pull/2370)  
- **#2369** — Refined artifact share permission flow: distinguishes creation from management states, adds explicit “create share” and “update permissions” actions, and improves UX for local service deployment. Author: liugang519. [PR #2369](https://github.com/netease-youdao/LobsterAI/pull/2369)  
- **#2368** — Windows updates now install silently via NSIS `/S` flag (elevated with PowerShell), with graceful fallback on UAC decline. Author: fisherdaddy. [PR #2368](https://github.com/netease-youdao/LobsterAI/pull/2368)  

**Notable Open PR**  

- **#2373** — (Open) Syncs image attachment state (base64 vs file path) when the user switches between visual and non‑visual models. This directly addresses issue #1861. Author: yaodong-shen. [PR #2373](https://github.com/netease-youdao/LobsterAI/pull/2373)

---

## 4. Community Hot Topics

**Most Active Issue**  
- **#1861** — “图片附件不随模型切换重新处理（supportsImage 状态不同步）”  
  User reports that image attachments do not adjust when toggling between models that support images and those that do not. 2 comments, opened 2026-04-28, updated 2026-07-21.  
  [Issue #1861](https://github.com/netease-youdao/LobsterAI/issues/1861)

**Analysis:** This bug has been open for nearly three months but only saw action today with the creation of fix PR #2373. The underlying need is clear: users expect a seamless experience when switching models mid-conversation, especially when mixing vision and non‑vision models.

**Most Active PR (by recency)**  
- **#2374** — Adds a permanent setting to hide the sidebar ad banner (resolves #2342).  
  [PR #2374](https://github.com/netease-youdao/LobsterAI/pull/2374)  
  This feature request (hide ads permanently) had been implicitly requested by users; it signals a desire for a less cluttered UI.

---

## 5. Bugs & Stability

| Severity | Bug ID / PR | Description | Status |
|----------|-------------|-------------|--------|
| **Medium** | Issue #1861 | Image attachment state not updated when switching between vision / non‑vision models. Causes loss of base64 data for visual models or stale data for non‑visual models. | Open, fix PR #2373 submitted |
| **Low** | PR #2372 | SSE response truncation in OpenClaw token proxy. Likely affected streaming outputs. | Fixed / merged |
| **Low** | PR #2371 (sub‑fixes) | Cowork browser annotations not clearing properly, leftover stall states in WebView. | Fixed / merged |
| **Low** | PR #2368 | Windows installer previously required interactive UAC, now silent with error handling. | Fixed / merged |

Overall stability appears good; no crashes or regressions were reported today. The image sync bug is the only open medium‑severity issue, with a fix already in review.

---

## 6. Feature Requests & Roadmap Signals

- **Permanent ad‑banner hide (PR #2374)** – A user‑facing toggle in Settings → General to permanently disable the sidebar ad banner. This suggests the community values a cleaner workspace. Likely to appear in the next minor release.
- **Artifact sharing & subscription enhancements (PR #2370, #2369)** – Improved permission management, subscription gating, and UX for sharing artifacts. These changes indicate ongoing work toward a more monetized and controllable sharing ecosystem.
- **Windows silent updates (PR #2368)** – Already merged; makes updates less disruptive on Windows. Signals continued platform polish.

**Prediction for next version:** The fixes from PR #2373 (image sync) and PR #2374 (ad hide) are strong candidates for inclusion, along with the already‑merged artifact sharing improvements.

---

## 7. User Feedback Summary

**Pain Points**  
- Image attachment handling inconsistency when switching models (Issue #1861) – user explicitly described three failure scenarios, indicating a real workflow disruption.  
- No permanent way to hide sidebar ads until PR #2374; previous dismissals were temporary (Issue #2342).

**Satisfaction Signals**  
- The cooperative (cowork) browser annotation system is receiving iterative improvements (PR #2371), showing the dev team actively polishing features users rely on.  
- Artifact sharing permission flow has been refined based on feedback (PR #2369).

Overall, users appear to be engaged with the product’s advanced features (vision, artifacts, cowork) but expect reliable state management and minimal visual clutter.

---

## 8. Backlog Watch

Three dependency‑update PRs have been open since 2026-04-02 with no maintainer response:

- **#1279** — chore(deps-dev): bump cross-env from 7.0.3 to 10.1.0  
  [PR #1279](https://github.com/netease-youdao/LobsterAI/pull/1279)
- **#1280** — chore(deps): bump react-dom from 18.3.1 to 19.2.4  
  [PR #1280](https://github.com/netease-youdao/LobsterAI/pull/1280)
- **#1281** — chore(deps-dev): bump vite from 5.4.21 to 8.0.9  
  [PR #1281](https://github.com/netease-youdao/LobsterAI/pull/1281)

These involve major version bumps (React 18→19, Vite 5→8, cross-env 7→10) and could introduce breaking changes if merged blindly. They have been stale for over three months and require maintainer decision (merge, close, or rebase). Leaving them unresolved may increase security risk or cause divergence from upstream.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-07-22

## Today's Overview
Activity across the Moltis repository remains very low. Only one open issue and one open pull request were updated in the last 24 hours, and no new commits, merged PRs, or releases occurred. The project appears stable but with limited momentum; no features or bug fixes were advanced today. The single PR is a routine dependency bump, indicating ongoing maintenance rather than active development.

## Releases
None – no new releases were published today.

## Project Progress
No pull requests were merged or closed today. The only open PR, [#1161](https://github.com/moltis-org/moltis/pull/1161), is an automated dependency update (Astro from 7.0.9 to 7.1.3 in the `/docs` directory). No feature work or bug fixes were integrated.

## Community Hot Topics
The most active item today is an enhancement request:

- **[Issue #574 – [Feature]: Model Routing Per topic](https://github.com/moltis-org/moltis/issues/574)**  
  *Author: azharkov78 | Comments: 5 | 👍: 1*  
  This open issue proposes routing queries to different AI models based on topic. It has drawn modest discussion (5 comments) since its creation in April 2026. The underlying need is for intelligent model selection to optimize cost, performance, or domain specificity per user request. No maintainer response is visible in the last 24 hours.

The PR [#1161](https://github.com/moltis-org/moltis/pull/1161) has no comments or reactions.

## Bugs & Stability
No bug reports, crashes, or regressions were filed or updated today. The project shows no stability concerns reflected in the past day's data.

## Feature Requests & Roadmap Signals
The only feature request is **Issue #574** (topic-based model routing). Given its age (over 3 months) and lack of recent maintainer engagement, it is uncertain whether this will be included in the next release. The feature would likely require significant architectural changes to Moltis’s routing layer, and today’s lack of activity suggests it is not currently prioritized.

## User Feedback Summary
No explicit user feedback (positive or negative) was recorded today. The single enhancement request indicates a user desire for more granular control over model selection, which could improve flexibility for diverse use cases. No pain points or satisfaction indicators are otherwise available.

## Backlog Watch
- **[Issue #574 – Model Routing Per topic](https://github.com/moltis-org/moltis/issues/574)**  
  Created on 2026-04-06, last updated today (2026-07-22) with no maintainer comment. This enhancement request has 5 comments and 1 thumbs-up. Its prolonged open state without progress may signal a backlog item that needs maintainer attention or a decision on whether to accept or reject the proposal.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-22

## 1. Today’s Overview

The CoPaw project (github.com/agentscope-ai/QwenPaw) saw high activity over the past 24 hours: **42 issues** were updated (21 open, 21 closed) and **50 pull requests** were updated (20 open, 30 merged/closed). One new release, **v2.0.1-beta.1**, was tagged with fixes for Tauri entry points and memory space errors. The community remains engaged around bug reports and feature discussions, with the longest-running help-wanted issue (#2291) still drawing 65 comments. The PR pipeline is healthy, with multiple governance and tool-registration improvements being reviewed and merged.

## 2. Releases

**v2.0.1-beta.1** was released today. Changes include:

- **Fix:** Use absolute import in the Tauri entry point ([#6234](https://github.com/agentscope-ai/QwenPaw/pull/6234))
- **Chore:** Bump version to 2.0.1b1 ([#6266](https://github.com/agentscope-ai/QwenPaw/pull/6266))
- **Fix (memoryspace):** Catch `OSError` in `_saved_tool_refs` to prevent crashes during memory operations

No breaking changes are documented in the release notes. Users upgrading from v2.0.0 should update their Docker images or pip install accordingly.

## 3. Project Progress

**30 pull requests were merged or closed** in the last 24 hours. Notable advances include:

- **Governance & sandbox interface** – PR [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) (closed) and [#5546](https://github.com/agentscope-ai/QwenPaw/pull/5546) (closed) introduced foundational governance policy patterns and a permission-asking mechanism for `sudo`.
- **OMP workflow mode integration** – PR [#5882](https://github.com/agentscope-ai/QwenPaw/pull/5882) (closed) added five workflow modes (UltraQA, Ralph, Ultrawork, Autopilot, Team) as a bundle plugin, along with `spawn_subagent` enhancements.
- **Tool registration unification** – PR [#6190](https://github.com/agentscope-ai/QwenPaw/pull/6190) (closed) auto-registers tools via `@tool_descriptor` and `PluginApi`, reducing manual maintenance.
- **Logging rotation configuration** – PR [#6183](https://github.com/agentscope-ai/QwenPaw/pull/6183) (closed) made log rotation limits configurable via environment variables.
- **Agent configuration copy** – PR [#6262](https://github.com/agentscope-ai/QwenPaw/pull/6262) (closed) added a one-click copy feature for agent settings.
- **User-editable agent modes** – PR [#6270](https://github.com/agentscope-ai/QwenPaw/pull/6270) (closed) allows users to edit agent mode configurations.

Several follow-up PRs remain open, including scroll context compaction ([#6323](https://github.com/agentscope-ai/QwenPaw/pull/6323)), per-session model overrides ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)), and OMP hardening ([#6317](https://github.com/agentscope-ai/QwenPaw/pull/6317)).

## 4. Community Hot Topics

The most active issues (by comment count) are:

- **[#2291 – Help Wanted: Open Tasks](https://github.com/agentscope-ai/QwenPaw/issues/2291)** (65 comments, closed) – A meta-issue listing open tasks for contributors. It remains a magnet for discussion and task assignment.
- **[#6257 – Multiple tool calls produce identical thinking output](https://github.com/agentscope-ai/QwenPaw/issues/6257)** (13 comments, closed) – A bug where repeated tool calls share the same reasoning block. Users expressed frustration with inefficient tool loops.
- **[#4873 – Dual subagents cause infinite polling and cannot interrupt from Feishu](https://github.com/agentscope-ai/QwenPaw/issues/4873)** (5 comments, closed) – Highlights a critical concurrency issue in channel integrations.
- **[#6242 – Console embedding dimensions not sent to OpenAI API](https://github.com/agentscope-ai/QwenPaw/issues/6242)** (4 comments, closed) – A configuration gap for ReMe Light memory dimensions.
- **[#6297 – Drag-and-drop file upload for images/documents](https://github.com/agentscope-ai/QwenPaw/issues/6297)** (4 comments, open) – A feature request reflecting a strong workflow need (contract review).

PR comment counts were not provided, but open PRs such as [#6284](https://github.com/agentscope-ai/QwenPaw/pull/6284) (QwenPaw Creator app) and [#6323](https://github.com/agentscope-ai/QwenPaw/pull/6323) (scroll compaction) are likely to attract discussion.

## 5. Bugs & Stability

Several bugs were reported or addressed today. They are ranked by severity:

- **High Severity:**
  - **[#6324](https://github.com/agentscope-ai/QwenPaw/issues/6324)** – Large model responses are truncated (MiniMax-M3). No fix PR yet; likely a streaming/chunking issue.
  - **[#6314](https://github.com/agentscope-ai/QwenPaw/issues/6314)** – `RemoteProtocolError` because CoPaw actively closes the connection before the model finishes sending response body. A network-level regression.
  - **[#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307)** – v2.0 introduces ~2s fixed overhead per conversational reply compared to v1.x, attributed to request processing architecture.
  - **[#6299](https://github.com/agentscope-ai/QwenPaw/issues/6299)** – Deleted session records persist in `history.db`, causing sequence collisions and cross-session contamination. A fix PR ([#6068](https://github.com/agentscope-ai/QwenPaw/pull/6068)) is under review.

- **Medium Severity:**
  - **[#6320](https://github.com/agentscope-ai/QwenPaw/issues/6320)** – LaTeX formulas with square roots fail to render.
  - **[#6322](https://github.com/agentscope-ai/QwenPaw/issues/6322)** – Platform domain redirects to advertisement pages on mobile networks.
  - **[#6301](https://github.com/agentscope-ai/QwenPaw/issues/6301)** – Incorrect timezone conversion for naive UTC timestamps; a fix PR ([#6309](https://github.com/agentscope-ai/QwenPaw/pull/6309)) is open.

- **Low Severity (with fix PRs):**
  - **[#6273](https://github.com/agentscope-ai/QwenPaw/issues/6273)** – Unify task tracking semantics across entry points (PR in discussion).
  - **[#6258](https://github.com/agentscope-ai/QwenPaw/issues/6258)** – OpenAI max output tokens setting not honored.

Several bug-fix PRs were merged today: [#6313](https://github.com/agentscope-ai/QwenPaw/pull/6313) (tool registration fix), [#6079](https://github.com/agentscope-ai/QwenPaw/pull/6079) (sudo permission), and [#6183](https://github.com/agentscope-ai/QwenPaw/pull/6183) (log rotation). Open fix PRs include [#6068](https://github.com/agentscope-ai/QwenPaw/pull/6068) (scroll session consistency) and [#6317](https://github.com/agentscope-ai/QwenPaw/pull/6317) (OMP hardening).

## 6. Feature Requests & Roadmap Signals

The following feature requests received community attention today:

- **Drag-and-drop file upload** ([#6297](https://github.com/agentscope-ai/QwenPaw/issues/6297)) – Essential for contract review workflows. Likely to be prioritized in next minor release.
- **Mobile web console adaptation** ([#6281](https://github.com/agentscope-ai/QwenPaw/issues/6281)) – Repeated need from users; could be a design sprint candidate.
- **Desktop workspace shortcut button** ([#6083](https://github.com/agentscope-ai/QwenPaw/issues/6083)) – One-click access to output files. Already has community support.
- **Per-session model overrides** ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) – An open PR, likely to be merged after review.
- **Configurable tool descriptions** ([#6286](https://github.com/agentscope-ai/QwenPaw/issues/6286), closed) – Users want to disable or customize built-in tool descriptions to save tokens. Implementation is under discussion.
- **Pre-condition rules in AGENTS.md** ([#6321](https://github.com/agentscope-ai/QwenPaw/issues/6321)) – A sophisticated request for workflow verification before tool calls.
- **Qwen3.8 Max preview model support** ([#6285](https://github.com/agentscope-ai/QwenPaw/issues/6285)) – Straightforward model list update, likely in next release.
- **Theme/skin module** ([#6312](https://github.com/agentscope-ai/QwenPaw/pull/6312)) – A draft PR from the help-wanted tasks.

Predictions for next version: drag-and-drop upload, per-session model overrides, mobile web improvements, and model list updates.

## 7. User Feedback Summary

User sentiment in the past 24 hours shows a mix of satisfaction with the feature richness and frustration with v2.0 stability:

- **Pain points:**
  - Performance regression: v2.0 adds ~2s overhead per reply ([#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307)).
  - Session contamination: deleted chats reappear and cause context confusion ([#6299](https://github.com/agentscope-ai/QwenPaw/issues/6299)).
  - Repeated / infinite tool calls: multiple issues report identical thinking output ([#6257](https://github.com/agentscope-ai/QwenPaw/issues/6257)) and loop detection gaps ([#5657](https://github.com/agentscope-ai/QwenPaw/issues/5657)).
  - File type handling: no drag-and-drop for images/office docs ([#6297](https://github.com/agentscope-ai/QwenPaw/issues/6297)).
  - Channel integration: subagent approval requests not pushed to external channels ([#5295](https://github.com/agentscope-ai/QwenPaw/issues/5295)).

- **Use cases driving requests:**
  - Contract review (drag-and-drop documents)
  - Data analysis (workspace file access)
  - Multi-agent workflows (governance, sandbox)
  - Mobile/tablet operation (on-the-go monitoring)

Overall, users appreciate the rapid development pace but are vocal about regressions introduced in v2.0.

## 8. Backlog Watch

The following issues and PRs have been open for some time and may need maintainer attention:

- **Issues:**
  - [#2055](https://github.com/agentscope-ai/QwenPaw/issues/2055) (closed, but unresolved behavior) – OpenAI-compatible model returning excessive tool_calls. Originally opened March 2026, closed today but the underlying compatibility problem may still exist.
  - [#5295](https://github.com/agentscope-ai/QwenPaw/issues/5295) (closed) – Subagent approval notification not pushed to external channel. The fix may be partial; users continue to report similar problems.
  - [#6083](https://github.com/agentscope-ai/QwenPaw/issues/6083) (open) – Desktop workspace shortcut button. No assignee, open since July 14.

- **PRs needing review or merging:**
  - [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992) – Per-session model overrides (first-time contributor). No reviewer comments yet.
  - [#6203](https://github.com/agentscope-ai/QwenPaw/pull/6203) – Fix Windows tasklist liveness probe (first-time contributor). Marked “ready-for-human-review”.
  - [#6068](https://github.com/agentscope-ai/QwenPaw/pull/6068) – Fix Scroll session ID migration. Addresses the critical #6299 bug.
  - [#6296](https://github.com/agentscope-ai/QwenPaw/pull/6296) – Refresh skills after market installation. Minor but still open.
  - [#6284](https://github.com/agentscope-ai/QwenPaw/pull/6284) – QwenPaw Creator app. Large feature PR; needs architectural review.

Maintainers should prioritize the session consistency fix (#6068) and the performance regression (#6307) to improve stability.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw Project Digest – 2026-07-22

**Analysis of GitHub activity from 2026-07-21 00:00 UTC to 2026-07-22 00:00 UTC.**

---

### 1. Today's Overview

Development velocity remains very high: **50 issues** and **50 pull requests** received updates in the last 24 hours, with only 3 issues and 9 PRs reaching a closed/merged state. The open backlog is substantial (47 open issues, 41 open PRs), and many items carry `priority:p1` or `S0/S1` severity labels, indicating significant unresolved stability and security concerns. No new releases were cut today, but multiple high-risk RFCs and large feature branches (Goal mode, OpenAI compatible adapter, MCP memory leak) are advancing. The project appears to be in a phase of aggressive feature addition while simultaneously contending with regressions and architectural debt.

- **Activity level**: Very high
- **Health signals**: Strong community engagement, but bug triage and PR merge velocity lag behind issue creation.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress

Only 9 pull requests were merged or closed today; the top 20 PRs (by comment count) remain open. Based on available closed issues, notable resolutions include:

- **#7082** [CLOSED] – `feat(channel/mattermost): add optional WebSocket listener mode` – An enhancement to Mattermost channel, now merged.
- **#9120** [CLOSED] – `[Bug]: SOP routing evaluates switch after a false top-level when` – A runtime bug in SOP routing fixed, preventing incorrect step traversal.
- **#9086** [CLOSED] – `RFC: Structured Security Audit Pipeline` – A design proposal accepted and closed, though not yet implemented.

No PRs were explicitly listed as merged today, but the 9 merged/closed items likely include smaller fixes or documentation updates not shown in the top 20.

---

### 4. Community Hot Topics

The most active discussions (by comments and reactions) touch on core architecture and user-facing features:

- **#8226** [6 comments] – *Feature: Add typed per-agent git identity for built-in git operations* – Sustained interest around multi-tenancy in tool configuration.
- **#8505** [6 comments] – *Bug: Telegram channel cannot be configured* – High frustration; users cannot get Telegram working despite Quickstart instructions.
- **#8303** [4 comments, 1 👍] – *RFC: Goal mode for bounded autonomous session work* – A heavily anticipated feature; the discussion probes scope and integration with existing channels.
- **#8603** [4 comments] – *RFC: OpenAI Chat Completions compatibility adapter* – Broad demand for OpenAI API compatibility; critical for tool ecosystem adoption.
- **#9086** [1 comment, 1 👍, now CLOSED] – *RFC: Structured Security Audit Pipeline* – Closed without implementation, suggesting maintainers may have deferred or redirected the design.

**Underlying needs**: Users want reliable Telegram setup, seamless integration with existing LLM clients (OpenAI API), durable goal-driven sessions, and better security observability.

---

### 5. Bugs & Stability

Multiple **S0 (data loss/security risk)** and **S1 (workflow blocked)** bugs were active this period. No fix PRs are yet visible for the highest-severity items:

| Issue | Severity | Title | Status |
|-------|----------|-------|--------|
| [#8279](zeroclaw-labs/zeroclaw Issue #8279) | S0 | Delegate bypasses parent's tool allowlist – sub-agent can invoke excluded tools | Open, risk:high |
| [#9247](zeroclaw-labs/zeroclaw Issue #9247) | S0 | Shell Tool Workspace Boundary Bypass (symlink escape) | Open, new today |
| [#8505](zeroclaw-labs/zeroclaw Issue #8505) | S1 | Telegram channel cannot be configured | Open, S1 |
| [#8642](zeroclaw-labs/zeroclaw Issue #8642) | S2 (risk:high) | MCP/tool-schema cloning drives unbounded RSS growth (OOM path) | In progress |
| [#8731](zeroclaw-labs/zeroclaw Issue #8731) | S2 | Stdio-based MCP servers accumulating as zombie processes | In progress |
| [#8718](zeroclaw-labs/zeroclaw Issue #8718) | S2 | `zeroclaw config init` ships a config template that breaks local_whisper transcription | In progress |
| [#9240](zeroclaw-labs/zeroclaw Issue #9240) | unlabeled | `save_dirty` silently drops writes when map key contains a dot (e.g. `gpt-4.1`) | Open, risk:medium |

**Worst regressions**: The two S0 security bypasses (workspace escape and tool allowlist bypass) are critical and require immediate maintainer attention. The MCP memory leak is also concerning as it affects long-running deployments.

---

### 6. Feature Requests & Roadmap Signals

Several ambitious RFCs and feature requests suggest a busy near-term roadmap:

- **#8603** – OpenAI Chat Completions adapter — large PR [#8486](zeroclaw-labs/zeroclaw PR #8486) is already in progress, likely shipping in the next release.
- **#8303** – Goal mode — a stacked PR series [#8687–#8746](zeroclaw-labs/zeroclaw) is under review; could land within one or two releases.
- **#8568** – Mixture-of-Agents virtual provider — RFC, not yet implemented, but fits the trend toward multi-model orchestration.
- **#8780** – Real-time speech-to-speech for Gemini Live — newer RFC; longer-term.
- **#9228** – Eval harness results dashboard — deferred from #7065, but a follow-up with PR [#9248](zeroclaw-labs/zeroclaw PR #9248) suggests active work.

**Predictions**: OpenAI compatibility and Goal mode are the most likely features to appear in the next minor release (v0.9?). The eval harness dashboard and skill CRUD hooks may follow.

---

### 7. User Feedback Summary

Real user pain points surfaced in the last 24 hours include:

- **Telegram onboarding broken** (#8505) – Setup fails despite Quickstart; bot remains unresponsive. User frustration is high.
- **Documentation errors** (#8810) – A contributor bluntly called exampledocs “slop,” indicating quality concerns.
- **Silent data loss** (#9240) – Config saves with dot-containing model IDs silently fail; users lose cost-rate settings without warning.
- **Windows shell ignored** (#9182 PR) – Users could not use PowerShell despite configuration; fix PR exists.
- **Config init broken** (#8718) – New installations get a template that disables voice transcription silently, surprising users.
- **Channel no-reply confusion** (#8410) – Conditional tasks that choose silence still produce unwanted replies.

**Satisfaction signals**: The Goal mode RFC (#8303) and MoA (#8568) received positive reactions. The active PR stacks show strong contributor investment.

---

### 8. Backlog Watch

Several important issues and PRs have been open for weeks or lack maintainer response:

- **#8226** *(June 23)* – Typed per-agent git identity – `status:accepted, no-stale` but no assignee or PR. Community interest suggests it should be scheduled.
- **#8309** *(June 25)* – SkillForge orphaned – the feature is wired to nothing; maintainers need to decide to finish or remove.
- **#8348** *(June 26)* – Skill CRUD hook – accepted but no movement; external users waiting for notification hooks.
- **#8396** *(June 27)* – Wire protocol RFC – accepted without follow-up; impacts provider onboarding.
- **#8541** *(June 30)* – Matrix thread-scoped history – accepted, no PR yet.
- **#8718** *(July 4)* – Config init bug – `priority:p1, quickstart` with a fix PR likely pending, but no closure for a week.
- **#8600** *(July 1)* – Per-chat model switching – high demand (1 👍) but no assignee.

Many PRs are also stalled with the `needs-author-action` label (#9194, #8949, #9182, #8486, etc.). Maintainer bandwidth appears strained.

**Conclusion**: ZeroClaw is in a high-innovation phase but must address security-critical bugs and unstick the PR review pipeline to maintain project health.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*