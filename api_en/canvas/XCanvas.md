# 

- 更新时间:2026-10-22 10:55:46

> 画布对象（XCanvas），用来在一张图片上画画、填色、贴图、写字。
> 
> 先用 $canvas.create(宽, 高) 建一块空白画布，或 $canvas.create(图片路径) 打开一张已有图片，
> 然后用各种 draw 方法往上画东西。画完可以 toImg() 转成图片、show() 预览或 save() 存盘。
> 画笔用 $canvas.paint() 获得。



```javascript
var canvas = $canvas.create(320, 200);     //建一块 320x200 的空白画布
var paint = $canvas.paint("#FFFF0000");   //拿一支红色画笔
canvas.drawCircle(160, 100, 50, paint);   //画一个圆
canvas.save("/sdcard/Pictures/out.png");  //保存到本地
```




### getCanvas()

> 拿到底层 Android 原始 Canvas 对象。
> 
> 一般用不到，除非要调本类没封装的底层绘制功能。

- 返回 : {Canvas} 底层原始画布对象


```javascript
var canvas = $canvas.create(320, 200);
var raw = canvas.getCanvas();
log(raw);
```


### toImg()

> 把画布内容转换成图片对象（Image）。
> 
> 之后就能对这张图片做找图、保存、显示等操作。必须是用 create(宽,高) 或 create(图片) 建的画布才行。

- 返回 : {Image} 画好的图片对象


```javascript
var canvas = $canvas.create(320, 200);
var img = canvas.toImg();   //转成图片对象
img.show();
```


### show()

> 把当前画布里的内容直接弹窗预览显示出来。


```javascript
var canvas = $canvas.create(320, 200);
var paint = $canvas.paint("#FF0000");
canvas.drawCircle(160, 100, 50, paint);
canvas.show();   //弹窗看看画了啥
```


### save(path)

> 把画布内容保存成图片文件到本地。

- 参数 : path {string} 要保存到的完整路径（含文件名）


```javascript
var canvas = $canvas.create(320, 200);
var paint = $canvas.paint("#FF0000");
canvas.drawCircle(160, 100, 50, paint);
canvas.save("/sdcard/Pictures/out.png");
```


### isHardwareAccelerated()

> 判断这块画布是不是开了硬件加速。

- 返回 : {boolean} 开了硬件加速返回 true


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.isHardwareAccelerated());
```


### setBitmap(bitmap)

> 把画布的绘制目标换成另一张 Bitmap 图片。
> 
> 一般用 $canvas.create(图片) 直接建画布即可，很少手动调这个。

- 参数 : bitmap {Bitmap} 要作为绘制目标的 Bitmap


```javascript
var canvas = $canvas.create(320, 200);
//传入一张可变的 Bitmap 对象
```


### getBitmap()

> 拿到底层正在绘制的那张 Bitmap 图片。

- 返回 : {Bitmap} 底层 Bitmap 对象，空白画布可能为 null


```javascript
var canvas = $canvas.create(320, 200);
var bmp = canvas.getBitmap();
log(bmp);
```


### isOpaque()

> 判断画布是不是不透明的（没有透明背景）。

- 返回 : {boolean} 不透明返回 true


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.isOpaque());
```


### getWidth()

> 读取画布的宽度，单位像素。

- 返回 : {int} 画布宽度，单位像素


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getWidth());   //320
```


### getHeight()

> 读取画布的高度，单位像素。

- 返回 : {int} 画布高度，单位像素


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getHeight());   //200
```


### getDensity()

> 读取当前画布用的屏幕密度（dpi）。

- 返回 : {int} 密度 dpi


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getDensity());
```


### setDensity(density)

> 设置画布用的屏幕密度（dpi）。

- 参数 : density {int} 要设置的密度 dpi


```javascript
var canvas = $canvas.create(320, 200);
canvas.setDensity(320);
```


### getMaximumBitmapWidth()

> 读取这台设备允许创建的 Bitmap 最大宽度。

- 返回 : {int} 允许的最大 Bitmap 宽度


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getMaximumBitmapWidth());
```


### getMaximumBitmapHeight()

> 读取这台设备允许创建的 Bitmap 最大高度。

- 返回 : {int} 允许的最大 Bitmap 高度


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getMaximumBitmapHeight());
```


### save()

> 保存当前画布的状态（位置、旋转、裁剪等），之后可以 restore() 恢复。
> 
> 返回一个状态编号，常用来成对使用：先 save() 记一下，画完再 restoreToCount() 弹回去。

- 返回 : {int} 本次保存的状态编号


```javascript
var canvas = $canvas.create(320, 200);
var state = canvas.save();   //记下当前状态
canvas.rotate(45);          //后面的旋转不影响之前画的
canvas.restoreToCount(state);
```


### saveLayer(bounds, paint, saveFlags)

> 在一块指定矩形区域上开一个新图层单独绘制，画完再合成回来。

- 参数 : bounds {RectF} 图层区域，用 $canvas.rectf() 创建
- 参数 : paint {Paint} 画笔，用 $canvas.paint() 创建
- 参数 : saveFlags {int}   保存标志，一般传 0
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 100, 100);
var paint = $canvas.paint("#88FF0000");
canvas.saveLayer(rect, paint, 0);   //flags 一般传 0
//在图层里画东西
canvas.restore();
```


