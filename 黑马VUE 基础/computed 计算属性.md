##### computed计算属性的特点

1. 计算属性的本质是一个方法，但是在使用的时候，是把它们的名称直接当作 普通属性 来使用，而不是当作方法去调用。

2. 计算属性的 function 内部所用到的任何 data值 发生变化，都会立即重新计算这个计算属性的值。

   ```js
   var vm = new Vue({
     el: '#app',
     data: {
       firstname: '',
       lastname: ''
     },
     methods: {},
   
     computed: {
       'fullname': function(){
         return  this.firstname + '-' + this.lastname
       }
     }
   })
   ```

   

3. 计算属性的求值结果会被缓存起来，方便下次直接使用。如果计算属性方法中的任何数据都没有发生变化，则不会重新对计算属性求值。

   例如：多处调用了同一个计算属性，其实只有第一次调用的是受数据变化影响而计算的，其他处调用的是缓存的值。

```html
// 调用
<input type="text" v-model="firstname">
<input type="text" v-model="lastname">
  
<input type="text" v-model="fullname">   
// 这里的 fullname 就是通过计算属性绑定的，而不是绑定了方法。

<p> {{ fullname }} </p>
<p> {{ fullname }} </p>
<p> {{ fullname }} </p>    // 这里多次调用的是缓存值。
```

