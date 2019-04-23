##### 轮播图加载数据步骤

1. vue-resource   this.$http.get  获取数据
2. console.log 查看请求回来的数据结构以便后续调用
3. 把获取到的数据保存到 data 里
4. v-for 循环渲染到每个 item 

##### 在methods里定义请求数据的方法

```js
methods: {
   getSwipe(){
this.$http.get('http://www.liulongbin.top:3005/api/getlunbo').then(result => {
         if(result.body.status === 0) {
            this.swipeList = result.body.message; 
            // 请求回来的数据赋值给 data 的 this.swipeList 数组
         }else{
            Toast('加载轮播图失败') // Toast是mint-ui里的弹窗式样
            // 要使用，先在对应组件script中 import
         }
      })
   }
}
```

##### created() 生命周期函数中挂载方法

```js
export default {
  data(){
    return {
      swipeList: [] // 保存轮播图数据的数组
    }
  },
  created() {
    this.getSwipe()  // 在created() 阶段 挂载请求数据的方法
  }
```

##### v-for 渲染轮播图数据

```html
<mt-swipe-item v-for="item in swipeList" :key="item.img">
  // v-for 循环 data 数据来渲染轮播图
  // :key绑定值 只要是请求的数据中的唯一值，即每项都不重复就可以，不一定是ID
	<img :src="item.img" alt="">
  // 
</mt-swipe-item>
```

##### :src="item.img" / src="item.img"

```
src="item.img"    src  普通属性，会被当成字符串解析
:src="item.img"  :src  用 v-bind 属性绑定，会被当成表达式解析
```

