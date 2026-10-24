# $engine - 脚本引擎

- 更新时间:2026-10-22 10:55:46

> $engine：脚本引擎，用来运行和管理 JS 脚本任务。
> 
> 可以运行脚本文件、直接跑一段代码，并拿到任务 ID 去暂停、继续、停止、查询任务。
> 每个 run/runCode 都会新开一个任务，任务结束后自动销毁。



```javascript
// 直接跑一行代码
$engine.runCode("log('hello from Rhino')");
```




这是一个文档示例占位字段，本身不用在脚本里调用。

仅用于在文档里演示用法格式。
:::


### run(path)

> 运行指定路径的脚本文件，返回这个任务的 ID。
> 
> 后面可以拿这个 ID 去暂停、继续、停止这个脚本。脚本会在新任务里跑。

- 参数 : path {string} 脚本文件的绝对路径
- 返回 : {string} 新任务的 ID，后续操作用它
- 版本 : 1.0.0


```javascript
// 运行 sdcard 下的脚本，拿到任务 ID
var id = $engine.run("/sdcard/脚本.js");
```


### run(jsFile)

> 用一个 File 对象来指定脚本并运行，返回任务 ID。
> 
> File 对象通常由 $file.open(...) 得到。

- 参数 : jsFile {File} 用 $file.open 得到的文件对象
- 返回 : {string} 新任务的 ID
- 版本 : 1.0.0


```javascript
// 先用 $file 打开成 File，再交给引擎运行
var f = $file.open("/sdcard/脚本.js");
var id = $engine.run(f);
```


### runCode(code)

> 直接运行一段写死的 JS 代码字符串，返回任务 ID。
> 
> 不用先存成文件，把代码当字符串传进去就会跑。

- 参数 : code {string} 要运行的 JS 代码字符串
- 返回 : {string} 新任务的 ID
- 版本 : 1.0.0


```javascript
// 直接跑一段代码
var id = $engine.runCode('toast("我被运行了");');
```


### runCode(path, code)

> 运行一段代码字符串，并给它指定一个"脚本路径"标识。
> 
> 第一个参数是给这段代码起的路径名（影响报错时显示的文件名），第二个是代码本身。

- 参数 : path {string} 给这段代码起的路径标识
- 参数 : code {string} 要运行的 JS 代码字符串
- 返回 : {string} 新任务的 ID
- 版本 : 1.0.0


```javascript
// 给代码一个路径名再运行
var id = $engine.runCode("/sdcard/main.js", 'toast("我被运行了");');
```


### pause(id)

> 暂停指定 ID 的任务。
> 
> 暂停后脚本停在原地，用 start 可以继续。

- 参数 : id {string} 任务 ID
- 版本 : 1.3.9


```javascript
var id = $engine.run("/sdcard/脚本.js");
// 暂停运行
$engine.pause(id);
sleep(2000);
// 继续运行
$engine.start(id);
```


### isPause(id)

> 查询指定任务当前是不是处于暂停状态。
> 
> 如果任务找不到，会返回 true（并打条警告）。

- 参数 : id {string} 任务 ID
- 返回 : {boolean} true 表示已暂停（或任务不存在）
- 版本 : 1.3.9


```javascript
var isPause = $engine.isPause(id);
if (isPause) {
    log("任务已暂停");
} else {
    log("任务正在跑");
}
```


### start(id)

> 恢复（继续）一个被暂停的任务。

- 参数 : id {string} 任务 ID
- 版本 : 1.3.9


```javascript
var id = $engine.run("/sdcard/脚本.js");
$engine.pause(id);
sleep(2000);
// 继续运行
$engine.start(id);
```


### ls()

> 列出所有任务的信息，返回一个 JsTaskInfo 列表。

- 返回 : {JsTaskInfo[]} 任务信息列表
- 版本 : 1.0.0


```javascript
// 列出所有任务
var taskList = $engine.ls();
for (var i = 0; i < taskList.length; i++) {
    log(taskList[i]);
}
```


### stop(id)

> 停止（结束）指定 ID 的任务。

- 参数 : id {string} 任务 ID
- 版本 : 1.0.0


```javascript
var id = $engine.run("/sdcard/脚本.js");
// 停止它
$engine.stop(id);
```


### stopAll(exit)

> 停止所有脚本任务。
> 
> 参数为 true 时连 App 一起退出；为 false 只停脚本、保留 App。

- 参数 : exit {boolean} true 连 App 一起退出，false 只停脚本
- 版本 : 1.0.0


```javascript
// 停掉所有脚本，但不退出 App
$engine.stopAll(false);
log("已停止所有脚本，但应用仍在运行");
```


### stopAll()

> 停止所有脚本任务，但不退出 App。

- 版本 : 1.0.0


```javascript
// 停掉所有脚本
$engine.stopAll();
log("已停止所有脚本");
```


### lsTask()

> 列出所有正在执行的任务对象（JsExecuteTask）。
> 
> 跟 ls 类似，但返回的是可操作的任务对象本身。

- 返回 : {JsExecuteTask[]} 正在执行的任务对象列表
- 版本 : 1.0.0


```javascript
var taskList = $engine.lsTask();
for (var i = 0; i < taskList.length; i++) {
    log(taskList[i]);
}
```


### has(id)

> 判断指定 ID 的任务现在是否还存在。
> 
> 任务跑完会自动销毁，所以停之前可以先 has 一下确认它还在。

- 参数 : id {string} 任务 ID
- 返回 : {boolean} true 表示任务还存在
- 版本 : 1.5.0


```javascript
var id = $engine.run("/sdcard/脚本.js");
// 先判断任务是否还在
var hasTask = $engine.has(id);
if (hasTask) {
    $engine.stop(id);
}
```


