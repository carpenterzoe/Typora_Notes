

npm run build 打包报错

1. 外部引入的CSS，svg 单引号格式错误。改成双引号。

https://www.cnblogs.com/Richard-Tang/p/9968456.html



项目打包之后生成 github pages 不生效

2. 静态资源根路径的问题

   新建 vue.config.js，配置如下

```js
module.exports = {
  publicPath:"./",
  assetsDir: "./"
}
```

​	修改完配置之后记得 npm run build 重新打包！

3. 跨域请求服务器资源

   https://blog.csdn.net/li420520/article/details/85018786

   https://cli.vuejs.org/zh/config/#devserver-proxy

   https://yhf7.github.io/2018/11/10/2018-11-10/

vue.config.js 中 proxy配置

```js
devServer: {
  proxy: {
    '/api': {
      target: 'http://www.liulongbin.top:3005',
      changeOrigin: true,
      pathRewrite: {
      '^/api': '/api'
      }
    }
  }
}
```

