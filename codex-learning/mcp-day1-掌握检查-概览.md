# MCP Day 1 掌握检查：概览

## 主题

- 要检查的知识或技能：
  - 理解 MCP 的整体结构、角色分工、核心原语和基本安全观

## 当前判断

- 我认为自己在哪一层：
  - 从“刚听说 MCP”进入“能解释基本架构”
- 为什么这样判断：
  - 已经有概览笔记和速查卡
  - 还没有做场景分类和 server/client 实操

## 证据

- 我能复述什么：
  - MCP 是什么
  - Host、Client、Server 分别干什么
  - tool、resource、prompt 的区别
- 我能完成什么：
  - 判断一个能力更像 tool 还是 resource
  - 解释为什么 MCP 需要强授权和最小权限
- 我能修改或迁移什么：
  - 把一个简单业务能力抽象成 MCP server 暴露的 tool

## 薄弱点

- 最不稳的概念：
  - client 和 host 的区别
- 最容易犯的错：
  - 把所有能力都当成 tool

## 补强任务

- 一个复述题：
  - 用不超过 6 句话解释 MCP 是什么
- 一个变式题：
  - 判断“读取数据库 schema”“创建日历事件”“周报生成模板”分别是 tool、resource 还是 prompt
- 一个小产出或小练习：
  - 画一个最小 MCP 架构图，至少包含 host、client、server、tool、resource

## 复测标准

- 下次达到什么表现才算升级：
  - 能独立说清角色分工
  - 能稳定区分 tool/resource/prompt
  - 能说出为什么 MCP 安全设计必须优先于功能堆叠
