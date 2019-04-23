##### 在 main.js 的 Vuex  store 仓储中

```js
var store = new Vuex.Store({
  state: {
    cart: []  // 将购物车中商品的数据，用数组存储起来
  }
```

##### 设计商品对象

```js
{ id: 商品的id, count: 要购买的数量, price: 商品的单价, selected: true }
```

##### 在 GoodsInfo.vue 中，点击购物车，调用 addToCart( );

1. 拼接出一个要保存到store中cart数组里的 商品信息对象
2. 在方法内部触发 mutations 中的方法

```js
addToCart(){
  // 拼接出一个要保存到store中cart数组里的 商品信息对象
  var goodsinfo = { 
    id: this.id,  // 商品详情 data 里的 id
    count: this.selectedCount,
    price: this.goodsinfo.sell_price, // 从服务器获取的商品价格
    selected: true // 默认在购物车中选中该商品
  }
  // 在方法内部 触发 mutations 中的方法
  // 把拼接的商品信息对象保存到 state
  this.$store.commit('addToShoppingCart', goodsinfo)
},
```

##### 在 mutations 中，把拼接的商品信息对象 保存到 state

加入购物车的逻辑：

1. **如果购物车里已经有该商品，那么只增加数量 count 。**

   判断购物车里有无该商品，数组方法  some( ); 

   ```js
   state.cart.some(item => {
     if(item.id == goodsinfo.id) {
       item.count += parseInt(goodsinfo.count) // 客户端传过来的可能是字符串
       return true // 找到了对应的id，中止some循环
     }
   })
   ```

   > some() 方法用于检测数组中的元素是否满足指定条件（函数提供）。
   >
   > some() 方法会依次执行数组的每个元素：
   >
   > - 如果有一个元素满足条件，则表达式返回*true* , 剩余的元素不会再执行检测。
   > - 如果没有满足条件的元素，则返回false。
   >
   > **注意：** some() 不会对空数组进行检测。
   >
   > **注意：** some() 不会改变原始数组。

   

2. 如果some( ); 方法把数组整个遍历完了也没有找到对应id，表示购物车里没有该商品，就把整个商品信息对象 push 到 state 中的 cart 数组里。

   1. 启用 flag 标识符，先赋值为 false。

      > 要注意 启用标识符 false / true 布尔值转换的用法！！！

   2. 一旦找到了对应id，执行了增加count值的函数，就把 flag 赋值为 true。
   3. false 代表没找到已存在的id，true代表找到了已存在的id。
   4. 在some(); 方法之外，判断 flag 是否为 false，false 时才把商品信息对象整个push 到 cart 数组里。 

   ```js
   addToShoppingCart(state, goodsinfo){
     
     var flag = false   // 启用 flag 标识符
     
     state.cart.some(item => {
       if(item.id == goodsinfo.id) {
         item.count += parseInt(goodsinfo.count)
         flag = true  // 如果找到了对应id，执行完增加count值的函数后，就把flag 赋值为 true
         return true
       }
     })
   
     if(flag === false){  // 只有当flag仍为 false(即初始值)时，才表示没有找到对应id
       state.cart.push(goodsinfo)  // 就直接把整个商品信息对象都 push 到 cart 数组里。
     }
   }
   ```

##### if (flag === false)   和 if ( !flag )  

if ( flag ) 表示 当 flag 为 true 时才执行后面的代码块。即 if ( flag === true )

所以if ( !flag )  等同于  if ( !flag === true)，则  flag === false

if 语句的括号内，如果只有变量，没有用于判断的 === ，则表示括号内的值为 true 才能执行后续代码块。



