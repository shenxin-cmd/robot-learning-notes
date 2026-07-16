---
date: 2026-07-16
categories:
  - 工具搭建
tags:
  - MkDocs
  - GitHub
  - Git
---
好的，这篇我建议作为你知识库的**第一篇正式博客/工程记录**，而不是简单记录“如何安装MkDocs”。因为它实际上包含了你以后机器人开发非常重要的一套工程能力：

* 环境管理（Conda）
* 文档工程（MkDocs）
* 版本控制（Git）
* 自动部署（GitHub Actions）
* 工程调试思维
* AI辅助工作流

我按照你的知识库风格，整理成可以直接放入：

```
docs/blog/setup-mkdocs-github.md
```

的 Markdown 文件。

---

```markdown
# 使用 MkDocs Material + GitHub Pages 搭建个人机器人学习知识库

> 日期：2026-07-16  
> 项目：robot-learning-notes  
> 目的：建立长期维护的机器人、人工智能、计算机知识库，并形成高效学习闭环

---

# 1. 为什么建立个人知识库？

随着机器人、大模型、强化学习等方向快速发展，仅依靠零散学习已经难以形成系统能力。

因此建立一个长期维护的个人知识库，用于：

- 记录学习过程；
- 总结技术原理；
- 保存代码实验；
- 记录项目经验；
- 沉淀Debug过程；
- 形成未来面试和科研的技术资产。


一个优秀的工程师不仅需要：

> 会写代码

更需要：

> 能够组织知识、管理项目、复现问题、总结经验。


因此，本知识库采用：

```

Markdown
+
MkDocs Material
+
Git
+
GitHub Actions
+
GitHub Pages

```

构建。

---

# 2. 最终工作流程

未来所有学习和项目记录遵循：

```

学习/实验
↓
整理Markdown笔记
↓
本地MkDocs预览
↓
Git提交版本
↓
GitHub自动部署
↓
在线知识库更新

```

即：

```

write → preview → commit → push → deploy

````

---

# 3. 环境搭建过程

## 3.1 创建Conda环境

为了避免不同项目之间Python依赖冲突，单独创建：

```powershell
conda create -n robot-blog python=3.11 -y
````

激活：

```powershell
conda activate robot-blog
```

检查：

```powershell
python --version
```

输出：

```
Python 3.11.x
```

---

# 4. 遇到的问题与解决方法

## 问题1：Conda Terms of Service错误

创建环境时出现：

```
CondaToSNonInteractiveError
Terms of Service have not been accepted
```

原因：

新版Anaconda要求用户确认默认channel服务条款。

解决：

执行：

```powershell
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main

conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r

conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/msys2
```

然后重新创建环境。

---

## 问题2：conda activate没有切换环境

现象：

虽然：

```powershell
conda activate robot-blog
```

但是：

```powershell
python
```

仍然来自：

```
D:\Python311\python.exe
```

原因：

PowerShell没有加载Conda初始化脚本。

解决：

```powershell
conda init powershell
```

关闭PowerShell重新打开。

验证：

```powershell
python -c "import sys;print(sys.executable)"
```

正确：

```
D:\Miniconda3\envs\robot-blog\python.exe
```

---

# 5. 安装MkDocs Material

安装：

```powershell
pip install mkdocs-material
```

检查：

```powershell
mkdocs --version
```

---

# 6. 创建MkDocs项目

项目结构：

```
robot-learning-notes

├── docs
│
├── mkdocs.yml
│
└── ...
```

启动：

```powershell
mkdocs serve
```

本地访问：

```
http://127.0.0.1:8000/
```

---

# 7. MkDocs目录管理

MkDocs通过：

```
mkdocs.yml
```

控制网页目录。

例如：

```yaml
nav:

  - 首页:
      - index.md

  - 机器人学:
      - robotics/index.md
      - 运动学:
          - robotics/kinematics/index.md
          - Jacobian:
              robotics/kinematics/jacobian.md
```

注意：

Linux环境中路径使用：

```
/
```

不要使用：

```
\
```

否则GitHub Actions可能失败。

---

# 8. Git版本管理

## 初始化Git

```powershell
git init
```

添加：

```powershell
git add .
```

第一次提交：

```powershell
git commit -m "initialize robot knowledge base"
```

连接Github：

```powershell
git remote add origin <repository-url>
```

上传：

```powershell
git push origin main
```

---

# 9. GitHub Actions自动部署

创建：

```
.github/workflows/deploy.yml
```

作用：

每次：

```
git push
```

自动：

```
Github服务器
    ↓
