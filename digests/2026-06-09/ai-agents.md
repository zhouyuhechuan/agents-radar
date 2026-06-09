# OpenClaw 生态日报 2026-06-09

> Issues: 500 | PRs: 471 | 覆盖项目: 13 个 | 生成时间: 2026-06-09 02:30 UTC

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

好的，没问题。作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的OpenClaw项目GitHub数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-09

### 1. 今日速览

OpenClaw 项目在过去24小时内展现出极高的社区活跃度和工程交付密度。项目共处理了超过500条Issue和470条Pull Request，其中包含两个新版本发布。虽然社区讨论异常热烈，但大量的待处理（OPEN）问题和未合并的PR也表明项目当前处于一个功能迭代和质量巩固并行的高压期。核心开发者团队正在积极处理会话状态、安全边界和多代理协作等关键领域的修复。

**活跃度评估：极高** (Issues: 9.5/10, PRs: 9/10)

---

### 2. 版本发布

**本次周期内发布了 2 个版本。**

#### v2026.6.5-beta.5
- **主要内容**：
    - **QQBot 修复**：修复了模型推理/思考框架（如 `<thinking>` 标签）内容泄露到QQ频道回复的问题。这显著提升了用户体验和隐私保护。
    - **MCP 工具结果处理**：增强了MCP工具返回结果的兼容性，能够处理`resource_link`、`resource`、`audio`、畸形图片等新型或非标准格式。
- **破坏性变更**：无明确说明。
- **迁移注意事项**：建议所有使用QQBot和MCP工具的用户关注此更新，以获取更稳定的体验。

#### v2026.6.5-beta.3
- **主要内容**：与`beta.5`版本的核心更新内容相同，主要集中在**QQBot**的`<thinking>`标签处理和**MCP工具结果**的兼容性增强。
- **破坏性变更**：无明确说明。

---

### 3. 项目进展

本次报告周期内，项目完成并合并了诸多重要的修复和改进，标志着项目在稳定性和功能完备性上又迈进了关键一步。

