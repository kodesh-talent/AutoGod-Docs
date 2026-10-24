# $engine - 脚本引擎

- 更新时间:2026-10-22 10:55:48



### runCode(path, jsCode)

> 直接执行一段脚本代码。
> 
> 第一个参数是这段代码“所在的路径”（用来给脚本定位资源），第二个参数是要跑的代码内容。
> 它会新起一条线程去跑，不阻塞当前页面。

- 参数 : path {String} 这段代码对应的路径（只是个标识，可为空字符串）
- 参数 : jsCode {String} 要执行的脚本代码内容
- 版本 : 1.9.6


```javascript
//直接执行一段打印代码
$engine.runCode("main.js", 'log("你好，世界");');
```


### runJs(jsPath)

> 运行指定路径下的脚本文件。

- 参数 : jsPath {String} 要运行的脚本文件完整路径
- 版本 : 1.9.6


```javascript
//运行 /sdcard/scripts/main.js 这个脚本文件
$engine.runJs("/sdcard/scripts/main.js");
```


### stop()

> 停止当前所有正在运行的脚本。

- 版本 : 1.9.6


```javascript
//一键全部停止
$engine.stop();
```


