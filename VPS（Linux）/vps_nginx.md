---
title: VPS配置Nginx
date: 2025-10-28
tags: [vps,linux,nginx]
---

# VPS配置Nginx

### Nginx默认页面及反向代理
#### 默认页面
Nginx 默认把网页文件存放在 ```/var/www/html```(绝对路径，现在在root文件夹)。我们先进入这个文件夹：

```Bash

cd /var/www/html
```
然后看看里面有什么（输入 ls）：
```Bash

ls
```
你应该会看到一个名字很长的文件，比如 ```index.nginx-debian.html```。这就是你刚才看到的那个默认页面。

#### 第二步：创建一个新的“首页”
我们不需要删除旧文件，只需要创建一个名字叫 ```index.html``` 的新文件。 因为 Nginx 的默认规则是：只要有 ```index.html```，就优先展示它。

我们使用 Linux 最简单的文本编辑器 nano 来创建并编辑这个文件。

输入以下命令（注意前面要加 sudo，因为这个文件夹属于系统，普通用户没权限写）：

```Bash
sudo nano index.html
```
#### 第三步：写入你的 HTML 代码
现在你应该进入了一个黑底白字的编辑界面。把下面的代码复制进去（或者随便写点什么英文）：

```HTML
<!DOCTYPE html>
<html>
<head>
    <title>My VPS</title>
    <style>
        body {
            background-color: #f0f0f0;
            font-family: sans-serif;
            text-align: center;
            padding-top: 50px;
        }
        h1 { color: #333; }
    </style>
</head>
<body>
    <h1>Hello World!</h1>
    <p>This is my first customized page.</p>
    <p>Nginx is running successfully!</p>
</body>
</html>
```
#### 第四步：保存并退出（新手最容易卡住的地方！）
nano 编辑器的操作和 Windows 记事本不一样，全是快捷键操作：

保存文件：按键盘上的 ```Ctrl + O ```(字母O)，然后按 回车 (Enter) 确认文件名。

退出编辑器：按 ```Ctrl + X```。

现在，不需要重启 Nginx，直接去你的浏览器，刷新刚才那个页面。

### Nginx 最强大的功能——反向代理 (Reverse Proxy)。

我们需要写一张“指引条”，告诉 Nginx：如果有客人找 kevinx.cc，就把他转到 127.0.0.1:5000（Python）。

我们采用最佳实践的方式来配置，不要直接修改原来的默认文件，而是新建一个专属配置文件。

#### 第一步：清理旧的“默认配置”
为了防止冲突（因为默认配置也在占用 80 端口），我们需要先把它“关掉”（其实就是删掉它的软链接，原文件还在）。

在终端输入：

```Bash
sudo rm /etc/nginx/sites-enabled/default
```
#### 第二步：创建你的专属配置文件
我们需要在 ```/etc/nginx/sites-available/``` 下创建一个新文件。假设你的项目叫 myapp。

输入：

```Bash
sudo nano /etc/nginx/sites-available/myapp
```
#### 第三步：写入配置代码 (核心步骤)
把下面的代码复制进去。这是最标准、最简洁的反向代理配置：

```Nginx

server {
    # 1. 监听 80 端口 (HTTP)
    listen 80;
    
    # 2. 服务器名字 (域名或 IP)
    # 如果你有域名就填域名，没有就填你的 VPS IP 地址 (比如 123.45.67.89)
    # 如果暂时不想管，填下划线 _ 代表“任何访问者”
    server_name kevinx.cc www.kevinx.cc;

    # 3. 核心转发规则
    location / {
        # 把请求转发给本机的 8000 端口
        proxy_pass http://127.0.0.1:8000;

        # 下面这几行是“标准头部信息”
        # 作用：把顾客的真实 IP 告诉 Python，否则 Python 以为所有请求都来自 Nginx (127.0.0.1)
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```
(按 ```Ctrl+O``` 回车保存，```Ctrl+X``` 退出)

#### 第四步：激活这个配置
Linux 的 Nginx 有个很聪明的设计：

```sites-available```: 存放所有写好的配置（仓库）。

```sites-enabled```: 存放正在生效的配置（货架）。

你需要把刚才写的文件“链接”到生效目录去：

```Bash

sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
```

#### 第五步：检查并重启
在重启之前，养成好习惯，先检查有没有写错字：

```Bash
sudo nginx -t
```
如果看到 ```syntax is ok``` 和 ```test is successful```，说明没问题。

如果报错，它会告诉你是第几行写错了。

#### 最后，重启 Nginx 加载新配置：

```Bash
sudo systemctl restart nginx
```

### 再次运行 Certbot SSL 配置

我们要让 Certbot 重新扫描一次，把 SSL 配置“注入”进去。

输入：

```Bash
sudo certbot --nginx
```
接下来会出现的情况：

它会检测到你在配置文件里写的域名，问你是不是要给这几个域名配置 HTTPS。输入对应的数字（例如 1 或 1,2），回车。

关键点： 因为你之前申请过证书，它可能会提示你：

```You have an existing certificate that has exactly the same domains... (1) Attempt to reinstall this existing certificate （尝试重新安装现有证书） (2) Renew & replace the cert （重新申请并替换）```

请选择 1 (Reinstall)。因为证书还在硬盘里，我们要做的只是把配置找回来，不需要重新向官方申请。

接着它可能会问你是否要开启 Redirect (强制跳转)：

```(1) No redirect (2) Redirect```

建议选择 2。这样以后用户访问 ```http://``` 会自动跳到 ```https://```，更安全。

第三步：大功告成
Certbot 跑完后，它会自动修改你的 Nginx 配置并重启服务。