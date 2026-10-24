# Image - 图片

- 更新时间:2026-10-22 10:55:50

> 封装图片数据的对象，可读取尺寸、像素并保存或复制图片。
> 
> 通过 $img.read 读取文件可得到本对象；读取可能返回 null，也可能得到内部位图为空的对象，因此使用前要检查。
> 公开宽高字段只是保存的数据；修改字段不会缩放位图。关闭图片后这些数字也不会自动清零。
> 底层位图引用由 getBitmap 返回，直接取得它不会复制。真正独立复制应调用 copy，复制结果也需要单独释放。
> 下面演示读取文件和尺寸；文件应事先存在且可读取。手动管理的图片用完应关闭，不能假设每个接口都自动回收。



```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 换成已有图片路径。
if (image != null) {
    try {
        var bitmap = image.getBitmap(); // 确认底层位图存在且仍可使用。
        if (bitmap != null && !bitmap.isRecycled()) {
            log(image.getWidth() + " x " + image.getHeight()); // 读取保存的尺寸。
        }
    } finally {
        image.close(); // 本例使用结束后释放。
    }
}
```




### const {int} width;

> 保存图片宽度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 这个公开字段可以被修改，但不建议把它当成缩放设置。脚本优先用明确的取值方法，避免同名字段与方法造成混淆。


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.getWidth()); // 使用取值方法读取保存尺寸。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### const {int} height;

> 保存图片高度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 这个公开字段可以被修改，但不建议把它当成缩放设置。脚本优先用明确的取值方法，避免同名字段与方法造成混淆。


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.getHeight()); // 使用取值方法读取保存尺寸。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### getBitmap()

> 取得内部位图引用。
> 
> 没有输入参数，返回 Android Bitmap 对象，可能为 null；这是原对象的引用，不是复制品。
> 位图可以通过 getWidth、getHeight 等系统方法读取实际尺寸，系统方法保留英文名称。
> 对共享位图执行回收会影响所有持有者；本图片关闭后，不应继续使用此前取得的引用。

- 返回 : {Bitmap} 内部位图引用，可能为 null


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        var bitmap = image.getBitmap(); // 取得原位图。
        if (bitmap != null && !bitmap.isRecycled()) {
            log(bitmap.getWidth() + " x " + bitmap.getHeight()); // 读取底层实际尺寸。
        }
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### width()

> 读取保存的图片宽度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 没有输入参数，返回 int。此方法读取英文 width 字段，即使方法名为中文也不读取单独的中文字段。

- 返回 : {int} 当前保存的宽度，单位像素


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.width()); // 读取当前保存的宽度。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### height()

> 读取保存的图片高度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 没有输入参数，返回 int。此方法读取英文 height 字段，即使方法名为中文也不读取单独的中文字段。

- 返回 : {int} 当前保存的高度，单位像素


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.height()); // 读取当前保存的高度。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### getWidth()

> 读取保存的图片宽度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 没有输入参数，返回 int。此方法读取英文 width 字段，即使方法名为中文也不读取单独的中文字段。

- 返回 : {int} 当前保存的宽度，单位像素


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.getWidth()); // 读取当前保存的宽度。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### getHeight()

> 读取保存的图片高度。
> 
> 类型为 int（整数），单位像素；它是对象保存的尺寸，不会每次重新读取底层位图。
> 英文和中文字段是独立存储。一般读图构造时填入相同值，但直接修改其中一份不会同步另一份，也不会缩放真正的图片。
> 以 Image 对象构造 Image 时，当前构造方法只共享位图，没有填入原图宽高；这种对象的保存尺寸可能为零。
> 关闭图片不会清零尺寸；判断图片能否使用，应另行检查位图引用和回收状态。
> 没有输入参数，返回 int。此方法读取英文 height 字段，即使方法名为中文也不读取单独的中文字段。

- 返回 : {int} 当前保存的高度，单位像素


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        log(image.getHeight()); // 读取当前保存的高度。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### close()

