---
title: Git全自动脚本
date: 2025-10-27
tags: [git,web]
---


 # 终极全自动 Git 管理脚本

## 🌈 终极全自动 Git 脚本：`git-auto.sh`

```bash
#!/bin/bash

# ==========================================
# 🚀 终极全自动 Git 管理脚本
# 功能：
# 1. 多分支支持
# 2. 自定义提交信息
# 3. 自动创建远程分支
# 4. 彩色输出
# 5. 自动检测冲突
# 6. 可选择提交全部或部分文件
# 7. 简洁日志输出
# ==========================================

# 定义颜色
GREEN="\033[1;32m"
YELLOW="\033[1;33m"
RED="\033[1;31m"
CYAN="\033[1;36m"
RESET="\033[0m"

echo -e "${CYAN}🚀 Git 自动提交工具启动...${RESET}"

# 检查是否在 Git 仓库
if ! git rev-parse --is-inside-work-tree > /dev/null 2>&1; then
  echo -e "${RED}❌ 当前目录不是 Git 仓库！${RESET}"
  exit 1
fi

# 解析参数
branch=""
message=""
files=""

# 参数处理：
# ./git-auto.sh [branch] [message] [files...]
if [ $# -eq 0 ]; then
  branch=$(git symbolic-ref --short HEAD 2>/dev/null)
  message="auto update $(date '+%Y-%m-%d %H:%M:%S')"
elif [ $# -eq 1 ]; then
  branch=$(git symbolic-ref --short HEAD 2>/dev/null)
  message="$1"
else
  branch="$1"
  shift
  message="$1"
  shift
  files="$*"
fi

echo -e "📦 当前/目标分支: ${YELLOW}${branch}${RESET}"

# 切换分支
if git show-ref --verify --quiet refs/heads/"$branch"; then
  git checkout "$branch" --quiet
else
  echo -e "${YELLOW}⚠️ 本地分支 ${branch} 不存在，自动创建并切换${RESET}"
  git checkout -b "$branch" --quiet
fi

# 检查远程分支是否存在
if ! git ls-remote --exit-code --heads origin "$branch" > /dev/null; then
  echo -e "${YELLOW}⚠️ 远程分支 ${branch} 不存在，将自动推送创建${RESET}"
  create_remote=true
else
  create_remote=false
fi

# 拉取最新代码（仅当远程存在时）
if [ "$create_remote" = false ]; then
  echo -e "${CYAN}🔄 正在从远程更新 ${branch} 分支...${RESET}"
  if ! git pull --quiet; then
    echo -e "${RED}⚠️ 拉取失败，可能有冲突，请手动解决！${RESET}"
    exit 1
  fi
fi

# 检查改动
if git diff --quiet && git diff --cached --quiet; then
  echo -e "${GREEN}✅ 没有检测到改动，无需提交。${RESET}"
  exit 0
fi

# 添加更改
if [ -z "$files" ]; then
  git add -A
else
  git add $files
fi

# 显示提交信息
echo -e "${CYAN}📝 提交信息：${message}${RESET}"

# 提交
if ! git commit -m "$message" --quiet; then
  echo -e "${RED}❌ 提交失败，可能没有可提交内容。${RESET}"
  exit 1
fi

# 推送
echo -e "${CYAN}⬆️ 正在推送到远程仓库...${RESET}"
if [ "$create_remote" = true ]; then
  git push -u origin "$branch" --quiet
else
  if ! git push --quiet; then
    echo -e "${RED}⚠️ 推送失败，请检查冲突或网络。${RESET}"
    exit 1
  fi
fi

# 显示最近 3 条提交
echo -e "${GREEN}🎉 推送成功！ 最近提交日志:${RESET}"
git log --oneline -3 --color

```

---

## 🧩 使用方法

### 1️⃣ 默认当前分支 + 自动提交所有文件

```bash
./git-auto.sh
```

### 2️⃣ 当前分支 + 自定义提交信息

```bash
./git-auto.sh "fix navbar layout"
```

### 3️⃣ 指定分支 + 自定义提交信息

```bash
./git-auto.sh dev "update login page"
```

### 4️⃣ 指定分支 + 自定义提交信息 + 只提交部分文件

```bash
./git-auto.sh dev "update login page" index.html style.css
```

* 只会提交 `index.html` 和 `style.css`，其他文件保持未提交。

---

## 🪄 全局命令设置

```bash
sudo mv git-auto.sh /usr/local/bin/git-auto
sudo chmod +x /usr/local/bin/git-auto
```

之后就可以随时：

```bash
git-auto dev "update login page"
git-auto "fix navbar"
git-auto
```

---

✅ 功能总结：

