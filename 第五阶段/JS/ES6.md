# E36 
[菜鸟教程：ES6教程](https://www.runoob.com/w3cnote/es6-tutorial.html)

## 一、let 和 const
### var 的旧问题（为什么淘汰var）
1. **没有块级作用域**，`if/for {}`大括号里面声明，外面也能访问
2. **变量提升**：可以先使用，后声明
3. 允许重复声明同一个变量，不会报错，容易覆盖变量
4. 全局var变量会挂载到`window`对象上

```js
// var 问题演示
for(var i = 0; i<3; i++){}
console.log(i) //3，循环结束i泄露到外部
```

### let
1. **块级作用域**：`{ }`内部生效（if、for、while大括号）
2. **不能重复声明**同一个变量，直接报错
3. **存在暂时性死区**：变量在块内已经被绑定，在声明之前不能使用
4. **不会挂载到window**
5. 可以修改赋值

```js
if(true){
  let a = 10
}
console.log(a) // ❌ a is not defined，块外面访问不到

let num;
num = 100 //可以先声明，后赋值
```

> 暂时性死区：只要进入块作用域，let变量就已经绑定这块区域，在let执行之前，不能访问该变量。
```js
console.log(x) //报错
let x = 10
```

### const
> const 常量
1. **块级作用域**，和let一样
2. **声明的时候必须赋值，不能只声明不赋值**
3. **禁止重复声明**
4. 同样存在暂时性死区，不挂载window
5. ⚠重点：**const不是值不能改，是不能重新赋值**
    - 基本数据类型：值不可修改
    - **引用类型（对象、数组）：可以修改内部属性/元素，不能整体重新赋值**

```js
const arr = [1,2,3]
arr.push(4) // ✅允许，修改数组内部元素
arr = [] // ❌报错，不能重新赋值

const obj = {name:'张三'}
obj.name = '李四' //✅修改属性没问题
obj = {} //❌报错
```

### var / let / const 对比表
| | var | let | const |
|----|-----|-----|-------|
|块级作用域|❌无|✅有|✅有|
|变量提升|✅有|✅有（暂时性死区，不能先使用）|✅有|
|重复声明|允许|禁止报错|禁止报错|
|声明不赋值|可以|可以|❌必须初始化赋值|
|重新赋值|可以|可以|不可以（引用类型可改内部）|
|挂载window|是|否|否|

✅开发推荐：**优先使用const，只有需要改变变量的时候用let，禁止使用var**

---

## 二、Promise异步编程
### 1. 为什么需要Promise？
js异步场景：定时器、ajax请求、接口调用。
旧写法：回调函数，多层嵌套会产生**回调地狱**，代码横向越来越长，可读性差，难以维护。

Promise专门用来处理异步，把嵌套回调改成链式调用。

### 2.Promise三种状态（状态不可逆，一旦改变就不会再变）
1. `pending` 等待中（初始状态）
2. `fulfilled(resolved)` 成功
3. `rejected` 失败

> 状态只能从pending → fulfilled 或者 pending → rejected；**状态改变之后就固定，不能再次修改**。

### 3.基础语法
```js
const p = new Promise((resolve, reject)=>{
  // resolve：函数，把promise变成成功状态，传递成功结果
  // reject：函数，把promise变成失败状态，传递失败错误信息
  setTimeout(()=>{
    //模拟异步请求
    let ok = true
    if(ok){
      resolve('请求成功的数据')
    }else{
      reject('请求失败')
    }
  },1000)
})

// .then 接收成功结果
// .catch 捕获失败
// .finally 无论成功失败都会执行
p.then(res=>{
  console.log(res)
}).catch(err=>{
  console.log(err)
}).finally(()=>{
  console.log('不管成功失败，一定执行')
})
```

### 4.Promise链式调用
`.then()`会返回一个全新Promise对象，实现链式，解决回调地狱
```js
//连续多次请求
new Promise(resolve=>resolve(1))
.then(res=>{
  console.log(res)
  return 2 //return的值会包装成resolved的promise传给下一个then
})
.then(res=>{
  console.log(res)
  return 3
})
.then(res=>console.log(res))
```

> 如果then里面抛出错误，或者返回`Promise.reject()`，后续会进入catch。

### 5.Promise静态方法
1. `Promise.resolve(值)`：快速创建成功的Promise
2. `Promise.reject(错误信息)`：快速创建失败的Promise
```js
Promise.resolve(100).then(res=>console.log(res))
Promise.reject('出错').catch(err=>console.log(err))
```

3. `Promise.all([p1,p2,p3])`
- 接收promise数组，**全部成功才成功，返回全部结果数组；只要有一个失败，整体直接失败**
> 适合：多个接口同时请求，全部拿到数据之后再处理

4. `Promise.race([p1,p2,p3])`
- 赛跑，**哪个先状态改变，就用哪个结果，不管成功失败**

---

## 三、async / await
> `async / await` 是 Promise 的语法糖，只是包装，底层依然是Promise，目的：**把异步代码写的像同步代码一样，阅读更直观**

### async关键字
写在函数前面，这个函数永远返回Promise对象
- 函数内部return普通值 → 返回成功Promise
- 函数抛出错误 → 返回失败Promise

```js
async function fn(){
  return 'hello'
}
fn().then(res=>console.log(res))
```

### await关键字
⚠**await 只能写在 async修饰的函数里面，普通函数直接写await直接报错！**
作用：等待Promise执行完成，直接拿到成功的结果。
```js
async function getInfo(){
  // await 等待promise成功，把resolve结果赋值给data
  const data = await new Promise(resolve=>{
    setTimeout(()=>resolve('接口返回数据'),1000)
  })
  console.log(data)
}
getInfo()
```

### await捕获错误（重点！）
`await遇到rejected失败状态，会直接抛出异常，程序报错终止`
两种捕获错误方案：
1. `try {} catch(err){}` （开发最常用）
```js
async function load(){
  try{
    //如果这个promise失败，代码跳入catch
    const res = await fetch('/api')
    console.log('成功',res)
  }catch(err){
    console.log('请求失败',err)
  }
}
```
2. `.catch()`直接跟在await后面
```js
const res = await fetch('/api').catch(err=>{})
```

### ❗易错坑点
1. await是阻塞该async函数内部后面代码，**不会阻塞外面全局代码**
```js
async function test(){
  console.log('A')
  await new Promise(r=>setTimeout(r,1000))
  console.log('B') //等待1秒之后打印
}
test()
console.log('C')
//打印顺序 A → C → B
//外面的同步代码不会等待await
```

2. await多个promise，如果直接顺序写，会串行（一个执行完才执行下一个）
```js
//串行，总共耗时2000ms
await p1
await p2

//想要并行同时执行，用Promise.all
await Promise.all([p1,p2])
```

### 1. Promise有几种状态？
pending等待、fulfilled成功、rejected失败；状态一旦变更，不可更改。

### 2. async await和Promise的关系
async await是Promise语法糖，底层基于Promise；Promise链式调用还是一堆.then，async await可以用同步写法书写异步逻辑。

### 3. await失败会怎么样？
await接收rejected的Promise，会抛出错误，需要try‑catch捕获，否则JS报错。

### 4. Promise.all 和 Promise.race区别
- Promise.all：全部成功才成功，任意一个失败直接失败；适合并发请求，全部完成再处理。
- Promise.race：竞速，第一个完成（无论成功失败）就返回结果。

### 5.什么是回调地狱？
异步回调层层嵌套，代码横向增长，维护困难，Promise/async await解决回调地狱。

## 易错题总结
1. const对象可以修改属性，只是不能重新赋值整个对象。
2. let/const存在暂时性死区，有变量提升但是不能声明前使用。
3. await不能脱离async函数直接写在全局。
4. Promise状态不可逆，更改之后不会二次改变。

如果你需要，我可以出5道选择判断题巩固知识点。
