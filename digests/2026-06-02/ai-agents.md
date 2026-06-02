# OpenClaw 生态日报 2026-06-02

> Issues: 463 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-02 02:52 UTC

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

# OpenClaw 项目动态日报 — 2026-06-02

## 1. 今日速览
过去 24 小时项目保持高活跃度：共处理 **463 条 Issue**（新开/活跃 298，关闭 165），**500 条 PR**（待合并 396，已合并/关闭 104），发布 **2 个 Beta 版本**。核心主线围绕 Codex 运行时稳定性（中断恢复、OAuth 刷新、turn‑completion 超时）、多渠道消息去重（Telegram、QQBot、Feishu）以及会话存储迁移（SQLite seam）。社区讨论焦点集中在 Codex / OpenAI 模型兼容性、Token 用量膨胀及本地模型支持需求。长期待处理的 Multi‑Agent 协作 RFC（#35203）和多项 P1/P2 级 Bug 仍未闭合，维护者需优先介入。

---

## 2. 版本发布
### v2026.6.1‑beta.1 / v2026.6.1‑beta.2
- **主要改进**：
  - Agent 及 CLI 运行时：中断工具调用、过期会话绑定、压缩交接、媒体重试等场景恢复更干净（#88129、#88136 等）。
  - 多渠道投递：Telegram、WhatsApp、iMessage、Slack 的投递稳定性增强。
- **破坏性变更**：无明确标记，但建议升级前检查自定义插件或 OAuth 配置文件，特别是使用 `openai-codex/` 配置路径的用户（参见 #84038）。
- **迁移注意事项**：`doctor --fix` 曾将 `openai-codex/` 配置错误迁移为 `openai/`，需确认该修复已包含在本次 Beta 中。

---

## 3. 项目进展
今日合并/关闭的 PR 与 Issue 推进了以下关键修复：

