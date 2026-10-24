# SysFloaty - 系统级悬浮窗

- 更新时间:2026-10-22 10:55:49

> 系统级悬浮窗。
> 
> 它是一个可以浮在所有 App 最上面的小窗口（系统权限级），用来放自己的按钮、文字、开关等界面。
> 可以自由设置位置、宽高、是否全屏、是否能被手指点到，还能监听屏幕横竖屏切换。
> 脚本里一般用 $floaty.newSys("布局文件") 创建并显示；创建后用 id("控件id") 找里面的控件。
> 设置位置、大小的方法都会把悬浮窗自己返回，所以可以一串连着写（链式调用）。
> 它和应用级悬浮窗（AppFloaty）用法几乎一样，区别是它能在更多场景下显示、层级更高。



```javascript
var floaty = $floaty.newSys("main.xml");   //按 main.xml 创建系统级悬浮窗
floaty.setXY(100, 200);                   //把它挪到 (100,200)
var btn = floaty.id("btn_close");         //找里面的关闭按钮
btn.点击事件(function(){                   //点按钮就关闭悬浮窗
    floaty.close();
});
```




### const {WindowManager.LayoutParams} params;

> 这个悬浮窗在系统里的窗口参数（WindowManager.LayoutParams）。
> 
> 记录悬浮窗的位置、宽高、窗口类型等底层信息，是公开字段。普通用户一般用 setX/setY 这些方法就够了。

- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");   //创建一个系统级悬浮窗
log(floaty.params);                        //打印它的窗口参数（高级用户才改）
```


### const {WindowManager} manager;

> 系统的悬浮窗管理器（WindowManager）。
> 
> 负责把这个悬浮窗加到屏幕上、更新位置或移除。普通用户一般不需要直接碰它。

- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");   //创建一个系统级悬浮窗
log(floaty.manager);                       //打印系统悬浮窗管理器
```


### onScreenChange(callback)

> 注册一个“屏幕横竖屏切换时”会被调用的函数。
> 
> 当用户把手机横着拿或竖着拿、屏幕方向变了时，你传进来的这个函数会自动被调用，
> 系统会把最新的屏幕信息（ScreenInfo）当作参数传给它，方便在里面重新摆放悬浮窗。

- 参数 : callback {Function} 屏幕旋转时要执行的函数，会收到一个 ScreenInfo 屏幕信息参数
- 版本 : 1.4.3


```javascript
var floaty = $floaty.newSys("main.xml");
//屏幕旋转时回调，screenInfo 是最新的屏幕信息
floaty.onScreenChange(function(screenInfo) {
    log("屏幕方向变了，宽：" + screenInfo.getW());
});
```


### id(id)

> 在这个悬浮窗里，按控件 id 找到对应的控件（XView）。
> 
> 悬浮窗里放了按钮、文字等控件后，用这个方法按它们的 id 把对象取出来，才能进一步加事件、改文字。
> 找不到时返回 null。

- 参数 : id {String} 要找的控件 id 字符串，比如 "mButton"
- 返回 : {XView} 找到的控件对象；找不到时返回 null
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
var mButton = floaty.id("mButton");      //找 id 为 mButton 的按钮
if (mButton != null) {
    mButton.点击事件(function(){          //点它就关闭悬浮窗
        floaty.close();
    });
}
```


### fill(fill)

> 设置悬浮窗是否铺满整个屏幕（全屏）。
> 
> 传 true，悬浮窗就撑满整个屏幕；传 false，又回到按内容大小自动收缩的状态。
> 返回悬浮窗自己，可链式调用。

- 参数 : fill {boolean} true 表示全屏铺满，false 表示按内容大小
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.fill(true);                       //让它全屏显示
```


### touch(touchable)

> 设置悬浮窗能不能被手指点到。
> 
> 传 true，悬浮窗上的按钮可以正常点击；传 false，悬浮窗变成“透明”的，手指点它会穿透到下面的 App。
> 返回悬浮窗自己，可链式调用。

- 参数 : touchable {boolean} true 表示可以点，false 表示不可触摸（点击穿透）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.touch(false);                   //设置成不可触摸（点击穿透）
```


### setX(x)

> 设置悬浮窗左上角的 X 坐标（离屏幕左边的距离，单位像素）。
> 
> 设完会立刻刷新显示。返回悬浮窗自己，可链式调用。

- 参数 : x {int} 新的 X 坐标（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setX(100);                       //把左边移到离屏幕左缘 100 像素
```


### setY(y)

> 设置悬浮窗左上角的 Y 坐标（离屏幕顶部的距离，单位像素）。
> 
> 设完会立刻刷新显示。返回悬浮窗自己，可链式调用。

- 参数 : y {int} 新的 Y 坐标（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setY(200);                       //把上边移到离屏幕顶部 200 像素
```


### setXY(x, y)

> 一次同时设置悬浮窗的 X、Y 坐标（位置，单位像素）。
> 
> 相当于同时调 setX 和 setY，但只刷新一次，更省事。返回悬浮窗自己，可链式调用。

- 参数 : x {int} 新的 X 坐标（像素）
- 参数 : y {int} 新的 Y 坐标（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setXY(100, 200);                //一次把位置设到 (100,200)
```


### setW(w)

> 设置悬浮窗的宽度（单位像素）。
> 
> 设完会立刻刷新显示。返回悬浮窗自己，可链式调用。

- 参数 : w {int} 新的宽度（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setW(300);                       //把宽度设为 300 像素
```


### setH(h)

> 设置悬浮窗的高度（单位像素）。
> 
> 设完会立刻刷新显示。返回悬浮窗自己，可链式调用。

- 参数 : h {int} 新的高度（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setH(200);                       //把高度设为 200 像素
```


### setWH(w, h)

> 一次同时设置悬浮窗的宽度和高度（单位像素）。
> 
> 相当于同时调 setW 和 setH。返回悬浮窗自己，可链式调用。

- 参数 : w {int} 新的宽度（像素）
- 参数 : h {int} 新的高度（像素）
- 返回 : {SysFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
floaty.setWH(300, 200);                //宽设 300、高设 200
```


### check()

> 检查这个悬浮窗现在还能不能用。
> 
> 返回 true 表示它还好好显示着、可以继续操作；返回 false 表示它已经被关闭或没正常显示，
> 这时再去 setX、id 之类的操作都没有意义。做循环操作前，先用它判断一下更安全。

- 返回 : {boolean} 还能正常用返回 true；已关闭或不可用返回 false
- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
if (floaty.check()) {                   //先检查还在不在
    log("悬浮窗还在，可以操作");
} else {
    log("悬浮窗已经关闭了");
}
```


### close()

> 关闭并销毁这个悬浮窗。
> 
> 调用后悬浮窗会从屏幕上消失，相关资源也会被释放；之后再操作它就没用了。

- 版本 : 1.3.5


```javascript
var floaty = $floaty.newSys("main.xml");  //创建系统级悬浮窗
sleep(3000);                            //显示 3 秒
floaty.close();                         //然后关闭悬浮窗
```


