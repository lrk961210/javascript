## 什么情况下浏览器会进行layout
一般情况下，浏览器的layout是lazy的，也就是说：在js脚本执行时，是不会去更新DOM的，
任何对DOM的修改都会被暂存在一个队列中，在当前js的执行上下文完成执行后，会根据这个队列中的修改，进行一次layout。

然而有时希望在js代码中立刻获取最新的DOM节点信息，浏览器就不得不提前执行layout，这是导致DOM性能问题的主因。

如下的操作会打破常规，并触发浏览器执行layout

- 通过js获取需要计算的DOM属性
- 添加或删除DOM元素
- resize浏览器窗口大小
- 改变字体
- css伪类的激活，比如:hover
- 通过js修改DOM元素样式且该样式涉及到尺寸的改变
参考链接：https://blog.csdn.net/qq_30100043/article/details/79571066
