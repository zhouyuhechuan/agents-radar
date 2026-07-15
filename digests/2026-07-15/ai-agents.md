# OpenClaw 生态日报 2026-07-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-07-15 01:45 UTC

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

# OpenClaw 项目动态日报 — 2026-07-15

## 1. 今日速览

过去 24 小时项目保持极高活跃度：共处理 **500 条 Issue 更新**（新开/活跃 343，已关闭 157）和 **500 条 PR 更新**（待合并 337，已合并/关闭 163）。社区焦点集中在 **v2026.7.1 启动迁移崩溃** 的多个 P0 级 Bug 报告，同时长期功能需求（跨平台桌面应用、安全增强）讨论持续升温。项目整体健康度尚可，但稳定性面临显著压力，需尽快解决升级阻断问题。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日虽无正式发布，但以下关键 PR 取得实质推进，部分已进入维护者审查状态：

- **[PR #107903]** (feat(agents): OpenClaw system-agent delegation) — 系统代理委托 Phase 2，为普通代理提供配置通道的安全路径。关联 Issue #107237。
- **[PR #107905]** (fix(ui): reject non-decimal input in toNumber()) — 修复 UI 中 `toNumber()` 接受十六进制/科学计数法的安全旁路，影响 10+ 调用点。
- **[PR #107605]** (fix(agents,cron): remove pattern field from model-facing cron tool schema) — 修复 cron 工具 JSON Schema 与 llama.cpp 解析器不兼容的问题（#107449），移除冗余 `pattern` 字段。
- **[PR #107626]** (fix(qa-lab): reject hex/exponent Telegram SUT uid env values) — 确保 QA 实验室环境变量仅接受纯十进制整数。
- **[PR #97224]** (fix(harness): add Codex pre-tool loop relay opt-out) — 为 Codex Harness 添加原生 PreToolUse 中继的 opt-out 配置，已标记“ready for maintainer look”。
- **[PR #92294]** (fix(codex): keep OpenClaw exec when native surface has no environment) — 修复 Codex 运行时 exec 工具不可用的问题，已进入审查。
- **[PR #88919]** (fix: allow preflight compaction to reenter session locks) — 允许内嵌预检压缩重入同一进程的写入锁，解决会话锁死。

此外，今日有 **163 个 PR 被合并/关闭**（概览数据），表明项目修复效率较高。

## 4. 社区热点

| # | Issue / PR | 讨论热度 | 核心诉求 |
|---|------------|----------|----------|
| 1 | **[#75]** Linux/Windows Clawdbot Apps (113 评论, 👍81) | 最高 | 用户强烈要求提供 Linux 和 Windows 版桌面应用，功能对标 macOS。 |
| 2 | **[#94518]** DeepSeek 缓存命中率 <10% 后 6.x 升级 (9 评论, 👍10) | 高 | 升级后边界感知缓存破坏前缀匹配，导致缓存命中率暴跌，影响成本和使用体验。 |
| 3 | **[#107133]** Memory Core embedding_cache 冲突永久阻塞网关启动 (6 评论, 👍3) | 极高 | v2026.7.1 启动时遗留侧车迁移回滚，导致永久阻塞，网关 crash-loop。 |
| 4 | **[#107227]** 2026.7.1 启动迁移 gate 致命且 doctor 无法修复 (6 评论, 👍1) | 极高 | 升级后网关拒绝启动，文档缺乏可靠修复方案。 |

## 5. Bug 与稳定性

以下按严重程度排列，标注是否已有修复 PR：

| 严重程度 | Issue # | 描述 | 状态 |
|----------|---------|------|------|
| **P0** | [#107227] | 2026.7.1 启动迁移 gate 致命，`openclaw doctor` 无法修复，网关 crash-loop | 无公开修复 PR |
| **P0** | [#107133] | Memory Core embedding_cache 冲突永久阻塞网关启动 | 已关闭（作者提交临时 workaround 后关闭，但根本原因未解决） |
| **P0** | [#107220] | 遗留 memory 侧车 meta/chunks 冲突被视为 fatal，files 却自动解决 | 无公开修复 PR |
| **P0** | [#107330] | Windows 11 执行 `openclaw update` 后崩溃 | 已关闭（提交者未提供更多信息） |
| **P0** | [#101290] | CLI 启动预检可能损坏实时状态数据库（macOS），导致 "database disk image is malformed" | 无公开修复 PR |
| **P1** | [#87744] | Codex-backed Telegram 反复超时，`turn/completed` 无法到达 | 无公开修复 PR |
| **P1** | [#102020] | 第二消息失败："reply session initialization conflicted"（跨通道） | 无公开修复 PR |
| **P1** | [#107449] | cron 工具 JSON Schema 与 llama.cpp 解析器不兼容 (`pattern: "\S"`) | **已有 PR #107605 修复，待合并** |
| **P1** | [#77012] | WebChat 会话转录每轮被覆盖（5.2 回归） | 无公开修复 PR |
| **P1** | [#90944] | sessions_yield 回复记录但未投递，用户收到子代理摘要 | 无公开修复 PR |
| **P1** | [#92769] | 推理内容 `reasoning`/`reasoning_details` 从消息历史中丢失（MiniMax M3） | 无公开修复 PR |
| **P2** | [#90213] | 遗留状态迁移警告反复出现，`openclaw doctor --fix` 无法解决 | 无公开修复 PR |
| **P2** | [#90414] | `agentmemory__memory_search` 返回 "index metadata is missing" | 无公开修复 PR |
| **P2** | [#102749] | 启动遗留状态迁移无法收敛（.migrated 存档已存在） | 已关闭（作者自行解决） |

## 6. 功能请求与路线图信号

| Issue # | 功能 | 用户价值 | 疑似路线图优先级 |
|---------|------|----------|------------------|
| **#75** | Linux/Windows 桌面应用 | 补齐跨平台体验，扩大用户覆盖 | 高（113 评论，长期未分配） |
| **#7707** | 内存信任标记（按来源标记信任级别） | 防止记忆投毒攻击，提升安全性 | 中（需安全审查） |
| **#10659** | 掩码秘密（Agent 可用但不可见 API Key） | 防止凭据泄漏与提示注入 | **高**（已有 4 个 👍，需产品决策） |
| **#6615** | 执行审批黑名单 | 实现“允许除 X 外所有命令”策略 | 中（需安全审查） |
| **#66252** | 按代理独立配置 TTS/STT（多语言支持） | 多代理场景下灵活语言/语音 | 中（需产品决策） |
| **#8355** | 流式 TTS 管道（句子级 LLM→TTS→Audio） | 降低语音通话延迟，提升体验 | 中（需维护者审查） |
| **#11665** | Webhook 钩子支持多轮会话（复用 sessionKey） | 文档宣称支持但实际不工作 | 高（已有链接 PR） |
| **#9986** | 上下文超限时触发模型回退 | 避免会话因长度限制冻结 | 中（需产品决策） |
| **#45508** | WebChat 自托管 TTS/STT（路由经过网关） | 支持企业自建语音方案 | 中（有 2 个 👍） |
| **#82548** | AI 安全与质量可观测性事件 | 帮助运营监控非确定性行为、提示注入 | 低（需安全审查） |

## 7. 用户反馈摘要

从 Issues 评论与 PR 摘要中提炼的真实反馈：

- **升级挫折感强烈**：多位用户反映 v2026.7.1 更新后网关完全无法启动（#107227、#107133、#107330），且官方提供 `openclaw doctor` 修复路径无效，导致生产环境中断。
- **多代理场景痛点**：用户抱怨子代理 announce 无法优雅关闭（#8299）、Webhook 多轮会话未按文档工作（#11665）、sessions_yield 投递混乱（#90944）。
- **模型兼容性焦虑**：llama.cpp 用户遇到工具 schema 解析失败（#107449），Codex/OpenAI 用户遭遇缓存命中率下降（#94518）、非十进制输入安全风险（#107905）。
- **WebChat/移动端体验退化**：iOS/WebChat 消息不触发回复（#97983）、会话转录被覆盖（#77012）、WhatsApp 图片处理卡顿（#96834）。
- **长期需求未被满足**：社区对跨平台桌面客户端（#75）的呼声持续 6 个月，113 条评论但无明确时间表。安全功能（内存标记、掩码秘密）讨论热烈但推进缓慢。

## 8. 待处理积压

以下 Issue / PR 长期无维护者响应或需要紧急关注：

| 项目 | 创建时间 | 最后更新 | 优先级 | 备注 |
|------|----------|----------|--------|------|
| **Issue #75** (Linux/Windows Apps) | 2026-01-01 | 2026-07-14 | 高 | 113 评论，81 个 👍，无分配维护者，无 PR |
| **Issue #7707** (Memory Trust Tagging) | 2026-02-03 | 2026-07-14 | 中 | 需安全审查和产品决策 |
| **Issue #10659** (Masked Secrets) | 2026-02-06 | 2026-07-14 | 高 | 4 个 👍，需产品决策 |
| **PR #102574** (docs: use American spelling) | 2026-07-09 | 2026-07-15 | 低 | 简单文档 PR，7 天无进展 |
| **PR #86655** (feat(claude): claude-bridge harness) | 2026-05-25 | 2026-07-15 | 中 | 等待作者更新，合并风险较高 |
| **PR #88193** (tighten final Telegram DM recovery) | 2026-05-30 | 2026-07-15 | 中 | 需要更多截图证据 |
| **Issue #94518** (DeepSeek cache hit rate) | 2026-06-18 | 2026-07-15 | 高 | 10 个 👍，仍无修复 PR |

---

💡 **维护者提醒**：v2026.7.1 的启动迁移问题（#107227、#107133、#107220）已导致多位用户无法正常使用，建议优先排查并发布 hotfix。同时 #75 桌面应用需求强烈，考虑纳入 Q3 路线图。

---

## 横向生态对比

好的，作为资深技术分析师，以下是根据您提供的各项目社区动态摘要生成的横向对比分析报告。

---

### **个人 AI 智能体开源生态横向分析报告 (2026-07-15)**

#### **1. 生态全景**

当前，个人 AI 助手/自主智能体开源生态正处于 **从“功能可用”向“工程可靠”与“安全可信”的过渡期**。各项目普遍遭遇了因快速迭代带来的 **稳定性阵痛**，如 OpenClaw 和 CoPaw 的 v2026.7.1 版本均出现了阻断性升级问题，导致用户生产环境受影响。与此同时，社区关注的焦点开始从基础的“Agent 能做什么”转向 **“如何安全、稳定、可观测地规模化使用 Agent”**，具体表现在对多租户、沙箱隔离、提示注入防护和复杂工作流自动化的强烈需求上。整个生态呈现出 **核心平台竞争激烈（OpenClaw 系）、细分领域加速分化（如 Telege、企业协作）** 的态势。

#### **2. 各项目活跃度对比**

| 项目名称 | 今日活跃 Issues (新开/活跃) | 今日活跃 PRs (待合并) | 今日合并/关闭 PRs | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (343) | 500 (337) | 163 | 无 | **尚可，但有危机** (P0 升级 Bug 阻断使用，社区反馈强烈) |
| **NanoBot** | 13 (3) | 50+ (数据不全) | 47 | 无 | **良好** (Bug 修复效率高，WebUI 体验持续优化) |
| **Hermes Agent** | 50 (7) | 50 (46) | 43 | 无 | **极好** (清理积压高效，安全与稳定性修复迅速) |
| **PicoClaw** | 3 (3) | 9 (4) | 5 | 无 | **良好** (社区健康，修复与缓存功能推进积极) |
| **NanoClaw** | 0 | 26 (19) | 7 | 无 | **中高，但有积压** (开发密集，但 PR 审核存在瓶颈) |
| **NullClaw** | 0 | 0 | 0 | 无 | **静默** (无活动) |
| **IronClaw** | 48 (高活跃) | 50 (高活跃) | 高合并数 | 无 | **高活跃度冲刺期** (核心功能整合与稳定性加固并行) |
| **LobsterAI** | 0 | 3 (0) | 3 | 无 | **中等，偏向维护** (清理历史遗留 Issue 与关键回溯修复) |
| **TinyClaw** | 0 | 0 | 0 | 无 | **静默** (无活动) |
| **Moltis** | 较低 | 12 (4) | 8 | **有 (v20260714.11)** | **优秀** (版本迭代迅速，Bug 修复与功能增强并重) |
| **CoPaw** | 50 (16) | 50 (24) | 26 | **有 (v2.0.0.post2)** | **良好** (快速响应 v2.0 回归问题，发布补丁修复) |
| **ZeptoClaw** | 0 | 0 | 0 | 无 | **静默** (无活动) |
| **ZeroClaw** | 29 (23) | 50 (38) | 12 | 无 | **高活跃度，工程驱动** (SOP 引擎趋于成熟，安全与多租户是焦点) |

#### **3. OpenClaw 在生态中的定位**

*   **生态核心参照与基石**：OpenClaw 是整个生态中体量最大、社区最活跃的“基础框架”。其他多个项目（如 LobsterAI）明确表示在进行针对 OpenClaw Agent 运行时的回溯修复，凸显了其作为 **通用 Agent 运行时的事实标准** 地位。
*   **优势与劣势**：
    *   **优势**：社区规模空前（每日处理 500+ Issue/PR），功能覆盖面广，是许多衍生项目（如 PicoClaw, ZeptoClaw）的技术上游。
    *   **劣势**：**过度臃肿与稳定性危机**。功能模块的快速堆叠导致 v2026.7.1 版本出现致命启动 Bug，表明其架构复杂度已对稳定性构成挑战，用户体验受损。
*   **技术路线差异**：与专注于特定场景的项目（如 NanoBot 的 WebUI 交互、ZeroClaw 的 SOP 工作流）不同，OpenClaw 追求 **“大一统”的通用性**，这使其成为生态创新的泥板，但也因其复杂性成为“巨人肩膀”。
*   **社区对比**：OpenClaw 的社区热度远超其他项目（如 CoPaw、IronClaw 的活跃度也仅为 OpenClaw 的十分之一）。其讨论的议题（如跨平台、安全增强）通常是生态的风向标。

#### **4. 共同关注的技术方向**

1.  **桌面端与跨平台应用**：**OpenClaw (#75)** 和 **ZeroClaw** 社区均强烈要求提供 Linux/Windows 原生桌面应用。这反映了用户对于 **脱离命令行、拥抱更友好用户界面** 的普遍期待。
2.  **安全与治理**：
    *   **沙箱与特权管控**：**CoPaw (#5951)** 和 **ZeroClaw (#8973)** 同时遭遇了沙箱功能导致的系统级问题（Windows 递归爆炸、Linux Landlock 兼容性）。
    *   **凭证与数据保护**：**Hermes Agent (#50734)** 修复了 Agent 被诱导泄露 `.env` 凭证的严重安全漏洞。**OpenClaw (#10659)** 提出了“掩码秘密”功能。这表明 Agent 安全已从“推荐”变为“必须”。
    *   **多租户与访问控制**：**ZeroClaw (#5982)** 社区正在深入讨论 `per-sender RBAC` 以实现多租户部署，这是走向企业级应用的关键一步。
3.  **模型兼容性与稳定性**：
    *   **缓存问题**：**OpenClaw (#94518)** 报告 DeepSeek 缓存命中率暴跌；**PicoClaw** 则积极引入 Bedrock/Anthropic 提示缓存来降低成本。缓存机制的健壮性是提升模型使用经济性的关键。
    *   **工具调用兼容性**：**OpenClaw (#107905)** 和 **Moltis (#1098)** 均修复了因模型输出非标准参数（如十六进制输入、`null` 值）导致工具调用失败的问题。Agent 框架需要更健壮的防护来应对模型的“不稳定”行为。
4.  **多代理协作与记忆管理**：
    *   **代理循环与死锁**：**OpenClaw** 和 **LobsterAI (PR #2331)** 都在解决 Agent 陷入“工具调用死循环”的问题。
    *   **记忆可靠性**：**CoPaw (#6113)** 用户反馈 Agent 陷入“搜索记忆”的死循环，**ZeroClaw (#9048)** 社区则在探讨对话历史和长期记忆的分离存储。记忆系统正在从“有”走向“好用”。

#### **5. 差异化定位分析**

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **通用个人 AI 平台**，强调系统代理、跨模型兼容 | **高级用户、开发者**，追求高度自定义 | 插件式架构，生态系统最庞大，社区即市场 |
| **NanoBot** | **即时通讯 (IM) 频道集成**，强调 WebUI 交互 | **普通用户、聊天机器人爱好者** | 专注于粘合消息平台与 LLM，轻量级 Agent Runner |
| **Hermes Agent** | **以 Agent 为核心的安全与可靠性**，强调修复效率 | **DevOps、安全敏感用户** | 将 Agent 视为系统级组件，安全与稳定性修复优先级最高 |
| **PicoClaw** | **Pico 硬件终端集成**，轻量级 Agent 运行时 | **极客、嵌入式开发者** | 针对资源受限环境优化，强调与具体硬件（如 Sipeed 设备）的绑定 |
| **NanoClaw** | **多 IM 平台集成**，强调 Agent 间协作与审批 | **团队、企业工作组** | 独特的“技能分组”和“审批生命周期”机制，服务于结构化团队协作 |
| **IronClaw** | **大型基础设施集成**，如 Slack, Notion 的统一扩展运行时 | **大型团队、企业 IT** | 提出“扩展运行时”概念，将第三方应用视为 Agent 的扩展能力 |
| **ZeroClaw** | **SOP (标准操作程序) 引擎与工作流**，强调低代码自动化 | **企业流程管理者、运维人员** | 核心是 SOP 引擎，将 Agent 能力封装为工作流步骤，强调可审计性 |
| **CoPaw** | **安全治理与沙箱**，强调“墙内”安全策略 | **企业内部应用、合规要求高的组织** | 独特的“沙箱”与“审批”系统，注重 Agent 行为的可控性和审计性 |
| **Moltis** | **浏览器自动化与会话管理**，强调端到端交付 | **个人效率工具用户、Web 自动化需求者** | 深度集成浏览器工具，优化长对话管理和会话历史“再水合” |

#### **6. 社区热度与成熟度**

*   **高活跃、快速迭代期（扩张型）**：
    *   **OpenClaw, IronClaw, ZeroClaw, CoPaw**：这些项目 PR 和 Issue 吞吐量极大，功能更新频繁，但伴随较高的 Bug 回归风险。它们处于“野蛮生长”阶段，社区贡献者和维护者均非常繁忙。
*   **中等活跃、质量巩固期（收敛型）**：
    *   **NanoBot, Hermes Agent, PicoClaw, Moltis**：这些项目在保持一定开发节奏的同时，更侧重于 Bug 修复、依赖更新和清理积压。项目成熟度较高，用户基础相对稳定，体验更好。
*   **低活跃/静默期（停滞型）**：
    *   **NullClaw, TinyClaw, ZeptoClaw, LobsterAI**：这些项目在过去 24 小时几乎没有活动。可能是进入了功能维护期、等待下一轮大版本，或者项目本身已被边缘化。

#### **7. 值得关注的趋势信号**

1.  **“桌面化”浪潮来袭**：**OpenClaw** 和 **ZeroClaw** 社区对桌面客户端的强烈诉求是一个明确的信号。AI 智能体正在从“服务”向“应用”演进，独立、持久、拥有良好 GUI 的桌面形态将是下一阶段的竞争焦点。
2.  **工程可靠性压倒一切**：**OpenClaw** 的升级灾难和 **IronClaw** 的复杂“扩展运行时”整合，都指向同一个结论：**对个人 AI 智能体来说，“稳定运行”的价值远高于“功能堆砌”**。未来的竞争将从“谁能做更多”转向“谁能做得更稳”。
3.  **安全不再是可选项**：从 Hermes Agent 的安全事件到 ZeroClaw 的沙箱问题，社区对 **沙箱、凭证保护、提示注入防护、多租户访问控制** 的需求正在从“高级功能”变为“基础要求”。企业级落地必须迈过安全这道坎。
4.  **可观测性与调试能力成刚需**：**OpenClaw** 的缓存命中率问题、**ZeroClaw** 的 Provider 错误反馈模糊（#9001）、**NanoBot** 的内存泄漏（#4787）等，表明用户迫切需要 **更深度的运行时洞察、更精确的错误定位和更好的监控工具**。这是提升 Agent 应用可靠性的关键一环。
5.  **向 OpenAI API 兼容性靠拢**：**ZeroClaw** 正在推进的 OpenAI 兼容端点（PR #8486）是一个重要信号。尽管自己的协议可能更优，但 **为了无缝对接现有开发工具链（如 LangChain, Continue.dev），拥抱事实标准是项目获得更广泛生态支持的最高效路径**。

**对 AI 智能体开发者的建议**：当前阶段，建议将 **30% 的开发精力放在新功能**，**70% 的精力投入到稳定性加固、安全审计、可观测性建设以及提供简洁的 API 兼容性** 上。关注 OpenClaw 系的生态动向，但警惕其稳定性陷阱，可考虑基于其上游版本稳定后定制，或选择 NanoBot、Hermes Agent 等更聚焦、更稳健的成熟替代品作为起点。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手开源项目分析师，以下是根据您提供的 NanoBot (HKUDS/nanobot) GitHub 数据生成的每日项目动态日报。

---

### **NanoBot 项目动态日报 | 2026-07-15**

---

#### **1. 今日速览**

今日 NanoBot 项目活跃度极高。社区贡献者提交了大量 Pull Request，其中近 **47 个 PR** 成功合并或关闭，显示出项目在 Bug 修复、功能增强和代码重构方面均取得了显著进展。Issues 方面，关闭了 **10 个**存量问题，但同时也有 **3 个**新 Bug 被报告，集中在核心功能（心跳、模型兼容性、资源管理）上，表明项目虽在快速迭代，但稳定性仍是需持续关注的焦点。整体来看，项目处于高速发展期，社区参与度旺盛，健康度良好。

---

#### **2. 版本发布**

无新版本发布。

---

#### **3. 项目进展**

今日项目合并/关闭了大量 PR，主要推进了以下方面的优化与修复：

- **核心功能修复 (心跳/重启)**：
    - [PR #4931](https://github.com/HKUDS/nanobot/pull/4931) 修复了频道重连后无法正常传递“重启完成”通知的 Bug，提升了连接的健壮性。
    - [PR #4915](https://github.com/HKUDS/nanobot/pull/4915) 使心跳的响应评估机制更可配置，解决了因心跳迁移到 Cron 作业导致的其他回归问题，并允许禁用评估以始终发送 AI 回复。
- **WebUI 体验优化**：
    - [PR #4933](https://github.com/HKUDS/nanobot/pull/4933) 在 WebUI 中添加了斜杠命令和应用提及的高亮显示，增强了用户交互引导。
    - [PR #4930](https://github.com/HKUDS/nanobot/pull/4930) 为用户消息添加了“复制”动作，提升了用户操作的便利性。
- **架构与稳定性加固**：
    - [PR #4936](https://github.com/HKUDS/nanobot/pull/4936) 加速了 CI 流程并增强了测试套件的稳定性。
    - [PR #4631](https://github.com/HKUDS/nanobot/pull/4631) 添加了脚本化 Agent Runner 测试平台，为未来的 Agent 行为测试打下了坚实基础。
- **CLI 标准化**：
    - [PR #4932](https://github.com/HKUDS/nanobot/pull/4932) 统一了 CLI 命令中关于 `--config` 选项的帮助文本，提升了用户体验的一致性。

---

#### **4. 社区热点**

今日讨论最活跃的议题聚焦于 **心跳机制** 和 **频道架构**：

- **[Issue #4924](https://github.com/HKUDS/nanobot/issues/4924): `_pick_heartbeat_target_from_sessions` fails when `unifiedSession: true`**
    - **热度分析**：该 Bug 报告触及了核心功能——统一会话模式下的心跳路由问题。社区很快就此问题展开了讨论，并迅速提交了修复 PR [#4928](https://github.com/HKUDS/nanobot/pull/4928)，体现出项目对核心稳定性问题的快速响应。
- **[PR #4928](https://github.com/HKUDS/nanobot/pull/4928): fix(heartbeat): route unified sessions to last channel**
    - **热度分析**：作为上述 Issue 的修复方案，该 PR 详细分析了问题的根源和解决方案，引发了开发者的高度关注。它直接关系到使用统一会话功能的用户能否正常接收 Agent 的主动消息。

---

#### **5. Bug 与稳定性**

今日报告了 **3 个**新的 Bug，并按严重程度排列如下：

- **[严重] Issue #4924**: `unifiedSession` 为 true 时，心跳目标选择失败，导致 Agent 无法向正确的频道发送主动消息。已有修复 [PR #4928](https://github.com/HKUDS/nanobot/pull/4928)。
- **[严重] Issue #4787**: **`Session.messages` 列表无限制增长**，导致长期运行的会话可能出现内存泄漏。此问题涉及资源管理，影响范围广，目前仍在开放状态。
- **[中等] Issue #4934**: **Qwen 模型暴露思考/推理内容**。使用 DashScope 提供商时，模型的思考过程被错误地包含在最终回复中，影响聊天体验。暂无相关 PR。
- **[已修复] Issue #4795**: 流式 LLM 调用绕过了网络层面的超时机制，可能导致资源无限占用。该问题于 8 天前报告，今日已关闭，修复方法可能是近期其他 PR 的一部分。
- **[已修复] Issue #4881**: Windows 平台下，`ExecTool` 错误地将 PowerShell 的 UTF-16 输出解码为 UTF-8，导致输出内容损坏。该问题于 4 天前报告，今日已关闭。

---

#### **6. 功能请求与路线图信号**

- **WebUI Cron 作业管理 (Issue #4218)**: 用户请求在 WebUI 中增加 Cron 作业管理功能，此需求呼声很高，且 WebUI 已具备管理其他模块的能力。这是一个强烈的产品化信号，可能被纳入中期路线图。
- **钉钉频道增强 (PR #4446)**: 这是一个针对钉钉频道的功能增强 PR，包括 `disable_private_chat` 配置项和群回复中的“@提及”功能。这表明社区对特定企业通讯工具的集成有明确需求。
- **记忆/归档功能增强 (PR #4621)**: 通过提供 `MEMORY.md` 上下文来优化事实归档，避免重复和冲突。这体现了项目在 Agent 长期记忆领域的持续深耕，是未来高级智能的重要基石。
- **OAuth 状态可视化 (PR #4689)**: 旨在提供 OAuth 提供商的状态及令牌过期警告。这是一个提升企业级用户运维体验的关键特性。

---

#### **7. 用户反馈摘要**

- **痛点与使用场景**:
    - **频道兼容性**: Issue #2568 中用户反馈 Telegram 频道在特定版本后存在 Markdown 渲染不稳定的问题，显示在多平台兼容性方面仍有优化的空间。
    - **资源消耗**: Issue #1086 获得了 4 个 👍，用户反映 WhatsApp Bridge 的 WebSocket 绑定问题导致 Docker 容器间无法通信，这揭示了容器化部署环境下的常见配置痛点。
    - **无用通知**: Issue #1445 获得 2 个 👍，用户希望 Cron 任务在没有实质性变化时不发送通知，反映了用户对智能过滤和噪音控制的强烈需求。
- **满意与积极反馈**:
    - 用户对于 Bug 的快速修复（如 #4881, #4795）和 WebUI 功能的持续改进（如 #4930, #4933）给予了积极关注。PR #4930 的用户消息复制功能是社区长期呼声的体现。

---

#### **8. 待处理积压**

- **长期未响应的重要 Issue**:
    - **[Issue #1086](https://github.com/HKUDS/nanobot/issues/1086): WhatsApp Bridge WebSocket 绑定限制通信** (获得 4 个 👍)。
        - **状态**: 已关闭，但根本问题可能未在代码层面彻底解决，而是作为已知限制被关闭。对于依赖 WhatsApp 通道的容器化部署用户来说，这是一个潜在的痛点，维护者应考虑在文档中明确说明或提供一个更通用的解决方案。
- **重要的开放 PR**:
    - **[PR #4908](https://github.com/HKUDS/nanobot/pull/4908): 重构频道架构**。
        - **状态**: 开放中。这是一个影响较大的架构重构，旨在解耦频道的设置和实例管理。虽然 PR 已标记为 `priority: p1`，但至今已开放 2 天，需要维护者重点关注并推动审查，以防阻塞其他依赖于该架构的 PR。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据您提供的Hermes Agent GitHub数据，为您生成了2026年7月15日的项目动态日报。

---

### **Hermes Agent 项目动态日报 | 2026年7月15日**

---

#### **1. 今日速览**

截至2026年7月15日，Hermes Agent项目在过去24小时内展现出极高的社区活跃度。项目迎来了大量Issue和PR的更新（各50条），其中Issue关闭数（43条）远超新开/活跃数（7条），表明核心团队正在高效地清理积压问题，维护工作取得显著进展。当前主要PR池中仍有46条等待合并，社区贡献力量持续涌入。尽管没有新版本发布，但项目在Bug修复、安全加固和核心功能优化上迈出了坚实的一步。

---

#### **2. 版本发布**

无

---

#### **3. 项目进展**

今日项目核心进展体现在对多个高影响Bug的快速修复和功能增强的合并上。主力修复了Cron任务重复触发（#51329）、会话状态丢失（#50713）以及安全相关的凭证泄露（#50734）等关键问题。此外，多项针对桌面端（#51273）、Telegram平台（#50991）和多Provider集成（#51278）的PR也已合并，极大提升了跨平台与多模型环境下的稳定性。整体而言，项目在**稳定性**和**安全**这两个维度取得了明显进步。

- **高影响Bug修复合并:**
    - **Cron任务修复：** 修复了因并发竞争导致Cron任务可能重复执行、消息重复投递的Bug（[PR #51329](NousResearch/hermes-agent Issue #51329)）。
    - **安全漏洞修复：** 解决了代理（Agent）可能忽略安全指令，通过 `read_file` 工具被诱导泄露 `.env` 凭证的严重问题（[PR #50734](NousResearch/hermes-agent Issue #50734)）。
    - **会话恢复修复：** 修复了在多个Hermes部署间重启会话时，部分聊天文本内容丢失的问题（[PR #50713](NousResearch/hermes-agent Issue #50713)）。
    - **平台集成修复：** 修复了Telegram平台在多Profile模式下因 `apply_env_overrides` 作用域错误导致的令牌泄露（[PR #51029](NousResearch/hermes-agent Issue #51029)）及缓存驱逐后Typing状态残留（[PR #50991](NousResearch/hermes-agent Issue #50991)）问题。
- **功能增强与改进:**
    - **vLLM兼容性修复：** `chat_completions` 传输层已更新，以兼容vLLM >=0.23版本，正确处理并传播`reasoning`字段（[PR #51530](NousResearch/hermes-agent PR #51530)）。
    - **桌面端体验优化：** 修复了桌面端会话 source 标记错误（[PR #50932](NousResearch/hermes-agent Issue #50932)）和模型选择器持久化错误（[PR #50944](NousResearch/hermes-agent Issue #50944)）。

---

#### **4. 社区热点**

今日社区讨论焦点集中在平台集成细节、安全边界和用户体验上。

- **热点 Issue #50703 (已关闭):** `[type/bug, comp/agent, provider/nvidia]` 关于在使用NVIDIA NIM时，`extra_body` 的翻译过程会剔除顶层的 `chat_template_kwargs`，导致`thinking_mode`无法生效。该问题获得了8条评论，是今日讨论最热烈的。其背后反映了用户对**精确配置多模型、尤其是支持思考模式**的强烈需求，以及不同Provider间配置兼容性的痛点。
    - [链接](NousResearch/hermes-agent Issue #50703)

- **热点 Issue #64674 (新开):** `[type/bug, comp/gateway, platform/telegram]` 电报适配器在多Profile模式下，当bot token配置在次要Profile中时无法启动。这是今日唯一的新开高活跃度Issue，暴露出多Profile部署场景下的配置加载存在问题，对依赖Telegram作为主要入口的用户影响较大。
    - [链接](NousResearch/hermes-agent Issue #64674)

- **热点 Issue #50734 (已关闭):** `[type/security]` 关于代理无视安全指令，通过 `read_file` 工具泄露 `.env` 全量凭证的安全事件。虽然Issues描述方式有些特殊（自称是受命操作的Agent），但问题本身的严重性引发了社区对安全机制的讨论，社区贡献者快速响应并修复了此问题。
    - [链接](NousResearch/hermes-agent Issue #50734)

---

#### **5. Bug 与稳定性**

今日报告的大多数Bug已得到快速修复。按严重程度排列如下：

| 严重程度 | 问题标题 | 所属模块 | 状态 | Fix PR/Commit 关联 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [Bug]: Agent ignores all safety directives and exfiltrates full .env credentials (#50734) | tool/file, area/auth | **已关闭/已修复** | 已合并 |
| **严重** | [Bug]: Dashboard no longer works with docker (#59113) | comp/dashboard, area/auth, area/docker | **开放中** | 暂无 |
| **中等** | Telegram adapter fails to start on default-profile gateway (#64674) | comp/gateway, platform/telegram | **开放中** | 暂无 |
| **中等** | Cron double-fire: race between tick dispatch and in-flight guard registration (#51329) | comp/cron | **已关闭/已修复** | 已合并 |
| **中等** | [Bug]: Desktop app sessions saved as source "tui" instead of "desktop" (#50932) | comp/tui, comp/desktop | **已关闭/已修复** | 已合并 |
| **低** | bug: Desktop app sessions saved as source "tui" instead of "desktop" (#50966) | comp/tui, tool/browser | **无法复现** | 无 |
| **低** | [Bug]: 桌面端无法更新 (Desktop can‘t update) (#51273) | comp/desktop, platform/windows | **已关闭/已修复** | 已合并 |

---

#### **6. 功能请求与路线图信号**

用户提出的功能请求主要围绕**配置灵活性**和**提供商兼容性**。

- **通用配置增强：**
    - **TUI WebSocket超时时间可配置：** 用户请求添加 `HERMES_TUI_WS_WRITE_TIMEOUT_S` 环境变量，以解决硬编码10秒超时问题（[#51288](NousResearch/hermes-agent Issue #51288)）。该Issue已关闭，核心思路可能已被采纳。
    - **模型层次化与故障转移：** 用户希望支持模型“层级”配置，以便在主模型配额用尽时无缝切换（[#51257](NousResearch/hermes-agent Issue #51257)）。结合已有的 `fallback_providers` 配置（[#51278](NousResearch/hermes-agent Issue #51278)的修复），这表明项目正在积极完善**模型路由和故障转移**能力。
- **平台与提供商集成：**
    - **Google Chat格式修复：** 社区提交了修复Google Chat集成中格式占位符泄露的PR（[#51567](NousResearch/hermes-agent PR #51567)），表明Slack、Google Chat等平台集成仍在打磨中。
    - **GLM-5推理支持：** 用户期望通过ZAI Provider直接使用GLM-5模型的 `/reasoning` 控制端点（[#50696](NousResearch/hermes-agent Issue #50696)），该功能已被标记为已实现。

**路线图信号：** 项目明显在向**更强大的多Profile/多模型配置**、**更灵活的错误处理与故障转移**、以及**更深度的第三方平台集成**方向发展。`delegate_task` 系统的持续改进（如#51303, #51294）也暗示了项目可能正在加强其**多Agent协作**的内核能力。

---

#### **7. 用户反馈摘要**

从今日的Issues中提炼出以下用户痛点与使用场景：

- **部署与配置痛点：** Docker用户反映Dashboard在部署后无法工作（#59113），Telegram bot token的配置和Profile加载逻辑令人困惑（#64674）。这表明**简化部署和配置流程**仍是提升用户体验的关键。
- **安全担忧：** 用户对Agent可能被恶意诱导泄露敏感信息（#50734）表达了严重关切。尽管已快速修复，但这突显了**Agent安全性作为核心特性**的极高优先级。
- **跨平台一致性：** 用户期望在桌面端、TUI和不同消息平台（Telegram）上获得一致且可靠的使用体验。从会话状态丢失（#50713）、界面更新失败（#51273）到模型选择器混乱（#50944），这些“小毛病”严重影响了用户的信任感。
- **清晰度与可控性：** 用户希望更能“控制的”Agent行为。例如，对TUI超时时间的可配置需求（#51288），以及希望Cron任务在失败或执行时提供更清晰的反馈（#51294, #51526）。

---

#### **8. 待处理积压**

以下为长期未响应或存在搁置风险的重要Issue和PR，建议维护团队重点关注。

- **高影响开放Issue:**
    - **[Bug]: Dashboard no longer works with docker (#59113):** 已开放10天，评论数3，获得2个点赞。这是一个影响Docker用户群体的关键问题，涉及Dashboard的认证机制变更，可能与最新的Docker部署指南冲突。
    - **Telegram adapter fails to start on default-profile gateway (#64674):** 今日新开，但影响Telegram平台用户的核心功能，应优先处理。
- **长期未合并PR:**
    - **fix(dashboard): set headers for JWKS requests (#49608):** 已开放25天，涉及OIDC认证跨Provider兼容性，属于安全与合规边界性问题，风险较高。
    - **fix(tools): allow file writes under the active temp dir on macOS (#41285):** 已开放超过一个月，是一个已被测试验证过的跨平台缺陷修复。其长时间未合并可能阻塞macOS用户的相关功能。
- **标记“无法复现”的Issue:**
    - **browser_vision tool in desktop GUI always routes to browser_scroll (#50966):** 标记为“无法复现”，但用户详细描述了环境与步骤。若该问题影响特定配置（如Windows 11 + OpenRouter），可能需要更精确的复现指引。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-07-15

---

## 📋 今日速览

过去 24 小时，PicoClaw 社区保持活跃：共更新 3 条 Issue（全部为新开/活跃），9 条 Pull Request（其中 5 条已合并/关闭）。无新版本发布。项目在 **稳定性修复**（如 Bedrock 模型兼容、流式工具调用丢失、配置 panic）和 **功能增强**（如 Bedrock 提示缓存、飞书原生媒体类型）两个方向均有实质进展。社区焦点集中在安全库替换（`vodozemac` vs `libolm`）和缓存优化两个议题上，整体健康度良好。

---

## 🚀 版本发布

**无新版本发布。** 最新版本仍为 0.3.1（参见 Issue #3232 中用户提及）。

---

## 🔧 项目进展

过去 24 小时共有 **5 个 Pull Request 被合并或关闭**，均为重要修复或功能推进：

| PR 编号 | 标题 | 状态 | 意义 |
|---------|------|------|------|
| [#2982](https://github.com/sipeed/picoclaw/pull/2982) | fix(bedrock): drop temperature for models that deprecate it (Opus 4.8) | 已合并 | 修复 AWS Bedrock 上升级至 Claude Opus 4.8 后所有 LLM 调用失败的问题（因该模型弃用了 `temperature` 参数） |
| [#2957](https://github.com/sipeed/picoclaw/pull/2957) | fix(channels): prevent tool_calls from being dropped during streaming | 已合并 | 修复流式响应中 `tool_calls` 被错误过滤为辅助消息的回归问题，确保工具调用完整传递 |
| [#2270](https://github.com/sipeed/picoclaw/pull/2270) | fix(config): handle non-addressable SecureString values in collectSensitive | 已合并 | 修复配置遍历时因 Go 反射非可寻址值导致的 panic，增强配置安全性 |
| [#2128](https://github.com/sipeed/picoclaw/pull/2128) | fix(tools): ensure tool parameters have valid JSON Schema properties field | 已合并 | 修复部分 MCP 服务器返回无 `properties` 字段的工具参数时，与严格 OpenAI 兼容 API（如 LM Studio）的兼容性问题 |
| [#3156](https://github.com/sipeed/picoclaw/pull/3156) | feat(pico): emit per-turn LLM token usage on finalized message | 已合并 | 新增功能：在 Pico 通道的最终消息中输出每轮 LLM 的输入/输出 token 用量，方便下游按用量计费 |

**整体评价**：项目在修复关键 Bug 的同时，持续推进缓存优化（待合并 PR #3163、#3228）和消息类型拓展（PR #3256），向更稳定、更可观测的方向迈进。

---

## 🔥 社区热点

### 1. 安全库替换：`vodozemac` 替代 `libolm`  
- **Issue [#3088](https://github.com/sipeed/picoclaw/issues/3088)**（已开放 36 天，8 条评论，2 👍）  
  用户 `pbsds` 提出将已无人维护且不安全的 `libolm` 替换为官方推荐库 `vodozemac`。该 Issue 带有 `help wanted` 和 `priority: high` 标签，尽管过去24小时无新评论，但仍是社区高优先级诉求。  

### 2. 提示缓存（Prompt Caching）相关 PR 并行推进  
- PR [#3163](https://github.com/sipeed/picoclaw/pull/3163)（feat(bedrock): leverage Converse prompt caching via cache points）—— 实现 AWS Bedrock Converse API 的提示缓存，可降低输入成本约 0.1×。  
- PR [#3228](https://github.com/sipeed/picoclaw/pull/3228)（fix(anthropic-messages): send SystemParts as system blocks with cache_control）—— 修复 Anthropic 消息提供者无法为每个 `SystemPart` 设置 `cache_control` 标记的问题，使 Anthropic 的提示缓存可用。  

两个 PR 均处于开放待合并状态，体现了社区对 **降低大模型推理成本** 的强烈需求。

---

## 🐛 Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| **中** | [#3255](https://github.com/sipeed/picoclaw/issues/3255) (新开) | 钉钉频道聊天列表预览始终显示固定文本 `"PicoClaw"` 而非实际回复内容，但聊天内部显示正确 | 无修复 PR |
| **中** | [#3232](https://github.com/sipeed/picoclaw/issues/3232) (stale) | 未配置回退模型时，速率限制（rpm）完全不生效 | 仅有 1 条评论，无修复 PR |
| **高** | [#2982](https://github.com/sipeed/picoclaw/pull/2982) (已合并) | AWS Bedrock Claude Opus 4.8 因弃用 `temperature` 参数导致全部 LLM 调用失败 | **已修复** |
| **高** | [#2957](https://github.com/sipeed/picoclaw/pull/2957) (已合并) | 流式响应中工具调用（tool_calls）被错误丢弃 | **已修复** |
| **中** | [#2128](https://github.com/sipeed/picoclaw/pull/2128) (已合并) | 部分工具参数缺少 `properties` 字段导致 JSON Schema 验证失败 | **已修复** |

**注意**：今日新报告的 Bug #3255（钉钉预览问题）目前无对应 PR，需维护者关注。

---

## 💡 功能请求与路线图信号

| 功能 | 来源 | 状态 | 路线图可能性 |
|------|------|------|-------------|
| 用 `vodozemac` 替换 `libolm` | Issue [#3088](https://github.com/sipeed/picoclaw/issues/3088) | 开放，high priority | **高** —— 安全关键且官方推荐 |
| AWS Bedrock 提示缓存 | PR [#3163](https://github.com/sipeed/picoclaw/pull/3163) | 开放待合并 | **高** —— 可大幅降低成本 |
| Anthropic 系统消息 cache_control | PR [#3228](https://github.com/sipeed/picoclaw/pull/3228) | 开放待合并 | **高** —— 配合 #3163 完善缓存生态 |
| 飞书频道原生音频/视频消息 | PR [#3256](https://github.com/sipeed/picoclaw/pull/3256) | 新开待合并 | **中** —— 改善用户体验 |
| 每轮 LLM token 用量输出 | PR [#3156](https://github.com/sipeed/picoclaw/pull/3156) | 已合并 | **已纳入** |

此外，PR [#3233](https://github.com/sipeed/picoclaw/pull/3233)（Fix pr 3222 backward compat）仍在开放，说明社区在推进功能时对向后兼容性比较重视。

---

## 💬 用户反馈摘要

- **安全担忧**：用户 `pbsds` 强调 `libolm` 已无人维护且存在安全隐患，建议立即替换为 `vodozemac`（#3088）。  
- **使用痛点**：用户 `MrTreasure` 反馈钉钉聊天列表预览只显示固定文字，导致无法快速识别机器人回复内容（#3255）。  
- **配置困惑**：用户 `VictorSu000` 表示只设置了 `agents.defaults.model_name` 而未配置回退模型时，速率限制配置不工作（#3232）。  
- **正向反馈**：尽管无直接评论，但 5 个历史 PR 在 24 小时内被合并，表明社区修复问题的效率较高，用户痛点正逐步解决。

---

## 📦 待处理积压

以下为长期未响应或需优先关注的重要工作项：

1. **#3088 – 安全库替换**（开放 36 天，high priority，2 👍）  
   [https://github.com/sipeed/picoclaw/issues/3088](https://github.com/sipeed/picoclaw/issues/3088)  
   → 需维护者评估实现方案，可考虑从 PR #3163 或 #3228 的缓存优化中调配资源。

2. **#3232 – 速率限制不回退模型时失效**（开放 8 天，stale，仅 1 条评论）  
   [https://github.com/sipeed/picoclaw/issues/3232](https://github.com/sipeed/picoclaw/issues/3232)  
   → 用户等待回复，建议标记 `bug` 并确认是否需要补充文档或代码修正。

3. **#3233 – PR #3222 向后兼容修复**（开放 8 天，stale）  
   [https://github.com/sipeed/picoclaw/pull/3233](https://github.com/sipeed/picoclaw/pull/3233)  
   → 阻塞另一项功能落地，需 Review。

4. **#3163 与 #3228 缓存相关 PR**（分别开放 22 天、9 天）  
   [https://github.com/sipeed/picoclaw/pull/3163](https://github.com/sipeed/picoclaw/pull/3163)  
   [https://github.com/sipeed/picoclaw/pull/3228](https://github.com/sipeed/picoclaw/pull/3228)  
   → 两项 PR 高度互补，建议同时 Review 并决定是否一起合并。

---

*Data source: sipeed/picoclaw GitHub repository | Snapshot time: 2026-07-15 00:00 – 2026-07-15 23:59 UTC*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoClaw 项目数据，我为您生成 2026 年 7 月 15 日的项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-07-15

## 1. 今日速览

过去24小时内，NanoClaw 项目呈现出**高开发活跃度**但**社区讨论趋于平静**的状态。我们监测到大量 Pull Requests (PRs) 提交，其中 19 个处于待合并状态，仅 7 个被合并或关闭，说明项目核心团队正集中进行功能开发和问题修复，但合并审核流程可能存在瓶颈。值得注意的是，过去一天内没有任何新的 Issue 被创建或活跃讨论，社区反馈进入了一个短暂的静默期。总体来看，项目处于密集的**功能迭代与 Bug 修复冲刺阶段**，代码库在快速演进，但也伴随着一定的积压风险。

## 2. 项目进展

今日有 7 个 PR 被合并或关闭，主要贡献集中于**Telegram 集成、安全增强和文档同步**三个方面，显著提升了项目的稳定性和用户文档准确性。

- **【修复】Telegram 集成向导与漏洞修复**
  - **[PR #2728] (已关闭):** 修复了通过 `wire-to` 意图配对 Telegram 时，未创建必要的 `messaging_group_agents` 数据库记录的问题。该 Bug 会导致配对成功但消息路由失败。
  - **[PR #2729] (已关闭):** 修正了 `add-telegram` 技能文档中与实际安装步骤不匹配的状态块名称，避免用户在遵循向导时产生混淆。
  - **[PR #3043] (已关闭):** 将 Telegram 深度链接从 `t.me` 切换至 `telegram.me`，以解决特定网络环境下的访问问题。

- **【修复】系统稳定性与安全增强**
  - **[PR #2753] (已关闭):** 修复了当系统中缺少 `pnpm` 时，Git 预提交钩子 (pre-commit hook) 会报错退出的问题。提升了对非标准开发环境的兼容性。
  - **[PR #2730] (已关闭):** 修复了通过 `launchd/systemd` 等系统服务启动时，`.env` 文件中的 `NANOCLAW_*` 环境变量无法被正确加载的严重 Bug。该问题直接影响 `NANOCLAW_EGRESS_LOCKDOWN` 等重要安全标志的生效。

- **【功能】新增 Dial 渠道集成**
  - **[PR #3042] (已关闭):** 完成了在频道选择器、安装向导及技能文档中添加对 **Dial** 渠道的支持。这是一项重要的功能扩展，标志着 NanoClaw 不再是 Telegram 专有。

**项目整体进展判断**：项目在解决此前遗留的 Telegram 集成问题和文档歧义上取得了决定性进展，同时强化了部署环境的安全与稳定性。新增的 Dial 渠道支持表明项目正在向平台无关的 AI 代理方向迈进。

## 3. 社区热点

尽管没有新增 Issue，但多个 PR 在创建当日就进入了待合并状态，反映出核心开发团队（如 `sturdy4days`）本周的极高产出。其中最值得关注的 PR 如下：

- **PR #2921 [待合并] - `fix(compose): gate skill fragments on group skill selection`**
  - **链接:** [PR #2921](https://github.com/nanocoai/nanoclaw/pull/2921)
  - **活跃分析:** 此 PR 自 7 月 3 日开放，已收到 **12 条评论**，是近期评论最多的 PR。作者 `michaelzetune` 和 `sturdy4days` 等多位核心贡献者在此深度讨论了关于技能片段 (skill fragments) 在分组组合时的行为逻辑。
  - **背后诉求:** 用户和开发者关心的核心是**多技能知识组合的正确性和可控性**。原问题导致无论哪个分组选择了技能，所有技能的知识都会被注入，造成混乱。此 PR 试图严格遵从分组配置，确保 AI 代理只获得被授权分组的技能上下文，这对于复杂的、多代理协作场景至关重要。

- **PR #2899 [待合并] - `fix(discord): strip newline suffix from custom_id before parsing Gateway interactions`**
  - **链接:** [PR #2899](https://github.com/nanocoai/nanoclaw/pull/2899)
  - **活跃分析:** 该 PR 解决了 Discord 集成中的一个关键 Bug，导致所有审批按钮点击都返回“拒绝”。虽然评论数不多，但问题影响面广，讨论触及了不同通信协议下数据编码格式的兼容性难题。
  - **背后诉求:** 反映出用户对 **“渠道功能完整性与零错率”** 的强烈需求。任何官方的 Discord 集成功能都必须是可信的，此 Bug 会严重破坏用户信任。

## 4. Bug 与稳定性

今日未报告新的 Bug，但此前报告的多个长期 Bug 在今日有重要的修复 PR 提交或直接关闭。

- **【严重】系统级环境变量加载失败 - 已修复**
  - **问题描述:** `NANOCLAW_*` 系列环境变量在 `launchd/systemd` 等系统服务下无法读取 `.env` 文件。直接导致安全机制（如 `NANOCLAW_EGRESS_LOCKDOWN`）失效。
  - **严重程度:** 严重
  - **PR #2730** 已合并关闭，该问题已解决。

- **【中高】Telegram 配对逻辑缺陷 - 已修复**
  - **问题描述:** 使用 `--intent wire-to` 进行配对操作，表面成功，但核心的 `messaging_group_agents` 数据库记录缺失，导致消息无法路由。
  - **严重程度:** 中高
  - **PR #2728** 已合并关闭，该问题已解决。

- **【重要】Discord 审批按钮始终拒绝 - 有 Fix PR**
  - **问题描述:** Discord 所有 DM 中的审批卡片按钮点击后路由至“拒绝”流程，功能完全失效。
  - **严重程度:** 高
  - **Fix PR:** #2899 **(待合并)**，还未合并到主分支，问题仍然存在。

- **【中】语音/音频附件下载失败 - 有 Fix PR**
  - **问题描述:** Telegram 的语音/音频消息作为空文本 + 附件到达，但后端无法获取其 `fetchData`，导致 AI 代理无法处理。
  - **严重程度:** 中等 (影响特定渠道的特定功能)
  - **Fix PR:** #3044 **(待合并)**，问题等待修复。

## 5. 功能请求与路线图信号

- **新增渠道支持：Dial 集成**
  - **描述:** 用户 `OmriBenShoham` 提交了 PR #3042 (已合并) 和 #3050 (待合并)，系统性地为 NanoClaw 添加了对通信平台 **Dial** 的支持。
  - **路线图信号:** **强烈信号**。这表明项目路线图中明确包含了**渠道无关化**的方向。Dial 的加入不仅丰富了连接选项，也验证了项目设计的可扩展性。可以预期，更多渠道（如 Slack, Discord 的深度集成等）会成为下一版本的重点。

- **统一审批生命周期**
  - **描述:** 核心开发人员 `moshe-nanoco` 提交了 PR #3040 (待合并)，旨在将所有请求的“审批保持”机制统一到一个生命周期合约中。
  - **路线图信号:** **中等信号**。这暗示了项目后端架构正在经历一次**治理与审批机制的规范化重构**。这意味着未来的审批流程将更可预测、更安全，可能涉及多级审批、超时策略等功能。此变更将是下一版本的重要基础能力。

## 6. 用户反馈摘要

由于过去 24 小时无新 Issue 创建，用户反馈主要隐含在已合入的修复 PR 的描述中。

- **痛点:** 用户在遵循官方文档进行 Telegram 集成时，遇到了**文档与实际操作脱节**的问题，例如状态块名称不匹配。这体现了用户对“开箱即用”文档体验的高要求。
- **痛点:** 在非开发环境（如使用服务管理工具）下部署时，遭遇**环境变量加载失败**，导致安全功能“静默失效”。这暴露了项目在**生产环境部署的健壮性**方面仍有提升空间，用户需要更明确的部署指引。
- **场景:** 用户尝试通过 Discord 进行审批操作，但所有按钮均指向“拒绝”，**严重破坏了工作流**。这突显了跨平台功能完整性对于实际使用者来说是不容妥协的核心诉求。

## 7. 待处理积压

以下为长期未处理或关键节点遭遇瓶颈的 PR，建议维护者优先关注。

- **PR #2921 (待合并 - 7月3日创建，已有15条评论)**: `fix(compose): gate skill fragments on group skill selection`
  - **链接:** [PR #2921](https://github.com/nanocoai/nanoclaw/pull/2921)
  - **重要性:** **极高**。此 PR 涉及基础的多技能组合逻辑，是支撑项目核心功能（多代理协作）的关键。当前的讨论已非常深入，且有技术分歧，需要核心团队做出最终决策，否则将成为后续开发的一大阻碍。
  - **建议:** 维护者需尽快组织会议或在 PR 中给出明确的方向性意见，推动合并或修改。

- **PR #2800 (待合并 - 6月17日创建)**: `fix(security): validate group folders and forbid implicit image pulls`
  - **链接:** [PR #2800](https://github.com/nanocoai/nanoclaw/pull/2800)
  - **重要性:** **高**。这是一个**安全修复**，涉及组文件夹验证和阻止隐式 Docker 镜像拉取，直接关系到系统安全性。悬而未决近一个月，有可能会对用户系统造成安全风险。

- **PR #2899 (待合并 - 7月1日创建)**: `fix(discord): strip newline suffix from custom_id before parsing Gateway interactions`
  - **链接:** [PR #2899](https://github.com/nanocoai/nanoclaw/pull/2899)
  - **重要性:** **高**。该 Bug 完全破坏了 Discord 渠道的核心交互功能，严重影响相关用户的正常使用。尽管有新 PR 提交，但该问题应被优先解决。

- **PR #2750 (待合并 - 6月12日创建)**: `fix: recover stale outbound.db journals after container kills...`
  - **链接:** [PR #2750](https://github.com/nanocoai/nanoclaw/pull/2750)
  - **重要性:** **高**。修复了两个与容器非正常结束相关的罕见但严重的数据一致性问题（#2516, #2640）。长时间未合并，可能导致用户在特定场景下遭遇消息丢失或重复投递。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的IronClaw项目GitHub数据生成的2026年7月15日项目动态日报。

---

# IronClaw 项目动态日报 | 2026年07月15日

## 今日速览

截至2026年7月15日，IronClaw项目在过去24小时内呈现出极高的活跃度，标志着项目进入了密集的功能集成与问题修复阶段。社区和核心团队的沟通与协作异常频繁，共有48条Issue和50条PR被更新。项目当前主线工作聚焦于“统一扩展运行时”（Unified Extension Runtime）的最终落地与稳定性修复，与此同时，多个关键Bug（如消息乱序、扩展状态报告不实）的修复正在进行中，显示出项目在交付新功能的同时，对现有系统健康度给予了高度关注。这是一个功能开发与稳定性加固并行的关键冲刺期。

## 项目进展

今日项目核心进展在于“扩展运行时”工作流的多个大型合并请求被成功合入，标志着该重大基础设施功能已进入尾声。此外，数个关键错误修复也已合并，提升了系统的健壮性。

- **扩展运行时（Extension Runtime）核心合并**：团队完成了代号为“Train B”的扩展运行时最终整合（PR #6090），这是一个包含了9个阶段工作的树形-相同（tree-identical）压缩提交。同时，项目主要分支也完成了“Train A”的整合（PR #6061），这为后续功能开发奠定了坚实基础。
- **Slack渠道生命周期测试**：PR #6110 已提交，为Slack扩展的安装、连接、断开、重连等完整状态机添加了集成测试，直接回应了Issue #6105中提出的高频Bug家族（Slack扩展生命周期问题）。
- **关键Bug修复合并**：
    - 修复了Slack认证不可用时提供模糊的错误信息（#5884、#6095）。
    - 修复了资源管理器因libSQL数据库争用而崩溃的问题（#6089）。
    - 修复了WebUI中“内存（Memory）”浏览区域未正确隔离用户数据的问题（#5896）。
    - 修复了扩展目录加载失败时显示空白页面的UI问题（#6087）。
    - 修复了WebUI v2中的多个UI/UX问题，包括主题色、聊天连接状态及MCP标签页渲染错误（#6039, #6037, #6028）。

- **日常推进**：Agent循环新增了工具感知的完成提示功能（PR #6013）；性能方面，通过调整工具结果预览的限制（PR #6097），基于真实数据优化了ClawBench测试集表现。

## 社区热点

今日社区讨论的热点主要集中在**扩展/渠道生命周期**和**核心消息时序**两大问题上。

- **🎙️ 扩展/渠道生命周期状态机（#6105）**：该Issue收集了超过一周以来围绕Slack集成的多个回归Bug，包括连接状态冲突（#6091）、重连后“思考中”挂起（#6092）、凭据丢失后未正确通知（#5884）。社区开发者对此类高频问题表达了强烈关注。团队已在PR #6110中直接响应此问题，预计在下个版本中会得到显著改善。
    [查看 Issue #6105](https://github.com/nearai/ironclaw/issues/6105)

- **🎙️ Slack 连接状态冲突（#6091）**：连接断开后，系统仍报告为连接状态，UI不同部分状态不一致，导致Agent行为异常。该问题直接影响了用户对扩展状态的可信度，引发了较多讨论。
    [查看 Issue #6091](https://github.com/nearai/ironclaw/issues/6091)

- **🎙️ 消息时序错乱（#6047）**：当两个任务消息被快速发送时，UI显示顺序颠倒，导致后续自动触发创建基于错误的消息。该问题直接破坏了对话的连续性，是用户对聊天功能最核心的诉求之一。对应的修复PR #6096 已提交并附带了复现测试用例。
    [查看 Issue #6047](https://github.com/nearai/ironclaw/issues/6047)

## Bug 与稳定性

过去24小时内报告的Bug数量较多，部分为高频问题的复发。已有明确的修复PR在应对这些问题。

- **严重（P2）**
    - **Slack集成完全中断**：重连Slack后无法正常工作，陷入“思考中”状态（#6092）；断开后系统仍认为连接正常（#6091）。**状态：已有相关测试PR (#6110) 和修复PR (#6095)。**
    - **消息处理失序**：快速发送的消息以错误顺序被处理和显示（#6047）。**状态：修复PR #6096 已提交。**
    - **常规任务凭据丢失**：外部令牌吊销后，常规任务（Routine）丢失凭据信息（#5884）。**状态：修复PR #6095 已合并。**
    - **用户反馈：错误处理不当**：`/llm/test-connection` API在无法访问的端点上报告成功（#6099）。**状态：新提交，等待处理。**
        [查看 Issue #6099](https://github.com/nearai/ironclaw/issues/6099)

- **中等（P3）**
    - **扩展状态报告不准确**：仅安装但未激活的GitHub扩展，被报告为已激活（#5948，已关闭，推测已修复）。**状态：已关闭。**
    - **扩展目录加载失败无反馈**：网络或服务器错误导致扩展列表为空时，UI无任何错误提示（#6087）。**状态：已合并修复PR。**
    - **管理页面功能缺陷**：管理员详情页面的“创建Token”按钮功能不存在（#6085）。**状态：新提交，等待处理。**
        [查看 Issue #6085](https://github.com/nearai/ironclaw/issues/6085)

- **其他与回归**
    - **Windows平台启动阻断**：由于文件系统操作无法在Windows上执行，`ironclaw-reborn` 完全无法在该平台启动（PR #6098）。**状态：修复PR #6098 已提交。**
    - **UI相关回归**：修复了主题颜色、聊天连接状态显示、MCP服务器页面的显示错误（#6039, #6037, #6028）。**状态：均已合并。**

## 功能请求与路线图信号

今日用户和核心贡献者提出了多项功能增强请求，方向明确指向了**工程质量和开发者体验**的提升。

- **CI与测试基础设施升级**：多项增强请求指向了CI系统的可靠性问题（#6103）和发布前的自动化检查（#6106），并建议设立24小时修复SLA（#6104），显示出社区对项目稳定性和响应速度的更高要求。
- **模型与工具兼容性**：提出了对模型输入兼容性的自动化测试（#6107），以及API请求中模型覆盖设置的正确性验证（#6109）。这表明随着支持的模型和工具增多，兼容性验证正成为关键挑战。
- **错误处理标准化**：Issue #6108 要求实现统一的、高保真的错误处理和报告机制，避免“成功谎言”和笼统的错误信息，以提升用户和开发者的调试效率。

这些功能请求大多由核心开发者提出，结合已有的PR（如#6090、#6093、#6111），表明项目团队正在推动一套更严谨的工程规范。

## 用户反馈摘要

从今日的Issues评论和描述中，可以提炼出以下用户核心痛点：

1. **信任危机与困惑**：扩展和渠道的状态报告不一致（例如，已断开连接的系统仍显示为连接状态）严重影响了用户对Agent能力的判断和信任。用户不确定Agent当前真正能做什么。
2. **沟通时间线的混乱**：消息顺序错乱直接破坏了对话的连贯性和逻辑性，这被认为是最基础的聊天功能，容错率极低。用户期望任何工具调用或操作都不应破坏这种时间线。
3. **无声的失败**：当网络错误或凭据过期时，系统要么静默失败（如扩展目录加载失败显示空白），要么给出模糊的通用错误消息（如“模型服务不可用”）。用户需要明确的、可操作的错误信息来替代“黑盒”般的失败体验。
4. **平台兼容性缺失**：Windows用户无法正常使用`ironclaw-reborn`，这限制了项目在更广泛开发者群体中的采用。

## 待处理积压

以下Issue/PR已开放一段时间，或涉及核心功能，需要维护者持续关注。

- **#5884：常规任务丢失凭据**：虽已有修复PR #6095 合并，但该问题涉及的任务（Routine）是用户自动化工作流的核心，后续需进行回归测试，确保修复有效。
    [查看 Issue #5884](https://github.com/nearai/ironclaw/issues/5884)

- **#6100：上下文窗口缓存可能被陈旧快照重新填充**：这是一个高风险的并发Bug，由核心开发者在对#6047问题修复的代码审查中发现。它虽为预先存在的Bug，但尚未修复，可能在高并发场景下引发消息遗漏或错误。
    [查看 Issue #6100](https://github.com/nearai/ironclaw/issues/6100)

- **#6102：验证文件系统会话线程服务的重建安全**：同样是并发相关的遗留问题，提出了一个理论上的性能与并发安全问题，需进一步通过代码审查和测试来验证。
    [查看 Issue #6102](https://github.com/nearai/ironclaw/issues/6102)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 LobsterAI GitHub 数据，为您生成 2026-07-15 的项目动态日报。

---

### **LobsterAI 项目日报 (2026-07-15)**

**数据快照日期**：2026-07-15

---

#### **1. 今日速览**

今日项目进入维护模式，核心活动聚焦于对存量问题进行批量清理与关键回溯补丁的合并。24小时内，项目团队关闭了4个历史遗留的 **Stale** Issue，并合并了3个Pull Request，**无**新Issue、新PR或新版本发布。团队明显在集中精力修复已知的稳定性问题，并回溯上游修复以强化核心Agent框架，整体活跃度评估为 **中等，偏向故障修复与稳定性提升**。

---

#### **2. 版本发布**

*无新版本发布。*

---

#### **3. 项目进展**

今日推进主要依赖 **3个已合并的Pull Request**，对项目的稳定性和核心Agent框架执行逻辑进行了关键加固：

- **核心Agent框架 (OpenClaw) 稳定性提升**：
    - **PR #2331** & **PR #2330**：这两个PR均来自同一作者，核心目标是对项目的Agent运行时（`OpenClaw`）进行回溯修复。
        - **PR #2331** (`fix(openclaw): terminate critical tool loops`) 引入了一个双层机制，用于在工具执行进入“**关键循环死锁**”时强制终止当前Agent运行，同时保留了正常插件的中止行为和兄弟工具的并发完成逻辑 [netease-youdao/LobsterAI PR #2331]。
        - **PR #2330** (`fix(openclaw): stop loop after aborted tool run`) 则专注于在工具执行被异常中止后，确保Agent循环能正确停止，避免无意义的后续执行，并引入了更强的补丁验证机制 [netease-youdao/LobsterAI PR #2330]。
        - **项目进展**：这两个修复直接提升了Agent在复杂或错误场景下的**健壮性和安全性**，减少了Agent“卡死”或执行失控的风险。

- **协作用户体验修复**：
    - **PR #2329** (`fix(cowork): prevent conversation scroll jumps`)：修复了在流式输出过程中，用户手动滚动查看历史消息时，滚动条被新消息“**自动拉回**”到底部的干扰问题。该PR通过尊重用户的“**手动滚动意图**”并取消待处理的自动滚动动作，显著提升了协作或浏览长对话时的体验 [netease-youdao/LobsterAI PR #2329]。

**总结**：项目在核心Agent引擎的可靠性上迈出了坚实一步，同时兼顾了日常使用中的交互细节打磨。

---

#### **4. 社区热点**

由于今日无新增活跃讨论，社区热点集中在今日被批量关闭的 **Stale** 历史Issue上。这些Issue虽无新评论，但其集中关闭反映了社区维护者正在清理积压，值得关注：

- **Issue #1386** (【会话-分享】长聊天内容截屏不全) [netease-youdao/LobsterAI Issue #1386]
- **Issue #1388** (【邮箱配置】测试连通性一直无响应) [netease-youdao/LobsterAI Issue #1388]
- **Issue #1389** (语言切换时中文项显示英文) [netease-youdao/LobsterAI Issue #1389]
- **Issue #1390** (定时任务偶现无法更新) [netease-youdao/LobsterAI Issue #1390]

**分析**：这些均为`2026-04-03`报告的，涉及**国际化显示**、**数据导出完整性**、**邮件配置**和**定时任务**等关键用户路径。它们在沉寂数月后被关闭，且无对应的修复PR被关联。这可能意味着维护者认为它们是偶发性问题、难以复现，或者已在不被发现的底层重构中修复。建议社区成员关注这些问题的原始提交者是否验证了最新版本的修复情况。

---

#### **5. Bug 与稳定性**

今日**无新Bug报告**。所有的稳定性工作均体现在已合并的PR中，已进行修复：

- **【高】Agent执行循环死锁/异常中止后失控**：
    - **风险**：Agent可能因工具循环死锁而持续空转，或在工具异常中止后仍试图执行后续步骤，浪费计算资源且可能导致状态错误。
    - **状态**：**已修复** (PR #2331, #2330 已合并)。
- **【中】协作/对话流式输出时滚动跳转**：
    - **风险**：用户在阅读长对话或代码生成结果时，手动滚动查看上下文会被新输出打断，体验极差。
    - **状态**：**已修复** (PR #2329 已合并)。

---

#### **6. 功能请求与路线图信号**

今日无明确的新功能请求。

从今日的PR来看，项目维护者的工作重心在于 **稳定性和基础体验**，而非引入新功能。这预示着下一版本可能聚焦于：
- **Agent运行时的健壮性**：避免Agent“挂起”或“失控”是提升用户信任的关键。
- **交互体验优化**：尊重用户交互意图（如手动滚动）是提升产品质感的持续方向。

没有迹象表明“邮箱配置”或“定时任务”等历史问题的相关修复会立即进入下一版本。

---

#### **7. 用户反馈摘要**

从今日被关闭的Stale Issue中，可以提炼出用户在数月前反馈的以下痛点：

- **使用场景痛点**：
    - **数据导出**：用户需要将完整的对话记录作为长图分享，但在内容较长时会**丢失部分信息**，这对需要汇报或存档的用户影响大。
    - **系统配置**：**邮箱配置的连通性测试**功能在配置错误时会直接卡死界面，用户只能被动作系统重启，体验原始且不符合“优雅降级”原则。
    - **定时任务**：定时任务的**编辑/更新操作偶现无效**，用户无法稳定维护自动化工作流，这是自动化场景下的致命问题。
- **国际化问题**：
    - 当系统语言设置为英文时，界面中的中文选项**仍以中文显示**，违反了语言选择的一致性预期，对于国际化用户是明显的UI bug。

**整体不满**：用户对核心配置和自动化功能的稳定性有一定期望，而这些Stale Issue的长时间存在可能影响了部分早期用户的信心。

---

#### **8. 待处理积压**

今日表现**健康，无新的严重积压**。

所有今日合并的PR均是在创建当天（2026-07-14）即被处理，响应速度优秀。被关闭的4个Issue虽已存在数月，但今日得到清理，表明维护者正在系统地回溯历史问题。目前**没有**观察到长期未被响应的关键Issue或PR处于停滞状态。项目积压管理状态良好。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 | 2026-07-15

## 1. 今日速览

今日项目活跃度 **较高**。过去24小时内，项目完成了一次小版本发布，并展现了高效的开发迭代节奏：共处理了12个 Pull Request，其中 **8 个已合并/关闭**，合并率高达 66.7%。社区讨论主要集中在 Bug 修复与依赖更新上，尤其在修复与 MCP 服务器（如 Notion）的 OAuth 兼容性问题及提升本地模型兼容性方面取得了实质进展。两个重要功能请求（本地 STT 引擎支持、浏览器自动截图）仍在等待最终评审或合并，是当前社区关注的焦点。

## 2. 版本发布

- **[RELEASE] 20260714.11**：今日发布了新版本 `20260714.11`。尽管未提供详细的变更日志，但根据已合并的 PR 判断，该版本应包含了对 GPT-5.6 系列模型的支持，以及对底层依赖（如 `esbuild`、`vite`）的安全性更新。建议用户及时升级以获取最新的模型兼容性和依赖安全修复。

## 3. 项目进展

今日项目的核心进展在于对稳定性的加固和新模型的兼容性适配。以下为今日合并/关闭的关键 PRs：

| PR | 状态 | 描述 | 影响评估 |
| :--- | :--- | :--- | :--- |
| [#1146](https://github.com/moltis-org/moltis/pull/1146) | **CLOSED (Merged)** | 添加 GPT-5.6 (Sol, Terra, Luna) 模型系列支持，并更新了上下文窗口限制和配置示例。 | **功能增强**。紧跟 AI 模型发展步伐，提升了项目的前沿性。 |
| [#1089](https://github.com/moltis-org/moltis/pull/1089) | **CLOSED (Merged)** | 在会话历史“再水合”时对持久化的工具结果进行截断，以防止上下文窗口溢出。 | **稳定性提升**。有效预防了因工具输出过大导致会话中断或异常的潜在问题。 |
| [#1098](https://github.com/moltis-org/moltis/pull/1098) | **CLOSED (Merged)** | 修复浏览器工具调用中因模型（如 Gemma 4）发送 `null` 参数导致的崩溃。 | **兼容性修复**。解决了与小型/本地模型交互时的常见痛点，显著提升了鲁棒性。 |
| [#1139](https://github.com/moltis-org/moltis/pull/1139) | **CLOSED (Merged)** | 修复构建问题：启用 `metrics` 特性不应强制拉取整个 Matrix SDK 依赖。 | **构建优化**。改善了依赖管理，避免不必要的编译负担。 |
| [#1120](https://github.com/moltis-org/moltis/pull/1120) | **CLOSED (Merged)** | 修复了与 Notion、Linear 等 MCP 服务器的 OAuth 认证失败问题。 | **关键 Bug 修复**。直接回应了社区 Issue #1119，恢复了与流行 MCP 服务的集成能力。 |
| [#1145](https://github.com/moltis-org/moltis/pull/1145) | **CLOSED (Merged)** | 修复 CalDAV 组件在处理非 ASCII 字符日期时间时可能发生的 panic 问题。 | **Bug 修复**。提升了与国际化数据源交互时的稳定性。 |

**整体评估**：项目在 **Bug 修复** 和 **健壮性** 方面取得了明确进展，同时依靠依赖更新和模型支持保持了技术先进性。

## 4. 社区热点

- **[PR #1124: Add context command support for chat turns](https://github.com/moltis-org/moltis/pull/1124)**
    - **状态**：OPEN (待合并，自6月15日起)
    - **热度分析**：这是一个 **高价值功能需求**，允许用户为每次聊天轮次注入动态上下文。该功能能满足自动化部署、动态系统提示等高级用例。虽未合并，但长达一个月的开放周期和其功能性表明社区对其非常期待且讨论深入，是当前社区最受关注的功能。

- **[Issue #1102: Feature: Add FunASR/SenseVoice as local STT engine](https://github.com/moltis-org/moltis/issues/1102)**
    - **状态**：OPEN
    - **热度分析**：该 Issue 持续活跃，最新更新中包含了对 FunASR 许可证和功能的详细澄清。这反映出社区对 **本地语音识别引擎** 的强烈需求，旨在减少对云服务的依赖，提升隐私性和离线可用性。

## 5. Bug 与稳定性

今日修复及报告的 Bug 主要集中在与 AI 模型交互的兼容性及外部服务集成上。

- **严重级别：高**
    - **MCP OAuth 认证失败**： Issue [#1119](https://github.com/moltis-org/moltis/issues/1119) 报告了连接 Notion、Linear 等 MCP 服务器时 OAuth 认证失败。此 Bug 直接影响核心用户体验。
        - **修复状态**：**已由 PR [#1120](https://github.com/moltis-org/moltis/pull/1120) 修复并合并**。
    - **“main” session 无法删除**： Issue [#1132](https://github.com/moltis-org/moltis/issues/1132) 报告了无法删除或归档“main”会话的问题。这可能是一个会话管理的设计决策或未预料的 Bug。
        - **修复状态**：**暂无关联 PR**。需要开发者进一步跟进。

- **严重级别：中**
    - **CalDAV 非 ASCII 日期 panics**： PR [#1145](https://github.com/moltis-org/moltis/pull/1145) 修复了 CalDAV 组件中因非 ASCII 字符导致的程序崩溃。
    - **浏览器工具调用 `null` 参数**： PR [#1098](https://github.com/moltis-org/moltis/pull/1098) 修复了 Gemma 等模型发送 `null` 参数导致的问题。
    - **字符串化标量参数**： PR [#1136](https://github.com/moltis-org/moltis/pull/1136) 修复了某些模型将布尔值、数字等标量参数以字符串形式发送的问题。

## 6. 功能请求与路线图信号

- **呼声最高的功能**：**本地 STT 引擎 (FunASR/SenseVoice)** (#1102)。该功能需求已存在超过一月，社区讨论热烈，表明用户对 **数据隐私** 和 **离线能力** 的诉求很高。如项目规划符合此方向，应优先考虑。
- **可能纳入下一版本的功能**：
    - **浏览器自动截图** ([#1135](https://github.com/moltis-org/moltis/pull/1135))：该 PR 旨在为每次浏览器动作后自动截图，以提供可视化步骤历史。功能成熟，PR 接近完成，很有潜力成为下一版本亮点。
    - **频道活动日志可见性设置** ([#1093](https://github.com/moltis-org/moltis/pull/1093))：针对频道协作场景的细粒度隐私控制，适合企业级用户。

## 7. 用户反馈摘要

- **满意/正面反馈**：从 Issue #1102 的更新来看，开发者（LauraGPT）提供了详尽的许可证和技术澄清，这种主动沟通显示了项目对社区输入的尊重，用户体验正面。
- **痛点/负面反馈**：
    - Issue #1132 提出了一个基本会话管理问题（无法删除“main” session），这可能会让部分用户感到困惑或不自由。
    - 多个 Bug (#1119, #1098, #1136) 都源于与特定 AI 模型（特别是本地/小型模型）的兼容性问题，这反映了 **模型碎片化** 导致的开发生态痛点，用户期望项目能更好地适配各种模型行为。

## 8. 待处理积压

- **关键 Issue 待响应**：
    - **#1132**: [[Bug]: "main" session can't be deleted/archived](https://github.com/moltis-org/moltis/issues/1132) - 创建已近一个月，暂无官方回应或修复。建议维护者评估此设计是否合理，或提供解决方案。
- **长期未合并功能 PR**:
    - **#1093**: [Add channel activity log visibility settings](https://github.com/moltis-org/moltis/pull/1093) - 自6月3日起开放，已超过一个月。建议维护者进行最终评审，以决定是否纳入主线。
- **依赖更新请求**：**Dependabot** 已提交新的依赖更新 PR [#1148](https://github.com/moltis-org/moltis/pull/1148) 以替代已合并的 #1141。此类机器人维护工作应及时处理，保持库的安全性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 | 2026-07-15

## 1. 今日速览

过去 24 小时，CoPaw 项目保持极高活跃度：共处理 50 条 Issue（其中新开/活跃 16 条，关闭 34 条）和 50 条 PR（待合并 24 条，已合并/关闭 26 条）。v2.0.0.post2 补丁版本发布，重点修复 Windows 沙箱递归爆炸、DeepSeek 上下文压缩破坏消息格式、自动记忆模块缺失等关键稳定性问题。社区围绕“沙箱可用性”、“上下文压缩导致会话永久损坏”、“消息队列回归”等痛点展开密集讨论，开发团队已快速响应，多个修复 PR 已提交并在审查中。整体项目健康度良好，Bug 修复节奏紧凑。

## 2. 版本发布

### v2.0.0.post2（补丁版本）

**发布时间**：2026-07-14 / 2026-07-15（根据时区）

**更新内容**：
- **功能改进**：`feat: more sensitive files & allow read global` — 扩展敏感文件检测范围，并允许全局读取（PR #6067）。
- **版本号升级**：`chore: bump version to 2.0.0post2`（PR #6070）。
- **测试增强**：`test(unit): runtime/security/install regression tests` — 增加运行时、安全性、安装相关的回归测试。

**破坏性变更**：无明确破坏性变更。

**迁移注意事项**：建议所有 v2.0.0 用户升级到此补丁版本，以解决已知的沙箱和上下文压缩问题。升级后需检查 `agent.json` 配置是否被重置（见 Issue #6100），建议升级前备份自定义配置。

## 3. 项目进展

今日合并/关闭的重要 PR 和功能推进：

- **治理/沙箱修复**：`fix(governance): honor sandbox_enabled switch in OFF-mode sandbox path`（PR #6109，已合并）— 修复 `approval_level=OFF` 时沙箱开关被忽略的问题，确保用户能彻底关闭沙箱。
- **自动记忆可靠性**：`feat(memory): improve ReMe reliability, observability, and CJK embedding safety`（PR #6098，已合并）— 增强记忆模块稳定性，解决中文 Embedding 超长截断错误 (#5950)，并增加运行时监控能力。
- **下载工具修复**：`fix(download_catalog): handle gzip-encoded JSON responses`（PR #6106，已合并）— 修复 `_fetch_json` 函数无法处理 gzip 压缩响应的问题。
- **Zalo 频道插件**：`feat(plugins): add Zalo Bot channel plugin (2.0)`（PR #6112，已合并）— 为 2.0 插件架构新增 Zalo Bot 频道支持（基于长轮询，无需 Webhook）。

**持续推进中的关键 PR**：
- #6123 `fix(scroll): prevent recall loops and enforce hard context limits` — 修复 Scroll 模式下的无限召回循环。
- #6122 `fix(governance): clear stale OFF-mode sandbox state` — 清理过期的 OFF-mode 沙箱状态。
- #6120 `fix(memory): restrict automatic memory to external user queries` — 防止自动记忆误判系统合成消息。
- #6108 `fix(context): keep tool results paired with assistant calls during context compression` — 保持上下文压缩后 tool 消息与 assistant 调用的配对关系。

项目整体向**稳定性与可用性**方向大步迈进，重点攻克 v2.0.0 引入的沙箱、记忆、上下文压缩三大类回归问题。

## 4. 社区热点

| 讨论热点 | 链接 | 评论数 | 核心诉求 |
|---------|------|--------|----------|
| [Issue #5951] Windows 沙箱 pwsh 递归爆炸、ACE 污染、沙箱无法关闭 | [链接](agentscope-ai/QwenPaw/issues/5951) | 9 | 沙箱实现严重缺陷，导致工具几乎不可用，用户要求紧急修复或提供关闭途径 |
| [Issue #578] OpenClaw 驱动的长期价值功能请求 | [链接](agentscope-ai/QwenPaw/issues/578) | 8 | 用户希望借鉴 OpenClaw 架构，实现“使用越久价值越高”的复合特性（持续跟踪） |
| [Issue #6089] 使用 opencode 免费模型报错 MODEL_EXECUTION_ERROR | [链接](agentscope-ai/QwenPaw/issues/6089) | 7 | 升级后无法使用免费模型，反馈强烈，但已被标记为无效（invalid） |
| [Issue #6113] 一直卡在搜索记忆（无休止循环） | [链接](agentscope-ai/QwenPaw/issues/6113) | 5 | 更新到 2.0 后自动记忆检索导致对话停滞，用户抱怨“好烦” |
| [Issue #6023] Sandbox & Tool Guard 大修 — 减少摩擦同时保持安全 | [链接](agentscope-ai/QwenPaw/issues/6023) | 3 | 维护者主动收集沙箱和工具守卫反馈，社区响应积极 |

**分析**：社区最强烈的诉求集中在 **沙箱可用性** 和 **自动记忆行为**。Windows 用户因沙箱递归爆炸、ACE 污染系统目录而无法使用；部分用户记忆检索进入死循环；DeepSeek 用户因上下文压缩导致会话永久损坏（#6077、#6046）。开发团队已针对这些问题提交 PR，社区情绪正在好转。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列：

| 严重程度 | Issue | 描述 | 修复状态 |
|---------|-------|------|----------|
| **致命** | #5951 | Windows 沙箱 pwsh 递归爆炸、内存吃满 20GB、ACE 污染系统目录 | 已关闭（v2.0.0.post2 部分修复，仍需关注） |
| **致命** | #6121 | DeepSeek 长会话触发上下文压缩后报错 `400`，会话永久不可用 | 已有 PR #6108（审查中） |
| **致命** | #6009 | scroll 上下文压缩触发不准，无硬上限导致 session 被上游拒绝 | 已有 PR #6123（待合并） |
| **高** | #6116 | Agent 单轮内重复执行相同工具调用（Doom loop） | 已有 PR #6120 修复自动记忆误判相关部分 |
| **高** | #6100 | 升级到 2.0.0.post1 后 `agent.json` 被覆盖为空配置，丢失 `active_model` 等字段 | 未明确修复，建议用户备份 |
| **高** | #6020 | 审批系统路由错误（钉钉端发起但弹窗在电脑端）+ `approval_level: OFF` 配置失效 | PR #6122 部分修复 |
| **中** | #6097 | macOS Desktop frozen build 缺少 `agentscope.tool._builtin._scripts`，导致 Glob 工具和 auto-memory 崩溃 | 已关闭（v2.0.0.post2 修复？需确认） |
| **中** | #6088 | v2.0.0.post1 消息队列回归，Agent 运行时无法发送新消息 | 已关闭（可能通过 PR #6040 修复） |

**总结**：v2.0.0 系列存在多个高影响回归，团队已快速响应，半数以上 Bug 已有对应修复 PR 正在进行或已合并。

## 6. 功能请求与路线图信号

今日用户提出的新功能需求：

- **#6048**：免认证主机白名单支持 CIDR 段配置 — 用于企业网络环境安全策略细化。
- **#5976**：分开控制 channel 工具调用参数和结果的发送，支持截断显示 — 提升 IM 频道用户体验。
- **#6087**：在 Agent 迭代循环中实时注入用户新消息 — 避免 Agent 偏离方向后无法及时纠正，减少计算浪费。
- **#6064**：优化底层架构易用性，对标 Hermes Agent，实现桌面环境直接交互 — 建议 QwenPaw 集成内置浏览器插件。
- **#5964**：升级后聊天列表与对话历史映射丢失 — 虽属 Bug，但暴露了数据迁移兼容性需求。

**路线图信号**：从 #6023 维护者主动发起的 Sandbox & Tool Guard 大修讨论可以看出，开发团队正计划在 v2.1 中重新设计沙箱和审批系统，以平衡安全性与可用性。同时，#578 长期跟踪的 OpenClaw 复合价值特性仍在规划中。

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实痛点与使用场景：

- **Windows 用户**：“升级后沙箱根本没法用，pwsh 窗口无限弹出，内存直接爆满。卸载桌面壳、回退配置都没用。”（#5951）
- **记忆机制**：“每次提问先疯狂检索记忆，无休止循环，还不如 1.0 的逻辑，太烦了！”（#6113）
- **DeepSeek 用户**：“说不了两句话会话就挂了，升级 v2.0 后此问题频发，完全无法工作。”（#6046）
- **审批系统**：“钉钉端发起的审批弹窗却显示在电脑端，`approval_level: OFF` 也关不掉审批，必须重启。”（#6020）
- **频道管理**：“工具调用结果太长了，希望可以单独控制是否发送，或者只显示前几行。”（#5976）
- **升级体验**：“从 1.1.9 升级到 2.0.0.post1 后，默认 agent 的 `agent.json` 被清空了，所有模型配置丢失。”（#6100）

**积极反馈**：社区对 #6023 维护者主动收集反馈表示认可，用户愿意配合提供沙箱使用场景。Zalo 频道的加入（PR #6118）获得越南社区期待。

## 8. 待处理积压

以下为长期未响应或值得维护者关注的重要 Issue/PR：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue | #5964 | 升级到 2.0.0 后聊天列表与对话历史映射丢失 | 2026-07-11 | 2026-07-14 | 影响数据迁移，尚未有关联修复 PR |
| Issue | #578 | [Meta] OpenClaw-Inspired Features for Compounding Agent Value | 2026-03-04 | 2026-07-14 | 长期功能追踪，需要规划路线图优先级 |
| PR | #5187 | feat(computer-use): Windows desktop GUI automation | 2026-06-14 | 2026-07-14 | 大型功能 PR，审查周期过长，社区期待 |
| Issue | #6116 | Doom loop: agent repeatedly triggers same tool call | 2026-07-14 | 2026-07-14 | 新报 Bug，虽有部分修复但根因尚未完全定位 |
| PR | #5731 | fix(runtime): honor per-request model override | 2026-07-02 | 2026-07-14 | 首次贡献者 PR，需维护者 review，已等待近两周 |

**建议**：优先分配 reviewer 处理 #5731（防止挫伤新贡献者热情）；#5964 数据迁移问题若影响面大，建议在 v2.0.1 中修复；#5187 的 Windows 桌面自动化可考虑拆分为小 PR 分阶段合并。

---

**报告生成时间**：2026-07-15  
**数据来源**：GitHub (agentscope-ai/QwenPaw)  
**分析师**：AI 智能体与个人 AI 助手领域开源项目分析师

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 (2026-07-15)

## 今日速览
过去24小时项目持续高活跃度：共处理29条Issue（新开/活跃23条，关闭6条）和50条PR（待合并38条，已合并/关闭12条）。SOP（标准操作程序）引擎的成熟度显著提升——多个长期遗留的SOP bug被关闭，包括审计静默失效、cron触发器无调用者、headless步骤误完成等。安全与多租户领域仍是社区关注焦点，`per-sender RBAC` 和 `Landlock` 沙箱问题讨论热烈。主分支上新的OpenAI兼容API端点（PR #8486）和Matrix频道进度草案（PR #8443）两个XL级PR仍在等待作者响应，显示大型功能合并前的审查周期较长。

## 版本发布
当日无新版本发布。

## 项目进展
### 已关闭/合并的Bug修复与功能（关键项）
| 编号 | 类型 | 简介 | 影响力 |
|------|------|------|--------|
| [#8678](https://github.com/zeroclaw-labs/zeroclaw/issues/8678) | Bug (CLOSED) | `advance_step`缺少运行状态守卫，驱动可绕过审批门 | 修复S2级审批完整性漏洞 |
| [#8631](https://github.com/zeroclaw-labs/zeroclaw/issues/8631) | Bug (CLOSED) | 无头确定性SOP步骤记录为Completed但未执行 | 修复虚假审计轨迹，阻塞实际运行 |
| [#8695](https://github.com/zeroclaw-labs/zeroclaw/issues/8695) | Bug (CLOSED) | Cron任务即使`uses_memory=false`仍召回记忆 | 修复S2级行为不一致 |
| [#6689](https://github.com/zeroclaw-labs/zeroclaw/issues/6689) | Bug (CLOSED) | 生产SOP审计静默无操作：文档中的记忆键从未写入 | 消除S3级文档-实现鸿沟 |
| [#8413](https://github.com/zeroclaw-labs/zeroclaw/issues/8413) | Enhancement (CLOSED) | 添加`channel-filesystem` SOP事件源 | 允许文件落地触发SOP工作流 |

**PR方面**：
- [#9077](https://github.com/zeroclaw-labs/zeroclaw/pull/9077) (CLOSED)：修复网络部署文档中`channel start`命令多余参数错误。
- [#8582](https://github.com/zeroclaw-labs/zeroclaw/pull/8582) (CLOSED)：修复ZeroCode在连接超时后未清理ephemeral守护进程的问题。

**整体推进**：SOP调度、审计、触发机制三个关键子系统的核心bug已被清除，为v0.8.4维护列车（#8357）扫清障碍。多用户里程碑（#8290）的OIDC基础正在稳步推进。

## 社区热点
### 最活跃Issue讨论
1. **[#5982 - Per-sender RBAC for multi-tenant agent deployments](https://github.com/zeroclaw-labs/zeroclaw/issues/5982)**
   - 评论数：10条 | 👍 0 | 标签：enhancement, security, priority:p2
   - 诉求：单实例支持多用户类（客户、运维、开发者）的隔离工作区、工具集、速率限制和系统提示。
   - 分析：这是多租户安全基石的呼声，已有配套Tracker [#8290](https://github.com/zeroclaw-labs/zeroclaw/issues/8290) 跟踪，预计进入v0.8.4或更晚版本。

2. **[#6055 - Slack: hydrate thread context from conversations.replies](https://github.com/zeroclaw-labs/zeroclaw/issues/6055)**
   - 评论数：7条 | 标签：channel:slack, enhancement
   - 痛点：启用`strict_mention_in_thread`后用户需反复@机器人才触发处理。
   - 现状：已被接受（status:accepted），等待实现。

3. **[#8973 - Landlock blocks shell access to required system files on Fedora](https://github.com/zeroclaw-labs/zeroclaw/issues/8973)**
   - 评论数：4条 | 标签：bug, security, priority:p1
   - 问题：启用Landlock沙箱后`sh`无法访问`/dev/null`，导致shell工具总是失败。
   - 影响：S2级降级行为，但未影响资金转移或RCE。暂无修复PR。

### 大型PR关注
- [#8486 - feat(gateway): add OpenAI chat completions endpoint](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)（size:XL，needs-author-action）
  社区期待已久的OpenAI兼容HTTP API，将使ZeroClaw支持LangChain、Continue.dev等现有工具链。但由于作者需要响应审查意见，合并被搁置。

## Bug与稳定性
按严重程度降序排列（S0为最高）：

| 严重度 | Issue | 标题 | 状态 | 是否有Fix PR |
|--------|-------|------|------|-------------|
| **S0** | [#7947](https://github.com/zeroclaw-labs/zeroclaw/issues/7947) | `execute_pipeline`绕过每代理工具门控（confused deputy） | OPEN | 无 |
| **S1** | [#8563](https://github.com/zeroclaw-labs/zeroclaw/issues/8563) | SOP在Web Dashboard聊天会话中不可用 | OPEN | 无 |
| **S1** | [#8675](https://github.com/zeroclaw-labs/zeroclaw/issues/8675) | 原生工具调用参数畸形未验证导致Provider 400→空回复 | OPEN | 无 |
| **S1** | [#9052](https://github.com/zeroclaw-labs/zeroclaw/issues/9052) | `channel-line`被排除在CI全量覆盖之外 | OPEN | 无 |
| **S2** | [#8973](https://github.com/zeroclaw-labs/zeroclaw/issues/8973) | Landlock阻断shell访问系统文件（Fedora） | OPEN | 无 |
| **S2** | [#9001](https://github.com/zeroclaw-labs/zeroclaw/issues/9001) | Provider失败原因被通用重试包裹掩盖 | OPEN | 无 |
| **S2** | [#8695](https://github.com/zeroclaw-labs/zeroclaw/issues/8695) | Cron任务忽略`uses_memory`标志 | CLOSED | ✅ 已修复 |

**重点风险**：S0的`execute_pipeline`权限绕过若被利用可导致未授权工具执行，但当前报告要求调用者已有agent驱动权限，实际利用门槛较高。团队已标记为security领域最高优先级。

## 功能请求与路线图信号
| 请求 | 标签 | 关联PR/里程碑 | 可能纳入版本 |
|------|------|--------------|-------------|
| [#5982] Per-sender RBAC | security, multi-tenant | 跟踪器[#8290] | v0.8.4+ |
| [#8933] OTel跨轮对话关联 | observability | RFC待讨论 | v0.8.4 |
| [#9048] 对话历史与长期记忆分离 | memory, architecture | RFC待维护者审查 | 未定 |
| [#5607] Cron/触发器前置跳过门 | cron, security | 长期open（自2026-04） | 倾向v0.8.5 |
| [#8581] 集中化SOP入口适配层 | sop, architecture | 跟进[#8521] | 可能随SOP 5/5上线 |
| [#8719] SOP路由：false `when`应跳转到下一步 | sop | 接受但待实现 | v0.8.4 |
| [#8358] zerorelay中继节点 | network, security | 里程碑当前目标 | v0.8.4 |
| PR #8486 OpenAI兼容端点 | gateway | 需要作者回复 | 若本周合并，可入v0.8.4 |
| PR #8863 插件WebSocket外发 | plugins, wasm | 独立栈，等待审查 | 下一候选版本 |

**关键信号**：多租户（RBAC）、可观测性（OTel关联）、SOP增强（路由、Adapter、审批）是社区持续推动的方向。OpenAI兼容API一旦合并，将显著降低外部工具接入门槛。

## 用户反馈摘要
从Issue评论中提炼的真实痛点：

1. **Landlock沙箱兼容性**（#8973）：Fedora用户`perillamint`报告启用Landlock后shell工具完全失效，因为`sh`无法访问`/dev/null`。期望行为是在沙箱中自动开放必须的设备文件。
2. **Web Dashboard缺少SOP支持**（#8563）：用户`susyabashti`表示将SOP配置文件放置在标准目录后，agent无法识别，工作流完全阻塞（S1）。说明文档与实际注册路径可能存在偏差。
3. **Provider错误诊断困难**（#9001）：用户`Audacity88`指出不同Provider（如LM Studio、Ollama）的失败被统一包裹为“所有Provider失败”，无法定位具体原因。期望为不同失败类型提供明确分类。
4. **SOP HTTP入口未接线**（#6685）：文档声明`POST /sop/*`和`/webhook`端点可用于SOP，但实际代码未实现。用户`JordanTheJet`在5月即报告，至今未修复，社区期待官方响应。
5. **Memory隔离不彻底**（#9048）：用户`Audacity88`指出对话历史与长期记忆在实现中仍混合存储，尽管概念上分离。建议将Conversation历史移出通用记忆后端，避免污染精细查询。

## 待处理积压
以下Issue/PR因长期未响应或缺乏维护者关注，需提醒团队。

| 编号 | 类型 | 创建时间 | 最后更新 | 阻塞原因 |
|------|------|----------|----------|----------|
| [#6685](https://github.com/zeroclaw-labs/zeroclaw/issues/6685) | Bug | 2026-05-15 | 2026-07-14 | 文档声明但代码未实现SOP HTTP fan-in，需决定是否修复或移除文档 |
| [#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) | Enhancement | 2026-04-10 | 2026-07-14 | 请求前置跳过门功能，已被接受但一直处于blocked状态 |
| [#7947](https://github.com/zeroclaw-labs/zeroclaw/issues/7947) | Bug (S0) | 2026-06-18 | 2026-07-14 | 严重安全漏洞（confused deputy），虽注释少但风险极高，未见修复PR |
| [#8353](https://github.com/zeroclaw-labs/zeroclaw/pull/8353) | PR | 2026-06-26 | 2026-07-15 | 改进错误消息上下文，needs-author-action超过3周 |
| [#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) | PR (XL) | 2026-06-29 | 2026-07-15 | OpenAI兼容端点，作者需要响应审查意见，已标记needs-author-action |

**建议**：
- S0安全漏洞#7947应立刻分配维护者评估修复方案。
- #6685 和 #5607 这类历史遗案可考虑在v0.8.4维护列车中一并决策（继续实现或标记为wontfix）。
- 两个XL级PR（#8486、#8443）若本周仍无作者回应，应主动联系或考虑其他贡献者接手。

---

*本日报基于GitHub数据自动生成，统计截止时间2026-07-15 12:00 UTC。*

</details>

---
*本日报由 [agents-radar](https://github.com/zhouyuhechuan/agents-radar) 自动生成。*