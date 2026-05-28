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
