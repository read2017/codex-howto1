# MCP Day 1 学习笔记：概览

## 主题

- 本次主题：快速建立 Model Context Protocol（MCP）的整体心智模型
- 来源资料：
  - 官方介绍：<https://modelcontextprotocol.io/docs/getting-started/intro>
  - 官方架构：<https://modelcontextprotocol.io/docs/learn/architecture>
  - 官方规范：<https://modelcontextprotocol.io/specification>
  - 官方资源说明：<https://modelcontextprotocol.io/specification/2025-06-18/server/resources>
  - 官方客户端最佳实践：<https://modelcontextprotocol.io/docs/develop/clients/client-best-practices>
  - 官方安全最佳实践：<https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices>
  - 官方参考服务器仓库：<https://github.com/modelcontextprotocol/servers>

## 核心概念

- MCP 是什么
  - MCP（Model Context Protocol）是一个开源协议，用来把 AI 应用连接到外部系统
  - 官方类比是 AI 世界里的 `USB-C`
- MCP 解决什么问题
  - 让 AI 应用以统一方式访问外部数据、工具和工作流
  - 避免每个 AI 客户端都为每个外部系统单独做一套私有集成
- MCP 不解决什么
  - 它只规定“上下文交换协议”
  - 它不规定你的 AI 应用怎么用 LLM，也不规定产品 UI 该怎么做

## 结构框架

- 参与者
  - Host：AI 应用本体，例如 Claude Desktop、ChatGPT、VS Code 插件
  - Client：Host 内部负责连接某个 MCP Server 的连接器
  - Server：对外暴露能力的程序
- 两层结构
  - Data layer：基于 JSON-RPC 2.0，负责能力协商、工具调用、资源读取、通知等
  - Transport layer：负责进程间或网络间传输
- 三个核心原语
  - Tools：可执行操作
  - Resources：只读上下文
  - Prompts：可复用提示模板

一句话总览：

- Host 管总控
- Client 负责连线
- Server 提供能力
- Tool 干活
- Resource 给上下文
- Prompt 给套路

## 关键概念拆解

### 1. Tools

- 定义：
  - 由模型主动调用的函数能力
- 例子：
  - 查天气
  - 写文件
  - 调数据库
  - 调 GitHub API
- 特征：
  - 有输入 schema
  - 有执行结果
  - 通常风险最高，因为它可能产生副作用

### 2. Resources

- 定义：
  - 提供给模型或用户的只读上下文数据
- 例子：
  - 文件内容
  - 数据库 schema
  - API 文档
  - 应用状态快照
- 特征：
  - 更像“把信息拿来给模型看”
  - 常常比 tool 更安全，但依然涉及隐私和授权

### 3. Prompts

- 定义：
  - 预先设计好的提示模板
- 例子：
  - “总结会议记录”
  - “根据这个资源生成周报”
- 特征：
  - 它不是外部动作能力
  - 更像可复用交互入口

## 传输方式

- `stdio`
  - 本地进程间通信
  - 常见于本地 MCP server
  - 优点：简单、快、没有网络开销
- `Streamable HTTP`
  - 远程服务通信
  - 常见于远程 MCP server
  - 优点：适合多客户端、适合服务化部署

截至 `2026-05-21`，官方规范页显示最新协议版本为 `2025-11-25`。官方当前规范页列出的基础传输是 `stdio` 和 `Streamable HTTP`。

## 为什么 MCP 重要

- 对开发者：
  - 一次实现，多客户端复用
- 对 AI 应用：
  - 能快速接入越来越多的外部能力
- 对终端用户：
  - AI 终于不只是“会说”，而是“能读、能查、能做”

## 官方最佳实践

- 小规模工具集可以直接加载，大规模工具集应做 progressive discovery
- 不要把所有 tool definition 一次性塞进模型上下文
- 工具描述和工具注释也要当作不可信输入看待
- 本地 server 尽量最小权限运行
- 用户必须明确同意高风险操作和数据暴露

## 安全要点

- MCP 很强，但强在“能执行”，也因此风险高
- 官方规范强调 4 个安全原则：
  - User Consent and Control
  - Data Privacy
  - Tool Safety
  - LLM Sampling Controls
- 官方安全最佳实践特别提醒：
  - 高亮危险命令模式，例如 `sudo`、`rm -rf`、网络访问、越界文件访问
  - 本地 server 最好跑在受限环境里
  - 权限要渐进式提升，而不是一开始就给大 scope

## 关键例子或案例

- 例子 1：本地 filesystem server
  - Host 通过 `stdio` 启动本地 server
  - Server 暴露目录读取或写入能力
  - 模型可以在授权后查看或修改指定目录内容
- 例子 2：远程 GitHub server
  - Host 通过 `Streamable HTTP` 连接远程服务
  - Server 提供仓库搜索、issue 查询、PR 操作等能力
- 例子 3：多 server 场景
  - 一个 AI 应用同时连 filesystem、GitHub、calendar、database
  - Host 统一协调，模型按需触发对应工具

## 常见混淆点

- 容易和什么混淆：把 MCP 理解成“某个单独产品”
  - 区别是什么：
    - MCP 是协议，不是单一产品
- 容易和什么混淆：把 tool、resource、prompt 混成一类
  - 区别是什么：
    - tool 是执行
    - resource 是上下文
    - prompt 是模板
- 容易和什么混淆：把 MCP server 当成 agent
  - 区别是什么：
    - server 提供能力
    - agent/host 决定何时使用这些能力

## 我的理解

- 我现在能怎么解释：
  - MCP 是 AI 应用连接外部世界的标准接口层
  - 它最重要的不是“有多少 server”，而是“角色分工和安全边界”
- 我还没搞清楚什么：
  - 真实项目里什么时候该自己写 server，什么时候该直接接现成 server
  - 远程 MCP 的认证和授权在工程上应该怎么设计

## 下一步

- 要补的资料：
  - 官方 Build an MCP server 教程
  - 官方 Build an MCP client 教程
  - 官方 MCP Inspector 文档
- 要做的练习或产出：
  - 用自己的话画出 Host / Client / Server 关系
  - 判断 5 个场景里哪些是 tool、resource、prompt
