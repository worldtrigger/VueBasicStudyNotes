# Vue3 之 Vuex

> Vue3 里面使用 Vuex 必须会用到 useStore 模块

- 使用模块版本

- 不使用模块版本

## 不使用模块版本

- Vuex 里面的数据

```javascript
import { createStore } from "vuex";

export default createStore({
  state: {
    message: "初始数据",
  },
  mutations: {
    changemessage(state, value) {
      state.message = value;
    },
  },
  actions: {},
  modules: {},
});
```

- 使用 State 里面的数据

- 改变数据必须 commit 方法,而不能直接使用

```html
<template>
  <div>
    {{ message }}
    <button @click="changevuex">改变数据</button>
  </div>
</template>

<script>
  import { computed, reactive, toRefs } from "vue";
  import { useStore } from "vuex";
  export default {
    setup() {
      const Store = useStore();
      const data = reactive({
        message: computed(() => {
          return Store.state.message;
        }),
        changevuex() {
          Store.commit("changemessage", "改变数据了");
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

## 使用模块版本

### 新建模块

```javascript
const moduleA = {
  state: {
    message: "ModuleA 里面的信息",
  },
  mutations: {
    changemessage(state, value) {
      state.message = value;
    },
  },
  actions: {},
  getters: {},
};
export default moduleA;
```

### 在 Vuex 中使用

```javascript
import { createStore } from "vuex";
import OneContent from "./modules/One";
export default createStore({
  state: {},
  mutations: {},
  actions: {},
  modules: {
    ModuleA: OneContent,
  },
});
```

### 在组件里面使用

```html
<template>
  <div>
    {{ message }}
    <button @click="changevuex">改变数据</button>
  </div>
</template>

<script>
  import { computed, reactive, toRefs } from "vue";
  import { useStore } from "vuex";
  export default {
    setup() {
      const Store = useStore();
      const data = reactive({
        message: computed(() => {
          return Store.state.ModuleA.message;
        }),
        changevuex() {
          Store.commit("changemessage", "改变数据了");
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
