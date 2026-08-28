

## 一、现有代码里使用的DOM API梳理


>
><img width="587" height="103" alt="image" src="https://github.com/user-attachments/assets/b495d2fc-ab83-48c2-af63-c1718025a6da" />
>
>
><img width="587" height="103" alt="image" src="https://github.com/user-attachments/assets/b7df3ee9-2a6a-49ba-a258-41b107f39d2c" />


```
document.createElement()       // 创建元素
document.createTextNode()      // 创建文本节点
element.setAttribute()         // 设置标签属性
element.style.xxx = ...        // 设置行内样式
element.textContent            // 设置文本内容
element.innerHTML              // 注入style样式字符串
node.appendChild()              // 添加子节点
document.head.appendChild()
document.body.append()         // 现代append，支持多节点
element.remove()               // 直接移除元素
element.onclick = fn           // 绑定DOM事件
document.getElementById()      // 获取元素
```

### 现有写法小问题

1. 自定义`el()`工具内部混用 `setAttribute`；**布尔属性（`disabled`）直接用`setAttribute`不如直接操作DOM属性更可靠**。
2. 循环批量生成角色卡片，每生成一张没有做内存片段缓冲，中间多次DOM对象操作（好在最后一次性append到body，没有频繁回流）。
3. 样式直接大段塞进 `style.textContent` 可行；也有其他方案。
4. 事件用`onclick`赋值，简单够用，但不支持多事件监听。

> 
> 优点：整体已经做得不错，**所有节点在内存组装完毕，最后一次性挂到body，不会频繁触发页面重排回流**。

---

## 二、更现代、更规范的替代方案

### 1. 元素添加：`appendChild` vs `append` / `prepend`

- `appendChild(node)`：只能传单个DOM节点，不支持字符串，返回追加的节点，老浏览器兼容。
- ✅现代：`parent.append(node1, node2, "文本")`，支持多个节点、文本直接传入，无返回值，**推荐优先使用**。
- `prepend()` 加到最开头。

### 2. 属性设置：区分 HTML‑Attribute 和 DOM‑Property

❌不好：`node.setAttribute('disabled', true)`
✅更好：`node.disabled = true`（表单布尔属性直接操作对象属性，`checked`/`selected`同理）。

> 
> `setAttribute`适合设置HTML属性如`class`、`alt`、`src`；表单状态布尔属性直接点属性。

### 3. 批量渲染大量节点：`DocumentFragment` 文档片段

> 
> 现在代码：所有组件内存组装好，最后一次性 `body.append(...)`，已经规避频繁重排。
> 如果是循环渲染大量列表，进一步可以用`DocumentFragment`，**完全不触发页面回流，直到fragment整体append进真实DOM**。

示例：

```
const frag = document.createDocumentFragment();
roles.forEach(r => {
  const card = el('div',{class:'role-card'},[...]);
  frag.append(card);
})
roleWrap.append(frag); // 一次性全部挂载
```

### 4. 事件绑定：从 `xxx.onclick = fn` → `addEventListener`

```
//旧
magicBtn.onclick = async function(){...}

//✅现代，支持叠加多个事件，可removeEventListener解绑
magicBtn.addEventListener('click', async ()=>{
  //逻辑
})
```

### 5. 模板方案：`<template>`标签（把HTML写在HTML内，JS克隆）

现在全部DOM由JS字符串/JS函数创建；
现代原生可以用`<template>`写静态HTML模板，JS中`cloneNode(true)`克隆使用，**HTML与JS分离，可读性更高**。

```
<template id="roleCardTpl">
  <div class="role-card">
    <img alt="">
    <h3></h3>
    <p></p>
    <span class="tag"></span>
  </div>
</template>
```

```
const tpl = document.querySelector('#roleCardTpl');
roles.forEach(r=>{
  const card = tpl.content.cloneNode(true);
  card.querySelector('h3').textContent = r.name;
  card.querySelector('img').src = r.img;
  //填充数据，append
})
```

### 6. 样式注入其他方案

现在：`style.textContent = "大段css字符串"`，完全没问题。
备选：

1. CSS单独外置`<link href="xxx.css">`，业务JS只操作DOM；
2. `element.classList.add/remove/toggle` 代替操作className，不要用`setAttribute('class','xxx')`。

### 7. 文本：优先 textContent，尽量少 innerHTML

- `textContent`：只设置纯文本，不会解析HTML，天然防XSS，优先用。
- `innerHTML`：解析HTML字符串，有XSS风险，**只在可信静态模板使用，绝对不要直接塞用户输入**。

### 8. 删除节点

旧：`parent.removeChild(child)`
✅现代：`child.remove()`，不需要父节点引用，更简洁。

---



