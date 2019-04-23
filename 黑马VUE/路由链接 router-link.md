##### 把a标签改成router-link

```html
<router-link to="/home/newslist">
  <img src="../../images/menu1.png" alt="">
  <div class="mui-media-body">新闻资讯</div>
</router-link>

// 旧的
<a href="#">
  <img src="../../images/menu1.png" alt="">
  <div class="mui-media-body">新闻资讯</div>
</a>

// 示例2  注意属性绑定的表达式用法
<router-link :to="'/home/newsinfo/' + item.id">
</router-link>

src="item.img"    src  普通属性，会被当成字符串解析
:src="item.img"  :src  用 v-bind 属性绑定，会被当成表达式解析
```

##### 创建组件模板 .vue文件

##### 在 router.js 中写入路由规则

```js
import NewsList from './components/news/NewsList.vue'

var router = new VueRouter({
  routes: [
    { path: '/home/newslist', component: NewsList } 
    												// 这里注意 component是单数
  ]
```

##### path参数匹配

```js
{ path: '/home/newsinfo/:id', component: NewsInfo }
// id不能直接写，要用:id表明这里是个参数
```