### saveLayer(bounds, paint)

> 在指定矩形区域上开一个新图层（用默认 flags）。
> 
> 是 saveLayer(区域, 画笔, flags) 的简写。

- 参数 : bounds {RectF} 图层区域
- 参数 : paint {Paint} 画笔
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 100, 100);
canvas.saveLayer(rect, $canvas.paint());
canvas.restore();
```


### saveLayer(left, top, right, bottom, paint)

> 用四个角坐标开一个新图层（用默认 flags）。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : paint {Paint} 画笔
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
canvas.saveLayer(0, 0, 100, 100, $canvas.paint());
canvas.restore();
```


### saveLayerAlpha(bounds, alpha, saveFlags)

> 开一个带透明度的新图层（0 全透明，255 不透明）。

- 参数 : bounds {RectF} 图层区域
- 参数 : alpha {int}   透明度 0~255
- 参数 : saveFlags {int}   保存标志，一般传 0
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 100, 100);
canvas.saveLayerAlpha(rect, 128, 0);   //半透明图层
canvas.restore();
```


### saveLayerAlpha(bounds, alpha)

> 开一个带透明度的新图层（用默认 flags）。

- 参数 : bounds {RectF} 图层区域
- 参数 : alpha {int}   透明度 0~255
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 100, 100);
canvas.saveLayerAlpha(rect, 128);
canvas.restore();
```


### saveLayerAlpha(left, top, right, bottom, alpha, saveFlags)

> 用四个角坐标开一个带透明度的新图层。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : alpha {int}   透明度 0~255
- 参数 : saveFlags {int}   保存标志，一般传 0
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
canvas.saveLayerAlpha(0, 0, 100, 100, 128, 0);
canvas.restore();
```


### saveLayerAlpha(left, top, right, bottom, alpha)

> 用四个角坐标开一个带透明度的新图层（用默认 flags）。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : alpha {int}   透明度 0~255
- 返回 : {int} 状态编号


```javascript
var canvas = $canvas.create(320, 200);
canvas.saveLayerAlpha(0, 0, 100, 100, 128);
canvas.restore();
```


### restore()

> 恢复到上一次 save() 保存的状态。


```javascript
var canvas = $canvas.create(320, 200);
canvas.save();
canvas.rotate(45);
canvas.restore();   //撤销刚才的旋转
```


### getSaveCount()

> 读取当前已经 save 了多少层状态。

- 返回 : {int} 当前保存的层数


```javascript
var canvas = $canvas.create(320, 200);
canvas.save();
log(canvas.getSaveCount());
```


### restoreToCount(saveCount)

> 一次性恢复到指定编号的 save 状态。

- 参数 : saveCount {int} 之前 save() 返回的状态编号


```javascript
var canvas = $canvas.create(320, 200);
var state = canvas.save();
canvas.rotate(45);
canvas.restoreToCount(state);   //直接回到 state 那一层
```


### translate(dx, dy)

> 把整个坐标系平移一段距离，之后画的东西都会按新原点偏移。

- 参数 : dx {float} 横向移动多少像素
- 参数 : dy {float} 纵向移动多少像素


```javascript
var canvas = $canvas.create(320, 200);
canvas.translate(50, 30);   //原点移到 (50,30)
canvas.drawCircle(0, 0, 20, $canvas.paint());   //画在 (50,30)
```


### scale(sx, sy)

> 把之后画的内容整体放大或缩小。
> 
> sx、sy 是横向、纵向的缩放倍数，1 表示原大小，2 表示放大一倍，0.5 表示缩小一半。

- 参数 : sx {float} 横向缩放倍数
- 参数 : sy {float} 纵向缩放倍数


```javascript
var canvas = $canvas.create(320, 200);
canvas.scale(2, 2);   //之后的内容放大一倍
canvas.drawCircle(50, 50, 20, $canvas.paint());
```


### scale(sx, sy, px, py)

> 围绕指定点把之后画的内容整体放大或缩小。
> 
> px、py 是缩放中心的坐标，不填则默认原点 (0,0)。

- 参数 : sx {float} 横向缩放倍数
- 参数 : sy {float} 纵向缩放倍数
- 参数 : px {float} 缩放中心 x
- 参数 : py {float} 缩放中心 y


```javascript
var canvas = $canvas.create(320, 200);
canvas.scale(2, 2, 160, 100);   //以 (160,100) 为中心放大一倍
```


### rotate(degrees)

> 把之后画的内容绕原点旋转指定角度。

- 参数 : degrees {float} 旋转角度（度）


```javascript
var canvas = $canvas.create(320, 200);
canvas.rotate(45);   //之后的内容顺时针转 45 度
```


### rotate(degrees, px, py)

> 围绕指定点把之后画的内容旋转指定角度。

- 参数 : degrees {float} 旋转角度（度）
- 参数 : px {float} 旋转中心 x
- 参数 : py {float} 旋转中心 y


```javascript
var canvas = $canvas.create(320, 200);
canvas.rotate(45, 160, 100);   //绕中心点转 45 度
```


### skew(sx, sy)

> 把之后画的内容倾斜（斜切）一定比例，做出“压扁变形”的效果。

- 参数 : sx {float} 横向倾斜比例
- 参数 : sy {float} 纵向倾斜比例


```javascript
var canvas = $canvas.create(320, 200);
canvas.skew(0.5, 0);   //横向倾斜
```


### concat(matrix)

> 把一个矩阵的变换叠加到当前画布变换上。

- 参数 : matrix {Matrix} 变换矩阵，用 $canvas.matrix() 创建


```javascript
var canvas = $canvas.create(320, 200);
var m = $canvas.matrix();
m.setScale(2, 2);
canvas.concat(m);   //叠加这个缩放矩阵
```


### setMatrix(matrix)

> 直接把画布变换替换成指定矩阵（覆盖之前的平移/旋转/缩放）。

- 参数 : matrix {Matrix} 变换矩阵


```javascript
var canvas = $canvas.create(320, 200);
var m = $canvas.matrix();
m.setScale(2, 2);
canvas.setMatrix(m);
```


### getMatrix(ctm)

> 把当前画布的变换矩阵读进给定的 Matrix 对象里。
> 
> 此方法已废弃，新代码建议用 getMatrix() 拿返回值。

- 参数 : ctm {Matrix} 用来接收结果的矩阵


```javascript
var canvas = $canvas.create(320, 200);
var m = $canvas.matrix();
canvas.getMatrix(m);
```


### getMatrix()

> 读取当前画布的变换矩阵。
> 
> 此方法已废弃，一般用不到。

- 返回 : {Matrix} 当前变换矩阵


```javascript
var canvas = $canvas.create(320, 200);
var m = canvas.getMatrix();
log(m);
```


### clipRect(rect, op)

> 把之后的绘制限制在一个浮点矩形区域内（配合区域操作模式）。
> 
> 区域外的内容不会被画出来。Region.Op 是高级裁剪模式，一般用下面那个不传 op 的简单版即可。

- 参数 : rect {RectF} 裁剪区域，用 $canvas.rectf() 创建
- 参数 : op {Region.Op} 区域组合模式，可传 null
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 100, 100);
canvas.clipRect(rect, null);
```


