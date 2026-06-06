# OpenClaw 生态日报 2026-06-06

> Issues: 467 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-06-06 02:31 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw 项目 GitHub 数据，我为您生成了 **2026-06-06** 的项目动态日报。

---

## **OpenClaw 项目日报 | 2026-06-06**

### **今日速览**

今日 OpenClaw 项目展现出极高的社区活跃度，24小时内产生了超过 950 条 Issues 和 PR 互动。虽然社区讨论热烈，修复和功能贡献频繁（特别是针对 v2026.6.1 的回归问题），但 **P1 级别的严重 Bug 和持续存在的回归问题依然突出**，包括 Coding Agent 不完成任务、升级后性能严重退化及多个通道的消息丢失问题。此外，大量 PR 处于待合并状态（364 条），显示项目维护效能面临压力。整体来看，项目正处于一个 **“高活跃度、高修复投入，但稳定性风险较大”的调整期**。

### **版本发布**

无。

### **项目进展**

尽管存在稳定性挑战，今天仍有多个关键修复和功能改进通过 PR 成功合并，提升了项目健壮性和用户体验。主要进展包括：

- **内存与稳定性修复**：
    -   **PR #90748** (已合并): 修复了 `openclaw memory status` 命令在索引成功后仍显示“空白期望”模型的 Bug，解决了模型适配器的默认模型解析问题。这确保了记忆功能的状态报告准确性。
        [链接](https://github.com/openclaw/openclaw/pull/90748)
    -   **PR #90736** (已合并): 修复了 macOS 节点模式在健康网关会话中可能“静默重连”的 Bug，通过缓存 TLS 钉选 WebSocket 会话对象，避免了不必要的重连通知和资源消耗。
        [链接](https://github.com/openclaw/openclaw/pull/90736)
    -   **PR #90620** (已合并): 修复了 Twilio 语音通话 `stale reaper` 可能错误地结束正在进行中的通话（`speaking`/`listening` 状态）的 Bug，保证了实时语音通话的稳定性。
        [链接](https://github.com/openclaw/openclaw/pull/90620)

- **核心逻辑与用户体验**：
    -   **PR #90773** (已关闭): 修复了自动压缩（`auto-compaction`）在释放提示锁期间可能丢失写入的问题，确保了会话 JSONL 记录的一致性。
        [链接](https://github.com/openclaw/openclaw/pull/90773)
    -   **PR #90772** (已关闭): 引入了一个“路由守卫”的初步修复，旨在防止消息被错误路由，尽管该 PR 还在等待实机行为证明。
        [链接](https://github.com/openclaw/openclaw/pull/90772)
    -   **PR #90809** (已关闭): 改进了 TUI (终端用户界面) 在加载模型列表时的反馈，从“无响应”变为显示“加载中”状态，提升了用户体验。
        [链接](https://github.com/openclaw/openclaw/pull/90809)

### **社区热点**

今日最受关注的议题集中在**版本升级后的功能退化**和**对核心 AI Agent 行为的期望**上。

1.  **Coding Agent 完全失效 (Issue #62505, 14 条评论)**:
    -   **诉求**: 用户 `drpau` 反馈，其专门用于编码的 Agent 在升级后“什么都不做”，只给出模糊的状态更新和道歉。这是一个影响重大的回归问题，得到了社区的共鸣和关注，被标记为 `P1` 和 `regression`。
    -   **链接**: [openclaw/openclaw Issue #62505](https://github.com/openclaw/openclaw/Issue/62505)

2.  **升级后性能严重退化 (Issue #76562, 13 条评论)**:
    -   **诉求**: 用户 `Nsch11` 报告从 v2026.4.24 升级到 v2026.4.29/v2026.5.2 后，CPU 接近 100%，控制面 RPC 延迟极高，系统不稳定。该问题获得了 5 个 👍，说明此性能回归在社区中影响范围很广。
    -   **链接**: [openclaw/openclaw Issue #76562](https://github.com/openclaw/openclaw/Issue/76562)

3.  **MCP 工具调用审批机制 (Issue #78308, 12 条评论)**:
    -   **诉求**: 用户 `oalterg` 提出了一个重要的安全特性请求：希望 MCP 服务器能像 Shell 执行一样，通过统一的 `/approve <id>` 管道实现人工审批。这反映了社区对有状态、高权限工具调用的安全控制需求。
    -   **链接**: [openclaw/openclaw Issue #78308](https://github.com/openclaw/openclaw/Issue/78308)

### **Bug 与稳定性**

今日报告的 Bug 中，**回归问题（Regression）** 是绝对的重灾区，特别是围绕 v2026.6.1 版本。以下为严重程度排列的关键问题：

-   **P1 / 严重**:
    -   **[Bug] (已关闭)**: Mattermost 斜杠命令在 v2026.4.15 返回 503 (Issue #68113) - 已关闭，问题已解决。
        [链接](https://github.com/openclaw/openclaw/Issue/68113)
    -   **[Bug]**: Coding Agent 从 v2026.4.2 后不再完成任何工作 (Issue #62505) - 开放中，待维护者介入。
        [链接](https://github.com/openclaw/openclaw/Issue/62505)
    -   **[Bug]**: 服务器升级后 CPU 占满、控制面延迟极高 (Issue #76562) - 已关闭，或已找到临时解决方案。
        [链接](https://github.com/openclaw/openclaw/Issue/76562)
    -   **[Bug]**: OpenAI gpt-5.4/gpt-5.5 在 v2026.6.1 上认证失败 (Issue #90083) - 开放中，是 6.1 版本的核心障碍之一。
        [链接](https://github.com/openclaw/openclaw/Issue/90083)
    -   **[Bug]**: v2026.6.1 原生回复导致后续对话失败 (Issue #90093) - 开放中，影响使用特定 GPT 模型的用户。
        [链接](https://github.com/openclaw/openclaw/Issue/90093)
    -   **[Bug]**: v2026.6.1 升级时 SQLite 迁移错误地清除了 44/45 个 Cron 任务 (Issue #90072) - 已关闭，属于关键数据丢失问题。
        [链接](https://github.com/openclaw/openclaw/Issue/90072)
    -   **[Bug]**: v2026.6.1 中 Matrix 频道消息派发完全损坏 (Issue #90325) - 开放中，影响 Matrix 用户的基础功能。
        [链接](https://github.com/openclaw/openclaw/Issue/90325)

-   **P2 / 重要**:
    -   [Bug] (新): `launchd plist` 硬编码错误，导致所有网关 stderr 被丢弃 (Issue #90711)
        [链接](https://github.com/openclaw/openclaw/Issue/90711)
    -   [Bug]: 飞书 (Feishu) 频道启用流式卡片后，内容被截断至最后一个字符 (Issue #88929)
        [链接](https://github.com/openclaw/openclaw/Issue/88929)
    -   [Bug]: Telegram 话题中的心跳事件会 “吞掉” 正在进行的用户回复 (Issue #64810)
        [链接](https://github.com/openclaw/openclaw/Issue/64810)

**Fix PR 快照**：上述开放 Bug 中，**目前尚无直接的、已合并的修复 PR**。但今日合并的 PR #90736 (macOS重连) 和 PR #90773 (自动压缩写入) 等，修复了另一些不同但同样影响稳定性的问题，体现了维护团队正在努力解决积压问题。

### **功能请求与路线图信号**

今日涌现的功能请求显示了项目未来的发展方向，主要聚焦于**更精细的上下文控制**、**更强的安全模型**和**更好的可观察性**。

-   **分层配置文件加载 (Issue #22438)**: 用户请求按层级（如全局、Agent、会话）加载配置文件，以优化 LLM Token 消耗，避免将无关文件加载到所有会话中。这表明社区对成本优化和上下文窗口管理有强烈需求。
-   **MCP 工具调用审批通道 (Issue #78308)**: 请求为 MCP 工具调用引入类似 Shell 执行的人工审批管道。这是一个强烈的安全特性信号，预示着更细粒度的权限控制可能进入路线图。
-   **按 Agent 隔离记忆维基 (Issue #63829)**: 支持为多 Agent 系统中的每个 Agent 配置独立的记忆维基，而不是共享一个全局知识库。这反映了用户对多 Agent 场景下知识隔离的要求。
-   **保障上下文中的原始消息 (Issue #58818)**: 希望即使在会话压缩或重置后，Agent 也能保留最近的 N 条原始消息。这直接关系到 Agent 的短期记忆和对话连续性。
-   **会话最大时长与 Token 上限配置 (Issue #64463)**: 用户请求增加硬性限制，以阻止因 Agent 失控或长时间运行导致的成本无限制累积。
-   **WebChat 用户界面优化 (Issue #90246)**: 请求允许隐藏或折叠工作区/文件面板。这是一个用户体验的微调请求，表明 UI 定制化也是社区关心的一个点。

结合今日合并的 PR #78441（子代理工具转发），未来版本的路线图很可能围绕**更智能的上下文管理**、**更可靠的多Agent架构**和**更安全的执行沙箱**展开。

### **用户反馈摘要**

从今日的 Issues 和 PR 评论中，我们可以提炼出以下用户核心声音：

-   **“版本升级是我的噩梦”**：大量用户反馈在升级到较新的版本（特别是 v2026.4.x 和 v2026.6.1）后，遇到了核心功能不工作、性能严重下降或数据丢失的“灾难性”问题。这是目前社区里最大的挫折来源。
-   **“我希望 Agent 能正确完成我交给它的任务”**：Coding Agent 无法完成任何工作的回归 Bug (#62505) 获得了广泛共鸣，表明用户高度依赖 Agent 的自动执行能力，任何退化都会直接打击他们对项目的信心。
-   **“我需要控制 Agent 的开销和安全等级”**：关于分层配置文件、会话时长限制、MCP 审批等特性请求，都指向用户希望在享受 AI 能力的同时，能够有效控制 Token 成本和工具调用的安全风险。

### **待处理积压**

以下是一些长期未响应或未解决的重要 Issues 和 PR，它们可能成为项目健康的潜在风险点。

**重要积压 Issues：**

-   **Issue #63101**: 飞书频道配置在 v4.5 升级到 v4.8 后验证失败。自 2026-04-08 以来开放，被标记为 `stale`，影响部分飞书用户。
    [链接](https://github.com/openclaw/openclaw/Issue/63101)
-   **Issue #62985**: Telegram 多账户配置在 v2026.4.8 出错。自 2026-04-08 开放，同为 `stale` 状态。
    [链接](https://github.com/openclaw/openclaw/Issue/62985)
-   **Issue #61005**: Android 版 “Connect”按钮在离线时不可用，新用户会卡在引导页面。自 2026-04-04 开放，这是一个影响新用户入门的体验问题。
    [链接](https://github.com/openclaw/openclaw/Issue/61005)

**积压 PRs：**

-   **PR #65198**: 测试用例，用于覆盖“非流式字符串回复”场景。自 2026-04-12 开放，状态为 `needs-real-behavior-proof`。此类测试 PR 长期搁置，无法覆盖潜在代码路径风险。
    [链接](https://github.com/openclaw/openclaw/pull/65198)
-   **PR #88796**: 修复 Discord `search` 操作在缺少 `guildId` 时失败的 Bug。自 2026-05-31 开放，状态为 `needs proof`。
    [链接](https://github.com/openclaw/openclaw/pull/88796)

**分析：** 这些积压项大多与社区功能（飞书、Discord、Telegram）和移动端体验相关。维护团队可能需要优先考虑解决这些长期搁置的 Issue，以避免社区信心下降。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，基于您提供的2026-06-06各项目动态数据，我为您生成了以下横向对比分析报告。

---

### **AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-06-06)**

#### **1. 生态全景**

2026年6月6日，个人 AI 助手/自主智能体开源生态呈现出 **“高活跃、高迭代、碎片化与两极分化”** 的总体态势。一方面，以 OpenClaw 和 ZeroClaw 为代表的头部项目社区互动极其频繁（分别达950+和100+条Issues/PRs），显示出强大的市场关注度与社区贡献热情。另一方面，大量项目仍在快速迭代中，**回归Bug频发**（如OpenClaw、Hermes、CoPaw），稳定性成为普遍痛点。技术路线上，**安全增强、多Agent协作、上下文精细控制及更开放的Provider生态**成为各项目共同发力的方向，但具体实现路径和功能侧重已出现显著分化。

#### **2. 各项目活跃度对比**

| 项目名称 | 24h Issues数 (新开/活跃) | 24h PR数 (待合并/已合并关闭) | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 极高 (+950条互动) | 密集 (+364待合并) | 无 | **高风险活跃**：社区极活跃，但P1级回归Bug及大量待合并PR构成严重稳定性隐患。 |
| **NanoBot** | 中 (6活跃，5关闭) | 中 (17待合并，11已处理) | 无 | **良好**：修复高效，功能持续稳定推进，社区反馈响应快。 |
| **Hermes Agent** | 高 (48新开/活跃) | 高 (28待合，22已合并/关闭) | **v0.16.0** | **优秀**：里程碑式版本发布，修复与增强并重，活跃度与成熟度兼备。 |
| **PicoClaw** | 中 (2新开，4关闭) | 高 (2待合，20已合并/关闭) | **Nightly** | **良好**：修复响应迅速，安全加固积极，但存在高优Token消耗Bug待解。 |
| **NanoClaw** | 低 (0新开) | 低 (1待合并) | 无 | **平稳**：功能迭代期，社区参与度低，需关注是否进入维护静默期。 |
| **NullClaw** | 低 (0新开) | 低 (1待合并) | 无 | **平稳**：类似静默期，唯一PR指向Provider扩展，方向性明确。 |
| **IronClaw** | 高 (13活跃) | 高 (28待，50已处理) | 无 | **极速迭代**：Reborn架构重构为主，开发密度极高，但对早期用户稳定性有挑战。 |
| **LobsterAI** | 低 (活跃Bug数) | 高 (13已合并) | **v2026.6.5** | **良好**：Bug修复与功能增强并重，版本发布稳定，Cowork模式打磨中。 |
| **TinyClaw** | 无 | 无 | 无 | **静默**：24h无活动。 |
| **Moltis** | 中 (3新Bug，1功能) | 中 (4待合并) | 无 | **健康**：Bug修复效率高（Telegram严重Bug当日修复），新功能稳步推进。 |
| **CoPaw** | 高 (21活跃) | 高 (24活跃) | 无 | **高投入高波动**：大量Bug修复和功能PR合并，但Yuanbao通道集中爆发Bug，稳定性仍需加固。 |
| **ZeptoClaw** | 无 | 无 | 无 | **静默**：24h无活动。 |
| **ZeroClaw** | **极高** (50活跃) | **极高** (50活跃) | 无 | **极速迭代-架构革命期**：0.9.0架构规划（RFC）进入实质阶段，社区对安全、可观测性等投入巨大，长期潜力大，短期风险高。 |

#### **3. OpenClaw 在生态中的定位**

*   **核心优势**: **“社区驱动”的先行者**。拥有生态中最庞大的社区互动量，这意味着极快的Bug发现和功能需求汇聚速度。其广泛的通道支持（Mattermost、Matrix等）和插件生态是重要护城河。
*   **技术路线**: 采用 **“平台与Agent分离”** 的架构，强调了“Coding Agent”等专项能力，但对社区贡献的代码质量把控相对较弱，导致回归问题频发。
*   **社区规模**: **最大**，但质量参差。24小时950+的互动量远超其他项目（如NanoBot的30+，Hermes的70+），这既是其生命力来源，也是其管理瓶颈（364条待合并PR即是明证）。
*   **与同类相比**: 与 **Hermes Agent** 相比，Hermes 在发布节奏（v0.16.0 vs 无）和稳定性上更具优势，而 OpenClaw 在生态宽度和社区热度上领先，更像一个“大杂烩”式的技术试验田。

#### **4. 共同关注的技术方向**

以下需求在多个项目中涌现，构成了生态的技术共识：

1.  **上下文管理与成本控制**:
    *   **相关项目**: **Hermes Agent** (#40201 压缩后幻觉), **OpenClaw** (分层配置文件 #22438, 会话时长限制 #64463), **Moltis** (PR#1089 截断工具结果)
    *   **具体诉求**: 用户强烈要求更精细、更智能的上下文窗口管理，避免Token浪费和因历史过长导致的模型幻觉或成本失控。

2.  **工具调用安全与控制**:
    *   **相关项目**: **OpenClaw** (MCP审批 #78308), **ZeroClaw** (Shell命令确认层级 #7155), **PicoClaw** (exec守卫误报 #1042), **IronClaw** (WeCom审批回复失效 #4502)
    *   **具体诉求**: 从简单的“允许/禁止”转向更细致的权限模型，如引入人工审批通道、可配置的确认层级、以及对敏感操作（如Shell执行、文件写入）提供更智能的中断机制。

3.  **记忆与知识持久化**:
    *   **相关项目**: **OpenClaw** (按Agent隔离维基 #63829), **Hermes Agent** (修复mem0记忆读取 #38444), **NanoBot** (历史注入固化错误推理 #4212)
    *   **具体诉求**: 用户不满足于简单的对话记忆，要求更可靠（防止副作用固化）、更隔离（多Agent场景）和更可控的知识库系统。

4.  **版本升级后稳定性**:
    *   **相关项目**: **OpenClaw** (回归问题高发), **Hermes Agent** (桌面端IME问题), **NanoBot** (Copilot登录失败), **CoPaw** (Yuanbao通道回归)
    *   **具体诉求**: 对版本升级带来的功能退化（Regression）极度敏感，“升级是灾难”成为社区普遍声音。这是所有快速发展项目的共性问题。

5.  **多Agent协作机制**:
    *   **相关项目**: **OpenClaw** (子代理工具转发), **NanoBot** (跨实例消息总线 #3992, 子代理/结果记录 #4205), **ZeroClaw** (A2A Agent发现 #7218)
    *   **具体诉求**: 推动Agent从单兵作战向团队协作演进，需要标准化的通信协议、任务分发和结果聚合机制。

#### **5. 差异化定位分析**

*   **功能侧重**:
    *   **OpenClaw/ZeroClaw**: 定位为**平台级Agent操作系统**，强调多通道、多模型、多插件的高度可扩展性，社区驱动，功能“大而全”。
    *   **Hermes Agent / CoPaw**: 定位于**开发者与深度用户工具**，注重与IDE/CLI的集成，桌面端体验，以及如Coding Agent、Shell执行等核心开发场景。
    *   **NanoBot / LobsterAI**: 定位为**个人效率助手**，侧重日常对话、通道适配（微信、钉钉等）和UI交互体验（如LobsterAI的Cowork模式）。
    *   **Moltis / PicoClaw**: 定位于**轻量级、易部署的个人助手**，追求简洁架构和功能明确，强调健壮性和易用性。

*   **目标用户**:
    *   **开发者与极客**: **OpenClaw、Hermes、ZeroClaw、IronClaw**。
    *   **个人用户与轻量级使用者**: **NanoBot、PicoClaw、Moltis**。
    *   **企业级/专业用户**: **ZeroClaw** (强调安全与可观测性)、**LobsterAI** (协作模式)。

*   **技术架构**:
    *   **高度模块化、插件化**: **OpenClaw、ZeroClaw**。
    *   **核心驱动、重点优化**: **NanoBot、Hermes** (如在桌面端和IME上投入巨大)。
    *   **刻意保持精简**: **Moltis、PicoClaw** (不追求功能堆砌，追求核心稳定)。

#### **6. 社区热度与成熟度**

*   **第一梯队 (高速迭代/不稳定期)**: **OpenClaw, ZeroClaw, IronClaw, CoPaw**。这些项目社区活跃度极高，开发者投入巨大，但伴随大量功能开发与架构重构，稳定性风险大，Bug回归率高。适合愿意尝鲜并参与贡献的开发者。
*   **第二梯队 (质量巩固/稳健创新期)**: **Hermes Agent, NanoBot, LobsterAI, PicoClaw, Moltis**。这些项目已形成稳定的版本发布节奏，或处于大版本发布后的巩固期，修复效率高，用户体验更平滑。适合对稳定性要求更高的用户部署使用。
*   **第三梯队 (静默/维护期)**: **TinyClaw, ZeptoClaw, NullClaw, NanoClaw**。项目活跃度低，社区贡献稀疏，可能需要关注项目维护者是否精力不足或项目方向调整。

#### **7. 值得关注的趋势信号**

1.  **“稳定性”是最大的显性需求，也是最大的商业机会**：大量数据表明，用户对现有产品的“不稳定”极其不满。能够提供“发布即稳定”特性的项目或产品，将具备巨大优势。这预示着一个专注于**回归测试、版本兼容性管理和可靠发布流程**的细分服务或工具的需求将会出现。

2.  **安全层成为新的“竞争门槛”**：从可插拔的安全提供者接口(ZeroClaw)到MCP工具审批(OpenClaw)，再到对敏感命令的高风险控制(Hermes, CoPaw)，安全不再是附加功能，而是核心架构的一部分。这预示着未来AI Agent框架的竞争将从“能不能做”转向“在安全的前提下能不能做”。

3.  **快速迭代的“双刃剑”效应已现**：高频的版本发布带来了新功能，但也频繁打断了用户的工作流。社区已经开始出现对更**明确的变更日志、细粒度的功能开关和可回滚的版本管理**的需求。这为电子书、博客或“平滑升级最佳实践”类内容产品提供了市场空间。

4.  **“上下文的幻觉代价”被量化**：用户已开始主动讨论并量化上下文管理不当带来的Token成本和模型行为退化（幻觉、不完成任务）。这推动了对**分层配置、会话时长硬性限制、智能上下文压缩**等技术方案的深入研究，并可能催生一套用于评估Agent记忆效率的新标准或工具。

5.  **多Agent协作的“Babel困境”**：即便大家都在探索多Agent，但通信协议、任务调度、结果聚合的标准远未统一。ZeroClaw提出A2A协议，NanoBot尝试消息总线，这表明**跨框架的Agent互操作性标准化需求**已经站在了风口浪尖，任何能提出并推广一个被广泛接受的标准的实体，都可能成为生态未来几年的重要基石。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报（2026-06-06）

## 1. 今日速览

过去 24 小时，NanoBot 项目保持高度活跃：共处理 11 条 Issue（新开/活跃 6 条，关闭 5 条），25 条 Pull Request（待合并 17 条，已合并/关闭 11 条）。社区贡献热情高涨，多份修复关键 Bug 的 PR 被快速合并，同时涌现出多项新功能提案（如 Exa 搜索、子代理配置、邮件后处理等）。项目健康度良好，团队响应及时，但在 Matrix 通道测试、CI 流程等基础设施方面仍有长期积压待处理。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭了 11 个 PR，主要推进了以下方向和修复：

- **SDK 稳定性**：PR #4216 修复了 SDK 使用 stdio MCP 时 shutdown 报错“exit cancel scope in a different task”的问题（对应 Issue #4211），已合并。
- **会话管理 Bug 修复**：PR #4215 修复了 `find_legal_message_start` 在孤立工具结果后丢弃所有消息的严重 Bug（Issue #4203），已合并。
- **桌面端优化**：PR #4210 修复了桌面端重启后 token 丢失及 WebSocket 回放间隙问题，同时支持流式回复桌面通知，已合并。
- **技能命令完善**：PR #3968 新增 `/skill` 内建斜杠命令，用于列出所有启用的技能，解决了用户无法发现可用技能的问题（Issue #3959），已合并。
- **消息配对修复**：PR #4197 修复了微信和 Telegram 私信配对问题，确保被拒绝的发送者走统一配对流程，已合并。
- **子代理结果机制**：PR #4205 新增基于内存信箱的子代理任务/结果记录协议，替换了原有的隐藏轮询等待，提升子代理协作效率，目前为开放状态，待进一步审查。
- **其他功能**：PR #4206 为钉钉通道添加了群聊白名单配置；PR #4208 新增 WebUI 的“从此处 fork”功能，支持按消息创建分支对话；PR #4209 允许通过 `null extraBody` 删除 OpenAI 图片参数中的默认字段等。

整体上，项目在 Bug 修复、桌面体验、通道适配和协作机制上均有实质性推进。

---

## 4. 社区热点

- **Issue #2573**（Github Copilot 登录失败）：9 个 👍 表示非常关注。用户报告使用 OAuth 登录时出现 `Authorization header is badly formatted` 错误，怀疑是改用 openai 替代 litellm 后的回归。该 Issue 已被关闭，但未说明具体修复方案。社区对提供商兼容性仍有强烈诉求。
- **Issue #3959**（`/skill` 命令列出已禁用的技能）：用户提交配置后 disabledSkills 仍被列出，引发了对技能过滤逻辑的质疑。该 Issue 已由 PR #3968 解决，但仍有用户建议增加可视化区分。
- **Issue #4212**（历史注入导致未确认推理被强化为事实）：零评论但设计精巧，作者深入分析了 Consolidator 与 Memory 双向回写导致的长效错误固化问题，引发对记忆系统架构的讨论。虽暂无 PR，但属于高价值设计讨论。
- **PR #3992**（跨实例消息总线）：由外部贡献者实现的多 Agent 通信机制，评论数未显示但持续更新至 6 月 5 日，反映社区对 Agent 协作场景的浓厚兴趣。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 | 修复 PR |
|----------|-------|------|------|---------|
| **高** | #4211 | SDK 使用 stdio MCP 时 shutdown 抛 RuntimeError | 已有修复 | #4216（已合并） |
| **高** | #4203 | `find_legal_message_start` 丢消息（孤立工具结果导致全部消息被丢弃） | 已有修复 | #4215（已合并） |
| **中** | #4200 | 刷新浏览器后用户消息丢失（WebUI 回归） | 已关闭，可能由 #4210 修复 | #4210（已合并） |
| **中** | #3959 | `/skill` 列出已禁用的技能 | 已修复 | #3968（已合并） |
| **低** | #1946 | Matrix 通道测试在 `main` 分支失败 | **长期开放（3月13日至今）** | 无 |

另外，PR #4210 还修复了桌面端重启 token 丢失和 WebSocket 回放间隙问题，提升了系统可靠性。

---

## 6. 功能请求与路线图信号

- **#4204**（为 OpenAI 兼容提供商增加 `extra_query` 支持）：用户需要向 Azure 风格网关传递 `?api-version=`，已提交 PATCH 和 Issue，社区关注度高，大概率进入下一版本。
- **#4198**（子代理 `fail_on_tool_error` 行为可配置）：用户希望子代理在工具错误后有机会自行调整，而非直接返回，已提出具体配置方案，有 PR 潜力。
- **#4213**（Exa 搜索提供商）：已有 PR #4213 实现，首次贡献者提交，若通过审查将丰富搜索能力。
- **#4132**（支持自定义图像生成提供商）：已关闭（可能是已有方案或重复），但用户对图像生成可扩展性的需求清晰，可通过类似方式快速支持。
- **#4196**（支持火山引擎图像生成）：已关闭（标记为重复），建议用户参考 #4132 的解决方案。
- **#4212**（防止历史注入固化错误推断）：属于架构级增强，短期内可能不会直接实现，但为记忆系统优化提供了方向。
- **#4170**（邮件通道 IMAP 后处理动作）：PR 已开放，允许对已处理的邮件执行标记、归档等操作，适合 Agent 管理邮箱场景。

此外，PR #3992（跨 Agent 消息总线）若合并，将推动 NanoBot 向多 Agent 协作平台迈出重要一步。

---

## 7. 用户反馈摘要

- **Copilot 登录不畅**（#2573）：用户 cheanus 反映“用 openai 替代 litellm 后出现新 bug”，显示提供商切换引入了兼容性问题，用户对提供商支持的一致性敏感。
- **技能列表困惑**（#3959）：用户 mraad 指出 disabledSkills 配置无效，“禁用了 weather 仍然被列出”，希望命令能区分启用/禁用状态。
- **消息丢失恐慌**（#4200）：用户 chengyongru 提交 Bug 时附带截图（可惜无法显示），描述“chat refresh browser 后消息丢失”，属于影响用户体验的回归，已迅速修复。
- **逻辑缺陷发现**（#4203）：用户 huji820 深入代码发现 `find_legal_message_start` 在特定消息序列下会返回空列表，导致整个会话历史被丢弃，体现社区贡献者对代码质量的高参与度。
- **内存与推理纠缠**（#4212）：用户 joaoinacio 提出 Consolidator 和 Memory 双向回写可能导致未确认的推断被错误强化，并建议增加置信度标记，属于高级用户对语义记忆机制的思考。

---

## 8. 待处理积压

- **Issue #1946**（Matrix 测试错误）：自 3 月 13 日开启，已超过 85 天无人处理。测试失败可能影响 Matrix 通道的 CI 信心，建议维护者分配资源或标记为需社区协助。
- **PR #1408**（添加 CI 工作流 + 覆盖率门禁）：自 3 月 2 日提交，更新至 6 月 5 日仍处于开放状态，与另一个 PR #1284 功能重叠，需维护者决定优先级并合并或关闭。
- **PR #1284**（CI/CD + 开发工具链）：同样自 2 月 27 日开放，已有 3 个多月，内容包含测试和验证，但长期搁置可能增加合并冲突风险。
- **PR #3538**（gateway start/stop/restart 命令）：自 4 月 29 日提交，涉及 CLI 增强和部署文档，对运维友好，但缺少维护者反馈。
- **PR #4170**（邮件后处理）：6 月 3 日提交，更新至 6 月 5 日，需审查是否满足设计规范。

建议团队关注上述长期未响应的基础设施类和功能类 PR，以保持社区贡献者的积极性。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-06-06

## 1. 今日速览
- **项目活跃度极高**：过去24小时新开/活跃Issue 48条、PR更新50条（其中22条已合并/关闭），贡献者社区响应迅速。
- **里程碑式版本发布**：Hermes Agent v0.16.0 "The Surface Release" 于昨日（6月5日）正式发布，包含874次提交、542个合并PR、399个issue关闭（含2个P0、62个P1及16个安全标记），社区贡献者达170人。
- **桌面端与平台适配成为焦点**：多起关于macOS Intel支持缺失、中文IME输入交互异常、Feishu/Discord平台适配Bug等用户反馈集中涌现，项目组已通过`fix(desktop)`系列PR快速响应。
- **安全与稳定性持续加固**：两条P2安全PR（#40253、#40176）正在解决依赖CVE及模块加载风险；MCP重连、Gateway配置桥接等长期稳定性问题仍在修复中。

## 2. 版本发布
### v2026.6.5 · Hermes Agent v0.16.0 – "The Surface Release"
- **发布日期**：2026年6月5日  
- **主要统计**：自v0.15.2以来，874 commits · 542 merged PRs · 1,962 files changed · 205,216行新增 · 46,217行删除  
- **问题关闭**：399 issues，其中P0级别2个，P1级别62个，安全标记16个  
- **社区贡献**：170位社区贡献者（包含合作作者）  
- **破坏性变更与迁移注意事项**：  
  - 本次发布未详细说明破坏性变更，但根据PR趋势，建议用户关注以下几点：  
    - `gateway/config.py` 的Platform枚举可能影响插件平台（如LINE）；  
    - `hermes security` 工具已升级CVE扫描规则，旧依赖可能被标记；  
    - 桌面端Electron包在macOS上仅提供arm64版本，Intel Mac用户需等待后续修复或自行从源码构建。

## 3. 项目进展
今日合并/关闭的重要PR（24小时内共22条合并/关闭，以下为重点推进）：
- **[#39647] fix(desktop): reconcile composer draft on compositionend for IME reliability**  
  修复macOS越南语Telex及东亚IME在合成结束后不触发`input`事件的问题，提升中文/日文输入可靠性。  
- **[#39427] fix(desktop): preserve previous unpacked dir on failed pack**  
  修复Electron-builder打包失败时删除旧目录导致构建无法恢复的问题。  
- **[#38828] fix(matrix): propagate room name to session source**  
  Matrix适配器现在正确向`channel_directory.json`传递房间名称，而不再使用用户显示名称。  
- **[#38444] fix(mem0): include agent-attributed memories in read filter**  
  Mem0记忆提供者查询现在能获取agent归属的记忆，修复`mem0_search`无法检索到由agent写入的记忆的Bug。  
- **[#37765] fix: prevent config dual-write conflict in gateway model switch**  
  修复桌面端与Gateway之间通过`/model --global`切换模型时配置双写冲突的问题。  
- **[#37380] fix(send_message): route WeCom MEDIA through live gateway adapter**  
  企业微信（WeCom）消息中的`MEDIA`指令现在能正确通过Gateway适配器发送附件。  
- **[#37067] fix: expose model reasoning/thinking blocks in /v1/chat/completions**  
  开放API兼容端点现在会输出模型的`last_reasoning`字段，使Open WebUI等下游UI能显示思考链。  
- **[#32297] fix(vision): don't retry non-retryable 4xx image downloads**  
  视觉工具不再对`404`/`403`等确定性错误重复下载，减少无效请求。  
- **[#38619] fix: bump version from 0.15.1 to 0.15.2**  
  将`pyproject.toml`版本对齐到实际release tag `v2026.5.29.2`。  
- **[#38237] fix: warn when claw migrate source is a remote-mode OpenClaw client**  
  迁移命令现在会在源为远程模式时给出警告，避免用户误以为迁移成功。  

> 项目整体在桌面端IME、平台适配、记忆系统、安全修复、配置一致性等方面均有显著推进，社区活跃度持续走高。

## 4. 社区热点
- **[#37505] Hermes Desktop macOS DMG is arm64-only and fails on Intel Macs**  
  **评论数**：5 | **状态**：Open | **标签**：P3 Bug  
  用户反映官方DMG仅包含arm64架构，Intel Mac上无法启动。已有多位用户反馈（包括#38227），目前尚无对应PR，但项目组可能将其视为P2级别。  
- **[#40219] Add Japanese language support (i18n / localization)**  
  **评论数**：4 | **状态**：Open | **标签**：P3 Feature  
  日本用户请求添加日语UI及系统消息支持。目前仅支持英文和简体中文。同期还有#40239（pt-BR）请求，表明i18n需求正在扩大。  
- **[#31101] QQ Bot adapter: _read_events() silent loop after reconnect failure**  
  **评论数**：4 | **状态**：Open | **标签**：P2 Bug  
  QQ Bot在WebSocket重连失败后陷入无限静默循环，导致机器人永久离线。该问题已存在两周，社区呼吁尽快修复。  
- **[#40146] Desktop app: Send button doesn't switch from voice button when typing Chinese (IME)**  
  **评论数**：3 | **状态**：Open | **标签**：P3 Bug  
  Windows桌面端中文输入法下，发送按钮不出现，需等到文字提交后才显示。与#39614、#40226形成一组IME相关Bug群。  
- **[#40251] ❤️ 一个中国用户的感谢信：Hermes 的 skill/memory 系统让我看到了 AI Agent 真正的可成长性**  
  **评论数**：0（刚发布） | **状态**：Open  
  中文用户提交的长篇反馈，高度赞扬Hermes的“skill + memory + session_search”构建的学习闭环，认为这是目前最天才的AI Agent设计。代表了核心用户对产品方向的深度认同。

## 5. Bug 与稳定性
按严重程度排列（P1最高）：

| 等级 | Issue | 描述 | 状态 | 是否有fix PR |
|------|-------|------|------|------------|
| **P1** | #40201 | 上下文压缩后最终合成出现幻觉，声称的发现无来源支撑 | Open | 无 |
| **P1** | #39886 | Cron调度器：profile上下文泄漏到非profile任务，导致脚本找不到 | Open | 无 |
| **P2** | #38412 | 远程Gateway WebSocket连接被拒绝（4403），Electron客户端无法连接 | Open | 无 |
| **P2** | #38488 | MCP服务器在短暂后端故障后永久放弃重连，直到Gateway重启 | Open | 无 |
| **P2** | #38963 | Hermes Desktop启动时提示“no git???”（Windows） | Open | 无 |
| **P2** | #40139 | 密钥脱敏功能修改实际命令执行和输出，而不仅是显示掩码 | Open | 无 |
| **P2** | #40145 | 桌面端输入截断（中文输入时部分文本丢失） | Open | 无 |
| **P2** | #31101 | QQ Bot适配器重连后静默循环 | Open | 无 |
| **P2** | #40176 | 锁定依赖中存在已知CVE（urllib3 / python-multipart 等） | Open | 无 |
| **P2** | #40225 | Feishu卡片审批按钮在DM中总是返回“未授权” | Open | 无 |
| **P3** | #37505 | macOS Intel 不支持（仅arm64） | Open | 无 |
| **P3** | #40101 | mnemosyne-hermes插件未正确发现 | Open | 无 |
| **P3** | #40181 | Gateway配置桥接跳过插件平台（LINE），`channel_prompts`静默失效 | Open | 无 |
| **P3** | #40215 | Desktop远程Gateway调用配置API时出现`net::ERR_INVALID_ARGUMENT` | Open | 无 |
| **P3** | #40250 | 终端转义序列泄漏到输出，导致前1-3字符被切除 | Open | 无 |

> 今日有两条P1严重Bug（#40201 幻觉、#39886 cron上下文泄漏）尚未有修复PR，需重点关注。依赖CVE问题已有安全PR #40253 和 #40176 在讨论中。

## 6. 功能请求与路线图信号

| 功能 | Issue # | 描述 | 优先级 | 是否已有PR/合并 | 可能纳入版本 |
|------|---------|------|--------|----------------|-------------|
| 日文语言支持 | #40219 | UI及系统消息i18n增加日语 | P3 | 无 | v0.17+ |
| 葡萄牙语pt-BR支持 | #40239 | 桌面端增加葡萄牙语 | P3 | 无 | v0.17+ |
| `/approvals` 斜杠命令 | #39425 | 允许在会话中切换审批模式到smart | P3 | 无 | v0.17 (若社区呼声高) |
| 网关状态暴露平台健康 | #40199 | 显示平台适配器健康状况，自动恢复失效适配器 | P3 | 无 | v0.16.x patch |
| Schema sanitizer 字符验证 | #40232 | 对MCP工具参数键名做无效字符清洗，适配严格后端 | P3 | 无 | v0.16.x |
| ToolCallStormBreaker | #35573 | 抑制重复工具调用循环（RFC） | P3 | 无 | 可能作为实验性功能 |
| 当前时间注入prompt | #40252 | 通过`ephemeral_system_prompt`注入当前时间 | — | 已提交PR #40252 | v0.16.1 |
| Hermex MVP 代理 | #40248 | 添加兼容Anthropic的LLM代理，支持会话指纹等 | — | 已提交PR #40248 | v0.17+ |
| Profile Builder Web Flow | #40254 | 添加仪表盘profile构建向导 | — | 已提交PR #40254 | v0.16.x |

> 社区对i18n（日语、葡萄牙语）和桌面端中文输入体验的需求明显增强。同时，项目内已出现多个面向开发者体验的功能PR（Profile Builder、Hermex代理），可能推动下一个minor版本。

## 7. 用户反馈摘要
- **中国用户深度赞赏**：@skill-zhang 在#40251中详细描述了Hermes的skill+memory系统如何支撑“阶段性进展累积式构建”工作流，认为这是“最天才的AI agent设计”。这一反馈反映了项目在**可成长性**和**知识闭环**方面的设计获得了核心用户的极高认可。
- **桌面端中文输入是最大痛点**：多位用户（#40146、#40145、#40226、#39614）报告相同的交互问题——在中文IME下发送按钮不显示、输入截断或Enter无法发送。大多数反馈来自Windows用户。已有PR #39647 被合并，但问题似乎未完全解决。
- **Intel Mac用户被抛弃感**：@JE4NVRG、@Keshkov 多次反映DMG只提供arm64，即使macOS 12+系统要求下也不支持Intel。建议项目组提供Universal Binary或至少Intel版本。
- **安全审计阳性反馈**：@zebadee2kk 提交CVE审计报告（#40176），项目组已讨论是否有必要立即锁定依赖。社区对此表示欢迎，认为这是专业态度的体现。
- **MCP断开不重连**：@area51tazz 反馈MCP服务器在短暂故障后永久无法恢复，只能重启Gateway。这对于生产中依赖MCP工具的团队是严重问题，已有大量同感。

## 8. 待处理积压
| 序号 | Issue/PR | 创建时间 | 最后更新 | 状态 | 重要性 | 备注 |
|------|----------|----------|----------|------|--------|------|
| 1 | [#9553] examples/reward_functions_library.py does not exist | 2026-04-14 | 2026-06-06 | Open | P3 | 文档错误，已搁置近2个月，仅有1条评论 |
| 2 | [#35573] ToolCallStormBreaker RFC | 2026-05-30 | 2026-06-05 | Open | P3 | 功能性RFC，无进一步讨论，建议维护者评估是否推进实验性实现 |
| 3 | [#34215] fix(memory): compact recall context boundaries | 2026-05-29 | 2026-06-06 | Open (PR) | P2 | 大内存优化PR，已存在8天但未合并，需要核心团队review |
| 4 | [#38412] Remote Gateway WebSocket被拒 | 2026-06-03 | 2026-06-06 | Open | P2 | 影响远程桌面用户，尚无PR，需尽快定位bind配置或Electron问题 |
| 5 | [#40101] mnemosyne-hermes插件未发现 | 2026-06-05 | 2026-06-06 | Open | P3 | 第三方插件集成问题，可能影响Plugin生态 |

> 建议维护团队优先处理**P1级的#40201（上下文压缩幻觉）**和**#39886（cron上下文泄漏）** ，并尽快对**#38412（远程WS连接）**给出诊断或workaround。对于搁置超过1个月的#9553文档错误，应考虑在下一小版本中关闭。

---

**数据分析日期**：2026-06-06  
**数据来源**：NousResearch/hermes-agent GitHub 仓库公开数据  
**声明**：本日报由AI系统自动生成，基于实时仓库统计数据，仅供参考。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 | 2026-06-06

---

## 1. 今日速览

过去24小时项目保持较高活跃度：共更新 **6 个 Issue**（其中 4 个关闭）、**22 个 PR**（20 个合并/关闭），并发布了一个 **nightly 构建版本**。重点集中在修复 OneBot 群聊回复错误、类型断言导致的 panic 风险、以及 `/context` 命令显示不全的用户反馈。此外还合并了多项安全加固（CSRF、路径穿越保护）和依赖更新。项目整体健康度良好，社区反馈的 bug 响应迅速，但仍有少量长期待办（如频道重构 PR）和新生 bug 需持续跟踪。

---

## 2. 版本发布

### nightly (v0.2.9-nightly.20260606.89ee8f1b)

- **类型**：自动构建，可能不稳定
- **变更记录**：`v0.2.9...main` 之间的全部提交
- **改动亮点**：包含当日所有合并的修复（OneBot 群聊、类型断言安全、技能文档修正等），以及依赖升级（Anthropic SDK、React、shadcn 等）
- **迁移注意**：无破坏性变更声明，但夜间构建未经过完整回归测试，生产环境建议使用稳定版
- **链接**：https://github.com/sipeed/picoclaw/releases/tag/v0.2.9-nightly.20260606.89ee8f1b

---

## 3. 项目进展

以下为今日合并/关闭的重要 PR，推动项目在稳定性、安全性和功能体验上取得进展：

| PR | 内容 | 影响 |
|----|------|------|
| [#3009](https://github.com/sipeed/picoclaw/pull/3009) | **fix(onebot): use prefixed chatID for group reply routing** | 修复 OneBot 群聊回复误用 `send_private_msg` 的 bug，使群聊消息正确路由 |
| [#3010](https://github.com/sipeed/picoclaw/pull/3010) | **fix(channels): add ok checks for type assertions in toChannelHashes** | 防止因 JSON 反序列化产生意外类型时 panic，提升配置稳定性 |
| [#3011](https://github.com/sipeed/picoclaw/pull/3011) | **fix(agent): add ok check for LoadAndDelete type assertion** | 修复 `UnsubscribeEvents` 中潜在的 panic 风险 |
| [#2985](https://github.com/sipeed/picoclaw/pull/2985) | **fix(context): show both summarize and compress thresholds in /context** | 解决用户困惑：`/context` 命令现同时显示软摘要阈值和硬压缩阈值 |
| [#3013](https://github.com/sipeed/picoclaw/pull/3013) | **docs: remove missing skill-creator helper script references** | 修正技能创建文档，移除不存在的脚本引用，提供手动操作指南 |
| [#2900](https://github.com/sipeed/picoclaw/pull/2900) | **fix: add CSRF protection, path traversal validation, and security headers** | 增加 CSRF 保护、路径穿越校验和安全响应头，加固 Web 后端 |
| [#2905](https://github.com/sipeed/picoclaw/pull/2905) | **Fix fallback chain handling for expired contexts** | 修复回退链中已过期上下文未及时终止的问题，减少无效尝试 |
| [#2907](https://github.com/sipeed/picoclaw/pull/2907) | **Fix JSONL store metadata drift after crash** | 修复崩溃后 JSONL 元数据与数据文件不一致的问题，提高可靠性 |
| [#2913](https://github.com/sipeed/picoclaw/pull/2913) | **Fix JSONL session index hot-path cloning and TTL refresh semantics** | 优化内存索引克隆开销，并修复 TTL 刷新语义 |
| [#2962](https://github.com/sipeed/picoclaw/pull/2962) | **build(deps): bump anthropic-sdk-go from 1.26.0 to 1.46.0** | 大幅升级 Anthropic SDK，获得新 API 支持和性能改进 |
| 其余 | 10+ 个依赖更新（React、shadcn、TanStack 等） | 保持前端依赖最新，减少安全漏洞 |

此外，已关闭的 20 个 PR 中包括多个由 `dependabot` 发起的依赖升级和多个 stale 但已合并的修复。项目在**内存存储 crash 一致性**、**回退链处理**和 **OneBot 协议兼容**方面取得了实质性进展。

---

## 4. 社区热点

### 4.1 最活跃讨论：Issue #1042（已关闭）
- **标题**：[BUG] exec工具的guardCommand方法问题
- **评论数**：15 | 👍：2
- **内容**：用户报告 `exec` 工具的安全守卫方法过于简单粗暴，将 `curl -s "wttr.in/Beijing?T"` 误判为路径穿越，导致命令被阻断。该问题最终关闭，但未在提交中明确关联修复 PR，推测已在早期版本修复或由用户自行配置解决。
- **链接**：https://github.com/sipeed/picoclaw/issues/1042

### 4.2 新开热点：Issue #3012（OPEN）
- **标题**：[BUG] Continuous consumption of tokens every minutes when evolution is enabled
- **评论数**：1（作者后续可能补充）
- **内容**：用户开启 Evolution 功能后，每分钟持续消耗 tokens，严重影响资源使用。目前无修复 PR，需维护者关注。
- **链接**：https://github.com/sipeed/picoclaw/issues/3012

### 4.3 待合并功能 PR： #2964（OPEN）
- **标题**：Feat/image input compression
- **状态**：OPEN，stale
- **内容**：为视觉管道增加可配置的入站图片压缩策略，避免因 `max_media_size` 单一限制导致的过大 payload。该 PR 已 stale 8 天，社区关注度较高。
- **链接**：https://github.com/sipeed/picoclaw/pull/2964

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重性 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| **高** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | 进化模式开启后每分钟持续消耗 tokens，可能导致用户账户使用量暴涨 | 🟡 未修复，待诊断 |
| **中** | [#3002](https://github.com/sipeed/picoclaw/issues/3002) | OneBot 群聊回复误用 `send_private_msg`，并错将群号当作用户 ID | ✅ 已由 PR #3009 修复 |
| **中** | [#2968](https://github.com/sipeed/picoclaw/issues/2968) | `/context` 命令始终显示 `Compress at: 76800 tokens`，未展示摘要阈值 | ✅ 已由 PR #2985 修复 |
| **低** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` 工具守卫误报路径穿越（假阳性） | ✅ 已关闭（可能已修复或通过白名单规避） |
| **低** | [#3010](https://github.com/sipeed/picoclaw/pull/3010) / [#3011](https://github.com/sipeed/picoclaw/pull/3011) | 两处类型断言缺少 ok 检查，存在 panic 风险（代码质量提升） | ✅ 已修复 |

**总结**：今日修复了两个中等严重度的 bug（OneBot 路由和 /context 显示），以及两个潜在的 panic 风险。主要残留问题为 #3012 的 token 消耗异常，需尽快定位。

---

## 6. 功能请求与路线图信号

### 6.1 可能纳入下一版本的功能

- **图片输入压缩（PR #2964）**：该功能解决用户发送大图时模型调用失败的问题，且与视觉能力深度绑定。虽已 stale，但需求明确，维护者应评估并合并。
- **频道识别重构（PR #2551）**：解耦频道名称与提供者类型，允许同一提供者多实例配置，并统一消息总线标识。该 PR 已存在近两个月，属于架构级改进，预计将在后续稳定版中引入。

### 6.2 用户明确提出的需求

- 在 Issue #652 中，用户要求检查和修正 `workspace/skills/skill-creator` 的技能创建流程，PR #3013 已修复文档部分，但技能创建功能本身仍需审计。

### 6.3 路线图信号

- 随着 Anthropic SDK 的大版本更新（#2962），项目对 Claude 模型的支持将更加完善。
- 安全加固（#2900）表明项目正在向生产环境友好方向演进。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的真实用户声音：

- **痛点：OneBot 群聊回复错误**（#3002）  
  用户 `Xuan-Xuann` 报告 NapCat 返回“无法获取用户信息”，经排查为群聊回复误用私聊 API。该问题已快速修复，用户满意度应提升。

- **困惑：/context 显示不全**（#2968）  
  用户 `xpader` 在 FreeBSD 环境下使用 MiniMax 模型，发现 `/context` 始终显示同一个压缩阈值，怀疑是 bug。修复后用户可同时看到软摘要和硬压缩两个阈值。

- **严重问题：进化模式消耗 token**（#3012）  
  同一用户 `xpader` 报告进化模式每分钟持续消耗 token，但无显式请求。这是当前最严重的用户投诉，可能导致账户费用失控。

- **操作安全误解**（#1042）  
  用户 `icyfire` 认为 `exec` 工具的安全守卫过于激进，导致合法命令被误杀。虽然该 Issue 已关闭，但社区对安全策略的“可配置性”仍有期待。

- **技能创建流程不畅**（#652）  
  用户 `mst42a` 提出了技能创建步骤缺失的问题，PR #3013 虽然更新了文档，但用户可能仍需要更完善的自动化工具。

---

## 8. 待处理积压

以下为长期未响应或亟待关注的重要 Issue/PR：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|---------|---------|------|
| **PR** | [#2551](https://github.com/sipeed/picoclaw/pull/2551) | refactor: standardize channel identification (stale) | 2026-04-16 | 2026-06-05 | 核心架构重构，已多个标签（bug, domain: channel/agent/tool/cron），但长期未合并，可能需基于最新 main 分支 rebase |
| **PR** | [#2964](https://github.com/sipeed/picoclaw/pull/2964) | Feat/image input compression (stale) | 2026-05-28 | 2026-06-05 | 功能增强，需审查和解决冲突 |
| **Issue** | [#652](https://github.com/sipeed/picoclaw/issues/652) | [Task] Check correction of workspace skills/ skill-creator | 2026-02-22 | 2026-06-05 | 开放任务，涉及技能创建流程的完整审计 |
| **Issue** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | [BUG] Continuous consumption of tokens every minutes | 2026-06-05 | 2026-06-05 | 新报告，尚无修复 PR，需紧急评估 |

**建议维护者优先处理**：  
1. 调查 #3012 的 token 消耗问题并给出修复或临时规避方案。  
2. 推进 #2551 的重构，以避免分叉过久导致合并成本增加。  
3. 评审 #2964 的功能并决定是否纳入下一个稳定版本（v0.3.0）。

---

*本日报基于 GitHub 公开数据生成，反映截至 2026-06-06 UTC 的项目动态。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# 🧠 NanoClaw 项目动态日报 | 2026-06-06

---

## 1. 今日速览

过去 24 小时内，NanoClaw 仓库**无新 Issue 提出**，但合并/关闭了 2 个 PR，并新增 1 个待合并的修复 PR，显示出 **中等活跃度**。项目重点集中在 **API 错误重试机制的增强**（#2692）以及 **OneCLI 与 HF Token 配置的简化与文档修正**（#2691, #2690）。版本发布为 0，整体处于稳定的功能迭代与缺陷修复期。

---

## 2. 版本发布

**无新版本发布**（最新 Releases 为空）。

---

## 3. 项目进展

### 已合并/关闭的 PR（2 项）

- **#2691** `feat: show OneCLI's own setup URL when HF token is missing`  
  *作者：gavrielc*  
  解决了一处登录提示中硬编码网关 URL 的问题，改为从凭证缺失时的错误响应中动态获取实际网关 URL，提升了多网关部署场景下的用户指引准确性。  
  🔗 [PR #2691](https://github.com/nanocoai/nanoclaw/pull/2691)

- **#2690** `fix: simplify HF token setup + correct secret-mode docs`  
  *作者：gavrielc*  
  修正了 OneCLI 代理默认 secret 模式的文档：实际默认值为 `all`（而非文档中描述的 `selective`），并移除了不必要的 `upload-trace.ts` 中逐个代理赋值的步骤，降低了配置复杂度。  
  🔗 [PR #2690](https://github.com/nanocoai/nanoclaw/pull/2690)

### 待合并的 PR（1 项）

- **#2692** `fix(poll-loop): retry transient 5xx API-error results, notify on exhaustion`  
  *作者：ddaniels*  
  处理 Claude Agent SDK 内部重试耗尽后返回错误 `result` 消息（非抛出异常）的场景，避免将临时性 5xx 错误误判为终端失败，并在重试耗尽后给出通知。  
  🔗 [PR #2692](https://github.com/nanocoai/nanoclaw/pull/2692)

**小结**：项目在 **用户体验引导**（动态 URL）、**文档准确性**（默认 secret mode）及 **API 稳定性**（5xx 重试）方面均有推进，整体稳健。

---

## 4. 社区热点

今日 **无活跃讨论**（#2691 与 #2690 评论数均为 undefined 且无点赞，实际无互动）。  
开放 PR #2692 亦无评论或反应。社区参与度较低，可能处于项目周期中的静默期。

---

## 5. Bug 与稳定性

### 严重程度：中

- **（待修复）** 临时性 5xx API 错误（如 `529 Overloaded`）在 Claude Agent SDK 重试耗尽后以 `result` 消息形式返回，当前未做区分处理，可能导致错误被当作正常结果传递。  
  **对应修复 PR**：#2692（open），已实现重试逻辑与通知机制。

其余已关闭的 PR 均为文档与功能改进，不涉及 Bug 报告。

---

## 6. 功能请求与路线图信号

今日未收到用户提交的 Issue 形式新功能请求。  
但从已合并的 PR 可看出以下方向：

- **多网关自适应 URL 提示**（#2691）—— 提升跨部署环境的用户体验，可能被纳入后续版本特性。
- **默认 secret mode 修正**（#2690）—— 属于高优文档修复，非新功能，但间接降低了用户配置门槛。

整体路线图信号：**稳定性（重试机制）** > **用户体验细节** > **文档纠错**。

---

## 7. 用户反馈摘要

由于今日无 Issue 评论，且 PR 均无互动，无直接用户反馈可提取。  
潜在痛点可从 PR 提交动机推断：

- 用户可能遇到配置 OneCLI 时 secret mode 错误文档导致不必要的步骤（#2690）。
- 用户可能因 5xx 临时错误导致调用中断，期望更智能的重试（#2692）。
- 用户在多网关部署时被错误硬编码 URL 误导（#2691）。

---

## 8. 待处理积压

| 类型 | 编号 | 标题 | 状态 | 搁置天数 | 备注 |
|------|------|------|------|----------|------|
| PR   | #2692 | `fix(poll-loop): retry transient 5xx API-error results, notify on exhaustion` | Open | 1 天 | 需要 reviewer 审核，暂无 Comments |
| —    | —    | （无长期未响应 Issue） | —    | —       | —    |

唯一积压项为 #2692，建议维护者尽快安排代码审查，以增强 API 异常场景下的鲁棒性。

---

*报告生成时间：2026-06-06 08:00 UTC*  
*数据来源：[NanoClaw GitHub](https://github.com/qwibitai/nanoclaw)*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 | 2026-06-06

## 1. 今日速览
- 过去24小时内项目活跃度较低，无新Issue产生，也无新版本发布。
- 一项重要Pull Request（#947）被提交，旨在将Evolink添加为OpenAI兼容的Provider，扩展了多模型网关接入能力。
- 项目维护节奏放缓，但社区仍保持对多Provider兼容性方向的关注，整体状态平稳。

## 3. 项目进展
- **合并/关闭的PR**：无（今日无已合并或关闭的PR）。
- **重要开放的PR**：
  - **#947** [feat(providers): add Evolink as an OpenAI-compatible provider](https://github.com/NullClaw/nullclaw/pull/947) – 由EvoLinkAI提交，为NullClaw增加对Evolink（多模型网关，提供GPT-5、Gemini、DeepSeek等模型）的一等支持。该PR直接通过OpenAI兼容的`/v1/chat/completions`端点接入，降低了用户使用多种模型的配置门槛。目前处于待合并状态，尚未收到维护者反馈或社区评论。

## 4. 社区热点
- **#947** 是今日唯一活跃的PR，虽然暂无评论或点赞，但其内容涉及开源社区广泛关注的“OpenAI兼容Provider”扩展。背景：用户普遍希望在一个框架内动态切换多个后端的LLM，Evolink的加入能显著简化这一过程。该PR反映了社区对**统一API抽象层**的持续需求。

## 6. 功能请求与路线图信号
- **新增功能**：PR #947 请求将Evolink作为一等provider。若合并，将进一步完善NullClaw的“多Provider”策略，尤其是对国产模型（如DeepSeek、Doubao）的覆盖。
- **路线图信号**：该PR指向项目未来可能继续采纳“OpenAI兼容”作为标准接入层，并鼓励更多类似网关的集成。鉴于无其他新功能请求，#947大概率会被纳入下一个迭代版本。

## 7. 用户反馈摘要
- 由于今日无Issue更新及评论，暂无新用户反馈。从PR #947的描述看，提交者认为“Evolink slots straight away without additional code changes”，暗示当前集成成本低，但需注意**Bearer-token认证**的细节，可能影响部分自定义认证场景。

## 8. 待处理积压
- **长期未响应的Issues/PRs**：当前仓库中无明确标记为“长期未响应”的待处理项。PR #947刚刚提交，尚需维护者评估；建议维护者尽快给予初始反馈以避免积压。

> **项目健康度评估**：今日社区活跃度低（0 Issue，1 PR），但新增PR体现了有价值的功能扩展。若该PR能快速合并，可提升项目对多模型接入的吸引力。需关注后续测试及文档更新。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，这是为您生成的 IronClaw 项目动态日报。

***

### IronClaw 项目日报 — 2026-06-06

**分析师点评：** 项目进入高活跃度阶段，开发重心集中在 Reborn 架构的收尾优化与安全加固上。24小时内处理了13个Issue和50个PR，社区贡献活跃，核心开发者（@zmanian, @danielwpz, @serrrfirat）提交了大量高质量PR。项目整体健康度良好，但PR积压数（28个待合并）较高，需关注合并节奏。

---

#### 1. 今日速览

- **整体状态：** 项目活跃度极高，代码库经历了一次大规模开发密度爆发。
- **核心亮点：** **Hook（钩子）框架**已正式在生产环境中激活（见 Issue #3934 关闭），标志着从开发到部署的关键一步。
- **主要活动：** 开发重心完全在 **Reborn** 架构升级上，包括核心组件 `ProductWorkflow` 的拆分（#4488/#4506）、Slack 集成的深度改造（#4510/#4463）、以及 IronHub 安装流程的重写（#4479）。
- **潜在风险：** 待合并PR高达28个，主要来自 `dependabot` 的大规模依赖更新和多个大型功能PR，合并压力较大。同时，WeCom 渠道的 Bug 报告持续出现，表明该渠道稳定性仍需打磨。

---

#### 2. 版本发布

*（无）*

---

#### 3. 项目进展

今日项目在关键架构层面取得了实质性进展，下面列出最重要的合并/关闭项：

- **🎉 Hook 框架生产环境激活**
  - PR #3938 ([链接](https://github.com/nearai/ironclaw/pull/3938)): 将 Hook 框架正式接入生产环境的 `HOOKS_ENABLED` 标志（默认关闭），实现 Issue #3934。
  - PR #3937 ([链接](https://github.com/nearai/ironclaw/pull/3937)): 实现跨后端的对抗性测试套件，验证了 `PredicateStateBackend` 实现的行为一致性，完成了持久化后端的开发闭环。
  - PR #3936, #3933 ([链接](https://github.com/nearai/ironclaw/pull/3936) , [链接](https://github.com/nearai/ironclaw/pull/3933)): 分别完成了 **LibSQL** 和 **PostgreSQL** 的 `PredicateStateBackend` 实现，为 Hook 框架提供了可选的持久化后端。
  - PR #3931 ([链接](https://github.com/nearai/ironclaw/pull/3931)): 修复了三个严重的跨租户数据泄露和信息安全问题，增强了 Hook 框架的安全性。
  - PR #3922 ([链接](https://github.com/nearai/ironclaw/pull/3922)): 将 `SecurityAuditSink` 审计模块整合进请求处理与拒绝路径，增强了系统的可追溯性。

- **🔧 Reborn 架构与工具链进化**
  - PR #4506 ([链接](https://github.com/nearai/ironclaw/pull/4506)): 对应 Issue #4488，正式将 `ProductWorkflow` 拆分为 `submit_inbound`、`read_projection` 和 `subscribe` 三个明确的入口，为未来兼容 OpenAI API 奠定基础。
  - PR #4479 ([链接](https://github.com/nearai/ironclaw/pull/4479)): 将 IronHub 安装流程完整迁移至 Reborn 架构，并集成了签名验证、来源确认等安全机制。
  - PR #4463 ([链接](https://github.com/nearai/ironclaw/pull/4463)): 为 Slack 渠道初始化了持久化存储，并优化了消息的实时投递体验。

---

#### 4. 社区热点

今日最受关注的是两个架构讨论相关的 Issue：

1.  **Issue #4311: Reborn 模式网关预算治理失败映射** ([链接](https://github.com/nearai/ironclaw/issues/4311))
    - **热度：** 获得2条评论，是今日讨论最多的 Issue 之一。
    - **诉求：** 开发者 `henrypark133` 报告了一个架构性问题：在 Reborn 模式中，网关将多种非上下文相关的预算违规（Budget Governance Failure）错误映射为了 `ContextOverflow`，这可能导致 Agent 在错误的条件下进行上下文恢复，而非正确处理预算超支的问题。这折射出对状态/错误分类精细化管理的需求。

2.  **Issue #4488: 将 ProductWorkflow 拆分为显式入口** ([链接](https://github.com/nearai/ironclaw/issues/4488))
    - **热度：** 获得2条评论，是架构讨论的核心。
    - **诉求：** 开发者 `danielwpz` 提出了对核心组件 `ProductWorkflow` 进行重构，将其拆分为 `submit`（提交）、`read`（读取）、`subscribe`（订阅）三个独立的“门”（doors）。该诉求已由今日合并的 PR #4506 实现。

---

#### 5. Bug 与稳定性

- **[严重] Issue #4502: 企业微信审批回复失效** ([链接](https://github.com/nearai/ironclaw/issues/4502))
    - **报告者：** @sunglow666
    - **描述：** 在企业微信群聊中，机器人请求工具审批后，用户回复 `y`、`yes` 或 `always` 无法完成授权，机器人会重复发送审批请求。这是一个阻断用户正常交互流程的严重Bug，影响了 WeCom 渠道的核心审批功能。
    - **状态：** 已提交 Issue，尚无关联的 fix PR。

- **[严重] Issue #4500: 渠道引导系统事件写入错误的会话** ([链接](https://github.com/nearai/ironclaw/issues/4500))
    - **报告者：** @sunglow666
    - **描述：** 在完成渠道配对后，系统欢迎消息被错误地写入了已有旧会话，而非新建的专属会话中。该Bug在 WeCom 和 Telegram 渠道均有复现，表明问题可能存在于更通用的抽象层。
    - **状态：** 已提交 Issue，尚无关联的 fix PR。

- **[轻度] Issue #4512: 并发沙箱信号量未获取** ([链接](https://github.com/nearai/ironclaw/issues/4512))
    - **报告者：** @saketh-are
    - **描述：** 发现 `job_semaphore`（用户级沙箱并发限制的信号量）在代码中被定义，但从未在任何地方调用 `.acquire()`，导致该限制机制形同虚设，可能存在资源竞争风险。
    - **状态：** 新提交的 Issue，尚无修复 PR。

- **[关注] Issue #4108: 夜间 E2E 测试失败** ([链接](https://github.com/nearai/ironclaw/issues/4108))
    - **描述：** 自动化测试报告显示前夜（2026-06-05）的端到端测试失败，虽未明确失败原因，但作为项目质量门禁，需开发团队优先排查。

---

#### 6. 功能请求与路线图信号

- **Issue #4491: 使用 Slack AI 流式传输交互状态** ([链接](https://github.com/nearai/ironclaw/issues/4491))
    - 请求提升 Slack 渠道的用户体验，从简单的“正在思考...”过渡到使用 Slack 的 “streaming” 能力来实时展示 AI 响应进度。这符合改善用户等待体验的大方向。关联的 PR #4490 已实现初步方案。

- **Issues from @sunglow666:** 来自 WeCom 渠道的持续反馈。
  - **Issue #4505: 群聊标题不具区分度** ([链接](https://github.com/nearai/ironclaw/issues/4505)): 修复了群聊/私聊分离后，多个群聊在 Web UI 侧边栏显示为相同标题，难以区分。
  - **Issue #4191: v0.29.0 阶段 WeCom 渠道验证报告** ([链接](https://github.com/nearai/ironclaw/issues/4191)): 一份详尽的验证报告，总结了 WeCom 渠道的多个待优化点，包括稳定性与交互细节。这构成了下一轮 WeCom 改进的基础路线图。

---

#### 7. 用户反馈摘要

- **正面反馈（含蓄）：** 从 Issue 提交的细节来看，如 #4505 “经过最近的修复”，说明用户认可了开发团队之前（#4194）对群聊/私聊分离的修复。
- **痛点明确：**
    - **审批流程断裂：** WeCom 渠道的审批回复功能完全失效（#4502），是当前最影响核心业务流程的体验问题。
    - **会话管理混乱：** 渠道引导消息写入错误会话（#4500）导致用户对话体验割裂，属于典型的 onboarding 流程缺陷。
    - **信息辨识困难：** Web UI 无法区分多个群聊会话（#4505），对于需要管理多个企业微信群组的运营人员而言非常不便。用户希望标题能基于群名而非机器人ID。
    - **权限可见性混乱：** 已关闭的 Issue #4198 指出，群聊中未配对的用户消息对管理员不可见，引发了对这是“预期行为”还是“功能缺失”的困惑。

---

#### 8. 待处理积压

- **⏳ PR #3708: 版本发布 PR** ([链接](https://github.com/nearai/ironclaw/pull/3708))
    - **状态：** 自2026-05-16起开放，已长达三周。
    - **重要性：** 此 PR 计划将 `ironclaw_common` 和 `ironclaw_skills` 发布为破坏性变更版本。该 PR 长期搁置可能阻碍了其他团队或项目的依赖更新。建议项目维护者尽快审阅合并，以推进外部使用者的体验。

- **⚠️ Issue #4191: WeCom 渠道深度验证报告** ([链接](https://github.com/nearai/ironclaw/issues/4191))
    - **风险：** 这是 @sunglow666 发布的综合性验证报告，尽管已有许多子 Issue 被关闭，但主 Issue 仍处于开放状态。建议开发团队根据此报告进行一次全面的回归测试，以确保 WeCom 渠道在 Reborn 架构迁移后功能完备且稳定。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，以下是基于 LobsterAI 项目在 2026年6月5日 数据生成的日报。

---

# LobsterAI 项目动态日报 | 2026年6月6日

## 今日速览

项目在2026年6月5日保持高度活跃，共合并了13个 Pull Request，发布了新的小版本2026.6.5。开发重心集中在提升Cowork协作模式的用户体验、修复关键Bug（如输入框内容丢失和覆盖）、以及增强语音输入和文件预览等核心功能。社区反馈的几项长期存在的Bug（内容丢失、脚本问题等）虽未直接关闭，但团队仍在持续推进修复工程。整体来看，项目正处于快速迭代、修复与功能增强并重的阶段，健康度良好。

## 版本发布

### **LobsterAI 2026.6.5**

- **发布时间**: 2026年6月5日
- **核心更新**:
    - **提升频道会话同步与清理**：改进了Cowork模式下频道会话的数据同步逻辑和清理机制，提升了协作稳定性。
    - **优化键盘快捷键系统**：对快捷键功能进行了全面检修，扩展了可触发的操作，并改善了用户交互体验。
- **破坏性变更**: 无
- **迁移注意事项**: 常规更新即可。

## 项目进展

今日共有13个PR被合并，显著推动了项目在多个方面的进展：

- **核心功能增强**:
    - **Artifacts (文件预览与展开面板)**：`#2114` 进行了重大改进，优化了Office文件（Word、PPT、Excel）的预览、缩放和布局，并支持了预览面板展开和HTML文件预览，显著提升了内容浏览体验。
    - **语音输入 (Voice Input)**：`#2113` 和 `#2118` 解决了macOS平台麦克风权限请求问题，并集成了经过认证的ASR（自动语音识别）语音输入功能，为Cowork模式增添了新的交互方式。
    - **键盘快捷键**：`#2108` 与版本发布中的更新一致，对快捷键系统进行了全面升级。
- **稳定性与Bug修复**:
    - **配置迁移修复**：`#2117` 修复了在更新后，用户从供应商处手动删除的模型会被重新添加的问题，通过版本追踪确保了配置的持久性。
    - **安全加固**：`#1534` 和 `#1535` 这两项安全相关的PR终于合并。前者防止了API代理日志泄露凭证和请求详情，后者为渲染进程访问KV存储增加了键白名单，有效提升了项目的纵深防御能力。
    - **IM消息组装修复**：`#2115` 修复了IM（即时消息）模式下，消息回复仅应基于当前轮次消息组装的问题，避免了上下文混乱。
- **功能新增**:
    - **设置页面统计面板**：`#1533` 在设置中添加了基于本地数据的会话使用统计面板，让用户能直观了解自己的使用情况。

## 社区热点

- **最受关注 Issue**: `#1487` “会话中调用python脚本出现问题，同样的skills仔claude code cli和其他地方都正常。” 该Issue距今已两个月，作者仍在期待回复。背后诉求是用户希望在LobsterAI内部调用外部工具（如Python脚本）时，能得到与其他平台一致的支持体验。这反映了用户对Agent能力成熟度和跨平台一致性的高要求。
    - 链接: [Issue #1487](https://github.com/netease-youdao/LobsterAI/issues/1487)

## Bug 与稳定性

以下是今日报告的三个活跃Bug，均出现在Cowork核心交互流程中，对用户体验影响较大：

1.  **【严重】编辑历史消息覆盖未发送草稿**: `#1472` 当用户输入框中有未发送内容时，点击“重新编辑”会直接覆盖且无任何确认提示，导致输入内容静默丢失。**（暂无直接关联的Fix PR）**
    - 链接: [Issue #1472](https://github.com/netease-youdao/LobsterAI/issues/1472)
2.  **【严重】切换视图导致输入框草稿丢失**: `#1471` 因去抖（debounce）机制，用户快速切换会话或视图时，输入框中的草稿内容因组件卸载而丢失。**（暂无直接关联的Fix PR）**
    - 链接: [Issue #1471](https://github.com/netease-youdao/LobsterAI/issues/1471)
3.  **【中等】会话中Python脚本调用失败**: `#1487` 用户报告在LobsterAI的对话会话中调用Python脚本失败，但在其他工具（如Claude Code CLI）中正常。**（该Issue已表态“需要更多信息”或“认可”）**
    - 链接: [Issue #1487](https://github.com/netease-youdao/LobsterAI/issues/1487)

## 功能请求与路线图信号

尽管今日无全新的功能请求，但合并的PR揭示了明显的路线图方向：
- **Artifacts增强**：`#2114` 对文件预览的大幅度改进表明团队正在将Artifacts作为核心体验进行打磨，未来可能支持更多文件类型或交互。
- **数据驱动功能**：`#1533` 在设置中增加使用统计面板，暗示未来可能会向用户提供更丰富的数据看板，用于分析自己的AI使用行为。
- **权限与安全强化**：`#1530` 和 `#1535` 的合并表明项目正在系统和流程上加强安全基线，这是进入更广泛企业级应用的必经之路。

## 用户反馈摘要

从今日活跃的Issue评论中，可以提炼出以下用户痛点：
- **数据安全与可预期性**：用户在“输入框草稿丢失”（#1471）和“编辑覆盖”（#1472）问题中，表达了对应用行为不可预期的失望。用户期望应用在任何操作前都应妥善保存用户已投入的工作，或在执行破坏性操作前给出明确提示。
- **工具链兼容性**：用户（#1487）期望LobsterAI作为一个AI助手平台，其脚本执行等核心Agent能力需要与主流工具（如Claude Code）保持一致的可靠性，否则会严重影响开发工作流的选择和信任。

## 待处理积压

以下两项安全/可靠性相关的PR在积压了两个月后终于被合并，非常值得关注。此外，仍有几个遗留的PR可能待处理：

- **`#1531` [CLOSED] feat(settings): replace theme color grid with compact circle selector**：主题色选择器的UI优化PR，已关闭，标志着UI细节优化仍在进行。
    - 链接: [PR #1531](https://github.com/netease-youdao/LobsterAI/pull/1531)
- **`#367` [CLOSED] fix: import mcp json streamable http configs**：一个解决MCP配置导入的PR，虽然已关闭，但时间跨度从3月到6月，表明此类底层配置导入曾是难点。
    - 链接: [PR #367](https://github.com/netease-youdao/LobsterAI/pull/367)
- **长期未响应的重要Issue**: **`#1487`** (Python脚本调用问题) 和 **`#1471`**、**`#1472`** (草稿丢失、覆盖问题) 自4月初创建以来，虽有维护者认可但始终未能被修复，且相关Bug复现路径清晰，应作为下一版本Bug修复的优先项。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 Moltis 项目数据生成的 2026-06-06 项目动态日报。

---

## Moltis 项目动态日报 (2026-06-06)

### 1. 今日速览

过去 24 小时，Moltis 项目表现出**中等活跃度**。社区提交了 3 个新的 Bug 报告和 1 个功能请求，同时贡献者提交了 4 个待合并的 PR，显示出积极的开发推进。一个关键 Bug (Telegram 流式输出混淆问题) 已得到修复，并合并了相应的修复 PR。总体来看，项目在修复问题和扩展功能（特别是容器化部署支持）方面稳步前进，社区反馈和开发者响应均保持健康节奏。

### 2. 版本发布

- **无新版本发布。**
- 最新版本无更新。

### 3. 项目进展

今日项目在修复关键 Bug 和增强基础设施方面取得明确进展。

- **[已合并] PR #1099: 分离 Telegram 的进度流与最终回复** ([链接](https://github.com/moltis-org/moltis/pull/1099))
  - **影响**: 这是一个重要的修复，解决了 Issue #1097 中报告的“编辑中流式输出干扰最终回复”的问题。
  - **进展**: 通过将 Telegram 频道的流式更新视为临时进度消息，并在流结束后删除，确保了最终回复的独立和清晰。这显著改善了 Telegram 用户的使用体验。
- **[待合并] PR #1089: 在会话恢复前截断工具结果** ([链接](https://github.com/moltis-org/moltis/pull/1089))
  - **进展**: 该 PR 旨在对会话历史记录中的工具及工具结果进行长度截断，然后再注入到与供应商绑定的聊天消息中。这将优化会话上下文管理，提升性能并降低因历史过长导致的错误风险。虽然尚未合并，但代码改动已覆盖多种核心场景，是项目向更稳健会话管理迈进的重要一步。

### 4. 社区热点

今日社区活跃度集中在新提交的 Bug 报告和功能请求上，虽然评论数较少，但反映了用户对特定使用场景的细致关注。

- **最受关注的 Bug**: **#1109 更新横幅未考虑 Docker 安装** ([链接](https://github.com/moltis-org/moltis/issues/1109)) 和 **#1108 Web UI 会话列表未显示日期** ([链接](https://github.com/moltis-org/moltis/issues/1108))
  - **分析**: 这两个 Bug 由同一名用户 (IlyaBizyaev) 提交，显示出用户对部署便利性和 UI 信息完整性的明确诉求。前者指出对于 Docker 部署的用户，“更新”横幅的检测逻辑无效，这可能导致 Docker 用户错过重要更新。后者则是一个典型的 UI 优化点，对于管理多天前会话的用户来说，只显示时间不显示日期会带来很大困扰。
- **带有修复 PR 的 Bug**: **#1109** 背后的问题与 PR **#1099** (已合并) 紧密相关，彰显了社区发现问题、开发者快速响应并解决问题的有效协作模式。

### 5. Bug 与稳定性

今日新报告了 3 个 Bug，其中 1 个严重问题已修复，其余 2 个为 UI/UX 相关问题。

| 严重程度 | Issue | 摘要 | 状态 | 是否有修复 PR |
| :--- | :--- | :--- | :--- | :--- |
| **高** | [#1097](https://github.com/moltis-org/moltis/issues/1097) | Telegram 编辑-原地流式输出将中间产出混入最终回复 | **已关闭** | 是，[PR #1099](https://github.com/moltis-org/moltis/pull/1099) 已合并 |
| **中** | [#1109](https://github.com/moltis-org/moltis/issues/1109) | 更新横幅未考虑 Docker 安装 | **开放** | 暂无 |
| **低** | [#1108](https://github.com/moltis-org/moltis/issues/1108) | Web UI 会话列表仅显示时间，不显示日期 | **开放** | 暂无 |

- **分析**: 核心流式输出 Bug 已快速解决，体现了项目对核心功能的重视。Docker 和 UI 的问题是典型的用户体验优化点，严重度不高，但社区已提出，预计后续版本会进行改进。

### 6. 功能请求与路线图信号

今日收到 1 个新的功能请求，同时从待合并的 PR 中可以窥见项目未来的功能方向。

- **新功能请求**:
  - **[#1107] 移动 Web UI 的多行文本输入** ([链接](https://github.com/moltis-org/moltis/issues/1107)): 用户请求为移动端 Web UI 增加多行输入支持。这是一个提升移动端用户体验的直接改进，很可能在下一个 UI 迭代中被纳入。
- **路线图信号 (来自待合并 PRs)**:
  - **Podman 支持强化**: [PR #1106](https://github.com/moltis-org/moltis/pull/1106) 为沙盒加入了 Podman 的逃逸机制支持、改进诊断和部署兼容性。这表明项目正积极扩展其容器化运行环境的选择。
  - **容器化部署的稳健性**: [PR #1105](https://github.com/moltis-org/moltis/pull/1105) 修复了 Docker 沙盒文件系统工具的降级问题，确保在主机挂载不可用时有可靠的容器内复制回退。这增强了 Docker 部署的稳定性。
  - **模型偏好管理**: [PR #1104](https://github.com/moltis-org/moltis/pull/1104) 允许用户替换已偏好的模型，并支持清空偏好，提供了更灵活的用户模型选择管理。

### 7. 用户反馈摘要

- **正面反馈 (间接)**: Issue #1097 中的用户 (s-salamatov) 详尽地描述了 Bug，其最终被快速修复并关闭，这表明项目维护者对用户报告的细粒度 Bug 响应积极且有效。
- **体验痛点**:
  - **部署与管理**: Issue #1109 指出 Docker 用户无法获得正确的更新提示，这是一个影响部署维护的痛点。
  - **信息呈现**: Issue #1108 反映了当前 Web UI 在信息呈现上的缺陷，对于需要回顾过往会话的用户来说，缺乏日期信息造成了显著不便。
  - **移动端适配**: Issue #1107 明确表达了移动端用户在输入长文本时的困难。

### 8. 待处理积压

当前所有开放 Issues 和 PRs 均创建于 1-5 天前，没有出现长期积压无人响应的重要项目。项目维护者对社区反馈的响应速度良好。建议维护者关注以下新提交的开放项目：

- **Issues**: **#1109** 和 **#1108** (Docker 更新横幅与 UI 日期问题)，由同一用户集中提出，建议优先排期修复。
- **PRs**: **#1106** 和 **#1105** (Podman 支持与 Docker 稳健性) 这两个 PR 明显增强了 Moltis 的容器化部署能力，对于项目吸引更多企业级或自托管用户至关重要，建议尽快审阅合并。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-06-06

## 今日速览

CoPaw 项目在过去 24 小时内保持高活跃度：共处理 21 条 Issue（新开/活跃 17 条，关闭 4 条）和 24 条 PR（待合并 9 条，已合并/关闭 15 条）。核心团队和社区贡献者协同推进了多项关键 Bug 修复（包括浏览器启动稳定性、LaTeX 渲染、Yuanbao 通道兼容性等），同时收录了多位首次贡献者的 PR 以丰富安全与 UI 功能。无新版本发布，但修复密度和社区参与度均属近期高点。

## 版本发布

**无** —— 过去 24 小时无新版本发布。

## 项目进展

今日合并/关闭的重要 PR 涵盖功能扩展、安全增强、UI 优化及跨环境兼容性修复：

- **安全加固**  
  - [#4026](https://github.com/agentscope-ai/QwenPaw/pull/4026)（已合并）：新增 `write_file` 的文件状态感知守卫，防止覆盖非空文件。  
  - [#3403](https://github.com/agentscope-ai/QwenPaw/pull/3403)（已合并）：修复 gunicorn 启动时因 provider 初始化过早导致的崩溃。

- **浏览器与工具修复**  
  - [#4944](https://github.com/agentscope-ai/QwenPaw/pull/4944)（已合并）：增加浏览器 CDP 超时参数并隔离不同浏览器用户数据目录，提升 `browser_use` 启动稳定性。  
  - [#4905](https://github.com/agentscope-ai/QwenPaw/pull/4905)（已合并）：为 `browser_control` 添加页面坐标点击支持。

- **UI/前端体验**  
  - [#4765](https://github.com/agentscope-ai/QwenPaw/pull/4765) 与 [#4766](https://github.com/agentscope-ai/QwenPaw/pull/4766)（已合并）：优化安全页面 shield 图标居中、规则表列宽及环境变量页面滚动条闪烁问题。  
  - [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972)（已合并）：启用 KaTeX 插件，修复 LaTeX 公式渲染异常。

- **通道与插件**  
  - [#4934](https://github.com/agentscope-ai/QwenPaw/pull/4934)（已合并）：新增 OpenSandbox 插件，支持在沙箱内执行 shell 命令。  
  - [#1240](https://github.com/agentscope-ai/QwenPaw/pull/1240)（已合并）：将状态存储从 JSON 文件迁移至 SQLite，提升抗损坏能力。

这些 PR 使项目在安全性、跨环境稳定性、前端易用性和扩展性上均向前迈进一步，尤其修复了长期存在的 `gunicorn` 崩溃和状态文件损坏等严重问题。

## 社区热点

今日讨论最活跃的 Issue 排名如下：

1. **[#4754](https://github.com/agentscope-ai/QwenPaw/issues/4754) [已关闭]** — 打包方式（7 条评论）  
   **诉求**：用户询问官方两种 Windows 桌面客户端（标准版 vs Tauri 版）的区别，以及如何自行打包成 exe。反映用户对部署方案和版本差异的困惑。

2. **[#4919](https://github.com/agentscope-ai/QwenPaw/issues/4919) [已关闭]** — `browser_use` 启动失败：CDP 超时 + 浏览器闪退（6 条评论）  
   **诉求**：Win10 用户在使用 Playwright 管理浏览器时遇到启动超时，最终只能靠 `playwright-cli` 兜底。暴露了 CDP 连接和浏览器配置兼容性问题。

3. **[#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) [开放]** — 左侧会话界面列顺序调整（5 条评论）  
   **诉求**：用户希望将 “更新时间” 列左移，将 ID/Session ID 右移，因为后两者对普通用户无价值。已收到 [PR #4975](https://github.com/agentscope-ai/QwenPaw/pull/4975) 的回应。

4. **[#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) [开放]** — 执行过程陷入死循环（4 条评论）  
   **诉求**：v1.1.10 用户报告 agent 在任务中无限循环无法退出，急需修复。

社区活跃度高，用户反馈集中在**部署便捷性**、**关键功能稳定性**和**UI 易用性**三方面。

## Bug 与稳定性

以下为今日报告的 Bug，按严重程度排列：

| 严重程度 | Issue 编号 | 标题 | 状态 | 是否有 Fix PR |
|----------|------------|------|------|---------------|
| 🔴 阻断 | [#4967](https://github.com/agentscope-ai/QwenPaw/issues/4967) | 执行过程陷入死循环，无法退出 | 开放 | 无 |
| 🔴 阻断 | [#4968](https://github.com/agentscope-ai/QwenPaw/issues/4968) | subprocess fork 因虚拟内存泄漏导致 “Cannot allocate memory” | 开放 | 无 |
| 🔴 阻断 | [#4970](https://github.com/agentscope-ai/QwenPaw/issues/4970) | `loop_config.json` / `prd.json` 损坏导致整个 Agent 会话崩溃 | 开放 | 无 |
| 🟡 严重 | [#4976](https://github.com/agentscope-ai/QwenPaw/issues/4976) | v1.1.10 wheel 中缺少 Yuanbao 通道所需的 proto 文件 | 开放 | 无 |
| 🟡 严重 | [#4977](https://github.com/agentscope-ai/QwenPaw/issues/4977) | protobuf 兼容性：`including_default_value_fields` 在低版本中不支持 | 开放 | 无 |
| 🟡 严重 | [#4978](https://github.com/agentscope-ai/QwenPaw/issues/4978) | `AuthBindRsp` 缺少 `connectId` 字段定义导致连接跟踪失败 | 开放 | [#4983](https://github.com/agentscope-ai/QwenPaw/pull/4983) |
| 🟡 严重 | [#4979](https://github.com/agentscope-ai/QwenPaw/issues/4979) | `streaming_enabled=True` 导致 Yuanbao 回复被静默丢弃 | 开放 | [#4982](https://github.com/agentscope-ai/QwenPaw/pull/4982) |
| 🟡 严重 | [#4980](https://github.com/agentscope-ai/QwenPaw/issues/4980) | `SendC2CMessage` 始终返回 “bot_id is required” | 开放 | 无 |
| 🟠 中等 | [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962) | DeepSeek API 回复总是折叠在思考过程中 | 开放 | 无 |
| 🟠 中等 | [#4832](https://github.com/agentscope-ai/QwenPaw/issues/4832) | Shell 命令子进程缺少 CREATE_NO_WINDOW 标志导致 cmd 窗口闪烁 | 开放 | 无 |
| 🟢 轻微 | [#4959](https://github.com/agentscope-ai/QwenPaw/issues/4959) [已关闭] | LaTeX 公式显示异常 | 已关闭 | [#4972](https://github.com/agentscope-ai/QwenPaw/pull/4972) |

**分析**：Yuanbao 通道相关的 5 个 Bug（#4976~#4980）集中爆发，涉及 proto 文件缺失、protobuf 兼容性、字段定义、流式响应处理等，表明该通道在 v1.1.10 中可能存在测试覆盖不足。已有 2 个对应修复 PR（#4982, #4983）提交。此外，死循环和内存泄漏两个阻断性 Bug 尚未有修复方案，需重点关注。

## 功能请求与路线图信号

| Issue 编号 | 功能描述 | 关联 PR | 可能进入下一版本的信号 |
|------------|----------|--------|----------------------|
| [#4770](https://github.com/agentscope-ai/QwenPaw/issues/4770) | 左侧会话列顺序可自定义（将更新时间提前） | [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975)（开放） | 已有实现 PR，合并可能性高 |
| [#4963](https://github.com/agentscope-ai/QwenPaw/issues/4963) | Cron 任务支持直接执行脚本/Shell 命令 | 无 | 用户需求明确，但尚未有实现 |
| [#4974](https://github.com/agentscope-ai/QwenPaw/issues/4974) | 为每个 Agent 配置头像并在 UI 各位置统一显示 | 无 | 符合主流聊天工具习惯，可能被采纳 |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | 增加会话侧边栏，支持一键切换会话 | 无 | 涉及前端较大改动，需评估 |
| [#4965](https://github.com/agentscope-ai/QwenPaw/issues/4965) | 合并同品牌 provider 卡片，用下拉框选择计划/端点 | 无 | UI 精简优化，被纳入可能性中等 |

此外，PR [#4973](https://github.com/agentscope-ai/QwenPaw/pull/4973)（开放）新增了 129 个单元测试用例，覆盖 `local_models`、`providers`、`tunnel`、`utils` 等模块，表明团队在持续提升代码质量。

## 用户反馈摘要

从 Issue 评论区提炼的真实用户声音：

- **打包与部署困惑**（#4754）：用户对官方提供的两种 Windows 客户端版本（标准版 vs Tauri 版）的差异不清楚，希望有更清晰的文档说明，并想自己复现打包过程。
- **局域网访问受阻**（#4960）：用户尝试用手机通过局域网访问桌面版控制台失败，即使已添加白名单、关闭防火墙，仍无法连接。这说明网络访问配置指引或默认绑定地址可能存在问题。
- **DeepSeek 回复折叠**（#4962）：用户抱怨每次都需要手动展开思考过程才能看到实际回复，体验不佳。暗示流式输出与模型思考内容的展示逻辑需要优化。
- **内存泄漏导致系统崩溃**（#4968）：Ubuntu 用户报告经过 1200+ 对话后 agent fork 失败，显示 `Cannot allocate memory`，严重影响长时间运行场景。
- **Yuanbao 通道完全不可用**（#4976~#4980）：多位用户反馈安装 v1.1.10 后该通道无法正常工作（缺少文件、protobuf 错误、消息发送失败），属于回归性严重问题。

## 待处理积压

以下为可能被忽视的重要开放条目：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 说明 |
|------|------|------|----------|----------|------|
| Issue | [#4744](https://github.com/agentscope-ai/QwenPaw/issues/4744) | 桌面客户端 macOS Tauri 不支持 Intel 芯片？ | 2026-05-28 | 2026-06-05 | 用户询问 Intel Mac 支持情况，未获官方回复。 |
| Issue | [#4705](https://github.com/agentscope-ai/QwenPaw/issues/4705) [已关闭] | Mission Phase 2 循环迭代不退出（已关闭但问题可能未彻底解决） | 2026-05-26 | 2026-06-05 | 虽已关闭，但今日新报告的死循环 Issue #4967 有相似特征，建议复盘。 |
| PR | [#4822](https://github.com/agentscope-ai/QwenPaw/pull/4822) | fix(crons): fix share_session cron agent tasks producing empty traces | 2026-05-29 | 2026-06-05 | 持续开放 8 天未合并，cron 任务相关 Bug 影响定时任务用户。 |
| PR | [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) | Decouple plugin loader initialization from agent startup | 2026-06-02 | 2026-06-05 | 涉及 Tauri/PyInstaller 冻结环境，对桌面客户端打包友好，值得推进。 |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 2026-06-06

## 今日速览

过去 24 小时内 ZeroClaw 社区保持了 **极高活跃度**：Issues 更新 50 条（新开/活跃 44 条，关闭 6 条），PR 更新 50 条（待合并 37 条，已合并/关闭 13 条），无新版本发布。项目核心方向集中在 **安全增强（OIDC、执行确认、隔离模式）**、**可观测性重构**、**渠道扩展（SMS、社交平台）** 以及 **MCP/Skills/Plugin 管理体验提升**。大量高风险 RFC 进入 accepted 状态，标志着 0.9.0 架构规划进入实质推进阶段。

## 项目进展

### 关键合并与关闭
今日共有 **13 个 PR 被合并或关闭**，未出现在下方列表中的高价值合井包括：
- **安全层可插拔化**（#7142 tracking）相关子 PR 取得合并进展。
- **OIDC 认证提供者**（#7141 tracking）首个 PR 已合并。
- **Shell 命令执行确认层级**（#7155）的初始实现 PR 已合并。

### 重要功能推进
| PR 编号 | 标题 | 摘要 |
|--------|------|------|
| #7233 | Structured Observability Enhancement — Rich Events, OTel Trace Correlation, and Bridge Refactoring | 重构可观测层，增加信道/Agent/LLM I/O 上下文，实现 OTel 跨度关联（RFC #7232） |
| #7229 | feat(web): MCP, Skills, Plugins & Providers dashboard tabs | 为 Web UI 新增四个管理标签页，支持 MCP 连接状态、Skills 加载、Plugin 生命周期及 Provider 配置 |
| #7265 | feat(channels): add Twilio, Plivo, Telnyx, Sinch & Vonage SMS channels | 一次提交 5 个短信渠道（schema v3），支持签名验证 Webhook |
| #7270 | feat(channels): add Mastodon, Rocket.Chat, Zulip & Lemmy polling channels | 新增 4 个社交/聊天渠道，基于 REST API 拉取模式 |
| #7260 | feat(providers): add 7 OpenAI-compatible providers under schema v3 | 扩展 7 个兼容 Provider（Morph、GitHub Models、Upstage 等） |
| #7267 | feat(config): per-field editing for [[mcp.servers]] | 允许 Web/TUI 逐字段编辑 MCP 服务器配置，无需手写 TOML |
| #7277 | feat(plugins): add Shazam WASM plugin (pilot) | 第二个参考 WASM 插件，展示 Extism 沙盒集成模式 |

### 修复与稳定性
- **#7258 fix(runtime): tombstone killed ACP sessions** — 防止被杀死的 ACP 会话被悄悄复活。
- **#7254 fix(runtime): strip think blocks before native tool-call output** — 避免 `think` 块泄漏到工具调用输出。
- **#7261 fix(config): redact nested object-array secrets** — 修复嵌套机密字段在配置显示中未脱敏的漏洞。
- **#7123 fix(zerocode/channels/tools): avoid UTF-8 char-boundary panics in text truncation** — 修复 CJK 等多字节字符截断崩溃。
- **#7247 fix(web): fix paired_tokens drift false-positive** — 修复 `paired_tokens` 字段误报配置漂移。

## 社区热点

### 最活跃 Issue（按评论数排序）

1. **#6808** — *RFC: Work Lanes, Board Automation, and Label Cleanup*（9 条评论）  
   > 提议轻量级 PR 通道和看板自动化，减少维护者人工跟踪负担。社区对标签清理规则与 CI 集成有激烈讨论。

2. **#6969** — *RFC: unified output routing model*（7 条评论）  
   > 用户从 Letta 迁移后强烈需要“按用户偏好选择输出通道/路由”的能力，涉及 agent send_via 工具设计。

3. **#5601** — *Add subscription-native OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax*（6 条评论）  
   > 扩展 OAuth 登录支持，降低 API Key 管理风险；已获得首次 👍，但长期 blocked。

4. **#7155** — *Add per-execution confirmation tier for high-risk shell commands*（4 条评论）  
   > 增加“允许但每次确认”的中间安全等级，参考 Claude Code 策略，社区普遍支持。

5. **#7142** — *Expose the security enforcement layer as a pluggable provider interface*（4 条评论）  
   > 架构级追踪 Issue，讨论如何将安全内建功能抽象为 trait，目标 0.9.0。

6. **#7141** — *OIDC Authentication Provider support for the RPC/WSS transport*（4 条评论）  
   > 配合上一条，OIDC 认证是可插拔安全层的第一个实现。

### 最活跃 PR
| PR 编号 | 标题 | 特点 |
|--------|------|------|
| #7229 | feat(web): MCP, Skills, Plugins & Providers dashboard tabs | XL 尺寸，高风险，社区关注 UI 操作便捷性 |
| #7233 | Structured Observability Enhancement | XL 尺寸，高风险，带完整 RFC，与 #7232 联动 |
| #7265 / #7270 | 新增 5 SMS + 4 社交渠道 | 单 PR 集成多个渠道，引发对不同平台 API 差异的讨论 |
| #7244 | reinforce tool formatting prompts and add robust JSON fallback parser | 针对 Gemini/Discord 场景的 JSON 解析兜底，工具使用稳定性提升 |

## Bug 与稳定性

### 严重 Bug（S1/S2）
| Issue | 标题 | 状态 | 说明 |
|-------|------|------|------|
| #7059 | excise "default model provider" credential/URL fallback from channel orchestrator | **open** / S2 | 旧架构遗留的默认凭据回退与 V3 schema 冲突，导致凭据泄漏风险 |
| #6120 | Onboarding: choosing OpenAI Codex prompts for OpenAI API key instead | **已关闭** | 造成工作流阻塞的严重 Bug，已修复 |
| #7240 | fix(zerocode): make quickstart provider alias editable | 已提 PR | 修复 Quickstart 硬编码别名导致的配置验证失败 |
| #7247 | fix(web): fix paired_tokens drift false-positive and make ReloadBanner dismissable | 已提 PR | `paired_tokens` 大小写不匹配导致持续误报配置漂移 |

### 其他稳定性修复
- **#6914** — `allowed_tools` 在调用分发时未执行，现已通过 PR 修复（状态 accepted）。
- **#6916** — Shell 子进程无内存限制导致容器 OOM，RFC 已接受，需后续 PR。
- **#6714** — Skill 审计中远程 Markdown 链接误报，已接受改进提案。

## 功能请求与路线图信号

### 即将进入 0.9.0 的核心 RFC（状态均为 accepted）
- **安全增强**  
  - #7155：Shell 命令确认层级 + 模式策略  
  - #7142：可插拔安全提供者接口  
  - #7141：OIDC 认证  
  - #6916：子进程内存限制  
  - #6971：安全 UX 与凭据边界  
- **可观测性**  
  - #7232：结构化事件、OTel 关联  
- **互操作性**  
  - #7218：A2A Agent 发现（`.well-known/agent-card.json`）  
- **渠道扩展**  
  - #7265 / #7270：9 个新渠道（SMS + 社交）已实现  
- **提供者生态**  
  - #5601：4 个供应商 OAuth 支持（blocked）  
  - #7260：7 个 OpenAI 兼容提供者  
- **核心精简**  
  - #6165：通过外部集成（Skills/MCP）替代内建工具代码  

### 用户呼声较高的新需求
- **#6065**：XCode 集成（MCP 到 XCode）  
- **#7024**：Office 文档解析 WASM 插件（DOCX/XLSX/PPTX）  
- **#7089**：Windows Shell 主机可配置（PowerShell vs cmd.exe）  
- **#7100**：Per-model 能力与上下文窗口配置  
- **#5842**：Codex CLI `extra_args` 安全验证  
- **#5907**：LSP 支持（opt-in）  

## 用户反馈摘要

- **迁移痛点**（#6969）：从 Letta 迁移的用户反映“输出路由控制”缺失，希望 agent 能按用户偏好或指令选择发送通道（vs 固定渠道）。
- **配置验证缺失**（#6120 / #6416）：Quickstart 在设置 OpenAI Codex 时错误地请求 OpenAI API 密钥，用户感到困惑；建议 Quickstart 预检配置兼容性。
- **允许列表不生效**（#6914）：用户发现 `allowed_tools` 字段存在但未在运行时执行，导致安全预期落空。
- **技能审计误报**（#6714）：真实 Marketplace 插件因引用文档 URL（`.md` 后缀）被审计阻止，用户建议区分引用 vs 潜在风险。
- **Windows 支持期待**（#7089）：Windows 用户希望由 cmd.exe 切换到 PowerShell 或可配置，以兼容现代命令行行为。
- **OAuth 便捷性**（#5601）：多个用户希望增加免费/付费订阅商的 OAuth 登录，减少 API Key 管理负担。

## 待处理积压

### 长期 Blocked / Needs Maintainer Review 的重要 Issue
| Issue | 标题 | 阻塞原因 | 影响 |
|-------|------|----------|------|
| #5601 | 4 个供应商 OAuth 支持 | 等待维护者审查，已 blocked 逾 2 个月 | 提升易用性，降低密钥泄漏风险 |
| #6165 | 精简核心代码（外部集成） | 需要架构决策（RFC 已 accepted） | 影响代码库维护成本 |
| #5907 | LSP 支持 | 待维护者批准方向 | 改善代码生成质量，尤其本地模型 |
| #6715 | 删除无用分支 | 简单操作但无人执行 | 仓库混乱，影响 fork 管理 |
| #6279 | 改进 Release 里程碑选择标准 | 未获得足够关注 | 可能导致关键修复延迟发布 |
| #5908 | 容器镜像 CI/CD | 需 CI 维护更新 | 确保 Debian 镜像可用性 |
| #6074 | 追踪 153 个被回滚的提交 | 需要手动整理恢复 | 丢失多个已合并的功能和修复 |
| #6917 | Composio action-scope 过滤 | 等待维护者审查 | 细粒度权限控制缺失 |

建议维护团队优先处理带有 `needs-maintainer-review` 标签且已 blocked 超过 2 周的高风险 Issue，尤其是 #5601（社区赞数 1）和 #6165（架构层面的长期诉求），以避免社区贡献流失。

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*