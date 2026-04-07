# 🚀 JavaScript 学习笔记

## 1️⃣ 什么是 JavaScript？

- JavaScript（简称 JS）是一种轻量级的解释型或即时编译型脚本语言
- 运行在浏览器中，为网页添加交互行为（动态效果、数据请求、用户响应等）
- 也可在服务端运行（如 Node.js）
- 遵循 ECMAScript 标准（ES6、ES7 等是版本迭代）

---

## 2️⃣ 三种引入方式
```
方式 语法 位置
行内 <button onclick="alert('Hi')">点击</button> 不推荐
内部 <script> console.log('Hello'); </script> 一般放在 </body> 前
外部 <script src="app.js"></script> 推荐，利于维护和缓存
```
📌 最佳实践：将 <script> 放在页面底部，或使用 defer / async 属性。

---

## 3️⃣ 基础语法

**变量声明**

```javascript
var a = 1;       // 旧方式，函数作用域，可重复声明（不推荐）
let b = 2;       // 块级作用域，推荐
const c = 3;     // 常量，不可重新赋值
```

**数据类型**
```
类型 示例 说明
Number 42, 3.14, NaN, Infinity 整数与浮点数
String "hello", 'world',  `模板`  字符串
Boolean true, false 布尔值
Undefined undefined 声明未赋值
Null null 空值（手动设置）
Symbol Symbol('id') 唯一标识（ES6）
BigInt 9007199254740991n 大整数
Object { name: 'Tom' }, [1,2,3], function(){} 引用类型
```
**类型检查**

```javascript
typeof 42;            // "number"
typeof "hi";          // "string"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object"  （历史遗留 bug）
typeof [1,2];         // "object"
typeof function(){};  // "function"
```

**运算符**

```javascript
// 算术
+ - * / % **
// 赋值
= += -= *= /=
// 比较（注意 == 与 === 的区别）
==   // 值相等（会类型转换）
===  // 值和类型都相等（推荐）
!=   !==
// 逻辑
&& || !
// 三元
condition ? expr1 : expr2;
// 可选链（ES2020）
obj?.prop?.subprop;
// 空值合并（ES2020）
value ?? '默认值';   // 只有 null/undefined 时才取默认值
```

---

## 4️⃣ 流程控制

>条件语句

```javascript
if (score >= 60) {
    console.log('及格');
} else if (score >= 80) {
    console.log('良好');
} else {
    console.log('不及格');
}

// switch
switch (day) {
    case 1: console.log('周一'); break;
    case 2: console.log('周二'); break;
    default: console.log('其他');
}
```

>循环

```javascript
// for
for (let i = 0; i < 5; i++) { }

// for...of（遍历可迭代对象：数组、字符串等）
for (let val of arr) { }

// for...in（遍历对象属性，不推荐用于数组）
for (let key in obj) { }

// while / do...while
while (condition) { }
do { } while (condition);
```

---

## 5️⃣ 函数

>函数声明与表达式

```javascript
// 声明式（提升）
function add(a, b) {
    return a + b;
}

// 函数表达式（赋值给变量）
const subtract = function(a, b) {
    return a - b;
};

// 箭头函数（ES6）
const multiply = (a, b) => a * b;
const greet = name => `Hello ${name}`;   // 单个参数可省略括号
const log = () => console.log('Hi');     // 无参数写 ()
```

> 默认参数、剩余参数

```javascript
function greet(name = 'Guest') { }
function sum(...numbers) {   // 收集剩余参数为数组
    return numbers.reduce((a,b) => a+b, 0);
}
```

> 闭包

```javascript
function outer() {
    let count = 0;
    return function inner() {
        count++;
        return count;
    };
}
const counter = outer();
counter(); // 1
counter(); // 2
```

---

## 6️⃣ 数组（Array）

**常用方法**
```
方法 作用 是否改变原数组
push(elem) 尾部添加 ✅
pop() 尾部删除并返回 ✅
unshift(elem) 头部添加 ✅
shift() 头部删除并返回 ✅
concat(arr2) 合并数组 ❌
slice(start, end) 截取部分 ❌
splice(start, deleteCount, ...items) 删除/替换/添加 ✅
map(fn) 映射为新数组 ❌
filter(fn) 筛选 ❌
reduce(fn, init) 累计计算 ❌
forEach(fn) 遍历 ❌
find(fn) 返回第一个匹配元素 ❌
some(fn) / every(fn) 测试是否有/所有满足条件 ❌
includes(value) 是否包含 ❌
```
---
```javascript
const arr = [1,2,3];
const doubled = arr.map(x => x * 2);   // [2,4,6]
const evens = arr.filter(x => x % 2 === 0); // [2]
const sum = arr.reduce((acc, cur) => acc + cur, 0); // 6
```

---

## 7️⃣ 对象（Object）

**创建与访问**

```javascript
// 字面量
const person = {
    name: 'Alice',
    age: 25,
    sayHi() {   // 方法简写
        console.log(`Hi, I'm ${this.name}`);
    }
};

// 属性访问
person.name;        // "Alice"
person['age'];      // 25

// 动态属性名
const key = 'score';
person[key] = 100;
```

>对象常用操作

```javascript
// 复制/合并
const copy = { ...person };           // 浅拷贝
const merged = { ...obj1, ...obj2 };

