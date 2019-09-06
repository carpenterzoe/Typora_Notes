1. 已完成的list，重新切换回未完成 有bug，是完成按钮 hover事件的bug

2.   function addItemToDOM(text, done){ }

   var oUl = (done) ? document.getElementById('doneID'):document.getElementById('todoID');

   调用 addItemToDOM(value, true);

   这里第二个参数如果不传，是不是就是 false ?

3. 删除按钮 hover样式没生效