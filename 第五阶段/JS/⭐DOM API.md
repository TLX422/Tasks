# DOM API笔记

## 1. DOM是什么

**DOM：Document Object Model 文档对象模型**
浏览器把 HTML 页面，解析成一个**树形对象**，JS 通过 DOM API 操作这个树，从而修改页面。

- `document` 是整个网页的根对象，JS操作页面入口。
- HTML标签 → DOM节点对象；属性、文本也是节点。> 
> 通俗理解：HTML是写出来的文本，DOM是浏览器内存里的“页面副本对象”，JS改DOM，浏览器页面就跟着变。

DOM树结构：
`document` → html → head / body → 各种标签元素

## 2. 获取元素（查询DOM）

### 2.1 常用获取元素API

```
// 1. id获取，返回单个元素
let box = document.getElementById("box")

// 2. class类名获取，返回HTMLCollection集合（动态集合）
let items = document.getElementsByClassName("item")

// 3. 标签名获取
let divs = document.getElementsByTagName("div")

// 4. css选择器（最常用！）
// querySelector 返回【第一个匹配】的元素，没有返回null
let one = document.querySelector(".list li")

// querySelectorAll 返回所有匹配，NodeList静态集合
let allLi = document.querySelectorAll(".list li")
```

> 
> ⚠️重点区分

- `getElementsByClassName`：**动态集合**，DOM变化集合自动跟着变
- `querySelectorAll`：**静态NodeList**，获取完之后DOM改变，集合不会更新

### 2.2 获取/修改元素内容

```
let el = document.querySelector("#demo")

// innerHTML：读写html内容，可以识别标签
el.innerHTML = "<b>你好</b>"  

// innerText：读写纯文本，标签直接忽略，只显示文字
el.innerText = "<b>你好</b>" 

// textContent：纯文本，性能比innerText好，不会处理css样式
el.textContent
```

> 
> innerHTML风险：容易XSS注入，不要直接把用户输入直接赋值innerHTML。

### 2.3 获取设置元素属性

#### 方式1：`.属性名`（标准属性）

```
let img = document.querySelector("img")
img.src = "images/a.jpg"
img.title = "图片"
img.id = "pic1"
```

#### 方式2：getAttribute / setAttribute / removeAttribute

适合自定义属性

```
//读取属性
el.getAttribute("data-id")
//设置属性
el.setAttribute("data-id","1001")
//删除属性
el.removeAttribute("data-id")
```

**data‑* 自定义属性（dataset）⭐**
html: `<div data‑name="小魔仙" data‑age="14"></div>`

```
let div = document.querySelector("div")
console.log(div.dataset.name) //小魔仙
div.dataset.age = 15 //修改
```

### 2.4 操作样式

```
//行内样式操作 .style
let box = document.querySelector(".box")
box.style.width = "200px"
box.style.backgroundColor = "#f40"
//注意：css横杠属性转为小驼峰 background‑color → backgroundColor
```

> 
> `.style` 只能读取**行内样式**，读不到css文件写的样式。

读取计算后的全部样式（包含css样式）

```
let styleObj = getComputedStyle(box)
console.log(styleObj.width)
```

class操作（推荐，不要一个个改style）

```
let div = document.querySelector(".box")
div.classList.add("active")    //增加类
div.classList.remove("active") //删除类
div.classList.toggle("active") //有就删，没有就加（切换）
div.classList.contains("active") //判断是否存在该类，返回布尔
```

## 3. DOM节点关系（父子兄弟）

页面每个标签都是节点对象

```
let parent = document.querySelector(".parent")

// 子节点（包含文本、换行、注释节点，不只是标签！）
parent.childNodes  

// 只拿元素标签节点（重点）
parent.children

// 父元素
childEle.parentElement

// 上一个兄弟元素
ele.previousElementSibling
//下一个兄弟元素
ele.nextElementSibling

//第一个子元素
parent.firstElementChild
//最后一个子元素
parent.lastElementChild
```

> 
> `childNodes` 会拿到空白换行文本节点，**开发尽量用 Element 系列（children、previousElementSibling）只拿标签**。

## 4. 创建、增加、删除、替换节点⭐

```
//1. 创建元素节点
let newDiv = document.createElement("div")
newDiv.innerText = "新的div"

//2. 添加到父元素末尾
parent.appendChild(newDiv)

//3. 在某个参考节点前面插入
parent.insertBefore(newDiv, referenceNode)

//4. 删除节点
parent.removeChild(childNode)
//现代简写：直接调用元素自己remove()
childNode.remove()

//5. 替换节点
parent.replaceChild(newNode, oldNode)

//6. 克隆节点
// true：深克隆，复制里面所有子节点；false只复制外层标签
let cloneEle = oldEle.cloneNode(true)
```

