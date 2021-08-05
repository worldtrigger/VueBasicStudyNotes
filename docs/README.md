# 快速开始

Vue.js 是一套构建用户界面的渐进式框架，Vue 采用自下向上增量开发的设计，其核心库只关注视图层，易于上手，同时 vue 完全有能力驱动采用单文件组件和 Vue 生态系统支持的库开发的复杂单页应用。其实抛开官方的一些不知所云的说法，简单来说，在传统 web 开发中，我们搭建项目都以 html 结构为基础，然后通过 jquery 或者 js 来添加各种特效功能，需要去选中每一个元素进行命令，这些内容在简单的项目中或者不变的项目中还能应付得来，一旦项目改动或者项目工程较大，代码的修改将是复杂繁琐的，而这时候用了 vue，这些问题都不复存在。在比如一些单网页制作成的应用程序，一般涉及到数据交互的内容都很多，而应用了 vue 之后将大大缩减工作量。

# Vue 好处

## 数据绑定

vue 会根据对应的元素，进行设置元素数据，通过输入框，以及 get 获取数据等多种方式进行数据的实时绑定，进行网页及应用的数据渲染 。

## 组件式开发

通过 vue 的模块封装，它可以将一个 web 开发中设计的各种模块进行拆分，变成单独的组件，然后通过数据绑定，调用对应模版组件，同时传入参数，即可完成对整个项目的开发。

# 安装设置淘宝镜像

- 设置淘宝镜像

```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

# Vue2.0 安装

## 安装 vue-cli

```javascript
cnpm i vue-cli - g
```

## 初始化项目

```javascript
vue init webpack text2(项目名称随意填写不要有大写)
```

## 按照提示

```javascript
cd  text2
npm run dev
```

## 这样就完成了安装下面再说下配置

```bash
一般情况我们在build文件下找到webpack.base.conf.js 在里面修改别名比如proxy

config 文件夹下面就是项目配置文件，我们要的变量配置都在这里

src 重点我们平时写的文件都在这里

components 文件夹就是组件

assets 文件夹就是静态文件

router 文件就是路由文件里面都是js文件

main.js 就是入口文件。引入全部来自这里

```

## 设置别名

- 在 webpack.base.conf.js 文件中可以找到下面的一段代码

- @components 是我们自己定义的，可以随意替换

```javascript

resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      '@components': resolve('src/components')
    }
},

```

## 设置代理

- 找到 config 文件夹下面的 index.js 文件

```javascript
proxyTable: {
"/api": {    // api相当于一个别名，代指 http://192.168.0.14:8081
'target':'http://192.168.0.14:8081',
'changeOrigin':true,
'pathRewrite': {
'^/api':""
}
}
}
```

# Vuecli3.0 版本的安装

## 利用 cnpm 来安装

```javascript
npm i @vue/cli -g
or
yarn global add @vue/cli
```

## 创建项目

```javascript
vue create 项目名称(必须小写)
```

## 正式安装步骤

```javascript
Vue CLI v3.3.0
? Please pick a preset: (Use arrow keys)
> default (babel, eslint)
  Manually select features

它的意思是选择默认还是手动选择
```

## 下一步空格表示选择,回车表示进入下一步

```javascript
Vue CLI v3.3.0
? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
>(*) Babel
 ( ) TypeScript
 ( ) Progressive Web App (PWA) Support
 (*) Router
 (*) Vuex
 (*) CSS Pre-processors
 (*) Linter / Formatter
 ( ) Unit Testing
 ( ) E2E Testing
```

## 模块安装询问 因为安装了 router 所以会弹出 Y

```javascript
Vue CLI v3.3.0
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, Router, Vuex, CSS Pre-processors, Linter
? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n)
```

## 后面还有几步我就不列举了,发一个汇总版本的

```javascript
Vue CLI v3.3.0
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, Router, Vuex, CSS Pre-processors, Linter
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Less
? Pick a linter / formatter config: Prettier
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection)Lint on save
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? In package.json
? Save this as a preset for future projects? (y/N) N //是否记录下，以便下次继续使用这套配置
```

## 安装最后一步

```javascript
cd demo1  // 进入项目目录 这里demo1就是你一上来create 那个名称
npm run serve  // 这里和2不一样了。2是run dev 而 3 是run serve

