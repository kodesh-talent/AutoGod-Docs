# $app - 应用操作

- 更新时间:2026-10-22 10:55:45

> 应用管理工具（脚本里的 $app 对象）。
> 应用管理工具（脚本里的 $app 对象）。



```javascript
$app.runApp("com.example.reader");
```




### getIcon(name)

> 获取应用图标。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 返回 : {Image} 该应用的图标图片对象 Image；取不到时可能为 null
- 版本 : 1.0.0


```javascript
//获取悬浮窗权限
$floaty.getPermit();
//获取图标
var icon = $app.getIcon("QQ");//应用名称或者包名
//显示图片
$img.show(icon);//(需要用悬浮窗权限) 也可以直接调用 icon.show(); //icon是{Image}类对象，因此可以世界调用show()方法。
```


### runApp(appName)

> 按应用名称或包名启动应用。

- 参数 : appName {String} 要操作的应用名称（桌面上显示的中文/英文名字）
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.runApp("QQ");//应用名
```


### launchApp(appName)

> 按应用名称或包名启动应用。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : appName {String} 要操作的应用名称（桌面上显示的中文/英文名字）
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.launchApp("QQ");//应用名
```


### launch(appName)

> 按应用名称或包名启动应用。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : appName {String} 要操作的应用名称（桌面上显示的中文/英文名字）
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.launch("QQ");//应用名或包名
```


### launchPkg(packageName)

> 按包名启动应用。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : packageName {String} 应用的包名，如 "com.tencent.mm"
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.launchPkg("com.tencent.mobileqq");//传入包名
```


### runPkg(packageName)

> 按包名启动应用。

