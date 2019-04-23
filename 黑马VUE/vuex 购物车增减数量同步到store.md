P 196

##### input 标签添加 readonly 属性

1. 该输入框不能再通过双击，用户输入字符来更改value。
2. 在number box 组件中，仍然可以通过两边的 + - 按钮来实现增减数量。

##### 在 Shoppingcart 中 给子组件 NumberBox_Cart 传 id

```html
<numbox :initcount="$store.getters.getGoodsCount[item.id]" 
        :goodsid="item.id"></numbox>   // item.id 就是循环每一项的id
```

没有id，在进行数量增减操作时，不知道对应的是哪个商品。

这样在 NumberBox_Cart 中就可以使用父组件传过来的 id。

##### 在 mutations 中 定义 updateGoodsInfo( ); 方法，修改购物车中 商品的数量值

```js
updateGoodsInfo(state, goodsinfo){  // goodsinfo形参，表示 组件调用该方法时传入的对象或者值。
  state.cart.some( item => {
    if(item.id == goodsinfo.id) {
      item.count = parseInt(goodsinfo.count)
      return true
    }
  })
  // 修改完商品的数量，把最新的购物车数据 保存到本地存储中。
  localStorage.setItem('cart', JSON.stringify(state.cart))
}
```

每当数量值改变，把最新的数量同步到store中，覆盖之前的数量值。

在 NumberBox_Cart 中，文本框的值发生变化，就会触发@change后面的方法

```html
<input id="test" class="mui-input-numbox" type="number" :value="initcount" 
    @change="countChanged" ref="numbox" readonly/>
```

```js
methods: {
  countChanged(){
    this.$store.commit("updateGoodsInfo", {   
      id: this.goodsid,
      count: this.$refs.numbox.value
    })
      // 触发 mutations 里的方法
      // 第一个参数，要触发的方法名
      // 第二个参数，调用该方法传入的参数。即 mutations的 updateGoodsInfo();里的 goodsinfo.
  }
},
 	props: ["goodsid"]
}
```

