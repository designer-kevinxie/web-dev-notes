---
title: python使用app.config
date: 2025-10-28
tags: [python]
---


# python使用app.config
使用app.config“**以后要换路径，只改一处就行**”。


## 🎯 先看一个没用 `app.config` 的写法（不好维护）

```python
from flask import Flask, request
from werkzeug.utils import secure_filename
import os

app = Flask(__name__)

@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['file']
    filename = secure_filename(file.filename)
    save_path = os.path.join('./uploads', filename)  # ❌ 直接写死路径
    file.save(save_path)
    return f"文件已保存到 {save_path}"
```

如果你哪天想换路径，比如改成：

```bash
./static/user_files
```

你就得去**每一个 `./uploads` 的地方改成 `./static/user_files`**。
项目一大，几十处要改，非常麻烦。

---

## ✅ 用 `app.config` 管理路径（推荐）

```python
from flask import Flask, request
from werkzeug.utils import secure_filename
import os

app = Flask(__name__)

# 只在这里定义一次上传目录 👇
UPLOAD_FOLDER = './uploads'
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER

# 如果文件夹不存在，就自动创建
os.makedirs(app.config['UPLOAD_FOLDER'], exist_ok=True)

@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['file']
    filename = secure_filename(file.filename)
    save_path = os.path.join(app.config['UPLOAD_FOLDER'], filename)
    file.save(save_path)
    return f"文件已保存到 {save_path}"
```

---

### 🪄 改路径的方式就变得超简单：

假设项目上线后，你要把上传路径换成：

```bash
/var/www/project/uploads
```

你只需要改**这一行**：

```python
UPLOAD_FOLDER = '/var/www/project/uploads'
```

其他地方完全不用动。
所有用到 `app.config['UPLOAD_FOLDER']` 的地方，都会自动用新的路径。

---

### ✅ 优点总结

| 优点   | 说明              |
| ---- | --------------- |
| 集中管理 | 只改一处，全局生效       |
| 可扩展  | 其他文件、模块都能访问这个配置 |
| 安全   | 避免路径拼错或重复定义     |
| 清晰   | 一看代码就知道项目上传目录在哪 |

