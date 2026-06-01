# Git & GitHub 操作知识库

> YURM | 广州应用科技学院 网络工程专业
> 更新时间：2026-06-01

## 📚 目录结构

```
git-github-notes/
├── README.md              # 本文件 - 总览
├── 01-git-basics.md       # Git 基础命令速查
├── 02-github-cli.md       # GitHub CLI (gh) 操作手册
├── 03-repo-management.md  # 仓库管理最佳实践
├── 04-practice-cases.md   # 实战案例集
└── cheatsheet.md          # 一页速查表
```

## 🎯 知识库定位

**不是**Git教程大全，而是**实战中真正用到的命令**。

每条命令都经过验证，每个案例都是真实操作。

## 📋 快速导航

| 场景 | 文件 | 关键命令 |
|------|------|----------|
| 初始化仓库 | 01-git-basics.md | `git init` → `git add` → `git commit` |
| 推送到GitHub | 02-github-cli.md | `gh repo create --push` |
| 克隆/拉取 | 03-repo-management.md | `git clone` / `git pull` |
| 文件提交 | 04-practice-cases.md | 完整实战流程 |

## 🔥 最常用命令 TOP 5

```bash
# 1. 初始化并推送新仓库
gh repo create 仓库名 --public --source=. --push

# 2. 日常提交
git add . && git commit -m "说明" && git push

# 3. 克隆仓库
gh repo clone 用户名/仓库名

# 4. 查看状态
git status

# 5. 拉取更新
git pull
```

## ⚠️ 常见坑

1. **文件名中文乱码** → Git默认不转义，用 `git config --global core.quotepath false`
2. **大文件推送失败** → GitHub限制100MB，用 Git LFS
3. **权限被拒** → 检查 `gh auth status`

---

*本知识库持续更新，每次实战后补充案例。*