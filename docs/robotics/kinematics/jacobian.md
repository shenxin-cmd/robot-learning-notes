---
title: 机械臂Jacobian基础
tags:
  - 机器人学
  - 运动学
  - Jacobian
---

# 机械臂Jacobian基础

## 1. 问题背景

机械臂关节速度如何影响末端速度？

## 2. 问题定义

给定关节角：

\[
q=[q_1,q_2,\ldots,q_n]^T
\]

末端位置：

\[
x=f(q)
\]

希望得到关节速度与末端速度之间的关系。

## 3. 核心原理

\[
\dot{x}=J(q)\dot{q}
\]

其中：

- \(q\)：关节角；
- \(\dot{q}\)：关节速度；
- \(x\)：末端状态；
- \(J(q)\)：Jacobian矩阵。

## 4. 最小实现

```python
import numpy as np


def numerical_jacobian(
    forward_kinematics,
    q: np.ndarray,
    epsilon: float = 1e-6,
) -> np.ndarray:
    """使用中心差分计算数值 Jacobian。"""
    if epsilon <= 0:
        raise ValueError("epsilon must be positive")

    q = np.asarray(q, dtype=float)
    x0 = np.asarray(forward_kinematics(q), dtype=float)

    jacobian = np.zeros((x0.size, q.size), dtype=float)

    for index in range(q.size):
        q_plus = q.copy()
        q_minus = q.copy()

        q_plus[index] += epsilon
        q_minus[index] -= epsilon

        x_plus = np.asarray(forward_kinematics(q_plus), dtype=float)
        x_minus = np.asarray(forward_kinematics(q_minus), dtype=float)

        jacobian[:, index] = (
            x_plus - x_minus
        ) / (2.0 * epsilon)

    return jacobian