DONE  Compiled successfully in 2232ms                                                                                                                                                                        App running at:
  - Local:   http://localhost:8080/
  - Network: http://192.168.0.8:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

## 根目录新建 vue.config.js 里面的配置

```javascript
// vue.config.js 配置说明
//官方vue.config.js 参考文档 https://cli.vuejs.org/zh/config/#css-loaderoptions
// 这里只列一部分，具体配置参考文档
module.exports = {
  //别名设置
  configureWebpack: {
    resolve: {
      alias: {
        assets: "@/assets",
        components: "@/components",
        views: "@/views",
      },
    },
  },
  // 部署生产环境和开发环境下的URL。
  // 默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上
  //例如 https://www.my-app.com/。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 https://www.my-app.com/my-app/，则设置 baseUrl 为 /my-app/。
  baseUrl: process.env.NODE_ENV === "production" ? "./" : "/",

  // outputDir: 在npm run build 或 yarn build 时 ，生成文件的目录名称（要和baseUrl的生产环境路径一致）
  outputDir: "dist",
  //用于放置生成的静态资源 (js、css、img、fonts) 的；（项目打包之后，静态资源会放在这个文件夹下）
  assetsDir: "assets",
  //指定生成的 index.html 的输出路径  (打包之后，改变系统默认的index.html的文件名)
  // indexPath: "myIndex.html",
  //默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。你可以通过将这个选项设为 false 来关闭文件名哈希。(false的时候就是让原来的文件名不改变)
  filenameHashing: false,

  //   lintOnSave：{ type:Boolean default:true } 问你是否使用eslint
  lintOnSave: true,
  //如果你想要在生产构建时禁用 eslint-loader，你可以用如下配置
  // lintOnSave: process.env.NODE_ENV !== 'production',

  //是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。(默认false)
  // runtimeCompiler: false,

  /**
   * 如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。
   *  打包之后发现map文件过大，项目文件体积很大，设置为false就可以不输出map文件
   *  map文件的作用在于：项目打包后，代码都是经过压缩加密的，如果运行时报错，输出的错误信息无法准确得知是哪里的代码报错。
   *  有了map就可以像未加密的代码一样，准确的输出是哪一行哪一列有错。
   * */
  productionSourceMap: false,

  // 它支持webPack-dev-server的所有选项
  devServer: {
    /* 这里有个前提必须引入文件
     const appData = require("./data.json");
     const seller = appData.seller;
     const goods = appData.goods;
     const ratings = appData.ratings;
    */
    before(app) {
      app.get("/api/seller", function (req, res) {
        res.json({
          errno: 0,
          data: seller,
        });
      });
      app.get("/api/goods", function (req, res) {
        res.json({
          errno: 0,
          data: goods,
        });
      });
      app.get("/api/ratings", function (req, res) {
        res.json({
          errno: 0,
          data: ratings,
        });
      });
    },
    host: "localhost", //也可以直接写IP地址这样方便真机测试
    port: 8080, // 端口号
    https: false, // https:{type:Boolean}
    open: true, //配置自动启动浏览器
    // proxy: 'http://localhost:4000' // 配置跨域处理,只有一个代理

    // 配置多个代理
    proxy: {
      "/api": {
        target: "<url>", //写地址
        ws: true, // 允许跨域
        changeOrigin: true, //允许跨域
        pathRewrite: {
          "^/api": "",
        },
      },
      "/foo": {
        target: "<other_url>",
      },
    },
  },
};
```

## 修改配置 在 package.json 里面

- 增加了 rules 选项

```javascript
"eslintConfig": {
    "root": true,
    "env": {
      "node": true
    },
    "extends": [
      "plugin:vue/essential",
      "@vue/prettier"
    ],
    "rules": {
      "no-console": "off"
    },
    "parserOptions": {
      "parser": "babel-eslint"
    }
  },
```
