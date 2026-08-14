# CSS 笔记
---
## 一、响应式布局完整基础知识
### 1. 什么是响应式布局
响应式布局：**一套网页代码，自动适配手机、平板、电脑不同屏幕宽度**。  
屏幕变大自动变多列、屏幕变小自动变少列，**不需要写多套网站**。

 >学习网址：[CSDNcss响应式布局](https://blog.csdn.net/m0_73916603/article/details/138133083)
### 2. 响应式四大核心要素
1. **视口 viewport**：让手机正常识别网页宽度（必须写）
2. **相对单位**：%、rem、vw、fr（不写固定px）
3. **媒体查询 @media**：根据屏幕宽度改变样式
4. **弹性布局 Flex / Grid**：实现自动自适应排列

### 3. 视口标签（响应式生效的前提）
所有响应式页面**必须写在 head 内**
作用：
- 网页宽度 = 设备屏幕宽度
- 禁止手机默认缩放
- 适配移动端

### 4. 响应式推荐单位
| 单位 | 含义 | 使用场景 |
|-----|------|----------|
| % | 相对父元素 | 盒子宽度 |
| rem | 相对根标签HTML字体 | 字体、边距 |
| vw | 相对屏幕宽度 | 自适应布局 |
| fr | 网格等分单位 | Grid布局专用 |
| px | 固定像素 | **响应式尽量少用** |

### 5. 图片响应式万能代码
```css
img {
  max-width: 100%;
  height: auto;
}
```
> 作用：图片最大宽度不会超过父盒子宽度，不会溢出，高度等比例缩放


### 6. 媒体查询标准断点（给网页设置if判断条件，满足才执行）

>[菜鸟教程媒体查询](https://www.runoob.com/css/css-rwd-mediaqueries.html)

<img width="678" height="410" alt="屏幕截图 2026-08-14 214143" src="https://github.com/user-attachments/assets/35bbd50b-bc70-485d-873f-e4be71af66e1" />

```
@media screen and (max-width: 768px) {
  /* 满足条件才执行的样式 */
}
```
1. `@media`：关键字，代表开始媒体查询
2. `screen`：媒体类型，代表**屏幕设备**（电脑、手机、平板）
3. `and`：并且，连接设备和宽度条件
4. `(max-width:768px)`：条件
   - `max-width:768px`：屏幕宽度 **小于等于 768px**
   - `min-width:768px`：屏幕宽度 **大于等于 768px**
>手机屏幕上显示
<img width="944" height="857" alt="屏幕截图 2026-08-14 215107" src="https://github.com/user-attachments/assets/9df1802e-ea99-4536-b8c7-70deb7b460fe" />

> 行业通用尺寸断点
> ✅ 手机：0 ~ 768px
> ✅ 平板：768px ~ 1200px
> ✅ 电脑大屏：≥1200px

### ⚠️媒体查询致命规则

**媒体查询代码必须写在默认样式下方！**
CSS 规则：后面样式覆盖前面样式。

```
/* ✅正确 */
.box{}
@media{}

/* ❌错误，不会覆盖 */
@media{}
.box{}
```
### 7. 两种开发模式
1. **PC优先**：先写电脑样式，用 max-width 向下适配手机
2. **移动端优先（推荐）**：先写手机样式，用 min-width 向上适配电脑

---

# 二、Flex 弹性布局

>[菜鸟教程FLexb布局](https://www.runoob.com/w3cnote/flex-grammar.html)
## 1. Flex布局介绍
Flex 全称 Flexible Box，**弹性盒子布局**。
作用：**简便实现盒子水平居中、垂直居中、自动排列、自动换行**，解决传统浮动 `float` 清除浮动、垂直居中困难等痛点。
- **一维布局**：只能控制 **一条轴线**（横向 或 纵向）
- 子元素**自动均分、自动挤压、自动换行**
- 适合：导航栏、列表、卡片、自适应排列
- **移动端响应式首选布局**

## 2. 开启 Flex 布局
![](https://i-blog.csdnimg.cn/blog_migrate/69bfc61e4b7b55c1b805f561f324829b.png#pic_center)
1. **弹性容器（父盒子）**：设置 `display: flex` 的元素
2. **弹性项目（子元素）**：容器里面直接子元素
3. **主轴**：默认水平方向（从左 → 右）
4. **侧轴（交叉轴）**：默认垂直方向（从上 → 下）

> ⚠️重点：
> 设置 `display:flex` 之后，**子元素自动变成行内块，浮动失效**！

```
/* 开启弹性布局：写在父容器 */
.box {
  display: flex;
}
```
给**父容器**设置：
```css
.father {
  display: flex;
}
```
设置后：**子元素自动横向排列**

## 3. 父容器六大核心属性
>例子
<img width="830" height="616" alt="屏幕截图 2026-08-14 211246" src="https://github.com/user-attachments/assets/c3f38d10-8cf0-428f-b4cf-44809fafc6bc" />

### ① flex-direction 主轴方向（定方向）
```css
flex-direction: row;        /* 默认：水平从左到右 */
flex-direction: column;     /* 垂直从上到下 */
flex-direction: row-reverse;/* 水平反向 */
flex-direction: column-reverse;/* 垂直反向 */
```

### ② flex-wrap 子元素是否换行（响应式必备）
```css
flex-wrap: nowrap; /* 默认：不换行，挤压子元素 */
flex-wrap: wrap;   /* 自动换行 —— 响应式必须加！ */
```

### ③ justify-content 水平对齐方式（垂直方向上）
```css
justify-content: center;        /* 居中 */
justify-content: flex-start;    /* 靠左 */
justify-content: flex-end;      /* 靠右 */
justify-content: space-between;/* 两端对齐，中间均分 */
justify-content: space-around;  /* 两边留有空隙 */
```

### ④ align-items 水平对齐方式
```css
align-items: center;      /* 垂直居中 */
align-items: flex-start;  /* 顶部对齐 */
align-items: flex-end;    /* 底部对齐 */
```

✅ **水平 + 垂直居中万能组合**

<img width="838" height="848" alt="屏幕截图 2026-08-14 211909" src="https://github.com/user-attachments/assets/f09671a8-10df-4b72-a0fd-0dc15dd69d4f" />

```
.father{
  display: flex;
  justify-content: center;  /*水平居中*/
  align-items: center;      /*垂直居中*/
}
```

### ⑤. `align-content`：多行侧轴对齐

⚠️ **只有出现换行 `flex-wrap:wrap` 多行时才生效！**
单行无效！

```
align-content: stretch;
align-content: flex-start;
align-content: flex-end;
align-content: center;
align-content: space-between;
align-content: space-around;
```
### ⑥. `flex-flow` 复合属性

一次性简写 `flex-direction` + `flex-wrap`

```
flex-flow: row wrap; /*主轴水平，自动换行*/
```
###  gap 间距（最干净）
```css
gap: 20px; /* 上下左右统一间距 */
```

### 标准响应式Flex父容器模板
**写响应式必用！！**
```css
.box {
  display: flex;
  flex-wrap: wrap;//自动换行
  justify-content: space-between;
  gap: 20px;间隙为20px
}
```

## 4. 子元素常用属性
### 1. `flex-grow/flex` 弹性放大比例

<img width="810" height="331" alt="屏幕截图 2026-08-14 212715" src="https://github.com/user-attachments/assets/6e302cf1-a676-42c5-b099-470c41cb6e97" />

默认值 `0`：有剩余空间，也不放大
数字代表**分配剩余空间的比例**
**设置的宽度不再起效**
```
.item{
  flex-grow: 1; /*所有子元素均分剩余宽度*/
}
```

### 2. `flex-shrink` 弹性缩小比例

默认值 `1`：空间不足时自动缩小
值为 `0`：空间不足**禁止缩小**

### 3. `flex-basis`

设置子元素基础宽度，优先级高于 width。

### 4. `flex` 简写（高频考点）

```
flex: 数值;
/* flex: 1 等价于 flex:1 1 0; */
flex:1;  /* 均分宽度，最常用！ */
```

完整格式：`flex: grow shrink basis`

### 5. `align-self`

单独控制**某一个子元素**垂直对齐，覆盖父盒子 `align-items`

```
align-self: center;
align-self: flex-end;
```

### 6. `order`

控制子元素排列顺序，默认 `0`
数值越小，排列越靠前，可以写负数

```
order: -1; /*排到最前面*/
```

## 5. Flex完整响应式案例（三列→两列→单列）
### 案例 1：导航栏水平均匀分布

```
.nav{
  display:flex;
  justify-content: space-around;
}
```

### 案例 2：卡片布局，大屏一行 4 个，手机一行 2 个（配合响应式媒体查询）

```
<style>
  *{margin:0;padding:0;box-sizing:border-box;}
  .container{
    display:flex;
    flex-wrap: wrap; /*自动换行*/
  }
  .card{
    width:25%;
    height:150px;
    background:#87ceeb;
    border:1px solid #fff;
  }
  /*响应式：手机*/
  @media screen and (max-width:768px){
    .card{
      width:50%;
    }
  }
</style>
<div class="container">
  <div class="card">1</div>
  <div class="card">2</div>
  <div class="card">3</div>
  <div class="card">4</div>
</div>
```

## 6.Flex 常见坑点

1. `display:flex` 设置在父元素，**只作用于直接子元素，孙子元素不受影响**
2. 默认不换行！宽度溢出不会自动换行，必须手动加 `flex-wrap:wrap`
3. 子元素设置 flex 后，`float`、`clear` 失效
4. 想要多行垂直对齐，使用 `align-content`，不要用 `align-items`
5. 想要单独修改某个盒子垂直位置：使用 `align-self`
## 6. Flex布局优缺点
- Float：只能左右排版，垂直居中麻烦，需要清除浮动
- Flex：一维布局（横向 / 竖向），轻松实现居中、自适应、自动换行，**开发首选**

> 
> 拓展区分：
> Flex：一维布局（一条轴线）
> Grid：二维布局（同时控制行 + 列）

# 三、Grid 网格布局

>[菜鸟教程grid布局](https://www.runoob.com/css3/css-grid.html)
## 一、Grid 是什么

Grid（网格布局）是 **CSS 二维布局方案**。
Flex 只能控制**一条轴线（一维：横向 OR 竖向）**；
Grid 同时控制 **行 + 列（二维布局）**，适合相册、后台页面、卡片排版、整体页面布局。

> 
> 核心概念

1. **网格容器**：父元素，设置 `display: grid`
2. **网格项目**：容器的直接子元素
3. **网格线**：划分行列的分界线
4. **网格轨道**：行高、列宽（单元格大小）
5. **单元格**：行与列交叉的最小格子
6. **网格区域**：多个单元格合并成一块区域

开启网格布局（写在父盒子）

```
.father {
  display: grid;
}
```

## 二、父容器属性（写在父元素）

### 1. grid-template-columns 定义列宽

### 2. grid-template-rows 定义行高

```
/* 3列：宽度依次 100px 200px 100px */
grid-template-columns: 100px 200px 100px;
/* 2行：高度 80px 120px */
grid-template-rows: 80px 120px;
```

#### 🔥高频函数 repeat () 重复定义

```
/* 创建4列，每一列宽度1fr */
grid-template-columns: repeat(4, 1fr);
/* 等价：1fr 1fr 1fr 1fr */
```

#### 单位 fr 网格剩余空间单位（重点）

`fr` = free space 剩余空间分配单位

```
/* 2列：1份 : 2份 */
grid-template-columns: 1fr 2fr;
```

> 
> 总剩余空间按照比例分配，自适应，响应式常用！

### 3. gap 间距（行列间隙）

```
gap: 10px;                /* 行间距、列间距都是10px */
gap: 10px 20px;           /* 行间距 10px，列间距20px */

/* 拆分写法 */
row-gap: 10px;    /* 行间距 */
column-gap:20px;  /* 列间距 */
```

### 4. justify-items：单元格内【水平对齐】

控制**每个格子内部子元素水平位置**

```
justify-items: stretch;    /* 默认：拉伸填满宽度 */
justify-items: start;      /* 左对齐 */
justify-items: center;     /* 水平居中 */
justify-items: end;        /* 右对齐 */
```

### 5. align-items：单元格内【垂直对齐】

格子内部垂直方向

```
align-items: stretch;
align-items: start;
align-items: center;
align-items: end;
```

✅ 格子内水平 + 垂直居中

```
justify-items: center;
align-items: center;
```

### 6. place-items 简写

```
place-items: center center; /* 垂直 水平 */
```

### 7. justify-content：整个网格【水平对齐】

网格总宽度 < 父容器宽度时生效，控制**整个网格块**位置

```
justify-content: start;
justify-content: center;
justify-content: end;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

### 8. align-content：整个网格【垂直对齐】

网格总高度 < 父容器高度时生效

### 9. place-content 简写

```
place-content: center center;
```

### 10. grid-template-area 网格区域合并（布局划分）

用于页面大块布局：头部、侧边栏、主体、底部

```
.container{
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header header"
    "aside main"
    "footer footer";
}
/* 子元素绑定区域 */
.header { grid-area: header; }
.aside  { grid-area: aside; }
.main   { grid-area: main; }
.footer { grid-area: footer; }
```

## 三、子元素属性（写在网格项目）

### 1. grid-column 控制单元格横跨列

```
/* 从第1根列线，跨越2格 */
grid-column: 1 / span 2;
```

拆分写法

```
grid-column-start:1;
grid-column-end:3;
```

### 2. grid-row 控制单元格横跨行

```
grid-row: 1 / span 2;
```

### 3. align-self 单独控制单个元素垂直对齐

### 4. justify-self 单独控制单个元素水平对齐

```
.item{
  justify-self: center;
  align-self: center;
}
```

## 四、Grid + 响应式媒体查询 经典案例

大屏 4 列，手机 2 列

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container{
  display: grid;
  /* 默认电脑：4列 */
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  width: 90%;
  margin: 30px auto;
}
.box{
  height: 100px;
  background: #6cf;
}
/* 手机适配 */
@media screen and (max-width:768px){
  .container{
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
</head>
<body>
<div class="container">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
  <div class="box">4</div>
</div>
</body>
</html>
```

## 五、Flex 和 Grid 核心区别（考试重点）

1. **Flex：一维布局**
只能单行 / 单列；适合导航栏、单行列表。
2. **Grid：二维布局**
同时管理行、列；适合整体页面布局、卡片相册。

> 
> 开发经验：
> 局部单行排列 → Flex
> 整体页面、多行多列规整排版 → Grid

## 六、高频易错点

1. `display:grid` 只对**直接子元素**生效，孙子元素不受网格影响
2. fr 只分配**剩余空间**，不能和固定宽度简单叠加理解
3. `justify-items`（格子内对齐）≠ `justify-content`（整个网格对齐）极易混淆
4. Grid 默认不会自动换行！列数固定，超出会溢出（和 Flex-wrap 区别很大）
5. 网格项目浮动 `float`、`display:inline-block` 全部失效
---

# 四、Flex 和 Grid 终极区别（必考重点）
## 1. Flex
- **一维布局**（要么横、要么竖）
- 适合：导航、菜单、流式卡片、不规则布局
- **移动端开发首选**

## 2. Grid
- **二维布局**（同时控制行列）
- 适合：整齐卡片、官网整体布局、相册、产品展示
- **做规整页面首选**

## 3. 一句话区分
**想要灵活自由 → 用 Flex**  
**想要整齐规范 → 用 Grid**

---

# 五、响应式布局易错点总结（避坑）
1. 忘记写 viewport → 移动端完全失效
2. 盒子写固定 width:1200px → 无法适配
3. 不写 flex-wrap:wrap → 手机不会换行、内容溢出
4. 大量使用px → 无法自适应
5. 媒体查询断点顺序混乱 → 样式覆盖失效

---
