# OpenClaw 生态日报 2026-06-17

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-17 02:56 UTC

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

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 OpenClaw 项目于 2026-06-17 的 GitHub 数据生成的日报。

---

## OpenClaw 项目动态日报 | 2026-06-17

### 1. 今日速览

OpenClaw 项目今日保持高度活跃，过去24小时内产生了500条 Issue 和 500条 PR 更新。社区讨论焦点集中在**会话稳定性**和**消息丢失**等高优先级 Bug 上，其中多项 P1 级问题的长期存在值得关注。虽然新版本 `v2026.6.8` 已发布，但代码合并（93条）与待处理 PR（407条）的比率显示项目吞吐能力有待加强。总体而言，项目社区活跃度极高，但面临严峻的 Bug 积压和稳定性挑战。

### 2. 版本发布

- **新版本: `v2026.6.8`**
  - **链接**: [OpenClaw v2026.6.8 Release](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8)
  - **主要更新内容**:
    - **Telegram 消息渲染增强**: 支持结构化文本，包括表格、列表、可展开的引用块、保留的换行符以及 CLI 支持的回复功能。 (#92679, #931)
    - **WhatsApp 渠道修复**: 修复了 WhatsApp 渠道，使其能够正确解析和执行用户配置的 ACP（高级控制协议）绑定。
  - **分析与建议**: 此次发布重点改进了两个主流渠道的用户体验和可靠性。Telegram 的功能增强尤为实用，提升了消息的可读性。建议用户在更新时注意检查原有 Telegram 和 WhatsApp 配置是否适配新的渲染和行为逻辑。

### 3. 项目进展

过去24小时内，共有来自 93 个 Pull Request 的修改被合并或关闭，主要集中在关键 Bug 修复和功能增强上，体现了项目在解决具体问题上的努力。

- **安全与配置**: [#93877](https://github.com/openclaw/openclaw/pull/93877) 修复了 exec 秘密提供者未将基础设施环境变量传递给子进程的问题，增强了配置的完整性。 [#93840](https://github.com/openclaw/openclaw/pull/93840) 修复了 `web_fetch` 在使用代理时忽略 `NO_PROXY` 环境变量的 Bug，增强了网络访问的灵活性。
- **渠道与消息**: [#93848](https://github.com/openclaw/openclaw/pull/93848) 修复了 Telegram 等渠道传入图片无法被模型识别为视觉内容的问题，解决了三个相关的 Issue。 [#93821](https://github.com/openclaw/openclaw/pull/93821) 修复了 Qdrant 内存核心插件因守护进程启动日志导致 JSON 解析失败的问题，确保了长期会话记忆功能的稳定性。
- **平台兼容性**: [#93876](https://github.com/openclaw/openclaw/pull/93876) 修复了 Docker 25+ 环境中，由技能挂载路径冲突导致的容器创建失败问题。

**总结**: 项目在修复用户报告的、影响广泛的功能性 Bug（如媒体处理、代理配置）方面取得了扎实进展，提升了核心功能的稳定性和健壮性。

### 4. 社区热点

今日讨论最热烈、评论最多的议题主要集中在以下方面：

1.  **跨平台支持呼声高**: [#75](https://github.com/openclaw/openclaw/issues/75) 《Linux/Windows Clawdbot Apps》拥有 **109 条评论**和 **79 个点赞**，是当前社区最受关注的议题。用户强烈期望 OpenClaw 能扩展其原生客户端至 Linux 和 Windows 平台，与现有的 macOS、iOS、Android 客户端形成完整生态。这表明社区用户对原生桌面端体验有刚性需求。
2.  **核心架构迁移讨论**: [#88838](https://github.com/openclaw/openclaw/issues/88838) 《Track core session/transcript SQLite migration via accessor seam》在 17 天内获得 **30 条评论**，是维护者和核心贡献者讨论的焦点。议题讨论如何通过“分支-抽象”模式，分步进行高风险的核心与会话/记录迁移。这体现了项目团队在追求技术演进与维持稳定性间的权衡，属于保证项目长期健康度的关键讨论。
3.  **子代理任务稳定性的普遍关注**: [#44925](https://github.com/openclaw/openclaw/issues/44925) 《[Bug]: Subagent completion silently lost》拥有 **19 条评论**，其描述的“任务静默丢失”问题引发了许多用户的共鸣。用户在 3 月提出此问题，目前仍未修复，是项目稳定性的主要痛点之一。

### 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题中，**“会话状态丢失”** 和 **“消息丢失”** 是出现频次最高的关键词，多个 P0/P1 级问题亟待解决。

| 严重等级 | 问题描述 | 链接 | Fix PR 情况 |
| :--- | :--- | :--- | :--- |
| **P0** | 核心会话/记录SQLite迁移追踪 | [#88838](https://github.com/openclaw/openclaw/issues/88838) | 讨论中 |
| **P1** | **子代理完成静默丢失**（无重试、无通知、无自动重启） | [#44925](https://github.com/openclaw/openclaw/issues/44925) | 无 |
| **P1** | **SIGUSR1重启时信号守护进程竞态条件**，导致孤儿进程和发送失败 | [#22676](https://github.com/openclaw/openclaw/issues/22676) | 无 |
| **P1** | **编码代理无法完成任何任务**（2026.4.2 及之前版本正常工作的回归问题） | [#62505](https://github.com/openclaw/openclaw/issues/62505) | 无 |
| **P1** | **Steer模式无法在回合中注入消息** | [#48003](https://github.com/openclaw/openclaw/issues/48003) | 无 |
| **P1** | **安全防护压缩忽略自定义模型配置** | [#57901](https://github.com/openclaw/openclaw/issues/57901) | 无 |
| **P2** | 代理承诺后续跟进但未启动任何实际行动 | [#58450](https://github.com/openclaw/openclaw/issues/58450) | 无 |
| **P2** | 图像工具在缺少sharp库时报错不明确 | [#73148](https://github.com/openclaw/openclaw/issues/73148) | 无 |

### 6. 功能请求与路线图信号

今日收到的功能请求显示出社区对**精细化权限控制**、**多代理差异化配置** 和 **上下文感知** 的强烈需求。

- **已有可能被纳入下版本的信号**:
  - **私有网络访问**: [#39604](https://github.com/openclaw/openclaw/issues/39604) 要求为 `web_fetch` 工具增加 `allowPrivateNetwork` 配置，以可选地允许访问内网地址。该请求与安全相关，属于常见的企业和高级用户诉求。
  - **渠道中介MCP工具审批**: [#78308](https://github.com/openclaw/openclaw/issues/78308) 提出，希望 MCP 工具调用也能像 shell 执行一样，通过渠道审批机制进行二次确认。这直接回应了安全风险，很可能被优先考虑。
  - **按代理配置内存/知识库**: [#63829](https://github.com/openclaw/openclaw/issues/63829) 要求在 multi-agent 场景下，每个 Agent 能拥有独立的“记忆维基”知识库。这表明项目正往更复杂、更专业的分工应用场景演进。
  - **持久化任务状态面板**: [#52640](https://github.com/openclaw/openclaw/issues/52640) 提议为长时间运行的任务增加一个可见的状态面板，改善用户对异步任务进度的感知。

### 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出用户的核心反馈：

- **对子代理稳定性的极度不满**: 用户对 `Subagent completion silently lost` (#44925) 表达了严重关切，任务静默失败且缺乏反馈，使得依赖于子代理协同工作的复杂场景（如并行编码）不可用。
- **回归问题影响信任**: 多个 `regression` 标签的 Issue (如 #62505, #45765) 表明新版本引入了之前正常工作的功能退化，这降低了用户对“升级即改进”的信任感。尤其是编码 Agent 完全无法工作 (#62505)，直接影响核心生产力。
- **对配置文档和错误信息的期待**: 用户对模糊不清的报错（如 `Failed to optimize image` #73148）和复杂的配置选项（如 Telegram 代理设置）表现出困惑，期望提供更清晰、可操作的帮助信息和指导。
- **中国区用户的特定反馈**: 多项涉及飞书、百度等中国服务集成的问题（如 #37626, #53486），以及关于API Key明文存储的安全担忧 (#64046)，反映了中国用户群体的积极参与及其特定场景下的需求。

### 8. 待处理积压

以下清单列出了当前社区高度关注、但迟迟未得到维护者响应的关键议题，建议项目维护团队重点关注：

- **Issue #75 - [OPEN] [2026-01-01] Linux/Windows 客户端**: 拥有 109 条评论和 79 个点赞，是社区第一诉求。虽已添加 `help wanted` 标签，但维护者未发布明确计划。
- **Issue #44925 - [OPEN] [2026-03-13] 子代理完成静默丢失**: P1 级稳定性 Bug，至今无任何官方回应或修复 PR，风险极高。
- **Issue #22676 - [OPEN] [2026-02-21] SIGUSR1 重启导致进程泄漏**: P1 级稳定性 Bug，存在近 4 个月，严重影响 Gateway 的可靠运行。
- **Issue #54531 - [OPEN] [2026-03-25] 强制回复原始渠道**: 用户痛点明确，影响 Telegram/Discord 等主流渠道的使用体验，长期处于 `P1` 但无进展。
- **Pull Request #50520 - [OPEN] [2026-03-19] 剥离出站消息中的内部元数据**: 修复一个重要的信息安全问题，但超过 3 个月未合并，可能触及复杂的架构决策。

---

## 横向生态对比

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的各项目动态数据（2026-06-17）生成的横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向分析报告

**报告日期**: 2026-06-17
**分析范围**: OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw, NullClaw, IronClaw, LobsterAI, TinyClaw, Moltis, CoPaw, ZeptoClaw, ZeroClaw

#### 1. 生态全景

当前个人AI助手/自主智能体开源生态呈现出 **“高位活跃下的分化与成熟化”** 特征。一方面，以 OpenClaw 为代表的头部项目社区规模极其庞大（日处理500+ Issue/PR），但面临严重的稳定性挑战和 Bug 积压；另一方面，以 NanoBot、CoPaw 为代表的项目正通过精细化迭代（如上下文压缩、流式处理优化）向产品级稳定性冲刺。市场对 **企业级多租户部署**、**会话与任务可靠性的绝对保障**、以及 **跨平台与渠道的深度集成** 发出了最强烈的需求信号。值得注意的是，多个项目不约而同地将 **安全加固** 和 **高性能/低成本推理** 作为下一阶段的核心关注点。

#### 2. 各项目活跃度对比

| 项目名称 | 新/活跃 Issues | 新/活跃 PRs | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~500 | ~500 | ✅ `v2026.6.8` | **警惕** (极高热度，但高优先级Bug积压严重) |
| **NanoBot** | 详见表2附* | 24 | 无 | **良好** (高效修复，社区贡献积极) |
| **Hermes Agent** | 50 | 50 | 无 | **高活跃** (企业级功能密集开发，Bug并行) |
| **PicoClaw** | ~11 (安全相关) | 12 (合并) | ✅ `v0.3.0-nightly` | **健康** (发布能力强，安全审计是机会) |
| **NanoClaw** | 5 | 5 | 无 | **稳定** (关键Bug修复，社区理性健康) |
| **NullClaw** | 2 | 3 | 无 | **中等** (修复与功能开发推进，需加速审查) |
| **IronClaw** | 50 | 50 | 无 | **高活跃** (Engine V2架构升级期，社区参与度高) |
| **LobsterAI** | ~1 | 3 (合并) | 无 | **稳定** (功能优化为主，社区关注点集中) |
| **TinyClaw** | 0 | 1 | 无 | **静默** (活跃度极低，Windows支持受阻) |
| **Moltis** | 4 | 2 | 无 | **健康** (讨论质量高，聚焦配置与扩展性) |
| **CoPaw** | 44 | 38 | ✅ `v1.1.12-beta.1` | **高活跃** (高强度迭代，稳定性与社区并重) |
| **ZeptoClaw** | 0 | 1 (Dependabot) | 无 | **休眠** (依赖自动更新，无实质性进展) |
| **ZeroClaw** | 50 | 50 | 无 | **高活跃** (关键修复多，文档是核心短板) |

*注：NanoBot 详细Issue/PR数据未在摘要中完全列出，但从其合并14个PR的规模来看，健康度良好。*

#### 3. OpenClaw 在生态中的定位

- **无可争议的第一梯队与参照系**: OpenClaw 凭借极端庞大的社区数量（日500+条互动）定义了“热门”的边界，是生态中最核心的参照项目。
- **优势与社区规模**: 版本发布频繁 (`v2026.6.8`)，功能迭代覆盖面广，尤其在Telegram、WhatsApp等渠道的渲染增强上走在前列。用户对跨平台原生客户端 (Linux/Windows) 的呼声极高，也侧面反映了其用户基础的广泛。
- **技术路线差异**: 与追求极致稳定性和精细化架构的PicoClaw、NanoBot相比，OpenClaw更侧重于功能的广度与快速实验，但其代价是核心稳定性（如子代理任务静默丢失、会话状态丢失）问题积压严重，引发了社区“升级即破坏”的信任危机。
- **社区对比**: 其社区规模远超所有其他项目，但社区情绪更为复杂：既有大量功能请求的兴奋，也夹杂着对关键Bug长时间未解决的不满。相比之下，PicoClaw的社区虽小，但贡献者（如安全研究员）更为硬核；NanoBot社区则表现为高效、理性的协作氛围。

#### 4. 共同关注的技术方向

1.  **部署与环境的稳定性与扩展性**:
    - **多租户/多实例**: **Hermes Agent** (`#34352` 多租户隔离), **IronClaw** (`#4853` 多租户活动记录消失)。
    - **跨平台兼容**: OpenClaw (`#75` Linux/Windows客户端), **TinyClaw** (`#281` Windows CLI修复), **PicoClaw** (`#3137` 远程管理命令)。
    - **容器化与编排**: **PicoClaw** (发布nightly Docker), **NanoClaw** (`#2784` 容器运行器), **CoPaw** (macOS Tauri CI修复)。

2.  **会话、任务与上下文管理的可靠性**:
    - **任务静默丢失/假成功**: **OpenClaw** (`#44925` 子代理静默丢失), **LobsterAI** (`#1424` 定时任务假成功), **ZeroClaw** (`#7820` shell审批循环)。
    - **状态与上下文管理**: **CoPaw** (`#5218` 上下文压缩冻结), **NanoBot** (`#4352` 截断逻辑优化), **IronClaw** (`#5003` SSO线程丢失)。
    - **会话隔离与持久化**: **CoPaw** (`#5225` 临时文件管理), **ZeroClaw** (`#7799` 恢复会话后空白)。

3.  **安全、合规与权限控制**:
    - **集中安全审计**: **PicoClaw** (11项批量安全报告, #3070-#3082)。
    - **计费与合规**: **Hermes Agent** (`#40014` Claude OAuth 计费问题), **NanoClaw** (`#1669`平台合规性)。
    - **精细化权限**: **ZeroClaw** (`#7747` MCP服务器按代理隔离), **PicoClaw** (`#3137` 远程渠道授权)。

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 功能广度、多渠道生态 | 成熟开发者、极客、寻求一站式方案的团队 | 插件化渠道、注重社区驱动的快速开发 |
| **PicoClaw** | 极致稳定性、安全性、硬核技术 | 安全敏感用户、嵌入式/边缘设备开发者 | Rust实现，强类型、线程安全、安全审计深度集成 |
| **NanoBot** | 精细化用户体验、性能优化 | 注重生产力与交互流畅度的个人开发者 | 强调“梦”机制与自动上下文压缩，精细化参数调优 |
| **Hermes Agent** | 多云多租户、渠道深度集成 | 企业级用户、B2B服务提供方 | 平台适配器优先 (企业微信, QQ), 重视多租户与计费模型 |
| **IronClaw** | 架构升级 (Engine V2)、自动化、基准测试 | 研发团队、对LLM评估和自动化有深度需求的组织 | 强大的自动化框架 (Automations)、基准测试 (Benchmark) 是其特色 |
| **CoPaw** | 协同 (Cowork)、多语言、AI原生IDE | 独立开发者、小团队、追求极致性能与AI原生体验的用户 | 对长对话和上下文压缩有深入算法优化，桌面端体验好 |
| **ZeroClaw** | 运行时隔离、MCP集成、工作流自动化 | 高级开发人员、平台架构师、需要稳定基座的团队 | 强调MCP与服务隔离，有Rust和“硬件”相关的技术路线表 |
| **NullClaw, NanoClaw, Moltis等** | 特定领域或轻量级场景 | 个人用户、特定兴趣小组 | 功能相对聚焦，典型如Moltis侧重于语音交互和TTS |

#### 6. 社区热度与成熟度

- **快速迭代与功能拓展期**:
    - **OpenClaw**: 极速迭代，社区规模庞大，但高质量反馈与Bug堆积并存。
    - **Hermes Agent**: 企业级功能并行开发，社区参与度高，但Bug频发。
    - **CoPaw**: 高强度迭代，社区贡献积极，正快速向产品级靠拢。
    - **ZeroClaw**: 同样高强度，修复速度快，功能（如MCP隔离）有深度。

- **质量巩固与性能调优期**:
    - **NanoBot**: 社区理性，PR速度快，重在精细化修复(流式超时、空响应)和性能优化(上下文管理)。
    - **PicoClaw**: 代码合并效率高，发布能力强。面临专业安全审计，是走向成熟的必经之路。
    - **IronClaw**: 处在架构升级期 (Engine V2)，热点集中在核心架构与自动化上，社区反馈深度高。

- **稳定或低速发展期**:
    - **NanoClaw, NullClaw, Moltis**: 功能方向清晰，社区稳定，响应速度适中或偏慢，尚未进入爆发期。
    - **LobsterAI**: 社区关注点集中，开发节奏平稳，重在打磨现有功能。
    - **TinyClaw, ZeptoClaw**: 活跃度极低，进入维护或休眠状态，对开发者吸引力有限。

#### 7. 值得关注的趋势信号

1.  **“‘零容忍’可靠性与可恢复性”成为核心生存法则**: 从OpenClaw的“子代理静默丢失”到LobsterAI的“定时任务假成功”，再到ZeroClaw的“shell审批循环”，**“静默失败”是当前社区最恐惧的Bug**。这对AI智能体开发者而言，意味着必须将**完备的错误处理、状态持久化和恢复机制、以及用户可理解的行为反馈**作为核心能力来构建。

2.  **安全已从“可选项”变为“入场券”**: PicoClaw的11项批量安全报告，以及多项目对SSRF、命令注入、OAuth计费合规的讨论，预示着安全不再是高并发场景下的奢侈品，而是所有智能体项目走向企业级部署的 **最低门槛**。开发者应尽早将安全审计集成到开发流程中，并支持细粒度的权限隔离。

3.  **企业级部署需求催生新的基础设施**: 多租户隔离 (Hermes Agent)、跨平台原生支持 (OpenClaw)、容器化部署 (多个项目)、以及精细API成本控制 (Hermes Agent)，这些共同指向一个趋势：**AI智能体正从个人玩具快速演变为企业基础设施的一部分，对部署、运维、治理的要求日益提高**。

4.  **“专注与克制”比“大而全”更具竞争力**: 在OpenClaw因功能膨胀而面临稳定性困境时，NanoBot、PicoClaw和Moltis分别以**性能调优、安全加固、特化场景**（如语音交互）取胜。这表明，在日益喧嚣的生态中，**明确的目标用户群和聚焦的技术路线**是构建高粘性社区、降低维护成本的有效策略。对开发者而言，选择深耕而非撒网，可能是一条更可持续的开源道路。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据您提供的 NanoBot 项目数据，生成 2026 年 6 月 17 日的项目动态日报。

---

### NanoBot 项目动态日报 | 2026-06-17

---

#### 1. 今日速览

今日项目活跃度极高。代码库经历了大规模的“清理与优化”浪潮：24 个 Pull Request (PR) 中超过半数（14 个）被合并或关闭。修复工作集中在安装器兼容性、代理配置、流式超时验证等用户体验细节上。同时，多个旨在优化系统提示词（System Prompt）大小和缓存机制的改进型 PR 被提出。这显示出项目在持续吸纳社区贡献（特别是来自 `chengyongru`、`yu-xin-c` 的系列修复）的同时，开发者正将重心转向核心性能的精细打磨。

---

#### 2. 版本发布

今日无新版本发布。

---

#### 3. 项目进展

今日有 14 个 PR 被合并或关闭，标志着多项关键修复和功能增强已完成：

-   **核心稳定性增强：**
    -   **合并** PR **[#4363]**：新增 `resolve_stream_idle_timeout_s()` 函数，统一并强化了流式超时配置的校验，解决了因无效配置导致 `ValueError` 崩溃的问题。
    -   **合并** PR **[#4358]**：修复了 API 返回空响应时重试机制会“复制”用户消息的 bug，提升了对话历史记录的准确性。
    -   **合并** PR **[#4352]**：将系统提示词中“近期历史摘要”的截断逻辑从字符数改进为 token 数，避免了 CJK 等文本因 token 估算不准而超出上下文窗口的风险。
-   **用户体验与配置优化：**
    -   **合并** PR **[#4368]** 与 **[#4365]**：修复了 macOS 上因 PEP 668 导致的安装失败问题，并优化了 curl 安装命令的写法，使其在 Dockerfile 中更兼容。
    -   **合并** PR **[#4370]**：将空闲自动压缩（auto-compact）的默认值从 `0`（禁用）改为 `15` 分钟，鼓励用户自动管理上下文，减少梦（Dream）机制的等待时间。
    -   **合并** PR **[#4369]**：当梦（Dream）机制无可处理的历史时，不再返回空响应，而是给出可读性更强的解释并引导用户配置空闲压缩。
    -   **合并** PR **[#4361]**：为 Kimi K2.7 系列模型添加了“思考”（Thinking）能力的支持。
-   **WebUI 与开发者体验：**
    -   **合并** PR **[#4364]**：修复了在局域网内通过 Vite 开发服务器访问 WebUI 时，因 host 头重写导致 WebSocket 连接卡死的 bug。
-   **构建与兼容性：**
    -   **合并** PR **[#4355]**：将 bridge 模块的 node_modules 加入 .gitignore，防止误提交。
    -   **合并** PR **[#4330]**：新增了 WebUI 自动化管理视图，允许用户过滤、搜索、运行、暂停/恢复自动化任务。

---
---

#### 4. 社区热点

-   **最活跃的 Bug 报告：`#4360` [CLOSED] “The Markitecht” 报告的安装器报错**
    -   **概述**：用户在纯净的 Debian 13 Docker 容器中运行安装器时，遇到 `pip: 20: Syntax error: end of file unexpected (expecting "}")` 错误。作者推测与之前的网络问题导致下载脚本损坏有关。
    -   **链接**：[Issue #4360](https://github.com/HKUDS/nanobot/issues/4360)
    -   **分析**：该 Issue 有 9 条评论，是今日讨论最热烈的议题。虽然已被关闭，但这暴露出项目安装脚本在处理网络不稳定或特定环境（如 Docker）时的脆弱性。用户的详细排查过程对后续优化安装流程非常有价值。

-   **最具影响力的增强提议：PR `#4350` [OPEN] 新增 Keenable 搜索提供商**
    -   **概述**：用户 `IlyaGusev` 提交 PR，希望将 `Keenable` 作为内嵌的 Web 搜索提供商。Keenable 自称是专注于研究的搜索引擎。
    -   **链接**：[PR #4350](https://github.com/HKUDS/nanobot/pull/4350)
    -   **分析**：这是社区贡献者主动引入第三方服务的典型例子。表明用户对搜索工具的多样性和专业化有持续需求。该 PR 如果被合并，将为项目增加一个专注于研究质量的搜索选项。

---

#### 5. Bug 与稳定性

| 严重程度 | Issue / PR 编号 | Bug 描述 | 状态与备注 |
| :--- | :--- | :--- | :--- |
| **高** | [#4375](https://github.com/HKUDS/nanobot/issues/4375) [OPEN] | **Git 命令在工作区子目录中被安全策略阻止。** 用户报告在工作区内的子目录执行 `git add` 等操作被安全防护机制拦截。 | **待解决。** 这是一个工作区边界和权限问题，可能影响在项目中使用 Git 进行版本控制的用户。 |
| **中** | [#4374](https://github.com/HKUDS/nanobot/issues/4374) [OPEN] | **项目工作区中，`SOUL.md` 等重启文件的读写路径不对称。** 读取从项目目录获取，但写入却写到了默认工作区，导致状态丢失。 | **待解决。** 这会破坏 WebUI 项目工作区的一致性体验。 |
| **中** | [#4366](https://github.com/HKUDS/nanobot/issues/4366) [CLOSED] | **本地模型服务器受系统代理影响无法连接。** 当机器配置了 HTTP 代理时，对 `localhost` 的 API 请求被错误地路由到代理。 | **已修复。** 对应的 PR [#4367](https://github.com/HKUDS/nanobot/pull/4367) 已提交，对代理行为进行了精细化处理：本地/局域网请求绕过代理，云端请求才使用。 |
| **低** | [#4360](https://github.com/HKUDS/nanobot/issues/4360) [CLOSED] | **安装器在 Debian 13 Docker 中因脚本截断报错。** | **已关闭。** 属于偶发性网络问题，但安装脚本的健壮性仍有改进空间。 |
| **低** | [#4065](https://github.com/HKUDS/nanobot/issues/4065) [CLOSED] | **无效的流式超时配置导致崩溃。** | **已修复。** 此项已在这次的 PR [#4363](https://github.com/HKUDS/nanobot/pull/4363) 中解决。 |
| **低** | [#4079](https://github.com/HKUDS/nanobot/issues/4079) [CLOSED] | **API 空响应重试导致用户消息重复。** | **已修复。** 此项已在这次的 PR [#4358](https://github.com/HKUDS/nanobot/pull/4358) 中解决。 |

---

#### 6. 功能请求与路线图信号

-   **新增搜索提供商**：PR [#4350](https://github.com/HKUDS/nanobot/pull/4350) 提议集成 `Keenable` 搜索。这延续了项目作为“万能接口”的定位，持续扩充外部工具生态。
-   **WebUI 自动化管理**：PR [#4330](https://github.com/HKUDS/nanobot/pull/4330) *(今日合并)* 将自动化管理从后台搬到了 WebUI，这是提升用户自主配置能力的重要一步，预计未来会继续完善该功能。
-   **代理精细化配置**：PR [#4367](https://github.com/HKUDS/nanobot/pull/4367) *(已提交)* 和 Issue [#4366](https://github.com/HKUDS/nanobot/issues/4366) 表明，用户对于网络代理的处理有更精细化的要求。未来版本可能会引入更复杂的代理规则配置。
-   **语境/缓存优化**：PR [#4371](https://github.com/HKUDS/nanobot/pull/4371) *(待合并)* 提议在系统提示词中增加“断点”以优化缓存，PR [#4370](https://github.com/HKUDS/nanobot/pull/4370) *(今日合并)* 默认启用了空闲压缩。这表明项目正积极探索通过技术手段（而非单纯扩大窗口）来优化 LLM 的成本和延迟。

---

#### 7. 用户反馈摘要

-   **积极的用户反馈**：
    -   用户 `adminmetavision-rgb` 在 Issue [#4362][已关闭] 中主动宣传其产品 `MetaVision AI Studio` 已适配 NanoBot 的 A2A/MCP 协议，这表明项目在业界具有一定的吸引力和生态影响力。

-   **典型的用户痛点**：
    -   **安装/环境问题**：Issue [#4360] 和 PR [#4368] 反映了用户在 Docker、macOS 等不同环境中安装时遇到的各种问题，安装脚本兼容性是持续需要关注的领域。
    -   **配置理解的偏差**：Issue [#4242] 显示用户对 `dream.enabled` 的理解存在偏差。用户期望关闭梦功能后系统提示词中的“近期历史”部分也随之消失，但实际并非如此。这说明功能文档和预期行为需要更清晰的定义。
    -   **工作区边界问题**：Issue [#4375] 和 [#4374] 凸显了“项目工作区”功能虽然强大，但其边界规则（读写路径、安全策略）对普通用户来说可能过于复杂，易产生混淆。

---

#### 8. 待处理积压

-   **重要且长期未响应的 PR（需要维护者关注）**：
    -   **[#3662]** *[OPEN]* `fix(tokens): avoid network loads during estimation`：该 PR 试图避免令牌估算时产生网络请求。**自 2026-05-06 开放至今已 42 天**，但无新评论。这是一个有价值且能提升离线/内网环境下用户体验的优化，建议项目维护者尽快评估合并。([链接](https://github.com/HKUDS/nanobot/pull/3662))
    -   **[#4053]** *[OPEN]* `fix(tools): keep read-only roots out of write paths`：该 PR 旨在加强文件系统访问的安全性，防止工具将只读目录写入。**自 2026-05-29 开放，已近三周**。建议考虑并入。([链接](https://github.com/HKUDS/nanobot/pull/4053))

-   **长期未解决的重要 Issue**：
    -   **无**。数据显示，近期提交的 Bug 多数得到了快速响应或已有关联的修复 PR，项目 Bug 处理效率较高。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目 2026-06-17 动态日报。

---

## Hermes Agent 项目日报 — 2026-06-17

### 1. 今日速览

项目今日处于**极高活跃度**状态，24小时内产生50条Issue和50条PR，社区参与非常热烈。核心开发集中在**多云多租户支持**、**平台适配器稳定性**（特别是企业微信WeCom和QQ Bot）以及**安全与轨道控制**的增强。尽管今日无新版本发布，但大量的PR提交和Bug修复表明项目正处于密集的开发迭代期。值得关注的是，关于**多租户隔离**的深度技术讨论和**Claude OAuth计费**的Bug报告表明，项目在服务化、商业化部署方面面临关键挑战。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日有少量PR被合并/关闭，主要集中于修复性工作，体现了项目对稳定性的关注：
- **平台适配器修复**：
    - [PR #47562](https://github.com/NousResearch/hermes-agent/pull/47562) **[merged]** 修复了飞书平台交互式卡片中表格数据无法被正确提取为回复上下文的问题。
    - [Issue #47529](https://github.com/NousResearch/hermes-agent/issues/47529) **[closed as duplicate]** 关于Slack平台交互按钮的功能请求被标记为重复，说明该功能已在其他PR中涵盖或规划。
    - [Issue #47360](https://github.com/NousResearch/hermes-agent/issues/47360) **[closed as duplicate]** Discord平台网关收不到消息事件的Bug被标记为重复，表明有更核心的修复路径。
- **维护性工作**：
    - [PR #47575](https://github.com/NousResearch/hermes-agent/pull/47575) **[merged]** 临时关闭了Dependabot自动更新，以解决其与PR检查自动化工具的冲突问题，这是一个积极的工程运维调整。

### 4. 社区热点

今日社区讨论热度高，主要围绕几个焦点展开：

1.  **多租户架构挑战**：[Issue #34352](https://github.com/NousResearch/hermes-agent/issues/34352) “解决多租户Hermes问题” 获得了高达7条评论。用户 `NimbleCoAI` 提出了一个核心痛点：当前的内存操作绕过了系统的钩子系统，导致在不修改核心代码的情况下无法实现租户隔离。该用户声称已在生产环境中运行了一套修复方案数月，这一呼声反映了企业级用户对多租户部署的迫切需求。

2.  **平台交互体验迭代**：[Issue #8552](https://github.com/NousResearch/hermes-agent/issues/8552) “Slack平台应使用Block Kit Markdown块类型” 获得了9个赞和7条评论。用户强烈希望Slack适配器支持更现代的Block Kit功能（如表格），以替代旧的 `mrkdwn` 格式，提升消息的可读性和交互性。

3.  **付费订阅用户的计费困扰**：[Issue #40014](https://github.com/NousResearch/hermes-agent/issues/40014) “Claude Code OAuth仍然调用按token付费的API” 持续引发关注。用户在使用Claude Max订阅时，其OAuth认证下的请求仍被路由到付费API，导致消耗的是“额外使用”积分而非订阅配额。此问题直接关系到核心付费用户的利益，急需解决。

### 5. Bug 与稳定性

今日报告了大量Bug，按严重程度排列如下：

- **严重 (P1)**:
    - [Issue #47134](https://github.com/NousResearch/hermes-agent/issues/47134) **(修复中)**: 执行 `/reload-mcp` 命令导致网关崩溃，原因是 `killpg` 信号误杀网关自身进程组。这是一个严重的功能性崩溃问题。  *(已有相关讨论和PR)*

- **高 (P2)**:
    - [Issue #19821](https://github.com/NousResearch/hermes-agent/issues/19821) **(修复中)**: QQ Bot的WebSocket连接会进入“僵尸”状态，静默断连长达18+小时，导致服务不可用。*（已有 [PR #47586](https://github.com/NousResearch/hermes-agent/pull/47586) 提出三层修复方案）*
    - [Issue #47121](https://github.com/NousResearch/hermes-agent/issues/47121): TUI会话中MCP工具缺失，原因是 `wait_for_mcp_discovery` 超时设置(0.75秒)远短于实际发现时间(约6秒)，属于时序竞争Bug。
    - [Issue #47571](https://github.com/NousResearch/hermes-agent/issues/47571): 企业微信适配器在发送消息时硬截断4000字符，破坏了插件级的分段逻辑。
    - [Issue #47564](https://github.com/NousResearch/hermes-agent/issues/47564): 企业微信适配器在收到特定错误码后，未触发WebSocket重连，导致57-79秒的死窗口期。

- **中 (P3)**:
    - [Issue #47539](https://github.com/NousResearch/hermes-agent/issues/47539): Telegram打字指示器可能无限持续，原因是 `_keep_typing` 异步任务在特定边缘情况下未能正确清理。
    - [Issue #47498](https://github.com/NousResearch/hermes-agent/issues/47498): 桌面应用在发送图片时崩溃，抛出“`Maximum call stack size exceeded`”错误。
    - 多项关于企业微信、桌面端、Kanban工作流的其他Bug。

### 6. 功能请求与路线图信号

社区积极贡献新功能设想，一些方向与现有PR呼应，可能影响未来路线：

- **核心架构演进**：
    - [Issue #34352](https://github.com/NousResearch/hermes-agent/issues/34352) 提出的**多租户隔离**是迈向企业级服务的必由之路。
    - [PR #47027](https://github.com/NousResearch/hermes-agent/pull/47027) 提出的 **CICS模型单守护进程多Agent架构**，与多租户需求高度相关，可能是未来的重要方向。

- **平台能力增强**：
    - [Issue #8552](https://github.com/NousResearch/hermes-agent/issues/8552) 的 **Slack Block Kit支持**和 [Issue #47517](https://github.com/NousResearch/hermes-agent/issues/47517) 的 **WhatsApp群组Skill**，表明用户对核心平台交互体验有更高要求。

- **工具与集成**：
    - [Issue #10011](https://github.com/NousResearch/hermes-agent/issues/10011) **自动发现自定义模型端点**的需求，对于使用API网关的用户至关重要。
    - [Issue #47199](https://github.com/NousResearch/hermes-agent/issues/47199) **将Claude Code订阅集成为MCP Provider**，旨在让用户无需额外API密钥即可使用本地后端，是提升付费用户体验的重要方向。

### 7. 用户反馈摘要

从今日的Issues中可以看出用户的真实痛点：

- **“我们的生产部署希望任务在创建时是‘阻塞’状态，但系统在1秒后自动将其提升为‘就绪’并执行，绕过了人工审批环节。”** - [Issue #39609](https://github.com/NousResearch/hermes-agent/issues/39609) 描述的Kanban工作流Bug，体现了对工作流状态控制的严格要求。
- **“我在MacBook上本地部署的Gemma 4模型，通过Ollama能正常对话，但配置到Hermes后连‘hello’都回复不了。”** - [Issue #45924](https://github.com/NousResearch/hermes-agent/issues/45924) 指出了与Ollama等本地模型的兼容性问题，影响本地开发体验。
- **“Claude Max订阅是收费的，但Hermes依然从我的‘额外使用’积分扣费，而不是从订阅配额中走。”** - [Issue #40014](https://github.com/NousResearch/hermes-agent/issues/40014) 反映了付费用户对计费逻辑不透明的强烈不满。
- **“桌面自动更新在Linux上完成100%后就卡死了，应用也重启不了，只能强制杀掉进程。”** - [Issue #41737](https://github.com/NousResearch/hermes-agent/issues/41737) 报告了一个平台特定的桌面应用更新问题，影响用户升级维护。

### 8. 待处理积压

以下为长期未解决或近期活跃但尚未得到充分回应的重要问题，提醒维护者关注：

- **[Issue #19821](https://github.com/NousResearch/hermes-agent/issues/19821)** (2026-05-04 创建，P2): QQ Bot WebSocket“僵尸”连接问题，虽已有修复PR，但问题存在超过1个月，对用户影响大。
- **[Issue #40014](https://github.com/NousResearch/hermes-agent/issues/40014)** (2026-06-05 创建，P2): Claude OAuth计费问题直接影响付费用户的核心利益，虽然近两日有更新，但仍需明确解决方案和时间线。
- **[PR #19159](https://github.com/NousResearch/hermes-agent/pull/19159)** (2026-05-03 创建): 支持macOS系统的LaunchDaemons服务管理，该PR已开放超过1个月，对macOS用户的服务化部署很重要。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 GitHub 数据，为您生成了 PicoClaw 项目 2026-06-17 的每日动态日报。

# PicoClaw 项目动态日报 (2026-06-17)

## 1. 今日速览

项目今日活跃度极高，尤其在 Bug 修复和代码合并方面。过去 24 小时内成功合并/关闭了 12 个 PR，并处理了 2 个 Issue，显示出强大的发布能力。然而，社区焦点集中在一组由安全研究员集中提交的 11 个安全相关 Issue 上，这些 Issue 已被标记为“stale”，虽更新但尚未有对应的修复 PR，构成潜在风险。总体而言，项目在快速迭代功能与稳定性的同时，正面临一轮集中的安全审计压力。

## 2. 版本发布

今日发布了一个新的 **Nightly Build** 版本：

- **版本**: `v0.3.0-nightly.20260617.a16a1e15`
- **特性**: 自动化构建，旨在让早期用户和开发者体验 `v0.3.0` 主线上的最新变更。
- **风险提示**: 官方警告此版本为自动化构建，可能不稳定，建议谨慎使用。
- **变更日志**: [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

**迁移/使用注意事项**:
- **破坏性变更**: 无明确声明，但因是 nightly 版本，可能包含未测试完全的代码。
- **常规建议**: 生产环境用户应继续使用稳定版 `v0.3.0`。若想尝鲜，建议在非核心环境部署并做好数据备份。

## 3. 项目进展

今日的 PR 活动揭示了项目在多个维度上的重要推进：

- **稳定性与韧性增强**:
  - **panic 恢复**: PR #3132 为核心路径上的 goroutine 添加了 `defer-recover` 保护，防止单一协程崩溃导致整个进程退出，这是一个关键的系统韧性提升。
  - **错误处理优化**: 多个 PR (#3127, #3129, #3130) 专注于显式处理或忽略文件描述符关闭、JSON 编解码等操作中的错误，提升了代码的健壮性和可维护性。

- **功能迭代**:
  - **远程管理**: PR #3137 新增了 `tools.cron.command_allowed_remotes` 配置，允许用户指定哪些远程渠道可以执行 cron 命令，强化了远程控制的安全边界。
  - **插件化扩展**: PR #3120 移除了为第三方（out-of-tree）渠道注册配置的障碍，通过 `RegisterChannelSettings` 钩子，使项目在不 fork 的情况下更易扩展，这将吸引社区开发更多渠道适配器。

- **关键 Bug 修复**:
  - **Telegram 适配器**: PR #3135 修复了一个用户反馈的 Telegram Forum 话题回复问题（Issue #3110），确保机器人在特定话题内回复时，消息不会错误地发送到 `#General` 频道。
  - **Gemini 提供者**: PR #3136 修复了 Gemini API 工具调用中 `thoughtSignature` 字段格式问题，增加了对 Gemini 3.5 Flash Agentic 模型所需的 `thought_signature`（snake_case）格式的支持。

这些进展表明项目在稳固基础、修复高频 Bug 和拓展生态方面正在稳步前进。

## 4. 社区热点

今日最引人注目的社区事件是安全研究员 **YLChen-007** 集中提交了一系列（11个）安全漏洞报告（Issue #3070 - #3082）。虽然每个 Issue 的评论数不高（约1-2条），但如此集中的、高质量的安全报告提交，构成了今日最重要的社区信号。

- **热点链接**:
    - [Security] PicoClaw Feishu reply-context expansion bypasses `allow_from` for fetched parent messages (#3082)
    - [Security] Approval hook `cwd` symlink race allows `exec` to run in a different directory than the approved one (#3081)
    - [Security] Cross-Site Request Forgery in PicoClaw Launcher First-Run Password Setup Allows Local Control-Plane Takeover (#3072)
    - （以及其他 #3070 至 #3081 系列 Issue）

- **背后诉求分析**:
  - **深度安全审计**: 这些 Issue 并非普通用户报告，而是有组织的安全审计。研究员系统性地挖掘了从 SSRF 绕过、命令注入、CSRF 到认证绕过等多种攻击面。
  - **功能安全与权限管理**: 报告核心集中在`exec`工具、`web_fetch`工具、Webhook 和渠道授权机制等关键的交互和权限节点上，反映出社区对项目在生产环境中安全性的高度关注。
  - **紧迫感**: 所有 Issue 均被标记为“stale”，暗示社区希望维护者能尽快确认和响应这些潜在的高危漏洞。

另外，功能请求 Issue **#2404**（支持Streaming HTTP请求）虽非今日新建，但保持了 12 条评论和 1 个点赞，是长期以来的社区愿望，其需求热度依然不减。

## 5. Bug 与稳定性

今日报告的 Bug 以集中式安全漏洞为最严重级别，其他功能性 Bug 已迅速关闭。

| 严重程度 | Bug 描述 | Issue/PR 链接 | 当前状态 |
| :--- | :--- | :--- | :--- |
| **严重 (安全)** | 批量报告了 11 个安全漏洞，涵盖 SSRF、CSRF、命令注入、提权、认证绕过等多个方面。 | #3070至#3082 | **待修复** - 已标记为 `stale`，收到社区关注，但尚无 PR 认领。 |
| **高** | `su -c 'echo OK'` 命令执行导致 agent 崩溃退出。 | Issue #3134 | **已关闭** - 报告当日即被关闭，应被视为已修复或已确认。 |
| **中** | Telegram Forum 话题回复时消息错误发送到 `#General`。 | Issue #3110 | **已修复** - 对应 PR #3135 已合并。 |

## 6. 功能请求与路线图信号

- **高优先级信号: Streaming (流式)请求支持**:
  - **诉求**: 用户 `OuSatoru` 在 Issue #2404 中提出，希望在配置文件中增加 `"streaming": true` 选项，以支持向 LLM 后端发送流式 HTTP 请求。这是对标 Python OpenAI Client 的功能。
  - **信号**: 该 Issue 自 4 月提出以来持续活跃（12条评论、1个赞），是当前社区呼声最高的功能需求之一。考虑到今天多个修复 PR 都与底层通信和响应处理相关，该功能可能已被项目路线图考虑。

- **中优先级信号: 远程命令管理**:
  - **诉求**: 允许特定远程渠道执行 cron 命令。
  - **信号**: 对应的 PR #3137 已在今日合并。这表明项目团队正在积极回应用户对远程管理和控制的需求，并已将其落地方案上线。

- **其他信号**: PR #3115 修复了工具输出中的内联 `data:` URL 被错误解析为附件的问题。这反映了社区对通用工具（如 `read_file`）输出结果的准确性有更高要求。

## 7. 用户反馈摘要

- **正面反馈**:
  - **错误处理透明化**: 部分社区贡献者（如 `chengzhichao-xydt`）专注于提升代码的健壮性，通过显式处理（或标记忽略）错误，提高了代码质量，此类贡献通常受到维护团队欢迎。

- **负面/痛点反馈**:
  - **功能稳定性**: Issue #3134 报告了核心 `exec` 工具在固定场景 (`su -c`) 下的崩溃问题，直接影响了用户的命令行交互体验。但问题已很快关闭。
  - **适配器兼容性**: Issue #3110 显示了 Telegram 适配器在 Forum 话题功能上存在瑕疵，这与使用 Telegram 进行群组协作的用户场景直接相关。
  - **安全意识**: 来自安全研究员 `YLChen-007` 的系列报告 (Issues #3070-#3082) 是社区发出的最强烈的负面/担忧信号。这些非用户反馈，而是专业的安全审计报告，表明项目在应对复杂安全威胁方面仍存在短板。

## 8. 待处理积压

**关键积压: 批量安全漏洞报告**
- **问题**: 安全研究员 `YLChen-007` 于 2026-06-09 集中提交的 11 个安全漏洞报告（#3070-#3082），涵盖从 SSRF、CSRF 到命令注入等多种类型，至今已有一周，**尚未有任何公开的修复 PR**。
- **风险**: 这些漏洞被公开披露且无缓解措施，给项目使用者带来了显著的安全风险。
- **建议**: **项目维护团队应立刻将这批安全 Issue 标记为最高优先级**，组织人力评估漏洞影响、分配修复任务，并向社区发布安全公告。考虑到漏洞性质，对生产环境用户的潜在影响极大。
- **链接**:
    - [Security] OneBot inbound media URL handling allows host-side arbitrary fetch (#3070)
    - [Security] Authenticated Pico WebSocket clients can trigger unauthorized gateway configuration reload (#3071)
    - [Security] Cross-Site Request Forgery in PicoClaw Launcher First-Run Password Setup (#3072)
    - [Security] Signed LINE webhook replay allows duplicate inbound event execution (#3073)
    - [Security] PicoClaw `web_fetch` SSRF guard bypass via ISATAP IPv6 literals (#3074)
    - [Security] Untrusted repository-local `skills/` metadata is auto-loaded (#3075)
    - [Security] WeCom group trigger policy bypass (#3076)
    - [Security] PicoClaw `web_fetch` SSRF protection can be bypassed via environment-configured HTTP proxy (#3078)
    - [Security] PicoClaw `exec` command whitelist allows jq environment disclosure (#3079)
    - [Security] Approval hook `cwd` symlink race (#3081)
    - [Security] PicoClaw Feishu reply-context expansion bypasses `allow_from` (#3082)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的 NanoClaw 项目数据生成的 2026-06-17 日报。

---

# NanoClaw 项目动态日报 | 2026-06-17

## 1. 今日速览

过去 24 小时内，NanoClaw 项目保持着中高活跃度。社区共提交了 5 个新 Issue 和 5 个 PR，其中 4 个 PR 已被合并或关闭，显示出高效的协作和问题解决能力。**最关键的进展是修复了预算超限导致用户消息被静默丢弃的 Bug (#2751)**，该修复已合并；同时，一个关于 Tailscale 路由自愈的 PR (#2782) 也被合并，提升了项目的稳定性。社区讨论热点集中在 **Anthropic 账户合规性风险 (#1669)** 和 **Slack 集成中的 URL 链接损坏问题 (#2779)**。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并或关闭了 4 个重要的 PR，显著提升了项目的健壮性和功能稳定性。

- **修复：预算超限不响应问题** [PR #2759](https://github.com/nanocoai/nanoclaw/pull/2759) (已关闭)：此 PR 合并了针对 Issue #2751 的修复，确保当 LLM 调用因预算或用尽而中断时，代理不会静默丢弃响应，而是向用户返回明确的错误或提示信息。这直接解决了用户体验中的关键痛点。

- **自愈：Tailscale Docker 路由服务** [PR #2782](https://github.com/nanocoai/nanoclaw/pull/2782) (已关闭)：修复了 Tailscale 在会话中重建 IP 规则导致路由服务中断的问题。该 PR 将系统服务从 `oneshot` 改为 `service`，实现了路由的自动恢复，提升了网络连通性的稳定性。

- **文档澄清：OneCLI 网关更新说明** [PR #2775](https://github.com/nanocoai/nanoclaw/pull/2775) (已关闭)：修正了关于 OneCLI 网关升级的变更日志，避免用户误解为更新 NanoClaw 会自动升级 OneCLI 网关，明确了这是两个独立的升级过程，降低了用户维护时的困扰。

- **新技能：Webchat v1** [PR #2069](https://github.com/nanocoai/nanoclaw/pull/2069) (已关闭)：一个期待已久的功能，为项目新增了 Webchat 频道/集成技能，拓展了项目的接入能力。

**项目推进度量**：今日有 2 个 Bug 修复合并，1 个功能技能合并，1 个文档改进合并，项目向 1.0 版本稳步迈进。

## 4. 社区热点

- **Anthropic 账户合规性风险讨论** [Issue #1669](https://github.com/nanocoai/nanoclaw/issues/1669)：尽管创建于两个月前，但至今仍在活跃讨论。核心用户在询问当前实现的 Credential Proxy 是否会因为违反了 Anthropic 禁止 OAuth 反向代理的政策，从而触发账户的反欺诈检查。这反映了社区对**平台政策合规性**的高度敏感性和担忧。

- **Slack URL 中的 @handle 被破坏** [Issue #2779](https://github.com/nanocoai/nanoclaw/issues/2779)：作为今日新开的 BUG Issue，迅速成为热点。用户报告，当智能体向 Slack 发送包含 `@` 符号的 URL（如 HackMD、Mastodon 个人主页链接）时，该部分会自动被 Slack 解析为成员提及，导致链接损坏。此问题 **直击日常协作场景**，影响广泛且修复优先级可能较高。

## 5. Bug 与稳定性

- **[严重]** 预算超限消息被静默丢弃 [Issue #2751](https://github.com/nanocoai/nanoclaw/issues/2751)：用户得不到任何回复，可能导致任务失败且无法排查原因。**已有修复 PR #2759 已合并，问题已解决。**

- **[中等]** Slack URL 中 `@handle` 被破坏 [Issue #2779](https://github.com/nanocoai/nanoclaw/issues/2779)：直接破坏用户体验，导致链接失效。**暂无对应修复 PR。**

- **[低-中]** 容器运行器更新检查不完整 [Issue #2784](https://github.com/nanocoai/nanoclaw/issues/2784)：容器运行器的会话源有效性检查仅监控 `index.ts` 文件，当 `ipc-mcp-stdio.ts` 等文件变更时无法被识别，可能导致开发时使用到过期代码。**暂无对应修复 PR。**

- **[低]** SECURITY.md 文档过时 [Issue #2783](https://github.com/nanocoai/nanoclaw/issues/2783)：官方安全文档描述的是已废弃的 v1 信任模型，可能对新手用户造成严重误解。**暂无对应修复 PR。**

## 6. 功能请求与路线图信号

- **绕过 OneCLI 直接使用外部凭据** [Issue #2781](https://github.com/nanocoai/nanoclaw/issues/2781)：“下游打包者”希望在沙盒环境中直接使用环境变量中已配置的凭据，省去配置 OneCLI 的步骤。这表明社区对**部署灵活性**和**与既有基础设施集成**的需求正在增长。

- **管理集群的升级检查可选退出** [PR #2780](https://github.com/nanocoai/nanoclaw/pull/2780) (待合并)：针对将 NanoClaw 打包成不可变镜像的部署场景，需要禁用启动时的升级检查。这一信号与 Issue #2781 相呼应，共同指向了 **“面向系统集成商和管理集群”** 的下一阶段演进方向。

## 7. 用户反馈摘要

- **对话预算警告**：从 Issue #2751 及修复 PR #2759 可以看出，用户（`assapin`）对“静默失败”非常不满意。用户核心痛点是 **“花了预算却没得到任何反馈”**。
- **平台合规担忧**：Issue #1669 的发起者（`LCJD99`）从技术角度提出 Credential Proxy 的合规问题，反映了用户对**长期稳定运行**和**规避账号风险**的深层诉求。
- **数据丢失与格式问题**：Issue #2779 的提交者（`GitOnion`）描述了 `@handle` 被 Slack“篡改”导致链接损坏的精确过程，这体现了用户对**输出数据的准确性和完整性**有严格要求。

## 8. 待处理积压

- **Anthropic 账户风险讨论** [Issue #1669](https://github.com/nanocoai/nanoclaw/issues/1669)：此 Issue 已存在超过两个月，尚未有官方回应或解决方案。考虑到其 **“账号存在被 Ban 风险”** 的严重性，应列为最高优先级进行技术评审和答复，否则可能阻碍用户部署生产环境。

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 · 2026-06-17

## 1. 今日速览

过去 24 小时内，NullClaw 项目保持中等活跃度：共收到 2 条新 Issue（均为 bug 报告），3 条待合并的 Pull Request，无新版本发布。社区反馈主要集中在本地模型集成稳定性（Ollama 回答不完整）与调度器权限问题。3 条 PR 分别修复了 Teams 认证容错、调度器令牌持久化以及扩展了 cron 子代理功能，显示出项目在集成可靠性和自动调度方面的持续投入。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

当日没有 PR 被合并或关闭，但 3 条待合并 PR 对项目关键功能有明显推进：

- **PR #959**（`fix(cron): persist paired token for scheduler tool access`）针对 Issue #839 中“bit 无法访问 scheduler”的问题，在配对成功后向本地加密存储写入 bearer token，使 cron 工具可复用它。这是影响调度工具可用性的重要修复。
- **PR #958**（`fix(teams): accept lowercase serviceurl JWT claim and raise JWKS fetch cap`）修复了 Microsoft Teams Bot Framework 认证中的两个小问题：接受小写 `serviceurl` 声明并提高 JWKS 拉取上限，解决入站消息 403 拒绝问题，提升了企业协作集成可靠性。
- **PR #783**（`feat(cron): cron subagent, run history, JSON output, security hardening`）是功能增强型 PR，引入基于 DB 的 cron 调度引擎（cron_runs 历史表、原子任务队列）、支持多种作业类型（skill/agent/shell）、时区偏移、交付路由和操作告警，同时添加了 JSON CLI 输出。若合并将大幅提升项目的自动化调度能力。

（链接：[PR #959](nullclaw/nullclaw PR #959)、[PR #958](nullclaw/nullclaw PR #958)、[PR #783](nullclaw/nullclaw PR #783)）

## 4. 社区热点

- **Issue #952**（`bug: Local model using ollama returns incomplete answers`）是今日最受关注的讨论，尽管赞数不多（0），但作为新发 issue 且附有截图，描述清晰：使用 Ollama 的 gemma 模型时，代理输出不完整句子。用户期望完整的自然语言回复。该问题尚未有 PR 关联，反映了社区对本地模型对接质量的高要求。
- **Issue #839**（`bug: bit has no access to scheduler !?`）虽然创建于 4 月 18 日，但在今日有 PR #959 直接修复，代表社区反馈已进入解决通道。该 issue 讲的是“bit”组件无法访问调度器，影响了自动任务执行，属于功能使用上的阻塞性 bug。

（链接：[Issue #952](nullclaw/nullclaw Issue #952)、[Issue #839](nullclaw/nullclaw Issue #839)）

## 5. Bug 与稳定性

当日报告的 Bug 按严重程度排列如下：

- **严重：本地模型回答不完整** (Issue #952) — 用户通过 Ollama 加载 gemma 模型后，代理返回截断或不完整的句子，严重影响对话体验。尚无关联修复 PR，需要项目团队定位是模型端问题还是 gateway 处理异常。
- **中等：调度器访问权限** (Issue #839) — “bit”用户无法调用调度器，导致 cron 任务无法被正常触发。已有修复 PR #959 处于待合并状态，该 PR 通过 token 持久化方式解决身份复用问题。

两个 bug 目前均未导致崩溃或数据丢失，但影响核心功能的使用流畅性。

## 6. 功能请求与路线图信号

从 PR #783（cron 子代理功能增强）可以看出，项目团队正在推进**高级调度功能**：DB 化调度器、多种作业类型、JSON 输出以及安全加固。该 PR 如果合并，将显著扩展项目的自动化能力，可能成为下一个小版本（v2026.6.x）的核心特性。

此外，Issue #952（Ollama 不完整回答）虽为 bug，但间接反映了用户对**本地模型集成质量**的期望。若得到修复，将改善面向个人开发者的部署体验。

目前没有明确的 roadmap 文档，但从 PR 及 Issue 趋势判断，“调度可靠性”与“第三方集成兼容性”是近期的开发重点。

## 7. 用户反馈摘要

- 用户在 Issue #952 中表示：“Pulled gemma using ollama and started the agent the agent doesn't answer in complete sentences ”，附带了截图，表明操作流程清晰但结果异常。用户希望得到完整的回答，而非截断输出。这可能是流式响应处理或模型上下文窗口设置问题。
- Issue #839 的用户仅指出“bit has no access to scheduler”，未提供更多上下文，但重现步骤简单（使用最新版本），说明该问题是稳定复现的。PR #959 的贡献者 vernonstinebaker 在摘要中详细解释了修复方案：配对后持久化 bearer token 以允许 scheduler 工具后续调用。这表明开发者已理解用户痛点并给出针对性修复。

整体来看，用户对功能集成（如 Teams、cron）和使用便利性有较高要求，愿意报告具体场景下的失败情况。

## 8. 待处理积压

- **Issue #839** 虽已有 PR #959 修复，但自 4 月 18 日创建以来搁置近 2 个月才得到修复。该 issue 当前仍为 OPEN 状态，PR #959 需合入后才能关闭。建议维护者尽快审查并合并 PR ，以解决长期存在的调度器权限问题。
- **PR #783**（cron 子代理功能）自 4 月 7 日提交后已搁置 2 个多月，期间历经多次更新（最新更新时间 2026-06-16），可能是较大的功能变更导致 review 周期长。该 PR 涉及数据库结构变更和安全加固，若合并需注意向后兼容和迁移脚本。
- 此外，Issue #952 为今日新开，未分配标签或负责人，建议项目核心维护者尽快回复并标记 bug 类型，以稳定社区信心。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-06-17

---

## 1. 今日速览

过去 24 小时，IronClaw 项目保持了 **高活跃度**：共 50 条 Issue 更新（新开/活跃 31 条，关闭 19 条），50 条 PR 更新（待合并 35 条，已合并/关闭 15 条）。本期焦点集中在 **Reborn WebUI** 的自动化与 Skills 页面用户体验改进、**Engine V2** 的持续架构修复、以及 **Google Drive/OAuth** 集成稳定性的增强。核心贡献者（serrrfirat、think-in-universe、sunglow666 等）密集提交了多批 Bug 修复与功能补丁，社区测试反馈（Dogfooding）进一步推动了多个 UX 痛点的确认。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

当日合入/关闭的 **重要 PR** 推动了以下关键改进：

| PR | 标题 | 影响 |
|----|------|------|
| [#4902](https://github.com/nearai/ironclaw/pull/4902) (CLOSED) | `feat(openai-compat): vision support for inline images` | 为 `/v1/chat/completions` 增加内联 Base64 图像支持，完成附件史诗的 Step 4，增强了 OpenAI 兼容层能力。 |
| [#4858](https://github.com/nearai/ironclaw/pull/4858) (CLOSED) | `fix(reborn): show sanitized command details` | 修复 `builtin.shell` 命令在审批对话框和活动历史中不可见的问题，提升安全性与可追溯性。 |
| [#4954](https://github.com/nearai/ironclaw/pull/4954) (CLOSED) | `fix(reborn): surface approval-gate denial to model` | 将审批拒绝结果反馈给模型，避免重复触发相同审批请求而陷入死循环。 |
| [#4995](https://github.com/nearai/ironclaw/pull/4995) (CLOSED) | `feat(bench): forward NEARAI_API_KEY so /benchmark reborn runs use NEAR cloud` | 使基准测试任务可传入 API 密钥，确保评估链路使用 NEAR AI 云而非 OpenRouter。 |

此外，**#5003**（修复 SSO 自动化线程丢失）、**#5002**（修正对话排序）、**#5001**（松弛 provider 输出验证）等高优先级 PR 已提交待审，预计后续合并后将进一步提升自动化与命中的稳定性。

---

## 4. 社区热点

当日讨论量最高的 Issue 集中在用户体验与集成可靠性：

- **[#4942](https://github.com/nearai/ironclaw/issues/4942) (2 评论)**：Reborn WebUI 中工具调用失败后需手动刷新才显示，用户 `zetyquickly` 报告 GSuite 场景下复现，涉及 SSE 推送延迟。
- **[#4853](https://github.com/nearai/ironclaw/issues/4853) (1 评论)**：Railway 多租户环境中工具活动记录在完成后消失，影响运维排障。`sunglow666` 提出后获得维护者确认。
- **[#4881](https://github.com/nearai/ironclaw/issues/4881) (1 评论)**：提议为 IronClaw PR 添加类似 Vercel 的预览部署，工程师 `think-in-universe` 提出该需求，暗示社区开发者对快速验证环境有强烈诉求。

整体社区讨论偏向功能性反馈，DevX 和运维友好度成为隐形热点。

---

## 5. Bug 与稳定性

当日上报的 Bug 按严重程度排列：

| 严重等级 | Issue / PR | 描述 | 修复状态 |
|----------|------------|------|----------|
| **严重** | [#4986](https://github.com/nearai/ironclaw/issues/4986) | 自动化工具审批被永久阻塞，无法超时或重试 | 暂无 fix PR |
| **严重** | [#4992](https://github.com/nearai/ironclaw/issues/4992) | Railway 本地开发 SSO 访问不匹配导致自动化执行失败（无 run/thread 挂载） | **已有 fix PR (#5003)** |
| **中** | [#4991](https://github.com/nearai/ironclaw/issues/4991) | WASM Google Drive OAuth 令牌失效后静默失败，无 AuthRequired 网关 | 暂未修复 |
| **中** | [#4977](https://github.com/nearai/ironclaw/issues/4977) | 审批拒绝后的工具活动状态不一致（仍显示 `RUN`） | 关联 [#4954](https://github.com/nearai/ironclaw/pull/4954) 已合入类似逻辑 |
| **低** | [#4942](https://github.com/nearai/ironclaw/issues/4942) | 工具失败需重新加载才能看到 | 待定 |

值得注意，[#4853](https://github.com/nearai/ironclaw/issues/4853) （多租户活动记录消失）当前无直接修复，但维护者正在调查。

---

## 6. 功能请求与路线图信号

当日新提出的功能需求紧密围绕 **架构演进** 和 **开发者体验**：

| Issue / PR | 内容 | 路线图信号 |
|------------|------|------------|
| [#4881](https://github.com/nearai/ironclaw/issues/4881) | 添加 PR 预览部署（类似 Vercel） | 可能进入 CI/CD 优化阶段，提升 PR reviewer 效率 |
| [#4985](https://github.com/nearai/ironclaw/issues/4985) | Engine V2 持久化 LLM 用量数据到 `/api/admin/usage` | 运维监控需求，V2 成熟度配套 |
| [#4983](https://github.com/nearai/ironclaw/issues/4983) | 移除 NEAR AI 工具消息扁平化兼容路径 | 标记为清理技术债，预计下一版本移除 |
| [#4999](https://github.com/nearai/ironclaw/issues/4999) | 突破 Google Drive `download_file` 1MB WASM 传输上限 | 已有关联 PR [#4997](https://github.com/nearai/ironclaw/pull/4997) 实现主机端提取，但 1MB 容量限制需后续放宽 |
| [#5000](https://github.com/nearai/ironclaw/pull/5000) | Content-digest 流水线（PR2） | Engine V2 无进度检测重构的一部分，长期提升循环可靠性 |

结合已有 PR（#5001、#5000、#4993 等），**Engine V2 的无进展检测与输出感知（content-digest）是当前最活跃的路线图主线**，预计将在 6 月下旬合并形成完整闭环。

---

## 7. 用户反馈摘要

从 Issue 评论和 QA 测试中提炼出以下典型痛点：

- **自动化管理混乱**：`sunglow666` 反复指出仪表盘状态徽章含义不明（MUTED/SIGNAL/INFO/SUCCESS）、失败摘要不可操作、无创建/暂停/删除入口。用户期望“自动化”页面具备完整的 CRUD 交互。
- **Skills 页面缺少搜索**：系统技能列表庞大，无搜索/过滤，用户需手动滚动查找。
- **审批与活动历史脱节**：多次提到审批拒绝后 UI 仍显示运行中、日志页面为空、运行线程难以发现。用户认为审批流应保持实时同步。
- **新建对话排序随机**：`think-in-universe` 反馈新对话未被置顶，导致“最近”列表名不副实。该问题已在 PR #5002 中修复。
- **验证错误残留**：Skills 表单验证后，即使填写正确，错误信息仍不清除，造成混淆。

整体反馈指向 **WebUI 的可用性仍需打磨**，尤其在自动化、Skills、审批三个子区域。积极方面：contributor 对近期 Shell 命令可见性修复（#4858）和审批反馈（#4954）表示认可。

---

## 8. 待处理积压

以下 Issue/PR 长期未获关闭或回复，建议维护者重点审视：

| 项目 | 类型 | 创建时间 | 当前状态 | 需关注原因 |
|------|------|----------|----------|------------|
| [#3890](https://github.com/nearai/ironclaw/pull/3890) | PR | 2026-05-22 | OPEN | 多租户隔离契约测试，已在 crate 级别覆盖，但未合入，可能阻塞后续多租户部署 |
| [#4518](https://github.com/nearai/ironclaw/pull/4518) | PR | 2026-06-06 | OPEN | Reborn 扩展生命周期 E2E 测试，涉及扩展搜索/安装/激活/删除，对扩展生态稳定性至关重要 |
| [#4692](https://github.com/nearai/ironclaw/issues/4692) | Issue | 2026-06-10 | OPEN | 本地 Dogfooding 大合集，内含多条子问题的跟踪，若迟迟不关闭可能导致用户报告感受不到反馈 |
| [#4879](https://github.com/nearai/ironclaw/issues/4879) | Issue | 2026-06-15 | OPEN | 最新一期 Dogfooding，与 #4692 重叠，建议合并或明确区分阶段 |
| [#4881](https://github.com/nearai/ironclaw/issues/4881) | Issue | 2026-06-15 | OPEN | 预览部署需求虽已有 1 条评论但未获得 maintainer 评估标签，社区期待尽早响应 |

建议：对 #3890 和 #4518 设定合入时间线；对 #4692/#4879 进行分解或关闭老条目，以保持积压可控。

---

*本文档基于公开 GitHub 数据生成，仅供项目健康度参考。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-06-17

---

## 1. 今日速览

过去 24 小时项目保持中等活跃度。共合并/关闭 3 个 PR，涵盖 Cowork 任务搜索优化、Artifacts 预览体验提升以及聊天滚动控制；另有 1 个早期提交的 PR 仍未合并，且 1 个老 Issue 被重新讨论。社区反馈集中在对操作校验缺失和后台任务假成功的担忧，项目健康度整体稳定，但积压问题需维护者重点关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

昨日合并/关闭的 3 个 PR 主要围绕 Cowork 协同模块和 Artifacts 预览体验的优化：

- **#2170 – fix(cowork): search tasks from database**  
  将 Cowork 任务搜索改为从底层 SQLite 数据库检索，而非仅过滤预加载的最近会话。未提供搜索查询时保持现有会话列表行为不变。  
  [netease-youdao/LobsterAI PR #2170](https://github.com/netease-youdao/LobsterAI/pull/2170)

- **#2169 – feat(artifacts): 优化预览卡片与浏览器预览体验**  
  统一对话窗预览卡片样式、暗色 hover 效果及多文件折叠展示；优化 HTML 打开方式菜单，内置浏览器置顶；调整同路径预览文件的去重与打开逻辑，并补充测试文档。  
  [netease-youdao/LobsterAI PR #2169](https://github.com/netease-youdao/LobsterAI/pull/2169)

- **#2168 – feat(cowork): add scroll-to-bottom control**  
  为 Cowork 对话添加紧凑型浮动“滚动到底部”按钮，支持平滑滚动、滚轮穿透、多语言标签及点击诊断。  
  [netease-youdao/LobsterAI PR #2168](https://github.com/netease-youdao/LobsterAI/pull/2168)

以上改动使 Cowork 的数据查询更可靠，Artifacts 预览交互更流畅，并提升了聊天场景下的用户体验。项目在功能完善和 bug 修复上均有进展。

---

## 4. 社区热点

昨日讨论较为集中的是以下两个话题：

- **Issue #1425 – 快捷键重复无校验**  
  [netease-youdao/LobsterAI Issue #1425](https://github.com/netease-youdao/LobsterAI/issues/1425)  
  用户报告在设置快捷键时，重复绑定同一快捷键可正常保存而不触发校验，期望系统给出提示。此问题自 4 月初以来已有 1 条评论，昨日再次被更新，表明用户对该体验问题仍有关注。

- **PR #1424 – 定时任务“停止” IPC 假成功**  
  [netease-youdao/LobsterAI PR #1424](https://github.com/netease-youdao/LobsterAI/pull/1424)  
  该 PR 指出定时任务的 `stop` 处理器实际上不执行任何操作却返回 `{ success: true }`，且所有定时任务操作（切换、创建、删除等）失败时均没有 UI 错误提示。该问题严重性高，但 PR 自 4 月初提交后始终未合并，昨日有新的动态（更新），社区期待维护者尽快回应。

两个话题均反映了用户对操作反馈和校验缺失的不满，属于 UI/UX 层面的明显缺口。

---

## 5. Bug 与稳定性

| 严重程度 | Bug 描述 | 关联链接 | 是否有修复 PR |
|----------|----------|----------|----------------|
| **严重** | 定时任务“停止”操作假成功：IPC handler 返回 `{ success: true }`，实际不停止任务；且所有定时任务操作失败时 UI 无任何错误提示。 | [PR #1424](https://github.com/netease-youdao/LobsterAI/pull/1424) | 已有 PR 但未合并（stale） |
| **中等** | 快捷键重复绑定无校验，用户可保存冲突快捷键配置。 | [Issue #1425](https://github.com/netease-youdao/LobsterAI/issues/1425) | 暂无 |

定时任务假成功问题风险较高，可能导致用户误以为任务已停止而造成预期外行为；快捷键校验缺失则影响配置体验。

---

## 6. 功能请求与路线图信号

近期合并的 PR 暴露了社区对以下能力的实际需求：

- **Cowork 任务搜索数据库化**（#2170）：用户需要搜索所有历史任务，而不只是加载的近期会话。
- **Artifacts 预览体验优化**（#2169）：用户希望在对话中更清晰地查看 HTML 文件，并能方便地在内置浏览器中打开。
- **聊天滚动控制**（#2168）：在长对话中快速定位底部。

这些功能已在本轮合并中落地，预计将在下一个发布版本中包含。此外，PR #1424 提出的“定时任务错误 UI 反馈”是明确的用户体验改进需求，若被纳入后续版本将补全功能完整性。

---

## 7. 用户反馈摘要

- **快捷键重复校验缺失**（Issue #1425）：用户反馈“设置快捷键重复时，点击保存即可正常保存，无重复校验”，期望保存时有弹窗或提示。  
- **定时任务错误无反馈**（PR #1424 描述）：所有操作（开关、创建、更新、删除、运行）失败时，Redux 中的错误状态未在任何 UI 组件中读取，导致用户完全感知不到失败。该问题影响所有使用定时任务的用户。  
- **搜索范围局限**（PR #2170 动机）：用户之前只能搜索预加载的最近会话，导致找不到较早的任务，现在通过数据库搜索得以改善。

这些反馈揭示了用户对操作即时反馈和数据检索范围的明确期望。

---

## 8. 待处理积压

以下两个条目长期未得到有效处理，建议维护者优先跟进：

| 类型 | 编号 | 描述 | 状态 | 最后更新 |
|------|------|------|------|----------|
| PR | [#1424](https://github.com/netease-youdao/LobsterAI/pull/1424) | 定时任务“停止”假成功 + 无错误 UI 反馈 | OPEN / stale | 2026-06-16 |
| Issue | [#1425](https://github.com/netease-youdao/LobsterAI/issues/1425) | 快捷键重复绑定无校验 | OPEN / stale | 2026-06-16 |

这两个条目均自 4 月初创建，昨日有不同程度的活动（更新），但尚未被明确处理。PR #1424 本身已包含修复代码，建议维护者评估后合并或给出替代方案；Issue #1425 则需确认是否与某个已存在的重复校验机制冲突，或作为新功能标签加入路线图。

---

**总结**：项目昨天在功能优化上有所推进，但两个积压问题（定时任务假成功、快捷键无校验）持续受到社区关注，需要尽快处置以提升用户信任度。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw 项目日报 | 2026-06-17

**数据来源：** [TinyAGI/tinyagi](https://github.com/TinyAGI/tinyagi)  
**报告周期：** 2026-06-16 00:00 UTC — 2026-06-17 00:00 UTC

---

## 1. 今日速览

- 项目过去24小时整体活跃度极低，**Issues 无新增、无关闭，PR 仅一条待合并，无新版本发布**。
- 唯一的一条 PR #281 专注于解决 Windows 原生环境下 CLI 的兼容性问题，属于关键平台支持修复，但尚未获得 Reviewer 关注。
- 没有社区互动（无评论、无点赞），项目处于**静默维护状态**，建议维护团队加速对 PR 的评审以保持社区信心。
- 综合来看，TinyClaw 项目健康度**中等偏低**，功能开发和社区运营均出现停滞。

---

## 3. 项目进展

### 关键 PR（待合并）

#### #281 [OPEN] fix: Windows cross-platform support in CLI
- **作者：** mperkins0155
- **状态：** 等待合并
- **解决的问题：** Windows 原生终端（非 WSL）下运行 `tinyagi` CLI 时遇到的三个 Bug：
  1. **驱动器号重复导致 `MODULE_NOT_FOUND`**  
     `new URL('.', import.meta.url).pathname` 在 Windows 下返回 `/C:/Users/...`，与 `path.resolve` 结合时产生 `C:\C:\...` 路径，引发模块加载失败。
  2. **路径分隔符兼容**（推测，PR 摘要未完整列出，但属于典型 Window 问题）
  3. **进程/子进程调用差异**
- **意义：** 该修复填补了项目在**跨平台部署**上的重要空白。此前仅支持 WSL 或 Linux，Windows 原生用户无法使用 CLI，成为 adoption 瓶颈。

> 📎 [PR #281 详情](https://github.com/TinyAGI/tinyagi/pull/281)

---

## 4. 社区热点

今日无任何 Issues 或 PR 产生评论或点赞，社区讨论量为零。PR #281 虽为重要修复，但未引发反馈，可能原因包括：

- 项目通知设置导致社区未及时知晓；
- 贡献者缺乏 reviewer 关注；
- 潜在 Windows 用户群体尚未被有效触达。

**建议：** 维护者在社区渠道（如 Discord、Discussion）主动推送此 PR，鼓励 Windows 用户测试并反馈。

---

## 5. Bug 与稳定性

当前没有新报告的 Bug。PR #281 指向的 Windows 兼容性问题属于**已知回归/平台缺失问题**，严重程度**高**（阻碍 Windows 原生用户使用 CLI）。该修复已由 PR 提供，但尚未集成。

| 级别 | 问题描述 | 关联 PR | 状态 |
|------|----------|---------|------|
| 🔴 高 | Windows CLI 启动失败（路径重复导致模块未找到） | #281 | 待合并 |

---

## 6. 功能请求与路线图信号

今日无新功能请求。PR #281 属于**平台支持**而非新功能，但可能暗示用户对**跨平台原生体验**的需求上升。若合并，将为后续 Windows 上构建 Docker、GUI 等扩展奠定基础。

---

## 7. 用户反馈摘要

无新 Issues 或 PR 评论可供分析。仅有 PR #281 的摘要叙述，反映了贡献者 mperkins0155 的实际使用痛点：

- **场景：** Windows 开发者希望在 VS Code / PowerShell 中直接运行 `tinyagi`，避免启用 WSL。
- **痛点：** `new URL` + `path.resolve` 的跨平台行为差异导致模块解析失败，属于 Node.js 生态的经典陷阱。
- **满意度：** 未收到回复，但贡献者已提供完整修复代码，表明有较强的贡献投入。

---

## 8. 待处理积压

目前无长期未回应的 Issues 或 PR。唯一的 PR #281 创建于 2026-06-16，已过去约 24 小时，尚未获得任何审查。建议维护者尽快指定 Reviewer 或合并，避免贡献者流失。

| 编号 | 类型 | 标题 | 等待时间 | 重要性 |
|------|------|------|----------|--------|
| #281 | PR   | Windows cross-platform support in CLI | 1 天 | ⚠️ 高（阻塞 Windows 用户） |

---

**总结：** 今日 TinyClaw 项目进展缓慢，唯一亮点为 Windows 兼容性修复 PR #281，但缺乏社区响应和管理层关注。建议立即对 PR 进行 code review 并纳入主分支，同时通过公告激活 Windows 用户群体。下一版本若能包含此修复，将显著扩大项目受众。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于给定数据生成的Moltis项目日报。

---

# Moltis 项目动态日报 | 2026-06-17

## 1. 今日速览
项目今日活跃度较高，社区贡献者与维护者互动频繁。过去24小时内，共产生4条Issue和2条Pull Request (PR)，均为高质量的技术讨论。Issues方面，包含3个新开放的工单和1个已关闭的问题，覆盖了功能增强和关键Bug修复。PR方面，两个重要的功能扩展仍在等待合并审查，暂无新的发布版本。整体来看，项目正处于功能升级与稳定性并重的阶段，社区反馈积极，开发进展稳健。

## 2. 版本发布
无。

## 3. 项目进展
今日无PR被合并或关闭。两项重要的待合并PR（#1124和#1125）仍在审查中，代表了项目在可扩展性和配置灵活性方面的重要进展：
- **#1124** 引入了“上下文命令”支持，允许在每次对话轮次前执行外部脚本并将输出注入提示上下文。这对于需要动态获取运行时信息（如当前环境状态、外部数据）的部署场景非常关键。
- **#1125** 为外部代理提供商增加了模型（Model）和努力度（Effort）选择支持，并集成到`/model`命令中。这显著增强了Moltis作为多模型AI中枢的调度能力。

尽管未合并，但这两条PR的存在表明项目在提升复杂场景下的实用性和可配置性方面迈出了重要一步。

## 4. 社区热点
**最活跃 Issue：** [#1126 - [Feature]: allow to configure the format of tts output](https://github.com/moltis-org/moltis/issues/1126)
- **热度分析：** 该Issue在短时间内获得了2条评论，是今日讨论最集中的议题。
- **背后诉求：** 用户 `khimaros` 希望允许用户配置文本转语音（TTS）输出的格式。这反映出社区对于Moltis语音能力的深度定制需求，不仅仅满足于基础的TTS功能，而是期望能对接不同输出设备或处理流程（例如，直接输出二进制音频流、指定文件格式或采样率）。这是提升项目在硬件和音频集成领域适用性的关键需求。

## 5. Bug 与稳定性
今日报告了2个Bug，其中1个已被快速关闭，显示出团队对稳定性问题的响应速度。

| 严重程度 | Issue | 问题描述 | 状态 | 是否关联Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | [#1129 - [Bug]: lack of echo cancellation...](https://github.com/moltis-org/moltis/issues/1129) | **回声消除缺失导致智能体在实时模式下自我触发。** 这是一个严重影响用户体验的Bug，会导致对话循环和混乱。此问题直接关联到语音交互的核心功能。 | 开放 | 否 |
| **中** | [#1128 - [Bug]: transcription errors...](https://github.com/moltis-org/moltis/issues/1128) | 自托管Whisper.cpp存在**转录错误**问题。该问题已于今日被用户关闭，推测可能与配置或特定模型版本有关，或已通过其他方式解决。 | 已关闭 | 否 |

**分析：** #1129提到的回声消除问题是语音助手中的典型痛点，若不解决将严重制约“实时对话模式”的可用性，需要优先处理。

## 6. 功能请求与路线图信号
今日用户提出的功能请求具有高度一致性，均指向**增强系统的可配置性和扩展性**：

- **Issue #1126 (TTS格式配置)** 和 **Issue #1127 (RPC超时配置)** : 这两个需求显示出用户希望有更细粒度的控制权，以适配不同的后端服务和硬件环境。
- **与已有PR的关联：** 这两个新需求与待合并的PR #1124（上下文命令）和PR #1125（模型/努力度选择）在理念上高度一致。它们共同构成了一个清晰的 **“可配置性”路线图**。这强烈暗示，**下一版本的核心主题很可能是“配置与扩展性增强”**，开发团队很可能将合并当前的PR，并考虑将这些新的配置项纳入后续规划中。

## 7. 用户反馈摘要
今日的Issue和PR主要来自两位核心贡献者（`khimaros` 和 `gptme-thomas`），反馈内容专业且具体，代表了高级用户或开发者的真实使用场景：

- **对自我触发机制的困扰（#1129）：** 用户报告了在日常使用实时对话模式时的严重痛点，即智能体听到自己的输出而不断重复触发，这直接导致会话无法正常进行。用户强烈期望加入回声消除功能。
- **对自托管模型的配置期望（#1128）：** 用户在使用自托管Whisper时遇到转录错误，反映了社区用户希望项目能够更好地兼容和维护除官方服务外的多种自部署方案。
- **对集成与自动化的渴求（#1124, #1126, #1127）：** 无论是上下文命令、TTS输出格式还是RPC超时，都表明用户正在将Moltis集成到更复杂的自动化流水线中，不再满足于单一聊天界面，而是需要其作为系统组件运行。

## 8. 待处理积压
今日无长期未响应的积压Issue或PR。所有新提交的Issue和PR均创建于过去24-48小时内，处于活跃处理状态。
- **新开放的2个PR（#1124, #1125）** 和 **3个开放式Issue（#1126, #1127, #1129）** 均需要维护者尽快安排审查和优先级排序，特别是标有 `bug` 标签的 #1129，应优先处理。

---

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-06-17

## 1. 今日速览

过去 24 小时项目保持高强度活跃：共产生 44 条 Issue 更新（新开/活跃 22 条，关闭 22 条）和 38 条 PR 更新（待合并 16 条，已合并/关闭 22 条），并发布了 **v1.1.12-beta.1** 版本。社区讨论焦点集中在上下文压缩导致的进程冻结、桌面端崩溃循环、渠道（钉钉/飞书）稳定性以及模型兼容性问题。多个由社区贡献者提交的 PR 正在处理关键 Bug 和新功能，项目整体呈现“高社区参与、高修复密度”的健康态势。

## 2. 版本发布

**最新版本：v1.1.12-beta.1** ([Release 链接](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12-beta.1))

| 变更类型 | 内容 |
|----------|------|
| 安全修复 | 隔离每个安装实例的 keychain master key，防止跨实例密钥泄露 |
| 桌面端 CI | 强化 Tauri Windows CI 对 crates.io 拉取失败的容错能力 |
| 代码重构 | 持续重构（refactor(cons...），提升内部代码质量 |

**破坏性变更**：无明确提示，预计为兼容性升级。  
**迁移注意事项**：如使用自托管 keychain 或依赖旧版密钥派生逻辑，建议测试后升级；其余用户可直接更新。

## 3. 项目进展

今日合并/关闭的 22 个 PR 中，重要进展包括：

- **#5255** — `chore: bump version 1.1.12b2`，版本递增为下一个候选版做准备。
- **#5175** — 社区贡献者 @nguyenthanhthe 添加了 **越南语界面语言支持**（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5175)），关闭 #5169。
- **#5178** — 同一贡献者实现 **会话标题过滤功能**（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5178)），关闭 #4999，提升会话管理体验。
- **#5248** — 在 ConsoleChannel 中添加 **OSC 8 超链接支持**，终端链接可点击（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5248)）。
- **#5240** — 移除 agent 配置缓存中的冗余深拷贝，**减少内存占用和加载延迟**（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5240)）。
- **#5247** — “Ponytail 编程哲学” + **零依赖代码索引器**，用于提升 coding 模式下代码理解速度（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5247)）。
- **#5201** — 添加 Sprint 2.4 集成测试，覆盖 cron 执行和工具 API（[PR 详情](https://github.com/agentscope-ai/QwenPaw/pull/5201)）。

同时，多项 Bug 修复 PR 已被合入或处于开放待审状态（详见第 5 节），项目在稳定性、性能、多语言支持和开发体验方面均取得实质推进。

## 4. 社区热点

以下 Issue/PR 在本日获得最多评论与关注：

- **[#5218] 子Agent触发上下文压缩时QwenPaw进程冻结无响应**（评论 14）  
  👤 @malongan  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/5218  
  用户报告子 Agent 执行上下文压缩（context compaction）时进程完全卡死，只能靠手动重启恢复。该问题已关联 #5161（长对话无响应），社区讨论强烈，多个用户表示遭遇相同现象，是目前最严重的稳定性投诉。

- **[#5063] 集成 Headroom 作为可选上下文压缩层**（评论 6）  
  👤 @K1-lihongrong  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/5063  
  提议引入第三方压缩层 Headroom，可降低 60–95% 的 token 消耗，且零数据离开本地。社区反响积极，已有对应 PR #5244 进入开放状态。

- **[#4625] MiniMax-M2.5 模型返回 XML 格式导致不兼容**（评论 6）  
  👤 @dcxj163  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/4625  
  问题持续近一个月仍未修复，用户反馈思考过程返回 XML 导致指令与技能无法执行，影响日常使用。该 Issue 关联的 PR 尚不明确，社区等待度高。

- **[#5167] 飞书流式卡片长回复刷新慢**（评论 5）  
  👤 @wjt0321  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/5167  
  用户指出长回复场景下卡片呈“一个字一个字往外吐”的效果，体验比非流式分段更新更差，建议优化流式渲染机制。

- **[#5161] 长对话后QwenPaw无响应**（评论 5）  
  👤 @tecgic  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/5161  
  核心诉求与 #5218 类似，均是上下文积累后的进程冻结问题，社区怀疑同一根源。

## 5. Bug 与稳定性

按严重程度排列今日报告的主要 Bug：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|----------|-------|------|---------------|
| **严重** | #5218 | 子Agent上下文压缩导致进程冻结，需手动重启 | 无，关联 #5242（超时保护）正开放中 |
| **严重** | #5209 | macOS ARM64 桌面端崩溃循环 (SIGSEGV)，chromadb 空指针 | ✅ PR #5238（修复 Tauri 插件依赖循环）已开放；PR #5246（macOS chromadb 配置重写）已开放 |
| **严重** | #5162 | 对话思考逻辑进入死循环 | 无 |
| **中等** | #5206 | `load_agent_config` 返回缓存引用导致配置被静默覆盖 | ✅ PR #5240 已关闭（移除深拷贝） |
| **中等** | #4988 | Windows 路径超限：session ID 在文件名中被重复拼接 | 无，但已关闭（需确认修复版本） |
| **中等** | #4970 | `loop_config.json` / `prd.json` 损坏导致 Agent 会话崩溃 | 无 |
| **较轻** | #5235 | Cron 定时任务不执行，`last_run_at: null` | PR #5241（增加 `misfire_grace_seconds`）已开放 |
| **较轻** | #5250 | Cron 任务干扰主聊天流，注入虚假用户消息 | ✅ PR #5251（添加 silent 选项）已开放 |

**稳定性总评**：核心稳定问题集中在上下文压缩与桌面端内存损坏（chromadb），项目组已通过多个 PR 积极介入，但仍需社区协助测试修复效果。

## 6. 功能请求与路线图信号

以下新功能请求获得较高讨论热度，结合已有 PR 判断可能进入下一版本：

- **Headroom 集成**（#5063）→ PR #5244 已开放，`HeadroomContextManager` 作为可选压缩后端，预计随 v1.1.12 正式版本或 v1.2.0 引入。
- **Agent 自我进化机制**（#5205）—— 用户建议从静态规则文件升级为编译时行为修正，目前无对应 PR，但有社区原型讨论。
- **企业微信图文组合推送**（#5217）—— 当前只能逐条发送，用户期望一次推送文本+图片，未看到对应 PR。
- **Kimi for coding 加入 uv 白名单**（#5156）—— 允许已订阅 Kimi coding 的用户直接接入，社区共鸣较强，尚未有实现。
- **Cron 静默执行选项**（#5250）→ PR #5251 已开放，避免 Agent 在任务中被打断。
- **工作区临时文件位置优化**（#5225）—— 用户建议将所有临时文件移出工作区根目录，避免与用户文件混淆，目前无对应 PR。

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户声音：

- **痛点**：“长对话后 QwenPaw 直接卡死，已经发生多次，严重影响工作流。”（#5161）  
- **痛点**：“飞书流式卡片长回复时，刷新速度比非流式还慢，体感极差。”（#5167）  
- **痛点**：“笔记本睡眠唤醒后钉钉频道静默失效，进程还在但消息无响应，必须手动重启。”（#5214）  
- **痛点**：“MiniMax-M2.5 模型思考过程返回 XML，所有问答中断，求快修复！”（#4625）  
- **满意**：“感谢社区把越南语界面加进来了，我们终于可以用母语操作了。”（#5169 评论）  
- **期望**：“希望能支持 Headroom，这样可以用本地压缩减轻 API 费用，还能保护隐私。”（#5063）  
- **抱怨**：“升级到 1.1.11 后自动宕机重启，docker 环境不稳定。”（#5155）  
- **建议**：“侧边栏菜单太复杂，会话列表却要额外点击，建议参考 Claude Desktop 的简洁设计。”（#4904）

## 8. 待处理积压

以下问题或讨论已存在较长时间，至今未有显著进展，建议维护团队关注：

| 编号 | 类型 | 简介 | 创建日期 | 备注 |
|------|------|------|----------|------|
| #4625 | Bug | MiniMax-M2.5 XML 格式不兼容，影响问答 | 2026-05-22 | 38 天未关闭，社区多次催促 |
| #4622 | PR | datapaw 数据分析插件（12 个 BI 技能） | 2026-05-22 | 初稿后无更新，等待 review |
| #5088 | PR (Breaking) | 治理与沙箱接口讨论 | 2026-06-10 | 涉及重大变更，需谨慎推进 |
| #5063 | Feature | Headroom 压缩层集成 | 2026-06-10 | 已有 PR #5244，但尚未合并 |
| #4904 | Feature | 侧边栏简化建议 | 2026-06-02 | 多个用户表示赞同，但未安排实现 |

> **日报生成说明**：以上数据基于 CoPaw（仓库 agentscope-ai/QwenPaw）在 2026-06-17 的公开活动抽取，内容力求客观准确，供项目团队和社区参考。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目动态日报（2026-06-17）

**数据来源：** [ZeptoClaw GitHub](https://github.com/qhkm/zeptoclaw)  
**统计时段：** 2026-06-16 00:00 UTC – 2026-06-17 00:00 UTC  
**报告生成时间：** 2026-06-17 08:00 UTC

---

## 1. 今日速览

- 过去24小时项目整体活跃度极低：未产生任何新Issue或已关闭Issue，仅有一条由Dependabot自动发出的依赖更新PR（待合并）。
- 无新版本发布，无重要功能合并或Bug修复，社区讨论近乎静默。
- 项目当前处于**低活跃维护期**，主要活动集中在基础设施依赖的常规升级，无实质性功能推进或用户互动。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

**今日无任何PR被合并或关闭。**  
唯一开放的 PR #630 为Dependabot自动提出的Docker基础镜像版本更新（debian `trixie-slim` 从 `b6e2a15` 至 `4e401d9`），尚未有维护者响应。该更新不涉及功能改动，仅提升容器安全性与稳定性。

---

## 4. 社区热点

**今日无热门的Issues或PRs。**  
当前所有Issues及PRs的评论数、反应数均为零，社区未产生讨论。

---

## 5. Bug 与稳定性

**今日无任何新报告的Bug、崩溃或回归问题。**  
项目稳定性未受新事件影响，但需注意长期未处理的潜在技术债务（见第8部分）。

---

## 6. 功能请求与路线图信号

**今日未收到新的功能请求。**  
从已有GitHub数据看，短期内无明确的功能路线图信号。建议维护者关注长期开放性Issue中用户积累的提案。

---

## 7. 用户反馈摘要

**今日无用户反馈。**  
Issues评论区没有任何新评论，无法提取用户痛点或满意度信息。

---

## 8. 待处理积压

**唯一待处理项：**  
- **#630** [OPEN] chore(deps): bump debian from `b6e2a15` to `4e401d9`  
  - 作者：dependabot[bot]  
  - 创建时间：2026-06-16  
  - 链接：https://github.com/qhkm/zeptoclaw/pull/630  
  - **状态：** 待合并。该PR已开放超过24小时，建议维护者尽快审查并合并，以避免Docker镜像安全漏洞暴露窗口。

当前无更长期积压的Issue或PR。项目整体健康度**静默稳定**，但若持续无互动可能暗示维护力量不足或项目进入休眠期。

---

*本日报由AI自动生成，数据基于公开GitHub仓库信息。建议维护者定期与社区互动以保持项目活力。*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-06-17

## 今日速览

过去24小时 ZeroClaw 项目保持高活跃度：共处理50条 Issue（37条新开/活跃，13条关闭）和50条 Pull Request（40条待合并，10条已合并/关闭）。社区提交集中在配置与运行时稳定性修复、文档改进以及 MCP 集成增强。尽管无新版本发布，但多个高优先级 Bug 已被确认并进入修复状态，项目整体健康度良好，但文档和部分关键功能的回归问题（如预编译二进制缺少 Slack/Discord 支持）仍需紧急关注。

## 版本发布

无新版本发布。

## 项目进展

今日共有10个 PR 被合并或关闭（具体列表未公开），同时大量开放 PR 正积极迭代。以下为值得关注的高价值开放 PR：

| PR | 描述 | 影响 |
|----|------|------|
| [#7747](zeroclaw-labs/zeroclaw PR #7747) | **fix(runtime): wire mcp_bundles into agent loop — enforce per-agent MCP server scoping** | 修复所有代理共享全部 MCP 服务器的安全问题，实现按代理隔离 MCP 能力 |
| [#7755](zeroclaw-labs/zeroclaw PR #7755) | **fix(runtime): recover poisoned activated-tool lock reads** | 解决工具锁中毒导致轮次崩溃的严重运行时错误 |
| [#7760](zeroclaw-labs/zeroclaw PR #7760) | **fix(i18n): auto-detect system locale when none is configured** | 恢复 CLI 自动检测系统语言环境的能力，改善全球化体验 |
| [#7722](zeroclaw-labs/zeroclaw PR #7722) | **fix(runtime): condition anti-narration on show_tool_calls config** | 根据 `show_tool_calls` 配置条件化系统提示中的反叙述部分 |
| [#7725](zeroclaw-labs/zeroclaw PR #7725) | **fix(providers): stop reasoning_content from leaking into response text** | 修复 GLM-5.1 等模型将思考内容泄露到最终回复的问题 |

这些 PR 覆盖了运行时安全、工具调用、提供商兼容性和国际化等多个关键领域，全部处于待合并状态，预计将在近期纳入主分支。

## 社区热点

今日讨论最活跃的 Issue：

1. [#6808](zeroclaw-labs/zeroclaw Issue #6808) — **RFC: Work Lanes, Board Automation, and Label Cleanup**（11条评论）  
   社区围绕工作流自动化与标签清理展开治理层面讨论，涉及 0.8.0 版本后的项目管理流程改进。

2. [#6856](zeroclaw-labs/zeroclaw Issue #6856) — **[Bug]: show_tool_calls is missing from [channel]**（5条评论，已关闭）  
   用户反馈 schema v3 缺少 `show_tool_calls` 选项，导致工具调用详情无法在频道响应中显示。该 Issue 已被关闭，表明已有对应修复（关联 PR #7722）。

3. [#6312](zeroclaw-labs/zeroclaw Issue #6312) — **feat(gateway): per-alias webhook path routing for multi-instance channels**（4条评论，已关闭）  
   多实例频道 Webhook 路由方案经长期讨论后今日关闭，标志着该功能进入正式部署阶段。

核心诉求：社区普遍关注配置兼容性、多实例部署、以及工作流治理自动化。

## Bug 与稳定性

按严重程度排列的今日报告 Bug：

**S1 - 工作流阻塞**  
- [#7756](zeroclaw-labs/zeroclaw Issue #7756) — 原生/MCP 工具在 OpenAI Responses/reasoning 和 Anthropic 轮次中不可用（已接受，暂无 fix PR）  
- [#7804](zeroclaw-labs/zeroclaw Issue #7804) — Code 历史可能发送非交替的 Anthropic 消息，导致 400 错误（无 fix PR）  
- [#7758](zeroclaw-labs/zeroclaw Issue #7758) — **文档质量极差，无法编写配置文件**（已关闭，但本质问题未完全解决）

**S2 - 功能降级**  
- [#7820](zeroclaw-labs/zeroclaw Issue #7820) — 本地 shell 审批循环重复执行相同命令（无 fix PR）  
- [#7809](zeroclaw-labs/zeroclaw Issue #7809) — 频道轮次忽略运行时 profile 的 strict/parallel 工具标志（无 fix PR）  
- [#7799](zeroclaw-labs/zeroclaw Issue #7799) — 恢复 Code 会话后显示空白转录（无 fix PR）  
- [#7787](zeroclaw-labs/zeroclaw Issue #7787) — v0.8.0 预编译二进制缺少 Slack/Discord 频道功能（回归，已接受，需紧急修复）

关键回归：v0.8.0 二进制构建时未包含 Slack/Discord 功能，导致众多用户回退到 v0.7.5。该问题已被标记为 P1 并接受。

## 功能请求与路线图信号

今日新提出的功能需求中，以下信号表明可能被纳入后续版本：

| Issue | 描述 | 关联 PR/状态 |
|-------|------|--------------|
| [#7822](zeroclaw-labs/zeroclaw Issue #7822) | WASM 插件应支持生命周期钩子订阅（PluginCapability::Hook） | 新开，无 PR |
| [#7794](zeroclaw-labs/zeroclaw Issue #7794) | **每代理可选梦模式（Dream Mode）** + 聊天命令与网关 Dreams 视图 | 状态：进行中，有基础实现 #6693 |
| [#7762](zeroclaw-labs/zeroclaw Issue #7762) | 定时任务（Cron）缺少文档，且无法指定运行模型 | 新开，无 PR |
| [#7675](zeroclaw-labs/zeroclaw Issue #7675) | **RFC: 硬化 CI 管道** — 供应链扫描、来源证明、SBOM 生成 | 有 PR #? 待确认 |

此外，[#7320](zeroclaw-labs/zeroclaw Issue #7320) v0.8.3 跟踪器显示 MCP 仪表盘及 Web/插件管理界面是下一个里程碑重点。

## 用户反馈摘要

从今日评论中提炼的用户真实痛点：

1. **文档灾难**（#7758）：用户直言“代码再好也没用，文档太烂”，配置语法完全不可知，Quickstart 无法运行。该 Issue 虽已关闭，但文档满意度仍为负值。
2. **shell 审批循环**（#7143, #7820）：多位用户反映 ZeroClaw 反复执行相同 shell 命令（如 `pwd`），耗尽最大工具迭代次数，且审批提示缺乏去重逻辑。
3. **GLM-5.1 思考泄露**（#6643）：使用 GLM-5.1 时，模型思考内容被合并到最终回复中，用户要求重新开放 Issue #5285。
4. **预编译二进制功能缺失**（#7787）：v0.8.0 用户需自行编译才能使用 Slack/Discord，影响团队部署。
5. **时区/国际化**：用户在 S2 反馈中提及 CJK 字符删除需按字节（3次退格），本地化自动检测在无配置时失效（已由 PR #7760 修复）。

## 待处理积压

长期未响应或缺乏关注的重要 Issue 与 PR：

- **Issue #5266**（创建于 2026-04-03）：网关在非默认端口时无法显示配对码，状态 `status:accepted` 且标记 `no-stale`，但至今无 PR。影响多环境部署体验。
- **Issue #6643**（2026-05-13）：GLM-5.1 思考泄露，用户要求重新开放，但昨日仅有1条评论，需维护者确认是否已通过 PR #7725 彻底修复。
- **PR #7077**（2026-06-02）：修复浏览器翻译破坏 React 聊天 DOM，但至今仍在开放，标记 `risk: medium`，可能因测试覆盖不足未合并。
- **PR #7532**（2026-06-12）：配置保存往返丢失问题（#7498），标记 `needs-author-action`，作者未响应。

建议维护者优先处理 #5266 和 #6643，以降低长期积压带来的信任成本。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*