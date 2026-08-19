
# Vue 学习笔记


## 一、前端框架的认识
### 1. Web前端框架概念
前端框架是一套封装完成的JavaScript代码解决方案，封装了原生DOM操作、路由、状态管理等通用功能。
核心优势：告别频繁手动操作DOM，采用组件化、数据驱动思想，大幅提升大型项目开发效率。
主流前端框架：Vue、React、Angular。

## 二、Vue 的基本认识
>[Vue快速入门](https://vuejs.org/guide/quick-start.html)
>[菜鸟教程：Vue3教程](https://www.runoob.com/vue3/vue3-tutorial.html)
1. Vue 是**渐进式 JavaScript 前端框架**
2. 两大核心思想：**数据驱动视图、组件化开发**
3. 单文件组件：`.vue` 文件（SFC），分为三层结构
- `<template>`：页面HTML结构
- `<script>`：JavaScript业务逻辑
- `<style>`：CSS样式代码

## 三、Vue 开发环境安装（Vue3）
> 前置条件：电脑安装 Node.js
```bash
# 创建Vue项目
npm create vue@latest
# 进入项目文件夹
cd 项目名称
# 安装项目依赖
npm install
# 启动开发服务器（命令行运行，唤醒网页预览）
npm run dev
```

启动成功后，终端会给出本地地址 `http://localhost:5173/`，浏览器打开即可访问页面。

## 四、Vue 文件基础模板

### 任务：VSCode自定义代码片段

目标：模仿HTML输入`!`自动生成骨架，在`.vue`文件输入`!` + Tab一键生成组件模板。

#### 操作步骤

1. VSCode 快捷键 `Ctrl + Shift + P`
2. 输入：配置用户代码片段 → 新建全局代码片段文件
3. 命名：`vue.code-snippets`

#### Vue3 setup 片段配置代码

```
{
  "Vue3基础组件模板": {
    "prefix": "!",
    "scope": "vue",
    "body": [
      "<template>",
      "  <div class=\"container\">",
      "    $1",
      "  </div>",
      "</template>",
      "",
      "<script setup>",
      "// 业务逻辑编写区域",
      "",
      "</script>",
      "",
      "<style scoped>",
      "",
      "</style>"
    ],
    "description": "Vue3 SFC基础模板 ! 快捷键触发"
  }
}
```

- `prefix:"!"`：触发关键词
- `scope:"vue"`：仅在vue文件生效
- `$1`：生成模板后光标停留位置
- `<style scoped>`：样式仅作用于当前组件，防止全局样式污染

## 五、创建Vue项目并启动网页
>[菜鸟教程：Vue创建项目](https://www.runoob.com/vue3/vue3-create-project.html)
1. 使用npm命令初始化Vue项目
2. 安装依赖包 `npm install`
3. 命令行执行 `npm run dev` 启动本地服务
4. 访问终端地址实时预览页面，修改代码浏览器自动刷新

## 六、Vuex / Pinia 简单了解

1. **Vuex**：Vue2官方全局状态管理库，用于多个组件共享全局数据。
2. **Pinia**：Vue3推荐新一代状态管理工具，简化API，替代Vuex。
作用：统一管理全局共享数据，解决组件之间传值麻烦的问题。

## 七、Vue 引入组件库使用方式（示例：Element Plus）

组件库提供现成按钮、表单、弹窗等UI组件，无需重复编写样式。

```
# 安装组件库
npm install element-plus
```

在`main.js`全局注册

```
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

注册完成后，所有`.vue`页面可以直接使用UI组件。

```
