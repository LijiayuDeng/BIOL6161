# Git & GitHub 工作流与代码管理指南 (BIOL6161)

本文档总结了如何初始化 Git、连接 GitHub 以及日常管理代码和文件的全流程操作。您可以将这个文件作为备忘录。

---

## 1. 初始设置 (已完成)

以下是我们在最开始将本地文件夹连接到 GitHub 时所做的完整步骤。**对于这个文件夹，以下步骤已经完成，您不需要再次运行。**

```bash
# 1. 初始化 Git 仓库
git init

# 2. 设置您的 GitHub 用户名和邮箱 (一台电脑通常只需设置一次)
git config --global user.name "LijiayuDeng"
git config --global user.email "lichiayuteng@gmail.com"

# 3. 将所有文件添加到暂存区并进行第一次保存 (提交)
git add .
git commit -m "first commit"

# 4. 将默认分支重命名为 main
git branch -M main

# 5. 关联远程 GitHub 仓库
git remote add origin https://github.com/LijiayuDeng/BIOL6161.git

# 6. 将本地代码推送到云端 (第一次推送需要带 -u 参数，设定默认的上游分支)
git push -u origin main
```

---

## 2. 日常管理：我有了新的改动怎么办？(最常用)

当您在这个文件夹中**修改了原有文件**、**新建了文件** (比如写了新的笔记)，或者**删除了文件**后，您需要通过以下 **"经典三步曲"** 将更改同步到 GitHub 上：

### 第一步：告诉 Git 你要保存哪些改动 (Add)
```bash
# 最简单粗暴的方法：将当前文件夹下的所有改动都添加到暂存区
git add .

# (进阶) 如果您只想单独添加某个特定文件，例如：
# git add Lecture_Notes.md
```

### 第二步：给这次改动写个留言并正式保存 (Commit)
```bash
# -m 后面是您对这次改动的简短描述。写清楚改了什么，以后找起来方便。
git commit -m "update annotations in lecture 1" 
```

### 第三步：推送到 GitHub 云端 (Push)
```bash
# 因为第一次已经配置好了 -u，以后推送直接打 push 即可：
git push
```

---

## 3. 日常查询状态：我卡住了 / 不知道现在的进度怎么办？

Git 提供了非常有用的命令来查看当前状态。

### **最强排错命令：查看当前状态 (推荐经常使用)**
```bash
git status
```
*这个命令非常安全，它不会修改任何东西。它会用醒目的颜色告诉您：*
* *哪些文件被修改了但还没 `add` (红色)*
* *哪些文件已经 `add` 了但还没 `commit` (绿色)*
* *您的本地代码和云端相比有没有落后*

### **查看历史记录：我以前都提交了什么？**
```bash
# 查看详细的提交历史，按 q 退出
git log

# 查看精简版的历史 (只看一行摘要)
git log --oneline
```

---

## 4. 进阶场景处理

### 场景 A：我刚在本地修改了文件，但发现改错了想撤销 (还没 commit 前)
如果您不小心把代码改乱了，想恢复成上次 `commit` 时的干净样子：
```bash
# 撤销对某个特定文件的修改
git restore <文件名>  

# 例如：git restore Lecture_Notes.md
```

### 场景 B：我在别的电脑上提交了代码，或者在 GitHub 网页上直接修改了，如何同步到当前的这台电脑？
在开始一天的工作前，建议先拉取（下载）云端最新的代码，避免冲突：
```bash
git pull
```

### 场景 C：我想做一些实验性的改动，怕把主要作业搞坏？
您可以开一个“平行宇宙”（分支）来折腾：
```bash
# 创建并切换到一个叫 "experiment" 的新分支
git checkout -b experiment

# ... 您现在在这个分支里可以随便 add, commit 甚至 push ...

# 如果折腾完发现效果很好，想合并回主线 (main)：
git checkout main
git merge experiment
```