- 参数 : packageName {String} 应用的包名，如 "com.tencent.mm"
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.runPkg("com.tencent.mobileqq");//传入包名
```


### run(name)

> 打开应用，这是推荐使用的方法。
> 
> 这是最简短的启动方式，推荐使用。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 返回 : {boolean} true 表示启动成功，false 表示失败
- 版本 : 1.0.0


```javascript
$app.run("QQ");//可传入包名或者应用名
```


### ls()

> 查询全部可查询应用，返回可逐项读取的宿主列表。
> 输入：无参数。输出：List<AppInfo>，每个元素都是 AppInfo 对象。
> 列表不是普通脚本数组：用 size() 读取数量，用 get(索引) 取元素，索引从零开始；不要直接假设第一项存在。
> 本方法基于系统返回的应用信息构建结果，不承诺列出设备上的每一个应用；以当前环境能查询到的结果为准。
> 每项含名称、包名、原生应用信息和图标；加载图标失败时 icon 为 null。查询会尝试加载所有返回项的图标，不宜在高频循环里反复调用。

- 返回 : {List<AppInfo>} 全部可查询应用列表；可能为空，使用 size() 和 get(索引) 读取
- 版本 : 1.0.0


```javascript
var apps = $app.ls(); //只查询一次，重复使用返回的列表
log("记录数量：" + apps.size());
for (var i = 0; i < apps.size(); i++) { //空列表不会进入循环
    var item = apps.get(i); //取得 AppInfo 对象
    log("名称：" + item.appName);
    log("包名：" + item.pkgName);
    var icon = item.getIcon(); //继续取得关联的 Image 图片对象
    if (icon != null) {
        log("图标宽高：" + icon.getWidth() + " × " + icon.getHeight()); //单位为像素
    }
}
```


### lsUserApp()

> 查询用户应用，返回可逐项读取的宿主列表。
> 输入：无参数。输出：List<AppInfo>，每个元素都是 AppInfo 对象。
> 列表不是普通脚本数组：用 size() 读取数量，用 get(索引) 取元素，索引从零开始；不要直接假设第一项存在。
> 本方法基于系统返回的应用信息构建结果，不承诺列出设备上的每一个应用；以当前环境能查询到的结果为准。
> 每项含名称、包名、原生应用信息和图标；加载图标失败时 icon 为 null。查询会尝试加载所有返回项的图标，不宜在高频循环里反复调用。
> 当前判断排除带系统应用标志或系统应用更新标志的应用，保留其他应用。

- 返回 : {List<AppInfo>} 用户应用列表；可能为空，使用 size() 和 get(索引) 读取
- 版本 : 1.3.2


```javascript
var apps = $app.lsUserApp(); //只查询一次，重复使用返回的列表
log("记录数量：" + apps.size());
for (var i = 0; i < apps.size(); i++) { //空列表不会进入循环
    var item = apps.get(i); //取得 AppInfo 对象
    log("名称：" + item.appName);
    log("包名：" + item.pkgName);
    var icon = item.getIcon(); //继续取得关联的 Image 图片对象
    if (icon != null) {
        log("图标宽高：" + icon.getWidth() + " × " + icon.getHeight()); //单位为像素
    }
}
```


### lsSysApp()

> 查询系统应用，返回可逐项读取的宿主列表。
> 输入：无参数。输出：List<AppInfo>，每个元素都是 AppInfo 对象。
> 列表不是普通脚本数组：用 size() 读取数量，用 get(索引) 取元素，索引从零开始；不要直接假设第一项存在。
> 本方法基于系统返回的应用信息构建结果，不承诺列出设备上的每一个应用；以当前环境能查询到的结果为准。
> 每项含名称、包名、原生应用信息和图标；加载图标失败时 icon 为 null。查询会尝试加载所有返回项的图标，不宜在高频循环里反复调用。
> 当前判断保留带系统应用标志或系统应用更新标志的应用。

- 返回 : {List<AppInfo>} 系统应用列表；可能为空，使用 size() 和 get(索引) 读取
- 版本 : 1.3.2


```javascript
var apps = $app.lsSysApp(); //只查询一次，重复使用返回的列表
log("记录数量：" + apps.size());
for (var i = 0; i < apps.size(); i++) { //空列表不会进入循环
    var item = apps.get(i); //取得 AppInfo 对象
    log("名称：" + item.appName);
    log("包名：" + item.pkgName);
    var icon = item.getIcon(); //继续取得关联的 Image 图片对象
    if (icon != null) {
        log("图标宽高：" + icon.getWidth() + " × " + icon.getHeight()); //单位为像素
    }
}
```


### lsRecent()

> 查询最近使用记录，返回可逐项读取的宿主列表。
> 输入：无参数。输出：List<AppTaskInfo>，每个元素都是 AppTaskInfo 对象。
> 列表不是普通脚本数组：用 size() 读取数量，用 get(索引) 取元素，索引从零开始；不要直接假设第一项存在。
> 先通过使用情况权限检查，再调用查询。本实现查询最近五小时的使用统计，过滤掉最后使用早于起点或无法取得应用信息的记录，再按最后使用时间从近到远排列。
> 该结果不等同于系统最近任务界面的全部卡片，也不表示应用仍在运行。当前实现从统计列表末尾遍历到索引一，会跳过索引零，因此不能承诺记录完整。
> 安卓版本低于本实现支持范围时返回空列表；没有可用统计时也可能为空。
> lastUseTime 是 yyyy-MM-dd HH:mm:ss 日期文字，lastUsedTime 是毫秒时间戳，两者不能混用。

- 返回 : {List<AppTaskInfo>} 最近使用记录列表；可能为空，使用 size() 和 get(索引) 读取
- 版本 : 1.0.1


```javascript
if ($app.hasUsagePermit()) {
    var apps = $app.lsRecent(); //只查询一次，重复使用返回的列表
    log("记录数量：" + apps.size());
    for (var i = 0; i < apps.size(); i++) { //空列表不会进入循环
        var item = apps.get(i); //取得 AppTaskInfo 对象
        log("名称：" + item.appName);
        log("包名：" + item.pkgName);
        log("最后使用：" + item.lastUseTime); //格式化的日期文字
        log("对应毫秒数：" + item.getLastUsedTime()); //调用返回对象的方法
    }
} else {
    log("请先在系统设置中授予使用情况访问权限，之后重新运行查询");
}
```


### startActivity(name)

> 按应用名启动它的默认界面。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 版本 : 1.6.9


```javascript
//打开日志界面
$app.startActivity("log");//推荐写法
$app.startActivity("console");//兼容auto.js写法
//打开设备信息界面
$app.startActivity("device");
// （示例中的一行配置/说明）
$app.startActivity("ocr");
// （示例中的一行配置/说明）
$app.startActivity("yolo");
// （示例中的一行配置/说明）
$app.startActivity("shizuku");
```


### startActivity(name, activityName)

> 按应用名启动它的默认界面。

- 参数 : name {String} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 参数 : activityName {String} 要启动的 Activity 类名（可带包名）
- 返回 : {boolean} true 表示成功/成立，false 表示失败/不成立
- 版本 : 1.0.0


```javascript
//打开QQ
$app.startActivity("QQ","com.tencent.mobileqq.activity.SplashActivity");
```


### pkgExists(pkgName)

> 检查指定包是否已安装。

- 参数 : pkgName {String} 应用的包名，如 "com.tencent.mm"
- 返回 : {boolean} true 表示该包已安装，false 表示未安装
- 版本 : 1.0.0


```javascript
var pkg = "org.aigame.pro";
if ($app.pkgExists(pkg)) {
    alert(pkg,"存在");
} else {
    alert(pkg,"不存在");
}
```


### getPackageName(appName)

> 获取应用对应的包名。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : appName {String} 要操作的应用名称（桌面上显示的中文/英文名字）
- 返回 : {String} 应用名对应的包名；找不到返回 null
- 版本 : 1.0.0


```javascript
//获得包名
var pkg = $app.getPackageName("QQ");
alert("应用包名",pkg);
```


### pkgName(appName)

> 获取应用对应的包名。

- 参数 : appName {String} 要操作的应用名称（桌面上显示的中文/英文名字）
- 返回 : {String} 应用名对应的包名；找不到返回 null
- 版本 : 1.0.0


```javascript
//获得包名
var pkg = $app.pkgName("QQ");
alert("应用包名",pkg);
```


### appName(packageName)

> 根据包名获取应用名称。

- 参数 : packageName {String} 应用的包名，如 "com.tencent.mm"
- 返回 : {String} 包名对应的应用名称；找不到返回 null
- 版本 : 1.0.0


```javascript
//获得应用名
var appName = $app.appName("com.android.settings");
alert("应用名称",appName);//设置
```


### installApk(apkPath)

> 安装手机上某个路径下的 apk 安装包。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : apkPath {string} 要安装的 apk 文件在手机上的完整路径，如 "/sdcard/xx.apk"
- 返回 : {boolean} true 表示安装成功，false 表示失败
- 版本 : 1.3.3


```javascript
// （示例中的一行配置/说明）
$app.installApk("./apk/qq.apk");
```


### uninstallApp(name)

> 按应用名称或包名卸载应用。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstallApp("QQ");
```


