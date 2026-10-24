# $permit - 权限工具

- 更新时间:2026-10-22 10:55:50

> 权限工具对象（脚本里写作 $permit），用来“申请”和“检查”安卓系统的各种权限。
> 
> 安卓为了保护隐私，很多功能（悬浮窗、无障碍、存储、相机、定位、短信、联系人等）都要先向用户申请、
> 用户同意后才能用。这个对象把每一种权限都封装成了一对方法：
> <ul>
>     <li>hasXxx()：检查“现在有没有这个权限”（只判断，不弹窗）；</li>
>     <li>xxx()：去“申请这个权限”（会跳到系统设置页或弹出授权框）。</li>
> </ul>
> 用户必须在系统界面完成授权；请求权限不代表系统一定会授予。
> 注意：在 $权限 中调用任何权限申请方法，一般只调用一次（已经有就不会重复弹）。



```javascript
//先检查有没有悬浮窗权限
var canFloat = $permit.hasFloaty();
if (!canFloat) {
    $permit.floaty(); //没有就去申请
}
```




### floaty()

> 申请悬浮窗权限（会跳到系统“显示在其他应用上层”的设置页）。
> 
> 悬浮窗权限是用来在别的 App 上面画按钮、提示框、画板的前提。调用后会跳到系统设置让用户手动开启，
> 开启后返回。已经有这个权限时不会重复跳。

- 版本 : 1.1.6


```javascript
//获取悬浮窗权限
$permit.floaty();
```


### hasFloaty()

> 检查是否已获得悬浮窗权限。
> 
> 返回 true 表示已经能在别的 App 上面画悬浮窗；false 表示还没开，需要先调 floaty() 去申请。

- 返回 : {boolean} 已有悬浮窗权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("悬浮窗权限：" + $permit.hasFloaty());
```


### wza()

> 申请无障碍权限（自动化脚本最核心的权限，用来读取界面、模拟点击）。
> 
> 无障碍权限是 AutoGod 自动化的基础：没有它就没法自动识别界面控件、自动点击滑动。
> 调用后会跳到系统无障碍设置页让用户手动开启本服务。
> 
> 如果已经有 Root 或 Shizuku 权限，它还会尝试用这两条路自动开启无障碍，免去手动去设置里找。
> 已经有无障碍权限时直接返回，不会重复弹。

- 版本 : 1.1.6


```javascript
//获取无障碍权限
$permit.wza();
```


### hasWza()

> 检查是否已获得无障碍权限。
> 
> 返回 true 表示无障碍服务已开启、可以自动操作界面；false 表示还没开，需要先调 wza() 去申请。

- 返回 : {boolean} 无障碍服务已开启返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("无障碍权限：" + $permit.hasWza());
```


### sd()

> 申请存储（读写存储卡）权限。
> 
> 用来读写手机里的文件、保存截图等。调用后会弹出系统授权框让用户同意。已经有权限时直接返回，不重复弹。

- 版本 : 1.1.6


```javascript
//获取存储权限
$permit.sd();
```


### hasSd()

> 检查是否已获得存储权限。
> 
> 返回 true 表示已经能读写存储卡文件；false 表示还没授权，需要先调 sd() 去申请。

- 返回 : {boolean} 已有存储权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("存储权限：" + $permit.hasSd());
```


### call()

> 申请电话（拨打/状态）权限。
> 
> 用来拨打电话、读取手机状态等。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取电话权限
$permit.call();
```


### hasCall()

> 检查是否已获得电话权限。
> 
> 返回 true 表示已经允许打电话/读手机状态；false 表示还没授权，需要先调 call() 去申请。

- 返回 : {boolean} 已有电话权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("电话权限：" + $permit.hasCall());
```


### set()

> 申请“修改系统设置”权限（用来改亮度、屏幕方向等）。
> 
> 想让脚本修改屏幕亮度、自动旋转方向等系统设置，就需要这个权限。调用后会跳到系统设置页让用户手动开启。

- 版本 : 1.1.6


```javascript
//获取修改设置权限
$permit.set();
```


### hasSet()

> 检查是否已获得“修改系统设置”权限。
> 
> 返回 true 表示已经能改亮度、方向等系统设置；false 表示还没授权，需要先调 set() 去申请。

- 返回 : {boolean} 已有修改系统设置权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("修改系统设置权限：" + $permit.hasSet());
```


