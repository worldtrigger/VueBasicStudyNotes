# 路由参数

- 动态路径传参数

> 比如我们要传递的路径 /hi/haha/123 第一个是组件名,第二个,第三个是参数

## 路由里面配置参数

> 看路径 利用冒号绑定好参数

```javascript
{
      path:'/Hi/:username/:id',
      name:"Hi",
      component:Hi,
      children:[
        {path:"hi1",name:"Hi1",component:Hi1},
        {path:"hi2",name:"Hi2",component:Hi2},
      ]
    }
```

- 组件里输出的时候

```javascript
{
  {
    $route.params.username;
  }
}

{
  {
    $route.params.id;
  }
}
```

## 路由跳转参数的两种方法

- 利用 query 方式传递参数

- 利用 params 方式传递参数

## 利用 query 传递参数

- 刷新后页面参数不丢失

```html
<script>
  传参:
  this.$router.push({
          path:'/xxx'
          query:{
            id:id
          }
        })

  接收参数:
  this.$route.query.id
</script>
```

## 利用 params 传递参数

```html
<script>
  传参:
  this.$router.push({
          name:'xxx'
          params:{
            id:id
          }
        })

  接收参数:
  this.$route.params.id
</script>
```

## Vue2.x 里面的路由拦截

- 第一种 全局匹配 beforeEach

- 第二种单个路由下面写配置 beforeEnter

- 第三种就是组件里面写钩子函数 beforeRouterEnter

## 全局匹配

> 一般情况 我们管这个叫路由守卫,简称全拦,他一般有 3 个参数,to,from,next 表示通过才跳转。一般写在 main.js 里面

> to 表示要跳转的路径信息,from 要是从哪里来的信息,next 表示路由控制的参数,通过与否

> 代码

```javascript
router.beforeEach((to, from, next) => {
  // 定义一个列表
  const auth = ["/about", "/", "/login"];
  if (auth.includes(to.fullPath)) {
    // 如果to.fullPath 在这个列表里,就验证token, 否则放行
    // console.log('验证token')
    if (to.path == "/about") {
      next({
        path: "/login",
        query: {
          id: "哈哈",
        },
      }); // 当没有token就next到login页面
    } else {
      next(); // 有就放行
    }
  } else {
    next();
  }
});
```

## 单个路由下配置

```javascript
{
      path: '/',
      name: 'HelloWorld',
      components: {
        default: HelloWorld,
        left: Hi1,
        right: Hi2,
      }
    },
beforeEnter:(to,from,next)=>{
    console.log("我进来了");
    console.log(to);
    console.log(from);
    next()
}
```

## 组件里面写好了钩子函数 beforeRouterEnter,beforeRouterLeave

```javascript
export default {
      name:"Hi2",
      data(){
         return {
           message2:"这个就是Hi2页面"
         }
      },
beforeRouterEnter:(to,from,next){
  console.log("我进来了")
}.
beforeRouterLeave:(to,form,next){
  console.log("我离开了")
}
    }
```
