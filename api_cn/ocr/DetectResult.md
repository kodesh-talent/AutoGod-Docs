# 

- 更新时间:2026-10-22 10:56:19

> 一次文字识别的结果容器，脚本类型名为 DetectResult。
> 
> 先检查结果非空，再检查 isSuccess()；成功后从 getData() 取得 Java 列表，逐项读取 DetectResultItem。
> 状态、说明、错误和列表独立保存；修改其中一项不会自动改变其他项。结果内容反映识别时的画面，不会实时更新。



```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    if (result.isSuccess()) {
        var items = result.getData(); // Java 列表，不是脚本数组。
        if (items != null) {
            for (var index = 0; index < items.size(); index++) {
                var item = items.get(index);
                if (item != null) {
                    log(item.getWord()); // 从关联的文字条目读取内容。
                }
            }
        }
    } else {
        log(result.getDes());
        log(result.getErr());
    }
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```




### const {boolean} success;

> 识别成功标记，类型为 boolean（布尔值），新对象默认 false。
> 
> 它是独立保存的状态值；true 不保证列表非空，也不保证文字绝对正确。直接赋值不会启动识别或改变其他字段。


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    log("成功标记：" + result.success);
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### const {String} des;

> 结果说明，类型为 String（字符串），新对象默认“处理失败”。
> 
> 这是提示信息，不保证所有引擎都返回中文，也不保证非空；判断成功请用 isSuccess()。


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    log("结果说明：" + result.des);
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### const {List<DetectResultItem>} data;

> 文字条目列表，类型为 List<DetectResultItem>。构造时创建空列表，之后允许被替换成其他列表或 null。
> 
> 列表及条目均为直接引用，修改它们会影响当前结果；条目划分由识别引擎决定，不一定一个字符对应一项。


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    var items = result.getData(); // Java 列表，不是脚本数组。
    if (items != null) {
        for (var index = 0; index < items.size(); index++) {
            var item = items.get(index);
            if (item != null) {
                log(item.getWord()); // 从关联的文字条目读取内容。
            }
        }
    }
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### const {String} err;

> 错误说明，类型为 String（字符串），新对象默认“暂无异常”。
> 
> 字段可以被赋成 null；没有详细错误文字也不等于识别成功，应同时检查 success 和 des。


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    log("错误说明：" + result.err);
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### isSuccess()

> 读取成功标记。输入参数：无；返回类型为 boolean，即 true 或 false。
> 
> 只返回 success 当前保存的值，不会检查列表是否有文字或重新运行识别。

- 返回 : {boolean} 当前字段值或文本表达，详见说明


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    if (result.isSuccess()) {
        var items = result.getData(); // Java 列表，不是脚本数组。
        if (items != null) {
            for (var index = 0; index < items.size(); index++) {
                var item = items.get(index);
                if (item != null) {
                    log(item.getWord()); // 从关联的文字条目读取内容。
                }
            }
        }
    } else {
        log(result.getDes());
        log(result.getErr());
    }
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### setSuccess(success)

> 设置对象保存的成功标记。输入 success 类型为 boolean；输出类型为 void，没有返回值。
> 
> 只修改 success 字段，不会重新识别、创建文字条目或同步其他状态。

- 参数 : success {boolean} 写入当前字段的新值


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
result.setSuccess(true); // 仅修改教学对象。
log(result.isSuccess()); // 检查刚设置的值。
```


### getDes()

> 读取结果说明。输入参数：无；返回类型为 String，可能为 null。
> 
> 只读取 des 字段；说明文字不代替成功状态判断。

- 返回 : {String} 当前字段值或文本表达，详见说明


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    log(result.getDes()); // 读取本次识别的提示信息。
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### getErr()

> 读取错误说明。输入参数：无；返回类型为 String，可能为 null。
> 
> 只读取 err 字段，不会抛出或清除错误；新对象的默认值为“暂无异常”。

- 返回 : {String} 当前字段值或文本表达，详见说明


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    log(result.getErr()); // 查看对象保存的错误文字。
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### setErr(err)

> 设置对象保存的错误文字。输入 err 类型为 String；输出类型为 void，没有返回值。
> 
> 只修改 err 字段，不会重新识别、创建文字条目或同步其他状态。字符串可为 null。

- 参数 : err {String} 写入当前字段的新值


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
result.setErr("教学错误"); // 仅修改教学对象。
log(result.getErr()); // 检查刚设置的值。
```


### setDes(des)

> 设置对象保存的说明文字。输入 des 类型为 String；输出类型为 void，没有返回值。
> 
> 只修改 des 字段，不会重新识别、创建文字条目或同步其他状态。字符串可为 null。