### clipRect(rect, op)

> 把之后的绘制限制在一个整数矩形区域内（配合区域操作模式）。

- 参数 : rect {Rect} 裁剪区域，用 $canvas.rect() 创建
- 参数 : op {Region.Op} 区域组合模式，可传 null
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rect(0, 0, 100, 100);
canvas.clipRect(rect, null);
```


### clipRect(rect)

> 把之后的绘制限制在一个浮点矩形区域内，区域外不画。

- 参数 : rect {RectF} 裁剪区域
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
canvas.clipRect($canvas.rectf(0, 0, 100, 100));
```


### clipRect(rect)

> 把之后的绘制限制在一个整数矩形区域内，区域外不画。

- 参数 : rect {Rect} 裁剪区域
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
canvas.clipRect($canvas.rect(0, 0, 100, 100));
```


### clipRect(left, top, right, bottom, op)

> 用四个角坐标把之后的绘制限制在矩形内（配合区域操作模式）。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : op {Region.Op} 区域组合模式，可传 null
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
canvas.clipRect(0, 0, 100, 100, null);
```


### clipRect(left, top, right, bottom)

> 用四个角坐标把之后的绘制限制在矩形内，区域外不画。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
canvas.clipRect(0, 0, 100, 100);
```


### clipRect(left, top, right, bottom)

> 用四个整数坐标把之后的绘制限制在矩形内。

- 参数 : left {int} 左边界
- 参数 : top {int} 上边界
- 参数 : right {int} 右边界
- 参数 : bottom {int} 下边界
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
canvas.clipRect(0, 0, 100, 100);
```


### clipPath(path, op)

> 把之后的绘制限制在一条 Path 路径围成的形状内（配合区域模式）。

- 参数 : path {Path} 路径对象
- 参数 : op {Region.Op} 区域组合模式，可传 null
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
//path 为一条用 android.graphics.Path 构造的路径对象
//canvas.clipPath(path, null);
```


### clipPath(path)

> 把之后的绘制限制在一条 Path 路径围成的形状内。

- 参数 : path {Path} 路径对象
- 返回 : {boolean} 裁剪成功返回 true


```javascript
var canvas = $canvas.create(320, 200);
//path 为一条用 android.graphics.Path 构造的路径对象
//canvas.clipPath(path);
```


### getDrawFilter()

> 读取当前画布用的绘制过滤器。一般用不到。

- 返回 : {DrawFilter} 当前绘制过滤器，可能为 null


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.getDrawFilter());
```


