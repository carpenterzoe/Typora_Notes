![1554434353271](C:\Users\Zoe\AppData\Roaming\Typora\typora-user-images\1554434353271.png)

##### margin 塌陷

小卡片的margin，引发盒子塌陷 造成的白色部分，overflow: hidden; 解决



这里是父子div嵌套造成的 margin 塌陷。

如图示

​         ![img](https://images2015.cnblogs.com/blog/979950/201609/979950-20160923182706012-1314391800.png)

　　　 当为子盒子添加margin-top：10px;时会发生如下情况：

​          ![img](https://images2015.cnblogs.com/blog/979950/201609/979950-20160923182706340-1945431455.png)

　　　 子盒子和父盒子之间并没出现期望的10px间隙而是父盒子与子盒子一起与页面顶端产生了10px间隙。



**解决方法：**

**（1）为父盒子设置border，为外层添加border后父子盒子就不是真正意义上的贴合。**

**（2）为父盒子添加overflow：hidden；**

**（3）为父盒子设定padding值。**

