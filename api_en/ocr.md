# $ocr - 文字识别

- 更新时间:2026-10-22 10:55:50

> 文字识别对象，脚本里叫 $ocr（中文文档里叫 $文字识别）。
> 
> 负责对截屏或本地图片做 OCR，把图里的文字读出来，还能拿到每段文字在屏幕上的坐标，常配合 $act 做自动点按。



```javascript
$ocr.init();
var text = $ocr.onlyRec("/sdcard/Pictures/text.png");
```




### v(name)

> 选择要使用的 OCR 识别引擎。
> 
> 可选值："mlkit"（谷歌 ML Kit，默认，免初始化）、"ppv5"（PaddleOCR v5）、"ncnn"（轻量版）。
> 必须在第一次识别之前、init 之前调用，否则不生效。

- 参数 : name {string} 引擎名称：mlkit / ppv5 / ncnn
- 版本 : 1.2.2


```javascript
//此函数要放在识别之前调用
$ocr.v("mlkit");//设置要使用的OCR引擎
```


### init()

> 初始化当前选择的 OCR 引擎。
> 
> ppv5/ncnn 引擎需要先加载模型；mlkit 则直接返回成功。
> 
> 一般在脚本开头、用 v() 选好引擎后调用一次。

- 返回 : {DetectResult} 识别结果集，用 isSuccess() 判断成败，getData() 取每段文字和坐标
- 版本 : 1.0.0


```javascript
$ocr.init();
```


### getPoint(word, options)

> 识别屏幕并找到指定文字所在的位置。
> 
> 识别后会逐行去掉空格换行，看哪一行包含你要找的文字，命中就返回它左上角的坐标。
> 
> 它是对 detect() 的封装，省去你自己遍历结果集的麻烦。

- 参数 : word {string} 要在识别结果里查找的文字（包含匹配即可）
- 参数 : options {Ocr选项} 识别配置对象（范围/灰度化/颜色/阈值等，见示例）
- 返回 : {Point} 命中文字的坐标；没找到返回 null
- 版本 : 1.0.0


```javascript
//配置方式1:灰度化识别
var options = {
    范围: [0, 0, 200, 100],   //可选，识别范围；不填就识别整屏
    是否灰度化: true,          //必须，开启灰度化，速度更快
    是否保存图片: false        //可选，是否把识别图存到本地
};
//配置方式2:二值化识别
var options = {
    范围: [0, 0, 200, 100],   //可选，识别范围；不填就识别整屏
    颜色: "#FFFFFF",           //必须，要找的文字颜色
    阈值: 20,                  //可选，二值化阈值，建议 20-50
    是否保存图片: false,       //可选，是否把识别图存到本地
    保存路径: "/sdcard/a.png"  //开启保存时给出保存路径
};
//上面的配置自己根据自身需求选择一个即可
//在屏幕上找"文字"两个字
var point = $ocr.getPoint("文字", options);
if (point != null) {
    //找到了就点它
    $act.click(point);
}
```


### line(options)

> 识别当前屏幕指定区域，将文字拼接成一行。
> 
> 输入类型为 Object，使用普通脚本对象填写 OcrOptions 的配置键。先取得截屏权限，再确保识别区域在截图范围内。
> 范围四个数依次为左上角横坐标、纵坐标、宽、高，单位像素；下例只是示范，需要按实际画面修改。
> 灰度模式把图片转成灰度后识别；二值化模式按文字颜色和阈值筛选像素。不同画面应选择合适方式，不保证哪种总是更快或更准。
> 不要在同一配置中混用同一选项的中英文键；字段优先级详见 OcrOptions。
> 返回类型为 String。按识别结果顺序去掉各条文字中的空白后直接拼接，不会在条目间补空格或换行，也不是只识别画面的第一行。
> 开启提取数字后会从拼接的文字中提取数字并用逗号分隔，结果仍是字符串。配置无法转换、识别失败时可能返回 null，未拼接出内容时可能是空字符串。
> 配置转换、图像处理或识别过程可能抛出异常，示例使用异常处理记录原因。

- 参数 : options {Object} 可转换成 OcrOptions 的配置对象
- 返回 : {String} 拼接后的文字，可能为 null 或空字符串
- 版本 : 1.0.0


```javascript
// 提前取得截屏权限；把范围改为实际文字所在区域。
var options = {
    region: [0, 0, 300, 100],
    gray: true, // 本例选择灰度处理。
    save: false // 示例不向设备保存图片。
};
options.number = false; // 改成 true 可提取数字。
try {
    var result = $ocr.line(options);
    if (result != null && String(result).length > 0) {
        log(result); // 使用拼接后的字符串。
    } else {
        log("没有取得文字，请检查画面、权限和配置。");
    }
} catch (error) {
    log("文字识别异常：" + error);
}
```


