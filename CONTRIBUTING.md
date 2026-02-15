# Agent 贡献指南

## 如何迭代本 Skill: Abacus-Developer

本项目使用 Fork + PR 工作流，无需仓库推送权限即可贡献。

### 1. Fork 仓库

点击仓库页面右上角的 **Fork** 按钮，将仓库 fork 到你的 GitHub 账号。

或者使用 GitHub API:
```bash
curl -X POST https://api.github.com/repos/SciX-Skill/skill-abacus-developer-1ed42f/forks \
  -H 'Authorization: token $GITHUB_TOKEN'
```

### 2. 克隆你 fork 的仓库

将 `<YOUR_USERNAME>` 替换为你的 GitHub 用户名：
```bash
git clone https://github.com/<YOUR_USERNAME>/skill-abacus-developer-1ed42f.git
cd skill-abacus-developer-1ed42f
```

### 3. 创建新版本分支

```bash
# 基于 main 分支创建新版本分支
git checkout -b version/v2 main
# 或如果 version/v1 已存在，基于它创建
git checkout -b version/v2 version/v1
```

### 4. 修改 SKILL.md 和实现代码

### 5. 提交并推送
```bash
git add .
git commit -m "feat: update skill to v2"
git push origin version/v2
```

### 6. 创建 Pull Request

从你的 fork 创建 PR 到原始仓库的 version/v2 分支：
```bash
# 方法 1: 使用 gh CLI（推荐）
gh pr create --base version/v2 --head version/v2 \
  --title "feat: update skill to v2" \
  --body "## 改进\n- 更新内容"

# 方法 2: 使用 GitHub API
curl -X POST https://api.github.com/repos/SciX-Skill/skill-abacus-developer-1ed42f/pulls \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
-d '{
    "title": "feat: update skill to v2",
    "head": "version/v2",
    "base": "version/v2"
  }'
```

### 7. 等待自动合并

- 提交后系统会自动运行 CI
- CI 通过后自动合并到 main 分支
- 版本号自动更新

## 版本规则

- 每个版本对应一个 PR
- PR 必须指向 `version/v{n+1}` 分支
- CI 成功后会自动合并到 main

## 反馈问题

如果使用本 Skill 遇到问题，请提交 Issue 或 PR！
