<p align="center" style="font-size:20px; color:#666;">
  🔥  Markdown 进阶笔记  🔥
</p >  

## 📌 表格 —— 整齐排列数据

用 `|` 和 `-` 画表格，冒号 `:` 控制对齐。

```markdown
| 名字   | 年龄 | 城市     |
|--------|------|----------|
| 小明   | 18   | 北京     |
| 小红   | 20   | 上海     |
```

名字 年龄 城市
小明 18 北京
小红 20 上海

对齐小技巧：
:--- 左对齐，:---: 居中，---: 右对齐。

---

## ✅ 任务列表 —— 待办事项一目了然

在 - 后面加上 [ ] 或 [x]。

```markdown
- [x] 写完笔记
- [ ] 复习一遍
- [ ] 分享给朋友
```

-  写完笔记
-  复习一遍
-  分享给朋友

---

## 💻 代码块 —— 展示代码更漂亮

用三个反引号 ``` 包裹，可以指定语言（会高亮）。

```markdown
```python
print("Hello, Markdown!")
```
```

```python
print("Hello, Markdown!")
```

---

## 🔗 链接与图片

**链接**

- [文字](网址)  

例如：[Markdown语法教程](https://blog.csdn.net/2301_77569009/article/details/137957203?ops_request_misc=elastic_search_misc&request_id=8eee0e629f46cc1e215fdfd5f4d6e525&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-137957203-null-null.142^v102^pc_search_result_base7&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187) 

**图片**

- ![替代文字](图片地址)  

例如：
- ![小猫](https://img95.699pic.com/photo/60013/3202.jpg_wh860.jpg)

---

## 📝 引用 —— 强调别人的话或摘录

- 用 > 开头。

```markdown
> 这是引用内容。
> 可以多行。
```

这是引用内容。
可以多行。

引用里还可以嵌套列表、代码块。

---

## 📚 列表嵌套 —— 结构更清晰

**缩进两个空格就能嵌套。**

```markdown
1. 水果
   - 苹果
   - 香蕉
2. 蔬菜
   - 西兰花
```

1. 水果
   · 苹果
   · 香蕉
2. 蔬菜
   · 西兰花

---

高亮文字

```html
这是<mark>高亮</mark>效果。
```

这是<mark>高亮</mark>效果。


---

## 🧭 锚点链接 —— 页面内跳转

**给标题加个 {#id}，就能从别处跳转过来。**

```markdown
### 我的秘密基地 {#secret}

[跳去秘密基地](#secret)
```

---

## 📖 脚注 —— 补充说明

```markdown
Markdown[^1] 很好用。

[^1]: 一种轻量级标记语言。
```

Markdown[^1] 很好用。

---

## 😊 Emoji —— 让文字活泼起来

- 直接复制 🎉，或使用简码 :smile: → :smile:

常用：:heart: :heart:  :rocket: :rocket:  :zap: :zap:

---