### setDrawFilter(filter)

> 设置一个绘制过滤器，对之后的绘制做统一处理。一般用不到。

- 参数 : filter {DrawFilter} 绘制过滤器对象


```javascript
var canvas = $canvas.create(320, 200);
//canvas.setDrawFilter(filter);
```


### quickReject(rect, type)

> 快速判断一个矩形是否完全在当前裁剪区域之外（可以用来跳过绘制、提速）。

- 参数 : rect {RectF} 要判断的矩形
- 参数 : type {Canvas.EdgeType} 边类型，可传 null
- 返回 : {boolean} 完全在裁剪区外返回 true


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(0, 0, 10, 10);
log(canvas.quickReject(rect, null));
```


### quickReject(path, type)

> 快速判断一条 Path 是否完全在当前裁剪区域之外。

- 参数 : path {Path} 要判断的路径
- 参数 : type {Canvas.EdgeType} 边类型，可传 null
- 返回 : {boolean} 完全在裁剪区外返回 true


```javascript
var canvas = $canvas.create(320, 200);
//path 为 Path 对象
//log(canvas.quickReject(path, null));
```


### quickReject(left, top, right, bottom, type)

> 快速判断一个由四角坐标确定的矩形是否完全在裁剪区域之外。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : type {Canvas.EdgeType} 边类型，可传 null
- 返回 : {boolean} 完全在裁剪区外返回 true


```javascript
var canvas = $canvas.create(320, 200);
log(canvas.quickReject(0, 0, 10, 10, null));
```


### getClipBounds(bounds)

> 把当前裁剪范围的边界矩形写进给定的 Rect 对象。

- 参数 : bounds {Rect} 用来接收结果的矩形，用 $canvas.rect() 创建
- 返回 : {boolean} 成功写回返回 true


```javascript
var canvas = $canvas.create(320, 200);
var r = $canvas.rect();
canvas.getClipBounds(r);
log(r);
```


### getClipBounds()

> 直接返回当前裁剪范围的边界矩形。

- 返回 : {Rect} 裁剪范围矩形


```javascript
var canvas = $canvas.create(320, 200);
var r = canvas.getClipBounds();
log(r);
```


### drawRGB(r, g, b)

> 用指定红绿蓝三色把整块画布填满（不透明）。

- 参数 : r {int} 红 0~255
- 参数 : g {int} 绿 0~255
- 参数 : b {int} 蓝 0~255


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRGB(255, 0, 0);   //整屏涂成红色
```


### drawARGB(a, r, g, b)

> 用指定透明度+红绿蓝把整块画布填满。

- 参数 : a {int} 透明度 0~255
- 参数 : r {int} 红 0~255
- 参数 : g {int} 绿 0~255
- 参数 : b {int} 蓝 0~255


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawARGB(128, 255, 0, 0);   //半透明红
```


### drawColor(color)

> 用一个颜色整数把整块画布填满。

- 参数 : color {int} ARGB 颜色整数


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawColor($颜色.白色);
```


### drawColor(color, mode)

> 用一个颜色整数按指定混合模式把整块画布填满。
> 
> mode 是 PorterDuff 混合模式，高级用法，一般用上面那个不带 mode 的即可。

- 参数 : color {int} ARGB 颜色整数
- 参数 : mode {PorterDuff.Mode} 混合模式


```javascript
var canvas = $canvas.create(320, 200);
//canvas.drawColor($颜色.半透明, null);
```


### drawPaint(paint)

> 用一支画笔把整块画布填满（画笔的颜色、纹理会铺满整个画布）。

- 参数 : paint {Paint} 画笔，用 $canvas.paint() 创建


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawPaint($canvas.paint("#FFCCCCCC"));
```


### drawPoints(pts, offset, count, paint)

> 在一组坐标上画多个点（可指定从第几个开始、画几个）。

- 参数 : pts {array} 坐标数组，两两一组 [x1,y1,x2,y2,...]
- 参数 : offset {int}   从第几个数开始画
- 参数 : count {int}   画几个数
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var pts = [10, 10, 50, 50, 100, 100];   //两两一组是一个点的 x,y
canvas.drawPoints(pts, 0, 6, $canvas.paint());
```


### drawPoints(pts, paint)

> 在一组坐标上画多个点。

- 参数 : pts {array} 坐标数组，两两一组 [x1,y1,x2,y2,...]
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var pts = [10, 10, 50, 50, 100, 100];
canvas.drawPoints(pts, $canvas.paint());
```


### drawPoint(x, y, paint)

> 在指定坐标画一个点。

- 参数 : x {float} 点的 x
- 参数 : y {float} 点的 y
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawPoint(160, 100, $canvas.paint("#FF0000"));
```


### drawLine(startX, startY, stopX, stopY, paint)

> 在两点之间画一条直线。

