# 路由

- Vue-router 通过管理 URL 来实现 url 和组件的对应。通过 url 来进行组件之间的切换

# Vue-Router 两种模式

## 第一种 hash 模式,就是地址栏 url 中的#符号,一般默认就是 hash

```html
<p>例如这个URL http://www.abc.com/#/home</p>
<p>那么他的hash值就是为/#/home</p>
<p>hash值好处就是对后端完全没有影响,改变hash值不会重新加载页面</p>
```

## history(就是平常的 url)

```html
<p>但是在2.x版本中打包后会出现一片空白</p>
```

# Vue-router 的使用

## 纯静态加载组件

```javascript
import Vue from "vue"; //引入vue
import Router from "vue-router"; //引入router
import HelloWorld from "@/components/HelloWorld"; //加载组件

Vue.use(Router); //使用组件

//路由的核心文件
export default new Router({
  routes: [
    {
      path: "/",
      name: "HelloWorld",
      component: HelloWorld,
    },
  ],
});
```

## 纯动态引入,按需加载(常用)

```javascript
import Vue from "vue";
import Router from "vue-router";
const Index = import("@/views/Index.vue"); //首页
Vue.use(Router);

export default new Router({
  mode: "history",
  base: process.env.BASE_URL,
  routes: [
    {
      path: "/",
      name: "Index",
      component: () => Index,
    },
  ],
});
```

## html 要是想跳转的话,通过链接

```html
<router-link to="/xxx" tag="li" event="mouseover"></router-link>
```

> 选中了以后他会自动给当前路由加载一个类名,表示选中的状态

```html
<p>router-link-active 全局匹配 即path名包含在所有路由都会匹配</p>
<p>router-link-exact-active 精确匹配 即点击哪个路由，哪个被匹配。</p>
```

> 如果你想改变这个类名可以在下面改变

```javascript
export default new Router({
  mode: "history",
  base: process.env.BASE_URL,
  linkActiveClass: "is-active", //这样选中的类名就改变了就变成router-link-active
  routes: [
    {
      path: "/",
      name: "Index",
      component: () => Index,
    },
  ],
});
```

## 404 页面,必须把\*放在最后,否则他会直接 404

```javascript
import Vue from "vue";
import Router from "vue-router";
const Index = import("@/views/Index.vue"); //首页
Vue.use(Router);

export default new Router({
  mode: "history",
  base: process.env.BASE_URL,
  routes: [
    {
      path: "/",
      name: "Index",
      component: () => Index
    }，
   {
      path: "*",
      name: "Index",
      component: () => Index
    }
  ]
})
```

## 重定向 redirect 就是用户访问的是 A 网址,实际跳转到 B

- 重定向

```javascript
{
 path:'/goback/:username/:id',
 redireact: '/Hi/:username/:id'
 //也可以跳转到name
 // redireact: {name:'home'} 前提是必须有name属性
 //也可以使用函数比如
 /*
 redirect:(to)=>{
   if(to.path==="123")
   {
     return {name:'home'} // 或者path之类的或者路径
   }
 }
 */
```

## 别名

- 关键字 alias

- 它不同于重定向,它仅仅是换了个名字

```javascript
{
     path:'/Hi/:username/:id',
     component:Hi,
     alias:"gofor"  //前面不要加/
}
```

> 前端访问 gofor 实际访问的还是那个 hi 路由

```html
<router-link to="/gofor">gofor</router-link>
```

# 子路由

> 比如我们想 /h1/hi1 这样的,我们管这个叫子路由

## 子路由必须要在路由是 hi 里面放一个 routerview

```html
<template>
  <div>
    <div class="hello">{{msg}}</div>
    <router-view></router-view>
  </div>
</template>
```

## 然后在里面写 children 属性,千万记住了子路由不能加 /

```javascript
{
      path:'/hi',
      name:"Hi",
      component:Hi,
      children:[
        {path:" ",component:Hi,name:"Hi"},
        {path:"hi1",component:Hi1,name:"Hi1"},
        {path:"hi2",component:Hi2,name:"Hi2"},
      ]
    }
```

# 单页面由多个路由组成

- routerview

## 写好位置

```html
<router-view></router-view>
<router-view
  name="left"
  style="width:50%;height:400px;background:red;float:left"
></router-view>
<router-view
  name="right"
  style="width:50%;height:400px;background:blue;float:left;"
></router-view>
```

## 在路由里面设置,记住一定是 components

```javascript
import Vue from "vue";
import Router from "vue-router";
import HelloWorld from "@/components/HelloWorld";
import Hi from "@/components/Hi";
import Hi1 from "@/components/Hi1";
import Hi2 from "@/components/Hi2";
Vue.use(Router);

export default new Router({
  routes: [
    {
      path: "/",
      name: "HelloWorld",
      //这里就是要加载你要显示的组件 对应name
      components: {
        default: HelloWorld,
        left: Hi1,
        right: Hi2,
      },
    },
  ],
});
```

# 路由嵌套

- children

就是在已知的 1 级页面下面有 2 级页面

```html
<template>
  <div>
    <div>展示用户列表页</div>
    <router-link to="/userList/userInfo">用户基本信息页</router-link>
    //to后必须用绝对地址
    <router-link to="/userList/changePaw">修改密码页</router-link>
    <div>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
  export default {
    name: "userList",
    data() {
      return {
        msg: "",
      };
    },
  };
</script>

<style scoped></style>
```

- 比如在列表页/userlist/userinfo

```javascript
import Vue from "vue";
import Router from "vue-router";
import userList from "@/components/userList";
import userInfo from "@/components/userInfo";
import changePaw from "@/components/changePaw";

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: "/userList",
      name: "userList",
      component: userList,
      children: [
        {
          path: "userInfo",
          name: "userInfo",
          component: userInfo,
        },
        {
          path: "changePaw",
          name: "changePaw",
          component: changePaw,
        },
      ],
    },
  ],
});
```

# 重点开始滚动行为,当用户滚动后加载路由

> 要是有记录滚动条就从记录开始,要是没记录就从 0 开始,要是想从 0 开始,直接 return {x:0,y:0}

```javascript
export default new Router({
  mode: "history",
  base: process.env.BASE_URL,
  scrollBehavior(to, from, savePosition) {
    console.log(to);
    console.log(from);
    console.log(savePosition);
    //如果滚动条有位置就记住，没有就是从0开始
    // if (savePosition) {
    //   return savePosition;
    // } else {
    //   return { x: 0, y: 0 };
    // }
    return {
      x: 0,
      y: 0,
    };
  },
  routes: [
    {
      path: "/",
      name: "home",
      component: Home,
    },
    {
      path: "/about",
      name: "about",
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => About,
    },
    {
      path: "/index",
      name: "Index",
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => Index,
    },
  ],
});
```

## 如果希望刷新后滚动条从 0 开始

```html
只有在最外层export default 的最外面 写代码

<script>
  window.addEventListener("beforeunload", (e) => {
    window.scrollTo(0, 0);
  });
  export default {
    xxxxxxxxxxxx,
  };
</script>
```
