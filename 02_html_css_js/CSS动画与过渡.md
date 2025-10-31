太好了 👍
接下来整理 **CSS 动画与过渡（Transitions & Keyframes）** 章节，适合现代网页交互、动效设计与性能优化。

下面是完整内容（📘重点知识 + 🔍细节 + ✅开发 Checklist）：

---

## 🎞 第四章：CSS 动画与过渡

---

### 🎯 一、重点知识与细节

#### 1️⃣ 过渡（Transition）

用于在状态变化时平滑过渡属性值。

**基本语法**

```css
.element {
  transition-property: all; /* 或具体属性：width, opacity */
  transition-duration: 0.3s;
  transition-timing-function: ease; /* linear, ease-in, ease-out, cubic-bezier() */
  transition-delay: 0s;
}
```

**示例：鼠标悬停渐变**

```css
button {
  background-color: #09f;
  transition: background-color 0.3s ease;
}
button:hover {
  background-color: #f06;
}
```

**细节：**

* 推荐只对需要的属性添加过渡，避免 `all` 影响性能。
* 支持多个属性：

```css
transition: opacity 0.3s, transform 0.4s ease-in-out;
```

---

#### 2️⃣ 关键帧动画（Keyframes）

适合连续、多状态的复杂动画。

**语法**

```css
@keyframes slideIn {
  0%   { transform: translateX(-100%); opacity: 0; }
  50%  { transform: translateX(0); opacity: 0.5; }
  100% { transform: translateX(0); opacity: 1; }
}

.box {
  animation-name: slideIn;
  animation-duration: 1s;
  animation-timing-function: ease-out;
  animation-delay: 0s;
  animation-iteration-count: 1; /* or infinite */
  animation-fill-mode: forwards; /* 保持结束状态 */
}
```

**细节：**

* `animation-fill-mode`：

  * `forwards`：动画结束后保持最终状态
  * `backwards`：延迟期间应用起始状态
  * `both`：结合前两者
* `animation-iteration-count` 可以循环：

  * `infinite` 无限循环
* `animation-direction`：

  * `normal`、`reverse`、`alternate`、`alternate-reverse`

---

#### 3️⃣ 动画函数（Timing Function）

* `linear`：匀速
* `ease` / `ease-in` / `ease-out` / `ease-in-out`：渐进缓动
* 自定义贝塞尔曲线：

```css
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
```

* `steps(n, start|end)`：

  * 用于帧动画或像素级跳动

---

#### 4️⃣ 动画性能优化

* 尽量动画 **transform / opacity**，避免布局触发（reflow/repaint）。
* 使用 `will-change` 提前告诉浏览器：

```css
.element {
  will-change: transform, opacity;
}
```

* 避免在滚动大面积元素上使用复杂滤镜或多层动画。
* 使用 GPU 加速：

  * `transform: translateZ(0)` 或 `translate3d()`

---

#### 5️⃣ Scroll / Viewport 动画（现代特性）

* CSS Scroll Timeline（部分浏览器支持）

```css
@scroll-timeline myTimeline {
  source: auto;
  orientation: block;
}

.box {
  animation: fadeIn 1s linear;
  animation-timeline: myTimeline;
}
```

* 结合 Intersection Observer 可实现懒加载动画或滚动触发效果。

---

#### 6️⃣ 常见动效应用场景

* 按钮 hover 效果（渐变/缩放）
* 图片或卡片入场（slide/fade）
* loading spinner / 旋转动画
* 页面切换 / 弹窗开合
* scroll-triggered 动画（视差/滚动进场）

---

### ✅ 二、开发 Checklist

| 类别                | 检查点                                                         |
| ----------------- | ----------------------------------------------------------- |
| 过渡                | 仅为必要属性添加过渡，避免 `all` 影响性能                                    |
| 关键帧               | 明确动画起始/结束状态，使用 `forwards` 保持最终状态                            |
| 循环与方向             | 确认 `animation-iteration-count` 与 `animation-direction` 是否合理 |
| 动画函数              | 使用合理的缓动函数，必要时自定义 cubic-bezier                               |
| 性能优化              | 优先使用 transform / opacity，必要时加 `will-change`                 |
| GPU 加速            | 对大面积动画或滚动区域使用 3D transform                                  |
| Scroll / Viewport | 配合 `@scroll-timeline` 或 Intersection Observer               |
| 可访问性              | 避免快速闪烁或影响感光性用户，可提供 `prefers-reduced-motion` 支持              |

---

#### 7️⃣ 可访问性与降级方案

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

* 尊重用户系统设置，避免眩晕或不适。
* 过渡和动画不影响功能可用性。

---

是否继续下一章？
👉 下一章可以整理 **CSS 变量、自定义属性、主题切换与现代 CSS 函数**（`var()`, `calc()`, `clamp()`, `color-mix()` 等），这是现代前端最重要的模块化与主题设计技能。
