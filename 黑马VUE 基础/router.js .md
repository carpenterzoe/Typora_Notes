```js
import VueRouter from 'vue-router'
```

##### 导入对应的路由组件

```js
import Home from './components/tabbar/Home.vue'
import Member from './components/tabbar/Member.vue'
import Shopcart from './components/tabbar/Shopcart.vue'
import Search from './components/tabbar/Search.vue'
```

##### 创建路由对象

```javascript
var router = new VueRouter({
  routes: [
    { path: '/home', component: Home },
    { path: '/member', component: Member },
    { path: '/shopcart', component: Shopcart },
    { path: '/search', component: Search }
  ],
  linkActiveClass: 'mui-active'
})
```

##### 修改默认高亮的类名

```js
linkActiveClass: 'mui-active'
// 覆盖默认高亮的类名，默认的类 router-link-active
```

##### 把路由对象暴露出去

```js
export default router
```

##### 首页重定向

```js
{ path: '/', redirect: '/home' }
```

