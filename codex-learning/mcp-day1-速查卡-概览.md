# MCP Day 1 速查卡：概览

## 一句话记忆

- MCP：AI 世界的 `USB-C`
- Host：总控应用
- Client：连接器
- Server：能力提供者

## 3 个核心原语

- `Tools`
  - 模型可调用的动作
  - 有副作用风险
- `Resources`
  - 只读上下文数据
- `Prompts`
  - 可复用提示模板

## 2 层结构

- `Data layer`
  - JSON-RPC 2.0
  - 生命周期
  - 能力协商
  - tools/resources/prompts/notifications
- `Transport layer`
  - `stdio`
  - `Streamable HTTP`

## 角色分工

- Host：协调多个 MCP client
- Client：维护到某个 server 的连接
- Server：暴露能力给 client

## 高频判断

- 要“做事”：
  - 大概率是 `tool`
- 要“给模型看资料”：
  - 大概率是 `resource`
- 要“复用提示套路”：
  - 大概率是 `prompt`

## 为什么重要

- 一次接入，多处复用
- 让 AI 从“只会回答”变成“能读、能查、能做”

## 安全速记

- tool 默认高风险
- 本地 server 默认最小权限
- 工具描述也可能是不可信输入
- 用户授权不能省
- 大 scope 不要一上来就全给

## 最新口径

- 截至 `2026-05-21`，官方规范页显示最新协议版本：`2025-11-25`
- 当前主流基础传输：`stdio`、`Streamable HTTP`
