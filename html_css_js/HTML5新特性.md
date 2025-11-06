非常好，这一块是 HTML 进化的核心内容之一。
HTML5 已经稳定多年，但在 2025 年仍然是前端开发必须熟练掌握的基石。

以下是：

✅ **HTML5 新特性重点知识（含细节说明）**
✅ **实际开发 Checklist**

---

# 🚀 HTML5 新特性重点知识与细节（2025版）

---

## 🧱 一、语义化结构标签（Structural Elements）

HTML5 引入了大量语义化标签，使得页面结构更清晰、SEO 与可访问性更好。

| 标签                          | 用途          | 说明              |
| --------------------------- | ----------- | --------------- |
| `<header>`                  | 页头或区块头部     | 可包含 logo、标题、导航等 |
| `<nav>`                     | 导航区         | 包含主菜单、目录链接      |
| `<main>`                    | 主内容区域       | 页面主体，唯一一个       |
| `<section>`                 | 章节性内容       | 按逻辑或主题分组        |
| `<article>`                 | 独立内容单元      | 新闻、博客、评论等       |
| `<aside>`                   | 侧栏          | 辅助信息、广告等        |
| `<footer>`                  | 页脚          | 版权、联系信息等        |
| `<figure>` / `<figcaption>` | 媒体内容 + 说明文字 | 结合图片、代码片段说明等    |

✅ **细节：**

* 每页只应有一个 `<main>`
* `<article>` 通常包含独立的标题（`<h1>`~`<h3>`）
* `<section>` 必须有标题（通常是 `<h2>`）

---

## 🎯 二、表单新特性（Forms）

HTML5 大幅强化了表单功能，无需额外 JS。

### 🧩 新增输入类型

| 类型                                        | 示例                                       | 功能            |
| ----------------------------------------- | ---------------------------------------- | ------------- |
| `email`                                   | `<input type="email">`                   | 自动验证邮箱格式      |
| `url`                                     | `<input type="url">`                     | 自动验证 URL      |
| `number`                                  | `<input type="number" min="0" max="10">` | 数字选择器         |
| `range`                                   | `<input type="range" min="0" max="100">` | 滑块            |
| `date`, `time`, `month`, `datetime-local` | 日期时间选择                                   |               |
| `color`                                   | `<input type="color">`                   | 取色器           |
| `search`                                  | `<input type="search">`                  | 搜索框（样式略不同）    |
| `tel`                                     | `<input type="tel">`                     | 手机输入键盘优化（移动端） |

### 🧠 新增属性

| 属性             | 功能          |
| -------------- | ----------- |
| `required`     | 必填验证        |
| `placeholder`  | 输入提示        |
| `pattern`      | 正则验证        |
| `autocomplete` | 自动填充        |
| `autofocus`    | 自动聚焦        |
| `multiple`     | 多文件或多邮箱上传   |
| `form`         | 可把输入与不同表单关联 |
| `novalidate`   | 禁用自动验证      |

---

## 🖼️ 三、媒体标签（Multimedia）

### 🧩 新标签

| 标签         | 功能                 |
| ---------- | ------------------ |
| `<audio>`  | 播放音频               |
| `<video>`  | 播放视频               |
| `<track>`  | 添加字幕、说明文字          |
| `<source>` | 提供多格式资源            |
| `<canvas>` | 绘制 2D 动画、图形        |
| `<svg>`    | 矢量图形（XML 格式，可直接内嵌） |

✅ **细节：**

* `<video>` 自动播放必须加 `muted` 才能生效
* `<canvas>` 用 JS 控制绘图内容
* `<track>` 用于字幕，支持多语言

---

## 📦 四、离线与存储（Offline & Storage）

| 特性                    | 说明                      | 状态     |
| --------------------- | ----------------------- | ------ |
| **LocalStorage**      | 持久存储（无过期时间）             | ✅ 推荐使用 |
| **SessionStorage**    | 临时存储（关闭标签页失效）           | ✅      |
| **IndexedDB**         | 结构化数据库，存储大量数据           | ✅      |
| **Application Cache** | 已弃用（请使用 Service Worker） | ❌      |

### 示例：

```js
localStorage.setItem('user', 'Ken');
console.log(localStorage.getItem('user'));
```

---

## 🌐 五、通信与多线程（Communication & Performance）

| 特性                           | 功能          |
| ---------------------------- | ----------- |
| **WebSocket**                | 双向通信        |
| **Server-Sent Events (SSE)** | 单向推送        |
| **Web Workers**              | 后台线程计算      |
| **Shared Workers**           | 多标签页共享线程    |
| **Service Workers**          | 离线缓存、PWA 核心 |

---

## 🧠 六、其他新特性与细节

| 特性                        | 功能                   |
| ------------------------- | -------------------- |
| `<template>`              | 预定义 HTML 模板（JS 动态克隆） |
| `<dialog>`                | 原生模态框（可用 JS 控制）      |
| `<details>` / `<summary>` | 可折叠信息块               |
| `<progress>` / `<meter>`  | 进度条与测量值              |
| `<mark>`                  | 高亮文本                 |
| `<time>`                  | 标准化时间标记              |
| `<output>`                | 显示计算或脚本结果            |

### 示例：

```html
<details>
  <summary>点击展开</summary>
  <p>更多内容……</p>
</details>
```

---

# ✅ HTML5 开发 Checklist（实战用）

### 🧱 结构与语义

* [ ] 使用 `<main>`, `<section>`, `<article>` 清晰组织结构
* [ ] 每页一个 `<h1>`
* [ ] 语义标签替代 `<div>` 滥用
* [ ] `<figure>` + `<figcaption>` 说明图片内容

### 🧩 表单

* [ ] 使用新输入类型（`email`, `date`, `color`）
* [ ] 启用原生验证：`required`, `pattern`, `min`, `max`
* [ ] 使用 `<datalist>` 提供建议选项
* [ ] 提供 `<label>` 关联输入

### 🎥 媒体

* [ ] `<video>` 和 `<audio>` 提供多格式与控制条
* [ ] 懒加载图片：`loading="lazy"`
* [ ] 兼容性格式：WebP / MP4 / Ogg
* [ ] 提供字幕文件（`<track>`）

### 💾 存储与离线

* [ ] 小数据：`localStorage` 或 `sessionStorage`
* [ ] 大数据：`IndexedDB`
* [ ] 使用 `Service Worker` 缓存关键资源

### ⚙️ 其他功能

* [ ] 模态框使用 `<dialog>`
* [ ] 折叠信息用 `<details>` / `<summary>`
* [ ] 使用 `<progress>` 显示加载状态
* [ ] `<template>` 管理动态内容
* [ ] 正确使用 `<time>`、`<mark>`、`<output>`


