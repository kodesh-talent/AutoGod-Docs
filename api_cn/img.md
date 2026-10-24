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




### 读取(图片路径)

> 读取图片
> 
> 支持相对路径写法。

- 参数 : 图片路径 {string} 图片路径
- 返回 : {Image} 读取成功返回 Image 对象；失败返回 null
- 版本 : 1.7.0


```javascript
//图片路径
var 路径 = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
var 图片 = $img.read(路径);
```


### 打开(图片路径)

> 打开（读入）一张图片（open 的中文写法）。

- 参数 : 图片路径 {string} 图片路径
- 返回 : {Image} 成功返回 Image 对象；失败返回 null
- 版本 : 1.7.0


```javascript
//图片路径
var 路径 = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
var 图片 = $img.open(路径);
```


### 打开(位图)

> 把安卓 Bitmap 包装成 Image 对象（open(Bitmap) 的中文写法）。

- 参数 : 位图 {Bitmap} 安卓位图对象
- 返回 : {Image} 包装好的 Image 对象
- 版本 : 1.7.0


```javascript
//先从控件拿到位图
var 图片控件 = ui.id("myImg");
var 位图 = 图片控件.getImg();
//包装成 Image 对象
var 图片 = $img.open(位图);
```


### 读取(图片文件)

> 读取图片
> 
> 从 File 对象读入图片（read(File) 的中文写法）。

- 参数 : 图片文件 {File} 文件对象
- 返回 : {Image} 成功返回 Image 对象；失败返回 null
- 版本 : 1.7.0


```javascript
var file = new java.io.File("/sdcard/Pictures/sample.png");
var image = $img.read(file);
if (image != null) $img.show(image);
```


### 保存(图片, 路径, 格式, 质量)

> 保存图片
> 
> 支持相对路径写法

- 参数 : 图片 {Image} 要保存的 Image 对象
- 参数 : 路径 {string} 保存路径
- 参数 : 格式 {string} 图片格式，如 "png"、"jpg"
- 参数 : 质量 {int} 保存质量 1 到 100
- 版本 : 1.7.0


```javascript
//截屏并且保存到本地
$screen.getPermit();
var 截屏图片 = $screen.getScreen();
$img.save(截屏图片, "/sdcard/s05.png", "png", 100);
```


### 保存(图片, 路径)

> 保存图片
> 
> 把 Image 保存成 png 图片文件（默认质量 100）。

- 参数 : 图片 {Image} 要保存的 Image 对象
- 参数 : 路径 {string} 保存路径
- 版本 : 1.7.0


```javascript
//截屏并且保存到本地
$screen.getPermit();
var 屏幕截屏 = $screen.getScreen();
$img.save(屏幕截屏, "/sdcard/s05.png");
```


### 转base64(图片, 格式, 质量)

> 把图片转成 Base64 字符串（toBase64 的中文写法）。

- 参数 : 图片 {Image} 要转换的 Image 对象
- 参数 : 格式 {string} 图片格式
- 参数 : 质量 {int} 压缩质量 1 到 100
- 返回 : {string} Base64 字符串；失败返回 null
- 版本 : 1.7.0


```javascript
var img = $img.read("/sdcard/p01.png");
var baseStr = $img.toBase64(img, "png", 50);
log(baseStr);
```


### 转base64(图片)

> 把图片转成 Base64（toBase64(Image) 的中文写法）。

- 参数 : 图片 {Image} 要转换的 Image 对象
- 返回 : {string} Base64 字符串；失败返回 null
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p01.png";
var 图片 = $img.read(路径);
var base64 = $img.toBase64(图片);
log(base64);
```


### 转base64(路径)

> 按路径读图并转 Base64（toBase64(path) 的中文写法）。

- 参数 : 路径 {string} 图片路径
- 返回 : {string} Base64 字符串；失败返回 null
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p01.png";
var base64 = $img.toBase64(路径);
log(base64);
```


### 读取base64(base64)

