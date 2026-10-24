# $act - 手势动作

- 更新时间:2026-10-22 10:55:44

> 手势动作对象，脚本里叫 $act。
> 
> 它负责模拟人的手指操作：点击、长按、滑动、手势轨迹等，还能通过选择器在界面上定位控件节点并操作。
> 需要先开启无障碍服务（必要时配合 Root 或 Shizuku）才能对屏幕做手势。



```javascript
$act.click(320, 640);
```




### hasPermit()

> 检查无障碍服务是否已开启。
> 
> 只是查询当前状态，不会主动弹窗去申请；返回 true 才能做手势和节点操作。

- 返回 : {boolean} 操作成功或状态满足时返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
//判断是否有权限
var hasPermit = $act.hasPermit();
$tip.show("是否获得无障碍",hasPermit);
```


### getPermit()

> 请求无障碍权限，并等待权限可用。
> 
> 如果还没开启，会弹出系统无障碍设置页让你去打开。
> 
> 脚本会一直阻塞在这里等待，直到权限真正可用才往下走。
> 
> 每隔几秒会再次提示你去开启；超过一段时间还没开，会再次跳设置页。
> 
> 如果已授权 Root 或 Shizuku，会尝试用它们自动开启无障碍，省去手动点。
> 一般在脚本最开头调用一次，确保后续手势能正常执行。

- 返回 : {boolean} 操作成功或状态满足时返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
$act.getPermit();//获得权限
```


### click(x, y)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 版本 : 1.0.0


```javascript
//点击手势
$act.click(500,800);
```


### click(x, y, dur)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//设置点击时常(长按效果)
sleep(1000);
$act.click(135,344,1500);
```


### click(x, y, dur, delay)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.click(500,800,1500,100);
```


### click(index)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {int[]} 坐标数组 [x, y]，x 横坐标、y 纵坐标
- 版本 : 1.0.0


```javascript
//点击
$act.click([500,800]);
```


### click(index, dur)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {int[]} 坐标数组 [x, y]，x 横坐标、y 纵坐标
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//点击手势(长按)
$act.click([135,347],1500);
```


### click(index, dur, delay)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {int[]} 坐标数组 [x, y]，x 横坐标、y 纵坐标
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.click([136,347],1500,100);
```


### click(index)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {Point} 一个坐标点对象（含 x、y）
- 版本 : 1.0.0


```javascript
//用一个 Point 坐标对象来点击
var point = new org.opencv.core.Point(136,347);
$act.click(point);
```


### click(index, dur)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {Point} 坐标数组 [x, y]，x 横坐标、y 纵坐标
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
var point = new org.opencv.core.Point(136,347);
$act.click(point,1500);
```


### click(index, dur, delay)

> 执行点击。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : index {Point} 坐标数组 [x, y]，x 横坐标、y 纵坐标
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
var point = new org.opencv.core.Point(136,347);
$act.click(point,1500,100);
```


### click(node)

> 点击指定节点。
> 
> 如果节点本身可点击，优先直接对节点执行点击；不行就退回到点它的中心坐标。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来点击节点
var node = $act.selector().text("确定").findOne();
if(node!=null){
     // 绘制节点位置
     node.bounds();      //可在屏幕上画出节点范围，方便调试
     // 可以这样点击
     node.click();       //直接点这个节点
     // 也可以这样点击
     $act.click(node);
}
```


### click(node, useAct)

> 点击指定节点（可选择是否强制用坐标点击）。
> 
> 多了一个开关：useAct 为 true 时，不管节点能不能点，都直接点它的中心坐标。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : useAct {boolean} 是否强制改用坐标方式去点节点中心（true=坐标点击，false=优先用节点自身的点击能力）
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来点击节点
var node = $act.selector().text("确定").findOne();
if(node!=null){
     // 绘制节点位置
     node.bounds();
     // 可以这样点击
     node.click();
     // 也可以这样点击
     $act.click(node,true);//true表示直接使用$act的点击坐标方式进行点击
}
```


### press(node)

> 长按指定节点。
> 
> 节点支持长按就直接对它执行长按；不行就退回到长按它的中心坐标。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来长按节点
var node = $act.selector().text("列表项").findOne();
if(node!=null){
     // 绘制节点位置
     node.bounds();
     node.press();   //直接长按这个节点
     $act.press(node);
}
```


### press(node, useAct)

> 长按指定节点（可选择是否强制用坐标长按）。
> 
> useAct 为 true 时，直接用坐标长按节点中心；否则优先用节点自身的长按能力。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : useAct {boolean} 是否强制改用坐标方式去点节点中心（true=坐标点击，false=优先用节点自身的点击能力）
- 版本 : 1.0.0


```javascript
var node = $act.selector().text("列表项").findOne();
$act.press(node, true);
```


### press(x, y)

> 执行长按。
> 

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.press(136,347);
```


