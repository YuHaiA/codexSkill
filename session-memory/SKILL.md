---
name: session-memory
description: Extract durable project memory from Codex sessions, convert it into project-level memory skills, and decide when old sessions can be archived or removed. Use when Codex sessions are growing large, when you want to preserve reusable project knowledge outside session history, or when you need to migrate stable facts, decisions, and conventions into a project-scoped memory skill.
---

# Session Memory Maintainer

## 目标

从 session 里提炼“可长期复用”的项目记忆，写入项目级 skill，避免把临时对话长期挂在活跃 session 里。

## 适用场景

- session 变大、UI 变慢、历史加载卡顿
- 需要把稳定项目知识从聊天记录迁移出去
- 需要判断某个 session 是否已经可以归档或移除
- 需要维护“全局规则 + 项目级记忆”两层结构

## 基本原则

- 只保留稳定事实、长期偏好、架构决策、项目约束、已确认流程。
- 不写临时任务进展、一次性排错过程、未确认猜测、敏感信息、原始日志。
- 全局 skill 只负责规则和流程，项目级 skill 才承载具体记忆。
- 先写入项目级 skill，再考虑清理 session。
- 若用户请求 session 清理，默认按自动流程执行，不需要再为常规清理步骤逐项确认。
  - 这条仅适用于 session / archived session / session index 这类会话清理流程。
  - 仍然要遵守项目边界、先提取后清理、以及全局资源默认不动的规则。
- 每次清理前都必须先做一次“是否存在可提取稳定记忆”的检查。
  - 不能因为上一次清理时已经提取过，就默认这一次没有新增记忆点。
  - 只要本轮候选 session 中还有新的稳定事实、长期约束、确认过的流程或复用性强的坑点，就先写入项目级 skill / `SYSTEM.md`，再继续清理。
- 默认按“当前项目”收敛范围：在某个项目目录中启动时，只处理 `cwd` / `rollout_path` / session 内容明确属于该项目的 session。
- 只有用户明确说“全局清理 / 所有项目 / 全部 session / 清全局日志”时，才允许扩大到全局范围。
- 如果无法确认某个 session 属于当前项目，宁可跳过，不要误删其他项目上下文。

## 工作流

1. 先定位项目根目录和对应 session。
2. 只读取和该项目有关的 session 段落。
3. 先判断这批候选 session 里是否存在尚未迁移的稳定记忆点。
4. 提炼稳定记忆点，按 [project-memory-format.md](references/project-memory-format.md) 整理。
5. 写入或更新项目级 skill。
6. 验证项目级 skill 已保存后，只删除已迁移完成、明确属于当前项目、且不再作为活跃上下文的旧 session。

## 项目边界

- 当前项目的判断优先级：
  - `state_*.sqlite` / session meta 中的 `cwd` 指向当前项目根目录。
  - session 文件名对应的 thread id 在 `session_index.jsonl` 或线程状态中能关联到当前项目标题 / 路径。
  - session 正文中反复出现当前项目根路径、项目名、核心文件路径，并且没有明显属于其他项目的工作目录。
- 不要因为 session 位于同一个全局 `sessions` 或 `archived_sessions` 目录，就把它视为当前项目可清理对象。
- 不要批量清空全局 `archived_sessions`，除非用户明确要求全局清理。
- 清理前必须先输出候选数量、路径范围、预计释放空间，并说明是否仅限当前项目。
- 若用户要求“瘦身 / 清理旧 session / UI 不要未响应”，默认解释为清理当前项目相关旧 session，不代表授权清理其他项目。

## 选择 session

- 优先看 `session_index.jsonl` 和最近 session 的 `session_meta`。
- 优先选择和当前项目路径一致的 session。
- 优先选择最近一次、覆盖面最大、信息最完整的 session。
- 避免把跨项目、跨账号、纯噪声对话混进来。

## 抽取规则

- 抽取对象：
  - 项目目标
  - 技术栈和目录约定
  - 重要接口、状态流、数据流
  - 已确认的设计决策
  - 长期有效的操作规程
  - 反复出现且稳定的偏好
- 不抽取对象：
  - 短期排障过程
  - 临时 workaround
  - 未验证结论
  - 大段原文
  - 密钥、Token、Cookie、身份证号等敏感信息

## 写入位置

- 项目级 skill 放在项目自己的 `.codex/skills/` 下。
- 项目级 skill 只记录该项目自己的记忆点。
- 如果项目还没有对应 skill，先创建最小可用骨架，再补记忆。
- 全局 skill 不存放项目专属内容。

## 清理规则

- 记忆已成功落到项目级 skill 后，才考虑清理旧 session。
- 若本轮检查结果为“没有新增可提取记忆”，也要在回报中明确说明“已检查，无新增稳定记忆”，不能跳过这个检查步骤。
- 只删除已经完成迁移、明确属于当前项目、且不再是当前活跃线程来源的 session。
- 活跃、未稳定、仍在反复引用的 session 不删。
- 对 Codex 应用左侧线程列表中的旧项目线程，默认动作应是“归档”而不是放任其继续停留在活跃列表里；前提仍然是这些线程已完成记忆迁移、明确属于当前项目，且不是当前活跃线程。
- 任何删除都要先确认“记忆已迁移成功”。
- 清理操作优先删除 / 压缩明确的体积来源，不要把“清理”扩大解释为删除全部历史。
- 全局日志库如 `logs_2.sqlite` 属于全局资源；只有用户明确点名该文件或明确要求全局日志瘦身时才处理。

## 参考

- [session-extraction-rules.md](references/session-extraction-rules.md)
- [project-memory-format.md](references/project-memory-format.md)
