# setUp 使用 props

## 在 setUp 中使用 props

父组件

- 父组件

传递字符串和对象,监听 emit 发射过来的数据

```html
<template>
  <div>
    <ZiContent
      :message="message"
      :ziyuansu="ziyuansu"
      @fashe="changezi"
    ></ZiContent>
    父亲
  </div>
</template>

<script>
  import { reactive, toRefs } from "@vue/reactivity";
  import ZiContent from "./zi.vue";
  export default {
    components: {
      ZiContent,
    },
    setup() {
      const data = reactive({
        message: "父元素给的信息",
        ziyuansu: {
          name: "子元素对象",
          id: 1,
        },
        changezi(content) {
          console.log("收到数据了");
          data.ziyuansu.name = content;
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

- 子组件

> 通过 props 来传递数据，通过 emit 来发射,props 里面必须要声明,否则不出来

```html
<template>
  <div>
    {{ ziyuansu.id }}--- {{ message }} ---{{ ziyuansu.name }} 测试子元素
    <button @click="changeValue">改变父元素给子元素的值</button>
  </div>
</template>

<script>
  import { reactive, toRefs } from "vue";
  export default {
    props: {
      message: String,
      ziyuansu: {
        id: Number,
        name: String,
      },
    },
    setup(props, context) {
      const data = reactive({
        message: props.message,
        changeValue() {
          console.log("点击了");
          context.emit("fashe", "确实改变了");
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
