# 实战案例集

> 每个案例都是真实操作，可复现

---

## 案例1：推送本地文件到 GitHub

**场景**：把微信收到的课程大作业文档推送到 GitHub 备份

**日期**：2026-06-01

### 操作步骤

```bash
# 1. 找到文件（微信文件路径）
ls -la "/mnt/d/software/xwechat_files/wxid_fmd2e6dobxkw22_bb0e/msg/file/2026-06/202310012730YURM+网络规划和设计大作业PDF.doc"

# 2. 创建项目目录并复制文件
mkdir -p ~/network-planning-assignment
cd ~/network-planning-assignment
cp "/mnt/d/software/xwechat_files/wxid_fmd2e6dobxkw22_bb0e/msg/file/2026-06/202310012730YURM+网络规划和设计大作业PDF.doc" .

# 3. 初始化 Git 并提交
git init
git add .
git commit -m "添加网络规划与设计大作业文档"

# 4. 创建 GitHub 仓库并推送（一步完成）
gh repo create network-planning-assignment \
  --public \
  --description "网络规划与设计大作业 - YURM 广州应用科技学院" \
  --source=. \
  --remote=origin \
  --push
```

### 结果

```
仓库地址：https://github.com/RM3836/network-planning-assignment
文件名：202310012730YURM+网络规划和设计大作业PDF.doc
文件大小：约20MB
页数：62页
创建工具：WPS Office
```

### 关键点

1. **微信文件路径**：`D:\software\xwechat_files\` 对应 WSL 路径 `/mnt/d/software/xwechat_files/`
2. **gh repo create**：一行命令搞定创建仓库 + 推送
3. **中文文件名**：Git 会自动处理，无需担心

### 踩坑记录

| 问题 | 原因 | 解决 |
|------|------|------|
| 文件名显示八进制 | Git默认转义中文 | `git config --global core.quotepath false` |
| 推送超时 | 文件太大(20MB) | GitHub支持100MB，正常推送 |

---

## 案例2：创建课程知识库

**场景**：把多门课程的复习资料整理成知识库推送到 GitHub

**日期**：2026-05-24

### 操作步骤

```bash
# 1. 创建本地知识库目录
mkdir -p ~/course-knowledge-base
cd ~/course-knowledge-base

# 2. 按课程创建子目录
mkdir -p 01-计网路由交换
mkdir -p 02-网络安全实验
mkdir -p 03-ENSP网络规划
mkdir -p 04-AI机器学习
mkdir -p 05-编程项目
mkdir -p 06-思政与其他

# 3. 创建 README.md
cat > README.md << 'EOF'
# 课程知识库

> 广州应用科技学院 · 网络工程 · 大二下学期

## 目录
- 01-计网路由交换
- 02-网络安全实验
- 03-ENSP网络规划
- 04-AI机器学习
- 05-编程项目
- 06-思政与其他
EOF

# 4. 添加 .gitignore
cat > .gitignore << 'EOF'
*.tmp
*.bak
.DS_Store
Thumbs.db
EOF

# 5. 初始化并推送
git init
git add .
git commit -m "初始化课程知识库"
gh repo create course-knowledge-base --public \
  --description "📚 广州应用科技学院·网络工程·大二下学期课程知识库" \
  --source=. --push
```

### 结果

```
仓库地址：https://github.com/RM3836/course-knowledge-base
状态：public
```

---

## 案例3：批量创建课程仓库

**场景**：一次性创建多门课程的 GitHub 仓库

**日期**：2026-05-24

### 操作步骤

```bash
# 定义仓库列表
repos=(
  "routing-switching-notes|📡 路由与交换技术 WLAN 期末复习知识库"
  "wireless-network-notes|📡 无线网络技术期末复习资料库"
  "auto-ops-course|🤖 自动化运维技术课程代码"
)

# 循环创建
for item in "${repos[@]}"; do
  IFS='|' read -r name desc <<< "$item"
  mkdir -p ~/$name
  cd ~/$name
  git init
  echo "# $name" > README.md
  git add .
  git commit -m "初始化仓库"
  gh repo create "$name" --public --description "$desc" --source=. --push
done
```

### 结果

| 仓库名 | 描述 |
|--------|------|
| routing-switching-notes | 路由与交换技术 |
| wireless-network-notes | 无线网络技术 |
| auto-ops-course | 自动化运维技术 |

---

## 案例4：Fork 并克隆开源项目

**场景**：参与开源项目

### 操作步骤

```bash
# 1. Fork 仓库
gh repo fork original-owner/repo-name

# 2. 克隆自己的 fork
gh repo clone RM3836/repo-name
cd repo-name

# 3. 添加上游仓库
git remote add upstream https://github.com/original-owner/repo-name.git

# 4. 同步上游更新
git fetch upstream
git merge upstream/main
```

---

## 案例5：使用 Git LFS 管理大文件

**场景**：仓库中有超过 100MB 的文件

### 操作步骤

```bash
# 1. 安装 Git LFS
git lfs install

# 2. 跟踪大文件类型
git lfs track "*.zip"
git lfs track "*.psd"
git lfs track "*.mp4"

# 3. 提交 .gitattributes
git add .gitattributes
git commit -m "配置 Git LFS"

# 4. 正常提交大文件
git add large-file.zip
git commit -m "添加大文件"
git push
```

---

## 案例6：修复提交信息

**场景**：提交信息写错了，想修改

### 操作步骤

```bash
# 修改最后一次提交信息
git commit --amend -m "新的提交信息"

# 强制推送（如果已经推送到远程）
git push --force
```

**注意**：`--force` 会覆盖远程历史，仅限个人项目使用！

---

## 案例7：撤销误操作

**场景**：误删了文件，想恢复

### 操作步骤

```bash
# 查看最近提交
git log --oneline -5

# 恢复到指定提交
git checkout abc1234 -- 文件名

# 或者恢复整个仓库到指定版本
git reset --hard abc1234
```

---

## 案例8：同步 Fork 的上游仓库

**场景**：Fork 的项目有更新，想同步

### 操作步骤

```bash
# 方式1：gh CLI
gh repo sync RM3836/repo-name -b main

# 方式2：手动同步
git fetch upstream
git checkout main
git merge upstream/main
git push
```

---

*持续更新中... 每次实战后补充新案例*