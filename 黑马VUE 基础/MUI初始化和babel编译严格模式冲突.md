多处出现的同一个问题。

解决方案：

在 babel.config.js 文件中配置ignore，让babel编译直接忽略要引入的 JS

```json
"ignore": [
  "./src/lib/mui/js/mui.min.js"
]
```



##### 滚动条左右可以滑动，但是控制台一直报错如下

[Intervention] Unable to preventDefault inside passive event listener due to target being treated as passive.

解决方案：

在PhotoList.vue （也就是需要应用滑动的页面中） CSS 样式部分设置

```css
*{
  touch-action: pan-y;
}
```

##### 刚点进页面滚动条不起作用，必须刷新页面

解决办法：

初始化mui，放到vue生命周期的 mounted( ) { } 函数里。 

created( ){ }，数据已经有了，还没渲染到页面中。

mounted( ){ }，组件中的DOM结构在页面中渲染好了。

滚动条是在页面渲染完成之后再控制滚动，所以初始化放在mounted里。

```js
import mui from '../../lib/mui/js/mui.min.js'

export default {
  mounted() {
    mui('.mui-scroll-wrapper').scroll({
      deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
    });
  },
}
```

