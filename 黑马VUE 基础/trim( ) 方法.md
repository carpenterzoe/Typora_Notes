trim( ); 方法  -  作用：去除字符串两边的空白。

案例：判断评论内容是否为空。

```js
if (this.msg.trim().length === 0){
  return Toast('评论内容不能为空！')
  }
```

