### Nginx默认页面及更换
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

### 告诉前台怎么带路 (配置 Nginx) 📝
我们需要写一张“指引条”，告诉 Nginx：如果有客人找 kevinx.cc，就把他转到 127.0.0.1:5000。

创建配置文件：

```Bash
nano /etc/nginx/sites-available/kevinx.cc
```
粘贴下面的内容： (请直接复制粘贴，除了 server_name 不用改别的)

```Nginx

server {
    listen 80;
    server_name kevinx.cc www.kevinx.cc;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```
保存并退出： ```Ctrl + O``` -> 回车 -> ```Ctrl + X```

激活这个配置： (运行这行命令建立一个软链接)

```Bash

ln -s /etc/nginx/sites-available/kevinx.cc /etc/nginx/sites-enabled/
```
检查配置有没有写错：

```Bash

nginx -t
```
(如果看到 successful 字样，就说明没问题)

重启 Nginx 让配置生效：

```Bash
systemctl restart nginx
```


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

