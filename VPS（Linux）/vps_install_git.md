---
title: VPS安装Git
date: 2025-10-28
tags: [vps,linux,git]
---

# VPS安装Git
在 **VPS 上安装 Git** 很简单，下面根据你常见的服务器系统给出最直接的指令。


## ✅ 1. 查看你的 VPS 是哪种系统

一般是：

* **Ubuntu / Debian**
* **CentOS / Rocky / AlmaLinux**

你可以先执行：

```bash
cat /etc/os-release
```

看 `ID=` 和 `VERSION_ID=` 就知道了。

---

# ✅ 2. Ubuntu / Debian 安装 Git

```bash
sudo apt update
sudo apt install -y git
```

查看版本：

```bash
git --version
```

---

# ✅ 3. CentOS / Rocky / AlmaLinux 安装 Git

### 方法 A：直接用系统默认 Git（简单）

```bash
sudo yum install -y git
```

### 方法 B：安装较新版本的 Git（推荐）

系统自带版本很旧，可以用源安装新版本：

```bash
sudo yum remove -y git
sudo yum install -y https://repo.ius.io/ius-release-el7.rpm
sudo yum install -y git236
```

---

# ✅ 4. 配置 Git（首次使用必做）

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

查看配置：

```bash
git config --list
```

---

# ❗ 5. 如需使用 GitHub，需要配置 SSH Key（否则会 Permission denied）

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱"
```

一路回车后，查看公钥：

```bash
cat ~/.ssh/id_ed25519.pub
```

复制粘贴到 GitHub → Settings → SSH and GPG keys → New SSH key。

测试是否成功：

```bash
ssh -T git@github.com
```

看到类似 “Hi xxx!” 就成功了。


