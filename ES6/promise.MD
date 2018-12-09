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
// 类比 angular中的Observable
let stream1$ = new Observable(observer => {
    let timeout = setTimeout(() => {
      observer.next('observable timeout')
    })
    
    return () => {
      clearTimeout(timeout)
    }
})
let disposable = stream1$.subscribe(value => console.log(value))