> 
> 注意：一个DOM节点只能在页面出现一次；appendChild 如果节点已经在页面，会**移动节点，不是复制**，想要复制必须 cloneNode。

## 5. DOM事件

### 5.1 三种绑定事件方式

1. html行间：`<div onclick="fn()"></div>` 不推荐
2. onxxx属性绑定（同一个事件只能绑定一个函数，后面覆盖前面）

```
box.onclick = function(){
  console.log("点击")
}
box.onclick = null //解绑
```

3. addEventListener 标准DOM2事件绑定 ✅项目用这个

```
// 事件名不加on，第三个参数 false冒泡 / true捕获
box.addEventListener("click",function(e){
  console.log("点击")
},false)

//解绑事件，必须具名函数
function handleClick(){ }
box.addEventListener("click", handleClick)
box.removeEventListener("click",handleClick)
```

### 5.2 事件对象 event

触发事件浏览器自动传入事件对象e

```
box.addEventListener("click",function(e){
  e.target   //真正触发事件的元素（实际点击的那个）
  e.currentTarget //绑定事件的元素
  e.preventDefault() //阻止默认行为（a跳转、form提交）
  e.stopPropagation() //阻止事件冒泡
})
```

### 5.3 事件冒泡 & 事件捕获

- **冒泡（默认）**：事件从最里面被点击元素向外一层一层向外传递。子→父→祖先。
- **捕获**：从最外层向内传递。父→子。

> 
> 事件委托（事件代理）⭐面试高频
> 原理：利用**事件冒泡**，把多个子元素事件绑定给父元素，不用循环给每一个子元素绑定。
> 适合：动态新增的标签，新增后不用重新绑定事件。

```
<ul id="list">
  <li>1</li>
  <li>2</li>
</ul>
```

```
let ul = document.querySelector("#list")
ul.addEventListener("click",function(e){
  //判断点击目标是不是li
  if(e.target.tagName === "LI"){
    console.log("点击li",e.target.innerText)
  }
})
```

## 6. 表单DOM操作

```
let input = document.querySelector("#username")
//获取输入框值
console.log(input.value)
//赋值
input.value = "默认文字"

//单选框复选框 .checked
let radio = document.querySelector("#r1")
console.log(radio.checked) //布尔 true/false

//select下拉框
select.value //拿到选中值
```

## 7. 尺寸、滚动相关DOM API

### 元素自身大小

- `clientWidth / clientHeight`：内容+内边距，**不含边框滚动条**
- `offsetWidth / offsetHeight`：内容+padding+边框，包含滚动条
- `scrollWidth / scrollHeight`：内容实际总大小（内容溢出时比盒子大）

### 偏移位置

- `offsetLeft / offsetTop`：距离**定位父级**的距离

### 页面滚动

```
//页面滚动距离
window.scrollY
window.scrollX

//滚动到指定位置
window.scrollTo(0,200)
```

### 监听滚动事件

```
window.addEventListener("scroll",()=>{
  console.log(window.scrollY)
})
```

## 8.文档加载顺序大坑

```
<body>
<!-- 脚本写在head里面，此时下面html还没解析 -->
<script>
// 此时#box还没生成，获取得到null！
let box = document.querySelector("#box")
</script>
<div id="box"></div>
</body>
```

**解决办法三种：**

1. script标签放到body末尾（最常用）
2. 用 `DOMContentLoaded` 事件，等DOM全部解析完成执行代码

```
document.addEventListener("DOMContentLoaded",function(){
  //在这里写获取DOM的代码
})
```

3. 使用 defer 属性：`<script defer src="xxx.js"></script>`，脚本延迟到DOM解析完执行。

> 
> 区分：

- `DOMContentLoaded`：DOM树构建完成，图片、样式还没加载完
- `load`：页面所有资源（图片、css全部加载完毕）



## 开发常见坑

1. JS写在head，直接获取DOM得到null，忘记等DOM加载完成。
2. `childNodes`拿到换行空白节点，混淆元素节点和普通节点。
3. appendChild移动原有DOM，不是复制，忘记cloneNode。
4. addEventListener解绑必须传入同一个函数引用，匿名函数无法解绑。
5. `.style`只能读行内样式，读不到css样式，要用getComputedStyle。

如果你需要，我可以给你出几道DOM练习题。