安装MkDocs
    ↓
生成网页
    ↓
部署Pages
```

因此以后无需手动上传网站。

---

# 10. 部署过程中遇到的问题

## 问题：GitHub Actions失败

错误：

```
Get Pages site failed
HttpError: Not Found
```

原因：

Github Pages没有完成初始化。

解决：

Settings

↓

Pages

↓

临时切换：

```
Deploy from branch
```

保存

↓

切回：

```
GitHub Actions
```

重新触发workflow。

---

# 11. 日常工作流程

以后学习机器人相关知识时：

## Step 1：学习

例如：

机械臂Jacobian。

记录：

* 概念
* 数学公式
* 推导
* 实验

---

## Step 2：整理Markdown

例如：

```
docs/robotics/kinematics/jacobian.md
```

结构：

```markdown
# Jacobian


## 1. 基本概念


## 2. 数学推导


## 3. Python实现


## 4. MuJoCo实验


## 5. 工程应用


## 6. 面试问题

```

---

## Step 3：本地检查

运行：

```powershell
mkdocs serve
```

检查：

* 图片
* 公式
* 代码
* 页面结构

---

## Step 4：提交

```powershell
git add .

git commit -m "docs: update jacobian notes"

git push
```

---

# 12. 如何使用AI提升学习效率

AI应该作为：

> 思考辅助工具

而不是：

> 替代学习工具。

---

# 12.1 学习前：让AI生成学习路线

错误：

```
什么是Jacobian？
```

更好的方式：

```
我是机器人专业研究生，
正在学习机械臂Jacobian。

请按照：
1. 数学基础
2. 机器人应用
3. Python实现
4. MuJoCo实验
5. 面试问题

设计学习路线。
```

---

# 12.2 学习中：让AI帮助理解

例如：

```
请结合机械臂末端速度控制解释Jacobian。

不要只给定义，
请说明：
为什么需要它？
如何计算？
如何用于控制？
```

---

# 12.3 编程时：AI辅助Debug

不要：

```
代码报错怎么办？
```

应该：

```
下面是我的代码。

目标：
实现机械臂IK。

环境：
Python3.11
PyTorch
MuJoCo

错误：
xxx

请分析：
1. 错误原因
2. 修改方案
3. 背后的原理
```

---

# 12.4 学习结束：AI整理知识

每天结束：

输入：

```
根据我的学习笔记，
帮我整理成MkDocs格式Markdown。

要求：
- 保留我的理解
- 补充遗漏知识
- 增加面试问题
- 增加代码案例
```

然后人工修改后提交。

---

# 13. AI工具使用原则

## 可以交给AI：

* 查询资料
* 生成模板
* Debug辅助
* 代码解释
* 格式整理

## 不应该完全交给AI：

* 核心算法理解
* 数学推导
* 项目架构设计
* 科研创新思考

目标：

```
AI提高效率
+
自己掌握能力
```

---

# 14. 当前知识库规划

```
robot-learning-notes

├── weekly
│   └── 每周学习总结


├── programming
│   ├── Python
│   ├── C++
│   └── Git


├── computer-science
│   ├── 数据结构
│   ├── 算法
│   └── 操作系统


├── machine-learning
│   ├── Machine Learning
│   ├── Deep Learning
│   └── PyTorch


├── robotics
│   ├── Kinematics
│   ├── Dynamics
│   ├── Control
│   └── ROS2


├── mujoco

├── projects
│   ├── Robot PingPong
│   └── Other Projects


└── debugging
    └── 问题记录
```

---

# 15. 总结

通过搭建这个知识库，完成了：

* Python环境管理
* Conda使用
* MkDocs文档工程
* Git版本管理
* GitHub Actions自动部署
* Markdown知识整理

未来所有机器人学习、科研项目、代码实验，都将在这个体系中持续积累。

最终目标：

建立一个属于自己的：

> Robotics + AI + Computer Science 技术知识库。

```

---

这篇建议你保存为：

```

docs/blog/setup-mkdocs-github.md

````

并且在 `mkdocs.yml` 加入：

```yaml
- 博客:
    - 搭建个人知识库: blog/setup-mkdocs-github.md
````

以后你每次遇到环境、工具、工程流程问题，都可以继续追加到：

```
docs/debugging/
```

这会逐渐变成你非常有价值的“工程踩坑数据库”。你今天搭建博客的过程，其实正好成为了你机器人开发学习路线里的第一个工程项目。
