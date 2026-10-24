# $root - ROOT与Shell命令

- 更新时间:2026-10-22 10:55:50

> Root 权限与 Shell 命令工具对象（脚本里的全局对象 $root）。
> 
> 它让脚本以“管理员（Root）”身份执行系统命令，能力远大于普通权限：
> <ul>
>     <li>查权限：hasPermit 判断是否已拿到 Root，getPermit 主动申请；</li>
>     <li>模拟操作：click 点击、press 长按、move 滑动、home/back/menu 系统键、input 输入文字；</li>
>     <li>跑命令：exeRootShell 以 Root 身份跑 shell，exeShell 以普通身份跑 shell；</li>
>     <li>改设置：锁屏/解锁、电源键、改分辨率/DPI、强停应用等。</li>
> </ul>
> 注意：绝大多数方法都需要设备已经 Root。脚本一启动会自动尝试申请一次 Root。



```javascript
//先看看有没有 Root 权限
var hasRoot = $root.hasPermit();
if (hasRoot) {
    log("已经有 Root 权限，可以执行 $root 命令");
} else {
    log("没有 Root 权限");
}
```




### 有权限()

> 检查是否拥有 Root 权限（hasPermit 的中文写法）。

- 返回 : {boolean} 已有 Root 权限返回 true，否则返回 false
- 版本 : 1.7.0


```javascript
//检查是否有 Root 权限
var has = $root.hasPermit();
log("是否有root权限：" + has);
```


### 获取权限()

> 主动申请 Root 权限（getPermit 的中文写法）。

- 返回 : {boolean} 成功获得 Root 返回 true，否则返回 false
- 版本 : 1.7.0


```javascript
//主动申请 Root 权限
var ok = $root.getPermit();
log("获取 Root 权限结果：" + ok);
```


### 指针授权(启用)

> 启用指针
> 
> 打开或者关闭开发者调试的指针位置选项

- 参数 : 启用 {boolean} true 开启指针位置显示，false 关闭
- 版本 : 1.7.0


```javascript
//打开指针位置显示
$管理员.指针授权(是);
```


### 点击(x, y)

> 点击
> 

- 参数 : x {int} 要点击位置的横坐标（像素）
- 参数 : y {int} 要点击位置的纵坐标（像素）
- 版本 : 1.7.0


```javascript
//点击手势
$管理员.点击(500,800);
```

```javascript
//点击手势
$root.click(500, 800);
```


### 点击(x, y, 时长)

> 点击
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : 时长 {int} 按住时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击手势(长按)
$管理员.点击(500,800,1500);
```


### 点击(x, y, 时长, 延迟)

> 点击
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : 时长 {int} 按住时长，单位毫秒
- 参数 : 延迟 {int} 执行前等待时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击手势(长按)(延迟一秒)
$管理员.点击(500,800,1500,100);
```


### 点击(坐标)

> 点击
> 

- 参数 : 坐标 {Number[]} 长度为 2 的数组，依次是 x、y 坐标
- 版本 : 1.7.0


```javascript
//点击
$管理员.点击([500,800]);
```


### 点击(坐标, 时长)

> 点击
> 

- 参数 : 坐标 {Number[]} 长度为 2 的数组，依次是 x、y
- 参数 : 时长 {int} 按住时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击
$管理员.点击([500,800],50);
```


### 点击(坐标, 时长, 延迟)

> 点击
> 

- 参数 : 坐标 {Number[]} 长度为 2 的数组，依次是 x、y
- 参数 : 时长 {int} 按住时长，单位毫秒
- 参数 : 延迟 {int} 执行前等待时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击
$管理员.点击([500,800],50,2000);
```


### 点击(坐标)

> 点击
> 

- 参数 : 坐标 {Point} 要点击位置的点对象（含 x、y 字段）
- 版本 : 1.7.0


```javascript
//点击手势：先建一个点对象
var 位置 = new org.opencv.core.Point(500, 800);
$root.click(位置);
```


### 点击(坐标, 时长)

> 点击
> 