- 参数 : des {String} 写入当前字段的新值


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
result.setDes("教学说明"); // 仅修改教学对象。
log(result.getDes()); // 检查刚设置的值。
```


### getData()

> 读取文字条目列表。输入参数：无；返回类型为 List<DetectResultItem>，可能为 null。
> 
> 返回原列表引用，不是副本。修改列表或其中的条目，会影响当前结果。读取第一项前应检查列表非空且 size() 大于零。

- 返回 : {List<DetectResultItem>} 当前字段值或文本表达，详见说明


```javascript
// 把路径改成当前脚本有权读取的真实文字图片。
var result = $ocr.detectPath("/sdcard/ocr.png");
if (result != null) {
    var items = result.getData(); // Java 列表，不是脚本数组。
    if (items != null) {
        for (var index = 0; index < items.size(); index++) {
            var item = items.get(index);
            if (item != null) {
                log(item.getWord()); // 从关联的文字条目读取内容。
            }
        }
    }
} else {
    log("没有取得识别结果，请检查图片路径和识别配置。");
}
```


### setData(data)

> 替换当前结果的文字列表。输入 data 类型为 List<DetectResultItem>；输出类型为 void，没有返回值。
> 
> 直接保存传入的 Java 列表引用，不复制列表，也不更新 success、des 或 err。传 null 后读取列表会得到 null。
> 下面同时演示创建关联条目、添加到 Java 列表和读取。

- 参数 : data {List<DetectResultItem>} 要保存的文字条目列表，可为 null


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
var item = new DetectResultItem(); // 构造一条演示文字。
item.setWord("教学文字");
var items = new java.util.ArrayList(); // 使用 Java 列表。
items.add(item);
result.setData(items);
var items = result.getData(); // Java 列表，不是脚本数组。
if (items != null) {
    for (var index = 0; index < items.size(); index++) {
        var item = items.get(index);
        if (item != null) {
            log(item.getWord()); // 从关联的文字条目读取内容。
        }
    }
}
item.setWord("修改后的教学文字"); // 列表中的同一对象也随之改变。
log(result.getData().get(0).getWord());
```


### json()

> 把当前对象拼接成结果文本。输入参数：无；返回类型为 String。
> 
> 当前实现直接拼接列表、状态和说明，没有对文字里的引号、反斜杠或换行进行规范转义。
> 输出仅适合查看，不能保证任意内容都可被 JSON.parse 解析；不要把此方法当作可靠的通用序列化器。

- 返回 : {String} 当前字段值或文本表达，详见说明


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
var item = new DetectResultItem(); // 构造一条演示文字。
item.setWord("教学文字");
var items = new java.util.ArrayList(); // 使用 Java 列表。
items.add(item);
result.setData(items);
log(result.json()); // 查看当前对象的文本表达。
```


### pushData(resultArr)

> 把文字条目数组追加到现有列表末尾。输入 resultArr 类型为 DetectResultItem[]；输出类型为 void，没有返回值。
> 
> 数组为 null 或长度为零时直接返回；不会清空原有条目，也不会更新成功标记。
> 追加的是条目引用，不复制对象，也不检查数组元素是否为 null。现有 data 必须非空且支持添加，否则会抛出异常。

- 参数 : resultArr {DetectResultItem[]} 要追加的文字条目数组，空数组不做任何操作


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
var item = new DetectResultItem();
item.setWord("追加的教学文字");
// 显式创建 Java 条目数组，避免把列表和数组混淆。
var entries = java.lang.reflect.Array.newInstance(DetectResultItem, 1);
entries[0] = item;
result.pushData(entries); // 追加一个条目。
var items = result.getData(); // Java 列表，不是脚本数组。
if (items != null) {
    for (var index = 0; index < items.size(); index++) {
        var item = items.get(index);
        if (item != null) {
            log(item.getWord()); // 从关联的文字条目读取内容。
        }
    }
}
```


### toString()

> 读取对象的文本表达。输入参数：无；返回类型为 String。
> 
> 内部直接调用 json()，同样不保证对特殊字符进行规范转义；打印对象不会运行识别或改变状态。

- 返回 : {String} 当前字段值或文本表达，详见说明


```javascript
// 新建教学数据，不会启动识别或修改真实图片。
var result = new DetectResult();
var item = new DetectResultItem(); // 构造一条演示文字。
item.setWord("教学文字");
var items = new java.util.ArrayList(); // 使用 Java 列表。
items.add(item);
result.setData(items);
log(result.toString()); // 输出与 json() 相同的表达。
```


