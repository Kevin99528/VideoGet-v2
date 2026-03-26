# VideoGet Git 分支工作流指南

## 分支结构

```
main (主分支) ──────── 生产环境，稳定版本
    ↑
develop (开发分支) ──── 集成测试，功能汇总
    ↑
feature/* (功能分支) ── 具体开发，临时存在
```

## 分支说明

### main 分支
- **定位**: 生产环境代码，永远保持稳定
- **保护**: 禁止直接提交，只能通过合并 develop 更新
- **触发**: 代码更新后自动部署到生产环境

### develop 分支
- **定位**: 开发集成中心，所有功能的汇合点
- **保护**: 禁止直接提交，只能通过合并 feature/* 更新
- **触发**: 用于集成测试和预发布验证

### feature/* 分支
- **定位**: 具体功能开发，临时存在
- **命名**: `feature/功能名称`，如 `feature/ai-summary`
- **生命周期**: 创建 → 开发 → 合并到 develop → 删除

## 工作流程

### 1. 开始新功能开发

```bash
# 确保在 develop 分支
 git checkout develop

# 拉取最新代码（如果是团队协作）
git pull origin develop

# 创建功能分支
git checkout -b feature/your-feature-name

# 开始开发...
```

### 2. 功能开发中

```bash
# 查看修改的文件
git status

# 添加修改到暂存区
git add .

# 提交修改
git commit -m "feat: 添加xxx功能"

# 继续开发...
```

### 3. 功能完成，合并到 develop

```bash
# 切换到 develop 分支
git checkout develop

# 合并功能分支
git merge feature/your-feature-name

# 删除功能分支（可选）
git branch -d feature/your-feature-name
```

### 4. 发布到 main

```bash
# 切换到 main 分支
git checkout main

# 合并 develop
git merge develop

# 打标签（可选）
git tag -a v1.0.0 -m "版本 1.0.0"
```

## 常用命令

| 命令 | 说明 |
|------|------|
| `git branch` | 查看所有分支 |
| `git branch -a` | 查看所有分支（包括远程） |
| `git checkout 分支名` | 切换到指定分支 |
| `git checkout -b 新分支名` | 创建并切换到新分支 |
| `git merge 分支名` | 合并指定分支到当前分支 |
| `git branch -d 分支名` | 删除分支 |
| `git log --oneline` | 查看简洁提交历史 |
| `git status` | 查看当前状态 |

## 注意事项

1. **不要直接在 main 分支上开发**
2. **功能分支命名要有意义**，如 `feature/download-progress` 而不是 `feature/test`
3. **经常提交代码**，不要等到功能完成才提交
4. **提交信息要清晰**，如 `feat: 添加下载进度显示` 而不是 `update`
5. **功能完成后及时合并并删除功能分支**，保持仓库整洁

## 紧急情况处理

### 如果改坏了代码

```bash
# 放弃所有未提交的修改（谨慎使用）
git checkout .

# 回退到上一个提交
git reset --hard HEAD

# 回退到指定提交（通过 git log 查看提交ID）
git reset --hard 提交ID
```

### 如果提交了敏感信息

```bash
# 修改最后一次提交
git commit --amend

# 然后强制推送（如果是已推送的提交）
git push --force
```

## 提交信息规范

格式：`类型: 描述`

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: 添加AI视频总结功能` |
| `fix` | 修复bug | `fix: 修复下载进度不更新问题` |
| `docs` | 文档更新 | `docs: 更新API文档` |
| `style` | 代码格式 | `style: 格式化代码` |
| `refactor` | 重构 | `refactor: 优化下载逻辑` |
| `test` | 测试 | `test: 添加单元测试` |
| `chore` | 构建/工具 | `chore: 更新依赖版本` |