- **核心架构与稳定性**：
    - Josh Avant 主导修复了 **`Fix transcript image redaction`** ([#91529](https://github.com/openclaw/openclaw/pull/91529))，解决了会话上下文因图片数据被错误截断而损坏的严重问题。
    - M. Joshi 提交的 **`fix(openai): harden Codex OAuth callback cleanup`** ([#89491](https://github.com/openclaw/openclaw/pull/89491)) 修复了 OpenAI Codex 授权流程的漏洞，增强了安全性。
- **用户体验与平台兼容性**：
    - **`fix(config): use Start-Process -FilePath for Windows config opener`** ([#91536](https://github.com/openclaw/openclaw/pull/91536)) 修复了Windows系统上“打开配置文件”功能失效的Bug。
    - **`fix(cli): bound native hook relay process lifetime`** ([#91147](https://github.com/openclaw/openclaw/pull/91147)) 解决了`openclaw-hooks`子进程泄漏的问题，提升了资源管理。
    - WhatsApp 频道迎来了更新，**`fix(whatsapp): emit hooks for auto-replies`** ([#67477](https://github.com/openclaw/openclaw/pull/67477)) 让自动回复也能触发插件钩子，增强了可扩展性。
- **功能完善**：
    - **`docs(exec): correct host=node auto-routing under an active sandbox`** ([#89439](https://github.com/openclaw/openclaw/pull/89439)) 修正了文档中关于沙箱环境下`host=node`路由的错误描述，解决了用户混淆。
    - **`fix(telegram): restore /compact on generic message ingress`** ([#89588](https://github.com/openclaw/openclaw/pull/89588)) 恢复了Telegram上`/compact`命令的回复功能。

**自我评价：** 项目在修复“会话上下文损坏”和“子进程泄漏”这类关键稳定性问题上取得了决定性进展，并保持着良好的跨平台兼容性修复节奏。

---

### 4. 社区热点

过去24小时内，社区讨论主要围绕几个长期存在的、影响核心体验的功能缺陷和安全问题展开。

- **#48788: 文件名编码问题** ([链接](https://github.com/openclaw/openclaw/issues/48788))
    - **热度**：18条评论，持续讨论近3个月。
    - **诉求**：用户 `alex-xuweilong` 提议建立一个中心化的文件名编码工具，以处理跨平台、多语言（如Shift-JIS、GB18030）的文件名乱码问题。这反映了用户在高可用、多语言环境下的一个普遍痛点。

- **#32473: 控制UI需要HTTPS安全上下文** ([链接](https://github.com/openclaw/openclaw/issues/32473))
    - **热度**：17条评论，4个点赞。
    - **诉求**：用户 `RafaelLee` 报告了一个回归Bug，即控制UI在使用VPS+Docker部署时必须要求HTTPS或`localhost`。社区讨论反映了对更灵活的设备身份认证机制的强烈需求，以便于私有化部署。

- **#90083: OpenAI gpt-5.4/5.5 兼容性失败** ([链接](https://github.com/openclaw/openclaw/pull/90083))
    - **热度**：15条评论，3个点赞。
    - **诉求**：用户 `jimmielightner` 报告在升级到2026.6.1后，OpenAI最新的gpt-5.4/5.5模型无法使用，提示`invalid_provider_content_type`。这反映了社区对紧跟大模型最新发布节奏的迫切期望。

- **#50090: 社区技能生态 (ClawHub)** ([链接](https://github.com/openclaw/openclaw/issues/50090))
    - **热度**：15条评论。
    - **诉求**：用户 `ocdlmv1` 指出社区技能生态（Skills & ClawHub）存在“承诺与现实的差距”。开发、测试、发布和版本管理的体验不佳，技能难以复用。这揭示了社区对更成熟、更开发者友好的插件生态系统的强烈渴望。

**总结：** 社区热点集中在 **“多语言/多环境兼容性”、“安全与部署便利性”、“新模型快速适配”** 以及 **“生态系统成熟度”** 这四个核心维度。

---

### 5. Bug 与稳定性

以下为本次周期内报告的最需要关注的问题，按严重程度排列。

#### 高风险 (P1, 影响核心功能/安全)

1.  **[高频] OpenAI gpt-5.4/5.5 兼容性失败** `#90083`
    - **摘要**：升级后，使用最新GPT-5模型失败。
    - **严重性**：高，阻碍用户使用最新模型。
    - **Fix PR**：暂无。

2.  **[关键] 会话上下文混乱** `#32296`
    - **摘要**：代理回复的是上一条消息而非当前消息，导致对话错乱。
    - **严重性**：高，影响核心对话体验。
    - **Fix PR**：暂无。

3.  **[安全] 控制UI HTTPS要求回归** `#32473`
    - **摘要**：非`localhost`部署要求HTTPS，限制部署场景。
    - **严重性**：高，影响部署灵活性和易用性。
    - **Fix PR**：暂无。

4.  **[安全] 技能注入攻击** `#45740`
    - **摘要**：`gh-issues`技能直接将issue内容注入模型提示词，有提示词注入风险。
    - **严重性**：高，存在安全威胁。
    - **Fix PR**：暂无。

#### 中风险 (P2, 影响特定功能或场景)

1.  **[会话] 僵尸子代理** `#48573`
    - **摘要**：`embedded-run`创建的代理终止后，状态泄漏，影响后续会话。
    - **Fix PR**：暂无。

2.  **[数据] 飞书流式卡片内容截断** `#88929` **(已关闭)**
    - **摘要**：飞书卡片消息流式输出异常，最终内容丢失。该问题已被修复并关闭。
    - **Fix PR**：已合并。

3.  **[稳定性] Control UI 卡死** `#45698`
    - **摘要**：仪表盘界面打开一段时间后变得无响应。
    - **Fix PR**：暂无。

---

### 6. 功能请求与路线图信号

用户提出的功能需求显示出对平台“精细化控制”和“生态扩展”的强烈期望。

- **代理级成本预算** `#42475`：用户 `hkochar` 提议在网关层面实施每日/每月成本预算，防止模型调用费用失控。这是一个备受期待的企业级/运营级功能。
- **技能级模型路由** `#43260`：用户 `AlethiaQuizForge` 希望在 `SKILL.md` 中指定使用的模型，允许不同技能使用不同的模型（如小技能用便宜模型，复杂技能用强模型），优化成本和性能。
- **技能优先级配置** `#50199`：用户 `jimmylzt188` 提议为技能配置优先级，当多个技能都可以执行同一任务时，能有明确的选择规则。
- **会话前记忆刷新** `#45608`：用户 `kamikariat` 希望在执行 `/new` 或 `/reset` 前，模型能像做内存压缩一样，执行一次静默的记忆写入，确保重要信息不被丢失。
- **更强大的浏览器工具** `#44431`：用户 `ibadukefan` 基于实地测试提出了7项浏览器工具改进，包括CSS选择器支持，这表明了用户在复杂的网页自动化场景中遇到了瓶颈。

**信号解读：** 当前社区正从“能用”阶段转向“好用”和“可管控”阶段。`#42475`和`#43260`代表了对**运营成本**的关注；`#44431`和`#50199`代表了对**工具易用性和自动化深度**的追求；`#45608`则是用户对**数据安全和记忆连续性**的深层需求。结合仓库中的PR `#91093` (ACP委托会话)，未来的路线图很可能向架构解耦和功能精细化定制方向发展。

---

### 7. 用户反馈摘要

- **正面反馈**： 用户对项目的迭代速度和响应能力总体满意。`#88929` 飞书流式卡片问题的快速修复就是一个积极的信号。
- **负面反馈**：
    - **“升级后出现问题”**：多个Bug报告 (如 `#90083`, `#32473`, `#45698`) 都提到“升级后出现回归”，表明版本发布的质量控制仍需加强。
    - **“承诺与现实的差距”**：`#50090` 社区技能生态的讨论非常尖锐，直指现有技能开发体验不佳，开发者对 ClawHub 的期望与现实之间存在巨大落差。
    - **“硬编码路径”**：`#51429` 中文用户报告代码中存在硬编码的工作路径（`/Users/wangtao`），表述直接且讽刺，反映出对代码质量审查不严的失望。

**用户画像：** OpenClaw 的用户群正在从个人爱好者扩展到小团队和专业开发者，他们对**稳定性、安全性、运营成本和生态系统**提出了更高的要求。

---

### 8. 待处理积压

以下是一些长期未解决的、对项目健康度和社区信心有较大影响的 Issue 和 PR，建议维护团队优先关注。

- **[#43367] 多代理编排不稳定** (3月11日创建，P1)
    - **摘要**：并发添加代理配置会相互覆盖，会话锁定失败，子工作“脱离”主会话。这是多代理场景的核心稳定性问题。
    - [链接](https://github.com/openclaw/openclaw/issues/43367)

- **[#48788] 中心化文件名编码** (3月17日创建，P2)
    - **摘要**：如前所述，社区对此有强烈需求且讨论深入，但迟迟未有明确的推进计划。
    - [链接](https://github.com/openclaw/openclaw/issues/48788)

- **[#45740] gh-issues技能注入风险** (3月14日创建，P1)
    - **摘要**：这是一个明确的安全漏洞，涉及提示词注入，应当优先处理。
    - [链接](https://github.com/openclaw/openclaw/issues/45740)

- **[#49876] Cron会话输出幻觉内容** (3月18日创建，P1)
    - **摘要**：Cron任务在工具调用失败时，会编造内容回复用户，而不是如实报告错误。这是信任与安全的重大隐患。
    - [链接](https://github.com/openclaw/openclaw/issues/49876)

**结语：** 今日的OpenClaw项目像一个高速运转的引擎，既充满了创新和社区热情，也承受着快速迭代带来的稳定性压力。解决上述积压问题，特别是在多代理、安全和高可用性方面的瓶颈，将是项目能否从“先进”走向“成熟”的关键。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将基于您提供的各项目动态数据，为您呈现一份全面的横向对比分析报告。

---

## AI智能体与个人AI助手开源生态横向对比分析报告 (2026-06-09)

### 1. 生态全景

今日，个人 AI 助手/自主智能体开源生态呈现出一幅 **“高速创新与快速迭代并行的双轨图景”**。一方面，以 **ZeroClaw、OpenClaw、IronClaw** 为代表的核心项目正在进行大胆的架构演进（如 ZeroClaw 的“Reborn”架构、IronClaw 的“智能体学习循环”），展现出对下一代智能体能力的探索。另一方面，大量项目（如 **NanoBot、PicoClaw、LobsterAI**）则专注于**安全性加固、跨平台兼容性修复和开发者体验优化**，致力于将产品打磨得更为稳定可用。社区讨论的焦点正从“能否实现”转向“如何安全、可靠、经济地落地”，**安全性、可观测性、精细化控制和开发者生态**成为所有项目共同面对的核心挑战。

### 2. 各项目活跃度对比

| 项目 | 活跃度评级 | Issues 更新数 | PR 更新数 | 新版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 极高 | 500+ | 470+ | 2 | 高速迭代，略有过热，稳定性压力大 |
| **ZeroClaw** | 极高 | 50 | 50 | 0 | 高产出，但 Bug 积压与架构探险并存，风险同在 |
| **IronClaw** | 极高 | 5 | 25 (合并/关闭) | 0 | 聚焦“Reborn”迁移，架构重构期，交付密集 |
| **NanoBot** | 高 | 7 | 37 | 0 | 安全与功能并进，健康度良好 |
| **PicoClaw** | 高 | 1 (关闭) | 19 | 1 (nightly) | 代码质量改善期，但仍需关注平台兼容性问题 |
| **CoPaw** | 高 | 42 | 43 | 0 | 社区活跃，功能迭代与稳定性加固并行 |
| **LobsterAI** | 中-高 | 0 (主要PR) | 19 | 0 | 集中清理长期问题，数据安全功能是亮点 |
| **NanoClaw** | 中 | 1 | 2 | 0 | 安全是主线，但新 Bug 影响核心功能 |
| **TinyClaw** | 低 | 0 | 1 | 0 | 处于静默期，仅安装体验有微小改进 |
| **Hermes Agent** | 高 | 50 | 50 | 0 | 社区需求旺盛，但维护者响应速度与 Bug 积压是短板 |
| **NullClaw / Moltis / ZeptoClaw** | 无活动 | 0 | 0 | 0 | 项目进入静默状态 |

### 3. OpenClaw 在生态中的定位

**OpenClaw 在生态中扮演着“全能型平台”与“核心参照系”的角色**。

- **优势与定位**：与同类相比，OpenClaw 的**社区规模最大、生态最为复杂**，其社区讨论已覆盖了从安全（#32473）、运营成本（#42475）、开发者生态（#50090）到新模型适配（#90083）等全维度议题。它更像一个经过高度抽象、支持广泛集成的“母舰”。
- **技术路线差异**：
    - **与 IronClaw 相比**：IronClaw 正在激进地进行“Reborn”架构迁移，核心是 **产品级认证与授权**。而 OpenClaw 的路线图似乎更倾向于 **功能精细化定制**（如技能级模型路由、成本预算）和 **架构解耦**（如 PR #91093 ACP委托会话）。
    - **与 ZeroClaw 相比**：ZeroClaw 更侧重于 **运行时安全与物理世界交互**（ESP32演示），其社区论坛讨论的 `trait` 安全接口和 OIDC 支持更具“企业级安全”色彩。OpenClaw 则更多在平衡安全、易用性和社区需求。
- **社区规模对比**：OpenClaw 的日活 Issues/PRs 数量级（500+）远超其他项目（多数为50左右），表明其社区参与度和问题暴露程度是其他项目的数倍甚至一个量级。这既是其生态系统繁荣的证明，也是维护压力的来源。

### 4. 共同关注的技术方向

多个项目在同一时间涌现出相似的技术诉求，标志着行业的紧迫需求：

1.  **安全加固与权限控制（所有高活跃度项目）**：
    - **具体诉求**：SSRF 防护（NanoBot #4074）、提示词注入（OpenClaw #45740）、密钥绑定与隔离（CoPaw #5028）、可插拔安全接口（ZeroClaw #7142）、网络出口锁定（NanoClaw #2713）。
    - **涉及项目**：OpenClaw, NanoBot, CoPaw, ZeroClaw, NanoClaw.

2.  **多模态能力与跨平台兼容性**：
    - **具体诉求**：语音转写集成（NanoBot 新增4个提供商）、图片/文档上传处理（NanoBot #4251, Hermes Agent #24860）、Telegram/QQ/WeChat 等渠道的稳定性（PicoClaw, CoPaw, ZeroClaw）。
    - **涉及项目**：NanoBot, Hermes Agent, PicoClaw, CoPaw, ZeroClaw.

3.  **记忆、上下文与 Agent 行为控制**：
    - **具体诉求**：记忆系统自进化（CoPaw #5017）、记忆权重与 Prompt 优先级调整（ZeroClaw #5844）、会话前记忆刷新（OpenClaw #45608）、上下文混乱修复（OpenClaw #32296, Hermes Agent #42449）。
    - **涉及项目**：CoPaw, ZeroClaw, OpenClaw, Hermes Agent.

4.  **开发者体验与插件生态**：
    - **具体诉求**：插件市场与优先级配置（CoPaw #5023, OpenClaw #50199）、动态模型列表（LobsterAI #1522）、声明式技能保护策略（Hermes Agent #27997）、构建/安装自动化（TinyClaw #280）。
    - **涉及项目**：CoPaw, OpenClaw, LobsterAI, Hermes Agent, TinyClaw.

5.  **可观测性与运维**：
    - **具体诉求**：WebUI 显示版本号与更新通知（NanoBot #4233）、自动化运行历史（IronClaw #4580）、崩溃原因诊断（Hermes Agent #42528）。
    - **涉及项目**：NanoBot, IronClaw, Hermes Agent.

### 5. 差异化定位分析

| 维度 | OpenClaw | ZeroClaw | IronClaw | NanoBot | CoPaw | PicoClaw |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全功能通用平台 | 高性能、安全导向 | 产品级/企业级自动化 | 轻量、多模态、可定制 | 本地化、Agent 学习 | 嵌入式、通道网关 |
| **目标用户** | 高级开发/社区 | 安全/运维专家 | 企业/商业用户 | 个人/开发者 | 中国/亚洲个人用户 | IoT/嵌入式开发者 |
| **技术架构** | 高度模块化/插件化 | 运行时可插拔安全层 | “Reborn”架构迁移 | 提供商抽象层 | AgentScope 2.0 迁移 | 轻量级 Go 实现 |
| **核心优势** | 生态最大、功能最全 | 安全边界、物理世界 | 认证、授权、工作流 | 语音/多模集成快 | 开箱即用、本地化 | 性能、平台适应性 |
| **当前痛点** | 迭代过快、稳定性压力 | Bug 积压、架构探险 | 迁移过渡期兼容性 | 长期 Bug 响应慢 | 渠道稳定性 | 非 x86 平台兼容 |

### 6. 社区热度与成熟度分层

- **第一梯队：极高活跃度与快速迭代期**
    - **代表项目**：**ZeroClaw, OpenClaw, IronClaw**。
    - **特征**：日更 Issues/PRs 总数超过 50，社区讨论深度高，涉及架构级变革（如 ZeroClaw 的安全接口，IronClaw 的 Reborn）。项目处于高速演进期，但同时面临较大的稳定性挑战和技术债务。对于寻求前沿功能、愿意承担风险参与早期测试的用户是首选。

- **第二梯队：高活跃度与质量巩固期**
    - **代表项目**：**NanoBot, PicoClaw, CoPaw, LobsterAI**。
    - **特征**：日更 Issues/PRs 总数在 10-50之间。开发节奏稳健，多聚焦于 Bug 修复、安全性加固、特定功能扩展（如语音、消息处理）和开发者体验优化。项目成熟度较高，适合追求稳定生产力的用户。

- **第三梯队：中低活跃度或静默期**
    - **代表项目**：**NanoClaw, TinyClaw, NullClaw, Moltis, ZeptoClaw**。
    - **特征**：活动稀疏，偶有单个 PR 或 Issue。项目可能已进入维护模式、人员变动或计划搁置。NanoClaw 仍在处理安全修复，TinyClaw 仅有安装优化。不建议将此梯队项目作为核心依赖。

### 7. 值得关注的趋势信号

1.  **从“聊天机器人”到“自主智能体”的本质跨越**：**ZeroClaw 的“Computer-use”RFC** 和 **CoPaw 的“学习循环”需求**，清晰表明行业目标不再是简单的对话工具，而是能够主动执行多步骤任务、与物理世界交互、并能从经验中自我进化的“数字员工”。这是一个根本性的范式转变。

2.  **安全与治理成为“刚需”，而非“选配”**：多个项目（ZeroClaw, OpenClaw, NanoBot）不约而同地将 SSRF 防护、提示词注入、密钥隔离、声明式策略作为核心议题。对于计划将 AI Agent 部署到任何生产环境（包括个人自动化场景）的开发者，**安全审计和权限建模**应成为技术选型的第一评估要素。

3.  **开发者体验（DX）将是生态繁荣的分水岭**：从 TinyClaw 的安装修复，到 CoPaw 的插件市场，再到 ZeroClaw 的文档重构，社区对“易用性”的呼声越来越高。**项目能否提供清晰、可维护的 SDK、文档和插件管理机制，将直接决定其能否从“小众工具”成长为“主流平台”**。

4.  **企业级部署与运维能力成为差异化竞争点**：IronClaw 的“Reborn”迁移专注于认证、授权和可观测性；OpenClaw 的代理级成本预算和技能级模型路由也指向了运营管控。这表明 AI Agent 正从个人玩具向**企业级生产力工具**快速演进，具备 OIDC、审计日志、资源预算等能力的项目将更具竞争力。

5.  **IoT 与边缘端是 AI Agent 的下一战场**：**ZeroClaw 的 ESP32 端到端演示**是今日最令人兴奋的信号之一。将智能体能力直接下沉到硬件，实现从云端到设备的闭环自动化（如智能家居、工业控制），这将是 AI Agent 价值实现的重要延伸。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的NanoBot GitHub数据，生成一份结构清晰、客观专业的项目动态日报。

---

# NanoBot 项目动态日报 | 2026-06-09

## 1. 今日速览

昨日NanoBot项目开发活动非常活跃，核心聚焦于 **安全性修复、新功能集成和稳定性增强**。尽管没有新版本发布，但社区与维护者通过 **37条PR**（其中16条已合并/关闭）和 **7条Issue** 的高频互动，展现了强劲的迭代势头。项目在处理社区反馈（如SSRF漏洞、消息分割Bug）的同时，积极合并了多项新功能（如多个新的语音转写提供商、跨智能体通信），整体健康度与成熟度稳步提升。

## 2. 版本发布

*   无新版本发布。

## 3. 项目进展

过去24小时，项目在功能丰富性、代码安全性和系统稳定性上取得了显著进展。

*   **新功能集成**：
    *   **新增多个语音转写提供商**：成功合并了对 **小米MiMo ASR (#4175)**、**AssemblyAI (#4224)** 以及 **OpenRouter (#4113)** 作为转写提供商的支持，极大丰富了用户的选择。同时，合并了 **共享语音输入支持 (#4232)**，将转写能力从特定频道提升为全局功能。
    *   **扩展提供商兼容性**：合并了 `extra_query` 配置支持 **(#4217)**，允许用户为Azure等需要特定查询参数（如 `?api-version=`）的兼容网关添加自定义配置，解决了相关访问问题。
    *   **智能体协作**：合并了 **跨智能体消息传递功能 (#3992)**，允许运行多个NanoBot实例并相互通信，初步实现了智能体间的协作。

*   **安全与稳定性修复**：
    *   **修复SSRF安全漏洞**：通过 **#4221** 修复了执行工具（ExecTool）中的符号链接逃逸问题，并补充了回归测试。
    *   **修复会话历史Bug**：通过 **#4219** 修复了修剪历史记录时可能丢弃孤立工具结果的问题，确保了会话上下文的完整性。

*   **WebUI改进**：
    *   **显示版本号**：合并了 **#4235**，在WebUI设置概览中显示了当前NanoBot版本，并集成了PyPI更新检查，方便用户知晓更新。

项目整体上正在从一个单一的对话引擎，向一个具备 **多模态能力**、**高度可定制** 和 **安全性更强** 的智能体协作平台迈进。

## 4. 社区热点

*   **Issues #4233 & PR #4255: WebUI显示版本号与更新通知**
    *   **链接**: [Issue #4233](https://github.com/HKUDS/nanobot/issues/4233) | [PR #4255](https://github.com/HKUDS/nanobot/pull/4255)
    *   **分析**: 这是最受关注的社区热点之一。用户 `viblo` 提出在WebUI上直观显示版本号的需求，以替代需要访问 `/status` 端点的繁琐操作。这一诉求迅速得到了维护者和其他贡献者的共鸣，并促使了PR #4235（已合并）的诞生。随后，另一贡献者 `JiajunBernoulli` 进一步提交了PR #4255，在显示版本号的基础上增加了 **实时PyPI更新通知**，体现了社区在“用户体验”层面的自主迭代能力，也反映出用户对于“透明度和易用性”的高度关注。

*   **Issues #4253: 支持按对话切换模型**
    *   **链接**: [Issue #4253](https://github.com/HKUDS/nanobot/issues/4253)
    *   **分析**: 用户 `rombert` 提出的“按需切换模型”的需求获得了讨论热度。该用户在使用OpenRouter（快速能力）和本地llamacpp（私密慢速）两种模型时，希望能根据任务类型（如隐私、时效性）在同一会话中灵活切换，而非全局设置。这代表了一类 **高级用户对“精细化控制能力”的迫切需求**，即希望AI助手能更好地适应多样化的工作流。这是一个明确且具潜力的功能方向。

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#4074](https://github.com/HKUDS/nanobot/issues/4074) | **安全漏洞**: MCP HTTP/SSE配置在SSRF拒绝前会尝试回环连接。(已关闭) | **已修复** (相关PR [#4217](https://github.com/HKUDS/nanobot/pull/4217) 已合并) |
| **高** | [#4223](https://github.com/HKUDS/nanobot/pull/4223) | **功能失效**: 微信频道在Session token过期后进入永久静默的“死循环”，无法自动重新扫码登录。 | **待合并** (已提交修复PR, 待审核) |
| **中** | [#4250](https://github.com/HKUDS/nanobot/issues/4250) | **功能损坏**: Telegram频道 `split_message` 功能在分割长消息时，会破坏Fenced Code Block，导致两端渲染出错。 | **已提交修复** (PR [#4257](https://github.com/HKUDS/nanobot/pull/4257) 已提交) |
| **低** | [#4256](https://github.com/HKUDS/nanobot/pull/4256) | **内存管理**: `MemoryStore` 在特定情况下可能出现历史光标分配不单调的问题。 | **待合并** (已提交修复PR, 待审核) |

## 6. 功能请求与路线图信号

*   **支持按对话切换模型 (#4253)**: 该需求已被社区强烈表达，且具有明确的用户场景。虽然暂无直接对应的PR，但结合项目正在强化智能体协作和灵活性，**此功能有极高概率被纳入下一版本的路线图**。
*   **文件/图片上传处理 (#4251)**: 用户 `JFPURE` 提出了在输入框上传文件（如图片、PDF）并让AI分析或总结的需求。这是一个非常普遍的多模态应用场景。考虑到项目近期已合并了 **共享语音输入支持 (#4232)**，将支持范围扩展到了语音，将视觉和文档处理纳入进来是合乎逻辑的下一步。**这是一个明确的路线图信号**，表明项目正向多模态AI助手演进。
*   **WebUI显示版本号 (#4233)**: 已通过 #4235 合并，并将通过 #4255 得到增强。

## 7. 用户反馈摘要

*   **痛点解决**：一位使用 **Azure风格网关的用户** 因无法配置 `?api-version=` 查询参数而遇到404错误 (#4204)。此问题已通过新增的 `extra_query` 功能 (#4217) 得到解决，用户痛点已被响应。
*   **使用场景需求**：用户 `rombert` (#4253) 的工作流需要 **在“能力”与“隐私”之间灵活切换模型**，这反映了个人AI助手用户对 **隐私与性能平衡** 的精细化控制诉求。
*   **体验改善**：用户 `viblo` (#4233) 和 `JFPURE` (#4251) 的反馈，共同指向了用户对 **更直观、更强大WebUI体验** 的期望，包括版本透明度、多模态交互等。
*   **功能损坏感**：Telegram频道用户反馈，消息分割Bug (#4250) 会导致 **代码块渲染失败**，对于需要分享代码的用户来说，这是一个影响使用体验的破坏性Bug。

## 8. 待处理积压

以下为长期存在且未合并/关闭的关键PR，建议维护者重点关注：

*   **[OPEN] PR #4053**: `fix(tools): keep read-only roots out of write paths` (2026-05-29)
    *   **链接**: [https://github.com/HKUDS/nanobot/pull/4053](https://github.com/HKUDS/nanobot/pull/4053)
    *   **说明**: 这是一个重要的安全增强PR，旨在防止写工具（如编辑文件）继承不应有的读写权限。已提交超过10天，且与近期修复的符号链接逃逸问题 (#4221) 同属安全加固领域，建议优先审阅。

*   **[OPEN] PR #4119**: `fix(exec): block relative symlink workspace escapes` (2026-05-31)
    *   **链接**: [https://github.com/HKUDS/nanobot/pull/4119](https://github.com/HKUDS/nanobot/pull/4119)
    *   **说明**: 这是与已合并PR #4221 同一个问题的早期版本。需确认其是否已因 #4221 被取代，或仍包含 #4221 未覆盖的部分，需尽快进行状态清理，避免维护者混淆。

*   **[CLOSED] Issue #4074**: `Security: MCP HTTP/SSE configuration attempts loopback connection...`
    *   **链接**: [https://github.com/HKUDS/nanobot/issues/4074](https://github.com/HKUDS/nanobot/issues/4074)
    *   **说明**: 该安全漏洞已关闭，但鉴于其严重性，建议维护者考虑发布一个 **安全公告** 或 **补丁版本的快速发布**，以告知所有用户尽快更新。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent 项目动态日报 — 2026-06-09

### 1. 今日速览

过去24小时项目活跃度极高，共产生50条Issue更新和50条PR更新。社区反馈密集：新开/活跃Issue达46条，但仅有4条关闭；PR方面，待合并43条，已合并/关闭7条，显示出维护团队正在积极处理大量提交。无新版本发布。主要关注点集中在**安全性**（技能保护策略、Matrix恢复密钥日志泄露）、**稳定性**（多容器s6-log死锁、代理上下文污染）以及**用户体验**（桌面应用粘贴失效、会话丢失等）。整体项目健康度良好，但Bug修复积压压力较大。

### 2. 版本发布

无。

### 3. 项目进展

今日有7个PR被合并或关闭，其中较为重要的包括：

- **PR #26982**（已关闭）：修复成就系统中基于工具动作参数统计`memory_write_events`的逻辑，提升插件数据准确性。🎯  
  [NousResearch/hermes-agent PR #26982](https://github.com/NousResearch/hermes-agent/pull/26982)

- **PR #42532**（已关闭）：新增Kanban工作板概览面板（Workboard），支持Inbox→Plan→Scheduled→Ready→In Progress→Blocked→Preview→Verified/Done流程，并保留后端Kanban状态映射。这是社区呼声较高的项目管理工作流增强。  
  [NousResearch/hermes-agent PR #42532](https://github.com/NousResearch/hermes-agent/pull/42532)

此外，还有多个修复型PR处于待合并状态（见Bug与稳定性部分），预计将在未来几天内合并。整体项目在**桌面应用交互修复**、**代理行为优化**和**插件生态扩展**方面稳步推进。

### 4. 社区热点

今日讨论最活跃的Issue集中在以下三个话题：

1. **#27997 声明式技能保护策略**（评论7条）  
   用户`zccyman` 指出技能保护规则分散在6+文件中，且`skill_manager_tool.py`存在高严重性漏洞。社区普遍认为需要一个集中式声明式策略来确保所有技能操作遵循统一保护规则。该Issue得到7条讨论，但尚无对应的PR，可能成为下个版本的关键特性。  
   [NousResearch/hermes-agent Issue #27997](https://github.com/NousResearch/hermes-agent/issues/27997)

2. **#24860 Dashboard Ctrl+V粘贴失效与图片粘贴不支持**（评论6条，👍1）  
   `sccasupercat` 报告在Web Dashboard中Ctrl+V无法粘贴文本，且无法粘贴图片。此Bug直接影响日常使用，社区讨论聚焦于TUI后端的事件传递机制问题。该Issue已存在近一个月，仍未被修复。  
   [NousResearch/hermes-agent Issue #24860](https://github.com/NousResearch/hermes-agent/issues/24860)

3. **#34457 多容器s6-log锁碰撞死循环**（评论6条，👍3）  
   `CMOS3` 描述在共享数据卷的Gateway+Dashboard多容器部署中，`s6-log`出现亚秒级锁冲突，导致Dashboard侧容器无限重启。该问题影响Docker部署稳定性，获得3个👍，表明许多用户受此困扰。暂时无PR关联。  
   [NousResearch/hermes-agent Issue #34457](https://github.com/NousResearch/hermes-agent/issues/34457)

### 5. Bug 与稳定性

按严重程度排列今日报告的Bug（含已有fix PR的标注）：

| 严重级别 | Issue | 描述 | 已有Fix PR |
|---------|-------|------|-----------|
| P1 | #42449 | `delegate_task` 通过共享插件上下文引擎单例破坏父agent的`context_length`，导致上下文压缩异常 | 无 |
| P1 | #42524 | macOS 26上`hermes gateway start`导致`launchctl`返回exit 5，回退到独立进程，失去LaunchAgent管理 | 无 |
| P2 | #42405 | 记忆容量满时`replace`操作因零匹配进入重试循环，最终无响应（静默挂起） | ✅ **PR #42522** 已提交，返回预览信息帮助代理自愈 |
| P2 | #30399 | Docker镜像中缺失Matrix gateway所需的`mautrix[encryption]`包，且根文件系统只读导致无法安装 | 无 |
| P2 | #42376 | macOS 26.5.1上`hermes gateway restart`生成的plist包含`LimitLoadToSessionType`破坏`launchctl bootstrap` | 无 |
| P2 | #42130 | 已配置OpenRouter凭据但Hermes发送请求时缺少`Authentication`头（已关闭） | 已关闭（可能修复） |
| P3 | #42468 | 桌面侧边栏“Copy ID”因嵌套Radix菜单冲突无效 | ✅ **PR #42529** 已提交 |
| P3 | #42409 | 桌面Artifacts视图所有时间戳显示为1970年1月（epoch秒传入毫秒Date构造函数） | 无 |
| P3 | #42466 | Cron任务中Hindsight内存提供者导致“cannot schedule new futures after interpreter shutdown”错误 | 无 |
| P3 | #42306 | Langfuse插件生成GENERATION span但缺少usage/token计数和成本数据（已关闭） | 已关闭（可能已修复） |

此外还有多个P3级别Bug如桌面文件面板默认远程cwd导致ENOENT、停止按钮后UI运行状态未清除、删除会话后自动复活等，均对日常使用体验有显著影响。

### 6. 功能请求与路线图信号

社区提出的新功能需求中，以下几个可能被纳入下个版本：

- **#27997 声明式技能保护策略**：涉及安全审计和操作一致性，很可能作为v0.17.0的安全基座。
- **#42506 添加usememos内存提供者插件**：开源轻量笔记服务集成请求，有明确第三方仓库链接，实现成本较低。
- **#38357 桌面应用侧边栏显示所有profile的会话**：多profile用户强烈需求，已有初步设计讨论。
- **#16675 / #38641 WeCom（企业微信）优化**：包括消息响应确认和流式编辑支持，表明企业用户需求增长。

已提交的PR也反映了后续路线：
- **PR #42528** 实现网关崩溃原因诊断并在“网关恢复在线”通知中附带崩溃回溯，提升排查效率。
- **PR #42534** 添加Dashboard文件浏览器，支持上传下载删除和拖拽，扩展Web管理能力。
- **PR #42512** 修复Goal Mode过早停止问题，增强代理任务完成判断。
- **PR #42509** 修复413错误（内联图片过大）导致无法恢复的问题，提升多模态使用体验。

这些PR若合并，将显著提升**管理能力**、**可靠性**和**企业场景适配**。

### 7. 用户反馈摘要

从Issue评论中提炼的真实用户痛点：

- **Dashboard粘贴体验**：`sccasupercat` 表示“Ctrl+V无法粘贴文本”严重影响日常聊天输入，且图片粘贴缺失使得多模态场景受阻。用户期望TUI后端能正确转发剪贴板事件。
- **OpenRouter认证失败**：`HermitRobot` 描述“请求缺少认证头”，不得不人工添加`--header`参数绕过。表明提供商配置的自动化认证流程存在分支逻辑缺陷。
- **桌面应用响应闪烁**：`elzorromexican` 报告NVIDIA NIM提供商下助手回答闪一下就消失，终端/工具输出正常但桌面UI无法保持，用户质疑前端渲染与流式数据的同步机制。
- **Windows工具安装问题**：`Marstudioo` 提交了完整的Windows环境诊断技能包，指出Hermes CN Desktop在Windows上首次启动时虽列出缺失依赖，但即便手动安装后仍无法识别。用户寻求“一键修复”方案，并贡献了诊断技能。
- **Cron视图空白**：`Burhanawan90` 发现桌面Cron视图无法渲染`script`/`no_agent`作业，运行历史为空，导致用户无法查看定时任务的执行状态。

### 8. 待处理积压

以下重要Issue或PR长期未响应，提请维护者关注：

- **#12020**（4月18日创建）：希望增加开关关闭API响应中的`hermes.tool.progress`事件，该事件导致兼容OpenAI接口的前端解析失败。至今无任何官方回复。  
  [NousResearch/hermes-agent Issue #12020](https://github.com/NousResearch/hermes-agent/issues/12020)

- **#16675**（4月27日创建）：WeCom优化请求——接收消息后提供“已接收”即时响应。同样无维护者参与。  
  [NousResearch/hermes-agent Issue #16675](https://github.com/NousResearch/hermes-agent/issues/16675)

- **#27997**（5月18日创建）：声明式技能保护策略，评论7条但无PR关联。安全相关项目应优先处理。

- **#24860**（5月13日创建）：Dashboard粘贴问题，严重影响用户体验，已开放近一个月仍未修复。

- **#34457**（5月29日创建）：Docker多容器s6-log锁死循环，获得3个👍，但暂无修复PR。建议维护者评估并给出时间表。

---
*数据来源：Hermes Agent GitHub 仓库（NousResearch/hermes-agent），统计周期 2026-06-08 至 2026-06-09。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-06-09

## 1. 今日速览
过去24小时项目保持高活跃度：处理了19条 Pull Request（其中9条已合并/关闭），关闭1个Bug Issue，并发布了新的 Nightly 构建版本。代码质量改进成为今日主线，大量 PR 聚焦于类型断言安全性、错误包装规范以及日志统一，显示出项目对稳定性和可维护性的持续投入。同时，新增 **DeltaChat 通道网关** 的功能性 PR 也标志着社区对多平台接入的兴趣正在上升。**活跃度评估：★★★★☆（高）**

---

## 2. 版本发布
- **nightly (v0.2.9-nightly.20260609.46b29a0a)**  
  自动构建的每日快照，可能不稳定，仅供测试。  
  **变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  无破坏性变更声明，但升级前建议备份配置文件。

---

## 3. 项目进展（今日合并/关闭的重要PR）
今日共合并/关闭 9 条 PR，主要覆盖以下方面：

| PR | 标题 | 说明 |
|----|------|------|
| [#3052](https://github.com/sipeed/picoclaw/pull/3052) | fix: handle Telegram location messages | 修复 Telegram 位置消息被静默忽略的 Bug，现已支持转换为文本输入代理管道 |
| [#3062](https://github.com/sipeed/picoclaw/pull/3062) | fix: health check always returning not ready | 修复健康检查端点始终返回“未就绪”的问题 |
| [#3051](https://github.com/sipeed/picoclaw/pull/3051) | fix: use %w instead of %v for error wrapping in channels and mcp | 统一错误包装格式，使 `errors.Is/As` 链式调用正常工作 |
| [#3050](https://github.com/sipeed/picoclaw/pull/3050) | refactor: replace log.Printf/fmt.Printf with structured logger | 将多处生产代码中的原始日志替换为结构化日志系统 |
| [#3058](https://github.com/sipeed/picoclaw/pull/3058)、[#3057](https://github.com/sipeed/picoclaw/pull/3057)、[#3056](https://github.com/sipeed/picoclaw/pull/3056)、[#3055](https://github.com/sipeed/picoclaw/pull/3055)、[#3018](https://github.com/sipeed/picoclaw/pull/3018) | 多处类型断言安全性修复 | 在 `webfetch`、`subagent/spawn`、`base.go`、`agent.NewContextBuilder`、LINE 通道和 Evolution 存储中增加 `ok` 检查，消除潜在 panic |

**小结**：项目在稳定性与代码健壮性上迈进一步，尤其是 Telegram 位置消息的修复解决了真实用户反馈（#3049），健康检查回归问题的修复则提升了运维可靠性。

---

## 4. 社区热点
- **Issue #2887** [OPEN] [BUG] .deb version on RISC-V is not functional with OpenAI model  
  作者: s0me0ne-unkn0wn | 评论: 9  
  [链接](https://github.com/sipeed/picoclaw/issues/2887)  
  该问题已存在近一个月（2026-05-17 创建），至今无维护者回复或关联 PR。用户报告在 RISC-V 架构的 Debian 系统上，.deb 包无法正常连接 OpenAI 模型，核心功能受损。目前有 9 条评论，讨论着替代安装方式和调试尝试，但官方未介入。**这是当前社区最大的痛点**，可能影响 RISC-V 生态用户的采用信心。

- **Issue #3015** [OPEN] [BUG] QQ channel connection failed on Windows  
  作者: cuandada | 评论: 2  
  [链接](https://github.com/sipeed/picoclaw/issues/3015)  
  报告 Windows 版 `picoclaw gateway` 启动时无法获取 QQ 频道 App Access Token，导致通道不可用。该问题与 #2887 类似，均为平台特定功能失效，但影响面（Windows 用户）更广，目前无关联 PR。

---

## 5. Bug 与稳定性
| 严重程度 | Issue/PR | 描述 | 状态 |
|----------|----------|------|------|
| 🔴 严重 | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | RISC-V .deb 无法使用 OpenAI 模型 | 未修复，无关联 PR，已开放 23 天 |
| 🔴 严重 | [#3015](https://github.com/sipeed/picoclaw/issues/3015) | Windows QQ 通道连接超时失败 | 未修复，等待反馈 |
| 🟡 中等 | [#3049](https://github.com/sipeed/picoclaw/issues/3049) | Telegram 位置消息被忽略 | **已关闭**，由 PR [#3052](https://github.com/sipeed/picoclaw/pull/3052) 修复 |
| 🟢 轻微 | 多条 PR | 未检查的类型断言、错误包装、日志不规范 | 大部分已通过今日 PR 修复 |

**特别注意**：RISC-V 和 Windows 上两个功能 Bug 仍未获得修复，可能成为下一版本发布阻塞项。

---

## 6. 功能请求与路线图信号
- **PR #3063** [OPEN] feat: add deltachat gateway  
  [链接](https://github.com/sipeed/picoclaw/pull/3063)  
  作者 trufae 为 PicoClaw 贡献了 **DeltaChat 通道网关**，这是一个新兴的去中心化聊天协议。此 PR 目前处于待合并状态，若合入将扩展 PicoClaw 的通道生态，符合社区对多平台接入的期待。无破坏性变更，属于纯新增功能。

- **PR #2904** [OPEN] Fix agent loop reload and panic cleanup stability  
  [链接](https://github.com/sipeed/picoclaw/pull/2904)  
  该 PR 已开放三周，旨在修复 agent 循环重载时的挂起 Goroutine 和 panic 清理问题。虽然属于稳定性修复，但其改动涉及核心循环，可能对于可靠性要求高的用户是重要升级，建议维护者尽快 review。

---

## 7. 用户反馈摘要
- **“无法在 RISC-V 上使用 OpenAI 模型”**（Issue #2887）：  
  用户尝试了多种方法（包括手动编译），但 .deb 包在 RISC-V 上启动后无法正常调用 GPT 模型，日志无有用信息。社区成员建议用户从源码构建，但问题在于官方 .deb 应能开箱即用。这反映出官方对非 x86 架构的测试覆盖不足。

- **“Telegram 位置消息无响应”**（Issue #3049）：  
  用户发现发送定位时客户端无任何反应，日志也无输出，只有文本消息才会触发代理。**该反馈今日已获修复**（PR #3052），预期下一 Nightly 即可体验。

- **“Windows QQ 通道无法获取 Token”**（Issue #3015）：  
  用户反映在 Windows 执行 `picoclaw gateway` 后，一直卡在“attempt to get app access token”阶段，但 Pico 通道正常。可能涉及 Windows 环境下的网络栈差异或证书问题。

---

## 8. 待处理积压
以下 Issue/PR 长期未得到维护者响应，建议优先关注：

| 事项 | 创建时间 | 最新活动 | 备注 |
|------|----------|----------|------|
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | 2026-05-17 | 2026-06-08 | RISC-V .deb 失效，9 条评论，无任何官方回复 |
| [#2904](https://github.com/sipeed/picoclaw/pull/2904) | 2026-05-20 | 2026-06-08 | Agent 循环稳定性修复，已起草完整方案，待 review |
| [#3015](https://github.com/sipeed/picoclaw/issues/3015) | 2026-06-06 | 2026-06-08 | Windows QQ 通道 Bug，2 条评论，无官方响应 |

**建议**：维护者可考虑在下一次发布前对 RISC-V 构建流程进行专项验证，并优先合并 #2904 以解决潜在的重载死锁问题。

---

*本日报基于 GitHub 公开数据自动生成，数据统计截止于 2026-06-09 06:00 UTC。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，以下是为您生成的 NanoClaw 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-06-09

## 今日速览

过去24小时内，项目活跃度中等，主要集中在安全加固与关键Bug修复上。一个关于WhatsApp媒体文件在v2版本中无法被Agent访问的严重Bug被报告，可能影响部分用户的正常使用。与此同时，两项重要的安全改进PR被提交或合并，包括网络出口锁定和对多个认证/安全漏洞的修复，显示出项目团队对安全性的持续关注。整体来看，项目在安全性和稳定性上稳步推进，但新发现的挂载路径Bug值得尽快处理。

## 版本发布

无

## 项目进展

今日有两项重要PR被处理，显著提升了项目的安全性和可配置性：

1.  **出口锁定功能已合并**：[PR #2713](https://github.com/nanocoai/nanoclaw/pull/2713) 已合并。此功能允许用户选择性地将每个Agent容器置于 `--internal` 网络中，强制所有流量通过OneCLI网关代理。这从根本上将Agent与外部互联网隔离，有效防止数据外泄，对于企业级部署场景是一个重要的安全增强。

2.  **多项安全修复已提交**：[PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714) 正在开放审查，专注于修复四个特定的认证与安全问题：
    -   `webhook-server` 默认绑定地址从 `0.0.0.0` 改为 `127.0.0.1`，降低了未授权外部访问的风险。
    -   使用 `crypto.randomUUID()` 替换 `Math.random()` 生成审批ID，增强了抗预测攻击能力。
    -   此外还包括了若干未详细列出的安全加固措施。

## 社区热点

今日没有出现评论数或点赞数特别高的热门讨论。然而，以下两个议题因直接关系到核心功能与安全，成为社区关注的焦点：

- **[问题 #2715](https://github.com/nanocoai/nanoclaw/issues/2715)：WhatsApp媒体文件访问失败**。该问题详细描述了在v2版本中，用户发送的图片、文档、音频等文件被下载到了一个未挂载到Agent容器内的目录，导致Agent无法访问。这直接违反了用户的预期，即Agent能够处理接收到的媒体文件，是一个典型的功能性Bug。

- **[PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714)：修复四项认证/安全问题**。由于安全问题直接影响系统安全性和用户数据，此项PR虽然评论不多，但其内容和性质决定了它是社区高度关心的改进。

## Bug 与稳定性

今日报告了一个影响核心功能的重要Bug：

- **严重程度：高** | **已报告，尚无修复PR**
    - **[问题 #2715](https://github.com/nanocoai/nanoclaw/issues/2715)**：WhatsApp媒体文件路径问题。在v2版本中，Agent无法访问用户发送的媒体文件，因为文件被存储到主机目录 `DATA_DIR/attachments`，而Agent被提供了一个不存在的容器内路径 `/workspace/attachments/...`。
    - **影响**：所有依赖WhatsApp渠道接收图片、文档、音频的用例均会受到影响。

## 功能请求与路线图信号

今日提交的PR均属于安全与稳定性改进，没有明确的新功能请求。然而，从已合并的[PR #2713](https://github.com/nanocoai/nanoclaw/pull/2713)（出口锁定）和开放的[PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714)（多项安全修复）来看，**安全加固**可能是近期项目路线图上的一个重点方向。这些优化很有可能被纳入下一个版本。

## 用户反馈摘要

从唯一活跃的 [问题 #2715](https://github.com/nanocoai/nanoclaw/issues/2715) 中可以提炼出以下用户痛点：

- **失去对核心功能的信任**：用户期望Agent能够“看到”并处理其接收的媒体文件。该Bug破坏了这一核心交互模式，导致WhatsApp渠道的功能性严重受损。
- **配置错误导致故障**：用户遇到的问题并非功能性缺失，而是因为文件挂载配置错误，这反映出在升级到v2时可能存在不易察觉的兼容性或配置问题，增加了用户的使用成本。

## 待处理积压

- **[PR #2714](https://github.com/nanocoai/nanoclaw/pull/2714) (开放中)**：该PR修复了四个重要的安全/认证问题，包括webhook绑定地址和验证ID生成方式。这些是系统级的安全基座，建议维护者尽早审查并合并，以减少潜在的攻击面。

- **[问题 #2715](https://github.com/nanocoai/nanoclaw/issues/2715) (开放中)**：这是一项严重阻碍特定渠道功能的问题，可能导致用户数据丢失或无法处理。建议维护者将其列为高优先级，并尽快提供一个修复PR或临时解决方案，以恢复用户对平台稳定性的信心。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是为您准备的 IronClaw 项目 2026-06-09 动态日报。

---

### IronClaw 项目动态日报 (2026-06-09)

**分析师:** AI 智能体与个人 AI 助手开源项目分析师
**数据来源:** GitHub (github.com/nearai/ironclaw)

---

#### 1. 今日速览

项目今日呈现极高的活跃度，核心开发团队与社区贡献者正全力推进 **“Reborn”** 架构迁移，特别是围绕 **OpenAI 兼容 API 路由**和**产品级认证与授权**两大核心模块进行攻坚。昨日合并/关闭了 25 个 Pull Requests (PR)，成功将关键功能（如 Google Calendar 修复、Codex 模型发现优化）落地，并完成了多项 Reborn 架构重构。同时，社区报告了 5 个新 Bug，主要集中在生产环境升级后的问题和特定场景下的功能异常，显示出项目在快速迭代中遇到的稳定性挑战。整体来看，项目正处于向下一代架构转型的关键冲刺阶段，技术债务清理和新功能开发并行，社区贡献活跃，项目健康度良好但需关注近期暴露的 Bug。

---

#### 3. 项目进展 (合并/关闭的重要 PR)

昨日项目在功能交付和架构完善上取得了显著进展。以下是合并/关闭的核心 PR 及其影响：

- **功能修复与改进**：
    - **[#4578] fix(tools/google-calendar):** 修复了 Google Calendar 工具的 `list_events` 长期存在的 Bug，现在默认返回未来的日程事件，而非最早的事件。这直接提升了用户询问“我有哪些会议？”的体验。([链接](https://github.com/nearai/ironclaw/pull/4578))
    - **[#4576] feat(llm):** 扩展了 `ToolCall` 数据结构，添加了 `arguments_parse_error` 字段，为未来更好地处理模型调用工具时的参数解析错误打下了基础。([链接](https://github.com/nearai/ironclaw/pull/4576))
    - **[#4572] feat(reborn):** 将子代理类型 `researcher` 重构为 `planner`，并重新设计了 `spawn_subagent` 的接口，这意味着 Reborn 智能体将具备更强的结构化规划能力。([链接](https://github.com/nearai/ironclaw/pull/4572))
    - **[#4580] Add automation run history UI:** 合并了自动化运行历史记录的前端UI，用户现在可以在 WebUI 上查看触发器的执行记录，增加了产品的可观测性。([链接](https://github.com/nearai/ironclaw/pull/4580))
    - **[#4566] fix(llm):** 解决了因 `client_version` 硬编码导致 GPT-5.5 等新模型被 Codex 隐藏的问题，用户现在可以自动发现并使用最新的模型。([链接](https://github.com/nearai/ironclaw/pull/4566))
    - **[#4523] fix(host_api):** 修复了 `TenantId`/`UserId` 序列化与反序列化的不对称问题，解决了特定场景下服务不可用的 Bug。([链接](https://github.com/nearai/ironclaw/pull/4523))

- **功能交付与新特性**：
    - **[#4528] feat(slack):** 为 Slack 通道引入了持久化主机-beta 工作流状态，确保关键中断或重启后，Slack 对话的幂等性和状态得以保留。([链接](https://github.com/nearai/ironclaw/pull/4528))
    - **[#4581] Add scoped outbound delivery defaults:** 实现了触发器投递的默认作用域偏好设置，为个人和工作空间/代理场景提供差异化的投递行为。([链接](https://github.com/nearai/ironclaw/pull/4581))

**项目里程碑总结：**
项目成功修复了多个长期存在的“小但恼人”的 Bug，显著提升了工具的可用性。同时，Reborn 架构下的功能交付正在加速，从子代理规划到 Slack 持久化，再到自动化历史 UI，开发者正在有序地填补新架构与现有 V1 产品之间的功能鸿沟，并为用户提供更好的体验。

---

#### 4. 社区热点

今日社区讨论的热点高度集中在 **Reborn 架构下 OpenAI 兼容 API 的实现**。

- **[Issue #3283]:** 作为顶层任务，该 Issue 旨在将 OpenAI 兼容的聊天和响应 API 迁移到 Reborn 平台上。它关联了多个子任务，是当前开发工作的核心目标之一，吸引了核心开发者和社区贡献者的共同关注和投入。([链接](https://github.com/nearai/ironclaw/issues/3283))
- **[PR #4495]:** 该 PR 尝试将非流式的聊天补全路由从 V1 网关迁移到基于 `ProductWorkflow` 的 Reborn 服务上。作为 `#3283` 的关键前置步骤，它引入了智能体重试、幂等性处理等复杂逻辑，评论区和代码审查非常密集，体现了架构迁移过程的严谨性。([链接](https://github.com/nearai/ironclaw/pull/4495))
- **[Issue #4175]:** 关于完成 Reborn 中 `ProductAuth` 的生产后端功能和对齐，以及 OAuth PKCE 的高可用性安全。这表明社区和开发者都在高度关注新架构下的安全性和认证可靠性，确保从 V1 平滑过渡。([链接](https://github.com/nearai/ironclaw/issues/4175))

**分析：**
社区不再满足于 V1 功能的简单复刻，讨论的焦点已经从“是否迁移”转向了“如何迁移得更好”。开发者们正在积极解决新架构下的复杂工程问题，如权限、状态管理和安全，这对于项目的长期健康发展至关重要。

---

#### 5. Bug 与稳定性

昨日共报告 5 个新 Bug，按严重程度排列如下：

- **(严重) [Issue #4548]:** **Bug: Chat completion request serializes duplicate top-level `model` field**。当向 DeepSeek 发送带工具请求时，JSON 序列化产生重复 `model` 字段，导致 API 拒绝请求（HTTP 400）。这是一个严重的功能Bug，影响特定模型提供商的工具使用场景。**状态：** 未修复，问题已提交。([链接](https://github.com/nearai/ironclaw/issues/4548))
- **(严重) [Issue #4536]:** **Bug: OAuth (Google/GitHub) users can't chat**。生产环境问题，启用了 SSO 的情况下，通过 Google/GitHub 登录的用户无法发送任何消息。虽已标记为已关闭，但需要确认根本原因和修复方案是否已部署。**状态：** 已修复/关闭。([链接](https://github.com/nearai/ironclaw/issues/4536))
- **(中等) [Issue #4556]:** **Production: Telegram creates a new conversation after upgrade**。代理升级后，Telegram 通道会创建新会话而非继续原有会话，干扰用户的连续对话体验。**状态：** 未修复，等待评估。([链接](https://github.com/nearai/ironclaw/issues/4556))
- **(中等) [Issue #4554]:** **Incomplete i18n coverage and translator runtime crashes**。WebUI v2 国际化覆盖不全，部分区域仍为硬编码英文，且翻译器在运行时可能崩溃。**状态：** 未修复，问题已提交。([链接](https://github.com/nearai/ironclaw/issues/4554))
- **(轻微) [Issue #4557]:** **Some hosted agents return 403 Forbidden while instance remains running**。某些托管代理在实例运行状态下返回 403 错误，但能自动恢复。**状态：** 未修复，需排查根本原因。([链接](https://github.com/nearai/ironclaw/issues/4557))

---

#### 6. 功能请求与路线图信号

昨日提交的 Issues 中，涌现出对 **产品级运维和开发者体验** 的强烈需求，预示着项目下一阶段的发展方向。

- **运维与开发者体验 (Epic):**
    - **[Issue #4533] Epic: Reborn operator setup, config, diagnostics, and service lifecycle**。明确提出了让 Reborn 替代 V1 作为运营二进制文件所需的一系列功能，包括设置、配置、检查和本地服务生命周期管理。这标志着项目正式将 Reborn 的稳定运营和用户友好作为高优先级事项。([链接](https://github.com/nearai/ironclaw/issues/4533))
    - **[Issue #4545] [EPIC] Self-serve secret setup and grants for user-generated tools**。用户希望对用户生成的功能/工具进行自助式的密钥管理，这是增强平台安全性和易用性的关键一步。([链接](https://github.com/nearai/ironclaw/issues/4545))
    - **[Issue #4539] Epic: Reborn approvals parity**。用户希望在 Reborn 中获得与 V1 同等的审批功能，表明用户对 Reborn 替代 V1 的期待不仅仅是基础功能，还包括完整的操作流程。([链接](https://github.com/nearai/ironclaw/issues/4539))

- **高级功能需求:**
    - **[Issue #4543] Runtime service profiles for credentialed generic HTTP**。用户希望在运行时为泛型 HTTP 调用配置凭据（如 Stripe API Keys），表明 IronClaw 正被用于更复杂的、需要第三方 API 身份验证的场景。([链接](https://github.com/nearai/ironclaw/issues/4543))
    - **[Issue #4585] Reborn auth evidence should carry tenant identity**。需求来自代码审查，要求认证凭证携带租户身份信息，以实现租户感知的验证，这是一个重要的安全增强。([链接](https://github.com/nearai/ironclaw/issues/4585))

**趋势分析：**
项目路线图正在从“核心功能迁移”向“运营就绪和用户体验完善”迈进。开发者不仅关注新架构能否运行，更关注它能否被高效、安全地部署、配置、监控和使用。

---

#### 7. 用户反馈摘要

从昨日提交的 Issues 评论中可以提炼出以下用户痛点：

- **工具实用性：** 用户对工具的行为有很高期望。例如，Google Calendar 工具默认显示过去事件的行为被社区成员 [BenKurrek] 发现并提出 Issue，而核心团队在数小时内就提供了修复 PR ([#4578])，体现了对用户反馈的积极回应。
- **兼容性敏感：** 用户对与第三方服务的兼容性非常敏感。Codex 模型被隐藏、DeepSeek 请求失败等问题，直接影响了用户对不同模型和提供商的使用。用户 [darren2013] 详细分析了 DeepSeek 400 错误的原因，显示了社区成员具备深度排障能力。
- **升级体验待优化：** 用户 [sunglow666] 报告的 Telegram 升级后会话断裂问题，是典型的升级体验不佳场景。这表明项目需要为通道提供更平滑的迁移/升级方案。
- **UI 与国际化：** 用户 [italic-jinxin] 确认了 WebUI v2 的国际化问题，并报告了运行时崩溃。这表明产品在拥抱全球用户时，还需要在基础 UI 健壮性上付出更多努力。
- **OAuth 登录至关重要：** 用户 [italic-jinxin] 报告的 OAuth 用户无法聊天的问题（#4536）是典型的阻塞性问题，虽然已修复，但其严重性表明了 SSO 功能对于产品生产环境部署的重要性。

---

#### 8. 待处理积压

以下长期开放的重要 Issue/PR 需要维护者关注：

- **[Issue #3026] Epic: Reborn production wiring and cutover readiness (P0, reborn)**。这是 Reborn 生产就绪的关键史诗任务，已开放一个多月，目前仍在进行中。它关联大量子任务，是项目当前第一优先级。建议维护者定期更新进度并同步关键依赖。([链接](https://github.com/nearai/ironclaw/issues/3026))
- **[Issue #3283] Migrate OpenAI-compatible chat and Responses APIs onto Reborn**。与上面类似，同样是 Reborn 的核心里程碑。虽然昨日有大量相关 PR，但整个 Issue 的完成度仍需关注。([链接](https://github.com/nearai/ironclaw/issues/3283))
- **[Issue #4108] Nightly E2E failed**。持续多日的 Nightly E2E 测试失败是一个严重信号。虽未直接归因于某个 Bug，但它表明代码库稳定性可能存在隐患，需要维护者立即排查根因并修复 CI 管道。([链接](https://github.com/nearai/ironclaw/issues/4108))

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的 LobsterAI (netease-youdao/LobsterAI) GitHub 数据，生成一份结构清晰的 2026-06-09 项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-06-09

### 1. 今日速览

今日项目活跃度极高，核心聚焦于功能开发与基础设施的稳定性与体验优化。虽然无新版本发布，但共有 **19 条 PR 更新**，其中 **18 条已合并/关闭**，表明开发团队正在进行一次集中的清理与迭代。关键进展包括：推出了用户数据备份与恢复的重大功能，优化了桌面端的登录流程，并修复了多个长期存在的 Bug（如 IM 通知失效、日志导出超时等）。整体来看，项目正积极提升用户数据安全、认证体验与系统健壮性。

### 2. 版本发布

无

---

### 3. 项目进展

今日合并/关闭了多项重要 PR，主要集中在**数据管理、认证流程和平台修复**三个方向，项目在功能完整性和用户体验上迈进了坚实一步。

- **用户数据备份与恢复 (Data Migration)**
    - **PR #2125** [已合并] 新增了用户数据备份与恢复功能，允许将数据打包为便携式 tar 包并通过重启进行恢复，且支持回滚。这是数据安全方面的重要里程碑。
    - **PR #2126** [已合并] 优化了恢复逻辑，确保运行时锁文件（如 SingletonLock）不被覆盖，提升软件稳定性。
    - **PR #2128** [已合并] 修复了备份中错误包含 `Network` 目录的问题，并确保该目录在恢复时被保留，避免网络配置丢失。

- **桌面端认证流程优化 (Auth)**
    - **PR #2122** [已合并] 引入了基于本地回环地址 (localhost) 的回调登录流程，旨在避免浏览器弹出的“外部应用确认”对话框，简化登录过程。
    - **PR #2127** [已合并] 修复了 Windows 系统下登录后的窗口焦点问题，通过短暂置顶窗口来确保桌面应用能被顺利切换到前台。
    - **PR #2129** [已合并] 增加了登录回调的诊断日志，有助于快速定位 Windows 开发模式下回调失败的根因。

- **其他重要修复与功能**
    - **PR #1526** [已关闭] 为协作模块的会话列表添加了7种颜色标注功能，提升用户对会话的视觉区分和管理效率。
    - **PR #1522** [已关闭] 在设置中增加了从供应商 API 动态拉取模型列表的功能，用户无需手动添加，即可发现新上线的模型。
    - **PR #1524** [已关闭] 模型配置测试连接失败的错误信息从笼统的“连接失败”升级为包含网络、鉴权、速率限制等具体原因的详细提示。

---

### 4. 社区热点

由于今日关闭的 PR 大多超期未更新，且评论数据缺失，热点主要集中在由开发者提出的、影响广泛的功能与修复。

与会话管理相关的 UI 优化 (#1526) 和连接测试的详细错误提示 (#1524) 均是为了解决用户在日常使用中的普遍痛点，预计它们将成为社区的积极讨论点。

---

### 5. Bug 与稳定性

今日修复了一批显著的 Bug，按严重程度排列如下：

- **高度**
    - **IM 通知静默失败** [PR #1510 - 已合并]: 用户创建定时任务后，若未选择 IM 通知会话，通知会静默失败。现已修复，表单提交时会强制校验通知目标。
    - **日志导出超时** [PR #1515 - 已合并]: 导出的日志文件因压缩耗时过长导致超时。已升级压缩库并优化压缩逻辑，解决了此问题。
- **中度**
    - **QQ Bot 白名单无法配置** [PR #1514 - 已合并]: QQ Bot 群组白名单功能的 UI 缺少输入框，导致功能形同虚设。现已修复，补齐了必要的界面元素。
    - **GitHub Copilot 认证 Token 丢失** [PR #1517 - 已合并]: 用户在 OAuth 认证轮询期间关闭设置面板，会导致认证成功后 Token 丢失。现已通过 `useEffect` cleanup 机制取消轮询。
    - **OpenClaw 网关误重启** [PR #1521 - 已合并]: 修复了因“技能变更”信号导致 OpenClaw 网关异常重启的问题，提升了底层服务的稳定性。

---

### 6. 功能请求与路线图信号

- **用户数据备份与恢复 (PR #2125)**: 该功能的实现表明开发者非常重视用户数据安全与迁移场景，极可能成为下一版本的核心亮点。
- **动态模型列表 (PR #1522)**: 该功能的实现表明项目在尝试解决“模型碎片化”和“配置繁琐”的痛点，未来可能进一步集成更多云服务的自动发现能力。
- **会话颜色标注 (PR #1526)**: 这是一个典型的用户反馈驱动的功能，预示着项目在协作体验上正进行精细化打磨，可能出现在近期的更新中。

---

### 7. 用户反馈摘要

从今日被关闭的 Issues 和 PR 摘要中，可以提炼出以下用户反馈：

- **痛点明确**: “定时任务的 IM 通知静默失败”，这直接导致用户认为任务配置成功，但实际未收到通知，造成信任危机。
- **功能缺失**: “QQ Bot 白名单无法配置”，UI 不完整导致核心管理功能无法使用，属于明显的功能不完整。
- **体验不佳**: “导出日志超时”和“GitHub Copilot Token 丢失”直接影响了专业用户的故障排查和第三方工具集成流程。
- **满意之处**: “测试连接错误详情”的改进和“动态模型列表”的引入，均体现了对用户日常操作体验的重视。

---

### 8. 待处理积压

- **PR #1277** [状态: **打开**] chore(deps-dev): bump the electron group across 1 directory with 2 updates
    - 该 PR 由 `dependabot[bot]` 自动创建于 2026-04-02，旨在升级 Electron 及其构建工具。虽已更新（2026-06-08），但至今仍处于打开状态。鉴于 Electron 版本升级可能带来破坏性变更或安全修正，建议维护者优先关注并合并它。
    - 链接: https://github.com/netease-youdao/LobsterAI/pull/1277

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyClaw 项目动态日报 — 2026-06-09

## 1. 今日速览

- 过去24小时内 **无新 Issue 提交或关闭**，社区讨论热度极低，项目处于“相对静默”状态。
- **唯一活跃的贡献** 是对构建流程的改进：PR #280 为 `better-sqlite3` 原生模块添加了自动重建脚本，减少用户手动操作，属于开发者体验（DX）优化。
- 无新版本发布，无 Bug 报告，无功能请求，项目整体健康度稳定但缺乏新动向。
- 活跃度评估：**低**（1条未合并 PR，0 Issue 交互）。
- 建议维护者关注长期积压的 Issue 或提前规划下一版本功能。

## 2. 版本发布

无。

## 3. 项目进展

### 待合并 PR（关键贡献）
- **#280 [OPEN] fix(install): add postinstall script to auto-rebuild better-sqlite3**  
  作者：dsy122 | 创建：2026-06-08 | 更新：2026-06-08  
  链接：https://github.com/TinyAGI/tinyagi/pull/280

  - **摘要**：在 `npm install` 后自动执行 `npm rebuild better-sqlite3`，消除用户手动重建原生 C++ 模块的需要。`better-sqlite3` 依赖 Node.js 原生编译环境，新安装时容易因预编译产物缺失报错，此 PR 通过 `postinstall` 钩子自动触发编译。
  - **项目推进**：  
    - 提升首次安装成功率，降低新手使用门槛。
    - 若合并，将使安装流程更自动化，减少 Issue 中关于“模块加载失败”的求助。
  - **状态**：尚未合并，需维护者审查兼容性及对 CI 构建时间的影响。

## 4. 社区热点

今日无活跃讨论的 Issue/PR。PR #280 目前 **0 条评论、0 个 👍**，尚未引起社区注意。社区整体沉寂，无热点话题。

## 5. Bug 与稳定性

- **新增 Bug：0**  
  过去24小时内未报告任何崩溃、回归或功能异常。
- **稳定性提示**：虽然无新 Bug，但 PR #280 的背景暗示了 `better-sqlite3` 在安装阶段存在已知的“预编译产物缺失”问题（常见于纯 Node.js 环境）。该问题已在 PR 中提出修复方案，但尚未合并，因此当前版本仍可能受此影响。

## 6. 功能请求与路线图信号

- **无新功能请求**。  
- **从 PR #280 判断**：维护者/贡献者正在优化开发者体验（DX），可能暗示下一版本将重点解决**安装流畅性**和**跨平台兼容性**。建议后续关注是否引入类似 `packageManager` 或 Docker 开发容器配置。

## 7. 用户反馈摘要

- 由于过去24小时 **无 Issue 评论**，无法提炼直接用户反馈。  
- 间接反馈来自 PR #280 的描述：用户“在全新安装时遇到错误”，原因是 `better-sqlite3` 的预编译包缺失。这表明部分用户期望“零配置安装”，对原生模块的自动构建有较高要求。

## 8. 待处理积压

- **PR #280**（未合并）是当前最需要关注的代码变更，但因无讨论和评审，可能被忽视。建议维护者尽快审查并确认是否合并，或与贡献者沟通修改建议。  
- 除此之外，无其他长期未响应的 Issue 或 PR 记录。建议定期扫描仓库中已打开但近30天无更新的 Issue，防止问题积压。

---

**数据来源**：TinyClaw 项目 GitHub 仓库 [TinyAGI/tinyagi](https://github.com/TinyAGI/tinyagi)  
**生成时间**：2026-06-09 07:00 UTC

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，以下是为您生成的CoPaw项目2026年6月9日动态日报。

---

# CoPaw (github.com/agentscope-ai/CoPaw) 项目日报

**日期:** 2026-06-09

## 1. 今日速览

过去24小时内，CoPaw项目保持了极高的社区活跃度，共产生42条Issue和43条PR更新。虽然项目没有发布新版本，但Issue和PR的处理量（关闭/合并数量各约半）表明核心开发者与社区贡献者均在高效推进工作。社区讨论热度主要集中在**后端向AgentScope 2.0迁移的破坏性变更**、**借鉴Hermes Agent等竞品的学习循环特性**以及**微信/钉钉等多渠道的稳定性问题**上。总体而言，项目处于功能迭代与稳定性加固并行的高强度开发阶段，社区生态充满活力。

## 3. 项目进展

今日完成了多项重要的功能推进和Bug修复，项目整体稳健向前。以下为已合并/关闭的关键PR和Issue，体现了项目在多方面的进展：

- **钉钉频道稳定性提升**：PR #4932 已被合并，修复了因`conversation_id`后缀冲突导致的跨用户消息错误合并问题，提升了钉钉通信的可靠性。
- **安全加固**：PR #5028（已合并） 将Keychain主密钥与安装实例绑定，解决了同一机器上不同安装实例共享密钥的安全风险。
- **基础架构与开发者体验**：
    - PR #4997 合并，为前端引入了统一的插件扩展点注册机制（菜单、路由、UI插槽），为插件生态繁荣奠定了基础。
    - Issue #4340 关闭，完成了核心运行层 (`app/runner` 和 `app/routers`) 的单元测试覆盖，提升了代码质量和可维护性。
- **Bug修复**：
    - PR #5021 修复了`active_model`未设置时，`/compact`命令和自动压缩功能无法使用正确模型最大输入长度的问题，解决了内存压缩生效的障碍。
    - Issue #4587、#4585、#4877、#4918 等多个关于进程残留、工具自动发现、MCP工具名包含"."的Bug被关闭，表明项目正在系统地清理积压问题。

## 4. 社区热点

今日社区讨论最热烈的议题反映了用户对项目未来发展方向和技术细节的高度关注。

1.  **【Feature Request】借鉴 Hermes Agent 学习循环 (Issue #5017)**：这是目前社区呼声极高的一个功能建议，收获了2个👍和7条评论。用户认为QwenPaw拥有出色的本地化和开箱即用体验，但建议关注并借鉴Hermes Agent的“学习循环”机制，让Agent能够从自身行为中自动创建和迭代技能。这反映了社区对提升Agent自主学习和进化能力的迫切需求，是项目未来可能的重要演进方向。

2.  **【Breaking Change】后端迁移至AgentScope 2.0 (Issue #4727)**：此议题获得2个👍和6条评论，是一个影响深远的重大决策。讨论集中在对新架构的期待、迁移的复杂性以及对现有插件、工具兼容性的担忧。这标志着项目正在进行一次关键的技术栈升级，以确保长期的技术先进性和可扩展性。

3.  **【Bug】阿里coding plan模型卡死 (Issue #5003)**：该问题有7条评论，表明特定模型提供商和特定功能组合下的稳定性问题是用户日常使用中的一个痛点。用户希望QwenPaw能够更好地适配和兼容国内的主流模型服务。

## 5. Bug 与稳定性

过去24小时报告的Bug涵盖多个方面，其中一些已有了对应的修复PR，反映了项目对稳定性的高度重视。

| 严重程度 | Bug 标题 | Issue链接 | 状态 | 修复PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | 阿里 coding plan 使用 Qwen3.7-plus 一直卡住 | [#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003) | 活跃 | 无 |
| **高** | MCP服务器进程在重启后堆积，导致控制台加载缓慢 | [#4834](https://github.com/agentscope-ai/QwenPaw/issues/4834) | 活跃 | **PR #5014 (Open)** |
| **高** | 内存压缩时出现`AttributeError: 'str' object has no attribute 'get'`导致崩溃 | [#5019](https://github.com/agentscope-ai/QwenPaw/issues/5019) | 已关闭 | 已修复 |
| **中** | Web Console多Agent聊天不稳定，新聊天无法可靠注册/显示 | [#5016](https://github.com/agentscope-ai/QwenPaw/issues/5016) | 活跃 | 无 |
| **中** | KimiCode API的思考过程（Thinking）不显示 | [#5013](https://github.com/agentscope-ai/QwenPaw/issues/5013) | 活跃 | 无 |
| **中** | 图片预览放大后拖动出现异常抖动 | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | 活跃 | 无 |
| **低** | `loop_config.json` / `prd.json`损坏导致整个Agent会话崩溃 | [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) | 活跃 | 无 |

## 6. 功能请求与路线图信号

今日用户提出的功能请求具有很高的参考价值，结合已有的PR，可以看到项目未来增强的清晰轮廓：

- **Agent能力进化**：请求“记忆系统自进化”(#4994) 和引入Hermes Agent的“学习循环”(#5017)，表明用户不满于当前静态的技能模式，希望Agent能像人一样从经验中学习。这将是下一阶段智能体能力的核心竞争点。
- **多模态处理优化**：“支持独立视觉模型配置”（Visual Model Fallback, #4992）获得了社区支持。这显示用户需要在主模型不具备多模态能力时，系统能灵活调用另一个视觉模型处理图片，对系统架构的灵活性提出了更高要求。
- **用户体验增强**：请求“在工具调用后抑制最终文本回复”(#4838) 和“支持9router模型接入”(#5001) 都是针对特定使用场景的细节优化。**PR #5023 (Open)** 计划增加的“插件市场”标签页，与社区对“集百家之长”的呼声相呼应，将直接提升插件生态的可用性。
- **未来架构与迭代**：**PR #5027 (Open)** 旨在清理后端预热会话对用户界面的污染，并支持会话恢复，这是对`paw` TUI等高级客户端的体验优化。**PR #4443 (Open)** 的`/goal`轻量级目标模式，为会话级任务管理提供了新的思路。

## 7. 用户反馈摘要

从Issue评论中提炼的真切用户反馈，揭示了项目的优势与待改进之处：

- **正面反馈**：用户在提出“借鉴Hermes Agent”建议时，首先肯定了QwenPaw“**国内用起来特别舒服——本地化做得很到位，设置清晰无门槛，开箱即用**”。这表明本地化体验是项目的核心优势之一。
- **用户痛点**：
    - **WeChat iLink通道稳定性堪忧**：用户报告`context_token`过期无重试逻辑、文件发送失败无日志等问题(#4477)，严重影响了日常使用的可靠性。
    - **多渠道一致性问题**：用户反馈自研插件在桌面端聊天界面可自动发现，但在企业微信渠道会话中无法自动调用(#4585)，凸显了不同渠道间功能一致性的难题。
    - **进程管理混乱**：多次重启后MCP进程堆积(#4834)、QwenPaw关闭后遗留后台进程(#4587)等问题，给用户造成了系统资源浪费和体验割裂感。
    - **“Pet”功能体验不佳**：用户反馈Pet功能“**闪退、卡顿严重，体验极差**”(#5029)，建议在稳定前标注为实验性功能，这关系到产品对用户第一印象的塑造。

## 8. 待处理积压

以下为长期未解决或需要维护者高度关注的重要议题，可能成为影响项目健康度的风险点：

1.  **GPT-5.x模型`max_tokens`参数错误 (Issue #2777)**：该问题自2026年4月1日提出至今，已超过两个月仍处于开放状态。涉及硬编码模型列表和对新版OpenAI API的兼容性，需要尽快评估和修复，以保证主流模型提供商的支持能力。
    [Issue链接](https://github.com/agentscope-ai/QwenPaw/issues/2777)

2.  **后端迁移至AgentScope 2.0 (Issue #4727)**：作为一个破坏性变更，该议题虽然有更新的PR在讨论，但其本身就是一项长期、高风险的任务。社区对此充满期待但也存在担忧。需要持续跟踪其方案设计、迁移计划和向后兼容性策略，并定期同步进度，以管理社区预期。 [Issue链接](https://github.com/agentscope-ai/QwenPaw/issues/4727)

3.  **MCP服务器进程累积 (Issue #4834)**：尽管已有修复PR #5014，但其开放状态仍需关注。此问题直接影响了用户对服务稳定性和资源占用的感知，是影响体验的关键点，应推动其尽快合入。 [Issue链接](https://github.com/agentscope-ai/QwenPaw/issues/4834)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为一名专注于AI智能体与个人AI助手领域的开源项目分析师，我将根据您提供的ZeroClaw项目数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

### **ZeroClaw 项目动态日报 (2026-06-09)**

#### **1. 今日速览**

ZeroClaw 项目今日继续保持极高的社区活跃度，过去24小时内产生了50条Issue和50条PR，数量可谓巨大。项目目前正处于密集的功能开发与稳定性修复并行阶段，合计39条待合并PR表明维护团队任务繁重，同时也有2个严重Bug（一为S1关键，一为S1阻塞）在今日被关闭，是值得肯定的积极信号。高优先级（P1）的Bug报告和处理中（in-progress）的问题占据了显著比例，建议关注交付质量与合并速度之间的平衡。

#### **2. 版本发布**

无新版本发布。

#### **3. 项目进展**

今日有11个功能或修复被合并/关闭，推进了项目在重要领域的进展：

- **修复与稳定性**：
    - **[PR #7403] (已关闭) - 修复运行时空对话崩溃**：修复了`trim_history`在孤立消息清理级联后可能清空所有消息的边界情况，通过在检测到消息将被清空时跳过修剪，确保会话不会因空消息数组而崩溃。这是对运行时稳定性的重要修补。
    - **[PR #7388] (已关闭) - Matrix频道会话隔离**：成功解决了**Issue #6487**（一个曾标记为P0阻塞器的问题）。现在，同一守护进程下的多个Matrix频道实例将使用独立的会话存储路径，有效防止了会话相互覆盖和消息发送错乱的问题。这是一个关键的破坏性变更，需要通过会话迁移来解决。

- **重大功能推进**：
    - **[PR #6148] (已关闭) - 智能房间ESP32演示**：这是一个重要成果，完成了一个从手机（Telegram）到ZeroClaw再到ESP32硬件的端到端演示项目。这标志着ZeroClaw从纯软件代理向物理世界交互（IoT）迈出了实质性的一步，展示了项目在硬件控制领域的潜力。

- **其他合并/关闭的PR**：
    - **[PR #7365] (待合并)** - 重写官方文档，从源码生成配置/提供商说明，提升文档的准确性和可维护性。
    - **[PR #7404] (待合并)** - 修复Matrix频道的同步超时问题，防止因忙碌轮询导致的资源浪费和网关错误。

#### **4. 社区热点**

今日讨论最热烈的议题主要集中在核心功能BUG和重大新特性的RFC提案上。

- **`tool_filter_groups` 对真实MCP工具失效** (`#6699`，7条评论)：这是社区发现的一个高优先级Bug，表明用于过滤工具的`tool_filter_groups`配置项对于真正的MCP（Model Context Protocol）工具完全不起作用。社区成员深入分析了代码逻辑错误（前缀匹配Bug）和与延迟加载机制的集成问题，这是许多依赖该功能配置多工具代理的用户的核心痛点。
- **计算机使用（Computer-use）功能RFC** (`#6909`，6条评论)：该RFC提议让ZeroClaw具备截屏和控制鼠标键盘的能力，以实现桌面自动化。有6条评论表明社区对“Computer-use”能力有强烈需求，特别是希望追赶OpenAI Codex等先行者的功能。
- **记忆系统（Memory）权重过大** (`#5844`，5条评论)：用户反馈在定时任务（cron job）中，系统提示词过度强调历史记忆而忽略当前Prompt，导致任务执行偏离预期。这反映了代理的记忆管理机制在实际生产环境中（特别是自动化场景）存在设计上的缺陷。

#### **5. Bug 与稳定性**

今日报告了多个严重Bug，主要集中在运行时安全、插件系统和特定提供商兼容性上。

- **严重程度: 数据丢失/安全风险 (S0)**：
    - **无新报告**。但一个重要修复`file_write`问题（`#4627`）的相关PR `#7129` 今日仍在更新，该PR旨在彻底解决文件写入工具在临时工作区静默失败的问题。

- **严重程度: 工作流阻断 (S1)**
    - **[#6434] Shell工具在`full`自治模式下被拒绝**：一个令人困惑的行为，即使在最宽松的配置下，Shell工具也无法被调度执行。目前状态为`in-progress`，亟待修复。
    - **[#6361] MiniMax提供商工具循环**：上下文压缩功能会丢失关键的`assistant(tool_calls)`和`tool(result)`消息，导致与OpenAI兼容提供商（如MiniMax）的多轮工具对话陷入死循环。

- **严重程度: 行为降级 (S2)**
    - **[#6254] WASM插件路径不一致**：`plugin install`和`agent runtime`扫描插件的路径不同，导致已安装的WASM插件对代理不可见。虽有`in-progress`标签，但长期存在，影响插件生态的可用性。
    - **[#6350] WhatsApp频道号码白名单绕过**：针对LID联系人的消息过滤失效，导致本应被阻止的消息被静默丢弃。这是一个让安全配置形同虚设的Bug。

*注：另有2个Bug（`#6487`, `#6225`）于今日关闭。*

#### **6. 功能请求与路线图信号**

今日涌现了大量架构级别的RFC，暗示v0.9.0版本可能是一次重大的安全性、可扩展性和配置管理能力升级。

- **安全性增强（可能纳入v0.9.0）**：
    - **可插拔安全接口** (`#7142`): 提议将安全执行、报告和事件响应抽象为单一`trait`接口，使安全策略可插拔。
    - **OIDC认证支持** (`#7141`): 为守护进程和网关添加OpenID Connect认证支持，是企业级部署的关键能力。
    - **高级Shell策略** (`#7155`): 增加“执行前需确认”的中间级，以及类似Claude Code的通配策略（允许/询问/拒绝），提升高风险操作的精细控制。

- **配置与易用性增强**：
    - **将翻译文件分离到Git子模块** (`#7184`): 将非英语的`.ftl`和`.po`文件移出主仓库，解决翻译提交导致的git历史混乱问题。
    - **[PR #7267] MCP服务器配置编辑**：通过`#[natural_key]`支持在网页仪表盘中对MCP服务器配置进行逐字段编辑，告别JSON粘贴板。

#### **7. 用户反馈摘要**

- **痛点**：
    - **配置项不生效**：用户`perlowja`指出`[runtime_profiles.*].max_tool_iterations`配置项完全不起作用，正确的配置位置在`[agents.*]`下，表明文档和实现之间存在差距。
    - **记忆系统过重**：用户`databillm`在使用cron job时频繁发现代理更倾向于遵守旧记忆而非当前指令，导致任务执行不符合预期，代理的“记忆力”反而成了障碍。
    - **Gemini OAuth流程断裂**：用户`nrpx`在成功进行Gemini CLI的OAuth认证后，紧接着就遇到API限速错误，认证流程的健壮性受到质疑。
    - **Feishu集成默认行为错误**：用户`yaoyunnuo`反馈，集成飞书后，默认调用的是LLM（大模型）而不是Agent（智能体），这从根本上违背了集成意图。

- **期望**：
    - **智能消息截断**：用户`egorsmkv`希望Telegram频道能增加智能截断功能，以尊重Markdown结构，避免代码块被截断得面目全非。
    - **本地优先模式**：用户`ThirDecade2020`强烈希望ZeroClaw能提供一种针对小模型的紧凑、本地优先模式，以减少prompt膨胀和内部指令泄露。

#### **8. 待处理积压**

部分重要问题长期未解决，可能成为项目健康度的隐患。

- **[#6074] 审计：追踪153个丢失的提交**：由于之前的批量回滚，153个已合入的commit（包含bug修复和功能）丢失。该Issue自4月24日提出，至今仍标记为`in-progress`，但无实质进展。**这个代码库的完整性和历史回溯问题值得维护者高度关注。**
- **[#3767] 跨渠道TOTP门控**：三月提出，为关键命令添加跨渠道TOTP二次验证。这对安全场景至关重要，但目前只有2条评论，缺乏实质性推进。
- **[#4467] MCP资源与提示支持**：用户期望ZeroClaw成为一个完整的MCP客户端，而不仅仅是工具客户端。该功能请求在社区中有4个👍，但相关PR `#7267`才刚刚提出合并。此功能的实现将显著提升ZeroClaw的生态位。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*