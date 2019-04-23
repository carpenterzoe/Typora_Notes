##### 安装vuex

```javascript
npm install vuex --save
```

##### 在 main.js 中，通过 Vue.use(Vuex) 注册 vuex 到 vue 中 

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```

##### 实例化 store，得到数据仓储对象

```js
const store = new Vuex.Store({
   state: {
      // 可以想象成组件中的data
      count: 0
   },
   mutations: {
      // 相当于组件中的 methods
      // mutations 里的方法专门用来操作 state 里的数据
   }
})
```

##### 把 **store** 挂载到vue实例中

```javascript
const vm = new Vue ({
   el: '#app',
   render: c => c(App),
   store // 只要挂载到了 vm 实例上，任何组件都能使用 store 来存取数据
})
```

##### $store  - 在组件中访问 store 的数据 - 直接引用 和 computed

1. $store.state.***   直接引用

   ```javascript
   v-model="$store.state.***"
   ```

2. computed 计算属性

   不需要用属性绑定传值，也不需要用event事件给父级传值。

   ```javascript
   // .vue 文件  script 标签中
   export default {
      computed: {
         products(){
            return this.$store.state.products
         }
      }
   }
   ```

   

##### mutations基本语法

```javascript
mutations: {
	// 方法中的第一个参数必须是 state
   increment(state) {
      state.count ++
   }
}
```

##### 子组件中调用 mutations

当触发事件时用mutations

```javascript
methods: {
   // 在 add() 代码块内部，通过 this.$store.commit("方法名") 来使用在 mutations 中定义的方法。
   // 在子组件template中实际调用的还是 @click = "add"   即 methods 中的方法名。
   add(){
      this.$store.commit("increment");
   }
}
```

##### mutations  和 methods 区别

1. 混用 vuex 和 子组件中自己的 methods，虽然可以生效，但不符合 vuex 的设计理念。
2. 在严格模式下，混用会报错。
3. 用 Vue devtools 时，用 mutations 才会提示当前触发的方法，更方便追踪调试。 而直接用 methods 触发是没有显示的。

##### mutations 传参

```javascript
mutations: {
	// 传一个参
	substract(state, num){
      state.count -= num
	}
}

// 子组件中 commit 传值， 单个值
methods: {
   remove() {
      this.$store.commit("substract", 3)
      // ("方法名", 参数)
	}
}
```

```javascript
mutations: {
   // 传多个参 -- 传对象
	substract(state, obj){
      state.count -= (obj.c + obj.d)
	}
}

// 子组件中 commit 传值， 对象
methods: {
   remove() {
      this.$store.commit("substract", {c:3, d:1})
      // ("方法名", 对象参数)
	}
}
```

##### getters

和 过滤器 类似点：都没有修改原数据，而是对原数据做一层包装。

和 computed 类似点：如果state中的数据发生变化，且getters引用了该数据，就会立即触发getters重新求值。

```javascript
getters: {
   optCount: function(state){
      return '当前最新的count值是:' + state.count
   }
}
```

```html
// 子组件 template中调用 getters
<h3>{{ $store.getters.optCount }} </h3>
```

##### 总结 state  mutations  getters

1. state 中的数据不能直接修改，如果想要修改，必须通过mutations
2. 组件从state上获取数据： this.$store.state.***
3. 组件修改数据必须通过 mutations 提供的方法，通过 this.$store.commit('方法的名称', 参数)
4. 如果store仓储中的state数据，在对外提供的时候需要做一层包装，推荐使用getters
5. 调用getters处理过的数据：this.$store.getters.***2

##### mutations 和 getters 区别 （个人理解

getters的方法操作的是基于state数据变动的一套副本数据，不改变state原本的值。所以等于是提供了两套数据供组件使用。

mutations 是直接修改state的值。