# Vue 生命周期

## 什么是生命周期函数

生命周期函数俗称钩子函数,它指的是只有在特定的时候才执行的函数,这个时候以前或者以后都不执行

## Vue 里面有八大钩子函数

### beforeCreate

- 它只得是在组件创建前执行，这个时候它仅仅是个对象

### created 创建后

- 这个时候对象及其事件完全初始化了

### beforeMounted

- 加载组件之前。这个时候表示还没有加载组件

### mounted

- 加载组件之后,这个时候表示加载完毕了。一般在这个函数里面获取数据，写一些异步操作赋值等等

### beforeUpdate

- 更新组件 表示的是组件里面的数据有变化的时候,它在组件变化之前执行

### updated

- 更新组件之后,他表示的是组件里面的数据更新完毕才执行

### beforeDestroy

- 销毁前 表示组件在销毁前执行的函数

### destroyed

- 销毁后表示的是组件销毁后执行的函数

```html
<div id="container">
  <button @click="changeMsg()">change</button>
  <span>{{msg}}</span>
</div>

<script type="text/javascript">
  var vm = new Vue({
    el: "#container",
    data: {
      msg: "TigerChain",
    },
    beforeCreate() {
      console.group("%c%s", "color:red", "beforeCreate--实例创建前状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    created() {
      console.group("%c%s", "color:red", "created--实例创建完成状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    beforeMount() {
      console.group("%c%s", "color:red", "beforeMount--挂载之前的状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    mounted() {
      console.group("%c%s", "color:red", "mounted--已经挂载的状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    beforeUpdate() {
      console.group("%c%s", "color:red", "beforeUpdate--数据更新前的状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el.innerHTML);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
      console.log(
        "%c%s",
        "color:green",
        "真实的 DOM 结构:" + document.getElementById("container").innerHTML
      );
    },
    updated() {
      console.group("%c%s", "color:red", "updated--数据更新完成时状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el.innerHTML);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
      console.log(
        "%c%s",
        "color:green",
        "真实的 DOM 结构:" + document.getElementById("container").innerHTML
      );
    },
    activated() {
      console.group(
        "%c%s",
        "color:red",
        "activated-- keep-alive 组件激活时调用"
      );
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    deactivated() {
      console.group("%c%s", "color:red", "deactivated-- keep-alive 停用时调用");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    beforeDestroy() {
      console.group("%c%s", "color:red", "beforeDestroy-- vue实例销毁前的状态");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    destroyed() {
      console.group("%c%s", "color:red", "destroyed-- vue实例销毁完成时调用");
      console.log("%c%s", "color:blue", "el  :" + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:blue", "data  :" + this.$data);
      console.log("%c%s", "color:blue", "message  :" + this.msg);
    },
    methods: {
      changeMsg() {
        this.msg = "TigerChain111";
      },
    },
  });
</script>
```
