# $szk - Shizuku工具

- 更新时间:2026-10-22 10:55:51

> Shizuku 工具对象（脚本里写作 $szk，中文名叫 $始祖库）。
> 
> Shizuku 是一个能让 App 以"系统级权限"执行操作的工具。装好并开启 Shizuku 后，$szk 就能帮你
> 做一些普通权限做不到的事：模拟点击/滑动、长按、返回/主页键、输入文字、强停应用、改分辨率、
> 直接执行 shell 命令等。
> 
> 新手提示：用之前要先确认 Shizuku 已经授权。脚本里先调用 hasPermit 检查，没权限就调用
> getPermit 去申请。很多手势 $act 已经封装好了，Shizuku 可用时底层会自动走这里。



```javascript
// 先检查 Shizuku 权限有没有拿到
var allowed = $szk.hasPermit();
if (allowed) {
    log("Shizuku 已授权，可以使用 $szk");
} else {
    log("还没授权，先调用 $szk.getPermit()");
}
```




### getPermit()

> 申请并等待 Shizuku 权限（会一直阻塞等待用户授权）。
> 
> 调用后会弹出 Shizuku 的授权请求，脚本会卡在这里反复检查，直到授权成功或 Shizuku 没开启才返回。
> 一般在脚本最开头调用一次即可。

- 版本 : 1.0.8


```javascript
// 申请 Shizuku 权限，阻塞等待结果
$szk.getPermit();
```


### hasPermit()

> 检查当前有没有 Shizuku 权限。
> 
> 做任何 Shizuku 操作前都先问一句。返回 true 表示已授权、可以用；false 表示还没授权，
> 需要先调用 getPermit 申请。

- 返回 : {boolean} 已授权返回 true，否则返回 false
- 版本 : 1.0.8


```javascript
// 检查权限
if ($szk.hasPermit()) {
    log("Shizuku权限已获取");
}
```


### enablePointer(enable)

> 打开或关闭开发者选项里的"指针位置"（屏幕触控轨迹显示）。
> 
> 调试点击时很有用：打开后屏幕上会显示手指点在哪、轨迹怎么走。传 true 开，false 关。

- 参数 : enable {boolean} true 打开，false 关闭
- 版本 : 1.4.1


```javascript
// 打开指针位置显示
$szk.enablePointer(true);
```


### waitPermit()

> 阻塞等待 Shizuku 权限就绪，直到拿到权限或失败。
> 
> 它会一直卡在这里等，直到授权成功才继续往下走。返回 true 表示拿到了权限。

- 返回 : {boolean} 成功拿到权限返回 true，否则返回 false
- 版本 : 1.2.0


```javascript
// 阻塞等待权限
var result = $szk.waitPermit();
log("是否拿到权限：" + result);
```


### waitPermit(callback)

> 异步等待 Shizuku 权限，结果通过回调告诉你。
> 
> 和阻塞版不同，这个方法不卡脚本，授权结果出来后会调用你传进去的回调函数。

- 参数 : callback {function(成功布尔)} 权限就绪后的回调函数
- 版本 : 1.2.0


```javascript
// 异步等待，完成后回调
$szk.waitPermit(function() {
    log("权限就绪");
});
```


### click(x, y)

> 在屏幕 (x, y) 位置点一下（模拟一次轻点）。
> 
> 底层走的是 shell 的 input tap。注意：$act 里已经封装好手势，Shizuku 可用时会自动走这里。

- 参数 : x {int} 点击位置的横坐标
- 参数 : y {int} 点击位置的纵坐标
- 版本 : 1.0.8


```javascript
// 在屏幕坐标 (500, 800) 处点一下
$szk.click(500, 800);
```


### click(x, y, dur)

> 在 (x, y) 位置按住一段时间（模拟长按）。
> 
> 第三个参数是按住的时长，单位毫秒。传 1000 就是长按 1 秒。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住时长，单位毫秒
- 版本 : 1.0.8


```javascript
// 在 (500, 800) 长按 1000 毫秒
$szk.click(500, 800, 1000);
```


### click(x, y, dur, delay)

> 先等一会，再在 (x, y) 位置长按指定时长。
> 
> 第四个参数是"点击前先等待多少毫秒"，用来在多步操作间留出间隔。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住时长（毫秒）
- 参数 : delay {int} 点击前先等待的毫秒数
- 版本 : 1.0.8


```javascript
// 先等 1000 毫秒，再在 (500,800) 长按 1000 毫秒
$szk.click(500, 800, 1000, 100);
```


### click(index)

> 用一个 [x, y] 数组来指定点击位置。
> 
> 第一个元素是横坐标，第二个是纵坐标。数组不足 2 个会警告并不执行。

- 参数 : index {int[]} 长度为 2 的数组 [x, y]
- 版本 : 1.0.8


```javascript
// 用数组表示要点击的位置
$szk.click([500, 800]);
```


### click(index, dur)

> 用 [x, y] 数组指定位置，并按住指定时长（长按）。

- 参数 : index {int[]} [x, y] 数组
- 参数 : dur {int} 按住毫秒数
- 版本 : 1.0.8


