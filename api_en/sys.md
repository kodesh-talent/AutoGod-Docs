# $sys - 系统工具

- 更新时间:2026-10-22 10:55:51

> $sys：一堆和手机系统有关的小工具。
> 
> 包括飞行模式、音量、设备标识、剪切板读写、电池优化白名单、前台保活、开发者指针等。
> 很多改系统设置的功能需要先拿到"修改系统设置"权限（用 $permit.set()）。



```javascript
// 取一下设备唯一标识
var id = $sys.getDeviceId();
```




### airplane(enable)

> 打开或关闭飞行模式。
> 
> 需要"修改系统设置"权限，先调 $permit.set() 获取。如果系统安全策略不允许直接改，
> 会自动跳到手动设置页面让用户自己开。

- 参数 : enable {boolean} true 打开，false 关闭
- 版本 : 1.0.0


```javascript
// 打开飞行模式
$sys.airplane(true);
```


### volume(mode, volume)

> 设置某一类声音的音量大小。
> 
> 第一个参数是声音类型，第二个是音量（会自动夹在 0 到该类型最大值之间）。
> 常用类型：system=系统、ring=铃声、music=媒体、alarm=闹钟、notification=通知、call=通话。

- 参数 : mode {string} 声音类型，如 system/ring/music/alarm/notification/call
- 参数 : volume {int} 目标音量，会自动限制在合法范围内
- 版本 : 1.0.0


```javascript
// 把媒体音量拉满
$sys.volume("music", 100);
// 把闹钟音量设到一半
$sys.volume("alarm", 5);
```


### getDeviceId()

> 获取这台设备的唯一标识（一串 MD5 后的字符串）。
> 
> 它由设备型号、厂商等信息拼起来再 MD5 得到，同一台手机每次结果相同，可用来区分设备。

- 返回 : {String} 这台设备的唯一标识字符串
- 版本 : 1.0.0


```javascript
// 取设备标识
var id = $sys.getDeviceId();
toast("设备id：" + id);
```


### hasClip()

> 检查系统剪切板里现在有没有内容。

- 返回 : {boolean} true 表示剪切板有内容
- 版本 : 1.0.0


```javascript
// 有内容就取出来看看
if ($sys.hasClip()) {
    var content = $sys.getClip();
    toast("剪切板：" + content);
}
```


### clearClip()

> 清空系统剪切板里的内容。

- 返回 : {boolean} true 表示清空成功
- 版本 : 1.0.0


```javascript
// 清空剪切板
$sys.clearClip();
```


### getClip()

> 读取系统剪切板里当前复制的文字。
> 
> 一般先 hasClip 确认有内容再读。

- 返回 : {String} 剪切板里的文字，可能为空
- 版本 : 1.0.0


```javascript
// 读出剪切板内容
var content = $sys.getClip();
toast("剪切板：" + content);
```


### setClip(text)

> 把一段文字写进系统剪切板（相当于帮用户复制了这段文字）。

- 参数 : text {String} 要复制到剪切板的文字
- 返回 : {boolean} true 表示设置成功
- 版本 : 1.0.0


```javascript
// 复制一段文字
$sys.setClip("Hello AIGame !");
```


### ignorePower(pkgName)

> 检查某个应用是否已经被加入"忽略电池优化"白名单。
> 
> 开了这个，后台更不容易被系统杀掉。部分低版本安卓才可用。

- 参数 : pkgName {string} 要检查的应用包名
- 返回 : {boolean} true 表示已在白名单
- 版本 : 1.0.0


```javascript
// 检查本应用是否已忽略电池优化
var is = $sys.ignorePower("org.aigame.app");
toast("是否忽略电池优化：" + is);
```


### requestIgnorePower(pkgName)

> 弹出系统请求，让用户把指定应用加入"忽略电池优化"白名单。
> 
> 通常在脚本刚启动时调用一次，请求用户授权保活。

- 参数 : pkgName {string} 要申请的应用包名
- 版本 : 1.0.0


```javascript
// 弹请求框，请用户授权
$sys.requestIgnorePower("org.aigame.app");
```


### stayAlive(enable)

> 开启或关闭前台保活服务，让脚本在后台更不容易被杀。

- 参数 : enable {boolean} true 开启保活，false 关闭
- 版本 : 1.1.2


```javascript
// 开启前台保活
$sys.stayAlive(true);
// 关闭保活
$sys.stayAlive(false);
```


### hasStayAlive()

> 查询前台保活服务当前是否正在运行。

- 返回 : {boolean} true 表示保活正在运行
- 版本 : 1.1.2


```javascript
// 查一下保活状态
var is = $sys.hasStayAlive();
toast("保活是否开启：" + is);
```


### hasPointer()

> 检查开发者选项里的"指针位置"显示是否已经打开。
> 
> 指针显示会在屏幕上画出触摸轨迹，常用于辅助调试点击位置。

- 返回 : {boolean} true 表示指针显示已打开
- 版本 : 1.4.1


```javascript
if ($sys.hasPointer()) {
    toast("指针已开启");
}
```


### pointer(enable)

> 开启或关闭开发者选项里的"指针位置"显示。
> 
> 它会依次尝试用 Root、Shizuku、写 secure 设置三种方式去开。
> 注意：授权不是立刻生效，开完最好等 1 秒再用 hasPointer 确认。

- 参数 : enable {boolean} true 开启，false 关闭
- 版本 : 1.7.0


```javascript
// 开启指针
$sys.pointer(true);
// 等 1 秒让它生效
sleep(1000);
if ($sys.hasPointer()) {
    toast("指针已开启");
}
```


### volumeCtrl(enable)

> 打开或关闭 App 内部的音量控制功能。
> 
> 用来决定是否接管音量键。

- 参数 : enable {boolean} true 开启音量控制，false 关闭
- 版本 : 1.9.4


```javascript
// 关闭音量控制
$sys.volumeCtrl(false);
```


