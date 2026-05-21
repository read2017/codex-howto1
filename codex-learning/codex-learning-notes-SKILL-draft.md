---
name: codex-learning-notes
description: Use when the user is learning Codex in this repository and asks to organize study notes, review notes, mistake logs, cheat sheets, or mastery checks into Markdown files under codex-learning/. Do not use for unrelated coding tasks, one-off concept explanations, or generic chat that does not need repository artifacts.
---

# Codex Learning Notes

Use this skill when the task is part of the structured Codex learning workflow in this repository.

## Goal

Turn repeated learning interactions into reusable repository artifacts instead of leaving them only in chat.

## Output location

Write all study outputs under `codex-learning/`.

Preferred file types:

- study notes
- review notes
- cheat sheets
- mistake logs
- mastery checks

## Workflow

1. Identify the learning topic for the current round.
2. Decide whether the task is a reusable learning workflow rather than a one-off explanation.
3. Choose the output artifact that best fits the task:
   - study notes for concept learning
   - cheat sheet for quick recall
   - mistake log for corrections and misconceptions
   - mastery check for evaluation
   - session review for short learning retrospectives
4. Reuse the repository's existing naming style when possible:
   - `codex-dayN-学习笔记-主题.md`
   - `codex-dayN-速查卡-主题.md`
   - `codex-dayN-错题整理-主题.md`
   - `codex-dayN-掌握检查-主题.md`
   - `codex-dayN-复盘-主题.md`
5. Summarize the key concept in concise, reusable language.
6. Distinguish facts from advice when the source is mixed.
7. If the conversation includes mistakes or corrections, record:
   - the original answer
   - the corrected answer
   - the error pattern
   - the next review point
8. Prefer compact Markdown that is easy to scan and continue later.

## Boundaries

- Do not create files outside `codex-learning/` unless the user explicitly asks.
- Do not treat unrelated engineering work as a learning-note task.
- Do not use this skill for one-off concept Q&A that does not need reusable notes.
- Do not dump raw chat transcripts into files; rewrite them into structured notes.

## Completion standard

The result should be useful even if the original chat is no longer available.
