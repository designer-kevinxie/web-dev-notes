太好了 👍
接下来整理 **CSS 变量与现代自定义属性（CSS Variables & Functions）** 章节，这是 2025 年前端开发非常核心的一部分，尤其在**主题切换、响应式设计、组件化**中非常实用。

下面是完整内容（📘重点知识 + 🔍细节 + ✅开发 Checklist）：

---

## 🧩 第五章：CSS 变量与自定义属性

---

### 🎯 一、重点知识与细节

#### 1️⃣ CSS 自定义属性（CSS Variables）

* 定义：

```css
:root {
  --primary-color: #09f;
  --font-size-base: 16px;
}
```

* 使用：

```css
button {
  background-color: var(--primary-color);
  font-size: var(--font-size-base);
}
```

**细节：**

* 可以提供默认值：

```css
color: var(--text-color, black);
```

* 作用域：

  * 在 `:root` 全局定义 → 整个页面可用
  * 在局部元素定义 → 仅对子元素有效

---

#### 2️⃣ 变量的动态主题切换

```css
[data-theme="dark"] {
  --primary-color: #f06;
  --background-color: #111;
}

body {
  background: var(--background-color);
  color: var(--primary-color);
}
```

* 利用 JS 切换 `data-theme`：

```js
document.documentElement.setAttribute('data-theme', 'dark');
```

---

#### 3️⃣ 与 `calc()`、`min()`、`max()`、`clamp()` 结合

* 动态计算尺寸或间距：

```css
h1 {
  font-size: calc(var(--font-size-base) * 2);
}

.container {
  width: min(80%, 1200px);
  padding: clamp(1rem, 2vw, 2rem);
}
```

* 解释：

  * `calc()`: 基于变量和单位运算
  * `min()/max()/clamp()`: 响应式、自适应范围控制

---

#### 4️⃣ color-mix() 与现代色彩处理（CSS Color Module Level 5）

* 混合两种颜色：

```css
:root {
  --primary: #09f;
  --secondary: #f06;
  --primary-mix: color-mix(in srgb, var(--primary) 70%, var(--secondary) 30%);
}

.button {
  background-color: var(--primary-mix);
}
```

* 可用于主题渐变、按钮 hover 色彩变化等。

---

#### 5️⃣ CSS 自定义属性注意事项

* **性能**：

  * 不会触发布局重绘，值变化仅影响使用它的属性
* **继承**：

  * 默认可继承到子元素
  * 可在局部覆盖，不影响全局其他元素
* **限制**：

  * 不能用于 `@keyframes` 的动画百分比值
  * 只能应用于支持 CSS 值的属性（width, color, margin…）

---

#### 6️⃣ 响应式主题和组件化

* 在组件化开发中，CSS 变量可用于：

  * **组件主题色**：

  ```css
  .card {
    --card-bg: white;
    background: var(--card-bg);
  }
  ```

  * **响应式布局**：

  ```css
  :root {
    --gap: clamp(0.5rem, 2vw, 2rem);
  }
  .grid {
    gap: var(--gap);
  }
  ```

---

### ✅ 二、开发 Checklist

| 类别     | 检查点                                               |
| ------ | ------------------------------------------------- |
| 变量定义   | 是否全局统一命名，局部覆盖合理                                   |
| 默认值    | 使用 `var(--name, fallback)` 防止 undefined           |
| 主题切换   | 利用 `data-theme` 或 class 切换变量，支持动态主题               |
| 计算单位   | 结合 `calc()`, `clamp()`, `min()`, `max()` 提高响应式适应性 |
| 颜色处理   | 使用 `color-mix()` 优化主题和 hover 效果                   |
| 继承与作用域 | 确保组件内变量不会意外污染全局                                   |
| 可维护性   | 命名规范、注释清晰、易读易修改                                   |
| 动画兼容   | 避免在 `@keyframes` 中直接使用自定义变量百分比                    |

---

下一步推荐整理 **现代 CSS 特性与模块化架构** 章节，
包含：`:has()`, `@layer`, `@scope`, `subgrid`, `container queries`, Utility-first / BEM 等，
这是 2025 年 CSS 高级开发与大型项目管理的核心技能。

你希望我继续整理吗？
