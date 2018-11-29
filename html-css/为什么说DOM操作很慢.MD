## 什么情况下浏览器会进行layout
一般情况下，浏览器的layout是lazy的，也就是说：在js脚本执行时，是不会去更新DOM的，
任何对DOM的修改都会被暂存在一个队列中，在当前js的执行上下文完成执行后，会根据这个队列中的修改，进行一次layout。

参考链接：https://blog.csdn.net/qq_30100043/article/details/79571066
