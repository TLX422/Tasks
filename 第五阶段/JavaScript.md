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
## ①
`call()` 是函数的方法，用来**改变函数里 this 的指向**，并且立刻执行函数。

>把f2的this指向了f3的name，所以显示的小白

><img width="465" height="303" alt="屏幕截图 2026-08-15 192511" src="https://github.com/user-attachments/assets/a3abe792-46d8-43ed-a5ff-477d3e3354c0" />
---
<img width="669" height="249" alt="屏幕截图 2026-08-15 192658" src="https://github.com/user-attachments/assets/ec84dcd4-1794-48bc-b653-9e7d84ff2d82" />


## 语法

```
函数.call(thisArg, 参数1, 参数2, 参数3...)
```

- `thisArg`：函数内部 `this` 指向谁
- 后面是一个个传入的参数，逗号隔开
- **call 会马上调用函数**

## 基础例子

```
let person1 = {
  name:"小蓝"
}
let person2 = {
  name:"小粉"
}

function sayHi(a,b){
  console.log(this.name, a, b)
}

sayHi("11","22") 
// this指向window，输出：  11 22

sayHi.call(person1,"你好","哈哈") 
// this → person1，输出：小蓝 你好 哈哈

sayHi.call(person2,"hi","ok")
// this → person2，输出：小粉 hi ok
```

## 核心作用 1：借用别的对象的方法（最常用）

```
let obj1 = {
  name:"小明",
  show(){
    console.log(this.name)
  }
}

let obj2 = {
  name:"小红"
}

// obj2自己没有show方法，借用obj1的show
obj1.show.call(obj2) 
//输出：小红
```

## 核心作用 2：伪数组借用数组方法

类数组没有数组的 `slice`，用 call 借来用

```
function fn(){
  // arguments是伪数组，没有slice方法
  let arr = Array.prototype.slice.call(arguments)
  console.log(arr)
}
fn(10,20,30)
```

## call vs apply 区别

- `call(this, arg1,arg2)` 参数一个个传
- `apply(this, [arg1,arg2])` 参数放数组里面

```
fn.call(obj,1,2,3)
fn.apply(obj,[1,2,3])
```
## ②
`pply()` 和 `call()` 几乎一模一样：**修改函数内部 this，并且立刻执行函数**
**唯一区别：传参格式不一样**

## 语法

```
函数.apply(thisArg, [参数1,参数2])
```

- 第一个参数：`thisArg`，设置函数里面 `this` 指向谁
- **第二个参数必须是数组 / 伪数组**，数组里面的元素当作函数的实参

> 
> call：参数一个个分开写
> apply：参数放在一个数组里面

## 示例对比 call 和 apply

```
function sum(a,b){
  console.log(this.num, a + b)
}
let obj = { num: 100 }

// call 传参：逗号隔开
sum.call(obj, 10, 20)  

// apply 传参：数组包裹
sum.apply(obj, [10, 20]) 
```
### 4. 构造函数调用 new

**构造函数首字母大写，普通函数小写**。
```
function Person(name){
  this.name = name;
}
let p1 = new Person("王五");
```

new 执行四步：

1. **创建一个空的全新普通对象** `{}`
2. **把这个空对象，赋值给函数内部的 `this`**
3. **执行构造函数里面的代码**（给 this 添加属性、方法）
4. **如果函数没有手动 return 对象，自动返回这个新对象**

# 不写 new，调用构造函数 `F()`，会发生什么

完整代码：

```
function F(){
  this.name = '安安'
}

// 👉 没有 new！普通函数调用
let y = F()
console.log(y)      
console.log(window.name)
```

## 1、4 个关键点

1. **不会自动创建新对象**，没有凭空出来的 `{}`
2. **函数里面的 `this` 不再是实例！**
非严格模式下，`this` 指向浏览器全局对象 **`window`**
3. 执行 `this.name='安安'` → 等价于 `window.name = '安安'`
👉 **污染全局 window，全局多出一个 name 变量**
4. 函数没有写 `return`，所以返回值是 `undefined`

