# Skills Library

## 自动加载指令

每次对话自动遵循 `dev-workflow` 技能定义的开发流程。

## 技能路径

本项目包含自定义技能，存放在 `skills/` 目录下。每个技能是一个独立文件夹，内含 `SKILL.md` 文件作为入口描述文件。Claude 会自动加载这些技能。

## 技能格式

每个技能文件夹必须包含 `SKILL.md` 文件，包含 YAML frontmatter：
- `name`: 技能名称
- `description`: 简短描述
- `metadata.type`: 固定为 `skill`

## 约定

- git commit 使用中文，保持简短
- 新增技能时需同时在 INDEX.md 中登记