```javascript
// 在数组给出的位置长按 50 毫秒
$szk.click([500, 800], 50);
```


### click(index, dur, delay)

> 先等待 delay 毫秒，再在 [x, y] 位置长按 dur 毫秒。

- 参数 : index {int[]} [x, y] 数组
- 参数 : dur {int} 按住毫秒数
- 参数 : delay {int} 点击前等待毫秒数
- 版本 : 1.0.8


```javascript
// 先等 2000 毫秒，再在该位置点一下（持续 50 毫秒）
$szk.click([500, 800], 50, 2000);
```


### click(index)

> 用一个 Point 点对象来指定点击位置。
> 
> Point 通常由找图找色返回（比如 $img.findColor），也可以自己 importClass 后 new。

- 参数 : index {Point} 要点击的点对象
- 版本 : 1.0.8


```javascript
// 引入 Point 类并创建一个点
importClass(Packages.top.kodesh.app.clib.opencv.Point);
var point = new Point(500, 800);
// 在这个点上点一下
$szk.click(point);
```


### click(index, dur)

> 在 Point 点对象位置长按指定时长。

- 参数 : index {Point} 点对象
- 参数 : dur {int} 按住毫秒数
- 版本 : 1.0.8


```javascript
importClass(Packages.top.kodesh.app.clib.opencv.Point);
var point = new Point(500, 800);
// 在该点长按 1000 毫秒
$szk.click(point, 1000);
```


### click(index, dur, delay)

> 先等待 delay 毫秒，再在 Point 位置长按 dur 毫秒。

- 参数 : index {Point} 点对象
- 参数 : dur {int} 按住毫秒数
- 参数 : delay {int} 点击前等待毫秒数
- 版本 : 1.0.8


```javascript
importClass(Packages.top.kodesh.app.clib.opencv.Point);
var point = new Point(500, 800);
// 等 100 毫秒后长按 1000 毫秒
$szk.click(point, 1000, 100);
```


### press(x, y)

> 在 (x, y) 位置长按（默认按住 1 秒）。
> 
> 相当于 click 并按住 1000 毫秒。想自己定时长用带 dur 的版本。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 版本 : 1.0.8


```javascript
// 在 (500, 800) 长按 1 秒
$szk.press(500, 800);
```


### press(x, y, dur)

> 在 (x, y) 位置长按，并自己指定按住时长。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住毫秒数
- 版本 : 1.0.8


```javascript
// 在 (500, 800) 长按 1000 毫秒
$szk.press(500, 800, 1000);
```


### press(x, y, dur, delay)

> 先等待 delay 毫秒，再在 (x, y) 长按 dur 毫秒。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住毫秒数
- 参数 : delay {int} 操作前等待毫秒数
- 版本 : 1.0.8


```javascript
// 先等 100 毫秒，再长按 1500 毫秒
$szk.press(500, 800, 1500, 100);
```


### move(x1, y1, x2, y2)

> 从起点 (x1,y1) 滑动到终点 (x2,y2)（默认划 1 秒）。
> 
> 就是模拟一次手指拖动。比如从屏幕上半滑到下半，实现翻页。

