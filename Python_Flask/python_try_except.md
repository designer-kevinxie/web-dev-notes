---
title: python try except 语法
date: 2025-10-28
tags: [python]
---


# python try except 语法
`try: ... except: ...` 是 Python 里**错误处理（异常处理）**的核心语法之一，
可以让程序在遇到错误时**不中断运行**，而是**优雅地处理问题**。

我们来系统讲清楚它👇

---

## 🧩 一、基本语法结构

```python
try:
    # 可能出错的代码
except:
    # 出错时执行的代码
```

示例：

```python
try:
    x = 1 / 0
except:
    print("发生错误！")
```

输出：

```
发生错误！
```

没有 `try` 的话，`1/0` 会直接让程序崩溃报错。
有了 `try-except`，程序继续运行。

---

## 🧠 二、异常类型（推荐写法）

最好**不要**直接写裸的 `except:`，而是指定**异常类型**：

```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("不能除以 0！")
```

更精确地控制要捕获哪种错误，避免掩盖别的 bug。

---

### 常见异常类型：

| 异常类型                | 含义                 |
| ------------------- | ------------------ |
| `ZeroDivisionError` | 除以 0               |
| `ValueError`        | 值错误（类型对，但值非法）      |
| `TypeError`         | 类型错误               |
| `FileNotFoundError` | 文件不存在              |
| `KeyError`          | 字典中找不到 key         |
| `IndexError`        | 列表索引越界             |
| `OSError`           | 操作系统相关错误（文件路径、权限等） |

---

## 🧱 三、多个 except 块

可以写多个 `except` 分开处理：

```python
try:
    num = int(input("请输入一个数字: "))
    print(10 / num)
except ValueError:
    print("输入的不是数字！")
except ZeroDivisionError:
    print("不能除以0！")
```

---

## 🎯 四、else 和 finally

### 1️⃣ `else`：当 **try 里没出错** 才执行

```python
try:
    print("执行成功")
except:
    print("出错了")
else:
    print("没有出错，所以执行 else")
```

### 2️⃣ `finally`：**无论是否出错都执行**

常用于“清理操作”，例如关闭文件或断开数据库连接：

```python
try:
    f = open("data.txt")
    # 处理文件
except FileNotFoundError:
    print("文件没找到")
finally:
    f.close()  # ✅ 不管成功或失败，都会执行
```

---

## 🧩 五、捕获错误对象（查看错误信息）

```python
try:
    1 / 0
except Exception as e:
    print("出错类型：", type(e).__name__)
    print("错误详情：", e)
```

输出：

```
出错类型： ZeroDivisionError
错误详情： division by zero
```

---

## 🧩 六、综合示例（Flask 上传场景）

```python
from werkzeug.utils import secure_filename
import os

try:
    filename = secure_filename(upload.filename)
    upload.save(os.path.join("./uploads", filename))
except FileNotFoundError:
    print("❌ 上传目录不存在")
except OSError as e:
    print(f"❌ 文件系统错误: {e}")
except Exception as e:
    print(f"未知错误: {e}")
else:
    print("✅ 上传成功")
finally:
    print("上传任务结束")
```

---

## ✅ 小结表格

| 关键字       | 作用                |
| --------- | ----------------- |
| `try`     | 包裹可能出错的代码         |
| `except`  | 捕获并处理错误           |
| `else`    | 没有出错时执行           |
| `finally` | 无论是否出错都执行（用于清理资源） |
| `as e`    | 获取错误对象，打印或记录详情    |


