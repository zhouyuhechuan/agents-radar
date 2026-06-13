# OpenClaw 生态日报 2026-06-13

> Issues: 500 | PRs: 484 | 覆盖项目: 13 个 | 生成时间: 2026-06-13 02:42 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是基于 OpenClaw 项目数据生成的 2026-06-13 项目动态日报。

---

# OpenClaw 项目日报 2026-06-13

## 1. 今日速览

今日项目活跃度极高，社区参与热情不减。过去24小时内，有 **409 条新 Issues** 被创建或重新活跃，同时 **141 个 PRs** 被合并或关闭，显示了项目维护者较强的处理能力。两个版本 (`v2026.6.6` 和 `v2026.6.6-beta.2`) 的同时发布，核心聚焦于大规模安全边界收紧，但“一刀切”的策略也可能引入新的兼容性问题，需要用户密切关注。社区最关注的问题集中在 **内存泄露**、**消息丢失/重复** 和 **会话状态混乱** 等影响核心体验的稳定性 Bug 上。整体来看，项目处于快速迭代与强化安全的关键阶段，虽然修复活跃，但高优先级问题积压也较为严重。

## 2. 版本发布

- **[v2026.6.6 / v2026.6.6-beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.6.6)**: 同日发布了正式版和 Beta 版。
    - **核心变更**: 显著收紧了多处安全边界，涉及 **transcripts（对话记录）**、**sandbox binds（沙箱绑定）**、**host environment inheritance（主机环境继承）**、**MCP stdio（模型上下文协议标准输入输出）**、**Codex HTTP access（Codex HTTP访问）**、**native search policy（本地搜索策略）**、**elevated sender checks（权限提升发送者检查）**、**deleted-agent ACP bypasses（已删除代理ACP绕过）**、**loopback tools（环回工具）**、**Discord moderation（Discord审核）** 以及 **Teams group actions（Teams群组操作）** 等多个方面。
    - **破坏性变更/迁移注意事项**: 本次发布的 “exec” (执行) 相关安全策略变更尤为关键。用户在使用 `exec` 工具时，需要检查其技能条目 (`skills.entries.*.env`) 的环境变量继承、exec 审批路径等配置是否受到影响。任何依赖于旧有宽松安全策略的工作流（如跨沙箱数据传递、未授权的MCP stdio调用）可能会在新版本中失败。**强烈建议用户阅读完整的 Release Notes，并根据自身部署场景（特别是使用了 Discord、Teams、Sandbox 的用户）进行充分测试。**

## 3. 项目进展 (合并/关闭的 PR)

今日共有 **140 个 PRs** 被合并或关闭，显著推动了项目稳定性和功能完善。

