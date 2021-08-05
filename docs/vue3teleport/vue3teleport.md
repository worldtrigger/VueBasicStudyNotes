# Teleport 挂载

## 使用场景

- 有的时候弹出框需要挂载在顶层另外一个 DOM 节点

- 而不是挂载到顶层 DOM 节点

## 使用它的作用很简单,想把组件挂载到哪个节点都行

- 要挂载的组件,挂载到 id 是 modal2 的组件上,起名必须是 teleport 来命名

```html
<template>
  <div>
    <teleport to="#modal2"> 这就是中间层 </teleport>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: "中间层",
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

- 父组件

```html
<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <div id="modal2"></div>
  <router-view />
</template>

<style lang="less"></style>
```