- 参数 : startX {float} 起点 x
- 参数 : startY {float} 起点 y
- 参数 : stopX {float} 终点 x
- 参数 : stopY {float} 终点 y
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawLine(0, 0, 320, 200, $canvas.paint("#FF0000"));
```


### drawLines(pts, offset, count, paint)

> 按一组坐标画多条线段（可指定从第几个开始、画几个）。
> 
> 坐标数组每 4 个数画一条线：x1,y1,x2,y2。

- 参数 : pts {array} 坐标数组
- 参数 : offset {int}   从第几个数开始
- 参数 : count {int}   画几个数
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var pts = [0, 0, 100, 100, 100, 0, 0, 100];
canvas.drawLines(pts, 0, 8, $canvas.paint());
```


### drawLines(pts, paint)

> 按一组坐标画多条线段。

- 参数 : pts {array} 坐标数组，每 4 个数一条线
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var pts = [0, 0, 100, 100, 100, 0, 0, 100];
canvas.drawLines(pts, $canvas.paint());
```


### drawRect(rect, paint)

> 画一个矩形（用浮点矩形对象）。

- 参数 : rect {RectF} 矩形区域，用 $canvas.rectf() 创建
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRect($canvas.rectf(10, 10, 100, 80), $canvas.paint("#FF0000"));
```


### drawRect(r, paint)

> 画一个矩形（用整数矩形对象）。

- 参数 : r {Rect} 矩形区域，用 $canvas.rect() 创建
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRect($canvas.rect(10, 10, 100, 80), $canvas.paint());
```


### drawRect(left, top, right, bottom, paint)

> 用四个角坐标画一个矩形。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRect(10, 10, 100, 80, $canvas.paint("#FF0000"));
```


### drawOval(oval, paint)

> 在一个矩形范围内画内切椭圆。

- 参数 : oval {RectF} 外接矩形，用 $canvas.rectf() 创建
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawOval($canvas.rectf(10, 10, 150, 100), $canvas.paint());
```


### drawOval(left, top, right, bottom, paint)

> 用四个角坐标画内切椭圆。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawOval(10, 10, 150, 100, $canvas.paint());
```


### drawCircle(cx, cy, radius, paint)

> 画一个圆。

- 参数 : cx {float} 圆心 x
- 参数 : cy {float} 圆心 y
- 参数 : radius {float} 半径
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawCircle(160, 100, 50, $canvas.paint("#FF0000"));
```


### drawArc(oval, startAngle, sweepAngle, useCenter, paint)

> 画一段圆弧（用外接矩形确定椭圆范围）。

- 参数 : oval {RectF} 外接矩形
- 参数 : startAngle {float} 起始角度（度，0 指向 3 点钟方向）
- 参数 : sweepAngle {float} 划过的角度（顺时针）
- 参数 : useCenter {boolean} 是否把圆心连进来（画扇形传 true，画弧线传 false）
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var rect = $canvas.rectf(10, 10, 150, 110);
canvas.drawArc(rect, 0, 180, true, $canvas.paint());
```


### drawArc(left, top, right, bottom, startAngle, sweepAngle, useCenter, paint)

> 用四个角坐标画一段圆弧。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : startAngle {float} 起始角度（度）
- 参数 : sweepAngle {float} 划过的角度（顺时针）
- 参数 : useCenter {boolean} 画扇形传 true，画弧线传 false
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawArc(10, 10, 150, 110, 0, 180, true, $canvas.paint());
```


### drawRoundRect(rect, rx, ry, paint)

> 画一个圆角矩形（用矩形对象）。

- 参数 : rect {RectF} 矩形范围
- 参数 : rx {float} 圆角横向半径
- 参数 : ry {float} 圆角纵向半径
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRoundRect($canvas.rectf(10, 10, 150, 100), 20, 20, $canvas.paint());
```


### drawRoundRect(left, top, right, bottom, rx, ry, paint)

> 用四个角坐标画一个圆角矩形。

- 参数 : left {float} 左边界
- 参数 : top {float} 上边界
- 参数 : right {float} 右边界
- 参数 : bottom {float} 下边界
- 参数 : rx {float} 圆角横向半径
- 参数 : ry {float} 圆角纵向半径
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawRoundRect(10, 10, 150, 100, 20, 20, $canvas.paint());
```


### drawPath(path, paint)

> 沿一条 Path 路径画线或填充。

- 参数 : path {Path} 路径对象
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
//path 为用 android.graphics.Path 构造的路径
//canvas.drawPath(path, $canvas.paint());
```


### drawBitmap(bitmap, left, top, paint)

> 在指定左上角位置贴一张 Bitmap 图片。
> 
> 普通脚本建议用 drawImage(图片或路径, left, top, paint) 更方便。