> 把 Base64 字符串还原成图片（readBase64 的中文写法）。

- 参数 : base64 {string} Base64 字符串
- 返回 : {Image} 还原成功返回 Image 对象；失败返回 null
- 版本 : 1.7.0


```javascript
var baseStr = $img.toBase64(img, "png", 50);
var 图片2 = $img.readBase64(baseStr);
$img.show(图片2);
```


### 裁剪(图片, x, y, w, h)

> 裁剪图片

- 参数 : 图片 {Image} 要裁剪的原图片
- 参数 : x {int} 裁剪区域左上角 x
- 参数 : y {int} 裁剪区域左上角 y
- 参数 : w {int} 裁剪宽度
- 参数 : h {int} 裁剪高度
- 返回 : {Image} 裁剪后的新图片
- 版本 : 1.7.0


```javascript
//图片路径
var 路径 = "/sdcard/p01.png";
//读取图片
var 图片 = $img.read(路径);
//裁剪出左上角 300x200
var 裁剪后图片 = $img.clip(图片, 0, 0, 300, 200);
//显示图片
$img.show(裁剪后图片);
```


### 设置尺寸(图片, w, h, 插值方式)

> 把图片缩放到指定宽高（resize 的中文写法）。
> 
> 插值方式（忽略大小写）：INTER_NEAREST、INTER_LINEAR、INTER_CUBIC、
> INTER_AREA、INTER_LANCZOS4、INTER_LINEAR_EXACT。

- 参数 : 图片 {Image} 要缩放的原图片
- 参数 : w {int} 目标宽度
- 参数 : h {int} 目标高度
- 参数 : 插值方式 {string} 插值方式
- 返回 : {Image} 缩放后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.resize(图片, 200, 200, "INTER_CUBIC");
$img.show(新图片);
```


### 设置尺寸(图片, w, h)

> 设置尺寸
> 
> 把图片缩放到指定宽高（用默认插值算法）。

- 参数 : 图片 {Image} 要缩放的原图片
- 参数 : w {int} 目标宽度
- 参数 : h {int} 目标高度
- 返回 : {Image} 缩放后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.resize(图片, 200, 200);
$img.show(新图片);
```


### 缩放(图片, 缩放X, 缩放Y, 插值方式)

> 缩放图片

- 参数 : 图片 {Image} 原图片
- 参数 : 缩放X {double} 宽度倍数
- 参数 : 缩放Y {double} 高度倍数
- 参数 : 插值方式 {string} 插值方式
- 返回 : {Image} 缩放后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.scale(图片, 0.3, 0.2, "CUBIC");
$img.show(新图片);
```


### 缩放(图片, 缩放X, 缩放Y)

> 缩放图片

- 参数 : 图片 {Image} 原图片
- 参数 : 缩放X {double} 宽度倍数
- 参数 : 缩放Y {double} 高度倍数
- 返回 : {Image} 缩放后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.scale(图片, 0.3, 0.2);
$img.show(新图片);
```


### 旋转(图片, 角度, x, y)

> 旋转图片

- 参数 : 图片 {Image} 要旋转的图片
- 参数 : 角度 {float} 旋转角度（度）
- 参数 : x {int} 旋转中心 x，null 用中心
- 参数 : y {int} 旋转中心 y，null 用中心
- 返回 : {Image} 旋转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.rotate(图片, 45, 100, 200);
$img.show(新图片);
```


### 旋转(图片, 角度)

> 旋转图片

- 参数 : 图片 {Image} 要旋转的图片
- 参数 : 角度 {float} 旋转角度（度）
- 返回 : {Image} 旋转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.rotate(图片, 45);
$img.show(新图片);
```


### 旋转(图片)

> 旋转图片
> 
> 默认旋转90度

