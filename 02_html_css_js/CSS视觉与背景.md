非常好 👍
你进入了 **CSS 视觉表现层的核心章节** —— 这是现代网页视觉设计（尤其是动效、视觉层叠、毛玻璃、遮罩效果）的关键知识点。

下面是完整内容（含 **重点知识 + 实用细节 + 开发 Checklist**），适合做为你 2025 年版 CSS 视觉章节笔记。

---

## 🎨 第三章：CSS 视觉与背景

（背景图层、滤镜、混合模式、mask、clip-path）

---

### 🎯 一、重点知识与细节

#### 1️⃣ 背景（Background）

CSS 背景可以叠加多个图层，每个图层从下往上绘制。

```css
background: 
  url(bg-pattern.svg) repeat,
  linear-gradient(45deg, #ff9, #f0f);
```

##### 常用属性

| 属性                      | 说明                                     |
| ----------------------- | -------------------------------------- |
| `background-color`      | 背景色                                    |
| `background-image`      | 背景图片（可多层）                              |
| `background-repeat`     | 是否重复：`no-repeat / repeat-x / repeat-y` |
| `background-size`       | 尺寸：`cover`（全屏）、`contain`（完整显示）         |
| `background-position`   | 位置：`center / top / 50% 50%`            |
| `background-attachment` | 滚动行为：`scroll / fixed / local`          |
| `background-blend-mode` | 背景混合模式（见下）                             |

💡 **技巧：全屏背景图**

```css
body {
  background: url(hero.jpg) center/cover no-repeat fixed;
}
```

💡 **多层背景常用写法**

```css
.hero {
  background:
    linear-gradient(to bottom, rgba(0,0,0,0.5), rgba(0,0,0,0.8)),
    url(hero.jpg) center/cover no-repeat;
}
```

---

#### 2️⃣ 背景混合模式（`background-blend-mode`）

可以让多个背景层进行颜色混合（类似 Photoshop 图层模式）。

```css
.bg {
  background: url(photo.jpg), linear-gradient(#09f, #f06);
  background-blend-mode: multiply;
}
```

常见模式：

* `multiply`：颜色相乘，常用于压暗背景。
* `screen`：颜色变亮。
* `overlay`：结合 multiply 与 screen。
* `soft-light` / `hard-light`：光影效果。
* `difference` / `exclusion`：反色效果。

🎨 示例用途：

* 增强可读性（文字上加色彩层）；
* 营造电影感对比；
* 动态主题背景。

---

#### 3️⃣ 滤镜（`filter`）

为元素或图像添加图像效果（模糊、亮度、对比、灰度等）。

```css
img {
  filter: grayscale(80%) contrast(1.2);
}
```

常见滤镜：

| 滤镜名                           | 示例         |
| ----------------------------- | ---------- |
| `blur(px)`                    | 模糊         |
| `brightness(%)`               | 亮度         |
| `contrast(%)`                 | 对比度        |
| `grayscale(%)`                | 灰度化        |
| `sepia(%)`                    | 复古色调       |
| `hue-rotate(deg)`             | 色相旋转       |
| `saturate(%)`                 | 饱和度        |
| `drop-shadow(x y blur color)` | 阴影（不受背景干扰） |

💡 **毛玻璃效果**

```css
.backdrop {
  backdrop-filter: blur(10px) brightness(0.9);
  background: rgba(255,255,255,0.3);
}
```

⚠️ 注意：

* `filter` 影响元素绘制性能，尽量用于少量元素。
* Safari 上需加 `-webkit-backdrop-filter`。

---

#### 4️⃣ 遮罩（Mask）

用于根据形状或透明度显示部分内容。
类似于 Photoshop 的“蒙版层”。

```css
.masked {
  mask-image: url(mask-shape.png);
  mask-size: contain;
  mask-repeat: no-repeat;
}
```

* `mask-image`: 使用透明度作为遮罩。
* `mask-mode`: 定义遮罩是否基于 alpha 或亮度。
* `mask-position`, `mask-size`: 同背景图。

💡 **渐变遮罩**

```css
.fade-out {
  mask-image: linear-gradient(to bottom, black 80%, transparent 100%);
}
```

💡 **SVG 遮罩**

```css
mask: url(#svgMask);
```

⚠️ 浏览器支持仍有差异（Safari / iOS 较好，部分 Android 需前缀）。

---

#### 5️⃣ 裁剪路径（`clip-path`）

用于裁剪元素的可见区域（不影响布局）。

```css
.circle {
  clip-path: circle(50% at 50% 50%);
}
```

支持的函数：

| 函数          | 示例     |
| ----------- | ------ |
| `circle()`  | 圆形     |
| `ellipse()` | 椭圆     |
| `polygon()` | 自定义多边形 |
| `inset()`   | 矩形区域裁剪 |

💡 **实用例子**

```css
.triangle {
  clip-path: polygon(50% 0, 0 100%, 100% 100%);
}
```

💡 **SVG 路径裁剪**

```css
clip-path: path("M10,10 h80 v80 h-80 Z");
```

💡 **配合动画**

```css
@keyframes reveal {
  from { clip-path: circle(0% at 50% 50%); }
  to { clip-path: circle(150% at 50% 50%); }
}
```

---

### ✅ 二、开发 Checklist

| 类别        | 检查点                                        |
| --------- | ------------------------------------------ |
| 背景图层      | 是否合并为一行简洁语法？是否设置 `background-size: cover`？ |
| 混合模式      | 是否考虑文字对比度可读性？                              |
| 滤镜        | 是否避免滥用、影响性能？是否使用 GPU-friendly 属性？          |
| 毛玻璃效果     | 使用 `backdrop-filter` + 半透明背景，确保 Safari 兼容  |
| 遮罩 mask   | 检查浏览器支持与后备方案（fallback）                     |
| clip-path | 是否简化路径点数量？是否与交互/动画结合？                      |
| 图层管理      | 同时使用背景/混合/遮罩时，注意堆叠顺序和透明度                   |
| 性能        | 滤镜与混合尽量避免在滚动区域或大面积应用                       |

---

是否继续下一章？
👉 下一章推荐进入 **「CSS 动画与过渡（Transitions, Keyframes, Motion Principles）」**，这是现代网页动效与交互动线的重点章节。
