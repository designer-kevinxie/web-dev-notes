「**HTML 性能与优化**」这一章非常必要，尤其是现在 2025 年前端环境下，HTML 本身也承担了不少性能与体验优化的基础职责。下面是完整、实用、可直接加入笔记的内容（含重点知识 + 开发 Checklist）：

---

# ⚡️HTML 性能与优化（2025 年版重点与细节）

---

## 一、加载与渲染性能优化

### 1️⃣ 合理使用 `defer` 与 `async`

```html
<script src="app.js" defer></script>
<script src="analytics.js" async></script>
```

* **`defer`**：脚本延迟到 DOM 解析完成后执行（按顺序）。
* **`async`**：脚本下载完立即执行（无顺序保证）。
* ✅ 建议：业务逻辑用 `defer`，统计脚本用 `async`。

---

### 2️⃣ CSS 优化

```html
<link rel="stylesheet" href="main.css">
```

* CSS 会**阻塞渲染**，应尽量减少文件数、合并关键样式。
* 对非关键样式使用：

  ```html
  <link rel="preload" href="print.css" as="style" onload="this.rel='stylesheet'">
  ```
* ✅ 样式顺序：**关键 CSS 在前，非关键异步加载**。

---

### 3️⃣ 图片优化

* 使用现代格式：

  * `AVIF` / `WebP` 优先，回退到 `JPEG/PNG`

  ```html
  <picture>
    <source srcset="photo.avif" type="image/avif">
    <source srcset="photo.webp" type="image/webp">
    <img src="photo.jpg" alt="描述文字">
  </picture>
  ```
* 设置合适尺寸：

  ```html
  <img src="photo.jpg" width="800" height="600" loading="lazy" decoding="async">
  ```

  ✅ `loading="lazy"` 可延迟加载；`decoding="async"` 提高渲染性能。

---

### 4️⃣ 字体加载优化

```html
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
```

* 避免 FOIT（空白闪烁），使用：

  ```css
  font-display: swap;
  ```
* ✅ 只加载必要的字重。

---

### 5️⃣ HTML 结构优化

* 避免过度嵌套（Deep DOM Tree 会拖慢渲染）。
* 使用语义化标签，减少不必要的 `<div>`。
* 合理拆分内容区块，提升可维护性。

---

## 二、数据与交互优化

### 6️⃣ 使用 `data-*` 存储轻量信息

* 替代隐藏 input 或全局变量。
* 避免频繁 DOM 查询与重绘。
  （详见你已有的 `data-*` 章节。）

---

### 7️⃣ 懒加载与延迟渲染

* 图片：`loading="lazy"`
* 视频：

  ```html
  <video preload="metadata" poster="preview.jpg" controls></video>
  ```
* iframe：

  ```html
  <iframe src="map.html" loading="lazy"></iframe>
  ```

✅ 优化页面首屏加载时间。

---

### 8️⃣ 缓存与资源提示（Resource Hints）

```html
<link rel="dns-prefetch" href="//cdn.example.com">
<link rel="preconnect" href="https://api.example.com">
<link rel="prefetch" href="/next.html">
<link rel="prerender" href="/next.html">
```

* **dns-prefetch**：提前解析 DNS。
* **preconnect**：提前建立 TCP/SSL 连接。
* **prefetch/prerender**：提前加载下一页资源。

✅ 对多页应用或资源繁多的项目很有效。

---

### 9️⃣ meta 性能优化相关设置

```html
<meta http-equiv="Cache-Control" content="max-age=3600">
<meta name="theme-color" content="#000000">
<meta name="color-scheme" content="light dark">
```

* 控制缓存策略与渲染主题。
* `color-scheme` 可优化暗黑模式显示。

---

## 三、开发与维护优化

### 🔟 可访问性与语义化（间接性能提升）

* 屏幕阅读器与 SEO 依赖语义结构。
* 减少多余标签能提高浏览器解析速度。

### 11️⃣ DOM 操作优化（与 JS 交互）

* 使用 `DocumentFragment`、`innerHTML` 批量更新。
* 合并多次 DOM 改动。
* 减少读取 layout 属性的次数（如 `offsetHeight`）。

---

## ✅ HTML 性能优化 Checklist

| 分类            | 检查点                                        |
| ------------- | ------------------------------------------ |
| 🧠 基础结构       | HTML 语义化合理，避免深层嵌套                          |
| ⚙️ 脚本加载       | 使用 `defer` / `async`，按需加载                  |
| 🎨 样式加载       | 合并关键 CSS，异步加载非关键样式                         |
| 🖼️ 图片        | 使用现代格式（WebP/AVIF）+ 懒加载                     |
| 🔤 字体         | `font-display: swap;` + 预加载必要字体            |
| 📦 数据         | 使用 `data-*` 存储轻量数据                         |
| 🚀 缓存提示       | `dns-prefetch` / `preconnect` / `prefetch` |
| 📱 响应式        | `<meta viewport>` + 正确尺寸属性                 |
| 🌙 主题         | 使用 `color-scheme` 支持暗黑模式                   |
| 🧩 DOM 操作     | 批量更新 DOM，避免频繁重排                            |
| 🧭 SEO / 可访问性 | 正确使用 `<main>`, `<header>`, `<nav>` 等       |