- 参数 : 图片 {Image} 要旋转的图片
- 返回 : {Image} 旋转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.rotate(图片); //默认旋转90度
$img.show(新图片);
```


### 拼接(图片1, 图片2, 拼接方向)

> 拼接图片

- 参数 : 图片1 {Image} 第一张图
- 参数 : 图片2 {Image} 第二张图
- 参数 : 拼接方向 {string} "left"/"right"/"top"/"bottom"
- 返回 : {Image} 拼接后的新图片
- 版本 : 1.7.0


```javascript
var 图片1 = $img.read("/$img/res/t02.png");
var 图片2 = $img.read("/$img/res/t03.png");
图片1 = $img.resize(图片1, 300, 200);
图片2 = $img.resize(图片2, 300, 200);
var 图片 = $img.concat(图片1, 图片2, "bottom");
$img.show(图片);
```


### 灰度化(图片)

> 灰度化

- 参数 : 图片 {Image} 要处理的图片
- 返回 : {Image} 灰度化后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.gray(图片);
$img.show(新图片);
```


### 二值化(图片, 阈值)

> 二值化图片

- 参数 : 图片 {Image} 要处理的图片
- 参数 : 阈值 {double} 阈值 0 到 255
- 返回 : {Image} 二值化后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.threshold(图片, 150);
$img.show(新图片);
```


### 自适应二值化(图片, 最大值, 自适应算法, 阈值化类型, 邻域块大小, 偏移值调整量)

> 自适应二值化

- 参数 : 图片 {Image} 要处理的图片
- 参数 : 最大值 {number} 最大值（通常 255）
- 参数 : 自适应算法 {string} 自适应算法
- 参数 : 阈值化类型 {string} 阈值化类型
- 参数 : 邻域块大小 {number} 邻域块大小
- 参数 : 偏移值调整量 {number} 偏移调整量
- 返回 : {Image} 处理后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.adaptiveThreshold(图片, 255, "MEAN_C", "BINARY", 11, 2);
$img.show(新图片);
```


### 颜色空间转换(图片, 转换类型, 颜色通道数量)

> 颜色空间转换

- 参数 : 图片 {Image} 要转换的图片
- 参数 : 转换类型 {string} 转换类型，如 "RGBA2BGR"
- 参数 : 颜色通道数量 {int} 目标通道数，null 表示不变
- 返回 : {Image} 转换后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.cvtColor(图片, "RGBA2BGR", null);
$img.show(新图片);
```


### 颜色空间转换(图片, 转换类型)

> 颜色空间转换

- 参数 : 图片 {Image} 要转换的图片
- 参数 : 转换类型 {string} 转换类型
- 返回 : {Image} 转换后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.cvtColor(图片, "RGBA2BGR");
$img.show(新图片);
```


### 图片二值化(图片, 颜色下界, 颜色上界)

> 图片二值化

- 参数 : 图片 {Image} 要处理的图片
- 参数 : 颜色下界 {string} 颜色下界 "#RRGGBB"
- 参数 : 颜色上界 {string} 颜色上界 "#RRGGBB"
- 返回 : {Image} 处理后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.inRange(图片, "#666666", "#FFFFFF");
$img.show(新图片);
```


### 滤波(图片, 滤波器大小, 锚点, 推断类型)

> 对图片做模糊处理（blur 的中文写法）。
> 
> 边框类型（不区分大小写）：DEFAULT、REPLICATE、REFLECT、WRAP、CONSTANT。

- 参数 : 图片 {Image} 要模糊的图片
- 参数 : 滤波器大小 {double[]} 滤波器大小
- 参数 : 锚点 {double[]} 锚点，[-1,-1] 为中心
- 参数 : 推断类型 {string} 边框类型
- 返回 : {Image} 模糊后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.blur(图片, [10, 10], [-1, -1], "REPLICATE");
$img.show(新图片);
```


### 中值滤波(图片, 滤波器大小)

> 中值滤波

