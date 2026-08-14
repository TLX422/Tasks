# JavaScript 笔记
---

# 一、JavaScript 函数系统（核心重点 ⭐）

>[CSDNJS基础函数](https://blog.csdn.net/m0_74399244/article/details/140186796)

### 1. ⭐自定义函数（函数声明）

<img width="451" height="501" alt="屏幕截图 2026-08-14 234130" src="https://github.com/user-attachments/assets/c5436ac1-dfea-4b64-8b6f-515c03914abe" />

>return后面不能再添加任何代码，不能执行
```
// 语法
function 函数名(参数列表) {
  // 函数体
  return 返回值;
}

//示例
function sayHello(name) {
  return "你好：" + name;
}
//调用
sayHello("小明");
```
<img width="477" height="464" alt="屏幕截图 2026-08-14 232908" src="https://github.com/user-attachments/assets/3a18ade3-b161-4aed-827a-03360e7d0c47" />

✅ 特点：**函数提升**，可以先调用，后定义。

### 2. 函数表达式（匿名函数）

```
let fn = function() {
  console.log("函数表达式");
};
fn();
```

❌ 不存在提升，必须先定义再调用。

### 3. 箭头函数 ES6

```
let add = (a,b)=>{
  return a + b;
}
//简写：只有一行return可以省略{}和return
let add = (a,b)=> a+b;
```

### 4. 构造函数方式（极少使用）

```
let fn = new Function("a","b","return a+b");
```

## 2. 函数四种调用方式
### 1. ⭐全局直接调用（普通调用）

```
function test(){
  console.log(this); // window（浏览器）
}
test();
```

> 
> `this` → 全局对象 window

### 2. ⭐方法调用（函数作为对象方法）

```
let obj = {
  name:"张三",
  fn:function(){
    console.log(this); // this === obj
  }
};
obj.fn();
```

> 
> `this` 指向调用方法的对象

### 3. ⭐call /apply 绑定调用（改变 this 指向）

作用：**手动指定函数内 this 是谁**

```
function show(age){
  console.log(this.name, age);
}
let p = {name:"李四"};

// call：参数逐个传递
show.call(p, 18);

// apply：参数放在数组内传递
show.apply(p, [18]);
```

区分：

- `call(obj, 参数1,参数2)`
- `apply(obj, [参数1,参数2])`

### 4. 构造函数调用 new

```
function Person(name){
  this.name = name;
}
let p1 = new Person("王五");
```

new 执行四步：

1. 创建空新对象
2. 对象绑定为函数 this
3. 执行函数体
4. 默认返回这个新对象
## 二、return 返回值

1. `return` 终止函数执行
2. 可以返回任意数据类型（数字、对象、函数）
3. 不写 return，函数默认返回 `undefined`

```
function getNum(){
  return 100;
}
let res = getNum();
```
# 三、闭包 ⭐
## 1. 闭包定义
**内层函数访问外层函数的变量，并且内层函数被外部使用，形成闭包**

## 2. 闭包形成三个条件
1. 函数嵌套
2. 内层引用外层变量
3. 内层函数被外部调用

## 3. 闭包特点
- 让**局部变量常驻内存，不会销毁**
- 可以实现**私有变量**，外部无法直接修改

## 4. 闭包优点
- 延长变量生命周期
- 保护变量私有化

## 5. 闭包缺点
- **容易内存泄漏**，占用内存不释放

## 6. 闭包经典案例
```js
function outer() {
  let num = 10;
  return function inner() {
    console.log(num);
  };
}
let res = outer();
res(); 
```

---

# 四、作用域 &amp; 作用域链 ⭐必考难点
## 1. 作用域
**变量的可访问范围**，JS分为两种：

### 全局作用域
- 整个页面都能访问
- 页面关闭才销毁

### 局部作用域（函数作用域）
- 函数内部生效
- 函数执行完毕，变量销毁

## 2. 作用域链
**内层可以访问外层变量，外层不能访问内层变量**

变量查找规则：
1. **先在当前作用域找**
2. 找不到 → 向外层父作用域找
3. 一直找到全局作用域
4. 找不到 → 报错 `is not defined`

> 作用域链本质：**层层嵌套的变量查找机制**

---



# 五、正则表达式 RegExp
## 1. 作用
匹配、校验、替换、截取字符串（手机号、账号、密码、邮箱）

## 2. 创建方式
```js
// 字面量
let reg = /\d+/;

// 构造函数
let reg2 = new RegExp("\\d+");
```

## 3. 常用元字符
- `\d` 数字
- `\D` 非数字
- `\w` 字母数字下划线
- `\s` 空格
- `^` 开头
- `$` 结尾
- `+` 至少1次
- `*` 任意次数
- `?` 0或1次

## 4. 常用方法
```js
reg.test("内容") // 校验返回布尔值
str.match(reg)   // 匹配内容
str.replace(reg,"") // 替换
```

---

# 五、JS 错误处理机制
防止代码报错卡死整个页面

```js
try {
  // 可能出错的代码
} catch (err) {
  // 捕获错误信息
  console.log(err);
} finally {
  // 无论对错一定执行
}
```

---

# 六、JS 事件
## 1. 事件三要素
1. 事件源（谁触发）
2. 事件类型（什么动作）
3. 事件处理函数（触发后做什么）

## 2. 常用事件
- 鼠标：`click`、`mouseenter`、`mouseleave`
- 键盘：`keydown`、`keyup`
- 表单：`input`、`change`、`submit`
- 页面：`scroll`、`resize`、`load`

## 3. 事件绑定
```js
dom.addEventListener("click", function(){})
```

---

# 七、严格模式 use strict
## 开启方式
```js
"use strict";
```

## 严格模式作用
1. **变量必须声明才能使用**（杜绝全局变量污染）
2. 禁止函数 this 指向 window
3. 禁止重复参数
4. 禁止不合理语法

---

# 八、JSON 数据格式
## 特点
- 键名**必须双引号**
- 不能存函数、undefined

## 两个核心转换
```js
// JS对象 → JSON字符串（传给后端）
JSON.stringify(obj)

// JSON字符串 → JS对象（后端数据渲染）
JSON.parse(jsonStr)
```

---

# 九、⭐ DOM API 文档对象模型
## 1. 作用
操作网页：**增、删、改、查**页面元素

## 2. 获取元素
```js
document.getElementById("id")
document.getElementsByClassName("box")
document.querySelector(".box") // 推荐！
document.querySelectorAll(".box")
```

## 3. 常用操作
- 内容：`innerText`、`innerHTML`
- 属性：`src`、`href`、`value`
- 样式：`style.xxx`
- 节点：`createElement`、`appendChild`、`removeChild`

## 4. 节点操作流程
创建 → 设置属性 → 追加页面

---

# 十、性能优化：防抖 &amp; 节流 ⭐
## 1. 防抖 Debounce
**停止触发后，延迟一段时间执行一次**

适用场景：
- 搜索框输入联想
- 窗口缩放
- 输入框监听

核心：**多次触发，只执行最后一次**

## 2. 节流 Throttle
**固定时间内只执行一次**

适用场景：
- 页面滚动
- 高频点击
- 拖拽移动

核心：**频繁触发，匀速执行**

### 记忆口诀
**防抖停了才执行，节流一直匀速跑**

---

# 十一、Ajax 异步请求
## 作用
**局部刷新**，不刷新页面请求后端数据

## 原生 Ajax 四步
1. 创建 XMLHttpRequest 对象
2. open(请求方式, 地址)
3. send() 发送请求
4. onreadystatechange 监听返回

```js
let xhr = new XMLHttpRequest();
xhr.open("GET","接口地址");
xhr.send();
xhr.onreadystatechange = function(){
  if(xhr.readyState === 4 && xhr.status === 200){
    console.log(xhr.responseText);
  }
}
```

---

# 十二、ES6 核心语法
## 1. let / const
- `let`：块级作用域、可修改、不允许变量提升
- `const`：常量、不可修改、必须初始化

解决 var 的问题：
- 变量提升
- 没有块级作用域
- 可以重复声明

## 2. 箭头函数
```js
let fn = (a,b) =&gt; a+b;
```
特点：
- 没有自己 this
- 不能 new
- 没有 arguments

---

# 十三、⭐ 异步编程：Promise + async / await
## 1. Promise
解决**回调地狱**，让异步代码扁平化

三种状态：
1. pending 等待
2. fulfilled 成功
3. rejected 失败

```js
new Promise((resolve,reject)=&gt;{
  // 异步操作
  resolve("成功数据");
}).then(res=&gt;{
  console.log(res);
})
```

## 2. async / await ⭐终极异步方案
**Promise 语法糖，异步代码同步写法**

```js
async function getData(){
  let res = await 异步请求;
  console.log(res);
}
```
- async 修饰函数
- await 等待 Promise 结束

---

# 十四、Web 端 JS 调试技巧
1. `console.log()` 打印输出
2. 浏览器 Sources 断点调试
3. `debugger;` 强制暂停代码
4. 控制台查看作用域、this、变量变化

---

# 十五、前端 JS 性能优化
1. 防抖节流减少高频事件执行
2. 缓存 DOM 节点，避免频繁获取元素
3. 避免滥用闭包，防止内存泄漏
4. 减少全局变量，避免全局污染
5. 大量操作 DOM 使用文档碎片
6. 合理使用异步，避免阻塞主线程

---

# 十六、整体知识体系总结
函数四种调用 → this指向 → call/apply  
作用域 → 作用域链 → 闭包  
正则 → 错误处理 → 事件机制  
严格模式 → JSON数据交互  
DOM页面操作 → 防抖节流性能优化  
Ajax异步请求 → ES6语法  
Promise/async-await 异步终极方案  
Web调试 + 前端性能优化