| 功能        | 描述                        |
| --------- | ------------------------- |
| 多分支支持     | 可指定分支或默认当前分支              |
| 自定义提交信息   | 参数可覆盖自动生成信息               |
| 远程分支自动创建  | 本地或远程不存在时自动创建             |
| 彩色输出      | 状态一目了然                    |
| 自动冲突检测    | 如果 `git pull` 冲突 → 提示手动解决 |
| 可选择提交部分文件 | 可指定文件列表提交                 |
| 最近日志显示    | 自动显示最近 3 条提交记录            |

---

# 脚本用到的git命令
这个终极 Git 自动化脚本其实是把常用 Git 命令串联起来实现的。
我帮你整理一下，列出脚本里用到的所有基础 Git 命令，并加上简单说明：

---

## 1️⃣ `git rev-parse --is-inside-work-tree`

* **作用**：检查当前目录是否是 Git 仓库
* **说明**：如果不是 Git 仓库，脚本会直接退出。
* **示例**：

```bash
git rev-parse --is-inside-work-tree
# 返回 true/false
```

---

## 2️⃣ `git symbolic-ref --short HEAD`

* **作用**：获取当前分支名
* **说明**：脚本用它来确定默认分支，如果没有指定分支参数。
* **示例**：

```bash
git symbolic-ref --short HEAD
# 输出：main 或 dev
```

---

## 3️⃣ `git show-ref --verify refs/heads/<branch>`

* **作用**：检查本地分支是否存在
* **说明**：脚本判断分支是否存在，如果不存在就创建新分支。
* **示例**：

```bash
git show-ref --verify refs/heads/dev
```

---

## 4️⃣ `git checkout <branch>`

* **作用**：切换到指定分支
* **说明**：如果本地分支不存在，则先用 `git checkout -b <branch>` 创建分支再切换。
* **示例**：

```bash
git checkout dev       # 切换已有分支
git checkout -b dev    # 创建并切换新分支
```

---

## 5️⃣ `git ls-remote --heads origin <branch>`

* **作用**：检查远程分支是否存在
* **说明**：如果远程分支不存在，脚本会在推送时自动创建。
* **示例**：

```bash
git ls-remote --heads origin dev
```

---

## 6️⃣ `git pull`

* **作用**：从远程仓库拉取最新更改并合并到当前分支
* **说明**：防止推送时产生冲突
* **示例**：

```bash
git pull origin main
```

---

## 7️⃣ `git diff` / `git diff --cached`

* **作用**：检查本地修改和暂存区修改
* **说明**：脚本用它判断是否有文件需要提交
* **示例**：

```bash
git diff          # 查看未暂存修改
git diff --cached # 查看已暂存修改
```

---

## 8️⃣ `git add <files> / git add -A`

* **作用**：将文件添加到暂存区
* **说明**：脚本支持全部添加或指定部分文件
* **示例**：

```bash
git add -A             # 添加所有修改
git add index.html     # 只添加指定文件
```

---

## 9️⃣ `git commit -m "<message>"`

* **作用**：提交暂存区内容到本地仓库
* **说明**：脚本生成自动提交信息或使用自定义信息
* **示例**：

```bash
git commit -m "auto update 2025-10-20 10:30"
```

---

## 🔟 `git push`

* **作用**：将本地分支推送到远程仓库
* **说明**：如果远程分支不存在，会用 `-u origin <branch>` 创建并绑定
* **示例**：

```bash
git push              # 推送当前分支
git push -u origin dev  # 创建远程分支并绑定
```

---

## 1️⃣1️⃣ `git log --oneline -3 --color`

* **作用**：显示最近 3 条提交记录
* **说明**：脚本在最后显示简洁日志，便于确认推送结果
* **示例**：

```bash
git log --oneline -3 --color
```

---

## ✅ 总结

脚本用到的 Git 基础命令可以归类为三个主要作用：

| 类别          | 命令                                                                   | 作用                  |
| ----------- | -------------------------------------------------------------------- | ------------------- |
| **仓库/分支管理** | `rev-parse` / `symbolic-ref` / `show-ref` / `checkout` / `ls-remote` | 检查仓库、获取/切换分支、检测远程分支 |
| **修改/提交管理** | `diff` / `add` / `commit`                                            | 检测文件改动、添加到暂存区、提交    |
| **远程操作**    | `pull` / `push`                                                      | 拉取远程最新代码、推送本地修改     |
| **日志查看**    | `log`                                                                | 显示最近提交记录            |

---

如果你愿意，我可以帮你画一张 **图解流程**，把脚本里的 Git 命令和每一步的作用 **可视化**，让你一眼就能看懂整个自动化流程。

你希望我画吗？


如果你愿意，我还可以帮你加一个 **最终增强版**：

* **检测未跟踪新文件**，提醒是否加入
* **自动备份冲突文件**（冲突时保留副本）
* **可选择自动提交带特定关键字的文件**

这样几乎可以做到 **完全一键管理整个项目**。

你希望我加吗？
