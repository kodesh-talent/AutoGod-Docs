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




### hasPermit()

> 检查当前是否已经拥有 Root 权限。
> 
> 它会悄悄试着执行一条 su 命令探测：能成功就是已 Root，否则没有。
> 结果会被记住，重复调用很快。

- 返回 : {boolean} 已有 Root 权限返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
//检查是否有 Root 权限
var has = $root.hasPermit();
log("是否有root权限：" + has);
```


### getPermit()

> 主动申请并激活 Root 权限。
> 
> 如果还没拿到 Root，会尝试弹授权框并执行一条需要 Root 的命令来确认。
> 返回 true 表示 Root 可用，false 表示当前设备没 Root 或授权被拒。

- 返回 : {boolean} 成功获得并可用 Root 返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
//主动申请 Root 权限
var ok = $root.getPermit();
log("获取 Root 权限结果：" + ok);
```


### enablePointer(enable)

> 打开或关闭“指针位置”调试开关。
> 
> 这是开发者选项里的功能：开启后屏幕上会显示手指触控的轨迹和坐标，
> 调脚本时非常有用，能看清点击到底落在了哪里。

- 参数 : enable {boolean} true 表示开启指针位置显示，false 表示关闭
- 版本 : 1.4.1


```javascript
//打开指针位置显示，屏幕上会画出触控轨迹
$root.enablePointer(true);
//用完再关掉
// $root.enablePointer(false);
```


### click(x, y)

> 执行点击。
> 

- 参数 : x {int} 要点击位置的横坐标（像素）
- 参数 : y {int} 要点击位置的纵坐标（像素）
- 版本 : 1.0.0


```javascript
//点击手势
$root.click(500,800);
```

```javascript
//点击手势
$root.click(500, 800);
```


### click(x, y, dur)

> 执行点击。
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : dur {int} 按住时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)
$root.click(500,800,1500);
```


### click(x, y, dur, delay)

> 执行点击。
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : dur {int} 按住时长，单位毫秒
- 参数 : delay {int} 执行前等待时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.click(500,800,1500,100);
```


### click(index)

> 执行点击。
> 

- 参数 : index {Number[]} 长度为 2 的数组，依次是 x、y 坐标
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800]);
```


### click(index, dur)

> 执行点击。
> 

- 参数 : index {Number[]} 长度为 2 的数组，依次是 x、y 坐标
- 参数 : dur {int} 按住时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800],50);
```


### click(index, dur, delay)

> 执行点击。
> 

- 参数 : index {Number[]} 长度为 2 的数组，依次是 x、y
- 参数 : dur {int} 按住时长，单位毫秒
- 参数 : delay {int} 执行前等待时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800],50,2000);
```


### click(index)

> 执行点击。
> 

- 参数 : index {Point} 要点击位置的点对象（含 x、y 字段）
- 版本 : 1.0.0


```javascript
//点击手势
var point = new org.opencv.core.Point(500,800);
$root.click(point);
```


### click(index, dur)

> 执行点击。
> 

- 参数 : index {Point} 要点击位置的点对象
- 参数 : dur {int} 按住时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
var point = new org.opencv.core.Point(500,800);
$root.click(point,1500);
```


### click(index, dur, delay)

> 执行点击。
> 

- 参数 : index {Point} 要点击位置的点对象
- 参数 : dur {int} 按住时长，单位毫秒
- 参数 : delay {int} 执行前等待时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
var point = new org.opencv.core.Point(500,800);
$root.click(point,1500,100);
```


### press(x, y)

> 执行长按。
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800);
```


### press(x, y, dur)

> 执行长按。
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : dur {int} 按住时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800,1500);
```


### press(x, y, dur, delay)

> 执行长按。
> 

- 参数 : x {int} 位置横坐标（像素）
- 参数 : y {int} 位置纵坐标（像素）
- 参数 : dur {int} 按住时长，单位毫秒
- 参数 : delay {int} 执行前等待时长，单位毫秒
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800,1500,100);
```


### move(x1, y1, x2, y2)

> 执行滑动。
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800);
```


### move(x1, y1, x2, y2, dur)

> 执行滑动。
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 滑动全程用时，单位毫秒
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800,500);
```


### move(x1, y1, x2, y2, dur, delay)