- 参数 : 坐标 {Point} 要点击位置的点对象
- 参数 : 时长 {int} 按住时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击并长按：先建点对象
var 位置 = new org.opencv.core.Point(500, 800);
$root.click(位置, 1500);
```


### 点击(坐标, 时长, 延迟)

> 点击
> 

- 参数 : 坐标 {Point} 要点击位置的点对象
- 参数 : 时长 {int} 按住时长，单位毫秒
- 参数 : 延迟 {int} 执行前等待时长，单位毫秒
- 版本 : 1.7.0


```javascript
//先等待再长按：先建点对象
var 位置 = new org.opencv.core.Point(500, 800);
$root.click(位置, 1500, 100);
```


### 长按(x, y)

> 长按
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 版本 : 1.7.0


```javascript
//点击手势(长按)(延迟一秒)
$管理员.长按(500,800);
```


### 长按(x, y, 时长)

> 长按
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : 时长 {int} 按住时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击手势(长按)(延迟一秒)
$管理员.长按(500,800,1500);
```


### 长按(x, y, 时长, 延迟)

> 长按
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : 时长 {int} 按住时长，单位毫秒
- 参数 : 延迟 {int} 执行前等待时长，单位毫秒
- 版本 : 1.7.0


```javascript
//点击手势(长按)(延迟一秒)
$管理员.长按(500,800,1500,100);
```


### 滑动(x1, y1, x2, y2)

> 滑动
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 版本 : 1.7.0


```javascript
//滑动手势
$管理员.滑动(500,0,500,800);
```


### 滑动(x1, y1, x2, y2, 时长)

> 滑动
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : 时长 {int} 滑动全程用时，单位毫秒
- 版本 : 1.7.0


```javascript
//滑动手势
$管理员.滑动(500,0,500,800,500);
```


### 滑动(x1, y1, x2, y2, 时长, 延迟)

> 滑动
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : 时长 {int} 滑动全程用时，单位毫秒
- 参数 : 延迟 {int} 执行前等待时长，单位毫秒
- 版本 : 1.7.0


```javascript
//滑动手势
$管理员.滑动(500,0,500,800,500.1000);
```


### 锁屏()

> 锁屏

- 版本 : 1.7.0


```javascript
$管理员.锁屏();
```


### 解锁屏幕()

> 解锁屏幕

- 版本 : 1.7.0


```javascript
$管理员.解锁屏幕();
```


### 电源键()

> 电源按键

- 版本 : 1.7.0


```javascript
$管理员.电源键();
```


### 执行(命令)

> 以 Root 身份执行一条 shell 命令（exec 的中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 版本 : 1.7.0


```javascript
//列一下 /system 目录
$root.exec("ls /system");
```


### 执行root命令(命令)

> 以 Root 身份执行一条 shell 命令（exeRootShell 的中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 版本 : 1.7.0


```javascript
//以 Root 身份查看 mac 地址文件
$root.exeRootShell("cat /sys/class/net/wlan0/address");
```


### 执行root命令(命令, 输出回调)

> 以 Root 身份执行命令，并逐行接收输出（中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 输出回调，每输出一行调用一次
- 版本 : 1.7.0


```javascript
//查看系统网络配置，每行输出都回调
$root.exeRootShell("cat /data/misc/dhcp/mac", function(line) {
    log(line);
});
```


### 执行root命令(命令, 输出回调, 中止回调)

> 以 Root 身份执行命令，接收输出并在异常终止时回调（中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 每输出一行调用一次
- 参数 : 中止回调 {function} 命令异常终止时调用，参数是原因
- 版本 : 1.7.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
});
```


### 执行root命令(命令, 输出回调, 中止回调, 完成回调)

> 以 Root 身份执行命令的完整版（中文写法）：输出、中止、完成三种回调。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 每输出一行调用一次
- 参数 : 中止回调 {function} 命令异常终止时调用
- 参数 : 完成回调 {function} 命令执行完毕时调用，参数是退出码
- 版本 : 1.7.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
}, function(exitCode) {
    log("执行完毕，退出码：" + exitCode);
});
```


### 同步执行root命令(命令)

> 以 Root 身份同步执行命令并返回输出（中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 返回 : {string} 命令的完整标准输出（多行字符串）
- 版本 : 1.9.1


```javascript
//罗列根目录文件列表
var res = $root.exeRootShellSync("ls /");
//按行切开并遍历
var fileArr = res.split("\n");
for (var i = 0; i < fileArr.length; i++) {
    log("第" + i + "项：" + fileArr[i]);
}
```


### 执行shell(命令)

> 以普通身份执行 shell 命令（exeShell 的中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 版本 : 1.7.0


