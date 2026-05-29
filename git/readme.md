## Git 与 SVN 区别

Git 不仅仅是个版本控制系统，它也是个内容管理系统(CMS)，工作管理系统等。

如果你是一个具有使用 SVN 背景的人，你需要做一定的思想转换，来适应 Git 提供的一些概念和特征。

Git 与 SVN 区别点：

- **1、Git 是分布式的，SVN 不是**：这是 Git 和其它非分布式的版本控制系统，例如 SVN，CVS 等，最核心的区别。
- **2、Git 把内容按元数据方式存储，而 SVN 是按文件：**所有的资源控制系统都是把文件的元信息隐藏在一个类似 .svn、.cvs 等的文件夹里。
- **3、Git 分支和 SVN 的分支不同：**分支在 SVN 中一点都不特别，其实它就是版本库中的另外一个目录。
- **4、Git 没有一个全局的版本号，而 SVN 有：**目前为止这是跟 SVN 相比 Git 缺少的最大的一个特征。
- **5、Git 的内容完整性要优于 SVN：**Git 的内容存储使用的是 SHA-1 哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。

# Git 常用命令笔记（按使用流程整理）

## 一、基础概念

* 工作区：你正在编辑的文件
* 暂存区：准备提交的修改
* 本地仓库：已保存的版本记录
* 远程仓库：云端代码（如 GitHub）

---

## 二、基础流程（最重要）

```bash
修改文件
→ git add
→ git commit
→ git push
```

---

## 三、初始化仓库

```bash
git init
```

作用：创建一个新的 Git 仓库

---

## 四、查看状态

```bash
git status
```

作用：查看文件修改情况（是否已添加/提交）

---

## 五、添加修改

```bash
git add 文件名
git add .
```

作用：将修改加入暂存区

---

## 六、提交版本

```bash
git commit -m "提交说明"
```

作用：保存当前版本快照

---

## 七、查看历史记录

```bash
git log
git log --oneline
```

作用：查看提交历史

---

## 八、远程仓库操作

### 1. 添加远程仓库

```bash
git remote add origin 仓库地址
```

### 2. 推送代码

```bash
git push -u origin main   # 第一次
git push                  # 之后
```

### 3. 拉取代码

```bash
git pull
```

---

## 九、分支操作

### 查看分支

```bash
git branch
```

### 创建分支

```bash
git branch dev
```

### 切换分支

```bash
git switch dev
```

### 创建并切换

```bash
git switch -c dev
```

### 合并分支

```bash
git switch main
git merge dev
```

---

## 十、撤销操作

### 撤销工作区修改

```bash
git restore 文件名
```

### 撤销 add

```bash
git reset 文件名
```

### 回退提交

```bash
git reset --soft HEAD~1   # 保留修改
git reset --hard HEAD~1   # 删除修改（危险）
```

---

## 十一、常用开发流程

```bash
git pull
git switch -c feature
# 开发代码
git add .
git commit -m "完成功能"
git push -u origin feature
```

---

## 十二、核心常用命令（必记）

```bash
git init
git status
git add .
git commit -m "msg"
git log --oneline
git pull
git push
git branch
git switch 分支名
git merge 分支名
```

---

## 十三、一句话总结

* `add`：加入暂存区
* `commit`：保存版本
* `push`：上传远程
* `pull`：拉取更新
* `branch`：分支管理
* `merge`：合并代码

---
