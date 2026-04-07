# HTML 学习笔记
## 1. 什么是 HTML？
- **HTML** 是超文本标记语言（HyperText Markup Language）
- 用于描述网页的结构和内容
- 文件后缀通常为 `.html` 或 `.htm`

## 2. 最基本的 HTML 文档结构

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

**结构说明**
```
 <!DOCTYPE html> ：声明文档类型为 HTML5
 <html> ：根标签
 <head> ：存放元数据（标题、字符集、样式等）
 <body> ：页面可见内容
```
## 3. 常用标签速查

### 3.1 文本标签
```
· 标题：<h1> ~ <h6>
· 段落：<p>
· 换行：<br>（自闭合）
· 水平线：<hr>
· 加粗：<strong> 或 <b>
· 斜体：<em> 或 <i>
```

### 3.2 链接与图片
```
· 链接：<a href=" ">文字</a >
· 新窗口打开：target="_blank"
· 图片：< img src="图片路径" alt="替代文字">
```
### 3.3 列表

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

### 3.4 表格

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

### 3.5 表单

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
## 4. 块级元素 vs 行内元素
```
· 块级元素：独占一行，可设置宽高，例如 <div>、<p>、<h1>、<ul>、<table>
· 行内元素：不换行，宽度由内容决定，例如 <span>、<a>、<strong>、<img>
· 行内块元素：不换行但可设宽高，例如 <input>、<button>
```
---
## 5. HTML5 语义化标签
```
· <header> ：页眉
· <nav> ：导航
· <main> ：主体内容
· <article> ：独立文章
· <section> ：章节
· <aside> ：侧边栏
· <footer> ：页脚

```

## 6. 常用转义字符（实体）
```
显示 实体名
< &lt;
> &gt;
& &amp;
" &quot;
空格 &nbsp;
```
## 7. 注释

```html
<!-- 这是注释，不会显示在页面上 -->
```
