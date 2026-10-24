# QrOptions - 制作二维码配置

- 更新时间:2026-10-22 10:55:50

> 二维码制作配置对象。
> 
> 先新建对象，再填写需要改变的选项，最后传给 $qr.make 或 $二维码.制作。
> 中英文配置是独立字段：中文值不为 null 时优先，否则使用英文字段。建议同一份配置统一采用一种语言。



```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```

```javascript
// 新建配置，每次示例都使用独立对象。
var 配置 = new QrOptions();
// 制作成功后得到图像对象，失败时可能为空。
var 图片 = $二维码.制作("教学示例", 配置);
if (图片 != null) {
    try {
        日志("宽度：" + 图片.获取宽度());
        日志("高度：" + 图片.获取高度());
    } finally {
        图片.回收(); // 不再使用后释放图片占用的内存。
    }
} else {
    日志("制作失败，请检查设备版本和配置值。");
}
```




### const {Integer} w;

> 输出图片宽度的英文配置字段。
> 
> 类型为 Integer（可为空的整数）。
> 此字段默认是 500。
> 中文字段 宽 不为 null 时优先使用中文值，否则使用 w；给其中一个字段赋值不会同步另一个。
> 单位是像素，请填写正整数。内容多时需要更大的图片，不要用过小尺寸；创建失败时制作方法可能返回空值。
> 修改配置只影响随后制作的图片，不会改变已经生成的图片。


```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
options.w = 600; // 设置本次要演示的选项。
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```


### const {Integer} h;

> 输出图片高度的英文配置字段。
> 
> 类型为 Integer（可为空的整数）。
> 此字段默认是 500。
> 中文字段 高 不为 null 时优先使用中文值，否则使用 h；给其中一个字段赋值不会同步另一个。
> 单位是像素，请填写正整数。建议宽高相等，让二维码呈正方形；大尺寸会占用更多内存。
> 修改配置只影响随后制作的图片，不会改变已经生成的图片。


```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
options.h = 600; // 设置本次要演示的选项。
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```


### const {Integer} margin;

> 二维码周围的留白的英文配置字段。
> 
> 类型为 Integer（可为空的整数）。
> 此字段默认是 2。
> 中文字段 边距 不为 null 时优先使用中文值，否则使用 margin；给其中一个字段赋值不会同步另一个。
> 填写非负整数。这个值作为二维码编码器的留白参数传入，不应理解为固定的输出图片像素数；实际留白会随图案缩放。
> 修改配置只影响随后制作的图片，不会改变已经生成的图片。


```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
options.margin = 4; // 设置本次要演示的选项。
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```


### const {String} foreColor;

> 二维码图案颜色的英文配置字段。
> 
> 类型为 String（字符串）。
> 此字段默认是 "#000000"。
> 中文字段 前景色 不为 null 时优先使用中文值，否则使用 foreColor；给其中一个字段赋值不会同步另一个。
> 填写颜色字符串，例如 #000000 表示黑色。颜色由安卓颜色解析器处理；无效字符串可能使制作失败。建议使用深色图案和浅色背景。
> 修改配置只影响随后制作的图片，不会改变已经生成的图片。


```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
options.foreColor = "#000000"; // 设置本次要演示的选项。
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```


### const {String} bgColor;

> 二维码背景颜色的英文配置字段。
> 
> 类型为 String（字符串）。
> 此字段默认是 "#FFFFFF"。
> 中文字段 背景色 不为 null 时优先使用中文值，否则使用 bgColor；给其中一个字段赋值不会同步另一个。
> 填写颜色字符串，例如 #FFFFFF 表示白色。请与前景色保持明显差异，避免图案和背景同色而难以识别。
> 修改配置只影响随后制作的图片，不会改变已经生成的图片。


```javascript
// 新建配置，每次示例都使用独立对象。
var options = new QrOptions();
options.bgColor = "#FFFFFF"; // 设置本次要演示的选项。
// 制作成功后得到图像对象，失败时可能为空。
var image = $qr.make("教学示例", options);
if (image != null) {
    try {
        log("宽度：" + image.getWidth());
        log("高度：" + image.getHeight());
    } finally {
        image.recycle(); // 不再使用后释放图片占用的内存。
    }
} else {
    log("制作失败，请检查设备版本和配置值。");
}
```


