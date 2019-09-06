##### 整个路由页面切换过渡

```html
<!-- 中间 路由 router-view 区域 -->
<transition>
  <router-view></router-view>
</transition>
```

##### 外部container overflow-x: hidden

作用是隐藏在右侧等待进入的动画，避免滚动条。

只能设置x方向的，否则上下滑动页面会有问题。

##### 根组件中设置样式

```css
.v-enter {
  opacity: 0;
  transform: translateX(100%);
}

// .v-enter .v-leave-to 拆分开写，避免动画进出往同一个方向，导致页面混乱

.v-leave-to {
  opacity: 0;
  transform: translateX(-100%);
  position: absolute;
}
// position:absolute 平滑过渡，让删除的元素脱离文档流，后面的元素才能同时平滑过渡过来。

.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease;
}
```

