# Vue 基础学习笔记

## 一、Vue 的基本认识

### 1. 什么是Vue

Vue 是一套**渐进式 JavaScript 前端框架**，用于构建用户界面。

- **渐进式**：可以部分引入使用，也可以整套完整开发大型SPA项目，按需选用能力。
- 核心思想：**数据驱动视图、组件化开发**，尽量避免手动操作DOM。
- 版本：现在主流 **Vue3（组合式API setup）**，旧项目 Vue2（选项式API）。

### 2. 核心特点

1. **声明式渲染**：只描述页面长什么样，Vue帮我们操作DOM
2. **双向数据绑定**：数据和页面视图自动同步
3. **组件化**：页面拆分成一个个`.vue`组件，复用、好维护
4. **虚拟DOM**：提高页面更新性能
5. 适合开发 **SPA单页应用**

### 3. 两个API风格

- **选项式API（Vue2默认，Vue3也支持）**：写`data、methods、mounted`等配置选项
- **组合式API（Vue3推荐）**：用`setup()`，`ref、reactive`，代码聚合，适合大项目

> 
> 面试简答：Vue是渐进式JS框架，基于数据驱动视图，采用组件化开发，分为选项式、组合式两种写法。

---

## 二、Vue开发环境的安装

> 
> 现在官方推荐构建工具：**Vite**（速度快，替代旧的vue‑cli）
> 前提：电脑安装好 **Node.js**（自带npm包管理器）

### 步骤1：检查Node环境

打开终端(cmd/终端)

```
node -v
npm -v
```

输出版本号代表安装成功。

### 步骤2：使用Vite创建Vue项目

```
# npm 创建vue项目
npm create vite@latest my‑vue‑demo -- --template vue
```

- `my‑vue‑demo`：项目文件夹名字，可以自定义
- `--template vue`：代表创建vue3项目

### 步骤3：进入项目、安装依赖、启动项目

```
# 进入项目文件夹
cd my‑vue‑demo
# 安装项目所有依赖包
npm install
# 启动开发服务器
npm run dev
```

终端会输出访问地址 `http://localhost:5173`，浏览器打开即可看到Vue欢迎页面。

### 补充：项目目录简单认识

```
my‑vue‑demo
├─ src
│   ├─ App.vue     # 根组件
│   ├─ main.js     # 入口文件，创建vue实例，挂载页面
│   └─ components  # 存放自定义组件
├─ index.html      # 单页面唯一html
└─ package.json    # 项目配置、依赖清单
```

> 
> main.js（Vue3默认入口）

```
import { createApp } from 'vue'
import App from './App.vue'
// 创建vue应用，挂载到index.html的#app节点
createApp(App).mount('#app')
```

---

## 三、.vue 文件单文件组件基本模板

`.vue` 是Vue**单文件组件SFC**，一个文件就是一个组件。
一个组件固定三部分：

1. `<template>`：**模板HTML**，写页面结构【必须有】
2. `<script>`：**JS逻辑**，数据、方法
3. `<style>`：**CSS样式**，写组件样式，加`scoped`样式只对当前组件生效

### ✅ Vue3 组合式API模板（setup语法糖，`<script setup>`，项目最常用）

```
<template>
  <!-- 页面HTML结构，只能有一个根标签 -->
  <div class="box">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script setup>
// 组合式API 语法糖，不需要写setup函数
import { ref } from 'vue'
// 定义响应式数据
const msg = ref('Hello Vue3')
</script>

<style scoped>
/* scoped：样式隔离，只作用于当前组件 */
.box {
  color: red;
}
</style>
```

### ✅ Vue3 选项式API模板（兼容老项目）

```
<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      message:"hello vue"
    }
  },
  methods:{

  }
}
</script>

<style scoped>

</style>
```

### 重点知识点

1. `<template>`里面，**顶层只允许一个根元素**。
2. `<script setup>`是Vue3推荐语法糖，代码更简洁。
3. `<style scoped>`：样式隔离，组件之间样式互不污染，写组件一定要加。
4. 插值语法 `{{ 变量名 }}`，把JS数据渲染到页面。

### 易错点

- .vue文件不能直接浏览器打开，**必须经过vite/webpack编译**，要启动`npm run dev`运行。
- `scoped`只对当前组件生效；去掉scoped，样式全局生效。

---

