---
title: CSS盒模型与布局
date: 2025-10-28
tags: [css,web]
---


## 🧱 一、CSS 盒模型与布局（Box Model & Layout）

---

### 1️⃣ 基础盒模型（Box Model）

每个 HTML 元素都是一个“盒子”，由四个区域组成：

```
+-------------------------+
|       margin            |
|  +-------------------+  |
|  |     border        |  |
|  | +---------------+ |  |
|  | |   padding     | |  |
|  | | +-----------+ | |  |
|  | | |  content  | | |  |
|  | | +-----------+ | |  |
|  | +---------------+ |  |
|  +-------------------+  |
+-------------------------+
```

| 属性        | 含义  |
| --------- | --- |
| `content` | 内容区 |
| `padding` | 内边距 |
| `border`  | 边框  |
| `margin`  | 外边距 |

---

### 2️⃣ box-sizing（盒模型计算方式）

默认是 `content-box`（传统模式）：

```css
/* content-box */
div {
  width: 200px;   /* 不包含 padding 和 border */
  padding: 20px;
  border: 10px solid;
  /* 实际宽度 = 200 + 20*2 + 10*2 = 260px */
}
```

推荐使用 `border-box`（现代开发标准）：

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

> 优点：padding 与 border 不再影响元素总宽度，更易布局。

---

### 3️⃣ 块级与内联盒（Display）

| display 值      | 说明        |
| -------------- | --------- |
| `block`        | 独占一行，支持宽高 |
| `inline`       | 不换行，不支持宽高 |
| `inline-block` | 同行显示，支持宽高 |
| `none`         | 隐藏        |
| `flex`         | 弹性布局容器    |
| `grid`         | 网格布局容器    |

---

### 4️⃣ 外边距折叠（Margin Collapsing）

**现象**：垂直方向上相邻元素的 margin 会合并。

```css
p { margin: 20px 0; }
/* 两个 p 之间间距不是 40px，而是 20px */
```

**解决方法：**

* 添加 `padding` 或 `border`
* 使用 `overflow: hidden` 或 `display: flow-root`
* 新方法：`margin-trim`（CSS Working Draft）

---

### 5️⃣ 定位（Position）

| 属性值        | 说明             |
| ---------- | -------------- |
| `static`   | 默认流布局          |
| `relative` | 相对定位（相对自身偏移）   |
| `absolute` | 绝对定位（相对最近定位祖先） |
| `fixed`    | 相对视口固定         |
| `sticky`   | 滚动到某位置时固定      |

示例：

```css
header {
  position: sticky;
  top: 0;
  background: white;
}
```

---

### 6️⃣ Flexbox 弹性布局

#### 核心属性：

容器（父级）：

```css
.container {
  display: flex;
  flex-direction: row; /* row | column */
  justify-content: space-between; /* 主轴对齐 */
  align-items: center; /* 交叉轴对齐 */
  gap: 1rem;
}
```

子项（flex item）：

```css
.item {
  flex: 1 1 200px; /* flex-grow, flex-shrink, flex-basis */
}
```

#### 常见用途：

* 水平垂直居中：

  ```css
  display: flex;
  justify-content: center;
  align-items: center;
  ```
* 自适应导航栏：

  ```css
  justify-content: space-between;
  align-items: center;
  ```

---

### 7️⃣ Grid 网格布局

#### 定义网格：

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 三列等宽 */
  gap: 1rem;
}
```

#### 自动调整：

```css
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

#### 区域命名：

```css
grid-template-areas:
  "header header"
  "sidebar main"
  "footer footer";

header { grid-area: header; }
```

#### 对齐与间距：

```css
place-items: center;   /* align-items + justify-items */
place-content: center; /* align-content + justify-content */
```

---

### 8️⃣ 尺寸控制与函数单位

| 函数                           | 作用      |
| ---------------------------- | ------- |
| `min()`                      | 取最小值    |
| `max()`                      | 取最大值    |
| `clamp(min, preferred, max)` | 限制范围内变化 |

示例：

```css
font-size: clamp(1rem, 2vw, 2rem);
```

> 可随屏幕宽度变化自动调整。

---

### 9️⃣ aspect-ratio（保持宽高比）

```css
img {
  aspect-ratio: 16 / 9;
  object-fit: cover;
}
```

> 替代旧的 `padding-bottom` 技巧，更直观、可响应。

---

### 🔟 现代布局辅助属性

| 属性                                  | 说明              |
| ----------------------------------- | --------------- |
| `gap`                               | flex/grid 内部间距  |
| `place-items`                       | 快速设置水平垂直对齐      |
| `align-content` / `justify-content` | 多行内容对齐          |
| `overflow: clip`                    | 比 `hidden` 更高性能 |
| `display: flow-root`                | 清除浮动、独立布局上下文    |

---

## ✅ 二、开发 Checklist

| 项目            | 检查目标                             |
| ------------- | -------------------------------- |
| 📦 box-sizing | 全局设为 `border-box`                |
| 🧩 布局模式清晰     | 合理选择 flex / grid / flow          |
| 🧠 外边距折叠      | 注意上下文是否触发                        |
| 📏 响应式尺寸      | 使用 `min()` / `max()` / `clamp()` |
| 🖼️ 比例控制      | 使用 `aspect-ratio`                |
| 🎯 对齐方式       | 用 `gap` 替代 `margin` 分隔           |
| 🧱 层次关系       | 了解 `position` 与 `z-index` 关系     |
| 🧰 容器自适应      | 尝试 `auto-fit` 与 `minmax()`       |
| 🪶 清除浮动       | 使用 `display: flow-root` 代替伪元素    |
| 🔍 浏览器兼容      | 检查 Flex 和 Grid 在旧版浏览器的表现         |

