安装

npm i mint-ui -S

在App.vue中，使用Mint-UI里需要用的组件

```vue
<template>
	<div>
      <mt-header fixed title="固定在顶部"></mt-header>
   </div>
</template>
```

在 main.js 中按需导入

```js
import { Header } from 'mint-ui'
Vue.component(Header.name, Header) 
// (组件名，组件模板)
// 这里注册的组件内容，就是上面按需导入的
```