> 执行滑动。
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 滑动全程用时，单位毫秒
- 参数 : delay {int} 执行前等待时长，单位毫秒
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800,500.1000);
```


### lock()

> 锁定屏幕。

- 版本 : 1.0.0


```javascript
$root.lock();
```


### unlock()

> 点亮并解锁屏幕（唤醒设备）。
> 
> 如果屏幕本来就是亮的，则什么都不做；如果是息屏状态，就模拟电源键点亮屏幕。

- 版本 : 1.0.0


```javascript
//点亮/解锁屏幕
$root.unlock();
```


### power()

> 模拟按下电源键（亮屏/息屏切换）。
> 
> 相当于按一下手机的电源键：亮着就熄、熄着就亮。

- 版本 : 1.0.9


```javascript
//按一下电源键
$root.power();
```


### exec(cmd)

> 以 Root 身份执行一条 shell 命令（不关心输出）。
> 
> 这是最直接的 Root 命令入口，命令在 Root 环境里跑。
> 注意：这里执行的是 Linux 命令，写错（尤其涉及删/system、改分区）可能让设备变砖，请谨慎。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 版本 : 1.5.9


```javascript
//列一下 /system 目录
$root.exec("ls /system");
```


### exeRootShell(cmd)

> 以 Root 身份执行一条 shell 命令（不关心输出）。
> 
> 和 exec 作用相同，在 Root 环境里跑命令，输出被忽略。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 版本 : 1.0.0


```javascript
//以 Root 身份查看 mac 地址文件
$root.exeRootShell("cat /sys/class/net/wlan0/address");
```


### exeRootShell(cmd, output)

> 以 Root 身份执行命令，并逐行接收输出。
> 
> 命令每打印一行，就会回调一次 output 函数，把这行文字传进来。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 输出回调，每输出一行调用一次，参数是这行文字
- 版本 : 1.0.0


```javascript
//查看系统网络配置，每行输出都回调
$root.exeRootShell("cat /data/misc/dhcp/mac", function(line) {
    log(line);
});
```


### exeRootShell(cmd, output, terminate)

> 以 Root 身份执行命令，接收输出并在命令异常终止时收到回调。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 输出回调，每输出一行调用一次
- 参数 : terminate {function} 命令异常终止时的回调，参数是原因字符串
- 版本 : 1.0.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
});
```


### exeRootShell(cmd, output, terminate, complete)

> 以 Root 身份执行命令的完整版：接收输出、异常终止、执行完毕三种回调。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 每输出一行调用一次
- 参数 : terminate {function} 命令异常终止时调用，参数是原因
- 参数 : complete {function} 命令正常执行完毕时调用，参数是退出码（0 表示成功）
- 版本 : 1.0.0


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


### exeRootShellSync(cmd)

> 以 Root 身份同步执行命令，并把全部输出作为字符串返回。
> 
> 这个方法会“卡住等待”命令跑完，直接把输出结果返回，
> 适合想立刻拿到结果再往下写逻辑的场景。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 返回 : {string} 命令的完整标准输出（多行字符串）；异常时可能返回错误原因
- 版本 : 1.9.1


```javascript
//罗列根目录文件列表
var res = $root.exeRootShellSync("ls /");
//处理结果
var fileArr = res.split("\n");
for (var i = 0; i < fileArr.length; i++) {
    log("第" + i + "项：" + fileArr[i]);
}
```


### exeShell(cmd)

> 以普通（非 Root）身份执行一条 shell 命令，不接收输出。
> 
> 和 exeRootShell 的区别：这条命令跑在普通 shell 里，没有 Root 权限，
> 只能访问普通应用能碰的东西。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 版本 : 1.0.0


```javascript
//列出 sdcard 图片目录
$root.exeShell("ls /sdcard/Pictures");
```


### exeShell(cmd, output)

> 以普通身份执行 shell 命令，并逐行接收输出。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 输出回调，每输出一行调用一次
- 版本 : 1.0.0


```javascript
//列出 sdcard 目录，每行输出回调
$root.exeShell("ls /sdcard", function(line) {
    log(line);
});
```


### exeShell(cmd, output, terminate)

> 以普通身份执行 shell 命令，接收输出并在异常终止时回调。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 每输出一行调用一次
- 参数 : terminate {function} 命令异常终止时调用，参数是原因
- 版本 : 1.0.0


