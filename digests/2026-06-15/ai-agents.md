# OpenClaw 生态日报 2026-06-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-15 02:59 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是基于您提供的 OpenClaw 项目 GitHub 数据生成的 2026-06-15 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-15

## 1. 今日速览

今日 OpenClaw 项目活动量处于**极高**水平，24小时内共有 **500 条 Issues** 和 **500 条 PRs** 更新，显示出社区参与度非常活跃。然而，新开/活跃的 Issues（437条）远大于已关闭的（63条），待合并 PR（429条）也远多于合并/关闭的（71条），表明项目维护者面临**严重的处理积压**，且**平台稳定性问题**成为社区讨论的绝对焦点。绝大多数高热度 Issue 集中在**会话状态丢失、消息截断或重复、供应链/插件（如 Codex、MiniMax、DeepSeek、WhatsApp）接入异常**等核心功能体验问题上。尽管发布了 `v2026.6.8-beta.1` 版本，但新版本似乎并未解决多个已存在数周的 P0/P1 级 Bug，社区反馈存在一定的不满与焦虑。

## 2. 版本发布

**新版本：`v2026.6.8-beta.1`**
- **发布时间**：2026-06-15
- **主要亮点**：
    - **Telegram 和 WhatsApp 频道改进**：
        - Telegram 现支持发送带表格、列表、可展开引用块的富文本、提示保留的 CLI 后端交付、废弃的原生草稿迁移以及更安全的富媒体边界。
        - 发布说明中提及了 WhatsApp 的相关改进（但未提供细节）。

*注：破坏性变更与迁移注意事项未在摘要中提供，建议查阅完整 Release Notes。*

## 3. 项目进展

尽管有大量 PR 待处理，今日仍有部分关键修复取得进展：

- **WhatsApp 稳定性修复**：`#93076` (`fix(whatsapp): preserve auth on terminal disconnects`) 和 `#93094` (`fix(whatsapp): bound socket operations`) 两篇 PR 均获得维护者关注或进入准备合并状态。它们分别解决了 WhatsApp 在终端断开连接时的认证保留问题和操作超时问题，有望终结近期 WhatsApp 会话频繁中断的顽疾。
- **Feishu 飞书功能增强**：`#92340` (`feat(feishu): handle VC meeting invites`) 新增了对飞书视频会议邀请事件的处理，扩展了飞书频道的交互场景。
- **Gateway 安全加固**：`#85916` (`fix(gateway): require admin scope for browser proxy invoke`) 对浏览器代理调用增加了管理员权限校验，修复了一个潜在的越权安全边界问题。
- **内存/记忆文档对齐**：`#85899` (`docs(memory): align descriptors and docs with recursive memory/**/*.md`) 文档更新，使描述与实际递归读取 `memory/` 目录的行为保持一致，对插件开发者友好。

**项目整体向前迈进了**一步，特别是在 WhatsApp 和飞书频道层面，但核心服务层（Gateway、会话管理、模型调用）的严重问题仍未得到有效解决。

## 4. 社区热点

今日讨论最活跃的议题聚焦于**模型服务中断和消息静默丢失**两大痛点：

