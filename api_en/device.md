# $device - 设备信息

- 更新时间:2026-10-22 10:55:46

> 设备信息工具对象（脚本里的全局对象 $device）。
> 
> 它用来“读取和控制这台手机本身的状态”，主要分两类：
> <ul>
>     <li>读信息：手机型号、品牌、安卓版本、屏幕宽高、电量、内存、音量、IMEI、安卓ID、MAC 地址等；</li>
>     <li>控状态：亮屏/息屏、保持屏幕常亮、震动、判断是否在充电、是否锁屏等。</li>
> </ul>
> 很多硬件信息（型号、品牌等）是开机就固定好的静态常量，直接用 $device.字段名 读取即可。



```javascript
//读取当前屏幕亮度
var brightness = $device.getBrightness();
log("当前屏幕亮度是：" + brightness);
//顺便看看手机型号和电量
log("手机型号：" + $device.model);
log("当前电量：" + $device.getBattery() + "%");
```




### const {int} width;

> 屏幕的宽度


### const {int} height;

> 屏幕的高度


### const {String} buildId;

> 系统构建 ID（一串由厂商和系统版本组成的内部标识字符串）。
> 
> 它是安卓系统 Build.ID 的原样读取，通常用来区分同型号手机刷的不同系统版本。


```javascript
log("系统构建ID：" + $device.buildId);
```


### const {String} buildDisplay;

> 系统显示版本号（给人看的那串内部版本描述字符串）。
> 
> 它是安卓 Build.DISPLAY 的原样读取，和“发行版”不同，这里更偏厂商内部的编译描述。


```javascript
log("系统显示版本：" + $device.buildDisplay);
```


### const {String} product;

> 产品名称


### const {String} board;

> 主板名称


### const {String} brand;

> 品牌名称


### const {String} device;

> 设备名称


### const {String} model;

> 型号名称


### const {String} bootloader;

> 引导加载程序名称


### const {String} hardware;

> 硬件名称


### const {String} fingerprint;

> 系统“指纹”信息（一长串拼起来的完整版本标识字符串）。
> 
> 它把品牌、型号、版本号等一长串信息拼成一个唯一字符串，常用于判断这台机器的系统到底是什么版本。


```javascript
log("系统指纹：" + $device.fingerprint);
```


### const {int} sdkInt;

> 系统 SDK 版本号（整数）。
> 
> 这是安卓给每个系统版本编的数字代号：比如安卓 13 是 33、安卓 14 是 34。
> 写脚本时常用它判断“这台手机支不支持某个新功能”，数字越大系统越新。


```javascript
var v = $device.sdkInt;
log("系统SDK版本号：" + v);
if (v >= 33) {
    log("这是安卓13或以上");
}
```


### const {String} incremental;

> 内部版本号


### const {String} release;

> 系统发行版本号（给人看的版本数字字符串，比如 "13"、"14"）。
> 
> 这就是设置里“关于手机”看到的那个安卓版本号，和数字形式的 sdkInt 对应。


```javascript
log("安卓版本：" + $device.release);
```


### const {String} code;

> 开发代号


### const {String} serial;

> 序列号


### const {String} baseOS;

> 基础操作系统版本。
> 
> 表示这台设备底层基础操作系统的版本字符串。注意：在安卓 6.0 以下的旧系统上它取不到值，会是 null。


```javascript
log("基础操作系统版本：" + $device.baseOS);
```


### const {String} securityPatch;

> 系统安全补丁版本日期（一串类似 "2024-01-05" 的日期字符串）。
> 
> 表示这台手机最近一次系统安全更新打到了哪个时间点。安卓 6.0 以下旧系统取不到值，会是 null。


```javascript
log("安全补丁日期：" + $device.securityPatch);
```


### getIMEI()

> 读取手机的 IMEI（设备识别码）。
> 
> IMEI 是手机通话模块的唯一串号。注意：读取它需要“读取手机状态”权限，
> 安卓 10 以后系统对普通 App 限制很严，多数情况下读不到会返回 null。

