# OpenClaw Ecosystem Digest 2026-06-13

> Issues: 500 | PRs: 484 | Projects covered: 13 | Generated: 2026-06-13 02:42 UTC

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

# OpenClaw Project Digest — 2026-06-13

## Today's Overview
The project shows **high activity** with 500 issues and 484 PRs updated in the last 24 hours, including 140 merged/closed PRs and 2 new releases. Activity is broadly distributed across security hardening, bug fixes, and feature development, but a significant portion of open issues (409 out of 500) and PRs (344 out of 484) signals a growing maintenance backlog. The two new releases (v2026.6.6 stable and v2026.6.6-beta.2) focus on tightening security boundaries across multiple subsystems, reflecting a sustained push toward safer agent execution. Several P0/P1 regressions and memory leak reports indicate stability remains an active concern.

## Releases
- **v2026.6.6** (stable) and **v2026.6.6-beta.2** (preview) were published today.
- **Highlights (same for both):** Security boundaries are substantially tighter across transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, elevated sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group actions; exec
- No breaking changes or migration notes were included in the data provided.

## Project Progress
The following notable PRs were merged/closed today (based on the top 30 by comment count):

- **#92568** (closed) – Fix cron task cancellation by routing through Gateway’s `tasks.cancel` method with AbortSignal support.
- **#92382** (closed) – Fix webchat text streaming being stalled when `before_agent_finalize` hooks are registered.
- **#92319** (closed) – Add `workboard_delete` agent tool and CLI command for card removal (fixes #92314).
- **#92357** (closed) – Fix keyword-only results being silently dropped in hybrid memory search when chunk IDs don’t overlap (fixes #92337).
- **#92427** (closed) – Increase `skill_workshop` description limit from 160 to 500 characters.
- **#92308** (closed) – Fix Windows absolute path mangling in QMD command resolution (fixes #92302).

Other open PRs that advanced code quality or features include: `#92577` (deduplicate assistant thinking transcripts), `#92579` (bound ancestor context file walk to home dir), `#92341` (CJK textScore=0 fix in memory-core), `#92103` (preserve Commander exit codes), `#92493` (clear provider auth prewarm on stop), and `#92574` (browser action-input coverage).

## Community Hot Topics
Most active issues (by comment count and reactions):

