call 和 apply 都是为了改变某个函数运行时的上下文（context）而存在的，即，改变函数体内部 this 的指向。

#### 区别
接受参数的方式不太一样
func.call(this, arg1, arg2);
func.apply(this, [arg1, arg2])

bind： 和call差不多，但是它会将参数继续拼接下去

```
  function func(a, b, c) {
      console.log(a, b, c);
  }
  var func1 = func.bind(null,'linxin');

  func('A', 'B', 'C');            // A B C
  func1('A', 'B', 'C');           // linxin A B
  func1('B', 'C');                // linxin B C
  func.call(null, 'linxin');      // linxin undefined undefined

```

具体例子 ：https://www.cnblogs.com/coco1s/p/4833199.html
https://github.com/lin-xin/blog/issues/7