- 参数 : bitmap {Bitmap} 要贴的图片
- 参数 : left {float} 左上角 x
- 参数 : top {float} 左上角 y
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
//canvas.drawBitmap(bitmap, 10, 10, $canvas.paint());
```


### drawBitmap(bitmap, src, dst, paint)

> 把 Bitmap 的一部分按目标矩形贴上来（可缩放）。

- 参数 : bitmap {Bitmap} 原图
- 参数 : src {Rect} 从原图截取哪一块，null 表示整图
- 参数 : dst {RectF} 贴到画布的哪个位置/大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
//canvas.drawBitmap(bitmap, srcRect, dstRectF, $canvas.paint());
```


### drawBitmap(bitmap, src, dst, paint)

> 把 Bitmap 的一部分按目标矩形贴上来（目标也是整数矩形）。

- 参数 : bitmap {Bitmap} 原图
- 参数 : src {Rect} 从原图截取哪一块
- 参数 : dst {Rect} 贴到画布的哪个位置/大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
//canvas.drawBitmap(bitmap, srcRect, dstRect, $canvas.paint());
```


### drawBitmap(colors, offset, stride, x, y, width, height, hasAlpha, paint)

> 用一组颜色数组直接生成一张小图贴上来。
> 
> 此方法已废弃，一般用不到。

- 参数 : colors {array} 颜色数组
- 参数 : offset {int} 从第几个颜色开始
- 参数 : stride {int} 每行跨多少个
- 参数 : x {float} 贴的 x
- 参数 : y {float} 贴的 y
- 参数 : width {int} 宽
- 参数 : height {int} 高
- 参数 : hasAlpha {boolean} 是否有透明通道
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawBitmap(colors, offset, stride, x, y, w, h, true, paint);
```


### drawBitmap(colors, offset, stride, x, y, width, height, hasAlpha, paint)

> 用一组颜色数组直接生成一张小图贴上来（坐标为整数版）。
> 
> 此方法已废弃，一般用不到。

- 参数 : colors {array} 颜色数组
- 参数 : offset {int} 从第几个颜色开始
- 参数 : stride {int} 每行跨多少个
- 参数 : x {int} 贴的 x
- 参数 : y {int} 贴的 y
- 参数 : width {int} 宽
- 参数 : height {int} 高
- 参数 : hasAlpha {boolean} 是否有透明通道
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawBitmap(colors, offset, stride, x, y, w, h, true, paint);
```


### drawBitmap(bitmap, matrix, paint)

> 用一个矩阵做变换后再贴一张 Bitmap。

- 参数 : bitmap {Bitmap} 原图
- 参数 : matrix {Matrix} 变换矩阵
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var m = $canvas.matrix();
m.setScale(2, 2);
//canvas.drawBitmap(bitmap, m, $canvas.paint());
```


### drawBitmapMesh(bitmap, meshWidth, meshHeight, verts, vertOffset, colors, colorOffset, paint)

> 把 Bitmap 拉成网格并按顶点数组扭曲变形贴上来（做水波纹等特效用）。
> 
> 高级特效方法，参数较多，普通脚本一般用不到。

- 参数 : bitmap {Bitmap} 原图
- 参数 : meshWidth {int} 横向网格数
- 参数 : meshHeight {int} 纵向网格数
- 参数 : verts {array} 顶点坐标数组
- 参数 : vertOffset {int} 顶点数组起始偏移
- 参数 : colors {array} 顶点颜色数组，可传 null
- 参数 : colorOffset 颜色数组起始偏移
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawBitmapMesh(bitmap, meshW, meshH, verts, 0, colors, 0, paint);
```


### drawVertices(mode, vertexCount, verts, vertOffset, texs, texOffset, colors, colorOffset, indices, indexOffset, indexCount, paint)

> 用顶点数组绘制三维纹理（OpenGL 风格的高级绘制）。
> 
> 非常底层，普通脚本一般用不到。

- 参数 : mode {Canvas.VertexMode} 顶点模式
- 参数 : vertexCount {int} 顶点个数
- 参数 : verts {array} 顶点坐标
- 参数 : vertOffset {int} 顶点偏移
- 参数 : texs {array} 纹理坐标
- 参数 : texOffset {int} 纹理偏移
- 参数 : colors {array} 顶点颜色
- 参数 : colorOffset {int} 颜色偏移
- 参数 : indices {array} 索引
- 参数 : indexOffset {int} 索引偏移
- 参数 : indexCount {int} 索引个数
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawVertices(mode, count, verts, 0, texs, 0, colors, 0, indices, 0, count, paint);
```


### drawText(text, index, count, x, y, paint)

> 在指定位置画一段文字（文字为字符数组，可只画其中一段）。

- 参数 : text {array} 文字字符数组
- 参数 : index {int} 从第几个字符开始画
- 参数 : count {int} 画几个字符
- 参数 : x {float} 文字左下角 x
- 参数 : y {float} 文字基线 y
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
var chars = ["H", "e", "l", "l", "o"];
canvas.drawText(chars, 0, 5, 10, 50, $canvas.paint("#FF0000"));
```


### drawText(text, x, y, paint)

> 在指定位置画一段文字（最常用的写法）。

- 参数 : text {string} 要画的文字
- 参数 : x {float} 文字左下角 x
- 参数 : y {float} 文字基线 y
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawText("你好", 10, 50, $canvas.paint("#FF0000"));
```


