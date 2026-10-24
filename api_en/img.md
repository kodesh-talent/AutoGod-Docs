# $img - 图片操作

- 更新时间:2026-10-22 10:55:50

> 图片处理工具对象（脚本里的全局对象 $img）。
> 
> 它负责读图、保存、裁剪、缩放、旋转、拼接、模糊、找图找色等一切图片相关操作。
> 绝大多数方法都需要先用 $img.read(路径) 读出一个 Image 对象再传进去。



```javascript
//先读入一张图片，得到 Image 对象
var image = $img.read("/sdcard/Pictures/sample.png");
//显示出来看看
$img.show(image);
```




### read(imgPath)

> 从指定路径读入一张图片，得到一个 Image 对象。
> 
> 这是用得最多的入口：后续裁剪、缩放、找图找色都要先有 Image 对象。
> 路径支持相对项目目录的写法（以 / 开头）和绝对路径。

- 参数 : imgPath {string} 图片路径（相对项目目录或绝对路径）
- 返回 : {Image} 读取成功返回 Image 对象；路径不存在或失败返回 null


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片，得到 Image 对象
var img = $img.read(path);
//读出来可能为空，要判断一下
if (img != null) {
    log("读图成功，宽：" + img.width() + " 高：" + img.height());
}
```


### open(imgPath)

> 打开（读入）一张图片，和 read 完全一样，只是另一个名字。

- 参数 : imgPath {string} 图片路径
- 返回 : {Image} 成功返回 Image 对象；失败返回 null
- 版本 : 1.2.4


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
var img = $img.open(path);
```


### open(bitmap)

> 把一个安卓 Bitmap 对象包装成 Image 对象。
> 
> 当你从 UI 控件或截屏拿到的是 Bitmap 时，用它包一层，才能用 $img 的各种处理方法。

- 参数 : bitmap {Bitmap} 安卓位图对象
- 返回 : {Image} 包装好的 Image 对象
- 版本 : 1.2.4


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var mImg = ui.id("mImg");
//获取图片(安卓图片对象)
var bitmap = mImg.getImg();
//包装成 Image 对象
var img = $img.open(bitmap);
```


### read(imgFile)

> 从一个 Java File 对象读入图片。
> 
> 和 read(路径) 一样，只是入参换成了文件对象。

- 参数 : imgFile {File} 文件对象
- 返回 : {Image} 成功返回 Image 对象；失败返回 null


```javascript
var file = new java.io.File("/sdcard/Pictures/sample.png");
var image = $img.read(file);
if (image != null) $img.show(image);
```


### save(image, path, format, quality)

> 把 Image 对象保存成图片文件到磁盘。

- 参数 : image {Image} 要保存的 Image 对象
- 参数 : path {string} 保存路径（含文件名）
- 参数 : format {string} 图片格式，如 "png"、"jpg"
- 参数 : quality {int} 保存质量，1 到 100，越大越清晰文件也越大


```javascript
//截屏并且保存到本地
$screen.getPermit();
var screenImg = $screen.getScreen();
//保存为 png，质量 100
$img.save(screenImg, "/sdcard/s05.png", "png", 100);
```


### save(image, path)

> 把 Image 保存成 png 图片（默认质量 100）。

- 参数 : image {Image} 要保存的 Image 对象
- 参数 : path {string} 保存路径（含文件名）


```javascript
//截屏并且保存到本地
$screen.getPermit();
var screenImg = $screen.getScreen();
$img.save(screenImg, "/sdcard/s05.png");
```


### toBase64(image, format, quality)

> 把图片按指定格式和质量转成 Base64 字符串。

- 参数 : image {Image} 要转换的 Image 对象
- 参数 : format {string} 图片格式，如 "png"、"jpg"
- 参数 : quality {int} 压缩质量 1 到 100
- 返回 : {string} 图片的 Base64 字符串；失败返回 null


```javascript
var img = $img.read("/$img/res/t01.png");
var baseStr = $img.toBase64( img ,"png" , 50);
alert("图片Base64",baseStr);
```


### toBase64(image)

> 把图片转成 Base64 字符串（默认 png、质量 100）。

- 参数 : image {Image} 要转换的 Image 对象
- 返回 : {string} Base64 字符串；失败返回 null


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
var img = $img.read(path);
//转成 base64
var imgBase64 = $img.toBase64(img);
log(imgBase64);
```


### toBase64(path)

> 直接按路径读图并转成 Base64（内部读完会自动回收图片）。

