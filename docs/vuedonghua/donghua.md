# Vue 动画

- Vue 里面的动画有 2 种方式

- 第一种利用动画提供的钩子函数

- 第二种利用@keyframes 关键帧

## Vue2 动画里面的钩子函数

- 需要利用 transiton 标签

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
            <title>
                css动画原理
            </title>
        </meta>
        <script src="./vue.js" type="text/javascript">
        </script>
        <style>
          .fade-enter,
          .fade-leave-to{
              opacity: 0;
          }
          .fade-enter-active,
          .fade-leave-active{
            transition: opacity 1s;
          }
        </style>
    </head>
    <body>
        <div id="app">
            <transition name='fade'>
                <div v-show="show">
                    content
                </div>
            </transition>
            <button @click="handleClick">
                切换
            </button>
        </div>
        <script>
            var app=new Vue({
            el:"#app",
            data:{
              show:true
            },
            methods:{
              handleClick:function(event){
                this.show=!this.show;
                // event.preventDefault();//阻止了，但是由于点击事件位置的变化，所以效果未成功。
              }
            },
            mounted:function(){
              document.onselectstart = function(){return false;};
            }
          })
        </script>
    </body>
</html>
```

- 使用 keyframes

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
            <title>
                css动画原理keyframes
            </title>
        </meta>
        <script src="./vue.js" type="text/javascript">
        </script>
        <style>
        @keyframes bounce-in{
          0%{
            transform: scale(0);
          }
          50%{
            transform: scale(1.5);
          }
          100%{
            transform: scale(1);
          }
        }
          .in{
            transform-origin: left center;
            animation: bounce-in 1s;
          }
          .out{
            transform-origin: left center;
            animation: bounce-in 1s reverse;
          }
        </style>
    </head>
    <body>
        <div id="app">
            <transition enter-active-class='in' leave-active-class='out'>
                <div v-show="show">
                    content
                </div>
            </transition>
            <button @click="handleClick">
                切换
            </button>
        </div>
        <script>
            var app=new Vue({
            el:"#app",
            data:{
              show:true
            },
            methods:{
              handleClick:function(event){
                this.show=!this.show;
                // event.preventDefault();//阻止了，但是由于点击事件位置的变化，所以效果未成功。
              }
            },
            mounted:function(){
              document.onselectstart = function(){return false;};
            }
          })
        </script>
    </body>
</html>
```
