#### 在 Shoppingcart 组件中

##### 添加点击事件，阻止 a 链接默认行为

1. @click.prevent 阻止默认行为。

2. 渲染列表时，增加索引 i ，v-for 渲染页面时，每一项都有对应的索引值 i.

   ```html
   <div class="mui-card" v-for="(item, i) in goodslist" :key="item.id">
   ```

3. remove( item.id, i ) 传入两个参数，item.id 用于删除 store 的数据，i 索引 删除从服务器保存到组件data上的数据。

   ```html
   <a href="#" @click.prevent="remove(item.id, i)">删除</a>
   ```

##### remove( id, index );  分别删除对应数据

点击删除，1. 把商品信息从 store 中删除（ 根据 id ），2. 从组件 data 中删除 （ 索引 index ）。

```js
remove(id, index){
  this.goodslist.splice(index, 1)
  this.$store.commit("removeFromCart", id)
}
```

##### mutations 中定义删除方法

```js
removeFromCart(state, id){
  
  // 删除一般是根据索引来删。 记住用法！！   splice + 遍历的索引 i 
  state.cart.some( (item, i) => {
    if (item.id == id) {
      state.cart.splice(i, 1)
      return true
    }
  })
  // 删除完成后，最新的购物车数据，同步到本地存储。
  localStorage.setItem('cart', JSON.stringify(state.cart))
}
```

