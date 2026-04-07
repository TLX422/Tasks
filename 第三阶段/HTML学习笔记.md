# 📘 HTML 学习笔记

## 1️⃣ 什么是 HTML？

- **HTML** 是超文本标记语言（HyperText Markup Language）
- 用于描述网页的结构和内容
- 文件后缀通常为 `.html` 或 `.htm`
<img width="652" height="429" alt="屏幕截图 2026-04-07 225622" src="https://github.com/user-attachments/assets/f5f90744-4b18-4ca0-a57c-95c57a4bce49" />
---

## 2️⃣ 最基本的 HTML 文档结构
>来自[菜鸟教程][https://www.runoob.com/html/html-intro.html]
<img width="1329" height="649" alt="屏幕截图 2026-04-07 225111" src="https://github.com/user-attachments/assets/0e61e46c-fa70-411d-9e42-e6135182f69f" />


```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
<body>
    <h1>这是一个标题</h1>
    <p>这是一个段落。</p >
</body>
</html>
```

>结构说明
<img width="1223" height="717" alt="屏幕截图 2026-04-07 225432" src="https://github.com/user-attachments/assets/b07cf559-9d0d-4cfb-b142-58188925e2c2" />
```
· <!DOCTYPE html> ：声明文档类型为 HTML5
· <html> ：根标签
· <head> ：存放元数据（标题、字符集、样式等）
· <body> ：页面可见内容
```

---

3️⃣ 常用标签速查

📝 文本标签
```
· 标题：<h1> ~ <h6>
· 段落：<p>
· 换行：<br>（自闭合）
· 水平线：<hr>
· 加粗：<strong> 或 <b>
· 斜体：<em> 或 <i>
```
🔗 链接与图片
```
· 链接：<a href=" ">文字</a >
· 新窗口打开：target="_blank"
· 图片：< img src="图片路径" alt="替代文字">
```
📃 列表

 **无序列表**

```html
<ul>
    <li>苹果</li>
    <li>香蕉</li>
</ul>
```

**有序列表**

```html
<ol>
    <li>第一步</li>
    <li>第二步</li>
</ol>
```

📊 表格

```html
<table border="1">
    <tr>
        <th>姓名</th>
        <th>成绩</th>
    </tr>
    <tr>
        <td>张三</td>
        <td>95</td>
    </tr>
</table>
```

📋 表单

```html
<form action="/submit" method="post">
    <label>用户名：</label>
    <input type="text" name="username">
    <br>
    <label>密码：</label>
    <input type="password" name="pwd">
    <br>
    <input type="submit" value="登录">
</form>
```

---

4️⃣ 块级元素 vs 行内元素
```
类型 特点 常见标签
块级元素 独占一行，可设置宽高 <div>、<p>、<h1>、<ul>、<table>
行内元素 不换行，宽度由内容决定 <span>、<a>、<strong>、<img>
行内块元素 不换行但可设宽高 <input>、<button>
```
---

5️⃣ HTML5 语义化标签
```
标签 含义
<header> 页眉
<nav> 导航
<main> 主体内容
<article> 独立文章
<section> 章节
<aside> 侧边栏
<footer> 页脚
```
---

6️⃣ 常用转义字符（实体）
```
显示 实体名
< &lt;
> &gt;
& &amp;
" &quot;
空格 &nbsp;
```
---

7️⃣ 注释

```html
<!-- 这是注释，不会显示在页面上 -->
```
***学习笔记手写**
![HTML笔记](https://github.com/user-attachments/assets/099ba1c9-07bc-4587-ae95-2325facaab77)

---

