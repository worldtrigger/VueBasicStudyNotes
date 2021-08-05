# Vue3 卡槽的使用和传值

## 使用 v-slot 来命名后边跟卡槽要传递过来的值

## 默认卡槽

- 父组件

```html
<template>
  <div>
    <ZiContent>
      <p>传递过来</p>
    </ZiContent>
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

- 子元素

```html
<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  import { reactive, toRefs } from "vue";
  export default {
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

<style lang="scss" scoped></style>
```

## 具名卡槽

- 父元素,必须加上 template 包裹层

```html
<template>
  <div>
    <ZiContent>
      <template v-slot:header>
        <p>传递过来带有名字的卡槽</p>
      </template>
    </ZiContent>
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

- 子元素

```html
<template>
  <div>
    <slot name="header"></slot>
  </div>
</template>

<script>
  import { reactive, toRefs } from "vue";
  export default {
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

<style lang="scss" scoped></style>
```

## 卡槽之间传值

### 单一数据

- 父组件

- 必须通过 scope

```html
<template>
  <div>
    <ZiContent>
      <template v-slot:header="scope">
        <p>传递过来带有名字的卡槽--{{ scope.color }}</p>
      </template>
    </ZiContent>
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

```html
<template>
  <div>
    <slot name="header" :color="color"></slot>
  </div>
</template>

<script>
  import { reactive, toRefs } from "vue";
  export default {
    setup(props, context) {
      return {
        color: "red",
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

### 传递对象

- 父组件

```html
<template>
  <div>
    <ZiContent>
      <template v-slot:header="scope">
        <p>
          传递过来带有名字的卡槽--{{ scope.color.message }}--{{
          scope.color.message2 }}
        </p>
      </template>
    </ZiContent>
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

```html
<template>
  <div>
    <slot name="header" :color="{ message, message2 }"></slot>
  </div>
</template>

<script>
  import { reactive, toRefs } from "vue";
  export default {
    setup(props, context) {
      return {
        color: "red",
        message: "子组件传递过来的",
        message2: "子组件传递过来的第二个",
      };
    },
  };
</script>

<style lang="less" scoped></style>
```
