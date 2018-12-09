## promise
```
let promise = new Promise(resolve => {
  //这一段代码会立即执行
  // 2s 后调用resolve
    setTimeout(() => {
        resolve("---promise timeout ---")
    }, 2000)
})

promise.then(value => console.log(value)) //等 resolve
```
