Vuex是Vue配套的 公共数据管理工具，它可以把一些共享的数据，保存到vuex中，方便整个程序中的任何组件直接获取或修改公共数据。

##### vuex安装

```js
cnpm i vuex -S
```

##### 导入包

```
import Vuex from 'vuex'
```

##### 注册 vuex 到 vue 中

```
Vue.use(Vuex)
```

##### new Vuex.Store( ) 实例，得到 数据仓储对象

```js
var store = new Vuex.Store({
  state: {
    // 可以把 state 想象成组件中的 data，专门用来存储数据
    count: 0
  }
}),
mutations: {}
```

##### 把 store 挂载到 vm 实例上

```js
const vm = new Vue({
  el: '#app',
  render: c=>c(App),
  store 
  // 将 vuex 创建的 store 挂载到vm实例上
  // 
})
```

##### 在组件中访问store中的数据

只要把store挂载到了 vm 上，任何组件都能使用 $store 来存取数据

```
$store.state.count
```

##### 不要用组件内部的 methods 修改 store 数据

原因：如果导致数据紊乱，不能快速定位到错误的原因。因为每个组件都可能有操作数据的方法。

##### mutations

```js
var store = new Vuex.Store({
  state: {
    count: 0
  }
}),
mutations: { // 在mutations里定义 修改state数据的方法。
  
  increment(state){ // mutations 中定义的函数，第一个参数是规定好的 state。
    state.count++
  }
}
```

##### 组件内部调用 mutations 中的方法，this.$store.commit('方法名')

```js
methods: {
  add(){
    this.$store.commit('increment')
  }
}
```

##### mutations 传参

```js
// 传一个参
mutations: {
  increment(state, c){
    state.count += c
  }
}
// 组件中调用
methods: {
  add(){
    this.$store.commit('increment', 3)
  }
}

// 传多个参，用对象
mutations: {
  increment(state, obj){
    state.count += (obj.c + obj.d)
  }
}
// 调用
methods: {
  add(){
    this.$store.commit('increment', {c:3, d:1})
  }
}
```

##### getters

getters 里面的内容都是function，第一个参数都是 state。

```js
getters: {
  optCount: function(state){
    return '当前最新的count值是：' + state.count
  }
}

// 组件中调用
$store.getters.optCount
```

getters 和 过滤器 相似点：都没有修改原数据，只是把原数据做了一层包装，提供给了调用者。

getters 和 computed 相似点：只要state中的数据发生变化， 且getters引用了这个数据，就会触发 getters 重新求值。