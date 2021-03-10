---
title:vuex
time:2021-02-27 20:05:00
categories:前端,vue,vuex
tags:vuex,vue
summary:vuex的简要说明，快速开发
---
# vuex

state、getter、mutations、actions、modules

state是状态保存

修改state的唯一方法是提交mutation，但是 mutations中的方法是同步的

**为什么必须是同步的？**

主要原因在于同步异步混合，devtools不容易调试追踪，实际上数据的改变是不会有错误的。

actions中可以提交mutations