1.  **MiniMax 早高峰定时故障 (`#85888`)**：这是一个典型的“定时炸弹”问题。大量 Cron 作业在凌晨 5-7:30 点（北京时间）调用 MiniMax API 时持续 503 故障，但手动触发却成功。评论区高度活跃（12条），反映出**对 OpenClaw 调度机制与上游 API 交互的非透明性**的广泛质疑。用户认为问题不在 API 本身，而在 OpenClaw 的定时调度或连接池管理。 [链接](https://github.com/openclaw/openclaw/issues/85888)

2.  **Agent 回复被静默截断 (`#84516`)**：此问题收获了大量关注（11条评论，2个赞）。用户报告称，在无头模式下使用 Codex 代理时，回复内容总会在大约 1000-1100 字符时被静默截断，但模型返回的状态却是“未中止”。这种行为**极大地破坏了自动化流程的可靠性**，社区正在激烈讨论问题根源在于 Codex app-server 的处理还是 OpenClaw 的返回机制。 [链接](https://github.com/openclaw/openclaw/issues/84516)

3.  **模型 Fallback 链失效 (`#85103`)**：当主用模型（如 OpenAI Codex）限流后，配置好的 fallback 模型链未被正确触发，反而导致了 `EmbeddedAttemptSessionTakeoverError`。这违背了用户对高可用性的基本预期，质疑了架构设计中模型切换的逻辑健壮性。 [链接](https://github.com/openclaw/openclaw/issues/85103)

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在会话、消息、认证和安全领域，许多为**P0/P1 级严重问题**，但大多尚未有对应的 Fix PR。

| 严重程度 | Issue | 摘要 | 是否有 Fix PR | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | #84882 | `memory-core` 插件的梦境管线会**静默删除**日常记忆文件，导致关键数据永久丢失。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/84882) |
| **P1** | #84516 | **Codex 代理回复被静默截断**（<1100字符），影响自动化工作流。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/84516) |
| **P1** | #85103 | **模型 Fallback 链失效**，触发 `EmbeddedAttemptSessionTakeoverError`，导致服务不可用。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/85103) |
| **P1** | #84903 | 单一代理卡住（死锁）会**阻塞整个 Gateway 事件循环**，影响所有其他代理的可用性。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/84903) |
| **P1** | #91016 | 升级到 `2026.6.1` 后，DeepSeek 的 **Prompt Cache 完全失效**，导致推理成本飙升（每小时约$6）。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/91016) |
| **P1** | #85888 | **Cron 作业调用 MiniMax 定时 503 失败**，手动调同模型却成功，暗示调度层Bug。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/85888) |
| **P1** | #90886 | **Gateway 启动时挂起**，因为配置中声明了但未配置的 Provider 导致无法启动（回归）。 | 已关闭 | [链接](https://github.com/openclaw/openclaw/issues/90886) |
| **P1** | #85030 | **MCP 工具无法注入**到子代理（`sessions_spawn`）会话中，限制了插件生态系统的高级使用。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/85030) |
| **P1** | #81917 | `openclaw dashboard` 在日志中**泄露裸 URL（含 token）** ，并在特定环境下无法正常启动浏览器。 | 无 | [链接](https://github.com/openclaw/openclaw/issues/81917) |

## 6. 功能请求与路线图信号

本周社区提出的功能请求更趋务实，旨在解决现有痛点：

- **稳定的插件 SDK (`#81913`)**： 用户要求暴露稳定的插件 SDK 以支持安装的工作流技能（`skill workflows`），包括解析 `SKILL.md`、读取技能配置等。相关的 PR `#85664` (`wire read coding tool into HTTP /tools/invoke`) 正在审查中，预计这会成为下一版本的核心特性。
- **可配置的流模式切换 (`#74077`)**： 用户希望在聊天会话中通过 `/stream` 命令动态切换流模式，避免修改配置重启 Gateway，提升用户体验。
- **更好的记忆搜索 (`#44395`)**： 社区期待已久的 Heading-aware 分割和实体提取功能（`#44395`）仍在待办中，这能显著提升长文档的记忆检索精度。
- **图像生成成本可见性 (`#85461`)**： 用户希望图像生成提供商能返回消耗的成本和使用数据，以便进行预算监控。这是一个重要的可观测性需求。

**路线图信号**：`#81913` 和 `#44395` 这类与插件化和记忆系统深度相关的特性被标注为 P2 且已有 PR 关联，显示项目团队有意在下个里程碑推进，但短期重点仍在于修复上述 P1 级稳定性 Bug。

## 7. 用户反馈摘要

从今日的 Issues 评论中可以提炼出以下用户声音：

- **不满**：“升级后 Prompt Cache 失效，一小时烧掉我们$6，而且没任何警告！”（`#91016`）—— 对升级导致的功能降级和经济损失表示强烈不满。
- **困惑**：“Cron 作业失败，但手动触发就成功，这说不通啊。”（`#85888`）—— 用户对自动化作业和手动操作之间行为的不一致感到困惑和挫折。
- **焦虑**：“MCP 工具是我们构建复杂子代理的核心，但它完全无法工作。”（`#85030`）—— 高级用户在核心功能上受阻，影响了他们对平台扩展能力的信任。
- **赞赏**：“新的 `fast: auto` 模式文档写得不错”（源自 PR `#85104` 描述）—— 对部分清晰且有文档的功能设计表示肯定。
- **痛点**：“45000 行的记忆文件导致看板无法加载，后来发现是行数限制问题。”（源自 Issue 摘要）—— 暴露了在处理大规模个人记忆数据时的性能瓶颈。

## 8. 待处理积压

以下是一些长期未响应或未解决，但影响重大的问题，需要维护者重点关注：

1.  **`#45494 - Cron agent jobs silently time out...`** （创建于 3月13日）
    - **问题**：Cron 作业在上游 LLM API 返回明确错误时，不会快速失败，而是会耗尽整个 `timeoutSeconds` 窗口。
    - **关注度**：标记为 P1，但未被验证或分配。
    - **链接**： [Issue #45494](https://github.com/openclaw/openclaw/issues/45494)

2.  **`#56781 - Feature request: fallback model chain for compaction and LCM summaryModel`** （创建于 3月29日）
    - **问题**：压缩和总结模型不接受 fallback 链，导致单点故障。
    - **状态**：这是一项重要的可靠性和健壮性改进功能请求，但一直停留在 `pending triage`。
    - **链接**： [Issue #56781](https://github.com/openclaw/openclaw/issues/56781)

3.  **`#44395 - feat: heading-aware chunking + entity extraction for memory search`** （创建于 3月12日）
    - **问题**：改进记忆分块和搜索质量的长期功能请求。
    - **状态**：P2，已有 PR 关联但进展缓慢。这是提升个人 AI 助手记忆质量的关键功能。
    - **链接**： [Issue #44395](https://github.com/openclaw/openclaw/issues/44395)

**总结**：OpenClaw 项目社区活跃度极高，但项目健康度正面临严峻挑战。核心基础设施（模型 Fallback、Gateway 隔离性、消息传递可靠性）的多个 P0/P1 级 Bug 积累严重，且许多悬而未决达数周。新版本的发布未能有效缓解主要痛点。维护者需要立即投入资源解决这些核心稳定性问题，以避免社区信心进一步流失。

---

## 横向生态对比

# AI智能体开源生态横向对比分析报告（2026-06-15）

## 1. 生态全景

当前个人AI助手/自主智能体开源生态呈现“**高活跃、高痛点、强分化**”的态势。社区对**核心稳定性**（会话截断、模型Fallback失效、数据隔离）和**安全性**（Shell绕过、凭证泄露、权限滥用）的诉求空前集中，与此同时，**多模型提供商架构、插件化扩展、跨平台集成**成为各项目竞相发力的主赛道。用户不再满足于基础对话能力，而是要求Agent具备可靠的事务性执行能力和企业级合规性。项目间分化明显：头部项目在社区规模上遥遥领先，但普遍面临维护瓶颈；中小型项目则凭借垂直场景的深度优化快速崛起。

## 2. 各项目活跃度对比

| 项目 | Issues（新开/活跃） | PRs（待合并/合并） | 版本发布 | 健康度评估 |
|------|-------------------|-------------------|---------|-----------|
| **OpenClaw** | 437 / 63关闭 | 429 / 71 | v2026.6.8-beta.1 | ⚠️ 严重积压，核心稳定性问题多发 |
| **NanoBot** | 2新开 / 0关闭 | 46 / 28合并 | 无 | ✅ 稳健迭代，响应快速 |
| **Hermes Agent** | 约3条活跃 | 约5合并 | 无 | ✅ 稳定修复，安全加固积极 |
| **PicoClaw** | 5条（1新） | 9 / 5合并 | v0.2.9-nightly | 🟡 少量积压，关键Bug待解 |
| **NanoClaw** | 约8条 | 10 / 5合并 | 无 | 🟡 安全漏洞集中爆发，功能推进快 |
| **NullClaw** | 1条新开 | 0 | 无 | 🔴 极低活跃，近乎停滞 |
| **IronClaw** | 32 / 7关闭 | 27 / 17合并 | 无 | 🟢 极高活跃，安全议题激增 |
| **LobsterAI** | 0新开 | 3待合并 / 1合并 | 无 | 🔴 低活跃，维护模式 |
| **Moltis** | 1条新开 | 0 | 无 | 🔴 低活跃，技术探索期 |
| **CoPaw** | 16 / 1关闭 | 12待合并 / 0合并 | 无 | 🟡 高输入待消化，回归Bug严重 |
| **TinyClaw** | 0 | 0 | 无 | 🔴 无活动 |
| **ZeptoClaw** | 0 | 0 | 无 | 🔴 无活动 |
| **ZeroClaw** | 42 / 28关闭 | 约50 / 约20合并 | 无 | 🟢 极高活跃，功能扩展迅猛 |

## 3. OpenClaw在生态中的定位

OpenClaw仍是生态中**社区规模最大、Issue/PR基数最高的项目**，但也是**稳定性挑战最严峻**的项目。其优势在于：多通道集成（Telegram、WhatsApp、飞书）、丰富的插件生态（Codex、MiniMax等）以及持续快速的版本迭代。然而，437条开放Issue与429条待合并PR表明维护能力已严重滞后于社区贡献速度，多个P0/P1级Bug（如记忆静默删除、模型Fallback失效、Gateway事件循环阻塞）持续数周未修复，导致用户信任度下滑。

相比之下，**NanoBot**和**Hermes Agent**的社区规模虽小（各自日均数十条PR），但维护响应更及时，Bug-修复闭环效率更高。**ZeroClaw**则展现出极强的“吞并式”发展态势，单日关闭28条Issue、合并大量集成PR，生态扩张速度惊人。**OpenClaw正从“全能标杆”向“规模陷阱”过渡**，若不能迅速提升维护效率，其生态中心地位可能受到侵蚀。

## 4. 共同关注的技术方向

以下为多个项目同期涌现的共性诉求（按热度排序）：

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|----------|
| **模型Fallback/供应高可用** | OpenClaw #85103、NanoClaw #2751、PicoClaw #2978 | 主用模型限流/失败时自动切换备用模型链，避免服务中断或静默降级 |
| **会话/记忆数据隔离** | Hermes #46303、OpenClaw #84882、CoPaw #5171 | 多会话数据交叉污染、记忆文件被静默删除、上下文压缩导致信息丢失 |
| **安全审计与权限最小化** | IronClaw #4861-4865、NanoClaw #2760-2762、Hermes #46413 | Shell工具绕过风险、文件读取越权、本地网关授权缺失 |
| **WebUI配置管理一体化** | NanoBot #4313、PicoClaw #3118、ZeroClaw #7594 | WebUI与配置文件深度同步，支持无需重启的动态配置变更 |
| **插件/通道扩展标准化** | OpenClaw #81913、PicoClaw #3120、NanoClaw #2760 | 稳定的插件SDK、第三方通道注册钩子、工具注入机制 |
| **边缘/气隙部署支持** | ZeroClaw #6293、Moltis #1123、CoPaw #5183 | 离线Agent容器、纯Rust后端、低资源环境兼容 |
| **长文本处理与记忆搜索** | OpenClaw #44395、Hermes #7237、CoPaw #5171 | Heading-aware分块、实体提取、长响应截断优化 |

## 5. 差异化定位分析

| 维度 | OpenClaw | NanoBot | Hermes | ZeroClaw | CoPaw |
|------|---------|--------|--------|---------|-------|
| **功能侧重** | 全能型个人助手（多通道+插件+记忆） | 轻量级高效能Agent（WASM插件+快速迭代） | 安全优先的企业级Agent（凭证隔离+审计） | 生态集成枢纽（SMS/智能家居/流媒体等） | 桌面自动化+多Agent协作（Windows GUI驱动+团队模式） |
| **目标用户** | 技术爱好者+早期采用者 | 开发者/DevOps工程师 | 安全敏感型企业/合规团队 | 想要“万物互联”的极客/非技术用户 | 国内开发者（钉钉/飞书/微信生态） |
| **技术架构** | Python后端+TypeScript前端 | Go+WASM运行时 | Rust+类型驱动配置 | Rust+WebUI（全栈Rust） | Python+Electron+Tauri |
| **社区风格** | 大规模但维护滞后 | 小而精，响应快 | 专业严谨，安全驱动 | 激进扩张，生态合作为主 | 本地化强，插件贡献活跃 |

## 6. 社区热度与成熟度分层

**第一梯队（极高活跃，面临规模挑战）**：OpenClaw、ZeroClaw、IronClaw。日均Issue/PR超30条，社区贡献者众多，但OpenClaw的积压问题突出，ZeroClaw和IronClaw正处于功能快速合并期，需警惕维护债务积累。

**第二梯队（高活跃，迭代稳健）**：NanoBot、Hermes Agent、CoPaw。日均贡献5-20条PR，团队维护响应快，Bug修复效率高，属于“质量优先”模式。Hermes在安全领域形成专业口碑，NanoBot以极简架构吸引开发者。

**第三梯队（中等活跃，特定方向深耕）**：PicoClaw、NanoClaw。社区规模中等，前者聚焦边缘计算场景，后者在多Agent提供商架构上快速突破。安全漏洞的集中报告表明其正在经历“成长痛”。

**第四梯队（低活跃，维护/探索期）**：NullClaw、LobsterAI、Moltis、TinyClaw、ZeptoClaw。长期无新版本或活跃贡献，社区增长停滞，可能面临被淘汰风险。

## 7. 值得关注的趋势信号

1. **安全成为第一性原理**：IronClaw、NanoClaw、Hermes几乎同时爆发Shell绕过、凭证泄露等安全问题，说明Agent自主操作权限的边控制尚不成熟。未来项目必须内置“默认拒绝”的安全模型，否则将失去企业用户。

2. **多通道集成从“加分项”变为“入场券”**：ZeroClaw单日合并15+新SMS和IoT集成，表明用户期望Agent能连接一切。项目必须在核心稳定基础上快速构建通道适配器生态，否则将被新兴项目超越。

3. **记忆系统仍是最大薄弱点**：OpenClaw的梦境管线静默删记忆、CoPaw的上下文压缩失效、Hermes的会话污染，共同指向Agent长期记忆的可靠性远未达标。这不只是Bug，而是技术范式的缺失。

4. **开发者体验决定社区活力**：NanoBot通过快速合并PR、OpenClaw因积压导致社区不满。项目的“有效反馈率”将成为衡量健康度的关键指标。维护者应优先处理那些能让贡献者“看到结果”的PR，而非仅盯新增功能。

5. **Rust语言在Agent基础设施层崛起**：ZeroClaw、Moltis、Hermes均采用Rust构建核心，PicoClaw也趋向于Rust原生。Rust在性能、安全、跨平台上的优势使其成为下一代Agent引擎的首选语言。开发者若涉足底层框架，应优先掌握Rust。

---

*报告基于2026年6月15日各项目GitHub公开数据，数据分析由AI辅助完成，供技术决策者参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的NanoBot项目GitHub数据，我已为您生成2026年6月15日的项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-15

#### 1. 今日速览

本日项目活跃度极高，主要集中在Bug修复和代码质量改善上。过去24小时内，社区提交了46个拉取请求（PR），其中28个已合并或关闭，显示出强大的开发动能。同时，两个新报告的Bug（涉及API返回值和图像处理）引发了关注，并已迅速有对应的修复PR提交。项目整体在提升稳定性、完善WebUI功能以及重构核心架构方面取得了显著进展。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日项目核心架构和功能模块迎来重要更新。关键进展如下：

- **WebUI与配置同步**：[PR #4313](HKUDS/nanobot PR #4313) 已合并，实现了WebUI设置面板与`config.json`的深度同步，新增了多项设置写入接口和UI控件，极大改善了可用性和配置一致性。
- **桌面客户端稳定性**：[PR #4210](HKUDS/nanobot PR #4210) 已合并，修复了桌面端重启后令牌失效和WebSocket回放丢失消息的问题。
- **核心配置与工具系统重构**：包含[PR #4314](HKUDS/nanobot PR #4314)（打破工具配置模块循环导入）和[PR #4344](HKUDS/nanobot PR #4344)（重构配置与代理循环边界）在内的一系列重构PR被合并，提升了代码可维护性和模块化程度。
- **提示历史与Agent行为优化**：[PR #4274](HKUDS/nanobot PR #4274) 已合并，按会话范围限制最近历史记录，避免跨会话的上下文污染。 [PR #4269](HKUDS/nanobot PR #4269) 优化了Agent在达到最大迭代次数时的用户反馈。
- **快速失败机制**：[PR #4275](HKUDS/nanobot PR #4275) 已合并，当配置文件无效时将快速报错并退出，而非静默使用默认值，有助于用户尽早发现配置问题。

#### 4. 社区热点

尽管单一Issue的评论数不高，但大量高质量PR的涌入和快速合并表明社区参与度非常高。其中，关于**WebUI与配置同步**的 [PR #4313](HKUDS/nanobot PR #4313) 和关于 **Agent与子代理协作**的 [PR #4293](HKUDS/nanobot PR #4293) 是开发者关注的焦点。前者反映了用户对更完善、更直观的配置管理界面的强烈需求；后者则揭示了在生产环境中对复杂任务编排（如定时任务触发子代理）能力的期待。此外，[PR #4330](HKUDS/nanobot PR #4330) 新增的**自动化管理视图**功能，也预示着项目在任务自动化和系统管理方面迈出了重要一步。

#### 5. Bug 与稳定性

今日上报了2个新Bug，其中1个已附带修复PR，整体响应迅速。

- **严重**：**API返回零使用量** - [Issue #4309](HKUDS/nanobot Issue #4309) 指出 `/v1/chat/completions` 端点始终返回 `0` tokens用量，这对于依赖用量统计的应用来说是关键缺陷。目前仍为开放状态。
- **严重**：**图像回退机制导致路径泄露** - [Issue #4345](HKUDS/nanobot Issue #4345) 报告了一个安全与功能性问题：当模型拒绝图像输入时，系统在移除图像块后，会向模型泄露本地文件路径。此问题已由修复PR [PR #4346](HKUDS/nanobot PR #4346) 跟进，方案是将其标记为“不可见”而非泄露路径。
- **较严重（已修复）**：**Anthropic提供者API兼容性** - [Issue #4333](HKUDS/nanobot Issue #4333) 报告了发送已废弃的 `temperature` 参数到新模型导致400错误的问题，已在过去24小时内关闭。

#### 6. 功能请求与路线图信号

从今日数据看，社区和开发团队对以下方向表现出明确兴趣：

- **增强WebUI管理能力**：除已合并的配置同步外，新提交的 [PR #4330](HKUDS/nanobot PR #4330) （自动化管理视图）和 [PR #4339](HKUDS/nanobot PR #4339) （移动端响应式优化）是重要的路线图信号，表明WebUI正从基础使用向全面管理平台演进。
- **精细化工具控制**：已合并的 [PR #4273](HKUDS/nanobot PR #4273) （`pathPrepend`配置）和新提交的 [PR #4343](HKUDS/nanobot PR #4343) （拒绝未知工具参数）预示着对工具执行环境的控制将变得更加严格和灵活。
- **用户界面个性化**：已关闭的[Issue #4262](HKUDS/nanobot Issue #4262)关于在Agent模式启动时使用自定义机器人图标（`botIcon`）的请求，尽管当前无对应PR，但反映出用户对个性化UI的期待，可能在未来版本中被纳入考量。

#### 7. 用户反馈摘要

- **API兼容性痛点**：[Issue #4309](HKUDS/nanobot Issue #4309) 的用户 `alx1379` 反馈OpenAI兼容API的Token统计缺失，这对于依赖成本监控和用量优化的用户是个显著障碍。
- **安全顾虑**：[Issue #4345](HKUDS/nanobot Issue #4345) 的用户 `BearMett` 指出图像退避机制可能意外地向模型透露本地文件路径，这是一个很好的安全发现，修复PR [PR #4346](HKUDS/nanobot PR #4346) 也已迅速响应。
- **配置管理与易用性**：[PR #4313](HKUDS/nanobot PR #4313) 的合并，本身就在积极响应社区长期以来的一个痛点：WebUI与配置文件修改之间存在“鸿沟”，导致行为不一致。此PR的合并将显著提升用户体验。
- **模型兼容性**：[Issue #4333](HKUDS/nanobot Issue #4333) 指出对Anthropic新模型（Opus-4-8）的兼容性问题，暴露出提供者适配代码需要更灵活地跟随上游API变化。

#### 8. 待处理积压

- **0 tokens使用量Bug**：[Issue #4309](HKUDS/nanobot Issue #4309) 作为新发现的严重Bug，目前仍无处理标签和关联的修复PR，需要维护者优先关注。
- **子代理执行依赖**：[PR #4293](HKUDS/nanobot PR #4293) 添加了 `pending_queue` 支持以修复子代理结果注入问题，当前为开放状态。此修复对定时任务（Cron）等场景至关重要，应加速审查与合并。
- **核心重构收尾**：[PR #4344](HKUDS/nanobot PR #4344)（配置/代理循环重构）作为大的结构性变更，需要社区和核心维护者的仔细审查，以确保不会引入回归问题。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-15

## 今日速览

项目今日维持高活跃度，主要聚焦于**安全加固**、**跨会话数据隔离**和**平台适配性修复**。社区反馈集中在 Web 搜索后门路由、会话交叉污染和桌面端 UI/UX 体验上。开发者积极响应，已针对多个严重 Bug 提交了修复 PR，并对长期积压的测试覆盖率问题进行了清理。总体来看，项目处于**稳定迭代**阶段，但安全与数据隔离问题是当前重点。

## 项目进展

今日合并/关闭的 PR 主要围绕安全、基础设施和平台适配进行加固和修复。

- **安全与权限加固**：
    - **PR #46422** 和 **PR #46425**（已合并）：`fix(workflows): harden token permissions`。对 GitHub Actions 工作流的 Token 权限进行了最小化限制，将写入权限下放至特定 Job，并对只读 Job 禁用凭据持久化，提升了 CI/CD 流水线的安全性。
    - **PR #45915**（已合并）：`fix(mcp): validate tool timeout config values`。为 MCP 服务器工具的超时配置添加了类型校验和清理，防止因无效超时值导致（例如字符串、负数）的异常行为。

- **平台适配与数据修复**：
    - **PR #46387**（已合并）：`fix(signal): preserve document attachments`。修复了 Signal 平台非媒体文件（如文档）被错误丢弃的问题，确保附件能正确缓存并传递给 Agent。
    - **PR #46389**（已合并）：`fix(signal): scope group target parsing to Signal targets`。修正了 `group:` 目标解析的范围，防止在非 Signal 平台上错误解析该语法。

- **维护与测试**：
    - **Issue #36515**（已关闭）：`Improve test coverage: plugins/web/parallel/provider.py`。该 Issue 关注模块覆盖率低于 70% 的问题（22.52%），今日被关闭，意味着相关代码的测试覆盖得到改善。

## 社区热点

1.  **[#45058] web_search/web_extract silently routes to Parallel.ai without user opt-in**（评论:7，👍:15）
    - **链接**: [Issue #45058](https://github.com/NousResearch/hermes-agent/issues/45058)
    - **分析**: 这是今日社区反应最激烈的 Issue。用户发现 Web 搜索和提取工具在用户未配置任何后端的情况下，会**静默地将流量路由到 Parallel.ai**。这是严重的隐私和透明度问题，社区担心数据在不经同意的情况下被发送给第三方。高赞数（👍15）表明这是社区广泛关注的隐私痛点，开发者需尽快给出明确说明或配置选项。

2.  **[#7237] Error: Response truncated due to output length limit**（评论:46，👍:6）【已关闭】
    - **链接**: [Issue #7237](https://github.com/NousResearch/hermes-agent/issues/7237)
    - **分析**: 这是今日讨论最活跃的 Issue（46条评论）。用户报告在生成长文本响应时，Agent会因“输出长度限制”而截断输出。该问题虽已关闭，但其高评论量反映出用户在生成长文档、代码或分析报告时遇到的普遍障碍，是个影响核心体验的关键痛点（该 Issue 创建于 4月，今日更新）。

3.  **[#44140] Desktop GUI — auto-scroll, sidebar overlap fix, custom session groups**（评论:3，👍:3）
    - **链接**: [Issue #44140](https://github.com/NousResearch/hermes-agent/issues/44140)
    - **分析**: 代表了桌面端用户对 UI/UX 改进的集中诉求。自动滚动、侧边栏遮挡等问题虽然微小，但严重影响了日常使用流畅度。3个点赞反映了该功能需求有一定社区基础。

## Bug 与稳定性

今日报告的 Bug 涉及多个方面，按严重程度排列：

- **P1（严重）** | **会话数据交叉污染**
    - **Issue #46303**: `Concurrent sessions cross-contaminate`。多个并发会话（包括桌面与桌面、桌面与CLI之间的会话）共享内存注入和 Git 工作目录，导致数据污染。这是底层架构问题，影响数据隔离和安全。
- **P1（严重）** | **Matrix 平台消息丢失**
    - **Issue #46310**: `send_message Matrix (media) path reconnects + re-inits E2EE per message`。每次发送媒体消息都重建 E2EE 连接，会耗尽接收方 one-time keys，在高频发送时导致消息静默丢失。这是平台适配的严重 Bug。
- **P2（中危）** | **安全漏洞**
    - **Issue #46413** (现已存在 修复PR #46430): `Desktop file preview can read Hermes credential stores`。桌面端文件预览功能可读取本应用的凭证存储文件。
    - **Issue #46411**: `read_file can exfiltrate credential stores from sibling profiles`。`read_file` 工具可越权读取其他 Profile 的凭证文件。
- **P3（低危）** | **性能退步**
    - **Issue #46090**: `Agent becoming extremely slow for basic tasks`。用户发现 Agent 在执行基础任务时变得异常缓慢，怀疑与上下文增长和压缩策略有关。
- **P3（低危）** | **Windows 兼容性**
    - **Issue #46332 (Duplicate)**: `Cron jobs with .sh scripts fail`。在原生 Windows 环境中，Cron 任务执行 `.sh` 脚本失败，原因是错误地选择了 WSL 的 Bash 而非 Git Bash。

## 功能请求与路线图信号

- **高优先级呼声：内存与插件集成**
    - **Issue #46253**: `GBrain as memory provider plugin`。用户希望将 GBrain 这样的语义记忆后端与 Hermes 的 `memory` 工具管道深度集成。这反映了社区对更强大、可插拔的记忆管理系统的需求。
    - 现有 **PR #46428**（`feat: add recursive large-context workflow`）展示了开发方正在朝外部化上下文、支持更大上下文窗口的方向探索，这与社区对于长文本处理和记忆管理的需求高度吻合。

- **桌面端 UI/UX 改进**
    - **Issues #44140, #45103, #46304** 等持续反映社区对桌面端 UI/UX 有大量改进需求，包括自动滚动、AI 摘要侧边栏、隐藏未配置 Provider 的选项等。维护者可考虑在下一个大版本中集中处理这些反馈。

- **外部服务平台集成**
    - **Issue #41553**: `Integration / Official Support for Hermes Workspace`。社区工具 `hermes-workspace` 正在发展壮大，用户希望获得官方支持。这可能是未来扩展生态系统的重要信号。

## 用户反馈摘要

- **痛点**：
    - **配置不透明与隐私担忧**：用户对 `web_search` 静默切换到 Parallel.ai（#45058）感到不安。
    - **数据隔离不足**：多会话（#46303）和多 Profile（#46411）间的数据交叉污染是明确的安全风险。
    - **平台兼容性问题**：Windows 用户报告 Git Bash 选择逻辑错误（#46332）和 Docker 环境下的 Token 冲突（#45963）。
    - **性能退化**：有用户报告 Agent 变得异常缓慢（#46090），严重影响了使用体验。
- **期望**：
    - **安全性**：用户期望默认配置是安全和透明的，并强烈要求增加安全审计。
    - **更智能的长文本处理**：用户希望解决长响应截断（#7237）问题，并期待更大上下文窗口的解决方案。
    - **更流畅的桌面体验**：对自动滚动、侧边栏遮挡等细枝末节的改进有很高呼声，这些“小问题”是提升用户满意度的关键。

## 待处理积压

- **长期未响应的重大 Issue**:
    - **Issue #7237**: `Error: Response truncated due to output length limit`。虽已关闭，但其核心问题（长文本处理）仍未从根源解决。建议提供一个官方的路线图或策略说明，回应社区关切。
- **长期未解决的配置问题**:
    - **Issue #23094**: `Make fallback session-stickiness configurable`。创建于5月10日，讨论回退机制的粘性行为，至今仍在开放状态，无明确进展。这表明一个被用户期望的功能点尚未进入开发视野。
- **需关注的安全相关 PR**:
    - **PR #46430**: `fix(desktop): block Hermes credential stores in file preview IPC`。该 PR 针对严重的安全漏洞（#46413）提出了修复方案，但截至目前状态为 `OPEN`。建议优先合并，以解决暴露的凭证泄露风险。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 (2026-06-15)

---

## 1. 今日速览

过去24小时项目保持高度活跃，共处理5条Issue、9条Pull Request，并发布了一个不稳定的Nightly构建版本（v0.2.9-nightly）。社区提交了多个功能性PR（远程Agent模式、第三方通道扩展等），同时暴露了两个关键的Stale Bug（MCP子命令解析错误、Matrix用户ID过滤失效）和一个新报告的Web搜索工具失效问题。维护者合并了5个修复类PR，主要集中于资源清理和日志一致性改进。整体健康度良好，但部分长期Bug仍未修复，建议优先处理。

---

## 2. 版本发布

- **[nightly] v0.2.9-nightly.20260615.13a38bd1**  
  自动构建的Nightly版本，可能不稳定，建议谨慎使用。  
  **完整变动日志**：[compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  无破坏性变更或迁移注意事项说明。

---

## 3. 项目进展

### 合并/关闭的重要PR（5个）

- **#2904 — Fix agent loop reload and panic cleanup stability**（已合并）  
  修复了 `pkg/agent` 中三个问题：`ReloadProviderAndConfig` 不再创建分离goroutine、使用同步 `defer/recover` 消除阻塞goroutine风险、以及 panic 清理稳定性。  
  [链接](https://github.com/sipeed/picoclaw/pull/2904)

- **#3124 — fix(tts): handle io.ReadAll error in error response path**（已合并）  
  TTS API 非200响应时，`io.ReadAll` 的异常返回将不再被静默忽略，改为记录诊断信息。  
  [链接](https://github.com/sipeed/picoclaw/pull/3124)

- **#3123 — fix(filesystem): explicitly ignore Close() error on directory file descriptor**（已合并）  
  目录文件描述符关闭错误显式忽略（`_ =`），统一代码风格。  
  [链接](https://github.com/sipeed/picoclaw/pull/3123)

- **#3122 — fix(evolution): capture Close() error on write file in appendJSONLRecords**（已合并）  
  `appendJSONLRecords` 中延迟关闭文件不再丢弃错误，避免延迟写入失败（如磁盘满、NFS错误）被静默吞掉。  
  [链接](https://github.com/sipeed/picoclaw/pull/3122)

- **#3121 — refactor(openai_compat): replace log.Printf with structured logger**（已合并）  
  移除文件内唯一的 `log.Printf` 调用，改为结构化日志，删除不再需要的 `log` 导入。  
  [链接](https://github.com/sipeed/picoclaw/pull/3121)

**总结**：项目在稳定性（agent重启、资源关闭错误处理）和代码可维护性（日志结构化）方面取得了明确进展。

---

## 4. 社区热点

今日社区讨论热度一般，以下条目有用户互动：

- **#2978 — [CLOSED] Add omniroute as provider**  
  [链接](https://github.com/sipeed/picoclaw/issues/2978)  
  用户请求添加Omniroute作为Provider，并询问如何自行配置。该Issue有2条评论，但在昨日被标记为`stale`并关闭。社区对此功能仍有潜在需求。

- **#3044 — [OPEN] Bug: allow_from fails for Matrix user IDs containing colon**  
  [链接](https://github.com/sipeed/picoclaw/issues/3044)  
  用户报告标准Matrix用户ID（`@localpart:domain`）在 `allow_from` 中无效，消息被静默拒绝。有1条评论，但尚未被修复。

- **#3041 — [OPEN] `mcp add` mis-parses global flags into positionals**  
  [链接](https://github.com/sipeed/picoclaw/issues/3041)  
  用户提供详细复现步骤：`picoclaw --no-color mcp add -t http ...` 时全局标志被误解析为位置参数，导致HTTP/SSE服务器添加失败，stdio服务器被错误命名。已有1条评论。

**分析**：社区关注的焦点集中在配置兼容性与命令行行为正确性上，尤其是MCP子命令的Flag解析问题（#3041）和Matrix用户ID格式兼容（#3044）这两个Stale Bug影响了实际使用。

---

## 5. Bug与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 修复状态 |
|----------|-------|------|----------|
| **高** | [#3125](https://github.com/sipeed/picoclaw/issues/3125) (NEW) | `web_search` 工具在迁移至 `.security.yml` 后静默失败，LLM调用返回“No results” | 无关联PR |
| **高** | [#3044](https://github.com/sipeed/picoclaw/issues/3044) (Stale) | Matrix频道 `allow_from` 过滤不识别含冒号的用户ID，消息被静默拒绝 | 无PR |
| **中** | [#3041](https://github.com/sipeed/picoclaw/issues/3041) (Stale) | `mcp add` 子命令错误解析全局flags，导致HTTP/SSE添加失败、stdio命名错误 | 无PR |
| **低** | [#3090](https://github.com/sipeed/picoclaw/issues/3090) (Stale) | Panel在iOS Safari < 16.4上无法工作（登录后白屏） | 无PR |

**说明**：今日新报告的#3125影响核心搜索功能，需优先排查。其余三个Stale Bug已存在一周以上，建议本周内给出回应或修复。

---

## 6. 功能请求与路线图信号

| 功能请求 | 类型 | 可能纳入下一版本的理由 |
|----------|------|------------------------|
| [#2975](https://github.com/sipeed/picoclaw/pull/2975) — Telegram回复视为@提及 | PR (待合并) | 实现简单，社区有用例，PR已有代码 |
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) — 远端Pico WebSocket模式 | PR (待合并) | 扩展agent使用场景，通过WebSocket远程连接 |
| [#3120](https://github.com/sipeed/picoclaw/pull/3120) — out-of-tree channel注册钩子 | PR (待合并) | 提升架构可扩展性，允许第三方模块无需fork即可接入 |
| [#2978](https://github.com/sipeed/picoclaw/issues/2978) 添加Omniroute Provider（已关闭） | Issue | 虽已关闭，但用户强烈表达需求；若PR #3120合并，可简化第三方provider添加流程 |

**路线图信号**：项目正朝着**更灵活的通道/Provider扩展**（PR #3120）和**agent远程控制**（PR #3118）方向推进。这两个PR如果合并，将显著提升PicoClaw的生态扩展能力。

---

## 7. 用户反馈摘要

从今日Issue评论中提炼的用户痛点：

- **#3044**（Matrix用户）：`allow_from` 配置与标准Matrix用户ID格式不兼容，导致私信被静默拒绝，用户无法自行排查原因。
- **#3041**（MCP用户）：执行 `mcp add` 时由于全局标志解析错误，添加HTTP/SSE服务器完全失败，且stdio服务器被错误命名（例如添加 `--name myserver` 实际注册为 `myserver` 而非预期值）。
- **#3090**（移动用户）：iOS 16.4以下Safari无法使用Panel登录后无响应，限制了低版本iOS设备的访问。
- **#3125**（搜索功能用户）：迁移API密钥到 `.security.yml` 后 `web_search` 工具完全失效，LLM虽识别但后端无结果返回，影响对话搜索能力。

没有收到积极的“满意”反馈，表明用户当前遇到的问题多于好评。建议维护者重点回应以上痛点，尤其是 #3125 和 #3044 可复现性明确。

---

## 8. 待处理积压

以下Issue/PR长期未获得维护者回应或合并，建议重点关注：

- **#3044**（Bug，6月7日创建，14天无回复） — Matrix allow_from 失效  
  [链接](https://github.com/sipeed/picoclaw/issues/3044)
- **#3041**（Bug，6月7日创建，14天无回复） — MCP add 标志解析错误  
  [链接](https://github.com/sipeed/picoclaw/issues/3041)
- **#3090**（Bug，6月10日创建，11天无回复） — Panel Safari兼容性  
  [链接](https://github.com/sipeed/picoclaw/issues/3090)
- **#2975**（PR，5月30日创建，16天未合并） — Telegram回复视为提及  
  [链接](https://github.com/sipeed/picoclaw/pull/2975)
- **#3118**（PR，6月12日创建，3天无评论） — 远端WebSocket agent模式  
  [链接](https://github.com/sipeed/picoclaw/pull/3118)
- **#3120**（PR，6月14日创建，1天） — 第三方通道钩子  
  [链接](https://github.com/sipeed/picoclaw/pull/3120)

以上积压中，#3044 和 #3041 已超过两周无维护者回应，社区可能因此产生挫败感；#2975 和 #3118 功能清晰且代码质量较好，建议在下个稳定版之前合并。

---

**日报生成时间**：2026-06-15 | **数据来源**：PicoClaw GitHub ([github.com/sipeed/picoclaw](https://github.com/sipeed/picoclaw))

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 NanoClaw 项目 GitHub 数据生成的 2026-06-15 项目动态日报。

---

## NanoClaw 项目动态日报 | 2026-06-15

### 1. 今日速览
项目今日呈现出极高的社区活跃度，矛盾主要集中在**安全性、功能缺陷和文档维护**三个维度。安全审计方面，社区报告了三个高危漏洞（#2760, #2761, #2762），涉及文件泄露、授权绕过等核心安全问题，且目前均无已合并的修复PR，需项目方高度关注。与此同时，项目功能迭代依然迅速，Codex Agent Provider 的重大重构（#2757）和预算错误提示机制（#2759）等重要PR已合并或提出，显示项目在快速前进。总体来看，项目健康度处于“**高活跃但面临严重安全挑战**”的状态。

### 2. 版本发布
- 过去24小时无新版本发布。

### 3. 项目进展
今日项目在核心功能和基础设施方面有显著推进，共合并/关闭了5个PR，另有5个PR待合并。

- **核心功能演进**
    - **Codex Agent Provider V2** [PR #2757] *(已关闭-已合并)*：这是一个重量级更新，将Codex打造成一个完整的Agent Provider，运行在宿主的能力接缝（capability seams）上，并通过OneCLI进行仅限Vault的身份验证。这是项目向“多Agent提供商”架构演进的关键一步。
    - **Operator驱动的提供商切换** [PR #2756] *(已关闭-已合并)*：实现了由操作员（operator）显式选择、切换和迁移Agent提供商的机制。这为未来用户灵活选择不同后端模型（如Anthropic, Codex等）奠定了基础。
    - **基础设施与DevOps**
        - **数据驱动的CLI安装** [PR #2758] *(已关闭-已合并)*：将Dockerfile中硬编码的CLI工具安装改为由`cli-tools.json`数据清单驱动，使添加新CLI工具更加便捷和可维护。

- **文档与修复**
    - **修复CLAUDE.md中错误的文件路径** [PR #2764] *(已关闭-已合并)* & [PR #2769] *(已关闭-已合并)*：修复了`CLAUDE.md`文档中指向两个已迁移源文件的错误路径，并更新了Codex的交互式认证文档。这体现了社区对项目文档质量的关注。

- **待合并的重要PR**：
    - **预算/计费错误提示** [PR #2759] *(待合并)*：修复了LLM预算耗尽时提示信息被静默丢弃的缺陷。
    - **健康审计加固** [PR #2732] *(待合并)*：根据多项Agent健康审计发现，对核心Host和Agent Runner进行安全加固。

### 4. 社区热点
今日社区讨论和关注的焦点高度集中于安全领域，以及长期未解决的UX问题。

- **三大安全漏洞报告**：由用户 `YLChen-007` 提交的三个安全漏洞（[#2762](https://github.com/nanocoai/nanoclaw/issues/2762), [#2761](https://github.com/nanocoai/nanoclaw/issues/2761), [#2760](https://github.com/nanocoai/nanoclaw/issues/2760)）无疑是今日热点。这些报告在短时间内集中爆发，且描述详细，揭示了项目在`add_mcp_server`流程（隐藏参数）、本地网关（授权绕过）和文件读取（绝对路径遍历）等方面的严重设计缺陷。社区对此高度敏感，反映出用户对Agent安全性的核心诉求。

- **预算错误静默丢弃**：[Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751) 虽然并非今日新开，但其对应的修复PR ([#2759](https://github.com/nanocoai/nanoclaw/pull/2759)) 今日提出，引起了关注。该问题描述了一个严重影响用户体验的缺陷：当LLM调用因预算耗尽而失败时，用户得不到任何反馈，以为自己被“无视”。这直接关系到Agent“智能体”的基本可用性问题——反馈的透明性。

### 5. Bug 与稳定性
今日报告的 Bug 主要集中在安全漏洞和功能性缺陷，按严重程度排列如下：

- **【严重】安全漏洞**
    - **任意本地文件泄露** [Issue #2760](https://github.com/nanocoai/nanoclaw/issues/2760)：`send_file` MCP工具可读取任意绝对路径文件，有巨大的信息泄露风险。**目前无已合并的修复PR。**
    - **本地网关授权绕过** [Issue #2761](https://github.com/nanocoai/nanoclaw/issues/2761)：本地 webhook 未验证发送者身份，可被利用绕过审批流程。**目前无已合并的修复PR。**
    - **MCP服务器隐藏参数注入** [Issue #2762](https://github.com/nanocoai/nanoclaw/issues/2762)：`add_mcp_server` 的审批流不显示 `args` 和 `env`，可能被恶意Agent利用注入危险参数。**目前无已合并的修复PR。**

- **【高】功能性缺陷**
    - **预算耗尽时无反馈** [Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)：预算用尽时，LLM调用错误被静默丢弃，用户无感知。**已有修复PR** ([#2759](https://github.com/nanocoai/nanoclaw/pull/2759)) *待合并*。

- **【中】性能与功能缺失**
    - **Claude Provider 未启用提示缓存** [Issue #2768](https://github.com/nanocoai/nanoclaw/issues/2768)：导致每次对话都需要重发完整的系统提示，对含有复杂系统提示的Agent场景影响较大，增加成本和延迟。
    - **Codex 文件事件未传递** [PR #2770](https://github.com/nanocoai/nanoclaw/pull/2770) *(待合并)*：修复Codex生成的图片文件无法传递给聊天界面的问题。

### 6. 功能请求与路线图信号
今日的功能请求信号已明确指向**更安全、更智能、更易用的多提供商架构**。

- **多提供商架构的落地**：[PR #2756](https://github.com/nanocoai/nanoclaw/pull/2756) 和 [PR #2757](https://github.com/nanocoai/nanoclaw/pull/2757) 的合并，表明“多Agent提供商”不再是一个设想，而是成为项目当前版本的核心功能。未来用户可以期待在Claude、Codex等多个后端之间切换，并实现记忆迁移。
- **集成兼容性优化**：[Issue #2767](https://github.com/nanocoai/nanoclaw/issues/2767) 指出了Telegram适配器Markdown格式的兼容性问题。虽然这是由上游依赖更新引起的，但反映了社区对**渠道集成保持最新和兼容**的需求。这应作为未来维护工作的常规部分。
- **开发体验提升**：[PR #2766](https://github.com/nanocoai/nanoclaw/pull/2766) 和 [PR #2765](https://github.com/nanocoai/nanoclaw/pull/2765) 专注于为渠道和提供商添加 `.format-lint-off` 功能。这虽然是开发工具层面的改进，但表明社区贡献者开始关注**提升代码质量和开发效率**。

### 7. 用户反馈摘要
从今日的Issues和评论中，我们可以提炼出以下几点用户声音：

- **痛点：安全是悬顶之剑**：从 `YLChen-007` 提交的三个报告可以看出，用户（特别是安全意识强的开发者）对Agent的自主操作权限产生严重担忧。他们害怕Agent在不知不觉中泄露文件、执行未授权的操作。
- **痛点：可用性需“有回应”**：`assapin` 报告的预算问题 ( [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) ) 揭示了“智能体”互动的一个基本期望：无论任务成功与否，都必须给出明确反馈。静默失败是用户体验的“灾难”。
- **积极信号：社区参与文档维护**：`glifocat` 和 `Koshkoshinsk` 对文档修复的贡献表明，社区不仅在使用，也在积极维护项目的可访问性。他们希望`CLAUDE.md`这类核心指引文件是准确、可靠的，以便AI助手能据此正确理解项目。

### 8. 待处理积压
以下是长期未响应或需要重要关注的工作项：

- **【高优先级】安全审计加固PR** [PR #2732](https://github.com/nanocoai/nanoclaw/pull/2732)：该PR旨在修复来自健康审计的安全问题，已存在4天且未合并。鉴于今日新发现了3个严重漏洞，维护团队应优先审查并合并此PR，并评估其是否能完全或部分涵盖今日发现的问题。
- **【高优先级】预算错误提示修复PR** [PR #2759](https://github.com/nanocoai/nanoclaw/pull/2759)：该PR直接修复了#2751的严重可用性问题，应尽快合并。
- **【未解决】性能优化** [Issue #2768](https://github.com/nanocoai/nanoclaw/issues/2768)：提示缓存请求虽非关键Bug，但对提升大上下文Agent的性能和成本有直接影响，建议排入下一迭代。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 NullClaw 项目 2026年6月15日数据生成的每日动态报告。

---

# NullClaw 项目动态日报 (2026-06-15)

## 1. 今日速览

项目今日整体活跃度处于 **平静** 状态。过去24小时内，社区未产生任何拉取请求 (PR) 或新版本发布，项目主干的代码集成与发布活动暂停。唯一的动态是社区提交了一条功能增强请求 (Issue #955)，旨在为 Azure OpenAI LLM 提供者增加基于身份的认证支持。这表明尽管核心开发工作放缓，但社区用户仍在提出针对特定云环境部署的安全性与合规性需求，项目的长期发展路线仍受到关注。

## 2. 版本发布

无

## 3. 项目进展

**无**

今日未有任何 PR 被合并或关闭，项目整体功能推进未产生可量化的变化。

## 4. 社区热点

- **[enhancement] Identity based authentication support for Azure OpenAI LLM Provider** ([#955](nullclaw/nullclaw Issue #955))
    - **作者**: kunalk16
    - **状态**: OPEN
    - **热度**: 今日唯一活跃议题。
    - **诉求分析**: 此 Issue 请求为 Azure OpenAI 提供者添加基于身份的认证支持，具体使用 `DefaultTokenCredential` 来利用 Azure CLI 登录后的开发者凭据。此举背后的核心诉求是满足企业级用户在 Azure 订阅中因安全策略而无法使用 API Key 的痛点。用户希望采用更安全的、无密钥的托管身份认证方式，以遵循严格的合规要求并简化本地开发与 CI/CD 流程中的凭证管理。

## 5. Bug 与稳定性

**无**

今日未报告任何新的 Bug、崩溃或回归问题。

## 6. 功能请求与路线图信号

- **新功能请求**: **[#955] Azure OpenAI Identity-based authentication** ([链接](nullclaw/nullclaw Issue #955))
    - **分析**: 此请求与企业级安全合规趋势高度契合。对于依赖 Azure 生态的用户而言，这是关键功能。考虑到 NullClaw 作为 AI 助手平台需支持多种 LLM 提供者，该请求如果被认可，很可能作为“次要增强”被排入下一个版本的开发计划。该功能与现有认证模块的集成度高，且不涉及破坏性变更，实现路径相对清晰。

## 7. 用户反馈摘要

- **用户痛点**: 用户在 Issue #955 的“动机”中明确指出了在 Azure 订阅中因安全策略限制 API Key 使用的痛点。这表明部分企业用户在受管控的云环境中部署 NullClaw 时存在合规障碍。
- **使用场景**: 用户期望能够在已通过 `az login` 认证的开发环境中无缝使用 NullClaw 的 Azure OpenAI 功能，避免硬编码密钥。
- **满意度**: 当前 Issue 暂无评论，无法直接评估用户对现有功能的满意度。但提出新功能请求本身暗示现有认证方式不能满足其特定场景的合规性要求。

## 8. 待处理积压

**无**

今日未发现长期未响应或处于“待处理”状态的关键 Issue 或 PR。Issues #955 为新开议题，尚未得到维护者响应，建议维护者尽快评估其可行性并给予初步反馈，以维持社区参与度。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 | 2026-06-15

---

## 1. 今日速览

过去24小时内，IronClaw 项目保持高度活跃：共产生 **39 条 Issue 更新**（新开/活跃 32 条，关闭 7 条）和 **44 条 PR 更新**（待合并 27 条，已合并/关闭 17 条）。**安全相关议题集中爆发**：多位贡献者报告了 shell 工具的分类绕过与沙箱逃逸漏洞（共6个新 issue），构成当前最大风险；同时，项目团队发起的 **“工程生产力提升”专项**（#4878）拆出了5个子任务，涵盖测试覆盖率、预览部署、自动化代码审查等，显示团队正加速向 AI-native 开发流水线转型。基础设施侧，v2 附件功能前后端已合并入主（#4738），重要 PR 持续落地。整体活跃度评估：**极高**，社区贡献与内部开发双轮驱动。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共有 **17 个 PR 被合并或关闭**，以下为重点推进项：

### 🚀 功能合并
- **[Reborn] 附件上传 Web UX** — PR [#4738](https://github.com/nearai/ironclaw/pull/4738) (ilblackdragon)  
  为 Reborn WebChat v2 SPA 实现了完整的附件上传、暂存、重命名、删除与预览 UI，补齐了 #4644 的前端缺口。后端（注册表、合约、入站上传、MountView 落地）已在前序 #4677 中落地，本次仅剩 SPA 交互。合并后 Reborn 用户可在聊天中直接发送文件。

- **运行上下文通信切片** — PR [#4836](https://github.com/nearai/ironclaw/pull/4836) (henrypark133)  
  实现了 #4828，在每次循环开始向模型暴露：已连接通道、外发投递目标、运行来源（`msg:runtime.*`）。此举显著提升模型对运行环境感知能力，是 Reborn 多通道协同的基础设施改进。

- **审批→认证→最终回复 e2e 测试重建** — PR [#4873](https://github.com/nearai/ironclaw/pull/4873) (henrypark133)  
  将之前因 CI 失败的 Slack 投递 e2e 测试重新安置到正确的位置，关闭 #4847，确保审批与认证流程的回归保护。

### 🛠️ 修复与优化
- **无凭据提前拒绝** — PR [#4840](https://github.com/nearai/ironclaw/pull/4840) (henrypark133)  
  调整认证门序：先检查凭据缺失，再进入审批门，避免用户批准一个注定失败的操作。

- **“始终允许”跨线程持久化** — PR [#4835](https://github.com/nearai/ironclaw/pull/4835) (zetyquickly)  
  修复 #4825：将持久化审批范围从 `(thread_id, …)` 缩减为 `(tenant_id, user_id, agent_id?, project_id?)`，使得同一用户在同一 agent 上的 “始终允许” 设置对所有线程生效。

- **Re-run 被拒绝时的非阻塞提示** — PR [#4838](https://github.com/nearai/ironclaw/pull/4838) (henrypark133)  
  当新消息抵达已被占用的线程时，不再缓存等待，而是直接返回明确的拒绝提示，由用户手动重试，简化并发模型。

此外，**dependabot 提交的 4 个长期依赖更新 PR**（#4002、#4499、#4032、#4498）仍保持开放但持续更新；Release 版本发布 PR（#3708）仍有待合并决策。

---

## 4. 社区热点

### 🔥 安全漏洞集中报告
贡献者 **YLChen-007** 于 6月14日集中提交了 **6 个独立的 shell 工具安全 Issue**，均在今天引起关注：

| Issue | 标题 | 严重程度 |
|-------|------|----------|
| [#4861](https://github.com/nearai/ironclaw/issues/4861) | Newline 链式命令绕过风险分类 | 高危 |
| [#4862](https://github.com/nearai/ironclaw/issues/4862) | GNU sort --compress-program 绕过 | 高危 |
| [#4863](https://github.com/nearai/ironclaw/issues/4863) | env/shell 包装器绕过高风险审批 | 高危 |
| [#4864](https://github.com/nearai/ironclaw/issues/4864) | 包装命令继承先前自动审批 | 高危 |
| [#4865](https://github.com/nearai/ironclaw/issues/4865) | env /bin/sh -c 透明包装绕过 | 高危 |
| [#4797](https://github.com/nearai/ironclaw/issues/4797) | write_file 通过悬空符号链接逃逸 | 高危 |

这些 Issue 的诉求清晰：**IronClaw 的 shell 工具在对命令进行风险分级时，未覆盖包装器、链式、压缩程序等手段，导致原本应要求显式审批的破坏性命令以低风险名义自动执行。** 至今无一对应 fix PR，维护者需紧急评估。

### 💡 工程生产力倡议
**think-in-universe** 发起了 [#4878](https://github.com/nearai/ironclaw/issues/4878) “用 IronClaw 自身提升工程生产力”，并拆出 5 个子任务：
- [#4883](https://github.com/nearai/ironclaw/issues/4883) 测试覆盖率追踪
- [#4882](https://github.com/nearai/ironclaw/issues/4882) 云端编码 agent 工作流
- [#4881](https://github.com/nearai/ironclaw/issues/4881) 预览部署（Vercel 风格）
- [#4880](https://github.com/nearai/ironclaw/issues/4880) 自动化代码审查
- [#4879](https://github.com/nearai/ironclaw/issues/4879) 本地 dogfooding 发现

这些议题标志着 IronClaw 团队开始“吃自己的狗粮”，将 Agent 能力应用到自身开发流程中，可能塑造下一阶段的路线图。

---

## 5. Bug 与稳定性

按严重程度排列（高 → 低）：

| 严重程度 | Issue | 描述 | 状态 |
|----------|-------|------|------|
| 🚨 严重 | [#4865](https://github.com/nearai/ironclaw/issues/4865) 等6个 | shell 安全绕过（详见社区热点） | 无 fix PR |
| ⚠️ 高 | [#4884](https://github.com/nearai/ironclaw/issues/4884) | Google Calendar 扩展请求 OAuth 时，错误地索要 access token 而非引导用户完成 OAuth 流程 | 无 fix |
| ⚠️ 高 | [#4870](https://github.com/nearai/ironclaw/issues/4870) | Reborn WebChat v2 WebSocket 辅助函数使用 token 参数，但 v2 auth 合约拒绝此种认证方式 | 无 fix |
| ⚠️ 高 | [#4874](https://github.com/nearai/ironclaw/issues/4874) | WebChat v2 在非 localhost 纯 HTTP 访问时发消息抛 “Illegal invocation” | 无 fix |
| ⚠️ 高 | [#4852](https://github.com/nearai/ironclaw/issues/4852) | Shell 命令在审批对话框和活动历史中不可见，仅显示 `Capability: builtin.shell` | 无 fix |
| 🟡 中 | [#4751](https://github.com/nearai/ironclaw/issues/4751) | 大响应请求导致 provider tool 参数超过 16384 字节限制（已关闭，但未说明修复） | 已关闭 |
| 🟢 低 | [#4868](https://github.com/nearai/ironclaw/issues/4868) | 移动端设置页推理提供商标题按钮溢出屏幕 | 无 fix |
| 🟢 低 | [#4857](https://github.com/nearai/ironclaw/issues/4857) | 干净状态下 NEAR AI 提供商标记为 ACTIVE | 无 fix |
| 🟢 低 | [#4867](https://github.com/nearai/ironclaw/issues/4867) | GitHub 仓库分析可能绕过 GitHub Extension 回退到 builtin.http | 无 fix |

此外，#4872 (外部 comm 标签渲染为指令文本) 和 #4875 (runtime_context.rs 拆分) 属于设计决策问题，尚未影响稳定版本。

---

## 6. 功能请求与路线图信号

- **Universal Attachments** (#4644) 是近期最受关注的功能请求，今日 #4738 已合并，补全了前端 UX；后续 #4871（图片附件支持视觉模型）已提交 PR 待合并，附件路线正向多模态迈进。
- **运行上下文感知** (#4828) 相关 PR #4836 已合并，模型将获得通道、投递、来源等完整信息，这为动态路由和跨渠道调度奠定基础。
- **可观测性缝** (PR #4588) 提出了 Trajectory Observer 与 LLM provider 注入两个 seam，允许外部宿主（如 bench 工具）驱动和观察 Reborn 运行，是平台化的重要一步。
- **工程生产力自动提升** (#4878系列) 虽非直接面向用户的功能，但若落地将显著改善开发体验与发布质量。其中 #4882（云端 coding agent）和 #4880（自动化审查）可能会催生新的内部工具。
- **Slack 产品适配器扩展** (PR #4778) 正在尝试将 Slack 从硬编码通道转为可插拔扩展，若合入将允许第三方开发自己的通道扩展。

这些信号表明，IronClaw 的下一个版本（预计 0.30.x）将着重于 **多模态附件、平台化扩展、工程自动化**。

---

## 7. 用户反馈摘要

由于评论数普遍较低（多数 Issue 评论数为 0 或 1），真实用户反馈主要来自 **dogfooding 发现**和**安全报告**：

- **Dogfooding 正负面**  
  Issue [#4879](https://github.com/nearai/ironclaw/issues/4879) 记录了本地使用 Reborn 时的摩擦点，包括 WebUI 启动耗时、模型提供商配置路径不直观、首次运行指导缺失。这反映出自托管用户的常见痛点。
  Issue [#4692](https://github.com/nearai/ironclaw/issues/4692)（上一周 dogfooding）积累的问题得到一定程度修复，但仍有残余。

- **安全性担忧**  
  多位贡献者对 shell 工具的分类逻辑表达不信任，指出即使使用看似安全的命令（如 `sort`、`env`），也能构造出破坏性载荷。这暴露了基于前缀的风险分类模型的根本缺陷。用户期望引入更严格的命令分析（如 AST 解析）或沙箱机制。

- **Google Calendar 集成体验**  
  Issue [#4884](https://github.com/nearai/ironclaw/issues/4884) 描述 OAuth 流程被简化为索要 token，用户无法完成授权，导致扩展无法使用。表明第三方凭据管理的边缘处理仍需加强。

- **WebUI 跨网访问**  
  Issue [#4874](https://github.com/nearai/ironclaw/issues/4874) 指出通过网络名称访问时发送消息失败，这限制了企业局域网内的团队协作场景。

---

## 8. 待处理积压

以下为长期开放且值得维护者重点关注的事项：

| 类型 | 编号 | 说明 | 存活时间 |
|------|------|------|----------|
| 🔒 安全 | [#4797](https://github.com/nearai/ironclaw/issues/4797) | write_file 悬空 symlink 逃逸，已上报 3 天，仍无 fix PR | 2026-06-12 |
| 🔒 安全 | [#4861-4865](https://github.com/nearai/ironclaw/issues/4861) | 5 个 shell 工具绕过漏洞，今日新开，等待评估 | 2026-06-14 |
| 🔄 未合并 PR | [#4778](https://github.com/nearai/ironclaw/pull/4778) | Slack 扩展化 PR，已开放 4 天，review 停滞 | 2026-06-11 |
| 📦 版本发布 | [#3708](https://github.com/nearai/ironclaw/pull/3708) | Release PR 已开放 30 天，包含 API 破坏性变更，需决策是否合并 | 2026-05-16 |
| 🔄 长期 Dependabot | [#4002](https://github.com/nearai/ironclaw/pull/4002) | actions 组依赖更新（共 16 个包），持续积压 22 天 | 2026-05-24 |
| 🔄 长期 Dependabot | [#4499](https://github.com/nearai/ironclaw/pull/4499) | tokio 生态依赖更新，积

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我将根据您提供的LobsterAI数据，为您生成一份客观、严谨、数据驱动的2026年6月15日项目动态日报。

---

### LobsterAI 项目动态日报

**日期**: 2026年6月15日
**分析师**: AI 智能体与个人 AI 助手开源项目分析师

#### 1. 今日速览

本日项目整体活跃度较低，属于**低活跃/维护模式**。过去24小时内无新版本发布，Issues方面仅有2条长期未更新的“stale”条目，无任何新问题或讨论产生。Pull Requests（PR）侧是今日主要进展来源，虽然大部分为待合并状态，但成功合并了一个重要的Bug修复PR（#1465）。这表明项目团队当前的工作重点在于清理和合并历史遗留的PR，而非响应新的社区反馈或推出新功能。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日项目核心进展是 **1个重要Bug修复PR被合并**，解决了定时任务功能中的一个数据一致性问题。

-   **已合并PR**:
    -   **#1465** [已关闭] **修复(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现**。此PR解决了用户删除定时任务后，任务记录消失，但重启应用后又以“幽灵会话”形式重新出现的顽固Bug。根本原因是删除流程未清理本地SQLite数据库中由该任务创建的关联会话记录。此合并修复了后端数据一致性问题，提升了定时任务功能的稳定性。
        -   链接: netease-youdao/LobsterAI PR #1465

-   **待合并PR (功能增强)**:
    -   **#1429**: 为Cowork会话视图添加了会话内消息搜索功能，并支持`mark.js`实时高亮和快捷键操作。
    -   **#1430**: 在Cowork会话运行期间，利用Electron API自动阻止系统休眠，防止长时间任务因系统挂起而中断。
    -   **#1431**: 在`StreamingActivityBar`上添加了实时的会话运行计时器，提升用户对耗时任务的进度感知。

这些待合并的PR全部聚焦于**Cowork功能模块的体验增强**，包括搜索、防休眠和计时器。它们一旦完成合并，将显著提升“AI代理”协作场景下的用户体验和稳定性。项目正在向更专业、更稳定的“代理”工作流方向迈进。

#### 4. 社区热点

今日无新产生的高热度讨论。社区互动主要集中在几个旧Issue上，但未形成新的对话。考虑到当前项目活跃度较低，社区情绪表现为**沉默的接受**（即没有新报怨或少有表扬）。

-   **值得关注的Issue**:
    -   **#1434** 和 **#1435** 在近一个多月内有人（可能是代码维护者）标记为 `stale`，但并未进一步解决或关闭。这反映出社区反馈已进入审核队列，但尚未被优先处理。
        -   链接: #1434, #1435

#### 5. Bug 与稳定性

今日确认了一个较重要的Bug被修复，同时有两个已知的UI Bug处于待处理状态。

| 严重程度 | Bug描述 | 状态 | 详细说明 |
| :--- | :--- | :--- | :--- |
| **高** | 已删除的定时任务重启后幽灵复活 | **已修复** | 此Bug影响数据一致性，复现率高，体验极差。已被PR #1465修复并合并。 |
| **中** | UI国际化缺失 | **待解决** | Issue #1434指出，当语言设置为中文时，“我的代理”技能页面的搜索无数据提示和按钮仍为英文，影响非英语用户的体验。 |
| **中** | UI溢出 | **待解决** | Issue #1435指出，新建自定义Agent时，名称过长会超出弹框边界，影响界面美观和信息展示。 |
> **说明**: 以上两个UI Issue均为社区用户`xuzx-code`报告，距今已有73天未更新，可能陷入低优先级处理的困境。

#### 6. 功能请求与路线图信号

今日无新的功能请求。但待合并的PR是重要的路线图信号，为我们揭示了项目的下一步发展方向：

-   **核心场景**: "Cowork（协同工作/代理执行）"被视为未来版本的重心。三个待合并PR均围绕此场景展开。
-   **未来可能纳入的功能**:
    -   **高级会话管理 (已提PR #1429)**: 针对长会话或复杂任务，提供会话内搜索是用户刚需要求，可能在下一版本（如v1.x.x）中发布。
    -   **系统级稳定性 (已提PR #1430)**: 防止系统休眠是一个明确的“稳定性”需求，对于成为可靠的“代理”至关重要，优先级较高。
    -   **执行可视化 (已提PR #1431)**: 实时计时器是提升用户体验、增加透明度的标准做法，预计也会很快合并。

这些功能如果成功合并，将标志着 **LobsterAI 从一个对话工具向一个可靠的、可监控的自主代理执行平台迈出了关键一步。**

#### 7. 用户反馈摘要

从现有数据（多为历史数据）中，我们可以提炼出真实的用户痛点：

-   **痛点1：国际化不彻底**。Issue #1434 的作者在设置中文界面的情况下，看到了英文提示，这是对本地化期待的一种直接不满。用户期望产品在语言切换后，所有界面元素（包括反馈提示、UI按钮）都**无缝切换**。
-   **痛点2：数据残留带来坏体验**。Issue #1359（被PR #1465修复）的用户，在删除定时任务后却遭遇“幽灵任务”复活，是一种典型的“操作未实际生效”的糟糕感受，会**严重打击用户对产品数据管理能力的信任**。
-   **痛点3：执行过程缺乏控制和感知**。三个待合并的PR（搜索、防休眠、计时器）所对应的需求，反映出用户在执行长时间任务时，**对会话内信息检索、任务是否会意外中断、以及任务的持续时间高度不安**。用户希望获得更多的掌控权和反馈。

#### 8. 待处理积压

以下为长期未得到响应或解决的重要Issue和PR，需要项目维护者重点关注，以避免社区反馈积压和贡献者热情消退。

-   **积压的Bug (UI/UX)**:
    -   **#1434**: [Open] 中文环境下的英文提示问题 (已标记stale超70天)
    -   **#1435**: [Open] Agent名称过长溢出问题 (已标记stale超70天)

-   **积压的功能PR (功能增强)**:
    -   **#1429**: [Open] Cowork会话内消息搜索 (已标记stale超70天)
    -   **#1430**: [Open] 运行期间防止系统休眠 (已标记stale超70天)
    -   **#1431**: [Open] 会话运行计时器 (已标记stale超70天)
    > **潜在风险**: 这3个待合并PR若迟迟无法合并，不仅无法为项目带来实际价值，更可能挫伤外部贡献者的积极性。建议项目维护者在下一个发布周期前优先处理这批高质量PR。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-06-15

---

## 1. 今日速览

- 项目在过去24小时内整体活跃度偏低，仅新增一条 Issue（#1123），无新PR或版本发布。
- 该 Issue 为功能增强请求，提议引入纯 Rust 实现的 turbovec 作为内存后端，以优化极端场景下的压缩效率。
- 未出现新 Bug、崩溃或回归报告，项目当前稳定性未见异常，但社区讨论热情有待提升。
- 长期来看，Moltis 近期进入功能规划与基础设施探索阶段，社区贡献者更倾向于提出前瞻性技术方案而非紧急修复。

---

## 2. 版本发布

**无** – 过去24小时内未发布任何新版本。

---

## 3. 项目进展

- **无合并/关闭的 PR**：今日无 PR 更新，项目主线未合并新代码。整体开发节奏放缓，可能处于内部重构或技术选型阶段。

---

## 4. 社区热点

**唯一活跃 Issue：**  
- [#1123 [Feature]: Add pure-Rust turbovec as an alternative memory backend for extreme edge compression](https://github.com/moltis-org/moltis/issues/1123)  
  作者：`joeblew999` | 评论：0 | 👍：0  
  **摘要**：请求集成纯 Rust 实现的 [`turbovec`](https://crates.io/crates/turbovec)（一种针对边缘设备优化的内存压缩方案），作为现有内存后端的备选，以在资源极度受限的环境下实现更高压缩比和数据吞吐量。

**分析**：  
- 该 Issue 目前无评论、无 👍，尚未引起广泛讨论，但其指向的技术方向值得关注。turbovec 作为新兴的 Rust 原生向量压缩库，若被采纳，可显著提升 Moltis 在 IoT、嵌入式等低资源场景下的竞争力。
- 作者已在问题中附上预检查清单，说明其对项目贡献流程熟悉，且可能已有初步实现思路。建议维护团队及时评估技术可行性，避免该需求长期积压。

---

## 5. Bug 与稳定性

**无** – 今日未报告任何 Bug、崩溃或回归问题。项目在稳定性层面表现良好，未发现需要紧急修复的缺陷。

---

## 6. 功能请求与路线图信号

**唯一请求**：
- **turbovec 后端**（#1123）—— 该请求可视为路线图上的一个潜在方向，尤其适合与 Moltis 现有的内存管理架构相结合。若实现，将直接拓展项目的应用边界至“极端边缘”场景。  
  由于目前无关联 PR 或维护者回应，暂无法判断是否会被纳入下个版本。建议社区成员在 Issue 下补充性能对比数据或原型测试结果，推动评估。

**信号**：  
- 当前无任何 PR 暗示下一版本的明确目标。维护者可能需要从该 Issue 出发，启动一次关于内存后端插件化设计的讨论。

---

## 7. 用户反馈摘要

- 由于仅有一条 Issue 且无评论，当日无直接用户反馈。但从 Issue 内容可推断用户场景：  
  - **痛点**：现有内存后端在极端边缘设备（如低功耗 MCU、有限 RAM 环境）上压缩效率或性能不足。  
  - **期望**：引入纯 Rust 实现的后端，减少对 C/C++ 绑定的依赖，同时提升压缩比和速度。  
  - **未满足点**：当前 Issue 无人回复，用户可能等待维护者表态。

---

## 8. 待处理积压

**长期未响应的 Issue/PR 提醒**（基于项目历史状态推测，需维护者自查）：  
- 今日数据未体现长期积压，但建议维护者关注 #1123 的后续动态，避免像部分历史 Issue 一样被长时间忽略。  
- 此外，可检查是否存在超过30天未获得回应的 [其他开放 Issue](https://github.com/moltis-org/moltis/issues?q=is%3Aissue+is%3Aopen+sort%3Acreated-asc)，必要时进行标注或关闭。

---

**项目健康度评估**：⭐⭐☆☆☆（低活跃度）  
当前项目处于技术酝酿期，无代码变更但有一条带有前瞻性的功能请求。社区需更多维护者参与讨论以保持发展动力。建议在下一个版本计划中明确回应 #1123，避免创新提议被埋没。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 (2026-06-15)

---

## 1. 今日速览

过去24小时内，项目保持了较高的社区活跃度：共处理17条Issue（新开/活跃16条，关闭1条），新增12条Pull Request（全部待合并），无新版本发布。Bug报告数量增长明显，涵盖了桌面端启动性能、长对话无响应、特定模型提供者显示异常等影响核心体验的问题；同时社区贡献者积极提交了多项功能改进与本地化翻译PR，包括Windows桌面GUI自动化、PRD管理工具、越南语界面等。整体项目处于“高输入、待消化”状态，维护团队需重点关注回归问题和关键Bug的修复进度。

---

## 3. 项目进展

今日无任何PR被合并或关闭，12条PR均处于开放待审查状态。但其中多项PR预示了重要的功能推进：

- **Windows桌面GUI自动化**：[#5187](https://github.com/agentscope-ai/QwenPaw/pull/5187) 新增 `computer_use` 内置工具，使用UIA + Tauri控制模式，允许Agent驱动Windows桌面（截图、描述、点击/输入/滚动等），并附带控制模式界面供用户观察Agent操作。这是桌面端Agent能力的一大跃升。
- **请求负载转换**：[#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188) 引入了请求负载转换注册表，允许插件通过SDK在请求发送前修改负载，增强扩展性。
- **插件命令建议**：[#5189](https://github.com/agentscope-ai/QwenPaw/pull/5189) 在控制台支持插件命令建议及跨标签语言同步。
- **内置PRD管理工具**：[#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902) 替换插件实现，提供CRUD操作及前端交互组件，方便管理产品需求文档。
- **定时/心跳机制修复**：[#5180](https://github.com/agentscope-ai/QwenPaw/pull/5180) 增加超时时间并添加自主上下文提示，直接回应社区反馈的定时任务不执行问题。
- **多Agent协作技能触发词扩展**：[#5179](https://github.com/agentscope-ai/QwenPaw/pull/5179) 修复“团队协作”模式有时被忽略的问题。

这些PR展现了社区贡献者持续推动项目在桌面自动化、插件体系、协作能力等方面的拓展，但均需等待核心团队审阅合并。

---

## 4. 社区热点

今日讨论最集中的两个议题：

### [#5047 [已关闭] Windows Tauri桌面端启动特别慢](https://github.com/agentscope-ai/QwenPaw/issues/5047)
5条评论，用户强烈反馈从Python迁移到Tauri后启动时间从1-2分钟骤增至十几分钟，且经常无响应。该Issue已于今日关闭，但未说明具体解决方案，可能已在后续版本中修复或标记为已知问题。此议题反映了核心用户对桌面端性能的高度敏感。

### [#5156 建议支持kimi-for-coding / 加入uv白名单](https://github.com/agentscope-ai/QwenPaw/issues/5156)
5条评论，用户提出将kimi-for-coding纳入uv白名单，以便已订阅Kimi coding套餐的用户能在QwenPaw中使用。背后诉求是**付费API套餐的兼容性问题**，用户已在其他平台付费，不希望重复开支。虽未被官方回应，但体现出用户对模型供应商生态整合的期望。

此外，[#5161 (长对话无响应)](https://github.com/agentscope-ai/QwenPaw/issues/5161) 和 [#5162 (思考死循环)](https://github.com/agentscope-ai/QwenPaw/issues/5162) 也收到2条评论，但关注度稍低。

---

## 5. Bug 与稳定性

按严重程度排列今日报告的Bug（已有关联Fix PR的标注）：

| 严重等级 | Issue | 描述 | 关联PR |
|----------|-------|------|--------|
| **P0 - 核心功能回归** | [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) | v1.1.11.post2 与 v1.1.10 之间Gemini工具调用回归，模型无法正常使用内置工具 | 无 |
| **P0 - 功能完全不可用** | [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | 长对话后QwenPaw完全无响应，停止回复 | 无 |
| **P0 - 逻辑死循环** | [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | 对话思考逻辑进入死循环 | 无 |
| **P1 - 功能异常** | [#5184](https://github.com/agentscope-ai/QwenPaw/issues/5184) | v1.1.11.post2中本地模型提供者创建后不显示 | 无 |
| **P1 - 数据丢失** | [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | 上下文压缩导致信息完全丢失（当人设文件token超过阈值时） | 无 |
| **P2 - 平台兼容** | [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) | Python 3.13安装TeamChat插件失败，依赖imghdr模块缺失 | 无 |
| **P2 - 平台兼容** | [#5183](https://github.com/agentscope-ai/QwenPaw/issues/5183) | 宠物功能在Wayland (Niri WM)下无法使用 | 无 |
| **P2 - 体验问题** | [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181) | 插件依赖安装导致cmd窗口持续弹窗，死循环重试 | 无 |
| **P2 - 功能缺失** | [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177) | 钉钉Channel消息未注册到chats.json，前端会话不可见 | 无 |
| **P2 - 功能缺陷** | [#5174](https://github.com/agentscope-ai/QwenPaw/issues/5174) | Cron/心跳机制不执行知识提取等重任务，被描述为“should-do”清单 | [#5180](https://github.com/agentscope-ai/QwenPaw/pull/5180) 已提交修复 |
| **P3 - 打包问题** | [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165) | 使用build_win_pyinstaller.ps1打包后白屏，spec引用了不存在的模块 | 无 |

**关键发现**：v1.1.11.post2 存在多个回归和严重Bug，尤其Gemini工具调用回归（#5163）和长对话无响应（#5161）直接影响核心功能，建议尽快发布补丁版本。

---

## 6. 功能请求与路线图信号

当前社区提出的新功能需求中，部分已有对应PR或明确讨论方向：

| 功能请求 | Issue | 对应PR/状态 |
|----------|-------|-------------|
| **kimi-for-coding / uv白名单** | [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) | 无PR，高票需求，需评估API兼容性 |
| **飞书CardKit流式优化（长回复刷新慢）** | [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167) | 无PR，但用户给出了详细优化建议 |
| **官方Zalo Bot Channel** | [#5168](https://github.com/agentscope-ai/QwenPaw/issues/5168) | 无PR，越南社区强烈需求，可能与本地化翻译PR（#5186）形成联动 |
| **统一模型配置（支持多种类型）** | [#5182](https://github.com/agentscope-ai/QwenPaw/issues/5182) | 无PR，属于架构级别改进 |
| **实时时间戳注入** | [#5185](https://github.com/agentscope-ai/QwenPaw/issues/5185) | 无PR，简单但实用的增强 |
| **请求负载转换插件接口** | – | [#5188](https://github.com/agentscope-ai/QwenPaw/pull/5188) |
| **插件命令建议** | – | [#5189](https://github.com/agentscope-ai/QwenPaw/pull/5189) |
| **PRD管理内置工具** | – | [#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902) |
| **越南语界面** | [#5169](https://github.com/agentscope-ai/QwenPaw/issues/5169) | [#5175](https://github.com/agentscope-ai/QwenPaw/pull/5175)、[#5186](https://github.com/agentscope-ai/QwenPaw/pull/5186) |
| **会话过滤（按标题）** | [#4999](https://github.com/agentscope-ai/QwenPaw/issues/4999) | [#5178](https://github.com/agentscope-ai/QwenPaw/pull/5178) |
| **批准命令文本自动换行** | [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) | [#5176](https://github.com/agentscope-ai/QwenPaw/pull/5176) |

**路线图信号**: 越南语支持和Windows桌面自动化是两个最突出的社区贡献方向，预计会随下一版本合并。而kimi-for-coding和Zalo Bot则代表了新的模型/渠道集成需求，可能成为后续版本的重点。

---

## 7. 用户反馈摘要

从Issue评论中提炼真实用户声音：

- **性能之痛**：“自从桌面端从Python打包换为Tauri以后，启动速度严重变慢，从原本的一两分钟变成了十几分钟，而且启动时经常进入无响应状态。” —— [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047)
- **付费兼容性诉求**：“已经付费订阅了Kimi的coding套餐，但没法直接接入到QwenPaw里使用，感觉比较难受。” —— [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156)
- **体验下降**：“长回复场景下刷新较慢，体感上已经影响可用性……甚至会比‘非流式+分段更新’还慢。” —— [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167)
- **数据丢失恐慌**：“压缩会出现将上下文完全压缩保留为0的情况，模型无法继续任务，因为上下文已经完全丢失。” —— [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171)
- **桌面干扰**：“当网络环境无法正常连接PyPI时，pip安装失败导致死循环重试，每次重试都弹出一个可见的cmd窗口，桌面频繁闪现。” —— [#5181](https://github.com/agentscope-ai/QwenPaw/issues/5181)
- **渠道集成短板**：“通过钉钉channel发送消息后，agent正常回复，但chats.json中没有对应记录……前端console的会话列表中看不到该对话。” —— [#5177](https://github.com/agentscope-ai/QwenPaw/issues/5177)

这些反馈共同指向**性能优化、付费模型兼容、数据完整性、渠道稳定性**四个核心痛点。

---

## 8. 待处理积压

以下Issue和PR长期存在但至今未获得明确答复或合并，建议维护团队优先关注：

| 类型 | 编号 | 标题 | 创建日期 | 状态 |
|------|------|------|----------|------|
| PR | [#4902](https://github.com/agentscope-ai/QwenPaw/pull/4902) | feat(manage_prd): add built-in PRD CRUD tool with frontend renderer | 2026-06-02 | 待合并，已13天 |
| PR | [#5051](https://github.com/agentscope-ai/QwenPaw/pull/5051) | fix(desktop): persist backend port across restarts to preserve localStorage | 2026-06-09 | 待合并，已6天 |
| Issue | [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) | [CLOSED] Windows Tauri桌面端启动特别慢 | 2026-06-09 | 已关闭但未公开修复方案，引发用户困惑 |
| Issue | [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) | Gemini

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，各位关注 ZeroClaw 项目的朋友，大家好。我是你们的老朋友，AI 智能体与个人助手开源项目分析师。今天，我将基于 2026 年 6 月 15 日的 GitHub 数据，为大家带来 ZeroClaw 项目的每日动态报告。

---

# ZeroClaw 项目动态日报 | 2026-06-15

## 1. 今日速览

ZeroClaw 项目今日继续保持超高活跃度，社区贡献者和维护团队正以极高的效率推进项目迭代。过去 24 小时内，Issue 关闭率达到 67%（42条中关闭28条），显示出项目团队在处理用户反馈和 Bug 修复方面响应迅速。PR 待合并积压量较大（47条），但也不乏高质量的合并，尤其在 Config 重构、Cron 任务管理、以及大量新型集成工具方面取得了实质性进展。整体来看，项目处于功能快速扩展和稳定性持续加固的健康周期。

## 2. 版本发布

无。

## 3. 项目进展

今日项目在多个关键领域取得了显著进展，以下为本日所合并/关闭的重要Pull Request：

- **[Config 系统深度重构 (#7594) - CLOSED]**: 由维护者 `singlerider` 提交的 PR **#7594** 成功合并。该 PR 实现了类型驱动的别名引用选择器和自声明配置枚举，消除了原有的硬编码特殊路径处理。**这意味着未来新增任何配置字段，其UI交互行为将自动从其Rust类型派生，显著降低了配置系统的维护成本，并提升了健壮性。**
- **[Cron 任务暂停/恢复功能 (#7384) - CLOSED]**: 由贡献者 `Nillth` 提交的 PR **#7384** 成功合并。此 PR 为 UI 仪表盘上的定时任务增加了“暂停/恢复”开关，用户现在无需删除任务即可灵活控制其执行，提升了任务管理的人机交互体验。
- **[One-Click 插件路径修复 (#7549) - OPEN]**: 贡献者 `alanpjohn` 提交了 PR **#7549**，修复了 CLI 安装插件路径与运行时扫描路径不匹配的 Bug。此前，通过 `zeroclaw plugin install` 安装的 WASM 插件对系统不可见，该修复对插件生态的完善至关重要。

同时，大量由社区开发者 `theonlyhennygod` 提交的关于 SMS 渠道集成（Vonage、Sinch、Plivo、Telnyx）和工具集成（Sonos、Shazam、Spotify、8Sleep、Philips Hue）的 Issue 均在今日被关闭，标志着这些功能已正式落地，极大地丰富了 ZeroClaw 的生态连接能力。

## 4. 社区热点

今日社区讨论主要聚焦于基础设施优化和遗留技术债务处理：

- **【🔥 最热议题】工作流管理与标签清理 RFC (#6808)**: Issue **#6808** 获得了今日最高的 11 条评论，且仍处于开放状态。该 RFC 提议引入“工作泳道”（Work Lanes）和看板自动化，旨在解决日益复杂的 Issue 和 PR 路由问题，减轻维护者负担。社区对此反响热烈，讨论集中在如何在不增加手动维护量的前提下实现自动化路由。**这反映了项目规模增长后，对规范化开发流程的迫切需求。**
- **【🔥 高风险 Bug】委托代理模式权限拒绝 (#7470)**: Issue **#7470** 被标记为高风险（S1 - 工作流被阻塞），收获了7条评论。该 Bug 描述了委托（delegate）模式下，当目标 agent 的 `allowed_tools` 配置为空或与当前 agent 一致时，会出现权限错误，导致多 agent 协作场景（如代码审查、异步研究）无法正常工作。**该问题触及 ZeroClaw 最核心的 agent 协作架构，社区高度关注其修复进展。**
- **【🚀 前瞻性架构】气隙执行模式 RFC (#6293)**: Issue **#6293** 在今日获得更新，也收获了 5 条评论。该 RFC 提出将 ZeroClaw 拆分为离线 agent 容器与在线代理守护进程，通过 Unix Socket 连接，以实现高安全要求的离线/气隙环境部署。**这显示了项目在向企业级安全合规场景迈进的重要探索。**

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在安全和核心工作流层面，均已被标记并有一系列修复 PR 正在跟进。

| 严重程度 | Issue / PR | 描述 | 当前状态 |
| :--- | :--- | :--- | :--- |
| **S0 - 数据泄露/安全风险** | **#5528 (Closed)** | **Email 频道配置逻辑缺陷**，不正确的示例配置可能导致配置错误。 | 已关闭，确认为文档/配置问题。 |
| **S1 - 工作流被阻塞** | **#7470 (Open)** | **委托代理模式权限拒绝**，当 `allowed_tools` 为空或冲突时，多 agent 协作流程被完全阻塞。 | **关键高危**，正在加速修复中，关注相关 PR **#7592**。 |
| 中等 | **#6856 (Open)** | **[channel] 配置项缺失**: `show_tool_calls` 在 schema v3 中无法使用，导致工具调用细节不在频道响应中展示。 | 状态为 in-progress，已有直接关联的修复方案。 |
| 中等 | **#5662 (Open)** | **QQ 频道语音消息重复处理**，单条语音消息被处理 20+ 次，导致 `brain.db` 中出现大量重复条目。 | 状态为 in-progress，需要关注该项目承诺的上游依赖修复。 |

## 6. 功能请求与路线图信号

今日的社区功能请求呈现出两个清晰的方向：

1.  **生态扩张（已落地）**：大量关于集成新型 SMS 提供商、智能家居设备和流媒体服务的请求（如 #6449, #6450, #6475, #6477）今日均已完成，这反映了社区希望 ZeroClaw 成为 **“万物互联”的中枢**。这类特性很可能已纳入下一版本。
2.  **架构演进（未来预期）**：**零信任/气隙部署**（#6293）、**工作流自动化**（#6808）和**全功能 Docker 镜像**（#3642, 已关闭但未发布）等 RFC 表明，社区期望 ZeroClaw 能适应更安全、更复杂的企业级部署场景。这些很可能成为 0.80 或后续版本的核心方向。

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中，我们听到了社区真实的声音：

- **降低入门门槛**：社区成员 `@LaurensBosscher` 在 #3642 中提出，功能默认禁用虽然降低了内存占用，但给新用户和非技术用户设置了“过高门槛”。这表明社区的共识是：**提供功能性更全面的开箱即用体验比极端优化内存更重要**。
- **配置 & 文档配合问题**：多个 Bug 报告（如 #5528, #6856）显示，用户经常因为配置示例不完整、文档与实际行为不符而感到困惑。社区在 #6760 的讨论中主动提供了完整的 Docker Compose 示例，体现了极强的社区自助互助精神。
- **硬件与架构适配**：来自 `@dwc1997` 的多项修复 PR (#7614, #7617) 专注于解决 musl libc 等特定环境下的安装和配置问题，说明用户群体广泛，且对跨平台兼容性有非常高的要求。

## 8. 待处理积压

以下列举几项长期未响应或进展缓慢，但具有重要影响的项目，提请维护者关注：

- **【严重】审计跟踪：153 个提交因批量回滚丢失 (#6074)**: 自 2026-04-24 提出以来，该 Issue 仅收到2条评论。**涉及 153 个已合并功能的永久丢失，是项目历史中的重大事故**，需要制定详细的仲裁与恢复计划。
- **【RFC】气隙执行模式 (#6293)**: 自 2026-05-03 提出，目前状态为 `status:blocked` 且 `needs-maintainer-review`，等待维护者给出方向性反馈。
- **【长期积压 PR】 “梦境模式”（记忆整合）(#6693)**: 由 `@JordanTheJet` 提交的用于周期性内存整合的 XL 尺寸 PR，已开放超过一个月仍为 `needs-author-action` 状态，急需贡献者回应维护者的审查意见，避免被标记为 stale。

---

以上就是今日的 ZeroClaw 项目日报。项目在稳定中高速发展，社区自我治理的能力和贡献者的专业度令人印象深刻。我们明天再见。


</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*