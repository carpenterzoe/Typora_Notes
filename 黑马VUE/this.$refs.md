在vue中获取dom元素

##### 在元素标签中

```html
<div class="ball" v-show="ballFlag" ref="ball"></div>
```

##### 调用 this.$refs

```js
const ballPostion = this.$refs.ball.getBoundingClientRect();
```



