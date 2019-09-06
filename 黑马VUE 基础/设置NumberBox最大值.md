##### 在父组件 GoodsInfo.vue 中

```html
<NumBox @getcount="getSelectedCount"
       	:max="goodsinfo.stock_quantity"></NumBox>
```

:max="goodsinfo.stock_quantity"

属性绑定，从服务器获取到的库存数量，绑定到 max 这个属性上。

##### 在子组件 Numberbox.vue 中

props 定义一下从父组件传来的数据，才可以调用

```js
props: ["max"]
```

通过属性绑定 :data-numbox-max='max'  设置输入框的最大值。

```html
<div class="mui-numbox" data-numbox-min='1' :data-numbox-max='max'>
```

##### max值 传过来是 undefined，异步请求服务器数据引发的 bug

原因：:max="goodsinfo.stock_quantity" 。

goodsinfo.stock_quantity 是 父组件 从服务器获取的数据，执行的是异步函数。

```JS
created() {
  this.getGoodsInfo()
},
```

当父组件在内存中被创建，就会立即发送异步请求。这不耽误组件的继续渲染。

在请求数据还没拿到时，NumberBox子组件已经被渲染完毕，此时传过去的 max 就是 undefined。

```js
getGoodsInfo(){
  this.$http.get( 'api/goods/getinfo/' + this.id ).then( result => {
    if( result.body.status === 0 ){
      this.goodsinfo = result.body.message[0]
    }
  })
},
```

##### watch 监听 max的变化

watch：只要监听的数据发生变化，就会调用后面的function。

当max值发生变化，表示已经从服务器获请求到了数据。于是调用后面的function，为输入框设置最大值。

这里定义的function，调用了mui的API，用来更新指定选项。（API文档截图在末尾）

本例中是更新了原本框架中data-numbox-max的最大值（初始是9）。

```js
// 在 NumberBox.vue 子组件中
export default {
  mounted() {
    mui(".mui-numbox").numbox()
  },
  props: ["max"],
  
  // watch 监听，只要监听的数据发生变化，就会调用后面的function
  watch: {
    'max': function(newVal, oldVal){
      mui(".mui-numbox").numbox().setOption("max", newVal)
    }
  }
}
```

![1554863533383](C:\Users\Zoe\AppData\Roaming\Typora\typora-user-images\1554863533383.png)