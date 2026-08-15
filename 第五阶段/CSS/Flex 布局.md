# Flex 弹性布局

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
