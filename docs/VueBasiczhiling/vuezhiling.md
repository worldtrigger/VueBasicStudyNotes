# Vue 基本指令

## (1) v-text

- 它的作用就是里面有 HTML 代码的话 也不转义直接显示

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-text="msg"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          msg: "<strong>Hello</strong> Vue!",
        },
      });
    </script>
  </body>
</html>
```

## (2) v-html

- 它的作用就是绑定 html 属性把里面的 html 代码渲染出来

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-html="msg"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          msg: "<strong>Hello</strong> Vue!",
        },
      });
    </script>
  </body>
</html>
```

## (3) v-if 判断

- 真 就渲染 假就不渲染 假的话根本没有这个 DOM

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-if="flag">不渲染</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: false,
        },
      });
    </script>
  </body>
</html>
```

这样的结果就是不渲染,移除 DOM 了

- 有 if 就会有 v-else

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-if="flag">不渲染</p>
      <p v-else>最后的结果</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: false,
        },
      });
    </script>
  </body>
</html>
```

- v-else-if

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-if="show==='a'">渲染A</p>
      <p v-else-if="show==='b'">渲染B</p>
      <p v-else>渲染C</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          show: "a",
        },
      });
    </script>
  </body>
</html>
```

> 依据 show 值不同渲染不同的数据

## (4) v-show

- 它不用于 v-if,它的作用是渲染了,但是依据变量的真假来隐藏,等价于 display:none

- 而 v-if 则是 DOM 不会加载

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-show="flag">渲染了,有DOM但是隐藏了</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: false,
        },
      });
    </script>
  </body>
</html>
```

## (5) v-for

- 列表循环,里面必须有 key

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-for="(content,index) in listdata" :key="index">
        这是第{{index}}数据,数据内容是{{content}}
      </p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          listdata: ["第一条数据", "第二条数据", "第三条数据"],
        },
      });
    </script>
  </body>
</html>
```

## (6) v-once

- 只会渲染一次,即使数据改变了,他也不会改变

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p v-once="msg"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          msg: "只渲染一次，即使改变了也不会再次渲染",
        },
      });
    </script>
  </body>
</html>
```

## (7) v-bind

- v-bind 绑定数据在 Vue 中可以简写成:可以绑定数据,也可以当作给子组件传递数据

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p :class="[flag?'active':'']"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: true,
        },
      });
    </script>
  </body>
</html>
```

- flag 要是真 就加载 active 的类名,flag 要是假 就加载空

- 动态 class 几种方式

- 最简单的 flag 为真就加载,active 为假就不加载

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p :class="{'active':flag}"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: true,
        },
      });
    </script>
  </body>
</html>
```

- 依据条件来加载 flag 要是-1 就加载 要不是就不加载

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p :class="{'active':flag==-1}"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          flag: -1,
        },
      });
    </script>
  </body>
</html>
```

- 绑定并判断多个,属性名就是类名,值就是判断条件

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p :class="{'active':flag,'sort':flagsort}"></p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: '#app', //element
        data: {
          flag: -1
          flagsort:true
        }
      })
    </script>
  </body>
</html>
```

## (8) v-on

- 监听事件可以简写成@

- v-on:click 可以简写成@click

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <p @click="change">点击我弹出来</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        methods: {
          change() {
            window.alert("弹出来");
          },
        },
      });
    </script>
  </body>
</html>
```

## (9) v-model

- 数据的双向绑定 一般结合 input textarea 使用的修饰符可以是.lazy,.number,.trim

```html
<html>
  <head>
    <title></title>
    <script src="https://unpkg.com/vue"></script>
  </head>
  <body>
    <div id="app">
      <input v-model="inputdata" type="text" />
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app", //element
        data: {
          inputdata: "获取到数据",
        },
      });
    </script>
  </body>
</html>
```
