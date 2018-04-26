## Canvas绘图

> 使用<canvas>元素，必须设置width、height 

> 如果浏览器不支持<canvas>，会显示标签里面的内容

> 实现canvas

- 获取canvas元素
- 调用getContext()传入上下文名字（如：2D）

```
var drawing = document.getElementById("drawing");

if (drawing.getContext){  //检测getContext()方法是否存在
  var context = drawing.getContext("2d");
  // 其他操作
}

```

> 导出canvas上面的图像

```
//获取canvas上面的图像URI 传入图片MIME类型格式 没有参数默认为png
var imgURI = drawing.toDataURL("image/png");

//展示图片
var image = document.createElement("img");
image.src = imgURI;
document.body.appendChild(image);

```

