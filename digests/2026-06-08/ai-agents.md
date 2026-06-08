# OpenClaw 生态日报 2026-06-08

> Issues: 295 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-08 02:52 UTC

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

## OpenClaw 项目深度报告

好的，以下是基于 OpenClaw 项目 GitHub 数据生成的 2026-06-08 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-08

## 今日速览

过去 24 小时内，OpenClaw 项目保持了极高的社区活跃度。**Issues 更新量达到 295 条**，其中新开和活跃议题 180 条；**Pull Requests 更新量高达 500 条**，但待合并数量占到了三分之二，表明社区贡献踊跃但审核流程存在瓶颈。**今日无新版本发布**，但数个关键的 P1 级 Bug 修复 PR 已进入待审核状态，核心功能修复正在稳步推进。整体来看，项目处于**高产出、高关注度、高修复压力**的活跃发展期。

## 版本发布

今日无新版本发布。

## 项目进展

尽管没有新版本发布，但多个关键 PR 已完成合并或处于待合并状态，显著推动了项目的稳定性和功能完善：

- **关键 Bug 修复合并**：PR **#91304** ([link](https://github.com/openclaw/openclaw/pull/91304))（已关闭）修复了 session 从 JSONL 重放时，因 `thinkingSignature` 标记残留导致 Anthropic 模型报错的问题，这对多模型切换的用户至关重要。PR **#87909** ([link](https://github.com/openclaw/openclaw/pull/87909))（已关闭）修复了长消息回复时内容被过度截断的问题，提升了 Slack/Telegram 等渠道的回复体验。PR **#70330** ([link](https://github.com/openclaw/openclaw/pull/70330))（已关闭）修复了网关重启后，WebChat 会话可能被静默轮替导致历史丢失的问题。PR **#91303** ([link](https://github.com/openclaw/openclaw/pull/91303))（已关闭）更新了 `hono` 依赖，解决了 4 个中等安全漏洞，提升了项目安全性。

- **关键功能推进**：PR **#90328** ([link](https://github.com/openclaw/openclaw/pull/90328))（待合并）新增了模型选择器中的 `agentRuntime` 元数据，使用户在 WebUI 中能清晰区分不同模型的运行环境（如原生 vs Codex），提升了配置透明度。PR **#72984** ([link](https://github.com/openclaw/openclaw/pull/72984))（待合并）和 **#58823** ([link](https://github.com/openclaw/openclaw/pull/58823))（待合并）共同致力于修复子代理模型解析的优先级问题，确保全局默认设置能正确覆盖父代理的设置，这对于复杂的多代理部署意义重大。

## 社区热点

今日讨论最激烈的议题主要围绕**稳定性、安全性和核心功能表现**展开：

1.  **#25592 ([link](https://github.com/openclaw/openclaw/issues/25592)) - 工具调用间文本泄漏**：这个 P1 级安全议题获得了 27 条评论，社区反响强烈。用户报告智能体在调用工具之间产生的“内心独白”文本会意外泄漏到聊天渠道，这是一个严重的 UX 和隐私问题。该 Discussion 表明社区对 AI 行为透明度和可控性的高度关注。
2.  **#88312 ([link](https://github.com/openclaw/openclaw/issues/88312)) - Codex 端到端回复卡死回归**：这是一个 P1 级的回归问题，获得了 14 条评论。自 2026.5.27 版本后，Codex 应用服务器上的多步工具调用频繁失败，严重影响核心体验。社区对这类影响日常使用的稳定性回归问题反应非常敏感。
3.  **#29387 ([link](https://github.com/openclaw/openclaw/issues/29387)) - 代理目录引导文件被忽略**：这是一个长期存在的 P1 Bug，获得了 14 条评论。用户报告位于 `agentDir` 下的核心引导文件（如 `SOUL.md`）被静默忽略，导致复杂的多代理人格设定完全失效。这反映了用户对**高自由度、高定制性**的渴望与当前实现缺陷之间的矛盾。

## Bug 与稳定性

今日报告的 Bug 和回归问题主要集中在**安全突破、核心功能失效和配置错误**三个层面，按严重程度排列如下：

- **P0/安全风险：**
    - **#91283 ([link](https://github.com/openclaw/openclaw/issues/91283))** - **`minSecurity` 逻辑倒置**：严重的安全缺陷，`minSecurity` 函数将 `full` 视为最高限制等级而非最低，导致安全设置完全失效。此问题今早才被报告，尚无修复 PR，需最高优先级处理。

- **P1/回归 & 严重 Bug：**
    - **#88312 ([link](https://github.com/openclaw/openclaw/issues/88312))** - **Codex 端到端回复卡死**：已影响用户使用的 P1 回归问题。维护者已确认是 #84076 问题的复现，需尽快定位 #85107 的修复方案是否被部分回滚。
    - **#90991 ([link](https://github.com/openclaw/openclaw/issues/90991))** - **Cron 触发污染全局运行时状态**：P1 级 Bug。Cron 任务执行后残留的运行时状态会导致后续所有业务请求过载失败。这是一个严重的影响系统可用性的问题。
    - **#90428 ([link](https://github.com/openclaw/openclaw/issues/90428))** - **WSL2 上 exec 工具触发网关崩溃**：P1 级回归问题。在 WSL2 + Node 24 环境下，使用 `exec` 工具会导致网关被 SIGTERM 重启，完全阻塞了工作流。
    - **#91212 ([link](https://github.com/openclaw/openclaw/issues/91212))** - **消息投递恢复失效**：网关重启后，待投递消息因通道连接未就绪导致恢复失败，造成消息静默丢失。P1 级影响用户体验的问题。

- **P1/P2 其他重要 Bug：**
    - **#90639 ([link](https://github.com/openclaw/openclaw/issues/90639))** - `safeguard` 压缩模式失效，导致长会话在 Slack 上无修复地崩溃。
    - **#87136 ([link](https://github.com/openclaw/openclaw/issues/87136))** - 绝对 Token 阈值在多模型切换下一个模型满而另一个模型爆的问题。
    - **#90212 (未在列表中，但相关)** - 消息投递恢复在通道连接前执行导致失败。

## 功能请求与路线图信号

今日的功能请求显示出社区对 **智能体编排、轻量化部署和运行时弹性** 的强烈需求：

- **智能体编排增强**：**#22358 ([link](https://github.com/openclaw/openclaw/issues/22358))** 请求为子代理添加完成后的扩展钩子（post-subagent hook），用于自动生成轨迹文件。**#90916 ([link](https://github.com/openclaw/openclaw/issues/90916))** 提出了“主题会话族”概念，允许一个代理在不同命名上下文间隔离。结合已提交的 **PR #78441 ([link](https://github.com/openclaw/openclaw/pull/78441))** (子代理工具白名单转发)，可以预见下一版本将在子代理控制和隔离上有所突破。
- **轻量化部署**：**#86881 ([link](https://github.com/openclaw/openclaw/issues/86881))** 提议一个无需 AI 模型的“纯网关模式”，适用于仅需要调度和通道桥接的场景。这与 **PR #89712 ([link](https://github.com/openclaw/openclaw/pull/89712))** (cron 命令任务) 的思路上一致，都旨在降低资源消耗、提升部署灵活性。这是一个很强的路线图信号。
- **运行时质量与弹性**：**#90354 ([link](https://github.com/openclaw/openclaw/issues/90354))** 请求为预压缩内存刷新添加有界追加逻辑，防止数据损坏。**PR #91081 ([link](https://github.com/openclaw/openclaw/pull/91081))** (缓存 Session 文件列表) 则直接针对高负载下的性能瓶颈。这些信号表明项目正在从“功能堆砌”转向“精细化运维”。

## 用户反馈摘要

从今天的 Issues 评论中可以提炼出以下核心用户声音：

