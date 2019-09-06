P194

##### 从服务器获取购物车列表的数据

根据API文档的要求，请求地址是

```js
 api/goods/getshopcarlist/:ids
 // ids：商品 id 字符串，多个id之间用逗号分隔  例：87,88,89
```

##### 获取 store 中 所有商品的 id，拼接出一个用逗号分隔的字符串

```js
// 在 ShoppingCart.vue 中定义的methods

	getGoodsList(){
    var idArr = []
    
    // forEach(); 遍历数组的每一项， 获取到每项商品信息对象的id，push到 idArr 这个数组里。
    this.$store.state.cart.forEach( item => idArr.push(item.id))
    
    if (idArr.length <=0) return
    // 如果 idArr 是空的，就不需要执行后续从服务器请求数据的操作了。
    // 直接return，中止运行后续代码，否则会报错。
    
    // join(','); 用逗号分隔数组里全部的id
    this.$http.get('api/goods/getshopcarlist/' + idArr.join(','))
      .then( result => {
      if(result.body.status === 0) {
        
        this.goodslist = result.body.message  
        // 把请求到的数据保存到 当前组件的data中定义的空数组 goodslist 里
      }
    })
  },
```

P195

##### 服务器数据渲染到页面后，不包含商品数量 count，需要到 state.cart 中获取

1. 定义一个空对象

2. 遍历 cart 数组里的每个商品信息对象，获取每一项的 id 和 count值

3. **用获取到的 id 和 count 组成键值对，往现有的对象里 新增键值对  o[key] = value**  // 注意这个用法！

4. 返回保存了 id 和 数量 的对应关系的这个对象。

   **获取到的数据格式：{ 88: 1, 89: 3, 90: 4 }**

```js
getters: {
  getGoodsCount(state){
    var o = {}
    
    // 把 state.cart 数组里每个商品信息对象上的 id 和 count 取到，组成新的键值对，保存到 o 身上。
    state.cart.forEach(item => {
      o[item.id] = item.count
    })
    return o  // o 这个对象上保存了 id 和 数量 的对应关系 { item.id: item.count }
  }
}
```

##### 在 Shoppingcart.vue 中 使用 getters 获取的商品数量 count 值

属性绑定传值给 numbox 子组件

```html
<numbox :initcount="$store.getters.getGoodsCount[item.id]"  
        :goodsid="item.id"></numbox>
```

注意这里调用getters是直接写方法名，后面跟中括号[key]，来获取对应value。

而不是写方法里return的对象 o

```js
$store.getters.getGoodsCount[item.id]
```

##### 在 NumberBox.vue 子组件中 接收父组件的传值并使用

```html
props: ["initcount", "goodsid"],

<input id="test" class="mui-input-numbox" type="number" 
       :value="initcount"/> // 使用父组件的传值 initcount
```