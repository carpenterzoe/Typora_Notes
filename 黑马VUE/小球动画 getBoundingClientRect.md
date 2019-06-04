![1554511792716](C:\前端\Typora笔记\黑马VUE\assets\1554511792716.png)

bug描述：小球动画添加到购物车，只有特定的距离才能实现效果。一旦上下滚动界面，小球到一半就消失了，不能准确落到购物车徽标处。

原因：动画的 enter( ){ } 函数中，transform 位置一开始写死了。

解决方法：动态获取购物车徽标的 x, y 和 小球初始位置 x, y，利用动态差值实现 transform 位移。

##### 在App.vue中

给购物车的徽标直接加上id，方便获取位置x, y的信息。

在偶尔需要获取某个dom元素的信息，又不涉及双向数据绑定的时候，可以考虑操作dom

只要所有元素在一个界面，不是一个组件的，也可以通过dom id 直接获取。

```html
<span class="mui-badge" id="badge">0</span>
```

##### 在 GoodsInfo.vue 中

```js
enter(el, done){
  el.offsetWidth;

  const ballPostion = this.$refs.ball.getBoundingClientRect()
  // 这里就是通过 id 直接调用了 App.vue 组件里的元素。
  const badgePostion = document.getElementById('badge').getBoundingClientRect()
  
  const xDist = badgePostion.left - ballPostion.left
  const yDist = badgePostion.top - ballPostion.top

  el.style.transform = `translate(${xDist}px, ${yDist}px)`
  el.style.transition = "all 1s cubic-bezier(.4, -0.3, 1, .68)"
  done()
}
```

