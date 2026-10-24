# $task - 脚本任务

- 更新时间:2026-10-22 10:56:52

> 脚本任务
> 
> 每个正在执行的代码文件中都会内置一个专属对象：任务对象($task)
> 
> 你可以通过任务对象($task)来控制当前任务的执行
> 
> 你也可以通过任务对象($task)来获取当前任务的信息




### const {String} ID;

> 任务唯一序列
> 
> 该序列会和当前线程名称保持一致


```javascript
log("当前任务唯一序列:",$task.ID);
```


### const {long} startTime;

> 当前任务的开始执行时间

- 版本 : 1.3.9


```javascript
log("当前任务的开始执行时间:",$task.startTime);
```


### const {String} name;

> 当前任务名称
> 
> 有时也指路径或文件名称

- 版本 : 1.3.9


```javascript
log("当前任务名称:",$task.name);
```


### const {String} threadName;

> 当前任务线程名称
> 
> 线程名称通常与ID相同

- 版本 : 1.3.9


```javascript
log("当前任务线程名称:",$task.threadName);
```


### const {String} path;

> 当前脚本路径
> 
> 此属性并不重要，取决于执行脚本时传入的路径参数值，如果是临时文件，则路径是随机生成的。

- 版本 : 1.3.9


```javascript
log("当前脚本路径:",$task.path);
```


### stop()

> 停止任务
> 
> 每个任务($task)都是一条新的线程，如果你的代码中存在死循环，则循环不会停止(因为循环会被当作一条命令执行，表示执行完毕这个命令了)，请处理好脚本逻辑。

- 版本 : 1.0.0


```javascript
$task.stop();
```


### getInfo()

> 获取脚本任务信息

- 返回 : {JsTaskInfo} 任务信息
- 版本 : 1.0.0


```javascript
let info = $task.getInfo();
alert("任务信息",info.toString());
```


### isRunning()

> 是否正在运行

- 返回 : {boolean} 返回是否正在运行
- 版本 : 1.0.0


```javascript
let is = $task.isRunning();
if(is){
    alert("任务正在运行");
}else{
    alert("任务已经停止运行");
}
```


### getID()

> 获取当前任务的ID

- 返回 : {string} 返回当前任务的ID
- 版本 : 1.0.0


```javascript
let id = $task.getID();
alert("任务ID",id);
```


### getStartTime()

> 获取当前任务的开始时间

- 返回 : {long} 返回当前任务的开始时间
- 版本 : 1.0.0


```javascript
let time = $task.getStartTime();
alert("任务开始时间",time);
```


### getName()

> 获取当前任务的名称

- 返回 : {string} 返回当前任务的名称
- 版本 : 1.0.0


```javascript
let name = $task.getName();
alert("任务名称",name);
```


### getThreadName()

> 获取当前任务的线程名称

- 返回 : {string} 返回当前任务的线程名称
- 版本 : 1.0.0


```javascript
let tn = $task.getThreadName();
alert("线程名称",tn);
```


### getPath()

> 获取当前任务的脚本路径

- 返回 : {string} 返回当前任务的脚本路径
- 版本 : 1.0.0


```javascript
let path = $task.getPath();
alert("脚本路径",path);
```


### getPath(relativePath)

> 获取相对当前脚本路径的绝对路径

- 参数 : relativePath {string} 相对路径
- 返回 : {string} 返回绝对路径
- 版本 : 1.0.0


```javascript
let path = $task.getPath("../res");
alert("相对路径",path);
```


### pause()

> 暂停当前任务

- 版本 : 1.3.9


```javascript
//我演示一个错误的用法：
$task.pause();//当暂停以后，下面的代码不会被执行
//...其他代码
$task.start();//这行代码不被执行到，因此这样调用毫无意义
```


### start()

> 继续运行暂停的任务

- 版本 : 1.3.9


```javascript
$task.start();
```


### isPause()

> 任务是否暂停

- 返回 : {boolean} 是否暂停
- 版本 : 1.3.9


```javascript
log("是否暂停",$task.isPause());
```


### isStop()

> 判断任务是否停止
> 
> 只有当调用了'$task.stop()'或者'$engine.stop(ID)'或'$engine.stopAll()'才会返回'true'

- 返回 : {boolean} 是否停止
- 版本 : 1.7.0


```javascript
//因此，在多线程中正确书写死循环的方式：
$thread.run(()=>{
    while(!$task.isStop()){
        log("正在运行...");
        sleep(1000);
    }
    log("脚本停止");
});
```