输出结果：

```
console.log(y) // undefined，函数没有返回东西
console.log(window.name) // "安安"，挂载到全局window上了
```

---

## 对比：有 new 的时候

```
let y = new F()
```

1. new 自动新建空对象
2. 函数内部 `this` = 这个新建对象
3. `this.name='安安'` 给新对象增加属性，**不会碰 window**
4. 自动把新对象返回给 y

```
console.log(y.name) // 安安
console.log(window.name) // 不受影响
```

## 严格模式下 'use strict' 的情况

```
'use strict'
function F(){
  this.name = '安安'
}
F() //没有new直接调用
```

严格模式普通函数调用，`this = undefined`
执行 `this.name='安安'` → **直接报错！**
## return 在构造函数里面的特殊规则

1. 如果 `return` **对象类型**（对象、数组）：new 返回你 return 的对象
2. 如果 `return` **基本类型**（数字、字符串、boolean）：忽略，依旧返回新建的 this 实例
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

<img width="509" height="286" alt="屏幕截图 2026-08-15 214706" src="https://github.com/user-attachments/assets/ac1be25a-9dab-4362-935b-dc4dd4dd43a4" />

**内层函数访问外层函数的变量，并且内层函数被外部使用，形成闭包**

## 2. 闭包形成三个条件
1. 函数嵌套
2. 内层引用外层变量
3. 内层函数被外部调用

## 3. 闭包特点
- 让**局部变量常驻内存，不会销毁**
- 可以实现**私有变量**，外部无法直接修改
><img width="630" height="329" alt="屏幕截图 2026-08-15 215645" src="https://github.com/user-attachments/assets/6c3347c9-f712-4694-a69d-fd409ccea5a0" />
  

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

<img width="612" height="494" alt="屏幕截图 2026-08-15 162517" src="https://github.com/user-attachments/assets/feca8376-a9fc-4815-9501-f9fdd85071bc" />


### 全局作用域
- 整个页面都能访问
- 页面关闭才销毁

### 局部作用域（函数作用域）
- 函数内部生效
- 函数执行完毕，变量销毁

## 2. 作用域链
**内层可以访问外层变量，外层不能访问内层变量**


><img width="460" height="370" alt="屏幕截图 2026-08-15 162744" src="https://github.com/user-attachments/assets/a58450ef-e08c-48b9-9619-1a9e7ee64f10" />


变量查找规则：
1. **先在当前作用域找**
2. 找不到 → 向外层父作用域找
3. 一直找到全局作用域
4. 找不到 → 报错 `is not defined`

> 作用域链本质：**层层嵌套的变量查找机制**

---



# 五、正则表达式 RegExp

