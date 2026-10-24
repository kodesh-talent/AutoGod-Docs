# 图片信息

- 更新时间:2026-10-22 10:55:48

> 图片的媒体库信息对象（ImageInfo）。
> 
> 通过 $file.lsImages() 取得 Java 列表，再用列表的 get 方法取出一个对象。
> 这里只保存查询时的资料，不会自动跟随文件变化；修改对象不会改写真实文件或系统媒体库。
> 时间是加入媒体库的秒数，大小是字节。查询按加入时间从新到旧排列，只包含当前可见的记录。
> 图片对象这里只描述尺寸和路径，不是用于绘图或识图的图像对象。
> 查询需要设备授予访问权限；无权限可能取得空列表，系统查询也可能抛出异常。



```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    log("名称：" + info.getName());
    log("路径：" + info.getPath());
    log("大小（字节）：" + info.getSize());
    // 日期对象接收毫秒，因此先把秒乘以一千。
    log(new Date(Number(info.getTime()) * 1000).toString());
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```




### const {long} id;

> 图片的编号记录。
> 
> 字段类型为 long（长整数；系统媒体库中这条记录的编号，不是列表下标）。
> 这是对象内部的私有字段，脚本请调用公开的 getId() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setId，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getId(); // 读取这一项资料。
    log("编号：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {String} name;

> 图片的名称记录。
> 
> 字段类型为 String（字符串；媒体库记录的显示名称，可能没有提供）。
> 这是对象内部的私有字段，脚本请调用公开的 getName() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setName，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getName(); // 读取这一项资料。
    log("名称：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {String} 名称;

> 图片的名称记录。
> 
> 字段类型为 String（字符串；媒体库记录的显示名称，可能没有提供）。
> 这是对象内部的私有字段，脚本请调用公开的 getName() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getName(); // 读取这一项资料。
    log("名称：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {long} size;

> 图片的大小记录。
> 
> 字段类型为 long（长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节）。
> 这是对象内部的私有字段，脚本请调用公开的 getSize() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setSize，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getSize(); // 读取这一项资料。
    log("大小：" + value);
    log("大小（二进制千字节）：" + Number(value) / 1024); // 按一千零二十四字节换算。
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {long} 大小;

> 图片的大小记录。
> 
> 字段类型为 long（长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节）。
> 这是对象内部的私有字段，脚本请调用公开的 getSize() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getSize(); // 读取这一项资料。
    log("大小：" + value);
    log("大小（二进制千字节）：" + Number(value) / 1024); // 按一千零二十四字节换算。
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {String} path;

> 图片的路径记录。
> 
> 字段类型为 String（字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件）。
> 这是对象内部的私有字段，脚本请调用公开的 getPath() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setPath，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getPath(); // 读取这一项资料。
    log("路径：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {String} 路径;

> 图片的路径记录。
> 
> 字段类型为 String（字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件）。
> 这是对象内部的私有字段，脚本请调用公开的 getPath() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getPath(); // 读取这一项资料。
    log("路径：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {long} time;

> 图片的时间记录。
> 
> 字段类型为 long（长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒）。
> 这是对象内部的私有字段，脚本请调用公开的 getTime() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setTime，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getTime(); // 读取这一项资料。
    log("时间：" + value);
    // 日期对象需要毫秒，媒体库时间却是秒，要先换算。
    log(new Date(Number(value) * 1000).toString());
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {long} 时间;

> 图片的时间记录。
> 
> 字段类型为 long（长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒）。
> 这是对象内部的私有字段，脚本请调用公开的 getTime() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getTime(); // 读取这一项资料。
    log("时间：" + value);
    // 日期对象需要毫秒，媒体库时间却是秒，要先换算。
    log(new Date(Number(value) * 1000).toString());
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {int} width;

> 图片的宽度记录。
> 
> 字段类型为 int（整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 这是对象内部的私有字段，脚本请调用公开的 getWidth() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setWidth，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getWidth(); // 读取这一项资料。
    log("宽度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {int} 宽;

> 图片的宽度记录。
> 
> 字段类型为 int（整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 这是对象内部的私有字段，脚本请调用公开的 getWidth() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getWidth(); // 读取这一项资料。
    log("宽度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {int} height;

> 图片的高度记录。
> 
> 字段类型为 int（整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 这是对象内部的私有字段，脚本请调用公开的 getHeight() 读取，不要直接访问此字段。
> 需要修改这份资料时使用 setHeight，该方法只改变内存中的信息。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getHeight(); // 读取这一项资料。
    log("高度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### const {int} 高;

> 图片的高度记录。
> 
> 字段类型为 int（整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 这是对象内部的私有字段，脚本请调用公开的 getHeight() 读取，不要直接访问此字段。
> 中文名称只是内部保存的另一份值；公开读取方法仍使用上面的英文名称。


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getHeight(); // 读取这一项资料。
    log("高度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getId()

> 读取这条图片信息的编号。
> 
> 输入参数：无。返回类型为 long（长整数；系统媒体库中这条记录的编号，不是列表下标）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {long} 长整数；系统媒体库中这条记录的编号，不是列表下标


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getId(); // 取得返回值，留给后面的脚本使用。
    log("编号：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setId(id)

> 设置当前图片信息对象的编号。
> 
> 输入参数 id 的类型为 long（长整数；系统媒体库中这条记录的编号，不是列表下标）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getId() 检查结果。
> 这只修改内存中的资料，不会修改系统记录的编号，也不会保存到系统媒体库。

- 参数 : id {long} 长整数；系统媒体库中这条记录的编号，不是列表下标


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getId(); // 保存原来的值，演示后恢复。
    try {
        info.setId(1); // 仅修改这份信息，不操作真实文件。
        log("修改后的编号：" + info.getId());
    } finally {
        info.setId(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getName()

> 读取这条图片信息的名称。
> 
> 输入参数：无。返回类型为 String（字符串；媒体库记录的显示名称，可能没有提供）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {String} 字符串；媒体库记录的显示名称，可能没有提供


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getName(); // 取得返回值，留给后面的脚本使用。
    log("名称：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setName(name)

> 设置当前图片信息对象的名称。
> 
> 输入参数 name 的类型为 String（字符串；媒体库记录的显示名称，可能没有提供）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getName() 检查结果。
> 这只修改内存中的资料，不会重命名真实文件，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : name {String} 字符串；媒体库记录的显示名称，可能没有提供


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getName(); // 保存原来的值，演示后恢复。
    try {
        info.setName("教学名称"); // 仅修改这份信息，不操作真实文件。
        log("修改后的名称：" + info.getName());
    } finally {
        info.setName(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getSize()

> 读取这条图片信息的大小。
> 
> 输入参数：无。返回类型为 long（长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {long} 长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getSize(); // 取得返回值，留给后面的脚本使用。
    log("大小：" + value);
    log("大小（二进制千字节）：" + Number(value) / 1024); // 按一千零二十四字节换算。
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setSize(size)

> 设置当前图片信息对象的大小。
> 
> 输入参数 size 的类型为 long（长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getSize() 检查结果。
> 这只修改内存中的资料，不会压缩文件或改变真实文件大小，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : size {long} 长整数；文件大小，单位字节，除以一千零二十四可换算成二进制千字节


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getSize(); // 保存原来的值，演示后恢复。
    try {
        info.setSize(2048); // 仅修改这份信息，不操作真实文件。
        log("修改后的大小：" + info.getSize());
    } finally {
        info.setSize(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getPath()

> 读取这条图片信息的路径。
> 
> 输入参数：无。返回类型为 String（字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {String} 字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getPath(); // 取得返回值，留给后面的脚本使用。
    log("路径：" + value);
    if (value == null || String(value).length === 0) {
        log("媒体库尚未提供这项文字信息。");
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setPath(path)

> 设置当前图片信息对象的路径。
> 
> 输入参数 path 的类型为 String（字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getPath() 检查结果。
> 这只修改内存中的资料，不会移动、复制或创建真实文件，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : path {String} 字符串；媒体库记录的文件路径，可能为空；有路径也不代表当前脚本有权读取文件


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getPath(); // 保存原来的值，演示后恢复。
    try {
        info.setPath("/sdcard/example.dat"); // 仅修改这份信息，不操作真实文件。
        log("修改后的路径：" + info.getPath());
    } finally {
        info.setPath(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getTime()

> 读取这条图片信息的时间。
> 
> 输入参数：无。返回类型为 long（长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {long} 长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getTime(); // 取得返回值，留给后面的脚本使用。
    log("时间：" + value);
    // 日期对象需要毫秒，媒体库时间却是秒，要先换算。
    log(new Date(Number(value) * 1000).toString());
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setTime(time)

> 设置当前图片信息对象的时间。
> 
> 输入参数 time 的类型为 long（长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getTime() 检查结果。
> 这只修改内存中的资料，不会修改文件时间或媒体库的加入时间，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : time {long} 长整数；加入媒体库的时间，单位秒，从一九七零年一月一日零时的世界协调时间开始计算；不是拍摄时间，也不是毫秒


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getTime(); // 保存原来的值，演示后恢复。
    try {
        info.setTime(1700000000); // 仅修改这份信息，不操作真实文件。
        log("修改后的时间：" + info.getTime());
    } finally {
        info.setTime(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getWidth()

> 读取这条图片信息的宽度。
> 
> 输入参数：无。返回类型为 int（整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {int} 整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getWidth(); // 取得返回值，留给后面的脚本使用。
    log("宽度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setWidth(width)

> 设置当前图片信息对象的宽度。
> 
> 输入参数 width 的类型为 int（整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getWidth() 检查结果。
> 这只修改内存中的资料，不会缩放真实图片，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : width {int} 整数；图片宽度，单位像素，零可能表示媒体库未提供有效尺寸


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getWidth(); // 保存原来的值，演示后恢复。
    try {
        info.setWidth(1080); // 仅修改这份信息，不操作真实文件。
        log("修改后的宽度：" + info.getWidth());
    } finally {
        info.setWidth(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### getHeight()

> 读取这条图片信息的高度。
> 
> 输入参数：无。返回类型为 int（整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 读取的是对象中保存的值，不会重新扫描文件；调用对应设置方法后会读到修改后的值。

- 返回 : {int} 整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var value = info.getHeight(); // 取得返回值，留给后面的脚本使用。
    log("高度：" + value);
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


### setHeight(height)

> 设置当前图片信息对象的高度。
> 
> 输入参数 height 的类型为 int（整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸）。
> 输出类型为 void，表示没有返回值；请单独调用，再使用 getHeight() 检查结果。
> 这只修改内存中的资料，不会缩放真实图片，也不会保存到系统媒体库。
> 设置方法会同时更新对应的中文和英文字段。

- 参数 : height {int} 整数；图片高度，单位像素，零可能表示媒体库未提供有效尺寸


```javascript
// 先取得媒体信息列表；请提前在设备上授予相应的读取权限。
var list = $file.lsImages();
// 这是 Java 列表，用 size() 计数、get(0) 取第一项。
if (list != null && list.size() > 0) {
    var info = list.get(0); // 一条图片信息，不是文件内容。
    var original = info.getHeight(); // 保存原来的值，演示后恢复。
    try {
        info.setHeight(1920); // 仅修改这份信息，不操作真实文件。
        log("修改后的高度：" + info.getHeight());
    } finally {
        info.setHeight(original); // 即使打印出错，也恢复这项资料。
    }
} else {
    log("没有可读取的图片记录，请检查权限和媒体库内容。");
}
```