### uninstallPkg(name)

> 按包名卸载应用。
> 
> 部分设备不支持此操作。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstallPkg("com.tencent.mobileqq");
```


### uninstall(name)

> 卸载应用。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstall("QQ");//应用名或包名
```


### openUrl(url)

> 打开网页链接。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : url {string} 要打开的网址，需带 http:// 或 https:// 前缀
- 版本 : 1.0.0


```javascript
//打开网址
var myUrl = "www.baidu.com";
$app.openUrl(myUrl);//http://www.baidu.com
```


### shareImg(imgPath)

> 分享图片。

- 参数 : imgPath {string} 图片文件在手机上的完整路径
- 版本 : 1.0.0


```javascript
//分享本地图片
var path = "/sdcard/Pictures/t01.png";
$app.shareImg(path);
```


### shareText(content)

> 分享文本。

- 参数 : content {string} 要分享出去的文本内容
- 版本 : 1.0.0


```javascript
//分享文本
var text = "你好";
$app.shareText(text);
```


### sendSms(phone, message)

> 打开短信编辑界面。
> 
> 打开短信编辑界面。

- 参数 : phone {string} 电话号码字符串
- 参数 : message {string} 短信正文内容
- 版本 : 1.0.0


```javascript
$app.sendSms("13593749477","你好我是xxx");
```


### call(phoneNumber)

> 拨打电话。
> 
> 如果已获得电话权限，会直接拨打电话。

- 参数 : phoneNumber {string} 电话号码字符串
- 版本 : 1.0.0


