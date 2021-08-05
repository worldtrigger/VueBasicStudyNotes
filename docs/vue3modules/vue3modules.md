# 模块

- Vue3 为了方便业务拓展。引入了模块的改变

## 自定义模块

```javascript
import { ref, onMounted, onUnmounted } from "vue";

function useMouseDownHooks() {
  let x = ref(0);
  let y = ref(0);
  onMounted(() => {
    document.addEventListener("click", function (e) {
      x.value = e.x;
      y.value = e.y;
    });
  });
  onUnmounted(() => {
    document.removeEventListener("click", function () {
      console.log("移除了");
    });
  });

  return {
    x,
    y,
  };
}

export default useMouseDownHooks;
```

## 组件里面引入模块

- 使用模块

```html
<template>
  <div>
    <span>{{count}}</span>
    <span>{{double}}</span>
    <div @click="changecount">点击增加</div>
    <span> x:{{x}} y:{{y}}</span>
  </div>
</template>

<script>
  import { ref, computed, reactive, toRefs, onMounted, watch } from "vue"; //ref接收一个参数 返回一个响应式对象  //computed是一个函数接收一个参数是函数
  import useMouseDownHooks from "../hooks/useMousedown";
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
        }
      );
      let { x, y } = useMouseDownHooks(); //开始赋值
      const result = toRefs(data);
      return {
        ...result,
        x,
        y,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

## 有的时候需要在模块里面互用数据

- 引入的模块 usehooks2.js

```javascript
import { ref } from "vue";

function useMouseDownHooks2() {
  let x = ref(200);
  let y = ref(2000);
  return {
    x,
    y,
  };
}

export default useMouseDownHooks2;
```

- 主模块

```javascript
import { ref, onMounted, onUnmounted } from "vue";
import UseHooks2 from "./usehooks2";
function useMouseDownHooks() {
  onMounted(() => {
    console.log(UseHooks2);
  });
  const { x, y } = UseHooks2();
  return {
    x,
    y,
  };
}

export default useMouseDownHooks;
```

- 组件里面使用的时候只会使用主模块

```html
<template>
  <div>{{ message }} --- {{ data2 }}</div>
  <div>{{ x }} ---{{ y }}</div>
</template>

<script>
  import { reactive, ref, toRefs } from "vue";
  import UseHooks from "../hooks/usehooks";
  export default {
    setup() {
      const data = reactive({
        message: "首页",
      });
      const data2 = ref("测试");
      let { x, y } = UseHooks(); //开始
      return {
        ...toRefs(data),
        x,
        y,
        data2,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

## 引用的模块里面要使用方法

- 引入的模块

```javascript
import { ref } from "vue";

function useMouseDownHooks2() {
  let x = ref(200);
  let y = ref(2000);
  return {
    x,
    y,
  };
}

export default useMouseDownHooks2;
```

- 主模块

```javascript
import { ref, onMounted, onUnmounted, reactive, toRefs } from "vue";
import UseHooks2 from "./usehooks2";
function useMouseDownHooks() {
  onMounted(() => {
    console.log(UseHooks2);
  });
  const { x, y } = UseHooks2();
  const data = reactive({
    printworld() {
      console.log("打印出来");
    },
  });
  return {
    x,
    y,
    ...toRefs(data),
  };
}

export default useMouseDownHooks;
```

- 组件使用(有所不同)

> 要是集成的话必须使用 value,通过它传递参数

```html
<template>
  <div>{{ message }} --- {{ data2 }}</div>
  <div>{{ x }} ---{{ y }}</div>
</template>

<script>
  import { onMounted, reactive, ref, toRefs } from "vue";
  import UseHooks from "../hooks/usehooks";
  export default {
    setup() {
      let ContentHooks = UseHooks(); //开始
      const data = reactive({
        message: "首页",
        x: ContentHooks.x,
        y: ContentHooks.y,
      });
      const data2 = ref("测试");
      onMounted(() => {
        console.log(ContentHooks);
        ContentHooks.printworld.value();
      });

      return {
        ...toRefs(data),
        ...ContentHooks,
        data2,
      };
    },
  };
</script>

<style lang="less" scoped></style>
```
