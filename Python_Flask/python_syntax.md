---
title: python语法 什么时候要写冒号：
date: 2025-10-28
tags: [python]
---

# python语法 什么时候要写冒号：

在 **Python** 里，冒号 `:` 是一个非常重要的语法标记。它的作用是：

> **表示“接下来是一个代码块（缩进块）”的开始。**

几乎所有需要缩进结构的语句后面，都要加冒号。

---

## ✅ 常见需要冒号的情况

### 1️⃣ 条件语句（`if` / `elif` / `else`）

```python
if x > 10:
    print("大于10")
elif x == 10:
    print("等于10")
else:
    print("小于10")
```

冒号表示「条件判断完毕，下面是满足条件时要执行的代码块」。

---

### 2️⃣ 循环语句（`for` / `while`）

```python
for i in range(5):
    print(i)

while True:
    print("循环中")
```

冒号表示「循环条件或范围定义完毕，下面是循环体」。

---

### 3️⃣ 函数定义（`def`）

```python
def greet(name):
    print("你好", name)
```

冒号表示「函数头定义完毕，下面是函数体」。

---

### 4️⃣ 类定义（`class`）

```python
class Animal:
    def speak(self):
        print("动物叫")
```

冒号表示「类定义完毕，下面是类的内容」。

---

### 5️⃣ 异常处理（`try` / `except` / `finally`）

```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("除以0错误")
finally:
    print("结束")
```

每个语句（`try`, `except`, `finally`）后都要加冒号。

---

### 6️⃣ with 上下文管理器

```python
with open("data.txt", "r") as f:
    content = f.read()
```

冒号表示「资源管理语句结束，下面是使用资源的代码」。

---

### 7️⃣ match-case 模式匹配（Python 3.10+）

```python
match command:
    case "start":
        print("开始")
    case "stop":
        print("停止")
```

---

## ⚠️ 注意

冒号后**必须有缩进（通常是4个空格或1个Tab）**，否则会报错：

```python
if x > 0:
print("正数")  # ❌ 错误：缺少缩进
```