- **安全担忧与信任危机**：“内部处理输出泄漏到聊天频道” (#25592) 和“安全级别逻辑完全颠倒” (#91283) 让用户对平台的信任基础产生动摇。一位用户在 #25592 中评论：“This is more than a UX issue, it’s a data leak。”
- **对“回溯”的强烈不满**：多个回归问题（#88312, #31583, #90428）表明社区对“修了旧 Bug，引出新 Bug”的循环现象已感到失望。用户在 #88312 中形容：“This is the **third** time this specific class of stall has come back. Can we add a permanent regression test?”
- **对配置复杂性和不透明性的抱怨**：用户期待“开箱即用”的体验，但现实是代理目录文件被忽略 (#29387)、`exec` 工具不继承配置 (#31583)、`sandbox` 权限不准确 (#37634) 等问题反复出现。用户在 #31583 中评论：“I spent 3 hours debugging why my secrets weren't being injected. Again.”
- **对“文档”与“行为”不一致的困扰**：`minSecurity` (#91283) 和 `Deep Sleep` 报告写入逻辑 (#91299) 的问题表明，项目行为与文档描述的偏差正在增加，导致用户学习和诊断成本上升。

## 待处理积压

以下为长期未得到响应或解决方案，但对项目健康度构成严重威胁的关键议题和 PR，提醒维护者重点关注：

- **高优先级长期 Bug：**
    - **#25592 ([link](https://github.com/openclaw/openclaw/issues/25592))** (P1, 安全, 积压 3个月+)：工具调用间文本泄漏。虽已有标签 `needs-product-decision`，但旷日持久，属于安全红线问题。
    - **#29387 ([link](https://github.com/openclaw/openclaw/issues/29387))** (P1, 积压 3个月+)：`agentDir` 引导文件被忽略。这是社区中多代理/人格化需求的核心支柱，长期无法使用严重影响用户忠诚度。
    - **#31583 ([link](https://github.com/openclaw/openclaw/issues/31583))** (P1, 回归, 积压 3个月+)：`exec` 工具不继承特定技能的环境变量。对需要复杂编排的用户是致命伤。

- **等待合并或审核的重要 PR：**
    - **#72984 ([link](https://github.com/openclaw/openclaw/pull/72984))** (核心修复, 积压 1个月+)：子代理模型解析修复。该 PR 与 #58823 关联，是解决多代理模型混乱的关键。维护者已标记 `👀 ready for maintainer look`。
    - **#88212 ([link](https://github.com/openclaw/openclaw/pull/88212))** (功能推进, 积压 9天)：自动修剪小型本地模型的工具列表。对于资源有限的本地部署场景至关重要。
    - **#89712 ([link](https://github.com/openclaw/openclaw/pull/89712))**

---

## 横向生态对比

好的，以下是根据您提供的各项目日报生成的横向对比分析报告。

---

# 个人 AI 助手开源生态横向分析报告 | 2026-06-08

## 1. 生态全景

2026年6月8日，个人AI助手与自主智能体开源生态呈现出**高速分化与集中攻坚**的双重态势。头部项目（OpenClaw、Hermes、ZeroClaw、IronClaw）日处理Issue/PR总量均超过50条，社区贡献热情高涨，但代码审核瓶颈和回归问题频发成为普遍痛点。技术方向上，**Agent-to-Agent（A2A）协议**、**多渠道集成（如飞书、企业微信）**、**沙箱安全加固**成为跨项目共同焦点。与此同时，多个项目（如PicoClaw、NanoBot）开始从功能堆砌转向精细化运维，关注技术债务清理和文档质量，标志着生态正从“野蛮生长”向“工程成熟”过渡。

## 2. 各项目活跃度对比

| 项目 | Issues 日更新 | PR 日更新 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 295（新开/活跃180） | 500（待合并~330） | 无 | 高产出、高关注、高修复压力 |
| **Hermes Agent** | 50 | 50 | 无 | 极高活跃，A2A协议里程碑 |
| **ZeroClaw** | 50 | 50（合并12） | 无 | 极高活跃，TUI快速迭代 |
| **IronClaw** | 50 | 38 | 无 | 高度活跃，Reborn架构重写 |
| **PicoClaw** | ~20 | ~20（合并12） | Nightly | 高强度迭代与清理并行 |
| **CoPaw** | 18 | 8（合并3） | 无 | 高活跃，多渠道稳定性修复 |
| **NanoBot** | 未精确统计（2个新Issue关闭） | 4合并，15待合并 | 无 | 扎实进展，审查瓶颈 |
| **NanoClaw** | 2新开 | 3合并 | 无 | 快速迭代，安全关注 |
| **LobsterAI** | 15新开 | 2合并 | 无 | 社区驱动，开发积极回应 |
| **Moltis** | 1新开 | 3待合并 | 无 | 中等活跃，功能完善期 |
| **NullClaw / TinyClaw / ZeptoClaw** | 0 | 0 | 无 | 停滞 |

> 注：部分项目Issues/PR总数为日报描述值，非精确计数。

## 3. OpenClaw 在生态中的定位

OpenClaw 是生态中**规模最大、社区最活跃**的参照性项目，其日处理PR数（500条）远超其他项目（第二名仅50条），但**待合并比例高达2/3**，暴露出维护团队审查能力的瓶颈。技术路线方面，OpenClaw 侧重于**通用网关+多模型调度+丰富插件**，社区关注的Bug集中于安全逻辑倒置（`minSecurity`）、工具调用文本泄漏等核心稳定性问题。与同类相比：
- **优势**：社区基础庞大、功能覆盖面广（Slack/Telegram/WebChat等）、模型兼容性强。
- **劣势**：复杂配置导致用户信任危机，多个P1级Bug长期积压（如#25592安全泄漏已3个月），回归问题反复出现。
- **社区规模**：最大，但用户抱怨“修旧引新”现象较其他项目更突出。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **A2A（智能体间通信）协议** | Hermes Agent、ZeroClaw、IronClaw | 开放互操作，支持跨框架智能体发现与协作。Hermes已合并多个PR，ZeroClaw有高赞Feature Request。 |
| **沙箱/安全隔离** | NanoBot（Bwrap）、CoPaw（会话文件损坏）、OpenClaw（minSecurity） | 增强沙箱兼容性（Ubuntu 24.04）、防止文件泄露、修复安全逻辑倒置。 |
| **多渠道集成与稳定性** | PicoClaw（Matrix、Telegram）、CoPaw（元宝、企业微信）、ZeroClaw（飞书） | 修复平台特定Bug（@提及、消息类型、OAuth轮询），统一多端体验。 |
| **会话历史与状态管理** | NanoBot（修剪Bug）、Moltis（工具结果截断）、IronClaw（压缩保留） | 防止历史丢失、控制Token消耗、修复配置变更后状态不同步。 |
| **子代理/多代理控制** | OpenClaw（模型解析优先级）、NanoBot（spawn模型覆盖）、ZeroClaw（多代理路由） | 允许子代理使用不同模型、实现技能白名单转发、配置全局默认覆盖。 |
| **轻量化部署与可观察性** | OpenClaw（纯网关模式）、NanoBot（版本号显示）、PicoClaw（Termux指南） | 降低资源需求、提升运维可见性、简化新用户上手。 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型网关+多模型调度+丰富插件 | 高级开发者、管理多AI服务的团队 | 模块化微服务，强调可扩展性，但配置复杂度高 |
| **Hermes Agent** | A2A协议先锋、多智能体互操作 | 构建分布式AI系统的研究者 | 核心零代码插件方案，推动A2A标准化 |
| **ZeroClaw** | TUI（终端UI）优先，zerocode交互 | CLI爱好者、云原生开发者 | 以zerocode TUI为核心，消息队列和实时模型切换 |
| **IronClaw** | 企业级Reborn架构、配置即代码 | 企业运维、多租户场景 | 基于Reborn框架，强调安全防护（no-exposure）、产品工作流 |
| **PicoClaw** | 嵌入式/边缘部署，轻量可裁剪 | IoT、树莓派用户 | 用Go编写（推测），支持Termux，Nightly构建 |
| **CoPaw** | 阿里/企业生态集成（元宝、企业微信） | 国内企业用户 | 专注于国产生态API和Proto协议兼容性 |
| **NanoBot** | 多平台IM集成（飞书、钉钉、WhatsApp） | 跨平台办公用户 | 强大的通道适配层，Bwrap沙箱 |
| **NanoClaw** | 轻量化CLI+MCP工具，快速启动 | 个人开发者、实验者 | 启动安全机制，账号轮换 |
| **LobsterAI** | 教育协作、技能创作 | 教师、内容创作者 | 技能生成、记事本协作 |
| **Moltis** | 轻量功能、活动日志可见性 | 隐私敏感的中小团队 | 控制持久化、频道粒度权限 |

## 6. 社区热度与成熟度

- **第一梯队（极高活跃，快速迭代）**：**OpenClaw、Hermes Agent、ZeroClaw、IronClaw**。日均Issue/PR更新≥50，项目处于功能密集开发期，但面临回归问题和审核瓶颈。
- **第二梯队（高活跃，稳定性提升）**：**PicoClaw、CoPaw、NanoBot、NanoClaw**。日均更新10-40条，同时进行大量Bug修复和技术债务清理。
- **第三梯队（中等活跃，功能完善）**：**LobsterAI、Moltis**。日均更新≤20条，社区反馈积极但开发节奏较慢。
- **停滞梯队**：**NullClaw、TinyClaw、ZeptoClaw**。过去24小时无任何活动，可能处于维护或休眠状态。

**成熟度观察**：
- OpenClaw、ZeroClaw虽然活跃度高，但长期的P1级安全问题（OpenClaw #25592）和配置复杂度显示其**用户信任度尚未稳固**。
- 而NanoBot、Moltis虽规模较小，但Bug修复响应速度快（如NanoBot沙箱环境变量问题当天提交PR），社区满意度相对更高。

## 7. 值得关注的趋势信号

1. **安全从“可选项”升级为“生命线”**：多个项目暴露安全逻辑缺陷（OpenClaw的`minSecurity`倒置、NanoBot的Bwrap环境变量、ZeroClaw的Web Dashboard持续不可用）。这提示开发者：**安全测试不能成为功能开发的事后补充，而应内置在架构设计中**。未来AI Agent平台的安全审计（如SSRF防护、权限分离）将成为竞争核心。

2. **A2A协议进入工程落地期**：Hermes Agent将A2A整合为“零核心代码修改”的插件，ZeroClaw获得高赞支持，IronClaw的产品工作流也在向开放API演进。**跨Agent互操作不再是概念，而是被多个项目纳入路线图**。对开发者而言，投资支持A2A的框架将获得生态红利。

3. **“可观察性”从增值变为必备**：用户/运维者普遍要求版本号显示、会话统计、活动日志、配置变更审计。**部署后“黑箱运行”的模式正被抛弃**，开发者应在早期就设计好监控、日志和诊断接口。

4. **轻量化和边缘部署需求崛起**：PicoClaw的Termux官方指南、OpenClaw的“纯网关模式”请求、NanoClaw的快速启动，反映了用户希望**在低配设备或容器化环境下运行AI助手**。这表明市场正从“云端AI”向“终端AI”扩展。

5. **多平台集成从“能做”到“做稳”**：Flybook、钉钉、企业微信、Matrix等平台Bug集中涌现，说明单纯“支持”某一渠道已不够，用户要求**零瑕疵的适配（如@提及、消息类型识别、OAuth态保持）**。未来竞争会细化到每个平台的行为一致性。

6. **回归测试基础设施成为项目健康基石**：OpenClaw、ZeroClaw中多次“修旧引新”的现象，以及NanoBot长期未被合并的测试PR（#3982等），表明**缺乏自动化回归测试是导致稳定性恶化的根本原因**。建议所有活跃项目优先投资CI/CD和测试框架。

--- 

**总结**：2026年6月的AI Agent开源生态正处于“由量变到质变”的关键转折期。社区贡献热情极高，但项目维护者需要平衡功能速度与代码质量，尤其是在安全、可观察性和跨平台可靠性方面。A2A协议和轻量化部署是下一阶段最具潜力的技术方向。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据您提供的NanoBot GitHub数据，生成了2026年6月8日的项目动态日报。报告严格遵循您的要求，力求客观、专业、数据驱动。

---

### NanoBot 项目动态日报 | 2026-06-08

#### 1. 今日速览
今日项目活跃度极高，开发活动密集。PR合并/关闭数量（4个）与Issue关闭数量（2个）表明社区修复和功能实施的节奏加快。值得注意的是，社区对沙箱（Bwrap）安全性和兼容性的讨论显著增多，同时一项关于推理内容处理的关键Bug得以修复。总体来看，项目在稳定性和功能扩展方面都取得了扎实进展，但积压的待合并PR（15个）数量较多，提示维护团队可能需要加速审查流程。

#### 2. 版本发布
无新版本发布。

#### 3. 项目进展
今日有4个Pull Request被合并或关闭，标志着平台兼容性、核心功能修复和用户体验的改进。主要进展包括：

- **推理内容修复（#4227）**：合并了PR #4227，该PR修复了一个影响所有自定义提供商（如DeepSeek，Kimi）的关键问题。此前，当模型返回空字符串 `""` 作为 `reasoning_content` 时，系统会错误地将其转换为 `None`，导致后续处理（如工具调用）失败。现在该字段得以保持原样，避免信息丢失。
- **飞书/钉钉/WhatsApp 集成增强（#2885, #2663, #4206）**：PR #2885 和 #2663 被合并，分别解决了飞书通道的@提及解析问题，以及WhatsApp在群聊中处理特定格式用户ID（LID）的提及检测。同时，新的PR #4206 为钉钉通道增加了群聊白名单功能。
- **WebUI 功能增强（#4240, #4235）**：PR #4240（已合并）为WebUI中的代码块增加了ANSI输出渲染支持，使终端输出的彩色化内容在UI中得以正确显示。新PR #4235 则向WebUI设置页面添加了版本号显示，提升用户便利性。

这些合并和关闭的PR显著推进了项目的**跨平台兼容性**（修复非OpenAI API兼容性问题）、**企业级功能**（钉钉群白名单）以及**用户界面体验**（ANSI渲染，版本显示）。

#### 4. 社区热点
今日社区讨论的焦点主要集中在Bug修复和系统稳定性上。

- **会话历史修剪Bug（#4203）**：[链接](https://github.com/HKUDS/nanobot/issues/4203)
  该Issue由用户 `huji820` 创建，详细描述了一个严重的逻辑缺陷：当消息序列中出现“孤立的工具结果”时，`find_legal_message_start`函数会错误地丢弃所有历史消息。此问题引发了开发者深度讨论（2条评论），并迅速得到了回应。关联的修复PR #4219 已处于开放状态。
- **长期遗留问题关闭（#2256）**：[链接](https://github.com/HKUDS/nanobot/issues/2256)
  一个自2026年3月19日提出的关于飞书话题群回复的Feature Request被关闭。虽然最终关闭，但4条评论展示了社区对平台特定功能需求的探索和讨论，体现了社区对不同场景下机器人行为的细致要求。

**诉求分析**：社区的讨论核心围绕着**数据安全**（#4203 避免历史消息丢失）和**平台功能完善**（#2256 适配飞书话题群特性）。这表明随着项目用户增多，对边缘场景的处理和健壮性要求正在提升。

#### 5. Bug 与稳定性
今日共报告了4个新的Bug，其中有2个已关联修复PR，项目稳定性面临沙箱兼容性的新挑战。

| 严重程度 | Issue | 摘要 | 修复PR | 状态 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [#4203](https://github.com/HKUDS/nanobot/issues/4203) | `find_legal_message_start`函数在有孤立工具结果时丢弃所有历史消息 | `#4219` (已开放) | 已定位，修复中 |
| **高** | [#4237](https://github.com/HKUDS/nanobot/issues/4237) | Bwrap沙箱未重置HOME环境变量，导致工具写入失败 | `#4239` (已开放) | 已定位，修复中 |
| **高** | [#4236](https://github.com/HKUDS/nanobot/issues/4236) | Bwrap沙箱在Ubuntu 24.04上因用户命名空间限制而启动失败 | 无 | 待定位 |
| **中** | [#4242](https://github.com/HKUDS/nanobot/issues/4242) | 禁用dream功能后，系统仍将全部聊天历史注入系统提示词 | 无 | 待定位 |
| **低** | [#4105](https://github.com/HKUDS/nanobot/issues/4105) | 自定义提供商中，空字符串的`reasoning_content`会被丢弃 (已关闭) | `#4227` (已合并) | 已修复 |

**分析**：今日报告的Bug主要集中在 **Bwrap沙箱** 的兼容性和行为上，分别涉及环境变量（#4237）和操作系统限制（#4236）。这提示项目在向更安全、更隔离的执行环境迁移时，需要更全面地考虑不同操作系统发行版的差异。此外，`dream`功能的配置逻辑Bug（#4242）也可能导致不必要的Token消耗和性能问题。

#### 6. 功能请求与路线图信号
今日的Feature Request显示出用户对**可观察性**、**子代理灵活性**和**沙箱功能扩展**的强烈需求。

- **显示版本号（#4233）**：用户 `viblo` 提议在WebUI中显式展示NanoBot版本，并建议提示新版本可用性。该请求非常合理且易于实现，关联PR #4235 已提交，**极有可能被纳入下一版本**。
- **子代理模型覆盖（#4231）**：用户 `jsapede` 请求为 `spawn` 工具增加 `model` 参数，允许子代理使用不同于主代理的模型。这是一个高级功能需求，可以提高任务分配的灵活性和成本效益。考虑到其复杂度，可能需要在后续大版本中实现。
- **MCP URL安全加固（#4123）**：PR #4123 提出了一个重要的安全增强，即对MCP (Model Context Protocol) 的URL进行SSRF（服务端请求伪造）防护检查。这与当前提升系统安全性的趋势一致，预计会优先审查并合并。

#### 7. 用户反馈摘要
- **痛点击中**：用户在 `#4203` 中明确指出了会话历史丢失的Bug，并将其追溯到代码的具体行和逻辑，体现了用户的高技术水平和对系统的深入了解。此类反馈对项目健壮性至关重要。
- **场景驱动**：用户 `primit1v0` 在 `#4237` 和 `#4236` 中报告了在Ubuntu 24.04上启用Bwrap沙箱时遇到的问题，这反映了真实的生产环境部署痛点，也是Linux发行版演进对安全软件提出的新挑战。
- **期望明确**：用户在 `#4233` 中的诉求非常直接——“知道版本”和“知道是否需要更新”，展现了普通用户和运维人员对软件可管理性的基本期望。

#### 8. 待处理积压
需要关注以下长期未响应或积压的重要议题：

- **长期待审功能PR（#2663）**：关于WhatsApp LID群提及的修复PR `#2663` 在4月提交，于今日才合并，历时超过两个月。这表明社区贡献的PR审查可能面临瓶颈，维护团队应考虑如何提高审查效率。
- **大规模测试基础设施PR（#3982, #4193）**：由开发者 `yu-xin-c` 提交的一系列测试框架PR（如 `#3982`, `#4193`, `#3983`）持续开放中。这些PR致力于为项目建立脚本化的测试和内存生命周期测试，是提升项目长期质量和可维护性的关键基础设施。项目维护者应优先关注并加速此类“地基”工作的合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报（2026-06-08）。

---

## Hermes Agent 项目日报 — 2026-06-08

### 1. 今日速览

Hermes Agent 项目今日保持极高的活跃度，社区讨论与代码提交都非常频繁。过去24小时内，项目共收到50条Issue和50条PR更新，但“新开/活跃”与“待合并”的数量偏高，反映出项目在快速演进的同时，也存在一定程度的积压。核心维护者 `teknium1` 集中提交了多项关键修复，特别是对A2A协议的最终整合。A2A（Agent-to-Agent）协议支持是今日的绝对焦点，其相关功能合并与持续讨论，标志着项目向更宏大的多智能体互操作生态迈出了重要一步。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日有多个高价值PR被合并或推进，整体项目在稳定性和功能完整性上均有显著提升。

- **A2A 协议里程碑达成**：PR #4135、#11025、#14559 等多个与A2A相关的PR最终被合并。维护者 `teknium1` 今日提交了PR #41711，旨在将A2A支持整合为一个零核心代码修改的统一插件，标志着A2A功能从分散的尝试走向了工程化的终极形态。
- **核心架构修复**：PR #41715 修复了会话范围的控制模型和推理参数在主题恢复和压缩后失效的Bug。PR #41708 修复了背景审查（background-review）分支导致会话ID冲突的问题。
- **稳定性提升**：多个针对特定平台和场景的Bug修复PR被提交，包括：修复终端工具中工作目录丢失导致的崩溃（#41706）、修复依赖项携带已知CVE的安全问题（#40176）、修复Windows平台下Gateway重启无法自动恢复的问题（#41662）。
- **社区贡献合并**：维护者 `teknium1` 提交了PR #41651，批量“抢救”并合并了社区贡献者 `@islam666` 的10项低风险Bug修复，有效吸纳了社群的力量。

### 4. 社区热点

- **🏆 最热门 Issue: #514 - A2A (Agent-to-Agent) 协议支持**
  - **链接**: [NousResearch/hermes-agent Issue #514](https://github.com/NousResearch/hermes-agent/issues/514)
  - **热度**: 20条评论，18个👍
  - **诉求分析**：该Issue不仅是今日，也是近期社区最关注的话题。讨论的核心是引入Google的A2A协议，以实现不同框架、不同厂商的智能体之间进行发现、通信和协作。用户不满足于当前仅限于Hermes内部的委托/子代理模式（`delegate_task`），渴望构建更加开放、灵活的多智能体网络。今天多个相关PR的合并，正是对社区这一强烈诉求的直接回应。

- **Issue #24114: Matrix 网关错误地将双人房间识别为私聊**
  - **链接**: [NousResearch/hermes-agent Issue #24114](https://github.com/NousResearch/hermes-agent/issues/24114)
  - **热度**: 2条评论，2个👍
  - **诉求分析**：该Bug影响Matrix平台的用户体验。用户期望在双人房间（非私聊）中使用需要“@提及”才能触发回复的功能，以及群组自动线程功能，但这些功能因房间被错误归类而失效。这反映了用户对精细、可控的平台权限和路由策略的需求。

- **Issue #40176: 依赖库携带已知CVE**
  - **链接**: [NousResearch/hermes-agent Issue #40176](https://github.com/NousResearch/hermes-agent/issues/40176)
  - **热度**: 2条评论
  - **诉求分析**：用户对软件供应链安全高度关注。该Issue指出了`urllib3`、`python-multipart`等多个核心依赖存在已知的、可被利用的漏洞。这不仅是Bug报告，更是对项目安全性承诺的检验。

- **Issue #39685: 小米API集成问题**
  - **链接**: [NousResearch/hermes-agent Issue #39685](https://github.com/NousResearch/hermes-agent/issues/39685)
  - **热度**: 2条评论
  - **诉求分析**：该Bug报告了与国产厂商（Xiaomi）API的集成问题，说明了Hermes Agent在适配不同商业模型API时遇到的现实挑战。用户期望多模态功能在各种模型下都能稳定工作。

### 5. Bug 与稳定性

今日报告的Bug数量较多，覆盖了从核心到边缘的多种场景。以下是按严重程度排列的关键问题：

- **P1 (严重)**
  - **[BUG] 会话压缩导致消息丢失** (Issue #34089)
    - *已经关闭*，表明问题已得到解决。这是一个关乎数据完整性的严重问题。
    - 链接: [NousResearch/hermes-agent Issue #34089](https://github.com/NousResearch/hermes-agent/issues/34089)

- **P2 (重要)**
  - **[BUG] Matrix网关错误分类双人房间** (Issue #24114)
    - *开放中*，影响核心聊天平台功能。
    - 链接: [NousResearch/hermes-agent Issue #24114](https://github.com/NousResearch/hermes-agent/issues/24114)
  - **[BUG] OpenAI Codex 重新认证循环** (Issue #6653)
    - *开放中*，影响特定配置下（本地模型与云端模型切换）的用户体验。
    - 链接: [NousResearch/hermes-agent Issue #6653](https://github.com/NousResearch/hermes-agent/issues/6653)
  - **[BUG] Gateway 在 MacOS 上闪退 / 与 launchctl 冲突** (Issue #41676)
    - *开放中*，新报告的Bug，影响macOS平台Gateway模式的稳定性。
    - 链接: [NousResearch/hermes-agent Issue #41676](https://github.com/NousResearch/hermes-agent/issues/41676)
  - **[BUG] Windows 平台 Gateway 崩溃后无法自动恢复** (Issue #41662)
    - *开放中*，新报告的Bug，影响Windows作为服务器环境的使用。
    - 链接: [NousResearch/hermes-agent Issue #41662](https://github.com/NousResearch/hermes-agent/issues/41662)
  - **[BUG] 依赖项存在已知CVE** (Issue #40176)
    - *开放中*，需尽快升级依赖以确保安全。
    - 链接: [NousResearch/hermes-agent Issue #40176](https://github.com/NousResearch/hermes-agent/issues/40176)

- **P3 (一般)**
  - **[BUG] 小米API视觉分析失败** (Issue #39685)
    - *开放中*。
    - 链接: [NousResearch/hermes-agent Issue #39685](https://github.com/NousResearch/hermes-agent/issues/39685)
  - **[BUG] 终端转义序列导致输出字符被截断** (Issue #40250)
    - *开放中*，影响CLI交互体验。
    - 链接: [NousResearch/hermes-agent Issue #40250](https://github.com/NousResearch/hermes-agent/issues/40250)
  - **[BUG] WhatsApp发送失败** (Issue #41660)
    - *开放中*，新报告的Bug，影响WhatsApp平台通信。
    - 链接: [NousResearch/hermes-agent Issue #41660](https://github.com/NousResearch/hermes-agent/issues/41660)

### 6. 功能请求与路线图信号

- **A2A 协议支持**：尽管已有多个PR被合并，但全新的PR #41711旨在提供一个“零核心编辑”的统一插件方案。这表明A2A支持将从“可用”迈向“工程化”，很可能在下一个版本中被正式纳入。
- **桌面端增强**：用户提出了多个针对桌面应用的细粒度功能请求，如**自动打开预览附件** (Issue #41702)、**渲染 YAML 元数据为表格** (Issue #41701) 以及**集成看板** (Issue #41222)。这些功能表明用户对桌面客户端的体验寄予厚望，希望其超越纯聊天界面，成为真正的生产力工具。特别是集成看板功能，若能实现，将极大增强多Agent工作流的可视化管理。
- **无缝文件上传**：报告 Gateway 模式无法附加本地文件的 Bug (Issue #41669) 可被视作一个强烈的功能信号：用户期望“桌面应用”和“Gateway模式”在文件处理体验上应该一致。

### 7. 用户反馈摘要

- **痛点与Bug**：
  - **数据库损坏**：用户 `baofuen` 报告了在看板（Kanban）功能中，当Gateway和Dashboard同时打开同一数据库时会因并发写入导致数据损坏。（Issue #33169）
  - **更新卡死**：来自macOS用户的反馈，执行 `hermes update` 命令在安装依赖时卡住，导致更新失败。（Issue #38974）
  - **终端体验差**：用户 `gustemax` 抱怨终端转义序列导致输出被截断，严重影响阅读体验。（Issue #40250）
  - **复杂配置困惑**：用户 `cdata` 报告Matrix网关对房间识别逻辑过于简单，导致复杂场景下配置预期与实际行为不符。（Issue #24114）

- **场景与诉求**：
  - **多Agent生产集群**：用户 `rightnourburge4648-maker` 描述了一个真实的“AI动漫制作工作室”场景，需要多个专业Agent协同工作。他们强烈需求一个稳定、高效的A2A通信渠道来表达复杂的编排需求。（Issue #25176）
  - **内存管理**：用户 `awitherow` 抱怨有界内存（Bounded Memory）模式频繁导致用户偏好等信息丢失，呼吁实现持久的、基于检索的用户记忆。（Issue #32064）
  - **安全保障**：用户 `zebadee2kk` 通过安全审计发现项目依赖存在CVE，体现了高技术水平用户对软件供应链安全的敏感性。（Issue #40176）

### 8. 待处理积压

- **热点Issue #514 (A2A协议)**：虽然其关联的几个PR已合并，但Issue本身仍**开放**。这表明社区的讨论和期待并未结束，开发者需关闭该Issue并发布公告，以明确A2A功能的现状和未来规划。
  - 链接: [NousResearch/hermes-agent Issue #514](https://github.com/NousResearch/hermes-agent/issues/514)
- **Issue #24114 (Matrix路由)**：这是一个影响特定用户群体的P1级Bug，且已开放近一个月。尽管难度可能不小，但需持续关注并投入资源修复。若无维护者认领，应明确说明当前进展和优先级。
  - 链接: [NousResearch/hermes-agent Issue #24114](https://github.com/NousResearch/hermes-agent/issues/24114)
- **Issue #40176 (CVE)**：安全性问题是定时炸弹。Issue已提出三天，但尚未有对应的修复PR关联。建议将依赖升级安排进短期迭代计划，避免风险累积。
  - 链接: [NousResearch/hermes-agent Issue #40176](https://github.com/NousResearch/hermes-agent/issues/40176)
- **Issue #41662 (Windows Gateway崩溃)**：新报告的Windows平台严重问题，目前没有维护者回应。考虑到跨平台支持的广度，应尽快进行问题定位并给出初步响应。
  - 链接: [NousResearch/hermes-agent Issue #41662](https://github.com/NousResearch/hermes-agent/issues/41662)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是为您生成的 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-06-08

## 1. 今日速览

今日项目活跃度极高，日处理 Issues 和 PR 总数超过 40 条，显示出社区和开发团队的高频互动。**1个 Nightly 版本**已发布，但并非稳定版。核心活动集中在修复稳定性与代码质量上，多名贡献者（如 `chengzhichao-xydt`）提交了多份针对**错误处理、类型断言**等技术债务的修复 PR，同时修复了 Matrix 用户 ID 解析、MCP 参数解析等具体 Bug。社区中也涌现了 Telegram 位置消息支持、Kagi 搜索集成等新功能请求与 PR。总体来看，项目处于**高强度迭代与清理并行**的健康状态。

## 2. 版本发布

- **nightly: Nightly Build (v0.2.9-nightly.20260608.875cf4a2)**
    - 这是一个自动化的 **Nightly 构建版本**，基于 `main` 分支。
    - **注意**: 该版本可能不稳定，仅用于测试。请谨慎在生产环境中使用。
    - **完整更新日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
    - 无破坏性变更或迁移说明。

## 3. 项目进展

今日有 **12 个 PR 被合并或关闭**，主要集中在**代码稳定性**和**配置修复**两大方面：

- **核心稳定性修复**：多项 PR 聚焦于强化代码健壮性，主要贡献来自 `chengzhichao-xydt`：
    - **[PR #3046](https://github.com/sipeed/picoclaw/pull/3046)**: 修复 Agent 启动信息中缺失的类型断言检查，防止潜在 panic。
    - **[PR #3042](https://github.com/sipeed/picoclaw/pull/3042)**: 修复 Evolution 模块中 `os.Getwd()` 错误被忽略的问题。
    - **[PR #3040](https://github.com/sipeed/picoclaw/pull/3040)**: 修复模型探测中的类型断言 panic 风险。
    - **[PR #3034](https://github.com/sipeed/picoclaw/pull/3034)**, **[PR #3035](https://github.com/sipeed/picoclaw/pull/3035)**, **[PR #3033](https://github.com/sipeed/picoclaw/pull/3033)**: 修复多处文件写入操作（如飞书资源下载、文件复制）后未检查 `Close()` 错误的问题，防止因磁盘满或 I/O 错误导致数据损坏。

- **配置与功能修复**：
    - **[PR #3036](https://github.com/sipeed/picoclaw/pull/3036)**: 修复了 Anthropic 默认模型 ID 错误（`claude-sonnet-4.6` 改为 `claude-sonnet-4-6`），解决了用户报告的新环境首次使用报错问题。
    - **[PR #2902](https://github.com/sipeed/picoclaw/pull/2902)**: (已合并) 添加了在 Android Termux 上运行 PicoClaw 的官方文档指南。
    - **[PR #2936](https://github.com/sipeed/picoclaw/pull/2936)**: (已合并) 技能系统现在可以跳过那些依赖的二进制文件未安装的技能，避免了在低配设备上因调用不存在的命令而报错。
    - **[PR #3037](https://github.com/sipeed/picoclaw/pull/3037)**: (已合并) 添加了原生 **Kagi 搜索**提供商，丰富了搜索能力。

## 4. 社区热点

- **[Issue #2674](https://github.com/sipeed/picoclaw/issues/2674)**: **Codex OAuth 返回空响应** (8 条评论 | 4 👍)
    - **背景**: 用户反馈在使用 ChatGPT 后端 (`chatgpt.com/backend-api/codex`) 的 OAuth 时，助手会返回空响应，提示“provider error or token limit”。
    - **分析**: 这是一个持续了较长时间的 Bug，至今仍在讨论。社区对该问题关注度高，期望项目能针对特定流式传输场景（`response.output_item.done`）做出适配，以兼容非 OpenAI 标准 API 的后端。

- **[Issue #286](https://github.com/sipeed/picoclaw/issues/286)**: **Android Termux 运行指南** (8 条评论 | 2 👍)
    - **背景**: 用户长期呼吁为 Termux 添加官方指南。
    - **现状**: 该 Issue 已关闭，因为对应的 **[PR #2902](https://github.com/sipeed/picoclaw/pull/2902)** 已于今日被合并，社区的长期诉求得到满足。

- **[Issue #3044](https://github.com/sipeed/picoclaw/issues/3044)**: **Matrix 用户 ID 含冒号导致 `allow_from` 失效** (新开)
    - **背景**: 用户反馈标准 Matrix 用户 ID （如 `@localpart:domain`）无法通过 `allow_from` 白名单验证。
    - **响应**: 该 Issue 被标记为 Bug 后，`chengzhichao-xydt` 迅速提交了修复 **[PR #3045](https://github.com/sipeed/picoclaw/pull/3045)**，展现了极高的响应速度。

## 5. Bug 与稳定性

今日报告了数个 Bug，均已被快速响应：

- **严重**:
    - **[Issue #3044](https://github.com/sipeed/picoclaw/issues/3044)**: Matrix 用户 ID 含冒号被 `allow_from` 拒绝。**已有修复 PR #3045**。
    - **[Issue #3041](https://github.com/sipeed/picoclaw/issues/3041)**: `mcp add` 命令解析全局标志失败（如 `--no-color`），导致参数被错误解析为位置参数。**已有修复 PR #3048**。
- **普通**:
    - **[Issue #3049](https://github.com/sipeed/picoclaw/issues/3049)**: Telegram 渠道完全忽略位置消息（`message.location`），导致无任何反应。
    - **[Issue #3039](https://github.com/sipeed/picoclaw/issues/3039)** & **[Issue #3038](https://github.com/sipeed/picoclaw/issues/3038)**: 用户重复提交了与 Issue #3044 相同的 Bug 报告，已被标记为 `PLEASE DELETE`，社区已明确方向。

## 6. 功能请求与路线图信号

- **新提供商请求**:
    - **[Issue #2978](https://github.com/sipeed/picoclaw/issues/2978)**: 用户请求集成 **OmniRoute** 作为新的模型提供商。
    - **[PR #3037](https://github.com/sipeed/picoclaw/pull/3037)**: **Kagi 搜索**已被成功合并为原生提供商，这是一个强烈的信号，表明项目正在积极吸纳社区对更多服务商的需求。

- **用户体验相关**:
    - **[Issue #2952](https://github.com/sipeed/picoclaw/issues/2952)**: 中文用户“好久没发新版本了”的反馈，提出了 exec 命令问题、QQ 渠道重启问题以及对模型界面 UI/UX 的改进建议（如默认显示已有 key 的提供商、下拉选择、一键添加模型列表）。此 Issue 虽已关闭，但体现了用户对版本发布周期和易用性的关注。

## 7. 用户反馈摘要

- **痛点与抱怨**: 用户 `xhynice` 在 Issue #2952 中的反馈非常具体，提出了 `exec` 命令的**模型默认不带参数**、**QQ 渠道重启后错误重复执行**等实际使用中遇到的严重问题，并批评其“好像不太遵循 agent.md”，表明当前版本在基础功能可靠性上仍有提升空间。
- **成功案例**: 长期饱受 Matrix 白名单问题折磨的用户 `weissfl` 在提交 Bug 后，当天就获得了对应修复 PR，这极大地提升了用户对项目活跃度和维护者响应速度的信心。
- **呼声**: 社区（如 Issue #2834 和 #286）对于清晰、准确的**升级/运行指南**有持续的需求，特别是对于非标准平台（如 Termux）和首次使用的用户。

## 8. 待处理积压

- **[Issue #2978](https://github.com/sipeed/picoclaw/issues/2978)**: 请求添加 **OmniRoute** 提供商，已过去一周且无维护者回复，建议团队评估此请求的可行性并给予回应。
- **[PR #2904](https://github.com/sipeed/picoclaw/pull/2904)**: **修复 Agent 循环重载和 panic 清理稳定性**的 PR 已开放超过两周，并带有 `stale` 标签。该 PR 涉及核心模块的稳定性和资源释放，建议维护者审阅或发表意见。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 NanoClaw 项目的 AI 分析师，根据您提供的 GitHub 数据，我为您生成了 2026-06-08 的项目动态日报。

---

### NanoClaw 项目动态日报 | 2026-06-08

---

#### 1. 今日速览

今日项目活跃度极高，主要驱动力来自社区贡献者的高质量 Pull Requests。虽然过去 24 小时内没有新版本发布，但合并和待处理的 PR 多达 9 条，覆盖了 Bug 修复、功能增强、文档改进以及测试覆盖等多个方面。值得注意的是，新开的 2 个 Issues 揭示了两个关键问题：一个导致开发环境工作树永久“脏”的启动 Bug，以及一个潜在的严重安全权限漏洞。整体而言，项目正处于快速迭代和社区贡献的高峰期，代码质量和安全性是当前讨论的焦点。

#### 2. 版本发布

**无**。过去 24 小时内无新版本发布。

#### 3. 项目进展

今日共有 **3** 个 Pull Requests 被合并/关闭，对项目稳定性和功能集有显著推进：

- **[PR #2707] 启动安全机制**：由 `gavrielc` 贡献，该 PR 引入了一个启动“绊线”机制。未通过 `/setup` 或 `/update-nanoclaw` 等官方路径更新的部署（例如直接 `git pull` 跳过迁移）现在会启动失败，并显示清晰的自我修复指引。此举显著提升了部署的一致性和可靠性。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2707)

- **[PR #2706] 账号轮换修复与状态校准**：由 `tier2tech-tian` 贡献，修复了账号轮换逻辑中的关键问题。包括阻止 Codex/Gemini 模式误入 Anthropic 轮换、通过读取 OneCLI 实际状态来校准数据库游标、以及优化进程杀死逻辑。此修复增强了多 API 提供商场景下账号管理的稳定性和准确性。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2706)

- **[PR #2710] Ollama 文档改进**：由 `markbala` 贡献，新增了关于如何启用提示缓存的文档，解决了 Claude-Code-CLI 使用 Ollama 后端时速度慢的问题。改善了用户体验和文档质量。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2710)

#### 4. 社区热点

今日社区讨论的热点并非单一的 Issue 或 PR，而是围绕着一个核心议题展开：**权限与安全性**，同时也有关于长期待办功能的讨论。

1.  **[Issue #2711] 严重的权限安全漏洞**：`create_agent` MCP 工具被标记为“仅管理员”，但实际运行时未进行任何角色校验，任何容器都可以创建新的 agent 组。这是一个高优先级的权限提升漏洞，引发了广泛关注，虽然评论数不多，但其安全敏感性使其成为今日头号热点。
    [🔗 查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2711)

2.  **[PR #2531] 与 [PR #1626] 长期悬而未决的 PR**：这两个 PR 都获得了新的更新并再次进入公众视野。`#2531` 旨在解决 `send_message` 触发时的文本重复问题，`#1626` 则是一个期待已久的 Telegram 话题隔离功能。它们在沉寂一段时间后被重新激活，反映出社区对提升用户端体验和核心功能完整性的持续关注。
    - [🔗 查看 PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531)
    - [🔗 查看 PR #1626](https://github.com/nanocoai/nanoclaw/pull/1626)

#### 5. Bug 与稳定性

**高严重性**：
- **[Issue #2711] `create_agent` 权限绕过漏洞**：任何容器均可创建 agent 组，无视“仅管理员”的声明。**严重性：高**。目前尚无修复 PR。
  [🔗 查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2711)

**中严重性**：
- **[Issue #2312] 启动时无条件删除文件导致工作树“脏”**：`groups/global/CLAUDE.md` 文件被提交到仓库，但每次启动时又被删除，导致任何 `git pull` 并重启服务后的实例都会出现永久性工作树“脏”状态。**严重性：中**。影响开发者体验和自动化部署。目前尚无修复 PR。
  [🔗 查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2312)

**低严重性**：
- **[PR #2705] `use-native-credential-proxy` 技能失效**：该技能未能正确绕过 OneCLI 网关，存在功能退化和环境变量读取错误。已有修复 PR 提出。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2705)

#### 6. 功能请求与路线图信号

社区对项目功能拓展的热情很高，今日提交的功能请求和 PR 主要关注以下方向：

- **持久化与状态管理**：**[PR #2709]** 为 `ContainerConfig` 增加数据库支持的 `env` 和 `blocked_hosts` 字段，这是对配置持久化和动态管理能力的重要增强，可能纳入下一个版本。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2709)

- **核心功能完善**：**[PR #1626]** 的 Telegram 话题隔离功能，**[PR #2531]** 的文本重复修复，以及与 **[Issue #2706 中文 PR]** 相关的账号轮换改进，显示出社区对完善现有功能、提升用户体验的强烈需求。这些是项目走向成熟的关键一步。

- **测试与质量保障**：**[PR #2704]** 为 `cli-agent` 增加了单元测试，这是提升代码质量和防止回归的积极信号，表明社区和贡献者在关注项目的长期健康。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/2704)

#### 7. 用户反馈摘要

- **对文件管理的困惑**：Issue #2312 的作者抱怨，提交到仓库的 `CLAUDE.md` 文件被代码删除，导致 `git status` 始终显示为已修改。这反映了用户对项目构建和清理逻辑的不理解，也暴露了项目在启动流程设计上对开发者不友好的一面。
- **对安全机制的担忧**：Issue #2711 的提出者尖锐地指出了“声明与实现不符”的权限漏洞。这反映出核心用户对项目安全模型的关注，他们期望权限声明与实际执行逻辑保持一致，而不是一个“伪”安全功能。

#### 8. 待处理积压

- **[PR #1626] Telegram话题隔离功能**：自2026-04-04 提出以来，一直在等待进一步的审查或更新。这是一个被广泛期待的功能，长时间未合并可能会打击贡献者积极性。
  [🔗 查看 PR](https://github.com/nanocoai/nanoclaw/pull/1626)

- **[Issue #2312] 启动文件删除Bug**：自2026-05-06 创建以来，至今已一个多月未有修复 PR 或实质性进展，影响多位开发者的日常使用。
  [🔗 查看 Issue](https://github.com/nanocoai/nanoclaw/issues/2312)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是为您生成的 IronClaw 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-06-08

## 1. 今日速览

项目目前处于高度活跃的开发状态，社区贡献和核心开发活动都非常密集。过去24小时内，Issues 和 PR 的更新数量（50条和38条）均处于高位，显示出项目正处于大规模的功能迭代和架构演进阶段。当前开发的核心主题明确指向 **“Reborn”架构重写及产品化**，大量 Issue 和 PR 都围绕此展开，涉及工作流、安全、UI、集成等多个模块。虽然无新版本发布，但多个大型 PR 已被合并或正在推进中，项目正在从架构设计阶段稳步进入功能落地与系统稳定阶段。

## 2. 版本发布

无。

## 3. 项目进展

过去24小时内，项目完成了多项关键功能的落地与合并，主要集中于 **“Reborn”架构的产品化推进和安全加固**。

- **产品工作流（ProductWorkflow）细化**：PR [#4488](https://github.com/nearai/ironclaw/issues/4488)（现已关闭）成功将 `ProductWorkflow` 拆分为明确的提交/读取/订阅三个门面，这是实现开放API兼容性及后续#3280任务的关键一步。
- **结构化模型观测字段**：PR [#4530](https://github.com/nearai/ironclaw/pull/4530)（现已关闭）被合并，为工具调用结果增加了结构化、类型化的模型可见观测信息，替代了之前的纯文本 `LoopSafeSummary`，提升了模型对工具执行结果的理解能力。
- **扩展凭证暂存修复**：PR [#4492](https://github.com/nearai/ironclaw/pull/4492) 仍在开放中，但核心功能已实现。它修复了开发环境中扩展凭证的暂存问题，确保本地开发时能力调用的凭证立即可用，并重构了相关代码模块，提升了可维护性。
- **Slack集成主体功能完成**：PR [#4463](https://github.com/nearai/ironclaw/pull/4463)（现已关闭）完成了Slack host-beta模式下的持久化存储、会话恢复和即时消息推送，使Slack集成向生产就绪迈出重要一步。
- **出站偏好门面建立**：PR [#4511](https://github.com/nearai/ironclaw/pull/4511)（现已关闭）为产品工作流增加了出站交付偏好合约的门面，为未来实现智能的出站消息路由能力奠定了基础。

## 4. 社区热点

过去24小时内，社区讨论热度最高的议题依旧集中在 **“Reborn”架构的具体实现和演进路径**上。

- **Issue #3280** ([链接](https://github.com/nearai/ironclaw/issues/3280))：关于“添加 ProductWorkflow 和 InboundTurnService”的讨论最为热烈（7条评论）。该 Issue 是整个 Reborn 产品工作流的核心，它定义了产品层面的适配器如何与底层 Reborn 服务交互。贡献者们正在围绕该接口的具体形状、与现有系统的集成方式以及安全边界进行深入探讨。这反映出社区对确立一个清晰、稳健的新架构核心模式的强烈关注。

- **Issue #3036** ([链接](https://github.com/nearai/ironclaw/issues/3036))：作为“配置即代码（Configuration-as-Code）”的史诗级 Issue，也保持了高关注度（5条评论，1个👍）。社区成员正在讨论如何通过声明式配置（如蓝图和用例编排）来管理复杂的租户设置，旨在替代当前零散的 `.env` 文件、JSON和运行时标志做法。这体现了社区对提升项目可运维性和标准化配置管理的迫切期望。

## 5. Bug 与稳定性

过去24小时内，未报告严重级别的崩溃或回归错误。当前的关键稳定性工作主要集中在 **“Reborn”架构的安全性保障** 上。

- **高优先级/高风险**：
    - **Issue #3032** ([链接](https://github.com/nearai/ironclaw/issues/3032))：为 Reborn 架构增加“无暴露（no-exposure）安全防护”，防止敏感数据在模型可见、传输、日志等边界泄露。这是一个生产环境就绪的阻塞性问题，目前仍在开放中，暂无对应的 fix PR。
    - **Issue #4042** ([链接](https://github.com/nearai/ironclaw/issues/4042))：关注于完善租户沙箱进程的能力，当前 Docker 沙箱功能有限，无法安全地支撑工作区交互等场景。这是影响沙箱安全性和功能完整性的关键问题。
    - **PR #4534** ([链接](https://github.com/nearai/ironclaw/pull/4534))：正在处理一个数据一致性 Bug，旨在确保在执行任务压缩（compaction）时，能够保留当前激活的任务状态，避免数据丢失。

## 6. 功能请求与路线图信号

从开放的 PR 和 Issue 中可以清晰地看到项目的短期路线图：

- **用户界面与体验增强（计划纳入下个版本）**：
    - **技能管理**：PR [#4527](https://github.com/nearai/ironclaw/pull/4527) 尝试添加用户级别的技能管理用户界面，允许用户查看、编辑和管理自己的技能，这将是 WebUI 走向成熟的标志性功能。
    - **渐进式技能披露**：PR [#4531](https://github.com/nearai/ironclaw/pull/4531) 为技能引入了“可发现”和“已加载”的状态区分，能更好管理技能上下文，提升模型的使用效率。
    - **Slack 频道选择器**：PR [#4532](https://github.com/nearai/ironclaw/pull/4532)（现已关闭）为 Slack 集成增加了管理端频道选择器，完善了多租户场景下的频道控制。
- **长期规划**：
    - **配置即代码（Issue #3036）** 作为史诗级 Issue，虽然短期内不会被完全实现，但其讨论热度表明这是一个社区强烈需求的方向，可能作为后续重大版本的核心特性。
    - **WebUI Beta 发布路径（Issue #3607）** 被明确标记为路线图跟踪问题，并计划以 WebUI 作为 Reborn 架构的第一个 Beta 发布产品。

## 7. 用户反馈摘要

从 Issues 的评论中可以提炼出一些用户关注点：

- **痛点**：用户（开发者/运维者）明确表示对当前零散的配置方式（`.env`、JSON、运行时标志）感到困扰，缺乏标准的模式、审计和变更追踪（Issue #3036）。这直接驱动了“配置即代码”的需求。
- **使用场景**：社区讨论和代码贡献高度集中于两个具体场景：
    1.  **本地开发体验**：通过 Issue #3044 和 PR #4517，社区希望简化本地开发者的配置和启动流程，例如通过 `ironclaw run local` 一键启动。
    2.  **外部应用集成**：大量的工作和讨论（如 Issue #3280, PR #4463, #4532）集中于如何更好地与外部平台（如 OpenAI API、Slack、Google Calendar/Gmail）交互，表明项目正将自身定位为 AI Agent 的多渠道交互中枢。

## 8. 待处理积压

以下是长期未关闭或响应的重要 Issue/PR，可能成为项目前进的拥堵点，建议维护者重点关注：

1.  **[Issue #3032] Reborn cutover blocker: add no-exposure safeguards** ([链接](https://github.com/nearai/ironclaw/issues/3032))
    - **状态**：从2026-04-28起开放，P0优先级，仍未关闭。
    - **影响**：作为生产环境就绪的阻塞性问题，它的长期开放可能会延迟整个“Reborn”架构的正式发布。

2.  **[Issue #3036] [EPIC] Configuration-as-Code for IronClaw Reborn** ([链接](https://github.com/nearai/ironclaw/issues/3036))
    - **状态**：从2026-04-28起开放，社区共识高，但进展缓慢。
    - **影响**：这是一个大型史诗级任务，需要明确的规划和里程碑。虽然目前还未阻碍主线开发，但长期悬而未决可能影响新用户的采用。

3.  **[PR #3708] release** ([链接](https://github.com/nearai/ironclaw/pull/3708))
    - **状态**：从2026-05-16起开放，一个包含多个包（含破坏性变更）的版本发布 PR，被暂停在三周前。
    - **影响**：该 PR 的停滞可能意味着一些旨在发布的破坏性变更或新功能因此被阻塞，影响了社区使用和下游依赖更新。

---

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 项目的开源项目分析师，我将根据您提供的 GitHub 数据生成一份结构清晰的 2026 年 6 月 8 日的项目动态日报。

---

### LobsterAI 项目动态日报

**日期**: 2026-06-08
**分析师**: AI 智能体

---

#### 1. 今日速览

今日项目活跃度较高，社区反馈踊跃，而开发团队则聚焦于稳定性与基础架构的修复。过去 24 小时内，社区提交了 15 条新 Issue，主要集中在 UI/UX 问题和功能请求上，表明用户群体正在增长且对产品有较高期待。与此同时，开发团队合并了 2 个重要的 PR，分别解决了 LLM 消息负载过大和配置模型迁移后的数据保留问题，显示了团队在优化性能和修复关键缺陷方面的持续投入。综合来看，项目处于 **“社区驱动反馈，开发团队积极回应”** 的健康发展状态。

#### 2. 版本发布

**无**。

#### 3. 项目进展

今日合并了 2 个 Pull Request，标志着项目在稳定性和代码健壮性上迈进了重要两步：

- **修复核心通信问题**: **[PR #2110](https://github.com/netease-youdao/LobsterAI/pull/2110)** 被合并。该 PR 针对 `cowork` 协作场景，修复了 OpenClaw 图像负载过大的问题。它通过在发送前检测过大的 `chat.send` 负载，防止了因数据包过大导致的网关错误，并优化了相关的错误提示。这对于确保多模态协作功能的稳定性至关重要。
- **修复配置迁移问题**: **[PR #2117](https://github.com/netease-youdao/LobsterAI/pull/2117)** 被合并。该 PR 修复了配置迁移后，用户之前删除的提供商模型（provider models）会意外恢复的问题。通过跟踪迁移版本，确保预设模型只注入一次，并保留了用户的删除操作，提升了用户体验和配置的可靠性。

#### 4. 社区热点

今日社区讨论最为热烈的 Issue 是 **#2121** `对一个现象的疑问（怀疑是bug）`：
- **链接**: [Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121)
- **热度**: 作为今日唯一新开的 Issue，且在无评论情况下迅速成为关注焦点。其标题和截图显示了真实用户的担忧。
- **诉求分析**: 用户“nbjoe”对聊天界面中出现的“重复输出文字”现象感到困惑，怀疑这会导致 Token 被大量浪费。这反映了用户对**Token 消耗透明度和输出质量**的密切关注。深层诉求是希望 LobsterAI 能提供更高效的对话机制，避免产生不必要的开销，并期望项目方能尽快定位问题并给出解决方案。

#### 5. Bug 与稳定性

今日活跃的 Issue 中，报告了大量用户界面和逻辑问题，按严重程度排序如下：

**严重 Bug (影响核心功能)**

1.  **技能生成阻塞无反馈**: **[Issue #1509](https://github.com/netease-youdao/LobsterAI/issues/1509)** (stale): 用户使用 `skill-creator` 技能时，文件生成过程长时间阻塞，无任何进度提示，且无法进行后续操作。**影响面广，用户核心任务的完成受阻。**
2.  **禁用技能后仍被调用**: **[Issue #1500](https://github.com/netease-youdao/LobsterAI/issues/1500)** (stale): 在技能管理器中禁用技能后，该技能ID仍保留在活跃状态（`activeSkillIds`）中，导致下次对话时仍被调用。**这是一个明显的状态管理逻辑 Bug。**
3.  **Agent 设置保存不同步**: **[Issue #1502](https://github.com/netease-youdao/LobsterAI/issues/1502)** (stale): 修改 Agent 的技能列表并保存后，当前会话的技能状态未立即同步，需要手动切换 Agent 才能生效。**破坏了配置的即时反馈，影响用户体验。**

**中等严重 Bug (影响特定功能)**

1.  **IM 机器人配置校验缺失**: **[Issue #1504](https://github.com/netease-youdao/LobsterAI/issues/1504)** (stale): popo IM 机器人的 AES Key 没有必填校验，可以保存空值，导致后续功能可能异常。
2.  **定时任务会话为空可提交**: **[Issue #1506](https://github.com/netease-youdao/LobsterAI/issues/1506)** (stale): 定时任务的 IM 通知频道设置中，即使在未选择有效会话的情况下也可提交，导致通知静默失败。
3.  **QQ Bot 白名单无法添加**: **[Issue #1512](https://github.com/netease-youdao/LobsterAI/issues/1512)** (stale): QQ 机器人白名单模式缺少添加群组的输入框，白名单功能完全不可用。
4.  **OAuth Token 静默丢失**: **[Issue #1516](https://github.com/netease-youdao/LobsterAI/issues/1516)** (stale): GitHub Copilot OAuth 认证时，如果在轮询期间关闭设置面板，后台轮询持续但 Token 会静默丢失。**这是一个可能引发用户不便的异步处理 Bug。**

**低严重/UI Bug**

- **[Issue #1513](https://github.com/netease-youdao/LobsterAI/issues/1513)** (stale): “声明条款”页面内容格式不统一，存在序号重复、括号不完整等问题。

**今日新增 Bug**

- **[Issue #2121](https://github.com/netease-youdao/LobsterAI/issues/2121)** (新): 用户发现对话中存在重复输出文字现象，担心消耗 Token，需项目组确认是否为 Bug。

#### 6. 功能请求与路线图信号

今日用户提出了多个功能改进请求，均为提升信息管理效率的典型需求，这些信号可能影响项目的后续路线图：

- **会话管理增强**: 用户连续提出了**会话颜色标注 (Issue #1525)、批量导出 (Issue #1528)、标签分类与筛选 (Issue #1541)** 以及**消息收藏/书签 (Issue #1537)** 等四项功能。这表明随着用户会话数量的增加，对会话进行**组织、管理和快速检索**的需求变得非常迫切。这些功能是 LobsterAI 从“可用”走向“好用”的关键。
- **本地数据看板**: **[Issue #1532](https://github.com/netease-youdao/LobsterAI/issues/1532)** 请求在设置页面增加本地使用统计面板（总会话数、消息数等），反映了用户希望量化自身使用行为的需求。

结合已合并的 PR，目前项目的开发重点似乎仍在基础架构和稳定性修复上。上述功能请求（特别是会话管理类）若无对应的 PR 或 Milestone，很可能属于 **“社区呼声高，但排期未定”** 的状态，建议项目维护者注意收集并评估这些需求。

#### 7. 用户反馈摘要

- **痛点**:
    - **核心任务不可预测**: 用户 `jimmy-xz` (Issue #1509) 反馈在使用技能生成文件时，过程完全黑盒，无法感知进度，也无法正常进行下一步，导致工作中断。
    - **配置不一致**: 用户 `MaoQianTu` (多个 Issue) 发现多个配置保存不同步或校验缺失的问题，如禁用技能无效、Agent 技能列表保存不生效、定时任务配置静默失败，**削弱了用户对系统配置的信任**。
    - **额外成本担忧**: 用户 `nbjoe` (Issue #2121) 对对话中的重复输出表达了明确的“Token浪费”担忧，**这是一个直接关联到用户成本的负面体验**。
- **满意/期望**:
    - **竞品对比期望**: 用户 `jimmy-xz` (Issue #1509) 提到“同样的提示词给到Openclaw...就能很好的理解”，**暗示用户对 LobsterAI 的技能理解能力有更高期待**，并进行了竞品对比。
    - **功能升级呼声**: `MaoQianTu` 提出的一系列功能请求（颜色标注、批量导出、标签、消息收藏），代表了重度和高价值用户希望产品进化的明确方向。

#### 8. 待处理积压

今日无新发现的长期未响应 Issue，但以下之前报告的 Bug 均为 2026 年 4 月创建，至今超过 2 个月，且目前状态仍为 `OPEN` 和 `[stale]`（标记为陈旧），需要维护者重点关注和评估。这些 Issue 都属于比较影响体验的中等严重 Bug。

- **[Issue #1500](https://github.com/netease-youdao/LobsterAI/issues/1500)**: 禁用技能后仍被调用。
- **[Issue #1502](https://github.com/netease-youdao/LobsterAI/issues/1502)**: Agent 技能列表保存不同步。
- **[Issue #1504](https://github.com/netease-youdao/LobsterAI/issues/1504)**: popo 机器人 AES Key 未校验。
- **[Issue #1506](https://github.com/netease-youdao/LobsterAI/issues/1506)**: 定时任务空会话可提交。
- **[Issue #1516](https://github.com/netease-youdao/LobsterAI/issues/1516)**: Copilot OAuth Token 静默丢失。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 Moltis (github.com/moltis-org/moltis) GitHub 数据生成的 2026-06-08 项目动态日报。

---

### Moltis 项目日报 | 2026-06-08

#### 1. 今日速览

Moltis 项目今日活跃度中等，核心贡献者主要集中在 Pull Request 的最后冲刺和代码审查阶段，并无新版本发布。过去 24 小时内，项目新增了 1 个 Issues，同时有 3 个关键 PR 处于待合并状态。整体来看，项目处于功能完善和稳定性提升的密集开发期，特别集中在 Telegram 集成、会话历史管理以及用户控制权限等后端模块。没有报告新的严重 Bug，社区讨论相对平静，热点主要集中在移动端体验优化。

#### 2. 版本发布

无

#### 3. 项目进展

过去 24 小时内无 PR 被合并或关闭，但 3 个高质量 PR 正处于待合并状态，对项目核心功能有显著推进：

- **处理 Telegram 流式回复问题** ([PR #1113](https://github.com/moltis-org/moltis/pull/1113)): 这是一个重要的热修复，解决了当启用 Telegram 流式回复但关闭完成通知时，最终回答无法被正确显示的问题。这直接影响了 Telegram 用户的使用体验，修复后将确保流式输出的完整性。
- **控制工具结果持久化大小** ([PR #1089](https://github.com/moltis-org/moltis/pull/1089)): 该 PR 引入了一项关键优化，在将会话历史重新注入给 AI 提供商时，对 `tool` 和 `tool_result` 的内容进行截断 (capped)。此举旨在控制 token 消耗和内存占用，对于处理长对话的业务场景至关重要，是提升项目稳定性的基石。
- **增加频道活动日志可见性设置** ([PR #1093](https://github.com/moltis-org/moltis/pull/1093)): 该 PR 为用户提供了更精细的权限控制，允许按账户、频道甚至个体用户设置活动日志的可见性级别（全部、仅错误、关闭）。这是对项目可观察性和企业级部署支持的重要增强。

**总结**: 虽然今天没有代码合入，但上述 3 个 PR 代表了 Moltis 在**可靠性、资源效率和用户权限控制**三个方向上的明确进步，项目整体向更成熟、更健壮的方向迈进。

#### 4. 社区热点

今日社区讨论较为平静，无特别高活跃或争议性讨论。唯一活跃的 Issue #1107 反映了当前的核心用户需求：

- **[Feature Request] 移动端 Web UI 支持多行文本输入** ([Issue #1107](https://github.com/moltis-org/moltis/issues/1107)): 由用户 `IlyaBizyaev` 提出。虽然评论数不多，但其核心诉求——**移动端用户体验优化**，是 AI 聊天类应用的关键痛点。用户已在提交前搜索过现有请求，表明这是一个普遍且未满足的需求，当前移动端 UI 仍使用单行输入，导致长文本编辑体验极差。

#### 5. Bug 与稳定性

今日未报告新的 Bug 或崩溃问题。但需关注以下稳定性相关的待处理 PR：

| 严重程度 | 问题/PR | 分析 |
| :--- | :--- | :--- |
| **中等** | [PR #1113](https://github.com/moltis-org/moltis/pull/1113) (Hotfix) | **功能回归**: 该修复针对的是 `#1099` 提出的流式回复功能，在特定配置组合下出现的错误行为。这属于新功能引入的回归问题，但已被快速定位并提出了修复方案，表明项目响应及时。 |
| **低** | [PR #1089](https://github.com/moltis-org/moltis/pull/1089) | **稳定性优化**: 该 PR 并非修复 Bug，而是通过限制 `tool_result` 的持久化大小，预防性地解决了长对话中可能出现的 Token 超限或内存溢出问题。 |

#### 6. 功能请求与路线图信号

- **高潜力功能**: **移动端多行文本输入** ([Issue #1107](https://github.com/moltis-org/moltis/issues/1107)) 是提升 Web UI 可用性的核心功能，具有较强的用户呼声。项目应将其纳入短期路线图。目前尚无关联 PR，预计短期内会有社区或核心开发者响应。
- **已实现/待合并功能**: **频道活动日志可见性设置** ([PR #1093](https://github.com/moltis-org/moltis/pull/1093)) 是社区或开发者基于企业级用户需求提出的，该功能一旦合并，将显著增强项目的多用户、多频道的管理能力，符合 Moltis 向团队协作工具演进的方向。

#### 7. 用户反馈摘要

- **用户**: `IlyaBizyaev`
- **反馈场景**: 移动端 Web UI 下的聊天输入。
- **核心痛点**: 当前仅限于单行文本输入，在移动设备上难以编辑较长的提示词或进行复杂的文本修改，严重影响了移动端的使用体验。
- **期望**: 支持多行文本输入框，提供更好的文本编辑和浏览能力。
- **满意度**: 该用户明确表示这是一个未满足的需求，反映出对当前移动端输入体验的不满意。

#### 8. 待处理积压

以下是当前值得关注的长期未合并 PR，提醒维护者重点关注。

- **[PR #1089] Cap persisted tool results before rehydration** (创建于 6月1日，已 7 天无更新)
  - **链接**: https://github.com/moltis-org/moltis/pull/1089
  - **重要性**: **高**。该 PR 解决了工具调用结果可能占用大量 Token 的问题，对会话历史的处理性能有直接影响。长时间未合并可能导致后续提交产生合并冲突或增加审查难度。最后一次更新是添加了针对多种场景的适配，建议尽快完成 Code Review。
- **[PR #1093] Add channel activity log visibility settings** (创建于6月3日，已 5 天无更新)
  - **链接**: https://github.com/moltis-org/moltis/pull/1093
  - **重要性**: **中**。为项目引入了关键的审计和权限控制功能。此 PR 与 #1089 类似，涉及代码逻辑较多，且无评论，可能是等待主维护者的反馈或 CI/CD 验证。建议尽快合并或给出反馈，避免代码腐烂。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是为您生成的 CoPaw 项目 2026年6月8日 动态日报。

---

# CoPaw 项目动态日报 | 2026年6月8日

## 1. 今日速览

今日项目活跃度 **高**。24小时内共有 **18条** Issue 更新和 **8条** PR 更新，社区讨论和代码提交均十分活跃。关键动向包括：**元宝（Yuanbao）通道的多项兼容性 Bug 被快速修复和关闭**，显示出维护团队对渠道稳定性的重视；同时，社区对 **插件扩展基础设施** 的关注度很高，新提交的 PR (WIP) 与用户反馈的功能需求（如独立视觉模型、Shell交互）高度呼应，项目正从基础稳定性向架构扩展性迈进。`loop_config.json` 损坏导致 Agent 崩溃的 Bug 已有修复 PR，表明项目在健壮性方面也在持续改进。

## 2. 版本发布

**无**。今日无新版本发布。

## 3. 项目进展

今日项目在处理遗留 Bug 和推进新架构方面均有进展。主要贡献包括：

- **修复元宝（Yuanbao）通道关键连接问题**：PR [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) 和 [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) 已合并，分别修复了 `AuthBindRsp` 缺少 `connectId` 字段导致的连接跟踪失败，以及 `streaming_enabled=True` 时回复被静默丢弃的问题。这解决了元宝通道用户无法使用核心功能的问题。
- **修复 Protobuf 协议兼容性问题**：PR [#4981](https://github.com/agentscope-ai/QwenPaw/pull/4981) (已合并，引用于 Issue #4977 修复) 解决了新版 Protobuf 库不兼容旧版 `SerializeToString` 参数导致元宝通道启动失败的问题。
- **修复 Proto 文件缺失问题**：PR [#4981](https://github.com/agentscope-ai/QwenPaw/pull/4981) (已合并，引用于 Issue #4976 修复) 确保通过 pip 安装的 Wheel 包包含了元宝通道所必需的 Proto 定义文件。
- **修复渠道渲染器问题**：PR [#4995](https://github.com/agentscope-ai/QwenPaw/pull/4995) (由首次贡献者提交) 修复了在隐藏工具详细信息时，工具输出的附件和可见文本丢失的问题，提升了多渠道的交互体验。
- **提交关键 Bug 修复 PR**：PR [#5000](https://github.com/agentscope-ai/QwenPaw/pull/5000) 针对 Issue #4970（配置文件损坏导致 Agent崩溃）提交了修复，将 `_safe_json_loads` 提取为公共方法，防止单个文件损坏影响整个会话。

项目整体上修复了 **3个严重 Bug**，合并了 **3个关键 PR**，并在 **插件扩展基础设施** 上取得了初步进展。

## 4. 社区热点

今日社区讨论的重点集中于两个方向：**新架构的探索** 与 **渠道稳定性的修复**。

- **热点 PR：插件扩展基础设施**，PR [#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997) 和 [#4998](https://github.com/agentscope-ai/QwenPaw/pull/4998) 同时提交，虽然是 “Work In Progress”，但在开发者社区中引起了广泛关注。这表明社区对 QwenPaw 未来通过插件系统实现**功能解耦**和**高度可定制化**有强烈期待。
- **快速修复的 Bug 集群**：由用户 `ABAC-123456` 集中提交的关于 **元宝通道** 的一批 Issue ([#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976), [#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977), [#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978), [#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979), [#4980](https://github.com/agentscope-ai/QwenPaw/issues/4980)) 在一天内全部关闭，引发了用户对项目响应速度的好评。这些 Bug 的共同点在于 **Proto 文件打包、字段定义、序列化参数**等底层协议问题，暴露出渠道模块在标准化和测试覆盖上的不足，但也展示了项目组解决问题的高效。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在**多渠道兼容性**和 **Windows 平台** 问题，其中两个已有修复 PR。

| 严重程度 | Issue | 描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) | `loop_config.json`/`prd.json` 损坏导致整个 Agent 会话崩溃 | **已有修复 PR**: [#5000](https://github.com/agentscope-ai/QwenPaw/pull/5000) |
| **严重** | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | Windows 系统下，Session 文件 ID 重复拼接导致路径超限 | 待处理 |
| **高** | [#4990](https://github.com/agentscope-ai/QwenPaw/issues/4990) | 企业微信中，关闭工具调用信息会返回“无法回答”的错误提示 | 待处理 |
| **高** | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | v1.1.9 和 v1.1.10 版本连接本地部署的千问3.6-27B模型后无响应 | 待处理 |
| **中** | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | 图片预览放大后拖动时出现异常抖动 (macOS) | 待处理 |
| **中** | [#4587](https://github.com/agentscope-ai/QwenPaw/issues/4587) | QwenPaw 关闭后会残留后台进程 | 待处理 |
| **低** | [#4585](https://github.com/agentscope-ai/QwenPaw/issues/4585) | 自研插件工具在企业微信频道中无法被自动发现 | 待处理 |

## 6. 功能请求与路线图信号

今日用户提出的功能需求非常有前瞻性，与项目现有 PR 方向一致。

- **独立视觉模型配置**: [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) 提出为主模型不支持多模态时提供视觉模型回退方案。这与主模型解耦的“插件化”思路相符，很可能通过未来的插件基础设施实现。
- **会话按标题筛选**: [#4999](https://github.com/agentscope-ai/QwenPaw/issues/4999) 提出的 UI 优化需求，属于易用性改进，可能在后续版本中被采纳。
- **记忆系统自进化**: [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994) 用户希望记忆系统能像主流 Agent 框架一样具备分层学习和进化能力，这指向了未来长期的重要路线图。
- **Shell 命令实时交互**: [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) 和 **审批命令换行**: [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) 反映了用户对 **开发/运维类 Agent** 的使用场景需求，强调实时反馈和良好的交互体验。

**路线图信号**：今日提交的 **插件扩展基础设施** PR ([#4997](https://github.com/agentscope-ai/QwenPaw/pull/4997), [#4998](https://github.com/agentscope-ai/QwenPaw/pull/4998)) 是强有力的路线图信号，表明项目正在向 **插件化架构** 升级。这有望系统性地解决上述功能请求，例如独立视觉模型、Shell交互增强等功能都可以通过插件来实现。

## 7. 用户反馈摘要

从今日的 Issues 和 PR 中，可以提炼出以下用户痛点和使用场景：

- **企业用户的多渠道痛点**：用户 `DrewZt` 和 `shanghai-Jerry` 分别反馈了企业微信渠道的工具调用信息显示错误和插件不被发现的问题。这表明企业微信是重要的使用场景，但体验仍需打磨。
- **版本升级的兼容性问题**：用户 `Cancerhzc` 反馈从 v1.1.5 升级到 v1.1.9/10 后，本地模型无法正常对话。这是一个典型的**回归问题**，提示维护者在发版前需要进行更全面的全流程回归测试，特别是针对自定义/本地模型部署方案。
- **开发者对新架构的期待**：多位用户（`rescodexa`, `rescodexx`, `lecheng2018`）提出的功能需求（记忆系统、Shell交互、视觉模型）都指向了对更强大、更灵活的 Agent 能力的向往。他们对 `AgentScope` 社区中的主流方案（如分层记忆、类似Cursor/WorkBuddy的交互）很熟悉，并希望 QwenPaw 能快速跟进。
- **强大的个人贡献者**：用户 `ABAC-123456` 连续提交多个关于元宝通道的、难度较高的底层协议问题，表现了极强的专业能力和贡献意愿，是社区中宝贵的诊断力量。

## 8. 待处理积压

- **长期未响应的 Issue**：
  - [#4585](https://github.com/agentscope-ai/QwenPaw/issues/4585): 关于自研插件在企业微信频道中不工作的问题，创建至今已超过两周，尽管标记为开放，但需关注后续进展。
  - [#4587](https://github.com/agentscope-ai/QwenPaw/issues/4587): 进程残留问题，同样创建超过两周，属于稳定性问题，建议优先级提升。

- **待审核的重要 PR**：
  - [#4949](https://github.com/agentscope-ai/QwenPaw/pull/4949): 扩展 ACP 协议以支持元数据广告，已处于“Under Review”状态较长时间（自6月3日），建议维护者尽快给予反馈或合并，以避免 CI 冲突或社区贡献者流失。
  - [#5000](https://github.com/agentscope-ai/QwenPaw/pull/5000): 针对严重崩溃 Bug 的修复，需要尽快评审和合并。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 ZeroClaw 项目数据，以下是 2026 年 6 月 8 日的项目动态日报。

---

## ZeroClaw 项目动态日报 | 2026-06-08

### 1. 今日速览

ZeroClaw 项目在**2026年6月8日**处于**极高活跃度**状态。过去 24 小时内，社区提交了 50 条 Issue 与 50 个 PR，其中 12 个 PR 已被合并或关闭，表明代码审查和合并流程运转高效。虽然无新版本发布，但多个大型功能 PR（如消息队列、模型切换、主题引擎）在昨日被合并，标志着用户交互体验（zerocode TUI）进入快速迭代期。Bug 修复方面，数个影响用户工作流的 S1 级问题已被解决，但“Web 仪表板不可用”等长期存在的回归问题仍需关注。整体上看，项目正积极吸纳社区贡献，向着 0.8.0 版本稳步推进。

### 2. 项目进展

本日项目前进了一大步，主要集中在 **zerocode TUI 用户体验**和**核心架构稳定性**的提升。

- **zerocode TUI 核心功能增强**：
    - **[merged] #7209 feat(zerocode): /model and /model-provider picker with live switching** 被合并。用户在会话中现在可以实时切换模型和提供商，无需重启或重配置，显著提升了交互灵活性。
    - **[merged] #7190 feat(zerocode): outbound message queue with sidebar and injection** 被合并。解决了之前模型响应时用户无法输入的问题，引入了外发消息队列，允许用户在 AI 回复的同时继续编辑和提交下一条消息。
    - **[merged] #7249 feat(zerocode): theme enhancements** 被合并。引入高级主题功能，包括颜色深度回退、预设、按代理覆盖和调色板，极大增强了 TUI 的视觉定制能力。

- **配置与 Provider 架构优化**：
    - **[merged] #7178 feat(providers): per-alias model-provider fallback on failure** 被合并。重构了模型提供商的故障回退机制，允许用户为每个模型别名指定独立的回退链，提升了配置的精细度和系统的鲁棒性。
    - **[open] #7260 feat(providers): add 7 OpenAI-compatible providers** 仍在开发中，计划增加对更多 OpenAI 兼容提供商的支持，表明项目在扩展底层模型生态。

- **Gateway 与文档梳理**：
    - **[open] #7367 feat(gateway): route inbound webhooks per channel alias** 被提出。解决了多实例通道的 Webhook 路由问题，对多账号用户是重要改进。
    - **[open] #7365 docs(book): em-dash sweep, markdownlint fixes...** 展示了项目对文档质量的重视，正在进行大规模的文档清理和 CI 构建。

### 3. 社区热点

本日讨论热度集中在**核心功能缺失**与**未来架构愿景**上。

- **#4866 [bug] Web dashboard is still not available**（评论 28，已关闭）
  - **链接**: [Issue #4866](https://github.com/zeroclaw-labs/zeroclaw/issues/4866)
  - 尽管已关闭，但该问题获得了高达 28 条评论，反映了“Web 仪表板不可用”是困扰大量用户的**长期和严重的问题**。其关闭可能意味着修复已合并，但用户社区的期待和挫败感非常强烈。

- **#4710 [Feature]: A better LOGO**（评论 11，👍 2）
  - **链接**: [Issue #4710](https://github.com/zeroclaw-labs/zeroclaw/issues/4710)
  - 社区对项目视觉形象的讨论持续活跃，体现用户对 ZeroClaw 品牌认同感的关切。

- **#5146 [Feature]: Token consumption minimization via skill compilation**（评论 9，👍 1）
  - **链接**: [Issue #5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146)
  - 此 Feature 请求旨在通过预编译技能来减少Token消耗。9条评论讨论了技术方案的可行性，反映了社区对**成本优化**和**性能提升**的核心诉求。

- **#3566 [Feature]: A2A Protocol Support**（评论 6，👍 7）
  - **链接**: [Issue #3566](https://github.com/zeroclaw-labs/zeroclaw/issues/3566)
  - 获 7 个👍，是社区反馈最积极的功能请求之一。社区高度渴望支持 Agent-to-Agent 协议，以实现 ZeroClaw 与外部 AI 代理的互联互通，构建更广泛的生态系统。

### 4. Bug 与稳定性

过去 24 小时内，修复了多个高优先级 Bug，但仍有新的问题暴露。

- **严重 (S0/S1) 级问题**:
    - **有待观察**: #4866 (Web Dashboard 不可用) 已关闭，但这是长期存在的 S1 级问题，需在新版本中验证修复是否彻底。
    - **已修复 (S1)**: #5803 ([Bug]: Fallback provider chain ignores config) 已关闭。修复了故障回滚链忽略配置文件，仅从环境变量获取凭证的关键 Bug。
    - **已修复 (S1)**: #5155 ([Bug]: Delegate agents ignore prompt_injection_mode) 已关闭。修复了代理委托时忽略技能注入模式的 Bug，该问题会显著增加 Token 消耗。
    - **当前活跃 (S1)**: #4879 ([Bug]: Gemini CLI OAuth is simply not working) 和 #4627 ([Bug]: file_write tool silently fails) 仍是开放威胁，分别阻挡了 Gemini 用户和文件写入功能，目前处于 `in-progress` 状态。

- **功能退化 (S2/S3) 级问题**:
    - #4880 ([Bug]: context_compression not triggered in daemon mode) 虽已关闭，但其修复结果需要跟踪。
    - #4873 ([Bug]: After integrating Feishu, only the LLM is called) 是特定的渠道集成（飞书）问题，影响用户体验。
    - #4721 ([Bug]: zeroclaw should log to stderr instead of stdout) 是一个小而影响范围广的 UX 问题，社区持续有反馈。
    - **已修复 (S2)**: #4848 ([Bug]: MCP's not working) 和 #5122 ([Bug]: web_fetch allowed_private_hosts list) 均已关闭。

### 5. 功能请求与路线图信号

- **可能纳入 v0.8.0 的功能**:
    - **多代理路由 (#2767)** 与 **A2A 协议支持 (#3566)** 等高复杂度功能虽仍为开放状态，但已被接受 (status:accepted) 并加星，是 0.8.0 之后路线图上的重要候选。
    - **Token 消耗优化 (#5146)** 和 **Webhook 转换 (#2467)** 表明项目正在处理核心效率和集成扩展性问题。
    - **Provider 生态扩展**: PR #7260 (新增 7 个 OpenAI 兼容 Provider) 明确指向下一版本将覆盖更多模型提供商，是明确的路线图信号。

- **Zerocode TUI 的未来**: 昨日合并的一系列“大型”PR 表明，团队将 **zerocode TUI 作为下一阶段的核心交互模式**，功能快速迭代（实时模型切换、消息队列、主题引擎）显示了这一趋势。PR #7346 (修复 `zeroclaw models list` 输出模型名) 和 #7366 (修复 mid-turn 输入) 等小修小补，也证明团队正在打磨 TUI 的细节体验。

### 6. 用户反馈摘要

从议题评论中提炼的核心用户痛点：

- **“长期 Bug”带来的挫败感**: Issue #4866（Web 仪表板不可用）持续数月，用户反复提及“超出预期”（exceeded expected behavior），体现了对长期未解决问题的失望。
- **“开箱即用”的障碍**: Issue #3642 (提供全功能 Docker 镜像) 和 #4848 (MCP 不工作) 反映了新用户上手门槛高的问题，特别是**非技术用户**被复杂配置所困扰。
- **配置的复杂性**: #5803 (回滚链忽略配置) 和 #4879 (Gemini OAuth) 表明用户在配置不同提供商时常遇到不直观或文档未覆盖的问题，他们**需要更可靠的配置逻辑和更清晰的错误提示**。
- **对不同聊天平台的支持**: #2503 (找不到 NapCat/OneBot频道) 和 #4873 (飞书集成问题) 显示用户强烈希望 ZeroClaw 能无缝接入他们日常使用的各种 IM 工具，这类**渠道兼容性请求**是社区的一大驱动力。
- **对性能的关切**: #5146 (Token最小化) 的提出，显示有经验的用户正在关注长链推理时的**成本与延迟**问题，期望有更高效的技能处理模式。

### 7. 待处理积压

以下为需要维护者重点关注或社区讨论停滞的重要 Issue：

- **#3642 [Feature]: Provide a “full” docker image**
  - 状态: **Open, Accepted**
  - **分析**: 该议题创建于 2026-03-15，已积压近 3 个月。虽然被接受，但迟迟未进入开发。这是一个**高影响力的入门障碍问题**，建议优先排期。

- **#2767 [Feature]: Multi-Agent Routing**
  - 状态: **Open, Accepted**
  - **分析**: 作为一个获赞 9 次且标记为高风险的架构级功能，该议题自 2026-03-04 以来一直停滞。建议项目维护者在新路线图中明确其阶段或提供 RFC 草案。

- **#5127 [Feature]: bubblewrap sandbox: configurable writable paths**
  - 状态: **Open, Accepted**, 仅有 2 条评论。
  - **分析**: 这项安全特性讨论了数周，社区参与度较低。建议维护者主动发起讨论，以推进实现或澄清技术路径。

- **PR #7365 docs(book): em-dash sweep...**
  - 状态: **Open**, 作者明确标记为 **DO NOT MERGE (WIP)**。
  - **分析**: 这是一个大规模文档清理 PR，涉及 markdownlint 和文档 CI 的引入。虽然作者声明不要合并，但其进展直接影响项目文档质量，值得关注。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*