### line(img)

> 识别一个 Bitmap 位图，把其中的文字拼成一行返回。
> 
> 直接传入位图，免去再包一层 Image。
> 
> 识别完记得手动释放图片资源。

- 参数 : img {Image} 要识别的图片对象（由 $img.read 等获得）
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.7


```javascript
//设置版本
$ocr.v("mlkit");
//获取图片对象
var img = $img.read("t01.png");
//识别位图、拿到文本
var txt = $ocr.line(img.getBitmap());
log(txt);
//释放资源
img.recycle();
```


### line(img)

> 识别一个 Image 图片对象，把其中的文字拼成一行返回。
> 
> 直接传入图片对象即可。
> 
> 识别完记得手动释放图片资源。

- 参数 : img {Image} 要识别的图片对象（由 $img.read 等获得）
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.7


```javascript
//设置版本
$ocr.v("mlkit");
//获取图片对象
var img = $img.read("t01.png");
//识别图片、拿到文本
var txt = $ocr.line(img);
log(txt);
//释放资源
img.recycle();
```


### line(img, x, y, w, h)

> 识别图片上指定小区域里的文字，拼成一行返回。
> 
> 先按 x、y、w、h 从原图裁出一块，再对这块做识别。
> 
> 裁出来的临时图片会自动释放，原图片需手动释放。

- 参数 : img {Image} 要识别的图片对象（由 $img.read 等获得）
- 参数 : x {int} 裁剪区域左上角横坐标
- 参数 : y {int} 裁剪区域左上角纵坐标
- 参数 : w {int} 裁剪区域宽度
- 参数 : h {int} 裁剪区域高度
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.7


```javascript
//设置版本
$ocr.v("mlkit");
//获取图片对象
var img = $img.read("t01.png");
//识别范围中的图片、拿到文本
var txt = $ocr.line(img,660,350,100,32);
log(txt);
//释放资源
img.recycle();
```


### detect(options)

> 识别当前屏幕指定区域，返回包含文字和位置的结果对象。
> 
> 输入类型为 Object，使用普通脚本对象填写 OcrOptions 的配置键。先取得截屏权限，再确保识别区域在截图范围内。
> 范围四个数依次为左上角横坐标、纵坐标、宽、高，单位像素；下例只是示范，需要按实际画面修改。
> 灰度模式把图片转成灰度后识别；二值化模式按文字颜色和阈值筛选像素。不同画面应选择合适方式，不保证哪种总是更快或更准。
> 不要在同一配置中混用同一选项的中英文键；字段优先级详见 OcrOptions。
> 返回类型为 DetectResult。先检查对象非空，再调用 isSuccess() 判断成功与否；getData() 返回 List<DetectResultItem>，是 Java 列表。
> 每个 DetectResultItem 可以用 getWord() 读取文字，用坐标读取方法获取位置；列表用 size() 和 get() 遍历。
> 配置无法转换时可能返回 null；获取截图失败等情况也可能返回表示失败的结果对象，不能只检查非空就当作成功。
> 配置转换、图像处理或识别过程可能抛出异常，示例使用异常处理记录原因。

- 参数 : options {Object} 可转换成 OcrOptions 的配置对象
- 返回 : {DetectResult} 识别结果对象；可能为 null，也可能表示失败
- 版本 : 1.0.0


```javascript
// 提前取得截屏权限；把范围改为实际文字所在区域。
var options = {
    region: [0, 0, 300, 100],
    gray: true, // 本例选择灰度处理。
    save: false // 示例不向设备保存图片。
};
try {
    var result = $ocr.detect(options);
    if (result != null && result.isSuccess()) {
        var items = result.getData(); // 取得文字条目列表。
        if (items != null) {
            for (var index = 0; index < items.size(); index++) {
                var item = items.get(index);
                log(item.getWord()); // 读取一个条目的文字。
                log("中心位置：" + item.getCx() + "," + item.getCy());
            }
        }
    } else {
        log("识别未成功，请检查截屏权限、区域和引擎。");
    }
} catch (error) {
    log("文字识别异常：" + error);
}
```


### detect64(base64)

> 识别一段 base64 编码的图片。

- 参数 : base64 {String} 图片的 base64 编码字符串
- 返回 : {DetectResult} 识别结果集，用 isSuccess() 判断成败，getData() 取每段文字和坐标
- 版本 : 1.0.0


```javascript
//先把图片转成 base64
var img = $img.read("/sdcard/test.png");
var base64 = $img.toBase64(img);
//再交给 OCR 识别
var result = $ocr.detect64(base64);
```