### net()

> 申请网络访问权限。
> 
> 脚本要联网（$http 请求、WebSocket 等）就需要这个权限。调用后会弹出系统授权框让用户同意；已有则直接返回。

- 版本 : 1.1.6


```javascript
//获取网络权限
$permit.net();
```


### hasNet()

> 检查是否已获得网络权限。
> 
> 返回 true 表示已经允许联网；false 表示还没授权，需要先调 net() 去申请。

- 返回 : {boolean} 已有网络权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("网络权限：" + $permit.hasNet());
```


### camera()

> 申请相机权限。
> 
> 想用摄像头拍照、扫码等就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取相机权限
$permit.camera();
```


### hasCamera()

> 检查是否已获得相机权限。
> 
> 返回 true 表示已经允许用摄像头；false 表示还没授权，需要先调 camera() 去申请。

- 返回 : {boolean} 已有相机权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("相机权限：" + $permit.hasCamera());
```


### record()

> 申请录音（麦克风）权限。
> 
> 想用麦克风录音、语音识别等就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取录音权限
$permit.record();
```


### hasRecord()

> 检查是否已获得麦克风（录音）权限。
> 
> 返回 true 表示已经允许用麦克风录音；false 表示还没授权，需要先调 record() 去申请。

- 返回 : {boolean} 已有录音权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("录音权限：" + $permit.hasRecord());
```


### readSms()

> 申请“读取短信”权限。
> 
> 想自动读取收到的短信（比如自动填验证码）就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取读取信息权限
$permit.readSms();
```


### hasReadSms()

> 检查是否已获得“读取短信”权限。
> 
> 返回 true 表示已经允许读短信；false 表示还没授权，需要先调 readSms() 去申请。

- 返回 : {boolean} 已有读取短信权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("读取短信权限：" + $permit.hasReadSms());
```


### sendSms()

> 申请“发送短信”权限。
> 
> 想让脚本自动发短信就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取发送信息权限
$permit.sendSms();
```


### hasSendSms()

> 检查是否已获得“发送短信”权限。
> 
> 返回 true 表示已经允许发短信；false 表示还没授权，需要先调 sendSms() 去申请。

- 返回 : {boolean} 已有发送短信权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("发送短信权限：" + $permit.hasSendSms());
```


### readContact()

> 申请“读取联系人”权限。
> 
> 想读取手机里的通讯录联系人就需要这个权限。调用后会弹出系统授权框让用户同意；已有则直接返回。

- 版本 : 1.1.6


```javascript
//获取读取联系人权限
$permit.readContact();
```


### hasReadContact()

> 检查是否已获得“读取联系人”权限。
> 
> 返回 true 表示已经能读通讯录；false 表示还没授权，需要先调 readContact() 去申请。

- 返回 : {boolean} 已有读取联系人权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("读取联系人权限：" + $permit.hasReadContact());
```


### writeContact()

> 申请“写入联系人”权限。
> 
> 想往通讯录里新增/修改联系人就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取写入联系人权限
$permit.writeContact();
```


### hasWriteContact()

> 检查是否已获得“写入联系人”权限。
> 
> 返回 true 表示已经能改通讯录；false 表示还没授权，需要先调 writeContact() 去申请。

- 返回 : {boolean} 已有写入联系人权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("写入联系人权限：" + $permit.hasWriteContact());
```


### loc()

> 申请定位权限。
> 
> 想获取手机位置（GPS/WiFi 定位）就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.1.6


```javascript
//获取定位权限
$permit.loc();
```


### hasLoc()

> 检查是否已获得定位权限。
> 
> 返回 true 表示已经允许定位；false 表示还没授权，需要先调 loc() 去申请。

- 返回 : {boolean} 已有定位权限返回 true，否则返回 false
- 版本 : 1.1.6


