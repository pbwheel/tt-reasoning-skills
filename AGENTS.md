# AGENTS.md

本仓库的 AI 贡献者指南；人类贡献者同样适用。

## 仓库布局

- `skills/<name>/SKILL.md`：13 个 skill（12 个原子 skill + `reason` 路由器）
- `protocols/`：5 份共享协议，是路由与行为的规范性文档
- `evals/`：行为导向的路由 / 边界 / 组合用例（不是措辞快照）
- `examples/`：四类典型工作流示例
- `README.md`（中文，主文档）与 `README.en.md`（英文镜像）：内容必须同步修改
- `package.json`：纯元数据，无 scripts 无依赖，`version` 即发布锚点

## 硬性约定

- skill 与 protocol 正文保持**英文**；两份 README 保持中英对应
- SKILL.md 的 YAML frontmatter 只允许 `name` 和 `description` 两个字段；其余路由属性（Category、Primary gap、Use when / Do not use when、Input requirements、Questions、Evidence policy、组合字段、Termination）放在正文 `## Metadata` 段，遵照 `protocols/reasoning-contract.md`
- 措辞平台无关：不要引入特定 CLI 的专有语法（如 `$command`、`--flag`）；平台差异只在 README 的调用说明里描述
- 不引入构建工具、脚本或依赖；仓库保持纯 Markdown
- 本仓库公开发布：不要提交个人邮箱、绝对路径、密钥或本地笔记（`docs/superpowers/` 已 gitignore）

## 新增一个 skill

1. 在 `skills/<kebab-name>/` 创建 `SKILL.md`：frontmatter（name + description，description 须含正向与负向触发条件）+ `## Metadata` 段 + 正文
2. 对照 `protocols/reasoning-contract.md` 自查元数据与行为要求
3. 在 `evals/` 对应文件补用例（路由、边界或组合）
4. 如影响路由：更新 `protocols/skill-boundaries.md`
5. 两份 README 开头的技能表（缺口 / Skill / 原文方法 / 它做什么）各加一行
6. 版本：用户可见行为变化升 minor，内部润色升 patch

## 发布流程

- 语义化版本写在 `package.json` 的 `version`
- 不设 CHANGELOG：git 历史即 changelog
- 发布 = 升版本 → 提交 → 打 `vX.Y.Z` tag → 推送