```javascript
//列出 sdcard 图片目录
$root.exeShell("ls /sdcard/Pictures");
```


### 执行shell(命令, 输出回调)

> 以普通身份执行 shell 命令并逐行接收输出（中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 每输出一行调用一次
- 版本 : 1.7.0


```javascript
//列出 sdcard 目录
$root.exeShell("ls /sdcard", function(line) {
    log(line);
});
```


### 执行shell(命令, 输出回调, 中止回调)

> 以普通身份执行 shell 命令，接收输出并在异常终止时回调（中文写法）。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 每输出一行调用一次
- 参数 : 中止回调 {function} 命令异常终止时调用
- 版本 : 1.7.0


```javascript
//列出图片目录
$root.exeShell("ls /sdcard/Pictures", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
});
```


### 执行shell(命令, 输出回调, 中止回调, 完成回调)

> 以普通身份执行 shell 命令完整版（中文写法）：输出、中止、完成三种回调。

- 参数 : 命令 {string} 要执行的 shell 命令字符串
- 参数 : 输出回调 {function} 每输出一行调用一次
- 参数 : 中止回调 {function} 命令异常终止时调用
- 参数 : 完成回调 {function} 命令执行完毕时调用，参数是退出码
- 版本 : 1.7.0


```javascript
//列出图片目录
$root.exeShell("ls /sdcard/Pictures", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
}, function(exitCode) {
    log("执行结束，退出码：" + exitCode);
});
```


### 关闭root命令()

> 关闭 Root shell 会话（closeRootShell 的中文写法）。

- 版本 : 1.7.0


```javascript
//关闭 Root shell
$root.closeRootShell();
```


### 关闭shell命令()

> 关闭普通 shell 会话（closeShell 的中文写法）。

- 版本 : 1.7.0


```javascript
//关闭普通 shell
$root.closeShell();
```


### 关闭所有()

> 关闭所有

- 版本 : 1.7.0


```javascript
$管理员.关闭所有();
```


### 输入(文本)

> 输入文本

- 参数 : 文本 {string} 要输入的文本内容
- 版本 : 1.7.0


```javascript
$管理员.输入("我是输入的文本");
```


### 杀死应用(包名)

> 强制停止指定应用（killApp 的中文写法）。

- 参数 : 包名 {string} 要杀掉的应用包名
- 版本 : 1.7.0


```javascript
//强制停止示例 App
$root.killApp("com.example.app");
```


### 罗列运行的应用(回调)

> 列出所有运行的应用

- 参数 : 回调 {function} 回调，每发现一个运行中的应用就调用一次，参数是包名
- 版本 : 1.7.0


```javascript
//列出所有正在运行的应用包名
$root.lsRunningApps(function(pkg) {
    log("正在运行：" + pkg);
});
```


### 主页()

> 回到主页

- 版本 : 1.7.0


```javascript
$管理员.主页();
```


### 返回()

> 返回按键

- 版本 : 1.7.0


```javascript
$管理员.返回();
```


### 菜单()

> 菜单按键

- 版本 : 1.7.0


```javascript
$管理员.菜单();
```


### 最近()

> 最近任务

- 版本 : 1.7.0


```javascript
$管理员.最近();
```


### 设置分辨率(宽度, 高度)

> 设置手机分辨率

- 参数 : 宽度 {int} 要设置的屏幕宽度（像素）
- 参数 : 高度 {int} 要设置的屏幕高度（像素）


```javascript
$管理员.设置分辨率(1080,2200);
```


### 设置dpi(密度因子)

> 设置屏幕密度 DPI（setDpi 的中文写法）。

- 参数 : 密度因子 {int} 要设置的屏幕密度数值
- 版本 : 1.7.0


```javascript
//把屏幕密度设为 320
$root.setDpi(320);
```


### 重置分辨率()

> 恢复默认分辨率和密度（resetWm 的中文写法）。

- 版本 : 1.7.0


```javascript
//恢复默认分辨率和密度
$root.resetWm();
```


### 按键(按键名称)

> 模拟按下指定名称的按键（key 的中文写法）。

- 参数 : 按键名称 {string} 要按的按键名称，例如 "KEYCODE_POWER"
- 版本 : 1.7.0


```javascript
//按一下电源键
$root.key("KEYCODE_POWER");
```


