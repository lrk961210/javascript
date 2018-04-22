## Ajax

### Ajax 技术的核心是 XMLHttpRequest 对象（简称 XHR）,其通信与数据格式无关
注意：只能向同一个域中使用相同端口和协议的 URL 发送请求

#### 只兼容IE7及以上

```
var xhr = new XMLHttpRequest();

//在open前指定onreadystatechange确保兼容性，每次readystate改变触发
xhr.onreadystatechange = function(){
    //已经接收到全部响应数据
    if (xhr.readyState == 4){
        //收到响应后，检查status，200为成功返回，304代表请求的资源没有被修改，可使用缓存
        //有的浏览器会错误地报告 204 状态代码。
        //IE 中 XHR 的 ActiveX 版本会将 204 设置为 1223，而 
        //IE 中原生的 XHR 则会将 204 规范化为 200。
        //Opera 会在取得 204 时报告 status 的值为 0。
        
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            alert(xhr.statusText);
            alert(xhr.responseText);
        } else {
            alert("Request was unsuccessful: " + xhr.status);
        }
    }
};

//open（）启动一个请求以备发送
//get/post URL 是否异步
xhr.open("get", "example.txt", ture);
        xhr.send(null);

        
```

#### 兼容IE7以下

```
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        return new XMLHttpRequest();
    } else if (typeof ActiveXObject != "undefined"){
        if (typeof arguments.callee.activeXString != "string"){
            var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                            "MSXML2.XMLHttp"],
                i, len;
    
            for (i=0,len=versions.length; i < len; i++){
                try {
                    new ActiveXObject(versions[i]);
                    arguments.callee.activeXString = versions[i];
                    break;
                } catch (ex){
                    //什么都不做直接跳过
                }
            }
        }
    
        return new ActiveXObject(arguments.callee.activeXString);
    } else {
        throw new Error("No XHR object available.");
    }
}

var xhr = createXHR();
...

```
