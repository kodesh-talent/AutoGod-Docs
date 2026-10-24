# $timer - 定时任务

- 更新时间:2026-10-22 10:55:52

> 定时任务对象，脚本里叫 $timer。
> 
> 它可以让脚本"到点自动运行"：设置好时间后，即使现在把脚本停掉，到了设定的时间，
> 系统也会自动去运行你指定的那个脚本文件。适合做每天定时打卡、定时签到、隔几秒重复执行等任务。
> 任务记录会被持久化保存，重启手机后仍然有效。



```javascript
$timer.add("sample", "/sdcard/Scripts/timer.js", 5, false);
```




### add(name, script, hours, minutes, seconds, repeat)

> 添加定时任务
> 
> 适合用于设定每天何时执行定时任务，可以设置每天都执行，也可以只是明天或者今天执行一次。
> 这里的 hours、minutes、seconds 是"一天中的几点几分几秒"（24 小时制），
> 例如 10 点 0 分 0 秒就是每天上午 10 点运行。

- 参数 : name {String} 这个定时任务的名字，用来唯一标识它，之后删除、查询都靠它
- 参数 : script {String} 到点时要运行的脚本文件路径（例如 "/sdcard/Scripts/run.js"）
- 参数 : hours {Integer} 每天几点运行（0~23，24 小时制）
- 参数 : minutes {Integer} 几点几分里的"分"（0~59）
- 参数 : seconds {Integer} 几分几秒里的"秒"（0~59）
- 参数 : repeat {Boolean} 是否每天重复执行；true 每天都跑，false 只跑一次


```javascript
//添加一个每天上午 10 点整运行的任务，任务名叫"我的任务"，运行 run.js
$timer.add("我的任务", "run.js", 10, 0, 0, true);
```


### add(name, script, seconds, repeat)

> 添加定时任务
> 
> 适合用于间隔几秒后执行的任务，可以设置重复执行，也可以一次性执行。
> 这里的 seconds 是"距离现在多少秒后运行"，而不是一天中的某个时刻。

- 参数 : name {String} 这个定时任务的名字，用来唯一标识它，之后删除、查询都靠它
- 参数 : script {String} 到点时要运行的脚本文件路径（例如 "/sdcard/Scripts/run.js"）
- 参数 : seconds {Integer} 间隔多少秒后运行（repeat 为 true 时就是每隔这么多秒跑一次）
- 参数 : repeat {Boolean} 是否重复执行；true 每隔 seconds 秒重复跑，false 只在 seconds 秒后跑一次


```javascript
//添加一个任务：5 秒后运行 run.js，并且每隔 5 秒重复运行
$timer.add("我的任务", "run.js", 5, true);
```


### ls()

> 获取所有定时任务信息

- 返回 : {TimerTaskInfo[]} 所有已添加定时任务的信息列表（每个元素含任务名、脚本路径、时间、是否重复等）；一个都没有时返回空列表


```javascript
var myTasks = $timer.ls();
log(myTasks);
```


### has(name)

> 判断是否存在时钟
> 
> 每次添加时钟任务的时候会向本地持久化一个时钟任务文件，这个方法只是判断文件中是否写入了这个任务，而无法判断系统中是否存在这个时钟任务。

- 参数 : name {String} 要检查的任务名字（添加任务时起的那个名字）
- 返回 : {boolean} 本地记录里存在这个任务就返回 true，否则返回 false


```javascript
var myTasks = $timer.ls();
log(myTasks);
```


### del(name)

> 移除定时任务
> 
> 移除本地时钟任务记录以及移除系统中的时钟任务

- 参数 : name {String} 要移除的任务名字（添加任务时起的那个名字）


```javascript
$timer.del("我的任务");
```


### delAll()

> 移除所有定时任务
> 
> 移除本地时钟任务记录以及移除系统中的时钟任务


```javascript
$timer.delAll();
```


