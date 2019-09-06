##### 获取state.cart数组中 每个对象的 count 值，并累加

```js
state: {
  cart: [{ id: 商品的id, count: 要购买的数量, price: 商品的单价, selected: true }] // 数组中有多个商品信息对象
},
getters: {
  getAllCount(state){
    var c = 0;
    state.cart.forEach( item => {  // 遍历数组中的每一项 item
      c += item.count
    })
    return c  // 最终 c 就是state.cart中 count值的总和
  },
```

##### 在App.vue 中调用getters方法获取的值

```html
<span id="badge"> {{ $store.getters.getAllCount }}</span>  // 没有 this
```

