# $color - 颜色操作

- 更新时间:2026-10-22 10:55:46

> 颜色操作工具（脚本里用 $color 调用）。
> 
> 它负责两件事：一是在图片/屏幕上“找颜色”——告诉你某个颜色出现在画面的哪个位置；
> 二是处理颜色值本身——把颜色转成数字、比较两个颜色是否相同、调亮调暗、算相似度等。
> 
> 颜色在脚本里最常见的写法是十六进制字符串，例如 "#FF0000" 表示纯红色（前两位是透明度，
> 接着两位红、两位绿、两位蓝）。本类还内置了一批常用颜色常量（$color.红色、$color.BLACK 等），
> 直接拿来用即可。
> 
> 新手提示：找色前先截屏得到一张图片（$screen.takeScreenshot），再在这张图上找；
> region（找色范围）格式是 [左上角x, 左上角y, 宽, 高]，不传就是整张图。



```javascript
//第一步：截取当前屏幕，得到一张图片对象
var image = $screen.takeScreenshot();
//第二步：在这张图上找纯红色，12 是颜色允许的误差（阈值）
var point = $color.find(image, "#FF0000", 12);
//第三步：判断是否找到了
if (point != null) {
    log("红色出现在：" + point.x + ", " + point.y);
}
```




### const {int} BLACK;

> 预定义颜色：黑色（英文常量 BLACK）。
> 
> 等价于十六进制 "#FF000000"。凡是需要传入“颜色数字”的地方，都可以直接用它，免去自己写色值。


```javascript
var c = $color.BLACK;      //取出黑色这个预定义颜色
log("黑色的数字是：" + c);
```


### const {int} DGRAY;

> 预定义颜色：深灰色（英文常量 DGRAY）。
> 
> 等价于十六进制 "#FF444444"，是比较暗的一种灰色。


```javascript
var c = $color.DGRAY;      //取出深灰色
log("深灰色的数字是：" + c);
```


### const {int} GRAY;

> 预定义颜色：灰色（英文常量 GRAY）。
> 
> 等价于十六进制 "#FF888888"，不深不浅的中间灰。


```javascript
var c = $color.GRAY;       //取出灰色
log("灰色的数字是：" + c);
```


### const {int} LGRAY;

> 预定义颜色：浅灰色（英文常量 LGRAY）。
> 
> 等价于十六进制 "#FFCCCCCC"，比较淡的一种灰色。


```javascript
var c = $color.LGRAY;      //取出浅灰色
log("浅灰色的数字是：" + c);
```


### const {int} WHITE;

> 预定义颜色：白色（英文常量 WHITE）。
> 
> 等价于十六进制 "#FFFFFFFF"。


```javascript
var c = $color.WHITE;      //取出白色
log("白色的数字是：" + c);
```


### const {int} RED;

> 预定义颜色：红色（英文常量 RED）。
> 
> 等价于十六进制 "#FFFF0000"，纯正的红色。


```javascript
var c = $color.RED;        //取出红色
log("红色的数字是：" + c);
```


### const {int} GREEN;

> 预定义颜色：绿色（英文常量 GREEN）。
> 
> 等价于十六进制 "#FF00FF00"，纯正的绿色。


```javascript
var c = $color.GREEN;      //取出绿色
log("绿色的数字是：" + c);
```


### const {int} BLUE;

> 预定义颜色：蓝色（英文常量 BLUE）。
> 
> 等价于十六进制 "#FF0000FF"，纯正的蓝色。


```javascript
var c = $color.BLUE;       //取出蓝色
log("蓝色的数字是：" + c);
```


### const {int} YELLOW;

> 预定义颜色：黄色（英文常量 YELLOW）。
> 
> 等价于十六进制 "#FFFFFF00"，纯正的黄色。


```javascript
var c = $color.YELLOW;     //取出黄色
log("黄色的数字是：" + c);
```


### const {int} CYAN;

> 预定义颜色：青色（英文常量 CYAN）。
> 
> 等价于十六进制 "#FF00FFFF"，即蓝绿相间的青色。


```javascript
var c = $color.CYAN;       //取出青色
log("青色的数字是：" + c);
```


### const {int} MAGENTA;

> 预定义颜色：品红色（英文常量 MAGENTA）。
> 
> 等价于十六进制 "#FFFF00FF"，即红紫相间的品红色。


```javascript
var c = $color.MAGENTA;    //取出品红色
log("品红色的数字是：" + c);
```


### const {int} TRANSPARENT;

