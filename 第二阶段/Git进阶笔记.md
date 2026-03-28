# Git 团队协作标准流程

---
一、准备工作

1. 安装 Git + 配置身份

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

> Git 会把你每次提交都贴上“谁做的”标签，方便团队追溯代码历史。这个配置全局生效，一次搞定。

2. 生成 SSH 密钥（**推荐，免密码**）

```bash
ssh-keygen -t ed25519 -C "你的邮箱"
```

将 ~/.ssh/id_ed25519.pub 内容粘贴到 GitHub → Settings → SSH and GPG keys。

> SSH 就像一把专属钥匙，GitHub 存着你的公钥，你本地存着私钥。这样每次 push 都不用输密码，安全又方便。

3. 加入项目

-  项目负责人：仓库 → Settings → Collaborators → Add collaborator（输入对方 GitHub 用户名）
-  你：收到邮件/通知，接受邀请即可

> 项目需要授权才能写代码。负责人把你加入 Collaborators 列表，你就有权限直接推送到仓库，不用走 Fork 流程。

---

二、标准协作流程

1. 克隆仓库到本地

```bash
git clone git@github.com:团队名/项目名.git
cd 项目名
```

>把远程仓库的完整代码（包括所有历史）下载到你的电脑上，相当于“本地工作区”。

2. 同步最新代码（每次开工必做!!!）

```bash
git checkout main
git pull origin main
```

> 团队成员可能已经合入了新代码。开工前先拉取最新的 main 分支，保证你的代码基于最新版本，避免后面合并时出现大量冲突。

3. 新建功能分支（核心：不直接改 main）

```bash
git switch -c feat/登录功能   # 新建并切换
# 命名规范：类型/描述（feat/功能、fix/修复、docs/文档）
```

>main 分支是稳定版本，直接在上面改风险大。每个人在独立分支上开发，互不干扰，最后通过 Pull Request 审核合并。分支名要清晰，比如 feat/登录功能，别人一看就知道你在做什么。

4. 开发 + 提交（小步提交）

```bash
git add .
git commit -m "feat: 实现用户登录接口"
# 提交规范：类型: 简短说明（feat/fix/docs/refactor）
```

>add 把修改放进“暂存区”，commit 生成一个版本记录。提交信息要清晰，方便以后查看或回滚。用“类型: 说明”的格式，团队都能看懂。

5. 推送到远程

```bash
git push -u origin feat/登录功能   # -u 关联远程分支
```

>把你本地分支推到远程仓库，这样团队成员才能看到你的代码，也方便后续发起 Pull Request。-u 只需设置一次，下次直接用 git push 就行。

6. 发起 Pull Request（PR，协作核心）

1. 打开 GitHub 仓库 → 看到 Compare & pull request 按钮
2. base: main（要合并到的分支），compare: 你的分支
3. 写 PR 标题 + 描述：做了什么、解决什么问题、如何测试
4. 指定 Reviewer（代码审核人）→ Create pull request

> 是请求别人审核你的代码并合并到主分支。它是团队协作的关键：通过描述让审核人快速理解改动，通过讨论提升代码质量。base 是目标分支，compare 是你的分支。

7. 代码审查（Code Review）

· Reviewer 在 PR 页面评论、提修改建议
· 你在本地修改 → commit → push，PR 自动更新
· 所有评论处理完、CI 通过 → Reviewer Approve

>Code Review 能发现 bug、统一代码风格、分享知识。你只需继续 commit + push，PR 会自动刷新，不需要重新创建。

8. 合并 + 清理

· 点击 Merge pull request → 选择合并方式（推荐 Squash and merge）
· 合并后删除远程分支 + 本地分支：

```bash
git checkout main
git pull origin main
git branch -D feat/登录功能   # 删除本地分支
```

**🤔 为什么？**

· Squash and merge：把你在分支上的多个提交压缩成一个，历史干净。
· 删除分支：避免远程仓库和本地积累一堆过期的分支，保持整洁。

---

三、开源项目协作（Fork 流程）

1. 打开目标仓库 → 右上角 Fork（复制到你的账号）

>你没有原仓库的直接写权限，Fork 相当于在你的账号下创建一个副本，你可以随便改。

2. 克隆你自己的 Fork 仓库

```bash
git clone git@github.com:你的用户名/项目名.git
```

3. 添加上游（原项目）远程

```bash
git remote add upstream git@github.com:原团队/项目名.git
```

>origin 指向你自己的 Fork，upstream 指向原项目。这样你既能推送改动到自己的 Fork，又能从原项目拉取最新代码。

4. 同步上游最新代码

```bash
git fetch upstream
git checkout main
git merge upstream/main
```

5. 后续开发、提交、push 同前

PR 时 base 选原项目 main，compare 选你的分支。