```javascript
$app.call("13593749477");
```


### sendMail(mail, title, content)

> 打开邮件编辑界面。
> 
> 设备必须安装邮件应用或提供内置邮件支持。

- 参数 : mail {string} 收件人邮箱地址
- 参数 : title {string} 标题（邮件/彩信标题）
- 参数 : content {string} 要分享出去的文本内容
- 返回 : {boolean} true 表示成功调起发送界面，false 表示失败
- 版本 : 1.0.0


```javascript
$app.sendMail("3502037911@qq.com","标题","内容");
```


### openAppSetting(name)

> 打开应用的系统设置页面。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。
> 
> 打开系统设置中的应用详情页面。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 返回 : {boolean} true 表示成功打开设置页
- 版本 : 1.0.0


```javascript
//前往权限设置界面
$app.openAppSetting("AIGame");
```


### appSetting(name)

> 跳到这个应用的系统“应用信息”设置页。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 返回 : {boolean} true 表示成功打开设置页
- 版本 : 1.0.0


```javascript
//前往权限设置界面
$app.appSetting("AIGame");
```


### viewFile(path)

> 打开文件进行查看。

- 参数 : path {string} 文件在手机上的完整路径
- 返回 : {boolean} true 表示成功打开文件
- 版本 : 1.0.0


```javascript
//打开文件
$app.viewFile("/sdcard/Pictures/test.text");
```


### editFile(path)

> 打开文件进行编辑。

- 参数 : path {string} 文件在手机上的完整路径
- 返回 : {boolean} true 表示成功打开编辑
- 版本 : 1.0.0


```javascript
//编辑文件
$app.editFile("/sdcard/Pictures/test.text");
```


### hasUsagePermit()

> 通过查询最近一年的应用使用记录，判断当前能否读取使用情况。
> 本方法不需要输入参数，返回 boolean 布尔值。
> 当前实现依据是否查到非空记录判断，不是直接读取权限开关。没有记录也会返回 false，因此 false 不能单独证明用户拒绝了权限。
> 安卓 5.1 以下直接返回 false；查询过程遇到系统异常时可能抛出异常。

- 返回 : {boolean} 最近一年查到非空使用记录时为 true，否则为 false。
- 版本 : 1.0.1


```javascript
// 把结果保存在变量中，便于观察，而不是忽略返回值。
var result = $app.hasUsagePermit();
log("是否查到使用记录：" + result);
```


### getUsagePermit()

> 打开使用情况访问权限的设置入口，或在当前检查已通过时直接返回。
> 本方法不需要输入参数，返回 boolean 布尔值。
> 返回 true 有两种可能：当前检查已经通过，或者系统设置页已成功打开。它不表示用户已经在设置中打开开关。
> 请在设置页中手动完成授权，回到脚本后再次调用权限检查方法，不要紧接着本方法就假定授权成功。

- 返回 : {boolean} 当前检查通过或设置页打开成功时为 true；尝试打开设置页失败时为 false。
- 版本 : 1.0.1


```javascript
// 把结果保存在变量中，便于观察，而不是忽略返回值。
var result = $app.getUsagePermit();
log("已检查或已打开设置入口：" + result);
// 用户完成设置并回到脚本后，再单独运行下面这行进行检查。
// log($app.hasUsagePermit());
```


### intent(options)

> 根据脚本配置创建 Android 意图对象，用来描述想打开的页面或想发送的内容。
> 输入是普通脚本对象，输出是 android.content.Intent 对象。这里只构造对象，不会自动启动页面、发送广播或把内容分享出去。
> 中文入口和英文入口使用相同的英文字段名，不要把 action、component、extras 等键翻译成中文。
> action 可填 VIEW、SEND 等系统动作简称；data 是数据地址；type 是内容类型；pkg 是目标应用包名。
> component 使用 {pkg: 包名, cls: 完整页面类名}；顶层 cls 当前没有被读取。categories 使用完整类别名称的字符串数组。
> extras 是数组，每项包含 name 和 value；空名称或 null 值会被忽略。flags 是标志名称数组，当前只使用第一个有效标志，不会合并多个标志。
> 当前实现先设置 data 再设置 type，同时设置时类型操作可能清除数据地址，下面把网址查看和文本分享拆成两个独立示例。

