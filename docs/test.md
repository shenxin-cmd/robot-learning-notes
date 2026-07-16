# 测试页面

## 数学公式

机器人动力学：

\[
\tau=M(q)\ddot q+C(q,\dot q)\dot q+g(q)
\]

## Python代码

```python
import numpy as np

q=np.zeros(6)

print(q)
```
---

# 十三、Markdown常用写法

## 标题

markdown
# 一级标题
## 二级标题
### 三级标题

**重要内容**

`变量名`

*轻微强调*

```python
import numpy as np

q = np.zeros(2)
```

| 方法 | 优点 | 缺点 |
|---|---|---|
| P控制 | 简单 | 容易有稳态误差 |
| PD控制 | 抑制振荡 | 需要调参 |



- [x] 安装MuJoCo
- [x] 运行最小模型
- [ ] 读取关节位置
- [ ] 绘制轨迹

!!! note "说明"
    这里填写普通补充信息。

!!! warning "注意"
    这里填写容易出错的内容。

!!! danger "危险"
    这里填写可能导致真机损坏或实验失败的内容。

??? example "展开查看示例"
    这里填写可以折叠的代码或说明。

参见[机械臂运动学](./ros2/index.md)。