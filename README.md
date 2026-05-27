# AI Assisted Engineering Skill

一份面向 AI 辅助软件开发与 LLM 应用构建的可分享 Skill。

它帮助开发者和 AI Agent 在使用模型提高效率的同时，继续守住工程质量底线：范围清晰、上下文克制、能力渐进、结果可验证、成本可治理、安全边界明确。

## 这是什么

`ai-assisted-engineering` 是一个适用于 Codex 风格 `SKILL.md` 机制的技能包，也可以被其他能够读取 Markdown 指令的 AI Agent 手动加载。

它不是框架教程的复制品，也不是一个 AI 应用脚手架项目。它提供的是一套可复用的工程工作方式，用于指导 Agent 或开发者：

- 实现 AI 辅助的代码修改、重构、审查与成本优化。
- 构建聊天、RAG、Agent、Tool Calling、MCP 或流式响应功能。
- 在 `Spring AI`、`LangChain4j` 一类集成方案中保持清晰的服务边界。
- 在模型能力、价格或 API 持续变化时，知道哪些结论必须回到官方资料验证。

## 适用场景

| 场景 | Skill 提供的帮助 |
| --- | --- |
| 使用 AI 编程助手修改现有项目 | 约束范围、控制上下文、验证改动，而不是盲目生成代码 |
| 开发聊天或助手类应用 | 建立模型调用边界、会话记忆、流式响应与错误处理思路 |
| 开发 RAG 知识库问答 | 引导检索测试、来源展示和提示词注入防护 |
| 开发工具调用或 MCP 能力 | 强调参数校验、最小权限、审批边界与日志 |
| 控制模型使用成本 | 减少无关上下文和无效输出，但不以牺牲测试或安全为代价 |
| 进行架构选型或代码审查 | 要求结合仓库惯例、官方文档和实际验证做判断 |

## 核心原则

1. 先定义交付结果，再让 AI 动手。
2. 只提供当前任务真正需要的上下文。
3. 从最小可测能力开始，按需求增加记忆、检索、工具、流式输出和可观测性。
4. 验证行为与失败路径，不把模型输出当成正确性的证明。
5. 优化成本时，保留必要的测试、审查、文档、安全与错误处理。
6. 对模型价格、额度、功能和框架接口等时效性信息，优先核对官方来源。

## 快速开始

### 1. 安装到 Codex

将仓库中的 `ai-assisted-engineering` 目录复制到个人 Codex 技能目录。需要复制的是技能子目录，不是整个仓库。

Windows PowerShell:

```powershell
git clone https://github.com/rapdoxxl/yupiSkill.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -Recurse -Force .\yupiSkill\ai-assisted-engineering "$env:USERPROFILE\.codex\skills\"
```

macOS / Linux:

```bash
git clone https://github.com/rapdoxxl/yupiSkill.git
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R yupiSkill/ai-assisted-engineering "${CODEX_HOME:-$HOME/.codex}/skills/"
```

安装后，在新的或已刷新技能列表的 Codex 会话中使用该技能。

### 2. 在 Codex 中调用

显式调用示例：

```text
使用 $ai-assisted-engineering 为现有 Spring Boot 服务增加带引用来源的 RAG 问答接口，并完成必要验证。
```

```text
使用 $ai-assisted-engineering 审查这个 MCP 工具服务的权限边界、参数校验和可观测性。
```

```text
使用 $ai-assisted-engineering 降低当前 AI 编程工作流的 token 消耗，但不要省略必要测试和安全检查。
```

### 3. 在其他 AI Agent 中使用

如果你的 Agent 不支持自动发现 Skill，可将入口文件直接提供给它：

```text
Read ./ai-assisted-engineering/SKILL.md and follow it while completing this task:
Implement a streamed chat endpoint with session memory and safe error handling.

If the task includes chat, RAG, tools, MCP, agents, or streaming, also read:
./ai-assisted-engineering/references/ai-application-checklist.md
```

## 给 AI Agent 的读取协议

以下协议用于让 AI 能够稳定、低歧义地加载本 Skill：

```text
Skill name: ai-assisted-engineering
Required entrypoint: ./ai-assisted-engineering/SKILL.md
Conditional reference: ./ai-assisted-engineering/references/ai-application-checklist.md

Load the conditional reference when the task involves:
- model-backed chat
- RAG or retrieval
- agent workflows
- tool calling or MCP
- streamed model responses

Execution contract:
1. Establish the deliverable, touched boundaries, risks, and acceptance checks.
2. Gather only relevant context and confirm changing provider/framework facts from primary sources.
3. Implement incrementally using existing project conventions.
4. Preserve tests, security, secret handling, failure handling, and appropriate approvals.
5. Verify the result and report remaining assumptions.

Output contract:
- scoped implementation or recommendation
- verification performed
- unresolved provider/runtime assumptions or risks
```

