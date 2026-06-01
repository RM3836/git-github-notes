# GitHub CLI (gh) 操作手册

## 一、安装与认证

```bash
# 安装 gh CLI
sudo apt install gh   # Ubuntu/Debian
brew install gh       # macOS

# 登录 GitHub
gh auth login
# 选择：GitHub.com → HTTPS → Paste token 或 浏览器登录

# 查看认证状态
gh auth status

# 刷新 token 权限
gh auth refresh -h github.com
```

## 二、仓库操作

### 创建仓库

```bash
# 创建本地仓库并推送到 GitHub（最常用）
gh repo create 仓库名 --public --source=. --push

# 创建私有仓库
gh repo create 仓库名 --private --source=. --push

# 带描述
gh repo create 仓库名 --public --description "这是描述" --source=. --push

# 在指定目录创建
gh repo create 仓库名 --public --source=/path/to/dir --push
```

### 克隆仓库

```bash
# 克隆自己的仓库
gh repo clone 仓库名

# 克隆别人的仓库
gh repo clone 用户名/仓库名

# 克隆到指定目录
gh repo clone 用户名/仓库名 /path/to/dir
```

### 查看仓库

```bash
# 查看仓库信息
gh repo view 用户名/仓库名

# 在浏览器打开
gh repo view --web

# 列出自己的仓库
gh repo list

# 列出指定用户的仓库
gh repo list 用户名

# 限制数量
gh repo list --limit 10
```

### 仓库操作

```bash
# fork 仓库
gh repo fork 用户名/仓库名

# 归档仓库
gh repo archive 仓库名

# 删除仓库（危险！）
gh repo delete 仓库名 --yes
```

## 三、Issue 操作

```bash
# 创建 Issue
gh issue create --title "标题" --body "内容"

# 交互式创建
gh issue create

# 查看 Issue 列表
gh issue list

# 查看指定 Issue
gh issue view 编号

# 关闭 Issue
gh issue close 编号

# 重新打开
gh issue reopen 编号
```

## 四、Pull Request 操作

```bash
# 创建 PR
gh pr create --title "标题" --body "内容"

# 交互式创建
gh pr create

# 查看 PR 列表
gh pr list

# 查看指定 PR
gh pr view 编号

# 合并 PR
gh pr merge 编号

# 检出 PR（本地测试）
gh pr checkout 编号
```

## 五、GitHub Actions

```bash
# 查看工作流列表
gh workflow list

# 查看工作流运行记录
gh run list

# 查看运行详情
gh run view 运行ID

# 手动触发工作流
gh workflow run 工作流名

# 查看日志
gh run view 运行ID --log
```

## 六、GitHub Gist

```bash
# 创建 Gist
gh gist create 文件名

# 创建私有 Gist
gh gist create 文件名 --public=false

# 列出 Gist
gh gist list

# 查看 Gist
gh gist view GistID

# 编辑 Gist
gh gist edit GistID
```

## 七、搜索

```bash
# 搜索仓库
gh search repos 关键词

# 搜索 Issue
gh search issues 关键词

# 搜索代码
gh search code 关键词

# 搜索用户
gh search users 关键词
```

## 八、实用技巧

### 1. 快速推送本地项目

```bash
# 一步完成：创建仓库 + 推送
gh repo create my-project --public --source=. --push
```

### 2. 设置默认仓库

```bash
# 设置当前目录的默认远程仓库
gh repo set-default 用户名/仓库名
```

### 3. 查看仓库的 Release

```bash
gh release list --repo 用户名/仓库名
```

### 4. 下载 Release 资产

```bash
gh release download 标签 --repo 用户名/仓库名
```

## 九、gh vs git 对照表

| 操作 | git 命令 | gh 命令 |
|------|----------|---------|
| 克隆 | `git clone URL` | `gh repo clone 用户/仓库` |
| 推送 | `git push` | `git push`（gh无替代）|
| 创建仓库 | 网页操作 | `gh repo create` |
| 创建Issue | 网页操作 | `gh issue create` |
| 创建PR | 网页操作 | `gh pr create` |

## 十、常见问题

### Q1: 权限不足 (403)

```bash
# 刷新 token
gh auth refresh -h github.com
```

### Q2: 推送被拒

```bash
# 先拉取再推送
git pull --rebase origin main
git push
```

### Q3: 中文文件名显示为八进制

```bash
git config --global core.quotepath false
```

---

*gh CLI 版本：2.x | 适用环境：Linux/macOS/WSL*