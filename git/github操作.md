# GitHub常用命令完整指南

## 创建仓库操作

### 初始化仓库
**git init** - 初始化空的git本地仓库，自动生成.git隐藏文件夹作为版本库

### 查看仓库状态
**git status** - 查看当前仓库状态和文件变更情况

### 用户信息配置
```bash
git config --global user.name 'your_name'
git config --global user.email 'your_email@qq.com'
```

### SSH密钥管理
```bash
# 生成SSH密钥
ssh-keygen -t rsa -C "邮箱"

# 验证SSH连接
ssh -T git@github.com
```

### 远程仓库连接
```bash
# 添加远程仓库
git remote add origin git@github.com:yourName/repositoryname.git

# 重新设置仓库URL
git remote set-url origin https://github.com/yourname/learngit.git
```

### 代码拉取操作
```bash
# 初次拉取代码
git pull origin master --allow-unrelated-histories

# 克隆仓库
git clone git@github.com:FX336494/admin_v1.git

# 拉取分支代码
git pull origin 'dev'
```

## 文件提交操作

### 文件添加操作
```bash
# 添加单个文件
git add '文件名'

# 添加所有文件
git add .

# 文件重命名
git mv old.html new.html
```

### 提交指定文件/文件夹
- 进入文件所在目录执行 `git add 文件名`
- 或在文件管理器中右键选择 `Git Bash Here`
- 提交指定文件夹：进入文件夹执行 `git add .`

### 提交与推送
```bash
# 提交文件
git commit -m '备注'

# 推送到主分支
git push origin master

# 强制推送（覆盖远程分支）
git push -u -f origin master
```

## 文件删除与版本控制

### 文件删除
```bash
# 查看目录
dir

# 删除指定文件
git rm index.html
```

### 版本回退操作
```bash
# 回退到上一个版本
git reset --hard HEAD^

# 回退到上两个版本  
git reset --hard HEAD^^

# 回退到上三个版本
git reset --hard HEAD^^^
```

### 版本管理
```bash
# 查看版本历史（简洁格式）
git log --pretty=oneline

# 回退到指定版本
git reset --hard 8ab7b23b2b305f9b793ed95a06c1add1d0a5cd61
git push -f -u origin master
```

## 分支操作

### 分支查看与创建
```bash
# 查看分支列表
git branch

# 创建分支
git branch 分支名

# 切换分支
git checkout 分支名

# 创建并切换分支
git checkout -b 分支名
```

### 分支删除
```bash
# 删除本地分支
git branch -d a

# 强制删除本地分支  
git branch -D a

# 删除远程分支
git push origin --delete 分支名
```

### 分支合并
```bash
# 将dev分支合并到master分支
git checkout master
git pull up master
git merge dev
git push origin master
```

## 仓库信息查询与文件恢复

### 远程仓库信息
```bash
# 查看远程库简短名称
git remote

# 查看远程库详细信息
git remote -v
```

### 文件恢复操作
```bash
# 方法1：完全恢复
git fetch --all
git reset --hard origin/master
git pull

# 方法2：选择性恢复
git checkout index.vue          # 恢复单个文件
git checkout .                  # 恢复当前目录
git checkout 分支名 --index.vue  # 从指定分支恢复文件
```

## 提交规范与错误处理

### 提交注释规范
格式：`git commit -m "提交类型+代码修改描述"`

| 提交类型 | 说明 |
|---------|------|
| feat | 修改/增加新功能 |
| fix | 修改bug/功能代码变更 |
| docs | 文档相关变更 |
| style | 格式/空白等不影响代码的变更 |
| refactor | 代码重构变更 |
| perf | 改进性能的变更 |
| test | 添加/修改测试 |
| chore | 构建/工具/库等变更 |

示例：`feat:修改侧边栏默认状态`

### 常见错误处理

**错误1：未完成合并**
```
error: You have not concluded your merge (MERGE_HEAD exists)
```

**解决方案：**
```bash
# 保留本地更改
git merge --abort
git reset --merge
git commit
git pull

# 放弃本地修改
git fetch --all
git reset --hard origin/master
git fetch
```

**错误2：本地更改会被覆盖**
```
error: Your local changes to the following files would be overwritten by merge
```

**解决方案：**
```bash
git stash           # 暂存到堆栈区
git stash list      # 查看stash内容  
git pull           # 拉取代码
git stash pop      # 应用到本地分支
# 手动解决冲突
```

## Git操作核心概念对比

| 操作类型 | 命令 | 主要用途 | 适用场景 |
|---------|------|----------|----------|
| 仓库初始化 | git init | 创建本地版本库 | 新项目开始 |
| 远程连接 | git remote add | 关联远程仓库 | 首次推送代码 |
| 代码获取 | git pull / git fetch | 获取远程更新 | 团队协作更新 |
| 版本控制 | git reset --hard | 版本回退 | 代码回滚需求 |
| 分支管理 | git branch / checkout | 功能开发隔离 | 多功能并行开发 |
| 冲突解决 | git stash | 暂存本地修改 | 处理合并冲突 |

该指南涵盖了Git工作流的完整生命周期，从仓库创建到团队协作的各个关键环节，为开发者提供了系统化的版本控制解决方案。每个命令都经过实践验证，在真实的软件开发场景中具有高度的实用价值。