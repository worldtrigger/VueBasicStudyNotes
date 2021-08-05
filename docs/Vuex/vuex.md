# Vuex

- 可以理解为公共仓库,但是它只要一刷新数据就清空.父组组件之间传值。父子兄弟都可以

# Vuex 分成几个部分

- state(存放公共数据)

- getters(对 state 数据的二次封装, 防止污染 state)

- mutations(里面都是方法,它的作用就是修改 state 里面的数据)

- actions(可以理解为 mutations 里面的一个合集,它能执行很多个 mutations)

```javascript
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);
const state = {
  //要设置的全局访问的state对象
  showFooter: true,
  changableNum: 0,
  //要设置的初始属性值
};
const getters = {
  //实时监听state值的变化(最新状态)
  isShow(state) {
    //承载变化的showFooter的值
    return state.showFooter;
  },
  getChangedNum() {
    //承载变化的changebleNum的值
    return state.changableNum;
  },
};
const mutations = {
  show(state) {
    //自定义改变state初始值的方法，这里面的参数除了state之外还可以再传额外的参数(变量或对象);
    state.showFooter = true;
  },
  hide(state) {
    //同上
    state.showFooter = false;
  },
  newNum(state, sum) {
    //同上，这里面的参数除了state之外还传了需要增加的值sum
    state.changableNum += sum;
  },
};
const actions = {
  hideFooter(context) {
    //自定义触发mutations里函数的方法，context与store 实例具有相同方法和属性
    context.commit("hide");
  },
  showFooter(context) {
    //同上注释
    context.commit("show");
  },
  getNewNum(context, num) {
    //同上注释，num为要变化的形参
    context.commit("newNum", num);
  },
};
const store = new Vuex.Store({
  state,
  getters,
  mutations,
  actions,
});
export default store;
```

- 使用的时候 actions 第一个参数和 mutations 的第一个参数都可以不传

- mapState,mapMutations 是 Vue 提供的语法糖可以直接使用

```html
<script>
  import { mapState, mapMutations } from "vuex";
  export default {
    computed: {
      ...mapState({
        singerId: "singer", //改名
      }),
    },
    data() {
      return {
        message: "汇总",
        showflag2: false,
      };
    },
    methods: {
      ...mapMutations({
        setsinger: "setsinger", //改名
      }),
      // 点击方法
      gotourl(id) {
        this.setsinger(id);
      },
    },
  };
</script>
```

# 下面是使用 modules 模块开发的

- 当功能非常多，我们需要对这些功能划分出模块来区分

## 1.新建一个 module 模块

- 在 Store 文件夹下面新建一个 model 模块起名 app.js,然后里面

- `特别注意的就是namespaced必须写`要不然出不来

```javascript
const moduleA = {
  namespaced: true, //采用了命名空间，必须要有
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

## 2.Vuex 里面引入这个模块

- 我这里还引入了其他的模块

```javascript
import Vue from "vue";
import Vuex from "vuex";
import ModuleA from "./models/app";
import ModuleB from "./models/app2";
Vue.use(Vuex);

export default new Vuex.Store({
  state: {},
  mutations: {},
  actions: {},
  modules: {
    moduleA: ModuleA,
    moduleB: ModuleB,
  },
});
```

## 3.组件里面使用的时候

- 需要使用语法糖 mapState,mapMutations

- State `...mapState("moduleA", {messageNew:"message"})`

- 方法 `...mapMutations("moduleA", ["changemessage"]),`

```html
<template>
  <div>
    <div class="home">{{ messageNew }} --哈哈</div>
    <div>{{ messageB }}</div>
    <button @click="changestate">改变state信息</button>
    <button @click="changestateB">改变stateB的信息</button>
  </div>
</template>

<script>
  import { mapState, mapMutations } from "vuex";

  export default {
    name: "Home",
    computed: {
      ...mapState("moduleA", {
        messageNew: "message",
      }),
      ...mapState("moduleB", {
        messageB: "message",
      }),
    },
    methods: {
      changestate() {
        this.changemessage("改变了");
      },
      changestateB() {
        this.changemessageB("B里面的数据改变了");
      },
      ...mapMutations("moduleA", ["changemessage"]),
      ...mapMutations("moduleB", ["changemessageB"]),
    },
  };
</script>
```