### press(x, y, dur)

> 执行长按。
> 

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.press(136,347,1500);
```


### press(x, y, dur, delay)

> 执行长按。
> 

- 参数 : x {int} 屏幕横坐标（像素，从屏幕左边缘往右算）
- 参数 : y {int} 屏幕纵坐标（像素，从屏幕上边缘往下算）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.press(136,347,1500,100);
```


### slide(startX, startY, endX, endY, duration)

> 沿指定路径模拟自然的人手滑动。

- 参数 : startX {int} 起点横坐标（像素）
- 参数 : startY {int} 起点纵坐标（像素）
- 参数 : endX {int} 终点横坐标（像素）
- 参数 : endY {int} 终点纵坐标（像素）
- 参数 : duration {int} 整段手势的持续时长（毫秒）
- 版本 : 1.7.8


```javascript
//随机模拟真人滑动(推荐)
$act.slide(189,244,733,1440,3000);
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
$act.move(500,0,500,800);
```


### move(x1, y1, x2, y2, dur)

> 执行滑动。
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(500,0,500,800,500);
```


### move(x1, y1, x2, y2, dur, delay)

> 执行滑动。
> 

- 参数 : x1 {int} 起点横坐标（像素）
- 参数 : y1 {int} 起点纵坐标（像素）
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(500,0,500,800,500.1000);
```


### move(node, dir)

> 让一个可滚动的节点（如列表）按指定方向滚动一页。
> 
> 此操作只能通过无障碍服务执行。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : dir {String} 滑动方向，如 左/右/上/下
- 版本 : 1.0.0


```javascript
$act.move(null, "up");
```


### move(node, x2, y2, dur)

> 执行滑动。
> 

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(node,800,500,1000);
```


### move(node, x2, y2, dur, delay)

> 执行滑动。
> 

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : x2 {int} 终点横坐标（像素）
- 参数 : y2 {int} 终点纵坐标（像素）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(node,800,500,1000,100);
```


### gesture(gesture)

> 执行多指手势。

- 参数 : gesture {int[]} 一段手势的坐标点数组 [x,y,x,y,...]
- 版本 : 1.0.0


```javascript
// 手势模拟向下滑动
$act.gesture([500,0,500,800,0,500]);
```


### gesture(gesture1, gesture2)

> 执行双指手势。
> 

- 参数 : gesture1 {int[]} 第一段手势的坐标点数组
- 参数 : gesture2 {int[]} 第二段手势的坐标点数组
- 版本 : 1.0.0


```javascript
// 双指放大
var centerX = 500;
var centerY = 800;
$act.gesture(
    [centerX-100, centerY, centerX-300, centerY, 0, 300],
    [centerX+100, centerY, centerX+300, centerY, 0, 300]
);
```


### gesture(gesture1, gesture2, gesture3)

> 执行三指手势。
> 

- 参数 : gesture1 {int[]} 第一段手势的坐标点数组
- 参数 : gesture2 {int[]} 第二段手势的坐标点数组
- 参数 : gesture3 {int[]} 第三段手势的坐标点数组
- 版本 : 1.0.0


```javascript
//三指滑动动作
$act.gesture( [500,0,500,800,500,0] ,
[550,0,550,800,500,0] ,
[600,0,600,800,500,0]
);
```


### gesture(gesture1, gesture2, gesture3, gesture4)

> 执行四指手势。
> 

- 参数 : gesture1 {int[]} 第一段手势的坐标点数组
- 参数 : gesture2 {int[]} 第二段手势的坐标点数组
- 参数 : gesture3 {int[]} 第三段手势的坐标点数组
- 参数 : gesture4 {int[]} 第四段手势的坐标点数组
- 版本 : 1.0.0


```javascript
//四指滑动动作
$act.gesture( [500,0,500,800,500,0] ,
[550,0,550,800,500,0] ,
[600,0,600,800,500,0] ,
[650,0,650,800,500,0]
);
```


### createPath(paths)

> 创建一个默认时长为一秒的手势路径对象。

