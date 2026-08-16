# JSON 笔记

## 1. 什么是 JSON

**JSON（JavaScript Object Notation）**：JavaScript 对象表示法，是一种**轻量级数据交换格式**。

- 作用：前后端传输数据，后端给前端返回数据大多用 JSON
- JSON 不是 JS 对象，只是长得像，是**字符串格式**

## 2.JSON 两种结构

### ① 对象格式 `{ }` 键值对

```
{
  "name":"小明",
  "age":18,
  "hobby":["看书","打球"]
}
```

> 
> ⚠️JSON 严格规则：

1. **键名 key 必须双引号包裹，不能单引号，不能不写引号**
2. 字符串值也必须**双引号**
3. 数字、布尔、null 不用引号
4. 不能写注释！不能写函数！

### ② 数组格式 `[ ]`

```
[
  {"id":1,"title":"新闻1"},
  {"id":2,"title":"新闻2"}
]
```

## 3.JS 和 JSON 互相转换⭐（最重要）

### JSON.stringify ()  JS 对象 → JSON 字符串

```
const obj = { name:"小红", age:20 }
//转成json字符串
let jsonStr = JSON.stringify(obj)
console.log(jsonStr)
```

### JSON.parse () JSON 字符串 → JS 对象

```
let str = '{"name":"小红","age":20}'
//解析成js对象
let jsObj = JSON.parse(str)
console.log(jsObj.name)
```

> 
> 记忆口诀：
> 
> 
> - stringify：**对象变字符串（JSON）**
> - parse：**JSON 字符串解析成 JS 对象**

## 4.JSON 允许的数据类型

✅可以：

- 字符串、数字、布尔 `true/false`
- `null`
- 对象`{}`、数组`[]`

❌**不允许**：

- 函数 function
- undefined
- 注释 //  /**/

## 5. 易错对比

```
//JS对象（js代码，可以单引号，写函数）
let jsObj = { name:'张三' }

//JSON字符串（数据格式，全部双引号）
let json = '{"name":"张三"}'
```

## 6. 综合小 demo

```
// js对象
let student = {
  username:"小李",
  gender:"女",
  score:[88,92,76]
}

//1.对象转json字符串
let jsonText = JSON.stringify(student)
console.log(jsonText)

//2.json字符串转回js对象
let res = JSON.parse(jsonText)
console.log(res.score[0])
```
