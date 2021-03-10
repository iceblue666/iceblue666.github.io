---
title:Vue的坑
time:2021-03-04 16:56:00
categories:前端,总结
tags:前端,知识点汇总,学习,Vue,坑
summary:Vue中有挺多坑的，记录一下吧
---
# Vue的坑

## 1. vue检测prop和data是否变化，不变化直接复用原来的组件

```vue
<tabs :value="value" @change="changeTabValue">
    <tab label="tab1" index="1">
    	<span>tab content 1 {{ sth }}</span>
    </tab>
    <tab label="tab3" index="3">
      	<span>tab content 3</span>
     </tab>
</tabs>
<input v-model="sth" />
```

会发现改变input时候，tab1渲染出来的span里的内容没变，这就是因为Vue检测prop和data是否变了，而没管插槽。

### 2. 记一下

1. 用<transition>组件进行过渡的时候，屏幕会闪一下，可能是mode问题，默认是"in-out"，改成"out-in"就好了。

2. 既然 Vuex 的 store 中的状态是响应式的，那么当我们变更状态时，监视状态的 Vue 组件也会自动更新。这也意味着 Vuex 中的 mutation 也需要与使用 Vue 一样遵守一些注意事项：
   1. 最好提前在你的 store 中初始化好所有所需属性。
   2. 当需要在对象上添加新属性时，你应该

- 使用 `Vue.set(obj, 'newProp', 123)`, 或者

- 以新对象替换老对象。例如，利用[对象展开运算符](https://github.com/tc39/proposal-object-rest-spread)我们可以这样写：

  ```js
  state.obj = { ...state.obj, newProp: 123 }
  ```