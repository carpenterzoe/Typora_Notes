##### 在main.js中全局配置请求地址

```js
Vue.http.options.root = 'http://www.liulongbin.top:3005/'
```



全局配置了请求地址之后，this.$http.get( URL )

这里只需要写后面连着的部分即可，如：

```js
this.$http.get('api/getnew/' + this.id )
  .then(result => {
  if (result.body.code === 0) {
    // 成功回调
  }else {
    // 失败回调
  }
})
```



##### 全局设置 post 表单数据格式组织形式  application/x-www-form-urlencoded

```js
Vue.http.options.emulateJSON = true
```

配置之后，后续调用 this.$http.post 时， 此参数都可以直接省略，例如：

```js
this.$http.post('api/postcomment' + this.$route.params.id, { content: this.msg }, { emulateJSON: true } )    // 全局设置后，参数3 直接省略
// 参数1  请求的url地址
// 参数2  提交给服务器的数据对象  - 是对象
// 参数3  定义提交时 表单中的数据格式 是 { emulateJSON: true }  
```

