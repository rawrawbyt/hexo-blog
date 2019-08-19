---
title: vue集合
date: 2018-05-20 14:38:18
tags: [vue]
categories: Note
---

<div align=center>
![“封面”](/images/bg/0163.jpeg)
</div>

<!--more-->
# 原理
### 数据双向绑定
Vue3之前通过get和set完成，而Vue3后通过proxy来完成。
### 虚拟dom
一个内部的json字符串。

# bugs

### for中的key

<font color='red'>[Vue warn]: Error in render: "TypeError: _self.$scopedSlots.default is not a function”</font>

> 究其原因，是因为表格是element-ui通过循环产生的，而vue在dom重新渲染时有一个性能优化机制，就是相同dom会被复用，这就是问题所在，所以，通过key去标识一下当前行是唯一的，不许复用，就行了。

方案：添加 <font color='red'>:key="Math.random()"</font>

# 优化
## 代码
#### v-if / v-show
`v-if`:惰性;切换过程中条件块内的事件监听器和子组件适当地被销毁和重建;
`v-show`:不管初始条件是什么，元素总是会被渲染;
v-if 适用于在运行时不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。
#### computed / watch
`computed`： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed  的值；
`watch`： 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；
computed适用于需要进行数值计算，并且依赖于其它数据时；因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
watch适用于需要在数据变化时执行异步或开销较大的操作时；使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。
#### v-for 遍历必须为 item 添加 key，且避免同时使用 v-if
1. v-for 遍历必须为 item 添加 key
在列表数据进行遍历渲染时，需要为每一项 item 设置唯一 key 值，方便 Vue.js 内部机制精准找到该条列表数据。当 state 更新时，新的状态值和旧的状态值对比，较快地定位到 diff 。
2. v-for 遍历避免同时使用 v-if
v-for 比 v-if 优先级高，如果每一次都需要遍历整个数组，将会影响速度，尤其是当之需要渲染很小一部分的时候，必要情况下应该替换成 computed 属性。
百度小程序里面for和if同时使用是直接语法报错的；
```js

<div
v-for="(key,obj) in lists"
:key="key">
{{ obj.name }}
</div>

computed: {
  lists: function () {
    return this.lists.filter(function (list) {
        return list.isActive
    })
  }
}
```
#### 懒加载

##### 图片资源懒加载

1. 插件：`yarn add vue-lazyload --save-dev`
2. 
```js [main.js]
import VueLazyload from 'vue-lazyload'
```
3. 
```js
Vue.use(VueLazyload)
or
Vue.use(VueLazyload, {
    preLoad: 1.3,
    error: 'dist/error.png',
    loading: 'dist/loading.gif',
    attempt: 1
})
```
4. vue文件
```html
<img v-lazy="/static/img/1.png">
```

##### 路由懒加载
1. 首屏加载问题；
`const goodslist = () => import( /* webpackChunkName: "trade" */ './views/Goodslist.vue');`
2. 服务端渲染 SSR/预渲染
SSR:重点优化的场景；
预渲染:少量页面优化；在构建时 (build time) 简单地生成针对特定路由的静态 HTML 文件。优点是设置预渲染更简单，并可以将你的前端作为一个完全静态的站点，具体你可以使用 prerender-spa-plugin 就可以轻松地添加预渲染 。

#### 第三方插件的按需引入
1. `yarn add babel-plugin-component -D`
2. 
```js [.babelrc]
{
  "presets": [["es2015", { "modules": false }]],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```
3. 
```js [main.js]
import Vue from 'vue';
import { Button,} from 'element-ui';

Vue.use(Button)
```



#### 长列表性能优化
1. Vue 会通过 `Object.defineProperty`对数据进行劫持，来实现视图响应数据的变化;纯粹的数据展示，不会做任何修改的数据可以通过 Object.freeze 方法来冻结一个对象；
`this.lists = Object.freeze(lists);`
2. 无限列表性能;` vue-virtual-scroll-list 和 vue-virtual-scroller `