## 使用方式示例

### 示例一：聊天接口

需求：

```text
使用 $ai-assisted-engineering 给我的 Java 服务增加流式聊天接口，需要支持多会话和断线错误处理。
```

期望行为：

- Agent 先检查现有控制器、服务、配置和测试模式。
- 仅在需要时增加会话记忆与 SSE 流式接口。
- 将 API Key 留在安全的外部配置中。
- 验证接口协议、错误处理和关键测试。

### 示例二：RAG 问答

需求：

```text
使用 $ai-assisted-engineering 实现内部文档问答，需要显示回答来源，并评估提示词注入风险。
```

期望行为：

- Agent 将检索效果与生成效果分开验证。
- 对检索内容视为不可信输入，避免其覆盖系统约束或扩大工具权限。
- 设计来源标识或引用信息。
- 在决定上线前说明评估数据、隐私与成本风险。

### 示例三：成本优化

需求：

```text
使用 $ai-assisted-engineering 优化我们的 AI 编程成本。
```

期望行为：

- Agent 优先减少无关上下文、冗余输出与不必要的高成本模型使用。
- Agent 不会建议为了节省 token 取消必要的测试、审查、安全控制或错误处理。
- 对当前价格、套餐或模型能力的判断会要求依据官方最新信息。

## 文件结构

```text
yupiSkill/
|-- README.md
`-- ai-assisted-engineering/
    |-- SKILL.md
    |-- agents/
    |   `-- openai.yaml
    `-- references/
        `-- ai-application-checklist.md
```

| 文件 | 面向对象 | 用途 |
| --- | --- | --- |
| `README.md` | 人类读者与需要手动加载的 Agent | 发布说明、安装方式、使用示例与读取协议 |
| `ai-assisted-engineering/SKILL.md` | Skill 运行时 | 触发范围、核心工作流、成本纪律与质量边界 |
| `ai-assisted-engineering/agents/openai.yaml` | 支持技能 UI 的客户端 | 展示名称、简述与默认调用提示 |
| `ai-assisted-engineering/references/ai-application-checklist.md` | 处理 AI 应用功能的 Agent | 聊天、RAG、工具、MCP、流式响应与验证清单 |

## 质量边界

本 Skill 有意排除以下做法：

- 为了节省 token 而跳过必要测试、审查、安全处理或文档。
- 把模型输出、教程宣传或基准结论直接当作生产事实。
- 在仓库、提示词或日志中暴露 API Key 与敏感配置。
- 在没有验证和审批边界的情况下让工具执行破坏性、财务、账号或生产操作。
- 将侮辱、虚构威胁或所谓越狱技巧作为工程方法。

## 来源与取舍

该 Skill 最初从 [liyupi/ai-guide](https://github.com/liyupi/ai-guide) 中筛选有工程价值的部分进行沉淀，尤其包括：

- `LangChain4j` 项目实践中关于模型调用、会话记忆、RAG、Tools/MCP、SSE 与可观测性的思路。
- 关于聚焦上下文和关注模型成本的有效提醒。

本 Skill 并非原仓库的镜像或全文转载。对于其中偏推广、偏娱乐化、或会降低工程质量的建议，未予采纳；对于模型和框架的动态信息，使用时应核对官方资料。

## 校验

该 Skill 按 Codex Skill 结构组织，并已使用 `skill-creator` 提供的结构校验器验证：

```bash
python "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" ./ai-assisted-engineering
```

有效的技能目录应至少保留：

- `SKILL.md` 及其 YAML frontmatter 中的 `name` 和 `description`。
- `agents/openai.yaml` 中的界面元数据。
- `references/` 下被入口文件明确引用的按需资料。

## 贡献

欢迎通过 Issue 或 Pull Request 贡献改进，尤其是：

- 可复用的 AI 应用验证清单。
- 能降低上下文噪声、同时不损害质量的协作方法。
- 对聊天、RAG、MCP、流式输出或可观测性边界的补充。

修改 `SKILL.md` 或引用资料时，请保持规则简洁、可验证，并避免加入易过时而未经来源确认的模型结论。

## 许可说明

本仓库当前未附带独立开源许可证。公开可阅读不等同于自动授予复制、修改或再发布许可；若计划开放复用，请由仓库所有者补充明确的 `LICENSE` 文件。
