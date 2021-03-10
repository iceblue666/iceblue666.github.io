[TOC]

# Vue问题

## 1. v-model父子组件双向绑定

https://www.xiaoboy.com/topic/vue-parent-child-communication-by-v-model.html

<input v-on:input="total=arguments[0]" :value="total">

## 2. 实现$emit和$on

```js
    class Bus {
        constructor(){
            this.callbacks = {};
        }
        $emit(name, args){
            if(this.callbacks[name]){
                this.callbacks[name].forEach((fn) => fn(args));
            }
        }
        $on(name, fn){
            this.callbacks[name] = this.callbacks[name] || [];
            this.callbacks[name].push(fn);
            this.print(); 
        }


    }

    var bus = new Bus();


    function on(){
        bus.$on('matter', function(msg){
            console.log(msg);
        })
    }
    function emit(){
        bus.$emit('matter', 'a msg from A');
    }

```

## 3. computed和watch的区别

**计算属性computed：**

- 支持缓存，只有依赖数据发生改变，才会重新进行计算
- 不支持异步，当computed内有异步操作时无效，无法监听数据的变化
- computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值
- 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个多对一或者一对一，一般用computed
- 如果computed属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法。

**侦听属性watch：**

- 不支持缓存，数据变，直接会触发相应的操作；
- watch支持异步；
- 监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；
- 当一个属性发生变化时，需要执行对应的操作；一对多；
- 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数：

watch的使用

**immediate：组件加载立即触发回调函数执行**

**deep: deep的意思就是深入观察，监听器会一层层的往下遍历，给对象的所有属性都加上这个监听器，但是这样性能开销就会非常大了，任何修改obj里面任何一个属性都会触发这个监听器里的 handler**

所以如果需要观察对象的属性，可以用字符串。如'obj.a.b'，就可以不用deep，减轻开销。

## 4. MVC和MVVM 开发模式

**MVC**

model（模型、数据）

controller（控制器）

view（视图，渲染）

**MVVM**

model（模型、数据）

viewmodel（核心调度，数据双向绑定）

view（视图，渲染）