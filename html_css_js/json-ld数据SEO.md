---
title: JSON-LD 数据 SEO
date: 2025-10-28
tags: [html,web,seo]
---

# JSON-LD 数据 SEO
**JSON-LD数据**（全称 **JavaScript Object Notation for Linked Data**）——
是现代网页中非常重要的一个 **SEO 和结构化信息标记方式**。
下面我用清晰的方式帮你解释它的 **作用、原理和实际应用示例**👇

---

## 💡 一句话总结

**JSON-LD 的作用：**
👉 向搜索引擎（Google、Bing 等）提供结构化的数据，让机器能“理解”网页内容是什么，而不仅仅是“看见”文字。

---

## 🧱 二、为什么需要它？

网页给人类看时很清楚：

> “kevin是一位网页开发者，住在日本。”

但对搜索引擎来说，它只能看到一堆文本，它不知道“谢啓文”是一个人、“网页开发者”是职业。

于是就需要一种“机器可读的语义描述格式”——这就是 **结构化数据（Structured Data）**，而 **JSON-LD 是目前推荐的写法**。

---

## ⚙️ 三、它的工作方式

JSON-LD 通常放在网页的 `<head>` 或 `<body>` 内，用 `<script type="application/ld+json">` 包裹，不影响页面显示。
搜索引擎会读取它的内容，构建网页的语义信息。

---

## 📘 四、基础示例：描述一个网页文章

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "HTML 元信息大全（2025年版）",
  "author": {
    "@type": "Person",
    "name": "谢啓文"
  },
  "datePublished": "2025-10-21",
  "image": "https://example.com/cover.jpg",
  "publisher": {
    "@type": "Organization",
    "name": "啓文のWeb",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png"
    }
  }
}
</script>
```

🔍 搜索引擎会理解为：

> 这是一篇名为「HTML 元信息大全（2025年版）」的文章，作者是“谢啓文”，发布于 2025-10-21，有一张封面图。

---

## 🧭 五、有哪些常见类型(type)？

| 类型               | 用途        | 对应 Schema.org 标准                                                       |
| ---------------- | --------- | ---------------------------------------------------------------------- |
| `Article`        | 新闻、博客、技术文 | [https://schema.org/Article](https://schema.org/Article)               |
| `Person`         | 个人资料、作者信息 | [https://schema.org/Person](https://schema.org/Person)                 |
| `Product`        | 商品页面      | [https://schema.org/Product](https://schema.org/Product)               |
| `Organization`   | 公司、网站信息   | [https://schema.org/Organization](https://schema.org/Organization)     |
| `LocalBusiness`  | 实体店铺      | [https://schema.org/LocalBusiness](https://schema.org/LocalBusiness)   |
| `Event`          | 活动、演唱会等   | [https://schema.org/Event](https://schema.org/Event)                   |
| `BreadcrumbList` | 面包屑导航     | [https://schema.org/BreadcrumbList](https://schema.org/BreadcrumbList) |
| `FAQPage`        | 问答内容      | [https://schema.org/FAQPage](https://schema.org/FAQPage)               |

---

## 📈 六、实际效果

当你在 Google 搜索时看到这些丰富展示👇
✅ 带评分的商品
✅ 有时间与作者的文章卡片
✅ FAQ 折叠区
✅ 组织 Logo + 联系信息

这些 **都来自 JSON-LD**。

---

## 🚀 七、开发者建议

1. **推荐使用 JSON-LD**，不要再使用旧的 `microdata` 或 `RDFa`。
2. 写完后可用 Google 工具验证：
   👉 [https://search.google.com/test/rich-results](https://search.google.com/test/rich-results)
3. 每个网页建议写一个对应类型的 JSON-LD。
4. **SEO 加分项**：丰富摘要（Rich Snippet）更容易获得点击。

---

## 🧾 八、小结

| 项目   | 内容                                      |
| ---- | --------------------------------------- |
| 名称   | JSON-LD（结构化数据）                          |
| 放置位置 | `<script type="application/ld+json">` 中 |
| 作用   | 让搜索引擎理解网页内容结构                           |
| 优点   | 不影响页面显示、格式清晰、Google 官方推荐                |
| 使用标准 | [Schema.org](https://schema.org)        |

---

是否希望我帮你整理成一页「JSON-LD 结构化数据速查表」Markdown 笔记？
可以收录常用类型（文章、产品、个人、FAQ 等）的完整模板。
