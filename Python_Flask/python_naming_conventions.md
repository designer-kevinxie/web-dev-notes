---
title: python命名规范
date: 2025-10-28
tags: [python]
---

# python命名规范

在 Flask（以及大部分 Python 项目）里，
`UPLOAD_FOLDER` 这种 **全大写变量名** 是一种**约定俗成的写法**，
表示它是一个 **配置常量（configuration constant）**。

---

## 🧩 一、简单来说：

| 写法              | 含义                 |
| --------------- | ------------------ |
| `UPLOAD_FOLDER` | ✅ 常量（不会在程序运行中被修改）  |
| `upload_folder` | ⚙️ 普通变量（可能在运行中被改变） |

---

## 🧠 二、在 Flask 中为什么用全大写

Flask（底层是基于 Werkzeug）有一个配置系统：

```python
app.config["UPLOAD_FOLDER"] = "uploads"
```

在 Flask 里，**所有配置项都是全大写的**，比如：

| 配置项名                 | 含义             |
| -------------------- | -------------- |
| `DEBUG`              | 是否开启调试模式       |
| `SECRET_KEY`         | 加密 session 的密钥 |
| `UPLOAD_FOLDER`      | 上传文件保存目录       |
| `MAX_CONTENT_LENGTH` | 限制上传文件大小       |

👉 这是 Flask 官方推荐的写法（来源：[Flask 官方文档 Config 部分](https://flask.palletsprojects.com/en/latest/config/)）

---

## 🧩 三、Python 的命名习惯（PEP 8 规范）

Python 官方的风格指南 **PEP 8** 建议：

| 命名方式                         | 用于           |
| ---------------------------- | ------------ |
| `lowercase_with_underscores` | 变量、函数名       |
| `CamelCase`                  | 类名           |
| `ALL_CAPS_WITH_UNDERSCORES`  | 常量（constant） |

所以：

```python
UPLOAD_FOLDER = "uploads"     # ✅ 常量（推荐）
upload_folder = "uploads"     # 🟡 可以，但不符合习惯
UploadFolder = "uploads"      # ❌ 类命名风格
```

---

## 💡 小结

`UPLOAD_FOLDER` 用全大写，是为了：

1. 表示这是配置常量，不应该被修改；
2. 与 Flask 的配置系统（`app.config[...]`）保持一致；
3. 符合 Python 官方 PEP 8 风格规范。


