## 🧩 HTML 与 JavaScript 的交互接口（重点 + 细节 + Checklist）

### 一、核心知识点

#### 1. DOM（Document Object Model）

* **定义**：HTML 被解析后生成的树状结构，JS 可通过 DOM API 操作页面元素。
* **重点操作**：

  ```js
  document.querySelector('h1').textContent = 'Hello!';
  document.getElementById('btn').addEventListener('click', () => alert('clicked'));
  ```
* **常见选择器**：

  * `getElementById()`
  * `querySelector()` / `querySelectorAll()`
  * `closest()`（找到最近的祖先元素）
* **性能优化**：避免频繁操作 DOM，可使用 fragment 或一次性 innerHTML 替换。



#### 2. 自定义属性（data-*）

* **用途**：安全地向 HTML 元素添加自定义数据，供 JS 读取。

  ```html
  <button data-user-id="42">Click</button>
  <script>
    const btn = document.querySelector('button');
    console.log(btn.dataset.userId); // "42"
  </script>
  ```
* **注意**：`dataset` 自动转为小驼峰，如 `data-user-id → dataset.userId`。

#### 3. 事件（Event）

* **事件绑定方式**：

  * HTML 内联（不推荐）
    `<button onclick="doSomething()">`
  * JS 绑定（推荐）
    `element.addEventListener('click', handler)`
* **事件委托**：使用父元素监听子元素事件，减少绑定数。

  ```js
  document.querySelector('ul').addEventListener('click', e => {
    if (e.target.tagName === 'LI') console.log(e.target.textContent);
  });
  ```
* **常见事件类型**：

  * 用户操作：`click`, `input`, `submit`, `change`
  * 页面：`load`, `DOMContentLoaded`, `scroll`, `resize`
  * 键盘鼠标：`keydown`, `mouseenter`, `contextmenu`

#### 4. 表单与 JS 交互

* **获取输入值**：

  ```js
  const name = document.querySelector('input[name="username"]').value;
  ```
* **防止默认提交**：

  ```js
  form.addEventListener('submit', e => e.preventDefault());
  ```
* **表单验证**：

  * 使用 HTML5 的 `required`, `pattern`, `minlength`
  * JS 自定义验证结合 `setCustomValidity()`

#### 5. 多媒体控制（HTMLMediaElement API）

```js
const video = document.querySelector('video');
video.play();
video.pause();
video.currentTime = 30;
```

* 支持事件：`play`, `pause`, `ended`, `timeupdate`
* 可用于制作自定义播放器或交互动画。

#### 6. Web Components 与自定义元素

* **定义**：通过自定义标签封装功能模块。

  ```js
  class MyCard extends HTMLElement {
    connectedCallback() {
      this.innerHTML = `<div class="card">${this.getAttribute('title')}</div>`;
    }
  }
  customElements.define('my-card', MyCard);
  ```
* 结合 Shadow DOM 提供样式隔离与封装。

---

### 二、HTML ↔ JS 常见交互细节

| 场景     | HTML 技巧              | JS 操作                          |
| ------ | -------------------- | ------------------------------ |
| 动态更新文本 | `id` 或 `data-*`      | `textContent`                  |
| 改变样式   | `class` / `style` 属性 | `classList.add/remove/toggle`  |
| 动态加载内容 | `<template>`         | `document.importNode()`        |
| 控制媒体   | `<video>`, `<audio>` | `.play() / .pause()`           |
| 动态表单   | `<form>`             | `.submit() / preventDefault()` |

---

### 三、开发 Checklist ✅

| 项目       | 检查点                                         |
| -------- | ------------------------------------------- |
| ✅ DOM 操作 | 是否减少重排重绘？是否批量更新？                            |
| ✅ 数据属性   | 是否统一使用 `data-*` 存储业务数据？                     |
| ✅ 事件     | 是否使用事件委托代替多次绑定？                             |
| ✅ 表单     | 是否正确阻止默认行为并进行验证？                            |
| ✅ 媒体     | 是否设置 preload / controls / accessibility 属性？ |
| ✅ 自定义组件  | 是否封装成可复用 Web Component？                     |
| ✅ JS 安全性 | 是否避免 innerHTML 注入？是否转义用户输入？                 |


