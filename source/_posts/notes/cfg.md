---
title: cfg
date: '2022-5-14 7:40:00'
tags:
  - csgo
  - cfg
categories: csgo
cover: /img/csgo.jpg
abbrlink: 55a194b1
top_img: "#0f4c81"
---

## my常用启动项

```
-worldwide -tickrate 128 -novid -freq 300 -refreshrate 144 +exec zf.cfg
```

国服启动项：`-perfectworld` 

国际服启动项：`-worldwide`

## 空格大跳
```
alias +cjump "+jump; +duck" 
alias -cjump "-jump; -duck" 
bind "space" "+cjump"
```

## 侧键跳投
```
alias +jumpthrow"+jump;-attack;-attack2";
alias -jumpthrow -jump;
bind  mouse4+jumpthrow;
```
## 手臂
手臂模型上下＋左右晃动幅度：**cl_bobamt_vert 0.1 、cl_bobamt_lat 0.1**（直接0.1,多了恶心）

手臂模型向身体靠近幅度：**cl_bob_lower_amt (5~30)**

手臂长度：**viewmodel_fov 68**

