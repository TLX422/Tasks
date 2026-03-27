
# 📘 Git 学习笔记

> 记录 Git 的基本操作、常用命令以及协作流程。

---

## 📑 目录
1. [Git 是什么](#-git-是什么)
2. [安装与配置](#-安装与配置)
3. [基本操作流程](#-基本操作流程)
4. [分支管理简介](#-分支管理简介)
5. [远程协作](#-远程协作)
6. [常用命令速查表](#-常用命令速查表)
7. [遇到问题怎么办](#-遇到问题怎么办)

---

## 🔍 Git 是什么
Git 是一个**分布式版本控制系统**，用于跟踪文件的变化，方便多人协作开发。

---

## ⚙️ 安装与配置

### 安装 Git
- Windows：下载 [Git for Windows](https://git-scm.com/download/win)，安装后可使用 **Git Bash**
- macOS：`brew install git`
- Linux：`sudo apt install git`

### 首次配置
```bash
git config --global user.name "你的姓名"
git config --global user.email "你的邮箱"
```

---

🚀 基本操作流程

1. 克隆远程仓库

```bash
git clone <仓库地址>
```

2. 查看仓库状态

```bash
git status
```

3. 添加文件到暂存区

```bash
git add <文件名>      # 添加单个文件
git add .             # 添加所有改动
```

4. 提交到本地仓库

```bash
git commit -m "提交说明"
```

5. 推送到远程仓库

```bash
git push
```

✅ 完整提交示例

```bash
# 1. 查看当前状态
git status

# 2. 新建文件并编辑（例如 hello.md）
echo "# Hello 张三" > hello.md

# 3. 添加到暂存区
git add hello.md

# 4. 提交到本地
git commit -m "添加 hello.md 文件"

# 5. 推送到远程
git push
```

---

🌿 分支管理简介

查看分支

```bash
git branch          # 本地分支
git branch -a       # 所有分支（含远程）
```

创建并切换分支

```bash
git checkout -b 新分支名
```

切换分支

```bash
git checkout 分支名
```

合并分支

```bash
# 先切换到要合并到的分支（如 main）
git checkout main
git merge 被合并的分支
```

---

👥 远程协作

拉取最新代码

```bash
git pull
```

相当于 git fetch + git merge

推送新分支到远程

```bash
git push origin 分支名
```

提交 Pull Request (PR)

1. 在 GitHub 上点击 Compare & pull request
2. 填写说明，提交 PR
3. 等待审核与合并

---

📋 常用命令速查表

操作 命令
克隆仓库 git clone <url>
查看状态 git status
添加文件 git add <file>
提交 git commit -m "msg"
推送 git push
拉取 git pull
查看历史 git log --oneline
创建分支 git branch <name>
切换分支 git checkout <name>
合并分支 git merge <name>
查看远程仓库 git remote -v

---

🧩 遇到问题怎么办

提交错了怎么办？

· 回滚到上一个版本（保留改动）
  ```bash
  git reset --soft HEAD~1
  ```
· 彻底回滚（不保留改动）
  ```bash
  git reset --hard <commit-id>
  ```

出现冲突怎么办？

1. 执行 git pull 时提示冲突
2. 打开冲突文件，找到 <<<<<<< 标记
3. 手动保留需要的代码，删除冲突标记
4. 保存文件，执行：
   ```bash
   git add .
   git commit -m "解决冲突"
   git push
   ```

---

🎯 总结

Git 的学习需要多动手实践，从 clone → add → commit → push 开始，逐步掌握分支、合并、冲突解决等高级操作。熟练后可以尝试使用 VS Code 或 GitHub Desktop 等图形化工具提升效率。

---

笔记持续更新中… 🚀

```

---

你可以直接将以上内容保存为 `Git学习笔记.md`，然后使用 `git add`、`commit`、`push` 提交到仓库。如果还需要调整格式或补充内容，随时告诉我！
