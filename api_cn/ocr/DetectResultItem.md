# 

- 更新时间:2026-10-22 10:56:19

> 一条文字识别记录，脚本类型名为 DetectResultItem。
> 
> 从 DetectResult.getData() 返回的 Java 列表中取出条目，再读取文字、角点、中心、宽高和评分。
> 各字段独立保存，不会因改动某个角点而自动重算中心或宽高。新建对象只是空数据容器，不会启动识别。
> 评分来源依赖引擎，有的实现使用固定值，不能简单当作文字正确概率。



```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            log(item.getWord()); // 读取文字内容。
            log("中心：" + item.getCx() + "," + item.getCy());
            log("宽高：" + item.getW() + " × " + item.getH());
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```




### const {float} x1;

> 保存第1个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.x1; // 读取第一条文字的这项信息。
            log("第1个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} y1;

> 保存第1个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.y1; // 读取第一条文字的这项信息。
            log("第1个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} x2;

> 保存第2个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.x2; // 读取第一条文字的这项信息。
            log("第2个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} y2;

> 保存第2个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.y2; // 读取第一条文字的这项信息。
            log("第2个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} x3;

> 保存第3个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.x3; // 读取第一条文字的这项信息。
            log("第3个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} y3;

> 保存第3个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.y3; // 读取第一条文字的这项信息。
            log("第3个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} x4;

> 保存第4个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.x4; // 读取第一条文字的这项信息。
            log("第4个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} y4;

> 保存第4个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.y4; // 读取第一条文字的这项信息。
            log("第4个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} cx;

> 保存中心横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心横向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.cx; // 读取第一条文字的这项信息。
            log("中心横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} cy;

> 保存中心纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心纵向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.cy; // 读取第一条文字的这项信息。
            log("中心纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} w;

> 保存文字区域宽度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的宽度，不是右侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.w; // 读取第一条文字的这项信息。
            log("文字区域宽度：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} h;

> 保存文字区域高度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的高度，不是下侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.h; // 读取第一条文字的这项信息。
            log("文字区域高度：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {String} word;

> 保存识别文字。
> 
> 类型为 String（字符串）。字符串，可能为 null 或空字符串。一个条目可能是一行、一块或一个词，具体划分由引擎决定。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该字符串为 null。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.word; // 读取第一条文字的这项信息。
            log("识别文字：" + value);
            if (value == null || String(value).length === 0) {
                log("该条目没有提供文字内容。");
            }
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### const {float} similar;

> 保存识别评分。
> 
> 类型为 float（单精度浮点数）。单精度浮点数，含义由识别引擎决定。本项目的部分识别实现填入固定的 0.85，不能一律解释为真实的正确概率，也不能只凭它断定文字一定正确。
> 这是公开字段，可以直接读取或赋值；修改它不会自动同步其他字段。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.similar; // 读取第一条文字的这项信息。
            log("识别评分：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### getX1()

> 读取第1个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第1个角点的横坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getX1(); // 读取第一条文字的这项信息。
            log("第1个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setX1(x1)

> 设置第1个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 x1 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : x1 {float} 要保存的第1个角点的横坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setX1(100.5); // 写入演示值。
log(item.getX1()); // 通过读取方法检查设置结果。
```


### getY1()

> 读取第1个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第1个角点的纵坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getY1(); // 读取第一条文字的这项信息。
            log("第1个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setY1(y1)

> 设置第1个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 y1 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : y1 {float} 要保存的第1个角点的纵坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setY1(100.5); // 写入演示值。
log(item.getY1()); // 通过读取方法检查设置结果。
```


### getX2()

> 读取第2个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第2个角点的横坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getX2(); // 读取第一条文字的这项信息。
            log("第2个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setX2(x2)

> 设置第2个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 x2 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : x2 {float} 要保存的第2个角点的横坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setX2(100.5); // 写入演示值。
log(item.getX2()); // 通过读取方法检查设置结果。
```


### getY2()

> 读取第2个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第2个角点的纵坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getY2(); // 读取第一条文字的这项信息。
            log("第2个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setY2(y2)

> 设置第2个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 y2 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : y2 {float} 要保存的第2个角点的纵坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setY2(100.5); // 写入演示值。
log(item.getY2()); // 通过读取方法检查设置结果。
```


### getX3()

> 读取第3个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第3个角点的横坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getX3(); // 读取第一条文字的这项信息。
            log("第3个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setX3(x3)

> 设置第3个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 x3 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : x3 {float} 要保存的第3个角点的横坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setX3(100.5); // 写入演示值。
log(item.getX3()); // 通过读取方法检查设置结果。
```


### getY3()

> 读取第3个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第3个角点的纵坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getY3(); // 读取第一条文字的这项信息。
            log("第3个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setY3(y3)

> 设置第3个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 y3 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : y3 {float} 要保存的第3个角点的纵坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setY3(100.5); // 写入演示值。
log(item.getY3()); // 通过读取方法检查设置结果。
```


### getX4()

> 读取第4个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第4个角点的横坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getX4(); // 读取第一条文字的这项信息。
            log("第4个角点的横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setX4(x4)

> 设置第4个角点的横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 x4 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : x4 {float} 要保存的第4个角点的横坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setX4(100.5); // 写入演示值。
log(item.getX4()); // 通过读取方法检查设置结果。
```


### getY4()

> 读取第4个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的第4个角点的纵坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getY4(); // 读取第一条文字的这项信息。
            log("第4个角点的纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setY4(y4)

> 设置第4个角点的纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数。角点顺序由识别引擎填入；不要仅凭编号就假设所有引擎都使用相同方向。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 y4 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : y4 {float} 要保存的第4个角点的纵坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setY4(100.5); // 写入演示值。
log(item.getY4()); // 通过读取方法检查设置结果。
```


### getCx()

> 读取中心横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心横向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的中心横坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getCx(); // 读取第一条文字的这项信息。
            log("中心横坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setCx(cx)

> 设置中心横坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心横向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 cx 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : cx {float} 要保存的中心横坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setCx(150.5); // 写入演示值。
log(item.getCx()); // 通过读取方法检查设置结果。
```


### getCy()

> 读取中心纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心纵向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的中心纵坐标


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getCy(); // 读取第一条文字的这项信息。
            log("中心纵坐标：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setCy(cy)

> 设置中心纵坐标。
> 
> 类型为 float（单精度浮点数）。单位为像素，表示结果中保存的中心纵向位置。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 cy 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : cy {float} 要保存的中心纵坐标，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setCy(80.5); // 写入演示值。
log(item.getCy()); // 通过读取方法检查设置结果。
```


### getW()

> 读取文字区域宽度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的宽度，不是右侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的文字区域宽度


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getW(); // 读取第一条文字的这项信息。
            log("文字区域宽度：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setW(w)

> 设置文字区域宽度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的宽度，不是右侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 w 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : w {float} 要保存的文字区域宽度，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setW(100); // 写入演示值。
log(item.getW()); // 通过读取方法检查设置结果。
```


### getH()

> 读取文字区域高度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的高度，不是下侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的文字区域高度


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getH(); // 读取第一条文字的这项信息。
            log("文字区域高度：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setH(h)

> 设置文字区域高度。
> 
> 类型为 float（单精度浮点数）。单位为像素，可包含小数；这是保存的高度，不是下侧坐标。
> 坐标以所属图像为参照；屏幕区域识别可能已由调用入口加回区域偏移。请确认来源，不要重复加偏移或直接把图片坐标当成设备点击坐标。
> 输入 h 类型为 float；输出类型为 void，没有返回值。
> 只修改当前字段，不会重算角点、中心或宽高，也不会重新识别图片。多个几何字段需要调用方自己保持一致。

- 参数 : h {float} 要保存的文字区域高度，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setH(30); // 写入演示值。
log(item.getH()); // 通过读取方法检查设置结果。
```


### getWord()

> 读取识别文字。
> 
> 类型为 String（字符串）。字符串，可能为 null 或空字符串。一个条目可能是一行、一块或一个词，具体划分由引擎决定。
> 输入参数：无；返回类型为 String，只读取当前保存值，不会重新识别。
> 新建条目时该字符串为 null。

- 返回 : {String} 当前保存的识别文字，可能为 null


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getWord(); // 读取第一条文字的这项信息。
            log("识别文字：" + value);
            if (value == null || String(value).length === 0) {
                log("该条目没有提供文字内容。");
            }
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setWord(word)

> 设置识别文字。
> 
> 类型为 String（字符串）。字符串，可能为 null 或空字符串。一个条目可能是一行、一块或一个词，具体划分由引擎决定。
> 输入 word 类型为 String；输出类型为 void，没有返回值。
> 只修改这份结果数据，不会修改真实图片、重新识别或改变结果容器的成功标记。

- 参数 : word {String} 要保存的识别文字，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setWord("教学文字"); // 写入演示值。
log(item.getWord()); // 通过读取方法检查设置结果。
```


### getSimilar()

> 读取识别评分。
> 
> 类型为 float（单精度浮点数）。单精度浮点数，含义由识别引擎决定。本项目的部分识别实现填入固定的 0.85，不能一律解释为真实的正确概率，也不能只凭它断定文字一定正确。
> 输入参数：无；返回类型为 float，只读取当前保存值，不会重新识别。
> 新建条目时该数值为零，零不代表已经得到有效识别结果。

- 返回 : {float} 当前保存的识别评分


```javascript
// 请替换成真实存在且当前脚本有权读取的文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null && result.isSuccess()) {
    var items = result.getData(); // Java 列表，需要检查数量。
    if (items != null && items.size() > 0) {
        var item = items.get(0); // 第一条文字，序号是零。
        if (item != null) {
            var value = item.getSimilar(); // 读取第一条文字的这项信息。
            log("识别评分：" + value);
        }
    }
} else {
    log("未取得成功的识别结果，请检查图片和识别配置。");
}
```


### setSimilar(similar)

> 设置识别评分。
> 
> 类型为 float（单精度浮点数）。单精度浮点数，含义由识别引擎决定。本项目的部分识别实现填入固定的 0.85，不能一律解释为真实的正确概率，也不能只凭它断定文字一定正确。
> 输入 similar 类型为 float；输出类型为 void，没有返回值。
> 只修改这份结果数据，不会修改真实图片、重新识别或改变结果容器的成功标记。

- 参数 : similar {float} 要保存的识别评分，只影响当前字段


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setSimilar(0.85); // 写入演示值。
log(item.getSimilar()); // 通过读取方法检查设置结果。
```


### json()

> 读取这条识别结果的文本表达。
> 
> 输入参数：无；返回类型为 String。本方法直接拼接各字段。
> 当前实现没有规范转义文字中的引号、反斜杠和换行，不能保证输出总能通过 JSON.parse 解析。
> 请将此输出用于观察数据，不要把它当作任意文字均适用的通用序列化方法。

- 返回 : {String} 当前条目的文本表达，特殊字符可能导致其不符合标准数据格式


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setWord("教学文字");
log(item.json()); // 查看字段的文本表达。
```


### toString()

> 读取这条识别结果的文本表达。
> 
> 输入参数：无；返回类型为 String。本方法直接调用 json()。
> 当前实现没有规范转义文字中的引号、反斜杠和换行，不能保证输出总能通过 JSON.parse 解析。
> 请将此输出用于观察数据，不要把它当作任意文字均适用的通用序列化方法。

- 返回 : {String} 当前条目的文本表达，特殊字符可能导致其不符合标准数据格式


```javascript
// 新建教学条目，不会运行识别或修改图片。
var item = new DetectResultItem();
item.setWord("教学文字");
log(item.toString()); // 查看字段的文本表达。
```


