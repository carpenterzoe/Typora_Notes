##### 监听 data 的变化

```js
var vm = new Vue({
  el: '#app',
  data: {
    firstname: '',
    lastname: ''
	},
  methods: {},
  // 使用 watch 属性，可以监视 data 中指定数据的变化，然后触发对应的 function 处理函数。
  watch: {
    'firstname': function(newVal, oldVal){
      // 当 firstname 的数据发生变化，会触发这里的函数。
      
      // 两个参数， newVal 最新的数据  oldVal 旧的数据
      // 参数可写可不写，有需要才写。
    }
  }
})
```

##### watch 监视路由变化

```js
watch: {
  '$route.path': function(newVal, oldVal){
    // 当路由地址发生变化，会触发这里的函数。
    
    // watch 适合监听非dom元素的数据改变。
  }
}
```

