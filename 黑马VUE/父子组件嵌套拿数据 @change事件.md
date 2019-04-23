按钮属于 goodsinfo ，数字属于 numberbox 组件。涉及到了父子组件嵌套，所以无法直接在 goodsinfo 页面中获取到商品的数量值。

怎么解决：涉及到了 子组件向父组件传值。（事件调用机制）

事件调用的本质：父向子传递方法，子调用这个方法，同时把数据当作参数，传递给这个方法。

##### 在父组件中

```js
data() {
  return {
    selectedCount: 1 // 保存用户选中的商品数量，默认选中1
  }
},
```

```js
getSelectedCount(count){
  this.selectedCount = count
  // 当子组件把选中的数量传递给父组件时，把选中的值保存到data上
}
```

##### 在父组件中，通过子组件的标签 进行事件绑定，传递方法

所以在子组件内部需要 this.$emit 触发的方法名称为 getcount

```html
<NumBox @getcount="getSelectedCount"  
    	:max="goodsinfo.stock_quantity"></NumBox>
```

##### @change 事件

每当文本框数据被修改的时候，会触发 @change事件，本例中会调用后面的 countChanged 函数。

```html
<input id="test" class="mui-input-numbox" type="number" value="1" 
    @change="countChanged" ref="numbox"/>
```



```js
methods: {
  // 每当文本框数据被修改的时候，@change事件会触发，这里则是会调用countChanged 函数。
  // 函数内部 立即把最新的数据 通过事件调用 传递给父组件
  countChanged(){
    this.$emit('getcount', parseInt(this.$refs.numbox.value)) // 触发父组件的方法，并传参
  }
},
  // this.$refs.numbox  拿到原生的 dom 对象
```

