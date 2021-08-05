# Vue3 reactive 和 toRefs

- 前面的数据都是分散的不太管理,于是出现了 reactive 组合封装的

- setup(){}必须要有

```html
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
  </div>
</template>

<script>
  import { ref, computed, reactive, toRefs } from "vue"; //ref接收一个参数 返回一个响应式对象  //computed是一个函数接收一个参数是函数
  export default {
    setup() {
      const data = reactive({
        count: 0,
        double: computed(() => {
          return data.count * 2;
        }),
        changecount: () => {
          data.count++;
        },
      });
      return {
        ...toRefs(data),
      };
    },
  };
</script>
<style lang="less" scoped></style>
```

> toRefs 是为了转化对象,否则显示的时候必须写 data.count 之类的。这样利用 toRefs 转化起来方便
