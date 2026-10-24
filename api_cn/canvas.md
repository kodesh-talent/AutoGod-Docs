# $canvas - 画布

- 更新时间:2026-10-22 10:55:46

> 画布工具对象，脚本里叫 $canvas。
> 
> 它用来创建和绘图相关的"工具对象"：画布 XCanvas、画笔 Paint、矩形 Rect/RectF、变换矩阵 Matrix。
> 拿到这些对象后，就可以在图片上画画、写字、画框做标记，常用于截图后圈出识别到的位置等。
> 最常用的是 create 方法新建一块画布。



```javascript
var canvas = $canvas.create(320, 200); //新建一块宽 320、高 200 的空白画布
```




### paint()

> 获得一个画笔对象

- 返回 : {Paint} 一个新建的画笔对象，默认开启了抗锯齿（画出来边缘更平滑）
- 版本 : 1.3.1


```javascript
var result = $canvas.paint();
```


### paint(color)

> 获得一个画笔对象

- 参数 : color {int} 画笔颜色，用安卓的颜色整数表示（例如 android.graphics.Color.RED 的值）
- 返回 : {Paint} 一个新建的、已设置好指定颜色并开启抗锯齿的画笔对象
- 版本 : 1.3.1


```javascript
var result = $canvas.paint(1);
```


### paint(color)

> 获得一个画笔对象

- 参数 : color {String} 画笔颜色，用十六进制颜色字符串表示，例如 "#FF0000" 纯红、"#00FF00" 纯绿
- 返回 : {Paint} 一个新建的、已按字符串解析出颜色并开启抗锯齿的画笔对象；颜色字符串格式不对会报错
- 版本 : 1.3.1


```javascript
var result = $canvas.paint("sample");
```


### rect()

> 创建整数类型矩形

- 返回 : {Rect} 一个新建的、初始位置全为 0 的空白整数矩形对象


```javascript
var result = $canvas.rect();
```


### rect(left, top, right, bottom)

> 创建整数类型矩形

- 参数 : left {int} 矩形左边距离屏幕（图片）左边缘的像素
- 参数 : top {int} 矩形上边距离屏幕（图片）上边缘的像素
- 参数 : right {int} 矩形右边距离左边缘的像素（通常大于 left）
- 参数 : bottom {int} 矩形下边距离上边缘的像素（通常大于 top）
- 返回 : {Rect} 一个用这四个边界新建好的整数矩形对象


```javascript
var result = $canvas.rect(1, 1, 100, 1);
```


### rectf()

> 创建浮点类型矩形

- 返回 : {RectF} 一个新建的、初始位置全为 0 的空白浮点矩形对象（坐标可以带小数）


```javascript
var result = $canvas.rectf();
```


### rectf(left, top, right, bottom)

> 创建浮点类型矩形

- 参数 : left {float} 矩形左边距离左边缘的像素（可带小数）
- 参数 : top {float} 矩形上边距离上边缘的像素（可带小数）
- 参数 : right {float} 矩形右边距离左边缘的像素（通常大于 left）
- 参数 : bottom {float} 矩形下边距离上边缘的像素（通常大于 top）
- 返回 : {RectF} 一个用这四个浮点边界新建好的矩形对象


```javascript
var result = $canvas.rectf(1, 1, 100, 1);
```


### matrix()

> 获得一个矩阵对象

- 返回 : {Matrix} 一个新建的、单位矩阵（不做任何变换）的矩阵对象，可用于后续旋转、缩放、平移绘图


```javascript
var result = $canvas.matrix();
```


### matrix(src)

> 获得一个矩阵对象

- 参数 : src {Matrix} 作为模板的矩阵对象，新矩阵会复制它的变换状态；传 null 等同于得到一个单位矩阵
- 返回 : {Matrix} 一个根据传入矩阵复制出来的新矩阵对象


```javascript
var result = $canvas.matrix(null);
```


### create()

> 创建一个画布对象

- 返回 : {XCanvas} 一个新建的空白画布对象，之后可以在它上面绘图、写字
- 版本 : 1.3.1


```javascript
var result = $canvas.create();
```


### create(image)

> 创建一个画布对象

- 参数 : image {Image} 要在上面作画的图片对象（用 $img.read 或截屏得到），画布会以这张图为底图
- 返回 : {XCanvas} 一个绑定到该图片上的画布对象，之后画的内容会画在这张图上
- 版本 : 1.3.1


```javascript
var result = $canvas.create($img.read("/sdcard/Pictures/sample.png"));
```


### create(path)

> 创建一个画布对象

- 参数 : path {string} 图片文件的路径（例如 "/sdcard/Pictures/sample.png"），会先把它读成图片再作为画布底图
- 返回 : {XCanvas} 一个绑定到该图片上的画布对象；图片读取失败时返回 null
- 版本 : 1.3.1


```javascript
var result = $canvas.create("/sdcard/Pictures/sample.png");
```


### create(image)

> 创建一个画布对象

- 参数 : image {Bitmap} 一个安卓原生位图对象，画布会以它为底图（一般由内部或其他图片对象转换而来）
- 返回 : {XCanvas} 一个绑定到该位图上的画布对象
- 版本 : 1.3.1


```javascript
var result = $canvas.create(null);
```


### create(w, h)

> 创建一个画布对象

- 参数 : w {int} 新建画布的宽度（像素）
- 参数 : h {int} 新建画布的高度（像素）
- 返回 : {XCanvas} 一块按指定宽高新建出来的空白画布对象
- 版本 : 1.3.1


```javascript
var result = $canvas.create(100, 100);
```


