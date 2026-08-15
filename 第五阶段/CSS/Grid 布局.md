# Grid 网格布局

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
<img width="1029" height="482" alt="屏幕截图 2026-08-14 224942" src="https://github.com/user-attachments/assets/7de7780a-2ceb-4ec1-a861-dc2043501630" />

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

<img width="1335" height="861" alt="屏幕截图 2026-08-14 225919" src="https://github.com/user-attachments/assets/10f69f5d-d3eb-4f5b-8e39-1aade0eafa71" />

---
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

<img width="1902" height="852" alt="屏幕截图 2026-08-14 230358" src="https://github.com/user-attachments/assets/0a67fa09-3437-4d5c-8fb2-f33c2c55c019" />

---
<img width="579" height="543" alt="屏幕截图 2026-08-14 230748" src="https://github.com/user-attachments/assets/3f797d6a-7be0-4e38-b171-db917e13c174" />

>跨两列，2和3和合并，把2再类名加上one，把3注释掉
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

# 跨两行两列

<img width="625" height="454" alt="屏幕截图 2026-08-14 231248" src="https://github.com/user-attachments/assets/fe201b84-9b1c-4b0f-9e9f-6bf62477a546" />

<img width="1914" height="819" alt="屏幕截图 2026-08-14 231340" src="https://github.com/user-attachments/assets/72365148-85fc-4d59-a6c4-2ad4ed1f7652" />


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

# 四、Flex 和 Grid 终极区别
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
