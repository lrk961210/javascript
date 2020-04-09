参考 https://juejin.im/post/5c984610e51d45656702a785

## 工厂模式
提供一个创建对象的接口/方法，让我们可以通过调用函数生成对象（不用使用new），即工厂批量生产对象
```
    // 某个需要创建的具体对象
    class Product {
        constructor (name) {
            this.name = name;
        }
        init () {}
    }
    // 工厂对象
    class Creator {
        create (name) {
            return new Product(name);
        }
    }
    const creator = new Creator();
    const p = creator.create(); // 通过工厂对象创建出来的具体对象

```

## 单例模式
保证一个类仅有一个实例，并提供一个访问它的全局访问点，一般登录、购物车等都是一个单例。
```
    // 单例对象
    class SingleObject {
        login () {}
    }
    // 访问方法
    SingleObject.getInstance = (function () {
        let instance;
        return function () {
            // 第一次才进行创建，闭包保证效果
            if (!instance) {
                instance = new SingleObject();
            }
            return instance;
        }
    })()
    const obj1 = SingleObject.getInstance();
    const obj2 = SingleObject.getInstance();
    console.log(obj1 === obj2); // true
    
```


## 适配器模式
用来解决两个接口不兼容问题，由一个对象来包装不兼容的对象，比如参数转换，允许直接访问
```
    class Adapter {
        specificRequest () {
            return '德国标准插头';
        }
    }
    // 适配器对象，对原来不兼容对象进行包装处理
    class Target {
        constructor () {
            this.adapter = new Adapter();
        }
        request () {
            const info = this.adapter.specificRequest();
            console.log(`${info} - 转换器 - 中国标准插头`)
        }
    }
    const target = new Target();
    console.log(target.request()); // 德国标准插头 - 转换器 - 中国标准插头


```

## 装饰器模式
在不改变对象自身的基础上，动态的给某个对象添加新的功能，同时又不改变其接口

```
    class Plane {
        fire () {
            console.log('发送普通子弹');
        }
    }
    // 装饰过的对象
    class Missile {
        constructor (plane) {
            this.plane = plane;
        }
        fire () {
            this.plane.fire();
            console.log('发射导弹');
        }
    }
    let plane = new Plane();
    plane = new Missile(plane);
    console.log(plane.fire()); // 依次打印 发送普通子弹 发射导弹

```
利用AOP(面向切面编程)给函数动态添加功能，即Function的after或者before

```
    Function.prototype.before = function (beforeFn) {
      const _self = this;
      return function () {
        beforeFn.apply(this, arguments);
        return _self.apply(this, arguments);
      }
    }

    Function.prototype.after = function (afterFn) {
      const _self = this;
      return function () {
        const ret = _self.apply(this, arguments);
        afterFn.apply(this, arguments);
        return ret;
      }
    }

    let func = function () {
      console.log('2');
    }

    func = func.before(function() {
      console.log('1');
    }).after(function() {
      console.log('3');
    })

    func();
    console.log(func()); // 依次打印 1 2 3

```

## 代理模式
为其他对象提供一种代理，便以控制对这个对象的访问，不能直接访问目标对象
```
    class Flower {}
    // 源对象
    class Jack {
        constructor (target) {
            this.target = target;
        }
        sendFlower (target) {
            const flower = new Flower();
            this.target.receiveFlower(flower)
        }
    }
    // 目标对象
    class Rose {
        receiveFlower (flower) {
            console.log('收到花: ' + flower)
        }
    }
    // 代理对象
    class ProxyObj {
        constructor () {
            this.target = new Rose();
        }
        receiveFlower (flower) {
            this.sendFlower(flower)
        }
        sendFlower (flower) {
            this.target.receiveFlower(flower)
        }
    }
    const proxyObj = new ProxyObj();
    const jack = new Jack(proxyObj);
    jack.sendFlower(proxyObj); // 收到花：[object Object]

```

## 策略模式
将算法和使用分离开
参考 https://blog.csdn.net/u011350550/article/details/84430880

```
    // 分离前
    function calBonus(grade, salary) {
      if (grade === 'S') {
        return salary*4;
      } else if (grade === 'A') {
        return salary*3;
      } else if (grade === 'B') {
        return salary*2;
      } else {
        return salary;
      }
    }
    
    // 分离后
    //计算绩效为S的年终
    function S(salary) {
      return salary * 4;
    }

    //策略使用
    function calBonus(fn, salary) {
      return  fn(salary);
    }

    //计算绩效为S，工资为20000的年终
    calBonus(S, 20000);
```

未完待续