- 参数 : path {string} 图片路径
- 返回 : {string} Base64 字符串；失败返回 null


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p01.png";
//直接转 base64
var imgBase64 = $img.toBase64(path);
log(imgBase64);
```


### readBase64(base64)

> 把一段 Base64 字符串还原成 Image 对象。
> 
> 和 toBase64 相反。支持带 "data:image/...;base64," 前缀的数据。

- 参数 : base64 {string} Base64 字符串
- 返回 : {Image} 还原成功返回 Image 对象；失败返回 null


```javascript
//先把图片转成 base64
var img = $img.read("/$img/res/t01.png");
var baseStr = $img.toBase64(img, "png", 50);
//再从 base64 还原成图片
var img2 = $img.readBase64(baseStr);
$img.show(img2);
```


### clip(image, x, y, w, h)

> 裁剪图片：从原图切出一块矩形小图，返回新图片。

- 参数 : image {Image} 要裁剪的原图片
- 参数 : x {int} 裁剪区域左上角 x（像素）
- 参数 : y {int} 裁剪区域左上角 y（像素）
- 参数 : w {int} 裁剪宽度
- 参数 : h {int} 裁剪高度
- 返回 : {Image} 裁剪后的新图片；越界则返回原图


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p03.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.clip(img, 0, 0, 300, 200);
//显示图片
$img.show(image);
```


### resize(image, w, h, interpolation)

> 把图片缩放到指定宽高。
> 
> 插值方式（不区分大小写，可传 "INTER_NEAREST"、"INTER_LINEAR"、"INTER_CUBIC"、
> "INTER_AREA"、"INTER_LANCZOS4"、"INTER_LINEAR_EXACT"），传 null 用默认。

- 参数 : image {Image} 要缩放的原图片
- 参数 : w {int} 目标宽度
- 参数 : h {int} 目标高度
- 参数 : interpolation {string} 插值方式，传 null 用默认
- 返回 : {Image} 缩放后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//缩放到 200x200
var image = $img.resize(img, 200, 200, "INTER_CUBIC");
//显示图片
$img.show(image);
```


### resize(image, w, h)

> 把图片缩放到指定宽高（用默认插值方式）。

- 参数 : image {Image} 要缩放的原图片
- 参数 : w {int} 目标宽度
- 参数 : h {int} 目标高度
- 返回 : {Image} 缩放后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.resize(img, 200, 200);
$img.show(image);
```


### scale(image, scaleX, scaleY, interpolation)

> 按比例（倍数）缩放图片。
> 
> scaleX、scaleY 是相对于原图宽高的倍数：0.5 表示缩小一半，2 表示放大两倍。

- 参数 : image {Image} 原图片
- 参数 : scaleX {double} 宽度缩放倍数
- 参数 : scaleY {double} 高度缩放倍数
- 参数 : interpolation {string} 插值方式
- 返回 : {Image} 缩放后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
//宽缩到0.3倍、高缩到0.2倍
var image = $img.scale(img, 0.3, 0.2, "CUBIC");
$img.show(image);
```


### scale(image, scaleX, scaleY)

> 按倍数缩放图片（用默认插值方式）。

- 参数 : image {Image} 原图片
- 参数 : scaleX {double} 宽度倍数
- 参数 : scaleY {double} 高度倍数
- 返回 : {Image} 缩放后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.scale(img, 0.3, 0.2);
$img.show(image);
```


### rotate(image, degree, x, y)

> 旋转图片：围绕指定中心点按角度旋转，返回新图片。

- 参数 : image {Image} 要旋转的图片
- 参数 : degree {float} 旋转角度（度）
- 参数 : x {int} 旋转中心 x，传 null 用图片中心
- 参数 : y {int} 旋转中心 y，传 null 用图片中心
- 返回 : {Image} 旋转后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.rotate(img, 45, 100, 200);
//显示图片
$img.show(image);
```


### rotate(image, degree)

> 以图片中心为轴旋转指定角度。

- 参数 : image {Image} 要旋转的图片
- 参数 : degree {float} 旋转角度（度）
- 返回 : {Image} 旋转后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.rotate(img, 45);
$img.show(image);
```


### rotate(image)

> 把图片默认旋转 90 度。

