# 正则表达式 RegExp

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

# JS 错误处理机制
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

# JS 事件

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
