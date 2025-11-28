---
title: 2025年版HTML+CSS总览Checklist
date: 2025-10-28
tags: [html,css,web]
---

## 🧭 2025 年版 HTML + CSS 总览 Checklist

**（重点知识 + 开发实用检查点）**

---

### 🏷 HTML 基础结构与语义

**重点知识：**

* 文档声明：`<!DOCTYPE html>`
* 语言声明：`<html lang="ja">`
* 语义化标签：`<header> <main> <article> <section> <nav> <footer>`
* 块级/行内元素差异、嵌套规则

**开发 Checklist：**

* [ ] HTML 结构清晰、层级合理
* [ ] 使用语义化标签，不滥用 `<div>`
* [ ] 所有标签闭合且缩进规范
* [ ] 包含 `<title>`、`<meta charset="utf-8">`

---

### 🧩 HTML 元信息与 SEO

**重点知识：**

* `<meta name="description" content="">`
* `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
* `<meta property="og:title">`, `<meta property="og:image">`（Open Graph）
* `<link rel="canonical" href="">`

**开发 Checklist：**

* [ ] 页面有唯一 title、description
* [ ] OG / Twitter Card 信息配置完整
* [ ] favicon、manifest.json 可用
* [ ] canonical URL 指向正确版本

---

### 📊 JSON-LD 与结构化数据

**重点知识：**

* 使用 `<script type="application/ld+json">`
* 标记：`@context`, `@type`, `name`, `url`, `image`
* 常见类型：`WebPage`, `Product`, `Organization`, `Article`

**开发 Checklist：**

* [ ] JSON-LD 数据结构通过 Google Rich Result 测试
* [ ] JSON 语法校验无误
* [ ] 对应内容真实、无关键词堆砌

---

### ✏️ 表单与输入

**重点知识：**

* 现代输入类型：`email`, `tel`, `url`, `number`, `date`, `color`
* 表单验证属性：`required`, `pattern`, `min/max`, `step`
* `<datalist>` 自动补全、`<output>` 动态输出
* 无障碍：`<label for="">`、`aria-describedby`

**开发 Checklist：**

* [ ] 所有输入字段有 label
* [ ] 验证逻辑前端 + 后端双重
* [ ] 输入类型与语义一致
* [ ] 移动端键盘类型合理

---

### 🖼 图片与多媒体

**重点知识：**

* 响应式图片：`<picture>`, `<source srcset>`, `sizes`
* 懒加载：`loading="lazy"`
* `<video>` 与 `<audio>` 属性：`controls`, `autoplay`, `muted`, `loop`
* WebP / AVIF 优化

**开发 Checklist：**

* [ ] 使用 `srcset` 提供多分辨率
* [ ] 图片 lazyload 生效
* [ ] 视频文件带封面 poster
* [ ] 文件格式尽量优化（WebP）

---

### ♿ 可访问性（A11Y）与 SEO

**重点知识：**

* `alt`、`aria-label`、`role`
* `tabindex` 键盘导航
* `lang` 声明与结构顺序
* SEO：语义结构 + 标题层级 + 内链逻辑

**开发 Checklist：**

* [ ] 图片均有 `alt`
* [ ] 支持键盘导航（Tab / Enter）
* [ ] 标题层级 H1-H2-H3 有逻辑顺序
* [ ] 页面可被屏幕阅读器识别

---

### 🧱 HTML5 新特性

**重点知识：**

* 新标签：`<dialog>`, `<template>`, `<details>`, `<summary>`
* 本地存储：`localStorage`, `sessionStorage`
* 新 API：`fetch()`, `navigator.geolocation`
* Web Components：`<custom-element>` 自定义组件

**开发 Checklist：**

* [ ] `<dialog>` 实现模态交互
* [ ] 使用 `<template>` 提高复用性
* [ ] API 权限获取安全可控
* [ ] 本地数据存储有清理机制

---

## 🎨 CSS 总览

---

### 🎯 选择器与结构

**重点知识：**

* 层级选择器、伪类（`:hover`, `:nth-child()`）
* 属性选择器 `[data-type="primary"]`
* 伪元素 `::before`, `::after`
* 优先级规则（!important、内联样式）

**开发 Checklist：**

* [ ] 不滥用 `!important`
* [ ] 命名采用 BEM / 语义化方式
* [ ] 伪类、伪元素命名逻辑统一

---

### 📐 布局基础

**重点知识：**

* 盒模型：`box-sizing: border-box`
* 流式布局、内联块布局
* Flexbox、Grid、position、float

**开发 Checklist：**

* [ ] 全局使用 `box-sizing: border-box`
* [ ] 优先使用 Flex / Grid 替代 float
* [ ] 响应式断点逻辑清晰

---

### 🎨 视觉与背景

**重点知识：**

* 背景多层叠加：`background: url() center/cover no-repeat`
* 滤镜：`filter: blur(), brightness(), contrast()`
* 混合模式：`mix-blend-mode`
* 裁剪与遮罩：`clip-path`, `mask-image`

**开发 Checklist：**

* [ ] 背景图片大小自适应
* [ ] 滤镜与混合模式性能可接受
* [ ] 使用 SVG 或 clip-path 优化形状效果

---

### 🧩 过渡与动画

**重点知识：**

* `transition` 平滑交互
* `@keyframes` 定义多阶段动画
* `transform` GPU 加速
* `prefers-reduced-motion` 无障碍支持

**开发 Checklist：**

* [ ] 动画仅用于 transform / opacity
* [ ] 复杂动画命名统一
* [ ] 动画节奏自然，支持 reduced motion

---

### 🪄 响应式与变量

**重点知识：**

* CSS 变量：`--primary-color`
* 媒体查询：`@media (min-width: 768px)`
* 容器查询：`@container (min-width: 500px)`
* 流式单位：`vw`, `vh`, `clamp()`

**开发 Checklist：**

* [ ] 使用 clamp() 控制字体缩放
* [ ] 用 CSS 变量统一主题
* [ ] 容器查询简化组件适配

---

### 🧠 性能与维护

**重点知识：**

* 减少层叠复杂度
* 合理拆分 CSS 文件
* 使用现代工具（PostCSS / Tailwind）
* 避免过度动画、阴影、滤镜

**开发 Checklist：**

* [ ] 样式文件按模块拆分
* [ ] 动画与阴影可控
* [ ] 样式表压缩与缓存设置


