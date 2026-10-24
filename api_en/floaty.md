# $floaty - 悬浮窗

- 更新时间:2026-10-22 10:55:48

> $floaty：悬浮窗工具，用来在屏幕上盖自己的小窗口。
> 
> 支持三种悬浮窗：应用级（隐蔽、只盖本 App）、系统级（全屏覆盖但易被检测）、
> 可调节（可拖动调整大小），还有一个框选区域的范围选择器。用之前必须先拿到悬浮窗权限。



```javascript
// 先检查悬浮窗权限
var allowed = $floaty.hasPermit();
```




### getPermit()

> 申请并一直等待悬浮窗权限直到拿到。
> 
> 这是个阻塞方法：拿不到权限时后面的代码不会继续，每隔几秒会再弹一次权限申请。
> 做任何悬浮窗前都先调它。

- 返回 : {boolean} true 表示已获得权限
- 版本 : 1.0.0


```javascript
// 申请并等待悬浮窗权限
var ok = $floaty.getPermit();
if (ok) {
    log("拿到悬浮窗权限");
}
```


### hasPermit()

> 只检查一下悬浮窗权限有没有，不阻塞、不弹窗。

- 返回 : {boolean} true 表示已有权限
- 版本 : 1.0.0


```javascript
// 检查权限
var hasPermit = $floaty.hasPermit();
if (hasPermit) {
    log("有悬浮窗权限");
}
```


### newAdj(xmlOrPath)

> 创建一个"可调节"悬浮窗，返回 AdjFloaty 对象。
> 
> 可调节悬浮窗就是用户可以用手指拖动位置、调整大小的那种。传入一个布局 xml 的路径，
> 创建后用返回的对象来显示/关闭。

- 参数 : xmlOrPath {string} 布局 xml 的路径，或直接是一段 xml 内容
- 返回 : {AdjFloaty} 创建好的可调节悬浮窗对象
- 版本 : 1.4.4


```javascript
// 先确保有悬浮窗权限
$floaty.getPermit();
// 用一个布局文件创建可调节悬浮窗
var adjFloaty = $floaty.newAdj("./res/layout/floaty_adj.xml");
// 之后对 adjFloaty 做显示、关闭等操作
```


### newApp(xmlOrPath)

> 创建一个"应用级"悬浮窗，返回 AppFloaty 对象。
> 
> 应用级悬浮窗只在本 App 上面显示，不容易被检测到，适合做按钮面板。

- 参数 : xmlOrPath {string} 布局 xml 路径或内容
- 返回 : {AppFloaty} 应用级悬浮窗对象
- 版本 : 1.4.4


```javascript
$floaty.getPermit();
// 用布局文件创建应用级悬浮窗
var appFloaty = $floaty.newApp("./res/layout/floaty_app.xml");
// 之后操作 appFloaty
```


### newApp(xmlOrPath, touchable)

> 创建应用级悬浮窗，并指定它能不能被触摸。
> 
> touchable 传 false 时，这个悬浮窗不挡触摸，下面的按钮还能点到（透明穿透层常用）。

- 参数 : xmlOrPath {string} 布局 xml 路径或内容
- 参数 : touchable {boolean} true 可触摸，false 穿透不挡手
- 返回 : {AppFloaty} 应用级悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.getPermit();
// 创建一个不可触摸（穿透）的应用级悬浮窗
var appFloaty = $floaty.newApp("./res/layout/floaty_app.xml", false);
```


### newSys(xmlOrPath)

> 创建一个"系统级"悬浮窗，返回 SysFloaty 对象。
> 
> 系统级悬浮窗能全屏覆盖到状态栏和导航栏，但容易被第三方 App（尤其游戏）检测到，
> 可能导致对方闪退，谨慎使用。

- 参数 : xmlOrPath {string} 布局 xml 路径或内容
- 返回 : {SysFloaty} 系统级悬浮窗对象
- 版本 : 1.4.4


```javascript
$floaty.getPermit();
// 用布局文件创建系统级悬浮窗
var sysFloaty = $floaty.newSys("./res/layout/floaty_sys.xml");
```


### newSys(xmlOrPath, touchable)

> 创建系统级悬浮窗，并指定是否可触摸。

- 参数 : xmlOrPath {string} 布局 xml 路径或内容
- 参数 : touchable {boolean} true 可触摸，false 穿透
- 返回 : {SysFloaty} 系统级悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.getPermit();
// 不可触摸的系统级悬浮窗
var sysFloaty = $floaty.newSys("./res/layout/floaty_sys.xml", false);
```


### newSelect(callback)

> 弹出一个"范围选择"悬浮窗，让用户拖出一个选框。
> 
> 用户可以调整选框的大小和位置；关闭时回调里会拿到选框的位置和范围数据，
> 常用于截屏找图前先框选区域。

- 参数 : callback {function(rect){}} 选完后回调，参数是选框区域数据
- 返回 : {SelectFloaty} 范围选择悬浮窗对象
- 版本 : 1.8.3


```javascript
$floaty.getPermit();
// 弹出范围选择器，选完回调出区域
var select = $floaty.newSelect(function(rect) {
    log("用户选择范围：" + rect);
});
```


![](./img/floaty_newSelect.png)

### closeAll()

> 把当前脚本创建的所有悬浮窗全部关掉。

- 版本 : 1.0.0


```javascript
// 关闭所有悬浮窗
$floaty.closeAll();
```


