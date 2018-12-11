## promise
```
// 传递resolve，函数里面要通过这个resolve来控制，如果不传入肯定调用不到了
let promise = new Promise(resolve => {
  //这一段代码会立即执行
  // 2s 后调用resolve
    setTimeout(() => {
        resolve("---promise timeout ---") // 核心
    }, 2000)
})

promise.then(value => console.log(value)) //等 resolve
```
#### 类比 angular中的Observable
```
let stream1$ = new Observable(observer => {
    let timeout = setTimeout(() => {
      observer.next('observable timeout')
    })
    
    return () => {
      clearTimeout(timeout)
    }
})
// 下面这个变量可以用来取消订阅
let disposable = stream1$.subscribe(value => console.log(value))
```

#### 不同之处
- angular中的Observable 可以取消订阅
- angular中的Observable 可以发射多个值 (如连续调用observer.next方法)
- angular中的Observable 提供了工具函数（如stream1$.filter(value => value % 2 == 0).subscribe()


代码： https://gitee.com/mumu-osc/NiceFish/tree/master
视频： https://www.youtube.com/watch?v=5Rj8_4ftZeE