- 返回 : {string} 手机 IMEI 字符串；没有权限或读取失败时返回 null
- 版本 : 1.0.0


```javascript
var imei = $device.getIMEI();
log("IMEI：" + imei);   //没权限或被系统限制时是 null
```


### getAndroidId()

> 读取安卓 ID（设备在本机上的一个固定识别字符串）。
> 
> 安卓 ID 是“本机这一套系统”的标识，不需要特殊权限就能读，常用于在不涉及隐私的前提下区分设备。
> 恢复出厂设置后它会变。

- 返回 : {string} 安卓 ID 字符串；读取失败时可能返回 null
- 版本 : 1.0.0


```javascript
var id = $device.getAndroidId();
log("Android ID：" + id);
```


### getBrightness()

> 获取屏幕亮度

- 返回 : {int} 当前屏幕亮度，范围一般是 0~255（0最暗、255最亮）；读取异常时返回 -1
- 版本 : 1.0.0


```javascript
log("屏幕亮度:", $device.getBrightness());
```


### getBrightnessMode()

> 读取屏幕亮度模式（是手动亮度还是自动亮度）。
> 
> 返回 0 表示手动调节亮度，返回 1 表示自动亮度（随环境光自动变亮变暗）。

- 返回 : {int} 亮度模式：0=手动，1=自动；读取异常时返回 -1
- 版本 : 1.0.0


```javascript
log("屏幕亮度模式:", $device.getBrightnessMode());
```


### getMusicVolume()

> 获取音乐音量

- 返回 : {int} 当前“媒体/音乐”音量大小（0 到该类型最大音量之间的整数）
- 版本 : 1.0.0


```javascript
log("音乐音量:", $device.getMusicVolume());
```


### getNotificationVolume()

> 获取通知音量

- 返回 : {int} 当前“通知”音量大小
- 版本 : 1.0.0


```javascript
log("通知音量:", $device.getNotificationVolume());
```


### getAlarmVolume()

> 获取闹钟音量

- 返回 : {int} 当前“闹钟”音量大小
- 版本 : 1.0.0


```javascript
log("闹钟音量:", $device.getAlarmVolume());
```


### getMusicMaxVolume()

> 获取最大音乐音量

- 返回 : {int} “音乐/媒体”音量能调到的最大值（档位上限）
- 版本 : 1.0.0


```javascript
log("音乐最大音量:", $device.getMusicMaxVolume());
```


### getNotificationMaxVolume()

> 获取最大通知音量

- 返回 : {int} “通知”音量能调到的最大值
- 版本 : 1.0.0


```javascript
log("通知最大音量:", $device.getNotificationMaxVolume());
```


### getAlarmMaxVolume()

> 获取最大闹钟音量

- 返回 : {int} “闹钟”音量能调到的最大值
- 版本 : 1.0.0


```javascript
log("闹钟最大音量:", $device.getAlarmMaxVolume());
```


### getBattery()

> 电池电量百分比

- 返回 : {float} 当前电量百分比（0~100，可带一位小数，如 87.5）；读取失败时返回 -1
- 版本 : 1.0.0


```javascript
log("电池电量百分比:", $device.getBattery());
```


### getTotalMem()

> 获取总内存

- 返回 : {long} 设备总内存大小，单位字节（除以 1024/1024 可得 MB）
- 版本 : 1.0.0


```javascript
log("总内存:", $device.getTotalMem());
```


### getAvailMem()

> 获取可用内存

- 返回 : {long} 当前可用内存大小，单位字节
- 版本 : 1.0.0


```javascript
log("可用内存:", $device.getAvailMem());
```


### isCharging()

> 检查设备是否正在充电

