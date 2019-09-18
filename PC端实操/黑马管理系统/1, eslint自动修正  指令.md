自定义eslint语法修正指令

```json
// package.json

"scripts" :{
  "lintfix": "eslint --ext .js,.vue src --fix"
}
```



修改了配置文件，要重新 npm run dev

但如果一开始用了eslint，有语法错误时，npm run dev不会生效，所以需要先把语法错误修正。