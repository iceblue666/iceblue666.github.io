---
title:webpack的Bug
time:2021-02-19 22:08:00
categories:webpack,前端
tags:webpack,Bug
summary:遇到的一些webpack的坑，记下来
---

[TOC]

# webpack的Bug

## 错误

### 1. css顺序错误

解析是逆向的，自下而上

这个不行

```js
config.module.rules.push({
    test: /\.styl/,
    use: [
        MiniCssExtractPlugin.loader,
        'postcss-loader',
        'css-loader',
        'stylus-loader'
    ]
})
```

这个行

```js
config.module.rules.push({
    test: /\.styl/,
    use: [
        MiniCssExtractPlugin.loader,
        'css-loader',
        'postcss-loader',
        'stylus-loader'
    ]
})
```

### 2. module.exports

​	不要写成`module.export`

### 3. rules里面的test是正则，不要手贱加引号变成字符串

如下找不出原因，还看到模块没有被loader处理，看着还很对。

```js
config.module.rules.push({
    test: '/\.styl/',
    use: [
        MiniCssExtractPlugin.loader,
        'css-loader',
        'postcss-loader',
        'stylus-loader'
    ]
})
```

### 4. [待解决]vue-style-loader失效

https://blog.csdn.net/vv_bug/article/details/108148263

消极办法：回退css-loader到v3

修改配置：

```
{
    loader: 'css-loader',
    options: {
        esModule: false
    }
}
```