- 参数 : image {Image} 要旋转的图片
- 返回 : {Image} 旋转后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.rotate(img); //默认旋转90度
$img.show(image);
```


### concat(img1, img2, dir)

> 把两张图片拼接成一张。
> 
> dir 控制拼接方向："left"/"right" 左右拼，"top"/"bottom" 上下拼。

- 参数 : img1 {Image} 第一张图
- 参数 : img2 {Image} 第二张图
- 参数 : dir {string} 方向："left"/"right"/"top"/"bottom"
- 返回 : {Image} 拼接后的新图片；失败返回 null


```javascript
var t1 = $img.read("/$img/res/t02.png");
var t2 = $img.read("/$img/res/t03.png");
//两张图尺寸调成一致
t1 = $img.resize(t1, 300, 200);
t2 = $img.resize(t2, 300, 200);
//上下拼接
var img = $img.concat(t1, t2, "bottom");
$img.show(img);
```


### gray(image)

> 转换为灰度图

- 参数 : image {Image} 要处理的图片
- 返回 : {Image} 灰度化后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.gray(img);
//显示图片
$img.show(image);
```


### threshold(image, thre)

> 把图片二值化：比阈值亮的变白、暗的变黑。

- 参数 : image {Image} 要处理的图片
- 参数 : thre {double} 阈值（0 到 255）
- 返回 : {Image} 二值化后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.threshold(img, 150);
$img.show(image);
```


### adaptiveThreshold(image, maxValue, adaptiveMethod, thresholdType, blockSize, C)

> 自适应二值化：按每个像素周围邻域算阈值，把图转成纯黑白，适合光照不均的图。

- 参数 : image {Image} 要处理的图片
- 参数 : maxValue {number} 最大值（通常 255）
- 参数 : adaptiveMethod {string} 自适应算法，如 "MEAN_C"、"GAUSSIAN_C"
- 参数 : thresholdType {string} 阈值化类型，如 "BINARY"
- 参数 : blockSize {number} 邻域块大小（奇数）
- 参数 : C {number} 偏移调整量
- 返回 : {Image} 处理后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.adaptiveThreshold(img,255,"MEAN_C","BINARY", 11, 2);
//显示图片
$img.show(image);
```


### cvtColor(img, code, dstCn)

> 转换颜色空间

- 参数 : img {Image} 要转换的图片
- 参数 : code {string} 转换类型，如 "RGBA2BGR"
- 参数 : dstCn {int} 目标颜色通道数，传 -1 表示和原图一致
- 返回 : {Image} 转换后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.cvtColor(img,"RGBA2BGR",null);
//显示图片
$img.show(image);
```


### cvtColor(img, code)

> 转换颜色空间

- 参数 : img {Image} 要转换的图片
- 参数 : code {string} 转换类型，如 "RGBA2BGR"
- 返回 : {Image} 转换后的新图片


```javascript
//图片路径
var path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
var img = $img.read(path);
//操作图片
var image = $img.cvtColor(img,"RGBA2BGR");
//显示图片
$img.show(image);
```


### inRange(img, lowerBound, upperBound)

> 按颜色区间做二值化：落在区间内的像素变白，其余变黑。
> 
> 常用于把某一种颜色抠出来。颜色用 "#RRGGBB" 字符串表示。

- 参数 : img {Image} 要处理的图片
- 参数 : lowerBound {string} 颜色下界，如 "#666666"
- 参数 : upperBound {string} 颜色上界，如 "#FFFFFF"
- 返回 : {Image} 处理后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.inRange(img, "#666666", "#FFFFFF");
$img.show(image);
```


### blur(img, size, point, type)

> 对图片做模糊（滤波）处理。
> 
> 边框类型（不区分大小写）："DEFAULT"、"REPLICATE"、"REFLECT"、"WRAP"、"CONSTANT"。

- 参数 : img {Image} 要模糊的图片
- 参数 : size {double[]} 滤波器大小，如 [10,10]
- 参数 : point {double[]} 锚点，传 [-1,-1] 表示中心
- 参数 : type {string} 边框类型
- 返回 : {Image} 模糊后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.blur(img, [10, 10], [-1, -1], "REPLICATE");
$img.show(image);
```


### medianBlur(img, size)

> 中值滤波，对去除椒盐噪点特别有效。

- 参数 : img {Image} 要处理的图片
- 参数 : size {int} 滤波器大小（奇数）
- 返回 : {Image} 处理后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.medianBlur(img, 3);
$img.show(image);
```


### gaussianBlur(img, size, sigmaX, sigmaY, type)