#### 事件的销毁
Vue 组件销毁时，会自动清理它与其它实例的连接，解绑它的全部指令及事件监听器，但是仅限于组件本身的事件。如果在 js 内使用 addEventListene 等方式是不会自动销毁的，我们需要在组件销毁时手动移除这些事件的监听，以免造成内存泄露;
```js
created() {
  addEventListener('click', this.click, false)
},
beforeDestroy() {
  removeEventListener('click', this.click, false)
}
```
## webpack
#### 图片压缩
1. `yarn add image-webpack-loader --save-dev`
2. 
```js [webpack.base.conf.js]
{
  test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
  use:[
    {
    loader: 'url-loader',
    options: {
      limit: 10000,
      name: utils.assetsPath('img/[name].[hash:7].[ext]')
      }
    },
    {
      loader: 'image-webpack-loader',
      options: {
        bypassOnDebug: true,
      }
    }
  ]
}
```
#### 减少 ES6 转为 ES5 的冗余代码
```
ES6 转为 ES5,需要以下两个辅助函数：
babel-runtime/helpers/createClass  // 用于实现 class 语法
babel-runtime/helpers/inherits  // 用于实现 extends 语法   
```
在默认情况下， Babel 会在每个输出文件中内嵌这些依赖的辅助函数代码，如果多个源代码文件都依赖这些辅助函数，那么这些辅助函数的代码将会出现很多次，造成代码冗余。
1. `yarn add babel-plugin-transform-runtime --save-dev`
2. 
```js [.babelrc]
"plugins": [
    "transform-runtime"
]
```
#### 提取公共代码
如果项目中没有去将每个页面的第三方库和公共模块提取出来，则项目会存在以下问题：
* 相同的资源被重复加载，浪费用户的流量和服务器的成本。
* 每个页面需要加载的资源太大，导致网页首屏加载缓慢，影响用户体验。
所以我们需要将多个页面的公共代码抽离成单独的文件，来优化以上问题 。Webpack 内置了专门用于提取多个Chunk 中的公共部分的插件 CommonsChunkPlugin，我们在项目中 CommonsChunkPlugin 的配置如下：
```js
// 所有在 package.json 里面依赖的包，都会被打包进 vendor.js 这个文件中。
new webpack.optimize.CommonsChunkPlugin({
  name: 'vendor',
  minChunks: function(module, count) {
    return (
      module.resource &&
      /\.js$/.test(module.resource) &&
      module.resource.indexOf(
        path.join(__dirname, '../node_modules')
      ) === 0
    );
  }
}),
// 抽取出代码模块的映射关系
new webpack.optimize.CommonsChunkPlugin({
  name: 'manifest',
  chunks: ['vendor']
})
```
#### 模版预编译
当使用 DOM 内模板或 JavaScript 内的字符串模板时，模板会在运行时被编译为渲染函数。通常情况下这个过程已经足够快了，但对性能敏感的应用还是最好避免这种用法。
预编译模板最简单的方式就是使用单文件组件——相关的构建设置会自动把预编译处理好，所以构建好的代码已经包含了编译出来的渲染函数而不是原始的模板字符串。
如果你使用 webpack，并且喜欢分离 JavaScript 和模板文件，你可以使用 vue-template-loader，它也可以在构建过程中把模板文件转换成为 JavaScript 渲染函数。

#### 提取组件的 CSS
当使用单文件组件时，组件内的 CSS 会以 style 标签的方式通过 JavaScript 动态注入。这有一些小小的运行时开销，如果你使用服务端渲染，这会导致一段 “无样式内容闪烁 (fouc) ” 。将所有组件的 CSS 提取到同一个文件可以避免这个问题，也会让 CSS 更好地进行压缩和缓存。
查阅这个构建工具各自的文档来了解更多：
* webpack + vue-loader ( vue-cli 的 webpack 模板已经预先配置好)
* Browserify + vueify
* Rollup + rollup-plugin-vue