- **稳定性与 Bug 修复**:
    - **[#92382](https://github.com/openclaw/openclaw/pull/92382)**: 修复了注册 `before_agent_finalize` 钩子后，Webchat 流式文本输出被延迟的问题，用户将获得更即时的反馈体验。
    - **[#92357](https://github.com/openclaw/openclaw/pull/92357)**: 修复了混合搜索（Hybrid Search）中，当关键词和向量搜索结果 ID 不重叠时，关键词结果被丢弃的 Bug，这对于使用 CJK（中文、日文、韩文）等语言进行搜索的用户至关重要。
    - **[#92308](https://github.com/openclaw/openclaw/pull/92308)**: 修复了在 Windows 系统上，QMD 命令中的绝对路径因反斜杠被当成转义字符而被错误处理的兼容性问题。
    - **[#92568](https://github.com/openclaw/openclaw/pull/92568)**: 修复了 `openclaw tasks cancel` 命令无法优雅中断正在运行的 Cron 任务的问题，提高了任务调度的可控性。

- **功能增强**:
    - **[#92319](https://github.com/openclaw/openclaw/pull/92319)**: 为 Workboard 插件增加了 `workboard_delete` 工具和 CLI 命令，现在用户和 Agent 都可以通过此命令删除卡片，补全了工作板的管理功能。
    - **[#92427](https://github.com/openclaw/openclaw/pull/92427)**: 将 Skill Workshop 工具中技能描述的字符限制从 160 提高到 500，提升了灵活性和开发者体验。

## 4. 社区热点

今日讨论最激烈的 Issues 集中在会话和消息处理的可靠性问题上：

- **[#25592](https://github.com/openclaw/openclaw/issues/25592)**: [评论 32] “工具调用间产生的文本泄露到消息通道”是高危的UX问题。用户抱怨 Agent 在处理工具时产生的内部处理信息、错误提示等被当作正常消息发送到 Slack、iMessage 等渠道，造成信息污染。社区核心诉求是区分“内部处理输出”与“最终用户消息”。
- **[#9443](https://github.com/openclaw/openclaw/issues/9443)**: [评论 25] “请求发布预构建 Android APK” 的呼声持续高涨，反映了移动端用户对便捷性的强烈需求。目前编译需要用户自行搭建环境，门槛较高。
- **[#91588](https://github.com/openclaw/openclaw/issues/91588)**: [评论 9] “严重：网关内存泄漏” 被标记为 **P0** 级别，社区对此问题反应强烈。用户报告进程的 RSS 内存占用在几天内从350MB飙升到15.5GB，最终被OOM Killer杀死，导致服务不稳定，这是当前最致命的稳定性问题之一。
- **[#32296](https://github.com/openclaw/openclaw/issues/32296)**: [评论 15] “Agent 回复错乱（Session Context Confusion）” 严重影响了对话体验。用户描述 Agent 经常回复上一条消息而不是当前消息，社区推测这与会话上下文管理机制在并发或快速消息场景下的竞态条件有关。

## 5. Bug 与稳定性

以下是按严重程度排列的关键 Bug：

- **[P0] [#91588](https://github.com/openclaw/openclaw/issues/91588)**: **致命内存泄漏**。RSS内存持续增长导致进程OOM崩溃。**尚无 PR**，维护者需立即介入。
- **[P0] [#91778](https://github.com/openclaw/openclaw/issues/91778)**: **`memory_search` 功能损坏**。自 v2026.6.1 版本后，向量搜索索引元数据丢失，导致所有Agent的记忆搜索功能瘫痪。**尚无 PR**。
- **[P1] [#32296](https://github.com/openclaw/openclaw/issues/32296)**: **会话上下文混乱**。Agent 回复错位，影响多轮对话核心体验。**尚无 PR**。
- **[P1] [#22676](https://github.com/openclaw/openclaw/issues/22676)**: **Signal 守护进程重启竞争条件**。SIGUSR1重启导致孤儿进程和消息发送失败，影响 Signal 渠道稳定性。**已有 [PR #92578](https://github.com/openclaw/openclaw/pull/92578) 等关联PR，但非直接修复**。
- **[P1] [#71491](https://github.com/openclaw/openclaw/issues/71491)**: **Kimi 模型 `reasoning_content` 回归**。长对话推理内容缺失，此问题在先前修复后又复发，表明问题未根除。

## 6. 功能请求与路线图信号

- **Agent 能力增强**:
    - **[#18160](https://github.com/openclaw/openclaw/issues/18160)**: 要求为 Cron 任务提供“直接执行模式”，以绕过LLM执行简单的命令行任务，提升效率和可靠性。该需求呼声较高（👍11），可能被纳入未来版本。
    - **[#22438](https://github.com/openclaw/openclaw/issues/22438)**: 提议“分层引导文件加载”以节省LLM上下文Token。这是一个降低使用成本的关键功能，对大型项目用户极具吸引力。
    - **[#27445](https://github.com/openclaw/openclaw/issues/27445)**: 希望子Agent完成通知能以“用户消息”形式路由到父会话，而非直接发送到消息通道，以实现更精细的多步工作流编排。

- **平台与集成**:
    - **[#9443](https://github.com/openclaw/openclaw/issues/9443)**: **请求发布Android APK**。该需求长期存在且呼声高（👍2），是打开移动端市场的关键一步。
    - **[#12602](https://github.com/openclaw/openclaw/issues/12602)**: **支持 Slack Block Kit**。让Agent能够发送更丰富的交互式消息（如按钮、选择器），提升在Slack中的实用性和用户体验。

- **安全与治理**:
    - **[#13583](https://github.com/openclaw/openclaw/issues/13583)**: 提议“预响应强制钩子”，确保在高风险场景（如金融交易）中，Agent在回应前必须调用特定工具，从机制上杜绝违规响应。

## 7. 用户反馈摘要

- **#9443** 中，用户 **AstridQing-AI** 指出，虽然有Android源码，但编译环境搭建复杂，对非开发者用户极不友好，强烈请求提供开箱即用的APK。
- **#25592** 中，用户 **doomclaw** 详细描述了工具调用间隙文本泄漏的场景，包括异常处理和日志等内部信息被“误发”到群聊中的尴尬和安全风险，反映出用户对Agent行为边界不清晰的困扰。
- **#32473** 中，用户 **RafaelLee** 在使用Hostinger VPS和Docker部署时，在配置Brave key后遇到 Control UI 要求 HTTPS 或 localhost 的问题，用户感觉困惑且难以解决，反映出文档和错误引导的不足。
- **#29387** 中，用户 **tuna-chin** 报告了Agent目录下的Bootstrap文件被“静默忽略”的Bug，即配置了 `agentDir` 后，放入该目录的SOUL.md等文件不生效，造成用户配置无反馈，体验较差。

## 8. 待处理积压

以下为长期未取得明显进展或仍需维护者关注的重要 Issue/PR：

- **长期缺失功能**:
    - **[#7707](https://github.com/openclaw/openclaw/issues/7707)**: [Feature: 按来源添加内存信任标签] (2026-02-03 创建，评论9) 用于防御记忆投毒攻击。此功能对于构建可信Agent记忆至关重要，但至今无PR。
    - **[#6615](https://github.com/openclaw/openclaw/issues/6615)**: [Feature:为 exec-approvals 添加拒绝列表支持] (2026-02-01 创建，评论7，👍7) 该功能允许“允许除了X之外的一切”策略，是现有白名单模型的重要补充，用户呼声很高但停滞已久。
    - **[#13610](https://github.com/openclaw/openclaw/issues/13610)**: [Feature:集成原生密钥管理（AWS Secrets Manager等）] (2026-02-10 创建，评论7) 是提升企业级安全性的关键需求，但长期未被规划。

- **长期未解决 Bug**:
    - **[#57326](https://github.com/openclaw/openclaw/issues/57326)**: [CLI 辅助路径绕过 CLI 调度] (2026-03-29 创建，安全影响) 部分 CLI 辅助路径仍绕过 `runCliAgent()`，存在安全隐患，但修复进度缓慢。
    - **[#74484](https://github.com/openclaw/openclaw/issues/74484)**: [Gateway 配对作用域死锁] (2026-04-29 创建) 此问题导致用户无法批准/拒绝某些修复请求，是一个令人沮丧的“卡住”场景，影响关键管理流程。

- **需要反馈或决策的项目**:
    - **大量**带有 `clawsweeper:needs-product-decision` 或 `clawsweeper:needs-maintainer-review` 标签的 Issues 正在等待产品决策或维护者审查，表明项目在处理海量社区反馈时，决策链条可能面临瓶颈。例如 [#18160](https://github.com/openclaw/openclaw/issues/18160)、 [#11665](https://github.com/openclaw/openclaw/issues/11665) 等。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已仔细审阅了上述 13 个项目的详细日报。以下是根据您的要求生成的横向对比分析报告。

---

### 个人 AI 助手/自主智能体开源生态横向对比分析报告 (2026-06-13)

#### 1. 生态全景

本日，个人 AI 助手开源生态呈现 **高度活跃、两极分化、快节奏迭代** 的特征。头部项目（如 OpenClaw, NanoClaw, IronClaw）在核心安全、会话稳定性、跨平台集成上进行了大量工程投入，但 “一刀切” 的安全策略和版本过渡期也引入了新的兼容性问题。大量项目共同聚焦于 **上下文管理（内存泄露/丢失）、工具调用可靠性、以及会话连续性** 这三大用户核心痛点。与此同时，社区对 **Agent 协作能力、本地化执行沙箱、以及更丰富的消息通道适配** 的需求在多个项目间涌现，成为下一阶段竞争的关键方向。整体来看，生态正从功能“可用”向体验“好用”与架构“健壮”过渡。

#### 2. 各项目活跃度对比

| 项目 | Issues (新开/活跃) | PRs (合并/关闭) | 版本发布 | 社区健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **409** | **141** | **2 (v2026.6.6 & beta.2)** | **高(快速迭代期)** |
| **NanoBot** | 3 | 9 | 无 | **高(功能拓展期)** |
| **Hermes Agent** | 50 | 5 | 无 | **高(高度活跃期)** |
| **PicoClaw** | 6 | 3 | 1 (Nightly) | **高(稳健发展期)** |
| **NanoClaw** | 5 | **10** | 无 | **极高(迅猛开发期)** |
| **NullClaw** | 1 | 0 | 无 | 中(修复配置期) |
| **IronClaw** | 大量 (具体数未给) | 约10 | 无 | **极高(深度打磨期)** |
| **LobsterAI** | 14 (新开) | 11 | 无 | **高(版本合并期)** |
| **Moltis** | 3 | 0 | 无 | 中(需求积累期) |
| **CoPaw** | 14 (新开) | 11 | 无 | **高(版本过渡期)** |
| **ZeroClaw** | 7 | 3 | 无 | **极高(架构重组期)** |

**活跃度解读**:
- **极高活跃（快速发展）**: OpenClaw, NanoClaw, IronClaw, ZeroClaw。这些项目拥有社区贡献者和核心开发者的密集投入，在大型架构变更和功能迭代上最为积极。
- **高活跃（并行推进）**: Hermes Agent, PicoClaw, LobsterAI, CoPaw, NanoBot。它们在bug修复和新功能引入上保持平衡，社区讨论活跃。
- **中活跃（需求响应中）**: Moltis, NullClaw。这两个项目社区有呼声，但维护者的响应或PR合并的速度相对较慢。

#### 3. OpenClaw 在生态中的定位

- **生态定位**：OpenClaw 是本生态当之无愧的 **“核心参照”和“功能集大成者”**。其社区规模、Issue/PR流量远超其他项目，是所有衍生项目（如 PicoClaw, NanoClaw）的 **上游和标杆**。
- **核心优势**：
    1.  **功能广度**：几乎覆盖了所有其他项目整合的功能点（MCP、Sandbox、Codex、Discord/Teams集成），是看齐行业最佳实践的模板。
    2.  **社区领导力**：`v2026.6.6` 版本的 “大规模安全边界收紧” 策略，直接影响了整个生态对安全的重视程度。
    3.  **开发马力**：单日 409条Issue和141个PR的处理量，彰显了其强大的社区贡献者和维护者团队。
- **技术路线差异**：
    - **“重安全” vs “灵活扩展”**: OpenClaw 本次版本的核心是“一刀切”式收紧安全边界，这提升了整体安全性，但也可能导致像 NanoClaw 等依赖其某些特性的下游项目出现兼容性问题，引发 “社区配置混乱” 的指责。相比之下，NanoBot 在审计模块上的引入则显得更模块化、可配置。
    - **“大而全” vs “小而美”**: OpenClaw 倾向于集成所有功能，而 Moltis 则更专注于 “K8s沙箱”、“本地STT” 等**特定垂直场景**的深度优化。

#### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **会话/消息可靠性** | OpenClaw, NanoBot, Hermes Agent, NanoClaw | **内存泄露**、**消息丢失/重复**、**会话上下文混淆**、**工具调用间隙文本泄露**是影响用户体验的**公敌**。所有活跃项目都在处理类似问题。 |
| **长期记忆管理** | OpenClaw, NanoBot, PicoClaw | 记忆搜索功能损坏、短期记忆丢失、上下文窗口被系统提示挤占。**如何高效管理Agent的记忆是限制其进行长对话的核心瓶颈。** |
| **Agent 协作/团队** | OpenClaw, LobsterAI, CoPaw | 用户希望Agent能组成团队处理复杂任务（条带/群组/Swarm），并有精细的跨Agent消息路由和任务编排。 |
| **安全与治理** | OpenClaw, IronClaw, NanoClaw, ZeroClaw | 从“安全边界收紧”到“审计模块”和“权限挂载”，项目都在加强安全防线，特别是应对LLM生成不可信代码和执行高风险操作。 |
| **跨平台/通道集成** | Hermes Agent, PicoClaw, CoPaw, ZeroClaw | 用户需求不再局限于单一IM（如Discord），正迅速扩展到**Signal、Telegram、Slack、飞书、微信、Twitch** 等，对适配器的丰富度和稳定性有很高要求。 |

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能旗舰，主推安全与扩展性 | 追求功能完整、高安全合规的企业及高级开发者 | 双版本发布策略，大型安全边界收紧，MCP/Codex集成标准制定者。 |
| **NanoBot** | 工具调用与可观测性 | 注重调试、成本和开发者体验的开发者 | 引入**审计模块(Audit)**，能清晰追踪Agent行为；修复了Cron任务子代理生命周期管理。 |
| **Hermes Agent** | 桌面端原生体验 | 重度桌面用户，追求流畅交互的macOS/Windows用户 | 专注**桌面GUI性能优化**（从28fps提升至56fps）、系统托盘、剪贴板加速等，是目前最注重“原生桌面应用感”的项目。 |
| **PicoClaw** | 轻量化衍生版 | 追求稳定、配置简洁开发者 | 重构了渠道标识，支持多实例复用提供者，是OpenClaw生态下注重稳定性的“轻量级”选择。 |
| **NanoClaw** | Signal通道集成专家 | 对Signal通道有强依赖的用户和开发者 | **最强的Signal支持深度**，包括双向附件、Reaction等，并将其与MCP工具和轮询稳定性深度打通。 |
| **Moltis** | 特定场景深度优化 | 企业/高级用户，关注本地化、安全执行 | 致力于**K8s原生沙箱** 和 **本地STT引擎集成**，走的是企业级、安全隔离的差异化路线。 |
| **IronClaw** | 架构设计先驱 | 核心开发者，关注底层架构设计 | 是**DeferredBusy架构**、**“始终允许”审批持久化**等设计模式的提出者和实践者，代表着该领域的架构演进方向。 |
| **ZeroClaw** | 架构重构与跨平台适配 | 对最新构建和macOS/Docker有高要求的开发者 | 正进行**核心引擎统一 (RFC #7415)** 和 **V3配置迁移**，专注于解决版本演进过程中的历史包袱和跨平台兼容性问题。 |

#### 6. 社区热度与成熟度

- **快速迭代与功能拓展期**: **OpenClaw, NanoClaw, Hermes Agent, ZeroClaw**。这些项目引入新功能（如Agent协作、计算机使用）的速度快，伴随大量Bug反馈和功能请求。社区以贡献者和早期采用者为主，活跃但稳定性波动大。
- **质量巩固与精品打磨期**: **NanoBot, PicoClaw, IronClaw, LobsterAI**。这些项目在确保核心功能稳定的基础上进行优化。它们更关注技术债务清除、测试覆盖率提升和架构抽象，如NanoBot的审计模块、IronClaw的测试回放机制。社区用户更资深，对产品质量要求更高。
- **需求积累与功能探索期**: **NullClaw, Moltis, CoPaw**。这些项目社区活跃度中等，有明确的需求萌芽（如K8s沙箱、Agent团队），但缺乏足够的开发马力或维护者响应来快速落地。

#### 7. 值得关注的趋势信号

1.  **从“被动响应”到“架构防御”的转变**: **IronClaw** 的 `DeferredBusy`机制和 **OpenClaw** 的“安全边界收紧”，已不再只是对Bug的修补，而是从架构设计层面去**预防**消息丢失、越权访问等系统性问题。这标志着生态开始成熟，走向更稳健的系统设计。

2.  **“Agent 可观测性”成为刚需**: **NanoBot** 的审计模块获得高度关注，验证了社区对**了解Agent“为什么这么做”** 的需求。随着Agent自主性增强，调试、审计、合规功能将是说服企业用户的关键因素。

3.  **Agent 记忆管理是下一个“军备竞赛”**: 几乎每个项目的日报都提到了**内存泄露、短期记忆丢失、上下文混乱**。谁能最先提供一个**高效、可靠、成本可控**的长期记忆方案，谁就能在“深度对话”和“持续性任务”的体验上拉开与竞争者的差距。

4.  **跨平台/服务集成不再是“锦上添花”，而是“生存必备”**: 多个项目同时收到对 **Slack、飞书、Signal、Telegram** 等通道的功能请求。未来的AI助手将是一个**无缝连接各种生产力工具和社交渠道的“信息中枢”**，集成深度是用户体验的核心决定因素。

5.  **“安全执行” 成为技术选型的关键分水岭**: **OpenClaw** 收紧安全边界，**ZeroClaw** 引入沙箱讨论，**Moltis** 则直接将K8s沙箱作为核心卖点。对于需要执行代码或访问系统资源的Agent，**安全抽象层（如沙箱、权限模型）的质量**将成为用户在部署时的重要考量，这或将成为新项目进入生态的“入场券”。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 | 2026-06-13

## 1. 今日速览

- 过去 24 小时项目保持活跃：3 个新 Issues 开启，3 个已关闭；29 个 PR 中有 9 个被合并/关闭，20 个仍在审查。
- 无新版本发布，但 PR 流水线密集，涉及 TTS 配置系统、WebUI 与 config.json 对齐、审计模块、光标单调性修复等关键改进。
- 社区关注点集中在短期记忆丢失（#4044）和对话上下文丢失（#4307）等稳定性问题，同时开发者正积极提交多项补丁。
- 项目整体健康度良好，功能推进与 bug 修复同步进行，但长期未合并的 PR（如 #3982、#3983 等）需引起维护团队注意。

## 2. 版本发布

无（今日无新版本发布）

## 3. 项目进展

以下 PR 已在过去 24 小时内被合并或关闭，代表项目的实质性推进：

| PR 编号 | 标题 | 说明 |
|--------|------|------|
| #4319 / #4318 | `feat(audit): Add tools.audit for agent action observability` | 新增审计模块，支持工具调用记录、作用域过滤和多种传输方式（loguru、HTTP webhook、JSONL 文件、回调），已集成到 AgentLoop 和 AgentRunSpec。 |
| #4304 | `fix(cron): wait for spawned subagents before marking cron job complete` | 修复 cron 作业在子代理未完成时就标记完成的问题，避免后台任务失控。 |
| #4203 | `[CLOSED] Bug: find_legal_message_start 丢弃所有消息` | 关闭了因孤立工具结果导致消息全部丢弃的 bug。 |
| #4006 | `[CLOSED] 对话历史中存在孤立 tool result` | 关闭了工具结果与 tool_calls 不匹配的校验问题。 |
| #4305 | `[CLOSED] [enhancement] Multiple custom providers` | 功能请求虽未直接合入代码，但关闭表明可能已通过其他方式解决或纳入规划。 |

**项目向前迈进**：
- 审计能力的初步落地使得代理行为的可观测性显著提升，便于调试与合规监控。
- 子代理生命周期管理修复减少了后台任务泄漏风险。
- 多个历史遗留 bug 被清理，增强了会话管理的鲁棒性。

## 4. 社区热点

本周最受关注的 Issues 按评论数排序：

1. **#4044 [OPEN] [bug] short term memory loss**（5 条评论）
   - 链接：https://github.com/HKUDS/nanobot/issues/4044
   - 核心诉求：用户反映 Nanobot 在对话中“失忆”，刚刚问过的问题下一轮就忘记。根因指向上下文窗口压力（SOUL.md、USER.md、MEMORY.md 等系统提示挤占可用 token），以及可能的上下文压缩逻辑缺陷。这是影响用户体验最直接的问题，讨论热度高。

2. **#4203 [CLOSED] Bug: find_legal_message_start 丢弃所有消息**（3 条评论）
   - 链接：https://github.com/HKUDS/nanobot/issues/4203
   - 用户报告了在特定消息序列下，所有历史消息被清空的严重 bug。已关闭，修复已合并。

3. **#4006 [CLOSED] 对话历史中存在孤立 tool result**（2 条评论）
   - 链接：https://github.com/HKUDS/nanobot/issues/4006
   - 反映 OpenAI/Anthropic 规范强制要求 tool call 与 tool result 配对，孤立结果会导致 API 拒绝请求。已关闭。

这些热点反映了用户对**对话连续性**和**工具调用规范性**的高度关注。

## 5. Bug 与稳定性

以下为过去 24 小时报告/活跃的 Bug，按严重程度排列：

| 严重性 | Issue | 描述 | 状态 | 是否有 Fix PR |
|--------|-------|------|------|---------------|
| 🔴 严重 | #4307 | **Post-turn consolidation 擦除代理自身消息**：当设置较小 `context_window_tokens`（如 40k）时，长轮次累积超过窗口后，合并归档会删除助手自己的交付消息，导致用户后续引用丢失。 | OPEN | 暂无对应 PR |
| 🔴 严重 | #4044 | **短期记忆丢失**：系统提示占用窗口，导致代理无法记住刚问的问题。 | OPEN | 无，但社区讨论活跃 |
| 🟡 中等 | #4309 | `/v1/chat/completions` 端点始终返回 `usage` 为 0（`prompt_tokens: 0, completion_tokens: 0`），尽管 agent loop 已跟踪真实用量。 | OPEN | 暂无 |
| 🟢 已修复 | #4203 | `find_legal_message_start` 导致所有消息被丢弃 | CLOSED | 已合并 |
| 🟢 已修复 | #4006 | 孤立 tool result 破坏 API 请求 | CLOSED | 已合并 |

**重点提示**：`#4307` 和 `#4044` 均涉及**上下文管理核心逻辑**，建议维护者优先排查，以免影响长期运行场景。

## 6. 功能请求与路线图信号

### 新提出需求

- **#4305 [CLOSED] Multiple custom providers**  
  用户需要同时配置多个“自定义”/“openai”类型 provider。提议在 Provider 配置中添加 `template` 参数选择内置实现。虽然已关闭，但可能已通过其他 PR 部分解决。

- **#4309 [OPEN] fix zero usage**（本质为 Bug，但也暴露了配置缺失）  
  提示 `usage` 统计未暴露，可能因配置未启用 token 计数。

### 已进入开发通道的功能

以下 PR 表明这些能力已被开发者采纳并进入开发阶段：

- **TTS 系统**（#4316）：支持 OpenAI、Groq (Orpheus)、ElevenLabs 等多 provider，配置通过 WebUI 和 config.json 持久化，已附带 agent 发现文档。
- **WebUI/config.json 对齐**（#4313）：补全了温度、工具限制、dream 通道、记忆等写入端点，消除 WebUI 与配置文件的差距。
- **Python SDK 扩展**（#4296）：为开发者提供更丰富的 `RunResult` 元数据，稳定的 session、memory、运行时接口。
- **审计模块**（#4320 改良版）：已被合并（#4319），未来可用于管控代理行为日志。

**路线图信号**：项目正朝向**多模态（TTS）、可观测性（Audit）、开发者体验（SDK）** 拓展，同时修复积累的稳定性 bug，整体处于功能快速迭代期。

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户痛点：

- **“我回答了问题，但代理根本不记得刚刚问过。”**  
  （#4044）用户对短期记忆丢失感到困惑，认为这是对话体验的最大瓶颈。建议增加上下文窗口管理策略的透明度。

- **“每次请求都返回零 token 用量，无法监控成本。”**  
  （#4309）服务部署者关注资源消耗，硬编码 zero usage 不符合生产环境要求。

- **“我需要两个不同的自定义 provider 来满足不同业务需求。”**  
  （#4305）用户希望在单一部署中灵活切换多个私有 LLM 服务。

- **“合并归档后我丢掉了刚才代理说的话，用户引用不了上一轮结果。”**  
  （#4307）高级用户通过长链推理后，发现归档逻辑反直觉地删除了有用信息，导致工作流断裂。

**满意点**：社区对修复 issue 的速度（#4203、#4006 快速关闭）表示认可，PR #4313 等让配置体验更一致也获得正面评价。

## 8. 待处理积压

以下为长期未得到响应或未合并的重要 Issue/PR，请维护团队关注：

| 类型 | 编号 | 标题 | 创建日期 | 备注 |
|------|------|------|----------|------|
| PR | #3982 | test: add scripted agent runner harness | 2026-05-24 | 已 20 天未合并，提供可重用测试框架，对回归测试很重要 |
| PR | #3983 | test: cover runner blocked tool-call finish reasons | 2026-05-24 | 同样超 20 天，增强对 provider 拒绝响应的测试 |
| PR | #4053 | fix(tools): keep read-only roots out of write paths | 2026-05-29 | 安全修复，阻止写工具继承只读路径，已 15 天 |
| PR | #4119 | fix(exec): block relative symlink workspace escapes | 2026-05-31 | 安全漏洞修复，阻止符号链接逃逸工作区，已 13 天 |
| PR | #4193 | test: add memory lifecycle harness | 2026-06-04 | 内存生命周期测试脚本，覆盖归档、持久化路径 |
| Issue | #4044 | short term memory loss | 2026-05-28 | 核心用户体验 bug，16 天未分配 |
| Issue | #4307 | post-turn consolidation wipes delivery message | 2026-06-12 | 新报告但影响严重，需尽快评估 |

**建议**：优先处理安全类 PR（#4053、#4119）和测试基础设施 PR（#3982、#3983），它们合并后可减少后续回归风险；同时成立专项小组解决 #4044 和 #4307 这两大上下文管理问题。

---

*日报生成截至 2026-06-13 17:00 UTC，数据源：HKUDS/nanobot GitHub 仓库。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-06-13

---

## 1. 今日速览

过去24小时内，Hermes Agent 项目保持了极高的社区活跃度：共处理 **50 条 Issues**（其中44条新开或活跃，6条关闭）和 **50 条 Pull Requests**（其中45条待合并，5条已合并/关闭）。无新版本发布。社区反馈集中在 **长响应截断 bug**（#7237）、**自定义端点兼容性问题**（#17199）以及 **MiniMax 提供商的 MCP 参数折叠 bug**（#44976）等核心功能痛点。同时，PR 方面有多项针对桌面端性能、状态修复和安全加固的提交，显示项目在稳定性和用户体验上持续迭代。整体衡量，项目处于 **高活跃度、快节奏迭代** 状态，但部分长期 issue（如 #7237 已于4月关闭，仍被讨论）反映出经典问题社区关注度持高不下。

---

## 2. 版本发布

**无新版本发布。**

---

## 3. 项目进展

今日共有 **5 个 PR 被合并或关闭**，其中关键进展如下：

- **#41757** [已关闭] feat(clipboard): 添加跨平台剪贴板文本写入与 PyObjC 图片粘贴加速。该 PR 为 macOS 用户提供了零子进程的剪贴板操作，减少终端闪烁。  
- **#45343** [已关闭] perf(desktop): 大幅降低 GUI 流式输出与交互延迟。通过六项针对性优化，将 879 条消息会话的标记流帧率从 28–38 fps 提升至 56 fps，阻塞时间从 2–5.2 秒降至几乎为零。  
- **#45347** [已关闭] fix: 修复 cron 回退继承、仓库脏标记误判、malformed 回退拒绝三个 bug，增强了定时任务系统的健壮性。  

此外，还有多个新 PR 被提交，涉及桌面文件树忽略显示开关、图像生成占位符主题适配、WeChat 适配器断开前清空获取数据等，表明项目在 **跨平台体验、桌面 GUI 和消息通道适配** 方面正在积极打磨。

> 关联链接：  
> - #41757 https://github.com/NousResearch/hermes-agent/pull/41757  
> - #45343 https://github.com/NousResearch/hermes-agent/pull/45343  
> - #45347 https://github.com/NousResearch/hermes-agent/pull/45347  

---

## 4. 社区热点

### 最活跃 Issue（评论数最高）

| Issue | 评论数 | 主题 |
|-------|--------|------|
| **#7237** [已关闭] | 41 | 长响应截断错误 `Response truncated due to output length limit` |
| **#17199** [开放] | 4 | deepseek 提供商：模型命名归一化与 base_url 覆盖破坏自定义端点 |
| **#44976** [开放] | 3 | MiniMax-M3 中嵌套单元素数组在 MCP 工具参数中被折叠为 `{"item":...}` |

**#7237 虽然已于4月关闭**，但仍有41条评论，说明该 Bug 影响面广、社区持续关注。用户反馈在 CLI 聊天和 Telegram/Discord/Slack 网关中频繁遇到输出截断，导致对话被中断。该问题可能涉及 token 预算与输出长度限制的设计权衡，修复方式未公开。

**#17199** 和 **#44976** 则反映了用户对 **自定义端点兼容性** 和 **新型模型提供商（MiniMax）** 的集成需求旺盛。后者尤其涉及 MCP（Model Context Protocol）的参数序列化错误，可能导致复杂工具调用结果异常。

> 关联链接：  
> - #7237 https://github.com/NousResearch/hermes-agent/issues/7237  
> - #17199 https://github.com/NousResearch/hermes-agent/issues/17199  
> - #44976 https://github.com/NousResearch/hermes-agent/issues/44976  

---

## 5. Bug 与稳定性

按严重程度排列（从高到低）：

| 严重性 | Issue | 描述 | 是否已有 Fix PR |
|--------|-------|------|----------------|
| **P1** | #38389 / #38391 / #38392 [已关闭] | 上下文压缩摘要以普通助手消息注入，污染可见对话 | 已关闭（重复） |
| **P1** | #44837 [已关闭] | Session DB 在修复消息序列后丢失助手消息 | 已关闭 |
| **P2** | #45129 [开放] | `docker_extra_args` 在网关中被忽略（`_terminal_env_map` 缺失） | 无 |
| **P2** | #45250 [开放] | Anthropic OAuth 登录因陈旧 token 端点失败（404） | 无 |
| **P2** | #45323 [开放] | Telegram 富文本表格被共享格式化器改写为 bullet | 无 |
| **P2** | #44763 [开放] | macOS `computer_use` 元素 bounds 始终为零，破坏空间定位 | **有 PR #45329** |
| **P2** | #44866 [开放] | MCP OAuth 探测失败时仍轮询30秒 | 无 |
| **P2** | #45258 [开放] | 网关日志目录权限问题导致后续配置失败 | **有 PR #45346** |
| **P3** | #45242 / #45241 [已关闭/开放] | MiniMax OAuth 用户辅助任务全部崩溃 | 无 |

**关键发现**：  
- #44763 的修复 PR #45329 已提交，将零坐标标记为“未知”而非静默返回零，提升 macOS 屏幕元素定位的透明度。  
- #45258 的修复 PR #45346 已提交，通过 `chown` 父目录解决权限问题。  
- **P2 级 issue 数量较多**，且多数无对应修复 PR，需维护团队重点关注，特别是 #45129（`docker_extra_args` 被忽略）和 #45250（Anthropic OAuth 404）直接影响用户部署和使用。

> 关联链接：  
> - #44763 https://github.com/NousResearch/hermes-agent/issues/44763  
> - #45329 https://github.com/NousResearch/hermes-agent/pull/45329  
> - #45258 https://github.com/NousResearch/hermes-agent/issues/45258  
> - #45346 https://github.com/NousResearch/hermes-agent/pull/45346  

---

## 6. 功能请求与路线图信号

以下功能请求获得了较多关注，且部分已有相关 PR 在开发中：

- **#41222** [P3] 请求将 Kanban 板集成到桌面应用，减少多终端切换。当前桌面端与看板分离，用户需打开独立 CLI 执行命令。该请求获得 2 条评论和 1 个 👍，如果实现将显著提升多 Agent 工作流的桌面体验。  
- **#44140** [P3] 桌面 GUI 改进：自动滚动、侧边栏重叠修复、自定义会话分组。获得 2 个 👍，反映了桌面端 UI 细节的普遍期望。  
- **#45355** (PR) 桌面文件树增加“显示/隐藏被忽略文件”切换按钮，解决 `.gitignore` 文件完全不可见的问题。该 PR 已提交，预计将进入下一个版本。  
- **#45348** (PR) 增加法语 (fr) 界面本地化，呼应社区多语言需求。  

**路线图信号**：  
- **Cross-platform session unification**（#45275）用户期望在桌面 App 和 Telegram 之间统一会话历史，虽未明确纳入路线图，但已是高频反馈主题。  
- **安全加固**：#42846 PR 增加向 LLM 提供商发送消息前的凭据隐去功能，#44743 PR 增加 SSRF 防护，显示项目正加强安全边界。  

> 关联链接：  
> - #41222 https://github.com/NousResearch/hermes-agent/issues/41222  
> - #44140 https://github.com/NousResearch/hermes-agent/issues/44140  
> - #45355 https://github.com/NousResearch/hermes-agent/pull/45355  
> - #45348 https://github.com/NousResearch/hermes-agent/pull/45348  

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实痛点与使用场景：

- **长响应截断**（#7237）：用户反复反馈 CLI 和网关消息被截断，严重影响多轮对话完整性。“每次生成长回复都被强行中断，无法继续对话。”  
- **自定义端点兼容性**（#17199）：用户配置深度求索提供商访问火山引擎 ARK 时，因模型名称归一化和 base_url 覆盖导致完全不可用。“两个 bug 让配置变得不可用。”  
- **MiniMax-M3 参数折叠**（#44976）：MCP 工具调用中嵌套单元素数组被错误转换为 `{"item": <element>}`，导致服务端无法解析。“深层次数组参数被压缩，破坏复杂工具调用。”  
- **桌面端闪退**（#45226）：Windows 用户反馈 `hermes desktop` 反复闪退，GPU 进程异常退出。该问题未收到维护者回复。  
- **Slack bot 消息丢失**（#30091）：即使配置 `allow_bots: all`，同一线程中的其他 bot 消息仍被静默丢弃，影响多 Agent 协作。  
- **Telegram 表格渲染**（#45323）：富文本表格在 Telegram 中被转换为无序列表，丧失原生表格显示效果。  

整体用户情绪：**对核心功能（长响应、自定义集成）的不稳定感到 frustration**，但对桌面端性能优化和新特性（如剪贴板加速）表示期待。部分 Bug 长期未修复（如 #30091 已存在近一个月）可能削弱用户信任。

---

## 8. 待处理积压

以下为长期未响应或延迟的重要 Issue/PR，建议维护团队重点关注：

| 编号 | 类型 | 描述 | 创建时间 | 最近更新 |
|------|------|------|----------|----------|
| **#17199** | Issue (P2) | deepseek 提供商模型归一化与 base_url 覆盖破坏自定义端点 | 2026-04-29 | 2026-06-13 |
| **#30091** | Issue (P2) | Slack bot 消息在共享线程中静默丢失 | 2026-05-21 | 2026-06-12 |
| **#16769** | PR (开放) | 添加 Nostr NIP-17 私有 DM 平台适配器 | 2026-04-28 | 2026-06-13 |
| **#36286** | PR (开放) | 添加 minimax-cn-oauth 中国区 OAuth 提供商 | 2026-06-01 | 2026-06-13 |
| **#42846** | PR (开放) | 凭据隐去（安全加固） | 2026-06-09 | 2026-06-13 |
| **#43277** | PR (开放) | 修复 codex 池回退解析器中冷却期未尊重问题 | 2026-06-10 | 2026-06-13 |

其中 #17199 和 #30091 均为 **P2 级别且超过一个月未获得根本修复**，直接影响 deepseek 用户和 Slack 集成场景的使用。PR #16769（Nostr 适配器）已等待近两个月无合并，可能因评审资源不足或优先级调整。建议维护者优先处理 #17199 和 #30091，并评估 #16769 的合并时机。

> 关联链接：  
> - #17199 https://github.com/NousResearch/hermes-agent/issues/17199  
> - #30091 https://github.com/NousResearch/hermes-agent/issues/30091  
> - #16769 https://github.com/NousResearch/hermes-agent/pull/16769  

---

*以上日报基于 2026-06-13 的公开数据自动生成，旨在为社区和团队提供决策参考。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-06-13

## 1. 今日速览

过去24小时内，PicoClaw 社区保持高度活跃：共处理 **6 条 Issue**（5 条新开/活跃、1 条已关闭）和 **14 条 Pull Request**（11 条待合并、3 条已合并/关闭），并发布了一个 **nightly 版本**。项目在协议完善、渠道适配、错误处理强化等方面有明确推进，但部分长期存在的 Issue 和 PR 仍处于积压状态。整体来看，项目健康度良好，开发节奏稳健。

## 2. 版本发布

- **Nightly Build v0.2.9-nightly.20260613.c362114c**  
  [GitHub Release](https://github.com/sipeed/picoclaw/releases/tag/v0.2.9)  
  此为自动化构建，可能不稳定。完整变更日志：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)。暂无破坏性变更或迁移注意事项。

## 3. 项目进展

今日共有 3 个 PR 被合并/关闭，主要聚焦于**渠道处理稳健性**与**工具调用错误处理**：

- **#2551** [CLOSED] `refactor: standardize channel identification and decouple name from provider type`  
  重构渠道标识，允许多实例复用同一提供者，已关闭（积压一个月后最终合入）。  
  [PR #2551](https://github.com/sipeed/picoclaw/pull/2551)

- **#3113** [CLOSED] `fix(channels): check json marshal/unmarshal errors in toChannelHashes`  
  修复渠道配置序列化时静默忽略错误的问题，提升配置一致性。  
  [PR #3113](https://github.com/sipeed/picoclaw/pull/3113)

- **#3112** [CLOSED] `fix(tools): handle json.Marshal error in toolloop tool call arguments`  
  修复工具调用参数序列化失败时数据丢失的隐患。  
  [PR #3112](https://github.com/sipeed/picoclaw/pull/3112)

此外，Issue **#3109**（Channel-level permission scoping）被关闭，表明该功能已完成设计与实现，将在后续版本中提供正式支持。

## 4. 社区热点

- **#2984** [OPEN] `Add explicit turn completion signal for Pico WebSocket clients`  
  👍: 2，评论: 2。该需求获得了较高关注。用户期望外部 WebSocket 客户端能明确知道 Agent 处理消息完成，以便进行后续操作。目前已有 PR #3116 实现 `turn.done` 生命周期信令，但 Issue 仍开放以跟踪剩余缺口。  
  [Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)

- **#3012** [OPEN] `Continuous consumption of tokens every minutes when evolution is enabled`  
  评论: 2，涉及 FreeBSD 环境下开启 Evolution 模式后每分钟持续消耗 Token 的严重 Bug，用户表示“Quick Summary”未提供完整日志但确认复现。当前无关联 Fix PR，社区讨论热度较高。  
  [Issue #3012](https://github.com/sipeed/picoclaw/issues/3012)

## 5. Bug 与稳定性

按严重程度排列：

| 严重级别 | Issue # | 描述 | 状态 | 关联 Fix PR |
|----------|---------|------|------|-------------|
| **严重** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | Evolution 模式下每分钟持续消耗 Token | Open，6天未更新 | 无 |
| **高** | [#3111](https://github.com/sipeed/picoclaw/issues/3111) | Gemini 3.5 Flash 工具执行失败（400 Bad Request），与 Agentic reasoning schema 不兼容 | Open，无评论 | 无 |
| **中** | [#3110](https://github.com/sipeed/picoclaw/issues/3110) | Telegram Forum 话题中回复错发到 #General 主题 | Open，无评论 | 无 |
| **低** | [#3109](https://github.com/sipeed/picoclaw/issues/3109) 已作为功能关闭，不视为 Bug | - | Closed | - |

**点评**：Token 消耗异常可能影响用户成本，建议优先排查 Evolution 循环逻辑；Gemini 兼容性问题影响新模型用户，需调整请求 schema。

## 6. 功能请求与路线图信号

- **#2984** `Add explicit turn completion signal for Pico WebSocket`（已有 PR #3116 部分实现）  
  信号：项目正在完善 WebSocket 协议的生命周期管理，预计将纳入 v0.3.0。

- **#3114** [OPEN] `Telegram 渠道按对话类型（私聊/群组/频道）的权限分级控制`  
  用户明确描述安全边界需求，与已关闭的 #3109 主题相近，很可能被列为下一版本的功能项。

- **#3118** [OPEN] PR `Add remote Pico WebSocket mode to picoclaw agent`  
  新增远程连接模式，支持 `picoclaw agent --remote ws://...`，扩展了 CLI 使用场景，反映出项目向分布式部署发展的趋势。

## 7. 用户反馈摘要

- **#3012** 免费 BSD 用户反馈：启用 Evolution 功能后 Token 每分钟持续消耗，怀疑是与系统 cron 或循环触发有关，期待紧急修复。
- **#2984** WebSocket 客户端开发者指出：目前无法区分“typing.stop”与“处理完成”，导致轮询中断不准确，强烈要求增加 `turn.completed` 事件。
- **#3114** 社区用户 v2up-32mb 详细描述了 Telegram 群组中危险操作（exec、文件修改）缺乏权限分级的问题，认为当前“允许所有能力”的设计在多人场景下不可控。

## 8. 待处理积压

以下 Issue/PR 已存在较长时间（>2周），且无充分更新，提醒维护者评估：

| 项目 | 创建时间 | 最后更新 | 说明 |
|------|----------|----------|------|
| [#2964](https://github.com/sipeed/picoclaw/pull/2964) `Feat/image input compression` | 2026-05-28 | 2026-06-12 | 图片压缩功能，已经 stale 标签，需确认是否继续合入 |
| [#2917](https://github.com/sipeed/picoclaw/pull/2917) `feat(provider): add NEAR AI Cloud provider` | 2026-05-21 | 2026-06-12 | 新增 LLM 提供者，一个月未合入，可能需解决冲突或测试 |
| [#3053](https://github.com/sipeed/picoclaw/pull/3053) `fix(evolution): add ok check for LoadOrStore type assertion` | 2026-06-08 | 2026-06-12 | 修复 Evolution 存储的 panic 风险，无评论，应尽快合并 |
| [#3091](https://github.com/sipeed/picoclaw/pull/3091) `fix(openai_compat): add ok check for native_search type assertion` | 2026-06-10 | 2026-06-12 | 类似的类型断言安全检查，需及时合并 |

---

**项目健康度评分：** ⭐⭐⭐⭐☆（4/5）  
社区活跃、合并节奏良好，但 Token 消耗 Bug 与部分积压需尽快处理以避免用户流失。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，遵循您的指示，以下是为 NanoClaw 项目生成的 2026-06-13 动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-13

## 1. 今日速览

今日项目活跃度极高，开发节奏迅猛。过去24小时内，共有**18个PR**被更新（其中10个已合并/关闭），**5个Issue**被更新（其中1个已关闭）。项目核心正在经历一波密集的功能合并与Bug修复，尤其在**Signal通道功能完善**、**会话/轮询稳定性修复**以及**安全加固**方面取得显著进展。社区贡献者提交了多个高质量的修补与新特性PR，显示出项目生态的活跃度。同时，数个关键的稳定性和安全Issue仍然有待解决，成为项目当前的主要痛点。

**活跃度评估：高**

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日共有 **10个PR** 被合并/关闭，主要集中在以下方面：

- **通道功能完善：** 多个关于Signal通道的PR被合并，极大地增强了其成熟度。
    - **#2203** [已合并] 实现了Signal的**双向反应（Reaction）支持**，允许用户对消息进行表情反应，也允许Agent通过MCP工具添加反应。
    - **#2071** [已合并] **重写了Signal附件路由**，现在所有非音频附件（如PDF、文档、图片）都会通过Inbox路径传递给Agent，使其可读可用。
    - **#2070** [已合并] **扩展了附件的处理能力**，支持从宿主文件路径（而非仅base64）提取附件，为Signal等原生通道适配器铺平了道路。
    - **#2040** [已合并] 为Signal通道添加了 **“传出附件”支持**，Agent现在可以发送文件给用户。

- **稳定性与健壮性：**
    - **#2670** [已合并] **修复了会话崩溃循环**：当会话因损坏的转录文件（`thinking`/`redacted_thinking`块）而崩溃时，现在能进行自愈，避免了无限重启。
    - **#2692** [已合并] **增强了API错误处理**：当Claude Agent SDK遇到可恢复的5xx错误（如`529 Overloaded`）时，系统会进行重试，并在最终失败时通知用户，而非静默失败。
    - **#2277** [已合并] **修复了后续消息的路由问题**：当在轮询过程中有新的后续消息到达时，系统现在能正确刷新路由上下文，确保消息能送达正确的Agent。

- **功能增强：**
    - **#2072** [已合并] **支持了Ollama多模态模型**：`ollama_generate`工具现在可以接收工作区路径下的图片，并将其作为base64编码发送给本地多模态模型。
    - **#2084** [已合并] **引入了灾难恢复备份功能**：每日自动备份项目状态，并提供完整或单Agent的恢复CLI工具。

- **修复与回滚** **#2267** [已合并] **修复了Agent间通信的路由问题**：当Agent组有多个活跃会话时，a2a回复现在会正确路由回源会话，解决了“分裂脑”问题。

**小结：** 项目在Signal通道的“最后一公里”（附件、反应）上取得突破，同时系统性解决了会话引擎中的多个关键稳定性Bug，并对LLM链路和备份策略进行了加固，整体健壮性上了一个台阶。

## 4. 社区热点

- **#2506 [Bug] send_message dedup silently drops responses …** ([链接](nanocoai/nanoclaw Issue #2506))
    - **热度：** 3条评论
    - **分析：** 这是一个影响核心用户体验的严重Bug。当两个回合在60秒内完成，或后续消息在流式传输中到达时，Agent的响应会被静默丢弃。社区成员mshirel详细描述了复现步骤，引发了对`send_message`去重机制和轮询逻辑的讨论。该Issue反映了用户对交互可靠性的强烈诉求，尤其是需要处理快速连续对话的场景。

- **#2632 [Question] Clarify status of Telegram agent-swarm …** ([链接](nanocoai/nanoclaw Issue #2632))
    - **热度：** 1条评论
    - **分析：** 用户arthurkrupa正在规划从v1到v2的迁移，但对Telegram的Agent-swarm/多机器人身份功能在v2中的状态感到困惑。这代表了老用户在版本迁移过程中的典型痛点——寻找旧特性在新架构下的对应实现或替代方案。这提示项目维护者需要加强v1到v2的迁移文档或兼容性说明。

## 5. Bug 与稳定性

| 严重程度 | Issue编号 | 标题摘要 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | **#2506** | `send_message`去重逻辑会在60秒内静默丢弃响应 | **活跃** | 影响核心交互，导致客户端超时。暂无关联PR修复。 |
| **较高** | **#2668** | Agent会话无单工具超时，挂起工具会阻塞会话30分钟 | **活跃** | 单个MCP工具调用若挂起，会阻塞整个会话直至被“冷杀”，严重影响生产环境可用性。 |
| **中等** | **#2711** | `create_agent` MCP工具未进行管理员权限校验 | **活跃** | 任何容器都可创建Agent组，存在严重越权风险。 |
| **已解决** | **#2751** | 预算耗尽的LLM调用被静默丢弃，用户收不到回复 | **已关闭** | 虽已解决，但暴露出预算超限处理逻辑的缺陷。 |
| **待修复** | **#2750 (PR)** | 修复容器kill后outbound.db日志损坏及轮询竞争问题 | **开放** | Contributor提交了修复PR，瞄准了两个关键的生产环境数据库损坏问题。等待合并。 |
| **待修复** | **#2752 (PR)** | 修复Discord附件的文本和图片无法被Agent读取的问题 | **开放** | Contributor提交了修复PR，解决了Discord通道中附件无法传递的通用性问题。 |

**分析：** 核心会话引擎的两个Bug（#2506, #2668）严重影响了用户体验和系统可靠性，是当前最高优先级的修复目标。权限校验漏洞(#2711)存在安全风险，应尽快修复。社区贡献者已为几个关键问题提供了修复PR(#2750, #2752)，审核与合并工作迫在眉睫。

## 6. 功能请求与路线图信号

- **新功能PR（信号）：**
    - **#2747** [开放] **OneCLI SDK 2.2.1 集成**：引入了凭证挂载和机器可验证的PIN。这似乎是针对OneCLI云环境的功能增强，可能用于满足企业级的安全和凭证管理需求。
    - **#2746** [开放] **Provider能力缝（Capability Seam）**：引入主机端注册表，让Provider按照能力声明自身功能。这是一个**架构层面的抽象**，可能为未来更灵活的Provider插件系统打下基础。
    - **#2745** [开放] **可选持久记忆脚手架**：为Provider增加`usesMemoryScaffold`能力。这是一个**长期路线图的重要信号**，预示着项目计划将“记忆”功能作为对Provider的可选增强特性，而非核心硬编码功能。
- **功能请求（来自Issue）:**
    - **#2632** 用户请求明确 **Telegram Agent-swarm** 在v2的状态，这可能是社区用户期望恢复或引导至替代方案的功能。

**预判：** `OneCLI SDK升级`、`Provider能力缝`和`持久记忆`这三个PR表明项目正在向更模块化、可扩展的企业级方向演进。尤其是“持久记忆”和“能力缝”的设计，将对开发者的Plugin开发体验产生深远影响，很可能被纳入下一个里程碑版本。

## 7. 用户反馈摘要

- **痛点与场景：**
    - **可靠性是第一要务**：用户mshirel连续提交了两个关于“静默失败”的Bug(#2506, #2751)，反映出用户在依赖Agent处理自动化任务时，对**不可预期和无反馈的行为**的零容忍态度。他们需要明确的错误处理和反馈，而不是在“空白”中等待超时。
    - **迁移的迷茫**：用户arthurkrupa(#2632)的提问揭示了从一个主要版本迁移到另一个版本时的典型困境。老用户依赖的特定功能（Telegram swarm）在新版中可能不存在或已被重写，缺少清晰的迁移指导会增加用户的流失风险。
    - **安全意识**：用户jonazri(#2711)发现了未授权的`create_agent`漏洞，这是一个非常积极的信号，表明社区用户不仅在“用”，还在主动进行安全审计，为项目健康做出了贡献。

- **满意/不满意点：**
    - **积极贡献**：`boazdori`和`sturdy4days`等贡献者直接提交了安全加固(#2748, #2749)和稳定性修复(#2750, #2753)的PR，展示了社区强大的自愈能力。他们对项目架构的理解和贡献质量非常高。
    - **沟通需求**：`assapin`通过#2751报告了预算耗尽的静默失败问题，虽然该Issue已关闭，但其背后反映的是用户希望了解LLM调用失败的具体原因（预算、限流等），而不仅是一个空洞的失败结果。

## 8. 待处理积压

- **#2506** [Bug] `send_message` 静默丢弃响应 ([链接](nanocoai/nanoclaw Issue #2506))
    - **创建于：** 2026-05-16，**已开放 28 天**
    - **分析：** 作为影响核心交互的严重Bug，却在一个月的时间内没有关联的修复PR被提出。该Issue有详细的复现步骤和社区讨论，应被确认为P0优先级，并分配给核心开发者。

- **#2668** [Bug] 会话无单工具超时，阻塞30分钟 ([链接](nanocoai/nanoclaw Issue #2668))
    - **创建于：** 2026-06-01，**已开放 12 天**
    - **分析：** 同样是严重稳定性的问题，任何挂起的MCP工具调用都会导致整个Agent会话被阻塞半小时。这个设计缺陷对依赖Agent进行关键任务的应用是致命的，需要架构层面的修复。

- **#2632** [Question] Telegram swarm 功能在v2中状态不明 ([链接](nanocoai/nanoclaw Issue #2632))
    - **创建于：** 2026-05-28，**已开放 16 天**
    - **分析：** 维护者未对用户的迁移咨询做出明确回应。长期未回复会打击社区用户参与新版本的积极性。建议项目组提供正式回复，或在文档中注明该功能的替代方案。

**提醒：** 上述三个Issue和PR已存在较长时间，对项目信誉和用户满意度有潜在负面影响。强烈建议维护团队在未来一周内给予关注，至少对#2632进行官方回复，并对#2506和#2668给出修复计划或进度更新。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，这是根据NullClaw (github.com/nullclaw/nullclaw) GitHub数据生成的2026-06-13项目动态日报。

---

## NullClaw 项目日报 - 2026-06-13

### 1. 今日速览

本日NullClaw项目整体处于**修复与配置阶段**，活跃度中等。过去24小时未发布新版本，但社区提交了1个关于本地模型集成（Ollama）的关键Bug报告，和3个专注于功能优化与稳定性修复的PR。所有PR均由同一贡献者提交，体现了社区在核心功能打磨上的集中投入。项目当前无PR被合并，表明维护者正在进行审慎的代码审查。

### 3. 项目进展

本日无PR被合并或关闭。**所有3个PR（#949, #951, #953）均处于待合并状态**，它们分别推进了以下重要方向：
- **配置可定制性增强**：[PR #949](https://github.com/nullclaw/nullclaw/pull/949) 旨在允许用户通过配置文件（config.json）设定新会话的默认队列模式，使项目配置更灵活。
- **用户体验与日志清晰度提升**：[PR #951](https://github.com/nullclaw/nullclaw/pull/951) 修复了当Agent进程异常退出时，错误地将初始化日志（如内存计划）作为Agent响应输出的问题，避免了渠道中的信息污染。
- **稳定性的关键修复**：[PR #953](https://github.com/nullclaw/nullclaw/pull/953) 专注于修复Discord网关连接问题，包括在重连时安全关闭旧Socket、处理连接超时等场景，增强了与Discord平台集成的健壮性。

这些PR体现了项目当前正在从“功能可用”向“配置灵活、运行稳定”迈进。

### 4. 社区热点

本日社区讨论焦点唯一且明确，即 **Bug报告 #952** ([Link](https://github.com/nullclaw/nullclaw/issues/952))。该Issue由用户`bloodgroup-cplusplus`提出，描述了使用Ollama加载Gemma模型时，Agent无法输出完整句子的问题。尽管暂无评论，但其直接关联到项目最核心的“本地模型”功能，且附有截图证明问题存在，很可能成为下一个修复的重点。

### 5. Bug 与稳定性

本日报告的Bug按照严重程度排列如下：

| 严重程度 | 问题描述 | Issue / PR | 解决方案状态 |
| :--- | :--- | :--- | :--- |
| **高** | 使用Ollama本地模型（Gemma）时，Agent回答不完整。这直接影响了核心功能体验。 | [#952](https://github.com/nullclaw/nullclaw/issues/952) | 无相关Fix PR |
| **中** | Agent进程异常退出时，错误地将初始化日志（stdout/stderr）发布到消息渠道。 | [#951](https://github.com/nullclaw/nullclaw/pull/951) | 已有Fix PR（待合并） |
| **中** | Discord网关Socket在重连时可能出现未关闭或连接卡死的问题。 | [#953](https://github.com/nullclaw/nullclaw/pull/953) | 已有Fix PR（待合并） |

### 6. 功能请求与路线图信号

本日未有用户直接提出新的功能请求。但从已有的PR中可以看见清晰的路线图信号：
- **配置驱动的Agent行为**：来自PR #949，允许通过配置文件预设`default_queue_mode`，表明项目正在向更灵活的、通过外部配置控制Agent行为的方向发展。
- **第三方平台集成健壮性**：PR #953集中优化Discord网关的重连机制，预示下一版本将着力提升与主流通讯平台的集成稳定性。

### 7. 用户反馈摘要

本日来自用户的直接反馈较为有限，主要来自Issue #952：
- **用户痛点**: 用户`bloodgroup-cplusplus`尝试使用项目最核心的本地模型功能，但遇到了输出不完整的严重问题。这表明**Ollama集成在特定模型或配置下存在兼容性问题**，直接影响了用户对新用户的上手体验。用户附上了截图，说明问题具有可复现性。

### 8. 待处理积压

本日无长期未响应的Issue或PR。当前主要积压项为3个打开状态的PR（#949, #951, #953），它们已存在2-3天，需要维护者尽快审查与合并，以解决已经明确的Bug并推进功能优化。Bug报告#952也需要维护者及时跟进并复现。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，这是根据您提供的 IronClaw 项目数据生成的2026年6月13日动态日报。

---

## IronClaw 项目动态日报 | 2026-06-13

### 1. 今日速览

今日 IronClaw 项目展现出极高的开发活跃度。核心开发者团队密集地围绕 **DeferredBusy（延迟忙）消息排水架构**、**“始终允许”审批持久化**、**频道连接与交付状态的上下文感知** 以及 **安全审计与边界控制** 等关键领域进行设计、评审与迭代。社区方面，用户测试团队 (sunglow666) 提交了大量关于 **Reborn WebUI v2** 的 UX/UI 问题与 bug，主要集中在对话状态管理、附件处理、主题一致性等方面。同时，**cargo-deny 安全公告** 和 **CI 测试效率** 问题也获得了维护者的关注。整体来看，项目正处于核心功能深度打磨与用户体验优化并重的阶段，健康状况良好。

### 2. 版本发布

无

### 3. 项目进展

今日项目在多个关键功能线上取得了实质性的推进，特别是关于阻塞线程的用户体验和系统安全性：

- **核心架构变更：阻塞线程处理策略重塑**
    - **PR #4812 (已关闭)**: 实现了`DeferredBusy`（延迟忙）消息的自动排水功能，即当阻塞线程的那个“运行（Run）”结束后，之前被阻塞的消息会自动提交处理。这是一个重要的用户体验改进，解决了消息“石沉大海”的问题。
    - **PR #4838 (新开)**: 以更简单直接的方式替代了 #4812 的复杂方案。它不再自动排水，而是直接拒绝在繁忙线程上发送的新消息，并给出明确的提示，将重试的主动权交给用户。这体现了设计思路从“后台自动处理”向“明确告知用户”的转变。

- **测试与QA基础设施增强**
    - **PR #4773 (已关闭)**: 引入了用于 Reborn 运行时的记录/回放机制。现在可以录制真实大模型在QA场景下的行为轨迹，并在CI中确定性回放，从而精确验证代理的工具选择和行为，大幅提升测试可靠性。

- **安全审计与风险控制**
    - **PR #4561 (开放中)**: 记录MCP（模型上下文协议）直接租赁拒绝事件到安全审计日志中，增强了安全审计的全面性。
    - **PR #4562, #4568, #4569 (均已关闭)**: 针对授权、权限Hook（钩子）系统进行了强化，包括记录失败事件、设置分发上限和聚合租户谓词键限制，加强了系统的安全边界和防滥用能力。

- **用户体验修复**
    - **PR #4835 (新开)**: 修复了一个关键的UX问题——“始终允许”的审批现在可以在不同对话线程间持久生效，用户不再需要在每个新对话中都重复授权同一个工具。
    - **PR #4836 (新开)**: 使模型能够感知当前已连接的频道、消息投递状态和运行起源，为实现更智能的上下文感知交互奠定了基础。

### 4. 社区热点

今日社区讨论（以评论数衡量）主要集中在三个核心议题上，反映了用户对**长期架构设计**和**核心功能正确性**的高度关注。

1.  **`#4817` - DeferredBusy排水后续设计决策** ([链接](nearai/ironclaw Issue #4817)): 评论: 3
    - **焦点**： 这是对 `#4812` (现已关闭的排水PR) 的架构性后续跟踪，记录了三个关键的设计待定项。社区和核心开发者共同探讨了排水提交的门户、陈旧意图策略和启动时的扫描问题，体现了对系统长期稳健性的深思熟虑。
    - **诉求**： 社区不仅关注功能“是否可用”，更关注其底层架构“是否正确和可扩展”。

2.  **`#4825` - “始终允许”审批的跨线程持久化** ([链接](nearai/ironclaw Issue #4825)): 评论: 3
    - **焦点**： 这是一个用户痛点驱动的Issue，详细描述了“始终允许”授权无法跨对话线程持久的问题。该问题获得了高度关注，并在一天内就有了对应的修复PR (#4835)。
    - **诉求**： 用户对简化重复性操作有强烈需求，期望核心功能（如授权）能够智能、持久地工作，而非在每个新对话中都需要重新操作。

3.  **`#4703` - NEAR AI模型选择器保存显示名称而非模型ID** ([链接](nearai/ironclaw Issue #4703)): 评论: 3
    - **焦点**： 这是一个典型的配置Bug，导致选择了错误的模型。虽然已经关闭，但其评论数表明它是一个容易触发且影响使用体验的问题。
    - **诉求**： 用户期望配置UI的反馈与实际执行逻辑完全一致，任何不匹配都会被迅速发现并视为严重问题。

### 5. Bug 与稳定性

昨日报告的Bug数量较多，主要集中在 Reborn 前端，但也包含了关键的后端和基础设施问题。

**严重程度：高**
- **`#4824` - cargo-deny CI 因新 RUSTSEC 安全公告失败** ([链接](nearai/ironclaw Issue #4824)): 安全漏洞导致所有PR的CI检查失败。这直接影响开发流程，需立即修复。**状态：无对应fix PR，已记录问题。**
- **`#4762` - 工具工作流失败导致后续消息和活动排序不一致** ([链接](nearai/ironclaw Issue #4762)): 用户报告了一个核心流程Bug，工具调用失败后整个对话状态陷入混乱。**状态：无对应fix PR。**
- **`#4796` - LLM 缺乏当前时间/日期感知** ([链接](nearai/ironclaw Issue #4796)): 影响所有依赖时间敏感性的工作流（日历、任务、提醒等）。**状态：无对应fix PR。**
- **`#4759` - 工作区路径重复** ([链接](nearai/ironclaw Issue #4759)): 一个路径处理逻辑错误，会导致文件创建在错误的位置。**状态：无对应fix PR。**

**严重程度：中**
- **`#4705` & `#4706` - NEAR AI SSO 设置失败和授权流程无法恢复** ([链接](nearai/ironclaw Issue #4705) | [链接](nearai/ironclaw Issue #4706)): 核心账号对接和授权流程存在严重问题，是用户入门体验的关键障碍。**状态：均已关闭，推测已有修复。**
- **`#4697` - 活动Provider状态显示不一致** ([链接](nearai/ironclaw Issue #4697)): 用户无法确定系统实际使用的推理提供商，造成配置和使用上的困惑。
- **`#4770` - 工具活动刷新后停止更新（可能SSE重连问题）** ([链接](nearai/ironclaw Issue #4770)): 影响对话实时性体验。

**严重程度：低 (UX问题)**
- **`#4819` - 附件警告横幅在Light主题下难以阅读** ([链接](nearai/ironclaw Issue #4819))
- **`#4823` - 删除运行中的对话无UI反馈** ([链接](nearai/ironclaw Issue #4823))
- **`#4725` - 工作状态下Composer仍显示可交互** ([链接](nearai/ironclaw Issue #4725))
- **`#4719` - 对话内容区在返回时闪烁** ([链接](nearai/ironclaw Issue #4719))

### 6. 功能请求与路线图信号

- **附件功能持续推进**：由 `ilblackdragon` 主导的一系列PR（如 `#4655`, `#4670`, `#4738`）正在稳步推进附件支持，覆盖从合同、存储后端到前端的完整链路。这将是下一个版本的一个亮点。
- **DeferredBusy 机制路线图调整**：#4812 的关闭和 #4838 的新开，以及相关的 `#4831`, `#4832` 等Issue，标志着项目对“处理阻塞线程消息”这一问题的策略发生了根本性转变，从“后台自动排水”转向“即时拒绝并通知用户”。这个新策略可能会被优先纳入下一版本。
- **性能与基础设施**：
    - `#4813` 提出的“拆分长CI测试任务”建议，若被采纳将显著提升开发者的反馈效率。
    - `#4822` 要求跟踪 Engine V2 的LLM用量，这是系统监控和计费体系的必要功能，信号明确。
- **模型与上下文能力增强**：`#4796` (时间感知) 和 `#4836` PR (运行时上下文) 表明，项目正在探索如何让代理拥有更丰富的上下文信息以做出更智能的决策。

### 7. 用户反馈摘要

从 `sunglow666` 提交的大量Issues中，可以提炼出明确的用户反馈：

- **痛点**： Reborn v2 WebUI 在用户体验细节上仍不完善。用户反复遇到 **对话状态不一致**（工作区显示、删除反馈）、**配置冲突**（Provider状态、模型选择）、**交互干扰**（链接跳转、Composer状态、闪烁）以及 **草稿丢失** 等问题。这些看似小的体验问题累积起来，会严重破坏用户的使用流畅感。
- **使用场景**： 用户正在 **真实地使用 Reborn v2** 进行工具调用、文件操作、SSO登录等多种复杂流程。例如，`#4762` 描述的“下载文件并保存到工作区”场景，`#4705` 的 SSO 场景，都反映了用户正在探索产品的核心能力边界。
- **满意点**： 虽然未明确表达满意，但从用户愿意花费精力提交如此详尽的Bug报告来看，他们对 IronClaw 项目抱有较高期望并积极参与测试。项目组对 `#4703`, `#4705` 等问题的快速响应和关闭，也向社区传递了积极信号。

### 8. 待处理积压

- **`#3708` - 发布版本PR (已开放近一个月)** ([链接](nearai/ironclaw PR #3708)): 这是一个由 CI 自动生成的版本发布PR，包含了多个crate的API破坏性变更。它长期处于开放状态，表明项目可能积累了大量的待发布变更，或者发布流程存在阻塞。维护者应评估其状态，推动或关闭它。
- **`#4561` - 记录MCP直接租赁拒绝事件 (等待合并)** ([链接](nearai/ironclaw PR #4561)): 这是一个重要的安全审计增强PR，但已在开放状态停留了5天。建议维护者尽快评审并合并，以完善安全事件的可见性。
- **核心附件功能系列PR**：`#4654`, `#4655`, `#4668`, `#4670` 等PR由 `ilblackdragon` 提交，目标是为项目引入完整的附件支持。这些PR虽然近期都有更新，但尚未合并。作为重要的路线图功能，应持续关注其评审进度，避免成为开发瓶颈。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 开源项目的分析师，根据您提供的 GitHub 数据，以下是 2026 年 6 月 13 日的项目动态日报。

---

### LobsterAI 项目动态日报 (2026-06-13)

#### 1. 今日速览

今日项目主要处于 **版本合并与问题修复** 阶段。过去24小时内，项目活跃度较高，主要依托于一个重大的 Release 分支合并（`release/2026.6.11`），将“计算机使用”（Computer Use）、实时语音输入等新功能合入主分支。同时，项目组修复了多个关键 Bug，包括文生图格式、同名词包模型选择等问题。值得注意的是，虽然今日无新 Issue 提交，但仍有 6 个从 4 月份遗留的 PR 处于待合并状态，长期积压问题值得关注。

#### 2. 版本发布

今日无新版本发布。

#### 3. 项目进展

今日共计合并/关闭了 11 个 PR，主要包括一个大型 Release 分支合并和多个关键 Bug 修复，项目正稳步向新的里程碑推进。

-   **重大功能合并**：(PR [#2158](https://github.com/netease-youdao/LobsterAI/pull/2158)) 将 `release/2026.6.11` 分支合并回 `main` 主分支。这是今日最核心的进展，合入了以下亮点功能：
    -   **新增“计算机使用”MVP 及内置工具包**：这标志着 LobsterAI 向 Agent 自主操作计算机迈出了重要一步。
    -   **协同时作模式新增实时 ASR 语音输入**：提升了用户在协作场景下的输入效率。
    -   **丰富 Artifact 分享功能**：新增 HTML 工件公开分享模式选择，并支持图片和 SVG 工件的分享。
-   **图片保存格式修复**：(PR [#2157](https://github.com/netease-youdao/LobsterAI/pull/2157)) 修复了文生图功能保存图片时，因第三方返回的文件后缀名错误（如 `.jpg`）导致与实际 PNG 内容不匹配的问题。现在会根据文件字节内容识别真实格式，显著提升用户体验。
-   **模型选择持久化修复**：(PR [#2153](https://github.com/netease-youdao/LobsterAI/pull/2153)) 修复了在 OpenClaw 模型归一化过程中，因同名前缀导致的模型选择丢失问题，确保用户在会话中能正确保持其模型选择。
-   **流式响应体验优化**：(PR [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154)) 修复了在手动停止 AI 流式响应后，模型元数据（如 Token 用量）无法正常显示的问题，优化了交互反馈的完整性。
-   **语音输入稳定性**：(PR [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155)) 修复了协作输入流程中可能导致重复启动实时 ASR 的竞态条件，提升了语音功能的稳定性。

#### 4. 社区热点

今日社区讨论相对平静，无新增高热度 Issue 或 PR 讨论。但多个从 4 月遗留至今的 PR 在今天被更新，侧面反映出社区对以下问题的持续关注：

-   **[长期积压 PR] `fix(openclaw): 修复网关反复启动失败导致的无限重启循环`** (PR [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446))：该 PR 旨在解决 OpenClaw 网关因竞态条件导致的无限重启瘫痪问题，对使用 OpenClaw 架构的用户至关重要，评论为零但状态为“stale”且被更新。
-   **[长期积压 PR] `feat(cowork): 定时任务多次执行记录折叠分组展示`** (PR [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449))：该 PR 试图改进定时任务积累过多会话记录，导致侧边栏混乱的体验问题。社区对此优化功能的关注度较高，但长期未合并。

**分析**：社区的核心诉求依然集中在 **稳定性和易用性** 上。OpenClaw 网关的无限重启 Bug 是严重的稳定性问题，而定时任务记录的混乱则是高频使用场景下的易用性痛点。这两个 PR 的长期搁置可能会影响核心用户的留存。

#### 5. Bug 与稳定性

今日主要 Bug 均已在修复 PR 中处理完成，无明显的新增严重 Bug。

| 严重程度 | 问题描述 | 状态 | 相关 PR/Issue |
| :--- | :--- | :--- | :--- |
| **高** | **文生图保存扩展名错误**：服务器返回错误的文件后缀，导致PNG内容被错误保存为`.jpg`。 | **已修复 (Merged)** | [#2157](https://github.com/netease-youdao/LobsterAI/pull/2157) |
| **中** | **模型选择丢失**：因同名前缀模型，用户选择的模型在会话中无法被正确持久化。 | **已修复 (Merged)** | [#2153](https://github.com/netease-youdao/LobsterAI/pull/2153) |
| **中** | **手动停止流响应后信息不完整**：手动停止 AI 生成后，回复消息的元数据信息丢失。 | **已修复 (Merged)** | [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154) |
| **中** | **重复启动实时语音**：协作输入中存在竞态条件，可能意外启动多个语音识别实例。 | **已修复 (Merged)** | [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155) |
| **低** | **(已解决) Hit API Error**： (Issue [#1](https://github.com/netease-youdao/LobsterAI/issues/1)) 用户在使用 OpenAI API 类型时遇到参数无效错误。该问题已在更早的时间点被关闭。 | **已关闭** | [#1](https://github.com/netease-youdao/LobsterAI/issues/1) |

#### 6. 功能请求与路线图信号

今日无新增 Issues 明确提出的新功能请求。但从合并的 PR [#2158](https://github.com/netease-youdao/LobsterAI/pull/2158) 可以看出项目路线图的明确信号：

-   **“计算机使用”Agent**：已被列为 MVP 功能，并提供了内置工具包，这将是近期乃至下个版本的核心功能方向。
-   **实时语音协作**：已在协作模式下落地，预示项目在多模态交互上的投入。
-   **Artifact 分享优化**：社区对 Artifact（如 HTML、图片）的分享功能有需求，新增的分享模式选择和多格式支持是对此类反馈的直接响应。

**预测**：结合开放 PR [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) 的诉求，**优化定时任务/会话管理** 的功能很可能被纳入到后续的版本迭代计划中。

#### 7. 用户反馈摘要

1.  **用户痛点：API 配置兼容性**
    在已关闭的 Issue [#1](https://github.com/netease-youdao/LobsterAI/issues/1) 中，用户 `simson2010` 在配置 MiniMax API 并以 OpenAI 类型使用时，遇到了 `invalid params` 错误。这反映了用户在使用第三方 API 对接时的常见痛点，提示项目需要进一步优化对不同 API 协议的兼容性和错误提示。

2.  **用户场景：功能全面性**
    今日无新的具体用户评论。但从 PR 内容引申看，社区用户的需求场景已从基础的对话，拓展到**文生图保存**、**计算机控制**、**定时任务自动化**等更复杂的领域，表明用户群体正从普通使用者向深度用户发展。

#### 8. 待处理积压

以下为需维护者重点关注、长期未被合并的重要 PR：

1.  **`fix(openclaw): 修复网关反复启动失败导致的无限重启循环`** (PR [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446)) - **创建于 2026-04-03**。这是一个稳定性问题，可能导致 OpenClaw 架构瘫痪，影响面广，严重度高。建议尽快评审并合入下一个补丁版本。

2.  **`feat(cowork): 定时任务多次执行记录折叠分组展示`** (PR [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449)) - **创建于 2026-04-03**。这是一个良好的易用性改进，能解决定时任务用户的痛点。长期搁置可能降低用户对定时任务功能的使用意愿。

3.  **`fix(i18n): Agent 设置页面删除按钮及技能选择器显示英文`** (PR [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448)) - **创建于 2026-04-03**。国际化不完整的问题。对于多语言用户而言，这会直接影响使用体验。

**总结**：LobsterAI 今日的开发和维护工作非常高效，尤其在 Bug 修复和功能合并上表现突出。然而，长达两个月的“老 PR”积压问题不容忽视，特别是涉及核心稳定性的 OpenClaw 网关修复，需要项目维护者给予最高优先级的关注。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报  
**日期：2026-06-13** | 数据来源：[GitHub - moltis-org/moltis](https://github.com/moltis-org/moltis)

---

## 1. 今日速览
过去 24 小时内，Moltis 项目保持中等活跃度：共产生 3 条 Issue 更新（均为新开或重新活跃），无 PR 变动，无新版本发布。其中包含 1 个 Bug 报告（Fastmail MCP 授权问题）和 2 个功能请求（K8s 沙箱后端、本地 STT 引擎）。社区讨论集中在扩展执行沙箱隔离能力与语音交互本地化技术选型上，整体项目健康度良好，但需关注长时间未响应的功能请求（#1102）及新 Bug 的修复计划。

---

## 2. 版本发布
无新版本发布。

---

## 3. 项目进展
过去 24 小时内无 PR 被合并或关闭，因此未记录到明确的代码推进。但 Issue 更新反映社区持续提出改进方向，为后续开发积累了需求清单。

---

## 4. 社区热点
- **#1118 – [Feature]: Add Kubernetes-native sandbox backend with runtimeClassName support**  
  [链接](https://github.com/moltis-org/moltis/issues/1118)  
  该 Issue 提出为代理命令执行增加 K8s 原生沙箱后端，支持通过 `runtimeClassName` 接入 Kata Containers、gVisor 等 VM 级隔离方案。这是当前 AI 代理安全执行领域的热点诉求——如何安全运行 LLM 生成的不可信代码。社区已有 1 条评论积极讨论实现路径，预计会成为下一阶段架构演进的关键参考。

- **#1102 – [Feature]: Add FunASR/SenseVoice as local STT engine**  
  [链接](https://github.com/moltis-org/moltis/issues/1102)  
  自 6 月 4 日创建以来，该 Issue 今日获得更新（评论），用户强烈建议集成 FunASR 或 SenseVoice，强调“超快”推理速度（SenseVoice-Small 对 10 秒音频仅需 70ms）及原生流式能力。背后反映社区对低延迟、本地化语音识别方案的高期待，尤其适合资源受限或注重隐私的部署场景。

---

## 5. Bug 与稳定性
- **#1115 – [Bug]: Fastmail MCP Authorisation**  
  [链接](https://github.com/moltis-org/moltis/issues/1115)  
  **严重程度：中等**  
  用户报告在与 Fastmail MCP（模型上下文协议）集成时出现授权问题，但未提供完整会话上下文。该问题可能影响使用 Fastmail 作为外部记忆或工具存储的用户。目前有 2 条评论，尚未关联任何修复 PR。建议维护者尽快要求补充完整日志与复现步骤，以便定位根本原因。

其余 Issues 均为功能请求，未发现崩溃、回归或数据丢失类严重 Bug。

---

## 6. 功能请求与路线图信号
以下两个功能请求均未出现在现有 PR 或标签计划中，但具有较高采纳潜力：

| Issue | 功能 | 可能纳入版本 | 原因 |
|-------|------|--------------|------|
| #1118 | K8s 原生沙箱后端（runtimeClassName） | 下一大版本（v0.x） | 符合 Agent 安全执行的核心需求，且实现方案清晰（K8s Ephemeral Pods） |
| #1102 | 集成 FunASR/SenseVoice 作为本地 STT | 中期规划 | 已有多位社区成员点赞（👍），与当前主流语音助手项目（如 Mycroft、Pipecat）趋势一致 |

另外，注意到 #1102 已开放 9 天，累计 1 条评论，建议维护者回应是否已将其列入 roadmap，避免社区重复或失望。

---

## 7. 用户反馈摘要
- **#1115 用户**：明确提及已检查现有 Bug 列表并运行最新版本，但授权失败时未能附带完整会话上下文。可能源于 OAuth 令牌管理或 MCP 端点配置错误。
- **#1118 作者**：强调“Moltis agents execute untrusted LLM-generated code”是核心痛点，希望获得 Kata Containers 级隔离，表明部分用户部署场景对安全合规要求较高（如企业内部）。
- **#1102 作者**：以“Ultra-fast”和“Native streaming”为关键卖点，暗示当前内置 STT 引擎（如 Whisper）可能存在延迟过高或不支持流式的问题，用户期待更轻量的替代方案。

总体而言，社区对项目扩展性（沙箱、语音引擎）有明确诉求，但对核心功能（如 MCP 授权）的稳定性也保持敏感。

---

## 8. 待处理积压
以下为长期未获维护者响应的关键 Issue，建议优先关注：

- **#1102 – [Feature]: Add FunASR/SenseVoice as local STT engine**  
  [链接](https://github.com/moltis-org/moltis/issues/1102)  
  自 2026-06-04 创建至今已 9 天，无任何维护者标签或评论。若采纳，可显著提升语音交互性能与本地化能力；若不采纳，应明确说明技术选型原因（如版权、依赖复杂度）。

- 另请注意：**#1115** 虽为新 Bug，但若不及时回应可能导致用户流失，建议在 48 小时内打上 `needs-more-info` 标签并引导补充细节。

---

**总结**：Moltis 项目处于功能扩充与安全强化并行的活跃阶段，社区贡献意愿较强。当前最紧急的是对 #1115 Bug 的跟进，以及为两个功能请求提供官方反馈。建议团队在下一次迭代中至少安排一个沙箱隔离相关的 MVP 实现。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，已根据 CoPaw (QwenPaw) 2026-06-13 的GitHub数据，为您生成项目动态日报。

---

### CoPaw 项目动态日报 | 2026年06月13日

**数据源:** github.com/agentscope-ai/CoPaw (主要仓库 QwenPaw)

---

#### 1. 今日速览

项目在6月12日-13日维持高活跃度，社区与开发团队互动频繁。过去24小时内，Issue处理量为21条（新开14，关闭7），PR处理量为24条（待合并13，合并/关闭11）。核心信号是**版本过渡期**：大量Issue集中在`v1.1.11`及后续补丁的Bug反馈和稳定性问题，同时存在将后端从 AgentScope 1.x 迁移至 2.0 的关键讨论与开发。社区对新功能的需求（如Agent协作、桌面体验优化）持续涌现，表明项目生态正从“可用”向“好用”演进。

#### 2. 版本发布

**无** 新版本发布。但内部版本号已推进至 `v1.1.12b1` (PR #5159, #5157)，预示着新版本的发布周期已开启，可能包含对近期Bug的修复。

#### 3. 项目进展

今日合并/关闭的PR集中在**Bug修复**和**工程优化**，具体进展如下：

- **修复关键Bug：**
    - **#5144** `fix(console): force render Collapse panels to prevent memory config loss` - 已合并。修复了长期记忆配置保存时因面板未展开而导致配置丢失的Bug，直接回应了Issue #5137。这是一个典型的UI交互逻辑Bug，现已修复。
    - **#5147** `fix(console): fixed session redirection when switching code mode` - 已合并。修复了 Coding Mode 下刷新页面导致Session丢失的问题，解决了 Issue #5142。此修复增强了Coding模式的可用性。
    - **#5154** `refactor(console): Refactor the result style of the memory search tool.` - 已合并。重构了记忆搜索工具的UI展示结果，修复了Issue #5098中提到的`unknown`显示问题。

- **工程与流程优化：**
    - **#5121** `feat(ci): add release verification gate between build and publish` - 已合并。在CI/CD流程中引入了发布验证门，在构建后、发布前进行自动化健康检查，此举将有效减少发布有缺陷版本的几率，提升项目交付质量。
    - **#5022** `[codex] Guard agent workspace restore targets` - 已合并。增加了对Agent工作区还原路径的验证，阻止将工作区放置到系统管理的私有目录下，提升了安全性。

**总结：** 项目主要精力集中在稳定前端Console，尤其是解决因新版UI更新带来的交互和渲染问题，并加固了底层基础设施的安全性。

#### 4. 社区热点

-   **热烈讨论：后端架构升级**
    -   **Issue #4727** `[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0` (👍: 2, 评论: 10) - 这是一个重大变更讨论。虽然创建稍早，但今天依然有新的讨论。社区和用户对升级到AgentScope 2.0非常关注。
    -   **关联Issue #5149** `[Question]: 什么时候可以升级到agentscope2.0` (已关闭) - 用户直接提问，表明对AgentScope 2.0新架构、新API的期待很高。维护者可能已引导到#4727继续讨论。
    -   **关联PR #5078** `feat(runtime): Runtime 2.0 modular architecture with enhanced tool-call coordination` (待合并, Breaking Change) - 与迁移到AgentScope 2.0紧密相关，拟用模块化Runtime 2.0架构替换旧有执行路径。该PR代表了项目的技术远景，社区高度关注。

-   **高关注度Bug：定时任务功能故障**
    -   **Issue #5064** `[Bug]: 由agnet生产的定时任务, 无法正常触发` (评论: 11) - 该问题获得了大量评论。用户报告Agent创建的定时任务无法触发，且无法编辑。这是一个影响任务自动化核心功能的问题，社区反响强烈，亟需官方确认和修复。

#### 5. Bug 与稳定性

报告了一批影响用户体验的Bug，严重程度以下降序列出：

| 严重程度 | Issue | 描述 | 状态 & 修复PR |
| :--- | :--- | :--- | :--- |
| **严重** | [#5155](https://github.com/agentscope-ai/QwenPaw/issues/5155) | v1.1.11 Docker环境自动宕机重启 | 待开发。稳定性问题，影响服务部署。 |
| **严重** | [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | 长对话后应用无响应，卡死 | 待开发。影响核心聊天功能，可能与内存/上下文管理有关。 |
| **严重** | [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) | Python3.13环境安装TeamChat插件失败（imghdr模块缺失） | 待开发。影响新Python版本的兼容性。 |
| **严重** | [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) | v1.1.11.post2 Gemini工具调用回归（v1.1.10正常） | 待开发。功能回归，影响使用Gemini模型的用户。 |
| **中等** | [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) (已关闭) | v1.1.11.post2附件下载（docx/pdf)报错404 | 已修复。用户确认问题解决？ |
| **中等** | [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | 对话思考逻辑进入死循环 | 待开发。影响AI响应逻辑。 |
| **中等** | [#5145](https://github.com/agentscope-ai/QwenPaw/issues/5145) | 执行细节(Details)无法折叠，干扰主要输出 | 待开发。UI/UX问题，降低信息展示效率。 |
| **低严重**| [#5148](https://github.com/agentscope-ai/QwenPaw/pull/5148) (已关闭) | 网页UI数学公式（根号）渲染错误 | 已修复。UI渲染问题。 |

#### 6. 功能请求与路线图信号

-   **高频信号：Agent协作与生态**
    -   **Issue #5139** `[Feature]: Add Agent Team / Swarm Collaboration Capability` - 用户提议增加**原生Agent团队/群组协作**能力，以处理复杂任务。结合已存在多时的 **PR #4622** `plugin(datapaw): add data-analysis plugin`（数据分析插件）和 **PR #5067** `feat(driver): introduce Agent OS Driver`（Agent OS驱动，支持MCP/A2A等协议），项目正在构建一个“**Agent+插件+外部工具**”的强大生态。
    -   **PR #5088** `feat: initial governance & sandbox interface disscussion` - 正在讨论**治理与沙箱接口**，这可能是为了让Agent在更安全、可控的环境下执行任务，是走向企业级应用的重要一步。

-   **桌面端体验：**
    -   **Issue #5164** `[Feature]: 建议完善桌面版系统托盘、开机自启、后台常驻和服务管理能力` - 用户对桌面版的专业性提出了更高要求。结合 **PR #5153** `feat: replicate Tauri instant-window startup to pywebview client`，项目正在优化桌面客户端的启动速度和后台能力，表明团队重视桌面端体验。

-   **渠道扩展：**
    -   **Issue #5152** `[Feature]: Slack频道支持` - 用户请求增加Slack IM渠道集成。
    -   **Issue #5167** `一个关于 Feishu CardKit 流式卡片体验的小建议` - 用户对飞书渠道的流式卡片体验提出了性能优化建议，表明现有渠道在长文本场景下性能有待提升。

**预测：** 上述功能有望被排入未来版本，特别是Agent协作能力、Agent OS Driver，以及桌面端体验优化。

#### 7. 用户反馈摘要

-   **痛点明显：**
    -   **“定时任务不触发”** (Issue #5064): 用户对Agent的自动化能力有很高期待，但定时任务“看得见用不了”的体验造成了较大失望。
    -   **“付费订阅无法使用”** (Issue #5156): 用户希望将已付费的Kimi coding套餐能力引入QwenPaw，这反映了用户对打通不同AI服务的强烈需求。
    -   **“桌面端体验不够专业”** (Issue #5164): 用户期望QwenPaw成为一个能融入日常操作系统的专业工具，而非仅是浏览器中的一个页面。
    -   **“飞书流式卡片慢”** (Issue #5167): 用户对渠道交互的实时性敏感，长回复的缓慢刷新体验降低了使用效率。
    -   **“打包后白屏”** (Issue #5165): 打包脚本存在错误，导致使用pyinstaller打包的exe无法使用，影响用户二次分发和内部部署。

-   **满意与期待：**
    -   用户对AgentScope 2.0的升级充满期待，认为这是项目走向成熟的关键一步。
    -   用户对`DataPaw`等插件（PR #4622）和Agent生态发展表现出积极态度，认为这能扩展QwenPaw的应用边界。
    -   开发团队对Bug的响应迅速，例如记忆配置丢失（#5137）、Coding Session丢失（#5142）等问题在用户提交后很快获得了修复PR，赢得社区好感。

#### 8. 待处理积压

-   **重要功能请求：**
    -   **Issue #4727** `[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0` - 已讨论近三周，仍未有明确的实施计划。社区密切关注，维护者应给出时间表或阶段性计划。
    -   **PR #4622** `plugin(datapaw): add data-analysis plugin with 12 BI skills` - 已打开超过三周仍未合并。该插件是构建数据分析能力生态的关键，合并优先级应提高。

-   **长期Bug：**
    -   **Issue #5064** `[Bug]: 由agnet生产的定时任务, 无法正常触发` - 虽然创建时间不长，但因其核心功能和高评论数，需要尽快指派并定位根因。

-   **等待评审的架构性PR：**
    -   **PR #5067** `feat(driver): introduce Agent OS Driver`， **PR #5088** `feat: initial governance & sandbox interface disscussion`， **PR #4900** `Decouple plugin loader initialization from agent startup` - 这些PR是项目未来架构和生态发展的基础，应尽快完成评审，避免阻塞后续开发。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，这是基于 ZeroClaw (github.com/zeroclaw-labs/zeroclaw) 项目数据生成的 **2026-06-13 项目动态日报**。

---

## ZeroClaw 项目动态日报 (2026-06-13)

### 1. 今日速览

ZeroClaw 项目今日处于 **极高活跃度** 状态，尤其是在 Pull Request (PR) 提交方面，显示出密集的开发周期。社区提交了 **32 条 PR**，但合并/关闭的仅有 3 条，导致 PR 积压严重。核心开发团队正聚焦于 **架构统一 (RFC #7415)** 和 **V3 配置迁移** 的收尾工作，这些工作带来了大量关联的 Bug 修复和重构 PR。另一方面，用户报告的 Bug 数量激增，尤其是针对 **macOS 环境**、**Docker 构建** 和 **Web 仪表盘** 的问题，表明 v0.8.0 版本的稳定性和跨平台兼容性仍需加强。

### 2. 版本发布

*无新版本发布。*

### 3. 项目进展

今日项目在核心架构和关键集成方面取得了实质性进展，主要体现在以下重要 PR 的合并/关闭上：

-   **核心架构统一 (RFC #7415 实施):** [PR #7540](https://github.com/zeroclaw-labs/zeroclaw/pull/7540) 已合并。该 PR 将三个独立的 Agent 执行引擎 (`run_tool_call_loop`, `turn_streamed`, `Agent::turn`) 统一为一个，这是对维护者方向的直接响应，旨在简化核心逻辑并提升代码一致性。这一改动是项目进入 v0.9 阶段的关键一步。
-   **插件安装路径问题修复:** [PR #7549](https://github.com/zeroclaw-labs/zeroclaw/pull/7549) (状态: OPEN) 解决了 CLI 安装的 WASM 插件因安装路径与运行时扫描路径不一致而“隐形”的问题。此修复对 v0.8.1 的插件生态至关重要。
-   **Discord 网关意图 (Gateway Intents) 可配置化:** [PR #7524](https://github.com/zeroclaw-labs/zeroclaw/pull/7524) (状态: OPEN) 将 Discord 频道的硬编码网关意图改为基于配置的动态派生，提高了灵活性和对未来 Discord API 变化的适配能力。
-   `zeroclaw doctor` 诊断工具增强: [PR #7485](https://github.com/zeroclaw-labs/zeroclaw/pull/7485) 修复了 `doctor` 工具误报自定义模型提供者配置无效的问题，[PR #7544](https://github.com/zeroclaw-labs/zeroclaw/pull/7544) 则使其支持多 Agent 场景的检查。

### 4. 社区热点

今日社区讨论的焦点集中在两个问题上，反映了用户对 **核心可用性** 和 **清晰架构** 的关注：

-   **核心架构统一决议 ([#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)):** 该 RFC 虽未产生新的评论，但其直接产出 [PR #7540](https://github.com/zeroclaw-labs/zeroclaw/pull/7540) 的提交和合并是今日最重大的社区事件。这回应了社区长期以来对 Agent 执行逻辑复杂性的关切，是降低未来贡献门槛的关键重构。
-   **Web 仪表盘不可用 ([#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)):** 这是一个热度很高的 Bug 报告，收到 1 条评论。用户 `luckbyte` 报告通过 Homebrew 安装 v0.8.0 后，Web 仪表盘无法访问。这直接影响新用户的首次体验，导致 [PR #7529](https://github.com/zeroclaw-labs/zeroclaw/pull/7529) 被迅速提交以修复启动时日志的误导性。

### 5. Bug 与稳定性

今日报告了 **7 个** 新 Bug，其中 5 个严重等级为 S1 (工作流阻塞)，表明当前版本的稳定性面临压力。

**S1 - 工作流阻塞:**
-   **Web 仪表盘不可访问 ([#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)):** 用户通过 `brew install` 后无法打开仪表盘。
-   **macOS 应用完全失效 ([#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)):** 用户在 macOS 15.7.7 上安装后，应用无法获取权限，无响应，重启后窗口消失。**这是一个严重的平台性问题。**
-   **Docker 构建失败 ([#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533)):** 因缺少 C++ 编译器 (`g++`)，`cargo web build` 步骤失败。**已有对应 fix PR [#7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534)。**
-   **`ask_user` 工具在 WebSocket 会话中崩溃 ([#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542)):** Agent 通过 Web 仪表盘调用 `ask_user` 时立即失败。
-   **`zeroclaw quickstart` 命令失败 ([#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537)):** 新用户在 Windows 10 上执行入门命令时，因配置文件解析错误而失败。

**S2 - 行为降级:**
-   **V3 遗留路径问题 ([#7541](https://github.com/zeroclaw-labs/zeroclaw/issues/7541)):** `data_dir` 被错误地用作 Agent 的工作目录，而非共享数据目录，可能导致状态和模型文件混乱。

**其他:**
-   **Windows 更新功能缺陷 ([#7528](https://github.com/zeroclaw-labs/zeroclaw/issues/7528) 引发的修复):** 社区通过 [PR #7528](https://github.com/zeroclaw-labs/zeroclaw/pull/7528) 和 [#7530](https://github.com/zeroclaw-labs/zeroclaw/pull/7530) 修复了 Windows 平台上的自更新功能，解决了 `.zip` 资产未被识别的问题。

### 6. 功能请求与路线图信号

今日社区提出了 **4 个** 新功能请求，部分与当前路线图高度契合：

-   **Web UI 多会话支持 ([#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543)):** 用户 `NiuBlibing` 提出为 Web 聊天 UI 添加会话管理功能（新建/切换/重命名/删除）。这与项目增强 Web 仪表盘体验的路线图方向一致，很可能在 v0.9 或后续版本中被采纳。
-   **llama.cpp 模型路由器 ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)):** 请求支持快速切换不同的 llama.cpp 本地模型。这反映了本地部署用户对灵活性的需求。
-   **多平台流式卡片消息 ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)):** 为 QQ/DingTalk/WeChat/Feishu 等国内主流 IM 平台增加富文本卡片消息的流式输出支持，以减少用户等待焦虑。这是一个很强的中国市场需求信号。
-   **Twitch 频道集成 ([#6443](https://github.com/zeroclaw-labs/zeroclaw/issues/6443)):** 此前的功能请求今日被关闭，表明其对应的开发工作已完成。

### 7. 用户反馈摘要

从今日的 Issues 中，我们可以提炼出以下核心用户痛点：

-   **“开箱即用”体验不佳:** 来自新用户 `hejiangda` 的反馈，`zeroclaw quickstart` 命令在 Windows 上失败，显示“no map-keyed/list section at peer-groups”错误。这凸显了 **新手引导流程** 的脆弱性。
-   **核心功能不可用:** 用户 `luckbyte` 和 `swellee` 分别报告了 Web 仪表盘和 macOS 原生应用完全不可用的情况，这对用户体验是毁灭性的。特别是 macOS 用户，安装后应用直接“消失”，表明平台适配存在严重问题。
-   **配置与行为困惑:** 用户 `NiuBlibing` 发现 `data_dir` 的语义与文档和用户预期不符，暗示 V3 配置重命名后，部分遗留逻辑未完全清理干净的文档更新滞后。

### 8. 待处理积压

以下为长期存在且对项目有重要影响的 Issue/PR，需维护者优先关注：

-   ****[#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) **v0.8.1 集成/频道/提供者/工具 PR 队列追踪器:** 该追踪器创建于 2026-05-27，旨在管理 v0.8.1 版本的集成工作。尽管今日有多条 PR 提交，但该追踪器本身处于无评论状态，缺乏维护者更新，建议维护者定期总结进度。
-   **长期未处理的 S1 Bug:**  [PR #7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245) “修复 read_skill 无法加载插件捆绑的技能” 从 6 月 5 日提交后仍处于 `needs-author-action` 状态，这是一个影响插件生态的关键功能，需要作者或维护者推动。
-   **NEAR AI Cloud 提供者支持 ([#6842](https://github.com/zeroclaw-labs/zeroclaw/pull/6842)):** 该为提供者添加 `nearai` 支持的 PR 自 5 月 21 日提交后一直处于开放状态，虽然风险不高，但长期未合并会打击外部贡献者的积极性。

---

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*