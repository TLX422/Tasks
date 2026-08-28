# document.write() 为什么现代开发不推荐

`document.write()` 是非常古老的 DOM API，属于 DOM Level 0，浏览器兼容极好，但**现代项目几乎禁止使用**。

## 一、document.write() 的主要问题

### 1. 执行时机严重依赖文档解析状态，行为诡异

`document.write()` 的效果取决于**文档是否解析完成**。
1）**页面还在解析（HTML流未读完）**：直接把文本/HTML写入当前解析位置，追加到页面。

```
<body>
  <script>
    document.write("<p>Hello</p>")
  </script>
</body>
```

此时正常输出。

2）**文档已经解析完毕（DOMContentLoaded之后、onload之后）再调用 `document.write()`**

> 
> **会隐式调用 `document.open()`，清空整个当前页面文档，重写一个全新空白页面！**
> 页面所有 HTML、CSS、DOM、JS 全部清空，只剩你 write 的内容。

```
window.onload = ()=>{
  document.write('<h1>全部页面被清空了！</h1>')
}
```

这是最臭名昭著的坑，一不小心把整个页面搞没。

### 2. 会阻塞 HTML 解析、阻塞页面渲染

`document.write()` 写入脚本时，浏览器会停下HTML解析，等待脚本下载、执行，**造成解析阻塞，影响首屏性能**。
早年经常用它加载第三方脚本，现在被性能规范标记为不好的实践。

### 3. 和异步代码、模块化完全不搭

- 回调、定时器、Promise、`fetch` 里面调用 `document.write`，此时文档大概率已经关闭，直接清空页面。

```
setTimeout(()=>{
  document.write("<div>test</div>") // 定时器延迟执行 → 页面直接清空
},1000)
```

> 
> 异步逻辑中几乎不能安全使用它。

### 4. 不操作DOM树，和现代DOM体系割裂

`document.write` 输出字符串到 HTML 字节流，**不是操作DOM节点**。
写出来的元素，你无法拿到它 DOM 对象；无法配合 `appendChild`、事件委托、Vue/React框架。
框架环境下用 `document.write` 会直接破坏虚拟DOM。

### 5. 存在XSS安全隐患

`document.write(用户输入内容)`，会直接把字符串解析为HTML标签；如果输入包含 `<script>`，就会执行恶意脚本。

> 
> 补充：浏览器已经对部分 `document.write` 场景做降级限制，例如Chrome在某些条件下会忽略 `document.write` 写入的脚本。

---

## 二、需求：必须动态插入内容，现代该怎么做？

分4种场景：**插入纯文本、插入HTML片段、插入完整DOM节点、动态加载脚本**

### 场景1：插入纯文本（优先，防XSS）

✅ `element.textContent`

```
const box = document.querySelector("#box");
box.textContent = "这里是纯文本内容，<script>不会被解析执行";
```

### 场景2：插入HTML片段（可信HTML才可以用，不可信不要用）

✅ `element.innerHTML`

```
box.innerHTML = `<h2>标题</h2><p>段落</p>`
```

> 
> 注意：innerHTML 同样解析HTML，**不要直接放用户输入内容，会XSS**。

> 
> 区别：
> 
> 
> - `document.write`：写进文档流；时机不对直接清页面
> - `innerHTML`：修改某个DOM节点内部，**永远不会清空整个文档**，安全可控。

### 场景3：创建真实DOM节点（最规范，适合复杂组件）

`document.createElement` + `append()` / `prepend()`

```
const div = document.createElement('div');
div.textContent = "内容";
div.classList.add("demo");
box.append(div);
```

批量渲染大量节点用 **`DocumentFragment`**，减少页面重排回流：

```
const frag = document.createDocumentFragment();
for(let i=0;i<100;i++){
  const p = document.createElement('p');
  p.textContent = `第${i}条`;
  frag.append(p);
}
box.append(frag); //一次性挂载
```

### 场景4：模板复用，HTML写在template标签

```
<template id="tpl">
  <div class="card">
    <h3></h3>
  </div>
</template>
```

```
const tpl = document.querySelector("#tpl");
const card = tpl.content.cloneNode(true);
card.querySelector('h3').textContent = "标题";
box.append(card);
```

