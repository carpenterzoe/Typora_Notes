##### 点击加入购物车，触发mutations的addToCart( ) 方法

1. 把商品信息添加到 store 里面。

2. 在 localStorage 里也保存一份最新的商品信息。

   无论 mutations 里的 addToShoppingCart 方法，执行的是增加商品数量，还是push整个新的商品信息，在执行完了之后，都保存到 localStorage里。

   > 保存数据：localStorage.setItem(key,value);
   >
   > 读取数据：localStorage.getItem(key);
   >
   > localStorage 存储的是 字符串值，所以保存时，需要用 JSON.stringfy( ); ，读取时 JSON.parse( );

```js
mutations: {
  addToShoppingCart(state, goodsinfo){
    var flag = false
    // 点击加入购物车，把商品信息保存到 state 中的 cart 上
    state.cart.some(item => {
      if(item.id == goodsinfo.id) {
        item.count += parseInt(goodsinfo.count)
        flag = true
        return true
      }
    })

    if(flag === false){
      state.cart.push(goodsinfo)
    }
    
    // 当更新完 cart 之后，把 cart 数组存储到本地 localStorage
    // 保存数据：localStorage.setItem(key,value);
    
    localStorage.setItem('cart', JSON.stringify(state.cart))
  },
}   
```

##### 用户进入页面时，会运行main.js，需要读取localStorage里的数据

每次刚进入网站，肯定会调用main.js。

在调用时，把本地localStorage存储的购物车数据读出来，放到 store 中。

```js
Vue.use(Vuex)

var cart_local = JSON.parse(localStorage.getItem('cart') || '[]')

var store = new Vuex.Store({
  state: {
    cart: cart_local  // 将购物车中商品的数据，用数组存储起来
  },
```