- 参数 : paths {[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 返回 : {Path} 构造好的安卓 Path 路径对象，可用于执行手势
- 版本 : 1.0.0


```javascript
var result = $act.createPath(["one", "two"]);
```


### createPath(paths, dur)

> 根据传入的手势路径创建路径对象。

- 参数 : paths {[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 返回 : {AgPath} 包装好的路径对象，可直接交给多段手势执行
- 版本 : 1.0.0


```javascript
var result = $act.createPath(["one", "two"], 500);
```


### createPath(paths, delay, dur)

> 根据传入的手势路径创建路径对象。

- 参数 : paths {[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 参数 : delay {int} 正式开始前延迟等待的时间（毫秒）
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 返回 : {Path} 构造好的安卓 Path 路径对象，可用于执行手势
- 版本 : 1.0.0


```javascript
var result = $act.createPath(["one", "two"], 1, 500);
```


### path(paths)

> 执行一个或多个手势路径。

- 参数 : paths {AgPath...} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 版本 : 1.0.0


```javascript
$act.path(null);
```


### path(paths)

> 创建并执行一个默认时长为一秒的手势路径。

- 参数 : paths {int[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 版本 : 1.0.0


```javascript
$act.path(["one", "two"]);
```


### path(paths, dur)

> 创建并执行手势路径。

- 参数 : paths {int[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
$act.path(["one", "two"], 500);
```


### path(paths, startTime, dur)

> 创建并执行手势路径。

- 参数 : paths {int[][]} 一组路径点（每个点是 [x,y] 或坐标对象），按顺序连成手势轨迹
- 参数 : startTime {int} 手势开始的时间偏移（毫秒），用于多段手势错峰启动
- 参数 : dur {int} 手势持续时长（毫秒），按下去停留多久
- 版本 : 1.0.0


```javascript
$act.path(["one", "two"], 500, 500);
```


### home()

> 执行返回桌面的操作。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
// 返回主页前先确认无障碍权限
if ($act.hasPermit()) $act.home();
}</pre>


```javascript
$act.home();
```


### back()

> 执行返回操作。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.back();
sleep(300);
log("已返回上一页");
}</pre>


```javascript
$act.back();
```


### menu()

> 打开系统菜单。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.menu();
log("已打开系统菜单");
}</pre>


```javascript
$act.menu();
```


### recent()

> 打开最近任务界面。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.recent();
log("已打开最近任务");
}</pre>


```javascript
$act.recent();
```


### power()

> 长按电源键。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.power();
log("已发送电源键事件");
}</pre>


```javascript
$act.power();
```


### lock()

> 锁定屏幕。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
if ($act.getPermit()) $act.lock();
}</pre>


```javascript
$act.lock();
```


### unlock()

> 唤醒屏幕。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.unlock();
log("已尝试唤醒屏幕");
}</pre>


```javascript
$act.unlock();
```


### splitScreen()

> 进入分屏模式。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.splitScreen();
log("已发送分屏按键事件");
}</pre>


```javascript
$act.splitScreen();
```


### settings()

> 打开系统设置。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.settings();
$thread.sleep(500);
log("已打开系统设置");
}</pre>


```javascript
$act.settings();
```


### notifications()

> 打开通知栏。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.notifications();
log("已打开通知栏");
}</pre>


```javascript
$act.notifications();
```


### screenshot()

> 打开系统截屏界面。
> 
> 打开设备截屏界面。

- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.screenshot();
log("已发送截屏按键事件");
}</pre>


```javascript
$act.screenshot();
```


### input(text)

> 将文本粘贴到输入框。
> 
> 优先使用 Root 或 Shizuku（若已授权）执行该手势；
> 否则，在无障碍服务可用时通过无障碍服务执行。
> 以上方式都不可用时，此操作不会生效。

- 参数 : text {String} 要输入或写入的文本内容
- 版本 : 1.0.0


```javascript
$act.input("我是要粘贴的内容");
```


### input(node, text)

> 直接把文本写入指定的原生输入框节点（相当于设置文本，不用手动弹键盘打字）。
> 
> 此函数需要无障碍服务。

- 参数 : node {AccessibilityNodeInfo} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : text {String} 要输入或写入的文本内容
- 版本 : 1.0.0


```javascript
//先通过选择器拿到输入框节点，再把文本写进去
var box = $act.selector().className("EditText").findOne();
$act.input(box, "我是要粘贴的内容");
```


### input(node, text)

> 直接把文本写入指定的输入框节点（Node 包装版）。
> 
> 用法同上，只是传入的是用选择器找到的 Node 对象。

- 参数 : node {Node} 要操作的无障碍节点对象，由 $act.selector() 查找获得
- 参数 : text {String} 要输入或写入的文本内容
- 版本 : 1.0.0


```javascript
var box = $act.selector().className("EditText").findOne();
$act.input(box, "我是要粘贴的内容");
```


### activity()

> 获取当前活动类名。

- 返回 : 操作结果，一般为成功与否或对应的数据对象
- 版本 : 1.0.0


```javascript
var name = $act.activity();
log("当前类名:"+name);
```


### activity(callback)

> 注册活动变化回调。

- 参数 : callback {(name)=>{} 页面变化时的回调，参数是当前页面名
- 版本 : 1.0.0


```javascript
//设置监听:
$act.activity(function(name) {
    log("当前界面==>" + name);
});
```


### selector()

> 创建界面选择器。
> 

- 返回 : {UiSelector} 选择器对象，用它在界面上按条件查找控件节点
- 版本 : 1.0.0


```javascript
var result = $act.selector();
```


### setDevDensity(density)

> 设置开发屏幕密度。
> 
> 填你"写脚本时那台手机"的密度，坐标适配时按它做换算。
> 
> 配合 setAdapt(true) 一起用，才能在不同分辨率手机上点对位置。

- 参数 : density {float} 屏幕密度（dpi/160），用于适配坐标
- 版本 : 1.0.0


```javascript
$act.setDevDensity(1);
```


### setAdapt(usable)

> 启用或停用屏幕坐标适配。
> 
> 开启后，你写的坐标会按"开发机→当前机"的密度比例自动换算。
> 
> 这样同一份脚本在不同分辨率的手机上都能点到大概正确的位置。

- 参数 : usable {boolean} 是否启用该能力
- 版本 : 1.0.0
<p>使用示例：
<pre>{@code
$act.setAdapt(true);
$act.click(100, 200);
// 开启后坐标会按设备密度适配
}</pre>


```javascript
$act.setAdapt(true);
```


### isOnlyAcc()

> 查询当前是否被强制为"只使用无障碍手势"。

- 返回 : {boolean} 操作成功或状态满足时返回 true，否则返回 false


```javascript
var result = $act.isOnlyAcc();
```


### setOnlyAcc(onlyAcc)

> 设置是否强制只用无障碍手势，不走 Root/Shizuku。
> 
> $act 会自动挑一个可用的手势执行方式：优先 Root，其次 Shizuku，最后才是无障碍手势。
> 
> 设为 true 后，就只用无障碍自带的手势执行。
> 
> 适合没有 Root/Shizuku、或想统一行为时使用。

- 参数 : onlyAcc {boolean} 是否强制只使用无障碍手势（不走 Root/Shizuku）
- 版本 : 1.4.3


```javascript
$act.setOnlyAcc(true);
```


### setJitter(jitter)

> 设置坐标抖动范围。
> 
> 开启后，每次点击/滑动的坐标都会在原位置附近随机偏移几像素。
> 
> 这样不会每次都点在完全相同的坐标上，模拟真人操作更自然。
> 
> 传 0 表示关闭抖动。

- 参数 : jitter {int} 随机抖动范围（像素），点击时加随机偏移，避免每次点在完全相同位置
- 版本 : 1.4.3
<p>使用示例：
<pre>{@code
$act.setJitter(3);
$act.click(500, 800);
// 点击时加入轻微随机抖动
}</pre>


```javascript
$act.setJitter(1);
```


### enableRoot(enableRoot)

> 设置是否允许在有 Root 时优先用 Root 执行手势。
> 
> 开启后，若设备已 Root，$act 会优先用 Root 来做点击/滑动等手势。
> 
> Root 默认是开启的；不需要时可以用这个方法关掉。

- 参数 : enableRoot {boolean} 是否允许优先使用 Root 执行手势
- 版本 : 1.4.7


```javascript
$act.enableRoot(true);
```


### isEnableRoot()

> 查询当前是否允许优先使用 Root 执行手势。

- 返回 : {boolean} 操作成功或状态满足时返回 true，否则返回 false
- 版本 : 1.4.7


```javascript
var result = $act.isEnableRoot();
```


### enableSzk(enableSzk)

> 设置是否允许在有 Shizuku 时优先用 Shizuku 执行手势。
> 
> 开启后，若已连接 Shizuku，$act 会优先用它来做手势。
> 
> Shizuku 默认是开启的；不需要时可以用这个方法关掉。

- 参数 : enableSzk {boolean} 是否允许优先使用 Shizuku 执行手势
                 <p>使用示例：
                 <pre>{@code
                                  $act.enableSzk(true);
                                  log("优先尝试使用 Shizuku 执行动作");
                                  }</pre>


```javascript
$act.enableSzk(true);
```


### isEnableSzk()

> 查询当前是否允许优先使用 Shizuku 执行手势。

- 返回 : {boolean} 操作成功或状态满足时返回 true，否则返回 false
- 版本 : 1.4.7


```javascript
var result = $act.isEnableSzk();
```


