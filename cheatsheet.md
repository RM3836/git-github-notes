# Git & GitHub 一页速查表

## 日常操作

```bash
# 初始化并推送到 GitHub
gh repo create 项目名 --public --source=. --push

# 日常提交流程
git add . && git commit -m "说明" && git push

# 克隆仓库
gh repo clone 用户名/仓库名

# 查看状态
git status

# 拉取更新
git pull
```

## 仓库管理

```bash
# 列出我的仓库
gh repo list

# 查看仓库信息
gh repo view 用户名/仓库名

# 在浏览器打开
gh repo view --web

# 同步 fork
gh repo sync 用户名/仓库名
```

## 分支操作

```bash
# 创建并切换分支
git checkout -b 新分支名

# 查看分支
git branch -a

# 合并分支
git merge 分支名

# 删除分支
git branch -d 分支名
```

## 撤销操作

```bash
# 撤销工作区修改
git restore 文件名

# 撤销暂存
git restore --staged 文件名

# 修改最后一次提交
git commit --amend -m "新说明"
```

## Issue & PR

```bash
# 创建 Issue
gh issue create --title "标题" --body "内容"

# 创建 PR
gh pr create --title "标题" --body "内容"

# 查看 PR 列表
gh pr list
```

## 配置

```bash
# 设置用户信息
git config --global user.name "余凯楠"
git config --global user.email "steam3836@foxmail.com"

# 解决中文乱码
git config --global core.quotepath false

# 查看认证状态
gh auth status
```

## 常见问题速解

| 问题 | 命令 |
|------|------|
| 中文文件名乱码 | `git config --global core.quotepath false` |
| 推送被拒 | `git pull --rebase origin main` |
| 权限不足 | `gh auth refresh -h github.com` |
| 撤销未提交修改 | `git restore .` |
| 查看远程地址 | `git remote -v` |

## 文件路径对照

| Windows | WSL |
|---------|-----|
| `D:\` | `/mnt/d/` |
| `C:\Users\` | `/mnt/c/Users/` |
| 微信文件 `D:\software\xwechat_files\` | `/mnt/d/software/xwechat_files/` |

---

**记忆口诀**：
- 初始化：`init → add → commit`
- 日常流：`改 → add → commit → push`
- 推新库：`gh repo create --push`（一行搞定）