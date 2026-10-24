# $touch - 触摸驱动

- 更新时间:2026-10-22 10:55:52

> $touch：基于无障碍服务的触摸驱动，用来模拟手指点击、长按、滑动和按键。
> 
> 它通过 C/C++ 层注入触摸事件，速度较快。使用前要先确认无障碍权限已开启、再 init 初始化，
> 之后才能做点击滑动。适合做不需要 Root 的手势模拟。



```javascript
// 标准用法：先检查权限、初始化，再点击
if ($touch.hasPermit()) {
    $touch.init();
    $touch.click(320, 640);
}
```




### hasPermit()

> 检查触摸事件注入（无障碍）权限是否已经开好。
> 
> 用 $touch 做任何点击滑动前，都要先确认有权限、再 init 初始化，否则操作没效果。

- 返回 : {boolean} true 表示权限已就绪，false 表示没开好
- 版本 : 1.5.2


```javascript
// 先检查权限
if ($touch.hasPermit()) {
    // 有权限就初始化
    $touch.init();
}
// 初始化之后再做点击滑动，否则没效果
```


### init()

> 初始化触摸事件注入，准备开始模拟点击滑动。
> 
> 必须先 hasPermit 通过，再调用本方法。一般在脚本开头做一次。

- 返回 : {boolean} true 表示初始化成功


```javascript
// 开始初始化
var ok = $touch.init();
log("初始化结果：" + ok);
```


### touchDown(fingerId, x, y)

> 让指定的一根手指在 (x, y) 位置按下屏幕。
> 
> fingerId 用来区分多根手指：0 是第一根手指，1 是第二根。
> 通常和 touchMove、touchUp 配合，自己手搓一个手势。

- 参数 : fingerId {int} 手指编号（0、1、2…）
- 参数 : x {int} 按下的横坐标
- 参数 : y {int} 按下的纵坐标
- 版本 : 1.5.2


```javascript
// 0 号手指在 (100,100) 按下
$touch.touchDown(0, 100, 100);
```


### touchMove(fingerId, x, y)

> 让已经按下的那根手指，移动到新的 (x, y) 位置。

- 参数 : fingerId {int} 手指编号
- 参数 : x {int} 新横坐标
- 参数 : y {int} 新纵坐标
- 版本 : 1.5.2


```javascript
// 0 号手指移到 (300,500)
$touch.touchMove(0, 300, 500);
```


### touchUp(fingerId)

> 把指定的那根手指从屏幕上抬起来（结束本次触摸）。

- 参数 : fingerId {int} 要抬起的手指编号
- 版本 : 1.5.2


```javascript
// 抬起 0 号手指
$touch.touchUp(0);
```


### click(x, y)

> 在 (x, y) 位置点一下。
> 
> 通过 C/C++ 层系统命令注入触摸事件，速度比普通方式更快。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 版本 : 1.5.4


```javascript
// 在 (300,500) 点一下
$touch.click(300, 500);
```


### click(pointerId, x, y)

> 指定一根手指，在 (x, y) 位置点一下。
> 
> 第一根手指用 0。

- 参数 : pointerId {int} 手指编号
- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 版本 : 1.5.2


```javascript
// 1 号手指在 (300,500) 点一下
$touch.click(1, 300, 500);
```


### click(pointerId, x, y, dur)

> 指定手指在 (x, y) 按住 dur 毫秒后松开（长按）。

- 参数 : pointerId {int} 手指编号
- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住毫秒数
- 版本 : 1.5.2


```javascript
// 1 号手指在 (300,500) 按住 50 毫秒
$touch.click(1, 300, 500, 50);
```


### press(x, y)

> 在 (x, y) 位置长按（用默认手指 0）。

- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 版本 : 1.5.2


```javascript
// 在 (300,500) 长按
$touch.press(300, 500);
```


### press(pointerId, x, y)

> 指定一根手指在 (x, y) 长按（默认按住 750 毫秒）。

- 参数 : pointerId {int} 手指编号
- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 版本 : 1.5.2


```javascript
// 1 号手指长按
$touch.press(1, 300, 500);
```


### press(pointerId, x, y, dur)

> 指定手指在 (x, y) 长按 dur 毫秒，自己定时长。

- 参数 : pointerId {int} 手指编号
- 参数 : x {int} 横坐标
- 参数 : y {int} 纵坐标
- 参数 : dur {int} 按住毫秒数
- 版本 : 1.5.2


```javascript
// 1 号手指长按 2000 毫秒
$touch.press(1, 300, 500, 2000);
```


### move(x, y, x2, y2)

> 从 (x,y) 滑到 (x2,y2)，默认滑 1 秒。
> 
> 就是模拟一次手指拖动，用来翻页、滑动列表。

- 参数 : x {int} 起点横坐标
- 参数 : y {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 版本 : 1.5.2


```javascript
// 从 (100,100) 滑到 (300,500)
$touch.move(100, 100, 300, 500);
```


### move(x, y, x2, y2, dur)

> 从 (x,y) 滑到 (x2,y2)，自己指定滑动耗时。

- 参数 : x {int} 起点横坐标
- 参数 : y {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 参数 : dur {int} 滑动耗时毫秒数
- 版本 : 1.5.2


```javascript
// 用 1000 毫秒滑过去
$touch.move(100, 100, 300, 500, 1000);
```


### move(pointerId, x, y, x2, y2, dur)

> 指定一根手指，从 (x,y) 滑到 (x2,y2)，耗时 dur 毫秒。

- 参数 : pointerId {int} 手指编号
- 参数 : x {int} 起点横坐标
- 参数 : y {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 参数 : dur {int} 滑动耗时毫秒数
- 版本 : 1.5.2


```javascript
// 1 号手指滑动 1000 毫秒
$touch.move(1, 100, 100, 300, 500, 1000);
```


### swipe(x, y, x2, y2, dur)

> 模拟一次快速滑动（C/C++ 层注入滑动事件）。
> 
> 和 move 类似，从起点滑到终点。

- 参数 : x {int} 起点横坐标
- 参数 : y {int} 起点纵坐标
- 参数 : x2 {int} 终点横坐标
- 参数 : y2 {int} 终点纵坐标
- 参数 : dur {int} 滑动耗时毫秒数
- 版本 : 1.5.4


```javascript
// 从 (100,200) 用 2000 毫秒滑到 (600,1200)
$touch.swipe(100, 200, 600, 1200, 2000);
```


### key(keyCode)

> 模拟按下一个安卓按键，传按键码（KeyCode）。
> 
> 比如 4 是返回键。常用键值：3=主页，4=返回。

- 参数 : keyCode {int} 安卓按键码
- 版本 : 1.5.4


```javascript
// 4 = 返回键
$touch.key(4);
```


