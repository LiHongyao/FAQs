### 001：Vue生命周期 ⭐️

Vue 实例从创建到销毁的过程。

[生命周期图示 >>](https://cn.vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

[生命周期钩子 >>](https://v3.cn.vuejs.org/api/options-lifecycle-hooks.html)

### 002：谈谈你对keep-alive的了解

内置组件，用于缓存和保持组件的状态，以避免重复创建和销毁组件。

### 003：v-**if**和v-show区别

- `v-show`：通过修改元素的 display 属性让其显示或者隐藏；

- `v-if`：通过销毁和重建DOM达到让元素显示和隐藏的效果；

### 004：v-**if**和v-**for**优先级

当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。

### 005：**ref**是什么？

`ref` 是一个特殊的属性，用于在模板中给元素或组件注册一个引用。

### 006：谈谈你对nextTick的理解? ⭐️

定义：在下次DOM更新循环结束之后执行延迟回调。在修改数据之后立即使用它，获取更新后的DOM。

Q：为什么要使用nextTick？

A：Vue是异步执行DOM更新的



Q：使用场景

A：

1. 在created钩子函数中进行DOM操作时（因为此时DOM还未挂载渲染）
2. 数据更新之后立即获取更新后的DOM



Q：原理

A：Vue是异步执行 DOM 更新的，一旦观察到数据变化，Vue 就会开启一个队列，然后把在同一个事件循环当中观察到数据变化的 watcher 推送进这个队列。如果这个 watcher 被触发多次，只会被推送到队列一次。这种缓冲行为可以有效的去掉重复数据造成的不必要的计算和 DOM 操作。而在下一个事件循环时，Vue会清空队列，并进行必要的DOM更新。



### 007：**scoped** 原理 ⭐️

scoped 属性可以将样式作用域限制在当前组件的范围内，避免全局污染。其实现原理是通过给当前组件的所有选择器加上一个唯一的标识符（如 `data-v-xxx`），从而让当前组件的样式仅对带有这个标识符的元素生效。

具体来说，当一个 Vue 组件中使用了 `scoped` 属性时，Vue 在编译组件时会通过 PostCSS 插件（如 postcss-selector-scope）将组件中的所有样式选择器添加一个特殊的属性选择器，以确保样式只作用于当前组件。



### 008：Vue中如何做样式穿透？ ⭐️

1. Vue2

   - 使用 `::v-deep` 选择器：

     ```less
     /* 在父组件中 */
     .parent ::v-deep .child {
       /* 修改子组件的样式 */
     }
     ```

   - 使用 `/deep/` 选择器：

     ```less
     /* 在父组件中 */
     .parent /deep/ .child {
       /* 修改子组件的样式 */
     }
     ```

   - 使用 `>>>` 选择器（仅在单文件组件中有效）：

     ```less
     /* 在父组件中 */
     .parent >>> .child {
       /* 修改子组件的样式 */
     }
     ```

2. Vue3

   - `:deep(.类名)`
   - `::v-deep(.类名)`

3. `!important`

### 009：Vue组件传值 ⭐️

1. `$props ` ⇔ `$emits`
2. `v-model` 
3. `ref`
4. `provide` → `inject`
5. `eventBus`
6. `Vuex` / `Pinia`

### 010：computed、methods、watch有什么区别？

- `computed` 是用于声明计算属性，根据依赖的数据自动计算并缓存结果。
- `methods` 是用于定义组件中的方法，需要手动调用执行。
- `watch` 是用于观察数据的变化并执行相应的操作，适用于对数据变化做出响应或进行异步操作。

### 011：Vuex有哪些属性？

1. `state`：存储应用程序的状态数。
2. `mutaions`：同步状态变更，用于修改 `state` 中的状态。
3. `actions`：异步操作和提交 `mutations`。
4. `getters`：计算属性，用于从 `state` 中派生出新的状态数据。
5. `modules`：模块化管理状态。

### 012：Vuex是单向数据流还是双向数据流？

单向数据流

在 Vuex 中，数据流动是单向的，从 `state`（状态）到 `getters`（计算属性）到视图（组件），最后通过 `mutations`（同步变更）或 `actions`（异步操作）来修改状态。这遵循了 Flux 架构中的单向数据流概念。

当组件需要修改状态时，它们会触发 `mutations` 或 `actions` 来提交一个变更请求，然后在 `mutations` 中进行**同步的状态变更**。这种单向数据流确保了状态的可追踪性，因为所有的状态变更都经过中央的 `mutations`，我们可以清楚地看到每个状态的修改历史。

另外，由于 Vuex 中的状态是响应式的，当状态发生变化时，相关的组件会自动更新视图，从而保持视图与状态的同步。

需要注意的是，尽管 Vuex 的数据流是单向的，但并不意味着数据流只能从状态到视图。视图也可以通过提交 `mutations` 来修改状态，但这应该是通过 `actions` 或其他逻辑的结果，而不是直接在视图中修改状态。

### 013：Vuex中的mutaitons和actions区别

1. mutaions：仅支持同步操作
2. actions：支持异步

### 014：Vuex如何做持久化存储

- localStorage：监听 beforeunload 事件持久化state，每次加载应用时从本地读取
- 插件：vuex-persist

### 015：Vue路由模式

Vue路由模式主要有两种：**哈希模式** / **历史模式**

区别：

1. 表现形式不同
   - 历史模式：https://51plus.cn/index
   - 哈希模式：https://51plus.cn/#/index
2. 路由切换是否向服务器发送请求
   - 历史模式：https://51plus.cn/id → 发送请求
   - 哈希模式：不会发送请求 
3. 哈希模式是默认模式
4. 历史模式比哈希模式更符合传统的URL格式

### 016：介绍一下SPA以及SPA有什么缺点

SPA：**S**ingle-**P**age **A**pplication，单页应用。

优点：

1. 用户体验
2. 前后端分离
3. 可重用性和可维护性高
4. 快速响应

缺陷：

1. 首次加载较慢
2. SEO难度较高
3. 内存占用较大
4. 浏览器兼容性

### 017：双向绑定原理 ⭐️

Vue数据双向绑定原理是通过 **数据劫持结合发布者-订阅者模式** 的方式来实现的，首先是对**数据进行监听**，然后当**监听的属性发生变化时**则告诉订阅者是否要更新，若更新就会**执行对应的更新函数从而更新视图**。

### 018：什么是虚拟DOM？

虚拟DOM是一个用于表示真实DOM结构和属性的 **js对象**。

这个对象用于对比前后虚拟 DOM 的差异化，然后进行局部渲染从而实现性能上的优化。

### 019：为什么要用虚拟DOM？

浏览器在生成DOM树的时候，非常消耗资源，因此引入虚拟DOM概念通过一定的算法优化之后能够非常快捷的根据数据生成真实的html节点。

### 020：Diff算法 ⭐️

Diff算法是对虚拟DOM进行比较的算法，用于在更新视图时，实现局部更新，从而达到性能优化的目的。

1. Vue2使用**双向指针**来进行虚拟DOM的比较，而Vue3则使用了**单向链表**的方式。

2. 在计算key值不同时，Vue2会采用**首尾两端比较**的方法，而Vue3则采用了更高效的**Map数据结构**。

3. 在节点移动时，Vue2通过**splice**函数进行数组操作，而Vue3则采用了更轻量级的**移动节点**算法。

4. Vue3还增加了一种新的优化方式——**静态提升**，它可以将静态节点在编译阶段提前处理，避免在运行时进行比较。

总体来说，Vue3的diff算法相比Vue2更加高效，并且新增的静态提升优化方式可以进一步提升渲染性能

### 021：响应式原理 ⭐️

响应式原理3个步骤：数据劫持、依赖收集、派发更新

1. 从 new Vue 开始，首先通过 get、set 监听 Data 中的数据变化，同时创建 Dep 用来搜集使用该 Data 的 Watcher
2. 编译模板，创建 Watcher，并将 Dep.target 标识为当前 Watcher。
3. 编译模板时，如果使用到了 Data 中的数据，就会触发 Data 的 get 方法，然后调用 Dep.addSub 将 Watcher 搜集起来。
4. 数据更新时，会触发 Data 的 set 方法，然后调用 Dep.notify 通知所有使用到该 Data 的 Watcher 去更新 DOM。

### 022：data 为什么是函数？

避免数据污染

对象在栈中存储的都是地址，函数的作用就是属性私有化，保证组件修改自身属性时不会影响其他复用组件。

### 023：子组件prop接收数据之后刷新页面，数据丢失怎么处理？

1. 通过后台来保存数据
2. 本地持久化
3. 通过Vuex/Pinia持久化
4. 通过url传递参数，保存在url中

### 024：Vue2 vs Vue3 ⭐️

1. API模式不同

   - Vue2：选项式API
   - Vue3：选项式API / 组合式API

2. 检测机制的变化

   Vue3 中使用了ES6 的 Proxy API 对数据代理，监测的是整个对象，而不再是某个属性。

   - 消除了 Vue2 当中基于 Object.defineProperty 的实现所存在的很多限制。
   - Vue3可以监测到对象属性的添加和删除，可以监听数组的变化。
   - Vue3支持 Map、Set、WeakMap 和 WeakSet。

3. 建立数据的方式不同

   - Vue2：在data属性中定义数据
   - Vue3：在 `setup()` 函数中定义数据

4. 生命周期钩子不同

   - Vue3的钩子函数在Vue2的基础上加了on，如：created → onCreated
   - beforeDestory 和 destoryed 更名为 onBeforeUnmount 和 onUnmounted
   - 用setup代替beforeCreate和created。

5. 父子传参不同

   - definProps

总结：**Vue3 性能更高、体积更小、更利于复用、代码维护更方便**

### 025：defineProperty和Proxy的区别？⭐️

Vue 在实例初始化时遍历 data 中的所有属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。并劫持各个属性 getter 和 setter，在数据变化时发布消息给订阅者，触发相应的监听回调，而这之间存在几个问题。

1.  初始化时需要遍历对象所有 key，如果对象层次较深，性能不好

2. 通知更新过程需要维护大量 dep 实例和 watcher 实例，额外占用内存较多
3. Object.defineProperty 无法监听到数组元素的变化，只能通过劫持重写数组方法
4. 动态新增，删除对象属性无法拦截，只能用特定 set/delete API 代替
5. 不支持 Map、Set 等数据结构

Vue3 使用 Proxy 来监控数据的变化，Proxy 是 ES6 中提供的功能，其作用为：用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等），相对于Object.defineProperty()，其有以下特点：

1. Proxy 直接代理整个对象而非对象属性，这样只需做一层代理就可以监听同级结构下的所有属性变化，包括新增属性和删除属性。
2. 它的处理方式是在 getter 中去递归响应式，这样的好处是真正访问到的内部属性才会变成响应式，简单的可以说是按需实现响应式，减少性能消耗。
3. Proxy 可以监听数组的变化。

### 026：Vue3 Diff算法和 Vue2 的区别？⭐️

我们知道在数据变更触发页面重新渲染，会生成虚拟 DOM 并进行 patch 过程，这一过程在 Vue3 中的优化有如下

1. 编译阶段的优化
   - 事件缓存：将事件缓存(如: @click)，可以理解为变成静态的了
   - 静态提升：第一次创建静态节点时保存，后续直接复用
   - 添加静态标记：给节点添加静态标记，以优化 Diff 过程
     由于编译阶段的优化，除了能更快的生成虚拟 DOM 以外，还使得 Diff 时可以跳过"永远不会变化的节点"，
2. Diff 算法的优化
   - Vue2 是全量 Diff，Vue3 是静态标记 + 非全量 Diff
   - 使用最长递增子序列优化了对比流程

### 027：Vuex vs Pinia ⭐️

Pinia和Vuex都是Vue状态管理库，但是它们有一些区别：

1. API风格
   - Vuex 是 Vue.js 官方提供的状态管理库，它在 Vue 2 中被广泛使用。它使用基于选项的 API 设计，通过定义 `state`、`mutations`、`actions` 等选项来管理状态和处理业务逻辑。
   - Pinia 是一个由 Vue 社区维护的状态管理库，专门为 Vue 3 设计。它采用了基于类的 API 设计，通过定义 `state`、`getters`、`actions` 等类成员来管理状态和处理业务逻辑。
2. 响应式系统
   - Vuex 使用 Vue 2 的响应式系统来管理状态，它基于 Object.defineProperty() 来监听状态的变化，并在状态变化时触发视图更新。
   - Pinia 使用 Vue 3 的基于 Proxy 的响应式系统来管理状态，使用 Proxy 对象监听状态变化，并在状态变化时触发更新。这种基于 Proxy 的响应式系统在性能上优于 Vue 2 中的 Object.defineProperty()。
3. TypeScript 支持
   - Vuex 对 TypeScript 有一定的支持，提供了一些类型定义和接口声明，使得在 TypeScript 项目中使用时更加方便。
   - Pinia 在设计上更加友好于 TypeScript，并提供了更好的类型推断和类型检查支持，使得在 TypeScript 项目中的开发更加高效和安全。

### 028：Vue 🆚 React

https://worktile.com/kb/ask/19606.html

