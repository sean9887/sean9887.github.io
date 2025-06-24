---
published: true
layout: post
title: "Euler Angles"
categories: Python]
tags: [Euler Angles]
---

## Yaw, Pitch, Roll 이란?

3차원 공간에서 물체의 방향(Orientation)을 표현하는 방식.
각각은 **자신의 축(Roll, Pitch, Yaw)**을 중심으로 회전하는 **회전 각도**를 의미.

<img src="/assets/img/euler_angles.png" alt="euler_angles" width="100%"/>


### 각 축의 정의

1. **Roll**
   - 물체가 **전방을 유지한 채 좌우로 회전**하는 것
   - 비행기로 비유하면 **날개를 중심으로 기체가 좌우로 기울어짐**
   - X축을 중심으로 회전 (오른손 법칙 기준)

<img src="/assets/img/roll.png" alt="roll" width="80%"/>


2. **Pitch**
   - 물체가 **상하로 고개를 드는 동작**
   - 비행기로 비유하면 **기수가 올라가거나 내려가는 동작**
   - Y축을 중심으로 회전

<img src="/assets/img/pitch.png" alt="pitch" width="80%"/>


3. **Yaw**
   - 물체가 **좌우로 방향을 트는 동작**
   - 차량이 **핸들을 좌우로 꺾을 때의 움직임**
   - Z축을 중심으로 회전

<img src="/assets/img/yaw.png" alt="yaw" width="80%"/>

### python 코드 예시

```python
import numpy as np

def euler_to_rotation_matrix(yaw, pitch, roll):
    # R_z (Yaw)
    Rz = np.array([
        [np.cos(yaw), -np.sin(yaw), 0],
        [np.sin(yaw),  np.cos(yaw), 0],
        [0,            0,           1]
    ])

    # R_y (Pitch)
    Ry = np.array([
        [ np.cos(pitch), 0, np.sin(pitch)],
        [ 0,             1, 0],
        [-np.sin(pitch), 0, np.cos(pitch)]
    ])

    # R_x (Roll)
    Rx = np.array([
        [1, 0,            0],
        [0, np.cos(roll), -np.sin(roll)],
        [0, np.sin(roll),  np.cos(roll)]
    ])

    # Combined rotation matrix (Z → Y → X)
    R = Rz @ Ry @ Rx
    return R

yaw = np.deg2rad(30)    # Z축 회전
pitch = np.deg2rad(45)  # Y축 회전
roll = np.deg2rad(60)    # X축 회전

R = euler_to_rotation_matrix(yaw, pitch, roll)
print(R)
```