- 参数 : x1 {int} 起点横坐标
- 参数 : y1 {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 版本 : 1.0.8


```javascript
// 从 (500,0) 滑到 (500,800)，模拟上滑翻页
$szk.move(500, 0, 500, 800);
```


### move(x1, y1, x2, y2, dur)

> 从起点滑到终点，并自己指定滑动耗时。
> 
> 时间越长滑得越慢，时间越短滑得越快。

- 参数 : x1 {int} 起点横坐标
- 参数 : y1 {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 参数 : dur {int} 滑动耗时毫秒数
- 版本 : 1.0.8


```javascript
// 用 1000 毫秒从 (500,0) 滑到 (500,800)
$szk.move(500, 0, 500, 800, 1000);
```


### move(x1, y1, x2, y2, dur, delay)

> 先等待 delay 毫秒，再从起点滑到终点，耗时 dur 毫秒。

- 参数 : x1 {int} 起点横坐标
- 参数 : y1 {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 参数 : dur {int} 滑动耗时毫秒数
- 参数 : delay {int} 滑动前等待毫秒数
- 版本 : 1.0.8


```javascript
// 先等 2000 毫秒，再用 1000 毫秒滑过去
$szk.move(500, 0, 500, 800, 1000, 2000);
```


### home()

> 返回桌面。

- 版本 : 1.0.8


```javascript
$szk.home();
```


### back()

> 模拟按下手机的"返回"键。

- 版本 : 1.0.8


```javascript
// 相当于点一下返回
$szk.back();
```


### menu()

> 模拟打开菜单键（最近任务/多任务界面）。

- 版本 : 1.0.8


```javascript
// 打开菜单
$szk.menu();
```


### recent()

> 打开最近任务（多任务）列表。
> 
> 效果和菜单键一样。

- 版本 : 1.0.8


```javascript
// 打开最近任务列表
$szk.recent();
```


### power()

> 模拟按下电源键（亮屏/灭屏/弹出关机菜单）。

- 版本 : 1.0.8


```javascript
// 按一下电源键
$szk.power();
```


### lock()

> 锁屏（如果屏幕本来就是关着的就不重复操作）。

- 版本 : 1.0.8


```javascript
// 锁屏
$szk.lock();
```


### unlock()

> 唤醒/解锁屏幕（如果屏幕本来就亮着就不重复操作）。

- 版本 : 1.0.8


```javascript
// 唤醒屏幕
$szk.unlock();
```


### input(text)

> 在当前聚焦的输入框里输入一段文字。
> 
> 相当于把文字打进当前光标所在的输入框。传空串会警告并不执行。

- 参数 : text {string} 要输入的文字
- 版本 : 1.0.8


```javascript
// 在输入框里输入文字
$szk.input("我是文本");
```


### killApp(pkgName)

> 强制停止（杀掉）指定包名的应用。
> 
> 相当于设置里"强行停止"。需要传入应用的包名，如 "com.tencent.mm"。

- 参数 : pkgName {string} 要停止的应用包名
- 版本 : 1.0.8


```javascript
// 杀掉微信（包名仅作示例）
$szk.killApp("com.tencent.mm");
```


### setWmSize(width, height)

> 修改屏幕分辨率（宽 x 高）。
> 
> 比如改成 1080x2200。改完界面会按新分辨率重新布局；用 resetWm 可恢复默认。

- 参数 : width {int} 新的屏幕宽度（像素）
- 参数 : height {int} 新的屏幕高度（像素）


```javascript
// 把分辨率设为 1080 宽、2200 高
$szk.setWmSize(1080, 2200);
```


### setDpi(density)

> 修改屏幕的密度（DPI），让界面整体显得更大或更小。
> 
> 数字越大图标文字越小。改完可能需要重新渲染界面；用 resetWm 可恢复默认。

- 参数 : density {int} 密度值，常见如 320、480
- 版本 : 1.5.4


```javascript
// 把密度设为 320
$szk.setDpi(320);
```


### resetWm()

> 把分辨率和密度都恢复成系统默认。
> 
> 配合 setWmSize、setDpi 使用：改乱了就调用它一键还原。

- 版本 : 1.5.4


```javascript
// 恢复默认分辨率和密度
$szk.resetWm();
```


### exe(cmd)

> 以 Shizuku 权限直接执行一条 shell 命令，并返回输出结果。
> 
> 这是 $szk 最底层的能力：很多方法（点击、滑动、按键）内部就是拼命令后调它。
> 你也可以自己拼命令执行，比如点电源键。

- 参数 : cmd {string} 要执行的 shell 命令
- 返回 : {string} 命令执行后的输出文字
- 版本 : 1.0.8


```javascript
// 先确保有权限
$szk.getPermit();
// 执行 shell 命令，返回命令输出
var out = $szk.exe("input keyevent KEYCODE_POWER");
log(out);
```


### exe(cmd, infoCallback, errorCallback)

> 异步执行 shell 命令，输出和错误分别通过回调返回。
> 
> 命令执行过程中的普通输出会走 infoCallback；出错会走 errorCallback。

- 参数 : cmd {string} 要执行的 shell 命令
- 参数 : infoCallback {function(info){}} 普通输出回调
- 参数 : errorCallback {function(err){}} 错误输出回调
- 版本 : 1.0.8


```javascript
// 先授权
$szk.getPermit();
// 执行 ls，过程输出和错误分别回调
$szk.exe("ls",
    function(info) {       // 普通输出回调
        log(info);
    },
    function(error) {      // 错误输出回调
        log(error);
    }
);
```


### exe(cmd, infoCallback, errorCallback, endCallback)

> 异步执行 shell 命令，并在命令结束时再回调一次。
> 
> 比上一版多一个 endCallback：命令整个执行完后会回调，结果里带结束状态。

- 参数 : cmd {string} shell 命令
- 参数 : infoCallback {function(info){}} 普通输出回调
- 参数 : errorCallback {function(err){}} 错误输出回调
- 参数 : endCallback {function(result){}} 执行结束回调
- 版本 : 1.0.8


```javascript
$szk.getPermit();
$szk.exe("ls",
    function(info) { log(info); },      // 普通输出
    function(error) { log(error); },    // 错误输出
    function(result) { log("结束：" + result); } // 执行结束
);
```


### exe(cmd, startCallback, infoCallback, errorCallback, endCallback)

> 异步执行 shell 命令，全过程回调：开始、输出、错误、结束。
> 
> 最完整的版本：命令开始时回调 startCallback，过程输出走 info，错误走 error，结束走 end。

- 参数 : cmd {string} shell 命令
- 参数 : startCallback {function(){}} 开始执行回调
- 参数 : infoCallback {function(info){}} 普通输出回调
- 参数 : errorCallback {function(err){}} 错误输出回调
- 参数 : endCallback {function(result){}} 结束回调
- 版本 : 1.0.8


```javascript
$szk.getPermit();
$szk.exe("ls",
    function() { log("开始执行"); },        // 开始回调
    function(info) { log(info); },          // 普通输出
    function(error) { log(error); },        // 错误输出
    function(result) { log("结束：" + result); } // 结束
);
```