```javascript
//列出图片目录
$root.exeShell("ls /sdcard/Pictures", function(line) {
    log(line);
}, function(err) {
    $log.e(err);
});
```


### exeShell(cmd, output, terminate, complete)

> 以普通身份执行 shell 命令完整版：输出、中止、完成三种回调。

- 参数 : cmd {string} 要执行的 shell 命令字符串
- 参数 : output {function} 每输出一行调用一次
- 参数 : terminate {function} 命令异常终止时调用
- 参数 : complete {function} 命令执行完毕时调用，参数是退出码
- 版本 : 1.0.0


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


### closeRootShell()

> 关闭 Root shell 会话。
> 
> 脚本结束或长时间不再用 Root 命令时调用，释放 Root shell 连接，省电省资源。

- 版本 : 1.0.0


```javascript
//关闭 Root shell
$root.closeRootShell();
```


### closeShell()

> 关闭普通 shell 会话。
> 
> 释放 exeShell 用的普通 shell 连接。

- 版本 : 1.0.0


```javascript
//关闭普通 shell
$root.closeShell();
```


### closeAll()

> 关闭所有 shell 会话（Root 的和普通的都关掉）。
> 
> 脚本结束前调用最省事，一次性释放所有 shell 连接。

- 版本 : 1.0.0


```javascript
//脚本结束前关闭所有 shell
$root.closeAll();
```


### input(text)

> 通过 Root 的 input 命令，在当前聚焦的输入框里输入文字。
> 
> 适合输入英文和数字；空格会被自动处理。中文一般用粘贴方式。

- 参数 : text {string} 要输入的文本内容
- 版本 : 1.0.0


```javascript
//在当前输入框输入一段文字
$root.input("hello123");
```


### killApp(pkgName)

> 强制停止（杀掉）指定包名的应用。
> 
> 相当于设置里“强行停止”，把某个 App 整个关掉。需要 Root。

- 参数 : pkgName {string} 要杀掉的应用包名，比如 com.example.app
- 版本 : 1.0.4


```javascript
//强制停止示例 App
$root.killApp("com.example.app");
```


### lsRunningApps(callback)

> 罗列当前正在运行的应用，逐个通过回调返回包名。
> 
> 它会读取系统进程列表，每发现一个带包名的进程，就回调一次把包名传给你。

- 参数 : callback {function} 回调，每发现一个运行中的应用就调用一次，参数是包名字符串
- 版本 : 1.0.4


```javascript
//列出所有正在运行的应用包名
$root.lsRunningApps(function(pkg) {
    log("正在运行：" + pkg);
});
```


### home()

> 返回桌面。

- 版本 : 1.0.9


```javascript
$root.home();
```


### back()

> 模拟按下返回键。
> 
> 相当于按底部的返回箭头，回到上一页。

- 版本 : 1.0.9


```javascript
//按下返回键
$root.back();
```


### menu()

> 模拟按下菜单/多任务键。

- 版本 : 1.0.9


```javascript
//按下菜单键
$root.menu();
```


### recent()

> 打开最近任务界面。

- 版本 : 1.0.9


```javascript
$root.recent();
```


### setWmSize(width, height)

> 设置屏幕分辨率。

- 参数 : width {int} 要设置的屏幕宽度（像素）
- 参数 : height {int} 要设置的屏幕高度（像素）


```javascript
$root.setWmSize(1080,2200);
```


### setDpi(density)

> 设置屏幕分辨率。

- 参数 : density {int} 要设置的屏幕密度（DPI）数值，越大显示越细腻
- 版本 : 1.5.4


```javascript
$root.setDpi(320);
```


### resetWm()

> 把屏幕分辨率和密度恢复成系统默认。
> 
> 之前如果用 setWmSize/setDpi 改过显示，用这个一键还原。

- 版本 : 1.5.4


```javascript
//恢复默认分辨率和密度
$root.resetWm();
```


### key(keyName)

> 模拟按键。

- 参数 : keyName {string} 要按的按键名称，例如 "KEYCODE_POWER"、"KEYCODE_BACK"
- 版本 : 1.5.9


```javascript
$root.key("KEYCODE_POWER");
```


