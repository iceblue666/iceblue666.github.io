# 坑

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

### 2. 如何解决vue中markdown解析渲染

https://blog.csdn.net/qq_34691227/article/details/105845460