- 返回 : {boolean} 正在充电（插着充电器或USB）返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
log("是否正在充电:", $device.isCharging());
```


### isScreenOn()

> 检查屏幕是否点亮

- 返回 : {boolean} 屏幕当前处于点亮状态返回 true，已熄灭返回 false
- 版本 : 1.0.0


```javascript
log("是否亮起:", $device.isScreenOn());
```


### isScreenOff()

> 检查屏幕是否熄灭

- 返回 : {boolean} 屏幕当前已熄灭（息屏）返回 true，还亮着返回 false
- 版本 : 1.0.0


```javascript
log("是否熄灭:", $device.isScreenOff());
```


### wakeUp()

> 唤醒设备屏幕

- 版本 : 1.0.0


```javascript
// 唤醒设备屏幕
$device.wakeUp();
```


### keepScreenOn()

> 保持屏幕点亮

- 版本 : 1.0.0


```javascript
// 保持屏幕常亮
$device.keepScreenOn();
```


### keepScreenOn(timeout)

> 保持屏幕常亮一段时间（到点自动恢复可自动息屏）。
> 
> 和无参的 keepScreenOn() 区别：这个版本只在指定时长内保持屏幕亮着，超时后会自动释放，不再强制亮屏。
> 适合“接下来要做一段几分钟的任务，别让屏幕中途灭掉”的场景。

- 参数 : timeout {long} 保持亮屏的时长，单位毫秒（1000 毫秒 = 1 秒）
- 版本 : 1.0.0


```javascript
//接下来 10 秒内保持屏幕常亮，期间执行任务
$device.keepScreenOn(10000);
```


### keepScreenDim()

> 保持屏幕暗屏

- 版本 : 1.0.0


```javascript
// 保持屏幕低亮
$device.keepScreenDim();
```


### keepScreenDim(timeout)

> 保持屏幕暗屏

- 参数 : timeout {long} 保持低亮的时长，单位毫秒
- 版本 : 1.0.0


```javascript
// 保持屏幕低亮
$device.keepScreenDim(1000);
```


### cancelKeepingAwake()

> 停止保持屏幕唤醒

- 版本 : 1.0.0


```javascript
// 取消唤醒
$device.cancelKeepingAwake();
```


### vibrate(millis)

> 振动指定时长

- 参数 : millis {long} 震动时长，单位毫秒
- 版本 : 1.0.0


```javascript
// 震动
$device.vibrate(1000);
```


### cancelVibration()

> 停止振动

- 版本 : 1.0.0


```javascript
// 取消震动
$device.cancelVibration();
```


### getMacAddress()

> 读取本机无线网卡（WiFi）的 MAC 地址。
> 
> MAC 地址是网卡的物理地址，形如 "AA:BB:CC:11:22:33"。
> 由于安卓 6.0 以后系统出于隐私限制，普通 App 多数情况下拿不到真实 MAC，
> 方法内部会依次尝试从 WiFi 信息、网卡接口、系统文件多处读取；都失败时返回 null。

- 返回 : {string} MAC 地址字符串；读取失败时返回 null
- 版本 : 1.0.0


```javascript
//读取本机 WiFi 的 MAC 地址
var mac = $device.getMacAddress();
log("mac地址:" + mac);   //被系统限制时可能为 null
```


### hasNavBar()

> 是否存在导航栏

- 返回 : {boolean} 屏幕底部有虚拟导航栏（那排返回/主页按键）返回 true，没有（手势或实体键）返回 false
- 版本 : 1.0.0


```javascript
// 是否存在导航栏
log("是否存在导航栏:",$device.hasNavBar());
```


### getVirtualBarHeight()

> 获取虚拟导航栏高度

- 返回 : {int} 屏幕底部虚拟导航栏的高度，单位像素；没有导航栏时为 0
- 版本 : 1.0.0


```javascript
// 导航栏高度
log("导航栏高度:",$device.getVirtualBarHeight());
```


### isLock()

> 检查设备是否锁定

- 返回 : {boolean} 屏幕当前处于锁屏（键盘锁）状态返回 true，已解锁返回 false
- 版本 : 1.0.0


```javascript
// 设备是否锁定
log("设备是否锁定:",$device.isLock());
```