> 释放这张图片持有的位图资源。
> 
> 没有输入参数，返回 void，无返回值。四种关闭或释放名称最终调用相同实现。
> 内部会尝试回收尚未回收的位图，然后把本对象的位图引用设为 null；再次调用不重复处理空引用。
> 宽高字段不会被清零。如果其他对象共享同一位图，它们也会受到回收影响；确认都不再使用后再释放。

- 返回 : {void} 无返回值


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    image.close(); // 此例读取后立即释放，仅用于演示。
    // 之后不要再读取像素或使用此前取得的位图引用。
}
```


### recycle()

> 释放这张图片持有的位图资源。
> 
> 没有输入参数，返回 void，无返回值。四种关闭或释放名称最终调用相同实现。
> 内部会尝试回收尚未回收的位图，然后把本对象的位图引用设为 null；再次调用不重复处理空引用。
> 宽高字段不会被清零。如果其他对象共享同一位图，它们也会受到回收影响；确认都不再使用后再释放。

- 返回 : {void} 无返回值


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    image.recycle(); // 此例读取后立即释放，仅用于演示。
    // 之后不要再读取像素或使用此前取得的位图引用。
}
```


### pixel(x, y)

> 读取图片内指定位置的像素颜色。
> 
> 输入为 两个 int 整数，分别表示横坐标和纵坐标。
> 返回类型为 Integer（颜色整数），其中包含透明度和红绿蓝分量，不是颜色名称或十六进制文字。
> 内部位图引用为空时返回 null；坐标越界、底层位图被其他对象回收等情况可能抛出异常，本方法不会统一转成 null。
> 坐标从零开始：(0, 0) 是第一列第一行，(1, 1) 是第二列第二行。横坐标必须小于实际位图宽度，纵坐标必须小于实际位图高度。
> 图片公开的宽高字段可以被手动改动；需要验证边界时，应以仍可使用的底层位图尺寸为准。
> 下例读取已有图片的左上角；文件路径须事先存在且可读取，最后释放图片资源。

- 参数 : x {int} 从零开始的横坐标
- 参数 : y {int} 从零开始的纵坐标
- 返回 : {Integer} 像素颜色整数；内部位图引用为空时为 null


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 换成真实图片路径。
if (image != null) {
    try {
        var bitmap = image.getBitmap(); // 得到内部位图引用，用于检查状态。
        if (bitmap != null && !bitmap.isRecycled() && bitmap.getWidth() > 0 && bitmap.getHeight() > 0) {
            var color = image.pixel(0, 0); // 读取第一列第一行。
            if (color != null) { log(color); } // 检查返回值后使用。
        }
    } finally {
        image.close(); // 用完后释放，不再访问此前取得的位图引用。
    }
}
```


### pixel(point)

> 读取图片内指定位置的像素颜色。
> 
> 输入为 Point 点对象，使用其 x、y 两个整数成员；不能传 null。
> 返回类型为 Integer（颜色整数），其中包含透明度和红绿蓝分量，不是颜色名称或十六进制文字。
> 内部位图引用为空时返回 null；坐标越界、底层位图被其他对象回收等情况可能抛出异常，本方法不会统一转成 null。
> 坐标从零开始：(0, 0) 是第一列第一行，(1, 1) 是第二列第二行。横坐标必须小于实际位图宽度，纵坐标必须小于实际位图高度。
> Point 使用图片内部坐标，不能直接把另一张裁剪图片或屏幕上的坐标拿来读取。
> 下例读取已有图片的左上角；文件路径须事先存在且可读取，最后释放图片资源。

- 参数 : point {Point} 图片内部的坐标点，不能为 null
- 返回 : {Integer} 像素颜色整数；内部位图引用为空时为 null


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 换成真实图片路径。
if (image != null) {
    try {
        var bitmap = image.getBitmap(); // 得到内部位图引用，用于检查状态。
        if (bitmap != null && !bitmap.isRecycled() && bitmap.getWidth() > 0 && bitmap.getHeight() > 0) {
            var point = new Point(0, 0); // 创建图片内部的点对象。
            log(point.x + "," + point.y); // 先检查传入点的两个成员。
            var color = image.pixel(point); // 读取第一列第一行。
            if (color != null) { log(color); } // 检查返回值后使用。
        }
    } finally {
        image.close(); // 用完后释放，不再访问此前取得的位图引用。
    }
}
```


