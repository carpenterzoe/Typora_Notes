```html
<span slot="left" @click="goBack" v-show="flag">
  <mt-button icon="back">返回</mt-button>
</span>
```



```js
data(){
  return {
    flag: false
  }
},
  created() {
    this.flag = this.$route.path === '/home' ? false:true
  },
    methods: {
      goBack(){
        this.$router.go(-1)
      }
    },
      watch: {
        "$route.path": function(newVal) {
          if (newVal === '/home'){
            this.flag = false
          } else {
            this.flag = true
          }
        }
      }
```

