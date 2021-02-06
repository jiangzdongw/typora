

# 珠峰公开课

## 1 MVVM 原理的理解

![image-20201230003826314](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230003826314.png)



![image-20201230004034910](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230004034910.png)

## 2 请说一下响应式数据的原理

![image-20201230004118655](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184942.png)

![image-20201230004345341](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185003.png)



## 3 VUE 中如何检测数据的变化

![image-20201230005102053](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005102053.png)

![image-20201230005217053](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005217053.png)



![image-20201230005250135](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005250135.png)

![image-20201230005526151](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005552593.png)

![image-20201230005552593](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005552593.png)

## 4 VUE 为何使用异步渲染

![image-20201230005721899](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005721899.png)

![image-20201230005744160](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230005744160.png)





## 5 nextTick 的实现原理

![image-20201230011141860](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185046.png)![image-20201230011208085](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230011208085.png)

## 6 VUE 中Computed 的特点

![image-20201230011323773](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230011323773.png)



computed method 区别

computed watch 区别

![image-20201230013050266](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/image-20201230013050266.png)

## 7 WATCH 中的 deep: true 如何实现的

![image-20201230013429639](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206182959.png)

> **选项：deep**
>
> 为了发现对象内部值的变化，可以在选项参数中指定 `deep: true`。注意监听数组的变更不需要这么做。



## 8 VUE 组件的生命周期

![image-20201230015716211](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206182959.png)



![image-20201230020005085](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206182959.png)

## 9  AJAX 放在 VUE 的哪个生命周期中？

![image-20201230020233036](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183222.png)

## 10 何时需要使用 beforeDestroy

![image-20201230020746068](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183248.png)

## 11 VUE 中的模板编译原理

![image-20201230021140589](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185123.png)

![image-20201230021118941](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185131.png)





## 12 V-IF 与 V-SHOW 的区别

![image-20201230022256410](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183312.png)



## 13 V-FOR 和 V-IF 为什么不能连用

![image-20201230022816885](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183407.png)

## 14 VNODE 描述一个 DOM 结构

![image-20201230022949885](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183412.png)

## 15 DIFF 算法的时间复杂度

![image-20201230023855609](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183426.png)

## 16 简述 VUE DIFF 算法的原理

![image-20201230023952002](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183436.png)

![image-20201230025414022](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183512.png)

![image-20201230025449251](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183520.png)



# 珠峰课 VUE

## 1 v-for 中为什么要使用 key

![image-20201229173640846](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183530.png)

鉴于性能考虑，diff算法只会做同级比较;

key主要用来做DOM DIFF，只有 tag 与 key 相同时，vue会认为该dom节点未发生变化，直接就地复用该节点，最多移动位置或都修改节点中的内容（如果节点中的内容对比后不一样，见图二）。 

使用索引也同样存在问题，数组发生改变的时候，索引也同步进行了更改。导致 VUE 认为 key 没有发生变化可能会继续复用。

## 2 描述组件的演染和更新过程

![image-20201229175436478](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183536.png)



​	在线作流程图：www.processon.com

![image-20201229175813206](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206183626.png)

![image-20201229180511546](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185750.png)

## 3 组件的 data 为什么是一个函数

![image-20201229235444819](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184247.png)

## 4 VUE 中的事件绑定原理

![image-20201230000638505](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184302.png)

## 5 V-MODEL 的实现原理及如何自定义 V-MODEL

![image-20201230002138465](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184306.png)

![image-20201230002605400](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184310.png)



![image-20201230002202635](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185305.png)





## 6 VUE-HTML 会导致哪些问题？

![image-20201229161333785](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184341.png)

![image-20201229161417348](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184347.png)

## 7 VUE 父子组件生命周期调用顺序

![image-20201229161556948](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184356.png)

![image-20201229162311793](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184404.png)

![image-20201229162356718](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185530.png)

## 8 VUE 组件如何通信 单向数据流

![image-20201229162740666](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185327.png)

1. EventBus Vue.prototype.$Bus = new Vue()
2. $listeners & attrs

## 9 VUE 中相同逻辑如何抽离

![image-20201229163134160](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185732.png)

![image-20201229163239921](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185336.png)

![image-20201229163430900](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185345.png)

## 10 为什么要使用异步组件

![image-20201229163510853](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206185356.png)

可以使异步组件分分开打包，并使用JSONP（webpack import 的实现就是通过 jsonp） 的形式异步加载;

异步组件一定是一个函数 新版本提供了对象的写法

### 动态组件 & 异步组件

