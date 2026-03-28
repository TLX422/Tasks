# 📝 Git 完整操作流程笔记
 
## 🔧 一、前期准备
### 1. 确认文件位置
- 打开 `E:\Git\Tasks` 文件夹
- 新建 `hello.md`，内容为 `# Hello 池海秀`
- 确保文件名是 `hello.md`（无 `.txt` 后缀）
> 如果看不到拓展名就点击查看！！！
---
### 2. 打开 Git Bash
- 找到 Git Bash 快捷方式，打开黑色命令行窗口
---
## 🚀 二、核心操作步骤
### 步骤 1：进入仓库目录
```bash
cd /e/Git/Tasks
```
>cd后面必须有空格
- 提示符变成  **MINGW64~/Tasks (main) ** → 进入仓库成功 ✅
  
### 步骤 2：配置 Git 身份（仅需一次）
 ```
bash
  
git config --global user.name "池海秀"
git config --global user.email "2938085760@qq.com"
```
 
>作用：让 Git 记录你的提交者身份
> 注意： --global  是两个减号， user.name / user.email  拼写不能错
 
 
 
### 步骤 3：添加文件到暂存区
``` 
bash
git add hello.md
 
 ```
> 作用：告诉 Git 要跟踪这个文件的修改
> 无报错 → 添加成功 ✅
 
 
 
### 步骤 4：提交到本地仓库
``` 
bash
git commit -m "添加hello.md文件"

```
 
>注意： -m  后必须加空格和英文双引号包裹的提交说明
>看到  1 file changed  → 提交成功 ✅
 
### 步骤 5：同步远程代码（解决冲突）
```
bash 
git pull origin main
 ```
 ```
> 作用：拉取 GitHub 上的最新代码，避免推送冲突
> 若弹出合并编辑界面：
1. 按  Esc  → 输入  :wq  → 回车（保存并退出）

2. 或直接按  Shift + Z + Z  快捷键退出

>若提示「未完成合并」：先执行  git commit -m "合并远程main分支"  收尾

### 步骤 6：推送到 GitHub 远程仓库
```
bash
  
git push origin main
``` 
```
 
>作用：把本地提交的代码同步到 GitHub 仓库
> 看到  main -> main  → 推送成功 ✅
> 若提示登录：按网页提示完成 GitHub 授权
 
 
 
## ✅ 三、验证结果
 
1. 网页验证：打开  https://github.com/TLX422/Tasks ，查看  hello.md  是否存在

2. 命令验证：
```
bash
  
git status
 ```
 ```
若显示：
plaintext
  
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
 
 
→ 本地与远程完全同步，操作完成 ✅
 
---
 
### 🎯 核心概念总结
 
- 本地仓库：你电脑里的  E:\Git\Tasks  文件夹
- 远程仓库：GitHub 上的  https://github.com/TLX422/Tasks 
-  add ：把文件加入 Git 跟踪列表
-  commit ：把修改保存到本地仓库
-  pull ：把远程代码同步到本地
-  push ：把本地代码同步到远程
 