#### 优化 SourceMap
我们在项目进行打包后，会将开发中的多个文件代码打包到一个文件中，并且经过压缩、去掉多余的空格、babel编译化后，最终将编译得到的代码会用于线上环境，那么这样处理后的代码和源代码会有很大的差别，当有 bug的时候，我们只能定位到压缩处理后的代码位置，无法定位到开发环境中的代码，对于开发来说不好调式定位问题，因此 sourceMap 出现了，它就是为了解决不好调式代码问题的。
SourceMap 的可选值如下（+ 号越多，代表速度越快，- 号越多，代表速度越慢, o 代表中等速度 ）
开发环境推荐：`cheap-module-eval-source-map`
生产环境推荐：`cheap-module-source-map`
原因如下：
* cheap：源代码中的列信息是没有任何作用，因此我们打包后的文件不希望包含列相关信息，只有行信息能建立打包前后的依赖关系。因此不管是开发环境或生产环境，我们都希望添加 cheap 的基本类型来忽略打包前后的列信息；
* module ：不管是开发环境还是正式环境，我们都希望能定位到bug的源代码具体的位置，比如说某个 Vue 文件报错了，我们希望能定位到具体的 Vue 文件，因此我们也需要 module 配置；
* soure-map ：source-map 会为每一个打包后的模块生成独立的 soucemap 文件 ，因此我们需要增加source-map 属性；
* eval-source-map：eval 打包代码的速度非常快，因为它不生成 map 文件，但是可以对 eval 组合使用 eval-source-map 使用会将 map 文件以 DataURL 的形式存在打包后的 js 文件中。在正式环境中不要使用 eval-source-map, 因为它会增加文件的大小，但是在开发环境中，可以试用下，因为他们打包的速度很快。

#### 构建结果输出分析
vue-cli2:
`webpack-bundle-analyzer`
```js [webpack.prod.conf.js]
if (config.build.bundleAnalyzerReport) {
  var BundleAnalyzerPlugin =   require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
  webpackConfig.plugins.push(new BundleAnalyzerPlugin());
}
```
`yarn run build --report`
vue-cli3:
```js [vue.config.js]
module.exports={
    chainWebpack:config=>{
        // config.moudle
        //     .rule('vue')
        //     .user('vue-loader')
        //     .loader('vue-loader')
        //     .tap(options=>{
        //         //update
        //         return options
        //     })
        // Examples
        //config
        // .plugin('hot')
        // .use(webpack.HotModuleReplacementPlugin);
        // config
        // .plugin('env')
        // .use(webpack.EnvironmentPlugin, ['NODE_ENV']);
        config
        .plugin('webpack-bundle-analyzer')
        .use(require('webpack-bundle-analyzer').BundleAnalyzerPlugin)
    }
}
```
if (process.env.npm_config_report) {
  // ...    
}
```js [package.json]
"analyz": "npm_config_report=true npm run build"
```

## 基础web
#### 开启 gzip 压缩
gzip 是 GNUzip 的缩写，最早用于 UNIX 系统的文件压缩。HTTP 协议上的 gzip 编码是一种用来改进 web 应用程序性能的技术，web 服务器和客户端（浏览器）必须共同支持 gzip。目前主流的浏览器，Chrome，firefox，IE等都支持该协议。常见的服务器如 Apache，Nginx，IIS 同样支持，gzip 压缩效率非常高，通常可以达到 70% 的压缩率，也就是说，如果你的网页有 30K，压缩之后就变成了 9K 左右
1. `yarn add compression --save`
2. 
```js
var compression = require('compression');
var app = express();
app.use(compression())
```
3. 重启服务，观察网络面板里面的 response header，如果看到content-encoding的字段则表明 gzip 开启成功;
#### 浏览器缓存;静态资源进行缓存
#### CDN 的使用
#### Chrome Performance 查找性能瓶颈

