---
name: pss-dev-sync
description: 手动触发，从指定 git 提交提取变更文件的当前版本，打包为 modify.zip 供审查或分享。
metadata:
  type: skill
  tags: [git, file, archive, manual]
---

# 提取提交文件 (pss-dev-sync)

手动触发的技能。将某次提交中变更的文件（当前工作区版本）复制到 `modify/` 文件夹并打包为 zip。

## 触发方式

手动调用，通过 `Skill` 工具或 `/pss-dev-sync` 触发。

## 执行步骤

### 0. 检查 worktree 状态

如果当前在 git worktree 中，先切回主分支：

```powershell
git worktree list
# 如果当前在 worktree 中，切换到主分支目录
```

### 1. 预备检查

如果项目根目录已存在 `modify/` 文件夹或 `modify.zip` 文件，先询问用户是否删除。

### 2. 获取提交列表

```powershell
git log --oneline -5
```

显示最近 5 个提交，格式为：

```
序号. [缩写哈希] 提交信息
```

### 3. 用户选择

等待用户选择其中一个提交（输入序号或哈希）。

### 4. 获取变更文件列表

```powershell
git diff-tree --no-commit-id -r --name-only <commit-hash>
```

### 5. 复制文件到 modify/

为每个变更文件创建对应的目录结构：

```powershell
# 对每个文件执行
$file = "<相对路径>"
$dest = "modify/$file"
$dir = Split-Path $dest -Parent
if ($dir) { New-Item -ItemType Directory -Path $dir -Force | Out-Null }
Copy-Item $file $dest
```

跳过已不存在的文件（该文件可能已在后续提交中被删除）。

### 6. 打包压缩

```powershell
Compress-Archive -Path ./modify -DestinationPath ./modify.zip -Force
```

### 7. 清理

删除 `modify/` 目录：

```powershell
Remove-Item ./modify -Recurse -Force
```

### 8. 完成

告知用户 `modify.zip` 已生成。

## 注意事项

- 复制的是文件的**当前工作区版本**（HEAD），而非该提交时的历史版本
- 仅在当前工作区干净时操作效果最佳
- 已删除的文件会跳过（不会报错）
- 压缩包生成在项目根目录
