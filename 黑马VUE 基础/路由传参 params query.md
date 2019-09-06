##### 从服务器获取到的id写在 router-link

```html
<router-link :to="'/home/newsinfo/' +item.id ">
// 在路由链接中调用了从服务器获取到的 id

 to="/home/newsinfo/+item.id "  解析成普通字符串
:to="'/home/newsinfo/' +item.id "   解析成表达式，所以前面的普通字符串部分需要单引号再包裹起来。
```

#### query传参

##### 组件内部访问路由地址传过来的参数

```js
path: '/login?id=10'   // 请求路径 带参数

$this.route.query.id  // 通过这种方式在组件内部访问
```

##### $route对象

每个路由都有个$route路由对象。

可以获取name、path、query、params等。

#### params传参

##### :id占位符  path: '/login/:id' 

```js
path: '/login/:id'  
// :id表示此处为id占位符，将来传过来的数字要当成id解析。

path: '/login/10'
<router-link :to="'/login/' +item.id ">
// 比如这里，假设从服务器获取的值是 10，这里解析的路径就是 /login/10
// params 会把 /login/10 这样传入参数的路径 解析为 id=10
```

通过上面这种形式传过来的参数，params直接解析好了。

**调用方式： $route.params.id**