- 参数 : 图片 {Image} 要处理的图片
- 参数 : 滤波器大小 {int} 滤波器大小（奇数）
- 返回 : {Image} 处理后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.medianBlur(图片, 3);
$img.show(新图片);
```


### 高斯滤波(图片, 滤波器大小, x方差, y方差, 推断类型)

> 高斯模糊（gaussianBlur 的中文写法）。

- 参数 : 图片 {Image} 要模糊的图片
- 参数 : 滤波器大小 {double[]} 滤波器大小
- 参数 : x方差 {double} x 方向方差，0 自动
- 参数 : y方差 {double} y 方向方差，0 自动
- 参数 : 推断类型 {string} 边框类型
- 返回 : {Image} 模糊后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.gaussianBlur(图片, [15, 15], 0, 0, "WRAP");
$img.show(新图片);
```


### 左右翻转(图片)

> 左右翻转

- 参数 : 图片 {Image} 要翻转的图片
- 返回 : {Image} 翻转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.flip(图片);
$img.show(新图片);
```


### 上下翻转(图片)

> 上下翻转

- 参数 : 图片 {Image} 要翻转的图片
- 返回 : {Image} 翻转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.upside(图片);
$img.show(新图片);
```


### 翻转(图片, sx, sy)

> 水平翻转

- 参数 : 图片 {Image} 要翻转的图片
- 参数 : sx {float} 横向系数，-1 水平镜像
- 参数 : sy {float} 纵向系数，-1 垂直镜像
- 返回 : {Image} 翻转后的新图片
- 版本 : 1.7.0


```javascript
var 路径 = "/sdcard/p02.png";
var 图片 = $img.read(路径);
var 新图片 = $img.flip(图片, -1, -1);
$img.show(新图片);
```


### 放在上面(大图, 小图, x, y)

> 在大图片上面放置一个小图片

- 参数 : 大图 {Image} 大背景图
- 参数 : 小图 {Image} 要贴上去的小图
- 参数 : x {int} 小图左上角 x
- 参数 : y {int} 小图左上角 y
- 返回 : {Image} 合成后的新图片
- 版本 : 1.7.0


```javascript
var 大图 = $img.read("/sdcard/big.png");
var 小图 = $img.read("/sdcard/small.png");
//把小图贴到大图 (20,20) 处
var 新图片 = $img.putTop(大图, 小图, 20, 20);
$img.show(新图片);
```


### 找色(图片, 颜色, 阈值, x, y, w, h)

> 查找颜色

- 参数 : 图片 {Image} 要查找的图片
- 参数 : 颜色 {string} 要找的颜色
- 参数 : 阈值 {int} 颜色容差
- 参数 : x {int} 区域左上角 x
- 参数 : y {int} 区域左上角 y
- 参数 : w {int} 区域宽
- 参数 : h {int} 区域高
- 返回 : {Point} 找到返回点；否则 null
- 版本 : 1.7.0


```javascript
var img = $img.read("/$img/res/t01.png");
var 位置 = $img.findColor(img, "#d80005", 5, 0, 0, 100, 100);
log("找到：" + 位置);
```


### 找色(图片, 颜色, 阈值, 范围)

> 查找颜色

- 参数 : 图片 {Image} 要查找的图片
- 参数 : 颜色 {string} 要找的颜色
- 参数 : 阈值 {int} 颜色容差
- 参数 : 范围 {int[]} 搜索区域 [x,y,w,h]
- 返回 : {Point} 找到返回点；否则 null
- 版本 : 1.7.0


```javascript
var img = $img.read("/$img/res/t01.png");
var 位置 = $img.findColor(img, "#d80005", 5, [0, 0, 100, 100]);
log("找到：" + 位置);
```


### 找色(图片, 颜色, 阈值)

> 查找颜色

- 参数 : 图片 {Image} 要查找的图片
- 参数 : 颜色 {string} 要找的颜色
- 参数 : 阈值 {int} 颜色容差
- 返回 : {Point} 找到返回点；否则 null
- 版本 : 1.7.0


```javascript
var img = $img.read("/$img/res/t01.png");
var 位置 = $img.findColor(img, "#d80005", 5);
log("找到：" + 位置);
```


