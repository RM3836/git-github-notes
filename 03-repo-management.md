# 仓库管理最佳实践

## 一、目录结构规范

### 项目仓库标准结构

```
project-name/
├── README.md          # 项目说明（必须）
├── .gitignore         # 忽略规则（必须）
├── LICENSE            # 开源协议
├── docs/              # 文档
├── src/               # 源代码
├── tests/             # 测试
├── scripts/           # 脚本
└── config/            # 配置
```

### 知识库仓库结构

```
knowledge-base/
├── README.md          # 总览 + 目录
├── cheatsheet.md      # 速查表
├── 01-topic-xxx.md    # 按主题分文件
├── 02-topic-yyy.md
├── 03-practice.md     # 实战案例
└── scripts/           # 配套脚本
```

## 二、README.md 编写规范

### 模板

```markdown
# 项目名称

> 一句话描述

## 功能特性
- 特性1
- 特性2

## 快速开始
\`\`\`bash
# 安装
pip install xxx

# 使用
python main.py
\`\`\`

## 目录结构
\`\`\`
├── xxx/
└── yyy/
\`\`\`

## 更新日志
- 2026-06-01: 初始版本

## 作者
YURM | 广州应用科技学院
```

## 三、.gitignore 常用规则

### Python 项目

```gitignore
# 字节码
*.pyc
__pycache__/

# 虚拟环境
venv/
.venv/
env/

# 包
*.egg-info/
dist/
build/

# IDE
.vscode/
.idea/
*.swp

# 环境变量
.env

# 日志
*.log

# 数据库
*.db
*.sqlite3
```

### 通用

```gitignore
# 系统文件
.DS_Store
Thumbs.db
desktop.ini

# 临时文件
*.tmp
*.bak
*.cache
```

## 四、分支管理策略

### 简单项目（个人）

```
main        ← 主分支，稳定版本
└── dev     ← 开发分支（可选）
```

### 团队项目

```
main        ← 生产环境
├── develop ← 开发环境
├── feature/xxx  ← 功能分支
├── bugfix/xxx   ← 修复分支
└── release/v1.0 ← 发布分支
```

### 命名规范

```bash
# 功能分支
feature/user-login
feature/add-search

# 修复分支
bugfix/fix-login-error

# 发布分支
release/v1.0.0
```

## 五、提交信息规范

### 格式

```
<类型>(<范围>): <描述>

<正文>

<脚注>
```

### 类型

| 类型 | 说明 | 示例 |
|------|------|------|
| feat | 新功能 | feat(user): 添加登录功能 |
| fix | 修复 | fix(auth): 修复token过期问题 |
| docs | 文档 | docs: 更新README |
| style | 格式 | style: 调整缩进 |
| refactor | 重构 | refactor: 重构登录模块 |
| test | 测试 | test: 添加单元测试 |
| chore | 杂项 | chore: 更新依赖 |

### 简化版（个人项目）

```bash
# 直接用中文描述
git commit -m "添加用户登录功能"
git commit -m "修复密码验证bug"
git commit -m "更新文档"
```

## 六、Tag 管理

```bash
# 创建标签
git tag v1.0.0

# 创建带注释的标签
git tag -a v1.0.0 -m "第一个正式版本"

# 推送标签
git push origin v1.0.0

# 推送所有标签
git push --tags

# 查看标签
git tag

# 删除标签
git tag -d v1.0.0
```

## 七、仓库权限管理

### 协作者管理（gh CLI）

```bash
# 添加协作者
gh api repos/OWNER/REPO/collaborators/USERNAME -X PUT

# 查看协作者
gh api repos/OWNER/REPO/collaborators
```

### 保护分支

```bash
# 通过网页设置：Settings → Branches → Add rule
# - 要求PR审查
# - 要求状态检查通过
# - 禁止强制推送
```

## 八、仓库备份

```bash
# 克隆所有仓库
gh repo list --limit 100 --json name -q '.[].name' | while read repo; do
  gh repo clone "$repo"
done

# 导出仓库列表
gh repo list --json name,url,description > repos.json
```

## 九、大文件处理

### Git LFS

```bash
# 安装
git lfs install

# 跟踪大文件类型
git lfs track "*.psd"
git lfs track "*.zip"

# 查看跟踪列表
git lfs ls-files

# 推送
git add .gitattributes
git commit -m "添加 LFS 跟踪"
git push
```

### 文件大小限制

| 平台 | 单文件限制 | 仓库限制 |
|------|-----------|---------|
| GitHub | 100MB | 1GB（推荐）|
| GitLab | 100MB | 5GB |
| Gitee | 100MB | 5GB |

## 十、常用工作流

### 日常开发流

```bash
# 1. 拉取最新
git pull

# 2. 修改文件
vim xxx.py

# 3. 查看状态
git status

# 4. 添加并提交
git add .
git commit -m "描述修改"

# 5. 推送
git push
```

### 新功能开发流

```bash
# 1. 创建功能分支
git checkout -b feature/new-feature

# 2. 开发并提交
git add .
git commit -m "feat: 新功能"

# 3. 推送分支
git push -u origin feature/new-feature

# 4. 创建 PR
gh pr create

# 5. 合并后删除分支
git checkout main
git pull
git branch -d feature/new-feature
```

---

*适用：个人项目、课程作业、小型团队*