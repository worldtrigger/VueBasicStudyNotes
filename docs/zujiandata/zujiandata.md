# 组件之间的数据传递

## 组件之间数据传递的方式有 4 种

- 父子组件

- Vuex

- 总线机制

- 卡槽

## 父子组件

父子组件船值就两点

- 传递数据 props

- 子组件改变数据

## 父组件

- 通过绑定来传递数据,这样就把数据传递过去了,监听子组件传递过来的事件,来调用父组件的方法改变值

```html
<template>
  <div class="login">
    <header></header>
    <div class="loginbox_wrap">
      <main :info="message" :infoflag="flag" @changeflag="switchflag"></main>
    </div>
    <footer></footer>
  </div>
</template>

<script>
  import Header from "@/pages/common/Header";
  import Footer from "@/pages/common/Footer";
  import Main from "@/pages/Login/components/Main";
  export default {
    data() {
      return {
        message: "登陆",
        flag: false,
      };
    },
    components: {
      Header,
      Footer,
      Main,
    },
    methods: {
      switchflag(content) {
        this.flag = content;
      },
    },
  };
</script>

<style lang="less" scoped></style>
```

## 子组件

- 通过 props 接受数据

- 发射出一个自定义事件来改变父元素的值,然后传递新的值,子组件永远不能直接改变父元素的值

```html
<template>
  <div class="login">
    {{info}} ----{{infoflag}}
    <button @click="changedata"></button>
  </div>
</template>
<script>
  export default {
    props: ["info", "infoflag"],
    data() {
      return {
        message: "子组件",
      };
    },

    methods: {
      changedata() {
        this.$emit("changeflag", true);
      },
    },
  };
</script>
<style></style>
```

- 也可以有第二种父元素传递过的值验证

- 下面的例子说明两个值必须要传递进来,一个数字,一个布尔

```html
<template>
  <div class="login">
    {{info}} ----{{infoflag}}
    <button @click="changedata"></button>
  </div>
</template>
<script>
  export default {
    props: {
      info: {
        type: Number,
        required: true,
      },
      infoflag: {
        type: Boolean,
        required: true,
      },
    },
    data() {
      return {
        message: "子组件",
      };
    },

    methods: {
      changedata() {
        this.$emit("changeflag", true);
      },
    },
  };
</script>
<style></style>
```

## Vue 总线机制

- 总线机制主要用在爷孙组件或者隔了 N 代不好传值,这样省的一层层发射

### 第一步创建总线 挂载到 Bus 属性上

```javascript
Vue.prototype.bus = new Vue();
```

### 第二步孙子组件发射出去自定义事件

```javascript
this.bus.$emit("change", "想改变的值");
```

### 第三步爷爷组件监听此事件

```javascript
let _this = this;
this.bus.$on("change", function (content) {
  _this.xxx = content;
});
```

## Vue2 中的卡槽和 Vuex 后面在说
