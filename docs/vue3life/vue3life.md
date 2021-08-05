# Vue3 生命周期

## Vue3 生命周期,必须写在 setup 里面,然后 reactive 外面

```bash
beforeCreate ===  setup()
created === setup()
beforeMount === onBeforeMount()
mounted === onMounted()
beforeUpdate === onBeforeUpdate()
updated === onUpdated()
beforeDestroy === onBeforeUnmount()
destroyed === onUnmounted()
activated === onActivated()
deactivated === onDeactivated()
errorCaptured === onErrorCaptured()
```

## 在此基础上又新增加了两个

```bash
onRenderTracked
onRenderTriggered
```

> 这两个钩子函数都会接到一个参数 e,这个 e 返回组件更新的所有信息

```html
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
  </div>
</template>

<script>
  //ref接收一个参数 返回一个响应式对象
  //computed是一个函数接收一个参数是函数
  import { ref, computed, reactive, toRefs, onMounted } from "vue";
  export default {
    setup() {
      onRenderTriggered((e) => {
        console.log(e);
      });
      onMounted(() => {
        console.log("挂在了");
      });
      const data = reactive({
        count: 0,
        double: computed(() => {
          return data.count * 2;
        }),
        changecount: () => {
          data.count++;
        },
      });
      const result = toRefs(data);
      return {
        ...result,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```
