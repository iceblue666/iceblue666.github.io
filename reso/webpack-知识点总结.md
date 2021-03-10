---
title:webpack的Bug
time:2021-03-02 15:43:00
categories:webpack,前端,总结
tags:webpack,优化
summary:webpack基本知识总概述，方面齐全，有个印象
---

[TOC]

# webpack总结

## 1. entry

可能是单入口，可能多入口

多入口选择两个HtmlWebpackPlugin，就出来两个html。否则，默认会把两个入口的文件都插入在默认的index.html

## 2. module

### 2.1 import解析模块时

**解析相对路径**

1. 查找相对当前模块的路径下是否有对应文件或文件夹
2. 是文件则直接加载
3. 是文件夹则继续查找文件夹下的 package.json 文件
4. 有 package.json 文件则按照文件中 `main` 字段的文件名来查找文件
5. 无 package.json 或者无 `main` 字段则查找 `index.js` 文件

**解析模块名**

查找当前文件目录下，父级目录及以上目录下的 `node_modules` 文件夹，看是否有对应名称的模块

**解析绝对路径**

直接查找

### 2.2 resolve

`alias`---起别名，**方便写路径**

```
alias: {
  utils: path.resolve(__dirname, 'src/utils') // 这里使用 path.resolve 和 __dirname 来获取绝对路径
}
```

`extensions`---忽略扩展名，简化写代码路径

```
extensions: ['.wasm', '.mjs', '.js', '.json', '.jsx'],
// 这里的顺序代表匹配后缀的优先级，例如对于 index.js 和 index.jsx，会优先选择 index.js
```

## 3. loader

**resource和issuer**

举个例子：在 /path/to/app.js 中声明引入 `import './src/style.scss'`，`resource` 是「/path/to/src/style.scss」，`issuer` 是「/path/to/app.js」，规则条件会对这两个值来尝试匹配。

**字段：**

- `{ test: ... }` 匹配特定条件
- `{ include: ... }` 匹配特定路径
- `{ exclude: ... }` 排除特定路径
- `{ and: [...] }`必须匹配数组中所有条件
- `{ or: [...] }` 匹配数组中任意一个条件
- `{ not: [...] }` 排除匹配数组中所有条件

## 4. plugins

**mode**

- development

  会启动NamedChunksPlugin 和 NamedModulesPlugin，主要是在HMR下提示内容chunk或者module名字

- production

  production 下会启动多个 plugins，分别是：

  - FlagDependencyUsagePlugin 在构建时给使用的依赖添加标识，用于减少构建生成的代码量。
  - FlagIncludedChunksPlugin 在构建时给 chunk 中所包含的所有 chunk 添加 id，用于减少不必要的 chunk。
  - ModuleConcatenationPlugin 构建时添加作用域提升的处理，用于减少构建生成的代码量，详细参考：[module-concatenation-plugin](http://webpack.js.org/plugins/module-concatenation-plugin/)。
  - NoEmitOnErrorsPlugin 编译时出错的代码不生成，避免构建出来的代码异常。
  - OccurrenceOrderPlugin 按使用的次数来对模块进行排序，可以进一步减少构建代码量。
  - SideEffectsFlagPlugin 在构建时给带有 Side Effects 的代码模块添加标识，用于优化代码量时使用。
  - TerserPlugin 压缩 JS 代码，参考：[Terser](https://terser.org/)。

**webpack.DefinePlugin**

定义变量，可以在业务代码里使用

**webpack-bundle-analyzer**

这个 plugin 可以用于分析 webpack 构建打包的内容，用于查看各个模块的依赖关系和各个模块的代码内容多少，便于开发者做性能优化。

## 5. 图片优化 & HTML &CSS

**图片优化**

url-loader

雪碧图

webp

**HTML**

HtmlWebpackPlugin压缩

CSS

postcss-loader---cssnano压缩

## 6. 构建优化

- 尽可能写全路径名，不让webpack自己查询
- 减少plugin消耗，有针对性
- 合适的devtool: ` eval-cheap-source-map`
- 