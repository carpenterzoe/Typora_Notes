##### getters 中定义的方法

当selected状态为选中，遍历 state.cart 这个购物车商品信息数组，得出购物车中所有选中商品的数量 count，和单价 price * count

```js
getGoodsCountAndAmount(state){
  var o = {
    count: 0,  // 勾选的数量
    amount: 0  // 勾选的总价
  }
  state.cart.forEach( item => {
    if(item.selected){
      o.count += item.count   // 所有选中的商品数量累加到 o.count
      o.amount += item.price + item.count  // 所有单价(price*count) 累加到 o.amount
    }
  })
  return o
}
```

##### 在 Shoppingcart 调用

getters 数据会根据 state 变化而变化。

```html
<p>已勾选商品 <span class="red">{{ $store.getters.getGoodsCountAndAmount.count }}</span>
件，总价<span class="red">￥{{ $store.getters.getGoodsCountAndAmount.amount }}</span></p>
```