### drawText(text, start, end, x, y, paint)

> 在指定位置画一段文字，只画其中从 start 到 end 的那一段。

- 参数 : text {string} 完整文字
- 参数 : start {int} 从第几个字开始
- 参数 : end {int} 画到第几个字（不含）
- 参数 : x {float} 文字左下角 x
- 参数 : y {float} 文字基线 y
- 参数 : paint {Paint} 画笔


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawText("你好世界", 1, 3, 10, 50, $canvas.paint());   //画“好世”
```


### drawTextRun(text, index, count, contextIndex, contextCount, x, y, isRtl, paint)

> 画一段带上下文的文字（处理复杂文字排版，如阿拉伯文连字）。一般用不到。

- 参数 : text {array} 字符数组
- 参数 : index {int} 起始下标
- 参数 : count {int} 字符个数
- 参数 : contextIndex 上下文起始下标
- 参数 : contextCount 上下文字符个数
- 参数 : x {float} x
- 参数 : y {float} 基线 y
- 参数 : isRtl {boolean} 是否从右到左
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawTextRun(chars, index, count, ctxIndex, ctxCount, x, y, false, paint);
```


### drawTextRun(text, start, end, contextStart, contextEnd, x, y, isRtl, paint)

> 画一段带上下文的文字（字符串版）。一般用不到。

- 参数 : text {string} 文字
- 参数 : start {int} 起始下标
- 参数 : end {int} 结束下标
- 参数 : contextStart 上下文起始
- 参数 : contextEnd {int} 上下文结束
- 参数 : x {float} x
- 参数 : y {float} 基线 y
- 参数 : isRtl {boolean} 是否从右到左
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawTextRun(text, start, end, ctxStart, ctxEnd, x, y, false, paint);
```


### drawPosText(text, index, count, pos, paint)

> 按一组坐标逐个位置摆放字符画出来。此方法已废弃。

- 参数 : text {array} 字符数组
- 参数 : index {int} 起始下标
- 参数 : count {int} 字符个数
- 参数 : pos {array} 每个字符的坐标
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawPosText(chars, index, count, pos, paint);
```


### drawPosText(text, pos, paint)

> 按一组坐标逐个位置摆放字符画出来。此方法已废弃。

- 参数 : text {string} 文字
- 参数 : pos {array} 每个字符的坐标
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawPosText(text, pos, paint);
```


### drawTextOnPath(text, index, count, path, hOffset, vOffset, paint)

> 让文字沿着一条 Path 路径排列画出来。

- 参数 : text {array} 字符数组
- 参数 : index {int} 起始下标
- 参数 : count {int} 字符个数
- 参数 : path {Path} 文字要沿其排列的路径
- 参数 : hOffset {float} 沿路径横向偏移
- 参数 : vOffset {float} 离路径垂直方向的偏移
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawTextOnPath(chars, index, count, path, 0, 0, paint);
```


### drawTextOnPath(text, path, hOffset, vOffset, paint)

> 让文字沿着一条 Path 路径排列画出来。

- 参数 : text {string} 文字
- 参数 : path {Path} 文字要沿其排列的路径
- 参数 : hOffset {float} 沿路径横向偏移
- 参数 : vOffset {float} 离路径垂直方向的偏移
- 参数 : paint {Paint} 画笔


```javascript
//canvas.drawTextOnPath("你好", path, 0, 0, paint);
```


### drawPicture(picture)

> 把一段录好的绘制记录（Picture）重放到当前画布上。一般用不到。

- 参数 : picture {Picture} 录制好的绘制记录


```javascript
//canvas.drawPicture(picture);
```


### drawPicture(picture, dst)

> 把一段绘制记录缩放到指定浮点矩形后重放。一般用不到。

- 参数 : picture {Picture} 绘制记录
- 参数 : dst {RectF} 目标矩形


```javascript
//canvas.drawPicture(picture, $canvas.rectf(0,0,100,100));
```


### drawPicture(picture, dst)

> 把一段绘制记录缩放到指定整数矩形后重放。一般用不到。

- 参数 : picture {Picture} 绘制记录
- 参数 : dst {Rect} 目标矩形


```javascript
//canvas.drawPicture(picture, $canvas.rect(0,0,100,100));
```


### drawImage(image, left, top, paint)

> 把一张图片对象按原大小贴到画布的指定位置。

- 参数 : image {Image} 要贴的图片对象，用 $img.read() 获得
- 参数 : left {float} 左上角 x
- 参数 : top {float} 左上角 y
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
canvas.drawImage(img, 10, 10, null);
```


### drawImage(image, left, top, width, height, paint)

> 把一张图片对象缩放到指定宽高后贴到画布上。

- 参数 : image {Image} 要贴的图片对象
- 参数 : left {float} 左上角 x
- 参数 : top {float} 左上角 y
- 参数 : width {float} 贴出来的宽度
- 参数 : height {float} 贴出来的高度
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
canvas.drawImage(img, 10, 10, 100, 50, null);   //缩放到 100x50
```


