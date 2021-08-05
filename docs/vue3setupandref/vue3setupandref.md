# Vue3.0 之 setup,ref

Vue3.0 解决的问题就是封装

以前数据的方法和数据不是写在一起看起来非常不方便。现在写在了一起，方便很多。

## setup 是 created 之前就会执行的声明周期函数

```javascript
export default {
  setup() {},
};
```

## ref 和 computed

- ref 的主要作用就是定义数据

- ref 它接收一个参数作为值,然后返回一个响应式对象

- `要是想改变ref的值必须改变它里面有个属性value,否贼不起作用`

```html
//ref接收一个参数 返回一个响应式对象
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
  </div>
</template>

<script>
  import { ref } from "vue"; //ref接收一个参数 返回一个响应式对象  //computed是一个函数接收一个参数是函数
  export default {
    setup() {
      const count = ref(0);
      const changecount = () => {
        count.value++; //更新值就是value,渲染的时候就是count
      };
      return {
        count,
        changecount,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

## computed 作用就是对数据的二次加工,必须有返回值

- `computed(()=>{}) 里面必须嵌套函数` 必须有返回值

```html
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
  </div>
</template>

<script>
  import { ref, computed } from "vue"; //ref接收一个参数 返回一个响应式对象  //computed是一个函数接收一个参数是函数
  export default {
    setup() {
      const count = ref(0);
      const double = computed(() => {
        return count.value * 2;
      });
      const changecount = () => {
        count.value++; //更新值就是value,渲染的时候就是count
      };
      return {
        count,
        double,
        changecount,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```
