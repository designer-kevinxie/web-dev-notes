---
title: 拿到一台新VPS该做的事
date: 2025-10-28
tags: [vps,linux]
---

# 拿到一台新VPS该做的事

### 通过 SSH 远程连接
打开你电脑上的终端（Terminal），输入以下命令（记得把 <你的IP地址> 换成你刚拿到的那一串数字）：

``` Bash
ssh root@<你的IP地址>
```

### 验证成功 & 第一次“大扫除”
如果你看到了一堆欢迎信息（比如 Welcome to Ubuntu 24.04），恭喜你，你已经进去了！🎉

既然进来了，我们先执行一个“标准动作”，把系统里的软件都更新到最新状态，确保安全和稳定。复制粘贴下面这行命令（apt：Advanced Package Tool 管理软件）并回车：


```Bash
apt update && apt upgrade -y
```

### 可能需要重启一次
重启服务器
请在终端里输入这条命令：

```Bash
reboot
```

### 安装并启动 Nginx
我们要请出一个新角色：Nginx: 把它想象成你大楼的“金牌前台”。

以前：客人必须知道你的房间号 :5000 才能找到你。

以后：客人只要访问 kevinx.cc，前台 Nginx 会自动把他们带到 5000 房间，并且给他们发一张安全通行证（HTTPS 证书）。


第一步：安装这位“金牌前台” (Nginx) 🎩
在你的 VS Code 终端里（确保连着服务器），运行这两条命令：

```Bash
apt install nginx -y
```

启动它(systemctl：系统控制)
```bash
systemctl start nginx
```
如果你现在直接在浏览器访问 http://kevinx.cc (不带端口)，你应该会看到一个 "Welcome to nginx!" 的默认页面。这说明前台已经上班了！

#### Nginx开机自启 (非常重要)
```Bash
systemctl enable nginx
```
解释： 设置 Nginx 为“开机自动启动”。

为什么要用： 否则万一你的 VPS 重启了，网页服务就不会自动恢复，必须手动再去敲一遍 start。

#### 检查状态 (排错必备)
```Bash
systemctl status nginx
```
解释： 查看 Nginx 现在到底是“死”是“活”。

为什么要用： 如果启动失败，这里会显示绿色的 active (running) 或者红色的报错信息。

#### 重启服务 (修改配置后用)
```Bash

systemctl restart nginx
```

解释： 关闭再启动。

为什么要用： 每次你修改了 Nginx 的配置文件（比如配置反向代理到你的 Python 程序），必须执行这个命令，修改才会生效。

### 颁发“安全证书” (HTTPS) 🔒
我们用 Certbot 这个工具来免费申请证书，它会自动帮你改好剩下的配置。

#### 安装 Certbot：

```Bash
apt install certbot python3-certbot-nginx -y
```
#### 一键申请证书：

```Bash
certbot --nginx -d kevinx.cc -d www.kevinx.cc
```
跟着提示走：

```Enter email address```: 输入你的邮箱（用来接收证书过期提醒）。

```Terms of Service```: 输入 Y 同意。

```Share email```: 输入 N (不想收广告)。

关键一步： 它可能会问你是否要 Redirect (重定向)。

一定要选 2 (Redirect)。这就意味着如果有人访问 ```http```，会自动变成 ```https```。