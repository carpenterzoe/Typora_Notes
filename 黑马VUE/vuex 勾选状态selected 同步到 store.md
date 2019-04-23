#### 把 store 中 selected 的选中状态同步到购物车列表

##### getters中定义方法，获取键值对 { item.id: item.selected }

1. 定义一个空对象

2. 遍历 cart 数组里的每个商品信息对象，获取每一项的 id 和 selected布尔值。

3. **用获取到的 id 和 selected布尔值 组成键值对，往 现有的空对象o 里 新增键值对  o[key] = value**  

   // 注意这个用法！

4. 返回 保存了 id 和 selected布尔值 对应关系的这个对象。

   **获取到的数据格式：{ "88": true, "89": true, "90": true }**   // 都是true，因为在一开始初始化商品信息对象时默认都写的true。

```js
getGoodsSelected(state){
  var o = {}
  state.cart.forEach( item => {
    o[item.id] = item.selected
  })
  return o // o 这个对象上保存了 id 和 selected 的对应关系 { item.id: item.selected }
}
```

##### 在 Shoppingcart 组件中，调用 getters 的数据

1. v-model 绑定的value，true / false，会触发 mt-switch 显示按钮选中与否。
2. $store.getters.getGoodsSelected[item.id]   用这个方法，获取到 对应id是 true 或 false 的数据布尔值。

```html
<mt-switch v-model="$store.getters.getGoodsSelected[item.id]"></mt-switch>
```

注意这里调用getters是直接写方法名，后面跟中括号[key]，来获取对应value。

而不是写方法里return的对象 o

```js
$store.getters.getGoodsCount[item.id]
```

#### 在购物车列表页面，点击选中取消，同步到store

这里的v-model 没有起到双向数据绑定的作用，因为 store 里的数据不能直接通过 v-model 双向绑定，getters的数据只是用来取用的。

修改数据需要通过mutations定义方法。

```html
<mt-switch v-model="$store.getters.getGoodsSelected[item.id]"
            @change="selectedChanged(item.id, $store.getters.getGoodsSelected[item.id])">
```

##### 在 mutations 中定义修改 state.cart 数据的方法

1. 遍历state.cart 数组，判断 传入的 info对象的id值，是否和数组item.id 相符。
2. 找到对应的item之后，把传入的info对象身上的 selected 布尔值 保存到state中。

```js
updateGoodsSelected(state, info){
  state.cart.some( item => {
    if (item.id == info.id) {
      item.selected = info.selected
    }
  })
  // 最新的所有购物车商品状态，保存到 localStorage
  localStorage.setItem('cart', JSON.stringify(state.cart))
}
```

##### mt-switch 的 @change 事件，触发 mutations 定义好的方法

```html
<mt-switch v-model="$store.getters.getGoodsSelected[item.id]"
            @change="selectedChanged(item.id, $store.getters.getGoodsSelected[item.id])">
```

```js
selectedChanged(id, val){
  this.$store.commit('updateGoodsSelected', { id, selected: val })
}
```

