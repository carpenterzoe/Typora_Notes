接口

```html
http://www.liulongbin.top:3005
```

涉及到获取数据的组件

|   组件名称   |                       接口                        |
| :----------: | :-----------------------------------------------: |
|     Home     |                   /api/getlunbo                   |
| Shoppingcart |            /api/goods/getshopcarlist/             |
|   Comment    | /api/getcomments/         POST  /api/postcomment/ |
|  PhotoInfo   |    /api/getimageInfo/     /api/getthumimages/     |
|  PhotoList   |     /api/getimgcategory       /api/getimages/     |
|   NewsInfo   |                   /api/getnew/                    |
|   NewsList   |                 /api/getnewslist                  |
|  GoodsDesc   |                /api/goods/getdesc/                |
|  GoodsInfo   |    /api/getthumimages/     /api/goods/getinfo/    |
|  GoodsList   |             /api/getgoods?pageindex=              |

装包

```js
cnpm i axios -S
```

main.js 引入

```
import axios from 'axios'
Vue.prototype.$ajax = axios
```

调用

注意 和vue-resource的区别

1. $http 变成 $ajax

2. result.body 变成 result.data

3.   .then( result => if { xxx } else { xxx })  

   变成  .then( result =>  if { xxx })    .catch  ( error => { } )

```js
methods: {
  getPhotoInfo() {
    this.$ajax.get('http://www.liulongbin.top:3005/api/getimageInfo/' + this.id )
      .then( result => {
      if(result.data.status === 0){
        this.photoinfo = result.data.message[0]
      }
    })
      .catch(error => {
      Toast('加载数据失败')
    })
  },
}
```

