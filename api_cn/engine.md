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


### 运行(脚本路径)

> 运行路径中的脚本：启动并返回任务 ID。
> 
> 这是 $engine.run 的中文叫法。

- 参数 : 脚本路径 {字符串} 脚本绝对路径
- 返回 : {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
var id = $engine.运行("/sdcard/脚本.js");
```


### 运行(js文件)

> 运行 File 对象指向的脚本。
> 
> 这是 $engine.run(File) 的中文叫法。

- 参数 : js文件 {File} 文件对象
- 返回 : {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
var f = $file.open("/sdcard/脚本.js");
var id = $engine.运行(f);
```


### 运行代码(代码)

> 运行代码：直接执行一段 JS 字符串。
> 
> 这是 $engine.runCode 的中文叫法。

- 参数 : 代码 {字符串} JS 代码字符串
- 返回 : {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
var id = $engine.运行代码('toast("我被运行了");');
```


### 运行代码(脚本路径, 代码)

> 运行代码（带路径名）：给一段代码指定路径标识。
> 
> 这是带路径版 $engine.runCode 的中文叫法。

- 参数 : 脚本路径 {字符串} 路径标识
- 参数 : 代码 {字符串} JS 代码
- 返回 : {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
var id = $engine.运行代码("/sdcard/main.js", 'toast("我被运行了");');
```


### 暂停(任务ID)

> 暂停运行：让指定任务停住。
> 
> 这是 $engine.pause 的中文叫法。

- 参数 : 任务ID {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
$engine.暂停(任务ID);
sleep(2000);
$engine.开始(任务ID);
```


### 暂停了(任务ID)

> 判断任务是否处于暂停状态。
> 
> 这是 $engine.isPause 的中文叫法。

- 参数 : 任务ID {字符串} 任务 ID
- 返回 : {布尔值} true 表示已暂停
- 版本 : 1.6.8


```javascript
var 暂停了 = $engine.暂停了(任务ID);
if (暂停了) {
    log("任务已暂停");
}
```


### 开始(任务ID)

> 开始运行：继续被暂停的任务。
> 
> 这是 $engine.start 的中文叫法。

- 参数 : 任务ID {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
$engine.暂停(任务ID);
sleep(2000);
$engine.开始(任务ID);
```


### 罗列()

> 罗列：列出所有任务信息。
> 
> 这是 $engine.ls 的中文叫法。

- 返回 : {JsTaskInfo[]} 任务信息列表
- 版本 : 1.6.8


```javascript
var 任务列表 = $engine.罗列();
for (var i = 0; i < 任务列表.length; i++) {
    log(任务列表[i]);
}
```


### 停止(任务ID)

> 停止指定任务。
> 
> 这是 $engine.stop 的中文叫法。

- 参数 : 任务ID {字符串} 任务 ID
- 版本 : 1.6.8


```javascript
$engine.停止(任务ID);
```


### 停止所有(是否退出系统)

> 停止所有任务（可选是否退出 App）。
> 
> 这是带退出参数版 $engine.stopAll 的中文叫法。

- 参数 : 是否退出系统 {布尔值} true 连 App 退出
- 版本 : 1.6.8


```javascript
$engine.停止所有(false);
```


### 停止所有()

> 停止所有任务（不退出 App）。
> 
> 这是 $engine.stopAll() 的中文叫法。

- 版本 : 1.7.0


```javascript
$engine.停止所有();
```


### 罗列任务()

> 罗列任务：列出正在执行的任务对象。
> 
> 这是 $engine.lsTask 的中文叫法。

- 返回 : {JsExecuteTask[]} 任务对象列表
- 版本 : 1.6.8


```javascript
var 任务列表 = $engine.罗列任务();
for (var i = 0; i < 任务列表.length; i++) {
    log(任务列表[i]);
}
```


### 有(任务ID)

> 有：判断任务是否还存在。
> 
> 这是 $engine.has 的中文叫法。

- 参数 : 任务ID {字符串} 任务 ID
- 返回 : {布尔值} true 表示任务还在
- 版本 : 1.6.8


```javascript
var 有任务 = $engine.有(任务ID);
if (有任务) {
    $engine.停止(任务ID);
}
```


