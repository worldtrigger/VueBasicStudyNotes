# Vue3Watch

> 在 Vue3 里面使用 watch 必须引用

## watch 里面也是一个函数，它里面必须要接收两个参数

- 第一个参数就是数组,监听要改变的值

里面分成两类,数据要是 ref 的就直接使用,如果是 reactive 或者 Store 里面的数据就必须要使用一个函数，里面返回值写 xxx.数据名称

- 第二个参数就是回调函数

里面有两个参数,第一个就是新的值,第二个就是老的值

```html
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
  </div>
</template>

<script>
  import { ref, computed, reactive, toRefs, onMounted, watch } from "vue"; //ref接收一个参数 返回一个响应式对象  //computed是一个函数接收一个参数是函数
  export default {
    setup() {
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
      let data2 = ref("哈哈");
      watch(
        [
          data2,
          () => {
            return data.count;
          },
          () => {
            return data.double;
          },
        ],
        (newval, oldval) => {
          console.log(newval);
          console.log(oldval);
          console.log(data2.value); //只能这样获取value
        }
      );
      const result = toRefs(data);
      return {
        ...result,
      };
    },
  };
</script>
<style lang="less" scoped></style>
```