| Issue | Comments | Reactions | Topic |
|-------|----------|-----------|-------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 32 | 1 👍 | Text between tool calls leaks to messaging channels (P1, security) |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | 25 | 2 👍 | Request for prebuilt Android APK releases (P2) |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | 17 | 5 👍 | Control UI requires HTTPS/localhost secure context (regression) |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | 17 | 0 👍 | Tiered bootstrap file loading for progressive context control |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | 17 | 0 👍 | Signal daemon stop() race condition on SIGUSR1 restart |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) | 15 | 1 👍 | Agent replies to previous message instead of current (session confusion) |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 14 | 5 👍 | Bootstrap files in agentDir ignored (only workspace works) |
| [#18160](https://github.com/openclaw/openclaw/issues/18160) | 13 | **11 👍** | Direct exec mode for cron jobs (highly requested) |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | 12 | 2 👍 | `exec` tool doesn’t inherit `skills.entries.*.env` env vars |
| [#20786](https://github.com/openclaw/openclaw/issues/20786) | 8 | **6 👍** | Telegram Business Bot support |

**Underlying needs:** Users are demanding (a) better security around unintended message leaks, (b) more flexibility in bootstrap file management, (c) reliable cron job execution without LLM overhead, (d) smoother onboarding and multi-platform support (Telegram Business, Android APK), and (e) consistent environment variable inheritance for exec.

## Bugs & Stability
Several serious regressions and stability issues surfaced in the last 24 hours:

- **P0 – Memory leak** ([#91588](https://github.com/openclaw/openclaw/issues/91588)): Gateway RSS grows from 350MB to 15.5GB over days, causing repeated OOM crashes. No fix PR yet.
- **P1 – Text leakage** ([#25592](https://github.com/openclaw/openclaw/issues/25592)): Internal processing output leaks to messaging channels. No linked fix PR.
- **P1 – Session context confusion** ([#32296](https://github.com/openclaw/openclaw/issues/32296)): Agent responds to wrong message. No fix PR.
- **P1 – Bootstrap silently ignored** ([#29387](https://github.com/openclaw/openclaw/issues/29387)): Per-agent `agentDir` bootstrap files not loaded. No fix PR.
- **P1 – Exec tool env vars missing** ([#31583](https://github.com/openclaw/openclaw/issues/31583)): Regression in env inheritance. No fix PR.
- **P1 – Signal daemon race condition** ([#22676](https://github.com/openclaw/openclaw/issues/22676)): Orphaned processes on restart. No fix PR.
- **P1 – CLI scope deadlock** ([#74484](https://github.com/openclaw/openclaw/issues/74484)): Cannot approve/reject pairing repair requests. No fix PR.
- **P1 – Memory search broken** ([#91778](https://github.com/openclaw/openclaw/issues/91778), reported in French): Index metadata missing since v2026.6.1. Likely P0 for affected users. No fix PR.
- **P1 – Compaction timeout** ([#92043](https://github.com/openclaw/openclaw/issues/92043)): 180s timeout too short for long sessions, causing loop. No fix PR.
- **P1 – Duplicate messages** ([#88951](https://github.com/openclaw/openclaw/issues/88951)): Responses duplicated 2–4 times after upgrade. No fix PR.
- **P1 – WhatsApp session stalls** ([#84569](https://github.com/openclaw/openclaw/issues/84569)): Long model calls cause stalled turns. No fix PR.
- **P1 – Webchat avatar 404** ([#38439](https://github.com/openclaw/openclaw/issues/38439)): Regression returning 404 for valid avatars. No fix PR.
- **P1 – `null` object error** ([#38327](https://github.com/openclaw/openclaw/issues/38327)): Google Vertex Gemini 3.1 model fails after update. No fix PR.
- **P1 – Heartbeat stuck on pendingFinalDelivery** ([#83184](https://github.com/openclaw/openclaw/issues/83184)): Blocks subsequent heartbeats. No fix PR.

A few regressions have closed PRs today (e.g., #71491 Kimi K2.6 reasoning_content fix was closed), but most P1 issues lack linked fix PRs, indicating the team is resource-constrained.

## Feature Requests & Roadmap Signals
Top community feature requests (by reactions and recency):

- **Direct Exec Mode for Cron Jobs** ([#18160](https://github.com/openclaw/openclaw/issues/18160), 11 👍) – Avoid LLM overhead for simple cron tasks.
- **Telegram Business Bot support** ([#20786](https://github.com/openclaw/openclaw/issues/20786), 6 👍) – Enable business_message/business_connection updates.
- **Denylist for exec-approvals** ([#6615](https://github.com/openclaw/openclaw/issues/6615), 7 👍) – “Allow everything except X” security policies.
- **Slack Block Kit support** ([#12602](https://github.com/openclaw/openclaw/issues/12602), 0 👍 but practical) – Rich interactive messages in Slack.
- **Multi-agent collaboration enhancement** ([#35203](https://github.com/openclaw/openclaw/issues/35203)) – Capability profiling, blackboard, layered memory.
- **Sub-agent completion hook** ([#22358](https://github.com/openclaw/openclaw/issues/22358)) – Post-subagent extension.
- **Pre-response enforcement hooks** ([#13583](https://github.com/openclaw/openclaw/issues/13583)) – Hard gates for mandatory tool calls.
- **AnnounceTarget for sub-agent completion** ([#27445](https://github.com/openclaw/openclaw/issues/27445)) – Route completion to parent session.
- **Memory trust tagging by source** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) – Prevent memory poisoning.
- **Dynamic model discovery** ([#10687](https://github.com/openclaw/openclaw/issues/10687)) – OpenRouter and other fast-moving catalogs.
- **Backup/restore utility** ([#13616](https://github.com/openclaw/openclaw/issues/13616)) – Config, cron jobs, session history.
- **Android APK releases** ([#9443](https://github.com/openclaw/openclaw/issues/9443)) – Prebuilt companion app.

**Prediction for next version:** The current release already shipped major security hardening. The next minor version (2026.6.x) is likely to include fixes for the worst P1 regressions (text leakage, bootstrap ignoring, control UI HTTPS), possibly the sub-agent completion hook (already has linked PRs), and continued improvement of cron and session reliability. Longer-term roadmap items (Telegram Business, dynamic models, memory trust) will probably remain open.

## User Feedback Summary
**Pain points expressed strongly:**
- **Security leaks**: Users are frustrated that agent internal output appears in public channels (#25592).
- **Bootstrap configuration**: Bootstrap files placed in agent directories are silently ignored, breaking expected per-agent behavior (#29387).
- **Environment variable propagation**: Exec tools lack env variables from skills config, causing secret injection failures (#31583).
- **Session context drift**: The agent frequently replies to wrong messages, especially after session resets (#32296, #47975).
- **Memory unreliability**: `memory_search` broken for several weeks (#91778), and CJK text scoring issues (#92341) hurt non-English users.
- **Platform gaps**: No prebuilt Android APK (#9443), missing Telegram Business support (#20786), Slack Block Kit pain (#12602), and WhatsApp stalls (#84569).

**Positive signals:** The community actively tests and reports regressions, suggesting high engagement. Features like the workboard delete tool (#92319) and increased skill description limit (#92427) show responsive improvements.

## Backlog Watch
Several important issues have been open for months without maintainer review or fix PRs:

| Issue | Age | Priority | Topic |
|-------|-----|----------|-------|
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | Since Feb 5 | P2 | Android APK prebuilt releases |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Since Feb 3 | P2 | Memory trust tagging by source |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | Since Feb 1 | P2 | Exec-approvals denylist |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | Since Feb 9 | P2 | Slack Block Kit support |
| [#14785](https://github.com/openclaw/openclaw/issues/14785) | Since Feb 12 | P2 | Reduce tool schema token overhead |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | Since Feb 6 | P2 | Dynamic model discovery |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) | Since Feb 10 | P2 | Backup/restore utility |
| [#13610](https://github.com/openclaw/openclaw/issues/13610) | Since Feb 10 | P3 | Secrets management integration |
| [#33329](https://github.com/openclaw/openclaw/issues/33329) | Since Mar 3 | P3 | Implicit discovery toggles |

These issues carry the `clawsweeper:no-new-fix-pr` and often `clawsweeper:needs-maintainer-review` labels, indicating they are in limbo. Some have linked PRs open but stalled (e.g., #22438, #20786). The high volume of new P1 reports (especially the P0 memory leak #91588) may further delay these older enhancements.

---

*Generated on 2026-06-13 from OpenClaw GitHub activity data.*

---

## Cross-Ecosystem Comparison

好的，这是基于您提供的社区摘要生成的跨项目对比分析报告。

---

### 跨项目生态系统对比报告: 个人AI代理/助手开源版图

**日期:** 2026-06-13
**分析师:** AI Agent与个人AI助手开源生态系统高级分析师

---

### 1. 生态系统概述

当前个人AI代理与助手开源生态正经历**高强度的并行开发与迭代**。核心项目（如OpenClaw）虽保持巨大体量，但面临着**维护积压与稳定性挑战**并存的局面。与此同时，以IronClaw、ZeroClaw和Hermes Agent为代表的新兴或快速迭代项目，正通过**架构重构（如引擎整合）** 和**领域特定优化（如桌面UI、企业级沙箱）** 来开拓生存空间。社区需求高度集中于**执行可靠性、内存管理、安全沙箱和跨平台体验**，表明市场正从“基础功能可用”向“稳定性与安全性”过渡。尽管有部分项目（如TinyClaw, ZeptoClaw）表现平静，但整体生态系统呈现**蓬勃且竞争激烈**的态势。

### 2. 活动对比

下表展示了各项目在过去24小时内的活动关键指标和健康度评估。**健康度**基于综合评估，考虑因素包括：活动密集程度、bug修复速度、关键问题响应情况、代码合并速度及社区反馈质量。

| 项目 | 更新Issues数 | 更新PRs数 | 发布状态 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 484 | **已发布** (`v2026.6.6`) | ⚠️ **中等** (高积压、多P0/P1未修复) |
| **NanoBot** | 6 | 29 | 无新发布 | ✅ **良好** (积极合并，核心内存问题待解) |
| **Hermes Agent** | 50 | 50 | 无新发布 | ✅ **良好** (活跃修复，长输出bug已解决) |
| **PicoClaw** | 6 | 14 | **已发布** (`nightly`) | ✅ **良好** (快速迭代，社区贡献活跃) |
| **NanoClaw** | 5 | 18 | 无新发布 | ✅ **良好** (合并爆发，安全性关注度高) |
| **NullClaw** | 1 | 3 | 无新发布 | 🟡 **稳定** (活动量低，聚焦小范围修复) |
| **IronClaw** | 50 | 50 | 无新发布 | ✅ **优秀** (高产出，专注Reborn V2) |
| **LobsterAI** | 1 | 17 | **待发布** (`release/2026.6.11`) | ✅ **优秀** (合并爆发，大版本发布前兆) |
| **CoPaw** | 21 | 24 | **待发布** (`v1.1.12b1`) | ✅ **良好** (修复积极，但有致命回归bug) |
| **Moltis** | 3 | 0 | 无新发布 | 🟡 **稳定** (社区讨论活跃，但代码合并停滞) |
| **ZeroClaw** | 13 | 32 | 无新发布 | ⚠️ **中等** (引擎重构重大，但S1阻塞bug频发) |
| **TinyClaw / ZeptoClaw** | 0 | 0 | 无新发布 | ✅ **休眠** (24小时内无活动) |

### 3. OpenClaw 的定位

- **优势:**
    - **社区规模无人能及:** 500+ issues和PRs的更新量是其他项目的5-10倍，生态讨论和问题反馈最丰富。
    - **成熟与安全:** 作为核心参考实现和最新发布的 `v2026.6.6`，其安全边界强化（沙箱、MCP、代码执行等）是所有项目中最系统和最前沿的。
    - **功能广度:** 集成了几乎所有主流平台（Discord, Telegram, Slack, WhatsApp等）和功能（如cron jobs, skills工具）。
- **劣势:**
    - **严重的维护积压:** 409个未解决的issues和344个未合并PRs构成巨大技术债务，许多P0/P1级别的bug（如内存泄漏、文本泄露）缺乏修复PR。
    - **资源约束:** 热门功能请求（如Telegram Business Bot）长期未被处理，社区对安全泄露、配置问题的反馈强烈。这暗示核心团队可能在“灭火”而非“开发”。
- **技术差异:**
    - 相比之下，OpenClaw更像一个“大而全”的操作系统，而其他项目（如NanoBot, ZeroClaw）则在特定架构（模块化、引擎整合）上更灵活。
- **结论:** OpenClaw是**社区领导者**和**安全标杆**，但正在为其巨大的体量付出**稳定性和维护速度**的代价。其未来健康度取决于能否有效清理积压。

### 4. 共享技术重点领域

以下需求在多个项目中反复出现，代表了社区核心关切：

| 需求 | 相关项目 | 具体表现 |
| :--- | :--- | :--- |
| **内存与上下文管理** | **OpenClaw**, **NanoBot**, **Hermes Agent** | 智能体“健忘”（NanoBot #4044）、上下文上下文窗口压力、内存泄露（OpenClaw P0）、记忆搜索功能损坏（OpenClaw） |
| **安全与沙箱强化** | **OpenClaw**, **NanoClaw**, **ZeroClaw**, **IronClaw**, **Moltis** | 代码沙箱泄露（OpenClaw #25592）、容器安全能力降级（NanoClaw PR #2748）、MCP授权问题（Moltis #1115）。企业级沙箱需求（Moltis #1118） |
| **平台兼容性与集成** | **OpenClaw**, **Hermes Agent**, **NanoClaw**, **PicoClaw**, **ZeroClaw** | Windows/macOS安装与运行问题（ZeroClaw S1 bugs）、Telegram Business支持（OpenClaw）、Discord/Weixin断连（Hermes Agent）、Android APK需求（OpenClaw） |
| **执行可靠性与可观测性**| **OpenClaw**, **NanoBot**, **ZeroClaw** | Cron任务不触发（CoPaw）、工具调用超时与失败（NanoClaw #2668）、`ask_user`工具失效（ZeroClaw）、审计日志（NanoBot） |
| **环境变量与配置传递**| **OpenClaw** | `exec`工具不继承技能配置的环境变量（#31583）、Bootstrap文件被忽略（#29387） |

### 5. 差异化分析

| 项目 | 核心聚焦点 | 目标用户 | 架构特点 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用型安全代理、庞大生态系统、全面平台集成 | 高级用户、开发者、社区 | 大而全的参考设计，功能最全面 |
| **Hermes Agent** | **桌面优先**体验、GUI性能、Clipboard集成 | macOS用户、桌面重度用户 | 深度优化桌面交互 (GUI帧率、Clipboard、文件树) |
| **IronClaw** | **Reborn (V2) 引擎**、企业级安全审计、架构重构 | 追求前沿架构的开发者 | 模块化、可观测性内建、专注于重构和可测试性 |
| **ZeroClaw** | **代理进程运行时**、**turn引擎统一**、插件系统 | 底层开发者、插件生态贡献者 | 专注于运行时架构，通过统一引擎解决行为不一致问题 |
| **CoPaw** | **AgentScope生态系统**、中文社区、多模态交互 | 中文社区用户、需要多模态支持的开发者 | 与AgentScope框架深度绑定；强中文平台集成（微信、飞书） |
| **LobsterAI** | **Computer Use (计算机使用)**、**语音交互(ASR)**、**制品分享** | 追求自动化和协作的工作流用户 | 强产品导向，专注于模拟用户操作、语音实时输入和结果分享 |
| **NanoBot** | **轻盈小巧**、**模块化**、高集成度 (TTS, WebUI) | 喜欢简洁、快速部署的个人开发者 | 小而精的设计，社区贡献活跃，开发伦理规则内建 |
| **PicoClaw**| **轻量级参考实现** (Go语言)、**渠道解耦** | 对特定技术栈有偏好的开发者 | 技术栈简洁，快速实验新思路，如前文提及的NEAR AI Cloud Provider |

### 6. 社区动力与成熟度

- **第一梯队 (高速迭代与创新):**
    - **IronClaw, LobsterAI, ZeroClaw** 处于最高速开发状态。它们正在进行重大架构重构（IronClaw Reborn V2, ZeroClaw Turn Engine）或发布前沿特性（LobsterAI Computer Use）。这些项目具有最高的风险/回报比。
- **第二梯队 (高活动度与维护):**
    - **OpenClaw, Hermes Agent** 保持着极高的活动量，但主要驱动力来自于“维护”和“修复”，而非全新的架构变化。它们有大量积压问题，但同时也有最广泛的用户基础和最成熟的特性集。
- **第三梯队 (稳健增长):**
    - **NanoBot, PicoClaw, NanoClaw, CoPaw** 项目健康状况良好，正在稳步推进特性优化和bug修复。它们在特定领域（如NanoBot的可观测性、NanoClaw的安全性）有明确的进展。
- **第四梯队 (稳定/休眠):**
    - **Moltis, NullClaw** 活动量较低，社区讨论多于代码贡献，处于稳定进化或维护模式。**TinyClaw, ZeptoClaw** 24小时内无更新，可能处于休眠或研究阶段。

### 7. 趋势信号

以下是来自社区反馈的、对AI代理开发者有价值的行业趋势：

- **执行环境代理正从“对话接口”转向“系统管理层”：** 代理不再仅仅是聊天机器人。它们需要执行Cron任务、管理文件、操作桌面（Computer Use）、并与其他代理组队。这要求开发者将代理视为**轻量级的操作系统进程**，需要关注资源、安全和生命周期管理。
- **对上下文窗口和记忆可靠性的信任正在动摇：** “智能体健忘”是跨项目的最大共同痛点。社区不再满足于简单地增加上下文窗口大小，而是要求**更智能、更可预测的记忆管理**（如标签化、可配置的持久化、防毒化机制）。这表明下一代代理的核心竞争力将在于其记忆系统的可靠性。
- **多模态交互进入“务实落地”阶段：** 请求从“支持多模态”转向了具体的、低延迟的场景，如**实时语音输入（ASR）**、**屏幕操作（Computer Use）** 和**制品分享**。开发者需要关注这些具体场景的**性能和可靠性**，而不仅仅是模型能力。
- **企业级/生产级部署需求普遍化：** 即使是个人项目也开始关注**沙箱隔离**、**审计日志**、**细粒度权限控制（如allow/denylist）** 和**备份恢复**。这表明个人代理正在被用于更有价值的工作流，而不再仅仅是实验。
- **平台粘性来自“一致性”而非“数量”：** 用户不再满足于能连接多个平台，而是要求**跨平台体验的一致性（如同步会话历史Hermes Agent #45275）** 和**在单一平台上的可靠交互（如Telegram Forum线程回复PicoClaw #3110）**。深度整合和可靠行为比广度更关键。
- **工具编排能力是下一竞争高地：** 来自OpenClaw、CoPaw和ZeroClaw的需求表明，用户需要**更灵活的工具调用控制**（如preresponse hooks、sub-agent hooks, ACP/A2A抽象）和**更好的错误处理**（如工具超时、重试逻辑）。代理的“智能”将在很大程度上取决于其**编排和链式调用工具**的健壮性。

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-13

**Generated from** [HKUDS/nanobot](https://github.com/HKUDS/nanobot) — 24h data snapshot (2026-06-12 → 2026-06-13)

---

## 1. Today's Overview

NanoBot remains in a **high-activity phase**: 29 pull requests were updated in the last 24 hours (9 merged/closed, 20 open), and 6 issues were touched (3 closed, 3 still open). The project is shipping multiple feature PRs (audit infrastructure, WebUI/config parity, multi-provider TTS) while simultaneously addressing several memory‑management bugs and runtime stability issues. No new releases were cut today, but the volume of integrated PRs signals a possible release window soon. Community involvement is solid, with some issues attracting moderate discussion and one long‑standing memory‑loss bug (#4044) still unresolved.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Project Progress

**Merged / Closed PRs (9 total; notable examples below):**

| PR | Title | Status | Significance |
|----|-------|--------|-------------|
| [#4319](https://github.com/HKUDS/nanobot/pull/4319) | feat(audit): Add tools.audit for agent action observability | **closed** | Adds configurable audit tracking (loguru, webhook, JSONL, callback) for agent tool calls. Integrated into AgentLoop and AgentRunSpec. |
| [#4318](https://github.com/HKUDS/nanobot/pull/4318) | feat(audit): Add tools.audit for agent action observability | **closed** | Duplicate effort? Both closed; likely earlier iteration superseded by #4319. |
| [#4304](https://github.com/HKUDS/nanobot/pull/4304) | fix(cron): wait for spawned subagents before marking cron job complete | **closed** | Fixes a race where cron jobs that spawn subagents were marked done prematurely, causing background tasks to run untracked. |

**Key advances reflected across open/merged PRs:**
- **Memory & context robustness:** multiple PRs handle malformed history entries (#4315), monotonic cursor (#4256), and symlink escape prevention (#4119).
- **New feature surface:** TTS system (#4316), WebUI settings parity (#4313), audit framework (#4320), SDK runtime controls (#4296).
- **Tool hardening:** media attachment validation (#4312), file pagination limits (#4311), read‑only root enforcement (#4053).
- **Testing infrastructure:** scripted agent runner harness (#3982) and memory lifecycle harness (#4193) – though still open.

---

## 4. Community Hot Topics

The most active discussions (by comment count) over the last 24h:

| Issue/PR | Comments | Topic & Analysis |
|----------|----------|------------------|
| [#4044](https://github.com/HKUDS/nanobot/issues/4044) [OPEN] | 5 | **“Short term memory loss”** – Agent forgets the immediate question it just asked. User suspects context window pressure from system prompts (SOUL.md, USER.md, MEMORY.md). **Underlying need:** Reliable conversational continuity; the project’s memory subsystem is being stress‑tested. |
| [#4203](https://github.com/HKUDS/nanobot/issues/4203) [CLOSED] | 3 | **`find_legal_message_start` discards all messages** when an orphaned tool result follows a user message. **Impact:** Session history pile‑up, API rejection from strict providers. Fixed via PR (closed today). |
| [#4006](https://github.com/HKUDS/nanobot/issues/4006) [CLOSED] | 2 | **Orphaned tool results** persist even after PR #3984. Causes API schema violations and renderers to crash. Also closed today – likely related to #4203 fix. |
| [#4307](https://github.com/HKUDS/nanobot/issues/4307) [OPEN] | 1 | **Post‑turn consolidation wipes agent’s own delivery message** – user follow‑ups lose context. A moderate‑sized `context_window_tokens` (40k) triggers the bug after long multi‑iteration turns. |

**Analysis:** Memory and history handling dominate user pain points this cycle. The community is actively testing edge cases around context window limits, orphaned tool results, and consolidation behavior. The closed issues (#4203, #4006) show maintainers are responsive, but the open #4044 and #4307 indicate the core memory manager still has gaps.

---

## 5. Bugs & Stability

Bugs newly reported or updated today, ranked by severity:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| 🟥 Critical | [#4307](https://github.com/HKUDS/nanobot/issues/4307) | Post‑turn consolidation discards the assistant’s own final message, making user follow‑up references impossible. Likely to cause data loss in long conversations. | None yet |
| 🟥 Critical | [#4044](https://github.com/HKUDS/nanobot/issues/4044) | Short‑term memory loss – agent cannot remember its own previous turn. Affects all interactive sessions. Open since May 28 with 5 comments but no fix PR. | None |
| 🟧 High | [#4044](https://github.com/HKUDS/nanobot/issues/4309) | `/v1/chat/completions` endpoint always returns zero usage tokens. While not a functional crash, it breaks API consumers that rely on usage tracking. | None |
| 🟨 Medium | [#4203](https://github.com/HKUDS/nanobot/issues/4203) (closed) | `find_legal_message_start` drops all messages under specific orphaned‑tool‑result conditions. **Fixed today** (see PR #? – likely linked fix merged). | ✅ Closed |
| 🟨 Medium | [#4006](https://github.com/HKUDS/nanobot/issues/4006) (closed) | Orphaned tool results cause API schema rejections. **Fixed today** (possibly by same underlying PR). | ✅ Closed |

Additionally, an open fix PR addresses a **MCP server crash** during reconnection ([#4303](https://github.com/HKUDS/nanobot/pull/4303)) — `RuntimeError: Attempted to exit cancel scope in a different task` – which is an async lifecycle bug.

---

## 6. Feature Requests & Roadmap Signals

Notable user‑requested capabilities from today’s data:

| Feature | Issue/PR | Likelihood for Next Version |
|---------|----------|-----------------------------|
| **Multiple custom providers** | [#4305](https://github.com/HKUDS/nanobot/issues/4305) [CLOSED] | ⬆️ High – the issue was closed quickly, possibly as a duplicate or because a solution is already in progress. The proposed “template” parameter is clean. |
| **Multi‑provider TTS** | [#4316](https://github.com/HKUDS/nanobot/pull/4316) | ✅ Already implemented as an open PR; expected to land soon. |
| **WebUI/config.json parity** | [#4313](https://github.com/HKUDS/nanobot/pull/4313) | ✅ Open PR; likely to be merged. |
| **WhatApp mentions** | [#4317](https://github.com/HKUDS/nanobot/pull/4317) | 🟡 Open PR; low complexity, but depends on maintainer review. |
| **SDK runtime controls** | [#4296](https://github.com/HKUDS/nanobot/pull/4296) | 🟡 Large PR with backward compatibility; may take more review cycles. |

**Roadmap signals:** The push toward **agent action observability** (audit #4320) and **configuration parity** suggests the maintainers are focusing on production‑grade operational tooling. The multiple memory‑related PRs indicate a concerted effort to stabilise the context‑window management.

---

## 7. User Feedback Summary

- **Pain points:** Memory loss (#4044, #4307) is the dominant frustration. Users report that even simple Q&A turns lose context, making the agent seem unreliable. Workarounds involve manually managing `context_window_tokens`.
- **Tool‑call reliability:** Several users hit orphaned‑tool‑result bugs that broke API compatibility (OpenAI/Anthropic). The fixes for #4203 and #4006 should alleviate this.
- **API completeness:** One user (#4309) noted that the built‑in OpenAI‑compatible server returns zero usage tokens, which is a minor but annoying gap for anyone monitoring costs.
- **Configuration flexibility:** Request for multiple custom providers (#4305) indicates power users want to mix and match backends without code changes.
- **Overall satisfaction:** The community is **highly engaged** (29 PRs updated in 24h) and maintainers are actively merging fixes. However, the persistence of critical memory bugs (#4044) may erode confidence if not addressed soon.

---

## 8. Backlog Watch

Long‑standing/open items that may require maintainer attention:

| Item | Age (since creation) | Notes |
|------|---------------------|-------|
| [#4044](https://github.com/HKUDS/nanobot/issues/4044) [OPEN] | 16 days (May 28) | Short‑term memory loss – 5 comments, no fix PR. Critical impact. |
| [#3983](https://github.com/HKUDS/nanobot/pull/3983) [OPEN] | 20 days (May 24) | Test coverage for blocked tool‑call finish reasons. Unmerged – could be stuck on review. |
| [#3982](https://github.com/HKUDS/nanobot/pull/3982) [OPEN] | 20 days (May 24) | Scripted agent runner harness. Unmerged – important for testing reliability. |
| [#4053](https://github.com/HKUDS/nanobot/pull/4053) [OPEN] | 15 days (May 29) | Keep read‑only roots out of write paths – security hardening. Unmerged. |
| [#4119](https://github.com/HKUDS/nanobot/pull/4119) [OPEN] | 13 days (May 31) | Block relative symlink escapes – security fix. Unmerged. |
| [#4193](https://github.com/HKUDS/nanobot/pull/4193) [OPEN] | 9 days (Jun 4) | Memory lifecycle test harness – important for validating the consolidation logic that users complain about. |
| [#4256](https://github.com/HKUDS/nanobot/pull/4256) [OPEN] | 5 days (Jun 8) | Keep history cursor monotonic – directly related to memory corruption issues. |

**Observations:** Several **test‑infrastructure PRs** and **security fixes** have been open for weeks without merging. The memory‑related PRs (#4256, #4193) are particularly notable given the active bug reports (#4044, #4307). Merging these could move the needle on stability. The lack of activity on #4044 (no assigned fix) is concerning for a critical bug.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-13

## Today's Overview

The project remained highly active with **50 issues** and **50 pull requests** updated in the last 24 hours. Activity was balanced: 6 issues closed, 5 PRs merged/closed, and 44 open issues and 45 open PRs continue to be worked on. No new releases were cut today, but the volume of fixes—especially around gateway reliability, desktop UI performance, and provider compatibility—shows a sustained development pace. Community engagement remains robust, with several long-standing bugs finally resolved and critical regressions addressed.

---

## Releases

None today.

---

## Project Progress

Five pull requests were merged or closed today. Key advances include:

- **🖥️ Desktop GUI performance** — [#45343](https://github.com/NousResearch/hermes-agent/pull/45343) (merged) cut GUI streaming and interaction lag with six targeted fixes, improving frame rate from 28–38 fps to 56 fps and reducing blocked time from 5.2 s to near zero.
- **🗂️ Clipboard improvements** — [#41757](https://github.com/NousResearch/hermes-agent/pull/41757) (merged) added `set_clipboard_text()` and PyObjC acceleration for picture paste, reducing flicker and subprocess overhead.
- **🗓️ Cron job visibility** — [#44087](https://github.com/NousResearch/hermes-agent/pull/44087) (open but updated) fixes `no_agent: true` cron runs not appearing in the Desktop GUI.
- **🗂️ File tree toggle** — [#45355](https://github.com/NousResearch/hermes-agent/pull/45355) (new) adds a show/hide ignored files toggle to the desktop file tree.
- **💬 Weixin disconnect drain** — [#45353](https://github.com/NousResearch/hermes-agent/pull/45353) (new) prevents message loss during Weixin gateway disconnects.

Three critical bug fixes were also merged (see Bugs & Stability section).

---

## Community Hot Topics

The most engaged issue remains the **output length limit bug** [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) (41 comments, 5 👍), which was closed today. It affected CLI chat and gateway messaging when generating long responses. The community’s deep involvement suggests high reliance on Hermes for extensive, multi-step conversations.

Other active discussions:

- **Deepseek provider custom endpoint issues** [#17199](https://github.com/NousResearch/hermes-agent/issues/17199) (4 comments) — users hitting aggressive model name normalization and base_url overrides that break custom endpoints like Volcengine ARK.
- **MiniMax-M3 nested array collapse** [#44976](https://github.com/NousResearch/hermes-agent/issues/44976) (3 comments) — a subtle MCP tool-args bug affecting structured tool calls.
- **Desktop auto-scroll & sidebar overlap** [#44140](https://github.com/NousResearch/hermes-agent/issues/44140) (2 comments, 2 👍) — user-driven feature request that garnered quick upvotes, signalling strong demand for desktop UX polish.

Underlying needs: users want **reliable long-form responses** (now fixed), **flexible provider configuration** (unresolved for custom endpoints), and **smoother desktop interaction** (being addressed).

---

## Bugs & Stability

The following bugs were reported today (sorted by severity):

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#45323](https://github.com/NousResearch/hermes-agent/issues/45323) | P2 | Telegram rich tables rewritten into bullets by shared formatter | No |
| [#45250](https://github.com/NousResearch/hermes-agent/issues/45250) | P2 | Anthropic OAuth login (CLI command) fails with 404 — stale token endpoint | No |
| [#45258](https://github.com/NousResearch/hermes-agent/issues/45258) | P2 | Gateway per-profile log/run creates root-owned parent dir → s6-log fatal loop | [#45346](https://github.com/NousResearch/hermes-agent/pull/45346) |
| [#45279](https://github.com/NousResearch/hermes-agent/issues/45279) | P2 | PR #38889 still creates Node/npm shims in ~/.local/bin, shadowing Homebrew | No |
| [#44763](https://github.com/NousResearch/hermes-agent/issues/44763) | P2 | macOS computer_use: AX/SOM element bounds always zero, breaking spatial grounding | [#45329](https://github.com/NousResearch/hermes-agent/pull/45329) |
| [#44866](https://github.com/NousResearch/hermes-agent/issues/44866) | P2 | MCP OAuth polls 30s on probe failure instead of returning immediately | No |
| [#45264](https://github.com/NousResearch/hermes-agent/issues/45264) | P3 | macOS full-screen moves sidebar and swap buttons | No |
| [#45303](https://github.com/NousResearch/hermes-agent/issues/45303) | P3 | `monitor` and `session_search` auxiliary models missing from `hermes model` picker | No |
| [#45295](https://github.com/NousResearch/hermes-agent/issues/45295) | P3 | Telegram docs don’t mention user-created DM topic read-state limitation | No |
| [#45307](https://github.com/NousResearch/hermes-agent/issues/45307) | P3 | `_find_skill()` does not resolve category/skill path format | No |
| [#45226](https://github.com/NousResearch/hermes-agent/issues/45226) | P3 | Windows desktop crashes with GPU process exit code | No |
| [#45308](https://github.com/NousResearch/hermes-agent/issues/45308) | P2 | BlueBubbles webhook URL normalizing 127.0.0.1 → localhost breaks IPv4 delivery | No |
| [#45328](https://github.com/NousResearch/hermes-agent/issues/45328) | - | auxiliary_client cache eviction calls async close without awaiting | No |

Additionally, earlier P1/P2 issues were **closed** today:

- [#38389](https://github.com/NousResearch/hermes-agent/issues/38389), [#38391](https://github.com/NousResearch/hermes-agent/issues/38391), [#38392](https://github.com/NousResearch/hermes-agent/issues/38392) — Context compression summaries injected as regular assistant messages (all closed).
- [#44837](https://github.com/NousResearch/hermes-agent/issues/44837) — Session DB flush drops assistant after repair_message_sequence merge (closed).
- [#45242](https://github.com/NousResearch/hermes-agent/issues/45242) — `auxiliary_client.py` unhandled `oauth_minimax` auth_type (closed as duplicate).

---

## Feature Requests & Roadmap Signals

User requests logged today include:

- **Unified session history across Desktop and Telegram** [#45275](https://github.com/NousResearch/hermes-agent/issues/45275) (P3) — a +1 to cross-platform session portability.
- **Kanban board integration into Desktop app** [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) (P3, 1 👍) — users want a unified workspace.
- **Desktop GUI auto-scroll, sidebar overlap fix, custom session groups** [#44140](https://github.com/NousResearch/hermes-agent/issues/44140) — already actively discussed.
- **./** [45286](https://github.com/NousResearch/hermes-agent/issues/45286) — show/hide ignored files in file tree (already fixed by [#45355](https://github.com/NousResearch/hermes-agent/pull/45355)).

Prediction for next release: The desktop UX improvements (auto-scroll, file tree toggle, French locale [#45348](https://github.com/NousResearch/hermes-agent/pull/45348)) and the cron `--profile` flag [#45350](https://github.com/NousResearch/hermes-agent/pull/45350) are likely to land soon. The **Anthropic OAuth fix** and **MCP OAuth timeout** are also strong candidates given P2 severity.

---

## User Feedback Summary

Real pain points expressed by users today:

- **Windows desktop instability** — [#45226](https://github.com/NousResearch/hermes-agent/issues/45226) reports repeated crashes (GPU process exit). The user shared trace logs.
- **Missing auxiliary models in CLI configuration** — [#45303](https://github.com/NousResearch/hermes-agent/issues/45303) shows users who rely on `monitor` and `session_search` tasks cannot configure them via the interactive menu.
- **Apple silicon user frustration** — [#45279](https://github.com/NousResearch/hermes-agent/issues/45279) reports that Node/npm shims still shadow Homebrew/nvm despite a claimed fix, causing PATH confusion.
- **Cross-platform session isolation** — [#45275](https://github.com/NousResearch/hermes-agent/issues/45275) highlights a desire for a unified session list, suggesting current per-platform silos are a daily friction.
- **Slack bot-to-bot silent drops** — [#30091](https://github.com/NousResearch/hermes-agent/issues/30091) (open since May 21) is a persistent complaint from multi-agent workspace users.

Satisfaction indicators: Several long-standing annoyances (output truncation, compression pollution, session DB drops) were fixed today, which should improve trust.

---

## Backlog Watch

The following issues/PRs have been open for an extended period without recent maintainer attention and may need prioritisation:

- **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237)** — Response truncated error (closed today after 2 months, but the fix should be verified for regressions).
- **[#17199](https://github.com/NousResearch/hermes-agent/issues/17199)** — Deepseek provider custom endpoint breakage (open since April 29, 4 comments). A popular provider with a clear bug.
- **[#30091](https://github.com/NousResearch/hermes-agent/issues/30091)** — Slack bot-to-bot messages silently dropped (open since May 21). Affects multi-agent workflows.
- **[#16769](https://github.com/NousResearch/hermes-agent/pull/16769)** — Nostr NIP-17 gateway adapter (open since April 28). No recent activity; may be blocked on design decisions.
- **[#36286](https://github.com/NousResearch/hermes-agent/pull/36286)** — MiniMax CN OAuth provider (open since June 1). China-region users are likely waiting.
- **[#43277](https://github.com/NousResearch/hermes-agent/pull/43277)** — Fix auth cooldown exhaustion in OpenAI codex pool (open since June 10). Affects users with rate-limited accounts.

Maintainers should prioritise [#17199](https://github.com/NousResearch/hermes-agent/issues/17199) and [#30091](https://github.com/NousResearch/hermes-agent/issues/30091) as they block multi-provider and multi-agent adopters.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-13

## 1. Today’s Overview
The PicoClaw project saw **high activity** on June 13, 2026, with 14 pull requests and 6 issues updated in the last 24 hours. A **nightly build** (`v0.2.9-nightly.20260613.c362114c`) was automatically released from `main`. The community is actively contributing fixes and features: three PRs were merged, including a major refactor of channel identification, while two new bugs were reported involving Gemini 3.5 Flash compatibility and Telegram Forum replies. Overall, the project is in a **healthy, fast-moving development cycle** with strong contributor engagement.

## 2. Releases
- **`nightly` (v0.2.9-nightly.20260613.c362114c)** — Automated nightly build. Unstable; use with caution.  
  [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  No breaking changes or migration notes are provided for this build.

## 3. Project Progress (Merged/Closed PRs Today)
Three pull requests were merged or closed in the last 24 hours:

- **#2551 — refactor: standardize channel identification** (merged)  
  Decouples channel names from provider types, enabling multiple instances of the same provider. This refactor improves routing across the message bus and agent dispatch logic.  
  [PR #2551](https://github.com/sipeed/picoclaw/pull/2551)

- **#3113 — fix(channels): check JSON marshal/unmarshal errors in toChannelHashes** (merged)  
  Silently discarded serialization errors are now properly handled, preventing silent data loss in channel configuration hashing.  
  [PR #3113](https://github.com/sipeed/picoclaw/pull/3113)

- **#3112 — fix(tools): handle json.Marshal error in tool loop call arguments** (merged)  
  Fixes a bug where marshaling failures in tool call arguments could silently erase conversation history.  
  [PR #3112](https://github.com/sipeed/picoclaw/pull/3112)

Additionally, **Issue #3109** (feat: channel-level permission scoping) was closed, suggesting the feature has been implemented or superseded.  
[Issue #3109](https://github.com/sipeed/picoclaw/issues/3109)

## 4. Community Hot Topics
The most active discussions (by comments and reactions) revolve around **protocol completeness** and **token consumption**:

- **#2984 — Add explicit turn completion signal for Pico WebSocket clients**  
  2 comments, 2 👍. Users need a deterministic `turn.done` signal to know when the agent finishes processing a message. The PR #3116 (open) addresses this gap.  
  [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)

- **#3012 — Continuous consumption of tokens every minute when evolution is enabled**  
  2 comments, 0 👍. A bug report from a FreeBSD user reports that enabling “Evolution” causes token drain every minute. No fix PR has appeared yet.  
  [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

- **#3109 — Feat: Channel-level permission scoping (closed)**  
  1 comment, 0 👍. The idea of restricting dangerous operations in group/channel chats was well-received and appears to have been resolved (likely via code changes not listed here).  
  [Issue #3109](https://github.com/sipeed/picoclaw/issues/3109)

## 5. Bugs & Stability
Two new bugs were reported today, plus one older open bug remains critical:

| Severity | Issue | Description | Fix PR Available? |
|----------|-------|-------------|-------------------|
| **High** | [#3111](https://github.com/sipeed/picoclaw/issues/3111) | Tool execution fails with Gemini 3.5 Flash due to `Missing thought_signature in schema` (400 error from Google API). | No |
| **High** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | Continuous token consumption every minute with Evolution enabled (v0.2.9, FreeBSD). | No (stale) |
| **Medium** | [#3110](https://github.com/sipeed/picoclaw/issues/3110) | Telegram adapter ignores `message_thread_id` in Forum topics; replies default to `#General`. | No |

A related fix for **issue #3108** (media turns not routed to image models) is now under review in **[PR #3117](https://github.com/sipeed/picoclaw/pull/3117)**.

## 6. Feature Requests & Roadmap Signals
Several feature requests and contributions signal the direction of upcoming releases:

- **Turn completion signal** — [#2984](https://github.com/sipeed/picoclaw/issues/2984) (likely to land soon via PR #3116)
- **Channel-level permission scoping** — [#3109](https://github.com/sipeed/picoclaw/issues/3109) (closed, likely in `main`)
- **Telegram private/group/channel permission tiers** — [#3114](https://github.com/sipeed/picoclaw/issues/3114) (future request)
- **DeltaChat gateway** — [PR #3063](https://github.com/sipeed/picoclaw/pull/3063) (open, new channel integration)
- **NEAR AI Cloud provider** — [PR #2917](https://github.com/sipeed/picoclaw/pull/2917) (stale, but valuable for TEE-capable models)
- **Image input compression** — [PR #2964](https://github.com/sipeed/picoclaw/pull/2964) (stale, reduces bandwidth for vision pipeline)
- **Shift+Enter hint in Web chat composer** — [PR #3097](https://github.com/sipeed/picoclaw/pull/3097) (open, UX improvement)
- **Remote Pico WebSocket mode for agents** — [PR #3118](https://github.com/sipeed/picoclaw/pull/3118) (open, enables `picoclaw agent --remote`)

Likely candidates for the **next stable release**: turn completion signal, permission scoping, and the DeltaChat gateway if reviews proceed.

## 7. User Feedback Summary
User feedback highlights both pain points and desired capabilities:

- **Pain points**:  
  - Token waste from Evolution mode (`#3012`) — impacts cost-sensitive deployments.  
  - Incompatibility with Gemini 3.5 Flash (`#3111`) — blocks adoption of newer, cheaper models.  
  - Telegram Forum reply misrouting (`#3110`) — hurts usability in community groups.  
  - Missing `turn.done` signal (`#2984`) — complicates client-side state management for WebSocket integrations.

- **Desired capabilities**:  
  - Fine-grained permission scoping by chat type (`#3109`, `#3114`) — critical for safety in multi-user environments.  
  - Additional channel backends (DeltaChat, NEAR AI) — expand deployment flexibility.  
  - Improved image handling (compression `#2964`, media routing `#3117`) — optimise cost and reliability.

No explicit satisfaction or praise was captured in today’s data, but the volume of contributed fixes and features indicates a **responsive and engaged maintainer/contributor community**.

## 8. Backlog Watch
The following items have remained unresolved for an extended period and may require maintainer attention:

| Item | Age | Description | Impact |
|------|-----|-------------|--------|
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) | 8 days | Continuous token consumption with Evolution enabled | High – cost & resource waste |
| [#3045](https://github.com/sipeed/picoclaw/pull/3045) | 6 days | Matrix user ID `allow_from` fallthrough fix (PR open) | Medium – authentication bypass risk |
| [#3053](https://github.com/sipeed/picoclaw/pull/3053) | 5 days | Evolution store type assertion panic fix (PR open) | High – potential crashes |
| [#2964](https://github.com/sipeed/picoclaw/pull/2964) | 16 days | Image input compression (PR stale) | Medium – bandwidth savings |
| [#2917](https://github.com/sipeed/picoclaw/pull/2917) | 23 days | NEAR AI Cloud provider (PR stale) | Low – new feature, not critical |
| [#3091](https://github.com/sipeed/picoclaw/pull/3091) | 3 days | OpenAI compat native search type assertion (PR open) | Medium – silent disable of search |

These items should be prioritised in the next review cycle to prevent technical debt and user frustration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-13

## Today's Overview
NanoClaw saw a **burst of merge activity** with 10 PRs closed today alongside 8 new open PRs, indicating a maintainer push to clear a backlog of feature and fix branches. The issue tracker is moderately active with 5 updated items (4 open, 1 closed). No new release was cut, but the volume of merged work—spanning Signal integration, backup/restore, agent routing, and error resilience—suggests a significant internal milestone may be approaching. The community is contributing notably, with first-time and repeat contributors submitting security-hardening and reliability fixes.

---

## Releases
None.

---

## Project Progress

### Merged/Closed PRs (10 total)

**Signal Channel Enhancements**
- [#2203 feat(signal): inbound + outbound reaction support](https://github.com/nanocoai/nanoclaw/pull/2203) — Agents can now add/read reactions on Signal messages, mirroring the chat-sdk-bridge pattern.
- [#2071 feat(signal): route every non-audio attachment through the inbox path](https://github.com/nanocoai/nanoclaw/pull/2071) — All file types (PDFs, archives, images) are now persisted to `/workspace/inbox/<msgId>/` for agent consumption.
- [#2040 feat(signal): support outbound attachments](https://github.com/nanocoai/nanoclaw/pull/2040) — signal-cli's existing attachment support is now wired into the adapter; outbound files are no longer silently dropped.

**Ollama Multimodal Support**
- [#2072 feat(ollama): images field for multimodal models via inbox paths](https://github.com/nanocoai/nanoclaw/pull/2072) — Agents can now pass workspace-relative paths to `ollama_generate` for base64-encoded image ingestion.

**Infrastructure & Reliability**
- [#2084 feat(backup): daily project backup + full/per-agent restore](https://github.com/nanocoai/nanoclaw/pull/2084) — Adds disaster-recovery with daily snapshots, pluggable backends (local/S3), and CLI restore.
- [#2070 feat(inbox): accept host-path attachments in extractAttachmentFiles](https://github.com/nanocoai/nanoclaw/pull/2070) — Native adapters that hand files off disk (Signal, future) are now properly routed.
- [#2692 fix(poll-loop): retry transient 5xx API-error results, notify on exhaustion](https://github.com/nanocoai/nanoclaw/pull/2692) — SDK transient errors (e.g., 529 Overloaded) are now retried before failing; exhaustion produces a user notification.
- [#2670 fix(agent-runner): self-heal poisoned-resume crash loop](https://github.com/nanocoai/nanoclaw/pull/2670) — Fixes a crash loop (#2669) caused by corrupt `thinking`/`redacted_thinking` blocks in resumed transcripts.
- [#2277 fix(agent-runner): refresh routing on follow-up messages mid-query](https://github.com/nanocoai/nanoclaw/pull/2277) — Routing context is now refreshed when a follow-up arrives mid-query, fixing misrouted replies for null-routed cron tasks.
- [#2267 fix(agent-to-agent): route a2a replies back to originating session](https://github.com/nanocoai/nanoclaw/pull/2267) — Agent-group conversations with multiple sessions (e.g., Signal + email) no longer split-brain; replies land in the correct session.

### Open PRs (8 new, from 2026-06-12)
- [#2745 feat(memory): opt-in persistent memory scaffold for providers](https://github.com/nanocoai/nanoclaw/pull/2745)
- [#2746 feat(providers): agent-surfaces capability seam](https://github.com/nanocoai/nanoclaw/pull/2746)
- [#2747 feat(onecli): SDK 2.2.1 — credential-stub mounts + machine-checkable pins](https://github.com/nanocoai/nanoclaw/pull/2747)
- [#2748 security: harden agent containers (cap-drop, no-new-privileges, pids-limit)](https://github.com/nanocoai/nanoclaw/pull/2748)
- [#2749 security: gate agent-requested npm installs by package release age](https://github.com/nanocoai/nanoclaw/pull/2749)
- [#2750 fix: recover stale outbound.db journals after container kills](https://github.com/nanocoai/nanoclaw/pull/2750)
- [#2752 fix: stage inbound attachments that expose only a url (Discord)](https://github.com/nanocoai/nanoclaw/pull/2752)
- [#2753 fix(hooks): pre-commit fell open when pnpm was missing from PATH](https://github.com/nanocoai/nanoclaw/pull/2753)

---

## Community Hot Topics

### Most Discussed Issue
[**#2506 bug: send_message dedup silently drops responses**](https://github.com/nanocoai/nanoclaw/issues/2506) (3 comments)  
**Author:** mshirel | **Created:** 2026-05-16  
The most active conversation this period centers on a subtle race condition: when two turns complete within 60 seconds, or a follow-up arrives mid-stream, agent responses are silently dropped and the client times out. The bug has been open for nearly a month with no fix PR attached, suggesting it is complex to reproduce or fix cleanly.

### Notable Issue Activity
- [**#2711 create_agent MCP tool is ungated despite "admin-only" claims**](https://github.com/nanocoai/nanoclaw/issues/2711) by jonazri — Highlights a discrepancy between documentation and implementation; any container can create agent groups. This has significant security implications and has drawn maintainer attention.

### Active PR Discussions
Several new PRs arrived co-ordinated on 2026-06-12, suggesting a batch contribution from multiple community members:
- boazdori submitted two security PRs ([#2748](https://github.com/nanocoai/nanoclaw/pull/2748), [#2749](https://github.com/nanocoai/nanoclaw/pull/2749)).
- sturdy4days submitted two reliability fixes ([#2750](https://github.com/nanocoai/nanoclaw/pull/2750), [#2753](https://github.com/nanocoai/nanoclaw/pull/2753)).
- omri-maya submitted three feature PRs ([#2745](https://github.com/nanocoai/nanoclaw/pull/2745), [#2746](https://github.com/nanocoai/nanoclaw/pull/2746), [#2747](https://github.com/nanocoai/nanoclaw/pull/2747)) — these are core source seams, suggesting the contributor has deep familiarity with the codebase.

---

## Bugs & Stability

### High Severity

| Bug | Severity | Status | Linked Fix |
|-----|----------|--------|------------|
| [#2506] send_message dedup silently drops responses when two turns complete < 60s apart | **High** — user-visible data loss (silent timeout) | Open, 1 month old | None |
| [#2668] No per-tool timeout: hung MCP tool blocks session up to 30 min | **High** — DoS-like resource drain | Open, 2 weeks old | None |
| [#2711] create_agent ungated — any container can create agent groups | **High** — unauthorized agent creation | Open, 1 week old | None |

### Medium Severity
- [**#2751 (Closed) Budget-exhausted LLM turns silently dropped**](https://github.com/nanocoai/nanoclaw/issues/2751) by assapin — OneCLI cloud org cap reached; LLM call returns a fabricated 200 with `budget_exceeded`. The SDK treats it as success, user gets no reply. This was the only closed issue today; no fix PR was explicitly linked, but the issue may have been resolved by discussion.

### Bugs Addressed by New Open PRs
- [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) directly addresses [#2516](https://github.com/nanocoai/nanoclaw/issues/2516) and [#2640](https://github.com/nanocoai/nanoclaw/issues/2640) — stale `outbound.db` journals after container kills. This is a **high-severity** crash-loop fix.
- [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) fixes Discord attachments (images and text files) never reaching the agent in readable form — a **medium-severity** integration bug.

---

## Feature Requests & Roadmap Signals

### Likely for Next Release
The following core-seam PRs are newly open and come from a contributor with apparent maintainer trust:
- **Persistent memory scaffold** ([#2745](https://github.com/nanocoai/nanoclaw/pull/2745)) — Adds `usesMemoryScaffold` capability and a container for opt-in provider-side memory.
- **Agent-surfaces capability seam** ([#2746](https://github.com/nanocoai/nanoclaw/pull/2746)) — Host-side registry where providers declare capabilities.
- **OneCLI SDK bump + credential-stub mounts** ([#2747](https://github.com/nanocoai/nanoclaw/pull/2747)) — SDK 0.5.0 → 2.2.1, adds machine-checkable pins.

These three together suggest a **provider composability and security** theme for the next version.

### Security Roadmap Signals
Two open security PRs from boazdori signal growing community concern about container isolation:
- [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) — Default `--cap-drop=ALL`, `--no-new-privileges`, `--pids-limit 2048`.
- [#2749](https://github.com/nanocoai/nanoclaw/pull/2749) — NPM installs gated by 3-day release age, matching existing pnpm policy.

### User-Requested Features
- [#2632](https://github.com/nanocoai/nanoclaw/issues/2632) — **Multi-bot identity in Telegram v2** (arthurkrupa). User needs clarity on migration path from v1's `/add-telegram-swarm` to the current state. No resolution yet.

---

## User Feedback Summary

### Pain Points
- **Silent failures** dominate feedback: budget exhaustion ([#2751](https://github.com/nanocoai/nanoclaw/issues/2751)), duplicate response drops ([#2506](https://github.com/nanocoai/nanoclaw/issues/2506)), and long tool-call timeouts with no feedback ([#2668](https://github.com/nanocoai/nanoclaw/issues/2668)) all result in users waiting indefinitely with no error message.
- **Migration friction** — One user ([#2632](https://github.com/nanocoai/nanoclaw/issues/2632)) is planning a v1→v2 migration but finds the current Telegram multi-identity support ambiguous, noting the feature exists in git history but lacks documentation.
- **Discord integration** is broken for basic use cases (images, text pastes never reach agent) ([#2752](https://github.com/nanocoai/nanoclaw/pull/2752)).
- **Security confusion** — The `create_agent` tool's docstring claims admin-only but behavior is unrestricted ([#2711](https://github.com/nanocoai/nanoclaw/issues/2711)).

### Positive Signals
- Multiple community members are contributing fix PRs with test coverage and references to existing issues, indicating a healthy contributor ecosystem.
- The speed of merge (10 PRs in one day) suggests maintainers are actively addressing the backlog.

---

## Backlog Watch

### Stale High-Impact Issues Needing Maintainer Attention

- [**#2506 bug: send_message dedup silently drops responses**](https://github.com/nanocoai/nanoclaw/issues/2506) — **Open 28 days.** No fix PR. This is the most-commented issue and describes a user-visible data loss scenario that could affect production reliability. High priority.
- [**#2668 No per-tool timeout**](https://github.com/nanocoai/nanoclaw/issues/2668) — **Open 12 days.** No fix PR. A hung MCP tool blocks a session for up to 30 minutes; the bug report includes a clear reproduction path.
- [**#2632 Clarify Telegram multi-bot identity**](https://github.com/nanocoai/nanoclaw/issues/2632) — **Open 16 days.** No maintainer response. The user

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-13

## 1. Today's Overview
The project shows moderate activity with one open bug report and three open pull requests updated within the last 24 hours. No new releases were published today, and no PRs were merged or closed. The development focus appears to be on bug fixes and quality-of-life improvements: two PRs address agent output handling and Discord gateway resilience, while a third adds a configuration option for queue mode. The single open issue highlights a recurring pain point when using local models via Ollama, where responses are truncated or incomplete. Overall, the project is in an active bug-fixing phase, with no major regressions or disruptive changes observed.

## 2. Releases
*None today.* No new versions or release tags were created.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. However, three open PRs received updates, indicating ongoing work:
- **PR #949 (fix: make queue_mode configurable from config.json)** — Adds a new `agent.default_queue_mode` field and refactors the `QueueMode` enum to a shared location. This improves configurability for new sessions.
- **PR #951 (fix(agent_runner): suppress stderr initialization logs on agent failure)** — Prevents spurious initialization logs (memory plans, MCP server registration) from being posted to channels when the agent process exits with an error.
- **PR #953 (fix(discord): recover closed gateway sockets)** — Implements proper cleanup and health-check logic for Discord gateway reconnections, including regression tests for stalled pre-HELLO states.

## 4. Community Hot Topics
The only issue updated in the last 24 hours is **#952 (bug: Local model using ollama returns incomplete answers)**. It has zero comments and no reactions, but the author reported that an agent using a locally pulled Gemma model via Ollama fails to answer in complete sentences. A screenshot was attached. Despite the low engagement, this is the sole active issue and likely reflects a common user frustration.

- [Issue #952](https://github.com/nullclaw/nullclaw/issues/952)  
- All three open PRs (listed above) have no comments or reactions, so no other discussion topics are currently trending.

## 5. Bugs & Stability
One bug was reported today (updated):

**#952 — Local model using Ollama returns incomplete answers**  
*Severity: Medium* — Affects users who rely on local inference via Ollama. The agent’s responses are cut short, which may stem from stream handling, context limits, or a misconfiguration in the Ollama integration. No fix PR exists yet.  
- [Issue #952](https://github.com/nullclaw/nullclaw/issues/952)

No crashes, regressions, or other stability issues were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed as issues. However, **PR #949** introduces a new configuration option (`default_queue_mode`), which signals that the team is working on improving session initialisation flexibility. This could be a step toward a broader configurable agent orchestration system. No other roadmap signals are visible in today’s data.

## 7. User Feedback Summary
The sole user-reported pain point is the incomplete answer problem with Ollama local models (issue #952). The user described the issue with a screenshot, indicating they followed standard setup steps but received unsatisfactory results. This suggests that the agent’s output pipeline for local models may need attention—either in how the agent parses streamed responses or how it handles token limits. No feedback on satisfaction or use cases was otherwise recorded.

## 8. Backlog Watch
No long-standing, unanswered issues or PRs were identified in today’s data. The only open bug (#952) was created two days ago and has not yet received a maintainer response. While it is not yet “backlogged,” it may benefit from a quick triage to prevent it from slipping. The three open PRs (#949, #951, #953) are recent (last 2–3 days) and appear to be actively worked on by a contributor (vernonstinebaker). No items currently require urgent maintainer attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-13

## 1. Today’s Overview
The project saw **50 issues and 50 PRs updated in the past 24 hours**, with **20 issues closed** and **17 PRs merged or closed** — a high-activity day driven by feature work, bug fixes, and infrastructure improvements. The team is actively shipping Reborn (Engine V2) capabilities, including attachment support, Slack integration, and blocked-thread UX. No new releases were published today. CI stability and test sharding are emerging as internal priorities.

## 2. Releases
**None.** No new versions were published in the last 24 hours.

## 3. Project Progress
**Merged/closed PRs today (selected):**

- **[#4812] Drain DeferredBusy messages when the blocking run reaches terminal state** — Completes the blocked-thread UX arc; messages sent while a run is blocked on a gate now drain automatically once the blocking run terminates. *(CLOSED)*
- **[#4773] Record/replay machinery for QA-phrase traces on the Reborn runtime** — Adds deterministic replay of QA agent behavior in CI. *(CLOSED)*
- **[#4562] Record auth continuation dispatch failures** — Adds SecurityAuditSink entries for auth-continuation failures. *(CLOSED)*
- **[#4568] Bound before-capability dispatch fan-out** — Caps hook dispatch fan-out per boundary, fails closed. *(CLOSED)*
- **[#4569] Enforce aggregate tenant predicate key caps** — Enforces MAX_KEYS_PER_TENANT across predicate backends. *(CLOSED)*

**Notable open PRs (active work):**
- [#4838] Explicit gate-open feedback for busy threads (no parking) — Replaces deferred drain with a rejection‑and‑notice contract.
- [#4837] Gated final-answer nudge for empty/canned turn endings — Issues one extra tool-free call when the agent would otherwise end with no real answer.
- [#4836] Surface connected channels, delivery state, and run origin as runtime-context slice — Adds `msg:runtime.*` lines for model awareness.
- [#4835] Persist “always allow” approvals across threads — Drops `thread_id` from persistent approval scope.
- Attachment track PRs [#4654], [#4655], [#4668], [#4670] — Building the full Reborn attachment pipeline (format registry, transcript refs, storage landing, byte bridging).

## 4. Community Hot Topics
Most active issues by comment count (3 comments each):

- **[#4817] DeferredBusy drain follow-ups: trusted-resubmit seam, stale-intent policy, startup sweep** — Tracks three deferred design decisions from the merged drain PR; discusses architectural choices around resubmission and intent persistence.  
  [Issue #4817](https://github.com/nearai/ironclaw/issues/4817)

- **[#4825] Reborn: persist “always allow” approvals across threads (drop thread_id from persistent approval scope)** — Users are re-prompted for the same capability in every new thread; the fix is being addressed in PR #4835.  
  [Issue #4825](https://github.com/nearai/ironclaw/issues/4825)

- **[#4703] [CLOSED] NEAR AI model picker saves display name instead of model ID** — *Closed today; highlights a persistence bug that confused provider configuration.*

PR activity is dominated by the Reborn attachment set and runtime context PRs, each with follow-up discussion.

## 5. Bugs & Stability
**New open bugs today (ranked by severity):**

- **High** — `cargo-deny` CI failure [#4824] — New RUSTSEC advisories against postgres crates block all PRs. Immediate infrastructure issue. *(Open, no fix PR yet)*  
  [Issue #4824](https://github.com/nearai/ironclaw/issues/4824)

- **Medium** — [#4762] Failed tool workflow causes inconsistent follow-up message ordering and activity display. *(Open)*  
- **Medium** — [#4796] LLM lacks awareness of current date/time unless explicitly using a time tool — affects calendar/scheduling workflows. *(Open)*  
- **Medium** — [#4759] Workspace path is duplicated when using workspace-relative paths. *(Open)*  
- **Low** — [#4697] Active provider status inconsistent in Inference settings (displays wrong active provider). *(Open)*  
- **Low** — [#4823] No UI feedback when deleting a running conversation fails. *(Open)*  
- **Low** — [#4819] Attachment warning banner difficult to read in Light theme. *(Open)*  
- **Low** — [#4696] Local Ollama Test connection falsely reports success when Ollama is not running. *(Open)*  

**Closed bugs today** (from previous days): #4703, #4705, #4673, #4706, #4733, #4722, #4721, #4719, #4725, #4720, #4724, #4770 — Many UX and onboarding issues fixed.

## 6. Feature Requests & Roadmap Signals
**New feature requests / enhancements:**

- **Surface connected channels & delivery state** [#4828] — Model needs ambient knowledge of connected Slack/Discord and delivery target. PR #4836 implements this.
- **Track Engine V2 LLM usage in /api/admin/usage** [#4822] — Admin usage endpoints need to cover Reborn (V2) calls. Likely next iteration.
- **Split long CI test jobs into smaller shards** [#4813] — Improves developer feedback loop. Internal need, likely upcoming.
- **Decompose slack_delivery.rs (~4k lines)** [#4818] — Code health driven by file-size budget rule.

**Trending feature area:** The Reborn attachment pipeline (multiple PRs) and blocked‑thread UX (drain, explicit feedback) are clearly the next major deliverables. The “always allow” approval persistence fix (PR #4835) should land soon, addressing a common user pain point.

## 7. User Feedback Summary
Recent user feedback (from issues filed 2026-06-10 to 2026-06-12) highlights:

- **Onboarding friction**: NEAR AI SSO setup fails locally (#4705, #4706); provider save after test connection does not persist (#4673).
- **UX regressions**: Conversation messages show no user/assistant identity (#4722); sidebar PINNED section incorrectly shows active conversation (#4721); drafts lost when leaving New Conversation (#4724); composer remains interactive while working (#4725); attachment warning persists across conversations (#4720); flickering on conversation return (#4719); response links navigate away (#4733).
- **Connectivity confusion**: Active provider status inconsistent (#4697); Slack reconnect loop (addressed by #4777, #4778).  
- **Functional gaps**: No date/time awareness (#4796); workspace path duplication (#4759); tool activity may stop updating after refresh (#4770, closed).

Most of these have been closed with fixes; a few remain open (#4697, #4762, #4796, #4759). Overall satisfaction seems mixed — users appreciate progress but encounter rough edges in the Reborn UI and provider configuration.

## 8. Backlog Watch
Notable items requiring maintainer attention:

- **PR #3708** — Release PR (`ironclaw_common`, `ironclaw_skills`, `ironclaw` version bumps) — Open since May 16, awaiting final review and merging. Blocking new releases.  
  [PR #3708](https://github.com/nearai/ironclaw/pull/3708)

- **Issue #4824** — `cargo-deny` CI failures blocking all PRs — No fix or workaround yet.  
- **PR #4561** — Record MCP direct-lease denials in SecurityAuditSink — Open since June 8, may need re-review after other hook PRs merged.  
- **PR #4588** — Reborn observability seams (trajectory observer + LLM provider injection) — Open since June 9, important for benchmarking parity.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-13

## 1. Today's Overview
Project activity was **very high**, with **17 pull requests updated** in the last 24 hours (11 closed/merged, 6 still open) and **1 issue closed**. The major event was the **merge of release branch `release/2026.6.11` into `main`** (PR #2158), which bundles several new features (Computer Use MVP, real-time ASR voice input, HTML artifact sharing, image/SVG artifact sharing support) and a wave of stability fixes. The sole issue update (Issue #1) was also closed after being reported back in February, indicating ongoing bug triage. No new releases were published today, but the merge suggests a release is imminent.

---

## 2. Releases
No new releases were published on 2026-06-13. The release merge (PR #2158) signals that **version 2026.6.11** (or 2026.6.12) is being prepared; its highlights include Computer Use MVP, real-time ASR voice input for cowork prompts, HTML artifact public sharing mode, and image/SVG artifact sharing. Breaking changes and migration notes are not yet available.

---

## 3. Project Progress (Merged/Closed PRs Today)
**11 PRs were closed/merged** (all from 2026-06-12). They fall into two groups:

### A. Release preparation
- **[#2158] chore(release): merge release/2026.6.11 into main**  
  Bundles all features and fixes for the upcoming release.  
  [PR #2158](https://github.com/netease-youdao/LobsterAI/pull/2158)

### B. Bug fixes and refinements (recent)
- **[#2156] fix(computer-use): bump runtime to 1.0.7**  
  Improves diagnostic capabilities (UIA breadcrumbs) for the Computer Use helper.  
  [PR #2156](https://github.com/netease-youdao/LobsterAI/pull/2156)

- **[#2157] fix(media): correct image extension when saving**  
  Saves images with the real format (detected from bytes) instead of trusting server filename extensions (e.g., PNG content no longer saved as .jpg).  
  [PR #2157](https://github.com/netease-youdao/LobsterAI/pull/2157)

- **[#2155] fix(voice-input): prevent duplicate real-time ASR starts**  
  Avoids race conditions in the cowork voice input flow.  
  [PR #2155](https://github.com/netease-youdao/LobsterAI/pull/2155)

- **[#2154] fix(cowork): show model metadata after stopped streams**  
  Preserves model information for manually stopped partial replies; adds regression test.  
  [PR #2154](https://github.com/netease-youdao/LobsterAI/pull/2154)

- **[#2153] fix(cowork): preserve same-name package model selection**  
  Keeps explicit model references (e.g., `lobsterai-server/...`) during normalization; adds logs and regression tests.  
  [PR #2153](https://github.com/netease-youdao/LobsterAI/pull/2153)

### C. Stale PRs closed today (merged after months)
These were originally created in early April 2026 but were closed today, likely as part of the release merge:
- **#1473 – AgentCreateModal: unsaved changes confirmation** (closes #1468)
- **#1474 – AgentSettingsPanel: unsaved changes confirmation** (closes #1469)
- **#1475 – MCP server form modal: unsaved changes confirmation** (closes #1470)
- **#1476 – CoworkPromptInput: draft persistence on unmount** (closes #1471)
- **#1477 – Re-edit message: overwrite confirmation** (closes #1472)

[PR #1473](https://github.com/netease-youdao/LobsterAI/pull/1473) | [PR #1474](https://github.com/netease-youdao/LobsterAI/pull/1474) | [PR #1475](https://github.com/netease-youdao/LobsterAI/pull/1475) | [PR #1476](https://github.com/netease-youdao/LobsterAI/pull/1476) | [PR #1477](https://github.com/netease-youdao/LobsterAI/pull/1477)

These fixes address user data loss risks across multiple UI dialogs and session transitions.

---

## 4. Community Hot Topics
Only **one issue** was updated (Issue #1, now closed), and none of the PRs have comments recorded. Activity is therefore concentrated on code contributions rather than discussion.

- **[#1] hit API error with OpenAI API Type** [CLOSED]  
  *Author: simson2010 | Created: 2026-02-19 | Updated: 2026-06-12 | 7 comments*  
  A user on macOS 13.7.8 (2017 Intel Mac) got a 400 API error when using OpenAI message type after configuring a MiniMaxi API key. The issue was closed today after 4 months, likely with a fix included in the release.  
  [Issue #1](https://github.com/netease-youdao/LobsterAI/issues/1)

**Underlying need**: Seamless compatibility between different API providers and message types – users expect the “OpenAI message type” to work even when using a non-OpenAI backend.

---

## 5. Bugs & Stability
### High severity (fixed today)
- **Image format corruption** (PR #2157): Images could be saved with wrong extension (e.g., PNG as .jpg). **Fixed**.
- **Duplicate ASR start requests** (PR #2155): Could cause duplicate voice input or erratic behavior. **Fixed**.
- **Stopped stream model metadata loss** (PR #2154): Manually stopped partial replies lost model info. **Fixed**.
- **Same-name model selection overwritten** (PR #2153): Package models with same name as custom models could be silently mis-assigned. **Fixed**.

### Medium severity (fixed in stale PRs merged today)
- **Data loss – unsaved changes**: Four separate modals (Agent creation, Agent settings, MCP server config, session draft) lacked confirmation dialogs. All fixed.
- **Re-edit message overwrite**: Editing a past message could silently discard current input. Fixed.

### Low severity (open stale PRs still not merged)
- **Gateway infinite restart loop** (#1446) – still open.
- **Missing i18n** (#1448, #1449) – English text in Chinese UI.
- **Disabled skill still injected** (#1453) – serious but fix exists and is open since April.
- **Scheduled task “no repeat” mode broken** (#1454) – button does nothing.
- **Shortcut duplication** (#1456) – no conflict detection.

[PR #1446](https://github.com/netease-youdao/LobsterAI/pull/1446) | [PR #1448](https://github.com/netease-youdao/LobsterAI/pull/1448) | [PR #1453](https://github.com/netease-youdao/LobsterAI/pull/1453) | [PR #1454](https://github.com/netease-youdao/LobsterAI/pull/1454) | [PR #1456](https://github.com/netease-youdao/LobsterAI/pull/1456)

---

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, the **release merge** (PR #2158) reveals clear roadmap priorities:

- **Computer Use MVP** – enabling AI agents to interact with the desktop (new built-in kit).
- **Real-time ASR voice input** – hands-free voice for cowork prompts.
- **Artifact sharing** – public sharing mode for HTML, image, and SVG artifacts (likely aiming for collaborative or portfolio use cases).

These features suggest LobsterAI is moving toward **multimodal agent interfaces** (voice, screen automation) and **sharing capabilities** – probably in preparation for a v1.0 or major update.

---

## 7. User Feedback Summary
The single issue (#1) indicates a **real user pain point**: configuring a non-OpenAI API (MiniMaxi) and selecting “OpenAI message type” produced a silent 400 error. The user waited 4 months for a fix, which suggests that **API compatibility** is a critical concern for users trying to use alternative providers. No satisfaction/dissatisfaction data beyond the issue closure.

Additionally, the stale fixes merged today address **user data loss** (unsaved changes, draft overwrites) – these had been reported (issues #1468–#1472) and are now resolved, likely improving user trust.

---

## 8. Backlog Watch
Several **important PRs remain open** (all created in early April, last updated today, marked `stale`):

| PR | Summary | Age | Potential Impact |
|---|---|---|---|
| [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) | Gateway infinite restart loop | 71 days | Critical – crashes application on startup |
| [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448) | i18n missing in Agent settings | 71 days | UX quality – non-Chinese users affected |
| [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) | Scheduled task session grouping | 71 days | Usability – session list becomes cluttered |
| [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) | Disabled skills still injected | 71 days | Security/functionality – unintended skill activation |
| [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) | “No repeat” scheduled task broken | 71 days | Bug – feature dead |
| [#1456](https://github.com/netease-youdao/LobsterAI/pull/1456) | Shortcut duplication detection | 71 days | UX – ambiguous shortcuts |

All six PRs have been open for over two months, though they were updated today (possibly rebased). Maintainers should consider merging them in the next release cycle, especially #1446 (crash) and #1453 (security-like issue).

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-13

## Today’s Overview
The project is in a quiet but productive state today. In the last 24 hours, three issues have been updated, all remaining open, and no pull requests have been merged or closed. No new releases were published, indicating a period of evaluation rather than rapid iteration. The community is actively discussing one bug report and two feature proposals, suggesting that the project is attracting interest from users with diverse deployment and integration needs – from enterprise Kubernetes isolation to local speech-to-text engines.

## Releases
*No new releases were published today.*

## Project Progress
**Merged/Closed PRs today:** None  
No pull requests were updated or completed in the last 24 hours. No code changes were merged, so no features or fixes have advanced today.

## Community Hot Topics
Three issues are receiving recent attention:

- **#1115 – [Bug]: Fastmail MCP Authorisation**  
  *(open, updated 2026-06-12, 2 comments)*  
  [Link to issue](https://github.com/moltis-org/moltis/issues/1115)  
  A user reports an authorization problem when using Fastmail’s MCP (Model Context Protocol) integration. The reporter has confirmed they are on the latest version. The underlying need appears to be a reliable, authenticated connection to Fastmail for agent-based email workflows. This issue may require maintainers to reproduce the authorization flow or provide configuration guidance.

- **#1118 – [Feature]: Add Kubernetes-native sandbox backend with runtimeClassName support**  
  *(open, updated 2026-06-12, 1 comment)*  
  [Link to issue](https://github.com/moltis-org/moltis/issues/1118)  
  A detailed proposal to introduce a `kubernetes` sandbox backend that spawns ephemeral pods with configurable `runtimeClassName` (e.g., Kata Containers, gVisor). The author highlights the need for stronger isolation of untrusted LLM-generated commands. This feature would appeal to enterprise users running Moltis in cloud-native environments.

- **#1102 – Feature: Add FunASR/SenseVoice as local STT engine**  
  *(open, updated 2026-06-12, 1 comment)*  
  [Link to issue](https://github.com/moltis-org/moltis/issues/1102)  
  A request to integrate FunASR or SenseVoice for local speech-to-text, citing ultra-low latency (~70ms for 10s audio) and native streaming support. This indicates demand for offline, high-performance voice interfaces within Moltis.

## Bugs & Stability
One bug is currently open and active:

- **#1115 – Fastmail MCP Authorisation** (severity: medium)  
  This is the only bug reported in the last 24 hours. No fix PRs exist yet. The author has followed the issue template, so the details should be actionable. If the authorization flow fails consistently, it could block users relying on Fastmail integration. No other regressions or crashes were reported.

## Feature Requests & Roadmap Signals
Two feature requests were updated today:

1. **Kubernetes-native sandbox backend** (#1118) – This is a substantial architectural addition. Given the specificity and the fact that it was filed very recently (2026-06-12), it is likely still under community review. It could be considered for a future minor release if the maintainers see alignment with their security roadmap.

2. **FunASR/SenseVoice local STT** (#1102) – This request is two weeks old but still active. The project already supports some STT engines (e.g., Whisper, Azure), so adding another local option is plausible. The low-latency argument may accelerate its inclusion, especially if the maintainers prioritize on-device performance.

Both features signal a community leaning toward more self‑hosted, secure, and high‑performance configurations.

## User Feedback Summary
- **Pain points:** Authorization complexity with third‑party MCP services (Fastmail) and a desire for stronger sandbox isolation when executing LLM‑generated commands.
- **Use cases:** Email automation via Fastmail (requiring robust auth) and deployment on Kubernetes clusters with security‑sensitive workloads.
- **Satisfaction/dissatisfaction:** Users are engaged and filing well‑structured proposals and bug reports, indicating a generally healthy relationship with the project. The lack of maintainer responses on these issues (none today) may be a point of mild friction, but it is not unusual for a 24‑hour window.

## Backlog Watch
- **#1115 – Fastmail MCP Authorisation** (open since 2026-06-11) – No response from maintainers yet. This is the only current bug and has been awaiting a reply for two days; it should be prioritized to prevent user frustration.
- **#1102 – FunASR/SenseVoice STT** (open since 2026-06-04) – No maintainer comment in the last 8 days. While it’s a feature request, a brief acknowledgement could encourage the contributor and the community.
- **#1118 – Kubernetes sandbox** (open since yesterday) – No maintainer response yet, but that’s expected within 24 hours. Watch for triage label assignment.

*No other long‑unanswered issues were found in the provided data.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-13

## 1. Today's Overview
Activity remains high with **21 issues** and **24 pull requests** updated in the last 24 hours. Of those, 7 issues were closed and 11 PRs merged or closed – indicating solid momentum in bug fixing and feature delivery. No new release was cut today, but the project is actively preparing a beta (v1.1.12b1). The community is engaged around critical bugs (scheduled task failures, download regressions) and forward-looking features (AgentScope 2.0 migration, multi-agent collaboration). The overall health is strong, though a few high-severity regressions (auto‑crash, conversation hangs) require immediate attention.

## 2. Releases
**None** – no new releases in the last 24 hours.

## 3. Project Progress
Several important fixes and infrastructure improvements were merged or closed today:

| PR | Summary |
|----|---------|
| [#5159](https://github.com/agentscope-ai/QwenPaw/pull/5159) | **Release version format fix** – switched to `1.1.12b1` for the next beta. |
| [#5157](https://github.com/agentscope-ai/QwenPaw/pull/5157) | **Chore release bump** – aligned package version with beta increment. |
| [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) | **Fix memory config loss** – forces Collapse panels to render so form values are not lost (fixes [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137)). |
| [#5147](https://github.com/agentscope-ai/QwenPaw/pull/5147) | **Fix session redirect on coding mode refresh** – updated routing to preserve session (fixes [#5142](https://github.com/agentscope-ai/QwenPaw/issues/5142)). |
| [#5154](https://github.com/agentscope-ai/QwenPaw/pull/5154) | **Refactor memory search tool UI** – corrected empty/unknown display in results (fixes [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098)). |
| [#5121](https://github.com/agentscope-ai/QwenPaw/pull/5121) | **Release verification gate** – new CI step for end-to-end install/boot check before publishing. |
| [#4144](https://github.com/agentscope-ai/QwenPaw/pull/4144) | **CLI readiness check fix** – uses loopback when host is `0.0.0.0` (Windows compatibility). |
| [#5022](https://github.com/agentscope-ai/QwenPaw/pull/5022) | **Guard workspace restore** – prevents placing agent workspaces inside managed directories. |
| [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) | **Runtime 2.0** – modular architecture with `ToolCoordinator` (breaking change). |

These show the team is actively squashing UI bugs, hardening the release pipeline, and laying the groundwork for the much-anticipated runtime upgrade.

## 4. Community Hot Topics
The most discussed issues reflect deep user needs:

- **[Issue #5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)** – *“由agnet生产的定时任务, 无法正常触发”* (11 comments)  
  Scheduled tasks created by agents are not triggered. No error is shown, but the task never fires. Users cannot manually edit these tasks. **Underlying need**: reliable agent-driven job scheduling with manual override.

- **[Issue #4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)** – *“Migrate backend from AgentScope 1.x to AgentScope 2.0”* (10 comments, 2 👍)  
  A planned breaking change to adopt the new AgentScope 2.0 architecture. This is a major community concern and a sign that users are eagerly awaiting the upgrade.

- **[Issue #5140](https://github.com/agentscope-ai/QwenPaw/issues/5140)** – *“附件下载还是有bug”* (6 comments, closed)  
  Downloading non‑text files (docx, pdf) returns HTTP 404 in v1.1.11.post2. Text files work fine. Closed today, implying a fix was deployed.

- **[Issue #5137](https://github.com/agentscope-ai/QwenPaw/issues/5137)** – *“向量模型自动记忆搜索配置丢失”* (5 comments, closed)  
  Memory configuration lost when saving without expanding collapsed cards. Fixed by PR #5144.

Other active threads include feature requests for Kimi‑for‑coding support, agent swarm collaboration, and Slack integration (see section 6).

## 5. Bugs & Stability
Several bugs reported today, ranked by severity:

| Severity | Issue | Description | Status | Fix PR? |
|----------|-------|-------------|--------|---------|
| 🔴 High | [#5155](https://github.com/agentscope-ai/QwenPaw/issues/5155) | Auto crash/restart on Docker (v1.1.11) | Open | None yet |
| 🔴 High | [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | Long conversation causes complete hang | Open | None yet |
| 🔴 High | [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | Dialogue thinking logic enters infinite loop | Open | None yet |
| 🟡 Medium | [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | Agent‑generated scheduled tasks never fire | Open | None yet |
| 🟡 Medium | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | File download 404 for docx/pdf (fixed in today’s build) | Closed | Internal fix |
| 🟢 Low | [#5145](https://github.com/agentscope-ai/QwenPaw/issues/5145) | Execution details always expanded, cluttering UI | Open | None yet |
| 🟢 Low | [#5148](https://github.com/agentscope-ai/QwenPaw/issues/5148), [#5143](https://github.com/agentscope-ai/QwenPaw/issues/5143) | Math formula rendering (square root displayed as line) | Closed | No dedicated PR (likely UI fix) |

Three critical regressions (auto‑crash, conversation hang, infinite loop) have no associated fix PRs yet – these should be prioritised for the upcoming beta release.

## 6. Feature Requests & Roadmap Signals
Today’s feature requests and enhancement issues point to strong community demand:

| Request | Issue/PR | Likelihood for Next Version |
|---------|----------|-----------------------------|
| **Kimi‑for‑coding API support** | [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) | Medium – straightforward provider addition |
| **Agent team/swarm collaboration** | [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | High – PR #5078 (Runtime 2.0) lays groundwork |
| **System tray, auto‑start, background service** | [#5164](https://github.com/agentscope-ai/QwenPaw/issues/5164) | Medium – fits desktop enhancement trend |
| **Slack channel support** | [#5152](https://github.com/agentscope-ai/QwenPaw/issues/5152) | High – active channel development (Yuanbao, WeCom) |
| **Feishu CardKit streaming optimisation** | [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167) | Medium – performance improvement |
| **Visual model fallback for text‑only LLMs** | PR [#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069) | High – under review, likely in v1.1.12 |
| **Token and context usage popover** | PR [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) | High – adds visibility to token consumption |
| **Agent OS Driver (MCP/A2A/ACP abstraction)** | PR [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) | Medium‑long term – foundational for interoperability |

The **AgentScope 2.0 migration** (Issue #4727) and the merged **Runtime 2.0** PR #5078 are the strongest roadmap signals – they will enable multi‑agent collaboration and modern tool‑calling.

## 7. User Feedback Summary
**Pain points** reported today centre on reliability and functionality:
- Scheduled tasks created by agents are broken (no trigger, no edit capability) – a core agent capability.
- File downloads regressed in post‑releases (now fixed for most cases).
- Memory configuration lost due to UI collapsing behaviour (fixed).
- Session loss when refreshing in coding mode (fixed).
- Three separate reports of system‑level hangs/crashes (auto‑restart, conversational deadlock).
- UI rendering glitches (execution details always expanded, math formulas mis‑rendered).

**Positive signals**: users are actively requesting deeper integrations (Slack, Kimi, agent teams) and performance improvements (Feishu CardKit streaming, token usage visibility). The community is engaged and invested in the project’s evolution.

## 8. Backlog Watch
The following items need maintainer attention due to age, importance, or lack of response:

| Issue/PR | Days Open | Comment | Action Needed |
|----------|-----------|---------|---------------|
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) – AgentScope 2.0 migration | 17 days | 10 comments, 2 👍, no merged PR yet | Update with timeline or assign to a release milestone |
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) – Scheduled tasks not firing | 3 days | 11 comments, high severity | Urgent – needs root‑cause analysis and fix |
| [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) – Gemini tool‑call regression | 1 day | 1 comment, no maintainer reply | Reproduce and triage |
| [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165) – White screen after packaging | 1 day | 1 comment, no maintainer reply | Investigate missing modules in spec |
| [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) – Plugin installation fails on Python 3.13 (missing `imghdr`) | 1 day | 1 comment, no reply | Add compatibility shim for removed stdlib module |
|

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-06-13

## Today’s Overview

The project remains in a high-activity state with **32 pull requests** and **13 issues** updated in the last 24 hours. A major structural RFC (unifying the three agent turn engines) has been implemented via a single consolidation PR (#7540) and is now under review. The v0.8.0 release queue (tracker #7112) was closed, signalling that the stable-tier blockers are resolved, while the v0.8.1 additive PR queue (#6970) continues to grow. However, a cluster of **S1 (workflow-blocked) bugs** reported today – affecting macOS installation, Windows quickstart, Docker builds, the web dashboard, and the `ask_user` tool – indicates that stability and onboarding require immediate attention. No new releases were published.

## Releases

**None.**  
No releases were cut in the last 24 hours. The latest available version is v0.8.0 (as referenced in bug reports). The v0.8.0 release tracker (#7112) was closed, suggesting that the release content is finalised and the next tagged version will likely be v0.8.1.

## Project Progress

**Merged/Closed PRs (3):**

- [[CLOSED] **#7548** – Chore/01.5 cargo cleanup](https://github.com/zeroclaw-labs/zeroclaw/pull/7548) – A wide-ranging dependency and CI cleanup touching most subsystems.
- [[CLOSED] **#7545** – fix(runtime): auto-include discovered MCP tools in risk_profile allowed_tools](https://github.com/zeroclaw-labs/zeroclaw/pull/7545) – Fixes MCP tools being invisible when an agent’s `risk_profile` has an explicit `allowed_tools` list.
- [[CLOSED] **#7540 remains open** – refactor(runtime): consolidate the three agent turn engines](https://github.com/zeroclaw-labs/zeroclaw/pull/7540) – The implementation of RFC #7415 is still **open** and under review; it was not merged today.

**Issues Closed (2):**

- [**#7112** – v0.8.0 release queue and Stable-tier blockers](https://github.com/zeroclaw-labs/zeroclaw/issues/7112) – Closed as accepted.
- [**#6443** – Twitch chat channel (thin IRC adapter)](https://github.com/zeroclaw-labs/zeroclaw/issues/6443) – Closed after implementation.

**Key Features Advanced (Open PRs):**

- [**#7549** – fix(plugins): align install/discovery paths and add legacy migration](https://github.com/zeroclaw-labs/zeroclaw/pull/7549) – Resolves a critical mismatch between `plugin install` destination and runtime scan paths.
- [**#7547** – fix(runtime): auto-include discovered MCP tools in risk_profile allowed_tools](https://github.com/zeroclaw-labs/zeroclaw/pull/7547) – Second attempt (after #7545) to fix MCP tool visibility.
- [**#7546** – fix(runtime): unify SopEngine construction – single instance per daemon](https://github.com/zeroclaw-labs/zeroclaw/pull/7546) – Eliminates duplicate engine instances that were causing state divergence.
- [**#7524** – feat(channels/discord): derive gateway intents from config instead of hardcoding](https://github.com/zeroclaw-labs/zeroclaw/pull/7524) – Adds configurability for Discord bot intents.

## Community Hot Topics

**Most Active Issues (by comments):**

1. [**#7415** – RFC: Unify the three agent turn engines](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) (3 comments) – The RFC has been executed as a single consolidation PR (#7540). The discussion centred on implementation shape and maintainer direction.
2. [**#7112** – v0.8.0 release queue tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/7112) (3 comments) – Recently closed; comments covered final stable-tier decisions.
3. [**#6443** – Twitch chat channel](https://github.com/zeroclaw-labs/zeroclaw/issues/6443) (2 comments) – Closed feature request; garnered community interest for Twitch integration.

**Most Active PRs (no comment counts provided, but by recency and size):**

- [**#7540** – refactor(runtime): consolidate three agent turn engines](https://github.com/zeroclaw-labs/zeroclaw/pull/7540) – The biggest structural change this week. Underlying need: eliminate duplicated logic and subtle behavioral differences between channel/CLI, gateway, and embedded agent turns.
- [**#7245** – fix(read_skill): support plugin-bundled skills](https://github.com/zeroclaw-labs/zeroclaw/pull/7245) – Still open and requires author action after reviewers requested changes.
- [**#7429** – feat(plugins): add wasmtime dependency](https://github.com/zeroclaw-labs/zeroclaw/pull/7429) – Long-running effort to migrate away from Extism; carries high risk due to dependency version changes.

**Underlying Needs:**  
Users are pushing for **better model configurability** (llama.cpp router, streaming card messages), **multi-session web chat**, and **plugin path consistency**. The high volume of bug reports indicates that the v0.8.0 release, while feature-complete, introduced regressions that block new users.

## Bugs & Stability

**Critical (S1 – workflow blocked) bugs reported today:**

| Issue | Component | Summary | Fix PR exists? |
|-------|-----------|---------|----------------|
| [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | web dashboard | Dashboard not available on macOS (v0.8.0, brew install). | [#7529](https://github.com/zeroclaw-labs/zeroclaw/pull/7529) (partial – fixes misleading URL print) |
| [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | gateway/api | `ask_user` tool fails instantly with "Channel closed" in WS sessions. | None yet |
| [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | runtime/daemon | `zeroclaw quickstart` fails on Windows 10 with "no map-keyed/list section at peer-groups". | None yet |
| [#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) | unknown | Docker build fails due to missing `g++` in `cargo web build`. | [#7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534) |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | runtime/daemon | macOS app does not work; can't detect permissions, window disappears. | None yet |

**High Severity (S2 – degraded behavior) bug:**

| Issue | Component | Summary | Fix PR exists? |
|-------|-----------|---------|----------------|
| [#7541](https://github.com/zeroclaw-labs/zeroclaw/issues/7541) | gateway/api | V3 legacy paths still use `data_dir` as agent workspace dir; gateway WS and one-shot channel broken. | None yet |

**Additional bugs (lower severity or non-blocking):**

- [#7528](https://github.com/zeroclaw-labs/zeroclaw/pull/7528) – Windows update test panics due to `.zip` vs `.tar.gz` mismatch. Fixed in PR.
- [#7530](https://github.com/zeroclaw-labs/zeroclaw/pull/7530) – `zeroclaw update` fails on Windows because `.zip` assets are rejected. Fixed in PR.
- [#7538](https://github.com/zeroclaw-labs/zeroclaw/pull/7538) – `Cmd+C` on macOS triggers quit instead of copy in zerocode. Fixed in PR.

**Observations:**  
Five S1 bugs were opened in a single day – a worrying signal. While three have fix PRs (#7529, #7534, #7528/7530), the most impactful (dashboard unavailable, `ask_user` failure, Windows quickstart, macOS app) lack proposed fixes. The v0.8.0 release appears to have broken core onboarding paths.

## Feature Requests & Roadmap Signals

**New feature requests (opened today):**

- [**#7543** – Multi-session support in gateway web chat UI](https://github.com/zeroclaw-labs/zeroclaw/issues/7543) – Session sidebar with new/switch/rename/delete. High-demand for power users.
- [**#7539** – llama.cpp model router](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) – Allow quick switching between local models in llama.cpp without editing config.
- [**#7531** – Streaming card messages for QQ/DingTalk/WeChat/Feishu](https://github.com/zeroclaw-labs/zeroclaw/issues/7531) – Reduce user wait time for rich card messages on Chinese platforms.

**Ongoing roadmap signals:**

- The turn engine consolidation (RFC #7415 → PR #7540) is the most significant architectural change and is likely to land in v0.8.1.
- The WASM plugin migration (PR #7429) and the `plugins_dir` alignment (PR #7549) are steps toward the long-promised Plugins catalog (#6489).
- Multi-session web chat (#7543) and streaming card messages (#7531) are likely candidates for v0.8.1 or v0.9.0, given community interest.

**Prediction for next version (v0.8.1):**  
Turn engine consolidation, MCP tool visibility fixes, plugin path fixes, and at least one of the multi-session / streaming card features are probable. The llama.cpp router may be lower priority unless more users request it.

## User Feedback Summary

**Real pain points voiced in today’s bug reports:**

- **Onboarding disaster:** New users cannot install on Windows (quickstart fails) or macOS (app crashes / dashboard missing). The "brew install" path produced a non-functional dashboard (#7523). A Windows user reported a cryptic `peer-groups` error (#7537).
- **`ask_user` tool broken:** An agent using the web dashboard cannot ask the user a question – a core interactive workflow (#7542).
- **Docker unavailable:** Developers cannot build the container image (#7533).
- **Update mechanism broken on Windows:** `zeroclaw update` silently fails (#7530).
- **MacOS keybinding conflict:** `Cmd+C` invokes quit instead of copy in zerocode (#7538) – minor but annoying.

**Positive sentiment:**  
The user who requested the llama.cpp router (#7539) said "I recently tried this app and found it very useful for working on smaller tasks with small local models" – indicating that when it works, the app delivers value.

**Overall satisfaction:**  
Low. The high number of S1 bugs suggests the v0.8.0 release was not thoroughly tested on all platforms. New users are particularly affected. The community remains engaged (many PRs, feature requests), but stability is the top concern.

## Backlog Watch

**Important issues/PRs that need maintainer attention:**

- [**#7245** – fix(read_skill): cannot load plugin-bundled skills](https://github.com/zeroclaw-labs/zeroclaw/pull/7245) (open since 2026-06-05) – Marked `needs-author-action` for 8 days; the author has not responded to reviewer feedback. Blocks skills from plugins.
- [**#6970** – v0.8.1 integration/channel/provider/tool PR queue](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) (open since 2026-05-27) – The operational tracker has no comments and is not being actively updated; may be stale.
- [**#7429** – feat(plugins): add wasmtime dependency](https://github.com/zeroclaw-labs/zeroclaw/pull/7429) (open since 2026-06-09) – A high-risk PR that changes the WASM runtime; pending review.
- [**#6842** – feat(providers): add NEAR AI Cloud provider](https://github.com/zeroclaw-labs/zeroclaw/pull/6842) (open since 2026-05-21) – Lacks recent maintainer comments; may need updated to resolve conflicts.

**No issues older than 30 days without a response** – the maintainers are relatively responsive, but the backlog of unmerged PRs (29 open) is growing. The turn engine consolidation PR (#7540) is the only one with explicit maintainer direction and is being actively reviewed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/zhouyuhechuan/agents-radar).*