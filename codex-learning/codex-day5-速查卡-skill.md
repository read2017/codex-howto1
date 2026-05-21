# Codex Day 5 速查卡：Skills

## 一句话记忆

- `Skill`：可复用工作流
- `AGENTS.md`：项目总规则
- `Plugin`：可分发的打包单元

## Skill 最小结构

```text
my-skill/
  SKILL.md
```

## SKILL.md 必要字段

```md
---
name: skill-name
description: 说明什么时候该触发、什么时候不该触发
---
```

## Skill 何时触发

- 显式触发：你直接点名 skill
- 隐式触发：任务和 `description` 匹配

## description 怎么写

- 先写核心用途
- 再写触发场景
- 再写边界和排除项
- 关键词尽量前置

## 什么时候适合做 Skill

- 重复流程
- 有明确输入输出
- 能拆成固定步骤
- 值得跨多次任务复用

## 什么时候不适合

- 一次性问题
- 纯背景知识堆砌
- 作用范围过宽
- 跟仓库无关的临时提示

## 官方最佳实践

- 一次只做一件事
- 优先 instruction-only
- 步骤写成祈使句
- 明确输入输出
- 测试触发描述

## 保存位置

- repo-local：`.agents/skills`
- user-level：`$HOME/.agents/skills`
- 可分发时用 plugin

## 高频结论

- skill 不是越长越好，而是越聚焦越好
- skill 的关键不在“文采”，在“触发边界 + 流程稳定 + 输出明确”
- 如果一个流程你已经重复解释了 3 次，通常就该考虑写成 skill
