# E36 Web
[菜鸟教程：ES6教程](https://www.runoob.com/w3cnote/es6-tutorial.html)

## 一、HTML5

### 1.语义化标签

| 标签 | 作用 |
| --- | --- |
| `<header>` | 页面头部 |
| `<nav>` | 导航栏 |
| `<main>` | 页面主体（唯一） |
| `<article>` | 独立完整内容，文章、帖子 |
| `<section>` | 区块分组 |
| `<aside>` | 侧边栏、附属内容 |
| `<footer>` | 页脚 |

✅好处：

1. 代码可读性高，方便团队阅读维护
2. 利于SEO搜索引擎抓取
3. 屏幕阅读器无障碍设备识别页面结构

❌误区：语义标签不自带样式，和div一样都是盒子，只是语义含义不同。

### 2.form表单

- `<label for="id">`：点击文字自动选中表单控件，for绑定input的id

```
<label for="username">用户名</label>
<input type="text" id="username">
```

- input常用type：`text password radio checkbox file submit reset button`
- select下拉框、textarea多行文本域

### 3.H5新增特性

1. 本地存储

- `localStorage`：永久存储，手动删除才消失，同源下所有页面共享
- `sessionStorage`：会话存储，关闭浏览器标签页直接清空> 
> 两者都只能存字符串，存对象需要`JSON.stringify()`读取`JSON.parse()`

2. 自定义属性 `data-xxx`

```
<div data-id="100"></div>
//js获取：dataset.id
```

3. video音频视频、canvas画布

### 4.路径

- `./` 当前目录，可以省略
- `../` 返回上一级目录
- 绝对路径：完整http网址

---

## 二、CSS3

### 1.选择器

1. 基础选择器：标签、类、id、通配符`*`
2. 复合选择器

- 后代选择器 `div p` 所有后代
- 子代选择器 `div>p` 只直接子元素
- 兄弟选择器 `div+p` 紧邻下一个兄弟；`div~p`后面所有兄弟
3.伪类选择器
`hover鼠标悬浮 focus获得焦点 nth-child()`
4.伪元素 `::before ::after`> 
> 必须加content:""；属于行内元素；不会出现在DOM树

### 2.CSS三大特性

1. **层叠性**：同一个元素相同样式，后面的覆盖前面；不同样式全部生效
2. **继承性**> 
> 文字相关属性可以继承：color font font-size line-height text‑align
> ❗a标签不会继承color；盒子宽高、margin、padding、border不会继承
3. **优先级（权重）**
`!important > 行内样式style > id选择器 > 类/伪类/伪元素 > 标签选择器 > *通配符`> 
> 权重不会进位，10个类选择器也打不过1个id选择器

### 3.盒模型

1.标准盒模型（w3c）
`width = content内容宽度`；padding、border向外撑开盒子
2.怪异盒模型
`box-sizing:border-box;`
width包含 content + padding + border，不会撑大盒子

### 4.浮动 float

- `float:left/right`，元素脱离普通文档流，不再占据原来位置
- 问题：父盒子高度塌陷（子元素浮动，父盒子高度变成0）
✅清除浮动4种方案
1.父盒子设置 `overflow:hidden`
2.伪元素清除法（企业最常用）

```
.clearfix::after{
  content:"";
  display:block;
  clear:both;
}
```

3.额外空标签加clear:both
4.父盒子设置高度

> 
> 浮动目的：做横向排列布局，现在优先使用flex

### 5.position定位

| 取值 | 特性 |
| --- | --- |
| static | 默认，普通文档流，top/left无效 |
| relative相对定位 | 不脱离文档流；位置参照自己原来位置；保留原来位置 |
| absolute绝对定位 | 脱离文档流；参照最近已经定位的父元素；没有则参照浏览器窗口 |
| fixed固定定位 | 脱离文档流；参照浏览器视口；滚动页面位置不动 |
| sticky粘性定位 | 滚动到阈值变成固定，其余正常文档流 |

> 
> 定位之后可以用z-index控制层级；**只有定位元素z-index生效**

### 6.Flex弹性布局（高频）

开启：父盒子 `display:flex;`

> 
> 父容器属性

1. `flex‑direction`：主轴方向 row/column
2. `justify‑content`：主轴对齐方式 `flex‑center center space‑between space‑around space‑evenly`
3. `align‑items`：侧轴单行对齐
4. `flex‑wrap:wrap` 子元素超出父容器自动换行
5. `align‑content`：多行侧轴对齐

> 
> 子项属性

1. `flex-grow`：剩余空间分配比例，默认0不放大
2. `flex‑shrink`：空间不足收缩比例，默认1收缩
3. `flex‑basis`：子项基础尺寸
4. `flex:1` 简写：`flex‑grow:1;shrink:1;basis:0%`
5. `order`：排序，数字越小越靠前，默认0
6. `align‑self`：单独修改某一个子项侧轴对齐，覆盖父align‑items

### 7.Grid网格布局

`display:grid;`二维布局

- `grid‑template‑columns` 设置每一列宽度
- `gap`行列间隙
- `grid‑area` 合并单元格

### 8.过渡、动画、转换

1.过渡 `transition: 属性 时间 曲线 延迟`，实现状态变化平滑，需要触发条件hover等
2.2D转换 transform
`translate()位移 scale缩放 rotate旋转 skew倾斜`
3.动画@keyframes

```
@keyframes move{
  0%{}
  100%{}
}
animation: move 2s infinite alternate;
```

###9.移动端适配
1.vw/vh：视口单位，1vw=视口宽度1%
2.rem：相对根字体大小
3.媒体查询`@media (max-width:750px){}`

---

## 三、JavaScript基础

###1.变量 var let const
1.var：函数作用域，存在变量提升，可以重复声明，没有块级作用域
2.let：块级作用域，不能重复声明，不存在变量提升，暂时性死区
3.const：常量，块级作用域，声明必须赋值；简单类型不能修改；对象可以修改属性，不能重新赋值

> 
> 块：{} if for while大括号内部

###2.数据类型
简单数据类型（栈）
`number string boolean null undefined symbol`
复杂数据类型（堆）
`对象Object 数组Array 函数Function`

> 
> null 和undefined区别：null人为手动置空；undefined声明变量未赋值

###3.运算符
`===`严格相等：值和类型全部相等；`==`会做隐式类型转换

逻辑短路：
`a && b`：a为真返回b；a假返回a
`a || b`：a真返回a；a假返回b

###4.数组方法
✅改变原数组：
`push末尾添加 pop末尾删除 shift头部删除 unshift头部添加 splice删除/替换 sort排序 reverse反转`

✅返回新数组（不修改原数组）
`map映射 filter过滤 reduce累加 find查找元素 findIndex找索引 every全部满足 some至少一个满足 concat拼接 slice截取`

###5.对象

- `.`点语法、`[]`括号语法，[]可以写变量
- `for(let k in obj)`遍历对象，k得到属性名

###6.函数
1.函数声明 `function fn(){}`
2.函数表达式 `const fn=function(){}`
3.箭头函数 `const fn=()=>{}`

> 
> 箭头函数特点：
> ①没有this，继承外层作用域this
> ②没有arguments
> ③不能new做构造函数
> ④没有原型prototype

---

## 四、WebAPI DOM+BOM

### DOM文档对象模型：操作页面标签

1.获取元素

```
document.querySelector("选择器") //获取第一个
document.querySelectorAll("选择器") //获取全部，伪数组
document.getElementById("id")
```

2.操作内容

- `innerText` 获取设置纯文本，不识别html标签
- `innerHTML` 获取设置内容，可以识别html标签
3.操作属性
- `对象.属性` 操作内置属性
- `setAttribute("属性","值") getAttribute()`操作自定义属性
- `classList.add() remove() toggle()`操作类名，推荐，不会覆盖其他类

4.节点操作

- `document.createElement('div')` 创建节点
- `父.appendChild(子)` 末尾追加
- `父.removeChild(子)` 删除子节点

### 事件

绑定事件：`dom.addEventListener('click',function(e){})`

> 
> 事件三要素：事件源、事件类型、事件处理函数

**事件流：捕获阶段 →目标阶段 →冒泡阶段**
1.捕获：从window一层一层向内到目标元素
2.目标：触发点击的元素
3.冒泡：从目标向外一层一层传播到window

```
e.stopPropagation() //阻止冒泡
e.preventDefault() //阻止默认行为（a跳转、表单提交）
```

`e.target`真正触发事件的元素；`e.currentTarget`绑定事件的元素

#### ✨事件委托（事件代理）

原理：利用事件冒泡，给父元素绑定事件，代理所有子元素
好处：减少事件绑定，新动态生成的子元素也可以拥有事件

```
ul.addEventListener('click',function(e){
  if(e.target.tagName==='LI'){
    console.log('点击li')
  }
})
```

### BOM浏览器对象模型

1.window 浏览器全局对象，所有全局变量函数属于window
定时器

```
setTimeout(回调,毫秒) //延时执行一次
setInterval(回调,毫秒) //循环定时器
clearTimeout() clearInterval()清除定时器
```

2.location对象
`location.href` 获取设置浏览器地址；`location.search`获取url查询参数
3.history：浏览器前进后退历史记录
4.navigator.userAgent 获取浏览器设备信息

---

## 五、JS高级（面试重点）

###1.作用域、作用域链

- 全局作用域：整个script
- 函数作用域：函数内部
- 块级作用域：`let/const`在{}产生

作用域链：查找变量，先在当前作用域找，找不到向外层查找，直到全局。

###2.闭包

> 
> 定义：函数嵌套，内部函数访问外部函数的变量，内部函数被外部使用，就形成闭包。

```
function outer(){
  let num=10
  return function inner(){
    console.log(num)
  }
}
let f=outer()
f()
```

✅作用：保存变量，延长变量生命周期
❌缺点：变量不会释放，容易内存泄漏

###3.this指向
1.普通函数直接调用：`this → window`
2.对象方法调用：`this指向调用方法的对象`
3.new构造函数调用：`this指向new出来的实例对象`
4.call apply bind手动改变this指向

### call apply bind

1.`fn.call(thisArg,参数1,参数2)`：立即执行函数，参数逐个传
2.`fn.apply(thisArg,[数组])`：立即执行，参数数组传递
3.`fn.bind(thisArg,参数)`：返回新函数，**不会立刻执行**，后续调用才执行

### new关键字执行四步（必考）

1.创建一个全新空JS对象
2.将构造函数内部this指向这个空对象
3.执行构造函数函数体，给空对象添加属性方法
4.如果构造函数没有手动return对象，自动返回这个新对象

### 严格模式 `'use strict'`
写在脚本开头或者函数内部
1.变量必须声明，不能直接赋值未定义变量
2.普通函数调用this不再指向window，变成undefined
3.禁止函数参数重名
4.禁止使用with等语法

### 正则表达式

```
const reg=/a/g
reg.test('字符串') //返回布尔，检测是否匹配
'abc'.match(reg) //捕获匹配内容
```

修饰符：`g全局匹配 i忽略大小写`
元字符：
`\b单词边界 ^开头 $结尾 *任意次数(0次以上) +至少1次 ?0或者1次`

### 原型&原型链

- `prototype`：构造函数的原型对象，存放公共方法
- `__proto__`：实例身上属性，指向构造函数prototype> 
> 对象查找属性：对象自身→`__proto__`原型对象→原型对象的`__proto__`，直到null，这个链条就是原型链

---

## 六、ES6+
1.解构赋值：对象解构、数组解构

```
const {name,age}=obj
const [a,b]=arr
```

2.展开运算符`...`复制数组、对象
3.模板字符串 `\`hello ${变量}\``，支持换行插值
4.class类，extends继承
5.Promise处理异步，解决回调地狱
`.then成功回调 .catch捕获异常 .finally无论成功失败都执行`
`async await` 把异步写成同步的写法，await只能写在async函数内部

6.模块化
导出：`export`；导入：`import`

---

## 七、AJAX & JSON & HTTP
1.AJAX：Asynchronous JavaScript And XML，异步局部刷新页面，不用刷新整个网页
原生XMLHttpRequest，实际开发用axios库
2.GET和POST

- get：参数拼接url，参数大小有限，用于获取数据
- post：请求体传参，用于提交数据，参数放请求体
3.JSON
json字符串和js对象转换
`JSON.parse(json字符串) → JS对象`
`JSON.stringify(js对象) → json字符串`> 
> json格式要求：键名必须双引号，不能写注释，不能写undefined函数

4.HTTP状态码
200成功；404地址找不到；401未授权；403禁止访问；500服务器内部错误

5.同源策略：浏览器安全策略，协议、域名、端口全部一致才同源，不同源产生跨域
解决跨域：后端CORS

---

## 八、工程化 npm & git
### npm
1.`package.json`项目描述文件，记录项目依赖、脚本命令

- `dependencies`生产依赖：项目上线也要用
- `devDependencies`开发依赖：仅开发阶段使用，上线不需要
2.`package-lock.json`锁定版本，保证所有人安装版本完全一致
3.npm/yarn/pnpm区别
pnpm速度快，磁盘占用少；yarn早期解决npm版本混乱；npm官方自带
4.切换淘宝阿里镜像源

### git
四个区域：工作区 →暂存区 →本地仓库 →远程仓库
常用命令

```
git add . 加入暂存
git commit -m"提交信息" 本地提交
git push 推送到远程
git pull拉取远程更新
git clone 克隆远程仓库
```

## 九、Vue3组合式API
1.单文件组件`.vue`三部分：`<template>`模板、`<script>`脚本、`<style>`样式
2.响应式
`ref`：简单数据类型；`.value`修改值；模板中不用写.value
`reactive`：对象数组类型
3.计算属性`computed`：根据已有数据推导新数据，有缓存，依赖不变不会重复执行
4.侦听器`watch`：监听数据变化，变化之后执行业务逻辑
5.指令
`v‑for循环渲染 v‑if条件销毁 v‑show控制display显示隐藏 v‑bind(:)绑定属性 v‑on(@)绑定事件`
6.组件通信
父传子：子组件props接收
子传父：子组件`emit('自定义事件',数据)`，父组件监听事件接收
7.vue-router路由实现页面跳转
8.pinia新一代状态管理，替代vuex

## 十、浏览器底层原理
### 1.浏览器渲染流程
1.解析HTML，生成DOM树
2.解析CSS，生成CSSOM样式树
3.DOM+CSSOM合成渲染树（只包含可见元素）
4.Layout布局：计算每个盒子大小位置
5.Paint绘制：填充颜色、图片
6.Composite图层合成

### 2.EventLoop事件循环
JS单线程，处理异步任务

> 
> 任务分类

- 微任务Promise.then await、queueMicrotask
- 宏任务script整体代码、setTimeout setInterval ajax
执行顺序：
1.执行同步代码
2.同步执行完毕，清空所有微任务
3.执行一个宏任务
4.再次清空全部微任务，循环往复

### 3.事件流
捕获阶段→目标阶段→冒泡阶段