### save(path)

> 把当前图片按 PNG 格式保存到文件。
> 
> 输入为 String（文件路径），返回 void，不返回成功标志或实际保存路径。
> 已有同名文件时先生成未占用的路径，再尝试保存；应保证目标目录和写入权限可用。
> 实现捕获保存过程抛出的异常并记录日志；方法正常返回并不能证明文件保存成功，需另外检查文件。

- 参数 : path {String} 目标文件路径，建议使用 .png 扩展名
- 返回 : {void} 无返回值，不表示保存是否成功


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        image.save("/sdcard/Pictures/sample_copy.png"); // 保存到另一个路径，实际名称可能调整。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### show()

> 把当前图片交给界面线程显示。
> 
> 没有输入参数，返回 void。仅在位图引用存在且尚未回收时请求显示；否则不执行显示操作。
> 返回不代表用户已经看完图片。显示时仍然使用该位图，请在界面不再使用图片后才回收。

- 返回 : {void} 无返回值


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    image.show(); // 请求显示，不是等待对话框关闭。
    // 确认显示界面不再使用此图片后，再调用 image.close()。
}
```


### copy()

> 复制底层像素，创建独立的图片对象。
> 
> 没有输入参数，返回 Image。内部位图引用为空时返回 null；其他失败情况可能抛出异常，并不是所有失败都返回 null。
> 使用可修改的 ARGB_8888 格式复制像素，占用额外内存。复制出的位图与原位图独立，两张图片需要分别释放。
> 此方法与直接用 Image 构造 Image 不同，后者共享位图。

- 返回 : {Image} 独立图片对象；原位图引用为空时返回 null


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        var copied = image.copy(); // 得到新 Image 对象，可能为 null。
        if (copied != null) {
            try {
                log(copied.getWidth() + " x " + copied.getHeight()); // 继续读取返回对象的成员。
            } finally {
                copied.close(); // 单独释放副本。
            }
        }
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### base64()

> 把图片编码成 Base64 文本。
> 
> 没有输入参数，返回 String（字符串），不是图片对象。当前工具先按 PNG 格式编码，再转为 Base64 文字。
> 位图为空、已经回收或编码时捕获到异常会返回 null。编码会额外占用内存，大图不要在循环中反复转换。

- 返回 : {String} Base64 图片文本，失败时可能为 null


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        var text = image.base64(); // 得到编码文字或 null。
        if (text != null) {
            log(String(text).length); // 先转成脚本文字，再读取字符数量。
        } else {
            log("图片无法编码");
        }
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


### json()

> 使用通用 JSON 工具序列化此图片对象。
> 
> 没有输入参数，返回 String（字符串）。这不是图片文件编码，也不能代替 base64 保存像素。
> 实现将整个对象交给 JsonUtil，包含字段如何处理由序列化工具决定；不要假设输出永远只含宽高。
> 如果只需稳定的尺寸信息，可以自行构造只含宽高的脚本对象再 JSON.stringify。

- 返回 : {String} 通用序列化工具生成的文本


```javascript
var image = $img.read("/sdcard/Pictures/sample.png"); // 请换成可读取的真实图片路径。
if (image != null) {
    try {
        var info = {width: image.getWidth(), height: image.getHeight()}; // 明确选择需要的字段。
        log(JSON.stringify(info)); // 输出自己定义的尺寸结构。
        log(image.json()); // 再查看本方法的通用序列化结果。
    } finally {
        image.close(); // 本例使用结束后释放原图片。
    }
}
```


