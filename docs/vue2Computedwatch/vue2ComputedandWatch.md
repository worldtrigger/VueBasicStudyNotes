# Vue2 中的 Computed 与 Watch

## Computed

- computed 是一个计算属性,类似过滤器，对绑定的 view 的数据进行处理

- computed 里面必须有 return

```javascript
data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
```

> fullname 不能在 data 里面定义 因为 computed 作为计算属性定义的 fullName 并返回对应的结果这个变量,变量不可以重复定义和赋值

```javascript
data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
  fullName：{
   get(){//回调函数 当需要读取当前属性值是执行，根据相关数据计算并返回当前属性的值
      return this.firstName + ' ' + this.lastName
    },
   set(val){//监视当前属性值的变化，当属性值发生变化时执行，更新相关的属性数据
       //val就是fullName的最新属性值
       console.log(val)
        const names = val.split(' ');
        console.log(names)
        this.firstName = names[0];
        this.lastName = names[1];
   }
   }
  }
```

# Watch

- Watch 就是一个观察动作,实时更新。

```javascript
<div>
      <p>FullName: {{fullName}}</p>
      <p>FirstName: <input type="text" v-model="firstName"></p>
</div>

new Vue({
  el: '#root',
  data: {
    firstName: 'Dawei',
    lastName: 'Lou',
    fullName: ''
  },
  watch: {　　 //普通的watch监听
    firstName(newName, oldName) {
      this.fullName = newName + ' ' + this.lastName;
    }
  }
})
```

- 监听复杂类型

```javascript
watch: {
  firstName: {
    handler(newName, oldName) {
      this.fullName = newName + ' ' + this.lastName;
    },
    // 代表在wacth里声明了firstName这个方法之后立即先去执行handler方法
    immediate: true,
    deep:true
  }
}
```

> 我们给 firstName 绑定了一个 handler 方法,之前我们写的 watch 方法默认写的就是 handler 而 immediate:true 代表 如果在 watch 里声明了 firstName 之后，就会立即先去执行里面的 handler 方法,如果为 false 就跟我们以前的效果一样,不会在绑定的时候就执行
