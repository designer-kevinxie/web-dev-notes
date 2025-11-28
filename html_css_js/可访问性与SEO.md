---
title: HTML可访问性&SEO重点知识（2025全面版）
date: 2025-10-28
tags: [html,web,seo]
---

# 🌐 HTML 可访问性 & SEO 重点知识（2025 全面版）

---

## 🧱 一、语义化结构（核心基础）

### ✅ 原则

* 用合适的标签表达内容意义，而不是仅仅为了样式。
* 让浏览器、搜索引擎、读屏器都能理解页面结构。

### 💡 关键标签

| 功能   | 标签            | 注意点                  |
| ---- | ------------- | -------------------- |
| 页面头部 | `<header>`    | 通常包含导航或标题            |
| 主要内容 | `<main>`      | 页面中唯一一个              |
| 章节   | `<section>`   | 内容有逻辑分组时使用           |
| 文章   | `<article>`   | 独立完整的内容单元（博客、新闻等）    |
| 侧栏   | `<aside>`     | 辅助内容（广告、链接等）         |
| 页脚   | `<footer>`    | 版权、联系信息等             |
| 导航   | `<nav>`       | 主菜单或目录链接             |
| 标题层级 | `<h1>`~`<h6>` | 每页 1 个 `<h1>`，结构分层清晰 |

---

## 🔍 二、SEO 重点知识

### ✅ 基础 SEO 元信息

| 元标签                                                      | 用途                 |
| -------------------------------------------------------- | ------------------ |
| `<title>`                                                | 搜索结果标题（强烈影响 SEO）   |
| `<meta name="description">`                              | 搜索摘要说明             |
| `<meta name="keywords">`                                 | 次要作用（现代搜索引擎几乎忽略）   |
| `<meta name="robots" content="index, follow">`           | 控制爬虫行为             |
| `<link rel="canonical" href="https://example.com/">`     | 避免重复内容             |
| `<meta property="og:title">`、`og:image`、`og:description` | 社交平台预览（Open Graph） |
| `<meta name="twitter:card">` 等                           | Twitter/X 分享卡片信息   |

### 🧩 内容结构优化

* [ ] 每页只有一个 `<h1>`，并且与主要主题匹配
* [ ] 使用语义化的 `<h2> ~ <h4>` 结构组织内容
* [ ] 使用 `<a>` 包含描述性文字，不用 “点击这里”
* [ ] 图片必须有 `alt` 文本（SEO + 无障碍）
* [ ] 使用 `<strong>`、`<em>` 强调关键词
* [ ] URL 简短、语义化（例如 `/html-basics`）

---

## ♿ 三、可访问性（Accessibility）

### ✅ 基础要求

| 项目   | 说明                       |
| ---- | ------------------------ |
| 可见文本 | 所有按钮和链接要有明确文字            |
| 替代文本 | 图片必须有 `alt`              |
| 表单标签 | `<label for="id">` 关联输入框 |
| 键盘导航 | 页面操作可用 Tab / Enter 完成    |
| 对比度  | 前景与背景对比度 ≥ 4.5:1         |
| ARIA | 仅在原生标签无法表达语义时使用          |

### 🔤 常用 ARIA 属性

| 属性                   | 功能      | 示例                                          |
| -------------------- | ------- | ------------------------------------------- |
| `role="alert"`       | 通知提示    | `<div role="alert">错误发生</div>`              |
| `aria-label`         | 无文本时的说明 | `<button aria-label="关闭">×</button>`        |
| `aria-hidden="true"` | 屏幕阅读器忽略 | `<span aria-hidden="true">★</span>`         |
| `aria-expanded`      | 折叠面板状态  | `<button aria-expanded="false">菜单</button>` |
| `aria-live`          | 动态内容读出  | 用于聊天或加载提示                                   |

---

## ⚙️ 四、性能与技术细节（影响可访问与SEO）

* [ ] 所有图片加 `width`、`height` 属性，防止 CLS（布局位移）
* [ ] 视频、音频元素加 `controls`
* [ ] 懒加载图片：`loading="lazy"`
* [ ] meta viewport：`<meta name="viewport" content="width=device-width, initial-scale=1">`
* [ ] 页面标题和描述保持唯一且相关
* [ ] 使用 HTTPS 与正确的语言声明：`<html lang="zh-Hans">`

---

# ✅ HTML 可访问性 & SEO 开发 Checklist

### 🧱 结构

* [ ] 有 `<main>` 区域，主要内容唯一
* [ ] 每页一个 `<h1>`
* [ ] 标题层级有序（`h1 > h2 > h3`）
* [ ] 使用 `<nav>` 包含导航菜单
* [ ] 页脚用 `<footer>`

### 🔍 SEO

* [ ] `<title>` 与页面主题一致
* [ ] `<meta name="description">` 编写自然摘要
* [ ] `<meta property="og:*">` 设置社交分享信息
* [ ] 每个链接内容清晰有意义
* [ ] 图片文件名语义化（如 `sunset-osaka.jpg`）
* [ ] URL 简短且规范

### ♿ 可访问性

* [ ] 所有图片都有 `alt`
* [ ] 表单都有 `<label>` 或 `aria-label`
* [ ] 交互元素可用键盘操作
* [ ] 对比度通过（使用 Chrome Lighthouse 检测）
* [ ] 使用 `aria-*` 仅在必要时
* [ ] 禁用视觉隐藏内容的 `aria-hidden="true"`

### ⚡ 技术与性能

* [ ] 图片延迟加载
* [ ] 视频添加 `poster`、`controls`
* [ ] 设置 `<html lang="">`
* [ ] favicon 存在
* [ ] 使用 canonical 链接
* [ ] 检查 404、重定向、robots.txt 正常


