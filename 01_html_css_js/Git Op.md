#  Git 常用命令速查表

## git 安装
https://brew.sh/ 

`brew install git`

## 🧱 基础配置
```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
git config --list          # 查看配置
```
## ✅ 常用组合
```bash
git add . && git commit -m "update" && git push
```
## 📂 初始化与克隆
```bash
git init              # 初始化一个新的本地仓库
git clone <仓库地址>        # 克隆远程仓库
git clone <地址> <目录名>    # 克隆到指定目录
```

## 💾 查看状态与历史
```bash 
git status                 # 查看当前文件状态
git log                    # 查看提交历史
git log --oneline --graph  # 简洁图形化显示提交记录
git diff                   # 查看修改内容
```

## ✍️ 添加与提交
```bash
git add <文件>             # 添加单个文件
git add .                  # 添加所有修改的文件
git commit -m "提交信息"     # 提交
git commit -am "提交信息"    # 添加并提交（仅限已跟踪文件）
```

## 🔄 分支操作
```bash
git branch                 # 查看分支
git branch <分支名>         # 创建新分支
git checkout <分支名>       # 切换分支
git checkout -b <分支名>    # 创建并切换分支
git merge <分支名>          # 合并分支
git branch -d <分支名>      # 删除分支
```
### 为什么需要分支

在项目开发中，经常会遇到这些情况：

- 想修复一个 bug，但又不想影响正在运行的主分支（main 或 master）。
- 想开发新功能，可能代码不稳定。
- 多人协作，每个人在不同任务上工作，互不干扰。
- 如果没有分支，你只能直接在主分支上修改，容易出错或冲突。分支就像 “平行世界”，可以独立开发，随时合并。

### 💡 小技巧：开发新功能时，通常流程是：
```bash
git checkout -b feature/新功能
# 开发完成后
git add .
git commit -m "完成新功能"
git checkout main
git merge feature/新功能
```

这样 主分支始终稳定，新功能在独立分支上完成。

## 远程仓库
```bash
git remote -v              # 查看远程仓库
git remote add origin <地址> # 添加远程仓库
git remote remove origin   # 删除远程仓库
git push -u origin main    # 第一次推送
git push                   # 推送更新
git pull                   # 拉取更新
git fetch                  # 获取远程更新（不合并）
```

### 作用：

- 给已有本地仓库 绑定一个远程仓库

- 可以给远程仓库起一个名字（通常是 `origin`）

命令示例：
```
git remote add origin https://github.com/username/project.git
```


### 效果：

- 本地仓库可以通过 `origin` 与远程仓库交互

- 可以 `git push` 或 `git pull`

- 不会自动下载远程内容，需要手动 `git fetch` 或 `git pull`

### 场景：

- 你本地先建好了仓库 (`git init`)

- 想把它和远程仓库关联

### clone 对比表
| 命令                            | 场景      | 做了什么          | 远程关联              |
| ----------------------------- | ------- | ------------- | ----------------- |
| `git clone <url>`             | 第一次获取项目 | 克隆整个仓库，包含提交历史 | 自动添加 `origin`     |
| `git remote add <name> <url>` | 本地已有仓库  | 只添加远程仓库地址     | 手动添加，需要 push/pull |


## 多人协作流程
### 1️⃣ 克隆远程仓库到本地

第一次参与项目，需要把远程仓库复制到本地。

```bash 
git clone <仓库地址>
```


例如：

```bash
git clone https://github.com/username/project.git
```

- 这一步会创建一个本地仓库，并自动把远程仓库 origin 设置好。

- 默认会克隆主分支（通常是 main 或 master）。

注意事项：

- 如果仓库很大，可以加 --depth 1 只克隆最新提交。

- 默认 origin 是远程仓库名字，你可以改成别的（如 git remote rename origin upstream）。

### 2️⃣ 创建功能分支

为了避免直接修改主分支，创建一个功能分支（feature branch）：

```bash
git checkout -b feature/新功能
```

`-b` 表示 创建并切换 分支。

命名建议：

`feature/xxx` 新功能

`bugfix/xxx` 修复 bug

`hotfix/xxx` 紧急修复

为什么要分支？

- 主分支保持稳定。

- 分支独立开发，不影响别人工作。

- 便于合并和回滚。

### 3️⃣ 本地开发并提交

在功能分支上修改代码后：

```bash
git add .
git commit -m "完成新功能 A"
```

`git add .`：把修改的文件加入暂存区。

`git commit -m "说明"`：生成本地提交。

Tips：

- 提交信息尽量清晰，如 `fix login bug` 或 `add search feature`。

- 可以多次提交，最后合并到远程主分支时更容易追踪。

### 4️⃣ 推送分支到远程

开发完成后，将功能分支推送到远程仓库：

```bash
git push -u origin feature/新功能
```

- `-u` 设置上游（tracking）分支，以后直接 `git push` 就行。

- 远程会生成一个对应的分支 `feature/新功能`。

Tips：

- 每个人的分支最好用自己的功能分支，不直接 `push` 到主分支。

- 方便团队代码审查。

### 5️⃣ 发起 Pull Request / Merge Request

- 在 GitHub/GitLab 上选择 Compare & Pull Request。

- 填写功能说明，选择主分支作为目标分支（`main`）。

- 提交请求，团队其他成员可以审核代码、提出修改建议。

- 审核通过后，由负责人或自己合并到主分支。

作用：

- 确保主分支始终稳定。

- 代码变更可被团队讨论。

- 审核流程可以减少错误。

### 6️⃣ 拉取最新主分支更新

在开发新功能前或合并后，需要同步远程主分支：
```bash
git checkout main
git pull origin main
```

- `checkout main`：切换到主分支。

- `pull`：拉取远程更新并合并到本地。

Tips：

- 避免在旧版本上开发新功能，容易冲突。

- 可以在功能分支上用：

```bash 
git checkout feature/新功能
git merge main
```

将最新主分支代码合并到功能分支，解决冲突再 `push`。

### 7️⃣ 删除功能分支（可选）

功能合并到主分支后，本地和远程的功能分支可以删除：

```bash
git branch -d feature/新功能      # 删除本地分支
git push origin --delete feature/新功能  # 删除远程分支
```

作用：

- 保持分支整洁。

- 避免混乱。