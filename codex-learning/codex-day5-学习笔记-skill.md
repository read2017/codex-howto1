# Codex Day 5 学习笔记：Skills

## 主题

- 本次主题：理解 Codex `Skills` 是什么、什么时候该用、怎么写一个最小可用 skill
- 来源资料：
  - OpenAI Codex 官方文档：Agent Skills
  - OpenAI 官方 GitHub 仓库：`openai/skills`
  - 当前仓库中的 skill 草稿样例

## 核心概念

- `Skill`
  - Codex 的可复用工作流封装格式
  - 一个 skill 可以打包说明、参考资料、可选脚本、模板资源
- `SKILL.md`
  - skill 的核心文件
  - 至少包含 `name` 和 `description`
- 渐进加载
  - Codex 一开始只拿到 skill 的名字、描述、路径
  - 只有当它决定使用这个 skill 时，才会读取完整 `SKILL.md`

## 结构框架

- 一个 skill 的最小目录结构：

```text
my-skill/
  SKILL.md
```

- 常见扩展结构：

```text
my-skill/
  SKILL.md
  scripts/
  references/
  assets/
  agents/openai.yaml
```

- 一句话总览：
  - `Skill` 是“可复用工作流”，不是“随便塞一段长提示词”

## 技术要点

- 触发方式：
  - 显式触发：直接点名 skill
  - 隐式触发：任务和 `description` 高度匹配
- `description` 很关键：
  - 要写清楚什么时候该触发
  - 也要写清楚什么时候不该触发
- 常见保存位置：
  - repo-local：`.agents/skills`
  - user-level：`$HOME/.agents/skills`
  - 也可以通过插件分发

## 什么时候该用 Skill

- 适合：
  - 重复出现的固定流程
  - 某个任务总要先看哪些文件、再做哪些检查、最后产出什么
  - 某类仓库或子目录有稳定工作方法
- 不适合：
  - 一次性问题
  - 只有背景知识、没有操作流程的长文档
  - 过于宽泛、什么都想管的说明书

## 和 AGENTS.md 的区别

- `AGENTS.md`
  - 项目级总规则
  - 回答“在这个仓库里整体应该怎么做事”
- `Skill`
  - 任务级或流程级封装
  - 回答“遇到这类任务时应该按什么步骤做”

一句话区分：

- `AGENTS.md` 更像仓库操作手册
- `Skill` 更像具体工作流的 SOP

## 官方最佳实践

- 一个 skill 只做一件事
- 默认优先写说明，不急着加脚本
- 步骤要用祈使句，输入输出要明确
- 要测试 skill 的触发描述是否足够准确

## 当前仓库样例

本仓库已新增一个 skill 草稿：

- 路径：`codex-learning/codex-learning-notes-SKILL-draft.md`
- 用途：当你在这个仓库里学习 Codex，并要求整理学习笔记、复盘、错题、速查卡时，把内容统一落到 `codex-learning/`

这个样例体现了 skill 最重要的 3 点：

1. 触发范围清楚
2. 输出目录清楚
3. 步骤顺序清楚

## 常见混淆点

- 容易和什么混淆：把 skill 当成“超长系统提示词”
  - 区别是什么：
    - skill 应该针对一个明确任务族，而不是无限扩张
- 容易和什么混淆：把所有规则都塞进 skill
  - 区别是什么：
    - 全局规则更适合放在 `AGENTS.md`
- 容易和什么混淆：一上来就写很多脚本
  - 区别是什么：
    - 官方建议优先 instruction-only，只有需要确定性行为时再加脚本

## 我的理解

- 我现在能怎么解释：
  - Skill 是 Codex 的“可发现、可复用、可渐进加载”的任务工作流封装
  - 它最适合把高频动作变成稳定流程
- 我还没搞清楚什么：
  - 一个团队里哪些流程应该做成多个细 skill，哪些应该合并成一个
  - 什么时候需要额外的 skill 元数据

## 微产出任务

阅读当前仓库中的 skill 草稿，并尝试用自己的话回答：

1. 它是为哪类任务设计的？
2. 它的输入是什么？
3. 它要求产出什么？
4. 为什么这件事适合做成 skill，而不是只放在聊天里口头说明？

## 下一步

- 要补的资料：
  - `AGENTS.md` 官方文档
  - `openai/skills` 仓库中的 curated skill 样例
- 要做的练习或产出：
  - 自己写一个“修 bug 流程”或“学习笔记整理流程”的最小 skill