>网站：[菜鸟教程：正则表达式](https://www.runoob.com/js/js-regexp.html)
>
## 1. 什么是正则

正则（RegExp），用来**匹配、查找、替换字符串**，表单校验（手机号、邮箱）、提取字符、过滤内容经常用。

### 两种创建写法

```
// 字面量 /pattern/修饰符  ⭐常用
let reg1 = /abc/

// new RegExp 构造函数
let reg2 = new RegExp("abc")
```

## 2. 修饰符（写在斜杠后面）

表格

| 修饰符 | 作用 |
| --- | --- |
| `i` | ignoreCase 忽略大小写 |
| `g` | global 全局匹配，找全部，不是只找第一个 |
| `m` | multiline 多行匹配 |

示例：

```
let str = "Abc abc ABC"
let reg = /abc/gi
```
### 例子：找出数字
>- `[0-9]`：匹配**任意单个数字（0~9）**
- `+`：量词，**匹配至少 1 次（1 次或多次连续数字）**

```
document.write(str.match(patt1));
```

- `str.match(正则)`：字符串方法，**查找匹配正则的内容**
- `document.write()`：把结果输出显示在网页上
>
><img width="473" height="168" alt="屏幕截图 2026-08-15 230538" src="https://github.com/user-attachments/assets/12164fbc-2f5f-4482-8031-515e745ab50b" />


## 3. 元字符（核心符号）

### 预定义类

表格

| 符号 | 含义 |
| --- | --- |
| `\d` | 数字 等价 `[0‑9]` |
| `\D` | 非数字 |
| `\w` | 字母、数字、下划线 `[A‑Za‑z0‑9_]` |
| `\W` | 非单词字符 |
| `\s` | 空白（空格、换行、tab） |
| `\S` | 非空白字符 |
| `.` | 任意字符（**除换行**） |
|`\b|单词边界|

>例子
>
><img width="830" height="387" alt="屏幕截图 2026-08-15 223449" src="https://github.com/user-attachments/assets/51cac34d-d588-4e75-b5b5-4f45010d8e07" />


### 边界符

- `^` 开头
- `$` 结尾

>例子：只会匹配行首的a
>
><img width="374" height="350" alt="屏幕截图 2026-08-15 223606" src="https://github.com/user-attachments/assets/c5ca2115-13a3-4c8d-9f2d-277f40b2779e" />

---
> ✅表单校验必须加 `^ $`，代表**整串完全匹配**

```
// 只能是6位数字
let reg = /^\d{6}$/
```

## 4. 量词（控制出现多少次）

表格

| 符号 | 说明 |
| --- | --- |
| `{n}` | 恰好 n 次 |
| `{n,}` | 至少 n 次 |
| `{n,m}` | n~m 次 |
| `+` | 至少 1 次，等价 `{1,}` |
| `*` | 0 次或多次 |
| `?` | 0 次或 1 次 |

```
/\d{11}/   //11位数字，手机号基础
```
## 关于？
>表示可以只出现一次或者不出现 **可有可无**
>
><img width="347" height="249" alt="屏幕截图 2026-08-15 220444" src="https://github.com/user-attachments/assets/3791f3ae-a2a3-499f-aea9-6abd12dc56da" />
---
## 关于*：可以匹配多个
>**a与c之间只能出现b**
>
><img width="425" height="337" alt="屏幕截图 2026-08-15 221413" src="https://github.com/user-attachments/assets/6f7c4533-34f2-434c-aa1b-cfb43219f381" />

## 关于+：至少出现一次
>可以用{}来限定出现几次，{2}出现两次，{2，6}次数为2~6，{2，}为两次以上
>
><img width="539" height="413" alt="屏幕截图 2026-08-15 221755" src="https://github.com/user-attachments/assets/fc6bed09-6628-4fdc-8c06-0d21576a0ce3" />
---
>可以匹配多个单词的出现
>
><img width="433" height="461" alt="屏幕截图 2026-08-15 222150" src="https://github.com/user-attachments/assets/129140c2-3384-409c-adba-2c66b13825f1" />

## 或运算符
>首先匹配a，然后bb或者cc（**格式为a 空格 （bb|cc**)
>
><img width="400" height="336" alt="屏幕截图 2026-08-15 222513" src="https://github.com/user-attachments/assets/2071a3e7-9be6-47c9-934a-b8fea786cb19" />


## 5. 字符集 `[]`

```
[abc]      //a或者b或者c
[0‑9]      //数字
[a‑z]      //小写字母
[A‑Z]      //大写
[^abc]     //^在[]里面代表取反，就是除了abc以外的字符，不是开头
```
>例子
>
><img width="530" height="440" alt="屏幕截图 2026-08-15 223141" src="https://github.com/user-attachments/assets/770c1bd9-5b9f-4f57-898f-d9ed46526403" />

## 6. 或 `|` 和分组 `()`

- `|` 或者
- `()` 分组，提取内容

```
// abc 或者 abd
let r = /abc|abd/
```

## 7. 正则常用方法

### ① `test()` 返回布尔值⭐最常用


> 
> 检测字符串是否匹配，true /false，表单校验必用

```
let reg = /^\d{11}$/
let phone = "13800138000"
console.log(reg.test(phone)) // true
```

### ② `exec()` 查找匹配内容，返回数组 /null

```
let str = "a1b2c3"
let reg = /\d/g
console.log(reg.exec(str))
```

### 字符串方法使用正则

1. `str.match(reg)` 获取匹配结果
2. `str.replace(reg,"新内容")` 替换

```
let s = "hello world"
let res = s.replace(/l/g,"*")
console.log(res) //he**o wor*d
```

## 8. 简单实战案例

### 案例 1：手机号正则

```
// 1开头，第二位3‑9，后面9位数字，总共11位
let phoneReg = /^1[3‑9]\d{9}$/
console.log(phoneReg.test("13912345678"))
```

### 案例 2：密码 6‑16 位字母数字

```
let pwdReg = /^[0‑9A‑Za‑z]{6,16}$/
```

## 9.贪婪与懒惰匹配
>贪婪变懒惰：.是任意字符，+是至少出现一次，？是出现一次或者0次
>
><img width="547" height="261" alt="屏幕截图 2026-08-15 224204" src="https://github.com/user-attachments/assets/d56640f5-0574-4a18-a62d-99fabd150ba8" />

## 10. 常见坑

1. 不加 `^ $`：只要字符串包含片段就返回 true，校验表单会出错

```
let reg = /\d{11}/
reg.test("aaa13800138000bbb") //true！明明不是手机号，却通过
```

> 
> 表单校验**一定要加上开头 ^ 和结尾 $**

2. 忘记`g`，只会匹配第一个

---

# 五、JS 错误处理机制
## 1. 常见错误类型

表格

| 错误类型 | 说明 | 产生例子 |
| --- | --- | --- |
| `SyntaxError` 语法错误 | 代码写错语法，解析直接失败 | 少写分号、括号不配对 |
| `ReferenceError` 引用错误 | 使用**未定义的变量** | `console.log(a)`，a 没有声明 |
| `TypeError` 类型错误 | 数据类型不对，调用不存在方法 | `123.run()` 数字调用不存在函数 |
| `RangeError` 范围错误 | 数值超出合法范围 | 递归死循环、数组长度设置负数 |
| `URIError` | URL 处理函数参数非法 | `decodeURIComponent('%')` |

> 
> 💡 语法错误 `SyntaxError`：代码直接不运行！其他错误代码会执行到报错行才炸。

## 2. try‑catch‑finally 捕获错误⭐核心语法
>[菜鸟教程：错误](https://www.runoob.com/js/js-errors.html)
>
><img width="664" height="252" alt="屏幕截图 2026-08-15 234826" src="https://github.com/user-attachments/assets/e42da16f-ffe7-4199-992b-b0bb20937f9e" />

```
try {
    // 【有可能出错的代码放这里】
    let num = 10;
    num.run(); // 这里会报TypeError
} catch (err) {
    // ✅ 如果try里面出错，就进入catch，不会让整个程序崩溃
    console.log("捕获到错误：", err);
    console.log(err.name);   // 错误类型名字：TypeError
    console.log(err.message); // 错误文字描述
} finally {
    // 无论是否报错，这里**一定会执行**，可选，可以不写
    console.log("必定执行");
}
```

- `try`：尝试执行风险代码
- `catch(err)`：捕获异常，`err` 是错误对象
- `finally`：不管报错与否，一定运行，常用于关闭资源

> 
> ⚠注意：**try‑catch 抓不到异步代码（setTimeout）里面的错误**

```
try{
  setTimeout(()=>{ a.b() },100)
}catch(e){
  // ❗这里捕获不到定时器内部报错！异步代码要在定时器内部写try‑catch
}
```

## 3. 手动抛出错误 throw

自己主动制造错误，抛出异常对象

```
throw new Error("输入的数据不合法！");
```

示例完整：

```
let age = -5;
if(age <0){
  throw new RangeError("年龄不能是负数");
}
```

## 4. Error 对象自带属性

- `err.name`：错误类型名字 `TypeError` / `ReferenceError`
- `err.message`：错误的说明文字
- `err.stack`：调用栈（调试看报错在哪一行）

## 5. 全局捕获（浏览器）

页面任何 JS 未被捕获的错误，都会触发

```
window.onerror = function(msg,url,line){
  console.log('全局捕获错误',msg,line);
  return true; // 阻止控制台红色报错输出
}
```

## 6. 常见易错考点总结

1. `SyntaxError` 语法错，整个脚本直接罢工，**try‑catch 捕获不到语法错误**（代码解析阶段就失败，还没运行到 try）
2. `try‑catch` 只能捕获同步代码；异步回调内部错误，要在回调内部包裹
3. `throw` 可以抛出任意值，规范建议抛出 `new Error()` 对象，不要直接 throw 字符串
4. `finally` 不管 try 成功还是报错，都会执行；即使里面有 return，finally 依旧执行

---

# 六、JS 事件

> 
> **事件：网页上发生的动作。**
> 比如：鼠标点击、鼠标移动、按下键盘、页面加载、输入框输入文字。
> JS 可以监听这些动作，一旦事件发生，就执行写好的代码。

## 三种绑定事件方式

### 方式 1：行内写在 HTML 标签（不推荐）
>
><img width="612" height="262" alt="屏幕截图 2026-08-16 001731" src="https://github.com/user-attachments/assets/43add789-3219-41a1-b784-dd070d6c469a" />


```
<button onclick="alert('你点击按钮')">点我</button>
```

`onclick`：点击事件，鼠标单击就运行引号里面 JS 代码。
缺点：HTML 和 JS 混在一起，不好维护。

### 方式 2：DOM 对象 onXXX 属性（0 级事件）
>
><img width="613" height="283" alt="屏幕截图 2026-08-16 001816" src="https://github.com/user-attachments/assets/f1d8e5de-ddf8-49a5-9f6f-9c75d9c4a9eb" />

>`getElementById('demo')` → 找到 id 为 demo 的标签

```
<button id="btn">点我</button>
<script>
const btn = document.getElementById('btn');
btn.onclick = function(){
  alert("按钮被点击");
}
</script>
```

特点：

- 同一个元素同一个事件**只能绑定一个函数**

```
btn.onclick = function(){ console.log(1) }
btn.onclick = function(){ console.log(2) }
// 只会输出2！后面的直接覆盖前面
```

### 方式 3：`addEventListener()` 【⭐推荐，标准 DOM2 事件】
>
><img width="592" height="272" alt="屏幕截图 2026-08-16 002319" src="https://github.com/user-attachments/assets/5caace37-c298-4617-8145-f1a2317e6bd2" />


```
btn.addEventListener('click', function(){
  alert("点击触发");
})
```

优点：

1. 同一个事件可以绑定**多个函数，不会覆盖**

```
btn.addEventListener('click',()=>console.log(1))
btn.addEventListener('click',()=>console.log(2))
//点击会输出1，再输出2
```

2. 可以控制捕获 / 冒泡阶段

语法：

```
元素.addEventListener('事件名',回调函数,可选参数)
```

> 
> ⚠注意：这里事件名**不带 on**！写`click`，不是`onclick`

---

## 常用事件列表

表格

| 事件名称 | 触发时机 |
| --- | --- |
| `click` | 鼠标单击 |
| `dblclick` | 鼠标双击 |
| `mouseover` | 鼠标移入元素 |
| `mouseout` | 鼠标移出元素 |
| `mousemove` | 鼠标在元素上面移动（高频触发，防抖节流就是针对它） |
| `keydown` | 键盘按下按键 |
| `keyup` | 键盘松开按键 |
| `input` | 输入框内容发生变化 |
| `submit` | 表单提交事件 |
| `load` | 页面 / 图片加载完成 |

>例子
>
><img width="603" height="362" alt="屏幕截图 2026-08-16 003604" src="https://github.com/user-attachments/assets/d3e49594-e253-428b-8e4c-1c026e353152" />

## 事件对象 event
>
><img width="556" height="268" alt="屏幕截图 2026-08-16 004718" src="https://github.com/user-attachments/assets/54e3ddae-4862-4ae4-959d-cd11f8a9782f" />

回调函数里面可以接收 `event`（事件对象），保存这次事件全部信息。
### 关于target：可以获取事件节点
>
><img width="548" height="269" alt="屏幕截图 2026-08-16 005405" src="https://github.com/user-attachments/assets/a61d68f5-fdd6-4f7a-b5bb-e47da79d6c6b" />


><img width="668" height="133" alt="屏幕截图 2026-08-16 005419" src="https://github.com/user-attachments/assets/cda7d39b-eb3a-47ea-9250-2d23632f3e82" />
---
>可以利用target修改文本用innerHTML
>
><img width="533" height="175" alt="屏幕截图 2026-08-16 005648" src="https://github.com/user-attachments/assets/4df8312d-3a62-44dd-8af1-4f0e378f473a" />

### 关于type：可以获取事件类型
>
><img width="518" height="255" alt="屏幕截图 2026-08-16 005841" src="https://github.com/user-attachments/assets/92fc0845-db86-4529-a668-3021161a55a4" />

>
><img width="616" height="186" alt="屏幕截图 2026-08-16 005859" src="https://github.com/user-attachments/assets/c3f54794-7e11-4f93-ac47-b719984253fe" />


```
btn.addEventListener('click',function(e){
  // e就是事件对象event
  console.log(e.target); // e.target：真正触发事件的元素
  console.log(e.clientX,e.clientY); //鼠标点击坐标
})
```

## 事件冒泡

> 
> 当子元素触发事件，事件会一层一层向上传给父元素、祖先元素。
> 就像水泡从水底往上冒。

```
<div id="father">
  <button id="son">按钮</button>
</div>
```

给父 div、子按钮都绑定 click。**点击按钮，按钮触发，接着父 div 也会触发！**

阻止冒泡：

```
e.stopPropagation();
```

## 阻止默认行为

有些标签自带默认动作：

- a 标签点击跳转页面
- form 表单 submit 提交刷新页面

`e.preventDefault()` 取消浏览器自带默认行为

```
a.addEventListener('click',function(e){
  e.preventDefault(); //点击a标签，不会跳转网页
})
```

## 事件委托（事件代理）⭐实战高频

原理：利用**事件冒泡**，不给很多子元素绑定事件，只给父元素绑定一次。
好处：后期 JS 动态新增的子元素，不用重新绑定事件！

示例：ul 里面很多 li，点击 li 做操作

```
<ul id="ulBox">
  <li>选项1</li>
  <li>选项2</li>
</ul>
```

```
// 只给父ul绑定事件
document.querySelector("#ulBox").addEventListener('click',function(e){
  if(e.target.tagName === 'LI'){
    console.log("你点击了li：",e.target.innerText)
  }
})
```

## 简单对比记忆

1. `onclick`：会覆盖，写在 DOM 对象上，事件名带 on
2. `addEventListener('click',fn)`：不会覆盖，事件名不带 on，推荐使用
3. `e.stopPropagation()`：阻止冒泡，不让事件往上跑
4. `e.preventDefault()`：阻止浏览器默认动作
5. 事件委托：利用冒泡，父代理所有子，适合动态生成的元素

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

