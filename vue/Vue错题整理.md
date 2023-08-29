# Vue错题整理

## 23-3-5

1. 组件间传值相关：

   - 如果子组件修改，通过props获取的父组件传过去的==字符串或者数字==会报错 （√）

     > Vue组件间传值可以通过props、$emit、Vuex、事件总线这几种方法，通过修改props获取父组件的**基本数据类型**的值，在修改时会报错。（改深层数据比如数组、对象则不会报错）
     >
     > - props：仅能用于有祖先-子孙之间的通信
     >
     > - emit：适用于任意组件
     >
     > - Vuex：适用于任意组件间
     >
     > - 全局事件总线：适用于任意组件间通信，通过以下代码绑定事件：
     >
     >   ```vue
     >   methods(){
     >   demo(data){......}
     >   } 
     >   ......
     >   mounted() {        
     >   this.$bus.$on('xxxx',this.demo)  //这里的this.demo也可以替换成为箭头函数
     >   ```

   - 可以通过==context==进行组件间传值 （×）

     > context使用在**react**中进行组件间的传值，Vue没有

2. **单页面应用程序**（SPA）的特点：

   - 优点：
     - **无刷新切换**内容，提高用户体验。
     - 符合**前后端分离**的开发思想，通过ajax异步请求数据接口获取数据，后台只需要负责数据，不用考虑渲染。前端使用vue等MVVM框架渲染数据非常合适。
     - **减轻服务器压力**，展示逻辑和数据渲染在前端完成，服务器任务更明确，压力减轻。
     - 后端数据**接口可复用**，设计JSON格式数据可以在PC、移动端通用。

   - 缺点：

     - 不利于**SEO（搜索引擎优化**），应用数据是通过请求接口动态渲染，不利于SEO。

     > SEO就是指按照搜索引擎的算法，提升你的文章在搜索引擎中的自然排名
     >
     > ![img](https://pic4.zhimg.com/80/v2-575c3d03aa7e8a3f8003ee590eb23f3b_720w.webp)

     - **首页加载慢**，SPA下大部分的资源需要在首页加载，造成首页白屏等问题。

3. Vue与React

   - Vue和**React的this**都指向当前组件实例（×）

   - Vue进行数据拦截/代理，对数据更加敏感，数据驱动视图自更新，而React需要手动驱动数据更新视图（√）

     > - React 函数式组件中 this 为 **undefined**
     > - React 类式组件中：
     >   - constructor、render 中的 this 指向组件实例
     >   - 普通函数被组件实例调用，this 指向组件实例
     >   - 普通函数作为事件回调调用，**严格模式下 this 指向 undefined**，**非严格模式下 this 指向 window，需要通过 bind 修改指向**
     >   - 箭头函数没有自己的 this，this 为创建时的上下文，即指向组件实例

4. keep-alive

   - keep-alive 自身不会渲染成为一个DOM元素，也不会出现在组建的父组件链中（√）

   - max属性控制多可以缓存多少组件实例，一旦这个数字达到了，新创建的实例则不能再进行缓存。（×）

     > `<KeepAlive>` 是一个内置组件，它的功能是在多个组件间动态切换时缓存被移除的组件实例。
     >
     > ```vue
     > <!-- 非活跃的组件将会被缓存！ -->
     > <KeepAlive>
     >   <component :is="activeComponent" />
     > </KeepAlive>
     > ```
     >
     > `<KeepAlive>` 默认会缓存内部的所有组件实例，但我们可以通过 `include` 和 `exclude` prop 来定制该行为。这两个 prop 的值都可以是一个以英文逗号分隔的字符串、一个正则表达式，或是包含这两种类型的一个数组：
     >
     > 它会根据组件的 [`name`](https://cn.vuejs.org/api/options-misc.html#name) 选项进行匹配，所以组件如果想要条件性地被 `KeepAlive` 缓存，就必须显式声明一个 `name` 选项。
     >
     > ```vue
     > <!-- 以英文逗号分隔的字符串 -->
     > <KeepAlive include="a,b">
     >   <component :is="view" />
     > </KeepAlive>
     > 
     > <!-- 正则表达式 (需使用 `v-bind`) -->
     > <KeepAlive :include="/a|b/">
     >   <component :is="view" />
     > </KeepAlive>
     > 
     > <!-- 数组 (需使用 `v-bind`) -->
     > <KeepAlive :include="['a', 'b']">
     >   <component :is="view" />
     > </KeepAlive>
     > 
     > ```
     >
     > 我们可以通过传入 `max` prop 来限制可被缓存的最大组件实例数。`<KeepAlive>` 的行为在指定了 `max` 后类似一个 [LRU 缓存](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU))：如果缓存的实例数量即将超过指定的那个最大数量，则最久没有被访问的缓存实例将被销毁，以便为新的实例腾出空间。
     >
     > 当一个组件实例从 DOM 上移除但因为被 `<KeepAlive>` 缓存而仍作为组件树的一部分时，它将变为**不活跃**状态而不是被卸载。当一个组件实例作为缓存树的一部分插入到 DOM 中时，它将重新**被激活**。
     >
     > 一个持续存在的组件可以通过 [`activated`](https://cn.vuejs.org/api/options-lifecycle.html#activated) 和 [`deactivated`](https://cn.vuejs.org/api/options-lifecycle.html#deactivated) 选项来注册相应的两个状态的生命周期钩子：
     >
     > ```js
     > export default {
     >   activated() {
     >     // 在首次挂载、
     >     // 以及每次从缓存中被重新插入的时候调用
     >   },
     >   deactivated() {
     >     // 在从 DOM 上移除、进入缓存
     >     // 以及组件卸载时调用
     >   }
     > }
     > 
     > ```
     >
     > - `activated` 在组件挂载时也会调用，并且 `deactivated` 在组件卸载时也会调用。
     > - 这两个钩子不仅适用于 `<KeepAlive>` 缓存的根组件，也适用于缓存树中的后代组件。

5. Vue的特性

   - 轻量级
   - 双向数据绑定
   - 组件化
   - 数据驱动视图
   - 指令
   - 过滤器
   - 路由
   - 计算属性等

## 23-3-6

1. v-for

   - v-for指令基于一个数组来渲染一个列表 （√） Vue说明文档原文

2. Vuex

   - Vuex的属性有state、mutations、actions、**setters**等 （×）
     - vuex的**属性**：
       - state 存储状态
       - mutations 同步函数
       - actions 异步函数，并且调用的事mutations
       - getters 派生状态，类似与vue中的computed
       - module 组件，可以包含state，mutations，actions，getters，甚至module

   > 每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的**状态 (state)**。Vuex 和单纯的全局对象有以下两点不同：
   >
   > 1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
   > 2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。
   >
   > ```js
   > import { createApp } from 'vue'
   > import { createStore } from 'vuex'
   > 
   > // 创建一个新的 store 实例
   > const store = createStore({
   >   state () {
   >     return {
   >       count: 0
   >     }
   >   },
   >   mutations: {
   >     increment (state) {
   >       state.count++
   >     }
   >   }
   > })
   > 
   > const app = createApp({ /* 根组件 */ })
   > 
   > // 将 store 实例作为插件安装
   > app.use(store)
   > ```
   >
   > 现在，你可以通过 `store.state` 来获取状态对象，并通过 `store.commit` 方法触发状态变更：
   >
   > ```js
   > store.commit('increment')
   > console.log(store.state.count) // -> 1
   > ```
   >
   > 在 Vue 组件中， 可以通过 `this.$store` 访问store实例。现在我们可以从组件的方法提交一个变更
   >
   > ```js
   > methods: {
   >   increment() {
   >     this.$store.commit('increment')
   >     console.log(this.$store.state.count)
   >   }
   > }
   > ```

3. `$nextTick()`

   - 在created等虚拟DOM没有完成挂载的钩子函数中，不能把操作语句放在`$nextTick()`的回调函数中（×）

     > **定义**: 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM
     >
     > ```js
     > import { createApp, nextTick } from 'vue'
     > const app = createApp({
     >   setup() {
     >     const message = ref('Hello!')
     >     const changeMessage = async newMessage => {
     >       message.value = newMessage
     >       // 这里获取DOM的value是旧值
     >       await nextTick()
     >       // nextTick 后获取DOM的value是更新后的值
     >       console.log('Now DOM is updated')
     >     }
     >   }
     > })
     > ```
     >
     > js中主线程执行流程：
     >
     > ![image.png](https://static.vue-js.com/83308f80-d881-11ea-ae44-f5d67be454e7.png)
     >
     > `nextTick` 是 `vue` 中的更新策略，也是性能优化手段，基于`JS`执行机制实现
     >
     > ` vue`中我们改变数据时不会立即触发视图，如果需要实时获取到最新的`DOM`，这个时候可以手动调用 `nextTick `
     >
     > **总结：**
     >
     > ①vue更新dom时是异步更新的。简单说就是，有一个队列，里面都是等着更新的数据，数据都变完了，dom再跟新。就是异步更新。需要使用`$nextTick()`原因是Vue是异步渲染
     > ②使用场景：如果想要在修改数据后立刻得到更新后的DOM结构，可以使用`Vue.nextTick()`、在created等虚拟DOM没有完成挂载的钩子函数中，可以把操作语句放在`$nextTick`的回调函数中
     > ③原理：简单理解就是一个`setTimeout`函数

## 23-3-7

1. Vue

   - 当给某个组件**修改某个值**时，该组件**不会立刻重新渲染**（√）

     > ==vue中的dom是异步渲染的，不是立刻==

   - Vue内部使用原生`Promise.then`、`MutationObserver`和`seltmmediate` 实现异步队列，不会采用`setTimeout(fn,0)` （×）

     > Vue在内部对异步队列尝试使用原生的`Promise.then`、`MutationObserver`和`seltmmediate` ，如果执行环境不支持，则会采用`setTimeout(fn,0)`代替。

2. Vue自定义指令钩子函数

   - 自定义指令钩子函数参数 ‘el’ 指所绑定的元素，但是不可以通过 el 直接操作DOM元素（×）

     > **自定义指令**
     >
     > 全局定义：`Vue.directive( ' 自定义指令名 ' , { } )`；
     >
     > **参数一**是指令的名字，定义时指令前不需要加 v- 前缀，但调用的时候必须加上这个前缀；
     > **参数二**是一个对象，在这对象身上有一些指令相关的函数，这些函数可以在特定阶段执行相关的操作，叫**钩子函数**。
     >
     > 自定义指令钩子函数参数 ‘el’ 指所绑定的元素，**可以通过** el 直接操作DOM元素，比如：`el.style.color='red'`
     >
     > **钩子函数：**
     >
     > - `bind`：**只调用一次**，指令**第一次绑定**到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。
     >
     >   `inserted`：inserted表示元素插入到DOM中时，会执行inserted函数，**只触发一次**。
     >
     >   `update`：被绑定元素所在的模板**更新时调用**，而不论绑定值是否变化。
     >
     >   `componentUpdated`：被绑定元素所在模板完成**一次更新周期**时调用。
     >
     >   `unbind`：只调用一次，指令与元素**解绑时**调用。
     >
     > 执行顺序：bind ==> inserted ==> updated ==> componentUpdated ==> unbind
     >
     > **钩子函数所带参数：**
     >
     > - `el`：所绑定的元素，可直接操作dom
     >
     > - `binding`
     >
     >   ：可获取使用了此指令的绑定值有多个属性
     >
     >   - `name`：指令名，不包括v-前缀
     >   - `value`：指令的绑定值，如v-demo="1+1"中，绑定值为2
     >   - `oldValue`：指令绑定的前一个值，仅在update和componentUpdated中可用
     >   - `expression`：字符串形式的指令表达式,例如v-demo = "1 + 1"中，表达式为"1 + 1"
     >   - `argument`：传给指令的参数，可选。例如v-demo:message中，参数为"message"
     >   - `modifiers`：一个包含修饰符的对象。例如v-demo.foo.bar中，修饰符对象为{foo:true, bar:true}
     >
     > - `vnode`: 编译生成的虚拟节点
     > - `oldVnode`：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。
     >

3. Vue双向数据绑定

   - `Object.defineProperty(obj,key,val)`可以监听数组变化，不需要做数据处理（×）

     > `Object.defineProperty(obj,key,val)`不可以监听数组变化，需要做数据处理，所以Vue3使用Proxy实现数据监听。

   - 用户更新了View，Model的数据也自动被更新了，这种情况就是双向数据绑定。（√）

4. Vuex

   - Vuex是**单向数据流变更数据**。（√）

   - ajax一般放在mutations中，把获取到的数据存储在state中。（×）

     > **异步操作**放在**actions**中，actions通过commit调用mutations种方法操作state

5. 路由守卫

   - 单个路由独享的钩子函数只有一个`beforeEnter`（√）

   - 全局路由守卫的钩子函数有：`beforeRouteEach`(全局前置守卫)、`beforeRouteResolve`(全局解析守卫)、`afterRouteEach`（全局后置守卫）

     > 全局路由守卫的钩子函数有：`beforeEach`(全局前置守卫)、`beforeResolve`(全局解析守卫)、`afteEach`（全局后置守卫）
     >
     > 组件级路由守卫的钩子函数中间才有Route。
     >
     > 路由导航守卫分为 3 种：**全局路由守卫**、**路由独享的守卫**、组件内的守卫
     >
     > - 全局路由守卫：
     >   - 全局前置守卫：beforeEach
     >   - 全局解析守卫：beforeResolve
     >   - 全局后置钩子：afterEach
     > - 路由独享的守卫：beforeEnter
     > - 组件内的守卫：
     >   - beforeRouteEnter
     >   - beforeRouteUpdate
     >   - beforeRouteLeave

## 23-3-8

1. v-model

   - v-model是内置命令，不能使用在**自定义组件**中（×）

     > vue2.2+版本新增了一个功能，可以在自定义组件上使用v-model实现双向数据绑定。
     >
     > ```vue
     > <template>
     >   <!-- 自定义组件中使用v-mode指令 -->
     >   <input type="search" @input="changeInput" data-myValue="">
     > </template>
     > 
     > <script>
     > export default {
     >   name: 'CustomModel',
     >   // 当我们使用model的默认值的时候value作prop，input作event时，可以省略不写model。
     >   model: {
     >     prop: 'myValue', // 默认是value
     >     event: 'myInput', // 默认是input
     >   },
     >   props: {
     >     // 接收string和number类型的值，
     >     // 注意不能是写成字符串["String","Number"],因为此时它们是构造器，是全局变量
     >     myValue: [String, Number],
     >   },
     >   methods: {
     >     changeInput ($event) {
     >       // 向上派发myInput事件，这样model监听myInput才有意义：当输入字符时触发input事件，
     >       // 进而派发触发自定义的myInput事件，然后model监听myInput，就实现了数据绑定
     >       this.$emit('myInput', $event.target.value)
     >     },
     >   }
     > }
     > </script>
     > 
     > ```
     >
     > ```vue
     >  <!-- 父组件 -->
     > <template>
     >   <div class="home">
     >     <h3>输入的实时内容：{{ myValue }}</h3>
     >     <custom-model v-model="myValue"></custom-model>
     >   </div>
     > </template>
     > 
     > <script>
     > import CustomModel from './CustomModel'
     > 
     > export default {
     >   name: 'Home',
     >   components: {
     >     CustomModel,
     >   },
     >   data () {
     >     return {
     >       myValue: ''
     >     }
     >   },
     > }
     > </script>
     > ```
     >
     > 

   - 对input使用v-model，实际上是指定其**:value**和**input**事件（√）

2. `vue-lazyload`

   - 组件中使用`vue-lazyload`时，必须要加**:key**属性（×）

   - 使用`vue-lazyload`时，扩展功能api中的attempt代表尝试加载图片数量（√）

     > `vue-lazyload`：图片懒加载的一种方式
     >
     > **安装**：
     >
     > ```sh
     > npm i vue-lazyload
     > ```
     >
     > **参数介绍：**
     >
     > | key               | description                                        | default                                                      | options                                                      |
     > | ----------------- | -------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
     > | `preLoad`         | proportion of pre-loading height 预加载的高度比例  | `1.3`                                                        | `Number`                                                     |
     > | `error`           | src of the image upon load fail 加载错误显示的图片 | `'data-src'`                                                 | `String`                                                     |
     > | `loading`         | src of the image while loading 加载时显示的图片    | `'data-src'`                                                 | `String`                                                     |
     > | `attempt`         | attempts count 尝试加载的数量                      | `3`                                                          | `Number`                                                     |
     > | `listenEvents`    | events that you want vue listen for                | `['scroll', 'wheel', 'mousewheel', 'resize', 'animationend', 'transitionend', 'touchmove']` | [Desired Listen Events](https://www.npmjs.com/package/vue-lazyload#desired-listen-events) |
     > | `adapter`         | dynamically modify the attribute of element        | `{ }`                                                        | [Element Adapter](https://www.npmjs.com/package/vue-lazyload#element-adapter) |
     > | `filter`          | the image's listener filter                        | `{ }`                                                        | [Image listener filter](https://www.npmjs.com/package/vue-lazyload#image-listener-filter) |
     > | `lazyComponent`   | lazyload component                                 | `false`                                                      | [Lazy Component](https://www.npmjs.com/package/vue-lazyload#lazy-component) |
     > | `dispatchEvent`   | trigger the dom event                              | `false`                                                      | `Boolean`                                                    |
     > | `throttleWait`    | throttle wait                                      | `200`                                                        | `Number`                                                     |
     > | `observer`        | use IntersectionObserver                           | `false`                                                      | `Boolean`                                                    |
     > | `observerOptions` | IntersectionObserver options                       | { rootMargin: '0px', threshold: 0.1 }                        | [IntersectionObserver](https://www.npmjs.com/package/vue-lazyload#intersectionobserver) |
     > | `silent`          | do not print debug info                            | `true`                                                       | `Boolean`                                                    |
     >
     > **用法**：
     >
     > ```js
     > import VueLazyload from 'vue-lazyload'  //引入这个懒加载插件
     > 
     > Vue.use(VueLazyLoad, {
     >   preLoad: 1,
     >   error: require('./assets/img/error.jpg'),
     >   loading: require('./assets/img/homePage_top.jpg'),
     >   attempt: 2,
     > })
     > ```
     >
     > **使用：**在入口文件添加后，在组件任何地方都可以直接使用把 `img` 里的`:src -> v-lazy`，使用时最好给一个 key 属性，也可以不加
     >
     > ```html
     > <!-- img中使用图片懒加载。 v-lazy代替v-bind:src -->
     > <ul class="img">
     >     <li v-for="(item,index) in imgList"> 
     >         <img v-lazy="item" alt="" style="width: 768px;" :key='item'> 
     >     </li>
     > </ul>
     > ```

3. 路由模式

   - hash模式是通过`onchange`事件，监听 url 的修改。（√）

   - history模式需要后端进行配合。（×）

     > vue路由的三种模式：
     >
     > - hash模式
     >
     >   即地址栏 URL 中的 `#` 符号（此 hash 不是密码学里的散列运算）。
     >   比如这个 URL：`http://www.abc.com/#/hello`，hash 的值为 `#/hello`。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。监听hash改变时使用的方法是：`onhashchange`，也可以通过`window.location.hash`来获取或修改hash值
     >
     > - history模式
     >
     >   美化后的hash模式，会去掉路径中的 “#”。利用了 HTML5 History Interface 中新增的 `pushState()` 和 `replaceState()` 方法。（需要特定浏览器支持 i9以上）
     >   这两个方法应用于浏览器的历史记录栈，在当前已有的 `back`、`forward`、`go`（对应浏览器的前进，后退，跳转操作） 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。
     >
     > - abstract路由模式
     >
     >   abstract 是vue路由中的第三种模式，本身是用来在不支持浏览器API的环境中，充当fallback，而不论是hash还是history模式都会对浏览器上的url产生作用，本文要实现的功能就是在已存在的路由页面中内嵌其他的路由页面，而保持在浏览器当中依旧显示当前页面的路由path，这就利用到了abstract这种与浏览器分离的路由模式。

## 23-3-10

1. vue中的diff算法

   - 当老VNode节点的start和新VNode节点的end满足sameVnode时，新VNode节点会被提到start位置。（×）

     > diff 算法是一种通过同层的树节点进行比较的高效算法，避免了对树进行逐层搜索遍历，所以时间复杂度只有 O(n)。diff 算法的在很多场景下都有应用，例如在 vue 虚拟 dom 渲染成真实 dom 的新旧 VNode 节点比较更新时，就用到了该算法。diff 算法有两个比较显著的特点：
     >
     > - 比较只会在同层级进行, 不会跨层级比较。
     >
     >   ![img](https://static001.infoq.cn/resource/image/91/54/91e9c9519a11caa0c5bf70714383f054.png)
     >
     > - 在 diff 比较的过程中，循环从两边向中间收拢。
     >
     >   ![img](https://static001.infoq.cn/resource/image/2d/ec/2dcd6ad5cf82c65b9cfc43a27ba1e4ec.png)
     >
     > **diff流程**：
     >
     > 1. vue 的虚拟 dom 渲染真实 dom 的过程中首先会对新老 VNode 的开始和结束位置进行标记：oldStartIdx、oldEndIdx、newStartIdx、newEndIdx。
     >
     >    ![img](https://static001.infoq.cn/resource/image/80/6d/80dc339f73b186479e6d1fc18bfbf66d.png)
     >
     > 2. 标记好节点位置之后，就开始进入到的 while 循环处理中，这里是 diff 算法的核心流程，分情况进行了新老节点的比较并移动对应的 VNode 节点。while 循环的退出条件是直到老节点或者新节点的开始位置大于结束位置。
     >
     > 3. 循环过程中首先对新老 VNode 节点的头尾进行比较，寻找相同节点，如果有相同节点满足 sameVnode（可以复用的相同节点） 则直接进行 patchVnode (该方法进行节点复用处理)，并且根据具体情形，移动新老节点的 VNode 索引，以便进入下一次循环处理，一共有 2 * 2 = 4 种情形。下面根据代码展开分析:
     >
     >    - 当新老 VNode 节点的 start 满足 sameVnode 时，直接 patchVnode 即可，同时新老 VNode 节点的开始索引都加 1。
     >    - 当新老 VNode 节点的 end 满足 sameVnode 时，同样直接 patchVnode 即可，同时新老 VNode 节点的结束索引都减 1。
     >    - 当老 VNode 节点的 start 和新 VNode 节点的 end 满足 sameVnode 时，这说明这次数据更新后 oldStartVnode 已经跑到了 oldEndVnode 后面去了。这时候在 patchVnode 后，还需要将当前真实 dom 节点移动到 oldEndVnode 的后面，同时老 VNode 节点start索引加 1，新 VNode 节点的end索引减 1。
     >    - 当老 VNode 节点的 end 和新 VNode 节点的 start 满足 sameVnode 时，这说明这次数据更新后 oldEndVnode 跑到了 oldStartVnode 的前面去了。这时候在 patchVnode 后，还需要将当前真实 dom 节点移动到 oldStartVnode 的前面，同时老 VNode 节点结束索引减 1，新 VNode 节点的开始索引加 1。
     >    - 如果都不满足以上四种情形，那说明没有相同的节点可以复用。于是则通过查找事先建立好的以旧的 VNode 为 key 值，对应 index 序列为 value 值的哈希表。从这个哈希表中找到与 newStartVnode 一致 key 的旧的 VNode 节点，如果两者满足 sameVnode 的条件，在进行 patchVnode 的同时会将这个真实 dom 移动到 oldStartVnode 对应的真实 dom 的前面；如果没有找到，则说明当前索引下的新的 VNode 节点在旧的 VNode 队列中不存在，无法进行节点的复用，那么就只能调用 createElm 创建一个新的 dom 节点放到当前 newStartIdx 的位置。
     >
     > 4. 当 while 循环结束后，根据新老节点的数目不同，做相应的节点添加或者删除。若新节点数目大于老节点则需要把多出来的节点创建出来加入到真实 dom 中，反之若老节点数目大于新节点则需要把多出来的老节点从真实 dom 中删除。至此整个 diff 过程就已经全部完成了。

## 23-3-12

1. vue中数组的操作：下列对数组的操作哪个不会引起视图的更新

   - concat （√） //会生成新数组

     > Vue监视数据的原理：
     >
     > 1. vue会监视data中**所有层次**的数据。
     >
     >   2. 如何监测对象中的数据？
     >
     >      通过**setter**实现监视，且要在new Vue时就传入要监测的数据。
     >      (1).对象中后追加的属性，Vue默认不做响应式处理
     >      (2).如需给后添加的属性做响应式，请使用如下API：
     >      	**Vue.set**(target，propertyName/index，value) 或 
     >      	**vm.$set**(target，propertyName/index，value)
     >
     >
     > 3. 如何监测数组中的数据？
     >
     >    通过**包裹数组**更新元素的方法实现，本质就是做了两件事：
     >    (1).调用原生对应的方法对数组进行更新。
     >    (2).重新解析模板，进而更新页面。
     >
     > 4. 在**Vue修改数组**中的某个元素一定要用如下方法：
     >
     >    1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
     >    2.Vue.set() 或 vm.$set()
     >
     >    5. Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！