> 预定义颜色：完全透明（英文常量 TRANSPARENT）。
> 
> 等价于十六进制 "#00000000"，完全看不见。常用于悬浮窗/画布“擦除一块”或设置全透明背景。


```javascript
var c = $color.TRANSPARENT; //取出透明色
log("透明色的数字是：" + c);
```


### find(img, color, threshold, region)

> 查找图片中第一个匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point 点对象；没有匹配点时返回 null。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。
> 区域数组顺序为 [左上角横坐标, 左上角纵坐标, 宽度, 高度]，不是两个角的坐标。
> 示例明确传入整张图的宽高，避免把空数组误当成有效矩形。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 参数 : threshold {int} 颜色容差，建议取 0～255；数值越大匹配越宽松。
- 参数 : region {double[]} 四项区域数组 [x,y,宽,高]，建议使用位于图片范围内的正宽高矩形。
- 返回 : {Point} 匹配点；找不到时为 null。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.find(img, "#a55978", 5, [0, 0, img.getWidth(), img.getHeight()]);
        if (result != null) {
            // Point 是点对象，通过 x、y 读取相对于原图左上角的坐标。
            info("坐标：" + result.x + ", " + result.y);
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### find(img, color, threshold)

> 查找图片中第一个匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point 点对象；没有匹配点时返回 null。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 参数 : threshold {int} 颜色容差，建议取 0～255；数值越大匹配越宽松。
- 返回 : {Point} 匹配点；找不到时为 null。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.find(img, "#a55978", 5);
        if (result != null) {
            // Point 是点对象，通过 x、y 读取相对于原图左上角的坐标。
            info("坐标：" + result.x + ", " + result.y);
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### find(img, color)

> 查找图片中第一个匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point 点对象；没有匹配点时返回 null。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。
> 这个重载使用默认容差 5；需要自行指定容差时，调用多一个参数的重载。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 返回 : {Point} 匹配点；找不到时为 null。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.find(img, "#a55978");
        if (result != null) {
            // Point 是点对象，通过 x、y 读取相对于原图左上角的坐标。
            info("坐标：" + result.x + ", " + result.y);
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### findAll(img, color, threshold, region)

> 查找图片中全部匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point[] 点数组；使用前检查 null，再通过 length 判断是否有结果。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。
> 区域数组顺序为 [左上角横坐标, 左上角纵坐标, 宽度, 高度]，不是两个角的坐标。
> 示例明确传入整张图的宽高，避免把空数组误当成有效矩形。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 参数 : threshold {int} 颜色容差，建议取 0～255；数值越大匹配越宽松。
- 参数 : region {double[]} 四项区域数组 [x,y,宽,高]，建议使用位于图片范围内的正宽高矩形。
- 返回 : {Point[]} 匹配点数组；调用方应同时处理 null 和长度为 0 的情况。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.findAll(img, "#a55978", 5, [0, 0, img.getWidth(), img.getHeight()]);
        // 使用普通下标循环遍历 Java 数组，兼容 ES5。
        if (result != null) {
            for (var i = 0; i < result.length; i++) {
                var point = result[i];
                info("坐标：" + point.x + ", " + point.y);
            }
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### findAll(img, color, threshold)

> 查找图片中全部匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point[] 点数组；使用前检查 null，再通过 length 判断是否有结果。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 参数 : threshold {int} 颜色容差，建议取 0～255；数值越大匹配越宽松。
- 返回 : {Point[]} 匹配点数组；调用方应同时处理 null 和长度为 0 的情况。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.findAll(img, "#a55978", 5);
        // 使用普通下标循环遍历 Java 数组，兼容 ES5。
        if (result != null) {
            for (var i = 0; i < result.length; i++) {
                var point = result[i];
                info("坐标：" + point.x + ", " + point.y);
            }
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### findAll(img, color)

> 查找图片中全部匹配颜色的位置。
> 
> 输入图片必须是尚未回收的 Image 对象，颜色使用 String 字符串，例如 "#a55978"。
> 查找可能因无效图片或非法颜色抛出异常，返回值不是错误信息。
> 返回 Point[] 点数组；使用前检查 null，再通过 length 判断是否有结果。
> 坐标以整张原图的左上角为原点，单位为像素，不是查找区域内的相对坐标。
> 这个重载使用默认容差 5；需要自行指定容差时，调用多一个参数的重载。

- 参数 : img {Image} 尚未回收的图片对象。
- 参数 : color {String} 颜色字符串，例如 "#a55978"。
- 返回 : {Point[]} 匹配点数组；调用方应同时处理 null 和长度为 0 的情况。


```javascript
// 先准备一张本地图片，路径要改成实际可读取的文件。
var img = $img.read("/sdcard/Download/sample.png");
try {
    // 图片读取失败或图片已经释放时，不能继续查找。
    if (img != null && img.getWidth() > 0 && img.getHeight() > 0) {
        var result = $color.findAll(img, "#a55978");
        // 使用普通下标循环遍历 Java 数组，兼容 ES5。
        if (result != null) {
            for (var i = 0; i < result.length; i++) {
                var point = result[i];
                info("坐标：" + point.x + ", " + point.y);
            }
        }
    }
} finally {
    // 查找完毕释放图片；即使查找抛出异常也会执行这里。
    if (img != null) { img.close(); }
}
```


### similar(c1, c2)

> 比较两种颜色看起来有多接近。

- 参数 : c1 {string|int} 第一个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 参数 : c2 {string|int} 第二个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 返回 : {double} 两种颜色的相似度（0~1，越接近 1 越像）
- 版本 : 1.0.0


```javascript
//计算相似度
var result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


### similar(c1, c2)

> 比较两种颜色看起来有多接近。

- 参数 : c1 {string|int} 第一个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 参数 : c2 {string|int} 第二个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 返回 : {double} 两种颜色的相似度（0~1，越接近 1 越像）
- 版本 : 1.0.0


```javascript
//计算相似度
var result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


### similar(c1, c2)

> 比较两种颜色看起来有多接近。

- 参数 : c1 {string|int} 第一个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 参数 : c2 {string|int} 第二个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 返回 : {double} 两种颜色的相似度（0~1，越接近 1 越像）
- 版本 : 1.0.0


```javascript
//计算相似度
var result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


### similar(c1, c2)

> 比较两种颜色看起来有多接近。

- 参数 : c1 {string|int} 第一个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 参数 : c2 {string|int} 第二个颜色，可为 "#RRGGBB" 字符串或十进制颜色值
- 返回 : {double} 两种颜色的相似度（0~1，越接近 1 越像）
- 版本 : 1.0.0


```javascript
//计算相似度
var result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


### toString(color)

> 将颜色值转换为 8 位字符串。

- 参数 : color {int} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {string} 颜色对应的十六进制字符串，如 "#FF0000"
- 版本 : 1.0.0


```javascript
//转为#00000000
var color = $color.toString(-166780);
```


### str(color)

> 将颜色值转换为 6 位字符串。

- 参数 : color {int} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {string} 颜色对应的十六进制字符串，如 "#FF0000"
- 版本 : 1.0.0


```javascript
//转为#000000
var color = $color.str(-166780);
```


### parse(r, g, b)

> 把红绿蓝三个分量（或颜色字符串）合成一个十进制颜色值。

- 参数 : r {int} 红色分量，0~255
- 参数 : g {int} 绿色分量，0~255
- 参数 : b {int} 蓝色分量，0~255
- 返回 : {int} 由 RGB/颜色字符串解析出的十进制颜色值 int
- 版本 : 1.0.0


```javascript
var color = $color.parse(105,78,230);
```


### parse(color)

> 解析颜色值。
> 
> 颜色统一写成 "#RRGGBB" 或 "#AARRGGBB" 字符串，也可直接用十进制颜色值。

- 参数 : color {string} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 由 RGB/颜色字符串解析出的十进制颜色值 int
- 版本 : 1.0.0


```javascript
//解析颜色值
var colorValue = $color.parse("#1E1F22");
log("颜色值",colorValue);
// （示例步骤）
// （示例步骤）
var color = $color.parse("white");
var color = $color.parse("black");
var color = $color.parse("null");
var color = $color.parse("none");
var color = $color.parse("green");
var color = $color.parse("red");
var color = $color.parse("blue");
var color = $color.parse("yellow");
// （示例步骤）
var color = $color.parse("colorPrimary");//(常用)一般是主题最明显的颜色：蓝色主题一般呈现蓝色
var color = $color.parse("colorSurface");//(常用)一般是背景颜色：亮色主题一般呈现白色，暗色主题一般呈现黑色
var color = $color.parse("colorOnSurface");//(常用)一般是文字颜色：亮色主题一般呈现黑色，暗色主题一般呈现白色
var color = $color.parse("colorOnPrimary");
var color = $color.parse("colorPrimaryContainer");
var color = $color.parse("colorOnPrimaryContainer");
var color = $color.parse("colorSecondary");
var color = $color.parse("colorOnSecondary");
var color = $color.parse("colorSecondaryContainer");
var color = $color.parse("colorOnSecondaryContainer");
var color = $color.parse("colorTertiary");
var color = $color.parse("colorOnTertiary");
var color = $color.parse("colorTertiaryContainer");
var color = $color.parse("colorOnTertiaryContainer");
var color = $color.parse("colorError");
var color = $color.parse("colorErrorContainer");
var color = $color.parse("colorOnErrorContainer");
var color = $color.parse("colorOnBackground");
var color = $color.parse("colorSurfaceVariant");
var color = $color.parse("colorOnSurfaceVariant");
var color = $color.parse("colorOutline");
var color = $color.parse("colorOutlineVariant");
var color = $color.parse("colorPrimaryInverse");
```


### setAlpha(color, alpha)

> 给一个颜色设置透明度，得到半透明的新颜色。

- 参数 : color {int} 颜色值（十进制 int，如 -1 表示白色）
- 参数 : alpha {int} 透明度分量，0（全透明）~255（不透明）
- 返回 : {int} 设置好透明度后的新颜色值 int
- 版本 : 1.4.3


```javascript
//解析颜色值
var colorValue = $color.parse("#1E1F22");
//设置颜色的透明度
var color = $color.setAlpha(colorValue,100);
```


### brighter(color)

> 获取颜色的浅色版本。

- 参数 : color {int} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 变亮后的新颜色值
- 版本 : 1.4.3


```javascript
//解析颜色值
var colorValue = $color.parse("#1E1F22");
//获取较亮颜色
var color = $color.brighter(colorValue);
```


### darker(color)

> 获取颜色的深色版本。

- 参数 : color {int} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 变暗后的新颜色值
- 版本 : 1.4.3


```javascript
//解析颜色值
var colorValue = $color.parse("#1E1F22");
//获取较暗颜色值
var color = $color.darker(colorValue);
```


### rgb(red, green, blue)

> 由红、绿、蓝三个分量合成一个不透明颜色值。

- 参数 : red {int} 红色分量，0~255
- 参数 : green {int} 绿色分量，0~255
- 参数 : blue {int} 蓝色分量，0~255
- 返回 : {int} 由红绿蓝三色合成的十进制颜色值（不透明）
- 版本 : 1.0.0


```javascript
var color = $color.rgb(105,78,230);
```


### argb(alpha, red, green, blue)

> 由透明度、红、绿、蓝四个分量合成一个颜色值。

- 参数 : alpha {int} 透明度分量，0（全透明）~255（不透明）
- 参数 : red {int} 红色分量，0~255
- 参数 : green {int} 绿色分量，0~255
- 参数 : blue {int} 蓝色分量，0~255
- 返回 : {int} 由透明度+红绿蓝合成的十进制颜色值
- 版本 : 1.0.0


```javascript
var color = $color.argb(255,105,78,230);
```


### a(color)

> 取出颜色中的透明度(A)分量。

- 参数 : color {String} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 颜色中的透明度分量（0~255）
- 版本 : 1.0.0


```javascript
var a = $color.a("#357C94");
```


### r(color)

> 获取红色通道值。

- 参数 : color {String} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 颜色中的红色分量（0~255）
- 版本 : 1.0.0


```javascript
var r = $color.r("#357C94");
```


### g(color)

> 获取绿色通道值。

- 参数 : color {String} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 颜色中的绿色分量（0~255）
- 版本 : 1.0.0


```javascript
var g = $color.g("#357C94");
```


### b(color)

> 获取蓝色通道值。

- 参数 : color {String} 颜色值（十进制 int，如 -1 表示白色）
- 返回 : {int} 颜色中的蓝色分量（0~255）
- 版本 : 1.0.0


```javascript
var b = $color.b("#357C94");
```


### equals(c1, c2)

> 比较两个颜色的红、绿、蓝分量是否相同。
> 
> 返回 boolean 布尔值：三个颜色分量都相同为 true，否则为 false。
> 此方法忽略透明度，因此不能用它判断两个颜色的完整四个分量是否完全一致。
> 字符串会先解析为颜色值；请传可识别的颜色，不要把解析错误当作颜色不同的正常结果。

- 参数 : c1 {int} 第1个颜色，用包含颜色分量的整数表示，负数也是正常的颜色值。
- 参数 : c2 {int} 第2个颜色，用包含颜色分量的整数表示，负数也是正常的颜色值。
- 返回 : {boolean} 红绿蓝分量相同为 true；不比较透明度。


```javascript
// 本示例明确选择参数类型对应的重载，避免数字和字符串混用。
var same = $color["equals(int,int)"](-14803166, -14803166);
info("红绿蓝分量相同：" + same);
// 透明度不同但红绿蓝相同，也会被这个方法判定为相同。
var sameRgb = $color.equals(0x001E1F22, -14803166);
```


### equals(c1, c2)

> 比较两个颜色的红、绿、蓝分量是否相同。
> 
> 返回 boolean 布尔值：三个颜色分量都相同为 true，否则为 false。
> 此方法忽略透明度，因此不能用它判断两个颜色的完整四个分量是否完全一致。
> 字符串会先解析为颜色值；请传可识别的颜色，不要把解析错误当作颜色不同的正常结果。

- 参数 : c1 {int} 第1个颜色，用包含颜色分量的整数表示，负数也是正常的颜色值。
- 参数 : c2 {String} 第2个颜色，用颜色字符串表示，例如 "#1E1F22"。
- 返回 : {boolean} 红绿蓝分量相同为 true；不比较透明度。


```javascript
// 本示例明确选择参数类型对应的重载，避免数字和字符串混用。
var same = $color["equals(int,java.lang.String)"](-14803166, "#1E1F22");
info("红绿蓝分量相同：" + same);
// 透明度不同但红绿蓝相同，也会被这个方法判定为相同。
var sameRgb = $color.equals(0x001E1F22, "#1E1F22");
```


### equals(c1, c2)

> 比较两个颜色的红、绿、蓝分量是否相同。
> 
> 返回 boolean 布尔值：三个颜色分量都相同为 true，否则为 false。
> 此方法忽略透明度，因此不能用它判断两个颜色的完整四个分量是否完全一致。
> 字符串会先解析为颜色值；请传可识别的颜色，不要把解析错误当作颜色不同的正常结果。

- 参数 : c1 {String} 第1个颜色，用颜色字符串表示，例如 "#1E1F22"。
- 参数 : c2 {int} 第2个颜色，用包含颜色分量的整数表示，负数也是正常的颜色值。
- 返回 : {boolean} 红绿蓝分量相同为 true；不比较透明度。


```javascript
// 本示例明确选择参数类型对应的重载，避免数字和字符串混用。
var same = $color["equals(java.lang.String,int)"]("#1E1F22", -14803166);
info("红绿蓝分量相同：" + same);
// 透明度不同但红绿蓝相同，也会被这个方法判定为相同。
var sameRgb = $color.equals("#001E1F22", -14803166);
```


### equals(c1, c2)

> 比较两个颜色的红、绿、蓝分量是否相同。
> 
> 返回 boolean 布尔值：三个颜色分量都相同为 true，否则为 false。
> 此方法忽略透明度，因此不能用它判断两个颜色的完整四个分量是否完全一致。
> 字符串会先解析为颜色值；请传可识别的颜色，不要把解析错误当作颜色不同的正常结果。

- 参数 : c1 {String} 第1个颜色，用颜色字符串表示，例如 "#1E1F22"。
- 参数 : c2 {String} 第2个颜色，用颜色字符串表示，例如 "#1E1F22"。
- 返回 : {boolean} 红绿蓝分量相同为 true；不比较透明度。


```javascript
// 本示例明确选择参数类型对应的重载，避免数字和字符串混用。
var same = $color["equals(java.lang.String,java.lang.String)"]("#1E1F22", "#1E1F22");
info("红绿蓝分量相同：" + same);
// 透明度不同但红绿蓝相同，也会被这个方法判定为相同。
var sameRgb = $color.equals("#001E1F22", "#1E1F22");
```


### isDarkTheme()

> 检查应用是否使用深色主题。
> 

- 返回 : {boolean} true 表示当前系统是深色（暗色）主题


```javascript
var isDark = $color.isDarkTheme();
if(isDark){
    toast("黑暗主题");
}else{
    toast("亮色主题");
}
```


### isColor(colorStr)

> 检查颜色字符串格式是否有效。

- 参数 : colorStr {string} 要判断是否合法的颜色字符串
- 返回 : {boolean} true 表示该字符串是合法的颜色写法
- 版本 : 1.4.3


```javascript
var isColor = $color.isColor("#1E1F22");
if(isColor){
    toast("颜色格式正确");
}else{
    toast("颜色格式错误");
}
```