### drawImage(image, sx, sy, swidth, sheight, left, top, width, height, paint)

> 从图片里截取一块区域，缩放到画布上的指定位置和大小。

- 参数 : image {Image} 图片对象
- 参数 : sx {int} 从图片左上角 x 开始截
- 参数 : sy {int} 从图片左上角 y 开始截
- 参数 : swidth 截取多宽
- 参数 : sheight 截取多高
- 参数 : left {float} 贴到画布的 x
- 参数 : top {float} 贴到画布的 y
- 参数 : width {float} 贴出来的宽
- 参数 : height {float} 贴出来的高
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
//从图片 (0,0) 处截 50x50，贴到画布 (10,10) 并放大到 100x100
canvas.drawImage(img, 0, 0, 50, 50, 10, 10, 100, 100, null);
```


### drawImage(image, src, dst, paint)

> 把图片里 src 那块贴到画布的 dst 浮点矩形里。

- 参数 : image {Image} 图片对象
- 参数 : src {Rect} 从图片截取的区域，null 表示整图
- 参数 : dst {RectF} 贴到画布的位置和大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
canvas.drawImage(img, $canvas.rect(0, 0, 50, 50), $canvas.rectf(10, 10, 110, 110), null);
```


### drawImage(image, src, dst, paint)

> 把图片里 src 那块贴到画布的 dst 整数矩形里。

- 参数 : image {Image} 图片对象
- 参数 : src {Rect} 从图片截取的区域
- 参数 : dst {Rect} 贴到画布的位置和大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
canvas.drawImage(img, $canvas.rect(0, 0, 50, 50), $canvas.rect(10, 10, 110, 110), null);
```


### drawImage(image, matrix, paint)

> 用一个矩阵做变换后再把图片贴上来。

- 参数 : image {Image} 图片对象
- 参数 : matrix {Matrix} 变换矩阵
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var img = $img.read("/sdcard/Pictures/a.png");
var m = $canvas.matrix();
m.setScale(2, 2);
canvas.drawImage(img, m, null);
```


### drawImage(path, left, top, paint)

> 直接按图片路径把那张图按原大小贴到画布指定位置。

- 参数 : path {string} 图片文件路径
- 参数 : left {float} 左上角 x
- 参数 : top {float} 左上角 y
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawImage("/sdcard/Pictures/a.png", 10, 10, null);
```


### drawImage(path, left, top, width, height, paint)

> 直接按图片路径把图缩放到指定宽高后贴到画布上。

- 参数 : path {string} 图片文件路径
- 参数 : left {float} 左上角 x
- 参数 : top {float} 左上角 y
- 参数 : width {float} 贴出来的宽
- 参数 : height {float} 贴出来的高
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawImage("/sdcard/Pictures/a.png", 10, 10, 100, 50, null);
```


### drawImage(path, sx, sy, swidth, sheight, left, top, width, height, paint)

> 按图片路径，从图里截取一块缩放到画布指定位置和大小。

- 参数 : path {string} 图片文件路径
- 参数 : sx {int} 从图片 x 开始截
- 参数 : sy {int} 从图片 y 开始截
- 参数 : swidth {int} 截取多宽
- 参数 : sheight 截取多高
- 参数 : left {float} 贴到画布 x
- 参数 : top {float} 贴到画布 y
- 参数 : width {float} 贴出来的宽
- 参数 : height {float} 贴出来的高
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawImage("/sdcard/Pictures/a.png", 0, 0, 50, 50, 10, 10, 100, 100, null);
```


### drawImage(path, src, dst, paint)

> 按图片路径，把图里 src 那块贴到画布的 dst 浮点矩形里。

- 参数 : path {string} 图片文件路径
- 参数 : src {Rect} 从图片截取的区域，null 表示整图
- 参数 : dst {RectF} 贴到画布的位置和大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawImage("/sdcard/Pictures/a.png", $canvas.rect(0,0,50,50), $canvas.rectf(10,10,110,110), null);
```


### drawImage(path, src, dst, paint)

> 按图片路径，把图里 src 那块贴到画布的 dst 整数矩形里。

- 参数 : path {string} 图片文件路径
- 参数 : src {Rect} 从图片截取的区域
- 参数 : dst {Rect} 贴到画布的位置和大小
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
canvas.drawImage("/sdcard/Pictures/a.png", $canvas.rect(0,0,50,50), $canvas.rect(10,10,110,110), null);
```


### drawImage(path, matrix, paint)

> 按图片路径，用矩阵做变换后再把图贴上来。

- 参数 : path {string} 图片文件路径
- 参数 : matrix {Matrix} 变换矩阵
- 参数 : paint {Paint} 画笔，可传 null


```javascript
var canvas = $canvas.create(320, 200);
var m = $canvas.matrix();
m.setScale(2, 2);
canvas.drawImage("/sdcard/Pictures/a.png", m, null);
```


