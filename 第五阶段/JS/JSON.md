# JSON 笔记
>
>可以用来分辨是否写对：
>
>[JSON.cn](https://www.json.cn/)
>
>
><img width="1642" height="648" alt="屏幕截图 2026-08-16 231241" src="https://github.com/user-attachments/assets/c8b95e16-5bf7-4a3a-9984-1efe5e09277a" />

## 1.什么是 JSON
**JSON(JavaScript Object Notation)**：JavaScript 对象表示法，是一种**轻量级的数据交换格式**。
- JSON 不是 JS 对象，只是格式长得像，**独立于编程语言**，几乎所有语言都可以解析。
- 主要用途：前后端数据传输、配置文件、接口返回数据。
> 注意：JSON 是**字符串**，JS对象是内存中的对象。

## 2.JSON语法规则（硬性要求，错一个符号就解析失败）
>
><img width="955" height="447" alt="屏幕截图 2026-08-16 225944" src="https://github.com/user-attachments/assets/edda5f84-ae96-44d1-b2dc-f4249600d088" />

1. 数据由 `键:值` 组成
2. **键名必须使用双引号 `"`，不能单引号，不能不写引号**
3. 值的类型只能是下面6种：
    - 字符串（双引号）
    - 数字
    - 布尔值 `true / false`（不加引号）
    - `null`（不加引号）
    - 对象 `{}`
    - 数组 `[]`
4. JSON**不能写注释**！//  /* */ 写注释直接报错
5. 不能有函数、undefined、Date对象
6. 逗号不能写在最后一项末尾

✅正确JSON示例
```json
{
  "name": "巴啦啦小魔仙",
  "age": 12,
  "isMagic": true,
  "hobby": ["变身","魔法"],
  "info": {
    "address": "魔仙堡"
  },
  "data": null
}
```

❌错误写法
```json
{
  name:"小蓝",      //键没有双引号 ❌
  'sex':'女',       //单引号 ❌
  "func":function(){} //不能放函数 ❌
}
```
## 关于访问对象值
### 可以用.访问
>
><img width="730" height="151" alt="屏幕截图 2026-08-16 230526" src="https://github.com/user-attachments/assets/12d3cb9c-c921-4894-9a37-c0cd73c33c90" />

## 可以用[]访问
>
><img width="751" height="167" alt="屏幕截图 2026-08-16 230711" src="https://github.com/user-attachments/assets/e557615f-54a3-4b4d-82da-0ded9a26ff1b" />



## 3.JS中JSON两个核心API
### JSON.stringify()  JS对象 → JSON字符串
>
><img width="430" height="281" alt="屏幕截图 2026-08-16 233110" src="https://github.com/user-attachments/assets/074b77aa-3b23-4cd3-aae3-e644ac987ec4" />

>
>结果为：
><img width="683" height="197" alt="屏幕截图 2026-08-16 233043" src="https://github.com/user-attachments/assets/29c18b60-181b-4bdd-a7b2-fede9261d75e" />


> 作用：把 JS 对象/数组，转成 JSON格式字符串，传给后端。
```javascript
const obj = { name:"小蓝",age:18 };
//转json字符串
const jsonStr = JSON.stringify(obj);
console.log(jsonStr);
//输出：{"name":"小蓝","age":18}
```
参数拓展
```javascript
//第二个参数过滤器，第三个参数控制缩进美化输出
JSON.stringify(obj,null,2)
```

### JSON.parse() JSON字符串 → JS对象
> 作用：后端返回json字符串，解析成js对象，前端才能读取属性。
>
> 
><img width="781" height="322" alt="屏幕截图 2026-08-16 231603" src="https://github.com/user-attachments/assets/71253993-ab97-4deb-9f1d-f83cd5748cd2" />

```javascript
var mn='{ "name":"秀秀", "alexa":10000, "site":"www.runoob.com" }';
var obj=JSON.parse(mn)
console.log(obj);
```
>
><img width="649" height="216" alt="屏幕截图 2026-08-16 232210" src="https://github.com/user-attachments/assets/1e2964fc-8a7c-431b-a5f4-2b409eacb2ae" />

⚠️报错场景：字符串格式写错，JSON.parse直接抛出异常，需要 try‑catch捕获错误
>
><img width="678" height="154" alt="屏幕截图 2026-08-16 233417" src="https://github.com/user-attachments/assets/21c565ec-ba48-4748-92e0-3cec04ba5958" />

```javascript
let str = "{name:'小蓝'}" //错误json字符串
try{
  let res = JSON.parse(str)
}catch(err){
  console.log("解析失败",err)
}
```

## 4.JSON对象 和 JS对象 的区别
|对比|JSON|JS普通对象|
|---|---|---|
|键|必须双引号|单引号、双引号、不写引号都可以|
|本质|字符串|内存对象|
|注释|不支持|支持|
|值|不能函数、undefined|可以写函数、undefined|

```javascript
//JS对象（内存）
let jsObj = { name:"小蓝" }

//JSON字符串（文本，用于网络传输）
let json = JSON.stringify(jsObj)
```

## 5.JSON数组格式
最外层可以是数组
```json
[
  {"name":"小蓝"},
  {"name":"美琪"}
]
```

## 6.深拷贝经典小技巧
> 局限性：无法拷贝函数、undefined、Symbol、循环引用对象
```javascript
const obj = {a:1,b:{c:2}}
//简单深拷贝
const newObj = JSON.parse(JSON.stringify(obj))
```

## 7.常见坑
1. JSON字符串全部用**双引号**，单引号 `JSON.parse`直接报错
```javascript
//错误！单引号包裹内部键
JSON.parse("{'name':'123'}") //报错
```
2. JSON不允许注释，很多配置文件写注释会解析失败
3. `undefined`经过`JSON.stringify`会直接丢失这个key
```javascript
let o = {a:undefined}
JSON.stringify(o) // {} 直接消失
```
4. 对象循环引用，`JSON.stringify`直接报错
5. Date 对象序列化后变成字符串，不会保留Date类型


```
