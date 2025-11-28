---
title: HTML元信息metadata重点知识与细节
date: 2025-10-28
tags: [html,web]
---


HTML 的 **元信息（metadata）** 是网页中最容易忽视、但对 **SEO、性能、PWA、社交分享、移动端优化** 都极其重要的部分。
以下是截至 **2025 年** 常用、推荐掌握的元信息完整清单（含说明与示例）。

---

## 🧱 一、基本信息（Basic Metadata）

| 名称         | 示例                                                                       | 说明                    |
| ---------- | ------------------------------------------------------------------------ | --------------------- |
| 字符集        | `<meta charset="UTF-8">`                                                 | 网页文字编码（必须第一行之一）       |
| 视口         | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | 适配手机屏幕比例              |
| 描述         | `<meta name="description" content="网页简要描述，显示在搜索结果中">`                    | SEO 关键字段              |
| 作者         | `<meta name="author" content="Your Name">`                               | 作者信息                  |
| 关键词（已不再重要） | `<meta name="keywords" content="HTML, CSS, 教程">`                         | 现代搜索引擎基本忽略            |
| robots     | `<meta name="robots" content="index, follow">`                           | 控制爬虫行为（index/noindex） |
| 语言         | `<html lang="zh-CN">`                                                    | 建议在 `<html>` 标签中设置    |

---

## 📱 二、移动端与显示优化

| 名称                                    | 示例                                                                                | 说明                   |
| ------------------------------------- | --------------------------------------------------------------------------------- | -------------------- |
| theme-color                           | `<meta name="theme-color" content="#ffffff">`                                     | 设置浏览器顶部工具栏颜色（安卓效果显著） |
| color-scheme                          | `<meta name="color-scheme" content="light dark">`                                 | 支持暗黑模式适配             |
| apple-mobile-web-app-capable          | `<meta name="apple-mobile-web-app-capable" content="yes">`                        | iOS Safari 全屏显示（PWA） |
| apple-mobile-web-app-status-bar-style | `<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">` | iOS 状态栏样式            |
| apple-touch-icon                      | `<link rel="apple-touch-icon" href="icon.png">`                                   | iOS 桌面图标             |
| format-detection                      | `<meta name="format-detection" content="telephone=no">`                           | 阻止 iOS 自动识别电话号码      |

---

## 🔗 三、社交媒体分享（Open Graph + Twitter Card）

| 名称             | 示例                                                                   | 说明                            |
| -------------- | -------------------------------------------------------------------- | ----------------------------- |
| og:title       | `<meta property="og:title" content="我的网站标题">`                        | 分享时显示的标题                      |
| og:description | `<meta property="og:description" content="一句话摘要">`                   | 分享时显示的简介                      |
| og:image       | `<meta property="og:image" content="https://example.com/cover.jpg">` | 分享时显示的图片                      |
| og:url         | `<meta property="og:url" content="https://example.com">`             | 页面链接                          |
| og:type        | `<meta property="og:type" content="website">`                        | 内容类型（article, video, website） |
| twitter:card   | `<meta name="twitter:card" content="summary_large_image">`           | Twitter 分享卡片格式                |
| twitter:title  | `<meta name="twitter:title" content="网页标题">`                         | 分享标题                          |
| twitter:image  | `<meta name="twitter:image" content="封面图片链接">`                       | 分享图片                          |
| twitter:description  | `<meta name="twitter:description" content="网页简介">`                       | 网页简介                          |

> ✅ **建议**：
> 把 Open Graph 与 Twitter Card 一起写上，便于 Facebook / X / LINE / Discord 等平台解析分享卡片。

---

## ⚙️ 四、性能与资源提示（Performance Hints）

| 名称            | 示例                                                            | 说明       |
| ------------- | ------------------------------------------------------------- | -------- |
| preload       | `<link rel="preload" href="main.css" as="style">`             | 预加载关键资源  |
| prefetch      | `<link rel="prefetch" href="next-page.html">`                 | 提前加载下一页  |
| dns-prefetch  | `<link rel="dns-prefetch" href="//cdn.example.com">`          | 提前解析域名   |
| preconnect    | `<link rel="preconnect" href="https://fonts.googleapis.com">` | 提前建立连接   |
| defer / async | `<script src="main.js" defer>`                                | 控制脚本加载顺序 |

---

## 🧭 五、PWA（渐进式 Web 应用）

| 名称             | 示例                                            | 说明                |
| -------------- | --------------------------------------------- | ----------------- |
| manifest       | `<link rel="manifest" href="/manifest.json">` | PWA 配置文件（图标、启动页等） |
| service-worker | 注册在 JS 内，缓存离线功能                               | 现代 Web App 核心     |
| application-name | `<meta name="application-name" content="MyApp">` | 应用名称（安装时显示） |
---

## 🧩 六、SEO 与结构化数据

| 名称            | 示例                                                                   | 说明            |
| ------------- | -------------------------------------------------------------------- | ------------- |
| canonical     | `<link rel="canonical" href="https://example.com/page">`             | 防止重复内容        |
| hreflang      | `<link rel="alternate" href="https://example.com/en" hreflang="en">` | 多语言页面         |
| JSON-LD 结构化数据 | `<script type="application/ld+json">{ ... }</script>`                | Google 识别丰富摘要 |

示例：

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "谢啓文",
  "jobTitle": "Web Developer",
  "url": "https://example.com"
}
</script>
```

---

## 💡 七、其他实用元标签

| 名称               | 示例                                                                                         | 说明             |
| ---------------- | ------------------------------------------------------------------------------------------ | -------------- |
| referrer         | `<meta name="referrer" content="no-referrer">`                                             | 控制引用来源信息       |
| generator        | `<meta name="generator" content="VS Code">`                                                | 编辑器信息（非必要）     |
| copyright        | `<meta name="copyright" content="© 2025 Your Name">`                                       | 版权信息           |
| application-name | `<meta name="application-name" content="My App">`                                          | 显示在安装或PWA界面上   |
| viewport-fit     | `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">` | iPhone X 刘海屏适配 |

---

## ✅ 推荐实践组合（现代网页头部示例）

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <meta name="description" content="现代 HTML 元信息完整示例">
  <meta name="theme-color" content="#ffffff">
  <meta name="color-scheme" content="light dark">

  <link rel="icon" href="/favicon.svg" type="image/svg+xml">
  <link rel="manifest" href="/manifest.json">

  <!-- Open Graph -->
  <meta property="og:title" content="HTML 元信息大全">
  <meta property="og:description" content="2025 年最完整的 meta 标签整理">
  <meta property="og:image" content="https://example.com/cover.jpg">
  <meta property="og:type" content="website">

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image">

  <!-- 性能优化 -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preload" href="main.css" as="style">
</head>

```

---

### 💡 学习与实践建议

- 每个项目 都应该至少包含 `charset`, `viewport`, `descriptio`n, `theme-color`。
- 如果网站会分享到社交平台，一定要加上 Open Graph。
- 移动端网站务必加上 `viewport-fit`、`apple-touch-icon` 等优化。
- 定期检查 `<head>` 区内容是否符合最新 SEO 与性能标准。