// 获取键/值/条目
Object.keys(obj);     // 返回键数组
Object.values(obj);   // 返回值数组
Object.entries(obj);  // 返回 [key,value] 数组

// 删除属性
delete person.age;
```

>解构赋值

```javascript
// 数组解构
const [a, b] = [1, 2];   // a=1, b=2

// 对象解构
const { name, age } = person;
// 重命名 + 默认值
const { name: fullName, gender = 'unknown' } = person;

// 函数参数解构
function print({ name, age }) { }
```

---

## 8️⃣ 类（Class，ES6 语法糖）

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} makes a sound.`);
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name);   // 调用父类构造
        this.breed = breed;
    }
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog('Buddy', 'Golden');
dog.speak();   // Buddy barks.
```

---

## 9️⃣ 异步编程

>回调函数

```javascript
fs.readFile('a.txt', (err, data) => {
    if (err) throw err;
    fs.readFile('b.txt', (err2, data2) => { /* 嵌套 */ });
});
```

**Promise**

```javascript
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => {
        Math.random() > 0.5 ? resolve('成功') : reject('失败');
    }, 1000);
});

fetchData
    .then(result => console.log(result))
    .catch(error => console.error(error))
    .finally(() => console.log('完成'));
```

**静态 Promise 方法**

```javascript
Promise.all([p1, p2])       // 全部成功才成功
Promise.race([p1, p2])      // 最快的一个决定结果
Promise.allSettled([...])   // 等待所有完成（无论成败）
Promise.resolve(42)
Promise.reject('err')
```

async/await（ES2017）

```javascript
async function getData() {
    try {
        const result = await fetchData();   // 等待 Promise resolve
        console.log(result);
    } catch (error) {
        console.error(error);
    }
}
// 注意：await 只能在 async 函数内部使用（顶层 await 需模块支持）
```

---

## 🔟 DOM 操作（Document Object Model）

>选择元素

```javascript
// 单个元素
document.getElementById('id');
document.querySelector('.class');

// 集合
document.getElementsByClassName('class');   // HTMLCollection
document.getElementsByTagName('div');
document.querySelectorAll('.item');         // NodeList（可 forEach）
```

修改内容与属性

```javascript
// 文本与 HTML
element.textContent = '新文本';
element.innerHTML = '<strong>加粗</strong>';

// 属性
element.setAttribute('src', 'image.jpg');
element.getAttribute('src');
element.removeAttribute('disabled');

// 样式（内联）
element.style.color = 'red';
element.style.backgroundColor = '#f0f0f0';
element.classList.add('active');
element.classList.remove('hidden');
element.classList.toggle('visible');
```

>创建与删除元素

```javascript
const div = document.createElement('div');
div.textContent = 'Hello';
parent.appendChild(div);
parent.insertBefore(div, referenceChild);
parent.removeChild(child);
element.remove();  // 现代方法
```

>事件监听

```javascript
const btn = document.querySelector('button');
btn.addEventListener('click', (event) => {
    console.log(event.target);   // 触发元素
    event.preventDefault();      // 阻止默认行为
    event.stopPropagation();     // 阻止冒泡
});

// 常见事件：click, mouseenter, keydown, submit, load, scroll
```

>事件委托（性能优化）

```javascript
document.querySelector('.list').addEventListener('click', (e) => {
    if (e.target.matches('li')) {
        console.log('点击了列表项', e.target.textContent);
    }
});
```

---

## 1️⃣1️⃣ 常用内置对象
```
对象 作用 示例
Math 数学运算 Math.random(), Math.floor(), Math.max()
Date 日期时间 new Date(), date.getFullYear()
JSON 数据转换 JSON.stringify(obj), JSON.parse(jsonStr)
RegExp 正则表达式 /\d+/.test('123')
console 调试输出 log, error, table, time
```
---

## 1️⃣2️⃣ 模块化

>导出（export.js）：

```javascript
export const name = 'Tom';
export function greet() { return 'Hello'; }
export default class Person { }
```

>导入（import.js）：

```javascript
import Person, { name, greet as sayHi } from './export.js';
import * as all from './export.js';
```

📌 在 HTML 中使用：<script type="module" src="main.js"></script>

---

## 1️⃣3️⃣ 错误处理（try...catch）

```javascript
try {
    // 可能出错的代码
    throw new Error('自定义错误');
} catch (error) {
    console.error(error.message);
} finally {
    // 无论是否出错都会执行
}
```

---

## 1️⃣4️⃣ 常用小技巧

>深拷贝（简单版）

```javascript
const copy = JSON.parse(JSON.stringify(obj));  // 无法处理函数、undefined、循环引用
// 使用 structuredClone（现代浏览器）
const deepCopy = structuredClone(obj);
```

>防抖与节流（常用优化）

```javascript
// 防抖：延迟执行，频繁触发只执行最后一次
function debounce(fn, delay) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => fn.apply(this, args), delay);
    };
}

// 节流：每隔一段时间执行一次
function throttle(fn, interval) {
    let last = 0;
    return function(...args) {
        const now = Date.now();
        if (now - last >= interval) {
            last = now;
            fn.apply(this, args);
        }
    };
}
```

>数组去重

```javascript
const unique = [...new Set([1,2,2,3])];  // [1,2,3]
```

---

