# CSS 笔记

---
## 一、响应式布局完整基础知识
### 1. 什么是响应式布局
响应式布局：**一套网页代码，自动适配手机、平板、电脑不同屏幕宽度**。  
屏幕变大自动变多列、屏幕变小自动变少列，**不需要写多套网站**。

### 2. 响应式四大核心要素
1. **视口 viewport**：让手机正常识别网页宽度（必须写）
2. **相对单位**：%、rem、vw、fr（不写固定px）
3. **媒体查询 @media**：根据屏幕宽度改变样式
4. **弹性布局 Flex / Grid**：实现自动自适应排列

### 3. 视口标签（响应式生效的前提）
所有响应式页面**必须写在 head 内**
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
作用：
- 网页宽度 = 设备屏幕宽度
- 禁止手机默认缩放
- 适配移动端

### 4. 响应式推荐单位
| 单位 | 含义 | 使用场景 |
|-----|------|----------|
| % | 相对父元素 | 盒子宽度 |
| rem | 相对根字体 | 字体、边距 |
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
作用：图片永远不会超出屏幕，自动缩放。

### 6. 媒体查询标准断点（企业通用）
```css
/* 电脑：大于1024px */
@media screen and (min-width:1024px){}

/* 平板：768px ~ 1024px */
@media screen and (min-width:768px) and (max-width:1024px){}

/* 手机：小于768px */
@media screen and (max-width:768px){}
```

### 7. 两种开发模式
1. **PC优先**：先写电脑样式，用 max-width 向下适配手机
2. **移动端优先（推荐）**：先写手机样式，用 min-width 向上适配电脑

---

# 二、Flex 弹性布局（重点、最常用）
## 1. Flex布局介绍
- **一维布局**：只能控制 **一条轴线**（横向 或 纵向）
- 子元素**自动均分、自动挤压、自动换行**
- 适合：导航栏、列表、卡片、自适应排列
- **移动端响应式首选布局**

## 2. 开启 Flex 布局
给**父容器**设置：
```css
.father {
  display: flex;
}
```
设置后：**子元素自动横向排列**

## 3. 父容器六大核心属性（逐字背诵）

### ① flex-direction 主轴方向
```css
flex-direction: row;        /* 默认：水平从左到右 */
flex-direction: column;     /* 垂直从上到下 */
flex-direction: row-reverse;/* 水平反向 */
flex-direction: column-reverse;/* 垂直反向 */
```

### ② flex-wrap 是否换行（响应式必备）
```css
flex-wrap: nowrap; /* 默认：不换行，挤压子元素 */
flex-wrap: wrap;   /* 自动换行 —— 响应式必须加！ */
```

### ③ justify-content 水平对齐
```css
justify-content: center;        /* 居中 */
justify-content: flex-start;    /* 靠左 */
justify-content: flex-end;      /* 靠右 */
justify-content: space-between;/* 两端对齐，中间均分 */
justify-content: space-around;  /* 两边留有空隙 */
```

### ④ align-items 垂直对齐
```css
align-items: center;      /* 垂直居中 */
align-items: flex-start;  /* 顶部对齐 */
align-items: flex-end;    /* 底部对齐 */
```

### ⑤ gap 间距（最干净）
```css
gap: 20px; /* 上下左右统一间距 */
```

### ⑥ 标准响应式Flex父容器模板
**写响应式必用！！**
```css
.box {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 20px;
}
```

## 4. 子元素常用属性
### flex: 1 自动平分剩余空间
```css
.item {
  flex: 1;
}
```
多个子元素写 flex:1 → **自动等分宽度**

## 5. Flex完整响应式案例（三列→两列→单列）
```css
.list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
.item {
  width: 31%; /* 电脑三列 */
}

/* 平板两列 */
@media (max-width:1024px){
  .item {
    width: 48%;
  }
}

/* 手机单列 */
@media (max-width:768px){
  .item {
    width: 100%;
  }
}
```

## 6. Flex布局优缺点
✅ 优点
- 代码简单、兼容性极好
- 自动适配、自动挤压、自动换行
- 适合不规则、流式布局

❌ 缺点
- **一维布局**，无法同时精细控制行和列

---

# 三、Grid 网格布局（最整齐、最强大）
## 1. Grid布局介绍
- **二维布局系统**：**同时控制行 + 列**
- 页面最规整、最工整
- 适合：官网布局、卡片展示、相册、商品布局

## 2. 开启Grid布局
```css
.container {
  display: grid;
}
```

## 3. Grid核心属性详解

### ① grid-template-columns 定义列数
```css
/* 三等分三列 */
grid-template-columns: repeat(3,1fr);

/* 两等分两列 */
grid-template-columns: repeat(2,1fr);

/* 单列 */
grid-template-columns: 1fr;
```
- `fr`：剩余空间自动平分单位

### ② grid-template-rows 定义行数
```css
grid-template-rows: 100px 200px;
```

### ③ gap 间距
```css
gap: 20px;
```

## 4. Grid万能响应式代码
**电脑3列、平板2列、手机1列**
```css
.grid-box {
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 20px;
}

/* 平板 */
@media (max-width:1024px){
  .grid-box {
    grid-template-columns: repeat(2,1fr);
  }
}

/* 手机 */
@media (max-width:768px){
  .grid-box {
    grid-template-columns: 1fr;
  }
}
```

## 5. Grid布局优点
✅ 真正二维布局  
✅ 布局极度整齐  
✅ 自动等分、不用算宽度  
✅ 响应式代码极简  

## 6. Grid布局缺点
不适合**不规则、自由排列**的内容

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
