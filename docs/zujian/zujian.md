# 组件

Vue 的核心就在于组件,组件的作用就是:复用.

小到一个按钮,大到一个页面都可以是组件

## 组件的三元素

每个组件都必须包含三元素

- template(用来存放 html)

- script(用来写 js)

- style(用来写 css)

- 这里千万注意:组件必须都要大写

> 组件外面必须有一个包裹层,否则直接报错误

```html
<template>
  <div class="login">
    <header></header>
    <div class="loginbox_wrap">
      <main></main>
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
      };
    },
    components: {
      Header,
      Footer,
      Main,
    },
  };
</script>

<style lang="less" scoped>
  /*mobile*/
  @media (max-width: 767px) {
    .loginbox_wrap {
      width: 100%;
      min-height: calc(100vh - 200px - 73px);
      background: white;
    }
  }

  /*pad*/
  @media (min-width: 768px) and (max-width: 1024px) {
    .loginbox_wrap {
      width: 100%;
      min-height: calc(100vh - 108px - 150px - 50px);
      background: #f3f3f3;
      padding-top: 50px;
    }
  }

  /*desktop*/
  @media (min-width: 1025px) {
    .loginbox_wrap {
      width: 100%;
      min-height: calc(100vh - 108px - 150px - 50px);
      background: #f3f3f3;
      padding-top: 50px;
    }
  }
</style>
```

# 组件的引入必须三点

- 第一步:引入组件(import)

- 第二步:注册组件(components)

- 第三步:使用组件(自定义标签)

- 组件必须要大写

```javascript
<header>
  <div class="login">
    <Header></Header>
    <main></main>
    <footer></footer>
  </div>
</header>

<script>
  import Header from '@/pages/common/Header'
  import Footer from '@/pages/common/Footer'
  import Main from '@/pages/Login/components/Main'
  export default {
    data() {
      return {
        message: '登陆'
      }
    },
    components: {
      Header,
      Footer,
      Main
    }
  }
</script>

<style lang="less" scoped></style>
```
