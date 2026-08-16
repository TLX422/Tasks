# Ajax


## 1.什么是 Ajax
**AJAX：Asynchronous JavaScript And XML**
异步 JavaScript 和 XML。
> 作用：**不刷新整个网页，向服务器发送请求，获取数据，局部更新页面**。
- 以前网页提交表单就要整页刷新；Ajax 可以后台偷偷请求数据，页面不动。
- 早期传输数据用 XML，现在基本全部用 **JSON**。
- Ajax 不是一门新语言，是 JS 的一套技术方案。

> 核心特点：**异步**，发送请求之后，JS代码不会卡住，继续往下执行，等后端返回数据再执行回调。

## 2.原生 Ajax
`XMLHttpRequest` 浏览器内置对象，实现原生ajax。

### 完整基础模板
```javascript
//1. 创建请求对象
const xhr = new XMLHttpRequest();

//2. 设置请求方式和接口地址
// open(请求方式,url, 是否异步 true异步 / false同步)
xhr.open("GET", "https://xxx/api/list", true);

//3. 监听服务器响应状态
xhr.onload = function () {
  // status 状态码 200~299代表成功
  if (xhr.status >= 200 && xhr.status < 300) {
    // xhr.responseText 获取后端返回的字符串，一般是JSON字符串
    const res = JSON.parse(xhr.responseText);
    console.log("后端返回数据", res);
  } else {
    console.log("请求失败", xhr.status);
  }
};

//4. 发送请求
xhr.send();
```

### GET 请求
- 参数拼在url后面 `?key=value&a=1`
- send()里面不传参数
```js
xhr.open("GET","/api/user?name=xiaolan&age=16",true)
xhr.send()
```

### POST 请求
post 参数放在 send() 里面发送，**必须设置请求头**
```javascript
const xhr = new XMLHttpRequest();
xhr.open("POST", "/api/login", true);
//告诉后端我发送的数据是json格式
xhr.setRequestHeader("Content‑Type", "application/json");

//把js对象转为json字符串发送
const data = JSON.stringify({ username:"xiaolan",pwd:"123456" });
xhr.onload = function(){
  let result = JSON.parse(xhr.responseText)
}
xhr.send(data); //post参数写在这里
```

## 3.重要事件
1. `onload`：请求完成（成功/失败都会触发），推荐使用
2. `onreadystatechange`：旧写法，监听请求状态变化
`readyState` 请求状态：
- 0：未初始化
- 1：open已调用
- 2：响应头返回
- 3：正在接收数据
- 4：**全部数据接收完毕**
```js
xhr.onreadystatechange = function(){
  if(xhr.readyState ===4){
    //请求全部完成
  }
}
```
3. `onerror`：网络错误（断网、跨域）触发
4. `ontimeout`：请求超时

### 设置超时
```js
xhr.timeout = 3000; //3秒超时
xhr.ontimeout = function(){
  console.log("请求超时！")
}
```

## 4.同步 vs 异步
`xhr.open(method,url, boolean)`
- `true` → **异步（默认）**：发送请求，代码继续向下跑，不等后端返回。开发全部用异步。
- `false` → **同步**：代码卡住，原地等待服务器返回结果，页面卡死，**禁止使用**。

## 5.状态码 status
- `200‑299` 请求成功
- `400` 参数错误
- `401` 未登录，没有权限
- `404` 接口地址找不到
- `500` 服务器内部报错

> status 是http状态码；readyState是ajax对象自身的状态。

## 6.跨域问题
### 什么跨域
浏览器同源策略：**协议、域名、端口，任意一个不一样，就是跨域，ajax被拦截**。
> 浏览器安全限制：JS不能直接请求别的域名接口。

解决跨域三种方案：
1. **后端CORS**（最常用）后端设置响应头，允许前端域名访问
2. **jsonp**：只能get请求，利用script标签不受同源限制（旧方案，现在少用）
3. **代理服务器**：webpack/vite代理，开发环境使用

> ⚠️跨域错误是浏览器拦截，**请求已经发到服务器，只是浏览器不给JS读取返回结果**。

## 7.jQuery 的 $.ajax（了解）
以前项目大量使用，现在基本淘汰
```js
$.ajax({
  url:"/api/list",
  method:"GET",
  success(res){
    console.log(res)
  },
  error(err){
    console.log("出错")
  }
})
```

## 8.fetch API（浏览器新一代，属于ajax思想）
fetch是浏览器新API，替代XMLHttpRequest，返回Promise
```javascript
//get
fetch("/api/list")
.then(res=>{
  return res.json() //把返回json字符串解析成js对象
})
.then(data=>{
  console.log(data)
})
.catch(err=>{
  console.log("网络错误")
})
```

fetch post示例
```js
fetch("/api/login",{
  method:"POST",
  headers:{
    "Content‑Type":"application/json"
  },
  body:JSON.stringify({name:"xxx"})
})
.then(res=>res.json())
.then(d=>console.log(d))
```

> fetch坑：**http状态码404、500不会进catch，只有网络断网才会catch**，需要手动判断状态。

## 9.Ajax 和 Axios关系
- Ajax：是**技术思想**（局部刷新异步请求）
- XMLHttpRequest、fetch：浏览器原生API实现ajax
- **axios：第三方库，对XMLHttpRequest封装，基于Promise**
> axios不是浏览器自带，需要引入，开发实际项目用axios最多。

axios简单示例
```js
axios.get("/api/list").then(res=>{
  console.log(res.data)
})
```

