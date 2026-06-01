# Git 基础命令速查

## 一、配置（首次使用）

```bash
# 设置用户信息
git config --global user.name "余凯楠"
git config --global user.email "steam3836@foxmail.com"

# 解决中文文件名显示问题
git config --global core.quotepath false

# 设置默认分支名
git config --global init.defaultBranch main

# 查看配置
git config --list
```

## 二、仓库初始化

```bash
# 方式1：本地初始化
mkdir my-project && cd my-project
git init
git add .
git commit -m "初始提交"

# 方式2：直接创建远程仓库（推荐）
gh repo create my-project --public --source=. --push
```

## 三、文件操作

```bash
# 添加文件到暂存区
git add 文件名          # 添加单个文件
git add .              # 添加所有修改
git add *.py           # 添加所有Python文件

# 提交
git commit -m "提交说明"

# 查看状态
git status             # 简洁模式
git status -s          # 更简洁
```

## 四、查看历史

```bash
# 查看提交日志
git log                # 完整日志
git log --oneline      # 单行模式
git log -5             # 最近5条
git log --graph        # 图形化显示

# 查看文件差异
git diff               # 工作区 vs 暂存区
git diff --staged      # 暂存区 vs 仓库
```

## 五、分支操作

```bash
# 查看分支
git branch             # 本地分支
git branch -a          # 所有分支（含远程）

# 创建/切换分支
git branch 新分支名     # 创建
git checkout 分支名     # 切换
git checkout -b 新分支名  # 创建并切换

# 合并分支
git merge 分支名        # 合并到当前分支

# 删除分支
git branch -d 分支名    # 删除已合并分支
git branch -D 分支名    # 强制删除
```

## 六、远程操作

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin https://github.com/用户/仓库.git

# 推送
git push -u origin main   # 首次推送（设置上游）
git push                   # 后续推送

# 拉取
git pull                   # 拉取并合并
git fetch                  # 仅拉取，不合并
```

## 七、撤销操作

```bash
# 撤销工作区修改
git checkout -- 文件名     # 丢弃修改（危险！）
git restore 文件名         # 新版Git推荐

# 撤销暂存
git reset HEAD 文件名      # 从暂存区移除
git restore --staged 文件名  # 新版Git推荐

# 撤销提交
git reset --soft HEAD~1    # 撤销提交，保留修改
git reset --hard HEAD~1    # 撤销提交，丢弃修改（危险！）
```

## 八、.gitignore 文件

```bash
# 创建 .gitignore
cat > .gitignore << 'EOF'
# Python
*.pyc
__pycache__/
venv/

# IDE
.vscode/
.idea/

# 系统文件
.DS_Store
Thumbs.db

# 敏感信息
.env
*.key
EOF
```

## 九、常用别名设置

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
```

设置后可用：
- `git st` = `git status`
- `git co` = `git checkout`
- `git lg` = 图形化日志

## 十、速记口诀

```
初始化：init → add → commit
日常流：改 → add → commit → push
分支流：branch → checkout → 改 → commit → merge
```

---

*实战验证：每条命令均在 WSL2 + Git 2.x 环境测试通过*