### detectPath(imgPath)

> 识别本地图片文件（按路径），返回完整识别结果集。

- 参数 : imgPath {String} 本地图片的绝对路径
- 返回 : {DetectResult} 识别结果集，用 isSuccess() 判断成败，getData() 取每段文字和坐标
- 版本 : 1.0.0


```javascript
//识别本地图片
var result = $ocr.detectPath("/sdcard/test.png");
```


### detectImg(img)

> 识别一个图片对象，返回完整识别结果集。

- 参数 : img {Image} 要识别的图片对象（由 $img.read 等获得）
- 返回 : {DetectResult} 识别结果集，用 isSuccess() 判断成败，getData() 取每段文字和坐标
- 版本 : 1.0.0


```javascript
//获取本地图片对象
var img = $img.read("/sdcard/test.png");
//识别图片对象
var result = $ocr.detectImg(img);
if (result.isSuccess()) {
    //...
}
```


### detectBitmap(bitmap)

> 识别一个 Bitmap 位图，返回完整识别结果集。

- 参数 : bitmap {Bitmap} 要识别的 Bitmap 位图
- 返回 : {DetectResult} 识别结果集，用 isSuccess() 判断成败，getData() 取每段文字和坐标
- 版本 : 1.7.0


```javascript
//获取一个位图对象
var img = $img.read("/sdcard/t01.png");
var bitmap = img.getBitmap();
//识别本地图片
var result = $ocr.detectBitmap(bitmap);
```


### onlyRec(image)

> 只识别图片里的文字内容，不返回坐标。
> 
> 跳过文字位置检测，速度更快；适合已经把图片裁到只剩一个字或一小段文字时用。
> 
> 注意：传入的图片应当只含单一文字，图片太大或内容复杂可能识别异常。
> 返回识别出的文字字符串。

- 参数 : image {Image} 要识别的图片对象
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//获取本地图片对象
var img = $img.read("/sdcard/test.png");
//识别图片对象
var word = $ocr.onlyRec(img);
log(word);
```


### onlyRec(bitmap)

> 只识别位图里的文字内容，不返回坐标。
> 
> 跳过文字位置检测，速度更快。
> 
> 注意：传入的位图应当只含单一文字，图片太大或内容复杂可能识别异常。
> 返回识别出的文字字符串。

- 参数 : bitmap {Bitmap} 要识别的 Bitmap 位图
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//获取本地图片对象
var img = $img.read("/sdcard/test.png");
//获取位图对象
var bitmap = img.getBitmap();
//识别位图对象
var word = $ocr.onlyRec(bitmap);
log(word);
```


### onlyRec(path)

> 只识别路径上图片里的文字内容，不返回坐标。
> 
> 直接传入图片路径，内部会读图后识别。
> 
> 注意：图片应当只含单一文字，太大或内容复杂可能异常。
> 返回识别出的文字字符串。

- 参数 : path {String} 本地图片的绝对路径
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//识别路径上的图片
var word = $ocr.onlyRec("/sdcard/test.png");
log(word);
```


### onlyDet(image)

> 只检测图片里文字的位置，不识别具体是什么字。
> 
> 只做文字位置框选，不做内容识别，速度很快。
> 
> 允许传入整屏大图，返回每段文字的坐标框。
> 适合先定位文字位置、再做后续动作的场景。

- 参数 : image {Image} 要识别的图片对象
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//获取本地图片对象
var img = $img.read("/sdcard/test.png");
//识别图片对象
var result = $ocr.onlyDet(img);
log(result);
```


### onlyDet(bitmap)

> 只检测位图里文字的位置，不识别具体是什么字。
> 
> 只做文字位置框选，不做内容识别，速度很快。
> 
> 允许传入较大的位图，返回每段文字的坐标框。

- 参数 : bitmap {Bitmap} 要识别的 Bitmap 位图
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//获取本地图片对象
var img = $img.read("/sdcard/test.png");
//获取位图对象
var bitmap = img.getBitmap();
//识别位图对象
var result = $ocr.onlyDet(bitmap);
log(result);
```


### onlyDet(path)

> 只检测路径上图片里文字的位置，不识别具体是什么字。
> 
> 直接传入图片路径，内部读图后只做位置检测。
> 
> 速度很快，返回每段文字的坐标框。

- 参数 : path {String} 本地图片的绝对路径
- 返回 : {String} 识别出的文字字符串；失败或无内容返回空串/null
- 版本 : 1.9.6


```javascript
//识别路径上的图片
var result = $ocr.onlyDet("/sdcard/test.png");
log(result);
```


