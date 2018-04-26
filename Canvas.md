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

> 绘制矩形 
> fillRect() 填充指定的颜色的矩形 填充的颜色通过 fillStyle 属性指定

```
//绘制红色矩形
context.fillStyle = "#ff0000";
context.fillRect(10, 10, 50, 50); 

```

> strokeRect()绘制指定的颜色描边的矩形。描边颜色通过 strokeStyle 属性指定

```
//绘制红色描边矩形
context.strokeStyle = "#ff0000";
context.strokeRect(10, 10, 50, 50);
 
```

- lineWidth 属性控制描边线条的宽度，该属性的值可以是任意整数。 
- lineCap 属性可以控制线条末端的形状是平头、圆头还是方头（"butt"、"round"或"square"）  
- lineJoin 属性可以控制线条相交的方式是圆交、斜交还是斜接（"round"、"bevel"或"miter"）。

> clearRect()方法用于清除画布上的矩形区域


> 绘制路径----以绘制时钟为例

```
var drawing = document.getElementById("drawing");
//确定浏览器支持<canvas>元素

if (drawing.getContext){
 var context = drawing.getContext("2d");
 
 //要绘制路径，首先必须调用 beginPath()方法
 context.beginPath();
 
 //绘制外圆(以（100,100）为圆心，99为半径，起始角度0，结束角度360，顺时针)
 context.arc(100, 100, 99, 0, 2 * Math.PI, false);

 //将绘图游标移动到(x,y)，不画线(缺少这一句会导致外圆到內圆有一条线)
 context.moveTo(194, 100);
 
 //绘制内圆(以（100,100）为圆心，94为半径，起始角度0，结束角度360，顺时针)
 context.arc(100, 100, 94, 0, 2 * Math.PI, false);
 
 //绘制分针
 context.moveTo(100, 100);
 context.lineTo(100, 15);//从上一点开始绘制一条直线，到(x,y)为止
 
 //绘制时针
 context.moveTo(100, 100);
 context.lineTo(35, 100);
 
 //描边路径
 context.stroke();
 
} 

```
