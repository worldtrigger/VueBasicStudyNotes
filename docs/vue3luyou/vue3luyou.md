# Vue3 之路由传参

## 在 vue3.0 里面使用路由必须要引入 useRouter 和 useRoute

```javascript
import { useRoute, useRouter } from 'vue-router';
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
    console.log('执行了');
    //路由跳转
    Router.push({
      path: '/about',
      query: {
        id: '6666',
      },
    });
  };
  return {
    gotourl,
    Routeid,
  };
}
```

## Vue3 里面的路由拦截

```javascript
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router';
const HomePage = () => import('../pages/Home.vue');
const ErrorPage = () => import('../pages/ERROR.vue');
const AdminPage = () => import('../pages/Admin.vue');
const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    name: 'Home',
    component: HomePage,
  },
  {
    path: '/admin',
    name: 'Admin',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: AdminPage,
  },
  {
    path: '/error',
    name: 'error',
    component: ErrorPage,
  },
];

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes,
});

router.beforeEach((to, from, next) => {
  if (to.matched.length == 0) {
    from.name
      ? next({
          name: from.name,
        })
      : next('/error');
  } else {
    //匹配上了
    next();
  }
});

export default router;
```

## 路由拦截

- 这里特别注意的就是 store 的使用

```javascript
// request.js
import axios from 'axios';
// import router from "@/router";
import Store from '../store';

const instance = axios.create({
  //这里千万不能写headers否则会造成数据缓存
  timeout: 300000,
});
/** **** request拦截器==>对请求参数做处理 ******/
instance.interceptors.request.use(
  (config) => {
    // 加载
    Store.commit('changeLoadingFlag', true);
    let value = window.localStorage.getItem('token');
    console.log('token值');
    console.log(value);
    if (value) {
      let result = JSON.parse(value);
      let configall: any = config;
      configall.headers.authorization =
        result.token_type + ' ' + result.access_token;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
/** **** respone拦截器==>对响应做处理 ******/
instance.interceptors.response.use(
  (response) => {
    Store.commit('changeLoadingFlag', false);
    return response;
  },
  (error) => {
    // 错误提醒
    Store.commit('changeLoadingFlag', false);
    return Promise.reject(error);
  }
);
export default instance;
```

## 其他就和 Vue2 一样