> 高斯模糊，效果比普通 blur 更柔和自然。
> 
> 边框类型（不区分大小写）：DEFAULT、REPLICATE、REFLECT、WRAP、CONSTANT。

- 参数 : img {Image} 要模糊的图片
- 参数 : size {double[]} 滤波器大小，如 [15,15]
- 参数 : sigmaX {double} x 方向方差，传 0 自动算
- 参数 : sigmaY {double} y 方向方差，传 0 自动算
- 参数 : type {string} 边框类型
- 返回 : {Image} 模糊后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.gaussianBlur(img, [15, 15], 0, 0, "WRAP");
$img.show(image);
```


### flip(image)

> 把图片左右镜像翻转（水平翻转）。

- 参数 : image {Image} 要翻转的图片
- 返回 : {Image} 翻转后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.flip(img);
$img.show(image);
```


### upside(image)

> 把图片上下镜像翻转。

- 参数 : image {Image} 要翻转的图片
- 返回 : {Image} 翻转后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
var image = $img.upside(img);
$img.show(image);
```


### flip(image, sx, sy)

> 按横向、纵向缩放系数翻转图片。
> 
> sx/sy 取 -1 表示该方向镜像，取 1 表示不变；也可取其他数值做拉伸。

- 参数 : image {Image} 要翻转的图片
- 参数 : sx {float} 横向系数，-1 水平镜像
- 参数 : sy {float} 纵向系数，-1 垂直镜像
- 返回 : {Image} 翻转后的新图片


```javascript
var path = "sdcard/Pictures/示例/$img/res/p02.png";
var img = $img.read(path);
//sx=-1,sy=-1 等于水平垂直都翻转
var image = $img.flip(img, -1, -1);
$img.show(image);
```


### putTop(bigImg, smallImg, x, y)

> 大图找小图：在大图里按相似度匹配小图，找到后返回小图左上角坐标。

- 参数 : bigImg {Image} 大背景图
- 参数 : smallImg {Image} 要贴上去的小图
- 参数 : x {int} 小图贴在大图上的左上角 x
- 参数 : y {int} 小图贴在大图上的左上角 y
- 返回 : {Image} 合成后的新图片


```javascript
//图片路径
var path1 = "sdcard/Pictures/示例/$img/res/p02.png"; //大图片
var path2 = "sdcard/Pictures/示例/$img/res/p04.png"; //小图片
var bigImg = $img.read(path1);
var smallImg = $img.read(path2);
//设置放置的位置
var image = $img.putTop(bigImg, smallImg, 20, 20);
//显示图片
$img.show(image);
```


### findColor(image, color, threshold, x, y, w, h)

> 在图片的指定区域内找指定颜色，返回第一个命中的点。

- 参数 : image {Image} 要查找的图片
- 参数 : color {string} 要找的颜色，如 "#d80005"
- 参数 : threshold {int} 颜色容差，0 最严格
- 参数 : x {int} 搜索区域左上角 x
- 参数 : y {int} 搜索区域左上角 y
- 参数 : w {int} 搜索区域宽
- 参数 : h {int} 搜索区域高
- 返回 : {Point} 找到返回点对象；没找到返回 null


```javascript
var img = $img.read("/$img/res/t01.png");
//在 (0,0,100,100) 区域内找红色，容差 5
var point = $img.findColor(img, "#d80005", 5, 0, 0, 100, 100);
if (point != null) {
    log("找到位置：" + point.x + "," + point.y);
}
```


### findColor(image, color, threshold, region)

> 找色：在指定矩形区域内找第一个接近目标颜色的点，返回该点坐标。

- 参数 : image {Image} 要查找的图片
- 参数 : color {string} 要找的颜色
- 参数 : threshold {int} 颜色容差
- 参数 : region {int[]} 搜索区域 [x,y,w,h]
- 返回 : {Point} 找到返回点；否则 null


```javascript
var img = $img.read("/$img/res/t01.png");
var point = $img.findColor(img,"#d80005",5,[0,0,100,100]);
alert("结果",point);
```


### findColor(image, color, threshold)

> 找色：在整张图里找第一个接近目标颜色的点（带颜色容差），返回坐标。

- 参数 : image {Image} 要查找的图片
- 参数 : color {string} 要找的颜色
- 参数 : threshold {int} 颜色容差
- 返回 : {Point} 找到返回点；否则 null


```javascript
var img = $img.read("/$img/res/t01.png");
var point = $img.findColor(img,"#d80005",5);
alert("结果",point);
```


### findColor(image, color)

> 找色：在整张图里找第一个目标颜色的点（用默认容差），返回坐标。

- 参数 : image {Image} 要查找的图片
- 参数 : color {string} 要找的颜色
- 返回 : {Point} 找到返回点；否则 null


```javascript
var img = $img.read("/$img/res/t01.png");
var point = $img.findColor(img,"#d80005");
alert("结果",point);
```


### findMultiColors(image, region, color, threshold, colors)

> 多点找色：先找一个起点色，再按一组相对偏移和配套颜色共同定位，比单点更准。

- 参数 : image {Image} 要查找的图片
- 参数 : region {Number[]} 搜索区域 [x,y,w,h]
- 参数 : color {string} 起始基准点颜色
- 参数 : threshold {Number} 颜色容差
- 参数 : colors {Object[]} 相对点色数据：[dx,dy,"#颜色",容差, ...]
- 返回 : {Point} 找到返回基准点位置；否则 null


```javascript
var img = $img.read("/$img/res/t01.png");
var point = $img.findMultiColors(img,[0],"#e70216",5,[
	-54, -13, "#db0306", 5,
	-121, -13, "#dc0407", 5,
	-155, -18, "#d80306", 5,
	-132, -85, "#da0306", 5,
	-78, -63, "#dd0206", 5,
	-49, -100, "#db0306", 5,
	6, -77, "#db0306", 5,
	3, -42, "#db0306", 5,
	-103, -52, "#dc0406", 5,
]);
alert("结果",point);
```


### findImg(bigImg, minImg, options)

> 在大图里找小图，可通过 options 对象设置相似度、搜索区域等。

- 参数 : bigImg {Image} 大图（被搜索的底图）
- 参数 : minImg {Image} 小图（要找的图标）
- 参数 : options {object} 查找参数，如 { similar: 0.8, region: [x,y,w,h] }
- 返回 : {Point} 找到返回左上角点；否则 null


```javascript
var img1 = $img.read("/$img/res/t04.png");
var img2 = $img.read("/$img/res/t05.png");
var point = $img.findImg(img1, img2, {
    similar: 0.8,        //相似度 0~1
    region: [0,0,500,500] //只在这个区域找
});
if (point != null) {
    log("找到：" + point.x + "," + point.y);
}
```


### findImg(bigImg, minImg)

> 在大图里找小图，用默认相似度（全图搜索）。

- 参数 : bigImg {Image} 大图
- 参数 : minImg {Image} 小图
- 返回 : {Point} 找到返回左上角点；否则 null


```javascript
var img1 = $img.read("/$img/res/t05.png");
var img2 = $img.read("/$img/res/t04.png");
var point = $img.findImg(img1, img2);
if (point != null) log("找到：" + point.x + "," + point.y);
```


### findImgAll(bigImg, minImg, options)

> 在大图里找出所有小图出现的位置。

- 参数 : bigImg {Image} 大图
- 参数 : minImg {Image} 小图
- 参数 : options {object} 查找参数
- 返回 : {Point[]} 所有命中位置的数组，可能为空


```javascript
var img1 = $img.read("/$img/res/t06.png");
var img2 = $img.read("/$img/res/t07.png");
var points = $img.findImgAll(img1, img2, { similar: 0.8 });
for (var i = 0; i < points.length; i++) {
    log("第" + i + "个：" + points[i].x + "," + points[i].y);
}
```


### findImgAll(bigImg, minImg)

> 在大图里找出所有小图出现的位置（默认参数）。

- 参数 : bigImg {Image} 大图
- 参数 : minImg {Image} 小图
- 返回 : {Point[]} 所有命中位置的数组


```javascript
var img1 = $img.read("/$img/res/t06.png");
var img2 = $img.read("/$img/res/t07.png");
var points = $img.findImgAll(img1, img2);
for (var i = 0; i < points.length; i++) {
    log("第" + i + "个：" + points[i]);
}
```


### show(image)

> 把 Image 对象弹窗显示在屏幕上（调试用）。

- 参数 : image {Image} 要显示的图片


```javascript
var image = $img.read("/sdcard/Pictures/login.png");
if (image != null) $img.show(image);
```


### show(path)

> 按路径直接弹窗显示一张图片。

- 参数 : path {string} 图片路径


```javascript
//把图片显示在屏幕上
var imgPath = "sdcard/Pictures/t01.png";
$img.show(imgPath);
```


