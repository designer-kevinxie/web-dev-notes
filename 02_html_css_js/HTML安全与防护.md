## 🧱 一、重点知识与细节

### 1. XSS（跨站脚本攻击）

**概念**：恶意用户向页面注入 JavaScript（或 HTML），执行在其他用户的浏览器中。
**示例**：

```html
<!-- 危险的直接输出用户输入 -->
<p>欢迎：<span id="user"></span></p>
<script>
  document.getElementById('user').innerHTML = location.search; // ❌
</script>
```

**防护方法**：

* 不直接插入用户输入到 HTML 中。
* 使用 `textContent` 而不是 `innerHTML`。
* 服务端输出前进行 **HTML 转义**。
* 在 HTTP 头中启用：

  ```http
  Content-Security-Policy: default-src 'self';
  X-XSS-Protection: 1; mode=block
  ```

---

### 2. CSP（内容安全策略）

**概念**：限制浏览器加载哪些外部资源、执行哪些脚本。
**作用**：防止 XSS、数据注入、恶意脚本。
**示例**：

```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; img-src https://images.example.com; script-src 'self'">
```

**注意细节**：

* `'self'` 代表同源资源。
* 可搭配 `'nonce-xxx'` 机制只允许特定脚本执行。

---

### 3. iframe 安全

**风险**：外部网站可利用 `iframe` 注入或窃取信息。
**安全做法**：

```html
<iframe src="https://example.com" sandbox="allow-scripts allow-same-origin"></iframe>
```

* `sandbox` 限制 iframe 权限。
* 搭配 `allow` 属性控制权限：

  ```html
  <iframe allow="fullscreen; camera; microphone"></iframe>
  ```

---

### 4. HTTPS 与 Mixed Content

**问题**：HTTPS 页面内若引用 HTTP 资源，会导致“混合内容警告”。
**解决方案**：

* 所有资源（图片、脚本、字体）都使用 `https://`。
* 或使用相对协议：`//cdn.example.com/script.js`

---

### 5. 表单安全

**重点**：

* 防止 CSRF：配合 token 验证。
* 使用 `autocomplete="off"` 控制敏感信息。
* 使用 `input type="password"` 自动隐藏字符。
* 上传文件时指定：

  ```html
  <input type="file" accept="image/*" />
  ```

---

### 6. 隐私与追踪控制

**示例**：

```html
<meta name="referrer" content="no-referrer">
<meta http-equiv="Permissions-Policy" content="geolocation=(), microphone=()">
```

**作用**：

* 阻止 referrer 泄露敏感路径。
* 禁止页面滥用摄像头、地理位置等权限。

---

### 7. 点击劫持（Clickjacking）

**防护**：

* 使用响应头：

  ```http
  X-Frame-Options: DENY
  ```
* 或 CSP：

  ```http
  Content-Security-Policy: frame-ancestors 'none';
  ```

---

### 8. 可信脚本与外部依赖管理

**建议**：

* 不引用不明第三方脚本（尤其 CDN）。
* 使用 `integrity` 属性校验文件完整性。

```html
<script src="https://cdn.example.com/app.js"
        integrity="sha384-xxxxx"
        crossorigin="anonymous"></script>
```

---

## ✅ 二、开发 Checklist

| 项目           | 检查目标                                              |
| ------------ | ------------------------------------------------- |
| 🔒 HTTPS     | 所有资源均使用 HTTPS                                     |
| 🧱 CSP       | 已设置 Content-Security-Policy                       |
| 🧩 XSS 防护    | 所有用户输入均转义                                         |
| 🪟 iframe 限制 | 所有外部 iframe 添加 sandbox                            |
| 📋 表单安全      | 添加 CSRF token、限制上传类型                              |
| 🕵️ Referrer | 添加 `<meta name="referrer" content="no-referrer">` |
| 🧍 权限控制      | `<meta http-equiv="Permissions-Policy">`          |
| 🧰 外部脚本完整性   | 添加 `integrity` 和 `crossorigin`                    |
| 🚫 Frame 防护  | 添加 `X-Frame-Options` 或 CSP frame-ancestors        |
| 🧼 Cookie 安全 | 服务端设置 `HttpOnly; Secure; SameSite=Strict`         |


