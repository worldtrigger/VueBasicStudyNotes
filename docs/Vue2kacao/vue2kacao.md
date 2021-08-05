# 卡槽

- 卡槽的作用就是有的时候我们不想只传递数据,还必须传递 html 代码

## 匿名卡槽(只有一个卡槽,直接找默认)

- 父组件 我想把 div 里面的 html 代码传递给子组件

```html
<template>
  <div>
    <header></header>
    {{ message }}
    <Chacaoa>
      <div class="sloata">
        <p>A里面的数据</p>
      </div>
    </Chacaoa>
  </div>
</template>

<script>
  import Header from "@/components/common/Header";
  import Chacaoa from "@/components/common/Sloata";
  export default {
    data() {
      return {
        message: "首页",
      };
    },
    components: {
      Header,
      Chacaoa,
    },
  };
</script>

<style lang="less" scoped>
  .sloata {
    width: 300px;
    height: 100px;
    background: blue;
    color: yellow;
  }
</style>
```

- 子组件

```html
<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: "子组件",
        dataA: "dataA里面的数据",
        dataB: "dataB里面的数据",
      };
    },
  };
</script>

<style lang="less" scoped></style>
```

## 具名卡槽

- 卡槽不止一个,需要传递多个 html 代码(署名)

- 父组件

```html
<template>
  <div>
    <header></header>
    {{ message }}
    <Chacaoa>
      <div class="sloata" slot="kaocaoa">
        <p>A里面的内容</p>
      </div>
      <div class="sloatb" slot="kaocaob">
        <p>B里面的内容</p>
      </div>
    </Chacaoa>
  </div>
</template>

<script>
  import Header from "@/components/common/Header";
  import Chacaoa from "@/components/common/Sloata";
  export default {
    data() {
      return {
        message: "首页",
      };
    },
    components: {
      Header,
      Chacaoa,
    },
  };
</script>

<style lang="less" scoped>
  .sloata {
    width: 300px;
    height: 100px;
    background: blue;
    color: yellow;
  }
  .sloatb {
    width: 300px;
    height: 100px;
    background: red;
    color: black;
  }
</style>
```

- 子组件

```javascript
<template>
  <div>
    <slot name="kaocaoa"></slot>
    <slot name="kaocaob"></slot>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: '子组件',
        dataA: 'dataA里面的数据',
        dataB: 'dataB里面的数据'
      }
    }
  }
</script>

<style lang="less" scoped></style>
```

## 卡槽里面子组件想给父组件传值

- 只有利用 slot-scope

- 父组件

```html
<template>
  <div>
    <header></header>
    {{ message }}
    <Chacaoa>
      <div class="sloata" slot="kaocaoa" slot-scope="shuju1">
        <p>{{ shuju1.data }}</p>
      </div>
      <div class="sloatb" slot="kaocaob" slot-scope="shuju2">
        <p>{{ shuju2.data }}</p>
      </div>
    </Chacaoa>
  </div>
</template>

<script>
  import Header from "@/components/common/Header";
  import Chacaoa from "@/components/common/Sloata";
  export default {
    data() {
      return {
        message: "首页",
      };
    },
    components: {
      Header,
      Chacaoa,
    },
  };
</script>

<style lang="less" scoped>
  .sloata {
    width: 300px;
    height: 100px;
    background: blue;
    color: yellow;
  }
  .sloatb {
    width: 300px;
    height: 100px;
    background: red;
    color: black;
  }
</style>
```

- 子组件

```html
<template>
  <div>
    <header></header>
    {{ message }}
    <Chacaoa>
      <div class="sloata" slot="kaocaoa" slot-scope="shuju1">
        <p>{{ shuju1.data }}</p>
      </div>
      <div class="sloatb" slot="kaocaob" slot-scope="shuju2">
        <p>{{ shuju2.data }}</p>
      </div>
    </Chacaoa>
  </div>
</template>

<script>
  import Header from "@/components/common/Header";
  import Chacaoa from "@/components/common/Sloata";
  export default {
    data() {
      return {
        message: "首页",
      };
    },
    components: {
      Header,
      Chacaoa,
    },
  };
</script>

<style lang="less" scoped>
  .sloata {
    width: 300px;
    height: 100px;
    background: blue;
    color: yellow;
  }
  .sloatb {
    width: 300px;
    height: 100px;
    background: red;
    color: black;
  }
</style>
```