### 找色(图片, 颜色)

> 查找颜色

- 参数 : 图片 {Image} 要查找的图片
- 参数 : 颜色 {string} 要找的颜色
- 返回 : {Point} 找到返回点；否则 null
- 版本 : 1.7.0


```javascript
var img = $img.read("/$img/res/t01.png");
var 位置 = $img.findColor(img, "#d80005");
log("找到：" + 位置);
```


### 多点找色(图片, 范围, 起点颜色, 阈值, 点色数据)

> 多点找色

- 参数 : 图片 {Image} 要查找的图片
- 参数 : 范围 {Number[]} 搜索区域 [x,y,w,h]
- 参数 : 起点颜色 {string} 基准点颜色
- 参数 : 阈值 {int} 颜色容差
- 参数 : 点色数据 {Object[]} 相对点色数据
- 返回 : {Point} 找到返回基准点；否则 null
- 版本 : 1.7.0


```javascript
//多点找色：一组相对偏移的颜色共同定位
var 位置 = $img.findMultiColors(图片,[0],"#e70216",5,[
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
提示("结果",位置);
```


### 找图(大图片, 小图片, 参数)

> 在大图中查找小图，并按参数限制搜索区域或相似度。

- 参数 : 大图片 {Image} 大图（被搜索的底图）
- 参数 : 小图片 {Image} 小图（要找的图标）
- 参数 : 参数 {object} 查找参数 { similar: 0.8, region: [x,y,w,h] }
- 返回 : {Point} 找到返回左上角点；否则 null


```javascript
var screen = $img.read("/sdcard/Pictures/screen.png");
var icon = $img.read("/sdcard/Pictures/icon.png");
var point = $img.找图(screen, icon, { similar: 0.8 });
```


### 找图(大图片, 小图片)

> 找图

- 参数 : 大图片 {Image} 大图
- 参数 : 小图片 {Image} 小图
- 返回 : {Point} 找到返回左上角点；否则 null
- 版本 : 1.7.0


```javascript
var img1 = $img.read("/$img/res/t05.png");
var img2 = $img.read("/$img/res/t04.png");
var 位置 = $img.findImg(img1, img2);
log("找到：" + 位置);
```


### 找到所有图(大图片, 小图片, 参数)

> 找到所有图片位置

- 参数 : 大图片 {Image} 大图
- 参数 : 小图片 {Image} 小图
- 参数 : 参数 {object} 查找参数
- 返回 : {Point[]} 所有命中位置的数组
- 版本 : 1.7.0


```javascript
var 图片1 = $img.read("/$img/res/t06.png");
var 图片2 = $img.read("/$img/res/t07.png");
var 位置 = $img.findImgAll(图片1, 图片2, { similar: 0.8 });
for (var i = 0; i < 位置.length; i++) {
    log("第" + i + "个：" + 位置[i]);
}
```


### 找到所有图(大图片, 小图片)

> 找到所有图片位置

- 参数 : 大图片 {Image} 大图
- 参数 : 小图片 {Image} 小图
- 返回 : {Point[]} 所有命中位置的数组
- 版本 : 1.7.0


```javascript
var 图片1 = $img.read("/$img/res/t06.png");
var 图片2 = $img.read("/$img/res/t07.png");
var 位置 = $img.findImgAll(图片1, 图片2);
for (var i = 0; i < 位置.length; i++) {
    log("第" + i + "个：" + 位置[i]);
}
```


### 显示(图片)

> 显示图片

- 参数 : 图片 {Image} 要显示的图片
- 版本 : 1.7.0


```javascript
var image = $img.read("/sdcard/Pictures/login.png");
if (image != null) $img.显示(image);
```


### 显示(路径)

> 显示图片

- 参数 : 路径 {string} 图片路径
- 版本 : 1.7.0


```javascript
//把图片显示在屏幕上
var 图片路径 = "sdcard/Pictures/t01.png";
$img.show(图片路径);
```


