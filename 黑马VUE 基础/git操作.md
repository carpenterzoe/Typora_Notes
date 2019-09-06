把项目添加到本地 .git文件夹 的流程

git init   初始化本地仓储

git status   展示所有文件的状态，是否有文件需要commit

git add .    将文件的修改新建添加到暂存区

git commit -m "init my project"



和远程仓储关联

```
git remote add origin + 远程仓储地址
git push -u origin master
```



##### 初装 git 密钥配置

<https://www.bilibili.com/video/av24736323/?p=42>

安装git

桌面右键 git bash h-ere

```
ssh-keygen -t rsa -C carpenterzoe@outlook.com
```

连续回车直到如下提示

![1557111889241](C:\前端\Typora笔记\黑马VUE\assets\1557111889241.png)

找到生成的对应目录

![1557112018610](C:\前端\Typora笔记\黑马VUE\assets\1557112018610.png)

进入文件夹， git bash here

输入命令 cat id_rsa.pub

![1557112082420](C:\前端\Typora笔记\黑马VUE\assets\1557112082420.png)

把密钥复制到 github - setting - 左边栏 Personal setting - SSH and GPG keys - 右边 New SSH key

![1557112211907](C:\前端\Typora笔记\黑马VUE\assets\1557112211907.png)