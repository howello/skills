# Howe Skills

个人 Claude Code 技能库，用于增强和定制 Claude Code 的工作流程。

## 目录结构

```
.
├── README.md              # 本文件 - 项目概览
├── skills/                # 技能文件存放目录
│   ├── _template/         # 新建技能时的参考模板
│   │   └── SKILL.md
│   ├── dev-workflow/      # 开发工作流技能
│   │   └── SKILL.md
│   └── <skill-name>/      # 各技能文件夹
│       └── SKILL.md       # 技能定义文件（必需入口）
├── templates/             # 项目/代码模板（非技能文件）
├── scripts/               # 辅助脚本
└── .claude/
    └── settings.json      # Claude Code 项目配置
```

## 技能格式

每个技能是一个独立文件夹，内含 `SKILL.md` 文件，包含 YAML frontmatter：

```markdown
---
name: skill-name
description: 简短描述，说明技能的用途
metadata:
  type: skill
---

技能的具体指令内容...
```

## 如何添加新技能

1. 在 `skills/` 目录下创建 `<技能名>/` 文件夹
2. 在该文件夹内创建 `SKILL.md`，参考 `skills/_template/SKILL.md` 的格式编写
3. 在 `INDEX.md` 中登记

## 使用方法

在 Claude Code 会话中，直接描述需求，Claude 会自动匹配合适的技能。或者通过相关关键词触发。

## 设计原则

- **单一职责**：每个技能只做一件事
- **清晰描述**：description 字段能准确反映技能用途
- **可组合**：技能之间可以按需组合使用
