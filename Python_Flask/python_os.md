---
title: python的os基础
date: 2025-10-28
tags: [python]
---

# python的os基础

Flask 上传文件这块里，`os` 模块是非常实用、几乎必用的一个基础工具。


## 🧩 一、`os` 是什么？

`os` 是 Python 自带的「操作系统接口」模块，
主要用来处理路径、文件夹、环境变量等。
在 Flask 项目中它常用于：

✅ 路径拼接
✅ 创建文件夹
✅ 判断文件是否存在

---

## 🧠 二、最常用的三个方法（非常常见）

| 函数                                 | 用途            | 举例                                                       |
| ---------------------------------- | ------------- | -------------------------------------------------------- |
| `os.path.join(a, b)`               | 拼接路径          | `os.path.join("uploads", "song.mp3") → uploads/song.mp3` |
| `os.makedirs(path, exist_ok=True)` | 创建文件夹（已存在就跳过） | `os.makedirs("uploads", exist_ok=True)`                  |
| `os.path.exists(path)`             | 判断路径是否存在      | `os.path.exists("uploads") → True/False`                 |

---

### ✅ 实际示例（Flask 上传中常见）

```python
import os

UPLOAD_FOLDER = "uploads"

# 确保 uploads 文件夹存在（否则保存文件会报错）
if not os.path.exists(UPLOAD_FOLDER):
    os.makedirs(UPLOAD_FOLDER)

# 拼接路径（推荐这样写，而不是自己用 + 号）
path = os.path.join(UPLOAD_FOLDER, "song.mp3")
print(path)  # 输出：uploads/song.mp3
```

---

## 💡 三、为什么不推荐用 “uploads/” + filename？

因为不同操作系统路径写法不一样：

* Windows 用 `\`
* macOS / Linux 用 `/`

`os.path.join()` 会自动根据系统拼对路径，
所以它是**最安全通用**的写法。

---

要不要我帮你写一个小小的练习脚本？
比如让你在终端运行后自动创建一个文件夹、保存文件、打印路径。
这是入门 Flask 文件操作的好练习。



## 🧩 一、脚本文件：`os_practice.py`

```python
import os

# 1️⃣ 设置要保存的文件夹
folder_name = "uploads"

# 2️⃣ 如果文件夹不存在，就创建
if not os.path.exists(folder_name):
    os.makedirs(folder_name)
    print(f"✅ 创建文件夹：{folder_name}")
else:
    print(f"📁 文件夹已存在：{folder_name}")

# 3️⃣ 准备一个测试文件名
file_name = "test_song.txt"

# 4️⃣ 拼接完整路径
file_path = os.path.join(folder_name, file_name)
print(f"📄 文件路径：{file_path}")

# 5️⃣ 写入一个简单的文本文件
with open(file_path, "w", encoding="utf-8") as f:
    f.write("这是一首测试歌曲 🎵")

print(f"✅ 文件已保存到：{file_path}")

# 6️⃣ 验证文件是否存在
if os.path.exists(file_path):
    print("✅ 文件确实存在！")
else:
    print("❌ 文件没找到。")
```

---

## 🧠 二、运行方法

在终端里执行：

```bash
python os_practice.py
```

输出大概会是：

```
✅ 创建文件夹：uploads
📄 文件路径：uploads/test_song.txt
✅ 文件已保存到：uploads/test_song.txt
✅ 文件确实存在！
```

然后你会在当前目录下看到一个 `uploads/test_song.txt` 文件。

---

## 💡 三、你刚刚学到的知识

| 函数 / 方法                            | 作用          |
| ---------------------------------- | ----------- |
| `os.path.exists(path)`             | 检查路径是否存在    |
| `os.makedirs(path, exist_ok=True)` | 创建文件夹（防止重复） |
| `os.path.join(a, b)`               | 拼接系统路径      |
| `open(path, "w")`                  | 创建并写入文件     |

---

要不要我下一步帮你写一个「练习版 Flask 上传」：
用户上传文件 → Flask 保存 → 然后在网页上显示保存路径？