```javascript
log("定位权限：" + $permit.hasLoc());
```


### readCalendar()

> 申请“读取日历”权限。
> 
> 想读取手机日历里的日程就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.2.2


```javascript
//获取读取日历权限
$permit.readCalendar();
```


### hasReadCalendar()

> 检查是否已获得“读取日历”权限。
> 
> 返回 true 表示已经能读日历日程；false 表示还没授权，需要先调 readCalendar() 去申请。

- 返回 : {boolean} 已有读取日历权限返回 true，否则返回 false
- 版本 : 1.2.2


```javascript
log("读取日历权限：" + $permit.hasReadCalendar());
```


### writeCalendar()

> 申请“写入日历”权限。
> 
> 想往手机日历里新增/修改日程就需要这个权限。调用后会弹出系统授权框让用户同意。

- 版本 : 1.2.2


```javascript
//获取写入日历权限
$permit.writeCalendar();
```


### hasWriteCalendar()

> 检查是否已获得“写入日历”权限。
> 
> 返回 true 表示已经能改日历日程；false 表示还没授权，需要先调 writeCalendar() 去申请。

- 返回 : {boolean} 已有写入日历权限返回 true，否则返回 false
- 版本 : 1.2.2


```javascript
log("写入日历权限：" + $permit.hasWriteCalendar());
```


### hasPermit(permitName)

> 按权限名检查“某一个”权限有没有（通用版，可查任意安卓权限）。
> 
> 上面那些 hasXxx 都是封装好的常用权限；这个方法更通用，传入安卓权限的完整名字就能查。
> 权限名有两种写法，完全等价："android.Manifest.permission.XXX" 或简写 "android.permission.XXX"。

- 参数 : permitName {string} 要查询的安卓权限全名，例如 "android.permission.CAMERA"
- 返回 : {boolean} 已授予该权限返回 true，否则返回 false（传空串也返回 false）
- 版本 : 1.2.2


```javascript
//判断是否有获取账号列表权限
var ok = $permit.hasPermit("android.Manifest.permission.GET_ACCOUNTS");
//等同于
var ok2 = $permit.hasPermit("android.permission.GET_ACCOUNTS");
log("是否有该权限：" + ok);
```


### hasPermit(permitNames)

> 一次性检查“一组”权限是否全部都有。
> 
> 传一个权限名数组，只要其中有任意一个没授权就返回 false；全部都有才返回 true。
> 空数组或 null 直接返回 false。

- 参数 : permitNames {string[]} 要检查的权限名数组，例如 ["android.permission.READ_CALENDAR", ...]
- 返回 : {boolean} 数组里每一个权限都已授予才返回 true，否则（含空数组）返回 false
- 版本 : 1.2.2


```javascript
//要同时检查的一组权限
var permits = ["android.permission.READ_CALENDAR", "android.permission.WRITE_CALENDAR"];
//判断这一组是否全部都有权限
var allOk = $permit.hasPermit(permits);
log("日历读写权限是否齐全：" + allOk);
```


### getPermit(permitNames)

> 一次性申请“一组”权限。
> 
> 传一个权限名数组，系统会弹出授权框，让用户一次性同意这一组权限。空数组直接返回不弹窗。

- 参数 : permitNames {string[]} 要申请的权限名数组
- 版本 : 1.2.2


```javascript
//要申请的一组权限
var permits = ["android.permission.READ_CALENDAR", "android.permission.WRITE_CALENDAR"];
//弹出授权框申请这一组权限
$permit.getPermit(permits);
```


### getPermit(permitName)

> 申请“某一个”权限（通用版，可申请任意安卓权限）。
> 
> 传入安卓权限全名，系统会弹授权框让用户同意。权限名两种写法等价：
> "android.Manifest.permission.XXX" 或 "android.permission.XXX"。空串直接返回不弹窗。

- 参数 : permitName {string} 要申请的安卓权限全名，例如 "android.permission.CAMERA"
- 版本 : 1.2.2


```javascript
//申请获取账号列表权限
$permit.getPermit("android.Manifest.permission.GET_ACCOUNTS");
//等同于
$permit.getPermit("android.permission.GET_ACCOUNTS");
```


