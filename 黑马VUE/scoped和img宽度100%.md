![1554473884316](C:\Users\Zoe\AppData\Roaming\Typora\typora-user-images\1554473884316.png)

![1554473922241](C:\Users\Zoe\AppData\Roaming\Typora\typora-user-images\1554473922241.png)

图片不能自适应 width: 100%

解决办法：去除style标签里的  scoped 属性。 

由于根div有自己的类名，设置样式的时候都从这个类名往下嵌套，所以去除 scoped 并不会导致样式冲突污染。

```html
<style lang="scss">
.goodsdesc-container{
  h3{
    font-size: 16px;
    color: #226aff;
    text-align: center;
    margin: 15px 0;
  }
  .content{
    img{
      width: 100%;
    }
  }
}
</style>
```

