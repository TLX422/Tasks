## 1. Vue 的基本认识

1. Vue 是**渐进式 JavaScript 前端框架**，用于构建用户界面，核心是视图层。
2. 核心特点

- **声明式渲染**：只写想要的结果，不用手动操作DOM，框架帮你操作页面。
- **响应式**：数据改变，页面自动更新，不用`innerHtml`、`querySelector`手动改页面。
- **组件化开发**：页面拆成一个个`.vue`组件，复用、好维护。> 
> Vue2 选项式API（Options API）；Vue3 支持选项式 + 组合式API（setup）

## 2. Vue开发环境的安装

> 
> 前提：电脑装好 Node.js（自带npm包管理器）
> 打开系统终端（cmd/powershell）
> ### Windows 打开电脑系统终端（cmd）

1. 键盘：`Win + R`，输入 `cmd`，回车
或者文件夹地址栏输入 cmd 回车，直接在当前文件夹打开终端# Vue基础全套笔记（考试/复习）


```
# 查看版本，验证安装成功
node -v
npm -v

# 安装vue脚手架（Vue2旧项目）
npm install -g @vue/cli

# 创建vue项目（vue3）
npm create vue@latest
```

- `-g`：全局安装，电脑任意位置都可以使用命令。

## 3. Vue文件的基本模板（`.vue`单文件组件）

一个`.vue`文件分为三部分：

1. `<template>`：写HTML页面结构，**有且只能有一个根标签（Vue2）**；Vue3支持多根节点
2. `<script>`：写js逻辑，数据、方法
3. `<style>`：写css样式，`scoped`代表样式只作用当前组件，不会污染其他组件

### Vue3组合式基础模板

```
<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const msg = ref("hello vue3")
</script>

<style scoped>
h1{
  color:red;
}
</style>
```

## 4. VSCode自定义vue代码片段（输入快捷字符自动生成模板）

> 
> 类似 html 的 `!` 生成html骨架

1. VSCode 按 `Ctrl+Shift+P`
2. 输入 `Configure User Snippets` →新建全局代码片段文件，命名`vue.code‑snippets`
3. 把下面全部复制粘贴进去保存

```
{
  "vue3基础模板": {
    "prefix": "vue3",
    "body": [
      "<template>",
      "  <div></div>",
      "</template>",
      "",
      "<script setup>",
      "import { ref,reactive } from 'vue'",
      "",
      "</script>",
      "",
      "<style scoped>",
      "",
      "</style>"
    ],
    "description": "vue3单文件组件模板"
  }
}
```

✅使用：新建`.vue`文件，输入`vue3`，按tab键，自动生成整套模板。

## 5. 创建Vue项目 +命令行启动网页

### ①创建项目

```
npm create vue@latest
```

一路回车，会生成项目文件夹。

### ②进入项目文件夹

```
cd 你的项目文件夹名
```

### ③安装依赖

```
npm install
```

### ④启动开发服务器（唤醒网页）

```
npm run dev
```

终端会输出地址：`http://localhost:5173`，复制到浏览器打开，看到vue页面。

> 
> 重点：

- `npm install`：读取package.json下载所有第三方包
- `npm run dev`：启动本地开发服务器，修改代码网页自动刷新

## 6. 粗浅了解Vuex

> 
> Vuex：**Vue2官方全局状态管理库**，用来做跨组件共享数据。
> Vue3官方推荐用 Pinia，Vuex逐步不再维护。

- 作用：多个组件都要用的数据，放在vuex仓库，不用父子组件一层层传值。
- Vuex五大核心：

1. `state`：存放全局数据（仓库）
2. `mutations`：修改state数据（同步）
3. `actions`：写异步请求（接口请求）
4. `getters`：对state数据计算，类似计算属性
5. `modules`：拆分模块，仓库数据太多分块管理

> 
> 简单理解：Vuex就是一个公共大仓库，所有组件都可以读取/修改仓库里面的数据。

## 7. Vue引用组件库用法（例如Element‑Plus）

Element‑Plus是Vue3常用UI组件库，提供现成按钮、表单、弹窗，不用自己写css。

### 完整步骤

1.终端进入项目，安装组件库

```
npm install element-plus
```

2. 在`main.js`全局引入

```
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

3.任意`.vue`组件直接使用组件

```
<template>
  <el-button type="primary">主要按钮</el-button>
</template>
```

> 
> 知识点总结：

1. 安装：npm安装组件库包
2. main.js通过`app.use()`注册
3. vue模板直接写组件标签使用

## 📝小总结

1. `.vue`单文件三部分：template模板、script脚本、style样式；scoped让样式隔离。
2. 启动项目三部曲：`cd项目`→`npm install`→`npm run dev`
3. Vuex用来管理全局共享状态；Vue3优先Pinia。
4. UI组件库：npm下载，main.js注册，页面直接使用现成组件。

需要我给你出几道选择填空练习题巩固吗？。