- 参数 : options {Object} 脚本配置对象，字段按上面的说明填写；不要用 null 代替有效配置。
- 返回 : {android.content.Intent} 构造好的意图；配置转换结果为空时返回空意图，转换或设置过程中仍可能抛出异常。
- 版本 : 1.0.1


```javascript
// 示例一：准备查看网址的意图，此处只检查结果，不启动浏览器。
var options = {
    action: "VIEW", // 查看地址内容
    data: "https://example.com", // 换成需要查看的网址
    flags: ["FLAG_ACTIVITY_NEW_TASK"], // 从非页面环境启动时常用的标志
    categories: ["android.intent.category.BROWSABLE"] // 浏览器可处理的类别
};
var intent = $app.intent(options);
log(String(intent));
// 示例二：准备纯文本分享，正文放在 extras 中。
var shareOptions = {
    action: "SEND",
    type: "text/plain",
    extras: [{name: "android.intent.extra.TEXT", value: "你好，这是分享示例"}]
};
var shareIntent = $app.intent(shareOptions);
log(String(shareIntent));
```


应用管理工具（脚本里的 $app 对象）。


```html
//[工具] 可以用来添加QQ群
var joinQQGroup = function (qqNum) {
    $app.startActivity({
// （示例中的一行配置/说明）
// （示例中的一行配置/说明）
    });
}
//使用方式
joinQQGroup(661266412);
```


### sendBroadcast(intent)

> 发送异步广播。

- 参数 : intent {Intent} 用 $app.intent(options) 创建好的意图对象
- 版本 : 1.0.1


```javascript
$app.sendBroadcast(null);
```


### sendBroadcast(intent, permis)

> 发送一条广播，可指定接收方需要的权限。

- 参数 : intent {Intent} 用 $app.intent(options) 创建好的意图对象
- 参数 : permis {string} 广播需要的权限名称；不需要权限时传 null 或空串
- 版本 : 1.0.1


```javascript
$app.sendBroadcast(null, "sample");
```


### sendOrderedBroadcast(intent, permis)

> 发送同步广播。

- 参数 : intent {Intent} 用 $app.intent(options) 创建好的意图对象
- 参数 : permis {string} 广播需要的权限名称；不需要权限时传 null 或空串
- 版本 : 1.0.1


```javascript
$app.sendOrderedBroadcast(null, "sample");
```


### startActivity(intent)

> 按应用名启动它的默认界面。

- 参数 : intent {Intent} 用 $app.intent(options) 创建好的意图对象
- 版本 : 1.0.1


```javascript
$app.startActivity(null);
```


### startActivity(options)

> 按应用名启动它的默认界面。

- 参数 : options {Object} 配置对象（一个 JSON 对象），具体可填字段见下方示例
- 版本 : 1.1.1


```javascript
$app.startActivity({ action: "android.intent.action.VIEW", data: "https://example.com" });
```


### getForeApps()

> 获取前台应用包名列表。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 返回 : {String[]} 当前前台正在运行的应用包名列表
- 版本 : 1.0.4


```javascript
var result = $app.getForeApps();
```


### kill(name)

> 停止应用。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 参数 : name {string} 要操作的应用名称（桌面显示的名字）；也可以直接传包名
- 版本 : 1.0.4


```javascript
//结束应用
$app.kill("QQ");
$app.kill("MT管理器");
```


### sendMms(phone, title, message, imgPath)

> 打开彩信编辑界面。

- 参数 : phone {string} 电话号码字符串
- 参数 : title {string} 标题（邮件/彩信标题）
- 参数 : message {string} 短信正文内容
- 参数 : imgPath {string} 图片文件在手机上的完整路径
- 版本 : 1.4.9


```javascript
//发送彩信
$app.sendMms("13800000000", "测试彩信", "这是一条彩信", "/sdcard/DCIM/100ANDRO/IMG_20230801_100000.jpg");
```


### openSelf()

> 打开当前应用。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。
> 
> 调用前请确保已授予所需权限；具体可运行示例见下方代码块。

- 版本 : 1.6.2


```javascript
//打开自身应用
$app.openSelf();
```


