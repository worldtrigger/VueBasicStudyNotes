# Vue3 之路由传参

## 在 vue3.0 里面使用路由必须要引入 useRouter 和 useRoute

```javascript
import { useRoute, useRouter } from "vue-router";
```

## 传递参数和获取参数

- Router 负责跳转,Route 负责接收数据

```javascript
function useHooks() {
  const Router = useRouter(); //跳转
  const Route = useRoute(); //获取到值
  const Routeid = computed(() => {
    return Route.query.id; //接收数据
  });
  const gotourl = () => {
    console.log("执行了");
    //路由跳转
    Router.push({
      path: "/about",
      query: {
        id: "6666",
      },
    });
  };
  return {
    gotourl,
    Routeid,
  };
}
```

## 其他就和 Vue2 一样
