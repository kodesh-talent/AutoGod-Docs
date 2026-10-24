# $global - 全局函数

- 更新时间:2026-10-22 10:55:47

> 全局函数（脚本里直接写名字就能用，不需要加 $ 前缀）。
> 
> 这里放的是最常用的一批小工具：等待几秒、弹提示框、显示图片、操作剪贴板、
> 读取当前前台应用的包名/界面名、取当前时间等。
> 
> 这些函数大多同时提供英文版和中文版，功能完全一样，按习惯选一个用即可。



```javascript
sleep(1000);                 //等待 1 秒
tip("脚本开始运行");          //弹一个小提示
var pkg = curPkg();          //读当前前台应用包名
log("当前包名：" + pkg);
```




### sleep(ms)

> 让脚本暂停一会儿（单位毫秒，1000 毫秒 = 1 秒）。
> 
> 比如模拟人为操作时，点完按钮等界面加载，就常用它等一下。

- 参数 : ms {int} 要等待的毫秒数
- 版本 : 1.0.0


```javascript
sleep(1000);   //等待 1 秒钟
```


### tip(info)

> 弹出一个小提示框，显示一段文字（标题固定为“提示”）。

- 参数 : info {String} 要显示的提示文字
- 版本 : 1.0.0


```javascript
tip("我是提示内容");
```


### alert(title, msg)

> 弹出一个对话框，可以自己指定标题和内容。

- 参数 : title {String} 对话框标题
- 参数 : msg {String} 对话框内容
- 版本 : 1.0.0


```javascript
alert("提示对话框", "我很好");
```


### showImg(img)

> 在屏幕上悬浮显示一张图片。
> 
> 参数既可以直接传图片路径字符串，也可以传一个用 $img 读出来的图片对象。

- 参数 : img {Image|String} 图片对象或图片路径
- 版本 : 1.0.0


```javascript
//方式一：直接传图片路径
showImg("/sdcard/Pictures/t01.png");
//方式二：先读成图片对象再显示
var img = $img.read("/sdcard/Pictures/t01.png");
showImg(img);
```


### closeLog()

> 关闭屏幕上的绘制日志悬浮窗。

- 版本 : 1.0.0


```javascript
closeLog();
```


### closeDraw()

> 关闭所有绘制悬浮窗（把画在屏幕上的图形、线条等全部关掉）。

- 版本 : 1.0.0


```javascript
closeDraw();
```


### clearDraw()

> 清空当前画出来的内容，但不关闭绘制悬浮窗。
> 
> 和 closeDraw 的区别：closeDraw 是整个关掉，clearDraw 只是擦掉画面、悬浮窗还在。

- 版本 : 1.0.0


```javascript
clearDraw();
```


### getClip()

> 读取手机剪贴板里当前复制的文字。

- 返回 : {String} 剪贴板里的文字，读取不到时返回 null
- 版本 : 1.0.0


```javascript
var clip = getClip();
log("剪贴板内容：" + clip);
```


### setClip(text)

> 把一段文字写进手机剪贴板（相当于帮用户“复制”）。

- 参数 : text {String} 要复制到剪贴板的文字
- 版本 : 1.0.0


```javascript
setClip("我是剪贴板内容");
```


### hasClip()

> 判断剪贴板里现在有没有内容。

- 返回 : {boolean} 有内容返回 true，没有返回 false
- 版本 : 1.0.0


```javascript
if (hasClip()) {
    var clip = getClip();   //有内容再去读
    log("剪贴板内容：" + clip);
}
```


### clearClip()

> 清空剪贴板里的内容。

- 返回 : {boolean} 清空成功返回 true
- 版本 : 1.0.0


```javascript
clearClip();
```


### curPkg()

> 读取当前手机最前台正在显示的应用的包名。
> 
> 包名是一个应用的唯一身份证，比如微信是 com.tencent.mm。

- 返回 : {String} 当前前台应用的包名
- 版本 : 1.3.1


```javascript
var pkgName = curPkg();
log("当前前台应用包名：" + pkgName);
```


### curCls()

> 读取当前前台界面的“活动名”（Activity 类名）。
> 
> 它能告诉你现在打开的是哪个具体页面，常用来判断“是不是到了某个页面”。

- 返回 : {String} 当前界面的活动名
- 版本 : 1.3.1


```javascript
var actName = curCls();
log("当前界面活动名：" + actName);
```


### curTime()

> 读取当前的时间戳（从 1970 年到现在一共多少毫秒）。
> 
> 常用来计算一段代码跑了多久。

- 返回 : {long} 当前时间戳，单位毫秒
- 版本 : 1.7.8


```javascript
var stamp = curTime();
log("当前时间戳：" + stamp);
```


### info(msg)

> 弹出一个悬浮的土司提示，显示一段信息。
> 
> 可以一次传多个参数，会自动拼到一起。它会浮在屏幕上，适合给用户看运行状态。

- 参数 : msg {string...} 要显示的内容，可传多个


```javascript
// 弹一条悬浮提示
info("提示信息");
```


### infoLog(msg)

> 既弹悬浮土司，又在控制台打印一条信息。
> 
> 等于同时调用一次 info 和一次 log。

- 参数 : msg {string...} 要显示和打印的内容


```javascript
// 屏幕上弹提示，同时控制台也打印
infoLog("提示信息");
```


### toast(msg)

> 用系统自带的土司弹一条短提示。
> 
> 部分手机要先开通知权限，土司才能显示在其他应用上方。

- 参数 : msg {string...} 要显示的内容


```javascript
// 弹一条系统土司
toast("提示信息");
```


### toastLog(msg)

> 既弹系统土司，又在控制台打印。
> 
> 等于同时调用 toast 和 log。

- 参数 : msg {string...} 要显示和打印的内容


```javascript
// 弹土司并打印
toastLog("提示信息");
```


### log(msg)

> 往控制台打印一条日志，不弹窗。
> 
> 调试时最常用，用来在日志窗口看中间结果。

- 参数 : msg {string...} 要打印的内容


```javascript
// 打印日志
log("信息");
```


### print(msg)

> 往控制台打印一条日志，和 log 一样。

- 参数 : msg {string...} 要打印的内容


```javascript
// 打印
print("信息");
```


### random()

> 生成一个 0 到 1 之间的随机小数。

- 返回 : {float} 0 到 1 之间的随机小数


```javascript
// 打印一个 0~1 的随机数
log(random());
```


### random(max)

> 生成一个 0 到 max 之间的随机整数。

- 参数 : max {int} 随机数上限
- 返回 : {int} 0 到 max 之间的随机整数


```javascript
// 打印一个 0~10 的随机整数
log(random(10));
```


### random(min, max)

> 生成一个 min 到 max 之间的随机整数。

- 参数 : min {int} 最小值
- 参数 : max {int} 最大值
- 返回 : {int} min 到 max 之间的随机整数


```javascript
// 打印一个 10~30 的随机整数
log(random(10, 30));
```


### require(path)

> 引入一个外部 JS 模块文件，拿到它导出的对象/类。
> 
> 类似 Node 的 require：把另一个脚本里定义的类或对象加载进来，然后 new 出来用。

- 参数 : path {string} 模块脚本的路径
- 返回 : {JsObject} 模块导出的对象或类


```javascript
// 引入同目录下的模块，再 new 出它的类
var MyClass = require("mCls.js");
var obj = new MyClass();
```