### hasNotifyAccess()

> 检查是否已获得“通知访问”权限。
> 
> 有了这个权限，脚本才能读取收到的通知（比如监听某 App 弹了什么通知）。
> 返回 true 表示已开通知监听；false 表示还没开，需要先调 notifyAccess() 去申请。

- 返回 : {boolean} 已授予通知访问权限返回 true，否则返回 false
- 版本 : 1.6.4


```javascript
var result = $permit.hasNotifyAccess();
log("通知访问权限：" + result);
```


### notifyAccess()

> 申请“通知访问”权限（会跳到系统通知监听设置页）。
> 
> 有了它脚本才能读取收到的通知。调用后会跳到系统通知监听设置让用户手动开启本应用的监听；
> 已经有权限时不会再跳。

- 版本 : 1.6.4


```javascript
$permit.notifyAccess();
```


### hasReadVideo()

> 检查是否已获得“读取视频”权限。
> 
> 用来读手机里存的视频文件。安卓 13 及以上单独要“读视频”权限，老版本则用总的存储权限；
> 本方法已帮你按系统版本判断好。返回 true 表示能读视频，false 表示需先调 readVideo() 申请。

- 返回 : {boolean} 已可读取视频返回 true，否则返回 false
- 版本 : 1.6.4


```javascript
var result = $permit.hasReadVideo();
log("读取视频权限：" + result);
```


### readVideo()

> 申请“读取视频”权限。
> 
> 调用后按系统版本弹出对应授权框：安卓 13 及以上申请“读视频”，老版本申请总的存储权限。
> 已经有权限时不会重复弹。

- 版本 : 1.6.4


```javascript
$permit.readVideo();
```


### hasReadImage()

> 检查是否已获得“读取图片”权限。
> 
> 用来读手机相册里的图片。安卓 13 及以上单独要“读图片”权限，老版本用总的存储权限，本方法已按版本判断好。
> 返回 true 表示能读图片，false 表示需先调 readImage() 申请。

- 返回 : {boolean} 已可读取图片返回 true，否则返回 false
- 版本 : 1.6.4


```javascript
var result = $permit.hasReadImage();
log("读取图片权限：" + result);
```


### readImage()

> 申请“读取图片”权限。
> 
> 调用后按系统版本弹出对应授权框：安卓 13 及以上申请“读图片”，老版本申请总的存储权限。

- 版本 : 1.6.4


```javascript
$permit.readImage();
```


### hasReadAudio()

> 检查是否已获得“读取音频”权限。
> 
> 用来读手机里存的音乐、录音等音频文件。安卓 13 及以上单独要“读音频”权限，老版本用总的存储权限。
> 返回 true 表示能读音频，false 表示需先调 readAudio() 申请。

- 返回 : {boolean} 已可读取音频返回 true，否则返回 false
- 版本 : 1.6.4


```javascript
var result = $permit.hasReadAudio();
log("读取音频权限：" + result);
```


### readAudio()

> 申请“读取音频”权限。
> 
> 调用后按系统版本弹出对应授权框：安卓 13 及以上申请“读音频”，老版本申请总的存储权限。

- 版本 : 1.6.4


```javascript
$permit.readAudio();
```


### hasReadMedia()

> 检查是否已获得“读取媒体”综合权限。
> 
> 这个方法一次性检查图片、音频、视频三类媒体是否都能读（老版本则检查总的存储权限）。
> 全部都有才返回 true，有任意一个缺失就返回 false。

- 返回 : {boolean} 图片、音频、视频读取权限全部具备返回 true，否则返回 false
- 版本 : 1.6.4


```javascript
var result = $permit.hasReadMedia();
log("读取媒体权限：" + result);
```


### readMedia()

> 申请“读取媒体”综合权限。
> 
> 一次性把还缺的图片、音频、视频读取权限都列出来去申请（老版本则申请总的存储权限）。
> 已经具备的不会重复申请。

- 版本 : 1.6.4


```javascript
$permit.readMedia();
```