> 该页面假设你已经阅读过了[组件基础](https://cn.vuejs.org/v2/guide/components.html)。如果你还对组件不太了解，推荐你先阅读它。

#### [异步组件](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#异步组件)

[Watch a free video lesson on Vue School](https://vueschool.io/lessons/dynamically-load-components?friend=vuejs)

在大型应用中，我们可能需要将应用分割成小一些的代码块，并且只在需要的时候才从服务器加载一个模块。为了简化，Vue 允许你以一个工厂函数的方式定义你的组件，这个工厂函数会异步解析你的组件定义。Vue 只有在这个组件需要被渲染的时候才会触发该工厂函数，且会把结果缓存起来供未来重渲染。例如：

```
Vue.component('async-example', function (resolve, reject) {
  setTimeout(function () {
    // 向 `resolve` 回调传递组件定义
    resolve({
      template: '<div>I am async!</div>'
    })
  }, 1000)
})
```

如你所见，这个工厂函数会收到一个 `resolve` 回调，这个回调函数会在你从服务器得到组件定义的时候被调用。你也可以调用 `reject(reason)` 来表示加载失败。这里的 `setTimeout` 是为了演示用的，如何获取组件取决于你自己。一个推荐的做法是将异步组件和 [webpack 的 code-splitting 功能](https://webpack.js.org/guides/code-splitting/)一起配合使用：

```
Vue.component('async-webpack-example', function (resolve) {
  // 这个特殊的 `require` 语法将会告诉 webpack
  // 自动将你的构建代码切割成多个包，这些包
  // 会通过 Ajax 请求加载
  require(['./my-async-component'], resolve)
})
```

你也可以在工厂函数中返回一个 `Promise`，所以把 webpack 2 和 ES2015 语法加在一起，我们可以这样使用动态导入：

```
Vue.component(
  'async-webpack-example',
  // 这个动态导入会返回一个 `Promise` 对象。
  () => import('./my-async-component')
)
```

当使用[局部注册](https://cn.vuejs.org/v2/guide/components-registration.html#局部注册)的时候，你也可以直接提供一个返回 `Promise` 的函数：

```
new Vue({
  // ...
  components: {
    'my-component': () => import('./my-async-component')
  }
})
```

如果你是一个 **Browserify** 用户同时喜欢使用异步组件，很不幸这个工具的作者[明确表示](https://github.com/substack/node-browserify/issues/58#issuecomment-21978224)异步加载“并不会被 Browserify 支持”，至少官方不会。Browserify 社区已经找到了[一些变通方案](https://github.com/vuejs/vuejs.org/issues/620)，这些方案可能会对已存在的复杂应用有帮助。对于其它的场景，我们推荐直接使用 webpack，以拥有内置的头等异步支持。

##### [处理加载状态](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#处理加载状态)

> 2.3.0+ 新增

这里的异步组件工厂函数也可以返回一个如下格式的对象：

```
const AsyncComponent = () => ({
  // 需要加载的组件 (应该是一个 `Promise` 对象)
  component: import('./MyComponent.vue'),
  // 异步组件加载时使用的组件
  loading: LoadingComponent,
  // 加载失败时使用的组件
  error: ErrorComponent,
  // 展示加载时组件的延时时间。默认值是 200 (毫秒)
  delay: 200,
  // 如果提供了超时时间且组件加载也超时了，
  // 则使用加载失败时使用的组件。默认值是：`Infinity`
  timeout: 3000
})
```

> 注意如果你希望在 [Vue Router](https://github.com/vuejs/vue-router) 的路由组件中使用上述语法的话，你必须使用 Vue Router 2.4.0+ 版本。



## 11 作用域插槽

![image-20201229164753268](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184535.png)



![image-20201229165010869](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184605.png)

![image-20201229165240753](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184615.png)

![image-20201229165314670](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184626.png)

![image-20201229165439355](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184634.png)



![image-20201229165546402](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184717.png)

![image-20201229165614989](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184725.png)





## 12 KEEP-ALIVE 的理解

![image-20201229160616716](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184740.png)

## 13. Vue 中常见的性能优化

![image-20201229160655750](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184747.png)

![image-20201229161025778](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184758.png)



## 14. 你知道 的VUE3 有哪些改进？

![image-20201229160921093](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184804.png)

1. Compositon API 解决了 mixins 中的缺陷，代码可以放在 setup 中，逻辑更具有耦合性，也更合理，数据更好追踪（mixins 混入的东西，在实例中不好追踪）

2. Proxy 提升性能，不用递归去设置 get/se
3. diff 算法改了，只会重新渲染动态数据



## 15 实现 Hash 路由和 history 路由

- onhashchange
- history.pushState

## 16 VUE 中导航守卫有哪些？

![image-20201229155223330](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184811.png)

## 17 action 和 mutation 的区别

![image-20201229155319937](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184820.png)

mutation 如果不是同步操作的话，在严格模式下会报错，利用 $watch  检测

## 18 简述VUEX 的原理

![image-20201229155401597](https://raw.githubusercontent.com/jiangzdongw/typora/typora/.p/20210206184825.png)



# 其他

## 1 双向绑定和vuex是否冲突

## 2 Vue中内置组件 transition、transition-group 的源码实现原理？

## 3 说说 patch 函数里做了些什么？

## 4 知道VUE 生命周期里函数是怎么实现的？

## 5 SSR 项目如果并发很大服务器性能该如何优化？

## 6 说下项目中如何实现权限校验？

## 7 讲一下 vue-lazyloader 的原理，手写伪代码？

## 8 Vue.set 的原理？

## 9 Vue compile 过程详细描述一下，指令、插值表达式等 vue 语法如何生效？