| 领域 | PR/Issue | 进展 |
|------|----------|------|
| 内存 | [#77894](https://github.com/openclaw/openclaw/pull/77894)（已合并） | 修复 `readPhaseSignalStore` 非 ENOENT 错误导致梦境相位信号丢失的问题 |
| 会话锁 | [#57019](https://github.com/openclaw/openclaw/issues/57019)（已关闭） | 修复 session 写锁异步释放时误删新获得锁的竞态条件 |
| OAuth / Codex | [#86820](https://github.com/openclaw/openclaw/issues/86820)（已关闭） | 修复 Codex OAuth 压缩时回退直接 API 且缺少密钥的问题 |
| QQBot | [#87177](https://github.com/openclaw/openclaw/issues/87177)（已关闭） | 解决心跳消息泄漏、插件副作用等导致的重复消息 |
| 模型路由 | [#88102](https://github.com/openclaw/openclaw/issues/88102)（已关闭） | 修复 `openai/gpt-5.5` + Codex 运行时路线在 2026.5.27 被拒绝的问题 |

项目整体向前迈进了 **约 100 项修复/改进**（基于已关闭 Issue 与 PR 数量），且 CLI 文档、Telegram 进度条、Discord 斜杠命令等新功能仍在持续审查中。

---

## 4. 社区热点
过去 24 小时最受关注的话题（按评论 & 表态排序）：

1. **[#80380](https://github.com/openclaw/openclaw/issues/80380) — 升级到 Gemini 3.1 Flash‑Lite GA**  
   评论 14，👍 4。用户要求从预览版切换到正式版，Google 已宣布预览版弃用，社区呼声较高。

2. **[#88838](https://github.com/openclaw/openclaw/issues/88838) — 会话存储迁移到 SQLite**  
   评论 12，👍 1。维护者提出的分支抽象计划，涉及大规模代码变更，社区关注迁移风险和回归。

3. **[#84038](https://github.com/openclaw/openclaw/issues/84038) — `doctor --fix` 破坏 OAuth 配置**  
   评论 12，👍 3。用户报告该命令将 `openai-codex/` 错误迁移为 `openai/`，导致 3‑4x Token 膨胀，已关闭但有「linked‑pr‑open」标签，暗示修复 PR 仍在开放中。

4. **[#86820](https://github.com/openclaw/openclaw/issues/86820) — Codex OAuth 压缩失败**  
   评论 12，👍 6。用户强烈反馈缺少 `OPENAI_API_KEY` 导致会话压缩完全不可用，已关闭。

5. **[#86519](https://github.com/openclaw/openclaw/issues/86519) — Telegram 消息重复**  
   评论 9，👍 1。从 5.20 版本开始出现，升级后仍未彻底修复，用户表示 2‑10 倍重复。

**分析**：社区对 Codex 相关回归（配置迁移、OAuth、模型路由）呼声最高，其次是多渠道可靠性（Telegram 重复、Feishu 沉默）。Gemini 版本升级需求代表对低成本高性能模型的支持诉求。

---

## 5. Bug 与稳定性
按严重程度排列（P1 为最严重）：

| 严重程度 | Issue | 描述 | Fix PR |
|----------|-------|------|--------|
| P1 | [#88312](https://github.com/openclaw/openclaw/issues/88312) | Codex turn‑completion stall 回归（#84076 修复后重现） | 尚无 |
| P1 | [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex Telegram 超时，turn/completed 无法送达 | 尚无 |
| P1 | [#88102](https://github.com/openclaw/openclaw/issues/88102)（已关闭） | `openai/gpt-5.5` + Codex 被拒绝 | 已关闭，但 workaround 有副作用 |
| P1 | [#86519](https://github.com/openclaw/openclaw/issues/86519) | Telegram 消息重复 | 更新 2026.5.22 部分缓解，仍有残余 |
| P1 | [#88369](https://github.com/openclaw/openclaw/issues/88369) | 专用 cron agent 仍自冲突，`EmbeddedAttemptSessionTakeoverError` | 尚无 |
| P1 | [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败卡住数小时 | 尚无 |
| P2 | [#88039](https://github.com/openclaw/openclaw/issues/88039) | Session 选定模型被错误纳入 fallback 列表 | 尚无 |
| P2 | [#87938](https://github.com/openclaw/openclaw/issues/87938) | Feishu DM 重启后会话重复键 | 尚无 |
| P2 | [#85888](https://github.com/openclaw/openclaw/issues/85888) | Cron 在 MiniMax 凌晨超载时失败，手动触发成功 | 已有 linked PR 开放 |
| P2 | [#87641](https://github.com/openclaw/openclaw/issues/87641)（已关闭） | `opencode-go/kimi-k2.6` 多轮任务 400 错误 | 已关闭但标签异常 |

**新增重要 Bug**：  
- [#89139](https://github.com/openclaw/openclaw/issues/89139) WebChat 每个消息新建 agent run，破坏 prompt 缓存，命中率从 93% 跌至 29%（P2）。  
- [#88592](https://github.com/openclaw/openclaw/issues/88592) Control UI Workboard 卡片设置不保存、拖拽无效。

---

## 6. 功能请求与路线图信号

| 功能请求 | 热度 | 分析 |
|----------|------|------|
| [#78308](https://github.com/openclaw/openclaw/issues/78308) MCP 工具链审批通道 | 评论 11，👍 1 | 已有 channel‑mediated 审批框架，扩展至 MCP 是自然演进，可能纳入 2026.6.x |
| [#89265](https://github.com/openclaw/openclaw/issues/89265) 更多本地 Provider | 评论 4，👍 1 | 用户呼吁地方模型成为一等公民，与当前低成本趋势吻合，尚未有 PR |
| [#79077](https://github.com/openclaw/openclaw/issues/79077) Telegram Guest Bot / Bot‑to‑Bot 支持 | 评论 7，👍 7 | 对需要多机器人协作的场景关键，至今只有讨论无 PR |
| [#35203](https://github.com/openclaw/openclaw/issues/35203) 多 Agent 协作增强 | 评论 8（长期） | 3月提出的 RFC，包含能力画像、共享黑板、分层记忆、Token 治理，路线图信号强但优先级可能后移 |
| [#79458](https://github.com/openclaw/openclaw/issues/79458) 斜杠命令国际化 | 评论 5，👍 1 | 需要 i18n 基础设施支持，若有社区贡献可能快速纳入 |

**信号**：本地模型（#89265）和 Telegram 新特性（#79077）获得社区较高青睐，维护者或考虑在下一 mid‑cycle 版本中优先推动。

---

## 7. 用户反馈摘要
从 Issue 评论提炼的真实痛点与使用场景：

- **Telegram 消息重复**（#86519）：用户表示“从 5.20 升级后出现，每次回复都是 2‑10 倍相同文字”，严重影响体验，降级后正常。
- **Codex 配置迁移破坏**（#84038）：用户强调 `doctor --fix` 是“静默迁移”导致无意间使用高 Token 路由，产生额外费用。
- **Feishu 会话丢失**（#77666、#87938）：群聊消息收到但无回复，DM 正常，用户怀疑是 session 维护函数遗漏。
- **QQBot 重复消息**（#87177）：心跳泄漏、插件副作用导致同一消息多次回调。
- **WebChat 超低缓存命中**（#89139）：用户对比 Feishu 通道发现 93% vs 29% 命中率，要求复用 agent run。

**满意度**：用户普遍认可 OpenClaw 的功能覆盖面，但对近期回归频繁且修复周期较长感到不满，尤其 Beta 版本链中稳定性波动较大。

---

## 8. 待处理积压
以下为长期未闭合且影响面较大的 Issue / PR，建议维护者优先关注：

| 类型 | 编号 | 创建时间 | 优先级 | 简要 |
|------|------|----------|--------|------|
| Issue | [#35203](https://github.com/openclaw/openclaw/issues/35203) | 2026‑03‑05 | P2 | 多 Agent 协作 RFC，已 3 个月无实质更新 |
| Issue | [#42820](https://github.com/openclaw/openclaw/issues/42820) | 2026‑03‑11 | P1 | Feishu `message` 工具因 poll 字段污染无法发送文件 |
| Issue | [#51871](https://github.com/openclaw/openclaw/issues/51871) | 2026‑03‑21 | P2 | Control UI 后台 Cron 任务空白（Raspberry Pi） |
| Issue | [#44870](https://github.com/openclaw/openclaw/issues/44870) | 2026‑03‑13 | P2 | 自定义模型通过中转站验证失败，长期无回应 |
| Issue | [#75767](https://github.com/openclaw/openclaw/issues/75767) | 2026‑05‑01 | P2 | macOS 挂载 SMB 卷后 gateway 重启挂起 |
| Issue | [#80040](https://github.com/openclaw/openclaw/issues/80040) | 2026‑05‑10 | P2 | 三级级联故障（OAuth 失效、provider 切换、冷缓存） |
| PR | [#75961](https://github.com/openclaw/openclaw/pull/75961) | 2026‑05‑02 | P2 | Discord 斜杠命令部署功能，等待维护者审查 |
| PR | [#65301](https://github.com/openclaw/openclaw/pull/65301) | 2026‑04‑12 | P1 | 修复 poll 意图检测，需要实时行为证明 |

**建议**：维护团队应优先为上述 P1/P2 问题分配资源，尤其 #42820（Feishu 文件发送）和 #35203（多 Agent RFC）涉及核心架构，延期可能影响 2026.6 正式版的用户体验。

---

## 横向生态对比

好的，作为您的资深技术分析师，以下是根据您提供的2026年6月2日各开源项目动态，生成的横向对比分析报告。

---

### AI 智能体开源生态横向对比分析报告 (2026-06-02)

#### 1. 生态全景

当前个人AI助手/自主智能体开源生态正进入一个**密集迭代与质量巩固并行的关键阶段**。核心项目（如OpenClaw、ZeroClaw、Hermes Agent）均表现出极高的代码活跃度，但社区反馈显示，随着功能复杂度的提升，**稳定性回归（尤其是模型兼容性与核心链路可靠性）成为最突出的痛点**。同时，各项目不约而同地将重心转向**运行时健壮性**（中断恢复、崩溃自愈）、**成本控制**（Token优化）和**多平台适配**（Telegram、Discord、Feishu），显示出从“功能堆砌”向“生产级可用”的务实转变。此外，去中心化AI（NEAR AI Cloud）和本地化模型（Ollama、Whisper）的集成成为新的差异化竞争点。

#### 2. 各项目活跃度对比

| 项目名称 | Issues (新开/活跃) | PRs (待合并/已合并) | Releases | 核心聚焦 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 298 / 165 | 396 / 104 | 2 Beta | Codex稳定性、多渠道去重、社区回归修复 | 极高活跃，稳定性承压 |
| **ZeroClaw** | 28 / 8 | 24 / 13 | 0 | 高优Bug修复、插件化生态（WASI）、Agent评测 | 高活跃，工程化推进中 |
| **Hermes Agent** | 50 / 50 | 50 / 50+ | 0 | 系统稳定性（Cron、Docker）、多Agent Kanban编排 | 极高活跃，密集迭代与巩固并重 |
| **CoPaw** | 50 / - | 34 (合并9) | 2 (v1.1.10) | 定时任务稳定性、MCP资源管理、AgentScope 2.0迁移 | 高活跃，架构升级进行中 |
| **NanoBot** | - | 17 / - | 1 (v0.2.1) | WebUI重大升级、成本优化（心跳、本地模型） | 非常活跃，功能迭代加速 |
| **PicoClaw** | 7 (全活跃) | 6 (5合并) | 1 Nightly | Agent工具增强(exec, cron)、硬件兼容性(RISC-V) | 中等活跃，功能与稳定性并行 |
| **IronClaw** | 12 | 14 (32合并) | 0 | Reborn架构集成与测试（Budget, Trigger, OAuth） | 高活跃，Reborn分支重构关键期 |
| **NanoClaw** | 2 | 5 (1合并) | 0 | Agent运行时稳定性、容器兼容性 | 中等活跃，快速修复阶段 |
| **Moltis** | 0 | 0 (3合并) | 0 | 提供商生态扩展（NEAR AI）、代码质量重构 | 中等偏低，稳健推进 |
| **LobsterAI** | 1 | 50 (50合并) | 1 (2026.6.1) | Expert Kit Store、插件生态、功能后期清理 | 发布后密集合并期，社区情绪需关注 |
| **ZeptoClaw** | 0 | 1 (17合并) | 0 | 二进制大小控制，依赖更新与安全修复 | 低活跃，维护性开发，关注代码精良度 |
| **NullClaw** | 0 | 0 (1待合并) | 0 | Telegram交互视觉反馈 | 低活跃，维护性开发 |
| **TinyClaw** | - | - | - | 无活动 | 静默 |

#### 3. OpenClaw 在生态中的定位

- **核心参照（事实标准）**：OpenClaw 的数据量（近500条Issue和PR）和社区讨论规模明显高于其他项目，是生态中当之无愧的**旗舰项目**和**基准线**。许多项目的更新日志中都直接提及修复 `openclaw` 相关组件（如 LobsterAI 的PR #2015）。
- **优势**：
    - **生态系统最丰富**：多渠道（Telegram, QQ, Feishu, Discord）和多模型（Codex, OpenAI, Gemini）支持最为全面，是用户复用的首选。
    - **社区反馈最激烈**：其问题（Token膨胀、配置迁移破坏、Telegram重复）是社区的核心痛点，直接影响其他基于其构建的项目。
- **技术路线差异**：
    - **相比 Hermes Agent / IronClaw**： OpenClaw 更侧重于“粘合”和“兼容”，即通过插件化（？）或配置支持尽可能多的外部服务和模型。而 Hermes Agent 和 IronClaw 则在局部（如 Cron、Kanban、Reborn新架构）展现出更深的定制化开发和架构创新。
    - **相比 ZeroClaw / PicoClaw**： ZeroClaw 正尝试通过 WASI 接口定义建立插件标准，探索比 OpenClaw 更灵活、更标准化的扩展能力。PicoClaw 则更关注边缘硬件（RISC-V）和 Agent 工具本身的安全性（`guardCommand`），满足特定场景需求。

#### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/进展 |
| :--- | :--- | :--- |
| **运行时稳定性与自愈** | OpenClaw, Hermes, NanoClaw, IronClaw | Codex中断恢复、Cron崩溃修复、Agent crash-loop自愈（#2670）、上下文溢出死循环修复（#4310）。**共识：可靠性是迈入生产环境的第一道坎。** |
| **成本控制/Token优化** | OpenClaw, ZeroClaw, PicoClaw, NanoBot | Skill编译（#5146）、心跳优化跳过LLM调用、技能目录去重注入（#2781）。**共识：从“能用”到“用得起”的必然路径。** |
| **OpenAI Codex兼容性** | OpenClaw, Moltis, ZeroClaw | OAuth刷新修复、工具调用参数处理、配置迁移错误、400错误修复。**共识：Codex成为事实上的高级运行时标准，但适配细节繁多。** |
| **多Agent协作与编排** | OpenClaw, Hermes, PicoClaw | Multi-Agent RFC ( #35203 )、Kanban看板管理与自愈、Agent协作总线（#2937）。**趋势：从单一对话Agent向工作流Agent集群演进。** |
| **本地/低成本模型** | OpenClaw, ZeroClaw, NanoBot, | 本地Whisper、Ollama支持、Gemini Flex需求。**趋势：用户对成本敏感，渴望更多部署选择。** |
| **平台/渠道差异化需求** | OpenClaw, Hermes, CoPaw, ZeptoClaw | Telegram消息重复/回调反馈、Discord白名单/斜杠命令、Feishu文件发送、WhatsApp联系人过滤。**共识：成熟度取决于最弱的一环。** |
| **插件/生态扩展标准化** | ZeroClaw, LobsterAI, Moltis | WASI插件接口定义（#7060）、Expert Kit Store、NEAR AI Cloud集成。**趋势：平台化能力开始萌芽。** |

#### 5. 差异化定位分析

| 项目 | 功能侧重点 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用性最强的“超级粘合剂” | 追求功能全面、需要连接各种服务的开发者与高级用户 | 插件化（？）多渠道架构，高配置灵活性带来复杂性 |
| **ZeroClaw** | 安全性、资源受限、插件标准化 | 安全敏感、部署在IoT或边缘设备、重视社区治理的开发者 | WASI插件接口、极致的二进制大小控制、Skill编译 |
| **Hermes Agent** | 多Agent编排、系统运维与可观测性 | 需要复杂工作流（Kanban）、多用户协作、运维团队 | 内置Kanban看板、强大的Cron子系统、集群管理与Dashboard |
| **IronClaw** | 云原生、去中心化AI、下一代架构 | NEAR生态开发者、追求无状态、水平扩展的开发者 | **Reborn架构** (EventStream, Budget, Trigger)，前端与后端解耦 |
| **CoPaw** | 多模型（Qwen）、Windo环境深度优化 | 国内用户、Windows开发者、AgentScope生态用户 | 深度集成Qwen及AgentScope 2.0，专为Windows环境优化 |
| **NanoBot** | 极速迭代、低成本、人人可用 | 个人开发者、期望低门槛、关注运行成本的爱好者 | 本土化运营（钉钉、QQ频道）、WebUI工作台、低配模型优先 |
| **PicoClaw** | Agent工具安全、嵌入式/边缘计算 | 安全研究人员、RISC-V硬件开发者、对工具行为可定义需求高 | 严格的内置安全工具（exec guard）、轻量级、硬件兼容性优先 |

#### 6. 社区热度与成熟度

- **第一梯队 (极高活跃/快速迭代)**: **OpenClaw, ZeroClaw, Hermes Agent, IronClaw**。这些项目日均Issue和PR处理量均在数十以上，社区讨论激烈，功能开发与Bug修复同步高速推进。其中Hermes Agent和IronClaw偏向系统/架构级迭代，ZeroClaw和OpenClaw偏向功能广度和稳定性修复。
- **第二梯队 (高活跃/质量巩固)**: **CoPaw, NanoBot, LobsterAI**。这些项目处于版本发布后的密集合并期（LobsterAI）或架构升级期（CoPaw迁移AgentScope 2.0），功能迭代快，但整体稳定性在逐步提升。NanoBot的WebUI工作台是亮点。
- **第三梯队 (中/低活跃/维护性开发)**: **PicoClaw, NanoClaw, Moltis, ZeptoClaw**。这些项目活跃度中等偏低，主要精力在修复特定Bug和进行代码质量内省（如ZeptoClaw的二进制大小控制）。它们在特定细分领域（如硬件兼容性、提供商生态）有深度，但广度和社区规模有限。
- **静默/初始阶段**: **NullClaw, TinyClaw**。几乎无活动，处于维护或停滞状态。

#### 7. 值得关注的趋势信号

1.  **“生产级稳定性”成为集体挑战**：从 OpenClaw 的 Codex 回归到 Hermes Agent 的 Crash Loop 再到 IronClaw 的上下文溢出，项目间高度相似的稳定性 Bug 表明，当前 Agent 框架在应对复杂、长程、多工具的运行时场景时，仍缺乏一套经过大规模验证的、成熟的异常处理模式。**对开发者而言，这意味着在构建生产应用时，需要投入大量精力在自定义中断恢复、状态检查和降级策略上**。未来的核心竞争力将不取决于功能数量，而在于“有多少种方式优雅地失败”。

2.  **插件化与生态系统建设的“军备竞赛”开始**：ZeroClaw 的 WASI 接口、LobsterAI 的 Expert Kit Store、Moltis 对多个云原生提供商的支持，以及 Hermes Agent 强有力的 Dashboard 管理，都指向同一件事：**头部项目正在从“一个程序”向“一个平台”进化**。对于开发者，选择哪个项目，可能不再仅仅取决于其自带的功能，而是**其周边生态的丰富度、插件标准的开放性和未来平台锁定的风险**。

3.  **本地化与成本优化从“可选”变为“刚需”**：NanoBot 的 `faster-whisper` 集成、ZeroClaw 的 `Skill Compilation`、PicoClaw 的 Token 优化，以及多项目对 Ollama、Gemini Flex 的低成本推理支持，清晰表明**用户对运行成本极度敏感，且希望摆脱对单一商业化API的依赖**。对于AI智能体开发者，**设计时就必须将“成本效率”和“模型中立性”作为内置考量**，而非事后优化。

4.  **单一Agent的“能力边界”正在被打破**：OpenClaw 的 Multi-Agent RFC、Hermes Agent 的 Kanban、CoPaw 的子Agent生成、IronClaw 的 Trigger/EventStream，都在探索**从“点对点”聊天到“结构化工作流”** 的转变。**开发者需要开始思考如何将复杂任务（如数据监控、报告生成、多步骤审批）通过Agent编排系统来分解和自动化**，这预示着 AI Agent 的应用场景将从个人工具向团队协作和企业级任务处理升级。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将基于您提供的 NanoBot 项目数据，为您生成 2026 年 6 月 2 日的项目动态日报。

---

## NanoBot 项目动态日报 | 2026-06-02

### 1. 今日速览

今日 NanoBot 项目状态**非常活跃**。核心进展体现在 **v0.2.1 版本的正式发布**，带来了全新的 WebUI 工作台体验。社区反馈方面，Issues 和 PR 的关闭率很高（超过 80%），表明维护团队正在积极清理和解决积压问题。技术讨论焦点集中在**成本优化**、**会话管理一致性**以及**跨模态支持**（如语音、图片）上。整体来看，项目正处于功能迭代加速与稳定性加固并行的阶段，社区健康度良好。

### 2. 版本发布

- **v0.2.1 (最新发布)**
  - **更新内容**: 该版本是项目一个重要的里程碑，包含 84 个 PR 的合并，新增了 17 位贡献者。核心亮点是 **WebUI 的全面升级**，使其从简单的聊天界面进化成真正的“工作台”。具体改进包括：
    - **实时协作**: 文件编辑、工具执行痕迹在 UI 中实时渲染，提升了交互的透明度和可信度。
    - **性能与流畅度**: 聊天界面交互更流畅、响应更快。
  - **破坏性变更**: 发布说明中未明确列出，但涉及 84 个 PR 的大版本升级，建议用户在升级前仔细阅读 `CHANGELOG` 或 `v0.2.1` 的完整发布公告，特别是 WebUI 相关的配置项可能有所调整。
  - **迁移注意事项**: 建议用户在升级前备份 `config.json` 等核心配置文件，以避免因配置项变更导致服务启动异常。

### 3. 项目进展

今日项目推进效率极高，合并/关闭了 17 个 PR，解决了大量历史遗留问题和新的功能需求。

- **核心稳定性与连接修复**:
  - `#1536` **MCP重连逻辑**: 合并了 `crunchingcode` 的提交，为 MCP 服务器连接中断场景添加了自动重试机制，解决了 NanoBot 在 MCP 服务重启时必须重启才能恢复的问题。这显著提升了生产环境的可靠性。
  - `#3126` **Cron静默模式**: 修复了定时任务（Cron）在 `deliver: false` 模式下，仍会向用户发送中间思考过程的问题，让后台任务运行更“安静”。
- **功能增强**:
  - `#4016` **钉钉群聊隔离**: 合并了 `lmzopq` 的提交，新增 `group_user_isolation` 配置项，允许钉钉群聊中每个用户拥有独立的会话，避免了上下文相互干扰。
  - `#2482` & `#2435` **心跳优化**: 合并了多个关于心跳（Heartbeat）功能的优化 PR，当 `HEARTBEAT.md` 文件中没有活跃任务时，会跳过调用 LLM，从而显著节省 API 调用费用。
  - `#3723` **本地Whisper转录**: 合并了 `dilidin2` 的提交，支持集成 `faster-whisper` 实现完全离线的本地语音转录，为用户提供了无网络、无 API 费用的语音交互选项。
  - `#3509` **Napcat QQ频道**: 合并了 `LZDQ` 的提交，通过 Napcat 添加了对 QQ 频道的支持，相比官方 QQ 开放平台 bot 支持更多特性。
- **重大重构**:
  - `#4135` **WebUI事件总线**: 合入了对 WebUI 运行时状态的架构级重构，将其从硬编码的组件依赖中解耦，迁移到统一的事件总线上，这为未来 WebUI 功能的扩展和稳定性奠定了坚实基础。

### 4. 社区热点

今日最受关注的讨论主要围绕**成本优化**和**数据一致性问题**。

- **`#4142` [Discussion] 成本优化**: 这是一个关于**缓存未命中（Cache Miss）输入令牌成本优化**的讨论。作者 `hamb1y` 提出，像 DeepSeek V4 Flash/Pro 这类模型虽然本身价格低廉，但大量缓存未命中的上下文传递成本依然可观。该讨论旨在探索新的优化策略，社区关注度很高，反映了用户对**运行成本**的高度敏感。
- **`#4006` [BUG] 孤立工具结果**: 此 Bug 报告了在修复 `tool_call_id` 替换问题后，对话历史中仍然存在无法配对的“孤立”工具结果（tool result）。该问题会触发严格 API 的校验错误，并导致轨迹渲染异常。用户的诉求非常明确：**要求严格的、符合 OpenAI/Anthropic 规范的会话数据结构**。评论虽不多，但其技术影响面广，是当前亟待解决的稳定性问题。

### 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 | 修复 PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | #4006 | 对话历史中存在孤立的 tool result，导致 API 校验失败。 | **待修复** | 暂无 |
| **高** | #4081 | `append_history()` 方法在并发写入时可能导致重复消息。 | **已修复** | #4147 (已创建) |
| **高** | #4133 | Agent 完成工具调用后，最终响应未能传递给用户（如 Telegram）。 | **已解决** | 描述中提到“在 #4080 后仍存在问题”，但今日已关闭。 |
| **中** | #4128 | 会话归档逻辑 `retain_recent_legal_suffix` 在特定分支下导致用户消息被重复归档，可能引起上下文不一致。 | **已解决** | 已修复并关闭。 |
| **中** | #4069 | Dream 功能的定时任务没有 `enabled` 开关，始终被注册。 | **已解决** | 已修复并关闭。 |
| **低** | #3633 | 使用 GPT-5.5 模型时，因 `duplicate_` 工具调用 ID 导致报错。 | **已解决** | 已修复并关闭。 |

### 6. 功能请求与路线图信号

- **短期/下个版本候选**:
  - `#4142` **缓存优化**: 鉴于社区对其高度关注，且已有 `PR #3994` 对配置字段进行了重构，预计未来的版本会深入解决缓存未命中的成本问题。
  - `#4138` **文件工具开关**: 新增 `tools.file.enable` 配置，允许用户禁用内置的文件系统工具，这对仅希望使用 MCP 服务器的部署场景非常有用。`PR #4138` 已创建，极有可能被采纳。
  - `#4146` **Napcat QQ频道**: 相关 PR 已合并到 `main` 分支，正式成为官方支持的频道。
- **中期/潜力较大**:
  - `#4132` **自定义图像生成提供商**: 用户 `hesetiema` 请求支持自定义的图片生成 API，表明了用户对于扩展性和多供应商集成的强烈需求。如果该项目持续发展，这将是一个重要的里程碑。
  - `#4122` **WebUI语音录制与转录**: `PR #4122` 为 WebUI 添加了语音录制和本地 ASR 转录功能，这标志着 NanoBot 正在向**多模态交互**迈进。

### 7. 用户反馈摘要

- **正面反馈**:
  - **功能实用**: 用户 `jermeyhu` (Issue #3028) 在报告 Bug 时也肯定了心跳功能的价值，表示他期望的功能是“主动关心用户的状态和情绪”，这反映了用户对**个性化、有温度**的 AI 交互体验的期待。
  - **社区活跃**: 多个 Issue 的评论数量（如 #2880， #1932）表明社区成员乐于参与问题的排查和功能讨论，贡献者生态健康。
- **负面/痛点**:
  - **配置理解困难**: 许多问题（如 `#115`, `#1862`）反映用户对配置项的理解和文档存在偏差，特别是关于路径、权限和特定平台的设置。
  - **调试困难**: 用户 `starry-sky-domain` (Issue #1547) 和 `kronk307` (Issue #3064) 都反馈了**长时间等待无反馈**的问题，以及 Crontab 任务过多的“中间思考”消息导致渠道信息泛滥，影响了用户体验。
  - **工具泄露**: 用户 `lucndm` (PR #4124) 发现某些模型会以 XML 形式泄露工具调用细节给用户，这暴露了兼容性问题并破坏了用户体验。

### 8. 待处理积压

- **`#4142` [Discussion] 成本优化**: 该 Issue 虽然是一个讨论，但首次提出时间较早，且社区参与度高。目前尚未被项目组成员分配或标记为里程碑。建议维护者尽早介入，整理出明确的优化方向或纳入路线图。
- **`#4006` [BUG] Session数据一致性**: 作为今日最严重的 Bug 之一，目前在 4 小时内未有 Fix PR 关联，可能修复难度较大或需要更深入的讨论。建议优先分配资源，防止其阻塞其他依赖会话功能的开发工作。
- **`#3994` & `#3997` 性能与配置重构**: 这两个 PR 由 `outlook84` 创建，专注于改进 Provider 配置模型和 tokenizer 预热，属于架构层面的长期优化。虽然不紧急，但保持其活跃讨论将有助于提升项目的长期可维护性。
- **`#118` 工具动态加载**: 这是一个非常早期的 Issue，提出了“工具动态加载”的架构需求。虽然长时间未更新，但其背后的核心诉求（模块化、热插拔）仍是许多高级用户的期望。建议在未来的路线图讨论中回顾此 Issue，评估其是否与当前架构发展方向一致。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的Hermes Agent项目数据生成的日报。

---

## Hermes Agent 项目动态日报 | 2026-06-02

### 1. 今日速览

今日项目整体**活跃度极高**，过去24小时内产生了50条Issue和50条PR，社区参与度和开发响应速度均处于旺盛状态。值得注意的是，项目在**Bug修复**和**稳定性增强**方面投入了大量精力，多起严重（P1/P2）问题（如Cron子系统崩溃、Docker容器启动失败、Discord/Discord平台消息丢失）已得到快速修复并合并。同时，新功能开发（如Kanban看板管理、音频路由、TUI优化）亦有实质性推进，表明项目正处于一个**密集迭代与巩固并行的关键阶段**。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日合并/关闭了多项重要PR，显著提升了项目在各个维度的鲁棒性和功能完整性：

- **稳定性与健壮性提升**：修复了`cron`子系统因`jobs.json`格式异常而崩溃的关键问题（#37065）。针对MCP服务器配置错误（返回HTML）导致启动挂起60秒的问题，合并了多个修复方案（#36064, #36058, #37133），实现了快速故障检测与优雅降级。同时，修复了Docker容器在特定版本无法启动的回归问题（#36208已关闭）。
- **平台适配增强**：修复了WhatsApp（#37066, #37139）和WeCom（#37069）平台适配器在特定配置下权限策略未被网关正确执行的问题，确保了多平台安全模型的统一性。
- **用户体验优化**：合并了Web API的错误处理优化（#36840, #36843），将无效环境变量键名删除等操作返回明确的HTTP 400状态码，而非模糊的500错误。TUI方面也做了清理，去除了重复的`/provider`命令（#37112）。
- **功能推进**：`feat(dashboard)` PR（#36736）对管理面板进行了大幅完善，使MCP、Webhook、系统状态等运维操作在浏览器端完全可管理。同时，`feat: native audio routing`（#37149）为新多模态模型的原生音频支持铺平了道路。

### 4. 社区热点

本周讨论最热烈、反映社区核心诉求的议题如下：

1.  **[#5143] [Feature] Multi-Role Auto-Routing via Gateway Hooks（👍 14, 评论 5）**
    - **链接**: [NousResearch/hermes-agent Issue #5143](https://github.com/NousResearch/hermes-agent/issues/5143)
    - **分析**: 这是一个获得大量赞同的功能需求，旨在为Gateway增加多角色自动路由能力。社区用户（`OlegB333`）在5月份根据新架构重写了提案，表明其对项目现有设计有深入理解，并希望利用Gateway Hooks机制构建更复杂的、基于用户角色的访问控制和工作流分发逻辑。这反映了用户从单代理管理向多角色、细粒度协作模式演进的需求。

2.  **[#10149] [Bug]: No auxiliary LLM provider configured（👍 16, 评论 1）**
    - **链接**: [NousResearch/hermes-agent Issue #10149](https://github.com/NousResearch/hermes-agent/issues/10149)
    - **分析**: 这是一个老问题，但获得了迄今为止最高的反应数（16个赞），说明有大量用户正被此问题困扰。用户已配置了`OPENROUTER_API_KEY`，但运行时仍提示“未能配置辅助LLM提供程序”。这暴露出项目在配置检查、环境变量读取或模型路由选择上存在用户感知不清晰或逻辑错误的地方。社区强烈希望项目能提供更明确、友好的配置验证反馈。

3.  **[#35322] WebSocket connections rejected when dashboard bound to 0.0.0.0（评论 7）**
    - **链接**: [NousResearch/hermes-agent Issue #35322](https://github.com/NousResearch/hermes-agent/issues/35322)
    - **分析**: 该Bug报告详细描述了在`--insecure`模式下将Dashboard绑定到`0.0.0.0`时，HTTP中间件正常但WebSocket升级请求被拒绝的问题。这是一个典型的使用场景（开发环境或内部网络部署），背后诉求是希望项目能正确处理非loopback地址的WebSocket连接，以保证Dashboard功能的完整可用性。

### 5. Bug 与稳定性

今日报告的Bug呈现**低频次、高严重性**但**快速修复**的特点。以下按严重程度排列：

- **P1级（严重）**：
    - **Cron子系统崩溃**：`load_jobs()` 在读取格式错误的`cron/jobs.json`（如数组而非对象）时会抛出未捕获的`AttributeError`，导致整个定时任务系统停摆。 **【已修复】** PR #37065 已合并。
    - **Docker容器启动失败**：从版本2026.5.28开始，官方Docker容器在启动阶段失败，直接阻塞所有使用Docker部署的用户。 **【已修复】** PR #36208 已关闭。
    - **Discord消息静默丢弃**：当Agent响应涉及多次API调用时，包含工具使用的响应在Discord上会被静默丢弃（无日志），严重影响了核心通信链路。 **【已修复】** PR #29346 已关闭。
- **P2级（重要）**：
    - **WhatsApp/WeCom权限策略失效**：`dm_policy` 和 `group_policy` 设置为`open`时，因网关与适配器之间策略冲突未能生效，导致用户被错误拒绝。 **【已修复】** PRs #37066, #37139, #37069 已合并。
    - **MCP WebSocket连接阻塞**：MCP工具在WebSocket路径上执行后，连接未被正确关闭，导致资源泄漏和后续操作问题。
- **P3级（一般）**：
    - **错位的`hermes stop`命令提示**：`claw migrate`工具错误地提示用户使用不存在的`hermes stop`命令，造成用户困惑。【已修复】PR #36771 已关闭。

### 6. 功能请求与路线图信号

社区对未来版本的功能呼声主要集中在两个方面：

- **AI能力增强与成本优化**：
    - **支持Gemini Flex推理**（#12700, 👍 6）：用户希望利用Gemini新发布的低成本`Flex`模式来运行后台定时任务和子代理，以优化运营成本。这与项目正在发展的`cron`和Kanban功能高度契合。
    - **MongoDB记忆提供者**（#5495, 👍 1）：社区希望有一个官方的MongoDB记忆后端，以便在需要外部、持久化、可扩展记忆的场景下（如企业级或复杂个人助理）有一个稳定可靠的选择。
- **系统可观测性与运维体验**：
    - **多配置文件共享记忆与按需胶囊召回**（#31388）：在高级用户中，出现了对多配置文件环境本地共享记忆的明确需求，希望在不改变现有架构的前提下，实现用户偏好、项目约定等跨配置信息的共享。
    - **Kanban看板可靠性**（#35986） & **看板面板增强**（#37108, #37109）：用户（`magnus919`, `Sanetuk`）正积极推动Kanban多代理编排功能走向成熟，提出了包括任务卡住检测、故障静默恢复、活跃工作进程面板等在内的一系列可靠性增强和建议。这与今日合并的看板管理面板PR（#36736）方向一致，预示着Kanban可能会成为下个版本的核心亮点。

### 7. 用户反馈摘要

从Issue评论中可以提炼出以下真实用户反馈：

- **配置复杂度与透明度**：多位用户（如#10149, #35322, #28156）对配置项如何生效感到困惑。例如，用户不明确为何配置了环境变量仍报错，或者不理解为何WebSocket行为与HTTP不同。这表明项目在CLI向导、配置校验和文档说明上仍有提升空间，以降低用户的心智负担。
- **场景匹配与功能缺失**：用户`Twanislas`（#12700）和`leavedrop`（#31388）的请求表明，一些高级用户已经将Hermes Agent应用于复杂场景（如成本敏感的后台任务、团队协作环境），他们希望项目能提供更精细的**成本控制**（如选择推理层）和**更灵活的上下文共享**机制。
- **对快速修复的认可**：从多个P1/P2级别的Bug能迅速获得修复并合并来看（如Docker启动、Cron崩溃、Discord消息丢失），社区对项目维护团队的**快速响应和修复能力**是持肯定态度的。用户`karmeleon`在报告后不久，问题即被标记为已关闭。

### 8. 待处理积压

- **PR #10589 (feat: automatic Telegram bot creation)**：这是一个已开启近两个月的PR，旨在通过Telegram新API实现“零配置”创建Bot体验，对降低新用户入门门槛至关重要。虽然已有后续PR #28272跟进，但其长期开放状态值得维护者关注，以推动此重要特性尽快落地。
- **Issue #11665 (Memory char limits ignored by CLI/MCP tool dispatch path)**：此问题报告于4月17日，指出配置中的内存字符限制在CLI和MCP工具路径下失效。虽然评论数不多，但这是一个影响功能一致性的P2级Bug，可能导致用户精心配置的限制规则被意外绕过。建议维护者评估其影响范围并安排修复。

---

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报  
**日期：2026-06-02**  
**数据来源：** [sipeed/picoclaw GitHub](https://github.com/sipeed/picoclaw)

---

## 1. 今日速览

- 过去24小时项目活跃度较高：共更新 **7 个 Issues**（全部活跃，无关闭）和 **11 个 PR**（其中5个已合并/关闭，6个仍待合并）。
- **新版本发布**：`v0.2.9-nightly.20260602.426046fc`，为自动构建的夜间版，可能包含不稳定变更。
- **关键修复方向**：今日合并的 PR 聚焦于 **Agent LLM 空响应重试**、**Cron 工具增强**、**Bedrock 模型 temperature 兼容性** 以及 **路径符号链接修复**。
- **社区重点关注**：`exec` 工具的 `guardCommand` 路径校验逻辑缺陷（#1042）获得15条评论，成为讨论热点；多个 “safety guard” 相关的 Bug 和模型兼容性问题仍在推进。
- 项目整体处于 **功能迭代与稳定性并行** 的阶段：既有大型新特性（Agent 协作总线 #2937）在评审，也有多个长期存在的 Bug 等待合入修复。

---

## 2. 版本发布

### nightly: v0.2.9-nightly.20260602.426046fc  
- **类型**：自动构建的夜间版，声称“可能不稳定，请谨慎使用”。  
- **变更范围**：从 `v0.2.9` 到 `main` 分支的所有未发布更改，完整 changelog 见 [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)。  
- **破坏性变更 / 迁移注意事项**：  
  - 此版本为 nightly，未提供正式迁移指南，建议仅用于测试环境。  
  - 若用户希望使用稳定版本，建议等待下一个正式 patch 或 minor 版本发布。

---

## 3. 项目进展 （今日合并/关闭的重要 PR）

过去24小时内共有 **5 个 PR 被合并或关闭**，显著推进了以下功能与修复：

| PR | 标题 | 状态 | 影响概述 |
|----|------|------|----------|
| [#2982](https://github.com/sipeed/picoclaw/pull/2982) | fix(bedrock): drop temperature for models that deprecate it (Opus 4.8) | ✅ 已合并 | 修复 AWS Bedrock 下 Claude Opus 4.8 因 `temperature` 参数被弃用导致的 400 错误。 |
| [#2977](https://github.com/sipeed/picoclaw/pull/2977) | feat(cron): add get and update actions to cron tool | ✅ 已合并 | 扩展 Cron 工具，允许 Agent 查看完整的持久化任务负载并执行部分更新，避免“删除→重新添加”带来的调度重置问题。 |
| [#2890](https://github.com/sipeed/picoclaw/pull/2890) | fix: resolve symlinks in cwdPath on macOS | ✅ 已合并 | 修复 macOS 上 `/var`→`/private/var` 符号链接导致的路径验证失败，提高测试稳定性。 |
| [#2893](https://github.com/sipeed/picoclaw/pull/2893) | feat: add Server酱³ Bot (SC3Bot) channel support | ✅ 已合并 | 新增 Server酱³ 作为消息通道，支持轮询和 Webhook 模式，拓展了国内用户的通知集成能力。 |
| [#2781](https://github.com/sipeed/picoclaw/pull/2781) | perf: reduce skill catalog token usage on tool iterations | ✅ 已合并 | **重要性能优化**：技能目录（XML 列表）不再在每次 LLM 请求（包括工具调用回合）中重复注入，大幅节省 Token 消耗，尤其对无 prompt caching 的提供商效果显著。 |

> **项目整体进展**：今日合入了 **1 个性能优化、2 个新功能、2 个平台/模型兼容性修复**，项目在稳定性、功能丰富度和性能方面均有正向提升。

---

## 4. 社区热点

以下 Issues/PR 在24小时内获得最活跃的讨论（以评论数排序）：

### #1042 – [BUG] exec 工具的 guardCommand 方法问题  
- **评论数：** 15 | 👍：2  
- **链接：** [Issue #1042](https://github.com/sipeed/picoclaw/issues/1042)  
- **背景：** 当 `restrict_to_workspace` 开启时，正则匹配错误地将 `curl -s "wttr.in/Beijing?T"` 中的域名识别为 `../../../../Beijing?T` 路径，导致命令被误拦截。  
- **社区诉求：** 用户认为该方法“简单粗暴”，期望对非文件路径的命令进行更智能的检查（例如检查是否真的涉及文件操作）。目前没有对应的 fix PR，但讨论热度高，说明工具安全机制需要更细致的设计。

### #2887 – .deb 版本在 RISC-V 上无法使用 OpenAI 模型  
- **评论数：** 8 | 👍：0  
- **链接：** [Issue #2887](https://github.com/sipeed/picoclaw/issues/2887)  
- **背景：** RISC-V 架构的 .deb 包运行时，调用 OpenAI 模型（如 GPT-5.4-2026-03-05）失败。用户提供了详细的系统信息（Debian GNOME、Go 1.25.9），但问题原因尚未明确。  
- **社区诉求：** RISC-V 用户希望获得架构兼容性保障，可能涉及底层网络库或加密库的差异。

### #2720 – 单例 PID 检查未验证进程身份，导致崩溃循环  
- **评论数：** 7 | 👍：0  
- **链接：** [Issue #2720](https://github.com/sipeed/picoclaw/issues/2720)  
- **背景：** PID 文件中的旧 PID 被系统无关进程（如 `systemd-resolved`）复用，导致 Gateway 启动时误判已有实例运行，从而拒绝启动。已有修复 PR [#2813](https://github.com/sipeed/picoclaw/pull/2813) 在等待合并。  
- **社区诉求：** 用户期望尽快合入该修复，避免生产环境因意外 PID 复用导致的启动失败。

---

## 5. Bug 与稳定性

按严重程度排列，并标注是否已有 fix PR：

| 严重性 | Issue | 摘要 | 已有 fix PR? |
|--------|-------|------|--------------|
| **高** | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | 单例 PID 检查未验证进程身份，导致崩溃循环（stale PID 被系统进程占用）。 | ✅ PR [#2813](https://github.com/sipeed/picoclaw/pull/2813) 待合并 |
| **高** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | RISC-V 架构下 .deb 无法使用 OpenAI 模型。 | ❌ 无 |
| **中** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` 工具 `guardCommand` 误拦截无文件路径的命令。 | ❌ 无 |
| **中** | [#2941](https://github.com/sipeed/picoclaw/issues/2941) | 默认配置文件使用 `claude-sonnet-4.6`（点号），Anthropic API 要求连字符，导致 404。 | ✅ PR [#2942](https://github.com/sipeed/picoclaw/pull/2942) 待合并 |
| **中** | [#2939](https://github.com/sipeed/picoclaw/issues/2939) | `claude-opus-4-7` 调用失败：API 返回 `temperature is deprecated`。 | ✅ PR [#2940](https://github.com/sipeed/picoclaw/pull/2940) 待合并 |
| **低** | [#2796](https://github.com/sipeed/picoclaw/issues/2796) | 历史记录中，多次用户消息只能看到最后一条。 | ❌ 无 |
| **低** | [#2982](https://github.com/sipeed/picoclaw/pull/2982)（已修复） | Bedrock 上 Opus 4.8 因 temperature 弃用而失败。 | ✅ 今日已合并 |

> **稳定性风险提示：** 三个高/中严重度的 Bug 虽有对应 PR，但均处于“待合并”状态（`stale` 标签），未能及时进入主线，可能影响部分用户的实际使用。

---

## 6. 功能请求与路线图信号

### 正在评审的新功能（待合并 PR）

| PR | 标题 | 路线图关联 |
|----|------|-----------|
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) | **Feat/agent collaboration** – 引入 Agent 协作总线，支持持久化信箱、协作线程、结构化消息信封等 | ✅ **重大特性**，可能构成 v0.3.0 或后续版本的核心变化，需要社区和开发者深度评审。 |
| [#2917](https://github.com/sipeed/picoclaw/pull/2917) | **NEAR AI Cloud provider** – 新增 OpenAI 兼容的 NEAR AI Cloud 提供商，带默认 API 基址和 TEE 模型建议 | 🔥 扩展生态，满足去中心化 AI 场景需求。 |
| [#2983](https://github.com/sipeed/picoclaw/pull/2983) | **fix(agent): retry empty llm response** – 修复 OpenAI 兼容提供商返回空 `content: null` 导致失败的问题 | 属于稳定性和可靠性增强，很可能进入下一个小版本。 |

### 用户提出的功能需求（来自 Issues）

- **#2981** – 文档更新任务：v0.2.9 变更较多，需要更新使用手册。这是一个维护性任务，并非新功能，但反映了版本迭代后文档滞后的痛点。
- **#2796** – 历史记录显示不完整：用户期望消息压缩只针对 LLM，用户端应显示完整历史。这可能是 UI/UX 改进的信号。

> **判断：** 短期内项目重点可能是合入现有的待合并 PR（尤其是 #2937 和 #2917），并修复 #2720、#2941、#2939 等稳定性 Bug。文档更新（#2981）优先级可能被低估，建议维护者关注。

---

## 7. 用户反馈摘要

从 Issues 评论（基于摘要推断）及讨论热度中提炼的典型用户声音：

1. **“安全机制过于简单粗暴”** —— #1042 用户指出 `guardCommand` 仅通过正则检查路径，忽略了根本不存在文件操作的命令。期望更智能的安全检查逻辑（如区分“执行命令”与“读写文件”）。
2. **“默认配置开箱即用率低”** —— #2941、#2939 的用户在首次安装后立即遇到模型 ID 格式错误和参数弃用问题，表明默认配置的兼容性测试不足，影响了新用户的 onboarding 体验。
3. **“历史记录的信息完整性不足”** —— #2796 用户反馈多轮对话中只能看到最后一条用户消息，怀疑是消息压缩机制误影响了前端展示。用户明确表示“对用户显示的历史消息应该完整”。
4. **“RISC-V 用户被边缘化”** —— #2887 用户使用 .deb 包在 RISC-V 上运行，却无法调用主流 OpenAI 模型，且未得到及时回复（已创建 16 天）。这反映出对非 x86/ARM 架构的关注度不够。

---

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者响应或存在明显延迟，可能影响项目健康状况：

| 类型 | 链接 | 创建日期 | 最后更新 | 备注 |
|------|------|----------|----------|------|
| Issue | [#2720](https://github.com/sipeed/picoclaw/issues/2720) | 2026-04-30 | 2026-06-01 | 严重 Bug，对应 PR #2813 已存在一个月仍未被合并（带 `stale` 标签）。 |
| Issue | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | 2026-03-04 | 2026-06-01 | 3个月的老 Issue，评论数最多，但无任何维护者回复（无 `assigned` 或 `milestone`），处于事实上无人处理状态。 |
| Issue | [#2796](https://github.com/sipeed/picoclaw/issues/2796) | 2026-05-07 | 2026-06-01 | 历史记录显示 Bug，无 assignee，无 PR。 |
| PR | [#2813](https://github.com/sipeed/picoclaw/pull/2813) | 2026-05-07 | 2026-06-01 | 修复 #2720 的 PR，带 `stale` 标签，可能因未通过 CI 或缺乏 review 而停滞。 |
| PR | [#2942](https://github.com/sipeed/picoclaw/pull/2942) | 2026-05-25 | 2026-06-01 | 修复默认 model ID 格式，8天无人合并。 |
| PR | [#2940](https://github.com/sipeed/picoclaw/pull/2940) | 2026-05-25 | 2026-06-01 | 修复 temperature 弃用，同样8天待合并。 |

> **建议行动：** 维护者应优先 review 并合并 #2813（PID 安全修复）、#2942 和 #2940（模型兼容性修复），这些 Bug 直接影响用户首次使用体验。同时，对 #1042 给出明确答复或将任务指派给相关开发者，避免社区长期失望。

---
*本日报基于公开数据自动分析生成，仅供内部参考。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw 项目动态日报 (2026-06-02)

### 1. 今日速览
过去24小时项目保持活跃：新增2个Bug issue和1个High优先级Bug被关闭；6个PR中有5个待合并，1个已合并；无新版本发布。核心focus集中在**agent运行稳定性**与**容器兼容性**修复上，社区提交的crash-loop自愈方案（#2670）与Provider故障回滚机制（#2666）正在review中，项目整体处于“快速修复+功能加固”阶段。

---

### 3. 项目进展
- **[已合并] PR #2664 – 在v2容器中运行浏览器爬虫Sidecar**  
  作者`whahnize`在5月31日提交，该PR将browser scraping sidecar集成到v2容器架构中，缩短了多模态抓取场景的部署链路。  
  https://github.com/qwibitai/nanoclaw/pull/2664

- **[待合并] PR #2670 – 修复agent-runner中毒恢复崩溃循环**  
  针对Issue #2669提出的“thinking blocks cannot be modified”400错误，作者`ddaniels`通过检测result event而非throw异常来激活自愈逻辑，避免session永久卡死。  
  https://github.com/qwibitai/nanoclaw/pull/2670

- **[待合并] PR #2666 – Provider故障恢复：回滚、重放、确认与友好降级**  
  该PR实现了一个多层恢复机制：在LLM调用失败时自动回滚到上一个有效状态、重放请求、向用户发送in-turn确认，并支持降级到备选Provider。依赖#2667（rootless Podman修复）先合并。  
  https://github.com/qwibitai/nanoclaw/pull/2666

- **[待合并] PR #2671 – 修复附件目录挂载问题**  
  为agent容器添加只读绑定挂载`<DATA_DIR>/attachments/`至`/workspace/attachments/`，解决channel adapter无法访问传入附件的问题。  
  https://github.com/qwibitai/nanoclaw/pull/2671

- **[待合并] PR #2346 – 格式化器将未知斜杠命令视为普通聊天**  
  避免Claude Code SDK错误地将非标准命令归类为`passthrough`导致响应丢失。  
  https://github.com/qwibitai/nanoclaw/pull/2346

---

### 4. 社区热点
- **Issue #2331（已关闭）**  
  `findSessionByAgentGroup`在多频道组中路由A2A回复到错误session的Bug被修复。虽然评论仅1条，但该问题被标记为High优先级，社区维护者`glifocat`快速定位并关闭。  
  https://github.com/qwibitai/nanoclaw/issues/2331

- **Issue #2669（开放）**  
  讨论度虽低（0评论），但“crash-loop forever”的描述引发关注，已有对应PR #2670快速响应。社区对agent稳定性具有较高敏感度。  
  https://github.com/qwibitai/nanoclaw/issues/2669

---

### 5. Bug 与稳定性
| 严重程度 | Issue / PR | 描述 | 修复状态 |
|----------|------------|------|----------|
| 🔴 High | #2331 | `findSessionByAgentGroup`路由错误导致A2A回复错发 | ✅ 已关闭 |
| 🔴 High | #2669 | 损坏的恢复Transcript导致agent crash-loop | ⏳ 有PR #2670待合并 |
| 🟡 Medium | #2668 | 单工具调用无超时，挂起MCP工具会阻塞session长达30分钟 | ❌ 尚无PR |
| 🟡 Medium | #2671 | agent容器内附件目录缺失，导致channel adapter失败 | ⏳ 有PR #2671待合并 |
| 🟢 Low | #2346 | 未知斜杠命令被错误处理，造成响应消失 | ⏳ 有PR #2346待合并 |

---

### 6. 功能请求与路线图信号
- **每个工具独立超时设置（#2668）**  
  用户`mshirel`报告MCP工具调用无超时，导致session被阻塞。该问题本质是一个功能缺失请求：需要为每个工具配置独立的超时参数。目前无对应PR，但已有讨论表明社区希望加入。

- **Provider故障恢复机制（PR #2666）**  
  作者`dtreskunov`提交了包含回滚、重放、确认和友好降级的完整恢复方案。该PR被标记为依赖#2667（rootless Podman支持），表明项目正在构建更健壮的Provider容错层，很可能纳入下一版本。

- **浏览器爬虫Sidecar v2容器化（PR #2664，已合并）**  
  表明NanoClaw正在统一v2容器运行时，将更多外部服务（如browser scraping）作为容器sidecar运行，简化部署。

---

### 7. 用户反馈摘要
- **Issue #2331（已关闭）**  
  用户`glifocat`反馈`findSessionByAgentGroup`使用`ORDER BY created_at DESC LIMIT 1`选择最新活跃session，在多频道组（多agent group共享同一会话渠道）时，导致A2A回复路由到错误session。该问题在关闭前获得1条评论，推测为维护者确认修复。用户痛点：多通道场景下消息路由混乱，影响多机器人协作。

- **Issue #2669**  
  用户`ddaniels`描述agent session因corrupt transcript永久卡死，日志循环报`thinking blocks cannot be modified`400错误。用户认为应自愈而不是无限重试，表达了“agent-runner应有自我保护能力”的预期。

- **Issue #2668**  
  用户`mshirel`指出当前工具调用无超时，单个MCP工具挂起会导致整个session阻塞最长30分钟，且heartbeat在此期间不更新。用户希望有per-tool timeout或至少能中断长时间运行的调用。

---

### 8. 待处理积压
- **PR #2346（2026-05-08创建，超30日未合并）**  
  修复格式化器对未知斜杠命令的处理，属于用户体验改进，但长期未合并。可能与reviewer资源或与其他PR冲突有关，建议维护者尽快评估。  
  https://github.com/qwibitai/nanoclaw/pull/2346

- **Issue #2668（2026-06-01创建，无PR）**  
  缺少工具超时控制，虽为新提交但影响范围广（任何依赖MCP工具的场景），且无临时规避方案，建议列为下一版本必须项。  
  https://github.com/qwibitai/nanoclaw/issues/2668

- **PR #2667（rootless Podman修复）**  
  作为#2666的前置依赖，其进度直接影响Provider故障恢复功能的合入，至今未合并。建议reviewer优先处理。  
  https://github.com/qwibitai/nanoclaw/pull/2667

--- 
*数据采集截止时间：2026-06-02 12:00 UTC*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 — 2026-06-02

---

## 1. 今日速览

过去24小时，NullClaw 项目保持平稳低活跃度：无新的 Issue 或版本发布，仅有一项针对 Telegram 交互体验的 Pull Request 处于待合并状态。该 PR 修复了回调查询时缺少“正在输入”打字指示器的问题，属于对已有功能细节的打磨。整体来看，项目当前处于维护性开发阶段，社区讨论较冷清，无重大功能推进或用户反馈激增。

---

## 3. 项目进展

**今日无已合并/关闭的 PR**。唯一开放的 PR `#943` 仍在等待审核与合并，尚未对主分支产生实际推进。

- **PR #943**（待合并）  
  - 内容：修复 Telegram 回调查询（`callback_query`）处理期间无打字指示器的问题。当用户点击内联按钮（如 `nc_choices` 选项）时，代理处理过程中聊天窗口保持静默，该 PR 为这一过程添加了 `typing...` 指示器，提升用户等待时的可见反馈。  
  - 状态：由 raskevichai 于 2026-06-01 提交，截至今日未收到评论或审核。

> 链接：https://github.com/nullclaw/nullclaw/pull/943

---

## 4. 社区热点

今日社区讨论最为（唯一）活跃的条目为 **PR #943**，其背后诉求清晰：  
- 用户在使用 Telegram 交互时，内联按钮导致的回调处理全程无任何 UI 反馈（无“正在输入”指示器），导致体验割裂——用户无法判断代理是否仍在处理。  
- 该 PR 直接对应已关闭的 Issue #942，表明该问题至少由一位用户报告并推动了修复。

尽管当前零评论，但作为唯一活跃的 PR，它代表了社区对**即时交互反馈**的隐性需求。

> 链接：https://github.com/nullclaw/nullclaw/pull/943

---

## 5. Bug 与稳定性

**今日无新报告的 Bug / 崩溃**。  
该 PR 本身属于**视觉反馈缺失**的体验性缺陷修复，严重程度较低（非功能性崩溃或数据丢失）。已有对应修复 PR 等待合并。

---

## 6. 功能请求与路线图信号

**今日无新的功能请求 Issue 创建**。  
从 PR #943 的摘要看，其修复范围限定于 Telegram 通道的交互细节，未暗示新功能或架构变更。项目路线图暂无可见更新信号。

---

## 7. 用户反馈摘要

**今日无用户评论或 Issue 讨论**。  
唯一可参考的用户反馈来自已关闭的 Issue #942（未展示具体内容），其诉求即“在 Telegram 回调处理时显示打字指示器”。该反馈被视为真实痛点，促使开发者提交了修复 PR。

---

## 8. 待处理积压

**今日无长期未响应的 Issue 或 PR**。  
PR #943 提交仅一天，尚在正常等待审查周期内；但持续零评论和零审核可能表明核心维护者注意力有限，建议关注该 PR 的合并进度以避免积压。

> 链接：https://github.com/nullclaw/nullclaw/pull/943

---

**项目健康度评估**：低活跃但稳定；修复方向正确，但社区互动与响应速度有提升空间。建议维护者加速 PR #943 的审核与合并，并为 Telegram 交互体验的后续改进（如进度提示）保持关注。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 IronClaw GitHub 数据生成的 2026 年 6 月 2 日项目动态日报。

---

## IronClaw 项目日报 | 2026-06-02

### 1. 今日速览

项目今日进入 **高活跃度** 状态，尤其围绕“Reborn”分支的开发和重构工作密集推进。过去 24 小时内，共有 12 条 Issue 和 46 条 PR 被更新，其中 1 个遗留 Issue 被关闭，32 个 PR 已被合并/关闭。这表明核心开发团队正在进行一轮集中的代码合并与质量巩固工作。值得注意的是，新报告的 Issue 高度集中在 `module:M3-agentloop-turns` 模块的 Compaction 和 Budget 机制上，显示出项目正在攻克 Reborn 架构中的关键稳定性和正确性问题。

### 2. 版本发布

无

### 3. 项目进展

今日项目取得了显著进展，大量与 Reborn 架构相关的关键 PR 被合并，标志着项目从功能开发阶段逐步向集成和测试阶段迈进。

- **GSuite 与 OAuth 集成**：
    - 合并了一系列 PR (#4293, #4297, #4300) 以集成 GSuite（Gmail/Google Calendar）能力，并完善了 Google 和 Notion 的 OAuth 提供商支持。这显著增强了 Reborn 的生态集成能力。
    - PR #4294 也已开启，旨在将 Google/GitHub OAuth 登录功能真正生效于 WebUI v2。

- **Trigger（触发器）系统**：
    - PR #4301 (PR15: Add trigger poller core) 和 PR #4292 (Add trigger materialization turn-state seams) 被合并，为 Reborn 的定时触发器功能建立了核心轮询引擎和状态转换接口。PR #4308 (Add trigger poller harness coverage) 也已开启，旨在为这个新系统增加测试覆盖。

- **核心循环与预算管理**：
    - 大型 PR #3899 (Reborn budgets: address all follow-ups) 被合并，这是一个重要的里程碑，它实现了 Reborn 基于成本的预算管理系统的所有待办事项，使 Token 使用统计和预算决策更加完备。
    - PR #4286 (Surface NEAR AI credit exhaustion) 的合并，使得 Reborn 组件能够感知并报告因 NEAR AI 积分耗尽导致的模型调用失败，提升了用户体验。

- **安全性与验证**：
    - PR #4306 (Validate provider capability inputs) 被合并，增加了一层对工具调用参数的 JSON Schema 校验，提升了 Reborn 运行时环境的安全性。

- **文档与代码一致性**：
    - PR #4302 (reconcile crate AGENTS.md maps) 由社区贡献者开启，旨在更新各个 Crate 的文档以匹配最新代码，体现了社区对项目质量的关注。

**总结**：项目整体在“集成”和“稳定性”上迈进了一大步，Reborn 架构的核心组件（EventStream, Budget, Trigger, OAuth）正在被填充和连通。

### 4. 社区热点

今日最受关注的 Issue 是 **#3281 [CLOSED] [suggested_P0, reborn, module:M5-events-streaming] Add EventStreamManager for durable projection fanout**。

- **链接**: [nearai/ironclaw Issue #3281](https://github.com/nearai/ironclaw/issues/3281)
- **分析**: 该 Issue 被打上 `suggested_P0` (最高优先级) 标签，且积累了 6 条评论，是今日讨论最深入的议题。其核心诉求是创建一个生产级别的 `EventStreamManager`，将 Reborn 的投影快照/更新转化为持久化、可重放的事件流，供 Web SSE、WebSocket 等订阅服务使用。该 Issue 今日被关闭，表明其功能已在相关的 PR 中实现，标志着 Reborn 在支持实时、可靠的外部事件通知方面取得了关键突破。

### 5. Bug 与稳定性

今日报告的 Bug 高度集中，且全部由开发者 `henrypark133` 提出，主要涉及 Reborn 的 Compaction（上下文压缩）机制。这些问题严重性高，直接关系到 Agent 行为的正确性和可靠性。

- **严重**：
    1.  **#4310**: **Context-overflow recovery 修复错误**。
        - **问题**: 发生上下文溢出时，系统尝试发送“缩小上下文”的信号，但执行器并未真正执行缩小操作，导致重试时仍会提交过大的提示词，从而陷入死循环。
        - **状态**: **无修复 PR**。
        - **链接**: [nearai/ironclaw Issue #4310](https://github.com/nearai/ironclaw/issues/4310)
    2.  **#4309**: **Compaction 摘要写入导致重试阻塞**。
        - **问题**: 压缩摘要写入成功但检查点失败会导致状态不一致，重试时会尝试重建相同的压缩范围，可能无法推进对话。
        - **状态**: **无修复 PR**。
        - **链接**: [nearai/ironclaw Issue #4309](https://github.com/nearai/ironclaw/issues/4309)
    3.  **#4314**: **CompactionLeakDetected 里程碑已死**。
        - **问题**: 代码中定义了检测到内存泄漏的里程碑，但实际代码路径从未触发它，导致该功能形同虚设。
        - **状态**: **无修复 PR**。
        - **链接**: [nearai/ironclaw Issue #4314](https://github.com/nearai/ironclaw/issues/4314)

- **中等**：
    1.  **#4311**: **预算治理失败错误归类为上下文溢出**。
        - **问题**: 非上下文相关的预算错误被错误映射为上下文溢出，导致系统采取了错误的恢复策略。
        - **状态**: **无修复 PR**。
        - **链接**: [nearai/ironclaw Issue #4311](https://github.com/nearai/ironclaw/issues/4311)

- **自动化报告**：
    1.  **#4108**: **Nightly E2E 测试失败**。
        - **问题**: Github Actions 自动报告的 v2-engine 端的端到端测试持续失败。
        - **状态**: **无修复 PR**。
        - **链接**: [nearai/ironclaw Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

### 6. 功能请求与路线图信号

- **WebUI 与用户反馈**：
    - **#4287**: 请求为 WebUI 集成 OAuth 登录。这与今日合并的多个 OAuth 相关 PR 目标一致，很可能在下一个版本中实现。
        - [Issue #4287](https://github.com/nearai/ironclaw/issues/4287)
    - **#4312**: 请求在用户界面中展示“上下文压缩”的进度。这是对用户透明度的直接诉求，核心维护者 `henrypark133` 已创建该 Issue，表明其已被纳入考虑。
        - [Issue #4312](https://github.com/nearai/ironclaw/issues/4312)

- **社区疑问与架构探讨**：
    - **#4279**: 一位新用户 `liaoqianchuan` 对 Reborn 分支的云原生架构和无状态 Agent 模式表达了浓厚兴趣，并询问了路线图及开发者适配难度。这反映了社区对项目高层次的架构演进方向存在信息需求。
        - [Issue #4279](https://github.com/nearai/ironclaw/issues/4279)

### 7. 用户反馈摘要

- **正向反馈**：Issue #4279 的用户对 Reborn 分支“向无状态 Agent 模型和云原生部署的转变”表示认可，认为“解耦状态管理对于扩展到多用户、多租户环境至关重要”。这表明项目的技术愿景获得了早期关注者的积极评价。
- **痛点与优化建议**：同一用户在 Issue #4278 中指出了 `ENGINE_V2` 实现中的一个潜在性能问题：对话历史存储为单个 JSON 对象可能导致上下文窗口在长对话中快速耗尽。这指出了现有架构在新场景下的可扩展性瓶颈。
    - [Issue #4278](https://github.com/nearai/ironclaw/issues/4278)

### 8. 待处理积压

- **Nightly E2E 测试持续失败 (#4108)**：该 Issue 已存在 6 天，反映了主干代码可能包含了未经测试的破坏性变更，这会拖慢项目迭代并降低开发者对代码库稳定性的信心。建议核心维护者优先调查此问题。
    - [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

- **多个高优先级 Compaction Bug 尚无修复 PR**：Issues #4310, #4309, #4314 作为 `scope: agent` 和 `module:M3-agentloop-turns` 的关键 Bug，今日刚刚提出，尚未有对应的修复 PR。维护者应及时响应并规划修复优先级，以免影响整个 Reborn Agent 循环的可靠性。
    - [Issue #4310](https://github.com/nearai/ironclaw/issues/4310)
    - [Issue #4309](https://github.com/nearai/ironclaw/issues/4309)
    - [Issue #4314](https://github.com/nearai/ironclaw/issues/4314)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI 项目数据，我为您生成了 2026年6月2日的项目动态日报。

---

### LobsterAI 项目动态日报 (2026-06-02)

#### 1. 今日速览

今日项目整体处于 **新版本发布后的密集合并与清理期**。活跃度极高，24小时内合并/关闭了高达 **50个** Pull Request，并发布了 **2026.6.1** 版本，显示出项目组在版本迭代末尾的强力推进。然而，社区唯一新提出的 Issue 是一则关于积分订阅清零的强烈投诉，暴露了用户对现有积分策略的严重不满，这可能是社区层面的一个潜在风险点。总体而言，项目工程进展迅速，但用户情绪管理需引起重视。

#### 2. 版本发布

- **2026.6.1 (2026-06-01): LobsterAI 2026.6.1**
  - **更新内容**: 该版本主要集成了两个关键特性：
    - **Expert Kit Store 与对话集成**: 实现了专家工具包商店与对话功能的打通，意味着用户可能在对话中直接调用和购买专家工具（`#2060`）。
    - **插件更新检查**: 支持对 npm 和 clawhub 源的插件进行更新检查（`#2069`）。
    - **修复**: 针对 MCP (可能指 Model Context Protocol) 相关问题进行了修复。
  - **破坏性变更**: 发布说明中未明确提及破坏性变更，但“Expert Kit Store”的引入可能意味着新的数据模型或API端点，建议插件开发者关注相关接口变动。
  - **迁移注意事项**: 建议用户更新至该版本以获得新功能。插件开发者需检查其插件是否兼容新的更新检查机制。

#### 3. 项目进展

今日合并的 **50个 PR** 覆盖了从核心功能到用户体验的多个方面，表明项目正在为下一个开发周期进行全面的代码清理和优化。以下是一些关键进展：

- **功能增强**
    - **语音输入优化**: `#1952` 修复了 macOS 上语音输入权限被拒绝后无反馈的问题，改进了用户体验。
    - **安全监控**: `#1962` 在设置中增加了 `nsp-clawguard` 安全监控插件的开关，增强了系统的安全性配置能力。
    - **对话思考深度**: `#1985` 为聊天会话增加了思考级别控制（从关闭到自适应），为用户提供了更精细的模型响应控制。
    - **IM (即时通讯) 功能**: `#2025` 和 `#2037` 对视听通讯机器人的管理界面和相关文案进行了重构和优化。

- **稳定性与修复**
    - **核心引擎**: `#2015` 解决了 openclaw 的压缩重试和工具结果缺失问题；`#2018` 优化了 token 刷新逻辑，避免网关重启。
    - **浏览器与网络**: `#2023` 提升了浏览器和 web fetch 功能的稳定性和成功率。
    - **模型兼容性**: `#2000` 修复了 mimo 模型与 Anthropic 格式的兼容性问题；`#2035` 修复了 qwen coding plan 对 qwen 3.6 plus 的支持。
    - **UI/UX**: `#2022` 优化了 HTML 预览与源码展示体验，包括懒加载、主题适配等；`#2002` 修复了 Markdown 预览中本地图片路径不显示的问题。

- **代码清理与UI更新**: `#2028`, `#2037`, `#2008`, `#2009` 等多个 PR 专注于更新 UI 图标、优化文案以及清理代码，体现了项目对代码质量和用户体验的持续追求。

总体来说，项目在维持核心功能稳定的同时，积极扩展安全、IM、浏览器能力等周边功能，工程迭代步伐稳健。

#### 4. 社区热点

- **Issue #2081: [订阅] 积分清零投诉**
  - **热度**: 今日唯一的新 Issue，有1条评论，直接表达了用户的愤怒。
  - **链接**: [Issue #2081](https://github.com/netease-youdao/LobsterAI/issues/2081)
  - **分析**: 用户抱怨其花费积分购买的订阅服务，在月底积分被全部清零，质疑这是“搞笑的吧”。这背后反映了用户对 **积分订阅政策** 的强烈不满。核心诉求是：
    1.  **积分的有效性和使用权**: 用户认为已购买的积分应属于个人资产，不应轻易清零。
    2.  **政策透明度**: 用户可能对“积分月底清零”的规则不知情或认为不合理。
    3.  **公平性问题**: 这种扣费模式可能让用户感到被欺诈。

#### 5. Bug 与稳定性

今日未报告新的 Bug。但近期合并的大量 PR 中包含了对多个稳定性问题的修复，按严重程度排列如下：

- **模型兼容性相关问题**: `#2000` 解决了 mimo 模型的请求格式兼容问题；`#2035` 修复了特定模型的编码计划。这些问题可能导致用户无法正常使用某些模型。
- **核心逻辑问题**: `#2015` 修复了 openclaw 的压缩重试和工具结果缺失，这可能导致任务执行失败或数据丢失。
- **配置与应用崩溃**: `#2022` 修复了无效文件预览问题；`#2002` 修复了本地图片路径；`#2031` 和 `#2032` 修复了浏览器配置和自定义模型切换错误，这些都可能引发功能异常或应用闪退。
- **权限问题**: `#1952` 修复了 macOS 语音输入权限问题，属于功能可用性 Bug。

**结论**: 项目团队近期的修复工作非常密集，覆盖了多个关键领域的稳定性问题，项目稳定性正在快速提升。

#### 6. 功能请求与路线图信号

- **社区呼声**: Issue #2081 中用户对“积分不清零”的诉求，是一个强烈的功能请求信号。这表明用户期望更灵活的积分消费策略或更透明的续费提醒机制。
- **潜在路线图**: 合并的 PR 暗示了未来的方向：
    - **Expert Kit Store**: `#2060` 的合并标志着商业化生态的初步建立，未来可能会有更多专家工具和付费模型上线。
    - **插件生态完善**: `#2069` 的插件更新检查功能，表明项目在构建健壮的插件生态系统，未来可能开放更多插件API。
    - **IM 功能深化**: `#2025` 对IM Bot管理界面的重构，可能预示着 IM 功能会成为下一个重要增长点。

#### 7. 用户反馈摘要

今日唯一的用户反馈来自 **Issue #2081**。用户 `zjk648491625` 对LobsterAI 的积分订阅政策表达了 **强烈不满和失望**。其核心痛点是：**“已订阅并使用的积分在月底被无故清零”**。用户认为这是不合理、有欺骗性的行为。该反馈直接关联到 **商业策略和用户信任** 问题，是项目团队需要高度重视并给出正式回应的关键反馈。

#### 8. 待处理积压

今日无明显的长期未响应旧 Issue 或 PR。项目维护者对近期（上个月）的 Issue 和 PR 有及时的合并或关闭，维护效率较高。但需关注今日新开的 Issue #2081，它需要尽快被维护者回应，以避免负面情绪的发酵。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 | 2026-06-02

---

## 1. 今日速览

- 过去24小时项目无新Issue产生，活跃度集中在PR处理上。
- 3个历史PR全部被合并/关闭，其中包含一个重大功能“NEAR AI Cloud 提供商”的合并，以及两项代码质量改进（OpenAI能力显式策略、Codex参数处理）。
- 无新版本发布，项目处于功能迭代与重构的稳健推进期。
- 整体活跃度中等偏低，但合并的PR均具有实质性价值，项目健康度良好。

---

## 2. 版本发布

**无**（过去24小时无新Release）

---

## 3. 项目进展

今日合并/关闭了3个重要PR，推动了以下方面的改进：

### #1090 `refactor(providers): use explicit OpenAI capabilities` ✅ 已合并
- **作者**: penso
- **内容**: 将基于URL/名称的OpenAI兼容提供商行为检查重构为显式能力策略。为内置提供商和已解析模型的能力注册提供了统一机制，同时使自定义提供商严格遵循默认值。增加了回归测试，确保已知提供商URL和模型名称的行为正确。
- **影响**: 提升提供商配置的可维护性和可预测性，降低因隐式判断导致的行为错误风险。

### #1031 `Add NEAR AI Cloud provider` ✅ 已合并
- **作者**: PierreLeGuen
- **内容**: 新增NEAR AI Cloud作为OpenAI兼容提供商，使用`NEARAI_API_KEY`和端点`https://cloud-api.near.ai/v1`。自动发现该平台的模型（通过`/v1/model/list`），并暴露TEE（可信执行环境）感知的推荐和能力。同时更新了提供商设置、用户引导、文档及许可证列表。
- **影响**: 显著扩展了Moltis支持的云提供商生态，为NEAR生态用户提供原生集成。

### #1088 `[codex] Handle OpenAI Codex final tool-call arguments` ✅ 已合并
- **作者**: s-salamatov
- **内容**: 记录OpenAI Codex提供商中`response.function_call_arguments.done`的负载；当没有发出参数增量时，从最终参数合成一个流式参数增量；保持空累积参数字符串流经诊断解码，避免缺失参数错误。
- **影响**: 修复了Codex模型在处理工具调用时的边缘情况，提升了与OpenAI Codex API的兼容性。

**整体进度评估**: 项目在本周期内完成了一项重要功能扩展（NEAR AI Cloud）和两项框架级重构/修复，代码库质量和兼容性均有提升。

---

## 4. 社区热点

由于过去24小时无新Issue产生，且三个PR均无评论（评论字段为`undefined`），未出现高讨论量的热点。但从PR摘要可以看出：

- **#1031 (NEAR AI Cloud)** 是社区期待的新提供商集成，涉及文档和许可证更新，可能吸引NEAR生态贡献者关注。
- **#1090 (显式能力)** 代表项目在解决OpenAI兼容提供商行为不一致方面的系统性改进，可能获得长期关注。

---

## 5. Bug 与稳定性

本次数据中未发现过去24小时新报告的Bug。然而，从合并的PR中可识别以下潜在修复：

| 问题描述 | 严重程度 | 关联PR | 状态 |
|----------|----------|--------|------|
| OpenAI Codex 模型在工具调用参数末收到`function_call_arguments.done`时处理失败 | 中等 | #1088 | ✅ 已修复并合并 |
| OpenAI兼容提供商可能因URL/名称隐式判断导致行为错误 | 中低 | #1090 | ✅ 已通过显式能力策略修复 |

无崩溃或回归类问题报告。

---

## 6. 功能请求与路线图信号

- **NEAR AI Cloud 集成**: 已经合并（#1031），将成为下一个版本的组成部分。这是一个明确的路线图信号：项目正在扩大对去中心化AI平台的支持。
- **Explicit capability policies**: #1090 的合并意味着未来新添加的OpenAI兼容提供商将采用更严格的验证流程，自定义提供商的行为将更可预测，这反映了项目对稳定性的重视。
- **OpenAI Codex 改进**: #1088 显示项目持续关注与OpenAI最新API的兼容性，尤其是Codex系列模型（如o1、o3可能后续跟进）。

> **预测**: 基于过去数周的PR节奏，下一个版本发布可能包含上述三个功能，并可能伴随对其他云提供商（如OpenRouter、Groq等）的类似能力策略更新。

---

## 7. 用户反馈摘要

过去24小时无新Issue评论，因此无法提炼用户痛点。但从PR摘要和历史数据判断：

- 用户可能对NEAR AI Cloud集成感到满意，因为它允许开发者在NEAR生态中直接使用Moltis。
- 此前关于OpenAI兼容提供商行为不一致的反馈（如某些模型无法正确识别能力）在#1090中得到了系统性解决。
- 未发现明显的不满意度表达。

---

## 8. 待处理积压

过去24小时无未响应的新Issue或PR。历史积压列表需结合更长时间窗口数据，本次数据不足以判断长期未响应项。建议维护者定期检查以下类型的PR：

- 长期停留的“待合并”PR（当前数据为0）
- 超过2周未回复的Issue（当前数据无）

---

*本报告基于Moltis GitHub仓库截至2026-06-02凌晨的数据生成，数据快照时间为2026-06-01 23:59 UTC。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，以下是根据 CoPaw 项目 2026-06-02 的 GitHub 动态数据生成的日报。

---

# CoPaw 项目日报 | 2026-06-02

---

## 1. 今日速览

过去 24 小时内 CoPaw 项目保持高度活跃：共处理 50 条 Issue、34 条 PR，并发布 2 个新版本（v1.1.10 正式版与 v1.1.10-beta.2）。社区讨论集中在定时任务中断、配置持久化及 MCP 进程管理等稳定性问题上，同时后端迁移至 AgentScope 2.0 的大版本升级已进入实质推进阶段。总体项目健康度良好，关键 Bug 修复与功能增强并行。

**活跃度评估**：🟢 高（日均 50+ Issue / 34 PR / 2 发布）

---

## 2. 版本发布

### v1.1.10（正式版）
- **Agent System**：新增 `spawn_subagent` 工具，支持在工作空间中临时启动子 Agent 执行任务。
- **Coding Mode**：新增 "Open Directory" 标签页，可引用本地目录。
- 更多细节见 [Release v1.1.10](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.10)

### v1.1.10-beta.2
- 修复网站头部样式、自动继续视频播放问题。
- 修复技能标签保留、启用/禁用问题。

**破坏性变更与迁移注意事项**：
- 本版本无 Breaking Change，但请注意 v1.1.10-beta.2 为测试版，部分修复已在正式版中合并。
- 即将到来的 **AgentScope 2.0 迁移**（[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)）将带来架构变更，建议用户关注后续 RC 版本公告。

---

## 3. 项目进展

过去 24 小时共合并/关闭 **9 条 PR**，其中重要合并如下：

| PR | 摘要 | 类型 |
|----|------|------|
| [#4867](https://github.com/agentscope-ai/QwenPaw/pull/4867) | 发布 v1.1.10，更新发行说明 | 发布 |
| [#4849](https://github.com/agentscope-ai/QwenPaw/pull/4849) | 引入 `SharedMCPPool` 复用 MCP 服务器，解决 300+ Agent 时进程爆炸（修复 [#4842](https://github.com/agentscope-ai/QwenPaw/issues/4842)） | 性能优化 |
| [#4849 相关](https://github.com/agentscope-ai/QwenPaw/pull/4849) | 同上 | 已合并 |

此外，以下 PR 正处于 **“Under Review”** 或 **“OPEN”** 状态，但已完成关键功能：
- [#4853](https://github.com/agentscope-ai/QwenPaw/pull/4853) Windows 浏览器进程彻底清理（含子进程与锁文件）—— 修复 [#4844](https://github.com/agentscope-ai/QwenPaw/issues/4844)
- [#4884](https://github.com/agentscope-ai/QwenPaw/pull/4884) 修复 custom channel 保存时停止监听（修复 [#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877)）
- [#4822](https://github.com/agentscope-ai/QwenPaw/pull/4822) 修复 cron agent 的 `share_session=true` 时执行轨迹为空（修复 [#4818](https://github.com/agentscope-ai/QwenPaw/issues/4818)）

**项目里程碑**：后端单元测试覆盖（[#4340](https://github.com/agentscope-ai/QwenPaw/issues/4340)）第三阶段已完成，新增 153 个测试用例（[PR #4852](https://github.com/agentscope-ai/QwenPaw/pull/4852)）。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|------|----------|--------|----------|
| 1 | [#4653](https://github.com/agentscope-ai/QwenPaw/issues/4653) [已关闭] | 9 | 定时任务与用户消息共享 session 导致任务中断 |
| 2 | [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) [开放] | 6 | 新建会话后 Models 配置页面丢失且无法加载 |
| 3 | [#4649](https://github.com/agentscope-ai/QwenPaw/issues/4649) [已关闭] | 6 | `jobs.json` 更新后残留“幽灵” cron 任务无限执行 |
| 4 | [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) [开放] | 5 | 迁移后端至 AgentScope 2.0（Breaking Change） |

**分析**：
- 社区对 **定时任务/工作流稳定性** 关注度最高，多个 Issue 指向 cron 任务的 session、清理、状态展示等缺陷。
- 配置持久化问题（#4666）用户反馈强烈，若长期未修复可能影响新用户上手体验。
- [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) 的 Breaking Change 讨论热度不减，表明用户对架构升级既有期待也有疑虑。

---

## 5. Bug 与稳定性

### 严重度排序（🔥 高 / ⚠️ 中 / ℹ️ 低）

| 严重度 | Issue | 描述 | 是否有 Fix PR |
|--------|-------|------|---------------|
| 🔥 | [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 新建会话后 Models 配置页面丢失，需重启 | ❌ 无 |
| 🔥 | [#4888](https://github.com/agentscope-ai/QwenPaw/issues/4888) | Dream agent 相对路径写文件覆盖其他 workspace 的 MEMORY.md | ❌ 新报告 |
| 🔥 | [#4835](https://github.com/agentscope-ai/QwenPaw/issues/4835) | `jobs.json` 中单个无效 job 导致整个 workspace 无法启动 | ❌ 无 |
| ⚠️ | [#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834) | MCP 服务器进程累积不清理 | ✔️ [#4849](https://github.com/agentscope-ai/QwenPaw/pull/4849) 已合并 |
| ⚠️ | [#4818](https://github.com/agentscope-ai/QwenPaw/issues/4818) | Cron agent 的 `share_session=true` 时执行轨迹为空 | ✔️ [#4822](https://github.com/agentscope-ai/QwenPaw/pull/4822) 待合并 |
| ⚠️ | [#4877](https://github.com/agentscope-ai/QwenPaw/issues/4877) | custom channel 每次保存设置停止监听 | ✔️ [#4884](https://github.com/agentscope-ai/QwenPaw/pull/4884) 待合并 |
| ℹ️ | [#4864](https://github.com/agentscope-ai/QwenPaw/issues/4864) | 1.1.9 安装后发送消息无反应 | ✔️ 已关闭，推测已修复 |
| ℹ️ | [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807) | 升级后禁用内置技能又被恢复 | ❌ 无 |

**趋势**：Windows 相关进程资源泄漏（MCP、浏览器）在本日已获有效修复，但配置持久化和文件路径安全仍需关注。

---

## 6. 功能请求与路线图信号

### 已获 PR 跟进的功能

| 请求 Issue | 功能描述 | 对应 PR / 状态 |
|------------|----------|----------------|
| [#4211](https://github.com/agentscope-ai/QwenPaw/issues/4211) | 对齐 `multi_agent_collaboration` 技能与内置 Agent 交互工具 | 已关闭，优化完成 |
| [#4841](https://github.com/agentscope-ai/QwenPaw/issues/4841) | 新增 “Before You Build” Skill（暂停实现并审查） | 开放，社区贡献 |
| [#4859](https://github.com/agentscope-ai/QwenPaw/issues/4859) | 支持 Agent 级别的 Web 登录账号隔离 | 已关闭，功能已添加 |
| [#4879](https://github.com/agentscope-ai/QwenPaw/pull/4879) | 飞书 channel 支持交互式卡片内容提取 | PR 开放 |

### 可能纳入下一版本的用户诉求

| Issue | 功能 | 潜力评估 |
|-------|------|----------|
| [#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154) | Desktop 字体大小调节、文件路径可点击 | 高（持续活跃，多用户反馈） |
| [#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733) | Windows 桌面版重启后恢复上次智能体及对话 | 中 |
| [#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433) | 对话中展示 Token 用量 | 低（PR 搁置） |

**路线图信号**：迁移至 AgentScope 2.0 的 **WIP PR**（[#4846](https://github.com/agentscope-ai/QwenPaw/pull/4846)）已提交，预计将在未来 1-2 周内进入 Review，这将是 CoPaw 自发布以来最大的架构变化。

---

## 7. 用户反馈摘要

从历史 Issue 评论中提取的真实用户声音：

- **“每次升级都要手动禁用一次不用的内置技能，很烦”** —— [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807) 用户 @daigoopautoy
- **“新建对话时输入框没有光标，得用鼠标点一下，交互体验不好”** —— [#4714](https://github.com/agentscope-ai/QwenPaw/issues/4714) 用户 @rescodexa
- **“Tauri 桌面版使用 return-file 技能后无法下载文件，而 exe 版可以”** —— [#4874](https://github.com/agentscope-ai/QwenPaw/issues/4874) 用户 @H-TWINKLE
- **“在代码模式下切换对话会触发全局刷新，跳回原对话”** —— [#4819](https://github.com/agentscope-ai/QwenPaw/issues/4819) 用户 @Cederys
- **“每次重启后显示的智能体不是上次关闭时的那个”** —— [#4733](https://github.com/agentscope-ai/QwenPaw/issues/4733) 用户 @rescodexa

**小结**：用户对 **配置持久化、交互一致性、桌面端体验** 有较高期望，同时社区对 **新技能（Before You Build）** 和 **Agent 级权限** 等高级功能表现出主动贡献意愿。

---

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者响应或合并，建议优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 未响应天数 | 风险 |
|------|------|------|----------|------------|------|
| Issue | [#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154) | 字体大小可调节、后台服务模式、文件路径可点击 | 2026-05-09 | 24 天 | 中等（用户反复提及） |
| Issue | [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | 新建会话后 Models 配置页面丢失 | 2026-05-25 | 8 天 | 高（无 PR，影响配置） |
| Issue | [#4731](https://github.com/agentscope-ai/QwenPaw/issues/4731) | Windows 11 Edge 浏览器启动失败退出码21 | 2026-05-27 | 6 天 | 高（影响 browser_use 功能） |
| PR | [#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433) | 对话中展示 Token 用量（Under Review） | 2026-05-15 | 18 天 | 低（功能完善性） |
| PR | [#4772](https://github.com/agentscope-ai/QwenPaw/pull/4772) | Windows 启动优化（first-time contributor） | 2026-05-28 | 5 天 | 中（潜在性能提升） |

**建议**：优先安排 `#4666` 与 `#4731` 的 Bug 修复，并对长期搁置的 PR `#4433`、`#4772` 给予反馈或合并决策，以维持社区贡献热度。

---

*本日报由 AI 自动

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

好的，这是根据您提供的 ZeptoClaw GitHub 数据生成的 2026 年 6 月 2 日项目动态日报。

---

### ZeptoClaw 项目动态日报 | 2026-06-02

---

#### 1. 今日速览

过去24小时，ZeptoClaw 项目活动主要由自动化依赖更新流程驱动，合并了17个拉取请求，显示其维护生态健康。核心进展在于社区贡献者修复了一个可能导致生产环境100%错误率的重要 Bug（#592 / #610），并将其成功合入主分支。同时，维护者正通过提升CI门禁（PR #611）和发起精度审查（Issue #612），试图将项目二进制文件大小严格控制在7MB以内，这表明项目在功能迭代进入相对稳定期后，开始将重心转向性能优化和代码质量加固。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

- **关键Bug修复合并**：社区贡献者 `Sisuthros` 提交的 [#592](qhkm/zeptoclaw PR #592) “fix(providers): keyword fallback must not claim unconfigured provider” 在今天被合并至主分支（以 [#610](qhkm/zeptoclaw PR #610) 形式）。该修复解决了当模型名称通过关键字匹配时，可能错误地解析到用户未配置的提供者，从而导致请求100%失败的生产环境问题。这是一项重要的稳定性提升，直接修复了NIM-served Photon模型实例上的故障场景。
- **CI流程重大升级**：**[#611 (OPEN)](qhkm/zeptoclaw PR #611)** “chore(ci): promote binary-size to PR gate at 7.5MB” 提出了将现有的二进制文件大小监控任务提升为所有PR的准入检查（Gate）。此改动将门槛设定在7.5MB，旨在防止任何PR引入体积膨胀。
- **依赖生态全面更新**：项目在过去一天合并了15个由 `dependabot` 发起的依赖升级PR，覆盖Rust核心库（`clap`, `uuid`, `tower-http`, `mail-parser`, `bcrypt`）、GitHub Actions（`taiki-e/install-action`, `cargo-deny-action`）、Docker基础镜像（`rust`, `debian`）以及前端文档依赖（`astro`, `starlight`）。特别是跟随 **[#594](qhkm/zeptoclaw PR #594)** 解决了RUSTSEC安全公告问题，确保了整个CI流程的绿标状态。
- **内部优化**：项目清理并关闭了一批已处理或过时的PR，使项目积压维持在较低水平。

#### 4. 社区热点

**[#611 (OPEN)](qhkm/zeptoclaw PR #611)** 是今日唯一的开放PR，讨论热度最高。它由核心维护者 `qhkm` 发起，直接挑战项目的“物理极限”。

**核心诉求**：将二进制文件大小作为硬性准入标准。Issue #612 进一步揭示了该诉求背后的动机——当前大小（6.98MB）已非常接近7MB的长期战略目标，但有一次无意中漂移了近800KB。社区和项目团队核心关注点正从“功能是否实现”转向“核心构件是否精良”。这反映了项目在走向成熟阶段时，对资源占用和部署成本的严格把控。

#### 5. Bug 与稳定性

- **严重 Bug（已修复）**：
    - **`fix(providers): keyword fallback` (#592 / #610)**：这是一个在特定生产环境下（如NIM实例）导致100%错误率的逻辑错误。在关键字解析模型时，函数未检查`available_providers`，导致返回未配置的提供者。这是今日报告的最严重的 Bug，并且已经在当日完成了修复和合并。
- **预防性措施（进行中）**：
    - **二进制文件大小膨胀审计**：**Issue #612** 指出项目存在约800KB的无意体积漂移。虽然尚未形成具体的 Bug，但维护者已经识别到这是一个严重的质量风险，并计划收紧CI门禁来防止后续膨胀。

#### 6. 功能请求与路线图信号

今日未收到明确的新功能请求。所有活跃的议题（Issue #612, PR #611）均围绕 **性能与代码质量**，而非新功能。信号显示，项目路线图下一阶段的重中之重是 **二进制文件尺寸控制**。

- **可能纳入下一版本的变更**：将二进制大小CI门禁落地，并将7.5MB设为短期上限，7MB作为长期目标。这是对GitHub Actions工作流的配置变更，不涉及核心逻辑，因此最快会在下一个或多个迭代中被采纳。

#### 7. 用户反馈摘要

由于今日的 Issues 和 PR 讨论中无用户评论，因此无法提炼直接的用户反馈。从 Issue #612 的上下文中可以间接推断出，运行在资源受限环境（如边缘设备或对启动时间敏感的云函数）中的用户对二进制文件大小极其敏感。另外，贡献者 `Sisuthros` 通过提交修复 PR（#592），体现了社区用户在实际生产部署中遇到的问题（NIM 实例故障）及其对项目稳定性的高要求。

#### 8. 待处理积压

目前项目状态健康，积压较少。

- **[#611 (OPEN)](qhkm/zeptoclaw PR #611)**: 作为今日唯一开放的 PR，其评论数为 `undefined`，可能存在需要维护者或社区进行更多讨论才能决定是否合并，它应成为维护者的首要关注项。此PR的合并将直接改变项目贡献流程。

**主要关注点**：无长期（超过一周）未响应的标记为 `P1-critical` 或 `P2-high` 的 Issue，项目维护响应度高。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-06-02

---

## 1. 今日速览

过去24小时，ZeroClaw 社区保持高活跃度：共处理 **36 条 Issue**（新开/活跃 28，关闭 8）和 **37 个 PR**（待合并 24，合并/关闭 13）。无新版本发布。团队集中修复了一批高优先级 Bug（Gemini 400、Discord 投递失败、Kimi 温度参数冲突），同时推进了 WASI 插件接口定义、Agent 评测框架（Phase 0）和文档重设计等基础设施工作。社区讨论热度集中在 **Token 消耗优化**、**Ollama 兼容性** 和 **频道权限控制** 等方向。

---

## 2. 版本发布

本日无新版本发布。

---

## 3. 项目进展

以下为过去24小时已完成合并或关闭的重要 PR，体现了项目的稳定性和功能迭代节奏：

- **修复 Discord 投递失败通知泄露原始目标** ([#7031](https://github.com/zeroclaw-labs/zeroclaw/pull/7031))  
  避免失败日志中暴露未脱敏的 Marker 目标，提升安全合规性。

- **恢复非可见流错误的回退机制** ([#6983](https://github.com/zeroclaw-labs/zeroclaw/pull/6983))  
  当 Provider 流中断且客户端未收到任何有效内容时，自动降级为非流式重试，改善用户无响应体验。

- **忽略空白 SMTP 凭据覆写** ([#6979](https://github.com/zeroclaw-labs/zeroclaw/pull/6979), 对应 Issue [#6881](https://github.com/zeroclaw-labs/zeroclaw/issues/6881))  
  修复 Email 频道在配置空白 `smtp_username`/`smtp_password` 时无法正确回退到共享凭据的问题。

- **web_fetch 工具：尊重私有 DNS 主机白名单** ([#6974](https://github.com/zeroclaw-labs/zeroclaw/pull/6974))  
  使 `allowed_private_hosts` 配置项对通过域名访问的内部服务生效，修复安全策略绕过。

- **image_info 工具路径解析修复** ([#6972](https://github.com/zeroclaw-labs/zeroclaw/pull/6972))  
  恢复历史修复中遗漏的路径安全门控，防止路径穿越。

- **恢复日期上下文注入** ([#6931](https://github.com/zeroclaw-labs/zeroclaw/pull/6931))  
  将频道提示中的时间戳从精确时间改为“日期 + UTC 偏移”，减少缓存抖动。

- **定义精简默认频道集** ([#6904](https://github.com/zeroclaw-labs/zeroclaw/pull/6904), 对应 Issue [#6895](https://github.com/zeroclaw-labs/zeroclaw/issues/6895))  
  缩小默认构建包含的频道数量至 ACP、Webhook、Email、Telegram，控制二进制体积增长。

- **添加 Jina AI 作为 web_search 提供者** ([#6833](https://github.com/zeroclaw-labs/zeroclaw/pull/6833), 对应 Issue [#6827](https://github.com/zeroclaw-labs/zeroclaw/issues/6827))  
  集成 Jina AI 免费大额搜索 API，降低社区使用门槛。

- **修复 Kimi K2 模型温度参数冲突** ([#7049](https://github.com/zeroclaw-labs/zeroclaw/pull/7049), 对应 Issue [#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022))  
  OpenAiCompatibleModelProvider 不再为 Kimi K2.5/K2.6 强制发送 `temperature: 0.7`，避免 400 错误。

---

## 4. 社区热点

以下 Issues/PRs 在过去24小时内获得了最多评论或 reaction，反映了社区的关注焦点：

- **Token 消耗最小化 — Skill 编译机制** ([#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146), 评论 8 条)  
  用户 `jonsmirl` 提出每次查询“天气”都会完整加载 400+ 行的 `SKILL.md`，希望将 Skill 编译为紧凑表示以减少 Token 浪费。该议题已获得 **status:accepted**，且社区讨论中有多人提出预编译方案。这是 v0.8 路线图中的重要性能优化点。

- **Ollama Provider 调用工具时崩溃** ([#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962), 评论 6 条)  
  用户 `ufukbakan` 报告在配置 Ollama 后，任何工具调用都会导致会话卡死，无法恢复。该 Bug 标记为 S1（工作流阻塞），目前 **status:in-progress**，尚无合并的修复 PR。

- **Discord 频道白名单机制** ([#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378), 评论 6 条)  
  社区希望 Discord 频道支持 `allowed_channels` 配置，类似于 Matrix 的 `allowed_rooms`。该特性被标记为 **priority:p2**，已有不少用户表达需求。

- **Gemini 400 — 历史序列不满足“首个非系统轮次必须为 user”** ([#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302), 评论 4 条)  
  当 Agent 在首个 `user` 对话之前就发送了 `assistant` 的 `tool_calls`，Gemini 拒绝请求。该 Bug 标记为 **priority:p1**，目前正在修复中。

---

## 5. Bug 与稳定性

当日报告的 Bug 按严重程度排列如下：

| 严重程度 | Issue/PR | 描述 | 修复状态 |
|----------|----------|------|----------|
| **S1 - 工作流阻塞** | [#5962](https://github.com/zeroclaw-labs/zeroclaw/issues/5962) | Ollama Provider 在需要工具时彻底崩溃，会话无法继续 | 未修复，in-progress |
| **S1 - 工作流阻塞** | [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | Gemini 请求 400，因对话历史违反角色顺序 | 未修复，in-progress |
| **S1 - 工作流阻塞** | [#7022](https://github.com/zeroclaw-labs/zeroclaw/issues/7022) | Kimi K2.6 因强制发送 `temperature` 返回 400 | **已修复** (PR [#7049](https://github.com/zeroclaw-labs/zeroclaw/pull/7049)) |
| **S2 - 行为降级** | [#6472](https://github.com/zeroclaw-labs/zeroclaw/issues/6472) | Gateway 无法使用 Postgres 内存后端（Tokio 运行时嵌套 panic） | 未修复，in-progress |
| **S2 - 行为降级** | [#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) | WhatsApp Web 的 `allowed-numbers` 对 LID 联系人失效（消息静默丢失） | 未修复，in-progress |
| **S2 - 行为降级** | [#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068) | Telegram 频道收到 Codex 内部 scratchpad/工具转录而非正常回复 | 新报，未修复 |
| **S2 - 行为降级** | [#7063](https://github.com/zeroclaw-labs/zeroclaw/issues/7063) | Channel 中托管的 Agent 绕过 per-agent 工具白名单 (`apply_policy_tool_filter` 遗漏) | 新报，未修复 |
| **S2 - 行为降级** | [#7059](https://github.com/zeroclaw-labs/zeroclaw/issues/7059) | 频道编排器存在“默认模型提供商”凭据回退，与 V3 schema 冲突 | 新报，PR [#7066](https://github.com/zeroclaw-labs/zeroclaw/pull/7066) |

此外，以下 Bug 在当日被关闭（已修复）：

- [#6881](https://github.com/zeroclaw-labs/zeroclaw/issues/6881) — Email 频道空白 SMTP 凭据覆写问题（PR [#6979](https://github.com/zeroclaw-labs/zeroclaw/pull/6979)）
- [#7031](https://github.com/zeroclaw-labs/zeroclaw/pull/7031) — Discord 投递失败日志泄露

---

## 6. 功能请求与路线图信号

- **Skill 编译（Token 最小化）** ([#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146))  
  已获社区广泛支持，虽然暂无对应 PR，但被标记为 `priority:p2` 和 `status:accepted`，有望进入 v0.8.x 或 v0.9 路线图。

- **Agent 评测框架 `zeroclaw eval`** ([#7065](https://github.com/zeroclaw-labs/zeroclaw/issues/7065), PR [#7067](https://github.com/zeroclaw-labs/zeroclaw/pull/7067))  
  由 `mn13` 发起，提出 `zeroclaw eval` 命令，支持回放和实时两种模式，并内置 LLM-as-judge。Phase 0 PR 已提交（确定性回放），标志着 ZeroClaw 正式进入 Agent 质量度量领域。

- **从 `.well-known` URI 安装 Skill** ([#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853))  
  标准化 Skill 发现机制，社区有 Cloudflare、Vercel 等使用者，虽然开放已久（2026-03-27），但仍保持活跃，可能与外部标准工作组动向有关。

- **Prompt 触发缺失 Skill 安装建议** ([#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289))  
  当用户询问需要未安装 Skill 的能力时，自动提示安装。该功能与 v0.7.6 的 UX 改进主题一致，社区反馈积极。

- **Dashboard 更新按钮** ([#6365](https://github.com/zeroclaw-labs/zeroclaw/issues/6365))  
  将 CLI 的 `zeroclaw update` 流程暴露到 Web 界面，降低操作门槛。

- **节点管理 CLI `zeroclaw node add`** ([#6390](https://github.com/zeroclaw-labs/zeroclaw/issues/6390))  
  配合仪表盘节点健康追踪功能，实现多机集群注册。当前因依赖 #6346 而处于 `status:blocked`。

- **WASI 插件接口定义** ([PR #7060](https://github.com/zeroclaw-labs/zeroclaw/pull/7060))  
  `bheatwole` 提交了 Tool、Channel、Memory 三个插件接口的 WIT 文件，是 FND-001 架构文书中 §5.2 的第一步，标志着 ZeroClaw 向插件化生态转型进入实施阶段。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户痛点与场景：

- **“每个查询都要发送整个 Skill” — #5146**  
  用户 `jonsmirl` 精确描述了生产环境痛点：Weather Skill 的 markdown 文件约 400 行，每次推理都作为上下文传入，导致巨额 Token 浪费。希望类似编译器的方式只提取必要部分。

- **“Ollama 一调用工具就崩，会话彻底废了” — #5962**  
  用户 `ufukbakan` 反馈的 S1 问题至今无修复，严重影响本地部署体验。社区多次提及该问题，但可能因 Ollama 本身 API 兼容性差异导致修复复杂。

- **“Discord 机器人回复所有频道，没法限制” — #6378**  
  用户 `BaroDevelopment` 指出 Discord 缺少 `allowed_channels` 配置，而 Matrix 已有 `allowed_rooms`，希望保持一致性。该需求在群组运营场景中高频出现。

- **“Gemini 400 错误莫名其妙” — #6302**  
  用户 `dmnkhorvath` 详细分析了请求体，指出 ZeroClaw 构造的对话历史违反 Gemini 角色顺序约束。该问题在 Gemini 2.5 发布后尤为突出，属于 Provider 适配细节。

- **“WhatsApp 联系人白名单不生效，消息被静默丢弃” — #6350**  
  用户 `theonlyhennygod` 抱怨 LID 格式的联系人绕过配置检查，且日志无错误提示，运维人员难以发现。安全性问题需要优先处理。

- **“中文环境下还有硬编码英文回复” — #6548**  
  用户 `drbparadise` 指出部分频道运行时回复未使用 Fluent 本地化，即使配置了 `zh-CN`，仍出现英文字符串。社区对国际化有明确期待。

---

## 8. 待处理积压

以下 Issue 长期开放且具有重要影响，建议维护团队关注：

- **#5146 Token 最小化 - Skill 编译**  
  开放 65 天，社区高度关注，但尚未进入实现阶段。如果纳入 v0.8 路线图，建议尽快分配设计。

- **#4853 .well-known URI 技能安装**  
  开放 67 天，依赖外部标准制定进度。可考虑与 Agentskills 工作组同步，避免重复劳动。

- **#5155 委托代理忽略 prompt_injection_mode**  
  开放 65 天，导致委托代理总是全量注入 Skill，与全局配置冲突。标记为 S1 但长期未修复，可能因涉及核心上下文组合逻辑。

- **#6250 require_auth 中间件化**  
  开放 32 天，涉及 API 安全加固。若合并，可以简化后续所有新 handler 的鉴权逻辑。

- **#6391 实时心跳检测**  
  开放 28 天，阻塞于 Node 管理相关依赖。集群用户已报告 Dashboard 显示节点在线但实际已断开的问题。

---

> 本报告基于 GitHub 数据于 2026-06-02 生成，数据覆盖 2026-06-01 00:00 UTC 至 2026-06-02 00:00 UTC。所有链接均为 `github.com/zeroclaw-labs/zeroclaw` 下的对应条目。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*