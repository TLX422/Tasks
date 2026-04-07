# 🎨 CSS 学习笔记

## 1️⃣ 什么是 CSS？
- **CSS**（Cascading Style Sheets，层叠样式表）用于控制网页的**外观与布局**
- 可以独立于 HTML 文件，实现**内容与表现分离**
- 文件后缀为 `.css`

## 2️⃣ CSS 的三种使用方式

| 方式 | 语法 | 适用场景 |
|------|------|----------|
| **行内样式** | `<div style="color: red;">` | 单个元素特殊样式 |
| **内部样式表** | `<style> div { color: red; } </style>` | 单页面测试 |
| **外部样式表** | `<link rel="stylesheet" href="style.css">` | 实际项目（推荐） |

---

## 3️⃣ CSS 基础语法

```css
选择器 {
    属性名: 属性值;
    属性名: 属性值;
}
```

示例：

```css
h1 {
    color: blue;
    font-size: 24px;
}
```

📌 注释：/* 这是CSS注释 */

---

4️⃣ 常用选择器（优先级递增）
```
选择器 语法 示例 权重
通用选择器 * * { margin: 0; } 0
元素选择器 元素名 p { } 1
类选择器 .类名 .title { } 10
ID选择器 #id名 #header { } 100
属性选择器 [属性] [type="text"] { } 10
伪类选择器 : a:hover { } 10
伪元素选择器 :: p::first-line { } 1
```
组合与嵌套：

```css
/* 后代选择器 */
div p { }

/* 子选择器 */
div > p { }

/* 相邻兄弟 */
h1 + p { }

/* 通用兄弟 */
h1 ~ p { }

/* 多类选择器 */
.btn.primary { }
```

---

5️⃣ 层叠与继承

-- 层叠：多个选择器作用于同一元素时，按 权重 和 源顺序 决定最终样式。
-- 继承：部分属性（如 color, font-family）会自动从父元素传给子元素。
-- 强制覆盖：!important（慎用，会破坏层叠规则）

```css
p {
    color: red !important;
}
```

---

6️⃣ 盒模型（Box Model）

所有元素都是矩形盒子，由四部分组成：

```
+----------------------------------+
|            margin (外边距)        |
|  +----------------------------+  |
|  |          border (边框)      |  |
|  |  +----------------------+  |  |
|  |  |      padding (内边距)  |  |  |
|  |  |  +----------------+  |  |  |
|  |  |  |   content      |  |  |  |
|  |  |  |   内容区        |  |  |  |
|  |  |  +----------------+  |  |  |
|  |  +----------------------+  |  |
|  +----------------------------+  |
+----------------------------------+
```

盒模型类型：

```css
/* 标准盒模型（默认） */
box-sizing: content-box;
/* 宽度 = content */

/* IE盒模型（更常用） */
box-sizing: border-box;
/* 宽度 = content + padding + border */
```

✅ 最佳实践：全局设置 * { box-sizing: border-box; }

---

7️⃣ 常见样式属性速查

📌 文本与字体

```css
font-family: "微软雅黑", Arial, sans-serif;
font-size: 16px;        /* 常用单位：px, rem, em */
font-weight: bold;      /* 或 400, 700 */
text-align: center;     /* left, right, justify */
line-height: 1.5;
color: #333;
text-decoration: none;  /* 去掉下划线 */
```

🎨 背景

```css
background-color: #f0f0f0;
background-image: url('bg.jpg');
background-repeat: no-repeat;
background-position: center;
background-size: cover; /* contain / 100% auto */
```

📦 边框与圆角

```css
border: 1px solid #ccc;
border-radius: 8px;     /* 圆角 */
box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
```

📐 尺寸与边距

```css
width: 100%; max-width: 1200px;
height: auto;
margin: 10px 20px;      /* 上 左右 下 */
padding: 8px 12px;
```

---

8️⃣ 布局核心：Flexbox（一维布局）

父容器（flex container）属性：

```css
display: flex;
flex-direction: row | column;      /* 主轴方向 */
justify-content: center | space-between | flex-start; /* 主轴对齐 */
align-items: center | stretch;     /* 交叉轴对齐 */
flex-wrap: wrap;                   /* 换行 */
gap: 20px;                         /* 子项间距 */
```

子项（flex item）属性：

```css
flex: 1;               /* 比例分配剩余空间 */
align-self: center;    /* 单独对齐 */
order: 2;              /* 排序 */
```

📌 经典居中：display: flex; justify-content: center; align-items: center;

---

9️⃣ 布局核心：Grid（二维布局）

父容器：

```css
display: grid;
grid-template-columns: 1fr 2fr 1fr;   /* 三列 */
grid-template-rows: auto 200px;
gap: 16px;
```

区域命名：

```css
.container {
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
}
.header { grid-area: header; }
```

子项跨度：

```css
.item {
    grid-column: span 2;   /* 跨2列 */
    grid-row: 1 / 3;       /* 从第1行到第3行 */
}
```

---

🔟 定位（Position）

值 说明
static 默认，文档流
relative 相对自身正常位置偏移
absolute 相对于最近的非static祖先定位
fixed 相对于视口定位
sticky 粘性定位（滚动到阈值后固定）

```css
.parent {
    position: relative;
}
.child {
    position: absolute;
    top: 0;
    left: 0;
}
```

---

1️⃣1️⃣ 响应式设计（Media Queries）

```css
/* 当视口宽度 ≤ 768px 时生效 */
@media (max-width: 768px) {
    body {
        font-size: 14px;
    }
    .container {
        flex-direction: column;
    }
}

/* 同时限定宽度范围 */
@media (min-width: 769px) and (max-width: 1200px) { }
```

常用断点：

· 手机：≤ 768px
· 平板：769px ~ 1024px
· 桌面：≥ 1025px

---

1️⃣2️⃣ 过渡与动画

过渡（transition）

```css
.button {
    background-color: blue;
    transition: background-color 0.3s ease;
}
.button:hover {
    background-color: red;
}
```

关键帧动画

```css
@keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
}

.element {
    animation: fadeIn 1s infinite alternate;
}
```

---

1️⃣3️⃣ CSS 变量（自定义属性）

```css
:root {
    --primary-color: #3498db;
    --spacing: 8px;
}

.button {
    background-color: var(--primary-color);
    margin: var(--spacing);
}
```

---

1️⃣4️⃣ 常用单位总结

单位 相对对象
px 屏幕像素（绝对）
% 父元素的相同属性
em 当前元素的字体大小
rem 根元素（<html>）的字体大小
vw/vh 视口宽度的1%/高度的1%
fr Grid 中的剩余空间比例

✅ 推荐：全局用 rem，布局用 % 或 flex/grid，视口单位用于全屏元素。

---

1️⃣5️⃣ BFC（块级格式化上下文）

触发 BFC 的方式：

· overflow: auto/hidden
· display: flex / grid / inline-block
· position: absolute/fixed

作用：

· 清除浮动
· 避免外边距重叠
· 包含浮动子元素

---

✨ 学习建议

1. 使用浏览器开发者工具（F12）实时调试 CSS
2. 多练习布局：复制常见组件（导航栏、卡片、表单）
3. 学习 Flexbox 和 Grid 的互动小游戏（Flexbox Froggy, Grid Garden）
4. 遵循 BEM 命名规范（Block__Element--Modifier）

---
