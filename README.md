# Codex 技能集合

这个仓库同步了我当前全局 `~/.codex/skills` 目录中的自定义 Codex 技能，覆盖前端设计、交互、调试、自动化和工作流辅助等场景。

## 当前包含的技能

- `adaptive-structure-architect`：响应式结构和信息层级设计。
- `advanced-color-synthesizer`：配色系统、颜色层级和对比优化。
- `aesthetic-code-rules`：界面代码风格和视觉实现约束。
- `element-plus-patterns`：Vue 3 + Element Plus 常见业务流实现模式。
- `frontend-api-debugger`：前端接口联调和请求链路排查。
- `frontend-skill`：落地页、网站、应用、原型和游戏界面设计。
- `interaction-motion-designer`：动效语言、过渡效果和交互节奏优化。
- `layout-design-engine`：版式结构、间距节奏和整体布局设计。
- `pattern-recognition-engine`：界面模式抽取和系统一致性分析。
- `playwright`：浏览器自动化、页面流程调试和截图采集。
- `premium-ui-polish`：界面质感、阴影层次、排版和细节打磨。
- `screenshot`：系统级截图能力和相关脚本。
- `session-memory`：会话知识沉淀和项目记忆提取。
- `sora`：Sora 视频生成、编辑和批量工作流。
- `vue3-admin-crud`：Vue 3 后台 CRUD 页面和管理流模板。

## 仓库结构

每个技能都放在独立目录下，通常包含以下文件：

- `SKILL.md`：技能主说明和使用指引。
- `agents/openai.yaml`：供兼容工具读取的技能元数据。
- `references/`、`assets/`、`scripts/`：按技能需要提供的参考文档、资源和脚本。

## 说明

本地还存在一个空目录 `codex-primary-runtime`，因为没有实际文件，Git 不会追踪它，所以当前未纳入仓库。
